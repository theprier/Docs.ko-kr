---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application
title: "ASP.NET 4 웹 응용 프로그램에서 Entity Framework 4.0 사용 하 여 동시성 처리 | Microsoft Docs"
author: tdykstra
description: "이 자습서 시리즈의 Entity Framework 4.0 자습서 시리즈 시작 하기에 의해 만들어진 Contoso 대학 웹 응용 프로그램 기반으로 합니다. I 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/26/2011
ms.topic: article
ms.assetid: a5aa22a6-fb7f-4f41-9c7f-addda151940b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application
msc.type: authoredcontent
ms.openlocfilehash: 7bdcf610458631749531ed1279d27e90572f0371
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="handling-concurrency-with-the-entity-framework-40-in-an-aspnet-4-web-application"></a>ASP.NET 4 웹 응용 프로그램에서 Entity Framework 4.0 사용 하 여 동시성 처리
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

> 에 의해 만들어진 Contoso 대학 웹 응용 프로그램을 기반으로 하는이 자습서 시리즈의 [Entity Framework 4.0이 있는 시작](https://asp.net/entity-framework/tutorials#Getting%20Started) 자습서 시리즈 합니다. 이전 자습서를 완료 하지 않은 경우이 자습서에 대 한 시작 점으로 하면 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) 만들어졌을 것입니다. 수도 있습니다 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) 완료 하는 자습서 시리즈에서 만들어진 합니다. 이 자습서에 대 한 질문이 있으면에 게시할 수 있습니다는 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx)합니다.


사용 하 여 데이터 필터링 및 정렬 하는 방법을 알아보았습니다 이전 자습서에서는 `ObjectDataSource` 제어 및 Entity Framework. 이 자습서에서는 Entity Framework를 사용 하 여 ASP.NET 웹 응용 프로그램의 동시성을 처리 하기 위한 옵션입니다. 강사 사무실 할당을 업데이트 하도록 지정 된 새 웹 페이지가 만들어집니다. 사용자는 해당 페이지와 이전에 만든 부서 페이지에서 동시성 문제를 처리 합니다.

[![Image06](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image2.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image1.png)

[![Image01](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image4.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image3.png)

## <a name="concurrency-conflicts"></a>동시성 충돌

한 명의 사용자가 레코드를 편집 하 고 첫 번째 사용자의 변경 내용을 데이터베이스에 기록 되기 전에 다른 사용자가 동일한 레코드를 편집 동시성 충돌이 발생 합니다. 이러한 충돌을 검색 하는 Entity Framework를 설정 하지 않으면, 다른 사용자의 변경 내용을 덮어씁니다 마지막 누구 든 지 데이터베이스를 업데이트 합니다. 많은 응용 프로그램에서 이러한 위험 허용 될 수 이며 가능한 동시성 충돌을 처리 하도록 응용 프로그램을 구성할 필요가 없습니다. (적은 수의 사용자, 또는 몇 가지 업데이트 하거나 동시성에 대 한 프로그래밍의 비용의 이점 보다 클 수 일부 변경 내용이 덮어쓰면 실제로 중요 하지 않은.) 동시성 충돌에 걱정할 필요가 없습니다;이 자습서를 건너뛸 수 있습니다. 나머지 두 자습서 시리즈의 안 함이 세계에 구성한 내용에 따라 다릅니다.

### <a name="pessimistic-concurrency-locking"></a>비관적 동시성 (잠금)

응용 프로그램에서 동시성 시나리오에서 실수로 인 한 데이터 손실을 방지할 필요가 경우 작업을 수행 하는 한 가지 방법은 데이터베이스 잠금을 사용 하는 합니다. 이 라고 *비관적 동시성*합니다. 예를 들어 데이터베이스에서 행을 읽기 전에 요청에 대 한 잠금을 읽기 전용 이거나 업데이트 액세스 합니다. 업데이트 권한이 대 한 행을 잠그는 다른 사용자가 허용 되는 경우 행에 대해 잠글 읽기 전용 또는 변경 중인 데이터의 복사본을 가져오기 때문에 대 한 액세스를 업데이트 합니다. 읽기 전용 액세스에 대 한 행을 잠그는 경우 다른 사용자도 잠글 수 있지만 업데이트에 대 한 읽기 전용 액세스 합니다.

잠금 관리에 몇 가지 단점이 있습니다. 프로그램으로 복잡할 수 있습니다. 중요 한 데이터베이스 관리 리소스 있어야 하며 응용 프로그램의 사용자의 수로 성능 문제가 생길 수 증가 (즉, 하기 쉽지 않습니다). 이러한 이유로 모든 데이터베이스 관리 시스템 비관적 동시성을 지원 합니다. Entity Framework,에 대 한 기본 제공 지원이 제공 하 고이 자습서에서는 구현 하는 방법을 표시 되지 않습니다.

### <a name="optimistic-concurrency"></a>낙관적 동시성

비관적 동시성을 대신 사용 하는 *낙관적 동시성*합니다. 낙관적 동시성 현상이 동시성 충돌을 허용 하 고 그럴 경우 적절 하 게 반응 의미 합니다. 예를 들어 John 실행는 *Department.aspx* 페이지를 클릭은 **편집** 시키고 기록 부서에 대 한 링크는 **예산** $ 1000, 000.00 달러에서 금액 125,000.00 합니다. (John을 관리 하는 경쟁 부서 자신의 부서에 대 한 비용을 확보 하려고 합니다.)

[![Image07](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image6.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image5.png)

John 클릭 하기 전에 **업데이트**, Jane 동일한 페이지를 실행, 클릭는 **편집** 기록 부서, 한 다음 변경 내용에 대 한 링크는 **시작 날짜** 필드 2011 년 1 월 10 일에서 1/1/를 1999 합니다. (Jane을 관리 하는 기록 부서 자세한 근무 연수가 제공 하려고 합니다.)

[![Image08](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image8.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image7.png)

John 클릭 **업데이트** Jane이 클릭 한 다음 먼저 **업데이트**합니다. Jane의 브라우저 지금은 목록은 **예산** $ 1000, 000.00, 하지만이 시간이 잘못 되었습니다. 크기를 $125,000.00 John에 의해 변경 되었습니다.

이 시나리오에서 수행할 수 있는 작업 중 일부는 다음과 같습니다.

- 한 사용자가 수정 되는 속성을 추적 하 고 데이터베이스의 해당 열만 업데이트할 수 있습니다. 예제 시나리오에서 데이터가 손실 될, 서로 다른 속성 두 사용자가 업데이트 되었기 때문에 합니다. 다음에 기록 부서 이동, 1/1/1999 표시 되는 경우 및 $125,000.00 합니다. 

    이 Entity Framework에서 기본 동작이 며 데이터가 손실 될 수 있는 충돌 수를 줄일 수 있는 합니다. 그러나이 문제는 동일한 엔터티의 속성 경쟁 변경 되 면 데이터 손실을 방지 하지 않습니다. 또한이 동작은 항상 할 수 없습니다. 저장된 프로시저는 엔터티 형식에 매핑할 때는 모든 엔터티에 변경 될 때 데이터베이스의 엔터티 속성의 모두 업데이트 됩니다.
- John의 내용으로 덮어쓰게 Jane의 변경 하도록 할 수 있습니다. Jane을 클릭 한 후 **업데이트**, **예산** 양 1000, 000.00 달러로 돌아갑니다. 이 라고는 *클라이언트 우선* 또는 *최신으로* 시나리오입니다. (클라이언트의 값 보다 우선 데이터 저장소에 포함 된 내용입니다.)
- 데이터베이스에서 업데이트 되 고에서 Jane의 변경을 방지할 수 있습니다. 일반적으로 오류 메시지가 표시, 그녀는 데이터의 현재 상태를 표시 하는 그녀 여전히 있도록가 그녀의 변경 내용을 다시 입력 하는 수입니다. 그녀의 입력을 저장 하 고 다시 입력 하지 않고도 적용할 수 있는 옵션을 보려면 아래 제공 하 여 추가 프로세스를 자동화할 수 있습니다. 이 라고는 *저장소 Wins* 시나리오입니다. (데이터 저장소 값 보다 우선 적용 클라이언트에서 전송한 값.)

### <a name="detecting-concurrency-conflicts"></a>동시성 충돌 확인

Entity Framework에서 처리 하 여 충돌을 해결할 수 있습니다 `OptimisticConcurrencyException` Entity Framework throw 하는 예외입니다. 이러한 예외를 throw 하는 시기를 확인 하기 위해 Entity Framework에서 충돌을 검색할 수 있어야 합니다. 따라서 구성 해야 데이터베이스와 데이터 모델 적절 하 게 합니다. 충돌 감지를 사용 하기 위한 몇 가지 옵션은 다음과 같습니다.

- 데이터베이스에 행이 변경 된 시기를 결정 하는 데 사용할 수 있는 테이블 열을 포함 합니다. Entity Framework의 해당 열을 포함 하도록 구성할 수 있습니다는 `Where` sql 절 `Update` 또는 `Delete` 명령입니다.

    용도 하는 `Timestamp` 열에는 `OfficeAssignment` 테이블입니다.

    [![Image09](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image10.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image9.png)

    데이터 형식이 고 `Timestamp` 열 라고도 `Timestamp`합니다. 그러나 열은 날짜 또는 시간 값을 포함 실제로 하지 않습니다. 대신, 값은 행이 업데이트 될 때마다가 증가 하는 일련 번호입니다. 에 `Update` 또는 `Delete` 명령에는 `Where` 절 포함 하는 원래 `Timestamp` 값입니다. 업데이트 되는 행의 값을 다른 사용자가 변경 된 경우 `Timestamp` 가 원래 값과 다른 하므로 `Where` 절 업데이트할 행을 반환 합니다. Entity Framework에서를 찾을 경우의 행이 없는 현재 업데이트 `Update` 또는 `Delete` 명령 (즉 때 영향을 받는 행 수는 0), 동시성 충돌 하는 해석 합니다.
- Entity Framework에서 테이블의 모든 열의 원래 값을 포함 하도록 구성 된 `Where` 절 `Update` 및 `Delete` 명령 합니다.

    첫 번째 옵션 행 주체를 읽어 먼저 이후에 변경 된 행에 아무 것도 경우와 같이 `Where` 절 반환 하지 않습니다는 행을 업데이트 하려면 Entity Framework를 동시성 충돌로 해석 합니다. 이 메서드는 효율적으로 사용 하는 `Timestamp` 필드 이지만 비효율적일 수 있습니다. 많은 열이 있는 데이터베이스 테이블에 대 한 만들어질 수 있습니다 매우 큰 `Where` 절, 많은 양의 상태를 유지 관리 하는 필요할 수는 웹 응용 프로그램 및입니다. 많은 양의 상태를 유지 관리 서버 리소스 (예를 들어 세션 상태)을 필요로 하거나 웹 페이지 (예: 보기 상태) 자체에 포함 해야 하기 때문에 응용 프로그램 성능이 떨어질 수 있습니다.

이 자습서에는 추적 속성 없는 엔터티에 대 한 낙관적 동시성 충돌에 대해 오류 처리를 추가 합니다 (의 `Department` 엔터티) 및 추적 속성이 있는 엔터티에 대해 (의 `OfficeAssignment` 엔터티)입니다.

## <a name="handling-optimistic-concurrency-without-a-tracking-property"></a>추적 속성 없이 낙관적 동시성 처리

에 대 한 낙관적 동시성을 구현 하는 `Department` 추적 없는 경우이 엔터티에 (`Timestamp`) 속성을 다음 작업을 수행 합니다.

- 동시성에 대 한 추적을 사용 하도록 설정 하려면 데이터 모델을 변경 `Department` 엔터티.
- 에 `SchoolRepository` 클래스에서 동시성 예외 처리는 `SaveChanges` 메서드.
- 에 *Departments.aspx* 페이지 올바르게 시도 된 변경 되었는지 경고 사용자에 게 메시지를 표시 하 여 동시성 예외를 처리 합니다. 사용자는 현재 값이 표시 다음 수 여전히 필요할 경우 변경 내용의 다시 시도 하십시오.

### <a name="enabling-concurrency-tracking-in-the-data-model"></a>데이터 모델에서 추적 되는 동시성을 사용 하도록 설정

Visual Studio에서이 시리즈의 이전 자습서에서 작업 하는 Contoso 대학 웹 응용 프로그램을 엽니다.

열기 *SchoolModel.edmx*, 데이터 모델 디자이너에서 마우스 오른쪽 단추로 클릭 하 고는 `Name` 속성에는 `Department` 엔터티와 클릭 **속성**합니다. 에 **속성** 창에서 변경 된 `ConcurrencyMode` 속성을 `Fixed`합니다.

[![Image16](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image12.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image11.png)

다른 기본 키 아닌 스칼라 속성에 대해 동일한 작업을 수행 (`Budget`, `StartDate`, 및 `Administrator`.) (그럴 수 없으면 탐색 속성에 대 한 합니다.) 이 지정 될 때마다 Entity Framework가 생성 하는 `Update` 또는 `Delete` 업데이트 하려면 SQL 명령은 `Department` 데이터베이스의 엔터티를 (원래 값)으로 이러한 열에 포함 되어야 합니다는 `Where` 절. 행이 없는 경우 발견 되는 `Update` 또는 `Delete` 명령이 실행, Entity Framework는 낙관적 동시성 예외를 throw 합니다.

저장 하 고 데이터 모델을 닫습니다.

### <a name="handling-concurrency-exceptions-in-the-dal"></a>DAL에서 동시성 예외 처리

열기 *SchoolRepository.cs* 다음 추가 `using` 문에 `System.Data` 네임 스페이스:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample1.cs)]

새 다음 추가 `SaveChanges` 낙관적 동시성 예외를 처리 합니다. 메서드:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample2.cs)]

동시성 오류가 발생 하는이 메서드가 호출 될 때 메모리에서 엔터티의 속성 값은 현재 데이터베이스에에서 대 한 값으로 바뀝니다. 웹 페이지에서 처리할 수 있도록 동시성 예외가 다시 throw 됩니다.

`DeleteDepartment` 및 `UpdateDepartment` 메서드는 기존 호출으로 대체 `context.SaveChanges()` 을 호출 하 여 `SaveChanges()` 새 메서드를 호출할 수 있습니다.

### <a name="handling-concurrency-exceptions-in-the-presentation-layer"></a>프레젠테이션 계층에서 동시성 예외 처리

열기 *Departments.aspx* 추가 `OnDeleted="DepartmentsObjectDataSource_Deleted"` 특성을 `DepartmentsObjectDataSource` 제어 합니다. 이제 컨트롤에 대 한 여는 태그 다음 예와 비슷하게 표시 됩니다.

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample3.aspx)]

에 `DepartmentsGridView` 제어, 모든 테이블 열에 지정는 `DataKeyNames` 다음 예제와 같이 특성입니다. 참고가에서 만듦 매우 큰 보기 상태 필드는 추적 필드를 사용 하는 이유는 일반적으로 동시성 충돌을 추적 하는 것이 좋습니다.

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample4.aspx)]

