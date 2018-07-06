---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-vb
title: ASP.NET MVC 응용 프로그램 (VB)에 대 한 단위 테스트 만들기 | Microsoft Docs
author: StephenWalther
description: 컨트롤러 작업에 대 한 단위 테스트를 만드는 방법에 알아봅니다. 이 자습서에서는 Stephen walther가 컨트롤러 작업을 parti 반환 하는지 여부를 테스트 하는 방법에 설명 하는 중...
ms.author: aspnetcontent
ms.date: 08/19/2008
ms.assetid: eb35710d-1d99-44ac-b61f-e50af8cb328a
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-vb
msc.type: authoredcontent
ms.openlocfilehash: 3a8f142063a7addc8acca2b1a515295e36b26e29
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37837184"
---
<a name="creating-unit-tests-for-aspnet-mvc-applications-vb"></a>ASP.NET MVC 응용 프로그램 (VB)에 대 한 단위 테스트 만들기
====================
[Stephen walther가](https://github.com/StephenWalther)

[PDF 다운로드](http://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_VB.pdf)

> 컨트롤러 작업에 대 한 단위 테스트를 만드는 방법에 알아봅니다. 이 자습서에서는 Stephen walther가 테스트 컨트롤러 작업을 특정 뷰를 반환, 데이터의 특정 집합을 반환 또는 다른 유형의 작업 결과 반환 하는 방법을 보여 줍니다.


이 자습서의 목적은 작성 하는 방법의 컨트롤러에 대 한 단위 테스트에서 ASP.NET MVC 응용 프로그램을 보여 주기 위해 하는 것입니다. 세 가지 유형의 단위 테스트를 작성 하는 방법을 설명 합니다. 컨트롤러 작업에 의해 반환 된 보기를 테스트 하는 방법, 컨트롤러 작업에 의해 반환 되는 뷰 데이터를 테스트 하는 방법 및 하나의 컨트롤러 작업이 두 번째 컨트롤러 작업에 리디렉션됩니다 여부를 테스트 하는 방법에 알아봅니다.

## <a name="creating-the-controller-under-test"></a>테스트 컨트롤러 만들기

테스트 하려는 컨트롤러를 만들어 보겠습니다. 라는 컨트롤러를 `ProductController`, 목록 1에 포함 됩니다.

**목록 1 – `ProductController.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample1.vb)]

합니다 `ProductController` 라는 두 개의 작업 메서드를 포함 `Index()` 고 `Details()`입니다. 두 동작 메서드 뷰를 반환 합니다. 다음에 유의 합니다 `Details()` 작업 id 라는 이름의 매개 변수를 허용 합니다.

## <a name="testing-the-view-returned-by-a-controller"></a>컨트롤러에 의해 반환 된 뷰 테스트

테스트 한다고 가정해 보겠습니다. 여부는 `ProductController` 오른쪽 뷰를 반환 합니다. 있는지 확인 하고자 때는 `ProductController.Details()` 작업을 호출할 세부 정보 보기 반환 됩니다. 반환 된 뷰의 테스트에 대 한 단위 테스트를 포함 하는 목록 2의 test 클래스는 `ProductController.Details()` 동작 합니다.

**2 – 나열 `ProductControllerTest.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample2.vb)]

목록 2에서 클래스 라는 테스트 메서드 포함 `TestDetailsView()`합니다. 이 메서드는 코드의 세 줄을 포함합니다. 코드의 첫 번째 줄의 새 인스턴스를 만듭니다를 `ProductController` 클래스입니다. 컨트롤러의 호출 하는 두 번째 코드 줄 `Details()` 작업 메서드. 마지막으로, 코드 검사 보기에서 반환 하는 여부의 마지막 줄은 `Details()` 작업 세부 정보 보기입니다.

`ViewResult.ViewName` 속성 컨트롤러에 의해 반환 된 뷰의 이름을 나타냅니다. 이 속성을 테스트 하는 방법에 대 한 하나의 큰 경고 합니다. 두 가지 방법으로 컨트롤러는 보기를 반환할 수 있습니다. 컨트롤러는 다음과 같은 보기를 반환할 명시적으로 수 있습니다.

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample3.vb)]

또는 뷰의 이름은 다음과 같이 컨트롤러 작업의 이름에서 유추할 수 있습니다.

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample4.vb)]

이 컨트롤러 작업은 또한 라는 뷰를 반환 `Details`합니다. 그러나 뷰의 이름은 작업 이름에서 유추 됩니다. 뷰 이름을 테스트 하려는 경우 다음 하면 명시적으로 이름을 반환 해야 보기 컨트롤러 작업에서.

키보드 조합을 입력 하거나 목록 2에서 단위 테스트를 실행할 수 있습니다 **Ctrl + R, A** 클릭 하 여 합니다 **솔루션의 모든 테스트 실행** 단추 (그림 1 참조). 테스트를 통과 하면 그림 2에서 테스트 결과 창을 표시 됩니다.


