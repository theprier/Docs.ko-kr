---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: (8 / 10) ASP.NET MVC 응용 프로그램에서 Entity Framework 사용한 상속 구현 | Microsoft Docs
author: tdykstra
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 10ee0be62a1d601e323afc423e9022bed56f4f33
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831512"
---
<a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a><span data-ttu-id="7c768-103">(8 / 10) ASP.NET MVC 응용 프로그램에서 Entity Framework 사용한 상속 구현</span><span class="sxs-lookup"><span data-stu-id="7c768-103">Implementing Inheritance with the Entity Framework in an ASP.NET MVC Application (8 of 10)</span></span>
====================
<span data-ttu-id="7c768-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="7c768-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="7c768-105">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="7c768-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="7c768-106">Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio 2012를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="7c768-107">자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c768-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="7c768-108">시작 부분에서 자습서 시리즈를 시작할 수 있습니다 또는 [이 장이에 대 한 시작 프로젝트 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 여기에서 시작 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="7c768-109">해결할 수 없는 문제가 발생 하는 경우 [완성 된 장 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 문제를 재현 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="7c768-110">일반적으로 코드의 완성 된 코드를 비교 하 여 문제에 솔루션을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="7c768-111">몇 가지 일반적인 오류 및 해결 하는 방법에 대 한 참조 [오류 및 해결 방법입니다.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="7c768-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>


<span data-ttu-id="7c768-112">이전 자습서에서 동시성 예외를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-112">In the previous tutorial you handled concurrency exceptions.</span></span> <span data-ttu-id="7c768-113">이 자습서에서는 데이터 모델에서 상속을 구현하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-113">This tutorial will show you how to implement inheritance in the data model.</span></span>

<span data-ttu-id="7c768-114">개체 지향 프로그래밍에서 중복 코드를 제거 하기 위해 상속을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-114">In object-oriented programming, you can use inheritance to eliminate redundant code.</span></span> <span data-ttu-id="7c768-115">이 자습서에서는 강사와 학생 모두에게 공통적인 속성(예: `LastName`)이 포함된 `Person` 기본 클래스에서 클래스가 파생되도록 `Instructor` 및 `Student` 클래스를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-115">In this tutorial, you'll change the `Instructor` and `Student` classes so that they derive from a `Person` base class which contains properties such as `LastName` that are common to both instructors and students.</span></span> <span data-ttu-id="7c768-116">웹 페이지를 추가하거나 변경하지는 않지만 일부 코드를 변경하고 이러한 변경 내용이 데이터베이스에 자동으로 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-116">You won't add or change any web pages, but you'll change some of the code and those changes will be automatically reflected in the database.</span></span>

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a><span data-ttu-id="7c768-117">형식당 하나의 테이블 상속 및 계층 당 테이블</span><span class="sxs-lookup"><span data-stu-id="7c768-117">Table-per-Hierarchy versus Table-per-Type Inheritance</span></span>

<span data-ttu-id="7c768-118">개체 지향 프로그래밍에서는 쉽게 관련된 클래스를 사용 하 여 상속을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-118">In object-oriented programming, you can use inheritance to make it easier to work with related classes.</span></span> <span data-ttu-id="7c768-119">예를 들어 합니다 `Instructor` 하 고 `Student` 의 클래스는 `School` 데이터 모델 중복 코드에서 발생 하는 몇 가지 속성을 공유:</span><span class="sxs-lookup"><span data-stu-id="7c768-119">For example, the `Instructor` and `Student` classes in the `School` data model share several properties, which results in redundant code:</span></span>

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

<span data-ttu-id="7c768-121">`Instructor` 및 `Student` 엔터티에서 공유하는 속성에 대해 중복 코드를 제거하려고 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-121">Suppose you want to eliminate the redundant code for the properties that are shared by the `Instructor` and `Student` entities.</span></span> <span data-ttu-id="7c768-122">만들 수 있습니다는 `Person` 기본 공유 속성만 포함 하는 클래스를 확인 합니다 `Instructor` 및 `Student` 다음 그림에 나와 있는 것 처럼 해당 기본 클래스에서 상속 되는 엔터티:</span><span class="sxs-lookup"><span data-stu-id="7c768-122">You could create a `Person` base class which contains only those shared properties, then make the `Instructor` and `Student` entities inherit from that base class, as shown in the following illustration:</span></span>

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

