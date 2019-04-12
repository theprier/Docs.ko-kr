---
title: Razor 구성 요소 종속성 주입
author: guardrex
description: Blazor 및 Razor 구성 요소 앱 services을 사용 하 여 구성 요소를 삽입 하 여는 방법을 참조 하세요.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 03/27/2019
uid: razor-components/dependency-injection
ms.openlocfilehash: 40aec2e3a5032039c7d921f67d7d333b03c07fb1
ms.sourcegitcommit: 3e9e1f6d572947e15347e818f769e27dea56b648
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2019
ms.locfileid: "59515612"
---
# <a name="razor-components-dependency-injection"></a><span data-ttu-id="fb93c-103">Razor 구성 요소 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="fb93c-103">Razor Components dependency injection</span></span>

<span data-ttu-id="fb93c-104">[Rainer Stropek](https://www.timecockpit.com)</span><span class="sxs-lookup"><span data-stu-id="fb93c-104">By [Rainer Stropek](https://www.timecockpit.com)</span></span>

<span data-ttu-id="fb93c-105">Razor 구성 요소 지원 [종속성 주입 (DI)](xref:fundamentals/dependency-injection)합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-105">Razor Components supports [dependency injection (DI)](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="fb93c-106">앱 구성 요소를 삽입 하 여 기본 제공 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-106">Apps can use built-in services by injecting them into components.</span></span> <span data-ttu-id="fb93c-107">앱 수 또한 정의 및 사용자 지정 서비스를 등록 하 고 앱 전체에서 DI 통해 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-107">Apps can also define and register custom services and make them available throughout the app via DI.</span></span>

## <a name="dependency-injection"></a><span data-ttu-id="fb93c-108">종속성 주입</span><span class="sxs-lookup"><span data-stu-id="fb93c-108">Dependency injection</span></span>

<span data-ttu-id="fb93c-109">DI는 중앙 위치에 구성 된 서비스에 액세스 하기 위한 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-109">DI is a technique for accessing services configured in a central location.</span></span> <span data-ttu-id="fb93c-110">이 Razor 구성 요소 앱에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-110">This can be useful in Razor Components apps to:</span></span>

* <span data-ttu-id="fb93c-111">라고 하는 여러 구성 요소 간에 서비스 클래스의 단일 인스턴스를 공유를 *singleton* 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-111">Share a single instance of a service class across many components, known as a *singleton* service.</span></span>
* <span data-ttu-id="fb93c-112">참조 추상화를 사용 하 여 구체적인 서비스 클래스에서 구성 요소를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-112">Decouple components from concrete service classes by using reference abstractions.</span></span> <span data-ttu-id="fb93c-113">예를 들어 인터페이스 `IDataAccess` 앱에서 데이터에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-113">For example, consider an interface `IDataAccess` for accessing data in the app.</span></span> <span data-ttu-id="fb93c-114">인터페이스를 구현 하는 구체적으로 `DataAccess` 클래스 및 응용 프로그램의 서비스 컨테이너에서 서비스로 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-114">The interface is implemented by a concrete `DataAccess` class and registered as a service in the app's service container.</span></span> <span data-ttu-id="fb93c-115">구성 요소를 수신 하는 데 DI를 사용 하는 경우는 `IDataAccess` 구현, 구성 요소는 구체적인 형식 결합 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-115">When a component uses DI to receive an `IDataAccess` implementation, the component isn't coupled to the concrete type.</span></span> <span data-ttu-id="fb93c-116">아마도 단위 테스트에서 모의 구현을 구현을 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-116">The implementation can be swapped, perhaps to a mock implementation in unit tests.</span></span>

<span data-ttu-id="fb93c-117">자세한 내용은 <xref:fundamentals/dependency-injection>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb93c-117">For more information, see <xref:fundamentals/dependency-injection>.</span></span>

## <a name="add-services-to-di"></a><span data-ttu-id="fb93c-118">DI에 서비스 추가</span><span class="sxs-lookup"><span data-stu-id="fb93c-118">Add services to DI</span></span>

<span data-ttu-id="fb93c-119">새 앱을 만든 후 검사를 `Startup.ConfigureServices` 메서드:</span><span class="sxs-lookup"><span data-stu-id="fb93c-119">After creating a new app, examine the `Startup.ConfigureServices` method:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Add custom services here
}
```

<span data-ttu-id="fb93c-120">`ConfigureServices` 메서드에 전달 되는 <xref:Microsoft.Extensions.DependencyInjection.IServiceCollection>, 서비스 설명자 개체의 목록입니다 (<xref:Microsoft.Extensions.DependencyInjection.ServiceDescriptor>).</span><span class="sxs-lookup"><span data-stu-id="fb93c-120">The `ConfigureServices` method is passed an <xref:Microsoft.Extensions.DependencyInjection.IServiceCollection>, which is a list of service descriptor objects (<xref:Microsoft.Extensions.DependencyInjection.ServiceDescriptor>).</span></span> <span data-ttu-id="fb93c-121">서비스는 서비스 컬렉션에 대 한 서비스 설명자를 제공 하 여 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-121">Services are added by providing service descriptors to the service collection.</span></span> <span data-ttu-id="fb93c-122">다음 예제에서는 사용 하 여 개념은 `IDataAccess` 인터페이스 및 구체적인 구현 `DataAccess`:</span><span class="sxs-lookup"><span data-stu-id="fb93c-122">The following example demonstrates the concept with the `IDataAccess` interface and its concrete implementation `DataAccess`:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<IDataAccess, DataAccess>();
}
```

