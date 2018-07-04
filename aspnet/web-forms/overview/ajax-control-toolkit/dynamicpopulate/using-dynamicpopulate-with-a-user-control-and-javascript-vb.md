---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
title: 사용자 정의 컨트롤 및 JavaScript (VB)에 DynamicPopulate 사용 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에 DynamicPopulate 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 t 대상 컨트롤에 결과 값을 채웁니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 778b9009-76f2-4665-940e-afc0e35bc917
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: 6ab979347a3f412e3225a58a133ae63fcae0a11a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37365596"
---
<a name="using-dynamicpopulate-with-a-user-control-and-javascript-vb"></a>사용자 정의 컨트롤 및 JavaScript (VB)에 DynamicPopulate 사용
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)

> ASP.NET AJAX Control Toolkit에 DynamicPopulate 제어는 웹 서비스 (또는 페이지 메서드)를 호출 하 고 페이지 새로 고침 없이 페이지에서 대상 컨트롤에 결과 값을 채웁니다. 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 채우기를 트리거할 수 이기도 합니다. 그러나 특별 한 주의 extender는 사용자 정의 컨트롤에 상주 하는 경우 수행 해야 합니다.


## <a name="overview"></a>개요

`DynamicPopulate` ASP.NET AJAX Control Toolkit의 컨트롤을 웹 서비스 (또는 페이지 메서드)를 호출 하 고 페이지 새로 고침 없이 페이지에서 대상 컨트롤에 결과 값을 채웁니다. 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 채우기를 트리거할 수 이기도 합니다. 그러나 특별 한 주의 extender는 사용자 정의 컨트롤에 상주 하는 경우 수행 해야 합니다.

## <a name="steps"></a>단계

먼저 하 여 호출할 메서드를 구현 하는 ASP.NET 웹 서비스는 `DynamicPopulateExtender` 제어 합니다. 웹 서비스 메서드를 구현 `getDate()` 문자열 형식의 호출 인수 하나가 필요한 `contextKey`, 이후는 `DynamicPopulate` 컨트롤이 각 웹 서비스 호출을 사용 하 여 한 가지 상황에 맞는 정보를 전송 합니다. 코드는 다음과 같습니다 (파일 `DynamicPopulate.vb.asmx`)을 검색 하는 세 가지 형식 중 하나에 현재 날짜:

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample1.aspx)]

다음 단계에서는 새 사용자 컨트롤을 만듭니다 (`.ascx` 파일), 첫 번째 줄에 다음 선언에 의해 나타내는:

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample2.aspx)]

A &lt; `label` &gt; 서버에서 가져온 데이터를 표시할 요소가 사용 됩니다.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample3.aspx)]

또한 사용자 정의 컨트롤 파일에서는 사용 하 여 세 개의 라디오 단추, 웹 서비스에서 지 원하는 세 가지 가능한 날짜 형식 중 하나를 나타내는 각각. 라디오 단추 중 하나에서 사용자가 브라우저에는 다음과 같은 JavaScript 코드를 실행 됩니다.

[!code-powershell[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample4.ps1)]

이 코드에 액세스 합니다 `DynamicPopulateExtender` (이상한 ID에 대 한 걱정 하지 마십시오 아직 나중에 다룹니다) 하 고 데이터를 사용 하 여 동적 채우기를 트리거합니다. 현재 라디오 단추의 컨텍스트에서 `this.value` 해당 값은 참조 `format1`, `format2` 또는 `format3` 정확 하 게 웹 메서드에 필요한 것입니다.

아직 사용자 정의 컨트롤에서 누락 된 유일한 항목은는 `DynamicPopulateExtender` 웹 서비스에 연결 하는 라디오 단추 컨트롤입니다.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample5.aspx)]

컨트롤에 사용 되는 이상한 ID를 적어 둡니다 있습니다 다시: `mcd1$myDate` 대신 `myDate`합니다. 이전에 JavaScript 코드를 `mcd1_dpe1` 액세스 하는 `DynamicPopulateExtender` 대신 `dpe1`합니다. 사용 하는 경우이 명명 전략은 특별 한 요구 사항 `DynamicPopulateExtender` 사용자 컨트롤입니다. 또한 모든 작동 하도록 특정 방식으로 사용자 컨트롤을 포함 해야 합니다. 새 ASP.NET 페이지를 만들고 방금 구현한 사용자 컨트롤에 대 한 태그 접두사를 등록 합니다.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample6.aspx)]

ASP.NET AJAX를 포함 한 `ScriptManager` 새 페이지 컨트롤:

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample7.aspx)]

마지막으로, 페이지에 사용자 정의 컨트롤을 추가 합니다. 설정 해야 해당 `ID` 특성 (및 `runat="server"`물론,), 특정 이름으로 설정 해야 하지만: `mcd1` JavaScript를 사용 하 여 액세스 사용자 정의 컨트롤 내에서 사용 된 접두사 이기 때문입니다.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample8.aspx)]

됐습니다! 페이지에는 예상 대로 동작 하는지: 사용자가 라디오 단추 중 하나에서 컨트롤 도구 키트에서 웹 서비스를 호출 하 고 원하는 형식으로 현재 날짜를 표시 합니다.


[![사용자 정의 컨트롤에 있는 라디오 단추](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)

사용자 정의 컨트롤에 있는 라디오 단추 ([클릭 하 여 큰 이미지 보기](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](dynamically-populating-a-control-using-javascript-code-vb.md)