<span data-ttu-id="7c768-124">데이터베이스에 이 상속 구조를 여러 가지 방법으로 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-124">There are several ways this inheritance structure could be represented in the database.</span></span> <span data-ttu-id="7c768-125">바라는 `Person` 학생과 강사 단일 테이블에서에 대 한 정보를 포함 하는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-125">You could have a `Person` table that includes information about both students and instructors in a single table.</span></span> <span data-ttu-id="7c768-126">강사에만 적용할 수의 일부 열 (`HireDate`), 학생 들 에게만 일부 (`EnrollmentDate`), 둘 다로 일부 (`LastName`, `FirstName`).</span><span class="sxs-lookup"><span data-stu-id="7c768-126">Some of the columns could apply only to instructors (`HireDate`), some only to students (`EnrollmentDate`), some to both (`LastName`, `FirstName`).</span></span> <span data-ttu-id="7c768-127">일반적으로 해야는 *판별자* 각 행 형식을 나타내도록 열을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-127">Typically, you'd have a *discriminator* column to indicate which type each row represents.</span></span> <span data-ttu-id="7c768-128">예를 들어, 판별자 열은 강사에 대해 "Instructor"를, 학생에 대해 "Student"를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-128">For example, the discriminator column might have "Instructor" for instructors and "Student" for students.</span></span>

