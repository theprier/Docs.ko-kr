---
title: ASP.NET Core SignalR Java 클라이언트
author: mikaelm12
description: ASP.NET Core SignalR Java 클라이언트를 사용 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-2.2'
ms.author: mimengis
ms.custom: mvc
ms.date: 10/18/2018
uid: signalr/java-client
ms.openlocfilehash: 77ea338f08b1986e69ba8ef1578c4cfe01a310de
ms.sourcegitcommit: ce6b6792c650708e92cdea051a5d166c0708c7c0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49652308"
---
# <a name="aspnet-core-signalr-java-client"></a><span data-ttu-id="fd642-103">ASP.NET Core SignalR Java 클라이언트</span><span class="sxs-lookup"><span data-stu-id="fd642-103">ASP.NET Core SignalR Java client</span></span>

<span data-ttu-id="fd642-104">작성자: [Mikael Mengistu](https://twitter.com/MikaelM_12)</span><span class="sxs-lookup"><span data-stu-id="fd642-104">By [Mikael Mengistu](https://twitter.com/MikaelM_12)</span></span>

<span data-ttu-id="fd642-105">Java 클라이언트 Android 앱을 포함 하 여 Java 코드에서 ASP.NET Core SignalR 서버에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-105">The Java client enables connecting to an ASP.NET Core SignalR server from Java code, including Android apps.</span></span> <span data-ttu-id="fd642-106">같은 합니다 [JavaScript 클라이언트](xref:signalr/javascript-client) 하며 [.NET 클라이언트](xref:signalr/dotnet-client), Java 클라이언트를 사용 하면 실시간으로 허브에 메시지를 보내고 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-106">Like the [JavaScript client](xref:signalr/javascript-client) and the [.NET client](xref:signalr/dotnet-client), the Java client enables you to receive and send messages to a hub in real time.</span></span> <span data-ttu-id="fd642-107">Java 클라이언트는 ASP.NET Core 2.2에서 사용할 수 있는 이상.</span><span class="sxs-lookup"><span data-stu-id="fd642-107">The Java client is available in ASP.NET Core 2.2 and later.</span></span>

<span data-ttu-id="fd642-108">이 문서에에서 나와 있는 샘플 Java 콘솔 앱 SignalR Java 클라이언트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-108">The sample Java console app referenced in this article uses the SignalR Java client.</span></span>

<span data-ttu-id="fd642-109">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/java-client/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="fd642-109">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/java-client/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="install-the-signalr-java-client-package"></a><span data-ttu-id="fd642-110">SignalR Java 클라이언트 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-110">Install the SignalR Java client package</span></span>

<span data-ttu-id="fd642-111">합니다 *signalr 1.0.0-preview3 35501* JAR 파일에는 클라이언트가 SignalR 허브에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-111">The *signalr-1.0.0-preview3-35501* JAR file allows clients to connect to SignalR hubs.</span></span> <span data-ttu-id="fd642-112">최신 JAR 파일 버전 번호를 찾으려면 다음을 참조 합니다 [Maven 검색 결과](https://search.maven.org/search?q=g:com.microsoft.signalr%20AND%20a:signalr)합니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-112">To find the latest JAR file version number, see the [Maven search results](https://search.maven.org/search?q=g:com.microsoft.signalr%20AND%20a:signalr).</span></span>

<span data-ttu-id="fd642-113">Gradle을 사용 하는 경우에 다음 줄을 추가 합니다 `dependencies` 의 섹션에 *build.gradle* 파일:</span><span class="sxs-lookup"><span data-stu-id="fd642-113">If using Gradle, add the following line to the `dependencies` section of your *build.gradle* file:</span></span>

```gradle
implementation 'com.microsoft.signalr:signalr:1.0.0-preview3-35501'
implementation 'io.reactivex.rxjava2:rxjava:2.2.2'
```

<span data-ttu-id="fd642-114">Maven을 사용 하 여 내에 다음 줄을 추가 합니다 `<dependencies>` 의 요소에 *pom.xml* 파일:</span><span class="sxs-lookup"><span data-stu-id="fd642-114">If using Maven, add the following lines inside the `<dependencies>` element of your *pom.xml* file:</span></span>

[!code-xml[pom.xml dependency element](java-client/sample/pom.xml?name=snippet_dependencyElement)]

## <a name="connect-to-a-hub"></a><span data-ttu-id="fd642-115">허브에 연결</span><span class="sxs-lookup"><span data-stu-id="fd642-115">Connect to a hub</span></span>

<span data-ttu-id="fd642-116">설정 하는 `HubConnection`, `HubConnectionBuilder` 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-116">To establish a `HubConnection`, the `HubConnectionBuilder` should be used.</span></span> <span data-ttu-id="fd642-117">허브 URL 및 로그 수준에 대 한 연결을 구축 하는 동안 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-117">The hub URL and log level can be configured while building a connection.</span></span> <span data-ttu-id="fd642-118">중 하나를 호출 하 여 필요한 모든 옵션을 구성 합니다 `HubConnectionBuilder` 하기 전에 메서드 `build`합니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-118">Configure any required options by calling any of the `HubConnectionBuilder` methods before `build`.</span></span> <span data-ttu-id="fd642-119">사용 하 여 연결을 시작할 `start`합니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-119">Start the connection with `start`.</span></span>

[!code-java[Build hub connection](java-client/sample/src/main/java/Chat.java?range=16-17)]

## <a name="call-hub-methods-from-client"></a><span data-ttu-id="fd642-120">클라이언트에서 허브 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-120">Call hub methods from client</span></span>

<span data-ttu-id="fd642-121">에 대 한 호출 `send` 허브 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-121">A call to `send` invokes a hub method.</span></span> <span data-ttu-id="fd642-122">허브 메서드 이름 및 허브 메서드를 정의 하는 모든 인수를 전달 `send`합니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-122">Pass the hub method name and any arguments defined in the hub method to `send`.</span></span>

[!code-java[send method](java-client/sample/src/main/java/Chat.java?range=28)]

## <a name="call-client-methods-from-hub"></a><span data-ttu-id="fd642-123">허브에서 클라이언트 메서드를 호출</span><span class="sxs-lookup"><span data-stu-id="fd642-123">Call client methods from hub</span></span>

<span data-ttu-id="fd642-124">사용 하 여 `hubConnection.on` 허브를 호출할 수 있는 클라이언트에서 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-124">Use `hubConnection.on` to define methods on the client that the hub can call.</span></span> <span data-ttu-id="fd642-125">빌드 후 있지만 연결을 시작 하기 전에 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-125">Define the methods after building but before starting the connection.</span></span>

[!code-java[Define client methods](java-client/sample/src/main/java/Chat.java?range=19-21)]

## <a name="add-logging"></a><span data-ttu-id="fd642-126">로깅 추가</span><span class="sxs-lookup"><span data-stu-id="fd642-126">Add logging</span></span>

<span data-ttu-id="fd642-127">SignalR Java 클라이언트를 사용 하 여 [SLF4J](https://www.slf4j.org/) 로깅에 대 한 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-127">The SignalR Java client uses the [SLF4J](https://www.slf4j.org/) library for logging.</span></span> <span data-ttu-id="fd642-128">라이브러리의 사용자가 자신의 특정 로깅 구현을 특정 로깅 종속성에서 전환 하 여 선택한 수 있는 높은 수준의 로깅 API입니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-128">It's a high-level logging API that allows users of the library to chose their own specific logging implementation by bringing in a specific logging dependency.</span></span> <span data-ttu-id="fd642-129">다음 코드 조각을 사용 하는 방법을 보여 줍니다 `java.util.logging` SignalR Java 클라이언트를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-129">The following code snippet shows how to use `java.util.logging` with the SignalR Java client.</span></span>

```gradle
implementation 'org.slf4j:slf4j-jdk14:1.7.25'
```

<span data-ttu-id="fd642-130">종속성에 대 한 로깅을 구성 하지 않으면, SLF4J 다음 경고 메시지를 사용 하 여 기본 작업 없음로 거를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-130">If you don't configure logging in your dependencies, SLF4J loads a default no-operation logger with the following warning message:</span></span>

```
SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
SLF4J: Defaulting to no-operation (NOP) logger implementation
SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
```

<span data-ttu-id="fd642-131">이 안전 하 게 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-131">This can safely be ignored.</span></span>

## <a name="known-limitations"></a><span data-ttu-id="fd642-132">알려진 제한 사항</span><span class="sxs-lookup"><span data-stu-id="fd642-132">Known limitations</span></span>

<span data-ttu-id="fd642-133">이 Java 클라이언트의 미리 보기 릴리스입니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-133">This is a preview release of the Java client.</span></span> <span data-ttu-id="fd642-134">일부 기능은 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-134">Some features aren't supported:</span></span>

* <span data-ttu-id="fd642-135">JSON 프로토콜에만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-135">Only the JSON protocol is supported.</span></span>
* <span data-ttu-id="fd642-136">Websocket 전송만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-136">Only the WebSockets transport is supported.</span></span>
* <span data-ttu-id="fd642-137">스트리밍 아직 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd642-137">Streaming isn't supported yet.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fd642-138">추가 자료</span><span class="sxs-lookup"><span data-stu-id="fd642-138">Additional resources</span></span>

* [<span data-ttu-id="fd642-139">Java API 참조</span><span class="sxs-lookup"><span data-stu-id="fd642-139">Java API reference</span></span>](/java/api/com.microsoft.aspnet.signalr?view=aspnet-signalr-java)
* <xref:signalr/hubs>
* <xref:signalr/javascript-client>
* <xref:signalr/publish-to-azure-web-app>
