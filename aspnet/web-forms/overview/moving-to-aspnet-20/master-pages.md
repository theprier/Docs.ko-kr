---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: 마스터 페이지 | Microsoft Docs
author: microsoft
description: 성공적인 웹 사이트에 대 한 주요 구성 요소 중 하나에 일관 된 모양과 느낌입니다. ASP.NET에서 1.x 개발자는 일반적인 페이지 소형 복제 하기 위해 사용자 정의 컨트롤을 사용...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: f45dd9704f665244d2a48ec000326f6e98984e4f
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="master-pages"></a><span data-ttu-id="264c1-104">마스터 페이지</span><span class="sxs-lookup"><span data-stu-id="264c1-104">Master Pages</span></span>
====================
<span data-ttu-id="264c1-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="264c1-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="264c1-106">성공적인 웹 사이트에 대 한 주요 구성 요소 중 하나에 일관 된 모양과 느낌입니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-106">One of the key components to a successful Web site is a consistent look and feel.</span></span> <span data-ttu-id="264c1-107">ASP.NET에서 1.x 개발자는 웹 응용 프로그램에서 일반 페이지 요소를 복제 하기 위해 사용자 정의 컨트롤을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-107">In ASP.NET 1.x, developers used user controls to replicate common page elements across a Web application.</span></span> <span data-ttu-id="264c1-108">확실히 처리 가능한 여러 솔루션 사용 되 고 있지만, 사용자 정의 컨트롤을 사용 하 여 일부의 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-108">While that is certainly a workable solution, using user controls does have some drawbacks.</span></span> <span data-ttu-id="264c1-109">예를 들어, 사용자 정의 컨트롤의 위치는 변경 사이트 전체에서 여러 페이지에 대 한 변경이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-109">For example, a change in position of a user control requires a change to multiple pages across a site.</span></span> <span data-ttu-id="264c1-110">사용자 정의 컨트롤은 또한 페이지에 삽입 되 고 후 디자인 보기에서 렌더링 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-110">User controls are also not rendered in Design view after being inserted on a page.</span></span>


<span data-ttu-id="264c1-111">성공적인 웹 사이트에 대 한 주요 구성 요소 중 하나에 일관 된 모양과 느낌입니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-111">One of the key components to a successful Web site is a consistent look and feel.</span></span> <span data-ttu-id="264c1-112">ASP.NET에서 1.x 개발자는 웹 응용 프로그램에서 일반 페이지 요소를 복제 하기 위해 사용자 정의 컨트롤을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-112">In ASP.NET 1.x, developers used user controls to replicate common page elements across a Web application.</span></span> <span data-ttu-id="264c1-113">확실히 처리 가능한 여러 솔루션 사용 되 고 있지만, 사용자 정의 컨트롤을 사용 하 여 일부의 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-113">While that is certainly a workable solution, using user controls does have some drawbacks.</span></span> <span data-ttu-id="264c1-114">예를 들어, 사용자 정의 컨트롤의 위치는 변경 사이트 전체에서 여러 페이지에 대 한 변경이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-114">For example, a change in position of a user control requires a change to multiple pages across a site.</span></span> <span data-ttu-id="264c1-115">사용자 정의 컨트롤은 또한 페이지에 삽입 되 고 후 디자인 보기에서 렌더링 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-115">User controls are also not rendered in Design view after being inserted on a page.</span></span>

<span data-ttu-id="264c1-116">ASP.NET 2.0 소개 마스터 페이지 일관 된 모양 및 느낌을 유지 관리 하는 방법으로 및 때 보시, 마스터 페이지 사용자 지정 컨트롤 메서드를 통해 훨씬 향상 된 기능을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-116">ASP.NET 2.0 introduces Master pages as a way of maintaining a consistent look and feel, and as you'll soon see, Master pages represent a significant improvement over the user control method.</span></span>

## <a name="why-master-pages"></a><span data-ttu-id="264c1-117">이유 마스터 페이지?</span><span class="sxs-lookup"><span data-stu-id="264c1-117">Why Master Pages?</span></span>

<span data-ttu-id="264c1-118">마스터 페이지가 ASP.NET 2.0에서 필요한 이유 할까요?</span><span class="sxs-lookup"><span data-stu-id="264c1-118">You may be wondering why master pages were needed in ASP.NET 2.0.</span></span> <span data-ttu-id="264c1-119">즉, 웹 사이트 개발자가 이미 사용 하는 사용자 정의 컨트롤 ASP.NET에서 1.x를 콘텐츠 영역 페이지 간에 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-119">After all, Web site developers are already using user controls in ASP.NET 1.x to share content areas between pages.</span></span> <span data-ttu-id="264c1-120">사용자 정의 컨트롤의 일반적인 레이아웃을 만들기 위한 작음 보다 최적의 솔루션은 이유는 실제로 몇 가지 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-120">There are actually several reasons why user controls are a less-than-optimal solution for creating a common layout.</span></span>

