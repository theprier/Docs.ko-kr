---
title: ASP.NET Core에서 종속성 주입
author: ardalis
description: ASP.NET Core에서 종속성 주입을 구현하는 방법 및 사용 방법에 알아봅니다.
manager: wpickett
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/dependency-injection
ms.openlocfilehash: 700ceb081b2067f932ce8ed08c45c62058775e33
ms.sourcegitcommit: 3d071fabaf90e32906df97b08a8d00e602db25c0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="dependency-injection-in-aspnet-core"></a><span data-ttu-id="d989f-103">ASP.NET Core에서 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="d989f-103">Dependency injection in ASP.NET Core</span></span>

<a name="fundamentals-dependency-injection"></a>

<span data-ttu-id="d989f-104">작성자: [Steve Smith](https://ardalis.com/) 및 [Scott Addie](https://scottaddie.com)</span><span class="sxs-lookup"><span data-stu-id="d989f-104">By [Steve Smith](https://ardalis.com/) and [Scott Addie](https://scottaddie.com)</span></span>

<span data-ttu-id="d989f-105">ASP.NET Core는 처음부터 종속성 주입을 지원 및 활용하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-105">ASP.NET Core is designed from the ground up to support and leverage dependency injection.</span></span> <span data-ttu-id="d989f-106">ASP.NET Core 응용 프로그램은 기본 제공 프레임워크 서비스를 시작 클래스의 메서드에 주입하여 활용할 수 있으며, 응용 프로그램 서비스도 주입에 대해 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-106">ASP.NET Core applications can leverage built-in framework services by having them injected into methods in the Startup class, and application services can be configured for injection as well.</span></span> <span data-ttu-id="d989f-107">ASP.NET Core에서 제공되는 기본 서비스 컨테이너는 최소한의 기능 집합을 제공하며 다른 컨테이너를 대체하는 데 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-107">The default services container provided by ASP.NET Core provides a minimal feature set and isn't intended to replace other containers.</span></span>

<span data-ttu-id="d989f-108">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/dependency-injection/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="d989f-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/dependency-injection/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="d989f-109">종속성 주입이란?</span><span class="sxs-lookup"><span data-stu-id="d989f-109">What is dependency injection?</span></span>

<span data-ttu-id="d989f-110">DI(종속성 주입)란 개체와 협력자 또는 종속성 간의 느슨한 결합을 실현하기 위한 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-110">Dependency injection (DI) is a technique for achieving loose coupling between objects and their collaborators, or dependencies.</span></span> <span data-ttu-id="d989f-111">직접 협력자를 인스턴스화하거나 정적 참조를 사용하는 대신에, 해당 작업을 수행하기 위해 필요한 클래스의 개체가 특정 방식으로 클래스에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-111">Rather than directly instantiating collaborators, or using static references, the objects a class needs in order to perform its actions are provided to the class in some fashion.</span></span> <span data-ttu-id="d989f-112">대부분의 경우 클래스는 해당 생성자를 통해 해당 종속성을 선언하게 되며 [명시적 종속성 원칙](http://deviq.com/explicit-dependencies-principle/)을 따르도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-112">Most often, classes will declare their dependencies via their constructor, allowing them to follow the [Explicit Dependencies Principle](http://deviq.com/explicit-dependencies-principle/).</span></span> <span data-ttu-id="d989f-113">이 방법을 “생성자 주입”이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-113">This approach is known as "constructor injection".</span></span>

<span data-ttu-id="d989f-114">DI를 염두에 두고 클래스를 설계한 경우 협력자에게 직접적으로 하드 코드된 종속성이 없기 때문에 더 느슨하게 결합됩니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-114">When classes are designed with DI in mind, they're more loosely coupled because they don't have direct, hard-coded dependencies on their collaborators.</span></span> <span data-ttu-id="d989f-115">이는 *“높은 수준의 모듈은 낮은 수준의 모듈에 의존해서는 안되며 둘다 추상화에 의존해야 한다”* 는 [종속성 반전 원칙](http://deviq.com/dependency-inversion-principle/)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-115">This follows the [Dependency Inversion Principle](http://deviq.com/dependency-inversion-principle/), which states that *"high level modules shouldn't depend on low level modules; both should depend on abstractions."*</span></span> <span data-ttu-id="d989f-116">클래스는 특정 구현을 참조하는 대신, 클래스를 생성할 때에 제공되는 추상화(일반적으로 `interfaces`)를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-116">Instead of referencing specific implementations, classes request abstractions (typically `interfaces`) which are provided to them when the class is constructed.</span></span> <span data-ttu-id="d989f-117">인터페이스로 종속성을 추출하고 매개 변수로 이러한 인터페이스의 구현을 제공하는 것 또한 [전략 디자인 패턴](http://deviq.com/strategy-design-pattern/)의 예시입니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-117">Extracting dependencies into interfaces and providing implementations of these interfaces as parameters is also an example of the [Strategy design pattern](http://deviq.com/strategy-design-pattern/).</span></span>

<span data-ttu-id="d989f-118">시스템이 DI를 사용하도록 설계된 경우, 해당 생성자(또는 속성)를 통해 해당 종속성을 요청하는 많은 클래스를 사용하면 클래스가 연결된 종속성으로 이러한 클래스를 만들도록 하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-118">When a system is designed to use DI, with many classes requesting their dependencies via their constructor (or properties), it's helpful to have a class dedicated to creating these classes with their associated dependencies.</span></span> <span data-ttu-id="d989f-119">이러한 클래스를 *컨테이너* 또는 더 구체적으로 [IoC(Inversion of Control)](http://deviq.com/inversion-of-control/) DI(종속성 주입) 컨테이너라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-119">These classes are referred to as *containers*, or more specifically, [Inversion of Control (IoC)](http://deviq.com/inversion-of-control/) containers or Dependency Injection (DI) containers.</span></span> <span data-ttu-id="d989f-120">컨테이너는 본질적으로 요청된 유형의 인스턴스를 제공해야 하는 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-120">A container is essentially a factory that's responsible for providing instances of types that are requested from it.</span></span> <span data-ttu-id="d989f-121">지정된 유형에 종속성이 있음이 선언되고, 컨테이너가 종속성 유형을 제공하도록 구성된 경우, 요청된 인스턴스 생성의 일환으로 종속성이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-121">If a given type has declared that it has dependencies, and the container has been configured to provide the dependency types, it will create the dependencies as part of creating the requested instance.</span></span> <span data-ttu-id="d989f-122">이러한 방식에서는 모든 하드 코드된 개체를 생성할 필요 없이 복잡한 종속성 그래프가 클래스에 제공될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-122">In this way, complex dependency graphs can be provided to classes without the need for any hard-coded object construction.</span></span> <span data-ttu-id="d989f-123">해당 종속성이 있는 개체를 만드는 것 외에도 컨테이너는 일반적으로 응용 프로그램 내 개체 수명 주기를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-123">In addition to creating objects with their dependencies, containers typically manage object lifetimes within the application.</span></span>

<span data-ttu-id="d989f-124">ASP.NET Core에는 생성자 주입을 기본으로 지원하는 간단한 기본 제공 컨테이너(`IServiceProvider` 인터페이스에서 interface)가 포함되며, ASP.NET을 사용하면 DI를 통해 특정 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-124">ASP.NET Core includes a simple built-in container (represented by the `IServiceProvider` interface) that supports constructor injection by default, and ASP.NET makes certain services available through DI.</span></span> <span data-ttu-id="d989f-125">ASP.NET의 컨테이너는 *서비스*로 관리하는 유형을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-125">ASP.NET's container refers to the types it manages as *services*.</span></span> <span data-ttu-id="d989f-126">이 문서의 나머지 부분에서 *서비스*는 ASP.NET Core의 IoC 컨테이너에서 관리하는 유형을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-126">Throughout the rest of this article, *services* will refer to types that are managed by ASP.NET Core's IoC container.</span></span> <span data-ttu-id="d989f-127">응용 프로그램의 `Startup` 클래스에 있는 `ConfigureServices` 메서드에서 기본 제공 컨테이너의 서비스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-127">You configure the built-in container's services in the `ConfigureServices` method in your application's `Startup` class.</span></span>

> [!NOTE]
> <span data-ttu-id="d989f-128">Martin Fowler는 [Inversion of Control 컨테이너 및 종속성 주입 패턴](https://www.martinfowler.com/articles/injection.html)에 대한 광범위한 문서를 작성했습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-128">Martin Fowler has written an extensive article on [Inversion of Control Containers and the Dependency Injection Pattern](https://www.martinfowler.com/articles/injection.html).</span></span> <span data-ttu-id="d989f-129">Microsoft Patterns and Practices에도 [종속성 주입](https://msdn.microsoft.com/library/hh323705.aspx)에 대한 훌륭한 설명이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-129">Microsoft Patterns and Practices also has a great description of [Dependency Injection](https://msdn.microsoft.com/library/hh323705.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="d989f-130">이 문서에서는 모든 ASP.NET 응용 프로그램에 적용되는 종속성 주입을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-130">This article covers Dependency Injection as it applies to all ASP.NET applications.</span></span> <span data-ttu-id="d989f-131">MVC 컨트롤러 내 종속성 주입은 [종속성 주입 및 컨트롤러](../mvc/controllers/dependency-injection.md)에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-131">Dependency Injection within MVC controllers is covered in [Dependency Injection and Controllers](../mvc/controllers/dependency-injection.md).</span></span>

### <a name="constructor-injection-behavior"></a><span data-ttu-id="d989f-132">생성자 주입 동작</span><span class="sxs-lookup"><span data-stu-id="d989f-132">Constructor injection behavior</span></span>

<span data-ttu-id="d989f-133">생성자 주입을 위해서는 문제의 생성자가 *public*이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-133">Constructor injection requires that the constructor in question be *public*.</span></span> <span data-ttu-id="d989f-134">그렇지 않으면 앱은 `InvalidOperationException`을 throw하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-134">Otherwise, your app will throw an `InvalidOperationException`:</span></span>

> <span data-ttu-id="d989f-135">‘YourType’ 유형에 대한 적합한 생성자를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-135">A suitable constructor for type 'YourType' couldn't be located.</span></span> <span data-ttu-id="d989f-136">유형이 구체적이고 서비스가 public 생성자의 모든 매개 변수에 등록되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-136">Ensure the type is concrete and services are registered for all parameters of a public constructor.</span></span>

<span data-ttu-id="d989f-137">생성자 주입을 위해서는 적합한 생성자가 하나만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-137">Constructor injection requires that only one applicable constructor exist.</span></span> <span data-ttu-id="d989f-138">생성자 오버로드가 지원되지만, 해당 인수가 모두 종속성 주입으로 처리될 수 있는 하나의 오버로드만 존재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-138">Constructor overloads are supported, but only one overload can exist whose arguments can all be fulfilled by dependency injection.</span></span> <span data-ttu-id="d989f-139">둘 이상인 경우 앱은 `InvalidOperationException`을 throw하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-139">If more than one exists, your app will throw an `InvalidOperationException`:</span></span>

> <span data-ttu-id="d989f-140">지정된 모든 인수 형식을 수락하는 여러 명의 생성자를 ‘YourType’ 유형에서 찾았습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-140">Multiple constructors accepting all given argument types have been found in type 'YourType'.</span></span> <span data-ttu-id="d989f-141">적용 가능한 생성자는 하나여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-141">There should only be one applicable constructor.</span></span>

<span data-ttu-id="d989f-142">생성자는 종속성 주입으로 제공되지 않은 인수를 수락할 수 있지만, 기본값을 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-142">Constructors can accept arguments that are not provided by dependency injection, but these must support default values.</span></span> <span data-ttu-id="d989f-143">예:</span><span class="sxs-lookup"><span data-stu-id="d989f-143">For example:</span></span>

```csharp
// throws InvalidOperationException: Unable to resolve service for type 'System.String'...
public CharactersController(ICharacterRepository characterRepository, string title)
{
    _characterRepository = characterRepository;
    _title = title;
}

// runs without error
public CharactersController(ICharacterRepository characterRepository, string title = "Characters")
{
    _characterRepository = characterRepository;
    _title = title;
}
```

## <a name="using-framework-provided-services"></a><span data-ttu-id="d989f-144">프레임워크에서 제공한 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="d989f-144">Using framework-provided services</span></span>

<span data-ttu-id="d989f-145">`Startup` 클래스의 `ConfigureServices` 메서드는 응용 프로그램이 사용하는 서비스를 정의하는 작업을 담당하며, Entity Framework Core 및 ASP.NET Core MVC와 같은 플랫폼 기능을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-145">The `ConfigureServices` method in the `Startup` class is responsible for defining the services the application will use, including platform features like Entity Framework Core and ASP.NET Core MVC.</span></span> <span data-ttu-id="d989f-146">처음에 `ConfigureServices`에 제공된 `IServiceCollection`에는 정의된 다음과 같은 서비스가 있습니다([호스트 구성 방법](xref:fundamentals/hosting)에 따라).</span><span class="sxs-lookup"><span data-stu-id="d989f-146">Initially, the `IServiceCollection` provided to `ConfigureServices` has the following services defined (depending on [how the host was configured](xref:fundamentals/hosting)):</span></span>

| <span data-ttu-id="d989f-147">서비스 종류</span><span class="sxs-lookup"><span data-stu-id="d989f-147">Service Type</span></span> | <span data-ttu-id="d989f-148">수명</span><span class="sxs-lookup"><span data-stu-id="d989f-148">Lifetime</span></span> |
| ----- | ------- |
| [<span data-ttu-id="d989f-149">Microsoft.AspNetCore.Hosting.IHostingEnvironment</span><span class="sxs-lookup"><span data-stu-id="d989f-149">Microsoft.AspNetCore.Hosting.IHostingEnvironment</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment) | <span data-ttu-id="d989f-150">Singleton</span><span class="sxs-lookup"><span data-stu-id="d989f-150">Singleton</span></span> |
| [<span data-ttu-id="d989f-151">Microsoft.Extensions.Logging.ILoggerFactory</span><span class="sxs-lookup"><span data-stu-id="d989f-151">Microsoft.Extensions.Logging.ILoggerFactory</span></span>](/dotnet/api/microsoft.extensions.logging.iloggerfactory) | <span data-ttu-id="d989f-152">Singleton</span><span class="sxs-lookup"><span data-stu-id="d989f-152">Singleton</span></span> |
| [<span data-ttu-id="d989f-153">Microsoft.Extensions.Logging.ILogger&lt;T&gt;</span><span class="sxs-lookup"><span data-stu-id="d989f-153">Microsoft.Extensions.Logging.ILogger&lt;T&gt;</span></span>](/dotnet/api/microsoft.extensions.logging.ilogger) | <span data-ttu-id="d989f-154">Singleton</span><span class="sxs-lookup"><span data-stu-id="d989f-154">Singleton</span></span> |
| [<span data-ttu-id="d989f-155">Microsoft.AspNetCore.Hosting.Builder.IApplicationBuilderFactory</span><span class="sxs-lookup"><span data-stu-id="d989f-155">Microsoft.AspNetCore.Hosting.Builder.IApplicationBuilderFactory</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.builder.iapplicationbuilderfactory) | <span data-ttu-id="d989f-156">Transient</span><span class="sxs-lookup"><span data-stu-id="d989f-156">Transient</span></span> |
| [<span data-ttu-id="d989f-157">Microsoft.AspNetCore.Http.IHttpContextFactory</span><span class="sxs-lookup"><span data-stu-id="d989f-157">Microsoft.AspNetCore.Http.IHttpContextFactory</span></span>](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextfactory) | <span data-ttu-id="d989f-158">Transient</span><span class="sxs-lookup"><span data-stu-id="d989f-158">Transient</span></span> |
| [<span data-ttu-id="d989f-159">Microsoft.Extensions.Options.IOptions&lt;T&gt;</span><span class="sxs-lookup"><span data-stu-id="d989f-159">Microsoft.Extensions.Options.IOptions&lt;T&gt;</span></span>](/dotnet/api/microsoft.extensions.options.ioptions-1) | <span data-ttu-id="d989f-160">Singleton</span><span class="sxs-lookup"><span data-stu-id="d989f-160">Singleton</span></span> |
| [<span data-ttu-id="d989f-161">System.Diagnostics.DiagnosticSource</span><span class="sxs-lookup"><span data-stu-id="d989f-161">System.Diagnostics.DiagnosticSource</span></span>](https://docs.microsoft.com/dotnet/core/api/system.diagnostics.diagnosticsource) | <span data-ttu-id="d989f-162">Singleton</span><span class="sxs-lookup"><span data-stu-id="d989f-162">Singleton</span></span> |
| [<span data-ttu-id="d989f-163">System.Diagnostics.DiagnosticListener</span><span class="sxs-lookup"><span data-stu-id="d989f-163">System.Diagnostics.DiagnosticListener</span></span>](https://docs.microsoft.com/dotnet/core/api/system.diagnostics.diagnosticlistener) | <span data-ttu-id="d989f-164">Singleton</span><span class="sxs-lookup"><span data-stu-id="d989f-164">Singleton</span></span> |
| [<span data-ttu-id="d989f-165">Microsoft.AspNetCore.Hosting.IStartupFilter</span><span class="sxs-lookup"><span data-stu-id="d989f-165">Microsoft.AspNetCore.Hosting.IStartupFilter</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.istartupfilter) | <span data-ttu-id="d989f-166">Transient</span><span class="sxs-lookup"><span data-stu-id="d989f-166">Transient</span></span> |
| [<span data-ttu-id="d989f-167">Microsoft.Extensions.ObjectPool.ObjectPoolProvider</span><span class="sxs-lookup"><span data-stu-id="d989f-167">Microsoft.Extensions.ObjectPool.ObjectPoolProvider</span></span>](/dotnet/api/microsoft.extensions.objectpool.objectpoolprovider) | <span data-ttu-id="d989f-168">Singleton</span><span class="sxs-lookup"><span data-stu-id="d989f-168">Singleton</span></span> |
| [<span data-ttu-id="d989f-169">Microsoft.Extensions.Options.IConfigureOptions&lt;T&gt;</span><span class="sxs-lookup"><span data-stu-id="d989f-169">Microsoft.Extensions.Options.IConfigureOptions&lt;T&gt;</span></span>](/dotnet/api/microsoft.extensions.options.iconfigureoptions-1) | <span data-ttu-id="d989f-170">Transient</span><span class="sxs-lookup"><span data-stu-id="d989f-170">Transient</span></span> |
| [<span data-ttu-id="d989f-171">Microsoft.AspNetCore.Hosting.Server.IServer</span><span class="sxs-lookup"><span data-stu-id="d989f-171">Microsoft.AspNetCore.Hosting.Server.IServer</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.server.iserver) | <span data-ttu-id="d989f-172">Singleton</span><span class="sxs-lookup"><span data-stu-id="d989f-172">Singleton</span></span> |
| [<span data-ttu-id="d989f-173">Microsoft.AspNetCore.Hosting.IStartup</span><span class="sxs-lookup"><span data-stu-id="d989f-173">Microsoft.AspNetCore.Hosting.IStartup</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.istartup) | <span data-ttu-id="d989f-174">Singleton</span><span class="sxs-lookup"><span data-stu-id="d989f-174">Singleton</span></span> |
| [<span data-ttu-id="d989f-175">Microsoft.AspNetCore.Hosting.IApplicationLifetime</span><span class="sxs-lookup"><span data-stu-id="d989f-175">Microsoft.AspNetCore.Hosting.IApplicationLifetime</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime) | <span data-ttu-id="d989f-176">Singleton</span><span class="sxs-lookup"><span data-stu-id="d989f-176">Singleton</span></span> |

<span data-ttu-id="d989f-177">다음은 `AddDbContext`, `AddIdentity` 및 `AddMvc`와 같은 다양한 확장 메서드를 사용하여 추가 서비스를 컨테이너에 추가하는 방법에 대한 예시입니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-177">Below is an example of how to add additional services to the container using a number of extension methods like `AddDbContext`, `AddIdentity`, and `AddMvc`.</span></span>

[!code-csharp[](../common/samples/WebApplication1/Startup.cs?highlight=5-6,8-10,12&range=39-56)]

<span data-ttu-id="d989f-178">MVC와 같이 ASP.NET에서 제공하는 기능 및 미들웨어는 단일 Add*ServiceName* 확장 메서드 사용에 대한 규칙에 따라 해당 기능에 필요한 모든 서비스를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-178">The features and middleware provided by ASP.NET, such as MVC, follow a convention of using a single Add*ServiceName* extension method to register all of the services required by that feature.</span></span>

> [!TIP]
> <span data-ttu-id="d989f-179">해당 매개 변수 목록을 통해 `Startup` 메서드 내에서 특정 프레임워크에서 제공한 서비스를 요청할 수 있습니다. 자세한 내용은 [응용 프로그램 시작](startup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d989f-179">You can request certain framework-provided services within `Startup` methods through their parameter lists - see [Application Startup](startup.md) for more details.</span></span>

## <a name="registering-services"></a><span data-ttu-id="d989f-180">서비스 등록</span><span class="sxs-lookup"><span data-stu-id="d989f-180">Registering services</span></span>

<span data-ttu-id="d989f-181">다음과 같이 사용자 고유의 응용 프로그램 서비스를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-181">You can register your own application services as follows.</span></span> <span data-ttu-id="d989f-182">첫 번째 제네릭 형식은 컨테이너에서 요청되는 형식(일반적으로 인터페이스)을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-182">The first generic type represents the type (typically an interface) that will be requested from the container.</span></span> <span data-ttu-id="d989f-183">두 번째 제네릭 형식은 컨테이너에 의해 인스턴스화되고 그러한 요청을 처리하는 데 사용되는 구체적 형식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-183">The second generic type represents the concrete type that will be instantiated by the container and used to fulfill such requests.</span></span>

[!code-csharp[](../common/samples/WebApplication1/Startup.cs?range=53-54)]

> [!NOTE]
> <span data-ttu-id="d989f-184">각 `services.Add<ServiceName>` 확장 메서드는 서비스를 추가(및 잠재적으로 구성)합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-184">Each `services.Add<ServiceName>` extension method adds (and potentially configures) services.</span></span> <span data-ttu-id="d989f-185">예를 들어 `services.AddMvc()`는 MVC에서 요청하는 서비스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-185">For example, `services.AddMvc()` adds the services MVC requires.</span></span> <span data-ttu-id="d989f-186">이 규칙에 따라 `Microsoft.Extensions.DependencyInjection` 네임스페이스의 확장 메서드를 배치하여 서비스 등록의 그룹을 캡슐화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-186">It's recommended that you follow this convention, placing extension methods in the `Microsoft.Extensions.DependencyInjection` namespace, to encapsulate groups of service registrations.</span></span>

<span data-ttu-id="d989f-187">`AddTransient` 메서드는 추상 형식을 매핑하는 데 사용되어, 이를 요청하는 모든 개체에서 별도로 인스턴스화되는 서비스를 구체화합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-187">The `AddTransient` method is used to map abstract types to concrete services that are instantiated separately for every object that requires it.</span></span> <span data-ttu-id="d989f-188">이를 서비스의 *수명*이라고 하며, 추가 수명 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-188">This is known as the service's *lifetime*, and additional lifetime options are described below.</span></span> <span data-ttu-id="d989f-189">등록하는 서비스마다 적절한 수명을 선택하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-189">It's important to choose an appropriate lifetime for each of the services you register.</span></span> <span data-ttu-id="d989f-190">요청한 각 클래스에 서비스의 새 인스턴스를 제공해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="d989f-190">Should a new instance of the service be provided to each class that requests it?</span></span> <span data-ttu-id="d989f-191">지정된 웹 요청에 하나의 인스턴스만 사용해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="d989f-191">Should one instance be used throughout a given web request?</span></span> <span data-ttu-id="d989f-192">또는 응용 프로그램의 수명 동안 단일 인스턴스를 사용해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="d989f-192">Or should a single instance be used for the lifetime of the application?</span></span>

<span data-ttu-id="d989f-193">이 문서에 대한 샘플에서는 `CharactersController`라는 문자 이름을 표시하는 간단한 컨트롤러가 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-193">In the sample for this article, there's a simple controller that displays character names, called `CharactersController`.</span></span> <span data-ttu-id="d989f-194">해당 `Index` 메서드는 응용 프로그램에 저장된 문자의 현재 목록을 표시하고, 없는 경우 소수의 문자를 사용하여 컬렉션을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-194">Its `Index` method displays the current list of characters that have been stored in the application, and initializes the collection with a handful of characters if none exist.</span></span> <span data-ttu-id="d989f-195">이 응용 프로그램이 지속성을 위해 Entity Framework Core 및 `ApplicationDbContext` 클래스를 사용하긴 하지만 컨트롤러에는 해당 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-195">Note that although this application uses Entity Framework Core and the `ApplicationDbContext` class for its persistence, none of that's apparent in the controller.</span></span> <span data-ttu-id="d989f-196">대신, 특정 데이터 액세스 메커니즘은 [리포지토리 패턴](http://deviq.com/repository-pattern/)을 따르는 인터페이스 `ICharacterRepository` 뒤에서 추상화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-196">Instead, the specific data access mechanism has been abstracted behind an interface, `ICharacterRepository`, which follows the [repository pattern](http://deviq.com/repository-pattern/).</span></span> <span data-ttu-id="d989f-197">`ICharacterRepository`의 인스턴스는 생성자에 의해 요청되고 전용 필드에 할당됩니다. 그런 다음, 필요에 따라 문자에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-197">An instance of `ICharacterRepository` is requested via the constructor and assigned to a private field, which is then used to access characters as necessary.</span></span>

[!code-csharp[](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Controllers/CharactersController.cs?highlight=3,5,6,7,8,14,21-27&range=8-36)]

<span data-ttu-id="d989f-198">`ICharacterRepository`는 컨트롤러가 `Character` 인스턴스를 사용해야 하는 두 가지 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-198">The `ICharacterRepository` defines the two methods the controller needs to work with `Character` instances.</span></span>

[!code-csharp[](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Interfaces/ICharacterRepository.cs?highlight=8,9)]

<span data-ttu-id="d989f-199">이 인터페이스는 런타임에 사용되는 구체적인 형식인 `CharacterRepository`에 의해 차례로 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-199">This interface is in turn implemented by a concrete type, `CharacterRepository`, that's used at runtime.</span></span>

> [!NOTE]
> <span data-ttu-id="d989f-200">`CharacterRepository` 클래스와 함께 사용되는 DI 방식은 “리포지토리”나 데이터 액세스 클래스뿐 아니라 모든 응용 프로그램 서비스에 대해 따를 수 있는 일반 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-200">The way DI is used with the `CharacterRepository` class is a general model you can follow for all of your application services, not just in "repositories" or data access classes.</span></span>

[!code-csharp[](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Models/CharacterRepository.cs?highlight=9,11,12,13,14)]

<span data-ttu-id="d989f-201">`CharacterRepository`는 해당 생성자에서 `ApplicationDbContext`를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-201">Note that `CharacterRepository` requests an `ApplicationDbContext` in its constructor.</span></span> <span data-ttu-id="d989f-202">종속성 주입이 자체 종속성을 차례로 요청하는 요청된 각 종속성을 통해 이와 같이 연결된 방식으로 사용되는 것은 드문 일이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-202">It's not unusual for dependency injection to be used in a chained fashion like this, with each requested dependency in turn requesting its own dependencies.</span></span> <span data-ttu-id="d989f-203">컨테이너는 그래프의 모든 종속성을 해결하고, 완전히 해결된 서비스를 반환하는 작업을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-203">The container is responsible for resolving all of the dependencies in the graph and returning the fully resolved service.</span></span>

> [!NOTE]
> <span data-ttu-id="d989f-204">요청된 개체 및 거기에 필요한 모든 개체를 만드는 것을 경우에 따라 *개체 그래프*라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-204">Creating the requested object, and all of the objects it requires, and all of the objects those require, is sometimes referred to as an *object graph*.</span></span> <span data-ttu-id="d989f-205">마찬가지로, 해결해야 하는 종속성이 모인 집합은 일반적으로 *종속성 트리* 또는 *종속성 그래프*라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-205">Likewise, the collective set of dependencies that must be resolved is typically referred to as a *dependency tree* or *dependency graph*.</span></span>

<span data-ttu-id="d989f-206">이 경우 `ICharacterRepository`와 `ApplicationDbContext`는 모두 차례로 `Startup`에서 `ConfigureServices`의 서비스 컨테이너에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-206">In this case, both `ICharacterRepository` and in turn `ApplicationDbContext` must be registered with the services container in `ConfigureServices` in `Startup`.</span></span> <span data-ttu-id="d989f-207">`ApplicationDbContext`는 확장 메서드 `AddDbContext<T>`에 대한 호출로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-207">`ApplicationDbContext` is configured with the call to the extension method `AddDbContext<T>`.</span></span> <span data-ttu-id="d989f-208">다음 코드에서는 `CharacterRepository` 형식의 등록을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-208">The following code shows the registration of the `CharacterRepository` type.</span></span>

[!code-csharp[](dependency-injection/sample/DependencyInjectionSample/Startup.cs?highlight=3-5,11&range=16-32)]

<span data-ttu-id="d989f-209">Entity Framework 컨텍스트는 `Scoped` 수명을 사용하여 서비스 컨테이너에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-209">Entity Framework contexts should be added to the services container using the `Scoped` lifetime.</span></span> <span data-ttu-id="d989f-210">이는 위와 같이 도우미 메서드를 사용할 경우 자동으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-210">This is taken care of automatically if you use the helper methods as shown above.</span></span> <span data-ttu-id="d989f-211">Entity Framework를 사용하게 되는 리포지토리는 동일한 수명을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-211">Repositories that will make use of Entity Framework should use the same lifetime.</span></span>

> [!WARNING]
> <span data-ttu-id="d989f-212">경계해야 할 주요 위험은 Singleton의 `Scoped` 서비스를 해결하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-212">The main danger to be wary of is resolving a `Scoped` service from a singleton.</span></span> <span data-ttu-id="d989f-213">그러한 경우 후속 요청을 처리할 때 서비스가 잘못된 상태일 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-213">It's likely in such a case that the service will have incorrect state when processing subsequent requests.</span></span>

<span data-ttu-id="d989f-214">종속성이 있는 서비스는 컨테이너에 종속성을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-214">Services that have dependencies should register them in the container.</span></span> <span data-ttu-id="d989f-215">서비스의 생성자에게 `string`과 같은 기본 형식이 필요한 경우 [구성](xref:fundamentals/configuration/index) 및 [옵션 패턴](xref:fundamentals/configuration/options)을 사용하여 주입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-215">If a service's constructor requires a primitive, such as a `string`, this can be injected by using [configuration](xref:fundamentals/configuration/index) and the [options pattern](xref:fundamentals/configuration/options).</span></span>

## <a name="service-lifetimes-and-registration-options"></a><span data-ttu-id="d989f-216">서비스 수명 및 등록 옵션</span><span class="sxs-lookup"><span data-stu-id="d989f-216">Service lifetimes and registration options</span></span>

<span data-ttu-id="d989f-217">ASP.NET 서비스는 다음 수명을 사용하여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-217">ASP.NET services can be configured with the following lifetimes:</span></span>

<span data-ttu-id="d989f-218">**Transient**</span><span class="sxs-lookup"><span data-stu-id="d989f-218">**Transient**</span></span>

<span data-ttu-id="d989f-219">Transient 수명 서비스는 요청할 때마다 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-219">Transient lifetime services are created each time they're requested.</span></span> <span data-ttu-id="d989f-220">이 수명은 간단한 상태 비저장 서비스에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-220">This lifetime works best for lightweight, stateless services.</span></span>

<span data-ttu-id="d989f-221">**Scoped**</span><span class="sxs-lookup"><span data-stu-id="d989f-221">**Scoped**</span></span>

<span data-ttu-id="d989f-222">Scoped 수명 서비스는 요청당 한 번만 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-222">Scoped lifetime services are created once per request.</span></span>

> [!WARNING]
> <span data-ttu-id="d989f-223">미들웨어에서 범위가 지정된 서비스를 사용하는 경우 `Invoke` 또는 `InvokeAsync` 메서드에 서비스를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-223">If you're using a scoped service in a middleware, inject the service into the `Invoke` or `InvokeAsync` method.</span></span> <span data-ttu-id="d989f-224">생성자 삽입은 서비스가 싱글톤처럼 작동하게 하므로 이러한 방법으로 삽입하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d989f-224">Don't inject via constructor injection because it forces the service to behave like a singleton.</span></span>

<span data-ttu-id="d989f-225">**Singleton**</span><span class="sxs-lookup"><span data-stu-id="d989f-225">**Singleton**</span></span>

<span data-ttu-id="d989f-226">Singleton 수명 서비스는 처음 요청할 때 만들어집니다(또는 인스턴스를 지정한 경우 `ConfigureServices`가 실행될 때). 그런 다음, 모든 후속 요청이 동일한 인스턴스를 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-226">Singleton lifetime services are created the first time they're requested (or when `ConfigureServices` is run if you specify an instance there) and then every subsequent request will use the same instance.</span></span> <span data-ttu-id="d989f-227">응용 프로그램에 Singleton 동작이 필요한 경우, 자체 클래스에서 Singleton 디자인 패턴을 구현하고 사용자 개체의 수명을 관리하는 대신 서비스 컨테이너가 서비스의 수명을 관리하도록 허용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-227">If your application requires singleton behavior, allowing the services container to manage the service's lifetime is recommended instead of implementing the singleton design pattern and managing your object's lifetime in the class yourself.</span></span>

<span data-ttu-id="d989f-228">서비스는 여러 방법으로 컨테이너에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-228">Services can be registered with the container in several ways.</span></span> <span data-ttu-id="d989f-229">앞에서 우리는 사용할 구체적인 형식을 지정하여 주어진 형식으로 서비스 구현을 등록하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-229">We have already seen how to register a service implementation with a given type by specifying the concrete type to use.</span></span> <span data-ttu-id="d989f-230">또한 요청에 따라 인스턴스를 만드는 데 사용되도록 팩터리를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-230">In addition, a factory can be specified, which will then be used to create the instance on demand.</span></span> <span data-ttu-id="d989f-231">세 번째 방법은 사용할 형식의 인스턴스를 직접 지정하는 것입니다. 이 경우 컨테이너는 인스턴스 생성을 시도하지 않습니다(인스턴스를 제거하지도 않음).</span><span class="sxs-lookup"><span data-stu-id="d989f-231">The third approach is to directly specify the instance of the type to use, in which case the container will never attempt to create an instance (nor will it dispose of the instance).</span></span>

<span data-ttu-id="d989f-232">이러한 수명 및 등록 옵션 간의 차이점을 살펴보려면 하나 이상의 작업을 고유한 ID인 `OperationId`가 있는 *operation*으로 나타내는 간단한 인터페이스를 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="d989f-232">To demonstrate the difference between these lifetime and registration options, consider a simple interface that represents one or more tasks as an *operation* with a unique identifier, `OperationId`.</span></span> <span data-ttu-id="d989f-233">이 서비스에 대한 수명을 구성하는 방법에 따라 컨테이너는 클래스 요청에 동일하거나 다른 서비스 인스턴스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-233">Depending on how we configure the lifetime for this service, the container will provide either the same or different instances of the service to the requesting class.</span></span> <span data-ttu-id="d989f-234">어떤 수명이 요청되었는지 명확히 하기 위해 수명 옵션당 하나의 형식만 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-234">To make it clear which lifetime is being requested, we will create one type per lifetime option:</span></span>

[!code-csharp[](../fundamentals/dependency-injection/sample/DependencyInjectionSample/Interfaces/IOperation.cs?highlight=5-8)]

<span data-ttu-id="d989f-235">해당 생성자에서 `Guid`를 수락하거나, 아무것도 제공되지 않은 경우 새로운 `Guid`를 사용하는, 단일 클래스 `Operation`을 사용하여 이러한 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-235">We implement these interfaces using a single class, `Operation`, that accepts a `Guid` in its constructor, or uses a new `Guid` if none is provided.</span></span>

<span data-ttu-id="d989f-236">다음으로 `ConfigureServices`에서 각 형식이 명명된 수명에 따라 컨테이너에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-236">Next, in `ConfigureServices`, each type is added to the container according to its named lifetime:</span></span>

[!code-csharp[](dependency-injection/sample/DependencyInjectionSample/Startup.cs?range=26-32)]

<span data-ttu-id="d989f-237">`IOperationSingletonInstance` 서비스가 `Guid.Empty`의 알려진 ID의 특정 인스턴스를 사용 중이므로 이 형식을 언제 사용하는지 명확해집니다(해당 Guid는 모두 0이 됨).</span><span class="sxs-lookup"><span data-stu-id="d989f-237">Note that the `IOperationSingletonInstance` service is using a specific instance with a known ID of `Guid.Empty` so it will be clear when this type is in use (its Guid will be all zeroes).</span></span> <span data-ttu-id="d989f-238">또한 `Operation` 형식을 서로 종속하는 `OperationService`를 등록했으므로 이 서비스가 각 작업 형식에 대한 컨트롤러로 동일한 인스턴스를 가져오는지, 아니면 새로운 인스턴스를 가져오는지 여부가 요청 내에서 명확해집니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-238">We have also registered an `OperationService` that depends on each of the other `Operation` types, so that it will be clear within a request whether this service is getting the same instance as the controller, or a new one, for each operation type.</span></span> <span data-ttu-id="d989f-239">이 서비스는 모두 해당 종속성을 속성으로 노출하므로 보기에 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-239">All this service does is expose its dependencies as properties, so they can be displayed in the view.</span></span>

[!code-csharp[](dependency-injection/sample/DependencyInjectionSample/Services/OperationService.cs)]

<span data-ttu-id="d989f-240">응용 프로그램에 대한 서로 다른 개별 요청 내 및 요청 간 개체 수명을 보여 주기 위해 샘플에는 `OperationService` 뿐만 아니라 각 `IOperation` 형식 종류를 요청하는 `OperationsController`가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-240">To demonstrate the object lifetimes within and between separate individual requests to the application, the sample includes an `OperationsController` that requests each kind of `IOperation` type as well as an `OperationService`.</span></span> <span data-ttu-id="d989f-241">그런 다음, `Index` 작업은 모든 컨트롤러 및 서비스의 `OperationId` 값을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-241">The `Index` action then displays all of the controller's and service's `OperationId` values.</span></span>

[!code-csharp[](dependency-injection/sample/DependencyInjectionSample/Controllers/OperationsController.cs)]

<span data-ttu-id="d989f-242">이제 두 개의 개별 요청이 이 컨트롤러 작업에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-242">Now two separate requests are made to this controller action:</span></span>

![첫 번째 요청의 Transient, Scoped, Singleton에 대한 작업 ID 값(GUID), 인스턴스 컨트롤러 및 작업 서비스 작업을 표시하는 Microsoft Edge에서 실행되는 종속성 주입 샘플 웹 응용 프로그램의 작업 보기](dependency-injection/_static/lifetimes_request1.png)

![두 번째 요청의 작업 ID 값을 표시하는 작업 보기.](dependency-injection/_static/lifetimes_request2.png)

<span data-ttu-id="d989f-245">어떤 `OperationId` 값이 요청 내 및 요청 간 달라지는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-245">Observe which of the `OperationId` values vary within a request, and between requests.</span></span>

* <span data-ttu-id="d989f-246">*Transient* 개체는 항상 다릅니다. 새 인스턴스가 모든 컨트롤러 및 모든 서비스에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-246">*Transient* objects are always different; a new instance is provided to every controller and every service.</span></span>

* <span data-ttu-id="d989f-247">*Scoped* 개체는 요청 내에서는 동일하지만 다른 요청에서는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-247">*Scoped* objects are the same within a request, but different across different requests</span></span>

* <span data-ttu-id="d989f-248">*Singleton* 개체는 모든 개체 및 모든 요청에 대해 동일합니다(`ConfigureServices`에 인스턴스 제공 여부에 관계 없이).</span><span class="sxs-lookup"><span data-stu-id="d989f-248">*Singleton* objects are the same for every object and every request (regardless of whether an instance is provided in `ConfigureServices`)</span></span>

## <a name="resolve-a-scoped-service-within-the-application-scope"></a><span data-ttu-id="d989f-249">응용 프로그램 범위 내에서 범위가 지정된 서비스 확인</span><span class="sxs-lookup"><span data-stu-id="d989f-249">Resolve a scoped service within the application scope</span></span>

<span data-ttu-id="d989f-250">[IServiceScopeFactory.CreateScope](/dotnet/api/microsoft.extensions.dependencyinjection.iservicescopefactory.createscope)와 함께 [IServiceScope](/dotnet/api/microsoft.extensions.dependencyinjection.iservicescope)를 만들어 앱 범위 내에서 범위가 지정된 서비스를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-250">Create an [IServiceScope](/dotnet/api/microsoft.extensions.dependencyinjection.iservicescope) with [IServiceScopeFactory.CreateScope](/dotnet/api/microsoft.extensions.dependencyinjection.iservicescopefactory.createscope) to resolve a scoped service within the app's scope.</span></span> <span data-ttu-id="d989f-251">이 방법은 시작 시 범위가 지정된 서비스에 액세스하여 초기화 작업을 실행하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-251">This approach is useful to access a scoped service at startup to run initialization tasks.</span></span> <span data-ttu-id="d989f-252">다음 예제에서는 `Program.Main`에서 `MyScopedService`에 대한 컨텍스트를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-252">The following example shows how to obtain a context for the `MyScopedService` in `Program.Main`:</span></span>

```csharp
public static void Main(string[] args)
{
    var host = BuildWebHost(args);

    using (var serviceScope = host.Services.CreateScope())
    {
        var services = serviceScope.ServiceProvider;

        try
        {
            var serviceContext = services.GetRequiredService<MyScopedService>();
            // Use the context here
        }
        catch (Exception ex)
        {
            var logger = services.GetRequiredService<ILogger<Program>>();
            logger.LogError(ex, "An error occurred.");
        }
    }

    host.Run();
}
```

## <a name="scope-validation"></a><span data-ttu-id="d989f-253">범위 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="d989f-253">Scope validation</span></span>

<span data-ttu-id="d989f-254">앱이 ASP.NET Core 2.0 이상의 개발 환경에서 실행 중인 경우 기본 서비스 공급자가 다음을 확인하는 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-254">When the app is running in the Development environment on ASP.NET Core 2.0 or later, the default service provider performs checks to verify that:</span></span>

* <span data-ttu-id="d989f-255">범위가 지정된 서비스는 루트 서비스 공급자를 통해 간접적 또는 직접으로 확인되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-255">Scoped services aren't directly or indirectly resolved from the root service provider.</span></span>
* <span data-ttu-id="d989f-256">범위가 지정된 서비스는 직접 또는 간접적으로 싱글톤에 삽입되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-256">Scoped services aren't directly or indirectly injected into singletons.</span></span>

<span data-ttu-id="d989f-257">루트 서비스 공급자는 [BuildServiceProvider](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectioncontainerbuilderextensions.buildserviceprovider)를 호출할 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-257">The root service provider is created when [BuildServiceProvider](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectioncontainerbuilderextensions.buildserviceprovider) is called.</span></span> <span data-ttu-id="d989f-258">루트 서비스 공급자의 수명은 공급자가 앱과 함께 시작되고 앱이 종료될 때 삭제되는 앱/서버의 수명에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-258">The root service provider's lifetime corresponds to the app/server's lifetime when the provider starts with the app and is disposed when the app shuts down.</span></span>

<span data-ttu-id="d989f-259">범위가 지정된 서비스는 서비스를 만든 컨테이너에 의해 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-259">Scoped services are disposed by the container that created them.</span></span> <span data-ttu-id="d989f-260">범위가 지정된 서비스가 루트 컨테이너에서 만들어지는 경우 서비스의 수명은 효과적으로 싱글톤으로 승격됩니다. 해당 서비스는 앱/서버가 종료될 때 루트 컨테이너에 의해서만 삭제되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-260">If a scoped service is created in the root container, the service's lifetime is effectively promoted to singleton because it's only disposed by the root container when app/server is shut down.</span></span> <span data-ttu-id="d989f-261">서비스 범위의 유효성 검사는 `BuildServiceProvider`가 호출될 경우 이러한 상황을 catch합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-261">Validating service scopes catches these situations when `BuildServiceProvider` is called.</span></span>

<span data-ttu-id="d989f-262">자세한 내용은 [호스팅 토픽의 범위 유효성 검사](xref:fundamentals/hosting#scope-validation)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d989f-262">For more information, see [Scope validation in the Hosting topic](xref:fundamentals/hosting#scope-validation).</span></span>

## <a name="request-services"></a><span data-ttu-id="d989f-263">요청 서비스</span><span class="sxs-lookup"><span data-stu-id="d989f-263">Request Services</span></span>

<span data-ttu-id="d989f-264">`HttpContext`의 ASP.NET 요청 내에서 사용할 수 있는 서비스는 `RequestServices` 컬렉션을 통해 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-264">The services available within an ASP.NET request from `HttpContext` are exposed through the `RequestServices` collection.</span></span>

![요청 서비스가 요청의 서비스 컨테이너에 대한 액세스를 제공하는 IServiceProvider를 가져오거나 설정했다는 HttpContext 요청 서비스 Intellisense 상황별 대화 상자](dependency-injection/_static/request-services.png)

<span data-ttu-id="d989f-266">요청 서비스는 사용자가 응용 프로그램의 일부로 구성 및 요청한 서비스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-266">Request Services represent the services you configure and request as part of your application.</span></span> <span data-ttu-id="d989f-267">개체가 종속성을 지정한 경우에는 `ApplicationServices`가 아닌 `RequestServices`에 있는 형식으로 충족됩니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-267">When your objects specify dependencies, these are satisfied by the types found in `RequestServices`, not `ApplicationServices`.</span></span>

<span data-ttu-id="d989f-268">일반적으로 이러한 속성을 직접 사용해서는 안 됩니다. 대신 클래스의 생성자를 통해 요청한 클래스 형식을 요청하고 프레임워크에서 이러한 종속성을 주입하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-268">Generally, you shouldn't use these properties directly, preferring instead to request the types your classes you require via your class's constructor, and letting the framework inject these dependencies.</span></span> <span data-ttu-id="d989f-269">이는 더 쉽게 테스트할 수 있고([테스트 및 디버그](../testing/index.md) 참조) 더 느슨하게 결합되는 클래스를 일시 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-269">This yields classes that are easier to test (see [Test and debug](../testing/index.md)) and are more loosely coupled.</span></span>

> [!NOTE]
> <span data-ttu-id="d989f-270">`RequestServices` 컬렉션에 액세스하는 것보다 생성자 매개 변수로 종속성을 요청하는 것을 선호합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-270">Prefer requesting dependencies as constructor parameters to accessing the `RequestServices` collection.</span></span>

## <a name="designing-services-for-dependency-injection"></a><span data-ttu-id="d989f-271">종속성 주입을 위한 서비스 디자인</span><span class="sxs-lookup"><span data-stu-id="d989f-271">Designing services for dependency injection</span></span>

<span data-ttu-id="d989f-272">종속성 주입을 사용하여 자신의 협력자를 가져오도록 서비스를 디자인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-272">You should design your services to use dependency injection to get their collaborators.</span></span> <span data-ttu-id="d989f-273">즉, 서비스 내에서 상태 저장 정적 메서드 호출 사용([정적 집착](http://deviq.com/static-cling/)이라고 알려진 코드 스멜을 야기) 및 종속 클래스의 직접 인스턴스화를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-273">This means avoiding the use of stateful static method calls (which result in a code smell known as [static cling](http://deviq.com/static-cling/)) and the direct instantiation of dependent classes within your services.</span></span> <span data-ttu-id="d989f-274">형식을 인스턴스화할지 아니면 종속성 주입을 통해 요청할 것인지를 선택할 때 [New is Glue](https://ardalis.com/new-is-glue)라는 문구를 기억하는 것이 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-274">It may help to remember the phrase, [New is Glue](https://ardalis.com/new-is-glue), when choosing whether to instantiate a type or to request it via dependency injection.</span></span> <span data-ttu-id="d989f-275">[개체 지향 디자인의 SOLID 원칙](http://deviq.com/solid/)에 따라 클래스는 당연히 작고 잘 구성되며 쉽게 테스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-275">By following the [SOLID Principles of Object Oriented Design](http://deviq.com/solid/), your classes will naturally tend to be small, well-factored, and easily tested.</span></span>

<span data-ttu-id="d989f-276">클래스에 주입해야 할 종속성이 너무 많다면 어떻게 될까요?</span><span class="sxs-lookup"><span data-stu-id="d989f-276">What if you find that your classes tend to have way too many dependencies being injected?</span></span> <span data-ttu-id="d989f-277">이는 일반적으로 클래스가 너무 많은 작업을 시도하고 있으며 아마도 SRP([단일 책임 원칙](http://deviq.com/single-responsibility-principle/))를 위반하고 있다는 신호입니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-277">This is generally a sign that your class is trying to do too much, and is probably violating SRP - the [Single Responsibility Principle](http://deviq.com/single-responsibility-principle/).</span></span> <span data-ttu-id="d989f-278">해당 책임 몇 가지를 새로운 클래스로 이동하여 클래스를 리팩터링할 수 있는지 살펴 보세요.</span><span class="sxs-lookup"><span data-stu-id="d989f-278">See if you can refactor the class by moving some of its responsibilities into a new class.</span></span> <span data-ttu-id="d989f-279">`Controller` 클래스는 UI 고려 사항에 집중해야 하므로, 비즈니스 규칙 및 데이터 액세스 구현 세부 정보는 이러한 [개별 고려 사항](http://deviq.com/separation-of-concerns/)에 적합한 클래스에 유지되어야 한다는 점을 기억하세요.</span><span class="sxs-lookup"><span data-stu-id="d989f-279">Keep in mind that your `Controller` classes should be focused on UI concerns, so business rules and data access implementation details should be kept in classes appropriate to these [separate concerns](http://deviq.com/separation-of-concerns/).</span></span>

<span data-ttu-id="d989f-280">특히 데이터 액세스와 관련하여 `DbContext`를 컨트롤러에 주입할 수 있습니다(EF를 `ConfigureServices`의 서비스 컨테이너에 추가했다고 가정).</span><span class="sxs-lookup"><span data-stu-id="d989f-280">With regards to data access specifically, you can inject the `DbContext` into your controllers (assuming you've added EF to the services container in `ConfigureServices`).</span></span> <span data-ttu-id="d989f-281">일부 개발자는 `DbContext`를 직접 주입하는 대신 데이터베이스에 리포지토리 인터페이스를 사용하는 것을 선호합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-281">Some developers prefer to use a repository interface to the database rather than injecting the `DbContext` directly.</span></span> <span data-ttu-id="d989f-282">인터페이스를 사용하여 데이터 액세스 논리를 한 곳으로 캡슐화하면 데이터베이스가 변경될 때 변경해야 하는 장소 수를 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-282">Using an interface to encapsulate the data access logic in one place can minimize how many places you will have to change when your database changes.</span></span>

### <a name="disposing-of-services"></a><span data-ttu-id="d989f-283">서비스 해제</span><span class="sxs-lookup"><span data-stu-id="d989f-283">Disposing of services</span></span>

<span data-ttu-id="d989f-284">컨테이너는 만든 `IDisposable` 형식에 대해 `Dispose`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-284">The container will call `Dispose` for `IDisposable` types it creates.</span></span> <span data-ttu-id="d989f-285">그러나 인스턴스를 컨테이너에 직접 추가하는 경우에는 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-285">However, if you add an instance to the container yourself, it will not be disposed.</span></span>

<span data-ttu-id="d989f-286">예제:</span><span class="sxs-lookup"><span data-stu-id="d989f-286">Example:</span></span>

```csharp
// Services implement IDisposable:
public class Service1 : IDisposable {}
public class Service2 : IDisposable {}
public class Service3 : IDisposable {}

public interface ISomeService {}
public class SomeServiceImplementation : ISomeService, IDisposable {}


public void ConfigureServices(IServiceCollection services)
{
    // container will create the instance(s) of these types and will dispose them
    services.AddScoped<Service1>();
    services.AddSingleton<Service2>();
    services.AddSingleton<ISomeService>(sp => new SomeServiceImplementation());

    // container didn't create instance so it will NOT dispose it
    services.AddSingleton<Service3>(new Service3());
    services.AddSingleton(new Service3());
}
```

> [!NOTE]
> <span data-ttu-id="d989f-287">버전 1.0에서 컨테이너는 만들지 않은 개체를 포함한 *모든* `IDisposable` 개체에서 dispose를 호출했습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-287">In version 1.0, the container called dispose on *all* `IDisposable` objects, including those it didn't create.</span></span>

## <a name="replacing-the-default-services-container"></a><span data-ttu-id="d989f-288">기본 서비스 컨테이너 대체</span><span class="sxs-lookup"><span data-stu-id="d989f-288">Replacing the default services container</span></span>

<span data-ttu-id="d989f-289">기본 제공 서비스 컨테이너는 프레임워크의 기본 조건 및 이를 기반으로 구성된 대부분의 소비자 응용 프로그램을 제공하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-289">The built-in services container is meant to serve the basic needs of the framework and most consumer applications built on it.</span></span> <span data-ttu-id="d989f-290">그러나 개발자는 기본 제공 컨테이너를 선호하는 컨테이너로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-290">However, developers can replace the built-in container with their preferred container.</span></span> <span data-ttu-id="d989f-291">`ConfigureServices` 메서드는 일반적으로 `void`를 반환하지만, 해당 시그니처가 변경되어 `IServiceProvider`를 반환하는 경우 다른 컨테이너를 구성하거나 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-291">The `ConfigureServices` method typically returns `void`, but if its signature is changed to return `IServiceProvider`, a different container can be configured and returned.</span></span> <span data-ttu-id="d989f-292">.NET에서 사용 가능한 많은 IOC 컨테이너가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-292">There are many IOC containers available for .NET.</span></span> <span data-ttu-id="d989f-293">이 예제에서는 [Autofac](https://autofac.org/) 패키지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-293">In this example, the [Autofac](https://autofac.org/) package is used.</span></span>

<span data-ttu-id="d989f-294">먼저, 적절한 컨테이너 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-294">First, install the appropriate container package(s):</span></span>

* `Autofac`
* `Autofac.Extensions.DependencyInjection`

<span data-ttu-id="d989f-295">그런 다음, 컨테이너를 `ConfigureServices`에 구성하고 `IServiceProvider`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-295">Next, configure the container in `ConfigureServices` and return an `IServiceProvider`:</span></span>

```csharp
public IServiceProvider ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
    // Add other framework services

    // Add Autofac
    var containerBuilder = new ContainerBuilder();
    containerBuilder.RegisterModule<DefaultModule>();
    containerBuilder.Populate(services);
    var container = containerBuilder.Build();
    return new AutofacServiceProvider(container);
}
```

> [!NOTE]
> <span data-ttu-id="d989f-296">타사 DI 컨테이너를 사용하는 경우 `void` 대신 `IServiceProvider`를 반환하도록 `ConfigureServices`를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-296">When using a third-party DI container, you must change `ConfigureServices` so that it returns `IServiceProvider` instead of `void`.</span></span>

<span data-ttu-id="d989f-297">마지막으로 `DefaultModule`에서 Autofac을 정상적으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-297">Finally, configure Autofac as normal in `DefaultModule`:</span></span>

```csharp
public class DefaultModule : Module
{
    protected override void Load(ContainerBuilder builder)
    {
        builder.RegisterType<CharacterRepository>().As<ICharacterRepository>();
    }
}
```

<span data-ttu-id="d989f-298">런타임 시 형식을 확인하고 종속성을 주입하는 데 Autofac이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-298">At runtime, Autofac will be used to resolve types and inject dependencies.</span></span> <span data-ttu-id="d989f-299">[Autofac 및 ASP.NET Core를 사용하는 방법에 대해 자세히 알아보세요](http://docs.autofac.org/en/latest/integration/aspnetcore.html).</span><span class="sxs-lookup"><span data-stu-id="d989f-299">[Learn more about using Autofac and ASP.NET Core](http://docs.autofac.org/en/latest/integration/aspnetcore.html).</span></span>

### <a name="thread-safety"></a><span data-ttu-id="d989f-300">스레드로부터의 안전성</span><span class="sxs-lookup"><span data-stu-id="d989f-300">Thread safety</span></span>

<span data-ttu-id="d989f-301">Singleton 서비스는 스레드로부터 안전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-301">Singleton services need to be thread safe.</span></span> <span data-ttu-id="d989f-302">Singleton 서비스가 Transient 서비스에 대한 종속성을 갖는 경우 Transient 서비스는 Singleton에서 사용되는 방식에 따라 스레드로부터 안전해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-302">If a singleton service has a dependency on a transient service, the transient service may also need to be thread safe depending how it's used by the singleton.</span></span>

## <a name="recommendations"></a><span data-ttu-id="d989f-303">권장 사항</span><span class="sxs-lookup"><span data-stu-id="d989f-303">Recommendations</span></span>

<span data-ttu-id="d989f-304">종속성 주입을 사용할 때는 다음 권장 사항을 염두에 둬야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-304">When working with dependency injection, keep the following recommendations in mind:</span></span>

* <span data-ttu-id="d989f-305">DI는 복잡한 종속성이 있는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-305">DI is for objects that have complex dependencies.</span></span> <span data-ttu-id="d989f-306">컨트롤러, 서비스, 어댑터 및 리포지토리는 모두 DI에 추가할 수도 있는 개체의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-306">Controllers, services, adapters, and repositories are all examples of objects that might be added to DI.</span></span>

* <span data-ttu-id="d989f-307">데이터 및 구성을 DI에 직접 저장하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="d989f-307">Avoid storing data and configuration directly in DI.</span></span> <span data-ttu-id="d989f-308">예를 들어 사용자의 쇼핑 카트는 일반적으로 서비스 컨테이너에 추가하지 말아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-308">For example, a user's shopping cart shouldn't typically be added to the services container.</span></span> <span data-ttu-id="d989f-309">구성은 [옵션 패턴](xref:fundamentals/configuration/options)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-309">Configuration should use the [options pattern](xref:fundamentals/configuration/options).</span></span> <span data-ttu-id="d989f-310">마찬가지로 다른 일부 개체에 대한 액세스를 허용하기 위해서만 존재하는 “데이터 보유자” 개체를 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="d989f-310">Similarly, avoid "data holder" objects that only exist to allow access to some other object.</span></span> <span data-ttu-id="d989f-311">가능한 경우 DI를 통해 필요한 실제 항목을 요청하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-311">It's better to request the actual item needed via DI, if possible.</span></span>

* <span data-ttu-id="d989f-312">서비스에 정적 액세스를 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="d989f-312">Avoid static access to services.</span></span>

* <span data-ttu-id="d989f-313">응용 프로그램 코드에서 서비스 위치를 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="d989f-313">Avoid service location in your application code.</span></span>

* <span data-ttu-id="d989f-314">`HttpContext`에 정적 액세스를 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="d989f-314">Avoid static access to `HttpContext`.</span></span>

<span data-ttu-id="d989f-315">모든 권장 사항과 마찬가지로, 하나를 무시해야 하는 상황이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-315">Like all sets of recommendations, you may encounter situations where ignoring one is required.</span></span> <span data-ttu-id="d989f-316">예외는 드물었습니다. 대부분 매우 특별한 사례는 프레임워크 자체 내에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-316">We have found exceptions to be rare -- mostly very special cases within the framework itself.</span></span>

<span data-ttu-id="d989f-317">종속성 주입은 정적/전역 개체 액세스 패턴의 *대안*입니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-317">Dependency injection is an *alternative* to static/global object access patterns.</span></span> <span data-ttu-id="d989f-318">고정 개체 액세스와 함께 사용할 경우 DI의 장점을 실현할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d989f-318">You may not be able to realize the benefits of DI if you mix it with static object access.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d989f-319">추가 자료</span><span class="sxs-lookup"><span data-stu-id="d989f-319">Additional resources</span></span>

* [<span data-ttu-id="d989f-320">뷰에 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="d989f-320">Dependency injection into views</span></span>](xref:mvc/views/dependency-injection)
* [<span data-ttu-id="d989f-321">컨트롤러에 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="d989f-321">Dependency injection into controllers</span></span>](xref:mvc/controllers/dependency-injection)
* [<span data-ttu-id="d989f-322">요구 사항 처리기의 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="d989f-322">Dependency injection in requirement handlers</span></span>](xref:security/authorization/dependencyinjection)
* [<span data-ttu-id="d989f-323">응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="d989f-323">Application Startup</span></span>](xref:fundamentals/startup)
* [<span data-ttu-id="d989f-324">테스트 및 디버그</span><span class="sxs-lookup"><span data-stu-id="d989f-324">Test and debug</span></span>](xref:testing/index)
* [<span data-ttu-id="d989f-325">팩터리 기반 미들웨어 활성화</span><span class="sxs-lookup"><span data-stu-id="d989f-325">Factory-based middleware activation</span></span>](xref:fundamentals/middleware/extensibility)
* [<span data-ttu-id="d989f-326">종속성 주입으로 ASP.NET Core에 정리 코드 작성(MSDN)</span><span class="sxs-lookup"><span data-stu-id="d989f-326">Writing Clean Code in ASP.NET Core with Dependency Injection (MSDN)</span></span>](https://msdn.microsoft.com/magazine/mt703433.aspx)
* [<span data-ttu-id="d989f-327">컨테이너 관리 응용 프로그램 디자인, 서막: 컨테이너는 어디에 속합니까?</span><span class="sxs-lookup"><span data-stu-id="d989f-327">Container-Managed Application Design, Prelude: Where does the Container Belong?</span></span>](https://blogs.msdn.microsoft.com/nblumhardt/2008/12/26/container-managed-application-design-prelude-where-does-the-container-belong/)
* [<span data-ttu-id="d989f-328">명시적 종속성 원칙</span><span class="sxs-lookup"><span data-stu-id="d989f-328">Explicit Dependencies Principle</span></span>](http://deviq.com/explicit-dependencies-principle/)
* <span data-ttu-id="d989f-329">[Inversion of Control 컨테이너 및 종속성 주입 패턴](https://www.martinfowler.com/articles/injection.html)(Fowler)</span><span class="sxs-lookup"><span data-stu-id="d989f-329">[Inversion of Control Containers and the Dependency Injection Pattern](https://www.martinfowler.com/articles/injection.html) (Fowler)</span></span>
