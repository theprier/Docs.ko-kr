---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
title: 모델 추가 | Microsoft Docs
author: Rick-Anderson
description: 참고:이 자습서의 업데이트 된 버전은 ASP.NET MVC 5 및 Visual Studio 2013을 사용 하는 있습니다. 것이 더 안전 하 고 진행할 데모를 단순...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/28/2012
ms.topic: article
ms.assetid: 53db72da-e0b9-44d9-b60b-6e6988c00b28
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 562a06e22aad62b6982aca3316a2dfe18a6eba2e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="adding-a-model"></a><span data-ttu-id="2d6ef-104">모델 추가</span><span class="sxs-lookup"><span data-stu-id="2d6ef-104">Adding a Model</span></span>
====================
<span data-ttu-id="2d6ef-105">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="2d6ef-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="2d6ef-106">이 자습서의 업데이트 된 버전은 사용할 수 있는 [여기](../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 및 Visual Studio 2013을 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="2d6ef-107">더 안전 하 고 따라 하기 쉽고 이며 더 많은 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>


<span data-ttu-id="2d6ef-108">이 섹션에서는 데이터베이스에서 영화를 관리 하기 위한 몇 가지 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-108">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="2d6ef-109">이러한 클래스 됩니다는 &quot;모델&quot; ASP.NET MVC 응용 프로그램의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-109">These classes will be the &quot;model&quot; part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="2d6ef-110">라고 하는.NET Framework 데이터 액세스 기술 사용의 [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) 정의 하 고 이러한 모델 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-110">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) to define and work with these model classes.</span></span> <span data-ttu-id="2d6ef-111">Entity Framework (EF 라고도 함)에서 지 원하는 개발 패러다임 호출 *Code First*합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-111">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="2d6ef-112">먼저 코드에서는 간단한 클래스를 작성 하 여 모델 개체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-112">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="2d6ef-113">(이러한 라 하 고 POCO 클래스에서 &quot;old CLR 개체입니다.&quot;) 다음 클래스에서는 매우 명확 하 고 신속 하 게 개발 워크플로 매핑함으로써 즉석에서 생성 된 데이터베이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-113">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="2d6ef-114">모델 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-114">Adding Model Classes</span></span>

<span data-ttu-id="2d6ef-115">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *모델* 폴더를 **추가**를 선택한 후 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-115">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="2d6ef-116">입력은 *클래스* 이름 &quot;영화&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-116">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="2d6ef-117">다음 5 개의 속성을 추가 `Movie` 클래스:</span><span class="sxs-lookup"><span data-stu-id="2d6ef-117">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="2d6ef-118">에서는 `Movie` 를 데이터베이스에서 영화를 나타내는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-118">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="2d6ef-119">각 인스턴스는 `Movie` 개체는 데이터베이스 테이블과의 각 속성에 있는 행에 해당 하는 `Movie` 클래스는 테이블의 열에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-119">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="2d6ef-120">같은 파일에 다음 추가 `MovieDBContext` 클래스:</span><span class="sxs-lookup"><span data-stu-id="2d6ef-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

<span data-ttu-id="2d6ef-121">`MovieDBContext` 클래스 인출 저장 하 고 업데이트를 처리 하는 Entity Framework 영화 데이터베이스 컨텍스트를 나타냅니다. `Movie` 클래스 인스턴스는 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="2d6ef-122">`MovieDBContext` 에서 파생 되는 `DbContext` 기본 클래스는 Entity Framework에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="2d6ef-123">참조할 수 있도록 `DbContext` 및 `DbSet`, 다음 코드를 추가 해야 할 `using` 문을 파일의 맨:</span><span class="sxs-lookup"><span data-stu-id="2d6ef-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="2d6ef-124">전체 *Movie.cs* 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-124">The complete *Movie.cs* file is shown below.</span></span> <span data-ttu-id="2d6ef-125">(여러 되지 않는 문을 사용 하 여 필요한 제거 되었습니다.)</span><span class="sxs-lookup"><span data-stu-id="2d6ef-125">(Several using statements that are not needed have been removed.)</span></span>

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="2d6ef-126">연결 문자열 만들기 및 SQL Server LocalDB 사용</span><span class="sxs-lookup"><span data-stu-id="2d6ef-126">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="2d6ef-127">`MovieDBContext` 만든 클래스 매핑 및 데이터베이스에 연결 하는 작업을 처리 `Movie` 데이터베이스 레코드에는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-127">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="2d6ef-128">그러나 인지 궁금할 질문 중 하나는에 연결 하는 데이터베이스를 지정 하는 방법을입니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-128">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="2d6ef-129">연결 정보를 추가 하 여 작업입니다는 *Web.config* 응용 프로그램의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-129">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="2d6ef-130">응용 프로그램 루트를 열고 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-130">Open the application root *Web.config* file.</span></span> <span data-ttu-id="2d6ef-131">(하지는 *Web.config* 파일에 *뷰* 폴더입니다.) 열기는 *Web.config* 빨간색으로 윤곽선 처리 파일.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-131">(Not the *Web.config* file in the *Views* folder.) Open the *Web.config* file outlined in red.</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="2d6ef-132">다음 연결 문자열을 추가할는 `<connectionStrings>` 요소에는 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-132">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="2d6ef-133">다음 예제에서는의 일부는 *Web.config* 파일을 추가 하는 새 연결 문자열:</span><span class="sxs-lookup"><span data-stu-id="2d6ef-133">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml?highlight=6-9)]

<span data-ttu-id="2d6ef-134">이 적은 양의 코드 및 XML을 나타내고 동영상 데이터는 데이터베이스에 저장 하기 위해 작성 해야 할 모든 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-134">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="2d6ef-135">다음으로 빌드합니다.이 새 `MoviesController` 동영상 데이터를 표시 하 고 사용자가 새 동영상 목록을 만들 수 있도록 허용 하는 데 사용할 수 있는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2d6ef-135">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2d6ef-136">[이전](adding-a-view.md)
> [다음](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="2d6ef-136">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
