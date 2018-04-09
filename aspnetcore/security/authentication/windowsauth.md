---
title: ASP.NET Core에 Windows 인증을 구성 합니다.
author: ardalis
description: 이 문서에서는 IIS Express, IIS, HTTP.sys 및 WebListener를 사용 하 여 ASP.NET Core에 Windows 인증을 구성 하는 방법을 설명 합니다.
manager: wpickett
ms.author: riande
ms.date: 10/24/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authentication/windowsauth
ms.openlocfilehash: ff47519db4e9d1c5aea8811fef24c84bb564e80e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="configure-windows-authentication-in-aspnet-core"></a>ASP.NET Core에 Windows 인증을 구성 합니다.

작성자: [Steve Smith](https://ardalis.com) 및 [Scott Addie](https://twitter.com/Scott_Addie)

Iis에서 호스팅되는 ASP.NET Core 응용 프로그램에 대 한 Windows 인증을 구성할 수 있습니다 [HTTP.sys](xref:fundamentals/servers/httpsys), 또는 [WebListener](xref:fundamentals/servers/weblistener)합니다.

## <a name="what-is-windows-authentication"></a>Windows 인증 이란?

ASP.NET Core 응용 프로그램의 사용자를 인증 하는 운영 체제는 Windows 인증 사용 합니다. 서버에 다른 Windows 계정 또는 Active Directory 도메인 id를 사용 하 여 사용자를 식별 하는 회사 네트워크에서 실행 될 때 Windows 인증을 사용할 수 있습니다. Windows 인증은 사용자, 클라이언트 응용 프로그램 및 웹 서버는 동일한 Windows 도메인에 속해 인트라넷 환경에 가장 적합 합니다.

[Windows 인증 및 iis 설치에 대 한 자세한](https://docs.microsoft.com/iis/configuration/system.webServer/security/authentication/windowsAuthentication/)합니다.

## <a name="enable-windows-authentication-in-an-aspnet-core-app"></a>ASP.NET Core 응용 프로그램에서 Windows 인증을 사용 하도록 설정

Visual Studio 웹 응용 프로그램 템플릿은 Windows 인증을 지원 하도록 구성할 수 있습니다.

### <a name="use-the-windows-authentication-app-template"></a>Windows 인증 앱 템플릿을 사용 하 여

Visual Studio에서 합니다.
1. 새 ASP.NET Core 웹 응용 프로그램을 만듭니다. 
1. 템플릿 목록에서 웹 응용 프로그램을 선택 합니다.
1. 선택 된 **인증 변경** 선택한 단추 **Windows 인증**합니다. 

앱을 실행합니다. 사용자 이름 상단에 표시 됩니다. 응용 프로그램의 오른쪽입니다.

![Windows 인증에 대 한 브라우저 스크린 샷](windowsauth/_static/browser-screenshot.png)

IIS Express를 사용 하 여 개발 작업에서는 서식 파일에 Windows 인증을 사용 하는 데 필요한 모든 구성을 제공 합니다. 다음 섹션에는 Windows 인증에 대 한 ASP.NET Core 응용 프로그램을 수동으로 구성 하는 방법을 보여 줍니다.

### <a name="visual-studio-settings-for-windows-and-anonymous-authentication"></a>Windows 및 익명 인증에 대 한 visual Studio 설정

Visual Studio 프로젝트 **속성** 페이지의 **디버그** 탭은 Windows 인증 및 익명 인증에 대 한 확인란을 제공 합니다.

![Windows 인증에 대 한 브라우저 스크린 샷](windowsauth/_static/vs-auth-property-menu.png)

이러한 두 속성을 구성할 수 있습니다 또는 *launchSettings.json* 파일:

[!code-json[](windowsauth/sample/launchSettings.json?highlight=3-4)]

## <a name="enable-windows-authentication-with-iis"></a>Iis Windows 인증을 사용 하도록 설정

IIS에서 사용 하는 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module) ASP.NET Core 응용 프로그램 호스트에 있습니다. 모듈 흐름 Windows 인증을 IIS에 기본적으로입니다. Iis에서 응용 프로그램이 아닌 Windows 인증이 구성 됩니다. 다음 섹션에서는 Windows 인증을 사용 하도록 ASP.NET Core 응용 프로그램을 구성 하려면 IIS 관리자를 사용 하는 방법을 보여 줍니다.

### <a name="create-a-new-iis-site"></a>새 IIS 사이트 만들기

이름 및 폴더를 지정 하 고 새 응용 프로그램 풀을 만들 수 있도록 허용 합니다.

### <a name="customize-authentication"></a>인증을 사용자 지정

사이트에 대 한 인증 메뉴를 엽니다.

![IIS 인증 메뉴](windowsauth/_static/iis-authentication-menu.png)

익명 인증을 사용 하지 않도록 설정 하 고 Windows 인증을 사용 하도록 설정 합니다.

![IIS 인증 설정](windowsauth/_static/iis-auth-settings.png)

### <a name="publish-your-project-to-the-iis-site-folder"></a>IIS 사이트 폴더에 프로젝트를 게시 합니다.

Visual Studio 또는.NET Core CLI를 사용 하 여 대상 폴더에 응용 프로그램을 게시 합니다.

![Visual Studio 게시 대화 상자](windowsauth/_static/vs-publish-app.png)

에 대 한 자세한 내용은 [를 IIS에 게시](xref:host-and-deploy/iis/index)합니다.

Windows 인증 작동 확인 응용 프로그램을 실행 합니다.

## <a name="enable-windows-authentication-with-httpsys-or-weblistener"></a>HTTP.sys 또는 WebListener와 함께 Windows 인증을 사용 하도록 설정

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)
Kestrel Windows 인증을 지원 하지 않지만 사용할 수 있습니다 [HTTP.sys](xref:fundamentals/servers/httpsys) Windows에서 자체 호스팅된 시나리오를 지원 합니다. 다음 예제에서는 Windows 인증과 함께 HTTP.sys를 사용 하도록 응용 프로그램의 웹 호스트를 구성 합니다.

