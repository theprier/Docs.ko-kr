---
title: ClaimsPrincipal.Current에서 마이그레이션
author: mjrousos
description: 현재 인증 된 사용자의 id 및 ASP.NET 코어의 클레임을 검색 하는 ClaimsPrincipal.Current에서 마이그레이션하는 방법에 알아봅니다.
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 05/04/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: migration/claimsprincipal-current
ms.openlocfilehash: ea43d17e76380baf57cd9debbc508e8812cfa4a6
ms.sourcegitcommit: 477d38e33530a305405eaf19faa29c6d805273aa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/08/2018
---
# <a name="migrate-from-claimsprincipalcurrent"></a><span data-ttu-id="7678c-103">ClaimsPrincipal.Current에서 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="7678c-103">Migrate from ClaimsPrincipal.Current</span></span>

<span data-ttu-id="7678c-104">ASP.NET 프로젝트에서 사용 하는 것 [ClaimsPrincipal.Current](/dotnet/api/system.security.claims.claimsprincipal.current) 현재 검색을 사용자의 id 및 클레임 인증입니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-104">In ASP.NET projects, it was common to use [ClaimsPrincipal.Current](/dotnet/api/system.security.claims.claimsprincipal.current) to retrieve the current authenticated user's identity and claims.</span></span> <span data-ttu-id="7678c-105">ASP.NET Core에서 더 이상이 속성이 설정 되어 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-105">In ASP.NET Core, this property is no longer set.</span></span> <span data-ttu-id="7678c-106">큰지에 된 코드를 다른 수단을 통해 현재 인증 된 사용자의 id를 가져오려면 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-106">Code that was depending on it needs to be updated to get the current authenticated user's identity through a different means.</span></span>

## <a name="context-specific-data-instead-of-static-data"></a><span data-ttu-id="7678c-107">정적 데이터 대신 상황에 맞는 데이터</span><span class="sxs-lookup"><span data-stu-id="7678c-107">Context-specific data instead of static data</span></span>

<span data-ttu-id="7678c-108">ASP.NET Core를 둘 다의 값을 사용 하는 경우 `ClaimsPrincipal.Current` 및 `Thread.CurrentPrincipal` 를 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-108">When using ASP.NET Core, the values of both `ClaimsPrincipal.Current` and `Thread.CurrentPrincipal` aren't set.</span></span> <span data-ttu-id="7678c-109">이러한 두 속성에는 ASP.NET Core 일반적으로 하지 않습니다. 정적 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-109">These properties both represent static state, which ASP.NET Core generally avoids.</span></span> <span data-ttu-id="7678c-110">ASP.NET Core 아키텍처 상황에 맞는 서비스 컬렉션에서 종속성 (예: 현재 사용자의 id)를 검색 하는 대신 (사용 하 여 해당 [종속성 주입](xref:fundamentals/dependency-injection) (DI) 모델).</span><span class="sxs-lookup"><span data-stu-id="7678c-110">Instead, ASP.NET Core's architecture is to retrieve dependencies (like the current user's identity) from context-specific service collections (using its [dependency injection](xref:fundamentals/dependency-injection) (DI) model).</span></span> <span data-ttu-id="7678c-111">더 이란 `Thread.CurrentPrincipal` 는 스레드 정적 이므로 비동기 일부 시나리오에서는 변경 내용이 유지 되지 않을 수 있습니다 (및 `ClaimsPrincipal.Current` 호출 `Thread.CurrentPrincipal` 기본적으로).</span><span class="sxs-lookup"><span data-stu-id="7678c-111">What's more, `Thread.CurrentPrincipal` is thread static, so it may not persist changes in some asynchronous scenarios (and `ClaimsPrincipal.Current` just calls `Thread.CurrentPrincipal` by default).</span></span>

<span data-ttu-id="7678c-112">문제 스레드의 종류를 이해 하려면 정적 멤버 비동기 시나리오에서 다음 코드 조각을 참조 하십시오 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-112">To understand the sorts of problems thread static members can lead to in asynchronous scenarios, consider the following code snippet:</span></span>

