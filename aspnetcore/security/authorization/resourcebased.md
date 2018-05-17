---
title: ASP.NET Core에서 리소스 기반의 권한 부여
author: scottaddie
description: 권한 부여 속성 않습니다 요구 사항을 충족 하는 경우 ASP.NET Core 응용 프로그램의 리소스 기반 권한 부여를 구현 하는 방법을 알아봅니다.
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 11/07/2017
ms.devlang: csharp
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/resourcebased
ms.openlocfilehash: 3be2d9b9aef18763fbdba78e044dd6b68ddcef0c
ms.sourcegitcommit: 9bc34b8269d2a150b844c3b8646dcb30278a95ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/12/2018
---
# <a name="resource-based-authorization-in-aspnet-core"></a><span data-ttu-id="fe308-103">ASP.NET Core에서 리소스 기반의 권한 부여</span><span class="sxs-lookup"><span data-stu-id="fe308-103">Resource-based authorization in ASP.NET Core</span></span>

<span data-ttu-id="fe308-104">권한 부여 전략 액세스 되는 리소스에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-104">Authorization strategy depends upon the resource being accessed.</span></span> <span data-ttu-id="fe308-105">Author 속성에 문서를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-105">Consider a document which has an author property.</span></span> <span data-ttu-id="fe308-106">작성자만 문서를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-106">Only the author is allowed to update the document.</span></span> <span data-ttu-id="fe308-107">따라서 문서 권한 부여 평가 하기 전에 데이터 저장소에서 검색 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-107">Consequently, the document must be retrieved from the data store before authorization evaluation can occur.</span></span>

<span data-ttu-id="fe308-108">특성 평가 데이터 바인딩 전에 페이지 처리기 또는 문서를 로드 하는 작업의 실행 하기 전에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-108">Attribute evaluation occurs before data binding and before execution of the page handler or action which loads the document.</span></span> <span data-ttu-id="fe308-109">이러한 이유로, 사용한 선언적 권한 부여는 `[Authorize]` 특성으로 충분 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-109">For these reasons, declarative authorization with an `[Authorize]` attribute won't suffice.</span></span> <span data-ttu-id="fe308-110">대신, 사용자 지정 권한 부여 메서드를 호출할 수 있습니다&mdash;스타일 명령적 권한 부여 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-110">Instead, you can invoke a custom authorization method&mdash;a style known as imperative authorization.</span></span>