[![솔루션의 모든 테스트 실행](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image1.png)

**그림 01**: 솔루션의 모든 테스트 실행 ([큰 이미지를 보려면 클릭](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image3.png))


[![성공 했습니다.](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image4.png)

**그림 02**: 성공! ([클릭 하 여 큰 이미지 보기](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image6.png))


## <a name="testing-the-view-data-returned-by-a-controller"></a>컨트롤러에 의해 반환 된 뷰 데이터를 테스트 합니다.

MVC 컨트롤러 이라는 것을 사용 하 여 데이터 뷰로 전달 *`View Data`* 합니다. 예를 들어, 호출할 때 특정 제품에 대 한 세부 정보를 표시 한다고 가정해 보겠습니다는 `ProductController Details()` 동작 합니다. 이런 경우의 인스턴스를 만들 수 있습니다는 `Product` (모델에 정의 된) 클래스 인스턴스를 전달 하 고는 `Details` 뷰를 활용 하 여 `View Data`입니다.

수정 된 `ProductController` 보기 3의 업데이트 된 포함 `Details()` 제품을 반환 하는 작업입니다.

**3 – 나열 `ProductController.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample5.vb)]

먼저 합니다 `Details()` 작업의 새 인스턴스를 만듭니다는 `Product` 랩톱 컴퓨터를 나타내는 클래스입니다. 다음, 인스턴스를 `Product` 클래스는 두 번째 매개 변수로 전달 되는 `View()` 메서드.

단위 테스트를 작성할 수 예상된 데이터 인지를 테스트 하려면 보기에 데이터가 포함 되어 있습니다. 랩톱 컴퓨터를 나타내는 제품을 호출할 때 반환 되는 여부 4 테스트에서 단위 테스트는 `ProductController Details()` 작업 메서드.

**4-목록 `ProductControllerTest.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample6.vb)]

목록 4에는 `TestDetailsView()` 메서드를 호출 하 여 반환 되는 뷰 데이터를 테스트 합니다 `Details()` 메서드. 합니다 `ViewData` 에 속성으로 노출 되는 `ViewResult` 호출에서 반환 된를 `Details()` 메서드. `ViewData.Model` 속성 보기에 전달 하는 제품을 포함 합니다. 테스트는 단순히 데이터 보기에에서 포함 된 제품 이름을 랩톱에 있는지 확인 합니다.

## <a name="testing-the-action-result-returned-by-a-controller"></a>컨트롤러에서 반환 된 작업 결과 테스트 합니다.

더 복잡 한 컨트롤러 작업을 다양 한 컨트롤러 작업에 전달 된 매개 변수의 값에 따라 작업 결과 반환할 수 있습니다. 컨트롤러 작업을 다양 한 유형의 작업 결과 포함 하 여 반환할 수는 `ViewResult`, `RedirectToRouteResult`, 또는 `JsonResult`합니다.

예를 들어 수정 된 `Details()` 목록 5에서 작업을 반환 합니다 `Details` 작업에 올바른 제품 Id를 전달 하는 경우를 확인 합니다. 1--있다면 리디렉션됩니다 미만의 잘못 된 제품 Id-Id 값으로 전달 하는 경우는 `Index()` 동작 합니다.

**5-목록 `ProductController.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample7.vb)]

동작을 테스트할 수 있습니다는 `Details()` 목록 6에서 단위 테스트를 사용 하 여 작업 합니다. 목록 6에서 단위 테스트의 확인로 리디렉션됩니다 합니다 `Index` -1 값을 사용 하 여 Id로 전달 될 때 보기는 `Details()` 메서드.

**6-목록 `ProductControllerTest.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample8.vb)]

호출 하는 경우는 `RedirectToAction()` 컨트롤러 작업에서 메서드를 컨트롤러 작업 반환을 `RedirectToRouteResult`입니다. 테스트 검사 하는지 여부를 합니다 `RedirectToRouteResult` 가 명명 된 컨트롤러 작업에 사용자를 리디렉션합니다 `Index`합니다.

## <a name="summary"></a>요약

이 자습서에서는 MVC 컨트롤러 작업에 대 한 단위 테스트를 작성 하는 방법을 알아보았습니다. 첫째, 오른쪽 뷰의 컨트롤러 작업에 의해 반환 되는지 여부를 확인 하는 방법을 알아보았습니다. 사용 하는 방법과 `ViewResult.ViewName` 뷰의 이름을 확인 하는 속성입니다.

내용을 테스트 하는 방법을 검사한 다음으로, `View Data`합니다. 적합 한 제품에서 반환 된 여부를 확인 하는 방법과 `View Data` 컨트롤러 작업을 호출한 후입니다.

마지막으로, 컨트롤러 작업에서 다양 한 유형의 작업 결과 반환 하는지 여부를 테스트 하는 방법을 설명 합니다. 컨트롤러를 반환 하는지 여부를 테스트 하는 방법과 `ViewResult` 또는 `RedirectToRouteResult`합니다.

> [!div class="step-by-step"]
> [이전](creating-unit-tests-for-asp-net-mvc-applications-cs.md)
