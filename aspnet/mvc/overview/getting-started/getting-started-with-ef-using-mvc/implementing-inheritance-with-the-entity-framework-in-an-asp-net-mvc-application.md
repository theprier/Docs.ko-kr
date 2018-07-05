---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC 5 응용 프로그램 (11 12)에서 Entity Framework 6 사용한 상속 구현 | Microsoft Docs
author: tdykstra
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/07/2014
ms.topic: article
ms.assetid: 08834147-77ec-454a-bb7a-d931d2a40dab
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d10656f5ce0479e1290fa6921f2d1a99d1081b57
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37382980"
---
<a name="implementing-inheritance-with-the-entity-framework-6-in-an-aspnet-mvc-5-application-11-of-12"></a><span data-ttu-id="6aee3-103">ASP.NET MVC 5 응용 프로그램 (11 12)에서 Entity Framework 6 사용한 상속 구현</span><span class="sxs-lookup"><span data-stu-id="6aee3-103">Implementing Inheritance with the Entity Framework 6 in an ASP.NET MVC 5 Application (11 of 12)</span></span>
====================
<span data-ttu-id="6aee3-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="6aee3-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="6aee3-105">[완료 된 프로젝트를 다운로드](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) 또는 [PDF 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)</span><span class="sxs-lookup"><span data-stu-id="6aee3-105">[Download Completed Project](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) or [Download PDF](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)</span></span>

> <span data-ttu-id="6aee3-106">Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio 2013을 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 5 applications using the Entity Framework 6 Code First and Visual Studio 2013.</span></span> <span data-ttu-id="6aee3-107">자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6aee3-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>


<span data-ttu-id="6aee3-108">이전 자습서에서 동시성 예외를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-108">In the previous tutorial you handled concurrency exceptions.</span></span> <span data-ttu-id="6aee3-109">이 자습서에서는 데이터 모델에서 상속을 구현하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-109">This tutorial will show you how to implement inheritance in the data model.</span></span>

