---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-3
title: "Code First 마이그레이션을 사용 하 여 데이터베이스의 초기값 | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 76e2013a-65b7-488c-834d-9448ecea378e
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-3
msc.type: authoredcontent
ms.openlocfilehash: df75a69644033cc76fee86b5a9692ab65beb4d01
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="use-code-first-migrations-to-seed-the-database"></a><span data-ttu-id="4e292-102">Code First 마이그레이션을 사용 하 여 데이터베이스의 초기값</span><span class="sxs-lookup"><span data-stu-id="4e292-102">Use Code First Migrations to Seed the Database</span></span>
====================
<span data-ttu-id="4e292-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="4e292-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="4e292-104">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="4e292-105">이 섹션을 사용 하 여 [Code First 마이그레이션을](https://msdn.microsoft.com/en-us/data/jj591621) 를 테스트 데이터로 데이터베이스를 시드하는 EF에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-105">In this section, you will use [Code First Migrations](https://msdn.microsoft.com/en-us/data/jj591621) in EF to seed the database with test data.</span></span>

<span data-ttu-id="4e292-106">**도구** 메뉴 선택 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-106">From the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="4e292-107">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-107">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-3/samples/sample1.cmd)]

<span data-ttu-id="4e292-108">이 명령은 마이그레이션 프로젝트에 라는 폴더를 더한 Migrations 폴더에서 Configuration.cs 라는 코드 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-108">This command adds a folder named Migrations to your project, plus a code file named Configuration.cs in the Migrations folder.</span></span>

![](part-3/_static/image1.png)

<span data-ttu-id="4e292-109">Configuration.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-109">Open the Configuration.cs file.</span></span> <span data-ttu-id="4e292-110">다음 추가 **를 사용 하 여** 문.</span><span class="sxs-lookup"><span data-stu-id="4e292-110">Add the following **using** statement.</span></span>

[!code-csharp[Main](part-3/samples/sample2.cs)]

<span data-ttu-id="4e292-111">다음 코드를 다음 추가 **Configuration.Seed** 메서드:</span><span class="sxs-lookup"><span data-stu-id="4e292-111">Then add the following code to the **Configuration.Seed** method:</span></span>

[!code-csharp[Main](part-3/samples/sample3.cs)]

<span data-ttu-id="4e292-112">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-112">In the Package Manager Console window, type the following commands:</span></span>

[!code-console[Main](part-3/samples/sample4.cmd)]

