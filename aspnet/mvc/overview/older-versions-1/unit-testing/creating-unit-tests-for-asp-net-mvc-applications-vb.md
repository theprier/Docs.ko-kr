---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-vb
title: ASP.NET MVC 응용 프로그램 (VB)에 대 한 단위 테스트 만들기 | Microsoft Docs
author: StephenWalther
description: 컨트롤러 작업에 대 한 단위 테스트를 만드는 방법에 알아봅니다. 이 자습서에서는 Stephen Walther 컨트롤러 작업에는 parti 반환 하는지 여부를 테스트 하는 방법을 보여 줍니다 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/19/2008
ms.topic: article
ms.assetid: eb35710d-1d99-44ac-b61f-e50af8cb328a
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-vb
msc.type: authoredcontent
ms.openlocfilehash: 299665f45d72fee33f92344ed53c87dfb1a76d60
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="creating-unit-tests-for-aspnet-mvc-applications-vb"></a>ASP.NET MVC 응용 프로그램 (VB)에 대 한 단위 테스트 만들기
====================
으로 [Stephen Walther](https://github.com/StephenWalther)

[PDF 다운로드](http://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_VB.pdf)

> 컨트롤러 작업에 대 한 단위 테스트를 만드는 방법에 알아봅니다. 이 자습서에서는 Stephen Walther 테스트 컨트롤러 작업이 특정 보기 반환, 데이터의 특정 집합을 반환 또는 다른 유형의 작업 결과 반환 하는 방법을 보여 줍니다.


이 자습서의 목표 작성 하는 방법을 단위 테스트는 컨트롤러에 대 한 ASP.NET mvc에서 응용 프로그램을 보여 주기 위한 것입니다. 세 가지 유형의 단위 테스트를 작성 하는 방법에 설명 합니다. 컨트롤러 작업에서 반환 된 보기를 테스트 하는 방법, 컨트롤러 작업에 의해 반환 되는 뷰 데이터를 테스트 하는 방법 및 하나의 컨트롤러 작업 리디렉션합니다 두 번째 컨트롤러 작업에 있는지 여부를 테스트 하는 방법을 설명 합니다.

## <a name="creating-the-controller-under-test"></a>테스트 대상 컨트롤러 만들기

테스트 하 여 사용 하는 컨트롤러를 만들어 보겠습니다. 명명 된 컨트롤러는 `ProductController`, 목록 1에 포함 되어 있습니다.

**1 – 나열 `ProductController.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample1.vb)]

`ProductController` 라는 두 개의 작업 메서드가 포함 되어 `Index()` 및 `Details()`합니다. 두 동작 메서드는 뷰를 반환 합니다. 에 `Details()` 작업 id입니다. 명명 된 매개 변수를 허용 합니다.

## <a name="testing-the-view-returned-by-a-controller"></a>컨트롤러에 의해 반환 된 뷰를 테스트 합니다.

테스트 한다고 가정해 보세요. 여부는 `ProductController` 오른쪽 뷰를 반환 합니다. 있는지 확인 하고자 때는 `ProductController.Details()` 동작이 호출 자세히 보기 반환 됩니다. 테스트에서 반환 된 보기에 대 한 단위 테스트를 포함 하는 목록 2에서 테스트 클래스는 `ProductController.Details()` 동작 합니다.

**2 – 나열 `ProductControllerTest.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample2.vb)]

목록 2의 클래스는 라는 테스트 메서드를 포함 `TestDetailsView()`합니다. 이 메서드는 코드의 세 줄을 포함합니다. 코드의 첫 번째 줄의 새 인스턴스를 만듭니다.는 `ProductController` 클래스입니다. 코드의 두 번째 줄에는 컨트롤러의 호출 `Details()` 동작 메서드가 있습니다. 마지막으로, 마지막 줄의 코드 검사 보기에서 반환 되는 여부는 `Details()` 작업에도 자세히 보기.

`ViewResult.ViewName` 속성은 컨트롤러에 의해 반환 된 보기의 이름을 나타냅니다. 이 속성을 테스트 하는 방법에 대 한 하나의 큰 경고 합니다. 두 가지 방법으로 컨트롤러 보기를 반환할 수 있습니다. 컨트롤러는 다음과 같은 보기를 반환할 명시적으로 수 있습니다.

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample3.vb)]

또는 보기 이름은 다음과 같이 컨트롤러 동작의 이름에서 유추할 수 있습니다.

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample4.vb)]

이 컨트롤러 작업에도 라는 이름의 뷰가 반환 `Details`합니다. 그러나 뷰의 이름은 작업 이름에서 유추 됩니다. 뷰 이름을 테스트 하려는 경우 다음 명시적으로 반환 해야 뷰 이름을 컨트롤러 동작에서 합니다.

키보드 조합을 입력 하거나 목록 2에서 단위 테스트를 실행할 수 있습니다 **Ctrl-R, A** 클릭 하 여는 **솔루션의 모든 테스트 실행** 단추 (그림 1 참조). 테스트에 통과 하는 경우에 그림 2에는 테스트 결과 창을 표시 됩니다.


