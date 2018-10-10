---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-6
title: JavaScript 클라이언트 만들기 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 20360326-b123-4b1e-abae-1d350edf4ce4
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-6
msc.type: authoredcontent
ms.openlocfilehash: b5cb4d93c30ef80a48da48ffc51dd51411b1d0d0
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48912666"
---
<a name="create-the-javascript-client"></a>JavaScript 클라이언트 만들기
====================
[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://github.com/MikeWasson/BookService)

이 섹션에서는 HTML, JavaScript를 사용 하는 응용 프로그램에 대 한 클라이언트 만들어집니다 하며 [Knockout.js](http://knockoutjs.com/) 라이브러리입니다. 단계에서 클라이언트 앱을 빌드 해 보겠습니다.

- 온라인 설명서의 목록을 표시합니다.
- 책 세부 정보를 표시합니다.
- 새 책을 추가합니다.

Knockout 라이브러리-Model-view-viewmodel (MVVM) 패턴을 사용합니다.

- 합니다 **모델** (이 경우, 책과 저자)에서 비즈니스 도메인에 있는 데이터의 서버 쪽 표현입니다.
- 합니다 **보기** 는 프레젠테이션 계층 (HTML).
- 합니다 **뷰 모델** 는 모델을 포함 하는 JavaScript 개체입니다. 뷰 모델은 ui 코드 추상화 합니다. 이 HTML 표현의 알지 못합니다. 대신 해당 뷰의 추상 기능 같은 나타냅니다 &quot;책의 목록이&quot;합니다.

뷰는 데이터 바인딩된 뷰 모델입니다. 보기 모델에 대 한 업데이트 보기에서 자동으로 반영 됩니다. 뷰 모델도 가져옵니다 이벤트를 보기에서 단추 클릭 등.

![](part-6/_static/image1.png)

이 접근 방식을 쉽게 레이아웃 및 앱의 UI를 변경 하려면 바인딩 코드를 다시 작성 하지 않고 변경할 수 있으므로 있습니다. 항목의 목록을 표시할 수 있습니다 예를 들어를 `<ul>`, 나중에 변경할 테이블에 있습니다.

## <a name="add-the-knockout-library"></a>Knockout 라이브러리 추가

Visual Studio에서에서 합니다 **도구** 메뉴에서 **NuGet 패키지 관리자**합니다. 선택한 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-console[Main](part-6/samples/sample1.cmd)]

이 명령은 스크립트 폴더에 Knockout 파일을 추가합니다.

## <a name="create-the-view-model"></a>뷰 모델 만들기

스크립트 폴더에 app.js 라는 JavaScript 파일을 추가 합니다. (선택, 솔루션 탐색기에서 스크립트 폴더를 마우스 오른쪽 단추로 **추가**을 선택한 후 **JavaScript 파일**.) 다음 코드에 붙여 넣습니다.

[!code-javascript[Main](part-6/samples/sample2.js)]

Knockout에서 `observable` 클래스를 사용 하면 데이터 바인딩. 관찰 가능 개체의 내용이 변경 될 경우 관찰 가능 개체에 알립니다 데이터 바인딩된 컨트롤을 모두 자체를 업데이트할 수 있도록 합니다. (합니다 `observableArray` 클래스의 배열 버전이 *observable*.) 시작 하려면 보기 모델에는 두 관찰 가능 개체에 있습니다.

- `books` 책의 목록이 저장 됩니다.
- `error` AJAX 호출에 실패 하면 오류 메시지를 포함 합니다.

`getAllBooks` 메서드 책 목록을 가져오려면 AJAX 호출을 수행 합니다. 다음 결과를 푸시를 `books` 배열입니다.

`ko.applyBindings` 메서드는 Knockout 라이브러리의 일부입니다. 매개 변수로 뷰 모델을 사용 하 고 데이터 바인딩을 설정 합니다.

## <a name="add-a-script-bundle"></a>스크립트 번들을 추가 합니다.

번들로 쉽게 결합 하 여 단일 파일에 여러 파일을 번들에 ASP.NET 4.5의 기능입니다. 묶음 페이지 로드 시간을 향상 시킬 수 있는 서버에 요청 수를 줄입니다.

앱 파일을 열고\_Start/BundleConfig.cs 합니다. RegisterBundles 메서드에 다음 코드를 추가 합니다.

[!code-csharp[Main](part-6/samples/sample3.cs)]

> [!div class="step-by-step"]
> [이전](part-5.md)
> [다음](part-7.md)
