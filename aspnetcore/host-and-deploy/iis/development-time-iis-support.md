---
title: ASP.NET Core용 Visual Studio의 개발 시간 IIS 지원
author: shirhatti
description: Windows Server에서 IIS를 통해 실행될 경우 ASP.NET Core 앱 디버그에 대한 지원을 확인해 보세요.
ms.author: riande
ms.custom: mvc
ms.date: 05/14/2018
uid: host-and-deploy/iis/development-time-iis-support
ms.openlocfilehash: eb8b4369d6d5434adbac187f59b18d7a2b80055c
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36277656"
---
# <a name="development-time-iis-support-in-visual-studio-for-aspnet-core"></a>ASP.NET Core용 Visual Studio의 개발 시간 IIS 지원

작성자: [Sourabh Shirhatti](https://twitter.com/sshirhatti) 및 [Luke Latham](https://github.com/guardrex)

이 문서에서는 Windows Server에서 IIS를 통해 실행되는 ASP.NET Core 앱을 디버그하기 위한 [Visual Studio](https://www.visualstudio.com/vs/) 지원에 대해 설명합니다. 이 항목에서는 이 기능을 사용하도록 설정하고 프로젝트를 설정하는 방법을 안내합니다.

## <a name="prerequisites"></a>전제 조건

* [Windows용 Visual Studio](https://www.microsoft.com/net/download/windows)
* **ASP.NET 및 웹 개발** 워크로드
* **.NET Core 플랫폼 간 개발** 워크로드
* X.509 보안 인증서

## <a name="enable-iis"></a>IIS 활성화

1. **제어판** > **프로그램** > **프로그램 및 기능** > **Windows 기능 Windows 기능 사용/사용 안 함**(화면 왼쪽)으로 차례로 이동합니다.
1. **인터넷 정보 서비스** 확인란을 선택합니다.

![인터넷 정보 서비스 확인란이 검은 사각형(확인 표시 아님)으로 표시되어 있고 IIS 기능 중 일부가 활성화되었음을 보여주는 Windows 기능](development-time-iis-support/_static/enable_iis.png)

IIS를 설치하려면 시스템을 다시 시작해야 할 수 있습니다.

## <a name="configure-iis"></a>IIS 구성

IIS에서 웹 사이트는 다음과 같이 구성되어야 합니다.

* 앱의 시작 프로필 URL 호스트 이름과 일치하는 호스트 이름.
* 할당된 인증서가 있는 포트 443에 대한 바인딩.

예를 들어 추가된 웹 사이트의 **호스트 이름**은 “localhost”로 설정됩니다(이 항목의 뒷부분에서 시작 프로필에도 “localhost”를 사용함). 포트가 “443”(HTTPS)으로 설정됩니다. **IIS Express 개발 인증서**가 웹 사이트에 할당되지만 모든 유효한 인증서가 작동합니다.

![인증서가 할당된 포트 443에서 localhost에 대한 바인딩 집합을 표시하는 [웹 사이트] 창을 IIS에서 추가합니다.](development-time-iis-support/_static/add-website-window.png)

IIS 설치에 앱의 시작 프로필 URL 호스트 이름과 일치하는 호스트 이름을 가진 **기본 웹 사이트**가 이미 있는 경우:

* 포트 443(HTTPS)에 포트 바인딩을 추가합니다.
* 웹 사이트에 유효한 인증서를 할당합니다.

## <a name="enable-development-time-iis-support-in-visual-studio"></a>Visual Studio에서 개발 시간 IIS 지원 사용

1. Visual Studio 설치 관리자를 시작합니다.
1. **개발 시간 IIS 지원** 구성 요소를 선택합니다. 이 구성 요소는 **ASP.NET 및 웹 개발** 워크로드에 대한 **요약** 패널에 선택 사항으로 나열됩니다. 구성 요소는 역방향 프록시 구성에서 IIS를 통해 ASP.NET Core 앱을 실행하는 데 필요한 네이티브 IIS 모듈인 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 설치합니다.

![Visual Studio 기능 수정: 워크로드 탭이 선택되어 있습니다. 웹 및 클라우드 섹션에는 ASP.NET 및 웹 개발 패널이 선택되어 있습니다. [요약] 패널의 [선택 사항] 영역 오른쪽에 [개발 시간 IIS 지원] 확인란이 있습니다.](development-time-iis-support/_static/development_time_support.png)

## <a name="configure-the-project"></a>프로젝트 구성

### <a name="https-redirection"></a>HTTPS 리디렉션

새 프로젝트의 경우 **새 ASP.NET Core 웹 응용 프로그램** 창에서 **HTTPS에 대한 구성** 확인란을 선택합니다.

![HTTPS에 대한 구성 확인란이 선택된 새 ASP.NET Core 웹 응용 프로그램 창.](development-time-iis-support/_static/new-app.png)

기존 프로젝트에서는 [UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection) 확장 메서드를 호출하여 `Startup.Configure`에서 HTTPS 리디렉션 미들웨어를 사용합니다.

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

새 시작 프로필을 만들어 개발 시간 IIS 지원을 추가합니다.

1. **프로필**의 경우 **새로 만들기** 단추를 선택합니다. 팝업 창에서 프로필 이름을 “IIS”로 지정합니다. **확인**을 선택하여 프로필을 만듭니다.
1. **시작** 설정의 경우 목록에서 **IIS**를 선택합니다.
1. **브라우저 시작** 확인란을 선택하고 끝점 URL을 제공합니다. HTTPS 프로토콜을 사용합니다. 이 예제에서는 `https://localhost/WebApplication1`를 사용합니다.
1. **환경 변수** 섹션에서 **추가** 단추를 선택합니다. `ASPNETCORE_ENVIRONMENT` 키 및 `Development` 값을 사용하여 환경 변수를 제공합니다.
1. **웹 서버 설정** 영역에서 **앱 URL**을 설정합니다. 이 예제에서는 `https://localhost/WebApplication1`를 사용합니다.
1. 프로필을 저장합니다.

![디버그 탭이 선택된 프로젝트 속성 창입니다. 프로필 및 실행 설정은 IIS로 설정되어 있습니다. 브라우저 시작 기능에는 https://localhost/WebApplication1 주소가 사용됩니다. 웹 서버 설정 영역의 [앱 URL] 필드에도 동일한 주소가 제공됩니다.](development-time-iis-support/_static/project_properties.png)

또는 앱의 [launchSettings.json](http://json.schemastore.org/launchsettings) 파일에 시작 프로필을 수동으로 추가합니다.

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

VS UI에서 [실행] 단추를 **IIS** 프로필로 설정하고 단추를 선택하여 앱을 시작합니다.

![“IIS” 프로필로 설정된 VS 도구 모음의 실행 단추.](development-time-iis-support/_static/toolbar.png)

관리자로 실행하고 있지 않으면 Visual Studio에서 다시 시작하라는 메시지가 표시될 수 있습니다. 메시지가 표시되면 Visual Studio를 다시 시작합니다.

신뢰할 수 없는 개발 인증서를 사용하는 경우 브라우저에서 신뢰할 수 없는 인증서에 대한 예외를 만들어야 할 수 있습니다.

## <a name="additional-resources"></a>추가 자료

* [IIS가 있는 Windows에서 ASP.NET Core 호스팅](xref:host-and-deploy/iis/index)
* [ASP.NET Core 모듈 소개](xref:fundamentals/servers/aspnet-core-module)
* [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)
* [HTTPS 적용](xref:security/enforcing-ssl)
