---
uid: web-api/overview/advanced/httpclient-message-handlers
title: ASP.NET Web API의에서 HttpClient 메시지 처리기 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/01/2012
ms.topic: article
ms.assetid: 5a4b6c80-b2e9-4710-8969-d5076f7f82b8
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/advanced/httpclient-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: 805741b0ac682b7479ce82127df48b1b9a49a427
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
ms.locfileid: "26506792"
---
<a name="httpclient-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="0a267-102">ASP.NET Web API의에서 HttpClient 메시지 처리기</span><span class="sxs-lookup"><span data-stu-id="0a267-102">HttpClient Message Handlers in ASP.NET Web API</span></span>
====================
<span data-ttu-id="0a267-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0a267-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="0a267-104">A *메시지 처리기* 는 HTTP 요청을 수신 하 고 HTTP 응답을 반환 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-104">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span>

<span data-ttu-id="0a267-105">일반적으로 일련의 메시지 처리기 함께 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-105">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="0a267-106">첫 번째 처리기 HTTP 요청을 수신 하 고, 일부 처리를, 다음 처리기에 요청을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-106">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="0a267-107">어느 시점 부터는 응답 생성 되 고 체인 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-107">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="0a267-108">이 패턴 라고는 *위임* 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-108">This pattern is called a *delegating* handler.</span></span>

![](httpclient-message-handlers/_static/image1.png)

<span data-ttu-id="0a267-109">클라이언트 쪽에서의 **HttpClient** 클래스 메시지 처리기를 사용 하 여 요청을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-109">On the client side, the **HttpClient** class uses a message handler to process requests.</span></span> <span data-ttu-id="0a267-110">기본 처리기가 **HttpClientHandler**, 네트워크를 통해 요청을 전송 하 고 서버에서 응답을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-110">The default handler is **HttpClientHandler**, which sends the request over the network and gets the response from the server.</span></span> <span data-ttu-id="0a267-111">사용자 지정 메시지 처리기 클라이언트 파이프라인에 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-111">You can insert custom message handlers into the client pipeline:</span></span>

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="0a267-112">또한 ASP.NET Web API는 서버 쪽에서 메시지 처리기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-112">ASP.NET Web API also uses message handlers on the server side.</span></span> <span data-ttu-id="0a267-113">자세한 내용은 참조 [HTTP 메시지 처리기](http-message-handlers.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-113">For more information, see [HTTP Message Handlers](http-message-handlers.md).</span></span>


## <a name="custom-message-handlers"></a><span data-ttu-id="0a267-114">사용자 지정 메시지 처리기</span><span class="sxs-lookup"><span data-stu-id="0a267-114">Custom Message Handlers</span></span>

<span data-ttu-id="0a267-115">파생 한 사용자 지정 메시지 처리기를 작성 하려면 **System.Net.Http.DelegatingHandler** 재정의 **SendAsync** 메서드.</span><span class="sxs-lookup"><span data-stu-id="0a267-115">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="0a267-116">메서드 시그니처는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-116">Here is the method signature:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

<span data-ttu-id="0a267-117">메서드를 사용 하며는 **HttpRequestMessage** 으로 입력 하 고 비동기적으로 반환 된 **HttpResponseMessage**합니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-117">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="0a267-118">일반적인 구현은 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-118">A typical implementation does the following:</span></span>

1. <span data-ttu-id="0a267-119">요청 메시지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-119">Process the request message.</span></span>
2. <span data-ttu-id="0a267-120">호출 `base.SendAsync` 내부 처리기에 요청을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-120">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="0a267-121">내부 처리기는 응답 메시지를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-121">The inner handler returns a response message.</span></span> <span data-ttu-id="0a267-122">(이 단계는 비동기.)</span><span class="sxs-lookup"><span data-stu-id="0a267-122">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="0a267-123">응답을 처리 하 고 호출자에 게 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-123">Process the response and return it to the caller.</span></span>

<span data-ttu-id="0a267-124">다음 예제에서는 보내는 요청에 사용자 지정 헤더를 추가 하는 메시지 처리기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-124">The following example shows a message handler that adds a custom header to the outgoing request:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

<span data-ttu-id="0a267-125">에 대 한 호출 `base.SendAsync` 비동기적입니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-125">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="0a267-126">처리기는이 호출 후에 모든 작업을 수행 하는 경우 사용 하 여는 **await** 키워드를 메서드가 완료 된 후 실행을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-126">If the handler does any work after this call, use the **await** keyword to resume execution after the method completes.</span></span> <span data-ttu-id="0a267-127">다음 예제에서는 오류 코드를 기록 하는 처리기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-127">The following example shows a handler that logs error codes.</span></span> <span data-ttu-id="0a267-128">자체 로깅 그다지 흥미로 워 보이지 않습니다. 하지만 예제에서는 응답 처리기 내에서 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-128">The logging itself is not very interesting, but the example shows how to get at the response inside the handler.</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a><span data-ttu-id="0a267-129">클라이언트 파이프라인에 메시지 처리기 추가</span><span class="sxs-lookup"><span data-stu-id="0a267-129">Adding Message Handlers to the Client Pipeline</span></span>

<span data-ttu-id="0a267-130">사용자 지정 처리기를 추가 하려면 **HttpClient**를 사용 하 여는 **HttpClientFactory.Create** 메서드:</span><span class="sxs-lookup"><span data-stu-id="0a267-130">To add custom handlers to **HttpClient**, use the **HttpClientFactory.Create** method:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

<span data-ttu-id="0a267-131">메시지 처리기로 전달 하는 순서로 호출 됩니다는 **만들기** 메서드.</span><span class="sxs-lookup"><span data-stu-id="0a267-131">Message handlers are called in the order that you pass them into the **Create** method.</span></span> <span data-ttu-id="0a267-132">처리기가 중첩 때문에 응답 메시지는 반대 방향으로 이동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-132">Because handlers are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="0a267-133">마지막 처리기 즉, 가장 먼저 응답 메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0a267-133">That is, the last handler is the first to get the response message.</span></span>
