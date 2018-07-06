---
uid: web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-vb
title: 대체 봇 (VB) | Microsoft Docs
author: wenz
description: 자동화 된 봇 스팸, 사용자 개입 없이 주석 양식을 제출를 사용 하 여 웹 로그 및 기타 웹 사이트를 석고 합니다. ASP.NET AJAX Con NoBot 컨트롤 하는 중...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: e9803150-452d-4521-97e3-d75d5599383c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-vb
msc.type: authoredcontent
ms.openlocfilehash: e79a973f721c1feeddb00ecbf9d6a76786afb4bb
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37833445"
---
<a name="fighting-bots-vb"></a><span data-ttu-id="433ae-104">대체 봇 (VB)</span><span class="sxs-lookup"><span data-stu-id="433ae-104">Fighting Bots (VB)</span></span>
====================
<span data-ttu-id="433ae-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="433ae-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="433ae-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="433ae-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0VB.pdf)</span></span>

> <span data-ttu-id="433ae-107">자동화 된 봇 스팸, 사용자 개입 없이 주석 양식을 제출를 사용 하 여 웹 로그 및 기타 웹 사이트를 석고 합니다.</span><span class="sxs-lookup"><span data-stu-id="433ae-107">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="433ae-108">ASP.NET AJAX Control Toolkit에서 NoBot 컨트롤 이러한 봇 싸 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="433ae-108">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>


## <a name="overview"></a><span data-ttu-id="433ae-109">개요</span><span class="sxs-lookup"><span data-stu-id="433ae-109">Overview</span></span>

<span data-ttu-id="433ae-110">자동화 된 봇 스팸, 사용자 개입 없이 주석 양식을 제출를 사용 하 여 웹 로그 및 기타 웹 사이트를 석고 합니다.</span><span class="sxs-lookup"><span data-stu-id="433ae-110">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="433ae-111">ASP.NET AJAX Control Toolkit에서 NoBot 컨트롤 이러한 봇 싸 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="433ae-111">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>

## <a name="steps"></a><span data-ttu-id="433ae-112">단계</span><span class="sxs-lookup"><span data-stu-id="433ae-112">Steps</span></span>

<span data-ttu-id="433ae-113">봇을 무력화 하는 데 한 가지 일반적인 방법은 컴퓨터와 사용자 떨어져 CAPTCHAs 완전히 자동화 된 공용 Turing 테스트를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="433ae-113">One common approach to defeat bots is to use CAPTCHAs Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="433ae-114">Turing 테스트 원래 테스트 사람 또는 컴퓨터 통신 파트너 인지 여부를 결정 해야 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="433ae-114">A Turing test was originally a test where someone needed to decide whether a communication partner is a human or a machine.</span></span> <span data-ttu-id="433ae-115">웹에서 CAPTCHA를 왜곡 되어 일부 문자를 사용 하 여 이미지의 일반적으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="433ae-115">In the web, a CAPTCHA usually consists of an image with some distorted letters on it.</span></span> <span data-ttu-id="433ae-116">OCR 알고리즘 실패 하는 반면 것만 사람이 이미지의 문자를 읽을 수 있도록입니다.</span><span class="sxs-lookup"><span data-stu-id="433ae-116">The idea is that only a human can read the letters on the image, whereas OCR algorithms will fail.</span></span>

<span data-ttu-id="433ae-117">몇 가지 장점과이 방식의 단점은 있지만이 설명은이 자습서의 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="433ae-117">There are several advantages and disadvantages to this approach, but a discussion of this is beyond the scope of this tutorial.</span></span> <span data-ttu-id="433ae-118">그러나 유사한 접근 방식을 제공 하는 ASP.NET AJAX Control Toolkit의 컨트롤: `NoBot`합니다.</span><span class="sxs-lookup"><span data-stu-id="433ae-118">There is however a control in the ASP.NET AJAX Control Toolkit which provides a similar approach: `NoBot`.</span></span> <span data-ttu-id="433ae-119">대부분 스팸 시도 하는 경우 성공적인 간주 됩니다. 여기서 블로그 같은 웹 사이트에서 매우 잘 경우 약 48gb), 되며에 극복 CAPTCHA를 보다 쉽게 하지만 매우 쉽게 사용할 수는는 `NoBot` 제어 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="433ae-119">It is easier to overcome than a CAPTCHA, but is very easy to use and fares extremely well on websites like blogs where it is considered a success if most spam attempts are defeated, which the `NoBot` control can do.</span></span>

<span data-ttu-id="433ae-120">`NoBot` 이러한 조건 중 하나 이상이 충족 되 면 현재 ASP.NET web form의 포스트백을 가로채:</span><span class="sxs-lookup"><span data-stu-id="433ae-120">`NoBot` intercepts the postback of the current ASP.NET web form if at least one of these conditions is met:</span></span>

- <span data-ttu-id="433ae-121">브라우저 JavaScript 퍼즐 실패 (예를 들어 경우 JavaScript가 비활성화)</span><span class="sxs-lookup"><span data-stu-id="433ae-121">The browser fails to solve a JavaScript puzzle (for instance when JavaScript is deactivated)</span></span>
- <span data-ttu-id="433ae-122">사용자를 빠르게 양식을 제출</span><span class="sxs-lookup"><span data-stu-id="433ae-122">The user submitted the form to fast</span></span>
- <span data-ttu-id="433ae-123">특정 시간 내에 너무 자주 양식을 제출 하는 클라이언트 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="433ae-123">The client IP address submitted the form too often in a certain period of time.</span></span>

