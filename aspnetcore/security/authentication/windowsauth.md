---
title: ASP.NET Core에서 Windows 인증을 구성 합니다.
author: scottaddie
description: ASP.NET core에서 IIS Express, IIS 및 HTTP.sys를 사용 하 여 Windows 인증을 구성 하는 방법에 알아봅니다.
ms.author: riande
ms.custom: mvc, seodec18
ms.date: 12/18/2018
uid: security/authentication/windowsauth
ms.openlocfilehash: 94dff2f47b2b076cb15f8d385239179b52786678
ms.sourcegitcommit: 816f39e852a8f453e8682081871a31bc66db153a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2018
ms.locfileid: "53637822"
---
# <a name="configure-windows-authentication-in-aspnet-core"></a>ASP.NET Core에서 Windows 인증을 구성 합니다.

작성자: [Steve Smith](https://ardalis.com) 및 [Scott Addie](https://twitter.com/Scott_Addie)

IIS를 사용 하 여 호스팅되는 ASP.NET Core 앱에 대 한 Windows 인증을 구성할 수 있습니다 또는 [HTTP.sys](xref:fundamentals/servers/httpsys)합니다.

## <a name="windows-authentication"></a>Windows 인증

Windows 인증은 ASP.NET Core 앱의 사용자를 인증 하는 운영 체제에서 사용 합니다. 서버에 다른 Windows 계정 또는 Active Directory 도메인 id를 사용 하 여 사용자를 식별 하는 회사 네트워크에서 실행 될 때 Windows 인증을 사용할 수 있습니다. Windows 인증 사용자, 클라이언트 응용 프로그램 및 웹 서버는 동일한 Windows 도메인에 속해 인트라넷 환경에 가장 적합 합니다.

[Windows 인증에 자세히 알아보기 및 IIS에 대 한 설치](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/)합니다.

## <a name="enable-windows-authentication-in-an-aspnet-core-app"></a>ASP.NET Core 앱에서 Windows 인증을 사용 하도록 설정

Visual Studio 웹 응용 프로그램 템플릿은 Windows 인증을 지원 하도록 구성할 수 있습니다.

### <a name="use-the-windows-authentication-app-template"></a>Windows 인증 앱 템플릿 사용

Visual Studio에서 다음을 수행합니다.

1. 새 ASP.NET Core 웹 응용 프로그램을 만듭니다.
1. 템플릿 목록에서 웹 응용 프로그램을 선택 합니다.
1. 선택 된 **인증 변경** 단추를 선택 **Windows 인증**합니다.

앱을 실행합니다. 위쪽에 표시 되는 사용자 앱의 오른쪽입니다.

![Windows 인증에 대 한 브라우저 스크린 샷](windowsauth/_static/browser-screenshot.png)

IIS Express를 사용 하 여 개발 작업에 대 한 템플릿을 Windows 인증을 사용 하는 데 필요한 모든 구성을 제공 합니다. 다음 섹션에는 Windows 인증에 대 한 ASP.NET Core 앱을 수동으로 구성 하는 방법을 보여 줍니다.

### <a name="visual-studio-settings-for-windows-and-anonymous-authentication"></a>Windows 및 익명 인증을 위해 visual Studio 설정

Visual Studio 프로젝트 **속성** 페이지의 **디버그** 탭은 Windows 인증 및 익명 인증에 대 한 확인란을 제공 합니다.

![강조 표시 하는 인증 옵션을 사용 하 여 Windows 인증 브라우저 스크린 샷](windowsauth/_static/vs-auth-property-menu.png)

이러한 두 속성을 구성할 수 있습니다 또는 합니다 *launchSettings.json* 파일:

[!code-json[](windowsauth/sample/launchSettings.json?highlight=3-4)]

## <a name="enable-windows-authentication-with-iis"></a>IIS 사용 하 여 Windows 인증을 사용 하도록 설정

IIS에서 사용 하 여 [ASP.NET Core 모듈](xref:host-and-deploy/aspnet-core-module) ASP.NET Core 앱을 호스트 하 합니다. Windows 인증은 응용 프로그램이 아닌 IIS에서 구성 됩니다. 다음 섹션에서는 IIS 관리자를 사용 하 여 Windows 인증을 사용 하도록 ASP.NET Core 앱을 구성 하는 방법을 보여 줍니다.

### <a name="iis-configuration"></a>IIS 구성

Windows 인증을 위해 IIS 역할 서비스를 사용 하도록 설정 합니다. 자세한 내용은 [IIS 역할 서비스 (2 단계 참조)에서 Windows 인증 사용](xref:host-and-deploy/iis/index#iis-configuration)합니다.

IIS 통합 미들웨어는 기본적으로 자동으로 요청을 인증 하도록 구성 됩니다. 자세한 내용은 참조 하세요. [IIS 사용 하 여 Windows에서 ASP.NET Core 호스팅. IIS 옵션 (AutomaticAuthentication)](xref:host-and-deploy/iis/index#iis-options)합니다.

ASP.NET Core 모듈은 기본적으로 앱에 Windows 인증 토큰을 전달 하도록 구성 됩니다. 자세한 내용은 참조 하세요. [ASP.NET Core 모듈 구성 참조: AspNetCore 요소의 특성](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element)합니다.

### <a name="create-a-new-iis-site"></a>새 IIS 사이트 만들기

이름 및 폴더를 지정 하 고 새 응용 프로그램 풀을 만들 수 있도록 합니다.

### <a name="customize-authentication"></a>인증을 사용자 지정

사이트에 대 한 인증 기능을 엽니다.

![IIS 인증 메뉴](windowsauth/_static/iis-authentication-menu.png)

익명 인증을 사용 하지 않도록 설정 하 고 Windows 인증을 사용 하도록 설정 합니다.

![IIS 인증 설정](windowsauth/_static/iis-auth-settings.png)

### <a name="publish-your-project-to-the-iis-site-folder"></a>IIS 사이트 폴더에 프로젝트 게시

대상 폴더에 앱을 게시 Visual Studio 또는.NET Core CLI를 사용 합니다.

![Visual Studio 게시 대화 상자](windowsauth/_static/vs-publish-app.png)

에 대해 자세히 알아보세요 [IIS에 게시](xref:host-and-deploy/iis/index)합니다.

Windows 인증이 작동을 확인 하려면 앱을 시작 합니다.

## <a name="enable-windows-authentication-with-httpsys"></a>HTTP.sys 사용 하 여 Windows 인증을 사용 하도록 설정

Kestrel은 Windows 인증을 지원 하지 않지만 사용할 수 있습니다 [HTTP.sys](xref:fundamentals/servers/httpsys) Windows에서 자체 호스팅된 시나리오를 지원 합니다. 다음 예제에서는 Windows 인증을 사용 하 여 HTTP.sys를 사용 하도록 앱의 웹 호스트를 구성 합니다.

[!code-csharp[](windowsauth/sample/Program2x.cs?highlight=9-14)]

> [!NOTE]
> HTTP.sys는 Kerberos 인증 프로토콜을 사용하여 커널 모드 인증에 위임합니다. 사용자 모드 인증은 Kerberos 및 HTTP.sys로 지원되지 않습니다. 머신 계정은 Active Directory에서 가져온 Kerberos 토큰/티켓의 암호를 해독하는 데 사용되고 사용자를 인증하는 서버에 클라이언트에 의해 전달되어야 합니다. 앱의 사용자가 아닌 호스트에 대해 SPN(서비스 사용자 이름)을 등록합니다.

> [!NOTE]
> HTTP.sys는 Nano Server 버전 1709 이상에서 지원 되지 않습니다. Nano Server를 사용 하 여 Windows 인증 및 HTTP.sys를 사용 하려면 사용 된 [Server Core (microsoft/windowsservercore) 컨테이너](https://hub.docker.com/r/microsoft/windowsservercore/)합니다. Server Core에 대 한 자세한 내용은 참조 하세요. [Windows Server의 Server Core 설치 옵션 이란?](/windows-server/administration/server-core/what-is-server-core)합니다.

## <a name="work-with-windows-authentication"></a>Windows 인증 사용

익명 액세스 구성 상태는 방식을 결정 합니다 `[Authorize]` 및 `[AllowAnonymous]` 특성은 앱에서 사용 합니다. 다음 두 섹션에는 익명 액세스는 허용 되지 않는 및 허용 된 구성 상태를 처리 하는 방법을 설명 합니다.

### <a name="disallow-anonymous-access"></a>익명 액세스 허용 안 함

Windows 인증을 사용 하 고 익명 액세스가 비활성화 되어는 `[Authorize]` 고 `[AllowAnonymous]` 특성은 효과가 없습니다. IIS 사이트 (또는 HTTP.sys)를 익명 액세스를 허용 하도록 구성 하는 경우 요청에 하지 앱에 도달 합니다. 이러한 이유로 `[AllowAnonymous]` 특성 적용 되지 않습니다.

### <a name="allow-anonymous-access"></a>익명 액세스 허용

Windows 인증 및 익명 액세스를 모두 설정 된 경우 사용 합니다 `[Authorize]` 및 `[AllowAnonymous]` 특성입니다. `[Authorize]` 특성을 사용 하면 Windows 인증 필요 실제로 앱의 부분을 보호할 수 있습니다. 합니다 `[AllowAnonymous]` 재정의 특성 `[Authorize]` 특성 익명 액세스를 허용 하는 앱 내에서 사용 합니다. 참조 [단순 권한 부여](xref:security/authorization/simple) 자세한 특성 사용.

ASP.NET Core에서 2.x의 경우는 `[Authorize]` 특성 추가 구성이 필요 *Startup.cs* Windows 인증에 대 한 익명 요청 수입니다. 권장된 구성에 사용 중인 웹 서버에 따라 약간씩 달라 집니다.

> [!NOTE]
> 기본적으로 권한 부여를 페이지에 액세스할 수 없는 사용자는 빈 HTTP 403 응답으로 표시 됩니다. 합니다 [StatusCodePages 미들웨어](xref:fundamentals/error-handling#configure-status-code-pages) "액세스 거부" 더 나은 환경을 제공 하기 위해 구성할 수 있습니다.

#### <a name="iis"></a>IIS

IIS를 사용 하는 경우 다음을 추가 하 여 `ConfigureServices` 메서드:

```csharp
// IISDefaults requires the following import:
// using Microsoft.AspNetCore.Server.IISIntegration;
services.AddAuthentication(IISDefaults.AuthenticationScheme);
```

#### <a name="httpsys"></a>HTTP.sys

HTTP.sys를 사용 하는 경우 다음을 추가 하 여 `ConfigureServices` 메서드:

```csharp
// HttpSysDefaults requires the following import:
// using Microsoft.AspNetCore.Server.HttpSys;
services.AddAuthentication(HttpSysDefaults.AuthenticationScheme);
```

### <a name="impersonation"></a>가장

Asp.net 가장을 구현 하지 않습니다. 앱 풀 또는 프로세스 id를 사용 하 여 모든 요청에 대해 응용 프로그램 id를 사용 하 여 앱이 실행 됩니다. 사용 하 여 명시적으로 사용자를 대신 하 여 작업을 수행 해야 할 경우 `WindowsIdentity.RunImpersonated`합니다. 이 컨텍스트에서 단일 작업을 실행 하 고 컨텍스트를 닫습니다.

[!code-csharp[](windowsauth/sample/Startup.cs?name=snippet_Impersonate&highlight=10-18)]

`RunImpersonated` 비동기 작업을 지원 하지 않으며 복잡 한 시나리오에 사용할 수 없습니다. 예를 들어 전체 요청 또는 미들웨어 체인 래핑 지원 없거나 것이 좋습니다.
