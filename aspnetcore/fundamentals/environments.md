---
title: "ASP.NET Core에서 여러 환경 사용"
author: rick-anderson
description: "ASP.NET Core가 어떻게 여러 환경에 걸쳐 앱 동작을 제어하기 위한 지원을 제공하는지에 대해 알아봅니다."
manager: wpickett
ms.author: riande
ms.date: 12/25/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/environments
ms.openlocfilehash: b40ee9b1c6feae4942f05d22dab776d3cf6c26a0
ms.sourcegitcommit: 18d1dc86770f2e272d93c7e1cddfc095c5995d9e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="working-with-multiple-environments"></a><span data-ttu-id="222f1-103">여러 환경 사용</span><span class="sxs-lookup"><span data-stu-id="222f1-103">Working with multiple environments</span></span>

<span data-ttu-id="222f1-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="222f1-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="222f1-105">ASP.NET Core는 환경 변수를 통해 런타임 시 응용 프로그램 동작을 설정할 수 있는 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-105">ASP.NET Core provides support for setting application behavior at runtime with environment variables.</span></span>

<span data-ttu-id="222f1-106">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/environments/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="222f1-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/environments/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="environments"></a><span data-ttu-id="222f1-107">환경</span><span class="sxs-lookup"><span data-stu-id="222f1-107">Environments</span></span>

<span data-ttu-id="222f1-108">ASP.NET Core는 응용 프로그램 시작 시 `ASPNETCORE_ENVIRONMENT` 환경 변수를 읽고, [IHostingEnvironment.EnvironmentName](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_IHostingEnvironment_EnvironmentName)에 해당 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-108">ASP.NET Core reads the environment variable `ASPNETCORE_ENVIRONMENT` at application startup and stores that value in [IHostingEnvironment.EnvironmentName](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_IHostingEnvironment_EnvironmentName).</span></span> <span data-ttu-id="222f1-109">`ASPNETCORE_ENVIRONMENT`는 임의의 값으로 설정할 수 있지만 [개발](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.development?view=aspnetcore-2.0), [준비](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.staging?view=aspnetcore-2.0) 및 [프로덕션](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.production?view=aspnetcore-2.0)의 [3개 값](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname?view=aspnetcore-2.0)은 프레임워크에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-109">`ASPNETCORE_ENVIRONMENT` can be set to any value, but [three values](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname?view=aspnetcore-2.0) are supported by the framework: [Development](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.development?view=aspnetcore-2.0), [Staging](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.staging?view=aspnetcore-2.0), and [Production](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.production?view=aspnetcore-2.0).</span></span> <span data-ttu-id="222f1-110">`ASPNETCORE_ENVIRONMENT`를 설정하지 않으면 기본값은 `Production`으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-110">If `ASPNETCORE_ENVIRONMENT` isn't set, it will default to `Production`.</span></span>

[!code-csharp[Main](environments/sample/WebApp1/Startup.cs?name=snippet)]

<span data-ttu-id="222f1-111">위의 코드:</span><span class="sxs-lookup"><span data-stu-id="222f1-111">The preceding code:</span></span>

