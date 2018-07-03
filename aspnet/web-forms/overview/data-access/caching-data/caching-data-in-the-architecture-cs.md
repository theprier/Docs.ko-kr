---
uid: web-forms/overview/data-access/caching-data/caching-data-in-the-architecture-cs
title: 아키텍처 (C#)에서 데이터 캐싱 | Microsoft Docs
author: rick-anderson
description: 이전 자습서에서 프레젠테이션 계층 캐싱 적용 하는 방법을 알게 되었습니다. 이 자습서에서는 계층화 된 architectu를 활용 하는 방법을 알아봅니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/30/2007
ms.topic: article
ms.assetid: d29a7c41-0628-4a23-9dfc-bfea9c6c1054
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-in-the-architecture-cs
msc.type: authoredcontent
ms.openlocfilehash: 20c3c0cb5f3d13e66fbbceab77083c89f3015c53
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37402911"
---
<a name="caching-data-in-the-architecture-c"></a>아키텍처 (C#)에서 데이터 캐싱
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_59_CS.exe) 또는 [PDF 다운로드](caching-data-in-the-architecture-cs/_static/datatutorial59cs1.pdf)

> 이전 자습서에서 프레젠테이션 계층 캐싱 적용 하는 방법을 알게 되었습니다. 이 자습서에서는 비즈니스 논리 계층에서 데이터를 캐시 하는 계층화 된 아키텍처를 활용 하는 방법에 알아봅니다. 캐싱 계층을 포함 하려면 아키텍처를 확장 하 여이 작업을 수행 합니다.


## <a name="introduction"></a>소개

이전 자습서에서 살펴본 것 처럼 데이터를 캐싱하는 ObjectDataSource가 간단 하 게 두 가지 속성을 설정 합니다. 아쉽게도 ObjectDataSource 캐싱 밀접 하 게 ASP.NET 페이지를 사용 하 여 캐싱 정책을 결합 하는 프레젠테이션 계층에 적용 됩니다. 계층화 된 아키텍처를 만드는 이유 중 하나로을 해제 해야 이러한 여기서 허용 하는 것입니다. 예를 들어 비즈니스 논리 계층 데이터 액세스 계층 데이터 액세스 세부 정보를 분리 하는 동안 ASP.NET 페이지에서 비즈니스 논리를 분리 합니다. 비즈니스 논리와 데이터 액세스 세부 정보가 분리는 것이 좋습니다, 부분적으로 더 쉽게 읽을 수를 관리 하 고 변경할 수 있는 유연한 시스템을 했기 때문에 합니다. 도메인 지식 및 프레젠테이션 계층 만들어지고 t에서 작업 하는 개발자가 자신의 작업을 수행 하기 위해 데이터베이스 s 세부 사항을 잘 알고 있어야 해야 분업 수도 있습니다. 프레젠테이션 계층에서 캐싱 정책을 분리는 유사한 이점을 제공 합니다.

이 자습서에 포함 하도록 아키텍처를 살펴보면서를 *캐싱 계층* (또는 줄여서 CL) 캐싱 정책을 사용 합니다. 캐싱 계층을 포함 됩니다는 `ProductsCL` 와 같은 메서드를 사용 하 여 제품 정보에 대 한 액세스를 제공 하는 클래스 `GetProducts()`, `GetProductsByCategoryID(categoryID)`등,를 호출 하는 경우를 캐시에서 데이터를 검색 하는 첫 번째 하려고 합니다. 이러한 메서드는 적절 한 호출 캐시가 비어 있으면 `ProductsBLL` BLL은 DAL에서 데이터를 가져오는 차례로 경우는에서 메서드. `ProductsCL` 메서드는 반환 하기 전에 BLL에서 검색 한 데이터를 캐시 합니다.

그림 1에서 알 수 있듯이, 프레젠테이션 및 비즈니스 논리 계층 간에 CL 상주 합니다.


![캐싱 계층 (CL)는 이러한 아키텍처에서 다른 계층](caching-data-in-the-architecture-cs/_static/image1.png)

**그림 1**: The 캐싱 계층 (CL)는 이러한 아키텍처에서 다른 계층


## <a name="step-1-creating-the-caching-layer-classes"></a>1 단계: 캐싱 계층 클래스 만들기

이 자습서에서는 단일 클래스를 사용 하 여 매우 간단한 CL 만듭니다는 `ProductsCL` 메서드 중 일부만 포함 합니다. 전체 응용 프로그램을 만들기 위해서는 대 한 전체 캐싱 계층을 구축 `CategoriesCL`, `EmployeesCL`, 및 `SuppliersCL` 클래스 및 이러한 캐싱 계층 클래스 BLL에 각 데이터 액세스 또는 수정 방법에 대 한 메서드를 제공 합니다. BLL 및 DAL에서와 마찬가지로 캐싱 계층을 이상적으로 구현 해야 별도 클래스 라이브러리 프로젝트 그러나에서는 구현 하는 클래스에 `App_Code` 폴더입니다.

Let s 클래스 BLL 및 DAL에서에서 더 명확 하 게 별도 CL 클래스의 새 하위 폴더를 만듭니다는 `App_Code` 폴더입니다. 마우스 오른쪽 단추로 클릭 합니다 `App_Code` 솔루션 탐색기의 폴더에에서 새 폴더를 선택 하 고 새 폴더 이름을 `CL`입니다. 이 폴더를 만든 후에 추가 하 라는 새 클래스 `ProductsCL.cs`합니다.


![CL 라는 새 폴더 및 ProductsCL.cs 라는 클래스를 추가 합니다.](caching-data-in-the-architecture-cs/_static/image2.png)

**그림 2**: 라는 새 폴더 추가 `CL` 및 라는 클래스 `ProductsCL.cs`


합니다 `ProductsCL` 클래스는 해당 비즈니스 논리 계층 클래스에 있는 데이터 액세스 및 수정 방법의 동일한 집합을 포함 해야 (`ProductsBLL`). 이러한 모든 메서드를 통해 s만 빌드를 만드는 패턴에 대해 이해할 수 있도록 몇 가지 여기 사용한 CL에서 보다 합니다. 추가한 특히 합니다 `GetProducts()` 하 고 `GetProductsByCategoryID(categoryID)` 3 단계에서에서 메서드 및 `UpdateProduct` 4 단계에서에서 오버 로드. 나머지를 추가할 수 있습니다 `ProductsCL` 메서드 및 `CategoriesCL`를 `EmployeesCL`, 및 `SuppliersCL` 든 클래스입니다.

## <a name="step-2-reading-and-writing-to-the-data-cache"></a>2 단계: 읽기 및 쓰기 데이터 캐시를

내부적으로 이전 자습서에서 탐색 하는 기능을 캐싱 ObjectDataSource BLL에서 검색 된 데이터를 저장할 ASP.NET 데이터 캐시를 사용 합니다. 웹 응용 프로그램의 아키텍처의 클래스 또는 ASP.NET 페이지 코드 숨김 클래스에서 데이터 캐시를 프로그래밍 방식으로 액세스할 수도 있습니다. 에서 읽기 및 쓰기 데이터 캐시에는 ASP.NET 페이지의 코드 숨김 클래스에 다음 패턴을 사용 합니다.


[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample1.cs)]

