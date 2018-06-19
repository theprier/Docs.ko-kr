---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: 엔터티 프레임 워크 시나리오 MVC 웹 응용 프로그램 (10 / 10)에 대 한 고급 | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: 64906a1d-f734-41cf-9615-ee95f8740996
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: 277503b65d9b75a9d3cc05538d5327f9367f45e0
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30876711"
---
<a name="advanced-entity-framework-scenarios-for-an-mvc-web-application-10-of-10"></a><span data-ttu-id="586d4-103">MVC 웹 응용 프로그램 (10 / 10)에 대 한 고급 엔터티 프레임 워크 시나리오</span><span class="sxs-lookup"><span data-stu-id="586d4-103">Advanced Entity Framework Scenarios for an MVC Web Application (10 of 10)</span></span>
====================
<span data-ttu-id="586d4-104">으로 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="586d4-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="586d4-105">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="586d4-106">Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio 2012를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="586d4-107">자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="586d4-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="586d4-108">시작 부분에서 자습서 시리즈를 시작할 수 있습니다 또는 [이 장의 대 한 시작 프로젝트 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 여기에서 시작 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="586d4-109">해결할 수 없는 문제에 직면 하는 경우 [완료 장 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 문제를 재현 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="586d4-110">일반적으로 코드 완성 된 코드를 비교 하 여 문제에 솔루션을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="586d4-111">몇 가지 일반적인 오류 및 해결 하는 방법에 대 한 참조 [오류 및 해결 방법입니다.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="586d4-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>


<span data-ttu-id="586d4-112">이전 자습서에서 리포지토리 및 작업 패턴의 단위를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-112">In the previous tutorial you implemented the repository and unit of work patterns.</span></span> <span data-ttu-id="586d4-113">이 자습서는 다음 항목을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-113">This tutorial covers the following topics:</span></span>

- <span data-ttu-id="586d4-114">원시 SQL 쿼리를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-114">Performing raw SQL queries.</span></span>
- <span data-ttu-id="586d4-115">No 추적 쿼리를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-115">Performing no-tracking queries.</span></span>
- <span data-ttu-id="586d4-116">쿼리를 검사 하는 데이터베이스에 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-116">Examining queries sent to the database.</span></span>
- <span data-ttu-id="586d4-117">프록시 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-117">Working with proxy classes.</span></span>
- <span data-ttu-id="586d4-118">변경 내용 자동으로 검색을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-118">Disabling automatic detection of changes.</span></span>
- <span data-ttu-id="586d4-119">변경 저장할 때 유효성 검사를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-119">Disabling validation when saving changes.</span></span>
- [<span data-ttu-id="586d4-120">오류 및 해결</span><span class="sxs-lookup"><span data-stu-id="586d4-120">Errors and Work Arounds</span></span>](#errors)

<span data-ttu-id="586d4-121">다음이 항목 중 대부분의 경우 이미 만든 페이지를 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-121">For most of these topics, you'll work with pages that you already created.</span></span> <span data-ttu-id="586d4-122">원시 SQL 대량 업데이트 수행을 사용 하는 데이터베이스의 모든 과정의 크레딧의 수를 업데이트 하는 새 페이지를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-122">To use raw SQL to do bulk updates you'll create a new page that updates the number of credits of all courses in the database:</span></span>

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

<span data-ttu-id="586d4-124">와 아니요 추적 쿼리를 사용 하는 부서 편집 페이지를 새 유효성 검사 논리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-124">And to use a no-tracking query you'll add new validation logic to the Department Edit page:</span></span>

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image2.png)

## <a name="performing-raw-sql-queries"></a><span data-ttu-id="586d4-126">성능 원시 SQL 쿼리</span><span class="sxs-lookup"><span data-stu-id="586d4-126">Performing Raw SQL Queries</span></span>

<span data-ttu-id="586d4-127">엔터티 프레임 워크 코드의 첫 번째 API에는 SQL 명령을 데이터베이스에 직접 전달할 수 있도록 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-127">The Entity Framework Code First API includes methods that enable you to pass SQL commands directly to the database.</span></span> <span data-ttu-id="586d4-128">다음과 같은 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-128">You have the following options:</span></span>

- <span data-ttu-id="586d4-129">엔터티 형식을 반환하는 쿼리에 `DbSet.SqlQuery` 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-129">Use the `DbSet.SqlQuery` method for queries that return entity types.</span></span> <span data-ttu-id="586d4-130">반환 된 개체에 필요한 형식 이어야 합니다는 `DbSet` 있으며 개체를 자동으로 추적 됩니다는 데이터베이스 컨텍스트에서 해제 하지 않으면 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-130">The returned objects must be of the type expected by the `DbSet` object, and they are automatically tracked by the database context unless you turn tracking off.</span></span> <span data-ttu-id="586d4-131">(다음 섹션에 대 한 참조는 `AsNoTracking` 메서드.)</span><span class="sxs-lookup"><span data-stu-id="586d4-131">(See the following section about the `AsNoTracking` method.)</span></span>
- <span data-ttu-id="586d4-132">사용 하 여는 `Database.SqlQuery` 엔터티 지원 하지 않는 형식을 반환 하는 쿼리에 메서드.</span><span class="sxs-lookup"><span data-stu-id="586d4-132">Use the `Database.SqlQuery` method for queries that return types that aren't entities.</span></span> <span data-ttu-id="586d4-133">이 메서드를 사용하여 엔터티 형식을 검색하더라도 반환된 데이터는 데이터베이스 컨텍스트에 의해 추적되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-133">The returned data isn't tracked by the database context, even if you use this method to retrieve entity types.</span></span>
- <span data-ttu-id="586d4-134">사용 하 여 [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456(v=vs.103).aspx) 쿼리가 아닌 명령에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-134">Use the [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456(v=vs.103).aspx) for non-query commands.</span></span>

<span data-ttu-id="586d4-135">Entity Framework를 사용할 때 장점 중 하나는 코드가 데이터를 저장하는 특정 메서드에 너무 얽매이지 않아도 된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-135">One of the advantages of using the Entity Framework is that it avoids tying your code too closely to a particular method of storing data.</span></span> <span data-ttu-id="586d4-136">이것은 사용자를 위한 SQL 쿼리와 명령이 생성되므로 가능하며 사용자는 코드를 직접 작성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-136">It does this by generating SQL queries and commands for you, which also frees you from having to write them yourself.</span></span> <span data-ttu-id="586d4-137">하지만 예외적인 시나리오 수동으로 만든 특정 SQL 쿼리를 실행 해야 할 때 있으며 이러한 방법을 원활 하 게 이러한 예외를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-137">But there are exceptional scenarios when you need to run specific SQL queries that you have manually created, and these methods make it possible for you to handle such exceptions.</span></span>

<span data-ttu-id="586d4-138">웹 응용 프로그램에서 SQL 명령을 실행할 때 항상 그렇듯이 SQL 삽입 공격으로부터 사이트를 보호하기 위한 예방 조치를 취해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-138">As is always true when you execute SQL commands in a web application, you must take precautions to protect your site against SQL injection attacks.</span></span> <span data-ttu-id="586d4-139">이를 수행하는 한 가지 방법은 매개 변수가 있는 쿼리를 사용하여 웹 페이지에서 제출한 문자열을 SQL 명령으로 해석할 수 없도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-139">One way to do that is to use parameterized queries to make sure that strings submitted by a web page can't be interpreted as SQL commands.</span></span> <span data-ttu-id="586d4-140">이 자습서에서는 사용자 입력을 쿼리에 통합할 때 매개 변수가 있는 쿼리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-140">In this tutorial you'll use parameterized queries when integrating user input into a query.</span></span>

### <a name="calling-a-query-that-returns-entities"></a><span data-ttu-id="586d4-141">엔터티를 반환 하는 쿼리 호출</span><span class="sxs-lookup"><span data-stu-id="586d4-141">Calling a Query that Returns Entities</span></span>

<span data-ttu-id="586d4-142">한다고 가정은 `GenericRepository` 클래스 추가 필터링 및 추가 방법으로 파생된 클래스를 만들 필요 없이 유연성 정렬를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-142">Suppose you want the `GenericRepository` class to provide additional filtering and sorting flexibility without requiring that you create a derived class with additional methods.</span></span> <span data-ttu-id="586d4-143">이 위해 한 가지 방법은 SQL 쿼리를 허용 하는 메서드를 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-143">One way to achieve that would be to add a method that accepts a SQL query.</span></span> <span data-ttu-id="586d4-144">와 같은 모든 종류의 필터링 또는 정렬 하는 컨트롤러에서 원하는 지정할 수 있습니다는 `Where` 절에는 조인 또는 하위 쿼리에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-144">You could then specify any kind of filtering or sorting you want in the controller, such as a `Where` clause that depends on a joins or a subquery.</span></span> <span data-ttu-id="586d4-145">이 섹션에서는 이러한 메서드를 구현 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-145">In this section you'll see how to implement such a method.</span></span>

<span data-ttu-id="586d4-146">만들기는 `GetWithRawSql` 메서드에 다음 코드를 추가 하 여 *GenericRepository.cs*:</span><span class="sxs-lookup"><span data-stu-id="586d4-146">Create the `GetWithRawSql` method by adding the following code to *GenericRepository.cs*:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs)]

<span data-ttu-id="586d4-147">*CourseController.cs*에서 새 메서드를 호출 하는 `Details` 메서드를 다음 예제와 같이:</span><span class="sxs-lookup"><span data-stu-id="586d4-147">In *CourseController.cs*, call the new method from the `Details` method, as shown in the following example:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

<span data-ttu-id="586d4-148">이 경우 있습니다 사용할 수도 `GetByID` 수 있지만 메서드를 사용 하는 `GetWithRawSql` 되었는지 확인 하는 메서드는 `GetWithRawSQL` 메서드 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-148">In this case you could have used the `GetByID` method, but you're using the `GetWithRawSql` method to verify that the `GetWithRawSQL` method works.</span></span>

<span data-ttu-id="586d4-149">Select 쿼리 작동을 확인 하려면 세부 정보 페이지를 실행 (선택 된 **과정** 탭 한 다음 **세부 정보** 하나의 과정에 대 한).</span><span class="sxs-lookup"><span data-stu-id="586d4-149">Run the Details page to verify that the select query works (select the **Course** tab and then **Details** for one course).</span></span>

![Course_Details_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image3.png)

### <a name="calling-a-query-that-returns-other-types-of-objects"></a><span data-ttu-id="586d4-151">다른 형식의 개체를 반환 하는 쿼리 호출</span><span class="sxs-lookup"><span data-stu-id="586d4-151">Calling a Query that Returns Other Types of Objects</span></span>

<span data-ttu-id="586d4-152">이전에 등록 날짜별로 학생 수를 보여주는 [정보] 페이지의 학생 통계 표를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-152">Earlier you created a student statistics grid for the About page that showed the number of students for each enrollment date.</span></span> <span data-ttu-id="586d4-153">이 작업을 수행 하는 코드 *HomeController.cs* LINQ를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="586d4-153">The code that does this in *HomeController.cs* uses LINQ:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs)]

<span data-ttu-id="586d4-154">LINQ를 사용 하는 것이 아니라 SQL에서 직접이 데이터는 코드를 작성 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-154">Suppose you want to write the code that retrieves this data directly in SQL rather than using LINQ.</span></span> <span data-ttu-id="586d4-155">엔터티 개체 이외의 형식을 반환 하는 쿼리를 실행 해야 할 즉 사용 해야는 `Database.SqlQuery` 메서드.</span><span class="sxs-lookup"><span data-stu-id="586d4-155">To do that you need to run a query that returns something other than entity objects, which means you need to use the `Database.SqlQuery` method.</span></span>

<span data-ttu-id="586d4-156">*HomeController.cs*에서 LINQ 문을 대체는 `About` 메서드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="586d4-156">In *HomeController.cs*, replace the LINQ statement in the `About` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

<span data-ttu-id="586d4-157">정보 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-157">Run the About page.</span></span> <span data-ttu-id="586d4-158">이전과 동일한 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-158">It displays the same data it did before.</span></span>

![About_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image4.png)

### <a name="calling-an-update-query"></a><span data-ttu-id="586d4-160">업데이트 쿼리를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-160">Calling an Update Query</span></span>

<span data-ttu-id="586d4-161">Contoso 대학 관리자가 모든 과정에 대 한 크레딧의 수를 변경 하는 등 데이터베이스에 대량 변경 내용이 수행 하 려 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-161">Suppose Contoso University administrators want to be able to perform bulk changes in the database, such as changing the number of credits for every course.</span></span> <span data-ttu-id="586d4-162">대학에 과목이 많은 경우 엔터티로 모두 검색하여 개별적으로 변경하는 것은 비효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-162">If the university has a large number of courses, it would be inefficient to retrieve them all as entities and change them individually.</span></span> <span data-ttu-id="586d4-163">이 섹션에는 모든 과정에 대 한 크레딧의 수를 변경 하는 인수를 지정할 수 있도록 하는 웹 페이지를 구현 하 고 SQL을 실행 하 여 변경 내용을 지정 `UPDATE` 문.</span><span class="sxs-lookup"><span data-stu-id="586d4-163">In this section you'll implement a web page that allows the user to specify a factor by which to change the number of credits for all courses, and you'll make the change by executing a SQL `UPDATE` statement.</span></span> <span data-ttu-id="586d4-164">그러면 웹 페이지가 다음 그림과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-164">The web page will look like the following illustration:</span></span>

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image5.png)

