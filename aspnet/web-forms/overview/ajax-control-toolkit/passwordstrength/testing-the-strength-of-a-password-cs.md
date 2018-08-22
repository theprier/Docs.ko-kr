---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
title: (C#) 암호 강도 테스트 | Microsoft Docs
author: wenz
description: 암호는 지연 사용자 해독 하기 쉬운 간단한 암호를 선택 하는 경향이 있습니다 있도록 거의 모든 곳에서 필요 합니다. ASP에서 PasswordStrength 컨트롤입니다. N....
ms.author: riande
ms.date: 06/02/2008
ms.assetid: cb4afbae-9b8f-483d-9729-476d4b9f85fc
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
msc.type: authoredcontent
ms.openlocfilehash: b71744df46f8b8d20efafa333a10370397c37d2f
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828544"
---
<a name="testing-the-strength-of-a-password-c"></a>(C#) 암호 강도 테스트
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)

> 암호는 지연 사용자 해독 하기 쉬운 간단한 암호를 선택 하는 경향이 있습니다 있도록 거의 모든 곳에서 필요 합니다. ASP.NET AJAX Control Toolkit에서 PasswordStrength 컨트롤 성이나 암호를 확인할 수 있습니다.


## <a name="overview"></a>개요

암호는 지연 사용자 해독 하기 쉬운 간단한 암호를 선택 하는 경향이 있습니다 있도록 거의 모든 곳에서 필요 합니다. `PasswordStrength` ASP.NET AJAX Control Toolkit 컨트롤 성이나 암호를 확인할 수 있습니다.

## <a name="steps"></a>단계

`PasswordStrength` 컨트롤 텍스트 상자를 확장 하 고 그 안에 암호 충분 인지 확인 합니다. 다양 한 특성을 통해 옵션 제공 그 중 일부가 다음과 같습니다.

- `MinimumNumericCharacters` 암호에 필요한 숫자 문자의 최소 개수
- `MinimumSymbolCharacters` 암호에 필요한 기호 문자 (없습니다 문자 및 숫자)의 최소 수
- `PreferredPasswordLength` 암호의 최소 길이
- `RequiresUpperAndLowerCaseCharacters` 암호를 대 / 소문자를 사용 해야 하는 여부

합니다 `StrengthIndicatorType` 텍스트로, 암호의 강도 표시 하는 방법을 설명 (값 `"Text"`) 또는 진행률 표시줄의 종류 (값 `"BarIndicator"`). 에 `DisplayPosition` 특성을 구성한 위치 정보를 표시 합니다. ASP.NET AJAX를 포함 한 전체 예제를 다음과 같습니다 `ScriptManager` 컨트롤은 `PasswordStrength` 컨트롤과 물론 사용자 암호를 입력할 수 있는 텍스트 상자입니다. 데모를 위해 두 번째 폼 필드 입력 내용을 개발 하는 동안 볼 수 있도록 일반 텍스트 필드 및 암호 필드가 아닙니다입니다.

[!code-aspx[Main](testing-the-strength-of-a-password-cs/samples/sample1.aspx)]

페이지를 실행 하 고 지금 입력:만 소문자, 대문자, 숫자 및 기호를 입력 한 후 암호 unbreakable으로 간주 됩니다.


[![이제 암호 양호 (매우)](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)

이제 암호 () 활동적 ([클릭 하 여 큰 이미지 보기](testing-the-strength-of-a-password-cs/_static/image3.png))

> [!div class="step-by-step"]
> [다음](testing-the-strength-of-a-password-vb.md)
