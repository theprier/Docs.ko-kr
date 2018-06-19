---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
title: 웹 서비스 백 엔드 (C#)를 사용 하 여 숫자 위로/아래로 컨트롤 만들기 | Microsoft Docs
author: wenz
description: 확인란에 값을 입력 하는 사용자를 게 하지 않고 숫자 위로/아래로 컨트롤 (Windows 및 다른 운영 체제에 있음)을 더 많은 c 중일 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: c99bbc72-d4de-41ed-92a4-9a4632368363
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
msc.type: authoredcontent
ms.openlocfilehash: 942902bdba93fe4fef8a9122403c6d5c62e6123c
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30868817"
---
<a name="creating-a-numeric-updown-control-with-a-web-service-backend-c"></a><span data-ttu-id="7fa2f-103">웹 서비스 백 엔드 (C#)를 사용 하 여 숫자 위로/아래로 컨트롤 만들기</span><span class="sxs-lookup"><span data-stu-id="7fa2f-103">Creating a Numeric Up/Down Control with a Web Service Backend (C#)</span></span>
====================
<span data-ttu-id="7fa2f-104">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="7fa2f-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7fa2f-105">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="7fa2f-105">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)</span></span>

> <span data-ttu-id="7fa2f-106">확인란에 값을 입력 하는 사용자를 게 하지 않고 숫자 위로/아래로 컨트롤 (에 있는 Windows 및 기타 운영 체제) 중일 더 많은 방법을 잘 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fa2f-106">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="7fa2f-107">기본적으로 항상 증가 또는 감소 값을 1, NumericUpDown 컨트롤 하지만 더 많은 융통성을 증명 하는 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="7fa2f-107">By default, the NumericUpDown control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>


## <a name="overview"></a><span data-ttu-id="7fa2f-108">개요</span><span class="sxs-lookup"><span data-stu-id="7fa2f-108">Overview</span></span>

<span data-ttu-id="7fa2f-109">확인란에 값을 입력 하는 사용자를 게 하지 않고 숫자 위로/아래로 컨트롤 (에 있는 Windows 및 기타 운영 체제) 중일 더 많은 방법을 잘 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fa2f-109">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="7fa2f-110">기본적으로는 `NumericUpDown` 하지만 더 많은 융통성을 증명 하는 웹 서비스 제어는 항상 증가 또는 값 1, 감소 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fa2f-110">By default, the `NumericUpDown` control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="7fa2f-111">단계</span><span class="sxs-lookup"><span data-stu-id="7fa2f-111">Steps</span></span>

<span data-ttu-id="7fa2f-112">ASP.NET AJAX 컨트롤 Toolkit에 포함 되어는 `NumericUpDown` extender를 텍스트 상자에 두 개의 단추를 자동으로 추가: 감소에 대 한 해당 값이 증가 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fa2f-112">The ASP.NET AJAX Control Toolkit contains the `NumericUpDown` extender which automatically adds two buttons to a text box: One for increasing its value, one for decreasing it.</span></span> <span data-ttu-id="7fa2f-113">그러나 컨트롤 웹 서비스 호출 (또는 페이지 메서드 호출)도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7fa2f-113">However the control also supports a web service call (or page method call).</span></span> <span data-ttu-id="7fa2f-114">때마다의 위 또는 아래로 단추를 클릭 하면 JavaScript 코드는 웹 서버에 연결 하 고 있는 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fa2f-114">Whenever the up or down button is clicked, the JavaScript code connects to the web server and executes a method there.</span></span> <span data-ttu-id="7fa2f-115">메서드 시그니처는 다음 중:</span><span class="sxs-lookup"><span data-stu-id="7fa2f-115">The method signature is the following one:</span></span>

[!code-csharp[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample1.cs)]

<span data-ttu-id="7fa2f-116">`current` 인수는 텍스트 상자의; 현재 값의 `tag` 특성은의 속성으로 설정할 수 있는 추가 컨텍스트 데이터는 `NumericUpDown` extender (하지만 필요 하지 않습니다).</span><span class="sxs-lookup"><span data-stu-id="7fa2f-116">The `current` argument is the current value in the text box; the `tag` attribute is additional context data that can be set as a property of the `NumericUpDown` extender (but is not required).</span></span>

<span data-ttu-id="7fa2f-117">이 샘플에 대 한 숫자 위로/아래로 컨트롤은 허용 2의 거듭제곱 값: 1, 2, 4, 8, 16, 32, 64, 및 등입니다.</span><span class="sxs-lookup"><span data-stu-id="7fa2f-117">For this sample, the numeric up/down control shall only allow values that are powers of two: 1, 2, 4, 8, 16, 32, 64, and so on.</span></span> <span data-ttu-id="7fa2f-118">따라서 메서드가 값을 늘리려면 다음 사용자가를 실행 해야 double 이전 값입니다. 또 다른 방법은 두 값을 나눕니다 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fa2f-118">Therefore, the method executed when the user wants to increase the value must double the old value; the other method must divide value by two.</span></span> <span data-ttu-id="7fa2f-119">따라서 여기에 전체 웹 서비스:</span><span class="sxs-lookup"><span data-stu-id="7fa2f-119">So here is the complete web service:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample2.aspx)]

<span data-ttu-id="7fa2f-120">마지막으로 새 ASP.NET 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7fa2f-120">Finally, create a new ASP.NET page.</span></span> <span data-ttu-id="7fa2f-121">필요한 일반적으로 `ScriptManager` 컨트롤은 `TextBox` 제어 및 `NumericUpDownExtender` 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="7fa2f-121">As usual, you need a `ScriptManager` control, a `TextBox` control and a `NumericUpDownExtender` control.</span></span> <span data-ttu-id="7fa2f-122">후자의 경우 웹 서비스 정보를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fa2f-122">For the latter, you have to provide the web service information:</span></span>

- <span data-ttu-id="7fa2f-123">`ServiceDownMethod` 웹 메서드 또는 메서드 페이지를 아래로의 이름</span><span class="sxs-lookup"><span data-stu-id="7fa2f-123">`ServiceDownMethod` name of the down web method or page method</span></span>
- <span data-ttu-id="7fa2f-124">`ServiceDownPath` 아래쪽 서비스 메서드로; 웹 서비스에 대 한 경로 페이지 메서드를 사용 하는 경우 생략</span><span class="sxs-lookup"><span data-stu-id="7fa2f-124">`ServiceDownPath` path to the web service with the down service method; omit if you are using a page method</span></span>
- <span data-ttu-id="7fa2f-125">`ServiceUpMethod` 위쪽의 이름을 웹 메서드 또는 메서드를 페이지</span><span class="sxs-lookup"><span data-stu-id="7fa2f-125">`ServiceUpMethod` name of the up web method or page method</span></span>
- <span data-ttu-id="7fa2f-126">`ServiceUpPath` 최신 서비스 메서드로; 웹 서비스에 대 한 경로 페이지 메서드를 사용 하는 경우 생략</span><span class="sxs-lookup"><span data-stu-id="7fa2f-126">`ServiceUpPath` path to the web service with the up service method; omit if you are using a page method</span></span>

<span data-ttu-id="7fa2f-127">페이지에 대 한 전체 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7fa2f-127">Here is the complete markup for the page:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample3.aspx)]

<span data-ttu-id="7fa2f-128">페이지를 실행 하는 경우 어떻게 값 텍스트 상자에 항상 두 배로 만듭니다 위쪽 단추를 클릭 하 고는 아래쪽 단추를 클릭할 때 반 축소 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fa2f-128">If you run the page, notice how the value in the text box always doubles when you click on the upper button, and is halved when you click on the lower button.</span></span>


<span data-ttu-id="7fa2f-129">[![2의 거듭제곱 번호만 표시](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7fa2f-129">[![Only numbers that are a power of 2 appear](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image1.png)</span></span>

<span data-ttu-id="7fa2f-130">2의 거듭제곱 번호만 표시 ([전체 크기 이미지를 보려면 클릭](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="7fa2f-130">Only numbers that are a power of 2 appear ([Click to view full-size image](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="7fa2f-131">다음</span><span class="sxs-lookup"><span data-stu-id="7fa2f-131">Next</span></span>](creating-a-numeric-up-down-control-with-a-web-service-backend-vb.md)
