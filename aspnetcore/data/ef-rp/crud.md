---
title: "EF 코어 8-CRUD-2 사용 하 여 razor 페이지"
author: rick-anderson
description: "만들기, 읽기, 업데이트, EF 코어를 삭제 하는 방법을 보여 줍니다."
keywords: "ASP.NET Core, Entity Framework Core, CRUD, 만들기, 읽기, 업데이트, 삭제"
ms.author: riande
manager: wpickett
ms.date: 10/15/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-rp/crud
ms.openlocfilehash: 410829608540697ac4563f1399c8e72d28a13cf2
ms.sourcegitcommit: 703593d5fd14076e79be2ba75a5b8da12a60ab15
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="create-read-update-and-delete---ef-core-with-razor-pages-2-of-8"></a><span data-ttu-id="30721-104">만들기, 읽기, 업데이트 및 삭제-EF 코어 Razor 페이지 (2 / 8)</span><span class="sxs-lookup"><span data-stu-id="30721-104">Create, Read, Update, and Delete - EF Core with Razor Pages (2 of 8)</span></span>

<span data-ttu-id="30721-105">여 [Tom Dykstra](https://github.com/tdykstra), [Jon P Smith](https://twitter.com/thereformedprog), 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="30721-105">By [Tom Dykstra](https://github.com/tdykstra), [Jon P Smith](https://twitter.com/thereformedprog), and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE[about the series](../../includes/RP-EF/intro.md)]

<span data-ttu-id="30721-106">이 자습서에서는 스 캐 폴드 CRUD (만들기, 읽기, 업데이트, 삭제) 코드 검토 및 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-106">In this tutorial, the scaffolded CRUD (create, read, update, delete) code is reviewed and customized.</span></span>

<span data-ttu-id="30721-107">참고: 복잡성을 최소화 하 고 이러한 자습서 EF 코어 데 초점을 유지 하려면 EF 핵심 코드 Razor 페이지 코드 숨김 파일에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30721-107">Note: To minimize complexity and keep these tutorials focused on EF Core, EF Core code is used in the Razor Pages code-behind files.</span></span> <span data-ttu-id="30721-108">일부 개발자는 UI (Razor 페이지) 및 데이터 액세스 계층 간에 추상화 계층을 작성할에서 서비스 계층 또는 리포지토리 패턴을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-108">Some developers use a service layer or repository pattern in to create an abstraction layer between the UI (Razor Pages) and the data access layer.</span></span>

<span data-ttu-id="30721-109">이 자습서, 만들기, 편집, 삭제 및의 세부 정보 Razor 페이지에는 *학생* 폴더 수정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30721-109">In this tutorial, the Create, Edit, Delete, and Details Razor Pages in the *Student* folder are modified.</span></span>

<span data-ttu-id="30721-110">스 캐 폴드 코드 페이지를 만들기, 편집 및 삭제에 대 한 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-110">The scaffolded code uses the following pattern for Create, Edit, and Delete pages:</span></span>

* <span data-ttu-id="30721-111">Get 및 HTTP GET 메서드와 함께 요청 된 데이터를 표시할 `OnGetAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-111">Get and display the requested data with the HTTP GET method `OnGetAsync`.</span></span>
* <span data-ttu-id="30721-112">HTTP POST 메서드를 사용 된 데이터의 변경 내용을 저장 `OnPostAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-112">Save changes to the data with the HTTP POST method `OnPostAsync`.</span></span>

<span data-ttu-id="30721-113">인덱스 및 세부 정보 페이지를 가져와 HTTP GET 메서드와 함께 요청된 된 데이터를 표시 합니다.`OnGetAsync`</span><span class="sxs-lookup"><span data-stu-id="30721-113">The Index and Details pages get and display the requested data with the HTTP GET method `OnGetAsync`</span></span>

## <a name="replace-singleordefaultasync-with-firstordefaultasync"></a><span data-ttu-id="30721-114">FirstOrDefaultAsync SingleOrDefaultAsync 대체</span><span class="sxs-lookup"><span data-stu-id="30721-114">Replace SingleOrDefaultAsync with FirstOrDefaultAsync</span></span>

<span data-ttu-id="30721-115">생성 된 코드를 사용 하 여 [SingleOrDefaultAsync](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.singleordefaultasync?view=efcore-2.0#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_SingleOrDefaultAsync__1_System_Linq_IQueryable___0__System_Linq_Expressions_Expression_System_Func___0_System_Boolean___System_Threading_CancellationToken_) 를 요청한 엔터티를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="30721-115">The generated code uses [SingleOrDefaultAsync](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.singleordefaultasync?view=efcore-2.0#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_SingleOrDefaultAsync__1_System_Linq_IQueryable___0__System_Linq_Expressions_Expression_System_Func___0_System_Boolean___System_Threading_CancellationToken_)  to fetch the requested entity.</span></span> <span data-ttu-id="30721-116">[FirstOrDefaultAsync](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.firstordefaultasync?view=efcore-2.0#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_FirstOrDefaultAsync__1_System_Linq_IQueryable___0__System_Threading_CancellationToken_) 하나의 엔터티가 인출에서 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="30721-116">[FirstOrDefaultAsync](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.firstordefaultasync?view=efcore-2.0#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_FirstOrDefaultAsync__1_System_Linq_IQueryable___0__System_Threading_CancellationToken_) is more efficient at fetching one entity:</span></span>

* <span data-ttu-id="30721-117">되었는지 확인 하 고 코드에 필요한 경우가 아니면 않습니다는 쿼리에서 반환 되는 둘 이상의 엔터티.</span><span class="sxs-lookup"><span data-stu-id="30721-117">Unless the code needs to verify that there is not more than one entity returned from the query.</span></span> 
* <span data-ttu-id="30721-118">`SingleOrDefaultAsync`더 많은 데이터를 인출 하 고 불필요 한 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-118">`SingleOrDefaultAsync` fetches more data and does unnecessary work.</span></span>
* <span data-ttu-id="30721-119">`SingleOrDefaultAsync`필터 부분에 맞는 둘 이상의 엔터티인 경우 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-119">`SingleOrDefaultAsync` throws an exception if there is more than one entity that fits the filter part.</span></span>
*  <span data-ttu-id="30721-120">`FirstOrDefaultAsync`둘 이상의 엔터티 필터 부분에 맞는 경우 throw 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30721-120">`FirstOrDefaultAsync` doesn't throw if there is more than one entity that fits the filter part.</span></span>

<span data-ttu-id="30721-121">전역으로 대체 `SingleOrDefaultAsync` 와 `FirstOrDefaultAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-121">Globally replace `SingleOrDefaultAsync` with `FirstOrDefaultAsync`.</span></span> <span data-ttu-id="30721-122">`SingleOrDefaultAsync`5 위치에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30721-122">`SingleOrDefaultAsync` is used in 5 places:</span></span>

* <span data-ttu-id="30721-123">`OnGetAsync`세부 정보 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="30721-123">`OnGetAsync` in the Details page.</span></span>
* <span data-ttu-id="30721-124">`OnGetAsync`및 `OnPostAsync` 편집 및 삭제 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30721-124">`OnGetAsync` and `OnPostAsync` in the Edit and Delete pages.</span></span>

<a name="FindAsync"></a>
### <a name="findasync"></a><span data-ttu-id="30721-125">FindAsync</span><span class="sxs-lookup"><span data-stu-id="30721-125">FindAsync</span></span>

<span data-ttu-id="30721-126">스 캐 폴드 코드의 대부분에서 [FindAsync](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.dbcontext.findasync?view=efcore-2.0#Microsoft_EntityFrameworkCore_DbContext_FindAsync_System_Type_System_Object___) 대신 사용할 수 `FirstOrDefaultAsync` 또는 `SingleOrDefaultAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-126">In much of the scaffolded code, [FindAsync](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.dbcontext.findasync?view=efcore-2.0#Microsoft_EntityFrameworkCore_DbContext_FindAsync_System_Type_System_Object___) can be used in place of `FirstOrDefaultAsync` or `SingleOrDefaultAsync`.</span></span> 

<span data-ttu-id="30721-127">`FindAsync`:</span><span class="sxs-lookup"><span data-stu-id="30721-127">`FindAsync`:</span></span>

* <span data-ttu-id="30721-128">기본 키 (PK)가 있는 엔터티를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="30721-128">Finds an entity with the primary key (PK).</span></span> <span data-ttu-id="30721-129">PK가 있는 엔터티를 컨텍스트에 의해 추적 되 고, 요청 없이 DB에 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30721-129">If an entity with the PK is being tracked by the context, it is returned without a request to the DB.</span></span>
* <span data-ttu-id="30721-130">단순 하 고 간결 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-130">Is simple and concise.</span></span>
* <span data-ttu-id="30721-131">단일 엔터티를 조회 하도록 최적화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30721-131">Is optimized to look up a single entity.</span></span>
* <span data-ttu-id="30721-132">수에 따라서는 성능 이점이 있지만 일반 웹 시나리오에 대 한 재생이 거의 발휘 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-132">Can have perf benefits in some situations, but they rarely come into play for normal web scenarios.</span></span>
* <span data-ttu-id="30721-133">암시적으로 사용 하 여 [FirstAsync](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.firstasync?view=efcore-2.0#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_FirstAsync__1_System_Linq_IQueryable___0__System_Linq_Expressions_Expression_System_Func___0_System_Boolean___System_Threading_CancellationToken_) 대신 [SingleAsync](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.singleasync?view=efcore-2.0#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_SingleAsync__1_System_Linq_IQueryable___0__System_Linq_Expressions_Expression_System_Func___0_System_Boolean___System_Threading_CancellationToken_)합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-133">Implicitly uses [FirstAsync](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.firstasync?view=efcore-2.0#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_FirstAsync__1_System_Linq_IQueryable___0__System_Linq_Expressions_Expression_System_Func___0_System_Boolean___System_Threading_CancellationToken_) instead of [SingleAsync](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.singleasync?view=efcore-2.0#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_SingleAsync__1_System_Linq_IQueryable___0__System_Linq_Expressions_Expression_System_Func___0_System_Boolean___System_Threading_CancellationToken_).</span></span>
<span data-ttu-id="30721-134">하지만 다른 엔터티를 포함 하려는 경우 찾기는 더 이상 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-134">But if you want to Include other entities, then Find is no longer appropriate.</span></span> <span data-ttu-id="30721-135">즉, 찾기 취소 하 고 앱 진행 됨에 따라 쿼리를 이동 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30721-135">This means that you may need to abandon Find and move to a query as your app progresses.</span></span>

## <a name="customize-the-details-page"></a><span data-ttu-id="30721-136">사용자 지정 세부 정보 페이지</span><span class="sxs-lookup"><span data-stu-id="30721-136">Customize the Details page</span></span>

<span data-ttu-id="30721-137">찾아 `Pages/Students` 페이지.</span><span class="sxs-lookup"><span data-stu-id="30721-137">Browse to `Pages/Students` page.</span></span> <span data-ttu-id="30721-138">**편집**, **세부 정보**, 및 **삭제** 에 의해 생성 된 링크는 [앵커 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper) 에 *페이지/학생 / Index.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="30721-138">The **Edit**, **Details**, and **Delete** links are generated by the [Anchor Tag Helper](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper) in the *Pages/Students/Index.cshtml* file.</span></span>

[!code-cshtml[Main](intro/samples/cu/Pages/Students/Index1.cshtml?range=40-44)]

<span data-ttu-id="30721-139">세부 정보 링크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-139">Select a Details link.</span></span> <span data-ttu-id="30721-140">폼의 URL은 `http://localhost:5000/Students/Details?id=2`합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-140">The URL is of the form `http://localhost:5000/Students/Details?id=2`.</span></span> <span data-ttu-id="30721-141">쿼리 문자열을 사용 하 여 전달 된 학생 ID (`?id=2`).</span><span class="sxs-lookup"><span data-stu-id="30721-141">The Student ID is passed using a query string (`?id=2`).</span></span>

<span data-ttu-id="30721-142">업데이트 편집, 정보 및 Razor 페이지 삭제 사용 하는 `"{id:int}"` 경로 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="30721-142">Update the Edit, Details, and Delete Razor Pages to use the `"{id:int}"` route template.</span></span> <span data-ttu-id="30721-143">이러한 각 페이지에 대한 page 지시문을 `@page`에서 `@page "{id:int}"`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-143">Change the page directive for each of these pages from `@page` to `@page "{id:int}"`.</span></span>

<span data-ttu-id="30721-144">요청을 수행 하는 "{id: int}" 경로 템플릿 사용 하 여 페이지 **하지** 정수 경로 값 반환 HTTP 404 (찾을 수 없음) 오류를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-144">A request to the page with the "{id:int}" route template that does **not** include a integer route value returns an HTTP 404 (not found) error.</span></span> <span data-ttu-id="30721-145">예를 들어 `http://localhost:5000/Students/Details` 404 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-145">For example, `http://localhost:5000/Students/Details` returns a 404 error.</span></span> <span data-ttu-id="30721-146">ID를 옵션으로 설정하려면 경로 제약 조건에 `?`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-146">To make the ID optional, append `?` to the route constraint:</span></span>

 ```cshtml
@page "{id:int?}"
```

<span data-ttu-id="30721-147">응용 프로그램을 실행 세부 정보 링크를 클릭 하 고 URL 경로 데이터로 ID 전달 확인 (`http://localhost:5000/Students/Details/2`).</span><span class="sxs-lookup"><span data-stu-id="30721-147">Run the app, click on a Details link, and verify the URL is passing the ID as route data (`http://localhost:5000/Students/Details/2`).</span></span>

<span data-ttu-id="30721-148">전역으로 변경 하지 않는 `@page` 를 `@page "{id:int}"`, 끊어집니다 홈에 대 한 링크를 수행 하 고 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30721-148">Don't globally change `@page` to `@page "{id:int}"`, doing so breaks the links to the Home and Create pages.</span></span>

<!-- See https://github.com/aspnet/Scaffolding/issues/590 -->

### <a name="add-related-data"></a><span data-ttu-id="30721-149">관련된 데이터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-149">Add related data</span></span>

<span data-ttu-id="30721-150">학생 인덱스 페이지에 대 한 스 캐 폴드 코드에는 포함 된 `Enrollments` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="30721-150">The scaffolded code for the Students Index page does not include the `Enrollments` property.</span></span> <span data-ttu-id="30721-151">이 섹션의 내용에는 `Enrollments` 컬렉션 세부 정보 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30721-151">In this section, the contents of the `Enrollments` collection is displayed in the Details page.</span></span>

<span data-ttu-id="30721-152">`OnGetAsync` 방식의 *Pages/Students/Details.cshtml.cs* 사용 하 여는 `FirstOrDefaultAsync` 메서드는 단일 검색를 `Student` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="30721-152">The `OnGetAsync` method of *Pages/Students/Details.cshtml.cs* uses the `FirstOrDefaultAsync` method to retrieve a single `Student` entity.</span></span> <span data-ttu-id="30721-153">다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-153">Add the following highlighted code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Students/Details.cshtml.cs?name=snippet_Details&highlight=8-12)]

<span data-ttu-id="30721-154">`Include` 및 `ThenInclude` 메서드 인해 로드 컨텍스트는 `Student.Enrollments` 탐색 속성 및 각 등록 내는 `Enrollment.Course` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="30721-154">The `Include` and `ThenInclude` methods cause the context to load the `Student.Enrollments` navigation property, and within each enrollment the `Enrollment.Course` navigation property.</span></span> <span data-ttu-id="30721-155">이러한 메서드는 데이터 읽기 관련 자습서에서 자세히 examinied 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30721-155">These methods are examinied in detail in the reading-related data tutorial.</span></span>

<span data-ttu-id="30721-156">`AsNoTracking` 메서드는 현재 컨텍스트에서 업데이트 되지 않습니다는 엔터티 반환 될 때 시나리오의 성능을 향상 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="30721-156">The `AsNoTracking` method improves performance in scenarios when the entities returned are not updated in the current context.</span></span> <span data-ttu-id="30721-157">`AsNoTracking`이 자습서의 뒷부분에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-157">`AsNoTracking` is discussed later in this tutorial.</span></span>

### <a name="display-related-enrollments-on-the-details-page"></a><span data-ttu-id="30721-158">관련된 등록 세부 정보 페이지에 표시</span><span class="sxs-lookup"><span data-stu-id="30721-158">Display related enrollments on the Details page</span></span>

<span data-ttu-id="30721-159">열기 *Pages/Students/Details.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-159">Open *Pages/Students/Details.cshtml*.</span></span> <span data-ttu-id="30721-160">등록의 목록을 표시 하려면 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-160">Add the following highlighted code to display a list of enrollments:</span></span>

 <!--2do ricka. if doesn't change, remove dup -->
[!code-cshtml[Main](intro/samples/cu/Pages/Students/Details1.cshtml?highlight=35-53)]

<span data-ttu-id="30721-161">코드 들여쓰기 된 코드를 붙여 넣는 후 잘못 된 경우 CTRL-K-D를 수정한 후에 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="30721-161">If code indentation is wrong after the code is pasted, press CTRL-K-D to correct it.</span></span>

<span data-ttu-id="30721-162">위의 코드에서 엔터티는 반복의 `Enrollments` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="30721-162">The preceding code loops through the entities in the `Enrollments` navigation property.</span></span> <span data-ttu-id="30721-163">각 등록 과정 제목과 등급 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-163">For each enrollment, it displays the course title and the grade.</span></span> <span data-ttu-id="30721-164">에 저장 된 과정 엔터티에서 과정 이름을 검색 하는 `Course` 등록 엔터티의 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="30721-164">The course title is retrieved from the Course entity that's stored in the `Course` navigation property of the Enrollments entity.</span></span>

<span data-ttu-id="30721-165">응용 프로그램을 실행, 선택는 **학생** 탭을 클릭는 **세부 정보** 학생에 대 한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="30721-165">Run the app, select the **Students** tab, and click the **Details** link for a student.</span></span> <span data-ttu-id="30721-166">Courses 및 선택한 학생에 대 한 등급의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30721-166">The list of courses and grades for the selected student is displayed.</span></span>

## <a name="update-the-create-page"></a><span data-ttu-id="30721-167">업데이트 만들기 페이지</span><span class="sxs-lookup"><span data-stu-id="30721-167">Update the Create page</span></span>

<span data-ttu-id="30721-168">업데이트는 `OnPostAsync` 메서드에서 *Pages/Students/Create.cshtml.cs* 를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="30721-168">Update the `OnPostAsync` method in *Pages/Students/Create.cshtml.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Students/Create.cshtml.cs?name=snippet_OnPostAsync)]

<a name="TryUpdateModelAsync"></a>
### <a name="tryupdatemodelasync"></a><span data-ttu-id="30721-169">TryUpdateModelAsync</span><span class="sxs-lookup"><span data-stu-id="30721-169">TryUpdateModelAsync</span></span>

<span data-ttu-id="30721-170">검사는 [TryUpdateModelAsync](https://docs.microsoft.com/ dotnet/api/microsoft.aspnetcore.mvc.controllerbase.tryupdatemodelasync?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_ControllerBase_TryUpdateModelAsync_System_Object_System_Type_System_String_) 코드:</span><span class="sxs-lookup"><span data-stu-id="30721-170">Examine the [TryUpdateModelAsync](https://docs.microsoft.com/ dotnet/api/microsoft.aspnetcore.mvc.controllerbase.tryupdatemodelasync?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_ControllerBase_TryUpdateModelAsync_System_Object_System_Type_System_String_) code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Students/Create.cshtml.cs?name=snippet_TryUpdateModelAsync)]

<span data-ttu-id="30721-171">위의 코드에서 `TryUpdateModelAsync<Student>` 에서 업데이트 하는 `emptyStudent` 개체에서 게시 된 양식 값을 사용 하 여는 [PageContext](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel.pagecontext?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_RazorPages_PageModel_PageContext) 속성에는 [PageModel](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel?view=aspnetcore-2.0)합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-171">In the preceding code, `TryUpdateModelAsync<Student>` tries to update the `emptyStudent` object using the posted form values from the [PageContext](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel.pagecontext?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_RazorPages_PageModel_PageContext) property in the [PageModel](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel?view=aspnetcore-2.0).</span></span> <span data-ttu-id="30721-172">`TryUpdateModelAsync`나열 된 속성에만 업데이트 (`s => s.FirstMidName, s => s.LastName, s => s.EnrollmentDate`).</span><span class="sxs-lookup"><span data-stu-id="30721-172">`TryUpdateModelAsync` only updates the properties listed (`s => s.FirstMidName, s => s.LastName, s => s.EnrollmentDate`).</span></span>

<span data-ttu-id="30721-173">앞의 예제:</span><span class="sxs-lookup"><span data-stu-id="30721-173">In the preceding sample:</span></span>

* <span data-ttu-id="30721-174">두 번째 인수 (` "student", // Prefix`)는 접두사 값을 조회 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-174">The second argument (` "student", // Prefix`) is the prefix uses to look up values.</span></span> <span data-ttu-id="30721-175">대/소문자 구분 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30721-175">It's not case sensitive.</span></span>
* <span data-ttu-id="30721-176">게시 된 양식 값의 형식으로 변환 됩니다는 `Student` 를 사용 하 여 모델 [모델 바인딩](xref:mvc/models/model-binding#how-model-binding-works)합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-176">The posted form values are converted to the types in the `Student` model using [model binding](xref:mvc/models/model-binding#how-model-binding-works).</span></span>

<a id="overpost"></a>
### <a name="overposting"></a><span data-ttu-id="30721-177">초과 게시</span><span class="sxs-lookup"><span data-stu-id="30721-177">Overposting</span></span>

<span data-ttu-id="30721-178">사용 하 여 `TryUpdateModel` overposting 못하기 때문에 보안 모범 사례 게시 된 값이 포함 된 필드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-178">Using `TryUpdateModel` to update fields with posted values is a security best practice because it prevents overposting.</span></span> <span data-ttu-id="30721-179">예를 들어, 학생 엔터티를 포함 한 `Secret` 속성을이 웹 페이지를 업데이트 하거나 추가 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30721-179">For example, suppose the Student entity includes a `Secret` property that this web page should not update or add:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/StudentZsecret.cs?name=snippet_Intro&highlight=7)]

<span data-ttu-id="30721-180">앱에 없는 경우에 한 `Secret` 필드 만들기/업데이트 해커가 Razor 페이지에서 설정할 수는 `Secret` 초과 게시 값입니다.</span><span class="sxs-lookup"><span data-stu-id="30721-180">Even if the app doesn't have a `Secret` field on the create/update Razor Page, a hacker could set the `Secret` value by overposting.</span></span> <span data-ttu-id="30721-181">해커가 Fiddler와 같은 도구를 사용 하거나 게시 하려면 일부 JavaScript 작성 한 `Secret` 값을 형성 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-181">A hacker could use a tool such as Fiddler, or write some JavaScript, to post a `Secret` form value.</span></span> <span data-ttu-id="30721-182">원본 코드 학생 인스턴스를 만들 때 모델 바인더를 사용 하는 필드를 제한 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30721-182">The original code doesn't limit the fields that the model binder uses when it creates a Student instance.</span></span>

<span data-ttu-id="30721-183">어떤 값에 대해 지정 된 해커가 `Secret` 양식 필드 DB에서 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30721-183">Whatever value the hacker specified for the `Secret` form field is updated in the DB.</span></span> <span data-ttu-id="30721-184">다음 이미지에서는 Fiddler 도구 추가 보여 줍니다.는 `Secret` 게시 된 양식 값을 필드 (값 "OverPost")을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-184">The following image shows the Fiddler tool adding the `Secret` field (with the value "OverPost") to the posted form values.</span></span>

![암호 필드를 추가 하는 fiddler](../ef-mvc/crud/_static/fiddler.png)

<span data-ttu-id="30721-186">값 "OverPost"에 성공적으로 추가 되는 `Secret` 삽입된 된 행의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="30721-186">The value "OverPost" is successfully added to the `Secret` property of the inserted row.</span></span> <span data-ttu-id="30721-187">의도 하지 않은 응용 프로그램 디자이너는 `Secret` 속성을 만들기 페이지를 사용 하 여 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-187">The app designer never intended the `Secret` property to be set with the Create page.</span></span>

<a name="vm"></a>
### <a name="view-model"></a><span data-ttu-id="30721-188">뷰 모델</span><span class="sxs-lookup"><span data-stu-id="30721-188">View model</span></span>

<span data-ttu-id="30721-189">뷰 모델은 일반적으로 응용 프로그램에서 사용 되는 모델에 포함 된 속성의 하위 집합을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-189">A view model typically contains a subset of the properties included in the model used by the application.</span></span> <span data-ttu-id="30721-190">응용 프로그램 모델에는 도메인 모델을 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-190">The application model is often called the domain model.</span></span> <span data-ttu-id="30721-191">일반적으로 도메인 모델의 해당 엔터티 db에서에 필요한 모든 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-191">The domain model typically contains all the properties required by the corresponding entity in the DB.</span></span> <span data-ttu-id="30721-192">뷰 모델 (예를 들어 만들기 페이지) UI 계층에 필요한 속성에만 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30721-192">The view model contains only the properties needed for the UI layer (for example, the Create page).</span></span> <span data-ttu-id="30721-193">뷰 모델 외에도 일부 앱 Razor 페이지 코드 숨김 클래스와 브라우저 간에 데이터를 전달 바인딩 모델이 나 입력된 모델 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-193">In addition to the view model, some apps use a binding model or input model to pass data between the Razor Pages code-behind class and the browser.</span></span> <span data-ttu-id="30721-194">다음 사항을 고려 `Student` 뷰 모델:</span><span class="sxs-lookup"><span data-stu-id="30721-194">Consider the following `Student` view model:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/StudentVM.cs)]

<span data-ttu-id="30721-195">모델 보기 overposting 방지 하는 대체 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-195">View models provide an alternative way to prevent overposting.</span></span> <span data-ttu-id="30721-196">뷰 모델 (표시)을 확인 하거나 업데이트 하는 속성만 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30721-196">The view model contains only the properties to view (display) or update.</span></span>

<span data-ttu-id="30721-197">다음 코드에서는 `StudentVM` 새 학생 만들 보기 모델:</span><span class="sxs-lookup"><span data-stu-id="30721-197">The following code uses the `StudentVM` view model to create a new student:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Students/CreateVM.cshtml.cs?name=snippet_OnPostAsync)]

