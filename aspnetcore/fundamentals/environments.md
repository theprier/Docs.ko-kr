---
title: ASP.NET Core에서 여러 환경 사용
author: rick-anderson
description: ASP.NET Core 앱의 여러 환경에서 앱 동작을 제어하는 방법에 대해 알아봅니다.
ms.author: riande
ms.date: 06/21/2018
uid: fundamentals/environments
ms.openlocfilehash: 505f19d8b4df6e476b46a1fe7c49872d3c4acc1a
ms.sourcegitcommit: e22097b84d26a812cd1380a6b2d12c93e522c125
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/22/2018
ms.locfileid: "36314106"
---
# <a name="use-multiple-environments-in-aspnet-core"></a><span data-ttu-id="9e43a-103">ASP.NET Core에서 여러 환경 사용</span><span class="sxs-lookup"><span data-stu-id="9e43a-103">Use multiple environments in ASP.NET Core</span></span>

<span data-ttu-id="9e43a-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="9e43a-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="9e43a-105">ASP.NET Core는 환경 변수를 사용하여 런타임 환경에 따라 앱 동작을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-105">ASP.NET Core configures app behavior based on the runtime environment using an environment variable.</span></span>

<span data-ttu-id="9e43a-106">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/environments/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="9e43a-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/environments/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="environments"></a><span data-ttu-id="9e43a-107">환경</span><span class="sxs-lookup"><span data-stu-id="9e43a-107">Environments</span></span>

<span data-ttu-id="9e43a-108">ASP.NET Core는 앱 시작 시 환경 변수 `ASPNETCORE_ENVIRONMENT`를 읽고 [IHostingEnvironment.EnvironmentName](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname)에 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-108">ASP.NET Core reads the environment variable `ASPNETCORE_ENVIRONMENT` at app startup and stores the value in [IHostingEnvironment.EnvironmentName](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname).</span></span> <span data-ttu-id="9e43a-109">`ASPNETCORE_ENVIRONMENT`는 임의의 값으로 설정할 수 있지만 [개발](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.development), [준비](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.staging) 및 [프로덕션](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.production)의 [3개 값](/dotnet/api/microsoft.aspnetcore.hosting.environmentname)은 프레임워크에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-109">You can set `ASPNETCORE_ENVIRONMENT` to any value, but [three values](/dotnet/api/microsoft.aspnetcore.hosting.environmentname) are supported by the framework: [Development](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.development), [Staging](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.staging), and [Production](/dotnet/api/microsoft.aspnetcore.hosting.environmentname.production).</span></span> <span data-ttu-id="9e43a-110">`ASPNETCORE_ENVIRONMENT`가 설정되지 않은 경우 기본값은 `Production`입니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-110">If `ASPNETCORE_ENVIRONMENT` isn't set, it defaults to `Production`.</span></span>

[!code-csharp[](environments/sample/WebApp1/Startup.cs?name=snippet)]

<span data-ttu-id="9e43a-111">위의 코드:</span><span class="sxs-lookup"><span data-stu-id="9e43a-111">The preceding code:</span></span>

* <span data-ttu-id="9e43a-112">`ASPNETCORE_ENVIRONMENT`가 `Development`로 설정된 경우 [UseDeveloperExceptionPage](/dotnet/api/microsoft.aspnetcore.builder.developerexceptionpageextensions.usedeveloperexceptionpage) 및 [UseBrowserLink](/dotnet/api/microsoft.aspnetcore.builder.browserlinkextensions.usebrowserlink)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-112">Calls [UseDeveloperExceptionPage](/dotnet/api/microsoft.aspnetcore.builder.developerexceptionpageextensions.usedeveloperexceptionpage) and [UseBrowserLink](/dotnet/api/microsoft.aspnetcore.builder.browserlinkextensions.usebrowserlink) when `ASPNETCORE_ENVIRONMENT` is set to `Development`.</span></span>
* <span data-ttu-id="9e43a-113">`ASPNETCORE_ENVIRONMENT`의 값이 다음 중 하나로 설정된 경우 [UseExceptionHandler](/dotnet/api/microsoft.aspnetcore.builder.exceptionhandlerextensions.useexceptionhandler)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-113">Calls [UseExceptionHandler](/dotnet/api/microsoft.aspnetcore.builder.exceptionhandlerextensions.useexceptionhandler) when the value of `ASPNETCORE_ENVIRONMENT` is set one of the following:</span></span>

    * `Staging`
    * `Production`
    * `Staging_2`