<span data-ttu-id="264c1-121">실제로 사용자 정의 컨트롤 페이지 레이아웃을 정의 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-121">User controls don't actually define page layout.</span></span> <span data-ttu-id="264c1-122">대신, 레이아웃 및 기능 페이지의 부분을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-122">Instead, they define the layout and functionality for a portion of a page.</span></span> <span data-ttu-id="264c1-123">사용자 제어 솔루션의 관리를 하기가 훨씬 더 어려워지므로 만들므로이 두 구분이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-123">The distinction between these two is important because it makes manageability of a user control solution much more difficult.</span></span> <span data-ttu-id="264c1-124">예를 들어 페이지에서 사용자 정의 컨트롤의 위치를 변경 하려는 경우 사용자 정의 컨트롤이 표시 되는 실제 페이지를 편집 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-124">For example, when you want to change the position of a user control on your page, you must edit the actual page on which the user control appears.</span></span> <span data-ttu-id="264c1-125">Thats 일부 페이지만 있지만 대규모 사이트에서 확장 되는 사이트 관리 밋 미세!</span><span class="sxs-lookup"><span data-stu-id="264c1-125">Thats fine if you have only a few pages, but in large sites, it quickly becomes a site management nightmare!</span></span>

<span data-ttu-id="264c1-126">사용자 정의 컨트롤을 사용 하 여 일반적인 레이아웃을 정의 하기 위한 또 다른 단점은 작성과 자체 ASP.NET의 아키텍처.</span><span class="sxs-lookup"><span data-stu-id="264c1-126">Another drawback of using user controls for defining a common layout is rooted in the architecture of ASP.NET itself.</span></span> <span data-ttu-id="264c1-127">사용자 정의 컨트롤의 모든 public 멤버를 변경 하는 경우 모든 사용자 정의 컨트롤을 사용 하는 페이지를 다시 컴파일할 수 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-127">If any public member of a user control is changed, it requires you to recompile all of the pages that use the user control.</span></span> <span data-ttu-id="264c1-128">차례로 ASP.NET 다시 JIT 컴파일하는 처음 때 페이지에 액세스 한 다음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-128">In turn, ASP.NET will then re-JIT your pages when they are first accessed.</span></span> <span data-ttu-id="264c1-129">이 다시 한 번, 확장 불가능 아키텍처 및 대규모 사이트에 대 한 사이트 관리 문제를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-129">This, once again, produces a non-scalable architecture and a site management problem for larger sites.</span></span>

<span data-ttu-id="264c1-130">이러한 문제 (및 더 많은) 둘 다 ASP.NET 2.0의 마스터 페이지로 주소가 지정 원활 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-130">Both of these problems (and many more) are nicely addressed by master pages in ASP.NET 2.0.</span></span>

## <a name="how-master-pages-work"></a><span data-ttu-id="264c1-131">마스터 페이지의 작동 방식</span><span class="sxs-lookup"><span data-stu-id="264c1-131">How Master Pages Work</span></span>

<span data-ttu-id="264c1-132">마스터 페이지는 다른 페이지에 대 한 템플릿을 같습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-132">A master page is analogous to a template for other pages.</span></span> <span data-ttu-id="264c1-133">페이지 요소 (예: 메뉴, 테두리, 등)에 다른 페이지 간에 공유 해야 하는 마스터 페이지에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-133">Page elements that should be shared among other pages (i.e. menus, borders, etc.) are added to the master page.</span></span> <span data-ttu-id="264c1-134">새 페이지는 사이트에 추가 되 면 마스터 페이지와 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-134">When new pages are added to the site, you can associate them with a master page.</span></span> <span data-ttu-id="264c1-135">마스터 페이지와 연결 된 페이지 라고는 **콘텐츠 페이지**합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-135">A page that is associated with a master page is called a **content page**.</span></span> <span data-ttu-id="264c1-136">기본적으로 콘텐츠 페이지의 마스터 페이지에서 모양에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-136">By default, a content page takes on the appearance from the master page.</span></span> <span data-ttu-id="264c1-137">그러나 마스터 페이지를 만들 때 콘텐츠 페이지 자체 내용으로 대체할 수 있는 페이지의 일부를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-137">However, when you create a master page, you can define portions of the page that the content page can replace with its own content.</span></span> <span data-ttu-id="264c1-138">ASP.NET 2.0;에 도입 된 새 컨트롤을 사용 하 여 이러한 부분 정의 **ContentPlaceHolder** 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-138">These portions are defined using a new control introduced in ASP.NET 2.0; the **ContentPlaceHolder** control.</span></span>

