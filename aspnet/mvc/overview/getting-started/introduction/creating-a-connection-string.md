---
uid: mvc/overview/getting-started/introduction/creating-a-connection-string
title: 연결 문자열 만들기 및 SQL Server LocalDB 사용 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 6127804d-c1a9-414d-8429-7f3dd0f56e97
msc.legacyurl: /mvc/overview/getting-started/introduction/creating-a-connection-string
msc.type: authoredcontent
ms.openlocfilehash: 73a3149c8c789221baa2e3804ebf15ed5a509ddf
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829409"
---
<a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="48567-102">연결 문자열 만들기 및 SQL Server LocalDB 사용</span><span class="sxs-lookup"><span data-stu-id="48567-102">Creating a Connection String and Working with SQL Server LocalDB</span></span>
====================
<span data-ttu-id="48567-103">[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="48567-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="48567-104">연결 문자열 만들기 및 SQL Server LocalDB 사용</span><span class="sxs-lookup"><span data-stu-id="48567-104">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="48567-105">합니다 `MovieDBContext` 데이터베이스에 연결 및 매핑 작업을 처리 하는 클래스를 만든 `Movie` 데이터베이스 레코드에는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="48567-105">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="48567-106">할 질문 중 하나는 그러나에서 연결할 데이터베이스를 지정 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="48567-106">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="48567-107">사용할 데이터베이스를 지정할 필요는 없습니다, Entity Framework는 기본적으로 기본 [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)합니다.</span><span class="sxs-lookup"><span data-stu-id="48567-107">You don't actually have to specify which database to use, Entity Framework will default to using [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span></span> <span data-ttu-id="48567-108">이 섹션에서는 명시적으로 추가 연결 문자열을 *Web.config* 응용 프로그램의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="48567-108">In this section we'll explicitly add a connection string in the *Web.config* file of the application.</span></span>

## <a name="sql-server-express-localdb"></a><span data-ttu-id="48567-109">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="48567-109">SQL Server Express LocalDB</span></span>

<span data-ttu-id="48567-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) 는 SQL Server Express 데이터베이스 엔진의 요청 시 시작 하 고 사용자 모드에서 실행 되는 경량 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="48567-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) is a lightweight version of the SQL Server Express Database Engine that starts on demand and runs in user mode.</span></span> <span data-ttu-id="48567-111">LocalDB 데이터베이스를 사용 하 여 작업할 수 있도록 하는 SQL Server Express의 특수 실행 모드에서 실행 *.mdf* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="48567-111">LocalDB runs in a special execution mode of SQL Server Express that enables you to work with databases as *.mdf* files.</span></span> <span data-ttu-id="48567-112">일반적으로, LocalDB 데이터베이스 파일에 보관 되는 *앱\_데이터* 웹 프로젝트의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="48567-112">Typically, LocalDB database files are kept in the *App\_Data* folder of a web project.</span></span>

<span data-ttu-id="48567-113">SQL Server Express는 프로덕션 웹 응용 프로그램에서 사용 하 여에 대 한 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="48567-113">SQL Server Express is not recommended for use in production web applications.</span></span> <span data-ttu-id="48567-114">LocalDB 특히 해서는 안 웹 응용 프로그램을 사용 하 여 프로덕션에 있으므로 IIS를 사용 하 여 작동 하도록 설계 되지는 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="48567-114">LocalDB in particular should not be used for production with a web application because it is not designed to work with IIS.</span></span> <span data-ttu-id="48567-115">그러나 LocalDB 데이터베이스를 SQL Server 또는 SQL Azure 쉽게 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48567-115">However, a LocalDB database can be easily migrated to SQL Server or SQL Azure.</span></span>

<span data-ttu-id="48567-116">Visual Studio 2017에서 Visual Studio를 사용 하 여 기본적으로 LocalDB는 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48567-116">In Visual Studio 2017, LocalDB is installed by default with Visual Studio.</span></span>

