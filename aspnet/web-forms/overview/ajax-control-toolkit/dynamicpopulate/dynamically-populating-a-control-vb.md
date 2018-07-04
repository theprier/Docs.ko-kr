---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
title: 동적으로 컨트롤 (VB)를 채우기 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에 DynamicPopulate 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 t 대상 컨트롤에 결과 값을 채웁니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 27305347-7b5d-4519-97b7-197a357e7f6e
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: fd55b59f9375eb320711ffea8d971a8d86179c43
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37368662"
---
<a name="dynamically-populating-a-control-vb"></a>동적으로 채울 컨트롤 (VB)
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0VB.pdf)

> ASP.NET AJAX Control Toolkit에 DynamicPopulate 제어는 웹 서비스 (또는 페이지 메서드)를 호출 하 고 페이지 새로 고침 없이 페이지에서 대상 컨트롤에 결과 값을 채웁니다.


## <a name="overview"></a>개요

`DynamicPopulate` ASP.NET AJAX Control Toolkit의 컨트롤을 웹 서비스 (또는 페이지 메서드)를 호출 하 고 페이지 새로 고침 없이 페이지에서 대상 컨트롤에 결과 값을 채웁니다. 이 자습서에는이를 설정 하는 방법을 보여 줍니다.

## <a name="steps"></a>단계

호출할 메서드를 구현 하는 ASP.NET 웹 서비스 해야 먼저 `DynamicPopulate`합니다. 웹 서비스 클래스에 필요 합니다 `ScriptService` 내에 정의 된 특성 `Microsoft.Web.Script.Services`; ASP.NET AJAX에 필요한 웹 서비스에 대 한 클라이언트 쪽 JavaScript 프록시를 만들 수 없습니다이 고, 그렇지 `DynamicPopulate`합니다.

웹 메서드는 문자열 형식의 호출 인수 하나를 예상 해야 합니다 `contextKey`, 이후는 `DynamicPopulate` 컨트롤이 각 웹 서비스 호출을 사용 하 여 한 가지 상황에 맞는 정보를 전송 합니다. 표시 형식으로 현재 날짜를 반환 하는 다음 웹 서비스는 `contextKey` 인수:

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample1.aspx)]

웹 서비스로 저장 됩니다 `DynamicPopulate.vb.asmx`합니다. 구현할 수 있습니다 합니다 `getDate()` 실제 ASP.NET 페이지 내에서 페이지 메서드로 메서드를 `DynamicPopulate` 제어 합니다.

다음 단계에서는 새 ASP.NET 파일을 만듭니다. 포함할 첫 번째 단계는 항상를 `ScriptManager` ASP.NET AJAX 라이브러리를 로드 하 고 컨트롤 도구 키트 작동 하도록 현재 페이지에서:

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample2.aspx)]

그런 다음 레이블 컨트롤을 추가 (예를 들어 이름이 같은 HTML 컨트롤을 사용 하 여 또는 &lt; `asp:Label`  / &gt; 웹 컨트롤)는 나중에 웹 서비스 호출의 결과 표시 됩니다.

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample3.aspx)]

다음 HTML 단추 (컨트롤로 HTML에서는 서버로 다시 게시 하지 않아도 되므로) 동적 채우기를 트리거할 수 사용 됩니다.

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample4.aspx)]

끝으로 `DynamicPopulateExtender` 실시간 작업을 제어 합니다. 다음과 같은 특성 설정이 적용 됩니다 (확실 한 것 외에도 `ID` 하 고 `runat` = `"server"`):

- `TargetControlID` 웹 서비스 호출에서 결과 넣을 위치
- `ServicePath` 웹 서비스에 대 한 경로 (페이지 메서드를 사용 하려는 경우 생략)
- `ServiceMethod` 웹 메서드나 페이지 메서드에 이름
- `ContextKey` 웹 서비스에 보낼 컨텍스트 정보
- `PopulateTriggerControlID` 웹 서비스 호출을 트리거하는 요소
- `ClearContentsDuringUpdate` 웹 서비스 호출 하는 동안 대상 요소를 빈 것인지

알 수 있듯이 컨트롤 몇 가지 정보가 필요 이지만 위치에 배치 하는 모든 방법은 매우 간단 합니다. 여기에 대 한 태그는 `DynamicPopulateExtender` 현재 시나리오에는 제어:

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample5.aspx)]

브라우저에서 ASP.NET 페이지를 실행 하 고 단추 클릭 월-일-연도 형식의 현재 날짜를 받게 됩니다.


[![서버에서 날짜를 검색 하는 단추 클릭](dynamically-populating-a-control-vb/_static/image2.png)](dynamically-populating-a-control-vb/_static/image1.png)

서버에서 날짜를 검색 하는 단추 클릭 ([클릭 하 여 큰 이미지 보기](dynamically-populating-a-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
> [다음](dynamically-populating-a-control-using-javascript-code-vb.md)
