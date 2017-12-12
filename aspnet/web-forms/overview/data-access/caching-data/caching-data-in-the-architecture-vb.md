---
uid: web-forms/overview/data-access/caching-data/caching-data-in-the-architecture-vb
title: "아키텍처 (VB)에서 데이터 캐싱 | Microsoft Docs"
author: rick-anderson
description: "이전 자습서에서는 프레젠테이션 계층에서 캐시를 적용 하는 방법을 배웠습니다. 이 자습서에서는 계층화 된 우리의 architectu를 활용 하는 방법에 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/30/2007
ms.topic: article
ms.assetid: 5e189dd7-f4f9-4f28-9b3a-6cb7d392e9c7
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-in-the-architecture-vb
msc.type: authoredcontent
ms.openlocfilehash: f1d94045236cc8e1b12839ced4de1258466a626e
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="caching-data-in-the-architecture-vb"></a>아키텍처 (VB)에서 데이터 캐싱
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_59_VB.exe) 또는 [PDF 다운로드](caching-data-in-the-architecture-vb/_static/datatutorial59vb1.pdf)

> 이전 자습서에서는 프레젠테이션 계층에서 캐시를 적용 하는 방법을 배웠습니다. 이 자습서에서는 데이터를 캐시 하는 비즈니스 논리 계층에서 가이드의 계층화 된 아키텍처를 활용 하는 방법에 설명 합니다. 캐싱 계층을 포함 하는 아키텍처를 확장 하 여이 작업을 수행 했습니다.


## <a name="introduction"></a>소개

이전 자습서에서 살펴본 것 처럼 ObjectDataSource의 데이터 캐시 작업은을 속성을 설정 합니다. 그러나는 ObjectDataSource 밀접 하 게 캐싱 정책을 ASP.NET 페이지와 결합 하는 프레젠테이션 계층에서 캐싱 적용 됩니다. 계층화 된 아키텍처를 제공 하는 이유 중 하나는 이러한 신중을 해제 될 수 있도록 합니다. 예를 들어, 비즈니스 논리 계층 데이터 액세스 계층에서는 데이터 액세스 정보를 분리 하는 동안 ASP.NET 페이지에서 비즈니스 논리를 분리 합니다. 비즈니스 논리와 데이터 액세스 정보의 이러한 분리는 것이 좋습니다, 부분적으로 더 쉽게 읽을 수, 관리 하 고 변경할 수 있는 유연한 시스템을 만들므로 합니다. 도메인 지식 및 분업 프레젠테이션 계층 대상이 t에서 작업 하는 개발자가 업무를 수행 하려면 데이터베이스 s 세부 정보에 잘 알고 말아야 할 수도 있습니다. 프레젠테이션 계층과에서 캐싱 정책 분리 유사한 이점이 있습니다.

이 자습서에서는 가이드의 아키텍처를 포함 하도록 확장 됩니다 우리는 *캐싱 레이어* (또는 줄여서 CL) 우리의 캐싱 정책을 사용 하는 합니다. 캐싱 계층에 포함 됩니다는 `ProductsCL` 같은 방법으로 제품 정보에 대 한 액세스를 제공 하는 클래스 `GetProducts()`, `GetProductsByCategoryID(categoryID)`조각과, 해당, 호출 되 면 캐시에서 데이터를 검색 하는 첫 번째 시도 더 합니다. 이러한 메서드는 적절 한 호출 캐시가 비어 있으면 `ProductsBLL` DAL에서 데이터를 얻을 차례로 BLL에 메서드. `ProductsCL` 메서드 반환 하기 전에 BLL에서 검색 한 데이터를 캐시 합니다.

그림 1에서 볼 수 있듯이 CL 프레젠테이션 및 비즈니스 논리 계층 간에 상주 합니다.


![캐싱 계층 (CL)는 Our 아키텍처에서 다른 계층](caching-data-in-the-architecture-vb/_static/image1.png)

