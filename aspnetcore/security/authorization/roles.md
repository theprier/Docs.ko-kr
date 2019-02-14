---
title: ASP.NET Core의 역할 기반 권한 부여
author: rick-anderson
description: Authorize 특성에 역할을 전달하여 ASP.NET Core의 컨트롤러 및 액션에 대한 접근을 제한하는 방법을 알아봅니다.
ms.author: riande
ms.date: 10/14/2016
uid: security/authorization/roles
ms.openlocfilehash: 0467ea82831bffe6882e584930c2fa1212a244c7
ms.sourcegitcommit: 6ba5fb1fd0b7f9a6a79085b0ef56206e462094b7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56248097"
---
# <a name="role-based-authorization-in-aspnet-core"></a><span data-ttu-id="202e8-103">ASP.NET Core의 역할 기반 권한 부여</span><span class="sxs-lookup"><span data-stu-id="202e8-103">Role-based authorization in ASP.NET Core</span></span>

<a name="security-authorization-role-based"></a>

<span data-ttu-id="202e8-104">신원(Identity)이 생성될 때 해당 신원은 하나 이상의 역할에 속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="202e8-104">When an identity is created it may belong to one or more roles.</span></span> <span data-ttu-id="202e8-105">예를 들어 Tracy는 Administrator 및 User 역할에 모두 속하지만 Scott은 User 역할에만 속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="202e8-105">For example, Tracy may belong to the Administrator and User roles whilst Scott may only belong to the User role.</span></span> <span data-ttu-id="202e8-106">이런 역할이 생성되고 관리되는 방식은 권한 부여 프로세스에 사용되는 백업 저장소에 따라서 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="202e8-106">How these roles are created and managed depends on the backing store of the authorization process.</span></span> <span data-ttu-id="202e8-107">개발자는 [ClaimsPrincipal](/dotnet/api/system.security.principal.genericprincipal.isinrole) 클래스의 [IsInRole](/dotnet/api/system.security.claims.claimsprincipal) 메서드를 이용하여 역할에 접근할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="202e8-107">Roles are exposed to the developer through the [IsInRole](/dotnet/api/system.security.principal.genericprincipal.isinrole) method on the [ClaimsPrincipal](/dotnet/api/system.security.claims.claimsprincipal) class.</span></span>

::: moniker range=">= aspnetcore-2.0"

> [!IMPORTANT]
> <span data-ttu-id="202e8-108">이 항목은 Razor 페이지에는 적용되지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="202e8-108">This topic does **not** apply to Razor Pages.</span></span> <span data-ttu-id="202e8-109">Razor 페이지는 [IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter) 및 [IAsyncPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.iasyncpagefilter)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="202e8-109">Razor Pages supports [IPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.ipagefilter) and [IAsyncPageFilter](/dotnet/api/microsoft.aspnetcore.mvc.filters.iasyncpagefilter).</span></span> <span data-ttu-id="202e8-110">자세한 내용은 [Razor 페이지 필터의 메서드](xref:razor-pages/filter)를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="202e8-110">For more information, see [Filter methods for Razor Pages](xref:razor-pages/filter).</span></span>

::: moniker-end

## <a name="adding-role-checks"></a><span data-ttu-id="202e8-111">역할 검사 추가하기</span><span class="sxs-lookup"><span data-stu-id="202e8-111">Adding role checks</span></span>

<span data-ttu-id="202e8-112">역할 기반 권한 부여의 검사는 선언적으로 구성됩니다 &mdash;. 개발자는 컨트롤러나 컨트롤러 내의 개별 액션에 대해 현재 사용자가 요청한 리소스에 접근하기 위해 반드시 속해 있어야만 하는 역할을 지정해서 이를 코드 내부에 포함시킵니다.</span><span class="sxs-lookup"><span data-stu-id="202e8-112">Role-based authorization checks are declarative&mdash;the developer embeds them within their code, against a controller or an action within a controller, specifying roles which the current user must be a member of to access the requested resource.</span></span>

<span data-ttu-id="202e8-113">예를 들어 다음 코드는 `Administrator` 역할에 속한 사용자만 `AdministrationController` 의 모든 액션에 접근할 수 있도록 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="202e8-113">For example, the following code limits access to any actions on the `AdministrationController` to users who are a member of the `Administrator` role:</span></span>

```csharp
[Authorize(Roles = "Administrator")]
public class AdministrationController : Controller
{
}
```

<span data-ttu-id="202e8-114">쉼표로 구분된 목록을 지정해서 여러 역할을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="202e8-114">You can specify multiple roles as a comma separated list:</span></span>

```csharp
[Authorize(Roles = "HRManager,Finance")]
public class SalaryController : Controller
{
}
```

<span data-ttu-id="202e8-115">이 컨트롤러는 `HRManager` 역할이나 `Finance` 역할에 속한 사용자만 접근할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="202e8-115">This controller would be only accessible by users who are members of the `HRManager` role or the `Finance` role.</span></span>

