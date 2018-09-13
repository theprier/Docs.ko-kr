---
title: ASP.NET Core SignalR.NET 클라이언트
author: tdykstra
description: ASP.NET Core SignalR.NET 클라이언트에 대 한 정보
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
# <a name="aspnet-core-signalr-net-client"></a><span data-ttu-id="789eb-103">ASP.NET Core SignalR.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="789eb-103">ASP.NET Core SignalR .NET Client</span></span>

<span data-ttu-id="789eb-104">ASP.NET Core SignalR.NET 클라이언트 라이브러리를 사용 하면.NET 앱에서 SignalR 허브와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="789eb-104">The ASP.NET Core SignalR .NET client library lets you communicate with SignalR hubs from .NET apps.</span></span>

> [!NOTE]
> <span data-ttu-id="789eb-105">Xamarin에는 Visual Studio 버전에 대 한 특별 한 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="789eb-105">Xamarin has special requirements for Visual Studio version.</span></span> <span data-ttu-id="789eb-106">자세한 내용은 [Xamarin에서 SignalR 클라이언트 2.1.1](https://github.com/aspnet/Announcements/issues/305)합니다.</span><span class="sxs-lookup"><span data-stu-id="789eb-106">For more information, see [SignalR Client 2.1.1 in Xamarin](https://github.com/aspnet/Announcements/issues/305).</span></span>

<span data-ttu-id="789eb-107">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/dotnet-client/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="789eb-107">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/dotnet-client/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="789eb-108">이 문서의 코드 샘플은 ASP.NET Core SignalR.NET 클라이언트를 사용 하는 WPF 앱.</span><span class="sxs-lookup"><span data-stu-id="789eb-108">The code sample in this article is a WPF app that uses the ASP.NET Core SignalR .NET client.</span></span>

## <a name="install-the-signalr-net-client-package"></a><span data-ttu-id="789eb-109">SignalR.NET 클라이언트 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="789eb-109">Install the SignalR .NET client package</span></span>

<span data-ttu-id="789eb-110">`Microsoft.AspNetCore.SignalR.Client` SignalR 허브에 연결할.NET 클라이언트용 패키지가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="789eb-110">The `Microsoft.AspNetCore.SignalR.Client` package is needed for .NET clients to connect to SignalR hubs.</span></span> <span data-ttu-id="789eb-111">클라이언트 라이브러리를 설치 하려면에서 다음 명령을 실행 합니다 **패키지 관리자 콘솔** 창:</span><span class="sxs-lookup"><span data-stu-id="789eb-111">To install the client library, run the following command in the **Package Manager Console** window:</span></span>

```powershell
Install-Package Microsoft.AspNetCore.SignalR.Client
```

## <a name="connect-to-a-hub"></a><span data-ttu-id="789eb-112">허브에 연결</span><span class="sxs-lookup"><span data-stu-id="789eb-112">Connect to a hub</span></span>

<span data-ttu-id="789eb-113">연결을 설정 하려면 만듭니다는 `HubConnectionBuilder` 호출 `Build`합니다.</span><span class="sxs-lookup"><span data-stu-id="789eb-113">To establish a connection, create a `HubConnectionBuilder` and call `Build`.</span></span> <span data-ttu-id="789eb-114">연결을 만드는 동안 허브 URL, 프로토콜, 전송 종류, 로그 수준, 헤더 및 기타 옵션을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="789eb-114">The hub URL, protocol, transport type, log level, headers, and other options can be configured while building a connection.</span></span> <span data-ttu-id="789eb-115">중 하나를 삽입 하 여 필요한 모든 옵션을 구성 합니다 `HubConnectionBuilder` 메서드를 `Build`입니다.</span><span class="sxs-lookup"><span data-stu-id="789eb-115">Configure any required options by inserting any of the `HubConnectionBuilder` methods into `Build`.</span></span> <span data-ttu-id="789eb-116">사용 하 여 연결을 시작할 `StartAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="789eb-116">Start the connection with `StartAsync`.</span></span>

[!code-csharp[Build hub connection](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_MainWindowClass&highlight=15-17,39)]

## <a name="handle-lost-connection"></a><span data-ttu-id="789eb-117">연결 해제를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="789eb-117">Handle lost connection</span></span>

<span data-ttu-id="789eb-118">사용 된 <xref:Microsoft.AspNetCore.SignalR.Client.HubConnection.Closed> 끊긴된 연결에 응답 하는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="789eb-118">Use the <xref:Microsoft.AspNetCore.SignalR.Client.HubConnection.Closed> event to respond to a lost connection.</span></span> <span data-ttu-id="789eb-119">예를 들어, 다음 다시 연결을 자동화 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="789eb-119">For example, you might want to automate reconnection.</span></span>

<span data-ttu-id="789eb-120">`Closed` 반환 하는 대리자를 요구 하는 이벤트를 `Task`, 비동기 코드를 사용 하지 않고 실행할 수 있는 `async void`합니다.</span><span class="sxs-lookup"><span data-stu-id="789eb-120">The `Closed` event requires a delegate that returns a `Task`, which allows async code to run without using `async void`.</span></span> <span data-ttu-id="789eb-121">대리자 시그니처를 충족 하는 `Closed` 실행을 동기적으로 반환 하는 이벤트 처리기 `Task.CompletedTask`:</span><span class="sxs-lookup"><span data-stu-id="789eb-121">To satisfy the delegate signature in a `Closed` event handler that runs synchronously, return `Task.CompletedTask`:</span></span>

```csharp
connection.Closed += (error) => {
    // Do your close logic.
    return Task.CompletedTask;
};
```

<span data-ttu-id="789eb-122">비동기 지원에 대 한 주된 이유 이므로 연결을 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="789eb-122">The main reason for the async support is so you can restart the connection.</span></span> <span data-ttu-id="789eb-123">연결을 시작 하는 비동기 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="789eb-123">Starting a connection is an async action.</span></span>

<span data-ttu-id="789eb-124">에 `Closed` 연결을 다시 시작 하는 처리기는 다음 예와에서 같이 서버 오버 로드를 방지 하려면 임의의 지연 시간을 기다리는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="789eb-124">In a `Closed` handler that restarts the connection, consider waiting for some random delay to prevent overloading the server, as shown in the following example:</span></span>

[!code-csharp[Use Closed event handler to automate reconnection](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_ClosedRestart)]

## <a name="call-hub-methods-from-client"></a><span data-ttu-id="789eb-125">클라이언트에서 허브 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="789eb-125">Call hub methods from client</span></span>

<span data-ttu-id="789eb-126">`InvokeAsync` 허브 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="789eb-126">`InvokeAsync` calls methods on the hub.</span></span> <span data-ttu-id="789eb-127">허브 메서드 이름 및 허브 메서드를 정의 하는 모든 인수를 전달 `InvokeAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="789eb-127">Pass the hub method name and any arguments defined in the hub method to `InvokeAsync`.</span></span> <span data-ttu-id="789eb-128">SignalR은 비동기를 사용 하므로 `async` 및 `await` 호출 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="789eb-128">SignalR is asynchronous, so use `async` and `await` when making the calls.</span></span>

[!code-csharp[InvokeAsync method](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_InvokeAsync)]

## <a name="call-client-methods-from-hub"></a><span data-ttu-id="789eb-129">허브에서 클라이언트 메서드를 호출</span><span class="sxs-lookup"><span data-stu-id="789eb-129">Call client methods from hub</span></span>

<span data-ttu-id="789eb-130">허브를 사용 하 여 호출 하는 메서드를 정의 `connection.On` 을 빌드한 다음 있지만 연결을 시작 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="789eb-130">Define methods the hub calls using `connection.On` after building, but before starting the connection.</span></span>

[!code-csharp[Define client methods](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_ConnectionOn)]

<span data-ttu-id="789eb-131">위의 코드에서 `connection.On` 서버 쪽 코드를 사용 하 여 호출 될 때 실행 되는 `SendAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="789eb-131">The preceding code in `connection.On` runs when server-side code calls it using the `SendAsync` method.</span></span>

[!code-csharp[Call client method](dotnet-client/sample/signalrchat/hubs/chathub.cs?name=snippet_SendMessage)]

## <a name="error-handling-and-logging"></a><span data-ttu-id="789eb-132">오류 처리 및 로깅</span><span class="sxs-lookup"><span data-stu-id="789eb-132">Error handling and logging</span></span>

<span data-ttu-id="789eb-133">Try / catch 문 사용 하 여 오류를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="789eb-133">Handle errors with a try-catch statement.</span></span> <span data-ttu-id="789eb-134">검사는 `Exception` 오류가 발생 한 후 수행할 적절 한 작업을 결정 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="789eb-134">Inspect the `Exception` object to determine the proper action to take after an error occurs.</span></span>

[!code-csharp[Logging](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_ErrorHandling)]

## <a name="additional-resources"></a><span data-ttu-id="789eb-135">추가 자료</span><span class="sxs-lookup"><span data-stu-id="789eb-135">Additional resources</span></span>

* [<span data-ttu-id="789eb-136">허브</span><span class="sxs-lookup"><span data-stu-id="789eb-136">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="789eb-137">JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="789eb-137">JavaScript client</span></span>](xref:signalr/javascript-client)
* [<span data-ttu-id="789eb-138">Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="789eb-138">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
