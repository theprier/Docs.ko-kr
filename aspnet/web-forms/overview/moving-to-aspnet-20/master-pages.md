---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: 마스터 페이지 | Microsoft Docs
author: microsoft
description: 성공적인 웹 사이트에 대 한 주요 구성 요소 중 하나는 일관 된 모양과 느낌입니다. Asp.net에서 1.x에서 개발자는 일반적인 페이지 소형을 복제 하기 위해 사용자 정의 컨트롤을 사용...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: f40eb338a1b6b8eebb6578dd7938e96a05b1617f
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829749"
---
<a name="master-pages"></a><span data-ttu-id="338a8-104">마스터 페이지</span><span class="sxs-lookup"><span data-stu-id="338a8-104">Master Pages</span></span>
====================
<span data-ttu-id="338a8-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="338a8-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="338a8-106">성공적인 웹 사이트에 대 한 주요 구성 요소 중 하나는 일관 된 모양과 느낌입니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-106">One of the key components to a successful Web site is a consistent look and feel.</span></span> <span data-ttu-id="338a8-107">Asp.net에서 1.x에서 개발자는 웹 응용 프로그램에서 일반적인 페이지 요소를 복제할 사용자 정의 컨트롤을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-107">In ASP.NET 1.x, developers used user controls to replicate common page elements across a Web application.</span></span> <span data-ttu-id="338a8-108">확실히 작동 가능한 솔루션을 사용 되 고 있지만, 사용자 컨트롤을 사용 하는 몇 가지 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-108">While that is certainly a workable solution, using user controls does have some drawbacks.</span></span> <span data-ttu-id="338a8-109">예를 들어, 사용자 정의 컨트롤의 위치 변경 사이트 전체에서 여러 페이지에 대 한 변경에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-109">For example, a change in position of a user control requires a change to multiple pages across a site.</span></span> <span data-ttu-id="338a8-110">사용자 정의 컨트롤은 또한 페이지에 삽입 한 후 디자인 보기에서 렌더링 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-110">User controls are also not rendered in Design view after being inserted on a page.</span></span>


<span data-ttu-id="338a8-111">성공적인 웹 사이트에 대 한 주요 구성 요소 중 하나는 일관 된 모양과 느낌입니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-111">One of the key components to a successful Web site is a consistent look and feel.</span></span> <span data-ttu-id="338a8-112">Asp.net에서 1.x에서 개발자는 웹 응용 프로그램에서 일반적인 페이지 요소를 복제할 사용자 정의 컨트롤을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-112">In ASP.NET 1.x, developers used user controls to replicate common page elements across a Web application.</span></span> <span data-ttu-id="338a8-113">확실히 작동 가능한 솔루션을 사용 되 고 있지만, 사용자 컨트롤을 사용 하는 몇 가지 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-113">While that is certainly a workable solution, using user controls does have some drawbacks.</span></span> <span data-ttu-id="338a8-114">예를 들어, 사용자 정의 컨트롤의 위치 변경 사이트 전체에서 여러 페이지에 대 한 변경에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-114">For example, a change in position of a user control requires a change to multiple pages across a site.</span></span> <span data-ttu-id="338a8-115">사용자 정의 컨트롤은 또한 페이지에 삽입 한 후 디자인 보기에서 렌더링 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-115">User controls are also not rendered in Design view after being inserted on a page.</span></span>

<span data-ttu-id="338a8-116">ASP.NET 2.0에서는 마스터 페이지는 일관 된 모양과 느낌을 유지 관리 하는 방법으로 되며 곧 알게 되겠지만, 마스터 페이지 사용자 지정 컨트롤 메서드를 통해 상당히 향상 된 기능을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-116">ASP.NET 2.0 introduces Master pages as a way of maintaining a consistent look and feel, and as you'll soon see, Master pages represent a significant improvement over the user control method.</span></span>

## <a name="why-master-pages"></a><span data-ttu-id="338a8-117">마스터 페이지를 이유?</span><span class="sxs-lookup"><span data-stu-id="338a8-117">Why Master Pages?</span></span>

<span data-ttu-id="338a8-118">ASP.NET 2.0에서 마스터 페이지 필요한 이유는 궁금할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-118">You may be wondering why master pages were needed in ASP.NET 2.0.</span></span> <span data-ttu-id="338a8-119">결국 웹 사이트 개발자 이미 사용 하는 사용자 정의 컨트롤에서 ASP.NET 1.x 콘텐츠 영역 페이지 간에 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-119">After all, Web site developers are already using user controls in ASP.NET 1.x to share content areas between pages.</span></span> <span data-ttu-id="338a8-120">사용자 정의 컨트롤의 일반적인 레이아웃을 만드는 덜 보다 최적의 솔루션은 이유는 실제로 몇 가지 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-120">There are actually several reasons why user controls are a less-than-optimal solution for creating a common layout.</span></span>

