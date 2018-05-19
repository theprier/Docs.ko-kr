---
title: ASP.NET Core용 Visual Studio의 개발 시간 IIS 지원
author: shirhatti
description: Windows Server에서 IIS 뒤에서 실행 하는 경우 ASP.NET Core 응용 프로그램 디버깅에 대 한 지원이 검색 합니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 05/14/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/iis/development-time-iis-support
ms.openlocfilehash: 0bf4585d44e61c5e7e5b89ce9d8dfdfa10d5460e
ms.sourcegitcommit: a66f38071e13685bbe59d48d22aa141ac702b432
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
---
# <a name="development-time-iis-support-in-visual-studio-for-aspnet-core"></a>ASP.NET Core용 Visual Studio의 개발 시간 IIS 지원

여 [Sourabh Shirhatti](https://twitter.com/sshirhatti) 및 [Luke Latham](https://github.com/guardrex)

이 문서에서는 설명 [Visual Studio](https://www.visualstudio.com/vs/) Windows 서버에서 IIS 뒤에서 실행 되는 ASP.NET Core 응용 프로그램 디버깅에 대 한 지원. 이 항목에서는이 기능을 사용 하도록 설정 하 고 프로젝트를 설정 합니다.

## <a name="prerequisites"></a>전제 조건

[!INCLUDE[](~/includes/net-core-prereqs-windows.md)]

## <a name="enable-iis"></a>IIS 활성화

1. **제어판** > **프로그램** > **프로그램 및 기능** > **Windows 기능 Windows 기능 사용/사용 안 함**(화면 왼쪽)으로 차례로 이동합니다.
1. 선택 된 **인터넷 정보 서비스** 확인란 합니다.

![Windows 기능 보여 주는 인터넷 정보 서비스 확인란을 선택한 IIS 기능 중 일부는 사용할 수 있음을 나타내는 검은색 사각형 (하지: 확인 표시)으로](development-time-iis-support/_static/enable_iis.png)

IIS 설치는 시스템 다시 시작을 해야 합니다.

## <a name="configure-iis"></a>IIS 구성

IIS 웹 사이트를 다음으로 구성 되어 있어야 합니다.

* 응용 프로그램의 실행 프로필 URL 호스트 이름과 일치 하는 호스트 이름입니다.
* 할당 된 인증서로 포트 443에 대 한 바인딩입니다.

예를 들어는 **호스트 이름** 에서 추가 된 웹 사이트 ("실행 프로필은 또한 localhost" 사용이 항목의 뒷부분에 나오는) "localhost"으로 설정 되어 있습니다. 포트는 "443" (HTTPS)로 설정 됩니다. **IIS Express 개발 인증서** works는 웹 사이트 이지만 유효한 모든 인증서에 할당 됩니다.

![할당 된 인증서로 포트 443에서 localhost에 대 한 바인딩 집합을 표시 하는 IIS에서 웹 사이트 창을 추가 합니다.](development-time-iis-support/_static/add-website-window.png)

IIS 설치 된 이미는 **기본 웹 사이트** 응용 프로그램의 실행 프로필 URL 호스트 이름과 일치 하는 호스트 이름의:

* 포트 443 (HTTPS)에 대 한 포트 바인딩을 추가 합니다.
* 유효한 인증서를 웹 사이트에 할당 합니다.

## <a name="enable-development-time-iis-support-in-visual-studio"></a>Visual Studio에서 개발 시 IIS 지원을 사용 하도록 설정

1. Visual Studio 설치 관리자를 시작 합니다.
1. 선택 된 **IIS 지원 개발 시간** 구성 요소입니다. 구성 요소에 옵션으로 나열 됩니다는 **요약** 패널에 대 한는 **ASP.NET 및 웹 개발** 작업 합니다. 구성 요소 설치는 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module), 하는 역방향 프록시 구성에서 ASP.NET Core IIS 뒤에 있는 앱을 실행 하는 데 필요한 네이티브 IIS 모듈입니다.

![Visual Studio 기능 수정: 워크로드 탭이 선택되어 있습니다. 웹 및 클라우드 섹션에는 ASP.NET 및 웹 개발 패널이 선택되어 있습니다. 요약 패널의 선택적 영역의 오른쪽에 IIS를 지 원하는 개발 시간에 대 한 확인 상자는.](development-time-iis-support/_static/development_time_support.png)

## <a name="configure-the-project"></a>프로젝트 구성

### <a name="https-redirection"></a>HTTPS 리디렉션

새 프로젝트에 대 한 확인란을 선택 **HTTPS에 대 한 구성** 에 **새 ASP.NET Core 웹 응용 프로그램** 창:

![새 ASP.NET Core 웹 응용 프로그램 창 HTTPS 확인란을 선택에 대 한 구성입니다.](development-time-iis-support/_static/new-app.png)

기존 프로젝트를 HTTPS 리디렉션 미들웨어에서 사용 하 여 `Startup.Configure` 호출 하 여는 [UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection) 확장 메서드:

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    else
    {
        app.UseExceptionHandler("/Error");
        app.UseHsts();
    }

    app.UseHttpsRedirection();
    app.UseStaticFiles();
    app.UseCookiePolicy();

    app.UseMvc();
}
```

### <a name="iis-launch-profile"></a>IIS 시작 프로필

개발 시 IIS 지원을 추가 하려면 새 실행 프로필을 만듭니다.

1. 에 대 한 **프로필**, 선택는 **새로** 단추입니다. 팝업 창에서 프로필 "IIS" 이름을 지정 합니다. 선택 **확인** 프로필을 만듭니다.
1. 에 대 한는 **시작** 선택 설정을 **IIS** 목록에서 합니다.
1. 에 대 한 확인란을 선택 **실행 브라우저** 끝점 URL을 제공 합니다. HTTPS 프로토콜을 사용 합니다. 이 예제에서는 `https://localhost/WebApplication1`를 사용합니다.
1. 에 **환경 변수** 섹션에서는 **추가** 단추입니다. 키로 환경 변수를 제공 `ASPNETCORE_ENVIRONMENT` 값 `Development`합니다.
1. 에 **웹 서버 설정** 영역 설정에서 **앱 URL**합니다. 이 예제에서는 `https://localhost/WebApplication1`를 사용합니다.
1. 프로필을 저장 합니다.

