---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: "(8 / 10) ASP.NET MVC 응용 프로그램에서 Entity Framework 사용한 상속 구현 | Microsoft Docs"
author: tdykstra
description: "Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 54e46c6f996b6fe86a227c851562e61678b02780
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a><span data-ttu-id="b3b2c-103">(8 / 10) ASP.NET MVC 응용 프로그램에서 Entity Framework 사용한 상속 구현</span><span class="sxs-lookup"><span data-stu-id="b3b2c-103">Implementing Inheritance with the Entity Framework in an ASP.NET MVC Application (8 of 10)</span></span>
====================
<span data-ttu-id="b3b2c-104">으로 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="b3b2c-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="b3b2c-105">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="b3b2c-106">Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio 2012를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="b3b2c-107">자습서 시리즈에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="b3b2c-108">시작 부분에서 자습서 시리즈를 시작할 수 있습니다 또는 [이 장의 대 한 시작 프로젝트 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 여기에서 시작 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="b3b2c-109">해결할 수 없는 문제에 직면 하는 경우 [완료 장 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 문제를 재현 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="b3b2c-110">일반적으로 코드 완성 된 코드를 비교 하 여 문제에 솔루션을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="b3b2c-111">몇 가지 일반적인 오류 및 해결 하는 방법에 대 한 참조 [오류 및 해결 방법입니다.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="b3b2c-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>


<span data-ttu-id="b3b2c-112">이전 자습서에서 동시성 예외를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-112">In the previous tutorial you handled concurrency exceptions.</span></span> <span data-ttu-id="b3b2c-113">이 자습서에서는 데이터 모델에서 상속을 구현 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-113">This tutorial will show you how to implement inheritance in the data model.</span></span>

<span data-ttu-id="b3b2c-114">개체 지향 프로그래밍에서 중복 코드를 제거할 상속을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-114">In object-oriented programming, you can use inheritance to eliminate redundant code.</span></span> <span data-ttu-id="b3b2c-115">이 자습서에서는 변경 된 `Instructor` 및 `Student` 에서 파생 되도록 클래스는 `Person` 기본 클래스와 같은 속성이 포함 된 `LastName` 강사 및 학생 데이터 모두에 공통적인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-115">In this tutorial, you'll change the `Instructor` and `Student` classes so that they derive from a `Person` base class which contains properties such as `LastName` that are common to both instructors and students.</span></span> <span data-ttu-id="b3b2c-116">추가 하거나 모든 웹 페이지를 변경 하지 않습니다 되지만 일부 코드를 변경 합니다 및 이러한 변경 내용을 데이터베이스에 자동으로 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-116">You won't add or change any web pages, but you'll change some of the code and those changes will be automatically reflected in the database.</span></span>

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a><span data-ttu-id="b3b2c-117">형식당 하나의 테이블 상속 및 계층 당 테이블</span><span class="sxs-lookup"><span data-stu-id="b3b2c-117">Table-per-Hierarchy versus Table-per-Type Inheritance</span></span>

<span data-ttu-id="b3b2c-118">개체 지향 프로그래밍 관련된 클래스를 사용 하 여 쉽게 수행할 수 있도록 상속을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-118">In object-oriented programming, you can use inheritance to make it easier to work with related classes.</span></span> <span data-ttu-id="b3b2c-119">예를 들어는 `Instructor` 및 `Student` 에 있는 클래스는 `School` 데이터 모델을 중복 코드 줄어들고 결과적 몇 가지 속성을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-119">For example, the `Instructor` and `Student` classes in the `School` data model share several properties, which results in redundant code:</span></span>

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

