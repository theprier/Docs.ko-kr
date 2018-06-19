---
uid: web-api/overview/advanced/http-cookies
title: ASP.NET Web API의에서 HTTP 쿠키 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/17/2012
ms.topic: article
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: 363ca975cf75b635b766a53eeda87cf957eed60c
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
ms.locfileid: "30071631"
---
<a name="http-cookies-in-aspnet-web-api"></a><span data-ttu-id="6dc6e-102">ASP.NET Web API의에서 HTTP 쿠키</span><span class="sxs-lookup"><span data-stu-id="6dc6e-102">HTTP Cookies in ASP.NET Web API</span></span>
====================
<span data-ttu-id="6dc6e-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6dc6e-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="6dc6e-104">이 항목에는 Web API에서 HTTP 쿠키를 송수신 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-104">This topic describes how to send and receive HTTP cookies in Web API.</span></span>

## <a name="background-on-http-cookies"></a><span data-ttu-id="6dc6e-105">HTTP 쿠키에 대 한 배경</span><span class="sxs-lookup"><span data-stu-id="6dc6e-105">Background on HTTP Cookies</span></span>

<span data-ttu-id="6dc6e-106">이 섹션에서는 쿠키를 HTTP 수준에서 구현 하는 방법에 대해 간략하게 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-106">This section gives a brief overview of how cookies are implemented at the HTTP level.</span></span> <span data-ttu-id="6dc6e-107">자세한 내용은 참조 하십시오. [RFC 6265](http://tools.ietf.org/html/rfc6265)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-107">For details, consult [RFC 6265](http://tools.ietf.org/html/rfc6265).</span></span>

<span data-ttu-id="6dc6e-108">쿠키는 HTTP 응답에는 서버에서 전송 하는 데이터의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-108">A cookie is a piece of data that a server sends in the HTTP response.</span></span> <span data-ttu-id="6dc6e-109">(선택 사항) 클라이언트는 쿠키를 저장 하 고 subsequet 요청에서 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-109">The client (optionally) stores the cookie and returns it on subsequet requests.</span></span> <span data-ttu-id="6dc6e-110">이렇게 하면 클라이언트 및 서버 상태를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-110">This allows the client and server to share state.</span></span> <span data-ttu-id="6dc6e-111">쿠키를 설정 하려면 서버는 응답에서 Set-cookie 헤더를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-111">To set a cookie, the server includes a Set-Cookie header in the response.</span></span> <span data-ttu-id="6dc6e-112">쿠키의 형식은 선택적 특성이 있는 이름-값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-112">The format of a cookie is a name-value pair, with optional attributes.</span></span> <span data-ttu-id="6dc6e-113">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="6dc6e-113">For example:</span></span>

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

<span data-ttu-id="6dc6e-114">특성의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-114">Here is an example with attributes:</span></span>

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

<span data-ttu-id="6dc6e-115">서버에 쿠키를 반환 하려면 클라이언트가 이후 요청에 쿠키 헤더를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-115">To return a cookie to the server, the client includes a Cookie header in later requests.</span></span>

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

<span data-ttu-id="6dc6e-116">HTTP 응답에는 여러 Set-cookie 헤더를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-116">An HTTP response can include multiple Set-Cookie headers.</span></span>

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

<span data-ttu-id="6dc6e-117">클라이언트는 단일 쿠키 헤더를 사용 하 여 여러 쿠키를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-117">The client returns multiple cookies using a single Cookie header.</span></span>

[!code-console[Main](http-cookies/samples/sample5.cmd)]

<span data-ttu-id="6dc6e-118">범위 및 쿠키의 기간 Set-cookie 헤더에 다음 특성으로 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-118">The scope and duration of a cookie are controlled by following attributes in the Set-Cookie header:</span></span>

- <span data-ttu-id="6dc6e-119">**도메인**: 쿠키 받아야 하는 도메인을 클라이언트에 게 알립니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-119">**Domain**: Tells the client which domain should receive the cookie.</span></span> <span data-ttu-id="6dc6e-120">예를 들어 도메인이 "example.com" 경우 클라이언트 example.com의 모든 하위 도메인에 쿠키를 반환 합니다. 지정 하지 않으면 도메인에 원본 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-120">For example, if the domain is "example.com", the client returns the cookie to every subdomain of example.com. If not specified, the domain is the origin server.</span></span>
- <span data-ttu-id="6dc6e-121">**경로**: 도메인 내에서 지정된 된 경로에 쿠키를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-121">**Path**: Restricts the cookie to the specified path within the domain.</span></span> <span data-ttu-id="6dc6e-122">지정 하지 않으면 요청 URI의 경로가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-122">If not specified, the path of the request URI is used.</span></span>
- <span data-ttu-id="6dc6e-123">**만료**: 쿠키의 만료 날짜를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-123">**Expires**: Sets an expiration date for the cookie.</span></span> <span data-ttu-id="6dc6e-124">기간이 만료 되는 클라이언트 쿠키를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-124">The client deletes the cookie when it expires.</span></span>
- <span data-ttu-id="6dc6e-125">**Max-age**: 쿠키에 대 한 최대 기간을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-125">**Max-Age**: Sets the maximum age for the cookie.</span></span> <span data-ttu-id="6dc6e-126">최대 보존 기간에 도달할 때 클라이언트에서 쿠키를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-126">The client deletes the cookie when it reaches the maximum age.</span></span>

<span data-ttu-id="6dc6e-127">두 `Expires` 및 `Max-Age` 설정 `Max-Age` 우선적으로 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-127">If both `Expires` and `Max-Age` are set, `Max-Age` takes precedence.</span></span> <span data-ttu-id="6dc6e-128">둘 다 설정 하는 경우 현재 세션이 종료 될 때 클라이언트 쿠키를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-128">If neither is set, the client deletes the cookie when the current session ends.</span></span> <span data-ttu-id="6dc6e-129">("세션"의 정확한 의미는 사용자 에이전트에 의해 결정 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="6dc6e-129">(The exact meaning of "session" is determined by the user-agent.)</span></span>

<span data-ttu-id="6dc6e-130">그러나 수 클라이언트가 쿠키를 무시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-130">However, be aware that clients may ignore cookies.</span></span> <span data-ttu-id="6dc6e-131">예를 들어, 사용자 개인 정보 보호에 대 한 쿠키를 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-131">For example, a user might disable cookies for privacy reasons.</span></span> <span data-ttu-id="6dc6e-132">저장 된 쿠키가 수를 제한 하거나, 만료 하기 전에 클라이언트에서 쿠키를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-132">Clients may delete cookies before they expire, or limit the number of cookies stored.</span></span> <span data-ttu-id="6dc6e-133">개인 정보 보호를 위해 클라이언트는 종종 "제 3 자" 쿠키, 도메인이 원본 서버 일치 하지 않는 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-133">For privacy reasons, clients often reject "third party" cookies, where the domain does not match the origin server.</span></span> <span data-ttu-id="6dc6e-134">즉, 서버 다시 설정 하는 쿠키를 가져오는 방법에 되지는지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-134">In short, the server should not rely on getting back the cookies that it sets.</span></span>

## <a name="cookies-in-web-api"></a><span data-ttu-id="6dc6e-135">Web API의 쿠키</span><span class="sxs-lookup"><span data-stu-id="6dc6e-135">Cookies in Web API</span></span>

<span data-ttu-id="6dc6e-136">HTTP 응답에 쿠키를 추가 하려면 만듭니다는 **CookieHeaderValue** 쿠키를 나타내는 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-136">To add a cookie to an HTTP response, create a **CookieHeaderValue** instance that represents the cookie.</span></span> <span data-ttu-id="6dc6e-137">그런 다음 호출에서 **AddCookies** 에 정의 된 확장 메서드는 **System.Net.Http 합니다. HttpResponseHeadersExtensions** 쿠키를 추가할 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-137">Then call the **AddCookies** extension method, which is defined in the **System.Net.Http. HttpResponseHeadersExtensions** class, to add the cookie.</span></span>

<span data-ttu-id="6dc6e-138">예를 들어 다음 코드는 컨트롤러 작업 내에서 쿠키를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-138">For example, the following code adds a cookie within a controller action:</span></span>

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

<span data-ttu-id="6dc6e-139">다음에 유의 **AddCookies** 의 어레이 **CookieHeaderValue** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-139">Notice that **AddCookies** takes an array of **CookieHeaderValue** instances.</span></span>

<span data-ttu-id="6dc6e-140">호출 클라이언트 요청에서 쿠키를 추출 하는 **GetCookies** 메서드:</span><span class="sxs-lookup"><span data-stu-id="6dc6e-140">To extract the cookies from a client request, call the **GetCookies** method:</span></span>

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

<span data-ttu-id="6dc6e-141">A **CookieHeaderValue** 의 컬렉션을 포함 **CookieState** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-141">A **CookieHeaderValue** contains a collection of **CookieState** instances.</span></span> <span data-ttu-id="6dc6e-142">각 **CookieState** 쿠키를 두 개를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-142">Each **CookieState** represents one cookie.</span></span> <span data-ttu-id="6dc6e-143">인덱서 메서드를 사용 하 여 가져오기는 **CookieState** 이름순으로 표시 된 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-143">Use the indexer method to get a **CookieState** by name, as shown.</span></span>

## <a name="structured-cookie-data"></a><span data-ttu-id="6dc6e-144">구조적된 쿠키 데이터</span><span class="sxs-lookup"><span data-stu-id="6dc6e-144">Structured Cookie Data</span></span>

<span data-ttu-id="6dc6e-145">저장 하는 쿠키의 수를 제한 하는 다양 한 브라우저&#8212;총 수와 각 도메인 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-145">Many browsers limit how many cookies they will store&#8212;both the total number, and the number per domain.</span></span> <span data-ttu-id="6dc6e-146">따라서 여러 쿠키를 설정 하는 대신 단일 쿠키로 구조적된 데이터를 저장 하 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-146">Therefore, it can be useful to put structured data into a single cookie, instead of setting multiple cookies.</span></span>

> [!NOTE]
> <span data-ttu-id="6dc6e-147">RFC 6265 쿠키 데이터의 구조를 정의 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-147">RFC 6265 does not define the structure of cookie data.</span></span>


<span data-ttu-id="6dc6e-148">사용 하는 **CookieHeaderValue** 클래스 쿠키 데이터에 대 한 이름-값 쌍의 목록을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-148">Using the **CookieHeaderValue** class, you can pass a list of name-value pairs for the cookie data.</span></span> <span data-ttu-id="6dc6e-149">이러한 이름-값 쌍의 경우는 Set-cookie 헤더의 URL로 인코딩된 양식 데이터로 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-149">These name-value pairs are encoded as URL-encoded form data in the Set-Cookie header:</span></span>

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

<span data-ttu-id="6dc6e-150">앞의 코드는 다음과 같은 Set-cookie 헤더를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-150">The previous code produces the following Set-Cookie header:</span></span>

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

<span data-ttu-id="6dc6e-151">**CookieState** 클래스 요청 메시지에서 쿠키의 하위 값을 읽을 인덱서 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-151">The **CookieState** class provides an indexer method to read the sub-values from a cookie in the request message:</span></span>

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a><span data-ttu-id="6dc6e-152">예: 설정 하 고 메시지 처리기에서 쿠키를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-152">Example: Set and Retrieve Cookies in a Message Handler</span></span>

<span data-ttu-id="6dc6e-153">이전 예제에는 Web API 컨트롤러 내에서 쿠키를 사용 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-153">The previous examples showed how to use cookies from within a Web API controller.</span></span> <span data-ttu-id="6dc6e-154">또 다른 옵션은 사용 하도록 [메시지 처리기](http-message-handlers.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-154">Another option is to use [message handlers](http-message-handlers.md).</span></span> <span data-ttu-id="6dc6e-155">컨트롤러 보다 파이프라인의 앞부분에 나오는 메시지 처리기가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-155">Message handlers are invoked earlier in the pipeline than controllers.</span></span> <span data-ttu-id="6dc6e-156">메시지 처리기는 컨트롤러에 도착 하기 전에 요청에서 쿠키를 읽는 하거나 컨트롤러 응답을 생성 한 다음 응답에 쿠키를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-156">A message handler can read cookies from the request before the request reaches the controller, or add cookies to the response after the controller generates the response.</span></span>

![](http-cookies/_static/image2.png)

<span data-ttu-id="6dc6e-157">다음 코드에서는 세션 Id를 만들기 위한 메시지 처리기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-157">The following code shows a message handler for creating session IDs.</span></span> <span data-ttu-id="6dc6e-158">세션 ID는 쿠키에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-158">The session ID is stored in a cookie.</span></span> <span data-ttu-id="6dc6e-159">처리기는 세션 쿠키에 대 한 요청을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-159">The handler checks the request for the session cookie.</span></span> <span data-ttu-id="6dc6e-160">처리기 생성 새 세션 id입니다. 요청에 쿠키가 포함 되어 있지 않으면,</span><span class="sxs-lookup"><span data-stu-id="6dc6e-160">If the request does not include the cookie, the handler generates a new session ID.</span></span> <span data-ttu-id="6dc6e-161">두 경우 모두 처리기에 세션 ID를 저장 된 **HttpRequestMessage.Properties** 속성 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-161">In either case, the handler stores the session ID in the **HttpRequestMessage.Properties** property bag.</span></span> <span data-ttu-id="6dc6e-162">또한 세션 쿠키를 HTTP 응답에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-162">It also adds the session cookie to the HTTP response.</span></span>

<span data-ttu-id="6dc6e-163">이 구현에서는 클라이언트에서 세션 ID는 서버에서 실제로 발급 되었으며 하는 것을 확인 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-163">This implementation does not validate that the session ID from the client was actually issued by the server.</span></span> <span data-ttu-id="6dc6e-164">인증의 형식으로 사용 하지 마십시오!</span><span class="sxs-lookup"><span data-stu-id="6dc6e-164">Don't use it as a form of authentication!</span></span> <span data-ttu-id="6dc6e-165">이 예제에서는 지점의 HTTP 쿠키를 관리 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-165">The point of the example is to show HTTP cookie management.</span></span>

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

<span data-ttu-id="6dc6e-166">컨트롤러의 세션 ID를 가져올 수는 **HttpRequestMessage.Properties** 속성 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="6dc6e-166">A controller can get the session ID from the **HttpRequestMessage.Properties** property bag.</span></span>

[!code-csharp[Main](http-cookies/samples/sample12.cs)]