열기 *Departments.aspx.cs* 다음 추가 `using` 문에 `System.Data` 네임 스페이스:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample5.cs)]

데이터 소스 컨트롤에서 호출 하는 새 메서드를 추가 `Updated` 및 `Deleted` 동시성 예외 처리에 대 한 이벤트 처리기.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample6.cs)]

이 코드는 예외 형식이 확인 하 고 코드 동적으로 만듭니다 동시성 예외 이면는 `CustomValidator` 차례로의 메시지를 표시 하는 컨트롤의 `ValidationSummary` 제어 합니다.

새 메서드를 호출 하는 `Updated` 이전에 추가한 이벤트 처리기입니다. 또한 새를 만들 `Deleted` 같은 메서드를 호출 합니다 (그러나 다른 작업을 수행 하지) 하는 이벤트 처리기.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample7.cs)]

### <a name="testing-optimistic-concurrency-in-the-departments-page"></a>부서 페이지에서 낙관적 동시성을 테스트

실행 된 *Departments.aspx* 페이지.

[![Image17](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image14.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image13.png)

클릭 **편집** 행에 값을 변경 하 고는 **예산** 열입니다. (기억 하기 때문에이 자습서에서 만든 레코드만 편집할 수는 기존 `School` 데이터베이스 레코드에 잘못 된 데이터가 포함 되어 있습니다. 경제성 부서에 대 한 레코드는 시험해 안전 하나입니다.)

[![Image18](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image16.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image15.png)

새 브라우저 창을 열고 페이지 다시 (두 번째 브라우저 창으로 첫 번째 브라우저 창의 주소 상자에서 URL 복사 하는 경우)를 실행 합니다.

[![Image17](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image18.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image17.png)

클릭 **편집** 같은 이전 편집한 행 및 변경의 **예산** 를 다른 값입니다.

[![Image19](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image20.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image19.png)

두 번째 브라우저 창에서 클릭 **업데이트**합니다. **예산** 가 성공적으로 변경 된이 새 값으로.

[![Image20](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image22.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image21.png)

첫 번째 브라우저 창에서 클릭 **업데이트**합니다. 업데이트가 실패 합니다. **예산** 크기는 두 번째 브라우저 창에서 설정 된 값을 사용 하 여 다시 표시 하 고 오류 메시지가 나타납니다.

[![Image21](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image24.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image23.png)

## <a name="handling-optimistic-concurrency-using-a-tracking-property"></a>추적 속성을 사용 하 여 낙관적 동시성 처리

추적 속성을 가진 엔터티에 대 한 낙관적 동시성을 처리 하려면 다음 작업을 수행 합니다.

- 저장된 프로시저를 관리 하 고 데이터 모델에 추가 `OfficeAssignment` 엔터티. (추적 속성 및 저장된 프로시저를 함께 사용할 수 없는, 방금 상태별 함께 여기에 대 한 예시)
- DAL 및 BLL에 대 한 CRUD 메서드 추가 `OfficeAssignment` 엔터티, DAL의 낙관적 동시성 예외를 처리 하는 코드입니다.
- 사무실 할당 웹 페이지를 만듭니다.
- 새 웹 페이지에서 낙관적 동시성을 테스트 합니다.

### <a name="adding-officeassignment-stored-procedures-to-the-data-model"></a>OfficeAssignment 추가 저장 프로시저에는 데이터 모델

열기는 *SchoolModel.edmx* 파일에 모델 디자이너에서 디자인 화면을 마우스 오른쪽 단추로 클릭 하 고 클릭 **데이터베이스에서 모델 업데이트**합니다. 에 **추가** 탭은 **데이터베이스 개체 선택** 대화 상자에서 **Stored Procedures** 3 개를 선택 하 고 `OfficeAssignment` 저장 프로시저 (참조는 스크린 샷 뒤)를 클릭 하 고 **마침**합니다. (이러한 저장된 프로시저에에서 이미 있던 데이터베이스 다운로드 하거나 스크립트를 사용 하 여 만든.)

[![Image02](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image26.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image25.png)

마우스 오른쪽 단추로 클릭는 `OfficeAssignment` 엔터티와 선택 **저장 프로시저 매핑**합니다.

[![Image03](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image28.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image27.png)

설정의 **삽입**, **업데이트**, 및 **삭제** 의 해당 사용할 함수를 저장 프로시저입니다. 에 대 한는 `OrigTimestamp` 의 매개 변수는 `Update` 함수를 설정는 **속성** 를 `Timestamp` 선택 하 고는 **원래 값을 사용 하 여** 옵션입니다.

[![Image04](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image30.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image29.png)

Entity Framework 호출 하는 경우는 `UpdateOfficeAssignment` 저장된 프로시저의 원래 값을 전달 합니다는 `Timestamp` 열에는 `OrigTimestamp` 매개 변수입니다. 저장된 프로시저에서이 매개 변수를 사용 하 여 해당 `Where` 절:

[!code-sql[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample8.sql)]

저장된 프로시저의 새 값을 선택 된 `Timestamp` 업데이트 후 열 Entity Framework를 유지할 수 있도록는 `OfficeAssignment` 엔터티는 메모리에 해당 하는 데이터베이스 행과 동기화 합니다.

(참고 사무실 할당을 삭제 하기 위한 저장된 프로시저에 있지 않은 한 `OrigTimestamp` 매개 변수입니다. 따라서 Entity Framework 확인할 수 없습니다 삭제 하기 전에 엔터티는 변경 되지 않습니다.)

저장 하 고 데이터 모델을 닫습니다.

### <a name="adding-officeassignment-methods-to-the-dal"></a>DAL에 OfficeAssignment 메서드 추가

열기 *ISchoolRepository.cs* 다음 CRUD 방법에 대 한 추가 `OfficeAssignment` 엔터티 집합:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample9.cs)]

다음 새 메서드를 추가 *SchoolRepository.cs*합니다. 에 `UpdateOfficeAssignment` 로컬 호출 메서드를 `SaveChanges` 메서드 대신 `context.SaveChanges`합니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample10.cs)]

테스트 프로젝트를 열고 *MockSchoolRepository.cs* 다음 추가 `OfficeAssignment` 컬렉션과를 CRUD 메서드. 모의 리포지토리 리포지토리 인터페이스를 구현 해야 합니다 또는 솔루션 컴파일되지 않습니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample11.cs)]

### <a name="adding-officeassignment-methods-to-the-bll"></a>BLL에 OfficeAssignment 메서드 추가

주 프로젝트를 열고 *SchoolBL.cs* 다음 CRUD 방법에 대 한 추가 `OfficeAssignment` 엔터티 설정:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample12.cs)]

## <a name="creating-an-officeassignments-web-page"></a>OfficeAssignments 웹 페이지 만들기

사용 하는 새 웹 페이지를 만들고는 *Site.Master* 마스터 페이지 하 고 이름을 *OfficeAssignments.aspx*합니다. 다음 태그를 추가 `Content` 라는 컨트롤 `Content2`:

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample13.aspx)]