<span data-ttu-id="b3b2c-121">공유 하는 속성에 대 한 중복 코드를 제거 하려는 경우 다음과 같이 `Instructor` 및 `Student` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-121">Suppose you want to eliminate the redundant code for the properties that are shared by the `Instructor` and `Student` entities.</span></span> <span data-ttu-id="b3b2c-122">만들 수는 `Person` 확인 한 다음 기본 속성을 공유 하는 것만 포함 하는 클래스는 `Instructor` 및 `Student` 다음 그림에 나와 있는 것 처럼 해당 기본 클래스에서 상속 되는 엔터티:</span><span class="sxs-lookup"><span data-stu-id="b3b2c-122">You could create a `Person` base class which contains only those shared properties, then make the `Instructor` and `Student` entities inherit from that base class, as shown in the following illustration:</span></span>

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

<span data-ttu-id="b3b2c-124">여러 가지 방법으로 데이터베이스에이 상속 구조를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-124">There are several ways this inheritance structure could be represented in the database.</span></span> <span data-ttu-id="b3b2c-125">있을 수 있습니다는 `Person` 학생과 단일 테이블에서 강사에 대 한 정보를 포함 하는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-125">You could have a `Person` table that includes information about both students and instructors in a single table.</span></span> <span data-ttu-id="b3b2c-126">강사에만 적용할 수는 일부 열의 (`HireDate`), 학생에만 일부 (`EnrollmentDate`), 일부에 모두 (`LastName`, `FirstName`).</span><span class="sxs-lookup"><span data-stu-id="b3b2c-126">Some of the columns could apply only to instructors (`HireDate`), some only to students (`EnrollmentDate`), some to both (`LastName`, `FirstName`).</span></span> <span data-ttu-id="b3b2c-127">일반적으로, 한 *판별자* 는 형식을 각 행 표시 열을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-127">Typically, you'd have a *discriminator* column to indicate which type each row represents.</span></span> <span data-ttu-id="b3b2c-128">예를 들어 판별자 열 학생용 강사 및 "학생"에 대 한 "강사"를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-128">For example, the discriminator column might have "Instructor" for instructors and "Student" for students.</span></span>

