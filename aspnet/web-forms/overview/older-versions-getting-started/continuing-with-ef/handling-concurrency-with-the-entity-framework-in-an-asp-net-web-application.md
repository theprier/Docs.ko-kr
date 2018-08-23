---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application
title: ASP.NET 4 웹 응용 프로그램에서 Entity Framework 4.0으로 동시성 처리 | Microsoft Docs
author: tdykstra
description: 이 자습서 시리즈의 Entity Framework 4.0 자습서 시리즈를 사용 하 여 시작 하 여 만든 Contoso University 웹 응용 프로그램 기반으로 합니다. 필자는 중...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: a5aa22a6-fb7f-4f41-9c7f-addda151940b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application
msc.type: authoredcontent
ms.openlocfilehash: 6b10aca944a322cae252666218aee4d5a2d6ed35
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41835461"
---
<a name="handling-concurrency-with-the-entity-framework-40-in-an-aspnet-4-web-application"></a>ASP.NET 4 웹 응용 프로그램에서 Entity Framework 4.0으로 동시성 처리
====================
[Tom Dykstra](https://github.com/tdykstra)

> 이 자습서 시리즈에서 만든 Contoso University 웹 응용 프로그램 빌드를 [Entity Framework 4.0을 사용 하 여 시작](https://asp.net/entity-framework/tutorials#Getting%20Started) 자습서 시리즈입니다. 이전 자습서를 완료 하지 않은 경우이 자습서에 대 한 시작 지점으로 할 수 있습니다 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) 만들어졌을 것입니다. 할 수도 있습니다 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) 전체 자습서 시리즈에서 만들어집니다. 이 자습서에 대 한 질문이 있으면 하기를 게시할 수 있습니다 합니다 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx)합니다.


이전 자습서에서 알아보았습니다 정렬 하는 방법을 사용 하 여 필터 데이터는 `ObjectDataSource` 컨트롤 및 Entity Framework. 이 자습서에서는 Entity Framework를 사용 하는 ASP.NET 웹 응용 프로그램에서 동시성 처리에 대 한 옵션을 보여 줍니다. 강사 사무실 할당을 업데이트 하도록 지정 된 새 웹 페이지를 만들게 됩니다. 해당 페이지에 이전에 만든 부서 페이지에서 동시성 문제를 처리할 수 있습니다.

[![Image06](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image2.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image1.png)

[![Image01](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image4.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image3.png)

## <a name="concurrency-conflicts"></a>동시성 충돌

동시성 충돌을 한 명의 사용자가 레코드를 편집 하 고 첫 번째 사용자의 변경 내용을 데이터베이스에 기록 되기 전에 다른 사용자가 동일한 레코드를 편집 하는 경우 발생 합니다. 이러한 충돌을 검색 하는 Entity Framework를 설정 하지 않으면, 마지막으로 다른 사용자의 변경 내용을 덮어씁니다 누구 든 지 데이터베이스를 업데이트 합니다. 많은 응용 프로그램에서이 위험은 허용 하 고 가능한 동시성 충돌을 처리 하도록 응용 프로그램을 구성할 필요가 없습니다. (경우 또는 몇 명의 사용자 또는 적은 업데이트가 있을 경우 동시성에 대 한 프로그래밍의 비용은 이점 보다 클 수 일부 변경 내용이 덮어쓰여지는 경우 실제로 중요 하지 않습니다.) 동시성 충돌에 걱정할 필요가 없습니다, 하는 경우이 자습서를 건너뛸 수 있습니다. 나머지 두 자습서 시리즈의이 구성 파일에서 구성한 내용에 의존 하지.

### <a name="pessimistic-concurrency-locking"></a>비관적 동시성 (잠금)

응용 프로그램에서 동시성 시나리오에서 실수로 인한 데이터 손실을 방지할 필요가 있는 경우 해당 작업을 수행하는 한 가지 방법은 데이터베이스 잠금을 사용하는 것입니다. 이 이라고 *비관적 동시성*합니다. 예를 들어 데이터베이스에서 행을 읽기 전에 읽기 전용 또는 업데이트 액세스에 대한 잠금을 요청합니다. 업데이트 액세스에 대한 행을 잠그는 경우 변경 중인 데이터의 복사본을 가져오기 때문에 다른 사용자는 읽기 전용 또는 업데이트 액세스에 대한 행을 잠그도록 허용되지 않습니다. 읽기 전용 액세스에 대한 행을 잠그는 경우 다른 사용자도 읽기 전용에 대해 잠글 수 있지만 업데이트에 대해서는 잠글 수 없습니다.

잠금 관리에 몇 가지 단점이 있습니다. 프로그램을 설정하는 데 복잡할 수 있습니다. 상당한 데이터베이스 관리 리소스가 필요 하며 응용 프로그램의 사용자 수가 성능 문제가 발생할 수 있습니다 높아집니다 (즉, 확장 되지 않습니다도). 이러한 이유로 모든 데이터베이스 관리 시스템은 비관적 동시성을 지원하지 않습니다. 이 자습서를 구현 하는 방법을 표시 되지 않습니다 및 Entity Framework를 기본 제공 지원이 제공 합니다.

### <a name="optimistic-concurrency"></a>낙관적 동시성

비관적 동시성 대신 *낙관적 동시성*합니다. 낙관적 동시성은 동시성 충돌 발생을 허용한 다음, 그럴 경우 적절하게 반응하는 것을 의미합니다. 실행 예를 들어, 합니다 *Department.aspx* 페이지를 클릭 합니다 **편집** 줄이고 기록 부서에 대 한 링크를 **예산** $ $ 1000, 000.00에서 금액 125,000.00 합니다. (John 경쟁 부서를 관리 하는 방법과 및 자신의 부서에 대 한 비용을 확보 하려고 합니다.)

[![Image07](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image6.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image5.png)

John 클릭 하기 전에 **업데이트**, jane은 동일한 페이지를 실행를 클릭 합니다 **편집** 기록 부서 및 다음 변경 내용에 대 한 링크를 **시작 날짜** 2011 년 1 월 10에서에서 필드를 1/1 / 1999입니다. (Jane에 게 기록 부서를 관리 하는 방법과 및 자세한 근무 연수가 지정 하려고 합니다.)

[![Image08](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image8.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image7.png)

John 클릭 **업데이트** 먼저 jane은 클릭 **업데이트**합니다. Jane의 브라우저 이제 목록 합니다 **예산** $125,000.00에 John 하 여 크기 변경 되어 크기 1000 달러, 000.00, 하지만이 올바르지 않습니다.

이 시나리오에서 수행할 수 있는 작업 중 일부는 다음과 같습니다.

- 사용자가 수정한 속성의 추적을 유지하고 데이터베이스에서 해당하는 열만 업데이트할 수 있습니다. 예제 시나리오에서 서로 다른 속성이 두 사용자에 의해 업데이트되었기 때문에 데이터가 손실되지 않습니다. 다음에 누군가가 기록 부서, 1/1/1999 표시 및 $125,000.00 합니다. 

    Entity Framework의 기본 동작이 며 데이터가 손실 될 수 있는 충돌 횟수를 줄일 수 있는 합니다. 그러나이 동작은 엔터티의 동일한 속성에 변경 내용이 있는 경우 데이터 손실을 방지 하지 않습니다. 또한이 동작은 항상 가능한 것은; 저장된 프로시저에 엔터티 형식에 매핑할 때는 모든 엔터티에 변경 될 때 데이터베이스에서 엔터티의 속성 모두 업데이트 됩니다.
- Jane의 변경 사항으로 John의 변경 내용이 덮어쓸 수 있습니다. Jane은 클릭 한 후 **업데이트**의 **예산** 크기 1000 달러, 000.00로 돌아갑니다. 이를 *클라이언트 우선* 또는 *최종 우선* 시나리오라고 합니다. (클라이언트의 값이 우선 데이터 저장소의 새로운 기능 위에 있습니다.)
- 데이터베이스에서 업데이트 되지 Jane의 변경을 방지할 수 있습니다. 일반적으로 오류 메시지를 표시, 그녀는 데이터의 현재 상태를 표시 하는 여전히 수 있도록 하려고 하는 경우 변경 내용을 다시 입력 하 게 합니다. 추가 입력을 저장 하 고 그녀 다시 입력 하지 않고 적용할 수 있는 옵션을 제공 하 여 프로세스를 자동화할 수 있습니다. 이를 *저장소 우선* 시나리오라고 합니다. (데이터 저장소 값은 클라이언트가 전송한 값에 우선합니다.)

### <a name="detecting-concurrency-conflicts"></a>동시성 충돌 감지

Entity Framework에서 처리 하 여 충돌을 해결할 수 있습니다 `OptimisticConcurrencyException` Entity Framework에서 throw 하는 예외입니다. 이러한 예외를 throw하는 시기를 확인하기 위해 Entity Framework에서 충돌을 검색할 수 있어야 합니다. 따라서 데이터베이스와 데이터 모델을 적절하게 구성해야 합니다. 충돌 검색을 활성화하기 위한 몇 가지 옵션은 다음과 같습니다.

- 데이터베이스에 행이 변경 된 시기를 결정 하는 테이블 열을 포함 합니다. Entity Framework에서 해당 열을 포함 하도록 구성할 수 있습니다 합니다 `Where` SQL 절 `Update` 또는 `Delete` 명령입니다.

    용도 합니다 `Timestamp` 열에는 `OfficeAssignment` 테이블입니다.

    [![Image09](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image10.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image9.png)

    데이터 형식은 합니다 `Timestamp` 열이 라고도 `Timestamp`합니다. 그러나 열은 날짜 또는 시간 값을 포함 실제로 하지 않습니다. 대신 값은 행이 업데이트 될 때마다 증가는 일련 번호입니다. 에 `Update` 또는 `Delete` 명령인 합니다 `Where` 절에는 원래 포함 되어 `Timestamp` 값. 업데이트 되는 행의 값을 다른 사용자가 변경 된 경우 `Timestamp` 원래 값을 다른 하므로 `Where` 절 업데이트할 행을 반환 합니다. Entity Framework는 행이 없는 현재 업데이트 된 경우를 찾습니다 `Update` 또는 `Delete` (즉 때 영향을 받는 행 수가 0) 명령을 동시성 충돌로 해석 합니다.
- 테이블에 있는 모든 열의 원래 값을 포함 하도록 Entity Framework를 구성 합니다 `Where` 절 `Update` 및 `Delete` 명령입니다.

    행 처음 읽은 이후에 변경 된 행의 경우 첫 번째 옵션은 `Where` 절 반환 되지 않습니다는 행을 업데이트 하려면 Entity Framework는 동시성 충돌로 해석 합니다. 이 메서드는 효과적으로 작업을 사용 하는 `Timestamp` 필드에 있지만 비효율적일 수 있습니다. 데이터베이스 테이블의 여러 열이 있는 경우 발생할 수 있습니다 매우 큰 `Where` 절 및 많은 양의 상태를 유지 관리 하는 필요할 수 웹 응용 프로그램에서입니다. 많은 양의 상태를 유지 관리 서버 리소스 (예를 들어 세션 상태)를 필요로 하거나 웹 페이지 자체 (예를 들어, 보기 상태)에 포함 되어야 하기 때문에 응용 프로그램 성능이 저하 될 수 있습니다.

이 자습서에서는 추적 속성 없는 엔터티에 대 한 낙관적 동시성 충돌에 대해 오류 처리 추가 (합니다 `Department` 엔터티) 및 추적 속성 않은 엔터티에 대 한 (의 `OfficeAssignment` 엔터티).

## <a name="handling-optimistic-concurrency-without-a-tracking-property"></a>추적 속성을 사용 하지 않고 낙관적 동시성 처리

에 대 한 낙관적 동시성을 구현 합니다 `Department` 엔터티는 추적 하지 않습니다 (`Timestamp`) 속성을 다음 작업을 수행 합니다:

- 동시성에 대 한 추적을 사용 하도록 데이터 모델을 변경할 `Department` 엔터티.
- 에 `SchoolRepository` 클래스의 동시성 예외 처리는 `SaveChanges` 메서드.
- 에 *Departments.aspx* 페이지, 시도 된 변경 되지 않았습니다 경고 사용자에 게 메시지를 표시 하 여 동시성 예외를 처리 합니다. 그런 다음 사용자 현재 값을 참조 하 고 여전히 필요할 경우 변경 내용을 다시 시도 수 있습니다.

### <a name="enabling-concurrency-tracking-in-the-data-model"></a>동시성 데이터 모델에서 추적을 사용 하도록 설정

Visual Studio에서이 시리즈의 이전 자습서에서 사용 하 여 작업 하는 Contoso University 웹 응용 프로그램을 엽니다.

열기 *SchoolModel.edmx*, 데이터 모델 디자이너에서 마우스 오른쪽 단추로 클릭 하 고는 `Name` 속성에는 `Department` 엔터티와 클릭 **속성**합니다. 에 **속성** 창에서 변경 합니다 `ConcurrencyMode` 속성을 `Fixed`입니다.

[![Image16](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image12.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image11.png)

다른 기본 키가 아닌 스칼라 속성에 대해 동일한 작업을 수행 (`Budget`하십시오 `StartDate`, 및 `Administrator`.) (할 수 없는 탐색 속성에 대 한 합니다.) 이 때마다 Entity Framework 생성 하도록 지정는 `Update` 또는 `Delete` 업데이트 하려면 SQL 명령 합니다 `Department` 데이터베이스의 엔터티, 이러한 열 (원래 값)에 포함 되어야 합니다는 `Where` 절. 행이 없는 경우 발견 되는 `Update` 또는 `Delete` 명령 실행, Entity Framework에는 낙관적 동시성 예외가 throw 됩니다.

저장 하 고 데이터 모델을 닫습니다.

### <a name="handling-concurrency-exceptions-in-the-dal"></a>DAL의 동시성 예외 처리

열기 *SchoolRepository.cs* 다음을 추가 합니다 `using` 문을 여 `System.Data` 네임 스페이스:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample1.cs)]

다음의 새로운 추가 `SaveChanges` 낙관적 동시성 예외를 처리 하는 메서드:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample2.cs)]

동시성 오류가 발생 하는이 메서드가 호출 될 때 메모리에서 엔터티의 속성 값을 데이터베이스의 현재 값으로 바뀝니다. 웹 페이지에서 처리할 수 있도록 동시성 예외 다시 throw 됩니다.

에 `DeleteDepartment` 및 `UpdateDepartment` 메서드를 기존 호출을 바꿉니다 `context.SaveChanges()` 호출 하 여 `SaveChanges()` 새 메서드를 호출 하기 위해.

### <a name="handling-concurrency-exceptions-in-the-presentation-layer"></a>프레젠테이션 계층에서 동시성 예외 처리

오픈 *Departments.aspx* 추가 `OnDeleted="DepartmentsObjectDataSource_Deleted"` 특성을 `DepartmentsObjectDataSource` 제어 합니다. 컨트롤의 여는 태그는 이제 다음 예와 유사 합니다.

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample3.aspx)]

에 `DepartmentsGridView` 제어, 모든 테이블 열에 지정 합니다 `DataKeyNames` 특성을 다음 예와에서 같이 합니다. 이 만들 매우 큰 보기 상태 필드를 한 가지 이유는 추적 필드를 사용 하는 이유는 일반적으로 동시성 충돌을 추적 하는 것이 좋습니다.

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample4.aspx)]

