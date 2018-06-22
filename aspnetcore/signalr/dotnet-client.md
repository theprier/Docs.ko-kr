---
title: ASP.NET Core SignalR.NET 클라이언트
author: rachelappel
description: ASP.NET Core SignalR.NET 클라이언트에 대 한 정보
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 05/29/2018
uid: signalr/dotnet-client
ms.openlocfilehash: faa4368988971a3e7fcdcd1b044971e16d70f19a
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36273297"
---
# <a name="aspnet-core-signalr-net-client"></a>ASP.NET Core SignalR.NET 클라이언트

작성자: [Rachel Appel](http://twitter.com/rachelappel)

Xamarin, WPF, Windows Forms, 콘솔 및.NET Core 응용 프로그램에서 ASP.NET Core SignalR.NET 클라이언트를 사용할 수 있습니다. 마찬가지로 [JavaScript 클라이언트](xref:signalr/javascript-client),.NET 클라이언트를 사용 하면 수신 하 고 보내고 실시간으로 허브에 메시지를 받을 수 있습니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/dotnet-client/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

이 문서의 코드 예제는 ASP.NET Core SignalR.NET 클라이언트를 사용 하는 WPF 앱.

## <a name="install-the-signalr-net-client-package"></a>SignalR.NET 클라이언트 패키지를 설치 합니다.

`Microsoft.AspNetCore.SignalR.Client` SignalR 허브에 연결 하는.NET 클라이언트에 대 한 패키지가 필요 합니다. 클라이언트 라이브러리를 설치 하려면에서 다음 명령을 실행의 **패키지 관리자 콘솔** 창:

```powershell
Install-Package Microsoft.AspNetCore.SignalR.Client
```

## <a name="connect-to-a-hub"></a>허브에 연결

연결을 설정 하려면 만듭니다는 `HubConnectionBuilder` 호출 `Build`합니다. 연결을 구성 하는 동안 허브 URL, 프로토콜, 전송 종류, 로그 수준, 헤더 및 기타 옵션을 구성할 수 있습니다. 필수 옵션 중 하나를 삽입 하 여 구성 된 `HubConnectionBuilder` 에 메서드 `Build`합니다. 사용 하 여 연결 시작 `StartAsync`합니다.

[!code-csharp[Build hub connection](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?highlight=15-17,33)]

## <a name="call-hub-methods-from-client"></a>클라이언트에서 허브 메서드를 호출 합니다.

`InvokeAsync` 허브에서 메서드를 호출합니다. 허브 메서드 이름 및 허브 메서드를 정의 하는 인수를 전달 `InvokeAsync`합니다. SignalR은 비동기, 따라서 사용 `async` 및 `await` 호출 하는 경우.

[!code-csharp[InvokeAsync method](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?range=48-49)]

## <a name="call-client-methods-from-hub"></a>허브에서 클라이언트를 메서드 호출

허브를 사용 하 여 호출 하는 메서드를 정의 `connection.On` 을 빌드한 다음 하지만 연결을 시작 하기 전에.

[!code-csharp[Define client methods](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?range=22-29)]

위의 코드에서 `connection.On` 서버 쪽 코드를 사용 하 여 호출할 때 실행 되는 `SendAsync` 메서드.

[!code-csharp[Call client method](dotnet-client/sample/signalrchat/hubs/chathub.cs?range=8-11)]

## <a name="error-handling-and-logging"></a>오류 처리 및 로깅

Try / catch 문 사용 하 여 오류 처리 합니다. 검사는 `Exception` 오류가 발생 한 후 수행할 적절 한 작업을 결정 하는 개체입니다.

[!code-csharp[Logging](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?range=46-54)]

## <a name="additional-resources"></a>추가 자료

* [허브](xref:signalr/hubs)
* [JavaScript 클라이언트](xref:signalr/javascript-client)
* [Azure에 게시](xref:signalr/publish-to-azure-web-app)