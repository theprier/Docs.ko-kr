---
title: ASP.NET Core SignalR .NET 클라이언트
author: tdykstra
description: ASP.NET Core SignalR .NET 클라이언트에 대한 정보
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 09/10/2018
uid: signalr/dotnet-client
ms.openlocfilehash: ef84ede2ed45ddc3b64d4ce8f5bd0018a681faf6
ms.sourcegitcommit: 4db337bd47d70c06fff91000c58bc048a491ccec
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2018
ms.locfileid: "44749323"
---
# <a name="aspnet-core-signalr-net-client"></a>ASP.NET Core SignalR .NET 클라이언트

ASP.NET Core SignalR .NET 클라이언트 라이브러리를 사용하면 .NET 앱에서 SignalR 허브와 통신할 수 있습니다.

> [!NOTE]
> Xamarin에는 Visual Studio 버전에 대한 특별한 요구 사항이 있습니다. 자세한 내용은 [Xamarin과 SignalR 클라이언트 2.1.1](https://github.com/aspnet/Announcements/issues/305)을 참고하시기 바랍니다.

[코드 샘플 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/dotnet-client/sample) ([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

이 문서의 코드 샘플은 ASP.NET Core SignalR .NET 클라이언트를 사용하는 WPF 앱입니다.

## <a name="install-the-signalr-net-client-package"></a>SignalR .NET 클라이언트 패키지 설치하기

.NET 클라이언트에서 SignalR 허브에 연결하려면 `Microsoft.AspNetCore.SignalR.Client` 패키지가 필요합니다. 클라이언트 라이브러리를 설치하려면 **패키지 관리자 콘솔** 창에서 다음 명령을 실행합니다.

```powershell
Install-Package Microsoft.AspNetCore.SignalR.Client
```

## <a name="connect-to-a-hub"></a>허브에 연결하기

연결을 설정하려면 `HubConnectionBuilder`를 생성하고 `Build`를 호출합니다. 연결을 만드는 동안 허브 URL, 프로토콜, 전송 형태, 로그 수준, 헤더 및 기타 옵션을 구성할 수 있습니다. `HubConnectionBuilder` 메서드들 중 원하는 메서드를 `Build`에 삽입하여 필요한 모든 옵션을 구성합니다. `StartAsync`를 사용하여 연결을 시작합니다.

[!code-csharp[Build hub connection](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_MainWindowClass&highlight=15-17,39)]

## <a name="handle-lost-connection"></a>연결 해제 처리하기

<xref:Microsoft.AspNetCore.SignalR.Client.HubConnection.Closed> 이벤트를 이용해서 끊긴 연결에 대응합니다. 예를 들어 자동으로 재연결할 수 있습니다.

`Closed` 이벤트에는 `async void`를 사용하지 않고 비동기 코드를 실행할 수 있는 `Task`를 반환하는 대리자가 필요합니다. 동기적으로 실행되는 `Closed` 이벤트 처리기에서 대리자의 시그니처를 만족시키려면 `Task.CompletedTask`를 반환합니다.

```csharp
connection.Closed += (error) => {
    // Do your close logic.
    return Task.CompletedTask;
};
```

비동기를 지원하는 가장 큰 이유는 연결을 다시 시작할 수도 있기 때문입니다. 연결 시작은 비동기 작업입니다.

연결을 재시작하는 `Closed` 처리기에서는 다음 예제에서 볼 수 있는 것처럼 서버의 과부하를 방지할 수 있도록 임의의 지연 시간 동안 대기하는 것이 좋습니다.

[!code-csharp[Use Closed event handler to automate reconnection](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_ClosedRestart)]

## <a name="call-hub-methods-from-client"></a>클라이언트에서 허브 메서드 호출하기

`InvokeAsync`는 허브 메서드를 호출합니다. 허브 메서드의 이름과 허브 메서드에 정의된 모든 인수를 `InvokeAsync`에 전달합니다. SignalR은 비동기로 동작하므로 호출 시 `async`와 `await`를 사용해야 합니다.

[!code-csharp[InvokeAsync method](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_InvokeAsync)]

## <a name="call-client-methods-from-hub"></a>허브에서 클라이언트 메서드 호출하기

연결을 만든 다음, 그러나 연결을 시작하기 전에 `connection.On`을 이용해서 허브가 호출할 메서드를 정의합니다.

[!code-csharp[Define client methods](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_ConnectionOn)]

위의 `connection.On` 내부의 코드는 서버 쪽 코드에서 `SendAsync` 메서드를 사용하여 이 코드를 호출할 때 실행됩니다.

[!code-csharp[Call client method](dotnet-client/sample/signalrchat/hubs/chathub.cs?name=snippet_SendMessage)]

## <a name="error-handling-and-logging"></a>오류 처리 및 로깅

try-catch 문을 이용해서 오류를 처리합니다. `Exception` 개체를 검사해서 오류가 발생한 후 수행할 적절한 동작을 결정합니다.

[!code-csharp[Logging](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_ErrorHandling)]

## <a name="additional-resources"></a>추가 자료

* [허브](xref:signalr/hubs)
* [JavaScript 클라이언트](xref:signalr/javascript-client)
* [Azure에 게시](xref:signalr/publish-to-azure-web-app)
