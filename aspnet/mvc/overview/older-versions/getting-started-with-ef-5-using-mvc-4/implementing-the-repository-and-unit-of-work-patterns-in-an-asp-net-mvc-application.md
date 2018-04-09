---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
title: ASP.NET MVC 응용 프로그램 (9 / 10)에서 저장소 및 작업 패턴의 단위 구현 | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: 44761193-04ba-4990-9f90-145d3c10a716
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 1f870b61658686769304a7809bde62e66da3bd0c
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="implementing-the-repository-and-unit-of-work-patterns-in-an-aspnet-mvc-application-9-of-10"></a><span data-ttu-id="4acbc-103">ASP.NET MVC 응용 프로그램 (9 / 10)에서 저장소 및 단위의 작업 패턴 구현</span><span class="sxs-lookup"><span data-stu-id="4acbc-103">Implementing the Repository and Unit of Work Patterns in an ASP.NET MVC Application (9 of 10)</span></span>
====================
<span data-ttu-id="4acbc-104">으로 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="4acbc-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="4acbc-105">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="4acbc-106">Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio 2012를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="4acbc-107">자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4acbc-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="4acbc-108">시작 부분에서 자습서 시리즈를 시작할 수 있습니다 또는 [이 장의 대 한 시작 프로젝트 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 여기에서 시작 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="4acbc-109">해결할 수 없는 문제에 직면 하는 경우 [완료 장 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 문제를 재현 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="4acbc-110">일반적으로 코드 완성 된 코드를 비교 하 여 문제에 솔루션을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="4acbc-111">몇 가지 일반적인 오류 및 해결 하는 방법에 대 한 참조 [오류 및 해결 방법입니다.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="4acbc-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>


<span data-ttu-id="4acbc-112">이전 자습서에서 중복 코드를 줄이기 위해 상속 사용는 `Student` 및 `Instructor` 엔터티 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-112">In the previous tutorial you used inheritance to reduce redundant code in the `Student` and `Instructor` entity classes.</span></span> <span data-ttu-id="4acbc-113">이 자습서에서는 CRUD 작업에 대 한 리포지토리 및 작업 패턴의 단위를 사용 하는 몇 가지 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-113">In this tutorial you'll see some ways to use the repository and unit of work patterns for CRUD operations.</span></span> <span data-ttu-id="4acbc-114">이전 자습서에서와 같이이 중 하나 변경 하면 이미 작성 하지 않고 새 페이지 만들기 페이지와 코드 작동 방식을 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-114">As in the previous tutorial, in this one you'll change the way your code works with pages you already created rather than creating new pages.</span></span>

## <a name="the-repository-and-unit-of-work-patterns"></a><span data-ttu-id="4acbc-115">리포지토리 및 작업 패턴의 단위</span><span class="sxs-lookup"><span data-stu-id="4acbc-115">The Repository and Unit of Work Patterns</span></span>

<span data-ttu-id="4acbc-116">리포지토리 및 작업 패턴의 단위는 데이터 액세스 계층 및 응용 프로그램의 비즈니스 논리 계층 간에 추상화 계층을 만드는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-116">The repository and unit of work patterns are intended to create an abstraction layer between the data access layer and the business logic layer of an application.</span></span> <span data-ttu-id="4acbc-117">이러한 패턴을 구현하면 데이터 저장소의 변경 내용으로부터 응용 프로그램을 격리할 수 있으며 자동화된 단위 테스트 또는 TDD(테스트 중심 개발)를 용이하게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-117">Implementing these patterns can help insulate your application from changes in the data store and can facilitate automated unit testing or test-driven development (TDD).</span></span>

<span data-ttu-id="4acbc-118">이 자습서에서는 각 엔터티 형식에 대 한 저장소 클래스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-118">In this tutorial you'll implement a repository class for each entity type.</span></span> <span data-ttu-id="4acbc-119">에 대 한는 `Student` 리포지토리 인터페이스와 저장소 클래스를 만들어야 하는 엔터티 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-119">For the `Student` entity type you'll create a repository interface and a repository class.</span></span> <span data-ttu-id="4acbc-120">컨트롤러에서 저장소를 인스턴스화하는 경우에 컨트롤러 리포지토리 인터페이스를 구현 하는 모든 개체에 대 한 참조를 받아들일 수 있도록 인터페이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-120">When you instantiate the repository in your controller, you'll use the interface so that the controller will accept a reference to any object that implements the repository interface.</span></span> <span data-ttu-id="4acbc-121">컨트롤러는 웹 서버에서 실행 되 면 Entity Framework와 함께 작동 하는 리포지토리의 받습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-121">When the controller runs under a web server, it receives a repository that works with the Entity Framework.</span></span> <span data-ttu-id="4acbc-122">컨트롤러는 단위 테스트 클래스에서 실행 되 면 메모리 내 컬렉션과 같은 테스트를 쉽게 조작할 수 있는 방식으로 저장 된 데이터와 작동 하는 리포지토리의 받습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-122">When the controller runs under a unit test class, it receives a repository that works with data stored in a way that you can easily manipulate for testing, such as an in-memory collection.</span></span>

