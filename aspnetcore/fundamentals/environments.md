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
ms.openlocfilehash: 83d1593d46761b1c00aa431cfdcde59cb3b28b65
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="working-with-multiple-environments"></a><span data-ttu-id="9ffa4-103">여러 환경 작업</span><span class="sxs-lookup"><span data-stu-id="9ffa4-103">Working with multiple environments</span></span>

<span data-ttu-id="9ffa4-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="9ffa4-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="9ffa4-105">ASP.NET Core를 환경 변수와 런타임 시 응용 프로그램 동작을 설정 하기 위한 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-105">ASP.NET Core provides support for setting application behavior at runtime with environment variables.</span></span>

<span data-ttu-id="9ffa4-106">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/environments/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="9ffa4-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/environments/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="environments"></a><span data-ttu-id="9ffa4-107">환경</span><span class="sxs-lookup"><span data-stu-id="9ffa4-107">Environments</span></span>

<span data-ttu-id="9ffa4-108">ASP.NET Core 환경 변수를 읽는 `ASPNETCORE_ENVIRONMENT` 응용 프로그램 시작 및 값 저장소에서 [IHostingEnvironment.EnvironmentName](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_IHostingEnvironment_EnvironmentName)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-108">ASP.NET Core reads the environment variable `ASPNETCORE_ENVIRONMENT` at application startup and stores that value in [IHostingEnvironment.EnvironmentName](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_IHostingEnvironment_EnvironmentName).</span></span> <span data-ttu-id="9ffa4-109">`ASPNETCORE_ENVIRONMENT`임의의 값으로 설정할 수 있지만 [3 개의 값](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname?view=aspnetcore-2.0) 프레임 워크에서 지원 됩니다: [개발](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.development?view=aspnetcore-2.0), [준비](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.staging?view=aspnetcore-2.0), 및 [프로덕션](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.production?view=aspnetcore-2.0)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-109">`ASPNETCORE_ENVIRONMENT` can be set to any value, but [three values](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname?view=aspnetcore-2.0) are supported by the framework: [Development](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.development?view=aspnetcore-2.0), [Staging](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.staging?view=aspnetcore-2.0), and [Production](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.environmentname.production?view=aspnetcore-2.0).</span></span> <span data-ttu-id="9ffa4-110">경우 `ASPNETCORE_ENVIRONMENT` 값은 기본적으로 설정 되어 있지 않은 `Production`합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-110">If `ASPNETCORE_ENVIRONMENT` is not set, it will default to `Production`.</span></span>

[!code-csharp[Main](environments/sample/WebApp1/Startup.cs?name=snippet)]

<span data-ttu-id="9ffa4-111">위의 코드:</span><span class="sxs-lookup"><span data-stu-id="9ffa4-111">The preceding code:</span></span>