<span data-ttu-id="264c1-139">마스터 페이지에 임의 개수의 ContentPlaceHolder 컨트롤 (또는 전혀 나타나지 않습니다.)이 포함 될 수 있습니다. 콘텐츠 페이지에서 ContentPlaceHolder 컨트롤의 콘텐츠 안에 나타납니다 **콘텐츠** 컨트롤, ASP.NET 2.0의 다른 새 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-139">A master page can contain any number of ContentPlaceHolder controls (or none at all.) On the content page, the content from the ContentPlaceHolder controls appears inside of **Content** controls, another new control in ASP.NET 2.0.</span></span> <span data-ttu-id="264c1-140">기본적으로 직접 콘텐츠를 제공할 수 있도록 콘텐츠를 제어 하는 콘텐츠 페이지는 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-140">By default, the content pages Content controls are empty so that you can provide your own content.</span></span> <span data-ttu-id="264c1-141">콘텐츠 컨트롤 안의 마스터 페이지에서 콘텐츠를 사용 하려는 경우 수행할 수 있습니다 때마다이 모듈의 뒷부분에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-141">If you want to use the content from the master page inside of the Content controls, you can do so as you will see later in this module.</span></span> <span data-ttu-id="264c1-142">콘텐츠 컨트롤은 콘텐츠 컨트롤의 ContentPlaceHolderID 특성을 통해 ContentPlaceHolder 컨트롤에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-142">The Content control is mapped to the ContentPlaceHolder control via the ContentPlaceHolderID attribute of the Content control.</span></span> <span data-ttu-id="264c1-143">지도 아래 코드는 콘텐츠 ContentPlaceHolder 컨트롤을 mainBody 마스터 페이지를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-143">The code below maps a Content control to a ContentPlaceHolder control called mainBody on a master page.</span></span>

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> <span data-ttu-id="264c1-144">다른 페이지에 대 한 기본 클래스에 있는 것으로 마스터 페이지에 설명 하는 사용자를 종종 들립니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-144">You will often hear people describe master pages as being a base class for other pages.</span></span> <span data-ttu-id="264c1-145">Thats 실제로 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-145">Thats actually not true.</span></span> <span data-ttu-id="264c1-146">마스터 페이지 및 콘텐츠 페이지 간에 관계 상속의 하나가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-146">The relationship between master pages and content pages is not one of inheritance.</span></span>


<span data-ttu-id="264c1-147">**그림 1** 마스터 페이지와 연결 된 콘텐츠 페이지는 Visual Studio 2005에 나타나는 순서 대로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-147">**Figure 1** shows a master page and an associated content page as they appear in Visual Studio 2005.</span></span> <span data-ttu-id="264c1-148">마스터 페이지 및 해당 ContentPlaceHolder 컨트롤을 볼 수 콘텐츠 페이지에서 컨트롤의 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-148">You can see the ContentPlaceHolder control in the master page and the corresponding Content control in the content page.</span></span> <span data-ttu-id="264c1-149">ContentPlaceHolder는 밖에 있는 마스터 페이지 콘텐츠 표시 되기는 하지만 콘텐츠 페이지에서 흐리게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-149">Notice that the master pages content that is outside of the ContentPlaceHolder is visible but grayed out in the content page.</span></span> <span data-ttu-id="264c1-150">ContentPlaceHolder는 내부 콘텐츠만 콘텐츠 페이지에서 supplanted 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-150">Only the content inside of the ContentPlaceHolder can be supplanted by the content page.</span></span> <span data-ttu-id="264c1-151">마스터 페이지에서 제공 되는 모든 콘텐츠를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-151">All other content that comes from the master page is immutable.</span></span>


![마스터 페이지와 연결 된 해당 콘텐츠 페이지](master-pages/_static/image1.jpg)

<span data-ttu-id="264c1-153">**그림 1**: 마스터 페이지와 연결 된 해당 콘텐츠 페이지</span><span class="sxs-lookup"><span data-stu-id="264c1-153">**Figure 1**: A master page and its associated content page</span></span>


## <a name="creating-a-master-page"></a><span data-ttu-id="264c1-154">마스터 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="264c1-154">Creating a Master Page</span></span>

<span data-ttu-id="264c1-155">마스터 페이지를 새로 만들려면:</span><span class="sxs-lookup"><span data-stu-id="264c1-155">To create a new master page:</span></span>

1. <span data-ttu-id="264c1-156">Visual Studio 2005를 열고 새 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-156">Open Visual Studio 2005 and create a new Web site.</span></span>
2. <span data-ttu-id="264c1-157">파일을 새 파일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-157">Click File, New, File.</span></span>
3. <span data-ttu-id="264c1-158">에 표시 된 대로 마스터 파일을 새 항목 추가 대화 상자에서 선택 **그림 2**합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-158">Choose Master File from the Add New Item dialog as shown in **figure 2**.</span></span>
4. <span data-ttu-id="264c1-159">추가 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-159">Click Add.</span></span>


