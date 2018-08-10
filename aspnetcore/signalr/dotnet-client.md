---
title: ASP.NET Core SignalR.NET 클라이언트
author: tdykstra
description: ASP.NET Core SignalR.NET 클라이언트에 대 한 정보
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 08/07/2018
uid: signalr/dotnet-client
ms.openlocfilehash: 970888a410b2486a20f98ce77a8674f8ec357f50
ms.sourcegitcommit: 028ad28c546de706ace98066c76774de33e4ad20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39655254"
---
# <a name="aspnet-core-signalr-net-client"></a><span data-ttu-id="6ae64-103">ASP.NET Core SignalR.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="6ae64-103">ASP.NET Core SignalR .NET Client</span></span>

<span data-ttu-id="6ae64-104">작성자: [Rachel Appel](http://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="6ae64-104">By [Rachel Appel](http://twitter.com/rachelappel)</span></span>

<span data-ttu-id="6ae64-105">Xamarin, WPF, Windows Forms, 콘솔 및.NET Core 앱에서 ASP.NET Core SignalR.NET 클라이언트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ae64-105">The ASP.NET Core SignalR .NET client can be used by Xamarin, WPF, Windows Forms, Console, and .NET Core apps.</span></span> <span data-ttu-id="6ae64-106">같은 합니다 [JavaScript 클라이언트](xref:signalr/javascript-client),.NET 클라이언트를 사용 하면 수신 및 송신 및 실시간으로 허브에 메시지를 수신 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae64-106">Like the [JavaScript client](xref:signalr/javascript-client), the .NET client enables you to receive and send and receive messages to a hub in real time.</span></span>

> [!NOTE]
> <span data-ttu-id="6ae64-107">Xamarin에는 Visual Studio 버전에 대 한 특별 한 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ae64-107">Xamarin has special requirements for Visual Studio version.</span></span> <span data-ttu-id="6ae64-108">자세한 내용은 [Xamarin에서 SignalR 클라이언트 2.1.1](https://github.com/aspnet/Announcements/issues/305)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae64-108">For more information, see [SignalR Client 2.1.1 in Xamarin](https://github.com/aspnet/Announcements/issues/305).</span></span>

<span data-ttu-id="6ae64-109">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/dotnet-client/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="6ae64-109">[View or download sample code](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/dotnet-client/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="6ae64-110">이 문서의 코드 샘플은 ASP.NET Core SignalR.NET 클라이언트를 사용 하는 WPF 앱.</span><span class="sxs-lookup"><span data-stu-id="6ae64-110">The code sample in this article is a WPF app that uses the ASP.NET Core SignalR .NET client.</span></span>

## <a name="install-the-signalr-net-client-package"></a><span data-ttu-id="6ae64-111">SignalR.NET 클라이언트 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae64-111">Install the SignalR .NET client package</span></span>

<span data-ttu-id="6ae64-112">`Microsoft.AspNetCore.SignalR.Client` SignalR 허브에 연결할.NET 클라이언트용 패키지가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae64-112">The `Microsoft.AspNetCore.SignalR.Client` package is needed for .NET clients to connect to SignalR hubs.</span></span> <span data-ttu-id="6ae64-113">클라이언트 라이브러리를 설치 하려면에서 다음 명령을 실행 합니다 **패키지 관리자 콘솔** 창:</span><span class="sxs-lookup"><span data-stu-id="6ae64-113">To install the client library, run the following command in the **Package Manager Console** window:</span></span>

```powershell
Install-Package Microsoft.AspNetCore.SignalR.Client
```

## <a name="connect-to-a-hub"></a><span data-ttu-id="6ae64-114">허브에 연결</span><span class="sxs-lookup"><span data-stu-id="6ae64-114">Connect to a hub</span></span>

<span data-ttu-id="6ae64-115">연결을 설정 하려면 만듭니다는 `HubConnectionBuilder` 호출 `Build`합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae64-115">To establish a connection, create a `HubConnectionBuilder` and call `Build`.</span></span> <span data-ttu-id="6ae64-116">연결을 만드는 동안 허브 URL, 프로토콜, 전송 종류, 로그 수준, 헤더 및 기타 옵션을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ae64-116">The hub URL, protocol, transport type, log level, headers, and other options can be configured while building a connection.</span></span> <span data-ttu-id="6ae64-117">중 하나를 삽입 하 여 필요한 모든 옵션을 구성 합니다 `HubConnectionBuilder` 메서드를 `Build`입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae64-117">Configure any required options by inserting any of the `HubConnectionBuilder` methods into `Build`.</span></span> <span data-ttu-id="6ae64-118">사용 하 여 연결을 시작할 `StartAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae64-118">Start the connection with `StartAsync`.</span></span>

[!code-csharp[Build hub connection](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?highlight=15-17,33)]

## <a name="call-hub-methods-from-client"></a><span data-ttu-id="6ae64-119">클라이언트에서 허브 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae64-119">Call hub methods from client</span></span>

<span data-ttu-id="6ae64-120">`InvokeAsync` 허브 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae64-120">`InvokeAsync` calls methods on the hub.</span></span> <span data-ttu-id="6ae64-121">허브 메서드 이름 및 허브 메서드를 정의 하는 모든 인수를 전달 `InvokeAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae64-121">Pass the hub method name and any arguments defined in the hub method to `InvokeAsync`.</span></span> <span data-ttu-id="6ae64-122">SignalR은 비동기를 사용 하므로 `async` 및 `await` 호출 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="6ae64-122">SignalR is asynchronous, so use `async` and `await` when making the calls.</span></span>

[!code-csharp[InvokeAsync method](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?range=48-49)]

## <a name="call-client-methods-from-hub"></a><span data-ttu-id="6ae64-123">허브에서 클라이언트 메서드를 호출</span><span class="sxs-lookup"><span data-stu-id="6ae64-123">Call client methods from hub</span></span>

<span data-ttu-id="6ae64-124">허브를 사용 하 여 호출 하는 메서드를 정의 `connection.On` 을 빌드한 다음 있지만 연결을 시작 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae64-124">Define methods the hub calls using `connection.On` after building, but before starting the connection.</span></span>

[!code-csharp[Define client methods](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?range=22-29)]

<span data-ttu-id="6ae64-125">위의 코드에서 `connection.On` 서버 쪽 코드를 사용 하 여 호출 될 때 실행 되는 `SendAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="6ae64-125">The preceding code in `connection.On` runs when server-side code calls it using the `SendAsync` method.</span></span>

[!code-csharp[Call client method](dotnet-client/sample/signalrchat/hubs/chathub.cs?range=8-11)]

## <a name="error-handling-and-logging"></a><span data-ttu-id="6ae64-126">오류 처리 및 로깅</span><span class="sxs-lookup"><span data-stu-id="6ae64-126">Error handling and logging</span></span>

<span data-ttu-id="6ae64-127">Try / catch 문 사용 하 여 오류를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae64-127">Handle errors with a try-catch statement.</span></span> <span data-ttu-id="6ae64-128">검사는 `Exception` 오류가 발생 한 후 수행할 적절 한 작업을 결정 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae64-128">Inspect the `Exception` object to determine the proper action to take after an error occurs.</span></span>

[!code-csharp[Logging](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?range=46-54)]

## <a name="additional-resources"></a><span data-ttu-id="6ae64-129">추가 자료</span><span class="sxs-lookup"><span data-stu-id="6ae64-129">Additional resources</span></span>

* [<span data-ttu-id="6ae64-130">허브</span><span class="sxs-lookup"><span data-stu-id="6ae64-130">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="6ae64-131">JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="6ae64-131">JavaScript client</span></span>](xref:signalr/javascript-client)
* [<span data-ttu-id="6ae64-132">Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="6ae64-132">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
