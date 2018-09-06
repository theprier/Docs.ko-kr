---
title: ASP.NET Core SignalR Java 클라이언트
author: mikaelm12
description: ASP.NET Core SignalR Java 클라이언트를 사용 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-2.2'
ms.author: mimengis
ms.custom: mvc
ms.date: 09/06/2018
uid: signalr/java-client
ms.openlocfilehash: f110f5391ac34f5cb4a72f64c16d86c8a37369a2
ms.sourcegitcommit: 4cd8dce371d63a66d780e4af1baab2bcf9d61b24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43995421"
---
# <a name="aspnet-core-signalr-java-client"></a><span data-ttu-id="fec2a-103">ASP.NET Core SignalR Java 클라이언트</span><span class="sxs-lookup"><span data-stu-id="fec2a-103">ASP.NET Core SignalR Java Client</span></span>

<span data-ttu-id="fec2a-104">[Mikael Mengistu](https://twitter.com/MikaelM_12)</span><span class="sxs-lookup"><span data-stu-id="fec2a-104">By [Mikael Mengistu](https://twitter.com/MikaelM_12)</span></span>

<span data-ttu-id="fec2a-105">Java 클라이언트 Android 앱을 포함 하 여 Java 코드에서 ASP.NET Core SignalR 서버에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-105">The Java client enables connecting to an ASP.NET Core SignalR server from Java code, including Android apps.</span></span> <span data-ttu-id="fec2a-106">같은 합니다 [JavaScript 클라이언트](xref:signalr/javascript-client) 하며 [.NET 클라이언트](xref:signalr/dotnet-client), Java 클라이언트를 사용 하면 실시간으로 허브에 메시지를 보내고 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-106">Like the [JavaScript client](xref:signalr/javascript-client) and the [.NET client](xref:signalr/dotnet-client), the Java client enables you to receive and send messages to a hub in real time.</span></span> <span data-ttu-id="fec2a-107">Java 클라이언트는 ASP.NET Core 2.2에서 사용할 수 있는 이상.</span><span class="sxs-lookup"><span data-stu-id="fec2a-107">The Java client is available in ASP.NET Core 2.2 and later.</span></span>

<span data-ttu-id="fec2a-108">이 문서에에서 나와 있는 샘플 Java 콘솔 앱 SignalR Java 클라이언트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-108">The sample Java console app referenced in this article uses the SignalR Java client.</span></span>

<span data-ttu-id="fec2a-109">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/java-client/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="fec2a-109">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/java-client/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="install-the-signalr-java-client-package"></a><span data-ttu-id="fec2a-110">SignalR Java 클라이언트 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-110">Install the SignalR Java client package</span></span>

<span data-ttu-id="fec2a-111">합니다 *signalr 0.1.0-preview1 35029* JAR 파일에는 클라이언트가 SignalR 허브에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-111">The *signalr-0.1.0-preview1-35029* JAR file allows clients to connect to SignalR hubs.</span></span> <span data-ttu-id="fec2a-112">최신 JAR 파일 버전 번호를 찾으려면 다음을 참조 합니다 [Maven 검색 결과](https://search.maven.org/search?q=g:com.microsoft.aspnet%20AND%20a:signalr&core=gav)합니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-112">To find the latest JAR file version number, see the [Maven search results](https://search.maven.org/search?q=g:com.microsoft.aspnet%20AND%20a:signalr&core=gav).</span></span>

<span data-ttu-id="fec2a-113">Gradle을 사용 하는 경우에 다음 줄을 추가 합니다 `dependencies` 의 섹션에 *build.gradle* 파일:</span><span class="sxs-lookup"><span data-stu-id="fec2a-113">If using Gradle, add the following line to the `dependencies` section of your *build.gradle* file:</span></span>

```gradle
implementation 'com.microsoft.aspnet:signalr:0.1.0-preview1-35029'
```

<span data-ttu-id="fec2a-114">Maven을 사용 하 여 내에 다음 줄을 추가 합니다 `<dependencies>` 의 요소에 *pom.xml* 파일:</span><span class="sxs-lookup"><span data-stu-id="fec2a-114">If using Maven, add the following lines inside the `<dependencies>` element of your *pom.xml* file:</span></span>

[!code-xml[pom.xml dependency element](java-client/sample/pom.xml?name=snippet_dependencyElement)]

## <a name="connect-to-a-hub"></a><span data-ttu-id="fec2a-115">허브에 연결</span><span class="sxs-lookup"><span data-stu-id="fec2a-115">Connect to a hub</span></span>

<span data-ttu-id="fec2a-116">설정 하는 `HubConnection`, `HubConnectionBuilder` 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-116">To establish a `HubConnection`, the `HubConnectionBuilder` should be used.</span></span> <span data-ttu-id="fec2a-117">허브 URL 및 로그 수준에 대 한 연결을 구축 하는 동안 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-117">The hub URL and log level can be configured while building a connection.</span></span> <span data-ttu-id="fec2a-118">중 하나를 호출 하 여 필요한 모든 옵션을 구성 합니다 `HubConnectionBuilder` 하기 전에 메서드 `build`합니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-118">Configure any required options by calling any of the `HubConnectionBuilder` methods before `build`.</span></span> <span data-ttu-id="fec2a-119">사용 하 여 연결을 시작할 `start`합니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-119">Start the connection with `start`.</span></span>

[!code-java[Build hub connection](java-client/sample/src/main/java/Chat.java?range=17-20)]

## <a name="call-hub-methods-from-client"></a><span data-ttu-id="fec2a-120">클라이언트에서 허브 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-120">Call hub methods from client</span></span>

<span data-ttu-id="fec2a-121">에 대 한 호출 `send` 허브 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-121">A call to `send` invokes a hub method.</span></span> <span data-ttu-id="fec2a-122">허브 메서드 이름 및 허브 메서드를 정의 하는 모든 인수를 전달 `send`합니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-122">Pass the hub method name and any arguments defined in the hub method to `send`.</span></span>

[!code-java[send method](java-client/sample/src/main/java/Chat.java?range=31)]

## <a name="call-client-methods-from-hub"></a><span data-ttu-id="fec2a-123">허브에서 클라이언트 메서드를 호출</span><span class="sxs-lookup"><span data-stu-id="fec2a-123">Call client methods from hub</span></span>

<span data-ttu-id="fec2a-124">사용 하 여 `hubConnection.on` 허브를 호출할 수 있는 클라이언트에서 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-124">Use `hubConnection.on` to define methods on the client that the hub can call.</span></span> <span data-ttu-id="fec2a-125">빌드 후 있지만 연결을 시작 하기 전에 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-125">Define the methods after building but before starting the connection.</span></span>

[!code-java[Define client methods](java-client/sample/src/main/java/Chat.java?range=22-24)]

## <a name="known-limitations"></a><span data-ttu-id="fec2a-126">알려진 제한 사항</span><span class="sxs-lookup"><span data-stu-id="fec2a-126">Known limitations</span></span>

<span data-ttu-id="fec2a-127">이 Java 클라이언트의 초기 미리 보기 릴리스입니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-127">This is an early preview release of the Java client.</span></span> <span data-ttu-id="fec2a-128">아직 지원 되지 않는 많은 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-128">There are many features that aren't supported yet.</span></span> <span data-ttu-id="fec2a-129">향후 릴리스에 대 한 다음 간격에 작업 중인:</span><span class="sxs-lookup"><span data-stu-id="fec2a-129">The following gaps are being worked on for future releases:</span></span>

* <span data-ttu-id="fec2a-130">기본 형식만 매개 변수로 사용할 수 및 반환 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-130">Only primitive types can be accepted as parameters and return types.</span></span>
* <span data-ttu-id="fec2a-131">Api는 동기입니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-131">The APIs are synchronous.</span></span>
* <span data-ttu-id="fec2a-132">이 이번에는 "송신" 호출 유형만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-132">Only the "Send" call type is supported at this time.</span></span> <span data-ttu-id="fec2a-133">"호출" 및 반환 값의 스트리밍 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-133">"Invoke" and streaming of return values aren't supported.</span></span>
* <span data-ttu-id="fec2a-134">클라이언트에서 현재 지원 하지 않습니다 합니다 [Azure SignalR Service](/azure/azure-signalr/)합니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-134">The client doesn't currently support the [Azure SignalR Service](/azure/azure-signalr/).</span></span>
* <span data-ttu-id="fec2a-135">JSON 프로토콜에만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-135">Only the JSON protocol is supported.</span></span>
* <span data-ttu-id="fec2a-136">Websocket 전송만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fec2a-136">Only the WebSockets transport is supported.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fec2a-137">추가 자료</span><span class="sxs-lookup"><span data-stu-id="fec2a-137">Additional resources</span></span>

* <xref:signalr/hubs>
* <xref:signalr/javascript-client>
* <xref:signalr/publish-to-azure-web-app>
