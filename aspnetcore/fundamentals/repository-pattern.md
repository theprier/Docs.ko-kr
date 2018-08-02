---
title: ASP.NET Core를 사용한 리포지토리 패턴
author: ardalis
description: ASP.NET Core 앱에서 리포지토리 앱 디자인 패턴을 구현하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 07/02/2018
uid: fundamentals/repository-pattern
ms.openlocfilehash: d64c3d090f62c580ebc05a6bbc2744a4508bb9bc
ms.sourcegitcommit: 927e510d68f269d8335b5a7c8592621219a90965
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2018
ms.locfileid: "39342694"
---
# <a name="repository-pattern-with-aspnet-core"></a><span data-ttu-id="49c6d-103">ASP.NET Core를 사용한 리포지토리 패턴</span><span class="sxs-lookup"><span data-stu-id="49c6d-103">Repository pattern with ASP.NET Core</span></span>

<span data-ttu-id="49c6d-104">작성자: [Steve Smith](https://ardalis.com/), [Scott Addie](https://scottaddie.com) 및 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="49c6d-104">By [Steve Smith](https://ardalis.com/), [Scott Addie](https://scottaddie.com), and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="49c6d-105">‘리포지토리 패턴’은 인터페이스 추상화 뒤에 데이터 액세스를 격리하는 디자인 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-105">The *repository pattern* is a design pattern that isolates data access behind interface abstractions.</span></span> <span data-ttu-id="49c6d-106">데이터베이스 연결과 데이터 저장소 개체 조작은 인터페이스 구현에서 제공하는 메소드를 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-106">Connecting to the database and manipulating data storage objects is performed through methods provided by the interface's implementation.</span></span> <span data-ttu-id="49c6d-107">따라서 연결, 명령, 판독기 등 데이터베이스 관련 문제를 처리하기 위해 코드를 호출할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-107">Consequently, there's no need for calling code to deal with database concerns, such as connections, commands, and readers.</span></span>

<span data-ttu-id="49c6d-108">ASP.NET Core에서 리포지토리 패턴을 구현하면 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-108">Implementation of the repository pattern with ASP.NET Core has the following benefits:</span></span>

* <span data-ttu-id="49c6d-109">비즈니스와 데이터 액세스 계층 간의 직접적인 상호 종속성이 없으므로 앱 구성이 덜 복잡합니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-109">Organization of the app is less complex with no direct interdependency between the business and data access layers.</span></span>
* <span data-ttu-id="49c6d-110">하나 이상의 리포지토리를 통해 코드를 중앙에서 관리하므로 데이터베이스 액세스 코드를 더 쉽게 재사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-110">It's easier to reuse database access code because the code is centrally managed by one or more repositories.</span></span>
* <span data-ttu-id="49c6d-111">비즈니스 도메인을 데이터베이스 계층과 독립적으로 단위 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-111">The business domain can be independently unit tested from the database layer.</span></span>

<span data-ttu-id="49c6d-112">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/repository-pattern/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="49c6d-112">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/repository-pattern/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="49c6d-113">[샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/repository-pattern/samples)에서는 리포지토리 패턴을 사용하여 영화 캐릭터 이름의 목록을 초기화하고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-113">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/repository-pattern/samples) uses the repository pattern to initialize and display a list of movie character names.</span></span> <span data-ttu-id="49c6d-114">앱은 데이터 지속성을 위해 [Entity Framework Core](/ef/core/) 및 `ApplicationDbContext` 클래스를 사용하지만, 데이터베이스 인프라는 데이터가 액세스되는 위치를 모릅니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-114">The app uses [Entity Framework Core](/ef/core/) and an `ApplicationDbContext` class for its data persistence, but the database infrastructure isn't apparent where the data is accessed.</span></span> <span data-ttu-id="49c6d-115">데이터 액세스 및 데이터베이스 개체는 [리포지토리](https://martinfowler.com/eaaCatalog/repository.html) 뒤에 추상화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-115">Data access and database objects are abstracted behind a [repository](https://martinfowler.com/eaaCatalog/repository.html).</span></span>

## <a name="repository-interface"></a><span data-ttu-id="49c6d-116">리포지토리 인터페이스</span><span class="sxs-lookup"><span data-stu-id="49c6d-116">Repository interface</span></span>

<span data-ttu-id="49c6d-117">리포지토리 인터페이스는 구현의 속성 및 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-117">A repository interface defines the properties and methods for implementation.</span></span> <span data-ttu-id="49c6d-118">샘플 앱에서 영화 캐릭터 데이터의 리포지토리 인터페이스는 `ICharacterRepository`입니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-118">In the sample app, the repository interface for movie character data is `ICharacterRepository`.</span></span> <span data-ttu-id="49c6d-119">`ICharacterRepository`는 앱에서 `Character` 인스턴스를 사용하는 데 필요한 `ListAll` 및 `Add` 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-119">`ICharacterRepository` defines the `ListAll` and `Add` methods required to work with `Character` instances in the app:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](repository-pattern/samples/2.x/RepositoryPatternSample/Interfaces/ICharacterRepository.cs?name=snippet1)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](repository-pattern/samples/1.x/RepositoryPatternSample/Interfaces/ICharacterRepository.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="49c6d-120">`Character`는 다음과 같이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-120">`Character` is defined as:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](repository-pattern/samples/2.x/RepositoryPatternSample/Models/Character.cs?name=snippet1)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](repository-pattern/samples/1.x/RepositoryPatternSample/Models/Character.cs?name=snippet1)]