합니다 [ `Cache` 클래스](https://msdn.microsoft.com/library/system.web.caching.cache.aspx) s [ `Insert` 메서드](https://msdn.microsoft.com/library/system.web.caching.cache.insert.aspx) 에 오버 로드의 수입니다. `Cache["key"] = value` 및 `Cache.Insert(key, value)` 동의어인 정의 만료 없이 지정된 된 키를 사용 하 여 캐시에 항목을 추가 하는 둘 다 고 합니다. 일반적으로 종속성, 시간 기반 만료, 또는 둘 다로 캐시에 항목을 추가 하는 경우 만료를 지정 하려고 합니다. 다른 하나를 사용 하 여 `Insert`의 메서드 오버 로드 종속성 또는 시간 기반 만료 정보를 제공 합니다.

캐싱 계층의 메서드를 처음 요청한 데이터를 캐시에 있으면 및 경우를 확인 해야 합니다. 여기에서 반환 합니다. 요청한 데이터를 캐시에 없는 경우 적절 한 BLL 메서드를 호출 해야 합니다. 반환 값을 캐시 하 고 다음 시퀀스 다이어그램에서 볼 수 있듯이 다음 반환 해야 합니다.


![캐싱 계층의 메서드 경우 캐시에서 데이터를 반환 하기 s 사용 가능](caching-data-in-the-architecture-cs/_static/image3.png)

**그림 3**: The 캐싱 계층의 메서드 경우 캐시에서 데이터를 반환 하기 s 사용 가능


그림 3에 나와 있는 순서는 다음과 같은 패턴을 사용 하 여 CL 클래스에서 수행 됩니다.


[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample2.cs)]

