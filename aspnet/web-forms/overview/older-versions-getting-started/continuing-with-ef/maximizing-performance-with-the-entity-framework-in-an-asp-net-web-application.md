---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application
title: Entity framework 4.0 ASP.NET 4 웹 응용 프로그램의 성능을 최대화 | Microsoft Docs
author: tdykstra
description: 이 자습서 시리즈의 Entity Framework 4.0 자습서 시리즈 시작 하기에 의해 만들어진 Contoso 대학 웹 응용 프로그램 기반으로 합니다. I 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/26/2011
ms.topic: article
ms.assetid: 4e43455e-dfa1-42db-83cb-c987703f04b5
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application
msc.type: authoredcontent
ms.openlocfilehash: b85645eebf2822b33df944692736ea9d9b69b9aa
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="maximizing-performance-with-the-entity-framework-40-in-an-aspnet-4-web-application"></a>Entity framework 4.0 ASP.NET 4 웹 응용 프로그램에서 성능 최적화
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

> 에 의해 만들어진 Contoso 대학 웹 응용 프로그램을 기반으로 하는이 자습서 시리즈의 [Entity Framework 4.0이 있는 시작](https://asp.net/entity-framework/tutorials#Getting%20Started) 자습서 시리즈 합니다. 이전 자습서를 완료 하지 않은 경우이 자습서에 대 한 시작 점으로 하면 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) 만들어졌을 것입니다. 수도 있습니다 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) 완료 하는 자습서 시리즈에서 만들어진 합니다. 이 자습서에 대 한 질문이 있으면에 게시할 수 있습니다는 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx)합니다.


이전 자습서에서 동시성 충돌을 처리 하는 방법을 알아보았습니다. 이 자습서는 Entity Framework를 사용 하 여 ASP.NET 웹 응용 프로그램의 성능 향상을 위한 옵션을 보여 줍니다. 성능을 최대화 하거나 성능 문제를 진단 하기 위한 여러 가지 방법을 설명 합니다.

다음 섹션에 제시 된 정보는 다양 한 시나리오에서에서 유용 하 게 되려면 있습니다.

- 관련된 데이터를 효율적으로 로드 합니다.
- 뷰 상태를 관리 합니다.

다음 섹션에 제시 된 정보는 개별 쿼리에 있는 해당 성능 문제가 있는 경우 유용할 수 있습니다.

- 사용 하 여 `NoTracking` 병합 옵션입니다.
- LINQ 쿼리를 미리 컴파일하십시오.
- 데이터베이스에 전송 되는 쿼리 명령을 검토 합니다.

다음 섹션에 제시 된 정보는 매우 큰 데이터 모델에 있는 응용 프로그램에 대 한 잠재적으로 유용 합니다.

- 미리 보기를 생성 합니다.

> [!NOTE]
> 웹 응용 프로그램 성능은 요청 및 응답 데이터의 크기, 데이터베이스 쿼리, 몇 개의 요청 서버 큐에 대기 수 및 속도, 및의 효율성도 서비스할 수의 속도 등을 포함 하 여 다양 한 요인의 영향 클라이언트 스크립트 라이브러리를 사용할 수 있습니다. 성능이 응용 프로그램에서 중요 한 경우 하거나 테스트 또는 환경 표시 되는 응용 프로그램 성능 없습니다 만족 스러운 성능 조정에 대 한 일반 프로토콜을 따라야 합니다. 성능 병목 현상이 발생 하는 위치를 확인 하 고 전반적인 응용 프로그램 성능에 가장 큰 영향을 미칠 수 있는 영역을 해결.
> 
> 이 항목에서는 주로 구체적으로 ASP.NET의 Entity Framework의 성능을 잠재적으로 향상 수 있는 방법입니다. 여기에 제안 사항은 데이터 액세스 응용 프로그램에서 성능 병목 지점 중 하나 인지 확인 한 경우에 유용 합니다. 여기에서 설명한 방법으로 간주 해서는 안 언급 했 듯이 점을 제외 하 고 &quot;모범 사례&quot; 일반적-중 대부분이 예외적인 경우에만 또는 성능 병목 현상의 매우 구체적인 종류 주소에 해당 합니다.


이 자습서를 시작 하려면 Visual Studio를 시작 하 고 이전 자습서에서 작업 하는 Contoso 대학 웹 응용 프로그램을 엽니다.

## <a name="efficiently-loading-related-data"></a>관련된 데이터를 효율적으로 로드

여러 가지 방법으로 Entity Framework가 엔터티의 탐색 속성에 관련된 데이터를 로드할 수 있습니다.

- *지연 로드*. 엔터티를 처음 읽을 때 관련된 데이터가 검색되지 않습니다. 그러나 탐색 속성에 처음으로 액세스하려고 할 때 해당 탐색 속성에 필요한 데이터가 자동으로 검색됩니다. 이 인해 데이터베이스에 전송 하는 여러 개의 쿼리-엔터티 자체에 대 한 개와 때마다 관련 엔터티에 대 한 데이터를 검색 해야 합니다. 

    [![Image05](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image2.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image1.png)

*즉시 로드*. 엔터티를 읽을 때 관련된 데이터가 함께 검색됩니다. 이는 일반적으로 필요한 데이터를 모두 검색하는 단일 조인 쿼리를 발생시킵니다. 즉시 로드를 사용 하 여 지정 된 `Include` 메서드를 때를 살펴 보았으며 이미이 자습서에 합니다.

[![Image07](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image4.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image3.png)

- *명시적 로드*. 이 지연 로드를 제외 하 코드에서 관련된 데이터를 명시적으로 검색 탐색 속성에 액세스할 때 자동으로 발생 하지 않습니다. 관련된 데이터를 사용 하 여 수동으로 부하는 `Load` 컬렉션 또는 사용자에 대 한 탐색 속성의 메서드를 사용 하 여는 `Load` reference 속성의 단일 개체를 포함 하는 속성에 대 한 메서드. (호출 하는 예를 들어는 `PersonReference.Load` 개체에 대 한는 `Person` 의 탐색 속성을 `Department` 엔터티.)

    [![Image06](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image6.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image5.png)

속성 값을 즉시 검색 하지 않으므로 지연 로드 및 명시적 로딩 둘 다 라고도 *지연 된 로드*합니다.

지연 로드는 디자이너에서 생성 된 개체 컨텍스트에 대 한 기본 동작입니다. 여는 경우는 *SchoolModel.Designer.cs* 파일 개체 컨텍스트 클래스를 정의 하는, 세 가지 생성자 메서드를 찾을 수 있습니다 및 다음 문은 각각의 포함:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample1.cs)]

일반적으로 알고 있는 경우 관련 된 데이터에 필요한 모든 엔터티 검색, 신속 하 게 로드 최상의 성능을 제공 데이터베이스에 전송 하는 단일 쿼리를 검색할 각 엔터티에 대 한 별개의 쿼리와 보다 일반적으로 더 효율적 이므로 합니다. 반면, 자주 엔터티의 탐색 속성에 액세스 해야 할 경우에 대해서만 또는 작은 즉시 로드 필요한 것 보다 더 많은 데이터를 검색 하기 때문에 엔터티, 지연 로드 또는 명시적 로드 집합을 보다 효율적 수 있습니다.

웹 응용 프로그램에서 한 지연 로딩이 때문일 상대적으로 작은 값의 누르고, 페이지를 렌더링 하는 개체 컨텍스트에 연결 되지 브라우저에서 관련된 데이터에 대 한 필요성에 영향을 주는 사용자 작업이 수행입니다. 반면에 컨트롤 databind 알고 있는 경우 일반적으로 필요한을 즉시 로드 또는 지연 된 로드에 따라 선택할 수 있으므로 일반적으로 최상의 데이터 란 각 시나리오에 적합 합니다.

또한 데이터 바인딩된 컨트롤 개체 컨텍스트를 삭제 한 후 엔터티 개체를 사용할 수 있습니다. 이 경우에 탐색 속성 지연 로드 하려는 시도가 실패 합니다. 나타나는 오류 메시지는 명확. &quot;`The ObjectContext instance has been disposed and can no longer be used for operations that require a connection.`&quot;

`EntityDataSource` 컨트롤 기본적으로 지연 로딩을 사용 하지 않도록 설정 합니다. 에 대 한는 `ObjectDataSource` 컨트롤 현재 자습서에 사용 하는 (또는 개체 컨텍스트에 페이지 코드에서 액세스 하는 경우), 여러 가지 방법으로 지연 가능 로딩을 기본적으로 비활성화 합니다. 개체 컨텍스트에 인스턴스화할 때 해제할 수 있습니다. 예를 들어 다음 줄의 생성자 메서드를 추가할 수 있습니다는 `SchoolRepository` 클래스:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample2.cs)]

