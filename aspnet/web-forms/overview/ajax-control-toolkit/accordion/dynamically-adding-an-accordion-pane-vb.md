---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-vb
title: 동적으로 Accordion 창 (VB)를 추가 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 Accordion 컨트롤 여러 창을 제공 하 고 둘 중 한 번에 표시할 수 있습니다. 일반적으로 패널 w 선언 하는 중...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: fae968c9-1902-487d-b053-86a46dd52c3f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-vb
msc.type: authoredcontent
ms.openlocfilehash: 1fdb95ee1ee93bc011a257e4e21c876dbbc7d2a9
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37820028"
---
<a name="dynamically-adding-an-accordion-pane-vb"></a><span data-ttu-id="fa006-104">동적으로 Accordion 창 (VB)를 추가</span><span class="sxs-lookup"><span data-stu-id="fa006-104">Dynamically Adding An Accordion Pane (VB)</span></span>
====================
<span data-ttu-id="fa006-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="fa006-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="fa006-106">[코드를 다운로드](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="fa006-106">[Download Code](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2VB.pdf)</span></span>

> <span data-ttu-id="fa006-107">AJAX Control Toolkit의 Accordion 컨트롤 여러 창을 제공 하 고 둘 중 한 번에 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa006-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="fa006-108">패널은 일반적으로 페이지 자체 내에서 선언 하지만 서버 쪽 코드를 사용 하 여 동일한 결과 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa006-108">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>


## <a name="overview"></a><span data-ttu-id="fa006-109">개요</span><span class="sxs-lookup"><span data-stu-id="fa006-109">Overview</span></span>

<span data-ttu-id="fa006-110">AJAX Control Toolkit의 Accordion 컨트롤 여러 창을 제공 하 고 둘 중 한 번에 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa006-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="fa006-111">패널은 일반적으로 페이지 자체 내에서 선언 하지만 서버 쪽 코드를 사용 하 여 동일한 결과 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa006-111">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="steps"></a><span data-ttu-id="fa006-112">단계</span><span class="sxs-lookup"><span data-stu-id="fa006-112">Steps</span></span>

<span data-ttu-id="fa006-113">Accordion 컨트롤 서버 쪽 코드에 모든 중요 한 속성을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa006-113">The Accordion control exposes all important properties to server-side code.</span></span> <span data-ttu-id="fa006-114">무엇 보다도 `Panes` 속성은 Accordion을 구성 하는 창의 컬렉션에 대 한 액세스 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa006-114">Among other things, the `Panes` property grants access to the collection of panes that make up the Accordion.</span></span> <span data-ttu-id="fa006-115">형식의 모든 창 `AccordionPane`합니다.</span><span class="sxs-lookup"><span data-stu-id="fa006-115">Every pane there is of type `AccordionPane`.</span></span> <span data-ttu-id="fa006-116">따라서 이러한 창을 만드는 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa006-116">It is therefore trivial to create such a pane:</span></span>

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample1.vb)]

<span data-ttu-id="fa006-117">`HeaderContainer` 의 속성 `AccordionPane` ; 창의 헤더 섹션 내에 있는 ASP.NET 컨트롤에 대 한 액세스를 제공 합니다 `ContentContainer` 의 속성 `AccordionPane` 창의 콘텐츠 섹션에 대 한 동일한 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa006-117">The `HeaderContainer` property of `AccordionPane` provides access to the ASP.NET controls within the header section of the pane; the `ContentContainer` property of `AccordionPane` does the same for the content section of the pane.</span></span> <span data-ttu-id="fa006-118">이 ASP.NET 코드를 창에 내용을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa006-118">This allows ASP.NET code to add content to the panes:</span></span>

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample2.vb)]

<span data-ttu-id="fa006-119">마지막으로 pane(s) 추가 해야 합니다는 `Panes` 는 Accordion 컬렉션:</span><span class="sxs-lookup"><span data-stu-id="fa006-119">Finally, the pane(s) must be added to the `Panes` collection of the Accordion:</span></span>

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample3.vb)]

<span data-ttu-id="fa006-120">두 개의 창이 Accordion 컨트롤에 추가 하는 전체 서버 쪽 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fa006-120">Here is a complete server-side code that adds two panes to an Accordion control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-vb/samples/sample4.aspx)]

<span data-ttu-id="fa006-121">누락 된 유일한 요소는 ASP.NET의 유무에 따라 달라 지는 자체 Accordion `ScriptManager` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa006-121">The only missing element is the Accordion itself, which depends on the presence of the ASP.NET `ScriptManager` control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-vb/samples/sample5.aspx)]

<span data-ttu-id="fa006-122">Accordion 컨트롤에서 참조 하는 두 개의 CSS 클래스 예제를 완료 하려면 브라우저에 대 한 스타일 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa006-122">To finish the example, the two CSS classes referenced in the Accordion control provide style information for the browser:</span></span>

[!code-css[Main](dynamically-adding-an-accordion-pane-vb/samples/sample6.css)]


<span data-ttu-id="fa006-123">[![accordion에 데이터를 서버 쪽 코드에서 동적으로 추가](dynamically-adding-an-accordion-pane-vb/_static/image2.png)](dynamically-adding-an-accordion-pane-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fa006-123">[![The data in the accordion was dynamically added by server-side code](dynamically-adding-an-accordion-pane-vb/_static/image2.png)](dynamically-adding-an-accordion-pane-vb/_static/image1.png)</span></span>

<span data-ttu-id="fa006-124">서버 쪽 코드에서 동적으로 추가한는 accordion에 데이터 ([클릭 하 여 큰 이미지 보기](dynamically-adding-an-accordion-pane-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="fa006-124">The data in the accordion was dynamically added by server-side code ([Click to view full-size image](dynamically-adding-an-accordion-pane-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="fa006-125">이전</span><span class="sxs-lookup"><span data-stu-id="fa006-125">Previous</span></span>](databinding-to-an-accordion-vb.md)