여기에서 *형식* 캐시에 저장 되는 데이터의 형식입니다 `Northwind.ProductsDataTable`, 예를 들어 while *키* 는 캐시 항목을 고유 하 게 식별 하는 키입니다. 하는 경우 지정 된 항목 *키* 한 다음 캐시에 없는 *인스턴스* 됩니다 `null` 및 데이터를 적절 한 BLL 메서드에서 검색 하 고 캐시에 추가 됩니다. 시간 `return instance` 에 도달 *인스턴스* BLL에서 끌어온 또는 캐시에서 데이터에 대 한 참조를 포함 합니다.

캐시에서 데이터에 액세스 하는 경우 위의 패턴을 사용 해야 합니다. 얼핏 보기에 이와 동등한를 표시 하는 다음 패턴을 경합을 소개 하는 미묘한 차이 포함 합니다. 경합 상태는 산발적 변화와 하며 재현 하기 어려운 때문에 디버깅 하기 어렵습니다.


[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample3.cs)]

이 차이 잘못 된 코드는 로컬 변수에 캐시 된 항목에 대 한 참조를 저장, 데이터 캐시를 조건문에 직접 액세스 하지 않고 *하 고* 에 `return`합니다. 이 코드에 도달 하면 상상할 `Cache["key"]` 이 아닌`null`, 전에 `return` 문에 도달 하면, 시스템 제거 *키* 캐시에서 합니다. 드물긴 하지만 이런 경우에는 코드는 반환 된 `null` 예상 되는 형식의 개체 대신 값.

