---
title: IIS가 있는 Windows에서 ASP.NET Core 호스팅
author: guardrex
description: Windows Server IIS(인터넷 정보 서비스)에서 ASP.NET Core 앱을 호스팅하는 방법을 알아봅니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 03/13/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/iis/index
ms.openlocfilehash: 0cb9bc7d8bf415e5a0125c3798f2430c9e861c98
ms.sourcegitcommit: 43bd79667bbdc8a07bd39fb4cd6f7ad3e70212fb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34729654"
---
# <a name="host-aspnet-core-on-windows-with-iis"></a>IIS가 있는 Windows에서 ASP.NET Core 호스팅

이 문서의 작성자: [Luke Latham](https://github.com/guardrex) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)

## <a name="supported-operating-systems"></a>지원되는 운영 체제

지원되는 운영 체제는 다음과 같습니다.

* Windows 7 이상
* Windows Server 2008 R2 이상

[HTTP.sys 서버](xref:fundamentals/servers/httpsys)(이전의 [WebListener](xref:fundamentals/servers/weblistener))는 IIS를 사용하는 역방향 프록시 구성에서 작동하지 않습니다. [Kestrel 서버](xref:fundamentals/servers/kestrel)를 사용합니다.

## <a name="application-configuration"></a>응용 프로그램 구성

### <a name="enable-the-iisintegration-components"></a>IISIntegration 구성 요소 사용

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

일반적인 *Program.cs*는 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)를 호출하여 호스트 설정을 시작합니다. `CreateDefaultBuilder`는 [Kestrel](xref:fundamentals/servers/kestrel)을 웹 서버로 구성하고 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)의 기본 경로 및 포트를 구성하여 IIS 통합을 구현합니다.

```csharp
public static IWebHost BuildWebHost(string[] args) =>
    WebHost.CreateDefaultBuilder(args)
        ...
```

ASP.NET Core 모듈은 동적 포트를 생성하여 백 엔드 프로세스에 할당합니다. `CreateDefaultBuilder`는 메서드는 동적 포트를 선택하고 `http://localhost:{dynamicPort}/`에서 수신 대기하도록 Kestrel을 구성하는 [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions.useiisintegration) 메서드를 호합니다. 이는 `UseUrls` 또는 [Kestrel의 수신 API](xref:fundamentals/servers/kestrel#endpoint-configuration)에 대한 호출과 같은 다른 URL 구성을 재정의합니다. 따라서 모듈을 사용하는 경우 `UseUrls`에 대한 호출 또는 Kestrel의 `Listen` API가 필요하지 않습니다. `UseUrls` 또는 `Listen`을 호출하는 경우 Kestrel은 IIS 없이 앱을 실행할 때 지정된 포트에서 수신 대기합니다.

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

[Microsoft.AspNetCore.Server.IISIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/) 패키지에 대한 종속성을 앱의 종속성에 포함합니다. [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions.useiisintegration) 확장 메서드를 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder)에 추가하여 IIS 통합 미들웨어를 사용합니다.

```csharp
var host = new WebHostBuilder()
    .UseKestrel()
    .UseIISIntegration()
    ...
```

[UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel) 및 [UseIISIntegration](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions.useiisintegration)이 둘 다 필요합니다. `UseIISIntegration`을 호출하는 코드는 코드 이식성에 영향을 주지 않습니다. 앱이 IIS 배후에서 실행되지 않는 경우(예를 들어 앱이 Kestrel에서 바로 실행되는 경우)에는 `UseIISIntegration`이 작동하지 않습니다.

ASP.NET Core 모듈은 동적 포트를 생성하여 백 엔드 프로세스에 할당합니다. `UseIISIntegration` 메서드는 동적 포트를 선택하고 `http://locahost:{dynamicPort}/`에서 수신 대기하도록 Kestrel을 구성합니다. 이는 `UseUrls`에 대한 호출과 같은 다른 URL 구성을 재정의합니다. 따라서 모듈을 사용하는 경우 `UseUrls`에 대한 호출이 필요하지 않습니다. `UseUrls`를 호출하는 경우 Kestrel은 IIS 없이 앱을 실행할 때 지정된 포트에서 수신 대기합니다.

`UseUrls`를 ASP.NET Core 1.0 앱에서 호출하는 경우 모듈 구성 포트를 덮어 쓰지 않도록 `UseIISIntegration`을 호출하기 **전에** 호출합니다. 모듈 설정이 `UseUrls`를 재정의하기 때문에 이 호출 순서는 ASP.NET Core 1.1에서 필요하지 않습니다.

---

호스팅에 대한 자세한 내용은 [ASP.NET Core의 호스트](xref:fundamentals/host/index)를 참조하세요.

### <a name="iis-options"></a>IIS 옵션