<span data-ttu-id="fb93c-123">다음 표에 나와 있는 수명을 사용 하 여 서비스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-123">Services can be configured with the lifetimes shown in the following table.</span></span>

| <span data-ttu-id="fb93c-124">수명</span><span class="sxs-lookup"><span data-stu-id="fb93c-124">Lifetime</span></span> | <span data-ttu-id="fb93c-125">설명</span><span class="sxs-lookup"><span data-stu-id="fb93c-125">Description</span></span> |
| -------- | ----------- |
| <xref:Microsoft.Extensions.DependencyInjection.ServiceDescriptor.Singleton*> | <span data-ttu-id="fb93c-126">DI 만듭니다는 *단일 인스턴스* 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-126">DI creates a *single instance* of the service.</span></span> <span data-ttu-id="fb93c-127">필요한 모든 구성 요소는 `Singleton` 서비스는 동일한 서비스의 인스턴스를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-127">All components requiring a `Singleton` service receive an instance of the same service.</span></span> |
| <xref:Microsoft.Extensions.DependencyInjection.ServiceDescriptor.Transient*> | <span data-ttu-id="fb93c-128">구성 요소를 때마다의 인스턴스를 가져옵니다을 `Transient` 서비스 수신한 서비스 컨테이너에서를 *새 인스턴스* 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-128">Whenever a component obtains an instance of a `Transient` service from the service container, it receives a *new instance* of the service.</span></span> |
| <xref:Microsoft.Extensions.DependencyInjection.ServiceDescriptor.Scoped*> | <span data-ttu-id="fb93c-129">현재 클라이언트 쪽 Blazor DI 범위 개념이 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-129">Client-side Blazor doesn't currently have the concept of DI scopes.</span></span> <span data-ttu-id="fb93c-130">`Scoped` 처럼 `Singleton`합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-130">`Scoped` behaves like `Singleton`.</span></span> <span data-ttu-id="fb93c-131">그러나 ASP.NET Core Razor 구성 요소를 지원 합니다 `Scoped` 수명입니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-131">However, ASP.NET Core Razor Components support the `Scoped` lifetime.</span></span> <span data-ttu-id="fb93c-132">Razor 구성 요소를 연결으로 범위가 지정 된 서비스를 등록 하는 범위가 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-132">In a Razor Component, a scoped service registration is scoped to the connection.</span></span> <span data-ttu-id="fb93c-133">이러한 이유로 범위가 지정 된 서비스를 사용 하는 현재 사용자에 게 범위가 지정 되어야 합니다는 서비스에 대 한 기본 현재는 클라이언트 쪽에서 실행 하는 경우에 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-133">For this reason, using scoped services is preferred for services that should be scoped to the current user, even if the current intent is to run client-side in the browser.</span></span> |

<span data-ttu-id="fb93c-134">DI 시스템은 ASP.NET Core에서 DI 시스템을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-134">The DI system is based on the DI system in ASP.NET Core.</span></span> <span data-ttu-id="fb93c-135">자세한 내용은 <xref:fundamentals/dependency-injection>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb93c-135">For more information, see <xref:fundamentals/dependency-injection>.</span></span>

## <a name="default-services"></a><span data-ttu-id="fb93c-136">기본 서비스</span><span class="sxs-lookup"><span data-stu-id="fb93c-136">Default services</span></span>

<span data-ttu-id="fb93c-137">기본 서비스는 앱의 서비스 컬렉션에 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-137">Default services are automatically added to the app's service collection.</span></span>