**그림 1**: The 캐싱 레이어 (CL)는 Our 아키텍처에서 다른 계층


## <a name="step-1-creating-the-caching-layer-classes"></a>1 단계: 캐싱 레이어 클래스 만들기

이 자습서에서는 만듭니다 매우 간단한 CL 단일 클래스와 `ProductsCL` 방법 중 일부만 포함 합니다. 전체 응용 프로그램을 만드는 해야 전체 캐싱 레이어 만들 `CategoriesCL`, `EmployeesCL`, 및 `SuppliersCL` 클래스 및 BLL에 각 데이터 액세스 또는 수정 방법에 대 한 이러한 계층 캐싱 클래스에서 메서드를 제공 합니다. BLL 및 DAL와 마찬가지로 캐싱 계층을 이상적으로 구현를 별도 클래스 라이브러리 프로젝트로; 그러나 우리 구현을의 클래스로 `App_Code` 폴더입니다.

Let s DAL 및 BLL 클래스에서 더 많은 CL 명확 하 게 별도 클래스에서 새 하위 폴더를 만들는 `App_Code` 폴더입니다. 마우스 오른쪽 단추로 클릭는 `App_Code` 솔루션 탐색기의 폴더에에서 새 폴더를 선택 하 고 새 폴더 이름을 `CL`합니다. 이 폴더를 만든 후에 새 클래스를 추가 `ProductsCL.vb`합니다.


![CL 라는 새 폴더 및 ProductsCL.vb 라는 클래스를 추가 합니다.](caching-data-in-the-architecture-vb/_static/image2.png)

**그림 2**: 라는 새 폴더 추가 `CL` 및 라는 클래스`ProductsCL.vb`


`ProductsCL` 동급 해당 비즈니스 논리 계층에에서 있는 데이터 액세스 및 수정 방법의 동일한 집합을 포함 해야 하는 클래스 (`ProductsBLL`). 대신 이러한 메서드의 let s 정당한 빌드 모든 만드는 몇 가지 패턴에 대해 여기에서 사용 하는 CL 합니다. 특히, 추가 `GetProducts()` 및 `GetProductsByCategoryID(categoryID)` 3 단계에서에서 메서드 및 `UpdateProduct` 4 단계에서에서 오버 로드 합니다. 나머지를 추가할 수 있습니다 `ProductsCL` 메서드 및 `CategoriesCL`, `EmployeesCL`, 및 `SuppliersCL` 든 클래스입니다.

## <a name="step-2-reading-and-writing-to-the-data-cache"></a>2 단계: 읽기 및 쓰기 데이터 캐시를

캐싱 기능 이전 자습서에서 내부적으로 탐색할 ObjectDataSource ASP.NET 데이터 캐시를 사용 하 여 BLL에서 검색 된 데이터를 저장 합니다. 데이터 캐시의 ASP.NET 페이지 코드 숨김 클래스 또는 웹 응용 프로그램의 아키텍처의 클래스에도 프로그래밍 방식으로 액세스할 수 있습니다. 에서 읽기 및 쓰기 데이터 캐시에는 ASP.NET 페이지의 코드 숨김 클래스를 하려면 다음과 같은 패턴을 사용 합니다.


[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample1.vb)]