Contoso 대학 응용 프로그램에 대 한 개체 컨텍스트에 자동으로이 속성 컨텍스트 인스턴스화될 때마다 설정 하지 않아도 되도록 지연 로드를 사용 하지 않도록 지정 합니다.

열기는 *SchoolModel.edmx* 데이터 모델을 디자인 화면을 클릭 한 다음 속성 창에서 설정 된 **지연 로드 사용** 속성을 `False`합니다. 저장 하 고 데이터 모델을 닫습니다.

[![Image04](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image8.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image7.png)

## <a name="managing-view-state"></a>뷰 상태를 관리합니다.

업데이트 기능을 제공 하기 위해 ASP.NET 웹 페이지는 페이지가 렌더링 될 때 엔터티 원래 속성 값을 저장 해야 합니다. 포스트백 컨트롤을 처리 하는 동안 다시 엔터티의 원래 상태로 만들고 수 엔터티의 호출 `Attach` 메서드를 호출 하 고 변경 내용을 적용 하기 전에 `SaveChanges` 메서드. 기본적으로 ASP.NET Web Forms 데이터 컨트롤 뷰 상태를 사용 하 여 원래 값을 저장 합니다. 그러나 뷰 상태 브라우저에서 보내고 있는 페이지의 크기를 크게 높일 수 있는 숨겨진된 필드에 저장 되므로 성능에 영향을 줄 수 있습니다.

보기 상태나 세션 상태 등의 대체 기능을 관리 하기 위한 기술이 되므로이 자습서를 자세히가이 항목으로 이동 하지 않습니다 Entity Framework에 고유 하지 않습니다. 자세한 내용은 자습서의 끝에 링크를 참조 합니다.

버전 4의 ASP.NET Web Forms 응용 프로그램의 모든 ASP.NET 개발자가 알아야 할 뷰 상태와 함께 작업 하는 새로운 방식으로 제공 하는 반면:는 `ViewStateMode` 속성입니다. 이 새 속성 페이지 또는 제어 수준에서 설정할 수 있습니다 및 페이지에 대해 기본적으로 상태 보기를 사용 하지 않도록 설정 하 고 필요로 하는 컨트롤에 대해서만 사용 하도록 설정할 수 있습니다.

응용 프로그램의 성능 상태가 심각 경우 항상 페이지 수준에서 뷰 상태를 사용 하지 않도록 설정 하 고 필요로 하는 컨트롤에 대해서만 사용 하도록 설정 하는 좋은 좋습니다. Contoso 대학 페이지에 대 한 뷰 상태의 크기는이 메서드에 의해 상당히 줄일 수 없게 되지만 작동 방식을 보려면 합니다 것에 대 한는 *Instructors.aspx* 페이지. 다양 한 컨트롤을 포함 하 여 해당 페이지에 포함 되어는 `Label` 컨트롤을 포함 합니다. 이 페이지에 있는 컨트롤의 없음 실제로 필요 보기 상태에서 사용 됩니다. (의 `DataKeyNames` 속성은 `GridView` 다시 게시 간에 유지 해야 하는 상태를 지정 하는 제어 하지만 이러한 값에 영향을 받지 않습니다 컨트롤 상태를 유지 됩니다는 `ViewStateMode` 속성입니다.)

`Page` 지시문 및 `Label` 컨트롤 태그에는 현재 다음 예제와 유사 합니다.

[!code-aspx[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample3.aspx)]

다음과 같이 변경 합니다.

- 추가 `ViewStateMode="Disabled"` 에 `Page` 지시문입니다.
- 제거 `ViewStateMode="Disabled"` 에서 `Label` 제어 합니다.

태그에는 이제 다음 예제를 비슷합니다.

[!code-aspx[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample4.aspx)]

모든 컨트롤에 대 한 현재 뷰 상태 비활성화 되었습니다. 포함은 하기만 하면 나중에 뷰 상태를 사용 해야 하는 컨트롤을 추가 하는 경우는 `ViewStateMode="Enabled"` 해당 컨트롤에 대 한 특성입니다.

## <a name="using-the-notracking-merge-option"></a>NoTracking 병합 옵션을 사용 하 여

개체 컨텍스트에 데이터베이스 행을 검색 하 고을 나타내는 엔터티 개체를 만드는 경우 기본적으로도 추적의 개체 상태 관리자를 사용 하 여 해당 엔터티 개체입니다. 이 추적 데이터는 한 캐시 역할을 하 고 엔터티를 업데이트할 때 사용 됩니다. 일반적으로 웹 응용 프로그램의 수명이 짧은 개체 컨텍스트 인스턴스가 때문에 쿼리 보통 개체 컨텍스트를 읽어옵니다를 읽어 온 엔터티는 다시 사용 전에 삭제 되는지 때문에 추적 되어야 필요 없는 데이터를 반환 합니다. 또는 업데이트 됩니다.

Entity Framework에서 지정할 수 있습니다 개체 컨텍스트를 설정 하 여 엔터티 개체를 추적 하는지 여부를 *병합 옵션*합니다. 개별 쿼리에 대 한 또는 엔터티 집합에 대 한 병합 옵션을 설정할 수 있습니다. 엔터티 집합에 대해 설정한 경우 해당 엔터티 집합에 대해 생성 된 모든 쿼리에 대 한 기본 병합 옵션을 설정 하는 것입니다.

Contoso 대학 응용 프로그램에 대 한 추적 병합 옵션을 설정할 수 있는 저장소에서 액세스 하는 엔터티 집합에 대 한 필요 하지 않습니다 `NoTracking` 개체 컨텍스트 저장소 클래스를 인스턴스화할 때 해당 엔터티 집합에 대 한 합니다. (참고는이 자습서에서는 병합 옵션을 설정 하지 않습니다 필요 응용 프로그램의 성능에 별다른 영향입니다. `NoTracking` 옵션은 특정 데이터 대량 시나리오에만 예측 가능한 성능 향상 가능성이 있습니다.)

DAL 폴더를 열고는 *SchoolRepository.cs* 파일을 저장소에서 액세스 하는 엔터티 집합에 대 한 병합 옵션을 설정 하는 생성자 메서드를 추가 합니다.

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample5.cs)]