::: moniker-end

## <a name="repository-concrete-type"></a><span data-ttu-id="49c6d-121">리포지토리 구체적 형식</span><span class="sxs-lookup"><span data-stu-id="49c6d-121">Repository concrete type</span></span>

<span data-ttu-id="49c6d-122">인터페이스는 구체적인 형식에서 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-122">The interface is implemented by a concrete type.</span></span> <span data-ttu-id="49c6d-123">샘플 앱에서 `CharacterRepository`는 데이터베이스 컨텍스트를 관리하고 `ListAll` 및 `Add` 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-123">In the sample app, `CharacterRepository` manages the database context and implements the `ListAll` and `Add` methods:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](repository-pattern/samples/2.x/RepositoryPatternSample/Models/CharacterRepository.cs?name=snippet1)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](repository-pattern/samples/1.x/RepositoryPatternSample/Models/CharacterRepository.cs?name=snippet1)]

::: moniker-end

## <a name="register-the-repository-service"></a><span data-ttu-id="49c6d-124">리포지토리 서비스 등록</span><span class="sxs-lookup"><span data-stu-id="49c6d-124">Register the repository service</span></span>

<span data-ttu-id="49c6d-125">리포지토리 및 데이터베이스 컨텍스트는 `Startup.ConfigureServices`의 서비스 컨테이너에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-125">The repository and database context are registered with the service container in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="49c6d-126">샘플 앱에서 `ApplicationDbContext`는 확장 메서드 [AddDbContext](/dotnet/api/microsoft.extensions.dependencyinjection.entityframeworkservicecollectionextensions.adddbcontext)에 대한 호출로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-126">In the sample app, `ApplicationDbContext` is configured with the call to the extension method [AddDbContext](/dotnet/api/microsoft.extensions.dependencyinjection.entityframeworkservicecollectionextensions.adddbcontext).</span></span> <span data-ttu-id="49c6d-127">`ICharacterRepository`는 지정된 서비스로 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-127">`ICharacterRepository` is registered as a scoped service:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](repository-pattern/samples/2.x/RepositoryPatternSample/Startup.cs?name=snippet1&highlight=4-6,18)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](repository-pattern/samples/1.x/RepositoryPatternSample/Startup.cs?name=snippet1&highlight=4-6,12)]

::: moniker-end

## <a name="inject-an-instance-of-the-repository"></a><span data-ttu-id="49c6d-128">리포지토리 인스턴스 주입</span><span class="sxs-lookup"><span data-stu-id="49c6d-128">Inject an instance of the repository</span></span>