[ `Cache` 클래스](https://msdn.microsoft.com/en-us/library/system.web.caching.cache.aspx) s [ `Insert` 메서드](https://msdn.microsoft.com/en-us/library/system.web.caching.cache.insert.aspx) 다양 한 오버 로드 했습니다. `Cache("key") = value`및 `Cache.Insert(key, value)` 동의어인 둘 다가 정의 된 만료 없이 지정된 된 키를 사용 하 여 캐시에 항목을 추가 합니다. 일반적으로, 종속성, 시간 기반 만료 또는 둘 다로 캐시에 항목을 추가 하는 경우 만료를 지정 하려고 합니다. 다른 중 하나를 사용 하 여 `Insert`의 메서드 오버 로드 종속성 또는 시간 기반 만료 정보를 제공 합니다.

S 메서드 요청 된 데이터 캐시에 있는 경우 그리고 있다면을 먼저 확인 해야 하는 캐싱 계층에서에서 반환 합니다. 요청된 된 데이터 캐시에 없는 경우 적절 한 BLL 메서드를 호출 해야 합니다. 반환 값을 캐시 하 고 다음 시퀀스 다이어그램에서 같이 다음 반환 해야 합니다.


![캐싱 레이어의 메서드 경우 캐시에서 데이터를 반환 하기 s 사용 가능](caching-data-in-the-architecture-vb/_static/image3.png)

**그림 3**: 경우 The 캐싱 레이어의 메서드는 캐시에서 데이터를 반환 하기 s 사용 가능


그림 3에 나온 순서는 다음과 같은 패턴을 사용 하 여 CL 클래스에서 수행 됩니다.


[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample2.vb)]

여기에서 *형식* 캐시에 저장 되는 데이터 형식이 `Northwind.ProductsDataTable`, 같은 *키* 캐시 항목을 고유 하 게 식별 하는 키입니다. 하는 경우 지정 된 항목 *키* 다음 캐시에 없는 *인스턴스* 됩니다 `Nothing` 및 데이터를 적절 한 BLL 메서드를 검색 하 고 캐시에 추가 됩니다. 시간순으로 `Return instance` 에 도달 *인스턴스* BLL에서 푸시하거나 캐시에서 데이터에 대 한 참조를 포함 합니다.

캐시에서 데이터에 액세스할 때 위의 패턴을 사용 해야 합니다. 얼핏 보기에 같고를 표시 되는 다음 패턴 경합 조건을 정의 하는 미묘한 차이 포함 합니다. 경합 상태는 산발적으로 장애가 자체를 표시 하며 재현 하기 어려운 때문에 디버깅 하기 어렵습니다.


[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample3.vb)]

이 두 번째 차이점을 잘못 된 코드 조각은 조건문에서 직접 데이터 캐시에 액세스 로컬 변수에 캐시 된 항목에 대 한 참조를 저장 하지 않고 *및* 에 `Return`합니다. 이 코드에 도달 하면 상상할 `Cache("key")` 않습니다 `Nothing`, 하기 전에 `Return` 문에 도달 하면, 시스템 제거 *키* 캐시에서 합니다. 드물지만 이러한 경우에는 코드는 반환 `Nothing` 예상 되는 형식의 개체 대신 합니다.

> [!NOTE]
> 데이터 캐시 스레드로부터 안전한 이므로 간단한 읽기 또는 쓰기에 대 한 스레드 액세스를 동기화 할 필요가 없습니다. 그러나 원자성 캐시에 데이터에 대해 여러 작업을 수행 해야 할 모르는 경우 잠금이나 스레드로부터 안전을 보장 하기 위해 다른 메커니즘을 구현 해야 합니다. 참조 [ASP.NET 캐시에 대 한 동기화 액세스](http://www.ddj.com/184406369) 자세한 정보에 대 한 합니다.


사용 하 여 데이터 캐시에서 항목을 프로그래밍 방식으로 제거할 수는 [ `Remove` 메서드](https://msdn.microsoft.com/en-us/library/system.web.caching.cache.remove.aspx) 같이:


[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample4.vb)]

## <a name="step-3-returning-product-information-from-theproductsclclass"></a>3 단계: 제품 정보에서 반환 된`ProductsCL`클래스

이 자습서에서 제품 정보를 반환 하기 위한 두 메서드를 구현 하는 s 사용에 대 한는 `ProductsCL` 클래스: `GetProducts()` 및 `GetProductsByCategoryID(categoryID)`합니다. 와 함께 `ProductsBL` 비즈니스 논리 계층에서 클래스는 `GetProducts()` 모든으로 제품에 대 한 정보를 반환 하는 메서드는 cl에서는 `Northwind.ProductsDataTable` 개체를 동안 `GetProductsByCategoryID(categoryID)` 지정된 된 범주에서 모든 제품을 반환 합니다.

다음 코드의 메서드 일부를 보여 줍니다.는 `ProductsCL` 클래스:


[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample5.vb)]

