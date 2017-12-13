---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
title: "아코디언 창 (C#)를 동적으로 추가 | Microsoft Docs"
author: wenz
description: "들어에서 Accordion 컨트롤 여러 창을 하며 한 번에 둘 중 하나를 표시할 수 있습니다. 일반적으로 패널 w 선언 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 66d88cfa-f26f-46b1-ad52-1c9e03c04a48
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-cs
msc.type: authoredcontent
ms.openlocfilehash: 1c6af79186ca21082647beec500c47974a47c35a
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="dynamically-adding-an-accordion-pane-c"></a><span data-ttu-id="37b43-104">동적으로 추가 하는 아코디언 창 (C#)</span><span class="sxs-lookup"><span data-stu-id="37b43-104">Dynamically Adding An Accordion Pane (C#)</span></span>
====================
<span data-ttu-id="37b43-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="37b43-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="37b43-106">[코드를 다운로드](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="37b43-106">[Download Code](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2CS.pdf)</span></span>

> <span data-ttu-id="37b43-107">들어에서 Accordion 컨트롤 여러 창을 하며 한 번에 둘 중 하나를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b43-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="37b43-108">패널은 페이지 자체 내에서 일반적으로 선언 하지만 서버 쪽 코드는 동일한 결과 만드는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b43-108">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>


## <a name="overview"></a><span data-ttu-id="37b43-109">개요</span><span class="sxs-lookup"><span data-stu-id="37b43-109">Overview</span></span>

<span data-ttu-id="37b43-110">들어에서 Accordion 컨트롤 여러 창을 하며 한 번에 둘 중 하나를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b43-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="37b43-111">패널은 페이지 자체 내에서 일반적으로 선언 하지만 서버 쪽 코드는 동일한 결과 만드는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b43-111">Panels are usually declared within the page itself, but server-side code can be used to achieve the same result.</span></span>

## <a name="steps"></a><span data-ttu-id="37b43-112">단계</span><span class="sxs-lookup"><span data-stu-id="37b43-112">Steps</span></span>

<span data-ttu-id="37b43-113">Accordion 컨트롤 서버 쪽 코드에 모든 중요 한 속성을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b43-113">The Accordion control exposes all important properties to server-side code.</span></span> <span data-ttu-id="37b43-114">무엇 보다도 `Panes` 속성은 Accordion 구성 하는 창 컬렉션에 대 한 액세스 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b43-114">Among other things, the `Panes` property grants access to the collection of panes that make up the Accordion.</span></span> <span data-ttu-id="37b43-115">모든 창 없는 형식의 `AccordionPane`합니다.</span><span class="sxs-lookup"><span data-stu-id="37b43-115">Every pane there is of type `AccordionPane`.</span></span> <span data-ttu-id="37b43-116">따라서 이러한 창을 만드는 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="37b43-116">It is therefore trivial to create such a pane:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample1.cs)]

<span data-ttu-id="37b43-117">`HeaderContainer` 속성 `AccordionPane` 창의; 헤더 섹션 내의 ASP.NET 컨트롤에 대 한 액세스를 제공는 `ContentContainer` 속성 `AccordionPane` 창의 콘텐츠 섹션에 대 한 동일한 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b43-117">The `HeaderContainer` property of `AccordionPane` provides access to the ASP.NET controls within the header section of the pane; the `ContentContainer` property of `AccordionPane` does the same for the content section of the pane.</span></span> <span data-ttu-id="37b43-118">이 ASP.NET 코드를 창에 콘텐츠를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37b43-118">This allows ASP.NET code to add content to the panes:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample2.cs)]

<span data-ttu-id="37b43-119">에 pane(s) 마지막으로 추가 해야는 `Panes` 는 Accordion의 컬렉션:</span><span class="sxs-lookup"><span data-stu-id="37b43-119">Finally, the pane(s) must be added to the `Panes` collection of the Accordion:</span></span>

[!code-csharp[Main](dynamically-adding-an-accordion-pane-cs/samples/sample3.cs)]

<span data-ttu-id="37b43-120">두 개의 창이 Accordion 컨트롤을 추가 하는 전체 서버 쪽 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="37b43-120">Here is a complete server-side code that adds two panes to an Accordion control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample4.aspx)]

<span data-ttu-id="37b43-121">유일한 누락 된 요소는 ASP.NET의 유무에 따라 달라 지는 자체 Accordion `ScriptManager` 제어:</span><span class="sxs-lookup"><span data-stu-id="37b43-121">The only missing element is the Accordion itself, which depends on the presence of the ASP.NET `ScriptManager` control:</span></span>

[!code-aspx[Main](dynamically-adding-an-accordion-pane-cs/samples/sample5.aspx)]

<span data-ttu-id="37b43-122">이 예제에서는 끝나기를 Accordion 컨트롤에서 참조 하는 두 개의 CSS 클래스는 브라우저에 대 한 스타일 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="37b43-122">To finish the example, the two CSS classes referenced in the Accordion control provide style information for the browser:</span></span>

[!code-css[Main](dynamically-adding-an-accordion-pane-cs/samples/sample6.css)]


<span data-ttu-id="37b43-123">[![서버 쪽 코드에 의해 동적으로 추가한는 accordion의 데이터](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="37b43-123">[![The data in the accordion was dynamically added by server-side code](dynamically-adding-an-accordion-pane-cs/_static/image2.png)](dynamically-adding-an-accordion-pane-cs/_static/image1.png)</span></span>

<span data-ttu-id="37b43-124">accordion의 데이터를 서버 쪽 코드에 의해 동적으로 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](dynamically-adding-an-accordion-pane-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="37b43-124">The data in the accordion was dynamically added by server-side code ([Click to view full-size image](dynamically-adding-an-accordion-pane-cs/_static/image3.png))</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="37b43-125">[이전](databinding-to-an-accordion-cs.md)
[다음](databinding-to-an-accordion-vb.md)</span><span class="sxs-lookup"><span data-stu-id="37b43-125">[Previous](databinding-to-an-accordion-cs.md)
[Next](databinding-to-an-accordion-vb.md)</span></span>