IIS 옵션을 구성하려면 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configureservices)에 [IISOptions](/dotnet/api/microsoft.aspnetcore.builder.iisoptions)에 대한 서비스 구성을 포함합니다. 다음 예제에서는 `HttpContext.Connection.ClientCertificate`를 채우기 위해 클라이언트 인증서를 앱에 전달하는 옵션이 사용하지 않도록 설정되었습니다.

```csharp
services.Configure<IISOptions>(options => 
{
    options.ForwardClientCertificate = false;
});
```

| 옵션                         | 기본 | 설정 |
| ------------------------------ | :-----: | ------- |
| `AutomaticAuthentication`      | `true`  | `true`이면 IIS 통합 미들웨어가 [Windows 인증](xref:security/authentication/windowsauth)에 의해 인증된 `HttpContext.User`를 설정합니다. `false`이면 미들웨어가 `HttpContext.User`에게 ID만 제공하고, `AuthenticationScheme`에서 명시적으로 요청될 때 챌린지에 응답합니다. IIS에서 Windows 인증은 `AutomaticAuthentication`이 작동하기 위해 사용하도록 설정되어야 합니다. 자세한 내용은 [Windows 인증](xref:security/authentication/windowsauth) 항목을 참조하세요. |
| `AuthenticationDisplayName`    | `null`  | 로그인 페이지에서 사용자에게 나타나는 표시 이름을 설정합니다. |
| `ForwardClientCertificate`     | `true`  | `true`면서 `MS-ASPNETCORE-CLIENTCERT` 요청 헤더가 있는 경우 `HttpContext.Connection.ClientCertificate`가 채워집니다. |

### <a name="proxy-server-and-load-balancer-scenarios"></a>프록시 서버 및 부하 분산 장치 시나리오

체계(HTTP/HTTPS) 및 요청이 시작된 원격 IP 주소를 전달하도록 전달된 헤더 미들웨어를 구성하는 IIS 통합 미들웨어 및 ASP.NET Core 모듈을 구성합니다. 추가 프록시 서버 및 부하 분산 장치 외에도 호스팅되는 앱에 추가 구성이 필요할 수 있습니다. 자세한 내용은 [프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)을 참조하세요.

### <a name="webconfig-file"></a>web.config 파일

*web.config* 파일은 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 구성합니다. *web.config* 파일을 만들고, 변하고, 게시하는 작업은 프로젝트를 게시할 때 MSBuild 대상(`_TransformWebConfig`)에 의해 처리됩니다. 이 대상은 웹 SDK 대상(`Microsoft.NET.Sdk.Web`)에 나타납니다. SDK는 프로젝트 파일을 기반으로 해서 설정됩니다.

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">
```

프로젝트에 *web.config* 파일이 없는 경우, [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 구성하기 위해 올바른 *processPath* 및 *인수*로 파일이 생성되어 [게시된 출력](xref:host-and-deploy/directory-structure)으로 이동됩니다.

프로젝트에 *web.config* 파일이 있는 경우, ASP.NET Core 모듈을 구성하기 위해 올바른 *processPath* 및 *인수*로 파일이 변환되어 게시된 출력으로 이동됩니다. 변환은 이 파일의 IIS 구성 설정을 수정하지 않습니다.

*web.config* 파일은 활성 IIS 모듈을 제어하는 추가 IIS 구성 설정을 제공할 수 있습니다. ASP.NET Core 앱을 사용하여 요청을 처리할 수 있는 IIS 모듈에 대한 자세한 내용은 [IIS 모듈](xref:host-and-deploy/iis/modules) 항목을 참조하세요.

웹 SDK가 *web.config* 파일을 변환하지 못하게 하려면 프로젝트 파일의 **\<IsTransformWebConfigDisabled>** 속성을 사용합니다.

```xml
<PropertyGroup>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

웹 SDK가 파일을 변환하지 않도록 설정하는 경우 개발자가 *processPath* 및 *인수*를 수동으로 설정해야 합니다. 자세한 내용은 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)를 참조하세요.

### <a name="webconfig-file-location"></a>web.config 파일 위치

IIS 및 Kestrel 서버 간의 역방향 프록시를 만들려면 배포된 앱의 콘텐츠 루트 경로(일반적으로 앱 기본 경로)에 *web.config* 파일이 있어야 합니다. IIS에 제공되는 웹 사이트 실제 경로와 동일한 위치입니다. 웹 배포를 사용하여 여러 앱을 게시하도록 설정하려면 앱의 루트에 *web.config* 파일이 있어야 합니다.

중요한 파일은 *\<assembly>.runtimeconfig.json*, *\<assembly>.xml*(XML 문서 주석) 및 *\<assembly>.deps.json*과 같은 앱의 실제 경로에 있습니다. *web.config* 파일이 있고 사이트가 정상적으로 시작되면 IIS는 이러한 중요한 파일이 요청되어도 제공하지 않습니다. *web.config* 파일이 없거나, 이름이 잘못 지정되었거나, 정상적으로 시작되도록 사이트를 구성할 수 없는 경우 IIS에서 중요한 파일을 공개적으로 제공할 수도 있습니다.