<span data-ttu-id="fe308-111">사용 하 여는 [앱 샘플](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/resourcebased/samples) ([다운로드 하는 방법](xref:tutorials/index#how-to-download-a-sample))이이 항목에서 설명 하는 기능을 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-111">Use the [sample apps](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/resourcebased/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample)) to explore the features described in this topic.</span></span>

<span data-ttu-id="fe308-112">[권한 부여에 의해 보호 되는 사용자 데이터와 ASP.NET Core 응용 프로그램 만들기](xref:security/authorization/secure-data) 리소스 기반 권한 부여를 사용 하는 샘플 앱을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-112">[Create an ASP.NET Core app with user data protected by authorization](xref:security/authorization/secure-data) contains a sample app that uses resource-based authorization.</span></span>

## <a name="use-imperative-authorization"></a><span data-ttu-id="fe308-113">필수 권한 부여를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="fe308-113">Use imperative authorization</span></span>

<span data-ttu-id="fe308-114">권한 부여로 구현 됩니다는 [IAuthorizationService](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationservice) 내에서 서비스 컬렉션에 등록 하 고 서비스는 `Startup` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-114">Authorization is implemented as an [IAuthorizationService](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationservice) service and is registered in the service collection within the `Startup` class.</span></span> <span data-ttu-id="fe308-115">서비스를 통해 제공할 [종속성 주입](xref:fundamentals/dependency-injection#fundamentals-dependency-injection) 페이지 처리기 또는 작업에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-115">The service is made available via [dependency injection](xref:fundamentals/dependency-injection#fundamentals-dependency-injection) to page handlers or actions.</span></span>

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Controllers/DocumentController.cs?name=snippet_IAuthServiceDI&highlight=6)]

<span data-ttu-id="fe308-116">`IAuthorizationService` 에 두 개의 `AuthorizeAsync` 메서드 오버 로드: 리소스와 정책 이름 및 다른 리소스와 평가 하기 위한 요구 사항 목록이 수락 하나 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-116">`IAuthorizationService` has two `AuthorizeAsync` method overloads: one accepting the resource and the policy name and the other accepting the resource and a list of requirements to evaluate.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="fe308-117">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="fe308-117">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
Task<AuthorizationResult> AuthorizeAsync(ClaimsPrincipal user,
                          object resource,
                          IEnumerable<IAuthorizationRequirement> requirements);
Task<AuthorizationResult> AuthorizeAsync(ClaimsPrincipal user,
                          object resource,
                          string policyName);
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="fe308-118">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="fe308-118">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
Task<bool> AuthorizeAsync(ClaimsPrincipal user,
                          object resource,
                          IEnumerable<IAuthorizationRequirement> requirements);
Task<bool> AuthorizeAsync(ClaimsPrincipal user,
                          object resource,
                          string policyName);
```

---

<a name="security-authorization-resource-based-imperative"></a>

<span data-ttu-id="fe308-119">다음 예제에서는 보안을 유지 하도록 리소스는 사용자 지정에 로드 됩니다 `Document` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-119">In the following example, the resource to be secured is loaded into a custom `Document` object.</span></span> <span data-ttu-id="fe308-120">`AuthorizeAsync` 오버 로드는 현재 사용자가 제공 된 문서를 편집할 수 있는지 여부를 확인 하기 위해 호출 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-120">An `AuthorizeAsync` overload is invoked to determine whether the current user is allowed to edit the provided document.</span></span> <span data-ttu-id="fe308-121">사용자 지정 "EditPolicy" 권한 부여 정책에 대 한 결정으로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-121">A custom "EditPolicy" authorization policy is factored into the decision.</span></span> <span data-ttu-id="fe308-122">참조 [사용자 지정 정책 기반 권한 부여](xref:security/authorization/policies) 권한 부여 정책 만들기에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-122">See [Custom policy-based authorization](xref:security/authorization/policies) for more on creating authorization policies.</span></span>

> [!NOTE]
> <span data-ttu-id="fe308-123">다음 코드 샘플 인증을 실행 하는 것으로 가정 하 고 집합의 `User` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-123">The following code samples assume authentication has run and set the `User` property.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="fe308-124">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="fe308-124">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Pages/Document/Edit.cshtml.cs?name=snippet_DocumentEditHandler)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="fe308-125">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="fe308-125">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Controllers/DocumentController.cs?name=snippet_DocumentEditAction)]

---

## <a name="write-a-resource-based-handler"></a><span data-ttu-id="fe308-126">리소스 기반 처리기 작성</span><span class="sxs-lookup"><span data-stu-id="fe308-126">Write a resource-based handler</span></span>

<span data-ttu-id="fe308-127">리소스 기반 권한 부여 보다 큰 차이가 없습니다.에 대 한 처리기를 작성 [일반 요구 사항 처리기 작성](xref:security/authorization/policies#security-authorization-policies-based-authorization-handler)합니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-127">Writing a handler for resource-based authorization isn't much different than [writing a plain requirements handler](xref:security/authorization/policies#security-authorization-policies-based-authorization-handler).</span></span> <span data-ttu-id="fe308-128">사용자 지정 요구 사항 클래스를 만들고 요구 사항 처리기 클래스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-128">Create a custom requirement class, and implement a requirement handler class.</span></span> <span data-ttu-id="fe308-129">처리기 클래스 요구 사항 및 리소스 종류를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-129">The handler class specifies both the requirement and resource type.</span></span> <span data-ttu-id="fe308-130">예를 들어 한 처리기를 활용 하는 `SameAuthorRequirement` 요구 사항 및 `Document` 리소스 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-130">For example, a handler utilizing a `SameAuthorRequirement` requirement and a `Document` resource looks as follows:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="fe308-131">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="fe308-131">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Services/DocumentAuthorizationHandler.cs?name=snippet_HandlerAndRequirement)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="fe308-132">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="fe308-132">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Services/DocumentAuthorizationHandler.cs?name=snippet_HandlerAndRequirement)]

---

<span data-ttu-id="fe308-133">요구 사항 및 처리기에 등록 된 `Startup.ConfigureServices` 메서드:</span><span class="sxs-lookup"><span data-stu-id="fe308-133">Register the requirement and handler in the `Startup.ConfigureServices` method:</span></span>

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Startup.cs?name=snippet_ConfigureServicesSample&highlight=3-7,9)]

### <a name="operational-requirements"></a><span data-ttu-id="fe308-134">운영 요구 사항</span><span class="sxs-lookup"><span data-stu-id="fe308-134">Operational requirements</span></span>

<span data-ttu-id="fe308-135">CRUD (만들기, 읽기, 업데이트, 삭제) 작업의 결과에 따라 결정을 수행 하면 사용 하 여는 [OperationAuthorizationRequirement](/dotnet/api/microsoft.aspnetcore.authorization.infrastructure.operationauthorizationrequirement) 도우미 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-135">If you're making decisions based on the outcomes of CRUD (Create, Read, Update, Delete) operations, use the [OperationAuthorizationRequirement](/dotnet/api/microsoft.aspnetcore.authorization.infrastructure.operationauthorizationrequirement) helper class.</span></span> <span data-ttu-id="fe308-136">이 클래스를 사용 하면 각 작업 유형에 대해 개별 클래스 대신 단일 처리기를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-136">This class enables you to write a single handler instead of an individual class for each operation type.</span></span> <span data-ttu-id="fe308-137">이 기능을 사용 하려면 일부 작업 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-137">To use it, provide some operation names:</span></span>

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Services/DocumentAuthorizationCrudHandler.cs?name=snippet_OperationsClass)]

<span data-ttu-id="fe308-138">처리기는 다음과 같이 사용 하 여 구현 된 `OperationAuthorizationRequirement` 요구 사항 및 `Document` 리소스:</span><span class="sxs-lookup"><span data-stu-id="fe308-138">The handler is implemented as follows, using an `OperationAuthorizationRequirement` requirement and a `Document` resource:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="fe308-139">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="fe308-139">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Services/DocumentAuthorizationCrudHandler.cs?name=snippet_Handler)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="fe308-140">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="fe308-140">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Services/DocumentAuthorizationCrudHandler.cs?name=snippet_Handler)]

---

<span data-ttu-id="fe308-141">이전 처리기 리소스, 사용자의 id 및 요구 사항의를 사용 하 여 작업의 유효성을 검사 `Name` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-141">The preceding handler validates the operation using the resource, the user's identity, and the requirement's `Name` property.</span></span>

<span data-ttu-id="fe308-142">작업 리소스 처리기를 호출 하려면 작업을 호출할 때 지정 `AuthorizeAsync` 페이지 처리기의 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-142">To call an operational resource handler, specify the operation when invoking `AuthorizeAsync` in your page handler or action.</span></span> <span data-ttu-id="fe308-143">다음 예제에서는 인증 된 사용자가 제공 된 문서를 볼 수 있는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-143">The following example determines whether the authenticated user is permitted to view the provided document.</span></span>

> [!NOTE]
> <span data-ttu-id="fe308-144">다음 코드 샘플 인증을 실행 하는 것으로 가정 하 고 집합의 `User` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-144">The following code samples assume authentication has run and set the `User` property.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="fe308-145">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="fe308-145">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp2/Pages/Document/View.cshtml.cs?name=snippet_DocumentViewHandler&highlight=10-11)]

<span data-ttu-id="fe308-146">권한 부여에 성공 하면 문서를 보기 위한 페이지가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-146">If authorization succeeds, the page for viewing the document is returned.</span></span> <span data-ttu-id="fe308-147">경우 권한 부여 실패 하지만 사용자가 인증 되 면 반환 `ForbidResult` 권한 부여에 실패 한 모든 인증 미들웨어에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-147">If authorization fails but the user is authenticated, returning `ForbidResult` informs any authentication middleware that authorization failed.</span></span> <span data-ttu-id="fe308-148">A `ChallengeResult` 인증을 수행 해야 하는 경우 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-148">A `ChallengeResult` is returned when authentication must be performed.</span></span> <span data-ttu-id="fe308-149">대화형 브라우저 클라이언트에는 사용자를 로그인 페이지로 리디렉션합니다 적절 한 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-149">For interactive browser clients, it may be appropriate to redirect the user to a login page.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="fe308-150">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="fe308-150">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

[!code-csharp[](resourcebased/samples/ResourceBasedAuthApp1/Controllers/DocumentController.cs?name=snippet_DocumentViewAction&highlight=11-12)]

<span data-ttu-id="fe308-151">권한 부여에 성공 하면 문서에 대 한 보기 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-151">If authorization succeeds, the view for the document is returned.</span></span> <span data-ttu-id="fe308-152">권한 부여에 실패 하면 반환 `ChallengeResult` 모든 인증 미들웨어에 알리고 권한 부여 실패, 미들웨어 적절 한 응답을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-152">If authorization fails, returning `ChallengeResult` informs any authentication middleware that authorization failed, and the middleware can take the appropriate response.</span></span> <span data-ttu-id="fe308-153">적절 한 응답 401 또는 403 상태 코드를 반환 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-153">An appropriate response could be returning a 401 or 403 status code.</span></span> <span data-ttu-id="fe308-154">대화형 브라우저 클라이언트에 대 한 사용자를 로그인 페이지로 리디렉션하여 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe308-154">For interactive browser clients, it could mean redirecting the user to a login page.</span></span>

---