<span data-ttu-id="586d4-166">이전 자습서 읽고 업데이트 하는 일반 저장소 사용 `Course` 의 엔터티는 `Course` 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-166">In the previous tutorial you used the generic repository to read and update `Course` entities in the `Course` controller.</span></span> <span data-ttu-id="586d4-167">이 대량 업데이트 작업에 대 한 일반 저장소에 없는 새 저장소 메서드를 만들 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-167">For this bulk update operation, you need to create a new repository method that isn't in the generic repository.</span></span> <span data-ttu-id="586d4-168">이렇게 하려면 전용 만들게 `CourseRepository` 클래스에서 파생 되는 `GenericRepository` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-168">To do that, you'll create a dedicated `CourseRepository` class that derives from the `GenericRepository` class.</span></span>

<span data-ttu-id="586d4-169">에 *DAL* 폴더를 만들 *CourseRepository.cs* 기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-169">In the *DAL* folder, create *CourseRepository.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cs)]

<span data-ttu-id="586d4-170">*UnitOfWork.cs*, 변경 된 `Course` 에서 저장소 유형을 `GenericRepository<Course>` 를 `CourseRepository:`</span><span class="sxs-lookup"><span data-stu-id="586d4-170">In *UnitOfWork.cs*, change the `Course` repository type from `GenericRepository<Course>` to `CourseRepository:`</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.cs)]