<span data-ttu-id="4acbc-123">이 자습서의 뒷부분에 나오는 사용 하면 여러 저장소와에 대 한 작업 클래스의 단위는 `Course` 및 `Department` 엔터티 형식에 `Course` 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-123">Later in the tutorial you'll use multiple repositories and a unit of work class for the `Course` and `Department` entity types in the `Course` controller.</span></span> <span data-ttu-id="4acbc-124">작업 클래스의 단위 모두에서 공유 하는 단일 데이터베이스 컨텍스트 클래스를 만들어 여러 저장소 작업을 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-124">The unit of work class coordinates the work of multiple repositories by creating a single database context class shared by all of them.</span></span> <span data-ttu-id="4acbc-125">자동화 된 단위 테스트를 수행할 수 있게 되기를 원하는 경우 만들고에 대해 수행한 동일한 방식으로 이러한 클래스에 대 한 인터페이스를 사용 하 여는 `Student` 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-125">If you wanted to be able to perform automated unit testing, you'd create and use interfaces for these classes in the same way you did for the `Student` repository.</span></span> <span data-ttu-id="4acbc-126">그러나이 자습서를 간단히 유지 하기 위해 합니다 만들고 인터페이스 없이 이러한 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-126">However, to keep the tutorial simple, you'll create and use these classes without interfaces.</span></span>

<span data-ttu-id="4acbc-127">다음 그림에는 컨트롤러와 하지 리포지토리 또는 작업 패턴의 단위를 전혀 사용에 비해 컨텍스트 클래스 간의 관계를 개념화 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-127">The following illustration shows one way to conceptualize the relationships between the controller and context classes compared to not using the repository or unit of work pattern at all.</span></span>

