---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: 인증 및 ASP.NET Web API에서에서 권한 부여 | Microsoft Docs
author: MikeWasson
description: ASP.NET Web API에 인증 및 권한 부여의 일반적인 개요를 제공합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/27/2012
ms.topic: article
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 981eebeaa1daaf85cb90a52f073c88cb71099edb
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37365622"
---
<a name="authentication-and-authorization-in-aspnet-web-api"></a><span data-ttu-id="c8416-103">인증 및 ASP.NET Web API에서에서 권한 부여</span><span class="sxs-lookup"><span data-stu-id="c8416-103">Authentication and Authorization in ASP.NET Web API</span></span>
====================
<span data-ttu-id="c8416-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c8416-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="c8416-105">웹 API를 만들었지만 이제에 대 한 액세스를 제어 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-105">You've created a web API, but now you want to control access to it.</span></span> <span data-ttu-id="c8416-106">이 연재 기사의 권한 없는 사용자 로부터 웹 API를 보호 하기 위한 몇 가지 옵션에 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-106">In this series of articles, we'll look at some options for securing a web API from unauthorized users.</span></span> <span data-ttu-id="c8416-107">이 시리즈에서는 인증 및 권한 부여를 모두 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-107">This series will cover both authentication and authorization.</span></span>

- <span data-ttu-id="c8416-108">*인증* 사용자의 id를 아는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-108">*Authentication* is knowing the identity of the user.</span></span> <span data-ttu-id="c8416-109">예를 들어 alice가 자신의 사용자 이름과 암호를 로그인 및 서버 암호를 사용 하 여 Alice를 인증 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-109">For example, Alice logs in with her username and password, and the server uses the password to authenticate Alice.</span></span>
- <span data-ttu-id="c8416-110">*권한 부여* 사용자 작업을 수행할 수 있는지 여부를 결정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-110">*Authorization* is deciding whether a user is allowed to perform an action.</span></span> <span data-ttu-id="c8416-111">예를 들어 Alice는 리소스를 가져오지만 리소스를 만들 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-111">For example, Alice has permission to get a resource but not create a resource.</span></span>

<span data-ttu-id="c8416-112">시리즈의 첫 번째 기사는 ASP.NET Web API에서 인증 및 권한 부여의 일반적인 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-112">The first article in the series gives a general overview of authentication and authorization in ASP.NET Web API.</span></span> <span data-ttu-id="c8416-113">다른 항목 웹 API에 대 한 일반적인 인증 시나리오를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-113">Other topics describe common authentication scenarios for Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="c8416-114">이 시리즈를 검토 하 고 소중한 피드백을 제공 하는 사람들 덕분: Rick Anderson, Levi Broderick, Barry Dorrans, Tom Dykstra, Hongmei Ge, David Matson, Daniel Roth, Tim Teebken 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-114">Thanks to the people who reviewed this series and provided valuable feedback: Rick Anderson, Levi Broderick, Barry Dorrans, Tom Dykstra, Hongmei Ge, David Matson, Daniel Roth, Tim Teebken.</span></span>


## <a name="authentication"></a><span data-ttu-id="c8416-115">인증</span><span class="sxs-lookup"><span data-stu-id="c8416-115">Authentication</span></span>

<span data-ttu-id="c8416-116">Web API 호스트에서 발생 하는 인증을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-116">Web API assumes that authentication happens in the host.</span></span> <span data-ttu-id="c8416-117">웹 호스팅에 대 한 호스트가 인증에 대 한 HTTP 모듈을 사용 하는 IIS입니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-117">For web-hosting, the host is IIS, which uses HTTP modules for authentication.</span></span> <span data-ttu-id="c8416-118">IIS 또는 ASP.NET에 기본 제공 인증 모듈 중 하나를 사용 하도록 프로젝트를 구성할 수도 있고 사용자 지정 인증을 수행 하도록 사용자 고유의 HTTP 모듈을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-118">You can configure your project to use any of the authentication modules built in to IIS or ASP.NET, or write your own HTTP module to perform custom authentication.</span></span>