## <a name="pre-compiling-linq-queries"></a>미리 컴파일 LINQ 쿼리

Entity Framework의 수명 내에서 Entity SQL 쿼리를 실행 하는 처음으로 주어진 `ObjectContext` 인스턴스의 시간이 걸리는 쿼리를 컴파일하는 데 있습니다. 쿼리의 후속 실행 속도가 훨씬 빨라집니다 됨을 의미 하는 컴파일 결과 캐시 됩니다. LINQ 쿼리 제외 하 고 쿼리를 컴파일하는 데 필요한 작업의 일부 완료 때마다 쿼리가 실행 되는 유사한 패턴을 따릅니다. 즉, LINQ 쿼리에 대해 기본적으로 모든 컴파일 결과를 캐시 됩니다.

개체 컨텍스트에의 수명에서 반복적으로 실행 해야 하는 LINQ 쿼리를 사용 하도록 설정한 경우 모든 LINQ 쿼리를 실행 하는 처음으로 캐시 되도록 컴파일 결과 발생 시키는 코드를 작성할 수 있습니다.

그림과 같이 작업 2에 대 한 `Get` 의 메서드는 `SchoolRepository` 클래스 중 하나는 매개 변수를 사용 하지 않습니다 (의 `GetInstructorNames` 메서드)에 매개 변수가 필요 하 고 다른 하나 (의 `GetDepartmentsByAdministrator` 메서드). 이러한 방법으로 서식을 이제 실제로 필요가 없습니다 LINQ 쿼리 수 없기 때문에 컴파일할 수 없습니다:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample6.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample7.cs)]