<span data-ttu-id="338a8-121">사용자 정의 컨트롤 페이지 레이아웃을 실제로 정의 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-121">User controls don't actually define page layout.</span></span> <span data-ttu-id="338a8-122">대신, 레이아웃 및 기능 페이지의 일부를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-122">Instead, they define the layout and functionality for a portion of a page.</span></span> <span data-ttu-id="338a8-123">사용자 제어 솔루션의 관리를 훨씬 더 어렵습니다 되므로 이러한 두 간의 구분이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-123">The distinction between these two is important because it makes manageability of a user control solution much more difficult.</span></span> <span data-ttu-id="338a8-124">예를 들어 페이지에서 사용자 정의 컨트롤의 위치를 변경 하려는 경우 사용자 정의 컨트롤이 표시 되는 실제 페이지를 편집 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-124">For example, when you want to change the position of a user control on your page, you must edit the actual page on which the user control appears.</span></span> <span data-ttu-id="338a8-125">Thats 잠시 페이지만 있지만 대규모 사이트에서 신속 하 게 되기 사이트 관리 문제일 경우 미세!</span><span class="sxs-lookup"><span data-stu-id="338a8-125">Thats fine if you have only a few pages, but in large sites, it quickly becomes a site management nightmare!</span></span>

<span data-ttu-id="338a8-126">사용자 정의 컨트롤을 사용 하 여 일반적인 레이아웃을 정의 하기 위한 또 다른 단점은 ASP.NET 자체가의 아키텍처 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-126">Another drawback of using user controls for defining a common layout is rooted in the architecture of ASP.NET itself.</span></span> <span data-ttu-id="338a8-127">사용자 정의 컨트롤의 모든 public 멤버 변경 되 면 모든 사용자 정의 컨트롤을 사용 하는 페이지를 다시 컴파일할 수 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-127">If any public member of a user control is changed, it requires you to recompile all of the pages that use the user control.</span></span> <span data-ttu-id="338a8-128">따라서 ASP.NET 다시 JIT 첫 번째 경우에 페이지에 액세스 한 다음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-128">In turn, ASP.NET will then re-JIT your pages when they are first accessed.</span></span> <span data-ttu-id="338a8-129">이 확장 가능한 비 아키텍처 및 대규모 사이트의 사이트 관리 문제는 다시 한 번 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-129">This, once again, produces a non-scalable architecture and a site management problem for larger sites.</span></span>

<span data-ttu-id="338a8-130">ASP.NET 2.0에서 마스터 페이지에서 보기 좋게 사항은 모두 이러한 문제 (및 더 많은).</span><span class="sxs-lookup"><span data-stu-id="338a8-130">Both of these problems (and many more) are nicely addressed by master pages in ASP.NET 2.0.</span></span>

## <a name="how-master-pages-work"></a><span data-ttu-id="338a8-131">마스터 페이지의 작동 방식</span><span class="sxs-lookup"><span data-stu-id="338a8-131">How Master Pages Work</span></span>

<span data-ttu-id="338a8-132">마스터 페이지는 다른 페이지에 대 한 템플릿을 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-132">A master page is analogous to a template for other pages.</span></span> <span data-ttu-id="338a8-133">페이지 요소 (즉, 메뉴, 테두리 등)에 다른 페이지 간에 공유 해야 하는 마스터 페이지에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-133">Page elements that should be shared among other pages (i.e. menus, borders, etc.) are added to the master page.</span></span> <span data-ttu-id="338a8-134">새 페이지는 사이트에 추가 하는 경우에 마스터 페이지를 사용 하 여 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-134">When new pages are added to the site, you can associate them with a master page.</span></span> <span data-ttu-id="338a8-135">마스터 페이지와 연관 된 페이지가 호출 되는 **콘텐츠 페이지**합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-135">A page that is associated with a master page is called a **content page**.</span></span> <span data-ttu-id="338a8-136">기본적으로 콘텐츠 페이지 마스터 페이지의 모양을 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-136">By default, a content page takes on the appearance from the master page.</span></span> <span data-ttu-id="338a8-137">그러나 마스터 페이지를 만든 경우 콘텐츠 페이지 자체 콘텐츠를 사용 하 여 대체할 수 있는 페이지의 일부를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-137">However, when you create a master page, you can define portions of the page that the content page can replace with its own content.</span></span> <span data-ttu-id="338a8-138">이러한 일부 ASP.NET 2.0에 도입 된 새 컨트롤을 사용 하 여 정의 된 합니다 **ContentPlaceHolder** 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-138">These portions are defined using a new control introduced in ASP.NET 2.0; the **ContentPlaceHolder** control.</span></span>

