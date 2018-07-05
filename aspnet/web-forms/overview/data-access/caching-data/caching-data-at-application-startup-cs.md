---
uid: web-forms/overview/data-access/caching-data/caching-data-at-application-startup-cs
title: 응용 프로그램 시작 (C#) 시 데이터 캐싱 | Microsoft Docs
author: rick-anderson
description: 모든 웹 응용 프로그램에서 일부 데이터는 자주 사용 됩니다 하 고 일부 데이터는 자주 사용 됩니다. 이 ASP.NET 응용 프로그램 b의 성능을 개선할 수 있습니다...
ms.author: aspnetcontent
ms.date: 05/30/2007
ms.assetid: 22ca8efa-7cd1-45a7-b9ce-ce6eb3b3ff95
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-at-application-startup-cs
msc.type: authoredcontent
ms.openlocfilehash: fdc24f215238a0c44e40a3fcc087230565efa52b
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37829770"
---
<a name="caching-data-at-application-startup-c"></a>응용 프로그램 시작 (C#) 시 데이터 캐싱
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[PDF 다운로드](caching-data-at-application-startup-cs/_static/datatutorial60cs1.pdf)

> 모든 웹 응용 프로그램에서 일부 데이터는 자주 사용 됩니다 하 고 일부 데이터는 자주 사용 됩니다. 이라는 기술을 자주 사용 하는 데이터를 미리 로드 하 여 ASP.NET 응용 프로그램의 성능을 개선할 수 있습니다. 이 자습서에는 응용 프로그램 시작 시 캐시 데이터를 로드 하는 사전 로드는 한 가지 방법을 보여 줍니다.


## <a name="introduction"></a>소개

두 개의 이전 자습서에서 프레젠테이션 및 캐싱 계층에서 데이터 캐싱 살펴보았습니다. [ObjectDataSource 사용 하 여 데이터 캐싱](caching-data-with-the-objectdatasource-cs.md)를 사용 하는 ObjectDataSource 캐싱 프레젠테이션 계층에서 데이터를 캐시 하는 기능에 살펴보았습니다. [아키텍처에서 데이터 캐싱](caching-data-in-the-architecture-cs.md) 새, 별도 캐시 계층의 캐시를 검사 합니다. 사용 되는 다음이 자습서 중 둘 다 *사후 로드* 데이터 캐시를 사용 하 여 작업 합니다. 반응 형 로드, 데이터 요청 될 때마다 시스템 먼저 확인 하는 경우 해당 캐시의 합니다. 그렇지 않은 경우 데이터베이스와 같은 원래 원본에서 데이터를 가져와 하 고 캐시에 저장 합니다. 주요 이점은 반응 로딩 구현의 해당 간편 하다는 점입니다. 해당 단점 중 하나에 요청 간에 균등 하지 않은 성능입니다. 제품 정보를 표시 하려면 이전 자습서에서 캐싱 레이어를 사용 하는 페이지를 가정해 보겠습니다. 이 페이지를 처음으로 방문 하거나 캐시 된 데이터를 메모리 제약 조건 또는 도달 하지 하는 지정 된 만료로 인해 제거 된 후 처음으로 방문 때 데이터베이스에서 데이터를 검색 해야 합니다. 따라서 이러한 사용자 요청 캐시에서 제공 될 수 있는 사용자 요청 보다 오래 걸릴 됩니다.

*사전 로드* 제공 대체 캐시 관리 전략을 성능을 완만 하 게 하 요청 간에 필요한 하기 전에 캐시 된 데이터를 로드 합니다. 일반적으로 사전 로드 하거나 정기적으로 검사 또는 기본 데이터에 대 한 업데이트 된 경우 알림을 보낼지는 일부 프로세스를 사용 합니다. 이 프로세스는 다음 최신 상태로 유지 하려면 캐시를 업데이트 합니다. 사전 로드 느린 데이터베이스 연결, 웹 서비스 또는 다른 특히 느린 데이터 원본에서 기본 데이터를 가져오는 경우에 특히 유용 합니다. 하지만이 방법은 사전 로드는 만들기, 관리 및 배포 하는 변경 내용을 확인 하 고 캐시를 업데이트 하는 프로세스 필요 하므로 구현 하기가 더 어렵습니다.

이 자습서에서는 탐색 하려는 형식과 사전 로드의 또 다른 버전을 응용 프로그램 시작 시 캐시에 데이터를 로드 합니다. 이 방법은 데이터베이스 조회 테이블의 레코드와 같은 정적 데이터를 캐시 하는 데 특히 유용 합니다.

> [!NOTE]
> 장점과 단점, 구현 권장 사항 목록 뿐만 아니라 사전 및 사후 로드 간의 차이점에 대 한 자세한 설명에 대 한 참조를 [캐시의 내용을 관리](https://msdn.microsoft.com/library/ms978503.aspx) 섹션을 [ .NET Framework 응용 프로그램 아키텍처 가이드 캐싱](https://msdn.microsoft.com/library/ms978498.aspx)합니다.


## <a name="step-1-determining-what-data-to-cache-at-application-startup"></a>1 단계: 응용 프로그램 시작 시 캐시 데이터를 확인합니다.

캐싱 예제는 사후 로드를 사용 하 여 생성 하기 위해 데이터는 주기적으로 변경 될 수 있으며는 exorbitantly 오래 걸리지 않습니다 잘 이전 두 자습서 작업에서 검사 했습니다. 이지만 캐시 된 데이터를 변경 하지 않는 경우 사후 로드에서 사용 하는 만료 불필요 합니다. 마찬가지로, 생성 되 고 캐시 된 데이터를 사용 하는 매우 긴 시간이 요청이 찾을 캐시 빈 데이터 원본으로 사용 하는 동안 긴 대기를 허용 해야 합니다. 해당 사용자가 검색 됩니다. 정적 데이터 및 응용 프로그램 시작 시 생성 하는 매우 긴 시간이 소요 되는 데이터를 캐시 하는 것이 좋습니다.

데이터베이스 많은 동적이 자주 변경 값을 대부분 정적 데이터의 상당한이 있을 합니다. 예를 들어, 거의 모든 데이터 모델 선택 항목의 고정된 된 집합에서 특정 값이 포함 된 하나 이상의 열을 가집니다. A `Patients` 데이터베이스 테이블에 있는 `PrimaryLanguage` 열, 영어, 스페인어, 프랑스어, 러시아어, 일본어 및 등 값 집합이 될 수 없습니다. 사용 하 여 이러한 유형의 열은 구현 경우가 많습니다 *조회 테이블*합니다. 영어 또는의 프랑스어 문자열을 저장 하는 대신는 `Patients` 테이블, 두 번째 테이블을 만들 열이 있는, 일반적으로 두 개의 고유 식별자 및 문자열 설명을-가능한 각 값에 대 한 레코드를 사용 하 여 합니다. 합니다 `PrimaryLanguage` 열에는 `Patients` 테이블 조회 테이블에서 해당 고유 식별자를 저장 합니다. 그림 1에서 환자 John Doe가 기본 언어는 영어, Ed Johnson s는 러시아어입니다.


![언어 테이블이 Patients 테이블에서 조회 테이블 사용](caching-data-at-application-startup-cs/_static/image1.png)

**그림 1**: 합니다 `Languages` 테이블에서 조회 테이블 사용 되는 `Patients` 테이블


새 환자를 만들거나 편집에 대 한 사용자 인터페이스를 허용 되는 언어의 레코드에 채워지는 드롭다운 목록이 포함 된 `Languages` 테이블입니다. 이 인터페이스는 때마다 캐싱 없이 시스템을 방문한 쿼리해야는 `Languages` 테이블. 이 경우 낭비 되 고 불필요 한 조회 테이블 값이 자주 변경 되므로 적입니다.

캐시 수를 `Languages` 이전 자습서에서 검사할 동일한 사후 로드 기술을 사용 하 여 데이터입니다. 하지만 정적 조회 테이블 데이터에 대 한 필요 하지 않습니다 하는 시간 기반 만료를 사용, 사후 로드 합니다. 반응 형 로드를 사용 하 여 캐싱용 캐싱 전혀 없음 보다 더 좋을 수, 하는 동안 가장 좋은 방법은 응용 프로그램 시작 시 캐시에 사전 조회 테이블 데이터를 로드 하려면 것입니다.

이 자습서에서는 캐시 조회 테이블 데이터와 기타 정적 정보와 하는 방법을 살펴보겠습니다.

## <a name="step-2-examining-the-different-ways-to-cache-data"></a>2 단계: 데이터를 캐시에 대 한 다양 한 방법 검사

다양 한 방법 사용 하 여 ASP.NET 응용 프로그램에서 정보를 프로그래밍 방식으로 캐시할 수 있습니다. 에서는 ve 이미 이전 자습서에서 데이터 캐시를 사용 하는 방법을 살펴보았습니다. 또는 개체 프로그래밍 방식으로 캐시할 수를 사용 하 여 *정적 멤버* 하거나 *응용 프로그램 상태*합니다.

클래스를 사용할 때는 일반적으로 클래스 먼저 전에 인스턴스화되어야 합니다 해당 멤버에 액세스할 수 있습니다. 예를 들어이 비즈니스 논리 계층의 클래스 중 하나에서 메서드를 호출 하려면 클래스의 인스턴스 먼저 만들어야 합니다.


[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample1.cs)]

전에 호출할 수 있습니다 *SomeMethod* 하거나 작업할 *SomeProperty*를 사용 하 여 클래스의 인스턴스 먼저 만들어야 합니다를 `new` 키워드입니다. *SomeMethod* 하 고 *SomeProperty* 특정 인스턴스와 연결 합니다. 이러한 멤버의 수명 동안 해당 연결된 개체의 수명에 연결 됩니다. *정적 멤버*, 변수, 속성 및 메서드 간에 공유 되는 반면에 *모든* 클래스 인스턴스의 및 결과적으로 수명이 클래스도 합니다. 정적 멤버는 다음과 같은 키워드로 표시 됩니다. `static`합니다.

정적 멤버 외에도 응용 프로그램 상태를 사용 하 여 데이터를 캐시할 수 있습니다. 각 ASP.NET 응용 프로그램 이름/값 컬렉션을 모든 사용자 및 응용 프로그램의 페이지 간에 공유 되는 s를 유지 관리 합니다. 사용 하 여이 컬렉션에 액세스할 수 합니다 [ `HttpContext` 클래스](https://msdn.microsoft.com/library/system.web.httpcontext.aspx) s [ `Application` 속성](https://msdn.microsoft.com/library/system.web.httpcontext.application.aspx), ASP.NET 페이지의 코드 숨김 클래스에서 사용 하 고 다음과 같이:


[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample2.cs)]

데이터 캐시 시간 및 종속성 기반 expiries, 캐시 항목 우선 순위 등 메커니즘을 제공 하는 데이터를 캐시 하는 훨씬 더 풍부한 API를 제공 합니다. 정적 멤버 및 응용 프로그램 상태를 사용 하 여 이러한 기능 페이지 개발자가 수동으로 추가 해야 합니다. 그러나 응용 프로그램의 수명에 대 한 응용 프로그램 시작 시 데이터를 캐시할 때 데이터 캐시 s 장점은 이론에 불과합니다. 이 자습서에서는 정적 데이터를 캐시에 대 한 세 가지 기술 모두를 사용 하는 코드에서 살펴보겠습니다.

## <a name="step-3-caching-thesupplierstable-data"></a>3 단계: 캐시 된`Suppliers`데이터 테이블

Ve 누계 구현에서는 데이터베이스 테이블에서 Northwind는 기존의 조회 테이블을 포함 하지 않습니다. DAL에서 해당 값은 static이 아니고 모든 모델 테이블 구현 하는 4 개의 Datatable입니다. DAL 및 다음 새 클래스 BLL은 방법 새 DataTable을 추가 하는 데 시간을 소비 하는 대신이 자습서에서 s를 방금 수에 대 한 가정 하는 `Suppliers`의 테이블 데이터는 정적입니다. 따라서 응용 프로그램 시작 시이 데이터 캐시 수 없습니다.

시작 하려면 라는 새 클래스를 만듭니다 `StaticCache.cs` 에 `CL` 폴더입니다.


![CL 폴더에서 StaticCache.cs 클래스 만들기](caching-data-at-application-startup-cs/_static/image2.png)

**그림 2**: 만들기 합니다 `StaticCache.cs` 클래스는 `CL` 폴더


이 캐시에서 데이터를 반환 하는 방법 뿐만 아니라 적절 한 캐시 스토어에 시작 시 데이터를 로드 하는 메서드를 추가 해야 합니다.


[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample3.cs)]

위의 코드에서 정적 멤버 변수를 사용 `suppliers`의 결과 보관 하는 `SuppliersBLL` s 클래스 `GetSuppliers()` 에서 호출 되는 메서드를 `LoadStaticCache()` 메서드. `LoadStaticCache()` 메서드는 응용 프로그램의 시작 하는 동안 호출 될 것입니다. 응용 프로그램 시작 시이 데이터를 로드, 공급 업체 데이터를 사용 해야 하는 모든 페이지 호출 수를 `StaticCache` s 클래스 `GetSuppliers()` 메서드. 따라서 공급자를 가져오려면 데이터베이스에 대 한 호출에만 발생 한 번 응용 프로그램 시작 합니다.

캐시 저장소로 정적 멤버 변수를 사용 하는 대신 또는 사용 응용 프로그램 상태 또는 데이터 캐시 합니다. 다음 코드를 응용 프로그램 상태를 사용 하려면 retooled 클래스를 보여 줍니다.


[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample4.cs)]

