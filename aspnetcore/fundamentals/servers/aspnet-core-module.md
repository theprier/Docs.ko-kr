---
title: "ASP.NET Core 모듈"
author: tdykstra
description: "Kestrel 웹 서버에서 역방향 프록시 서버로 IIS 또는 IIS Express를 사용하도록 하는 ANCM(ASP.NET Core 모듈), IIS 모듈을 소개합니다."
manager: wpickett
ms.author: tdykstra
ms.custom: H1Hack27Feb2017
ms.date: 08/03/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/servers/aspnet-core-module
ms.openlocfilehash: 4337bc42c5454d6a9634a396d9c89f3518af148b
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="introduction-to-aspnet-core-module"></a>ASP.NET Core 모듈 소개

작성자: [Tom Dykstra](https://github.com/tdykstra), [Rick Strahl](https://github.com/RickStrahl) 및 [Chris Ross](https://github.com/Tratcher) 

ANCM(ASP.NET Core 모듈)을 사용하면 능숙한 것(보안, 관리 효율성 및 기타 등등)에 대해 IIS를 사용하고, 능숙한 것(굉장히 빠름)에 대해 [Kestrel](kestrel.md)을 사용하고, 두 기술에서 한 번에 이점을 얻어 IIS 뒤에서 ASP.NET Core 응용 프로그램을 실행할 수 있습니다. **ANCM은 Kestrel과만 작동하며 WebListener(ASP.NET Core 1.x에서) 또는 HTTP.sys(2.x에서)와 호환되지 않습니다.** 

지원되는 Windows 버전:

* Windows 7 및 Windows Server 2008 R2 이상

[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/aspnet-core-module/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="what-aspnet-core-module-does"></a>ASP.NET Core 모듈에서 수행하는 작업

ANCM은 IIS 파이프라인으로 후크하고 백 엔드 ASP.NET Core 응용 프로그램으로 트래픽을 리디렉션하는 네이티브 IIS 모듈입니다. Windows 인증과 같은 다른 대부분의 모듈은 여전히 실행할 기회를 갖습니다. ANCM은 요청에 대해 처리기가 선택되고 응용 프로그램 *web.config* 파일에서 처리기 매핑이 정의되는 경우에만 제어권을 갖습니다.

ASP.NET Core 응용 프로그램은 IIS 작업자 프로세스와 별도의 프로세스에서 실행되므로 ANCM은 프로세스 관리도 수행합니다. ANCM은 첫 번째 요청이 들어올 때 ASP.NET Core 응용 프로그램에 대한 프로세스를 시작하고 충돌할 때 다시 시작합니다. 이는 IIS에서 In Process를 실행하고 WAS(Windows Activation Service)에 의해 관리되는 클래식 ASP.NET 응용 프로그램과 기본적으로 동일한 동작입니다.

다음은 IIS, ANCM 및 ASP.NET Core 응용 프로그램 간의 관계를 보여 주는 다이어그램입니다.

![ASP.NET Core 모듈](aspnet-core-module/_static/ancm.png)

요청은 웹에서 들어오며 기본 포트(80) 또는 SSL 포트(443)에서 IIS로 라우팅하는 커널 모드 Http.Sys 드라이버를 적중합니다. ANCM은 포트 80/443이 아닌 응용 프로그램에 대해 구성된 HTTP 포트에서 ASP.NET Core 응용 프로그램에 요청을 전달합니다.

Kestrel은 ANCM에서 들어오는 트래픽을 수신 대기합니다.  ANCM은 시작 시 환경 변수를 통해 포트를 지정하고 [UseIISIntegration](#call-useiisintegration) 메서드는 `http://localhost:{port}`에서 수신하도록 서버를 구성합니다. ANCM에서 오지 않는 요청을 거부하는 추가 검사가 있습니다. (ANCM은 HTTPS 전달을 지원하지 않으므로 HTTPS를 통해 IIS에서 수신하는 경우에도 요청은 HTTP를 통해 전달됩니다.)

Kestrel은 ANCM의 요청을 선택하고 ASP.NET Core 미들웨어 파이프라인으로 푸시합니다. 그러면 이를 처리하고 `HttpContext` 인스턴스로 응용 프로그램 논리로 전달합니다. 응용 프로그램의 응답은 요청을 시작한 HTTP 클라이언트에 다시 푸시하는 IIS로 다시 전달됩니다.

ANCM에는 몇 가지 다른 기능도 있습니다.

* 환경 변수를 설정합니다.
* 파일 저장소에 `stdout` 출력을 기록합니다.
* Windows 인증 토큰을 전달합니다.

## <a name="how-to-use-ancm-in-aspnet-core-apps"></a>ASP.NET Core 앱에서 ANCM을 사용하는 방법

이 섹션에서는 IIS 서버 및 ASP.NET Core 응용 프로그램 설정에 대한 프로세스의 개요를 제공합니다. 자세한 지침은 [IIS를 사용하여 Windows에서 호스트](xref:host-and-deploy/iis/index)를 참조하세요.

### <a name="install-ancm"></a>ANCM 설치


ASP.NET Core 모듈은 서버의 IIS 및 개발 컴퓨터의 IIS Express에 설치되어야 합니다. 서버의 경우 ANCM은 [.NET Core Windows Server 호스팅 번들](https://aka.ms/dotnetcore-2-windowshosting)에 포함됩니다. 개발 컴퓨터의 경우 컴퓨터에 이미 설치되었으면 Visual Studio는 IIS Express 및 IIS에 ANCM을 자동으로 설치합니다.

### <a name="install-the-iisintegration-nuget-package"></a>IISIntegration NuGet 패키지 설치

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

[Microsoft.AspNetCore.Server.IISIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/) 패키지는 ASP.NET Core 메타패키지([Microsoft.AspNetCore](https://www.nuget.org/packages/Microsoft.AspNetCore/) 및 [Microsoft.AspNetCore.All](xref:fundamentals/metapackage))에 포함됩니다. 메타패키지 중 하나를 사용하지 않는 경우 `Microsoft.AspNetCore.Server.IISIntegration`을 별도로 설치합니다. `IISIntegration` 패키지는 앱을 설정하는 ANCM에 의해 브로드캐스팅되는 환경 변수를 읽는 상호 운용성 팩입니다. 환경 변수는 수신 대기하는 포트와 같은 구성 정보를 제공합니다. 

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

응용 프로그램에서 [Microsoft.AspNetCore.Server.IISIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/)을 설치합니다. `IISIntegration` 패키지는 앱을 설정하는 ANCM에 의해 브로드캐스팅되는 환경 변수를 읽는 상호 운용성 팩입니다. 환경 변수는 수신 대기하는 포트와 같은 구성 정보를 제공합니다. 

---

### <a name="call-useiisintegration"></a>UseIISIntegration 호출

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

[`WebHostBuilder`](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilder)의 `UseIISIntegration` 확장 메서드는 IIS를 사용하여 실행하는 경우 자동으로 호출됩니다.

ASP.NET Core 메타패키지 중 하나를 사용하고 있지 않으며 `Microsoft.AspNetCore.Server.IISIntegration` 패키지를 설치하지 않은 경우 런타임 오류가 발생합니다. `UseIISIntegration`을 명시적으로 호출하는 경우 패키지가 설치되지 않으면 컴파일 시간 오류가 발생합니다.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

응용 프로그램의 `Main` 메서드에서 [`WebHostBuilder`](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilder)의 `UseIISIntegration` 확장 메서드를 호출합니다. 

[!code-csharp[](aspnet-core-module/sample/Program.cs?name=snippet_Main&highlight=12)]

---

`UseIISIntegration` 메서드는 ANCM에서 설정하는 환경 변수를 찾으며 발견되지 않는 경우 작동하지 않습니다. 이 동작은 macOS 또는 Linux에서 개발 및 테스트, IIS를 실행하는 서버에 배포와 같은 시나리오를 용이하게 합니다. macOS 또는 Linux에서 실행되는 동안 Kestrel은 웹 서버 역할을 하지만 앱이 IIS 환경에 배포될 때 자동으로 ANCM 및 IIS를 사용합니다.

### <a name="ancm-port-binding-overrides-other-port-bindings"></a>ANCM 포트 바인딩은 다른 포트 바인딩을 재정의합니다

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

ANCM은 동적 포트를 생성하여 백 엔드 프로세스에 할당합니다. `UseIISIntegration` 메서드는 이 동적 포트를 선택하고 `http://locahost:{dynamicPort}/`에서 수신 대기하도록 Kestrel을 구성합니다. 이는 `UseUrls` 또는 [Kestrel의 수신 API](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration)에 대한 호출과 같은 다른 URL 구성을 재정의합니다. 따라서 ANCM을 사용하는 경우 `UseUrls` 또는 Kestrel의 `Listen` API를 호출할 필요가 없습니다. `UseUrls` 또는 `Listen`을 호출하는 경우 Kestrel은 IIS 없이 앱을 실행할 때 지정하는 포트에서 수신 대기합니다.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

ANCM은 동적 포트를 생성하여 백 엔드 프로세스에 할당합니다. `UseIISIntegration` 메서드는 이 동적 포트를 선택하고 `http://locahost:{dynamicPort}/`에서 수신 대기하도록 Kestrel을 구성합니다. 이는 `UseUrls`에 대한 호출과 같은 다른 URL 구성을 재정의합니다. 따라서 ANCM을 사용하는 경우 `UseUrls`를 호출할 필요가 없습니다. `UseUrls`를 호출하는 경우 Kestrel은 IIS 없이 앱을 실행할 때 지정하는 포트에서 수신 대기합니다.

ASP.NET Core 1.0에서 `UseUrls`를 호출하는 경우 ANCM 구성된 포트가 덮어쓰지 않도록 `UseIISIntegration`을 호출하기 **전에** 호출합니다. ANCM 설정은 `UseUrls`를 재정의하므로 이 호출 순서는 ASP.NET Core 1.1에서는 필요하지 않습니다.

---

### <a name="configure-ancm-options-in-webconfig"></a>Web.config에서 ANCM 옵션 구성

ASP.NET Core 모듈에 대한 구성은 응용 프로그램의 루트 폴더에 있는 *web.config* 파일에 저장됩니다. 이 파일의 설정은 시작 명령 및 ASP.NET Core 앱을 시작하는 인수를 가리킵니다. 샘플 *web.config* 코드 및 구성 옵션에 대한 지침은 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)를 참조하세요.

### <a name="run-with-iis-express-in-development"></a>개발에서 IIS Express로 실행

IIS Express는 ASP.NET Core 템플릿에 의해 정의된 기본 프로필을 사용하여 Visual Studio에서 실행할 수 있습니다.

## <a name="proxy-configuration-uses-http-protocol-and-a-pairing-token"></a>프록시 구성은 HTTP 프로토콜 및 페어링 토큰을 사용합니다.

ANCM과 Kestrel 사이에서 만든 프록시는 HTTP 프로토콜을 사용합니다. HTTP 사용은 ANCM과 Kestrel 간의 트래픽이 네트워크 인터페이스에서 분리된 루프백 주소에서 발생하는 성능 최적화입니다. 서버에서 분리된 위치에서 ANCM과 Kestrel 간 트래픽 도청의 위험은 없습니다.

페어링 토큰은 Kestrel에서 받은 요청이 IIS에서 프록시되었으며 다른 원본에서 오지 않았다는 것을 보장하는 데 사용됩니다. 페어링 토큰은 ANCM에 의해 생성되며 환경 변수(`ASPNETCORE_TOKEN`)로 설정됩니다. 페어링 토큰은 프록시된 모든 요청에서 헤더(`MSAspNetCoreToken`)로도 설정됩니다. IIS 미들웨어는 수신하는 각 요청을 검사하여 페어링 토큰 헤더 값이 환경 변수 값과 일치하는지 확인합니다. 토큰 값이 일치하지 않는 경우 요청이 기록되고 거부됩니다. 페어링 토큰 환경 변수와 ANCM과 Kestrel 간의 트래픽은 서버에서 분리된 위치에서 액세스할 수 없습니다. 페어링 토큰 값을 알지 못하면 공격자는 IIS 미들웨어에서 검사를 무시하는 요청을 전송할 수 없습니다.

## <a name="next-steps"></a>다음 단계

자세한 내용은 다음 리소스를 참조하세요.

* [이 문서에 대한 샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/aspnet-core-module/sample)
* [ASP.NET Core 모듈 원본 코드](https://github.com/aspnet/AspNetCoreModule)
* [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)
* [IIS를 사용하여 Windows에서 호스트](xref:host-and-deploy/iis/index)