> [!NOTE]
> 데이터 캐시 경우 스레드로부터 안전 하므로 간단한 읽기 또는 쓰기에 대 한 스레드 액세스를 동기화 해야 하는 t 고객은 소트프웨어 그러나, 원자성 해야 하는 캐시에 데이터에서 여러 작업을 수행 해야 할 경우 잠금이 또는 스레드 안전을 보장 하기 위해 다른 메커니즘을 구현할 책임이 됩니다. 참조 [ASP.NET 캐시에 대 한 동기화 액세스](http://www.ddj.com/184406369) 자세한 내용은 합니다.


사용 하 여 데이터 캐시에서 항목을 프로그래밍 방식으로 제거 될 수는 [ `Remove` 메서드](https://msdn.microsoft.com/library/system.web.caching.cache.remove.aspx) 다음과 같이 합니다.


[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample4.cs)]

## <a name="step-3-returning-product-information-from-theproductsclclass"></a>3 단계에서 제품 정보를 반환 합니다`ProductsCL`클래스

이 자습서에서 제품 정보를 반환 하기 위한 두 메서드를 구현 하는 수에 대 한 합니다 `ProductsCL` 클래스: `GetProducts()` 고 `GetProductsByCategoryID(categoryID)`입니다. 와 마찬가지로 `ProductsBL` 비즈니스 논리 계층 클래스는 `GetProducts()` CL에서 메서드는 제품의 모든 정보를 반환 합니다.는 `Northwind.ProductsDataTable` 개체를 하는 동안 `GetProductsByCategoryID(categoryID)` 지정된 된 범주에서 모든 제품을 반환 합니다.

다음 코드의 메서드 중 일부를 보여 줍니다.는 `ProductsCL` 클래스:


[!code-vb[Main](caching-data-in-the-architecture-cs/samples/sample5.vb)]

먼저 확인 합니다 `DataObject` 및 `DataObjectMethodAttribute` 특성 클래스 및 메서드를 적용 합니다. 이러한 특성 마법사의 단계 나타나는 해야 클래스 및 메서드를 나타내는 ObjectDataSource가의 마법사에 정보를 제공 합니다. CL 클래스 및 메서드를 프레젠테이션 계층에서 ObjectDataSource에서 액세스할 수, 있으므로 디자인 타임 환경을 개선 하기 위해 이러한 특성을 추가 했습니다. 다시 참조를 [비즈니스 논리 레이어 만들기](../introduction/creating-a-business-logic-layer-cs.md) 이러한 특성 및 그 영향에 대 한 자세한 설명은 자습서입니다.

에 `GetProducts()` 및 `GetProductsByCategoryID(categoryID)` 메서드에서 반환 되는 데이터는 `GetCacheItem(key)` 메서드가 로컬 변수에 할당 됩니다. 합니다 `GetCacheItem(key)` 기준으로 지정 된 캐시에서 특정 항목을 반환 하는 메서드를 잠시 후에 살펴보겠습니다 *키*합니다. 해당 되는 검색 데이터가 캐시에 있으면 `ProductsBLL` 클래스 메서드 및 사용 하 여 캐시에 추가 된 `AddCacheItem(key, value)` 메서드.

합니다 `GetCacheItem(key)` 고 `AddCacheItem(key, value)` 메서드 각각 데이터 캐시, 읽기 및 쓰기 값을 사용 하 여 인터페이스입니다. `GetCacheItem(key)` 메서드는 둘 중 더 간단 합니다. 전달 기능을 사용 하는 캐시 클래스에서 값을 반환 하기만 *키*:


[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample6.cs)]

`GetCacheItem(key)` 사용 하지 않습니다 *키* 호출 대신 제공 값을 `GetCacheKey(key)` 반환 하는 메서드를 *키* ProductsCache-를 사용 하 여 앞에 추가 합니다. `MasterCacheKeyArray`, 문자열 ProductsCache를 보유 하는 사용 하는 `AddCacheItem(key, value)` 메서드를 일시적으로 볼 수 있겠지만 합니다.