그러나 있으므로 진행 하는 컴파일된 쿼리를 수행 하려면 합니다 다음 LINQ 쿼리도 기록 된 이러한 하는 경우:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample8.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample9.cs)]

위에 표시 된 개이고 계속 하기 전에 작동 하는지 확인 하려면 응용 프로그램 실행 작업으로 이러한 메서드의 코드를 변경할 수 있습니다. 하지만 다음 지침에 미리 컴파일된 버전을 만드는 바로 합니다.

클래스 파일을 만듭니다는 *DAL* 폴더를 이름을 *SchoolEntities.cs*, 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample10.cs)]

이 코드는 자동으로 생성 된 개체 컨텍스트 클래스를 확장 하는 partial 클래스를 만듭니다. 사용 하 여 두 개의 컴파일된 LINQ 쿼리를 포함 하는 partial 클래스는 `Compile` 의 메서드는 `CompiledQuery` 클래스입니다. 또한 쿼리를 호출 하는 데 사용할 수 있는 메서드를 만듭니다. 저장 하 고이 파일을 닫습니다.

다음 *SchoolRepository.cs*, 기존 변경 `GetInstructorNames` 및 `GetDepartmentsByAdministrator` 저장소의 메서드는 컴파일된 쿼리를 호출할 수 있도록 클래스:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample11.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample12.cs)]