<span data-ttu-id="c8416-119">호스트에서 사용자를 인증 하는 경우 생성을 *주체*, 되는 [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) 코드가 실행 되는 보안 컨텍스트를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-119">When the host authenticates the user, it creates a *principal*, which is an [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) object that represents the security context under which code is running.</span></span> <span data-ttu-id="c8416-120">호스트를 현재 스레드에서 보안 주체를 설정 하 여 연결 **Thread.CurrentPrincipal**합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-120">The host attaches the principal to the current thread by setting **Thread.CurrentPrincipal**.</span></span> <span data-ttu-id="c8416-121">연결 된 보안 주체가 포함 **Identity** 사용자에 대 한 정보를 포함 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-121">The principal contains an associated **Identity** object that contains information about the user.</span></span> <span data-ttu-id="c8416-122">사용자가 인증 하는 경우는 **Identity.IsAuthenticated** 속성이 반환 **true**합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-122">If the user is authenticated, the **Identity.IsAuthenticated** property returns **true**.</span></span> <span data-ttu-id="c8416-123">익명 요청에 대 한 **IsAuthenticated** 반환 **false**합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-123">For anonymous requests, **IsAuthenticated** returns **false**.</span></span> <span data-ttu-id="c8416-124">보안 주체에 대 한 자세한 내용은 참조 하세요. [역할 기반 보안](https://msdn.microsoft.com/library/shz8h065.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-124">For more information about principals, see [Role-Based Security](https://msdn.microsoft.com/library/shz8h065.aspx).</span></span>

### <a name="http-message-handlers-for-authentication"></a><span data-ttu-id="c8416-125">인증에 대 한 HTTP 메시지 처리기</span><span class="sxs-lookup"><span data-stu-id="c8416-125">HTTP Message Handlers for Authentication</span></span>

<span data-ttu-id="c8416-126">인증에 대 한 호스트를 사용 하는 대신 인증 논리를 넣을 수 있습니다는 [HTTP 메시지 처리기](../advanced/http-message-handlers.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-126">Instead of using the host for authentication, you can put authentication logic into an [HTTP message handler](../advanced/http-message-handlers.md).</span></span> <span data-ttu-id="c8416-127">이런 경우 메시지 처리기는 HTTP 요청을 검사 하 고 보안 주체를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-127">In that case, the message handler examines the HTTP request and sets the principal.</span></span>

<span data-ttu-id="c8416-128">인증에 대 한 메시지 처리기를 사용 해야는 경우</span><span class="sxs-lookup"><span data-stu-id="c8416-128">When should you use message handlers for authentication?</span></span> <span data-ttu-id="c8416-129">절충은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-129">Here are some tradeoffs:</span></span>

- <span data-ttu-id="c8416-130">HTTP 모듈은 ASP.NET 파이프라인을 통과 하는 모든 요청을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-130">An HTTP module sees all requests that go through the ASP.NET pipeline.</span></span> <span data-ttu-id="c8416-131">메시지 처리기는 Web API 요청 에서만 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-131">A message handler only sees requests that are routed to Web API.</span></span>
- <span data-ttu-id="c8416-132">특정 경로 인증 체계를 적용할 수 있는 경로 당 메시지 처리기를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-132">You can set per-route message handlers, which lets you apply an authentication scheme to a specific route.</span></span>
- <span data-ttu-id="c8416-133">HTTP 모듈 IIS와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-133">HTTP modules are specific to IIS.</span></span> <span data-ttu-id="c8416-134">메시지 처리기 호스트 중립적 되므로 웹 호스팅 및 자체 호스팅을 사용 하 여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-134">Message handlers are host-agnostic, so they can be used with both web-hosting and self-hosting.</span></span>
- <span data-ttu-id="c8416-135">HTTP 모듈은 IIS 로깅, 감사 등에 참여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-135">HTTP modules participate in IIS logging, auditing, and so on.</span></span>
- <span data-ttu-id="c8416-136">HTTP 모듈 파이프라인의 이전 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-136">HTTP modules run earlier in the pipeline.</span></span> <span data-ttu-id="c8416-137">메시지 처리기에서 인증을 처리 하는 경우에 처리기가 실행 가져오기 주 설정지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-137">If you handle authentication in a message handler, the principal does not get set until the handler runs.</span></span> <span data-ttu-id="c8416-138">또한 응답 메시지 처리기를 벗어나면에 이전 주 서버 보안 주체가 되돌립니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-138">Moreover, the principal reverts back to the previous principal when the response leaves the message handler.</span></span>

<span data-ttu-id="c8416-139">일반적으로 자체 호스팅을 지원 하기 위해 필요 하지 않으면, HTTP 모듈은 더 나은 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-139">Generally, if you don't need to support self-hosting, an HTTP module is a better option.</span></span> <span data-ttu-id="c8416-140">자체 호스팅을 지원 해야 할 경우 메시지 처리기를 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-140">If you need to support self-hosting, consider a message handler.</span></span>

### <a name="setting-the-principal"></a><span data-ttu-id="c8416-141">보안 주체를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-141">Setting the Principal</span></span>

<span data-ttu-id="c8416-142">사용자 지정 인증 논리를 수행 하는 응용 프로그램을 두 위치에서 보안 주체가 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-142">If your application performs any custom authentication logic, you must set the principal on two places:</span></span>

- <span data-ttu-id="c8416-143">**Thread.CurrentPrincipal**.</span><span class="sxs-lookup"><span data-stu-id="c8416-143">**Thread.CurrentPrincipal**.</span></span> <span data-ttu-id="c8416-144">이 속성은.NET의 스레드 보안 주체를 설정 하는 표준 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-144">This property is the standard way to set the thread's principal in .NET.</span></span>
- <span data-ttu-id="c8416-145">**HttpContext.Current.User**.</span><span class="sxs-lookup"><span data-stu-id="c8416-145">**HttpContext.Current.User**.</span></span> <span data-ttu-id="c8416-146">이 속성은 ASP.NET에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-146">This property is specific to ASP.NET.</span></span>

<span data-ttu-id="c8416-147">다음 코드는 보안 주체를 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-147">The following code shows how to set the principal:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="c8416-148">웹 호스팅을 위한; 양쪽 모두에서 보안 주체를 설정 해야 합니다. 그렇지 않은 경우 보안 컨텍스트는 일관 되지 않은 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-148">For web-hosting, you must set the principal in both places; otherwise the security context may become inconsistent.</span></span> <span data-ttu-id="c8416-149">그러나 자체 호스팅, **HttpContext.Current** null입니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-149">For self-hosting, however, **HttpContext.Current** is null.</span></span> <span data-ttu-id="c8416-150">코드는 호스트-알 수 있도록 따라서 null 확인을 할당 하기 전에 **HttpContext.Current**표시 된 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-150">To ensure your code is host-agnostic, therefore, check for null before assigning to **HttpContext.Current**, as shown.</span></span>

## <a name="authorization"></a><span data-ttu-id="c8416-151">Authorization</span><span class="sxs-lookup"><span data-stu-id="c8416-151">Authorization</span></span>

<span data-ttu-id="c8416-152">파이프라인에서 나중에 발생 하는 권한 부여 컨트롤러에 가까운 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-152">Authorization happens later in the pipeline, closer to the controller.</span></span> <span data-ttu-id="c8416-153">기능을 사용 하면 리소스에 대 한 액세스 권한을 부여 하면 더 세분화 된 항목을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-153">That lets you make more granular choices when you grant access to resources.</span></span>

- <span data-ttu-id="c8416-154">*권한 부여 필터* 컨트롤러 작업 보다 먼저 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-154">*Authorization filters* run before the controller action.</span></span> <span data-ttu-id="c8416-155">요청 받지 않은 필터 오류 응답을 반환 하 고 작업 호출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-155">If the request is not authorized, the filter returns an error response, and the action is not invoked.</span></span>
- <span data-ttu-id="c8416-156">컨트롤러 작업 내에서 현재 주 서버를 가져올 수 있습니다 합니다 **ApiController.User** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-156">Within a controller action, you can get the current principal from the **ApiController.User** property.</span></span> <span data-ttu-id="c8416-157">예를 들어, 해당 사용자에 게 속하는 리소스에만 반환 합니다. 사용자 이름을 기반으로 하는 리소스의 목록을 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-157">For example, you might filter a list of resources based on the user name, returning only those resources that belong to that user.</span></span>

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a><span data-ttu-id="c8416-158">사용 하 여 [권한 부여] 특성</span><span class="sxs-lookup"><span data-stu-id="c8416-158">Using the [Authorize] Attribute</span></span>

<span data-ttu-id="c8416-159">기본 제공 권한 부여 필터를 제공 하는 web API [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-159">Web API provides a built-in authorization filter, [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx).</span></span> <span data-ttu-id="c8416-160">이 필터는 사용자가 인증 되었는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-160">This filter checks whether the user is authenticated.</span></span> <span data-ttu-id="c8416-161">그렇지 않은 경우 다음 작업을 호출 하지 않고 HTTP 상태 코드 401 (권한 없음)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-161">If not, it returns HTTP status code 401 (Unauthorized), without invoking the action.</span></span>

<span data-ttu-id="c8416-162">컨트롤러 수준에서 전역으로 또는 개별 작업 수준에서 필터를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-162">You can apply the filter globally, at the controller level, or at the level of individual actions.</span></span>

<span data-ttu-id="c8416-163">**전 세계**: 모든 Web API 컨트롤러에 대 한 액세스를 제한 하려면 추가 된 **AuthorizeAttribute** 필터를 전역 필터 목록:</span><span class="sxs-lookup"><span data-stu-id="c8416-163">**Globally**: To restrict access for every Web API controller, add the **AuthorizeAttribute** filter to the global filter list:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="c8416-164">**컨트롤러**: 특정 컨트롤러에 대 한 액세스를 제한 하려면 필터 특성으로 컨트롤러에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-164">**Controller**: To restrict access for a specific controller, add the filter as an attribute to the controller:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="c8416-165">**작업**: 특정 작업에 대 한 액세스를 제한 하려면 동작 메서드에 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-165">**Action**: To restrict access for specific actions, add the attribute to the action method:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="c8416-166">컨트롤러를 제한 한 다음 사용 하 여 특정 작업에 대 한 익명 액세스를 허용 하는 또는 `[AllowAnonymous]` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-166">Alternatively, you can restrict the controller and then allow anonymous access to specific actions, by using the `[AllowAnonymous]` attribute.</span></span> <span data-ttu-id="c8416-167">다음 예제에서는 `Post` 메서드는 제한 되지만 `Get` 익명 액세스를 허용 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="c8416-167">In the following example, the `Post` method is restricted, but the `Get` method allows anonymous access.</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="c8416-168">이전 예제에서는 필터는 제한 된 메서드를 액세스 하려면 인증 된 모든 사용자를 수 있습니다. 익명 사용자만 유지 됩니다. 특정 역할에 사용자 또는 특정 사용자에 게 액세스를 제한할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-168">In the previous examples, the filter allows any authenticated user to access the restricted methods; only anonymous users are kept out. You can also limit access to specific users or to users in specific roles:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> <span data-ttu-id="c8416-169">합니다 **AuthorizeAttribute** Web API 컨트롤러에 대 한 필터에는 **System.Web.Http** 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-169">The **AuthorizeAttribute** filter for Web API controllers is located in the **System.Web.Http** namespace.</span></span> <span data-ttu-id="c8416-170">MVC 컨트롤러에 대 한 유사한 필터를 **System.Web.Mvc** 네임 스페이스에 Web API 컨트롤러와 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-170">There is a similar filter for MVC controllers in the **System.Web.Mvc** namespace, which is not compatible with Web API controllers.</span></span>


### <a name="custom-authorization-filters"></a><span data-ttu-id="c8416-171">사용자 지정 권한 부여 필터</span><span class="sxs-lookup"><span data-stu-id="c8416-171">Custom Authorization Filters</span></span>

<span data-ttu-id="c8416-172">사용자 지정 권한 부여 필터를 작성 하려면 이러한 형식 중 하나에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-172">To write a custom authorization filter, derive from one of these types:</span></span>

- <span data-ttu-id="c8416-173">**AuthorizeAttribute**합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-173">**AuthorizeAttribute**.</span></span> <span data-ttu-id="c8416-174">현재 사용자 및 사용자의 역할 기반 권한 부여 논리를 수행 하려면이 클래스를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-174">Extend this class to perform authorization logic based on the current user and the user's roles.</span></span>
- <span data-ttu-id="c8416-175">**AuthorizationFilterAttribute**합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-175">**AuthorizationFilterAttribute**.</span></span> <span data-ttu-id="c8416-176">현재 사용자 또는 역할에 기반 하지 않는 동기 권한 부여 논리를 수행 하려면이 클래스를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-176">Extend this class to perform synchronous authorization logic that is not necessarily based on the current user or role.</span></span>
- <span data-ttu-id="c8416-177">**IAuthorizationFilter**합니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-177">**IAuthorizationFilter**.</span></span> <span data-ttu-id="c8416-178">비동기 권한 부여 논리를 수행 하려면이 인터페이스를 구현 합니다. 예를 들어, 권한 부여 논리에 비동기 I/O 또는 네트워크 호출을 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="c8416-178">Implement this interface to perform asynchronous authorization logic; for example, if your authorization logic makes asynchronous I/O or network calls.</span></span> <span data-ttu-id="c8416-179">(사용자 권한 부여 논리 CPU 바인딩된 경우 것이 더 간단를 파생할 **AuthorizationFilterAttribute**이므로 다음 비동기 메서드를 작성할 필요가 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="c8416-179">(If your authorization logic is CPU-bound, it is simpler to derive from **AuthorizationFilterAttribute**, because then you don't need to write an asynchronous method.)</span></span>

<span data-ttu-id="c8416-180">다음 다이어그램의 클래스 계층 구조를 표시 합니다 **AuthorizeAttribute** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-180">The following diagram shows the class hierarchy for the **AuthorizeAttribute** class.</span></span>

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a><span data-ttu-id="c8416-181">내부 컨트롤러 작업 권한 부여</span><span class="sxs-lookup"><span data-stu-id="c8416-181">Authorization Inside a Controller Action</span></span>

<span data-ttu-id="c8416-182">경우에 따라 계속 되지만 원칙을 기반으로 동작을 변경 하는 요청을 허용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-182">In some cases, you might allow a request to proceed, but change the behavior based on the principal.</span></span> <span data-ttu-id="c8416-183">예를 들어, 정보를 반환 하는 사용자의 역할에 따라 변경 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-183">For example, the information that you return might change depending on the user's role.</span></span> <span data-ttu-id="c8416-184">컨트롤러 메서드 내에서 현재 사용자를 가져올 수 있습니다 합니다 **ApiController.User** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c8416-184">Within a controller method, you can get the current principle from the **ApiController.User** property.</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