<span data-ttu-id="338a8-139">마스터 페이지는 임의 개수의 contentplaceholder (또는 전혀 나타나지 않습니다.)를 포함할 수 있습니다. 콘텐츠 페이지의 내에 ContentPlaceHolder 컨트롤에서 내용이 나타납니다 **콘텐츠** 컨트롤, ASP.NET 2.0의 다른 새로운 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-139">A master page can contain any number of ContentPlaceHolder controls (or none at all.) On the content page, the content from the ContentPlaceHolder controls appears inside of **Content** controls, another new control in ASP.NET 2.0.</span></span> <span data-ttu-id="338a8-140">기본적으로 사용자 고유의 콘텐츠를 제공할 수 있도록 콘텐츠 제어 콘텐츠 페이지는 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-140">By default, the content pages Content controls are empty so that you can provide your own content.</span></span> <span data-ttu-id="338a8-141">콘텐츠 컨트롤 내부에서 마스터 페이지의 콘텐츠를 사용 하려는 경우 수행할 수 있습니다 따라서 나중에이 모듈에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-141">If you want to use the content from the master page inside of the Content controls, you can do so as you will see later in this module.</span></span> <span data-ttu-id="338a8-142">콘텐츠 컨트롤의 콘텐츠 컨트롤의 ContentPlaceHolderID 특성을 통해 각각의 ContentPlaceHolder 컨트롤로 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-142">The Content control is mapped to the ContentPlaceHolder control via the ContentPlaceHolderID attribute of the Content control.</span></span> <span data-ttu-id="338a8-143">맵 아래 코드 mainBody 마스터 페이지 라는 ContentPlaceHolder 컨트롤에 콘텐츠 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-143">The code below maps a Content control to a ContentPlaceHolder control called mainBody on a master page.</span></span>

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> <span data-ttu-id="338a8-144">말을 자주 듣습니다 사람으로 다른 페이지에 대 한 기본 클래스 마스터 페이지에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-144">You will often hear people describe master pages as being a base class for other pages.</span></span> <span data-ttu-id="338a8-145">Thats 실제로 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-145">Thats actually not true.</span></span> <span data-ttu-id="338a8-146">마스터 페이지 콘텐츠 페이지와의 관계 상속의 하나가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-146">The relationship between master pages and content pages is not one of inheritance.</span></span>


<span data-ttu-id="338a8-147">**그림 1** Visual Studio 2005에 나타나는 대로 마스터 페이지와 연결 된 콘텐츠 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-147">**Figure 1** shows a master page and an associated content page as they appear in Visual Studio 2005.</span></span> <span data-ttu-id="338a8-148">마스터 페이지 및 해당 ContentPlaceHolder 컨트롤로 표시 콘텐츠 콘텐츠 페이지에는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-148">You can see the ContentPlaceHolder control in the master page and the corresponding Content control in the content page.</span></span> <span data-ttu-id="338a8-149">마스터 페이지 콘텐츠를 ContentPlaceHolder 외부를 볼 수 있지만 콘텐츠 페이지에서 회색 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-149">Notice that the master pages content that is outside of the ContentPlaceHolder is visible but grayed out in the content page.</span></span> <span data-ttu-id="338a8-150">ContentPlaceHolder 내부 콘텐츠만 콘텐츠 페이지에서 supplanted 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-150">Only the content inside of the ContentPlaceHolder can be supplanted by the content page.</span></span> <span data-ttu-id="338a8-151">마스터 페이지에서 제공 되는 다른 모든 콘텐츠는 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-151">All other content that comes from the master page is immutable.</span></span>


![마스터 페이지와 연결 된 해당 콘텐츠 페이지](master-pages/_static/image1.jpg)

<span data-ttu-id="338a8-153">**그림 1**: 마스터 페이지와 연결 된 해당 콘텐츠 페이지</span><span class="sxs-lookup"><span data-stu-id="338a8-153">**Figure 1**: A master page and its associated content page</span></span>


## <a name="creating-a-master-page"></a><span data-ttu-id="338a8-154">마스터 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="338a8-154">Creating a Master Page</span></span>

<span data-ttu-id="338a8-155">마스터 페이지를 새로 만들려면:</span><span class="sxs-lookup"><span data-stu-id="338a8-155">To create a new master page:</span></span>

1. <span data-ttu-id="338a8-156">Visual Studio 2005를 열고 새 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-156">Open Visual Studio 2005 and create a new Web site.</span></span>
2. <span data-ttu-id="338a8-157">파일을 새 파일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-157">Click File, New, File.</span></span>
3. <span data-ttu-id="338a8-158">에 표시 된 대로 마스터 파일을 새 항목 추가 대화 상자에서 선택 **그림 2**합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-158">Choose Master File from the Add New Item dialog as shown in **figure 2**.</span></span>
4. <span data-ttu-id="338a8-159">추가 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-159">Click Add.</span></span>


