---
uid: web-api/overview/advanced/http-message-handlers
title: ASP.NET Web API의에서 HTTP 메시지 처리기 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/13/2012
ms.topic: article
ms.assetid: 9002018b-3aa3-4358-bb1c-fbb5bc751d01
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/advanced/http-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: 931ad3330d5e4dc2424ab37b8a6e2a3d123a8684
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
ms.locfileid: "26506952"
---
<a name="http-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="70b05-102">ASP.NET Web API의에서 HTTP 메시지 처리기</span><span class="sxs-lookup"><span data-stu-id="70b05-102">HTTP Message Handlers in ASP.NET Web API</span></span>
====================
<span data-ttu-id="70b05-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="70b05-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="70b05-104">A *메시지 처리기* 는 HTTP 요청을 수신 하 고 HTTP 응답을 반환 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-104">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span> <span data-ttu-id="70b05-105">Abstract에서 파생 되는 메시지 처리기 **HttpMessageHandler** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-105">Message handlers derive from the abstract **HttpMessageHandler** class.</span></span>

<span data-ttu-id="70b05-106">일반적으로 일련의 메시지 처리기 함께 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-106">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="70b05-107">첫 번째 처리기 HTTP 요청을 수신 하 고, 일부 처리를, 다음 처리기에 요청을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-107">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="70b05-108">어느 시점 부터는 응답 생성 되 고 체인 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-108">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="70b05-109">이 패턴 라고는 *위임* 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-109">This pattern is called a *delegating* handler.</span></span>

![](http-message-handlers/_static/image1.png)

## <a name="server-side-message-handlers"></a><span data-ttu-id="70b05-110">서버 쪽 메시지 처리기</span><span class="sxs-lookup"><span data-stu-id="70b05-110">Server-Side Message Handlers</span></span>

<span data-ttu-id="70b05-111">서버 쪽에서 Web API 파이프라인 몇 가지 기본 제공 메시지 처리기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-111">On the server side, the Web API pipeline uses some built-in message handlers:</span></span>

- <span data-ttu-id="70b05-112">**HttpServer** 호스트에서 요청을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-112">**HttpServer** gets the request from the host.</span></span>
- <span data-ttu-id="70b05-113">**HttpRoutingDispatcher** 경로에 따라 요청을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-113">**HttpRoutingDispatcher** dispatches the request based on the route.</span></span>
- <span data-ttu-id="70b05-114">**HttpControllerDispatcher** Web API 컨트롤러에 요청을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-114">**HttpControllerDispatcher** sends the request to a Web API controller.</span></span>

<span data-ttu-id="70b05-115">사용자 지정 처리기를 파이프라인에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-115">You can add custom handlers to the pipeline.</span></span> <span data-ttu-id="70b05-116">메시지 처리기는 HTTP 메시지 (아니라 컨트롤러 작업)의 수준에서 작동 하는 일반적인 문제에 대 한 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-116">Message handlers are good for cross-cutting concerns that operate at the level of HTTP messages (rather than controller actions).</span></span> <span data-ttu-id="70b05-117">예를 들어 메시지 처리기 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-117">For example, a message handler might:</span></span>

- <span data-ttu-id="70b05-118">읽기 또는 요청 헤더를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-118">Read or modify request headers.</span></span>
- <span data-ttu-id="70b05-119">응답 헤더를 응답에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-119">Add a response header to responses.</span></span>
- <span data-ttu-id="70b05-120">컨트롤러에 도달 하기 전에 요청의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-120">Validate requests before they reach the controller.</span></span>

<span data-ttu-id="70b05-121">이 다이어그램에서는 파이프라인에 삽입 하는 두 명의 사용자 지정 처리기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-121">This diagram shows two custom handlers inserted into the pipeline:</span></span>

