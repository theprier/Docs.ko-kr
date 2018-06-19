---
title: ASP.NET Core의 컨트롤러에 종속성 주입
author: ardalis
description: ASP.NET Core MVC 컨트롤러가 ASP.NET Core의 종속성 주입을 사용하여 해당 생성자를 통해 명시적으로 해당 종속성을 요청하는 방법을 알아봅니다.
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/controllers/dependency-injection
ms.openlocfilehash: c3e26d294d51dc7044158b05c1ac39015c494610
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
ms.locfileid: "30071804"
---
# <a name="dependency-injection-into-controllers-in-aspnet-core"></a><span data-ttu-id="28eb1-103">ASP.NET Core의 컨트롤러에 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="28eb1-103">Dependency injection into controllers in ASP.NET Core</span></span>

<a name="dependency-injection-controllers"></a>

<span data-ttu-id="28eb1-104">작성자: [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="28eb1-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="28eb1-105">ASP.NET Core MVC 컨트롤러는 해당 생성자를 통해 명시적으로 해당 종속성을 요청해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-105">ASP.NET Core MVC controllers should request their dependencies explicitly via their constructors.</span></span> <span data-ttu-id="28eb1-106">경우에 따라 개별 컨트롤러 작업에는 서비스가 필요할 수 있으며, 컨트롤러 수준에서 요청하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-106">In some instances, individual controller actions may require a service, and it may not make sense to request at the controller level.</span></span> <span data-ttu-id="28eb1-107">이 경우에 작업 메서드의 매개 변수로 서비스를 주입할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-107">In this case, you can also choose to inject a service as a parameter on the action method.</span></span>

<span data-ttu-id="28eb1-108">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/dependency-injection/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="28eb1-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/controllers/dependency-injection/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="dependency-injection"></a><span data-ttu-id="28eb1-109">종속성 주입</span><span class="sxs-lookup"><span data-stu-id="28eb1-109">Dependency Injection</span></span>

<span data-ttu-id="28eb1-110">종속성 주입은 [종속성 반전 원칙](http://deviq.com/dependency-inversion-principle/)을 따르는 기술로, 응용 프로그램을 느슨하게 결합된 모듈로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-110">Dependency injection is a technique that follows the [Dependency Inversion Principle](http://deviq.com/dependency-inversion-principle/), allowing for applications to be composed of loosely coupled modules.</span></span> <span data-ttu-id="28eb1-111">ASP.NET Core는 [종속성 주입](../../fundamentals/dependency-injection.md)을 기본적으로 지원하므로 응용 프로그램을 더 쉽게 테스트하고 유지 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-111">ASP.NET Core has built-in support for [dependency injection](../../fundamentals/dependency-injection.md), which makes applications easier to test and maintain.</span></span>

## <a name="constructor-injection"></a><span data-ttu-id="28eb1-112">생성자 주입</span><span class="sxs-lookup"><span data-stu-id="28eb1-112">Constructor Injection</span></span>

<span data-ttu-id="28eb1-113">생성자 기반 종속성 주입을 위한 ASP.NET Core의 기본 지원은 MVC 컨트롤러까지 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-113">ASP.NET Core's built-in support for constructor-based dependency injection extends to MVC controllers.</span></span> <span data-ttu-id="28eb1-114">컨트롤러에 서비스 형식을 생성자 매개 변수로 추가하기만 하면 ASP.NET Core는 서비스 컨테이너의 기본 기능을 사용하여 해당 형식을 확인하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-114">By simply adding a service type to your controller as a constructor parameter, ASP.NET Core will attempt to resolve that type using its built in service container.</span></span> <span data-ttu-id="28eb1-115">서비스는 항상 그렇지는 않지만 일반적으로 인터페이스를 사용하여 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-115">Services are typically, but not always, defined using interfaces.</span></span> <span data-ttu-id="28eb1-116">예를 들어 현재 시간에 따라 달라지는 비즈니스 논리가 응용 프로그램에 있는 경우, 설정된 시간을 사용하는 구현에서 테스트가 통과될 수 있도록 시간을 검색하는(하드코딩이 아님) 서비스를 주입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-116">For example, if your application has business logic that depends on the current time, you can inject a service that retrieves the time (rather than hard-coding it), which would allow your tests to pass in implementations that use a set time.</span></span>

[!code-csharp[](dependency-injection/sample/src/ControllerDI/Interfaces/IDateTime.cs)]


<span data-ttu-id="28eb1-117">런타임 시 시스템 클록을 사용하도록 이와 같은 인터페이스를 구현하는 것은 매우 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-117">Implementing an interface like this one so that it uses the system clock at runtime is trivial:</span></span>

[!code-csharp[](dependency-injection/sample/src/ControllerDI/Services/SystemDateTime.cs)]


<span data-ttu-id="28eb1-118">준비된 이 항목을 통해 컨트롤러에서 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-118">With this in place, we can use the service in our controller.</span></span> <span data-ttu-id="28eb1-119">이 경우 시간에 따라 사용자에게 인사말을 표시하도록 일부 논리를 `HomeController` `Index` 메서드에 추가하였습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-119">In this case, we have added some logic to the `HomeController` `Index` method to display a greeting to the user based on the time of day.</span></span>

[!code-csharp[](./dependency-injection/sample/src/ControllerDI/Controllers/HomeController.cs?highlight=8,10,12,17,18,19,20,21,22,23,24,25,26,27,28,29,30&range=1-31,51-52)]

<span data-ttu-id="28eb1-120">지금 응용 프로그램을 실행하는 경우 오류가 발생할 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-120">If we run the application now, we will most likely encounter an error:</span></span>

```
An unhandled exception occurred while processing the request.

InvalidOperationException: Unable to resolve service for type 'ControllerDI.Interfaces.IDateTime' while attempting to activate 'ControllerDI.Controllers.HomeController'.
Microsoft.Extensions.DependencyInjection.ActivatorUtilities.GetService(IServiceProvider sp, Type type, Type requiredBy, Boolean isDefaultParameterRequired)
```

<span data-ttu-id="28eb1-121">이 오류는 `Startup` 클래스의 `ConfigureServices` 메서드에서 서비스를 구성하지 않은 경우에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-121">This error occurs when we have not configured a service in the `ConfigureServices` method in our `Startup` class.</span></span> <span data-ttu-id="28eb1-122">`IDateTime`에 대한 요청이 `SystemDateTime`의 인스턴스를 사용하여 확인되도록 지정하려면 아래 목록에서 강조 표시된 줄을 `ConfigureServices` 메서드에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-122">To specify that requests for `IDateTime` should be resolved using an instance of `SystemDateTime`, add the highlighted line in the listing below to your `ConfigureServices` method:</span></span>

[!code-csharp[](./dependency-injection/sample/src/ControllerDI/Startup.cs?highlight=4&range=26-27,42-44)]

> [!NOTE]
> <span data-ttu-id="28eb1-123">이 특정 서비스는 여러 가지 다른 수명 옵션 중 하나를 사용하여 구현할 수 있습니다(`Transient`, `Scoped` 또는 `Singleton`).</span><span class="sxs-lookup"><span data-stu-id="28eb1-123">This particular service could be implemented using any of several different lifetime options (`Transient`, `Scoped`, or `Singleton`).</span></span> <span data-ttu-id="28eb1-124">각 범위 옵션이 서비스의 동작에 미치는 영향을 이해하려면 [종속성 주입](../../fundamentals/dependency-injection.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="28eb1-124">See [Dependency Injection](../../fundamentals/dependency-injection.md) to understand how each of these scope options will affect the behavior of your service.</span></span>

<span data-ttu-id="28eb1-125">서비스를 한 번 구성하면 응용 프로그램을 실행하고 홈 페이지로 이동할 때 시간 기반 메시지가 예상대로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-125">Once the service has been configured, running the application and navigating to the home page should display the time-based message as expected:</span></span>

![서버 인사말](dependency-injection/_static/server-greeting.png)

>[!TIP]
> <span data-ttu-id="28eb1-127">컨트롤러에서 종속성 [http://deviq.com/explicit-dependencies-principle/](http://deviq.com/explicit-dependencies-principle/)을 명시적으로 요청하여 코드를 더 쉽게 테스트할 수 있는 방법을 알아보려면 [컨트롤러 논리 테스트](testing.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="28eb1-127">See [Test controller logic](testing.md) to learn how to explicitly request dependencies [http://deviq.com/explicit-dependencies-principle/](http://deviq.com/explicit-dependencies-principle/) in controllers makes code easier to test.</span></span>

<span data-ttu-id="28eb1-128">ASP.NET Core의 기본 제공 종속성 주입은 클래스 요청 서비스에 대해 단일 생성자만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-128">ASP.NET Core's built-in dependency injection supports having only a single constructor for classes requesting services.</span></span> <span data-ttu-id="28eb1-129">생성자가 둘 이상인 경우 다음과 같은 예외가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-129">If you have more than one constructor, you may get an exception stating:</span></span>

```
An unhandled exception occurred while processing the request.

InvalidOperationException: Multiple constructors accepting all given argument types have been found in type 'ControllerDI.Controllers.HomeController'. There should only be one applicable constructor.
Microsoft.Extensions.DependencyInjection.ActivatorUtilities.FindApplicableConstructor(Type instanceType, Type[] argumentTypes, ConstructorInfo& matchingConstructor, Nullable`1[]& parameterMap)
```

<span data-ttu-id="28eb1-130">오류 메시지에 나타난 대로 생성자가 하나여야 이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-130">As the error message states, you can correct this problem having just a single constructor.</span></span> <span data-ttu-id="28eb1-131">또한 [기본 종속성 주입 지원을 제3자 구현으로 대체](../../fundamentals/dependency-injection.md#replacing-the-default-services-container)할 수 있습니다. 다수는 여러 생성자를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-131">You can also [replace the default dependency injection support with a third party implementation](../../fundamentals/dependency-injection.md#replacing-the-default-services-container), many of which support multiple constructors.</span></span>

## <a name="action-injection-with-fromservices"></a><span data-ttu-id="28eb1-132">FromServices로 작업 삽입</span><span class="sxs-lookup"><span data-stu-id="28eb1-132">Action Injection with FromServices</span></span>

<span data-ttu-id="28eb1-133">경우에 따라 컨트롤러 내에서 둘 이상의 작업에 서비스가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-133">Sometimes you don't need a service for more than one action within your controller.</span></span> <span data-ttu-id="28eb1-134">이 경우 서비스를 매개 변수로 작업 메서드에 삽입을 하는 것이 적절할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-134">In this case, it may make sense to inject the service as a parameter to the action method.</span></span> <span data-ttu-id="28eb1-135">이는 다음과 같이 `[FromServices]` 특성으로 매개 변수를 표시하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-135">This is done by marking the parameter with the attribute `[FromServices]` as shown here:</span></span>

[!code-csharp[](./dependency-injection/sample/src/ControllerDI/Controllers/HomeController.cs?highlight=1&range=33-38)]

## <a name="accessing-settings-from-a-controller"></a><span data-ttu-id="28eb1-136">컨트롤러에서 설정 액세스</span><span class="sxs-lookup"><span data-stu-id="28eb1-136">Accessing Settings from a Controller</span></span>

<span data-ttu-id="28eb1-137">컨트롤러 내에서 응용 프로그램 또는 구성 설정에 액세스하는 것은 일반적인 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-137">Accessing application or configuration settings from within a controller is a common pattern.</span></span> <span data-ttu-id="28eb1-138">이 액세스는 [구성](xref:fundamentals/configuration/index)에 설명된 옵션 패턴을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-138">This access should use the Options pattern described in [configuration](xref:fundamentals/configuration/index).</span></span> <span data-ttu-id="28eb1-139">일반적으로 종속성 주입을 사용하여 컨트롤러에서 직접 설정을 요청해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-139">You generally shouldn't request settings directly from your controller using dependency injection.</span></span> <span data-ttu-id="28eb1-140">더 나은 방법은 `IOptions<T>` 인스턴스를 요청하는 것입니다. 여기서 `T`란 필요한 구성 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-140">A better approach is to request an `IOptions<T>` instance, where `T` is the configuration class you need.</span></span>

<span data-ttu-id="28eb1-141">옵션 패턴을 사용하려면 다음과 같은 옵션을 나타내는 클래스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-141">To work with the options pattern, you need to create a class that represents the options, such as this one:</span></span>

[!code-csharp[](dependency-injection/sample/src/ControllerDI/Model/SampleWebSettings.cs)]

<span data-ttu-id="28eb1-142">그런 다음, 옵션 모델을 사용하도록 응용 프로그램을 구성하고, 구성 클래스를 `ConfigureServices`의 서비스 컬렉션에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-142">Then you need to configure the application to use the options model and add your configuration class to the services collection in `ConfigureServices`:</span></span>

[!code-csharp[](./dependency-injection/sample/src/ControllerDI/Startup.cs?highlight=3,4,5,6,9,16,19&range=14-44)]

> [!NOTE]
> <span data-ttu-id="28eb1-143">위의 목록에서 JSON 형식 파일에서 설정을 읽도록 응용 프로그램을 구성하는 중 입니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-143">In the above listing, we are configuring the application to read the settings from a JSON-formatted file.</span></span> <span data-ttu-id="28eb1-144">또한 위의 주석으로 처리된 코드에 표시된 대로 코드에서 완전히 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-144">You can also configure the settings entirely in code, as is shown in the commented code above.</span></span> <span data-ttu-id="28eb1-145">추가 구성 옵션은 [구성](xref:fundamentals/configuration/index)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="28eb1-145">See [Configuration](xref:fundamentals/configuration/index) for further configuration options.</span></span>

<span data-ttu-id="28eb1-146">강력한 형식의 구성 개체를 지정하고(이 경우 `SampleWebSettings`) 서비스 컬렉션에 추가하고 나면, `IOptions<T>`의 인스턴스(이 경우 `IOptions<SampleWebSettings>`)를 요청하여 모든 컨트롤러 또는 작업 메서드에서 이를 요청할 수 있습니다 .</span><span class="sxs-lookup"><span data-stu-id="28eb1-146">Once you've specified a strongly-typed configuration object (in this case, `SampleWebSettings`) and added it to the services collection, you can request it from any Controller or Action method by requesting an instance of `IOptions<T>` (in this case, `IOptions<SampleWebSettings>`).</span></span> <span data-ttu-id="28eb1-147">다음 코드는 컨트롤러에서 설정을 요청하는 방법 중 하나를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-147">The following code shows how one would request the settings from a controller:</span></span>

[!code-csharp[](./dependency-injection/sample/src/ControllerDI/Controllers/SettingsController.cs?highlight=3,5,7&range=7-22)]

<span data-ttu-id="28eb1-148">옵션 패턴을 따르면 설정 및 구성을 서로 분리할 수 있으며, 컨트롤러가 [문제의 분리](http://deviq.com/separation-of-concerns/)를 따르고 있는지 확인합니다. 컨트롤러는 설정 정보를 찾는 방법이나 위치를 알 필요가 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-148">Following the Options pattern allows settings and configuration to be decoupled from one another, and ensures the controller is following [separation of concerns](http://deviq.com/separation-of-concerns/), since it doesn't need to know how or where to find the settings information.</span></span> <span data-ttu-id="28eb1-149">또한 컨트롤러가 더 쉽게 [컨트롤러 논리 테스트](testing.md)를 단위 테스트할 수 있습니다. 컨트롤러 클래스 내 설정 클래스의 [정적 집착](http://deviq.com/static-cling/) 또는 직접 인스턴스화가 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="28eb1-149">It also makes the controller easier to unit test [Test controller logic](testing.md), since there's no [static cling](http://deviq.com/static-cling/) or direct instantiation of settings classes within the controller class.</span></span>