ASP.NET 페이지가 코드 숨김 클래스에서 데이터 캐시를 통해 액세스할 수 있습니다 합니다 `Page` s 클래스 [ `Cache` 속성](https://msdn.microsoft.com/library/system.web.ui.page.cache.aspx), 구문에 대 한 허용 및 `Cache["key"] = value`2 단계에서에서 설명한 것 처럼 합니다. 클래스는 아키텍처 내에서 데이터 캐시를 액세스할 수 있습니다 사용 하 여 `HttpRuntime.Cache` 또는 `HttpContext.Current.Cache`합니다. [Peter Johnson](https://weblogs.asp.net/pjohnson/default.aspx)의 블로그 항목 [HttpRuntime.Cache vs. HttpContext.Current.Cache](https://weblogs.asp.net/pjohnson/httpruntime-cache-vs-httpcontext-current-cache) 정보를 사용 하 여에서 약간의 성능 이점이 `HttpRuntime` 대신 `HttpContext.Current`; 따라서 `ProductsCL` 사용 하 여 `HttpRuntime`입니다.

> [!NOTE]
> 아키텍처는 클래스 라이브러리 프로젝트를 사용 하 여 구현 된 경우에 대 한 참조를 추가 해야 합니다 `System.Web` 사용 하기 위해 어셈블리를 [HttpRuntime](https://msdn.microsoft.com/library/system.web.httpruntime.aspx) 및 [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx) 클래스입니다.


항목이 캐시에 없는 경우는 `ProductsCL` s 클래스 BLL에서 데이터를 가져오는 메서드와 사용 하 여 캐시에 추가 된 `AddCacheItem(key, value)` 메서드. 추가할 *값* 캐시에 60 초 시간 만료를 사용 하는 다음 코드를 사용할 수 했습니다.


[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample7.cs)]

`DateTime.Now.AddSeconds(CacheDuration)` 향후 동안에서 시간 기반 만료 60 초를 지정 [ `System.Web.Caching.Cache.NoSlidingExpiration` ](https://msdn.microsoft.com/library/system.web.caching.cache.noslidingexpiration(vs.80).aspx) 된다는 s 없는 상대 (sliding) 만료를 나타냅니다. 이렇게 하는 동안 `Insert` 메서드 오버 로드에 절대 모두에 대 한 매개 변수를 입력 하 고 슬라이딩 만료를 제공할 수 있습니다만 둘 중 하나입니다. 절대 시간 및 시간 범위를 지정 하려는 경우는 `Insert` 메서드는 throw는 `ArgumentException` 예외입니다.

> [!NOTE]
> 이 구현 된 `AddCacheItem(key, value)` 메서드에 현재 몇 가지 단점이 있습니다. 해결 하 고 4 단계에서에서 이러한 문제를 해결 하겠습니다.


## <a name="step-4-invalidating-the-cache-when-the-data-is-modified-through-the-architecture"></a>4 단계: 아키텍처를 통해 수정는 캐시 때의 데이터를 무효화 합니다.

데이터 검색 방법을 함께 캐싱 레이어를 삽입, 업데이트 및 데이터 삭제에 대 한 BLL과 같은 메서드를 제공 해야 합니다. CL의 데이터 수정 메서드에 캐시 된 데이터를 수정 하지 마십시오 있지만 대신 BLL s 해당 데이터 수정 메서드를 호출 하 고 캐시를 무효화 합니다. 이전 자습서에서 보았듯이이 ObjectDataSource의 캐싱 기능을 사용할 경우 적용 되는 동일한 동작 및 해당 `Insert`, `Update`, 또는 `Delete` 메서드가 호출 됩니다.

다음 `UpdateProduct` 오버 로드에 CL에서 데이터 수정 메서드를 구현 하는 방법을 보여 줍니다.


[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample8.cs)]

적절 한 데이터 수정 비즈니스 논리 계층 메서드를 호출 하지만 응답이 반환 되기 전에 캐시를 무효화 해야 합니다. 그러나 캐시를 무효화 하지 않습니다 간단 하기 때문에 `ProductsCL` s 클래스 `GetProducts()` 하 고 `GetProductsByCategoryID(categoryID)` 메서드 각 항목이 캐시에 추가할 다른 키를 가진 및 `GetProductsByCategoryID(categoryID)` 메서드 각각에 대 한 다양 한 캐시 항목을 추가 고유 *categoryID*합니다.

캐시를 무효화 하는 경우 제거 해야 *모든* 가 추가 했을 수 있는 항목의 합니다 `ProductsCL` 클래스입니다. 연결 하 여이 작업을 수행할 수 있습니다는 *캐시 종속성* 캐시에 추가 되는 각 항목을 사용 하 여는 `AddCacheItem(key, value)` 메서드. 일반적으로 캐시 종속성을 캐시에서 파일 시스템 또는 Microsoft SQL Server 데이터베이스에서 데이터 파일을 다른 항목을 수 있습니다. 때 종속성이 변경 되거나 캐시에서 제거, 연결 된 캐시 항목은 자동으로 캐시에서 제거 합니다. 이 자습서에 대 한 역할을 통해 모든 항목에 대 한 캐시 종속성을 추가 하는 캐시에 추가 항목을 생성 하려는 `ProductsCL` 클래스입니다. 이런 방식으로 이러한 항목을 모두 제거할 수 있습니다 캐시에서 캐시 종속성을 제거 하기만 하면.

Let s 업데이트는 `AddCacheItem(key, value)` 메서드는 캐시에이 메서드를 통해 추가 된 각 항목 있도록 연관 된 단일 캐시 종속성:


[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample9.cs)]