열기 *Departments.aspx.cs* 다음을 추가 합니다 `using` 문을 여 `System.Data` 네임 스페이스:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample5.cs)]

데이터 소스 컨트롤에서 호출 되는 새 메서드를 추가 `Updated` 고 `Deleted` 동시성 예외 처리에 대 한 이벤트 처리기:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample6.cs)]

이 코드 예외 형식을 확인 하 고 코드를 동적으로 만듭니다 동시성 예외 인 경우는 `CustomValidator` 에 메시지를 표시 하는 컨트롤을 `ValidationSummary` 컨트롤입니다.

새 메서드를 호출 합니다 `Updated` 이전에 추가한 이벤트 처리기입니다. 또한 새를 만들 `Deleted` 같은 메서드를 호출 합니다 (하지만 다른 작업을 수행 하지 않습니다)는 이벤트 처리기:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample7.cs)]

### <a name="testing-optimistic-concurrency-in-the-departments-page"></a>낙관적 동시성 부서 페이지에서 테스트

실행 합니다 *Departments.aspx* 페이지입니다.

[![Image17](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image14.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image13.png)

클릭 **편집** 행에 값을 변경 합니다 **예산** 열. (때문에이 자습서에서 만든 레코드만 편집할 수 기억 기존 `School` 일부 잘못 된 데이터를 포함 하는 데이터베이스 레코드입니다. 경제성 부서에 대 한 레코드를 사용 하 여 실험을 안전 하 게 단일.)

[![Image18](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image16.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image15.png)

새 브라우저 창을 열고 페이지 다시 (두 번째 브라우저 창으로 첫 번째 브라우저 창의 주소 상자에서 URL 복사 하는 경우)를 실행 합니다.

[![Image17](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image18.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image17.png)

클릭 **편집** 과 같은 이전 편집한 행 및 변경 합니다 **예산** 를 다른 값입니다.

[![Image19](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image20.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image19.png)

두 번째 브라우저 창에서 클릭 **업데이트**합니다. 합니다 **예산** 크기는이 새 값으로 변경 했습니다.

[![Image20](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image22.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image21.png)

첫 번째 브라우저 창에서 클릭 **업데이트**합니다. 업데이트가 실패 합니다. 합니다 **예산** 크기는 두 번째 브라우저 창에서 설정 된 값을 사용 하 여 다시 표시 하 고 오류 메시지가 표시 됩니다.

[![Image21](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image24.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image23.png)

## <a name="handling-optimistic-concurrency-using-a-tracking-property"></a>추적 속성을 사용 하 여 낙관적 동시성 처리

추적 속성을 가진 엔터티에 대 한 낙관적 동시성을 처리 하려면 다음 작업을 완료 합니다.

- 저장된 프로시저를 관리 하는 데이터 모델에 추가 `OfficeAssignment` 엔터티. (추적 속성 및 저장된 프로시저를 함께 사용할 필요가 없습니다; 해당 하는 방금 그룹화 여기에 대 한 예시입니다.)
- 에 대 한 BLL 및 DAL CRUD 메서드 추가 `OfficeAssignment` 엔터티를 DAL에서 낙관적 동시성 예외를 처리 하는 코드를 포함 합니다.
- 사무실 할당 웹 페이지를 만듭니다.
- 새 웹 페이지에서 낙관적 동시성을 테스트 합니다.

### <a name="adding-officeassignment-stored-procedures-to-the-data-model"></a>OfficeAssignment 추가 저장 프로시저를 데이터 모델

엽니다는 *SchoolModel.edmx* 모델 디자이너에서 파일, 디자인 화면을 마우스 오른쪽 단추로 클릭 하 고 클릭 **데이터베이스에서 모델 업데이트**합니다. 에 **추가** 탭을 **데이터베이스 개체 선택** 대화 상자에서 **저장 프로시저** 세 가지를 선택 하 고 `OfficeAssignment` 저장 프로시저 (참조는 다음 스크린샷에서)를 클릭 하 고 **완료**합니다. (이러한 저장된 프로시저가 이미 데이터베이스에 다운로드 하거나 스크립트를 사용 하 여 만든 경우.)

[![Image02](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image26.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image25.png)

마우스 오른쪽 단추로 클릭 합니다 `OfficeAssignment` 엔터티 및 선택 **저장 프로시저 매핑**합니다.

[![Image03](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image28.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image27.png)

설정 된 **삽입**를 **업데이트**, 및 **삭제** 함수를 사용 하 여 해당 저장 프로시저입니다. 에 대 한는 `OrigTimestamp` 의 매개 변수를 `Update` 함수를 설정 합니다 **속성** 를 `Timestamp` 선택한를 **Original Value 사용** 옵션.

[![Image04](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image30.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image29.png)

엔터티 프레임 워크에서 호출 하는 경우는 `UpdateOfficeAssignment` 저장된 프로시저의 원래 값을 전달 합니다 합니다 `Timestamp` 열에는 `OrigTimestamp` 매개 변수입니다. 저장된 프로시저에서이 매개 변수를 사용 하 여 해당 `Where` 절:

[!code-sql[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample8.sql)]

저장된 프로시저의 새 값을 선택 합니다 `Timestamp` 업데이트 후 열 Entity Framework를 유지할 수 있도록는 `OfficeAssignment` 엔터티는 메모리에 해당 하는 데이터베이스 행과 동기화 합니다.

(사무실 할당을 삭제 하기 위한 저장된 프로시저 없는 참고는 `OrigTimestamp` 매개 변수입니다. 따라서 Entity Framework 확인할 수 없습니다 삭제 하기 전에 엔터티는 변경 되지 않습니다.)

저장 하 고 데이터 모델을 닫습니다.

### <a name="adding-officeassignment-methods-to-the-dal"></a>DAL에 OfficeAssignment 메서드 추가

오픈 *ISchoolRepository.cs* 에 대 한 다음 CRUD 메서드를 추가 하 고는 `OfficeAssignment` 엔터티 집합:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample9.cs)]

다음 새 메서드를 추가 *SchoolRepository.cs*합니다. 에 `UpdateOfficeAssignment` 를 호출 하는 메서드는 로컬 `SaveChanges` 메서드 대신 `context.SaveChanges`합니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample10.cs)]

테스트 프로젝트를 엽니다 *MockSchoolRepository.cs* 추가한 다음 `OfficeAssignment` 를 CRUD 메서드와 컬렉션입니다. (모의 리포지토리의 리포지토리 인터페이스를 구현 해야 합니다 또는 솔루션을 컴파일되지 않습니다.)

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample11.cs)]

### <a name="adding-officeassignment-methods-to-the-bll"></a>BLL에 OfficeAssignment 메서드 추가

주 프로젝트를 엽니다 *SchoolBL.cs* 에 대 한 다음 CRUD 메서드를 추가 하 고는 `OfficeAssignment` 엔터티 집합:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample12.cs)]

## <a name="creating-an-officeassignments-web-page"></a>프로그램 OfficeAssignments 웹 페이지 만들기

사용 하는 새 웹 페이지 만들기를 *Site.Master* 페이지를 마스터 하 고 이름을 *OfficeAssignments.aspx*합니다. 다음 태그를 추가 합니다 `Content` 제어 라는 `Content2`:

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample13.aspx)]

