---
uid: mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-vb
title: "JavaScript 주입 공격 방지 (VB) | Microsoft Docs"
author: StephenWalther
description: "JavaScript 주입 공격 및 사이트 간 스크립팅 공격을 상황이 발생을 방지 합니다. 이 자습서에서는 Stephen Walther 하는 방법을 쉽게 de 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/19/2008
ms.topic: article
ms.assetid: 9274a72e-34dd-4dae-8452-ed733ae71377
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-vb
msc.type: authoredcontent
ms.openlocfilehash: 1d49d4d1afa30247d3452a96c8004441ba417ac8
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="preventing-javascript-injection-attacks-vb"></a>JavaScript 주입 공격 방지 (VB)
====================
으로 [Stephen Walther](https://github.com/StephenWalther)

[PDF 다운로드](http://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_06_VB.pdf)

> JavaScript 주입 공격 및 사이트 간 스크립팅 공격을 상황이 발생을 방지 합니다. 이 자습서에서는 Stephen Walther 이러한 종류의 HTML 콘텐츠 인코딩에 의해 공격이 쉽게 실패할 수는 방법을 설명 합니다.


이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 JavaScript 주입 공격을 방지 하는 방법에 대해 설명 하는입니다. 이 자습서에서는 JavaScript 삽입 공격 으로부터 웹 사이트를 보호 하는 데 두 가지 방법에 설명 합니다. 표시할 데이터를 인코딩하여 JavaScript 주입 공격을 방지 하는 방법을 배웁니다. 동의 하는 데이터를 인코딩하여 JavaScript 주입 공격을 방지 하는 방법을 배웁니다.

## <a name="what-is-a-javascript-injection-attack"></a>JavaScript 주입 공격 무엇입니까?

사용자 입력을 허용 하 고 사용자 입력을 다시 표시 될 때마다 JavaScript 주입 공격에 웹 사이트를 엽니다. JavaScript 주입 공격에 열려 있는 구체적인 응용 프로그램을 살펴보겠습니다.

고객 의견 웹 사이트를 만든 가정해 보세요 (그림 1 참조). 고객 웹 사이트를 방문할 수 및 제품을 사용 하 여 자신의 경험에 피드백을 입력 합니다. 고객이 검토자의 피드백을 제출 하는 피드백 피드백 페이지 다시 표시 됩니다.


[![고객 의견 웹 사이트](preventing-javascript-injection-attacks-vb/_static/image2.png)](preventing-javascript-injection-attacks-vb/_static/image1.png)

**그림 01**: 고객 의견 웹 사이트 ([전체 크기 이미지를 보려면 클릭](preventing-javascript-injection-attacks-vb/_static/image3.png))


사용 하 여 고객 의견 웹 사이트는 `controller` 목록 1에서입니다. 이 `controller` 라는 두 가지 동작 포함 `Index()` 및 `Create()`합니다.

**1 – 나열`HomeController.vb`**

[!code-vb[Main](preventing-javascript-injection-attacks-vb/samples/sample1.vb)]

`Index()` 메서드 표시는 `Index` 보기. 이 메서드는 이전 고객의 의견을 모두 통과 `Index` 피드백 (LINQ to SQL 쿼리를 사용 하 여) 데이터베이스에서 검색 하 여 보기.

`Create()` 메서드는 새 사용자 의견 항목을 만들고 데이터베이스에 추가 합니다. 폼에를 입력 하는 메시지에 전달 되는 `Create()` 메시지 매개 변수에서 메서드로 합니다. 피드백 항목 만들어지고 메시지에 사용자 의견 항목에 할당 되어 `Message` 속성입니다. 피드백 항목으로 데이터베이스에 전송 되는 `DataContext.SubmitChanges()` 메서드를 호출 합니다. 방문자에 다시 리디렉션되면 마지막으로 `Index` 보기의 모든 의견 표시 됩니다.

`Index` 보기 목록 2에 포함 되어 있습니다.

**2 – 나열`Index.aspx`**

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample2.aspx)]

`Index` 보기는 다음 두 섹션이 있습니다. 맨 위 섹션에는 실제 고객 의견 양식을 포함 되어 있습니다. 아래쪽 섹션에는 포함 For... 모든 이전 고객 의견 항목을 반복 하는 각 사용자 의견 항목에 대 한 EntryDate 및 메시지 속성을 표시 하는 각 루프입니다.

고객 의견 웹 사이트는 간단한 웹 사이트입니다. 안타깝게도,는 웹 사이트는 JavaScript 주입 공격에 노출 합니다.

고객 의견 양식으로 다음 텍스트를 입력 같이 가정해 봅니다.

[!code-html[Main](preventing-javascript-injection-attacks-vb/samples/sample3.html)]

이 텍스트는 경고 메시지 상자를 표시 하는 JavaScript 스크립트를 나타냅니다. 이 스크립트를 피드백 제출 누군가가 후 양식에서 메시지 *Boo!* 모든 사용자 고객 의견 웹 사이트에 방문 나중에 (그림 2 참조) 될 때마다 표시 됩니다.


[![JavaScript 주입](preventing-javascript-injection-attacks-vb/_static/image5.png)](preventing-javascript-injection-attacks-vb/_static/image4.png)

**그림 02**: JavaScript 주입 ([전체 크기 이미지를 보려면 클릭](preventing-javascript-injection-attacks-vb/_static/image6.png))


이제 JavaScript 주입 공격에 대 한 초기 응답 apathy 수 있습니다. JavaScript 주입 공격은 유형의 단순히 생각 *손상과* 공격입니다. 아무도 할 수 있는 악의적인 진정으로 아무 것도 JavaScript 주입 공격을 커밋하여 판단할 수도 있습니다.