`MasterCacheKeyArray` ProductsCache 단일 값을 보유 하는 문자열 배열이입니다. 첫째, 캐시 항목을 캐시에 추가 되 고 현재 날짜 및 시간을 할당 합니다. 캐시 항목이 이미 있는 경우 업데이트 됩니다. 다음으로, 캐시 종속성을 만들어집니다. 합니다 [ `CacheDependency` 클래스](https://msdn.microsoft.com/library/system.web.caching.cachedependency(VS.80).aspx) s 생성자의 오버 로드가 번호가 이지만 여기에 사용 되 고 두 `string` 입력 배열입니다. 첫 번째 종속성으로 사용할 파일의 집합을 지정 합니다. T 값의 모든 파일 기반 종속성을 사용 하려는 것 이므로 `null` 첫 번째 입력 매개 변수에 사용 됩니다. 두 번째 입력된 매개 변수 종속성으로 사용할 캐시 키 집합을 지정 합니다. 이 단일 종속성 지정 여기 `MasterCacheKeyArray`합니다. 합니다 `CacheDependency` 에 전달 되는 `Insert` 메서드.

이 수정 된 `AddCacheItem(key, value)`invaliding, 캐시 종속성을 제거 하는 것으로 간단 합니다.


[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample10.cs)]

## <a name="step-5-calling-the-caching-layer-from-the-presentation-layer"></a>5 단계: 프레젠테이션 계층에서 캐싱 레이어를 호출합니다.

캐싱 계층의 클래스 및 메서드를 사용할 수 있습니다 데이터로 작업 하는 기술을 사용 하 여에서는이 자습서 전체에서 ve. 캐시 된 데이터를 사용 하 여 작업을 설명 하기 위해 변경 내용을 저장 합니다 `ProductsCL` 클래스를 열고는 `FromTheArchitecture.aspx` 페이지에서 `Caching` 폴더 GridView를 추가 하 고 합니다. GridView가 스마트 태그에서 새 ObjectDataSource를 만듭니다. 마법사가 첫 번째 단계에 표시 됩니다는 `ProductsCL` 드롭 다운 목록에서 옵션 중 하나로 클래스입니다.


[![비즈니스 개체 드롭다운 목록에 포함 되어 ProductsCL 클래스](caching-data-in-the-architecture-cs/_static/image5.png)](caching-data-in-the-architecture-cs/_static/image4.png)

**그림 4**: 합니다 `ProductsCL` 클래스가 비즈니스 개체 드롭다운 목록에 포함 되어 ([클릭 하 여 큰 이미지 보기](caching-data-in-the-architecture-cs/_static/image6.png))


선택한 후 `ProductsCL`, 다음을 클릭 합니다. 선택 탭의 드롭다운 목록에 두 개의 항목이- `GetProducts()` 하 고 `GetProductsByCategoryID(categoryID)` [업데이트] 탭에 있는 유일한 및 `UpdateProduct` 오버 로드 합니다. 선택 된 `GetProducts()` 선택 탭에서 메서드 및 `UpdateProducts` 클릭 하 고 업데이트 탭에서 메서드를 완료 합니다.


[![드롭다운 목록에 s ProductsCL 클래스 메서드가 나와](caching-data-in-the-architecture-cs/_static/image8.png)](caching-data-in-the-architecture-cs/_static/image7.png)

