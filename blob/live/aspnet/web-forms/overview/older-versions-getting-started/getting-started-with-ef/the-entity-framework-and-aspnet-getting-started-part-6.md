---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-6
title: "먼저 Entity Framework 4.0 데이터베이스와 시작 및 ASP.NET 4 Web Forms-6 부 | Microsoft Docs"
author: tdykstra
description: "Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/03/2010
ms.topic: article
ms.assetid: 994a5496-c648-4830-b03c-55bb43f325d2
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-6
msc.type: authoredcontent
ms.openlocfilehash: 164c2002a119420555d2c7065c5a79a5f433a725
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-6"></a><span data-ttu-id="663ff-104">먼저 Entity Framework 4.0 데이터베이스와 시작 및 ASP.NET 4 Web Forms-6 부</span><span class="sxs-lookup"><span data-stu-id="663ff-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 6</span></span>
====================
<span data-ttu-id="663ff-105">으로 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="663ff-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="663ff-106">Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 4.0 및 Visual Studio 2010을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="663ff-107">자습서 시리즈에 대 한 정보를 참조 하세요. [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="663ff-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>


## <a name="implementing-table-per-hierarchy-inheritance"></a><span data-ttu-id="663ff-108">계층당 하나의 테이블 상속 구현</span><span class="sxs-lookup"><span data-stu-id="663ff-108">Implementing Table-per-Hierarchy Inheritance</span></span>

<span data-ttu-id="663ff-109">이전 자습서에서 사용한 관련된 데이터를 추가 하 고 관계를 삭제 하 고 기존 엔터티에 대 한 관계 수 있었던 새 엔터티를 추가 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-109">In the previous tutorial you worked with related data by adding and deleting relationships and by adding a new entity that had a relationship to an existing entity.</span></span> <span data-ttu-id="663ff-110">이 자습서에서는 데이터 모델에서 상속을 구현 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-110">This tutorial will show you how to implement inheritance in the data model.</span></span>

<span data-ttu-id="663ff-111">개체 지향 프로그래밍 관련된 클래스를 사용 하 여 쉽게 수행할 수 있도록 상속을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-111">In object-oriented programming, you can use inheritance to make it easier to work with related classes.</span></span> <span data-ttu-id="663ff-112">만들 수는 예를 들어 `Instructor` 및 `Student` 에서 파생 된 클래스는 `Person` 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-112">For example, you could create `Instructor` and `Student` classes that derive from a `Person` base class.</span></span> <span data-ttu-id="663ff-113">Entity Framework에서 동일한 종류의 엔터티 간에 상속 구조를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-113">You can create the same kinds of inheritance structures among entities in the Entity Framework.</span></span>

<span data-ttu-id="663ff-114">자습서의이 부분에서는 새 웹 페이지를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-114">In this part of the tutorial, you won't create any new web pages.</span></span> <span data-ttu-id="663ff-115">대신 엔터티 데이터 모델에 파생 된 추가 하 고 새 엔터티를 사용 하도록 기존 페이지를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-115">Instead, you'll add derived entities to the data model and modify existing pages to use the new entities.</span></span>

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a><span data-ttu-id="663ff-116">형식당 하나의 테이블 상속 및 계층 당 테이블</span><span class="sxs-lookup"><span data-stu-id="663ff-116">Table-per-Hierarchy versus Table-per-Type Inheritance</span></span>

<span data-ttu-id="663ff-117">데이터베이스는 여러 테이블에서 하나 이상의 테이블이 나 관련된 개체에 대 한 정보를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-117">A database can store information about related objects in one table or in multiple tables.</span></span> <span data-ttu-id="663ff-118">예를 들어는 `School` 데이터베이스는 `Person` 학생과 단일 테이블에서 강사에 대 한 정보가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-118">For example, in the `School` database, the `Person` table includes information about both students and instructors in a single table.</span></span> <span data-ttu-id="663ff-119">강사에만 적용의 일부 열 (`HireDate`), 학생에만 일부 (`EnrollmentDate`), 둘 다에 일부 (`LastName`, `FirstName`).</span><span class="sxs-lookup"><span data-stu-id="663ff-119">Some of the columns apply only to instructors (`HireDate`), some only to students (`EnrollmentDate`), and some to both (`LastName`, `FirstName`).</span></span>