![새 마스터 페이지 만들기](master-pages/_static/image2.jpg)

<span data-ttu-id="338a8-161">**그림 2**: 새 마스터 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="338a8-161">**Figure 2**: Creating a New Master Page</span></span>


<span data-ttu-id="338a8-162">마스터 페이지의 파일 확장명은 되었다는 <em>.master</em>합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-162">Notice that the file extension for a master page is <em>.master</em>.</span></span> <span data-ttu-id="338a8-163">일반 페이지에서 마스터 페이지와 다른 방법 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-163">This is one of the ways that a master page differs from an ordinary page.</span></span> <span data-ttu-id="338a8-164">대신 프로시저의 다른 주요 차이점은는 @Page 마스터 페이지 지시문을 포함을 @Master 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-164">The other primary difference is that in lieu of a @Page directive, the master page contains a @Master directive.</span></span> <span data-ttu-id="338a8-165">방금 만든 및 코드 검토 페이지 마스터에 대 한 소스 보기로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-165">Switch to Source View for the master page youve just created and review the code.</span></span>

<span data-ttu-id="338a8-166">새 마스터 페이지를 기본적으로 각각의 ContentPlaceHolder 컨트롤로 하나를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-166">A new master page will have one ContentPlaceHolder control by default.</span></span> <span data-ttu-id="338a8-167">대부분의 경우에서 것이 더 좋은 일반적인 페이지 요소를 먼저 만들고 contentplaceholder를 삽입 한 다음 사용자 지정 내용이 필요한 곳입니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-167">In most cases, it makes more sense to create the common page elements first and then insert ContentPlaceHolder controls where custom content is desired.</span></span> <span data-ttu-id="338a8-168">이러한 경우 개발자가 기본 ContentPlaceHolder 컨트롤을 삭제 하 여 페이지 개발은 새로 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-168">In those cases, developers will want to delete the default ContentPlaceHolder control and insert new ones as the page is developed.</span></span> <span data-ttu-id="338a8-169">ContentPlaceHolder 컨트롤은 크기 조정 핸들을 표시지 않습니다 팩트 불구 하 고 크기를 조정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-169">ContentPlaceHolder controls are not resizable despite the fact that they do display sizing handles.</span></span> <span data-ttu-id="338a8-170">한 가지 예외로; 포함 된 내용에 따라 자동으로 ContentPlaceHolder 컨트롤 크기 블록 요소 안에 각각의 ContentPlaceHolder 컨트롤로 같은 표 셀에 배치 하면 요소의 크기에 따라 크기 조정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-170">The ContentPlaceHolder control sizes automatically based upon the content that it contains with one exception; if you place a ContentPlaceHolder control inside of a block element such as a table cell, it will size according to the size of the element.</span></span>

## <a name="lab-1-working-with-master-pages"></a><span data-ttu-id="338a8-171">랩 1 마스터 페이지 작업</span><span class="sxs-lookup"><span data-stu-id="338a8-171">Lab 1 Working with Master Pages</span></span>

<span data-ttu-id="338a8-172">이 실습에서는 마스터 페이지를 새로 만들고 3 개의 ContentPlaceHolder 컨트롤을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-172">In this lab, you will create a new master page and define three ContentPlaceHolder controls.</span></span> <span data-ttu-id="338a8-173">그런 다음 새 콘텐츠 페이지를 만들고 ContentPlaceHolder 컨트롤 중 하나에서 콘텐츠를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-173">You will then create a new Content page and replace the content from at least one of the ContentPlaceHolder controls.</span></span>

1. <span data-ttu-id="338a8-174">마스터 페이지를 만들고 contentplaceholder를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-174">Create a master page and insert ContentPlaceHolder controls.</span></span> 

    1. <span data-ttu-id="338a8-175">위에서 설명한 대로 마스터 페이지를 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-175">Create a new master page as described above.</span></span>
    2. <span data-ttu-id="338a8-176">기본 ContentPlaceHolder 컨트롤을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-176">Delete the default ContentPlaceHolder control.</span></span>
    3. <span data-ttu-id="338a8-177">각각의 ContentPlaceHolder 컨트롤로 컨트롤의 음영 처리 된 위쪽 테두리를 클릭 하 여 선택한 다음 키보드에서 DEL 키를 눌러 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-177">Select the ContentPlaceHolder control by clicking the shaded top border of the control and then delete it by hitting the DEL key on your keyboard.</span></span>
    4. <span data-ttu-id="338a8-178">사용 하 여 새 테이블을 삽입 합니다 *머리글과 쪽* 그림 3 에서처럼 템플릿.</span><span class="sxs-lookup"><span data-stu-id="338a8-178">Insert a new table using the *Header and side* template as shown in figure 3.</span></span> <span data-ttu-id="338a8-179">전체 테이블 디자이너에 표시 되도록 너비와 높이 90%로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-179">Change the width and height to 90% each so that the entire table is visible in the designer.</span></span>