<span data-ttu-id="586d4-171">*CourseContoller.cs*, 추가 `UpdateCourseCredits` 메서드:</span><span class="sxs-lookup"><span data-stu-id="586d4-171">In *CourseContoller.cs*, add an `UpdateCourseCredits` method:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

<span data-ttu-id="586d4-172">이 메서드는 둘 다에 대해 `HttpGet` 및 `HttpPost`합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-172">This method will be used for both `HttpGet` and `HttpPost`.</span></span> <span data-ttu-id="586d4-173">때는 `HttpGet` `UpdateCourseCredits` 메서드가 실행 된 `multiplier` 변수는 null이 됩니다 하 고 앞의 그림에 나와 있는 것 처럼 보기는 빈 텍스트 상자 및 전송 단추에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-173">When the `HttpGet` `UpdateCourseCredits` method runs, the `multiplier` variable will be null and the view will display an empty text box and a submit button, as shown in the preceding illustration.</span></span>

<span data-ttu-id="586d4-174">경우는 **업데이트** 단추를 클릭 하면 및 `HttpPost` 메서드 실행 `multiplier` 텍스트 상자에 입력 된 값을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-174">When the **Update** button is clicked and the `HttpPost` method runs, `multiplier` will have the value entered in the text box.</span></span> <span data-ttu-id="586d4-175">저장소 호출 `UpdateCourseCredits` 영향을 받는 행, 수를 반환 하 고 해당 값에 저장 되는 `ViewBag` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-175">The code then calls the repository `UpdateCourseCredits` method, which returns the number of affected rows, and that value is stored in the `ViewBag` object.</span></span> <span data-ttu-id="586d4-176">보기의 영향을 받는 행 수를 받을 때의 `ViewBag` 개체를 텍스트 상자 대신 해당 숫자를 표시 하 고 다음 그림에 나와 있는 것 처럼 전송 단추를:</span><span class="sxs-lookup"><span data-stu-id="586d4-176">When the view receives the number of affected rows in the `ViewBag` object, it displays that number instead of the text box and submit button, as shown in the following illustration:</span></span>

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image6.png)

<span data-ttu-id="586d4-178">보기 만들기는 *Views\Course* 업데이트 과정 크레딧 페이지에 대 한 폴더:</span><span class="sxs-lookup"><span data-stu-id="586d4-178">Create a view in the *Views\Course* folder for the Update Course Credits page:</span></span>

![Add_View_dialog_box_for_Update_Course_Credits](https://asp.net/media/2578203/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Add_View_dialog_box_for_Update_Course_Credits.png)

<span data-ttu-id="586d4-180">*Views\Course\UpdateCourseCredits.cshtml*, 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-180">In *Views\Course\UpdateCourseCredits.cshtml*, replace the template code with the following code:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

<span data-ttu-id="586d4-181">**Courses(과정)** 탭을 선택하여 `UpdateCourseCredits` 메서드를 실행한 후 브라우저의 주소 표시줄에서 URL 끝에 "/UpdateCourseCredits"를 추가합니다(예: `http://localhost:50205/Course/UpdateCourseCredits`).</span><span class="sxs-lookup"><span data-stu-id="586d4-181">Run the `UpdateCourseCredits` method by selecting the **Courses** tab, then adding "/UpdateCourseCredits" to the end of the URL in the browser's address bar (for example: `http://localhost:50205/Course/UpdateCourseCredits`).</span></span> <span data-ttu-id="586d4-182">텍스트 상자에 숫자를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-182">Enter a number in the text box:</span></span>

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image7.png)

<span data-ttu-id="586d4-184">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-184">Click **Update**.</span></span> <span data-ttu-id="586d4-185">영향을 받은 행 수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-185">You see the number of rows affected:</span></span>

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image8.png)

<span data-ttu-id="586d4-187">학점 수가 수정된 과정 목록을 보려면 **목록으로 돌아가기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-187">Click **Back to List** to see the list of courses with the revised number of credits.</span></span>

![Courses_Index_page_showing_revised_credits](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image9.png)