먼저는 `DataObject` 및 `DataObjectMethodAttribute` 클래스 및 메서드에 적용 된 특성입니다. 이러한 특성 클래스 및 메서드 표시할 대상을 마법사 s 단계로 나타내는 ObjectDataSource s 마법사에 정보를 제공 합니다. CL 클래스 및 메서드를 프레젠테이션 계층에서 ObjectDataSource에서 액세스할 이후 디자인 타임 환경을 향상 시키기 위해 이러한 특성을 추가 했습니다. 다시 참조는 [는 비즈니스 논리 계층을 만드는](../introduction/creating-a-business-logic-layer-vb.md) 이러한 특성 및 그 영향에 대 한 보다 철저 한 설명은 자습서입니다.

에 `GetProducts()` 및 `GetProductsByCategoryID(categoryID)` 메서드에서 반환 된 데이터는 `GetCacheItem(key)` 메서드를 지역 변수에 할당 됩니다. `GetCacheItem(key)` 지정에 따라 캐시에서 특정 항목을 반환 하는 메서드를 곧를 검토 합니다 *키*합니다. 해당에서 검색 된 경우 해당 데이터가 캐시에서 발견 되 면 `ProductsBLL` 사용 하 여 캐시에 추가 하 고 클래스 메서드는 `AddCacheItem(key, value)` 메서드.

`GetCacheItem(key)` 및 `AddCacheItem(key, value)` 메서드 각각 데이터 캐시, 읽기 및 쓰기 값을 가진 인터페이스입니다. `GetCacheItem(key)` 메서드는 둘 중 보다 단순한 합니다. 전달 된 기능을 사용 하 여 캐시 클래스에서 값을 반환 하면 *키*:


[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample6.vb)]

`GetCacheItem(key)`사용 하지 않는 *키* 호출 그 대신 제공 될 때 값은 `GetCacheKey(key)` 반환 하는 *키* ProductsCache-로 시작 합니다. `MasterCacheKeyArray`, ProductsCache, 문자열을 보유 하를 사용 하 여 `AddCacheItem(key, value)` 메서드를 일시적으로 볼 수 있겠지만 합니다.