![Repository_pattern_diagram](https://asp.net/media/2578149/Windows-Live-Writer_8c4963ba1fa3_CE3B_Repository_pattern_diagram_1df790d3-bdf2-4c11-9098-946ddd9cd884.png)

<span data-ttu-id="4acbc-129">이 자습서 시리즈의 단위 테스트를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-129">You won't create unit tests in this tutorial series.</span></span> <span data-ttu-id="4acbc-130">리포지토리 패턴을 사용 하는 MVC 응용 프로그램과 TDD에 대 한 소개를 참조 하십시오. [연습: ASP.NET MVC와 함께 TDD를 사용 하 여](https://msdn.microsoft.com/library/ff847525.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-130">For an introduction to TDD with an MVC application that uses the repository pattern, see [Walkthrough: Using TDD with ASP.NET MVC](https://msdn.microsoft.com/library/ff847525.aspx).</span></span> <span data-ttu-id="4acbc-131">리포지토리 패턴에 대 한 자세한 내용은 다음 리소스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-131">For more information about the repository pattern, see the following resources:</span></span>

- <span data-ttu-id="4acbc-132">[리포지토리 패턴](https://msdn.microsoft.com/library/ff649690.aspx) msdn 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-132">[The Repository Pattern](https://msdn.microsoft.com/library/ff649690.aspx) on MSDN.</span></span>
- <span data-ttu-id="4acbc-133">[작업 단위 및 저장소 패턴을 사용 하 여 Entity Framework 4.0이 있는](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx) Entity Framework 팀 블로그.</span><span class="sxs-lookup"><span data-stu-id="4acbc-133">[Using Repository and Unit of Work patterns with Entity Framework 4.0](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx) on the Entity Framework team blog.</span></span>
- <span data-ttu-id="4acbc-134">[Agile Entity Framework 4 리포지토리](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/) 일련의 Julie Lerman 블로그 게시물입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-134">[Agile Entity Framework 4 Repository](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/) series of posts on Julie Lerman's blog.</span></span>
- <span data-ttu-id="4acbc-135">[작성 한 눈에 보기 HTML5/jQuery 응용 프로그램에서 계정을](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx) Dan Wahlin 블로그.</span><span class="sxs-lookup"><span data-stu-id="4acbc-135">[Building the Account at a Glance HTML5/jQuery Application](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx) on Dan Wahlin's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="4acbc-136">저장소와 단위 작업 패턴을 구현 하는 방법은 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-136">There are many ways to implement the repository and unit of work patterns.</span></span> <span data-ttu-id="4acbc-137">작업 클래스의 단위 유무 저장소 클래스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-137">You can use repository classes with or without a unit of work class.</span></span> <span data-ttu-id="4acbc-138">각 형식에 대 한 하나 또는 모든 엔터티 형식에 대 한 단일 저장소를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-138">You can implement a single repository for all entity types, or one for each type.</span></span> <span data-ttu-id="4acbc-139">각 형식에 대해 하나를 구현 하는 경우에 별도 클래스, 제네릭 기본 클래스 및 파생된 클래스 또는 추상 기본 클래스 및 파생 된 클래스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-139">If you implement one for each type, you can use separate classes, a generic base class and derived classes, or an abstract base class and derived classes.</span></span> <span data-ttu-id="4acbc-140">저장소에 비즈니스 논리를 포함 하거나 데이터 액세스 논리를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-140">You can include business logic in your repository or restrict it to data access logic.</span></span> <span data-ttu-id="4acbc-141">사용 하 여 데이터베이스 컨텍스트 클래스를 추상 계층을 작성할 수 있습니다 [IDbSet](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx) 대신 있습니다 인터페이스 [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) 엔터티 집합에 대 한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-141">You can also build an abstraction layer into your database context class by using [IDbSet](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx) interfaces there instead of [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) types for your entity sets.</span></span> <span data-ttu-id="4acbc-142">이 자습서에서 설명 하는 추상화 계층 구현 하는 방법에는 모든 시나리오 및 환경에 대 한 권장 하지를 고려 하는 한 가지 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-142">The approach to implementing an abstraction layer shown in this tutorial is one option for you to consider, not a recommendation for all scenarios and environments.</span></span>


## <a name="creating-the-student-repository-class"></a><span data-ttu-id="4acbc-143">학생 저장소 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="4acbc-143">Creating the Student Repository Class</span></span>

<span data-ttu-id="4acbc-144">에 *DAL* 폴더를 라는 클래스 파일을 만들 *IStudentRepository.cs* 기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-144">In the *DAL* folder, create a class file named *IStudentRepository.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="4acbc-145">이 코드는 일반적인 집합 두 읽기 메서드를 포함 하 여 CRUD 메서드의 선언-모두 반환 하는 하나 `Student` 엔터티 및 단일 발견 된 `Student` 엔터티 id</span><span class="sxs-lookup"><span data-stu-id="4acbc-145">This code declares a typical set of CRUD methods, including two read methods — one that returns all `Student` entities, and one that finds a single `Student` entity by ID.</span></span>

<span data-ttu-id="4acbc-146">에 *DAL* 폴더 라는 클래스 파일을 만들어 *StudentRepository.cs* 파일.</span><span class="sxs-lookup"><span data-stu-id="4acbc-146">In the *DAL* folder, create a class file named *StudentRepository.cs* file.</span></span> <span data-ttu-id="4acbc-147">기존 코드를 구현 하는 다음 코드로 대체는 `IStudentRepository` 인터페이스:</span><span class="sxs-lookup"><span data-stu-id="4acbc-147">Replace the existing code with the following code, which implements the `IStudentRepository` interface:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="4acbc-148">데이터베이스 컨텍스트 클래스 변수에 정의 된 인스턴스 컨텍스트를 전달 하려면 호출 하는 개체의 생성자에 인수가 및:</span><span class="sxs-lookup"><span data-stu-id="4acbc-148">The database context is defined in a class variable, and the constructor expects the calling object to pass in an instance of the context:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="4acbc-149">저장소에 대 한 새 컨텍스트를 인스턴스화할 수 있지만 다음 컨트롤러 하나에 여러 저장소를 사용 하는 경우 각 결국에 별도 컨텍스트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-149">You could instantiate a new context in the repository, but then if you used multiple repositories in one controller, each would end up with a separate context.</span></span> <span data-ttu-id="4acbc-150">나중에 여러 저장소 사용의 `Course` 컨트롤러를 확인할 수 어떻게 작업 클래스의 단위 모든 저장소 동일한 컨텍스트를 사용 되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-150">Later you'll use multiple repositories in the `Course` controller, and you'll see how a unit of work class can ensure that all repositories use the same context.</span></span>

<span data-ttu-id="4acbc-151">저장소 구현 [IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx) 하 고 컨트롤러의 앞부분에 언급 했 고 해당 CRUD 메서드 이전에 본 것과 동일한 방식에서 데이터베이스 컨텍스트를 호출 하기에 데이터베이스 컨텍스트를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-151">The repository implements [IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx) and disposes the database context as you saw earlier in the controller, and its CRUD methods make calls to the database context in the same way that you saw earlier.</span></span>

## <a name="change-the-student-controller-to-use-the-repository"></a><span data-ttu-id="4acbc-152">리포지토리를 사용 하도록 학생 컨트롤러 변경</span><span class="sxs-lookup"><span data-stu-id="4acbc-152">Change the Student Controller to Use the Repository</span></span>

<span data-ttu-id="4acbc-153">*StudentController.cs*, 클래스의 현재 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-153">In *StudentController.cs*, replace the code currently in the class with the following code.</span></span> <span data-ttu-id="4acbc-154">변경 내용은 강조 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-154">The changes are highlighted.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=13-18,44,75,77,102-103,120,137-138,159,172-174,186)]

<span data-ttu-id="4acbc-155">컨트롤러 구현 하는 개체에 대 한 클래스 변수를 선언 이제는 `IStudentRepository` 컨텍스트 클래스 대신 인터페이스:</span><span class="sxs-lookup"><span data-stu-id="4acbc-155">The controller now declares a class variable for an object that implements the `IStudentRepository` interface instead of the context class:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample5.cs)]

<span data-ttu-id="4acbc-156">기본 (매개 변수가 없는) 생성자 새 컨텍스트 인스턴스를 만들고 선택적 생성자 컨텍스트 인스턴스에서 전달 하려면 호출자가 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-156">The default (parameterless) constructor creates a new context instance, and an optional constructor allows the caller to pass in a context instance.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="4acbc-157">(사용 중 이었다 면 *종속성 주입*, DI를 사용할 필요는 기본 생성자는 DI 소프트웨어는 올바른 리포지토리 개체 제공 되는 항상 있으므로 또는.)</span><span class="sxs-lookup"><span data-stu-id="4acbc-157">(If you were using *dependency injection*, or DI, you wouldn't need the default constructor because the DI software would ensure that the correct repository object would always be provided.)</span></span>