실행 된 *Departments.aspx* 페이지 이전과 같이 작동 하는지 확인 합니다. `GetInstructorNames` 관리자 드롭 다운 목록 채우기 위해 메서드를 호출 및 `GetDepartmentsByAdministrator` 클릭 하면 메서드는 **업데이트** 없는 강사 둘 이상의의 관리자 인지 확인 하려면 부서입니다.

[![Image03](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image10.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image9.png)

미리 컴파일된 쿼리 성능이 눈에 띄게 향상 시키는 때문이 아니라, 수행 하는 방법을 참조에 Contoso 대학 응용 프로그램에서 했습니다. LINQ 쿼리를 미리 컴파일 코드에 간단한 수준을 제시 추가할가, 실제로 응용 프로그램에서 성능 병목 상태를 표현 하는 쿼리에 대해서만 수행 해야.

## <a name="examining-queries-sent-to-the-database"></a>데이터베이스에 전송 하는 쿼리

때 성능 문제를 조사 하는 것이 유용한 경우도 Entity Framework 데이터베이스에 전송 하는 정확한 SQL 명령에 알아야 합니다. 작업 하는 경우는 `IQueryable` 개체를 사용 하는 것이 작업을 수행 하는 한 가지 방법은 `ToTraceString` 메서드.

*SchoolRepository.cs*의 코드 변경의 `GetDepartmentsByName` 다음 예제와 일치 하도록 메서드:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample13.cs)]

`departments` 변수도 캐스팅 되어야 합니다는 `ObjectQuery` 때문에 입력는 `Where` 앞 줄의 끝에 메서드를 만듭니다는 `IQueryable` 개체 없이 `Where` 메서드를 캐스팅 필요 하지 않을 것입니다.

에 중단점을 설정의 `return` 줄을 실행 한 다음는 *Departments.aspx* 디버거에서 페이지입니다. 중단점에 도달 하면 검사는 `commandText` 에서 변수는 **지역** 창과 텍스트 시각화 도우미를 사용 하 여 (에 돋보기는 **값** 열)는 에해당값을표시**텍스트 시각화 도우미** 창. 이 코드에서 생성 된 전체 SQL 명령으로 확인할 수 있습니다.