| <span data-ttu-id="fb93c-138">서비스</span><span class="sxs-lookup"><span data-stu-id="fb93c-138">Service</span></span> | <span data-ttu-id="fb93c-139">설명</span><span class="sxs-lookup"><span data-stu-id="fb93c-139">Description</span></span> |
| ------- | ----------- |
| <xref:System.Net.Http.HttpClient> | <span data-ttu-id="fb93c-140">HTTP 요청 송수신 (singleton) URI로 식별 되는 리소스에서 HTTP 응답에 대 한 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-140">Provides methods for sending HTTP requests and receiving HTTP responses from a resource identified by a URI (singleton).</span></span> <span data-ttu-id="fb93c-141">이 인스턴스의 `HttpClient` 브라우저를 사용 하 여 백그라운드에서 HTTP 트래픽을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-141">Note that this instance of `HttpClient` uses the browser for handling the HTTP traffic in the background.</span></span> <span data-ttu-id="fb93c-142">[HttpClient.BaseAddress](xref:System.Net.Http.HttpClient.BaseAddress) 앱의 기본 URI 접두사를 자동으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-142">[HttpClient.BaseAddress](xref:System.Net.Http.HttpClient.BaseAddress) is automatically set to the base URI prefix of the app.</span></span> <span data-ttu-id="fb93c-143">`HttpClient` 클라이언트 쪽 Blazor 앱에만 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-143">`HttpClient` is only provided to client-side Blazor apps.</span></span> |
| `IJSRuntime` | <span data-ttu-id="fb93c-144">호출 될 수 있습니다 디스패치해야 하는 JavaScript 런타임 인스턴스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-144">Represents an instance of a JavaScript runtime to which calls may be dispatched.</span></span> <span data-ttu-id="fb93c-145">자세한 내용은 <xref:razor-components/javascript-interop>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb93c-145">For more information, see <xref:razor-components/javascript-interop>.</span></span> |
| `IUriHelper` | <span data-ttu-id="fb93c-146">Uri 및 탐색 상태 (단일 항목)를 사용 하 여 작업에 대 한 도우미를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-146">Contains helpers for working with URIs and navigation state (singleton).</span></span> <span data-ttu-id="fb93c-147">`IUriHelper` Blazor 및 Razor 구성 요소를 모두 앱에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-147">`IUriHelper` is provided to both Blazor and Razor Components apps.</span></span> |

<span data-ttu-id="fb93c-148">기본 템플릿을 통해 추가 하는 기본 서비스 공급자 대신 사용자 지정 서비스 공급자를 사용 하는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-148">It's possible to use a custom service provider instead of the default service provider added by the default template.</span></span> <span data-ttu-id="fb93c-149">사용자 지정 서비스 공급자 표에 나열 된 기본 서비스를 자동으로 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-149">A custom service provider doesn't automatically provide the default services listed in the table.</span></span> <span data-ttu-id="fb93c-150">사용자 지정 서비스 공급자를 사용 하는 표에 표시 된 서비스가 필요 하는 경우 새 서비스 공급자에 필요한 서비스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-150">If you use a custom service provider and require any of the services shown in the table, add the required services to the new service provider.</span></span>

## <a name="request-a-service-in-a-component"></a><span data-ttu-id="fb93c-151">구성 요소에서 서비스 요청</span><span class="sxs-lookup"><span data-stu-id="fb93c-151">Request a service in a component</span></span>

