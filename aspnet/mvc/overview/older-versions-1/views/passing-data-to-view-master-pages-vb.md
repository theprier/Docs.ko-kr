---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
title: 보기 마스터 페이지 (VB)에 데이터 전달 | Microsoft Docs
author: microsoft
description: 이 자습서의 목표는 보기 마스터 페이지에는 컨트롤러에서 데이터를 전달 하는 방법을 설명 합니다. 살펴봅니다 m 보기로 데이터를 전달 하기 위한 두 가지 전략을 중...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: 37a1ebae-8773-408f-8645-d21da7ff9ae1
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 9b840e0a5cc325a043ae88c10f52cca418589119
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41836392"
---
<a name="passing-data-to-view-master-pages-vb"></a>보기 마스터 페이지 (VB)에 데이터 전달
====================
[Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_VB.pdf)

> 이 자습서의 목표는 보기 마스터 페이지에는 컨트롤러에서 데이터를 전달 하는 방법을 설명 합니다. 보기 마스터 페이지에 데이터를 전달 하기 위한 두 가지 전략을 살펴봅니다. 첫째, 응용 프로그램 유지 관리 하기 어려울 정도로 초래 하는 쉬운 솔루션을 설명 합니다. 다음으로 필요한 약간 더 많은 초기 작업 하지만 훨씬 더 관리 하기 쉬운 응용 프로그램에서 결과 보다 나은 솔루션을 살펴봅니다.


## <a name="passing-data-to-view-master-pages"></a>보기 마스터 페이지에 데이터 전달

이 자습서의 목표는 보기 마스터 페이지에는 컨트롤러에서 데이터를 전달 하는 방법을 설명 합니다. 보기 마스터 페이지에 데이터를 전달 하기 위한 두 가지 전략을 살펴봅니다. 첫째, 응용 프로그램 유지 관리 하기 어려울 정도로 초래 하는 쉬운 솔루션을 설명 합니다. 다음으로 필요한 약간 더 많은 초기 작업 하지만 훨씬 더 관리 하기 쉬운 응용 프로그램에서 결과 보다 나은 솔루션을 살펴봅니다.

### <a name="the-problem"></a>문제

영화 데이터베이스 응용 프로그램을 빌드하는 하 고 영화 범주 목록 응용 프로그램에서 모든 페이지에 표시 하려는 imagine (그림 1 참조). 또한 영화 범주 목록 데이터베이스 테이블에 저장 되도록 한다고 가정 합니다. 이 경우 데이터베이스에서 범주를 검색 및 보기 마스터 페이지 내에 영화 범주 목록을 렌더링 하는 것이 없게 합니다.


[![보기 마스터 페이지에 동영상 범주 표시](passing-data-to-view-master-pages-vb/_static/image2.png)](passing-data-to-view-master-pages-vb/_static/image1.png)

**그림 01**: 영화 범주 보기 마스터 페이지에 표시 ([큰 이미지를 보려면 클릭](passing-data-to-view-master-pages-vb/_static/image3.png))


문제는 다음과 같습니다. 마스터 페이지에 동영상 범주 목록이 검색 하려면? 마스터 페이지에서 모델 클래스의 메서드를 직접 호출 하기 쉽습니다. 즉, 마스터 페이지에서 데이터베이스 오른쪽에서 데이터를 검색 하기 위한 코드를 포함 하 고 싶을 것입니다. 그러나 데이터베이스에 액세스 하기 위해 MVC 컨트롤러 무시을 위반 하는 MVC 응용 프로그램을 구축 하는 주요 이점 중 하나는 중요 한 부분의 분리 정리 합니다.

MVC 응용 프로그램에서는 MVC 뷰와 MVC 모델 MVC 컨트롤러에서 처리할 간의 모든 상호 작용을 해야 합니다. 이 중요 한 부분의이 분리 더 유지 하 고, 적응력이 테스트 가능 응용 프로그램에서 발생합니다.

