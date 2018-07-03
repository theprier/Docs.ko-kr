---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
title: 데이터 액세스 레이어 만들기 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 것에 대 한 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항 설명 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 0bbf7a6e-d7eb-4091-91e4-fff892777f32
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
msc.type: authoredcontent
ms.openlocfilehash: 5b4bb5bc89938836bc37e8ebd385fa966bc6f511
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37390040"
---
<a name="create-the-data-access-layer"></a><span data-ttu-id="c666c-103">데이터 액세스 레이어 만들기</span><span class="sxs-lookup"><span data-stu-id="c666c-103">Create the Data Access Layer</span></span>
====================
<span data-ttu-id="c666c-104">[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="c666c-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="c666c-105">[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF) 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="c666c-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="c666c-106">이 자습서 시리즈는 ASP.NET 4.5와 Microsoft Visual Studio Express 2013 for Web 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="c666c-107">Visual Studio 2013 [C# 소스 코드를 사용 하 여 프로젝트](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 이 자습서 시리즈를 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>


<span data-ttu-id="c666c-108">이 자습서에는 만들기, 액세스 및 ASP.NET Web Forms 및 Entity Framework Code First를 사용 하 여 데이터베이스에서 데이터를 검토 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-108">This tutorial describes how to create, access, and review data from a database using ASP.NET Web Forms and Entity Framework Code First.</span></span> <span data-ttu-id="c666c-109">이 자습서는 이전 자습서 "프로젝트 만들기"를 기반 하 고 Wingtip 장난감 자습서 시리즈의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-109">This tutorial builds on the previous tutorial "Create the Project" and is part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="c666c-110">이 자습서를 완료 하는 만든 데이터 액세스 클래스에 있는 그룹에는 *모델* 프로젝트의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-110">When you've completed this tutorial, you will have built a group of data-access classes that are in the *Models* folder of the project.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="c666c-111">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="c666c-111">What you'll learn:</span></span>

- <span data-ttu-id="c666c-112">데이터 모델을 만드는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-112">How to create the data models.</span></span>
- <span data-ttu-id="c666c-113">데이터베이스를 만들고 초기화 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="c666c-113">How to initialize and seed the database.</span></span>
- <span data-ttu-id="c666c-114">업데이트 및 데이터베이스를 지원 하도록 응용 프로그램을 구성 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-114">How to update and configure the application to support the database.</span></span>

### <a name="these-are-the-features-introduced-in-the-tutorial"></a><span data-ttu-id="c666c-115">다음은 자습서에서 도입 된 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-115">These are the features introduced in the tutorial:</span></span>

- <span data-ttu-id="c666c-116">Entity Framework Code First</span><span class="sxs-lookup"><span data-stu-id="c666c-116">Entity Framework Code First</span></span>
- <span data-ttu-id="c666c-117">LocalDB</span><span class="sxs-lookup"><span data-stu-id="c666c-117">LocalDB</span></span>
- <span data-ttu-id="c666c-118">데이터 주석</span><span class="sxs-lookup"><span data-stu-id="c666c-118">Data Annotations</span></span>

## <a name="creating-the-data-models"></a><span data-ttu-id="c666c-119">데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="c666c-119">Creating the Data Models</span></span>

<span data-ttu-id="c666c-120">[Entity Framework](https://msdn.microsoft.com/data/aa937723) 는 (ORM) 개체-관계형 매핑 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-120">[Entity Framework](https://msdn.microsoft.com/data/aa937723) is an object-relational mapping (ORM) framework.</span></span> <span data-ttu-id="c666c-121">일반적으로 작성 해야 하는 데이터 액세스 코드가 대부분 제거 개체로 관계형 데이터로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-121">It lets you work with relational data as objects, eliminating most of the data-access code that you'd usually need to write.</span></span> <span data-ttu-id="c666c-122">Entity Framework를 사용 하 여를 사용 하 여 쿼리를 실행할 수 있습니다 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx), 다음 검색 및 강력한 형식의 개체로 데이터를 조작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-122">Using Entity Framework, you can issue queries using [LINQ](https://msdn.microsoft.com/library/bb397926.aspx), then retrieve and manipulate data as strongly typed objects.</span></span> <span data-ttu-id="c666c-123">LINQ는 데이터 쿼리 및 업데이트에 대 한 패턴을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-123">LINQ provides patterns for querying and updating data.</span></span> <span data-ttu-id="c666c-124">Entity Framework를 사용 하 여 액세스 기초를 데이터에 집중 하는 것이 아니라 응용 프로그램의 나머지 부분을 만드는 데 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-124">Using Entity Framework allows you to focus on creating the rest of your application, rather than focusing on the data access fundamentals.</span></span> <span data-ttu-id="c666c-125">이 자습서 시리즈의 뒷부분에 나오는 데이터 탐색 및 제품 쿼리를 채우는 데 사용 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-125">Later in this tutorial series, we'll show you how to use the data to populate navigation and product queries.</span></span>

<span data-ttu-id="c666c-126">Entity Framework 지원 호출 하는 개발 패러다임 *Code First*합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-126">Entity Framework supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="c666c-127">먼저 코드에서는 클래스를 사용 하 여 데이터 모델을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-127">Code First lets you define your data models using classes.</span></span> <span data-ttu-id="c666c-128">클래스는 다른 형식, 메서드 및 이벤트 변수를 그룹화 하 여 사용자 고유의 사용자 지정 형식을 만들 수 있는 구문.</span><span class="sxs-lookup"><span data-stu-id="c666c-128">A class is a construct that enables you to create your own custom types by grouping together variables of other types, methods and events.</span></span> <span data-ttu-id="c666c-129">기존 데이터베이스에 클래스를 매핑할 수도 있고 하는 데이터베이스를 생성 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-129">You can map classes to an existing database or use them to generate a database.</span></span> <span data-ttu-id="c666c-130">이 자습서에서는 데이터 모델 클래스를 작성 하 여 데이터 모델을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-130">In this tutorial, you'll create the data models by writing data model classes.</span></span> <span data-ttu-id="c666c-131">그런 다음 Entity Framework에서 이러한 새 클래스를 즉석에서 데이터베이스를 만들 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-131">Then, you'll let Entity Framework create the database on the fly from these new classes.</span></span>

<span data-ttu-id="c666c-132">Web Forms 응용 프로그램에 대 한 데이터 모델을 정의 하는 엔터티 클래스를 만들어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-132">You will begin by creating the entity classes that define the data models for the Web Forms application.</span></span> <span data-ttu-id="c666c-133">그런 다음 엔터티 클래스를 관리 하 고 데이터베이스에 대 한 데이터 액세스를 제공 하는 상황에 맞는 클래스를 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-133">Then you will create a context class that manages the entity classes and provides data access to the database.</span></span> <span data-ttu-id="c666c-134">또한 데이터베이스를 채우는 데 사용할 이니셜라이저 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-134">You will also create an initializer class that you will use to populate the database.</span></span>

### <a name="entity-framework-and-references"></a><span data-ttu-id="c666c-135">엔터티 프레임 워크 및 참조</span><span class="sxs-lookup"><span data-stu-id="c666c-135">Entity Framework and References</span></span>

<span data-ttu-id="c666c-136">기본적으로 Entity Framework는 포함 된 새 만들면 **ASP.NET 웹 응용 프로그램** 사용 하는 **Web Forms** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="c666c-136">By default, Entity Framework is included when you create a new **ASP.NET Web Application** using the **Web Forms** template.</span></span> <span data-ttu-id="c666c-137">Entity Framework는 설치, 제거 및 NuGet 패키지로 업데이트 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-137">Entity Framework can be installed, uninstalled, and updated as a NuGet package.</span></span>

<span data-ttu-id="c666c-138">이 NuGet 패키지에는 다음과 같습니다 **런타임** 프로젝트 내에서 어셈블리:</span><span class="sxs-lookup"><span data-stu-id="c666c-138">This NuGet package includes the following **runtime** assemblies within your project:</span></span>

- <span data-ttu-id="c666c-139">EntityFramework.dll – 모든 공용 런타임 코드가 Entity Framework 사용</span><span class="sxs-lookup"><span data-stu-id="c666c-139">EntityFramework.dll – All the common runtime code used by Entity Framework</span></span>
- <span data-ttu-id="c666c-140">EntityFramework.SqlServer.dll-Entity Framework 용 Microsoft SQL Server 공급자</span><span class="sxs-lookup"><span data-stu-id="c666c-140">EntityFramework.SqlServer.dll – The Microsoft SQL Server provider for Entity Framework</span></span>

### <a name="entity-classes"></a><span data-ttu-id="c666c-141">엔터티 클래스</span><span class="sxs-lookup"><span data-stu-id="c666c-141">Entity Classes</span></span>

<span data-ttu-id="c666c-142">데이터의 스키마를 정의 하기 위해 만든 클래스에는 엔터티 클래스 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-142">The classes you create to define the schema of the data are called entity classes.</span></span> <span data-ttu-id="c666c-143">데이터베이스 디자인을 처음 접하는 경우 데이터베이스의 테이블 정의로 엔터티 클래스의 생각 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-143">If you're new to database design, think of the entity classes as table definitions of a database.</span></span> <span data-ttu-id="c666c-144">클래스의 각 속성 데이터베이스의 테이블의 열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-144">Each property in the class specifies a column in the table of the database.</span></span> <span data-ttu-id="c666c-145">이러한 클래스는 개체 지향 코드와 데이터베이스의 관계형 테이블 구조 개체-관계형 간단한 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-145">These classes provide a lightweight, object-relational interface between object-oriented code and the relational table structure of the database.</span></span>

<span data-ttu-id="c666c-146">이 자습서에서는 제품 및 범주에 대 한 스키마를 나타내는 간단한 엔터티 클래스를 추가 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-146">In this tutorial, you'll start out by adding simple entity classes representing the schemas for products and categories.</span></span> <span data-ttu-id="c666c-147">Products 클래스에는 각 제품에 대 한 정의가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-147">The products class will contain definitions for each product.</span></span> <span data-ttu-id="c666c-148">각 product 클래스의 멤버의 이름은 `ProductID`, `ProductName`, `Description`, `ImagePath`를 `UnitPrice`를 `CategoryID`, 및 `Category`합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-148">The name of each of the members of the product class will be `ProductID`, `ProductName`, `Description`, `ImagePath`, `UnitPrice`, `CategoryID`, and `Category`.</span></span> <span data-ttu-id="c666c-149">범주 클래스에 속하는 제품 수, 자동차, 보트, 평면 등 각 범주에 대 한 정의가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-149">The category class will contain definitions for each category that a product can belong to, such as Car, Boat, or Plane.</span></span> <span data-ttu-id="c666c-150">범주 클래스의 멤버는 각각의 이름은 `CategoryID`, `CategoryName`를 `Description`, 및 `Products`합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-150">The name of each of the members of the category class will be `CategoryID`, `CategoryName`, `Description`, and `Products`.</span></span> <span data-ttu-id="c666c-151">각 제품 범주 중 하나에 속하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-151">Each product will belong to one of the categories.</span></span> <span data-ttu-id="c666c-152">이러한 엔터티 클래스는 프로젝트의 기존에 추가할 *모델* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-152">These entity classes will be added to the project's existing *Models* folder.</span></span>

1. <span data-ttu-id="c666c-153">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *모델* 폴더를 선택 하 고 **추가**  - &gt; **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-153">In **Solution Explorer**, right-click the *Models* folder and then select **Add** -&gt; **New Item**.</span></span> 

    ![데이터 액세스 계층-새 항목 메뉴 만들기](create_the_data_access_layer/_static/image1.png)

   <span data-ttu-id="c666c-155">**새 항목 추가** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-155">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="c666c-156">아래 **Visual C#** 에서 합니다 **설치 됨** 창 왼쪽에서 선택 **코드**합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-156">Under **Visual C#** from the **Installed** pane on the left, select **Code**.</span></span> 

    ![데이터 액세스 계층-새 항목 메뉴 만들기](create_the_data_access_layer/_static/image2.png)
3. <span data-ttu-id="c666c-158">선택 **클래스** 가운데 창에서이 새 클래스 이름을 *Product.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-158">Select **Class** from the middle pane and name this new class *Product.cs*.</span></span>
4. <span data-ttu-id="c666c-159">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-159">Click **Add**.</span></span>  
   <span data-ttu-id="c666c-160">새 클래스 파일을 편집기에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-160">The new class file is displayed in the editor.</span></span>
5. <span data-ttu-id="c666c-161">기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-161">Replace the default code with the following code:</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample1.cs)]
6. <span data-ttu-id="c666c-162">1 ~ 4 단계에는 있지만 새 클래스 이름을 반복 하 여 다른 클래스를 만듭니다 *Category.cs* 기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-162">Create another class by repeating steps 1 through 4, however, name the new class *Category.cs* and replace the default code with the following code:</span></span>  

    [!code-csharp[Main](create_the_data_access_layer/samples/sample2.cs)]

<span data-ttu-id="c666c-163">에서 설명한 대로 합니다 `Category` 클래스는 응용 프로그램 제품 유형을 판매할 하도록 설계 되었습니다 (같은 <a id="a"> </a> &quot;자동차&quot;, &quot;배&quot;, &quot;로켓&quot;등), 및 `Product` 클래스는 데이터베이스의 개별 제품 (toys)를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-163">As previously mentioned, the `Category` class represents the type of product that the application is designed to sell (such as <a id="a"></a>&quot;Cars&quot;, &quot;Boats&quot;, &quot;Rockets&quot;, and so on), and the `Product` class represents the individual products (toys) in the database.</span></span> <span data-ttu-id="c666c-164">각 인스턴스는 `Product` 관계형 데이터베이스 테이블 내의 행에 해당 개체 및 Product 클래스의 각 속성은 관계형 데이터베이스 테이블의 열에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-164">Each instance of a `Product` object will correspond to a row within a relational database table, and each property of the Product class will map to a column in the relational database table.</span></span> <span data-ttu-id="c666c-165">이 자습서의 뒷부분에서 데이터베이스에 포함 된 제품 데이터를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-165">Later in this tutorial, you'll review the product data contained in the database.</span></span>

### <a name="data-annotations"></a><span data-ttu-id="c666c-166">데이터 주석</span><span class="sxs-lookup"><span data-stu-id="c666c-166">Data Annotations</span></span>

<span data-ttu-id="c666c-167">알 수 있습니다 클래스의 특정 멤버와 같은 멤버에 대 한 세부 정보를 지정 하는 특성이 있는 `[ScaffoldColumn(false)]`합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-167">You may have noticed that certain members of the classes have attributes specifying details about the member, such as `[ScaffoldColumn(false)]`.</span></span> <span data-ttu-id="c666c-168">이들은 *데이터 주석*합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-168">These are *data annotations*.</span></span> <span data-ttu-id="c666c-169">데이터 주석 특성, 형식 지정 하 고 데이터베이스를 만들 때 모델링 되는 방법을 지정 하는 멤버에 대 한 사용자 입력의 유효성을 검사 하는 방법을 설명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-169">The data annotation attributes can describe how to validate user input for that member, to specify formatting for it, and to specify how it is modeled when the database is created.</span></span>

### <a name="context-class"></a><span data-ttu-id="c666c-170">Context 클래스</span><span class="sxs-lookup"><span data-stu-id="c666c-170">Context Class</span></span>

<span data-ttu-id="c666c-171">데이터 액세스를 위한 클래스를 사용 하려면 상황에 맞는 클래스를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-171">To start using the classes for data access, you must define a context class.</span></span> <span data-ttu-id="c666c-172">이전에 설명한 대로 컨텍스트 클래스가 엔터티 클래스를 관리 하는 (같은 합니다 `Product` 클래스 및 `Category` 클래스) 하 고 데이터베이스에 대 한 데이터 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-172">As mentioned previously, the context class manages the entity classes (such as the `Product` class and the `Category` class) and provides data access to the database.</span></span>

<span data-ttu-id="c666c-173">이 절차에서는 새 C# 상황에 맞는 클래스를 추가 합니다 *모델* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-173">This procedure adds a new C# context class to the *Models* folder.</span></span>

1. <span data-ttu-id="c666c-174">마우스 오른쪽 단추로 클릭 합니다 *모델* 한 다음 선택한 폴더 **추가**  - &gt; **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-174">Right-click the *Models* folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="c666c-175">**새 항목 추가** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-175">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="c666c-176">선택 **클래스** 이름을 가운데 창에서 *ProductContext.cs* 누릅니다 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-176">Select **Class** from the middle pane, name it *ProductContext.cs* and click **Add**.</span></span>
3. <span data-ttu-id="c666c-177">다음 코드를 사용 하 여 클래스에 포함 된 기본 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-177">Replace the default code contained in the class with the following code:</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample3.cs)]

<span data-ttu-id="c666c-178">이 코드를 추가 합니다 `System.Data.Entity` 네임 스페이스 쿼리 하는 기능을 포함 하는 Entity Framework의 모든 핵심 기능에 액세스할 수 있도록 삽입, 업데이트 및 강력한 형식의 개체를 사용 하 여 데이터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-178">This code adds the `System.Data.Entity` namespace so that you have access to all the core functionality of Entity Framework, which includes the capability to query, insert, update, and delete data by working with strongly typed objects.</span></span>

<span data-ttu-id="c666c-179">`ProductContext` 페치, 저장 및 업데이트를 처리 하는 Entity Framework 제품 데이터베이스 컨텍스트 클래스를 나타냅니다 `Product` 클래스 인스턴스의 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-179">The `ProductContext` class represents Entity Framework product database context, which handles fetching, storing, and updating `Product` class instances in the database.</span></span> <span data-ttu-id="c666c-180">합니다 `ProductContext` 클래스에서 파생 되는 `DbContext` 기본 Entity Framework에서 제공 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-180">The `ProductContext` class derives from the `DbContext` base class provided by Entity Framework.</span></span>

### <a name="initializer-class"></a><span data-ttu-id="c666c-181">이니셜라이저 클래스</span><span class="sxs-lookup"><span data-stu-id="c666c-181">Initializer Class</span></span>

<span data-ttu-id="c666c-182">초기화 컨텍스트에서 사용 되는 첫 번째 데이터베이스에 사용자 지정 논리를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-182">You will need to run some custom logic to initialize the database the first time the context is used.</span></span> <span data-ttu-id="c666c-183">이렇게 하면 시드 된 데이터를 제품 및 범주를 즉시 표시할 수 있도록 데이터베이스에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-183">This will allow seed data to be added to the database so that you can immediately display products and categories.</span></span>

<span data-ttu-id="c666c-184">이 절차에서는 새 C# 이니셜라이저 클래스를 추가 합니다 *모델* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-184">This procedure adds a new C# initializer class to the *Models* folder.</span></span>

1. <span data-ttu-id="c666c-185">만들면 `Class` 에 *모델* 폴더 이름을 *ProductDatabaseInitializer.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-185">Create another `Class` in the *Models* folder and name it *ProductDatabaseInitializer.cs*.</span></span>
2. <span data-ttu-id="c666c-186">다음 코드를 사용 하 여 클래스에 포함 된 기본 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-186">Replace the default code contained in the class with the following code:</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample4.cs)]

<span data-ttu-id="c666c-187">데이터베이스를 생성 하 고 초기화 하는 경우 위의 코드에서 볼 수는 `Seed` 속성은 재정의 하 고 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-187">As you can see from the above code, when the database is created and initialized, the `Seed` property is overridden and set.</span></span> <span data-ttu-id="c666c-188">경우는 `Seed` 속성, 범주 및 제품에서 값이 데이터베이스를 채우는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-188">When the `Seed` property is set, the values from the categories and products are used to populate the database.</span></span> <span data-ttu-id="c666c-189">데이터베이스가 만들어진 후에 위의 코드를 수정 하 여 시드 데이터를 업데이트 하려고 하면 웹 응용 프로그램을 실행 하는 경우 업데이트가 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-189">If you attempt to update the seed data by modifying the above code after the database has been created, you won't see any updates when you run the Web application.</span></span> <span data-ttu-id="c666c-190">이유는 위 코드의 구현을 사용 합니다 `DropCreateDatabaseIfModelChanges` 모델 (스키마) 시드 데이터를 다시 설정 하기 전에 변경 되었는지 여부를 인식 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-190">The reason is the above code uses an implementation of the `DropCreateDatabaseIfModelChanges` class to recognize if the model (schema) has changed before resetting the seed data.</span></span> <span data-ttu-id="c666c-191">에 변경 된 경우는 `Category` 고 `Product` 시드 데이터를 사용 하 여 엔터티 클래스를 데이터베이스 다시 초기화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-191">If no changes are made to the `Category` and `Product` entity classes, the database will not be reinitialized with the seed data.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="c666c-192">응용 프로그램을 실행 될 때마다 다시 생성 하려면 데이터베이스를 하려는 경우, 사용할 수 있습니다 합니다 `DropCreateDatabaseAlways` 클래스 대신는 `DropCreateDatabaseIfModelChanges` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-192">If you wanted the database to be recreated every time you ran the application, you could use the `DropCreateDatabaseAlways` class instead of the `DropCreateDatabaseIfModelChanges` class.</span></span> <span data-ttu-id="c666c-193">그러나이 자습서 시리즈에서는 사용 된 `DropCreateDatabaseIfModelChanges` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-193">However for this tutorial series, use the `DropCreateDatabaseIfModelChanges` class.</span></span>


<span data-ttu-id="c666c-194">이 시점에서이 자습서에서는 해야는 *모델* 네 개의 새로운 클래스 및 기본 클래스를 사용 하 여 폴더:</span><span class="sxs-lookup"><span data-stu-id="c666c-194">At this point in this tutorial, you will have a *Models* folder with four new classes and one default class:</span></span>

![데이터 액세스 계층-Models 폴더 만들기](create_the_data_access_layer/_static/image3.png)

### <a name="configuring-the-application-to-use-the-data-model"></a><span data-ttu-id="c666c-196">데이터 모델을 사용 하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="c666c-196">Configuring the Application to Use the Data Model</span></span>

<span data-ttu-id="c666c-197">데이터를 나타내는 클래스를 만들었으므로 이제 클래스를 사용 하 여 응용 프로그램을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-197">Now that you've created the classes that represent the data, you must configure the application to use the classes.</span></span> <span data-ttu-id="c666c-198">에 *Global.asax* 파일 모델을 초기화 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-198">In the *Global.asax* file, you add code that initializes the model.</span></span> <span data-ttu-id="c666c-199">에 *Web.config* 어떤 데이터베이스 응용 프로그램에 알려 주는 정보를 사용 하 여 새 데이터 클래스에 의해 표현 되는 데이터를 저장 하는 것이 추가한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-199">In the *Web.config* file you add information that tells the application what database you'll use to store the data that's represented by the new data classes.</span></span> <span data-ttu-id="c666c-200">합니다 *Global.asax* 응용 프로그램 이벤트 또는 메서드를 처리 하도록 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-200">The *Global.asax* file can be used to handle application events or methods.</span></span> <span data-ttu-id="c666c-201">합니다 *Web.config* 파일을 사용 하면 ASP.NET 웹 응용 프로그램의 구성을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-201">The *Web.config* file allows you to control the configuration of your ASP.NET web application.</span></span>

#### <a name="updating-the-globalasax-file"></a><span data-ttu-id="c666c-202">Global.asax 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="c666c-202">Updating the Global.asax file</span></span>

<span data-ttu-id="c666c-203">업데이트 파일을 시작 하면 응용 프로그램 데이터 모델을 초기화 하려면 합니다 `Application_Start` 처리기에는 *Global.asax.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-203">To initialize the data models when the application starts, you will update the `Application_Start` handler in the *Global.asax.cs* file.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="c666c-204">솔루션 탐색기에서 선택할 수 있습니다 합니다 *Global.asax* 파일 또는 *Global.asax.cs* 파일을 편집 합니다 *Global.asax.cs* 파일.</span><span class="sxs-lookup"><span data-stu-id="c666c-204">In Solution Explorer, you can select either the *Global.asax* file or the *Global.asax.cs* file to edit the *Global.asax.cs* file.</span></span>


1. <span data-ttu-id="c666c-205">노란색으로 강조 표시 된 다음 코드를 추가 합니다 `Application_Start` 의 메서드를 *Global.asax.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-205">Add the following code highlighted in yellow to the `Application_Start` method in the *Global.asax.cs* file.</span></span>   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample5.cs?highlight=9-10,22-23)]

> [!NOTE] 
> 
> <span data-ttu-id="c666c-206">브라우저는 HTML5는 브라우저에서이 자습서 시리즈를 보고 하는 경우 노란색으로 강조 표시 하는 코드를 보려면 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-206">Your browser must support HTML5 to view the code highlighted in yellow when viewing this tutorial series in a browser.</span></span>


<span data-ttu-id="c666c-207">위의 코드에서 응용 프로그램을 시작 하는 경우와 같이 응용 프로그램 액세스 하는 데이터 중 처음으로 실행 되는 이니셜라이저를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-207">As shown in the above code, when the application starts, the application specifies the initializer that will run during the first time the data is accessed.</span></span> <span data-ttu-id="c666c-208">두 개의 추가 네임 스페이스 액세스 해야 하는 `Database` 개체 및 `ProductDatabaseInitializer` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-208">The two additional namespaces are required to access the `Database` object and the `ProductDatabaseInitializer` object.</span></span>

 <span data-ttu-id="c666c-209">Web.Config 파일 수정</span><span class="sxs-lookup"><span data-stu-id="c666c-209">Modifying the Web.Config File</span></span> 

<span data-ttu-id="c666c-210">Entity Framework Code First는 생성 하지만 데이터베이스를 기본 위치에 데이터베이스 시드 데이터를 사용 하 여 채워질 때 응용 프로그램에 직접 연결 정보를 추가 하면 데이터베이스 위치를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-210">Although Entity Framework Code First will generate a database for you in a default location when the database is populated with seed data, adding your own connection information to your application gives you control of the database location.</span></span> <span data-ttu-id="c666c-211">응용 프로그램의 연결 문자열을 사용 하 여이 데이터베이스 연결을 지정할 *Web.config* 프로젝트의 루트에 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-211">You specify this database connection using a connection string in the application's *Web.config* file at the root of the project.</span></span> <span data-ttu-id="c666c-212">새 연결 문자열에 추가 하 여 데이터베이스의 위치를 지정할 수 있습니다 (*wingtiptoys.mdf*) 응용 프로그램의 데이터 디렉터리에 빌드할 (*앱\_데이터*), 기본값 대신 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-212">By adding a new connection string, you can direct the location of the database (*wingtiptoys.mdf*) to be built in the application's data directory (*App\_Data*), rather than its default location.</span></span> <span data-ttu-id="c666c-213">이렇게 변경 하면를 찾고이 자습서의 뒷부분에서 데이터베이스 파일을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-213">Making this change will allow you to find and inspect the database file later in this tutorial.</span></span>

1. <span data-ttu-id="c666c-214">**솔루션 탐색기**찾기 및 열기, 합니다 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-214">In **Solution Explorer**, find and open the *Web.config* file.</span></span>
2. <span data-ttu-id="c666c-215">노란색으로 강조 표시 된 연결 문자열을 추가 합니다 `<connectionStrings>` 의 섹션을 *Web.config* 다음과 같이 파일:</span><span class="sxs-lookup"><span data-stu-id="c666c-215">Add the connection string highlighted in yellow to the `<connectionStrings>` section of the *Web.config* file as follows:</span></span>  

    [!code-xml[Main](create_the_data_access_layer/samples/sample6.xml?highlight=4-7)]

<span data-ttu-id="c666c-216">응용 프로그램을 처음으로 실행 하는 경우 데이터베이스 연결 문자열에서 지정 된 위치에 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-216">When the application is run for the first time, it will build the database at the location specified by the connection string.</span></span> <span data-ttu-id="c666c-217">하지만 응용 프로그램을 실행 하기 전에 빌드 해 보겠습니다 것 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-217">But before running the application, let's build it first.</span></span>

## <a name="building-the-application"></a><span data-ttu-id="c666c-218">응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="c666c-218">Building the Application</span></span>

<span data-ttu-id="c666c-219">모든 클래스 및 웹 응용 프로그램에 대 한 변경 내용을 올바르게 작동 하는지, 응용 프로그램이 빌드되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-219">To make sure that all the classes and changes to your Web application work, you should build the application.</span></span>

1. <span data-ttu-id="c666c-220">**디버그** 메뉴에서 **빌드 WingtipToys**합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-220">From the **Debug** menu, select **Build WingtipToys**.</span></span>  
 <span data-ttu-id="c666c-221">합니다 **출력** 창이 표시 되 고 순조롭게 경우 표시는 *성공* 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-221">The **Output** window is displayed, and if all went well, you see a *succeeded* message.</span></span>  

    ![출력 Windows 데이터 액세스 계층-만들기](create_the_data_access_layer/_static/image4.png)

<span data-ttu-id="c666c-223">오류를 실행 하는 경우 위의 단계를 다시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-223">If you run into an error, re-check the above steps.</span></span> <span data-ttu-id="c666c-224">정보는 **출력** 파일에 문제가 있어 파일에 변경 내용을 필요한 경우 창이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-224">The information in the **Output** window will indicate which file has a problem and where in the file a change is required.</span></span> <span data-ttu-id="c666c-225">이 정보를 사용 하면 부분 위 단계를 검토 하 고 프로젝트에서 수정 해야 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-225">This information will enable you to determine what part of the above steps need to be reviewed and fixed in your project.</span></span>

## <a name="summary"></a><span data-ttu-id="c666c-226">요약</span><span class="sxs-lookup"><span data-stu-id="c666c-226">Summary</span></span>

<span data-ttu-id="c666c-227">이 자습서 시리즈의 수 있는 데이터 모델을 만들 뿐 데이터베이스를 만들고 초기화 하는 데 사용할 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-227">In this tutorial of the series you have created the data model, as well as, added the code that will be used to initialize and seed the database.</span></span> <span data-ttu-id="c666c-228">또한 응용 프로그램이 실행 될 때 데이터 모델을 사용 하도록 응용 프로그램을 구성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-228">You have also configured the application to use the data models when the application is run.</span></span>

<span data-ttu-id="c666c-229">다음 자습서에서는 UI를 업데이트, 추가 탐색 하 고 데이터베이스에서 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-229">In the next tutorial, you'll update the UI, add navigation, and retrieve data from the database.</span></span> <span data-ttu-id="c666c-230">그러면이 자습서에서 만든 엔터티 클래스에 따라 자동으로 생성 되는 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c666c-230">This will result in the database being automatically created based on the entity classes that you created in this tutorial.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c666c-231">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c666c-231">Additional Resources</span></span>

<span data-ttu-id="c666c-232">[Entity Framework 개요](https://msdn.microsoft.com/library/bb399567.aspx) </span><span class="sxs-lookup"><span data-stu-id="c666c-232">[Entity Framework Overview](https://msdn.microsoft.com/library/bb399567.aspx) </span></span>  
<span data-ttu-id="c666c-233">[ADO.NET Entity Framework 초보자 가이드](https://msdn.microsoft.com/data/ee712907) </span><span class="sxs-lookup"><span data-stu-id="c666c-233">[Beginner's Guide to the ADO.NET Entity Framework](https://msdn.microsoft.com/data/ee712907) </span></span>  
<span data-ttu-id="c666c-234">[Entity Framework를 사용 하 여 첫 번째 개발 코드](http://www.msteched.com/2010/Europe/DEV212) (비디오)</span><span class="sxs-lookup"><span data-stu-id="c666c-234">[Code First Development with Entity Framework](http://www.msteched.com/2010/Europe/DEV212) (video)</span></span>   
<span data-ttu-id="c666c-235">[Code First 관계 Fluent API](https://msdn.microsoft.com/data/hh134698) </span><span class="sxs-lookup"><span data-stu-id="c666c-235">[Code First Relationships Fluent API](https://msdn.microsoft.com/data/hh134698) </span></span>  
[<span data-ttu-id="c666c-236">Code First 데이터 주석</span><span class="sxs-lookup"><span data-stu-id="c666c-236">Code First Data Annotations</span></span>](https://msdn.microsoft.com/data/gg193958)  
[<span data-ttu-id="c666c-237">Entity Framework에 대 한 생산성 향상</span><span class="sxs-lookup"><span data-stu-id="c666c-237">Productivity Improvements for the Entity Framework</span></span>](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)

> [!div class="step-by-step"]
> <span data-ttu-id="c666c-238">[이전](create-the-project.md)
> [다음](ui_and_navigation.md)</span><span class="sxs-lookup"><span data-stu-id="c666c-238">[Previous](create-the-project.md)
[Next](ui_and_navigation.md)</span></span>