그러나 해커가 수행할 수 있는 일부, 웹 사이트에 JavaScript를 삽입 하 여 실제로 나쁜 것입니다. 사이트 간 스크립팅 (XSS) 공격을 수행할 JavaScript 주입 공격을 사용할 수 있습니다. 사이트 간 스크립팅 공격이 있습니다 기밀 사용자 정보를 도용 하 고 다른 웹 사이트를 정보를 보냅니다.

예를 들어 해커가 다른 사용자의 브라우저 쿠키의 값을 도용 하 JavaScript 주입 공격을 사용할 수 있습니다. 암호, 신용 카드 번호나 주민 등록 번호 – 같은 중요 한 정보가-브라우저 쿠키에 저장 되는 해커가이 정보를 도용 하는 JavaScript 주입 공격을 사용할 수 있습니다. 또는 사용자가 해커 삽입 된 JavaScript를 사용 하 여 양식 데이터 하 고 다른 웹 사이트에 보낼 수 수 JavaScript 공격을 손상 된 페이지에 포함 된 폼 필드에 중요 한 정보를 입력 합니다.

*사항은 무서*합니다. JavaScript 주입 공격을 심각 하 게 수행 하 고 사용자의 기밀 정보를 보호 합니다. 다음 두 섹션에서는 JavaScript 주입 공격에서 ASP.NET MVC 응용 프로그램을 보호 하는 데 사용할 수 있는 다음 두 가지 기술에 설명 합니다.

## <a name="approach-1-html-encode-in-the-view"></a>보기에 접근 방식 1: HTML 인코딩

JavaScript 주입 공격 방지를 쉽게 HTML 하는 보기에서 데이터를 다시 표시 하면 웹 사이트 사용자가 입력 한 모든 데이터를 인코딩합니다. 업데이트 된 `Index` 는 접근이 방법을 나열 하는 3의 보기입니다.

**3 – 나열 `Index.aspx` (인코딩된 HTML)**

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample4.aspx)]

다음에 유의 값 `feedback.Message` 는 다음 코드와 값이 표시 되기 전에 인코딩된 HTML:

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample5.aspx)]

수행 하는 작업 평균 HTML로 인코딩 문자열로? HTML 인코딩할 때 문자열, 위험 등의 문자 `<` 및 `>` 와 같은 HTML 엔터티 참조로 대체 됩니다 `&lt;` 및 `&gt;`합니다. 따라서 문자열 `<script>alert("Boo!")</script>` 는 HTML으로 변환 가져옵니다 인코딩할 `&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`합니다. 인코딩된 문자열은 더 이상 해석 하는 브라우저에서 JavaScript 스크립트로 실행 합니다. 대신 그림 3에서 무해 한 페이지를 가져옵니다.


[![타원된 JavaScript 공격](preventing-javascript-injection-attacks-vb/_static/image8.png)](preventing-javascript-injection-attacks-vb/_static/image7.png)

**그림 03**: 타원 JavaScript 공격 ([전체 크기 이미지를 보려면 클릭](preventing-javascript-injection-attacks-vb/_static/image9.png))


에 `Index` 목록 3에만 값을 볼 `feedback.Message` 인코딩됩니다. 값 `feedback.EntryDate` 는 인코딩되지 않습니다. 사용자가 입력 한 데이터를 인코딩하려면 하기만 하면 됩니다. 컨트롤러에 생성 된 EntryDate 값 때문에 없습니다 필요를 HTML로 인코딩할이 값입니다.

## <a name="approach-2-html-encode-in-the-controller"></a>컨트롤러에 접근 방식 2: HTML 인코딩

HTML을 할 수 있습니다 HTML 인코딩 데이터 보기에서 데이터를 표시 하는 경우, 대신 바로 데이터를 데이터베이스에 제출 하기 전에 데이터를 인코딩합니다. 이 두 번째 방법은의 경우에 사용 되는 `controller` 4 나열 합니다.

**4 – 나열 `HomeController.cs` (인코딩된 HTML)**

[!code-vb[Main](preventing-javascript-injection-attacks-vb/samples/sample6.vb)]

메시지의 값은 값 내의 데이터베이스에 전송 하기 전에 인코딩된 HTML는 `Create()` 동작 합니다. 보기에서 메시지를 다시 표시 됩니다, 메시지는 HTML로 인코딩되지 않으며 메시지에 지정 된 모든 JavaScript 실행 되지 않습니다.

일반적으로이 두 번째 방식에 비해이 자습서에서 설명 하는 첫 번째 방법은 대개이 있습니다. 이 두 번째 방법은 문제는 /fd HTML로 인코딩된 데이터 데이터베이스의입니다. 즉, 데이터베이스 데이터 재미 있는 찾고 문자로 변경 된 됩니다.

이 이유는 잘못 된? 웹 페이지가 아닌 다른 방식으로 데이터베이스 데이터를 표시 해야 하는 경우 다음은 문제가 있습니다. 예를 들어 Windows Forms 응용 프로그램에서 쉽게 더 이상 데이터를 표시할 수 없습니다.

## <a name="summary"></a>요약

이 자습서의 목적은 JavaScript 주입 공격의 잠재 고객에 대 한 두려워 하는 것 이었습니다. 이 자습서에서는 JavaScript 주입 공격에 대 한 ASP.NET MVC 응용 프로그램을 방어 하기 위한 두 가지 방법을 설명: HTML 중 하나를 수행할 수 있습니다 제출 된 사용자를 인코딩하는 뷰 또는 사용자 데이터를 HTML 수 제출 된 사용자를 인코딩할 컨트롤러에는 데이터입니다.

>[!div class="step-by-step"]
[이전](authenticating-users-with-windows-authentication-vb.md)