<span data-ttu-id="4e292-113">첫 번째 명령은 데이터베이스가 생성 하는 코드를 생성 하 고 두 번째 명령은 해당 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-113">The first command generates code that creates the database, and the second command executes that code.</span></span> <span data-ttu-id="4e292-114">데이터베이스를 로컬로 사용 하 여 만들어집니다 [LocalDB](https://msdn.microsoft.com/en-us/library/hh510202.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-114">The database is created locally, using [LocalDB](https://msdn.microsoft.com/en-us/library/hh510202.aspx).</span></span>

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a><span data-ttu-id="4e292-115">(선택 사항) API를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-115">Explore the API (Optional)</span></span>

<span data-ttu-id="4e292-116">F5 키를 눌러 디버그 모드에서 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-116">Press F5 to run the application in debug mode.</span></span> <span data-ttu-id="4e292-117">Visual Studio는 IIS Express를 시작 하 고 웹 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-117">Visual Studio starts IIS Express and runs your web app.</span></span> <span data-ttu-id="4e292-118">그런 다음 visual Studio는 브라우저를 시작 하 고 응용 프로그램의 홈 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-118">Visual Studio then launches a browser and opens the app's home page.</span></span>

<span data-ttu-id="4e292-119">Visual Studio 웹 프로젝트를 실행 하는 경우 포트 번호를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-119">When Visual Studio runs a web project, it assigns a port number.</span></span> <span data-ttu-id="4e292-120">아래 이미지에 포트 번호가 50524입니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-120">In the image below, the port number is 50524.</span></span> <span data-ttu-id="4e292-121">응용 프로그램을 실행 하는 경우에 다른 포트 번호를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-121">When you run the application, you'll see a different port number.</span></span>

![](part-3/_static/image3.png)

<span data-ttu-id="4e292-122">홈 페이지는 ASP.NET MVC를 사용 하 여 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-122">The home page is implemented using ASP.NET MVC.</span></span> <span data-ttu-id="4e292-123">페이지 맨 위에 있는 링크는 "API" 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-123">At the top of the page, there is a link that says "API".</span></span> <span data-ttu-id="4e292-124">이 링크는 web API에 대 한 자동 생성 된 도움말 페이지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-124">This link brings you to an auto-generated help page for the web API.</span></span> <span data-ttu-id="4e292-125">(이 도움말 페이지 생성 되는 방식 및 추가 하는 방법을 직접 설명서 페이지를 참조 [ASP.NET Web API에 대 한 도움말 페이지 만들기](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) 요청 및 응답 형식을 비롯 한 API에 대 한 자세한 내용을 보려면 페이지 링크 제공 도움말 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-125">(To learn how this help page is generated, and how you can add your own documentation to the page, see [Creating Help Pages for ASP.NET Web API](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) You can click on the help page links to see details about the API, including the request and response format.</span></span>

![](part-3/_static/image4.png)

<span data-ttu-id="4e292-126">API를 통해 데이터베이스에 대해 CRUD 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-126">The API enables CRUD operations on the database.</span></span> <span data-ttu-id="4e292-127">다음은 API에 대 한 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-127">The following summarizes the API.</span></span>

| <span data-ttu-id="4e292-128">만든 이</span><span class="sxs-lookup"><span data-stu-id="4e292-128">Authors</span></span> |  |
| --- | -- |
| <span data-ttu-id="4e292-129">Api/작성자 가져오기</span><span class="sxs-lookup"><span data-stu-id="4e292-129">GET api/authors</span></span> | <span data-ttu-id="4e292-130">모든 작성자를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-130">Get all authors.</span></span> |
| <span data-ttu-id="4e292-131">GET api/작성자 / {id}</span><span class="sxs-lookup"><span data-stu-id="4e292-131">GET api/authors/{id}</span></span> | <span data-ttu-id="4e292-132">만든 id 가져오기</span><span class="sxs-lookup"><span data-stu-id="4e292-132">Get an author by ID.</span></span> |
| <span data-ttu-id="4e292-133">POST/api/작성자</span><span class="sxs-lookup"><span data-stu-id="4e292-133">POST /api/authors</span></span> | <span data-ttu-id="4e292-134">새로운 저자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-134">Create a new author.</span></span> |
| <span data-ttu-id="4e292-135">PUT /api/작성자 / {id}</span><span class="sxs-lookup"><span data-stu-id="4e292-135">PUT /api/authors/{id}</span></span> | <span data-ttu-id="4e292-136">기존 author를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-136">Update an existing author.</span></span> |
| <span data-ttu-id="4e292-137">삭제 /api/작성자 / {id}</span><span class="sxs-lookup"><span data-stu-id="4e292-137">DELETE /api/authors/{id}</span></span> | <span data-ttu-id="4e292-138">제작자를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-138">Delete an author.</span></span> |

| <span data-ttu-id="4e292-139">설명서</span><span class="sxs-lookup"><span data-stu-id="4e292-139">Books</span></span> |  |
| --- | -- |
| <span data-ttu-id="4e292-140">/Api/books 가져오기</span><span class="sxs-lookup"><span data-stu-id="4e292-140">GET /api/books</span></span> | <span data-ttu-id="4e292-141">모든 책을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-141">Get all books.</span></span> |
| <span data-ttu-id="4e292-142">가져오기 /api/설명서 / {id}</span><span class="sxs-lookup"><span data-stu-id="4e292-142">GET /api/books/{id}</span></span> | <span data-ttu-id="4e292-143">책 id 가져오기</span><span class="sxs-lookup"><span data-stu-id="4e292-143">Get a book by ID.</span></span> |
| <span data-ttu-id="4e292-144">게시/api/설명서</span><span class="sxs-lookup"><span data-stu-id="4e292-144">POST /api/books</span></span> | <span data-ttu-id="4e292-145">새 책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-145">Create a new book.</span></span> |
| <span data-ttu-id="4e292-146">PUT /api/설명서 / {id}</span><span class="sxs-lookup"><span data-stu-id="4e292-146">PUT /api/books/{id}</span></span> | <span data-ttu-id="4e292-147">기존 책을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-147">Update an existing book.</span></span> |
| <span data-ttu-id="4e292-148">삭제 /api/설명서 / {id}</span><span class="sxs-lookup"><span data-stu-id="4e292-148">DELETE /api/books/{id}</span></span> | <span data-ttu-id="4e292-149">책을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-149">Delete a book.</span></span> |

## <a name="view-the-database-optional"></a><span data-ttu-id="4e292-150">(선택 사항) 데이터베이스 보기</span><span class="sxs-lookup"><span data-stu-id="4e292-150">View the Database (Optional)</span></span>

<span data-ttu-id="4e292-151">Update-database 명령을 실행할 때 EF에서 데이터베이스를 만든 호출의 `Seed` 메서드.</span><span class="sxs-lookup"><span data-stu-id="4e292-151">When you ran the Update-Database command, EF created the database and called the `Seed` method.</span></span> <span data-ttu-id="4e292-152">EF 사용 하 여 응용 프로그램을 로컬로 실행할 때 [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-152">When you run the application locally, EF uses [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx).</span></span> <span data-ttu-id="4e292-153">Visual Studio에서 데이터베이스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-153">You can view the database in Visual Studio.</span></span> <span data-ttu-id="4e292-154">**보기** 메뉴 선택 **SQL Server 개체 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-154">From the **View** menu, select **SQL Server Object Explorer**.</span></span>

![](part-3/_static/image5.png)

<span data-ttu-id="4e292-155">에 **서버에 연결** 대화에는 **서버 이름** 편집 상자, "(localdb) \v11.0"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-155">In the **Connect to Server** dialog, in the **Server Name** edit box, type "(localdb)\v11.0".</span></span> <span data-ttu-id="4e292-156">둡니다는 **인증** "Windows 인증"으로 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-156">Leave the **Authentication** option as "Windows Authentication".</span></span> <span data-ttu-id="4e292-157">**연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-157">Click **Connect**.</span></span>

![](part-3/_static/image6.png)

<span data-ttu-id="4e292-158">Visual Studio는 LocalDB에 연결 하 고 SQL Server 개체 탐색기 창에서 기존 데이터베이스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-158">Visual Studio connects to LocalDB and shows your existing databases in the SQL Server Object Explorer window.</span></span> <span data-ttu-id="4e292-159">EF 만든 테이블을 보려면 노드를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-159">You can expand the nodes to see the tables that EF created.</span></span>

![](part-3/_static/image7.png)

<span data-ttu-id="4e292-160">데이터를 보려면 테이블을 마우스 오른쪽 단추로 클릭 하 고 선택 **데이터 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-160">To view the data, right-click a table and select **View Data**.</span></span>

![](part-3/_static/image8.png)

<span data-ttu-id="4e292-161">다음 스크린 샷에서 설명서 테이블에 대 한 결과 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4e292-161">The following screenshot shows the results for the Books table.</span></span> <span data-ttu-id="4e292-162">EF는 데이터베이스 시드 데이터로 채워진 Authors 테이블에 외래 키를 포함 하는 테이블에 유의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4e292-162">Notice that EF populated the database with the seed data, and the table contains the foreign key to the Authors table.</span></span>

![](part-3/_static/image9.png)

>[!div class="step-by-step"]
<span data-ttu-id="4e292-163">[이전](part-2.md)
[다음](part-4.md)</span><span class="sxs-lookup"><span data-stu-id="4e292-163">[Previous](part-2.md)
[Next](part-4.md)</span></span>