![디버그 탭이 선택된 프로젝트 속성 창입니다. 프로필 및 실행 설정은 IIS로 설정되어 있습니다. 실행 브라우저 기능에 속하는 주소를 사용 하도록 설정 되었는지 https://localhost/WebApplication1합니다. 동일한 주소 웹 서버 설정 영역에서의 앱 URL 필드에 제공 됩니다.](development-time-iis-support/_static/project_properties.png)

또는 실행 프로필을 수동으로 추가할는 [launchSettings.json](http://json.schemastore.org/launchsettings) 앱에서 파일:

```json
{
  "iisSettings": {
    "windowsAuthentication": false,
    "anonymousAuthentication": true,
    "iis": {
      "applicationUrl": "https://localhost/WebApplication1",
      "sslPort": 0
    }
  },
  "profiles": {
    "IIS": {
      "commandName": "IIS",
      "launchBrowser": true,
      "launchUrl": "https://localhost/WebApplication1",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```

## <a name="run-the-project"></a>프로젝트 실행

VS UI에서 [실행] 단추를 설정 된 **IIS** 프로 파일링 하 고 앱을 시작 단추를 선택 합니다.

!["IIS" 프로 파일링 하도록 설정 하 고 VS 도구 모음에서 단추를 실행 합니다.](development-time-iis-support/_static/toolbar.png)

관리자 권한으로 실행 되 고 있지 visual Studio를 다시 시작을 경우도 있습니다. 메시지가 표시되면 Visual Studio를 다시 시작합니다.

신뢰할 수 없는 개발 인증서를 사용 하는 경우 신뢰할 수 없는 인증서에 대 한 예외를 만들 수 있습니다 브라우저 필요할 수 있습니다.

## <a name="additional-resources"></a>추가 자료

* [IIS가 있는 Windows에서 ASP.NET Core 호스팅](xref:host-and-deploy/iis/index)
* [ASP.NET Core 모듈 소개](xref:fundamentals/servers/aspnet-core-module)
* [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)
* [HTTPS 적용](xref:security/enforcing-ssl)
