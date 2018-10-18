---
title: SignalR HubContext
author: tdykstra
description: ASP.NET Core SignalR HubContext 서비스를 사용해서 허브의 외부에서 클라이언트에 알림을 전송하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 06/13/2018
uid: signalr/hubcontext
ms.openlocfilehash: bb07a3b5c6e153092635fa4e1283619777865a53
ms.sourcegitcommit: 4bdf7703aed86ebd56b9b4bae9ad5700002af32d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2018
ms.locfileid: "49325356"
---
# <a name="send-messages-from-outside-a-hub"></a>허브 외부에서 메시지 전송하기

작성자: [Mikael Mengistu](https://twitter.com/MikaelM_12)

SignalR 허브는 SignalR 서버에 연결하는 클라이언트에 메시지를 전송하기 위한 핵심 추상화입니다. `IHubContext` 서비스를 이용해서 앱의 다른 위치에서 메시지를 전송할 수도 있습니다. 이 문서에서는 클라이언트로 알림을 전송하기 위해 허브의 외부에서 SignalR `IHubContext`에 접근하는 방법을 설명합니다.

[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubcontext/sample/) [(다운로드 방법)](xref:tutorials/index#how-to-download-a-sample)

## <a name="get-an-instance-of-ihubcontext"></a>`IHubContext` 인스턴스 가져오기

ASP.NET Core SignalR에서는 종속성 주입을 통해서 `IHubContext`의 인스턴스에 접근할 수 있습니다. 컨트롤러, 미들웨어 또는 다른 DI 서비스에 `IHubContext`의 인스턴스를 삽입할 수 있습니다. 이 인스턴스를 사용해서 클라이언트에 메시지를 전송합니다.

> [!NOTE]
> 이 점이 `IHubContext`에 대한 접근을 제공하기 위해 GlobalHost를 사용하는 ASP.NET 4.x SignalR과 다른 부분입니다. ASP.NET Core는 이런 전역 싱글톤이 필요 없는 종속성 주입 프레임워크를 갖고 있습니다.

### <a name="inject-an-instance-of-ihubcontext-in-a-controller"></a>컨트롤러에서 `IHubContext` 인스턴스 주입하기

생성자에 `IHubContext`를 추가하여 컨트롤러에 인스턴스를 주입할 수 있습니다.

[!code-csharp[IHubContext](hubcontext/sample/Controllers/HomeController.cs?range=12-19,57)]

이제 `IHubContext`의 인스턴스를 사용해서 허브 자체에 위치한 것처럼 허브 메서드를 호출할 수 있습니다.

[!code-csharp[IHubContext](hubcontext/sample/Controllers/HomeController.cs?range=21-25)]

### <a name="get-an-instance-of-ihubcontext-in-middleware"></a>미들웨어에서 `IHubContext` 인스턴스 가져오기

미들웨어 파이프라인 내부에서는 다음과 같이 `IHubContext`에 접근합니다.

```csharp
app.Use(next => async (context) =>
{
    var hubContext = context.RequestServices
                            .GetRequiredService<IHubContext<MyHub>>();
    //...
});
```

> [!NOTE]
> 허브 메서드가 `Hub` 클래스의 외부에서 호출되는 경우에는 해당 호출에 대한 호출자가 존재하지 않습니다. 따라서 `ConnectionId`, `Caller` 및 `Others` 속성에는 접근할 수 없습니다.

## <a name="related-resources"></a>관련 자료

* [시작하기](xref:tutorials/signalr)
* [허브](xref:signalr/hubs)
* [Azure에 게시하기](xref:signalr/publish-to-azure-web-app)
