---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-vb
title: 동적으로 Accordion 창 (VB)를 추가 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 Accordion 컨트롤 여러 창을 제공 하 고 둘 중 한 번에 표시할 수 있습니다. 일반적으로 패널 w 선언 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: fae968c9-1902-487d-b053-86a46dd52c3f
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-vb
msc.type: authoredcontent
ms.openlocfilehash: 3dd82fab03e06aa5dd3baba7dd24734fa964b350
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37378964"
---
<a name="dynamically-adding-an-accordion-pane-vb"></a>동적으로 Accordion 창 (VB)를 추가
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2VB.pdf)

> AJAX Control Toolkit의 Accordion 컨트롤 여러 창을 제공 하 고 둘 중 한 번에 표시할 수 있습니다. 패널은 일반적으로 페이지 자체 내에서 선언 하지만 서버 쪽 코드를 사용 하 여 동일한 결과 얻을 수 있습니다.


## <a name="overview"></a>개요

AJAX Control Toolkit의 Accordion 컨트롤 여러 창을 제공 하 고 둘 중 한 번에 표시할 수 있습니다. 패널은 일반적으로 페이지 자체 내에서 선언 하지만 서버 쪽 코드를 사용 하 여 동일한 결과 얻을 수 있습니다.

## <a name="steps"></a>단계

Accordion 컨트롤 서버 쪽 코드에 모든 중요 한 속성을 표시 합니다. 무엇 보다도 `Panes` 속성은 Accordion을 구성 하는 창의 컬렉션에 대 한 액세스 권한을 부여 합니다. 형식의 모든 창 `AccordionPane`합니다. 따라서 이러한 창을 만드는 간단 합니다.

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample1.vb)]

`HeaderContainer` 의 속성 `AccordionPane` ; 창의 헤더 섹션 내에 있는 ASP.NET 컨트롤에 대 한 액세스를 제공 합니다 `ContentContainer` 의 속성 `AccordionPane` 창의 콘텐츠 섹션에 대 한 동일한 작업을 수행 합니다. 이 ASP.NET 코드를 창에 내용을 추가할 수 있습니다.

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample2.vb)]

마지막으로 pane(s) 추가 해야 합니다는 `Panes` 는 Accordion 컬렉션:

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample3.vb)]

두 개의 창이 Accordion 컨트롤에 추가 하는 전체 서버 쪽 코드는 다음과 같습니다.

[!code-aspx[Main](dynamically-adding-an-accordion-pane-vb/samples/sample4.aspx)]

누락 된 유일한 요소는 ASP.NET의 유무에 따라 달라 지는 자체 Accordion `ScriptManager` 제어 합니다.

[!code-aspx[Main](dynamically-adding-an-accordion-pane-vb/samples/sample5.aspx)]

Accordion 컨트롤에서 참조 하는 두 개의 CSS 클래스 예제를 완료 하려면 브라우저에 대 한 스타일 정보를 제공 합니다.

[!code-css[Main](dynamically-adding-an-accordion-pane-vb/samples/sample6.css)]


[![accordion에 데이터를 서버 쪽 코드에서 동적으로 추가](dynamically-adding-an-accordion-pane-vb/_static/image2.png)](dynamically-adding-an-accordion-pane-vb/_static/image1.png)

서버 쪽 코드에서 동적으로 추가한는 accordion에 데이터 ([클릭 하 여 큰 이미지 보기](dynamically-adding-an-accordion-pane-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](databinding-to-an-accordion-vb.md)