<span data-ttu-id="4acbc-158">CRUD 메서드 저장소 이제 컨텍스트 대신 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-158">In the CRUD methods, the repository is now called instead of the context:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample7.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample8.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample9.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample10.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="4acbc-159">및 `Dispose` 메서드는 이제 컨텍스트 대신 리포지토리를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-159">And the `Dispose` method now disposes the repository instead of the context:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample12.cs)]

<span data-ttu-id="4acbc-160">사이트를 실행 하 고 클릭는 **학생** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-160">Run the site and click the **Students** tab.</span></span>

![Students_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="4acbc-162">페이지 찾아서 저장소를 사용 하도록 코드를 변경 하 고 다른 학생 페이지는 동일 하 게 작동도 마찬가지로 동일 하 게 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-162">The page looks and works the same as it did before you changed the code to use the repository, and the other Student pages also work the same.</span></span> <span data-ttu-id="4acbc-163">그러나 방식에는 중요 한 차이점이 있습니다.는 `Index` 컨트롤러의 메서드는 필터링 및 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-163">However, there's an important difference in the way the `Index` method of the controller does filtering and ordering.</span></span> <span data-ttu-id="4acbc-164">이 방법의 원래 버전에는 다음 코드 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-164">The original version of this method contained the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample13.cs?highlight=1)]

<span data-ttu-id="4acbc-165">업데이트 된 `Index` 메서드에 다음 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-165">The updated `Index` method contains the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=1)]

<span data-ttu-id="4acbc-166">강조 표시 된 코드에만 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-166">Only the highlighted code has changed.</span></span>

<span data-ttu-id="4acbc-167">코드의 원래 버전에 `students` 로 형식화 되는 `IQueryable` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-167">In the original version of the code, `students` is typed as an `IQueryable` object.</span></span> <span data-ttu-id="4acbc-168">쿼리는 같은 메서드를 사용 하 여 컬렉션으로 변환 될 때까지 데이터베이스에 전송 되지 않고 `ToList`, 인덱스 뷰 학생 모델에 액세스 될 때까지 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-168">The query isn't sent to the database until it's converted into a collection using a method such as `ToList`, which doesn't occur until the Index view accesses the student model.</span></span> <span data-ttu-id="4acbc-169">`Where` 위의 원본 코드에서 메서드는 `WHERE` 절에서 데이터베이스에 전송 되는 SQL 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-169">The `Where` method in the original code above becomes a `WHERE` clause in the SQL query that is sent to the database.</span></span> <span data-ttu-id="4acbc-170">그러면 데이터베이스에서 선택한 엔터티만 반환 되도록 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-170">That in turn means that only the selected entities are returned by the database.</span></span> <span data-ttu-id="4acbc-171">그러나 변경의 결과로 `context.Students` 를 `studentRepository.GetStudents()`, `students` 문이이 변수는 `IEnumerable` 데이터베이스에서 모든 학생을 포함 하는 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-171">However, as a result of changing `context.Students` to `studentRepository.GetStudents()`, the `students` variable after this statement is an `IEnumerable` collection that includes all students in the database.</span></span> <span data-ttu-id="4acbc-172">적용의 최종 결과 `Where` 메서드는 같지만 완료 이제 웹 서버 및 데이터베이스가 아니라 메모리에 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-172">The end result of applying the `Where` method is the same, but now the work is done in memory on the web server and not by the database.</span></span> <span data-ttu-id="4acbc-173">많은 양의 데이터를 반환 하는 쿼리의 경우이 수 있습니다. 수. 있습니다</span><span class="sxs-lookup"><span data-stu-id="4acbc-173">For queries that return large volumes of data, this can be inefficient.</span></span>

> [!TIP]
> 
> <span data-ttu-id="4acbc-174">**IQueryable vs입니다. IEnumerable**</span><span class="sxs-lookup"><span data-stu-id="4acbc-174">**IQueryable vs. IEnumerable**</span></span>
> 
> <span data-ttu-id="4acbc-175">구현한 후 저장소 여기에 표시 된 대로에 내용을 입력 해야 하는 경우에는 **검색** 상자 SQL 서버로 보내진 쿼리의 검색 조건에 포함 되지 않으므로 모든 학생 행을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-175">After you implement the repository as shown here, even if you enter something in the **Search** box the query sent to SQL Server returns all Student rows because it doesn't include your search criteria:</span></span>
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image2.png)
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample15.sql)]
> 
> <span data-ttu-id="4acbc-176">이 쿼리 저장소는 검색 조건에 대 한 알 필요 없이 쿼리를 실행 하기 때문에 모든 학생 데이터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-176">This query returns all of the student data because the repository executed the query without knowing about the search criteria.</span></span> <span data-ttu-id="4acbc-177">정렬, 검색 조건을 적용 하 고 메모리에서 페이징 (이 경우에 3 행 표시)가 수행에 대 한 데이터의 하위 집합을 선택 하는 과정 뒷부분에 나오는 경우에는 `ToPagedList` 메서드가 호출 되는 `IEnumerable` 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-177">The process of sorting, applying search criteria, and selecting a subset of the data for paging (showing only 3 rows in this case) is done in memory later when the `ToPagedList` method is called on the `IEnumerable` collection.</span></span>
> 
> <span data-ttu-id="4acbc-178">(저장소를 구현 하기) 전에 코드의 이전 버전에서는 쿼리가 보내집니다 될 때까지 데이터베이스에 검색 조건을 적용 한 후 때 `ToPagedList` 라고 하는 `IQueryable` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-178">In the previous version of the code (before you implemented the repository), the query is not sent to the database until after you apply the search criteria, when `ToPagedList` is called on the `IQueryable` object.</span></span>
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image3.png)
> 
> <span data-ttu-id="4acbc-179">ToPagedList에서 호출 될 때는 `IQueryable` 개체를 검색 문자열을 지정 하는 SQL Server로 전송 하는 쿼리 및 결과적으로 검색 조건을 충족 하는 행만 반환 되 고 필터링을 하지 않고 메모리에 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-179">When ToPagedList is called on an `IQueryable` object, the query sent to SQL Server specifies the search string, and as a result only rows that meet the search criteria are returned, and no filtering needs to be done in memory.</span></span>
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample16.sql)]
> 
> <span data-ttu-id="4acbc-180">(다음 자습서에는 SQL Server로 전송 하는 쿼리를 검사 하는 방법을 설명 합니다.)</span><span class="sxs-lookup"><span data-stu-id="4acbc-180">(The following tutorial explains how to examine queries sent to SQL Server.)</span></span>


