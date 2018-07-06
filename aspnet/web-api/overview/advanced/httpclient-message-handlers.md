---
uid: web-api/overview/advanced/httpclient-message-handlers
title: ASP.NET Web API의에서 HttpClient 메시지 처리기 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 10/01/2012
ms.assetid: 5a4b6c80-b2e9-4710-8969-d5076f7f82b8
msc.legacyurl: /web-api/overview/advanced/httpclient-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: db9edcf4fb31e967c3d4e7635f96c68829aec97d
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37831374"
---
<a name="httpclient-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="a2e7b-102">ASP.NET Web API의에서 HttpClient 메시지 처리기</span><span class="sxs-lookup"><span data-stu-id="a2e7b-102">HttpClient Message Handlers in ASP.NET Web API</span></span>
====================
<span data-ttu-id="a2e7b-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="a2e7b-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="a2e7b-104">A *메시지 처리기* 는 HTTP 요청을 수신 하 고 HTTP 응답을 반환 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-104">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span>

<span data-ttu-id="a2e7b-105">일반적으로 일련의 메시지 처리기를 함께 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-105">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="a2e7b-106">HTTP 요청을 받고 일부 처리를 요청 다음 처리기를 제공 하는 첫 번째 처리기 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-106">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="a2e7b-107">어느 시점에서 응답 생성 되 고 체인 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-107">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="a2e7b-108">이 패턴은 호출을 *위임* 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-108">This pattern is called a *delegating* handler.</span></span>

![](httpclient-message-handlers/_static/image1.png)

<span data-ttu-id="a2e7b-109">클라이언트 쪽에는 **HttpClient** 클래스 메시지 처리기를 사용 하 여 요청을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-109">On the client side, the **HttpClient** class uses a message handler to process requests.</span></span> <span data-ttu-id="a2e7b-110">기본 처리기가 **HttpClientHandler**, 네트워크를 통해 요청을 보냅니다 있으며 서버에서 응답을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-110">The default handler is **HttpClientHandler**, which sends the request over the network and gets the response from the server.</span></span> <span data-ttu-id="a2e7b-111">사용자 지정 메시지 처리기 클라이언트 파이프라인에 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-111">You can insert custom message handlers into the client pipeline:</span></span>

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="a2e7b-112">ASP.NET Web API는 또한 서버 쪽에서 메시지 처리기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-112">ASP.NET Web API also uses message handlers on the server side.</span></span> <span data-ttu-id="a2e7b-113">자세한 내용은 [HTTP 메시지 처리기](http-message-handlers.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-113">For more information, see [HTTP Message Handlers](http-message-handlers.md).</span></span>


## <a name="custom-message-handlers"></a><span data-ttu-id="a2e7b-114">사용자 지정 메시지 처리기</span><span class="sxs-lookup"><span data-stu-id="a2e7b-114">Custom Message Handlers</span></span>

<span data-ttu-id="a2e7b-115">파생 되는 사용자 지정 메시지 처리기를 작성 하려면 **System.Net.Http.DelegatingHandler** 재정의 **SendAsync** 메서드.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-115">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="a2e7b-116">메서드 시그니처는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-116">Here is the method signature:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

<span data-ttu-id="a2e7b-117">메서드는 **HttpRequestMessage** 입력 하 고 비동기적으로 반환은 **HttpResponseMessage**합니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-117">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="a2e7b-118">일반적인 구현은 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-118">A typical implementation does the following:</span></span>

1. <span data-ttu-id="a2e7b-119">요청 메시지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-119">Process the request message.</span></span>
2. <span data-ttu-id="a2e7b-120">호출 `base.SendAsync` 내부 처리기에는 요청을 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-120">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="a2e7b-121">내부 처리기는 응답 메시지를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-121">The inner handler returns a response message.</span></span> <span data-ttu-id="a2e7b-122">(이 단계는 비동기입니다.)</span><span class="sxs-lookup"><span data-stu-id="a2e7b-122">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="a2e7b-123">응답을 처리 하 고 호출자에 게 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-123">Process the response and return it to the caller.</span></span>

<span data-ttu-id="a2e7b-124">다음 예제에서는 사용자 지정 헤더를 나가는 요청에 추가 하는 메시지 처리기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-124">The following example shows a message handler that adds a custom header to the outgoing request:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

<span data-ttu-id="a2e7b-125">에 대 한 호출 `base.SendAsync` 은 비동기입니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-125">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="a2e7b-126">이 호출 후에 모든 작업 수행 하는 처리기를 사용 합니다 **await** 메서드가 완료 된 후 실행을 다시 시작 하는 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-126">If the handler does any work after this call, use the **await** keyword to resume execution after the method completes.</span></span> <span data-ttu-id="a2e7b-127">다음 예제에는 오류 코드를 기록 하는 처리기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-127">The following example shows a handler that logs error codes.</span></span> <span data-ttu-id="a2e7b-128">자체 로깅 매우 흥미로운 이지만 예제에는 처리기 내에서 응답에 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-128">The logging itself is not very interesting, but the example shows how to get at the response inside the handler.</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a><span data-ttu-id="a2e7b-129">클라이언트 파이프라인에 메시지 처리기 추가</span><span class="sxs-lookup"><span data-stu-id="a2e7b-129">Adding Message Handlers to the Client Pipeline</span></span>

<span data-ttu-id="a2e7b-130">사용자 지정 처리기를 추가할 **HttpClient**를 사용 합니다 **HttpClientFactory.Create** 메서드:</span><span class="sxs-lookup"><span data-stu-id="a2e7b-130">To add custom handlers to **HttpClient**, use the **HttpClientFactory.Create** method:</span></span>

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

<span data-ttu-id="a2e7b-131">메시지 처리기로 전달 하는 순서로 호출 되는 **만들기** 메서드.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-131">Message handlers are called in the order that you pass them into the **Create** method.</span></span> <span data-ttu-id="a2e7b-132">처리기가 중첩 되어 있으므로 응답 메시지는 반대 방향으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-132">Because handlers are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="a2e7b-133">마지막 처리기 즉, 첫 번째 응답 메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a2e7b-133">That is, the last handler is the first to get the response message.</span></span>