에 `DataKeyNames` 특성을 태그 지정의 `Timestamp` 속성 뿐만 아니라 레코드 키 (`InstructorID`). 속성을 지정 하는 `DataKeyNames` 특성 제어 되는 상태 (상태를 보려면 유사)에 저장 하도록 컨트롤을 사용 하면 처리를 다시 게시 하는 동안 원래 값을 사용할 수 있도록 합니다.

저장 하지 않은 경우는 `Timestamp` 값, Entity Framework 필요는 없습니다 것에 대 한는 `Where` sql 절 `Update` 명령입니다. 따라서 아무 것 업데이트할를 찾을 수 있습니다. Entity Framework는 때마다 낙관적 동시성 예외를 throw 하는 결과적으로, 한 `OfficeAssignment` 엔터티 업데이트 됩니다.

열기 *OfficeAssignments.aspx.cs* 다음 추가 `using` 데이터 액세스 계층에 대 한 문:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample14.cs)]

다음 추가 `Page_Init` 메서드 Dynamic Data 기능을 활성화 합니다. 에 대 한 다음 처리기를 추가할 수도 `ObjectDataSource` 컨트롤의 `Updated` 동시성 오류를 확인 하기 위해 이벤트:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample15.cs)]

### <a name="testing-optimistic-concurrency-in-the-officeassignments-page"></a>낙관적 동시성 OfficeAssignments 페이지에서 테스트