![새 마스터 페이지 만들기](master-pages/_static/image2.jpg)

<span data-ttu-id="264c1-161">**그림 2**: 새 마스터 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="264c1-161">**Figure 2**: Creating a New Master Page</span></span>


<span data-ttu-id="264c1-162">마스터 페이지에 대 한 파일 확장명은 <em>.master</em>합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-162">Notice that the file extension for a master page is <em>.master</em>.</span></span> <span data-ttu-id="264c1-163">일반 페이지에서 마스터 페이지와 다른 방법 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-163">This is one of the ways that a master page differs from an ordinary page.</span></span> <span data-ttu-id="264c1-164">다른 주요 차이점은 대신 하는 @Page 지시문, 마스터 페이지에는 @Master 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-164">The other primary difference is that in lieu of a @Page directive, the master page contains a @Master directive.</span></span> <span data-ttu-id="264c1-165">방금 만든 및 코드 검토 페이지는 마스터에 대 한 소스 보기로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-165">Switch to Source View for the master page youve just created and review the code.</span></span>

<span data-ttu-id="264c1-166">새 마스터 페이지에는 기본적으로 하나의 ContentPlaceHolder 권한을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-166">A new master page will have one ContentPlaceHolder control by default.</span></span> <span data-ttu-id="264c1-167">대부분의 경우는 것이를 일반적인 페이지 요소를 먼저 만들고 ContentPlaceHolder 컨트롤을 삽입 한 다음 사용자 지정 콘텐츠를 원할 경우.</span><span class="sxs-lookup"><span data-stu-id="264c1-167">In most cases, it makes more sense to create the common page elements first and then insert ContentPlaceHolder controls where custom content is desired.</span></span> <span data-ttu-id="264c1-168">이 경우 개발자가 기본 ContentPlaceHolder 컨트롤을 삭제 하 고 페이지도 개발 된 대로 새 레코드를 삽입 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-168">In those cases, developers will want to delete the default ContentPlaceHolder control and insert new ones as the page is developed.</span></span> <span data-ttu-id="264c1-169">ContentPlaceHolder 컨트롤은 크기 조정 핸들을 표시 않는지도 크기를 조정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-169">ContentPlaceHolder controls are not resizable despite the fact that they do display sizing handles.</span></span> <span data-ttu-id="264c1-170">한 가지 예외로; 포함 된 내용에 따라 자동으로 ContentPlaceHolder 컨트롤 크기 예: 표 셀 블록 요소 안에 ContentPlaceHolder 컨트롤을 추가 하면 그 요소의 크기에 따라 크기 됩니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-170">The ContentPlaceHolder control sizes automatically based upon the content that it contains with one exception; if you place a ContentPlaceHolder control inside of a block element such as a table cell, it will size according to the size of the element.</span></span>

## <a name="lab-1-working-with-master-pages"></a><span data-ttu-id="264c1-171">랩 1 마스터 페이지 사용</span><span class="sxs-lookup"><span data-stu-id="264c1-171">Lab 1 Working with Master Pages</span></span>

<span data-ttu-id="264c1-172">이 랩에서 마스터 페이지를 새로 만들고 세 개의 ContentPlaceHolder 컨트롤을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-172">In this lab, you will create a new master page and define three ContentPlaceHolder controls.</span></span> <span data-ttu-id="264c1-173">그런 다음 새 콘텐츠 페이지를 만들고 쿼리하고 ContentPlaceHolder 컨트롤 중 하나 이상에서 콘텐츠를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-173">You will then create a new Content page and replace the content from at least one of the ContentPlaceHolder controls.</span></span>

1. <span data-ttu-id="264c1-174">마스터 페이지를 만들고 ContentPlaceHolder 컨트롤을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-174">Create a master page and insert ContentPlaceHolder controls.</span></span> 

    1. <span data-ttu-id="264c1-175">위에 설명 된 대로 새 마스터 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-175">Create a new master page as described above.</span></span>
    2. <span data-ttu-id="264c1-176">기본 ContentPlaceHolder 컨트롤을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-176">Delete the default ContentPlaceHolder control.</span></span>
    3. <span data-ttu-id="264c1-177">컨트롤의 위쪽 회색된 테두리를 클릭 하 여 ContentPlaceHolder 컨트롤을 선택한 다음 키보드에서 DEL 키를 클릭 하 여 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-177">Select the ContentPlaceHolder control by clicking the shaded top border of the control and then delete it by hitting the DEL key on your keyboard.</span></span>
    4. <span data-ttu-id="264c1-178">사용 하 여 새 테이블을 삽입의 *헤더 편인* 그림 3에에서 표시 된 것 처럼 템플릿.</span><span class="sxs-lookup"><span data-stu-id="264c1-178">Insert a new table using the *Header and side* template as shown in figure 3.</span></span> <span data-ttu-id="264c1-179">전체 테이블 디자이너에서 볼 수 있도록을 90%의 너비와 높이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-179">Change the width and height to 90% each so that the entire table is visible in the designer.</span></span>


