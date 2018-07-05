---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
title: Creating Page Layouts with 보기 마스터 페이지 (C#) | Microsoft Docs
author: microsoft
description: 이 자습서에서는 보기 마스터 페이지를 활용 하 여 응용 프로그램에서 여러 페이지에 대 한 일반적인 페이지 레이아웃을 만드는 방법을 알아봅니다. 사용할 수는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/16/2008
ms.topic: article
ms.assetid: dff54fcb-68b1-4488-89a2-ca97532d6a4c
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: c23f397ad9dd5c26278d654ef2aec66d201166a3
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37387850"
---
<a name="creating-page-layouts-with-view-master-pages-c"></a><span data-ttu-id="c70e8-104">보기 마스터 페이지 (C#)를 사용 하 여 페이지 레이아웃 만들기</span><span class="sxs-lookup"><span data-stu-id="c70e8-104">Creating Page Layouts with View Master Pages (C#)</span></span>
====================
<span data-ttu-id="c70e8-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c70e8-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="c70e8-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="c70e8-106">Download PDF</span></span>](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_CS.pdf)

> <span data-ttu-id="c70e8-107">이 자습서에서는 보기 마스터 페이지를 활용 하 여 응용 프로그램에서 여러 페이지에 대 한 일반적인 페이지 레이아웃을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-107">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="c70e8-108">열이 두 페이지 레이아웃을 정의 하 고 모든 웹 응용 프로그램의 페이지에 대 한 2 열 레이아웃을 사용 예를 들어, 마스터 페이지 보기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-108">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>


## <a name="creating-page-layouts-with-view-master-pages"></a><span data-ttu-id="c70e8-109">보기 마스터 페이지를 사용 하 여 페이지 레이아웃 만들기</span><span class="sxs-lookup"><span data-stu-id="c70e8-109">Creating Page Layouts with View Master Pages</span></span>

<span data-ttu-id="c70e8-110">이 자습서에서는 보기 마스터 페이지를 활용 하 여 응용 프로그램에서 여러 페이지에 대 한 일반적인 페이지 레이아웃을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-110">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="c70e8-111">열이 두 페이지 레이아웃을 정의 하 고 모든 웹 응용 프로그램의 페이지에 대 한 2 열 레이아웃을 사용 예를 들어, 마스터 페이지 보기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-111">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>

<span data-ttu-id="c70e8-112">있습니다 수 활용할 보기의 콘텐츠를 공유 하려면 일반적인 응용 프로그램에서 여러 페이지에 걸쳐 마스터 페이지.</span><span class="sxs-lookup"><span data-stu-id="c70e8-112">You also can take advantage of view master pages to share common content across multiple pages in your application.</span></span> <span data-ttu-id="c70e8-113">예를 들어, 웹 사이트 로고, 탐색 링크와 배너 광고 보기 마스터 페이지에 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-113">For example, you can place your website logo, navigation links, and banner advertisements in a view master page.</span></span> <span data-ttu-id="c70e8-114">이런 방식으로 모든 페이지에서 응용 프로그램은 자동으로이 콘텐츠를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-114">That way, every page in your application would display this content automatically.</span></span>

<span data-ttu-id="c70e8-115">이 자습서에서는 마스터 페이지에 따라 새 뷰 콘텐츠 페이지를 만들고 새 보기 마스터 페이지를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-115">In this tutorial, you learn how to create a new view master page and create a new view content page based on the master page.</span></span>

### <a name="creating-a-view-master-page"></a><span data-ttu-id="c70e8-116">보기 마스터 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="c70e8-116">Creating a View Master Page</span></span>

<span data-ttu-id="c70e8-117">2 열 레이아웃을 정의 하는 보기 마스터 페이지를 만들어 시작 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-117">Let's start by creating a view master page that defines a two-column layout.</span></span> <span data-ttu-id="c70e8-118">추가한 새 보기 마스터 페이지를 MVC 프로젝트 Views\Shared 폴더를 마우스 오른쪽 단추로 클릭 하 여 메뉴 옵션을 선택 하면 **추가, 새 항목**를 선택 하 고는 **MVC 보기 마스터 페이지** 템플릿 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="c70e8-118">You add a new view master page to an MVC project by right-clicking the Views\Shared folder, selecting the menu option **Add, New Item**, and selecting the **MVC View Master Page** template (see Figure 1).</span></span>


<span data-ttu-id="c70e8-119">[![보기 마스터 페이지 추가](creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c70e8-119">[![Adding a view master page](creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)</span></span>

<span data-ttu-id="c70e8-120">**그림 01**: 뷰 마스터 페이지 추가 ([큰 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="c70e8-120">**Figure 01**: Adding a view master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image3.png))</span></span>


<span data-ttu-id="c70e8-121">응용 프로그램에서 둘 이상의 뷰 마스터 페이지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-121">You can create more than one view master page in an application.</span></span> <span data-ttu-id="c70e8-122">각 보기 마스터 페이지에는 다양 한 페이지 레이아웃을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-122">Each view master page can define a different page layout.</span></span> <span data-ttu-id="c70e8-123">예를 들어 좋습니다 2 열 레이아웃을 특정 페이지 및 기타 페이지 3 열 레이아웃 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-123">For example, you might want certain pages to have a two-column layout and other pages to have a three-column layout.</span></span>

<span data-ttu-id="c70e8-124">보기 마스터 페이지와 매우 비슷하며 표준 ASP.NET MVC 보기.</span><span class="sxs-lookup"><span data-stu-id="c70e8-124">A view master page looks very much like a standard ASP.NET MVC view.</span></span> <span data-ttu-id="c70e8-125">그러나 기본 보기와 달리 뷰 마스터 페이지를 하나 이상 포함 `<asp:ContentPlaceHolder>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-125">However, unlike a normal view, a view master page contains one or more `<asp:ContentPlaceHolder>` tags.</span></span> <span data-ttu-id="c70e8-126">`<contentplaceholder>` 태그는 개별 콘텐츠 페이지에서 재정의 될 수 있는 마스터 페이지의 영역을 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-126">The `<contentplaceholder>` tags are used to mark the areas of the master page that can be overridden in an individual content page.</span></span>

<span data-ttu-id="c70e8-127">예를 들어, 보기 마스터 페이지 목록 1에서 2 열 레이아웃을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-127">For example, the view master page in Listing 1 defines a two-column layout.</span></span> <span data-ttu-id="c70e8-128">포함 된 두 `<contentplaceholder>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-128">It contains two `<contentplaceholder>` tags.</span></span> <span data-ttu-id="c70e8-129">하나의 `<ContentPlaceHolder>` 각 열에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-129">One `<ContentPlaceHolder>` for each column.</span></span>

<span data-ttu-id="c70e8-130">**목록 1 – `Views\Shared\Site.master`**</span><span class="sxs-lookup"><span data-stu-id="c70e8-130">**Listing 1 – `Views\Shared\Site.master`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample1.aspx)]

<span data-ttu-id="c70e8-131">목록 1에서 마스터 페이지에는 두 개의 뷰의 본문 `<div>` 두 열에 해당 하는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-131">The body of the view master page in Listing 1 contains two `<div>` tags that correspond to the two columns.</span></span> <span data-ttu-id="c70e8-132">Cascading Style Sheet 열 클래스가 둘 다에 적용 된 `<div>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-132">The Cascading Style Sheet column class is applied to both `<div>` tags.</span></span> <span data-ttu-id="c70e8-133">이 클래스는 마스터 페이지의 맨 위에 선언 스타일 시트에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-133">This class is defined in the style sheet declared at the top of the master page.</span></span> <span data-ttu-id="c70e8-134">디자인 뷰로 전환 하 여 보기 마스터 페이지를 렌더링할 방식을 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-134">You can preview how the view master page will be rendered by switching to Design view.</span></span> <span data-ttu-id="c70e8-135">소스 코드 편집기의 왼쪽 아래에 있는 디자인 탭을 클릭 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="c70e8-135">Click the Design tab at the bottom-left of the source code editor (see Figure 2).</span></span>


<span data-ttu-id="c70e8-136">[![마스터 페이지 디자이너의 미리 보기](creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="c70e8-136">[![Previewing a master page in the designer](creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)</span></span>

<span data-ttu-id="c70e8-137">**그림 02**: 마스터 페이지 디자이너의 미리 보기 ([큰 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="c70e8-137">**Figure 02**: Previewing a master page in the designer ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image6.png))</span></span>


### <a name="creating-a-view-content-page"></a><span data-ttu-id="c70e8-138">뷰 콘텐츠 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="c70e8-138">Creating a View Content Page</span></span>

<span data-ttu-id="c70e8-139">보기 마스터 페이지를 만든 후에 하나 이상의 뷰 콘텐츠 페이지 보기 마스터 페이지를 기반으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-139">After you create a view master page, you can create one or more view content pages based on the view master page.</span></span> <span data-ttu-id="c70e8-140">예를 들어 Views\Home 폴더를 마우스 오른쪽 단추로 클릭 하 여 홈 컨트롤러에 대 한 인덱스 뷰 콘텐츠 페이지를 만들 수 있습니다 선택 **추가, 새 항목**선택 하는 **MVC 뷰 콘텐츠 페이지** 입력 템플릿 이름을 Index.aspx를 클릭 하 고는 **추가** 단추 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="c70e8-140">For example, you can create an Index view content page for the Home controller by right-clicking the Views\Home folder, selecting **Add, New Item**, selecting the **MVC View Content Page** template, entering the name Index.aspx, and clicking the **Add** button (see Figure 3).</span></span>


<span data-ttu-id="c70e8-141">[![뷰 콘텐츠 페이지 추가](creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="c70e8-141">[![Adding a view content page](creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)</span></span>

<span data-ttu-id="c70e8-142">**그림 03**: 뷰 콘텐츠 페이지 추가 ([큰 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-cs/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="c70e8-142">**Figure 03**: Adding a view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image9.png))</span></span>


<span data-ttu-id="c70e8-143">추가 단추를 클릭 하면 새 대화 상자가 나타나는 뷰 콘텐츠 페이지와 연결할 보기 마스터 페이지를 선택할 수 있습니다 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="c70e8-143">After you click the Add button, a new dialog appears that enables you to select a view master page to associate with the view content page (see Figure 4).</span></span> <span data-ttu-id="c70e8-144">이전 섹션에서 만든 Site.master 뷰 마스터 페이지를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-144">You can navigate to the Site.master view master page that we created in the previous section.</span></span>


<span data-ttu-id="c70e8-145">[![마스터 페이지를 선택합니다.](creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="c70e8-145">[![Selecting a master page](creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)</span></span>

<span data-ttu-id="c70e8-146">**그림 04**: 마스터 페이지 선택 ([큰 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="c70e8-146">**Figure 04**: Selecting a master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image12.png))</span></span>


<span data-ttu-id="c70e8-147">Site.master 마스터 페이지에 따라 새 뷰 콘텐츠 페이지를 만든 후 2 목록에서 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-147">After you create a new view content page based on the Site.master master page, you get the file in Listing 2.</span></span>

<span data-ttu-id="c70e8-148">**2 – 나열 `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="c70e8-148">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample2.aspx)]

<span data-ttu-id="c70e8-149">이 뷰를 포함 하는 `<asp:Content>` 각각에 해당 하는 태그를 `<asp:ContentPlaceHolder>` 보기 마스터 페이지의 태그에에서.</span><span class="sxs-lookup"><span data-stu-id="c70e8-149">Notice that this view contains a `<asp:Content>` tag that corresponds to each of the `<asp:ContentPlaceHolder>` tags in the view master page.</span></span> <span data-ttu-id="c70e8-150">각 `<asp:Content>` 태그를 포함 하는 특정 가리키는 ContentPlaceHolderID 특성을 `<asp:ContentPlaceHolder>` 를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-150">Each `<asp:Content>` tag includes a ContentPlaceHolderID attribute that points to the particular `<asp:ContentPlaceHolder>` that it overrides.</span></span>

<span data-ttu-id="c70e8-151">또한 콘텐츠 목록 2에서 페이지 보기는 통지 일반와 HTML 닫는 태그의 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-151">Notice, furthermore, that the content view page in Listing 2 does not contain any of the normal opening and closing HTML tags.</span></span> <span data-ttu-id="c70e8-152">예를 들어 없습니다을 열고 닫는 `<html>` 또는 `<head>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-152">For example, it does not contain the opening and closing `<html>` or `<head>` tags.</span></span> <span data-ttu-id="c70e8-153">모든 표준 태그와 닫는 태그 보기 마스터 페이지에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-153">All of the normal opening and closing tags are contained in the view master page.</span></span>

<span data-ttu-id="c70e8-154">뷰 콘텐츠 페이지에 표시 하려는 내용을 안에 있어야를 `<asp:Content>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-154">Any content that you want to display in a view content page must be placed within a `<asp:Content>` tag.</span></span> <span data-ttu-id="c70e8-155">HTML 또는 기타 콘텐츠 이러한 태그 외부에 배치 하면 다음 오류가 표시 됩니다는 페이지를 표시 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-155">If you place any HTML or other content outside of these tags, then you will get an error when you attempt to view the page.</span></span>

<span data-ttu-id="c70e8-156">재정의할 필요가 모든 `<asp:ContentPlaceHolder>` 뷰 콘텐츠 페이지의 마스터 페이지의 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-156">You don't need to override every `<asp:ContentPlaceHolder>` tag from a master page in a content view page.</span></span> <span data-ttu-id="c70e8-157">재정의 해야 하는 `<asp:ContentPlaceHolder>` 특정 콘텐츠를 사용 하 여 태그를 바꿀 때 태그를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-157">You only need to override a `<asp:ContentPlaceHolder>` tag when you want to replace the tag with particular content.</span></span>

<span data-ttu-id="c70e8-158">예를 들어 목록 3에서 수정 된 인덱스 보기에는 두 개의 `<asp:Content>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-158">For example, the modified Index view in Listing 3 contains only two `<asp:Content>` tags.</span></span> <span data-ttu-id="c70e8-159">각는 `<asp:Content>` 태그 일부 텍스트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-159">Each of the `<asp:Content>` tags includes some text.</span></span>

<span data-ttu-id="c70e8-160">**3 – 나열 `Views\Home\Index.aspx (modified)`**</span><span class="sxs-lookup"><span data-stu-id="c70e8-160">**Listing 3 – `Views\Home\Index.aspx (modified)`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample3.aspx)]

<span data-ttu-id="c70e8-161">보기 3의 보기를 요청 하면 그림 5에서 페이지를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-161">When the view in Listing 3 is requested, it renders the page in Figure 5.</span></span> <span data-ttu-id="c70e8-162">뷰를 두 개의 열을 사용 하 여 페이지를 렌더링 하는 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-162">Notice that the view renders a page with two columns.</span></span> <span data-ttu-id="c70e8-163">또한: 뷰 콘텐츠 페이지에서 콘텐츠 보기 마스터 페이지의 콘텐츠와 병합 되는 알 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="c70e8-163">Notice, furthermore, that the content from the view content page is merged with the content from the view master page</span></span>


<span data-ttu-id="c70e8-164">[![인덱스 뷰 콘텐츠 페이지](creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="c70e8-164">[![The Index view content page](creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)</span></span>

<span data-ttu-id="c70e8-165">**그림 05**: The 인덱스 뷰 콘텐츠 페이지 ([큰 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-cs/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="c70e8-165">**Figure 05**: The Index view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image15.png))</span></span>


### <a name="modifying-view-master-page-content"></a><span data-ttu-id="c70e8-166">보기 마스터 페이지 콘텐츠를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-166">Modifying View Master Page Content</span></span>

<span data-ttu-id="c70e8-167">보기 마스터 페이지를 사용 하는 경우에 즉시 거의 발생할 수 있는 한 가지 문제는 서로 다른 뷰 콘텐츠 페이지를 요청 하면 마스터 페이지 콘텐츠 보기를 수정 하는 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-167">One issue that you encounter almost immediately when working with view master pages is the problem of modifying view master page content when different view content pages are requested.</span></span> <span data-ttu-id="c70e8-168">예를 들어, 고유한 제목이 할 웹 응용 프로그램에서 각 페이지를 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-168">For example, you want each page in your web application to have a unique title.</span></span> <span data-ttu-id="c70e8-169">그러나 제목 뷰 콘텐츠 페이지 아니라 보기 마스터 페이지에 선언 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-169">However, the title is declared in the view master page and not in the view content page.</span></span> <span data-ttu-id="c70e8-170">따라서 수행할 사용자 지정 방법 각 뷰 콘텐츠 페이지에 대 한 페이지 제목을?</span><span class="sxs-lookup"><span data-stu-id="c70e8-170">So, how do you customize the page title for each view content page?</span></span>

<span data-ttu-id="c70e8-171">뷰 콘텐츠 페이지에 의해 표시 되는 제목 수정할 수 있는 두 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-171">There are two ways that you can modify the title displayed by a view content page.</span></span> <span data-ttu-id="c70e8-172">먼저 title 특성에 페이지 제목을 지정할 수 있습니다는 `<%@ page %>` 지시문 뷰 콘텐츠 페이지의 맨 위에 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-172">First, you can assign a page title to the title attribute of the `<%@ page %>` directive declared at the top of a view content page.</span></span> <span data-ttu-id="c70e8-173">예를 들어 인덱스 뷰에 페이지 제목을 "슈퍼 뛰어난 웹 사이트"를 할당 하려는 경우 인덱스 뷰의 맨 위에 있는 다음 지시문을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-173">For example, if you want to assign the page title "Super Great Website" to the Index view, then you can include the following directive at the top of the Index view:</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample4.aspx)]

<span data-ttu-id="c70e8-174">인덱스 보기 브라우저에 렌더링 되 면 원하는 제목 브라우저 제목 표시줄에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-174">When the Index view is rendered to the browser, the desired title appears in the browser title bar:</span></span>


<span data-ttu-id="c70e8-175">[![브라우저 제목 표시줄](creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="c70e8-175">[![Browser title bar](creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)</span></span>


<span data-ttu-id="c70e8-176">마스터 뷰 페이지를 작동 하려면 title 특성에 대 한 순서로 충족 해야 하는 중요 한 요구 사항 중 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-176">There is one important requirement that a master view page must satisfy in order for the title attribute to work.</span></span> <span data-ttu-id="c70e8-177">보기 마스터 페이지를 포함 해야 합니다는 `<head runat="server">` 태그는 보통 대신 `<head>` 헤더에 대 한 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-177">The view master page must contain a `<head runat="server">` tag instead of a normal `<head>` tag for its header.</span></span> <span data-ttu-id="c70e8-178">경우는 `<head>` 태그에는 runat = "server" 특성이 제목이 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-178">If the `<head>` tag does not include the runat="server" attribute then the title won't appear.</span></span> <span data-ttu-id="c70e8-179">마스터 페이지에 필요한 기본 보기 `<head runat="server">` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-179">The default view master page includes the required `<head runat="server">` tag.</span></span>

<span data-ttu-id="c70e8-180">개별 뷰 콘텐츠 페이지에서 마스터 페이지 콘텐츠를 수정 하는 다른 방법은을 수정 하려는 영역을 래핑하는 것을 `<asp:ContentPlaceHolder>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-180">An alternative approach to modifying master page content from an individual view content page is to wrap the region that you want to modify in a `<asp:ContentPlaceHolder>` tag.</span></span> <span data-ttu-id="c70e8-181">예를 들어, 제목, 뿐만 아니라 마스터 뷰 페이지에서 렌더링 메타 태그를 변경 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-181">For example, imagine that you want to change not only the title, but also the meta tags, rendered by a master view page.</span></span> <span data-ttu-id="c70e8-182">마스터 뷰 페이지 목록 4에는 `<asp:ContentPlaceHolder>` 태그 내에서 해당 `<head>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-182">The master view page in Listing 4 contains a `<asp:ContentPlaceHolder>` tag within its `<head>` tag.</span></span>

<span data-ttu-id="c70e8-183">**4-목록 `Views\Shared\Site2.master`**</span><span class="sxs-lookup"><span data-stu-id="c70e8-183">**Listing 4 – `Views\Shared\Site2.master`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample5.aspx)]

<span data-ttu-id="c70e8-184">에 `<asp:ContentPlaceHolder>` 태그 목록 4에서 기본 콘텐츠를 포함: 기본 제목과 기본 메타 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-184">Notice that the `<asp:ContentPlaceHolder>` tag in Listing 4 includes default content: a default title and default meta tags.</span></span> <span data-ttu-id="c70e8-185">이 재정의 하지 않으면 `<asp:ContentPlaceHolder>` 태그 개별 뷰 콘텐츠 페이지를 기본 콘텐츠가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-185">If you don't override this `<asp:ContentPlaceHolder>` tag in an individual view content page, then the default content will be displayed.</span></span>

<span data-ttu-id="c70e8-186">콘텐츠 보기 페이지 목록 5에서 재정의 된 `<asp:ContentPlaceHolder>` 사용자 지정 제목 및 사용자 지정 메타 태그를 표시 하기 위해 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-186">The content view page in Listing 5 overrides the `<asp:ContentPlaceHolder>` tag in order to display a custom title and custom meta tags.</span></span>

<span data-ttu-id="c70e8-187">**5-목록 `Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="c70e8-187">**Listing 5 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample6.aspx)]

### <a name="summary"></a><span data-ttu-id="c70e8-188">요약</span><span class="sxs-lookup"><span data-stu-id="c70e8-188">Summary</span></span>

<span data-ttu-id="c70e8-189">이 자습서는 마스터 페이지 및 콘텐츠 페이지를 볼 기본적인 소개를 사용 하 여 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-189">This tutorial provided you with a basic introduction to view master pages and view content pages.</span></span> <span data-ttu-id="c70e8-190">새 보기 마스터 페이지를 만들고 그에 따라 뷰 콘텐츠 페이지를 만들 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-190">You learned how to create new view master pages and create view content pages based on them.</span></span> <span data-ttu-id="c70e8-191">또한 특정 뷰 콘텐츠 페이지 로부터 마스터 뷰 페이지의 콘텐츠를 수정 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="c70e8-191">We also examined how you can modify the content of a view master page from a particular view content page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c70e8-192">[이전](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
> [다음](passing-data-to-view-master-pages-cs.md)</span><span class="sxs-lookup"><span data-stu-id="c70e8-192">[Previous](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
[Next](passing-data-to-view-master-pages-cs.md)</span></span>
