---
uid: webhooks/receiving/receivers
title: ASP.NET Webhook 수신기 | Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook 수신기
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/17/2012
ms.topic: article
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.technology: ''
ms.prod: .net-framework
ms.openlocfilehash: a8e42521f201f88b0ed433550e8786411b4487b0
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30896298"
---
# <a name="aspnet-webhooks-receivers"></a>ASP.NET Webhook 수신기

Webhook을 받는 보낸 사람에 게에 따라 다릅니다. 경우에 따라 구독자 실제로 수신 대기를 확인 하 여 webhook을 사용할지를 등록 하는 추가 단계가 있습니다. 일부 Webhook이를 독립적으로 검색할 이벤트 정보에 대 한 참조에 HTTP POST 요청만 포함 하는 푸시 풀 모델을 제공 합니다. 종종 보안 모델은 다소 달라 집니다.

Microsoft ASP.NET Webhook의 용도 모두 쉽고 간단 하 게 많은 Webhook의 특정 변형을 처리 하는 방법을 파악 하는 시간을 소비 하지 않고 사용자가 API를 연결 하는 보다 일관 된 것입니다.

WebHook 수신기가 수락 하 고 특정 보낸에서 Webhook을 확인 하는 일을 담당 합니다. WebHook 수신기 개수에 관계 없이 각각 고유한 구성을 Webhook 지원할 수 있습니다. 예를 들어 GitHub WebHook 수신기 GitHub 리포지토리에의 다양 한 Webhook을 사용할 수 있습니다.

## <a name="webhook-receiver-uris"></a>WebHook 수신기 Uri

Microsoft ASP.NET Webhook을 설치 하 여 WebHook 요청 개방형 개수의 서비스에서 허용 하는 일반 WebHook 컨트롤러를 얻을 수 있습니다. 요청이 도착 하면 사용자가 설치한 특정 WebHook 보낸 사람을 처리 하기 위한 적절 한 받는 사람을 선택 합니다.

이 컨트롤러의 URI는 서비스에 등록 하는 WebHook uri와 형식은:

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

보안상의 이유로 많은 WebHook 수신기를 사용 하려면 URI는 *https* URI 및 일부 경우에도 포함 해야 하는 의도 된 파티 위의 URI에 Webhook을 보낼 수에 적용 하는 데 사용 되는 추가 쿼리 매개 변수 .

<em> <receiver> </em> 구성 요소는 수신기의 이름 예를 들어 <em>github</em> 또는 <em>slack</em>합니다.

*{id}* 특정 WebHook 수신기 구성을 식별 하는 데 사용할 수 있는 선택적 식별자입니다. N Webhook 특정 수신기를 등록 데 될 수 있습니다. 예를 들어 3 개의 독립적인 Webhook에 대 한 등록 하는 다음 세 가지 Uri는 사용할 수 있습니다.:

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a>WebHook 수신기 설치

Microsoft ASP.NET Webhook을 사용 하 여 Webhook을 받으려면 먼저 WebHook 공급자나 Webhook에서 수신 하려는 공급자에 대 한 Nuget 패키지를 설치 합니다. Nuget 패키지 [Microsoft.AspNet.WebHooks.Receivers.*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) 여기서 마지막 부분에 지원 되는 서비스를 나타냅니다. 예

[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) GitHub에서 Webhook을 수신 하기 위한 지원을 제공 하 고 [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) ASP에 의해 생성 된 Webhook을 수신 하기 위한 지원을 제공 합니다. NET Webhook 합니다.

즉시 Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, 여유 시간, Stripe, Trello, 및 WordPress에 대 한 지원을 찾을 수 있습니다 하지만 개수에 관계 없이 다른 공급자를 지원 하기 위해 가능 합니다.

## <a name="configuring-a-webhook-receiver"></a>WebHook 수신기 구성

WebHook 수신기를 통해 구성 되는 [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) 인터페이스와 해당 인터페이스의 특정 구현을 등록할 수 있습니다는 종속성 주입 모델을 사용 하 여 합니다. 기본 구현에서는 Web.config 파일에서 설정할 수 있습니다 또는 Azure 웹 앱을 사용 하는 경우를 통해 설정할 수 있는 응용 프로그램 설정을 사용 하 여는 [Azure 포털](https://portal.azure.com/)합니다.

![Azure 앱 설정](_static/AzureAppSettings.png)

응용 프로그램 설정 키에 대 한 형식은 다음과 같습니다.

```
MS_WebHookReceiverSecret_<receiver>
```

값은 일치 하는 값의 쉼표로 구분 된 목록에서 *{id}* 는 대 한 Webhook 등록 된, 예를 들어 값:

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a>WebHook 수신기를 초기화합니다.

WebHook 수신기에서, 일반적으로 등록 하 여 초기화 되는 *경우 WebApiConfig* 정적 클래스:

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
