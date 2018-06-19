---
uid: web-forms/overview/data-access/caching-data/caching-data-at-application-startup-vb
title: 응용 프로그램 시작 (VB)에서 데이터를 캐시 | Microsoft Docs
author: rick-anderson
description: 모든 웹 응용 프로그램에서 일부 데이터는 자주 사용 됩니다 하 고 일부 데이터는 자주 사용 됩니다. 이 ASP.NET 응용 프로그램 b의 성능을 개선할 수 있는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/30/2007
ms.topic: article
ms.assetid: 84afe4ac-cc53-4f2e-a867-27eaf692c2df
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-at-application-startup-vb
msc.type: authoredcontent
ms.openlocfilehash: f8f322dae89480fc7ed5586d7f8eeb4c67d7839f
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30876347"
---
<a name="caching-data-at-application-startup-vb"></a>응용 프로그램 시작 (VB)에서 데이터 캐싱
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[PDF 다운로드](caching-data-at-application-startup-vb/_static/datatutorial60vb1.pdf)

> 모든 웹 응용 프로그램에서 일부 데이터는 자주 사용 됩니다 하 고 일부 데이터는 자주 사용 됩니다. 으로 자주 사용 하는 데이터를 미리 로드 하 여 ASP.NET 응용 프로그램의 성능을 개선할 수 있습니다. 이 자습서에서는 응용 프로그램 시작 시 캐시에 데이터를 로드 하는 사전 로드 하는 한 가지 방법을 설명 합니다.


## <a name="introduction"></a>소개

두 이전 자습서 프레젠테이션 및 캐싱 계층에서 데이터 캐싱 살펴보았습니다. [는 ObjectDataSource 사용 하 여 데이터 캐싱을](caching-data-with-the-objectdatasource-vb.md), ObjectDataSource s 캐싱 프레젠테이션 계층에서 데이터를 캐시 하는 기능을 사용 하 여 찾았습니다. [아키텍처에서 데이터 캐싱](caching-data-in-the-architecture-vb.md) 새 별도 캐싱 계층에서 캐시를 검사 합니다. 사용 되는이 자습서의 둘 다 *사후 로드* 데이터 캐시를 사용 합니다. 사후 로드할 데이터가 요청 될 때마다 시스템 먼저 확인 하는 경우이 캐시에는 s입니다. 그렇지 않으면 데이터베이스와 같은 원래 원본의 데이터를 가져와 하 고 캐시에 저장 합니다. 사후 로드 주요 장점은 구현 편이성입니다. 단점 중 하나에 요청에 대해 균일 하지 않은 성능입니다. 이전 자습서에서 캐싱 레이어를 사용 하 여 제품 정보를 표시 하는 페이지를 가정해 봅니다. 이 페이지를 처음으로 방문 하거나 캐시 된 데이터가 메모리 제약 조건 또는 필요에 도달 하면 지정 된 만료로 인해 제거 된 후 처음으로 방문한 때 데이터베이스에서 데이터를 검색 해야 합니다. 따라서 이러한 사용자가 요청 캐시에 의해 제공 될 수 있는 사용자가 요청에 비해 시간이 소요 됩니다.

*사전 로드* 제공 대체 캐시 관리 전략의 성능 모색 완만 하 게 하 요청에 대해 필요한 하기 전에 캐시 된 데이터를 로드 하 여 합니다. 일반적으로 사전 로드 중 하나 주기적으로 검사 또는 기본 데이터에 대 한 업데이트 되었을 때 알림을 보낼지 여부를 지정 하는 일부 프로세스를 사용 합니다. 이 프로세스는 다음 최신 상태로 유지 하려면 캐시를 업데이트 합니다. 사전 로드 느린 데이터베이스 연결, 웹 서비스 또는 다른 특히 느려지는 데이터 소스에서 제공 되는 기본 데이터의 경우 특히 유용 합니다. 하지만 만들고 관리 하 고 변경 내용을 확인 하 고 캐시를 업데이트 하는 프로세스를 배포 해야 하므로이 방법은 사전 로드 하는 구현 하려면 더 어렵습니다.

사전 로드 및 살펴보겠습니다이 자습서에서는 형식이 다른 버전은 응용 프로그램 시작 시 캐시에 데이터를 로드 합니다. 이 방법은 데이터베이스 조회 테이블의 레코드와 같은 정적 데이터를 캐싱하는 데 특히 유용 합니다.