<span data-ttu-id="30721-198">[SetValues](https://docs.microsoft.com/ dotnet/api/microsoft.entityframeworkcore.changetracking.propertyvalues.setvalues?view=efcore-2.0#Microsoft_EntityFrameworkCore_ChangeTracking_PropertyValues_SetValues_System_Object_) 에서 다른 값을 참조 하 여이 개체의 값을 설정 하는 메서드 [Propertyvalue](https://docs.microsoft.com/ dotnet/api/microsoft.entityframeworkcore.changetracking.propertyvalues) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="30721-198">The [SetValues](https://docs.microsoft.com/ dotnet/api/microsoft.entityframeworkcore.changetracking.propertyvalues.setvalues?view=efcore-2.0#Microsoft_EntityFrameworkCore_ChangeTracking_PropertyValues_SetValues_System_Object_) method sets the values of this object by reading values from another [PropertyValues](https://docs.microsoft.com/ dotnet/api/microsoft.entityframeworkcore.changetracking.propertyvalues) object.</span></span> <span data-ttu-id="30721-199">`SetValues`속성 이름 일치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-199">`SetValues` uses property name matching.</span></span> <span data-ttu-id="30721-200">보기 모델 형식을 모델 종류와 연결 될 필요가 없습니다, 그리고 일치 하는 속성이 하기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-200">The view model type doesn't need to be related to the model type, it just needs to have properties that match.</span></span>

<span data-ttu-id="30721-201">사용 하 여 `StudentVM` 필요 [CreateVM.cshtml](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu/Pages/Students/CreateVM.cshtml) 사용 하도록 업데이트 `StudentVM` 대신 `Student`합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-201">Using `StudentVM` requires [CreateVM.cshtml](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu/Pages/Students/CreateVM.cshtml) be updated to use `StudentVM` rather than `Student`.</span></span>

<span data-ttu-id="30721-202">Razor 페이지에는 `PageModel` 파생된 클래스는 뷰 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="30721-202">In Razor Pages, the `PageModel` derived class is the view model.</span></span> 

## <a name="update-the-edit-page"></a><span data-ttu-id="30721-203">업데이트 편집 페이지</span><span class="sxs-lookup"><span data-stu-id="30721-203">Update the Edit page</span></span>

<span data-ttu-id="30721-204">편집 페이지 코드 숨김 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-204">Update the Edit page code-behind file:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Students/Edit.cshtml.cs?name=snippet_OnPostAsync&highlight=20,36)]

<span data-ttu-id="30721-205">코드 변경이 몇 가지 예외 만들기 페이지와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-205">The code changes are similar to the Create page with a few exceptions:</span></span>

* <span data-ttu-id="30721-206">`OnPostAsync`선택적 `id` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="30721-206">`OnPostAsync` has an optional `id` parameter.</span></span>
* <span data-ttu-id="30721-207">현재 학생 DB에서 인출 되는 빈 학생을 만드는 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-207">The current student is fetched from the DB, rather than creating an empty student.</span></span>
* <span data-ttu-id="30721-208">`FirstOrDefaultAsync`으로 대체 되었습니다 [FindAsync](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.dbset-1.findasync?view=efcore-2.0)합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-208">`FirstOrDefaultAsync` has been replaced with [FindAsync](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.dbset-1.findasync?view=efcore-2.0).</span></span> <span data-ttu-id="30721-209">`FindAsync`기본 키의 엔터티를 선택 하는 경우이 좋은 대안입니다.</span><span class="sxs-lookup"><span data-stu-id="30721-209">`FindAsync` is a good choice when selecting an entity from the primary key.</span></span> <span data-ttu-id="30721-210">참조 [FindAsync](#FindAsync) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-210">See [FindAsync](#FindAsync) for more information.</span></span>

### <a name="test-the-edit-and-create-pages"></a><span data-ttu-id="30721-211">편집을 테스트 하 고 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="30721-211">Test the Edit and Create pages</span></span>

<span data-ttu-id="30721-212">만들고 몇 가지 학생 엔터티를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-212">Create and edit a few student entities.</span></span>

## <a name="entity-states"></a><span data-ttu-id="30721-213">엔터티 상태</span><span class="sxs-lookup"><span data-stu-id="30721-213">Entity States</span></span>

<span data-ttu-id="30721-214">DB 컨텍스트 엔터티 메모리에는 데이터베이스에서 해당 행과 동기화 여부를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-214">The DB context keeps track of whether entities in memory are in sync with their corresponding rows in the DB.</span></span> <span data-ttu-id="30721-215">DB 컨텍스트 정보 동기화 수행할 작업을 결정 때 `SaveChanges` 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-215">The DB context sync information determines what happens when `SaveChanges` is called.</span></span> <span data-ttu-id="30721-216">예를 들어 새 엔터티를 전달 경우 메서드는 `Add` 메서드 엔터티의 상태로 설정 된 `Added`합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-216">For example, when a new entity is passed to the `Add` method, that entity's state is set to `Added`.</span></span> <span data-ttu-id="30721-217">때 `SaveChanges` 를 호출 하는 DB 상황에 맞는 SQL INSERT 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-217">When `SaveChanges` is called, the DB context issues a SQL INSERT command.</span></span>

<span data-ttu-id="30721-218">엔터티 상태는 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30721-218">An entity may be in one of the following states:</span></span>

* <span data-ttu-id="30721-219">`Added`: 엔터티 DB에 아직 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30721-219">`Added`: The entity does not yet exist in the DB.</span></span> <span data-ttu-id="30721-220">`SaveChanges` 메서드는 INSERT 문을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-220">The `SaveChanges` method issues an INSERT statement.</span></span>

* <span data-ttu-id="30721-221">`Unchanged`: 변경 내용을이 엔터티와 함께 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-221">`Unchanged`: No changes need to be saved with this entity.</span></span> <span data-ttu-id="30721-222">DB에서 읽을 때 엔터티는이 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="30721-222">An entity has this status when it is read from the DB.</span></span>

* <span data-ttu-id="30721-223">`Modified`: 일부 또는 모든 엔터티의 속성 값 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="30721-223">`Modified`: Some or all of the entity's property values have been modified.</span></span> <span data-ttu-id="30721-224">`SaveChanges` 메서드는 UPDATE 문을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-224">The `SaveChanges` method issues an UPDATE statement.</span></span>

* <span data-ttu-id="30721-225">`Deleted`: 엔터티를 삭제 하도록 표시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="30721-225">`Deleted`: The entity has been marked for deletion.</span></span> <span data-ttu-id="30721-226">`SaveChanges` 메서드 DELETE 문을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-226">The `SaveChanges` method issues a DELETE statement.</span></span>

* <span data-ttu-id="30721-227">`Detached`: 엔터티 DB 컨텍스트에서 추적 되 고 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30721-227">`Detached`: The entity isn't being tracked by the DB context.</span></span>

<span data-ttu-id="30721-228">데스크톱 앱에서는 상태 변경 내용이 일반적으로 자동으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30721-228">In a desktop app, state changes are typically set automatically.</span></span> <span data-ttu-id="30721-229">엔터티는 읽기, 변경 및 엔터티 상태를 자동으로 변경 해야 `Modified`합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-229">An entity is read, changes are made, and the entity state to automatically be changed to `Modified`.</span></span> <span data-ttu-id="30721-230">호출 `SaveChanges` 변경된 된 속성을 업데이트 하는 SQL UPDATE 문을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-230">Calling `SaveChanges` generates a SQL UPDATE statement that updates only the changed properties.</span></span>

<span data-ttu-id="30721-231">웹 앱의 경우에 `DbContext` 읽는 엔터티 및 데이터 페이지를 렌더링 된 후 삭제 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-231">In a web app, the `DbContext` that reads an entity and displays the data is disposed after a page is rendered.</span></span> <span data-ttu-id="30721-232">페이지 때 `OnPostAsync` 메서드가 호출 되 면 새 웹 요청이 만들어지면의 새 인스턴스는 `DbContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-232">When a pages `OnPostAsync` method is called, a new web request is made and with a new instance of the `DbContext`.</span></span> <span data-ttu-id="30721-233">다시 새 해당 컨텍스트 내에서 엔터티를 읽어 시뮬레이션 데스크톱 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-233">Re-reading the entity in that new context simulates desktop processing.</span></span>

## <a name="update-the-delete-page"></a><span data-ttu-id="30721-234">업데이트 페이지 삭제</span><span class="sxs-lookup"><span data-stu-id="30721-234">Update the Delete page</span></span>

<span data-ttu-id="30721-235">사용자 지정 오류 구현에 코드가 추가이 섹션에서는 메시지에 대 한 호출 `SaveChanges` 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-235">In this section, code is added to implement a custom error message when the call to `SaveChanges` fails.</span></span> <span data-ttu-id="30721-236">Possile 오류 메시지를 포함 하는 문자열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-236">Add a string to contain possile error messages:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Students/Delete.cshtml.cs?name=snippet1&highlight=12)]