![](master-pages/_static/image3.jpg)

<span data-ttu-id="338a8-180">**그림 3**</span><span class="sxs-lookup"><span data-stu-id="338a8-180">**Figure 3**</span></span>


1. <span data-ttu-id="338a8-181">테이블의 각 셀에 커서를 놓고 설정 합니다 *valign* 속성을 *위쪽*합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-181">Place the cursor into each cell of the table and set the *valign* property to *top*.</span></span>
2. <span data-ttu-id="338a8-182">도구 상자에서 테이블 (헤더 셀입니다.)의 맨 위 셀에는 각각의 ContentPlaceHolder 컨트롤로 삽입</span><span class="sxs-lookup"><span data-stu-id="338a8-182">From the Toolbox, insert a ContentPlaceHolder control in the top cell of the table (the header cell.)</span></span>
3. <span data-ttu-id="338a8-183">이 각각의 ContentPlaceHolder 컨트롤로 삽입할 때에 행 높이 차지 하는 거의 전체 페이지 그림 4 에서처럼 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-183">When you insert this ContentPlaceHolder control, you will notice that the row height will take up almost the entire page as shown in figure 4.</span></span> <span data-ttu-id="338a8-184">Dont 신경 써야 하는 시점에서.</span><span class="sxs-lookup"><span data-stu-id="338a8-184">Dont be concerned about that at this point.</span></span>


![빈 공간이 ContentPlaceHolder로 같은 셀에서](master-pages/_static/image1.gif)

<span data-ttu-id="338a8-186">**그림 4**: 빈 공간이 ContentPlaceHolder로 같은 셀에서</span><span class="sxs-lookup"><span data-stu-id="338a8-186">**Figure 4**: The empty space is in the same cell as the ContentPlaceHolder</span></span>


1. <span data-ttu-id="338a8-187">다른 두 개의 셀에는 각각의 ContentPlaceHolder 컨트롤로 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-187">Place a ContentPlaceHolder control in the other two cells.</span></span> <span data-ttu-id="338a8-188">다른 ContentPlaceHolder 컨트롤이 삽입 후 테이블 셀의 크기를 짐작할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-188">Once the other ContentPlaceHolder controls have been inserted, the size of the table cells should be as you would expect.</span></span> <span data-ttu-id="338a8-189">페이지에 표시 되는 페이지 다음과 같아집니다 **그림 5**합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-189">The page should now look like the page shown in **figure 5**.</span></span>


![모든 ContentPlaceHolder 컨트롤과 마스터입니다.](master-pages/_static/image2.gif)

<span data-ttu-id="338a8-192">**그림 5**: 모든 ContentPlaceHolder 컨트롤로 마스터입니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-192">**Figure 5**: The Master with all ContentPlaceHolder controls.</span></span> <span data-ttu-id="338a8-193">머리글 셀에 대 한 셀 높이 이제 새로운 것이 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-193">Notice that the cell height for the header cell is now what it should be</span></span>


1. <span data-ttu-id="338a8-194">세 가지 ContentPlaceHolder 컨트롤로 각에 원하는 텍스트를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-194">Enter some text of your choice into each of the three ContentPlaceHolder controls.</span></span>
2. <span data-ttu-id="338a8-195">Exercise1.master로 마스터 페이지를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-195">Save the master page as exercise1.master.</span></span>
3. <span data-ttu-id="338a8-196">새 Web Form을 만들고 exercise1.master 마스터 페이지를 사용 하 여 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-196">Create a new Web Form and associate it with the exercise1.master master page.</span></span>
4. <span data-ttu-id="338a8-197">Visual Studio 2005에서 파일을 새 파일을 선택.</span><span class="sxs-lookup"><span data-stu-id="338a8-197">Select File, New, File in Visual Studio 2005.</span></span>
5. <span data-ttu-id="338a8-198">선택 **Web Form** 새 항목 추가 대화 상자에서.</span><span class="sxs-lookup"><span data-stu-id="338a8-198">Select **Web Form** in the Add New Item dialog.</span></span>
6. <span data-ttu-id="338a8-199">그림 6에에서 표시 된 대로 마스터 페이지 선택 확인란을 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-199">Make sure that the Select master page checkbox is checked as shown in figure 6.</span></span>


![새 콘텐츠 페이지 추가](master-pages/_static/image3.gif)

