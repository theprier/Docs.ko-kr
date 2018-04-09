---
uid: mvc/overview/getting-started/introduction/creating-a-connection-string
title: 연결 문자열 만들기 및 SQL Server LocalDB 사용 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: 6127804d-c1a9-414d-8429-7f3dd0f56e97
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/introduction/creating-a-connection-string
msc.type: authoredcontent
ms.openlocfilehash: edbd46ef8a03670f0cb7527142babe9bd5846c7a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="d1b33-102">연결 문자열 만들기 및 SQL Server LocalDB 사용</span><span class="sxs-lookup"><span data-stu-id="d1b33-102">Creating a Connection String and Working with SQL Server LocalDB</span></span>
====================
<span data-ttu-id="d1b33-103">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="d1b33-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="d1b33-104">연결 문자열 만들기 및 SQL Server LocalDB 사용</span><span class="sxs-lookup"><span data-stu-id="d1b33-104">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="d1b33-105">`MovieDBContext` 만든 클래스 매핑 및 데이터베이스에 연결 하는 작업을 처리 `Movie` 데이터베이스 레코드에는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-105">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="d1b33-106">그러나 인지 궁금할 질문 중 하나는에 연결 하는 데이터베이스를 지정 하는 방법을입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-106">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="d1b33-107">사용할 데이터베이스를 지정할 필요는 없습니다, Entity Framework는 기본적으로 기본 [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-107">You don't actually have to specify which database to use, Entity Framework will default to using [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span></span> <span data-ttu-id="d1b33-108">이 섹션에서 명시적으로 추가 하겠습니다에서 연결 문자열은 *Web.config* 응용 프로그램의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-108">In this section we'll explicitly add a connection string in the *Web.config* file of the application.</span></span>

## <a name="sql-server-express-localdb"></a><span data-ttu-id="d1b33-109">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="d1b33-109">SQL Server Express LocalDB</span></span>

<span data-ttu-id="d1b33-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) 는 SQL Server Express 데이터베이스 엔진의 요청에 따라 시작 하 고 사용자 모드에서 실행 하는 경량 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) is a lightweight version of the SQL Server Express Database Engine that starts on demand and runs in user mode.</span></span> <span data-ttu-id="d1b33-111">LocalDB 데이터베이스도 작업할 수 있도록 SQL Server Express의 특수 실행 모드에서 실행 *.mdf* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-111">LocalDB runs in a special execution mode of SQL Server Express that enables you to work with databases as *.mdf* files.</span></span> <span data-ttu-id="d1b33-112">LocalDB 데이터베이스 파일에 보관 되는 일반적으로 *앱\_데이터* 웹 프로젝트의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-112">Typically, LocalDB database files are kept in the *App\_Data* folder of a web project.</span></span>

<span data-ttu-id="d1b33-113">SQL Server Express 프로덕션 웹 응용 프로그램에서 사용 하기 위해 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-113">SQL Server Express is not recommended for use in production web applications.</span></span> <span data-ttu-id="d1b33-114">LocalDB 특히 쓰일 수 없습니다 프로덕션 웹 응용 프로그램에 대 한 하므로 IIS와 함께 작동 하도록 설계 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-114">LocalDB in particular should not be used for production with a web application because it is not designed to work with IIS.</span></span> <span data-ttu-id="d1b33-115">그러나 SQL Server 또는 SQL Azure에 LocalDB 데이터베이스를 쉽게 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-115">However, a LocalDB database can be easily migrated to SQL Server or SQL Azure.</span></span>

<span data-ttu-id="d1b33-116">Visual Studio 2017 LocalDB Visual Studio와 함께 기본적으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-116">In Visual Studio 2017, LocalDB is installed by default with Visual Studio.</span></span>

