---
title: ASP.NET Core SignalR JavaScript 클라이언트
author: tdykstra
description: ASP.NET Core SignalR JavaScript 클라이언트의 개요입니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 11/14/2018
uid: signalr/javascript-client
ms.openlocfilehash: acdb4d1a59d980010fe89fe381190425cbb12901
ms.sourcegitcommit: 42a8164b8aba21f322ffefacb92301bdfb4d3c2d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54341462"
---
# <a name="aspnet-core-signalr-javascript-client"></a><span data-ttu-id="fc3df-103">ASP.NET Core SignalR JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="fc3df-103">ASP.NET Core SignalR JavaScript client</span></span>

<span data-ttu-id="fc3df-104">작성자: [Rachel Appel](http://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="fc3df-104">By [Rachel Appel](http://twitter.com/rachelappel)</span></span>

<span data-ttu-id="fc3df-105">ASP.NET Core SignalR JavaScript 클라이언트 라이브러리를 사용 하면 서버 쪽 허브 코드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-105">The ASP.NET Core SignalR JavaScript client library enables developers to call server-side hub code.</span></span>

<span data-ttu-id="fc3df-106">[샘플 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/javascript-client/sample)([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="fc3df-106">[View or download sample code](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/javascript-client/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="install-the-signalr-client-package"></a><span data-ttu-id="fc3df-107">SignalR 클라이언트 패키지 설치하기</span><span class="sxs-lookup"><span data-stu-id="fc3df-107">Install the SignalR client package</span></span>

<span data-ttu-id="fc3df-108">SignalR JavaScript 클라이언트 라이브러리는 [npm](https://www.npmjs.com/) 패키지로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-108">The SignalR JavaScript client library is delivered as an [npm](https://www.npmjs.com/) package.</span></span> <span data-ttu-id="fc3df-109">Visual Studio를 사용하고 있다면 **패키지 관리자 콘솔** 에서 루트 폴더에 있을 때 `npm install` 을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-109">If you're using Visual Studio, run `npm install` from the **Package Manager Console** while in the root folder.</span></span> <span data-ttu-id="fc3df-110">Visual Studio Code에서는 **통합 터미널** 에서 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-110">For Visual Studio Code, run the command from the **Integrated Terminal**.</span></span>

  ```console
  npm init -y
  npm install @aspnet/signalr
  ```

<span data-ttu-id="fc3df-111">그러면 npm이 *node_modules\\@aspnet\signalr\dist\browser* 폴더에 패키지 콘텐츠를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-111">npm installs the package contents in the *node_modules\\@aspnet\signalr\dist\browser* folder.</span></span> <span data-ttu-id="fc3df-112">*wwwroot\\lib* 폴더 하위에 *signalr* 이라는 새 폴더를 만듭니다 </span><span class="sxs-lookup"><span data-stu-id="fc3df-112">Create a new folder named *signalr* under the *wwwroot\\lib* folder.</span></span> <span data-ttu-id="fc3df-113">*signalr.js* 파일을 *wwwroot\lib\signalr* 폴더로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-113">Copy the *signalr.js* file to the *wwwroot\lib\signalr* folder.</span></span>

## <a name="use-the-signalr-javascript-client"></a><span data-ttu-id="fc3df-114">SignalR JavaScript 클라이언트 사용하기</span><span class="sxs-lookup"><span data-stu-id="fc3df-114">Use the SignalR JavaScript client</span></span>

<span data-ttu-id="fc3df-115">`<script>` 요소를 이용해서 SignalR JavaScript 클라이언트를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-115">Reference the SignalR JavaScript client in the `<script>` element.</span></span>

```html
<script src="~/lib/signalr/signalr.js"></script>
```

## <a name="connect-to-a-hub"></a><span data-ttu-id="fc3df-116">허브에 연결하기</span><span class="sxs-lookup"><span data-stu-id="fc3df-116">Connect to a hub</span></span>

<span data-ttu-id="fc3df-117">다음 코드는 연결을 만들고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-117">The following code creates and starts a connection.</span></span> <span data-ttu-id="fc3df-118">허브의 이름은 대소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-118">The hub's name is case insensitive.</span></span>

[!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=9-12)]

### <a name="cross-origin-connections"></a><span data-ttu-id="fc3df-119">원본 간 연결</span><span class="sxs-lookup"><span data-stu-id="fc3df-119">Cross-origin connections</span></span>

<span data-ttu-id="fc3df-120">일반적으로 브라우저는 요청된 페이지와 동일한 도메인에서 연결을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-120">Typically, browsers load connections from the same domain as the requested page.</span></span> <span data-ttu-id="fc3df-121">그러나 다른 도메인에 연결해야 하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-121">However, there are occasions when a connection to another domain is required.</span></span>

<span data-ttu-id="fc3df-122">악의적인 사이트가 다른 사이트의 민감한 데이터를 읽지 못하게 막기 위해서, 기본적으로 [원본 간 연결](xref:security/cors) 은 비활성화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-122">To prevent a malicious site from reading sensitive data from another site, [cross-origin connections](xref:security/cors) are disabled by default.</span></span> <span data-ttu-id="fc3df-123">원본 간 요청을 허용하려면 `Startup` 클래스에서 이를 활성화하십시오.</span><span class="sxs-lookup"><span data-stu-id="fc3df-123">To allow a cross-origin request, enable it in the `Startup` class.</span></span>

[!code-csharp[Cross-origin connections](javascript-client/sample/Startup.cs?highlight=29-35,56)]

## <a name="call-hub-methods-from-client"></a><span data-ttu-id="fc3df-124">클라이언트에서 허브 메서드 호출하기</span><span class="sxs-lookup"><span data-stu-id="fc3df-124">Call hub methods from client</span></span>

<span data-ttu-id="fc3df-125">JavaScript 클라이언트는 [HubConnection](/javascript/api/%40aspnet/signalr/hubconnection)의 [invoke](/javascript/api/%40aspnet/signalr/hubconnection#invoke) 메서드를 통해서 허브의 public 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-125">JavaScript clients call public methods on hubs via the [invoke](/javascript/api/%40aspnet/signalr/hubconnection#invoke) method of the [HubConnection](/javascript/api/%40aspnet/signalr/hubconnection).</span></span> <span data-ttu-id="fc3df-126">이 `invoke` 메서드는 두 가지 인수를 전달받습니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-126">The `invoke` method accepts two arguments:</span></span>

* <span data-ttu-id="fc3df-127">허브 메서드의 이름.</span><span class="sxs-lookup"><span data-stu-id="fc3df-127">The name of the hub method.</span></span> <span data-ttu-id="fc3df-128">다음 예제에서 허브 메서드의 이름은 `SendMessage`입니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-128">In the following example, the method name on the hub is `SendMessage`.</span></span>
* <span data-ttu-id="fc3df-129">허브 메서드에 정의된 모든 인수.</span><span class="sxs-lookup"><span data-stu-id="fc3df-129">Any arguments defined in the hub method.</span></span> <span data-ttu-id="fc3df-130">다음 예제에서 인수의 이름은 `message`입니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-130">In the following example, the argument name is `message`.</span></span> <span data-ttu-id="fc3df-131">이 예제 코드에서는 최신 버전의 Internet Explorer를 제외 하 고 모든 주요 브라우저에서 지원 되는 화살표 함수 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-131">The example code uses arrow function syntax that is supported in current versions of all major browsers except Internet Explorer.</span></span>

  [!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=24)]

## <a name="call-client-methods-from-hub"></a><span data-ttu-id="fc3df-132">허브에서 클라이언트 메서드 호출하기</span><span class="sxs-lookup"><span data-stu-id="fc3df-132">Call client methods from hub</span></span>

<span data-ttu-id="fc3df-133">허브에서 메시지를 수신하려면 `HubConnection`의 [on](/javascript/api/%40aspnet/signalr/hubconnection#on) 메서드를 이용해서 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-133">To receive messages from the hub, define a method using the [on](/javascript/api/%40aspnet/signalr/hubconnection#on) method of the `HubConnection`.</span></span>

* <span data-ttu-id="fc3df-134">JavaScript 클라이언트 메서드의 이름.</span><span class="sxs-lookup"><span data-stu-id="fc3df-134">The name of the JavaScript client method.</span></span> <span data-ttu-id="fc3df-135">다음 예제에서 메서드 이름은 `ReceiveMessage`입니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-135">In the following example, the method name is `ReceiveMessage`.</span></span>
* <span data-ttu-id="fc3df-136">허브에서 메서드로 전달될 인수.</span><span class="sxs-lookup"><span data-stu-id="fc3df-136">Arguments the hub passes to the method.</span></span> <span data-ttu-id="fc3df-137">다음 예제에서 인수의 이름은 `message` 입니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-137">In the following example, the argument value is `message`.</span></span>

[!code-javascript[Receive calls from hub](javascript-client/sample/wwwroot/js/chat.js?range=14-19)]

<span data-ttu-id="fc3df-138">위의 `connection.on` 내부의 코드는 서버 쪽 코드에서 [SendAsync](/dotnet/api/microsoft.aspnetcore.signalr.clientproxyextensions.sendasync) 메서드를 사용하여 이 코드를 호출할 때 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-138">The preceding code in `connection.on` runs when server-side code calls it using the [SendAsync](/dotnet/api/microsoft.aspnetcore.signalr.clientproxyextensions.sendasync) method.</span></span>

[!code-csharp[Call client-side](javascript-client/sample/hubs/chathub.cs?range=8-11)]

<span data-ttu-id="fc3df-139">SignalR은 `SendAsync`와 `connection.on`에 정의된 메서드 이름과 인수들이 일치하는지를 검사해서 어떤 클라이언트 메서드를 호출할지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-139">SignalR determines which client method to call by matching the method name and arguments defined in `SendAsync` and `connection.on`.</span></span>

> [!NOTE]
> <span data-ttu-id="fc3df-140">권장되는 방식은 `on` 메서드를 호출한 뒤에 `HubConnection`의 [start](/javascript/api/%40aspnet/signalr/hubconnection#start) 메서드를 호출하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-140">As a best practice, call the [start](/javascript/api/%40aspnet/signalr/hubconnection#start) method on the `HubConnection` after `on`.</span></span> <span data-ttu-id="fc3df-141">이렇게 하면 모든 메시지를 수신하기 전에 처리기가 먼저 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-141">Doing so ensures your handlers are registered before any messages are received.</span></span>

## <a name="error-handling-and-logging"></a><span data-ttu-id="fc3df-142">오류 처리 및 로깅</span><span class="sxs-lookup"><span data-stu-id="fc3df-142">Error handling and logging</span></span>

<span data-ttu-id="fc3df-143">클라이언트 쪽 오류를 처리하려면 `start` 메서드의 끝에 `catch` 메서드를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-143">Chain a `catch` method to the end of the `start` method to handle client-side errors.</span></span> <span data-ttu-id="fc3df-144">브라우저의 콘솔에 오류를 출력하려면 `console.error`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-144">Use `console.error` to output errors to the browser's console.</span></span>

[!code-javascript[Error handling](javascript-client/sample/wwwroot/js/chat.js?range=43-45)]

<span data-ttu-id="fc3df-145">연결이 만들어지면 로거와 기록할 이벤트 유형을 전달하여 클라이언트 쪽 로그 추적을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-145">Setup client-side log tracing by passing a logger and type of event to log when the connection is made.</span></span> <span data-ttu-id="fc3df-146">지정한 로그 수준 이상의 메시지가 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-146">Messages are logged with the specified log level and higher.</span></span> <span data-ttu-id="fc3df-147">사용 가능한 로그 수준은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-147">Available log levels are as follows:</span></span>

* <span data-ttu-id="fc3df-148">`signalR.LogLevel.Error` &ndash; 오류 메시지.</span><span class="sxs-lookup"><span data-stu-id="fc3df-148">`signalR.LogLevel.Error` &ndash; Error messages.</span></span> <span data-ttu-id="fc3df-149">`Error` 메시지만 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-149">Logs `Error` messages only.</span></span>
* <span data-ttu-id="fc3df-150">`signalR.LogLevel.Warning` &ndash; 잠재적 오류에 대한 경고 메시지.</span><span class="sxs-lookup"><span data-stu-id="fc3df-150">`signalR.LogLevel.Warning` &ndash; Warning messages about potential errors.</span></span> <span data-ttu-id="fc3df-151">`Warning` 및 `Error` 메시지를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-151">Logs `Warning`, and `Error` messages.</span></span>
* <span data-ttu-id="fc3df-152">`signalR.LogLevel.Information` &ndash; 오류가 아닌 상태 메시지.</span><span class="sxs-lookup"><span data-stu-id="fc3df-152">`signalR.LogLevel.Information` &ndash; Status messages without errors.</span></span> <span data-ttu-id="fc3df-153">`Information`, `Warning` 및 `Error` 메시지를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-153">Logs `Information`, `Warning`, and `Error` messages.</span></span>
* <span data-ttu-id="fc3df-154">`signalR.LogLevel.Trace` &ndash; 추적 메시지.</span><span class="sxs-lookup"><span data-stu-id="fc3df-154">`signalR.LogLevel.Trace` &ndash; Trace messages.</span></span> <span data-ttu-id="fc3df-155">허브와 클라이언트 간에 전송되는 데이터를 포함한 모든 것을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-155">Logs everything, including data transported between hub and client.</span></span>

<span data-ttu-id="fc3df-156">로그 수준을 구성하려면 [HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder#configurelogging)의 [configureLogging](/javascript/api/%40aspnet/signalr/hubconnectionbuilder) 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-156">Use the [configureLogging](/javascript/api/%40aspnet/signalr/hubconnectionbuilder#configurelogging) method on [HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder) to configure the log level.</span></span> <span data-ttu-id="fc3df-157">메시지는 브라우저 콘솔에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-157">Messages are logged to the browser console.</span></span>

[!code-javascript[Logging levels](javascript-client/sample/wwwroot/js/chat.js?range=9-12)]

## <a name="reconnect-clients"></a><span data-ttu-id="fc3df-158">클라이언트를 다시 연결</span><span class="sxs-lookup"><span data-stu-id="fc3df-158">Reconnect clients</span></span>

<span data-ttu-id="fc3df-159">SignalR에 대 한 JavaScript 클라이언트가 자동으로 다시 연결 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-159">The JavaScript client for SignalR doesn't automatically reconnect.</span></span> <span data-ttu-id="fc3df-160">클라이언트에 수동으로 다시 연결 하는 코드를 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-160">You must write code that will reconnect your client manually.</span></span> <span data-ttu-id="fc3df-161">다음 코드는 일반적인 다시 연결 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-161">The following code demonstrates a typical reconnection approach:</span></span>

1. <span data-ttu-id="fc3df-162">함수 (이 경우에 `start` 함수) 연결을 시작 하기 위해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-162">A function (in this case, the `start` function) is created to start the connection.</span></span>
1. <span data-ttu-id="fc3df-163">호출 된 `start` 함수에서 연결의 `onclose` 이벤트 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="fc3df-163">Call the `start` function in the connection's `onclose` event handler.</span></span>

[!code-javascript[Reconnect the JavaScript client](javascript-client/sample/wwwroot/js/chat.js?range=28-40)]

<span data-ttu-id="fc3df-164">실제 구현을는 지 수 백오프를 사용 하거나 포기 하기 전에 지정 된 횟수를 다시 시도 하세요.</span><span class="sxs-lookup"><span data-stu-id="fc3df-164">A real-world implementation would use an exponential back-off or retry a specified number of times before giving up.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fc3df-165">추가 자료</span><span class="sxs-lookup"><span data-stu-id="fc3df-165">Additional resources</span></span>

* [<span data-ttu-id="fc3df-166">JavaScript API 참조</span><span class="sxs-lookup"><span data-stu-id="fc3df-166">JavaScript API reference</span></span>](/javascript/api/?view=signalr-js-latest)
* [<span data-ttu-id="fc3df-167">JavaScript 자습서</span><span class="sxs-lookup"><span data-stu-id="fc3df-167">JavaScript tutorial</span></span>](xref:tutorials/signalr)
* [<span data-ttu-id="fc3df-168">WebPack 및 TypeScript 자습서</span><span class="sxs-lookup"><span data-stu-id="fc3df-168">WebPack and TypeScript tutorial</span></span>](xref:tutorials/signalr-typescript-webpack)
* [<span data-ttu-id="fc3df-169">허브</span><span class="sxs-lookup"><span data-stu-id="fc3df-169">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="fc3df-170">.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="fc3df-170">.NET client</span></span>](xref:signalr/dotnet-client)
* [<span data-ttu-id="fc3df-171">Azure에 게시하기</span><span class="sxs-lookup"><span data-stu-id="fc3df-171">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
* [<span data-ttu-id="fc3df-172">원본 간 요청 (CORS)</span><span class="sxs-lookup"><span data-stu-id="fc3df-172">Cross-Origin Requests (CORS)</span></span>](xref:security/cors)
