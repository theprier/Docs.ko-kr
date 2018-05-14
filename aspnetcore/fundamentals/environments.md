---
title: ASP.NET Core에서 여러 환경 사용
author: rick-anderson
description: ASP.NET Core가 어떻게 여러 환경에 걸쳐 앱 동작을 제어하기 위한 지원을 제공하는지에 대해 알아봅니다.
manager: wpickett
ms.author: riande
ms.date: 12/25/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/environments
ms.openlocfilehash: b9c3b8a15424ca637a2486450bfdde2762204935
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="work-with-multiple-environments-in-aspnet-core"></a>ASP.NET Core에서 여러 환경 사용

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

ASP.NET Core는 환경 변수를 통해 런타임 시 응용 프로그램 동작을 설정할 수 있는 지원을 제공합니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/environments/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="environments"></a>환경

ASP.NET Core는 응용 프로그램 시작 시 `ASPNETCORE_ENVIRONMENT` 환경 변수를 읽고, [IHostingEnvironment.EnvironmentName](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_IHostingEnvironment_EnvironmentName)에 해당 값을 저장합니다. `ASPNETCORE_ENVIRONMENT`는 임의의 값으로 설정할 수 있지만 [개발](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.development?view=aspnetcore-2.0), [준비](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.staging?view=aspnetcore-2.0) 및 [프로덕션](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.production?view=aspnetcore-2.0)의 [3개 값](/dotnet/api/microsoft.aspnetcore.hosting.environmentname?view=aspnetcore-2.0)은 프레임워크에서 지원됩니다. `ASPNETCORE_ENVIRONMENT`를 설정하지 않으면 기본값은 `Production`으로 설정됩니다.

[!code-csharp[](environments/sample/WebApp1/Startup.cs?name=snippet)]

위의 코드:

