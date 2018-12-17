---
title: ASP.NET Core에서 WebListener 웹 서버 구현
author: guardrex
description: IIS 없이 인터넷에 직접 연결하는 데 사용할 수 있는 Windows의 ASP.NET Core용 웹 서버인 WebListener에 대해 알아봅니다.
monikerRange: < aspnetcore-2.0
ms.author: riande
ms.custom: mvc
ms.date: 10/24/2018
uid: fundamentals/servers/weblistener
ms.openlocfilehash: 92a2e567e968cce59ba7b6f374ebd4bc189b81ee
ms.sourcegitcommit: 9bb58d7c8dad4bbd03419bcc183d027667fefa20
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/04/2018
ms.locfileid: "52862124"
---
# <a name="weblistener-web-server-implementation-in-aspnet-core"></a>ASP.NET Core에서 WebListener 웹 서버 구현

작성자: [Tom Dykstra](https://github.com/tdykstra) 및 [Chris Ross](https://github.com/Tratcher)

> [!NOTE]
> 이 주제는 ASP.NET Core 1.x에만 적용됩니다. ASP.NET Core 2.0에서는 WebListener의 이름이 [HTTP.sys](httpsys.md)입니다.

WebListener는 Windows에서만 실행되는 [ASP.NET Core에 대한 웹 서버](index.md)입니다. [Http.Sys 커널 모드 드라이버](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)를 기반으로 합니다. WebListener는 역방향 프록시 서버로 IIS를 사용하지 않고 인터넷에 대한 직접 연결에 사용될 수 있는 [Kestrel](kestrel.md)에 대한 대안입니다. 사실상 **WebListener는 [ASP.NET Core 모듈](aspnet-core-module.md)과 호환되지 않으므로 IIS 또는 IIS Express와 함께 사용될 수 없습니다.**

WebListener는 ASP.NET Core에 대해 개발되었지만 [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/) NuGet 패키지를 통해 모든 .NET Core 또는 .NET Framework 응용 프로그램에서 직접 사용할 수 있습니다.

WebListener는 다음과 같은 기능을 지원합니다.

- [Windows 인증](xref:security/authentication/windowsauth)
- 포트 공유
- SNI를 사용하는 HTTPS
- TLS를 통한 HTTP/2(Windows 10)
- 직접 파일 전송
- 응답 캐싱
- WebSockets(Windows 8)

지원되는 Windows 버전:

- Windows 7 및 Windows Server 2008 R2 이상

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/weblistener/sample) ([다운로드 방법](xref:index#how-to-download-a-sample))

## <a name="when-to-use-weblistener"></a>WebListener를 사용하는 경우

WebListener는 IIS를 사용하지 않고 인터넷에 서버를 직접 노출해야 하는 배포에 유용합니다.

![WebListener는 인터넷과 직접 통신합니다.](weblistener/_static/weblistener-to-internet.png)

Http.Sys를 기반으로 하기 때문에 WebListener는 공격으로부터 보호하기 위한 역방향 프록시 서버가 필요하지 않습니다. Http.Sys는 많은 유형의 공격으로부터 보호하고 모든 기능을 갖춘 웹 서버의 견고성, 보안 및 확장성을 제공하는 완성도 높은 기술입니다. IIS 자체는 Http.Sys 위에 HTTP 수신기로 실행됩니다.

WebListener는 Kestrel을 사용하여 가져올 수 없는 제공하는 기능 중 하나가 필요할 때 내부 배포에 대한 적합한 선택이기도 합니다.

![WebListener는 내부 네트워크와 직접 통신합니다.](weblistener/_static/weblistener-to-internal.png)

## <a name="kernel-mode-authentication-with-kerberos"></a>Kerberos를 사용하여 커널 모드 인증

WebListener는 Kerberos 인증 프로토콜을 사용하여 커널 모드 인증에 위임합니다. 사용자 모드 인증은 Kerberos 및 WebListener로 지원되지 않습니다. 머신 계정은 Active Directory에서 가져온 Kerberos 토큰/티켓의 암호를 해독하는 데 사용되고 사용자를 인증하는 서버에 클라이언트에 의해 전달되어야 합니다. 앱의 사용자가 아닌 호스트에 대해 SPN(서비스 사용자 이름)을 등록합니다.

## <a name="how-to-use-weblistener"></a>WebListener 사용 방법

호스트 OS 및 ASP.NET Core 응용 프로그램에 대한 설치 작업의 개요는 다음과 같습니다.

### <a name="configure-windows-server"></a>Windows Server 구성

* [.NET Core](https://download.microsoft.com/download/0/A/3/0A372822-205D-4A86-BFA7-084D2CBE9EDF/DotNetCore.1.0.1-SDK.1.0.0.Preview2-003133-x64.exe) 또는 .NET Framework 4.5.1과 같은 응용 프로그램에 필요한 .NET 버전을 설치합니다.

* WebListener에 대해 바인딩하고 SSL 인증서를 설정하도록 URL 접두사 미리 등록

   Windows에서 URL 접두사를 미리 등록하지 않는 경우 관리자 권한으로 응용 프로그램을 실행해야 합니다. 유일한 예외는 1024보다 큰 포트 번호로 HTTP(HTTPS 아님)를 사용하여 로컬 호스트에 바인딩하는 경우이며 이 경우 관리자 권한이 필요하지 않습니다.

   자세한 내용은 이 문서의 뒷부분에 나오는 [접두사 미리 등록 및 SSL 구성 방법](#preregister-url-prefixes-and-configure-ssl)을 참조하세요.

* 방화벽 포트를 열어 WebListener에 도달하는 트래픽을 허용합니다.

   netsh.exe 또는 [PowerShell cmdlet](https://technet.microsoft.com/library/jj554906)을 사용할 수 있습니다.

[Http.Sys 레지스트리 설정](https://support.microsoft.com/kb/820129)도 있습니다.

### <a name="configure-your-aspnet-core-application"></a>ASP.NET Core 응용 프로그램 구성

* NuGet 패키지 [Microsoft.AspNetCore.Server.WebListener](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.WebListener/)를 설치합니다. 종속성으로 [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/)도 설치합니다.

* 다음 예제와 같이 필요한 WebListener [옵션](https://github.com/aspnet/HttpSysServer/blob/rel/1.1.2/src/Microsoft.AspNetCore.Server.WebListener/WebListenerOptions.cs) 및 [설정](https://github.com/aspnet/HttpSysServer/blob/rel/1.1.2/src/Microsoft.Net.Http.Server/WebListenerSettings.cs)을 지정하여 `Main` 메서드에서 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)의 `UseWebListener` 확장 메서드를 호출합니다.

  [!code-csharp[](weblistener/sample/Program.cs?name=snippet_Main&highlight=13-17)]

* 수신 대기하는 URL 및 포트 구성 

  기본적으로 ASP.NET Core는 `http://localhost:5000`으로 바인딩합니다. URL 접두사와 포트를 구성하기 위해 `UseURLs` 확장 메서드, `urls` 명령줄 인수 또는 ASP.NET Core 구성 시스템을 사용할 수 있습니다. 자세한 내용은 [ASP.NET Core의 호스트](xref:fundamentals/host/index)를 참조하세요.

  웹 수신기는 [Http.Sys 접두사 문자열 형식](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)을 사용합니다. WebListener와 관련된 접두사 문자열 형식 요구 사항이 없습니다.

  > [!WARNING]
  > 최상위 와일드카드 바인딩(`http://*:80/` 및 `http://+:80`)을 사용하지 **않아야** 합니다. 최상위 와일드카드 바인딩은 보안 취약점에 앱을 노출시킬 수 있습니다. 강력한 와일드카드와 약한 와일드카드 모두에 적용됩니다. 와일드카드보다는 명시적 호스트 이름을 사용합니다. 전체 부모 도메인을 제어하는 경우 하위 도메인 와일드카드 바인딩(예: `*.mysub.com`)에는 이러한 보안 위험이 없습니다(취약한 `*.com`과 반대임). 자세한 내용은 [rfc7230 섹션-5.4](https://tools.ietf.org/html/rfc7230#section-5.4)를 참조하세요.

  > [!NOTE]
  > 서버에서 미리 등록한 동일한 접두사 문자열을 `UseUrls`에 지정해야 합니다. 

* 응용 프로그램은 IIS 또는 IIS Express를 실행하도록 구성되지 않았습니다.

  Visual Studio에서 기본 실행 프로필은 IIS Express용입니다.  콘솔 응용 프로그램으로 프로젝트를 실행하려면 다음 스크린샷에 표시된 것처럼 수동으로 선택한 프로필을 변경해야 합니다.

  ![콘솔 앱 프로필 선택](weblistener/_static/vs-choose-profile.png)

## <a name="how-to-use-weblistener-outside-of-aspnet-core"></a>ASP.NET Core 외부에서 WebListener를 사용하는 방법

* [Microsoft.Net.Http.Server](https://www.nuget.org/packages/Microsoft.Net.Http.Server/) NuGet 패키지를 설치합니다.

* ASP.NET Core에서 사용을 위해 수행하는 것처럼 [WebListener에 대해 바인딩하고 SSL 인증서를 설정하도록 URL 접두사 미리 등록합니다](#preregister-url-prefixes-and-configure-ssl).

[Http.Sys 레지스트리 설정](https://support.microsoft.com/kb/820129)도 있습니다.


ASP.NET Core 외부에서 WebListener 사용을 보여 주는 코드 샘플은 다음과 같습니다.

```csharp
var settings = new WebListenerSettings();
settings.UrlPrefixes.Add("http://localhost:8080");

using (WebListener listener = new WebListener(settings))
{
    listener.Start();

    while (true)
    {
        var context = await listener.AcceptAsync();
        byte[] bytes = Encoding.ASCII.GetBytes("Hello World: " + DateTime.Now);
        context.Response.ContentLength = bytes.Length;
        context.Response.ContentType = "text/plain";

        await context.Response.Body.WriteAsync(bytes, 0, bytes.Length);
        context.Dispose();
    }
}
```

## <a name="preregister-url-prefixes-and-configure-ssl"></a>URL 접두사 미리 등록 및 SSL 구성

IIS와 WebListener는 기본 Http.Sys 커널 모드 드라이버를 사용하여 요청을 수신하고 초기 처리를 수행합니다. IIS에서 관리 UI는 모든 항목을 구성하는 상대적으로 쉬운 방법을 제공합니다. 그러나 WebListener를 사용하는 경우 Http.Sys를 직접 구성해야 합니다. 작업 수행을 위한 기본 도구는 netsh.exe입니다. 

netsh.exe를 사용해야 하는 가장 일반적인 작업은 URL 접두사 예약 및 SSL 인증서 할당입니다.

NetSh.exe는 초보자가 사용하기에 편리한 도구가 아닙니다. 다음 예제에서는 포트 80 및 443에 대해 URL 접두사를 예약하는 데 필요한 최소한의 것을 보여 줍니다.

```console
netsh http add urlacl url=http://+:80/ user=Users
netsh http add urlacl url=https://+:443/ user=Users
```

다음 예제에서는 SSL 인증서를 할당하는 방법을 보여 줍니다.

```console
netsh http add sslcert ipport=0.0.0.0:443 certhash=MyCertHash_Here appid="{00000000-0000-0000-0000-000000000000}".
```

다음은 공식 참조 설명서입니다.

* [HTTP(Hypertext Transfer Protocol)에 대한 Netsh 명령](https://technet.microsoft.com/library/cc725882.aspx)
* [UrlPrefix 문자열](https://msdn.microsoft.com/library/windows/desktop/aa364698.aspx)

다음 리소스는 여러 시나리오에 대한 자세한 지침을 제공합니다. `HttpListener`를 참조하는 문서는 모두 Http.Sys를 기반으로 하므로 `WebListener`에 동일하게 적용됩니다.

* [방법: SSL 인증서로 포트 구성](/dotnet/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate)
* [HTTPS 통신 - HttpListener 기반 호스팅 및 클라이언트 인증](http://sunshaking.blogspot.com/2012/11/https-communication-httplistener-based.html) 이는 타사 블로그이며 비교적 오래됐지만 여전히 유용한 정보가 있습니다.
* [방법: SSL 단순 서버로 HttpListener 또는 Http 서버 안전하지 않은 코드(C++)를 사용하는 연습](https://blogs.msdn.microsoft.com/jpsanders/2009/09/29/how-to-walkthrough-using-httplistener-or-http-server-unmanaged-code-c-as-an-ssl-simple-server/) 유용한 정보가 있는 오래된 블로그입니다.
* [SSL로 .NET Core WebListener를 어떻게 설정하나요?](https://blogs.msdn.microsoft.com/timomta/2016/11/04/how-do-i-set-up-a-net-core-weblistener-with-ssl/)

다음은 netsh.exe 명령줄보다 쉽게 사용할 수 있는 몇 가지 타사 도구입니다. 이러한 도구는 Microsoft에서 제공되거나 보증되지 않습니다. netsh.exe 자체는 관리자 권한이 필요하므로 도구는 기본적으로 관리자 권한으로 실행됩니다.

* [http.sys 관리자](http://httpsysmanager.codeplex.com/)는 SSL 인증서 및 옵션, 접두사 예약 및 인증서 신뢰 목록의 나열 및 구성을 위한 UI를 제공합니다. 
* [HttpConfig](http://www.stevestechspot.com/ABetterHttpcfg.aspx)를 통해 SSL 인증서와 URL 접두사를 나열하거나 구성할 수 있습니다. UI는 http.sys 관리자보다 성능이 우수하며 몇 가지 추가 구성 옵션을 노출하지만 그렇지 않은 경우 유사한 기능을 제공합니다. 새 CTL(인증서 신뢰 목록)을 만들 수 없지만 기존 것을 할당할 수 있습니다.

자체 서명된 SSL 인증서를 생성하기 위해 Microsoft는 명령줄 도구: [MakeCert.exe](https://msdn.microsoft.com/library/windows/desktop/aa386968) 및 PowerShell cmdlet [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pki/new-selfsignedcertificate)를 제공합니다. 자체 서명된 SSL 인증서를 쉽게 생성하도록 하는 타사 UI 도구도 있습니다.

* [SelfCert](https://www.pluralsight.com/blog/software-development/selfcert-create-a-self-signed-certificate-interactively-gui-or-programmatically-in-net)
* [Makecert UI](http://makecertui.codeplex.com/)

## <a name="next-steps"></a>다음 단계

자세한 내용은 다음 리소스를 참조하세요.

* [이 문서에 대한 샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/weblistener/sample)
* [WebListener 소스 코드](https://github.com/aspnet/HttpSysServer/)
* [호스팅](xref:fundamentals/host/index)