<span data-ttu-id="4acbc-181">다음 섹션에는 데이터베이스에서이 작업을 수행 해야 지정할 수 있습니다 사용할 수 있는 저장소 메서드를 구현 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-181">The following section shows how to implement repository methods that enable you to specify that this work should be done by the database.</span></span>

<span data-ttu-id="4acbc-182">이제 컨트롤러와 Entity Framework 데이터베이스 컨텍스트 간에 추상화 계층을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-182">You've now created an abstraction layer between the controller and the Entity Framework database context.</span></span> <span data-ttu-id="4acbc-183">이 응용 프로그램을 사용 하 여 테스트 하는 자동화 된 단위를 수행 하려는 만들 수 있습니다는 대체 저장소 클래스를 구현 하는 단위 테스트 프로젝트에서 `IStudentRepository` *합니다.*</span><span class="sxs-lookup"><span data-stu-id="4acbc-183">If you were going to perform automated unit testing with this application, you could create an alternative repository class in a unit test project that implements `IStudentRepository`*.*</span></span> <span data-ttu-id="4acbc-184">컨텍스트 데이터 읽기 및 쓰기를 호출 하는 대신이 모의 리포지토리 클래스 컨트롤러 함수를 테스트 하기 위해 메모리 내 컬렉션을 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-184">Instead of calling the context to read and write data, this mock repository class could manipulate in-memory collections in order to test controller functions.</span></span>

## <a name="implement-a-generic-repository-and-a-unit-of-work-class"></a><span data-ttu-id="4acbc-185">일반 저장소 및 작업 클래스의 단위를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-185">Implement a Generic Repository and a Unit of Work Class</span></span>

<span data-ttu-id="4acbc-186">중복 코드를 많이 발생할 수 있습니다 각 엔터티 형식에 대 한 저장소 클래스를 만드는 있으며 부분적으로 업데이트 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-186">Creating a repository class for each entity type could result in a lot of redundant code, and it could result in partial updates.</span></span> <span data-ttu-id="4acbc-187">예를 들어, 동일한 트랜잭션의 일부로 두 개의 서로 다른 형식의 엔터티를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-187">For example, suppose you have to update two different entity types as part of the same transaction.</span></span> <span data-ttu-id="4acbc-188">별도 데이터베이스 컨텍스트 인스턴스를 사용 하며 각 하나에 성공 하 고 다른 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-188">If each uses a separate database context instance, one might succeed and the other might fail.</span></span> <span data-ttu-id="4acbc-189">코드가 중복을 최소화 하는 한 가지 방법은 일반 저장소 및 확인 하는 방법을 사용 하는 모든 저장소 동일한 데이터베이스 컨텍스트를 사용 하 여 (및 따라서 모든 업데이트를 조정할)은 작업 클래스의 단위를 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-189">One way to minimize redundant code is to use a generic repository, and one way to ensure that all repositories use the same database context (and thus coordinate all updates) is to use a unit of work class.</span></span>

<span data-ttu-id="4acbc-190">자습서의이 섹션에서는 만듭니다는 `GenericRepository` 클래스 및 `UnitOfWork` 클래스에 사용 하 고는 `Course` 둘 다에 액세스 하기 위해 컨트롤러는 `Department` 및 `Course` 엔터티 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-190">In this section of the tutorial, you'll create a `GenericRepository` class and a `UnitOfWork` class, and use them in the `Course` controller to access both the `Department` and the `Course` entity sets.</span></span> <span data-ttu-id="4acbc-191">이전에 설명한 대로 자습서의이 부분을 간단 하 이러한 클래스에 대 한 인터페이스 만들기 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-191">As explained earlier, to keep this part of the tutorial simple, you aren't creating interfaces for these classes.</span></span> <span data-ttu-id="4acbc-192">TDD를 용이 하 게 사용법이 바뀔 때, 사용자는 일반적으로 구현는 인터페이스와 수행한 것과 동일한 방식으로 `Student` 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-192">But if you were going to use them to facilitate TDD, you'd typically implement them with interfaces the same way you did the `Student` repository.</span></span>