![](http-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="70b05-122">클라이언트 쪽에서 HttpClient도 메시지 처리기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-122">On the client side, HttpClient also uses message handlers.</span></span> <span data-ttu-id="70b05-123">자세한 내용은 참조 [HttpClient 메시지 처리기](httpclient-message-handlers.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-123">For more information, see [HttpClient Message Handlers](httpclient-message-handlers.md).</span></span>


## <a name="custom-message-handlers"></a><span data-ttu-id="70b05-124">사용자 지정 메시지 처리기</span><span class="sxs-lookup"><span data-stu-id="70b05-124">Custom Message Handlers</span></span>

<span data-ttu-id="70b05-125">파생 한 사용자 지정 메시지 처리기를 작성 하려면 **System.Net.Http.DelegatingHandler** 재정의 **SendAsync** 메서드.</span><span class="sxs-lookup"><span data-stu-id="70b05-125">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="70b05-126">이 메서드의 서명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-126">This method has the following signature:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample1.cs)]

<span data-ttu-id="70b05-127">메서드를 사용 하며는 **HttpRequestMessage** 으로 입력 하 고 비동기적으로 반환 된 **HttpResponseMessage**합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-127">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="70b05-128">일반적인 구현은 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-128">A typical implementation does the following:</span></span>

1. <span data-ttu-id="70b05-129">요청 메시지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-129">Process the request message.</span></span>
2. <span data-ttu-id="70b05-130">호출 `base.SendAsync` 내부 처리기에 요청을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-130">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="70b05-131">내부 처리기는 응답 메시지를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-131">The inner handler returns a response message.</span></span> <span data-ttu-id="70b05-132">(이 단계는 비동기.)</span><span class="sxs-lookup"><span data-stu-id="70b05-132">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="70b05-133">응답을 처리 하 고 호출자에 게 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-133">Process the response and return it to the caller.</span></span>

<span data-ttu-id="70b05-134">간단한 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-134">Here is a trivial example:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="70b05-135">에 대 한 호출 `base.SendAsync` 비동기적입니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-135">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="70b05-136">처리기는이 호출 후에 모든 작업을 수행 하는 경우 사용 하 여는 **await** 키워드를 표시 된 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-136">If the handler does any work after this call, use the **await** keyword, as shown.</span></span>


<span data-ttu-id="70b05-137">위임 처리기 내부 처리기를 건너뛸 수도 및 응답을 직접 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-137">A delegating handler can also skip the inner handler and directly create the response:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample3.cs)]

<span data-ttu-id="70b05-138">처리기를 호출 하지 않고 응답 만듭니다는 위임 하는 경우 `base.SendAsync`, 요청 파이프라인의 나머지 부분을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-138">If a delegating handler creates the response without calling `base.SendAsync`, the request skips the rest of the pipeline.</span></span> <span data-ttu-id="70b05-139">이 (오류 응답이 생성) 요청의 유효성을 검사 하는 처리기에 대 한 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-139">This can be useful for a handler that validates the request (creating an error response).</span></span>

![](http-message-handlers/_static/image3.png)

## <a name="adding-a-handler-to-the-pipeline"></a><span data-ttu-id="70b05-140">파이프라인에 처리기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-140">Adding a Handler to the Pipeline</span></span>

<span data-ttu-id="70b05-141">서버 쪽에서 메시지 처리기를 추가 하려면 처리기에 추가 된 **HttpConfiguration.MessageHandlers** 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-141">To add a message handler on the server side, add the handler to the **HttpConfiguration.MessageHandlers** collection.</span></span> <span data-ttu-id="70b05-142">"ASP.NET MVC 4 웹 응용 프로그램" 템플릿을 사용 하는 프로젝트를 만드는 경우에이 내부를 수행할 수 있습니다는 **경우 WebApiConfig** 클래스:</span><span class="sxs-lookup"><span data-stu-id="70b05-142">If you used the "ASP.NET MVC 4 Web Application" template to create the project, you can do this inside the **WebApiConfig** class:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample4.cs)]

<span data-ttu-id="70b05-143">에 표시 되는 순서 대로 메시지 처리기가 호출 **MessageHandlers** 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-143">Message handlers are called in the same order that they appear in **MessageHandlers** collection.</span></span> <span data-ttu-id="70b05-144">중첩 되어 있으므로 응답 메시지는 반대 방향으로 이동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-144">Because they are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="70b05-145">마지막 처리기 즉, 가장 먼저 응답 메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-145">That is, the last handler is the first to get the response message.</span></span>

<span data-ttu-id="70b05-146">내부 처리기;를 설정 하려면 필요 하지 않습니다 Web API 프레임 워크의 메시지 처리기를 자동으로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-146">Notice that you don't need to set the inner handlers; the Web API framework automatically connects the message handlers.</span></span>

<span data-ttu-id="70b05-147">있다면 [자체 호스팅](../older-versions/self-host-a-web-api.md)의 인스턴스를 만들는 **HttpSelfHostConfiguration** 클래스 처리기를 추가 하 고는 **MessageHandlers** 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-147">If you are [self-hosting](../older-versions/self-host-a-web-api.md), create an instance of the **HttpSelfHostConfiguration** class and add the handlers to the **MessageHandlers** collection.</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample5.cs)]

<span data-ttu-id="70b05-148">이제 사용자 지정 메시지 처리기의 몇 가지 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-148">Now let's look at some examples of custom message handlers.</span></span>

## <a name="example-x-http-method-override"></a><span data-ttu-id="70b05-149">예: X-HTTP-메서드-재정</span><span class="sxs-lookup"><span data-stu-id="70b05-149">Example: X-HTTP-Method-Override</span></span>

<span data-ttu-id="70b05-150">HTTP 메서드 재정의 X는 비표준 HTTP 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-150">X-HTTP-Method-Override is a non-standard HTTP header.</span></span> <span data-ttu-id="70b05-151">PUT 또는 DELETE와 같은 특정 HTTP 요청 형식을 보낼 수 없는 클라이언트에 대 한 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-151">It is designed for clients that cannot send certain HTTP request types, such as PUT or DELETE.</span></span> <span data-ttu-id="70b05-152">대신, 클라이언트 POST 요청을 보내고 HTTP 메서드 재정의 X 헤더 원하는 메서드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-152">Instead, the client sends a POST request and sets the X-HTTP-Method-Override header to the desired method.</span></span> <span data-ttu-id="70b05-153">예:</span><span class="sxs-lookup"><span data-stu-id="70b05-153">For example:</span></span>

[!code-console[Main](http-message-handlers/samples/sample6.cmd)]

<span data-ttu-id="70b05-154">HTTP 메서드 재정의 X에 대 한 지원을 추가 하는 메시지 처리기는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-154">Here is a message handler that adds support for X-HTTP-Method-Override:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample7.cs)]

<span data-ttu-id="70b05-155">에 **SendAsync** 요청 메시지는 POST 요청 인지 및 HTTP 메서드 재정의 X 헤더 포함 여부 메서드를 처리기를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-155">In the **SendAsync** method, the handler checks whether the request message is a POST request, and whether it contains the X-HTTP-Method-Override header.</span></span> <span data-ttu-id="70b05-156">이 경우 헤더 값의 유효성을 검사 하며 요청 메서드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-156">If so, it validates the header value, and then modifies the request method.</span></span> <span data-ttu-id="70b05-157">처리기가 호출 하는 마지막으로, `base.SendAsync` 다음 처리기에는 메시지를 전달 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-157">Finally, the handler calls `base.SendAsync` to pass the message to the next handler.</span></span>

<span data-ttu-id="70b05-158">요청에 도달 하면는 **HttpControllerDispatcher** 클래스 **HttpControllerDispatcher** 업데이트 요청 방법에 따라 요청을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-158">When the request reaches the **HttpControllerDispatcher** class, **HttpControllerDispatcher** will route the request based on the updated request method.</span></span>

## <a name="example-adding-a-custom-response-header"></a><span data-ttu-id="70b05-159">예: 사용자 지정 응답 헤더 추가</span><span class="sxs-lookup"><span data-stu-id="70b05-159">Example: Adding a Custom Response Header</span></span>

<span data-ttu-id="70b05-160">모든 응답 메시지에 사용자 지정 헤더를 추가 하는 메시지 처리기는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-160">Here is a message handler that adds a custom header to every response message:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample8.cs)]

<span data-ttu-id="70b05-161">첫째, 처리기가 호출 `base.SendAsync` 내부 메시지 처리기 요청을 전달 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-161">First, the handler calls `base.SendAsync` to pass the request to the inner message handler.</span></span> <span data-ttu-id="70b05-162">내부 처리기는 응답 메시지를 반환 하지만 매우 비동기적으로 사용 하 여 수행 된 **작업&lt;T&gt;**  개체입니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-162">The inner handler returns a response message, but it does so asynchronously using a **Task&lt;T&gt;** object.</span></span> <span data-ttu-id="70b05-163">응답 메시지를 때까지 사용할 수 없으면 `base.SendAsync` 비동기적으로 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-163">The response message is not available until `base.SendAsync` completes asynchronously.</span></span>

<span data-ttu-id="70b05-164">사용 하 여이 예제는 **await** 작업을 수행 하는 키워드 비동기적으로 `SendAsync` 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-164">This example uses the **await** keyword to perform work asynchronously after `SendAsync` completes.</span></span> <span data-ttu-id="70b05-165">.NET Framework 4.0을 대상으로 하는 경우 사용 하 여는 **작업**&lt;T&gt;**합니다. ContinueWith** 메서드:</span><span class="sxs-lookup"><span data-stu-id="70b05-165">If you are targeting .NET Framework 4.0, use the **Task**&lt;T&gt;**.ContinueWith** method:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample9.cs)]

## <a name="example-checking-for-an-api-key"></a><span data-ttu-id="70b05-166">예: API 키에 대 한 검사</span><span class="sxs-lookup"><span data-stu-id="70b05-166">Example: Checking for an API Key</span></span>

<span data-ttu-id="70b05-167">일부 웹 서비스 요청에 API 키를 포함 하려면 클라이언트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-167">Some web services require clients to include an API key in their request.</span></span> <span data-ttu-id="70b05-168">다음 예제에서는 메시지 처리기 수 올바른 API 키에 대 한 요청을 확인 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-168">The following example shows how a message handler can check requests for a valid API key:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample10.cs)]