<span data-ttu-id="30721-237">`OnGetAsync` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="30721-237">Replace the `OnGetAsync` method with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Students/Delete.cshtml.cs?name=snippet_OnGetAsync&highlight=1,9,17-20)]

<span data-ttu-id="30721-238">선택적 매개 변수를 포함 하는 위의 코드 `saveChangesError`합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-238">The preceding code contains the optional parameter `saveChangesError`.</span></span> <span data-ttu-id="30721-239">`saveChangesError`학생 개체를 삭제 하려면 실패 한 후 메서드가 호출 된 있는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="30721-239">`saveChangesError` indicates whether the method was called after a failure to delete the student object.</span></span> <span data-ttu-id="30721-240">일시적인 네트워크 문제 때문에 삭제 작업이 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30721-240">The delete operation might fail because of transient network problems.</span></span> <span data-ttu-id="30721-241">클라우드에서 일시적인 네트워크 오류 발생 가능성이 더 큽니다.</span><span class="sxs-lookup"><span data-stu-id="30721-241">Transient network errors are more likely in the cloud.</span></span> <span data-ttu-id="30721-242">`saveChangesError`가 false 때 페이지 삭제 `OnGetAsync` UI에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30721-242">`saveChangesError`is false when the Delete page `OnGetAsync` is called from the UI.</span></span> <span data-ttu-id="30721-243">때 `OnGetAsync` 호출한 `OnPostAsync` (못했기 때문에 삭제 작업), `saveChangesError` 매개 변수가 true.</span><span class="sxs-lookup"><span data-stu-id="30721-243">When `OnGetAsync` is called by `OnPostAsync` (because the delete operation failed), the `saveChangesError` parameter is true.</span></span>