<span data-ttu-id="433ae-124">이러한 조건을 확인 하기 위해는 `NoBot` 컨트롤 (모든 선택 사항) 이러한 특성이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="433ae-124">In order to check for these conditions, the `NoBot` control requires these attributes (all of them optional):</span></span>

- <span data-ttu-id="433ae-125">`ResponseMinimumDelaySeconds` 최소한의 포스트백 간격 (초)</span><span class="sxs-lookup"><span data-stu-id="433ae-125">`ResponseMinimumDelaySeconds` minimum amount of seconds between postbacks</span></span>
- <span data-ttu-id="433ae-126">`CutoffWindowSeconds` 하나의 IP에서 포스트백에 측정 하는 시간 간격의 길이</span><span class="sxs-lookup"><span data-stu-id="433ae-126">`CutoffWindowSeconds` length of time interval in which postbacks from one IP are measures</span></span>
- <span data-ttu-id="433ae-127">`CutoffMaximumInstances` 최대 시간 간격 (초)</span><span class="sxs-lookup"><span data-stu-id="433ae-127">`CutoffMaximumInstances` maximum amount of seconds per time interval</span></span>

<span data-ttu-id="433ae-128">다음 태그 요구는 적어도 2 초 포스트백 간에 경과 하 고 5 개만 포스트백을 가지는 작거나 30 초 간격 내에서:</span><span class="sxs-lookup"><span data-stu-id="433ae-128">The following markup demands that at least two seconds elapse between postbacks and that there are only five postbacks or less within a 30 seconds interval:</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample1.aspx)]

<span data-ttu-id="433ae-129">다음 일반적인 방식으로 포함 해야 합니다 `ScriptManager` 페이지에서 ASP.NET AJAX library가 로드 하 고 컨트롤 도구 키트를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="433ae-129">Then as usual make sure to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample2.aspx)]

<span data-ttu-id="433ae-130">대부분의 검사 이후 `NoBot` 수행 하는 서버 쪽에서 발생이 유효성 검사의 결과 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="433ae-130">Since most of the checks `NoBot` is doing occur on the server side, you need to check the result of these validations.</span></span> <span data-ttu-id="433ae-131">호출 하 여 이렇게 `NoBot`의 `IsValid()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="433ae-131">This can be done by calling `NoBot`'s `IsValid()` method.</span></span> <span data-ttu-id="433ae-132">에 인수가 하나 (으로 `out` 매개 변수 /`ByRef` 매개 변수)가 형식의 `NoBotState`합니다.</span><span class="sxs-lookup"><span data-stu-id="433ae-132">It has one argument (as an `out` parameter/`ByRef` parameter) which is of type `NoBotState`.</span></span> <span data-ttu-id="433ae-133">확인이 실패 하는 경우 해당 문자열 표현 이유를 포함 하 고 `Valid` 그렇지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="433ae-133">Its string representation contains the reason when the check fails and `Valid` otherwise.</span></span> <span data-ttu-id="433ae-134">다음 코드에 따라 메시지를 출력 `NoBot`의 결과:</span><span class="sxs-lookup"><span data-stu-id="433ae-134">The following code outputs a message according to `NoBot`'s result:</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample3.aspx)]

<span data-ttu-id="433ae-135">마지막으로 전송할 폼 및 레이블 요소를 메시지를 출력 해야 하 고 완료!</span><span class="sxs-lookup"><span data-stu-id="433ae-135">Finally, you need a form to submit and a label element to output the message, and you are done!</span></span>

[!code-aspx[Main](fighting-bots-vb/samples/sample4.aspx)]

<span data-ttu-id="433ae-136">이 스크립트를 실행 및 JavaScript를 비활성화 또는 처음 2 초 안에 양식을 제출 하거나 30 초 내에 7 번 양식을 제출, 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="433ae-136">When you run this script and deactivate JavaScript or submit the form within the first two seconds or submit the form seven times within thirty seconds, you will get an error message.</span></span> <span data-ttu-id="433ae-137">그러나이 컨트롤을 현명 하 게 사용, 사용자의 약 90 95% 활성화 하는 JavaScript가 사용자의 5 ~ 10% 실패는 `NoBot`의 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="433ae-137">However use this control wisely, since only about 90-95% of users have JavaScript activated, therefore 5-10% of users will fail `NoBot`'s test.</span></span>


<span data-ttu-id="433ae-138">[![이 오류 메시지는 봇 인해 발생할 수 있습니다.](fighting-bots-vb/_static/image2.png)](fighting-bots-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="433ae-138">[![This error message could have been caused by a bot](fighting-bots-vb/_static/image2.png)](fighting-bots-vb/_static/image1.png)</span></span>

<span data-ttu-id="433ae-139">이 오류 메시지는 봇 인해 발생할 수 있습니다 ([클릭 하 여 큰 이미지 보기](fighting-bots-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="433ae-139">This error message could have been caused by a bot ([Click to view full-size image](fighting-bots-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="433ae-140">이전</span><span class="sxs-lookup"><span data-stu-id="433ae-140">Previous</span></span>](fighting-bots-cs.md)
