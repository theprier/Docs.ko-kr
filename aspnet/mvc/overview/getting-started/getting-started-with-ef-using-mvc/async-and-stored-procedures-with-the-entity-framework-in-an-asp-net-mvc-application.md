---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
title: Async 및 ASP.NET MVC 응용 프로그램에서 Entity Framework 사용 하 여 저장된 프로시저 | Microsoft Docs
author: tdykstra
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다...
ms.author: riande
ms.date: 11/07/2014
ms.assetid: 27d110fc-d1b7-4628-a763-26f1e6087549
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 84be966c1e1a4357125c1a53b8065676c8f073f6
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48910735"
---
<a name="async-and-stored-procedures-with-the-entity-framework-in-an-aspnet-mvc-application"></a><span data-ttu-id="c270f-103">Async 및 ASP.NET MVC 응용 프로그램에서 Entity Framework 사용 하 여 저장된 프로시저</span><span class="sxs-lookup"><span data-stu-id="c270f-103">Async and Stored Procedures with the Entity Framework in an ASP.NET MVC Application</span></span>
====================
<span data-ttu-id="c270f-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="c270f-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="c270f-105">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="c270f-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)

> <span data-ttu-id="c270f-106">Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 5 applications using the Entity Framework 6 Code First and Visual Studio.</span></span> <span data-ttu-id="c270f-107">자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c270f-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>


<span data-ttu-id="c270f-108">이전 자습서에서 읽고 동기 프로그래밍 모델을 사용 하 여 데이터를 업데이트 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-108">In earlier tutorials you learned how to read and update data using the synchronous programming model.</span></span> <span data-ttu-id="c270f-109">이 자습서는 비동기 프로그래밍 모델을 구현 하는 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-109">In this tutorial you see how to implement the asynchronous programming model.</span></span> <span data-ttu-id="c270f-110">비동기 코드는 더 나은 서버 리소스 사용 했기 때문에 더 잘 수행 하는 응용 프로그램을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-110">Asynchronous code can help an application perform better because it makes better use of server resources.</span></span>

<span data-ttu-id="c270f-111">이 자습서에서는 또한 삽입, 업데이트 및 삭제 작업 엔터티에 대 한 저장된 프로시저를 사용 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-111">In this tutorial you'll also see how to use stored procedures for insert, update, and delete operations on an entity.</span></span>

<span data-ttu-id="c270f-112">마지막으로 처음 배포한 이후 구현한 데이터베이스 변경 내용을 모든와 함께 azure에 응용 프로그램을 다시 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-112">Finally, you'll redeploy the application to Azure, along with all of the database changes that you've implemented since the first time you deployed.</span></span>

<span data-ttu-id="c270f-113">다음 그림에서는 사용할 일부 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-113">The following illustrations show some of the pages that you'll work with.</span></span>