[![Image08](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image12.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image11.png)

대신 Visual Studio Ultimate에서 IntelliTrace 기능 코드를 변경 하거나도 중단점을 설정 하도록 요구 하지 않습니다는 Entity Framework에서 생성 된 SQL 명령을 확인 하는 방법을 제공 합니다.

> [!NOTE]
> Visual Studio Ultimate가 있는 경우에 다음 절차를 수행할 수 있습니다.


복원의 원본 코드는 `GetDepartmentsByName` 메서드와 다음 실행은 *Departments.aspx* 디버거에서 페이지입니다.

Visual Studio에서 선택 된 **디버그** 메뉴, **IntelliTrace**, 차례로 **IntelliTrace 이벤트**합니다.

[![Image11](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image14.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image13.png)

에 **IntelliTrace** 창 클릭 **모두 중단**합니다.

[![Image12](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image16.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image15.png)

**IntelliTrace** 창은 최근 이벤트의 목록을 표시 합니다.

[![Image09](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image18.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image17.png)

클릭는 **ADO.NET** 선입니다. 명령 텍스트를 표시 하려면 확장 합니다.

[![Image10](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image20.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image19.png)

전체 명령 텍스트 문자열에서 클립보드에 복사할 수 있습니다는 **지역** 창.

테이블, 관계 및 간단한 보다 열을 사용 하 여 데이터베이스를 사용 하는 가정 `School` 데이터베이스입니다. 단일에 필요한 모든 정보를 수집 하는 쿼리를 찾을 수 있습니다 `Select` 다중 포함 하는 문이 `Join` 효율적으로 작동 하도록 절 너무 복잡해 집니다. 이 경우 쿼리를 단순화 하기 위해 명시적으로 로드 하려면 로드 하는 eager에서 전환할 수 있습니다.

예를 들어 바꾸려고의 코드는 `GetDepartmentsByName` 메서드에서 *SchoolRepository.cs*합니다. 현재 수 있다는 점에서 메서드가 포함 된 개체 쿼리에 `Include` 에 대 한 메서드는 `Person` 및 `Courses` 탐색 속성입니다. 대체는 `return` 다음 예제와 같이 명시적 로드를 수행 하는 코드를 사용 하 여 문을:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample14.cs)]

실행 된 *Departments.aspx* 디버거에서 페이지는 **IntelliTrace** 창으로 다시 가입 하지 않은 합니다. 이제는 단일 쿼리 하기 전에 있었던의 긴 시퀀스가 참조 합니다.

[![Image13](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image22.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image21.png)

첫 번째 클릭 **ADO.NET** 줄 변경 된 것으로 복잡 한 쿼리 수를 확인 하려면 이전 표시 합니다.

[![Image14](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image24.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image23.png)

부서에서 쿼리는 간단한 바뀌었기 `Select` 없이 쿼리 `Join` 원본에서 반환 된 각 부서에 대 한 두 개의 쿼리 집합을 사용 하 여 관련된 과정 및 관리자를 검색 하는 별도 쿼리 절 하지만 뒤, 쿼리입니다.

> [!NOTE]
> 두면 지연 로드 사용, 동일한 쿼리를 여러 번 반복와 여기에서 표시 하는 패턴의 지연 로드 될 수 있습니다. 방지 하려면 일반적으로 하는 패턴은 기본 테이블의 모든 행에 대 한 지연 로딩이 관련된 데이터입니다. 단일 조인 쿼리가 너무 복잡해 서 효율적 임을 확인 한 경우가 아니면는 일반적으로 즉시 로드를 사용 하는 기본 쿼리를 변경 하 여 이러한 경우에는 성능 향상 시킬 수 없습니다.


## <a name="pre-generating-views"></a>뷰 미리 생성

경우는 `ObjectContext` 개체가 먼저 만들어진 새 응용 프로그램 도메인, Entity Framework에서 사용 하 여 데이터베이스에 액세스 하는 클래스 집합을 생성 합니다. 이러한 클래스 라고 *뷰*, 매우 큰 데이터 모델을 사용 하는 경우 이러한 뷰를 생성이 지연 될 수 웹 사이트의 요청에 응답 하는 첫 번째 페이지에 대 한 새 응용 프로그램 도메인 초기화 된 후입니다. 런타임이 아닌 컴파일 타임에 뷰를 만들어 이러한 첫 번째 요청 지연 시간을 줄일 수 있습니다.

> [!NOTE]
> 응용 프로그램이 없는 경우는 매우 큰 데이터 모델 또는 큰 데이터 모델에는 IIS가 재활용 후에 첫 번째 페이지 요청에 영향을 주는 성능 문제에 대 한 고려 하지 않는 경우에이 섹션을 건너뛸 수 있습니다. 보기 만들기를 인스턴스화할 때마다 발생 하지 않는 한 `ObjectContext` 개체는 뷰는 응용 프로그램 도메인에 캐시 되므로 합니다. 따라서 IIS에서 응용 프로그램 재활용 자주 하는 경우가 아니면 매우 적은 페이지 요청 미리 생성 된 뷰에서 좋지 있습니다.


사용 하 여 뷰를 미리 생성할 수 있습니다는 *EdmGen.exe* 명령줄 도구를 사용 하 여 또는 *Text Template Transformation Toolkit* (T4) 템플릿을 합니다. 이 자습서에서는 T4 템플릿을 사용 합니다.

에 *DAL* 폴더를 사용 하 여 파일을 추가 **텍스트 템플릿** 서식 파일 (은 아래에 **일반** 에서 노드는 **설치 된 템플릿** 목록), 이름을 지정 *SchoolModel.Views.tt*합니다. 파일의 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample15.cs)]

이 코드에 대 한 뷰를 생성 한 *.edmx* 템플릿 파일과 같은 이름을 가진 및 템플릿과 같은 폴더에 있는 파일입니다. 예를 들어, 템플릿 파일의 이름은 *SchoolModel.Views.tt*, 명명 된 데이터 모델 파일을 찾습니다 *SchoolModel.edmx*합니다.

파일을 마우스 오른쪽 단추로 클릭 한 다음 파일을 저장 **솔루션 탐색기** 선택 **사용자 지정 도구 실행**합니다.

[![Image02](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image26.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image25.png)

Visual Studio 이라고 하는 뷰를 만드는 코드 파일을 생성 *SchoolModel.Views.cs* 템플릿을 기반으로 합니다. (보았을 것을 선택 하기 전에 코드 파일이 생성 됩니다 **사용자 지정 도구 실행**서식 파일을 저장 하는 즉시,.)

[![Image01](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image28.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image27.png)

이제 응용 프로그램을 실행 하 고 이전과 같이 작동 하는지 확인할 수 있습니다.

미리 생성 된 뷰에 대 한 자세한 내용은 다음 리소스를 참조 합니다.

- [방법: 미리 생성 뷰를 쿼리 성능을 향상 시킬](https://msdn.microsoft.com/library/bb896240.aspx) MSDN 웹 사이트. 사용 하는 방법에 설명 된 `EdmGen.exe` 명령줄 도구를 미리 보기를 생성 합니다.
- [미리 컴파일된/사전 generated 보기와 Entity Framework 4의 성능 격리](https://blogs.msdn.com/b/appfabriccat/archive/2010/08/06/isolating-performance-with-precompiled-pre-generated-views-in-the-entity-framework-4.aspx) Windows Server AppFabric 고객 자문 팀 블로그.

Entity Framework를 사용 하 여 ASP.NET 웹 응용 프로그램의 성능 향상을 도입을 완료 합니다. 자세한 내용은 다음 리소스를 참조하세요.

- [성능 고려 사항 (Entity Framework)](https://msdn.microsoft.com/library/cc853327.aspx) MSDN 웹 사이트입니다.
- [Entity Framework 팀 블로그 게시물 성능 관련](https://blogs.msdn.com/b/adonet/archive/tags/performance/)합니다.
- [EF 병합 옵션 및 컴파일된 쿼리](https://blogs.msdn.com/b/dsimmons/archive/2010/01/12/ef-merge-options-and-compiled-queries.aspx)합니다. 컴파일된 쿼리와 병합의 예기치 않은 동작을 설명 하는 블로그 게시물와 같은 옵션 `NoTracking`합니다. 컴파일된 쿼리를 사용 하거나 응용 프로그램에서 병합 옵션 설정을 조작 하려는 경우 먼저 읽으십시오.
- [Entity Framework 관련 데이터 및 모델링 고객 자문 팀 블로그의 게시물](https://blogs.msdn.com/b/dmcat/archive/tags/entity+framework/)합니다. 컴파일된 쿼리 및 성능 문제를 발견 하는 Visual Studio 2010 프로파일러 사용에 대 한 게시를 포함 합니다.
- [매우 복잡 한 쿼리 성능 향상에 정보를 제공 entity Framework 포럼 스레드](https://social.msdn.microsoft.com/Forums/adodotnetentityframework/thread/ffe8b2ab-c5b5-4331-8988-33a872d0b5f6)합니다.
- [ASP.NET 상태 관리 권장 사항](https://msdn.microsoft.com/library/z1hkazw7.aspx)합니다.
- [Entity Framework와는 ObjectDataSource를 사용 하 여: 사용자 지정 페이징](http://geekswithblogs.net/Frez/articles/using-the-entity-framework-and-the-objectdatasource-custom-paging.aspx)합니다. 블로그 게시물에서 페이징을 구현 하는 방법을 설명 하기 위해이 자습서에서 만든 ContosoUniversity 응용에 작성 되는 *Departments.aspx* 페이지.

다음 자습서에서 중요 한 향상 된 기능은을 Entity Framework 버전 4의에서 새로운 기능 중 일부를 검토 합니다.

> [!div class="step-by-step"]
> [이전](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)
> [다음](what-s-new-in-the-entity-framework-4.md)
