---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
title: 작업 필터 (C#) 이해 | Microsoft Docs
author: microsoft
description: 이 자습서의 목표 작업 필터를 설명 하는 것입니다. 작업 필터는 컨트롤러 동작-또는 전체 컨트롤러에 적용할 수 있는 특성 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/16/2008
ms.topic: article
ms.assetid: a94e4e81-40c1-47b7-8613-126a1a6cc93d
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
msc.type: authoredcontent
ms.openlocfilehash: d68933297329370e227f524c4b96ed7e259ef833
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30870416"
---
<a name="understanding-action-filters-c"></a>작업 필터 (C#) 이해
====================
by [Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_CS.pdf)

> 이 자습서의 목표 작업 필터를 설명 하는 것입니다. 작업 필터는 컨트롤러 동작-또는 동작이 실행 되는 방법을 수정 하는 전체 controller--에 적용할 수 있는 특성.


## <a name="understanding-action-filters"></a>작업 필터 이해

이 자습서의 목표 작업 필터를 설명 하는 것입니다. 작업 필터는 컨트롤러 동작-또는 동작이 실행 되는 방법을 수정 하는 전체 controller--에 적용할 수 있는 특성. ASP.NET MVC 프레임 워크에 몇 가지 작업 필터가 있습니다.

- OutputCache –이 작업 필터는 지정된 된 기간에 대 한 컨트롤러 작업의 출력을 캐시합니다.
- 이 작업 필터 HandleError – 컨트롤러 작업이 실행 될 때 발생 하는 오류를 처리 합니다.
- 권한 부여-이 작업 필터를 사용 하면 특정 사용자 또는 역할에 대 한 액세스를 제한 합니다.

사용자 고유의 사용자 지정 작업 필터를 만들 수도 있습니다. 예를 들어 사용자 지정 인증 시스템을 구현 하기 위해 사용자 지정 작업 필터를 만들 수도 있습니다. 또는 컨트롤러 동작에 의해 반환 되는 뷰 데이터를 수정 하는 작업 필터를 만들 수도 있습니다.

이 자습서에서는 처음부터 다시 작업 필터 작성 하는 방법에 설명 합니다. Visual Studio 출력 창에 다른 작업의 처리 단계를 기록 하는 로그 작업 필터를 만듭니다.

### <a name="using-an-action-filter"></a>작업 필터를 사용 하 여

작업 필터 특성입니다. 대부분의 작업 필터는 개별 컨트롤러 작업이 나 전체 컨트롤러 중 하나에 적용할 수 있습니다.

목록 1의 데이터 컨트롤러 라는 동작을 노출 하는 예를 들어 `Index()` 하는 현재 시간을 반환 합니다. 이 작업으로 데코레이팅되 어는 `OutputCache` 작업 필터. 이 필터를 사용 하면 10 초 동안 캐시 될 동작에 의해 반환 되는 값입니다.

**1 – 나열 `Controllers\DataController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample1.cs)]

반복적으로 호출 하는 경우는 `Index()` 브라우저의 주소 표시줄에는 URL/데이터/인덱스를 입력 하 고 새로 고침에 도달 하 여 작업 단추를 여러 번 동시 10 초 동안 표시 됩니다. 출력은 `Index()` 작업 (그림 1 참조)는 10 초 동안 캐시 됩니다.


[![캐시 된 시간](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)

**그림 01**: 캐시 시간 ([전체 크기 이미지를 보려면 클릭](understanding-action-filters-cs/_static/image3.png))


목록 1로 설정 하는 단일 작업 필터 –는 `OutputCache` 작업 필터 –에 적용 되는 `Index()` 메서드. 필요한 경우 동일한 작업에 여러 작업 필터를 적용할 수 있습니다. 예를 들어 모두를 적용 해야 할 수 있습니다는 `OutputCache` 및 `HandleError` 동일한 작업에 작업 필터.

목록 1에서의 `OutputCache` 작업 필터에 적용 되는 `Index()` 동작 합니다. 이 특성을 적용할 수는 `DataController` 클래스 자체입니다. 경우 컨트롤러에 의해 노출 되는 모든 작업에 의해 반환 되는 결과 10 초 동안 캐시 합니다.

### <a name="the-different-types-of-filters"></a>다양 한 유형의 필터

ASP.NET MVC 프레임 워크에서는 네 가지 형식의 필터를 지원합니다.

1. 권한 부여 필터 – 구현 하는 `IAuthorizationFilter` 특성입니다.
2. 작업 필터 – 구현 하는 `IActionFilter` 특성입니다.
3. 필터 – 구현 결과 `IResultFilter` 특성입니다.
4. 예외 필터 – 구현 하는 `IExceptionFilter` 특성입니다.

필터는 위에 나열 된 순서로 실행 됩니다. 예를 들어 권한 부여 필터는 항상 작업 필터 전에 실행 되 고 예외 필터 다른 모든 유형의 필터 후 항상 실행 됩니다.

권한 부여 필터는 인증 및 컨트롤러 작업에 대 한 권한 부여를 구현 하는 데 사용 됩니다. 예를 들어 권한 부여 필터는 권한 부여 필터의 예시입니다.

작업 필터는 before 및 컨트롤러 작업이 실행 된 후 실행 되는 논리를 포함 합니다. 컨트롤러 동작을 반환 하는 뷰 데이터를 수정 하려면 예를 들어, 작업 필터를 사용할 수 있습니다.

결과 필터 전과 뷰 결과 실행 된 후 실행 되는 논리를 포함 합니다. 예를 들어 뷰 결과 수정 하려면 수 브라우저에 뷰를 렌더링 하기 전에 마우스 오른쪽 단추로 합니다.

예외 필터는 마지막 유형의 필터를 실행 합니다. 컨트롤러 동작 또는 컨트롤러 작업 결과 의해 발생 하는 오류를 처리 하는 예외 필터를 사용할 수 있습니다. 또한 예외 필터를 사용 하 여 오류를 기록할 수 있습니다.

필터의 각 유형 마다 특정 한 순서로 실행 됩니다. 같은 유형의 필터가 실행 되는 순서를 제어 하려는 경우 필터의 순서 속성을 설정할 수 있습니다.

모든 작업 필터에 대 한 기본 클래스는는 `System.Web.Mvc.FilterAttribute` 클래스입니다. 특정 형식의 필터를 구현 하려면 다음 기본 필터 클래스에서 상속 하 고 중 하나 이상을 구현 하는 클래스를 만들어야 하는 경우는 `IAuthorizationFilter`, `IActionFilter`, `IResultFilter`, 또는 `IExceptionFilter` 인터페이스입니다.

### <a name="the-base-actionfilterattribute-class"></a>기본 ActionFilterAttribute 클래스

ASP.NET MVC 프레임 워크의 기본 포함 사용자 지정 작업 필터를 구현 하기 위한 쉽게 `ActionFilterAttribute` 클래스입니다. 이 클래스에서 모두 구현 하는 `IActionFilter` 및 `IResultFilter` 인터페이스를 만들고에서 상속 되는 `Filter` 클래스입니다.

여기에 용어 완전히 일치 하지 않습니다. 기술적으로 ActionFilterAttribute 클래스에서 상속 되는 클래스는 작업 필터와 결과 필터. 그러나 느슨한 의미에서 단어 작업 필터는 ASP.NET MVC 프레임 워크에서 필터의 모든 형식을 참조 하도록 사용 됩니다.

기본 `ActionFilterAttribute` 클래스에는 다음과 같은 메서드를 재정의할 수 있습니다.

- OnActionExecuting –이 메서드는 컨트롤러 작업이 실행 되기 전에 호출 됩니다.
- OnActionExecuted –이 메서드는 컨트롤러 작업이 실행 된 후 호출 됩니다.
- OnResultExecuting –이 메서드는 컨트롤러 작업 결과가 실행 되기 전에 호출 됩니다.
- OnResultExecuted –이 메서드는 컨트롤러 작업 결과가 실행 된 후 호출 됩니다.

다음 섹션에서 각 다른 방법을 구현 하는 방법을 살펴보겠습니다.

### <a name="creating-a-log-action-filter"></a>로그 작업 필터 만들기

를 사용자 지정 작업 필터를 구축 하는 방법을 보여 주기 위해 Visual Studio 출력 창에는 컨트롤러 동작을 처리 하는 단계를 기록 하는 사용자 지정 작업 필터를 만들겠습니다. 우리의 `LogActionFilter` 목록 2에 포함 되어 있습니다.

**2 – 나열 `ActionFilters\LogActionFilter.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample2.cs)]