`LoadStaticCache()`, 공급 업체 정보를 응용 프로그램 변수에 저장 됩니다 *키*합니다. 것이 적절 한 형식으로 반환 (`Northwind.SuppliersDataTable`)에서 `GetSuppliers()`합니다. 응용 프로그램 상태를 사용 하 여 ASP.NET 페이지의 코드 숨김 클래스에서 액세스할 수 있습니다 하는 동안 `Application["key"]`, 아키텍처를 사용 해야 합니다 `HttpContext.Current.Application["key"]` 현재 얻으려면 `HttpContext`합니다.

마찬가지로, 다음 코드와 같이 캐시 저장소로 데이터 캐시를 사용할 수 있습니다.


[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample5.cs)]

시간 기반 만료 되지 않도록 데이터 캐시에 항목을 추가 하려면 사용 합니다 `System.Web.Caching.Cache.NoAbsoluteExpiration` 및 `System.Web.Caching.Cache.NoSlidingExpiration` 입력된 매개 변수 값입니다. S 데이터 캐시의이 특정 오버 로드 `Insert` 지정할 수 있도록 선택한 메서드를 *우선 순위* 캐시 항목의 합니다. 우선 순위는 사용 가능한 메모리가 부족 하면 캐시에서 청소에 항목을 결정 하는 데 사용 됩니다. 여기서 사용 하 여 우선 순위 `NotRemovable`, 청소이 캐시 항목-t 이득 있는지 확인 하는 합니다.

