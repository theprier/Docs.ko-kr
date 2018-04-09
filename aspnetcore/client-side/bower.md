---
title: ASP.NET Core에서 Bower 사용 하 여 클라이언트 패키지를 관리 합니다.
author: rick-anderson
description: Bower 사용 하 여 클라이언트 패키지를 관리 합니다.
manager: wpickett
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 02/14/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: client-side/bower
ms.openlocfilehash: 81244cfb71194876071c64899d627c296aad3802
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="manage-client-side-packages-with-bower-in-aspnet-core"></a><span data-ttu-id="0a68b-103">ASP.NET Core에서 Bower 사용 하 여 클라이언트 패키지를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-103">Manage client-side packages with Bower in ASP.NET Core</span></span>

<span data-ttu-id="0a68b-104">여 [Rick Anderson](https://twitter.com/RickAndMSFT), [Noel 밥](https://blog.falafel.com/falafel-software-recognized-sitefinity-website-year/), 및 [Scott Addie](https://scottaddie.com)</span><span class="sxs-lookup"><span data-stu-id="0a68b-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Noel Rice](https://blog.falafel.com/falafel-software-recognized-sitefinity-website-year/), and [Scott Addie](https://scottaddie.com)</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0a68b-105">Bower 유지 되는 동안 해당 유지 관리자는 다른 솔루션을 사용 하 여 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-105">While Bower is maintained, its maintainers recommend using a different solution.</span></span> <span data-ttu-id="0a68b-106">Yarn 시스템용으로 사용 하는 하나의 인기 있는를 [마이그레이션 지침](https://bower.io/blog/2017/how-to-migrate-away-from-bower/) 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-106">Yarn with Webpack is one popular alternative for which [migration instructions](https://bower.io/blog/2017/how-to-migrate-away-from-bower/) are available.</span></span>

<span data-ttu-id="0a68b-107">[Bower](https://bower.io/) "웹용 패키지 관리자" 자신을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-107">[Bower](https://bower.io/) calls itself "A package manager for the web".</span></span> <span data-ttu-id="0a68b-108">.NET 환경 내에서 NuGet의 불가능 정적 콘텐츠 파일을 전달 하 여 남아 있는 공간을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-108">Within the .NET ecosystem, it fills the void left by NuGet's inability to deliver static content files.</span></span> <span data-ttu-id="0a68b-109">ASP.NET Core 프로젝트에 대 한 이러한 정적 파일은과 같은 클라이언트 쪽 라이브러리에 따르는 [jQuery](http://jquery.com/) 및 [부트스트랩](http://getbootstrap.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-109">For ASP.NET Core projects, these static files are inherent to client-side libraries like [jQuery](http://jquery.com/) and [Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="0a68b-110">.NET 라이브러리에 대 한 계속 사용할 [NuGet](https://www.nuget.org/) 패키지 관리자.</span><span class="sxs-lookup"><span data-stu-id="0a68b-110">For .NET libraries, you still use [NuGet](https://www.nuget.org/) package manager.</span></span>

<span data-ttu-id="0a68b-111">클라이언트 쪽 설정에서 ASP.NET Core 프로젝트 템플릿을 사용 하 여 만든 새 프로젝트 빌드 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-111">New projects created with the ASP.NET Core project templates set up the client-side build process.</span></span> <span data-ttu-id="0a68b-112">[jQuery](http://jquery.com/) 및 [부트스트랩](http://getbootstrap.com/) 설치 되 면 Bower 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-112">[jQuery](http://jquery.com/) and [Bootstrap](http://getbootstrap.com/) are installed, and Bower is supported.</span></span>

<span data-ttu-id="0a68b-113">클라이언트 패키지에 나열 된는 *bower.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-113">Client-side packages are listed in the *bower.json* file.</span></span> <span data-ttu-id="0a68b-114">ASP.NET Core 프로젝트 템플릿 구성 *bower.json* 부트스트랩, jQuery 및 jQuery 유효성 검사와 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-114">The ASP.NET Core project templates configures *bower.json* with jQuery, jQuery validation, and Bootstrap.</span></span>

<span data-ttu-id="0a68b-115">이 자습서에 대 한 지원을 추가 [글꼴 놀라운](http://fontawesome.io)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-115">In this tutorial, we'll add support for [Font Awesome](http://fontawesome.io).</span></span> <span data-ttu-id="0a68b-116">Bower 패키지를 함께 설치할 수 있습니다는 **Bower 패키지 관리** UI에 수동으로 또는 *bower.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-116">Bower packages can be installed with the **Manage Bower Packages** UI or manually in the *bower.json* file.</span></span>

### <a name="installation-via-manage-bower-packages-ui"></a><span data-ttu-id="0a68b-117">Bower 패키지 관리 UI 통해 설치</span><span class="sxs-lookup"><span data-stu-id="0a68b-117">Installation via Manage Bower Packages UI</span></span>

* <span data-ttu-id="0a68b-118">새 ASP.NET Core 웹 앱을 만들기는 **ASP.NET Core 웹 응용 프로그램 (.NET Core)** 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-118">Create a new ASP.NET Core Web app with the **ASP.NET Core Web Application (.NET Core)** template.</span></span> <span data-ttu-id="0a68b-119">선택 **웹 응용 프로그램** 및 **인증 안 함**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-119">Select **Web Application** and **No Authentication**.</span></span>

* <span data-ttu-id="0a68b-120">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **Bower 패키지 관리** (또는 주 메뉴에서 **프로젝트** > **Bower 패키지 관리**).</span><span class="sxs-lookup"><span data-stu-id="0a68b-120">Right-click the project in Solution Explorer and select **Manage Bower Packages** (alternatively from the main menu, **Project** > **Manage Bower Packages**).</span></span>

* <span data-ttu-id="0a68b-121">에 **Bower: \<프로젝트 이름\>**  창 "찾아보기" 탭을 클릭 한 다음를 입력 하 여 패키지 목록 필터링 `font-awesome` 검색 상자에:</span><span class="sxs-lookup"><span data-stu-id="0a68b-121">In the **Bower: \<project name\>** window, click the "Browse" tab, and then filter the packages list by entering `font-awesome` in the search box:</span></span>

  ![bower 패키지 관리](bower/_static/manage-bower-packages.png)

* <span data-ttu-id="0a68b-123">확인 하는 "변경 내용을 저장 하 *bower.json*" 확인란이 선택 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-123">Confirm that the "Save changes to *bower.json*" checkbox is checked.</span></span> <span data-ttu-id="0a68b-124">드롭다운 목록에서 버전을 선택 하 고 클릭는 **설치** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-124">Select a version from the drop-down list and click the **Install** button.</span></span> <span data-ttu-id="0a68b-125">**출력** 설치 세부 정보 창에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-125">The **Output** window shows the installation details.</span></span>

### <a name="manual-installation-in-bowerjson"></a><span data-ttu-id="0a68b-126">Bower.json에 수동 설치</span><span class="sxs-lookup"><span data-stu-id="0a68b-126">Manual installation in bower.json</span></span>

<span data-ttu-id="0a68b-127">열기는 *bower.json* 파일 및 종속성에 "글꼴 놀라운"를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-127">Open the *bower.json* file and add "font-awesome" to the dependencies.</span></span> <span data-ttu-id="0a68b-128">IntelliSense 사용 가능한 패키지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-128">IntelliSense shows the available packages.</span></span> <span data-ttu-id="0a68b-129">패키지를 선택 하면 사용 가능한 버전 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-129">When a package is selected, the available versions are displayed.</span></span> <span data-ttu-id="0a68b-130">아래 이미지 오래 되었고 나타나는 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-130">The images below are older and won't match what you see.</span></span>

![Bower 패키지 탐색기의 IntelliSense](bower/_static/add-package.png)

![bower 버전 IntelliSense](bower/_static/version-intelliSense.png)

<span data-ttu-id="0a68b-133">사용 하 여 bower [의미 체계 버전 관리](http://semver.org/) 종속성을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-133">Bower uses [semantic versioning](http://semver.org/) to organize dependencies.</span></span> <span data-ttu-id="0a68b-134">의미 체계 버전 관리로도 알려져 SemVer 번호 매기기 구성표를 사용 하 여 패키지를 식별 \<주요 >.\< 사소한 > 합니다. \<패치 > 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-134">Semantic versioning, also known as SemVer, identifies packages with the numbering scheme \<major>.\<minor>.\<patch>.</span></span> <span data-ttu-id="0a68b-135">IntelliSense는 일반적인 몇 가지 옵션에만 표시 하 여 의미 체계 버전 관리를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-135">IntelliSense simplifies semantic versioning by showing only a few common choices.</span></span> <span data-ttu-id="0a68b-136">맨 위 항목 (위의 예에서 4.6.3) IntelliSense 목록에는 패키지의 안정적인 최신 버전으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-136">The top item in the IntelliSense list (4.6.3 in the example above) is considered the latest stable version of the package.</span></span> <span data-ttu-id="0a68b-137">캐럿 (^) 기호가 일치 하는 가장 최근의 주 버전 및 물결표 (~) 최신 부 버전 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-137">The caret (^) symbol matches the most recent major version and the tilde (~) matches the most recent minor version.</span></span>

<span data-ttu-id="0a68b-138">저장 된 *bower.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-138">Save the *bower.json* file.</span></span> <span data-ttu-id="0a68b-139">Visual Studio를 감시는 *bower.json* 파일에서 변경 내용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-139">Visual Studio watches the *bower.json* file for changes.</span></span> <span data-ttu-id="0a68b-140">저장할 때는 *bower 설치* 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-140">Upon saving, the *bower install* command is executed.</span></span> <span data-ttu-id="0a68b-141">출력 창을 참조 **npmBower/** 실행 되는 정확한 명령에 대 한 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-141">See the Output window's **Bower/npm** view for the exact command executed.</span></span>

<span data-ttu-id="0a68b-142">열기는 *.bowerrc* 아래 파일 *bower.json*합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-142">Open the *.bowerrc* file under *bower.json*.</span></span> <span data-ttu-id="0a68b-143">`directory` 속성이 *wwwroot/lib* Bower 위치를 나타내는 패키지 자산을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-143">The `directory` property is set to *wwwroot/lib* which indicates the location Bower will install the package assets.</span></span>

```json
{
 "directory": "wwwroot/lib"
}
```

<span data-ttu-id="0a68b-144">찾아 글꼴 놀라운 패키지를 표시 합니다. 솔루션 탐색기에서 검색 상자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-144">You can use the search box in Solution Explorer to find and display the font-awesome package.</span></span>

<span data-ttu-id="0a68b-145">열기는 *Views\Shared\_Layout.cshtml* 파일 환경에 놀라운 글꼴 CSS 파일을 추가 및 [태그 도우미](xref:mvc/views/tag-helpers/intro) 에 대 한 `Development`합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-145">Open the *Views\Shared\_Layout.cshtml* file and add the font-awesome CSS file to the environment [Tag Helper](xref:mvc/views/tag-helpers/intro) for `Development`.</span></span> <span data-ttu-id="0a68b-146">솔루션 탐색기에서 끌어서 놓기 *글꼴 awesome.css* 내에서 `<environment names="Development">` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-146">From Solution Explorer, drag and drop *font-awesome.css* inside the `<environment names="Development">` element.</span></span>

[!code-html[](bower/sample/_Layout.cshtml?highlight=4&range=9-13)]

<span data-ttu-id="0a68b-147">프로덕션 응용 프로그램에 추가 *글꼴 awesome.min.css* 에 대 한 환경 태그 도우미를 `Staging,Production`합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-147">In a production app you would add *font-awesome.min.css* to the environment tag helper for `Staging,Production`.</span></span>

<span data-ttu-id="0a68b-148">내용을 대체는 *Views\Home\About.cshtml* 다음 태그로 Razor 파일:</span><span class="sxs-lookup"><span data-stu-id="0a68b-148">Replace the contents of the *Views\Home\About.cshtml* Razor file with the following markup:</span></span>

[!code-html[](bower/sample/About.cshtml)]

<span data-ttu-id="0a68b-149">응용 프로그램을 실행 하 고 글꼴 놀라운 패키지 작동 하는지 확인 하는 정보 보기를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-149">Run the app and navigate to the About view to verify the font-awesome package works.</span></span>

## <a name="exploring-the-client-side-build-process"></a><span data-ttu-id="0a68b-150">클라이언트 쪽 빌드 프로세스를 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-150">Exploring the client-side build process</span></span>

<span data-ttu-id="0a68b-151">대부분의 ASP.NET Core 프로젝트 템플릿은 Bower를 사용 하도록 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-151">Most ASP.NET Core project templates are already configured to use Bower.</span></span> <span data-ttu-id="0a68b-152">다음이 연습에서는 빈 ASP.NET Core 프로젝트로 시작 되며 각 부분을 수동으로 추가 되므로 Bower 프로젝트에서 사용 방법에 대 한 지 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-152">This next walkthrough starts with an empty ASP.NET Core project and adds each piece manually, so you can get a feel for how Bower is used in a project.</span></span> <span data-ttu-id="0a68b-153">프로젝트 구조 및 각 구성을 변경 하는 대로 출력 런타임으로 수행 되는 작업을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-153">You can see what happens to the project structure and the runtime output as each configuration change is made.</span></span>

<span data-ttu-id="0a68b-154">Bower 클라이언트 쪽 빌드 프로세스를 사용 하는 일반적인 단계는</span><span class="sxs-lookup"><span data-stu-id="0a68b-154">The general steps to use the client-side build process with Bower are:</span></span>

* <span data-ttu-id="0a68b-155">프로젝트에 사용 되는 패키지를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-155">Define packages used in your project.</span></span> <!-- once defined, you don't need to download them, VS does -->
* <span data-ttu-id="0a68b-156">웹 페이지에서 패키지를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-156">Reference packages from your web pages.</span></span>

### <a name="define-packages"></a><span data-ttu-id="0a68b-157">패키지를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-157">Define packages</span></span>

<span data-ttu-id="0a68b-158">패키지를 나열 되 면는 *bower.json* 파일을 Visual Studio 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-158">Once you list packages in the *bower.json* file, Visual Studio will download them.</span></span> <span data-ttu-id="0a68b-159">다음 예제에서는 Bower를 사용 하 여 jQuery 및 부트스트랩을 로드할 수는 *wwwroot* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-159">The following example uses Bower to load jQuery and Bootstrap to the *wwwroot* folder.</span></span>

* <span data-ttu-id="0a68b-160">새 ASP.NET Core 웹 앱을 만들기는 **ASP.NET Core 웹 응용 프로그램 (.NET Core)** 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-160">Create a new ASP.NET Core Web app with the **ASP.NET Core Web Application (.NET Core)** template.</span></span> <span data-ttu-id="0a68b-161">선택 된 **빈** 프로젝트 템플릿과 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-161">Select the **Empty** project template and click **OK**.</span></span>

* <span data-ttu-id="0a68b-162">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 > **새 항목 추가** 선택 **Bower 구성 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-162">In Solution Explorer, right-click the project > **Add New Item** and select **Bower Configuration File**.</span></span> <span data-ttu-id="0a68b-163">참고: A *.bowerrc* 파일도 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-163">Note: A *.bowerrc* file is also added.</span></span>

* <span data-ttu-id="0a68b-164">열기 *bower.json*, jquery를 추가 하 고 영역에 부트스트랩는 `dependencies` 섹션.</span><span class="sxs-lookup"><span data-stu-id="0a68b-164">Open *bower.json*, and add jquery and bootstrap to the `dependencies` section.</span></span> <span data-ttu-id="0a68b-165">그 결과 *bower.json* 파일은 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-165">The resulting *bower.json* file will look like the following example.</span></span> <span data-ttu-id="0a68b-166">버전은 시간이 지남에 따라 변경 되 고 아래 이미지 일치 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-166">The versions will change over time and may not match the image below.</span></span>

[!code-json[](bower/sample/bower.json?highlight=5,6)]

* <span data-ttu-id="0a68b-167">저장 된 *bower.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-167">Save the *bower.json* file.</span></span>

  <span data-ttu-id="0a68b-168">프로젝트에 포함 되어는 *부트스트랩* 및 *jQuery* 디렉터리에 *wwwroot/lib*합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-168">Verify the project includes the *bootstrap* and *jQuery* directories in *wwwroot/lib*.</span></span> <span data-ttu-id="0a68b-169">사용 하 여 bower는 *.bowerrc* 파일을 자산에 설치 하려면 *wwwroot/lib*합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-169">Bower uses the *.bowerrc* file to install the assets in *wwwroot/lib*.</span></span>

  <span data-ttu-id="0a68b-170">참고: "Bower 패키지 관리" UI 수동 파일 편집에 대 한 대안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-170">Note: The "Manage Bower Packages" UI provides an alternative to manual file editing.</span></span>

### <a name="enable-static-files"></a><span data-ttu-id="0a68b-171">정적 파일을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="0a68b-171">Enable static files</span></span>

* <span data-ttu-id="0a68b-172">추가 `Microsoft.AspNetCore.StaticFiles` NuGet 패키지를 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-172">Add the `Microsoft.AspNetCore.StaticFiles` NuGet package to the project.</span></span>
* <span data-ttu-id="0a68b-173">와 제공에 정적 파일을 사용 하도록 설정 된 [정적 파일 미들웨어](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.staticfileextensions)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-173">Enable static files to be served with the [Static file middleware](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.staticfileextensions).</span></span> <span data-ttu-id="0a68b-174">에 대 한 호출 추가 [UseStaticFiles](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.staticfileextensions) 에 `Configure` 메서드 `Startup`합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-174">Add a call to [UseStaticFiles](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.staticfileextensions) to the `Configure` method of `Startup`.</span></span>

[!code-csharp[](bower/sample/Startup.cs?highlight=9)]

### <a name="reference-packages"></a><span data-ttu-id="0a68b-175">참조 패키지</span><span class="sxs-lookup"><span data-stu-id="0a68b-175">Reference packages</span></span>

<span data-ttu-id="0a68b-176">이 섹션에서는 배포 된 패키지에 액세스할 수를 확인 하는 HTML 페이지를 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-176">In this section, you will create an HTML page to verify it can access the deployed packages.</span></span>

* <span data-ttu-id="0a68b-177">라는 새 HTML 페이지를 추가 *Index.html* 에 *wwwroot* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-177">Add a new HTML page named *Index.html* to the *wwwroot* folder.</span></span> <span data-ttu-id="0a68b-178">참고: HTML 파일을 추가 해야는 *wwwroot* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-178">Note: You must add the HTML file to the *wwwroot* folder.</span></span> <span data-ttu-id="0a68b-179">기본적으로 정적 콘텐츠가 담긴 제공 될 수 없는 외부 *wwwroot*합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-179">By default, static content cannot be served outside *wwwroot*.</span></span> <span data-ttu-id="0a68b-180">참조 [정적 파일로 작업할](xref:fundamentals/static-files) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-180">See [Work with static files](xref:fundamentals/static-files) for more information.</span></span>

  <span data-ttu-id="0a68b-181">내용을 대체 *Index.html* 다음 태그로:</span><span class="sxs-lookup"><span data-stu-id="0a68b-181">Replace the contents of *Index.html* with the following markup:</span></span>

[!code-html[](bower/sample/Index.html)]

* <span data-ttu-id="0a68b-182">응용 프로그램을 실행 하 고 이동 `http://localhost:<port>/Index.html`합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-182">Run the app and navigate to `http://localhost:<port>/Index.html`.</span></span> <span data-ttu-id="0a68b-183">또는와 *Index.html* 열, 키를 눌러 `Ctrl+Shift+W`합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-183">Alternatively, with *Index.html* opened, press `Ctrl+Shift+W`.</span></span> <span data-ttu-id="0a68b-184">Jumbotron 스타일이 적용 되, jQuery 코드는 단추를 클릭할 때 응답 및 부트스트랩 단추 상태가 변경 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a68b-184">Verify that the jumbotron styling is applied, the jQuery code responds when the button is clicked, and that the Bootstrap button changes state.</span></span>

  ![jumbotron 스타일 적용](bower/_static/jumbotron.png)
