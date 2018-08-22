---
uid: mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-cs
title: JavaScript 주입 공격 방지 (C#) | Microsoft Docs
author: StephenWalther
description: JavaScript 주입 공격 및 사이트 간 스크립팅 공격 발생에서을 방지 합니다. 이 자습서에서는 Stephen walther가 하는 방법을 쉽게 de 설명 하는 중...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: d0136da6-81a4-4815-b002-baa84744c09e
msc.legacyurl: /mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-cs
msc.type: authoredcontent
ms.openlocfilehash: 77d0f0346e9eff756cd74c64c310918f3c367ab1
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41826897"
---
<a name="preventing-javascript-injection-attacks-c"></a>JavaScript 주입 공격 방지 (C#)
====================
[Stephen walther가](https://github.com/StephenWalther)

[PDF 다운로드](http://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_06_CS.pdf)

> JavaScript 주입 공격 및 사이트 간 스크립팅 공격 발생에서을 방지 합니다. 이 자습서에서는 Stephen walther가 이러한 유형의 HTML 콘텐츠 인코딩에 의해 공격을 쉽게 무력화 수 하는 방법을 설명 합니다.


이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 JavaScript 주입 공격을 방지 하는 방법 설명 합니다. 이 자습서에는 JavaScript 주입 공격 으로부터 웹 사이트를 보호 하는 데 두 가지 방법을 설명 합니다. 데이터 표시를 인코딩하여 JavaScript 주입 공격을 방지 하는 방법을 알아봅니다. 동의 하는 데이터를 인코딩하여 JavaScript 주입 공격을 방지 하는 방법을 배웁니다.

## <a name="what-is-a-javascript-injection-attack"></a>JavaScript 주입 공격을 란?

사용자 입력을 허용 하 고 사용자 입력을 다시 표시 될 때마다 JavaScript 주입 공격에 웹 사이트를 엽니다. JavaScript 주입 공격에 개방 된 구체적인 응용 프로그램을 살펴보겠습니다.

고객 피드백 웹 사이트를 만들었다고 가정해 보겠습니다 (그림 1 참조). 고객 웹 사이트를 방문 하 고 제품을 사용 하 여 해당 환경을 피드백 입력 수 있습니다. 고객 피드백을 제출 하는 경우 사용자 의견 피드백 페이지의 다시 표시 됩니다.


[![고객 피드백 웹 사이트](preventing-javascript-injection-attacks-cs/_static/image2.png)](preventing-javascript-injection-attacks-cs/_static/image1.png)

**그림 01**: 고객 피드백 웹 사이트 ([큰 이미지를 보려면 클릭](preventing-javascript-injection-attacks-cs/_static/image3.png))


고객 피드백 웹 사이트를 사용 하는 `controller` 목록 1에서. 이 `controller` 라는 두 가지 동작 포함 `Index()` 및 `Create()`합니다.

**목록 1 – `HomeController.cs`**

[!code-csharp[Main](preventing-javascript-injection-attacks-cs/samples/sample1.cs)]

합니다 `Index()` 메서드 표시는 `Index` 보기. 이 메서드는 모든 이전 고객 피드백에 전달 된 `Index` (LINQ to SQL 쿼리를 사용 하 여) 데이터베이스에서 피드백을 검색 하 여 보기.

`Create()` 메서드는 새 피드백 항목을 만들고 데이터베이스에 추가 합니다. 폼에서를 입력 하는 메시지에 전달 되는 `Create()` 메시지 매개 변수에 메서드. 피드백 항목을 만들고 메시지 피드백 항목에 할당 되어 `Message` 속성입니다. 피드백을 사용 하 여 데이터베이스에 제출 되는 `DataContext.SubmitChanges()` 메서드를 호출 합니다. 마지막으로, 방문자는 리디렉션됩니다는 `Index` 보기의 모든 의견 표시 됩니다.

`Index` 보기가 목록 2에 포함 됩니다.

**2 – 나열 `Index.aspx`**

[!code-aspx[Main](preventing-javascript-injection-attacks-cs/samples/sample2.aspx)]

`Index` 보기에는 두 섹션이 있습니다. 맨 위 섹션에는 실제 고객 피드백이 포함 되어 있습니다. 아래쪽 섹션에는 For 포함... 모든 이전 고객 피드백 항목을 반복 하 고 각 피드백 항목에 대 한 EntryDate 및 메시지 속성을 표시 하는 각 루프입니다.

고객 피드백 웹 사이트는 간단한 웹 사이트입니다. 그러나 웹 사이트는 JavaScript 주입 공격에 열려 있습니다.

고객 사용자 의견 양식으로 다음 텍스트를 입력 하는 가정해 보겠습니다.

[!code-html[Main](preventing-javascript-injection-attacks-cs/samples/sample3.html)]

이 텍스트는 경고 메시지 상자를 표시 하는 JavaScript 스크립트를 나타냅니다. 이 스크립트를 피드백 제출 누군가가 후 양식의 메시지 <em>Boo!</em> 모든 사용자가 고객 피드백 웹 사이트에 방문 앞으로 (그림 2 참조) 될 때마다 표시 됩니다.


[![JavaScript 주입](preventing-javascript-injection-attacks-cs/_static/image5.png)](preventing-javascript-injection-attacks-cs/_static/image4.png)

**그림 02**: JavaScript 주입 ([큰 이미지를 보려면 클릭](preventing-javascript-injection-attacks-cs/_static/image6.png))


이제 JavaScript 주입 공격에 대 한 초기 응답 무관심 수 있습니다. JavaScript 주입 공격의 형식일 뿐는 생각 *파손* 공격입니다. 아무도 작업을 수행 하려면 실제로 악의적인 JavaScript 주입 공격을 커밋하여 않다고 판단할 수도 있습니다.

아쉽게도 해커가 가능 일부 실제로 웹 사이트에 JavaScript를 주입 하 여 실제로 악의적인 작업 합니다. 사이트 간 스크립팅 (XSS) 공격을 수행 하는 JavaScript 주입 공격을 사용할 수 있습니다. 사이트 간 스크립팅 공격, 기밀 사용자 정보를 도용 하 고 다른 웹 사이트에 정보를 전송 합니다.

예를 들어 해커가 값을 다른 사용자의 브라우저 쿠키를 도용 하 JavaScript 주입 공격을 사용할 수 있습니다. 암호, 신용 카드 번호나 주민 등록 번호 – 같은 중요 한 정보는 브라우저 쿠키에 저장 됩니다, 해커가이 정보를 도용 하 JavaScript 주입 공격을를 사용할 수 있습니다. 또는 사용자가 해커는 주입 된 JavaScript를 사용 하 여 폼 데이터를 다른 사이트로 전송 하 수 JavaScript 공격을 사용 하 여 손상 된 페이지에 포함 된 폼 필드에 중요 한 정보를 입력 합니다.

*장단점이 수*입니다. JavaScript 주입 공격을 심각 하 게 수행 하 고 사용자의 기밀 정보를 보호 합니다. 다음 두 섹션에서는 JavaScript 주입 공격 으로부터 ASP.NET MVC 응용 프로그램을 보호 하는 데 사용할 수 있는 두 가지 기술을 설명 합니다.

## <a name="approach-1-html-encode-in-the-view"></a>방법 #1: HTML 보기에서 인코딩

HTML로 JavaScript 주입 공격을 방지 하는 쉬운 방법을 한 가지 뷰에서 데이터를 다시 표시 하면 웹 사이트 사용자가 입력 한 모든 데이터를 인코딩합니다. 업데이트 된 `Index` 보기 목록 3에서은이 접근 방식을 따릅니다.

**코드 3 – `Index.aspx` (인코딩된 HTML)**

[!code-aspx[Main](preventing-javascript-injection-attacks-cs/samples/sample4.aspx)]

값 `feedback.Message` html 값을 다음 코드로 표시 되기 전에 인코딩됩니다.

[!code-aspx[Main](preventing-javascript-injection-attacks-cs/samples/sample5.aspx)]

것 평균 HTML로 인코딩 문자열로? HTML 인코딩할 때 문자열, 위험 등의 문자 `<` 하 고 `>` 와 같은 HTML 엔터티 참조로 대체 됩니다 `&lt;` 및 `&gt;`합니다. 있으므로 문자열 `<script>alert("Boo!")</script>` html 인코딩 변환 `&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`합니다. 인코딩된 문자열은 더 이상 브라우저에서 해석 하는 경우 JavaScript 스크립트로 실행 합니다. 대신, 그림 3에 무해 한 페이지가 나타납니다.


[![패배 JavaScript 공격](preventing-javascript-injection-attacks-cs/_static/image8.png)](preventing-javascript-injection-attacks-cs/_static/image7.png)

**그림 03**: 패배 JavaScript 공격 ([큰 이미지를 보려면 클릭](preventing-javascript-injection-attacks-cs/_static/image9.png))


되었는지 확인 합니다 `Index` 의 값만 목록 3에서 볼 `feedback.Message` 인코딩됩니다. 변수의 `feedback.EntryDate` 는 인코딩되지 않습니다. 사용자가 입력 한 데이터를 인코드 해야 합니다. EntryDate 값 컨트롤러에서 생성 된 때문에 없는 필요한 HTML로 인코딩할이 값입니다.

## <a name="approach-2-html-encode-in-the-controller"></a>컨트롤러의 접근 방식 2: HTML 인코딩

HTML HTML 인코딩 데이터 뷰에서 데이터를 표시 하는 경우, 대신 있습니다 데이터베이스로 데이터를 제출 하기 전에만 데이터를 인코딩합니다. 이 두 번째 방법은의 경우 사용 되는 `controller` 4에서.

**코드 4 – `HomeController.cs` (인코딩된 HTML)**

[!code-csharp[Main](preventing-javascript-injection-attacks-cs/samples/sample6.cs)]

메시지의 값을 HTML 인코딩된 값 내에 데이터베이스에 전송 되기 전에는 `Create()` 동작 합니다. 보기에서 메시지를 다시 표시 됩니다, 경우 메시지 HTML 인코딩해야 이며 메시지에 지정 된 JavaScript 실행 되지 않습니다.

일반적으로이 두 번째 접근 방식을 통해이 자습서에 설명 된 첫 번째 방법은 선호 합니다. 이 두 번째 방법의 문제는 결국 HTML로 인코딩된 데이터를 사용 하 여 데이터베이스의 경우 즉, 데이터베이스 데이터 재미 있는 보이는 문자를 사용 하 여 정리 됩니다.

이 이유는 잘못 된? 웹 페이지 외의 다른 데이터베이스 데이터를 표시 해야 하는 경우 다음은 문제가 있습니다. 예를 들어, Windows Forms 응용 프로그램에서 데이터를 더 이상 쉽게 표시할 수 없습니다.

## <a name="summary"></a>요약

이 자습서의 목적은 JavaScript 주입 공격을 없어질 수 있다는 가능성에 대 한 두려워 하는 것 이었습니다. 이 자습서에는 JavaScript 주입 공격 으로부터 ASP.NET MVC 응용 프로그램을 방어 하기 위한 두 가지 방법을 설명: 할 수 있습니다 하거나 HTML 제출 하는 사용자를 인코딩할 수 있는 HTML 보기에는 데이터 제출 하는 사용자를 인코딩 컨트롤러의 데이터.

> [!div class="step-by-step"]
> [이전](authenticating-users-with-windows-authentication-cs.md)
> [다음](authenticating-users-with-forms-authentication-vb.md)