<span data-ttu-id="338a8-201">**그림 6**: 새 콘텐츠 페이지 추가</span><span class="sxs-lookup"><span data-stu-id="338a8-201">**Figure 6**: Adding a new Content Page</span></span>


1. <span data-ttu-id="338a8-202">추가 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-202">Click Add.</span></span>
2. <span data-ttu-id="338a8-203">선택 exercise1.master 선택에서 마스터 페이지 대화 상자 그림 7 에서처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-203">Select exercise1.master in the Select a master page dialog as shown in figure 7.</span></span>
3. <span data-ttu-id="338a8-204">새 콘텐츠 페이지를 추가 하려면 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-204">Click OK to add the new content page.</span></span>

<span data-ttu-id="338a8-205">새 콘텐츠 페이지는 마스터 페이지에 있는 각 ContentPlaceHolder 컨트롤에 대 한 콘텐츠 컨트롤을 사용 하 여 Visual Studio에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-205">The new content page appears in Visual Studio with one Content control for each ContentPlaceHolder control on the master page.</span></span> <span data-ttu-id="338a8-206">기본적으로 콘텐츠 컨트롤은 빈 사용자 고유의 콘텐츠를 추가할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-206">By default, the Content controls are empty so that you can add your own content.</span></span> <span data-ttu-id="338a8-207">분류 처럼을 마스터 페이지의 ContentPlaceHolder 컨트롤로의 콘텐츠를 사용할 수 있도록 하는 경우 단순히 스마트 태그 기호 (컨트롤의 오른쪽 위 모서리에 있는 작은 검은색 화살표)를 클릭 하 고 선택 *마스터 콘텐츠 기본값으로* 스마트 태그에 표시 된 것 처럼 **그림 8**합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-207">If youd like for them to use the content from the ContentPlaceHolder control on the master page, simply click on the smart tag symbol (the small black arrow in the upper-right corner of the control) and choose *Default to Masters Content* from the smart tag as shown in **figure 8**.</span></span> <span data-ttu-id="338a8-208">이렇게 하면 메뉴 항목으로 변경 *사용자 지정 콘텐츠 만들기*합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-208">When you do so, the menu item changes to *Create Custom Content*.</span></span> <span data-ttu-id="338a8-209">이때 클릭 하는 특정 콘텐츠 컨트롤에 대 한 사용자 지정 콘텐츠를 정의할 수 있도록 마스터 페이지에서 콘텐츠를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-209">Clicking it at that point removes the content from the master page allowing you to define custom content for that particular Content control.</span></span>


![기본적으로 마스터 페이지 콘텐츠를 콘텐츠 컨트롤을 설정 합니다.](master-pages/_static/image4.gif)

<span data-ttu-id="338a8-211">**그림 7**: 콘텐츠 컨트롤을 마스터 페이지 콘텐츠를 기본값으로 설정</span><span class="sxs-lookup"><span data-stu-id="338a8-211">**Figure 7**: Setting a Content Control to Default to the Master Pages Content</span></span>


## <a name="connecting-master-page-and-content-pages"></a><span data-ttu-id="338a8-212">마스터 페이지 및 콘텐츠 페이지 연결</span><span class="sxs-lookup"><span data-stu-id="338a8-212">Connecting Master Page and Content Pages</span></span>

<span data-ttu-id="338a8-213">네 가지 방법 중 하나에서 마스터 페이지 콘텐츠 페이지와의 연결을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-213">The association between a master page and a content page can be configured in one of four different ways:</span></span>

- <span data-ttu-id="338a8-214">합니다 <strong>MasterPageFile</strong> 특성을 @Page 지시문</span><span class="sxs-lookup"><span data-stu-id="338a8-214">The <strong>MasterPageFile</strong> attribute of the @Page directive</span></span>
- <span data-ttu-id="338a8-215">설정 된 **Page.MasterPageFile** 코드에서 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-215">Setting the **Page.MasterPageFile** property in code.</span></span>
- <span data-ttu-id="338a8-216">합니다 **&lt;페이지&gt;** 응용 프로그램 구성 파일 (응용 프로그램의 루트 폴더에 web.config)에서 요소</span><span class="sxs-lookup"><span data-stu-id="338a8-216">The **&lt;pages&gt;** element in the applications configuration file (web.config in the root folder of the application)</span></span>
- <span data-ttu-id="338a8-217">합니다 **&lt;페이지&gt;** 하위 구성 파일 (하위 폴더에 web.config)에서 요소</span><span class="sxs-lookup"><span data-stu-id="338a8-217">The **&lt;pages&gt;** element in a subfolders configuration file (web.config in a subfolder)</span></span>

