---
title: SignalR HubContext
author: tdykstra
description: 알림 허브를 외부 클라이언트에서 보내기를 ASP.NET Core SignalR HubContext 서비스를 사용 하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 06/13/2018
uid: signalr/hubcontext
ms.openlocfilehash: 6b955c2064d7d6a045594e56326e2f7df282675f
ms.sourcegitcommit: 3ca527f27c88cfc9d04688db5499e372fbc2c775
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39095309"
---
# <a name="send-messages-from-outside-a-hub"></a>허브를 외부에서 메시지 보내기

[Mikael Mengistu](https://twitter.com/MikaelM_12)

SignalR 허브는 SignalR 서버에 연결 하는 클라이언트에 메시지를 보내기 위한 핵심 추상화입니다. 사용 하 여 앱의 다른 위치에서 메시지를 보낼 수 이기도 합니다 `IHubContext` 서비스입니다. 이 문서는 SignalR에 액세스 하는 방법에 설명 `IHubContext` 허브 외부의 클라이언트에 알림을 보낼 수 있습니다.

[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubcontext/sample/) [(다운로드 하는 방법)](xref:tutorials/index#how-to-download-a-sample)

## <a name="get-an-instance-of-ihubcontext"></a>인스턴스 `IHubContext`

ASP.NET Core SignalR의 인스턴스에 액세스할 수 있습니다 `IHubContext` 종속성 주입을 통해. 인스턴스를 삽입할 수 있습니다 `IHubContext` 컨트롤러, 미들웨어 또는 다른 DI 서비스입니다. 클라이언트에 메시지를 보내는 인스턴스를 사용 합니다.

> [!NOTE]
> 이와 달리 GlobalHost를 액세스를 제공 하는 ASP.NET SignalR에서는 `IHubContext`합니다. ASP.NET Core는 전역이 단일 항목에 대 한 필요성을 제거 하는 종속성 주입 프레임 워크입니다.

### <a name="inject-an-instance-of-ihubcontext-in-a-controller"></a>인스턴스를 주입 `IHubContext` 컨트롤러에서

인스턴스를 삽입할 수 있습니다 `IHubContext` 생성자에 추가 하 여 컨트롤러:

[!code-csharp[IHubContext](hubcontext/sample/Controllers/HomeController.cs?range=12-19,57)]

인스턴스에 대 한 액세스를 사용 하 여 이제 `IHubContext`, 자체 허브에 것 처럼 허브 메서드를 호출할 수 있습니다.

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
> 외부에서 허브 메서드 호출 될 때를 `Hub` 클래스는 호출을 통해 연결 하는 호출자에 게 없습니다. 따라서이에 대 한 액세스는 `ConnectionId`, `Caller`, 및 `Others` 속성입니다.

## <a name="related-resources"></a>관련 참고 자료

* [시작](xref:tutorials/signalr)
* [허브](xref:signalr/hubs)
* [Azure에 게시](xref:signalr/publish-to-azure-web-app)
