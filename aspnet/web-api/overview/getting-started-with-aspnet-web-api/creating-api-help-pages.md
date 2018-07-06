---
uid: web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
title: ASP.NET Web API에 대 한 도움말 페이지 만들기 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 04/01/2013
ms.assetid: 0150e67b-c50d-4613-83ea-7b4ef8cacc5a
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
msc.type: authoredcontent
ms.openlocfilehash: 3e8a0e6c4555e2b8d880118ca499b801ac8be63e
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37811946"
---
<a name="creating-help-pages-for-aspnet-web-api"></a><span data-ttu-id="a63a3-102">ASP.NET Web API에 대 한 도움말 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="a63a3-102">Creating Help Pages for ASP.NET Web API</span></span>
====================
<span data-ttu-id="a63a3-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a63a3-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="a63a3-104">Web API를 만들 때 유용 도움말 페이지를 만들려면 다른 개발자가 API를 호출 하는 방법을 알 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-104">When you create a web API, it is often useful to create a help page, so that other developers will know how to call your API.</span></span> <span data-ttu-id="a63a3-105">문서의 모든 작업을 수동으로 만들 수 있지만 최대한 자동 생성 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-105">You could create all of the documentation manually, but it is better to autogenerate as much as possible.</span></span>

<span data-ttu-id="a63a3-106">이 작업을 쉽게 하려면 ASP.NET Web API 도움말 페이지를 자동으로 생성에 대 한 라이브러리를 런타임에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-106">To make this task easier, ASP.NET Web API provides a library for auto-generating help pages at run time.</span></span>

![](creating-api-help-pages/_static/image1.png)

## <a name="creating-api-help-pages"></a><span data-ttu-id="a63a3-107">API 도움말 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="a63a3-107">Creating API Help Pages</span></span>