* <span data-ttu-id="222f1-112">`ASPNETCORE_ENVIRONMENT`가 `Development`로 설정된 경우 [UseDeveloperExceptionPage](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.developerexceptionpageextensions.usedeveloperexceptionpage?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_DeveloperExceptionPageExtensions_UseDeveloperExceptionPage_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 및 [UseBrowserLink](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.browserlinkextensions.usebrowserlink?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_BrowserLinkExtensions_UseBrowserLink_Microsoft_AspNetCore_Builder_IApplicationBuilder_)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-112">Calls [UseDeveloperExceptionPage](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.developerexceptionpageextensions.usedeveloperexceptionpage?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_DeveloperExceptionPageExtensions_UseDeveloperExceptionPage_Microsoft_AspNetCore_Builder_IApplicationBuilder_) and [UseBrowserLink](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.browserlinkextensions.usebrowserlink?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_BrowserLinkExtensions_UseBrowserLink_Microsoft_AspNetCore_Builder_IApplicationBuilder_) when `ASPNETCORE_ENVIRONMENT` is set to `Development`.</span></span>
* <span data-ttu-id="222f1-113">`ASPNETCORE_ENVIRONMENT`의 값이 다음 중 하나로 설정된 경우 [UseExceptionHandler](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.exceptionhandlerextensions.useexceptionhandler?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_ExceptionHandlerExtensions_UseExceptionHandler_Microsoft_AspNetCore_Builder_IApplicationBuilder_)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-113">Calls [UseExceptionHandler](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.exceptionhandlerextensions.useexceptionhandler?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_ExceptionHandlerExtensions_UseExceptionHandler_Microsoft_AspNetCore_Builder_IApplicationBuilder_) when the value of `ASPNETCORE_ENVIRONMENT` is set one of the following:</span></span>

    * `Staging`
    * `Production`
    * `Staging_2`

<span data-ttu-id="222f1-114">[환경 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)는 `IHostingEnvironment.EnvironmentName`의 값을 사용하여 요소에 표시를 포함하거나 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-114">The [Environment Tag Helper ](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper) uses the value of `IHostingEnvironment.EnvironmentName` to include or exclude markup in the element:</span></span>

[!code-html[Main](environments/sample/WebApp1/Pages/About.cshtml)]

<span data-ttu-id="222f1-115">참고: Windows와 macOS에서 환경 변수 및 값은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-115">Note: On Windows and macOS, environment variables and values are not case sensitive.</span></span> <span data-ttu-id="222f1-116">Linux 환경 변수 및 값은 기본적으로 **대/소문자를 구분**합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-116">Linux environment variables and values are **case sensitive** by default.</span></span>

### <a name="development"></a><span data-ttu-id="222f1-117">개발</span><span class="sxs-lookup"><span data-stu-id="222f1-117">Development</span></span>

<span data-ttu-id="222f1-118">개발 환경은 프로덕션에서 노출해서는 안 되는 기능을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-118">The development environment can enable features that shouldn't be exposed in production.</span></span> <span data-ttu-id="222f1-119">예를 들어 ASP.NET Core 템플릿은 개발 환경에서 [개발자 예외 페이지](xref:fundamentals/error-handling#the-developer-exception-page)를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-119">For example, the ASP.NET Core templates enable the [developer exception page](xref:fundamentals/error-handling#the-developer-exception-page) in the development environment.</span></span>

<span data-ttu-id="222f1-120">로컬 컴퓨터 개발을 위한 환경은 프로젝트의 *Properties\launchSettings.json* 파일에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-120">The environment for local machine development can be set in the *Properties\launchSettings.json* file of the project.</span></span> <span data-ttu-id="222f1-121">*launchSettings.json*의 환경 값은 시스템 환경에서 설정된 값을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-121">Environment values set in *launchSettings.json* override values set in the system environment.</span></span>

<span data-ttu-id="222f1-122">다음 JSON에는 *launchSettings.json* 파일의 세 가지 프로필이 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-122">The following JSON shows three profiles from a *launchSettings.json* file:</span></span>

[!code-json[Main](environments/sample/WebApp1/Properties/launchSettings.json?highlight=10,11,18,26)]

<span data-ttu-id="222f1-123">응용 프로그램이 `dotnet run`으로 시작하는 경우 `"commandName": "Project"`가 있는 첫 번째 프로필이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-123">When the application is launched with `dotnet run`, the first profile with `"commandName": "Project"` will be used.</span></span> <span data-ttu-id="222f1-124">`commandName`의 값은 시작할 웹 서버를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-124">The value of `commandName` specifies the web server to launch.</span></span> <span data-ttu-id="222f1-125">`commandName`은 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-125">`commandName` can be one of :</span></span>

* <span data-ttu-id="222f1-126">IIS Express</span><span class="sxs-lookup"><span data-stu-id="222f1-126">IIS Express</span></span>
* <span data-ttu-id="222f1-127">IIS</span><span class="sxs-lookup"><span data-stu-id="222f1-127">IIS</span></span>
* <span data-ttu-id="222f1-128">프로젝트(Kestrel을 시작)</span><span class="sxs-lookup"><span data-stu-id="222f1-128">Project (which launches Kestrel)</span></span>

<span data-ttu-id="222f1-129">앱이 `dotnet run`으로 시작하는 경우:</span><span class="sxs-lookup"><span data-stu-id="222f1-129">When an app is launched with `dotnet run`:</span></span>

* <span data-ttu-id="222f1-130">가능한 경우 *launchSettings.json*을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-130">*launchSettings.json* is read if available.</span></span> <span data-ttu-id="222f1-131">*launchSettings.json*의 `environmentVariables` 설정은 환경 변수를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-131">`environmentVariables` settings in *launchSettings.json* override environment variables.</span></span>
* <span data-ttu-id="222f1-132">호스팅 환경이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-132">The hosting environment is displayed.</span></span>


<span data-ttu-id="222f1-133">다음 출력에는 `dotnet run`으로 시작되는 앱이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-133">The following output shows an app started with `dotnet run`:</span></span>
```bash
PS C:\Webs\WebApp1> dotnet run
Using launch settings from C:\Webs\WebApp1\Properties\launchSettings.json...
Hosting environment: Staging
Content root path: C:\Webs\WebApp1
Now listening on: http://localhost:54340
Application started. Press Ctrl+C to shut down.
```

<span data-ttu-id="222f1-134">Visual Studio **Debug** 탭은 *launchSettings.json* 파일을 편집할 수 있는 GUI를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-134">The Visual Studio **Debug** tab provides a GUI to edit the *launchSettings.json* file:</span></span>

![프로젝트 속성 설정 환경 변수](environments/_static/project-properties-debug.png)

<span data-ttu-id="222f1-136">웹 서버가 다시 시작되기 전에는 프로젝트 프로필의 변경 내용이 적용되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-136">Changes made to project profiles may not take effect until the web server is restarted.</span></span> <span data-ttu-id="222f1-137">해당 환경에 대한 변경 내용을 감지하려면 Kestrel을 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-137">Kestrel must be restarted before it will detect changes made to its environment.</span></span>

>[!WARNING]
> <span data-ttu-id="222f1-138">*launchSettings.json*은 암호를 저장하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-138">*launchSettings.json* shouldn't store secrets.</span></span> <span data-ttu-id="222f1-139">[암호 관리자 도구](xref:security/app-secrets)를 사용하여 로컬 개발에 대한 암호를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-139">The [Secret Manager tool](xref:security/app-secrets) can be used to store secrets for local development.</span></span>

### <a name="production"></a><span data-ttu-id="222f1-140">프로덕션</span><span class="sxs-lookup"><span data-stu-id="222f1-140">Production</span></span>

<span data-ttu-id="222f1-141">프로덕션 환경은 보안, 성능 및 응용 프로그램 견고성을 최대화하도록 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-141">The production environment should be configured to maximize security, performance, and application robustness.</span></span> <span data-ttu-id="222f1-142">프로덕션 환경에 있을 수 있는, 개발과 다를 수 있는 몇 가지 일반적인 설정에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-142">Some common settings that a production environment might have that would differ from development include:</span></span>

* <span data-ttu-id="222f1-143">캐싱.</span><span class="sxs-lookup"><span data-stu-id="222f1-143">Caching.</span></span>
* <span data-ttu-id="222f1-144">클라이언트 쪽 리소스가 번들로 제공되고, 축소되며, 잠재적으로 CDN에서 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-144">Client-side resources are bundled, minified, and potentially served from a CDN.</span></span>
* <span data-ttu-id="222f1-145">진단 오류 페이지를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-145">Diagnostic error pages disabled.</span></span>
* <span data-ttu-id="222f1-146">친숙한 오류 페이지를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-146">Friendly error pages enabled.</span></span>
* <span data-ttu-id="222f1-147">프로덕션 로깅 및 모니터링을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-147">Production logging and monitoring enabled.</span></span> <span data-ttu-id="222f1-148">예: [Application Insights](/azure/application-insights/app-insights-asp-net-core).</span><span class="sxs-lookup"><span data-stu-id="222f1-148">For example, [Application Insights](/azure/application-insights/app-insights-asp-net-core).</span></span>

## <a name="setting-the-environment"></a><span data-ttu-id="222f1-149">환경 설정하기</span><span class="sxs-lookup"><span data-stu-id="222f1-149">Setting the environment</span></span>

<span data-ttu-id="222f1-150">테스트를 위해 특정 환경을 설정하는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-150">It's often useful to set a specific environment for testing.</span></span> <span data-ttu-id="222f1-151">환경을 설정하지 않으면 대부분의 디버깅 기능을 사용하지 않는 `Production`으로 기본값이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-151">If the environment isn't set, it will default to `Production` which disables most debugging features.</span></span>

<span data-ttu-id="222f1-152">환경 설정에 대한 메서드는 운영 체제에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-152">The method for setting the environment depends on the operating system.</span></span>

### <a name="azure"></a><span data-ttu-id="222f1-153">Azure</span><span class="sxs-lookup"><span data-stu-id="222f1-153">Azure</span></span>

<span data-ttu-id="222f1-154">Azure App Service의 경우:</span><span class="sxs-lookup"><span data-stu-id="222f1-154">For Azure app service:</span></span>

* <span data-ttu-id="222f1-155">**응용 프로그램 설정** 블레이드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-155">Select the **Application settings** blade.</span></span>
* <span data-ttu-id="222f1-156">**앱 설정**에 키 및 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-156">Add the key and value in **App settings**.</span></span>


### <a name="windows"></a><span data-ttu-id="222f1-157">Windows</span><span class="sxs-lookup"><span data-stu-id="222f1-157">Windows</span></span>
<span data-ttu-id="222f1-158">현재 세션에 대한 `ASPNETCORE_ENVIRONMENT`를 설정하려면 앱이 `dotnet run`을 사용하여 시작된 경우 다음 명령이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-158">To set the `ASPNETCORE_ENVIRONMENT` for the current session, if the app is started using `dotnet run`, the following commands are used</span></span>

<span data-ttu-id="222f1-159">**명령줄**</span><span class="sxs-lookup"><span data-stu-id="222f1-159">**Command line**</span></span>
```
set ASPNETCORE_ENVIRONMENT=Development
```
<span data-ttu-id="222f1-160">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="222f1-160">**PowerShell**</span></span>
```
$Env:ASPNETCORE_ENVIRONMENT = "Development"
```

<span data-ttu-id="222f1-161">이러한 명령은 현재 창에 대해서만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-161">These commands take effect only for the current window.</span></span> <span data-ttu-id="222f1-162">창이 닫히면 ASPNETCORE_ENVIRONMENT 설정이 기본 설정 또는 컴퓨터 값으로 되돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-162">When the window is closed, the ASPNETCORE_ENVIRONMENT setting reverts to the default setting or machine value.</span></span> <span data-ttu-id="222f1-163">Windows에서 전역으로 값을 설정하려면 **제어판** > **시스템** > **고급 시스템 설정**을 열고 `ASPNETCORE_ENVIRONMENT` 값을 추가하거나 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-163">In order to set the value globally on Windows open the **Control Panel** > **System** > **Advanced system settings** and add or edit the `ASPNETCORE_ENVIRONMENT` value.</span></span>

![시스템 고급 속성](environments/_static/systemsetting_environment.png)

![ASPNET Core 환경 변수](environments/_static/windows_aspnetcore_environment.png)


<span data-ttu-id="222f1-166">**web.config**</span><span class="sxs-lookup"><span data-stu-id="222f1-166">**web.config**</span></span>

<span data-ttu-id="222f1-167">[ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module#setting-environment-variables) 주제의 *환경 변수 설정하기* 항목을 참고하시기 바랍니다</span><span class="sxs-lookup"><span data-stu-id="222f1-167">See the *Setting environment variables* section of the [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module#setting-environment-variables) topic.</span></span>

<span data-ttu-id="222f1-168">**IIS 응용 프로그램 풀마다**</span><span class="sxs-lookup"><span data-stu-id="222f1-168">**Per IIS Application Pool**</span></span>

<span data-ttu-id="222f1-169">격리된 응용 프로그램 풀에서 실행되는 (IIS 10.0 이상에서 지원됨) 개별 응용 프로그램에 대한 환경 변수를 설정해야 할 경우, IIS 참조 문서의 [\<environmentVariables> 환경 변수](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) 항목 중, *AppCmd.exe 명령* 섹션을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-169">To set environment variables for individual apps running in isolated Application Pools (supported on IIS 10.0+), see the *AppCmd.exe command* section of the [Environment Variables \<environmentVariables>](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) topic.</span></span>

### <a name="macos"></a><span data-ttu-id="222f1-170">macOS</span><span class="sxs-lookup"><span data-stu-id="222f1-170">macOS</span></span>
<span data-ttu-id="222f1-171">macOS에 대한 현재 환경 설정은 응용 프로그램을 실행할 때 인라인에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-171">Setting the current environment for macOS can be done in-line when running the application;</span></span>

```bash
ASPNETCORE_ENVIRONMENT=Development dotnet run
```
<span data-ttu-id="222f1-172">또는 `export`를 사용하여 앱을 실행하기 전에 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-172">or using `export` to set it prior to running the app.</span></span>

```bash
export ASPNETCORE_ENVIRONMENT=Development
```
<span data-ttu-id="222f1-173">컴퓨터 수준 환경 변수는 *.bashrc* 또는 *.bash_profile* 파일에서 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-173">Machine level environment variables are set in the *.bashrc* or *.bash_profile* file.</span></span> <span data-ttu-id="222f1-174">임의의 텍스트 편집기를 사용하여 파일을 편집하고 다음 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-174">Edit the file using any text editor and add the following statment.</span></span>

```bash
export ASPNETCORE_ENVIRONMENT=Development
```

### <a name="linux"></a><span data-ttu-id="222f1-175">Linux</span><span class="sxs-lookup"><span data-stu-id="222f1-175">Linux</span></span>
<span data-ttu-id="222f1-176">Linux 배포의 경우 세션 기반 변수 설정에 대한 명령줄에서 `export` 명령 또는 컴퓨터 수준 환경 설정에 대한 *bash_profile* 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-176">For Linux distros, use the `export` command at the command line for session based variable settings and *bash_profile* file for machine level environment settings.</span></span>

### <a name="configuration-by-environment"></a><span data-ttu-id="222f1-177">환경별 구성</span><span class="sxs-lookup"><span data-stu-id="222f1-177">Configuration by environment</span></span>

<span data-ttu-id="222f1-178">자세한 내용은 [환경에 의한 구성](xref:fundamentals/configuration/index#configuration-by-environment)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="222f1-178">See [Configuration by environment](xref:fundamentals/configuration/index#configuration-by-environment) for more information.</span></span>

<a name="startup-conventions"></a>
## <a name="environment-based-startup-class-and-methods"></a><span data-ttu-id="222f1-179">환경에 따른 시작 클래스 및 메서드</span><span class="sxs-lookup"><span data-stu-id="222f1-179">Environment based Startup class and methods</span></span>

<span data-ttu-id="222f1-180">ASP.NET Core 앱이 시작되면 [시작 클래스](xref:fundamentals/startup)가 앱을 부트스트랩합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-180">When an ASP.NET Core app starts, the [Startup class](xref:fundamentals/startup) bootstraps the app.</span></span> <span data-ttu-id="222f1-181">`Startup{EnvironmentName}` 클래스가 존재하는 경우 해당 클래스가 `EnvironmentName`에 대해 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-181">If a class `Startup{EnvironmentName}` exists, that class will be called for that `EnvironmentName`:</span></span>

[!code-csharp[Main](environments/sample/WebApp1/StartupDev.cs?name=snippet&highlight=1)]

<span data-ttu-id="222f1-182">참고: [WebHostBuilder.UseStartup<TStartup>](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_)을 호출하면 구성 섹션을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-182">Note: Calling [WebHostBuilder.UseStartup<TStartup>](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) overrides configuration sections.</span></span>

<span data-ttu-id="222f1-183">[Configure](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_StartupBase_Configure_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 및 [ConfigureServices](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices?view=aspnetcore-2.0)는 `Configure{EnvironmentName}` 및 `Configure{EnvironmentName}Services` 양식의 환경 특정 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="222f1-183">[Configure](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_StartupBase_Configure_Microsoft_AspNetCore_Builder_IApplicationBuilder_) and [ConfigureServices](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices?view=aspnetcore-2.0) support environment specific versions of the form `Configure{EnvironmentName}` and `Configure{EnvironmentName}Services`:</span></span>

[!code-csharp[Main](environments/sample/WebApp1/Startup.cs?name=snippet_all&highlight=15,37)]

## <a name="additional-resources"></a><span data-ttu-id="222f1-184">추가 자료</span><span class="sxs-lookup"><span data-stu-id="222f1-184">Additional resources</span></span>

* [<span data-ttu-id="222f1-185">응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="222f1-185">Application startup</span></span>](xref:fundamentals/startup)
* [<span data-ttu-id="222f1-186">구성</span><span class="sxs-lookup"><span data-stu-id="222f1-186">Configuration</span></span>](xref:fundamentals/configuration/index)
* [<span data-ttu-id="222f1-187">IHostingEnvironment.EnvironmentName</span><span class="sxs-lookup"><span data-stu-id="222f1-187">IHostingEnvironment.EnvironmentName</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_IHostingEnvironment_EnvironmentName)
