---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-cs
title: DynamicPopulate를 사용 하 여 사용자 정의 컨트롤 및 JavaScript (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트에서 DynamicPopulate 제어 웹 서비스 (또는 페이지 메서드)를 호출 및 t 대상 컨트롤에 결과 값을 채우는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 38ac8250-8854-444c-b9ab-8998faa41c5a
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-cs
msc.type: authoredcontent
ms.openlocfilehash: cced645733375de7ab6235efa46b8d20ed262e50
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="using-dynamicpopulate-with-a-user-control-and-javascript-c"></a>DynamicPopulate를 사용 하 여 사용자 정의 컨트롤 및 JavaScript (C#)
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2CS.pdf)

> ASP.NET AJAX 컨트롤 도구 키트에서 DynamicPopulate 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 없이 페이지 새로 고침 페이지에서 대상 컨트롤에 결과 값을 채웁니다. 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 모집단을 트리거할 수 이기도 합니다. 하지만 특별 한 주의 extender 사용자 정의 컨트롤에 있는 경우 수행할에 있습니다.


## <a name="overview"></a>개요

`DynamicPopulate` 제어는 ASP.NET AJAX 컨트롤 도구 키트에서 웹 서비스 (또는 페이지 메서드)를 호출 하 고 대상 컨트롤 페이지 새로 고침 없이 페이지에 결과 값을 채웁니다. 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 모집단을 트리거할 수 이기도 합니다. 하지만 특별 한 주의 extender 사용자 정의 컨트롤에 있는 경우 수행할에 있습니다.

## <a name="steps"></a>단계

ASP.NET 웹 서비스 호출 될 메서드를 구현 하는 우선, 해야는 `DynamicPopulateExtender` 제어 합니다. 웹 서비스 메서드를 구현 `getDate()` 인수 이라는 형식 문자열 중 하나 필요로 하 `contextKey`, 이후는 `DynamicPopulate` 컨트롤 각 웹 서비스 호출에 컨텍스트 정보의 한 부분을 보냅니다. 코드는 다음과 같습니다 (파일 `DynamicPopulate.cs.asmx`) 세 가지 형식 중 하나에 현재 날짜를 검색 하는 합니다.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample1.aspx)]

다음 단계에서 새 사용자 정의 컨트롤을 만듭니다 (`.ascx` 파일), 그 첫 번째 줄에 다음 선언으로 표시 합니다.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample2.aspx)]

A &lt; `label` &gt; 요소는 서버에서 가져온 데이터를 표시 하는 데 사용 됩니다.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample3.aspx)]

또한 사용자 정의 컨트롤 파일 사용 세 개의 라디오 단추, 웹 서비스에서 지 원하는 세 가지 가능한 형식 중 하나를 나타내는 각각. 라디오 단추 중 하나에서 사용자가 브라우저 그러면 다음과 같은 JavaScript 코드를 실행 합니다.

[!code-powershell[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample4.ps1)]

이 코드에 액세스는 `DynamicPopulateExtender` (이상한 ID에 대 한 걱정 하지 마십시오 아직, 나중에 설명 합니다.) 및 데이터와 동적 채우기를 트리거합니다. 현재 라디오 단추의 컨텍스트에서 `this.value` 참조 하는 값이 해당 `format1`, `format2` 또는 `format3` 정확 하 게 웹 메서드가 기대 합니다.

아직 사용자 정의 컨트롤에서 누락 된 유일한 항목은 `DynamicPopulateExtender` 컨트롤의 라디오 단추에 웹 서비스에 연결 합니다.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample5.aspx)]

컨트롤에 사용 되는 이상한 ID를 발견할 수 있습니다 다시: `mcd1$myDate` 대신 `myDate`합니다. 이전에 사용 되는 JavaScript 코드 `mcd1_dpe1` 액세스로는 `DynamicPopulateExtender` 대신 `dpe1`합니다. 이 명명 전략은 특별 한 요구 사항을 사용 하는 경우 `DynamicPopulateExtender` 사용자 정의 컨트롤입니다. 또한 모든 작업이 이루어지는를 특정 방식으로에 사용자 컨트롤을 포함 해야 합니다. 새 ASP.NET 페이지를 만들고 방금 구현 된 사용자 정의 컨트롤에 대 한 태그 접두사를 등록 합니다.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample6.aspx)]

그런 다음 ASP.NET AJAX 포함 `ScriptManager` 새 페이지에 컨트롤:

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample7.aspx)]

페이지에 마지막으로, 사용자 정의 컨트롤을 추가 합니다. 만 설정 해야 해당 `ID` 특성 (및 `runat="server"`물론,), 특정 이름으로 설정 해야 하지만: `mcd1` 이 JavaScript를 사용 하 여 액세스 하는 사용자 정의 컨트롤 내에서 사용 되는 접두사입니다.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample8.aspx)]

됐습니다! 예상 대로 동작 하는 페이지: 라디오 단추 중 하나에 사용자가 클릭, 제어 도구 키트에 웹 서비스를 호출 하 고 원하는 형식으로 현재 날짜를 표시 합니다.


[![사용자 정의 컨트롤에 있는 라디오 단추](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image1.png)

사용자 정의 컨트롤에 있는 라디오 단추 ([전체 크기 이미지를 보려면 클릭](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image3.png))

> [!div class="step-by-step"]
> [이전](dynamically-populating-a-control-using-javascript-code-cs.md)
> [다음](dynamically-populating-a-control-vb.md)
