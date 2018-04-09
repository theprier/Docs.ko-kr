---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
title: 클라이언트 코드 (VB)에서 DropShadow 속성 조작 | Microsoft Docs
author: wenz
description: 들어의 DropShadow 컨트롤 그림자가 있는 패널을 확장합니다. 이 extender 속성 JavaScrip 클라이언트를 사용 하 여 변경할 수 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 11be4211-2fb9-4e15-b6d4-2aa623d81f3e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
msc.type: authoredcontent
ms.openlocfilehash: b5b024811ea511e67ce180169de9f0b7e3ef51d9
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="manipulating-dropshadow-properties-from-client-code-vb"></a><span data-ttu-id="fe54a-104">클라이언트 코드 (VB)에서 DropShadow 속성 조작</span><span class="sxs-lookup"><span data-stu-id="fe54a-104">Manipulating DropShadow Properties from Client Code (VB)</span></span>
====================
<span data-ttu-id="fe54a-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="fe54a-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="fe54a-106">[코드를 다운로드](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="fe54a-106">[Download Code](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)</span></span>

> <span data-ttu-id="fe54a-107">들어의 DropShadow 컨트롤 그림자가 있는 패널을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="fe54a-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="fe54a-108">클라이언트 JavaScript 코드를 사용 하 여이 extender의 속성을 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe54a-108">Properties of this extender can also be changed using client JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="fe54a-109">개요</span><span class="sxs-lookup"><span data-stu-id="fe54a-109">Overview</span></span>

<span data-ttu-id="fe54a-110">들어의 DropShadow 컨트롤 그림자가 있는 패널을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="fe54a-110">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="fe54a-111">클라이언트 JavaScript 코드를 사용 하 여이 extender의 속성을 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe54a-111">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="fe54a-112">단계</span><span class="sxs-lookup"><span data-stu-id="fe54a-112">Steps</span></span>

<span data-ttu-id="fe54a-113">코드 몇 줄의 텍스트가 포함 된 패널으로 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe54a-113">The code starts with a panel containing some lines of text:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample1.aspx)]

<span data-ttu-id="fe54a-114">연결 된 CSS 클래스 좋은 배경색 패널을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fe54a-114">The associated CSS class gives the panel a nice background color:</span></span>

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample2.css)]

<span data-ttu-id="fe54a-115">`DropShadowExtender` 그림자 효과 불투명도 50%로 설정 된 패널을 확장에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe54a-115">The `DropShadowExtender` is added to extend the panel with a drop shadow effect, opacity set to 50%:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample3.aspx)]

<span data-ttu-id="fe54a-116">그런 다음 ASP.NET AJAX `ScriptManager` 컨트롤을 사용 하면 제어 도구 키트에서 실행 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe54a-116">Then, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample4.aspx)]

<span data-ttu-id="fe54a-117">그림자의 불투명도 설정 하기 위한 두 개의 JavaScript 링크를 포함 하는 다른 패널: 빼기 링크 그림자의 불투명도 감소, 더하기 링크 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="fe54a-117">Another panel contains two JavaScript links for setting the opacity of the drop shadow: the minus link decreases the shadow's opacity, the plus link increases it.</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample5.aspx)]

<span data-ttu-id="fe54a-118">JavaScript 함수 `changeOpacity()` 다음 먼저 찾아야는 `DropShadowExtender` 페이지에 있는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="fe54a-118">The JavaScript function `changeOpacity()` must then first find the `DropShadowExtender` control on the page.</span></span> <span data-ttu-id="fe54a-119">ASP.NET AJAX 정의 `$find()` 정확 하 게 해당 작업에 대 한 메서드.</span><span class="sxs-lookup"><span data-stu-id="fe54a-119">ASP.NET AJAX defines the `$find()` method for exactly that task.</span></span> <span data-ttu-id="fe54a-120">그런 다음 `get_Opacity()` 메서드 검색 현재 불투명도 `set_Opacity()` 설정 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="fe54a-120">Then, the `get_Opacity()` method retrieves the current opacity, the `set_Opacity()` method sets it.</span></span> <span data-ttu-id="fe54a-121">다음 JavaScript 코드에 현재 불투명 값을 놓입니다는 `<label>` 요소:</span><span class="sxs-lookup"><span data-stu-id="fe54a-121">The JavaScript code then puts the current opacity value in the `<label>` element:</span></span>

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample6.html)]


<span data-ttu-id="fe54a-122">[![클라이언트 쪽에서 변경 되는 불투명도](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fe54a-122">[![The opacity is changed on the client side](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="fe54a-123">클라이언트 쪽에서 변경 되는 불투명도 ([전체 크기 이미지를 보려면 클릭](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="fe54a-123">The opacity is changed on the client side ([Click to view full-size image](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="fe54a-124">이전</span><span class="sxs-lookup"><span data-stu-id="fe54a-124">Previous</span></span>](adjusting-the-z-index-of-a-dropshadow-vb.md)