MVC 응용 프로그램의 컨트롤러 작업에 의해 – 보기 마스터 페이지를 포함 하 여 – 보기로 전달 된 모든 데이터 보기에 전달 되어야 합니다. 또한 데이터 뷰 데이터를 활용 하 여 전달 되어야 합니다. 이 자습서의 나머지 부분에서는 보기 마스터 페이지 뷰 데이터를 전달 하는 두 가지 방법을 알아보겠습니다.

### <a name="the-simple-solution"></a>간단한 솔루션

보기 마스터 페이지에는 컨트롤러에서 뷰 데이터를 전달 하는 가장 간단한 솔루션을 사용 하 여 시작 해 보겠습니다. 가장 간단한 방법은 각 컨트롤러 작업에서 마스터 페이지에 대 한 뷰 데이터를 전달 하 하는 것입니다.

목록 1에서 컨트롤러를 고려해 야 합니다. 라는 두 가지 작업이 노출 `Index()` 고 `Details()`입니다. `Index()` 작업 메서드가 영화 데이터베이스 테이블에 있는 모든 영화를 반환 합니다. `Details()` 작업 메서드가 특정 영화 범주의 모든 영화를 반환 합니다.

**목록 1 – `Controllers\HomeController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample1.vb)]

모두를 `Index()` 하며 `Details()` 작업 데이터를 보려면 두 항목을 추가 합니다. `Index()` 두 키를 추가 하는 작업: 범주 및 동영상입니다. 범주 키 보기 마스터 페이지에서 표시 하는 영화 범주 목록을 나타냅니다. 영화 키 인덱스 뷰 페이지에서 표시 하는 영화 목록을 나타냅니다.

`Details()` 작업 범주 및 영화 라는 두 개의 키 추가. 범주 키를 다시 한 번 보기 마스터 페이지에서 표시 하는 영화 범주 목록을 나타냅니다. 영화 키 세부 정보 보기 페이지에서 표시 하는 특정 범주에는 영화 목록을 나타냅니다 (그림 2 참조).


[![세부 정보 보기](passing-data-to-view-master-pages-vb/_static/image5.png)](passing-data-to-view-master-pages-vb/_static/image4.png)

**그림 02**: 세부 정보 보기 ([큰 이미지를 보려면 클릭](passing-data-to-view-master-pages-vb/_static/image6.png))


인덱스 보기 목록 2에 포함 됩니다. 단순히 데이터 보기의에서 영화 항목으로 표시 하는 영화 목록을 반복 합니다.

**2 – 나열 `Views\Home\Index.aspx`**

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample2.aspx)]

보기 마스터 페이지는 목록 3에 포함 됩니다. 보기 마스터 페이지를 반복 하 고 모든 데이터 보기에서에서 범주 항목이 나타내는 영화 범주를 렌더링 합니다.

**3 – 나열 `Views\Shared\Site.master`**

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample3.aspx)]

모든 데이터 뷰 데이터 보기와 보기 마스터 페이지에 전달 됩니다. 마스터 페이지에 데이터를 전달 하는 올바른 방법입니다.

따라서이 솔루션을 사용 하 여 무엇이 있습니까? 이 솔루션 (없습니다 반복 직접) DRY 원칙을 위반 하는 것이 문제가입니다. 각 컨트롤러 작업에는 동일한 데이터를 보려면 동영상 범주 목록을 추가 해야 합니다. 응용 프로그램에 중복 코드를 포함 하면 응용 프로그램 유지 관리, 적응 및 수정 하기가 훨씬 어려워집니다.

### <a name="the-good-solution"></a>적합 한 솔루션

이 섹션에서는 보기 마스터 페이지에는 컨트롤러 작업에서 데이터를 전달 하려면 대체 하 고, 더 나은 솔루션을 살펴봅니다. 각 컨트롤러 작업에서 마스터 페이지에 대 한 동영상 범주를 추가 하는 대신 추가 동영상 범주는 뷰 데이터에 한 번만 합니다. 보기 마스터 페이지에 의해 사용 되는 모든 보기 데이터는 응용 프로그램 컨트롤러에 추가 됩니다.

ApplicationController 클래스 4에 포함 됩니다.

ApplicationController 클래스 4에 포함 됩니다.

**4-목록 `Controllers\ApplicationController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample4.vb)]

