---
title: "ASP.NET Core에서 세션 및 응용 프로그램 상태"
author: rick-anderson
description: "요청 간에 유지 응용 프로그램 및 사용자 (세션) 상태에 접근 합니다."
ms.author: riande
manager: wpickett
ms.date: 11/27/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/app-state
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e00960370fbe87ac0f81f8455526221fa992decd
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="introduction-to-session-and-application-state-in-aspnet-core"></a><span data-ttu-id="867fb-103">ASP.NET Core에서 세션 및 응용 프로그램 상태 소개</span><span class="sxs-lookup"><span data-stu-id="867fb-103">Introduction to session and application state in ASP.NET Core</span></span>

<span data-ttu-id="867fb-104">여 [Rick Anderson](https://twitter.com/RickAndMSFT), [Steve Smith](https://ardalis.com/), 및 [Diana LaRose](https://github.com/DianaLaRose)</span><span class="sxs-lookup"><span data-stu-id="867fb-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Steve Smith](https://ardalis.com/), and [Diana LaRose](https://github.com/DianaLaRose)</span></span>

<span data-ttu-id="867fb-105">HTTP는 상태 비저장 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-105">HTTP is a stateless protocol.</span></span> <span data-ttu-id="867fb-106">웹 서버 독립적인 요청으로 각 HTTP 요청을 처리 하 고 이전 요청에서 사용자 값을 유지 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-106">A web server treats each HTTP request as an independent request and doesn't retain user values from previous requests.</span></span> <span data-ttu-id="867fb-107">이 문서에서는 응용 프로그램 및 요청 간에 세션 상태를 유지 하기 위해 다양 한 방법 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-107">This article discusses different ways to preserve application and session state between requests.</span></span> 

## <a name="session-state"></a><span data-ttu-id="867fb-108">세션 상태</span><span class="sxs-lookup"><span data-stu-id="867fb-108">Session state</span></span>

<span data-ttu-id="867fb-109">세션 상태는 사용자가 웹앱을 탐색하는 동안 사용자 데이터를 저장하는 데 사용할 수 있는 ASP.NET Core의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-109">Session state is a feature in ASP.NET Core that you can use to save and store user data while the user browses your web app.</span></span> <span data-ttu-id="867fb-110">세션 상태 서버에 사전 또는 해시 테이블, 구성 된 브라우저에서 요청을 통해 데이터를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-110">Consisting of a dictionary or hash table on the server, session state persists data across requests from a browser.</span></span> <span data-ttu-id="867fb-111">세션 데이터는 캐시에 의해 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-111">The session data is backed by a cache.</span></span>

<span data-ttu-id="867fb-112">ASP.NET Core 클라이언트 각 요청과 함께 서버에 전송 된 세션 ID를 포함 하는 쿠키를 제공 하 여 세션 상태를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-112">ASP.NET Core maintains session state by giving the client a cookie that contains the session ID, which is sent to the server with each request.</span></span> <span data-ttu-id="867fb-113">서버 세션 ID를 사용 하 여 세션 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-113">The server uses the session ID to fetch the session data.</span></span> <span data-ttu-id="867fb-114">세션 쿠키의 브라우저 관련 이기 때문에 브라우저 세션을 공유할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-114">Because the session cookie is specific to the browser, you cannot share sessions across browsers.</span></span> <span data-ttu-id="867fb-115">세션 쿠키는 브라우저 세션이 끝나면 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-115">Session cookies are deleted only when the browser session ends.</span></span> <span data-ttu-id="867fb-116">쿠키가 만료 된 세션에 대 한 수신 되 면 같은 세션 쿠키를 사용 하는 새 세션 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-116">If a cookie is received for an expired session, a new session that uses the same session cookie  is created.</span></span> 

<span data-ttu-id="867fb-117">서버는 마지막 요청 이후 제한 된 시간에 대 한 세션을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-117">The server retains a session for a limited time after the last request.</span></span> <span data-ttu-id="867fb-118">세션 제한 시간을 설정 하거나 기본값인 20 분을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-118">You can either set the session timeout or use the default value of 20 minutes.</span></span> <span data-ttu-id="867fb-119">세션 상태는 영구적으로 유지 될 필요가 없습니다 있지만 특정 세션에 고유한 사용자 데이터를 저장 하는 데 이상적입니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-119">Session state is ideal for storing user data that's specific to a particular session but doesn’t need to be persisted permanently.</span></span> <span data-ttu-id="867fb-120">데이터에서에서 삭제 됩니다 백업 저장소 중 하나를 호출할 때 `Session.Clear` 세션 데이터 저장소에서 만료 될 때 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-120">Data is deleted from the backing store either when you call `Session.Clear` or when the session expires in the data store.</span></span> <span data-ttu-id="867fb-121">서버는 브라우저를 닫을 때 세션 쿠키를 삭제 하는 경우 또는 알지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-121">The server doesn't know when the browser is closed or when the session cookie is deleted.</span></span>

> [!WARNING]
> <span data-ttu-id="867fb-122">세션에 중요 한 데이터를 저장 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="867fb-122">Don't store sensitive data in session.</span></span> <span data-ttu-id="867fb-123">클라이언트 수 하지 브라우저를 닫고 세션 쿠키의 선택을 취소 (및 일부 브라우저 세션 쿠키 활성 상태를 유지할 전체 windows).</span><span class="sxs-lookup"><span data-stu-id="867fb-123">The client might not close the browser and clear the session cookie (and some browsers keep session cookies alive across windows).</span></span> <span data-ttu-id="867fb-124">또한 세션; 단일 사용자로 제한 될 수 있습니다. 다음 사용자는 동일한 세션 계속 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-124">Also, a session might not be restricted to a single user; the next user might continue with the same session.</span></span>

<span data-ttu-id="867fb-125">메모리 내 세션 공급자는 로컬 서버에 세션 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-125">The in-memory session provider stores session data on the local server.</span></span> <span data-ttu-id="867fb-126">서버 팜에서 웹 앱을 실행 하려는 경우 특정 서버에 각 세션에 연결할 고정 세션을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-126">If you plan to run your web app on a server farm, you must use sticky sessions to tie each session to a specific server.</span></span> <span data-ttu-id="867fb-127">Windows Azure 웹 사이트 플랫폼 고정 세션 (응용 프로그램 요청 라우팅 또는 ARR) 기본값으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-127">The Windows Azure Web Sites platform defaults to sticky sessions (Application Request Routing or ARR).</span></span> <span data-ttu-id="867fb-128">그러나는 고정 세션 확장성에 영향을 줄 수 있으며 웹 응용 프로그램 업데이트 복잡 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-128">However, sticky sessions can affect scalability and complicate web app updates.</span></span> <span data-ttu-id="867fb-129">Redis를 사용 하는 편이 더 나은지 되었거나 SQL Server 분산 캐시는 고정 세션이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-129">A better option is to use the Redis or SQL Server distributed caches, which don't require sticky sessions.</span></span> <span data-ttu-id="867fb-130">자세한 내용은 참조 [분산 캐시 작업](xref:performance/caching/distributed)합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-130">For more information, see [Working with a Distributed Cache](xref:performance/caching/distributed).</span></span> <span data-ttu-id="867fb-131">서비스 공급자를 설정에 대 한 자세한 내용은 참조 하십시오. [세션 구성](#configuring-session) 이 문서의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-131">For details on setting up service providers, see [Configuring Session](#configuring-session) later in this article.</span></span>

<a name="temp"></a>
## <a name="tempdata"></a><span data-ttu-id="867fb-132">TempData</span><span class="sxs-lookup"><span data-stu-id="867fb-132">TempData</span></span>

<span data-ttu-id="867fb-133">ASP.NET Core MVC 노출 된 [TempData](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Controller_TempData) 속성에는 [컨트롤러](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.controller?view=aspnetcore-2.0)합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-133">ASP.NET Core MVC exposes the [TempData](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.controller.tempdata?view=aspnetcore-2.0#Microsoft_AspNetCore_Mvc_Controller_TempData) property on a [controller](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.controller?view=aspnetcore-2.0).</span></span> <span data-ttu-id="867fb-134">이 속성은 읽을 때까지 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-134">This property stores data until it's read.</span></span> <span data-ttu-id="867fb-135">`Keep` 및 `Peek` 메서드를 사용하여 삭제 없이 데이터를 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-135">The `Keep` and `Peek` methods can be used to examine the data without deletion.</span></span> <span data-ttu-id="867fb-136">`TempData`단일 요청 보다 많이 필요한 데이터의 경우 리디렉션, 데 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-136">`TempData` is particularly useful for redirection, when data is needed for more than a single request.</span></span> <span data-ttu-id="867fb-137">`TempData`이 공급자에 의해 구현 TempData 예를 들어 세션 상태 또는 쿠키를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-137">`TempData` is implemented by TempData providers, for example, using either cookies or session state.</span></span>

<a name="tempdata-providers"></a>
### <a name="tempdata-providers"></a><span data-ttu-id="867fb-138">TempData 공급자</span><span class="sxs-lookup"><span data-stu-id="867fb-138">TempData providers</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="867fb-139">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="867fb-139">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="867fb-140">ASP.NET Core 2.0 이상에서는 TempData 쿠키에 저장 하려면 기본적으로는 쿠키 기반 TempData 공급자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-140">In ASP.NET Core 2.0 and later, the cookie-based TempData provider is used by default to store TempData in cookies.</span></span>

<span data-ttu-id="867fb-141">쿠키 데이터가 인코딩된는 [Base64UrlTextEncoder](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.webutilities.base64urltextencoder?view=aspnetcore-2.0)합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-141">The cookie data is encoded with the [Base64UrlTextEncoder](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.webutilities.base64urltextencoder?view=aspnetcore-2.0).</span></span> <span data-ttu-id="867fb-142">단일 쿠키 크기가 쿠키 암호화 되 고 청크를 있으므로 제한에 ASP.NET Core 1.x 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-142">Because the cookie is encrypted and chunked, the single cookie size limit found in ASP.NET Core 1.x does not apply.</span></span> <span data-ttu-id="867fb-143">쿠키 데이터가 같은 보안 문제를 일으킬 수 암호화 된 데이터를 압축 하기 때문에 압축 되지 않은 [범죄](https://wikipedia.org/wiki/CRIME_(security_exploit)) 및 [위반](https://wikipedia.org/wiki/BREACH_(security_exploit)) 공격입니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-143">The cookie data is not compressed because compressing encrypted data can lead to security problems such as the [CRIME](https://wikipedia.org/wiki/CRIME_(security_exploit)) and [BREACH](https://wikipedia.org/wiki/BREACH_(security_exploit)) attacks.</span></span> <span data-ttu-id="867fb-144">쿠키 기반 TempData 공급자에 대 한 자세한 내용은 참조 하십시오. [CookieTempDataProvider](https://github.com/aspnet/Mvc/blob/dev/src/Microsoft.AspNetCore.Mvc.ViewFeatures/ViewFeatures/CookieTempDataProvider.cs)합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-144">For more information on the cookie-based TempData provider, see [CookieTempDataProvider](https://github.com/aspnet/Mvc/blob/dev/src/Microsoft.AspNetCore.Mvc.ViewFeatures/ViewFeatures/CookieTempDataProvider.cs).</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="867fb-145">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="867fb-145">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="867fb-146">ASP.NET Core 1.0 및 1.1에서는 세션 상태 TempData 공급자가 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-146">In ASP.NET Core 1.0 and 1.1, the session state TempData provider is the default.</span></span>

--------------

<a name="choose-temp"></a>
### <a name="choosing-a-tempdata-provider"></a><span data-ttu-id="867fb-147">TempData 공급자 선택</span><span class="sxs-lookup"><span data-stu-id="867fb-147">Choosing a TempData provider</span></span>

<span data-ttu-id="867fb-148">TempData 공급자를 선택 하려면와 같은 몇 가지 고려 사항:</span><span class="sxs-lookup"><span data-stu-id="867fb-148">Choosing a TempData provider involves several considerations, such as:</span></span>

1. <span data-ttu-id="867fb-149">응용 프로그램이 이미 다른 용도에 세션 상태를 사용 합니까?</span><span class="sxs-lookup"><span data-stu-id="867fb-149">Does the application already use session state for other purposes?</span></span> <span data-ttu-id="867fb-150">이 경우 응용 프로그램 데이터의 크기) (외에 추가 비용 없이 세션 상태 TempData 공급자를 사용 하 여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-150">If so, using the session state TempData provider has no additional cost to the application (aside from the size of the data).</span></span>
2. <span data-ttu-id="867fb-151">응용 프로그램 사용 TempData만 제한적으로 상대적으로 적은 양의 데이터 (최대 500 바이트)에 대 한 합니까?</span><span class="sxs-lookup"><span data-stu-id="867fb-151">Does the application use TempData only sparingly, for relatively small amounts of data (up to 500 bytes)?</span></span> <span data-ttu-id="867fb-152">따라서 쿠키 TempData 공급자 TempData를 전달 하는 각 요청에 작은 비용 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-152">If so, the cookie TempData provider will add a small cost to each request that carries TempData.</span></span> <span data-ttu-id="867fb-153">그렇지 않은 경우 세션 상태 TempData 공급자 TempData 사용 될 때까지 왕복 많은 양의 각 요청에 데이터를 방지 하는 데 특히 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-153">If not, the session state TempData provider can be beneficial to avoid round-tripping a large amount of data in each request until the TempData is consumed.</span></span>
3. <span data-ttu-id="867fb-154">응용 프로그램 웹 팜 (다중 서버)에서 실행 됩니까?</span><span class="sxs-lookup"><span data-stu-id="867fb-154">Does the application run in a web farm (multiple servers)?</span></span> <span data-ttu-id="867fb-155">이 경우 쿠키 TempData 공급자를 사용 하는 데 필요한 추가 구성 없이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-155">If so, there's no additional configuration needed to use the cookie TempData provider.</span></span>

> [!NOTE]
> <span data-ttu-id="867fb-156">대부분의 웹 클라이언트 (예: 웹 브라우저)에 각 쿠키, 쿠키의 총 수 또는 둘 다의 최대 크기에 대 한 제한을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-156">Most web clients (such as web browsers) enforce limits on the maximum size of each cookie, the total number of cookies, or both.</span></span> <span data-ttu-id="867fb-157">따라서 쿠키 TempData 공급자를 사용 하는 경우 응용 프로그램에는 이러한 제한을 초과 하지 않습니다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-157">Therefore, when using the cookie TempData provider, verify the app won't exceed these limits.</span></span> <span data-ttu-id="867fb-158">암호화의 오버 헤드에 대 한 계정 및 청크는 데이터의 전체 크기를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-158">Consider the total size of the data, accounting for the overheads of encryption and chunking.</span></span>

<a name="config-temp"></a>
### <a name="configure-the-tempdata-provider"></a><span data-ttu-id="867fb-159">TempData 공급자 구성</span><span class="sxs-lookup"><span data-stu-id="867fb-159">Configure the TempData provider</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="867fb-160">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="867fb-160">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="867fb-161">쿠키 기반 TempData 공급자는 기본적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-161">The cookie-based TempData provider is enabled by default.</span></span> <span data-ttu-id="867fb-162">다음 `Startup` 클래스 코드 TempData 세션 기반 공급자를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-162">The following `Startup` class code configures the session-based TempData provider:</span></span>

[!code-csharp[](app-state/sample/src/WebAppSessionDotNetCore2.0App/StartupTempDataSession.cs?name=snippet_TempDataSession&highlight=4,6,11)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="867fb-163">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="867fb-163">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="867fb-164">다음 `Startup` 클래스 코드 TempData 세션 기반 공급자를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-164">The following `Startup` class code configures the session-based TempData provider:</span></span>

[!code-csharp[](app-state/sample/src/WebAppSession/StartupTempDataSession.cs?name=snippet_TempDataSession&highlight=4,9)]

---

<span data-ttu-id="867fb-165">순서 지정 하는 것은 미들웨어 구성 요소에 대 한 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-165">Ordering is critical for middleware components.</span></span> <span data-ttu-id="867fb-166">위의 예에서 형식의 예외가 `InvalidOperationException` 발생 때 `UseSession` 후 호출 `UseMvcWithDefaultRoute`합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-166">In the preceding example, an exception of type `InvalidOperationException` occurs when `UseSession` is invoked after `UseMvcWithDefaultRoute`.</span></span> <span data-ttu-id="867fb-167">참조 [미들웨어 순서](xref:fundamentals/middleware#ordering) 자세한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-167">See [Middleware Ordering](xref:fundamentals/middleware#ordering) for more detail.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="867fb-168">.NET Framework 대상 지정 및 세션 기반 공급자를 사용 하 여 추가 하는 경우는 [Microsoft.AspNetCore.Session](https://www.nuget.org/packages/Microsoft.AspNetCore.Session) NuGet 패키지를 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-168">If targeting .NET Framework and using the session-based provider, add the [Microsoft.AspNetCore.Session](https://www.nuget.org/packages/Microsoft.AspNetCore.Session) NuGet package to your project.</span></span>

## <a name="query-strings"></a><span data-ttu-id="867fb-169">쿼리 문자열</span><span class="sxs-lookup"><span data-stu-id="867fb-169">Query strings</span></span>

<span data-ttu-id="867fb-170">새 요청 쿼리 문자열에 추가 하 여 다른 한 요청에서 제한 된 양의 데이터를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-170">You can pass a limited amount of data from one request to another by adding it to the new request’s query string.</span></span> <span data-ttu-id="867fb-171">이에 포함 된 상태를 전자 메일 또는 소셜 네트워크를 통해 공유할 수 있는 링크를 허용 하는 영구적인 방식으로 상태를 캡처하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-171">This is useful for capturing state in a persistent manner that allows links with embedded state to be shared through email or social networks.</span></span> <span data-ttu-id="867fb-172">그러나 이러한 이유로 해야 사용 하지 쿼리 문자열을 중요 한 데이터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-172">However, for this reason, you should never use query strings for sensitive data.</span></span> <span data-ttu-id="867fb-173">뿐 아니라 쉽게 공유 되 고 쿼리 문자열에 데이터를 포함 하 여 만들 수에 대 한 기회 [교차 사이트 요청 위조 (CSRF)](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)) 공격으로, 사용자가 인증 하는 동안 악성 사이트를 방문 하도록 유도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-173">In addition to being easily shared, including data in query strings can create opportunities for [Cross-Site Request Forgery (CSRF)](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)) attacks, which can trick users into visiting malicious sites while authenticated.</span></span> <span data-ttu-id="867fb-174">공격자가 다음 앱에서 사용자 데이터를 도용 하거나 사용자를 대신 하 여 악의적인 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-174">Attackers can then steal user data from your app or take malicious actions on behalf of the user.</span></span> <span data-ttu-id="867fb-175">유지 된 모든 응용 프로그램이 나 세션 상태는 CSRF 공격 으로부터 보호 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-175">Any preserved application or session state must protect against CSRF attacks.</span></span> <span data-ttu-id="867fb-176">CSRF 공격에 대 한 자세한 내용은 참조 하십시오. [방지 교차 사이트 요청 위조 (XSRF/CSRF) 공격에 ASP.NET Core](../security/anti-request-forgery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-176">For more information on CSRF attacks, see [Preventing Cross-Site Request Forgery (XSRF/CSRF) Attacks in ASP.NET Core](../security/anti-request-forgery.md).</span></span>

## <a name="post-data-and-hidden-fields"></a><span data-ttu-id="867fb-177">게시 데이터 및 숨김된 필드</span><span class="sxs-lookup"><span data-stu-id="867fb-177">Post data and hidden fields</span></span>

<span data-ttu-id="867fb-178">데이터 숨겨진된 양식 필드에 저장 되며 다음 요청에 다시 게시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-178">Data can be saved in hidden form fields and posted back on the next request.</span></span> <span data-ttu-id="867fb-179">다중 페이지 폼에서 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-179">This is common in multi-page forms.</span></span> <span data-ttu-id="867fb-180">그러나 클라이언트 잠재적으로 데이터를 변조할 수 있습니다, 때문에 서버 해야 항상 유효성 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-180">However, because the client can potentially tamper with the data, the server must always revalidate it.</span></span> 

## <a name="cookies"></a><span data-ttu-id="867fb-181">쿠키</span><span class="sxs-lookup"><span data-stu-id="867fb-181">Cookies</span></span>

<span data-ttu-id="867fb-182">쿠키는 웹 응용 프로그램에서 사용자 관련 데이터를 저장 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-182">Cookies provide a way to store user-specific data in web applications.</span></span> <span data-ttu-id="867fb-183">쿠키는 모든 요청과 함께 전송 되므로, 해당 크기를 최소로 유지 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-183">Because cookies are sent with every request, their size should be kept to a minimum.</span></span> <span data-ttu-id="867fb-184">이상적으로 서버에 저장 된 실제 데이터와 식별자만 쿠키에 저장 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-184">Ideally, only an identifier should be stored in a cookie with the actual data stored on the server.</span></span> <span data-ttu-id="867fb-185">대부분의 브라우저는 4096 바이트에 쿠키를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-185">Most browsers restrict cookies to 4096 bytes.</span></span> <span data-ttu-id="867fb-186">또한 제한 된 개수의 쿠키는 각 도메인에 대해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-186">In addition, only a limited number of cookies are available for each domain.</span></span>  

<span data-ttu-id="867fb-187">쿠키는 변조 될 이기 때문에 서버에서 이러한 유효성을 검사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-187">Because cookies are subject to tampering, they must be validated on the server.</span></span> <span data-ttu-id="867fb-188">클라이언트에 쿠키의 지 속성 사용자 작업 및 만료 될 수 있는 경우에 클라이언트에서 데이터 지 속성 형식의 가장 영 속는 일반적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-188">Although the durability of the cookie on a client is subject to user intervention and expiration, they're generally the most durable form of data persistence on the client.</span></span>

<span data-ttu-id="867fb-189">쿠키는 자주 사용 개인 설정에 대 한 콘텐츠 알려진된 사용자에 대 한 사용자 지정한 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-189">Cookies are often used for personalization, where content is customized for a known user.</span></span> <span data-ttu-id="867fb-190">사용자만 파악 하 고 대부분의 경우에서 인증 되지 않은, 때문에 사용자 이름, 계정 이름 또는 고유한 사용자 ID (예: GUID)를 쿠키에 저장 하 여 쿠키를 일반적으로 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-190">Because the user is only identified and not authenticated in most cases, you can typically secure a cookie by storing the user name, account name, or a unique user ID (such as a GUID) in the cookie.</span></span> <span data-ttu-id="867fb-191">그런 다음 사이트의 사용자 개인 설정 인프라에 액세스할 쿠키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-191">You can then use the cookie to access the user personalization infrastructure of a site.</span></span>

## <a name="httpcontextitems"></a><span data-ttu-id="867fb-192">HttpContext.Items</span><span class="sxs-lookup"><span data-stu-id="867fb-192">HttpContext.Items</span></span>

<span data-ttu-id="867fb-193">`Items` 컬렉션은 필요한 데이터를 저장 하는 좋은 위치 하나의 특정 요청을 처리 하는 동안에 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-193">The `Items` collection is a good location to store data that's needed only while processing one particular request.</span></span> <span data-ttu-id="867fb-194">컬렉션의 각 요청 후 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-194">The collection's contents are discarded after each request.</span></span> <span data-ttu-id="867fb-195">`Items` 컬렉션은 가장 요청 하는 중에 다른 시점에서 작동 하 고 매개 변수를 전달할 방법이 없습니다 직접 때 통신 하도록 구성 요소 또는 미들웨어에 대 한 방법으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-195">The `Items` collection is best used as a way for components or middleware to communicate when they operate at different points in time during a request and have no direct way to pass parameters.</span></span> <span data-ttu-id="867fb-196">자세한 내용은 참조 [HttpContext.Items 작업](#working-with-httpcontextitems)이 문서의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-196">For more information, see [Working with HttpContext.Items](#working-with-httpcontextitems), later in this article.</span></span>

## <a name="cache"></a><span data-ttu-id="867fb-197">캐시</span><span class="sxs-lookup"><span data-stu-id="867fb-197">Cache</span></span>

<span data-ttu-id="867fb-198">캐싱은 데이터 저장 및 검색 하는 효율적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-198">Caching is an efficient way to store and retrieve data.</span></span> <span data-ttu-id="867fb-199">시간 및 기타 고려 사항에 따라 캐시 된 항목의 수명을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-199">You can control the lifetime of cached items based on time and other considerations.</span></span> <span data-ttu-id="867fb-200">에 대 한 자세한 내용은 [캐싱](../performance/caching/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-200">Learn more about [Caching](../performance/caching/index.md).</span></span>

<a name="session"></a>
## <a name="working-with-session-state"></a><span data-ttu-id="867fb-201">세션 상태 사용</span><span class="sxs-lookup"><span data-stu-id="867fb-201">Working with Session State</span></span>

### <a name="configuring-session"></a><span data-ttu-id="867fb-202">세션 구성</span><span class="sxs-lookup"><span data-stu-id="867fb-202">Configuring Session</span></span>

<span data-ttu-id="867fb-203">`Microsoft.AspNetCore.Session` 패키지 세션 상태를 관리 하기 위한 미들웨어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-203">The `Microsoft.AspNetCore.Session` package provides middleware for managing session state.</span></span> <span data-ttu-id="867fb-204">세션 미들웨어를 사용 하도록 설정 하려면 `Startup` 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-204">To enable the session middleware, `Startup` must contain:</span></span>

- <span data-ttu-id="867fb-205">중 하나는 [IDistributedCache](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.distributed.idistributedcache) 메모리 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-205">Any of the [IDistributedCache](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.distributed.idistributedcache) memory caches.</span></span> <span data-ttu-id="867fb-206">`IDistributedCache` 구현이 세션에 대 한 백업 저장소로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-206">The `IDistributedCache` implementation is used as a backing store for session.</span></span>
- <span data-ttu-id="867fb-207">[AddSession](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.dependencyinjection.sessionservicecollectionextensions#Microsoft_Extensions_DependencyInjection_SessionServiceCollectionExtensions_AddSession_Microsoft_Extensions_DependencyInjection_IServiceCollection_) 필요 "Microsoft.AspNetCore.Session" NuGet 패키지를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-207">[AddSession](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.dependencyinjection.sessionservicecollectionextensions#Microsoft_Extensions_DependencyInjection_SessionServiceCollectionExtensions_AddSession_Microsoft_Extensions_DependencyInjection_IServiceCollection_) call, which requires NuGet package "Microsoft.AspNetCore.Session".</span></span>
- <span data-ttu-id="867fb-208">[UseSession](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.sessionmiddlewareextensions#methods_) 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-208">[UseSession](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.sessionmiddlewareextensions#methods_) call.</span></span>

<span data-ttu-id="867fb-209">다음 코드에서는 메모리 내 세션 공급자를 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-209">The following code shows how to set up the in-memory session provider.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="867fb-210">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="867fb-210">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](app-state/sample/src/WebAppSessionDotNetCore2.0App/Startup.cs?highlight=11-19,24)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="867fb-211">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="867fb-211">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](app-state/sample/src/WebAppSession/Startup.cs?highlight=11-19,24)]

---

<span data-ttu-id="867fb-212">세션을 참조할 수 있습니다 `HttpContext` 후이 설치 되어 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-212">You can reference Session from `HttpContext` once it's installed and configured.</span></span>

<span data-ttu-id="867fb-213">액세스 하려는 경우 `Session` 전에 `UseSession` 예외 호출 된 `InvalidOperationException: Session has not been configured for this application or request` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-213">If you try to access `Session` before `UseSession` has been called, the exception `InvalidOperationException: Session has not been configured for this application or request` is thrown.</span></span>

<span data-ttu-id="867fb-214">새 하려고 하면 `Session` (즉, 세션 쿠키가 없는 만든)에 쓰기를 이미 시작 된 후의 `Response` 스트림, 예외 `InvalidOperationException: The session cannot be established after the response has started` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-214">If you try to create a new `Session` (that is, no session cookie has been created) after you have already begun writing to the `Response` stream, the exception `InvalidOperationException: The session cannot be established after the response has started` is thrown.</span></span> <span data-ttu-id="867fb-215">웹 서버 로그에서 예외를 확인할 수 있습니다. 브라우저에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-215">The exception can be found in the web server log; it will not be displayed in the browser.</span></span>

### <a name="loading-session-asynchronously"></a><span data-ttu-id="867fb-216">세션을 비동기적으로 로드</span><span class="sxs-lookup"><span data-stu-id="867fb-216">Loading Session asynchronously</span></span> 

<span data-ttu-id="867fb-217">기본 세션 레코드를 로드 하는 기본 세션 공급자에서 ASP.NET Core [IDistributedCache](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.distributed.idistributedcache) 경우에만 비동기적으로 저장소는 [ISession.LoadAsync](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.http.isession#Microsoft_AspNetCore_Http_ISession_LoadAsync) 명시적으로 메서드는 하기 전에  `TryGetValue`, `Set`, 또는 `Remove` 메서드.</span><span class="sxs-lookup"><span data-stu-id="867fb-217">The default session provider in ASP.NET Core loads the session record from the underlying [IDistributedCache](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.caching.distributed.idistributedcache) store asynchronously only if the [ISession.LoadAsync](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.http.isession#Microsoft_AspNetCore_Http_ISession_LoadAsync) method is explicitly called before  the `TryGetValue`, `Set`, or `Remove` methods.</span></span> <span data-ttu-id="867fb-218">경우 `LoadAsync` 호출 되지 않은 먼저 내부는 영향을 줄 수 크기를 조정 하는 앱의 기능 세션 레코드를 동기적으로 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-218">If `LoadAsync` isn't called first, the underlying session record is loaded synchronously, which could potentially impact the ability of the app to scale.</span></span>

<span data-ttu-id="867fb-219">이 패턴을 적용 하는 응용 프로그램을 래핑하는 [DistributedSessionStore](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.session.distributedsessionstore) 및 [DistributedSession](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.session.distributedsession) 구현 하면 예외가 throw 된 버전으로는 `LoadAsync` 메서드가 실행 되지 않으면 이전에 호출 `TryGetValue`, `Set`, 또는 `Remove`합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-219">To have applications enforce this pattern, wrap the [DistributedSessionStore](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.session.distributedsessionstore) and [DistributedSession](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.session.distributedsession) implementations with versions that throw an exception if the `LoadAsync` method isn't called before `TryGetValue`, `Set`, or `Remove`.</span></span> <span data-ttu-id="867fb-220">서비스 컨테이너에 래핑된 버전을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-220">Register the wrapped versions in the services container.</span></span>

### <a name="implementation-details"></a><span data-ttu-id="867fb-221">구현 세부 정보</span><span class="sxs-lookup"><span data-stu-id="867fb-221">Implementation Details</span></span>

<span data-ttu-id="867fb-222">세션 쿠키를 사용 하 여 추적 하 고 단일 브라우저에서 요청을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-222">Session uses a cookie to track and identify requests from a single browser.</span></span> <span data-ttu-id="867fb-223">기본적으로이 쿠키 이름은 "입니다. 경로 사용 하 여 AspNet.Session"하며"/"입니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-223">By default, this cookie is named ".AspNet.Session", and it uses a path of "/".</span></span> <span data-ttu-id="867fb-224">쿠키 기본 도메인을 지정 하지 않는 때문에 이루어지지 않습니다 클라이언트 쪽 스크립트에서 사용할 페이지에서 (때문에 `CookieHttpOnly` 기본값으로 `true`).</span><span class="sxs-lookup"><span data-stu-id="867fb-224">Because the cookie default doesn't specify a domain, it's not made available to the client-side script on the page (because `CookieHttpOnly` defaults to `true`).</span></span>

<span data-ttu-id="867fb-225">사용 하 여 세션 기본값을 재정의 하려면 `SessionOptions`:</span><span class="sxs-lookup"><span data-stu-id="867fb-225">To override session defaults, use `SessionOptions`:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="867fb-226">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="867fb-226">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](app-state/sample/src/WebAppSessionDotNetCore2.0App/StartupCopy.cs?name=snippet1&highlight=8-12)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="867fb-227">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="867fb-227">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](app-state/sample/src/WebAppSession/StartupCopy.cs?name=snippet1&highlight=8-12)]

---

<span data-ttu-id="867fb-228">서버에서 사용 하는 `IdleTimeout` 기간 세션 유휴 상태일 수 있는 내용이 중단 하기 전에 확인 하는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-228">The server uses the `IdleTimeout` property to determine how long a session can be idle before its contents are abandoned.</span></span> <span data-ttu-id="867fb-229">이 속성은 쿠키 만료 기한 무관 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-229">This property is independent of the cookie expiration.</span></span> <span data-ttu-id="867fb-230">(에서 읽기 또는 쓰기) 세션 미들웨어를 통해 전달 되는 각 요청은 제한 시간이 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-230">Each request that passes through the Session middleware (read from or written to) resets the timeout.</span></span>

<span data-ttu-id="867fb-231">때문에 `Session` 은 *잠기지 않은*, 마지막 세션의 내용을 수정 하려고 하는 둘 다 두 요청 첫 번째 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-231">Because `Session` is *non-locking*, if two requests both attempt to modify the contents of session, the last one overrides the first.</span></span> <span data-ttu-id="867fb-232">`Session`로 구현 됩니다는 *일관 된 세션*, 즉, 모든 내용을 함께 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-232">`Session` is implemented as a *coherent session*, which means that all the contents are stored together.</span></span> <span data-ttu-id="867fb-233">세션 (서로 다른 키)의 다른 부분을 수정 하는 두 요청 서로 저하 계속 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-233">Two requests that are modifying different parts of the session (different keys) might still impact each other.</span></span>

### <a name="setting-and-getting-session-values"></a><span data-ttu-id="867fb-234">설정 및 세션 값 가져오기</span><span class="sxs-lookup"><span data-stu-id="867fb-234">Setting and getting Session values</span></span>

<span data-ttu-id="867fb-235">세션을 통해 액세스는 `Session` 속성 `HttpContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-235">Session is accessed through the `Session` property on `HttpContext`.</span></span> <span data-ttu-id="867fb-236">이 속성은 한 [ISession](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.http.isession) 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-236">This property is an [ISession](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.http.isession) implementation.</span></span>

<span data-ttu-id="867fb-237">다음 예제에서는 설정 및 가져오기는 int와 문자열을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-237">The following example shows setting and getting an int and a string:</span></span>

[!code-csharp[Main](app-state/sample/src/WebAppSession/Controllers/HomeController.cs?range=8-27,49)]

<span data-ttu-id="867fb-238">다음 확장 메서드를 추가 하는 경우 설정할 수 있으며 세션에 직렬화 가능 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-238">If you add the following extension methods, you can set and get serializable objects to Session:</span></span>

[!code-csharp[Main](app-state/sample/src/WebAppSession/Extensions/SessionExtensions.cs)]

<span data-ttu-id="867fb-239">다음 샘플에는 설정 하 고 직렬화 가능 개체를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-239">The following sample shows how to set and get a serializable object:</span></span>

[!code-csharp[Main](app-state/sample/src/WebAppSession/Controllers/HomeController.cs?name=snippet2)]


## <a name="working-with-httpcontextitems"></a><span data-ttu-id="867fb-240">HttpContext.Items 작업</span><span class="sxs-lookup"><span data-stu-id="867fb-240">Working with HttpContext.Items</span></span>

<span data-ttu-id="867fb-241">`HttpContext` 추상화 형식의 사전 컬렉션에 대 한 지원을 제공 `IDictionary<object, object>`라는 `Items`합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-241">The `HttpContext` abstraction provides support for a dictionary collection of type `IDictionary<object, object>`, called `Items`.</span></span> <span data-ttu-id="867fb-242">이 컬렉션은의 시작 부분부터 사용할 수는 *HttpRequest* 은 각 요청의 끝에 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-242">This collection is available from the start of an *HttpRequest* and is discarded at the end of each request.</span></span> <span data-ttu-id="867fb-243">키가 지정 된 항목에 값을 지정 하거나 특정 키에 대 한 값을 요청 하 여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-243">You can access it by  assigning a value to a keyed entry, or by requesting the value for a particular key.</span></span>

<span data-ttu-id="867fb-244">아래 샘플에서 [미들웨어](middleware.md) 추가 `isVerified` 에 `Items` 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-244">In the sample below, [Middleware](middleware.md) adds `isVerified` to the `Items` collection.</span></span>

```csharp
app.Use(async (context, next) =>
{
    // perform some verification
    context.Items["isVerified"] = true;
    await next.Invoke();
});
```

<span data-ttu-id="867fb-245">파이프라인의 뒷부분에 나오는 다른 미들웨어를 액세스 하기:</span><span class="sxs-lookup"><span data-stu-id="867fb-245">Later in the pipeline, another middleware could access it:</span></span>

```csharp
app.Run(async (context) =>
{
    await context.Response.WriteAsync("Verified request? " + 
        context.Items["isVerified"]);
});
```

<span data-ttu-id="867fb-246">단일 앱에서 사용할만 미들웨어에 대 한 `string` 키 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-246">For middleware that will only be used by a single app, `string` keys are acceptable.</span></span> <span data-ttu-id="867fb-247">그러나 응용 프로그램 간에 공유 되는 미들웨어 키가 충돌 될 가능성을 방지 하기 위해 고유한 개체 키를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-247">However, middleware that will be shared between applications should use unique object keys to avoid any chance of key collisions.</span></span> <span data-ttu-id="867fb-248">여러 응용 프로그램에서 사용 해야 하는 미들웨어를 개발 하는 경우 아래와 같이 미들웨어 클래스에 정의 된 개체를 고유 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-248">If you are developing middleware that must work across multiple applications, use a unique object key defined in your middleware class as shown below:</span></span>

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

<span data-ttu-id="867fb-249">다른 코드에 저장 된 값에 액세스할 수 `HttpContext.Items` 미들웨어 클래스에 의해 노출 되는 키를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="867fb-249">Other code can access the value stored in `HttpContext.Items` using the key exposed by the middleware class:</span></span>

```csharp
public class HomeController : Controller
{
    public IActionResult Index()
    {
        string value = HttpContext.Items[SampleMiddleware.SampleKey];
    }
}
```

<span data-ttu-id="867fb-250">이 방법은 또한 반복 되는 코드에서 여러 위치에서 "매직 문자열"를 제거 하 여 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-250">This approach also has the advantage of eliminating repetition of "magic strings" in multiple places in the code.</span></span>

<a name="appstate-errors"></a>

## <a name="application-state-data"></a><span data-ttu-id="867fb-251">응용 프로그램 상태 데이터</span><span class="sxs-lookup"><span data-stu-id="867fb-251">Application state data</span></span>

<span data-ttu-id="867fb-252">사용 하 여 [종속성 주입](xref:fundamentals/dependency-injection) 모든 사용자에 게 데이터를 사용할 수 있도록 하려면:</span><span class="sxs-lookup"><span data-stu-id="867fb-252">Use [Dependency Injection](xref:fundamentals/dependency-injection) to make data available to all users:</span></span>

1. <span data-ttu-id="867fb-253">데이터를 포함 하는 서비스 정의 (예를 들어 라는 클래스 `MyAppData`).</span><span class="sxs-lookup"><span data-stu-id="867fb-253">Define a service containing the data (for example, a class named `MyAppData`).</span></span>

```csharp
public class MyAppData
{
    // Declare properties/methods/etc.
} 
```
2. <span data-ttu-id="867fb-254">에 대 한 서비스 클래스를 추가 `ConfigureServices` (예를 들어 `services.AddSingleton<MyAppData>();`).</span><span class="sxs-lookup"><span data-stu-id="867fb-254">Add the service class to `ConfigureServices` (for example `services.AddSingleton<MyAppData>();`).</span></span>
3. <span data-ttu-id="867fb-255">각 컨트롤러에서 데이터 서비스 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-255">Consume the data service class in each controller:</span></span>

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

## <a name="common-errors-when-working-with-session"></a><span data-ttu-id="867fb-256">세션을 작업할 때 일반적인 오류</span><span class="sxs-lookup"><span data-stu-id="867fb-256">Common errors when working with session</span></span>

* <span data-ttu-id="867fb-257">"'Microsoft.AspNetCore.Session.DistributedSessionStore' 활성화 하는 동안 'Microsoft.Extensions.Caching.Distributed.IDistributedCache' 형식에 대 한 서비스를 확인할 수 없습니다."</span><span class="sxs-lookup"><span data-stu-id="867fb-257">"Unable to resolve service for type 'Microsoft.Extensions.Caching.Distributed.IDistributedCache' while attempting to activate 'Microsoft.AspNetCore.Session.DistributedSessionStore'."</span></span>

  <span data-ttu-id="867fb-258">일반적으로는 하나 이상의 구성에 실패 `IDistributedCache` 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-258">This is usually caused by failing to configure at least one `IDistributedCache` implementation.</span></span> <span data-ttu-id="867fb-259">자세한 내용은 참조 [분산 캐시 작업](xref:performance/caching/distributed) 및 [메모리 캐싱에](xref:performance/caching/memory)합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-259">For more information, see [Working with a Distributed Cache](xref:performance/caching/distributed) and [In memory caching](xref:performance/caching/memory).</span></span>

* <span data-ttu-id="867fb-260">유지 하는 미들웨어가 세션 세션 이벤트 (예: 데이터베이스를 사용할 수 없는 경우), 예외를 기록 하 고이 swallow 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-260">In the event that the session middleware fails to persist a session (for example: if the database isn't available), it logs the exception and swallows it.</span></span> <span data-ttu-id="867fb-261">요청 매우 예기치 않은 동작이에 일반적으로 계속 다음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-261">The request will then continue normally, which leads to very unpredictable behavior.</span></span>

<span data-ttu-id="867fb-262">일반적인 예:</span><span class="sxs-lookup"><span data-stu-id="867fb-262">A typical example:</span></span>

<span data-ttu-id="867fb-263">사용자 세션에 장바구니를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-263">Someone stores a shopping basket in session.</span></span> <span data-ttu-id="867fb-264">사용자 항목을 추가 하지만 커밋이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-264">The user adds an item but the commit fails.</span></span> <span data-ttu-id="867fb-265">응용 프로그램 있는지 알 수 없으므로 실패에 대 한 "는 항목이 추가 되었습니다.", true 아닌 메시지를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-265">The app doesn't know about the failure so it reports the message "The item has been added", which isn't true.</span></span>

<span data-ttu-id="867fb-266">이러한 오류를 확인 하는 권장된 방법은 호출 하는 것 `await feature.Session.CommitAsync();` 완료 되 면 응용 프로그램 코드에서 세션에 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-266">The recommended way to check for such errors is to call `await feature.Session.CommitAsync();` from app code when you're done writing to the session.</span></span> <span data-ttu-id="867fb-267">그런 다음 어떤 점이 좋은지 오류가 발생 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-267">Then you can do what you like with the error.</span></span> <span data-ttu-id="867fb-268">호출할 때 동일한 방식으로 작동 `LoadAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="867fb-268">It works the same way when calling `LoadAsync`.</span></span>


### <a name="additional-resources"></a><span data-ttu-id="867fb-269">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="867fb-269">Additional Resources</span></span>


* [<span data-ttu-id="867fb-270">ASP.NET Core 1.x:이 문서에 사용 되는 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="867fb-270">ASP.NET Core 1.x: Sample code used in this document</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/app-state/sample/src/WebAppSession)
* [<span data-ttu-id="867fb-271">ASP.NET Core 2.x:이 문서에 사용 되는 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="867fb-271">ASP.NET Core 2.x: Sample code used in this document</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/app-state/sample/src/WebAppSessionDotNetCore2.0App)
