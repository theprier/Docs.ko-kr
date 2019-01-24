---
title: ASP.NET Core SignalR .NET 클라이언트
author: bradygaster
description: ASP.NET Core SignalR .NET 클라이언트에 대한 정보
monikerRange: '>= aspnetcore-2.1'
ms.author: bradyg
ms.custom: mvc
ms.date: 09/10/2018
uid: signalr/dotnet-client
ms.openlocfilehash: 25b618f7a424b217c0fb55417754ea358280b95a
ms.sourcegitcommit: ebf4e5a7ca301af8494edf64f85d4a8deb61d641
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54836308"
---
# <a name="aspnet-core-signalr-net-client"></a><span data-ttu-id="a95dd-103">ASP.NET Core SignalR .NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="a95dd-103">ASP.NET Core SignalR .NET Client</span></span>

<span data-ttu-id="a95dd-104">ASP.NET Core SignalR .NET 클라이언트 라이브러리를 사용하면 .NET 앱에서 SignalR 허브와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-104">The ASP.NET Core SignalR .NET client library lets you communicate with SignalR hubs from .NET apps.</span></span>

> [!NOTE]
> <span data-ttu-id="a95dd-105">Xamarin에는 Visual Studio 버전에 대한 특별한 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-105">Xamarin has special requirements for Visual Studio version.</span></span> <span data-ttu-id="a95dd-106">자세한 내용은 [Xamarin과 SignalR 클라이언트 2.1.1](https://github.com/aspnet/Announcements/issues/305)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-106">For more information, see [SignalR Client 2.1.1 in Xamarin](https://github.com/aspnet/Announcements/issues/305).</span></span>

<span data-ttu-id="a95dd-107">[코드 샘플 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/dotnet-client/sample) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="a95dd-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/dotnet-client/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

<span data-ttu-id="a95dd-108">이 문서의 코드 샘플은 ASP.NET Core SignalR .NET 클라이언트를 사용하는 WPF 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-108">The code sample in this article is a WPF app that uses the ASP.NET Core SignalR .NET client.</span></span>

## <a name="install-the-signalr-net-client-package"></a><span data-ttu-id="a95dd-109">SignalR .NET 클라이언트 패키지 설치하기</span><span class="sxs-lookup"><span data-stu-id="a95dd-109">Install the SignalR .NET client package</span></span>

<span data-ttu-id="a95dd-110">.NET 클라이언트에서 SignalR 허브에 연결하려면 `Microsoft.AspNetCore.SignalR.Client` 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-110">The `Microsoft.AspNetCore.SignalR.Client` package is needed for .NET clients to connect to SignalR hubs.</span></span> <span data-ttu-id="a95dd-111">클라이언트 라이브러리를 설치하려면 **패키지 관리자 콘솔** 창에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-111">To install the client library, run the following command in the **Package Manager Console** window:</span></span>

```powershell
Install-Package Microsoft.AspNetCore.SignalR.Client
```

## <a name="connect-to-a-hub"></a><span data-ttu-id="a95dd-112">허브에 연결하기</span><span class="sxs-lookup"><span data-stu-id="a95dd-112">Connect to a hub</span></span>

<span data-ttu-id="a95dd-113">연결을 설정하려면 `HubConnectionBuilder`를 생성하고 `Build`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-113">To establish a connection, create a `HubConnectionBuilder` and call `Build`.</span></span> <span data-ttu-id="a95dd-114">연결을 만드는 동안 허브 URL, 프로토콜, 전송 형태, 로그 수준, 헤더 및 기타 옵션을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-114">The hub URL, protocol, transport type, log level, headers, and other options can be configured while building a connection.</span></span> <span data-ttu-id="a95dd-115">`HubConnectionBuilder` 메서드들 중 원하는 메서드를 `Build`에 삽입하여 필요한 모든 옵션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-115">Configure any required options by inserting any of the `HubConnectionBuilder` methods into `Build`.</span></span> <span data-ttu-id="a95dd-116">`StartAsync`를 사용하여 연결을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-116">Start the connection with `StartAsync`.</span></span>

[!code-csharp[Build hub connection](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_MainWindowClass&highlight=15-17,39)]

## <a name="handle-lost-connection"></a><span data-ttu-id="a95dd-117">연결 해제 처리하기</span><span class="sxs-lookup"><span data-stu-id="a95dd-117">Handle lost connection</span></span>

<span data-ttu-id="a95dd-118"><xref:Microsoft.AspNetCore.SignalR.Client.HubConnection.Closed> 이벤트를 이용해서 끊긴 연결에 대응합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-118">Use the <xref:Microsoft.AspNetCore.SignalR.Client.HubConnection.Closed> event to respond to a lost connection.</span></span> <span data-ttu-id="a95dd-119">예를 들어 자동으로 재연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-119">For example, you might want to automate reconnection.</span></span>

<span data-ttu-id="a95dd-120">`Closed` 이벤트에는 `async void`를 사용하지 않고 비동기 코드를 실행할 수 있는 `Task`를 반환하는 대리자가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-120">The `Closed` event requires a delegate that returns a `Task`, which allows async code to run without using `async void`.</span></span> <span data-ttu-id="a95dd-121">동기적으로 실행되는 `Closed` 이벤트 처리기에서 대리자의 시그니처를 만족시키려면 `Task.CompletedTask`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-121">To satisfy the delegate signature in a `Closed` event handler that runs synchronously, return `Task.CompletedTask`:</span></span>

```csharp
connection.Closed += (error) => {
    // Do your close logic.
    return Task.CompletedTask;
};
```

<span data-ttu-id="a95dd-122">비동기를 지원하는 가장 큰 이유는 연결을 다시 시작할 수도 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-122">The main reason for the async support is so you can restart the connection.</span></span> <span data-ttu-id="a95dd-123">연결 시작은 비동기 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-123">Starting a connection is an async action.</span></span>

<span data-ttu-id="a95dd-124">연결을 재시작하는 `Closed` 처리기에서는 다음 예제에서 볼 수 있는 것처럼 서버의 과부하를 방지할 수 있도록 임의의 지연 시간 동안 대기하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-124">In a `Closed` handler that restarts the connection, consider waiting for some random delay to prevent overloading the server, as shown in the following example:</span></span>

[!code-csharp[Use Closed event handler to automate reconnection](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_ClosedRestart)]

## <a name="call-hub-methods-from-client"></a><span data-ttu-id="a95dd-125">클라이언트에서 허브 메서드 호출하기</span><span class="sxs-lookup"><span data-stu-id="a95dd-125">Call hub methods from client</span></span>

<span data-ttu-id="a95dd-126">`InvokeAsync`는 허브 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-126">`InvokeAsync` calls methods on the hub.</span></span> <span data-ttu-id="a95dd-127">허브 메서드의 이름과 허브 메서드에 정의된 모든 인수를 `InvokeAsync`에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-127">Pass the hub method name and any arguments defined in the hub method to `InvokeAsync`.</span></span> <span data-ttu-id="a95dd-128">SignalR은 비동기로 동작하므로 호출 시 `async`와 `await`를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-128">SignalR is asynchronous, so use `async` and `await` when making the calls.</span></span>

[!code-csharp[InvokeAsync method](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_InvokeAsync)]

## <a name="call-client-methods-from-hub"></a><span data-ttu-id="a95dd-129">허브에서 클라이언트 메서드 호출하기</span><span class="sxs-lookup"><span data-stu-id="a95dd-129">Call client methods from hub</span></span>

<span data-ttu-id="a95dd-130">연결을 만든 다음, 그러나 연결을 시작하기 전에 `connection.On`을 이용해서 허브가 호출할 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-130">Define methods the hub calls using `connection.On` after building, but before starting the connection.</span></span>

[!code-csharp[Define client methods](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_ConnectionOn)]

<span data-ttu-id="a95dd-131">위의 `connection.On` 내부의 코드는 서버 쪽 코드에서 `SendAsync` 메서드를 사용하여 이 코드를 호출할 때 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-131">The preceding code in `connection.On` runs when server-side code calls it using the `SendAsync` method.</span></span>

[!code-csharp[Call client method](dotnet-client/sample/signalrchat/hubs/chathub.cs?name=snippet_SendMessage)]

## <a name="error-handling-and-logging"></a><span data-ttu-id="a95dd-132">오류 처리 및 로깅</span><span class="sxs-lookup"><span data-stu-id="a95dd-132">Error handling and logging</span></span>

<span data-ttu-id="a95dd-133">try-catch 문을 이용해서 오류를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-133">Handle errors with a try-catch statement.</span></span> <span data-ttu-id="a95dd-134">`Exception` 개체를 검사해서 오류가 발생한 후 수행할 적절한 동작을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="a95dd-134">Inspect the `Exception` object to determine the proper action to take after an error occurs.</span></span>

[!code-csharp[Logging](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_ErrorHandling)]

## <a name="additional-resources"></a><span data-ttu-id="a95dd-135">추가 자료</span><span class="sxs-lookup"><span data-stu-id="a95dd-135">Additional resources</span></span>

* [<span data-ttu-id="a95dd-136">허브</span><span class="sxs-lookup"><span data-stu-id="a95dd-136">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="a95dd-137">JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="a95dd-137">JavaScript client</span></span>](xref:signalr/javascript-client)
* [<span data-ttu-id="a95dd-138">Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="a95dd-138">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