<span data-ttu-id="fb93c-152">서비스 서비스 컬렉션에 추가 된 후 서비스를 사용 하 여 구성 요소 Razor 템플릿에 삽입 합니다 [ @inject ](xref:mvc/views/razor#section-4) Razor 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-152">After services are added to the service collection, inject the services into the components' Razor templates using the [@inject](xref:mvc/views/razor#section-4) Razor directive.</span></span> <span data-ttu-id="fb93c-153">`@inject` 두 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-153">`@inject` has two parameters:</span></span>

* <span data-ttu-id="fb93c-154">유형 이름: 삽입할 서비스의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-154">Type name: The type of the service to inject.</span></span>
* <span data-ttu-id="fb93c-155">속성 이름: 삽입 된 app service를 수신 하는 속성의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-155">Property name: The name of the property receiving the injected app service.</span></span> <span data-ttu-id="fb93c-156">참고 속성 수동으로 만들기를 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-156">Note that the property doesn't require manual creation.</span></span> <span data-ttu-id="fb93c-157">컴파일러는 속성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-157">The compiler creates the property.</span></span>

<span data-ttu-id="fb93c-158">자세한 내용은 <xref:mvc/views/dependency-injection>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fb93c-158">For more information, see <xref:mvc/views/dependency-injection>.</span></span>

<span data-ttu-id="fb93c-159">사용 하 여 `@inject` 문을 서로 다른 서비스를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-159">Use multiple `@inject` statements to inject different services.</span></span>

<span data-ttu-id="fb93c-160">다음 예제에서는 `@inject`을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-160">The following example shows how to use `@inject`.</span></span> <span data-ttu-id="fb93c-161">서비스 구현 `Services.IDataAccess` 구성 요소의 속성에 주입 됩니다 `DataRepository`합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-161">The service implementing `Services.IDataAccess` is injected into the component's property `DataRepository`.</span></span> <span data-ttu-id="fb93c-162">만 코드를 사용 하는 방식을 참고 합니다 `IDataAccess` 추상화 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-162">Note how the code is only using the `IDataAccess` abstraction:</span></span>

[!code-cshtml[](dependency-injection/samples_snapshot/3.x/CustomerList.cshtml?highlight=2-3,23)]

<span data-ttu-id="fb93c-163">내부적으로 생성 된 속성 (`DataRepository`)으로 데코 레이트 된는 `InjectAttribute` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-163">Internally, the generated property (`DataRepository`) is decorated with the `InjectAttribute` attribute.</span></span> <span data-ttu-id="fb93c-164">일반적으로이 특성을 직접 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-164">Typically, this attribute isn't used directly.</span></span> <span data-ttu-id="fb93c-165">기본 클래스는 구성 요소에 필요한 경우 삽입 된 속성은 또한 필수 기본 클래스에 대 한 `InjectAttribute` 수동으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-165">If a base class is required for components and injected properties are also required for the base class, `InjectAttribute` can be manually added:</span></span>

```csharp
public class ComponentBase : IComponent
{
    // Dependency injection works even if using the
    // InjectAttribute in a component's base class.
    [Inject]
    protected IDataAccess DataRepository { get; set; }
    ...
}
```

<span data-ttu-id="fb93c-166">기본 클래스에서 파생 된 구성 요소에는 `@inject` 지시문은 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-166">In components derived from the base class, the `@inject` directive isn't required.</span></span> <span data-ttu-id="fb93c-167">`InjectAttribute` 기본 클래스는 충분 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-167">The `InjectAttribute` of the base class is sufficient:</span></span>

```cshtml
@page "/demo"
@inherits ComponentBase

<h1>Demo Component</h1>
```

## <a name="dependency-injection-in-services"></a><span data-ttu-id="fb93c-168">서비스에서 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="fb93c-168">Dependency injection in services</span></span>

<span data-ttu-id="fb93c-169">복잡 한 서비스에는 추가 서비스 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-169">Complex services might require additional services.</span></span> <span data-ttu-id="fb93c-170">이전 예에서 `DataAccess` 필요할 수 있습니다는 `HttpClient` 기본 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-170">In the prior example, `DataAccess` might require the `HttpClient` default service.</span></span> <span data-ttu-id="fb93c-171">`@inject` (또는 `InjectAttribute`) 서비스에서 사용 하기 위해 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-171">`@inject` (or the `InjectAttribute`) isn't available for use in services.</span></span> <span data-ttu-id="fb93c-172">*생성자 주입* 대신 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-172">*Constructor injection* must be used instead.</span></span> <span data-ttu-id="fb93c-173">필요한 서비스는 서비스의 생성자에 매개 변수를 추가 하 여 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-173">Required services are added by adding parameters to the service's constructor.</span></span> <span data-ttu-id="fb93c-174">종속성 주입 된 서비스를 만들 때이 생성자에 필요 하며, 적절 하 게 제공 서비스 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-174">When dependency injection creates the service, it recognizes the services it requires in the constructor and provides them accordingly.</span></span>

```csharp
public class DataAccess : IDataAccess
{
    // The constructor receives an HttpClient via dependency
    // injection. HttpClient is a default service.
    public DataAccess(HttpClient client)
    {
        ...
    }
}
```

<span data-ttu-id="fb93c-175">생성자 주입을 위한 필수 조건:</span><span class="sxs-lookup"><span data-stu-id="fb93c-175">Prerequisites for constructor injection:</span></span>

* <span data-ttu-id="fb93c-176">인수 모두 수행할 수 있습니다 종속성 주입으로 생성자가 하나 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-176">There must be one constructor whose arguments can all be fulfilled by dependency injection.</span></span> <span data-ttu-id="fb93c-177">DI에서 포함 하지 않는 추가 매개 변수는 기본값을 지정 하는 경우 허용 되는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-177">Note that additional parameters not covered by DI are allowed if they specify default values.</span></span>
* <span data-ttu-id="fb93c-178">해당 생성자 없어야 *공용*합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-178">The applicable constructor must be *public*.</span></span>
* <span data-ttu-id="fb93c-179">해당 생성자가 하나 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-179">There must only be one applicable constructor.</span></span> <span data-ttu-id="fb93c-180">모호성을 발생 시 DI에 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fb93c-180">In case of an ambiguity, DI throws an exception.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fb93c-181">추가 자료</span><span class="sxs-lookup"><span data-stu-id="fb93c-181">Additional resources</span></span>

* <xref:fundamentals/dependency-injection>
* <xref:mvc/views/dependency-injection>
