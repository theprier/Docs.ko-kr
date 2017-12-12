---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
title: "테스트 (C#) 암호의 강도 | Microsoft Docs"
author: wenz
description: "암호는 지연 사용자는 해독 하기 쉬운 간단한 암호를 선택 하는 경향이 있도록 거의 모든 곳에서 필요 합니다. ASP에서 PasswordStrength 컨트롤입니다. 14."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: cb4afbae-9b8f-483d-9729-476d4b9f85fc
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
msc.type: authoredcontent
ms.openlocfilehash: eda7baae1833b074ba34d8f10fa434df14cc592e
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="testing-the-strength-of-a-password-c"></a><span data-ttu-id="cd6d6-104">암호 (C#)의 강도 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="cd6d6-104">Testing the Strength of a Password (C#)</span></span>
====================
<span data-ttu-id="cd6d6-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="cd6d6-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="cd6d6-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="cd6d6-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)</span></span>

> <span data-ttu-id="cd6d6-107">암호는 지연 사용자는 해독 하기 쉬운 간단한 암호를 선택 하는 경향이 있도록 거의 모든 곳에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd6d6-107">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="cd6d6-108">ASP.NET AJAX 컨트롤 도구 키트에서 PasswordStrength 컨트롤 얼마나 양호한 암호 지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd6d6-108">The PasswordStrength control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>


## <a name="overview"></a><span data-ttu-id="cd6d6-109">개요</span><span class="sxs-lookup"><span data-stu-id="cd6d6-109">Overview</span></span>

<span data-ttu-id="cd6d6-110">암호는 지연 사용자는 해독 하기 쉬운 간단한 암호를 선택 하는 경향이 있도록 거의 모든 곳에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd6d6-110">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="cd6d6-111">`PasswordStrength` ASP.NET AJAX 컨트롤 도구 키트에서 컨트롤 얼마나 적절 한 암호를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cd6d6-111">The `PasswordStrength` control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="steps"></a><span data-ttu-id="cd6d6-112">단계</span><span class="sxs-lookup"><span data-stu-id="cd6d6-112">Steps</span></span>

<span data-ttu-id="cd6d6-113">`PasswordStrength` 컨트롤을 텍스트 상자를 확장 하 고에서 암호가 충분히 강력한 인지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd6d6-113">The `PasswordStrength` control extends a text box and checks whether the password in it is good enough.</span></span> <span data-ttu-id="cd6d6-114">다양 한 특성을 통해 옵션 제공 그 중 일부만 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cd6d6-114">It offers a wealth of options via attributes; here are just some of them:</span></span>

- <span data-ttu-id="cd6d6-115">`MinimumNumericCharacters`암호에 필요한 숫자 문자의 최소 개수</span><span class="sxs-lookup"><span data-stu-id="cd6d6-115">`MinimumNumericCharacters` minimum number of numeric characters required in the password</span></span>
- <span data-ttu-id="cd6d6-116">`MinimumSymbolCharacters`최소 기호 문자 (문자 및 숫자 하지) 암호에 필요한</span><span class="sxs-lookup"><span data-stu-id="cd6d6-116">`MinimumSymbolCharacters` minimum number of symbol characters (not letters and digits) required in the password</span></span>
- <span data-ttu-id="cd6d6-117">`PreferredPasswordLength`암호의 최소 길이</span><span class="sxs-lookup"><span data-stu-id="cd6d6-117">`PreferredPasswordLength` minimum length of the password</span></span>
- <span data-ttu-id="cd6d6-118">`RequiresUpperAndLowerCaseCharacters`암호를 대문자 및 소문자 모두 문자를 사용 해야 하는 여부</span><span class="sxs-lookup"><span data-stu-id="cd6d6-118">`RequiresUpperAndLowerCaseCharacters` whether the password needs to use both uppercase and lowercase characters</span></span>

<span data-ttu-id="cd6d6-119">`StrengthIndicatorType` 텍스트로 암호의 강도 제공 하는 방법 정보를 제공 합니다 (값 `"Text"`) 또는 진행률 표시줄의 한 종류로 (값 `"BarIndicator"`).</span><span class="sxs-lookup"><span data-stu-id="cd6d6-119">The `StrengthIndicatorType` provides the information how to present the strength of the password, as text (value `"Text"`) or as a kind of progress bar (value `"BarIndicator"`).</span></span> <span data-ttu-id="cd6d6-120">에 `DisplayPosition` 특성을 구성한 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd6d6-120">In the `DisplayPosition` attribute, you configure where the information appears.</span></span> <span data-ttu-id="cd6d6-121">ASP.NET AJAX를 포함 한 전체 예제는 다음과 같습니다 `ScriptManager` 컨트롤의 `PasswordStrength` 제어 및 물론 사용자 암호를 입력할 수 있는 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="cd6d6-121">Here is a complete example, including the ASP.NET AJAX `ScriptManager` control, the `PasswordStrength` control and of course a text box where the user may enter a password.</span></span> <span data-ttu-id="cd6d6-122">데모를 보려면 위해 후자 폼 필드 입력 내용을 개발 하는 동안 볼 수 있도록 일반 텍스트 필드 및 암호 필드가 아닙니다 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd6d6-122">For the sake of demonstration, the latter form field is a regular text field and not a password field so that you can see during development what you are typing.</span></span>

[!code-aspx[Main](testing-the-strength-of-a-password-cs/samples/sample1.aspx)]

<span data-ttu-id="cd6d6-123">페이지를 실행 하 고 다른 페이지로 입력: 암호 같이 엔터티로 간주 소문자, 대문자, 숫자 및 기호를 입력 한 후에 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd6d6-123">Run the page and type away: Only after you have entered lowercase letters, uppercase letters, digits and symbols, the password is deemed as unbreakable .</span></span>


<span data-ttu-id="cd6d6-124">[![암호는 () 활동적 이제](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="cd6d6-124">[![Now the password is (quite) good](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)</span></span>

<span data-ttu-id="cd6d6-125">암호는 () 활동적 ([전체 크기 이미지를 보려면 클릭](testing-the-strength-of-a-password-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="cd6d6-125">Now the password is (quite) good ([Click to view full-size image](testing-the-strength-of-a-password-cs/_static/image3.png))</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="cd6d6-126">다음</span><span class="sxs-lookup"><span data-stu-id="cd6d6-126">Next</span></span>](testing-the-strength-of-a-password-vb.md)
