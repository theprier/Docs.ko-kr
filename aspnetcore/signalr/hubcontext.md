---
title: SignalR HubContext
author: rachelappel
description: 알림 허브를 외부에서 클라이언트를 보내기 위한 ASP.NET Core SignalR HubContext 서비스를 사용 하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 06/13/2018
uid: signalr/hubcontext
ms.openlocfilehash: ccfcdc8337275fd26e09c1a43db36cf9ab90cf46
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36277763"
---
# <a name="send-messages-from-outside-a-hub"></a>허브 외부의 메시지 보내기

으로 [Mikael Mengistu](https://twitter.com/MikaelM_12)

SignalR 허브는 SignalR 서버에 연결 된 클라이언트에 메시지를 보내기 위한 핵심 추상화입니다. 사용 하 여 앱의 다른 위치에서 메시지를 보낼 수 이기도 `IHubContext` 서비스입니다. 이 문서는 SignalR에 액세스 하는 방법에 설명 `IHubContext` 허브 외부에서 클라이언트에 알림을 보낼 수 있습니다.

[보거나 다운로드 샘플 코드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubcontext/sample/) [(다운로드 하는 방법)](xref:tutorials/index#how-to-download-a-sample)

## <a name="get-an-instance-of-ihubcontext"></a>인스턴스를 가져옵니다 `IHubContext`

ASP.NET Core SignalR의 인스턴스를 액세스할 수 있습니다 `IHubContext` 종속성 주입을 통해. 인스턴스를 삽입할 수 `IHubContext` 는 컨트롤러, 미들웨어, 또는 기타 DI 서비스입니다. 메시지를 보내는 클라이언트에 인스턴스를 사용 합니다.

> [!NOTE]
> 이와 달리 ASP.NET signalr에 대 한 액세스를 제공 하기 위해 GlobalHost를 사용 하는 `IHubContext`합니다. ASP.NET Core 전역이 단일 항목에 대 한 필요성을 제거 하는 종속성 주입 프레임 워크를 있습니다.

### <a name="inject-an-instance-of-ihubcontext-in-a-controller"></a>인스턴스를 삽입할 `IHubContext` 컨트롤러

인스턴스를 삽입할 수 `IHubContext` 생성자를 추가 하 여 컨트롤러에:

[!code-csharp[IHubContext](hubcontext/sample/Controllers/HomeController.cs?range=12-19,57)]

인스턴스에 액세스할 수 있는 이제 `IHubContext`, 허브 자체에 있던 마치 허브 메서드를 호출할 수 있습니다.

[!code-csharp[IHubContext](hubcontext/sample/Controllers/HomeController.cs?range=21-25)]

### <a name="get-an-instance-of-ihubcontext-in-middleware"></a>인스턴스를 가져올 `IHubContext` 미들웨어에서

액세스는 `IHubContext` 미들웨어 파이프라인 내에서 다음과 같이 합니다.

```csharp
app.Use(next => (context) =>
{
    var hubContext = (IHubContext<MyHub>)context
                        .RequestServices
                        .GetServices<IHubContext<MyHub>>();
    //...
});
```

> [!NOTE]
> 외부에서 허브 메서드 호출 될 때는 `Hub` 클래스, 호출와 연결 된 호출자는 합니다. 따라서이에 대 한 액세스는 `ConnectionId`, `Caller`, 및 `Others` 속성입니다.

## <a name="related-resources"></a>관련 참고 자료

* [시작](xref:tutorials/signalr)
* [허브](xref:signalr/hubs)
* [Azure에 게시](xref:signalr/publish-to-azure-web-app)
