---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: "MVC 5 웹 응용 프로그램 (12 / 12)에 대 한 고급 Entity Framework 6 시나리오 | Microsoft Docs"
author: tdykstra
description: "Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/08/2014
ms.topic: article
ms.assetid: f35a9b0c-49ef-4cde-b06d-19d1543feb0b
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: 85276377671b96e65406639c8584d9ebf8d77ff7
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="advanced-entity-framework-6-scenarios-for-an-mvc-5-web-application-12-of-12"></a><span data-ttu-id="4d53b-103">MVC 5 웹 응용 프로그램 (12 / 12)에 대 한 고급 Entity Framework 6 시나리오</span><span class="sxs-lookup"><span data-stu-id="4d53b-103">Advanced Entity Framework 6 Scenarios for an MVC 5 Web Application (12 of 12)</span></span>
====================
<span data-ttu-id="4d53b-104">으로 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="4d53b-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="4d53b-105">[완료 된 프로젝트를 다운로드](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) 또는 [PDF 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)</span><span class="sxs-lookup"><span data-stu-id="4d53b-105">[Download Completed Project](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) or [Download PDF](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)</span></span>

> <span data-ttu-id="4d53b-106">Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio 2013을 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 5 applications using the Entity Framework 6 Code First and Visual Studio 2013.</span></span> <span data-ttu-id="4d53b-107">자습서 시리즈에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>


<span data-ttu-id="4d53b-108">이전 자습서에서 구현한 계층당 하나의 테이블 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-108">In the previous tutorial you implemented table-per-hierarchy inheritance.</span></span> <span data-ttu-id="4d53b-109">이 자습서에는 Entity Framework Code First를 사용 하는 ASP.NET 웹 응용 프로그램 개발의 기본 사항을 초과할 때 알고 있어야 하는 데 유용 하는 여러 항목을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-109">This tutorial includes introduces several topics that are useful to be aware of when you go beyond the basics of developing ASP.NET web applications that use Entity Framework Code First.</span></span> <span data-ttu-id="4d53b-110">단계별 지침 안내는 코드와 다음 항목에 대 한 Visual Studio를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="4d53b-110">Step-by-step instructions walk you through the code and using Visual Studio for the following topics:</span></span>

