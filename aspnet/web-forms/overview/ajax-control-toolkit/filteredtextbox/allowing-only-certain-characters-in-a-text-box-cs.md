---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-cs
title: "텍스트 상자 (C#)에 특정 문자만 허용 | Microsoft Docs"
author: wenz
description: "ASP.NET 유효성 검사 컨트롤은 사용자 입력에만 특정 문자는 사용할 수 있는지 확인할 수 있습니다. 그러나이 여전히 하더라도 사용자 입력에서 잘못 된..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: fd2a1c52-d717-44af-8a61-67c8279bb26e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-cs
msc.type: authoredcontent
ms.openlocfilehash: 246c3b5dd55ceb0f47ad1f4982ae5b3bf855e747
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="allowing-only-certain-characters-in-a-text-box-c"></a>텍스트 상자 (C#)에 특정 문자를 허용합니다.
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0CS.pdf)

> ASP.NET 유효성 검사 컨트롤은 사용자 입력에만 특정 문자는 사용할 수 있는지 확인할 수 있습니다. 그러나이 여전히 때도 사용자가 잘못 된 문자를 입력 하 고 양식을 제출 하려고 합니다.


## <a name="overview"></a>개요

ASP.NET 유효성 검사 컨트롤은 사용자 입력에만 특정 문자는 사용할 수 있는지 확인할 수 있습니다. 그러나이 여전히 때도 사용자가 잘못 된 문자를 입력 하 고 양식을 제출 하려고 합니다.

## <a name="steps"></a>단계

ASP.NET AJAX 컨트롤 Toolkit에 포함 되어는 `FilteredTextBox` 입력란을 확장 하는 제어 합니다. 활성화 되 면 특정 문자 집합만 필드에 입력할 수 있습니다.

이렇게 하려면 먼저 필요 평소와 같이 ASP.NET AJAX `ScriptManager` 도 ASP.NET AJAX 컨트롤 도구 키트에서 사용 되는 JavaScript 라이브러리를 로드 합니다.

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample1.aspx)]

그런 다음 텍스트 상자를 해야합니다.

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample2.aspx)]

마지막으로 `FilteredTextBoxExtender` 컨트롤 형식으로 사용자가 허용 되는 문자 제한의 담당 합니다. 먼저, 설정 된 `TargetControlID` 특성을 `ID` 의 `TextBox` 제어 합니다. 그런 다음 중 하나를 선택 `FilterType` 값:

- `Custom`기본; 유효한 문자 목록을 지정 해야 합니다.
- `LowercaseLetters`소문자만
- `Numbers`숫자만
- `UppercaseLetters`대문자만

경우는 `Custom FilterType` 사용 되는 `ValidChars` 속성 설정 해야 하며 형식화 될 수 있는 문자 목록을 제공 합니다. 그런데: 텍스트 상자에 텍스트를 시도 하는 경우 모든 잘못 된 문자 제거 됩니다.

여기에 대 한 태그는는 `FilteredTextBoxExtender` 만 자리 숫자를 허용 하는 컨트롤 (또한 되었을 수 있는 `FilterType="Numbers"`):

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-cs/samples/sample3.aspx)]

JavaScript가 설정 된 경우에 문자를 입력 하 고 페이지를 실행이 작동 하지 않습니다. 그러나 숫자 페이지에 표시 됩니다. 그러나 유의 보호 `FilteredTextBox` 제공 글머리 기호 증명 않습니다: 경우 JavaScript가 사용, 데이터 추가 유효성 검사 방법 즉, ASP를 사용 해야 하므로 텍스트 상자에 입력할 수 있습니다. NET의 유효성 검사를 제어 합니다.


[![숫자만 입력할 수](allowing-only-certain-characters-in-a-text-box-cs/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-cs/_static/image1.png)

숫자만 입력할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](allowing-only-certain-characters-in-a-text-box-cs/_static/image3.png))

>[!div class="step-by-step"]
[다음](allowing-only-certain-characters-in-a-text-box-vb.md)
