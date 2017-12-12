---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
title: "동적으로 (VB) 컨트롤을 채우는 | Microsoft Docs"
author: wenz
description: "ASP.NET AJAX 컨트롤 도구 키트에서 DynamicPopulate 제어 웹 서비스 (또는 페이지 메서드)를 호출 및 t 대상 컨트롤에 결과 값을 채우는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 27305347-7b5d-4519-97b7-197a357e7f6e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: ec0b6d429f3eb4a7243201c2a91adde462cf6345
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="dynamically-populating-a-control-vb"></a>동적으로 채울 컨트롤 (VB)
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0VB.pdf)

> ASP.NET AJAX 컨트롤 도구 키트에서 DynamicPopulate 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 없이 페이지 새로 고침 페이지에서 대상 컨트롤에 결과 값을 채웁니다.


## <a name="overview"></a>개요

`DynamicPopulate` 제어는 ASP.NET AJAX 컨트롤 도구 키트에서 웹 서비스 (또는 페이지 메서드)를 호출 하 고 대상 컨트롤 페이지 새로 고침 없이 페이지에 결과 값을 채웁니다. 이 자습서에는이 작업을 설정 하는 방법을 보여 줍니다.

## <a name="steps"></a>단계

메서드 호출을 구현 하는 ASP.NET 웹 서비스를 필요 우선, `DynamicPopulate`합니다. 웹 서비스 클래스에 필요한는 `ScriptService` 내에 정의 된 특성 `Microsoft.Web.Script.Services`; ASP.NET AJAX에 필요한는 웹 서비스에 대 한 클라이언트 쪽 JavaScript 프록시를 만들 수 없습니다 그렇지 않으면 `DynamicPopulate`합니다.

웹 메서드는 string 형식의 라는 하나의 인수를 예상 해야 `contextKey`, 이후는 `DynamicPopulate` 컨트롤 각 웹 서비스 호출에 컨텍스트 정보의 한 부분을 보냅니다. 가 나타내는 형식의 현재 날짜를 반환 하는 다음 웹 서비스는 `contextKey` 인수:

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample1.aspx)]

웹 서비스는 다음으로 저장 됩니다 `DynamicPopulate.vb.asmx`합니다. 구현할 수 있습니다는 `getDate()` 메서드 사용 하 여 실제 ASP.NET 페이지 내에서 페이지 메서드로 `DynamicPopulate` 제어 합니다.

다음 단계에서는 새 ASP.NET 파일을 만듭니다. 포함 하는 첫 번째 단계는 항상 그렇지는 것 처럼는 `ScriptManager` ASP.NET AJAX 라이브러리를 로드 하 고 제어 도구 키트 작업을 확인 하는 현재 페이지에:

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample2.aspx)]

레이블 컨트롤을 추가 합니다 (예를 들어 이름이 같은 HTML 컨트롤을 사용 하 여 또는 &lt; `asp:Label`  / &gt; 웹 컨트롤) 웹 서비스 호출의 결과 나중에 표시 됩니다입니다.

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample3.aspx)]

HTML 컨트롤을 서버에 다시 게시 하지 않아도 म 때문) (같은 HTML 단추는 다음 트리거하는 데 사용할 동적 채우기:

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample4.aspx)]

끝으로 `DynamicPopulateExtender` 높이려면 통신을 제어 합니다. 다음과 같은 특성을 설정 합니다 (명백한 것 외에도 `ID` 및 `runat` = `"server"`):

- `TargetControlID`웹 서비스 호출 로부터 결과 삽입 하는 위치
- `ServicePath`웹 서비스에 대 한 경로 (페이지 메서드를 사용 하려는 경우 생략)
- `ServiceMethod`웹 메서드 또는 페이지 메서드 이름
- `ContextKey`컨텍스트 정보를 웹 서비스에 보내도록
- `PopulateTriggerControlID`웹 서비스 호출을 트리거하는 요소
- `ClearContentsDuringUpdate`웹 서비스 호출 하는 동안 대상 요소 비워지도록 여부

볼 수 있듯이 컨트롤 몇 가지 정보가 필요 하지만 매우 간단한 것은 모든 것을 제자리에 배치 합니다. 여기에 대 한 태그는는 `DynamicPopulateExtender` 현재 시나리오에는 제어:

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample5.aspx)]

브라우저에서 ASP.NET 페이지를 실행 하 고 단추; 클릭 월-일-연도 형식의 현재 날짜를 받습니다.


[![서버에서 날짜를 검색 하는 단추 클릭](dynamically-populating-a-control-vb/_static/image2.png)](dynamically-populating-a-control-vb/_static/image1.png)

서버에서 날짜를 검색 하는 단추 클릭 ([전체 크기 이미지를 보려면 클릭](dynamically-populating-a-control-vb/_static/image3.png))

>[!div class="step-by-step"]
[이전](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
[다음](dynamically-populating-a-control-using-javascript-code-vb.md)
