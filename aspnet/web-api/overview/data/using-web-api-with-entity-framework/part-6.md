---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-6
title: "JavaScript 클라이언트 만들기 | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 20360326-b123-4b1e-abae-1d350edf4ce4
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-6
msc.type: authoredcontent
ms.openlocfilehash: b397c5a413ae213c9b79da1c0e0626efe21c7e21
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="create-the-javascript-client"></a>JavaScript 클라이언트 만들기
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트를 다운로드 합니다.](https://github.com/MikeWasson/BookService)

이 섹션에서는 HTML, JavaScript를 사용 하 여 응용 프로그램에 대 한 클라이언트 만들어집니다 및 [Knockout.js](http://knockoutjs.com/) 라이브러리입니다. 클라이언트 응용 프로그램을 단계별로 작성할 것:

- 책의 목록을 표시 합니다.
- 책 자세한 정보를 표시 합니다.
- 새 책을 추가 합니다.

Knockout 라이브러리 모델-뷰-MVVM () 패턴을 사용합니다.

- **모델** (대/소문자에 책 저자) 비즈니스 도메인에 있는 데이터의 서버 쪽 표현입니다.
- **보기** 프레젠테이션 계층 (HTML)입니다.
- **뷰 모델** 은 모델을 포함 하는 JavaScript 개체입니다. 뷰 모델은 UI의 코드 추상화입니다. 그는 HTML 표현의 알지 못합니다. 대신, 나타내는 보기의 추상 기능와 같은 &quot;책의 목록이&quot;합니다.

뷰 데이터 바인딩된 보기 모델에 있습니다. 보기 모델에 대 한 업데이트는 자동으로 보기에 반영 됩니다. 뷰 모델 이벤트도를 가져옵니다 보기에서 단추 클릭과 같은 합니다.

![](part-6/_static/image1.png)

이 접근 방식을 쉽게 레이아웃 및 응용 프로그램의 UI를 변경 하려면 바인딩, 모든 코드를 다시 작성 하지 않고 변경할 수 있으므로 있습니다. 으로 항목 목록이 표시 될 수 있습니다는 예를 들어 한 `<ul>`, 나중에 변경할 테이블에 있습니다.

## <a name="add-the-knockout-library"></a>Knockout 라이브러리 추가

Visual Studio에서에서 **도구** 메뉴 선택 **라이브러리 패키지 관리자**합니다. 그런 다음 선택 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-console[Main](part-6/samples/sample1.cmd)]

이 명령은 스크립트 폴더에 Knockout 파일을 추가합니다.

## <a name="create-the-view-model"></a>뷰 모델 만들기

라는 app.js 스크립트 폴더에 JavaScript 파일을 추가 합니다. (솔루션 탐색기에서 스크립트 폴더를 마우스 오른쪽 단추로 선택, **추가**을 선택한 후 **JavaScript 파일**.) 다음 코드에 붙여 넣습니다.

[!code-javascript[Main](part-6/samples/sample2.js)]

Knockout에 `observable` 클래스를 사용 하면 데이터 바인딩. Observable의 내용이 변경 될 경우 observable가 알립니다의 모든 데이터 바인딩된 컨트롤을 자체를 업데이트할 수 있도록 합니다. (의 `observableArray` 클래스는 배열 형식의 *observable*.) 시작 하 여 뷰 모델 두 관찰 가능 개체에 있습니다.

- `books`설명서의 목록을 저장 합니다.
- `error`AJAX 호출이 실패 한 경우 오류 메시지를 포함 합니다.

`getAllBooks` 메서드 책 목록을 AJAX 호출을 만듭니다. 다음 결과를 푸시합니다는 `books` 배열입니다.

`ko.applyBindings` 메서드는 Knockout 라이브러리의 일부입니다. 매개 변수로 보기 모델을 사용 하 고 데이터 바인딩을 설정 합니다.

## <a name="add-a-script-bundle"></a>스크립트 번들 추가

번들로 결합 하거나 단일 파일에 여러 파일을 번들로 쉽게 수 있도록 ASP.NET 4.5에서 기능입니다. 번들 페이지 로드 시간을 향상 시킬 수 있는 서버에 요청 수가 줄어듭니다.

응용 프로그램 파일을 열고\_Start/BundleConfig.cs 합니다. RegisterBundles 메서드에 다음 코드를 추가 합니다.

[!code-csharp[Main](part-6/samples/sample3.cs)]

>[!div class="step-by-step"]
[이전](part-5.md)
[다음](part-7.md)