### <a name="create-a-generic-repository"></a><span data-ttu-id="4acbc-193">제네릭 리포지토리 만들기</span><span class="sxs-lookup"><span data-stu-id="4acbc-193">Create a Generic Repository</span></span>

<span data-ttu-id="4acbc-194">에 *DAL* 폴더를 만들 *GenericRepository.cs* 기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-194">In the *DAL* folder, create *GenericRepository.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample17.cs)]

<span data-ttu-id="4acbc-195">데이터베이스 컨텍스트에 대 한 및 저장소를 위해 인스턴스화되는 엔터티 집합에 대 한 클래스 변수 선언 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-195">Class variables are declared for the database context and for the entity set that the repository is instantiated for:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample18.cs)]

<span data-ttu-id="4acbc-196">생성자는 데이터베이스 컨텍스트 인스턴스를 허용 하 고 엔터티 집합 변수를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-196">The constructor accepts a database context instance and initializes the entity set variable:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample19.cs)]

<span data-ttu-id="4acbc-197">`Get` 방법은 람다 식을 사용 하 여 필터 조건 및 by, 결과 정렬 하려면 열을 지정 하려면 호출 코드에서 및 문자열 매개 변수를 사용 하면 즉시 로드에 대 한 쉼표로 구분 된 탐색 속성 목록이 제공 호출자에 게 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-197">The `Get` method uses lambda expressions to allow the calling code to specify a filter condition and a column to order the results by, and a string parameter lets the caller provide a comma-delimited list of navigation properties for eager loading:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample20.cs)]

<span data-ttu-id="4acbc-198">코드 `Expression<Func<TEntity, bool>> filter` 호출자에 게는 람다 식에 따라 제공 의미는 `TEntity` 형식과이 식은 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-198">The code `Expression<Func<TEntity, bool>> filter` means the caller will provide a lambda expression based on the `TEntity` type, and this expression will return a Boolean value.</span></span> <span data-ttu-id="4acbc-199">예를 들어 저장소를 위해 인스턴스화되는 `Student` 엔터티 형식에 메서드 호출에서 코드를 지정할 수 있습니다 `student => student.LastName == "Smith` &quot; 에 대 한는 `filter` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-199">For example, if the repository is instantiated for the `Student` entity type, the code in the calling method might specify `student => student.LastName == "Smith`&quot; for the `filter` parameter.</span></span>

<span data-ttu-id="4acbc-200">코드 `Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy` 호출자에 게는 람다 식을 제공 함을 의미 하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-200">The code `Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy` also means the caller will provide a lambda expression.</span></span> <span data-ttu-id="4acbc-201">하지만 경우 식에 대 한 입력은 한 `IQueryable` 개체에 대 한는 `TEntity` 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-201">But in this case, the input to the expression is an `IQueryable` object for the `TEntity` type.</span></span> <span data-ttu-id="4acbc-202">식은 순서가 지정 된 버전에 반환 됩니다 `IQueryable` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-202">The expression will return an ordered version of that `IQueryable` object.</span></span> <span data-ttu-id="4acbc-203">예를 들어 저장소를 위해 인스턴스화되는 `Student` 엔터티 형식에 메서드 호출에서 코드를 지정할 수 있습니다 `q => q.OrderBy(s => s.LastName)` 에 대 한는 `orderBy` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-203">For example, if the repository is instantiated for the `Student` entity type, the code in the calling method might specify `q => q.OrderBy(s => s.LastName)` for the `orderBy` parameter.</span></span>

<span data-ttu-id="4acbc-204">코드는 `Get` 메서드 만듭니다는 `IQueryable` 를 있는 경우 필터 식을 적용 하는 개체:</span><span class="sxs-lookup"><span data-stu-id="4acbc-204">The code in the `Get` method creates an `IQueryable` object and then applies the filter expression if there is one:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample21.cs)]

<span data-ttu-id="4acbc-205">그런 다음 쉼표로 구분 된 목록 구분 분석 후 eager 로드 식을 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-205">Next it applies the eager-loading expressions after parsing the comma-delimited list:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample22.cs)]

<span data-ttu-id="4acbc-206">마지막으로 적용 되는 `orderBy` 식이 있는 경우; 결과 반환 하 고 그렇지 않으면 결과 정렬 되지 않은 쿼리에서 반환:</span><span class="sxs-lookup"><span data-stu-id="4acbc-206">Finally, it applies the `orderBy` expression if there is one and returns the results; otherwise it returns the results from the unordered query:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample23.cs)]