<span data-ttu-id="586d4-189">원시 SQL 쿼리 하는 방법에 대 한 자세한 내용은 참조 [원시 SQL 쿼리](https://blogs.msdn.com/b/adonet/archive/2011/02/04/using-dbcontext-in-ef-feature-ctp5-part-10-raw-sql-queries.aspx) Entity Framework 팀 블로그.</span><span class="sxs-lookup"><span data-stu-id="586d4-189">For more information about raw SQL queries, see [Raw SQL Queries](https://blogs.msdn.com/b/adonet/archive/2011/02/04/using-dbcontext-in-ef-feature-ctp5-part-10-raw-sql-queries.aspx) on the Entity Framework team blog.</span></span>

## <a name="no-tracking-queries"></a><span data-ttu-id="586d4-190">No 추적 쿼리</span><span class="sxs-lookup"><span data-stu-id="586d4-190">No-Tracking Queries</span></span>

<span data-ttu-id="586d4-191">데이터베이스 컨텍스트 데이터베이스 행을 검색 하 고을 나타내는 엔터티 개체를 만드는 경우 기본적으로를 추적 데이터베이스에 포함 된 내용으로 메모리에 엔터티 동기화 되었는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-191">When a database context retrieves database rows and creates entity objects that represent them, by default it keeps track of whether the entities in memory are in sync with what's in the database.</span></span> <span data-ttu-id="586d4-192">메모리의 데이터는 캐시의 역할을 하고 엔터티를 업데이트할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-192">The data in memory acts as a cache and is used when you update an entity.</span></span> <span data-ttu-id="586d4-193">컨텍스트 인스턴스는 일반적으로 수명이 짧으며(각 요청에 대해 새 것이 만들어지고 삭제됨) 엔터티를 읽는 컨텍스트는 일반적으로 해당 엔터티가 다시 사용되기 전에 삭제되므로 이 캐싱은 웹 응용 프로그램에 종종 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-193">This caching is often unnecessary in a web application because context instances are typically short-lived (a new one is created and disposed for each request) and the context that reads an entity is typically disposed before that entity is used again.</span></span>

<span data-ttu-id="586d4-194">컨텍스트를 사용 하 여 쿼리에 대 한 엔터티 개체를 추적 하는지 여부를 지정할 수는 `AsNoTracking` 메서드.</span><span class="sxs-lookup"><span data-stu-id="586d4-194">You can specify whether the context tracks entity objects for a query by using the `AsNoTracking` method.</span></span> <span data-ttu-id="586d4-195">이러한 작업을 수행할 수 있는 일반적인 시나리오는 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-195">Typical scenarios in which you might want to do that include the following:</span></span>

- <span data-ttu-id="586d4-196">쿼리 추적을 해제 성능을 눈에 띄게 향상 시킬 수 있는 데이터의 큰 볼륨을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-196">The query retrieves such a large volume of data that turning off tracking might noticeably enhance performance.</span></span>
- <span data-ttu-id="586d4-197">업데이트 하려면 엔터티를 연결 하려고 하지만 이전 다른 목적을 위해 동일한 엔터티를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-197">You want to attach an entity in order to update it, but you earlier retrieved the same entity for a different purpose.</span></span> <span data-ttu-id="586d4-198">엔터티는 데이터베이스 컨텍스트에서 이미 추적 중이므로 변경하려는 엔터티를 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-198">Because the entity is already being tracked by the database context, you can't attach the entity that you want to change.</span></span> <span data-ttu-id="586d4-199">이를 방지 하는 한 가지 방법은 사용 하는 것은 `AsNoTracking` 이전 쿼리를 사용 하는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-199">One way to prevent this from happening is to use the `AsNoTracking` option with the earlier query.</span></span>

<span data-ttu-id="586d4-200">이 섹션에서는 이러한 시나리오의 두 번째를 보여 주는 비즈니스 논리를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-200">In this section you'll implement business logic that illustrates the second of these scenarios.</span></span> <span data-ttu-id="586d4-201">구체적으로 비즈니스 규칙을 강사 둘 이상의 부서 관리자는 사용할 수 없습니다 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-201">Specifically, you'll enforce a business rule that says that an instructor can't be the administrator of more than one department.</span></span>

<span data-ttu-id="586d4-202">*DepartmentController.cs*에서 호출할 수 있는 새 메서드를 추가 하는 `Edit` 및 `Create` 없는 두 부서 동일한 관리자가 있는지 확인 하는 메서드:</span><span class="sxs-lookup"><span data-stu-id="586d4-202">In *DepartmentController.cs*, add a new method that you can call from the `Edit` and `Create` methods to make sure that no two departments have the same administrator:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.cs)]

<span data-ttu-id="586d4-203">코드를 추가 `try` 블록은 `HttpPost` `Edit` 메서드를 유효성 검사 오류가 없는 경우이 새 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-203">Add code in the `try` block of the `HttpPost` `Edit` method to call this new method if there are no validation errors.</span></span> <span data-ttu-id="586d4-204">`try` 블록은 이제 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-204">The `try` block now looks like the following example:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample11.cs?highlight=9-12)]

<span data-ttu-id="586d4-205">부서 편집 페이지를 실행 하는 부서 관리자를 다른 부서 관리자는 이미 강사를 변경 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-205">Run the Department Edit page and try to change a department's administrator to an instructor who is already the administrator of a different department.</span></span> <span data-ttu-id="586d4-206">예상 되는 오류 메시지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-206">You get the expected error message:</span></span>

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

<span data-ttu-id="586d4-208">이제 부서 편집 페이지 다시 고이 시간 변경 실행는 **예산** 양입니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-208">Now run the Department Edit page again and this time change the **Budget** amount.</span></span> <span data-ttu-id="586d4-209">클릭할 때 **저장**, 오류 페이지를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="586d4-209">When you click **Save**, you see an error page:</span></span>

![Department_Edit_page_with_object_state_manager_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image11.png)

<span data-ttu-id="586d4-211">예외 오류 메시지는 "`An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key.`" 이러한 다음과 같은 이벤트 순서가 때문에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-211">The exception error message is "`An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key.`" This happened because of the following sequence of events:</span></span>

- <span data-ttu-id="586d4-212">`Edit` 메서드 호출에서 `ValidateOneAdministratorAssignmentPerInstructor` Kim 손 자신의 관리자 권한으로이 있는 모든 department를 검색 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="586d4-212">The `Edit` method calls the `ValidateOneAdministratorAssignmentPerInstructor` method, which retrieves all departments that have Kim Abercrombie as their administrator.</span></span> <span data-ttu-id="586d4-213">읽을 영어 부서가 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-213">That causes the English department to be read.</span></span> <span data-ttu-id="586d4-214">편집 중인 부서, 이기 때문에 오류가 보고 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-214">Because that's the department being edited, no error is reported.</span></span> <span data-ttu-id="586d4-215">하지만이 읽기 작업의 결과로 데이터베이스에서 읽은 영어 부서 엔터티에 이제 추적 되 고 데이터베이스 컨텍스트에 의해 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-215">As a result of this read operation, however, the English department entity that was read from the database is now being tracked by the database context.</span></span>
- <span data-ttu-id="586d4-216">`Edit` 메서드 설정 하려고 시도 `Modified` 의 영어에 대 한 플래그 부서 엔터티에 MVC 모델 바인더를 통해 만들어지지만 컨텍스트 영어 부서에 대 한 엔터티를 이미 추적 하는 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-216">The `Edit` method tries to set the `Modified` flag on the English department entity created by the MVC model binder, but that fails because the context is already tracking an entity for the English department.</span></span>

<span data-ttu-id="586d4-217">이 문제에 대 한 한 가지 해결 메모리 부서 엔터티 유효성 검사 쿼리로 검색 된 추적에서 컨텍스트를 유지 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-217">One solution to this problem is to keep the context from tracking in-memory department entities retrieved by the validation query.</span></span> <span data-ttu-id="586d4-218">이 엔터티를 업데이트 하지 않습니다 하기 때문에이 수행 하거나 메모리에 캐시 되 고 그 이점을 얻을 수 있는 방식으로 다시 읽는 없습니다 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-218">There's no disadvantage to doing this, because you won't be updating this entity or reading it again in a way that would benefit from it being cached in memory.</span></span>

<span data-ttu-id="586d4-219">*DepartmentController.cs*에 `ValidateOneAdministratorAssignmentPerInstructor` 메서드를 다음에 표시 된 대로 없는 추적을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-219">In *DepartmentController.cs*, in the `ValidateOneAdministratorAssignmentPerInstructor` method, specify no tracking, as shown in the following:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample12.cs?highlight=4)]

<span data-ttu-id="586d4-220">편집 하려는 시도 반복 하는 **예산** 부서입니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-220">Repeat your attempt to edit the **Budget** amount of a department.</span></span> <span data-ttu-id="586d4-221">이 시간 후 작업을 성공 하 고 수정 된 예산 값을 보여 주는 부서 인덱스 페이지에 예상 대로 사이트를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-221">This time the operation is successful, and the site returns as expected to the Departments Index page, showing the revised budget value.</span></span>