[!code-csharp[](windowsauth/sample/Program2x.cs?highlight=9-14)]

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)
Kestrel Windows 인증을 지원 하지 않지만 사용할 수 있습니다 [WebListener](xref:fundamentals/servers/weblistener) Windows에서 자체 호스팅된 시나리오를 지원 합니다. 다음 예제에서는 Windows 인증과 함께 WebListener를 사용 하도록 응용 프로그램의 웹 호스트를 구성 합니다.

[!code-csharp[](windowsauth/sample/Program1x.cs?highlight=6-11)]

* * *
## <a name="work-with-windows-authentication"></a>Windows 인증 사용

구성 상태에 대 한 익명 액세스 결정 되는 방식으로 `[Authorize]` 및 `[AllowAnonymous]` 특성이 앱에서 사용 됩니다. 다음 두 섹션에서는 익명 액세스의 허용 되 고 허용 되지 않는 구성 상태를 처리 하는 방법을 설명 합니다.

### <a name="disallow-anonymous-access"></a>익명 액세스 허용 안 함

Windows 인증을 사용 하 고 익명 액세스를 비활성화 하는 경우는 `[Authorize]` 및 `[AllowAnonymous]` 특성은 효과가 없습니다. IIS 사이트 (또는 HTTP.sys 또는 WebListener 서버)에 익명 액세스를 허용 하도록 구성 된, 경우 요청에 결코 응용 프로그램에 도달 합니다. 이러한 이유로 `[AllowAnonymous]` 특성은 적용 되지 않습니다.

### <a name="allow-anonymous-access"></a>익명 액세스 허용

사용 하 여 Windows 인증 및 익명 액세스를 모두 설정 된 경우는 `[Authorize]` 및 `[AllowAnonymous]` 특성입니다. `[Authorize]` 특성을 사용 하면 Windows 인증 필요 진정으로 응용 프로그램의 부분을 보호할 수 있습니다. `[AllowAnonymous]` 특성 재정의 `[Authorize]` 특성 익명 액세스를 허용 하는 앱 내에서 사용 합니다. 참조 [간단한 인증](xref:security/authorization/simple) 특성 사용 정보에 대 한 합니다.

ASP.NET Core에서 2.x는 `[Authorize]` 특성 추가 구성이 필요 *Startup.cs* Windows 인증에 대 한 익명 요청을 보도록 하기 위해서입니다. 권장된 구성을 사용 하 고 웹 서버에 따라 약간 다릅니다.

> [!NOTE]
> 기본적으로 빈 403 HTTP 응답을 페이지에 액세스할 수 있는 권한 부족 한 사용자 표시 됩니다. [StatusCodePages 미들웨어](xref:fundamentals/error-handling#configuring-status-code-pages) "액세스 거부" 더 나은 환경을 제공 하기 위해 구성할 수 있습니다.

#### <a name="iis"></a>IIS

IIS를 사용 하는 경우 다음을 추가 `ConfigureServices` 메서드: 

```csharp
// IISDefaults requires the following import:
// using Microsoft.AspNetCore.Server.IISIntegration;
services.AddAuthentication(IISDefaults.AuthenticationScheme);
```

#### <a name="httpsys"></a>HTTP.sys

HTTP.sys를 사용 하는 경우 다음을 추가 `ConfigureServices` 메서드:

```csharp
// HttpSysDefaults requires the following import:
// using Microsoft.AspNetCore.Server.HttpSys;
services.AddAuthentication(HttpSysDefaults.AuthenticationScheme);
```

### <a name="impersonation"></a>가장

ASP.NET Core 가장을 구현 하지 않습니다. 앱에 대 한 모든 요청을 응용 프로그램 풀 또는 프로세스 id를 사용 하 여 응용 프로그램 id로 실행 됩니다. 사용 하 여 명시적으로 사용자를 대신 하 여 작업을 수행 해야 할 경우 `WindowsIdentity.RunImpersonated`합니다. 이 컨텍스트에서 단일 작업을 실행 하 고 컨텍스트를 닫습니다.

[!code-csharp[](windowsauth/sample/Startup.cs?name=snippet_Impersonate&highlight=10-18)]

`RunImpersonated` 비동기 작업을 지원 하지 않으므로 하 고 복잡 한 시나리오에 사용할 수 없습니다. 예를 들어 전체 요청 또는 미들웨어 체인 래핑 지원 아니거나 것이 좋습니다.

---