![](master-pages/_static/image3.jpg)

<span data-ttu-id="264c1-180">**그림 3**</span><span class="sxs-lookup"><span data-stu-id="264c1-180">**Figure 3**</span></span>


1. <span data-ttu-id="264c1-181">테이블의 각 셀에 커서를 놓고 설정는 *valign* 속성을 *top*합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-181">Place the cursor into each cell of the table and set the *valign* property to *top*.</span></span>
2. <span data-ttu-id="264c1-182">도구 상자에서 ContentPlaceHolder 컨트롤 테이블 (머리글 셀.)의 맨 위 셀 삽입</span><span class="sxs-lookup"><span data-stu-id="264c1-182">From the Toolbox, insert a ContentPlaceHolder control in the top cell of the table (the header cell.)</span></span>
3. <span data-ttu-id="264c1-183">이 ContentPlaceHolder 컨트롤을 삽입 하는 경우에 행 높이 차지 하는 거의 전체 페이지 그림 4에에서 나와 있는 것 처럼 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-183">When you insert this ContentPlaceHolder control, you will notice that the row height will take up almost the entire page as shown in figure 4.</span></span> <span data-ttu-id="264c1-184">금지 관여 하는 시점에서.</span><span class="sxs-lookup"><span data-stu-id="264c1-184">Dont be concerned about that at this point.</span></span>


![빈 공간은 ContentPlaceHolder로 동일한 셀](master-pages/_static/image1.gif)

<span data-ttu-id="264c1-186">**그림 4**: 빈 공간은 ContentPlaceHolder로 동일한 셀</span><span class="sxs-lookup"><span data-stu-id="264c1-186">**Figure 4**: The empty space is in the same cell as the ContentPlaceHolder</span></span>


1. <span data-ttu-id="264c1-187">다른 두 셀에서 ContentPlaceHolder 컨트롤을 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-187">Place a ContentPlaceHolder control in the other two cells.</span></span> <span data-ttu-id="264c1-188">다른 ContentPlaceHolder 컨트롤이 삽입 되 면 테이블 셀의 크기를 예상 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-188">Once the other ContentPlaceHolder controls have been inserted, the size of the table cells should be as you would expect.</span></span> <span data-ttu-id="264c1-189">이제 페이지에 표시 된 페이지 같은 모양이 **그림 5**합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-189">The page should now look like the page shown in **figure 5**.</span></span>


![모든 ContentPlaceHolder 컨트롤과 마스터입니다.](master-pages/_static/image2.gif)

<span data-ttu-id="264c1-192">**그림 5**: 모든 ContentPlaceHolder 컨트롤과 The 마스터 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-192">**Figure 5**: The Master with all ContentPlaceHolder controls.</span></span> <span data-ttu-id="264c1-193">머리글 셀에 대 한 셀 높이 이제가 원래 표시 되어야</span><span class="sxs-lookup"><span data-stu-id="264c1-193">Notice that the cell height for the header cell is now what it should be</span></span>


1. <span data-ttu-id="264c1-194">각각의 세 가지 ContentPlaceHolder 컨트롤에 사용자가 선택한 텍스트를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-194">Enter some text of your choice into each of the three ContentPlaceHolder controls.</span></span>
2. <span data-ttu-id="264c1-195">Exercise1.master로 마스터 페이지를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-195">Save the master page as exercise1.master.</span></span>
3. <span data-ttu-id="264c1-196">새 Web Form을 만들고 exercise1.master 마스터 페이지와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-196">Create a new Web Form and associate it with the exercise1.master master page.</span></span>
4. <span data-ttu-id="264c1-197">Visual Studio 2005에서 파일을 새 파일을 선택.</span><span class="sxs-lookup"><span data-stu-id="264c1-197">Select File, New, File in Visual Studio 2005.</span></span>
5. <span data-ttu-id="264c1-198">선택 **Web Form** 새 항목 추가 대화 상자에서.</span><span class="sxs-lookup"><span data-stu-id="264c1-198">Select **Web Form** in the Add New Item dialog.</span></span>
6. <span data-ttu-id="264c1-199">그림 6에에서 나와 있는 것 처럼에서 마스터 페이지 선택 확인란을 선택 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-199">Make sure that the Select master page checkbox is checked as shown in figure 6.</span></span>


