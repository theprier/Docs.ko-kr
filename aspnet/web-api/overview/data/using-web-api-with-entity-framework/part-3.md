---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-3
title: Code First 마이그레이션을 사용 하 여 데이터베이스를 시드하려면 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 06/16/2014
ms.assetid: 76e2013a-65b7-488c-834d-9448ecea378e
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-3
msc.type: authoredcontent
ms.openlocfilehash: bce662110fa63a9aee8e23e7b9fcc9ba9a8d2857
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37805459"
---
<a name="use-code-first-migrations-to-seed-the-database"></a><span data-ttu-id="4a311-102">Code First 마이그레이션을 사용 하 여 데이터베이스를 시드합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-102">Use Code First Migrations to Seed the Database</span></span>
====================
<span data-ttu-id="4a311-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="4a311-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="4a311-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="4a311-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="4a311-105">이 섹션에서는 사용할지 [Code First 마이그레이션을](https://msdn.microsoft.com/data/jj591621) 테스트 데이터로 데이터베이스를 시드하려면 EF의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-105">In this section, you will use [Code First Migrations](https://msdn.microsoft.com/data/jj591621) in EF to seed the database with test data.</span></span>

<span data-ttu-id="4a311-106">**도구** 메뉴에서 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-106">From the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="4a311-107">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-107">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-3/samples/sample1.cmd)]

<span data-ttu-id="4a311-108">이 명령은 프로젝트에 마이그레이션을 이라는 폴더와 마이그레이션 폴더에 Configuration.cs 라는 코드 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-108">This command adds a folder named Migrations to your project, plus a code file named Configuration.cs in the Migrations folder.</span></span>

![](part-3/_static/image1.png)

<span data-ttu-id="4a311-109">Configuration.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-109">Open the Configuration.cs file.</span></span> <span data-ttu-id="4a311-110">다음을 추가 합니다 **를 사용 하 여** 문입니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-110">Add the following **using** statement.</span></span>

[!code-csharp[Main](part-3/samples/sample2.cs)]

<span data-ttu-id="4a311-111">다음 코드를 추가 합니다 **Configuration.Seed** 메서드:</span><span class="sxs-lookup"><span data-stu-id="4a311-111">Then add the following code to the **Configuration.Seed** method:</span></span>

[!code-csharp[Main](part-3/samples/sample3.cs)]

<span data-ttu-id="4a311-112">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-112">In the Package Manager Console window, type the following commands:</span></span>

[!code-console[Main](part-3/samples/sample4.cmd)]

<span data-ttu-id="4a311-113">첫 번째 명령은 데이터베이스를 만드는 코드를 생성 하 고 두 번째 명령은 해당 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-113">The first command generates code that creates the database, and the second command executes that code.</span></span> <span data-ttu-id="4a311-114">데이터베이스를 로컬로 사용 하 여 만들어집니다 [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-114">The database is created locally, using [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx).</span></span>

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a><span data-ttu-id="4a311-115">(선택 사항) API를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-115">Explore the API (Optional)</span></span>

<span data-ttu-id="4a311-116">F5 키를 눌러 디버그 모드에서 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-116">Press F5 to run the application in debug mode.</span></span> <span data-ttu-id="4a311-117">Visual Studio IIS Express를 시작 하 고 웹 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-117">Visual Studio starts IIS Express and runs your web app.</span></span> <span data-ttu-id="4a311-118">그런 다음 visual Studio가 브라우저를 시작 하 고 앱의 홈 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-118">Visual Studio then launches a browser and opens the app's home page.</span></span>

<span data-ttu-id="4a311-119">Visual Studio 웹 프로젝트를 실행할 때 포트 번호를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-119">When Visual Studio runs a web project, it assigns a port number.</span></span> <span data-ttu-id="4a311-120">아래 이미지에서 포트 번호가 50524입니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-120">In the image below, the port number is 50524.</span></span> <span data-ttu-id="4a311-121">응용 프로그램을 실행 하는 경우 다른 포트 번호를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-121">When you run the application, you'll see a different port number.</span></span>