<span data-ttu-id="d1b33-117">기본적으로 개체 컨텍스트 클래스와 같은 이름으로 지정 하는 연결 문자열에 대 한 Entity Framework 찾습니다 (`MovieDBContext` 이 프로젝트에 대 한).</span><span class="sxs-lookup"><span data-stu-id="d1b33-117">By default, the Entity Framework looks for a connection string named the same as the object context class (`MovieDBContext` for this project).</span></span> <span data-ttu-id="d1b33-118">자세한 내용은 참조 [ASP.NET 웹 응용 프로그램에 대 한 SQL Server 연결 문자열](https://msdn.microsoft.com/library/jj653752.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-118">For more information see [SQL Server Connection Strings for ASP.NET Web Applications](https://msdn.microsoft.com/library/jj653752.aspx).</span></span>

<span data-ttu-id="d1b33-119">응용 프로그램 루트를 열고 *Web.config* 파일 아래에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-119">Open the application root *Web.config* file shown below.</span></span> <span data-ttu-id="d1b33-120">(하지는 *Web.config* 파일에 *뷰* 폴더입니다.)</span><span class="sxs-lookup"><span data-stu-id="d1b33-120">(Not the *Web.config* file in the *Views* folder.)</span></span>

![](creating-a-connection-string/_static/image1.png)

<span data-ttu-id="d1b33-121">찾기의 `<connectionStrings>` 요소:</span><span class="sxs-lookup"><span data-stu-id="d1b33-121">Find the `<connectionStrings>` element:</span></span>

![](creating-a-connection-string/_static/image2.png)

<span data-ttu-id="d1b33-122">다음 연결 문자열을 추가할는 `<connectionStrings>` 요소에는 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-122">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

<span data-ttu-id="d1b33-123">다음 예제에서는의 일부는 *Web.config* 파일을 추가 하는 새 연결 문자열:</span><span class="sxs-lookup"><span data-stu-id="d1b33-123">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

<span data-ttu-id="d1b33-124">두 개의 연결 문자열은 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-124">The two connection strings are very similar.</span></span> <span data-ttu-id="d1b33-125">첫 번째 연결 문자열 이름이 `DefaultConnection` 응용 프로그램에 액세스할 수 있는 컨트롤을 멤버 자격 데이터베이스에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-125">The first connection string is named `DefaultConnection` and is used for the membership database to control who can access the application.</span></span> <span data-ttu-id="d1b33-126">명명 된 LocalDB 데이터베이스를 지정 하는 사용자가 추가한 연결 문자열 *Movie.mdf* 에 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-126">The connection string you've added specifies a LocalDB database named *Movie.mdf* located in the *App\_Data* folder.</span></span> <span data-ttu-id="d1b33-127">내 자습서를 참조 하십시오 멤버 자격, 인증 및 보안에 대 한 자세한 내용은이 자습서의 멤버 자격 데이터베이스를 사용 하지 않습니다 म [인증 및 SQL DB ASP.NET MVC 응용 프로그램 만들기 및 Azure 앱 서비스 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-127">We won't use the membership database in this tutorial, for more information on membership, authentication and security, see my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span>

<span data-ttu-id="d1b33-128">연결 문자열의 이름의 이름과 일치 해야 합니다는 [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-128">The name of the connection string must match the name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class.</span></span>

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

<span data-ttu-id="d1b33-129">추가 하지 않아도 실제로 `MovieDBContext` 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-129">You don't actually need to add the `MovieDBContext` connection string.</span></span> <span data-ttu-id="d1b33-130">Entity Framework의 정규화 된 이름 사용 하 여 사용자가 디렉터리에 LocalDB 데이터베이스를 만드는 연결 문자열을 지정 하지 않으면는 [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) 클래스 (이 경우 `MvcMovie.Models.MovieDBContext`).</span><span class="sxs-lookup"><span data-stu-id="d1b33-130">If you don't specify a connection string, Entity Framework will create a LocalDB database in the users directory with the fully qualified name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class (in this case `MvcMovie.Models.MovieDBContext`).</span></span> <span data-ttu-id="d1b33-131">이름은 데이터베이스 원하는가지고 *합니다. MDF* 접미사입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-131">You can name the database anything you like, as long as it has the *.MDF* suffix.</span></span> <span data-ttu-id="d1b33-132">예를 들어, 데이터베이스 이름이 우리 *MyFilms.mdf*합니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-132">For example, we could name the database *MyFilms.mdf*.</span></span>

<span data-ttu-id="d1b33-133">다음으로 빌드합니다.이 새 `MoviesController` 동영상 데이터를 표시 하 고 사용자가 새 동영상 목록을 만들 수 있도록 허용 하는 데 사용할 수 있는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d1b33-133">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d1b33-134">[이전](adding-a-model.md)
> [다음](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="d1b33-134">[Previous](adding-a-model.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
