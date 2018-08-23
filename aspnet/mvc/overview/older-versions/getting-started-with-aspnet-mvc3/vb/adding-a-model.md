---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
title: 모델 (VB) 추가 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 하는 중...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: b3aa7720-5c78-4ca2-baef-9a52234fb7ce
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 0c846d31fb6b24ad964d69d0f81858c87305d68c
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824131"
---
<a name="adding-a-model-vb"></a><span data-ttu-id="6c4ee-103">모델 (VB) 추가</span><span class="sxs-lookup"><span data-stu-id="6c4ee-103">Adding a Model (VB)</span></span>
====================
<span data-ttu-id="6c4ee-104">[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="6c4ee-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="6c4ee-105">이 자습서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, Microsoft Visual Studio의 무료 버전인를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="6c4ee-106">시작 하기 전에 아래에 나열 된 필수 구성 요소를 설치한 다음 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="6c4ee-107">다음 링크를 클릭 하 여 이들 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="6c4ee-108">또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="6c4ee-109">Visual Studio Web Developer Express SP1 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="6c4ee-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="6c4ee-110">ASP.NET MVC 3 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="6c4ee-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="6c4ee-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)</span><span class="sxs-lookup"><span data-stu-id="6c4ee-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="6c4ee-112">Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소를 설치 합니다. [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="6c4ee-113">VB.NET 소스 코드를 사용 하 여 Visual Web Developer 프로젝트는 다음이 항목과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="6c4ee-114">[VB.NET 버전](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="6c4ee-115">원하는 경우 C#으로 전환 합니다 [C# 버전](../cs/adding-a-model.md) 이 자습서의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-115">If you prefer C#, switch to the [C# version](../cs/adding-a-model.md) of this tutorial.</span></span>


## <a name="adding-a-model"></a><span data-ttu-id="6c4ee-116">모델 추가</span><span class="sxs-lookup"><span data-stu-id="6c4ee-116">Adding a Model</span></span>

<span data-ttu-id="6c4ee-117">이 섹션에서는 데이터베이스에서 동영상을 관리 하기 위한 일부 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-117">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="6c4ee-118">이러한 클래스는 ASP.NET MVC 응용 프로그램에는 "모델" 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-118">These classes will be the "model" part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="6c4ee-119">이러한 모델 클래스를 정의 및 작업에.NET Framework 데이터 액세스 기술을 통해 Entity Framework를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-119">You'll use a .NET Framework data-access technology known as the Entity Framework to define and work with these model classes.</span></span> <span data-ttu-id="6c4ee-120">라고 하는 개발 패러다임을 Entity Framework (EF 라고도 함) 지원 *Code First*합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-120">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="6c4ee-121">먼저 코드를 사용 하면 간단한 클래스를 작성 하 여 모델 개체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-121">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="6c4ee-122">(이 경우 "plain old CLR object. POCO 클래스에도 함) 그런 다음이 매우 명확 하 고 신속한 개발 워크플로 통해 클래스를에서 즉석에서 생성 된 데이터베이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-122">(These are also known as POCO classes, from "plain-old CLR objects.") You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="6c4ee-123">모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="6c4ee-123">Adding Model Classes</span></span>

<span data-ttu-id="6c4ee-124">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *모델* 폴더를 선택 **추가**를 선택한 후 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-124">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="6c4ee-125">"영화" 클래스를 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-125">Name the class "Movie".</span></span>

<span data-ttu-id="6c4ee-126">다음 5 개의 속성을 추가 합니다 `Movie` 클래스:</span><span class="sxs-lookup"><span data-stu-id="6c4ee-126">Add the following five properties to the `Movie` class:</span></span>

[!code-vb[Main](adding-a-model/samples/sample1.vb)]

