---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
title: 서버 쪽 (VB)에서 애니메이션 수정 | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 애니메이션 있을 수 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: addcf4aa-340a-460b-9c64-506424a1f725
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
msc.type: authoredcontent
ms.openlocfilehash: 2b9ce85fc5040b2318233b3c553c2cf53dd03555
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="modifying-animations-from-the-server-side-vb"></a><span data-ttu-id="b269f-104">서버 쪽 (VB)에서 애니메이션 수정</span><span class="sxs-lookup"><span data-stu-id="b269f-104">Modifying Animations From The Server Side (VB)</span></span>
====================
<span data-ttu-id="b269f-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="b269f-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b269f-106">[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="b269f-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)</span></span>

> <span data-ttu-id="b269f-107">ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="b269f-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="b269f-108">애니메이션 서버 쪽에도 변경 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b269f-108">The animations may also be changed on the server-side</span></span>


## <a name="overview"></a><span data-ttu-id="b269f-109">개요</span><span class="sxs-lookup"><span data-stu-id="b269f-109">Overview</span></span>

<span data-ttu-id="b269f-110">ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="b269f-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="b269f-111">애니메이션 서버 쪽에도 변경 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b269f-111">The animations may also be changed on the server-side</span></span>

## <a name="steps"></a><span data-ttu-id="b269f-112">단계</span><span class="sxs-lookup"><span data-stu-id="b269f-112">Steps</span></span>

<span data-ttu-id="b269f-113">우선, 포함 된 `ScriptManager` 페이지; 그런 다음 ASP.NET AJAX 라이브러리 로드 되는 제어 도구 키트를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="b269f-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample1.aspx)]

<span data-ttu-id="b269f-114">그러면 다음과 같은 텍스트의 패널에 애니메이션 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b269f-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample2.aspx)]

<span data-ttu-id="b269f-115">패널에 대 한 연결 된 CSS 클래스 좋은 배경색을 정의 하 고도 패널 고정된 폭을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b269f-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](modifying-animations-from-the-server-side-vb/samples/sample3.css)]

<span data-ttu-id="b269f-116">코드의 나머지 서버 쪽에서 실행 되 고 태그; 사용 하지 않습니다. 대신, 사용 하 여 코드를 만드는 `AnimationExtender` 제어:</span><span class="sxs-lookup"><span data-stu-id="b269f-116">The rest of the code runs on the server-side and does not use markup; instead, it uses code to create the `AnimationExtender` control:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample4.aspx)]

<span data-ttu-id="b269f-117">그러나 컨트롤 Toolkit 현재 제공 하지 않습니다 개별 애니메이션 만들기에 대 한 API 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="b269f-117">However, the Control Toolkit currently does not provide an API access to create the individual animations.</span></span> <span data-ttu-id="b269f-118">그러나 설정 하 고는 `AnimationExtender`의 애니메이션 속성을 문자열로 애니메이션을 선언적으로 지정할 때 사용 되는 XML 태그를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b269f-118">It is however possible to set the `AnimationExtender`'s Animations property to a string containing the XML markup used when assigning the animations declaratively.</span></span> <span data-ttu-id="b269f-119">포함 되지 않아야 하는 XML을 만들기 위해는 `<Animations>` 요소는.NET Framework의 XML을 사용할 수 있습니다 지원 하거나, 다음 코드 에서처럼 방금 제공 된 문자열:</span><span class="sxs-lookup"><span data-stu-id="b269f-119">In order to create the XML which must not contain the `<Animations>` element you could use the .NET Framework's XML support or, as in the following code, just provide the string:</span></span>

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample5.vb)]

<span data-ttu-id="b269f-120">마지막으로 추가 된 `AnimationExtender` 내 컨트롤을 현재 페이지는 `<form runat="server">` 애니메이션 포함 되어 있고 실행 요소:</span><span class="sxs-lookup"><span data-stu-id="b269f-120">Finally, add the `AnimationExtender` control to the current page, within the `<form runat="server">` element, making sure that the animation is included and runs:</span></span>

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample6.vb)]


<span data-ttu-id="b269f-121">[![C# /VB 서버 쪽 코드를 사용 하 여 애니메이션이 만들어집니다.](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b269f-121">[![The animation is created using server-side C#/VB code](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)</span></span>

<span data-ttu-id="b269f-122">C# /VB 서버 쪽 코드를 사용 하 여 애니메이션 만들어집니다 ([전체 크기 이미지를 보려면 클릭](modifying-animations-from-the-server-side-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="b269f-122">The animation is created using server-side C#/VB code ([Click to view full-size image](modifying-animations-from-the-server-side-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b269f-123">[이전](triggering-an-animation-in-another-control-vb.md)
> [다음](executing-animations-using-client-side-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="b269f-123">[Previous](triggering-an-animation-in-another-control-vb.md)
[Next](executing-animations-using-client-side-code-vb.md)</span></span>
