---
uid: web-api/overview/advanced/http-message-handlers
title: ASP.NET Web API의에서 HTTP 메시지 처리기 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/13/2012
ms.topic: article
ms.assetid: 9002018b-3aa3-4358-bb1c-fbb5bc751d01
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/advanced/http-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: 931ad3330d5e4dc2424ab37b8a6e2a3d123a8684
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
ms.locfileid: "26506952"
---
<a name="http-message-handlers-in-aspnet-web-api"></a>ASP.NET Web API의에서 HTTP 메시지 처리기
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

A *메시지 처리기* 는 HTTP 요청을 수신 하 고 HTTP 응답을 반환 하는 클래스입니다. Abstract에서 파생 되는 메시지 처리기 **HttpMessageHandler** 클래스입니다.

일반적으로 일련의 메시지 처리기 함께 연결 됩니다. 첫 번째 처리기 HTTP 요청을 수신 하 고, 일부 처리를, 다음 처리기에 요청을 제공 합니다. 어느 시점 부터는 응답 생성 되 고 체인 돌아갑니다. 이 패턴 라고는 *위임* 처리기입니다.

![](http-message-handlers/_static/image1.png)

## <a name="server-side-message-handlers"></a>서버 쪽 메시지 처리기

서버 쪽에서 Web API 파이프라인 몇 가지 기본 제공 메시지 처리기를 사용합니다.

- **HttpServer** 호스트에서 요청을 가져옵니다.
- **HttpRoutingDispatcher** 경로에 따라 요청을 전달 합니다.
- **HttpControllerDispatcher** Web API 컨트롤러에 요청을 전송 합니다.

사용자 지정 처리기를 파이프라인에 추가할 수 있습니다. 메시지 처리기는 HTTP 메시지 (아니라 컨트롤러 작업)의 수준에서 작동 하는 일반적인 문제에 대 한 유용 합니다. 예를 들어 메시지 처리기 않을 수 있습니다.

- 읽기 또는 요청 헤더를 수정 합니다.
- 응답 헤더를 응답에 추가 합니다.
- 컨트롤러에 도달 하기 전에 요청의 유효성을 검사 합니다.

이 다이어그램에서는 파이프라인에 삽입 하는 두 명의 사용자 지정 처리기를 보여 줍니다.

![](http-message-handlers/_static/image2.png)

> [!NOTE]
> 클라이언트 쪽에서 HttpClient도 메시지 처리기를 사용합니다. 자세한 내용은 참조 [HttpClient 메시지 처리기](httpclient-message-handlers.md)합니다.


## <a name="custom-message-handlers"></a>사용자 지정 메시지 처리기

파생 한 사용자 지정 메시지 처리기를 작성 하려면 **System.Net.Http.DelegatingHandler** 재정의 **SendAsync** 메서드. 이 메서드의 서명은 다음과 같습니다.

[!code-csharp[Main](http-message-handlers/samples/sample1.cs)]

메서드를 사용 하며는 **HttpRequestMessage** 으로 입력 하 고 비동기적으로 반환 된 **HttpResponseMessage**합니다. 일반적인 구현은 다음을 수행합니다.

1. 요청 메시지를 처리 합니다.
2. 호출 `base.SendAsync` 내부 처리기에 요청을 보낼 수 있습니다.
3. 내부 처리기는 응답 메시지를 반환 합니다. (이 단계는 비동기.)
4. 응답을 처리 하 고 호출자에 게 반환 합니다.

간단한 예는 다음과 같습니다.

[!code-csharp[Main](http-message-handlers/samples/sample2.cs)]

> [!NOTE]
> 에 대 한 호출 `base.SendAsync` 비동기적입니다. 처리기는이 호출 후에 모든 작업을 수행 하는 경우 사용 하 여는 **await** 키워드를 표시 된 것 처럼 합니다.


위임 처리기 내부 처리기를 건너뛸 수도 및 응답을 직접 만들 수 있습니다.

[!code-csharp[Main](http-message-handlers/samples/sample3.cs)]

처리기를 호출 하지 않고 응답 만듭니다는 위임 하는 경우 `base.SendAsync`, 요청 파이프라인의 나머지 부분을 건너뜁니다. 이 (오류 응답이 생성) 요청의 유효성을 검사 하는 처리기에 대 한 유용할 수 있습니다.

![](http-message-handlers/_static/image3.png)

## <a name="adding-a-handler-to-the-pipeline"></a>파이프라인에 처리기를 추가합니다.

서버 쪽에서 메시지 처리기를 추가 하려면 처리기에 추가 된 **HttpConfiguration.MessageHandlers** 컬렉션입니다. "ASP.NET MVC 4 웹 응용 프로그램" 템플릿을 사용 하는 프로젝트를 만드는 경우에이 내부를 수행할 수 있습니다는 **경우 WebApiConfig** 클래스:

[!code-csharp[Main](http-message-handlers/samples/sample4.cs)]

에 표시 되는 순서 대로 메시지 처리기가 호출 **MessageHandlers** 컬렉션입니다. 중첩 되어 있으므로 응답 메시지는 반대 방향으로 이동 됩니다. 마지막 처리기 즉, 가장 먼저 응답 메시지를 가져옵니다.

내부 처리기;를 설정 하려면 필요 하지 않습니다 Web API 프레임 워크의 메시지 처리기를 자동으로 연결합니다.

있다면 [자체 호스팅](../older-versions/self-host-a-web-api.md)의 인스턴스를 만들는 **HttpSelfHostConfiguration** 클래스 처리기를 추가 하 고는 **MessageHandlers** 컬렉션입니다.

