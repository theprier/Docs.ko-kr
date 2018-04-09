---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
title: ASP.NET 웹 페이지를 소개-일관 된 레이아웃 만들기 | Microsoft Docs
author: tfitzmac
description: 이 자습서에서는 레이아웃을 사용 하 여 페이지에 일관 된 모양을 ASP.NET 웹 페이지를 사용 하는 사이트를 만들려고 하는 방법을 보여 줍니다. 완료 한 것으로 가정는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: c85ec591-f8d7-4882-b763-de6ab9f3df7a
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
msc.type: authoredcontent
ms.openlocfilehash: c2d5c4d8ed8a71979c16d484ab90d283a45de537
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="introducing-aspnet-web-pages---creating-a-consistent-layout"></a><span data-ttu-id="6b216-104">ASP.NET 웹 페이지-일관 된 레이아웃 만들기 소개</span><span class="sxs-lookup"><span data-stu-id="6b216-104">Introducing ASP.NET Web Pages - Creating a Consistent Layout</span></span>
====================
<span data-ttu-id="6b216-105">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="6b216-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="6b216-106">이 자습서를 사용 하는 방법을 보여 줍니다. *레이아웃* 페이지에 일관 된 모양을 ASP.NET 웹 페이지를 사용 하는 사이트를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-106">This tutorial shows you how to use *layouts* to create a consistent look for the pages on a site that uses ASP.NET Web Pages.</span></span> <span data-ttu-id="6b216-107">통해 시리즈를 완료 한 것으로 가정 [ASP.NET 웹 페이지에서 데이터베이스 데이터 삭제](https://go.microsoft.com/fwlink/?LinkId=251584)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-107">It assumes you have completed the series through [Deleting Database Data in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251584).</span></span>
> 
> <span data-ttu-id="6b216-108">학습 내용:</span><span class="sxs-lookup"><span data-stu-id="6b216-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="6b216-109">레이아웃 페이지가입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-109">What a layout page is.</span></span>
> - <span data-ttu-id="6b216-110">동적 콘텐츠가 있는 레이아웃 페이지를 결합 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-110">How to combine layout pages with dynamic content.</span></span>
> - <span data-ttu-id="6b216-111">레이아웃 페이지에 값을 전달 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="6b216-111">How to pass values to a layout page.</span></span>


## <a name="about-layouts"></a><span data-ttu-id="6b216-112">레이아웃 정보</span><span class="sxs-lookup"><span data-stu-id="6b216-112">About Layouts</span></span>

<span data-ttu-id="6b216-113">지금까지 만든 페이지 모두 완료 된, 독립 실행형 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-113">The pages you've created so far have all been complete, standalone pages.</span></span> <span data-ttu-id="6b216-114">동일한 사이트에 속한 모두 있지만 없습니다 모든 공통 요소 또는 표준 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-114">They all belong to the same site, but they don't have any common elements or a standard look.</span></span>

<span data-ttu-id="6b216-115">대부분의 사이트는 일관 된 모양과 레이아웃 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-115">Most sites do have a consistent look and layout.</span></span> <span data-ttu-id="6b216-116">예를 들어, 이동 하는 경우는 [Microsoft.com/web](https://www.microsoft.com/web/) 사이트 및 둘러보세요를 모든 페이지 전체 레이아웃을 시각적 테마를 준수 하는 것이 표시:</span><span class="sxs-lookup"><span data-stu-id="6b216-116">For example, if you go to the [Microsoft.com/web](https://www.microsoft.com/web/) site and look around, you see that the pages all adhere to an overall layout and to a visual theme:</span></span>

![헤더, 탐색 영역, 콘텐츠 영역 및 바닥글의 레이아웃을 보여 주는 Microsoft.com/web 사이트 페이지](layouts/_static/image1.png)

<span data-ttu-id="6b216-118">*비효율적인* 이 레이아웃을 만드는 방법은 각 페이지에 머리글, 탐색 모음과 바닥글을 개별적으로 정의 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-118">An *inefficient* way to create this layout would be to define a header, navigation bar, and footer separately on each of your pages.</span></span> <span data-ttu-id="6b216-119">사용자는 복제 동일한 태그 될 때마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-119">You'd be duplicating the same markup each time.</span></span> <span data-ttu-id="6b216-120">옵션을 변경 하려는 경우 (예를 들어 업데이트 바닥글) 각 페이지를 개별적으로 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-120">If you wanted to change something (for example, update the footer), you'd have to change each page separately.</span></span>

<span data-ttu-id="6b216-121">Where 즉 *레이아웃 페이지* 와 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-121">That's where *layout pages* come in.</span></span> <span data-ttu-id="6b216-122">ASP.NET 웹 페이지에서 사이트에 있는 페이지에 대 한 전체 컨테이너를 제공 하는 레이아웃 페이지를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-122">In ASP.NET Web Pages, you can define a layout page that provides an overall container for pages on your site.</span></span> <span data-ttu-id="6b216-123">예를 들어, 레이아웃 페이지, 탐색 영역에서 머리글과 바닥글을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-123">For example, the layout page can contain the header, navigation area, and footer.</span></span> <span data-ttu-id="6b216-124">레이아웃 페이지 주 콘텐츠 흐름 방향은 자리 표시자를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-124">The layout page includes a placeholder where the main content goes.</span></span>

<span data-ttu-id="6b216-125">다음 태그와 해당 페이지에만 대 한 코드를 포함 하는 개별 콘텐츠 페이지를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-125">You can then define individual content pages that contain the markup and the code for only that page.</span></span> <span data-ttu-id="6b216-126">콘텐츠 페이지를 HTML 페이지 전체; 쓸 필요가 없습니다. 가 전환할 필요도 `<body>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-126">Content pages don't have to be complete HTML pages; they don't even have to have a `<body>` element.</span></span> <span data-ttu-id="6b216-127">레이아웃 페이지의 콘텐츠를 표시 하려면 ASP.NET 지시 하는 코드 줄도 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-127">They also have a line of code that tells ASP.NET what layout page you want to display the content in.</span></span> <span data-ttu-id="6b216-128">다음은이 관계의 작동 원리 대략 보여 주는 그림이입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-128">Here's a picture that shows roughly how this relationship works:</span></span>

![두 콘텐츠 페이지 및 들어갈 있는 레이아웃 페이지를 보여 주는 개념 다이어그램](layouts/_static/image2.png)

<span data-ttu-id="6b216-130">이 상호 작용 작업에서 참조 하는 경우를 이해 하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-130">This interaction is easy to understand when you see it in action.</span></span> <span data-ttu-id="6b216-131">이 자습서에서는 레이아웃을 사용 하 여 동영상 페이지를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-131">In this tutorial, you'll change your movies pages to use a layout.</span></span>

## <a name="adding-a-layout-page"></a><span data-ttu-id="6b216-132">레이아웃 페이지 추가</span><span class="sxs-lookup"><span data-stu-id="6b216-132">Adding a Layout Page</span></span>

<span data-ttu-id="6b216-133">머리글, 바닥글 및 주 콘텐츠에 대 한 영역에 있는 일반적인 페이지 레이아웃을 정의 하는 레이아웃 페이지를 만들어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-133">You'll start by creating a layout page that defines a typical page layout with a header, footer, and an area for the main content.</span></span> <span data-ttu-id="6b216-134">WebPagesMovies 사이트에서 추가 라는 CSHTML 페이지  *\_Layout.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-134">In the WebPagesMovies site, add a CSHTML page named *\_Layout.cshtml*.</span></span>

<span data-ttu-id="6b216-135">선행 밑줄 ( `_` ) 문자는 매우 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-135">The leading underscore ( `_` ) character is significant.</span></span> <span data-ttu-id="6b216-136">페이지의 이름은 밑줄로 시작 되 면 ASP.NET 브라우저에 해당 페이지를 직접 보내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-136">If a page's name starts with an underscore, ASP.NET won't directly send that page to the browser.</span></span> <span data-ttu-id="6b216-137">이 규칙은 사이트에 필요한 없지만 사용자가 직접 요청할 수 아니어야 합니다. 페이지를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-137">This convention lets you define pages that are required for your site but that users shouldn't be able to request directly.</span></span>

<span data-ttu-id="6b216-138">다음 페이지의 내용을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-138">Replace the content in the page with the following:</span></span>

[!code-html[Main](layouts/samples/sample1.html)]

<span data-ttu-id="6b216-139">이 태그는 HTML을 사용 하는 바로 볼 수 있듯이 `<div>` 더 페이지와 1에서 3 개의 섹션을 정의 하는 요소 `<div>` 세 개의 섹션을 보유 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-139">As you can see, this markup is just HTML that uses `<div>` elements to define three sections in the page plus one more `<div>` element to hold the three sections.</span></span> <span data-ttu-id="6b216-140">Razor 코드의 비트를 포함 하는 바닥글: `@DateTime.Now.Year`, 페이지의 위치에 있는 현재 연도 렌더링 합니다입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-140">The footer contains a bit of Razor code: `@DateTime.Now.Year`, which will render the current year at that location in the page.</span></span>

<span data-ttu-id="6b216-141">명명 된 스타일 시트에 대 한 링크는 *Movies.css*합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-141">Notice that there's a link to a style sheet named *Movies.css*.</span></span> <span data-ttu-id="6b216-142">스타일 시트는 요소의 실제 레이아웃의 세부 정보는 정의 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-142">The style sheet is where the details of the physical layout of the elements will be defined.</span></span> <span data-ttu-id="6b216-143">잠시 후에 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-143">You'll create that in a moment.</span></span>

<span data-ttu-id="6b216-144">이 독특한 기능  *\_Layout.cshtml* 페이지는는 `@Render.Body()` 선입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-144">The only unusual feature in this *\_Layout.cshtml* page is the `@Render.Body()` line.</span></span> <span data-ttu-id="6b216-145">이 레이아웃은 다른 페이지와 병합 될 때 콘텐츠 어디로 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-145">That's the placeholder where the content will go when this layout is merged with another page.</span></span>

## <a name="adding-a-css-file"></a><span data-ttu-id="6b216-146">.Css 파일 추가</span><span class="sxs-lookup"><span data-stu-id="6b216-146">Adding a .css File</span></span>

<span data-ttu-id="6b216-147">해당 페이지에서 요소의 실제 정렬 (즉, 모양)을 정의 하는 기본 방법은 연계 스타일 시트 (CSS) 규칙을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-147">The preferred way to define the actual arrangement (that is, appearance) of elements on the page is to use cascading style sheet (CSS) rules.</span></span> <span data-ttu-id="6b216-148">만들 수 있도록 한 *.css* 새 레이아웃에 대 한 규칙을 포함 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-148">So you'll create a *.css* file that has the rules for your new layout.</span></span>

<span data-ttu-id="6b216-149">WebMatrix에서 사이트의 루트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-149">In WebMatrix, select the root of your site.</span></span> <span data-ttu-id="6b216-150">그런 다음는 **파일** 탭 리본 메뉴의 아래의 화살표를 클릭 합니다.는 **새로** 단추를 선택한 다음 클릭 **새 폴더**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-150">Then in the **Files** tab of the ribbon, click the arrow under the **New** button and then click **New Folder**.</span></span>

![리본에서 새로 ' 새 폴더 ' 옵션입니다.](layouts/_static/image3.png)

<span data-ttu-id="6b216-152">새 폴더 이름을 *스타일*합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-152">Name the new folder *Styles*.</span></span>

![새 폴더 '스타일' 이름 지정](layouts/_static/image4.png)

<span data-ttu-id="6b216-154">새로운 내부 *스타일* 폴더 라는 파일을 만들어 *Movies.css*합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-154">Inside the new *Styles* folder, create a file named *Movies.css*.</span></span>

![새 Movies.css 파일 만들기](layouts/_static/image5.png)

<span data-ttu-id="6b216-156">새 내용을 바꾸는 *.css* 다음 파일:</span><span class="sxs-lookup"><span data-stu-id="6b216-156">Replace the contents of the new *.css* file with the following:</span></span>

[!code-css[Main](layouts/samples/sample2.css)]

<span data-ttu-id="6b216-157">두 가지를 확인을 제외 하 고 이러한 CSS 규칙에 대해 잘 다루지 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-157">We won't say much about these CSS rules, except to note two things.</span></span> <span data-ttu-id="6b216-158">하나는 글꼴 및 크기를 설정 하는, 규칙 사용 하 여 절대 위치 설정 머리글, 바닥글 및 주 콘텐츠 영역의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-158">One is that in addition to setting fonts and sizes, the rules use absolute positioning to establish the location of the header, footer, and main content area.</span></span> <span data-ttu-id="6b216-159">읽을 수 있으면를 처음 접하는 CSS에 배치 하는 [CSS 위치](http://www.w3schools.com/css/css_positioning.asp) W3Schools 사이트 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-159">If you're new to positioning in CSS, you can read the [CSS Positioning](http://www.w3schools.com/css/css_positioning.asp) tutorial at the W3Schools site.</span></span>

<span data-ttu-id="6b216-160">에 개별적으로 정의 아래쪽에서 우리 스타일 규칙 원래을 복사 했는지 확인 하는 것은 *Movies.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-160">The other thing to note is that at the bottom, we've copied the style rules that were originally defined individually in the *Movies.cshtml* file.</span></span> <span data-ttu-id="6b216-161">이러한 규칙에 사용 된는 [데이터를 표시 하 여 사용 하 여 ASP.NET 웹 페이지 소개](https://go.microsoft.com/fwlink/?LinkId=251580) 확인 하기 위해 자습서는 `WebGrid` 도우미 테이블에 줄무늬를 추가 하는 태그를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-161">These rules were used in the [Introduction to Displaying Data by Using ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251580) tutorial to make the `WebGrid` helper render markup that added stripes to the table.</span></span> <span data-ttu-id="6b216-162">(사용 하는 경우는 *.css* 파일 스타일 정의 대 한 수도 기록 하는 전체 사이트에 대 한 스타일 규칙입니다.)</span><span class="sxs-lookup"><span data-stu-id="6b216-162">(If you're going to use a *.css* file for style definitions, you might as well put the style rules for the whole site in it.)</span></span>

## <a name="updating-the-movies-file-to-use-the-layout"></a><span data-ttu-id="6b216-163">레이아웃을 사용 하 여 영화 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="6b216-163">Updating the Movies File to Use the Layout</span></span>

<span data-ttu-id="6b216-164">이제 새 레이아웃을 사용 하도록 사이트를 기존 파일을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-164">Now you can update the existing files in your site to use the new layout.</span></span> <span data-ttu-id="6b216-165">열기는 *Movies.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-165">Open the *Movies.cshtml* file.</span></span> <span data-ttu-id="6b216-166">맨 위에 있는 코드의 첫 번째 줄으로 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-166">At the top, as the first line of code, add the following:</span></span>

[!code-csharp[Main](layouts/samples/sample3.cs)]

<span data-ttu-id="6b216-167">페이지는이 방법으로 이제 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-167">The page now starts out this way:</span></span>

[!code-cshtml[Main](layouts/samples/sample4.cshtml?highlight=2)]

<span data-ttu-id="6b216-168">이 한 줄의 코드 asp 때는 *동영상* 페이지가 실행와 병합 해야는  *\_Layout.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-168">This one line of code tells ASP.NET that when the *Movies* page runs, it should be merged with the *\_Layout.cshtml* file.</span></span>

<span data-ttu-id="6b216-169">이후는 *Movies.cshtml* 레이아웃 페이지에 이제 사용 하 여 파일에서 태그를 제거할 수는 *Movies.cshtml* 에서 처리에 있는 페이지는  *\_Layout.cshtml*파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-169">Since the *Movies.cshtml* file now uses a layout page, you can remove the markup from the *Movies.cshtml* page that's taken care of by the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="6b216-170">꺼내서는 `<!DOCTYPE>`, `<html>`, 및 `<body>` 태그 및 닫는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-170">Take out the `<!DOCTYPE>`, `<html>`, and `<body>` opening and closing tags.</span></span> <span data-ttu-id="6b216-171">전체 꺼내서 `<head>` 요소와 해당 규칙에 있으므로 이제 이후 눈금에 대 한 스타일 규칙을 포함 하는 해당 콘텐츠는 *.css* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-171">Take out the entire `<head>` element and its contents, which includes the style rules for the grid, since you've now got those rules in a *.css* file.</span></span> <span data-ttu-id="6b216-172">에 있을 때 기존 변경 `<h1>` 요소는 `<h2>` 요소;는 `<h1>` 이미 레이아웃 페이지의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-172">While you're at it, change the existing `<h1>` element to an `<h2>` element; you have an `<h1>` element in the layout page already.</span></span> <span data-ttu-id="6b216-173">변경 된 `<h2>` 텍스트 "동영상 목록"입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-173">Change the `<h2>` text to "List Movies".</span></span>

<span data-ttu-id="6b216-174">일반적으로 콘텐츠 페이지에 변경이 내용을 확인 해야 할가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-174">Normally you wouldn't have to make these sorts of changes in a content page.</span></span> <span data-ttu-id="6b216-175">레이아웃 페이지를 사이트를 시작 하면 이러한 모든 요소 없이 콘텐츠 페이지부터 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-175">When you start your site out with a layout page, you create content pages without all these elements to begin with.</span></span> <span data-ttu-id="6b216-176">이 경우 하지만 변환 대상 독립 실행형 페이지 하나 이므로 약간의 정리 레이아웃을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-176">In this case, though, you're converting a standalone page to one that uses a layout, so there's a bit of cleanup.</span></span>

<span data-ttu-id="6b216-177">완료 되 면는 *Movies.cshtml* 페이지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-177">When you're finished, the *Movies.cshtml* page will look like the following:</span></span>

[!code-cshtml[Main](layouts/samples/sample5.cshtml)]

### <a name="testing-the-layout"></a><span data-ttu-id="6b216-178">레이아웃 테스트</span><span class="sxs-lookup"><span data-stu-id="6b216-178">Testing the Layout</span></span>

<span data-ttu-id="6b216-179">이제 레이아웃의 모양을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-179">Now you can see what the layout looks like.</span></span> <span data-ttu-id="6b216-180">WebMatrix에서 마우스 오른쪽 단추로 클릭는 *Movies.cshtml* 페이지로 돌아간 후 선택 **브라우저에서 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-180">In WebMatrix, right-click the *Movies.cshtml* page and select **Launch in browser**.</span></span> <span data-ttu-id="6b216-181">브라우저 페이지를 표시 하는 경우이 페이지를 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-181">When the browser displays the page, it looks like this page:</span></span>

![동영상 페이지 레이아웃을 사용 하 여 렌더링](layouts/_static/image6.png)

<span data-ttu-id="6b216-183">ASP.NET은 병합에 Movies.cshtml 페이지의 콘텐츠는  *\_Layout.cshtml* 페이지 오른쪽 위치는 `RenderBody` 메서드는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-183">ASP.NET has merged the content of the Movies.cshtml page into the *\_Layout.cshtml* page right where the `RenderBody` method is.</span></span> <span data-ttu-id="6b216-184">물론 및는  *\_Layout.cshtml* 페이지 참조는 *.css* 페이지의 모양을 정의 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-184">And of course the *\_Layout.cshtml* page references a *.css* file that defines the look of the page.</span></span>

## <a name="updating-the-addmovie-page-to-use-the-layout"></a><span data-ttu-id="6b216-185">AddMovie 페이지 레이아웃을 사용 하려면 업데이트</span><span class="sxs-lookup"><span data-stu-id="6b216-185">Updating the AddMovie Page to Use the Layout</span></span>

<span data-ttu-id="6b216-186">레이아웃의 실제 이점은 사용할 수 있는 이러한 모든 페이지에 대 한 사이트에서입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-186">The real benefit of layouts is that you can use them for all the pages in your site.</span></span> <span data-ttu-id="6b216-187">열기는 *AddMovie.cshtml* 페이지.</span><span class="sxs-lookup"><span data-stu-id="6b216-187">Open the *AddMovie.cshtml* page.</span></span>

<span data-ttu-id="6b216-188">있습니다 수 있다는 점을 잘 알고는 *AddMovie.cshtml* 페이지 원래에 게 일부 CSS 규칙의 유효성 검사 오류 메시지의 모양을 정의 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-188">You might remember that the *AddMovie.cshtml* page originally had some CSS rules in it to define the look of validation error messages.</span></span> <span data-ttu-id="6b216-189">했으므로 *.css* 지금 사이트에 대 한 파일, 이러한 규칙을 이동할 수 있습니다는 *.css* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-189">Since you have a *.css* file for your site now, you can move those rules to the *.css* file.</span></span> <span data-ttu-id="6b216-190">제거는 *AddMovie.cshtml* 파일의 맨 아래에 추가 하는 *Movies.css* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-190">Remove them from the *AddMovie.cshtml* file and add them to the bottom of the *Movies.css* file.</span></span> <span data-ttu-id="6b216-191">다음 규칙 이동 하는:</span><span class="sxs-lookup"><span data-stu-id="6b216-191">You are moving the following rules:</span></span>

[!code-css[Main](layouts/samples/sample6.css)]

<span data-ttu-id="6b216-192">같은 종류의 변경 내용 확인 *AddMovie.cshtml* 에 대 한 사용 하 던 *Movies.cshtml* -추가 `Layout="~/_Layout.cshtml;` 는 불필요 한 이제는 HTML 태그를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-192">Now make the same sorts of changes in *AddMovie.cshtml* that you did for *Movies.cshtml* — add `Layout="~/_Layout.cshtml;` and remove the HTML markup that's now extraneous.</span></span> <span data-ttu-id="6b216-193">변경 된 `<h1>` 요소의 `<h2>`합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-193">Change the `<h1>` element to `<h2>`.</span></span> <span data-ttu-id="6b216-194">완료 되 면 페이지는이 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-194">When you're done, the page will look like this example:</span></span>

[!code-cshtml[Main](layouts/samples/sample7.cshtml)]

<span data-ttu-id="6b216-195">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-195">Run the page.</span></span> <span data-ttu-id="6b216-196">이제이 그림과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-196">Now it looks like this illustration:</span></span>

![동영상 추가' 페이지 레이아웃을 사용 하 여 렌더링](layouts/_static/image7.png)

<span data-ttu-id="6b216-198">사이트의 페이지에 대 한 유사한 변경 하려는- *EditMovie.cshtml* 및 *DeleteMovie.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-198">You want to make similar changes to the pages in the site — *EditMovie.cshtml* and *DeleteMovie.cshtml*.</span></span> <span data-ttu-id="6b216-199">그러나, 수행 하기 전에 또 다른 변경 좀 더 융통성이 레이아웃을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-199">However, before you do, you can make another change to the layout that makes it a little more flexible.</span></span>

## <a name="passing-title-information-to-the-layout-page"></a><span data-ttu-id="6b216-200">레이아웃 페이지에 제목 정보 전달</span><span class="sxs-lookup"><span data-stu-id="6b216-200">Passing Title Information to the Layout Page</span></span>

<span data-ttu-id="6b216-201"> *\_Layout.cshtml* 만든 페이지에는 `<title>` "내 동영상 사이트"로 설정 된 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-201">The *\_Layout.cshtml* page that you created has a `<title>` element that's set to "My Movie Site".</span></span> <span data-ttu-id="6b216-202">대부분의 브라우저 탭에 텍스트와이 요소의 내용 표시:</span><span class="sxs-lookup"><span data-stu-id="6b216-202">Most browsers display the content of this element as the text on a tab:</span></span>

![페이지의 &lt;제목&gt; 브라우저 탭에 표시 된 요소](layouts/_static/image8.png)

<span data-ttu-id="6b216-204">이 제목 정보는 제네릭입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-204">This title information is generic.</span></span> <span data-ttu-id="6b216-205">제목 텍스트를 현재 페이지에 더 구체적인 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-205">Suppose that you want the title text to be more specific to the current page.</span></span> <span data-ttu-id="6b216-206">(제목 텍스트는 검색 엔진에서 확인 하는 데도 페이지에 표시 되는 것입니다.) 와 같은 콘텐츠 페이지에서 정보를 전달할 수 *Movies.cshtml* 또는 *AddMovie.cshtml* 레이아웃 페이지 및 사용 하 여 해당 정보를 레이아웃 페이지를 사용자 지정 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-206">(The title text is also used by search engines to determine what your page is about.) You can pass information from a content page like *Movies.cshtml* or *AddMovie.cshtml* to the layout page, and then use that information to customize what the layout page renders.</span></span>

<span data-ttu-id="6b216-207">열기는 *Movies.cshtml* 페이지를 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-207">Open the *Movies.cshtml* page again.</span></span> <span data-ttu-id="6b216-208">맨 위에 있는 코드에서 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-208">In the code at the top, add the following line:</span></span>

[!code-csharp[Main](layouts/samples/sample8.cs)]

<span data-ttu-id="6b216-209">`Page` 개체는 모두에서 사용할 수 있는 *.cshtml* 페이지 이며이 작업을 위해 즉 페이지와 레이아웃 간에 정보를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-209">The `Page` object is available on all *.cshtml* pages and is for this purpose, namely to share information between a page and its layout.</span></span>

<span data-ttu-id="6b216-210">열기는<em>\_Layout.cshtml</em> 페이지.</span><span class="sxs-lookup"><span data-stu-id="6b216-210">Open the<em>\_Layout.cshtml</em> page.</span></span> <span data-ttu-id="6b216-211">변경 된 `<title>` 요소를이 태그 같이 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-211">Change the `<title>` element so that it looks like this markup:</span></span>

[!code-html[Main](layouts/samples/sample9.html)]

<span data-ttu-id="6b216-212">이 코드에는 렌더링 된 `Page.Title` 속성 페이지에서 해당 위치에서 바로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-212">This code renders whatever is in the `Page.Title` property right at that location in the page.</span></span>

<span data-ttu-id="6b216-213">실행 된 *Movies.cshtml* 페이지.</span><span class="sxs-lookup"><span data-stu-id="6b216-213">Run the *Movies.cshtml* page.</span></span> <span data-ttu-id="6b216-214">이 현재 브라우저 탭이 표시의 값으로 전달 된 `Page.Title`:</span><span class="sxs-lookup"><span data-stu-id="6b216-214">This time the browser tab shows what you passed as the value of `Page.Title`:</span></span>

![동적으로 만든 제목이 표시 브라우저 탭](layouts/_static/image9.png)

<span data-ttu-id="6b216-216">원하는 경우 브라우저에서 페이지 소스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-216">If you want, view the page source in the browser.</span></span> <span data-ttu-id="6b216-217">확인할 수 있습니다는 `<title>` 요소가로 렌더링 `<title>List Movies</title>`합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-217">You can see that the `<title>` element is rendered as `<title>List Movies</title>`.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="6b216-218">**Page 개체**</span><span class="sxs-lookup"><span data-stu-id="6b216-218">**The Page Object**</span></span>
> 
> <span data-ttu-id="6b216-219">유용한 특징 중 `Page` 동적 개체는-는 `Title` 속성은 고정 또는 예약 된 이름이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-219">A useful feature of `Page` is that it's a dynamic object — the `Title` property is not a fixed or reserved name.</span></span> <span data-ttu-id="6b216-220">사용할 수 있습니다 *모든* 의 값에 대 한 이름는 `Page` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-220">You can use *any* name for a value of the `Page` object.</span></span> <span data-ttu-id="6b216-221">예를 들어 수를 쉽게 전달한 제목을 라는 속성을 사용 하 여 `Page.CurrentName` 또는 `Page.MyPage`합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-221">For example, you could as easily have passed the title by using a property named `Page.CurrentName` or `Page.MyPage`.</span></span> <span data-ttu-id="6b216-222">유일한 제한 사항은 이름 속성 이름을 지정할 수에 대 한 일반 규칙을 준수 해야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-222">The only restriction is that the name has to follow the normal rules for what properties can be named.</span></span> <span data-ttu-id="6b216-223">(예를 들어 이름에는 공백입니다.)</span><span class="sxs-lookup"><span data-stu-id="6b216-223">(For example, the name can't contain a space.)</span></span>
> 
> <span data-ttu-id="6b216-224">사용 하 여 원하는 수의 값을 전달할 수 있습니다는 `Page` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-224">You can pass any number of values by using the `Page` object.</span></span> <span data-ttu-id="6b216-225">레이아웃 페이지에 동영상 정보를 전달 하려는 경우 다음과 같이 사용 하 여 값을 전달할 수 있습니다 `Page.MovieTitle` 및 `Page.Genre` 및 `Page.MovieYear`합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-225">If you wanted to pass movie information to the layout page, you could pass values by using something like `Page.MovieTitle` and `Page.Genre` and `Page.MovieYear`.</span></span> <span data-ttu-id="6b216-226">(또는 다른 이름 정보를 저장할 발명에.) 유일한 요구 사항은-는 아마도 분명 한 것은-콘텐츠 페이지와 페이지 레이아웃 페이지의 동일한 이름을 사용할 수 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-226">(Or any other names that you invented to store the information.) The only requirement — which is probably obvious — is that you have to use the same names in the content page and the layout page.</span></span>
> 
> <span data-ttu-id="6b216-227">사용 하 여 전달 되는 정보는 `Page` 개체를 레이아웃 페이지에 표시할 텍스트만으로 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-227">The information you pass by using the `Page` object isn't limited to just text to display on the layout page.</span></span> <span data-ttu-id="6b216-228">레이아웃 페이지에는 값을 전달할 수 있습니다 및 레이아웃 페이지의 코드 페이지의 부분을 표시 하려면 여부를 결정할 값을 사용할 수 다음 어떤 *.css* 파일을 사용 하려면 등에입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-228">You can pass a value to the layout page, and then code in the layout page can use the value to decide whether to display a section of the page, what *.css* file to use, and so on.</span></span> <span data-ttu-id="6b216-229">에 전달 하는 값은 `Page` 개체는 다른 모든 값과 같은 코드에서 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-229">The values you pass in the `Page` object are like any other values that you use in code.</span></span> <span data-ttu-id="6b216-230">값 콘텐츠 페이지에서 시작 하 고 페이지 레이아웃 페이지에 전달 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-230">It's just that the values originate in the content page and are passed to the layout page.</span></span>


<span data-ttu-id="6b216-231">열기는 *AddMovie.cshtml* 페이지 제목을 제공 하는 코드의 위쪽에 선을 추가 하 고는 *AddMovie.cshtml* 페이지:</span><span class="sxs-lookup"><span data-stu-id="6b216-231">Open the *AddMovie.cshtml* page and add a line to the top of the code that provides a title for the *AddMovie.cshtml* page:</span></span>

[!code-csharp[Main](layouts/samples/sample10.cs)]

<span data-ttu-id="6b216-232">실행 된 *AddMovie.cshtml* 페이지.</span><span class="sxs-lookup"><span data-stu-id="6b216-232">Run the *AddMovie.cshtml* page.</span></span> <span data-ttu-id="6b216-233">새 제목을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-233">You see the new title there:</span></span>

![동적으로 만든 추가 동영상 제목이 표시 브라우저 탭](layouts/_static/image10.png)

## <a name="updating-the-remaining-pages-to-use-the-layout"></a><span data-ttu-id="6b216-235">레이아웃을 사용 하 여 나머지 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-235">Updating the Remaining Pages to Use the Layout</span></span>

<span data-ttu-id="6b216-236">이제 새 레이아웃을 사용할 수 있도록 사이트의 나머지 페이지를 마칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-236">Now you can finish the remaining pages in your site so that they use the new layout.</span></span> <span data-ttu-id="6b216-237">열기 *EditMovie.cshtml* 및 *DeleteMovie.cshtml* 에 설정 하 고 각각에 동일한 변경 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-237">Open *EditMovie.cshtml* and *DeleteMovie.cshtml* in turn and make the same changes in each.</span></span>

<span data-ttu-id="6b216-238">레이아웃 페이지에 연결 하는 코드 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-238">Add the line of code that links to the layout page:</span></span>

[!code-csharp[Main](layouts/samples/sample11.cs)]

<span data-ttu-id="6b216-239">페이지의 제목을 설정 하는 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-239">Add a line to set the title of the page:</span></span>

[!code-csharp[Main](layouts/samples/sample12.cs)]

<span data-ttu-id="6b216-240">또는</span><span class="sxs-lookup"><span data-stu-id="6b216-240">or:</span></span>

[!code-csharp[Main](layouts/samples/sample13.cs)]

<span data-ttu-id="6b216-241">불필요 한 모든 HTML 태그 제거-기본적으로, 내부에 있는 비트만 둡니다는 `<body>` 요소 (및 맨 위에 있는 코드 블록).</span><span class="sxs-lookup"><span data-stu-id="6b216-241">Remove all the extraneous HTML markup — basically, leave only the bits that are inside the `<body>` element (plus the code block at the top).</span></span>

<span data-ttu-id="6b216-242">변경 된 `<h1>` 요소는 `<h2>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-242">Change the `<h1>` element to be an `<h2>` element.</span></span>

<span data-ttu-id="6b216-243">이러한 변경 내용을 수행 했으면, 테스트 실행 하 고 제대로 표시 된 대로, 그리고 제목이 올바른지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-243">When you've made these changes, test each and make sure that it's displaying properly and that the title is correct.</span></span>

## <a name="parting-thoughts-about-layout-pages"></a><span data-ttu-id="6b216-244">레이아웃 페이지에 대 한 분할 생각</span><span class="sxs-lookup"><span data-stu-id="6b216-244">Parting Thoughts About Layout Pages</span></span>

<span data-ttu-id="6b216-245">이 자습서에서 만든는  *\_Layout.cshtml* 페이지를 사용 하는 `RenderBody` 메서드를 다른 페이지의에서 콘텐츠를 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-245">In this tutorial you created a *\_Layout.cshtml* page and used the `RenderBody` method to merge content from another page.</span></span> <span data-ttu-id="6b216-246">웹 페이지의 레이아웃을 사용 하기 위한 기본 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-246">That's the basic pattern for using layouts in Web Pages.</span></span>

<span data-ttu-id="6b216-247">레이아웃 페이지는 여기 다룰 하지 않은 추가 기능도 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-247">Layout pages have additional features that we didn't cover here.</span></span> <span data-ttu-id="6b216-248">예를 들어, 레이아웃 페이지를 중첩할 수 있습니다-한 레이아웃 페이지를 참조할 수 다른 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-248">For example, you can nest layout pages — one layout page can in turn reference another.</span></span> <span data-ttu-id="6b216-249">중첩 된 레이아웃 다양 한 레이아웃을 필요로 하는 사이트의 하위 섹션으로 작업 하는 경우에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-249">Nested layouts can be useful if you're working with subsections of a site that require different layouts.</span></span> <span data-ttu-id="6b216-250">추가 메서드를 사용할 수도 있습니다 (예를 들어 `RenderSection`) 명명 된 레이아웃 페이지의 섹션을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-250">You can also use additional methods (for example, `RenderSection`) to set up named sections in the layout page.</span></span>

<span data-ttu-id="6b216-251">레이아웃 페이지의 조합 및 *.css* 파일은 강력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-251">The combination of layout pages and *.css* files is powerful.</span></span> <span data-ttu-id="6b216-252">다음 자습서 시리즈의 하겠지만 WebMatrix에서 만들 수 있습니다에 기반 하는 사이트는 *템플릿*, 있는 사이트를 제공 하는 미리 작성 된 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-252">As you'll see in the next tutorial series, in WebMatrix you can create a site based on a *template*, which gives you a site that has prebuilt functionality in it.</span></span> <span data-ttu-id="6b216-253">서식 파일의 레이아웃 페이지 및 CSS를 보기 좋게 있고 메뉴와 같은 기능 사이트를 만들 적절 하 게 사용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-253">The templates make good use of layout pages and CSS to create sites that look great and that have features like menus.</span></span> <span data-ttu-id="6b216-254">레이아웃 페이지 및 CSS를 사용 하는 기능을 보여 주는 하는 템플릿을 기반으로 하는 사이트에서 홈 페이지의 스크린 샷을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-254">Here's a screenshot of the home page from a site based on a template, showing features that use layout pages and CSS:</span></span>

![헤더, 탐색 영역, 콘텐츠 영역, 선택적 섹션 및 로그인 링크를 표시 하는 WebMatrix 사이트 템플릿으로 만든 레이아웃](layouts/_static/image11.png)

## <a name="complete-listing-for-movie-page-updated-to-use-a-layout-page"></a><span data-ttu-id="6b216-256">동영상 페이지 (페이지 레이아웃을 사용 하도록 업데이트)에 대 한 전체 목록을 보려면</span><span class="sxs-lookup"><span data-stu-id="6b216-256">Complete Listing for Movie Page (Updated to Use a Layout Page)</span></span>

[!code-cshtml[Main](layouts/samples/sample14.cshtml)]

## <a name="complete-page-listing-for-add-movie-page-updated-for-layout"></a><span data-ttu-id="6b216-257">완료 페이지에 대 한 목록 추가 (레이아웃에 대 한 업데이트) 동영상 페이지</span><span class="sxs-lookup"><span data-stu-id="6b216-257">Complete Page Listing for Add Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample15.cshtml)]

## <a name="complete-page-listing-for-delete-movie-page-updated-for-layout"></a><span data-ttu-id="6b216-258">전체 삭제 동영상 페이지 (레이아웃에 대 한 업데이트)에 대 한 목록 페이지</span><span class="sxs-lookup"><span data-stu-id="6b216-258">Complete Page Listing for Delete Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample16.cshtml)]

## <a name="complete-page-listing-for-edit-movie-page-updated-for-layout"></a><span data-ttu-id="6b216-259">전체 편집 동영상 페이지 (레이아웃에 대 한 업데이트)에 대 한 목록 페이지</span><span class="sxs-lookup"><span data-stu-id="6b216-259">Complete Page Listing for Edit Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample17.cshtml)]

## <a name="coming-up-next"></a><span data-ttu-id="6b216-260">다음에 나오는</span><span class="sxs-lookup"><span data-stu-id="6b216-260">Coming Up Next</span></span>

<span data-ttu-id="6b216-261">다음 자습서에서는 사람이 볼 수 있도록 사이트를 인터넷에 게시 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-261">In the next tutorial, you'll learn how to publish your site to the Internet so everyone can see it.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6b216-262">추가 자료</span><span class="sxs-lookup"><span data-stu-id="6b216-262">Additional Resources</span></span>

- <span data-ttu-id="6b216-263">[일관성 확인을 만드는](https://go.microsoft.com/fwlink/?LinkID=202891) -레이아웃 작업에 더 자세히 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-263">[Creating a Consistent Look](https://go.microsoft.com/fwlink/?LinkID=202891) — An article that provides some more detail on working with layouts.</span></span> <span data-ttu-id="6b216-264">또한를 표시 하거나 숨기는 콘텐츠 일부가 레이아웃 페이지에는 값을 전달 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-264">It also describes how to pass a value to a layout page that shows or hides some of the content.</span></span>
- <span data-ttu-id="6b216-265">[중첩 된 Razor 사용한 레이아웃 페이지](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor) -Mike Brind 블로그 레이아웃 페이지를 중첩 하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="6b216-265">[Nested Layout Pages with Razor](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor) — Mike Brind blogs an example of how to nest layout pages.</span></span> <span data-ttu-id="6b216-266">(페이지의 다운로드 포함).</span><span class="sxs-lookup"><span data-stu-id="6b216-266">(Includes a download of the pages.)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6b216-267">[이전](deleting-data.md)
> [다음](publishing.md)</span><span class="sxs-lookup"><span data-stu-id="6b216-267">[Previous](deleting-data.md)
[Next](publishing.md)</span></span>