<span data-ttu-id="4acbc-207">호출 하는 경우는 `Get` 메서드, 필터링 및 정렬을 수행할 수 있습니다는 `IEnumerable` 이러한 함수에 대 한 매개 변수를 제공 하는 대신 메서드에 의해 반환 된 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-207">When you call the `Get` method, you could do filtering and sorting on the `IEnumerable` collection returned by the method instead of providing parameters for these functions.</span></span> <span data-ttu-id="4acbc-208">하지만 정렬 하 고 작업을 필터링 한 다음 수행 웹 서버의 메모리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-208">But the sorting and filtering work would then be done in memory on the web server.</span></span> <span data-ttu-id="4acbc-209">이러한 매개 변수를 사용 하 여 웹 서버 대신 데이터베이스에서 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-209">By using these parameters, you ensure that the work is done by the database rather than the web server.</span></span> <span data-ttu-id="4acbc-210">특정 엔터티 형식에 대 한 파생된 클래스를 만들어 특수 추가 하는 대체 항목은 `Get` 메서드 같은 `GetStudentsInNameOrder` 또는 `GetStudentsByName`합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-210">An alternative is to create derived classes for specific entity types and add specialized `Get` methods, such as `GetStudentsInNameOrder` or `GetStudentsByName`.</span></span> <span data-ttu-id="4acbc-211">그러나 복잡 한 응용 프로그램을이 발생할 수 있습니다 이러한 파생 된 클래스 및 유지 하기 위해 더 많은 작업이 될 수 있는 특별 한 방법을 많은 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-211">However, in a complex application, this can result in a large number of such derived classes and specialized methods, which could be more work to maintain.</span></span>

<span data-ttu-id="4acbc-212">코드는 `GetByID`, `Insert`, 및 `Update` 메서드가 제네릭이 아닌 저장소에 확인 했던 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-212">The code in the `GetByID`, `Insert`, and `Update` methods is similar to what you saw in the non-generic repository.</span></span> <span data-ttu-id="4acbc-213">(를 즉시 로드 매개 변수로 제공 되지 않습니다는 `GetByID` 서명을 할 수 없습니다 즉시 로드 때문에 `Find` 메서드.)</span><span class="sxs-lookup"><span data-stu-id="4acbc-213">(You aren't providing an eager loading parameter in the `GetByID` signature, because you can't do eager loading with the `Find` method.)</span></span>

<span data-ttu-id="4acbc-214">두 오버 로드에 제공 되는 `Delete` 메서드:</span><span class="sxs-lookup"><span data-stu-id="4acbc-214">Two overloads are provided for the `Delete` method:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample24.cs)]

<span data-ttu-id="4acbc-215">삭제할 엔터티 ID만 전달이 사용 중 및 엔터티 인스턴스를 사용 하는 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-215">One of these lets you pass in just the ID of the entity to be deleted, and one takes an entity instance.</span></span> <span data-ttu-id="4acbc-216">볼 수 있듯이 [동시성 처리](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) 동시성 처리 하기 위해 자습서는 `Delete` 엔터티 인스턴스를 사용 하는 메서드에 추적 속성의 원래 값을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-216">As you saw in the [Handling Concurrency](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial, for concurrency handling you need a `Delete` method that takes an entity instance that includes the original value of a tracking property.</span></span>

<span data-ttu-id="4acbc-217">이 제네릭 리포지토리 CRUD 한 일반적인 요구 사항을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-217">This generic repository will handle typical CRUD requirements.</span></span> <span data-ttu-id="4acbc-218">특정 엔터티 형식에 특별 한 요구 사항이 보다 복잡 한 필터링 등 순서를 지정 하는 경우에 해당 형식에 대 한 추가 메서드가 파생된 클래스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-218">When a particular entity type has special requirements, such as more complex filtering or ordering, you can create a derived class that has additional methods for that type.</span></span>

## <a name="creating-the-unit-of-work-class"></a><span data-ttu-id="4acbc-219">작업 클래스의 단위를 만들기</span><span class="sxs-lookup"><span data-stu-id="4acbc-219">Creating the Unit of Work Class</span></span>

<span data-ttu-id="4acbc-220">작업 클래스의 단위 한 목적을 갖습니다: 고유 하도록 여러 저장소를 사용 하는 경우, 단일 데이터베이스 컨텍스트 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-220">The unit of work class serves one purpose: to make sure that when you use multiple repositories, they share a single database context.</span></span> <span data-ttu-id="4acbc-221">이런 방식으로 작업 단위의 완료 되 면 호출할 수 있습니다는 `SaveChanges` 컨텍스트의 해당 인스턴스에서 메서드는 관련 된 모든 변경 내용이 조정 될 것을 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-221">That way, when a unit of work is complete you can call the `SaveChanges` method on that instance of the context and be assured that all related changes will be coordinated.</span></span> <span data-ttu-id="4acbc-222">요구 사항 클래스는 모든 작업을 한 `Save` 메서드와 각 저장소에 대 한 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-222">All that the class needs is a `Save` method and a property for each repository.</span></span> <span data-ttu-id="4acbc-223">각 저장소 속성에는 동일한 컨텍스트 인스턴스에 데이터베이스를 사용 하 여 다른 저장소 인스턴스와 인스턴스화되어 저장소 인스턴스를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-223">Each repository property returns a repository instance that has been instantiated using the same database context instance as the other repository instances.</span></span>

<span data-ttu-id="4acbc-224">에 *DAL* 폴더를 라는 클래스 파일을 만들 *UnitOfWork.cs* 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-224">In the *DAL* folder, create a class file named *UnitOfWork.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample25.cs)]

<span data-ttu-id="4acbc-225">코드는 데이터베이스 컨텍스트 및 각 저장소에 대 한 클래스 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-225">The code creates class variables for the database context and each repository.</span></span> <span data-ttu-id="4acbc-226">에 대 한는 `context` 변수에 대 한 새 컨텍스트 인스턴스화됩니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-226">For the `context` variable, a new context is instantiated:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample26.cs)]

