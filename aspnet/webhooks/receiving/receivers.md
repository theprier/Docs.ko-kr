---
uid: webhooks/receiving/receivers
title: ASP.NET 웹 후크 수신기 | Microsoft Docs
author: rick-anderson
description: ASP.NET 웹 후크 수신기
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/17/2012
ms.topic: article
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.technology: ''
ms.openlocfilehash: be1f7dcef60642231af9c593eb7329ede7c2094f
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374745"
---
# <a name="aspnet-webhooks-receivers"></a><span data-ttu-id="3ed2d-103">ASP.NET 웹 후크 수신기</span><span class="sxs-lookup"><span data-stu-id="3ed2d-103">ASP.NET WebHooks receivers</span></span>

<span data-ttu-id="3ed2d-104">Webhook를 받는 발신자가 있는 사용자에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="3ed2d-104">Receiving WebHooks depends on who the sender is.</span></span> <span data-ttu-id="3ed2d-105">경우에 따라 구독자는 실제로 수신 대기 하는지 확인 하는 웹 후크를 등록 하는 추가 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ed2d-105">Sometimes there are additional steps registering a WebHook verifying that the subscriber is really listening.</span></span> <span data-ttu-id="3ed2d-106">일부 웹 후크 HTTP POST 요청을 독립적으로 검색 되는 이벤트 정보에 대 한 참조만 포함 되는 위치 밀어넣기-끌어오기 모델을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed2d-106">Some WebHooks provide a push-to-pull model where the HTTP POST request only contains a reference to the event information which is then to be retrieved independently.</span></span> <span data-ttu-id="3ed2d-107">종종 보안 모델은 상당히 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="3ed2d-107">Often the security model varies quite a bit.</span></span>

<span data-ttu-id="3ed2d-108">Microsoft ASP.NET 웹 후크의 목적은 간단 하 고 일관성 있게 Webhook의 특정 변형을 처리 하는 방법을 파악 하는 시간이 많이 소비 하지 않고 API를 연결 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed2d-108">The purpose of Microsoft ASP.NET WebHooks is to make it both simpler and more consistent to wire up your API without spending a lot of time figuring out how to handle any particular variant of WebHooks.</span></span>

<span data-ttu-id="3ed2d-109">웹 후크 수신기는 수락 하 고 특정 보낸에서 웹 후크를 확인 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed2d-109">A WebHook receiver is responsible for accepting and verifying WebHooks from a particular sender.</span></span> <span data-ttu-id="3ed2d-110">웹 후크 수신기는 임의 개수의 Webhook 각각 고유한 구성을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ed2d-110">A WebHook receiver can support any number of WebHooks, each with their own configuration.</span></span> <span data-ttu-id="3ed2d-111">예를 들어 GitHub 웹 후크 수신기 GitHub 리포지토리에 있는 모든 수의 웹 후크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ed2d-111">For example, the GitHub WebHook receiver can accept WebHooks from any number of GitHub repositories.</span></span>

## <a name="webhook-receiver-uris"></a><span data-ttu-id="3ed2d-112">웹 후크 수신기 Uri</span><span class="sxs-lookup"><span data-stu-id="3ed2d-112">WebHook Receiver URIs</span></span>

<span data-ttu-id="3ed2d-113">Microsoft ASP.NET 웹 후크를 설치 하 여 서비스는 개방형 수의 웹 후크 요청을 수락 하는 일반 웹 후크 컨트롤러를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ed2d-113">By installing Microsoft ASP.NET WebHooks you get a general WebHook controller which accepts WebHook requests from an open-ended number of services.</span></span> <span data-ttu-id="3ed2d-114">요청이 도착 하면 특정 WebHook 발신자를 처리 하는 것에 대 한 설치 된 적절 한 수신기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed2d-114">When a request arrives, it picks the appropriate receiver that you have installed for handling a particular WebHook sender.</span></span>

<span data-ttu-id="3ed2d-115">이 컨트롤러의 URI는 서비스를 사용 하 여 등록 하는 웹 후크 URI 이며 형식:</span><span class="sxs-lookup"><span data-stu-id="3ed2d-115">The URI of this controller is the WebHook URI that you register with the service and is of the form:</span></span>

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

<span data-ttu-id="3ed2d-116">보안상의 이유로 많은 WebHook 수신기를 사용 하려면 URI는 *https* URI 및 일부 경우에도 포함 해야는 의도 된 파티 위의 URI에 웹 후크를 보낼 수만 적용 하는 데 사용 되는 추가 쿼리 매개 변수 .</span><span class="sxs-lookup"><span data-stu-id="3ed2d-116">For security reasons, many WebHook receivers require that the URI is an *https* URI and in some cases it must also contain an additional query parameter which is used to enforce that only the intended party can send WebHooks to the URI above.</span></span>

<span data-ttu-id="3ed2d-117">합니다 <em> <receiver> </em> 구성 요소는 수신기의 이름 예를 들어 <em>github</em> 하거나 <em>slack</em>합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed2d-117">The <em><receiver></em> component is the name of the receiver, for example <em>github</em> or <em>slack</em>.</span></span>