![](part-3/_static/image3.png)

<span data-ttu-id="4a311-122">홈 페이지는 ASP.NET MVC를 사용 하 여 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-122">The home page is implemented using ASP.NET MVC.</span></span> <span data-ttu-id="4a311-123">페이지의 맨 위에 있는 "API" 이라는 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-123">At the top of the page, there is a link that says "API".</span></span> <span data-ttu-id="4a311-124">이 링크는 web API에 대 한 자동 생성 된 도움말 페이지에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-124">This link brings you to an auto-generated help page for the web API.</span></span> <span data-ttu-id="4a311-125">(이 도움말 페이지 생성 방법 및 고유한 설명서 페이지에 추가할 수 있습니다 하는 방법에 대해 알아보려면 [ASP.NET Web API에 대 한 도움말 페이지 만들기](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) 페이지 링크를 요청 및 응답 형식을 비롯 한 API에 대 한 자세한 내용은 도움말을 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-125">(To learn how this help page is generated, and how you can add your own documentation to the page, see [Creating Help Pages for ASP.NET Web API](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) You can click on the help page links to see details about the API, including the request and response format.</span></span>

![](part-3/_static/image4.png)

<span data-ttu-id="4a311-126">API를 통해 데이터베이스에 대 한 CRUD 작업을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-126">The API enables CRUD operations on the database.</span></span> <span data-ttu-id="4a311-127">다음 API를 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-127">The following summarizes the API.</span></span>

| <span data-ttu-id="4a311-128">만든 이</span><span class="sxs-lookup"><span data-stu-id="4a311-128">Authors</span></span> |  |
| --- | -- |
| <span data-ttu-id="4a311-129">Api/작성자 가져오기</span><span class="sxs-lookup"><span data-stu-id="4a311-129">GET api/authors</span></span> | <span data-ttu-id="4a311-130">모든 작성자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-130">Get all authors.</span></span> |
| <span data-ttu-id="4a311-131">GET api/작성자 / {id}</span><span class="sxs-lookup"><span data-stu-id="4a311-131">GET api/authors/{id}</span></span> | <span data-ttu-id="4a311-132">작성자 id 가져오기</span><span class="sxs-lookup"><span data-stu-id="4a311-132">Get an author by ID.</span></span> |
| <span data-ttu-id="4a311-133">POST/api/작성자</span><span class="sxs-lookup"><span data-stu-id="4a311-133">POST /api/authors</span></span> | <span data-ttu-id="4a311-134">새 작성자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-134">Create a new author.</span></span> |
| <span data-ttu-id="4a311-135">PUT/a p i/작성자 / {id}</span><span class="sxs-lookup"><span data-stu-id="4a311-135">PUT /api/authors/{id}</span></span> | <span data-ttu-id="4a311-136">기존 author를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-136">Update an existing author.</span></span> |
| <span data-ttu-id="4a311-137">삭제/a p i/작성자 / {id}</span><span class="sxs-lookup"><span data-stu-id="4a311-137">DELETE /api/authors/{id}</span></span> | <span data-ttu-id="4a311-138">작성자를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-138">Delete an author.</span></span> |

| <span data-ttu-id="4a311-139">책</span><span class="sxs-lookup"><span data-stu-id="4a311-139">Books</span></span> |  |
| --- | -- |
| <span data-ttu-id="4a311-140">/Api/books 가져오기</span><span class="sxs-lookup"><span data-stu-id="4a311-140">GET /api/books</span></span> | <span data-ttu-id="4a311-141">모든 책을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-141">Get all books.</span></span> |
| <span data-ttu-id="4a311-142">가져오기/a p i/책 / {id}</span><span class="sxs-lookup"><span data-stu-id="4a311-142">GET /api/books/{id}</span></span> | <span data-ttu-id="4a311-143">책 id 가져오기</span><span class="sxs-lookup"><span data-stu-id="4a311-143">Get a book by ID.</span></span> |
| <span data-ttu-id="4a311-144">Api 설명서를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-144">POST /api/books</span></span> | <span data-ttu-id="4a311-145">새 책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-145">Create a new book.</span></span> |
| <span data-ttu-id="4a311-146">PUT/a p i/책 / {id}</span><span class="sxs-lookup"><span data-stu-id="4a311-146">PUT /api/books/{id}</span></span> | <span data-ttu-id="4a311-147">기존 책을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-147">Update an existing book.</span></span> |
| <span data-ttu-id="4a311-148">삭제/a p i/책 / {id}</span><span class="sxs-lookup"><span data-stu-id="4a311-148">DELETE /api/books/{id}</span></span> | <span data-ttu-id="4a311-149">책을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-149">Delete a book.</span></span> |

## <a name="view-the-database-optional"></a><span data-ttu-id="4a311-150">(선택 사항) 데이터베이스 보기</span><span class="sxs-lookup"><span data-stu-id="4a311-150">View the Database (Optional)</span></span>

<span data-ttu-id="4a311-151">Update-database 명령을 실행할 때 EF에서 데이터베이스를 만든 호출을 `Seed` 메서드.</span><span class="sxs-lookup"><span data-stu-id="4a311-151">When you ran the Update-Database command, EF created the database and called the `Seed` method.</span></span> <span data-ttu-id="4a311-152">EF가 사용 하는 응용 프로그램을 로컬로 실행 하면 [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-152">When you run the application locally, EF uses [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx).</span></span> <span data-ttu-id="4a311-153">Visual Studio에서 데이터베이스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-153">You can view the database in Visual Studio.</span></span> <span data-ttu-id="4a311-154">**뷰** 메뉴에서 **SQL Server 개체 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-154">From the **View** menu, select **SQL Server Object Explorer**.</span></span>

![](part-3/_static/image5.png)

<span data-ttu-id="4a311-155">에 **서버에 연결** 대화의 합니다 **서버 이름** 편집 상자에 "(localdb) \v11.0"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-155">In the **Connect to Server** dialog, in the **Server Name** edit box, type "(localdb)\v11.0".</span></span> <span data-ttu-id="4a311-156">유지 된 **인증** 옵션 "Windows 인증"으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-156">Leave the **Authentication** option as "Windows Authentication".</span></span> <span data-ttu-id="4a311-157">**연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-157">Click **Connect**.</span></span>

![](part-3/_static/image6.png)

<span data-ttu-id="4a311-158">Visual Studio는 LocalDB에 연결 하 고 SQL Server 개체 탐색기 창에서 기존 데이터베이스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-158">Visual Studio connects to LocalDB and shows your existing databases in the SQL Server Object Explorer window.</span></span> <span data-ttu-id="4a311-159">EF에서 만든 테이블을 보려면 노드를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-159">You can expand the nodes to see the tables that EF created.</span></span>

![](part-3/_static/image7.png)

<span data-ttu-id="4a311-160">데이터를 보려면 테이블을 마우스 오른쪽 단추로 클릭 하 고 선택 **데이터 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-160">To view the data, right-click a table and select **View Data**.</span></span>

![](part-3/_static/image8.png)

<span data-ttu-id="4a311-161">다음 스크린 샷에서 책 테이블에 대 한 결과 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4a311-161">The following screenshot shows the results for the Books table.</span></span> <span data-ttu-id="4a311-162">EF 시드 데이터를 사용 하 여 데이터베이스를 채울 Authors 테이블에 외래 키를 포함 하는 테이블에 유의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4a311-162">Notice that EF populated the database with the seed data, and the table contains the foreign key to the Authors table.</span></span>

![](part-3/_static/image9.png)

> [!div class="step-by-step"]
> <span data-ttu-id="4a311-163">[이전](part-2.md)
> [다음](part-4.md)</span><span class="sxs-lookup"><span data-stu-id="4a311-163">[Previous](part-2.md)
[Next](part-4.md)</span></span>