<span data-ttu-id="6aee3-110">개체 지향 프로그래밍에서 사용할 수 있습니다 [상속](http://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)) 용이 하 게 [코드 재사용](http://en.wikipedia.org/wiki/Code_reuse)합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-110">In object-oriented programming, you can use [inheritance](http://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)) to facilitate [code reuse](http://en.wikipedia.org/wiki/Code_reuse).</span></span> <span data-ttu-id="6aee3-111">이 자습서에서는 강사와 학생 모두에게 공통적인 속성(예: `LastName`)이 포함된 `Person` 기본 클래스에서 클래스가 파생되도록 `Instructor` 및 `Student` 클래스를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-111">In this tutorial, you'll change the `Instructor` and `Student` classes so that they derive from a `Person` base class which contains properties such as `LastName` that are common to both instructors and students.</span></span> <span data-ttu-id="6aee3-112">웹 페이지를 추가하거나 변경하지는 않지만 일부 코드를 변경하고 이러한 변경 내용이 데이터베이스에 자동으로 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-112">You won't add or change any web pages, but you'll change some of the code and those changes will be automatically reflected in the database.</span></span>

## <a name="options-for-mapping-inheritance-to-database-tables"></a><span data-ttu-id="6aee3-113">상속을 데이터베이스 테이블에 매핑하기 위한 옵션</span><span class="sxs-lookup"><span data-stu-id="6aee3-113">Options for mapping inheritance to database tables</span></span>

<span data-ttu-id="6aee3-114">`Instructor` 및 `Student` 의 클래스는 `School` 데이터 모델은 일부의 속성이 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-114">The `Instructor` and `Student` classes in the `School` data model have several properties that are identical:</span></span>

![Student_and_Instructor_classes](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="6aee3-116">`Instructor` 및 `Student` 엔터티에서 공유하는 속성에 대해 중복 코드를 제거하려고 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-116">Suppose you want to eliminate the redundant code for the properties that are shared by the `Instructor` and `Student` entities.</span></span> <span data-ttu-id="6aee3-117">또는 강사 또는 학생의 이름인지 여부를 신경쓰지 않고 이름의 형식을 지정할 수 있는 서비스를 작성하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-117">Or you want to write a service that can format names without caring whether the name came from an instructor or a student.</span></span> <span data-ttu-id="6aee3-118">만들 수 있습니다는 `Person` 기본 공유 속성만 포함 하는 클래스를 확인 합니다 `Instructor` 및 `Student` 다음 그림에 나와 있는 것 처럼 해당 기본 클래스에서 상속 되는 엔터티:</span><span class="sxs-lookup"><span data-stu-id="6aee3-118">You could create a `Person` base class which contains only those shared properties, then make the `Instructor` and `Student` entities inherit from that base class, as shown in the following illustration:</span></span>

![Student_and_Instructor_classes_deriving_from_Person_class](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="6aee3-120">데이터베이스에 이 상속 구조를 여러 가지 방법으로 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-120">There are several ways this inheritance structure could be represented in the database.</span></span> <span data-ttu-id="6aee3-121">바라는 `Person` 학생과 강사 단일 테이블에서에 대 한 정보를 포함 하는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-121">You could have a `Person` table that includes information about both students and instructors in a single table.</span></span> <span data-ttu-id="6aee3-122">강사에만 적용할 수의 일부 열 (`HireDate`), 학생 들 에게만 일부 (`EnrollmentDate`), 둘 다로 일부 (`LastName`, `FirstName`).</span><span class="sxs-lookup"><span data-stu-id="6aee3-122">Some of the columns could apply only to instructors (`HireDate`), some only to students (`EnrollmentDate`), some to both (`LastName`, `FirstName`).</span></span> <span data-ttu-id="6aee3-123">일반적으로 해야는 *판별자* 각 행 형식을 나타내도록 열을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-123">Typically, you'd have a *discriminator* column to indicate which type each row represents.</span></span> <span data-ttu-id="6aee3-124">예를 들어, 판별자 열은 강사에 대해 "Instructor"를, 학생에 대해 "Student"를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-124">For example, the discriminator column might have "Instructor" for instructors and "Student" for students.</span></span>

![Hierarchy_example 당 테이블](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="6aee3-126">단일 데이터베이스 테이블에서 엔터티 상속 구조를 생성 하는이 패턴 이라고 *계층당 하나의 테이블* TPH () 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-126">This pattern of generating an entity inheritance structure from a single database table is called *table-per-hierarchy* (TPH) inheritance.</span></span>

<span data-ttu-id="6aee3-127">다른 방법은 데이터베이스를 상속 구조와 유사하게 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-127">An alternative is to make the database look more like the inheritance structure.</span></span> <span data-ttu-id="6aee3-128">예를 들어 이름 필드만 있을 수 있습니다는 `Person` 테이블 있고 별도 `Instructor` 및 `Student` 날짜 필드를 사용 하 여 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-128">For example, you could have only the name fields in the `Person` table and have separate `Instructor` and `Student` tables with the date fields.</span></span>

![Table-per-type_inheritance](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="6aee3-130">이 패턴의 각 엔터티 클래스는 호출에 대 한 데이터베이스 테이블을 만드는 *형식당 하나의 테이블* (TPT) 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-130">This pattern of making a database table for each entity class is called *table per type* (TPT) inheritance.</span></span>

<span data-ttu-id="6aee3-131">또 다른 옵션은 모든 비추상 형식을 개별 테이블에 매핑하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-131">Yet another option is to map all non-abstract types to individual tables.</span></span> <span data-ttu-id="6aee3-132">상속된 속성을 포함한 모든 클래스 속성을 해당 테이블의 열에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-132">All properties of a class, including inherited properties, map to columns of the corresponding table.</span></span> <span data-ttu-id="6aee3-133">이 패턴을 TPC(구체적 클래스당 하나의 테이블) 상속이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-133">This pattern is called Table-per-Concrete Class (TPC) inheritance.</span></span> <span data-ttu-id="6aee3-134">에 대 한 TPC 상속을 구현 하는 경우는 `Person`, `Student`, 및 `Instructor` 이전에 표시 된 것 처럼 클래스는 `Student` 및 `Instructor` 이전과 다르지 상속을 구현한 후 테이블 다르지 보입니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-134">If you implemented TPC inheritance for the `Person`, `Student`, and `Instructor` classes as shown earlier, the `Student` and `Instructor` tables would look no different after implementing inheritance than they did before.</span></span>

<span data-ttu-id="6aee3-135">TPC 및 TPH 상속 패턴 일반적으로 더 나은 성능을 제공 TPT 상속 패턴 보다 Entity Framework에서 TPT 패턴이 복잡 한 조인 쿼리에서 발생할 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-135">TPC and TPH inheritance patterns generally deliver better performance in the Entity Framework than TPT inheritance patterns, because TPT patterns can result in complex join queries.</span></span>

<span data-ttu-id="6aee3-136">이 자습서에서는 TPH 상속을 구현하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-136">This tutorial demonstrates how to implement TPH inheritance.</span></span> <span data-ttu-id="6aee3-137">만들기 위해 해야 할 모든 이므로 TPH는 Entity Framework에서 기본 상속 패턴을 `Person` 클래스를 변경 합니다 `Instructor` 및 `Student` 클래스에서 상속할 수 `Person`, 새 클래스를 추가 합니다를 `DbContext`, 만들고를 마이그레이션입니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-137">TPH is the default inheritance pattern in the Entity Framework, so all you have to do is create a `Person` class, change the `Instructor` and `Student` classes to derive from `Person`, add the new class to the `DbContext`, and create a migration.</span></span> <span data-ttu-id="6aee3-138">(다른 상속 패턴을 구현 하는 방법에 대 한 자세한 내용은 [(TPT) 형식당 하나의 테이블 상속 매핑](https://msdn.microsoft.com/data/jj591617#2.5) 하 고 [구체적 형식당 테이블 클래스 (TPC) 상속 매핑](https://msdn.microsoft.com/data/jj591617#2.6) msdn Entity Framework 설명서입니다.)</span><span class="sxs-lookup"><span data-stu-id="6aee3-138">(For information about how to implement the other inheritance patterns, see [Mapping the Table-Per-Type (TPT) Inheritance](https://msdn.microsoft.com/data/jj591617#2.5) and [Mapping the Table-Per-Concrete Class (TPC) Inheritance](https://msdn.microsoft.com/data/jj591617#2.6) in the MSDN Entity Framework documentation.)</span></span>

## <a name="create-the-person-class"></a><span data-ttu-id="6aee3-139">Person 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="6aee3-139">Create the Person class</span></span>

<span data-ttu-id="6aee3-140">에 *모델* 폴더를 만들기 *Person.cs* 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-140">In the *Models* folder, create *Person.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="make-student-and-instructor-classes-inherit-from-person"></a><span data-ttu-id="6aee3-141">Person 클래스로부터 상속되는 Student 및 Instructor 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="6aee3-141">Make Student and Instructor classes inherit from Person</span></span>

<span data-ttu-id="6aee3-142">*Instructor.cs*를 파생 합니다 `Instructor` 에서 클래스를 `Person` 클래스 및 키 및 이름 필드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-142">In *Instructor.cs*, derive the `Instructor` class from the `Person` class and remove the key and name fields.</span></span> <span data-ttu-id="6aee3-143">해당 코드는 다음 예제와 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-143">The code will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="6aee3-144">비슷하게 변경할 *Student.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-144">Make similar changes to *Student.cs*.</span></span> <span data-ttu-id="6aee3-145">`Student` 클래스는 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-145">The `Student` class will look like the following example:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="add-the-person-entity-type-to-the-model"></a><span data-ttu-id="6aee3-146">Person 엔터티 형식을 모델에 추가</span><span class="sxs-lookup"><span data-stu-id="6aee3-146">Add the Person Entity Type to the Model</span></span>

<span data-ttu-id="6aee3-147">*SchoolContext.cs*, 추가 `DbSet` 에 대 한 속성을 `Person` 엔터티 형식:</span><span class="sxs-lookup"><span data-stu-id="6aee3-147">In *SchoolContext.cs*, add a `DbSet` property for the `Person` entity type:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="6aee3-148">계층당 하나의 테이블 상속을 구성하기 위해 Entity Framework에 필요한 모든 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-148">This is all that the Entity Framework needs in order to configure table-per-hierarchy inheritance.</span></span> <span data-ttu-id="6aee3-149">더 알 수 있듯이, 데이터베이스가 업데이트 되는 경우는 `Person` 대신 테이블을 `Student` 및 `Instructor` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-149">As you'll see, when the database is updated, it will have a `Person` table in place of the `Student` and `Instructor` tables.</span></span>

## <a name="create-and-update-a-migrations-file"></a><span data-ttu-id="6aee3-150">마이그레이션 파일 만들기 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="6aee3-150">Create and Update a Migrations File</span></span>

<span data-ttu-id="6aee3-151">관리자 콘솔 (PMC (패키지)을 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-151">In the Package Manager Console (PMC), enter the following command:</span></span>

`Add-Migration Inheritance`

<span data-ttu-id="6aee3-152">실행 된 `Update-Database` PMC에서 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-152">Run the `Update-Database` command in the PMC.</span></span> <span data-ttu-id="6aee3-153">명령은 기존 데이터 마이그레이션을 처리 하는 방법을 알지에 있기 때문이 시점에서 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-153">The command will fail at this point because we have existing data that migrations doesn't know how to handle.</span></span> <span data-ttu-id="6aee3-154">다음과 같은 오류 메시지가 표시:</span><span class="sxs-lookup"><span data-stu-id="6aee3-154">You get an error message like the following one:</span></span>

> <span data-ttu-id="6aee3-155">*개체를 삭제할 수 없습니다 ' dbo입니다. 강사 ' FOREIGN KEY 제약 조건에 의해 참조 되므로 합니다.*</span><span class="sxs-lookup"><span data-stu-id="6aee3-155">*Could not drop object 'dbo.Instructor' because it is referenced by a FOREIGN KEY constraint.*</span></span>


<span data-ttu-id="6aee3-156">오픈 *마이그레이션을\&lt; 타임 스탬프&gt;\_Inheritance.cs* 바꾸고는 `Up` 메서드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="6aee3-156">Open *Migrations\&lt;timestamp&gt;\_Inheritance.cs* and replace the `Up` method with the following code:</span></span>

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

<span data-ttu-id="6aee3-157">이 코드는 다음과 같은 데이터베이스 업데이트 작업을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-157">This code takes care of the following database update tasks:</span></span>

- <span data-ttu-id="6aee3-158">Student 테이블을 가리키는 외래 키 제약 조건 및 인덱스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-158">Removes foreign key constraints and indexes that point to the Student table.</span></span>
- <span data-ttu-id="6aee3-159">Instructor 테이블 이름을 Person으로 바꾸고 Student 데이터를 저장하기 위해 필요한 변경을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-159">Renames the Instructor table as Person and makes changes needed for it to store Student data:</span></span>

    - <span data-ttu-id="6aee3-160">학생에 대한 Nullable EnrollmentDate를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-160">Adds nullable EnrollmentDate for students.</span></span>
    - <span data-ttu-id="6aee3-161">행이 학생용인지, 강사용인지 나타내는 판별자 열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-161">Adds Discriminator column to indicate whether a row is for a student or an instructor.</span></span>
    - <span data-ttu-id="6aee3-162">학생 행은 고용 날짜를 포함하지 않으므로 HireDate를 Nullable로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-162">Makes HireDate nullable since student rows won't have hire dates.</span></span>
    - <span data-ttu-id="6aee3-163">학생을 가리키는 외래 키를 업데이트하는 데 사용할 임시 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-163">Adds a temporary field that will be used to update foreign keys that point to students.</span></span> <span data-ttu-id="6aee3-164">학생에 게 Person 테이블로 복사할 때 새 기본 키 값 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-164">When you copy students into the Person table they'll get new primary key values.</span></span>
- <span data-ttu-id="6aee3-165">Student 테이블에서 Person 테이블로 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-165">Copies data from the Student table into the Person table.</span></span> <span data-ttu-id="6aee3-166">그러면 학생에게 새 기본 키 값이 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-166">This causes students to get assigned new primary key values.</span></span>
- <span data-ttu-id="6aee3-167">학생을 가리키는 외래 키 값을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-167">Fixes foreign key values that point to students.</span></span>
- <span data-ttu-id="6aee3-168">이제 Person 테이블을 가리키도록 외래 키 제약 조건 및 인덱스를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-168">Re-creates foreign key constraints and indexes, now pointing them to the Person table.</span></span>

<span data-ttu-id="6aee3-169">(기본 키 형식으로 정수 대신 GUID를 사용한 경우, 학생 기본 키 값을 변경할 필요가 없으며 이 단계 중 일부가 생략되었을 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="6aee3-169">(If you had used GUID instead of integer as the primary key type, the student primary key values wouldn't have to change, and several of these steps could have been omitted.)</span></span>

<span data-ttu-id="6aee3-170">실행 된 `update-database` 명령을 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-170">Run the `update-database` command again.</span></span>

<span data-ttu-id="6aee3-171">(프로덕션 시스템에는 변경한 해당 하위 메서드 이전 데이터베이스 버전으로 돌아가려면 사용 해야 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="6aee3-171">(In a production system you would make corresponding changes to the Down method in case you ever had to use that to go back to the previous database version.</span></span> <span data-ttu-id="6aee3-172">이 자습서에 사용 하지 않습니다 하위 메서드.)</span><span class="sxs-lookup"><span data-stu-id="6aee3-172">For this tutorial you won't be using the Down method.)</span></span>

> [!NOTE]
> <span data-ttu-id="6aee3-173">스키마 변경 하므로 및 데이터를 마이그레이션하는 경우 다른 오류가 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-173">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="6aee3-174">마이그레이션 오류가 발생할 경우 해결할 수 없는, 연결 문자열을 변경 하 여 자습서를 진행할 수 있습니다 합니다 *Web.config* 파일 또는 데이터베이스 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-174">If you get migration errors you can't resolve, you can continue with the tutorial by changing the connection string in the *Web.config* file or by deleting the database.</span></span> <span data-ttu-id="6aee3-175">가장 간단한 방법은 데이터베이스의 이름을 바꾸려면 합니다 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-175">The simplest approach is to rename the database in the *Web.config* file.</span></span> <span data-ttu-id="6aee3-176">다음 예와에서 같이 예를 들어, 데이터베이스 이름을 ContosoUniversity2로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-176">For example, change the database name to ContosoUniversity2 as shown in the following example:</span></span>
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.xml?highlight=2)]
> 
> <span data-ttu-id="6aee3-177">새 데이터베이스에 데이터가 없습니다. 마이그레이션할 및 `update-database` 명령은 오류 없이 완료 될 가능성이 훨씬 더 높습니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-177">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="6aee3-178">데이터베이스를 삭제 하는 방법에 지침은 [Visual Studio 2012에서 데이터베이스를 삭제 하는 방법](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-178">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span> <span data-ttu-id="6aee3-179">이 자습서를 계속 하려면이 방법을 사용 하는 경우이 자습서의 끝에서 배포 단계를 건너뛸 또는 새 사이트 및 데이터베이스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-179">If you take this approach in order to continue with the tutorial, skip the deployment step at the end of this tutorial or deploy to a new site and database.</span></span> <span data-ttu-id="6aee3-180">있습니다 했으므로 된 배포에 이미 동일한 사이트에 대 한 업데이트를 배포 하는 경우 자동 마이그레이션을 실행 하는 경우 EF가 동일한 오류가 받습니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-180">If you deploy an update to the same site you've been deploying to already, EF will get the same error there when it runs migrations automatically.</span></span> <span data-ttu-id="6aee3-181">마이그레이션 오류 문제를 해결 하려는 경우 가장 좋은 리소스는 Entity Framework 포럼 또는 StackOverflow.com 중입니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-181">If you want to troubleshoot a migrations error, the best resource is one of the Entity Framework forums or StackOverflow.com.</span></span>


## <a name="testing"></a><span data-ttu-id="6aee3-182">테스트</span><span class="sxs-lookup"><span data-stu-id="6aee3-182">Testing</span></span>

<span data-ttu-id="6aee3-183">사이트를 실행 하 고 다양 한 페이지를 시도 하세요.</span><span class="sxs-lookup"><span data-stu-id="6aee3-183">Run the site and try various pages.</span></span> <span data-ttu-id="6aee3-184">모든 항목이 이전과 같이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-184">Everything works the same as it did before.</span></span>

<span data-ttu-id="6aee3-185">**서버 탐색기** 확장 **데이터 Connections\SchoolContext** 차례로 **테이블**를 표시 하 고는 **학생** 및 **강사** 테이블 바뀌었습니다를 **Person** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-185">In **Server Explorer,** expand **Data Connections\SchoolContext** and then **Tables**, and you see that the **Student** and **Instructor** tables have been replaced by a **Person** table.</span></span> <span data-ttu-id="6aee3-186">확장 합니다 **Person** 테이블 표시 이어야 하는 데 사용 하는 열 모두에 **학생** 및 **강사** 테이블.</span><span class="sxs-lookup"><span data-stu-id="6aee3-186">Expand the **Person** table and you see that it has all of the columns that used to be in the **Student** and **Instructor** tables.</span></span>

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="6aee3-188">Person 테이블을 마우스 오른쪽 단추로 클릭한 후 **테이블 데이터 표시**를 클릭하여 판별자 열을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-188">Right-click the Person table, and then click **Show Table Data** to see the discriminator column.</span></span>

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="6aee3-189">다음 다이어그램에서는 새 School 데이터베이스의 구조를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-189">The following diagram illustrates the structure of the new School database:</span></span>

![School_database_diagram](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="6aee3-191">Azure에 배포</span><span class="sxs-lookup"><span data-stu-id="6aee3-191">Deploy to Azure</span></span>

<span data-ttu-id="6aee3-192">이 섹션에서는 선택적 완료 해야 **Azure에 앱을 배포** 단원의 [3 부에 정렬, 필터링 및 페이징](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md) 이 자습서 시리즈의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-192">This section requires you to have completed the optional **Deploying the app to Azure** section in [Part 3, Sorting, Filtering, and Paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md) of this tutorial series.</span></span> <span data-ttu-id="6aee3-193">로컬 프로젝트에서 데이터베이스를 삭제 하 여 해결 하는 마이그레이션 오류를 설치한 경우이 단계 건너뛰기 또는 새 사이트 및 데이터베이스를 만들고 새 환경에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-193">If you had migrations errors that you resolved by deleting the database in your local project, skip this step; or create a new site and database, and deploy to the new environment.</span></span>

1. <span data-ttu-id="6aee3-194">Visual studio에서에서 프로젝트를 마우스 오른쪽 단추로 **솔루션 탐색기** 선택한 **게시** 상황에 맞는 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-194">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>  
  
    ![프로젝트 상황에 맞는 메뉴에서 게시](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)
2. <span data-ttu-id="6aee3-196">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-196">Click **Publish**.</span></span>  
  
    ![게시](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)  
  
   <span data-ttu-id="6aee3-198">웹 앱에 기본 브라우저에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-198">The Web app will open in your default browser.</span></span>
3. <span data-ttu-id="6aee3-199">확인을 위해 응용 프로그램을 테스트 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-199">Test the application to verify it's working.</span></span>

    <span data-ttu-id="6aee3-200">실행 하는 페이지는 처음에는 데이터베이스에 액세스, Entity Framework를 실행 하 여 마이그레이션의 모든 `Up` 데이터베이스를 현재 데이터 모델을 사용 하 여 최신 상태로 만드는 데 필요한 메서드.</span><span class="sxs-lookup"><span data-stu-id="6aee3-200">The first time you run a page that accesses the database, the Entity Framework runs all of the migrations `Up` methods required to bring the database up to date with the current data model.</span></span>

## <a name="summary"></a><span data-ttu-id="6aee3-201">요약</span><span class="sxs-lookup"><span data-stu-id="6aee3-201">Summary</span></span>

<span data-ttu-id="6aee3-202">`Person`, `Student` 및 `Instructor` 클래스에 대해 계층당 하나의 테이블 상속을 구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-202">You've implemented table-per-hierarchy inheritance for the `Person`, `Student`, and `Instructor` classes.</span></span> <span data-ttu-id="6aee3-203">이 및 다른 상속 구조에 대 한 자세한 내용은 참조 하세요. [TPT 상속 패턴](https://msdn.microsoft.com/data/jj618293) 하 고 [TPH 상속 패턴](https://msdn.microsoft.com/data/jj618292) MSDN에서.</span><span class="sxs-lookup"><span data-stu-id="6aee3-203">For more information about this and other inheritance structures, see [TPT Inheritance Pattern](https://msdn.microsoft.com/data/jj618293) and [TPH Inheritance Pattern](https://msdn.microsoft.com/data/jj618292) on MSDN.</span></span> <span data-ttu-id="6aee3-204">다음 자습서에서는 다양한 고급 Entity Framework 시나리오를 처리하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-204">In the next tutorial you'll see how to handle a variety of relatively advanced Entity Framework scenarios.</span></span>

<span data-ttu-id="6aee3-205">다른 Entity Framework 리소스에 대 한 링크에서 찾을 수 있습니다 합니다 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6aee3-205">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6aee3-206">[이전](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [다음](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)</span><span class="sxs-lookup"><span data-stu-id="6aee3-206">[Previous](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)</span></span>
