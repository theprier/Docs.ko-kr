---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
title: 작업 필터 (C#) 이해 | Microsoft Docs
author: microsoft
description: 이 자습서의 목표는 작업 필터를 설명 합니다. 작업 필터는 컨트롤러 작업의 경우-또는 전체 컨트롤러에 적용할 수 있는 특성...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/16/2008
ms.topic: article
ms.assetid: a94e4e81-40c1-47b7-8613-126a1a6cc93d
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
msc.type: authoredcontent
ms.openlocfilehash: b1294eb61164d9f5c71152a542daa673de37f4ca
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37398234"
---
<a name="understanding-action-filters-c"></a>작업 필터 (C#) 이해
====================
[Microsoft](https://github.com/microsoft)

[PDF 다운로드](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_CS.pdf)

> 이 자습서의 목표는 작업 필터를 설명 합니다. 작업 필터는 컨트롤러 동작-또는 작업 실행 되는 방식을 수정 하는 전체 controller--에 적용할 수 있는 특성입니다.


## <a name="understanding-action-filters"></a>작업 필터 이해

이 자습서의 목표는 작업 필터를 설명 합니다. 작업 필터는 컨트롤러 동작-또는 작업 실행 되는 방식을 수정 하는 전체 controller--에 적용할 수 있는 특성입니다. ASP.NET MVC 프레임 워크에 몇 가지 작업 필터가 있습니다.

- OutputCache –이 작업 필터는 지정 된 기간에 대 한 컨트롤러 작업의 출력을 캐시합니다.
- HandleError –이 작업 필터는 컨트롤러 작업을 실행 하는 경우 발생 하는 오류를 처리 합니다.
- 권한 부여-이 작업 필터를 사용 하면 특정 사용자 또는 역할에 대 한 액세스를 제한 합니다.

사용자 고유의 사용자 지정 작업 필터를 만들 수도 있습니다. 예를 들어 다음 사용자 지정 인증 시스템을 구현 하기 위해 사용자 지정 작업 필터를 만들려면는 것이 좋습니다. 또는 컨트롤러 작업에 의해 반환 되는 뷰 데이터를 수정 하는 작업 필터를 만들 수 있습니다.

이 자습서에서는 처음부터 작업 필터를 작성 하는 방법을 알아봅니다. Visual Studio 출력 창에 여러 작업을 처리 하는 단계를 기록 하는 로그 작업 필터를 만듭니다.

### <a name="using-an-action-filter"></a>작업 필터를 사용 하 여

작업 필터 특성입니다. 대부분의 작업 필터는 개별 컨트롤러 작업 또는 전체 컨트롤러를 적용할 수 있습니다.

목록 1의 데이터 컨트롤러 라는 작업을 노출 하는 예를 들어 `Index()` 는 현재 시간을 반환 합니다. 이 작업은 데코 레이트 된 `OutputCache` 작업 필터. 이 필터를 사용 하면 10 초 동안 캐시 되도록 하려면 작업에 의해 반환 되는 값입니다.

**목록 1 – `Controllers\DataController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample1.cs)]

반복적으로 호출 하는 경우는 `Index()` 브라우저의 주소 표시줄에 입력 된 URL 데이터/인덱스 새로 고침에 도달 하는 작업 단추를 여러 번 10 초 동안 동일한 시간을 표시 됩니다. 출력을 `Index()` 작업 (그림 1 참조)는 10 초 동안 캐시 됩니다.


[![캐시 된 시간](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)

**그림 01**: 캐시 시간 ([큰 이미지를 보려면 클릭](understanding-action-filters-cs/_static/image3.png))


목록 1로 설정 하는 단일 작업 필터 – 합니다 `OutputCache` – 작업 필터에 적용 되는 `Index()` 메서드. 필요한 경우에 동일한 작업에 여러 작업 필터를 적용할 수 있습니다. 둘 다 적용 하려는 하는 예를 들어 합니다 `OutputCache` 및 `HandleError` 동일한 작업에 작업 필터.

목록 1에서 합니다 `OutputCache` 작업 필터에 적용 되는 `Index()` 작업 합니다. 이 특성을 적용할 수는 `DataController` 클래스 자체입니다. 이런 경우 10 초 동안 컨트롤러에 의해 노출 된 모든 작업에서 반환 된 결과 캐시할 수 됩니다.

### <a name="the-different-types-of-filters"></a>다양 한 유형의 필터

ASP.NET MVC 프레임 워크는 네 가지 유형의 필터를 지원합니다.

1. 권한 부여 필터 – 구현 된 `IAuthorizationFilter` 특성입니다.
2. 작업 필터 – 구현 된 `IActionFilter` 특성입니다.
3. 결과 필터 – 구현 된 `IResultFilter` 특성입니다.
4. 예외 필터 – 구현 된 `IExceptionFilter` 특성입니다.

필터는 위에 나열 된 순서로 실행 됩니다. 예를 들어, 권한 부여 필터는 항상 작업 필터 보다 먼저 실행 및 예외 필터는 필터의 다른 모든 형식 후 항상 실행 됩니다.

권한 부여 필터는 인증 및 컨트롤러 작업에 대 한 권한 부여를 구현 하는 데 사용 됩니다. 예를 들어, 권한 부여 필터는 권한 부여 필터의 예제.

작업 필터는 전과 컨트롤러 작업을 실행 한 후 실행 되는 논리를 포함 합니다. 예를 들어에 컨트롤러 작업을 반환 하는 뷰 데이터를 수정 하려면 작업 필터를 사용할 수 있습니다.

결과 필터는 뷰 결과 실행 된 후 및 하기 전에 실행 되는 논리를 포함 합니다. 보기 결과 수정 하려는 하는 예를 들어 뷰는 브라우저에 렌더링 되기 전에 마우스 오른쪽 단추로 합니다.

예외 필터는 마지막 형식의 필터를 실행 합니다. 컨트롤러 작업 또는 컨트롤러 작업 결과 의해 발생 하는 오류를 처리 하는 예외 필터를 사용할 수 있습니다. 오류를 기록할 예외 필터를 사용할 수도 있습니다.

각 다양 한 유형의 필터는 특정 순서로 실행 됩니다. 동일한 형식의 필터가 실행 되는 순서를 제어 하려는 경우 필터의 순서 속성을 설정할 수 있습니다.

모든 작업 필터에 대 한 기본 클래스를 `System.Web.Mvc.FilterAttribute` 클래스입니다. 특정 형식의 필터를 구현 하려는 경우 기본 필터 클래스에서 상속 하 고 하나 이상의 구현 하는 클래스를 만들어야 합니다 `IAuthorizationFilter`, `IActionFilter`를 `IResultFilter`, 또는 `IExceptionFilter` 인터페이스입니다.

### <a name="the-base-actionfilterattribute-class"></a>기본 ActionFilterAttribute 클래스

사용자 지정 작업 필터를 구현 하려면 하기 쉽게 하기 위해 ASP.NET MVC 프레임 워크는 기본 `ActionFilterAttribute` 클래스입니다. 이 클래스는 둘 다 구현 합니다 `IActionFilter` 및 `IResultFilter` 인터페이스에서 상속 되 고는 `Filter` 클래스입니다.

이 용어를 완전히 일치 하지 않습니다. 기술적으로 ActionFilterAttribute 클래스에서 상속 된 클래스는 작업 필터 및 결과 필터. 그러나 느슨한 점에서 word 작업 필터는 ASP.NET MVC 프레임 워크에서 필터의 모든 형식을 참조 하도록 사용 됩니다.

기본 `ActionFilterAttribute` 클래스에 메서드를 재정의할 수 있습니다.

- OnActionExecuting –이 메서드는 컨트롤러 작업을 실행 하기 전에 호출 됩니다.
- OnActionExecuted –이 메서드는 컨트롤러 작업이 실행 된 후 호출 됩니다.
- OnResultExecuting –이 메서드는 컨트롤러 작업 결과가 실행 되기 전에 호출 됩니다.
- OnResultExecuted –이 메서드는 컨트롤러 작업 결과가 실행 된 후 호출 됩니다.

다음 섹션에서는 각 이러한 다른 메서드를 구현 하는 방법을 살펴보겠습니다.

### <a name="creating-a-log-action-filter"></a>로그 작업 필터 만들기

사용자 지정 작업 필터를 구축 하는 방법을 보여 주기를 위해 Visual Studio 출력 창에는 컨트롤러 작업을 처리 하는 단계를 기록 하는 사용자 지정 작업 필터를 만듭니다. 우리의 `LogActionFilter` 목록 2에 포함 됩니다.

**2 – 나열 `ActionFilters\LogActionFilter.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample2.cs)]

목록 2에서 합니다 `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, 및 `OnResultExecuted()` 모든 메서드를 호출 합니다 `Log()` 메서드. 메서드 및 현재 경로 데이터의 이름을 전달 됩니다는 `Log()` 메서드. `Log()` 메서드는 Visual Studio 출력 창에 메시지를 씁니다 (그림 2 참조).


[![Visual Studio 출력 창에 쓰기](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)

**그림 02**: Visual Studio 출력 창에 작성 ([큰 이미지를 보려면 클릭](understanding-action-filters-cs/_static/image6.png))


보기 3의 Home 컨트롤러 전체 컨트롤러 클래스에 로그 작업 필터를 적용 하는 방법을 보여 줍니다. 호출 될 때마다 홈 컨트롤러에서 노출 하는 동작 중 하나는 – 하거나 합니다 `Index()` 메서드 또는 `About()` 메서드-단계의 처리 작업을 Visual Studio 출력 창에 기록 됩니다.

**3 – 나열 `Controllers\HomeController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample3.cs)]

### <a name="summary"></a>요약

이 자습서에서는 ASP.NET MVC 작업 필터를 소개 했습니다. 네 가지 유형의 필터에 대해 알아보았습니다: 권한 부여 필터, 작업 필터, 결과 필터 및 예외 필터. 또한 기본에 대해 알아보았습니다 `ActionFilterAttribute` 클래스입니다.

마지막으로, 간단한 작업 필터를 구현 하는 방법을 알아보았습니다. Visual Studio 출력 창에는 컨트롤러 작업을 처리 하는 단계를 기록 하는 로그 작업 필터를 만들었습니다.

> [!div class="step-by-step"]
> [이전](asp-net-mvc-routing-overview-cs.md)
> [다음](improving-performance-with-output-caching-cs.md)
