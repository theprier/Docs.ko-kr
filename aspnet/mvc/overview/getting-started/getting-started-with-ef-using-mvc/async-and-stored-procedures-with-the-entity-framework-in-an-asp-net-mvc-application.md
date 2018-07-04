---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
title: Async 및 ASP.NET MVC 응용 프로그램에서 Entity Framework 사용 하 여 저장된 프로시저 | Microsoft Docs
author: tdykstra
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/07/2014
ms.topic: article
ms.assetid: 27d110fc-d1b7-4628-a763-26f1e6087549
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 4c2deb53856d79a52415db48e04ea96111833b02
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37381931"
---
<a name="async-and-stored-procedures-with-the-entity-framework-in-an-aspnet-mvc-application"></a>Async 및 ASP.NET MVC 응용 프로그램에서 Entity Framework 사용 하 여 저장된 프로시저
====================
[Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트를 다운로드](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) 또는 [PDF 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)

> Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio 2013을 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요.


이전 자습서에서 읽고 동기 프로그래밍 모델을 사용 하 여 데이터를 업데이트 하는 방법을 알아보았습니다. 이 자습서는 비동기 프로그래밍 모델을 구현 하는 방법을 볼 수 있습니다. 비동기 코드는 더 나은 서버 리소스 사용 했기 때문에 더 잘 수행 하는 응용 프로그램을 수 있습니다.

이 자습서에서는 또한 삽입, 업데이트 및 삭제 작업 엔터티에 대 한 저장된 프로시저를 사용 하는 방법을 배웁니다.

마지막으로 처음 배포한 이후 구현한 데이터베이스 변경 내용을 모든와 함께 azure에 응용 프로그램을 다시 배포할 수 있습니다.

다음 그림에서는 사용할 일부 페이지를 보여 줍니다.

![부서 페이지](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![부서를 만듭니다](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="why-bother-with-asynchronous-code"></a>비동기 코드를 사용 하 여 굳이

웹 서버에는 사용할 수 있는 스레드 수가 제한적이며, 로드 양이 많은 상황에서는 사용 가능한 모든 스레드가 사용될 수 있습니다. 이 경우 서버는 스레드가 해제될 때까지 새 요청을 처리할 수 없습니다. 동기 코드를 사용하면 I/O 완료를 대기하느라 작업을 실제로 수행하지 않는 동안에 많은 스레드가 정체될 수 있습니다. 비동기 코드를 사용하면 프로세스가 I/O 완료를 대기할 때 다른 요청을 처리하는 데 사용하도록 해당 스레드가 서버에서 해제됩니다. 결과적으로, 비동기 코드를 사용 하면 서버 리소스를를 보다 효율적으로 사용 되며 서버 지연 없이 더 많은 트래픽을 처리할 수 수 있습니다.

.NET의 이전 버전에서 작성 하 고 비동기 코드를 테스트 된 복잡 한 오류가 발생 하기 쉽고, 디버깅 하기가 어렵습니다. .NET 4.5 작성, 테스트 및 비동기 코드를 디버깅은 훨씬 쉬워졌기 때문에 한 이유가 없다면 없는 비동기 코드 일반적으로 작성 해야 합니다. 비동기 코드는 적은 양의 오버 헤드를 도입 하지만 트래픽이 낮은 상황의 성능 저하는 미미 합니다 하는 동안 트래픽이 높은 상황에서는 잠재적 성능 향상이 상당한 합니다.

비동기 프로그래밍에 대 한 자세한 내용은 참조 하세요. [호출을 차단 하지 않기 위해 사용 하 여.NET 4.5의 비동기 지원](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async)합니다.

## <a name="create-the-department-controller"></a>부서 컨트롤러 만들기

이 시간을 제외 하 고 이전 컨트롤러에 수행한 것과 동일한 방식으로 선택 하는 부서 컨트롤러를 만들려면 합니다 **사용 하 여 비동기 컨트롤러** 작업 확인란 합니다.

![부서 컨트롤러 스 캐 폴드](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

다음 강조 표시에 대 한 동기 코드에 추가 된 기능을 `Index` 메서드를 비동기:

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=1,4)]

비동기적으로 실행 하는 Entity Framework 데이터베이스 쿼리를 사용 하도록 설정 하려면 네 가지 변경 내용이 적용 됩니다.

- 메서드가 사용 하 여 표시 합니다 `async` 키워드는 컴파일러가 메서드 본문 부분에 대 한 콜백을 생성 하 고 자동으로 만들 수 있는 `Task<ActionResult>` 반환 되는 개체입니다.
- 반환 형식을 변경한 `ActionResult` 에 `Task<ActionResult>`입니다. 합니다 `Task<T>` 형식을 나타내는 형식의 결과 사용 하 여 진행 중인 작업 `T`합니다.
- `await` 키워드 웹 서비스 호출에 적용 되었습니다. 컴파일러가이 키워드를 인식 하는 경우 백그라운드에서 해당 메서드를 두 부분으로 분할 합니다. 첫 번째 부분은 비동기적으로 시작 되는 작업을 사용 하 여 종료 합니다. 두 번째 부분은 작업이 완료 될 때 호출 되는 콜백 메서드에 배치 됩니다.
- 비동기 버전을 `ToList` 확장 메서드가 호출 되었습니다.

이유는 합니다 `departments.ToList` 문을 수정 하지만 `departments = db.Departments` 문을? 이유는 쿼리 또는 명령을 데이터베이스를 전송할 수 있도록 하는 명령문만 비동기적으로 실행 됩니다. `departments = db.Departments` 문은 쿼리 설정 되지만 쿼리 될 때까지 실행 되지 않습니다는 `ToList` 메서드가 호출 됩니다. 따라서만 `ToList` 메서드를 비동기적으로 실행 합니다.

에 `Details` 메서드 및 `HttpGet` `Edit` 하 고 `Delete` 메서드를 `Find` 메서드는 비동기적으로 실행 되는 메서드는 데이터베이스를 전송할 수 있도록 쿼리를 발생 시키는 것:

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs?highlight=7)]

