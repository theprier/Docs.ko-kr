---
title: ASP.NET Core SignalR JavaScript 클라이언트
author: tdykstra
description: ASP.NET Core SignalR JavaScript 클라이언트의 개요입니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 08/14/2018
uid: signalr/javascript-client
ms.openlocfilehash: 10958c414aa4a285c8a2810bb99e278f719c5b7f
ms.sourcegitcommit: ce6b6792c650708e92cdea051a5d166c0708c7c0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "46483051"
---
# <a name="aspnet-core-signalr-javascript-client"></a><span data-ttu-id="22df6-103">ASP.NET Core SignalR JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="22df6-103">ASP.NET Core SignalR JavaScript client</span></span>

<span data-ttu-id="22df6-104">작성자: [Rachel Appel](http://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="22df6-104">By [Rachel Appel](http://twitter.com/rachelappel)</span></span>

<span data-ttu-id="22df6-105">ASP.NET Core SignalR JavaScript 클라이언트 라이브러리를 사용하면 서버 쪽 허브 코드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-105">The ASP.NET Core SignalR JavaScript client library enables developers to call server-side hub code.</span></span>

<span data-ttu-id="22df6-106">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/javascript-client/sample) ([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="22df6-106">[View or download sample code](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/javascript-client/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="install-the-signalr-client-package"></a><span data-ttu-id="22df6-107">SignalR 클라이언트 패키지 설치하기</span><span class="sxs-lookup"><span data-stu-id="22df6-107">Install the SignalR client package</span></span>

<span data-ttu-id="22df6-108">SignalR JavaScript 클라이언트 라이브러리는 [npm](https://www.npmjs.com/) 패키지로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-108">The SignalR JavaScript client library is delivered as an [npm](https://www.npmjs.com/) package.</span></span> <span data-ttu-id="22df6-109">Visual Studio를 사용하고 있다면 **패키지 관리자 콘솔**의 루트 폴더에서 `npm install`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-109">If you're using Visual Studio, run `npm install` from the **Package Manager Console** while in the root folder.</span></span> <span data-ttu-id="22df6-110">Visual Studio Code에서는 **통합 터미널**에서 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-110">For Visual Studio Code, run the command from the **Integrated Terminal**.</span></span>

  ```console
  npm init -y
  npm install @aspnet/signalr
  ```

<span data-ttu-id="22df6-111">npm에서 패키지 콘텐츠를 설치 합니다 *node_modules\\@aspnet\signalr\dist\browser* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-111">npm installs the package contents in the *node_modules\\@aspnet\signalr\dist\browser* folder.</span></span> <span data-ttu-id="22df6-112">라는 새 폴더를 만듭니다 *signalr* 아래의 합니다 *wwwroot\\lib* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-112">Create a new folder named *signalr* under the *wwwroot\\lib* folder.</span></span> <span data-ttu-id="22df6-113">복사 합니다 *signalr.js* 파일을 합니다 *wwwroot\lib\signalr* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-113">Copy the *signalr.js* file to the *wwwroot\lib\signalr* folder.</span></span>

## <a name="use-the-signalr-javascript-client"></a><span data-ttu-id="22df6-114">SignalR JavaScript 클라이언트 사용하기</span><span class="sxs-lookup"><span data-stu-id="22df6-114">Use the SignalR JavaScript client</span></span>

<span data-ttu-id="22df6-115">`<script>` 요소를 이용해서 SignalR JavaScript 클라이언트를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-115">Reference the SignalR JavaScript client in the `<script>` element.</span></span>

```html
<script src="~/lib/signalr/signalr.js"></script>
```

## <a name="connect-to-a-hub"></a><span data-ttu-id="22df6-116">허브에 연결하기</span><span class="sxs-lookup"><span data-stu-id="22df6-116">Connect to a hub</span></span>

<span data-ttu-id="22df6-117">다음 코드는 연결을 만들고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-117">The following code creates and starts a connection.</span></span> <span data-ttu-id="22df6-118">허브의 이름은 대소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-118">The hub's name is case insensitive.</span></span>

[!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=9-12,28)]

### <a name="cross-origin-connections"></a><span data-ttu-id="22df6-119">원본 간 연결</span><span class="sxs-lookup"><span data-stu-id="22df6-119">Cross-origin connections</span></span>

<span data-ttu-id="22df6-120">일반적으로 브라우저는 요청된 페이지와 동일한 도메인에서 연결을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-120">Typically, browsers load connections from the same domain as the requested page.</span></span> <span data-ttu-id="22df6-121">그러나 다른 도메인에 연결해야 하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-121">However, there are occasions when a connection to another domain is required.</span></span>

<span data-ttu-id="22df6-122">악의적인 사이트가 다른 사이트의 민감한 데이터를 읽지 못하게 막기 위해서, 기본적으로 [원본 간 연결](xref:security/cors)은 비활성화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-122">To prevent a malicious site from reading sensitive data from another site, [cross-origin connections](xref:security/cors) are disabled by default.</span></span> <span data-ttu-id="22df6-123">원본 간 요청을 허용하려면 `Startup` 클래스에서 이를 활성화하십시오.</span><span class="sxs-lookup"><span data-stu-id="22df6-123">To allow a cross-origin request, enable it in the `Startup` class.</span></span>

[!code-csharp[Cross-origin connections](javascript-client/sample/Startup.cs?highlight=29-35,56)]

## <a name="call-hub-methods-from-client"></a><span data-ttu-id="22df6-124">클라이언트에서 허브 메서드 호출하기</span><span class="sxs-lookup"><span data-stu-id="22df6-124">Call hub methods from client</span></span>

<span data-ttu-id="22df6-125">JavaScript 클라이언트는 [HubConnection](/javascript/api/%40aspnet/signalr/hubconnection)의 [invoke](/javascript/api/%40aspnet/signalr/hubconnection#invoke) 메서드를 통해서 허브의 public 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-125">JavaScript clients call public methods on hubs via the [invoke](/javascript/api/%40aspnet/signalr/hubconnection#invoke) method of the [HubConnection](/javascript/api/%40aspnet/signalr/hubconnection).</span></span> <span data-ttu-id="22df6-126">이 `invoke` 메서드는 두 가지 인수를 전달 받습니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-126">The `invoke` method accepts two arguments:</span></span>

* <span data-ttu-id="22df6-127">허브 메서드의 이름.</span><span class="sxs-lookup"><span data-stu-id="22df6-127">The name of the hub method.</span></span> <span data-ttu-id="22df6-128">다음 예제에서 허브 메서드의 이름은 `SendMessage`입니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-128">In the following example, the method name on the hub is `SendMessage`.</span></span>
* <span data-ttu-id="22df6-129">허브 메서드에 정의된 모든 인수.</span><span class="sxs-lookup"><span data-stu-id="22df6-129">Any arguments defined in the hub method.</span></span> <span data-ttu-id="22df6-130">다음 예제에서 인수의 이름은 `message`입니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-130">In the following example, the argument name is `message`.</span></span>

  [!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=24)]

## <a name="call-client-methods-from-hub"></a><span data-ttu-id="22df6-131">허브에서 클라이언트 메서드 호출하기</span><span class="sxs-lookup"><span data-stu-id="22df6-131">Call client methods from hub</span></span>

<span data-ttu-id="22df6-132">허브에서 메시지를 수신하려면 `HubConnection`의 [on](/javascript/api/%40aspnet/signalr/hubconnection#on) 메서드를 이용해서 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-132">To receive messages from the hub, define a method using the [on](/javascript/api/%40aspnet/signalr/hubconnection#on) method of the `HubConnection`.</span></span>

* <span data-ttu-id="22df6-133">JavaScript 클라이언트 메서드의 이름.</span><span class="sxs-lookup"><span data-stu-id="22df6-133">The name of the JavaScript client method.</span></span> <span data-ttu-id="22df6-134">다음 예제에서 메서드 이름은 `ReceiveMessage`입니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-134">In the following example, the method name is `ReceiveMessage`.</span></span>
* <span data-ttu-id="22df6-135">허브에서 메서드로 전달될 인수.</span><span class="sxs-lookup"><span data-stu-id="22df6-135">Arguments the hub passes to the method.</span></span> <span data-ttu-id="22df6-136">다음 예제에서 인수의 이름은 `message`입니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-136">In the following example, the argument value is `message`.</span></span>

[!code-javascript[Receive calls from hub](javascript-client/sample/wwwroot/js/chat.js?range=14-19)]

<span data-ttu-id="22df6-137">위의 `connection.on` 내부의 코드는 서버 쪽 코드에서 [SendAsync](/dotnet/api/microsoft.aspnetcore.signalr.clientproxyextensions.sendasync) 메서드를 사용하여 이 코드를 호출할 때 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-137">The preceding code in `connection.on` runs when server-side code calls it using the [SendAsync](/dotnet/api/microsoft.aspnetcore.signalr.clientproxyextensions.sendasync) method.</span></span>

[!code-csharp[Call client-side](javascript-client/sample/hubs/chathub.cs?range=8-11)]

<span data-ttu-id="22df6-138">SignalR은 `SendAsync`와 `connection.on`에 정의된 메서드 이름과 인수가 일치하는지 검사하여 호출할 클라이언트 메서드를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-138">SignalR determines which client method to call by matching the method name and arguments defined in `SendAsync` and `connection.on`.</span></span>

> [!NOTE]
> <span data-ttu-id="22df6-139">권장되는 방식은 `on` 메서드를 호출한 후 `HubConnection`의 [start](/javascript/api/%40aspnet/signalr/hubconnection#start) 메서드를 호출하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-139">As a best practice, call the [start](/javascript/api/%40aspnet/signalr/hubconnection#start) method on the `HubConnection` after `on`.</span></span> <span data-ttu-id="22df6-140">이렇게 하면 메시지가 수신되기 전에 처리기가 먼저 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-140">Doing so ensures your handlers are registered before any messages are received.</span></span>

## <a name="error-handling-and-logging"></a><span data-ttu-id="22df6-141">오류 처리 및 로깅</span><span class="sxs-lookup"><span data-stu-id="22df6-141">Error handling and logging</span></span>

<span data-ttu-id="22df6-142">클라이언트 쪽 오류를 처리하려면 `catch` 메서드를 `start` 메서드 끝에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-142">Chain a `catch` method to the end of the `start` method to handle client-side errors.</span></span> <span data-ttu-id="22df6-143">브라우저의 콘솔에 오류를 출력하려면 `console.error`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-143">Use `console.error` to output errors to the browser's console.</span></span>

[!code-javascript[Error handling](javascript-client/sample/wwwroot/js/chat.js?range=28)]

<span data-ttu-id="22df6-144">연결이 만들어지면 로거와 기록할 이벤트 유형을 전달하여 클라이언트 쪽 로그 추적을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-144">Setup client-side log tracing by passing a logger and type of event to log when the connection is made.</span></span> <span data-ttu-id="22df6-145">지정한 로그 수준 이상의 메시지가 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-145">Messages are logged with the specified log level and higher.</span></span> <span data-ttu-id="22df6-146">사용 가능한 로그 수준은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-146">Available log levels are as follows:</span></span>

* <span data-ttu-id="22df6-147">`signalR.LogLevel.Error` &ndash; 오류 메시지.</span><span class="sxs-lookup"><span data-stu-id="22df6-147">`signalR.LogLevel.Error` &ndash; Error messages.</span></span> <span data-ttu-id="22df6-148">`Error` 메시지만 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-148">Logs `Error` messages only.</span></span>
* <span data-ttu-id="22df6-149">`signalR.LogLevel.Warning` &ndash; 잠재적 오류에 대한 경고 메시지.</span><span class="sxs-lookup"><span data-stu-id="22df6-149">`signalR.LogLevel.Warning` &ndash; Warning messages about potential errors.</span></span> <span data-ttu-id="22df6-150">`Warning` 및 `Error` 메시지를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-150">Logs `Warning`, and `Error` messages.</span></span>
* <span data-ttu-id="22df6-151">`signalR.LogLevel.Information` &ndash; 오류가 아닌 상태 메시지.</span><span class="sxs-lookup"><span data-stu-id="22df6-151">`signalR.LogLevel.Information` &ndash; Status messages without errors.</span></span> <span data-ttu-id="22df6-152">`Information`, `Warning` 및 `Error` 메시지를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-152">Logs `Information`, `Warning`, and `Error` messages.</span></span>
* <span data-ttu-id="22df6-153">`signalR.LogLevel.Trace` &ndash; 추적 메시지.</span><span class="sxs-lookup"><span data-stu-id="22df6-153">`signalR.LogLevel.Trace` &ndash; Trace messages.</span></span> <span data-ttu-id="22df6-154">허브와 클라이언트 간에 전송되는 데이터를 포함한 모든 것을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-154">Logs everything, including data transported between hub and client.</span></span>

<span data-ttu-id="22df6-155">로그 수준을 구성하려면 [HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder)의 [configureLogging](/javascript/api/%40aspnet/signalr/hubconnectionbuilder#configurelogging) 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-155">Use the [configureLogging](/javascript/api/%40aspnet/signalr/hubconnectionbuilder#configurelogging) method on [HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder) to configure the log level.</span></span> <span data-ttu-id="22df6-156">메시지는 브라우저 콘솔에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="22df6-156">Messages are logged to the browser console.</span></span>

[!code-javascript[Logging levels](javascript-client/sample/wwwroot/js/chat.js?range=9-12)]

## <a name="additional-resources"></a><span data-ttu-id="22df6-157">추가 자료</span><span class="sxs-lookup"><span data-stu-id="22df6-157">Additional resources</span></span>

* [<span data-ttu-id="22df6-158">JavaScript API 참조</span><span class="sxs-lookup"><span data-stu-id="22df6-158">JavaScript API reference</span></span>](/javascript/api/?view=signalr-js-latest)
* [<span data-ttu-id="22df6-159">허브</span><span class="sxs-lookup"><span data-stu-id="22df6-159">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="22df6-160">.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="22df6-160">.NET client</span></span>](xref:signalr/dotnet-client)
* [<span data-ttu-id="22df6-161">Azure에 게시하기</span><span class="sxs-lookup"><span data-stu-id="22df6-161">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
* [<span data-ttu-id="22df6-162">ASP.NET Core에서 원본 간 요청(CORS)을 사용하도록 설정하기</span><span class="sxs-lookup"><span data-stu-id="22df6-162">Enable Cross-Origin Requests (CORS) in ASP.NET Core</span></span>](xref:security/cors)