![새 콘텐츠 페이지를 추가합니다.](master-pages/_static/image3.gif)

<span data-ttu-id="264c1-201">**그림 6**: 새 콘텐츠 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-201">**Figure 6**: Adding a new Content Page</span></span>


1. <span data-ttu-id="264c1-202">추가 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-202">Click Add.</span></span>
2. <span data-ttu-id="264c1-203">Exercise1.master 선택에서 마스터 페이지 대화 상자에에서 표시 된 선택 그림 7입니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-203">Select exercise1.master in the Select a master page dialog as shown in figure 7.</span></span>
3. <span data-ttu-id="264c1-204">새 콘텐츠 페이지를 추가 하려면 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-204">Click OK to add the new content page.</span></span>

<span data-ttu-id="264c1-205">새 콘텐츠 페이지는 마스터 페이지에 있는 각 ContentPlaceHolder 컨트롤에 대 한 하나의 콘텐츠 컨트롤과 Visual Studio에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-205">The new content page appears in Visual Studio with one Content control for each ContentPlaceHolder control on the master page.</span></span> <span data-ttu-id="264c1-206">기본적으로 콘텐츠 컨트롤 내용을 직접 추가할 수 있도록 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-206">By default, the Content controls are empty so that you can add your own content.</span></span> <span data-ttu-id="264c1-207">Youd 마음에 마스터 페이지에서 ContentPlaceHolder 컨트롤에서 콘텐츠를 사용 하지 않으면 하기만 하면 스마트 태그 기호 (컨트롤의 오른쪽 위 모서리에 작은 검은색 화살표)를 클릭 하 고 선택 *마스터 콘텐츠 기본값* 와 같이 스마트 태그에서 **그림 8**합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-207">If youd like for them to use the content from the ContentPlaceHolder control on the master page, simply click on the smart tag symbol (the small black arrow in the upper-right corner of the control) and choose *Default to Masters Content* from the smart tag as shown in **figure 8**.</span></span> <span data-ttu-id="264c1-208">이렇게 하면 메뉴 항목을 변경 *사용자 지정 콘텐츠 만들기*합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-208">When you do so, the menu item changes to *Create Custom Content*.</span></span> <span data-ttu-id="264c1-209">시점 클릭 하면 해당 특정 콘텐츠 컨트롤에 대 한 사용자 지정 콘텐츠를 정의할 수 있도록 마스터 페이지에서 콘텐츠를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-209">Clicking it at that point removes the content from the master page allowing you to define custom content for that particular Content control.</span></span>


![콘텐츠 컨트롤을 마스터 페이지 콘텐츠를 기본값으로 설정](master-pages/_static/image4.gif)

<span data-ttu-id="264c1-211">**그림 7**: 콘텐츠 컨트롤에 마스터 페이지 콘텐츠를 기본값으로 설정</span><span class="sxs-lookup"><span data-stu-id="264c1-211">**Figure 7**: Setting a Content Control to Default to the Master Pages Content</span></span>


## <a name="connecting-master-page-and-content-pages"></a><span data-ttu-id="264c1-212">마스터 페이지 및 콘텐츠 페이지에 연결</span><span class="sxs-lookup"><span data-stu-id="264c1-212">Connecting Master Page and Content Pages</span></span>

<span data-ttu-id="264c1-213">네 가지 방법 중 하나에서 마스터 페이지 콘텐츠 페이지와의 연결을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-213">The association between a master page and a content page can be configured in one of four different ways:</span></span>

- <span data-ttu-id="264c1-214"><strong>MasterPageFile</strong> 특성에는 @Page 지시문</span><span class="sxs-lookup"><span data-stu-id="264c1-214">The <strong>MasterPageFile</strong> attribute of the @Page directive</span></span>
- <span data-ttu-id="264c1-215">설정의 **Page.MasterPageFile** 코드에서 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-215">Setting the **Page.MasterPageFile** property in code.</span></span>
- <span data-ttu-id="264c1-216">**&lt;페이지&gt;** 응용 프로그램 구성 파일 (응용 프로그램의 루트 폴더에 web.config)의 요소</span><span class="sxs-lookup"><span data-stu-id="264c1-216">The **&lt;pages&gt;** element in the applications configuration file (web.config in the root folder of the application)</span></span>
- <span data-ttu-id="264c1-217">**&lt;페이지&gt;** 하위 폴더 구성 파일 (하위 폴더에 web.config)의 요소</span><span class="sxs-lookup"><span data-stu-id="264c1-217">The **&lt;pages&gt;** element in a subfolders configuration file (web.config in a subfolder)</span></span>

