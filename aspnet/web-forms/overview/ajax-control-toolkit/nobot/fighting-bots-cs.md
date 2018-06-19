---
uid: web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
title: 봇 (C#)에 대처 | Microsoft Docs
author: wenz
description: 자동화 된 봇 웹 로그 및 기타 웹 사이트 사용자 상호 작용 없이 주석 양식 전송 스팸 석고 합니다. ASP.NET AJAX Con에서 NoBot 컨트롤 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 0a1917e0-884a-4576-8e93-9ed660faae51
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
msc.type: authoredcontent
ms.openlocfilehash: 1ea3aaa5461c2f58a927ae975568f18a34a4729b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30872015"
---
<a name="fighting-bots-c"></a><span data-ttu-id="16ac8-104">대처 봇 (C#)</span><span class="sxs-lookup"><span data-stu-id="16ac8-104">Fighting Bots (C#)</span></span>
====================
<span data-ttu-id="16ac8-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="16ac8-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="16ac8-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="16ac8-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0CS.pdf)</span></span>

> <span data-ttu-id="16ac8-107">자동화 된 봇 웹 로그 및 기타 웹 사이트 사용자 상호 작용 없이 주석 양식 전송 스팸 석고 합니다.</span><span class="sxs-lookup"><span data-stu-id="16ac8-107">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="16ac8-108">ASP.NET AJAX 컨트롤 도구 키트에서 NoBot 컨트롤 이러한 봇 방지 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16ac8-108">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>


## <a name="overview"></a><span data-ttu-id="16ac8-109">개요</span><span class="sxs-lookup"><span data-stu-id="16ac8-109">Overview</span></span>

<span data-ttu-id="16ac8-110">자동화 된 봇 웹 로그 및 기타 웹 사이트 사용자 상호 작용 없이 주석 양식 전송 스팸 석고 합니다.</span><span class="sxs-lookup"><span data-stu-id="16ac8-110">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="16ac8-111">ASP.NET AJAX 컨트롤 도구 키트에서 NoBot 컨트롤 이러한 봇 방지 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16ac8-111">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>

## <a name="steps"></a><span data-ttu-id="16ac8-112">단계</span><span class="sxs-lookup"><span data-stu-id="16ac8-112">Steps</span></span>

<span data-ttu-id="16ac8-113">봇을 무력화 하는 한 가지 일반적인 방법은 컴퓨터와 사용자 떨어져 CAPTCHAs 완전히 자동화 된 공용 Turing 테스트를 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="16ac8-113">One common approach to defeat bots is to use CAPTCHAs Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="16ac8-114">Turing 테스트 원래 테스트 누군가가 통신 파트너 사람 또는 컴퓨터를 지 여부를 결정 하는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="16ac8-114">A Turing test was originally a test where someone needed to decide whether a communication partner is a human or a machine.</span></span> <span data-ttu-id="16ac8-115">웹에서 CAPTCHA에 왜곡된 일부 문자를 사용 하 여 이미지의 일반적으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16ac8-115">In the web, a CAPTCHA usually consists of an image with some distorted letters on it.</span></span> <span data-ttu-id="16ac8-116">사람이 이미지에 문자를 읽을 수 있도록 반면 OCR 알고리즘 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="16ac8-116">The idea is that only a human can read the letters on the image, whereas OCR algorithms will fail.</span></span>

<span data-ttu-id="16ac8-117">몇 가지 장점 및 단점이이 방법에 있지만이 설명은이 자습서의 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="16ac8-117">There are several advantages and disadvantages to this approach, but a discussion of this is beyond the scope of this tutorial.</span></span> <span data-ttu-id="16ac8-118">그러나 유사한 방법을 제공 하는 ASP.NET AJAX 컨트롤 도구 키트에서 컨트롤: `NoBot`합니다.</span><span class="sxs-lookup"><span data-stu-id="16ac8-118">There is however a control in the ASP.NET AJAX Control Toolkit which provides a similar approach: `NoBot`.</span></span> <span data-ttu-id="16ac8-119">대부분 스팸 시도 하는 경우 성공 간주 됩니다. 여기서 블로그 같은 웹 사이트에서 매우 잘 fares, 되며에 보다 CAPTCHA를 극복 하기 쉽게 알고리즘은 매우 쉽게 사용할 수 있지만는 `NoBot` 제어 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16ac8-119">It is easier to overcome than a CAPTCHA, but is very easy to use and fares extremely well on websites like blogs where it is considered a success if most spam attempts are defeated, which the `NoBot` control can do.</span></span>

<span data-ttu-id="16ac8-120">`NoBot` 이러한 조건 중 하나 이상을 충족 될 경우에 현재 ASP.NET web form의 포스트백을 가로채:</span><span class="sxs-lookup"><span data-stu-id="16ac8-120">`NoBot` intercepts the postback of the current ASP.NET web form if at least one of these conditions is met:</span></span>

- <span data-ttu-id="16ac8-121">JavaScript 퍼즐을 해결 하기 위해 브라우저 실패 (예를 들어 JavaScript가 비활성화 된 경우)</span><span class="sxs-lookup"><span data-stu-id="16ac8-121">The browser fails to solve a JavaScript puzzle (for instance when JavaScript is deactivated)</span></span>
- <span data-ttu-id="16ac8-122">사용자를 빠른 양식을 제출</span><span class="sxs-lookup"><span data-stu-id="16ac8-122">The user submitted the form to fast</span></span>
- <span data-ttu-id="16ac8-123">특정 기간에 너무 자주 양식을 제출 하는 클라이언트 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="16ac8-123">The client IP address submitted the form too often in a certain period of time.</span></span>

<span data-ttu-id="16ac8-124">이러한 조건을 확인 하기 위해는 `NoBot` 컨트롤 (모든 옵션) 이러한 특성을 사용 하려면:</span><span class="sxs-lookup"><span data-stu-id="16ac8-124">In order to check for these conditions, the `NoBot` control requires these attributes (all of them optional):</span></span>

- <span data-ttu-id="16ac8-125">`ResponseMinimumDelaySeconds` 최소한의 포스트백 간격 (초)</span><span class="sxs-lookup"><span data-stu-id="16ac8-125">`ResponseMinimumDelaySeconds` minimum amount of seconds between postbacks</span></span>
- <span data-ttu-id="16ac8-126">`CutoffWindowSeconds` 하나의 IP에서 포스트백 측정값 되는 시간 간격의 길이</span><span class="sxs-lookup"><span data-stu-id="16ac8-126">`CutoffWindowSeconds` length of time interval in which postbacks from one IP are measures</span></span>
- <span data-ttu-id="16ac8-127">`CutoffMaximumInstances` 시간 간격 (초)의 최대 크기</span><span class="sxs-lookup"><span data-stu-id="16ac8-127">`CutoffMaximumInstances` maximum amount of seconds per time interval</span></span>

<span data-ttu-id="16ac8-128">다음 태그 요구 2 초 해당 이상 게시 하는 동안 경과 5 개만 포스트백 있는지 이하의 30 초 간격 내에서:</span><span class="sxs-lookup"><span data-stu-id="16ac8-128">The following markup demands that at least two seconds elapse between postbacks and that there are only five postbacks or less within a 30 seconds interval:</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample1.aspx)]