- [<span data-ttu-id="4d53b-111">원시 SQL 쿼리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-111">Performing raw SQL queries</span></span>](#rawsql)
- [<span data-ttu-id="4d53b-112">No 추적 쿼리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-112">Performing no-tracking queries</span></span>](#notracking)
- [<span data-ttu-id="4d53b-113">데이터베이스에 전송 SQL 검사</span><span class="sxs-lookup"><span data-stu-id="4d53b-113">Examining SQL sent to the database</span></span>](#sql)

<span data-ttu-id="4d53b-114">자습서에서는 다음 링크에 대 한 자세한 내용은 리소스에 대 한 간략 한 소개를 여러 항목을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-114">The tutorial introduces several topics with brief introductions followed by links to resources for more information:</span></span>

- [<span data-ttu-id="4d53b-115">작업 패턴의 단위 및 저장소</span><span class="sxs-lookup"><span data-stu-id="4d53b-115">Repository and unit of work patterns</span></span>](#repo)
- [<span data-ttu-id="4d53b-116">프록시 클래스</span><span class="sxs-lookup"><span data-stu-id="4d53b-116">Proxy classes</span></span>](#proxies)
- [<span data-ttu-id="4d53b-117">자동 변경 내용 검색</span><span class="sxs-lookup"><span data-stu-id="4d53b-117">Automatic change detection</span></span>](#changedetection)
- [<span data-ttu-id="4d53b-118">자동 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="4d53b-118">Automatic validation</span></span>](#validation)
- [<span data-ttu-id="4d53b-119">Visual Studio 용 EF 도구</span><span class="sxs-lookup"><span data-stu-id="4d53b-119">EF tools for Visual Studio</span></span>](#tools)
- [<span data-ttu-id="4d53b-120">Entity Framework 소스 코드</span><span class="sxs-lookup"><span data-stu-id="4d53b-120">Entity Framework source code</span></span>](#source)

<span data-ttu-id="4d53b-121">이 자습서에는 다음 섹션에서는 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-121">The tutorial also includes the following sections:</span></span>

- [<span data-ttu-id="4d53b-122">요약</span><span class="sxs-lookup"><span data-stu-id="4d53b-122">Summary</span></span>](#summary)
- [<span data-ttu-id="4d53b-123">승인</span><span class="sxs-lookup"><span data-stu-id="4d53b-123">Acknowledgments</span></span>](#acknowledgments)
- [<span data-ttu-id="4d53b-124">VB에 대 한 메모</span><span class="sxs-lookup"><span data-stu-id="4d53b-124">A note about VB</span></span>](#vb)
- [<span data-ttu-id="4d53b-125">일반적인 오류 해결 방법 또는을</span><span class="sxs-lookup"><span data-stu-id="4d53b-125">Common errors, and solutions or workarounds for them</span></span>](#errors)

<span data-ttu-id="4d53b-126">다음이 항목 중 대부분의 경우 이미 만든 페이지를 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-126">For most of these topics, you'll work with pages that you already created.</span></span> <span data-ttu-id="4d53b-127">원시 SQL 대량 업데이트 수행을 사용 하는 데이터베이스의 모든 과정의 크레딧의 수를 업데이트 하는 새 페이지를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-127">To use raw SQL to do bulk updates you'll create a new page that updates the number of credits of all courses in the database:</span></span>

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

<a id="rawsql"></a>
## <a name="performing-raw-sql-queries"></a><span data-ttu-id="4d53b-129">성능 원시 SQL 쿼리</span><span class="sxs-lookup"><span data-stu-id="4d53b-129">Performing Raw SQL Queries</span></span>

<span data-ttu-id="4d53b-130">엔터티 프레임 워크 코드의 첫 번째 API에는 SQL 명령을 데이터베이스에 직접 전달할 수 있도록 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-130">The Entity Framework Code First API includes methods that enable you to pass SQL commands directly to the database.</span></span> <span data-ttu-id="4d53b-131">다음과 같은 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-131">You have the following options:</span></span>

- <span data-ttu-id="4d53b-132">사용 하 여 [DbSet.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.dbset.sqlquery.aspx) 엔터티 형식을 반환 하는 쿼리에 대 한 메서드.</span><span class="sxs-lookup"><span data-stu-id="4d53b-132">Use the [DbSet.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.dbset.sqlquery.aspx) method for queries that return entity types.</span></span> <span data-ttu-id="4d53b-133">반환 된 개체에 필요한 형식 이어야 합니다는 `DbSet` 있으며 개체를 자동으로 추적 됩니다는 데이터베이스 컨텍스트에서 해제 하지 않으면 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-133">The returned objects must be of the type expected by the `DbSet` object, and they are automatically tracked by the database context unless you turn tracking off.</span></span> <span data-ttu-id="4d53b-134">(다음 섹션에 대 한 참조는 [AsNoTracking](https://msdn.microsoft.com/library/system.data.entity.dbextensions.asnotracking.aspx) 메서드.)</span><span class="sxs-lookup"><span data-stu-id="4d53b-134">(See the following section about the [AsNoTracking](https://msdn.microsoft.com/library/system.data.entity.dbextensions.asnotracking.aspx) method.)</span></span>
- <span data-ttu-id="4d53b-135">사용 하 여는 [Database.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery.aspx) 엔터티 지원 하지 않는 형식을 반환 하는 쿼리에 메서드.</span><span class="sxs-lookup"><span data-stu-id="4d53b-135">Use the [Database.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery.aspx) method for queries that return types that aren't entities.</span></span> <span data-ttu-id="4d53b-136">반환 된 데이터 엔터티 형식을 검색 하려면이 메서드를 사용 하는 경우에 데이터베이스 컨텍스트에 의해 추적 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-136">The returned data isn't tracked by the database context, even if you use this method to retrieve entity types.</span></span>
- <span data-ttu-id="4d53b-137">사용 하 여 [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456.aspx) 쿼리가 아닌 명령에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-137">Use the [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456.aspx) for non-query commands.</span></span>

<span data-ttu-id="4d53b-138">Entity Framework 사용의 장점 중 하나를 방지할 수 제한 된 데이터를 저장 하는 특정 방법에 가깝게 너무 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-138">One of the advantages of using the Entity Framework is that it avoids tying your code too closely to a particular method of storing data.</span></span> <span data-ttu-id="4d53b-139">생성 하 여 SQL 쿼리 및 명령, 직접 작성 하지 않아도 하므로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-139">It does this by generating SQL queries and commands for you, which also frees you from having to write them yourself.</span></span> <span data-ttu-id="4d53b-140">하지만 예외적인 시나리오 수동으로 만든 특정 SQL 쿼리를 실행 해야 할 때 있으며 이러한 방법을 원활 하 게 이러한 예외를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-140">But there are exceptional scenarios when you need to run specific SQL queries that you have manually created, and these methods make it possible for you to handle such exceptions.</span></span>

<span data-ttu-id="4d53b-141">항상 true 인 웹 응용 프로그램에서 SQL 명령을 실행 하는 경우, 사이트 SQL 삽입 공격 으로부터 보호 하기 위해 예방 조치 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-141">As is always true when you execute SQL commands in a web application, you must take precautions to protect your site against SQL injection attacks.</span></span> <span data-ttu-id="4d53b-142">작업을 수행 하는 한 가지 방법은 웹 페이지를 제출한 문자열 SQL 명령으로 해석할 수 없는 되도록 매개 변수가 있는 쿼리를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-142">One way to do that is to use parameterized queries to make sure that strings submitted by a web page can't be interpreted as SQL commands.</span></span> <span data-ttu-id="4d53b-143">이 자습서에서는 사용자 입력을 쿼리에 통합 하는 경우 매개 변수가 있는 쿼리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-143">In this tutorial you'll use parameterized queries when integrating user input into a query.</span></span>

### <a name="calling-a-query-that-returns-entities"></a><span data-ttu-id="4d53b-144">엔터티를 반환 하는 쿼리 호출</span><span class="sxs-lookup"><span data-stu-id="4d53b-144">Calling a Query that Returns Entities</span></span>

<span data-ttu-id="4d53b-145">[DbSet&lt;TEntity&gt; ](https://msdn.microsoft.com/library/gg696460.aspx) 클래스 형식의 엔터티를 반환 하는 쿼리를 실행 하는 데 사용할 수 있는 메서드를 제공 `TEntity`합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-145">The [DbSet&lt;TEntity&gt;](https://msdn.microsoft.com/library/gg696460.aspx) class provides a method that you can use to execute a query that returns an entity of type `TEntity`.</span></span> <span data-ttu-id="4d53b-146">이 방법을 보려면 있습니다의 코드를 변경 합니다는 `Details` 의 메서드는 `Department` 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-146">To see how this works you'll change the code in the `Details` method of the `Department` controller.</span></span>

<span data-ttu-id="4d53b-147">*DepartmentController.cs*에 `Details` 메서드를 대체는 `db.Departments.FindAsync` 메서드 호출을 `db.Departments.SqlQuery` 다음 강조 표시 된 코드에 나와 있는 것 처럼 메서드 호출:</span><span class="sxs-lookup"><span data-stu-id="4d53b-147">In *DepartmentController.cs*, in the `Details` method, replace the `db.Departments.FindAsync` method call with a `db.Departments.SqlQuery` method call, as shown in the following highlighted code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs?highlight=8-14)]

<span data-ttu-id="4d53b-148">새 코드는 올바르게 작동 하는지 확인 하려면 선택은 **부서** 탭 한 다음 **세부 정보** 부서 중 하나에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-148">To verify that the new code works correctly, select the **Departments** tab and then **Details** for one of the departments.</span></span>

![부서 세부 정보](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image2.png)

### <a name="calling-a-query-that-returns-other-types-of-objects"></a><span data-ttu-id="4d53b-150">다른 형식의 개체를 반환 하는 쿼리 호출</span><span class="sxs-lookup"><span data-stu-id="4d53b-150">Calling a Query that Returns Other Types of Objects</span></span>

<span data-ttu-id="4d53b-151">각 등록 날짜에 대 한 학생 수를 보여 주는 정보 페이지에 대 한 학생 통계 표에서 이전 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-151">Earlier you created a student statistics grid for the About page that showed the number of students for each enrollment date.</span></span> <span data-ttu-id="4d53b-152">이 작업을 수행 하는 코드 *HomeController.cs* LINQ를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="4d53b-152">The code that does this in *HomeController.cs* uses LINQ:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

<span data-ttu-id="4d53b-153">LINQ를 사용 하는 것이 아니라 SQL에서 직접이 데이터는 코드를 작성 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-153">Suppose you want to write the code that retrieves this data directly in SQL rather than using LINQ.</span></span> <span data-ttu-id="4d53b-154">엔터티 개체 이외의 형식을 반환 하는 쿼리를 실행 해야 할 즉 사용 해야는 [Database.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery(v=VS.103).aspx) 메서드.</span><span class="sxs-lookup"><span data-stu-id="4d53b-154">To do that you need to run a query that returns something other than entity objects, which means you need to use the [Database.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery(v=VS.103).aspx) method.</span></span>

<span data-ttu-id="4d53b-155">*HomeController.cs*에서 LINQ 문을 대체는 `About` 다음 강조 표시 된 코드에 표시 된 대로 SQL 문 사용 하 여 메서드:</span><span class="sxs-lookup"><span data-stu-id="4d53b-155">In *HomeController.cs*, replace the LINQ statement in the `About` method with a SQL statement, as shown in the following highlighted code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs?highlight=3-18)]

<span data-ttu-id="4d53b-156">정보 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-156">Run the About page.</span></span> <span data-ttu-id="4d53b-157">이전과 동일한 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-157">It displays the same data it did before.</span></span>

![About_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image3.png)

### <a name="calling-an-update-query"></a><span data-ttu-id="4d53b-159">업데이트 쿼리를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-159">Calling an Update Query</span></span>

<span data-ttu-id="4d53b-160">Contoso 대학 관리자가 모든 과정에 대 한 크레딧의 수를 변경 하는 등 데이터베이스에 대량 변경 내용이 수행 하 려 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-160">Suppose Contoso University administrators want to be able to perform bulk changes in the database, such as changing the number of credits for every course.</span></span> <span data-ttu-id="4d53b-161">대학교 많은 수의 과목 있으면 수 없기 엔터티로 모두 검색 하 고 개별적으로 변경 하 여 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-161">If the university has a large number of courses, it would be inefficient to retrieve them all as entities and change them individually.</span></span> <span data-ttu-id="4d53b-162">이 섹션의 사용자는 모든 과정에 대 한 크레딧의 수를 변경 하는 인수를 지정할 수 있게 하는 웹 페이지를 구현 하 고 SQL을 실행 하 여 변경 내용을 지정 `UPDATE` 문.</span><span class="sxs-lookup"><span data-stu-id="4d53b-162">In this section you'll implement a web page that enables the user to specify a factor by which to change the number of credits for all courses, and you'll make the change by executing a SQL `UPDATE` statement.</span></span> <span data-ttu-id="4d53b-163">웹 페이지는 다음 그림과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-163">The web page will look like the following illustration:</span></span>

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image4.png)

<span data-ttu-id="4d53b-165">*CourseContoller.cs*, 추가 `UpdateCourseCredits` 에 대 한 메서드 `HttpGet` 및 `HttpPost`:</span><span class="sxs-lookup"><span data-stu-id="4d53b-165">In *CourseContoller.cs*, add `UpdateCourseCredits` methods for `HttpGet` and `HttpPost`:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

<span data-ttu-id="4d53b-166">컨트롤러를 처리 한 `HttpGet` 요청에 아무 것도 반환에 `ViewBag.RowsAffected` 변수와 보기 표시 빈 텍스트 상자 및 전송 단추, 앞의 그림에 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-166">When the controller processes an `HttpGet` request, nothing is returned in the `ViewBag.RowsAffected` variable, and the view displays an empty text box and a submit button, as shown in the preceding illustration.</span></span>

<span data-ttu-id="4d53b-167">때는 **업데이트** 단추를 클릭 하면는 `HttpPost` 메서드를 호출 하 고 `multiplier` 에 텍스트 상자에 입력 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-167">When the **Update** button is clicked, the `HttpPost` method is called, and `multiplier` has the value entered in the text box.</span></span> <span data-ttu-id="4d53b-168">코드를 다음 과정을 업데이트 하 고 보기에 영향을 받는 행 수를 반환 하는 SQL 실행 하는 `ViewBag.RowsAffected` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-168">The code then executes the SQL that updates courses and returns the number of affected rows to the view in the `ViewBag.RowsAffected` variable.</span></span> <span data-ttu-id="4d53b-169">보기에는 값을 가져올 때 변수를 텍스트 상자 대신 업데이트 된 행의 수를 표시 하 고 다음 그림에 나와 있는 것 처럼 단추, 제출:</span><span class="sxs-lookup"><span data-stu-id="4d53b-169">When the view gets a value in that variable, it displays the number of rows updated instead of the text box and submit button, as shown in the following illustration:</span></span>

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image5.png)

<span data-ttu-id="4d53b-171">*CourseController.cs*, 중 하나를 마우스 오른쪽 단추로 클릭는 `UpdateCourseCredits` 메서드와 클릭 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-171">In *CourseController.cs*, right-click one of the `UpdateCourseCredits` methods, and then click **Add View**.</span></span>

![Add_View_dialog_box_for_Update_Course_Credits](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image6.png)

<span data-ttu-id="4d53b-173">*Views\Course\UpdateCourseCredits.cshtml*, 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-173">In *Views\Course\UpdateCourseCredits.cshtml*, replace the template code with the following code:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cshtml)]

<span data-ttu-id="4d53b-174">실행의 `UpdateCourseCredits` 메서드를 선택 하 여는 **Courses** 탭에서 다음 추가 "/ UpdateCourseCredits" 브라우저의 주소 표시줄에 URL의 끝에 (예: `http://localhost:50205/Course/UpdateCourseCredits`).</span><span class="sxs-lookup"><span data-stu-id="4d53b-174">Run the `UpdateCourseCredits` method by selecting the **Courses** tab, then adding "/UpdateCourseCredits" to the end of the URL in the browser's address bar (for example: `http://localhost:50205/Course/UpdateCourseCredits`).</span></span> <span data-ttu-id="4d53b-175">텍스트 상자에 숫자를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-175">Enter a number in the text box:</span></span>

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image7.png)

<span data-ttu-id="4d53b-177">**업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-177">Click **Update**.</span></span> <span data-ttu-id="4d53b-178">영향을 받는 행 수가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-178">You see the number of rows affected:</span></span>

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image8.png)

<span data-ttu-id="4d53b-180">클릭 **목록으로 돌아가기** 크레딧의 수정 된 번호로 과정의 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-180">Click **Back to List** to see the list of courses with the revised number of credits.</span></span>

![Courses_Index_page_showing_revised_credits](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image9.png)

<span data-ttu-id="4d53b-182">원시 SQL 쿼리 하는 방법에 대 한 자세한 내용은 참조 [원시 SQL 쿼리](https://msdn.microsoft.com/data/jj592907) msdn 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-182">For more information about raw SQL queries, see [Raw SQL Queries](https://msdn.microsoft.com/data/jj592907) on MSDN.</span></span>

<a id="notracking"></a>
## <a name="no-tracking-queries"></a><span data-ttu-id="4d53b-183">No 추적 쿼리</span><span class="sxs-lookup"><span data-stu-id="4d53b-183">No-Tracking Queries</span></span>

<span data-ttu-id="4d53b-184">데이터베이스 컨텍스트 테이블 행을 검색 하 고을 나타내는 엔터티 개체를 만드는 때 기본적으로를 추적 데이터베이스에 포함 된 내용으로 메모리에 엔터티 동기화 되었는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-184">When a database context retrieves table rows and creates entity objects that represent them, by default it keeps track of whether the entities in memory are in sync with what's in the database.</span></span> <span data-ttu-id="4d53b-185">데이터를 메모리에에서 한 캐시 역할을 하 고 엔터티를 업데이트할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-185">The data in memory acts as a cache and is used when you update an entity.</span></span> <span data-ttu-id="4d53b-186">이 캐싱은 종종에 필요 하지 않은 웹 응용 프로그램 컨텍스트는 일반적으로 수명이 짧은 (새로운 삭제을 만들어 각 요청에 대 한) 인스턴스와 컨텍스트 때문에 읽는 엔터티는 해당 엔터티를 다시 사용 하기 전에 일반적으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-186">This caching is often unnecessary in a web application because context instances are typically short-lived (a new one is created and disposed for each request) and the context that reads an entity is typically disposed before that entity is used again.</span></span>

<span data-ttu-id="4d53b-187">사용 하 여 메모리에 엔터티 개체의 추적을 해제할 수 있습니다는 [AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) 메서드.</span><span class="sxs-lookup"><span data-stu-id="4d53b-187">You can disable tracking of entity objects in memory by using the [AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) method.</span></span> <span data-ttu-id="4d53b-188">다음과 같은 일반적인 시나리오를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-188">Typical scenarios in which you might want to do that include the following:</span></span>

- <span data-ttu-id="4d53b-189">쿼리 추적을 해제 성능을 눈에 띄게 향상 시킬 수 있는 데이터의 큰 볼륨을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-189">A query retrieves such a large volume of data that turning off tracking might noticeably enhance performance.</span></span>
- <span data-ttu-id="4d53b-190">업데이트 하려면 엔터티를 연결 하려고 하지만 이전 다른 목적을 위해 동일한 엔터티를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-190">You want to attach an entity in order to update it, but you earlier retrieved the same entity for a different purpose.</span></span> <span data-ttu-id="4d53b-191">엔터티는 데이터베이스 컨텍스트에서 이미 추적 중인를 변경 하려면 해당 하는 엔터티를 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-191">Because the entity is already being tracked by the database context, you can't attach the entity that you want to change.</span></span> <span data-ttu-id="4d53b-192">이 상황을 처리 하는 한 가지 방법은 사용 하는 것은 `AsNoTracking` 이전 쿼리를 사용 하는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-192">One way to handle this situation is to use the `AsNoTracking` option with the earlier query.</span></span>

<span data-ttu-id="4d53b-193">사용 하는 방법을 보여 주는 예제는 [AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) 메서드를 참조 [이 자습서의 이전 버전](../../older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-193">For an example that demonstrates how to use the [AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) method, see [the earlier version of this tutorial](../../older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application.md).</span></span> <span data-ttu-id="4d53b-194">자습서의이 버전 하지 않는 Modified에 플래그를 설정 편집 메서드는 모델 바인더를 만든 엔터티 되므로 필요 하지 않습니다 `AsNoTracking`합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-194">This version of the tutorial doesn't set the Modified flag on a model-binder-created entity in the Edit method, so it doesn't need `AsNoTracking`.</span></span>

<a id="sql"></a>
## <a name="examining-sql-sent-to-the-database"></a><span data-ttu-id="4d53b-195">데이터베이스에 전송 SQL 검사</span><span class="sxs-lookup"><span data-stu-id="4d53b-195">Examining SQL sent to the database</span></span>

<span data-ttu-id="4d53b-196">데이터베이스에 전송 되는 실제 SQL 쿼리를 볼 수 많은 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-196">Sometimes it's helpful to be able to see the actual SQL queries that are sent to the database.</span></span> <span data-ttu-id="4d53b-197">이전 자습서에서는 인터셉터 코드에서 작업을 수행 하는 방법을 알아보았습니다. 이제 인터셉터 코드를 작성 하지 않고도 할 몇 가지 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-197">In an earlier tutorial you saw how to do that in interceptor code; now you'll see some ways to do it without writing interceptor code.</span></span> <span data-ttu-id="4d53b-198">이렇게 해 보려면 단순 쿼리를 확인 하 고 이러한 eager 로드, 필터링 및 정렬 옵션을 추가할 때를 어떻게 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-198">To try this out, you'll look at a simple query and then look at what happens to it as you add options such eager loading, filtering, and sorting.</span></span>

<span data-ttu-id="4d53b-199">*컨트롤러/CourseController*, 대체 된 `Index` 즉시 로드를 일시적으로 중지 하려면 다음 코드를 사용 하 여 메서드:</span><span class="sxs-lookup"><span data-stu-id="4d53b-199">In *Controllers/CourseController*, replace the `Index` method with the following code, in order to temporarily stop eager loading:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

<span data-ttu-id="4d53b-200">이제에 중단점을 설정의 `return` 문 (해당 줄에 커서를 놓고 F9).</span><span class="sxs-lookup"><span data-stu-id="4d53b-200">Now set a breakpoint on the `return` statement (F9 with the cursor on that line).</span></span> <span data-ttu-id="4d53b-201">F5 키를 눌러 디버그 모드에서 프로젝트를 실행 하 고 과정 인덱스 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-201">Press F5 to run the project in debug mode, and select the Course Index page.</span></span> <span data-ttu-id="4d53b-202">코드에서 중단점에 도달 하면 검사는 `sql` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-202">When the code reaches the breakpoint, examine the `sql` variable.</span></span> <span data-ttu-id="4d53b-203">SQL Server로 전송 하는 쿼리를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-203">You see the query that's sent to SQL Server.</span></span> <span data-ttu-id="4d53b-204">단순 `Select` 문.</span><span class="sxs-lookup"><span data-stu-id="4d53b-204">It's a simple `Select` statement.</span></span>

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.json)]

<span data-ttu-id="4d53b-205">돋보기 클래스에서 쿼리를 클릭 하 고 **텍스트 시각화 도우미**합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-205">Click the magnifying class to see the query in the **Text Visualizer**.</span></span>

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

<span data-ttu-id="4d53b-206">이제 사용자가 특정 부서에 필터링 할 수 있도록 Courses 인덱스 페이지에 드롭 다운 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-206">Now you'll add a drop-down list to the Courses Index page so that users can filter for a particular department.</span></span> <span data-ttu-id="4d53b-207">코스 제목별으로 정렬 하 고 즉시 로드에 대 한을 지정 합니다는 `Department` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-207">You'll sort the courses by title, and you'll specify eager loading for the `Department` navigation property.</span></span>

<span data-ttu-id="4d53b-208">*CourseController.cs*, 대체 된 `Index` 메서드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="4d53b-208">In *CourseController.cs*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

<span data-ttu-id="4d53b-209">중단점에 복원는 `return` 문.</span><span class="sxs-lookup"><span data-stu-id="4d53b-209">Restore the breakpoint on the `return` statement.</span></span>

<span data-ttu-id="4d53b-210">드롭다운 목록에서 선택한 값을 받습니다. 메서드는 `SelectedDepartment` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-210">The method receives the selected value of the drop-down list in the `SelectedDepartment` parameter.</span></span> <span data-ttu-id="4d53b-211">어떤 영역도 선택 하는 경우이 매개 변수가 null이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-211">If nothing is selected, this parameter will be null.</span></span>

<span data-ttu-id="4d53b-212">A `SelectList` 드롭 다운 목록에 대 한 모든 부서가 포함 된 컬렉션 뷰에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-212">A `SelectList` collection containing all departments is passed to the view for the drop-down list.</span></span> <span data-ttu-id="4d53b-213">에 전달 된 매개 변수는 `SelectList` 생성자 값 필드 이름, 텍스트 필드 이름 및 선택한 항목을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-213">The parameters passed to the `SelectList` constructor specify the value field name, the text field name, and the selected item.</span></span>

<span data-ttu-id="4d53b-214">에 대 한는 `Get` 의 메서드는 `Course` 필터 식, 정렬 순서 및에 대 한 로드 eager 리포지토리, 코드를 지정 된 `Department` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-214">For the `Get` method of the `Course` repository, the code specifies a filter expression, a sort order, and eager loading for the `Department` navigation property.</span></span> <span data-ttu-id="4d53b-215">필터 식에는 항상 반환 `true` 드롭 다운 목록에서 아무것도 선택 하는 경우 (즉, `SelectedDepartment` null).</span><span class="sxs-lookup"><span data-stu-id="4d53b-215">The filter expression always returns `true` if nothing is selected in the drop-down list (that is, `SelectedDepartment` is null).</span></span>

<span data-ttu-id="4d53b-216">*Views\Course\Index.cshtml*, 열기 바로 앞 `table` 태그에 다음 코드를 추가 드롭 다운 목록 및 전송 단추를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-216">In *Views\Course\Index.cshtml*, immediately before the opening `table` tag, add the following code to create the drop-down list and a submit button:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

<span data-ttu-id="4d53b-217">중단점이 설정 된 설정 여전히 과정 인덱스 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-217">With the breakpoint still set, run the Course Index page.</span></span> <span data-ttu-id="4d53b-218">페이지를 브라우저에 표시 되도록 코드 중단점에 도달 하는 첫 번째 시간까지 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-218">Continue through the first times that the code hits a breakpoint, so that the page is displayed in the browser.</span></span> <span data-ttu-id="4d53b-219">부서 드롭 다운 목록에서 선택 하 고 클릭 **필터**:</span><span class="sxs-lookup"><span data-stu-id="4d53b-219">Select a department from the drop-down list and click **Filter**:</span></span>

![Course_Index_page_with_department_selected](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image11.png)

<span data-ttu-id="4d53b-221">이 이번 드롭 다운 목록에 대 한 부서 쿼리에 대 한 첫 번째 중단점이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-221">This time the first breakpoint will be for the departments query for the drop-down list.</span></span> <span data-ttu-id="4d53b-222">생략 하 고 보기는 `query` 변수 다음에 코드 중단점에 도달 하면는 기능을 확인 하기 위해는 `Course` 이제 다음과 같은 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-222">Skip that and view the `query` variable the next time the code reaches the breakpoint in order to see what the `Course` query now looks like.</span></span> <span data-ttu-id="4d53b-223">다음과 같은 화면이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-223">You'll see something like the following:</span></span>

[!code-sql[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.sql)]

<span data-ttu-id="4d53b-224">이제 쿼리 인지 확인할 수 있습니다는 `JOIN` 로드 하는 쿼리 `Department` 와 함께 데이터는 `Course` 데이터를 포함 하 고 있음을 `WHERE` 절.</span><span class="sxs-lookup"><span data-stu-id="4d53b-224">You can see that the query is now a `JOIN` query that loads `Department` data along with the `Course` data, and that it includes a `WHERE` clause.</span></span>

<span data-ttu-id="4d53b-225">제거는 `var sql = courses.ToString()` 선입니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-225">Remove the `var sql = courses.ToString()` line.</span></span>

<a id="repo"></a>

## <a name="repository-and-unit-of-work-patterns"></a><span data-ttu-id="4d53b-226">작업 패턴의 단위 및 저장소</span><span class="sxs-lookup"><span data-stu-id="4d53b-226">Repository and unit of work patterns</span></span>

<span data-ttu-id="4d53b-227">대부분의 개발자는 Entity Framework와 함께 사용할 수 있는 코드 주위에서 래퍼로 저장소와 단위 작업 패턴을 구현 하는 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-227">Many developers write code to implement the repository and unit of work patterns as a wrapper around code that works with the Entity Framework.</span></span> <span data-ttu-id="4d53b-228">이러한 패턴은 데이터 액세스 계층 및 응용 프로그램의 비즈니스 논리 계층 간에 추상화 계층을 만드는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-228">These patterns are intended to create an abstraction layer between the data access layer and the business logic layer of an application.</span></span> <span data-ttu-id="4d53b-229">이러한 패턴을 구현 하는 데이터 저장소의 변경 내용 으로부터 응용 프로그램을 분리 하는 데 도움이 및 자동화 된 단위 테스트 또는 테스트 기반 개발 (TDD)으로 기여할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-229">Implementing these patterns can help insulate your application from changes in the data store and can facilitate automated unit testing or test-driven development (TDD).</span></span> <span data-ttu-id="4d53b-230">그러나 이러한 패턴을 구현 하는 추가 코드를 작성은 여러 가지 이유로 EF를 사용 하는 응용 프로그램에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-230">However, writing additional code to implement these patterns is not always the best choice for applications that use EF, for several reasons:</span></span>

- <span data-ttu-id="4d53b-231">EF 컨텍스트 클래스 자체 데이터 저장소 관련 코드에서 코드를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-231">The EF context class itself insulates your code from data-store-specific code.</span></span>
- <span data-ttu-id="4d53b-232">EF 컨텍스트 클래스 EF를 사용 하 여 수행 하는 데이터베이스에 대 한 작업 단위가 클래스 업데이트 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-232">The EF context class can act as a unit-of-work class for database updates that you do using EF.</span></span>
- <span data-ttu-id="4d53b-233">Entity Framework 6의 새로운 기능 쉽게 리포지토리에 코드를 작성 하지 않고 TDD를 구현 하려면.</span><span class="sxs-lookup"><span data-stu-id="4d53b-233">Features introduced in Entity Framework 6 make it easier to implement TDD without writing repository code.</span></span>

<span data-ttu-id="4d53b-234">저장소 및 작업 패턴의 단위를 구현 하는 방법에 대 한 자세한 내용은 참조 [이 자습서 시리즈의 Entity Framework 5 버전](../../older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-234">For more information about how to implement the repository and unit of work patterns, see [the Entity Framework 5 version of this tutorial series](../../older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="4d53b-235">Entity Framework 6에서 TDD를 구현 하는 방법에 대 한 내용은 다음 리소스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-235">For information about ways to implement TDD in Entity Framework 6, see the following resources:</span></span>

- [<span data-ttu-id="4d53b-236">EF6 사용 하는 방법을 Mocking DbSets 보다 쉽게</span><span class="sxs-lookup"><span data-stu-id="4d53b-236">How EF6 Enables Mocking DbSets more easily</span></span>](http://thedatafarm.com/data-access/how-ef6-enables-mocking-dbsets-more-easily/)
- [<span data-ttu-id="4d53b-237">모의 프레임 워크를 사용 하 여 테스트</span><span class="sxs-lookup"><span data-stu-id="4d53b-237">Testing with a mocking framework</span></span>](https://msdn.microsoft.com/data/dn314429)
- [<span data-ttu-id="4d53b-238">사용자 고유의 test double을 사용 하 여 테스트</span><span class="sxs-lookup"><span data-stu-id="4d53b-238">Testing with your own test doubles</span></span>](https://msdn.microsoft.com/data/dn314431)

<a id="proxies"></a>
## <a name="proxy-classes"></a><span data-ttu-id="4d53b-239">프록시 클래스</span><span class="sxs-lookup"><span data-stu-id="4d53b-239">Proxy classes</span></span>

<span data-ttu-id="4d53b-240">Entity Framework (예: 쿼리를 실행 하는 경우) 엔터티 인스턴스를 만들 때 종종 만듭니다는 엔터티에 대 한 프록시 역할을 동적으로 생성 된 파생 형식의 인스턴스 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-240">When the Entity Framework creates entity instances (for example, when you execute a query), it often creates them as instances of a dynamically generated derived type that acts as a proxy for the entity.</span></span> <span data-ttu-id="4d53b-241">예를 들어 다음 두 가지 디버거 이미지를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4d53b-241">For example, see the following two debugger images.</span></span> <span data-ttu-id="4d53b-242">첫 번째 이미지에 표시 하는 `student` 변수는 예상 된 `Student` 엔터티를 인스턴스화한 후에 즉시를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-242">In the first image, you see that the `student` variable is the expected `Student` type immediately after you instantiate the entity.</span></span> <span data-ttu-id="4d53b-243">두 번째 이미지에 EF 학생 엔터티는 데이터베이스에서 읽는 데 사용 된 프록시 클래스를 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-243">In the second image, after EF has been used to read a student entity from the database, you see the proxy class.</span></span>

![프록시 클래스 하기 전에](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

![프록시 클래스 후](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

<span data-ttu-id="4d53b-246">이 프록시 클래스 속성에 액세스할 때 자동으로 작업을 수행 하기 위한 후크를 삽입 하는 엔터티의 일부 가상 속성을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-246">This proxy class overrides some virtual properties of the entity to insert hooks for performing actions automatically when the property is accessed.</span></span> <span data-ttu-id="4d53b-247">하나의 함수에 대 한이 메커니즘을 사용 하는 지연 로드입니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-247">One function this mechanism is used for is lazy loading.</span></span>

<span data-ttu-id="4d53b-248">대부분의 프록시를 사용 하이 여가 주의 해야 할 필요 하지 않습니다 되지만 예외가:</span><span class="sxs-lookup"><span data-stu-id="4d53b-248">Most of the time you don't need to be aware of this use of proxies, but there are exceptions:</span></span>

- <span data-ttu-id="4d53b-249">일부 시나리오에서는 Entity Framework 프록시 인스턴스를 만들지 못하도록는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-249">In some scenarios you might want to prevent the Entity Framework from creating proxy instances.</span></span> <span data-ttu-id="4d53b-250">예를 들어 엔터티를 직렬화 하는 경우 일반적으로 POCO 클래스를 프록시 클래스가 아니라 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-250">For example, when you're serializing entities you generally want the POCO classes, not the proxy classes.</span></span> <span data-ttu-id="4d53b-251">에 표시 된 것 처럼 serialization 문제를 방지 하는 한 가지 방법은 데이터 전송 개체 (Dto) 대신 엔터티 개체를 serialize 하는 것은 [Entity Framework를 사용 하 여 웹 API를 사용 하 여](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-1.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-251">One way to avoid serialization problems is to serialize data transfer objects (DTOs) instead of entity objects, as shown in the [Using Web API with Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-1.md) tutorial.</span></span> <span data-ttu-id="4d53b-252">또 다른 방법은 [프록시 생성 기능을 해제](https://msdn.microsoft.com/data/jj592886.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-252">Another way is to [disable proxy creation](https://msdn.microsoft.com/data/jj592886.aspx).</span></span>
- <span data-ttu-id="4d53b-253">사용 하 여 엔터티 클래스를 인스턴스화하는 `new` 연산자, 프록시 인스턴스를 가져오지 않음.</span><span class="sxs-lookup"><span data-stu-id="4d53b-253">When you instantiate an entity class using the `new` operator, you don't get a proxy instance.</span></span> <span data-ttu-id="4d53b-254">즉, 변경 내용 추적을 지연 로드 및 자동과 같은 기능을 활용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-254">This means you don't get functionality such as lazy loading and automatic change tracking.</span></span> <span data-ttu-id="4d53b-255">이 일반적으로 알겠습니다. 일반적으로 필요 하지 않습니다 지연 로드는 데이터베이스에 없는 새 엔터티를 작성 하는 동안에 및 변경 내용 추적을으로 엔터티를 명시적으로 표시 하는 경우 일반적으로 필요 하지 않습니다 `Added`합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-255">This is typically okay; you generally don't need lazy loading, because you're creating a new entity that isn't in the database, and you generally don't need change tracking if you're explicitly marking the entity as `Added`.</span></span> <span data-ttu-id="4d53b-256">그러나 지연 로드 해야 하는 경우 필요한 변경 내용 추적을 만들 수 있습니다 새 엔터티 인스턴스를 사용 하 여 프록시는 [만들기](https://msdn.microsoft.com/library/gg679504.aspx) 의 메서드는 `DbSet` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-256">However, if you do need lazy loading and you need change tracking, you can create new entity instances with proxies using the [Create](https://msdn.microsoft.com/library/gg679504.aspx) method of the `DbSet` class.</span></span>
- <span data-ttu-id="4d53b-257">프록시 형식을에서 실제 엔터티 형식을 가져올 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-257">You might want to get an actual entity type from a proxy type.</span></span> <span data-ttu-id="4d53b-258">사용할 수는 [GetObjectType](https://msdn.microsoft.com/library/system.data.objects.objectcontext.getobjecttype.aspx) 의 메서드는 `ObjectContext` 클래스의 프록시 형식 인스턴스를 실제 엔터티 형식을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-258">You can use the [GetObjectType](https://msdn.microsoft.com/library/system.data.objects.objectcontext.getobjecttype.aspx) method of the `ObjectContext` class to get the actual entity type of a proxy type instance.</span></span>

<span data-ttu-id="4d53b-259">자세한 내용은 참조 [프록시 작업](https://msdn.microsoft.com/data/JJ592886.aspx) msdn 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-259">For more information, see [Working with Proxies](https://msdn.microsoft.com/data/JJ592886.aspx) on MSDN.</span></span>

<a id="changedetection"></a>
## <a name="automatic-change-detection"></a><span data-ttu-id="4d53b-260">자동 변경 내용 검색</span><span class="sxs-lookup"><span data-stu-id="4d53b-260">Automatic change detection</span></span>

<span data-ttu-id="4d53b-261">Entity Framework 엔터티의 현재 값과 원래 값을 비교 하 여 엔터티의 변경 된 방식을 (및 따라서로 업데이트를 데이터베이스에 전송 해야 할)를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-261">The Entity Framework determines how an entity has changed (and therefore which updates need to be sent to the database) by comparing the current values of an entity with the original values.</span></span> <span data-ttu-id="4d53b-262">엔터티 쿼리 하거나 연결 하는 경우 원래 값 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-262">The original values are stored when the entity is queried or attached.</span></span> <span data-ttu-id="4d53b-263">자동 변경 내용 검색 발생 하는 메서드 중 일부는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-263">Some of the methods that cause automatic change detection are the following:</span></span>

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

<span data-ttu-id="4d53b-264">많은 엔터티를 추적 하 고 있는 경우 루프에서 여러 번 다음이 방법 중 하나 호출 하면 변경 내용 자동 감지를 사용 하 여 일시적으로 해제 하 여 성능 향상을 발생할 수 있습니다는 [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled.aspx) 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-264">If you're tracking a large number of entities and you call one of these methods many times in a loop, you might get significant performance improvements by temporarily turning off automatic change detection using the [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled.aspx) property.</span></span> <span data-ttu-id="4d53b-265">자세한 내용은 참조 [자동으로 검색 되는 변경 내용을](https://msdn.microsoft.com/data/jj556205) msdn 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-265">For more information, see [Automatically Detecting Changes](https://msdn.microsoft.com/data/jj556205) on MSDN.</span></span>

<a id="validation"></a>
## <a name="automatic-validation"></a><span data-ttu-id="4d53b-266">자동 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="4d53b-266">Automatic validation</span></span>

<span data-ttu-id="4d53b-267">호출 하는 경우는 `SaveChanges` 메서드를 Entity Framework 기본적으로 모든 변경 된 엔터티의 모든 속성의 데이터를 하기 전에 유효성 검사 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-267">When you call the `SaveChanges` method, by default the Entity Framework validates the data in all properties of all changed entities before updating the database.</span></span> <span data-ttu-id="4d53b-268">많은 엔터티를 업데이트 한 및 이미이 작업은 필요 하지는 데이터를 확인 했으므로 있습니다 고 저장 프로세스를 만들 수는 경우 변경 내용을 유효성 검사를 일시적으로 해제 하 여 더 짧은 시간을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-268">If you've updated a large number of entities and you've already validated the data, this work is unnecessary and you could make the process of saving the changes take less time by temporarily turning off validation.</span></span> <span data-ttu-id="4d53b-269">사용 하 여 해당 하는 작업을 수행할 수는 [ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled.aspx) 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-269">You can do that using the [ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled.aspx) property.</span></span> <span data-ttu-id="4d53b-270">자세한 내용은 참조 [유효성 검사](https://msdn.microsoft.com/data/gg193959) msdn 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-270">For more information, see [Validation](https://msdn.microsoft.com/data/gg193959) on MSDN.</span></span>

<a id="tools"></a>
## <a name="entity-framework-power-tools"></a><span data-ttu-id="4d53b-271">Entity Framework 파워 도구</span><span class="sxs-lookup"><span data-stu-id="4d53b-271">Entity Framework Power Tools</span></span>

<span data-ttu-id="4d53b-272">[Entity Framework 파워 도구](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d) 이 자습서에 표시 된 Visual Studio 추가 기능에 데이터 모델 다이어그램을 만드는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-272">[Entity Framework Power Tools](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d) is a Visual Studio add-in that was used to create the data model diagrams shown in these tutorials.</span></span> <span data-ttu-id="4d53b-273">도구는 데이터베이스 Code First를 사용할 수 있도록 기존 데이터베이스의 테이블 기반 엔터티 클래스를 생성할와 같은 다른 함수를 수행할 수도 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-273">The tools can also do other function such as generate entity classes based on the tables in an existing database so that you can use the database with Code First.</span></span> <span data-ttu-id="4d53b-274">도구를 설치한 후에 몇 가지 추가 옵션이 상황에 맞는 메뉴에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-274">After you install the tools, some additional options appear in context menus.</span></span> <span data-ttu-id="4d53b-275">예를 들어 마우스 단추로 컨텍스트 클래스에서 **솔루션 탐색기**, 다이어그램을 생성 하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-275">For example, when you right-click your context class in **Solution Explorer**, you get an option to generate a diagram.</span></span> <span data-ttu-id="4d53b-276">Code First 사용 하는 경우는 다이어그램에 데이터 모델을 변경할 수 없습니다 되지만 보다 쉽게 이해할 수 있도록 작업을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-276">When you're using Code First you can't change the data model in the diagram, but you can move things around to make it easier to understand.</span></span>

![EF 상황에 맞는 메뉴](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image14.png)

![EF 다이어그램](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image15.png)

<a id="source"></a>
## <a name="entity-framework-source-code"></a><span data-ttu-id="4d53b-279">Entity Framework 소스 코드</span><span class="sxs-lookup"><span data-stu-id="4d53b-279">Entity Framework source code</span></span>

<span data-ttu-id="4d53b-280">Entity Framework 6에 대 한 소스 코드에서 제공 됩니다. [GitHub](https://github.com/aspnet/EntityFramework6)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-280">The source code for Entity Framework 6 is available at [GitHub](https://github.com/aspnet/EntityFramework6).</span></span> <span data-ttu-id="4d53b-281">버그를 보고할 수 있습니다 및 EF 소스 코드에 고유한 향상 된 기능에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-281">You can file bugs, and you can contribute your own enhancements to the EF source code.</span></span>

<span data-ttu-id="4d53b-282">소스 코드를 연 하지만 Entity Framework는 Microsoft 제품으로 완전히 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-282">Although the source code is open, Entity Framework is fully supported as a Microsoft product.</span></span> <span data-ttu-id="4d53b-283">Microsoft Entity Framework 팀 기여 허용 되는 제어를 유지 하 고 각 릴리스의 품질을 보장할 수 있는 모든 코드 변경 내용을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-283">The Microsoft Entity Framework team keeps control over which contributions are accepted and tests all code changes to ensure the quality of each release.</span></span>

<a id="summary"></a>
## <a name="summary"></a><span data-ttu-id="4d53b-284">요약</span><span class="sxs-lookup"><span data-stu-id="4d53b-284">Summary</span></span>

<span data-ttu-id="4d53b-285">이 일련의 ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하는 자습서를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-285">This completes this series of tutorials on using the Entity Framework in an ASP.NET MVC application.</span></span> <span data-ttu-id="4d53b-286">Entity Framework를 사용 하 여 데이터를 사용 하는 방법에 대 한 자세한 내용은 참조는 [msdn 설명서 페이지 EF](https://msdn.microsoft.com/data/ee712907) 및 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-286">For more information about how to work with data using the Entity Framework, see the [EF documentation page on MSDN](https://msdn.microsoft.com/data/ee712907) and [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

<span data-ttu-id="4d53b-287">작성 한 후 웹 응용 프로그램을 배포 하는 방법에 대 한 자세한 내용은 참조 하십시오. [권장 리소스-ASP.NET 웹 배포](../../../../whitepapers/aspnet-web-deployment-content-map.md) MSDN 라이브러리에서.</span><span class="sxs-lookup"><span data-stu-id="4d53b-287">For more information about how to deploy your web application after you've built it, see [ASP.NET Web Deployment - Recommended Resources](../../../../whitepapers/aspnet-web-deployment-content-map.md) in the MSDN Library.</span></span>

<span data-ttu-id="4d53b-288">인증 및 권한, 같은 MVC와 관련 된 다른 항목에 대 한 정보에 대 한 참조는 [ASP.NET MVC-권장 리소스](../recommended-resources-for-mvc.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-288">For information about other topics related to MVC, such as authentication and authorization, see the [ASP.NET MVC - Recommended Resources](../recommended-resources-for-mvc.md).</span></span>

<a id="acknowledgments"></a>
## <a name="acknowledgments"></a><span data-ttu-id="4d53b-289">승인</span><span class="sxs-lookup"><span data-stu-id="4d53b-289">Acknowledgments</span></span>

- <span data-ttu-id="4d53b-290">Tom Dykstra이이 자습서의 원래 버전을 작성 하려면 공동 EF 5 업데이트를 작성 하 고 EF 6 업데이트를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-290">Tom Dykstra wrote the original version of this tutorial, co-authored the EF 5 update, and wrote the EF 6 update.</span></span> <span data-ttu-id="4d53b-291">Tom은 Microsoft 웹 플랫폼 및 도구 콘텐츠 팀의 수석 프로그래밍 기록기입니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-291">Tom is a senior programming writer on the Microsoft Web Platform and Tools Content Team.</span></span>
- <span data-ttu-id="4d53b-292">[Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [ @RickAndMSFT ](http://twitter.com/RickAndMSFT)) 대부분의 자습서 5 EF 및 MVC 4에 대 한 업데이트 작업을 함께 EF 6 업데이트를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-292">[Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) did most of the work updating the tutorial for EF 5 and MVC 4 and co-authored the EF 6 update.</span></span> <span data-ttu-id="4d53b-293">Rick microsoft Azure 및 MVC에 중점을 두기 수석 프로그래밍 기록기입니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-293">Rick is a senior programming writer for Microsoft focusing on Azure and MVC.</span></span>
- <span data-ttu-id="4d53b-294">[Rowan Miller](http://www.romiller.com) 및 Entity Framework 팀의 다른 멤버가 코드 검토를 지 원하는 많은 म 자습서 EF 5 및 EF 6에 대 한 업데이트 하는 동안 발생 하는 마이그레이션 문제를 디버그 하는 데 도움을 준 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-294">[Rowan Miller](http://www.romiller.com) and other members of the Entity Framework team assisted with code reviews and helped debug many issues with migrations that arose while we were updating the tutorial for EF 5 and EF 6.</span></span>

<a id="vb"></a>
## <a name="vb"></a><span data-ttu-id="4d53b-295">VB</span><span class="sxs-lookup"><span data-stu-id="4d53b-295">VB</span></span>

<span data-ttu-id="4d53b-296">자습서 EF 4.1에 대 한 원래 생성 되었지만 다운로드 완료 된 프로젝트의 C# 및 VB 버전을 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-296">When the tutorial was originally produced for EF 4.1, we provided both C# and VB versions of the completed download project.</span></span> <span data-ttu-id="4d53b-297">시간 제한 및 기타 우선 순위의 인해 म 수행 하지 않은 하는이 버전에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-297">Due to time limitations and other priorities we have not done that for this version.</span></span> <span data-ttu-id="4d53b-298">VB 프로젝트의 경우 이러한 자습서를 사용 하 여 작성 하 고 다른 사용자와 공유 하려는, 알려 주시면 하려고 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-298">If you build a VB project using these tutorials and would be willing to share that with others, please let us know.</span></span>

<a id="errors"></a>
## <a name="common-errors-and-solutions-or-workarounds-for-them"></a><span data-ttu-id="4d53b-299">일반적인 오류 해결 방법 또는을</span><span class="sxs-lookup"><span data-stu-id="4d53b-299">Common errors, and solutions or workarounds for them</span></span>

### <a name="cannot-createshadow-copy"></a><span data-ttu-id="4d53b-300">복사본을 만들어 섀도 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-300">Cannot create/shadow copy</span></span>

<span data-ttu-id="4d53b-301">오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="4d53b-301">Error Message:</span></span>

> <span data-ttu-id="4d53b-302">복사본을 만들어 섀도 수 없습니다 '&lt;filename&gt;' 파일이 이미 있으므로 시기입니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-302">Cannot create/shadow copy '&lt;filename&gt;' when that file already exists.</span></span>


<span data-ttu-id="4d53b-303">솔루션</span><span class="sxs-lookup"><span data-stu-id="4d53b-303">Solution</span></span>

<span data-ttu-id="4d53b-304">몇 초 정도 기다린 페이지를 새로 고 치세요.</span><span class="sxs-lookup"><span data-stu-id="4d53b-304">Wait a few seconds and refresh the page.</span></span>

### <a name="update-database-not-recognized"></a><span data-ttu-id="4d53b-305">데이터베이스 업데이트 인식 되지 않습니다</span><span class="sxs-lookup"><span data-stu-id="4d53b-305">Update-Database not recognized</span></span>

<span data-ttu-id="4d53b-306">오류 메시지 (에서 `Update-Database` 의 PMC 명령을):</span><span class="sxs-lookup"><span data-stu-id="4d53b-306">Error Message (from the `Update-Database` command in the PMC):</span></span>

> <span data-ttu-id="4d53b-307">' Update-database ' 용어는 cmdlet, 함수, 스크립트 파일 또는 실행 프로그램의 이름으로 인식할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-307">The term 'Update-Database' is not recognized as the name of a cmdlet, function, script file, or operable program.</span></span> <span data-ttu-id="4d53b-308">이름의 철자를 확인 하거나 경로가 포함 된, 하는 경우 경로가 정확한 지 확인 하 고 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4d53b-308">Check the spelling of the name, or if a path was included, verify that the path is correct and try again.</span></span>


<span data-ttu-id="4d53b-309">솔루션</span><span class="sxs-lookup"><span data-stu-id="4d53b-309">Solution</span></span>

<span data-ttu-id="4d53b-310">Visual Studio를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-310">Exit Visual Studio.</span></span> <span data-ttu-id="4d53b-311">프로젝트를 열어야 하 고 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4d53b-311">Reopen project and try again.</span></span>

### <a name="validation-failed"></a><span data-ttu-id="4d53b-312">유효성 검사 실패</span><span class="sxs-lookup"><span data-stu-id="4d53b-312">Validation failed</span></span>

<span data-ttu-id="4d53b-313">오류 메시지 (에서 `Update-Database` 의 PMC 명령을):</span><span class="sxs-lookup"><span data-stu-id="4d53b-313">Error Message (from the `Update-Database` command in the PMC):</span></span>

> <span data-ttu-id="4d53b-314">하나 이상의 엔터티에 대해 유효성 검사가 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-314">Validation failed for one or more entities.</span></span> <span data-ttu-id="4d53b-315">자세한 내용은 'EntityValidationErrors' 속성을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4d53b-315">See 'EntityValidationErrors' property for more details.</span></span>


<span data-ttu-id="4d53b-316">솔루션</span><span class="sxs-lookup"><span data-stu-id="4d53b-316">Solution</span></span>

<span data-ttu-id="4d53b-317">이러한 문제가 발생 한 유효성 검사 오류는 경우는 `Seed` 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-317">One cause of this problem is validation errors when the `Seed` method runs.</span></span> <span data-ttu-id="4d53b-318">참조 [Seeding 및 디버깅 Entity Framework (EF)](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) 디버깅에 대 한 팁은 `Seed` 메서드.</span><span class="sxs-lookup"><span data-stu-id="4d53b-318">See [Seeding and Debugging Entity Framework (EF) DBs](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) for tips on debugging the `Seed` method.</span></span>

### <a name="http-50019-error"></a><span data-ttu-id="4d53b-319">HTTP 500.19 오류</span><span class="sxs-lookup"><span data-stu-id="4d53b-319">HTTP 500.19 error</span></span>

<span data-ttu-id="4d53b-320">오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="4d53b-320">Error Message:</span></span>

> <span data-ttu-id="4d53b-321">HTTP 오류 500.19-내부 서버 오류</span><span class="sxs-lookup"><span data-stu-id="4d53b-321">HTTP Error 500.19 - Internal Server Error</span></span>  
> <span data-ttu-id="4d53b-322">요청 된 페이지의 페이지에 대 한 관련된 구성 데이터가 잘못 되어 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-322">The requested page cannot be accessed because the related configuration data for the page is invalid.</span></span>


<span data-ttu-id="4d53b-323">솔루션</span><span class="sxs-lookup"><span data-stu-id="4d53b-323">Solution</span></span>

<span data-ttu-id="4d53b-324">이 오류가 발생 하는 한 가지 방법은 각각 동일한 포트 번호를 사용 하 여 솔루션의 여러 복사본이 있는 것은 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-324">One way you can get this error is from having multiple copies of the solution, each of them using the same port number.</span></span> <span data-ttu-id="4d53b-325">일반적으로 Visual Studio의 모든 인스턴스를 종료 한 다음에 작업 중인 프로젝트를 다시 시작 하 여이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-325">You can usually solve this problem by exiting all instances of Visual Studio, then restarting the project you're working on.</span></span> <span data-ttu-id="4d53b-326">그래도 문제가 해결 되지 포트 번호를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-326">If that doesn't work, try changing the port number.</span></span> <span data-ttu-id="4d53b-327">프로젝트 파일을 마우스 오른쪽 단추로 클릭 하 고 properties를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-327">Right click on the project file and then click properties.</span></span> <span data-ttu-id="4d53b-328">선택 된 **웹** 탭 한 다음에 포트 번호를 변경는 **프로젝트 Url** 입력란.</span><span class="sxs-lookup"><span data-stu-id="4d53b-328">Select the **Web** tab and then change the port number in the **Project Url** text box.</span></span>

### <a name="error-locating-sql-server-instance"></a><span data-ttu-id="4d53b-329">오류 찾기 SQL Server 인스턴스</span><span class="sxs-lookup"><span data-stu-id="4d53b-329">Error locating SQL Server instance</span></span>

<span data-ttu-id="4d53b-330">오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="4d53b-330">Error Message:</span></span>

> <span data-ttu-id="4d53b-331">SQL Server에 연결을 설정 하는 동안 네트워크 관련 또는 인스턴스 관련 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-331">A network-related or instance-specific error occurred while establishing a connection to SQL Server.</span></span> <span data-ttu-id="4d53b-332">서버를 찾을 수 없거나 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-332">The server was not found or was not accessible.</span></span> <span data-ttu-id="4d53b-333">인스턴스 이름이 올바르고 SQL Server가 원격 연결을 허용하도록 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-333">Verify that the instance name is correct and that SQL Server is configured to allow remote connections.</span></span> <span data-ttu-id="4d53b-334">(공급자: SQL 네트워크 인터페이스, 오류: 26-서버/인스턴스 지정 된 찾기 오류)</span><span class="sxs-lookup"><span data-stu-id="4d53b-334">(provider: SQL Network Interfaces, error: 26 - Error Locating Server/Instance Specified)</span></span>


<span data-ttu-id="4d53b-335">솔루션</span><span class="sxs-lookup"><span data-stu-id="4d53b-335">Solution</span></span>

<span data-ttu-id="4d53b-336">연결 문자열을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-336">Check the connection string.</span></span> <span data-ttu-id="4d53b-337">데이터베이스를 수동으로 삭제 하는 경우 생성 문자열에 데이터베이스의 이름을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d53b-337">If you have manually deleted the database, change the name of the database in the construction string.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="4d53b-338">이전</span><span class="sxs-lookup"><span data-stu-id="4d53b-338">Previous</span></span>](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