<span data-ttu-id="a63a3-108">설치할 [ASP.NET 및 웹 도구 2012.2 업데이트](https://go.microsoft.com/fwlink/?LinkId=282650)합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-108">Install [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="a63a3-109">이 업데이트는 Web API 프로젝트 템플릿으로 도움말 페이지를 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-109">This update integrates help pages into the Web API project template.</span></span>

<span data-ttu-id="a63a3-110">새 ASP.NET MVC 4 프로젝트를 만들고으로, Web API 프로젝트 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-110">Next, create a new ASP.NET MVC 4 project and select the Web API project template.</span></span> <span data-ttu-id="a63a3-111">프로젝트 템플릿이 라는 API 예제 컨트롤러를 만듭니다 `ValuesController`합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-111">The project template creates an example API controller named `ValuesController`.</span></span> <span data-ttu-id="a63a3-112">또한이 템플릿은 API 도움말 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-112">The template also creates the API help pages.</span></span> <span data-ttu-id="a63a3-113">도움말 페이지에 대 한 코드 파일의 모든 프로젝트의 영역 폴더에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-113">All of the code files for the help page are placed in the Areas folder of the project.</span></span>

![](creating-api-help-pages/_static/image2.png)

<span data-ttu-id="a63a3-114">응용 프로그램을 실행 하는 경우 홈 페이지 API 도움말 페이지에 대 한 링크를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-114">When you run the application, the home page contains a link to the API help page.</span></span> <span data-ttu-id="a63a3-115">상대 경로 홈 페이지에서 /Help은 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-115">From the home page, the relative path is /Help.</span></span>

![](creating-api-help-pages/_static/image3.png)

<span data-ttu-id="a63a3-116">이 링크는 API 요약 페이지에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-116">This link brings you to an API summary page.</span></span>

![](creating-api-help-pages/_static/image4.png)

<span data-ttu-id="a63a3-117">이 페이지에 대 한 MVC 뷰 Areas/HelpPage/Views/Help/Index.cshtml에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-117">The MVC view for this page is defined in Areas/HelpPage/Views/Help/Index.cshtml.</span></span> <span data-ttu-id="a63a3-118">레이아웃, 소개, 제목, 스타일 및 등을 수정 하려면이 페이지를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-118">You can edit this page to modify the layout, introduction, title, styles, and so forth.</span></span>

<span data-ttu-id="a63a3-119">페이지의 주요 부분에는 api, 컨트롤러 별로 그룹화 된 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-119">The main part of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="a63a3-120">사용 하 여 테이블 항목을 동적으로 생성 합니다 **IApiExplorer** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-120">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="a63a3-121">(하겠습니다이 인터페이스에 대 한 자세한 나중.) 새 API 컨트롤러를 추가 하는 경우 테이블은 런타임 시 자동으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-121">(I'll talk more about this interface later.) If you add a new API controller, the table is automatically updated at run time.</span></span>

<span data-ttu-id="a63a3-122">"API" 열에는 HTTP 메서드 및 상대 URI를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-122">The "API" column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="a63a3-123">"Description" 열에는 각 API에 대 한 설명서를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-123">The "Description" column contains documentation for each API.</span></span> <span data-ttu-id="a63a3-124">처음에 설명서에 자리 표시자 텍스트 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-124">Initially, the documentation is just placeholder text.</span></span> <span data-ttu-id="a63a3-125">다음 섹션에서는 XML 주석에서 문서를 추가 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-125">In the next section, I'll show you how to add documentation from XML comments.</span></span>

<span data-ttu-id="a63a3-126">각 API에는 예제 요청 및 응답 본문을 포함 하 여 자세한 정보를 사용 하 여 페이지에 대 한 링크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-126">Each API has a link to a page with more detailed information, including example request and response bodies.</span></span>

![](creating-api-help-pages/_static/image5.png)

## <a name="adding-help-pages-to-an-existing-project"></a><span data-ttu-id="a63a3-127">기존 프로젝트에 추가 도움말 페이지</span><span class="sxs-lookup"><span data-stu-id="a63a3-127">Adding Help Pages to an Existing Project</span></span>

<span data-ttu-id="a63a3-128">기존 Web API 프로젝트에 NuGet 패키지 관리자를 사용 하 여 도움말 페이지를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-128">You can add help pages to an existing Web API project by using NuGet Package Manager.</span></span> <span data-ttu-id="a63a3-129">이 옵션은 "Web API" 템플릿 보다 다른 프로젝트 템플릿에서 시작 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-129">This option is useful you start from a different project template than the "Web API" template.</span></span>

<span data-ttu-id="a63a3-130">**도구** 메뉴에서 **라이브러리 패키지 관리자**를 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-130">From the **Tools** menu, select **Library Package Manager**, and then select **Package Manager Console**.</span></span> <span data-ttu-id="a63a3-131">에 [패키지 관리자 콘솔](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) 창에서 다음 명령 중 하나를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-131">In the [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) window, type one of the following commands:</span></span>

<span data-ttu-id="a63a3-132">에 **C#** 응용 프로그램: `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span><span class="sxs-lookup"><span data-stu-id="a63a3-132">For a **C#** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span></span>

<span data-ttu-id="a63a3-133">에 **Visual Basic** 응용 프로그램: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span><span class="sxs-lookup"><span data-stu-id="a63a3-133">For a **Visual Basic** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span></span>

<span data-ttu-id="a63a3-134">두 개의 패키지, C# 및 Visual basic 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-134">There are two packages, one for C# and one for Visual Basic.</span></span> <span data-ttu-id="a63a3-135">프로젝트와 일치 하는 것을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-135">Make sure to use the one that matches your project.</span></span>

<span data-ttu-id="a63a3-136">이 명령은 필요한 어셈블리를 설치 하 고 (영역/HelpPage 폴더에 있음) 도움말 페이지에 대 한 MVC 보기 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-136">This command installs the necessary assemblies and adds the MVC views for the help pages (located in the Areas/HelpPage folder).</span></span> <span data-ttu-id="a63a3-137">도움말 페이지에 대 한 링크를 수동으로 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-137">You'll need to manually add a link to the Help page.</span></span> <span data-ttu-id="a63a3-138">URI가 /Help.</span><span class="sxs-lookup"><span data-stu-id="a63a3-138">The URI is /Help.</span></span> <span data-ttu-id="a63a3-139">Razor 보기에서 링크를 만들려면 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-139">To create a link in a razor view, add the following:</span></span>

[!code-cshtml[Main](creating-api-help-pages/samples/sample1.cshtml)]

<span data-ttu-id="a63a3-140">또한 영역을 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-140">Also, make sure to register areas.</span></span> <span data-ttu-id="a63a3-141">Global.asax 파일에 다음 코드를 추가 합니다 **응용 프로그램\_시작** 메서드를 사용할 수 없는 아직 경우:</span><span class="sxs-lookup"><span data-stu-id="a63a3-141">In the Global.asax file, add the following code to the **Application\_Start** method, if it is not there already:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample2.cs?highlight=4)]

## <a name="adding-api-documentation"></a><span data-ttu-id="a63a3-142">API 설명서를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-142">Adding API Documentation</span></span>

<span data-ttu-id="a63a3-143">기본적으로 도움말 페이지에 설명서에 대 한 자리 표시자 문자열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-143">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="a63a3-144">사용할 수 있습니다 [XML 문서 주석](https://msdn.microsoft.com/library/b2s063f7.aspx) 문서를 만들려면.</span><span class="sxs-lookup"><span data-stu-id="a63a3-144">You can use [XML documentation comments](https://msdn.microsoft.com/library/b2s063f7.aspx) to create the documentation.</span></span> <span data-ttu-id="a63a3-145">이 기능을 사용 하려면 영역/HelpPage/앱 파일을 엽니다\_Start/HelpPageConfig.cs 다음 줄을 주석 처리 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-145">To enable this feature, open the file Areas/HelpPage/App\_Start/HelpPageConfig.cs and uncomment the following line:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample3.cs)]