> [!NOTE]
> 이 자습서가의 다운로드를 구현 하는 `StaticCache` 클래스 정적 멤버 변수 접근 방식을 사용 합니다. 응용 프로그램 상태 및 데이터 캐시 기술에 대 한 코드는 클래스 파일의 주석을 사용할 수 있습니다.


## <a name="step-4-executing-code-at-application-startup"></a>4 단계: 응용 프로그램 시작 시 코드를 실행합니다.

를 웹 응용 프로그램을 처음 시작할 때 코드를 실행 하려면 이라는 특수 파일을 만듭니다 해야 `Global.asax`합니다. 이 파일에 대 한 응용 프로그램, 세션-이벤트 처리기를 포함할 수 있습니다 하 고 요청 수준 이벤트 되며 여기 있는 응용 프로그램이 시작 될 때마다 실행 코드를 추가할 수 있습니다.

추가 된 `Global.asax` 파일을 Visual Studio가의 솔루션 탐색기에서에서 웹 사이트 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가 선택 하 여 웹 응용 프로그램의 루트 디렉터리입니다. 새 항목 추가 대화 상자에서 전역 응용 프로그램 클래스 항목 종류를 선택 하 고 추가 단추를 클릭 합니다.

> [!NOTE]
> 이미 있는 경우는 `Global.asax` 프로젝트 항목 형식의 새 항목 추가 대화 상자에서 나열 되지 것입니다 하 고 전역 응용 프로그램 클래스에에서는 파일입니다.