ASP.NET 페이지의 코드 숨김 클래스에서 데이터 캐시 액세스할 수 있습니다를 사용 하는 `Page` s 클래스 [ `Cache` 속성](https://msdn.microsoft.com/en-us/library/system.web.ui.page.cache.aspx), 하 고 같은 구문을 허용 `Cache("key") = value`2 단계에서에서 설명 했 듯이, 합니다. 아키텍처 내에서 클래스에서 데이터 캐시 액세스할 수 중 하나를 사용 하 여 `HttpRuntime.Cache` 또는 `HttpContext.Current.Cache`합니다. [Peter Johnson](https://weblogs.asp.net/pjohnson/default.aspx)의 블로그 항목 [HttpRuntime.Cache vs. HttpContext.Current.Cache](https://weblogs.asp.net/pjohnson/httpruntime-cache-vs-httpcontext-current-cache) 정보를 사용 하 여에 약간의 성능 우위 `HttpRuntime` 대신 `HttpContext.Current`; 따라서 `ProductsCL` 사용 하 여 `HttpRuntime`합니다.

> [!NOTE]
> 아키텍처에는 클래스 라이브러리 프로젝트를 사용 하 여 구현 된 경우에 대 한 참조를 추가 해야 합니다는 `System.Web` 사용 하려면 어셈블리는 [ `HttpRuntime` ](https://msdn.microsoft.com/en-us/library/system.web.httpruntime.aspx) 및 [ `HttpContext` ](https://msdn.microsoft.com/en-us/library/system.web.httpcontext.aspx) 클래스입니다.


항목이 캐시에 없는 경우는 `ProductsCL` 클래스의 메서드 BLL에서 데이터를 가져오고 사용 하 여 캐시에 추가 된 `AddCacheItem(key, value)` 메서드. 추가할 *값* 캐시에 60 초 시간 만료를 사용 하 여 다음 코드를 사용할 수 있습니다.


[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample7.vb)]

`DateTime.Now.AddSeconds(CacheDuration)`시간 기반 만료 60 초 미래 시간이 지정 [ `System.Web.Caching.Cache.NoSlidingExpiration` ](https://msdn.microsoft.com/en-us/library/system.web.caching.cache.noslidingexpiration(vs.80).aspx) 한다는 문제가 s 슬라이딩 만료 없이 나타냅니다. 이 동안 `Insert` 메서드 오버 로드에는 절대 모두에 대 한 매개 변수를 입력 및 만료 슬라이딩에서는 제공할 수 있습니다만 둘 중 하나입니다. 절대 시간 및 시간 범위를 모두 지정 하려고 하면는 `Insert` 메서드는 throw 된 `ArgumentException` 예외입니다.

> [!NOTE]
> 이 구현에서 `AddCacheItem(key, value)` 메서드에 현재 가지 단점이 있습니다. 4 단계에서에서 이러한 문제를 극복 알아보고 해결 하겠습니다.


## <a name="step-4-invalidating-the-cache-when-the-data-is-modified-through-the-architecture"></a>4 단계: 아키텍처를 통해 수정는 캐시 때의 데이터를 무효화 합니다.

데이터 검색 방법을 함께 캐싱 레이어를 삽입, 업데이트 및 데이터 삭제에 대 한 BLL과 같은 메서드를 제공 해야 합니다. CL의 데이터 수정 메서드는 캐시 된 데이터를 수정 하지 않는 있고 BLL s 해당 데이터 수정 메서드를 호출 하는 대신 다음 캐시를 무효화 합니다. 이것은 해당 캐싱 기능을 사용할 경우의 ObjectDataSource 적용 되는 동일한 동작 이전 자습서에서 살펴본 것 처럼 및 해당 `Insert`, `Update`, 또는 `Delete` 메서드 호출 됩니다.

다음 `UpdateProduct` 오버 로드는 CL의 데이터 수정 메서드를 구현 하는 방법을 보여 줍니다.


[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample8.vb)]

적절 한 데이터 수정 비즈니스 논리 계층 메서드를 호출 하지만 해당 응답을 반환 하기 전에 캐시를 무효화 해야 합니다. 그러나 캐시를 무효화 하지 않습니다 간단 하기 때문에 `ProductsCL` s 클래스 `GetProducts()` 및 `GetProductsByCategoryID(categoryID)` 메서드 각 항목을 캐시에 추가 다른 키를 가진 및 `GetProductsByCategoryID(categoryID)` 메서드 각각에 대해 다양 한 캐시 항목을 추가 고유 *categoryID*합니다.

제거 해야 캐시를 무효화 하는 경우 *모든* 에 의해 추가 된 항목의는 `ProductsCL` 클래스입니다. 이 연결 하 여 수행할 수 있습니다는 *종속성 캐시* 에서 캐시에 추가 된 각 항목에는 `AddCacheItem(key, value)` 메서드. 일반적으로 캐시 종속성에는 캐시, 파일 시스템 또는 Microsoft SQL Server 데이터베이스의에서 데이터 파일에서 다른 항목 일 수 있습니다. 때 종속성 변경 되거나 캐시에서 제거와 연결 된 캐시 항목은 자동으로 캐시에서 제거 합니다. 이 자습서에 대 한 항목을 만드는 추가 역할을 통해 모든 항목에 대 한 캐시 종속성을 추가 하는 캐시에 원하는 `ProductsCL` 클래스입니다. 이런 방식으로 이러한 항목을 모두 제거할 수 캐시에서 캐시 종속성을 제거 하기만 하면 합니다.

Let s 업데이트는 `AddCacheItem(key, value)` 메서드가이 메서드를 통해 캐시에 각 항목을 추가할 수 있도록 연관 된 단일 캐시 종속성:


[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample9.vb)]

