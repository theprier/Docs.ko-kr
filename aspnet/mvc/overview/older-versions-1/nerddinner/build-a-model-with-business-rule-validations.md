---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: 비즈니스 규칙 유효성 검사를 사용 하 여 모델 빌드 | Microsoft Docs
author: microsoft
description: 3 단계는 म 두 쿼리를 사용 하 고 업데이트할 수 데이터베이스 업그레이드 되었으며 수정 응용 프로그램에 대 한 모델을 만드는 방법을 보여 줍니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: c5a482474fd2f41836f70952306ada5cd9136455
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874943"
---
<a name="build-a-model-with-business-rule-validations"></a><span data-ttu-id="5f2b7-103">비즈니스 규칙 유효성 검사를 사용 하 여 모델 빌드</span><span class="sxs-lookup"><span data-stu-id="5f2b7-103">Build a Model with Business Rule Validations</span></span>
====================
<span data-ttu-id="5f2b7-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="5f2b7-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="5f2b7-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="5f2b7-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="5f2b7-106">이 무료의 3 단계 ["업그레이드 되었으며 수정" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 하는 워크 쓰루는 작고 빌드만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-106">This is step 3 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="5f2b7-107">3 단계는 म 두 쿼리를 사용 하 고 업데이트할 수 데이터베이스 업그레이드 되었으며 수정 응용 프로그램에 대 한 모델을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-107">Step 3 shows how to create a model that we can use to both query and update the database for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="5f2b7-108">ASP.NET MVC 3을 사용 하는 경우 수행한 것이 좋습니다는 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-3-building-the-model"></a><span data-ttu-id="5f2b7-109">업그레이드 되었으며 수정 단계 3: 모델을 구축</span><span class="sxs-lookup"><span data-stu-id="5f2b7-109">NerdDinner Step 3: Building the Model</span></span>

<span data-ttu-id="5f2b7-110">모델-뷰-컨트롤러 프레임 워크에서 "모델" 용어 된 유효성 검사 및 비즈니스 규칙을 통합 하는 해당 도메인 논리는 응용 프로그램의 데이터를 나타내는 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-110">In a model-view-controller framework the term "model" refers to the objects that represent the data of the application, as well as the corresponding domain logic that integrates validation and business rules with it.</span></span> <span data-ttu-id="5f2b7-111">MVC 기반 응용 프로그램의 여러 가지 "핵심" 점에서 모델과 근본적으로 나중에 볼 수 있겠지만 드라이브의 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-111">The model is in many ways the "heart" of an MVC-based application, and as we'll see later fundamentally drives the behavior of it.</span></span>

<span data-ttu-id="5f2b7-112">ASP.NET MVC 프레임 워크를 지 원하는 모든 데이터 액세스 기술을 사용 하 고 개발자는 다양 한 포함 하 여 해당 모델을 구현 하는 풍부한.NET 데이터 옵션 중에서 선택할 수 있습니다: LINQ to Entities, LINQ to SQL, NHibernate, LLBLGen Pro, subsonic은 이러한 방식을, WilsonORM, 또는 원시 ADO. NET DataReaders 또는 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-112">The ASP.NET MVC framework supports using any data access technology, and developers can choose from a variety of rich .NET data options to implement their models including: LINQ to Entities, LINQ to SQL, NHibernate, LLBLGen Pro, SubSonic, WilsonORM, or just raw ADO.NET DataReaders or DataSets.</span></span>

<span data-ttu-id="5f2b7-113">업그레이드 되었으며 수정 응용 프로그램에 대 한을 하겠습니다 우리의 데이터베이스 디자인에 매우 밀접 하 게 해당 하 고 일부 사용자 지정 유효성 검사 논리와 비즈니스 규칙을 추가 하는 간단한 모델을 만들려면 LINQ to SQL 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-113">For our NerdDinner application we are going to use LINQ to SQL to create a simple model that corresponds fairly closely to our database design, and adds some custom validation logic and business rules.</span></span> <span data-ttu-id="5f2b7-114">추상 자리를 비울 도움이 되는 저장소 클래스 구현 다음 합니다 응용 프로그램 및 테스트 쉽게 단위를 사용 하 여 나머지 데이터 지 속성 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-114">We will then implement a repository class that helps abstract away the data persistence implementation from the rest of the application, and enables us to easily unit test it.</span></span>

### <a name="linq-to-sql"></a><span data-ttu-id="5f2b7-115">LINQ to SQL</span><span class="sxs-lookup"><span data-stu-id="5f2b7-115">LINQ to SQL</span></span>

<span data-ttu-id="5f2b7-116">LINQ to SQL은.NET 3.5의 일부로 제공 되는 ORM (개체 관계형 매퍼).</span><span class="sxs-lookup"><span data-stu-id="5f2b7-116">LINQ to SQL is an ORM (object relational mapper) that ships as part of .NET 3.5.</span></span>

<span data-ttu-id="5f2b7-117">LINQ to SQL 쉽게.NET 클래스에 대 한 코드를 작성할 수 있습니다에 데이터베이스 테이블을 매핑할 수 있는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-117">LINQ to SQL provides an easy way to map database tables to .NET classes we can code against.</span></span> <span data-ttu-id="5f2b7-118">업그레이드 되었으며 수정 응용 프로그램에 대 한 때 사용 해야 Dinners 및 RSVP 테이블 Dinner 및 RSVP 클래스에는 데이터베이스 내에서 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-118">For our NerdDinner application we'll use it to map the Dinners and RSVP tables within our database to Dinner and RSVP classes.</span></span> <span data-ttu-id="5f2b7-119">Dinners 및 RSVP 테이블의 열 Dinner 및 RSVP 클래스에서 속성에 해당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-119">The columns of the Dinners and RSVP tables will correspond to properties on the Dinner and RSVP classes.</span></span> <span data-ttu-id="5f2b7-120">각 Dinner 및 RSVP 개체는 데이터베이스의 Dinners 또는 RSVP 테이블 내에서 별도 행을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-120">Each Dinner and RSVP object will represent a separate row within the Dinners or RSVP tables in the database.</span></span>

<span data-ttu-id="5f2b7-121">LINQ to SQL SQL 문을 검색 하 고 Dinner 및 RSVP 업데이트를 수동으로 생성할 필요가 없도록 하는 데 사용할 수 있으며 데이터베이스 데이터를 사용 하 여 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-121">LINQ to SQL allows us to avoid having to manually construct SQL statements to retrieve and update Dinner and RSVP objects with database data.</span></span> <span data-ttu-id="5f2b7-122">대신, 매핑되는 방식을/데이터베이스 및 이들 간의 관계에서 Dinner 및 RSVP 클래스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-122">Instead, we'll define the Dinner and RSVP classes, how they map to/from the database, and the relationships between them.</span></span> <span data-ttu-id="5f2b7-123">LINQ to SQL은 상호 작용 하 고 사용 하는 경우 런타임에 사용할 적절 한 SQL 실행 논리를 생성 한 주의 ´ ù.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-123">LINQ to SQL will then takes care of generating the appropriate SQL execution logic to use at runtime when we interact and use them.</span></span>

<span data-ttu-id="5f2b7-124">VB 및 C#에서 LINQ 언어 지원 Dinner 및 RSVP를 검색 하는 표현 쿼리 작성에 사용할 수는 데이터베이스에서 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-124">We can use the LINQ language support within VB and C# to write expressive queries that retrieve Dinner and RSVP objects from the database.</span></span> <span data-ttu-id="5f2b7-125">이 최소화 되는 데이터는 코드를 작성 하려면 정리 실제로 응용 프로그램을 빌드할 수 있도록 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-125">This minimizes the amount of data code we need to write, and allows us to build really clean applications.</span></span>

### <a name="adding-linq-to-sql-classes-to-our-project"></a><span data-ttu-id="5f2b7-126">이 프로젝트에 LINQ to SQL 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="5f2b7-126">Adding LINQ to SQL Classes to our project</span></span>

<span data-ttu-id="5f2b7-127">이 프로젝트 내에서 "모델" 폴더를 마우스 오른쪽 단추로 클릭 하 여 시작 알아보고 선택 하겠습니다는 **추가-&gt;새 항목** 메뉴 명령:</span><span class="sxs-lookup"><span data-stu-id="5f2b7-127">We'll begin by right-clicking on the "Models" folder within our project, and select the **Add-&gt;New Item** menu command:</span></span>

![](build-a-model-with-business-rule-validations/_static/image1.png)

<span data-ttu-id="5f2b7-128">이 "새 항목 추가" 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-128">This will bring up the "Add New Item" dialog.</span></span> <span data-ttu-id="5f2b7-129">"데이터" 범주별으로 필터링 알아보고 내에서 "SQL 클래스를 LINQ" 템플릿을 선택 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-129">We'll filter by the "Data" category and select the "LINQ to SQL Classes" template within it:</span></span>

![](build-a-model-with-business-rule-validations/_static/image2.png)

<span data-ttu-id="5f2b7-130">"업그레이드 되었으며 수정" 항목 이름을 알아보고 "추가" 단추를 클릭 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-130">We'll name the item "NerdDinner" and click the "Add" button.</span></span> <span data-ttu-id="5f2b7-131">Visual Studio 우리의 \Models 디렉터리는 NerdDinner.dbml 파일이 추가 되 고 LINQ to SQL 개체 관계형 디자이너를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-131">Visual Studio will add a NerdDinner.dbml file under our \Models directory, and then open the LINQ to SQL object relational designer:</span></span>

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a><span data-ttu-id="5f2b7-132">Linq to SQL 데이터 모델 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="5f2b7-132">Creating Data Model Classes with LINQ to SQL</span></span>

<span data-ttu-id="5f2b7-133">LINQ to SQL 사용 하면 기존 데이터베이스 스키마에서 데이터 모델 클래스를 빠르게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-133">LINQ to SQL enables us to quickly create data model classes from existing database schema.</span></span> <span data-ttu-id="5f2b7-134">할 일에 모델링 하려는이 म 합니다 업그레이드 되었으며 수정 데이터베이스 서버 탐색기에서 열고 테이블 선택:</span><span class="sxs-lookup"><span data-stu-id="5f2b7-134">To-do this we'll open the NerdDinner database in the Server Explorer, and select the Tables we want to model in it:</span></span>

![](build-a-model-with-business-rule-validations/_static/image4.png)

<span data-ttu-id="5f2b7-135">테이블 LINQ로 SQL 디자이너 화면 끌어 놓을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-135">We can then drag the tables onto the LINQ to SQL designer surface.</span></span> <span data-ttu-id="5f2b7-136">이 LINQ to SQL 수행 하는 경우 Dinner 자동으로 만들어집니다 (데이터베이스 테이블 열에 매핑되는 클래스 속성)을 가진 테이블의 스키마를 사용 하 여 RSVP 클래스 및:</span><span class="sxs-lookup"><span data-stu-id="5f2b7-136">When we do this LINQ to SQL will automatically create Dinner and RSVP classes using the schema of the tables (with class properties that map to the database table columns):</span></span>

![](build-a-model-with-business-rule-validations/_static/image5.png)

<span data-ttu-id="5f2b7-137">LINQ to SQL 기본적으로 디자이너 자동으로 "복수로 바꿀지" 테이블 및 열 이름을 데이터베이스 스키마를 기반으로 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-137">By default the LINQ to SQL designer automatically "pluralizes" table and column names when it creates classes based on a database schema.</span></span> <span data-ttu-id="5f2b7-138">예: 위의 예에는 "Dinners" 테이블 "Dinner" 클래스에서 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-138">For example: the "Dinners" table in our example above resulted in a "Dinner" class.</span></span> <span data-ttu-id="5f2b7-139">이와 같은 클래스 이름을 통해 우리의 모델은.NET 명명 규칙과 일치 하 게 일반적으로 해당 디자이너의 수정이 반영 행이 있으면를 편리 하 게 특히 추가할 때 테이블의 많은 찾기.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-139">This class naming helps make our models consistent with .NET naming conventions, and I usually find that having the designer fix this up convenient (especially when adding lots of tables).</span></span> <span data-ttu-id="5f2b7-140">마음에 들지 않으면 클래스 또는 디자이너 생성 하지만 항상 재정의 하 고 원하는 이름으로 변경할 수 있는 속성의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-140">If you don't like the name of a class or property that the designer generates, though, you can always override it and change it to any name you want.</span></span> <span data-ttu-id="5f2b7-141">이렇게 하려면 두 줄을 편집 하는 엔터티/속성 이름에-디자이너 내에서 하거나 속성 표를 통해 수정 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-141">You can do this either by editing the entity/property name in-line within the designer or by modifying it via the property grid.</span></span>

<span data-ttu-id="5f2b7-142">LINQ to SQL 디자이너도 테이블의 기본 키/외래 키 관계를 검사 하 고 자동으로 그에 따라 기본적으로 기본을 만들므로 다른 모델 클래스 간에 "관계 연결" 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-142">By default the LINQ to SQL designer also inspects the primary key/foreign key relationships of the tables, and based on them automatically creates default "relationship associations" between the different model classes it creates.</span></span> <span data-ttu-id="5f2b7-143">RSVP 테이블 Dinners 테이블에 외래 키가 있다는 사실에 기반으로 때 우리는 Dinners 끌어서 RSVP 둘 사이 일 대 다 관계 연결을 LINQ to SQL 디자이너에 테이블 유추 된 예를 들어 (이에 화살표로 표시 됩니다는 디자이너):</span><span class="sxs-lookup"><span data-stu-id="5f2b7-143">For example, when we dragged the Dinners and RSVP tables onto the LINQ to SQL designer a one-to-many relationship association between the two was inferred based on the fact that the RSVP table had a foreign-key to the Dinners table (this is indicated by the arrow in the designer):</span></span>

![](build-a-model-with-business-rule-validations/_static/image6.png)

<span data-ttu-id="5f2b7-144">위의 연결 RSVP 클래스 개발자가 관련 된 주어진된 RSVP 저녁에 액세스 하는 데 사용할 수 있는 강력한 형식의 "Dinner" 속성을 추가 하려면 SQL LINQ 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-144">The above association will cause LINQ to SQL to add a strongly typed "Dinner" property to the RSVP class that developers can use to access the Dinner associated with a given RSVP.</span></span> <span data-ttu-id="5f2b7-145">개발자가 검색 하 고 특정 Dinner와 연결 된 RSVP 개체를 업데이트할 수 있는 "RSVPs" 컬렉션 속성이 있어야 Dinner 클래스도 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-145">It will also cause the Dinner class to have a "RSVPs" collection property that enables developers to retrieve and update RSVP objects associated with a particular Dinner.</span></span>

<span data-ttu-id="5f2b7-146">다음 새 RSVP 개체를 만든 하는 Dinner 않으십니까 컬렉션에 추가 하는 경우 Visual Studio 내에서 intellisense의 예를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-146">Below you can see an example of intellisense within Visual Studio when we create a new RSVP object and add it to a Dinner's RSVPs collection.</span></span> <span data-ttu-id="5f2b7-147">LINQ to SQL 자동으로 추가 하는 방법과 "않으십니까" 컬렉션 Dinner 개체에서 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-147">Notice how LINQ to SQL automatically added a "RSVPs" collection on the Dinner object:</span></span>

![](build-a-model-with-business-rule-validations/_static/image7.png)

<span data-ttu-id="5f2b7-148">RSVP 개체는 저녁 않으십니까 컬렉션에 추가 하 여 LINQ to SQL Dinner와 데이터베이스에 RSVP 행 간의 외래 키 관계를 연결할 한다는 म:</span><span class="sxs-lookup"><span data-stu-id="5f2b7-148">By adding the RSVP object to the Dinner's RSVPs collection we are telling LINQ to SQL to associate a foreign-key relationship between the Dinner and the RSVP row in our database:</span></span>

![](build-a-model-with-business-rule-validations/_static/image8.png)

<span data-ttu-id="5f2b7-149">어떻게 디자이너 모델링 했거나이 테이블 연결을 명명 된, 마음에 들지 않는 경우에이 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-149">If you don't like how the designer has modeled or named a table association, you can override it.</span></span> <span data-ttu-id="5f2b7-150">디자이너 내에서 연결 화살표를 클릭 하 고 이름 바꾸기, 삭제 또는 수정 하려면 속성 표를 통해 해당 속성에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-150">Just click on the association arrow within the designer and access its properties via the property grid to rename, delete or modify it.</span></span> <span data-ttu-id="5f2b7-151">이 업그레이드 되었으며 수정 응용 프로그램에 대 한 기본 연결 규칙을 작성 하는 데이터 모델 클래스에 대해 잘 작동 하지만 및 방금 기본 동작을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-151">For our NerdDinner application, though, the default association rules work well for the data model classes we are building and we can just use the default behavior.</span></span>

### <a name="nerddinnerdatacontext-class"></a><span data-ttu-id="5f2b7-152">NerdDinnerDataContext 클래스</span><span class="sxs-lookup"><span data-stu-id="5f2b7-152">NerdDinnerDataContext Class</span></span>

<span data-ttu-id="5f2b7-153">Visual Studio의 모델 및 LINQ to SQL 디자이너를 사용 하 여 정의 하는 데이터베이스 관계를 나타내는.NET 클래스를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-153">Visual Studio will automatically create .NET classes that represent the models and database relationships defined using the LINQ to SQL designer.</span></span> <span data-ttu-id="5f2b7-154">각 LINQ to SQL 디자이너 파일 솔루션에 추가 대 한 LINQ to SQL DataContext 클래스도 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-154">A LINQ to SQL DataContext class is also generated for each LINQ to SQL designer file added to the solution.</span></span> <span data-ttu-id="5f2b7-155">우리의 LINQ to SQL 클래스 항목 "업그레이드 되었으며 수정" 이라는 것 때문에 생성 된 DataContext 클래스 "NerdDinnerDataContext"가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-155">Because we named our LINQ to SQL class item "NerdDinner", the DataContext class created will be called "NerdDinnerDataContext".</span></span> <span data-ttu-id="5f2b7-156">이 NerdDinnerDataContext 클래스는 것이 데이터베이스와 상호 작용 하는 기본 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-156">This NerdDinnerDataContext class is the primary way we will interact with the database.</span></span>

<span data-ttu-id="5f2b7-157">NerdDinnerDataContext 클래스는 두 개의 속성-데이터베이스 내에서 모델링에서는 두 개의 테이블을 나타내는 "RSVPs-" 및 "Dinners"를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-157">Our NerdDinnerDataContext class exposes two properties - "Dinners" and "RSVPs" - that represent the two tables we modeled within the database.</span></span> <span data-ttu-id="5f2b7-158">사용 하 여 C# 데이터베이스에서 쿼리 및 검색 하 고 Dinner 및 RSVP 개체에 해당 속성에 대 한 LINQ 쿼리를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-158">We can use C# to write LINQ queries against those properties to query and retrieve Dinner and RSVP objects from the database.</span></span>

<span data-ttu-id="5f2b7-159">다음 코드 NerdDinnerDataContext 개체 인스턴스화를 나중에 발생 하는 Dinners의 시퀀스를 얻기 위해에 대해 LINQ 쿼리를 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-159">The following code demonstrates how to instantiate a NerdDinnerDataContext object and perform a LINQ query against it to obtain a sequence of Dinners that occur in the future.</span></span> <span data-ttu-id="5f2b7-160">LINQ 쿼리를 작성할 때 visual Studio는 전체 intellisense를 제공 하 고 여기에서 반환 된 개체 강력한 형식의 하며 intellisense 지원:</span><span class="sxs-lookup"><span data-stu-id="5f2b7-160">Visual Studio provides full intellisense when writing the LINQ query, and the objects returned from it are strongly-typed and also support intellisense:</span></span>

![](build-a-model-with-business-rule-validations/_static/image9.png)

<span data-ttu-id="5f2b7-161">허락해 Dinner 및 RSVP 개체를 쿼리 하는 것 외에도 NerdDinnerDataContext도 자동으로 변경에서는 이후에를 통해 검색 하는 Dinner 및 RSVP 개체를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-161">In addition to allowing us to query for Dinner and RSVP objects, a NerdDinnerDataContext also automatically tracks any changes we subsequently make to the Dinner and RSVP objects we retrieve through it.</span></span> <span data-ttu-id="5f2b7-162">데이터베이스에 다시-명시적 SQL 업데이트 코드를 작성할 필요 없이 변경 내용을 쉽게 저장할이 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-162">We can use this functionality to easily save the changes back to the database - without having to write any explicit SQL update code.</span></span>

<span data-ttu-id="5f2b7-163">예를 들어 아래 코드에는 데이터베이스에서 단일 Dinner 개체를 검색, 저녁 속성 중 두 업데이트 및 다음 변경 내용을 데이터베이스에 다시 저장 하는 LINQ 쿼리를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-163">For example, the code below demonstrates how to use a LINQ query to retrieve a single Dinner object from the database, update two of the Dinner properties, and then save the changes back to the database:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

<span data-ttu-id="5f2b7-164">위의 코드에 NerdDinnerDataContext 개체는 자동으로 Dinner 개체에서 검색 하는 것에 대 한 속성 변경 내용을 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-164">The NerdDinnerDataContext object in the code above automatically tracked the property changes made to the Dinner object we retrieved from it.</span></span> <span data-ttu-id="5f2b7-165">"SubmitChanges()" 메서드를 호출 하는 경우에 업데이트 된 값을 유지 하려면 데이터베이스에 적절 한 SQL "업데이트" 문을 실행 합니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-165">When we called the "SubmitChanges()" method, it will execute an appropriate SQL "UPDATE" statement to the database to persist the updated values back.</span></span>

### <a name="creating-a-dinnerrepository-class"></a><span data-ttu-id="5f2b7-166">DinnerRepository 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="5f2b7-166">Creating a DinnerRepository Class</span></span>

<span data-ttu-id="5f2b7-167">작은 응용 프로그램에 대 한 하는 것은 때로는 컨트롤러 LINQ to SQL DataContext 클래스에 대해 직접 작업 하 고 컨트롤러 내에서 LINQ 쿼리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-167">For small applications it is sometimes fine to have Controllers work directly against a LINQ to SQL DataContext class, and embed LINQ queries within the Controllers.</span></span> <span data-ttu-id="5f2b7-168">그러나 응용 프로그램은 더 큰 있게,이 방법은 유지 관리 및 테스트 하는 경우 다루기 집니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-168">As applications get larger, though, this approach becomes cumbersome to maintain and test.</span></span> <span data-ttu-id="5f2b7-169">여러 위치에서 동일한 LINQ 쿼리를 복제 합니다. 저희에 게 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-169">It can also lead to us duplicating the same LINQ queries in multiple places.</span></span>

<span data-ttu-id="5f2b7-170">응용 프로그램 유지 관리 및 테스트를 쉽게 만들 수 있는 한 가지 방법은 "repository" 패턴을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-170">One approach that can make applications easier to maintain and test is to use a "repository" pattern.</span></span> <span data-ttu-id="5f2b7-171">저장소 클래스는 데이터 쿼리 및 지 속성 논리와 떨어져 요약이 응용 프로그램에서 데이터 지 속성의 구현 정보를 캡슐화 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-171">A repository class helps encapsulate data querying and persistence logic, and abstracts away the implementation details of the data persistence from the application.</span></span> <span data-ttu-id="5f2b7-172">응용 프로그램 코드를 청소 하는 것 외에도 리포지토리 패턴을 사용 하 여 쉽게 만들 수를 데이터 저장소 구현을 나중에 변경 하 고 실제 데이터베이스를 요구 하지 않고 응용 프로그램을 테스트 하는 단위를 용이 하 게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-172">In addition to making application code cleaner, using a repository pattern can make it easier to change data storage implementations in the future, and it can help facilitate unit testing an application without requiring a real database.</span></span>

<span data-ttu-id="5f2b7-173">업그레이드 되었으며 수정 응용 프로그램에 대 한 사용 하 여 DinnerRepository 클래스 정의 하겠습니다는 아래 서명:</span><span class="sxs-lookup"><span data-stu-id="5f2b7-173">For our NerdDinner application we'll define a DinnerRepository class with the below signature:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

<span data-ttu-id="5f2b7-174">*참고:이 장의이 클래스 로부터 IDinnerRepository 인터페이스 추출 알아보고 하겠습니다 우리의 컨트롤러에 함께 종속성 주입을 사용 하도록 설정 합니다. 로 시작 하지만 하겠습니다 단순 시작한 DinnerRepository 클래스와 직접 작동 합니다.*</span><span class="sxs-lookup"><span data-stu-id="5f2b7-174">*Note: Later in this chapter we'll extract an IDinnerRepository interface from this class and enable dependency injection with it on our Controllers. To begin with, though, we are going to start simple and just work directly with the DinnerRepository class.*</span></span>

<span data-ttu-id="5f2b7-175">이 클래스는 "Models" 폴더를 마우스 오른쪽 단추로 클릭 알아보고 선택 하겠습니다를 구현 하는 **추가-&gt;새 항목** 메뉴 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-175">To implement this class we'll right-click on our "Models" folder and choose the **Add-&gt;New Item** menu command.</span></span> <span data-ttu-id="5f2b7-176">"새 항목 추가" 대화 상자 내에서 "클래스" 템플릿을 선택 하 고 "DinnerRepository.cs" 파일 이름을 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-176">Within the "Add New Item" dialog we'll select the "Class" template and name the file "DinnerRepository.cs":</span></span>

![](build-a-model-with-business-rule-validations/_static/image10.png)

<span data-ttu-id="5f2b7-177">아래 코드를 사용 하 여 DinnerRespository 클래스를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-177">We can then implement our DinnerRespository class using the code below:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a><span data-ttu-id="5f2b7-178">검색, 업데이트, 삽입 및 DinnerRepository 클래스를 사용 하 여 삭제</span><span class="sxs-lookup"><span data-stu-id="5f2b7-178">Retrieving, Updating, Inserting and Deleting using the DinnerRepository class</span></span>

<span data-ttu-id="5f2b7-179">DinnerRepository 클래스를 만든 했으므로 일반적인 작업에 수행할 수 있는 것을 보여 주는 몇 가지 코드 예제에서 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-179">Now that we've created our DinnerRepository class, let's look at a few code examples that demonstrate common tasks we can do with it:</span></span>

#### <a name="querying-examples"></a><span data-ttu-id="5f2b7-180">예제 쿼리</span><span class="sxs-lookup"><span data-stu-id="5f2b7-180">Querying Examples</span></span>

<span data-ttu-id="5f2b7-181">아래 코드 DinnerID 값을 사용 하 여 단일 Dinner를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-181">The code below retrieves a single Dinner using the DinnerID value:</span></span>


[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

<span data-ttu-id="5f2b7-182">아래 코드에 대해 모든 향후 dinners 및 루프를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-182">The code below retrieves all upcoming dinners and loops over them:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a><span data-ttu-id="5f2b7-183">삽입 및 업데이트 예제</span><span class="sxs-lookup"><span data-stu-id="5f2b7-183">Insert and Update Examples</span></span>

<span data-ttu-id="5f2b7-184">아래 코드는 두 개의 새 dinners 추가 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-184">The code below demonstrates adding two new dinners.</span></span> <span data-ttu-id="5f2b7-185">저장소에 추가/수정 사항에 "save" () 메서드를 호출할 때까지 데이터베이스에 커밋되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-185">Additions/modifications to the repository aren't committed to the database until the "Save()" method is called on it.</span></span> <span data-ttu-id="5f2b7-186">LINQ to SQL 자동 줄 바꿈되어 모든 변경 내용을 데이터베이스 트랜잭션에서 – 모든 변경이 발생 하거나 리포지토리의 저장할 때 수행 하는 사람은 하거나:</span><span class="sxs-lookup"><span data-stu-id="5f2b7-186">LINQ to SQL automatically wraps all changes in a database transaction – so either all changes happen or none of them do when our repository saves:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

<span data-ttu-id="5f2b7-187">아래 코드는 기존 Dinner 개체를 검색 하 고에 두 개의 속성을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-187">The code below retrieves an existing Dinner object, and modifies two properties on it.</span></span> <span data-ttu-id="5f2b7-188">이 저장소에서 "save" () 메서드를 호출할 때 변경이 다시 데이터베이스에 커밋된:</span><span class="sxs-lookup"><span data-stu-id="5f2b7-188">The changes are committed back to the database when the "Save()" method is called on our repository:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

<span data-ttu-id="5f2b7-189">아래 코드는 저녁을 검색 하 고는 RSVP를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-189">The code below retrieves a dinner and then adds an RSVP to it.</span></span> <span data-ttu-id="5f2b7-190">LINQ to SQL 만들어집니다 (있기 때문에 기본 키/외래 키 관계를 데이터베이스에서 둘 간의) 하는 Dinner 개체에서 않으십니까 컬렉션을 사용 하 여이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-190">It does this using the RSVPs collection on the Dinner object that LINQ to SQL created for us (because there is a primary-key/foreign-key relationship between the two in the database).</span></span> <span data-ttu-id="5f2b7-191">이 변경 내용은 저장소에서 "save" () 메서드를 호출할 때 다시 데이터베이스에 새 RSVP 테이블 행으로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-191">This change is persisted back to the database as a new RSVP table row when the "Save()" method is called on the repository:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a><span data-ttu-id="5f2b7-192">삭제 예제</span><span class="sxs-lookup"><span data-stu-id="5f2b7-192">Delete Example</span></span>

<span data-ttu-id="5f2b7-193">아래 코드는 기존 Dinner 개체를 검색 한 다음 삭제를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-193">The code below retrieves an existing Dinner object, and then marks it to be deleted.</span></span> <span data-ttu-id="5f2b7-194">저장소에서 "save" () 메서드를 호출할 때 주 복제본 데이터베이스에 다시 삭제를 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-194">When the "Save()" method is called on the repository it will commit the delete back to the database:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a><span data-ttu-id="5f2b7-195">유효성 검사 및 비즈니스 규칙 논리 모델 클래스를과 통합</span><span class="sxs-lookup"><span data-stu-id="5f2b7-195">Integrating Validation and Business Rule Logic with Model Classes</span></span>

<span data-ttu-id="5f2b7-196">유효성 검사 및 비즈니스 규칙은 데이터를 사용 하는 모든 응용 프로그램의 핵심이 라 할 논리를 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-196">Integrating validation and business rule logic is a key part of any application that works with data.</span></span>

#### <a name="schema-validation"></a><span data-ttu-id="5f2b7-197">스키마 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="5f2b7-197">Schema Validation</span></span>

<span data-ttu-id="5f2b7-198">LINQ to SQL 디자이너를 사용 하 여 모델 클래스 정의 되 면 데이터 모델 클래스에서 속성의 데이터 형식이 데이터베이스 테이블의 데이터 형식에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-198">When model classes are defined using the LINQ to SQL designer, the datatypes of the properties in the data model classes correspond to the datatypes of the database table.</span></span> <span data-ttu-id="5f2b7-199">예: "datetime" Dinners 테이블에 있는 "EventDate" 열을 사용 하는 경우 LINQ to SQL에서 만든 데이터 모델 클래스 (즉, 기본 제공.NET 데이터 형식)는 "DateTime" 형식의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-199">For example: if the "EventDate" column in the Dinners table is a "datetime", the data model class created by LINQ to SQL will be of type "DateTime" (which is a built-in .NET datatype).</span></span> <span data-ttu-id="5f2b7-200">즉, 여기에 코드에서 정수 또는 부울 값을 할당 하려고 하면 런타임 시에 유효 하지 않은 문자열 형식을 암시적으로 변환 하려고 하면 오류가 자동으로 발생 합니다 경우 컴파일 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-200">This means you will get compile errors if you attempt to assign an integer or boolean to it from code, and it will raise an error automatically if you attempt to implicitly convert a non-valid string type to it at runtime.</span></span>

<span data-ttu-id="5f2b7-201">사용자를 보호 SQL 삽입 공격을 사용할 문자열-를 사용 하는 경우 있습니다 LINQ to SQL 사용 하면 이스케이프 SQL 값도 자동으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-201">LINQ to SQL will also automatically handles escaping SQL values for you when using strings - which helps protect you against SQL injection attacks when using it.</span></span>

#### <a name="validation-and-business-rule-logic"></a><span data-ttu-id="5f2b7-202">유효성 검사 및 비즈니스 규칙 논리</span><span class="sxs-lookup"><span data-stu-id="5f2b7-202">Validation and Business Rule Logic</span></span>

<span data-ttu-id="5f2b7-203">스키마 유효성 검사는 첫 번째 단계로, 유용 하지만 거의 충분 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-203">Schema validation is useful as a first step, but is rarely sufficient.</span></span> <span data-ttu-id="5f2b7-204">대부분의 실제 시나리오 여러 속성에 걸쳐, 코드를 실행 하 고 모델의 상태에 대 한 인식을 경우가 수 있는 다양 한 유효성 검사 논리를 지정 하는 기능이 필요 (예: 것 만들어집니다/업데이트/삭제 되거나 도메인별 상태 내에서 마찬가지로 "보관").</span><span class="sxs-lookup"><span data-stu-id="5f2b7-204">Most real-world scenarios require the ability to specify richer validation logic that can span multiple properties, execute code, and often have awareness of a model's state (for example: is it being created /updated/deleted, or within a domain-specific state like "archived").</span></span> <span data-ttu-id="5f2b7-205">다양 한 다양 한 패턴 및 정의 하 고 모델 클래스에 유효성 검사 규칙을 적용 하는 데 사용할 수 있는 프레임 워크 되며 여러.NET 기반 프레임 워크 하셨습니까 이러한에 도움이 되는 데 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-205">There are a variety of different patterns and frameworks that can be used to define and apply validation rules to model classes, and there are several .NET based frameworks out there that can be used to help with this.</span></span> <span data-ttu-id="5f2b7-206">ASP.NET MVC 응용 프로그램 내에서 거의 모든를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-206">You can use pretty much any of them within ASP.NET MVC applications.</span></span>

<span data-ttu-id="5f2b7-207">업그레이드 되었으며 수정 응용 프로그램을 위해 사용 합니다는 비교적 간단 하 고 직관적인 패턴 우리의 Dinner 모델 개체에는 IsValid 속성과 GetRuleViolations() 메서드 공개 위치 지정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-207">For the purposes of our NerdDinner application, we'll use a relatively simple and straight-forward pattern where we expose an IsValid property and a GetRuleViolations() method on our Dinner model object.</span></span> <span data-ttu-id="5f2b7-208">IsValid 속성은 true 또는 false 유효성 검사 및 비즈니스 규칙은 모두 유효 여부에 따라 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-208">The IsValid property will return true or false depending on whether the validation and business rules are all valid.</span></span> <span data-ttu-id="5f2b7-209">GetRuleViolations() 메서드 목록이 규칙 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-209">The GetRuleViolations() method will return a list of any rule errors.</span></span>

<span data-ttu-id="5f2b7-210">프로젝트 진행에 "partial 클래스"를 추가 하 여 IsValid 및 GetRuleViolations() 예제의 Dinner 모델에 대 한 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-210">We'll implement IsValid and GetRuleViolations() for our Dinner model by adding a "partial class" to our project.</span></span> <span data-ttu-id="5f2b7-211">Partial 클래스 메서드/속성/이벤트 (예: LINQ to SQL 디자이너에 의해 생성 된 Dinner 클래스) VS 디자이너에서 유지 관리 하는 클래스를 추가 하려면 사용할 수 있으며에서 도구를 코드로 작업 하는 것을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-211">Partial classes can be used to add methods/properties/events to classes maintained by a VS designer (like the Dinner class generated by the LINQ to SQL designer) and help avoid the tool from messing with our code.</span></span> <span data-ttu-id="5f2b7-212">म \Models 폴더를 마우스 오른쪽 단추로 클릭 하 여이 프로젝트에 새 partial 클래스를 추가할 수 있으며 "새 항목 추가" 메뉴 명령을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-212">We can add a new partial class to our project by right-clicking on the \Models folder, and then select the "Add New Item" menu command.</span></span> <span data-ttu-id="5f2b7-213">"새 항목 추가" 대화 상자 내에서 "클래스" 템플릿을 선택 하 고 Dinner.cs 이름을 다음 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-213">We can then choose the "Class" template within the "Add New Item" dialog and name it Dinner.cs.</span></span>

![](build-a-model-with-business-rule-validations/_static/image11.png)

<span data-ttu-id="5f2b7-214">"추가" 단추를 클릭 하면이 프로젝트에 Dinner.cs 파일을 추가 하 고 IDE 내에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-214">Clicking the "Add" button will add a Dinner.cs file to our project and open it within the IDE.</span></span> <span data-ttu-id="5f2b7-215">사용 하 여 기본 규칙/유효성 검사 적용 프레임 워크를 구현할 수 있습니다는 아래 코드:</span><span class="sxs-lookup"><span data-stu-id="5f2b7-215">We can then implement a basic rule/validation enforcement framework using the below code:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

<span data-ttu-id="5f2b7-216">위의 코드에 대 한 참고 사항:</span><span class="sxs-lookup"><span data-stu-id="5f2b7-216">A few notes about the above code:</span></span>

- <span data-ttu-id="5f2b7-217">저녁 클래스 앞 키워드로 "부분" – 즉, 그 안에 포함 된 코드는 LINQ to SQL 디자이너에서 생성/유지 하는 클래스와 결합 되며 하나의 클래스로 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-217">The Dinner class is prefaced with a "partial" keyword – which means the code contained within it will be combined with the class generated/maintained by the LINQ to SQL designer and compiled into a single class.</span></span>
- <span data-ttu-id="5f2b7-218">RuleViolation 클래스가 통해 규칙 위반에 대 한 자세한 정보를 제공 하는 프로젝트에 추가 하는 도우미 클래스가입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-218">The RuleViolation class is a helper class we'll add to the project that allows us to provide more details about a rule violation.</span></span>
- <span data-ttu-id="5f2b7-219">Dinner.GetRuleViolations() 메서드를 유효성 검사 및 비즈니스 규칙 평가를 사용 하면 (구현에 곧).</span><span class="sxs-lookup"><span data-stu-id="5f2b7-219">The Dinner.GetRuleViolations() method causes our validation and business rules to be evaluated (we'll implement them shortly).</span></span> <span data-ttu-id="5f2b7-220">그런 다음 반환 다시는 RuleViolation는 개체 시퀀스의 모든 규칙 오류에 대 한 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-220">It then returns back a sequence of RuleViolation objects that provide more details about any rule errors.</span></span>
- <span data-ttu-id="5f2b7-221">Dinner.IsValid 속성 Dinner 개체 모든 활성 RuleViolations에 있는지 여부를 나타내는 편리한 도우미 속성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-221">The Dinner.IsValid property provides a convenient helper property that indicates whether the Dinner object has any active RuleViolations.</span></span> <span data-ttu-id="5f2b7-222">저녁 개체를 사용 하 여 언제 든 지 개발자가 적극적으로 확인할 수 있습니다 (하 고 예외가 발생 하지 않습니다).</span><span class="sxs-lookup"><span data-stu-id="5f2b7-222">It can be proactively checked by a developer using the Dinner object at anytime (and does not raise an exception).</span></span>
- <span data-ttu-id="5f2b7-223">Dinner.OnValidate() 부분 메서드를 Dinner 개체를 데이터베이스 내에서 유지 하려고 합니다. 언제 든 지 알림을 받을 수 있는 LINQ to SQL에서 제공 하는 후크 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-223">The Dinner.OnValidate() partial method is a hook that LINQ to SQL provides that allows us to be notified anytime the Dinner object is about to be persisted within the database.</span></span> <span data-ttu-id="5f2b7-224">위의 OnValidate() 구현 사용 하면 Dinner에 없는 RuleViolations 저장 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-224">Our OnValidate() implementation above ensures that the Dinner has no RuleViolations before it is saved.</span></span> <span data-ttu-id="5f2b7-225">잘못 된 상태에 있으면 LINQ to SQL 트랜잭션을 중단 하 고에 발생할 수 있는 예외가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-225">If it is in an invalid state it raises an exception, which will cause LINQ to SQL to abort the transaction.</span></span>

<span data-ttu-id="5f2b7-226">이 방법은 유효성 검사 및 비즈니스 규칙에 통합할 수 있습니다 하는 간단한 프레임 워크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-226">This approach provides a simple framework that we can integrate validation and business rules into.</span></span> <span data-ttu-id="5f2b7-227">지금은 추가해보겠습니다는 아래 우리의 GetRuleViolations() 메서드에 규칙:</span><span class="sxs-lookup"><span data-stu-id="5f2b7-227">For now let's add the below rules to our GetRuleViolations() method:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

<span data-ttu-id="5f2b7-228">C#의 "return을 yield" 기능 모든 RuleViolations의 시퀀스를 반환 하를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-228">We are using the "yield return" feature of C# to return a sequence of any RuleViolations.</span></span> <span data-ttu-id="5f2b7-229">위의 첫 번째 6 개의 규칙 검사는 단순히 null 또는 빈 문자열 속성 우리의 저녁에 일 수 없습니다 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-229">The first six rule checks above simply enforce that string properties on our Dinner cannot be null or empty.</span></span> <span data-ttu-id="5f2b7-230">마지막 규칙 약간 더 흥미롭습니다 이며 호출을 추가할 수 있습니다 되었는지 확인 하는 프로젝트에는 ContactPhone PhoneValidator.IsValidNumber() 도우미 메서드 형식 일치 Dinner의 국가 번호.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-230">The last rule is a little more interesting, and calls a PhoneValidator.IsValidNumber() helper method that we can add to our project to verify that the ContactPhone number format matches the Dinner's country.</span></span>

<span data-ttu-id="5f2b7-231">사용할 수 있습니다. 이 전화 유효성 검사 지원을 구현 하기 NET의 정규식 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-231">We can use .NET's regular expression support to implement this phone validation support.</span></span> <span data-ttu-id="5f2b7-232">다음은 추가할 수 있는 간단한 PhoneValidator 구현을 국가별 Regex 패턴 검사를 추가할 수 있도록 하는 프로젝트에:</span><span class="sxs-lookup"><span data-stu-id="5f2b7-232">Below is a simple PhoneValidator implementation that we can add to our project that enables us to add country-specific Regex pattern checks:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a><span data-ttu-id="5f2b7-233">유효성 검사 및 비즈니스 논리 위반 처리</span><span class="sxs-lookup"><span data-stu-id="5f2b7-233">Handling Validation and Business Logic Violations</span></span>

<span data-ttu-id="5f2b7-234">위의 유효성 검사 및 비즈니스 규칙 코드 만들기 또는 업데이트는 저녁에 언제 든 지 추가한, 했으므로 유효성 검사 논리 규칙을 평가 하 고 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-234">Now that we've added the above validation and business rule code, any time we try to create or update a Dinner, our validation logic rules will be evaluated and enforced.</span></span>

<span data-ttu-id="5f2b7-235">개발자 사전 유효 Dinner 개체 인지를 확인 하려면 아래와 같은 코드는 모든 예외를 생성 하지 않고 그 안에 모든 위반의 목록을 검색 합니다. 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-235">Developers can write code like below to proactively determine if a Dinner object is valid, and retrieve a list of all violations in it without raising any exceptions:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

<span data-ttu-id="5f2b7-236">잘못 된 상태에는 저녁 저장 하려고 하면, save () 메서드는 DinnerRepository에서 호출할 때 예외가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-236">If we attempt to save a Dinner in an invalid state, an exception will be raised when we call the Save() method on the DinnerRepository.</span></span> <span data-ttu-id="5f2b7-237">이 메서드는 저녁 변경 내용을 저장 하 고 Dinner에 존재 하는 규칙 위반 하는 경우 예외가 발생 하도록 Dinner.OnValidate()에 코드를 추가 했습니다 자동으로 LINQ to SQL 우리의 Dinner.OnValidate() 부분 메서드 호출 하기 때문에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-237">This occurs because LINQ to SQL automatically calls our Dinner.OnValidate() partial method before it saves the Dinner's changes, and we added code to Dinner.OnValidate() to raise an exception if any rule violations exist in the Dinner.</span></span> <span data-ttu-id="5f2b7-238">이 예외를 catch 할 수 있으며 사후 문제를 해결 하려면 위반 목록에 검색 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-238">We can catch this exception and reactively retrieve a list of the violations to fix:</span></span>

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

<span data-ttu-id="5f2b7-239">이 유효성 검사 및 비즈니스 규칙은 우리의 모델 계층 내에서 및 UI 계층 내에서 아닌를 구현 되므로 적용 되며 응용 프로그램 내에서 모든 시나리오에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-239">Because our validation and business rules are implemented within our model layer, and not within the UI layer, they will be applied and used across all scenarios within our application.</span></span> <span data-ttu-id="5f2b7-240">에서는 나중에 또는 비즈니스 규칙 추가 작동 하는 Dinner 개체 해당을 인식 하는 모든 코드를 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-240">We can later change or add business rules and have all code that works with our Dinner objects honor them.</span></span>

<span data-ttu-id="5f2b7-241">를 한 곳에서 비즈니스 규칙을 변경할 수는 데 이러한 변경 내용은 응용 프로그램 및 UI 논리 전체 ripple 필요 없이 잘 작성 된 응용 프로그램과 것을 권장 하는 MVC 프레임 워크는 데 도움이 되는 이점이 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-241">Having the flexibility to change business rules in one place, without having these changes ripple throughout the application and UI logic, is a sign of a well-written application, and a benefit that an MVC framework helps encourage.</span></span>

### <a name="next-step"></a><span data-ttu-id="5f2b7-242">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5f2b7-242">Next Step</span></span>

<span data-ttu-id="5f2b7-243">사용 하 여 쿼리하고 데이터베이스를 업데이트 하는 모델을 접수 이제 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-243">We've now got a model that we can use to both query and update our database.</span></span>

<span data-ttu-id="5f2b7-244">이제 추가해보겠습니다 컨트롤러와 뷰 일부 프로젝트에 테이블 주위의 HTML UI 경험을 만드는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f2b7-244">Let's now add some controllers and views to the project that we can use to build an HTML UI experience around it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5f2b7-245">[이전](create-a-database.md)
> [다음](use-controllers-and-views-to-implement-a-listingdetails-ui.md)</span><span class="sxs-lookup"><span data-stu-id="5f2b7-245">[Previous](create-a-database.md)
[Next](use-controllers-and-views-to-implement-a-listingdetails-ui.md)</span></span>