## <a name="examining-queries-sent-to-the-database"></a><span data-ttu-id="586d4-222">데이터베이스에 전송 하는 쿼리</span><span class="sxs-lookup"><span data-stu-id="586d4-222">Examining Queries Sent to the Database</span></span>

<span data-ttu-id="586d4-223">때로는 데이터베이스로 전송된 실제 SQL 쿼리를 볼 수 있는 것이 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-223">Sometimes it's helpful to be able to see the actual SQL queries that are sent to the database.</span></span> <span data-ttu-id="586d4-224">이렇게 하려면 디버거에서 쿼리 변수를 검사 하거나 쿼리를 호출할 수 있습니다 `ToString` 메서드.</span><span class="sxs-lookup"><span data-stu-id="586d4-224">To do this, you can examine a query variable in the debugger or call the query's `ToString` method.</span></span> <span data-ttu-id="586d4-225">이렇게 해 보려면 단순 쿼리를 확인 하 고 이러한 eager 로드, 필터링 및 정렬 옵션을 추가할 때를 어떻게 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-225">To try this out, you'll look at a simple query and then look at what happens to it as you add options such eager loading, filtering, and sorting.</span></span>

<span data-ttu-id="586d4-226">*컨트롤러/CourseController*, 대체 된 `Index` 메서드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="586d4-226">In *Controllers/CourseController*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample13.cs?highlight=3)]

<span data-ttu-id="586d4-227">이제에 중단점을 설정 *GenericRepository.cs* 에 `return query.ToList();` 및 `return orderBy(query).ToList();` 설명의는 `Get` 메서드.</span><span class="sxs-lookup"><span data-stu-id="586d4-227">Now set a breakpoint in *GenericRepository.cs* on the `return query.ToList();` and the `return orderBy(query).ToList();` statements of the `Get` method.</span></span> <span data-ttu-id="586d4-228">디버그 모드에서 프로젝트를 실행 하 고 과정 인덱스 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-228">Run the project in debug mode and select the Course Index page.</span></span> <span data-ttu-id="586d4-229">코드에서 중단점에 도달 하면 검사는 `query` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-229">When the code reaches the breakpoint, examine the `query` variable.</span></span> <span data-ttu-id="586d4-230">SQL Server로 전송 하는 쿼리를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-230">You see the query that's sent to SQL Server.</span></span> <span data-ttu-id="586d4-231">단순 `Select` 문:</span><span class="sxs-lookup"><span data-stu-id="586d4-231">It's a simple `Select` statement:</span></span>

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample14.json)]

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

<span data-ttu-id="586d4-232">쿼리는 너무 길어 Visual Studio에서 디버깅 창에 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-232">Queries can be too long to display in the debugging windows in Visual Studio.</span></span> <span data-ttu-id="586d4-233">전체 쿼리를 확인 하려면 변수 값 복사한 텍스트 편집기에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-233">To see the entire query, you can copy the variable value and paste it into a text editor:</span></span>

![Copy_value_of_variable_in_debug_mode](https://asp.net/media/2578239/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Copy_value_of_variable_in_debug_mode_0902a2b1-b799-47a6-9b4b-f266c79d83c1.png)

<span data-ttu-id="586d4-235">이제 사용자가 특정 부서에 필터링 할 수 있도록 과정 인덱스 페이지에 드롭 다운 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-235">Now you'll add a drop-down list to the Course Index page so that users can filter for a particular department.</span></span> <span data-ttu-id="586d4-236">코스 제목별으로 정렬 하 고 즉시 로드에 대 한을 지정 합니다는 `Department` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-236">You'll sort the courses by title, and you'll specify eager loading for the `Department` navigation property.</span></span> <span data-ttu-id="586d4-237">*CourseController.cs*, 대체 된 `Index` 메서드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="586d4-237">In *CourseController.cs*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample15.cs)]

<span data-ttu-id="586d4-238">드롭다운 목록에서 선택한 값을 받습니다. 메서드는 `SelectedDepartment` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-238">The method receives the selected value of the drop-down list in the `SelectedDepartment` parameter.</span></span> <span data-ttu-id="586d4-239">어떤 영역도 선택 하는 경우이 매개 변수가 null이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-239">If nothing is selected, this parameter will be null.</span></span>

<span data-ttu-id="586d4-240">A `SelectList` 드롭 다운 목록에 대 한 모든 부서가 포함 된 컬렉션 뷰에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-240">A `SelectList` collection containing all departments is passed to the view for the drop-down list.</span></span> <span data-ttu-id="586d4-241">에 전달 된 매개 변수는 `SelectList` 생성자 값 필드 이름, 텍스트 필드 이름 및 선택한 항목을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-241">The parameters passed to the `SelectList` constructor specify the value field name, the text field name, and the selected item.</span></span>

<span data-ttu-id="586d4-242">에 대 한는 `Get` 의 메서드는 `Course` 필터 식, 정렬 순서 및에 대 한 로드 eager 리포지토리, 코드를 지정 된 `Department` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-242">For the `Get` method of the `Course` repository, the code specifies a filter expression, a sort order, and eager loading for the `Department` navigation property.</span></span> <span data-ttu-id="586d4-243">필터 식에는 항상 반환 `true` 드롭 다운 목록에서 아무것도 선택 하는 경우 (즉, `SelectedDepartment` null).</span><span class="sxs-lookup"><span data-stu-id="586d4-243">The filter expression always returns `true` if nothing is selected in the drop-down list (that is, `SelectedDepartment` is null).</span></span>

<span data-ttu-id="586d4-244">*Views\Course\Index.cshtml*, 열기 바로 앞 `table` 태그에 다음 코드를 추가 드롭 다운 목록 및 전송 단추를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-244">In *Views\Course\Index.cshtml*, immediately before the opening `table` tag, add the following code to create the drop-down list and a submit button:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample16.cshtml)]

<span data-ttu-id="586d4-245">여전히 설정 된 중단점과 `GenericRepository` 과정 인덱스 페이지를 실행 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-245">With the breakpoints still set in the `GenericRepository` class, run the Course Index page.</span></span> <span data-ttu-id="586d4-246">페이지를 브라우저에 표시 되도록 코드 중단점에 도달 하는 처음 두 번까지 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-246">Continue through the first two times that the code hits a breakpoint, so that the page is displayed in the browser.</span></span> <span data-ttu-id="586d4-247">부서 드롭 다운 목록에서 선택 하 고 클릭 **필터**:</span><span class="sxs-lookup"><span data-stu-id="586d4-247">Select a department from the drop-down list and click **Filter**:</span></span>

![Course_Index_page_with_department_selected](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

<span data-ttu-id="586d4-249">이 이번 드롭 다운 목록에 대 한 부서 쿼리에 대 한 첫 번째 중단점이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-249">This time the first breakpoint will be for the departments query for the drop-down list.</span></span> <span data-ttu-id="586d4-250">생략 하 고 보기는 `query` 변수 다음에 코드 중단점에 도달 하면는 기능을 확인 하기 위해는 `Course` 이제 다음과 같은 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-250">Skip that and view the `query` variable the next time the code reaches the breakpoint in order to see what the `Course` query now looks like.</span></span> <span data-ttu-id="586d4-251">다음과 같은 화면이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-251">You'll see something like the following:</span></span>

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample17.json)]