<span data-ttu-id="202e8-116">여러 특성을 지정한 경우 접근하는 사용자는 지정된 모든 역할에 속해 있어야 하는데, 다음 예제에서 사용자는 `PowerUser` 및 `ControlPanelUser` 역할 모두에 속해 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="202e8-116">If you apply multiple attributes then an accessing user must be a member of all the roles specified; the following sample requires that a user must be a member of both the `PowerUser` and `ControlPanelUser` role.</span></span>

```csharp
[Authorize(Roles = "PowerUser")]
[Authorize(Roles = "ControlPanelUser")]
public class ControlPanelController : Controller
{
}
```

<span data-ttu-id="202e8-117">액션 수준에 역할 권한 부여 특성을 추가로 적용해서 접근을 더욱 제한할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="202e8-117">You can further limit access by applying additional role authorization attributes at the action level:</span></span>

```csharp
[Authorize(Roles = "Administrator, PowerUser")]
public class ControlPanelController : Controller
{
    public ActionResult SetTime()
    {
    }

    [Authorize(Roles = "Administrator")]
    public ActionResult ShutDown()
    {
    }
}
```

<span data-ttu-id="202e8-118">위의 코드 조각의 경우, `Administrator` 역할이나 `PowerUser` 역할에 속한 사용자는 컨트롤러와 `SetTime` 액션에 접근할 수 있지만, `ShutDown` 액션은 `Administrator` 역할에 속한 사용자만 접근이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="202e8-118">In the previous code snippet members of the `Administrator` role or the `PowerUser` role can access the controller and the `SetTime` action, but only members of the `Administrator` role can access the `ShutDown` action.</span></span>

<span data-ttu-id="202e8-119">또한, 컨트롤러를 잠글 수도 있고 개별 작업에 대한 익명의 인증되지 않은 액세스를 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="202e8-119">You can also lock down a controller but allow anonymous, unauthenticated access to individual actions.</span></span>

```csharp
[Authorize]
public class ControlPanelController : Controller
{
    public ActionResult SetTime()
    {
    }

    [AllowAnonymous]
    public ActionResult Login()
    {
    }
}
```

<a name="security-authorization-role-policy"></a>

## <a name="policy-based-role-checks"></a><span data-ttu-id="202e8-120">정책 기반 역할 검사</span><span class="sxs-lookup"><span data-stu-id="202e8-120">Policy based role checks</span></span>

<span data-ttu-id="202e8-121">역할 요구 사항은 개발자가 응용 프로그램 시작 시 Authorization 서비스 구성의 일부로 정책을 등록하는 새로운 Policy 구문을 사용해서 표현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="202e8-121">Role requirements can also be expressed using the new Policy syntax, where a developer registers a policy at startup as part of the Authorization service configuration.</span></span> <span data-ttu-id="202e8-122">일반적으로 이 작업은 *Startup.cs* 파일의 `ConfigureServices()`에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="202e8-122">This normally occurs in `ConfigureServices()` in your *Startup.cs* file.</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();

    services.AddAuthorization(options =>
    {
        options.AddPolicy("RequireAdministratorRole",
             policy => policy.RequireRole("Administrator"));
    });
}
```

<span data-ttu-id="202e8-123">정책은 `AuthorizeAttribute` 특성의 `Policy` 속성을 통해서 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="202e8-123">Policies are applied using the `Policy` property on the `AuthorizeAttribute` attribute:</span></span>

```csharp
[Authorize(Policy = "RequireAdministratorRole")]
public IActionResult Shutdown()
{
    return View();
}
```

<span data-ttu-id="202e8-124">하나의 요구 사항에 허용되는 여러 역할을 지정하고 싶다면 해당 역할들을 `RequireRole` 메서드에 매개 변수로 전달하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="202e8-124">If you want to specify multiple allowed roles in a requirement then you can specify them as parameters to the `RequireRole` method:</span></span>

```csharp
options.AddPolicy("ElevatedRights", policy =>
                  policy.RequireRole("Administrator", "PowerUser", "BackupAdministrator"));
```

<span data-ttu-id="202e8-125">이 예제는 `Administrator`, `PowerUser` 또는 `BackupAdministrator` 역할에 속한 사용자에게 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="202e8-125">This example authorizes users who belong to the `Administrator`, `PowerUser` or `BackupAdministrator` roles.</span></span>

### <a name="add-role-services-to-identity"></a><span data-ttu-id="202e8-126">Id에 역할 서비스 추가</span><span class="sxs-lookup"><span data-stu-id="202e8-126">Add Role services to Identity</span></span>

<span data-ttu-id="202e8-127">추가 [역할](/dotnet/api/microsoft.aspnetcore.identity.identitybuilder.addroles#Microsoft_AspNetCore_Identity_IdentityBuilder_AddRoles__1) 역할 서비스를 추가 하려면:</span><span class="sxs-lookup"><span data-stu-id="202e8-127">Append [AddRoles](/dotnet/api/microsoft.aspnetcore.identity.identitybuilder.addroles#Microsoft_AspNetCore_Identity_IdentityBuilder_AddRoles__1) to add Role services:</span></span>

[!code-csharp[](roles/samples/Startup.cs?name=snippet&highlight=7)]