* `ASPNETCORE_ENVIRONMENT`가 `Development`로 설정된 경우 [UseDeveloperExceptionPage](/dotnet/api/microsoft.aspnetcore.builder.developerexceptionpageextensions.usedeveloperexceptionpage?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_DeveloperExceptionPageExtensions_UseDeveloperExceptionPage_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 및 [UseBrowserLink](/dotnet/api/microsoft.aspnetcore.builder.browserlinkextensions.usebrowserlink?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_BrowserLinkExtensions_UseBrowserLink_Microsoft_AspNetCore_Builder_IApplicationBuilder_)를 호출합니다.
* `ASPNETCORE_ENVIRONMENT`의 값이 다음 중 하나로 설정된 경우 [UseExceptionHandler](/dotnet/api/microsoft.aspnetcore.builder.exceptionhandlerextensions.useexceptionhandler?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_ExceptionHandlerExtensions_UseExceptionHandler_Microsoft_AspNetCore_Builder_IApplicationBuilder_)를 호출합니다.

    * `Staging`
    * `Production`
    * `Staging_2`

[환경 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)는 `IHostingEnvironment.EnvironmentName`의 값을 사용하여 요소에 표시를 포함하거나 제외합니다.

[!code-html[](environments/sample/WebApp1/Pages/About.cshtml)]

참고: Windows와 macOS에서 환경 변수 및 값은 대/소문자를 구분하지 않습니다. Linux 환경 변수 및 값은 기본적으로 **대/소문자를 구분**합니다.

### <a name="development"></a>개발

개발 환경은 프로덕션에서 노출해서는 안 되는 기능을 활성화할 수 있습니다. 예를 들어 ASP.NET Core 템플릿은 개발 환경에서 [개발자 예외 페이지](xref:fundamentals/error-handling#the-developer-exception-page)를 활성화합니다.

로컬 컴퓨터 개발을 위한 환경은 프로젝트의 *Properties\launchSettings.json* 파일에서 설정할 수 있습니다. *launchSettings.json*의 환경 값은 시스템 환경에서 설정된 값을 재정의합니다.

다음 JSON에는 *launchSettings.json* 파일의 세 가지 프로필이 표시되어 있습니다.

[!code-json[](environments/sample/WebApp1/Properties/launchSettings.json?highlight=10,11,18,26)]

::: moniker range=">= aspnetcore-2.1"
> [!NOTE]
> *launchSettings.json*의 `applicationUrl` 속성은 서버 URL의 목록을 지정할 수 있습니다. 목록의 URL 사이에 세미콜론을 사용합니다.
>
> ```json
> "WebApplication1": {
>    "commandName": "Project",
>    "launchBrowser": true,
>    "applicationUrl": "https://localhost:5001;http://localhost:5000",
>    "environmentVariables": {
>      "ASPNETCORE_ENVIRONMENT": "Development"
>    }
> }
> ```
::: moniker-end

[dotnet run](/dotnet/core/tools/dotnet-run)을 사용하여 응용 프로그램을 시작하면 `"commandName": "Project"`를 포함한 첫 번째 프로필이 사용됩니다. `commandName`의 값은 시작할 웹 서버를 지정합니다. `commandName`은 다음 중 하나일 수 있습니다.

* IIS Express
* IIS
* 프로젝트(Kestrel을 시작)

앱이 [dotnet run](/dotnet/core/tools/dotnet-run)으로 시작하는 경우:

* 가능한 경우 *launchSettings.json*을 읽습니다. *launchSettings.json*의 `environmentVariables` 설정은 환경 변수를 재정의합니다.
* 호스팅 환경이 표시됩니다.


다음 출력은 [dotnet run](/dotnet/core/tools/dotnet-run)으로 시작되는 앱을 보여 줍니다.
```bash
PS C:\Webs\WebApp1> dotnet run
Using launch settings from C:\Webs\WebApp1\Properties\launchSettings.json...
Hosting environment: Staging
Content root path: C:\Webs\WebApp1
Now listening on: http://localhost:54340
Application started. Press Ctrl+C to shut down.
```

Visual Studio **Debug** 탭은 *launchSettings.json* 파일을 편집할 수 있는 GUI를 제공합니다.

![프로젝트 속성 설정 환경 변수](environments/_static/project-properties-debug.png)

웹 서버가 다시 시작되기 전에는 프로젝트 프로필의 변경 내용이 적용되지 않을 수 있습니다. 해당 환경에 대한 변경 내용을 감지하려면 Kestrel을 다시 시작해야 합니다.

>[!WARNING]
> *launchSettings.json*은 암호를 저장하지 않아야 합니다. [암호 관리자 도구](xref:security/app-secrets)를 사용하여 로컬 개발에 대한 암호를 저장할 수 있습니다.

### <a name="production"></a>프로덕션

프로덕션 환경은 보안, 성능 및 응용 프로그램 견고성을 최대화하도록 구성되어야 합니다. 개발과 다른 몇 가지 일반적인 설정은 다음과 같습니다.

* 캐싱.
* 클라이언트 쪽 리소스가 번들로 제공되고, 축소되며, 잠재적으로 CDN에서 처리됩니다.
* 진단 오류 페이지를 사용하지 않습니다.
* 친숙한 오류 페이지를 사용하도록 설정합니다.
* 프로덕션 로깅 및 모니터링을 사용합니다. 예: [Application Insights](/azure/application-insights/app-insights-asp-net-core).

## <a name="setting-the-environment"></a>환경 설정하기

테스트를 위해 특정 환경을 설정하는 것이 유용합니다. 환경을 설정하지 않으면 대부분의 디버깅 기능을 사용하지 않는 `Production`으로 기본값이 지정됩니다.

환경 설정에 대한 메서드는 운영 체제에 따라 다릅니다.

### <a name="azure"></a>Azure

Azure App Service의 경우:

* **응용 프로그램 설정** 블레이드를 선택합니다.
* **앱 설정**에 키 및 값을 추가합니다.


### <a name="windows"></a>Windows
현재 세션에 `ASPNETCORE_ENVIRONMENT`를 설정하려면 앱이 [dotnet run](/dotnet/core/tools/dotnet-run)을 사용하여 시작된 경우 다음 명령이 사용됩니다.

**명령줄**
```
set ASPNETCORE_ENVIRONMENT=Development
```
**PowerShell**
```
$Env:ASPNETCORE_ENVIRONMENT = "Development"
```

이러한 명령은 현재 창에 대해서만 적용됩니다. 창이 닫히면 ASPNETCORE_ENVIRONMENT 설정이 기본 설정 또는 컴퓨터 값으로 되돌아갑니다. Windows에서 전역으로 값을 설정하려면 **제어판** > **시스템** > **고급 시스템 설정**을 열고 `ASPNETCORE_ENVIRONMENT` 값을 추가하거나 편집합니다.

![시스템 고급 속성](environments/_static/systemsetting_environment.png)

![ASPNET Core 환경 변수](environments/_static/windows_aspnetcore_environment.png)


**web.config**

[ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module#setting-environment-variables) 주제의 *환경 변수 설정하기* 항목을 참고하시기 바랍니다

**IIS 응용 프로그램 풀마다**

격리된 응용 프로그램 풀에서 실행되는 (IIS 10.0 이상에서 지원됨) 개별 응용 프로그램에 대한 환경 변수를 설정해야 할 경우, IIS 참조 문서의 [\<environmentVariables> 환경 변수](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) 항목 중, *AppCmd.exe 명령* 섹션을 참고하시기 바랍니다.

### <a name="macos"></a>macOS
macOS에 대한 현재 환경 설정은 응용 프로그램을 실행할 때 인라인에서 수행할 수 있습니다.

```bash
ASPNETCORE_ENVIRONMENT=Development dotnet run
```
또는 `export`를 사용하여 앱을 실행하기 전에 설정할 수도 있습니다.

```bash
export ASPNETCORE_ENVIRONMENT=Development
```
컴퓨터 수준 환경 변수는 *.bashrc* 또는 *.bash_profile* 파일에서 설정됩니다. 임의의 텍스트 편집기를 사용하여 파일을 편집하고 다음 문을 추가합니다.

```bash
export ASPNETCORE_ENVIRONMENT=Development
```

### <a name="linux"></a>Linux
Linux 배포의 경우 세션 기반 변수 설정에 대한 명령줄에서 `export` 명령 또는 컴퓨터 수준 환경 설정에 대한 *bash_profile* 파일을 사용합니다.

### <a name="configuration-by-environment"></a>환경별 구성

자세한 내용은 [환경에 의한 구성](xref:fundamentals/configuration/index#configuration-by-environment)을 참조하세요.

<a name="startup-conventions"></a>
## <a name="environment-based-startup-class-and-methods"></a>환경에 따른 시작 클래스 및 메서드

ASP.NET Core 앱이 시작되면 [시작 클래스](xref:fundamentals/startup)가 앱을 부트스트랩합니다. `Startup{EnvironmentName}` 클래스가 존재하는 경우 해당 클래스가 `EnvironmentName`에 대해 호출됩니다.

[!code-csharp[](environments/sample/WebApp1/StartupDev.cs?name=snippet&highlight=1)]

참고: [WebHostBuilder.UseStartup<TStartup>](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_)을 호출하면 구성 섹션을 재정의합니다.

[Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_StartupBase_Configure_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 및 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices?view=aspnetcore-2.0)는 `Configure{EnvironmentName}` 및 `Configure{EnvironmentName}Services` 양식의 환경 특정 버전을 지원합니다.

[!code-csharp[](environments/sample/WebApp1/Startup.cs?name=snippet_all&highlight=15,37)]

## <a name="additional-resources"></a>추가 자료

* [응용 프로그램 시작](xref:fundamentals/startup)
* [구성](xref:fundamentals/configuration/index)
* [IHostingEnvironment.EnvironmentName](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_IHostingEnvironment_EnvironmentName)