실행 된 *OfficeAssignments.aspx* 페이지.

[![Image10](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image32.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image31.png)

클릭 **편집** 행에 값을 변경 하 고는 **위치** 열입니다.

[![Image11](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image34.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image33.png)

새 브라우저 창을 열고 페이지 다시 (두 번째 브라우저 창에는 첫 번째 브라우저 창에서 URL 복사 하는 경우)를 실행 합니다.

[![Image10](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image36.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image35.png)

클릭 **편집** 같은 이전 편집한 행 및 변경의 **위치** 를 다른 값입니다.

[![Image12](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image38.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image37.png)

두 번째 브라우저 창에서 클릭 **업데이트**합니다.

[![Image13](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image40.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image39.png)

첫 번째 브라우저 창으로 전환 하 고 클릭 **업데이트**합니다.

[![Image15](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image42.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image41.png)

오류 메시지가 표시 및 **위치** 값이 두 번째 브라우저 창에서 변경 하는 값만 표시 하도록 업데이트 되었습니다.

## <a name="handling-concurrency-with-the-entitydatasource-control"></a>EntityDataSource 컨트롤을 사용 하 여 동시성 처리

`EntityDataSource` 핸들 업데이트 및 삭제 작업을 적절 하 게 및 컨트롤에 데이터 모델에서 동시성 설정을 인식 하는 기본 제공 논리가 포함 됩니다. 그러나 모든 예외와 마찬가지로 처리 해야 `OptimisticConcurrencyException` 예외 친숙 한 오류 메시지를 제공 하기 위해 자신입니다.

다음으로 구성 됩니다는 *Courses.aspx* 페이지 (사용 하는 `EntityDataSource` 컨트롤) 업데이트를 허용 하 고 작업을 삭제 하 고 동시성 충돌이 발생 한 경우 오류 메시지를 표시할 수 있습니다. `Course` 수행한 것과 동일한 방법을 사용 합니다, 열을 추적 하는 동시성 없는 경우 엔터티는 `Department` 엔터티: 모든 키가 아닌 속성의 값을 추적 합니다.

열기는 *SchoolModel.edmx* 파일입니다. 키가 아닌 속성에 대 한는 `Course` 엔터티 (`Title`, `Credits`, 및 `DepartmentID`)로 설정 된 **동시성 모드** 속성을 `Fixed`합니다. 그런 다음 저장 하 고 데이터 모델을 닫습니다.

열기는 *Courses.aspx* 페이지 하 고 다음과 같이 변경 합니다.

- 에 `CoursesEntityDataSource` 컨트롤을 추가 `EnableUpdate="true"` 및 `EnableDelete="true"` 특성입니다. 해당 컨트롤에 대 한 여는 태그에는 이제 다음 예제를 비슷합니다.

    [!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample16.aspx)]
- 에 `CoursesGridView` 제어 하 고, 변경 된 `DataKeyNames` 특성 값을 `"CourseID,Title,Credits,DepartmentID"`합니다. 그런 다음 추가 `CommandField` 요소는 `Columns` 요소를 보여 주는 **편집** 및 **삭제** 단추 (`<asp:CommandField ShowEditButton="True" ShowDeleteButton="True" />`). `GridView` 컨트롤에는 이제 다음 예제와 유사 합니다.

    [!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample17.aspx)]

페이지를 실행 하 고 부서 페이지에 이전과 동일한 방법으로 충돌 상황을 만듭니다. 두 개의 브라우저 창에서 페이지를 실행, 클릭 **편집** 같은으로 각 창 고 각각에서 서로 다른 변경 합니다. 클릭 **업데이트** 클릭 한 다음 하나의 창에 **업데이트** 다른 창에 있습니다. 클릭할 때 **업데이트** 를 두 번 처리 되지 않은 동시성 예외가 결과인 오류 페이지가 표시 됩니다.

[![Image22](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image44.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image43.png)

에 대 한 처리 방식과 매우 유사한 방식으로이 오류를 처리 하는 `ObjectDataSource` 제어 합니다. 열기는 *Courses.aspx* 페이지 및는 `CoursesEntityDataSource` 컨트롤에 대 한 처리기를 지정는 `Deleted` 및 `Updated` 이벤트입니다. 컨트롤의 여는 태그에는 이제 다음 예제를 비슷합니다.

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample18.aspx)]

전에 `CoursesGridView` 컨트롤을 다음 추가 `ValidationSummary` 제어:

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample19.aspx)]

*Courses.aspx.cs*, 추가 `using` 문에 `System.Data` 동시성 예외에 대 한 확인 하는 메서드를 추가 하 고에 대 한 처리기를 추가 하는 네임 스페이스를는 `EntityDataSource` 컨트롤의 `Updated` 및 `Deleted`처리기입니다. 코드는 다음과 같이 표시 됩니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample20.cs)]

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample21.cs)]

이 코드와 수행한 작업에 대 한 간의 유일한 차이점은 `ObjectDataSource` 컨트롤은이 경우에 동시성 예외는 `Exception` 하지 않고 해당 예외는 이벤트 인수 개체의 속성 `InnerException` 속성입니다.

페이지를 실행 하 고 동시성 충돌을 다시 만듭니다. 이 시간 오류 메시지가 표시:

[![Image23](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image46.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image45.png)

동시성 충돌 처리 소개를 완료 합니다. 다음 자습서는 Entity Framework를 사용 하는 웹 응용 프로그램의 성능을 향상 하는 방법에 지침을 제공 합니다.

>[!div class="step-by-step"]
[이전](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)
[다음](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)