<span data-ttu-id="6c4ee-127">사용 된 `Movie` 데이터베이스에서 동영상을 나타내는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-127">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="6c4ee-128">각 인스턴스는 `Movie` 개체의 각 속성과 데이터베이스 테이블 내의 행에 해당 합니다 `Movie` 클래스는 테이블의 열에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-128">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="6c4ee-129">동일한 파일에 다음 추가 `MovieDBContext` 클래스:</span><span class="sxs-lookup"><span data-stu-id="6c4ee-129">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-vb[Main](adding-a-model/samples/sample2.vb)]

<span data-ttu-id="6c4ee-130">`MovieDBContext` 페치, 저장 및 업데이트를 처리 하는 Entity Framework 영화 데이터베이스 컨텍스트 클래스를 나타냅니다 `Movie` 클래스 인스턴스의 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-130">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="6c4ee-131">합니다 `MovieDBContext` 에서 파생 되는 `DbContext` 기본 Entity Framework에서 제공 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-131">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span> <span data-ttu-id="6c4ee-132">에 대 한 자세한 내용은 `DbContext` 하 고 `DbSet`를 참조 하세요 [Entity Framework에 대 한 생산성 향상](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="6c4ee-132">For more information about `DbContext` and `DbSet`, see [Productivity Improvements for the Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span></span>

<span data-ttu-id="6c4ee-133">참조할 수 있도록 `DbContext` 하 고 `DbSet`, 다음을 추가 해야 `imports` 파일의 맨 위에 있는 문을:</span><span class="sxs-lookup"><span data-stu-id="6c4ee-133">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `imports` statement at the top of the file:</span></span>

[!code-vb[Main](adding-a-model/samples/sample3.vb)]

<span data-ttu-id="6c4ee-134">전체 *Movie.vb* 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-134">The complete *Movie.vb* file is shown below.</span></span>

[!code-vb[Main](adding-a-model/samples/sample4.vb)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a><span data-ttu-id="6c4ee-135">연결 문자열 만들기 및 SQL Server Compact를 사용 하 여 작업</span><span class="sxs-lookup"><span data-stu-id="6c4ee-135">Creating a Connection String and Working with SQL Server Compact</span></span>

<span data-ttu-id="6c4ee-136">합니다 `MovieDBContext` 데이터베이스에 연결 및 매핑 작업을 처리 하는 클래스를 만든 `Movie` 데이터베이스 레코드에는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-136">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="6c4ee-137">할 질문 중 하나는 그러나에서 연결할 데이터베이스를 지정 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-137">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="6c4ee-138">연결 정보를 추가 하 여 로그인 할 수 있습니다 합니다 *Web.config* 응용 프로그램의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-138">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="6c4ee-139">응용 프로그램 루트를 엽니다 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-139">Open the application root *Web.config* file.</span></span> <span data-ttu-id="6c4ee-140">(하지 합니다 *Web.config* 파일을 *뷰* 폴더입니다.) 아래 이미지는 둘 다 표시 *Web.config* 파일; 열기를 *Web.config* 빨간색 원이 표시 된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-140">(Not the *Web.config* file in the *Views* folder.) The image below show both *Web.config* files; open the *Web.config* file circled in red.</span></span>

![](adding-a-model/_static/image2.png)

## 

<span data-ttu-id="6c4ee-141">다음 연결 문자열을 추가 합니다 `<connectionStrings>` 요소에는 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-141">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="6c4ee-142">다음 예제에서는 부분 합니다 *Web.config* 추가 되는 새 연결 문자열을 사용 하 여 파일:</span><span class="sxs-lookup"><span data-stu-id="6c4ee-142">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

<span data-ttu-id="6c4ee-143">코드 및 XML이 적은 양의 나타내고 영화 데이터를 데이터베이스에 저장 하기 위해 작성 하는 데 필요한 모든 경우</span><span class="sxs-lookup"><span data-stu-id="6c4ee-143">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="6c4ee-144">다음으로 빌드할 새 `MoviesController` 영화 데이터를 표시 하 고 새 동영상 목록을 만들 수 있도록 하는 데 사용할 수 있는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="6c4ee-144">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6c4ee-145">[이전](adding-a-view.md)
> [다음](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="6c4ee-145">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
