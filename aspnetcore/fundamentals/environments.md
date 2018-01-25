---
title: "여러 환경에서 ASP.NET Core 작업"
author: rick-anderson
description: "ASP.NET Core 여러 환경에 걸쳐 응용 프로그램 동작을 제어 하는 것에 대 한 지원에 제공 하는 방법에 대해 알아봅니다."
ms.author: riande
manager: wpickett
ms.date: 12/25/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/environments
ms.openlocfilehash: 60a1543ce11d08490e6df0eb84f980672ecfe672
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="working-with-multiple-environments"></a>여러 환경 작업

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

ASP.NET Core를 환경 변수와 런타임 시 응용 프로그램 동작을 설정 하기 위한 지원을 제공 합니다.

[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/environments/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="environments"></a>환경

ASP.NET Core 환경 변수를 읽는 `ASPNETCORE_ENVIRONMENT` 응용 프로그램 시작 및 값 저장소에서 [IHostingEnvironment.EnvironmentName](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_IHostingEnvironment_EnvironmentName)합니다. `ASPNETCORE_ENVIRONMENT`임의의 값으로 설정할 수 있지만 [3 개의 값](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname?view=aspnetcore-2.0) 프레임 워크에서 지원 됩니다: [개발](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.development?view=aspnetcore-2.0), [준비](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.staging?view=aspnetcore-2.0), 및 [프로덕션](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.production?view=aspnetcore-2.0)합니다. 경우 `ASPNETCORE_ENVIRONMENT` 값은 기본적으로 설정 되지 않습니다 `Production`합니다.

[!code-csharp[Main](environments/sample/WebApp1/Startup.cs?name=snippet)]

위의 코드:

* 호출 [UseDeveloperExceptionPage](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.developerexceptionpageextensions.usedeveloperexceptionpage?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_DeveloperExceptionPageExtensions_UseDeveloperExceptionPage_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 및 [UseBrowserLink](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.browserlinkextensions.usebrowserlink?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_BrowserLinkExtensions_UseBrowserLink_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 때 `ASPNETCORE_ENVIRONMENT` 로 설정 된 `Development`합니다.
* 호출 [UseExceptionHandler](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.exceptionhandlerextensions.useexceptionhandler?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_ExceptionHandlerExtensions_UseExceptionHandler_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 때의 값 `ASPNETCORE_ENVIRONMENT` 다음 중 하나를 설정 됩니다.

    * `Staging`
    * `Production`
    * `Staging_2`

[환경 태그 도우미 ](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper) 의 값을 사용 하 여 `IHostingEnvironment.EnvironmentName` 포함 하거나 제외할 요소의 태그:

[!code-html[Main](environments/sample/WebApp1/Pages/About.cshtml)]

참고: Windows와 macOS에서 환경 변수와 값은 대/소문자 구분 합니다. Linux 환경 변수와 값은 **대/소문자 구분** 기본적으로 합니다.

### <a name="development"></a>개발

개발 환경 프로덕션 환경에서 노출 하지 않아야 하는 기능을 활성화할 수 있습니다. ASP.NET Core 템플릿을 사용 하는 예를 들어는 [개발자 예외 페이지](xref:fundamentals/error-handling#the-developer-exception-page) 개발 환경에서 합니다.

로컬 컴퓨터 개발을 위한 환경에서 설정할 수 있습니다는 *Properties\launchSettings.json* 프로젝트의 파일입니다. 환경 값으로 설정할 *launchSettings.json* 시스템 환경에서 설정 값을 재정의 합니다.

다음 XML에서 프로필이 3 개를 보여 줍니다.는 *launchSettings.json* 파일:

[!code-xml[Main](environments/sample/WebApp1/Properties/launchSettings.json?highlight=10,11,18,26)]

응용 프로그램으로 시작 될 때 `dotnet run`를 사용 하 여 첫 번째 프로필 `"commandName": "Project"` 사용 됩니다. 값 `commandName` 를 시작 하려면 웹 서버를 지정 합니다. `commandName`하나일 수 있습니다.

* IIS Express
* IIS
* 프로젝트 (시작 하는 Kestrel)

응용 프로그램으로 시작 될 때 `dotnet run`:

* *launchSettings.json* 읽기 가능한 경우. `environmentVariables`설정 *launchSettings.json* 환경 변수 재정의 합니다.
* 호스팅 환경이 표시 됩니다.


다음과 같은 출력을 시작 하는 응용 프로그램을 보여 줍니다. `dotnet run`:
```bash
PS C:\Webs\WebApp1> dotnet run
Using launch settings from C:\Webs\WebApp1\Properties\launchSettings.json...
Hosting environment: Staging
Content root path: C:\Webs\WebApp1
Now listening on: http://localhost:54340
Application started. Press Ctrl+C to shut down.
```

Visual Studio **디버그** 탭 편집 하려면 GUI에서는 제공 된 *launchSettings.json* 파일:

![프로젝트 속성 설정 환경 변수](environments/_static/project-properties-debug.png)

웹 서버를 다시 시작 될 때까지 프로젝트 프로필의 변경 내용이 적용 되지 않을 수 있습니다. 해당 환경에 대해 변경 내용을 감지 합니다 kestrel은 다시 시작 해야 합니다.

>[!WARNING]
> *launchSettings.json* 비밀 정보를 저장 하지 않아야 합니다. [암호 관리자 도구](xref:security/app-secrets) 로컬 개발에 대 한 암호를 저장 하기 위해 사용할 수 있습니다.

### <a name="production"></a>프로덕션

프로덕션 환경 보안, 성능 및 응용 프로그램의 견고성을 최대화 하기 위해 구성 되어야 합니다. 다음과 같은 몇 가지 일반적인 프로덕션 환경에 있을 수 있는 것 다른 설정을 개발

* 캐시 합니다.
* 클라이언트 쪽 리소스가 번들로 제공 하 고, 축소 하 고 잠재적으로 CDN에서 처리 됩니다.
* 진단 오류 페이지를 사용 하지 않도록 설정 합니다.
* 오류 페이지를 사용 하도록 설정 합니다.
* 프로덕션 로깅 및 모니터링 사용 하도록 설정 합니다. 예를 들어 [Application Insights](https://azure.microsoft.com/documentation/articles/app-insights-asp-net-five/)합니다.

## <a name="setting-the-environment"></a>환경 설정

테스트 하기 위한 특정 환경을 설정 하는 것이 유용 합니다. 환경 설정 되지 않은 경우 값은 기본적으로 `Production` 는 대부분의 디버깅 기능을 사용 하지 않도록 설정 합니다.

환경 설정에 대 한 메서드는 운영 체제에 따라 달라 집니다.

### <a name="azure"></a>Azure

Azure 앱 서비스:

* 선택 된 **응용 프로그램 설정** 블레이드입니다.
* 키를 추가 하 고 값 **앱 설정**합니다.


### <a name="windows"></a>Windows
설정 하는 `ASPNETCORE_ENVIRONMENT` 를 사용 하 여 앱이 시작 하는 경우 현재 세션에 대 한 `dotnet run`, 다음 명령을 사용 하는

**명령줄**
```
set ASPNETCORE_ENVIRONMENT=Development
```
**PowerShell**
```
$Env:ASPNETCORE_ENVIRONMENT = "Development"
```

이 명령은 현재 창에 대해서만 적용 됩니다. 창이 닫히면 ASPNETCORE_ENVIRONMENT 설정을 기본 설정 또는 컴퓨터 값 되돌아갑니다. Windows 열 값을 전역으로 설정 된 **제어판** > **시스템** > **고급 시스템 설정** 추가 하거나는 편집`ASPNETCORE_ENVIRONMENT` 값입니다.

![시스템의 고급 속성](environments/_static/systemsetting_environment.png)

![ASPNET 코어 환경 변수](environments/_static/windows_aspnetcore_environment.png)


**web.config**

참조는 *환경 변수 설정* 의 섹션은 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module#setting-environment-variables) 항목입니다.

**IIS 응용 프로그램 풀 당**

격리 된 응용 프로그램 풀 (IIS 10.0 이상에서 지원 됨)에서 실행 되는 개별 앱에 대 한 환경 변수를 설정 하려면 참조는 *AppCmd.exe 명령을* 의 섹션은 [환경 변수 \< environmentVariables >](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) 항목입니다.

### <a name="macos"></a>macOS
MacOS에 대 한 현재 환경 설정 구성 방법은 인라인 응용 프로그램을 실행 하는 경우

```bash
ASPNETCORE_ENVIRONMENT=Development dotnet run
```
사용 하 여 또는 `export` 응용 프로그램을 실행 하기 전에 설정할 수 있습니다.

```bash
export ASPNETCORE_ENVIRONMENT=Development
```
시스템 수준 환경 변수 설정는 *.bashrc* 또는 *.bash_profile* 파일입니다. 임의의 텍스트 편집기를 사용 하 여 파일을 편집 하 고 다음 문을 추가 합니다.

```
export ASPNETCORE_ENVIRONMENT=Development
```

### <a name="linux"></a>Linux
사용 하 여 Linux 배포판는 `export` 세션 변수 설정을 기반으로 하는 명령줄에서 명령 및 *bash_profile* 시스템 수준 환경 설정에 대 한 파일입니다.

### <a name="configuration-by-environment"></a>환경별 구성

참조 [환경에 의해 구성](xref:fundamentals/configuration/index#configuration-by-environment) 자세한 정보에 대 한 합니다.

<a name="startup-conventions"></a>
## <a name="environment-based-startup-class-and-methods"></a>환경에 따라 시작 클래스 및 메서드

ASP.NET Core 응용 프로그램 시작 되 면는 [시작 클래스](xref:fundamentals/startup) 응용 프로그램 시작 되도록 합니다. 클래스 `Startup{EnvironmentName}` 는 클래스를 호출할 수 있는 `EnvironmentName`:

[!code-csharp[Main](environments/sample/WebApp1/StartupDev.cs?name=snippet&highlight=1)]

참고: 호출 [WebHostBuilder.UseStartup<TStartup> ](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) 구성 섹션을 재정의 합니다.

[구성](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_StartupBase_Configure_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 및 [ConfigureServices](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices?view=aspnetcore-2.0) 환경 폼의 특정 버전을 지원 `Configure{EnvironmentName}` 및 `Configure{EnvironmentName}Services`:

[!code-csharp[Main](environments/sample/WebApp1/Startup.cs?name=snippet_all&highlight=15,37)]

## <a name="additional-resources"></a>추가 리소스

* [응용 프로그램 시작](xref:fundamentals/startup)
* [구성](xref:fundamentals/configuration/index)
* [IHostingEnvironment.EnvironmentName](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_IHostingEnvironment_EnvironmentName)
