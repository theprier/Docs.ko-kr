---
uid: web-api/overview/advanced/http-cookies
title: ASP.NET Web API에서에서 HTTP 쿠키 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/17/2012
ms.topic: article
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: 5885586df1d0f67d4e7e04ad88bc4fd1af71dc80
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37368407"
---
<a name="http-cookies-in-aspnet-web-api"></a><span data-ttu-id="08daa-102">ASP.NET Web API에서에서 HTTP 쿠키</span><span class="sxs-lookup"><span data-stu-id="08daa-102">HTTP Cookies in ASP.NET Web API</span></span>
====================
<span data-ttu-id="08daa-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="08daa-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="08daa-104">이 항목에는 Web API에서 HTTP 쿠키를 송수신 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-104">This topic describes how to send and receive HTTP cookies in Web API.</span></span>

## <a name="background-on-http-cookies"></a><span data-ttu-id="08daa-105">HTTP 쿠키에 대 한 배경</span><span class="sxs-lookup"><span data-stu-id="08daa-105">Background on HTTP Cookies</span></span>

<span data-ttu-id="08daa-106">이 섹션에서는 쿠키 HTTP 수준에서 구현 하는 방법에 대해 간략하게 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-106">This section gives a brief overview of how cookies are implemented at the HTTP level.</span></span> <span data-ttu-id="08daa-107">자세한 내용은 참조 하세요 [RFC 6265](http://tools.ietf.org/html/rfc6265)합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-107">For details, consult [RFC 6265](http://tools.ietf.org/html/rfc6265).</span></span>

<span data-ttu-id="08daa-108">쿠키는 HTTP 응답에는 서버에 보내는 데이터의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-108">A cookie is a piece of data that a server sends in the HTTP response.</span></span> <span data-ttu-id="08daa-109">(선택 사항) 클라이언트는 쿠키를 저장 하 고 subsequet 요청에 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-109">The client (optionally) stores the cookie and returns it on subsequet requests.</span></span> <span data-ttu-id="08daa-110">이렇게 하면 클라이언트 및 서버 상태를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-110">This allows the client and server to share state.</span></span> <span data-ttu-id="08daa-111">쿠키를 설정 하려면 서버 응답에서 Set-cookie 헤더를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-111">To set a cookie, the server includes a Set-Cookie header in the response.</span></span> <span data-ttu-id="08daa-112">쿠키의 형식은 선택적 특성이 있는 이름-값 쌍을 합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-112">The format of a cookie is a name-value pair, with optional attributes.</span></span> <span data-ttu-id="08daa-113">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="08daa-113">For example:</span></span>

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

<span data-ttu-id="08daa-114">특성의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-114">Here is an example with attributes:</span></span>

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

<span data-ttu-id="08daa-115">쿠키를 서버에 반환할 클라이언트가 이후 요청에 쿠키 헤더를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-115">To return a cookie to the server, the client includes a Cookie header in later requests.</span></span>

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

<span data-ttu-id="08daa-116">HTTP 응답을 여러 Set-cookie 헤더를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-116">An HTTP response can include multiple Set-Cookie headers.</span></span>

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

<span data-ttu-id="08daa-117">클라이언트에서는 단일 쿠키 헤더를 사용 하 여 여러 쿠키를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-117">The client returns multiple cookies using a single Cookie header.</span></span>

[!code-console[Main](http-cookies/samples/sample5.cmd)]

<span data-ttu-id="08daa-118">범위 및 기간 쿠키를 Set-cookie 헤더에 다음 특성에 의해 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-118">The scope and duration of a cookie are controlled by following attributes in the Set-Cookie header:</span></span>

- <span data-ttu-id="08daa-119">**도메인**:는 도메인에 쿠키를 받아야 합니다. 클라이언트에 게 알립니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-119">**Domain**: Tells the client which domain should receive the cookie.</span></span> <span data-ttu-id="08daa-120">예를 들어 도메인이 "example.com" 인 경우 클라이언트 example.com의 모든 하위 도메인에 쿠키를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-120">For example, if the domain is "example.com", the client returns the cookie to every subdomain of example.com.</span></span> <span data-ttu-id="08daa-121">지정 하지 않으면 도메인에 원본 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-121">If not specified, the domain is the origin server.</span></span>
- <span data-ttu-id="08daa-122">**경로**: 도메인 내에서 지정된 된 경로에 쿠키를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-122">**Path**: Restricts the cookie to the specified path within the domain.</span></span> <span data-ttu-id="08daa-123">지정 하지 않으면 요청 URI의 경로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-123">If not specified, the path of the request URI is used.</span></span>
- <span data-ttu-id="08daa-124">**만료**: 쿠키의 만료 날짜를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-124">**Expires**: Sets an expiration date for the cookie.</span></span> <span data-ttu-id="08daa-125">클라이언트는 만료 되 면 쿠키를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-125">The client deletes the cookie when it expires.</span></span>
- <span data-ttu-id="08daa-126">**최대 처리 기간**: 쿠키의 최대 보관 기간을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-126">**Max-Age**: Sets the maximum age for the cookie.</span></span> <span data-ttu-id="08daa-127">최대 보존 기간에 도달 하면 클라이언트 쿠키를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-127">The client deletes the cookie when it reaches the maximum age.</span></span>

<span data-ttu-id="08daa-128">둘 다 `Expires` 하 고 `Max-Age` 설정 된 `Max-Age` 우선적으로 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-128">If both `Expires` and `Max-Age` are set, `Max-Age` takes precedence.</span></span> <span data-ttu-id="08daa-129">설정 하지 않으면 하는 경우 현재 세션이 종료 될 때 클라이언트 쿠키를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-129">If neither is set, the client deletes the cookie when the current session ends.</span></span> <span data-ttu-id="08daa-130">("세션"의 정확한 의미는 사용자-에이전트에 의해 결정 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="08daa-130">(The exact meaning of "session" is determined by the user-agent.)</span></span>

<span data-ttu-id="08daa-131">그러나 클라이언트가 쿠키를 무시 해도 주의 합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-131">However, be aware that clients may ignore cookies.</span></span> <span data-ttu-id="08daa-132">예를 들어, 사용자 개인 정보 보호에 대 한 쿠키를 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-132">For example, a user might disable cookies for privacy reasons.</span></span> <span data-ttu-id="08daa-133">저장 된 쿠키 수를 제한 하거나 만료 하기 전에 클라이언트에서 쿠키를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-133">Clients may delete cookies before they expire, or limit the number of cookies stored.</span></span> <span data-ttu-id="08daa-134">개인 정보 보호를 위해 클라이언트는 종종 "타사" 쿠키를 도메인 원본 서버에 맞지 않습니다 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-134">For privacy reasons, clients often reject "third party" cookies, where the domain does not match the origin server.</span></span> <span data-ttu-id="08daa-135">즉, 서버 설정 하는 쿠키를 다시 시작에 의존 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-135">In short, the server should not rely on getting back the cookies that it sets.</span></span>

## <a name="cookies-in-web-api"></a><span data-ttu-id="08daa-136">Web API에서 쿠키</span><span class="sxs-lookup"><span data-stu-id="08daa-136">Cookies in Web API</span></span>

<span data-ttu-id="08daa-137">HTTP 응답에 쿠키를 추가 하려면 만들기를 **CookieHeaderValue** 쿠키를 나타내는 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-137">To add a cookie to an HTTP response, create a **CookieHeaderValue** instance that represents the cookie.</span></span> <span data-ttu-id="08daa-138">다음 호출을 **AddCookies** 에 정의 된 확장 메서드를 **System.Net.Http 합니다. HttpResponseHeadersExtensions** 클래스에 쿠키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-138">Then call the **AddCookies** extension method, which is defined in the **System.Net.Http. HttpResponseHeadersExtensions** class, to add the cookie.</span></span>

<span data-ttu-id="08daa-139">예를 들어, 다음 코드는 컨트롤러 작업 내에서 쿠키를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-139">For example, the following code adds a cookie within a controller action:</span></span>

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

<span data-ttu-id="08daa-140">있음을 **AddCookies** 배열을 **CookieHeaderValue** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="08daa-140">Notice that **AddCookies** takes an array of **CookieHeaderValue** instances.</span></span>

<span data-ttu-id="08daa-141">호출에 클라이언트 요청에서 쿠키를 추출 합니다 **GetCookies** 메서드:</span><span class="sxs-lookup"><span data-stu-id="08daa-141">To extract the cookies from a client request, call the **GetCookies** method:</span></span>

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

<span data-ttu-id="08daa-142">A **CookieHeaderValue** 의 컬렉션을 포함 **CookieState** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="08daa-142">A **CookieHeaderValue** contains a collection of **CookieState** instances.</span></span> <span data-ttu-id="08daa-143">각 **CookieState** 하나 쿠키를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-143">Each **CookieState** represents one cookie.</span></span> <span data-ttu-id="08daa-144">인덱서 메서드를 사용 하 여 가져올는 **CookieState** 이름순으로 표시 된 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-144">Use the indexer method to get a **CookieState** by name, as shown.</span></span>

## <a name="structured-cookie-data"></a><span data-ttu-id="08daa-145">구조화 된 쿠키 데이터</span><span class="sxs-lookup"><span data-stu-id="08daa-145">Structured Cookie Data</span></span>

<span data-ttu-id="08daa-146">다양 한 브라우저 제한 횟수 쿠키를 저장 합니다&#8212;, 총 수와 각 도메인 수입니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-146">Many browsers limit how many cookies they will store&#8212;both the total number, and the number per domain.</span></span> <span data-ttu-id="08daa-147">따라서 여러 쿠키를 설정 하는 대신 단일 쿠키 구조화 된 데이터를 넣을 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-147">Therefore, it can be useful to put structured data into a single cookie, instead of setting multiple cookies.</span></span>

> [!NOTE]
> <span data-ttu-id="08daa-148">RFC 6265 쿠키 데이터 구조를 정의 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-148">RFC 6265 does not define the structure of cookie data.</span></span>


<span data-ttu-id="08daa-149">사용 하는 **CookieHeaderValue** 클래스 쿠키 데이터에 대 한 이름-값 쌍의 목록을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-149">Using the **CookieHeaderValue** class, you can pass a list of name-value pairs for the cookie data.</span></span> <span data-ttu-id="08daa-150">이러한 이름-값 쌍 Set-cookie 헤더의 URL로 인코딩된 양식 데이터로 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-150">These name-value pairs are encoded as URL-encoded form data in the Set-Cookie header:</span></span>

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

<span data-ttu-id="08daa-151">이전 코드는 다음과 같은 Set-cookie 헤더를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-151">The previous code produces the following Set-Cookie header:</span></span>

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

<span data-ttu-id="08daa-152">합니다 **CookieState** 클래스 값을 읽는 하위 요청 메시지의 쿠키에서 인덱서 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-152">The **CookieState** class provides an indexer method to read the sub-values from a cookie in the request message:</span></span>

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a><span data-ttu-id="08daa-153">예제: 설정 및 메시지 처리기에서 쿠키를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-153">Example: Set and Retrieve Cookies in a Message Handler</span></span>

<span data-ttu-id="08daa-154">이전 예제에는 Web API 컨트롤러 내에서 쿠키를 사용 하는 방법을 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-154">The previous examples showed how to use cookies from within a Web API controller.</span></span> <span data-ttu-id="08daa-155">사용 하는 다른 옵션도 [메시지 처리기](http-message-handlers.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-155">Another option is to use [message handlers](http-message-handlers.md).</span></span> <span data-ttu-id="08daa-156">이전 컨트롤러 보다 파이프라인에서에서 메시지 처리기가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-156">Message handlers are invoked earlier in the pipeline than controllers.</span></span> <span data-ttu-id="08daa-157">메시지 처리기 요청에는 컨트롤러에 도달 하기 전에 요청에서 쿠키를 읽을 하거나 컨트롤러 응답을 생성 한 후 응답에 쿠키를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-157">A message handler can read cookies from the request before the request reaches the controller, or add cookies to the response after the controller generates the response.</span></span>

![](http-cookies/_static/image2.png)

<span data-ttu-id="08daa-158">다음 코드는 세션 Id를 만들기에 대 한 메시지 처리기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-158">The following code shows a message handler for creating session IDs.</span></span> <span data-ttu-id="08daa-159">세션 ID는 쿠키에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-159">The session ID is stored in a cookie.</span></span> <span data-ttu-id="08daa-160">처리기는 세션 쿠키에 대 한 요청을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-160">The handler checks the request for the session cookie.</span></span> <span data-ttu-id="08daa-161">처리기는 새 세션 ID가 생성 요청 쿠키를 포함 하지 않는 경우</span><span class="sxs-lookup"><span data-stu-id="08daa-161">If the request does not include the cookie, the handler generates a new session ID.</span></span> <span data-ttu-id="08daa-162">두 경우 모두 처리기에 세션 ID를 저장 합니다 **HttpRequestMessage.Properties** 속성 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-162">In either case, the handler stores the session ID in the **HttpRequestMessage.Properties** property bag.</span></span> <span data-ttu-id="08daa-163">또한 세션 쿠키를 HTTP 응답에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-163">It also adds the session cookie to the HTTP response.</span></span>

<span data-ttu-id="08daa-164">이 구현은 클라이언트에서 세션 ID를 서버에서 실제로 발행 하는 것을 확인 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-164">This implementation does not validate that the session ID from the client was actually issued by the server.</span></span> <span data-ttu-id="08daa-165">인증 형식으로 사용 하지 않아도!</span><span class="sxs-lookup"><span data-stu-id="08daa-165">Don't use it as a form of authentication!</span></span> <span data-ttu-id="08daa-166">이 예제에서는 지점의 HTTP 쿠키 관리를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-166">The point of the example is to show HTTP cookie management.</span></span>

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

<span data-ttu-id="08daa-167">컨트롤러의 세션 ID를 가져올 수는 **HttpRequestMessage.Properties** 속성 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="08daa-167">A controller can get the session ID from the **HttpRequestMessage.Properties** property bag.</span></span>

[!code-csharp[Main](http-cookies/samples/sample12.cs)]