## <a name="masterpagefile-attribute"></a><span data-ttu-id="338a8-218">MasterPageFile 특성</span><span class="sxs-lookup"><span data-stu-id="338a8-218">MasterPageFile Attribute</span></span>

<span data-ttu-id="338a8-219">MasterPageFile 특성을 사용 하면 쉽게 특정 ASP.NET 페이지에 마스터 페이지를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-219">The MasterPageFile attribute makes it easy to apply a master page to a particular ASP.NET page.</span></span> <span data-ttu-id="338a8-220">선택 하면 마스터 페이지를 적용할 사용 되는 방법 이기도 합니다 **마스터 페이지 선택** 실습 1에서 수행한 것 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-220">It is also the method used to apply the master page when you check the **Select Master Page** checkbox as you did in Exercise 1.</span></span>

## <a name="setting-pagemasterpagefile-in-code"></a><span data-ttu-id="338a8-221">코드에서 Page.MasterPageFile 설정</span><span class="sxs-lookup"><span data-stu-id="338a8-221">Setting Page.MasterPageFile in Code</span></span>

<span data-ttu-id="338a8-222">코드의 MasterPageFile 속성을 설정 하 여 런타임 시 콘텐츠에 특정 마스터 페이지를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-222">By setting the MasterPageFile property in code, you can apply a particular master page to your content at runtime.</span></span> <span data-ttu-id="338a8-223">사용자 역할 또는 기타 일부 조건에 따라 특정 마스터 페이지를 적용 해야 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-223">This is useful in cases where you may need to apply a specific master page based upon a users role or some other criteria.</span></span> <span data-ttu-id="338a8-224">PreInit 메서드에서 MasterPageFile 속성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-224">The MasterPageFile property must be set in the PreInit method.</span></span> <span data-ttu-id="338a8-225">PreInit 메서드 후에 설정 된 경우 InvalidOperationException은 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-225">If it is set after the PreInit method, an InvalidOperationException will be thrown.</span></span> <span data-ttu-id="338a8-226">이 속성을 설정 하는 페이지에 콘텐츠가 있어야 컨트롤을 최상위 컨트롤로 페이지에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-226">The page on which this property is being set must also have a Content control as the top-level control for the page.</span></span> <span data-ttu-id="338a8-227">그렇지 않은 경우는 HttpException MasterPageFile 속성을 설정 하는 경우 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-227">Otherwise an HttpException will be thrown when the MasterPageFile property is set.</span></span>

## <a name="using-the-ltpagesgt-element"></a><span data-ttu-id="338a8-228">사용 하 여 &lt;페이지&gt; 요소</span><span class="sxs-lookup"><span data-stu-id="338a8-228">Using the &lt;pages&gt; Element</span></span>

<span data-ttu-id="338a8-229">MasterPageFile 특성을 설정 하 여 페이지의 마스터 페이지를 구성할 수 있습니다 합니다 &lt;페이지&gt; web.config 파일의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-229">You can configure a master page for your pages by setting the masterPageFile attribute in the &lt;pages&gt; element of the web.config file.</span></span> <span data-ttu-id="338a8-230">이 메서드를 사용 하면 응용 프로그램 구조에서 하위 web.config 파일에이 설정을 재정의할 수는 염두에서에 둡니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-230">When using this method, keep in mind that web.config files lower in the application structure can override this setting.</span></span> <span data-ttu-id="338a8-231">설정 MasterPageFile 특성을 @Page 지시문은이 설정을 재정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-231">Any MasterPageFile attribute set in a @Page directive will also override this setting.</span></span> <span data-ttu-id="338a8-232">사용 하는 &lt;페이지&gt; 요소를 사용 하면 간단 하 게 만들를 <em>마스터</em> 특정 폴더 또는 파일에서 필요한 경우 재정의할 수 있는 마스터 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-232">Using the &lt;pages&gt; element makes it simple to create a <em>master</em> master page that can be overridden if necessary in particular folders or files.</span></span>

## <a name="properties-in-master-pages"></a><span data-ttu-id="338a8-233">마스터 페이지의 속성</span><span class="sxs-lookup"><span data-stu-id="338a8-233">Properties in Master Pages</span></span>

<span data-ttu-id="338a8-234">마스터 페이지는 간단 하 게 속성만 마스터 페이지 내에서 공용 속성을 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-234">A master page can expose properties by simply making those properties public within the master page.</span></span> <span data-ttu-id="338a8-235">예를 들어, 다음 코드는 SomeProperty 라는 속성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-235">For example, the following code defines a property called SomeProperty:</span></span>

[!code-csharp[Main](master-pages/samples/sample2.cs)]