되었는지 확인 합니다 `DataKeyNames` 특성을 태그 지정 합니다 `Timestamp` 레코드 키 뿐만 아니라 속성 (`InstructorID`). 속성을 지정 하는 `DataKeyNames` 특성 제어 되는 상태 (뷰 상태와 유사한)에 저장할 컨트롤이 포스트백 처리 하는 동안 원래 값을 사용할 수 있도록 합니다.

저장 하지 않은 경우는 `Timestamp` 값, Entity Framework 없을 수에 `Where` SQL 절 `Update` 명령입니다. 결과적으로 업데이트를 찾을 수는 아무 작업도 수행 합니다. Entity Framework은 때마다 낙관적 동시성 예외를 throw 하는 결과적으로 `OfficeAssignment` 엔터티 업데이트 됩니다.

오픈 *OfficeAssignments.aspx.cs* 추가한 다음 `using` 데이터 액세스 계층에 대 한 문:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample14.cs)]

다음 추가 `Page_Init` 메서드를 Dynamic Data 기능을 사용 하도록 설정 합니다. 또한 다음 처리기를 추가 합니다 `ObjectDataSource` 컨트롤의 `Updated` 동시성 오류를 확인 하기 위해 이벤트:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample15.cs)]

### <a name="testing-optimistic-concurrency-in-the-officeassignments-page"></a>낙관적 동시성 OfficeAssignments 페이지에서 테스트