<span data-ttu-id="70b05-169">이 처리기는 URI 쿼리 문자열의 API 키를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-169">This handler looks for the API key in the URI query string.</span></span> <span data-ttu-id="70b05-170">(이 예에서는 라고 가정 키는 정적 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-170">(For this example, we assume that the key is a static string.</span></span> <span data-ttu-id="70b05-171">실제 구현 사용 보다 복잡 한 유효성 검사 합니다.) 쿼리 문자열 키를 포함 하는 경우 처리기 내부 처리기에 요청을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-171">A real implementation would probably use more complex validation.) If the query string contains the key, the handler passes the request to the inner handler.</span></span>

<span data-ttu-id="70b05-172">처리기의 상태 403, 응답 메시지를 만듭니다 요청에 유효한 키를 찾을 수 없는 경우 사용할 수 없음.</span><span class="sxs-lookup"><span data-stu-id="70b05-172">If the request does not have a valid key, the handler creates a response message with status 403, Forbidden.</span></span> <span data-ttu-id="70b05-173">이 경우 처리기가 호출 하지 않으면 `base.SendAsync`, 내부 처리기를 받지 요청 하므로 하지도 컨트롤러 않습니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-173">In this case, the handler does not call `base.SendAsync`, so the inner handler never receives the request, nor does the controller.</span></span> <span data-ttu-id="70b05-174">따라서 컨트롤러 들어오는 모든 요청에 올바른 API 키가 있는지 가정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-174">Therefore, the controller can assume that all incoming requests have a valid API key.</span></span>