<span data-ttu-id="586d4-252">이제 쿼리 인지 확인할 수 있습니다는 `JOIN` 로드 하는 쿼리 `Department` 와 함께 데이터는 `Course` 데이터를 포함 하 고 있음을 `WHERE` 절.</span><span class="sxs-lookup"><span data-stu-id="586d4-252">You can see that the query is now a `JOIN` query that loads `Department` data along with the `Course` data, and that it includes a `WHERE` clause.</span></span>

<a id="proxyclasses"></a>

## <a name="working-with-proxy-classes"></a><span data-ttu-id="586d4-253">프록시 클래스 사용</span><span class="sxs-lookup"><span data-stu-id="586d4-253">Working with Proxy Classes</span></span>

<span data-ttu-id="586d4-254">Entity Framework (예: 쿼리를 실행 하는 경우) 엔터티 인스턴스를 만들 때 종종 만듭니다는 엔터티에 대 한 프록시 역할을 동적으로 생성 된 파생 형식의 인스턴스 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-254">When the Entity Framework creates entity instances (for example, when you execute a query), it often creates them as instances of a dynamically generated derived type that acts as a proxy for the entity.</span></span> <span data-ttu-id="586d4-255">이 프록시는 속성에 액세스할 때 자동으로 작업을 수행 하기 위한 후크를 삽입 하는 엔터티의 일부 가상 속성을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-255">This proxy overrides some virtual properties of the entity to insert hooks for performing actions automatically when the property is accessed.</span></span> <span data-ttu-id="586d4-256">예를 들어이 메커니즘은 관계의 한 지연 로딩이 지원 하기 위해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-256">For example, this mechanism is used to support lazy loading of relationships.</span></span>

<span data-ttu-id="586d4-257">대부분의 프록시를 사용 하이 여가 주의 해야 할 필요 하지 않습니다 되지만 예외가:</span><span class="sxs-lookup"><span data-stu-id="586d4-257">Most of the time you don't need to be aware of this use of proxies, but there are exceptions:</span></span>

- <span data-ttu-id="586d4-258">일부 시나리오에서는 Entity Framework 프록시 인스턴스를 만들지 못하도록는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-258">In some scenarios you might want to prevent the Entity Framework from creating proxy instances.</span></span> <span data-ttu-id="586d4-259">예를 들어 비 프록시 인스턴스를 직렬화 하는 작업 프록시 인스턴스를 직렬화 하는 작업 보다 더 효율적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-259">For example, serializing non-proxy instances might be more efficient than serializing proxy instances.</span></span>
- <span data-ttu-id="586d4-260">사용 하 여 엔터티 클래스를 인스턴스화하는 `new` 연산자, 프록시 인스턴스를 가져오지 않음.</span><span class="sxs-lookup"><span data-stu-id="586d4-260">When you instantiate an entity class using the `new` operator, you don't get a proxy instance.</span></span> <span data-ttu-id="586d4-261">즉, 변경 내용 추적을 지연 로드 및 자동과 같은 기능을 활용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-261">This means you don't get functionality such as lazy loading and automatic change tracking.</span></span> <span data-ttu-id="586d4-262">이 일반적으로 알겠습니다. 일반적으로 필요 하지 않습니다 지연 로드는 데이터베이스에 없는 새 엔터티를 작성 하는 동안에 및 변경 내용 추적을으로 엔터티를 명시적으로 표시 하는 경우 일반적으로 필요 하지 않습니다 `Added`합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-262">This is typically okay; you generally don't need lazy loading, because you're creating a new entity that isn't in the database, and you generally don't need change tracking if you're explicitly marking the entity as `Added`.</span></span> <span data-ttu-id="586d4-263">그러나 지연 로드 해야 하는 경우 필요한 변경 내용 추적을 만들 수 있습니다 새 엔터티 인스턴스를 사용 하 여 프록시는 `Create` 의 메서드는 `DbSet` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-263">However, if you do need lazy loading and you need change tracking, you can create new entity instances with proxies using the `Create` method of the `DbSet` class.</span></span>
- <span data-ttu-id="586d4-264">프록시 형식을에서 실제 엔터티 형식을 가져올 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-264">You might want to get an actual entity type from a proxy type.</span></span> <span data-ttu-id="586d4-265">사용할 수는 `GetObjectType` 의 메서드는 `ObjectContext` 클래스의 프록시 형식 인스턴스를 실제 엔터티 형식을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-265">You can use the `GetObjectType` method of the `ObjectContext` class to get the actual entity type of a proxy type instance.</span></span>