* <span data-ttu-id="9ffa4-112">호출 [UseDeveloperExceptionPage](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.developerexceptionpageextensions.usedeveloperexceptionpage?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_DeveloperExceptionPageExtensions_UseDeveloperExceptionPage_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 및 [UseBrowserLink](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.browserlinkextensions.usebrowserlink?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_BrowserLinkExtensions_UseBrowserLink_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 때 `ASPNETCORE_ENVIRONMENT` 로 설정 된 `Development`합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-112">Calls [UseDeveloperExceptionPage](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.developerexceptionpageextensions.usedeveloperexceptionpage?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_DeveloperExceptionPageExtensions_UseDeveloperExceptionPage_Microsoft_AspNetCore_Builder_IApplicationBuilder_) and [UseBrowserLink](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.browserlinkextensions.usebrowserlink?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_BrowserLinkExtensions_UseBrowserLink_Microsoft_AspNetCore_Builder_IApplicationBuilder_) when `ASPNETCORE_ENVIRONMENT` is set to `Development`.</span></span>
* <span data-ttu-id="9ffa4-113">호출 [UseExceptionHandler](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.exceptionhandlerextensions.useexceptionhandler?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_ExceptionHandlerExtensions_UseExceptionHandler_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 때의 값 `ASPNETCORE_ENVIRONMENT` 다음 중 하나를 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-113">Calls [UseExceptionHandler](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.builder.exceptionhandlerextensions.useexceptionhandler?view=aspnetcore-2.0#Microsoft_AspNetCore_Builder_ExceptionHandlerExtensions_UseExceptionHandler_Microsoft_AspNetCore_Builder_IApplicationBuilder_) when the value of `ASPNETCORE_ENVIRONMENT` is set one of the following:</span></span>

    * `Staging`
    * `Production`
    * `Staging_2`

<span data-ttu-id="9ffa4-114">[환경 태그 도우미 ](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper) 의 값을 사용 하 여 `IHostingEnvironment.EnvironmentName` 포함 하거나 제외할 요소의 태그:</span><span class="sxs-lookup"><span data-stu-id="9ffa4-114">The [Environment Tag Helper ](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper) uses the value of `IHostingEnvironment.EnvironmentName` to include or exclude markup in the element:</span></span>

[!code-html[Main](environments/sample/WebApp1/Pages/About.cshtml)]

<span data-ttu-id="9ffa4-115">참고: Windows와 macOS에서 환경 변수와 값은 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-115">Note: On Windows and macOS, environment variables and values are not case sensitive.</span></span> <span data-ttu-id="9ffa4-116">Linux 환경 변수와 값은 **대/소문자 구분** 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-116">Linux environment variables and values are **case sensitive** by default.</span></span>

### <a name="development"></a><span data-ttu-id="9ffa4-117">개발</span><span class="sxs-lookup"><span data-stu-id="9ffa4-117">Development</span></span>

<span data-ttu-id="9ffa4-118">개발 환경 프로덕션 환경에서 노출 되지 않아야 하는 기능을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-118">The development environment can enable features that should not be exposed in production.</span></span> <span data-ttu-id="9ffa4-119">ASP.NET Core 템플릿을 사용 하는 예를 들어는 [개발자 예외 페이지](xref:fundamentals/error-handling#the-developer-exception-page) 개발 환경에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-119">For example, the ASP.NET Core templates enable the [developer exception page](xref:fundamentals/error-handling#the-developer-exception-page) in the development environment.</span></span>

<span data-ttu-id="9ffa4-120">로컬 컴퓨터 개발을 위한 환경에서 설정할 수 있습니다는 *Properties\launchSettings.json* 프로젝트의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-120">The environment for local machine development can be set in the *Properties\launchSettings.json* file of the project.</span></span> <span data-ttu-id="9ffa4-121">환경 값으로 설정할 *launchSettings.json* 시스템 환경에서 설정 값을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-121">Environment values set in *launchSettings.json* override values set in the system environment.</span></span>

<span data-ttu-id="9ffa4-122">다음 XML에서 프로필이 3 개를 보여 줍니다.는 *launchSettings.json* 파일:</span><span class="sxs-lookup"><span data-stu-id="9ffa4-122">The following XML shows three profiles from a *launchSettings.json* file:</span></span>

[!code-xml[Main](environments/sample/WebApp1/Properties/launchSettings.json?highlight=10,11,18,26)]

<span data-ttu-id="9ffa4-123">응용 프로그램으로 시작 될 때 `dotnet run`를 사용 하 여 첫 번째 프로필 `"commandName": "Project"` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-123">When the application is launched with `dotnet run`, the first profile with `"commandName": "Project"` will be used.</span></span> <span data-ttu-id="9ffa4-124">값 `commandName` 를 시작 하려면 웹 서버를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-124">The value of `commandName` specifies the web server to launch.</span></span> <span data-ttu-id="9ffa4-125">`commandName`하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-125">`commandName` can be one of :</span></span>

* <span data-ttu-id="9ffa4-126">IIS Express</span><span class="sxs-lookup"><span data-stu-id="9ffa4-126">IIS Express</span></span>
* <span data-ttu-id="9ffa4-127">IIS</span><span class="sxs-lookup"><span data-stu-id="9ffa4-127">IIS</span></span>
* <span data-ttu-id="9ffa4-128">프로젝트 (시작 하는 Kestrel)</span><span class="sxs-lookup"><span data-stu-id="9ffa4-128">Project (which launches Kestrel)</span></span>

<span data-ttu-id="9ffa4-129">응용 프로그램으로 시작 될 때 `dotnet run`:</span><span class="sxs-lookup"><span data-stu-id="9ffa4-129">When an app is launched with `dotnet run`:</span></span>

* <span data-ttu-id="9ffa4-130">*launchSettings.json* 읽기 가능한 경우.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-130">*launchSettings.json* is read if available.</span></span> <span data-ttu-id="9ffa4-131">`environmentVariables`설정 *launchSettings.json* 환경 변수 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-131">`environmentVariables` settings in *launchSettings.json* override environment variables.</span></span>
* <span data-ttu-id="9ffa4-132">호스팅 환경이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-132">The hosting environment is displayed.</span></span>


<span data-ttu-id="9ffa4-133">다음과 같은 출력을 시작 하는 응용 프로그램을 보여 줍니다. `dotnet run`:</span><span class="sxs-lookup"><span data-stu-id="9ffa4-133">The following output shows an app started with `dotnet run`:</span></span>
```bash
PS C:\Webs\WebApp1> dotnet run
Using launch settings from C:\Webs\WebApp1\Properties\launchSettings.json...
Hosting environment: Staging
Content root path: C:\Webs\WebApp1
Now listening on: http://localhost:54340
Application started. Press Ctrl+C to shut down.
```

<span data-ttu-id="9ffa4-134">Visual Studio **디버그** 탭 편집 하려면 GUI에서는 제공 된 *launchSettings.json* 파일:</span><span class="sxs-lookup"><span data-stu-id="9ffa4-134">The Visual Studio **Debug** tab provides a GUI to edit the *launchSettings.json* file:</span></span>

![프로젝트 속성 설정 환경 변수](environments/_static/project-properties-debug.png)

<span data-ttu-id="9ffa4-136">웹 서버를 다시 시작 될 때까지 프로젝트 프로필의 변경 내용이 적용 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-136">Changes made to project profiles may not take effect until the web server is restarted.</span></span> <span data-ttu-id="9ffa4-137">해당 환경에 대해 변경 내용을 감지 합니다 kestrel은 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-137">Kestrel must be restarted before it will detect changes made to its environment.</span></span>

>[!WARNING]
> <span data-ttu-id="9ffa4-138">*launchSettings.json* 비밀 정보를 저장 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-138">*launchSettings.json* should not store secrets.</span></span> <span data-ttu-id="9ffa4-139">[암호 관리자 도구](xref:security/app-secrets) 로컬 개발에 대 한 암호를 저장 하기 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-139">The [Secret Manager tool](xref:security/app-secrets) can be used to store secrets for local development.</span></span>

### <a name="production"></a><span data-ttu-id="9ffa4-140">프로덕션</span><span class="sxs-lookup"><span data-stu-id="9ffa4-140">Production</span></span>

<span data-ttu-id="9ffa4-141">프로덕션 환경 보안, 성능 및 응용 프로그램의 견고성을 최대화 하기 위해 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-141">The production environment should be configured to maximize security, performance, and application robustness.</span></span> <span data-ttu-id="9ffa4-142">다음과 같은 몇 가지 일반적인 프로덕션 환경에 있을 수 있는 것 다른 설정을 개발</span><span class="sxs-lookup"><span data-stu-id="9ffa4-142">Some common settings that a production environment might have that would differ from development include:</span></span>

* <span data-ttu-id="9ffa4-143">캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-143">Caching.</span></span>
* <span data-ttu-id="9ffa4-144">클라이언트 쪽 리소스가 번들로 제공 하 고, 축소 하 고 잠재적으로 CDN에서 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-144">Client-side resources are bundled, minified, and potentially served from a CDN.</span></span>
* <span data-ttu-id="9ffa4-145">진단 오류 페이지를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-145">Diagnostic error pages disabled.</span></span>
* <span data-ttu-id="9ffa4-146">오류 페이지를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-146">Friendly error pages enabled.</span></span>
* <span data-ttu-id="9ffa4-147">프로덕션 로깅 및 모니터링 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-147">Production logging and monitoring enabled.</span></span> <span data-ttu-id="9ffa4-148">예를 들어 [Application Insights](https://azure.microsoft.com/documentation/articles/app-insights-asp-net-five/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-148">For example, [Application Insights](https://azure.microsoft.com/documentation/articles/app-insights-asp-net-five/).</span></span>

## <a name="setting-the-environment"></a><span data-ttu-id="9ffa4-149">환경 설정</span><span class="sxs-lookup"><span data-stu-id="9ffa4-149">Setting the environment</span></span>

<span data-ttu-id="9ffa4-150">테스트 하기 위한 특정 환경을 설정 하는 것이 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-150">It's often useful to set a specific environment for testing.</span></span> <span data-ttu-id="9ffa4-151">환경 설정 되어 있지 않으면 기본적으로 선택 됩니다 `Production` 는 대부분의 디버깅 기능을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-151">If the environment is not set, it will default to `Production` which disables most debugging features.</span></span>

<span data-ttu-id="9ffa4-152">환경 설정에 대 한 메서드는 운영 체제에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-152">The method for setting the environment depends on the operating system.</span></span>

### <a name="azure"></a><span data-ttu-id="9ffa4-153">Azure</span><span class="sxs-lookup"><span data-stu-id="9ffa4-153">Azure</span></span>

<span data-ttu-id="9ffa4-154">Azure 앱 서비스:</span><span class="sxs-lookup"><span data-stu-id="9ffa4-154">For Azure app service:</span></span>

* <span data-ttu-id="9ffa4-155">선택 된 **응용 프로그램 설정** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-155">Select the **Application settings** blade.</span></span>
* <span data-ttu-id="9ffa4-156">키를 추가 하 고 값 **앱 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-156">Add the key and value in **App settings**.</span></span>


### <a name="windows"></a><span data-ttu-id="9ffa4-157">Windows</span><span class="sxs-lookup"><span data-stu-id="9ffa4-157">Windows</span></span>
<span data-ttu-id="9ffa4-158">설정 하는 `ASPNETCORE_ENVIRONMENT` 를 사용 하 여 앱이 시작 하는 경우 현재 세션에 대 한 `dotnet run`, 다음 명령을 사용 하는</span><span class="sxs-lookup"><span data-stu-id="9ffa4-158">To set the `ASPNETCORE_ENVIRONMENT` for the current session, if the app is started using `dotnet run`, the following commands are used</span></span>

<span data-ttu-id="9ffa4-159">**명령줄**</span><span class="sxs-lookup"><span data-stu-id="9ffa4-159">**Command line**</span></span>
```
set ASPNETCORE_ENVIRONMENT=Development
```
<span data-ttu-id="9ffa4-160">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="9ffa4-160">**PowerShell**</span></span>
```
$Env:ASPNETCORE_ENVIRONMENT = "Development"
```

<span data-ttu-id="9ffa4-161">이 명령은 현재 창에 대해서만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-161">These commands take effect only for the current window.</span></span> <span data-ttu-id="9ffa4-162">창이 닫히면 ASPNETCORE_ENVIRONMENT 설정을 기본 설정 또는 컴퓨터 값 되돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-162">When the window is closed, the ASPNETCORE_ENVIRONMENT setting reverts to the default setting or machine value.</span></span> <span data-ttu-id="9ffa4-163">Windows 열 값을 전역으로 설정 된 **제어판** > **시스템** > **고급 시스템 설정** 추가 하거나는 편집`ASPNETCORE_ENVIRONMENT` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-163">In order to set the value globally on Windows open the **Control Panel** > **System** > **Advanced system settings** and add or edit the `ASPNETCORE_ENVIRONMENT` value.</span></span>

![시스템의 고급 속성](environments/_static/systemsetting_environment.png)

![ASPNET 코어 환경 변수](environments/_static/windows_aspnetcore_environment.png)


<span data-ttu-id="9ffa4-166">**web.config**</span><span class="sxs-lookup"><span data-stu-id="9ffa4-166">**web.config**</span></span>

<span data-ttu-id="9ffa4-167">참조는 *환경 변수 설정* 의 섹션은 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module#setting-environment-variables) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-167">See the *Setting environment variables* section of the [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module#setting-environment-variables) topic.</span></span>

<span data-ttu-id="9ffa4-168">**IIS 응용 프로그램 풀 당**</span><span class="sxs-lookup"><span data-stu-id="9ffa4-168">**Per IIS Application Pool**</span></span>

<span data-ttu-id="9ffa4-169">격리 된 응용 프로그램 풀 (IIS 10.0 이상에서 지원 됨)에서 실행 되는 개별 앱에 대 한 환경 변수를 설정 하려면 참조는 *AppCmd.exe 명령을* 의 섹션은 [환경 변수 \< environmentVariables >](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-169">To set environment variables for individual apps running in isolated Application Pools (supported on IIS 10.0+), see the *AppCmd.exe command* section of the [Environment Variables \<environmentVariables>](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) topic.</span></span>

### <a name="macos"></a><span data-ttu-id="9ffa4-170">macOS</span><span class="sxs-lookup"><span data-stu-id="9ffa4-170">macOS</span></span>
<span data-ttu-id="9ffa4-171">MacOS에 대 한 현재 환경 설정 구성 방법은 인라인 응용 프로그램을 실행 하는 경우</span><span class="sxs-lookup"><span data-stu-id="9ffa4-171">Setting the current environment for macOS can be done in-line when running the application;</span></span>

```bash
ASPNETCORE_ENVIRONMENT=Development dotnet run
```
<span data-ttu-id="9ffa4-172">사용 하 여 또는 `export` 응용 프로그램을 실행 하기 전에 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-172">or using `export` to set it prior to running the app.</span></span>

```bash
export ASPNETCORE_ENVIRONMENT=Development
```
<span data-ttu-id="9ffa4-173">시스템 수준 환경 변수 설정는 *.bashrc* 또는 *.bash_profile* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-173">Machine level environment variables are set in the *.bashrc* or *.bash_profile* file.</span></span> <span data-ttu-id="9ffa4-174">임의의 텍스트 편집기를 사용 하 여 파일을 편집 하 고 다음 문을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-174">Edit the file using any text editor and add the following statment.</span></span>

```
export ASPNETCORE_ENVIRONMENT=Development
```

### <a name="linux"></a><span data-ttu-id="9ffa4-175">Linux</span><span class="sxs-lookup"><span data-stu-id="9ffa4-175">Linux</span></span>
<span data-ttu-id="9ffa4-176">사용 하 여 Linux 배포판는 `export` 세션 변수 설정을 기반으로 하는 명령줄에서 명령 및 *bash_profile* 시스템 수준 환경 설정에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-176">For Linux distros, use the `export` command at the command line for session based variable settings and *bash_profile* file for machine level environment settings.</span></span>

### <a name="configuration-by-environment"></a><span data-ttu-id="9ffa4-177">환경별 구성</span><span class="sxs-lookup"><span data-stu-id="9ffa4-177">Configuration by environment</span></span>

<span data-ttu-id="9ffa4-178">참조 [환경에 의해 구성](xref:fundamentals/configuration/index#configuration-by-environment) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-178">See [Configuration by environment](xref:fundamentals/configuration/index#configuration-by-environment) for more information.</span></span>

<a name="startup-conventions"></a>
## <a name="environment-based-startup-class-and-methods"></a><span data-ttu-id="9ffa4-179">환경에 따라 시작 클래스 및 메서드</span><span class="sxs-lookup"><span data-stu-id="9ffa4-179">Environment based Startup class and methods</span></span>

<span data-ttu-id="9ffa4-180">ASP.NET Core 응용 프로그램 시작 되 면는 [시작 클래스](xref:fundamentals/startup) 응용 프로그램 시작 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-180">When an ASP.NET Core app starts, the [Startup class](xref:fundamentals/startup) bootstraps the app.</span></span> <span data-ttu-id="9ffa4-181">클래스 `Startup{EnvironmentName}` 는 클래스를 호출할 수 있는 `EnvironmentName`:</span><span class="sxs-lookup"><span data-stu-id="9ffa4-181">If a class `Startup{EnvironmentName}` exists, that class will be called for that `EnvironmentName`:</span></span>

[!code-csharp[Main](environments/sample/WebApp1/StartupDev.cs?name=snippet&highlight=1)]

<span data-ttu-id="9ffa4-182">참고: 호출 [WebHostBuilder.UseStartup<TStartup> ](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) 구성 섹션을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-182">Note: Calling [WebHostBuilder.UseStartup<TStartup>](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) overrides configuration sections.</span></span>

<span data-ttu-id="9ffa4-183">[구성](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_StartupBase_Configure_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 및 [ConfigureServices](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices?view=aspnetcore-2.0) 환경 폼의 특정 버전을 지원 `Configure{EnvironmentName}` 및 `Configure{EnvironmentName}Services`:</span><span class="sxs-lookup"><span data-stu-id="9ffa4-183">[Configure](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_StartupBase_Configure_Microsoft_AspNetCore_Builder_IApplicationBuilder_) and [ConfigureServices](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices?view=aspnetcore-2.0) support environment specific versions of the form `Configure{EnvironmentName}` and `Configure{EnvironmentName}Services`:</span></span>

[!code-csharp[Main](environments/sample/WebApp1/Startup.cs?name=snippet_all&highlight=15,37)]

## <a name="additional-resources"></a><span data-ttu-id="9ffa4-184">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="9ffa4-184">Additional Resources</span></span>

* [<span data-ttu-id="9ffa4-185">응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="9ffa4-185">Application startup</span></span>](xref:fundamentals/startup)
* [<span data-ttu-id="9ffa4-186">구성</span><span class="sxs-lookup"><span data-stu-id="9ffa4-186">Configuration</span></span>](xref:fundamentals/configuration/index)
* [<span data-ttu-id="9ffa4-187">IHostingEnvironment.EnvironmentName</span><span class="sxs-lookup"><span data-stu-id="9ffa4-187">IHostingEnvironment.EnvironmentName</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname?view=aspnetcore-2.0#Microsoft_AspNetCore_Hosting_IHostingEnvironment_EnvironmentName)