```csharp
// Create a ClaimsPrincipal and set Thread.CurrentPrincipal
var identity = new ClaimsIdentity();
identity.AddClaim(new Claim(ClaimTypes.Name, "User1"));
Thread.CurrentPrincipal = new ClaimsPrincipal(identity);

// Check the current user
Console.WriteLine($"Current user: {Thread.CurrentPrincipal?.Identity.Name}");

// For the method to complete asynchronously
await Task.Yield();

// Check the current user after
Console.WriteLine($"Current user: {Thread.CurrentPrincipal?.Identity.Name}");
```

<span data-ttu-id="7678c-113">위의 샘플 코드 집합 `Thread.CurrentPrincipal` 비동기 호출을 대기 하기 전후에 해당 값을 확인 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-113">The preceding sample code sets `Thread.CurrentPrincipal` and checks its value before and after awaiting an asynchronous call.</span></span> <span data-ttu-id="7678c-114">`Thread.CurrentPrincipal` 관련는 *스레드* 기반이 설정 하 고 메서드가 await 뒤에 다른 스레드에서 실행을 다시 시작 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-114">`Thread.CurrentPrincipal` is specific to the *thread* on which it's set, and the method is likely to resume execution on a different thread after the await.</span></span> <span data-ttu-id="7678c-115">따라서 `Thread.CurrentPrincipal` 은 present를 먼저 검사 하지만를 호출한 후 null 때 `await Task.Yield()`합니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-115">Consequently, `Thread.CurrentPrincipal` is present when it's first checked but is null after the call to `await Task.Yield()`.</span></span>

<span data-ttu-id="7678c-116">응용 프로그램의 DI 서비스 컬렉션에서 현재 사용자의 id를 가져오는 없으므로 더 테스트 가능한도 테스트 identities 쉽게 삽입 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-116">Getting the current user's identity from the app's DI service collection is more testable, too, since test identities can be easily injected.</span></span>

## <a name="retrieve-the-current-user-in-an-aspnet-core-app"></a><span data-ttu-id="7678c-117">ASP.NET Core 응용 프로그램에서 현재 사용자를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-117">Retrieve the current user in an ASP.NET Core app</span></span>

<span data-ttu-id="7678c-118">현재 인증 된 사용자를 검색 하기 위한 여러 가지 `ClaimsPrincipal` 대신 ASP.NET Core에서 `ClaimsPrincipal.Current`:</span><span class="sxs-lookup"><span data-stu-id="7678c-118">There are several options for retrieving the current authenticated user's `ClaimsPrincipal` in ASP.NET Core in place of `ClaimsPrincipal.Current`:</span></span>