![Hierarchy_example 당 테이블](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

<span data-ttu-id="b3b2c-130">이 패턴의 단일 데이터베이스 테이블에서 엔터티 상속 구조를 생성 하 라고 *테이블 계층당* TPH () 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-130">This pattern of generating an entity inheritance structure from a single database table is called *table-per-hierarchy* (TPH) inheritance.</span></span>

<span data-ttu-id="b3b2c-131">대신 좀 더 상속 구조 처럼 보이도록 하는 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-131">An alternative is to make the database look more like the inheritance structure.</span></span> <span data-ttu-id="b3b2c-132">예를 들어 이름 필드에만 있을 수 있습니다는 `Person` 테이블 있고 별도 `Instructor` 및 `Student` 날짜 필드가 있는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-132">For example, you could have only the name fields in the `Person` table and have separate `Instructor` and `Student` tables with the date fields.</span></span>

![Type_inheritance 당 테이블](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

<span data-ttu-id="b3b2c-134">이 패턴의 각 엔터티 클래스에 대 한 데이터베이스 테이블을 만드는 *형식당 하나의 테이블* (TPT) 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-134">This pattern of making a database table for each entity class is called *table per type* (TPT) inheritance.</span></span>

<span data-ttu-id="b3b2c-135">TPH 상속 패턴 일반적으로 더 나은 성능을 제공 TPT 상속 패턴 보다 Entity Framework에서 TPT 패턴 복잡 한 조인 쿼리에서 발생할 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-135">TPH inheritance patterns generally deliver better performance in the Entity Framework than TPT inheritance patterns, because TPT patterns can result in complex join queries.</span></span> <span data-ttu-id="b3b2c-136">이 자습서에서는 TPH 상속 구현 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-136">This tutorial demonstrates how to implement TPH inheritance.</span></span> <span data-ttu-id="b3b2c-137">다음 단계를 수행 하 여 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-137">You'll do that by performing the following steps:</span></span>

- <span data-ttu-id="b3b2c-138">만들기는 `Person` 클래스 및 변경 된 `Instructor` 및 `Student` 클래스에서 상속할 수 `Person`합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-138">Create a `Person` class and change the `Instructor` and `Student` classes to derive from `Person`.</span></span>
- <span data-ttu-id="b3b2c-139">데이터베이스 컨텍스트 클래스를 데이터베이스에 모델 매핑 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-139">Add model-to-database mapping code to the database context class.</span></span>
- <span data-ttu-id="b3b2c-140">변경 `InstructorID` 및 `StudentID` 참조를 프로젝트 전반에 걸쳐 `PersonID`합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-140">Change `InstructorID` and `StudentID` references throughout the project to `PersonID`.</span></span>

## <a name="creating-the-person-class"></a><span data-ttu-id="b3b2c-141">사용자 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="b3b2c-141">Creating the Person Class</span></span>

 <span data-ttu-id="b3b2c-142">참고: 있습니다 할 수 없습니다 이러한 클래스를 사용 하는 컨트롤러를 업데이트할 때까지 아래 클래스를 만든 후 프로젝트를 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-142">Note: You won't be able to compile the project after creating the classes below until you update the controllers that uses these classes.</span></span> 

<span data-ttu-id="b3b2c-143">에 *모델* 폴더를 만들 *Person.cs* 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-143">In the *Models* folder, create *Person.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="b3b2c-144">*Instructor.cs*, 파생 된 `Instructor` 에서 클래스는 `Person` 클래스 및 키 / 이름 필드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-144">In *Instructor.cs*, derive the `Instructor` class from the `Person` class and remove the key and name fields.</span></span> <span data-ttu-id="b3b2c-145">코드는 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-145">The code will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="b3b2c-146">비슷한 변경 *Student.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-146">Make similar changes to *Student.cs*.</span></span> <span data-ttu-id="b3b2c-147">`Student` 클래스는 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-147">The `Student` class will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a><span data-ttu-id="b3b2c-148">Person 엔터티 형식을 모델에 추가</span><span class="sxs-lookup"><span data-stu-id="b3b2c-148">Adding the Person Entity Type to the Model</span></span>

<span data-ttu-id="b3b2c-149">*SchoolContext.cs*, 추가 `DbSet` 속성에 대 한는 `Person` 엔터티 형식:</span><span class="sxs-lookup"><span data-stu-id="b3b2c-149">In *SchoolContext.cs*, add a `DbSet` property for the `Person` entity type:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="b3b2c-150">Entity Framework 계층당 하나의 테이블 상속을 구성 하는 데 필요한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-150">This is all that the Entity Framework needs in order to configure table-per-hierarchy inheritance.</span></span> <span data-ttu-id="b3b2c-151">하겠지만, 데이터베이스를 다시 생성 하는 경우는 `Person` 대신 테이블는 `Student` 및 `Instructor` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-151">As you'll see, when the database is re-created, it will have a `Person` table in place of the `Student` and `Instructor` tables.</span></span>

## <a name="changing-instructorid-and-studentid-to-personid"></a><span data-ttu-id="b3b2c-152">InstructorID StudentID PersonID로 변경</span><span class="sxs-lookup"><span data-stu-id="b3b2c-152">Changing InstructorID and StudentID to PersonID</span></span>

<span data-ttu-id="b3b2c-153">*SchoolContext.cs*, 강사 과정 매핑 문에서 변경 `MapRightKey("InstructorID")` 를 `MapRightKey("PersonID")`:</span><span class="sxs-lookup"><span data-stu-id="b3b2c-153">In *SchoolContext.cs*, in the Instructor-Course mapping statement, change `MapRightKey("InstructorID")` to `MapRightKey("PersonID")`:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

<span data-ttu-id="b3b2c-154">이러한 변경에는; 필요 하지 않습니다. 방금 다 대 다 조인 테이블에 InstructorID 열의 이름을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-154">This change isn't required; it just changes the name of the InstructorID column in the many-to-many join table.</span></span> <span data-ttu-id="b3b2c-155">이름으로 InstructorID 었으 면 응용 프로그램은 제대로 작동 여전히.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-155">If you left the name as InstructorID, the application would still work correctly.</span></span> <span data-ttu-id="b3b2c-156">여기에 완성 된 *SchoolContext.cs*:</span><span class="sxs-lookup"><span data-stu-id="b3b2c-156">Here is the completed *SchoolContext.cs*:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

<span data-ttu-id="b3b2c-157">변경 해야 다음 `InstructorID` 를 `PersonID` 및 `StudentID` 를 `PersonID` 프로젝트 전반에 걸쳐 ***제외 하 고*** 의 타임 스탬프 마이그레이션 파일에는 *마이그레이션* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-157">Next you need to change `InstructorID` to `PersonID` and `StudentID` to `PersonID` throughout the project ***except*** in the time-stamped migrations files in the *Migrations* folder.</span></span> <span data-ttu-id="b3b2c-158">그렇게 하려면 찾 및 열고 변경 해야 할 파일만 다음 열린된 파일에서 전역 변경 수행 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-158">To do that you'll find and open only the files that need to be changed, then perform a global change on the opened files.</span></span> <span data-ttu-id="b3b2c-159">유일한 파일은 *마이그레이션* 변경 해야 하는 폴더는 *Migrations\Configuration.cs 합니다.*</span><span class="sxs-lookup"><span data-stu-id="b3b2c-159">The only file in the *Migrations* folder you should change is *Migrations\Configuration.cs.*</span></span>

1. > [!IMPORTANT]
 > <span data-ttu-id="b3b2c-160">Visual Studio에서 열려 있는 모든 파일을 닫고 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-160">Begin by closing all the open files in Visual Studio.</span></span>
2. <span data-ttu-id="b3b2c-161">클릭 **찾기 및 바꾸기 등의 모든 파일을 찾으려면** 에 **편집** 메뉴 및 포함 된 프로젝트의 모든 파일에 대 한 다음 검색 `InstructorID`합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-161">Click **Find and Replace -- Find all Files** in the **Edit** menu, and then search for all files in the project that contain `InstructorID`.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. <span data-ttu-id="b3b2c-162">각 파일을 열고는 **찾기 결과** 창 ***제외 하 고*** 는 &lt;타임 스탬프&gt;*\_.cs* 는 에서마이그레이션파일*마이그레이션* 폴더 각 파일에 대 한 줄을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-162">Open each file in the **Find Results** window ***except*** the &lt;time-stamp&gt;*\_.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. <span data-ttu-id="b3b2c-163">열기는 **파일에서 바꾸기** 대화 상자와 변경 **찾는 위치** 를 **열려 있는 모든 문서**합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-163">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
5. <span data-ttu-id="b3b2c-164">사용 하 여는 **파일에서 바꾸기** 모든 변경 하려면 대화 `InstructorID` 를`PersonID.`</span><span class="sxs-lookup"><span data-stu-id="b3b2c-164">Use the **Replace in Files** dialog to change all `InstructorID` to `PersonID.`</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. <span data-ttu-id="b3b2c-165">포함 된 프로젝트의 모든 파일을 찾을 `StudentID`합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-165">Find all the files in the project that contain `StudentID`.</span></span>
7. <span data-ttu-id="b3b2c-166">각 파일을 열고는 **찾기 결과** 창 ***제외 하 고*** 는 &lt;타임 스탬프&gt;*\_\*.cs* 마이그레이션 파일 에 *마이그레이션* 폴더 각 파일에 대 한 줄을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-166">Open each file in the **Find Results** window ***except*** the &lt;time-stamp&gt;*\_\*.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. <span data-ttu-id="b3b2c-167">열기는 **파일에서 바꾸기** 대화 상자와 변경 **찾는 위치** 를 **열려 있는 모든 문서**합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-167">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
9. <span data-ttu-id="b3b2c-168">사용 하 여는 **파일에서 바꾸기** 모든 변경 하려면 대화 `StudentID` 를 `PersonID`합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-168">Use the **Replace in Files** dialog to change all `StudentID` to `PersonID`.</span></span>   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. <span data-ttu-id="b3b2c-169">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-169">Build the project.</span></span>

<span data-ttu-id="b3b2c-170">(이 보이는 참고는 *단점은* 의 `classnameID` 패턴의 기본 키 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-170">(Note that this demonstrates a *disadvantage* of the `classnameID` pattern for naming primary keys.</span></span> <span data-ttu-id="b3b2c-171">기본 키 ID 클래스 이름에 접두사를 추가 하지 않고 명명 된 *없습니다* 이름 바꾸기을 수행 해야 이제.)</span><span class="sxs-lookup"><span data-stu-id="b3b2c-171">If you had named primary keys ID without prefixing the class name, *no* renaming would be necessary now.)</span></span>

## <a name="create-and-update-a-migrations-file"></a><span data-ttu-id="b3b2c-172">만들기 및 마이그레이션 파일 업데이트</span><span class="sxs-lookup"><span data-stu-id="b3b2c-172">Create and Update a Migrations File</span></span>

<span data-ttu-id="b3b2c-173">패키지 관리자 콘솔 (PMC)에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-173">In the Package Manager Console (PMC), enter the following command:</span></span>

`Add-Migration Inheritance`

<span data-ttu-id="b3b2c-174">실행 된 `Update-Database` 의 PMC 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-174">Run the `Update-Database` command in the PMC.</span></span> <span data-ttu-id="b3b2c-175">기존 데이터 마이그레이션 처리 하는 방법을 모릅니다를 지정 했으므로 시점에서 명령이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-175">The command will fail at this point because we have existing data that migrations doesn't know how to handle.</span></span> <span data-ttu-id="b3b2c-176">다음과 같은 오류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-176">You get the following error:</span></span>

<span data-ttu-id="b3b2c-177">*ALTER TABLE 문을 FOREIGN KEY 제약 조건 충돌 "FK\_dbo입니다. 부서\_dbo입니다. 사람\_PersonID "입니다. 데이터베이스 "ContosoUniversity" 테이블 "dbo에에서 충돌이 발생 했습니다. 사용자 ", 열 'PersonID'입니다.*</span><span class="sxs-lookup"><span data-stu-id="b3b2c-177">*The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK\_dbo.Department\_dbo.Person\_PersonID". The conflict occurred in database "ContosoUniversity", table "dbo.Person", column 'PersonID'.*</span></span>

<span data-ttu-id="b3b2c-178">열기 *마이그레이션\&lt; 타임 스탬프&gt;\_Inheritance.cs* 바꾸고는 `Up` 메서드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="b3b2c-178">Open *Migrations\&lt;timestamp&gt;\_Inheritance.cs* and replace the `Up` method with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

<span data-ttu-id="b3b2c-179">실행 된 `update-database` 명령을 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-179">Run the `update-database` command again.</span></span>

> [!NOTE]
> <span data-ttu-id="b3b2c-180">스키마 변경 하므로 및 데이터를 마이그레이션하는 경우 다른 오류를 가져오려는 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-180">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="b3b2c-181">마이그레이션 오류가 발생할 경우 해결할 수 없는, 연결 문자열을 변경 하 여이 자습서를 계속 하기는 *Web.config* 파일 또는 데이터베이스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-181">If you get migration errors you can't resolve, you can continue with the tutorial by changing the connection string in the *Web.config* file or deleting the database.</span></span> <span data-ttu-id="b3b2c-182">가장 간단한 방법은 데이터베이스의 이름을 바꾸는 하는 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-182">The simplest approach is to rename the database in the *Web.config* file.</span></span> <span data-ttu-id="b3b2c-183">예를 들어 데이터베이스 이름을 CU로 변경\_다음 예제와 같이 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-183">For example, change the database name to CU\_test as shown in the following example:</span></span>
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> <span data-ttu-id="b3b2c-184">새 데이터베이스에서는 데이터가 없는 마이그레이션하려면 및 `update-database` 명령 작업이 오류 없이 완료 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-184">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="b3b2c-185">데이터베이스를 삭제 하는 방법에 지침은 [Visual Studio 2012에서 데이터베이스를 삭제 하는 방법을](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-185">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span> <span data-ttu-id="b3b2c-186">이 자습서를 계속 하려면이 방법을 사용 하는 경우는 마이그레이션이 자동으로 실행 될 때 배포 된 사이트 동일한 오류가 대기줄 않으므로이 자습서의 끝에 배포 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-186">If you take this approach in order to continue with the tutorial, skip the deployment step at the end of this tutorial, since the deployed site would get the same error when it runs migrations automatically.</span></span> <span data-ttu-id="b3b2c-187">마이그레이션 오류 문제를 해결 하려면 가장 적합 한 리소스는 StackOverflow.com 또는 Entity Framework 포럼 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-187">If you want to troubleshoot a migrations error, the best resource is one of the Entity Framework forums or StackOverflow.com.</span></span>


## <a name="testing"></a><span data-ttu-id="b3b2c-188">테스트</span><span class="sxs-lookup"><span data-stu-id="b3b2c-188">Testing</span></span>

<span data-ttu-id="b3b2c-189">사이트를 실행 하 고 다양 한 페이지를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-189">Run the site and try various pages.</span></span> <span data-ttu-id="b3b2c-190">모든 항목이 작동 하기 전과 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-190">Everything works the same as it did before.</span></span>

<span data-ttu-id="b3b2c-191">**서버 탐색기** 확장 **SchoolContext** 차례로 **테이블**, 했다는 보고는 **학생** 및 **강사**  으로 바꾼 테이블을 **사람** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-191">In **Server Explorer,** expand **SchoolContext** and then **Tables**, and you see that the **Student** and **Instructor** tables have been replaced by a **Person** table.</span></span> <span data-ttu-id="b3b2c-192">확장 하 고는 **사람** 테이블을 모두 사용 하는 열 참조는 **학생** 및 **강사** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-192">Expand the **Person** table and you see that it has all of the columns that used to be in the **Student** and **Instructor** tables.</span></span>

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="b3b2c-194">Person 테이블을 마우스 오른쪽 단추로 누른 **테이블 데이터 표시** 판별자 열을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-194">Right-click the Person table, and then click **Show Table Data** to see the discriminator column.</span></span>

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="b3b2c-195">다음 다이어그램에서는 새 School 데이터베이스의 구조를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-195">The following diagram illustrates the structure of the new School database:</span></span>

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a><span data-ttu-id="b3b2c-197">요약</span><span class="sxs-lookup"><span data-stu-id="b3b2c-197">Summary</span></span>

<span data-ttu-id="b3b2c-198">에 대해 계층당 하나의 테이블 상속이 구현 이제는 `Person`, `Student`, 및 `Instructor` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-198">Table-per-hierarchy inheritance has now been implemented for the `Person`, `Student`, and `Instructor` classes.</span></span> <span data-ttu-id="b3b2c-199">이 및 다른 상속 구조에 대 한 자세한 내용은 참조 [상속 매핑 전략](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) Morteza Manavi 블로그.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-199">For more information about this and other inheritance structures, see [Inheritance Mapping Strategies](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) on Morteza Manavi's blog.</span></span> <span data-ttu-id="b3b2c-200">다음 자습서에서는 일부의 작업 패턴의 단위 및 저장소 구현 하기 위해 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-200">In the next tutorial you'll see some ways to implement the repository and unit of work patterns.</span></span>

<span data-ttu-id="b3b2c-201">다른 Entity Framework 리소스에 대 한 링크에서 확인할 수 있습니다는 [ASP.NET 데이터 액세스 콘텐츠 맵](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3b2c-201">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="b3b2c-202">[이전](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[다음](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="b3b2c-202">[Previous](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span></span>
