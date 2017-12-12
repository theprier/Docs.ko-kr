---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-cs
title: "JavaScript 코드 (C#)를 사용 하 여 컨트롤을 동적으로 채우는 | Microsoft Docs"
author: wenz
description: "ASP.NET AJAX 컨트롤 도구 키트에서 DynamicPopulate 제어 웹 서비스 (또는 페이지 메서드)를 호출 및 t 대상 컨트롤에 결과 값을 채우는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: cc4c2def-e88c-4456-ae8b-a6ae0ff8cc2d
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 5b3b23e16f2e4dd26f50eb3e07f35d078dd19a19
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="dynamically-populating-a-control-using-javascript-code-c"></a>JavaScript 코드 (C#)를 사용 하 여 컨트롤을 동적으로 채울
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1CS.pdf)

> ASP.NET AJAX 컨트롤 도구 키트에서 DynamicPopulate 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 없이 페이지 새로 고침 페이지에서 대상 컨트롤에 결과 값을 채웁니다. 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 모집단을 트리거할 수 이기도 합니다.


## <a name="overview"></a>개요

`DynamicPopulate` 제어는 ASP.NET AJAX 컨트롤 도구 키트에서 웹 서비스 (또는 페이지 메서드)를 호출 하 고 대상 컨트롤 페이지 새로 고침 없이 페이지에 결과 값을 채웁니다. 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 모집단을 트리거할 수 이기도 합니다.

## <a name="steps"></a>단계

ASP.NET 웹 서비스 호출 될 메서드를 구현 하는 우선, 해야는 `DynamicPopulateExtender` 제어 합니다. 웹 서비스 메서드를 구현 `getDate()` 인수 이라는 형식 문자열 중 하나 필요로 하 `contextKey`, 이후는 `DynamicPopulate` 컨트롤 각 웹 서비스 호출에 컨텍스트 정보의 한 부분을 보냅니다. 코드는 다음과 같습니다 (파일 `DynamicPopulate.cs.asmx`) 세 가지 형식 중 하나에 현재 날짜를 검색 하는 합니다.

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample1.aspx)]

다음 단계에서는 새 ASP.NET 사이트를 만들고 ASP.NET AJAX ScriptManager 컨트롤으로 시작 합니다.

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample2.aspx)]

레이블 컨트롤을 추가 합니다 (예를 들어 이름이 같은 HTML 컨트롤을 사용 하 여 또는 `<asp:Label />` 웹 컨트롤) 웹 서비스 호출의 결과 나중에 표시 됩니다입니다.

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample3.aspx)]

다음으로, 포함 된 `DynamicPopulateExtender` 제어 하 고 웹 서비스 정보, 대상 컨트롤 이지만 사용자 지정 JavaScript를 사용 하 여 나중에 수행 하는 모집단을 트리거하는 컨트롤의 이름이 아니라 제공!

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample4.aspx)]

JavaScript 부분입니다. `$find()` ASP.NET AJAX 라이브러리에 정의 된 함수 등의 ASP.NET AJAX 컨트롤 도구 키트 서버 측 개체에 대 한 참조를 반환 `DynamicPopulateExtender`합니다. 현재 파일에 `$find("dpe")` 것에 대 한 참조를 반환 `DynamicPopulateExtender` 페이지에서 제어 합니다. 라는 메서드가 노출 `populate()` 동적 채우기 프로세스를 트리거합니다. `populate()` 메서드는 하나의 인수가 필요:에 대 한 인수 역할을 수행 하는 상황에 맞는 키는 `getDate()` 웹 메서드. 예를 들어 `$find("dpe").populate("format1")` 월-일-연도 형식의 현재 날짜를 사용 하 여 레이블의 구성 합니다.

이 샘플을 좀 더 유연 하 게 하기 위해 사용자가 다양 한 날짜 형식을 이제 선택 될 수 있습니다. 그 중 한 각 라디오 단추가 표시 됩니다. 한 번 라디오 단추에서 사용자가 클릭 JavaScript 코드 동적으로 채우는 선택한 날짜 형식을 사용 하 여 레이블을 합니다. 다음은 이러한 라디오 단추입니다.

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-cs/samples/sample5.aspx)]

라디오 단추를 JavaScript 식의 컨텍스트 내에 유의 `this.value` 정확히 동일한 정보에는 현재 단추의 값을 참조 하는 `getDate()` 메서드와 함께 사용할 수 있습니다.


[![지정 된 형식으로 서버에서 날짜를 검색 하는 단추를 클릭](dynamically-populating-a-control-using-javascript-code-cs/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-cs/_static/image1.png)

지정 된 형식으로 서버에서 날짜를 검색 하는 단추를 클릭 ([전체 크기 이미지를 보려면 클릭](dynamically-populating-a-control-using-javascript-code-cs/_static/image3.png))

>[!div class="step-by-step"]
[이전](dynamically-populating-a-control-cs.md)
[다음](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
