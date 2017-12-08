---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model
title: "모델 (C#)을 추가 | Microsoft Docs"
author: Rick-Anderson
description: "참고:이 자습서의 업데이트 된 버전은 ASP.NET MVC 5 및 Visual Studio 2013을 사용 하는 있습니다. 것이 더 안전 하 고 진행할 데모를 단순..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: 42355b95-5f1f-413e-8d16-14cdfaaefcd8
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 32f2fcdae9d92b84dcd9be8746e416cdf9a14c48
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="adding-a-model-c"></a><span data-ttu-id="7f639-104">모델 (C#)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-104">Adding a Model (C#)</span></span>
====================
<span data-ttu-id="7f639-105">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="7f639-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="7f639-106">이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉 Microsoft Visual Studio의 무료 버전을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-106">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="7f639-107">시작 하기 전에 아래에 나열 된 필수 구성 요소가 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-107">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="7f639-108">다음 링크를 클릭 하 여 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-108">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="7f639-109">또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-109">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="7f639-110">Visual Studio Web Developer Express SP1 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="7f639-110">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="7f639-111">ASP.NET MVC 3 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="7f639-111">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="7f639-112">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)</span><span class="sxs-lookup"><span data-stu-id="7f639-112">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="7f639-113">Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소 설치: [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-113">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="7f639-114">이 항목에 수반 C# 소스 코드를 사용 하 여 Visual Web Developer 프로젝트 ´ ù.</span><span class="sxs-lookup"><span data-stu-id="7f639-114">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="7f639-115">[C# 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-115">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="7f639-116">Visual Basic을 선호 하는 경우 전환의 [Visual Basic 버전](../vb/adding-a-model.md) 이 자습서의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-116">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/adding-a-model.md) of this tutorial.</span></span>


## <a name="adding-a-model"></a><span data-ttu-id="7f639-117">모델 추가</span><span class="sxs-lookup"><span data-stu-id="7f639-117">Adding a Model</span></span>

<span data-ttu-id="7f639-118">이 섹션에서는 데이터베이스에서 영화를 관리 하기 위한 몇 가지 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-118">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="7f639-119">이러한 클래스는 ASP.NET MVC 응용 프로그램의 "모델" 일부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-119">These classes will be the "model" part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="7f639-120">정의 하 고 이러한 모델 클래스를 사용 하려면.NET Framework 데이터 액세스 기술을 통해 Entity Framework를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-120">You'll use a .NET Framework data-access technology known as the Entity Framework to define and work with these model classes.</span></span> <span data-ttu-id="7f639-121">Entity Framework (EF 라고도 함)에서 지 원하는 개발 패러다임 호출 *Code First*합니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-121">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="7f639-122">먼저 코드에서는 간단한 클래스를 작성 하 여 모델 개체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-122">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="7f639-123">(이러한는 POCO 클래스에서 "일반 이전 CLR 개체" 라고도 함) 다음 클래스에서는 매우 명확 하 고 신속 하 게 개발 워크플로 매핑함으로써 즉석에서 생성 된 데이터베이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-123">(These are also known as POCO classes, from "plain-old CLR objects.") You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="7f639-124">모델 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-124">Adding Model Classes</span></span>

<span data-ttu-id="7f639-125">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *모델* 폴더를 **추가**를 선택한 후 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-125">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="7f639-126">이름에서 *클래스* "영화"입니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-126">Name the *class* "Movie".</span></span>

<span data-ttu-id="7f639-127">[![CreateMovieClass](adding-a-model/_static/image3.png)](adding-a-model/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="7f639-127">[![CreateMovieClass](adding-a-model/_static/image3.png)](adding-a-model/_static/image2.png)</span></span>

<span data-ttu-id="7f639-128">다음 5 개의 속성을 추가 `Movie` 클래스:</span><span class="sxs-lookup"><span data-stu-id="7f639-128">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="7f639-129">에서는 `Movie` 를 데이터베이스에서 영화를 나타내는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-129">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="7f639-130">각 인스턴스는 `Movie` 개체는 데이터베이스 테이블과의 각 속성에 있는 행에 해당 하는 `Movie` 클래스는 테이블의 열에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-130">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="7f639-131">같은 파일에 다음 추가 `MovieDBContext` 클래스:</span><span class="sxs-lookup"><span data-stu-id="7f639-131">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

<span data-ttu-id="7f639-132">`MovieDBContext` 클래스 인출 저장 하 고 업데이트를 처리 하는 Entity Framework 영화 데이터베이스 컨텍스트를 나타냅니다. `Movie` 클래스 인스턴스는 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-132">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="7f639-133">`MovieDBContext` 에서 파생 되는 `DbContext` 기본 클래스는 Entity Framework에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-133">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span> <span data-ttu-id="7f639-134">에 대 한 자세한 내용은 `DbContext` 및 `DbSet`, 참조 [Entity Framework에 대 한 성능 향상 기능](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-134">For more information about `DbContext` and `DbSet`, see [Productivity Improvements for the Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span></span>

<span data-ttu-id="7f639-135">참조할 수 있도록 `DbContext` 및 `DbSet`, 다음 코드를 추가 해야 할 `using` 문을 파일의 맨:</span><span class="sxs-lookup"><span data-stu-id="7f639-135">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="7f639-136">전체 *Movie.cs* 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-136">The complete *Movie.cs* file is shown below.</span></span>

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a><span data-ttu-id="7f639-137">연결 문자열 만들기 및 SQL Server Compact 작업</span><span class="sxs-lookup"><span data-stu-id="7f639-137">Creating a Connection String and Working with SQL Server Compact</span></span>

<span data-ttu-id="7f639-138">`MovieDBContext` 만든 클래스 매핑 및 데이터베이스에 연결 하는 작업을 처리 `Movie` 데이터베이스 레코드에는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-138">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="7f639-139">그러나 인지 궁금할 질문 중 하나는에 연결 하는 데이터베이스를 지정 하는 방법을입니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-139">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="7f639-140">연결 정보를 추가 하 여 작업입니다는 *Web.config* 응용 프로그램의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-140">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="7f639-141">응용 프로그램 루트를 열고 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-141">Open the application root *Web.config* file.</span></span> <span data-ttu-id="7f639-142">(하지는 *Web.config* 파일에 *뷰* 폴더입니다.) 다음 이미지는 둘 다 표시 *Web.config* 파일; 열기는 *Web.config* 빨간색에서 원이 표시 된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-142">(Not the *Web.config* file in the *Views* folder.) The image below show both *Web.config* files; open the *Web.config* file circled in red.</span></span>

![](adding-a-model/_static/image4.png)

### 

<span data-ttu-id="7f639-143">다음 연결 문자열을 추가할는 `<connectionStrings>` 요소에는 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-143">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="7f639-144">다음 예제에서는의 일부는 *Web.config* 파일을 추가 하는 새 연결 문자열:</span><span class="sxs-lookup"><span data-stu-id="7f639-144">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

<span data-ttu-id="7f639-145">이 적은 양의 코드 및 XML을 나타내고 동영상 데이터는 데이터베이스에 저장 하기 위해 작성 해야 할 모든 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-145">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="7f639-146">다음으로 빌드합니다.이 새 `MoviesController` 동영상 데이터를 표시 하 고 사용자가 새 동영상 목록을 만들 수 있도록 허용 하는 데 사용할 수 있는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7f639-146">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="7f639-147">[이전](adding-a-view.md)
[다음](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="7f639-147">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
