---
uid: web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
title: 에서 만들고 사용 하는 도우미 ASP.NET 웹 페이지 (Razor) 사이트 | Microsoft Docs
author: Rick-Anderson
description: 이 문서에서는 ASP.NET Web Pages (Razor) 웹 사이트에서 도우미를 만드는 방법을 설명 합니다. 도우미는 코드와 성능에 태그를 포함 하는 재사용 가능한 구성 하는 중...
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 46bff772-01e0-40f0-9ae6-9e18c5442ee6
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 3b54ba8a35a354eb0562a47866cd8b5dcb66bc86
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021510"
---
<a name="creating-and-using-a-helper-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="fd8dd-104">만들기 및 ASP.NET 웹 페이지 (Razor) 사이트에서 도우미 사용</span><span class="sxs-lookup"><span data-stu-id="fd8dd-104">Creating and Using a Helper in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="fd8dd-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="fd8dd-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="fd8dd-106">이 문서에서는 ASP.NET Web Pages (Razor) 웹 사이트에서 도우미를 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-106">This article describes how to create a helper in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="fd8dd-107">A *도우미* 코드와 길거나 복잡 한 않을 수 있는 작업을 수행 하는 태그를 포함 하는 재사용 가능한 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-107">A *helper* is a reusable component that includes code and markup to perform a task that might be tedious or complex.</span></span>
> 
> <span data-ttu-id="fd8dd-108">**학습할 내용:**</span><span class="sxs-lookup"><span data-stu-id="fd8dd-108">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="fd8dd-109">만들고 간단한 도우미를 사용 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-109">How to create and use a simple helper.</span></span>
> 
> <span data-ttu-id="fd8dd-110">다음은 문서에 도입 된 ASP.NET 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-110">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="fd8dd-111">`@helper` 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-111">The `@helper` syntax.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="fd8dd-112">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="fd8dd-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="fd8dd-113">ASP.NET Web Pages (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="fd8dd-113">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="fd8dd-114">이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-114">This tutorial also works with ASP.NET Web Pages 2.</span></span>


## <a name="overview-of-helpers"></a><span data-ttu-id="fd8dd-115">도우미의 개요</span><span class="sxs-lookup"><span data-stu-id="fd8dd-115">Overview of Helpers</span></span>