[![솔루션의 모든 테스트 실행](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image1.png)

**그림 01**: 솔루션의 모든 테스트 실행 ([전체 크기 이미지를 보려면 클릭](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image3.png))


[![성공 했습니다!](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image4.png)

**그림 02**: 성공! ([전체 크기 이미지를 보려면 클릭](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image6.png))


## <a name="testing-the-view-data-returned-by-a-controller"></a>컨트롤러에 의해 반환 된 데이터 보기를 테스트 합니다.

MVC 컨트롤러 라는 것을 사용 하 여 데이터 뷰를 전달 *`View Data`*합니다. 예를 들어, 호출할 때 특정 제품에 대 한 정보를 표시 하 고 가정은 `ProductController Details()` 동작 합니다. 인스턴스를 만들 수는 경우에 `Product` (모델에 정의 됨) 하는 클래스 인스턴스를 전달 하 고는 `Details` 뷰를 이용 하 여 `View Data`합니다.

수정 된 `ProductController` 보기 3의 업데이트 된 포함 `Details()` 제품을 반환 하는 작업입니다.

**3 – 나열 `ProductController.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample5.vb)]

첫째는 `Details()` 동작의 새 인스턴스를 만듭니다.는 `Product` 랩톱 컴퓨터를 나타내는 클래스입니다. 다음으로의 인스턴스는 `Product` 클래스에 대 한 두 번째 매개 변수로 전달 되는 `View()` 메서드.

단위 테스트를 작성할 수 필요한 데이터가 있는지 여부를 테스트 보기에 데이터가 포함 됩니다. 테스트 목록 4에서에서 단위 테스트에 노트북 컴퓨터를 나타내는 제품 호출할 때 반환 되는 여부는 `ProductController Details()` 동작 메서드.

**4 – 나열 `ProductControllerTest.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample6.vb)]

목록 4에는 `TestDetailsView()` 메서드 호출에서 반환 된 데이터 보기 테스트는 `Details()` 메서드. `ViewData` 에 속성으로 노출 되는 `ViewResult` 호출에서 반환 된는 `Details()` 메서드. `ViewData.Model` 속성 뷰에 전달 되는 제품을 포함 합니다. 이 테스트는 단순히 데이터 보기에에서 포함 된 제품 이름을 랩톱에 있는지 확인 합니다.

## <a name="testing-the-action-result-returned-by-a-controller"></a>컨트롤러에 의해 반환 된 작업 결과 테스트 합니다.

더 복잡 한 컨트롤러 작업 다양 한 유형의 컨트롤러 작업에 전달 된 매개 변수의 값에 따라 작업 결과 반환할 수 있습니다. 컨트롤러 작업에는 다양 한 유형의 작업 결과 포함 하 여 반환할 수 있습니다는 `ViewResult`, `RedirectToRouteResult`, 또는 `JsonResult`합니다.

예를 들어 수정 된 `Details()` 목록 5의 동작은 반환는 `Details` 작업에 유효한 제품 Id를 전달 하는 경우를 확인 합니다. 1--합니다는 리디렉션됩니다 보다 작은 잘못 된 제품 Id-Id 값으로 전달 하는 경우는 `Index()` 동작 합니다.

**5-나열 `ProductController.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample7.vb)]

동작을 테스트할 수 있습니다는 `Details()` 목록 6에서 단위 테스트와 함께 작업 합니다. 단위 테스트 목록 6에서 확인으로 리디렉션됩니다는 `Index` 에 전달 된 값-1 Id 보기는 `Details()` 메서드.

**6-나열 `ProductControllerTest.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample8.vb)]

호출 하는 경우는 `RedirectToAction()` 는 컨트롤러 동작 메서드를 컨트롤러 작업 반환는 `RedirectToRouteResult`합니다. 테스트 검사 여부는 `RedirectToRouteResult` 는 라는 컨트롤러 작업으로 사용자를 리디렉션합니다 `Index`합니다.

## <a name="summary"></a>요약

이 자습서에서는 MVC 컨트롤러 작업에 대 한 단위 테스트를 작성 하는 방법을 배웠습니다. 첫째, 오른쪽 뷰의 컨트롤러 동작에 의해 반환 되는지 여부를 확인 하는 방법을 배웠습니다. 사용 하는 방법을 배웠습니다는 `ViewResult.ViewName` 속성을 보기의 이름이 유효한 지 확인 합니다.

다음으로의 콘텐츠를 테스트 하는 방법을 검사 했습니다 `View Data`합니다. 적합 한 제품에서 반환 된 있는지 여부를 확인 하는 방법을 배웠습니다 `View Data` 컨트롤러 작업을 호출한 후 합니다.

마지막으로, 다양 한 유형의 작업 결과 컨트롤러 작업에서 반환 되는 여부를 테스트 하는 방법을 설명 합니다. 컨트롤러를 반환 하는지 여부를 테스트 하는 방법을 배웠습니다는 `ViewResult` 또는 `RedirectToRouteResult`합니다.

> [!div class="step-by-step"]
> [이전](creating-unit-tests-for-asp-net-mvc-applications-cs.md)
