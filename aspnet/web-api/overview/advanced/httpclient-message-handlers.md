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
msc.legacyurl: /web-api/overview/advanced/httpclient-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: 1712f190c5a313c79b7c91b671214dd8972cb3c9
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37402943"
---
<a name="httpclient-message-handlers-in-aspnet-web-api"></a>ASP.NET Web API의에서 HttpClient 메시지 처리기
====================
[Mike Wasson](https://github.com/MikeWasson)

A *메시지 처리기* 는 HTTP 요청을 수신 하 고 HTTP 응답을 반환 하는 클래스입니다.

일반적으로 일련의 메시지 처리기를 함께 연결 됩니다. HTTP 요청을 받고 일부 처리를 요청 다음 처리기를 제공 하는 첫 번째 처리기 합니다. 어느 시점에서 응답 생성 되 고 체인 돌아갑니다. 이 패턴은 호출을 *위임* 처리기입니다.

![](httpclient-message-handlers/_static/image1.png)

클라이언트 쪽에는 **HttpClient** 클래스 메시지 처리기를 사용 하 여 요청을 처리 합니다. 기본 처리기가 **HttpClientHandler**, 네트워크를 통해 요청을 보냅니다 있으며 서버에서 응답을 가져옵니다. 사용자 지정 메시지 처리기 클라이언트 파이프라인에 삽입할 수 있습니다.

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> ASP.NET Web API는 또한 서버 쪽에서 메시지 처리기를 사용합니다. 자세한 내용은 [HTTP 메시지 처리기](http-message-handlers.md)합니다.


## <a name="custom-message-handlers"></a>사용자 지정 메시지 처리기

파생 되는 사용자 지정 메시지 처리기를 작성 하려면 **System.Net.Http.DelegatingHandler** 재정의 **SendAsync** 메서드. 메서드 시그니처는 다음과 같습니다.

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

메서드는 **HttpRequestMessage** 입력 하 고 비동기적으로 반환은 **HttpResponseMessage**합니다. 일반적인 구현은 다음을 수행합니다.

1. 요청 메시지를 처리 합니다.
2. 호출 `base.SendAsync` 내부 처리기에는 요청을 보내야 합니다.
3. 내부 처리기는 응답 메시지를 반환 합니다. (이 단계는 비동기입니다.)
4. 응답을 처리 하 고 호출자에 게 반환 합니다.

다음 예제에서는 사용자 지정 헤더를 나가는 요청에 추가 하는 메시지 처리기를 보여 줍니다.

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

에 대 한 호출 `base.SendAsync` 은 비동기입니다. 이 호출 후에 모든 작업 수행 하는 처리기를 사용 합니다 **await** 메서드가 완료 된 후 실행을 다시 시작 하는 키워드입니다. 다음 예제에는 오류 코드를 기록 하는 처리기를 보여 줍니다. 자체 로깅 매우 흥미로운 이지만 예제에는 처리기 내에서 응답에 가져오는 방법을 보여 줍니다.

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a>클라이언트 파이프라인에 메시지 처리기 추가

사용자 지정 처리기를 추가할 **HttpClient**를 사용 합니다 **HttpClientFactory.Create** 메서드:

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

메시지 처리기로 전달 하는 순서로 호출 되는 **만들기** 메서드. 처리기가 중첩 되어 있으므로 응답 메시지는 반대 방향으로 이동 합니다. 마지막 처리기 즉, 첫 번째 응답 메시지를 가져옵니다.
