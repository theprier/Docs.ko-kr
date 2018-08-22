---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
title: 클라이언트 코드 (C#)에서 DropShadow 속성 조작 | Microsoft Docs
author: wenz
description: DataList의 편집 인터페이스 사용자 지정
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c83ca3e6-c0bf-4158-a166-40c1ab0f33da
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
msc.type: authoredcontent
ms.openlocfilehash: f751e2378621a6ab74f9f15fe51fd18bdd8b4070
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831535"
---
<a name="manipulating-dropshadow-properties-from-client-code-c"></a><span data-ttu-id="c3c60-103">클라이언트 코드 (C#)에서 DropShadow 속성 조작</span><span class="sxs-lookup"><span data-stu-id="c3c60-103">Manipulating DropShadow Properties from Client Code (C#)</span></span>
====================
<span data-ttu-id="c3c60-104">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="c3c60-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c3c60-105">[코드를 다운로드](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="c3c60-105">[Download Code](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2CS.pdf)</span></span>

> <span data-ttu-id="c3c60-106">AJAX Control Toolkit에서 DropShadow 컨트롤 그림자를 사용 하 여 패널을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c60-106">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="c3c60-107">이 extender의 속성 클라이언트 JavaScript 코드를 사용 하 여 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c60-107">Properties of this extender can also be changed using client JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="c3c60-108">개요</span><span class="sxs-lookup"><span data-stu-id="c3c60-108">Overview</span></span>

<span data-ttu-id="c3c60-109">AJAX Control Toolkit에서 DropShadow 컨트롤 그림자를 사용 하 여 패널을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c60-109">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="c3c60-110">이 extender의 속성 클라이언트 JavaScript 코드를 사용 하 여 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3c60-110">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="c3c60-111">단계</span><span class="sxs-lookup"><span data-stu-id="c3c60-111">Steps</span></span>

<span data-ttu-id="c3c60-112">코드 몇 줄의 텍스트가 포함 된 패널을 사용 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c60-112">The code starts with a panel containing some lines of text:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample1.aspx)]

<span data-ttu-id="c3c60-113">연결된 된 CSS 클래스는 훌륭한 배경 색을 패널을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c60-113">The associated CSS class gives the panel a nice background color:</span></span>

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample2.css)]

<span data-ttu-id="c3c60-114">`DropShadowExtender` 그림자 효과 50%로 설정 하는 불투명도 사용 하 여 패널을 확장에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3c60-114">The `DropShadowExtender` is added to extend the panel with a drop shadow effect, opacity set to 50%:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample3.aspx)]

<span data-ttu-id="c3c60-115">그런 다음 ASP.NET AJAX `ScriptManager` 제어 하려면 컨트롤 도구 키트를 사용 하면:</span><span class="sxs-lookup"><span data-stu-id="c3c60-115">Then, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample4.aspx)]

<span data-ttu-id="c3c60-116">그림자의 불투명도 설정 하는 것에 대 한 두 개의 JavaScript 링크를 포함 하는 다른 패널: 빼기 링크 그림자의 불투명도 감소, 더하기 링크를 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="c3c60-116">Another panel contains two JavaScript links for setting the opacity of the drop shadow: the minus link decreases the shadow's opacity, the plus link increases it.</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample5.aspx)]

<span data-ttu-id="c3c60-117">JavaScript 함수 `changeOpacity()` 먼저 찾아야 다음는 `DropShadowExtender` 페이지의 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="c3c60-117">The JavaScript function `changeOpacity()` must then first find the `DropShadowExtender` control on the page.</span></span> <span data-ttu-id="c3c60-118">ASP.NET AJAX 정의 `$find()` 정확 하 게 해당 작업에 대 한 메서드.</span><span class="sxs-lookup"><span data-stu-id="c3c60-118">ASP.NET AJAX defines the `$find()` method for exactly that task.</span></span> <span data-ttu-id="c3c60-119">그런 다음, `get_Opacity()` 현재 불투명도 검색 하는 메서드를 `set_Opacity()` 메서드 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3c60-119">Then, the `get_Opacity()` method retrieves the current opacity, the `set_Opacity()` method sets it.</span></span> <span data-ttu-id="c3c60-120">다음 JavaScript 코드의 현재 불투명도 값을 배치 합니다 `<label>` 요소:</span><span class="sxs-lookup"><span data-stu-id="c3c60-120">The JavaScript code then puts the current opacity value in the `<label>` element:</span></span>

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample6.html)]


<span data-ttu-id="c3c60-121">[![클라이언트 쪽에서 변경 되는 불투명도](manipulating-dropshadow-properties-from-client-code-cs/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c3c60-121">[![The opacity is changed on the client side](manipulating-dropshadow-properties-from-client-code-cs/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="c3c60-122">클라이언트 쪽에서 변경 되는 불투명도 ([클릭 하 여 큰 이미지 보기](manipulating-dropshadow-properties-from-client-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="c3c60-122">The opacity is changed on the client side ([Click to view full-size image](manipulating-dropshadow-properties-from-client-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c3c60-123">[이전](adjusting-the-z-index-of-a-dropshadow-cs.md)
> [다음](adjusting-the-z-index-of-a-dropshadow-vb.md)</span><span class="sxs-lookup"><span data-stu-id="c3c60-123">[Previous](adjusting-the-z-index-of-a-dropshadow-cs.md)
[Next](adjusting-the-z-index-of-a-dropshadow-vb.md)</span></span>