[![웹 응용 프로그램 s 루트 디렉터리를 Global.asax 파일 추가](caching-data-at-application-startup-cs/_static/image4.png)](caching-data-at-application-startup-cs/_static/image3.png)

**그림 3**: 추가 된 `Global.asax` 웹 응용 프로그램 루트 디렉터리에 파일 ([클릭 하 여 큰 이미지 보기](caching-data-at-application-startup-cs/_static/image5.png))


기본값 `Global.asax` 서버 쪽에서 5 개의 메서드를 포함 하는 파일 템플릿을 `<script>` 태그:

- **`Application_Start`** 웹 응용 프로그램을 처음 시작할 때 실행
- **`Application_End`** 응용 프로그램이 종료 될 때 실행 됩니다.
- **`Application_Error`** 처리 되지 않은 예외로 응용 프로그램에 도달할 때마다 실행
- **`Session_Start`** 새 세션을 만들 때 실행
- **`Session_End`** 세션이 만료 되거나 중단 하면 실행 됩니다.

`Application_Start` s 응용 프로그램 수명 주기 동안 이벤트 처리기가 한 번만 호출 합니다. 처음으로 ASP.NET 리소스 응용 프로그램에서 요청 하는 응용 프로그램을 다시 시작 때까지 계속 실행의 내용을 수정 하 여 발생할 수 있는 응용 프로그램을 시작 합니다 `/Bin` 폴더를 수정 `Global.asax`수정는 콘텐츠를 `App_Code` 폴더 또는 수정 합니다 `Web.config` 다른 원인이 간에 파일. 가리킵니다 [ASP.NET 응용 프로그램 수명 주기 개요](https://msdn.microsoft.com/library/ms178473.aspx) 응용 프로그램 수명 주기에 대 한 자세한 논의 합니다.

이 자습서에서는 하기만 코드를 추가 하는 `Application_Start` 메서드, 따라서 자유롭게 다른를 제거 합니다. `Application_Start`를 호출 하기만 하면 됩니다 합니다 `StaticCache` s 클래스 `LoadStaticCache()` 메서드를 로드 하 고 공급 업체 정보를 캐시:


[!code-aspx[Main](caching-data-at-application-startup-cs/samples/sample6.aspx)]

S 모두 완료 되었습니다! 응용 프로그램 시작 시 합니다 `LoadStaticCache()` 메서드는 BLL은에서 공급 업체 정보를 얻 및 정적 멤버 변수에 저장 (또는 원하는 캐시 저장에 사용 하 여 종료를 `StaticCache` 클래스). 이 동작을 확인 하려면에서 중단점을 설정 합니다 `Application_Start` 메서드 및 응용 프로그램을 실행 합니다. 응용 프로그램 시작 시이 중단점 note 합니다. 하지만 후속 요청 하지 않게 된 `Application_Start` 메서드를 실행 합니다.


[![Application_Start 이벤트 처리기가 실행 되 고 확인 하도록 중단점을 사용 하 여](caching-data-at-application-startup-cs/_static/image7.png)](caching-data-at-application-startup-cs/_static/image6.png)

**그림 4**: 확인에 중단점을 사용 하는 합니다 `Application_Start` 이벤트 처리기가 실행 중인 ([전체 크기 이미지를 보려면 클릭](caching-data-at-application-startup-cs/_static/image8.png))


> [!NOTE]
> 에 도달 하지 하는 경우는 `Application_Start` 먼저 디버깅을 시작할 때 중단점을 있기 때문에 응용 프로그램이 이미 시작 되었습니다. 응용 프로그램을 수정 하 여 다시 시작을 강제 하 `Global.asax` 또는 `Web.config` 파일을 다시 시도 하십시오. 있습니다 수 단순히 추가 (또는 제거) 끝 신속 하 게 응용 프로그램 다시 시작 하려면 이러한 파일 중 하나에 빈 줄.


## <a name="step-5-displaying-the-cached-data"></a>5 단계: 캐시 된 데이터를 표시합니다.

이 시점에서 `StaticCache` 클래스를 통해 액세스할 수 있는 응용 프로그램 시작 시 캐시 데이터 중 버전이 해당 `GetSuppliers()` 메서드. 프레젠테이션 계층에서이 데이터를 사용 하려면 ObjectDataSource를 사용 하거나 프로그래밍 방식으로 호출할 수는 `StaticCache` s 클래스 `GetSuppliers()` ASP.NET의 페이지 코드 숨김 클래스에서 메서드. S를 ObjectDataSource와 GridView 컨트롤을 사용 하 여 캐시 된 공급 업체 정보를 표시 하려면 살펴볼 수 있습니다.

열어서 시작 합니다 `AtApplicationStartup.aspx` 페이지에 `Caching` 폴더입니다. 설정 디자이너 도구 상자에서 GridView를 끌어 해당 `ID` 속성을 `Suppliers`입니다. 그런 다음 GridView에서 s 스마트 태그 선택 라는 새로운 ObjectDataSource는 만들려는 `SuppliersCachedDataSource`합니다. ObjectDataSource를 사용 하 여 구성 합니다 `StaticCache` s 클래스 `GetSuppliers()` 메서드.


[![StaticCache 클래스를 사용 하는 ObjectDataSource 구성](caching-data-at-application-startup-cs/_static/image10.png)](caching-data-at-application-startup-cs/_static/image9.png)

**그림 5**: ObjectDataSource 사용 하도록 구성 된 `StaticCache` 클래스 ([클릭 하 여 큰 이미지 보기](caching-data-at-application-startup-cs/_static/image11.png))


[![GetSuppliers() 메서드를 사용 하 여 캐시 된 공급자 데이터를 검색 합니다.](caching-data-at-application-startup-cs/_static/image13.png)](caching-data-at-application-startup-cs/_static/image12.png)

**그림 6**: 사용 된 `GetSuppliers()` 캐시 공급자 데이터를 검색 하는 방법 ([전체 크기 이미지를 보려면 클릭](caching-data-at-application-startup-cs/_static/image14.png))


마법사를 완료 한 후 Visual Studio는 자동으로 추가 BoundFields 각 데이터 필드에 대 한 `SuppliersDataTable`합니다. GridView 및 ObjectDataSource가 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](caching-data-at-application-startup-cs/samples/sample7.aspx)]

