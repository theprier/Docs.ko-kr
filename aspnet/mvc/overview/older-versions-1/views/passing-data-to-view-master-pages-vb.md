---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
title: 데이터 뷰 마스터 페이지 (VB)를 전달 | Microsoft Docs
author: microsoft
description: 이 자습서의 목표 뷰 마스터 페이지에는 컨트롤러에서 데이터를 전달 하는 방법을 설명 하는 것입니다. 살펴볼 데이터 보기 m에 전달 하기 위한 두 가지 전략 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/16/2008
ms.topic: article
ms.assetid: 37a1ebae-8773-408f-8645-d21da7ff9ae1
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: fcd7c5baacc00490720d1f82252d81e40c097c88
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="passing-data-to-view-master-pages-vb"></a>마스터 페이지 보기 (VB)에 대 한 데이터 전달
====================
by [Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_VB.pdf)

> 이 자습서의 목표 뷰 마스터 페이지에는 컨트롤러에서 데이터를 전달 하는 방법을 설명 하는 것입니다. 데이터 뷰 마스터 페이지를 전달 하는 두 가지 전략이 살펴보겠습니다. 첫째, 유지 관리 하기 어려운 응용 프로그램에서 발생 하는 손쉬운 솔루션을 논의 합니다. 다음으로, 보다 나은 솔루션을 필요한 약간 더 많은 초기 작업이 훨씬 더 쉽게 유지 관리할 응용 프로그램에서 결과 제외한 살펴보겠습니다.


## <a name="passing-data-to-view-master-pages"></a>마스터 페이지 보기에 대 한 데이터 전달

이 자습서의 목표 뷰 마스터 페이지에는 컨트롤러에서 데이터를 전달 하는 방법을 설명 하는 것입니다. 데이터 뷰 마스터 페이지를 전달 하는 두 가지 전략이 살펴보겠습니다. 첫째, 유지 관리 하기 어려운 응용 프로그램에서 발생 하는 손쉬운 솔루션을 논의 합니다. 다음으로, 보다 나은 솔루션을 필요한 약간 더 많은 초기 작업이 훨씬 더 쉽게 유지 관리할 응용 프로그램에서 결과 제외한 살펴보겠습니다.

### <a name="the-problem"></a>문제

영화 데이터베이스 응용 프로그램을 작성 하는 한 응용 프로그램에서 모든 페이지에 동영상 범주 목록을 표시 하려면 (그림 1 참조). 또한 영화 범주 목록 데이터베이스 테이블에 저장 되도록 가정해 보세요. 이 경우 하기가 데이터베이스에서 사용 하 고 범주를 검색 하 고 뷰 마스터 페이지 내에서 영화 범주 목록이 렌더링할 것이 좋습니다.


[![영화 범주 뷰 마스터 페이지에 표시](passing-data-to-view-master-pages-vb/_static/image2.png)](passing-data-to-view-master-pages-vb/_static/image1.png)

**그림 01**: 영화 범주 뷰 마스터 페이지에 표시 ([전체 크기 이미지를 보려면 클릭](passing-data-to-view-master-pages-vb/_static/image3.png))


이 문제는 다음과 같습니다. 마스터 페이지에 동영상 범주 목록이 검색 방법을 마스터 페이지에서 모델 클래스의 메서드를 직접 호출 하기 쉽습니다. 즉, 마스터 페이지에서 데이터베이스 오른쪽에서 데이터를 검색 하기 위한 코드를 포함 하는 캐시는 합니다. 그러나 데이터베이스에 액세스 하기 위해 MVC 컨트롤러 무시 MVC 응용 프로그램 빌드 과정의 주요 이점 중 하나는 문제의 정리 분리를 위반 합니다.

MVC 응용 프로그램에서 MVC 컨트롤러에서 처리를 사용해 MVC 뷰 및 MVC 모델 간의 모든 상호 작용을 합니다. 이 문제의 분리 보다 유지 관리할 수, 적응력이 고 테스트 가능 응용 프로그램에서 발생합니다.