실행 합니다 *OfficeAssignments.aspx* 페이지입니다.

[![Image10](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image32.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image31.png)

클릭 **편집** 행에 값을 변경 합니다 **위치** 열.

[![Image11](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image34.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image33.png)

새 브라우저 창을 열고 페이지 다시 (두 번째 브라우저 창에는 첫 번째 브라우저 창에서 URL 복사 하는 경우)를 실행 합니다.

[![Image10](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image36.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image35.png)

클릭 **편집** 과 같은 이전 편집한 행 및 변경 합니다 **위치** 를 다른 값입니다.

[![Image12](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image38.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image37.png)

두 번째 브라우저 창에서 클릭 **업데이트**합니다.

[![Image13](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image40.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image39.png)

첫 번째 브라우저 창으로 전환 하 고 클릭 **업데이트**합니다.

[![Image15](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image42.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image41.png)

오류 메시지를 표시 하며 **위치** 값에 두 번째 브라우저 창에서 변경한 값을 표시 하도록 업데이트 되었습니다.

## <a name="handling-concurrency-with-the-entitydatasource-control"></a>EntityDataSource 컨트롤을 사용 하 여 동시성 처리

`EntityDataSource` 데이터 모델의 동시성 설정을 인식 하는 기본 제공 논리를 포함 하는 컨트롤 및 핸들 업데이트 및 삭제 작업을 적절 하 게 합니다. 그러나 모든 예외와 마찬가지로 처리 해야 `OptimisticConcurrencyException` 예외 친숙 한 오류 메시지를 제공 하기 위해 직접.

구성한 다음에 *Courses.aspx* 페이지 (사용 하는 `EntityDataSource` 컨트롤) 동시성 충돌이 발생 하는 경우 오류 메시지를 표시 하 고 업데이트 및 삭제 작업입니다. 합니다 `Course` 엔터티는 추적 열을 사용 했던 동일한 방법을 사용 하는 동시성 없는 `Department` 엔터티: 모든 키가 아닌 속성의 값을 추적 합니다.

엽니다는 *SchoolModel.edmx* 파일입니다. 키가 아닌 속성에 대 한는 `Course` 엔터티 (`Title`, `Credits`, 및 `DepartmentID`)로 설정 합니다 **동시성 모드** 속성을 `Fixed`. 그런 다음 저장 하 고 데이터 모델을 닫습니다.

열기는 *Courses.aspx* 페이지 하 고 다음과 같이 변경 합니다.

- 에 `CoursesEntityDataSource` 컨트롤에 추가 합니다 `EnableUpdate="true"` 고 `EnableDelete="true"` 특성입니다. 해당 컨트롤의 여는 태그에는 이제 다음 예제와 유사합니다.

    [!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample16.aspx)]
- 에 `CoursesGridView` 컨트롤을 변경 합니다 `DataKeyNames` 특성 값을 `"CourseID,Title,Credits,DepartmentID"`입니다. 다음 추가 `CommandField` 요소를 `Columns` 요소를 보여 주는 **편집** 및 **삭제** 단추 (`<asp:CommandField ShowEditButton="True" ShowDeleteButton="True" />`). `GridView` 컨트롤에는 이제 다음 예제와 유사 합니다.

    [!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample17.aspx)]

페이지를 실행 하 고 부서 페이지에서 이전에 수행한 대로 충돌 상황을 만듭니다. 두 개의 브라우저 창에서 페이지를 실행, 클릭 **편집** 동일한 각 창의 줄에 각각에서 다른 변경 합니다. 클릭 **업데이트** 하나의 창에서 클릭 **업데이트** 다른 창에서. 클릭 하면 **업데이트** 를 두 번 처리 되지 않은 동시성 예외 결과로 생성 되는 오류 페이지가 표시 됩니다.

[![Image22](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image44.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image43.png)

에 대해 처리 하는 방식과 매우 유사한 방식으로이 오류를 처리 하는 `ObjectDataSource` 제어 합니다. 열기는 *Courses.aspx* 페이지에서 및를 `CoursesEntityDataSource` 컨트롤에 대 한 처리기를 지정 합니다 `Deleted` 및 `Updated` 이벤트. 컨트롤의 여는 태그에는 이제 다음 예제와 유사합니다.

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample18.aspx)]

전에 `CoursesGridView` 컨트롤에 다음을 추가 합니다 `ValidationSummary` 제어 합니다.

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample19.aspx)]

*Courses.aspx.cs*, 추가 `using` 문을 합니다 `System.Data` 네임 스페이스는 동시성 예외에 대 한 확인 하는 메서드를 추가 하 고에 대 한 처리기를 추가 합니다 `EntityDataSource` 컨트롤의 `Updated` 및 `Deleted`처리기입니다. 코드는 다음과 같이 표시 됩니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample20.cs)]

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample21.cs)]

이 코드와 수행한 작업에 대 한 간의 유일한 차이점은 `ObjectDataSource` 컨트롤은이 경우 동시성 예외에는 `Exception` 해당 예외가 아닌 이벤트 인수 개체의 속성 `InnerException` 속성.

페이지를 실행 하 고 동시성 충돌을 다시 만듭니다. 이 이번에는 오류 메시지가 표시:

[![Image23](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image46.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image45.png)

동시성 충돌 처리에 대한 소개를 완료합니다. 다음 자습서에서는 Entity Framework를 사용 하는 웹 응용 프로그램의 성능을 향상 하는 방법에 지침을 제공 합니다.

> [!div class="step-by-step"]
> [이전](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)
> [다음](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)