`MasterCacheKeyArray`ProductsCache 단일 값을 보유 하는 문자열 배열이입니다. 첫째, 캐시 항목이 캐시에 추가 되 고 현재 날짜 및 시간을 할당 합니다. 캐시 항목이 이미 있는 경우 업데이트 됩니다. 다음으로, 캐시 종속성이 생성 됩니다. [ `CacheDependency` 클래스](https://msdn.microsoft.com/en-US/library/system.web.caching.cachedependency(VS.80).aspx) s 생성자에 다양 한 오버 로드가 있지만 여기에 사용 되는 두 `String` 입력 배열입니다. 첫 번째 파일을 사용 하 여 종속성으로 집합을 지정 합니다. T 값의 모든 파일 기반 종속성을 사용 하려면 것 때문 `Nothing` 첫 번째 입력된 매개 변수에 사용 됩니다. 두 번째 입력된 매개 변수 종속성으로 사용할 캐시 키의 집합을 지정 합니다. 이 단일 종속성 지정 여기 `MasterCacheKeyArray`합니다. `CacheDependency` 다음에 전달 되는 `Insert` 메서드.

이 수정 `AddCacheItem(key, value)`invaliding, 캐시는 하기만 하면 종속성을 제거 합니다.


[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample10.vb)]

## <a name="step-5-calling-the-caching-layer-from-the-presentation-layer"></a>프레젠테이션 계층에서 캐싱 계층을 호출 하는 5 단계:

캐싱 계층의 클래스 및 메서드를 사용할 수 데이터로 작업 하는 기술을 사용 하 여 우리 전체이 자습서에서 설명 했습니다. 를 설명 하기 위해 캐시 된 데이터와 작업에 변경 내용을 저장는 `ProductsCL` 클래스를 열고는 `FromTheArchitecture.aspx` 페이지에 `Caching` 폴더는 GridView를 추가 합니다. GridView s 스마트 태그에서 새 ObjectDataSource를 만듭니다. 마법사 s 첫 번째 단계에 표시 됩니다는 `ProductsCL` 드롭 다운 목록에서 옵션 중 하나로 클래스입니다.


[![ProductsCL 클래스가 포함 되어 있는 비즈니스 개체 드롭다운 목록에서](caching-data-in-the-architecture-vb/_static/image5.png)](caching-data-in-the-architecture-vb/_static/image4.png)

**그림 4**:는 `ProductsCL` 클래스가 비즈니스 개체 드롭다운 목록에 포함 되어 ([전체 크기 이미지를 보려면 클릭](caching-data-in-the-architecture-vb/_static/image6.png))


선택한 후 `ProductsCL`, 다음을 클릭 합니다. 선택 탭의 드롭다운 목록에 두 개의 항목이- `GetProducts()` 및 `GetProductsByCategoryID(categoryID)` 업데이트 탭에는 하나의 및 `UpdateProduct` 오버 로드 합니다. 선택 된 `GetProducts()` 선택 탭에서 메서드 및 `UpdateProducts` 업데이트 탭 클릭에서 방법을 완료 합니다.


[![드롭 다운 목록에 s ProductsCL 클래스 메서드는 나열](caching-data-in-the-architecture-vb/_static/image8.png)](caching-data-in-the-architecture-vb/_static/image7.png)