![Hierarchy_example 당 테이블](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

<span data-ttu-id="7c768-130">단일 데이터베이스 테이블에서 엔터티 상속 구조를 생성 하는이 패턴 이라고 *계층당 하나의 테이블* TPH () 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-130">This pattern of generating an entity inheritance structure from a single database table is called *table-per-hierarchy* (TPH) inheritance.</span></span>

<span data-ttu-id="7c768-131">다른 방법은 데이터베이스를 상속 구조와 유사하게 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-131">An alternative is to make the database look more like the inheritance structure.</span></span> <span data-ttu-id="7c768-132">예를 들어 이름 필드만 있을 수 있습니다는 `Person` 테이블 있고 별도 `Instructor` 및 `Student` 날짜 필드를 사용 하 여 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-132">For example, you could have only the name fields in the `Person` table and have separate `Instructor` and `Student` tables with the date fields.</span></span>

![Table-per-type_inheritance](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

<span data-ttu-id="7c768-134">이 패턴의 각 엔터티 클래스는 호출에 대 한 데이터베이스 테이블을 만드는 *형식당 하나의 테이블* (TPT) 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-134">This pattern of making a database table for each entity class is called *table per type* (TPT) inheritance.</span></span>

<span data-ttu-id="7c768-135">TPH 상속 패턴 일반적으로 더 나은 성능을 낼 TPT 상속 패턴 보다 Entity Framework에서 TPT 패턴이 복잡 한 조인 쿼리에서 발생할 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-135">TPH inheritance patterns generally deliver better performance in the Entity Framework than TPT inheritance patterns, because TPT patterns can result in complex join queries.</span></span> <span data-ttu-id="7c768-136">이 자습서에서는 TPH 상속을 구현하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-136">This tutorial demonstrates how to implement TPH inheritance.</span></span> <span data-ttu-id="7c768-137">다음 단계를 수행 하 여 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-137">You'll do that by performing the following steps:</span></span>

- <span data-ttu-id="7c768-138">만들기를 `Person` 클래스 및 변경 합니다 `Instructor` 하 고 `Student` 클래스에서 상속할 수 `Person`.</span><span class="sxs-lookup"><span data-stu-id="7c768-138">Create a `Person` class and change the `Instructor` and `Student` classes to derive from `Person`.</span></span>
- <span data-ttu-id="7c768-139">데이터베이스 컨텍스트 클래스를 데이터베이스에 모델 매핑 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-139">Add model-to-database mapping code to the database context class.</span></span>
- <span data-ttu-id="7c768-140">변경 `InstructorID` 하 고 `StudentID` 참조를 프로젝트 전체에 걸쳐 `PersonID`합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-140">Change `InstructorID` and `StudentID` references throughout the project to `PersonID`.</span></span>

## <a name="creating-the-person-class"></a><span data-ttu-id="7c768-141">Person 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="7c768-141">Creating the Person Class</span></span>

 <span data-ttu-id="7c768-142">참고: 수 없게 이러한 클래스를 사용 하는 컨트롤러를 업데이트할 때까지 아래의 클래스를 만든 후 프로젝트를 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-142">Note: You won't be able to compile the project after creating the classes below until you update the controllers that uses these classes.</span></span> 

<span data-ttu-id="7c768-143">에 *모델* 폴더를 만들기 *Person.cs* 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-143">In the *Models* folder, create *Person.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="7c768-144">*Instructor.cs*를 파생 합니다 `Instructor` 에서 클래스를 `Person` 클래스 및 키 및 이름 필드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-144">In *Instructor.cs*, derive the `Instructor` class from the `Person` class and remove the key and name fields.</span></span> <span data-ttu-id="7c768-145">해당 코드는 다음 예제와 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-145">The code will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="7c768-146">비슷하게 변경할 *Student.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-146">Make similar changes to *Student.cs*.</span></span> <span data-ttu-id="7c768-147">`Student` 클래스는 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-147">The `Student` class will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a><span data-ttu-id="7c768-148">Person 엔터티 형식을 모델에 추가</span><span class="sxs-lookup"><span data-stu-id="7c768-148">Adding the Person Entity Type to the Model</span></span>

<span data-ttu-id="7c768-149">*SchoolContext.cs*, 추가 `DbSet` 에 대 한 속성을 `Person` 엔터티 형식:</span><span class="sxs-lookup"><span data-stu-id="7c768-149">In *SchoolContext.cs*, add a `DbSet` property for the `Person` entity type:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="7c768-150">계층당 하나의 테이블 상속을 구성하기 위해 Entity Framework에 필요한 모든 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-150">This is all that the Entity Framework needs in order to configure table-per-hierarchy inheritance.</span></span> <span data-ttu-id="7c768-151">더 알 수 있듯이, 데이터베이스를 다시 만든 경우는 `Person` 대신 테이블을 `Student` 및 `Instructor` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-151">As you'll see, when the database is re-created, it will have a `Person` table in place of the `Student` and `Instructor` tables.</span></span>

## <a name="changing-instructorid-and-studentid-to-personid"></a><span data-ttu-id="7c768-152">InstructorID StudentID PersonID로 변경</span><span class="sxs-lookup"><span data-stu-id="7c768-152">Changing InstructorID and StudentID to PersonID</span></span>

<span data-ttu-id="7c768-153">*SchoolContext.cs*, 강사-강좌 매핑 문에서 변경 `MapRightKey("InstructorID")` 하려면 `MapRightKey("PersonID")`:</span><span class="sxs-lookup"><span data-stu-id="7c768-153">In *SchoolContext.cs*, in the Instructor-Course mapping statement, change `MapRightKey("InstructorID")` to `MapRightKey("PersonID")`:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

<span data-ttu-id="7c768-154">이 변경에는; 필요 하지 않습니다. 방금 다 대 다 조인 테이블에 InstructorID 열의 이름을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-154">This change isn't required; it just changes the name of the InstructorID column in the many-to-many join table.</span></span> <span data-ttu-id="7c768-155">InstructorID로 이름을 지정 하지, 응용 프로그램 여전히 올바르게 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-155">If you left the name as InstructorID, the application would still work correctly.</span></span> <span data-ttu-id="7c768-156">여기에 전체 *SchoolContext.cs*:</span><span class="sxs-lookup"><span data-stu-id="7c768-156">Here is the completed *SchoolContext.cs*:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

<span data-ttu-id="7c768-157">변경 해야 하는 다음 `InstructorID` 에 `PersonID` 및 `StudentID` 에 `PersonID` 프로젝트 전반에 걸쳐 ***제외 하 고*** 의 타임 스탬프 마이그레이션 파일에는 *마이그레이션을* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-157">Next you need to change `InstructorID` to `PersonID` and `StudentID` to `PersonID` throughout the project ***except*** in the time-stamped migrations files in the *Migrations* folder.</span></span> <span data-ttu-id="7c768-158">이렇게 하려면 찾 및 변경 해야 할 파일만 연 다음 열린된 파일에 전역 변경을 수행 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-158">To do that you'll find and open only the files that need to be changed, then perform a global change on the opened files.</span></span> <span data-ttu-id="7c768-159">유일한 파일을 *마이그레이션을* 변경 해야 하는 폴더는 *migrations\ configuration.cs 합니다.*</span><span class="sxs-lookup"><span data-stu-id="7c768-159">The only file in the *Migrations* folder you should change is *Migrations\Configuration.cs.*</span></span>

1. > [!IMPORTANT]
   > <span data-ttu-id="7c768-160">Visual Studio에서 열려 있는 모든 파일을 닫아 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-160">Begin by closing all the open files in Visual Studio.</span></span>
2. <span data-ttu-id="7c768-161">클릭 **찾기 및 바꾸기-모든 파일을 찾으려면** 에 **편집** 메뉴 및 포함 된 프로젝트의 모든 파일에 대 한 다음 검색 `InstructorID`합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-161">Click **Find and Replace -- Find all Files** in the **Edit** menu, and then search for all files in the project that contain `InstructorID`.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. <span data-ttu-id="7c768-162">각 파일을 엽니다는 **찾기 결과** 창 ***제외한*** 는 &lt;타임 스탬프&gt;*\_.cs* 합니다 에서마이그레이션파일*마이그레이션을* 폴더, 각 파일에 대 한 한 줄을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-162">Open each file in the **Find Results** window ***except*** the &lt;time-stamp&gt;*\_.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. <span data-ttu-id="7c768-163">열기를 **파일에서 바꾸기** 대화 상자 및 변경 **찾는 위치** 하 **모든 열린 문서**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-163">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
5. <span data-ttu-id="7c768-164">사용 된 **파일에서 바꾸기** 변경할 모든 대화 상자를 `InstructorID` 를 `PersonID.`</span><span class="sxs-lookup"><span data-stu-id="7c768-164">Use the **Replace in Files** dialog to change all `InstructorID` to `PersonID.`</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. <span data-ttu-id="7c768-165">포함 된 프로젝트의 모든 파일을 찾을 `StudentID`합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-165">Find all the files in the project that contain `StudentID`.</span></span>
7. <span data-ttu-id="7c768-166">각 파일을 엽니다는 **찾기 결과** 창이 ***제외한*** 는 &lt;타임 스탬프&gt;*\_\*.cs* 마이그레이션 파일 에 *마이그레이션을* 각 파일에 대 한 한 줄을 두 번 클릭 하 여 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-166">Open each file in the **Find Results** window ***except*** the &lt;time-stamp&gt;*\_\*.cs* migration files in the *Migrations* folder, by double-clicking one line for each file.</span></span>  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. <span data-ttu-id="7c768-167">열기를 **파일에서 바꾸기** 대화 상자 및 변경 **찾는 위치** 하 **모든 열린 문서**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-167">Open the **Replace in Files** dialog and change **Look in** to **All Open Documents**.</span></span>
9. <span data-ttu-id="7c768-168">사용 하 여는 **파일에서 바꾸기** 모두를 변경 하려면 대화 상자 `StudentID` 에 `PersonID`입니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-168">Use the **Replace in Files** dialog to change all `StudentID` to `PersonID`.</span></span>   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. <span data-ttu-id="7c768-169">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-169">Build the project.</span></span>

<span data-ttu-id="7c768-170">(이 보여 주는 참고를 *단점은* 의 `classnameID` 패턴 기본 키의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-170">(Note that this demonstrates a *disadvantage* of the `classnameID` pattern for naming primary keys.</span></span> <span data-ttu-id="7c768-171">기본 키 ID 클래스 이름 접두사 없이 명명 된 경우 *없습니다* 이름을 변경 해야 하지만 이제.)</span><span class="sxs-lookup"><span data-stu-id="7c768-171">If you had named primary keys ID without prefixing the class name, *no* renaming would be necessary now.)</span></span>

## <a name="create-and-update-a-migrations-file"></a><span data-ttu-id="7c768-172">마이그레이션 파일 만들기 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="7c768-172">Create and Update a Migrations File</span></span>

<span data-ttu-id="7c768-173">관리자 콘솔 (PMC (패키지)을 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-173">In the Package Manager Console (PMC), enter the following command:</span></span>

`Add-Migration Inheritance`

<span data-ttu-id="7c768-174">실행 된 `Update-Database` PMC에서 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-174">Run the `Update-Database` command in the PMC.</span></span> <span data-ttu-id="7c768-175">명령은 기존 데이터 마이그레이션을 처리 하는 방법을 알지에 있기 때문이 시점에서 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-175">The command will fail at this point because we have existing data that migrations doesn't know how to handle.</span></span> <span data-ttu-id="7c768-176">다음 오류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-176">You get the following error:</span></span>

<span data-ttu-id="7c768-177">*ALTER TABLE 문이 FOREIGN KEY 제약 조건 충돌 "FK\_dbo입니다. 부서\_dbo입니다. Person\_PersonID "입니다. 데이터베이스 "ContosoUniversity", "dbo 테이블에서에서 충돌이 발생 했습니다. 사용자 ", 열 'PersonID'입니다.*</span><span class="sxs-lookup"><span data-stu-id="7c768-177">*The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK\_dbo.Department\_dbo.Person\_PersonID". The conflict occurred in database "ContosoUniversity", table "dbo.Person", column 'PersonID'.*</span></span>

<span data-ttu-id="7c768-178">오픈 *마이그레이션을\&lt; 타임 스탬프&gt;\_Inheritance.cs* 바꾸고는 `Up` 메서드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="7c768-178">Open *Migrations\&lt;timestamp&gt;\_Inheritance.cs* and replace the `Up` method with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

<span data-ttu-id="7c768-179">실행 된 `update-database` 명령을 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-179">Run the `update-database` command again.</span></span>

> [!NOTE]
> <span data-ttu-id="7c768-180">스키마 변경 하므로 및 데이터를 마이그레이션하는 경우 다른 오류가 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-180">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="7c768-181">마이그레이션 오류가 발생할 경우 해결할 수 없는, 연결 문자열을 변경 하 여 자습서를 진행할 수 있습니다 합니다 *Web.config* 파일 또는 데이터베이스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-181">If you get migration errors you can't resolve, you can continue with the tutorial by changing the connection string in the *Web.config* file or deleting the database.</span></span> <span data-ttu-id="7c768-182">가장 간단한 방법은 데이터베이스의 이름을 바꾸려면 합니다 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-182">The simplest approach is to rename the database in the *Web.config* file.</span></span> <span data-ttu-id="7c768-183">예를 들어, CU로 데이터베이스 이름을 변경\_다음 예제에서와 같이 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-183">For example, change the database name to CU\_test as shown in the following example:</span></span>
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> <span data-ttu-id="7c768-184">새 데이터베이스에 데이터가 없습니다. 마이그레이션할 및 `update-database` 명령은 오류 없이 완료 될 가능성이 훨씬 더 높습니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-184">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="7c768-185">데이터베이스를 삭제 하는 방법에 지침은 [Visual Studio 2012에서 데이터베이스를 삭제 하는 방법](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-185">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span> <span data-ttu-id="7c768-186">이 자습서를 계속 하려면이 방법을 사용 하는 경우는 마이그레이션이 자동으로 실행 될 때 배포 된 사이트에서 동일한 오류를 얻게 되므로이 자습서의 끝에서 배포 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-186">If you take this approach in order to continue with the tutorial, skip the deployment step at the end of this tutorial, since the deployed site would get the same error when it runs migrations automatically.</span></span> <span data-ttu-id="7c768-187">마이그레이션 오류 문제를 해결 하려는 경우 가장 좋은 리소스는 Entity Framework 포럼 또는 StackOverflow.com 중입니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-187">If you want to troubleshoot a migrations error, the best resource is one of the Entity Framework forums or StackOverflow.com.</span></span>


## <a name="testing"></a><span data-ttu-id="7c768-188">테스트</span><span class="sxs-lookup"><span data-stu-id="7c768-188">Testing</span></span>

<span data-ttu-id="7c768-189">사이트를 실행 하 고 다양 한 페이지를 시도 하세요.</span><span class="sxs-lookup"><span data-stu-id="7c768-189">Run the site and try various pages.</span></span> <span data-ttu-id="7c768-190">모든 항목이 이전과 같이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-190">Everything works the same as it did before.</span></span>

<span data-ttu-id="7c768-191">**서버 탐색기** 확장 **SchoolContext** 차례로 **테이블**를 표시 하 고는 **학생** 및 **강사**  테이블 바뀌었습니다를 **Person** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-191">In **Server Explorer,** expand **SchoolContext** and then **Tables**, and you see that the **Student** and **Instructor** tables have been replaced by a **Person** table.</span></span> <span data-ttu-id="7c768-192">확장 합니다 **Person** 테이블 표시 이어야 하는 데 사용 하는 열 모두에 **학생** 및 **강사** 테이블.</span><span class="sxs-lookup"><span data-stu-id="7c768-192">Expand the **Person** table and you see that it has all of the columns that used to be in the **Student** and **Instructor** tables.</span></span>

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="7c768-194">Person 테이블을 마우스 오른쪽 단추로 클릭한 후 **테이블 데이터 표시**를 클릭하여 판별자 열을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-194">Right-click the Person table, and then click **Show Table Data** to see the discriminator column.</span></span>

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="7c768-195">다음 다이어그램에서는 새 School 데이터베이스의 구조를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-195">The following diagram illustrates the structure of the new School database:</span></span>

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a><span data-ttu-id="7c768-197">요약</span><span class="sxs-lookup"><span data-stu-id="7c768-197">Summary</span></span>

<span data-ttu-id="7c768-198">이제 계층당 하나의 테이블 상속에 대해 구현에 `Person`, `Student`, 및 `Instructor` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-198">Table-per-hierarchy inheritance has now been implemented for the `Person`, `Student`, and `Instructor` classes.</span></span> <span data-ttu-id="7c768-199">이 및 다른 상속 구조에 대 한 자세한 내용은 참조 하세요. [상속 매핑 전략](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) Morteza Manavi 블로그.</span><span class="sxs-lookup"><span data-stu-id="7c768-199">For more information about this and other inheritance structures, see [Inheritance Mapping Strategies](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) on Morteza Manavi's blog.</span></span> <span data-ttu-id="7c768-200">다음 자습서에서는 리포지토리 및 작업 패턴 단위를 구현 하는 몇 가지 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-200">In the next tutorial you'll see some ways to implement the repository and unit of work patterns.</span></span>

<span data-ttu-id="7c768-201">다른 Entity Framework 리소스에 대 한 링크에서 찾을 수 있습니다 합니다 [ASP.NET 데이터 액세스 콘텐츠 맵](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c768-201">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7c768-202">[이전](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [다음](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="7c768-202">[Previous](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)</span></span>
