---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
title: 서버 쪽 (VB)에서 애니메이션 수정 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 애니메이션 있을 수 있습니다...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: addcf4aa-340a-460b-9c64-506424a1f725
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
msc.type: authoredcontent
ms.openlocfilehash: 5ff8685b44e7d0c2261ea7b9f1ca6397ae05ce53
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37811168"
---
<a name="modifying-animations-from-the-server-side-vb"></a><span data-ttu-id="7f6d1-104">서버 쪽 (VB)에서 애니메이션 수정</span><span class="sxs-lookup"><span data-stu-id="7f6d1-104">Modifying Animations From The Server Side (VB)</span></span>
====================
<span data-ttu-id="7f6d1-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="7f6d1-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7f6d1-106">[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="7f6d1-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)</span></span>

> <span data-ttu-id="7f6d1-107">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7f6d1-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="7f6d1-108">서버 쪽에서 애니메이션 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f6d1-108">The animations may also be changed on the server-side</span></span>


## <a name="overview"></a><span data-ttu-id="7f6d1-109">개요</span><span class="sxs-lookup"><span data-stu-id="7f6d1-109">Overview</span></span>

<span data-ttu-id="7f6d1-110">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7f6d1-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="7f6d1-111">서버 쪽에서 애니메이션 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f6d1-111">The animations may also be changed on the server-side</span></span>

## <a name="steps"></a><span data-ttu-id="7f6d1-112">단계</span><span class="sxs-lookup"><span data-stu-id="7f6d1-112">Steps</span></span>

<span data-ttu-id="7f6d1-113">첫째, 포함 된 `ScriptManager` 페이지 그런 다음 ASP.NET AJAX 라이브러리 로드 되 면 컨트롤 도구 키트를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="7f6d1-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample1.aspx)]

<span data-ttu-id="7f6d1-114">그러면 다음과 같은 텍스트 패널에 애니메이션 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f6d1-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample2.aspx)]

<span data-ttu-id="7f6d1-115">패널에 대 한 연결 된 CSS 클래스에 유용한 배경 색을 정의 하 고 패널 고정된 너비를 설정할 수도:</span><span class="sxs-lookup"><span data-stu-id="7f6d1-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](modifying-animations-from-the-server-side-vb/samples/sample3.css)]

<span data-ttu-id="7f6d1-116">코드의 나머지 서버 쪽에서 실행 되 고 태그;를 사용 하지 않습니다. 대신 사용 하 여 코드 만들기는 `AnimationExtender` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6d1-116">The rest of the code runs on the server-side and does not use markup; instead, it uses code to create the `AnimationExtender` control:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample4.aspx)]

<span data-ttu-id="7f6d1-117">그러나 Control Toolkit 현재 제공 하지 않습니다 개별 애니메이션 만들기에 대 한 API 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f6d1-117">However, the Control Toolkit currently does not provide an API access to create the individual animations.</span></span> <span data-ttu-id="7f6d1-118">하지만 설정할 수는 `AnimationExtender`의 애니메이션 속성 문자열을 포함 하는 애니메이션을 선언적으로 할당할 때 사용 되는 XML 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="7f6d1-118">It is however possible to set the `AnimationExtender`'s Animations property to a string containing the XML markup used when assigning the animations declaratively.</span></span> <span data-ttu-id="7f6d1-119">없어야 하는 XML을 만들기 위해는 `<Animations>` .NET Framework의 XML을 사용할 수 있습니다 지원 요소나, 다음 코드와 같이 문자열을 제공 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f6d1-119">In order to create the XML which must not contain the `<Animations>` element you could use the .NET Framework's XML support or, as in the following code, just provide the string:</span></span>

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample5.vb)]

<span data-ttu-id="7f6d1-120">마지막으로 추가 합니다 `AnimationExtender` 내 현재 페이지로 컨트롤을 `<form runat="server">` 요소에 애니메이션이 포함 되며 실행 되었는지:</span><span class="sxs-lookup"><span data-stu-id="7f6d1-120">Finally, add the `AnimationExtender` control to the current page, within the `<form runat="server">` element, making sure that the animation is included and runs:</span></span>

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample6.vb)]


<span data-ttu-id="7f6d1-121">[![서버 쪽 C# /VB 코드를 사용 하 여 애니메이션이 만들어집니다.](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7f6d1-121">[![The animation is created using server-side C#/VB code](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)</span></span>

<span data-ttu-id="7f6d1-122">애니메이션은 서버 쪽 C# /VB 코드를 사용 하 여 생성 됩니다 ([클릭 하 여 큰 이미지 보기](modifying-animations-from-the-server-side-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="7f6d1-122">The animation is created using server-side C#/VB code ([Click to view full-size image](modifying-animations-from-the-server-side-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7f6d1-123">[이전](triggering-an-animation-in-another-control-vb.md)
> [다음](executing-animations-using-client-side-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7f6d1-123">[Previous](triggering-an-animation-in-another-control-vb.md)
[Next](executing-animations-using-client-side-code-vb.md)</span></span>