목록 4에서 응용 프로그램 컨트롤러에 대 한 유의 해야 하는 방법은 세 가지 있습니다. 먼저 기본 System.Web.Mvc.Controller 클래스에서 클래스를 상속 함을 알 수 있습니다. 응용 프로그램 컨트롤러는 컨트롤러 클래스.

둘째, 응용 프로그램 컨트롤러 클래스 MustInherit 클래스는 알 수 있습니다. MustInherit 클래스는 구체적인 클래스에서 구현 해야 하는 클래스입니다. 응용 프로그램 컨트롤러는 MustInherit 클래스 이기 때문에는 클래스에 직접 정의 된 메서드를 호출할 수 없습니다. 응용 프로그램 클래스를 직접 호출 하려고 하면 다음 하면 오류 메시지가 표시 됩니다는 리소스를 찾을 수 없습니다.

셋째, 응용 프로그램 컨트롤러에 데이터를 보려면 동영상 범주 목록에 추가 하는 생성자를 확인할 수 있습니다. 응용 프로그램 컨트롤러에서 상속 되는 모든 컨트롤러 클래스는 자동으로 응용 프로그램 컨트롤러의 생성자를 호출 합니다. 응용 프로그램 컨트롤러에서 상속 되는 모든 컨트롤러에서 모든 작업을 호출할 때마다 영화 범주 뷰 데이터에 자동으로 포함 됩니다.

영화 컨트롤러 목록 5에서 응용 프로그램 컨트롤러에서 상속 됩니다.

**5-목록 `Controllers\MoviesController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample5.vb)]

영화 컨트롤러를 이전 섹션에서 설명한 Home 컨트롤러와 마찬가지로 라는 두 개의 작업 메서드를 노출 `Index()` 고 `Details()`입니다. 보기 마스터 페이지에서 표시 하는 영화 범주 목록이 아닌 알림이 하나에서 데이터를 추가 합니다 `Index()` 또는 `Details()` 메서드. 영화 컨트롤러를 응용 프로그램 컨트롤러에서 상속 하기 때문에 자동으로 데이터를 보려면 동영상 범주 목록이 추가 됩니다.

보기 마스터 페이지에 대 한 뷰 데이터를 추가 하려면이 솔루션 (없습니다 반복 직접) DRY 원칙을 위반 하지 않도록 확인 합니다. 하나의 위치에 포함 된 데이터를 보려면 동영상 범주 목록에 추가 하는 것에 대 한 코드: 응용 프로그램 컨트롤러에 대 한 생성자입니다.

### <a name="summary"></a>요약

이 자습서에서는 보기 마스터 페이지를 컨트롤러에서 뷰 데이터를 전달 하는 두 가지 방법에 설명 했습니다. 첫째, 접근 방식을 유지 관리 하기가 있지만 단순 하 고 검사 했습니다. 첫 번째 섹션에서는 응용 프로그램에서 각 모든 컨트롤러 작업에서 보기 마스터 페이지에 대 한 뷰 데이터를 추가 하는 방법을 설명 합니다. 우리는 이것이 잘못 된 방법은 (없습니다 반복 직접) DRY 원칙을 위반 하기 때문에 결론을 내렸습니다.

다음으로 데이터를 보려면 보기 마스터 페이지에 필요한 데이터를 추가 하는 것에 대 한 훨씬 더 나은 전략을 검사 했습니다. 각 컨트롤러 작업에서 데이터 보기를 추가 하는 대신 응용 프로그램 제어기 내에서 한 번만 뷰 데이터를 추가 했습니다. 이런 방식으로 ASP.NET MVC 응용 프로그램에서 보기 마스터 페이지에 데이터를 전달 하는 경우 코드 중복을 방지할 수 있습니다.

> [!div class="step-by-step"]
> [이전](creating-page-layouts-with-view-master-pages-vb.md)