MVC 응용 프로그램에서 컨트롤러 작업에 의해 뷰 마스터 페이지를 포함 하 고 여 보기에 전달 되는 모든 데이터 보기에 전달 되어야 합니다. 또한 데이터 뷰 데이터를 활용 하 여 전달 되어야 합니다. 이 자습서의 나머지 부분에서 뷰 마스터 페이지를 뷰 데이터를 전달 하는 두 가지 방법을 검토 하려면.

### <a name="the-simple-solution"></a>간단한 솔루션

뷰 마스터 페이지에는 컨트롤러에서 뷰 데이터를 전달 하는 가장 간단한 솔루션으로 시작 하겠습니다. 간단한 솔루션은 각 컨트롤러 작업에서 마스터 페이지에 대 한 뷰 데이터를 전달 합니다.

목록 1의 컨트롤러를 고려해 야 합니다. 라는 두 가지 동작을 노출 `Index()` 및 `Details()`합니다. `Index()` 작업 메서드가 영화 데이터베이스 테이블의 모든 동영상을 반환 합니다. `Details()` 작업 메서드가 특정 영화 범주에 있는 모든 동영상을 반환 합니다.

**1 – 나열 `Controllers\HomeController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample1.vb)]

모두는 `Index()` 및 `Details()` 작업 데이터를 보려면 두 항목을 추가 합니다. `Index()` 두 키를 추가 하는 동작: 범주 및 동영상 합니다. 범주 키 보기 마스터 페이지에서 표시 영화 범주의 목록을 나타냅니다. 영화 키 인덱스 뷰 페이지에서 표시 하는 동영상 목록을 나타냅니다.

`Details()` 동작도 범주 및 동영상 라는 두 개의 키를 추가 합니다. 범주 키에는 다시 한 번 영화 범주 보기 마스터 페이지에서 표시 된 목록을 나타냅니다. 영화 키 세부 정보 보기 페이지에서 표시를 특정 범주에는 동영상 목록을 나타냅니다 (그림 2 참조).


[![세부 정보 보기](passing-data-to-view-master-pages-vb/_static/image5.png)](passing-data-to-view-master-pages-vb/_static/image4.png)

**그림 02**: 세부 정보 보기 ([전체 크기 이미지를 보려면 클릭](passing-data-to-view-master-pages-vb/_static/image6.png))


인덱스 뷰 목록 2에 포함 됩니다. 단순히 데이터 보기에서에서 영화 항목으로 표시 하는 동영상 목록을 반복 합니다.

**2 – 나열 `Views\Home\Index.aspx`**

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample2.aspx)]

마스터 페이지 보기는 보기 3에 포함 됩니다. 마스터 페이지 보기 반복 하 고 모든 데이터 보기에서에서 범주 항목이 나타내는 영화 범주를 렌더링 합니다.

**3 – 나열 `Views\Shared\Site.master`**

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample3.aspx)]

모든 데이터 보기와 보기의 마스터 페이지에 데이터 보기를 통해 전달 됩니다. 마스터 페이지에 데이터를 전달 하는 올바른 방법입니다.

따라서이 솔루션과 이유가 무엇입니까? 문제는이 솔루션 (하지 반복 직접) 드라이 원칙을 위반 합니다. 각 컨트롤러 작업 동일한 데이터를 보려면 영화 범주 목록에 추가 해야 합니다. 중복 되는 코드를 응용 프로그램에 두면 응용 프로그램 유지 관리 하 고 적용, 수정 하기가 훨씬 더 어렵습니다.

### <a name="the-good-solution"></a>적합 한 솔루션

이 섹션에서는 뷰 마스터 페이지에는 컨트롤러 작업에서 데이터를 전달 하는 대체를 하 고, 더 나은 솔루션을 살펴보겠습니다. 각 컨트롤러 작업에서 마스터 페이지에 대 한 동영상 범주를 추가 하는 대신 추가 영화 범주 뷰 데이터를 한 번만 합니다. 데이터 뷰 마스터 페이지에서 사용 하는 모든 보기 응용 프로그램 컨트롤러에 추가 됩니다.

ApplicationController 클래스 목록 4에 포함 됩니다.

ApplicationController 클래스 목록 4에 포함 됩니다.

**4 – 나열 `Controllers\ApplicationController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample4.vb)]

