---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
title: 테스트 (VB) 암호의 강도 | Microsoft Docs
author: wenz
description: 암호는 지연 사용자는 해독 하기 쉬운 간단한 암호를 선택 하는 경향이 있도록 거의 모든 곳에서 필요 합니다. ASP에서 PasswordStrength 컨트롤입니다. 14.
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 9215a37f-3133-4887-8ed2-3689f3a53551
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
msc.type: authoredcontent
ms.openlocfilehash: 1d46026535f3f5cf82944359599464e8a4725280
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30879454"
---
<a name="testing-the-strength-of-a-password-vb"></a>(VB) 암호의 강도 테스트합니다.
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)

> 암호는 지연 사용자는 해독 하기 쉬운 간단한 암호를 선택 하는 경향이 있도록 거의 모든 곳에서 필요 합니다. ASP.NET AJAX 컨트롤 도구 키트에서 PasswordStrength 컨트롤 얼마나 양호한 암호 지 확인할 수 있습니다.


## <a name="overview"></a>개요

암호는 지연 사용자는 해독 하기 쉬운 간단한 암호를 선택 하는 경향이 있도록 거의 모든 곳에서 필요 합니다. `PasswordStrength` ASP.NET AJAX 컨트롤 도구 키트에서 컨트롤 얼마나 적절 한 암호를 확인할 수 있습니다.

## <a name="steps"></a>단계

`PasswordStrength` 컨트롤을 텍스트 상자를 확장 하 고에서 암호가 충분히 강력한 인지를 확인 합니다. 다양 한 특성을 통해 옵션 제공 그 중 일부만 다음과 같습니다.

- `MinimumNumericCharacters` 암호에 필요한 숫자 문자의 최소 개수
- `MinimumSymbolCharacters` 최소 기호 문자 (문자 및 숫자 하지) 암호에 필요한
- `PreferredPasswordLength` 암호의 최소 길이
- `RequiresUpperAndLowerCaseCharacters` 암호를 대문자 및 소문자 모두 문자를 사용 해야 하는 여부

`StrengthIndicatorType` 텍스트로 암호의 강도 제공 하는 방법 정보를 제공 합니다 (값 `"Text"`) 또는 진행률 표시줄의 한 종류로 (값 `"BarIndicator"`). 에 `DisplayPosition` 특성을 구성한 정보가 표시 됩니다. ASP.NET AJAX를 포함 한 전체 예제는 다음과 같습니다 `ScriptManager` 컨트롤의 `PasswordStrength` 제어 및 물론 사용자 암호를 입력할 수 있는 텍스트 상자입니다. 데모를 보려면 위해 후자 폼 필드 입력 내용을 개발 하는 동안 볼 수 있도록 일반 텍스트 필드 및 암호 필드가 아닙니다 됩니다.

[!code-aspx[Main](testing-the-strength-of-a-password-vb/samples/sample1.aspx)]

페이지를 실행 하 고 다른 페이지로 입력: 암호 같이 엔터티로 간주 소문자, 대문자, 숫자 및 기호를 입력 한 후에 합니다.


[![암호는 () 활동적 이제](testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)

암호는 () 활동적 ([전체 크기 이미지를 보려면 클릭](testing-the-strength-of-a-password-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](testing-the-strength-of-a-password-cs.md)
