---
uid: webhooks/receiving/handlers
title: "ASP.NET Webhook 처리기 | Microsoft Docs"
author: rick-anderson
description: "ASP.NET Webhook에 대 한 요청을 처리 하는 방법."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/17/2012
ms.topic: article
ms.assetid: a55b0d20-9c90-4bd3-a471-20da6f569f0c
ms.technology: 
ms.prod: .net-framework
ms.openlocfilehash: 4cf5770a731ef77842eb29b0a66ee0aac5d85d85
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="aspnet-webhooks-handlers"></a><span data-ttu-id="a03ae-103">ASP.NET Webhook 처리기</span><span class="sxs-lookup"><span data-stu-id="a03ae-103">ASP.NET WebHooks handlers</span></span>

<span data-ttu-id="a03ae-104">Webhook 요청 WebHook 수신기가 확인 되 면 사용자 코드에서 처리할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a03ae-104">Once WebHooks requests has been validated by a WebHook receiver, it is ready to be processed by user code.</span></span> <span data-ttu-id="a03ae-105">여기에 *처리기* 와 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03ae-105">This is where *handlers* come in.</span></span> <span data-ttu-id="a03ae-106">처리기에서 파생 되는 [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) 인터페이스 얻으면서도 일반적으로 사용 하 여는 [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) 인터페이스에서 직접 파생 하는 대신 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a03ae-106">Handlers derive from the [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) interface but typically uses the [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) class instead of deriving directly from the interface.</span></span>

<span data-ttu-id="a03ae-107">하나 이상의 처리기가 WebHook 요청을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03ae-107">A WebHook request can be processed by one or more handlers.</span></span> <span data-ttu-id="a03ae-108">처리기는 각각의 해당 기반의 순서 대로 호출 됩니다 *순서* 것으로 가장 높은 순서는 (1에서 100 사이 여야 하도록 제안) 단순 정수 속성:</span><span class="sxs-lookup"><span data-stu-id="a03ae-108">Handlers are called in order based on their respective *Order* property going from lowest to highest where Order is a simple integer (suggested to be between 1 and 100):</span></span>

![WebHook 처리기 순서 속성 다이어그램](_static/Handlers.png)

<span data-ttu-id="a03ae-110">처리기를 선택적으로 설정할 수는 *응답* WebHookHandlerContext WebHook에 대 한 HTTP 응답으로 다시 전송 될 응답을 중지 하는 처리 진행 되는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a03ae-110">A handler can optionally set the *Response* property on the WebHookHandlerContext which will lead the processing to stop and the response to be sent back as the HTTP response to the WebHook.</span></span> <span data-ttu-id="a03ae-111">앞의 경우에서 B 및 B 응답 설정 하는 것 보다 더 높은 순서 있기 때문에 처리기 C 호출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a03ae-111">In the case above, Handler C won't get called because it has a higher order than B and B sets the response.</span></span>

<span data-ttu-id="a03ae-112">응답 설정 일반적으로 관련 된 Webhook 응답 정보를 다시 원래 API 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03ae-112">Setting the response is typically only relevant for WebHooks where the response can carry information back to the originating API.</span></span> <span data-ttu-id="a03ae-113">이 예의 경우와 Slack Webhook이에서 WebHook 있었던 채널에 다시 응답을 게시 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="a03ae-113">This is for example the case with Slack WebHooks where the response is posted back to the channel where the WebHook came from.</span></span> <span data-ttu-id="a03ae-114">처리기만 Webhook 해당 특정 수신기에서 수신 하려는 경우 수신기 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a03ae-114">Handlers can set the Receiver property if they only want to receive WebHooks from that particular receiver.</span></span> <span data-ttu-id="a03ae-115">수신기를 설정 하지 않는 경우 모든 작업이 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a03ae-115">If they don't set the receiver they are called for all of them.</span></span>

<span data-ttu-id="a03ae-116">사용 하는 응답의 다른 한 가지 일반적인 용도 *410 없음* 응답 표시 되는 WebHook 더 이상 활성화 되어 요청이 제출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03ae-116">One other common use of a response is to use a *410 Gone* response to indicate that the WebHook no longer is active and no further requests should be submitted.</span></span>