***web.config* 파일이 항상 배포에 있어야 하며, 올바르게 이름이 지정되고, 정상적으로 시작되도록 사이트를 구성할 수 있어야 합니다. 프로덕션 배포에서 *web.config* 파일을 제거하지 마세요.**

## <a name="iis-configuration"></a>IIS 구성

**Windows Server 운영 체제**

**웹 서버(IIS)** 서버 역할을 사용하도록 설정하고 역할 서비스를 설정합니다.

1. **관리** 메뉴 또는 **서버 관리자**의 링크를 통해 **역할 및 기능 추가** 마법사를 사용합니다. **서버 역할** 단계에서 **웹 서버(IIS)** 확인란을 선택합니다.

   ![서버 역할 선택 단계에서 선택된 웹 서버 IIS 역할](index/_static/server-roles-ws2016.png)

1. **기능** 단계 후에는 웹 서버(IIS)에 대한 **역할 서비스** 단계가 로드됩니다. 원하는 IIS 역할 서비스를 선택하거나 제공된 기본 역할 서비스를 적용합니다.

   ![역할 서비스 선택 단계에서 선택된 기본 역할 서비스](index/_static/role-services-ws2016.png)

   **Windows 인증(선택 사항)**  
   Windows 인증을 사용하도록 설정하려면 **웹 서버** > **보안** 노드를 확장합니다. **Windows 인증** 기능을 선택합니다. 자세한 내용은 [Windows 인증 \<windowsAuthentication>](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/) 및 [Windows 인증 구성](xref:security/authentication/windowsauth)을 참조하세요.

   **WebSockets(선택 사항)**  
   WebSockets는 ASP.NET Core 1.1 이상에서 지원됩니다. WebSockets를 사용하도록 설정하려면 **웹 서버** > **응용 프로그램 개발** 노드를 확장합니다. **WebSocket 프로토콜** 기능을 선택합니다. 자세한 내용은 [WebSocket](xref:fundamentals/websockets)을 참고하시기 바랍니다.

1. **확인** 단계를 진행하여 웹 서버 역할 및 서비스를 설치합니다. **웹 서버(IIS)** 역할을 설치한 후에 서버/IIS를 다시 시작할 필요는 없습니다.

**Windows 데스크톱 운영 체제**

**IIS 관리 콘솔** 및 **World Wide Web 서비스**를 사용하도록 설정합니다.

1. **제어판** > **프로그램** > **프로그램 및 기능** > **Windows 기능 Windows 기능 사용/사용 안 함**(화면 왼쪽)으로 차례로 이동합니다.

1. **인터넷 정보 서비스** 노드를 엽니다. **웹 관리 도구** 노드를 엽니다.

1. **IIS 관리 콘솔** 확인란을 선택합니다.

1. **World Wide Web 서비스** 확인란을 선택합니다.

1. **World Wide Web 서비스**의 기본 기능을 그대로 사용하거나 IIS 기능을 사용자 지정합니다.

   **Windows 인증(선택 사항)**  
   Windows 인증을 사용하도록 설정하려면 **World Wide Web 서비스** > **보안** 노드를 확장합니다. **Windows 인증** 기능을 선택합니다. 자세한 내용은 [Windows 인증 \<windowsAuthentication>](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/) 및 [Windows 인증 구성](xref:security/authentication/windowsauth)을 참조하세요.

   **WebSockets(선택 사항)**  
   WebSockets는 ASP.NET Core 1.1 이상에서 지원됩니다. WebSockets를 사용하도록 설정하려면 **World Wide Web 서비스** > **응용 프로그램 개발 기능** 노드를 확장합니다. **WebSocket 프로토콜** 기능을 선택합니다. 자세한 내용은 [WebSocket](xref:fundamentals/websockets)을 참고하시기 바랍니다.

1. IIS 설치 시 다시 시작해야 하는 경우 시스템을 다시 시작합니다.

![Windows 기능에서 선택된 IIS 관리 콘솔 및 World Wide Web 서비스](index/_static/windows-features-win10.png)

---

## <a name="install-the-net-core-hosting-bundle"></a>.NET Core 호스팅 번들 설치

