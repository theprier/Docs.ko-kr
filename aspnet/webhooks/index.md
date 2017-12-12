---
uid: webhooks/index
title: "ASP.NET Webhook 개요 | Microsoft Docs"
author: rick-anderson
description: "ASP.NET Webhook을 소개 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/17/2012
ms.topic: article
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.technology: 
ms.prod: .net-framework
ms.openlocfilehash: 52399c23cdf393a2f7f94661fd48098ced65948c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
# <a name="aspnet-webhooks-overview"></a>ASP.NET Webhook 개요

또한 Webhook 배선 함께 웹 Api 및 SaaS 서비스에 대 한 간단한 pub/sub 모델을 제공 하는 간단한 HTTP 패턴입니다. 서비스에는 이벤트가 발생 하면 등록 된 구독자에 HTTP POST 요청의 형태로 알림이 보내집니다. POST 요청의 수신자 문제에 대 한 가능 하 게 하는 이벤트에 대 한 정보를 포함 합니다.

그 단순 함으로 인해 Webhook 많이 포함 하 여 서비스에 의해 노출 이미 되 [Dropbox](http://dropbox.com/), [GitHub](http://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp ](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [스트라이프](http://www.stripe.com), [Trello](http://www.trello.com/), 및 기타 다양 합니다. 예를 들어 파일에서 변경 되었습니다 여 webhook을 사용할지를 나타낼 수 [Dropbox](http://dropbox.com/), 또는 GitHub에서 코드 변경이 커밋 또는 지불에 시작 되어 [PayPal](http://www.paypal.com/), 카드에 생성 되었음을 또는 [ Trello](http://www.trello.com/)합니다. 이 속성은 무한!

Microsoft ASP.NET Webhook을 사용 하면 쉽게 보내고 Webhook ASP.NET 응용 프로그램의 일환으로 받아:

* 수신 측에서 받아 WebHook 공급자의 다양 한 Webhook을 처리 하기 위한 일반적인 모델을 제공 합니다. 에 대 한 지원 사용 하 여 상자 나올 [Dropbox](http://dropbox.com/), [GitHub](http://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [스트라이프](http://www.stripe.com), [Trello](http://www.trello.com/),[ WordPress](http://www.wordpress.com) 및 [Zendesk](https://www.zendesk.com/) 하지만 더에 대 한 지원을 추가 하기 쉽습니다.

* 보내는 쪽에서 관리 하 고 올바른 집합이 구독자에 게 이벤트 알림을 전송 하는 경우와 구독을 저장 하기 위한 지원을 제공 합니다. 이 옵션을 사용 하면 이벤트 구독자를 구독 하 고 발생 하는 작업이 면 수의 자체 집합을 정의할 수 있습니다.

두 부분으로 구성 시나리오에 따라 떨어져 있는 또는 함께 사용할 수 있습니다. 방금 수신기 부분; 사용 하 여 다른 서비스에서 Webhook을 수신 해야 하는 경우 사용할 다른 사용자에 대 한 Webhook을 노출 하려는 경우 다음 할 수 있는 해당 합니다.

코드는 ASP.NET Web API 2 및 ASP.NET MVC 5를 대상으로 하 고로 제공 됩니다 [GitHub의 OSS](https://github.com/aspnet/WebHooks)합니다.

## <a name="webhooks-overview"></a>또한 Webhook 개요

Webhook은 서비스에 서비스에서 사용 방법 다양 하지만 기본 개념은 동일 의미는 패턴입니다. 생각할 수 있습니다 Webhook의 간단한 pub/sub 모델 사용자가 다른 곳에서 발생 하는 이벤트를 구독할 수입니다. 이벤트 알림은 이벤트 자체에 대 한 정보를 포함 하는 HTTP POST 요청으로 전파 됩니다.

일반적으로 HTTP POST 요청에는 JSON 개체 또는 HTML 폼 데이터를 트리거하는 WebHook을 유발 하는 이벤트에 대 한 정보를 포함 하 여 WebHook 발신자가 결정이 포함 되어 있습니다. 예를 들어에서 WebHook POST 요청 본문의 예 [GitHub](http://www.github.com/) 특정 저장소에서 열린 새 문제의 결과로이 것 같습니다.

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

WebHook가 의도 한 보낸 사람 으로부터 실제로 보장 하려면 POST 요청이 몇 가지 방법으로 보안 하 고 수신기의 확인 합니다. 예를 들어 [GitHub Webhook](https://developer.github.com/webhooks/) 포함는 *X 허브 서명* 걱정할 필요 없이 수신기 구현에서 확인 하는 요청 본문의 해시가 있는 HTTP 헤더입니다.

일반적으로 WebHook 흐름을 다음과 같이 진행합니다.

* WebHook 보낸 클라이언트가 구독할 수 있는 이벤트를 노출 합니다. 이벤트 observable 변경에 설명 시스템, 예를 들어 새 데이터 항목을 삽입 하는 프로세스가 완료 되 면 또는 다른 값인지 된 합니다.

* WebHook 수신기로 구성 된 4 가지 WebHook을 등록 하 여 구독:

     1. 이벤트 알림의 HTTP POST 요청;의 형태로 게시 해야 하는 위치에 대 한 URI

     2. 필터는에 대 한 WebHook 실행 되는; 특정 이벤트를 설명 하는 집합

     3. HTTP POST 요청을 서명 하는 데 사용 되는 비밀 키

     4. HTTP POST 요청에 포함 하는 추가 데이터입니다. 예를 들어 추가 HTTP 헤더 필드 또는 HTTP POST 요청 본문에 포함 된 속성 수 있습니다.

* 이벤트가 발생할 일치 하는 WebHook 등록이 발견 되 고 있는 HTTP POST 요청에 제출 됩니다. 일반적으로 HTTP POST 요청을 생성 하는 경우에 대 한 받는 사람에 게 응답 하지 않는 몇 가지 이유 또는 오류 응답에서 HTTP POST 요청 결과 여러 번 다시 시도 됩니다.

## <a name="webhooks-processing-pipeline"></a>또한 Webhook 처리 파이프라인

들어오는 Webhook에 대 한 Microsoft ASP.NET Webhook 처리 파이프라인은 다음과 같습니다.

![ASP.NET Webhook 처리 파이프라인](_static/WebHookReceivers.png)

다음 두 가지 핵심 개념은 *수신기* 및 *처리기*:

* *수신기* 되는지 알아보려면 WebHook 요청 실제로 의도 한 보낸 사람 으로부터 보안 검사를 적용 하 고 지정 된 보낸 사람 으로부터 WebHook의 특정 버전을 처리 하기 위한 해야 합니다.

* *처리기* 는 일반적으로 사용자 코드 처리 특정 WebHook 실행 되는 위치입니다.

다음 노드 이러한 개념을 자세히 설명 되어 있습니다.