<span data-ttu-id="a03ae-117">기본적으로 한 처리기는 모든 WebHook 수신기가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a03ae-117">By default a handler will be called by all WebHook receivers.</span></span> <span data-ttu-id="a03ae-118">그러나 경우는 *수신기* 는 처리기의 이름 속성은 다음 처리기에서 해당 수신기만 WebHook 요청을 받지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a03ae-118">However, if the *Receiver* property is set to the name of a handler then that handler will only receive WebHook requests from that receiver.</span></span>

## <a name="processing-a-webhook"></a><span data-ttu-id="a03ae-119">WebHook 처리</span><span class="sxs-lookup"><span data-stu-id="a03ae-119">Processing a WebHook</span></span>

<span data-ttu-id="a03ae-120">처리기가 호출 될 때 가져옵니다는 [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) WebHook 요청에 대 한 정보가 들어 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="a03ae-120">When a handler is called, it gets a [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) containing information about the WebHook request.</span></span> <span data-ttu-id="a03ae-121">일반적으로 HTTP 요청 본문 데이터를 사용할 수는 *데이터* 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a03ae-121">The data, typically the HTTP request body, is available from the *Data* property.</span></span>

<span data-ttu-id="a03ae-122">데이터의 형식을 JSON 또는 HTML 양식 데이터는 일반적으로 하지만 원하는 경우를 더 구체적인 형식으로 캐스팅 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03ae-122">The type of the data is typically JSON or HTML form data, but it is possible to cast to a more specific type if desired.</span></span> <span data-ttu-id="a03ae-123">ASP.NET Webhook에 의해 생성 된 사용자 지정 Webhook 형식으로 캐스팅할 수는 예를 들어 [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a03ae-123">For example, the custom WebHooks generated by ASP.NET WebHooks can be cast to the type [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) as follows:</span></span>

```csharp
public class MyWebHookHandler : WebHookHandler
{
    public MyWebHookHandler()
    {
        this.Receiver = "custom";
    }

    public override Task ExecuteAsync(string generator, WebHookHandlerContext context)
    {
        CustomNotifications notifications = context.GetDataOrDefault<CustomNotifications>();
        foreach (var notification in notifications.Notifications)
        {
            ...
        }
        return Task.FromResult(true);
    }
}
```

  ## <a name="queued-processing"></a><span data-ttu-id="a03ae-124">지연된 처리</span><span class="sxs-lookup"><span data-stu-id="a03ae-124">Queued Processing</span></span>

<span data-ttu-id="a03ae-125">응답은 약간의 시간 (초) 내에서 생성 되지 않은 경우 대부분 WebHook 발신자는 한 WebHook을 다시 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a03ae-125">Most WebHook senders will resend a WebHook if a response is not generated within a handful of seconds.</span></span> <span data-ttu-id="a03ae-126">즉, 처리기가 다시 호출 되어 하지 하기 위해에서 해당 시간 프레임 내에서 처리를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03ae-126">This means that your handler must complete the processing within that time frame in order not for it to be called again.</span></span>

<span data-ttu-id="a03ae-127">처리 더 오래 걸리며 또는 더 잘 콘텐츠를 수정 하는 경우 다음의 [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) 는 예를 들어 큐에 WebHook 요청을 제출 하는 데 사용할 수 [Azure 저장소 큐](https://msdn.microsoft.com/library/azure/dd179353.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="a03ae-127">If the processing takes longer, or is better handled separately then the [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) can be used to submit the WebHook request to a queue, for example [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span></span>

<span data-ttu-id="a03ae-128">개요는 [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) 구현을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a03ae-128">An outline of a [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) implementation is provided here:</span></span>

```csharp
public class QueueHandler : WebHookQueueHandler
{
    public override Task EnqueueAsync(WebHookQueueContext context)
    {

        // Enqueue WebHookQueueContext to your queuing system of choice

        return Task.FromResult(true);
    }
}
```
