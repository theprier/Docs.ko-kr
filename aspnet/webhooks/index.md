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
# <a name="aspnet-webhooks-overview"></a>ASP.NET 웹 후크 개요

WebHook는 Web API와 SaaS 서비스를 연결하는 간단한 pub/sub 모델을 제공하는 가벼운 HTTP 패턴입니다. 서비스에서 이벤트가 발생하면 등록된 구독자에게 HTTP POST 요청의 형태로 알림이 전송됩니다. POST 요청에는 수신자가 적절하게 대처할 수 있도록 이벤트에 대한 정보를 포함되어 있습니다.

단순성, 때문에 Webhook가 이미 노출 비롯 하 여 서비스의 많은 [Dropbox](http://dropbox.com/), [GitHub](http://www.github.com/)합니다 [Bitbucket](https://bitbucket.org/), [MailChimp ](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com)를 [스트라이프](http://www.stripe.com)를 [Trello](http://www.trello.com/), 더 많은 기능입니다. 예를 들어, 웹 후크에서 파일을이 변경 되었음을 나타낼 수 있습니다 [Dropbox](http://dropbox.com/)를 GitHub에서 코드 변경을 커밋한 또는 지불에 시작 되었습니다 [PayPal](http://www.paypal.com/), 카드에 만들어진 또는 [ Trello](http://www.trello.com/)합니다. 가능성은 무한!

Microsoft ASP.NET 웹 후크 쉽게 송신 및 ASP.NET 응용 프로그램의 일부로 웹 후크를 수신 합니다.

* 수신 측에서는 받아 WebHook 공급자의 다양 한 웹 후크를 처리 하기 위한 일반적인 모델을 제공 합니다. 에 대 한 지원 사용 하 여 상자 나올 [Dropbox](http://dropbox.com/)를 [GitHub](http://www.github.com/)를 [Bitbucket](https://bitbucket.org/)를 [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [푸 셔](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [스트라이프](http://www.stripe.com), [Trello](http://www.trello.com/)합니다[ WordPress](http://www.wordpress.com) 하 고 [Zendesk](https://www.zendesk.com/) 있지만 자세히에 대 한 지원을 추가 하는 것이 쉽습니다.

* 보내는 쪽에서 관리 및 구독자의 올바른 집합에 이벤트 알림을 보내는 경우와 구독을 저장 하기 위한 지원을 제공 합니다. 이 통해 사용자 고유의 이벤트 집합을 구독자가 구독 하 고 작업을 수행 하는 경우 사용자에 게 알릴 수를 정의할 수 있습니다.

두 부분 시나리오에 따라 분리 또는 함께 사용할 수 있습니다. 받는 사람 부분만;를 사용 하 여 다른 서비스에서 웹 후크를 수신 해야 하는 경우 사용할 다른 사용자에 대 한 웹 후크를 노출 하려는 경우 다음 수행할 수 있습니다는.

코드를 ASP.NET Web API 2 및 ASP.NET MVC 5를 대상으로 하 고이 제품은 [GitHub에서 OSS](https://github.com/aspnet/WebHooks)합니다.

## <a name="webhooks-overview"></a>웹 후크 개요

Webhook에는 해당 서비스에 서비스에서 사용 방법 다르지만 기본 개념은 동일 즉 패턴입니다. 생각할 수 있습니다 웹 후크의 간단한 pub/sub 모델을 사용자가 다른 곳에서 발생 하는 이벤트를 구독할 수 있는 합니다. 이벤트 알림은 이벤트 자체에 대 한 정보를 포함 하는 HTTP POST 요청으로 전파 됩니다.

일반적으로 HTTP POST 요청에는 JSON 개체 또는 HTML 양식 데이터를 트리거하는 WebHook를 유발 하는 이벤트에 대 한 정보를 포함 하 여 웹 후크 발신자가 결정이 포함 되어 있습니다. 예제에서 웹 후크 POST 요청 본문의 예를 들어 [GitHub](http://www.github.com/) 같습니다 특정 저장소에서 열린 새 문제를 결과로:

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

되도록 WebHook 실제로 의도 한 보낸 사람 으로부터, POST 요청을는 어떤 방식으로든에서 보호 되 고 그런 다음 수신자에 의해 확인 합니다. 예를 들어 [GitHub 웹 후크](https://developer.github.com/webhooks/) 포함을 *X-허브-서명* 걱정할 필요가 수신기 구현에서 확인 하는 요청 본문의 해시를 사용 하 여 HTTP 헤더입니다.

일반적으로 웹 후크 흐름을 다음과 같이 진행합니다.

* 웹 후크 발신자 클라이언트가 구독할 수 있는 이벤트를 노출 합니다. 이벤트 observable 변경 내용을 설명 시스템 예를 들어 된 새 데이터 항목을 삽입 하는 프로세스가 완료 되 면 또는 다른 항목이 있습니다.

* 웹 후크 수신기 네 가지 중 구성 된 웹 후크를 등록 하 여 구독:

     1. 여기서는 HTTP POST 요청의 형태로 이벤트 알림을 게시 해야 하는 것에 대 한 URI

     2. 웹 후크를 실행할지; 특정 이벤트를 설명 하는 필터 집합을

     3. HTTP POST 요청에 서명 하는 데 사용 되는 비밀 키

     4. HTTP POST 요청에 포함 하는 추가 데이터입니다. 예를 들어 추가 HTTP 헤더 필드 또는 속성 HTTP POST 요청 본문에 포함할 수 있습니다.

* 이벤트 발생 후 일치 하는 웹 후크 등록 검색 되 고 HTTP POST 요청 제출 됩니다. 일반적으로 HTTP POST 요청을 생성 하는 경우에 받는 사람이 응답 하지 않는 이유로 오류 응답에서 HTTP POST 요청 결과 여러 번 다시 시도 됩니다.

## <a name="webhooks-processing-pipeline"></a>웹 후크 처리 파이프라인

들어오는 웹 후크에 대 한 Microsoft ASP.NET 웹 후크 처리 파이프라인은 다음과 같습니다.

![웹 후크 ASP.NET 처리 파이프라인](_static/WebHookReceivers.png)

다음 두 가지 핵심 개념은 *수신자* 하 고 *처리기*:

* *수신기* 되도록 웹 후크 요청 실제로 의도 한 보낸 사람에 게 보안 검사를 적용 한 지정된 발신자에서 WebHook의 특정 버전을 처리 하는 것에 대 한 책임이 있습니다.

* *처리기* 는 일반적으로 사용자 코드 실행 특정 웹 후크를 처리 하는 위치입니다.

다음 노드가 이러한 개념 자세히 설명 합니다.
