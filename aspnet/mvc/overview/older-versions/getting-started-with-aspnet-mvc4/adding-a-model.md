---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
title: 모델 추가 | Microsoft Docs
author: Rick-Anderson
description: '참고: 업데이트 된이이 자습서는 ASP.NET MVC 5 및 Visual Studio 2013을 사용 하는 있습니다. 것이 더 안전 하 고 더 간단 하 게 따르고 데모 중...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 53db72da-e0b9-44d9-b60b-6e6988c00b28
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 5308d2d1d11f954db8a4502adb42223f69e0c675
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48578512"
---
<a name="adding-a-model"></a><span data-ttu-id="28947-104">모델 추가</span><span class="sxs-lookup"><span data-stu-id="28947-104">Adding a Model</span></span>
====================
<span data-ttu-id="28947-105">[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="28947-105">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> > [!NOTE]
> > <span data-ttu-id="28947-106">이 자습서는 업데이트 된 버전을 사용할 수 [여기](../../getting-started/introduction/getting-started.md) 는 ASP.NET MVC 5 및 Visual Studio 2013을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="28947-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="28947-107">보다 안전 하 고 더 간단 하 게 수행 되며 더 많은 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="28947-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>


<span data-ttu-id="28947-108">이 섹션에서는 데이터베이스에서 동영상을 관리 하기 위한 일부 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="28947-108">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="28947-109">이러한 클래스는 &quot;모델&quot; ASP.NET MVC 응용 프로그램의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="28947-109">These classes will be the &quot;model&quot; part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="28947-110">라고 하는.NET Framework 데이터 액세스 기술 사용 합니다 [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) 를 정의한 다음 이러한 모델 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="28947-110">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) to define and work with these model classes.</span></span> <span data-ttu-id="28947-111">라고 하는 개발 패러다임을 Entity Framework (EF 라고도 함) 지원 *Code First*합니다.</span><span class="sxs-lookup"><span data-stu-id="28947-111">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="28947-112">먼저 코드를 사용 하면 간단한 클래스를 작성 하 여 모델 개체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28947-112">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="28947-113">(이러한 이라고 POCO 클래스에서 &quot;plain old CLR object.&quot;) 그런 다음이 매우 명확 하 고 신속한 개발 워크플로 통해 클래스를에서 즉석에서 생성 된 데이터베이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28947-113">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="28947-114">모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="28947-114">Adding Model Classes</span></span>

<span data-ttu-id="28947-115">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *모델* 폴더를 선택 **추가**를 선택한 후 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="28947-115">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="28947-116">입력 된 *클래스* 이름 &quot;영화&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="28947-116">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="28947-117">다음 5 개의 속성을 추가 합니다 `Movie` 클래스:</span><span class="sxs-lookup"><span data-stu-id="28947-117">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="28947-118">사용 된 `Movie` 데이터베이스에서 동영상을 나타내는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="28947-118">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="28947-119">각 인스턴스는 `Movie` 개체의 각 속성과 데이터베이스 테이블 내의 행에 해당 합니다 `Movie` 클래스는 테이블의 열에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="28947-119">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="28947-120">동일한 파일에 다음 추가 `MovieDBContext` 클래스:</span><span class="sxs-lookup"><span data-stu-id="28947-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

<span data-ttu-id="28947-121">`MovieDBContext` 페치, 저장 및 업데이트를 처리 하는 Entity Framework 영화 데이터베이스 컨텍스트 클래스를 나타냅니다 `Movie` 클래스 인스턴스의 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28947-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="28947-122">합니다 `MovieDBContext` 에서 파생 되는 `DbContext` 기본 Entity Framework에서 제공 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="28947-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="28947-123">참조할 수 있도록 `DbContext` 하 고 `DbSet`, 다음을 추가 해야 `using` 파일의 맨 위에 있는 문을:</span><span class="sxs-lookup"><span data-stu-id="28947-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="28947-124">전체 *Movie.cs* 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="28947-124">The complete *Movie.cs* file is shown below.</span></span> <span data-ttu-id="28947-125">(여러이 아닌 문을 사용 하 여 필요한 제거 되었습니다.)</span><span class="sxs-lookup"><span data-stu-id="28947-125">(Several using statements that are not needed have been removed.)</span></span>

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="28947-126">연결 문자열 만들기 및 SQL Server LocalDB 사용</span><span class="sxs-lookup"><span data-stu-id="28947-126">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="28947-127">합니다 `MovieDBContext` 데이터베이스에 연결 및 매핑 작업을 처리 하는 클래스를 만든 `Movie` 데이터베이스 레코드에는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="28947-127">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="28947-128">할 질문 중 하나는 그러나에서 연결할 데이터베이스를 지정 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="28947-128">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="28947-129">연결 정보를 추가 하 여 로그인 할 수 있습니다 합니다 *Web.config* 응용 프로그램의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="28947-129">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="28947-130">응용 프로그램 루트를 엽니다 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="28947-130">Open the application root *Web.config* file.</span></span> <span data-ttu-id="28947-131">(하지 합니다 *Web.config* 파일을 *뷰* 폴더입니다.) 엽니다는 *Web.config* 빨간색 윤곽선이 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="28947-131">(Not the *Web.config* file in the *Views* folder.) Open the *Web.config* file outlined in red.</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="28947-132">다음 연결 문자열을 추가 합니다 `<connectionStrings>` 요소에는 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="28947-132">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="28947-133">다음 예제에서는 부분 합니다 *Web.config* 추가 되는 새 연결 문자열을 사용 하 여 파일:</span><span class="sxs-lookup"><span data-stu-id="28947-133">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml?highlight=6-9)]

<span data-ttu-id="28947-134">코드 및 XML이 적은 양의 나타내고 영화 데이터를 데이터베이스에 저장 하기 위해 작성 하는 데 필요한 모든 경우</span><span class="sxs-lookup"><span data-stu-id="28947-134">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="28947-135">다음으로 빌드할 새 `MoviesController` 영화 데이터를 표시 하 고 새 동영상 목록을 만들 수 있도록 하는 데 사용할 수 있는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="28947-135">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="28947-136">[이전](adding-a-view.md)
> [다음](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="28947-136">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