<span data-ttu-id="16ac8-129">다음 평소와 같이 포함 되었는지 확인는 `ScriptManager` 페이지에 있도록 ASP.NET AJAX 라이브러리를 로드 하 고 제어 도구 키트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16ac8-129">Then as usual make sure to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample2.aspx)]

<span data-ttu-id="16ac8-130">대부분의 검사 이후 `NoBot` 수행 하는 작업 서버 쪽에서 발생이 유효성 검사의 결과 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16ac8-130">Since most of the checks `NoBot` is doing occur on the server side, you need to check the result of these validations.</span></span> <span data-ttu-id="16ac8-131">호출 하 여이 작업을 수행할 수 있습니다 `NoBot`의 `IsValid()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="16ac8-131">This can be done by calling `NoBot`'s `IsValid()` method.</span></span> <span data-ttu-id="16ac8-132">하나의 인수를 포함 (으로 `out` 매개 변수 /`ByRef` 매개 변수)가 형식의 `NoBotState`합니다.</span><span class="sxs-lookup"><span data-stu-id="16ac8-132">It has one argument (as an `out` parameter/`ByRef` parameter) which is of type `NoBotState`.</span></span> <span data-ttu-id="16ac8-133">문자열 표현 검사가 실패 한 경우 이유를 포함 하 고 `Valid` 그렇지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="16ac8-133">Its string representation contains the reason when the check fails and `Valid` otherwise.</span></span> <span data-ttu-id="16ac8-134">다음 코드에 따라 메시지를 출력 `NoBot`의 발생:</span><span class="sxs-lookup"><span data-stu-id="16ac8-134">The following code outputs a message according to `NoBot`'s result:</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample3.aspx)]

<span data-ttu-id="16ac8-135">마지막으로 폼을 제출 해야 label 요소는 메시지를 출력 하 고 작업이 완료 되!</span><span class="sxs-lookup"><span data-stu-id="16ac8-135">Finally, you need a form to submit and a label element to output the message, and you are done!</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample4.aspx)]

<span data-ttu-id="16ac8-136">이 스크립트를 실행 하 고 JavaScript 비활성화 처음 2 초 안에 폼을 제출 하거나 7 번 30 초 내에서는 양식을 제출, 오류 메시지가 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16ac8-136">When you run this script and deactivate JavaScript or submit the form within the first two seconds or submit the form seven times within thirty seconds, you will get an error message.</span></span> <span data-ttu-id="16ac8-137">그러나이 컨트롤을 현명 하 게 사용를 사용자의 약 90 95% 활성화 하는 JavaScript에 한 사용자의 5-10% 되지 것입니다 `NoBot`의 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="16ac8-137">However use this control wisely, since only about 90-95% of users have JavaScript activated, therefore 5-10% of users will fail `NoBot`'s test.</span></span>


<span data-ttu-id="16ac8-138">[![이 오류 메시지는 bot 인해 발생 수 있습니다.](fighting-bots-cs/_static/image2.png)](fighting-bots-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="16ac8-138">[![This error message could have been caused by a bot](fighting-bots-cs/_static/image2.png)](fighting-bots-cs/_static/image1.png)</span></span>

<span data-ttu-id="16ac8-139">이 오류 메시지는 bot 인해 발생 수 ([전체 크기 이미지를 보려면 클릭](fighting-bots-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="16ac8-139">This error message could have been caused by a bot ([Click to view full-size image](fighting-bots-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="16ac8-140">다음</span><span class="sxs-lookup"><span data-stu-id="16ac8-140">Next</span></span>](fighting-bots-vb.md)