<span data-ttu-id="586d4-266">자세한 내용은 참조 [프록시 작업](https://blogs.msdn.com/b/adonet/archive/2011/02/02/using-dbcontext-in-ef-feature-ctp5-part-8-working-with-proxies.aspx) Entity Framework 팀 블로그.</span><span class="sxs-lookup"><span data-stu-id="586d4-266">For more information, see [Working with Proxies](https://blogs.msdn.com/b/adonet/archive/2011/02/02/using-dbcontext-in-ef-feature-ctp5-part-8-working-with-proxies.aspx) on the Entity Framework team blog.</span></span>

## <a name="disabling-automatic-detection-of-changes"></a><span data-ttu-id="586d4-267">변경 내용 자동으로 검색을 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="586d4-267">Disabling Automatic Detection of Changes</span></span>

<span data-ttu-id="586d4-268">Entity Framework는 엔터티의 현재 값을 원래 값과 비교하여 엔터티가 변경된 방법(즉, 데이터베이스에 전송해야 하는 업데이트)을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-268">The Entity Framework determines how an entity has changed (and therefore which updates need to be sent to the database) by comparing the current values of an entity with the original values.</span></span> <span data-ttu-id="586d4-269">엔터티 쿼리 또는 연결 되었을 때 원래 값 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-269">The original values are stored when the entity was queried or attached.</span></span> <span data-ttu-id="586d4-270">자동 변경 내용 검색을 발생시키는 일부 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-270">Some of the methods that cause automatic change detection are the following:</span></span>

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

<span data-ttu-id="586d4-271">많은 엔터티를 추적 하 고 있는 경우 루프에서 여러 번 다음이 방법 중 하나 호출 하면 변경 내용 자동 감지를 사용 하 여 일시적으로 해제 하 여 성능 향상을 발생할 수 있습니다는 [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled(VS.103).aspx) 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-271">If you're tracking a large number of entities and you call one of these methods many times in a loop, you might get significant performance improvements by temporarily turning off automatic change detection using the [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled(VS.103).aspx) property.</span></span> <span data-ttu-id="586d4-272">자세한 내용은 참조 [자동으로 검색 되는 변경 내용을](https://blogs.msdn.com/b/adonet/archive/2011/02/06/using-dbcontext-in-ef-feature-ctp5-part-12-automatically-detecting-changes.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-272">For more information, see [Automatically Detecting Changes](https://blogs.msdn.com/b/adonet/archive/2011/02/06/using-dbcontext-in-ef-feature-ctp5-part-12-automatically-detecting-changes.aspx).</span></span>

## <a name="disabling-validation-when-saving-changes"></a><span data-ttu-id="586d4-273">저장할 때 유효성 검사를 사용 하지 않도록 설정 변경</span><span class="sxs-lookup"><span data-stu-id="586d4-273">Disabling Validation When Saving Changes</span></span>

<span data-ttu-id="586d4-274">호출 하는 경우는 `SaveChanges` 메서드를 Entity Framework 기본적으로 모든 변경 된 엔터티의 모든 속성의 데이터를 하기 전에 유효성 검사 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-274">When you call the `SaveChanges` method, by default the Entity Framework validates the data in all properties of all changed entities before updating the database.</span></span> <span data-ttu-id="586d4-275">많은 엔터티를 업데이트 한 및 이미이 작업은 필요 하지는 데이터를 확인 했으므로 있습니다 고 저장 프로세스를 만들 수는 경우 변경 내용을 유효성 검사를 일시적으로 해제 하 여 더 짧은 시간을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-275">If you've updated a large number of entities and you've already validated the data, this work is unnecessary and you could make the process of saving the changes take less time by temporarily turning off validation.</span></span> <span data-ttu-id="586d4-276">사용 하 여 해당 하는 작업을 수행할 수는 [ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled(VS.103).aspx) 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-276">You can do that using the [ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled(VS.103).aspx) property.</span></span> <span data-ttu-id="586d4-277">자세한 내용은 참조 [유효성 검사](https://blogs.msdn.com/b/adonet/archive/2010/12/15/ef-feature-ctp5-validation.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-277">For more information, see [Validation](https://blogs.msdn.com/b/adonet/archive/2010/12/15/ef-feature-ctp5-validation.aspx).</span></span>

## <a name="summary"></a><span data-ttu-id="586d4-278">요약</span><span class="sxs-lookup"><span data-stu-id="586d4-278">Summary</span></span>

<span data-ttu-id="586d4-279">이 일련의 ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하는 자습서를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-279">This completes this series of tutorials on using the Entity Framework in an ASP.NET MVC application.</span></span> <span data-ttu-id="586d4-280">다른 Entity Framework 리소스에 대 한 링크에서 확인할 수 있습니다는 [ASP.NET 데이터 액세스 콘텐츠 맵](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-280">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

<span data-ttu-id="586d4-281">작성 한 후 웹 응용 프로그램을 배포 하는 방법에 대 한 자세한 내용은 참조 하십시오. [ASP.NET 배포 콘텐츠 맵](https://msdn.microsoft.com/library/bb386521.aspx) MSDN 라이브러리에서.</span><span class="sxs-lookup"><span data-stu-id="586d4-281">For more information about how to deploy your web application after you've built it, see [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521.aspx) in the MSDN Library.</span></span>

<span data-ttu-id="586d4-282">인증 및 권한, 같은 MVC와 관련 된 다른 항목에 대 한 정보에 대 한 참조는 [MVC 권장 리소스](../../getting-started/recommended-resources-for-mvc.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-282">For information about other topics related to MVC, such as authentication and authorization, see the [MVC Recommended Resources](../../getting-started/recommended-resources-for-mvc.md).</span></span>

<a id="acknowledgments"></a>

## <a name="acknowledgments"></a><span data-ttu-id="586d4-283">감사의 글</span><span class="sxs-lookup"><span data-stu-id="586d4-283">Acknowledgments</span></span>

- <span data-ttu-id="586d4-284">Tom Dykstra이이 자습서의 원래 버전을 작성 되며 Microsoft 웹 플랫폼 및 도구 콘텐츠 팀의 수석 프로그래밍 기록기 있습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-284">Tom Dykstra wrote the original version of this tutorial and is a senior programming writer on the Microsoft Web Platform and Tools Content Team.</span></span>
- <span data-ttu-id="586d4-285">[Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [ @RickAndMSFT ](http://twitter.com/RickAndMSFT))이이 자습서를 공동 작성 되 고 5 EF 및 MVC 4에 대 한 업데이트 작업의 대부분을 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-285">[Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) co-authored this tutorial and did most of the work updating it for EF 5 and MVC 4.</span></span> <span data-ttu-id="586d4-286">Rick microsoft Azure 및 MVC에 중점을 두기 수석 프로그래밍 기록기입니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-286">Rick is a senior programming writer for Microsoft focusing on Azure and MVC.</span></span>
- <span data-ttu-id="586d4-287">[Rowan Miller](http://www.romiller.com) 및 Entity Framework 팀의 다른 멤버가 코드 검토를 지 원하는 많은 म 자습서 EF 5에 대 한 업데이트 하는 동안 발생 하는 마이그레이션 문제를 디버그 하는 데 도움을 준 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-287">[Rowan Miller](http://www.romiller.com) and other members of the Entity Framework team assisted with code reviews and helped debug many issues with migrations that arose while we were updating the tutorial for EF 5.</span></span>

## <a name="vb"></a><span data-ttu-id="586d4-288">VB</span><span class="sxs-lookup"><span data-stu-id="586d4-288">VB</span></span>

<span data-ttu-id="586d4-289">자습서, 처음에 생성 하는 경우 다운로드 완료 된 프로젝트의 C# 및 VB 버전을 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-289">When the tutorial was originally produced, we provided both C# and VB versions of the completed download project.</span></span> <span data-ttu-id="586d4-290">이 업데이트 된 시간 제한 사항 및 작업을 하지 않으면 있는 VB.에 대 한 다른 중요 하지만 계열에서 아무 곳 이나 시작 하기 쉽게 수행할 수 있도록 각 장에 대 한 C# 다운로드 가능한 프로젝트를 제공 하 고</span><span class="sxs-lookup"><span data-stu-id="586d4-290">With this update we are providing a C# downloadable project for each chapter to make it easier to get started anywhere in the series, but due to time limitations and other priorities we did not do that for VB.</span></span> <span data-ttu-id="586d4-291">VB 프로젝트의 경우 이러한 자습서를 사용 하 여 작성 하 고 다른 사용자와 공유 하려는, 알려 주시면 하려고 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-291">If you build a VB project using these tutorials and would be willing to share that with others, please let us know.</span></span>

<a id="errors"></a>

## <a name="errors-and-workarounds"></a><span data-ttu-id="586d4-292">오류 및 해결 방법</span><span class="sxs-lookup"><span data-stu-id="586d4-292">Errors and Workarounds</span></span>

### <a name="cannot-createshadow-copy"></a><span data-ttu-id="586d4-293">복사본을 만들어 섀도 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-293">Cannot create/shadow copy</span></span>

<span data-ttu-id="586d4-294">오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="586d4-294">Error Message:</span></span>

<span data-ttu-id="586d4-295">*없습니다 만들어 섀도 복사본 'DotNetOpenAuth.OpenId' 파일이 이미 있으므로 합니다.*</span><span class="sxs-lookup"><span data-stu-id="586d4-295">*Cannot create/shadow copy 'DotNetOpenAuth.OpenId' when that file already exists.*</span></span>

<span data-ttu-id="586d4-296">해결책:</span><span class="sxs-lookup"><span data-stu-id="586d4-296">Solution:</span></span>

<span data-ttu-id="586d4-297">몇 초 정도 기다린 페이지를 새로 고 치세요.</span><span class="sxs-lookup"><span data-stu-id="586d4-297">Wait a few seconds and refresh the page.</span></span>

### <a name="update-database-not-recognized"></a><span data-ttu-id="586d4-298">데이터베이스 업데이트 인식 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="586d4-298">Update-Database not recognized</span></span>

<span data-ttu-id="586d4-299">오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="586d4-299">Error Message:</span></span>

<span data-ttu-id="586d4-300">*' Update-database ' 용어는 cmdlet, 함수, 스크립트 파일 또는 실행 프로그램의 이름으로 인식할 수 없습니다. 이름의 철자를 확인 하거나 경로가 포함 된, 하는 경우 경로가 정확한 지 확인 하 고 다시 시도 하십시오.* (에서 *`Update-Database`* 의 PMC 명령을.)</span><span class="sxs-lookup"><span data-stu-id="586d4-300">*The term 'Update-Database' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.*(From the *`Update-Database`* command in the PMC.)</span></span>

<span data-ttu-id="586d4-301">해결책:</span><span class="sxs-lookup"><span data-stu-id="586d4-301">Solution:</span></span>

<span data-ttu-id="586d4-302">Visual Studio를 끝냅니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-302">Exit Visual Studio.</span></span> <span data-ttu-id="586d4-303">프로젝트를 열어야 하 고 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="586d4-303">Reopen project and try again.</span></span>

### <a name="validation-failed"></a><span data-ttu-id="586d4-304">유효성 검사 실패</span><span class="sxs-lookup"><span data-stu-id="586d4-304">Validation failed</span></span>

<span data-ttu-id="586d4-305">오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="586d4-305">Error Message:</span></span>

<span data-ttu-id="586d4-306">*하나 이상의 엔터티에 대해 유효성 검사가 실패 했습니다. 자세한 내용은 'EntityValidationErrors' 속성을 참조 하십시오.*</span><span class="sxs-lookup"><span data-stu-id="586d4-306">*Validation failed for one or more entities. See 'EntityValidationErrors' property for more details.*</span></span> <span data-ttu-id="586d4-307">(에서 *`Update-Database`* 의 PMC 명령을.)</span><span class="sxs-lookup"><span data-stu-id="586d4-307">(From the *`Update-Database`* command in the PMC.)</span></span>

<span data-ttu-id="586d4-308">해결책:</span><span class="sxs-lookup"><span data-stu-id="586d4-308">Solution:</span></span>

<span data-ttu-id="586d4-309">이러한 문제가 발생 한 유효성 검사 오류는 경우는 `Seed` 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-309">One cause of this problem is validation errors when the `Seed` method runs.</span></span> <span data-ttu-id="586d4-310">참조 [Seeding 및 디버깅 Entity Framework (EF)](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) 디버깅에 대 한 팁은 `Seed` 메서드.</span><span class="sxs-lookup"><span data-stu-id="586d4-310">See [Seeding and Debugging Entity Framework (EF) DBs](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) for tips on debugging the `Seed` method.</span></span>

### <a name="http-50019-error"></a><span data-ttu-id="586d4-311">HTTP 500.19 오류</span><span class="sxs-lookup"><span data-stu-id="586d4-311">HTTP 500.19 error</span></span>

<span data-ttu-id="586d4-312">오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="586d4-312">Error Message:</span></span>

<span data-ttu-id="586d4-313">*HTTP 오류 500.19-내부 서버 오류는 요청 된 페이지의 페이지에 대 한 관련된 구성 데이터가 잘못 되어 액세스할 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="586d4-313">*HTTP Error 500.19 - Internal Server Error The requested page cannot be accessed because the related configuration data for the page is invalid.*</span></span>

<span data-ttu-id="586d4-314">해결책:</span><span class="sxs-lookup"><span data-stu-id="586d4-314">Solution:</span></span>

<span data-ttu-id="586d4-315">이 오류가 발생 하는 한 가지 방법은 각각 동일한 포트 번호를 사용 하 여 솔루션의 여러 복사본이 있는 것은 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-315">One way you can get this error is from having multiple copies of the solution, each of them using the same port number.</span></span> <span data-ttu-id="586d4-316">일반적으로 Visual Studio의 모든 인스턴스를 종료 한 다음 프로젝트에 작업을 다시 시작 하 여이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-316">You can usually solve this problem by exiting all instances of Visual Studio, then restarting the project your working on.</span></span> <span data-ttu-id="586d4-317">그래도 문제가 해결 되지 포트 번호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-317">If that doesn't work, try changing the port number.</span></span> <span data-ttu-id="586d4-318">프로젝트 파일을 마우스 오른쪽 단추로 클릭 하 고 properties를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-318">Right click on the project file and then click properties.</span></span> <span data-ttu-id="586d4-319">선택 된 **웹** 탭 한 다음에 포트 번호를 변경는 **프로젝트 Url** 입력란.</span><span class="sxs-lookup"><span data-stu-id="586d4-319">Select the **Web** tab and then change the port number in the **Project Url** text box.</span></span>

### <a name="error-locating-sql-server-instance"></a><span data-ttu-id="586d4-320">SQL Server 인스턴스 찾기 오류</span><span class="sxs-lookup"><span data-stu-id="586d4-320">Error locating SQL Server instance</span></span>

<span data-ttu-id="586d4-321">오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="586d4-321">Error Message:</span></span>

<span data-ttu-id="586d4-322">*SQL Server에 연결을 설정 하는 동안 네트워크 관련 또는 인스턴스 관련 오류가 발생 했습니다. 서버를 찾을 수 없거나 액세스할 수 없습니다. 인스턴스 이름이 올바르고 SQL Server 원격 연결을 허용 하도록 구성 되어 있는지 확인 합니다. (공급자: SQL 네트워크 인터페이스, 오류: 26-서버/인스턴스 지정 된 찾기 오류)*</span><span class="sxs-lookup"><span data-stu-id="586d4-322">*A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: SQL Network Interfaces, error: 26 - Error Locating Server/Instance Specified)*</span></span>

<span data-ttu-id="586d4-323">해결책:</span><span class="sxs-lookup"><span data-stu-id="586d4-323">Solution:</span></span>

<span data-ttu-id="586d4-324">연결 문자열을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-324">Check connection string.</span></span> <span data-ttu-id="586d4-325">데이터베이스를 수동으로 삭제 하는 경우 생성 문자열에 데이터베이스의 이름을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="586d4-325">If you have manually deleted the database, change the name of the database in the construction string.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="586d4-326">[이전](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
> [다음](building-the-ef5-mvc4-chapter-downloads.md)</span><span class="sxs-lookup"><span data-stu-id="586d4-326">[Previous](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
[Next](building-the-ef5-mvc4-chapter-downloads.md)</span></span>
