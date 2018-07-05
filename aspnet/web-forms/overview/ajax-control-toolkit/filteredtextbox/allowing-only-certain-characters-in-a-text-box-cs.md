---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-cs
title: 텍스트 상자 (C#)에 특정 문자만 허용 | Microsoft Docs
author: wenz
description: ASP.NET 유효성 검사 컨트롤은 사용자 입력에 특정 문자만 허용 됩니다 있는지 확인할 수 있습니다. 그러나이 여전히 해도 사용자 입력 으로부터 잘못 된...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: fd2a1c52-d717-44af-8a61-67c8279bb26e
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-cs
msc.type: authoredcontent
ms.openlocfilehash: dd7203d7f367f275d2d80c86119edc9645c9d24c
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37400732"
---
<a name="allowing-only-certain-characters-in-a-text-box-c"></a><span data-ttu-id="6b847-104">텍스트 상자 (C#)에 특정 문자만 허용</span><span class="sxs-lookup"><span data-stu-id="6b847-104">Allowing Only Certain Characters in a Text Box (C#)</span></span>
====================
<span data-ttu-id="6b847-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6b847-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6b847-106">[코드를 다운로드](http://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="6b847-106">[Download Code](http://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0CS.pdf)</span></span>

> <span data-ttu-id="6b847-107">ASP.NET 유효성 검사 컨트롤은 사용자 입력에 특정 문자만 허용 됩니다 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b847-107">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="6b847-108">그러나이 여전히 해도 잘못 된 문자를 입력 하 고 양식을 제출 하는 동안 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b847-108">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>


## <a name="overview"></a><span data-ttu-id="6b847-109">개요</span><span class="sxs-lookup"><span data-stu-id="6b847-109">Overview</span></span>

<span data-ttu-id="6b847-110">ASP.NET 유효성 검사 컨트롤은 사용자 입력에 특정 문자만 허용 됩니다 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b847-110">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="6b847-111">그러나이 여전히 해도 잘못 된 문자를 입력 하 고 양식을 제출 하는 동안 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b847-111">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="steps"></a><span data-ttu-id="6b847-112">단계</span><span class="sxs-lookup"><span data-stu-id="6b847-112">Steps</span></span>

<span data-ttu-id="6b847-113">ASP.NET AJAX Control Toolkit에 포함 된 `FilteredTextBox` 입력란을 확장 하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="6b847-113">The ASP.NET AJAX Control Toolkit contains the `FilteredTextBox` control which extends a text box.</span></span> <span data-ttu-id="6b847-114">활성화 되 면 특정 문자 집합만 필드에 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b847-114">Once activated, only a certain set of characters may be entered into the field.</span></span>

<span data-ttu-id="6b847-115">이렇게 하려면 먼저 해야 일반적으로 ASP.NET AJAX `ScriptManager` 도 ASP.NET AJAX Control Toolkit에서 사용 되는 JavaScript 라이브러리를 로드 하는:</span><span class="sxs-lookup"><span data-stu-id="6b847-115">For this to work, we first need as usual the ASP.NET AJAX `ScriptManager` which loads the JavaScript libraries which are also used by the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample1.aspx)]

<span data-ttu-id="6b847-116">그런 다음 텍스트 상자를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="6b847-116">Then, we need a text box:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample2.aspx)]

<span data-ttu-id="6b847-117">마지막으로 `FilteredTextBoxExtender` 문자는 사용자가 입력 수를 제한 하는 컨트롤을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b847-117">Finally, the `FilteredTextBoxExtender` control takes care of restricting the characters the user is allowed to type.</span></span> <span data-ttu-id="6b847-118">먼저 설정 합니다 `TargetControlID` 특성을 합니다 `ID` 의 `TextBox` 컨트롤.</span><span class="sxs-lookup"><span data-stu-id="6b847-118">First, set the `TargetControlID` attribute to the `ID` of the `TextBox` control.</span></span> <span data-ttu-id="6b847-119">그런 다음 중 하나를 선택 `FilterType` 값:</span><span class="sxs-lookup"><span data-stu-id="6b847-119">Then, choose one of the available `FilterType` values:</span></span>

- <span data-ttu-id="6b847-120">`Custom` 기본값은 유효한 문자 목록을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b847-120">`Custom` default; you have to provide a list of valid chars</span></span>
- <span data-ttu-id="6b847-121">`LowercaseLetters` 소문자만</span><span class="sxs-lookup"><span data-stu-id="6b847-121">`LowercaseLetters` lowercase letters only</span></span>
- <span data-ttu-id="6b847-122">`Numbers` 숫자만</span><span class="sxs-lookup"><span data-stu-id="6b847-122">`Numbers` digits only</span></span>
- <span data-ttu-id="6b847-123">`UppercaseLetters` 대문자로</span><span class="sxs-lookup"><span data-stu-id="6b847-123">`UppercaseLetters` uppercase letters only</span></span>

<span data-ttu-id="6b847-124">경우는 `Custom FilterType` 사용 되는 `ValidChars` 속성 집합 이어야 하며 입력 될 수 있는 문자 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b847-124">If the `Custom FilterType` is used, the `ValidChars` property must be set and provide a list of characters that may be typed.</span></span> <span data-ttu-id="6b847-125">그런데: 텍스트 상자에 텍스트를 붙여 넣습니다. 하려는 모든 유효 하지 않은 문자 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b847-125">By the way: if you try to paste text into the text box, all invalid chars are removed.</span></span>

<span data-ttu-id="6b847-126">여기에 대 한 태그를 `FilteredTextBoxExtender` 만 숫자를 허용 하는 컨트롤 (또한 되었을 수 있는 `FilterType="Numbers"`):</span><span class="sxs-lookup"><span data-stu-id="6b847-126">Here is the markup for the `FilteredTextBoxExtender` control that only allows digits (something that would also have been possible with `FilterType="Numbers"`):</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample3.aspx)]

<span data-ttu-id="6b847-127">JavaScript가 설정 된 경우에 문자를 입력 하 고 페이지를 실행 작동 하지 않습니다. 그러나 숫자 페이지에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b847-127">Run the page and try to enter a letter if JavaScript is enabled, it will not work; digits however appear on the page.</span></span> <span data-ttu-id="6b847-128">하지만 보호 `FilteredTextBox` 제공 완벽 아닙니다: 경우 JavaScript가 설정 된, 추가 유효성 검사 의미, 즉, ASP를 사용 해야 하므로 모든 데이터를 텍스트 상자에 입력 될 수 있습니다. NET의 유효성 검사를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b847-128">However note that the protection `FilteredTextBox` provides is not bullet-proof: If JavaScript is enabled, any data may be entered in the text box, so you have to use additional validation means, i.e. ASP.NET's validation controls.</span></span>


<span data-ttu-id="6b847-129">[![숫자만 입력할 수](allowing-only-certain-characters-in-a-text-box-cs/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6b847-129">[![Only digits may be entered](allowing-only-certain-characters-in-a-text-box-cs/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-cs/_static/image1.png)</span></span>

<span data-ttu-id="6b847-130">숫자만 입력 될 수 있습니다 ([클릭 하 여 큰 이미지 보기](allowing-only-certain-characters-in-a-text-box-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="6b847-130">Only digits may be entered ([Click to view full-size image](allowing-only-certain-characters-in-a-text-box-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="6b847-131">다음</span><span class="sxs-lookup"><span data-stu-id="6b847-131">Next</span></span>](allowing-only-certain-characters-in-a-text-box-vb.md)