> [!NOTE]
> 장점과 단점을 구현 권장 사항 목록 뿐만 아니라 사전 예방적 이며 반응 적인 로드 간의 차이점에 대 한 자세한 설명에 대 한 참조는 [캐시의 내용을 관리](https://msdn.microsoft.com/library/ms978503.aspx) 의 섹션은 [ .NET Framework 응용 프로그램에 대 한 아키텍처 가이드 캐싱](https://msdn.microsoft.com/library/ms978498.aspx)합니다.


## <a name="step-1-determining-what-data-to-cache-at-application-startup"></a>1 단계: 응용 프로그램 시작 시 캐시 데이터 확인

사후 로드를 사용 하 여 캐싱 예제 생성 하기 위해 데이터를 주기적으로 변경 될 수 있으며 exorbitantly 오래 사용 하지 않는 함께 이전 두 자습서 작업에서 검사 했습니다. 그러나 경우 캐시 된 데이터는 바뀌지 사후 로드에서 사용 하는 만료 불필요 한 있습니다. 마찬가지로, 생성 하 되 고 캐시 된 데이터를 사용 하는 매우 긴 시간이 인 요청 캐시 빈 endure 데이터 원본으로 사용 하는 동안 시간이 오래 걸리는 대기 해야 합니다를 찾을 사용자 검색 됩니다. 정적 데이터와 응용 프로그램 시작 시 생성 하는 매우 긴 시간이 소요 되는 데이터를 캐시 하는 것이 좋습니다.

데이터베이스가 많은 동적 값을 가장 자주 변경 정적 데이터에 대 한 상당한 양의 있을 합니다. 예를 들어 거의 모든 데이터 모델 고정 목록에서에서 특정 값을 포함 하는 열을 하나 이상 있어야 합니다. A `Patients` 데이터베이스 테이블에 있는 한 `PrimaryLanguage` 열에서 영어, 스페인어, 프랑스어, 러시아어, 일본어, 및 등 해당 값 집합을 수 있습니다. 사용 하 여 이러한 유형의 열은 구현 하는 경우도 많습니다 *조회 테이블*합니다. 영어 또는 프랑스어 문자열을 저장 하는 대신는 `Patients` 테이블을 두 번째 테이블을 만들 수 있는 각 값에 대 한 레코드와 두 개의 열-한 고유 식별자 및 설명 문자열-일반적으로 있습니다. `PrimaryLanguage` 열에는 `Patients` 테이블 조회 테이블에 해당 하는 고유 식별자를 저장 합니다. 그림 1에서 환자 John Doe s र ा थ는 Ed Johnson s 러시아어는 영어입니다.


![언어 테이블은 Patients 테이블에서 조회 테이블 사용](caching-data-at-application-startup-vb/_static/image1.png)

**그림 1**:는 `Languages` 테이블에서 조회 테이블 사용은 `Patients` 테이블


편집 하거나 만들 새 환자에 대 한 사용자 인터페이스에는 허용 가능한 언어의 레코드에 의해 채워진 드롭다운 목록이 포함 됩니다는 `Languages` 테이블입니다. 이 인터페이스는 때마다, 캐싱이 설정 되지 않은 시스템을 방문 쿼리해야는 `Languages` 테이블입니다. 이 불필요 불필요 한 조회 테이블의 값이 자주 변경 취소가 있더라도 있습니다.

캐시 수는 `Languages` 이전 자습서에서 검토할 동일한 사후 로드 기법을 사용 하 여 데이터입니다. 하지만 정적 조회 테이블 데이터에 대 한 필요 하지 않은 시간 기반 만료를 사용 사후 로드 합니다. 사후 로드를 사용 하 여 캐싱 캐싱이나 캐싱 전혀 보다 더 나은 것, 하는 동안 가장 좋은 방법은 사전 조회 테이블 데이터를 응용 프로그램 시작 시 캐시에 로드 하는 것입니다.

이 자습서에서는 캐시 조회 테이블 데이터와 기타 정적 정보 하는 방법을 살펴보겠습니다.

## <a name="step-2-examining-the-different-ways-to-cache-data"></a>2 단계: 데이터를 캐시 하는 여러 가지 방법을 검사

다양 한 방법 사용 하 여 ASP.NET 응용 프로그램에서 정보를 프로그래밍 방식으로 캐시할 수 있습니다. म 했습니다 이미 이전 자습서의 데이터 캐시를 사용 하는 방법을 확인 합니다. 또는 개체 수 프로그래밍 방식으로 캐시를 사용 하 여 *정적 멤버* 또는 *응용 프로그램 상태*합니다.

클래스를 사용할 때는 일반적으로 클래스 먼저 인스턴스화되어야 해당 멤버를 액세스할 수 있습니다. 예를 들어이 비즈니스 논리 계층의 클래스 중 하나에서 메서드를 호출 하려면 먼저 만들어야 클래스의 인스턴스:


[!code-vb[Main](caching-data-at-application-startup-vb/samples/sample1.vb)]

수 전에 *SomeMethod* 하거나 작업할 *SomeProperty*, 사용 하 여 클래스의 인스턴스 먼저 만들어야는 `New` 키워드입니다. *SomeMethod* 및 *SomeProperty* 특정 인스턴스와 연결 됩니다. 이러한 멤버의 수명은 해당 연결 된 개체의 수명에 연결 됩니다. *정적 멤버*, 변수, 속성 및 메서드 간에 공유 되는 반면에 *모든* 클래스 인스턴스의 따라서 수명은 클래스는 및입니다. 키워드에 의해 표시 됩니다. 정적 멤버 `Shared`합니다.

정적 멤버 뿐만 아니라 응용 프로그램 상태를 사용 하 여 데이터를 캐시할 수 있습니다. 각 ASP.NET 응용 프로그램 모든 사용자 및 응용 프로그램의 페이지에서 공유 s 이름/값 컬렉션을 유지 합니다. 사용 하 여이 컬렉션에 액세스할 수는 [ `HttpContext` 클래스](https://msdn.microsoft.com/library/system.web.httpcontext.aspx) s [ `Application` 속성](https://msdn.microsoft.com/library/system.web.httpcontext.application.aspx), ASP.NET 페이지의 코드 숨김 클래스에서 사용 되 고 같이:


[!code-vb[Main](caching-data-at-application-startup-vb/samples/sample2.vb)]

데이터 캐시 시간 및 종속성 기반 expiries, 캐시 항목 우선 순위 등에 대 한 메커니즘을 제공 하는 데이터를 캐시 하는 훨씬 더 풍부한 API를 제공 합니다. 정적 멤버 및 응용 프로그램 상태와 같은 기능 페이지 개발자가 수동으로 추가 해야 합니다. 응용 프로그램의 수명에 대 한 응용 프로그램 시작 시 데이터를 캐시할 때 데이터 캐시의 장점 사항은 이론에 불과합니다. 이 자습서에서 살펴보게 정적 데이터를 캐시에 대 한 세 가지 기술 모두를 사용 하는 코드입니다.

## <a name="step-3-caching-thesupplierstable-data"></a>3 단계: 캐싱는`Suppliers`데이터 표

날짜를 구현 했습니다에서는 데이터베이스 테이블에서 Northwind 기존의 조회 테이블을 포함 하지 않습니다. 4 개의 Datatable는 static이 아닌 값을 포함 하는 모든 모델 테이블 우리의 DAL에서 구현 합니다. DAL 다음 새 클래스 및 메서드가 있는 bll에 새 DataTable을 추가 하는 데 시간을 소비 하는 대신이 자습서에서 s를 방금 사용에 대 한 가장 하 여 `Suppliers`의 테이블 데이터는 정적입니다. 따라서 응용 프로그램 시작 시이 데이터를 캐시할 수 있습니다.

를 시작 하려면 이라는 새 클래스를 만들 `StaticCache.cs` 에 `CL` 폴더입니다.


![CL 폴더에서 StaticCache.vb 클래스 만들기](caching-data-at-application-startup-vb/_static/image2.png)

**그림 2**: 만들기는 `StaticCache.vb` 클래스에 `CL` 폴더


이 캐시에서 데이터를 반환 하는 방법 뿐만 아니라 적절 한 캐시 스토어에 시작할 때 데이터를 로드 하는 메서드를 추가 해야 합니다.


[!code-vb[Main](caching-data-at-application-startup-vb/samples/sample3.vb)]

위의 코드는 정적 멤버 변수를 사용 하 여 `suppliers`의 결과를 저장 하는 `SuppliersBLL` s 클래스 `GetSuppliers()` 에서 호출 되는 메서드는 `LoadStaticCache()` 메서드. `LoadStaticCache()` 메서드는 응용 프로그램의 시작 되는 동안 호출 될 것입니다. 응용 프로그램 시작 시이 데이터를 로드, 공급 업체 데이터를 사용 하는 모든 페이지 호출할 수 있습니다는 `StaticCache` s 클래스 `GetSuppliers()` 메서드. 따라서 가져올 공급 업체 데이터베이스에 대 한 호출 에서만 발생 한 번, 응용 프로그램 시작 시.

대신 정적 멤버 변수는 캐시 저장소를 사용 또는 사용할 수도 응용 프로그램 상태 또는 데이터 캐시 합니다. 다음 코드 retooled 응용 프로그램 상태를 사용 하는 클래스를 보여 줍니다.


[!code-vb[Main](caching-data-at-application-startup-vb/samples/sample4.vb)]

`LoadStaticCache()`, 공급 업체 정보를 응용 프로그램 변수에 저장 됩니다 *키*합니다. 그 s 적절 한 형식으로 반환 (`Northwind.SuppliersDataTable`)에서 `GetSuppliers()`합니다. 응용 프로그램 상태를 사용 하 여 ASP.NET 페이지의 코드 숨김 클래스에서 액세스할 수 있습니다 하는 동안 `Application("key")`, 사용 해야 하는 아키텍처에서 `HttpContext.Current.Application("key")` 현재를 얻으려면 `HttpContext`합니다.

마찬가지로, 다음 코드와 같이 캐시 저장소로 데이터 캐시를 사용할 수 있습니다.


[!code-vb[Main](caching-data-at-application-startup-vb/samples/sample5.vb)]

시간 기반 만료 되지 않도록 데이터 캐시에 항목을 추가 하려면 사용 된 `System.Web.Caching.Cache.NoAbsoluteExpiration` 및 `System.Web.Caching.Cache.NoSlidingExpiration` 입력된 매개 변수로 값입니다. 이 특정 오버 로드의 데이터 캐시 s `Insert` 지정 수 있도록 선택한 메서드는 *우선 순위* 캐시 항목의 합니다. 우선 순위는 사용 가능한 메모리가 부족 하면 캐시에서 청소에 있는 항목을 지정 하는 데 사용 됩니다. 우선 순위 사용 여기 `NotRemovable`, 청소를 통해이 캐시 항목 t 승리 하 합니다.

> [!NOTE]
> 이 자습서의 다운로드를 구현 하는 `StaticCache` 클래스 정적 멤버 변수 접근 방식을 사용 합니다. 응용 프로그램 상태 및 데이터 캐시 기술에 대 한 코드를 클래스 파일의 주석에 있습니다.


## <a name="step-4-executing-code-at-application-startup"></a>4 단계: 응용 프로그램 시작 시 코드를 실행합니다.

를 웹 응용 프로그램을 처음 시작할 때 코드를 실행 하려면 라는 특수 파일을 만들어 해야 `Global.asax`합니다. 이 파일에 대 한 응용 프로그램, 세션-이벤트 처리기를 포함할 수 있습니다 및 요청 수준 이벤트 되며 여기 응용 프로그램이 시작 될 때마다 실행 되는 코드를 추가할 수 있습니다.

추가 `Global.asax` s Visual Studio 솔루션 탐색기에서에서 웹 사이트 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가 선택 하 여 웹 응용 프로그램의 루트 디렉터리에 파일입니다. 새 항목 추가 대화 상자에서 전역 응용 프로그램 클래스 항목 형식을 선택 하 고 추가 단추를 클릭 합니다.

> [!NOTE]
> 이미 있는 경우는 `Global.asax` 프로젝트, 항목 형식의 새 항목 추가 대화 상자에 표시 되지 것입니다 전역 응용 프로그램 클래스에에서는 파일입니다.


[![웹 응용 프로그램 s 루트 디렉터리에 Global.asax 파일 추가](caching-data-at-application-startup-vb/_static/image4.png)](caching-data-at-application-startup-vb/_static/image3.png)

**그림 3**: 추가 된 `Global.asax` 웹 응용 프로그램 s 루트 디렉터리에 파일 ([전체 크기 이미지를 보려면 클릭](caching-data-at-application-startup-vb/_static/image5.png))


기본 `Global.asax` 내 서버 쪽에서 5 개의 메서드를 포함 하는 파일 템플릿의 `<script>` 태그:

- **`Application_Start`** 웹 응용 프로그램을 처음 시작할 때 실행
- **`Application_End`** 응용 프로그램이 종료 될 때 실행
- **`Application_Error`** 처리 되지 않은 예외가 응용 프로그램에 도달할 때마다 실행
- **`Session_Start`** 새 세션을 만들 때 실행
- **`Session_End`** 세션이 만료 되었거나 중단 하면 실행 됩니다.

`Application_Start` s 응용 프로그램 수명 주기 동안 한 번만 이벤트 처리기가 호출 됩니다. 응용 프로그램을 처음으로 응용 프로그램에서 요청 하 고 응용 프로그램은 다시 시작할 때까지 계속 실행 하는 ASP.NET 리소스의 내용을 수정 하 여 발생할 수 있음 시작는 `/Bin` 폴더 수정 `Global.asax`수정 하 고는 콘텐츠는 `App_Code` 폴더 또는 수정는 `Web.config` 다른 원인 중 파일입니다. 참조 [ASP.NET 응용 프로그램 수명 주기 개요](https://msdn.microsoft.com/library/ms178473.aspx) 에 대 한 자세한 내용은 응용 프로그램 수명 주기 합니다.

이 자습서에 대 한만 하면 코드를 추가 하는 `Application_Start` 메서드, 따라서 자유롭게 다른 항목을 제거 합니다. `Application_Start`를 호출 하기만 하면는 `StaticCache` s 클래스 `LoadStaticCache()` 메서드를 로드 하 고 공급 업체 정보를 캐시:


[!code-aspx[Main](caching-data-at-application-startup-vb/samples/sample6.aspx)]

모두 완료 s가입니다! 응용 프로그램 시작 시의 `LoadStaticCache()` 메서드는 BLL에서 공급 업체 정보를 클릭 하 고 정적 멤버 변수로 저장 (또는에서 사용 하 여 결국 모든 캐시에 저장 하는 `StaticCache` 클래스). 이 문제를 확인 하려면에 중단점을 설정의 `Application_Start` 메서드 및 응용 프로그램을 실행 합니다. 응용 프로그램 시작 시이 중단점 note 합니다. 하지만 후속 요청 하지 않게 된 `Application_Start` 메서드를 실행 합니다.


[![Application_Start 이벤트 처리기가 실행 되 고 확인 하도록 중단점을 사용 하 여](caching-data-at-application-startup-vb/_static/image7.png)](caching-data-at-application-startup-vb/_static/image6.png)

**그림 4**: 확인에 중단점을 사용 하는 `Application_Start` 이벤트 처리기가 실행 되 고 ([전체 크기 이미지를 보려면 클릭](caching-data-at-application-startup-vb/_static/image8.png))


> [!NOTE]
> 발생 하지 않는 경우는 `Application_Start` 처음 시작 하면 디버깅 중단점에 있기 때문에 응용 프로그램이 이미 시작 되었습니다. 수정 하 여 다시 시작 하면 응용 프로그램 프로그램 `Global.asax` 또는 `Web.config` 파일 한 후 다시 시도 하십시오. 수 단순히 (더하거나 빼는) 빈 줄 끝에 신속 하 게 응용 프로그램 다시 시작 하려면 이러한 파일 중 하나입니다.


## <a name="step-5-displaying-the-cached-data"></a>5 단계: 캐시 된 데이터를 표시합니다.

이 시점에서 `StaticCache` 클래스를 통해 액세스할 수 있는 응용 프로그램 시작 시 캐시 된 공급자 데이터의 버전에 해당 `GetSuppliers()` 메서드. 프레젠테이션 계층에서이 데이터를 사용 하는 ObjectDataSource를 사용 하거나 프로그래밍 방식으로 호출할 수는 `StaticCache` s 클래스 `GetSuppliers()` ASP.NET 페이지의 코드 숨김 클래스의 메서드가 있습니다. S ObjectDataSource 및 GridView 컨트롤을 사용 하 여 캐시 된 공급 업체 정보를 표시 하려면 살펴볼 수 있도록 합니다.

열어 시작는 `AtApplicationStartup.aspx` 페이지에 `Caching` 폴더입니다. 설정 디자이너 도구 상자에서는 GridView 끌어 해당 `ID` 속성을 `Suppliers`합니다. 다음으로, GridView에서 스마트 태그 s 만들려고 선택한 라는 새 ObjectDataSource `SuppliersCachedDataSource`합니다. ObjectDataSource 사용 하도록 구성 된 `StaticCache` s 클래스 `GetSuppliers()` 메서드.


[![ObjectDataSource StaticCache 클래스를 사용 하도록 구성](caching-data-at-application-startup-vb/_static/image10.png)](caching-data-at-application-startup-vb/_static/image9.png)

**그림 5**: ObjectDataSource 사용 하도록 구성 된 `StaticCache` 클래스 ([전체 크기 이미지를 보려면 클릭](caching-data-at-application-startup-vb/_static/image11.png))


[![GetSuppliers() 메서드를 사용 하 여 캐시 된 공급자 데이터를 검색 합니다.](caching-data-at-application-startup-vb/_static/image13.png)](caching-data-at-application-startup-vb/_static/image12.png)

**그림 6**: 사용 된 `GetSuppliers()` 캐시 된 공급자 데이터를 검색 하는 메서드입니다 ([전체 크기 이미지를 보려면 클릭](caching-data-at-application-startup-vb/_static/image14.png))


마법사를 완료 한 후 Visual Studio는 자동으로 추가 BoundFields 각 데이터 필드에 대 한 `SuppliersDataTable`합니다. GridView 및 ObjectDataSource s 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](caching-data-at-application-startup-vb/samples/sample7.aspx)]

그림 7 브라우저를 통해 볼 때 페이지를 보여줍니다. 출력은 동일한 BLL s에서 데이터를 끌어온 म 했습니다 `SuppliersBLL` 클래스 하지만 사용 하는 `StaticCache` 클래스 응용 프로그램 시작 시 캐시 된 공급 업체 데이터를 반환 합니다. 중단점을 설정할 수는 `StaticCache` s 클래스 `GetSuppliers()` 메서드가이 동작을 확인 합니다.


[![캐시 된 공급자 데이터는 GridView에 표시 됩니다.](caching-data-at-application-startup-vb/_static/image16.png)](caching-data-at-application-startup-vb/_static/image15.png)

**그림 7**: 캐시 된 공급자 데이터는 GridView에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](caching-data-at-application-startup-vb/_static/image17.png))