<span data-ttu-id="a63a3-146">이제 XML 문서를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-146">Now enable XML documentation.</span></span> <span data-ttu-id="a63a3-147">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-147">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="a63a3-148">선택 된 **빌드** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-148">Select the **Build** page.</span></span>

![](creating-api-help-pages/_static/image6.png)

<span data-ttu-id="a63a3-149">아래 **출력**, 체크 **XML 문서 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-149">Under **Output**, check **XML documentation file**.</span></span> <span data-ttu-id="a63a3-150">편집 상자에 입력 "앱\_Data/XmlDocument.xml"입니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-150">In the edit box, type "App\_Data/XmlDocument.xml".</span></span>

![](creating-api-help-pages/_static/image7.png)

<span data-ttu-id="a63a3-151">다음으로 코드를 열고는 `ValuesController` /Controllers/ValuesControler.cs에 정의 된 API 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-151">Next, open the code for the `ValuesController` API controller, which is defined in /Controllers/ValuesControler.cs.</span></span> <span data-ttu-id="a63a3-152">컨트롤러 메서드를 일부 문서 주석을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-152">Add some documentation comments to the controller methods.</span></span> <span data-ttu-id="a63a3-153">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="a63a3-153">For example:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="a63a3-154">팁: 메서드 위의 줄에 캐럿을 배치 하 고 3 개의 슬래시를 입력 하는 경우 Visual Studio 자동으로 삽입 하는 XML 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-154">Tip: If you position the caret on the line above the method and type three forward slashes, Visual Studio automatically inserts the XML elements.</span></span> <span data-ttu-id="a63a3-155">그런 다음 빈 칸에서 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-155">Then you can fill in the blanks.</span></span>


<span data-ttu-id="a63a3-156">이제 빌드 및 응용 프로그램을 다시 실행 및 도움말 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-156">Now build and run the application again, and navigate to the help pages.</span></span> <span data-ttu-id="a63a3-157">설명서 문자열 API 테이블에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-157">The documentation strings should appear in the API table.</span></span>

![](creating-api-help-pages/_static/image8.png)

<span data-ttu-id="a63a3-158">도움말 페이지를 런타임에 XML 파일에서 문자열을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-158">The help page reads the strings from the XML file at run time.</span></span> <span data-ttu-id="a63a3-159">(응용 프로그램을 배포할 때는 해야 XML 파일을 배포 합니다.)</span><span class="sxs-lookup"><span data-stu-id="a63a3-159">(When you deploy the application, make sure to deploy the XML file.)</span></span>

## <a name="under-the-hood"></a><span data-ttu-id="a63a3-160">내부 살펴보기</span><span class="sxs-lookup"><span data-stu-id="a63a3-160">Under the Hood</span></span>

<span data-ttu-id="a63a3-161">도움말 페이지의 맨 위에 빌드됩니다 합니다 **ApiExplorer** Web API 프레임 워크에 참가 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-161">The help pages are built on top of the **ApiExplorer** class, which is part of the Web API framework.</span></span> <span data-ttu-id="a63a3-162">합니다 **ApiExplorer** 클래스는 도움말 페이지를 만들기 위한 근본 자료를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-162">The **ApiExplorer** class provides the raw material for creating a help page.</span></span> <span data-ttu-id="a63a3-163">각 API에 대 한 **ApiExplorer** 포함 된 **ApiDescription** API를 설명 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-163">For each API, **ApiExplorer** contains an **ApiDescription** that describes the API.</span></span> <span data-ttu-id="a63a3-164">이 작업을 위해 "API" HTTP 메서드 및 상대 URI의 조합으로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-164">For this purpose, an "API" is defined as the combination of HTTP method and relative URI.</span></span> <span data-ttu-id="a63a3-165">예를 들어, 다음은 몇 가지 별개의 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-165">For example, here are some distinct APIs:</span></span>

- <span data-ttu-id="a63a3-166">/Api/Products 가져오기</span><span class="sxs-lookup"><span data-stu-id="a63a3-166">GET /api/Products</span></span>
- <span data-ttu-id="a63a3-167">가져오기/a p i/제품 / {id}</span><span class="sxs-lookup"><span data-stu-id="a63a3-167">GET /api/Products/{id}</span></span>
- <span data-ttu-id="a63a3-168">Api 제품 게시</span><span class="sxs-lookup"><span data-stu-id="a63a3-168">POST /api/Products</span></span>