1. 호스팅 시스템에 *.NET Core 호스팅 번들*을 설치합니다. 번들은 .NET Core 런타임, .NET Core 라이브러리 및 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 설치합니다. 이 모듈은 IIS와 Kestrel 서버 간에 역방향 프록시를 만듭니다. 시스템이 인터넷에 연결되지 않은 경우 [Microsoft Visual C++ 2015 재배포 가능 패키지](https://www.microsoft.com/download/details.aspx?id=53840)를 설치한 후에 .NET Core 호스팅 번들을 설치합니다.

   1. [.NET 모든 다운로드 페이지](https://www.microsoft.com/net/download/all)로 이동합니다.
   1. 테이블의 **런타임** 열에 있는 목록(**X.Y 런타임(vX.Y.Z) 다운로드**)에서 최신 미리 보기 상태가 아닌 .NET Core 런타임을 선택합니다. 최신 런타임에는 **현재** 레이블이 포함됩니다. 미리 보기 소프트웨어로 작업하려는 경우가 아니면 해당 링크 텍스트에서 “미리 보기” 또는 “rc”(릴리스 후보)라는 단어가 있는 런타임을 사용하지 마세요.
   1. .NET Core 런타임 다운로드 페이지의 **Windows**에서 **호스팅 번들 설치 관리자** 링크를 선택하여 *.NET Core 호스팅 번들* 설치 관리자를 다운로드합니다.
   1. 서버에서 설치 관리자를 실행합니다.

   **중요!** IIS 이전에 호스팅 번들이 설치된 경우 번들 설치를 복구해야 합니다. IIS를 설치한 후 호스팅 번들 설치 프로그램을 다시 실행합니다.
   
   설치 관리자가 x64 OS에서 x86 패키지를 설치하지 않도록 방지하려면 `OPT_NO_X86=1` 스위치를 사용하여 관리자 명령 프롬프트에서 설치 관리자를 실행합니다.

1. 시스템을 다시 시작하거나 명령 프롬프트에서 **net stop was /y**, **net start w3svc**를 차례로 실행합니다. IIS를 다시 시작하면 설치 관리자에 의한 시스템 PATH 변경 내용이 수집됩니다.

> [!NOTE]
> IIS 공유 구성에 대한 자세한 내용은 [IIS 공유 구성을 사용하는 ASP.NET Core 모듈](xref:host-and-deploy/aspnet-core-module#aspnet-core-module-with-an-iis-shared-configuration)을 참조하세요.

## <a name="install-web-deploy-when-publishing-with-visual-studio"></a>Visual Studio을 사용하여 게시할 때 웹 배포 설치

[웹 배포](/iis/publish/using-web-deploy/introduction-to-web-deploy)를 사용하여 앱을 서버에 배포하는 경우 최신 버전의 웹 배포를 서버에 설치합니다. 웹 배포를 설치하려면 [WebPI(웹 플랫폼 설치 관리자)](https://www.microsoft.com/web/downloads/platform.aspx)를 사용하거나 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=43717)에서 직접 설치 관리자를 가져옵니다. WebPI를 사용하는 것이 좋습니다. WebPI는 호스팅 공급자에 대한 독립 실행형 설치 및 구성을 제공합니다.

## <a name="create-the-iis-site"></a>IIS 사이트 만들기

1. 호스팅 시스템에서 앱의 게시된 폴더 및 파일을 포함할 폴더를 만듭니다. 앱의 배포 레이아웃은 [디렉터리 구조](xref:host-and-deploy/directory-structure) 항목에서 설명합니다.

1. stdout 로깅을 사용하도록 설정할 경우 ASP.NET Core 모듈 stdout 로그를 보관할 *logs* 폴더를 새 폴더 안에 만듭니다. 앱이 페이로드에서 *logs* 폴더로 배포되는 경우 이 단계를 건너뜁니다. 로컬에서 프로젝트가 빌드될 때 MSBuild에서 *logs* 폴더를 자동으로 만들도록 설정하는 방법에 대한 지침은 [디렉터리 구조](xref:host-and-deploy/directory-structure) 항목을 참조하세요.

   > [!IMPORTANT]
   > stdout 로그는 앱 시작 오류의 문제 해결 용도로만 사용해야 합니다. 일상적인 앱 로깅에는 stdout 로깅을 사용하지 마세요. 로그 파일 크기 또는 생성되는 로그 파일 수에 대한 제한은 없습니다. 앱 풀에는 로그가 기록될 위치에 쓰기 권한이 있어야 합니다. 로그 위치에 대한 해당 경로에 있는 모든 폴더가 있어야 합니다. stdout 로그에 대한 자세한 내용은 [로그 생성 및 리디렉션](xref:host-and-deploy/aspnet-core-module#log-creation-and-redirection)을 참조하세요. ASP.NET Core 앱의 로깅에 대한 자세한 내용은 [로깅](xref:fundamentals/logging/index) 항목을 참조하세요.

1. **IIS 관리자**의 **연결** 패널에서 서버 노드를 엽니다. **사이트** 폴더를 마우스 오른쪽 단추로 클릭합니다. 상황에 맞는 메뉴에서 **웹 사이트 추가**를 선택합니다.

1. **사이트 이름**을 제공하고 **실제 경로**를 앱의 배포 폴더로 설정합니다. **바인딩** 구성을 제공하고 **확인**을 선택하여 웹 사이트를 만듭니다.

   ![[웹 사이트 추가] 단계에서 사이트 이름, 실제 경로 및 호스트 이름을 제공합니다.](index/_static/add-website-ws2016.png)

   > [!WARNING]
   > 최상위 와일드카드 바인딩(`http://*:80/` 및 `http://+:80`)을 사용하지 **않아야** 합니다. 최상위 와일드카드 바인딩은 보안 취약점에 앱을 노출시킬 수 있습니다. 강력한 와일드카드와 약한 와일드카드 모두에 적용됩니다. 와일드카드보다는 명시적 호스트 이름을 사용합니다. 전체 부모 도메인을 제어하는 경우 하위 도메인 와일드카드 바인딩(예: `*.mysub.com`)에는 이러한 보안 위험이 없습니다(취약한 `*.com`과 반대임). 자세한 내용은 [rfc7230 섹션-5.4](https://tools.ietf.org/html/rfc7230#section-5.4)를 참조하세요.

1. 서버 노드에서 **응용 프로그램 풀**을 선택합니다.

1. 사이트의 앱 풀을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **기본 설정**을 선택합니다.

1. **응용 프로그램 풀 편집** 창에서 **.NET CLR 버전**을 **관리 코드 없음**으로 설정합니다.

   ![.NET CLR 버전에 대해 관리 코드 없음 설정](index/_static/edit-apppool-ws2016.png)

    ASP.NET Core는 별도의 프로세스에서 실행되며 런타임을 관리합니다. ASP.NET Core에서는 데스크톱 CLR을 로드할 필요가 없습니다. **.NET CLR 버전**을 **관리 코드 없음**으로 설정하는 것은 선택 사항입니다.

1. 프로세스 모델 ID에 적절한 권한이 있는지 확인합니다.

   응용 프로그램 풀의 기본 ID(**프로세스 모델** > **ID**)가 **ApplicationPoolIdentity**에서 다른 ID로 변경되면, 새 ID에 앱의 폴더, 데이터베이스 및 기타 필요한 리소스에 액세스하는 데 필요한 권한이 있는지 확인합니다. 예를 들어 앱 풀에는 앱이 파일을 읽고 쓰는 폴더에 대한 읽기 및 쓰기 권한이 필요합니다.

**Windows 인증 구성(선택 사항)**  
자세한 내용은 [Windows 인증 구성](xref:security/authentication/windowsauth)을 참조하세요.

## <a name="deploy-the-app"></a>앱 배포

호스팅 시스템에 만든 폴더에 앱을 배포합니다. [웹 배포](/iis/publish/using-web-deploy/introduction-to-web-deploy)는 배포에 권장되는 메커니즘입니다.

### <a name="web-deploy-with-visual-studio"></a>Visual Studio를 사용한 웹 배포

웹 배포에서 사용할 게시 프로필을 만드는 방법은 [ASP.NET Core 앱 배포용 Visual Studio 게시 프로필](xref:host-and-deploy/visual-studio-publish-profiles#publish-profiles) 항목을 참조하세요. 호스팅 공급자가 게시 프로필을 제공하거나 게시 프로필을 만들 수 있도록 지원하는 경우 해당 프로필을 다운로드하고 Visual Studio **게시** 대화 상자를 사용하여 가져옵니다.

![게시 대화 상자 페이지](index/_static/pub-dialog.png)

### <a name="web-deploy-outside-of-visual-studio"></a>Visual Studio 외부에서 웹 배포

[웹 배포](/iis/publish/using-web-deploy/introduction-to-web-deploy)는 Visual Studio 외부에서 명령줄을 통해 사용할 수도 있습니다. 자세한 내용은 [웹 배포 도구](/iis/publish/using-web-deploy/use-the-web-deployment-tool)를 참조하세요.

### <a name="alternatives-to-web-deploy"></a>웹 배포에 대한 대안

수동 복사, Xcopy, Robocopy, PowerShell 등의 여러 방법 중 하나를 사용하여 앱을 호스팅 시스템으로 이동합니다.

IIS에 ASP.NET Core 배포에 대한 자세한 내용은 [IIS 관리자를 위한 배포 리소스](#deployment-resources-for-iis-administrators) 섹션을 참조하세요.

## <a name="browse-the-website"></a>웹 사이트 찾아보기

![IIS 시작 페이지가 로드된 Microsoft Edge 브라우저](index/_static/browsewebsite.png)

## <a name="locked-deployment-files"></a>배포 파일이 잠겨 있음

앱이 실행 중이면 배포 폴더의 파일이 잠겨 있습니다. 잠긴 파일은 배포 중에 덮어쓸 수 없습니다. 배포에서 잠긴 파일을 해제하려면 다음 방법 중 **하나**를 사용하여 앱 풀을 중지합니다.

* 웹 배포를 사용하고 프로젝트 파일에서 `Microsoft.NET.Sdk.Web`을 참조합니다. *app_offline.htm* 파일은 웹앱 디렉터리의 루트에 배치됩니다. 파일이 있는 경우 ASP.NET Core 모듈은 앱을 정상적으로 종료하고, 배포하는 동안 *app_offline.htm* 파일을 제공합니다. 자세한 내용은 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module#app_offlinehtm)를 참조하세요.
* 서버의 IIS 관리자에서 앱 풀을 수동으로 중지합니다.
* PowerShell을 사용하여 응용 프로그램 풀을 중지하고 다시 시작합니다(PowerShell 5 이상 필요).

  ```PowerShell
  $webAppPoolName = 'APP_POOL_NAME'

  # Stop the AppPool
  if((Get-WebAppPoolState $webAppPoolName).Value -ne 'Stopped') {
      Stop-WebAppPool -Name $webAppPoolName
      while((Get-WebAppPoolState $webAppPoolName).Value -ne 'Stopped') {
          Start-Sleep -s 1
      }
      Write-Host `-AppPool Stopped
  }

  # Provide script commands here to deploy the app

  # Restart the AppPool
  if((Get-WebAppPoolState $webAppPoolName).Value -ne 'Started') {
      Start-WebAppPool -Name $webAppPoolName
      while((Get-WebAppPoolState $webAppPoolName).Value -ne 'Started') {
          Start-Sleep -s 1
      }
      Write-Host `-AppPool Started
  }
  ```

## <a name="data-protection"></a>데이터 보호

[ASP.NET Core 데이터 보호 스택](xref:security/data-protection/index)은 인증에 사용되는 미들웨어를 포함하여 여러 ASP.NET Core [미들웨어](xref:fundamentals/middleware/index)에서 사용됩니다. 사용자 코드에서 데이터 보호 API가 호출되지 않더라도 배포 스크립트 또는 사용자 코드를 통해 영구적 암호화 [키 저장소](xref:security/data-protection/implementation/key-management)를 만들도록 데이터 보호를 구성해야 합니다. 데이터 보호를 구성하지 않으면 키는 메모리에 보관되고 앱이 다시 시작되면 삭제됩니다.

키 링이 메모리에 저장된 경우 앱을 다시 시작하면 다음과 같이 됩니다.

* 모든 쿠키 기반 인증 토큰이 무효화됩니다. 
* 사용자는 다음 요청에서 다시 로그인해야 합니다. 
* 키 링으로 보호된 데이터의 암호를 더 이상 해독할 수 없습니다. 여기에는 [CSRF 토큰](xref:security/anti-request-forgery#aspnet-core-antiforgery-configuration) 및 [ASP.NET Core MVC TempData 쿠키](xref:fundamentals/app-state#tempdata)가 포함될 수 있습니다.

IIS에서 키 링을 저장하도록 데이터 보호를 구성하려면 다음 방법 중 **하나**를 사용합니다.

* **데이터 보호 레지스트리키 만들기**

  ASP.NET 앱에서 사용되는 데이터 보호 키는 앱 외부의 레지스트리에 저장됩니다. 지정된 앱의 키를 저장하려면 앱 풀에 대한 레지스트리 키를 만듭니다.

  WebFarm이 아닌 독립 실행형 IIS 설치의 경우 [Data Protection Provision-AutoGenKeys.ps1 PowerShell 스크립트](https://github.com/aspnet/DataProtection/blob/dev/Provision-AutoGenKeys.ps1)를 ASP.NET Core 앱과 함께 사용되는 각 응용 프로그램 풀에 사용할 수 있습니다. 이 스크립트는 앱의 앱 풀 작업자 프로세스 계정만 액세스할 수 있는 HKLM 레지스트리에 레지스트리 키를 만듭니다. 미사용 키는 컴퓨터 전체 키가 있는 DPAPI를 사용하여 암호화됩니다.

  웹 팜 시나리오에서는 UNC 경로를 사용하여 데이터 보호 키 링을 저장하도록 앱을 구성할 수 있습니다. 기본적으로 데이터 보호 키는 암호화되지 않습니다. 네트워크 공유에 대한 파일 권한은 앱 실행에 사용되는 Windows 계정으로 제한되어야 합니다. X509 인증서를 사용하여 미사용 키를 보호할 수도 있습니다. 사용자가 인증서를 업로드할 수 있는 메커니즘을 사용하는 것이 좋습니다. 즉 사용자의 신뢰할 수 있는 인증서 저장소에 인증서를 배치하고, 사용자의 앱이 실행되는 모든 컴퓨터에서 이 인증서를 사용할 수 있도록 합니다. 자세한 내용은 [ASP.NET Core 데이터 보호 구성](xref:security/data-protection/configuration/overview)을 참조하세요.

* **사용자 프로필을 로드하도록 IIS 응용 프로그램 풀 구성**

  이 설정은 앱 풀에 대한 **고급 설정** 아래의 **프로세스 모델** 섹션에 있습니다. 사용자 프로필 로드를 `True`로 설정합니다. 이렇게 하면 사용자 프로필 디렉터리 아래에 키가 저장되고, 앱 풀에서 사용되는 사용자 계정과 관련된 키로 DPAPI를 사용하여 키가 보호됩니다.

* **파일 시스템을 키 링 저장소로 사용**

  [파일 시스템을 키 링 저장소로 사용](xref:security/data-protection/configuration/overview)하도록 앱 코드를 조정합니다. X509 인증서를 사용하여 키 링을 보호하고 신뢰할 수 있는 인증서인지 확인합니다. 자체 서명된 인증서인 경우 신뢰할 수 있는 루트 저장소에 배치합니다.

  웹 팜에서 IIS를 사용하는 경우 다음을 수행합니다.

  * 모든 컴퓨터에서 액세스할 수 있는 파일 공유를 사용합니다.
  * 각 시스템에 X509 인증서를 배포합니다. [코드에 데이터 보호](xref:security/data-protection/configuration/overview)를 구성합니다.

* **데이터 보호에 대한 컴퓨터 수준 정책 설정**

  데이터 보호 시스템은 데이터 보호 API를 사용하는 모든 앱에 대한 기본 [컴퓨터 수준 정책](xref:security/data-protection/configuration/machine-wide-policy) 설정을 제한적으로 지원합니다. 자세한 내용은 [데이터 보호 문서](xref:security/data-protection/index)를 참조하세요.

## <a name="sub-application-configuration"></a>하위 응용 프로그램 구성

루트 앱 아래에 추가된 하위 앱에는 ASP.NET Core 모듈이 처리기로 포함되지 않아야 합니다. 하위 앱의 *web.config* 파일에 모듈이 처리기로 추가되면, 하위 앱을 찾으려고 할 때 잘못된 구성 파일을 참조하는 *500.19 내부 서버 오류*가 표시됩니다.

다음 예제에서는 ASP.NET Core 하위 앱에 대해 게시된 *web.config* 파일을 보여 줍니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <aspNetCore processPath="dotnet" 
      arguments=".\<assembly_name>.dll" 
      stdoutLogEnabled="false" 
      stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

ASP.NET Core 앱 아래에 비ASP .NET Core 하위 앱을 호스팅하는 경우, 하위 앱의 *web.config* 파일에서 상속된 처리기를 명시적으로 제거합니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <remove name="aspNetCore" />
    </handlers>
    <aspNetCore processPath="dotnet" 
      arguments=".\<assembly_name>.dll" 
      stdoutLogEnabled="false" 
      stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

ASP.NET Core 모듈을 구성하는 방법에 대한 자세한 내용은 [ASP.NET Core 모듈 소개](xref:fundamentals/servers/aspnet-core-module) 항목 및 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)를 참조하세요.

## <a name="configuration-of-iis-with-webconfig"></a>web.config를 사용하여 IIS 구성

IIS 구성은 역방향 프록시 구성에 적용되는 IIS 기능에 대한 *web.config*에 포함된 **\<system.webServer>** 섹션의 영향을 받습니다. IIS가 서버 수준에서 동적 압축을 사용하도록 구성된 경우 앱의 *web.config* 파일에 있는 **\<urlCompression>** 요소를 통해 사용하지 않도록 설정할 수 있습니다.

자세한 내용은 [\<system.webServer>에 대한 구성 참조](/iis/configuration/system.webServer/), [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module) 및 [ASP.NET Core와 IIS 모듈](xref:host-and-deploy/iis/modules)을 참조하세요. 격리된 앱 풀에서 실행되는 개별 앱에 대해 환경 변수를 설정하려면(IIS 10.0 이상에서 지원됨), IIS 참조 문서에서 [환경 변수 \<environmentVariables>](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) 항목의 *AppCmd.exe 명령* 섹션을 참조하세요.

## <a name="configuration-sections-of-webconfig"></a>web.config 구성 섹션

*web.config*에 있는 ASP.NET 4.x 앱의 구성 섹션은 ASP.NET Core 앱의 구성에 사용되지 않습니다.

* **\<system.web>**
* **\<appSettings>**
* **\<connectionStrings>**
* **\<location>**

ASP.NET Core 앱은 다른 구성 공급자를 사용하여 구성됩니다. 자세한 내용은 [구성](xref:fundamentals/configuration/index)을 참고하시기 바랍니다.

## <a name="application-pools"></a>응용 프로그램 풀

서버에서 여러 웹 사이트를 호스트하는 경우 각 앱을 해당 앱 풀에서 실행하여 서로 격리합니다. 이 구성은 IIS **웹 사이트 추가** 대화 상자의 기본값입니다. **사이트 이름**을 제공하면 해당 텍스트가 자동으로 **응용 프로그램 풀** 텍스트 상자로 전송됩니다. 사이트를 추가할 때 이 사이트 이름을 사용하여 새로운 앱 풀이 생성됩니다.

## <a name="application-pool-identity"></a>응용 프로그램 풀 ID

응용 프로그램 풀 ID 계정을 사용하면 도메인 또는 로컬 계정을 만들고 관리할 필요 없이 고유한 계정으로 앱을 실행할 수 있습니다. IIS 8.0 이상에서 IIS WAS(관리 작업자 프로세스)는 새로운 앱 풀의 이름으로 가상 계정을 만들고, 기본적으로 이 계정으로 앱 풀의 작업자 프로세스를 실행합니다. IIS 관리 콘솔의 응용 프로그램 풀에 대한 **고급 설정** 아래에서 **ID**가 **ApplicationPoolIdentity**를 사용하도록 설정되어 있는지 확인합니다.

![응용 프로그램 풀 고급 설정 대화 상자](index/_static/apppool-identity.png)

IIS 관리 프로세스는 Windows 보안 시스템에 앱 풀 이름이 포함된 보안 식별자를 만듭니다. 리소스는 이 ID를 사용하여 보호할 수 있습니다. 그러나 이 ID는 실제 사용자 계정이 아니며 Windows 사용자 관리 콘솔에 표시되지 않습니다.

IIS 작업자 프로세스에서 앱에 대한 높은 액세스 권한이 필요한 경우 앱이 포함된 디렉터리에 대한 ACL(액세스 제어 목록)을 수정합니다.

1. [Windows 탐색기]를 열고 해당 하위 디렉터리로 이동합니다.

1. 디렉터리를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.

1. **보안** 탭 아래에서 **편집** 단추, **추가** 단추를 차례로 선택합니다.

1. **위치** 단추를 선택하고 시스템이 선택되어 있는지 확인합니다.

1. **선택할 개체 이름 입력** 영역에 **IIS AppPool\\<app_pool_name>** 을 입력합니다. **이름 확인** 단추를 선택합니다. *DefaultAppPool*의 경우 **IIS AppPool\DefaultAppPool**을 사용하는 이름을 확인합니다. **이름 확인** 단추를 선택하면 개체 이름 영역에 **DefaultAppPool** 값이 표시됩니다. 개체 이름 영역에 앱 풀 이름을 직접 입력할 수는 없습니다. 개체 이름을 확인할 때는 **IIS AppPool\\<app_pool_name>** 형식을 사용합니다.

   ![앱 폴더에 대한 사용자 또는 그룹 대화 상자 선택: “이름 확인”을 선택하기 전에 개체 이름 영역의 “IIS AppPool\"에 앱 풀 이름 “DefaultAppPool”이 추가됩니다.](index/_static/select-users-or-groups-1.png)

1. **확인**을 선택합니다.

   ![앱 폴더에 대한 사용자 또는 그룹 대화 상자 선택: “이름 확인”을 선택하면 개체 이름 영역에 개체 이름 “DefaultAppPool”이 표시됩니다.](index/_static/select-users-or-groups-2.png)

1. 읽기 및 실행 권한은 기본적으로 부여됩니다. 필요에 따라 추가 권한을 제공합니다.

**ICACLS** 도구를 사용하여 명령 프롬프트에서 액세스 권한을 부여할 수도 있습니다. *DefaultAppPool*을 예로 들면, 다음 명령이 사용됩니다.

```console
ICACLS C:\sites\MyWebApp /grant "IIS AppPool\DefaultAppPool":F
```

자세한 내용은 [icacls](/windows-server/administration/windows-commands/icacls) 항목을 참조하세요.

## <a name="deployment-resources-for-iis-administrators"></a>IIS 관리자를 위한 배포 리소스

IIS 설명서에서 IIS에 대해 자세히 알아보세요.  
[IIS 설명서](/iis)

.NET Core 앱 배포 모델에 자세히 알아보세요.  
[.NET Core 응용 프로그램 배포](/dotnet/core/deploying/)

ASP.NET Core 모듈이 Kestrel 웹 서버에서 역방향 프록시 서버로 IIS 또는 IIS Express를 어떻게 사용하도록 허용하는지 알아봅니다.  
[ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)

ASP.NET Core 앱을 호스팅하기 위해 ASP.NET Core 모듈을 구성하는 방법을 알아봅니다.  
[ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)

게시된 ASP.NET Core 앱의 디렉터리 구조에 대해 알아봅니다.  
[디렉터리 구조](xref:host-and-deploy/directory-structure)

ASP.NET Core 앱용 활성 및 비활성 IIS 모듈과 IIS 모듈을 관리하는 방법을 살펴봅니다.  
[IIS 모듈](xref:host-and-deploy/iis/troubleshoot)

ASP.NET Core 앱의 IIS 배포에 대한 문제 진단 방법을 알아봅니다.  
[문제 해결](xref:host-and-deploy/iis/troubleshoot)

IIS에서 ASP.NET Core 앱을 호스팅할 때 일반적인 오류를 구분합니다.  
[Azure App Service 및 IIS에 대한 일반적인 오류 참조](xref:host-and-deploy/azure-iis-errors-reference)

## <a name="additional-resources"></a>추가 자료

* [ASP.NET Core 소개](xref:index)
* [공식 Microsoft IIS 사이트](https://www.iis.net/)
* [Windows Server 기술 콘텐츠 라이브러리](/windows-server/windows-server)