<span data-ttu-id="9e43a-114">[환경 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)는 `IHostingEnvironment.EnvironmentName`의 값을 사용하여 요소에 표시를 포함하거나 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-114">The [Environment Tag Helper](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper) uses the value of `IHostingEnvironment.EnvironmentName` to include or exclude markup in the element:</span></span>

[!code-cshtml[](environments/sample-snapshot/WebApp1/Pages/About.cshtml)]

<span data-ttu-id="9e43a-115">Windows와 macOS에서 환경 변수 및 값은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-115">On Windows and macOS, environment variables and values aren't case sensitive.</span></span> <span data-ttu-id="9e43a-116">Linux 환경 변수 및 값은 기본적으로 **대/소문자를 구분**합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-116">Linux environment variables and values are **case sensitive** by default.</span></span>

### <a name="development"></a><span data-ttu-id="9e43a-117">개발</span><span class="sxs-lookup"><span data-stu-id="9e43a-117">Development</span></span>

<span data-ttu-id="9e43a-118">개발 환경은 프로덕션에서 노출해서는 안 되는 기능을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-118">The development environment can enable features that shouldn't be exposed in production.</span></span> <span data-ttu-id="9e43a-119">예를 들어 ASP.NET Core 템플릿은 개발 환경에서 [개발자 예외 페이지](xref:fundamentals/error-handling#the-developer-exception-page)를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-119">For example, the ASP.NET Core templates enable the [developer exception page](xref:fundamentals/error-handling#the-developer-exception-page) in the development environment.</span></span>

<span data-ttu-id="9e43a-120">로컬 컴퓨터 개발을 위한 환경은 프로젝트의 *Properties\launchSettings.json* 파일에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-120">The environment for local machine development can be set in the *Properties\launchSettings.json* file of the project.</span></span> <span data-ttu-id="9e43a-121">*launchSettings.json*의 환경 값은 시스템 환경에서 설정된 값을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-121">Environment values set in *launchSettings.json* override values set in the system environment.</span></span>

<span data-ttu-id="9e43a-122">다음 JSON에는 *launchSettings.json* 파일의 세 가지 프로필이 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-122">The following JSON shows three profiles from a *launchSettings.json* file:</span></span>

[!code-json[](environments/sample/WebApp1/Properties/launchSettings.json?highlight=10,11,18,26)]

::: moniker range=">= aspnetcore-2.1"

> [!NOTE]
> <span data-ttu-id="9e43a-123">*launchSettings.json*의 `applicationUrl` 속성은 서버 URL의 목록을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-123">The `applicationUrl` property in *launchSettings.json* can specify a list of server URLs.</span></span> <span data-ttu-id="9e43a-124">목록의 URL 사이에 세미콜론을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-124">Use a semicolon between the URLs in the list:</span></span>
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

<span data-ttu-id="9e43a-125">[dotnet run](/dotnet/core/tools/dotnet-run)을 사용하여 앱을 시작하면 `"commandName": "Project"`를 포함한 첫 번째 프로필이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-125">When the app is launched with [dotnet run](/dotnet/core/tools/dotnet-run), the first profile with `"commandName": "Project"` is used.</span></span> <span data-ttu-id="9e43a-126">`commandName`의 값은 시작할 웹 서버를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-126">The value of `commandName` specifies the web server to launch.</span></span> <span data-ttu-id="9e43a-127">`commandName`은 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-127">`commandName` can be any one of the following:</span></span>

* <span data-ttu-id="9e43a-128">IIS Express</span><span class="sxs-lookup"><span data-stu-id="9e43a-128">IIS Express</span></span>
* <span data-ttu-id="9e43a-129">IIS</span><span class="sxs-lookup"><span data-stu-id="9e43a-129">IIS</span></span>
* <span data-ttu-id="9e43a-130">프로젝트(Kestrel을 시작)</span><span class="sxs-lookup"><span data-stu-id="9e43a-130">Project (which launches Kestrel)</span></span>

<span data-ttu-id="9e43a-131">앱이 [dotnet run](/dotnet/core/tools/dotnet-run)으로 시작하는 경우:</span><span class="sxs-lookup"><span data-stu-id="9e43a-131">When an app is launched with [dotnet run](/dotnet/core/tools/dotnet-run):</span></span>

* <span data-ttu-id="9e43a-132">가능한 경우 *launchSettings.json*을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-132">*launchSettings.json* is read if available.</span></span> <span data-ttu-id="9e43a-133">*launchSettings.json*의 `environmentVariables` 설정은 환경 변수를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-133">`environmentVariables` settings in *launchSettings.json* override environment variables.</span></span>
* <span data-ttu-id="9e43a-134">호스팅 환경이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-134">The hosting environment is displayed.</span></span>

<span data-ttu-id="9e43a-135">다음 출력은 [dotnet run](/dotnet/core/tools/dotnet-run)으로 시작되는 앱을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-135">The following output shows an app started with [dotnet run](/dotnet/core/tools/dotnet-run):</span></span>

```bash
PS C:\Webs\WebApp1> dotnet run
Using launch settings from C:\Webs\WebApp1\Properties\launchSettings.json...
Hosting environment: Staging
Content root path: C:\Webs\WebApp1
Now listening on: http://localhost:54340
Application started. Press Ctrl+C to shut down.
```

<span data-ttu-id="9e43a-136">Visual Studio **Debug** 탭은 *launchSettings.json* 파일을 편집할 수 있는 GUI를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-136">The Visual Studio **Debug** tab provides a GUI to edit the *launchSettings.json* file:</span></span>

![프로젝트 속성 설정 환경 변수](environments/_static/project-properties-debug.png)

<span data-ttu-id="9e43a-138">웹 서버가 다시 시작되기 전에는 프로젝트 프로필의 변경 내용이 적용되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-138">Changes made to project profiles may not take effect until the web server is restarted.</span></span> <span data-ttu-id="9e43a-139">해당 환경에 대한 변경 내용을 감지하려면 Kestrel을 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-139">Kestrel must be restarted before it can detect changes made to its environment.</span></span>

> [!WARNING]
> <span data-ttu-id="9e43a-140">*launchSettings.json*은 암호를 저장하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-140">*launchSettings.json* shouldn't store secrets.</span></span> <span data-ttu-id="9e43a-141">[암호 관리자 도구](xref:security/app-secrets)를 사용하여 로컬 개발에 대한 암호를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-141">The [Secret Manager tool](xref:security/app-secrets) can be used to store secrets for local development.</span></span>

<span data-ttu-id="9e43a-142">[Visual Studio Code](https://code.visualstudio.com/)를 사용하는 경우 환경 변수는 *.vscode/launch.json* 파일에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-142">When using [Visual Studio Code](https://code.visualstudio.com/), environment variables can be set in the *.vscode/launch.json* file.</span></span> <span data-ttu-id="9e43a-143">다음 예제에서는 환경을 `Development`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-143">The following example sets the environment to `Development`:</span></span>

```json
{
   "version": "0.2.0",
   "configurations": [
        {
            "name": ".NET Core Launch (web)",

            ... additional VS Code configuration settings ...

            "env": {
                "ASPNETCORE_ENVIRONMENT": "Development"
            }
        }
    ]
}
```

<span data-ttu-id="9e43a-144">*Properties/launchSettings.json*과 같은 방식으로 `dotnet run`을 사용하여 앱을 시작할 때 프로젝트의 *.vscode/launch.json* 파일은 읽히지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-144">A *.vscode/launch.json* file in the project isn't read when starting the app with `dotnet run` in the same way as *Properties/launchSettings.json*.</span></span> <span data-ttu-id="9e43a-145">*launchSettings.json* 파일이 없는 개발 환경에서 앱을 시작할 때는 `dotnet run` 명령에 대한 환경 변수 또는 명령줄 인수로 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-145">When launching an app in development that doesn't have a *launchSettings.json* file, either set the environment with an environment variable or a command-line argument to the `dotnet run` command.</span></span>

### <a name="production"></a><span data-ttu-id="9e43a-146">프로덕션</span><span class="sxs-lookup"><span data-stu-id="9e43a-146">Production</span></span>

<span data-ttu-id="9e43a-147">프로덕션 환경은 보안, 성능 및 앱 견고성을 최대화하도록 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-147">The production environment should be configured to maximize security, performance, and app robustness.</span></span> <span data-ttu-id="9e43a-148">개발과 다른 몇 가지 일반적인 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-148">Some common settings that differ from development include:</span></span>

* <span data-ttu-id="9e43a-149">캐싱.</span><span class="sxs-lookup"><span data-stu-id="9e43a-149">Caching.</span></span>
* <span data-ttu-id="9e43a-150">클라이언트 쪽 리소스가 번들로 제공되고, 축소되며, 잠재적으로 CDN에서 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-150">Client-side resources are bundled, minified, and potentially served from a CDN.</span></span>
* <span data-ttu-id="9e43a-151">진단 오류 페이지를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-151">Diagnostic error pages disabled.</span></span>
* <span data-ttu-id="9e43a-152">친숙한 오류 페이지를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-152">Friendly error pages enabled.</span></span>
* <span data-ttu-id="9e43a-153">프로덕션 로깅 및 모니터링을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-153">Production logging and monitoring enabled.</span></span> <span data-ttu-id="9e43a-154">예: [Application Insights](/azure/application-insights/app-insights-asp-net-core).</span><span class="sxs-lookup"><span data-stu-id="9e43a-154">For example, [Application Insights](/azure/application-insights/app-insights-asp-net-core).</span></span>

## <a name="setting-the-environment"></a><span data-ttu-id="9e43a-155">환경 설정하기</span><span class="sxs-lookup"><span data-stu-id="9e43a-155">Setting the environment</span></span>

<span data-ttu-id="9e43a-156">테스트를 위해 특정 환경을 설정하는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-156">It's often useful to set a specific environment for testing.</span></span> <span data-ttu-id="9e43a-157">환경을 설정하지 않으면 대부분의 디버깅 기능을 사용하지 않는 `Production`으로 기본값이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-157">If the environment isn't set, it defaults to `Production`, which disables most debugging features.</span></span> <span data-ttu-id="9e43a-158">환경 설정에 대한 메서드는 운영 체제에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-158">The method for setting the environment depends on the operating system.</span></span>

### <a name="azure-app-service"></a><span data-ttu-id="9e43a-159">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="9e43a-159">Azure App Service</span></span>

<span data-ttu-id="9e43a-160">[Azure App Service](https://azure.microsoft.com/services/app-service/)에서 환경을 설정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-160">To set the environment in [Azure App Service](https://azure.microsoft.com/services/app-service/), perform the following steps:</span></span>

1. <span data-ttu-id="9e43a-161">**App Services** 블레이드에서 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-161">Select the app from the **App Services** blade.</span></span>
1. <span data-ttu-id="9e43a-162">**SETTINGS** 그룹에서 **응용 프로그램 설정** 블레이드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-162">In the **SETTINGS** group, select the **Application settings** blade.</span></span>
1. <span data-ttu-id="9e43a-163">**응용 프로그램 설정** 영역에서 **새 설정 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-163">In the **Application settings** area, select **Add new setting**.</span></span>
1. <span data-ttu-id="9e43a-164">**이름 입력**의 경우, `ASPNETCORE_ENVIRONMENT`를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-164">For **Enter a name**, provide `ASPNETCORE_ENVIRONMENT`.</span></span> <span data-ttu-id="9e43a-165">**값 입력**의 경우 환경을 제공합니다(예: `Staging`).</span><span class="sxs-lookup"><span data-stu-id="9e43a-165">For **Enter a value**, provide the environment (for example, `Staging`).</span></span>
1. <span data-ttu-id="9e43a-166">배포 슬롯을 교환할 때 환경 설정을 현재 슬롯으로 유지하려면 **슬롯 설정** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-166">Select the **Slot Setting** check box if you wish the environment setting to remain with the current slot when deployment slots are swapped.</span></span> <span data-ttu-id="9e43a-167">자세한 내용은 [Azure 설명서: 어떤 설정이 교환됩니까?](/azure/app-service/web-sites-staged-publishing)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9e43a-167">For more information, see [Azure Documentation: Which settings are swapped?](/azure/app-service/web-sites-staged-publishing).</span></span>
1. <span data-ttu-id="9e43a-168">블레이드 상단에서 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-168">Select **Save** at the top of the blade.</span></span>

<span data-ttu-id="9e43a-169">Azure App Service는 Azure Portal에서 앱 설정(환경 변수)이 추가, 변경 또는 삭제된 후 앱을 자동으로 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-169">Azure App Service automatically restarts the app after an app setting (environment variable) is added, changed, or deleted in the Azure portal.</span></span>

### <a name="windows"></a><span data-ttu-id="9e43a-170">Windows</span><span class="sxs-lookup"><span data-stu-id="9e43a-170">Windows</span></span>

<span data-ttu-id="9e43a-171">현재 세션에 `ASPNETCORE_ENVIRONMENT`를 설정하려면 앱이 [dotnet run](/dotnet/core/tools/dotnet-run)을 사용하여 시작할 때 다음 명령이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-171">To set the `ASPNETCORE_ENVIRONMENT` for the current session when the app is started using [dotnet run](/dotnet/core/tools/dotnet-run), the following commands are used:</span></span>

<span data-ttu-id="9e43a-172">**명령 프롬프트**</span><span class="sxs-lookup"><span data-stu-id="9e43a-172">**Command prompt**</span></span>

```console
set ASPNETCORE_ENVIRONMENT=Development
```

<span data-ttu-id="9e43a-173">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="9e43a-173">**PowerShell**</span></span>

```powershell
$Env:ASPNETCORE_ENVIRONMENT = "Development"
```

<span data-ttu-id="9e43a-174">이러한 명령은 현재 창에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-174">These commands only take effect for the current window.</span></span> <span data-ttu-id="9e43a-175">창이 닫히면 `ASPNETCORE_ENVIRONMENT` 설정이 기본 설정 또는 컴퓨터 값으로 되돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-175">When the window is closed, the `ASPNETCORE_ENVIRONMENT` setting reverts to the default setting or machine value.</span></span> <span data-ttu-id="9e43a-176">Windows에서 전역으로 값을 설정하려면 **제어판** > **시스템** > **고급 시스템 설정**을 열고 `ASPNETCORE_ENVIRONMENT` 값을 추가하거나 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-176">To set the value globally in Windows, open the **Control Panel** > **System** > **Advanced system settings** and add or edit the `ASPNETCORE_ENVIRONMENT` value:</span></span>

![시스템 고급 속성](environments/_static/systemsetting_environment.png)

![ASPNET Core 환경 변수](environments/_static/windows_aspnetcore_environment.png)

<span data-ttu-id="9e43a-179">**web.config**</span><span class="sxs-lookup"><span data-stu-id="9e43a-179">**web.config**</span></span>

<span data-ttu-id="9e43a-180">[ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module#setting-environment-variables) 주제의 *환경 변수 설정하기* 항목을 참고하시기 바랍니다</span><span class="sxs-lookup"><span data-stu-id="9e43a-180">See the *Setting environment variables* section of the [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module#setting-environment-variables) topic.</span></span>

<span data-ttu-id="9e43a-181">**IIS 응용 프로그램 풀마다**</span><span class="sxs-lookup"><span data-stu-id="9e43a-181">**Per IIS Application Pool**</span></span>

<span data-ttu-id="9e43a-182">격리된 응용 프로그램 풀에서 실행되는 (IIS 10.0 이상에서 지원됨) 개별 앱에 대한 환경 변수를 설정하려면, [ 환경 변수 &lt;environmentVariables&gt;](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) 항목의 *AppCmd.exe 명령* 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9e43a-182">To set environment variables for individual apps running in isolated Application Pools (supported on IIS 10.0+), see the *AppCmd.exe command* section of the [Environment Variables &lt;environmentVariables&gt;](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) topic.</span></span>

### <a name="macos"></a><span data-ttu-id="9e43a-183">macOS</span><span class="sxs-lookup"><span data-stu-id="9e43a-183">macOS</span></span>

<span data-ttu-id="9e43a-184">macOS에 대한 현재 환경 설정은 앱을 실행할 때 인라인으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-184">Setting the current environment for macOS can be performed in-line when running the app:</span></span>

```bash
ASPNETCORE_ENVIRONMENT=Development dotnet run
```

<span data-ttu-id="9e43a-185">또는 앱을 실행하기 전에 `export`를 사용하여 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-185">Alternatively, set the environment with `export` prior to running the app:</span></span>

```bash
export ASPNETCORE_ENVIRONMENT=Development
```

<span data-ttu-id="9e43a-186">컴퓨터 수준 환경 변수는 *.bashrc* 또는 *.bash_profile* 파일에서 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-186">Machine-level environment variables are set in the *.bashrc* or *.bash_profile* file.</span></span> <span data-ttu-id="9e43a-187">임의의 텍스트 편집기를 사용하여 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-187">Edit the file using any text editor.</span></span> <span data-ttu-id="9e43a-188">다음 명령문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-188">Add the following statement:</span></span>

```bash
export ASPNETCORE_ENVIRONMENT=Development
```

### <a name="linux"></a><span data-ttu-id="9e43a-189">Linux</span><span class="sxs-lookup"><span data-stu-id="9e43a-189">Linux</span></span>

<span data-ttu-id="9e43a-190">Linux 배포의 경우 세션 기반 변수 설정에 대한 명령 프롬프트에서 `export` 명령 또는 컴퓨터 수준 환경 설정에 대한 *bash_profile* 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-190">For Linux distros, use the `export` command at a command prompt for session-based variable settings and *bash_profile* file for machine-level environment settings.</span></span>

### <a name="configuration-by-environment"></a><span data-ttu-id="9e43a-191">환경별 구성</span><span class="sxs-lookup"><span data-stu-id="9e43a-191">Configuration by environment</span></span>

<span data-ttu-id="9e43a-192">자세한 내용은 [환경에 의한 구성](xref:fundamentals/configuration/index#configuration-by-environment)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9e43a-192">See [Configuration by environment](xref:fundamentals/configuration/index#configuration-by-environment) for more information.</span></span>

## <a name="environment-based-startup-class-and-methods"></a><span data-ttu-id="9e43a-193">환경에 따른 시작 클래스 및 메서드</span><span class="sxs-lookup"><span data-stu-id="9e43a-193">Environment-based Startup class and methods</span></span>

<span data-ttu-id="9e43a-194">ASP.NET Core 앱이 시작되면 [시작 클래스](xref:fundamentals/startup)가 앱을 부트스트랩합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-194">When an ASP.NET Core app starts, the [Startup class](xref:fundamentals/startup) bootstraps the app.</span></span> <span data-ttu-id="9e43a-195">`Startup{EnvironmentName}` 클래스가 존재하는 경우 해당 클래스가 `EnvironmentName`에 대해 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-195">If a `Startup{EnvironmentName}` class exists, the class is called for that `EnvironmentName`:</span></span>

[!code-csharp[](environments/sample/WebApp1/StartupDev.cs?name=snippet&highlight=1)]

<span data-ttu-id="9e43a-196">[WebHostBuilder.UseStartup<TStartup>](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_)은 구성 섹션을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-196">[WebHostBuilder.UseStartup<TStartup>](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.usestartup#Microsoft_AspNetCore_Hosting_WebHostBuilderExtensions_UseStartup__1_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) overrides configuration sections.</span></span>

<span data-ttu-id="9e43a-197">[Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) 및 [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices)는 `Configure{EnvironmentName}` 및 `Configure{EnvironmentName}Services` 양식의 환경 특정 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9e43a-197">[Configure](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configure) and [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.startupbase.configureservices) support environment-specific versions of the form `Configure{EnvironmentName}` and `Configure{EnvironmentName}Services`:</span></span>

[!code-csharp[](environments/sample/WebApp1/Startup.cs?name=snippet_all&highlight=15,37)]

## <a name="additional-resources"></a><span data-ttu-id="9e43a-198">추가 자료</span><span class="sxs-lookup"><span data-stu-id="9e43a-198">Additional resources</span></span>

* [<span data-ttu-id="9e43a-199">응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="9e43a-199">Application startup</span></span>](xref:fundamentals/startup)
* [<span data-ttu-id="9e43a-200">구성</span><span class="sxs-lookup"><span data-stu-id="9e43a-200">Configuration</span></span>](xref:fundamentals/configuration/index)
* [<span data-ttu-id="9e43a-201">IHostingEnvironment.EnvironmentName</span><span class="sxs-lookup"><span data-stu-id="9e43a-201">IHostingEnvironment.EnvironmentName</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment.environmentname)