> [!NOTE]
> <span data-ttu-id="70b05-175">API 키는 특정 컨트롤러 작업에만 적용 되는 경우에 작업 필터를 사용 하 여 메시지 처리기를 대신 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-175">If the API key applies only to certain controller actions, consider using an action filter instead of a message handler.</span></span> <span data-ttu-id="70b05-176">작업 필터 URI 라우팅을 수행 된 후 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-176">Action filters run after URI routing is performed.</span></span>


## <a name="per-route-message-handlers"></a><span data-ttu-id="70b05-177">경로 당 메시지 처리기</span><span class="sxs-lookup"><span data-stu-id="70b05-177">Per-Route Message Handlers</span></span>

<span data-ttu-id="70b05-178">처리기에는 **HttpConfiguration.MessageHandlers** 컬렉션 전체적으로 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-178">Handlers in the **HttpConfiguration.MessageHandlers** collection apply globally.</span></span>

<span data-ttu-id="70b05-179">또는 경로 정의 하는 경우 특정 경로에 메시지 처리기를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-179">Alternatively, you can add a message handler to a specific route when you define the route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample11.cs?highlight=16)]

<span data-ttu-id="70b05-180">이 예제에서는 요청 URI "Route2" 일치 하는 경우 요청에 디스패치 됩니다 `MessageHandler2`합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-180">In this example, if the request URI matches "Route2", the request is dispatched to `MessageHandler2`.</span></span> <span data-ttu-id="70b05-181">다음 다이어그램에서는이 두 경로 대 한 파이프라인을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-181">The following diagram shows the pipeline for these two routes:</span></span>

![](http-message-handlers/_static/image4.png)

<span data-ttu-id="70b05-182">다음에 유의 `MessageHandler2` 기본 바꿉니다 **HttpControllerDispatcher**합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-182">Notice that `MessageHandler2` replaces the default **HttpControllerDispatcher**.</span></span> <span data-ttu-id="70b05-183">이 예제에서는 `MessageHandler2` 응답을 만들고 컨트롤러를로 이동 하지 "Route2"와 일치 하는 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-183">In this example, `MessageHandler2` creates the response, and requests that match "Route2" never go to a controller.</span></span> <span data-ttu-id="70b05-184">이렇게 하면 사용자 고유의 사용자 지정 끝점 전체 Web API 컨트롤러 메커니즘을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-184">This lets you replace the entire Web API controller mechanism with your own custom endpoint.</span></span>

<span data-ttu-id="70b05-185">경로 당 메시지 처리기를 위임할 수 또는 **HttpControllerDispatcher**, 컨트롤러에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-185">Alternatively, a per-route message handler can delegate to **HttpControllerDispatcher**, which then dispatches to a controller.</span></span>

![](http-message-handlers/_static/image5.png)

<span data-ttu-id="70b05-186">다음 코드에는이 경로 구성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="70b05-186">The following code shows how to configure this route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample12.cs)]
