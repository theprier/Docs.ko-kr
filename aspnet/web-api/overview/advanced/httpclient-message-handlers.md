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
<a name="httpclient-message-handlers-in-aspnet-web-api"></a>ASP.NET Web API의에서 HttpClient 메시지 처리기
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

A *메시지 처리기* 는 HTTP 요청을 수신 하 고 HTTP 응답을 반환 하는 클래스입니다.

일반적으로 일련의 메시지 처리기 함께 연결 됩니다. 첫 번째 처리기 HTTP 요청을 수신 하 고, 일부 처리를, 다음 처리기에 요청을 제공 합니다. 어느 시점 부터는 응답 생성 되 고 체인 돌아갑니다. 이 패턴 라고는 *위임* 처리기입니다.

![](httpclient-message-handlers/_static/image1.png)

클라이언트 쪽에서의 **HttpClient** 클래스 메시지 처리기를 사용 하 여 요청을 처리 합니다. 기본 처리기가 **HttpClientHandler**, 네트워크를 통해 요청을 전송 하 고 서버에서 응답을 가져옵니다. 사용자 지정 메시지 처리기 클라이언트 파이프라인에 삽입할 수 있습니다.

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> 또한 ASP.NET Web API는 서버 쪽에서 메시지 처리기를 사용합니다. 자세한 내용은 참조 [HTTP 메시지 처리기](http-message-handlers.md)합니다.


## <a name="custom-message-handlers"></a>사용자 지정 메시지 처리기

파생 한 사용자 지정 메시지 처리기를 작성 하려면 **System.Net.Http.DelegatingHandler** 재정의 **SendAsync** 메서드. 메서드 시그니처는 다음과 같습니다.

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

메서드를 사용 하며는 **HttpRequestMessage** 으로 입력 하 고 비동기적으로 반환 된 **HttpResponseMessage**합니다. 일반적인 구현은 다음을 수행합니다.

1. 요청 메시지를 처리 합니다.
2. 호출 `base.SendAsync` 내부 처리기에 요청을 보낼 수 있습니다.
3. 내부 처리기는 응답 메시지를 반환 합니다. (이 단계는 비동기.)
4. 응답을 처리 하 고 호출자에 게 반환 합니다.

다음 예제에서는 보내는 요청에 사용자 지정 헤더를 추가 하는 메시지 처리기를 보여 줍니다.

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

에 대 한 호출 `base.SendAsync` 비동기적입니다. 처리기는이 호출 후에 모든 작업을 수행 하는 경우 사용 하 여는 **await** 키워드를 메서드가 완료 된 후 실행을 다시 시작 합니다. 다음 예제에서는 오류 코드를 기록 하는 처리기를 보여 줍니다. 자체 로깅 그다지 흥미로 워 보이지 않습니다. 하지만 예제에서는 응답 처리기 내에서 가져오는 방법을 보여 줍니다.

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a>클라이언트 파이프라인에 메시지 처리기 추가

사용자 지정 처리기를 추가 하려면 **HttpClient**를 사용 하 여는 **HttpClientFactory.Create** 메서드:

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

메시지 처리기로 전달 하는 순서로 호출 됩니다는 **만들기** 메서드. 처리기가 중첩 때문에 응답 메시지는 반대 방향으로 이동 됩니다. 마지막 처리기 즉, 가장 먼저 응답 메시지를 가져옵니다.