<span data-ttu-id="fd8dd-116">사이트의 여러 페이지에 동일한 작업을 수행 해야 할 경우에 도우미를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-116">If you need to perform the same tasks on different pages in your site, you can use a helper.</span></span> <span data-ttu-id="fd8dd-117">다운로드 및 설치할 수 있는 기능이 더 많이 및 ASP.NET 웹 페이지에는 도우미 수가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-117">ASP.NET Web Pages includes a number of helpers, and there are many more that you can download and install.</span></span> <span data-ttu-id="fd8dd-118">(ASP.NET 웹 페이지에서 기본 제공 도우미 목록에 나열 됩니다는 [ASP.NET API 빠른 참조](https://go.microsoft.com/fwlink/?LinkId=202907).) 요구 사항을 충족할 수 없는 기존 도우미를 사용자 고유의 도우미를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-118">(A list of the built-in helpers in ASP.NET Web Pages is listed in the [ASP.NET API Quick Reference](https://go.microsoft.com/fwlink/?LinkId=202907).) If none of the existing helpers meet your needs, you can create your own helper.</span></span>

<span data-ttu-id="fd8dd-119">도우미를 사용 하면 공통 코드 블록을 사용 하 여 여러 페이지에 걸쳐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-119">A helper lets you use a common block of code across multiple pages.</span></span> <span data-ttu-id="fd8dd-120">페이지에서 종종 한다고 가정 일반 단락 외에도 설정 되어 있는 참고 항목을 만들려면.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-120">Suppose that in your page you often want to create a note item that's set apart from normal paragraphs.</span></span> <span data-ttu-id="fd8dd-121">참고 프로토타입이라 아마도 `<div>` 요소는 테두리가 있는 상자로 스타일이 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-121">Perhaps the note is created as a `<div>` element that's styled as a box with a border.</span></span> <span data-ttu-id="fd8dd-122">메모를 표시할 때마다 페이지에이 동일한 태그를 추가, 하기 보다는 태그 도우미로 패키징할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-122">Rather than add this same markup to a page every time you want to display a note, you can package the markup as a helper.</span></span> <span data-ttu-id="fd8dd-123">단일 코드 줄을 사용 하 여 참고 삽입할 수 있습니다 해야 아무 곳 이나 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-123">You can then insert the note with a single line of code anywhere you need it.</span></span>

<span data-ttu-id="fd8dd-124">다음과 같은 도우미를 사용 하 여 사용 하면 코드를 각 페이지에 간단 하 고 쉽게 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-124">Using a helper like this makes the code in each of your pages simpler and easier to read.</span></span> <span data-ttu-id="fd8dd-125">또한 쉽게 사이트를 유지 하기 위해 정보를 표시 되는 방식을 변경 해야 할 경우 한 곳에서 태그를 변경할 수 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-125">It also makes it easier to maintain your site, because if you need to change how the notes look, you can change the markup in one place.</span></span>

## <a name="creating-a-helper"></a><span data-ttu-id="fd8dd-126">도우미 만들기</span><span class="sxs-lookup"><span data-stu-id="fd8dd-126">Creating a Helper</span></span>

<span data-ttu-id="fd8dd-127">이 절차에서는 위에서 설명한 대로 메모를 만드는 도우미를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-127">This procedure shows you how to create the helper that creates the note, as just described.</span></span> <span data-ttu-id="fd8dd-128">간단한 예 이지만 사용자 지정 도우미는 모든 태그 및 해야 하는 ASP.NET 코드가 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-128">This is a simple example, but the custom helper can include any markup and ASP.NET code that you need.</span></span>

1. <span data-ttu-id="fd8dd-129">웹 사이트의 루트 폴더에서 라는 폴더를 만듭니다 *앱\_코드*합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-129">In the root folder of the website, create a folder named *App\_Code*.</span></span> <span data-ttu-id="fd8dd-130">도우미와 같은 구성 요소에 대 한 코드를 넣을 수 있는 ASP.NET에는 예약 된 폴더 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-130">This is a reserved folder name in ASP.NET where you can put code for components like helpers.</span></span>
2. <span data-ttu-id="fd8dd-131">에 *앱\_코드* 폴더를 만듭니다 *.cshtml* 파일을 이름을 *MyHelpers.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-131">In the *App\_Code* folder create a new *.cshtml* file and name it *MyHelpers.cshtml*.</span></span>
3. <span data-ttu-id="fd8dd-132">기존 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-132">Replace the existing content with the following:</span></span>

    [!code-cshtml[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    <span data-ttu-id="fd8dd-133">코드를 사용 하는 `@helper` 라는 새 도우미를 선언 하는 구문을 `MakeNote`합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-133">The code uses the `@helper` syntax to declare a new helper named `MakeNote`.</span></span> <span data-ttu-id="fd8dd-134">이 특정 도우미를 사용 하면 명명 된 매개 변수 전달 `content` 텍스트와 태그의 조합을 포함할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-134">This particular helper lets you pass a parameter named `content` that can contain a combination of text and markup.</span></span> <span data-ttu-id="fd8dd-135">도우미를 사용 하 여 참고 본문 문자열을 삽입 하는 `@content` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-135">The helper inserts the string into the note body using the `@content` variable.</span></span>

    <span data-ttu-id="fd8dd-136">파일 이름이 *MyHelpers.cshtml*을 도우미 라고 하지만 `MakeNote`합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-136">Notice that the file is named *MyHelpers.cshtml*, but the helper is named `MakeNote`.</span></span> <span data-ttu-id="fd8dd-137">단일 파일에 여러 사용자 지정 도우미를 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-137">You can put multiple custom helpers into a single file.</span></span>
4. <span data-ttu-id="fd8dd-138">파일을 저장한 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-138">Save and close the file.</span></span>

## <a name="using-the-helper-in-a-page"></a><span data-ttu-id="fd8dd-139">도우미를 사용 하 여 페이지에서</span><span class="sxs-lookup"><span data-stu-id="fd8dd-139">Using the Helper in a Page</span></span>

1. <span data-ttu-id="fd8dd-140">루트 폴더에서 라는 새 빈 파일을 만듭니다 *TestHelper.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-140">In the root folder, create a new blank file called *TestHelper.cshtml*.</span></span>
2. <span data-ttu-id="fd8dd-141">파일에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-141">Add the following code to the file:</span></span>

    [!code-html[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample2.html)]

    <span data-ttu-id="fd8dd-142">사용 하 여 만든 도우미를 호출 하려면 `@` 여기서 도우미는, 점, 파일 이름 및 다음 도우미 이름 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-142">To call the helper you created, use `@` followed by the file name where the helper is, a dot, and then the helper name.</span></span> <span data-ttu-id="fd8dd-143">(여러 폴더 설치한 경우 합니다 *앱\_코드* 폴더를 구문을 사용할 수 있습니다 `@FolderName.FileName.HelperName` 중첩 된 폴더 수준 내에서 도우미를 호출 하).</span><span class="sxs-lookup"><span data-stu-id="fd8dd-143">(If you had multiple folders in the *App\_Code* folder, you could use the syntax `@FolderName.FileName.HelperName` to call your helper within any nested folder level).</span></span> <span data-ttu-id="fd8dd-144">괄호 안에 인용 부호 안에 추가 하는 텍스트에는 웹 페이지에서 메모의 일부로 도우미를 표시 하는 텍스트가입니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-144">The text that you add in quotation marks within the parentheses is the text that the helper will display as part of the note in the web page.</span></span>
3. <span data-ttu-id="fd8dd-145">페이지를 저장 하 고 브라우저에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-145">Save the page and run it in a browser.</span></span> <span data-ttu-id="fd8dd-146">참고 항목 오른쪽 도우미를 호출 하는 위치를 생성 하는 도우미: 두 단락 간에 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-146">The helper generates the note item right where you called the helper: between the two paragraphs.</span></span>

    ![페이지에는 브라우저 도우미에서 지정된 된 텍스트 주위에 상자를 배치 하는 태그를 생성 하는 방법을 보여주는 스크린샷.](creating-and-using-a-helper-in-an-aspnet-web-pages-site/_static/image1.jpg)

## <a name="additional-resources"></a><span data-ttu-id="fd8dd-148">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="fd8dd-148">Additional Resources</span></span>


<span data-ttu-id="fd8dd-149">[Razor 도우미로 가로 메뉴](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-149">[Horizontal menu as a Razor helper](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341).</span></span> <span data-ttu-id="fd8dd-150">Mike 되 여이 블로그 항목에는 태그, CSS 및 코드를 사용 하 여 도우미로 가로 메뉴를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-150">This blog entry by Mike Pope shows how to create a horizontal menu as a helper using markup, CSS, and code.</span></span>

<span data-ttu-id="fd8dd-151">[WebMatrix 및 ASP.NET mvc 3에 대 한 도우미 페이지 ASP.NET 웹에서 HTML5를 활용 하 여](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx)입니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-151">[Leveraging HTML5 in ASP.NET Web Pages Helpers for WebMatrix and ASP.NET MVC3](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx).</span></span> <span data-ttu-id="fd8dd-152">이 블로그 항목 Sam Abraham에서 HTML5를 렌더링 하는 도우미를 보여 줍니다. `Canvas` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-152">This blog entry by Sam Abraham shows a helper that renders an HTML5 `Canvas` element.</span></span>

<span data-ttu-id="fd8dd-153">[차이점 @Helpers 하 고 @Functions WebMatrix에서](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-153">[The Difference Between @Helpers and @Functions in WebMatrix](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix).</span></span> <span data-ttu-id="fd8dd-154">Mike Brind 하 여이 블로그 항목에 설명 합니다 `@helper` 구문 및 `@function` 구문 및 각 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="fd8dd-154">This blog entry by Mike Brind describes `@helper` syntax and `@function` syntax and when to use each.</span></span>