**그림 5**: 합니다 `ProductsCL` s 클래스 메서드는 드롭다운 목록에 나열 됩니다 ([클릭 하 여 큰 이미지 보기](caching-data-in-the-architecture-cs/_static/image9.png))


마법사를 완료 한 후 Visual Studio에는 ObjectDataSource가 설정 됩니다 `OldValuesParameterFormatString` 속성을 `original_{0}` GridView에 적절 한 필드를 추가 합니다. 변경 된 `OldValuesParameterFormatString` 속성의 기본값을 다시 `{0}`, 및 GridView 페이징, 정렬 및 편집을 지원 하도록 구성 합니다. 이후를 `UploadProducts` CL에서 사용 하는 오버 로드만 이러한 필드는 편집할 수 있도록 편집된 제품 s 이름과 가격 제한 GridView를 허용 합니다.

GridView에 대 한 필드를 포함 하려면 이전 자습서에서 정의한 합니다 `ProductName`, `CategoryName`, 및 `UnitPrice` 필드입니다. 이 서식 지정 및 구조를 복제할 자유롭게,이 경우 GridView 및 ObjectDataSource s를 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](caching-data-in-the-architecture-cs/samples/sample11.aspx)]

이 시점에서 캐싱 계층을 사용 하는 페이지를 했습니다. 작업에서 캐시를 보려면에 중단점을 설정 합니다 `ProductsCL` s 클래스 `GetProducts()` 및 `UpdateProduct` 메서드. 정렬 하는 경우 코드를 단계별로 브라우저의 페이지를 방문 하 고 캐시에서 가져온 데이터를 확인 하기 위해 페이징 합니다. 그런 다음 레코드를 업데이트 하 고 캐시를 무효화 되며, 따라서 검색 BLL에서 데이터를 GridView에 다시 바인딩되는 경우.

> [!NOTE]
> 이 기사의 다운로드에 제공 된 캐싱 계층은 완전 하지 않습니다. 클래스가 하나만 포함 `ProductsCL`, 메서드의 소수의 스포츠는 합니다. 또한 단일 ASP.NET 페이지를 사용 CL (`~/Caching/FromTheArchitecture.aspx`) 다른 모든 여전히 BLL을 직접 참조 합니다. CL는 응용 프로그램에서 사용 하려는 경우 프레젠테이션 계층의 모든 호출은 해야 CL 해야 하는 CL의 클래스 이동한 메서드 프레젠테이션 계층에서 현재 사용 하는 BLL에 이러한 메서드와 클래스를 설명 합니다.


## <a name="summary"></a>요약

캐싱을 적용할 수 프레젠테이션 계층을 ASP.NET 2.0의 SqlDataSource 및 ObjectDataSource 컨트롤, 하는 동안 이상적으로 책임을 캐싱는 위임할 수 아키텍처에서 별도 계층입니다. 이 자습서에서는 프레젠테이션 계층 및 비즈니스 논리 계층 사이 있는 캐싱 계층을 만들었습니다. 캐싱 계층 클래스 BLL에 존재 하 고 프레젠테이션 계층에서 호출 되는 메서드 및 동일한 집합을 제공 해야 합니다.

이 단원과 이전 자습서에서 살펴본 계층 캐싱 예제 표시 *반응 형 로드*합니다. 사후 로드를 사용 하 여 데이터에 대 한 요청은 캐시에서 해당 데이터가 누락 된 경우에 데이터를 캐시에 로드 됩니다. 데이터 일 수도 있습니다 *사전에 로드 된* 캐시에 기술 로드 하는 데이터를 캐시에 실제로 필요 하기 전에 합니다. 다음 자습서에서 응용 프로그램 시작 시 캐시에 정적 값을 저장 하는 방법에 살펴봅니다 때 사전 로드 하는 예제를 살펴보겠습니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Teresa Murph 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](caching-data-with-the-objectdatasource-cs.md)
> [다음](caching-data-at-application-startup-cs.md)