<span data-ttu-id="a63a3-169">컨트롤러 작업에서 여러 HTTP 메서드를 지 원하는 경우는 **ApiExplorer** 고유한 API로 각 메서드를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-169">If a controller action supports multiple HTTP methods, the **ApiExplorer** treats each method as a distinct API.</span></span>

<span data-ttu-id="a63a3-170">API를 숨기려면를 **ApiExplorer**를 추가 합니다 **ApiExplorerSettings** 특성 집합과 작업을 *IgnoreApi* true로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-170">To hide an API from the **ApiExplorer**, add the **ApiExplorerSettings** attribute to the action and set *IgnoreApi* to true.</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample5.cs)]

<span data-ttu-id="a63a3-171">또한 전체 컨트롤러를 제외 하려면 컨트롤러에이 특성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-171">You can also add this attribute to the controller, to exclude the entire controller.</span></span>

<span data-ttu-id="a63a3-172">ApiExplorer 클래스의 설명서 문자열을 가져옵니다 합니다 **IDocumentationProvider** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-172">The ApiExplorer class gets documentation strings from the **IDocumentationProvider** interface.</span></span> <span data-ttu-id="a63a3-173">도움말 페이지 라이브러리에서 제공 하는 앞서 살펴본 대로 **IDocumentationProvider** 는 XML 문서 문자열에서 설명서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-173">As you saw earlier, the Help Pages library provides an **IDocumentationProvider** that gets documentation from XML documentation strings.</span></span> <span data-ttu-id="a63a3-174">코드는 /Areas/HelpPage/XmlDocumentationProvider.cs에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-174">The code is located in /Areas/HelpPage/XmlDocumentationProvider.cs.</span></span> <span data-ttu-id="a63a3-175">가져올 수 있습니다 설명서 다른 원본에서 작성 하 여 사용자 고유의 **IDocumentationProvider**합니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-175">You can get documentation from another source by writing your own **IDocumentationProvider**.</span></span> <span data-ttu-id="a63a3-176">호출 하 고 연결 하는 **SetDocumentationProvider** 에 정의 된 확장 메서드, **HelpPageConfigurationExtensions**</span><span class="sxs-lookup"><span data-stu-id="a63a3-176">To wire it up, call the **SetDocumentationProvider** extension method, defined in **HelpPageConfigurationExtensions**</span></span>

<span data-ttu-id="a63a3-177">**ApiExplorer** 에 자동으로 호출 합니다 **IDocumentationProvider** 인터페이스 각 API에 대 한 설명서 문자열을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-177">**ApiExplorer** automatically calls into the **IDocumentationProvider** interface to get documentation strings for each API.</span></span> <span data-ttu-id="a63a3-178">에 저장 합니다 **설명서** 의 속성을 **ApiDescription** 및 **ApiParameterDescription** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-178">It stores them in the **Documentation** property of the **ApiDescription** and **ApiParameterDescription** objects.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a63a3-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a63a3-179">Next Steps</span></span>

<span data-ttu-id="a63a3-180">여기에 표시 된 도움말 페이지에 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-180">You aren't limited to the help pages shown here.</span></span> <span data-ttu-id="a63a3-181">사실 **ApiExplorer** 도움말 페이지를 만들기로 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a63a3-181">In fact, **ApiExplorer** is not limited to creating help pages.</span></span> <span data-ttu-id="a63a3-182">기본적으로 생각 하는 데 몇 가지 훌륭한 블로그 게시물 Yao Huang Lin 기록한:</span><span class="sxs-lookup"><span data-stu-id="a63a3-182">Yao Huang Lin has written some great blog posts to get you thinking out of the box:</span></span>

- [<span data-ttu-id="a63a3-183">ASP.NET Web API 도움말 페이지에는 간단한 테스트 클라이언트 추가</span><span class="sxs-lookup"><span data-stu-id="a63a3-183">Adding a simple Test Client to ASP.NET Web API Help Page</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/02/adding-a-simple-test-client-to-asp-net-web-api-help-page.aspx)
- [<span data-ttu-id="a63a3-184">자체 호스팅된 서비스에서 작동 하는 ASP.NET Web API 도움말 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="a63a3-184">Making ASP.NET Web API Help Page work on self-hosted services</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/20/making-asp-net-web-api-help-page-work-on-self-hosted-services.aspx)
- [<span data-ttu-id="a63a3-185">ASP.NET Web API에 대 한 도움말 페이지 (또는 클라이언트)의 디자인 타임 생성</span><span class="sxs-lookup"><span data-stu-id="a63a3-185">Design-time generation of help page (or client) for ASP.NET Web API</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2013/01/20/design-time-generation-of-help-page-or-proxy-for-asp-net-web-api.aspx)
- [<span data-ttu-id="a63a3-186">고급 도움말 페이지 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="a63a3-186">Advanced Help Page customizations</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/10/asp-net-web-api-help-page-part-3-advanced-help-page-customizations.aspx)