![부서 페이지](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![부서를 만듭니다](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="why-bother-with-asynchronous-code"></a><span data-ttu-id="c270f-116">비동기 코드를 사용 하 여 굳이</span><span class="sxs-lookup"><span data-stu-id="c270f-116">Why bother with asynchronous code</span></span>

<span data-ttu-id="c270f-117">웹 서버에는 사용할 수 있는 스레드 수가 제한적이며, 로드 양이 많은 상황에서는 사용 가능한 모든 스레드가 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-117">A web server has a limited number of threads available, and in high load situations all of the available threads might be in use.</span></span> <span data-ttu-id="c270f-118">이 경우 서버는 스레드가 해제될 때까지 새 요청을 처리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-118">When that happens, the server can't process new requests until the threads are freed up.</span></span> <span data-ttu-id="c270f-119">동기 코드를 사용하면 I/O 완료를 대기하느라 작업을 실제로 수행하지 않는 동안에 많은 스레드가 정체될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-119">With synchronous code, many threads may be tied up while they aren't actually doing any work because they're waiting for I/O to complete.</span></span> <span data-ttu-id="c270f-120">비동기 코드를 사용하면 프로세스가 I/O 완료를 대기할 때 다른 요청을 처리하는 데 사용하도록 해당 스레드가 서버에서 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-120">With asynchronous code, when a process is waiting for I/O to complete, its thread is freed up for the server to use for processing other requests.</span></span> <span data-ttu-id="c270f-121">결과적으로, 비동기 코드를 사용 하면 서버 리소스를를 보다 효율적으로 사용 되며 서버 지연 없이 더 많은 트래픽을 처리할 수 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-121">As a result, asynchronous code enables server resources to be use more efficiently, and the server is enabled to handle more traffic without delays.</span></span>

<span data-ttu-id="c270f-122">.NET의 이전 버전에서 작성 하 고 비동기 코드를 테스트 된 복잡 한 오류가 발생 하기 쉽고, 디버깅 하기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-122">In earlier versions of .NET, writing and testing asynchronous code was complex, error prone, and hard to debug.</span></span> <span data-ttu-id="c270f-123">.NET 4.5 작성, 테스트 및 비동기 코드를 디버깅은 훨씬 쉬워졌기 때문에 한 이유가 없다면 없는 비동기 코드 일반적으로 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-123">In .NET 4.5, writing, testing, and debugging asynchronous code is so much easier that you should generally write asynchronous code unless you have a reason not to.</span></span> <span data-ttu-id="c270f-124">비동기 코드는 적은 양의 오버 헤드를 도입 하지만 트래픽이 낮은 상황의 성능 저하는 미미 합니다 하는 동안 트래픽이 높은 상황에서는 잠재적 성능 향상이 상당한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-124">Asynchronous code does introduce a small amount of overhead, but for low traffic situations the performance hit is negligible, while for high traffic situations, the potential performance improvement is substantial.</span></span>

<span data-ttu-id="c270f-125">비동기 프로그래밍에 대 한 자세한 내용은 참조 하세요. [호출을 차단 하지 않기 위해 사용 하 여.NET 4.5의 비동기 지원](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async)합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-125">For more information about asynchronous programming, see [Use .NET 4.5's async support to avoid blocking calls](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async).</span></span>

## <a name="create-the-department-controller"></a><span data-ttu-id="c270f-126">부서 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="c270f-126">Create the Department controller</span></span>

<span data-ttu-id="c270f-127">이 시간을 제외 하 고 이전 컨트롤러에 수행한 것과 동일한 방식으로 선택 하는 부서 컨트롤러를 만들려면 합니다 **사용 하 여 비동기 컨트롤러** 작업 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-127">Create a Department controller the same way you did the earlier controllers, except this time select the **Use async controller** actions check box.</span></span>

![부서 컨트롤러 스 캐 폴드](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="c270f-129">다음 강조 표시에 대 한 동기 코드에 추가 된 기능을 `Index` 메서드를 비동기:</span><span class="sxs-lookup"><span data-stu-id="c270f-129">The following highlights show what was added to the synchronous code for the `Index` method to make it asynchronous:</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=1,4)]

<span data-ttu-id="c270f-130">비동기적으로 실행 하는 Entity Framework 데이터베이스 쿼리를 사용 하도록 설정 하려면 네 가지 변경 내용이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-130">Four changes were applied to enable the Entity Framework database query to execute asynchronously:</span></span>

- <span data-ttu-id="c270f-131">메서드가 사용 하 여 표시 합니다 `async` 키워드는 컴파일러가 메서드 본문 부분에 대 한 콜백을 생성 하 고 자동으로 만들 수 있는 `Task<ActionResult>` 반환 되는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-131">The method is marked with the `async` keyword, which tells the compiler to generate callbacks for parts of the method body and to automatically create the `Task<ActionResult>` object that is returned.</span></span>
- <span data-ttu-id="c270f-132">반환 형식을 변경한 `ActionResult` 에 `Task<ActionResult>`입니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-132">The return type was changed from `ActionResult` to `Task<ActionResult>`.</span></span> <span data-ttu-id="c270f-133">합니다 `Task<T>` 형식을 나타내는 형식의 결과 사용 하 여 진행 중인 작업 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-133">The `Task<T>` type represents ongoing work with a result of type `T`.</span></span>
- <span data-ttu-id="c270f-134">`await` 키워드 웹 서비스 호출에 적용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-134">The `await` keyword was applied to the web service call.</span></span> <span data-ttu-id="c270f-135">컴파일러가이 키워드를 인식 하는 경우 백그라운드에서 해당 메서드를 두 부분으로 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-135">When the compiler sees this keyword, behind the scenes it splits the method into two parts.</span></span> <span data-ttu-id="c270f-136">첫 번째 부분은 비동기적으로 시작 되는 작업을 사용 하 여 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-136">The first part ends with the operation that is started asynchronously.</span></span> <span data-ttu-id="c270f-137">두 번째 부분은 작업이 완료 될 때 호출 되는 콜백 메서드에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-137">The second part is put into a callback method that is called when the operation completes.</span></span>
- <span data-ttu-id="c270f-138">비동기 버전을 `ToList` 확장 메서드가 호출 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-138">The asynchronous version of the `ToList` extension method was called.</span></span>

<span data-ttu-id="c270f-139">이유는 합니다 `departments.ToList` 문을 수정 하지만 `departments = db.Departments` 문을?</span><span class="sxs-lookup"><span data-stu-id="c270f-139">Why is the `departments.ToList` statement modified but not the `departments = db.Departments` statement?</span></span> <span data-ttu-id="c270f-140">이유는 쿼리 또는 명령을 데이터베이스를 전송할 수 있도록 하는 명령문만 비동기적으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-140">The reason is that only statements that cause queries or commands to be sent to the database are executed asynchronously.</span></span> <span data-ttu-id="c270f-141">`departments = db.Departments` 문은 쿼리 설정 되지만 쿼리 될 때까지 실행 되지 않습니다는 `ToList` 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-141">The `departments = db.Departments` statement sets up a query but the query is not executed until the `ToList` method is called.</span></span> <span data-ttu-id="c270f-142">따라서만 `ToList` 메서드를 비동기적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-142">Therefore, only the `ToList` method is executed asynchronously.</span></span>

<span data-ttu-id="c270f-143">에 `Details` 메서드 및 `HttpGet` `Edit` 하 고 `Delete` 메서드를 `Find` 메서드는 비동기적으로 실행 되는 메서드는 데이터베이스를 전송할 수 있도록 쿼리를 발생 시키는 것:</span><span class="sxs-lookup"><span data-stu-id="c270f-143">In the `Details` method and the `HttpGet` `Edit` and `Delete` methods, the `Find` method is the one that causes a query to be sent to the database, so that's the method that gets executed asynchronously:</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs?highlight=7)]

<span data-ttu-id="c270f-144">에 `Create`, `HttpPost Edit`, 및 `DeleteConfirmed` 메서드를 합니다 `SaveChanges` 실행할 명령을 발생 시키는 메서드 호출, 같은 문의 하지 `db.Departments.Add(department)` 엔터티 수정할 메모리에만 발생 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-144">In the `Create`, `HttpPost Edit`, and `DeleteConfirmed` methods, it is the `SaveChanges` method call that causes a command to be executed, not statements such as `db.Departments.Add(department)` which only cause entities in memory to be modified.</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=6)]

<span data-ttu-id="c270f-145">오픈 *Views\Department\Index.cshtml*, 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-145">Open *Views\Department\Index.cshtml*, and replace the template code with the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=3,5,20-22,36-38)]

<span data-ttu-id="c270f-146">이 코드 제목을 변경 하는 인덱스에서 부서, 관리자 이름 오른쪽으로 이동한 후 관리자의 전체 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-146">This code changes the title from Index to Departments, moves the Administrator name to the right, and provides the full name of the administrator.</span></span>

<span data-ttu-id="c270f-147">만들기, 삭제, 세부화, 고 뷰를 편집에 대 한 캡션을 변경는 `InstructorID` 필드를 "Administrator" 같은 방식으로 강좌 보기에 "부서"으로 부서 이름 필드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-147">In the Create, Delete, Details, and Edit views, change the caption for the `InstructorID` field to "Administrator" the same way you changed the department name field to "Department" in the Course views.</span></span>

<span data-ttu-id="c270f-148">뷰는 만들기 및 편집에 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-148">In the Create and Edit views use the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml)]

<span data-ttu-id="c270f-149">삭제 및 세부 정보 보기에서 다음 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-149">In the Delete and Details views use the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

<span data-ttu-id="c270f-150">응용 프로그램을 실행 하 고 클릭 합니다 **부서** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-150">Run the application, and click the **Departments** tab.</span></span>

![부서 페이지](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="c270f-152">모든 다른 컨트롤러와 동일 하 게 작동 하지만이 컨트롤러의 모든 SQL 쿼리는 비동기적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-152">Everything works the same as in the other controllers, but in this controller all of the SQL queries are executing asynchronously.</span></span>

<span data-ttu-id="c270f-153">Entity Framework를 사용한 비동기 프로그래밍을 사용할 때 알아야 할 몇 가지 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-153">Some things to be aware of when you are using asynchronous programming with the Entity Framework:</span></span>

- <span data-ttu-id="c270f-154">비동기 코드를 스레드로부터 안전 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-154">The async code is not thread safe.</span></span> <span data-ttu-id="c270f-155">즉, 즉, 하려고 하지 마세요 동일한 컨텍스트 인스턴스를 사용 하 여 병렬로 여러 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-155">In other words, in other words, don't try to do multiple operations in parallel using the same context instance.</span></span>
- <span data-ttu-id="c270f-156">비동기 코드의 성능 이점을 활용하려는 경우 사용 중인(예: 페이징) 라이브러리 패키지 또한 쿼리를 데이터베이스에 전송하도록 하는 Entity Framework 메서드를 호출하는 경우 비동기를 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-156">If you want to take advantage of the performance benefits of async code, make sure that any library packages that you're using (such as for paging), also use async if they call any Entity Framework methods that cause queries to be sent to the database.</span></span>

## <a name="use-stored-procedures-for-inserting-updating-and-deleting"></a><span data-ttu-id="c270f-157">삽입, 업데이트 및 삭제에 대 한 저장된 프로시저를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-157">Use stored procedures for inserting, updating, and deleting</span></span>

<span data-ttu-id="c270f-158">일부 개발자와 dba가 데이터베이스 액세스를 위한 저장된 프로시저를 사용 하려면.</span><span class="sxs-lookup"><span data-stu-id="c270f-158">Some developers and DBAs prefer to use stored procedures for database access.</span></span> <span data-ttu-id="c270f-159">이전 버전의 Entity Framework에서 저장된 프로시저를 사용 하 여 데이터를 검색할 수 있습니다 [원시 SQL 쿼리 실행](advanced-entity-framework-scenarios-for-an-mvc-web-application.md), 하지만 업데이트 작업에 대 한 저장된 프로시저를 사용 하는 EF를 지시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-159">In earlier versions of Entity Framework you can retrieve data using a stored procedure by [executing a raw SQL query](advanced-entity-framework-scenarios-for-an-mvc-web-application.md), but you can't instruct EF to use stored procedures for update operations.</span></span> <span data-ttu-id="c270f-160">EF 6에서 Code First 저장된 프로시저를 사용 하도록 구성 하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-160">In EF 6 it's easy to configure Code First to use stored procedures.</span></span>

1. <span data-ttu-id="c270f-161">*DAL\SchoolContext.cs*, 강조 표시 된 코드를 추가 하 여 `OnModelCreating` 메서드.</span><span class="sxs-lookup"><span data-stu-id="c270f-161">In *DAL\SchoolContext.cs*, add the highlighted code to the `OnModelCreating` method.</span></span>

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=9)]

    <span data-ttu-id="c270f-162">업데이트 및 삭제 작업에이 코드를 사용 하 여 저장 프로시저는 삽입, Entity Framework는 지시 된 `Department` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c270f-162">This code instructs Entity Framework to use stored procedures for insert, update, and delete operations on the `Department` entity.</span></span>
