---
title: ASP.NET Core에서 razor 페이지 단위 테스트
author: guardrex
description: Razor 페이지 앱에 대 한 단위 테스트를 만드는 방법에 알아봅니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 11/27/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: test/razor-pages-tests
ms.openlocfilehash: df74d8e44b2dff00e76139edba47fd8a30ce33ef
ms.sourcegitcommit: 63fb07fb3f71b32daf2c9466e132f2e7cc617163
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/10/2018
ms.locfileid: "35252307"
---
# <a name="razor-pages-unit-tests-in-aspnet-core"></a><span data-ttu-id="56cb1-103">ASP.NET Core에서 razor 페이지 단위 테스트</span><span class="sxs-lookup"><span data-stu-id="56cb1-103">Razor Pages unit tests in ASP.NET Core</span></span>

<span data-ttu-id="56cb1-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="56cb1-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="56cb1-105">ASP.NET Core Razor 페이지 응용 프로그램의 단위 테스트를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-105">ASP.NET Core supports unit tests of Razor Pages apps.</span></span> <span data-ttu-id="56cb1-106">테스트 데이터의 DAL (계층)에 액세스 하 고 페이지 모델 보장할 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-106">Tests of the data access layer (DAL) and page models help ensure:</span></span>

* <span data-ttu-id="56cb1-107">Razor 페이지 앱의 일부 응용 프로그램 생성 하는 동안 하나의 단위로 독립적으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-107">Parts of a Razor Pages app work independently and together as a unit during app construction.</span></span>
* <span data-ttu-id="56cb1-108">클래스 및 메서드 책임 범위 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-108">Classes and methods have limited scopes of responsibility.</span></span>
* <span data-ttu-id="56cb1-109">추가 설명서는 응용 프로그램 동작 방식에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-109">Additional documentation exists on how the app should behave.</span></span>
* <span data-ttu-id="56cb1-110">자동화 된 빌드 및 배포 하는 동안 재발 코드를 업데이트 하 여에 대 한 상태가 오류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-110">Regressions, which are errors brought about by updates to the code, are found during automated building and deployment.</span></span>

<span data-ttu-id="56cb1-111">이 항목에서는 Razor 페이지 앱 및 단위 테스트에 대 한 기본적인 이해 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-111">This topic assumes that you have a basic understanding of Razor Pages apps and unit tests.</span></span> <span data-ttu-id="56cb1-112">Razor 페이지 응용 프로그램 또는 테스트 개념 잘 모르는 경우 다음 항목을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-112">If you're unfamiliar with Razor Pages apps or test concepts, see the following topics:</span></span>

