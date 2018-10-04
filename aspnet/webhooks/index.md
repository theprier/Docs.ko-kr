---
uid: webhooks/index
title: ASP.NET 웹 후크 개요 | Microsoft Docs
author: rick-anderson
description: ASP.NET 웹 후크에 대해 소개 합니다.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: 702cc0bf0d0bb887c64bec19e1faf249bd96617a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "48254961"
---
# <a name="aspnet-webhooks-overview"></a><span data-ttu-id="f16eb-103">ASP.NET 웹 후크 개요</span><span class="sxs-lookup"><span data-stu-id="f16eb-103">ASP.NET WebHooks overview</span></span>

<span data-ttu-id="f16eb-104">WebHook는 Web API와 SaaS 서비스를 연결하는 간단한 pub/sub 모델을 제공하는 가벼운 HTTP 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-104">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="f16eb-105">서비스에서 이벤트가 발생하면 등록된 구독자에게 HTTP POST 요청의 형태로 알림이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-105">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="f16eb-106">POST 요청에는 수신자가 적절하게 대처할 수 있도록 이벤트에 대한 정보를 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-106">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="f16eb-107">단순성, 때문에 Webhook가 이미 노출 비롯 하 여 서비스의 많은 [Dropbox](http://dropbox.com/), [GitHub](http://www.github.com/)합니다 [Bitbucket](https://bitbucket.org/), [MailChimp ](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com)를 [스트라이프](http://www.stripe.com)를 [Trello](http://www.trello.com/), 더 많은 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-107">Because of their simplicity, WebHooks are already exposed by a large number of services including [Dropbox](http://dropbox.com/), [GitHub](http://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), and many more.</span></span> <span data-ttu-id="f16eb-108">예를 들어, 웹 후크에서 파일을이 변경 되었음을 나타낼 수 있습니다 [Dropbox](http://dropbox.com/)를 GitHub에서 코드 변경을 커밋한 또는 지불에 시작 되었습니다 [PayPal](http://www.paypal.com/), 카드에 만들어진 또는 [ Trello](http://www.trello.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-108">For example, a WebHook can indicate that a file has changed in [Dropbox](http://dropbox.com/), or a code change has been committed in GitHub, or a payment has been initiated in [PayPal](http://www.paypal.com/), or a card has been created in [Trello](http://www.trello.com/).</span></span> <span data-ttu-id="f16eb-109">가능성은 무한!</span><span class="sxs-lookup"><span data-stu-id="f16eb-109">The possibilities are endless!</span></span>

<span data-ttu-id="f16eb-110">Microsoft ASP.NET 웹 후크 쉽게 송신 및 ASP.NET 응용 프로그램의 일부로 웹 후크를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-110">Microsoft ASP.NET WebHooks makes it easier to both send and receive WebHooks as part of your ASP.NET application:</span></span>

* <span data-ttu-id="f16eb-111">수신 측에서는 받아 WebHook 공급자의 다양 한 웹 후크를 처리 하기 위한 일반적인 모델을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-111">On the receiving side, it provides a common model for receiving and processing WebHooks from any number of WebHook providers.</span></span> <span data-ttu-id="f16eb-112">에 대 한 지원 사용 하 여 상자 나올 [Dropbox](http://dropbox.com/)를 [GitHub](http://www.github.com/)를 [Bitbucket](https://bitbucket.org/)를 [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [푸 셔](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [스트라이프](http://www.stripe.com), [Trello](http://www.trello.com/)합니다[ WordPress](http://www.wordpress.com) 하 고 [Zendesk](https://www.zendesk.com/) 있지만 자세히에 대 한 지원을 추가 하는 것이 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-112">It comes out of the box with support for [Dropbox](http://dropbox.com/), [GitHub](http://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) and [Zendesk](https://www.zendesk.com/) but it is easy to add support for more.</span></span>

* <span data-ttu-id="f16eb-113">보내는 쪽에서 관리 및 구독자의 올바른 집합에 이벤트 알림을 보내는 경우와 구독을 저장 하기 위한 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-113">On the sending side it provides support for managing and storing subscriptions as well as for sending event notifications to the right set of subscribers.</span></span> <span data-ttu-id="f16eb-114">이 통해 사용자 고유의 이벤트 집합을 구독자가 구독 하 고 작업을 수행 하는 경우 사용자에 게 알릴 수를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-114">This allows you to define your own set of events that subscribers can subscribe to and notify them when things happens.</span></span>

<span data-ttu-id="f16eb-115">두 부분 시나리오에 따라 분리 또는 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-115">The two parts can be used together or apart depending on your scenario.</span></span> <span data-ttu-id="f16eb-116">받는 사람 부분만;를 사용 하 여 다른 서비스에서 웹 후크를 수신 해야 하는 경우 사용할 다른 사용자에 대 한 웹 후크를 노출 하려는 경우 다음 수행할 수 있습니다는.</span><span class="sxs-lookup"><span data-stu-id="f16eb-116">If you only need to receive WebHooks from other services then you can use just the receiver part; if you only want to expose WebHooks for others to consume, then you can do just that.</span></span>

<span data-ttu-id="f16eb-117">코드를 ASP.NET Web API 2 및 ASP.NET MVC 5를 대상으로 하 고이 제품은 [GitHub에서 OSS](https://github.com/aspnet/WebHooks)합니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-117">The code targets ASP.NET Web API 2 and ASP.NET MVC 5 and is available as [OSS on GitHub](https://github.com/aspnet/WebHooks).</span></span>

## <a name="webhooks-overview"></a><span data-ttu-id="f16eb-118">웹 후크 개요</span><span class="sxs-lookup"><span data-stu-id="f16eb-118">WebHooks Overview</span></span>

<span data-ttu-id="f16eb-119">Webhook에는 해당 서비스에 서비스에서 사용 방법 다르지만 기본 개념은 동일 즉 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-119">WebHooks is a pattern which means that it varies how it is used from service to service but the basic idea is the same.</span></span> <span data-ttu-id="f16eb-120">생각할 수 있습니다 웹 후크의 간단한 pub/sub 모델을 사용자가 다른 곳에서 발생 하는 이벤트를 구독할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-120">You can think of WebHooks as a simple pub/sub model where a user can subscribe to events happening elsewhere.</span></span> <span data-ttu-id="f16eb-121">이벤트 알림은 이벤트 자체에 대 한 정보를 포함 하는 HTTP POST 요청으로 전파 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-121">The event notifications are propagated as HTTP POST requests containing information about the event itself.</span></span>

<span data-ttu-id="f16eb-122">일반적으로 HTTP POST 요청에는 JSON 개체 또는 HTML 양식 데이터를 트리거하는 WebHook를 유발 하는 이벤트에 대 한 정보를 포함 하 여 웹 후크 발신자가 결정이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-122">Typically the HTTP POST request contains a JSON object or HTML form data determined by the WebHook sender including information about the event causing the WebHook to trigger.</span></span> <span data-ttu-id="f16eb-123">예제에서 웹 후크 POST 요청 본문의 예를 들어 [GitHub](http://www.github.com/) 같습니다 특정 저장소에서 열린 새 문제를 결과로:</span><span class="sxs-lookup"><span data-stu-id="f16eb-123">For example, an example of a WebHook POST request body from [GitHub](http://www.github.com/) looks like this as a result of a new issue being opened in a particular repository:</span></span>

```json
{
  "action": "opened",
  "issue": {
      "url": "https://api.github.com/repos/octocat/Hello-World/issues/1347",
      "number": 1347,
      ...
  },
  "repository": {
      "id": 1296269,
      "full_name": "octocat/Hello-World",
      "owner": {
          "login": "octocat",
          "id": 1
          ...
      },
      ...
  },
  "sender": {
      "login": "octocat",
      "id": 1,
      ...
  }
}
```

<span data-ttu-id="f16eb-124">되도록 WebHook 실제로 의도 한 보낸 사람 으로부터, POST 요청을는 어떤 방식으로든에서 보호 되 고 그런 다음 수신자에 의해 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-124">To ensure that the WebHook is indeed from the intended sender, the POST request is secured in some way and then verified by the receiver.</span></span> <span data-ttu-id="f16eb-125">예를 들어 [GitHub 웹 후크](https://developer.github.com/webhooks/) 포함을 *X-허브-서명* 걱정할 필요가 수신기 구현에서 확인 하는 요청 본문의 해시를 사용 하 여 HTTP 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-125">For example, [GitHub WebHooks](https://developer.github.com/webhooks/) includes an *X-Hub-Signature* HTTP header with a hash of the request body which is checked by the receiver implementation so you don't have to worry about it.</span></span>

<span data-ttu-id="f16eb-126">일반적으로 웹 후크 흐름을 다음과 같이 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-126">The WebHook flow generally goes something like this:</span></span>

* <span data-ttu-id="f16eb-127">웹 후크 발신자 클라이언트가 구독할 수 있는 이벤트를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-127">The WebHook sender exposes events that a client can subscribe to.</span></span> <span data-ttu-id="f16eb-128">이벤트 observable 변경 내용을 설명 시스템 예를 들어 된 새 데이터 항목을 삽입 하는 프로세스가 완료 되 면 또는 다른 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-128">The events describe observable changes to the system, for example that a new data item has been inserted, that a process has completed, or something else.</span></span>

* <span data-ttu-id="f16eb-129">웹 후크 수신기 네 가지 중 구성 된 웹 후크를 등록 하 여 구독:</span><span class="sxs-lookup"><span data-stu-id="f16eb-129">The WebHook receiver subscribes by registering a WebHook consisting of four things:</span></span>

     1. <span data-ttu-id="f16eb-130">여기서는 HTTP POST 요청의 형태로 이벤트 알림을 게시 해야 하는 것에 대 한 URI</span><span class="sxs-lookup"><span data-stu-id="f16eb-130">A URI for where the event notification should be posted in the form of an HTTP POST request;</span></span>

     2. <span data-ttu-id="f16eb-131">웹 후크를 실행할지; 특정 이벤트를 설명 하는 필터 집합을</span><span class="sxs-lookup"><span data-stu-id="f16eb-131">A set of filters describing the particular events for which the WebHook should be fired;</span></span>

     3. <span data-ttu-id="f16eb-132">HTTP POST 요청에 서명 하는 데 사용 되는 비밀 키</span><span class="sxs-lookup"><span data-stu-id="f16eb-132">A secret key which is used to sign the HTTP POST request;</span></span>

     4. <span data-ttu-id="f16eb-133">HTTP POST 요청에 포함 하는 추가 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-133">Additional data which is to be included in the HTTP POST request.</span></span> <span data-ttu-id="f16eb-134">예를 들어 추가 HTTP 헤더 필드 또는 속성 HTTP POST 요청 본문에 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-134">This can for example be additional HTTP header fields or properties included in the HTTP POST request body.</span></span>

* <span data-ttu-id="f16eb-135">이벤트 발생 후 일치 하는 웹 후크 등록 검색 되 고 HTTP POST 요청 제출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-135">Once an event happens, the matching WebHook registrations are found and HTTP POST requests are submitted.</span></span> <span data-ttu-id="f16eb-136">일반적으로 HTTP POST 요청을 생성 하는 경우에 받는 사람이 응답 하지 않는 이유로 오류 응답에서 HTTP POST 요청 결과 여러 번 다시 시도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-136">Typically, the generation of the HTTP POST requests are retried several times if for some reason the recipient is not responding or the HTTP POST request results in an error response.</span></span>

## <a name="webhooks-processing-pipeline"></a><span data-ttu-id="f16eb-137">웹 후크 처리 파이프라인</span><span class="sxs-lookup"><span data-stu-id="f16eb-137">WebHooks Processing Pipeline</span></span>

<span data-ttu-id="f16eb-138">들어오는 웹 후크에 대 한 Microsoft ASP.NET 웹 후크 처리 파이프라인은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-138">The Microsoft ASP.NET WebHooks processing pipeline for incoming WebHooks looks like this:</span></span>

![웹 후크 ASP.NET 처리 파이프라인](_static/WebHookReceivers.png)

<span data-ttu-id="f16eb-140">다음 두 가지 핵심 개념은 *수신자* 하 고 *처리기*:</span><span class="sxs-lookup"><span data-stu-id="f16eb-140">The two key concepts here are *Receivers* and *Handlers*:</span></span>

* <span data-ttu-id="f16eb-141">*수신기* 되도록 웹 후크 요청 실제로 의도 한 보낸 사람에 게 보안 검사를 적용 한 지정된 발신자에서 WebHook의 특정 버전을 처리 하는 것에 대 한 책임이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-141">*Receivers* are responsible for handling the particular flavor of WebHook from a given sender and for enforcing security checks to ensure that the WebHook request indeed is from the intended sender.</span></span>

* <span data-ttu-id="f16eb-142">*처리기* 는 일반적으로 사용자 코드 실행 특정 웹 후크를 처리 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-142">*Handlers* are typically where user code runs processing the particular WebHook.</span></span>

<span data-ttu-id="f16eb-143">다음 노드가 이러한 개념 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f16eb-143">In the following nodes these concepts are described in more details.</span></span>