<span data-ttu-id="4acbc-227">각 저장소 속성 저장소 이미 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-227">Each repository property checks whether the repository already exists.</span></span> <span data-ttu-id="4acbc-228">그렇지 않은 경우 리포지토리 상황에 맞는 인스턴스 전달를 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-228">If not, it instantiates the repository, passing in the context instance.</span></span> <span data-ttu-id="4acbc-229">결과적으로, 모든 저장소 동일한 컨텍스트 인스턴스에 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-229">As a result, all repositories share the same context instance.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample27.cs)]

<span data-ttu-id="4acbc-230">`Save` 메서드 호출 `SaveChanges` 데이터베이스 컨텍스트에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-230">The `Save` method calls `SaveChanges` on the database context.</span></span>

<span data-ttu-id="4acbc-231">클래스 변수에 데이터베이스 컨텍스트를 인스턴스화하는 모든 클래스와 마찬가지로 `UnitOfWork` 클래스 구현 `IDisposable` 컨텍스트를 삭제 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-231">Like any class that instantiates a database context in a class variable, the `UnitOfWork` class implements `IDisposable` and disposes the context.</span></span>

### <a name="changing-the-course-controller-to-use-the-unitofwork-class-and-repositories"></a><span data-ttu-id="4acbc-232">UnitOfWork 클래스와 리포지토리로 사용 하는 과정 컨트롤러 변경</span><span class="sxs-lookup"><span data-stu-id="4acbc-232">Changing the Course Controller to use the UnitOfWork Class and Repositories</span></span>

<span data-ttu-id="4acbc-233">에 현재 있는 코드 대체 *CourseController.cs* 를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="4acbc-233">Replace the code you currently have in *CourseController.cs* with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample28.cs?highlight=15,20,22,31,54-55,70,85-86,101-102,122-124,130)]

<span data-ttu-id="4acbc-234">이 코드에 대 한 클래스 변수를 추가 하는 `UnitOfWork` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-234">This code adds a class variable for the `UnitOfWork` class.</span></span> <span data-ttu-id="4acbc-235">(여기에 변수를 초기화 하지 인터페이스를 여기서 사용 된 경우;에 대해 수행한 것 처럼 두 명의 생성자의 패턴을 구현 합니다 대신는 `Student` 저장소.)</span><span class="sxs-lookup"><span data-stu-id="4acbc-235">(If you were using interfaces here, you wouldn't initialize the variable here; instead, you'd implement a pattern of two constructors just as you did for the `Student` repository.)</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample29.cs)]

<span data-ttu-id="4acbc-236">클래스의 나머지 부분에서는 데이터베이스 컨텍스트에 대 한 모든 참조 바뀝니다 적절 한 저장소에 대 한 참조를 사용 하 여 `UnitOfWork` 저장소에 액세스 하는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-236">In the rest of the class, all references to the database context are replaced by references to the appropriate repository, using `UnitOfWork` properties to access the repository.</span></span> <span data-ttu-id="4acbc-237">`Dispose` 메서드를 삭제는 `UnitOfWork` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="4acbc-237">The `Dispose` method disposes the `UnitOfWork` instance.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample30.cs)]

<span data-ttu-id="4acbc-238">사이트를 실행 하 고 클릭는 **Courses** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-238">Run the site and click the **Courses** tab.</span></span>

![Courses_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="4acbc-240">페이지 찾아서 변경 내용을 전과 다른 과정 페이지는 동일 하 게 작동도 동일 하 게 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-240">The page looks and works the same as it did before your changes, and the other Course pages also work the same.</span></span>

## <a name="summary"></a><span data-ttu-id="4acbc-241">요약</span><span class="sxs-lookup"><span data-stu-id="4acbc-241">Summary</span></span>

<span data-ttu-id="4acbc-242">저장소와 단위 작업 패턴을 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-242">You have now implemented both the repository and unit of work patterns.</span></span> <span data-ttu-id="4acbc-243">일반 저장소에서 메서드 매개 변수로 람다 식을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-243">You have used lambda expressions as method parameters in the generic repository.</span></span> <span data-ttu-id="4acbc-244">함께 이러한 식을 사용 하는 방법에 대 한 자세한 내용은 `IQueryable` 개체, 참조 [IQueryable(T) 인터페이스 (System.Linq)](https://msdn.microsoft.com/library/bb351562.aspx) MSDN 라이브러리에서.</span><span class="sxs-lookup"><span data-stu-id="4acbc-244">For more information about how to use these expressions with an `IQueryable` object, see [IQueryable(T) Interface (System.Linq)](https://msdn.microsoft.com/library/bb351562.aspx) in the MSDN Library.</span></span> <span data-ttu-id="4acbc-245">다음에서 자습서 일부를 처리 하는 방법을 알아봅니다 고급 시나리오를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-245">In the next tutorial you'll learn how to handle some advanced scenarios.</span></span>

<span data-ttu-id="4acbc-246">다른 Entity Framework 리소스에 대 한 링크에서 확인할 수 있습니다는 [ASP.NET 데이터 액세스 콘텐츠 맵](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4acbc-246">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4acbc-247">[이전](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [다음](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)</span><span class="sxs-lookup"><span data-stu-id="4acbc-247">[Previous](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)</span></span>