* [<span data-ttu-id="56cb1-113">Razor 페이지 소개</span><span class="sxs-lookup"><span data-stu-id="56cb1-113">Introduction to Razor Pages</span></span>](xref:mvc/razor-pages/index)
* [<span data-ttu-id="56cb1-114">Razor 페이지 시작</span><span class="sxs-lookup"><span data-stu-id="56cb1-114">Get started with Razor Pages</span></span>](xref:tutorials/razor-pages/razor-pages-start)
* [<span data-ttu-id="56cb1-115">에서 단위 테스트 C#.NET Core dotnet 테스트, xUnit를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="56cb1-115">Unit testing C# in .NET Core using dotnet test and xUnit</span></span>](/dotnet/articles/core/testing/unit-testing-with-dotnet-test)

<span data-ttu-id="56cb1-116">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/razor-pages-tests/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="56cb1-116">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/razor-pages-tests/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="56cb1-117">샘플 프로젝트에는 두 응용 프로그램이 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-117">The sample project is composed of two apps:</span></span>

| <span data-ttu-id="56cb1-118">앱</span><span class="sxs-lookup"><span data-stu-id="56cb1-118">App</span></span>         | <span data-ttu-id="56cb1-119">프로젝트 폴더</span><span class="sxs-lookup"><span data-stu-id="56cb1-119">Project folder</span></span>                        | <span data-ttu-id="56cb1-120">설명</span><span class="sxs-lookup"><span data-stu-id="56cb1-120">Description</span></span> |
| ----------- | ------------------------------------- | ----------- |
| <span data-ttu-id="56cb1-121">응용 프로그램 메시지</span><span class="sxs-lookup"><span data-stu-id="56cb1-121">Message app</span></span> | <span data-ttu-id="56cb1-122">*src/RazorPagesTestSample*</span><span class="sxs-lookup"><span data-stu-id="56cb1-122">*src/RazorPagesTestSample*</span></span>            | <span data-ttu-id="56cb1-123">추가, 하나를 삭제 하 고, all, 삭제 하 고 메시지를 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-123">Allows a user to add, delete one, delete all, and analyze messages.</span></span> |
| <span data-ttu-id="56cb1-124">응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="56cb1-124">Test app</span></span>    | <span data-ttu-id="56cb1-125">*tests/RazorPagesTestSample.Tests*</span><span class="sxs-lookup"><span data-stu-id="56cb1-125">*tests/RazorPagesTestSample.Tests*</span></span>    | <span data-ttu-id="56cb1-126">단위 테스트 메시지 응용 프로그램에 사용 되는: DAL (계층) 및 인덱스 페이지 모델 데이터에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-126">Used to unit test the message app: Data access layer (DAL) and Index page model.</span></span> |

<span data-ttu-id="56cb1-127">와 같은 IDE의 기본 제공 테스트 기능을 사용 하는 테스트를 실행할 수 있습니다 [Visual Studio](https://www.visualstudio.com/vs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-127">The tests can be run using the built-in test features of an IDE, such as [Visual Studio](https://www.visualstudio.com/vs/).</span></span> <span data-ttu-id="56cb1-128">사용 하는 경우 [Visual Studio Code](https://code.visualstudio.com/) 또는 명령줄에서 명령 프롬프트에서 다음 명령을 실행 하는 *tests/RazorPagesTestSample.Tests* 폴더:</span><span class="sxs-lookup"><span data-stu-id="56cb1-128">If using [Visual Studio Code](https://code.visualstudio.com/) or the command line, execute the following command at a command prompt in the *tests/RazorPagesTestSample.Tests* folder:</span></span>

```console
dotnet test
```

## <a name="message-app-organization"></a><span data-ttu-id="56cb1-129">메시지 앱 조직</span><span class="sxs-lookup"><span data-stu-id="56cb1-129">Message app organization</span></span>

<span data-ttu-id="56cb1-130">메시지 앱은 간단한 Razor 페이지 메시지 시스템에서 다음과 같은 특성:</span><span class="sxs-lookup"><span data-stu-id="56cb1-130">The message app is a simple Razor Pages message system with the following characteristics:</span></span>

* <span data-ttu-id="56cb1-131">응용 프로그램의 인덱스 페이지 (*Pages/Index.cshtml* 및 *Pages/Index.cshtml.cs*) UI 및 페이지를 추가, 삭제 및 메시지 (메시지 마다 평균 단어) 분석을 제어 하려면 모델 메서드 제공 .</span><span class="sxs-lookup"><span data-stu-id="56cb1-131">The Index page of the app (*Pages/Index.cshtml* and *Pages/Index.cshtml.cs*) provides a UI and page model methods to control the addition, deletion, and analysis of messages (average words per message).</span></span>
* <span data-ttu-id="56cb1-132">메시지에서 설명 된 `Message` 클래스 (*Data/Message.cs*) 두 개의 속성이 있는: `Id` (키) 및 `Text` (메시지).</span><span class="sxs-lookup"><span data-stu-id="56cb1-132">A message is described by the `Message` class (*Data/Message.cs*) with two properties: `Id` (key) and `Text` (message).</span></span> <span data-ttu-id="56cb1-133">`Text` 속성 인수가 필요 하 고 200 자로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-133">The `Text` property is required and limited to 200 characters.</span></span>
* <span data-ttu-id="56cb1-134">메시지를 사용 하 여 저장 된 [Entity Framework의 메모리 내 데이터베이스](/ef/core/providers/in-memory/)&#8224;합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-134">Messages are stored using [Entity Framework's in-memory database](/ef/core/providers/in-memory/)&#8224;.</span></span>
* <span data-ttu-id="56cb1-135">앱의 데이터베이스 컨텍스트 클래스의 데이터 액세스 계층 (DAL)에 포함 되어 `AppDbContext` (*Data/AppDbContext.cs*).</span><span class="sxs-lookup"><span data-stu-id="56cb1-135">The app contains a data access layer (DAL) in its database context class, `AppDbContext` (*Data/AppDbContext.cs*).</span></span> <span data-ttu-id="56cb1-136">DAL 메서드는 표시 `virtual`, 테스트에서 사용 하기 위해 메서드를 모의 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-136">The DAL methods are marked `virtual`, which allows mocking the methods for use in the tests.</span></span>
* <span data-ttu-id="56cb1-137">데이터베이스 응용 프로그램 시작 시에 비어 있으면 메시지 저장소 세 가지 메시지와 함께 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-137">If the database is empty on app startup, the message store is initialized with three messages.</span></span> <span data-ttu-id="56cb1-138">이러한 *메시지 시드* 테스트에도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-138">These *seeded messages* are also used in tests.</span></span>

<span data-ttu-id="56cb1-139">&#8224;EF 항목 [with InMemory 테스트](/ef/core/miscellaneous/testing/in-memory), MSTest 사용 하 여 테스트에 대 한 메모리 내 데이터베이스를 사용 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-139">&#8224;The EF topic, [Test with InMemory](/ef/core/miscellaneous/testing/in-memory), explains how to use an in-memory database for tests with MSTest.</span></span> <span data-ttu-id="56cb1-140">이 항목에서는 [xUnit](https://xunit.github.io/) 테스트 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-140">This topic uses the [xUnit](https://xunit.github.io/) test framework.</span></span> <span data-ttu-id="56cb1-141">다른 테스트 프레임 워크에서 테스트 구현 및 테스트 개념은 유사 하지만 동일 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-141">Test concepts and test implementations across different test frameworks are similar but not identical.</span></span>

<span data-ttu-id="56cb1-142">응용 프로그램을 사용 하지 않는 있지만 [리포지토리 패턴](http://martinfowler.com/eaaCatalog/repository.html) 와의 효율적인 예가 없습니다는 [작업 단위 (UoW) 패턴](https://martinfowler.com/eaaCatalog/unitOfWork.html), Razor 페이지 개발의 이러한 패턴을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-142">Although the app doesn't use the [repository pattern](http://martinfowler.com/eaaCatalog/repository.html) and isn't an effective example of the [Unit of Work (UoW) pattern](https://martinfowler.com/eaaCatalog/unitOfWork.html), Razor Pages supports these patterns of development.</span></span> <span data-ttu-id="56cb1-143">자세한 내용은 참조 [인프라 지 속성 계층 디자인](/dotnet/standard/microservices-architecture/microservice-ddd-cqrs-patterns/infrastructure-persistence-layer-design), [ASP.NET MVC 응용 프로그램에서 저장소 및 작업 단위 패턴을 구현](/aspnet/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application), 및 [테스트 컨트롤러 논리](/aspnet/core/mvc/controllers/testing) (샘플 리포지토리 패턴을 구현 하는 데 사용).</span><span class="sxs-lookup"><span data-stu-id="56cb1-143">For more information, see [Designing the infrastructure persistence layer](/dotnet/standard/microservices-architecture/microservice-ddd-cqrs-patterns/infrastructure-persistence-layer-design), [Implementing the Repository and Unit of Work Patterns in an ASP.NET MVC Application](/aspnet/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application), and [Test controller logic](/aspnet/core/mvc/controllers/testing) (the sample implements the repository pattern).</span></span>

## <a name="test-app-organization"></a><span data-ttu-id="56cb1-144">조직 앱 테스트</span><span class="sxs-lookup"><span data-stu-id="56cb1-144">Test app organization</span></span>

<span data-ttu-id="56cb1-145">테스트 응용 프로그램은 콘솔 앱 내에서 *tests/RazorPagesTestSample.Tests* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-145">The test app is a console app inside the *tests/RazorPagesTestSample.Tests* folder.</span></span>

| <span data-ttu-id="56cb1-146">테스트 응용 프로그램 폴더</span><span class="sxs-lookup"><span data-stu-id="56cb1-146">Test app folder</span></span> | <span data-ttu-id="56cb1-147">설명</span><span class="sxs-lookup"><span data-stu-id="56cb1-147">Description</span></span> |
| --------------- | ----------- |
| <span data-ttu-id="56cb1-148">*UnitTests*</span><span class="sxs-lookup"><span data-stu-id="56cb1-148">*UnitTests*</span></span>     | <ul><li><span data-ttu-id="56cb1-149">*DataAccessLayerTest.cs* DAL에 대 한 단위 테스트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-149">*DataAccessLayerTest.cs* contains the unit tests for the DAL.</span></span></li><li><span data-ttu-id="56cb1-150">*IndexPageTests.cs* 인덱스 페이지 모델에 대 한 단위 테스트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-150">*IndexPageTests.cs* contains the unit tests for the Index page model.</span></span></li></ul> |
| <span data-ttu-id="56cb1-151">*유틸리티*</span><span class="sxs-lookup"><span data-stu-id="56cb1-151">*Utilities*</span></span>     | <span data-ttu-id="56cb1-152">포함 된 `TestingDbContextOptions` 새 데이터베이스를 만들 각 DAL 단위 테스트에 대 한 상황에 맞는 옵션 데이터베이스를 각 테스트에 대 한 초기 상태로 다시 설정 되도록 사용 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-152">Contains the `TestingDbContextOptions` method used to create new database context options for each DAL unit test so that the database is reset to its baseline condition for each test.</span></span> |

<span data-ttu-id="56cb1-153">테스트 프레임 워크는 [xUnit](https://xunit.github.io/)합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-153">The test framework is [xUnit](https://xunit.github.io/).</span></span> <span data-ttu-id="56cb1-154">프레임 워크를 모의 개체는 [Moq](https://github.com/moq/moq4)합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-154">The object mocking framework is [Moq](https://github.com/moq/moq4).</span></span>

## <a name="unit-tests-of-the-data-access-layer-dal"></a><span data-ttu-id="56cb1-155">데이터의 단위 테스트 DAL (계층)에 액세스</span><span class="sxs-lookup"><span data-stu-id="56cb1-155">Unit tests of the data access layer (DAL)</span></span>

<span data-ttu-id="56cb1-156">메시지가 응용 프로그램에 포함 된 4 가지 방법으로는 DAL에는 `AppDbContext` 클래스 (*src/RazorPagesTestSample/Data/AppDbContext.cs*).</span><span class="sxs-lookup"><span data-stu-id="56cb1-156">The message app has a DAL with four methods contained in the `AppDbContext` class (*src/RazorPagesTestSample/Data/AppDbContext.cs*).</span></span> <span data-ttu-id="56cb1-157">각 메서드에 테스트 응용 프로그램의 하나 또는 두 개의 단위 테스트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-157">Each method has one or two unit tests in the test app.</span></span>

| <span data-ttu-id="56cb1-158">DAL 메서드</span><span class="sxs-lookup"><span data-stu-id="56cb1-158">DAL method</span></span>               | <span data-ttu-id="56cb1-159">기능</span><span class="sxs-lookup"><span data-stu-id="56cb1-159">Function</span></span>                                                                   |
| ------------------------ | -------------------------------------------------------------------------- |
| `GetMessagesAsync`       | <span data-ttu-id="56cb1-160">가져옵니다는 `List<Message>` 기준으로 정렬 하는 데이터베이스에서는 `Text` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-160">Obtains a `List<Message>` from the database sorted by the `Text` property.</span></span> |
| `AddMessageAsync`        | <span data-ttu-id="56cb1-161">추가 `Message` 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-161">Adds a `Message` to the database.</span></span>                                          |
| `DeleteAllMessagesAsync` | <span data-ttu-id="56cb1-162">모든 삭제 `Message` 데이터베이스에서 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-162">Deletes all `Message` entries from the database.</span></span>                           |
| `DeleteMessageAsync`     | <span data-ttu-id="56cb1-163">단일 삭제 `Message` 하 여 데이터베이스에서 `Id`합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-163">Deletes a single `Message` from the database by `Id`.</span></span>                      |

<span data-ttu-id="56cb1-164">DAL의 단위 테스트에 필요한 [DbContextOptions](/dotnet/api/microsoft.entityframeworkcore.dbcontextoptions) 를 새로 만들 때 `AppDbContext` 각 테스트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-164">Unit tests of the DAL require [DbContextOptions](/dotnet/api/microsoft.entityframeworkcore.dbcontextoptions) when creating a new `AppDbContext` for each test.</span></span> <span data-ttu-id="56cb1-165">만드는 한 가지 방법은 `DbContextOptions` 각 테스트를 사용 하는 것을 [DbContextOptionsBuilder](/dotnet/api/microsoft.entityframeworkcore.dbcontextoptionsbuilder):</span><span class="sxs-lookup"><span data-stu-id="56cb1-165">One approach to creating the `DbContextOptions` for each test is to use a [DbContextOptionsBuilder](/dotnet/api/microsoft.entityframeworkcore.dbcontextoptionsbuilder):</span></span>

```csharp
var optionsBuilder = new DbContextOptionsBuilder<AppDbContext>()
    .UseInMemoryDatabase("InMemoryDb");

using (var db = new AppDbContext(optionsBuilder.Options))
{
    // Use the db here in the unit test.
}
```

<span data-ttu-id="56cb1-166">이 방법을 사용이 문제는 각 테스트에서 상태로 이전 테스트 된 상태로 남아 서 데이터베이스를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-166">The problem with this approach is that each test receives the database in whatever state the previous test left it.</span></span> <span data-ttu-id="56cb1-167">서로 간섭 하지 않는 원자성 단위 테스트를 작성 하려고 할 때 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-167">This can be problematic when trying to write atomic unit tests that don't interfere with each other.</span></span> <span data-ttu-id="56cb1-168">강제로 `AppDbContext` 제공할 각 테스트에 대 한 새 데이터베이스 컨텍스트를 사용 하는 `DbContextOptions` 새 서비스 공급자를 기반으로 하는 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="56cb1-168">To force the `AppDbContext` to use a new database context for each test, supply a `DbContextOptions` instance that's based on a new service provider.</span></span> <span data-ttu-id="56cb1-169">테스트 응용 프로그램을 사용 하는 방법을 보여 줍니다 해당 `Utilities` 클래스 메서드에 `TestingDbContextOptions` (*tests/RazorPagesTestSample.Tests/Utilities/Utilities.cs*):</span><span class="sxs-lookup"><span data-stu-id="56cb1-169">The test app shows how to do this using its `Utilities` class method `TestingDbContextOptions` (*tests/RazorPagesTestSample.Tests/Utilities/Utilities.cs*):</span></span>

[!code-csharp[](razor-pages-tests/samples/2.x/tests/RazorPagesTestSample.Tests/Utilities/Utilities.cs?name=snippet1)]

<span data-ttu-id="56cb1-170">사용 하 여 `DbContextOptions` DAL 단위 테스트는 새 데이터베이스 인스턴스와 개별적으로 실행 하려면 각 테스트를 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="56cb1-170">Using the `DbContextOptions` in the DAL unit tests allows each test to run atomically with a fresh database instance:</span></span>

```csharp
using (var db = new AppDbContext(Utilities.TestingDbContextOptions()))
{
    // Use the db here in the unit test.
}
```

<span data-ttu-id="56cb1-171">각 테스트 메서드는 `DataAccessLayerTest` 클래스 (*UnitTests/DataAccessLayerTest.cs*) 정렬 Act Assert 비슷한 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-171">Each test method in the `DataAccessLayerTest` class (*UnitTests/DataAccessLayerTest.cs*) follows a similar Arrange-Act-Assert pattern:</span></span>

1. <span data-ttu-id="56cb1-172">정렬: 데이터베이스가 테스트에 대해 구성 된 및/또는 정의 된 예상된 결과</span><span class="sxs-lookup"><span data-stu-id="56cb1-172">Arrange: The database is configured for the test and/or the expected outcome is defined.</span></span>
1. <span data-ttu-id="56cb1-173">Act: 테스트 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-173">Act: The test is executed.</span></span>
1. <span data-ttu-id="56cb1-174">Assert: 테스트 결과 성공 인지 확인 하려면 어설션은 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-174">Assert: Assertions are made to determine if the test result is a success.</span></span>

<span data-ttu-id="56cb1-175">예를 들어는 `DeleteMessageAsync` 로 식별 되는 단일 메시지를 제거 하기 위한 메서드는 해당 `Id` (*src/RazorPagesTestSample/Data/AppDbContext.cs*):</span><span class="sxs-lookup"><span data-stu-id="56cb1-175">For example, the `DeleteMessageAsync` method is responsible for removing a single message identified by its `Id` (*src/RazorPagesTestSample/Data/AppDbContext.cs*):</span></span>

[!code-csharp[](razor-pages-tests/samples/2.x/src/RazorPagesTestSample/Data/AppDbContext.cs?name=snippet4)]

<span data-ttu-id="56cb1-176">이 메서드에 대 한 두 개의 테스트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-176">There are two tests for this method.</span></span> <span data-ttu-id="56cb1-177">하나의 테스트 메서드는 메시지가 데이터베이스에 있는 경우 메시지를 삭제를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-177">One test checks that the method deletes a message when the message is present in the database.</span></span> <span data-ttu-id="56cb1-178">데이터베이스는 변경 되지 않습니다는 다른 메서드 테스트 메시지 `Id` 삭제 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-178">The other method tests that the database doesn't change if the message `Id` for deletion doesn't exist.</span></span> <span data-ttu-id="56cb1-179">`DeleteMessageAsync_MessageIsDeleted_WhenMessageIsFound` 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-179">The `DeleteMessageAsync_MessageIsDeleted_WhenMessageIsFound` method is shown below:</span></span>

[!code-csharp[](razor-pages-tests/samples_snapshot/2.x/tests/RazorPagesTestSample.Tests/UnitTests/DataAccessLayerTest.cs?name=snippet1)]

<span data-ttu-id="56cb1-180">먼저, 메서드는 작업 단계에 대 한 준비 일어나 정렬 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-180">First, the method performs the Arrange step, where preparation for the Act step takes place.</span></span> <span data-ttu-id="56cb1-181">시드 메시지를 얻고에 보관 `seedMessages`합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-181">The seeding messages are obtained and held in `seedMessages`.</span></span> <span data-ttu-id="56cb1-182">시드 메시지는 데이터베이스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-182">The seeding messages are saved into the database.</span></span> <span data-ttu-id="56cb1-183">사용 하 여 메시지는 `Id` 의 `1` 삭제에 대해 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-183">The message with an `Id` of `1` is set for deletion.</span></span> <span data-ttu-id="56cb1-184">경우는 `DeleteMessageAsync` 메서드 실행 되 고, 필요한 메시지의 모든 메시지로 레코드를 제외 하 고 있어야는 `Id` 의 `1`합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-184">When the `DeleteMessageAsync` method is executed, the expected messages should have all of the messages except for the one with an `Id` of `1`.</span></span> <span data-ttu-id="56cb1-185">`expectedMessages` 변수는이 예상된 결과 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-185">The `expectedMessages` variable represents this expected outcome.</span></span>

[!code-csharp[](razor-pages-tests/samples/2.x/tests/RazorPagesTestSample.Tests/UnitTests/DataAccessLayerTest.cs?name=snippet1)]

<span data-ttu-id="56cb1-186">메서드는 역할:는 `DeleteMessageAsync` 전달 메서드가 실행 되는 `recId` 의 `1`:</span><span class="sxs-lookup"><span data-stu-id="56cb1-186">The method acts: The `DeleteMessageAsync` method is executed passing in the `recId` of `1`:</span></span>

[!code-csharp[](razor-pages-tests/samples/2.x/tests/RazorPagesTestSample.Tests/UnitTests/DataAccessLayerTest.cs?name=snippet2)]

<span data-ttu-id="56cb1-187">마지막으로 메서드가 가져오면는 `Messages` 컨텍스트에서 비교는 `expectedMessages` 둘이 같으면 어설션하:</span><span class="sxs-lookup"><span data-stu-id="56cb1-187">Finally, the method obtains the `Messages` from the context and compares it to the `expectedMessages` asserting that the two are equal:</span></span>

[!code-csharp[](razor-pages-tests/samples/2.x/tests/RazorPagesTestSample.Tests/UnitTests/DataAccessLayerTest.cs?name=snippet3)]

<span data-ttu-id="56cb1-188">비교를 위해 두 `List<Message>` 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-188">In order to compare that the two `List<Message>` are the same:</span></span>

* <span data-ttu-id="56cb1-189">메시지의 기준으로 정렬 된 `Id`합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-189">The messages are ordered by `Id`.</span></span>
* <span data-ttu-id="56cb1-190">메시지 쌍에 비교 되는 `Text` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-190">Message pairs are compared on the `Text` property.</span></span>

<span data-ttu-id="56cb1-191">비슷한 테스트 메서드, `DeleteMessageAsync_NoMessageIsDeleted_WhenMessageIsNotFound` 존재 하지 않는 메시지를 삭제 하는 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-191">A similar test method, `DeleteMessageAsync_NoMessageIsDeleted_WhenMessageIsNotFound` checks the result of attempting to delete a message that doesn't exist.</span></span> <span data-ttu-id="56cb1-192">이 경우 데이터베이스에서 예상된 메시지 같아야 하 후 실제 메시지는 `DeleteMessageAsync` 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-192">In this case, the expected messages in the database should be equal to the actual messages after the `DeleteMessageAsync` method is executed.</span></span> <span data-ttu-id="56cb1-193">데이터베이스의 콘텐츠를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-193">There should be no change to the database's content:</span></span>

[!code-csharp[](razor-pages-tests/samples/2.x/tests/RazorPagesTestSample.Tests/UnitTests/DataAccessLayerTest.cs?name=snippet4)]

## <a name="unit-tests-of-the-page-model-methods"></a><span data-ttu-id="56cb1-194">페이지 모델 메서드의 단위 테스트</span><span class="sxs-lookup"><span data-stu-id="56cb1-194">Unit tests of the page model methods</span></span>

<span data-ttu-id="56cb1-195">다른 일련의 단위 테스트는 테스트 페이지 모델 메서드를 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-195">Another set of unit tests is responsible for tests of page model methods.</span></span> <span data-ttu-id="56cb1-196">메시지 응용 프로그램에서 인덱스 페이지 모델에서 발견 되는 `IndexModel` 클래스 *src/RazorPagesTestSample/Pages/Index.cshtml.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-196">In the message app, the Index page models are found in the `IndexModel` class in *src/RazorPagesTestSample/Pages/Index.cshtml.cs*.</span></span>

| <span data-ttu-id="56cb1-197">페이지 모델 메서드</span><span class="sxs-lookup"><span data-stu-id="56cb1-197">Page model method</span></span> | <span data-ttu-id="56cb1-198">기능</span><span class="sxs-lookup"><span data-stu-id="56cb1-198">Function</span></span> |
| ----------------- | -------- |
| `OnGetAsync` | <span data-ttu-id="56cb1-199">사용 하 여 UI에 대 한 DAL에서 메시지를 가져옵니다는 `GetMessagesAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="56cb1-199">Obtains the messages from the DAL for the UI using the `GetMessagesAsync` method.</span></span> |
| `OnPostAddMessageAsync` | <span data-ttu-id="56cb1-200">경우는 `ModelState` 올바른지, 호출 `AddMessageAsync` 데이터베이스에 메시지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-200">If the `ModelState` is valid, calls `AddMessageAsync` to add a message to the database.</span></span> |
| `OnPostDeleteAllMessagesAsync` | <span data-ttu-id="56cb1-201">호출 `DeleteAllMessagesAsync` 모든 데이터베이스에서 메시지를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-201">Calls `DeleteAllMessagesAsync` to delete all of the messages in the database.</span></span> |
| `OnPostDeleteMessageAsync` | <span data-ttu-id="56cb1-202">실행 `DeleteMessageAsync` 포함 된 메시지를 삭제 하는 `Id` 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-202">Executes `DeleteMessageAsync` to delete a message with the `Id` specified.</span></span> |
| `OnPostAnalyzeMessagesAsync` | <span data-ttu-id="56cb1-203">하나 이상의 메시지는 데이터베이스에 있으면 메시지당 단어의 평균 수를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-203">If one or more messages are in the database, calculates the average number of words per message.</span></span> |

<span data-ttu-id="56cb1-204">페이지 모델 메서드 테스트에서 7 개의 테스트를 사용 하 여 `IndexPageTests` 클래스 (*tests/RazorPagesTestSample.Tests/UnitTests/IndexPageTests.cs*).</span><span class="sxs-lookup"><span data-stu-id="56cb1-204">The page model methods are tested using seven tests in the `IndexPageTests` class (*tests/RazorPagesTestSample.Tests/UnitTests/IndexPageTests.cs*).</span></span> <span data-ttu-id="56cb1-205">테스트는 친숙 한 정렬 Assert Act 패턴을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-205">The tests use the familiar Arrange-Assert-Act pattern.</span></span> <span data-ttu-id="56cb1-206">이러한 테스트에 집중 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-206">These tests focus on:</span></span>

* <span data-ttu-id="56cb1-207">메서드 수행 올바른 동작을 결정 하는 경우는 `ModelState` 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-207">Determining if the methods follow the correct behavior when the `ModelState` is invalid.</span></span>
* <span data-ttu-id="56cb1-208">올바르게 생성 방법을 확인 `IActionResult`합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-208">Confirming the methods produce the correct `IActionResult`.</span></span>
* <span data-ttu-id="56cb1-209">속성 값을 할당 내용이 확인 중입니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-209">Checking that property value assignments are made correctly.</span></span>

<span data-ttu-id="56cb1-210">이 그룹의 테스트 페이지 모델 메서드가 실행 될 작업 단계에 대 한 예상 되는 데이터를 생성 하기 위해 DAL의 메서드를 종종 모의 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-210">This group of tests often mock the methods of the DAL to produce expected data for the Act step where a page model method is executed.</span></span> <span data-ttu-id="56cb1-211">예를 들어는 `GetMessagesAsync` 의 메서드는 `AppDbContext` 출력을 생성 모의 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-211">For example, the `GetMessagesAsync` method of the `AppDbContext` is mocked to produce output.</span></span> <span data-ttu-id="56cb1-212">이 메서드를 실행 하는 페이지 모델 메서드를 모의 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-212">When a page model method executes this method, the mock returns the result.</span></span> <span data-ttu-id="56cb1-213">데이터는 데이터베이스에서 가져와야 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-213">The data doesn't come from the database.</span></span> <span data-ttu-id="56cb1-214">이 메서드는 DAL을 사용 하 여 페이지 모델 테스트에 대 한 예측 가능 하 고 신뢰할 수 있는 테스트 조건을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-214">This creates predictable, reliable test conditions for using the DAL in the page model tests.</span></span>

<span data-ttu-id="56cb1-215">`OnGetAsync_PopulatesThePageModel_WithAListOfMessages` 테스트 표시 방법을 `GetMessagesAsync` 페이지 모델에 대 한 메서드는 모의:</span><span class="sxs-lookup"><span data-stu-id="56cb1-215">The `OnGetAsync_PopulatesThePageModel_WithAListOfMessages` test shows how the `GetMessagesAsync` method is mocked for the page model:</span></span>

[!code-csharp[](razor-pages-tests/samples/2.x/tests/RazorPagesTestSample.Tests/UnitTests/IndexPageTests.cs?name=snippet1&highlight=3-4)]

<span data-ttu-id="56cb1-216">경우는 `OnGetAsync` 메서드는 동작 단계에서 실행 되 고, 페이지 모델 호출 `GetMessagesAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="56cb1-216">When the `OnGetAsync` method is executed in the Act step, it calls the page model's `GetMessagesAsync` method.</span></span>

<span data-ttu-id="56cb1-217">단위 테스트에 Act 단계 (*tests/RazorPagesTestSample.Tests/UnitTests/IndexPageTests.cs*):</span><span class="sxs-lookup"><span data-stu-id="56cb1-217">Unit test Act step (*tests/RazorPagesTestSample.Tests/UnitTests/IndexPageTests.cs*):</span></span>

[!code-csharp[](razor-pages-tests/samples/2.x/tests/RazorPagesTestSample.Tests/UnitTests/IndexPageTests.cs?name=snippet2)]

<span data-ttu-id="56cb1-218">`IndexPage` 페이지 모델 `OnGetAsync` 메서드 (*src/RazorPagesTestSample/Pages/Index.cshtml.cs*):</span><span class="sxs-lookup"><span data-stu-id="56cb1-218">`IndexPage` page model's `OnGetAsync` method (*src/RazorPagesTestSample/Pages/Index.cshtml.cs*):</span></span>

[!code-csharp[](razor-pages-tests/samples/2.x/src/RazorPagesTestSample/Pages/Index.cshtml.cs?name=snippet1&highlight=3)]

<span data-ttu-id="56cb1-219">`GetMessagesAsync` DAL에서 메서드는이 메서드 호출에 대 한 결과 반환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-219">The `GetMessagesAsync` method in the DAL doesn't return the result for this method call.</span></span> <span data-ttu-id="56cb1-220">모의 버전의 메서드는 결과 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-220">The mocked version of the method returns the result.</span></span>

<span data-ttu-id="56cb1-221">에 `Assert` 단계, 실제 메시지 (`actualMessages`)에서 할당 되는 `Messages` 페이지 모델의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-221">In the `Assert` step, the actual messages (`actualMessages`) are assigned from the `Messages` property of the page model.</span></span> <span data-ttu-id="56cb1-222">형식 검사를 메시지에 할당 된 경우에 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-222">A type check is also performed when the messages are assigned.</span></span> <span data-ttu-id="56cb1-223">예상 및 실제 메시지를 통해 비교 됩니다 자신의 `Text` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-223">The expected and actual messages are compared by their `Text` properties.</span></span> <span data-ttu-id="56cb1-224">테스트를 어설션하는 두 `List<Message>` 인스턴스 같은 메시지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-224">The test asserts that the two `List<Message>` instances contain the same messages.</span></span>

[!code-csharp[](razor-pages-tests/samples/2.x/tests/RazorPagesTestSample.Tests/UnitTests/IndexPageTests.cs?name=snippet3)]

<span data-ttu-id="56cb1-225">이 그룹의 다른 테스트 페이지를 포함 하는 모델 개체 만들기는 `DefaultHttpContext`, `ModelStateDictionary`, `ActionContext` 설정 하는 `PageContext`, `ViewDataDictionary`, 및 `PageContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-225">Other tests in this group create page model objects that include the `DefaultHttpContext`, the `ModelStateDictionary`, an `ActionContext` to establish the `PageContext`, a `ViewDataDictionary`, and a `PageContext`.</span></span> <span data-ttu-id="56cb1-226">이들은 테스트를 수행 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="56cb1-226">These are useful in conducting tests.</span></span> <span data-ttu-id="56cb1-227">예를 들어 메시지 응용 프로그램 설정는 `ModelState` 오류로 `AddModelError` 있는지 여부를 확인 하는 유효한 `PageResult` 이 반환 됩니다 `OnPostAddMessageAsync` 실행 됩니다:</span><span class="sxs-lookup"><span data-stu-id="56cb1-227">For example, the message app establishes a `ModelState` error with `AddModelError` to check that a valid `PageResult` is returned when `OnPostAddMessageAsync` is executed:</span></span>

[!code-csharp[](razor-pages-tests/samples/2.x/tests/RazorPagesTestSample.Tests/UnitTests/IndexPageTests.cs?name=snippet4&highlight=11,26,29,32)]

## <a name="additional-resources"></a><span data-ttu-id="56cb1-228">추가 자료</span><span class="sxs-lookup"><span data-stu-id="56cb1-228">Additional resources</span></span>

* [<span data-ttu-id="56cb1-229">에서 단위 테스트 C#.NET Core dotnet 테스트, xUnit를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="56cb1-229">Unit testing C# in .NET Core using dotnet test and xUnit</span></span>](/dotnet/articles/core/testing/unit-testing-with-dotnet-test)
* [<span data-ttu-id="56cb1-230">테스트 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="56cb1-230">Test controllers</span></span>](xref:mvc/controllers/testing)
* <span data-ttu-id="56cb1-231">[단위 테스트 코드](/visualstudio/test/unit-test-your-code) (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="56cb1-231">[Unit Test Your Code](/visualstudio/test/unit-test-your-code) (Visual Studio)</span></span>
* [<span data-ttu-id="56cb1-232">통합 테스트</span><span class="sxs-lookup"><span data-stu-id="56cb1-232">Integration tests</span></span>](xref:test/integration-tests)
* [<span data-ttu-id="56cb1-233">xUnit.net</span><span class="sxs-lookup"><span data-stu-id="56cb1-233">xUnit.net</span></span>](https://xunit.github.io/)
* [<span data-ttu-id="56cb1-234">시작 xUnit.net (.NET Core/ASP.NET 코어)</span><span class="sxs-lookup"><span data-stu-id="56cb1-234">Getting started with xUnit.net (.NET Core/ASP.NET Core)</span></span>](https://xunit.github.io/docs/getting-started-dotnet-core)
* [<span data-ttu-id="56cb1-235">Moq</span><span class="sxs-lookup"><span data-stu-id="56cb1-235">Moq</span></span>](https://github.com/moq/moq4)
* [<span data-ttu-id="56cb1-236">Moq 빠른 시작</span><span class="sxs-lookup"><span data-stu-id="56cb1-236">Moq Quickstart</span></span>](https://github.com/Moq/moq4/wiki/Quickstart)