<span data-ttu-id="663ff-120">[![image11](the-entity-framework-and-aspnet-getting-started-part-6/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="663ff-120">[![image11](the-entity-framework-and-aspnet-getting-started-part-6/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image1.png)</span></span>

<span data-ttu-id="663ff-121">만들려는 Entity Framework를 구성할 수 있습니다 `Instructor` 및 `Student` 에서 상속 하는 엔터티는 `Person` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="663ff-121">You can configure the Entity Framework to create `Instructor` and `Student` entities that inherit from the `Person` entity.</span></span> <span data-ttu-id="663ff-122">이 패턴의 단일 데이터베이스 테이블에서 엔터티 상속 구조를 생성 하 라고 *테이블 계층당* TPH () 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-122">This pattern of generating an entity inheritance structure from a single database table is called *table-per-hierarchy* (TPH) inheritance.</span></span>

<span data-ttu-id="663ff-123">과정을에 대 한는 `School` 데이터베이스는 다른 패턴을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-123">For courses, the `School` database uses a different pattern.</span></span> <span data-ttu-id="663ff-124">온라인 강좌 및 온사이트 과정을 가리키는 외래 키가 각각 별도 테이블에 저장 됩니다는 `Course` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-124">Online courses and onsite courses are stored in separate tables, each of which has a foreign key that points to the `Course` table.</span></span> <span data-ttu-id="663ff-125">두 과정 유형 모두에 공통적인 정보에만 저장 됩니다는 `Course` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-125">Information common to both course types is stored only in the `Course` table.</span></span>

<span data-ttu-id="663ff-126">[![image12](the-entity-framework-and-aspnet-getting-started-part-6/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="663ff-126">[![image12](the-entity-framework-and-aspnet-getting-started-part-6/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image3.png)</span></span>

<span data-ttu-id="663ff-127">Entity Framework 데이터 모델을 구성할 수 있도록 `OnlineCourse` 및 `OnsiteCourse` 에서 상속 하는 엔터티는 `Course` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="663ff-127">You can configure the Entity Framework data model so that `OnlineCourse` and `OnsiteCourse` entities inherit from the `Course` entity.</span></span> <span data-ttu-id="663ff-128">이 패턴의 모든 형식에 공통 된 데이터를 저장 하는 테이블을 다시 가리키는 별도 각 테이블의 각 유형에 대해 별도 테이블에서 엔터티 상속 구조를 생성 하 라고 *형식당 하나의 테이블* (TPT) 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-128">This pattern of generating an entity inheritance structure from separate tables for each type, with each separate table referring back to a table that stores data common to all types, is called *table per type* (TPT) inheritance.</span></span>

<span data-ttu-id="663ff-129">TPH 상속 패턴 일반적으로 더 나은 성능을 제공 TPT 상속 패턴 보다 Entity Framework에서 TPT 패턴 복잡 한 조인 쿼리에서 발생할 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-129">TPH inheritance patterns generally deliver better performance in the Entity Framework than TPT inheritance patterns, because TPT patterns can result in complex join queries.</span></span> <span data-ttu-id="663ff-130">이 연습에서는 TPH 상속 구현 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-130">This walkthrough demonstrates how to implement TPH inheritance.</span></span> <span data-ttu-id="663ff-131">다음 단계를 수행 하 여 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-131">You'll do that by performing the following steps:</span></span>

- <span data-ttu-id="663ff-132">만들 `Instructor` 및 `Student` 엔터티 형식에서 파생 되는 `Person`합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-132">Create `Instructor` and `Student` entity types that derive from `Person`.</span></span>
- <span data-ttu-id="663ff-133">파생 된 엔터티에 관련 된 이동 속성은 `Person` 파생된 엔터티.</span><span class="sxs-lookup"><span data-stu-id="663ff-133">Move properties that pertain to the derived entities from the `Person` entity to the derived entities.</span></span>
- <span data-ttu-id="663ff-134">파생된 형식에서 속성에 대 한 제약 조건을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-134">Set constraints on properties in the derived types.</span></span>
- <span data-ttu-id="663ff-135">확인 된 `Person` 엔터티는 추상 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-135">Make the `Person` entity an abstract entity.</span></span>
- <span data-ttu-id="663ff-136">지도는 각 엔터티를 파생는 `Person` 확인 하는 방법을 지정 하는 조건 포함 된 테이블 여부는 `Person` 행 파생 형식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-136">Map each derived entity to the `Person` table with a condition that specifies how to determine whether a `Person` row represents that derived type.</span></span>

## <a name="adding-instructor-and-student-entities"></a><span data-ttu-id="663ff-137">강사 및 학생 엔터티 추가</span><span class="sxs-lookup"><span data-stu-id="663ff-137">Adding Instructor and Student Entities</span></span>

<span data-ttu-id="663ff-138">열기는 *SchoolModel.edmx* 파일, 선택 디자이너에서 빈된 영역을 마우스 오른쪽 단추로 클릭 **추가**을 선택한 후 **엔터티***합니다.*</span><span class="sxs-lookup"><span data-stu-id="663ff-138">Open the *SchoolModel.edmx* file, right-click an unoccupied area in the designer, select **Add**, then select **Entity***.*</span></span>

<span data-ttu-id="663ff-139">[![image01](the-entity-framework-and-aspnet-getting-started-part-6/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="663ff-139">[![image01](the-entity-framework-and-aspnet-getting-started-part-6/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image5.png)</span></span>

<span data-ttu-id="663ff-140">에 **엔터티 추가** 대화 상자에서 엔터티 이름 `Instructor` 설정 하 고 해당 **기본 형식** 옵션을 `Person`합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-140">In the **Add Entity** dialog box, name the entity `Instructor` and set its **Base type** option to `Person`.</span></span>

<span data-ttu-id="663ff-141">[![image02](the-entity-framework-and-aspnet-getting-started-part-6/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="663ff-141">[![image02](the-entity-framework-and-aspnet-getting-started-part-6/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image7.png)</span></span>

<span data-ttu-id="663ff-142">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-142">Click **OK**.</span></span> <span data-ttu-id="663ff-143">디자이너에서 만듭니다는 `Instructor` 에서 파생 되는 엔터티는 `Person` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="663ff-143">The designer creates an `Instructor` entity that derives from the `Person` entity.</span></span> <span data-ttu-id="663ff-144">새 엔터티가 아직 없는 모든 속성.</span><span class="sxs-lookup"><span data-stu-id="663ff-144">The new entity does not yet have any properties.</span></span>

<span data-ttu-id="663ff-145">[![image03](the-entity-framework-and-aspnet-getting-started-part-6/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="663ff-145">[![image03](the-entity-framework-and-aspnet-getting-started-part-6/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image9.png)</span></span>

<span data-ttu-id="663ff-146">만드는 절차를 반복 하는 `Student` 또한에서 파생 된 엔터티 `Person`합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-146">Repeat the procedure to create a `Student` entity that also derives from `Person`.</span></span>

<span data-ttu-id="663ff-147">해당 속성을 이동 해야 하므로 강사가 고용 날짜는 `Person` 엔터티를는 `Instructor` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="663ff-147">Only instructors have hire dates, so you need to move that property from the `Person` entity to the `Instructor` entity.</span></span> <span data-ttu-id="663ff-148">에 `Person` 엔터티를 마우스 오른쪽 단추로 클릭는 `HireDate` 속성 **잘라내기**합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-148">In the `Person` entity, right-click the `HireDate` property and click **Cut**.</span></span> <span data-ttu-id="663ff-149">마우스 오른쪽 단추로 클릭 한 다음 **속성** 에 `Instructor` 엔터티와 클릭 **붙여넣기**합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-149">Then right-click **Properties** in the `Instructor` entity and click **Paste**.</span></span>

<span data-ttu-id="663ff-150">[![image04](the-entity-framework-and-aspnet-getting-started-part-6/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="663ff-150">[![image04](the-entity-framework-and-aspnet-getting-started-part-6/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image11.png)</span></span>

<span data-ttu-id="663ff-151">고용 날짜는 `Instructor` 엔터티는 null 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-151">The hire date of an `Instructor` entity cannot be null.</span></span> <span data-ttu-id="663ff-152">마우스 오른쪽 단추로 클릭는 `HireDate` 속성을 클릭 하 여 **속성**, 한 다음는 **속성** 창 변경 `Nullable` 를 `False`합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-152">Right-click the `HireDate` property, click **Properties**, and then in the **Properties** window change `Nullable` to `False`.</span></span>

<span data-ttu-id="663ff-153">[![image05](the-entity-framework-and-aspnet-getting-started-part-6/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="663ff-153">[![image05](the-entity-framework-and-aspnet-getting-started-part-6/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image13.png)</span></span>

<span data-ttu-id="663ff-154">이동 하는 절차를 반복 하는 `EnrollmentDate` 속성은 `Person` 엔터티를는 `Student` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="663ff-154">Repeat the procedure to move the `EnrollmentDate` property from the `Person` entity to the `Student` entity.</span></span> <span data-ttu-id="663ff-155">설정 하 고 있는지 확인 `Nullable` 를 `False` 에 대 한는 `EnrollmentDate` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-155">Make sure that you also set `Nullable` to `False` for the `EnrollmentDate` property.</span></span>

<span data-ttu-id="663ff-156">이제는 `Person` 엔터티에에 공통 된 속성만 `Instructor` 및 `Student` 엔터티 (외에도 탐색 속성을 이동 하지 않는), 엔터티 에서만 사용할 수 있습니다에 상속 구조를 기준 엔터티로 합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-156">Now that a `Person` entity has only the properties that are common to `Instructor` and `Student` entities (aside from navigation properties, which you're not moving), the entity can only be used as a base entity in the inheritance structure.</span></span> <span data-ttu-id="663ff-157">따라서 독립 엔터티로 처리 되지 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-157">Therefore, you need to ensure that it's never treated as an independent entity.</span></span> <span data-ttu-id="663ff-158">마우스 오른쪽 단추로 클릭는 `Person` 엔터티를 **속성**, 한 다음는 **속성** 의 값을 변경 하는 창 고 **추상** 속성을  **True 이면**합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-158">Right-click the `Person` entity, select **Properties**, and then in the **Properties** window change the value of the **Abstract** property to **True**.</span></span>

<span data-ttu-id="663ff-159">[![image06](the-entity-framework-and-aspnet-getting-started-part-6/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="663ff-159">[![image06](the-entity-framework-and-aspnet-getting-started-part-6/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image15.png)</span></span>

## <a name="mapping-instructor-and-student-entities-to-the-person-table"></a><span data-ttu-id="663ff-160">Person 테이블에 강사 및 학생 엔터티 매핑</span><span class="sxs-lookup"><span data-stu-id="663ff-160">Mapping Instructor and Student Entities to the Person Table</span></span>

<span data-ttu-id="663ff-161">이제 Entity Framework를 구별 하는 방법만 알리면 `Instructor` 및 `Student` 데이터베이스의 엔터티.</span><span class="sxs-lookup"><span data-stu-id="663ff-161">Now you need to tell the Entity Framework how to differentiate between `Instructor` and `Student` entities in the database.</span></span>

<span data-ttu-id="663ff-162">마우스 오른쪽 단추로 클릭는 `Instructor` 엔터티와 선택 **테이블 매핑**합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-162">Right-click the `Instructor` entity and select **Table Mapping**.</span></span> <span data-ttu-id="663ff-163">에 **매핑 정보** 창 클릭 **테이블 또는 뷰 추가** 선택 **사람**합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-163">In the **Mapping Details** window, click **Add a Table or View** and select **Person**.</span></span>

<span data-ttu-id="663ff-164">[![image07](the-entity-framework-and-aspnet-getting-started-part-6/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="663ff-164">[![image07](the-entity-framework-and-aspnet-getting-started-part-6/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image17.png)</span></span>

<span data-ttu-id="663ff-165">클릭 **조건을 추가**를 선택한 후 **HireDate**합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-165">Click **Add a Condition**, and then select **HireDate**.</span></span>

<span data-ttu-id="663ff-166">[![image09](the-entity-framework-and-aspnet-getting-started-part-6/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="663ff-166">[![image09](the-entity-framework-and-aspnet-getting-started-part-6/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image19.png)</span></span>

<span data-ttu-id="663ff-167">변경 **연산자** 를 **은** 및 **값 / 속성** 를 **Not Null**합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-167">Change **Operator** to **Is** and **Value / Property** to **Not Null**.</span></span>

<span data-ttu-id="663ff-168">[![image10](the-entity-framework-and-aspnet-getting-started-part-6/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="663ff-168">[![image10](the-entity-framework-and-aspnet-getting-started-part-6/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image21.png)</span></span>

<span data-ttu-id="663ff-169">에 대 한 절차를 반복 하는 `Students` 엔터티를이 엔터티에 매핑됩니다 지정 하는 `Person` 하면 테이블의 `EnrollmentDate` 열이 null입니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-169">Repeat the procedure for the `Students` entity, specifying that this entity maps to the `Person` table when the `EnrollmentDate` column is not null.</span></span> <span data-ttu-id="663ff-170">그런 다음 저장 하 고 데이터 모델을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-170">Then save and close the data model.</span></span>

<span data-ttu-id="663ff-171">새 엔터티 클래스를 만들고 디자이너에서 사용할 수 있도록 하기 위해 프로젝트를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="663ff-171">Build the project in order to create the new entities as classes and make them available in the designer.</span></span>

## <a name="using-the-instructor-and-student-entities"></a><span data-ttu-id="663ff-172">강사 및 학생 엔터티를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="663ff-172">Using the Instructor and Student Entities</span></span>

<span data-ttu-id="663ff-173">학생과 강사 데이터를 데이터 바인딩된 있습니다를 사용 하는 웹 페이지를 만들 때는 `Person` 엔터티 집합에 필터링 및는 `HireDate` 또는 `EnrollmentDate` 학생 또는 강사에 반환된 된 데이터를 제한 하는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-173">When you created the web pages that work with student and instructor data, you databound them to the `Person` entity set, and you filtered on the `HireDate` or `EnrollmentDate` property to restrict the returned data to students or instructors.</span></span> <span data-ttu-id="663ff-174">그러나 이제 바인딩하는 경우 각 데이터 소스 제어에는 `Person` 엔터티 집합만 지정할 수 있습니다 `Student` 또는 `Instructor` 엔터티 형식을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-174">However, now when you bind each data source control to the `Person` entity set, you can specify that only `Student` or `Instructor` entity types should be selected.</span></span> <span data-ttu-id="663ff-175">Entity Framework에서 강사 학생을 구분 하는 방법을 알기 때문에 `Person` 엔터티 집합을 제거할 수 있습니다는 `Where` 속성 설정 작업을 수행 하는 직접 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-175">Because the Entity Framework knows how to differentiate students and instructors in the `Person` entity set, you can remove the `Where` property settings you entered manually to do that.</span></span>

<span data-ttu-id="663ff-176">Visual Studio 디자이너에서 지정할 수 있습니다 하는 엔터티 유형는 `EntityDataSource` 컨트롤에서 선택 해야는 **EntityTypeFilter** 의 드롭다운 목록 상자는 `Configure Data Source` 마법사에서 다음 예제와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-176">In the Visual Studio Designer, you can specify the entity type that an `EntityDataSource` control should select in the **EntityTypeFilter** drop-down box of the `Configure Data Source` wizard, as shown in the following example.</span></span>

<span data-ttu-id="663ff-177">[![image13](the-entity-framework-and-aspnet-getting-started-part-6/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="663ff-177">[![image13](the-entity-framework-and-aspnet-getting-started-part-6/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image23.png)</span></span>

<span data-ttu-id="663ff-178">및에 **속성** 창을 제거할 수 없습니다 `Where` 더 이상 필요 없는, 다음 예제와 같이 절 값입니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-178">And in the **Properties** window you can remove `Where` clause values that are no longer needed, as shown in the following example.</span></span>

<span data-ttu-id="663ff-179">[![image14](the-entity-framework-and-aspnet-getting-started-part-6/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="663ff-179">[![image14](the-entity-framework-and-aspnet-getting-started-part-6/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image25.png)</span></span>

<span data-ttu-id="663ff-180">그러나에 대 한 태그를 변경한 후 때문에 `EntityDataSource` 사용할 수 있는 컨트롤의 `ContextTypeName` 특성을 실행할 수 없습니다.는 **데이터 소스 구성** 에서 마법사 `EntityDataSource` 이미 작성 하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-180">However, because you've changed the markup for `EntityDataSource` controls to use the `ContextTypeName` attribute, you cannot run the **Configure Data Source** wizard on `EntityDataSource` controls that you've already created.</span></span> <span data-ttu-id="663ff-181">따라서 대신 태그를 변경 하 여 필요한 변경 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-181">Therefore, you'll make the required changes by changing markup instead.</span></span>

<span data-ttu-id="663ff-182">열기는 *Students.aspx* 페이지.</span><span class="sxs-lookup"><span data-stu-id="663ff-182">Open the *Students.aspx* page.</span></span> <span data-ttu-id="663ff-183">에 `StudentsEntityDataSource` 컨트롤을 제거는 `Where` 특성을 추가 `EntityTypeFilter="Student"` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-183">In the `StudentsEntityDataSource` control, remove the `Where` attribute and add an `EntityTypeFilter="Student"` attribute.</span></span> <span data-ttu-id="663ff-184">이제 태그 다음 예와 비슷하게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-184">The markup will now resemble the following example:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample1.aspx)]

<span data-ttu-id="663ff-185">설정의 `EntityTypeFilter` 되도록 특성의 `EntityDataSource` 컨트롤에 지정 된 엔터티 형식에만 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-185">Setting the `EntityTypeFilter` attribute ensures that the `EntityDataSource` control will select only the specified entity type.</span></span> <span data-ttu-id="663ff-186">모두 검색 하려면 `Student` 및 `Instructor` 엔터티 형식에는 설정 하면이 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-186">If you wanted to retrieve both `Student` and `Instructor` entity types, you would not set this attribute.</span></span> <span data-ttu-id="663ff-187">(하나를 사용 하는 여러 엔터티 형식을 검색 하는 옵션이 제공 `EntityDataSource` 읽기 전용 데이터 액세스를 위한 컨트롤을 사용 하는 경우에 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-187">(You have the option of retrieving multiple entity types with one `EntityDataSource` control only if you're using the control for read-only data access.</span></span> <span data-ttu-id="663ff-188">사용 중인 경우는 `EntityDataSource` 컨트롤을 삽입, 업데이트 또는 엔터티를 삭제 하 고 엔터티 집합에 바인딩되어 여러 형식을 포함할 수 있으면 하나의 엔터티 형식에만 사용할 수 있습니다이 특성을 설정 해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="663ff-188">If you're using an `EntityDataSource` control to insert, update, or delete entities, and if the entity set it's bound to can contain multiple types, you can only work with one entity type, and you have to set this attribute.)</span></span>

<span data-ttu-id="663ff-189">에 대 한 절차를 반복 하는 `SearchEntityDataSource` 제거 부분에만 제외 하 고 제어는 `Where` 특성을 선택 하 `Student` 엔터티 속성을 모두 제거 하는 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-189">Repeat the procedure for the `SearchEntityDataSource` control, except remove only the part of the `Where` attribute that selects `Student` entities instead of removing the property altogether.</span></span> <span data-ttu-id="663ff-190">이제 컨트롤의 여는 태그 다음 예와 비슷하게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-190">The opening tag of the control will now resemble the following example:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample2.aspx)]

<span data-ttu-id="663ff-191">이전 동작을 확인 하려면 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-191">Run the page to verify that it still works as it did before.</span></span>

<span data-ttu-id="663ff-192">[![image15](the-entity-framework-and-aspnet-getting-started-part-6/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="663ff-192">[![image15](the-entity-framework-and-aspnet-getting-started-part-6/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image27.png)</span></span>

<span data-ttu-id="663ff-193">새 사용할 수 있도록 이전 자습서에서 만든 다음 페이지를 업데이트 `Student` 및 `Instructor` 엔터티 대신 `Person` 엔터티, 한 다음 실행 전과 마찬가지로 작동 하는지 확인 하려면:</span><span class="sxs-lookup"><span data-stu-id="663ff-193">Update the following pages that you created in earlier tutorials so that they use the new `Student` and `Instructor` entities instead of `Person` entities, then run them to verify that they work as they did before:</span></span>

- <span data-ttu-id="663ff-194">*StudentsAdd.aspx*, 추가 `EntityTypeFilter="Student"` 에 `StudentsEntityDataSource` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-194">In *StudentsAdd.aspx*, add `EntityTypeFilter="Student"` to the `StudentsEntityDataSource` control.</span></span> <span data-ttu-id="663ff-195">이제 태그 다음 예와 비슷하게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-195">The markup will now resemble the following example:</span></span> 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample3.aspx)]

    <span data-ttu-id="663ff-196">[![image16](the-entity-framework-and-aspnet-getting-started-part-6/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="663ff-196">[![image16](the-entity-framework-and-aspnet-getting-started-part-6/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image29.png)</span></span>
- <span data-ttu-id="663ff-197">*About.aspx*, 추가 `EntityTypeFilter="Student"` 에 `StudentStatisticsEntityDataSource` 제어 하 고 제거 `Where="it.EnrollmentDate is not null"`합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-197">In *About.aspx*, add `EntityTypeFilter="Student"` to the `StudentStatisticsEntityDataSource` control and remove `Where="it.EnrollmentDate is not null"`.</span></span> <span data-ttu-id="663ff-198">이제 태그 다음 예와 비슷하게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-198">The markup will now resemble the following example:</span></span> 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample4.aspx)]

    <span data-ttu-id="663ff-199">[![image17](the-entity-framework-and-aspnet-getting-started-part-6/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image31.png)</span><span class="sxs-lookup"><span data-stu-id="663ff-199">[![image17](the-entity-framework-and-aspnet-getting-started-part-6/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image31.png)</span></span>
- <span data-ttu-id="663ff-200">*Instructors.aspx* 및 *InstructorsCourses.aspx*, 추가 `EntityTypeFilter="Instructor"` 에 `InstructorsEntityDataSource` 제어 하 고 제거 `Where="it.HireDate is not null"`합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-200">In *Instructors.aspx* and *InstructorsCourses.aspx*, add `EntityTypeFilter="Instructor"` to the `InstructorsEntityDataSource` control and remove `Where="it.HireDate is not null"`.</span></span> <span data-ttu-id="663ff-201">에 있는 태그 *Instructors.aspx* 이제 다음 예제와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-201">The markup in *Instructors.aspx* now resembles the following example:</span></span> 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample5.aspx)]

    <span data-ttu-id="663ff-202">[![image18](the-entity-framework-and-aspnet-getting-started-part-6/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image33.png)</span><span class="sxs-lookup"><span data-stu-id="663ff-202">[![image18](the-entity-framework-and-aspnet-getting-started-part-6/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image33.png)</span></span>

    <span data-ttu-id="663ff-203">에 있는 태그 *InstructorsCourses.aspx* 는 이제 다음 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-203">The markup in *InstructorsCourses.aspx* will now resemble the following example:</span></span>

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample6.aspx)]

    <span data-ttu-id="663ff-204">[![image19](the-entity-framework-and-aspnet-getting-started-part-6/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image35.png)</span><span class="sxs-lookup"><span data-stu-id="663ff-204">[![image19](the-entity-framework-and-aspnet-getting-started-part-6/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image35.png)</span></span>

<span data-ttu-id="663ff-205">이러한 변경으로 인해 여러 가지 방법으로 Contoso 대학 응용 프로그램의 유지 관리를 개선 했습니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-205">As a result of these changes, you've improved the Contoso University application's maintainability in several ways.</span></span> <span data-ttu-id="663ff-206">선택 및 유효성 검사 논리 UI 계층 제외 이동한 (*.aspx* 태그) 및 데이터 액세스 계층의 필수적인 부분을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-206">You've moved selection and validation logic out of the UI layer (*.aspx* markup) and made it an integral part of the data access layer.</span></span> <span data-ttu-id="663ff-207">이렇게 하면 변경 된 내용 데이터베이스 스키마 나 데이터 모델을 나중에 하도록 할 수 있는 응용 프로그램 코드를 격리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-207">This helps to isolate your application code from changes that you might make in the future to the database schema or the data model.</span></span> <span data-ttu-id="663ff-208">예를 들어 학생 교사 보조 기능으로 고용 수 및 따라서 고용 날짜를 가져오는 것을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-208">For example, you could decide that students might be hired as teachers' aids and therefore would get a hire date.</span></span> <span data-ttu-id="663ff-209">다음에서 강사 학생을 구분 하 고 데이터 모델을 업데이트 하려면 새 속성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-209">You could then add a new property to differentiate students from instructors and update the data model.</span></span> <span data-ttu-id="663ff-210">웹 응용 프로그램에서 코드가 없는 학생용 고용 날짜를 표시 하려는 제외 하 고 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-210">No code in the web application would need to change except where you wanted to show a hire date for students.</span></span> <span data-ttu-id="663ff-211">추가 하는 또 다른 이점은 `Instructor` 및 `Student` 엔터티를 참조할 때 보다 더 쉽게 이해할 수 있는 코드 된다는 점입니다 `Person` 실제로 학생 했던 개체 또는 강사 합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-211">Another benefit of adding `Instructor` and `Student` entities is that your code is more readily understandable than when it referred to `Person` objects that were actually students or instructors.</span></span>

<span data-ttu-id="663ff-212">이제 Entity Framework에서 한 상속 패턴을 구현 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-212">You've now seen one way to implement an inheritance pattern in the Entity Framework.</span></span> <span data-ttu-id="663ff-213">다음 자습서에서는 Entity Framework 데이터베이스를 액세스 하는 방법을 보다 자세하게 제어 하기 위해 저장된 프로시저를 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="663ff-213">In the following tutorial, you'll learn how to use stored procedures in order to have more control over how the Entity Framework accesses the database.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="663ff-214">[이전](the-entity-framework-and-aspnet-getting-started-part-5.md)
[다음](the-entity-framework-and-aspnet-getting-started-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="663ff-214">[Previous](the-entity-framework-and-aspnet-getting-started-part-5.md)
[Next](the-entity-framework-and-aspnet-getting-started-part-7.md)</span></span>