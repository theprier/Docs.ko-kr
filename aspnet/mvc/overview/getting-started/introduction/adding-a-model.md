---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: 모델 추가 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: b3ef871c4d7627a03c8f0fd8cce9d3e97fc1a4ba
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="adding-a-model"></a><span data-ttu-id="7d4fd-102">모델 추가</span><span class="sxs-lookup"><span data-stu-id="7d4fd-102">Adding a Model</span></span>
====================
<span data-ttu-id="7d4fd-103">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="7d4fd-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

<span data-ttu-id="7d4fd-104">이 섹션에서는 데이터베이스에서 영화를 관리 하기 위한 몇 가지 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4fd-104">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="7d4fd-105">이러한 클래스 됩니다는 &quot;모델&quot; ASP.NET MVC 응용 프로그램의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="7d4fd-105">These classes will be the &quot;model&quot; part of the ASP.NET MVC app.</span></span>

<span data-ttu-id="7d4fd-106">라고 하는.NET Framework 데이터 액세스 기술 사용의 [Entity Framework](https://docs.microsoft.com/ef/) 정의 하 고 이러한 모델 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4fd-106">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://docs.microsoft.com/ef/) to define and work with these model classes.</span></span> <span data-ttu-id="7d4fd-107">Entity Framework (EF 라고도 함)에서 지 원하는 개발 패러다임 호출 *Code First*합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4fd-107">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="7d4fd-108">먼저 코드에서는 간단한 클래스를 작성 하 여 모델 개체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d4fd-108">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="7d4fd-109">(이러한 라 하 고 POCO 클래스에서 &quot;old CLR 개체입니다.&quot;) 다음 클래스에서는 매우 명확 하 고 신속 하 게 개발 워크플로 매핑함으로써 즉석에서 생성 된 데이터베이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d4fd-109">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span> <span data-ttu-id="7d4fd-110">데이터베이스를 만들려면 먼저 해야 할 경우에 EF 및 MVC 응용 프로그램 개발에 대 한 자세한 내용은이 자습서를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d4fd-110">If you are required to create the database first, you can still follow this tutorial to learn about MVC and EF app development.</span></span> <span data-ttu-id="7d4fd-111">Tom Fizmakens 수행 수 있습니다 [ASP.NET 스 캐 폴딩](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) 자습서 데이터베이스 첫 번째 접근 방식에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4fd-111">You can then follow Tom Fizmakens [ASP.NET Scaffolding](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) tutorial, which covers the database first approach.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="7d4fd-112">모델 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4fd-112">Adding Model Classes</span></span>

<span data-ttu-id="7d4fd-113">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *모델* 폴더를 **추가**를 선택한 후 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4fd-113">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="7d4fd-114">입력은 *클래스* 이름 &quot;영화&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4fd-114">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="7d4fd-115">다음 5 개의 속성을 추가 `Movie` 클래스:</span><span class="sxs-lookup"><span data-stu-id="7d4fd-115">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="7d4fd-116">에서는 `Movie` 를 데이터베이스에서 영화를 나타내는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7d4fd-116">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="7d4fd-117">각 인스턴스는 `Movie` 개체는 데이터베이스 테이블과의 각 속성에 있는 행에 해당 하는 `Movie` 클래스는 테이블의 열에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d4fd-117">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="7d4fd-118">참고: System.Data.Entity, 및 관련된 클래스를 사용 하기 위해 설치 해야는 [Entity Framework NuGet 패키지](https://www.nuget.org/packages/EntityFramework/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4fd-118">Note: In order to use System.Data.Entity, and the related class, you need to install the [Entity Framework NuGet Package](https://www.nuget.org/packages/EntityFramework/).</span></span> <span data-ttu-id="7d4fd-119">자세한 내용은 링크를 따라 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4fd-119">Follow the link for further instructions.</span></span>

<span data-ttu-id="7d4fd-120">같은 파일에 다음 추가 `MovieDBContext` 클래스:</span><span class="sxs-lookup"><span data-stu-id="7d4fd-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

<span data-ttu-id="7d4fd-121">`MovieDBContext` 클래스 인출 저장 하 고 업데이트를 처리 하는 Entity Framework 영화 데이터베이스 컨텍스트를 나타냅니다. `Movie` 클래스 인스턴스는 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d4fd-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="7d4fd-122">`MovieDBContext` 에서 파생 되는 `DbContext` 기본 클래스는 Entity Framework에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d4fd-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="7d4fd-123">참조할 수 있도록 `DbContext` 및 `DbSet`, 다음 코드를 추가 해야 할 `using` 문을 파일의 맨:</span><span class="sxs-lookup"><span data-stu-id="7d4fd-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="7d4fd-124">수동으로 using를 추가 하 여 이렇게 하려면 문이 빨간색의 구불구불한 선 위로 마우스를 가져가고 수, 클릭 `Show potential fixes` 클릭 `using System.Data.Entity;`</span><span class="sxs-lookup"><span data-stu-id="7d4fd-124">You can do this by manually adding the using statement, or you can hover over the red squiggly lines, click `Show potential fixes` and click `using System.Data.Entity;`</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="7d4fd-125">참고: 일부 사용 되지 않는 `using` 문이 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7d4fd-125">Note: Several unused `using` statements have been removed.</span></span> <span data-ttu-id="7d4fd-126">Visual Studio 회색으로 사용 하지 않는 종속성이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d4fd-126">Visual Studio will show unused dependencies as gray.</span></span> <span data-ttu-id="7d4fd-127">회색 종속성 위로 이동 하 여 사용 하지 않는 종속성을 제거, 클릭 수 `Show potential fixes` 클릭 **사용 하지 않는 Using 제거 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7d4fd-127">You can remove unused dependencies by hovering over the gray dependencies, click `Show potential fixes` and click **Remove Unused Usings.**</span></span>

![](adding-a-model/_static/image3.png)

<span data-ttu-id="7d4fd-128">마지막으로 모델 (MVC에서 M) 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7d4fd-128">We've finally added a model (the M in MVC).</span></span> <span data-ttu-id="7d4fd-129">다음 섹션에서 데이터베이스 연결 문자열이 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d4fd-129">In the next section you'll work with the database connection string.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7d4fd-130">[이전](adding-a-view.md)
> [다음](creating-a-connection-string.md)</span><span class="sxs-lookup"><span data-stu-id="7d4fd-130">[Previous](adding-a-view.md)
[Next](creating-a-connection-string.md)</span></span>