## <a name="masterpagefile-attribute"></a><span data-ttu-id="264c1-218">MasterPageFile 특성</span><span class="sxs-lookup"><span data-stu-id="264c1-218">MasterPageFile Attribute</span></span>

<span data-ttu-id="264c1-219">MasterPageFile 특성을 사용 하면 쉽게 특정 ASP.NET 페이지에 마스터 페이지를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-219">The MasterPageFile attribute makes it easy to apply a master page to a particular ASP.NET page.</span></span> <span data-ttu-id="264c1-220">마스터 페이지를 검사할 때 적용 하는 데 사용 하는 방법 이기도 **마스터 페이지 선택** 실습 1에서 수행한 때 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-220">It is also the method used to apply the master page when you check the **Select Master Page** checkbox as you did in Exercise 1.</span></span>

## <a name="setting-pagemasterpagefile-in-code"></a><span data-ttu-id="264c1-221">코드에서 Page.MasterPageFile 설정</span><span class="sxs-lookup"><span data-stu-id="264c1-221">Setting Page.MasterPageFile in Code</span></span>

<span data-ttu-id="264c1-222">코드에서 MasterPageFile 속성을 설정 하 여 특정 마스터 페이지를 런타임에 콘텐츠에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-222">By setting the MasterPageFile property in code, you can apply a particular master page to your content at runtime.</span></span> <span data-ttu-id="264c1-223">사용자가 역할 또는 기타 일부 조건에 따라 특정 마스터 페이지를 적용 해야 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-223">This is useful in cases where you may need to apply a specific master page based upon a users role or some other criteria.</span></span> <span data-ttu-id="264c1-224">MasterPageFile 속성 PreInit 메서드에서 설정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-224">The MasterPageFile property must be set in the PreInit method.</span></span> <span data-ttu-id="264c1-225">PreInit 메서드 다음으로 설정 하는 InvalidOperationException throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-225">If it is set after the PreInit method, an InvalidOperationException will be thrown.</span></span> <span data-ttu-id="264c1-226">이 속성을 설정 하는 페이지 콘텐츠 있어야 페이지에 대 한 최상위 컨트롤로 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-226">The page on which this property is being set must also have a Content control as the top-level control for the page.</span></span> <span data-ttu-id="264c1-227">그렇지 않은 경우는 HttpException MasterPageFile 속성이 설정 된 경우 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-227">Otherwise an HttpException will be thrown when the MasterPageFile property is set.</span></span>

## <a name="using-the-ltpagesgt-element"></a><span data-ttu-id="264c1-228">사용 하 여 &lt;페이지&gt; 요소</span><span class="sxs-lookup"><span data-stu-id="264c1-228">Using the &lt;pages&gt; Element</span></span>

<span data-ttu-id="264c1-229">masterPageFile 특성을 설정 하 여 페이지에 대 한 마스터 페이지를 구성할 수 있습니다는 &lt;페이지&gt; web.config 파일의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-229">You can configure a master page for your pages by setting the masterPageFile attribute in the &lt;pages&gt; element of the web.config file.</span></span> <span data-ttu-id="264c1-230">이 메서드를 사용 하면 응용 프로그램 구조에서 하위 web.config 파일에이 설정을 재정의할 수를 염두에서에 둬야 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-230">When using this method, keep in mind that web.config files lower in the application structure can override this setting.</span></span> <span data-ttu-id="264c1-231">모든 MasterPageFile 속성 세트는 @Page 지시문이이 설정을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-231">Any MasterPageFile attribute set in a @Page directive will also override this setting.</span></span> <span data-ttu-id="264c1-232">사용 하는 &lt;페이지&gt; 요소를 사용 하면 간단 하 게 만들 수는 <em>마스터</em> 특정 폴더 또는 파일에 필요한 경우 재정의할 수 있는 마스터 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-232">Using the &lt;pages&gt; element makes it simple to create a <em>master</em> master page that can be overridden if necessary in particular folders or files.</span></span>

## <a name="properties-in-master-pages"></a><span data-ttu-id="264c1-233">마스터 페이지에서 속성</span><span class="sxs-lookup"><span data-stu-id="264c1-233">Properties in Master Pages</span></span>

<span data-ttu-id="264c1-234">마스터 페이지 하기만 하면 이러한 속성 마스터 페이지 내에서 public 속성을 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-234">A master page can expose properties by simply making those properties public within the master page.</span></span> <span data-ttu-id="264c1-235">예를 들어 다음 코드는 SomeProperty 라는 속성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-235">For example, the following code defines a property called SomeProperty:</span></span>

[!code-csharp[Main](master-pages/samples/sample2.cs)]