그림 7에서는 브라우저를 통해 볼 때 페이지를 보여 줍니다. 출력은 동일한 BLL s에서 데이터를 우리가 가져온 했습니다 `SuppliersBLL` 클래스를 하지만 사용 하 여는 `StaticCache` 클래스에는 응용 프로그램 시작 시 캐시 된 공급자 데이터를 반환 합니다. 중단점을 설정할 수는 `StaticCache` s 클래스 `GetSuppliers()` 이 동작을 확인 하는 방법입니다.


[![캐시 된 공급자 데이터를 GridView에 표시 됩니다.](caching-data-at-application-startup-cs/_static/image16.png)](caching-data-at-application-startup-cs/_static/image15.png)

**그림 7**: 캐시 된 공급자 데이터를 GridView에 표시 됩니다 ([큰 이미지를 보려면 클릭](caching-data-at-application-startup-cs/_static/image17.png))


## <a name="summary"></a>요약

대부분의 모든 데이터 모델에는 일반적으로 조회 테이블의 형태로 구현 하는 정적 데이터의 상당한 포함 되어 있습니다. 이 정보는 정적 이므로 여기가이 정보를 표시 해야 합니다. 계속 해 서 데이터베이스에 액세스할 때마다 이유가 없습니다. 데이터를 캐시 하는 경우 고정 특성으로 인해 또한 s 여기 만료 필요 하지 않습니다. 이 자습서에서 이러한 데이터를 가져오고 정적 멤버 변수를 통해 응용 프로그램 상태 데이터 캐시에 캐시 하는 방법을 살펴보았습니다. 이 정보는 응용 프로그램 시작 시 캐시 되 고 s 응용 프로그램 수명 동안 캐시에 유지 됩니다.

이 자습서에는 지난 2에서는 ve 데이터 응용 프로그램의 수명 기간에 대 한 캐싱 뿐만 아니라 시간 기반 expiries를 사용 하 여 살펴보았습니다. 데이터베이스 데이터를 캐시 하지만 시간 기반 만료 될 수 있습니다 썩 훌륭하지 않습니다. 주기적으로 캐시를 플러시에 대신 기본 데이터베이스 데이터 수정 될 때만 캐시 된 항목을 제거 하는 데 가장 적합 한 것입니다. 다음 자습서에서 살펴봅니다 SQL 캐시 종속성을 사용 하 여이 이상적 모델이이 실현 불가능 해제 합니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자는 Teresa Murphy 및 Zack Jones 있었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](caching-data-in-the-architecture-cs.md)
> [다음](using-sql-cache-dependencies-cs.md)
