---
title: ASP.NET Core에서 HttpContext에 액세스
author: coderandhiker
description: ASP.NET Core에서 HttpContext에 액세스하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 07/20/2018
uid: fundamentals/httpcontext
ms.openlocfilehash: b1ff80943db1788b465accd51c70a3c3a3462d5c
ms.sourcegitcommit: a3675f9704e4e73ecc7cbbbf016a13d2a5c4d725
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2018
ms.locfileid: "39202713"
---
# <a name="access-httpcontext-in-aspnet-core"></a><span data-ttu-id="1ed9b-103">ASP.NET Core에서 HttpContext에 액세스</span><span class="sxs-lookup"><span data-stu-id="1ed9b-103">Access HttpContext in ASP.NET Core</span></span>

<span data-ttu-id="1ed9b-104">ASP.NET Core 앱은 [IHttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextaccessor) 인터페이스 및 기본 구현 [HttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.httpcontextaccessor)를 통해 `HttpContext`에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9b-104">ASP.NET Core apps access the `HttpContext` through the [IHttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextaccessor) interface and its default implementation [HttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.httpcontextaccessor).</span></span>

::: moniker range=">= aspnetcore-2.0"

## <a name="use-httpcontext-from-razor-pages"></a><span data-ttu-id="1ed9b-105">Razor Pages에서 HttpContext 사용</span><span class="sxs-lookup"><span data-stu-id="1ed9b-105">Use HttpContext from Razor Pages</span></span>

<span data-ttu-id="1ed9b-106">Razor Pages [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel)은 다음과 같이 [HttpContext](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel.httpcontext) 속성을 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9b-106">The Razor Pages [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel) exposes the [HttpContext](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel.httpcontext) property:</span></span>

```csharp
public class AboutModel : PageModel
{
    public string Message { get; set; }

    public void OnGet()
    {
        Message = HttpContext.Request.PathBase;
    }
}
```

::: moniker-end

## <a name="use-httpcontext-from-a-controller"></a><span data-ttu-id="1ed9b-107">컨트롤러에서 HttpContext 사용</span><span class="sxs-lookup"><span data-stu-id="1ed9b-107">Use HttpContext from a controller</span></span>

<span data-ttu-id="1ed9b-108">컨트롤러는 다음과 같이 [ControllerBase.HttpContext](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.httpcontext) 속성을 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9b-108">Controllers expose the [ControllerBase.HttpContext](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.httpcontext) property:</span></span>

```csharp
public class HomeController : Controller
{
    public IActionResult About()
    {
        var pathBase = HttpContext.Request.PathBase;
        // Do something with the PathBase.

        return View();
    }
}
```

## <a name="use-httpcontext-from-middleware"></a><span data-ttu-id="1ed9b-109">미들웨어에서 HttpContext 사용</span><span class="sxs-lookup"><span data-stu-id="1ed9b-109">Use HttpContext from middleware</span></span>

<span data-ttu-id="1ed9b-110">사용자 지정 미들웨어 구성 요소를 사용할 경우 `HttpContext`는 `Invoke` 또는 `InvokeAsync` 메서드로 전달되며 미들웨어가 구성될 때 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9b-110">When working with custom middleware components, `HttpContext` is passed into the `Invoke` or `InvokeAsync` method and can be accessed when the middleware is configured:</span></span>

```csharp
public class MyCustomMiddleware
{
    public Task InvokeAsync(HttpContext context)
    {
        // Middleware initialization optionally using HttpContext
    }
}
```

## <a name="use-httpcontext-from-custom-components"></a><span data-ttu-id="1ed9b-111">사용자 지정 구성 요소에서 HttpContext 사용</span><span class="sxs-lookup"><span data-stu-id="1ed9b-111">Use HttpContext from custom components</span></span>

<span data-ttu-id="1ed9b-112">`HttpContext`에 액세스해야 하는 기타 프레임워크 및 사용자 지정 구성 요소의 경우 기본 제공 [종속성 주입](xref:fundamentals/dependency-injection) 컨테이너를 사용하여 종속성을 등록하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9b-112">For other framework and custom components that require access to `HttpContext`, the recommended approach is to register a dependency using the built-in [dependency injection](xref:fundamentals/dependency-injection) container.</span></span> <span data-ttu-id="1ed9b-113">종속성 주입 컨테이너는 `IHttpContextAccessor`를 해당 생성자에서 종속성으로 선언하는 모든 클래스에 이를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9b-113">The dependency injection container supplies the `IHttpContextAccessor` to any classes that declare it as a dependency in their constructors.</span></span>

::: moniker range=">= aspnetcore-2.1"

```csharp
public void ConfigureServices(IServiceCollection services)
{
     services.AddMvc()
         .SetCompatibilityVersion(CompatibilityVersion.Version_2_1);
     services.AddHttpContextAccessor();
     services.AddTransient<IUserRepository, UserRepository>();
}
```

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

```csharp
public void ConfigureServices(IServiceCollection services)
{
     services.AddMvc();
     services.AddSingleton<IHttpContextAccessor, HttpContextAccessor>();
     services.AddTransient<IUserRepository, UserRepository>();
}
```

::: moniker-end

<span data-ttu-id="1ed9b-114">앞의 예제에서:</span><span class="sxs-lookup"><span data-stu-id="1ed9b-114">In the preceding example:</span></span>

* <span data-ttu-id="1ed9b-115">`UserRepository`는 `IHttpContextAccessor`에 대한 종속성을 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9b-115">`UserRepository` declares its dependency on `IHttpContextAccessor`.</span></span>
* <span data-ttu-id="1ed9b-116">종속성 주입이 종속성 체인을 확인하고 `UserRepository` 인스턴스를 만들 경우 종속성이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ed9b-116">The dependency is supplied when dependency injection resolves the dependency chain and creates an instance of `UserRepository`.</span></span>

```csharp
public class UserRepository : IUserRepository
{
    private readonly IHttpContextAccessor _httpContextAccessor;

    public UserRepository(IHttpContextAccessor httpContextAccessor)
    {
        _httpContextAccessor = httpContextAccessor;
    }

    public void LogCurrentUser()
    {
        var username = _httpContextAccessor.HttpContext.User.Identity.Name;
        service.LogAccessRequest(username);
    }
}
```