<span data-ttu-id="49c6d-129">데이터베이스 액세스가 필요한 클래스에서 생성자를 통해 리포지토리의 인스턴스를 요청하고 클래스 메소드에서 사용할 private 필드에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-129">In a class where database access is required, an instance of the repository is requested via the constructor and assigned to a private field for use by class methods.</span></span> <span data-ttu-id="49c6d-130">샘플 앱에서 `ICharacterRepository`는 다음을 수행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-130">In the sample app, `ICharacterRepository` is used to:</span></span>

* <span data-ttu-id="49c6d-131">문자가 없으면 데이터베이스를 문자로 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-131">Populate the database if no characters exist.</span></span>
* <span data-ttu-id="49c6d-132">표시할 문자 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-132">Obtain a list of the characters for display.</span></span>

<span data-ttu-id="49c6d-133">호출 코드는 인터페이스의 구현 `CharacterRepository`만 조작합니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-133">Notice how the calling code only interacts with the interface's implementation, `CharacterRepository`.</span></span> <span data-ttu-id="49c6d-134">호출 코드에서 `ApplicationDbContext`를 직접 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-134">Calling code doesn't use the `ApplicationDbContext` directly:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](repository-pattern/samples/2.x/RepositoryPatternSample/Pages/Index.cshtml.cs?name=snippet1)]

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](repository-pattern/samples/1.x/RepositoryPatternSample/Controllers/HomeController.cs?name=snippet1)]

::: moniker-end

## <a name="generic-repository-interface"></a><span data-ttu-id="49c6d-135">제네릭 리포지토리 인터페이스</span><span class="sxs-lookup"><span data-stu-id="49c6d-135">Generic repository interface</span></span>

<span data-ttu-id="49c6d-136">이 항목과 샘플 앱에서는 각 비즈니스 개체에 대해 리포지토리를 하나씩 만드는 가장 단순한 리포지토리 패턴 구현에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-136">This topic and its sample app demonstrate the simplest implementation of the repository pattern, where one repository is created for each business object.</span></span> <span data-ttu-id="49c6d-137">앱이 몇 개의 개체를 초과하여 커지는 경우 제네릭 리포지토리 인터페이스를 사용하면 리포지토리 패턴 구현에 필요한 코드의 양을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49c6d-137">If the app grows beyond a few objects, a *generic repository interface* may reduce the amount of code required to implement the repository pattern.</span></span> <span data-ttu-id="49c6d-138">자세한 내용은 [DevIQ: Repository Pattern: Generic Repository Interface](http://deviq.com/repository-pattern/)(DevIQ: 리포지토리 패턴: 제네릭 리포지토리 인터페이스)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49c6d-138">For more information, see [DevIQ: Repository Pattern: Generic Repository Interface](http://deviq.com/repository-pattern/).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="49c6d-139">추가 자료</span><span class="sxs-lookup"><span data-stu-id="49c6d-139">Additional resources</span></span>

* <span data-ttu-id="49c6d-140">[DevIQ: Repository Pattern](https://deviq.com/repository-pattern/)(DevIQ: 리포지토리 패턴)</span><span class="sxs-lookup"><span data-stu-id="49c6d-140">[DevIQ: Repository Pattern](https://deviq.com/repository-pattern/)</span></span>
* [<span data-ttu-id="49c6d-141">종속성 주입</span><span class="sxs-lookup"><span data-stu-id="49c6d-141">Dependency injection</span></span>](xref:fundamentals/dependency-injection)
* [<span data-ttu-id="49c6d-142">뷰에 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="49c6d-142">Dependency injection into views</span></span>](xref:mvc/views/dependency-injection)
* [<span data-ttu-id="49c6d-143">컨트롤러에 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="49c6d-143">Dependency injection into controllers</span></span>](xref:mvc/controllers/dependency-injection)
* [<span data-ttu-id="49c6d-144">요구 사항 처리기의 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="49c6d-144">Dependency injection in requirement handlers</span></span>](xref:security/authorization/dependencyinjection)
* [<span data-ttu-id="49c6d-145">Inversion of Control 컨테이너 및 종속성 주입 패턴</span><span class="sxs-lookup"><span data-stu-id="49c6d-145">Inversion of Control Containers and the Dependency Injection Pattern</span></span>](https://www.martinfowler.com/articles/injection.html)