<span data-ttu-id="264c1-236">콘텐츠 페이지의 SomeProperty 속성에 액세스 하려면 Master를 사용 해야 합니다 같이 속성:</span><span class="sxs-lookup"><span data-stu-id="264c1-236">To access the SomeProperty property from the Content page, you will need to use the Master property like so:</span></span>

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a><span data-ttu-id="264c1-237">중첩 마스터 페이지</span><span class="sxs-lookup"><span data-stu-id="264c1-237">Nesting Master Pages</span></span>

<span data-ttu-id="264c1-238">마스터 페이지는 대형 웹 응용 프로그램에서 공통 된 모양 및 느낌을 위한 완벽 한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-238">Master pages are the perfect solution for ensuring a common look and feel across a large Web application.</span></span> <span data-ttu-id="264c1-239">그러나 다른 파트는 다른 인터페이스를 공유 하는 동안 큰 사이트 공유 공통 인터페이스의 특정 부분에 있는 것 도지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-239">However, it's not uncommon to have certain parts of a large site share a common interface while other parts share a different interface.</span></span> <span data-ttu-id="264c1-240">해당 요구를 해결 하기 위해 다중 마스터 페이지는 완벽 한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-240">To address that need, multiple master pages are the perfect solution.</span></span> <span data-ttu-id="264c1-241">그러나 해당 여전히 사이트의 특정 섹션만 간에 공유 되는 다른 구성 요소 및 특정 구성 요소 (예: 메뉴, 예를 들어) 모든 페이지 간에 공유 되는 대형 응용 프로그램에 있을 수 있다는 사실을 해결 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-241">However, that still doesn't address the fact that a large application may have certain components (such as a menu, for example) that are shared among all pages and other components that are shared only among certain sections of the site.</span></span> <span data-ttu-id="264c1-242">해당 유형의 상황에 대 한 중첩 된 마스터 페이지의 필요성을 원활 하 게 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-242">For that type of situation, nested master pages fill the need nicely.</span></span> <span data-ttu-id="264c1-243">앞서 살펴본 것 처럼 표준 마스터 페이지 마스터 페이지 및 콘텐츠 페이지 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-243">As you've seen, a normal master page consists of a master page and a content page.</span></span> <span data-ttu-id="264c1-244">중첩 된 마스터 페이지를 사용 하는 경우에는 두 개의 마스터 페이지; 부모 마스터 및 하위 마스터 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-244">In a nested master page situation, there are two master pages; a parent master and a child master.</span></span> <span data-ttu-id="264c1-245">자식 마스터 페이지 콘텐츠 페이지 진행 되며 해당 마스터 부모 마스터 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-245">The child master page is also a content page and its master is the parent master page.</span></span>

<span data-ttu-id="264c1-246">일반적인 마스터 페이지에 대 한 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-246">Here is the code for a typical master page:</span></span>

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

<span data-ttu-id="264c1-247">중첩된 된 마스터 시나리오에서 부모 마스터가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-247">In a nested master scenario, this would be the parent master.</span></span> <span data-ttu-id="264c1-248">다른 마스터 페이지는 마스터 페이지의으로이 페이지를 사용 하 고 해당 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-248">Another master page would use this page as its master page, and that code would look like this:</span></span>

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

<span data-ttu-id="264c1-249">이 시나리오를 자식 마스터 부모 마스터에 대 한 콘텐츠 페이지 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-249">Note that in this scenario, the child master is also a content page for the parent master.</span></span> <span data-ttu-id="264c1-250">모든 자식 마스터 콘텐츠 부모의 ContentPlaceHolder 컨트롤에서 해당 콘텐츠를 가져오는 콘텐츠 컨트롤 안에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-250">All of the child master's content appears inside of a Content control that gets its content from the parent's ContentPlaceHolder control.</span></span>

> [!NOTE]
> <span data-ttu-id="264c1-251">중첩 된 마스터 페이지에 대 한 디자이너 지원을 ´ ù.</span><span class="sxs-lookup"><span data-stu-id="264c1-251">Designer support is not available for nested master pages.</span></span> <span data-ttu-id="264c1-252">중첩 된 마스터를 사용 하 여를 개발 하는 경우 소스 뷰를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-252">When you are developing using nested masters, you will need to use source view.</span></span>


<span data-ttu-id="264c1-253">이 비디오에서는 중첩 된 마스터 페이지를 사용 하 여 보여 주는 연습을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-253">This video shows a walkthrough of using nested master pages.</span></span>


![](master-pages/_static/image1.png)


[<span data-ttu-id="264c1-254">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="264c1-254">Open Full-Screen Video</span></span>](master-pages/_static/nested1.wmv)


![마스터 페이지를 선택합니다.](master-pages/_static/image4.jpg)

<span data-ttu-id="264c1-256">**그림 8**: 마스터 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="264c1-256">**Figure 8**: Selecting a Master Page</span></span>
