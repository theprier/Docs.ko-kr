---
title: ASP.NET SignalR JavaScript 코어 클라이언트
author: rachelappel
description: ASP.NET Core SignalR JavaScript 클라이언트 간략하게 설명 합니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 05/29/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: signalr/javascript-client
ms.openlocfilehash: 6ff888d3337bb53d435744009f4cc24b327ebcda
ms.sourcegitcommit: 7e87671fea9a5f36ca516616fe3b40b537f428d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35341940"
---
# <a name="aspnet-core-signalr-javascript-client"></a><span data-ttu-id="27c9b-103">ASP.NET SignalR JavaScript 코어 클라이언트</span><span class="sxs-lookup"><span data-stu-id="27c9b-103">ASP.NET Core SignalR JavaScript client</span></span>

<span data-ttu-id="27c9b-104">작성자: [Rachel Appel](http://twitter.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="27c9b-104">By [Rachel Appel](http://twitter.com/rachelappel)</span></span>

<span data-ttu-id="27c9b-105">ASP.NET Core SignalR JavaScript 클라이언트 라이브러리를 사용 하면 서버 쪽 허브 코드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-105">The ASP.NET Core SignalR JavaScript client library enables developers to call server-side hub code.</span></span>

<span data-ttu-id="27c9b-106">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/javascript-client/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="27c9b-106">[View or download sample code](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/javascript-client/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="install-the-signalr-client-package"></a><span data-ttu-id="27c9b-107">SignalR 클라이언트 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-107">Install the SignalR client package</span></span>

<span data-ttu-id="27c9b-108">SignalR JavaScript 클라이언트 라이브러리로 배달 되는 [npm](https://www.npmjs.com/) 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-108">The SignalR JavaScript client library is delivered as an [npm](https://www.npmjs.com/) package.</span></span> <span data-ttu-id="27c9b-109">Visual Studio를 사용 하는 경우 실행 `npm install` 에서 **패키지 관리자 콘솔** 루트 폴더에 있는 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-109">If you're using Visual Studio, run `npm install` from the **Package Manager Console** while in the root folder.</span></span> <span data-ttu-id="27c9b-110">Visual Studio 코드에 대 한에서 명령을 실행 하는 **통합 터미널**합니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-110">For Visual Studio Code, run the command from the **Integrated Terminal**.</span></span>

  ```console
   npm init -y
   npm install @aspnet/signalr
  ```

<span data-ttu-id="27c9b-111">Npm 설치에서 패키지 콘텐츠는 *node_modules\\ @aspnet\signalr\dist\browser*  폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-111">Npm installs the package contents in the *node_modules\\@aspnet\signalr\dist\browser* folder.</span></span> <span data-ttu-id="27c9b-112">라는 새 폴더 만들기 *signalr* 아래는 *wwwroot\\lib* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-112">Create a new folder named *signalr* under the *wwwroot\\lib* folder.</span></span> <span data-ttu-id="27c9b-113">복사는 *signalr.js* 파일을 여 *wwwroot\lib\signalr* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-113">Copy the *signalr.js* file to the *wwwroot\lib\signalr* folder.</span></span>

## <a name="use-the-signalr-javascript-client"></a><span data-ttu-id="27c9b-114">SignalR JavaScript 클라이언트 사용</span><span class="sxs-lookup"><span data-stu-id="27c9b-114">Use the SignalR JavaScript client</span></span>

<span data-ttu-id="27c9b-115">참조에서 SignalR JavaScript 클라이언트는 `<script>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-115">Reference the SignalR JavaScript client in the `<script>` element.</span></span>

```html
<script src="~/lib/signalr/signalr.js"></script>
```

## <a name="connect-to-a-hub"></a><span data-ttu-id="27c9b-116">허브에 연결</span><span class="sxs-lookup"><span data-stu-id="27c9b-116">Connect to a hub</span></span>

<span data-ttu-id="27c9b-117">다음 코드를 만들고 연결을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-117">The following code creates and starts a connection.</span></span> <span data-ttu-id="27c9b-118">허브의 이름은 대/소문자 구분입니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-118">The hub's name is case insensitive.</span></span>

[!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=9-12,28)]

### <a name="cross-origin-connections"></a><span data-ttu-id="27c9b-119">크로스-원본 연결</span><span class="sxs-lookup"><span data-stu-id="27c9b-119">Cross-origin connections</span></span>

<span data-ttu-id="27c9b-120">일반적으로 브라우저는 요청된 된 페이지와 동일한 도메인에서 연결을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-120">Typically, browsers load connections from the same domain as the requested page.</span></span> <span data-ttu-id="27c9b-121">그러나 다른 도메인에 대 한 연결 필요한 경우 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-121">However, there are occasions when a connection to another domain is required.</span></span>

<span data-ttu-id="27c9b-122">악성 사이트를 다른 사이트에서 중요 한 데이터를 읽는 하지 않도록 하려면 [크로스-원본 연결](xref:security/cors) 기본적으로 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-122">To prevent a malicious site from reading sensitive data from another site, [cross-origin connections](xref:security/cors) are disabled by default.</span></span> <span data-ttu-id="27c9b-123">크로스-원본 요청을 허용 하려면에서 사용 하도록 설정할는 `Startup` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-123">To allow a cross-origin request, enable it in the `Startup` class.</span></span>

[!code-csharp[Cross-origin connections](javascript-client/sample/Startup.cs?highlight=29-35,56)]

## <a name="call-hub-methods-from-client"></a><span data-ttu-id="27c9b-124">클라이언트에서 허브 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-124">Call hub methods from client</span></span>

<span data-ttu-id="27c9b-125">JavaScript 클라이언트 공용 메서드를 호출 하 여 허브를 사용 하 여 `connection.invoke`합니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-125">JavaScript clients call public methods on hubs by using `connection.invoke`.</span></span> <span data-ttu-id="27c9b-126">`invoke` 메서드는 두 인수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-126">The `invoke` method accepts two arguments:</span></span>

* <span data-ttu-id="27c9b-127">허브 메서드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-127">The name of the hub method.</span></span> <span data-ttu-id="27c9b-128">다음 예에서는 허브 이름은 `SendMessage`합니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-128">In the following example, the hub name is `SendMessage`.</span></span>
* <span data-ttu-id="27c9b-129">허브 메서드에 정의 된 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-129">Any arguments defined in the hub method.</span></span> <span data-ttu-id="27c9b-130">다음 예제에서는 인수 이름은 `message`합니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-130">In the following example, the argument name is `message`.</span></span>

[!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=24)]

## <a name="call-client-methods-from-hub"></a><span data-ttu-id="27c9b-131">허브에서 클라이언트를 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="27c9b-131">Call client methods from hub</span></span>

<span data-ttu-id="27c9b-132">허브에서 메시지를 받으려면 사용 하 여 메서드를 정의 고 `connection.on` 메서드.</span><span class="sxs-lookup"><span data-stu-id="27c9b-132">To receive messages from the hub, define a method using the `connection.on` method.</span></span>

* <span data-ttu-id="27c9b-133">JavaScript 클라이언트 메서드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-133">The name of the JavaScript client method.</span></span> <span data-ttu-id="27c9b-134">다음 예제에서는 메서드 이름은 `ReceiveMessage`합니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-134">In the following example, the method name is `ReceiveMessage`.</span></span>
* <span data-ttu-id="27c9b-135">허브 메서드에 전달 된 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-135">Arguments the hub passes to the method.</span></span> <span data-ttu-id="27c9b-136">인수 값이 다음 예에서 `message`합니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-136">In the following example, the argument value is `message`.</span></span>

[!code-javascript[Receive calls from hub](javascript-client/sample/wwwroot/js/chat.js?range=14-19)]

<span data-ttu-id="27c9b-137">위의 코드에서 `connection.on` 서버 쪽 코드를 사용 하 여 호출할 때 실행 되는 `SendAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="27c9b-137">The preceding code in `connection.on` runs when server-side code calls it using the `SendAsync` method.</span></span>

[!code-csharp[Call client-side](javascript-client/sample/hubs/chathub.cs?range=8-11)]

<span data-ttu-id="27c9b-138">SignalR 메서드 이름과 일치 하 여 호출 클라이언트 방법을 결정 하 고 인수에 정의 된 `SendAsync` 및 `connection.on`합니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-138">SignalR determines which client method to call by matching the method name and arguments defined in `SendAsync` and `connection.on`.</span></span>

> [!NOTE]
> <span data-ttu-id="27c9b-139">모범 사례로, 호출 `connection.start` 후 `connection.on` 모든 메시지를 수신 하기 전에 처리기를 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-139">As a best practice, call `connection.start` after `connection.on` so your handlers are registered before any messages are received.</span></span>

## <a name="error-handling-and-logging"></a><span data-ttu-id="27c9b-140">오류 처리 및 로깅</span><span class="sxs-lookup"><span data-stu-id="27c9b-140">Error handling and logging</span></span>

<span data-ttu-id="27c9b-141">체인을 `catch` 끝날 때까지 메서드는 `connection.start` 클라이언트 오류를 처리 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="27c9b-141">Chain a `catch` method to the end of the `connection.start` method to handle client-side errors.</span></span> <span data-ttu-id="27c9b-142">사용 하 여 `console.error` 브라우저의 콘솔에 출력 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-142">Use `console.error` to output errors to the browser's console.</span></span>

[!code-javascript[Error handling](javascript-client/sample/wwwroot/js/chat.js?range=28)]

<span data-ttu-id="27c9b-143">연결 되 면 로그로 거와 형식의 이벤트를 전달 하 여 클라이언트 쪽 로그 추적을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-143">Setup client-side log tracing by passing a logger and type of event to log when the connection is made.</span></span> <span data-ttu-id="27c9b-144">지정 된 로그 수준으로 및 더 높은 메시지가 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-144">Messages are logged with the specified log level and higher.</span></span> <span data-ttu-id="27c9b-145">사용 가능한 로그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-145">Available log levels are as follows:</span></span>

* <span data-ttu-id="27c9b-146">`signalR.LogLevel.Error` : 오류 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-146">`signalR.LogLevel.Error` : Error messages.</span></span> <span data-ttu-id="27c9b-147">로그 `Error` 만 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-147">Logs `Error` messages only.</span></span>
* <span data-ttu-id="27c9b-148">`signalR.LogLevel.Warning` : 잠재적 오류에 대 한 경고 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-148">`signalR.LogLevel.Warning` : Warning messages about potential errors.</span></span> <span data-ttu-id="27c9b-149">로그 `Warning`, 및 `Error` 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-149">Logs `Warning`, and `Error` messages.</span></span>
* <span data-ttu-id="27c9b-150">`signalR.LogLevel.Information` : 오류 없이 상태 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-150">`signalR.LogLevel.Information` : Status messages without errors.</span></span> <span data-ttu-id="27c9b-151">로그 `Information`, `Warning`, 및 `Error` 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-151">Logs `Information`, `Warning`, and `Error` messages.</span></span>
* <span data-ttu-id="27c9b-152">`signalR.LogLevel.Trace` : 메시지를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-152">`signalR.LogLevel.Trace` : Trace messages.</span></span> <span data-ttu-id="27c9b-153">허브와 클라이언트 간에 전송 되는 데이터를 포함 하 여 모든 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-153">Logs everything, including data transported between hub and client.</span></span>

<span data-ttu-id="27c9b-154">사용 하 여는 `configureLogging` 메서드를 `HubConnectionBuilder` 로그 수준을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-154">Use the `configureLogging` method on `HubConnectionBuilder` to configure the log level.</span></span> <span data-ttu-id="27c9b-155">메시지가는 브라우저 콘솔에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27c9b-155">Messages are logged to the browser console.</span></span>

[!code-javascript[Logging levels](javascript-client/sample/wwwroot/js/chat.js?range=9-12)]

## <a name="related-resources"></a><span data-ttu-id="27c9b-156">관련 참고 자료</span><span class="sxs-lookup"><span data-stu-id="27c9b-156">Related resources</span></span>

* [<span data-ttu-id="27c9b-157">허브</span><span class="sxs-lookup"><span data-stu-id="27c9b-157">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="27c9b-158">.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="27c9b-158">.NET client</span></span>](xref:signalr/dotnet-client)
* [<span data-ttu-id="27c9b-159">Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="27c9b-159">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
* [<span data-ttu-id="27c9b-160">ASP.NET Core에서 크로스-원본 요청 (CORS)를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="27c9b-160">Enable Cross-Origin Requests (CORS) in ASP.NET Core</span></span>](xref:security/cors)