에 `Create`, `HttpPost Edit`, 및 `DeleteConfirmed` 메서드를 합니다 `SaveChanges` 실행할 명령을 발생 시키는 메서드 호출, 같은 문의 하지 `db.Departments.Add(department)` 엔터티 수정할 메모리에만 발생 하는 합니다.

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=6)]

오픈 *Views\Department\Index.cshtml*, 템플릿 코드를 다음 코드로 바꿉니다.

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=3,5,20-22,36-38)]

이 코드 제목을 변경 하는 인덱스에서 부서, 관리자 이름 오른쪽으로 이동한 후 관리자의 전체 이름을 제공 합니다.

만들기, 삭제, 세부화, 고 뷰를 편집에 대 한 캡션을 변경는 `InstructorID` 필드를 "Administrator" 같은 방식으로 강좌 보기에 "부서"으로 부서 이름 필드를 변경 합니다.

뷰는 만들기 및 편집에 다음 코드를 사용합니다.

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml)]

삭제 및 세부 정보 보기에서 다음 코드를 사용 합니다.

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

응용 프로그램을 실행 하 고 클릭 합니다 **부서** 탭 합니다.

![부서 페이지](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

모든 다른 컨트롤러와 동일 하 게 작동 하지만이 컨트롤러의 모든 SQL 쿼리는 비동기적으로 실행 합니다.

Entity Framework를 사용한 비동기 프로그래밍을 사용할 때 알아야 할 몇 가지 사항은 다음과 같습니다.

- 비동기 코드를 스레드로부터 안전 하지 않습니다. 즉, 즉, 하려고 하지 마세요 동일한 컨텍스트 인스턴스를 사용 하 여 병렬로 여러 작업을 수행 합니다.
- 비동기 코드의 성능 이점을 활용하려는 경우 사용 중인(예: 페이징) 라이브러리 패키지 또한 쿼리를 데이터베이스에 전송하도록 하는 Entity Framework 메서드를 호출하는 경우 비동기를 사용하는지 확인합니다.

## <a name="use-stored-procedures-for-inserting-updating-and-deleting"></a>삽입, 업데이트 및 삭제에 대 한 저장된 프로시저를 사용 합니다.

일부 개발자와 dba가 데이터베이스 액세스를 위한 저장된 프로시저를 사용 하려면. 이전 버전의 Entity Framework에서 저장된 프로시저를 사용 하 여 데이터를 검색할 수 있습니다 [원시 SQL 쿼리 실행](advanced-entity-framework-scenarios-for-an-mvc-web-application.md), 하지만 업데이트 작업에 대 한 저장된 프로시저를 사용 하는 EF를 지시할 수 없습니다. EF 6에서 Code First 저장된 프로시저를 사용 하도록 구성 하기 쉽습니다.

1. *DAL\SchoolContext.cs*, 강조 표시 된 코드를 추가 하 여 `OnModelCreating` 메서드.

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=9)]

    업데이트 및 삭제 작업에이 코드를 사용 하 여 저장 프로시저는 삽입, Entity Framework는 지시 된 `Department` 엔터티.