목록 2에는 `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, 및 `OnResultExecuted()` 모든 메서드는 호출는 `Log()` 메서드. 메서드 및 현재 경로 데이터의 이름에 전달 되는 `Log()` 메서드. `Log()` 메서드는 Visual Studio 출력 창에 메시지를 씁니다 (그림 2 참조).


[![Visual Studio 출력 창에 쓰기](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)

**그림 02**: Visual Studio 출력 창에 쓰기 ([전체 크기 이미지를 보려면 클릭](understanding-action-filters-cs/_static/image6.png))


보기 3의 Home 컨트롤러를 전체 컨트롤러 클래스에는 로그 작업 필터를 적용 하는 방법을 보여 줍니다. 때마다 Home 컨트롤러에 의해 노출 되는 작업 중에 호출 되 – 하거나는 `Index()` 메서드 또는 `About()` 메서드-단계 처리 작업은 Visual Studio 출력 창에 기록 됩니다.

**3 – 나열 `Controllers\HomeController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample3.cs)]

### <a name="summary"></a>요약

이 자습서에서는 ASP.NET MVC 동작 필터를 도입 합니다. 네 가지 형식의 필터에 배웠습니다: 권한 부여 필터, 작업 필터, 결과 필터 및 예외 필터. 또한 기본에 대 한 배웠습니다 `ActionFilterAttribute` 클래스입니다.

마지막으로, 간단한 작업 필터를 구현 하는 방법을 배웠습니다. Visual Studio 출력 창에는 컨트롤러 동작을 처리 하는 단계를 기록 하는 로그 작업 필터를 만들었는지 여부입니다.

> [!div class="step-by-step"]
> [이전](asp-net-mvc-routing-overview-cs.md)
> [다음](improving-performance-with-output-caching-cs.md)
