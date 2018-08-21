---
title: ASP.NET Core SignalR JavaScript 클라이언트
author: tdykstra
description: ASP.NET Core SignalR JavaScript 클라이언트의 개요입니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 05/29/2018
uid: signalr/javascript-client
ms.openlocfilehash: c13c41b0344b0c880e842f2799d6ee97bd7fff7e
ms.sourcegitcommit: 3ca527f27c88cfc9d04688db5499e372fbc2c775
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39095426"
---
# <a name="aspnet-core-signalr-javascript-client"></a><span data-ttu-id="b56a5-103">ASP.NET Core SignalR JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="b56a5-103">ASP.NET Core SignalR JavaScript client</span></span>

<span data-ttu-id="b56a5-104">작성자: [Rachel Appel](http://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="b56a5-104">By [Rachel Appel](http://twitter.com/rachelappel)</span></span>

<span data-ttu-id="b56a5-105">ASP.NET Core SignalR JavaScript 클라이언트 라이브러리를 사용 하면 서버 쪽 허브 코드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-105">The ASP.NET Core SignalR JavaScript client library enables developers to call server-side hub code.</span></span>

<span data-ttu-id="b56a5-106">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/javascript-client/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="b56a5-106">[View or download sample code](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/javascript-client/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="install-the-signalr-client-package"></a><span data-ttu-id="b56a5-107">SignalR 클라이언트 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-107">Install the SignalR client package</span></span>

<span data-ttu-id="b56a5-108">SignalR JavaScript 클라이언트 라이브러리를 전달 되는 [npm](https://www.npmjs.com/) 패키지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-108">The SignalR JavaScript client library is delivered as an [npm](https://www.npmjs.com/) package.</span></span> <span data-ttu-id="b56a5-109">Visual Studio를 사용 하는 경우 실행할 `npm install` 에서 합니다 **패키지 관리자 콘솔** 루트 폴더에 있는 동안.</span><span class="sxs-lookup"><span data-stu-id="b56a5-109">If you're using Visual Studio, run `npm install` from the **Package Manager Console** while in the root folder.</span></span> <span data-ttu-id="b56a5-110">Visual Studio Code에서 명령을 실행 합니다 **통합 터미널**합니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-110">For Visual Studio Code, run the command from the **Integrated Terminal**.</span></span>

  ```console
   npm init -y
   npm install @aspnet/signalr
  ```

<span data-ttu-id="b56a5-111">Npm에서 패키지 콘텐츠를 설치 합니다 *node_modules\\@aspnet\signalr\dist\browser* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-111">Npm installs the package contents in the *node_modules\\@aspnet\signalr\dist\browser* folder.</span></span> <span data-ttu-id="b56a5-112">라는 새 폴더를 만듭니다 *signalr* 아래의 합니다 *wwwroot\\lib* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-112">Create a new folder named *signalr* under the *wwwroot\\lib* folder.</span></span> <span data-ttu-id="b56a5-113">복사 합니다 *signalr.js* 파일을 합니다 *wwwroot\lib\signalr* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-113">Copy the *signalr.js* file to the *wwwroot\lib\signalr* folder.</span></span>

## <a name="use-the-signalr-javascript-client"></a><span data-ttu-id="b56a5-114">SignalR JavaScript 클라이언트 사용</span><span class="sxs-lookup"><span data-stu-id="b56a5-114">Use the SignalR JavaScript client</span></span>

<span data-ttu-id="b56a5-115">SignalR JavaScript 클라이언트에서 참조 된 `<script>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-115">Reference the SignalR JavaScript client in the `<script>` element.</span></span>

```html
<script src="~/lib/signalr/signalr.js"></script>
```

## <a name="connect-to-a-hub"></a><span data-ttu-id="b56a5-116">허브에 연결</span><span class="sxs-lookup"><span data-stu-id="b56a5-116">Connect to a hub</span></span>

<span data-ttu-id="b56a5-117">다음 코드를 만들고 연결을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-117">The following code creates and starts a connection.</span></span> <span data-ttu-id="b56a5-118">허브의 이름은 대/소문자 구분입니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-118">The hub's name is case insensitive.</span></span>

[!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=9-12,28)]

### <a name="cross-origin-connections"></a><span data-ttu-id="b56a5-119">크로스-원본 연결</span><span class="sxs-lookup"><span data-stu-id="b56a5-119">Cross-origin connections</span></span>

<span data-ttu-id="b56a5-120">일반적으로 브라우저는 요청된 된 페이지와 동일한 도메인에서 연결을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-120">Typically, browsers load connections from the same domain as the requested page.</span></span> <span data-ttu-id="b56a5-121">그러나 다른 도메인에 연결할 때 필요한 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-121">However, there are occasions when a connection to another domain is required.</span></span>

<span data-ttu-id="b56a5-122">악성 사이트에서 다른 사이트의 중요 한 데이터를 읽을 않으려면 [크로스-원본 연결](xref:security/cors) 기본적으로 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-122">To prevent a malicious site from reading sensitive data from another site, [cross-origin connections](xref:security/cors) are disabled by default.</span></span> <span data-ttu-id="b56a5-123">크로스-원본 요청을 허용 하려면에 있도록는 `Startup` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-123">To allow a cross-origin request, enable it in the `Startup` class.</span></span>

[!code-csharp[Cross-origin connections](javascript-client/sample/Startup.cs?highlight=29-35,56)]

## <a name="call-hub-methods-from-client"></a><span data-ttu-id="b56a5-124">클라이언트에서 허브 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-124">Call hub methods from client</span></span>

<span data-ttu-id="b56a5-125">JavaScript 클라이언트 공용 메서드를 호출 하 여 허브를 사용 하 여 `connection.invoke`입니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-125">JavaScript clients call public methods on hubs by using `connection.invoke`.</span></span> <span data-ttu-id="b56a5-126">`invoke` 메서드는 두 인수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-126">The `invoke` method accepts two arguments:</span></span>

* <span data-ttu-id="b56a5-127">허브 메서드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-127">The name of the hub method.</span></span> <span data-ttu-id="b56a5-128">다음 예제에서는 허브 이름은 `SendMessage`합니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-128">In the following example, the hub name is `SendMessage`.</span></span>
* <span data-ttu-id="b56a5-129">허브 메서드에 정의 된 모든 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-129">Any arguments defined in the hub method.</span></span> <span data-ttu-id="b56a5-130">다음 예제에서는 인수 이름은 `message`합니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-130">In the following example, the argument name is `message`.</span></span>

[!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=24)]

## <a name="call-client-methods-from-hub"></a><span data-ttu-id="b56a5-131">허브에서 클라이언트 메서드를 호출</span><span class="sxs-lookup"><span data-stu-id="b56a5-131">Call client methods from hub</span></span>

<span data-ttu-id="b56a5-132">허브에서 메시지를 받으려면 사용 하는 메서드를 정의 합니다 `connection.on` 메서드.</span><span class="sxs-lookup"><span data-stu-id="b56a5-132">To receive messages from the hub, define a method using the `connection.on` method.</span></span>

* <span data-ttu-id="b56a5-133">JavaScript 클라이언트 메서드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-133">The name of the JavaScript client method.</span></span> <span data-ttu-id="b56a5-134">다음 예제에서는 메서드 이름은 `ReceiveMessage`합니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-134">In the following example, the method name is `ReceiveMessage`.</span></span>
* <span data-ttu-id="b56a5-135">허브 메서드에 전달 된 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-135">Arguments the hub passes to the method.</span></span> <span data-ttu-id="b56a5-136">다음 예제에서는 인수 값은 `message`합니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-136">In the following example, the argument value is `message`.</span></span>

[!code-javascript[Receive calls from hub](javascript-client/sample/wwwroot/js/chat.js?range=14-19)]

<span data-ttu-id="b56a5-137">위의 코드에서 `connection.on` 서버 쪽 코드를 사용 하 여 호출 될 때 실행 되는 `SendAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="b56a5-137">The preceding code in `connection.on` runs when server-side code calls it using the `SendAsync` method.</span></span>

[!code-csharp[Call client-side](javascript-client/sample/hubs/chathub.cs?range=8-11)]

<span data-ttu-id="b56a5-138">SignalR 클라이언트 호출할 메서드를 메서드 이름을 일치 시켜를 결정 하 고에 정의 된 인수 `SendAsync` 고 `connection.on`입니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-138">SignalR determines which client method to call by matching the method name and arguments defined in `SendAsync` and `connection.on`.</span></span>

> [!NOTE]
> <span data-ttu-id="b56a5-139">호출 하는 것이 좋습니다 `connection.start` 후 `connection.on` 처리기는 모든 메시지를 수신 하기 전에 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-139">As a best practice, call `connection.start` after `connection.on` so your handlers are registered before any messages are received.</span></span>

## <a name="error-handling-and-logging"></a><span data-ttu-id="b56a5-140">오류 처리 및 로깅</span><span class="sxs-lookup"><span data-stu-id="b56a5-140">Error handling and logging</span></span>

<span data-ttu-id="b56a5-141">체인을 `catch` 의 끝에 메서드를 `connection.start` 클라이언트 쪽 오류를 처리 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-141">Chain a `catch` method to the end of the `connection.start` method to handle client-side errors.</span></span> <span data-ttu-id="b56a5-142">사용 하 여 `console.error` 브라우저의 콘솔에 출력 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-142">Use `console.error` to output errors to the browser's console.</span></span>

[!code-javascript[Error handling](javascript-client/sample/wwwroot/js/chat.js?range=28)]

<span data-ttu-id="b56a5-143">연결이 설정 되 면 로그로 거와 이벤트의 형식을 전달 하 여 클라이언트 쪽 로그 추적을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-143">Setup client-side log tracing by passing a logger and type of event to log when the connection is made.</span></span> <span data-ttu-id="b56a5-144">지정 된 로그 수준을 사용 하 여 이상 메시지가 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-144">Messages are logged with the specified log level and higher.</span></span> <span data-ttu-id="b56a5-145">사용 가능한 로그 수준은 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-145">Available log levels are as follows:</span></span>

* <span data-ttu-id="b56a5-146">`signalR.LogLevel.Error` : 오류 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-146">`signalR.LogLevel.Error` : Error messages.</span></span> <span data-ttu-id="b56a5-147">로그 `Error` 메시지만 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-147">Logs `Error` messages only.</span></span>
* <span data-ttu-id="b56a5-148">`signalR.LogLevel.Warning` : 잠재적 오류에 대 한 경고 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-148">`signalR.LogLevel.Warning` : Warning messages about potential errors.</span></span> <span data-ttu-id="b56a5-149">로그 `Warning`, 및 `Error` 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-149">Logs `Warning`, and `Error` messages.</span></span>
* <span data-ttu-id="b56a5-150">`signalR.LogLevel.Information` : 오류 없이 상태 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-150">`signalR.LogLevel.Information` : Status messages without errors.</span></span> <span data-ttu-id="b56a5-151">로그 `Information`하십시오 `Warning`, 및 `Error` 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-151">Logs `Information`, `Warning`, and `Error` messages.</span></span>
* <span data-ttu-id="b56a5-152">`signalR.LogLevel.Trace` : 메시지를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-152">`signalR.LogLevel.Trace` : Trace messages.</span></span> <span data-ttu-id="b56a5-153">허브와 클라이언트 간에 전송 되는 데이터를 포함 하 여 모든 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-153">Logs everything, including data transported between hub and client.</span></span>

<span data-ttu-id="b56a5-154">사용 된 `configureLogging` 메서드를 `HubConnectionBuilder` 로그 수준을 구성 하려면.</span><span class="sxs-lookup"><span data-stu-id="b56a5-154">Use the `configureLogging` method on `HubConnectionBuilder` to configure the log level.</span></span> <span data-ttu-id="b56a5-155">메시지는 브라우저 콘솔에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b56a5-155">Messages are logged to the browser console.</span></span>

[!code-javascript[Logging levels](javascript-client/sample/wwwroot/js/chat.js?range=9-12)]

## <a name="related-resources"></a><span data-ttu-id="b56a5-156">관련 참고 자료</span><span class="sxs-lookup"><span data-stu-id="b56a5-156">Related resources</span></span>

* [<span data-ttu-id="b56a5-157">허브</span><span class="sxs-lookup"><span data-stu-id="b56a5-157">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="b56a5-158">.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="b56a5-158">.NET client</span></span>](xref:signalr/dotnet-client)
* [<span data-ttu-id="b56a5-159">Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="b56a5-159">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
* [<span data-ttu-id="b56a5-160">ASP.NET Core에서 원본 간 요청 (CORS)를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="b56a5-160">Enable Cross-Origin Requests (CORS) in ASP.NET Core</span></span>](xref:security/cors)