### <a name="the-delete-pages-onpostasync-method"></a><span data-ttu-id="30721-244">Delete 페이지 OnPostAsync 메서드</span><span class="sxs-lookup"><span data-stu-id="30721-244">The Delete pages OnPostAsync method</span></span>

<span data-ttu-id="30721-245">대체는 `OnPostAsync` 다음 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-245">Replace the `OnPostAsync` with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Students/Delete.cshtml.cs?name=snippet_OnPostAsync)]

<span data-ttu-id="30721-246">선택한 엔터티를 검색 하는 앞의 코드 호출는 `Remove` 엔터티의 상태 설정 하는 방법은 `Deleted`합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-246">The preceding code retrieves the selected entity, then calls the `Remove` method to set the entity's status to `Deleted`.</span></span> <span data-ttu-id="30721-247">때 `SaveChanges` 호출, SQL DELETE 명령이 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-247">When `SaveChanges` is called, a SQL DELETE command is generated.</span></span> <span data-ttu-id="30721-248">경우 `Remove` 실패:</span><span class="sxs-lookup"><span data-stu-id="30721-248">If `Remove` fails:</span></span>

* <span data-ttu-id="30721-249">DB 예외가 검색 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="30721-249">The DB exception is caught.</span></span>
* <span data-ttu-id="30721-250">Delete 페이지 `OnGetAsync` 메서드는 `saveChangesError=true`합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-250">The Delete pages `OnGetAsync` method is called with `saveChangesError=true`.</span></span>