**그림 5**:는 `ProductsCL` 클래스의 메서드 드롭 다운 목록에 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](caching-data-in-the-architecture-vb/_static/image9.png))


마법사를 완료 한 후 Visual Studio ObjectDataSource s 설정은 `OldValuesParameterFormatString` 속성을 `original_{0}` GridView에 적절 한 필드를 추가 합니다. 변경 된 `OldValuesParameterFormatString` 속성의 기본값을 다시 `{0}`, 및 GridView 페이징, 정렬 및 편집을 지원 하도록 구성 합니다. 이후는 `UploadProducts` CL에서 사용 하는 오버르드 s 편집 된 제품 이름 및 가격 GridView만 이러한 필드는 편집할 수 있도록 제한 합니다.

이전 자습서에 대 한 필드를 포함 하는 GridView 정의 `ProductName`, `CategoryName`, 및 `UnitPrice` 필드입니다. 이 서식 및 구조를 복제할 수 정도,이 경우에 GridView 및 ObjectDataSource s를 선언적 태그 다음과 같이 표시 됩니다.


[!code-aspx[Main](caching-data-in-the-architecture-vb/samples/sample11.aspx)]

이 시점에서 캐싱 계층을 사용 하는 페이지를 했습니다. 작업의 경우 캐시를 보려면에 중단점을 설정는 `ProductsCL` s 클래스 `GetProducts()` 및 `UpdateProduct` 메서드. 정렬 및 데이터를 볼 페이징 캐시에서 추출 하는 경우 코드를 단계별로 브라우저에서 페이지를 참조 하세요. 그런 다음 레코드를 업데이트 하 고 캐시를 무효화 되며, 따라서에서 검색 된 BLL GridView에는 데이터는 다시 바인딩할 때.

> [!NOTE]
> 이 문서와 함께 제공 되는 다운로드에 제공 된 캐싱 레이어 완전 하지 않습니다. 클래스가 하나만 포함 `ProductsCL`, 메서드는 소수의 스포츠입니다. 또한 단일 ASP.NET 페이지를 사용 CL (`~/Caching/FromTheArchitecture.aspx`) 다른 모든 여전히 BLL 직접 참조 합니다. CL 응용 프로그램에서 사용 하려는 경우에 프레젠테이션 계층의 모든 호출은 이동 해야 하는 해야 하는 CL CL의 클래스 및 메서드 포함 이러한 클래스와 프레젠테이션 계층에서 현재 사용 BLL의 메서드.


## <a name="summary"></a>요약

캐싱 ASP.NET 2.0의 SqlDataSource와 프레젠테이션 계층 및 ObjectDataSource 컨트롤에 적용할 수, 하는 동안 이상적으로 책임을 캐싱 것에 위임 될 아키텍처에서 별도 계층입니다. 이 자습서에서는 프레젠테이션 계층 및 비즈니스 논리 계층 사이 위치 하는 캐싱 계층을 만들었습니다. 캐싱 레이어는 동일한 집합이 BLL에 없고 프레젠테이션 계층에서 호출 되는 클래스와 메서드를 제공 해야 합니다.

이 예제와 이전 자습서에서 살펴본 계층 캐싱 예제에서는 *사후 로드*합니다. 사후 로드 하 여 데이터에 대 한 요청이 만들어지면 캐시에서 해당 데이터가 누락 된 경우에 데이터를 캐시에 로드 됩니다. 데이터 일 수도 있습니다 *사전 로드* 를 캐시에는 기술 하는 데이터를 로드를 캐시에 실제로 필요한 전에 합니다. 다음 자습서에서는 응용 프로그램 시작 시 캐시에 정적 값을 저장 하는 방법을 살펴볼 때 사전 로드의 예를 살펴보겠습니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Teresa 머피의 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](caching-data-with-the-objectdatasource-vb.md)
[다음](caching-data-at-application-startup-vb.md)