<span data-ttu-id="338a8-236">마스터를 사용 해야 SomeProperty 속성에서 콘텐츠 페이지에 액세스 하려면 다음과 같이 속성:</span><span class="sxs-lookup"><span data-stu-id="338a8-236">To access the SomeProperty property from the Content page, you will need to use the Master property like so:</span></span>

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a><span data-ttu-id="338a8-237">중첩 마스터 페이지</span><span class="sxs-lookup"><span data-stu-id="338a8-237">Nesting Master Pages</span></span>

<span data-ttu-id="338a8-238">마스터 페이지는 대규모 웹 응용 프로그램에서 일반적인 모양 및 느낌을 위한 완벽 한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-238">Master pages are the perfect solution for ensuring a common look and feel across a large Web application.</span></span> <span data-ttu-id="338a8-239">그러나 다른 부분에는 다른 인터페이스를 공유 하는 동안 대규모 사이트 공유 공용 인터페이스의 특정 부분을 해야 일반적이 지 않은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-239">However, it's not uncommon to have certain parts of a large site share a common interface while other parts share a different interface.</span></span> <span data-ttu-id="338a8-240">해당 요구를 해결 하기 위해 여러 마스터 페이지는는 완벽 한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-240">To address that need, multiple master pages are the perfect solution.</span></span> <span data-ttu-id="338a8-241">그러나 여전히 해당 사이트의 특정 섹션 간에 공유 되는 다른 구성 요소 및 특정 구성 요소 (예: 예를 들어 메뉴) 모든 페이지 간에 공유 되는 대형 응용 프로그램에 있을 팩트를 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-241">However, that still doesn't address the fact that a large application may have certain components (such as a menu, for example) that are shared among all pages and other components that are shared only among certain sections of the site.</span></span> <span data-ttu-id="338a8-242">이러한 상황을 중첩 된 마스터 페이지 필요 원활 하 게 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-242">For that type of situation, nested master pages fill the need nicely.</span></span> <span data-ttu-id="338a8-243">지금까지 살펴본 대로 기본 마스터 페이지는 마스터 페이지 콘텐츠 페이지의 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-243">As you've seen, a normal master page consists of a master page and a content page.</span></span> <span data-ttu-id="338a8-244">중첩된 마스터 페이지를 사용 하는 경우에는 두 마스터 페이지 부모 마스터 및 자식 master입니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-244">In a nested master page situation, there are two master pages; a parent master and a child master.</span></span> <span data-ttu-id="338a8-245">자식 마스터 페이지는 콘텐츠 페이지 및 마스터 부모 마스터 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-245">The child master page is also a content page and its master is the parent master page.</span></span>

<span data-ttu-id="338a8-246">일반적인 마스터 페이지에 대 한 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-246">Here is the code for a typical master page:</span></span>

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

<span data-ttu-id="338a8-247">중첩된 된 마스터 시나리오에서 부모 master가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-247">In a nested master scenario, this would be the parent master.</span></span> <span data-ttu-id="338a8-248">다른 마스터 페이지가이 페이지를 사용 하 여 해당 마스터 페이지는 하 고 해당 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-248">Another master page would use this page as its master page, and that code would look like this:</span></span>

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

<span data-ttu-id="338a8-249">이 시나리오에서, 자식 마스터의 부모 마스터에 대 한 콘텐츠 페이지 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-249">Note that in this scenario, the child master is also a content page for the parent master.</span></span> <span data-ttu-id="338a8-250">모든 자식 마스터의 콘텐츠를 콘텐츠 컨트롤 부모의 각각의 ContentPlaceHolder 컨트롤로에서 해당 콘텐츠를 가져오는 내부 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-250">All of the child master's content appears inside of a Content control that gets its content from the parent's ContentPlaceHolder control.</span></span>

> [!NOTE]
> <span data-ttu-id="338a8-251">디자이너 지원에 중첩 된 마스터 페이지에 대해 사용할 수 없는 경우</span><span class="sxs-lookup"><span data-stu-id="338a8-251">Designer support is not available for nested master pages.</span></span> <span data-ttu-id="338a8-252">중첩 된 마스터를 사용 하 여를 개발 하는 경우 소스 뷰를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-252">When you are developing using nested masters, you will need to use source view.</span></span>


<span data-ttu-id="338a8-253">이 비디오 연습은 중첩된 마스터 페이지를 사용 하 여 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-253">This video shows a walkthrough of using nested master pages.</span></span>


![](master-pages/_static/image1.png)


[<span data-ttu-id="338a8-254">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="338a8-254">Open Full-Screen Video</span></span>](master-pages/_static/nested1.wmv)


![마스터 페이지를 선택합니다.](master-pages/_static/image4.jpg)

<span data-ttu-id="338a8-256">**그림 8**: 마스터 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="338a8-256">**Figure 8**: Selecting a Master Page</span></span>