<span data-ttu-id="3ed2d-118">합니다 *{id}* 특정 WebHook 수신기 구성을 식별 하는 선택적 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="3ed2d-118">The *{id}* is an optional identifier which can be used to identify a particular WebHook receiver configuration.</span></span> <span data-ttu-id="3ed2d-119">이 특정 수신기를 사용 하 여 N 웹 후크를 등록 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ed2d-119">This can be used to register N WebHooks with a particular receiver.</span></span> <span data-ttu-id="3ed2d-120">예를 들어, 세 가지 독립적인 웹 후크에 대 한 등록 하는 다음 세 가지 Uri는 사용할 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="3ed2d-120">For example, the following three URIs can be used to register for three independent WebHooks:</span></span>

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a><span data-ttu-id="3ed2d-121">웹 후크 수신기 설치</span><span class="sxs-lookup"><span data-stu-id="3ed2d-121">Installing a WebHook Receiver</span></span>

<span data-ttu-id="3ed2d-122">Microsoft ASP.NET 웹 후크를 사용 하 여 웹 후크를 수신 하려면 먼저 웹 후크 공급자 또는 공급자의 웹 후크를 받으려면 Nuget 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed2d-122">To receive WebHooks using Microsoft ASP.NET WebHooks, you first install the Nuget package for the WebHook provider or providers you want to receive WebHooks from.</span></span> <span data-ttu-id="3ed2d-123">Nuget 패키지 라고 [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) 여기서 마지막 부분에 지원 되는 서비스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3ed2d-123">The Nuget packages are named [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) where the last part indicates the service supported.</span></span> <span data-ttu-id="3ed2d-124">예</span><span class="sxs-lookup"><span data-stu-id="3ed2d-124">For example</span></span>

<span data-ttu-id="3ed2d-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) GitHub에서 웹 후크를 수신 하기 위한 지원을 제공 하 고 [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) ASP에서 생성 하는 웹 후크를 수신 하기 위한 지원을 제공 합니다. NET 웹 후크입니다.</span><span class="sxs-lookup"><span data-stu-id="3ed2d-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) provides support for receiving WebHooks from GitHub and [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) provides support for receiving WebHooks generated by ASP.NET WebHooks.</span></span>

<span data-ttu-id="3ed2d-126">Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, 스트라이프, Trello 및 WordPress에 대 한 지원을 기본적 있습니다 하지만 임의 개수의 다른 공급자를 지원 하기 위해 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed2d-126">Out of the box you can find support for Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello, and WordPress but it is possible to support any number of other providers.</span></span>

## <a name="configuring-a-webhook-receiver"></a><span data-ttu-id="3ed2d-127">웹 후크 수신기 구성</span><span class="sxs-lookup"><span data-stu-id="3ed2d-127">Configuring a WebHook Receiver</span></span>

<span data-ttu-id="3ed2d-128">WebHook 수신기를 통해 구성 되는 [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) 해당 인터페이스의 특정 구현 및 인터페이스에 모든 종속성 주입 모델을 사용 하 여 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ed2d-128">WebHook Receivers are configured through the [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface and particular implementations of that interface can be registered using any dependency injection model.</span></span> <span data-ttu-id="3ed2d-129">기본 구현에는 Web.config 파일에서 설정할 수 있습니다, Azure Web Apps를 사용 하는 경우를 통해 설정할 수 있는 응용 프로그램 설정을 사용 합니다 [Azure Portal](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed2d-129">The default implementation uses Application Settings which can either be set in the Web.config file, or, if using Azure Web Apps, can be set through the [Azure Portal](https://portal.azure.com/).</span></span>

![Azure 앱 설정](_static/AzureAppSettings.png)

<span data-ttu-id="3ed2d-131">응용 프로그램 설정 키의 형식은 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3ed2d-131">The format for Application Setting keys is as follows:</span></span>

```
MS_WebHookReceiverSecret_<receiver>
```

<span data-ttu-id="3ed2d-132">값이 일치 하는 값의 쉼표로 구분 된 목록을 합니다 *{id}* 는 웹 후크 등록 된, 예를 들어 값:</span><span class="sxs-lookup"><span data-stu-id="3ed2d-132">The value is a comma-separated list of values matching the *{id}* values for which WebHooks have been registered, for example:</span></span>

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a><span data-ttu-id="3ed2d-133">웹 후크 수신기를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="3ed2d-133">Initializing a WebHook Receiver</span></span>

<span data-ttu-id="3ed2d-134">웹 후크 수신기에, 일반적으로 등록 하 여 초기화 되는 *WebApiConfig* 예를 들어 정적 클래스:</span><span class="sxs-lookup"><span data-stu-id="3ed2d-134">WebHook Receivers are initialized by registering them, typically in the *WebApiConfig* static class, for example:</span></span>

```csharp
namespace WebHookReceivers
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            // Load receivers
            config.InitializeReceiveGitHubWebHooks();
        }
    }
}
```
