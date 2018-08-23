---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
title: (VB) 암호 강도 테스트 | Microsoft Docs
author: wenz
description: 암호는 지연 사용자 해독 하기 쉬운 간단한 암호를 선택 하는 경향이 있습니다 있도록 거의 모든 곳에서 필요 합니다. ASP에서 PasswordStrength 컨트롤입니다. N....
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9215a37f-3133-4887-8ed2-3689f3a53551
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
msc.type: authoredcontent
ms.openlocfilehash: db4b2a6bbdb0716442b104c03d0c4138bf60f9be
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41836382"
---
<a name="testing-the-strength-of-a-password-vb"></a><span data-ttu-id="d9287-104">(VB) 암호 강도 테스트</span><span class="sxs-lookup"><span data-stu-id="d9287-104">Testing the Strength of a Password (VB)</span></span>
====================
<span data-ttu-id="d9287-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="d9287-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="d9287-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="d9287-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)</span></span>

> <span data-ttu-id="d9287-107">암호는 지연 사용자 해독 하기 쉬운 간단한 암호를 선택 하는 경향이 있습니다 있도록 거의 모든 곳에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9287-107">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="d9287-108">ASP.NET AJAX Control Toolkit에서 PasswordStrength 컨트롤 성이나 암호를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9287-108">The PasswordStrength control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>


## <a name="overview"></a><span data-ttu-id="d9287-109">개요</span><span class="sxs-lookup"><span data-stu-id="d9287-109">Overview</span></span>

<span data-ttu-id="d9287-110">암호는 지연 사용자 해독 하기 쉬운 간단한 암호를 선택 하는 경향이 있습니다 있도록 거의 모든 곳에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9287-110">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="d9287-111">`PasswordStrength` ASP.NET AJAX Control Toolkit 컨트롤 성이나 암호를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9287-111">The `PasswordStrength` control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="steps"></a><span data-ttu-id="d9287-112">단계</span><span class="sxs-lookup"><span data-stu-id="d9287-112">Steps</span></span>

<span data-ttu-id="d9287-113">`PasswordStrength` 컨트롤 텍스트 상자를 확장 하 고 그 안에 암호 충분 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9287-113">The `PasswordStrength` control extends a text box and checks whether the password in it is good enough.</span></span> <span data-ttu-id="d9287-114">다양 한 특성을 통해 옵션 제공 그 중 일부가 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d9287-114">It offers a wealth of options via attributes; here are just some of them:</span></span>

- <span data-ttu-id="d9287-115">`MinimumNumericCharacters` 암호에 필요한 숫자 문자의 최소 개수</span><span class="sxs-lookup"><span data-stu-id="d9287-115">`MinimumNumericCharacters` minimum number of numeric characters required in the password</span></span>
- <span data-ttu-id="d9287-116">`MinimumSymbolCharacters` 암호에 필요한 기호 문자 (없습니다 문자 및 숫자)의 최소 수</span><span class="sxs-lookup"><span data-stu-id="d9287-116">`MinimumSymbolCharacters` minimum number of symbol characters (not letters and digits) required in the password</span></span>
- <span data-ttu-id="d9287-117">`PreferredPasswordLength` 암호의 최소 길이</span><span class="sxs-lookup"><span data-stu-id="d9287-117">`PreferredPasswordLength` minimum length of the password</span></span>
- <span data-ttu-id="d9287-118">`RequiresUpperAndLowerCaseCharacters` 암호를 대 / 소문자를 사용 해야 하는 여부</span><span class="sxs-lookup"><span data-stu-id="d9287-118">`RequiresUpperAndLowerCaseCharacters` whether the password needs to use both uppercase and lowercase characters</span></span>

<span data-ttu-id="d9287-119">합니다 `StrengthIndicatorType` 텍스트로, 암호의 강도 표시 하는 방법을 설명 (값 `"Text"`) 또는 진행률 표시줄의 종류 (값 `"BarIndicator"`).</span><span class="sxs-lookup"><span data-stu-id="d9287-119">The `StrengthIndicatorType` provides the information how to present the strength of the password, as text (value `"Text"`) or as a kind of progress bar (value `"BarIndicator"`).</span></span> <span data-ttu-id="d9287-120">에 `DisplayPosition` 특성을 구성한 위치 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9287-120">In the `DisplayPosition` attribute, you configure where the information appears.</span></span> <span data-ttu-id="d9287-121">ASP.NET AJAX를 포함 한 전체 예제를 다음과 같습니다 `ScriptManager` 컨트롤은 `PasswordStrength` 컨트롤과 물론 사용자 암호를 입력할 수 있는 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="d9287-121">Here is a complete example, including the ASP.NET AJAX `ScriptManager` control, the `PasswordStrength` control and of course a text box where the user may enter a password.</span></span> <span data-ttu-id="d9287-122">데모를 위해 두 번째 폼 필드 입력 내용을 개발 하는 동안 볼 수 있도록 일반 텍스트 필드 및 암호 필드가 아닙니다입니다.</span><span class="sxs-lookup"><span data-stu-id="d9287-122">For the sake of demonstration, the latter form field is a regular text field and not a password field so that you can see during development what you are typing.</span></span>

[!code-aspx[Main](testing-the-strength-of-a-password-vb/samples/sample1.aspx)]

<span data-ttu-id="d9287-123">페이지를 실행 하 고 지금 입력:만 소문자, 대문자, 숫자 및 기호를 입력 한 후 암호 unbreakable으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9287-123">Run the page and type away: Only after you have entered lowercase letters, uppercase letters, digits and symbols, the password is deemed as unbreakable .</span></span>


<span data-ttu-id="d9287-124">[![이제 암호 양호 (매우)](testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d9287-124">[![Now the password is (quite) good](testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)</span></span>

<span data-ttu-id="d9287-125">이제 암호 () 활동적 ([클릭 하 여 큰 이미지 보기](testing-the-strength-of-a-password-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="d9287-125">Now the password is (quite) good ([Click to view full-size image](testing-the-strength-of-a-password-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="d9287-126">이전</span><span class="sxs-lookup"><span data-stu-id="d9287-126">Previous</span></span>](testing-the-strength-of-a-password-cs.md)