### <a name="update-the-delete-razor-page"></a><span data-ttu-id="30721-251">삭제 Razor 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-251">Update the Delete Razor Page</span></span>

<span data-ttu-id="30721-252">Razor 페이지 삭제를 강조 표시 된 오류 메시지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-252">Add the following highlighted error message to the Delete Razor Page.</span></span>

[!code-cshtml[Main](intro/samples/cu/Pages/Students/Delete.cshtml?range=1-13&highlight=10)]

<span data-ttu-id="30721-253">Delete를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-253">Test Delete.</span></span>

## <a name="common-errors"></a><span data-ttu-id="30721-254">일반적인 오류</span><span class="sxs-lookup"><span data-stu-id="30721-254">Common errors</span></span>

<span data-ttu-id="30721-255">학생/Home 또는 다른 링크는 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30721-255">Student/Home or other links don't work:</span></span>

<span data-ttu-id="30721-256">Razor 페이지에 올바른 확인 `@page` 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="30721-256">Verify the Razor Page contains the correct `@page` directive.</span></span> <span data-ttu-id="30721-257">학생/홈 Razor 페이지가 해야 하는 예를 들어 **하지** 경로 템플릿을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="30721-257">For example, The Student/Home Razor Page should **not** contain a route template:</span></span>

```cshtml
@page "{id:int}"
```

<span data-ttu-id="30721-258">각 Razor 페이지를 포함 해야는 `@page` 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="30721-258">Each Razor Page must include the `@page` directive.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="30721-259">[이전](xref:data/ef-rp/intro)
[다음](xref:data/ef-rp/sort-filter-page)</span><span class="sxs-lookup"><span data-stu-id="30721-259">[Previous](xref:data/ef-rp/intro)
[Next](xref:data/ef-rp/sort-filter-page)</span></span>