2. 패키지 관리 콘솔에서 다음 명령을 입력 합니다.

    `add-migration DepartmentSP`

    오픈 *마이그레이션을\&l t; 타임 스탬프&gt;\_DepartmentSP.cs* 의 코드를 참조 하는 `Up` 만드는 메서드를 삽입, 업데이트 및 삭제 저장 프로시저:

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs?highlight=3-4,26-27,42-43)]
3. 패키지 관리 콘솔에서 다음 명령을 입력 합니다.

     `update-database`
4. 디버그 모드에서 응용 프로그램 실행을 클릭 합니다 **부서** 탭을 클릭 한 다음 **새로 만들기**합니다.
5. 새 학과 대 한 데이터를 입력 한 다음 클릭 **만들기**합니다.

     ![부서를 만듭니다](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
6. Visual Studio에서 로그를 확인 합니다 **출력** 창 새 부서 행을 삽입 하려면 저장된 프로시저를 사용 했는지 확인 합니다.

     ![부서 삽입 SP](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

코드는 먼저 기본 저장 프로시저 이름을 만듭니다. 기존 데이터베이스를 사용 하는 경우 데이터베이스에 이미 정의 된 저장된 프로시저를 사용 하려면 저장된 프로시저 이름을 사용자 지정 해야 합니다. 그렇게 하는 방법에 대 한 정보를 참조 하세요 [Entity Framework 코드 첫 번째 Insert/Update/Delete 저장 프로시저](https://msdn.microsoft.com/data/dn468673)합니다.

항목 생성 저장된 프로시저를 수행 하는 사용자 지정 하려는 경우 마이그레이션 스 캐 폴드 된 코드를 편집할 수 있습니다 `Up` 메서드는 저장된 프로시저를 만듭니다. 이런 방식으로 변경 내용이 반영 됩니다 때마다 마이그레이션 실행 하 고 마이그레이션 배포 된 후 프로덕션에서 자동으로 실행 될 때 프로덕션 데이터베이스에 적용 됩니다.

추가 마이그레이션 명령을 사용 하 여 새 마이그레이션을 생성 하 고 수동으로 호출 하는 코드를 작성할 수 마이그레이션 이전에 만든 기존 저장된 프로시저를 변경 하려는 경우는 [AlterStoredProcedure](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx) 메서드 .

## <a name="deploy-to-azure"></a>Azure에 배포

이 섹션에서는 선택적 완료 해야 **Azure에 앱을 배포** 섹션을 [마이그레이션 및 배포](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md) 이 시리즈의 자습서입니다. 로컬 프로젝트에서 데이터베이스를 삭제 하 여 해결 하는 마이그레이션 오류를 설치한 경우이 섹션을 건너뜁니다.

1. Visual studio에서에서 프로젝트를 마우스 오른쪽 단추로 **솔루션 탐색기** 선택한 **게시** 상황에 맞는 메뉴입니다.
2. **게시**를 클릭합니다.

    Visual Studio에는 응용 프로그램을 azure에 배포 하 고 응용 프로그램이 Azure에서 실행 중인 기본 브라우저에서 열립니다.
3. 확인을 위해 응용 프로그램을 테스트 작동 합니다.

    실행 하는 페이지는 처음에는 데이터베이스에 액세스, Entity Framework를 실행 하 여 마이그레이션의 모든 `Up` 데이터베이스를 현재 데이터 모델을 사용 하 여 최신 상태로 만드는 데 필요한 메서드. 이제 마지막으로이 자습서에서 추가한 부서 페이지를 포함 하 여 배포한 이후에 추가 된 웹 페이지의 모든 사용할 수 있습니다.

## <a name="summary"></a>요약

이 자습서에서는 배웠습니다 비동기적으로 실행 되는 코드를 작성 하 여 서버 효율성을 개선 하는 방법에 대 한 저장된 프로시저를 사용 하는 방법을 삽입, 업데이트 및 삭제 작업. 다음 자습서에서는 여러 사용자가 동시에 동일한 레코드를 편집 하려고 하는 경우 데이터 손실을 방지 하는 방법을 배웁니다.

다른 Entity Framework 리소스에 대 한 링크에서 찾을 수 있습니다 합니다 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

> [!div class="step-by-step"]
> [이전](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [다음](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
