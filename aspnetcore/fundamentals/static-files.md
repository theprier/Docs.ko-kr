---
title: "ASP.NET Core에서 정적 파일로 작업"
author: rick-anderson
description: "처리 하 고 정적 파일을 보호 하 고 정적 파일 미들웨어 동작 ASP.NET Core 웹 앱에서 호스트를 구성 하는 방법을 알아봅니다."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 01/18/2018
ms.devlang: csharp
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/static-files
ms.openlocfilehash: 60b205bf0a45e2965f9dab46f46956947ae513fd
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="work-with-static-files-in-aspnet-core"></a><span data-ttu-id="ebc37-103">ASP.NET Core에서 정적 파일로 작업</span><span class="sxs-lookup"><span data-stu-id="ebc37-103">Work with static files in ASP.NET Core</span></span>

<span data-ttu-id="ebc37-104">여 [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Scott Addie](https://twitter.com/Scott_Addie)</span><span class="sxs-lookup"><span data-stu-id="ebc37-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Scott Addie](https://twitter.com/Scott_Addie)</span></span>

<span data-ttu-id="ebc37-105">HTML, CSS, JavaScript 및 이미지와 같은 정적 파일은 자산 클라이언트에 직접 ASP.NET Core 응용 프로그램을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-105">Static files, such as HTML, CSS, images, and JavaScript, are assets an ASP.NET Core app serves directly to clients.</span></span> <span data-ttu-id="ebc37-106">일부 구성은 이러한 파일의 처리를 사용 하도록 설정 하는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-106">Some configuration is required to enable to serving of these files.</span></span>

<span data-ttu-id="ebc37-107">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/static-files/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="ebc37-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/static-files/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="serve-static-files"></a><span data-ttu-id="ebc37-108">정적 파일을 제공</span><span class="sxs-lookup"><span data-stu-id="ebc37-108">Serve static files</span></span>

<span data-ttu-id="ebc37-109">정적 파일은 프로젝트의 웹 루트 디렉터리 안에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-109">Static files are stored within your project's web root directory.</span></span> <span data-ttu-id="ebc37-110">기본 디렉터리는  *\<content_root > / wwwroot*을 통해 변경할 수 있습니다 하지만 [UseWebRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usewebroot#Microsoft_AspNetCore_Hosting_HostingAbstractionsWebHostBuilderExtensions_UseWebRoot_Microsoft_AspNetCore_Hosting_IWebHostBuilder_System_String_) 메서드.</span><span class="sxs-lookup"><span data-stu-id="ebc37-110">The default directory is *\<content_root>/wwwroot*, but it can be changed via the [UseWebRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usewebroot#Microsoft_AspNetCore_Hosting_HostingAbstractionsWebHostBuilderExtensions_UseWebRoot_Microsoft_AspNetCore_Hosting_IWebHostBuilder_System_String_) method.</span></span> <span data-ttu-id="ebc37-111">참조 [콘텐츠 루트](xref:fundamentals/index#content-root) 및 [웹 루트](xref:fundamentals/index#web-root) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-111">See [Content root](xref:fundamentals/index#content-root) and [Web root](xref:fundamentals/index#web-root) for more information.</span></span>

<span data-ttu-id="ebc37-112">응용 프로그램의 웹 호스트 콘텐츠 루트 디렉터리의 인식 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-112">The app's web host must be made aware of the content root directory.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ebc37-113">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ebc37-113">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="ebc37-114">`WebHost.CreateDefaultBuilder` 메서드 콘텐츠 루트를 현재 디렉터리로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-114">The `WebHost.CreateDefaultBuilder` method sets the content root to the current directory:</span></span>

[!code-csharp[](../common/samples/WebApplication1DotNetCore2.0App/Program.cs?name=snippet_Main&highlight=9)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ebc37-115">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ebc37-115">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="ebc37-116">호출 하 여 콘텐츠 루트 현재 디렉터리로 설정 [UseContentRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usecontentroot#Microsoft_AspNetCore_Hosting_HostingAbstractionsWebHostBuilderExtensions_UseContentRoot_Microsoft_AspNetCore_Hosting_IWebHostBuilder_System_String_) 내부에 `Program.Main`:</span><span class="sxs-lookup"><span data-stu-id="ebc37-116">Set the content root to the current directory by invoking [UseContentRoot](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.usecontentroot#Microsoft_AspNetCore_Hosting_HostingAbstractionsWebHostBuilderExtensions_UseContentRoot_Microsoft_AspNetCore_Hosting_IWebHostBuilder_System_String_) inside of `Program.Main`:</span></span>

[!code-csharp[](static-files/samples/1x/Program.cs?name=snippet_ProgramClass&highlight=7)]

---

<span data-ttu-id="ebc37-117">정적 파일은 웹 루트에 상대적인 경로 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-117">Static files are accessible via a path relative to the web root.</span></span> <span data-ttu-id="ebc37-118">예를 들어는 **웹 응용 프로그램** 내에서 여러 폴더를 포함 하는 프로젝트 템플릿에 *wwwroot* 폴더:</span><span class="sxs-lookup"><span data-stu-id="ebc37-118">For example, the **Web Application** project template contains several folders within the *wwwroot* folder:</span></span>

* <span data-ttu-id="ebc37-119">**wwwroot**</span><span class="sxs-lookup"><span data-stu-id="ebc37-119">**wwwroot**</span></span>
  * <span data-ttu-id="ebc37-120">**css**</span><span class="sxs-lookup"><span data-stu-id="ebc37-120">**css**</span></span>
  * <span data-ttu-id="ebc37-121">**images**</span><span class="sxs-lookup"><span data-stu-id="ebc37-121">**images**</span></span>
  * <span data-ttu-id="ebc37-122">**js**</span><span class="sxs-lookup"><span data-stu-id="ebc37-122">**js**</span></span>

<span data-ttu-id="ebc37-123">파일에 액세스 하려면 URI 형식이 고 *이미지* 하위 폴더는 *http://\<server_address > /images/\<image_file_name >*합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-123">The URI format to access a file in the *images* subfolder is *http://\<server_address>/images/\<image_file_name>*.</span></span> <span data-ttu-id="ebc37-124">예를 들어 *http://localhost:9189/images/banner3.svg*합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-124">For example, *http://localhost:9189/images/banner3.svg*.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ebc37-125">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ebc37-125">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="ebc37-126">.NET Framework를 대상으로 하는 경우 추가 [Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles/) 프로젝트에 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-126">If targeting .NET Framework, add the [Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles/) package to your project.</span></span> <span data-ttu-id="ebc37-127">.NET Core를 대상으로 하는 경우는 [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) 이 패키지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-127">If targeting .NET Core, the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage) includes this package.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ebc37-128">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ebc37-128">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="ebc37-129">추가 [Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles/) 프로젝트에 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-129">Add the [Microsoft.AspNetCore.StaticFiles](https://www.nuget.org/packages/Microsoft.AspNetCore.StaticFiles/) package to your project.</span></span>

---

<span data-ttu-id="ebc37-130">구성에서 [미들웨어](xref:fundamentals/middleware) 정적 파일 처리 할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-130">Configure the [middleware](xref:fundamentals/middleware) which enables the serving of static files.</span></span>

### <a name="serve-files-inside-of-web-root"></a><span data-ttu-id="ebc37-131">웹 루트 내부에서 파일을 제공 합니다</span><span class="sxs-lookup"><span data-stu-id="ebc37-131">Serve files inside of web root</span></span>

<span data-ttu-id="ebc37-132">호출 된 [UseStaticFiles](/dotnet/api/microsoft.aspnetcore.builder.staticfileextensions.usestaticfiles#Microsoft_AspNetCore_Builder_StaticFileExtensions_UseStaticFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 메서드 내에서 `Startup.Configure`:</span><span class="sxs-lookup"><span data-stu-id="ebc37-132">Invoke the [UseStaticFiles](/dotnet/api/microsoft.aspnetcore.builder.staticfileextensions.usestaticfiles#Microsoft_AspNetCore_Builder_StaticFileExtensions_UseStaticFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_) method within `Startup.Configure`:</span></span>

[!code-csharp[](static-files/samples/1x/StartupStaticFiles.cs?name=snippet_ConfigureMethod&highlight=3)]

<span data-ttu-id="ebc37-133">매개 변수가 없는 `UseStaticFiles` 메서드 오버 로드로 servable 웹 루트에 있는 파일을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-133">The parameterless `UseStaticFiles` method overload marks the files in web root as servable.</span></span> <span data-ttu-id="ebc37-134">다음 태그 참조 *wwwroot/images/banner1.svg*:</span><span class="sxs-lookup"><span data-stu-id="ebc37-134">The following markup references *wwwroot/images/banner1.svg*:</span></span>

[!code-cshtml[](static-files/samples/1x/Views/Home/Index.cshtml?name=snippet_static_file_wwwroot)]

### <a name="serve-files-outside-of-web-root"></a><span data-ttu-id="ebc37-135">웹 루트 외부 파일을 제공 합니다</span><span class="sxs-lookup"><span data-stu-id="ebc37-135">Serve files outside of web root</span></span>

<span data-ttu-id="ebc37-136">서비스할 수 정적 파일 외부에 있는 웹 루트 디렉터리 계층 구조를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-136">Consider a directory hierarchy in which the static files to be served reside outside of the web root:</span></span>

* <span data-ttu-id="ebc37-137">**wwwroot**</span><span class="sxs-lookup"><span data-stu-id="ebc37-137">**wwwroot**</span></span>
  * <span data-ttu-id="ebc37-138">**css**</span><span class="sxs-lookup"><span data-stu-id="ebc37-138">**css**</span></span>
  * <span data-ttu-id="ebc37-139">**images**</span><span class="sxs-lookup"><span data-stu-id="ebc37-139">**images**</span></span>
  * <span data-ttu-id="ebc37-140">**js**</span><span class="sxs-lookup"><span data-stu-id="ebc37-140">**js**</span></span>
* <span data-ttu-id="ebc37-141">**MyStaticFiles**</span><span class="sxs-lookup"><span data-stu-id="ebc37-141">**MyStaticFiles**</span></span>
  * <span data-ttu-id="ebc37-142">**images**</span><span class="sxs-lookup"><span data-stu-id="ebc37-142">**images**</span></span>
      * <span data-ttu-id="ebc37-143">*banner1.svg*</span><span class="sxs-lookup"><span data-stu-id="ebc37-143">*banner1.svg*</span></span>

<span data-ttu-id="ebc37-144">요청에 액세스할 수는 *banner1.svg* 정적 파일 미들웨어를 다음과 같이 구성 하 여 파일:</span><span class="sxs-lookup"><span data-stu-id="ebc37-144">A request can access the *banner1.svg* file by configuring the static file middleware as follows:</span></span>

[!code-csharp[](static-files/samples/1x/StartupTwoStaticFiles.cs?name=snippet_ConfigureMethod&highlight=5-10)]

<span data-ttu-id="ebc37-145">위의 코드는 *MyStaticFiles* 디렉터리 계층 구조를 통해 공개적으로 노출 됩니다는 *StaticFiles* URI 세그먼트입니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-145">In the preceding code, the *MyStaticFiles* directory hierarchy is exposed publicly via the *StaticFiles* URI segment.</span></span> <span data-ttu-id="ebc37-146">요청을 *http://\<server_address > /StaticFiles/images/banner1.svg* 역할는 *banner1.svg* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-146">A request to *http://\<server_address>/StaticFiles/images/banner1.svg* serves the *banner1.svg* file.</span></span>

<span data-ttu-id="ebc37-147">다음 태그 참조 *MyStaticFiles/images/banner1.svg*:</span><span class="sxs-lookup"><span data-stu-id="ebc37-147">The following markup references *MyStaticFiles/images/banner1.svg*:</span></span>

[!code-cshtml[](static-files/samples/1x/Views/Home/Index.cshtml?name=snippet_static_file_outside)]

### <a name="set-http-response-headers"></a><span data-ttu-id="ebc37-148">HTTP 응답 헤더 설정</span><span class="sxs-lookup"><span data-stu-id="ebc37-148">Set HTTP response headers</span></span>

<span data-ttu-id="ebc37-149">A [StaticFileOptions](/dotnet/api/microsoft.aspnetcore.builder.staticfileoptions) 개체는 HTTP 응답 헤더를 설정할 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-149">A [StaticFileOptions](/dotnet/api/microsoft.aspnetcore.builder.staticfileoptions) object can be used to set HTTP response headers.</span></span> <span data-ttu-id="ebc37-150">웹 루트에서 정적 파일 서비스를 구성 하는 것 외에도 다음 코드에서는 `Cache-Control` 헤더:</span><span class="sxs-lookup"><span data-stu-id="ebc37-150">In addition to configuring static file serving from the web root, the following code sets the `Cache-Control` header:</span></span>

[!code-csharp[](static-files/samples/1x/StartupAddHeader.cs?name=snippet_ConfigureMethod)]

<span data-ttu-id="ebc37-151">[HeaderDictionaryExtensions.Append](/dotnet/api/microsoft.aspnetcore.http.headerdictionaryextensions.append) 에 있는 메서드는 [Microsoft.AspNetCore.Http](https://www.nuget.org/packages/Microsoft.AspNetCore.Http/) 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-151">The [HeaderDictionaryExtensions.Append](/dotnet/api/microsoft.aspnetcore.http.headerdictionaryextensions.append) method exists in the [Microsoft.AspNetCore.Http](https://www.nuget.org/packages/Microsoft.AspNetCore.Http/) package.</span></span>

<span data-ttu-id="ebc37-152">파일 내용이 공개적으로 캐시할 수 10 분 (600 초):</span><span class="sxs-lookup"><span data-stu-id="ebc37-152">The files have been made publicly cacheable for 10 minutes (600 seconds):</span></span>

![추가 된 캐시 제어 헤더를 보여 주는 응답 헤더](static-files/_static/add-header.png)

## <a name="static-file-authorization"></a><span data-ttu-id="ebc37-154">정적 파일 권한 부여</span><span class="sxs-lookup"><span data-stu-id="ebc37-154">Static file authorization</span></span>

<span data-ttu-id="ebc37-155">정적 파일 미들웨어 인증 검사를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-155">The static file middleware doesn't provide authorization checks.</span></span> <span data-ttu-id="ebc37-156">모든 파일에서 제공 비롯 *wwwroot*, 공개적으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-156">Any files served by it, including those under *wwwroot*, are publicly accessible.</span></span> <span data-ttu-id="ebc37-157">파일을 제공 하려면 권한 부여 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-157">To serve files based on authorization:</span></span>

* <span data-ttu-id="ebc37-158">외부에 보관해 두면 *wwwroot* 및 정적 파일 미들웨어에 액세스할 수 있는 모든 디렉터리 **및**</span><span class="sxs-lookup"><span data-stu-id="ebc37-158">Store them outside of *wwwroot* and any directory accessible to the static file middleware **and**</span></span>
* <span data-ttu-id="ebc37-159">권한 부여 적용 되는 동작 메서드를 통해 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-159">Serve them via an action method to which authorization is applied.</span></span> <span data-ttu-id="ebc37-160">반환 된 [FileResult](/dotnet/api/microsoft.aspnetcore.mvc.fileresult) 개체:</span><span class="sxs-lookup"><span data-stu-id="ebc37-160">Return a [FileResult](/dotnet/api/microsoft.aspnetcore.mvc.fileresult) object:</span></span>

[!code-csharp[](static-files/samples/1x/Controllers/HomeController.cs?name=snippet_BannerImageAction)]

## <a name="enable-directory-browsing"></a><span data-ttu-id="ebc37-161">디렉터리 검색을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="ebc37-161">Enable directory browsing</span></span>

<span data-ttu-id="ebc37-162">디렉터리 검색 웹 응용 프로그램의 사용자가 디렉터리 목록을 볼 수 및 지정된 된 디렉터리 내의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-162">Directory browsing allows users of your web app to see a directory listing and files within a specified directory.</span></span> <span data-ttu-id="ebc37-163">보안상의 이유로 기본적으로 비활성화 되어 디렉터리 검색 (참조 [고려 사항](#considerations)).</span><span class="sxs-lookup"><span data-stu-id="ebc37-163">Directory browsing is disabled by default for security reasons (see [Considerations](#considerations)).</span></span> <span data-ttu-id="ebc37-164">Enable 디렉터리를 호출 하 여 검색 된 [UseDirectoryBrowser](/dotnet/api/microsoft.aspnetcore.builder.directorybrowserextensions.usedirectorybrowser#Microsoft_AspNetCore_Builder_DirectoryBrowserExtensions_UseDirectoryBrowser_Microsoft_AspNetCore_Builder_IApplicationBuilder_Microsoft_AspNetCore_Builder_DirectoryBrowserOptions_) 메서드에서 `Startup.Configure`:</span><span class="sxs-lookup"><span data-stu-id="ebc37-164">Enable directory browsing by invoking the [UseDirectoryBrowser](/dotnet/api/microsoft.aspnetcore.builder.directorybrowserextensions.usedirectorybrowser#Microsoft_AspNetCore_Builder_DirectoryBrowserExtensions_UseDirectoryBrowser_Microsoft_AspNetCore_Builder_IApplicationBuilder_Microsoft_AspNetCore_Builder_DirectoryBrowserOptions_) method in `Startup.Configure`:</span></span>

[!code-csharp[](static-files/samples/1x/StartupBrowse.cs?name=snippet_ConfigureMethod&highlight=12-17)]

<span data-ttu-id="ebc37-165">필요한 서비스를 호출 하 여 추가 된 [AddDirectoryBrowser](/dotnet/api/microsoft.extensions.dependencyinjection.directorybrowserserviceextensions.adddirectorybrowser#Microsoft_Extensions_DependencyInjection_DirectoryBrowserServiceExtensions_AddDirectoryBrowser_Microsoft_Extensions_DependencyInjection_IServiceCollection_) 메서드에서 `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="ebc37-165">Add required services by invoking the [AddDirectoryBrowser](/dotnet/api/microsoft.extensions.dependencyinjection.directorybrowserserviceextensions.adddirectorybrowser#Microsoft_Extensions_DependencyInjection_DirectoryBrowserServiceExtensions_AddDirectoryBrowser_Microsoft_Extensions_DependencyInjection_IServiceCollection_) method from `Startup.ConfigureServices`:</span></span>

[!code-csharp[](static-files/samples/1x/StartupBrowse.cs?name=snippet_ConfigureServicesMethod&highlight=3)]

<span data-ttu-id="ebc37-166">위의 코드 디렉터리를 검색할 수는 *wwwroot/이미지* URL을 사용 하 여 폴더 *http://\<server_address > / MyImages*, 각 파일 및 폴더에 대 한 링크로:</span><span class="sxs-lookup"><span data-stu-id="ebc37-166">The preceding code allows directory browsing of the *wwwroot/images* folder using the URL *http://\<server_address>/MyImages*, with links to each file and folder:</span></span>

![디렉터리 검색](static-files/_static/dir-browse.png)

<span data-ttu-id="ebc37-168">참조 [고려 사항](#considerations) 검색을 사용 하도록 설정할 때는 보안 위험에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-168">See [Considerations](#considerations) on the security risks when enabling browsing.</span></span>

<span data-ttu-id="ebc37-169">두 참고 `UseStaticFiles` 다음 예제에서를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-169">Note the two `UseStaticFiles` calls in the following example.</span></span> <span data-ttu-id="ebc37-170">첫 번째 호출의 정적 파일 처리를 사용 하면는 *wwwroot* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-170">The first call enables the serving of static files in the *wwwroot* folder.</span></span> <span data-ttu-id="ebc37-171">두 번째 호출의 디렉터리 검색을 사용 하면는 *wwwroot/이미지* URL을 사용 하 여 폴더 *http://\<server_address > / MyImages*:</span><span class="sxs-lookup"><span data-stu-id="ebc37-171">The second call enables directory browsing of the *wwwroot/images* folder using the URL *http://\<server_address>/MyImages*:</span></span>

[!code-csharp[](static-files/samples/1x/StartupBrowse.cs?name=snippet_ConfigureMethod&highlight=3,5)]

## <a name="serve-a-default-document"></a><span data-ttu-id="ebc37-172">기본 문서를 제공</span><span class="sxs-lookup"><span data-stu-id="ebc37-172">Serve a default document</span></span>

<span data-ttu-id="ebc37-173">설정 기본 홈 페이지 방문자 논리는 시작점을 제공 사이트를 방문할 때.</span><span class="sxs-lookup"><span data-stu-id="ebc37-173">Setting a default home page provides visitors a logical starting point when visiting your site.</span></span> <span data-ttu-id="ebc37-174">기본 페이지의 URI를 정규화 하는 사용자 없이 처리 하려면 호출는 [UseDefaultFiles](/dotnet/api/microsoft.aspnetcore.builder.defaultfilesextensions.usedefaultfiles#Microsoft_AspNetCore_Builder_DefaultFilesExtensions_UseDefaultFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 메서드에서 `Startup.Configure`:</span><span class="sxs-lookup"><span data-stu-id="ebc37-174">To serve a default page without the user fully qualifying the URI, call the [UseDefaultFiles](/dotnet/api/microsoft.aspnetcore.builder.defaultfilesextensions.usedefaultfiles#Microsoft_AspNetCore_Builder_DefaultFilesExtensions_UseDefaultFiles_Microsoft_AspNetCore_Builder_IApplicationBuilder_) method from `Startup.Configure`:</span></span>

[!code-csharp[](static-files/samples/1x/StartupEmpty.cs?name=snippet_ConfigureMethod&highlight=3)]

> [!IMPORTANT]
> <span data-ttu-id="ebc37-175">`UseDefaultFiles`먼저 호출 해야 `UseStaticFiles` 기본 파일 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-175">`UseDefaultFiles` must be called before `UseStaticFiles` to serve the default file.</span></span> <span data-ttu-id="ebc37-176">`UseDefaultFiles`파일 사용 될 실제로 하지 않는 URL 재작성 기가입니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-176">`UseDefaultFiles` is a URL rewriter that doesn't actually serve the file.</span></span> <span data-ttu-id="ebc37-177">정적 파일 미들웨어를 통해 사용 하도록 설정 `UseStaticFiles` 파일 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-177">Enable the static file middleware via `UseStaticFiles` to serve the file.</span></span>

<span data-ttu-id="ebc37-178">와 `UseDefaultFiles`에 대 한 폴더 검색에 대 한 요청:</span><span class="sxs-lookup"><span data-stu-id="ebc37-178">With `UseDefaultFiles`, requests to a folder search for:</span></span>

* <span data-ttu-id="ebc37-179">*default.htm*</span><span class="sxs-lookup"><span data-stu-id="ebc37-179">*default.htm*</span></span>
* <span data-ttu-id="ebc37-180">*default.html*</span><span class="sxs-lookup"><span data-stu-id="ebc37-180">*default.html*</span></span>
* <span data-ttu-id="ebc37-181">*index.htm*</span><span class="sxs-lookup"><span data-stu-id="ebc37-181">*index.htm*</span></span>
* <span data-ttu-id="ebc37-182">*index.html*</span><span class="sxs-lookup"><span data-stu-id="ebc37-182">*index.html*</span></span>

<span data-ttu-id="ebc37-183">목록에서 첫 번째 파일이 요청에는 정규화 된 URI가 것 처럼 서비스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-183">The first file found from the list is served as though the request were the fully qualified URI.</span></span> <span data-ttu-id="ebc37-184">요청 된 URI를 반영 하기 위해 브라우저 URL이 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-184">The browser URL continues to reflect the URI requested.</span></span>

<span data-ttu-id="ebc37-185">다음 코드에서는 기본 파일 이름을 변경 *mydefault.html*:</span><span class="sxs-lookup"><span data-stu-id="ebc37-185">The following code changes the default file name to *mydefault.html*:</span></span>

[!code-csharp[](static-files/samples/1x/StartupDefault.cs?name=snippet_ConfigureMethod)]

## <a name="usefileserver"></a><span data-ttu-id="ebc37-186">UseFileServer</span><span class="sxs-lookup"><span data-stu-id="ebc37-186">UseFileServer</span></span>

<span data-ttu-id="ebc37-187">[UseFileServer](/dotnet/api/microsoft.aspnetcore.builder.fileserverextensions.usefileserver#Microsoft_AspNetCore_Builder_FileServerExtensions_UseFileServer_Microsoft_AspNetCore_Builder_IApplicationBuilder_) 의 기능을 결합 `UseStaticFiles`, `UseDefaultFiles`, 및 `UseDirectoryBrowser`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-187">[UseFileServer](/dotnet/api/microsoft.aspnetcore.builder.fileserverextensions.usefileserver#Microsoft_AspNetCore_Builder_FileServerExtensions_UseFileServer_Microsoft_AspNetCore_Builder_IApplicationBuilder_) combines the functionality of `UseStaticFiles`, `UseDefaultFiles`, and `UseDirectoryBrowser`.</span></span>

<span data-ttu-id="ebc37-188">다음 코드에서는 기본 파일 및 정적 파일 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-188">The following code enables the serving of static files and the default file.</span></span> <span data-ttu-id="ebc37-189">디렉터리 검색 기능이 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-189">Directory browsing isn't enabled.</span></span>

```csharp
app.UseFileServer();
```

<span data-ttu-id="ebc37-190">매개 변수가 없는 오버 로드에 디렉터리 검색을 사용 하 여 다음 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-190">The following code builds upon the parameterless overload by enabling directory browsing:</span></span>

```csharp
app.UseFileServer(enableDirectoryBrowsing: true);
```

<span data-ttu-id="ebc37-191">다음 디렉터리 계층 구조를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-191">Consider the following directory hierarchy:</span></span>

* <span data-ttu-id="ebc37-192">**wwwroot**</span><span class="sxs-lookup"><span data-stu-id="ebc37-192">**wwwroot**</span></span>
  * <span data-ttu-id="ebc37-193">**css**</span><span class="sxs-lookup"><span data-stu-id="ebc37-193">**css**</span></span>
  * <span data-ttu-id="ebc37-194">**images**</span><span class="sxs-lookup"><span data-stu-id="ebc37-194">**images**</span></span>
  * <span data-ttu-id="ebc37-195">**js**</span><span class="sxs-lookup"><span data-stu-id="ebc37-195">**js**</span></span>
* <span data-ttu-id="ebc37-196">**MyStaticFiles**</span><span class="sxs-lookup"><span data-stu-id="ebc37-196">**MyStaticFiles**</span></span>
  * <span data-ttu-id="ebc37-197">**images**</span><span class="sxs-lookup"><span data-stu-id="ebc37-197">**images**</span></span>
      * <span data-ttu-id="ebc37-198">*banner1.svg*</span><span class="sxs-lookup"><span data-stu-id="ebc37-198">*banner1.svg*</span></span>
  * <span data-ttu-id="ebc37-199">*default.html*</span><span class="sxs-lookup"><span data-stu-id="ebc37-199">*default.html*</span></span>

<span data-ttu-id="ebc37-200">다음 코드를 통해 정적 파일, 기본 파일 및 디렉터리 검색의 `MyStaticFiles`:</span><span class="sxs-lookup"><span data-stu-id="ebc37-200">The following code enables static files, default files, and directory browsing of `MyStaticFiles`:</span></span>

[!code-csharp[](static-files/samples/1x/StartupUseFileServer.cs?name=snippet_ConfigureMethod&highlight=5-11)]

<span data-ttu-id="ebc37-201">`AddDirectoryBrowser`호출 해야 합니다는 `EnableDirectoryBrowsing` 속성 값은 `true`:</span><span class="sxs-lookup"><span data-stu-id="ebc37-201">`AddDirectoryBrowser` must be called when the `EnableDirectoryBrowsing` property value is `true`:</span></span>

[!code-csharp[](static-files/samples/1x/StartupUseFileServer.cs?name=snippet_ConfigureServicesMethod)]

<span data-ttu-id="ebc37-202">Url 및 파일 계층 구조를 사용 하 여 앞에 오는 코드를 다음과 같이 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-202">Using the file hierarchy and preceding code, URLs resolve as follows:</span></span>

| <span data-ttu-id="ebc37-203">URI</span><span class="sxs-lookup"><span data-stu-id="ebc37-203">URI</span></span>            |                             <span data-ttu-id="ebc37-204">응답</span><span class="sxs-lookup"><span data-stu-id="ebc37-204">Response</span></span>  |
| ------- | ------|
| <span data-ttu-id="ebc37-205">*http://\<server_address>/StaticFiles/images/banner1.svg*</span><span class="sxs-lookup"><span data-stu-id="ebc37-205">*http://\<server_address>/StaticFiles/images/banner1.svg*</span></span>    |      <span data-ttu-id="ebc37-206">MyStaticFiles/images/banner1.svg</span><span class="sxs-lookup"><span data-stu-id="ebc37-206">MyStaticFiles/images/banner1.svg</span></span> |
| <span data-ttu-id="ebc37-207">*http://\<server_address>/StaticFiles*</span><span class="sxs-lookup"><span data-stu-id="ebc37-207">*http://\<server_address>/StaticFiles*</span></span>             |     <span data-ttu-id="ebc37-208">MyStaticFiles/default.html</span><span class="sxs-lookup"><span data-stu-id="ebc37-208">MyStaticFiles/default.html</span></span> |

<span data-ttu-id="ebc37-209">에 기본 이름이 지정 된 파일이 없는 경우는 *MyStaticFiles* 디렉터리 *http://\<server_address > / StaticFiles* 클릭 가능한 링크와 함께 나열 하는 디렉터리를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-209">If no default-named file exists in the *MyStaticFiles* directory, *http://\<server_address>/StaticFiles* returns the directory listing with clickable links:</span></span>

![정적 파일 목록](static-files/_static/db2.png)

> [!NOTE]
> <span data-ttu-id="ebc37-211">`UseDefaultFiles`및 `UseDirectoryBrowser` URL을 사용 하 여 *http://\<server_address > / StaticFiles* 리디렉션됩니다 후행 슬래시를 트리거하는 클라이언트 쪽 없이 *http://\<server_address > / StaticFiles /*합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-211">`UseDefaultFiles` and `UseDirectoryBrowser` use the URL *http://\<server_address>/StaticFiles* without the trailing slash to trigger a client-side redirect to *http://\<server_address>/StaticFiles/*.</span></span> <span data-ttu-id="ebc37-212">후행 슬래시를 추가 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-212">Notice the addition of the trailing slash.</span></span> <span data-ttu-id="ebc37-213">문서 내에서 상대 Url은 후행 슬래시가 없는 잘못 된 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-213">Relative URLs within the documents are deemed invalid without a trailing slash.</span></span>

## <a name="fileextensioncontenttypeprovider"></a><span data-ttu-id="ebc37-214">FileExtensionContentTypeProvider</span><span class="sxs-lookup"><span data-stu-id="ebc37-214">FileExtensionContentTypeProvider</span></span>

<span data-ttu-id="ebc37-215">[FileExtensionContentTypeProvider](/dotnet/api/microsoft.aspnetcore.staticfiles.fileextensioncontenttypeprovider) 클래스를 포함 한 `Mappings` 속성의 MIME 콘텐츠 형식에 대 한 파일 확장명 매핑을 역할을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-215">The [FileExtensionContentTypeProvider](/dotnet/api/microsoft.aspnetcore.staticfiles.fileextensioncontenttypeprovider) class contains a `Mappings` property serving as a mapping of file extensions to MIME content types.</span></span> <span data-ttu-id="ebc37-216">다음 샘플에서는 여러 파일 확장명이 알려진된 MIME 형식에 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-216">In the following sample, several file extensions are registered to known MIME types.</span></span> <span data-ttu-id="ebc37-217">*.rtf* 확장 바뀝니다 및 *.mp4* 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-217">The *.rtf* extension is replaced, and *.mp4* is removed.</span></span>

[!code-csharp[](static-files/samples/1x/StartupFileExtensionContentTypeProvider.cs?name=snippet_ConfigureMethod&highlight=3-12,19)]

<span data-ttu-id="ebc37-218">참조 [MIME 콘텐츠 형식을](http://www.iana.org/assignments/media-types/media-types.xhtml)합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-218">See [MIME content types](http://www.iana.org/assignments/media-types/media-types.xhtml).</span></span>

## <a name="non-standard-content-types"></a><span data-ttu-id="ebc37-219">사용할 수 없는 콘텐츠 형식</span><span class="sxs-lookup"><span data-stu-id="ebc37-219">Non-standard content types</span></span>

<span data-ttu-id="ebc37-220">거의 400 알려진된 파일 콘텐츠 형식을 이해 하는 정적 파일 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-220">The static file middleware understands almost 400 known file content types.</span></span> <span data-ttu-id="ebc37-221">사용자가 알 수 없는 파일 형식의 파일을 요청 하는 경우 정적 파일 미들웨어는 HTTP 404 (찾을 수 없음) 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-221">If the user requests a file of an unknown file type, the static file middleware returns a HTTP 404 (Not Found) response.</span></span> <span data-ttu-id="ebc37-222">디렉터리 검색을 사용 하는 경우 파일에는 링크가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-222">If directory browsing is enabled, a link to the file is displayed.</span></span> <span data-ttu-id="ebc37-223">URI는 HTTP 404 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-223">The URI returns an HTTP 404 error.</span></span>

<span data-ttu-id="ebc37-224">다음 코드는 알 수 없는 형식을 처리를 사용 하도록 설정 하 고 알 수 없는 파일을 이미지로 렌더링.</span><span class="sxs-lookup"><span data-stu-id="ebc37-224">The following code enables serving unknown types and renders the unknown file as an image:</span></span>

[!code-csharp[](static-files/samples/1x/StartupServeUnknownFileTypes.cs?name=snippet_ConfigureMethod)]

<span data-ttu-id="ebc37-225">위의 코드에서 알 수 없는 콘텐츠 형식으로 파일에 대 한 요청 이미지 형식으로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-225">With the preceding code, a request for a file with an unknown content type is returned as an image.</span></span>

> [!WARNING]
> <span data-ttu-id="ebc37-226">사용 하도록 설정 [ServeUnknownFileTypes](/dotnet/api/microsoft.aspnetcore.builder.staticfileoptions.serveunknownfiletypes#Microsoft_AspNetCore_Builder_StaticFileOptions_ServeUnknownFileTypes) 보안상 위험할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-226">Enabling [ServeUnknownFileTypes](/dotnet/api/microsoft.aspnetcore.builder.staticfileoptions.serveunknownfiletypes#Microsoft_AspNetCore_Builder_StaticFileOptions_ServeUnknownFileTypes) is a security risk.</span></span> <span data-ttu-id="ebc37-227">기본적으로 비활성화 되어 및의 사용은 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-227">It's disabled by default, and its use is discouraged.</span></span> <span data-ttu-id="ebc37-228">[FileExtensionContentTypeProvider](#fileextensioncontenttypeprovider) 비표준 확장명을 가진 파일을 처리 하는 보다 안전한 대체 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-228">[FileExtensionContentTypeProvider](#fileextensioncontenttypeprovider) provides a safer alternative to serving files with non-standard extensions.</span></span>

### <a name="considerations"></a><span data-ttu-id="ebc37-229">고려 사항</span><span class="sxs-lookup"><span data-stu-id="ebc37-229">Considerations</span></span>

> [!WARNING]
> <span data-ttu-id="ebc37-230">`UseDirectoryBrowser`및 `UseStaticFiles` 비밀 정보를 누출 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-230">`UseDirectoryBrowser` and `UseStaticFiles` can leak secrets.</span></span> <span data-ttu-id="ebc37-231">해제 디렉터리를 프로덕션 환경에서 검색을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-231">Disabling directory browsing in production is highly recommended.</span></span> <span data-ttu-id="ebc37-232">디렉터리를 활성화를 주의 깊게 검토 `UseStaticFiles` 또는 `UseDirectoryBrowser`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-232">Carefully review which directories are enabled via `UseStaticFiles` or `UseDirectoryBrowser`.</span></span> <span data-ttu-id="ebc37-233">전체 디렉터리와 해당 하위 디렉터리의 공개적으로 액세스할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-233">The entire directory and its sub-directories become publicly accessible.</span></span> <span data-ttu-id="ebc37-234">저장소 파일을 공개적으로 서비스에 대 한 적합 한 전용된 디렉터리에 같은  *\<content_root > / wwwroot*합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-234">Store files suitable for serving to the public in a dedicated directory, such as *\<content_root>/wwwroot*.</span></span> <span data-ttu-id="ebc37-235">MVC 뷰, Razor 페이지 (2.x에만 해당), 구성 파일 등에서 이러한 파일을 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-235">Separate these files from MVC views, Razor Pages (2.x only), configuration files, etc.</span></span>

* <span data-ttu-id="ebc37-236">노출 된 콘텐츠에 대 한 Url `UseDirectoryBrowser` 및 `UseStaticFiles` 는 대/소문자 구분 및 기본 파일 시스템의 문자 제한이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-236">The URLs for content exposed with `UseDirectoryBrowser` and `UseStaticFiles` are subject to the case sensitivity and character restrictions of the underlying file system.</span></span> <span data-ttu-id="ebc37-237">예를 들어 Windows는 대/소문자 구분&mdash;Mac 및 Linux 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-237">For example, Windows is case insensitive&mdash;Mac and Linux aren't.</span></span>

* <span data-ttu-id="ebc37-238">ASP.NET Core 응용 프로그램을 사용 하 여 IIS에서에서 호스팅되는 [ASP.NET Core 모듈 (ANCM)](xref:fundamentals/servers/aspnet-core-module) 정적 파일 요청을 비롯 한 응용 프로그램에 대 한 모든 요청을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-238">ASP.NET Core apps hosted in IIS use the [ASP.NET Core Module (ANCM)](xref:fundamentals/servers/aspnet-core-module) to forward all requests to the app, including static file requests.</span></span> <span data-ttu-id="ebc37-239">IIS 정적 파일 처리기는 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-239">The IIS static file handler isn't used.</span></span> <span data-ttu-id="ebc37-240">요청을 처리 하기 전에 ANCM 하 여 처리 중인 확률이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-240">It has no chance to handle requests before they're handled by the ANCM.</span></span>

* <span data-ttu-id="ebc37-241">IIS 관리자에서 서버 또는 웹 사이트 수준에서 IIS 정적 파일 처리기를 제거 하려면 다음 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-241">Complete the following steps in IIS Manager to remove the IIS static file handler at the server or website level:</span></span>
    1. <span data-ttu-id="ebc37-242">탐색 하 고 **모듈** 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-242">Navigate to the **Modules** feature.</span></span>
    1. <span data-ttu-id="ebc37-243">선택 **모듈은 staticfilemodule입니다** 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-243">Select **StaticFileModule** in the list.</span></span>
    1. <span data-ttu-id="ebc37-244">클릭 **제거** 에 **동작** 사이드바 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-244">Click **Remove** in the **Actions** sidebar.</span></span>

> [!WARNING]
> <span data-ttu-id="ebc37-245">IIS 정적 파일 처리기에서 사용 되는 경우 **및** 는 ANCM 올바르게 구성 되었는지, 정적 파일에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-245">If the IIS static file handler is enabled **and** the ANCM is configured incorrectly, static files are served.</span></span> <span data-ttu-id="ebc37-246">이런 경우 예를 들어 경우는 *web.config* 파일이 배포 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-246">This happens, for example, if the *web.config* file isn't deployed.</span></span>

* <span data-ttu-id="ebc37-247">코드 파일을 배치할 (포함 하 여 *.cs* 및 *.cshtml*) 응용 프로그램 프로젝트의 웹 루트 외부입니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-247">Place code files (including *.cs* and *.cshtml*) outside of the app project's web root.</span></span> <span data-ttu-id="ebc37-248">따라서 응용 프로그램의 클라이언트 쪽 콘텐츠 및 서버 기반 코드 사이 논리적 분리를 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-248">A logical separation is therefore created between the app's client-side content and server-based code.</span></span> <span data-ttu-id="ebc37-249">이렇게 하면 서버 쪽 코드를에서 유출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ebc37-249">This prevents server-side code from being leaked.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ebc37-250">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ebc37-250">Additional resources</span></span>

* [<span data-ttu-id="ebc37-251">미들웨어</span><span class="sxs-lookup"><span data-stu-id="ebc37-251">Middleware</span></span>](xref:fundamentals/middleware)

* [<span data-ttu-id="ebc37-252">ASP.NET Core 소개</span><span class="sxs-lookup"><span data-stu-id="ebc37-252">Introduction to ASP.NET Core</span></span>](xref:index)
