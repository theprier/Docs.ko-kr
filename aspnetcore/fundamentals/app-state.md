---
title: "ASP.NET Core에서 세션 및 응용 프로그램 상태"
author: rick-anderson
description: "요청 간에 응용 프로그램 및 사용자(세션) 상태를 유지하는 접근 방법입니다."
manager: wpickett
ms.author: riande
ms.custom: H1Hack27Feb2017
ms.date: 11/27/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/app-state
ms.openlocfilehash: f4ed38f7395e3f4fe939584c1f3f5b0dba93724c
ms.sourcegitcommit: f2a11a89037471a77ad68a67533754b7bb8303e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="introduction-to-session-and-application-state-in-aspnet-core"></a><span data-ttu-id="98865-103">ASP.NET Core에서 세션 및 응용 프로그램 상태 소개</span><span class="sxs-lookup"><span data-stu-id="98865-103">Introduction to session and application state in ASP.NET Core</span></span>

<span data-ttu-id="98865-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT), [Steve Smith](https://ardalis.com/) 및 [Diana LaRose](https://github.com/DianaLaRose)</span><span class="sxs-lookup"><span data-stu-id="98865-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Steve Smith](https://ardalis.com/), and [Diana LaRose](https://github.com/DianaLaRose)</span></span>

<span data-ttu-id="98865-105">HTTP는 상태 비저장 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="98865-105">HTTP is a stateless protocol.</span></span> <span data-ttu-id="98865-106">웹 서버는 독립적인 요청으로 각 HTTP 요청을 처리하고 이전 요청에서 사용자 값을 유지하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-106">A web server treats each HTTP request as an independent request and doesn't retain user values from previous requests.</span></span> <span data-ttu-id="98865-107">이 문서에서는 요청 간에 응용 프로그램 및 세션 상태를 유지하기 위한 다양한 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-107">This article discusses different ways to preserve application and session state between requests.</span></span> 

## <a name="session-state"></a><span data-ttu-id="98865-108">세션 상태</span><span class="sxs-lookup"><span data-stu-id="98865-108">Session state</span></span>

<span data-ttu-id="98865-109">세션 상태는 사용자가 웹앱을 탐색하는 동안 사용자 데이터를 저장하는 데 사용할 수 있는 ASP.NET Core의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="98865-109">Session state is a feature in ASP.NET Core that you can use to save and store user data while the user browses your web app.</span></span> <span data-ttu-id="98865-110">서버에서 사전 또는 해시 테이블로 구성하여 세션 상태는 브라우저에서 요청 간 데이터를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-110">Consisting of a dictionary or hash table on the server, session state persists data across requests from a browser.</span></span> <span data-ttu-id="98865-111">세션 데이터는 캐시에 의해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="98865-111">The session data is backed by a cache.</span></span>

<span data-ttu-id="98865-112">ASP.NET Core는 클라이언트에 각 요청과 함께 서버에 전송된 세션 ID를 포함하는 쿠키를 제공하여 세션 상태를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-112">ASP.NET Core maintains session state by giving the client a cookie that contains the session ID, which is sent to the server with each request.</span></span> <span data-ttu-id="98865-113">서버는 세션 ID를 사용하여 세션 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="98865-113">The server uses the session ID to fetch the session data.</span></span> <span data-ttu-id="98865-114">세션 쿠키는 브라우저와 관련되기 때문에 브라우저에서 세션을 공유할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-114">Because the session cookie is specific to the browser, you cannot share sessions across browsers.</span></span> <span data-ttu-id="98865-115">세션 쿠키는 브라우저 세션이 끝나면 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="98865-115">Session cookies are deleted only when the browser session ends.</span></span> <span data-ttu-id="98865-116">쿠키가 만료된 세션에 대해 수신되면 동일한 세션 쿠키를 사용하는 새 세션이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="98865-116">If a cookie is received for an expired session, a new session that uses the same session cookie  is created.</span></span> 

<span data-ttu-id="98865-117">서버는 마지막 요청 이후 제한된 시간에 대한 세션을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-117">The server retains a session for a limited time after the last request.</span></span> <span data-ttu-id="98865-118">세션 제한 시간을 설정하거나 20분의 기본값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-118">Either set the session timeout or use the default value of 20 minutes.</span></span> <span data-ttu-id="98865-119">세션 상태는 특정 세션에 고유한 사용자 데이터를 저장하는 데 이상적이지만 영구적으로 유지될 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-119">Session state is ideal for storing user data that's specific to a particular session but doesn't need to be persisted permanently.</span></span> <span data-ttu-id="98865-120">데이터는 `Session.Clear`를 호출하거나 세션이 데이터 저장소에서 만료될 때 백업 저장소에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="98865-120">Data is deleted from the backing store either when calling `Session.Clear` or when the session expires in the data store.</span></span> <span data-ttu-id="98865-121">서버는 브라우저가 닫히는 경우 또는 세션 쿠키가 삭제되는 경우를 알지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-121">The server doesn't know when the browser is closed or when the session cookie is deleted.</span></span>

> [!WARNING]
> <span data-ttu-id="98865-122">세션에 중요한 데이터를 저장하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="98865-122">Don't store sensitive data in session.</span></span> <span data-ttu-id="98865-123">클라이언트는 브라우저를 닫거나 세션 쿠키를 삭제하지 못할 수 있습니다(일부 브라우저는 창에서 세션 쿠키를 활성 상태로 유지).</span><span class="sxs-lookup"><span data-stu-id="98865-123">The client might not close the browser and clear the session cookie (and some browsers keep session cookies alive across windows).</span></span> <span data-ttu-id="98865-124">또한 세션은 단일 사용자로 제한될 수 없습니다. 다음 사용자는 동일한 세션으로 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-124">Also, a session might not be restricted to a single user; the next user might continue with the same session.</span></span>

<span data-ttu-id="98865-125">메모리 내 세션 공급자는 로컬 서버에 세션 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-125">The in-memory session provider stores session data on the local server.</span></span> <span data-ttu-id="98865-126">서버 팜에서 웹앱을 실행하려는 경우 특정 서버에 각 세션을 연결하도록 고정 세션을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-126">If you plan to run your web app on a server farm, you must use sticky sessions to tie each session to a specific server.</span></span> <span data-ttu-id="98865-127">Windows Azure 웹 사이트 플랫폼은 고정 세션을 기본값으로 설정합니다(응용 프로그램 요청 라우팅 또는 ARR).</span><span class="sxs-lookup"><span data-stu-id="98865-127">The Windows Azure Web Sites platform defaults to sticky sessions (Application Request Routing or ARR).</span></span> <span data-ttu-id="98865-128">그러나 고정 세션은 확장성에 영향을 주고 웹앱 업데이트를 복잡하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-128">However, sticky sessions can affect scalability and complicate web app updates.</span></span> <span data-ttu-id="98865-129">더 나은 옵션은 고정 세션이 필요하지 않은 Redis 또는 SQL Server 분산 캐시를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="98865-129">A better option is to use the Redis or SQL Server distributed caches, which don't require sticky sessions.</span></span> <span data-ttu-id="98865-130">자세한 내용은 [분산 캐시 사용](xref:performance/caching/distributed)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98865-130">For more information, see [Working with a Distributed Cache](xref:performance/caching/distributed).</span></span> <span data-ttu-id="98865-131">서비스 공급자 설정에 대한 자세한 내용은 이 문서의 뒷부분에 나오는 [세션 구성](#configuring-session)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98865-131">For details on setting up service providers, see [Configuring Session](#configuring-session) later in this article.</span></span>

<a name="temp"></a>
## <a name="tempdata"></a><span data-ttu-id="98865-132">TempData</span><span class="sxs-lookup"><span data-stu-id="98865-132">TempData</span></span>

<span data-ttu-id="98865-133">ASP.NET Core MVC는 [컨트롤러](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.controller?view=aspnetcore-2.0)에서 [TempData](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Controller_TempData) 속성을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-133">ASP.NET Core MVC exposes the [TempData](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Controller_TempData) property on a [controller](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.controller?view=aspnetcore-2.0).</span></span> <span data-ttu-id="98865-134">이 속성은 판독될 때까지 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-134">This property stores data until it's read.</span></span> <span data-ttu-id="98865-135">`Keep` 및 `Peek` 메서드를 사용하여 삭제 없이 데이터를 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-135">The `Keep` and `Peek` methods can be used to examine the data without deletion.</span></span> <span data-ttu-id="98865-136">`TempData`는 두 개 이상의 요청에 대한 데이터가 필요할 경우 리디렉션에 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-136">`TempData` is particularly useful for redirection, when data is needed for more than a single request.</span></span> <span data-ttu-id="98865-137">`TempData`는 TempData 공급자에 의해 구현됩니다(예: 쿠키 또는 세션 상태 사용).</span><span class="sxs-lookup"><span data-stu-id="98865-137">`TempData` is implemented by TempData providers, for example, using either cookies or session state.</span></span>

<a name="tempdata-providers"></a>
### <a name="tempdata-providers"></a><span data-ttu-id="98865-138">TempData 공급자</span><span class="sxs-lookup"><span data-stu-id="98865-138">TempData providers</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="98865-139">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="98865-139">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="98865-140">ASP.NET Core 2.0 이상에서 쿠키 기반 TempData 공급자는 TempData를 쿠키에 저장하는 데 기본적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="98865-140">In ASP.NET Core 2.0 and later, the cookie-based TempData provider is used by default to store TempData in cookies.</span></span>

<span data-ttu-id="98865-141">쿠키 데이터는 [Base64UrlTextEncoder](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.webutilities.base64urltextencoder?view=aspnetcore-2.0)로 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="98865-141">The cookie data is encoded with the [Base64UrlTextEncoder](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.webutilities.base64urltextencoder?view=aspnetcore-2.0).</span></span> <span data-ttu-id="98865-142">쿠키는 암호화되고 청크되므로 ASP.NET Core 1.x에서 확인한 단일 쿠키 크기 제한은 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-142">Because the cookie is encrypted and chunked, the single cookie size limit found in ASP.NET Core 1.x does not apply.</span></span> <span data-ttu-id="98865-143">암호화된 데이터를 압축하는 것은 [범죄](https://wikipedia.org/wiki/CRIME_(security_exploit)) 및 [위반](https://wikipedia.org/wiki/BREACH_(security_exploit)) 공격과 같은 보안 문제를 일으킬 수 있으므로 쿠키 데이터는 압축되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-143">The cookie data is not compressed because compressing encrypted data can lead to security problems such as the [CRIME](https://wikipedia.org/wiki/CRIME_(security_exploit)) and [BREACH](https://wikipedia.org/wiki/BREACH_(security_exploit)) attacks.</span></span> <span data-ttu-id="98865-144">쿠키 기반 TempData 공급자에 대한 자세한 내용은 [CookieTempDataProvider](https://github.com/aspnet/Mvc/blob/dev/src/Microsoft.AspNetCore.Mvc.ViewFeatures/ViewFeatures/CookieTempDataProvider.cs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98865-144">For more information on the cookie-based TempData provider, see [CookieTempDataProvider](https://github.com/aspnet/Mvc/blob/dev/src/Microsoft.AspNetCore.Mvc.ViewFeatures/ViewFeatures/CookieTempDataProvider.cs).</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="98865-145">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="98865-145">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="98865-146">ASP.NET Core 1.0 및 1.1에서는 세션 상태 TempData 공급자가 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="98865-146">In ASP.NET Core 1.0 and 1.1, the session state TempData provider is the default.</span></span>

--------------

<a name="choose-temp"></a>
### <a name="choosing-a-tempdata-provider"></a><span data-ttu-id="98865-147">TempData 공급자 선택</span><span class="sxs-lookup"><span data-stu-id="98865-147">Choosing a TempData provider</span></span>

<span data-ttu-id="98865-148">TempData 공급자를 선택하는 데는 다음과 같은 몇 가지 고려 사항이 수반됩니다.</span><span class="sxs-lookup"><span data-stu-id="98865-148">Choosing a TempData provider involves several considerations, such as:</span></span>

1. <span data-ttu-id="98865-149">응용 프로그램이 이미 다른 용도에 세션 상태를 사용합니까?</span><span class="sxs-lookup"><span data-stu-id="98865-149">Does the application already use session state for other purposes?</span></span> <span data-ttu-id="98865-150">그런 경우 세션 상태 TempData 공급자 사용에는 응용 프로그램에 대한 추가 비용이 없습니다(데이터 크기 외에).</span><span class="sxs-lookup"><span data-stu-id="98865-150">If so, using the session state TempData provider has no additional cost to the application (aside from the size of the data).</span></span>
2. <span data-ttu-id="98865-151">응용 프로그램은 상대적으로 적은 양의 데이터에 TempData만 제한적으로 사용합니까(최대 500바이트)?</span><span class="sxs-lookup"><span data-stu-id="98865-151">Does the application use TempData only sparingly, for relatively small amounts of data (up to 500 bytes)?</span></span> <span data-ttu-id="98865-152">그런 경우 쿠키 TempData 공급자는 TempData를 전달하는 각 요청에 적은 비용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-152">If so, the cookie TempData provider will add a small cost to each request that carries TempData.</span></span> <span data-ttu-id="98865-153">그렇지 않은 경우 세션 상태 TempData 공급자는 TempData가 사용될 때까지 각 요청에서 많은 양의 데이터를 왕복 작업하지 않도록 하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-153">If not, the session state TempData provider can be beneficial to avoid round-tripping a large amount of data in each request until the TempData is consumed.</span></span>
3. <span data-ttu-id="98865-154">응용 프로그램은 웹 팜(다중 서버)에서 실행됩니까?</span><span class="sxs-lookup"><span data-stu-id="98865-154">Does the application run in a web farm (multiple servers)?</span></span> <span data-ttu-id="98865-155">그런 경우 쿠키 TempData 공급자를 사용하는 데 필요한 추가 구성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-155">If so, there's no additional configuration needed to use the cookie TempData provider.</span></span>

> [!NOTE]
> <span data-ttu-id="98865-156">대부분의 웹 클라이언트(예: 웹 브라우저)는 각 쿠키의 최대 크기, 쿠키의 총 수 또는 둘 다에 제한을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-156">Most web clients (such as web browsers) enforce limits on the maximum size of each cookie, the total number of cookies, or both.</span></span> <span data-ttu-id="98865-157">따라서 쿠키 TempData 공급자를 사용하는 경우 앱이 이러한 제한을 초과하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-157">Therefore, when using the cookie TempData provider, verify the app won't exceed these limits.</span></span> <span data-ttu-id="98865-158">암호화의 오버헤드 및 청크를 확인하여 데이터의 전체 크기를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-158">Consider the total size of the data, accounting for the overheads of encryption and chunking.</span></span>

<a name="config-temp"></a>
### <a name="configure-the-tempdata-provider"></a><span data-ttu-id="98865-159">TempData 공급자 구성</span><span class="sxs-lookup"><span data-stu-id="98865-159">Configure the TempData provider</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="98865-160">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="98865-160">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="98865-161">쿠키 기반 TempData 공급자는 기본적으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="98865-161">The cookie-based TempData provider is enabled by default.</span></span> <span data-ttu-id="98865-162">다음 `Startup` 클래스 코드는 세션 기반 TempData 공급자를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-162">The following `Startup` class code configures the session-based TempData provider:</span></span>

[!code-csharp[](app-state/sample/src/WebAppSessionDotNetCore2.0App/StartupTempDataSession.cs?name=snippet_TempDataSession&highlight=4,6,11)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="98865-163">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="98865-163">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="98865-164">다음 `Startup` 클래스 코드는 세션 기반 TempData 공급자를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-164">The following `Startup` class code configures the session-based TempData provider:</span></span>

[!code-csharp[](app-state/sample/src/WebAppSession/StartupTempDataSession.cs?name=snippet_TempDataSession&highlight=4,9)]

---

<span data-ttu-id="98865-165">순서 지정은 미들웨어 구성 요소에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-165">Ordering is critical for middleware components.</span></span> <span data-ttu-id="98865-166">위의 예에서 `UseMvcWithDefaultRoute` 후에 `UseSession`이 호출되는 경우 형식 `InvalidOperationException`의 예외가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-166">In the preceding example, an exception of type `InvalidOperationException` occurs when `UseSession` is invoked after `UseMvcWithDefaultRoute`.</span></span> <span data-ttu-id="98865-167">자세한 내용은 [미들웨어 순서 지정](xref:fundamentals/middleware/index#ordering)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98865-167">See [Middleware Ordering](xref:fundamentals/middleware/index#ordering) for more detail.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98865-168">.NET Framework를 대상으로 하고 세션 기반 공급자를 사용하는 경우 [Microsoft.AspNetCore.Session](https://www.nuget.org/packages/Microsoft.AspNetCore.Session) NuGet 패키지를 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-168">If targeting .NET Framework and using the session-based provider, add the [Microsoft.AspNetCore.Session](https://www.nuget.org/packages/Microsoft.AspNetCore.Session) NuGet package to your project.</span></span>

## <a name="query-strings"></a><span data-ttu-id="98865-169">쿼리 문자열</span><span class="sxs-lookup"><span data-stu-id="98865-169">Query strings</span></span>

<span data-ttu-id="98865-170">새 요청의 쿼리 문자열에 추가하여 한 요청에서 다른 요청으로 제한된 양의 데이터를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-170">You can pass a limited amount of data from one request to another by adding it to the new request's query string.</span></span> <span data-ttu-id="98865-171">이는 이메일 또는 소셜 네트워크를 통해 공유되도록 포함된 상태가 있는 링크를 허용하는 영구적인 방식으로 상태를 캡처하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-171">This is useful for capturing state in a persistent manner that allows links with embedded state to be shared through email or social networks.</span></span> <span data-ttu-id="98865-172">그러나 이러한 이유로 중요한 데이터에 쿼리 문자열을 절대 사용하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98865-172">However, for this reason, you should never use query strings for sensitive data.</span></span> <span data-ttu-id="98865-173">쉽게 공유되는 것 뿐만 아니라 쿼리 문자열에 데이터를 포함하면 사용자가 인증되는 동안 악성 사이트를 방문하도록 유도할 수 있는 [CSRF(교차 사이트 요청 위조)](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)) 공격에 대한 기회를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-173">In addition to being easily shared, including data in query strings can create opportunities for [Cross-Site Request Forgery (CSRF)](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)) attacks, which can trick users into visiting malicious sites while authenticated.</span></span> <span data-ttu-id="98865-174">공격자는 앱에서 사용자 데이터를 도용하거나 사용자를 대신하여 악의적인 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-174">Attackers can then steal user data from your app or take malicious actions on behalf of the user.</span></span> <span data-ttu-id="98865-175">유지된 모든 응용 프로그램 또는 세션 상태를 CSRF 공격으로부터 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-175">Any preserved application or session state must protect against CSRF attacks.</span></span> <span data-ttu-id="98865-176">CSRF 공격에 대한 자세한 내용은 [ASP.NET Core에서 교차 사이트 요청 위조(XSRF/CSRF) 공격 방지](../security/anti-request-forgery.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98865-176">For more information on CSRF attacks, see [Preventing Cross-Site Request Forgery (XSRF/CSRF) Attacks in ASP.NET Core](../security/anti-request-forgery.md).</span></span>

## <a name="post-data-and-hidden-fields"></a><span data-ttu-id="98865-177">데이터 게시 및 숨겨진 필드</span><span class="sxs-lookup"><span data-stu-id="98865-177">Post data and hidden fields</span></span>

<span data-ttu-id="98865-178">데이터는 숨겨진 양식 필드에 저장되고 다음 요청에서 다시 게시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-178">Data can be saved in hidden form fields and posted back on the next request.</span></span> <span data-ttu-id="98865-179">이는 다중 페이지 폼에서 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="98865-179">This is common in multi-page forms.</span></span> <span data-ttu-id="98865-180">그러나 클라이언트는 잠재적으로 데이터를 변조할 수 있으므로 서버는 항상 유효성을 다시 검사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-180">However, because the client can potentially tamper with the data, the server must always revalidate it.</span></span> 

## <a name="cookies"></a><span data-ttu-id="98865-181">쿠키</span><span class="sxs-lookup"><span data-stu-id="98865-181">Cookies</span></span>

<span data-ttu-id="98865-182">쿠키는 웹 응용 프로그램에서 사용자 관련 데이터를 저장하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-182">Cookies provide a way to store user-specific data in web applications.</span></span> <span data-ttu-id="98865-183">쿠키는 모든 요청과 함께 전송되므로 해당 크기는 최소로 유지되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-183">Because cookies are sent with every request, their size should be kept to a minimum.</span></span> <span data-ttu-id="98865-184">이상적으로 식별자만 서버에 저장된 실제 데이터와 함께 쿠키에 저장되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-184">Ideally, only an identifier should be stored in a cookie with the actual data stored on the server.</span></span> <span data-ttu-id="98865-185">대부분의 브라우저는 4096바이트로 쿠키를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-185">Most browsers restrict cookies to 4096 bytes.</span></span> <span data-ttu-id="98865-186">또한 제한된 개수의 쿠키를 각 도메인에 대해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-186">In addition, only a limited number of cookies are available for each domain.</span></span>  

<span data-ttu-id="98865-187">쿠키는 변조될 수 있기 때문에 서버에서 유효성을 검사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-187">Because cookies are subject to tampering, they must be validated on the server.</span></span> <span data-ttu-id="98865-188">클라이언트에서 쿠키의 지속성은 사용자 작업 및 만료에 종속되지만 일반적으로 클라이언트에서 데이터 지속성의 가장 영구적인 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="98865-188">Although the durability of the cookie on a client is subject to user intervention and expiration, they're generally the most durable form of data persistence on the client.</span></span>

<span data-ttu-id="98865-189">쿠키는 종종 개인 설정에 사용됩니다. 여기서 콘텐츠는 알려진 사용자에 대해 사용자 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="98865-189">Cookies are often used for personalization, where content is customized for a known user.</span></span> <span data-ttu-id="98865-190">사용자만 식별되고 대부분의 경우에서 인증되지 않기 때문에 사용자 이름, 계정 이름 또는 고유한 사용자 ID(예: GUID)를 쿠키에 저장하여 쿠키를 일반적으로 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-190">Because the user is only identified and not authenticated in most cases, you can typically secure a cookie by storing the user name, account name, or a unique user ID (such as a GUID) in the cookie.</span></span> <span data-ttu-id="98865-191">그런 다음, 쿠키를 사용하여 사이트의 사용자 개인 설정 인프라에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-191">You can then use the cookie to access the user personalization infrastructure of a site.</span></span>

## <a name="httpcontextitems"></a><span data-ttu-id="98865-192">HttpContext.Items</span><span class="sxs-lookup"><span data-stu-id="98865-192">HttpContext.Items</span></span>

<span data-ttu-id="98865-193">`Items` 컬렉션은 하나의 특정 요청을 처리하는 동안에만 필요한 데이터를 저장하기 위한 좋은 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="98865-193">The `Items` collection is a good location to store data that's needed only while processing one particular request.</span></span> <span data-ttu-id="98865-194">컬렉션의 콘텐츠는 각 요청 후 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="98865-194">The collection's contents are discarded after each request.</span></span> <span data-ttu-id="98865-195">`Items` 컬렉션은 요청 중에 다른 시점에서 작동하고 매개 변수를 전달할 직접 방법이 없는 경우에 통신하는 구성 요소 또는 미들웨어에 대한 방법으로 가장 잘 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="98865-195">The `Items` collection is best used as a way for components or middleware to communicate when they operate at different points in time during a request and have no direct way to pass parameters.</span></span> <span data-ttu-id="98865-196">자세한 내용은 이 항목의 뒷부분에 나오는 [HttpContext.Items 작업](#working-with-httpcontextitems)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98865-196">For more information, see [Working with HttpContext.Items](#working-with-httpcontextitems), later in this article.</span></span>

## <a name="cache"></a><span data-ttu-id="98865-197">캐시</span><span class="sxs-lookup"><span data-stu-id="98865-197">Cache</span></span>

<span data-ttu-id="98865-198">캐싱은 데이터 저장 및 검색하는 효율적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="98865-198">Caching is an efficient way to store and retrieve data.</span></span> <span data-ttu-id="98865-199">시간 및 기타 고려 사항에 따라 캐시된 항목의 수명을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-199">You can control the lifetime of cached items based on time and other considerations.</span></span> <span data-ttu-id="98865-200">[캐싱](../performance/caching/index.md)에 대해 더 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="98865-200">Learn more about [Caching](../performance/caching/index.md).</span></span>

<a name="session"></a>
## <a name="working-with-session-state"></a><span data-ttu-id="98865-201">세션 상태 사용</span><span class="sxs-lookup"><span data-stu-id="98865-201">Working with Session State</span></span>

### <a name="configuring-session"></a><span data-ttu-id="98865-202">세션 구성</span><span class="sxs-lookup"><span data-stu-id="98865-202">Configuring Session</span></span>

<span data-ttu-id="98865-203">`Microsoft.AspNetCore.Session` 패키지는 세션 상태를 관리하기 위한 미들웨어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-203">The `Microsoft.AspNetCore.Session` package provides middleware for managing session state.</span></span> <span data-ttu-id="98865-204">세션 미들웨어를 활성화하려면 `Startup`은 다음을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-204">To enable the session middleware, `Startup` must contain:</span></span>

- <span data-ttu-id="98865-205">[IDistributedCache](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.distributed.idistributedcache) 메모리 캐시 중 하나</span><span class="sxs-lookup"><span data-stu-id="98865-205">Any of the [IDistributedCache](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.distributed.idistributedcache) memory caches.</span></span> <span data-ttu-id="98865-206">`IDistributedCache` 구현은 세션에 대한 백업 저장소로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="98865-206">The `IDistributedCache` implementation is used as a backing store for session.</span></span>
- <span data-ttu-id="98865-207">NuGet 패키지 "Microsoft.AspNetCore.Session"이 필요한 [AddSession](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.dependencyinjection.sessionservicecollectionextensions#Microsoft_Extensions_DependencyInjection_SessionServiceCollectionExtensions_AddSession_Microsoft_Extensions_DependencyInjection_IServiceCollection_) 호출</span><span class="sxs-lookup"><span data-stu-id="98865-207">[AddSession](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.dependencyinjection.sessionservicecollectionextensions#Microsoft_Extensions_DependencyInjection_SessionServiceCollectionExtensions_AddSession_Microsoft_Extensions_DependencyInjection_IServiceCollection_) call, which requires NuGet package "Microsoft.AspNetCore.Session".</span></span>
- <span data-ttu-id="98865-208">[UseSession](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.sessionmiddlewareextensions#methods_) 호출</span><span class="sxs-lookup"><span data-stu-id="98865-208">[UseSession](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.sessionmiddlewareextensions#methods_) call.</span></span>

<span data-ttu-id="98865-209">다음 코드에서는 메모리 내 세션 공급자를 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="98865-209">The following code shows how to set up the in-memory session provider.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="98865-210">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="98865-210">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](app-state/sample/src/WebAppSessionDotNetCore2.0App/Startup.cs?highlight=11-19,24)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="98865-211">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="98865-211">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](app-state/sample/src/WebAppSession/Startup.cs?highlight=11-19,24)]

---

<span data-ttu-id="98865-212">설치되고 구성되면 `HttpContext`에서 세션을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-212">You can reference Session from `HttpContext` once it's installed and configured.</span></span>

<span data-ttu-id="98865-213">`UseSession`이 호출되기 전에 `Session`에 액세스하려는 경우 예외 `InvalidOperationException: Session has not been configured for this application or request`가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="98865-213">If you try to access `Session` before `UseSession` has been called, the exception `InvalidOperationException: Session has not been configured for this application or request` is thrown.</span></span>

<span data-ttu-id="98865-214">`Response` 스트림에 이미 작성을 시작한 후 새 `Session`을 만들려는 경우(즉, 세션 쿠키가 만들어지지 않음) 예외 `InvalidOperationException: The session cannot be established after the response has started`가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="98865-214">If you try to create a new `Session` (that is, no session cookie has been created) after you have already begun writing to the `Response` stream, the exception `InvalidOperationException: The session cannot be established after the response has started` is thrown.</span></span> <span data-ttu-id="98865-215">웹 서버 로그에서 예외를 확인할 수 있습니다. 브라우저에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-215">The exception can be found in the web server log; it will not be displayed in the browser.</span></span>

### <a name="loading-session-asynchronously"></a><span data-ttu-id="98865-216">세션을 비동기적으로 로드</span><span class="sxs-lookup"><span data-stu-id="98865-216">Loading Session asynchronously</span></span> 

<span data-ttu-id="98865-217">ASP.NET Core에서 기본 세션 공급자는 [ISession.LoadAsync](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.http.isession#Microsoft_AspNetCore_Http_ISession_LoadAsync) 메서드가 `TryGetValue`, `Set` 또는 `Remove` 메서드 전에 명시적으로 호출된 경우에만 기본 [IDistributedCache](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.distributed.idistributedcache) 저장소에서 비동기적으로 세션 레코드를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-217">The default session provider in ASP.NET Core loads the session record from the underlying [IDistributedCache](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.distributed.idistributedcache) store asynchronously only if the [ISession.LoadAsync](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.http.isession#Microsoft_AspNetCore_Http_ISession_LoadAsync) method is explicitly called before  the `TryGetValue`, `Set`, or `Remove` methods.</span></span> <span data-ttu-id="98865-218">`LoadAsync`가 먼저 호출되지 않은 경우 기본 세션 레코드가 동기적으로 로드되며 이는 크기를 조정하는 앱의 기능에 잠재적으로 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-218">If `LoadAsync` isn't called first, the underlying session record is loaded synchronously, which could potentially impact the ability of the app to scale.</span></span>

<span data-ttu-id="98865-219">이 패턴을 응용 프로그램에 적용하려면 `LoadAsync` 메서드가 `TryGetValue`, `Set` 또는 `Remove` 이전에 호출되지 않은 경우 예외를 throw하는 버전으로 [DistributedSessionStore](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.session.distributedsessionstore) 및 [DistributedSession](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.session.distributedsession) 구현을 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-219">To have applications enforce this pattern, wrap the [DistributedSessionStore](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.session.distributedsessionstore) and [DistributedSession](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.session.distributedsession) implementations with versions that throw an exception if the `LoadAsync` method isn't called before `TryGetValue`, `Set`, or `Remove`.</span></span> <span data-ttu-id="98865-220">서비스 컨테이너에 래핑된 버전을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-220">Register the wrapped versions in the services container.</span></span>

### <a name="implementation-details"></a><span data-ttu-id="98865-221">구현 세부 정보</span><span class="sxs-lookup"><span data-stu-id="98865-221">Implementation details</span></span>

<span data-ttu-id="98865-222">세션은 쿠키를 사용하여 단일 브라우저에서 요청을 추적하고 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-222">Session uses a cookie to track and identify requests from a single browser.</span></span> <span data-ttu-id="98865-223">기본적으로 이 쿠키는 ".AspNet.Session"이라고 하며 "/"의 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-223">By default, this cookie is named ".AspNet.Session", and it uses a path of "/".</span></span> <span data-ttu-id="98865-224">쿠키 기본값은 도메인을 지정하지 않으므로 페이지에서 클라이언트 쪽 스크립트에 사용할 수 없습니다(`CookieHttpOnly`는 `true`를 기본값으로 설정하므로).</span><span class="sxs-lookup"><span data-stu-id="98865-224">Because the cookie default doesn't specify a domain, it's not made available to the client-side script on the page (because `CookieHttpOnly` defaults to `true`).</span></span>

<span data-ttu-id="98865-225">세션 기본값을 재정의하려면 `SessionOptions`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-225">To override session defaults, use `SessionOptions`:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="98865-226">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="98865-226">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](app-state/sample/src/WebAppSessionDotNetCore2.0App/StartupCopy.cs?name=snippet1&highlight=8-12)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="98865-227">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="98865-227">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](app-state/sample/src/WebAppSession/StartupCopy.cs?name=snippet1&highlight=8-12)]

---

<span data-ttu-id="98865-228">서버는 `IdleTimeout` 속성을 사용하여 해당 콘텐츠가 중단되기 전에 유휴 상태일 수 있는 세션의 기간을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-228">The server uses the `IdleTimeout` property to determine how long a session can be idle before its contents are abandoned.</span></span> <span data-ttu-id="98865-229">이 속성은 쿠키 만료와 무관합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-229">This property is independent of the cookie expiration.</span></span> <span data-ttu-id="98865-230">세션 미들웨어(읽거나 쓰는)를 통해 전달되는 각 요청은 시간 제한을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-230">Each request that passes through the Session middleware (read from or written to) resets the timeout.</span></span>

<span data-ttu-id="98865-231">`Session`은 *잠기지 않으므로* 두 요청이 모두 세션의 콘텐츠를 수정하려고 하는 경우 마지막 요청이 첫 번째 요청을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-231">Because `Session` is *non-locking*, if two requests both attempt to modify the contents of session, the last one overrides the first.</span></span> <span data-ttu-id="98865-232">`Session`은 *일관된 세션*으로 구현됩니다. 즉, 모든 콘텐츠는 함께 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="98865-232">`Session` is implemented as a *coherent session*, which means that all the contents are stored together.</span></span> <span data-ttu-id="98865-233">세션의 다른 부분(다른 키)을 수정하는 두 요청은 여전히 서로 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-233">Two requests that are modifying different parts of the session (different keys) might still impact each other.</span></span>

### <a name="setting-and-getting-session-values"></a><span data-ttu-id="98865-234">세션 값 설정 및 가져오기</span><span class="sxs-lookup"><span data-stu-id="98865-234">Setting and getting Session values</span></span>

<span data-ttu-id="98865-235">세션은 `HttpContext`의 `Session` 속성을 통해 액세스됩니다.</span><span class="sxs-lookup"><span data-stu-id="98865-235">Session is accessed through the `Session` property on `HttpContext`.</span></span> <span data-ttu-id="98865-236">이 속성은 [ISession](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.http.isession) 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="98865-236">This property is an [ISession](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.http.isession) implementation.</span></span>

<span data-ttu-id="98865-237">다음 예제에서는 int 및 문자열 설정 및 가져오기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="98865-237">The following example shows setting and getting an int and a string:</span></span>

[!code-csharp[Main](app-state/sample/src/WebAppSession/Controllers/HomeController.cs?range=8-27,49)]

<span data-ttu-id="98865-238">다음 확장 메서드를 추가하는 경우 세션에 직렬화 가능 개체를 설정하고 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-238">If you add the following extension methods, you can set and get serializable objects to Session:</span></span>

[!code-csharp[Main](app-state/sample/src/WebAppSession/Extensions/SessionExtensions.cs)]

<span data-ttu-id="98865-239">다음 샘플에서는 직렬화 가능 개체를 설정하고 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="98865-239">The following sample shows how to set and get a serializable object:</span></span>

[!code-csharp[Main](app-state/sample/src/WebAppSession/Controllers/HomeController.cs?name=snippet2)]


## <a name="working-with-httpcontextitems"></a><span data-ttu-id="98865-240">HttpContext.Items 작업</span><span class="sxs-lookup"><span data-stu-id="98865-240">Working with HttpContext.Items</span></span>

<span data-ttu-id="98865-241">`HttpContext` 추상화는 `Items`라는 형식 `IDictionary<object, object>`의 사전 컬렉션에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-241">The `HttpContext` abstraction provides support for a dictionary collection of type `IDictionary<object, object>`, called `Items`.</span></span> <span data-ttu-id="98865-242">이 컬렉션은 *HttpRequest*의 시작부터 사용할 수 있으며 각 요청의 끝에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="98865-242">This collection is available from the start of an *HttpRequest* and is discarded at the end of each request.</span></span> <span data-ttu-id="98865-243">키가 지정된 항목에 값을 지정하거나 특정 키에 대한 값을 요청하여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-243">You can access it by  assigning a value to a keyed entry, or by requesting the value for a particular key.</span></span>

<span data-ttu-id="98865-244">다음 샘플에서 [미들웨어](xref:fundamentals/middleware/index)는 `Items` 컬렉션에 `isVerified`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-244">In the following sample, [Middleware](xref:fundamentals/middleware/index) adds `isVerified` to the `Items` collection.</span></span>

```csharp
app.Use(async (context, next) =>
{
    // perform some verification
    context.Items["isVerified"] = true;
    await next.Invoke();
});
```

<span data-ttu-id="98865-245">파이프라인의 뒷부분에서 다른 미들웨어는 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-245">Later in the pipeline, another middleware could access it:</span></span>

```csharp
app.Run(async (context) =>
{
    await context.Response.WriteAsync("Verified request? " + 
        context.Items["isVerified"]);
});
```

<span data-ttu-id="98865-246">단일 앱에서만 사용되는 미들웨어의 경우 `string` 키가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="98865-246">For middleware that will only be used by a single app, `string` keys are acceptable.</span></span> <span data-ttu-id="98865-247">그러나 응용 프로그램 간에 공유되는 미들웨어는 키가 충돌될 가능성을 방지하기 위해 고유한 개체 키를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-247">However, middleware that will be shared between applications should use unique object keys to avoid any chance of key collisions.</span></span> <span data-ttu-id="98865-248">여러 응용 프로그램에서 사용해야 하는 미들웨어를 개발하는 경우 아래와 같이 미들웨어 클래스에서 정의된 고유한 개체 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-248">If you are developing middleware that must work across multiple applications, use a unique object key defined in your middleware class as shown below:</span></span>

```csharp
public class SampleMiddleware
{
    public static readonly object SampleKey = new Object();

    public async Task Invoke(HttpContext httpContext)
    {
        httpContext.Items[SampleKey] = "some value";
        // additional code omitted
    }
}
```

<span data-ttu-id="98865-249">다른 코드는 미들웨어 클래스에 의해 노출된 키를 사용하여 `HttpContext.Items`에 저장된 값에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-249">Other code can access the value stored in `HttpContext.Items` using the key exposed by the middleware class:</span></span>

```csharp
public class HomeController : Controller
{
    public IActionResult Index()
    {
        string value = HttpContext.Items[SampleMiddleware.SampleKey];
    }
}
```

<span data-ttu-id="98865-250">이 방법은 또한 코드의 여러 위치에서 "매직 문자열"의 반복을 제거하는 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-250">This approach also has the advantage of eliminating repetition of "magic strings" in multiple places in the code.</span></span>

<a name="appstate-errors"></a>

## <a name="application-state-data"></a><span data-ttu-id="98865-251">응용 프로그램 상태 데이터</span><span class="sxs-lookup"><span data-stu-id="98865-251">Application state data</span></span>

<span data-ttu-id="98865-252">[종속성 주입](xref:fundamentals/dependency-injection)을 사용하여 모든 사용자에게 데이터를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-252">Use [Dependency Injection](xref:fundamentals/dependency-injection) to make data available to all users:</span></span>

1. <span data-ttu-id="98865-253">데이터를 포함하는 서비스를 정의합니다(예: `MyAppData`라는 클래스).</span><span class="sxs-lookup"><span data-stu-id="98865-253">Define a service containing the data (for example, a class named `MyAppData`).</span></span>

```csharp
public class MyAppData
{
    // Declare properties/methods/etc.
} 
```
2. <span data-ttu-id="98865-254">`ConfigureServices`에 서비스 클래스를 추가합니다(예: `services.AddSingleton<MyAppData>();`).</span><span class="sxs-lookup"><span data-stu-id="98865-254">Add the service class to `ConfigureServices` (for example `services.AddSingleton<MyAppData>();`).</span></span>
3. <span data-ttu-id="98865-255">각 컨트롤러에서 데이터 서비스 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-255">Consume the data service class in each controller:</span></span>

```csharp
public class MyController : Controller
{
    public MyController(MyAppData myService)
    {
        // Do something with the service (read some data from it, 
        // store it in a private field/property, etc.)
    }
} 
```

## <a name="common-errors-when-working-with-session"></a><span data-ttu-id="98865-256">세션을 작업할 때 일반적인 오류</span><span class="sxs-lookup"><span data-stu-id="98865-256">Common errors when working with session</span></span>

* <span data-ttu-id="98865-257">"'Microsoft.AspNetCore.Session.DistributedSessionStore'를 활성화하려고 시도하는 동안 'Microsoft.Extensions.Caching.Distributed.IDistributedCache' 형식에 대한 서비스를 확인할 수 없습니다."</span><span class="sxs-lookup"><span data-stu-id="98865-257">"Unable to resolve service for type 'Microsoft.Extensions.Caching.Distributed.IDistributedCache' while attempting to activate 'Microsoft.AspNetCore.Session.DistributedSessionStore'."</span></span>

  <span data-ttu-id="98865-258">이는 일반적으로는 하나 이상의 `IDistributedCache` 구현을 구성하는 데 실패하여 발생됩니다.</span><span class="sxs-lookup"><span data-stu-id="98865-258">This is usually caused by failing to configure at least one `IDistributedCache` implementation.</span></span> <span data-ttu-id="98865-259">자세한 내용은 [분산 캐시 사용](xref:performance/caching/distributed) 및 [인 메모리 캐싱](xref:performance/caching/memory)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98865-259">For more information, see [Working with a Distributed Cache](xref:performance/caching/distributed) and [In memory caching](xref:performance/caching/memory).</span></span>

* <span data-ttu-id="98865-260">세션 미들웨어가 세션 유지에 실패하는 이벤트에서(예: 데이터베이스를 사용할 수 없는 경우) 예외를 기록하고 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="98865-260">In the event that the session middleware fails to persist a session (for example: if the database isn't available), it logs the exception and swallows it.</span></span> <span data-ttu-id="98865-261">그런 다음, 요청은 정상적으로 계속합니다. 이로 인해 매우 예기치 않은 동작이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-261">The request will then continue normally, which leads to very unpredictable behavior.</span></span>

<span data-ttu-id="98865-262">일반적인 예:</span><span class="sxs-lookup"><span data-stu-id="98865-262">A typical example:</span></span>

<span data-ttu-id="98865-263">일부 사용자는 세션에 장바구니를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-263">Someone stores a shopping basket in session.</span></span> <span data-ttu-id="98865-264">사용자는 항목을 추가하지만 커밋이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-264">The user adds an item but the commit fails.</span></span> <span data-ttu-id="98865-265">앱은 실패에 대해 알지 못하므로 true가 아닌 "항목이 추가되었습니다." 메시지를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-265">The app doesn't know about the failure so it reports the message "The item has been added", which isn't true.</span></span>

<span data-ttu-id="98865-266">이러한 오류를 확인하는 권장 방법은 세션에 작성을 완료하면 앱 코드에서 `await feature.Session.CommitAsync();`를 호출하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="98865-266">The recommended way to check for such errors is to call `await feature.Session.CommitAsync();` from app code when you're done writing to the session.</span></span> <span data-ttu-id="98865-267">그런 다음, 오류에 대해 원하는 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98865-267">Then you can do what you like with the error.</span></span> <span data-ttu-id="98865-268">`LoadAsync`를 호출할 때 동일한 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="98865-268">It works the same way when calling `LoadAsync`.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="98865-269">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="98865-269">Additional resources</span></span>

* [<span data-ttu-id="98865-270">ASP.NET Core 1.x: 이 문서에 사용되는 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="98865-270">ASP.NET Core 1.x: Sample code used in this document</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/app-state/sample/src/WebAppSession)
* [<span data-ttu-id="98865-271">ASP.NET Core 2.x: 이 문서에 사용되는 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="98865-271">ASP.NET Core 2.x: Sample code used in this document</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/app-state/sample/src/WebAppSessionDotNetCore2.0App)