* <span data-ttu-id="7678c-119">**ControllerBase.User**합니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-119">**ControllerBase.User**.</span></span> <span data-ttu-id="7678c-120">MVC 컨트롤러와 현재 인증 된 사용자에 액세스할 수 있는 해당 [사용자](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.user) 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-120">MVC controllers can access the current authenticated user with their [User](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.user) property.</span></span>
* <span data-ttu-id="7678c-121">**HttpContext.User**합니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-121">**HttpContext.User**.</span></span> <span data-ttu-id="7678c-122">현재에 액세스할 수 있는 구성 요소 `HttpContext` (예: 미들웨어) 현재 사용자를 가져올 수 `ClaimsPrincipal` 에서 [HttpContext.User](/dotnet/api/microsoft.aspnetcore.http.httpcontext.user)합니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-122">Components with access to the current `HttpContext` (middleware, for example) can get the current user's `ClaimsPrincipal` from [HttpContext.User](/dotnet/api/microsoft.aspnetcore.http.httpcontext.user).</span></span>
* <span data-ttu-id="7678c-123">**호출자에서 전달 된**합니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-123">**Passed in from caller**.</span></span> <span data-ttu-id="7678c-124">현재에 액세스 하지 않고 라이브러리 `HttpContext` 컨트롤러 또는 미들웨어 구성 요소에서 통칭 되 고 인수로 전달 하는 현재 사용자의 id를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-124">Libraries without access to the current `HttpContext` are often called from controllers or middleware components and can have the current user's identity passed as an argument.</span></span>
* <span data-ttu-id="7678c-125">**IHttpContextAccessor**합니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-125">**IHttpContextAccessor**.</span></span> <span data-ttu-id="7678c-126">ASP.NET Core로 마이그레이션되는 ASP.NET 프로젝트는 필요한 모든 위치에 현재 사용자의 id를 쉽게 전달할 수 없을 정도로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-126">The ASP.NET project being migrated to ASP.NET Core may be too large to easily pass the current user's identity to all necessary locations.</span></span> <span data-ttu-id="7678c-127">이러한 경우 [IHttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextaccessor) 해결 방법으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-127">In such cases, [IHttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextaccessor) can be used as a workaround.</span></span> <span data-ttu-id="7678c-128">`IHttpContextAccessor` 현재 액세스할 수 `HttpContext` (있는 경우).</span><span class="sxs-lookup"><span data-stu-id="7678c-128">`IHttpContextAccessor` is able to access the current `HttpContext` (if one exists).</span></span> <span data-ttu-id="7678c-129">ASP.NET Core DI 기반 아키텍처와 함께 작동 하도록 아직 업데이트 되지 않은 코드에서 현재 사용자의 id를 가져오는 단계는 임시 솔루션이 합니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-129">A short-term solution to getting the current user's identity in code that hasn't yet been updated to work with ASP.NET Core's DI-driven architecture would be:</span></span>

  * <span data-ttu-id="7678c-130">확인 `IHttpContextAccessor` 호출 하 여 DI 컨테이너에서 사용할 수 있는 [AddHttpContextAccessor](https://github.com/aspnet/Hosting/issues/793) 에서 `Startup.ConfigureServices`합니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-130">Make `IHttpContextAccessor` available in the DI container by calling [AddHttpContextAccessor](https://github.com/aspnet/Hosting/issues/793) in `Startup.ConfigureServices`.</span></span>
  * <span data-ttu-id="7678c-131">인스턴스를 가져올 `IHttpContextAccessor` 시작 하는 동안를 정적 변수에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-131">Get an instance of `IHttpContextAccessor` during startup and store it in a static variable.</span></span> <span data-ttu-id="7678c-132">인스턴스를 이전에 정적 속성에서 현재 사용자를 검색 하는 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-132">The instance is made available to code that was previously retrieving the current user from a static property.</span></span>
  * <span data-ttu-id="7678c-133">현재 사용자의 검색 `ClaimsPrincipal` 를 사용 하 여 `HttpContextAccessor.HttpContext?.User`합니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-133">Retrieve the current user's `ClaimsPrincipal` using `HttpContextAccessor.HttpContext?.User`.</span></span> <span data-ttu-id="7678c-134">이 코드는 HTTP 요청의 컨텍스트 외부에서 사용 되는 경우는 `HttpContext` null입니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-134">If this code is used outside of the context of an HTTP request, the `HttpContext` is null.</span></span>

<span data-ttu-id="7678c-135">최종 옵션을 사용 하 여 `IHttpContextAccessor`, ASP.NET Core 원칙 (정적 종속성에 삽입 된 종속성을 선호)에 위배 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-135">The final option, using `IHttpContextAccessor`, is contrary to ASP.NET Core principles (preferring injected dependencies to static dependencies).</span></span> <span data-ttu-id="7678c-136">정적에 대 한 종속성을 제거할 계획 `IHttpContextAccessor` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-136">Plan to eventually remove the dependency on the static `IHttpContextAccessor` helper.</span></span> <span data-ttu-id="7678c-137">것이 유용한 브리지 하지만 이전에 사용 하는 큰 기존 ASP.NET 응용 프로그램을 마이그레이션할 때 `ClaimsPrincipal.Current`합니다.</span><span class="sxs-lookup"><span data-stu-id="7678c-137">It can be a useful bridge, though, when migrating large existing ASP.NET apps that were previously using `ClaimsPrincipal.Current`.</span></span>