<span data-ttu-id="48567-117">기본적으로 Entity Framework 개체 컨텍스트 클래스와 동일 하 게 명명 된 연결 문자열을 찾습니다 (`MovieDBContext` 이 프로젝트에 대 한).</span><span class="sxs-lookup"><span data-stu-id="48567-117">By default, the Entity Framework looks for a connection string named the same as the object context class (`MovieDBContext` for this project).</span></span> <span data-ttu-id="48567-118">자세한 내용은 참조 [ASP.NET 웹 응용 프로그램에 대 한 SQL Server 연결 문자열](https://msdn.microsoft.com/library/jj653752.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="48567-118">For more information see [SQL Server Connection Strings for ASP.NET Web Applications](https://msdn.microsoft.com/library/jj653752.aspx).</span></span>

<span data-ttu-id="48567-119">응용 프로그램 루트를 엽니다 *Web.config* 파일 아래에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="48567-119">Open the application root *Web.config* file shown below.</span></span> <span data-ttu-id="48567-120">(하지 합니다 *Web.config* 파일을 *뷰* 폴더입니다.)</span><span class="sxs-lookup"><span data-stu-id="48567-120">(Not the *Web.config* file in the *Views* folder.)</span></span>

![](creating-a-connection-string/_static/image1.png)

<span data-ttu-id="48567-121">찾기는 `<connectionStrings>` 요소:</span><span class="sxs-lookup"><span data-stu-id="48567-121">Find the `<connectionStrings>` element:</span></span>

![](creating-a-connection-string/_static/image2.png)

<span data-ttu-id="48567-122">다음 연결 문자열을 추가 합니다 `<connectionStrings>` 요소에는 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="48567-122">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

<span data-ttu-id="48567-123">다음 예제에서는 부분 합니다 *Web.config* 추가 되는 새 연결 문자열을 사용 하 여 파일:</span><span class="sxs-lookup"><span data-stu-id="48567-123">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

<span data-ttu-id="48567-124">두 연결 문자열은 매우 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="48567-124">The two connection strings are very similar.</span></span> <span data-ttu-id="48567-125">첫 번째 연결 문자열 이름은 `DefaultConnection` 멤버 자격 데이터베이스가 응용 프로그램에 액세스할 수 있는 사용자를 제어 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48567-125">The first connection string is named `DefaultConnection` and is used for the membership database to control who can access the application.</span></span> <span data-ttu-id="48567-126">추가한 다음 연결 문자열을 명명 된 LocalDB 데이터베이스를 지정 합니다. *Movie.mdf* 에 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="48567-126">The connection string you've added specifies a LocalDB database named *Movie.mdf* located in the *App\_Data* folder.</span></span> <span data-ttu-id="48567-127">에서는 멤버 자격 데이터베이스를 사용 하 여 멤버 자격, 인증 및 보안에 대 한 자세한 내용은이 자습서에서는 won't, 내 자습서를 참조 하세요 [인증 및 SQL DB를 사용 하 여 ASP.NET MVC 앱을 만들고 Azure App Service에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다.</span><span class="sxs-lookup"><span data-stu-id="48567-127">We won't use the membership database in this tutorial, for more information on membership, authentication and security, see my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span>

<span data-ttu-id="48567-128">연결 문자열의 이름을의 이름과 일치 해야 합니다 [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="48567-128">The name of the connection string must match the name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class.</span></span>

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

<span data-ttu-id="48567-129">추가할 필요가 실제로 `MovieDBContext` 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="48567-129">You don't actually need to add the `MovieDBContext` connection string.</span></span> <span data-ttu-id="48567-130">연결 문자열을 지정 하지 않으면, Entity Framework 데이터베이스가 만들어집니다. LocalDB 사용자 디렉터리의 정규화 된 이름에는 [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) 클래스 (이 경우 `MvcMovie.Models.MovieDBContext`).</span><span class="sxs-lookup"><span data-stu-id="48567-130">If you don't specify a connection string, Entity Framework will create a LocalDB database in the users directory with the fully qualified name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class (in this case `MvcMovie.Models.MovieDBContext`).</span></span> <span data-ttu-id="48567-131">이름은 데이터베이스 원하는 붙어 있다면는 *합니다. MDF* 접미사.</span><span class="sxs-lookup"><span data-stu-id="48567-131">You can name the database anything you like, as long as it has the *.MDF* suffix.</span></span> <span data-ttu-id="48567-132">예를 들어 데이터베이스 이름이 했습니다 *MyFilms.mdf*합니다.</span><span class="sxs-lookup"><span data-stu-id="48567-132">For example, we could name the database *MyFilms.mdf*.</span></span>

<span data-ttu-id="48567-133">다음으로 빌드할 새 `MoviesController` 영화 데이터를 표시 하 고 새 동영상 목록을 만들 수 있도록 하는 데 사용할 수 있는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="48567-133">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="48567-134">[이전](adding-a-model.md)
> [다음](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="48567-134">[Previous](adding-a-model.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