2. <span data-ttu-id="c270f-163">패키지 관리 콘솔에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-163">In Package Manage Console, enter the following command:</span></span>

    `add-migration DepartmentSP`

    <span data-ttu-id="c270f-164">오픈 *마이그레이션을\&l t; 타임 스탬프&gt;\_DepartmentSP.cs* 의 코드를 참조 하는 `Up` 만드는 메서드를 삽입, 업데이트 및 삭제 저장 프로시저:</span><span class="sxs-lookup"><span data-stu-id="c270f-164">Open *Migrations\&lt;timestamp&gt;\_DepartmentSP.cs* to see the code in the `Up` method that creates Insert, Update, and Delete stored procedures:</span></span>

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs?highlight=3-4,26-27,42-43)]
3. <span data-ttu-id="c270f-165">패키지 관리 콘솔에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-165">In Package Manage Console, enter the following command:</span></span>

     `update-database`
4. <span data-ttu-id="c270f-166">디버그 모드에서 응용 프로그램 실행을 클릭 합니다 **부서** 탭을 클릭 한 다음 **새로 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-166">Run the application in debug mode, click the **Departments** tab, and then click **Create New**.</span></span>
5. <span data-ttu-id="c270f-167">새 학과 대 한 데이터를 입력 한 다음 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-167">Enter data for a new department, and then click **Create**.</span></span>

     ![부서를 만듭니다](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
6. <span data-ttu-id="c270f-169">Visual Studio에서 로그를 확인 합니다 **출력** 창 새 부서 행을 삽입 하려면 저장된 프로시저를 사용 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-169">In Visual Studio, look at the logs in the **Output** window to see that a stored procedure was used to insert the new Department row.</span></span>

     ![부서 삽입 SP](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="c270f-171">코드는 먼저 기본 저장 프로시저 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-171">Code First creates default stored procedure names.</span></span> <span data-ttu-id="c270f-172">기존 데이터베이스를 사용 하는 경우 데이터베이스에 이미 정의 된 저장된 프로시저를 사용 하려면 저장된 프로시저 이름을 사용자 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-172">If you are using an existing database, you might need to customize the stored procedure names in order to use stored procedures already defined in the database.</span></span> <span data-ttu-id="c270f-173">그렇게 하는 방법에 대 한 정보를 참조 하세요 [Entity Framework 코드 첫 번째 Insert/Update/Delete 저장 프로시저](https://msdn.microsoft.com/data/dn468673)합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-173">For information about how to do that, see [Entity Framework Code First Insert/Update/Delete Stored Procedures](https://msdn.microsoft.com/data/dn468673).</span></span>

<span data-ttu-id="c270f-174">항목 생성 저장된 프로시저를 수행 하는 사용자 지정 하려는 경우 마이그레이션 스 캐 폴드 된 코드를 편집할 수 있습니다 `Up` 메서드는 저장된 프로시저를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-174">If you want to customize what generated stored procedures do, you can edit the scaffolded code for the migrations `Up` method that creates the stored procedure.</span></span> <span data-ttu-id="c270f-175">이런 방식으로 변경 내용이 반영 됩니다 때마다 마이그레이션 실행 하 고 마이그레이션 배포 된 후 프로덕션에서 자동으로 실행 될 때 프로덕션 데이터베이스에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-175">That way your changes are reflected whenever that migration is run and will be applied to your production database when migrations runs automatically in production after deployment.</span></span>

<span data-ttu-id="c270f-176">추가 마이그레이션 명령을 사용 하 여 새 마이그레이션을 생성 하 고 수동으로 호출 하는 코드를 작성할 수 마이그레이션 이전에 만든 기존 저장된 프로시저를 변경 하려는 경우는 [AlterStoredProcedure](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx) 메서드 .</span><span class="sxs-lookup"><span data-stu-id="c270f-176">If you want to change an existing stored procedure that was created in a previous migration, you can use the Add-Migration command to generate a blank migration, and then manually write code that calls the [AlterStoredProcedure](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx) method.</span></span>

## <a name="deploy-to-azure"></a><span data-ttu-id="c270f-177">Azure에 배포</span><span class="sxs-lookup"><span data-stu-id="c270f-177">Deploy to Azure</span></span>

<span data-ttu-id="c270f-178">이 섹션에서는 선택적 완료 해야 **Azure에 앱을 배포** 섹션을 [마이그레이션 및 배포](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md) 이 시리즈의 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-178">This section requires you to have completed the optional **Deploying the app to Azure** section in the [Migrations and Deployment](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial of this series.</span></span> <span data-ttu-id="c270f-179">로컬 프로젝트에서 데이터베이스를 삭제 하 여 해결 하는 마이그레이션 오류를 설치한 경우이 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-179">If you had migrations errors that you resolved by deleting the database in your local project, skip this section.</span></span>

1. <span data-ttu-id="c270f-180">Visual studio에서에서 프로젝트를 마우스 오른쪽 단추로 **솔루션 탐색기** 선택한 **게시** 상황에 맞는 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-180">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>
2. <span data-ttu-id="c270f-181">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-181">Click **Publish**.</span></span>

    <span data-ttu-id="c270f-182">Visual Studio에는 응용 프로그램을 azure에 배포 하 고 응용 프로그램이 Azure에서 실행 중인 기본 브라우저에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-182">Visual Studio deploys the application to Azure, and the application opens in your default browser, running in Azure.</span></span>
3. <span data-ttu-id="c270f-183">확인을 위해 응용 프로그램을 테스트 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-183">Test the application to verify it's working.</span></span>

    <span data-ttu-id="c270f-184">실행 하는 페이지는 처음에는 데이터베이스에 액세스, Entity Framework를 실행 하 여 마이그레이션의 모든 `Up` 데이터베이스를 현재 데이터 모델을 사용 하 여 최신 상태로 만드는 데 필요한 메서드.</span><span class="sxs-lookup"><span data-stu-id="c270f-184">The first time you run a page that accesses the database, the Entity Framework runs all of the migrations `Up` methods required to bring the database up to date with the current data model.</span></span> <span data-ttu-id="c270f-185">이제 마지막으로이 자습서에서 추가한 부서 페이지를 포함 하 여 배포한 이후에 추가 된 웹 페이지의 모든 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-185">You can now use all of the web pages that you added since the last time you deployed, including the Department pages that you added in this tutorial.</span></span>

## <a name="summary"></a><span data-ttu-id="c270f-186">요약</span><span class="sxs-lookup"><span data-stu-id="c270f-186">Summary</span></span>

<span data-ttu-id="c270f-187">이 자습서에서는 배웠습니다 비동기적으로 실행 되는 코드를 작성 하 여 서버 효율성을 개선 하는 방법에 대 한 저장된 프로시저를 사용 하는 방법을 삽입, 업데이트 및 삭제 작업.</span><span class="sxs-lookup"><span data-stu-id="c270f-187">In this tutorial you saw how to improve server efficiency by writing code that executes asynchronously, and how to use stored procedures for insert, update, and delete operations.</span></span> <span data-ttu-id="c270f-188">다음 자습서에서는 여러 사용자가 동시에 동일한 레코드를 편집 하려고 하는 경우 데이터 손실을 방지 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-188">In the next tutorial, you'll see how to prevent data loss when multiple users try to edit the same record at the same time.</span></span>

<span data-ttu-id="c270f-189">다른 Entity Framework 리소스에 대 한 링크에서 찾을 수 있습니다 합니다 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c270f-189">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c270f-190">[이전](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [다음](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="c270f-190">[Previous](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>