다음 세 가지 목록 4에 응용 프로그램 컨트롤러에 대 한 확인할 수 있는 것입니다. 클래스의 기본 System.Web.Mvc.Controller 클래스에서 상속 되는 첫 번째, 알림 메시지입니다. 응용 프로그램 컨트롤러는 컨트롤러 클래스입니다.

둘째, 응용 프로그램 컨트롤러 클래스를 MustInherit 클래스 인지 확인 합니다. MustInherit 클래스는 구체적 클래스에 의해 구현 되어야 하는 클래스입니다. 응용 프로그램 컨트롤러 MustInherit 클래스 이기 때문에는 클래스에 직접 정의 하는 메서드를 호출할 수 없습니다. 응용 프로그램 클래스를 직접 호출 하려고 하면 다음 메시지가 표시 됩니다는 리소스를 찾을 수 없는 오류입니다.

셋째, 데이터를 보려면 영화 범주 목록에 추가 하는 생성자는 응용 프로그램 컨트롤러에 포함 되어 있는지 확인 합니다. 응용 프로그램 컨트롤러에서 상속 되는 모든 컨트롤러 클래스는 자동으로 응용 프로그램 컨트롤러의 생성자를 호출 합니다. 응용 프로그램 컨트롤러에서 상속 되는 모든 컨트롤러에서 모든 작업을 호출할 때마다 영화 범주 뷰 데이터에 자동으로 포함 됩니다.

영화 컨트롤러 목록 5에는 응용 프로그램 컨트롤러에서 상속합니다.

**5-나열 `Controllers\MoviesController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample5.vb)]

라는 두 개의 작업 메서드를 노출 하는 이전 섹션에서 설명한 Home 컨트롤러와 마찬가지로 영화 컨트롤러 `Index()` 및 `Details()`합니다. 공지 보기 마스터 페이지에서 표시 하는 영화 범주 목록에는 없는 추가 중 하나에서 데이터를 볼는 `Index()` 또는 `Details()` 메서드. 영화 컨트롤러 응용 프로그램 컨트롤러에서 상속 하기 때문에 동영상 범주 목록 데이터를 자동으로 추가 됩니다.

공지 보기 마스터 페이지에 대 한 뷰 데이터를 추가 하도록이 솔루션 (하지 반복 직접) 드라이 원칙을 위반 하지 않습니다. 하나의 위치에 포함 된 데이터를 보려면 영화 범주 목록에 추가 하기 위한 코드: 응용 프로그램 컨트롤러에 대 한 생성자입니다.

### <a name="summary"></a>요약

이 자습서에서는 뷰 마스터 페이지에는 컨트롤러에서 뷰 데이터를 전달 하는 두 가지 방법에 설명 했습니다. 첫째, 접근 방식을 어려워질 수 있지만 간단한을 검사 했습니다. 첫 번째 섹션에서는 응용 프로그램에서 각 모든 컨트롤러 동작의 뷰 마스터 페이지에 대 한 데이터 보기를 추가할 수는 방법을 설명 합니다. 이 잘못 된 접근 방식 (하지 반복 직접) 드라이 원칙을 위반 하기 때문에 결론을 내렸습니다.

다음으로 데이터를 보려면 보기 마스터 페이지에서 필요한 데이터를 추가 하는 데 훨씬 더 좋은 전략을 검사 했습니다. 각 컨트롤러 작업에서 데이터 보기를 추가 하는 대신 응용 프로그램 컨트롤러 내에서 한 번만 뷰 데이터를 추가 했습니다. 이런 방식으로 ASP.NET MVC 응용 프로그램의 뷰 마스터 페이지에 데이터를 전달 하는 경우 코드 중복을 방지할 수 있습니다.

> [!div class="step-by-step"]
> [이전](creating-page-layouts-with-view-master-pages-vb.md)