## <a name="summary"></a>요약

대부분의 모든 데이터 모델에는 일반적으로 조회 테이블의 형태로 구현 하는 정적 데이터에 대 한 상당한 양의 포함 되어 있습니다. 이 정보는 정적 이므로 s 여기서가이 정보를 표시 해야 합니다. 계속 해 서 데이터베이스에 액세스할 때마다 이유가 없습니다. 또한 데이터를 캐시할 때 정적 상태, 인해 여기 s expiry 필요 하지 않습니다. 이 자습서에서는 이러한 데이터 응용 프로그램 상태 데이터 캐시에서 및 정적 멤버 변수를 통해이 캐시 하는 방법에 살펴보았습니다. 이 정보는 응용 프로그램 시작 시 캐시 하 고 응용 프로그램 s 수명 주기 동안 캐시에 유지 됩니다.

이 자습서 및 지난 2에서는 응용 프로그램의 수명 기간에 대 한 데이터를 캐시할 수 있을 뿐만 아니라 expiries 시간을 기준으로 사용 하 여에 검토 했습니다. 데이터베이스 데이터 캐싱, 하지만 시간 기반 만료 될 수 있습니다 적합 하지 않습니다. 주기적으로 캐시 플러시, 하는 대신 기본 데이터베이스 데이터 수정 될 때에 캐시 된 항목을 제거 하려면 최적의 것입니다. 이 이상적 모델이 다음 자습서에서 살펴봅니다 SQL 캐시 종속성을 사용 하 여 불가능 합니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Teresa 머피 및 Zack jones 이면 특정 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](caching-data-in-the-architecture-vb.md)
> [다음](using-sql-cache-dependencies-vb.md)