[!code-csharp[Main](http-message-handlers/samples/sample5.cs)]

이제 사용자 지정 메시지 처리기의 몇 가지 예를 살펴보겠습니다.

## <a name="example-x-http-method-override"></a>예: X-HTTP-메서드-재정

HTTP 메서드 재정의 X는 비표준 HTTP 헤더입니다. PUT 또는 DELETE와 같은 특정 HTTP 요청 형식을 보낼 수 없는 클라이언트에 대 한 설계 되었습니다. 대신, 클라이언트 POST 요청을 보내고 HTTP 메서드 재정의 X 헤더 원하는 메서드를 설정 합니다. 예:

[!code-console[Main](http-message-handlers/samples/sample6.cmd)]

HTTP 메서드 재정의 X에 대 한 지원을 추가 하는 메시지 처리기는 다음과 같습니다.

[!code-csharp[Main](http-message-handlers/samples/sample7.cs)]

에 **SendAsync** 요청 메시지는 POST 요청 인지 및 HTTP 메서드 재정의 X 헤더 포함 여부 메서드를 처리기를 확인 합니다. 이 경우 헤더 값의 유효성을 검사 하며 요청 메서드를 수정 합니다. 처리기가 호출 하는 마지막으로, `base.SendAsync` 다음 처리기에는 메시지를 전달 하도록 합니다.

요청에 도달 하면는 **HttpControllerDispatcher** 클래스 **HttpControllerDispatcher** 업데이트 요청 방법에 따라 요청을 라우팅합니다.

## <a name="example-adding-a-custom-response-header"></a>예: 사용자 지정 응답 헤더 추가

모든 응답 메시지에 사용자 지정 헤더를 추가 하는 메시지 처리기는 다음과 같습니다.

[!code-csharp[Main](http-message-handlers/samples/sample8.cs)]

첫째, 처리기가 호출 `base.SendAsync` 내부 메시지 처리기 요청을 전달 하도록 합니다. 내부 처리기는 응답 메시지를 반환 하지만 매우 비동기적으로 사용 하 여 수행 된 **작업&lt;T&gt;**  개체입니다. 응답 메시지를 때까지 사용할 수 없으면 `base.SendAsync` 비동기적으로 완료 합니다.

사용 하 여이 예제는 **await** 작업을 수행 하는 키워드 비동기적으로 `SendAsync` 완료 합니다. .NET Framework 4.0을 대상으로 하는 경우 사용 하 여는 **작업**&lt;T&gt;**합니다. ContinueWith** 메서드:

[!code-csharp[Main](http-message-handlers/samples/sample9.cs)]

## <a name="example-checking-for-an-api-key"></a>예: API 키에 대 한 검사

일부 웹 서비스 요청에 API 키를 포함 하려면 클라이언트가 필요 합니다. 다음 예제에서는 메시지 처리기 수 올바른 API 키에 대 한 요청을 확인 하는 방법을 보여 줍니다.

[!code-csharp[Main](http-message-handlers/samples/sample10.cs)]

이 처리기는 URI 쿼리 문자열의 API 키를 찾습니다. (이 예에서는 라고 가정 키는 정적 문자열입니다. 실제 구현 사용 보다 복잡 한 유효성 검사 합니다.) 쿼리 문자열 키를 포함 하는 경우 처리기 내부 처리기에 요청을 전달 합니다.

처리기의 상태 403, 응답 메시지를 만듭니다 요청에 유효한 키를 찾을 수 없는 경우 사용할 수 없음. 이 경우 처리기가 호출 하지 않으면 `base.SendAsync`, 내부 처리기를 받지 요청 하므로 하지도 컨트롤러 않습니다. 따라서 컨트롤러 들어오는 모든 요청에 올바른 API 키가 있는지 가정할 수 있습니다.

> [!NOTE]
> API 키는 특정 컨트롤러 작업에만 적용 되는 경우에 작업 필터를 사용 하 여 메시지 처리기를 대신 하는 것이 좋습니다. 작업 필터 URI 라우팅을 수행 된 후 실행 합니다.


## <a name="per-route-message-handlers"></a>경로 당 메시지 처리기

처리기에는 **HttpConfiguration.MessageHandlers** 컬렉션 전체적으로 적용 합니다.

또는 경로 정의 하는 경우 특정 경로에 메시지 처리기를 추가할 수 있습니다.

[!code-csharp[Main](http-message-handlers/samples/sample11.cs?highlight=16)]

이 예제에서는 요청 URI "Route2" 일치 하는 경우 요청에 디스패치 됩니다 `MessageHandler2`합니다. 다음 다이어그램에서는이 두 경로 대 한 파이프라인을 보여 줍니다.

![](http-message-handlers/_static/image4.png)

다음에 유의 `MessageHandler2` 기본 바꿉니다 **HttpControllerDispatcher**합니다. 이 예제에서는 `MessageHandler2` 응답을 만들고 컨트롤러를로 이동 하지 "Route2"와 일치 하는 요청입니다. 이렇게 하면 사용자 고유의 사용자 지정 끝점 전체 Web API 컨트롤러 메커니즘을 바꿉니다.

경로 당 메시지 처리기를 위임할 수 또는 **HttpControllerDispatcher**, 컨트롤러에 전달 합니다.

![](http-message-handlers/_static/image5.png)

다음 코드에는이 경로 구성 하는 방법을 보여 줍니다.

[!code-csharp[Main](http-message-handlers/samples/sample12.cs)]
