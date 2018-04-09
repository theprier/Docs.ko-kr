---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
title: 데이터 액세스 계층 만들기 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈 것에 대 한 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 0bbf7a6e-d7eb-4091-91e4-fff892777f32
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
msc.type: authoredcontent
ms.openlocfilehash: 671d1bbf661dfb3e56c6ccd67ce0d383990918d6
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="create-the-data-access-layer"></a><span data-ttu-id="a3741-103">데이터 액세스 계층 만들기</span><span class="sxs-lookup"><span data-stu-id="a3741-103">Create the Data Access Layer</span></span>
====================
<span data-ttu-id="a3741-104">으로 [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="a3741-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="a3741-105">[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF)를 다운로드 합니다.](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="a3741-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="a3741-106">이 자습서 시리즈 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 웹에 대 한 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="a3741-107">Visual Studio 2013 [C# 소스 코드를 사용 하 여 프로젝트](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 이 자습서 시리즈를 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>


<span data-ttu-id="a3741-108">이 자습서에는 만들기, 액세스 및 ASP.NET Web Forms 및 Entity Framework Code First를 사용 하 여 데이터베이스에서 데이터를 검토 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-108">This tutorial describes how to create, access, and review data from a database using ASP.NET Web Forms and Entity Framework Code First.</span></span> <span data-ttu-id="a3741-109">이 자습서에서는 이전 자습서 "프로젝트 만들기"를 바탕으로 하며 Wingtip 장난감 저장소 자습서 시리즈의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-109">This tutorial builds on the previous tutorial "Create the Project" and is part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="a3741-110">이 자습서를 완료 합니다 빌드에 있는 데이터 액세스 클래스 들의 그룹은 *모델* 프로젝트의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-110">When you've completed this tutorial, you will have built a group of data-access classes that are in the *Models* folder of the project.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="a3741-111">학습 내용:</span><span class="sxs-lookup"><span data-stu-id="a3741-111">What you'll learn:</span></span>

- <span data-ttu-id="a3741-112">데이터 모델을 만드는 방법.</span><span class="sxs-lookup"><span data-stu-id="a3741-112">How to create the data models.</span></span>
- <span data-ttu-id="a3741-113">초기화 하 고 데이터베이스를 시드하고 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="a3741-113">How to initialize and seed the database.</span></span>
- <span data-ttu-id="a3741-114">업데이트 및 응용 프로그램 데이터베이스를 지원 하도록 구성 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="a3741-114">How to update and configure the application to support the database.</span></span>

### <a name="these-are-the-features-introduced-in-the-tutorial"></a><span data-ttu-id="a3741-115">다음은 자습서에 도입 된 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-115">These are the features introduced in the tutorial:</span></span>

- <span data-ttu-id="a3741-116">Entity Framework Code First</span><span class="sxs-lookup"><span data-stu-id="a3741-116">Entity Framework Code First</span></span>
- <span data-ttu-id="a3741-117">LocalDB</span><span class="sxs-lookup"><span data-stu-id="a3741-117">LocalDB</span></span>
- <span data-ttu-id="a3741-118">데이터 주석</span><span class="sxs-lookup"><span data-stu-id="a3741-118">Data Annotations</span></span>

## <a name="creating-the-data-models"></a><span data-ttu-id="a3741-119">데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="a3741-119">Creating the Data Models</span></span>

<span data-ttu-id="a3741-120">[Entity Framework](https://msdn.microsoft.com/data/aa937723) (ORM) 개체-관계형 매핑 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-120">[Entity Framework](https://msdn.microsoft.com/data/aa937723) is an object-relational mapping (ORM) framework.</span></span> <span data-ttu-id="a3741-121">관계형 데이터를 쓰려고 일반적으로 해야 하는 데이터 액세스 코드의 대부분 제거 개체로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-121">It lets you work with relational data as objects, eliminating most of the data-access code that you'd usually need to write.</span></span> <span data-ttu-id="a3741-122">Entity Framework를 사용 하 여 사용 하 여 쿼리를 실행할 수 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx), 다음 검색 및 강력한 형식의 개체로 데이터를 조작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-122">Using Entity Framework, you can issue queries using [LINQ](https://msdn.microsoft.com/library/bb397926.aspx), then retrieve and manipulate data as strongly typed objects.</span></span> <span data-ttu-id="a3741-123">LINQ 쿼리 및 데이터를 업데이트 하기 위한 패턴을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-123">LINQ provides patterns for querying and updating data.</span></span> <span data-ttu-id="a3741-124">Entity Framework를 사용 하 여 액세스 기초를 데이터에 집중 하는 대신 응용 프로그램의 나머지 부분을 만드는 데 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-124">Using Entity Framework allows you to focus on creating the rest of your application, rather than focusing on the data access fundamentals.</span></span> <span data-ttu-id="a3741-125">이 자습서 시리즈의 뒷부분에 나오는 데이터 탐색 및 제품 쿼리를 채우는 데 사용 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-125">Later in this tutorial series, we'll show you how to use the data to populate navigation and product queries.</span></span>

<span data-ttu-id="a3741-126">Entity Framework를 호출 하는 개발 패러다임 지원 *Code First*합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-126">Entity Framework supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="a3741-127">먼저 코드에서는 클래스를 사용 하 여 데이터 모델을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-127">Code First lets you define your data models using classes.</span></span> <span data-ttu-id="a3741-128">클래스는 고유한 사용자 지정 형식을 다른 형식, 메서드 및 이벤트 변수를 함께 그룹화 하 여 만들 수 있도록 하는 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-128">A class is a construct that enables you to create your own custom types by grouping together variables of other types, methods and events.</span></span> <span data-ttu-id="a3741-129">클래스는 기존 데이터베이스에 매핑하거나 데이터베이스를 생성 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-129">You can map classes to an existing database or use them to generate a database.</span></span> <span data-ttu-id="a3741-130">이 자습서에서는 데이터 모델 클래스를 작성 하 여 데이터 모델 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-130">In this tutorial, you'll create the data models by writing data model classes.</span></span> <span data-ttu-id="a3741-131">그런 다음 이러한 새 클래스에서 즉석에서 데이터베이스를 생성 하는 Entity Framework 해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-131">Then, you'll let Entity Framework create the database on the fly from these new classes.</span></span>

<span data-ttu-id="a3741-132">Web Forms 응용 프로그램에 대 한 데이터 모델을 정의 하는 엔터티 클래스를 만들어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-132">You will begin by creating the entity classes that define the data models for the Web Forms application.</span></span> <span data-ttu-id="a3741-133">그런 다음 엔터티 클래스를 관리 하 고 데이터베이스에 대 한 데이터 액세스를 제공 하는 컨텍스트 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-133">Then you will create a context class that manages the entity classes and provides data access to the database.</span></span> <span data-ttu-id="a3741-134">데이터베이스를 채우는 데 사용할 이니셜라이저 클래스도를 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-134">You will also create an initializer class that you will use to populate the database.</span></span>

### <a name="entity-framework-and-references"></a><span data-ttu-id="a3741-135">엔터티 프레임 워크 및 참조</span><span class="sxs-lookup"><span data-stu-id="a3741-135">Entity Framework and References</span></span>

<span data-ttu-id="a3741-136">기본적으로 Entity Framework는 포함 된 새를 만들 때 **ASP.NET 웹 응용 프로그램** 를 사용 하는 **Web Forms** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="a3741-136">By default, Entity Framework is included when you create a new **ASP.NET Web Application** using the **Web Forms** template.</span></span> <span data-ttu-id="a3741-137">Entity Framework 설치, 제거 및 NuGet 패키지를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-137">Entity Framework can be installed, uninstalled, and updated as a NuGet package.</span></span>

<span data-ttu-id="a3741-138">이 NuGet 패키지에는 다음과 같은 **런타임** 프로젝트 내에서 어셈블리:</span><span class="sxs-lookup"><span data-stu-id="a3741-138">This NuGet package includes the following **runtime** assemblies within your project:</span></span>

- <span data-ttu-id="a3741-139">EntityFramework.dll-모든 일반적인 런타임 코드 Entity Framework에서 사용 하는</span><span class="sxs-lookup"><span data-stu-id="a3741-139">EntityFramework.dll – All the common runtime code used by Entity Framework</span></span>
- <span data-ttu-id="a3741-140">EntityFramework.SqlServer.dll – Entity Framework 용 Microsoft SQL Server 공급자</span><span class="sxs-lookup"><span data-stu-id="a3741-140">EntityFramework.SqlServer.dll – The Microsoft SQL Server provider for Entity Framework</span></span>

### <a name="entity-classes"></a><span data-ttu-id="a3741-141">엔터티 클래스</span><span class="sxs-lookup"><span data-stu-id="a3741-141">Entity Classes</span></span>

<span data-ttu-id="a3741-142">데이터의 스키마를 정의 하기 위해 만드는 클래스는 엔터티 클래스 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-142">The classes you create to define the schema of the data are called entity classes.</span></span> <span data-ttu-id="a3741-143">데이터베이스 디자인을 처음 접하는 경우 데이터베이스의 테이블 정의로 엔터티 클래스의 생각 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-143">If you're new to database design, think of the entity classes as table definitions of a database.</span></span> <span data-ttu-id="a3741-144">클래스의 각 속성은 데이터베이스의 테이블에 열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-144">Each property in the class specifies a column in the table of the database.</span></span> <span data-ttu-id="a3741-145">이러한 클래스는 개체 지향 코드와 데이터베이스의 관계형 테이블 구조는 간단 하 고 개체-관계형 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-145">These classes provide a lightweight, object-relational interface between object-oriented code and the relational table structure of the database.</span></span>

<span data-ttu-id="a3741-146">이 자습서에서는 제품 및 범주에 대 한 스키마를 나타내는 간단한 엔터티 클래스를 추가 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-146">In this tutorial, you'll start out by adding simple entity classes representing the schemas for products and categories.</span></span> <span data-ttu-id="a3741-147">제품 클래스에는 각 제품에 대 한 정의가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-147">The products class will contain definitions for each product.</span></span> <span data-ttu-id="a3741-148">각 product 클래스 멤버의 이름은 됩니다 `ProductID`, `ProductName`, `Description`, `ImagePath`, `UnitPrice`, `CategoryID`, 및 `Category`합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-148">The name of each of the members of the product class will be `ProductID`, `ProductName`, `Description`, `ImagePath`, `UnitPrice`, `CategoryID`, and `Category`.</span></span> <span data-ttu-id="a3741-149">범주 클래스에는 제품 자동차, 보트, 평면 등,에 속할 수 있는 각 범주에 대 한 정의가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-149">The category class will contain definitions for each category that a product can belong to, such as Car, Boat, or Plane.</span></span> <span data-ttu-id="a3741-150">각 범주 클래스 멤버의 이름은 됩니다 `CategoryID`, `CategoryName`, `Description`, 및 `Products`합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-150">The name of each of the members of the category class will be `CategoryID`, `CategoryName`, `Description`, and `Products`.</span></span> <span data-ttu-id="a3741-151">각 제품 범주 중 하나에 속하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-151">Each product will belong to one of the categories.</span></span> <span data-ttu-id="a3741-152">이러한 엔터티 클래스를 프로젝트의 기존 추가할 *모델* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-152">These entity classes will be added to the project's existing *Models* folder.</span></span>

1. <span data-ttu-id="a3741-153">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *모델* 폴더 및 다음 선택 **추가**  - &gt; **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-153">In **Solution Explorer**, right-click the *Models* folder and then select **Add** -&gt; **New Item**.</span></span> 

    ![데이터 액세스 계층-새 항목 메뉴 만들기](create_the_data_access_layer/_static/image1.png)

   <span data-ttu-id="a3741-155">**새 항목 추가** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-155">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="a3741-156">아래 **Visual C#** 에서 **설치 됨** 선택 왼쪽 창에서 **코드**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-156">Under **Visual C#** from the **Installed** pane on the left, select **Code**.</span></span> 

    ![데이터 액세스 계층-새 항목 메뉴 만들기](create_the_data_access_layer/_static/image2.png)
3. <span data-ttu-id="a3741-158">선택 **클래스** 가운데 창에서이 새 클래스 이름 및 *Product.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-158">Select **Class** from the middle pane and name this new class *Product.cs*.</span></span>
4. <span data-ttu-id="a3741-159">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-159">Click **Add**.</span></span>  
   <span data-ttu-id="a3741-160">새 클래스 파일은 편집기에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-160">The new class file is displayed in the editor.</span></span>
5. <span data-ttu-id="a3741-161">기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-161">Replace the default code with the following code:</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample1.cs)]
6. <span data-ttu-id="a3741-162">하지만 1-4 단계는, 새 클래스의 이름을 반복 하 여 다른 클래스를 만들 *Category.cs* 기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-162">Create another class by repeating steps 1 through 4, however, name the new class *Category.cs* and replace the default code with the following code:</span></span>  

    [!code-csharp[Main](create_the_data_access_layer/samples/sample2.cs)]

<span data-ttu-id="a3741-163">에서 설명한 대로 `Category` 클래스는 응용 프로그램은 제품의 형식은 판매할 디자인 (같은 <a id="a"> </a> &quot;자동차&quot;, &quot;배&quot;, &quot;로켓&quot;등), 및 `Product` 클래스는 데이터베이스에서 개별 제품 (toys)를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-163">As previously mentioned, the `Category` class represents the type of product that the application is designed to sell (such as <a id="a"></a>&quot;Cars&quot;, &quot;Boats&quot;, &quot;Rockets&quot;, and so on), and the `Product` class represents the individual products (toys) in the database.</span></span> <span data-ttu-id="a3741-164">각 인스턴스는 `Product` 개체는 관계형 데이터베이스 테이블 내의 행에 해당 하 고 제품 클래스의 각 속성은 관계형 데이터베이스 테이블의 열에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-164">Each instance of a `Product` object will correspond to a row within a relational database table, and each property of the Product class will map to a column in the relational database table.</span></span> <span data-ttu-id="a3741-165">이 자습서의 뒷부분에 나오는 데이터베이스에 포함 된 제품 데이터를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-165">Later in this tutorial, you'll review the product data contained in the database.</span></span>

### <a name="data-annotations"></a><span data-ttu-id="a3741-166">데이터 주석</span><span class="sxs-lookup"><span data-stu-id="a3741-166">Data Annotations</span></span>

<span data-ttu-id="a3741-167">클래스의 특정 멤버와 같은 멤버에 대 한 세부 정보를 지정 하는 속성 한지 단어로 `[ScaffoldColumn(false)]`합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-167">You may have noticed that certain members of the classes have attributes specifying details about the member, such as `[ScaffoldColumn(false)]`.</span></span> <span data-ttu-id="a3741-168">이들은 *데이터 주석*합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-168">These are *data annotations*.</span></span> <span data-ttu-id="a3741-169">데이터 주석 특성,에 대 한 서식을 지정 하 고 데이터베이스를 만들 때 모델링 되는 방법을 지정 하려면 해당 멤버에 대 한 사용자 입력의 유효성을 검사 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-169">The data annotation attributes can describe how to validate user input for that member, to specify formatting for it, and to specify how it is modeled when the database is created.</span></span>

### <a name="context-class"></a><span data-ttu-id="a3741-170">Context 클래스</span><span class="sxs-lookup"><span data-stu-id="a3741-170">Context Class</span></span>

<span data-ttu-id="a3741-171">데이터 액세스를 위한 클래스를 사용 하 여을 시작 하려면 컨텍스트 클래스를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-171">To start using the classes for data access, you must define a context class.</span></span> <span data-ttu-id="a3741-172">컨텍스트 클래스는 엔터티 클래스를 관리에서 설명한 대로 (같은 `Product` 클래스 및 `Category` 클래스) 하 고 데이터베이스에 대 한 데이터 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-172">As mentioned previously, the context class manages the entity classes (such as the `Product` class and the `Category` class) and provides data access to the database.</span></span>

<span data-ttu-id="a3741-173">새 C# 컨텍스트 클래스를 추가 하는이 절차는 *모델* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-173">This procedure adds a new C# context class to the *Models* folder.</span></span>

1. <span data-ttu-id="a3741-174">마우스 오른쪽 단추로 클릭는 *모델* 폴더 및 다음 선택 **추가**  - &gt; **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-174">Right-click the *Models* folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="a3741-175">**새 항목 추가** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-175">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="a3741-176">선택 **클래스** 이름을 가운데 창에서 *ProductContext.cs* 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-176">Select **Class** from the middle pane, name it *ProductContext.cs* and click **Add**.</span></span>
3. <span data-ttu-id="a3741-177">다음 코드를 사용 하 여 클래스에 포함 된 기본 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-177">Replace the default code contained in the class with the following code:</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample3.cs)]

<span data-ttu-id="a3741-178">이 코드는 추가 `System.Data.Entity` 네임 스페이스를 쿼리 하는 기능을 포함 하는 Entity Framework의 모든 핵심 기능에 대 한 액세스를 마쳤으므로 삽입, 업데이트 및 강력한 형식의 개체를 사용 하 여 데이터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-178">This code adds the `System.Data.Entity` namespace so that you have access to all the core functionality of Entity Framework, which includes the capability to query, insert, update, and delete data by working with strongly typed objects.</span></span>

<span data-ttu-id="a3741-179">`ProductContext` 클래스 인출, 저장 및 업데이트 처리는 Entity Framework 제품 데이터베이스 컨텍스트를 나타내는 `Product` 클래스 인스턴스는 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-179">The `ProductContext` class represents Entity Framework product database context, which handles fetching, storing, and updating `Product` class instances in the database.</span></span> <span data-ttu-id="a3741-180">`ProductContext` 클래스에서 파생 되는 `DbContext` 기본 Entity Framework에서 제공 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-180">The `ProductContext` class derives from the `DbContext` base class provided by Entity Framework.</span></span>

### <a name="initializer-class"></a><span data-ttu-id="a3741-181">이니셜라이저 클래스</span><span class="sxs-lookup"><span data-stu-id="a3741-181">Initializer Class</span></span>

<span data-ttu-id="a3741-182">컨텍스트를 사용 하는 첫 번째 데이터베이스 시간을 초기화 하는 일부 사용자 지정 논리를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-182">You will need to run some custom logic to initialize the database the first time the context is used.</span></span> <span data-ttu-id="a3741-183">이렇게 하면 데이터 제품 및 범주를 즉시 표시할 수 있도록 데이터베이스에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-183">This will allow seed data to be added to the database so that you can immediately display products and categories.</span></span>

<span data-ttu-id="a3741-184">새 C# 이니셜라이저 클래스를 추가 하는이 절차는 *모델* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-184">This procedure adds a new C# initializer class to the *Models* folder.</span></span>

1. <span data-ttu-id="a3741-185">다른 만들 `Class` 에 *모델* 폴더 이름을 지정 *ProductDatabaseInitializer.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-185">Create another `Class` in the *Models* folder and name it *ProductDatabaseInitializer.cs*.</span></span>
2. <span data-ttu-id="a3741-186">다음 코드를 사용 하 여 클래스에 포함 된 기본 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-186">Replace the default code contained in the class with the following code:</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample4.cs)]

<span data-ttu-id="a3741-187">데이터베이스를 만들고 초기화 하는 위의 코드에서 볼 수 있듯이 `Seed` 속성을 재정의 하 고 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-187">As you can see from the above code, when the database is created and initialized, the `Seed` property is overridden and set.</span></span> <span data-ttu-id="a3741-188">경우는 `Seed` 속성이 설정 되어, 범주 및 제품에서 값이 데이터베이스를 채우는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-188">When the `Seed` property is set, the values from the categories and products are used to populate the database.</span></span> <span data-ttu-id="a3741-189">데이터베이스를 만든 후 위의 코드를 수정 하 여 시드 데이터를 업데이트 하려고 하면 웹 응용 프로그램을 실행 하면 모든 업데이트가 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-189">If you attempt to update the seed data by modifying the above code after the database has been created, you won't see any updates when you run the Web application.</span></span> <span data-ttu-id="a3741-190">이유는 위의 코드 구현을 사용 하는 `DropCreateDatabaseIfModelChanges` (스키마) 모델에는 데이터를 다시 설정 하기 전에 변경 되었는지 여부를 인식 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-190">The reason is the above code uses an implementation of the `DropCreateDatabaseIfModelChanges` class to recognize if the model (schema) has changed before resetting the seed data.</span></span> <span data-ttu-id="a3741-191">에 변경 될 경우는 `Category` 및 `Product` 시드 데이터 엔터티 클래스, 데이터베이스, 다시 초기화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-191">If no changes are made to the `Category` and `Product` entity classes, the database will not be reinitialized with the seed data.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="a3741-192">응용 프로그램을 실행 될 때마다 다시 만들어야 하는 데이터베이스를 원하는 경우, 사용할 수는 `DropCreateDatabaseAlways` 클래스 대신는 `DropCreateDatabaseIfModelChanges` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-192">If you wanted the database to be recreated every time you ran the application, you could use the `DropCreateDatabaseAlways` class instead of the `DropCreateDatabaseIfModelChanges` class.</span></span> <span data-ttu-id="a3741-193">그러나이 자습서 시리즈에 대 한 사용은 `DropCreateDatabaseIfModelChanges` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-193">However for this tutorial series, use the `DropCreateDatabaseIfModelChanges` class.</span></span>


<span data-ttu-id="a3741-194">이 시점에서이 자습서에서는 나면는 *모델* 네 개의 새로운 클래스 및 하나의 기본 클래스를 사용한 폴더:</span><span class="sxs-lookup"><span data-stu-id="a3741-194">At this point in this tutorial, you will have a *Models* folder with four new classes and one default class:</span></span>

![데이터 액세스 계층-모델 폴더를 만듭니다.](create_the_data_access_layer/_static/image3.png)

### <a name="configuring-the-application-to-use-the-data-model"></a><span data-ttu-id="a3741-196">데이터 모델을 사용 하 여 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="a3741-196">Configuring the Application to Use the Data Model</span></span>

<span data-ttu-id="a3741-197">데이터를 나타내는 클래스를 만들었으므로 이제 클래스를 사용 하는 응용 프로그램을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-197">Now that you've created the classes that represent the data, you must configure the application to use the classes.</span></span> <span data-ttu-id="a3741-198">에 *Global.asax* 모델을 초기화 하는 코드를 추가할 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-198">In the *Global.asax* file, you add code that initializes the model.</span></span> <span data-ttu-id="a3741-199">에 *Web.config* 어떤 데이터베이스 응용 프로그램에 알려 주는 정보를 사용 하 여 새 데이터 클래스에 의해 표현 되는 데이터 저장을 추가할 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-199">In the *Web.config* file you add information that tells the application what database you'll use to store the data that's represented by the new data classes.</span></span> <span data-ttu-id="a3741-200">*Global.asax* 응용 프로그램 이벤트 또는 메서드를 처리할 수 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-200">The *Global.asax* file can be used to handle application events or methods.</span></span> <span data-ttu-id="a3741-201">*Web.config* 파일을 사용 하면 ASP.NET 웹 응용 프로그램의 구성을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-201">The *Web.config* file allows you to control the configuration of your ASP.NET web application.</span></span>

#### <a name="updating-the-globalasax-file"></a><span data-ttu-id="a3741-202">Global.asax 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="a3741-202">Updating the Global.asax file</span></span>

<span data-ttu-id="a3741-203">을 초기화 하기 위해 데이터 모델 시작 하면 응용 프로그램을 업데이트 하는 `Application_Start` 의 처리기는 *Global.asax.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-203">To initialize the data models when the application starts, you will update the `Application_Start` handler in the *Global.asax.cs* file.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="a3741-204">솔루션 탐색기에서 선택할 수 있습니다는 *Global.asax* 파일 또는 *Global.asax.cs* 편집할 파일의 *Global.asax.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-204">In Solution Explorer, you can select either the *Global.asax* file or the *Global.asax.cs* file to edit the *Global.asax.cs* file.</span></span>


1. <span data-ttu-id="a3741-205">다음 코드를 노란색으로 강조 표시를 추가 `Application_Start` 에서 메서드는 *Global.asax.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-205">Add the following code highlighted in yellow to the `Application_Start` method in the *Global.asax.cs* file.</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample5.cs?highlight=9-10,22-23)]

> [!NOTE] 
> 
> <span data-ttu-id="a3741-206">브라우저는 HTML5 브라우저에서이 자습서 시리즈를 볼 때 노란색으로 강조 표시 하는 코드를 보려면를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-206">Your browser must support HTML5 to view the code highlighted in yellow when viewing this tutorial series in a browser.</span></span>


<span data-ttu-id="a3741-207">위의 코드는 응용 프로그램이 시작 될 때와 같이 이니셜라이저 중에 실행 되는 처음으로 데이터에 액세스 하는 응용 프로그램 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-207">As shown in the above code, when the application starts, the application specifies the initializer that will run during the first time the data is accessed.</span></span> <span data-ttu-id="a3741-208">두 개의 추가 네임 스페이스에 액세스 하는 데 필요한는 `Database` 개체 및 `ProductDatabaseInitializer` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-208">The two additional namespaces are required to access the `Database` object and the `ProductDatabaseInitializer` object.</span></span>

 <span data-ttu-id="a3741-209">Web.Config 파일 수정</span><span class="sxs-lookup"><span data-stu-id="a3741-209">Modifying the Web.Config File</span></span> 

<span data-ttu-id="a3741-210">Entity Framework Code First는 생성 하지만 데이터베이스를 기본 위치에 데이터베이스 데이터도 채워질 때 응용 프로그램에 직접 연결 정보를 추가 하면 데이터베이스 위치를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-210">Although Entity Framework Code First will generate a database for you in a default location when the database is populated with seed data, adding your own connection information to your application gives you control of the database location.</span></span> <span data-ttu-id="a3741-211">응용 프로그램의 연결 문자열을 사용 하 여이 데이터베이스 연결을 지정 *Web.config* 프로젝트의 루트에 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-211">You specify this database connection using a connection string in the application's *Web.config* file at the root of the project.</span></span> <span data-ttu-id="a3741-212">새 연결 문자열을 추가 하 여 데이터베이스의 위치를 지정할 수 있습니다 (*wingtiptoys.mdf*) 응용 프로그램의 데이터 디렉터리에 빌드할 (*앱\_데이터*), 기본 대신 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-212">By adding a new connection string, you can direct the location of the database (*wingtiptoys.mdf*) to be built in the application's data directory (*App\_Data*), rather than its default location.</span></span> <span data-ttu-id="a3741-213">이 변경을 적용 하면 검색 하 고이 자습서의 뒷부분에 나오는 데이터베이스 파일을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-213">Making this change will allow you to find and inspect the database file later in this tutorial.</span></span>

1. <span data-ttu-id="a3741-214">**솔루션 탐색기**찾기 및 열기는 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-214">In **Solution Explorer**, find and open the *Web.config* file.</span></span>
2. <span data-ttu-id="a3741-215">노란색으로 강조 표시 된 연결 문자열을 추가 `<connectionStrings>` 의 섹션은 *Web.config* 다음과 같이 파일:</span><span class="sxs-lookup"><span data-stu-id="a3741-215">Add the connection string highlighted in yellow to the `<connectionStrings>` section of the *Web.config* file as follows:</span></span>  

    [!code-xml[Main](create_the_data_access_layer/samples/sample6.xml?highlight=4-7)]

<span data-ttu-id="a3741-216">응용 프로그램을 처음으로 실행 된 연결 문자열에서 지정 된 위치의 데이터베이스가 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-216">When the application is run for the first time, it will build the database at the location specified by the connection string.</span></span> <span data-ttu-id="a3741-217">하지만 응용 프로그램을 실행 하기 전에 제작 해 보겠습니다 것 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-217">But before running the application, let's build it first.</span></span>

## <a name="building-the-application"></a><span data-ttu-id="a3741-218">응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="a3741-218">Building the Application</span></span>

<span data-ttu-id="a3741-219">을 모든 클래스와 웹 응용 프로그램에 대 한 변경 내용이 작동 하는지 확인 하기 위해 응용 프로그램을 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-219">To make sure that all the classes and changes to your Web application work, you should build the application.</span></span>

1. <span data-ttu-id="a3741-220">**디버그** 메뉴 선택 **빌드 WingtipToys**합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-220">From the **Debug** menu, select **Build WingtipToys**.</span></span>  
 <span data-ttu-id="a3741-221">**출력** 창이 표시 되 고 순조롭게 경우 표시는 *성공* 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-221">The **Output** window is displayed, and if all went well, you see a *succeeded* message.</span></span>  

    ![데이터 액세스 계층-출력 창을 만들기](create_the_data_access_layer/_static/image4.png)

<span data-ttu-id="a3741-223">오류를 실행 하면 위의 단계를 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-223">If you run into an error, re-check the above steps.</span></span> <span data-ttu-id="a3741-224">정보는 **출력** 에 문제가 되는 파일 및 파일의 변경이 필요한 경우 창을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-224">The information in the **Output** window will indicate which file has a problem and where in the file a change is required.</span></span> <span data-ttu-id="a3741-225">이 정보를 사용 하면 위 단계 중 어떤 부분이 검토 하 고 프로젝트에서 수정 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-225">This information will enable you to determine what part of the above steps need to be reviewed and fixed in your project.</span></span>

## <a name="summary"></a><span data-ttu-id="a3741-226">요약</span><span class="sxs-lookup"><span data-stu-id="a3741-226">Summary</span></span>

<span data-ttu-id="a3741-227">계열의이 자습서에서는 있습니다가 데이터 모델을 만든 뿐만 아니라, 초기화 하 고 데이터베이스를 시드하고 사용할 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-227">In this tutorial of the series you have created the data model, as well as, added the code that will be used to initialize and seed the database.</span></span> <span data-ttu-id="a3741-228">또한 응용 프로그램이 실행 될 때 데이터 모델을 사용 하도록 응용 프로그램을 구성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-228">You have also configured the application to use the data models when the application is run.</span></span>

<span data-ttu-id="a3741-229">다음 자습서에서는 UI를 업데이트, 추가 탐색 하 고 데이터베이스에서 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-229">In the next tutorial, you'll update the UI, add navigation, and retrieve data from the database.</span></span> <span data-ttu-id="a3741-230">이렇게 하면이 자습서에서 만든 엔터티 클래스에 따라 자동으로 생성 되는 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="a3741-230">This will result in the database being automatically created based on the entity classes that you created in this tutorial.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a3741-231">추가 자료</span><span class="sxs-lookup"><span data-stu-id="a3741-231">Additional Resources</span></span>

<span data-ttu-id="a3741-232">[Entity Framework 개요](https://msdn.microsoft.com/library/bb399567.aspx) </span><span class="sxs-lookup"><span data-stu-id="a3741-232">[Entity Framework Overview](https://msdn.microsoft.com/library/bb399567.aspx) </span></span>  
<span data-ttu-id="a3741-233">[ADO.NET Entity Framework에 대 한 기본 설명](https://msdn.microsoft.com/data/ee712907) </span><span class="sxs-lookup"><span data-stu-id="a3741-233">[Beginner's Guide to the ADO.NET Entity Framework](https://msdn.microsoft.com/data/ee712907) </span></span>  
<span data-ttu-id="a3741-234">[Entity Framework와 함께 첫 번째 개발 코드](http://www.msteched.com/2010/Europe/DEV212) (비디오)</span><span class="sxs-lookup"><span data-stu-id="a3741-234">[Code First Development with Entity Framework](http://www.msteched.com/2010/Europe/DEV212) (video)</span></span>   
<span data-ttu-id="a3741-235">[코드 첫 번째 관계 Fluent API](https://msdn.microsoft.com/data/hh134698) </span><span class="sxs-lookup"><span data-stu-id="a3741-235">[Code First Relationships Fluent API](https://msdn.microsoft.com/data/hh134698) </span></span>  
[<span data-ttu-id="a3741-236">코드의 첫 번째 데이터 주석</span><span class="sxs-lookup"><span data-stu-id="a3741-236">Code First Data Annotations</span></span>](https://msdn.microsoft.com/data/gg193958)  
[<span data-ttu-id="a3741-237">Entity Framework에 대 한 성능 향상 기능</span><span class="sxs-lookup"><span data-stu-id="a3741-237">Productivity Improvements for the Entity Framework</span></span>](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)

> [!div class="step-by-step"]
> <span data-ttu-id="a3741-238">[이전](create-the-project.md)
> [다음](ui_and_navigation.md)</span><span class="sxs-lookup"><span data-stu-id="a3741-238">[Previous](create-the-project.md)
[Next](ui_and_navigation.md)</span></span>
