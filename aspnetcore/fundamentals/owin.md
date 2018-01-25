---
title: OWIN(Open Web Interface for .NET)
author: ardalis
description: "ASP.NET Core 지 원하는 방법 열린 웹 인터페이스에 대 한.NET (OWIN), 웹 응용 프로그램 웹 서버에서 분리 될 수 있는 검색 합니다."
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/owin
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 42ffa01745b7a492b3b8cb2778805f254863b890
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="introduction-to-open-web-interface-for-net-owin"></a><span data-ttu-id="e2daf-103">.NET (OWIN)에 대 한 웹 인터페이스를 열려면 소개</span><span class="sxs-lookup"><span data-stu-id="e2daf-103">Introduction to Open Web Interface for .NET (OWIN)</span></span>

<span data-ttu-id="e2daf-104">여 [Steve Smith](https://ardalis.com/) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="e2daf-104">By [Steve Smith](https://ardalis.com/) and  [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="e2daf-105">ASP.NET Core는 OWIN(Open Web Interface for .NET)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-105">ASP.NET Core supports the Open Web Interface for .NET (OWIN).</span></span> <span data-ttu-id="e2daf-106">OWIN을 사용하면 웹앱을 웹 서버에서 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-106">OWIN allows web apps to be decoupled from web servers.</span></span> <span data-ttu-id="e2daf-107">요청과 관련된 응답을 처리 하는 파이프라인에 사용할 미들웨어에 대 한 표준 방법을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-107">It defines a standard way for middleware to be used in a pipeline to handle requests and associated responses.</span></span> <span data-ttu-id="e2daf-108">ASP.NET Core 응용 프로그램 및 미들웨어 OWIN 기반 응용 프로그램, 서버 및 미들웨어와 상호 운용이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-108">ASP.NET Core applications and middleware can interoperate with OWIN-based applications, servers, and middleware.</span></span>

<span data-ttu-id="e2daf-109">OWIN 두 프레임 워크를 함께 사용할 수 있는 서로 다른 개체 모델을 허용 하는 분리 계층을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-109">OWIN provides a decoupling layer that allows two frameworks with disparate object models to be used together.</span></span> <span data-ttu-id="e2daf-110">`Microsoft.AspNetCore.Owin` 패키지는 두 개의 어댑터 구현을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-110">The `Microsoft.AspNetCore.Owin` package provides two adapter implementations:</span></span>
- <span data-ttu-id="e2daf-111">OWIN에 대 한 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="e2daf-111">ASP.NET Core to OWIN</span></span> 
- <span data-ttu-id="e2daf-112">ASP.NET Core에는 OWIN</span><span class="sxs-lookup"><span data-stu-id="e2daf-112">OWIN to ASP.NET Core</span></span>

<span data-ttu-id="e2daf-113">이렇게 하면 ASP.NET Core를 호스트/OWIN 호환 서버를 기반으로 또는 ASP.NET Core를 기반으로 실행 되도록 다른 OWIN 호환 가능한 구성 요소에 대해 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-113">This allows ASP.NET Core to be hosted on top of an OWIN compatible server/host, or for other OWIN compatible components to be run on top of ASP.NET Core.</span></span>

<span data-ttu-id="e2daf-114">참고: 이러한 어댑터를 사용 하 여 성능 비용이 수반 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-114">Note: Using these adapters comes with a performance cost.</span></span> <span data-ttu-id="e2daf-115">Owin 패키지 또는 어댑터만 ASP.NET Core 구성 요소를 사용 하 여 응용 프로그램 사용 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-115">Applications using only ASP.NET Core components shouldn't use the Owin package or adapters.</span></span>

<span data-ttu-id="e2daf-116">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/owin/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="e2daf-116">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/owin/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="running-owin-middleware-in-the-aspnet-pipeline"></a><span data-ttu-id="e2daf-117">ASP.NET 파이프라인에서 OWIN 미들웨어를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-117">Running OWIN middleware in the ASP.NET pipeline</span></span>

<span data-ttu-id="e2daf-118">ASP.NET Core OWIN 지원의 일부로 배포 되는 `Microsoft.AspNetCore.Owin` 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-118">ASP.NET Core's OWIN support is deployed as part of the `Microsoft.AspNetCore.Owin` package.</span></span> <span data-ttu-id="e2daf-119">이 패키지를 설치 하 여 OWIN 지원 하 여 프로젝트에 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-119">You can import OWIN support into your project by installing this package.</span></span>

<span data-ttu-id="e2daf-120">OWIN 미들웨어를 준수 하는 [OWIN 사양](http://owin.org/spec/spec/owin-1.0.0.html), 요구 하는 `Func<IDictionary<string, object>, Task>` 인터페이스 및 특정 키 설정 (같은 `owin.ResponseBody`).</span><span class="sxs-lookup"><span data-stu-id="e2daf-120">OWIN middleware conforms to the [OWIN specification](http://owin.org/spec/spec/owin-1.0.0.html), which requires a `Func<IDictionary<string, object>, Task>` interface, and specific keys be set (such as `owin.ResponseBody`).</span></span> <span data-ttu-id="e2daf-121">다음과 같은 간단한 OWIN 미들웨어 "Hello World"를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-121">The following simple OWIN middleware displays "Hello World":</span></span>

```csharp
public Task OwinHello(IDictionary<string, object> environment)
{
    string responseText = "Hello World via OWIN";
    byte[] responseBytes = Encoding.UTF8.GetBytes(responseText);

    // OWIN Environment Keys: http://owin.org/spec/spec/owin-1.0.0.html
    var responseStream = (Stream)environment["owin.ResponseBody"];
    var responseHeaders = (IDictionary<string, string[]>)environment["owin.ResponseHeaders"];

    responseHeaders["Content-Length"] = new string[] { responseBytes.Length.ToString(CultureInfo.InvariantCulture) };
    responseHeaders["Content-Type"] = new string[] { "text/plain" };

    return responseStream.WriteAsync(responseBytes, 0, responseBytes.Length);
}
```

<span data-ttu-id="e2daf-122">샘플 서명을 반환는 `Task` 수락 하 고는 `IDictionary<string, object>` OWIN에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-122">The sample signature returns a `Task` and accepts an `IDictionary<string, object>` as required by OWIN.</span></span>

<span data-ttu-id="e2daf-123">다음 코드를 추가 하는 방법을 보여 줍니다는 `OwinHello` (위에 표시 된)으로 ASP.NET 파이프라인에 미들웨어는 `UseOwin` 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="e2daf-123">The following code shows how to add the `OwinHello` middleware (shown above) to the ASP.NET pipeline with the `UseOwin` extension method.</span></span>

```csharp
public void Configure(IApplicationBuilder app)
{
    app.UseOwin(pipeline =>
    {
        pipeline(next => OwinHello);
    });
}
```

<span data-ttu-id="e2daf-124">OWIN 파이프라인 내에서 수행 하는 기타 작업을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-124">You can configure other actions to take place within the OWIN pipeline.</span></span>

> [!NOTE]
> <span data-ttu-id="e2daf-125">응답 헤더 응답 스트림에 최초 쓰기 전에 수정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-125">Response headers should only be modified prior to the first write to the response stream.</span></span>

> [!NOTE]
> <span data-ttu-id="e2daf-126">여러 번 호출 `UseOwin` 은 성능상의 이유로 권장 되지 않음.</span><span class="sxs-lookup"><span data-stu-id="e2daf-126">Multiple calls to `UseOwin` is discouraged for performance reasons.</span></span> <span data-ttu-id="e2daf-127">OWIN 구성 요소는 함께 그룹화 하는 경우 가장 잘 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-127">OWIN components will operate best if grouped together.</span></span>

```csharp
app.UseOwin(pipeline =>
{
    pipeline(next =>
    {
        // do something before
        return OwinHello;
        // do something after
    });
});
```

<a name="hosting-on-owin"></a>

## <a name="using-aspnet-hosting-on-an-owin-based-server"></a><span data-ttu-id="e2daf-128">OWIN 기반 서버에서 ASP.NET 호스팅를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e2daf-128">Using ASP.NET Hosting on an OWIN-based server</span></span>

<span data-ttu-id="e2daf-129">OWIN 기반 서버 ASP.NET 응용 프로그램을 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-129">OWIN-based servers can host ASP.NET applications.</span></span> <span data-ttu-id="e2daf-130">이러한 서버도 [Nowin](https://github.com/Bobris/Nowin),.NET OWIN 웹 서버.</span><span class="sxs-lookup"><span data-stu-id="e2daf-130">One such server is [Nowin](https://github.com/Bobris/Nowin), a .NET OWIN web server.</span></span> <span data-ttu-id="e2daf-131">이 문서에 대 한 샘플에서는 Nowin 참조 하 고 만드는 데 사용 하는 프로젝트를 추가 했습니다는 `IServer` ASP.NET Core를 자체 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-131">In the sample for this article, I've included a project that references Nowin and uses it to create an `IServer` capable of self-hosting ASP.NET Core.</span></span>

[!code-csharp[Main](owin/sample/src/NowinSample/Program.cs?highlight=15)]

<span data-ttu-id="e2daf-132">`IServer`필요로 하는 인터페이스는 `Features` 속성 및 `Start` 메서드.</span><span class="sxs-lookup"><span data-stu-id="e2daf-132">`IServer` is an interface that requires an `Features` property and a `Start` method.</span></span>

<span data-ttu-id="e2daf-133">`Start`구성 하 고이 경우에 일련의 구문 분석 하는 주소는 IServerAddressesFeature 설정 하는 fluent API 호출을 통해 수행 된 서버를 시작 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-133">`Start` is responsible for configuring and starting the server, which in this case is done through a series of fluent API calls that set addresses parsed from the IServerAddressesFeature.</span></span> <span data-ttu-id="e2daf-134">fluent 구성을 `_builder` 요청에서 처리 되는 변수를 지정는 `appFunc` 메서드 이전에 정의 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-134">Note that the fluent configuration of the `_builder` variable specifies that requests will be handled by the `appFunc` defined earlier in the method.</span></span> <span data-ttu-id="e2daf-135">이 `Func` 들어오는 요청을 처리할을 요청할 때마다 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-135">This `Func` is called on each request to process incoming requests.</span></span>

<span data-ttu-id="e2daf-136">추가 `IWebHostBuilder` 확장을 쉽게 추가 하 고 Nowin 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-136">We'll also add an `IWebHostBuilder` extension to make it easy to add and configure the Nowin server.</span></span>

```csharp
using System;
using Microsoft.AspNetCore.Hosting.Server;
using Microsoft.Extensions.DependencyInjection;
using Nowin;
using NowinSample;

namespace Microsoft.AspNetCore.Hosting
{
    public static class NowinWebHostBuilderExtensions
    {
        public static IWebHostBuilder UseNowin(this IWebHostBuilder builder)
        {
            return builder.ConfigureServices(services =>
            {
                services.AddSingleton<IServer, NowinServer>();
            });
        }

        public static IWebHostBuilder UseNowin(this IWebHostBuilder builder, Action<ServerBuilder> configure)
        {
            builder.ConfigureServices(services =>
            {
                services.Configure(configure);
            });
            return builder.UseNowin();
        }
    }
}
```

<span data-ttu-id="e2daf-137">이 위치를에서 확장을 호출 하 여 사용자 지정이 서버를 사용 하 여 ASP.NET 응용 프로그램을 실행 하는 데 필요한에 있는 모든 *Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="e2daf-137">With this in place, all that's required to run an ASP.NET application using this custom server to call the extension in *Program.cs*:</span></span>

```csharp

using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Hosting;

namespace NowinSample
{
    public class Program
    {
        public static void Main(string[] args)
        {
            var host = new WebHostBuilder()
                .UseNowin()
                .UseContentRoot(Directory.GetCurrentDirectory())
                .UseIISIntegration()
                .UseStartup<Startup>()
                .Build();

            host.Run();
        }
    }
}

```

<span data-ttu-id="e2daf-138">ASP.NET에 대 한 자세한 [서버](servers/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-138">Learn more about ASP.NET [Servers](servers/index.md).</span></span>

## <a name="run-aspnet-core-on-an-owin-based-server-and-use-its-websockets-support"></a><span data-ttu-id="e2daf-139">OWIN 기반 서버에서 ASP.NET Core를 실행 하 고 해당 Websocket 지원 사용</span><span class="sxs-lookup"><span data-stu-id="e2daf-139">Run ASP.NET Core on an OWIN-based server and use its WebSockets support</span></span>

<span data-ttu-id="e2daf-140">OWIN 기반 서버의 기능의 또 다른 예를 활용 하 여 ASP.NET 코어는 Websocket 같은 기능에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-140">Another example of how OWIN-based servers' features can be leveraged by ASP.NET Core is access to features like WebSockets.</span></span> <span data-ttu-id="e2daf-141">이전 예제에서 사용 되는.NET OWIN 웹 서버에 ASP.NET Core 응용 프로그램에서 사용할 수 있는 기본 제공 되는 웹 소켓에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="e2daf-141">The .NET OWIN web server used in the previous example has support for Web Sockets built in, which can be leveraged by an ASP.NET Core application.</span></span> <span data-ttu-id="e2daf-142">다음 예제에서는 Websocket을 지원 하 고 Websocket 통해 서버에 보낸 모든 항목이 다시 에코 하는 단순한 웹 앱을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-142">The example below shows a simple web app that supports Web Sockets and echoes back everything sent to the server through WebSockets.</span></span>

```csharp
public class Startup
{
    public void Configure(IApplicationBuilder app)
    {
        app.Use(async (context, next) =>
        {
            if (context.WebSockets.IsWebSocketRequest)
            {
                WebSocket webSocket = await context.WebSockets.AcceptWebSocketAsync();
                await EchoWebSocket(webSocket);
            }
            else
            {
                await next();
            }
        });

        app.Run(context =>
        {
            return context.Response.WriteAsync("Hello World");
        });
    }

    private async Task EchoWebSocket(WebSocket webSocket)
    {
        byte[] buffer = new byte[1024];
        WebSocketReceiveResult received = await webSocket.ReceiveAsync(
            new ArraySegment<byte>(buffer), CancellationToken.None);

        while (!webSocket.CloseStatus.HasValue)
        {
            // Echo anything we receive
            await webSocket.SendAsync(new ArraySegment<byte>(buffer, 0, received.Count), 
                received.MessageType, received.EndOfMessage, CancellationToken.None);

            received = await webSocket.ReceiveAsync(new ArraySegment<byte>(buffer), 
                CancellationToken.None);
        }

        await webSocket.CloseAsync(webSocket.CloseStatus.Value, 
            webSocket.CloseStatusDescription, CancellationToken.None);
    }
}
```

<span data-ttu-id="e2daf-143">이 [샘플](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/owin/sample) 동일한을 사용 하도록 구성 `NowinServer` 는 이전 쿼리에서와-응용 프로그램의 구성 되는 방식에서 유일한 차이점은 해당 `Configure` 메서드.</span><span class="sxs-lookup"><span data-stu-id="e2daf-143">This [sample](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/owin/sample) is configured using the same `NowinServer` as the previous one - the only difference is in how the application is configured in its `Configure` method.</span></span> <span data-ttu-id="e2daf-144">사용 하 여 테스트 [간단한 websocket 클라이언트가](https://chrome.google.com/webstore/detail/simple-websocket-client/pfdhoblngboilpfeibdedpjgfnlcodoo?hl=en) 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-144">A test using [a simple websocket client](https://chrome.google.com/webstore/detail/simple-websocket-client/pfdhoblngboilpfeibdedpjgfnlcodoo?hl=en) demonstrates  the application:</span></span>

![웹 소켓 테스트 클라이언트](owin/_static/websocket-test.png)

## <a name="owin-environment"></a><span data-ttu-id="e2daf-146">OWIN 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-146">OWIN environment</span></span>

<span data-ttu-id="e2daf-147">사용 하 여 OWIN 환경을 구성할 수는 `HttpContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-147">You can construct a OWIN environment using the `HttpContext`.</span></span>

```csharp

   var environment = new OwinEnvironment(HttpContext);
   var features = new OwinFeatureCollection(environment);
   ```

## <a name="owin-keys"></a><span data-ttu-id="e2daf-148">OWIN 키</span><span class="sxs-lookup"><span data-stu-id="e2daf-148">OWIN keys</span></span>

<span data-ttu-id="e2daf-149">OWIN에 따라 달라 집니다는 `IDictionary<string,object>` HTTP 요청/응답 exchange 전체에서 정보를 전달 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-149">OWIN depends on an `IDictionary<string,object>` object to communicate information throughout an HTTP Request/Response exchange.</span></span> <span data-ttu-id="e2daf-150">ASP.NET Core 아래에 나열 된 키를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-150">ASP.NET Core implements the keys listed below.</span></span> <span data-ttu-id="e2daf-151">참조는 [기본 사양, 확장명](http://owin.org/#spec), 및 [OWIN 키 지침 및 공통 키](http://owin.org/spec/spec/CommonKeys.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2daf-151">See the [primary specification, extensions](http://owin.org/#spec), and [OWIN Key Guidelines and Common Keys](http://owin.org/spec/spec/CommonKeys.html).</span></span>

### <a name="request-data-owin-v100"></a><span data-ttu-id="e2daf-152">요청 데이터 (OWIN v1.0.0)</span><span class="sxs-lookup"><span data-stu-id="e2daf-152">Request Data (OWIN v1.0.0)</span></span>

| <span data-ttu-id="e2daf-153">Key</span><span class="sxs-lookup"><span data-stu-id="e2daf-153">Key</span></span>               | <span data-ttu-id="e2daf-154">값 (형식)</span><span class="sxs-lookup"><span data-stu-id="e2daf-154">Value (type)</span></span> | <span data-ttu-id="e2daf-155">설명</span><span class="sxs-lookup"><span data-stu-id="e2daf-155">Description</span></span> |
| ----------------- | ------------ | ----------- |
| <span data-ttu-id="e2daf-156">owin.RequestScheme</span><span class="sxs-lookup"><span data-stu-id="e2daf-156">owin.RequestScheme</span></span> | `String` |  |
| <span data-ttu-id="e2daf-157">owin.RequestMethod</span><span class="sxs-lookup"><span data-stu-id="e2daf-157">owin.RequestMethod</span></span>  | `String` | |    
| <span data-ttu-id="e2daf-158">owin.RequestPathBase</span><span class="sxs-lookup"><span data-stu-id="e2daf-158">owin.RequestPathBase</span></span>  | `String` | |    
| <span data-ttu-id="e2daf-159">owin.RequestPath</span><span class="sxs-lookup"><span data-stu-id="e2daf-159">owin.RequestPath</span></span> | `String` | |     
| <span data-ttu-id="e2daf-160">owin.RequestQueryString</span><span class="sxs-lookup"><span data-stu-id="e2daf-160">owin.RequestQueryString</span></span>  | `String` | |    
| <span data-ttu-id="e2daf-161">owin.RequestProtocol</span><span class="sxs-lookup"><span data-stu-id="e2daf-161">owin.RequestProtocol</span></span>  | `String` | |    
| <span data-ttu-id="e2daf-162">owin.RequestHeaders</span><span class="sxs-lookup"><span data-stu-id="e2daf-162">owin.RequestHeaders</span></span> | `IDictionary<string,string[]>`  | |
| <span data-ttu-id="e2daf-163">owin.RequestBody</span><span class="sxs-lookup"><span data-stu-id="e2daf-163">owin.RequestBody</span></span> | `Stream`  | |

### <a name="request-data-owin-v110"></a><span data-ttu-id="e2daf-164">요청 데이터 (OWIN v1.1.0)</span><span class="sxs-lookup"><span data-stu-id="e2daf-164">Request Data (OWIN v1.1.0)</span></span>

| <span data-ttu-id="e2daf-165">Key</span><span class="sxs-lookup"><span data-stu-id="e2daf-165">Key</span></span>               | <span data-ttu-id="e2daf-166">값 (형식)</span><span class="sxs-lookup"><span data-stu-id="e2daf-166">Value (type)</span></span> | <span data-ttu-id="e2daf-167">설명</span><span class="sxs-lookup"><span data-stu-id="e2daf-167">Description</span></span> |
| ----------------- | ------------ | ----------- |
| <span data-ttu-id="e2daf-168">owin.RequestId</span><span class="sxs-lookup"><span data-stu-id="e2daf-168">owin.RequestId</span></span> | `String` | <span data-ttu-id="e2daf-169">Optional</span><span class="sxs-lookup"><span data-stu-id="e2daf-169">Optional</span></span> |

### <a name="response-data-owin-v100"></a><span data-ttu-id="e2daf-170">응답 데이터 (OWIN v1.0.0)</span><span class="sxs-lookup"><span data-stu-id="e2daf-170">Response Data (OWIN v1.0.0)</span></span>

| <span data-ttu-id="e2daf-171">Key</span><span class="sxs-lookup"><span data-stu-id="e2daf-171">Key</span></span>               | <span data-ttu-id="e2daf-172">값 (형식)</span><span class="sxs-lookup"><span data-stu-id="e2daf-172">Value (type)</span></span> | <span data-ttu-id="e2daf-173">설명</span><span class="sxs-lookup"><span data-stu-id="e2daf-173">Description</span></span> |
| ----------------- | ------------ | ----------- |
| <span data-ttu-id="e2daf-174">owin.ResponseStatusCode</span><span class="sxs-lookup"><span data-stu-id="e2daf-174">owin.ResponseStatusCode</span></span> | `int` | <span data-ttu-id="e2daf-175">Optional</span><span class="sxs-lookup"><span data-stu-id="e2daf-175">Optional</span></span> |
| <span data-ttu-id="e2daf-176">owin.ResponseReasonPhrase</span><span class="sxs-lookup"><span data-stu-id="e2daf-176">owin.ResponseReasonPhrase</span></span> | `String` | <span data-ttu-id="e2daf-177">Optional</span><span class="sxs-lookup"><span data-stu-id="e2daf-177">Optional</span></span> |
| <span data-ttu-id="e2daf-178">owin.ResponseHeaders</span><span class="sxs-lookup"><span data-stu-id="e2daf-178">owin.ResponseHeaders</span></span> | `IDictionary<string,string[]>`  | |
| <span data-ttu-id="e2daf-179">owin.ResponseBody</span><span class="sxs-lookup"><span data-stu-id="e2daf-179">owin.ResponseBody</span></span> | `Stream`  | |


### <a name="other-data-owin-v100"></a><span data-ttu-id="e2daf-180">다른 데이터 (OWIN v1.0.0)</span><span class="sxs-lookup"><span data-stu-id="e2daf-180">Other Data (OWIN v1.0.0)</span></span>

| <span data-ttu-id="e2daf-181">Key</span><span class="sxs-lookup"><span data-stu-id="e2daf-181">Key</span></span>               | <span data-ttu-id="e2daf-182">값 (형식)</span><span class="sxs-lookup"><span data-stu-id="e2daf-182">Value (type)</span></span> | <span data-ttu-id="e2daf-183">설명</span><span class="sxs-lookup"><span data-stu-id="e2daf-183">Description</span></span> |
| ----------------- | ------------ | ----------- |
| <span data-ttu-id="e2daf-184">owin.CallCancelled</span><span class="sxs-lookup"><span data-stu-id="e2daf-184">owin.CallCancelled</span></span> | `CancellationToken` |  |
| <span data-ttu-id="e2daf-185">owin.Version</span><span class="sxs-lookup"><span data-stu-id="e2daf-185">owin.Version</span></span>  | `String` | |   


### <a name="common-keys"></a><span data-ttu-id="e2daf-186">공통 키</span><span class="sxs-lookup"><span data-stu-id="e2daf-186">Common Keys</span></span>

| <span data-ttu-id="e2daf-187">Key</span><span class="sxs-lookup"><span data-stu-id="e2daf-187">Key</span></span>               | <span data-ttu-id="e2daf-188">값 (형식)</span><span class="sxs-lookup"><span data-stu-id="e2daf-188">Value (type)</span></span> | <span data-ttu-id="e2daf-189">설명</span><span class="sxs-lookup"><span data-stu-id="e2daf-189">Description</span></span> |
| ----------------- | ------------ | ----------- |
| <span data-ttu-id="e2daf-190">ssl.ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="e2daf-190">ssl.ClientCertificate</span></span> | `X509Certificate` |  |
| <span data-ttu-id="e2daf-191">ssl.LoadClientCertAsync</span><span class="sxs-lookup"><span data-stu-id="e2daf-191">ssl.LoadClientCertAsync</span></span>  | `Func<Task>` | |    
| <span data-ttu-id="e2daf-192">server.RemoteIpAddress</span><span class="sxs-lookup"><span data-stu-id="e2daf-192">server.RemoteIpAddress</span></span>  | `String` | |    
| <span data-ttu-id="e2daf-193">server.RemotePort</span><span class="sxs-lookup"><span data-stu-id="e2daf-193">server.RemotePort</span></span> | `String` | |     
| <span data-ttu-id="e2daf-194">server.LocalIpAddress</span><span class="sxs-lookup"><span data-stu-id="e2daf-194">server.LocalIpAddress</span></span>  | `String` | |    
| <span data-ttu-id="e2daf-195">server.LocalPort</span><span class="sxs-lookup"><span data-stu-id="e2daf-195">server.LocalPort</span></span>  | `String` | |    
| <span data-ttu-id="e2daf-196">server.IsLocal</span><span class="sxs-lookup"><span data-stu-id="e2daf-196">server.IsLocal</span></span>  | `bool` | |    
| <span data-ttu-id="e2daf-197">server.OnSendingHeaders</span><span class="sxs-lookup"><span data-stu-id="e2daf-197">server.OnSendingHeaders</span></span>  | `Action<Action<object>,object>` | |


### <a name="sendfiles-v030"></a><span data-ttu-id="e2daf-198">SendFiles v0.3.0</span><span class="sxs-lookup"><span data-stu-id="e2daf-198">SendFiles v0.3.0</span></span>

| <span data-ttu-id="e2daf-199">Key</span><span class="sxs-lookup"><span data-stu-id="e2daf-199">Key</span></span>               | <span data-ttu-id="e2daf-200">값 (형식)</span><span class="sxs-lookup"><span data-stu-id="e2daf-200">Value (type)</span></span> | <span data-ttu-id="e2daf-201">설명</span><span class="sxs-lookup"><span data-stu-id="e2daf-201">Description</span></span> |
| ----------------- | ------------ | ----------- |
| <span data-ttu-id="e2daf-202">sendfile.SendAsync</span><span class="sxs-lookup"><span data-stu-id="e2daf-202">sendfile.SendAsync</span></span> | <span data-ttu-id="e2daf-203">참조 [대리자 시그니처](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span><span class="sxs-lookup"><span data-stu-id="e2daf-203">See [delegate signature](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span></span> | <span data-ttu-id="e2daf-204">요청에 따라</span><span class="sxs-lookup"><span data-stu-id="e2daf-204">Per Request</span></span> |


### <a name="opaque-v030"></a><span data-ttu-id="e2daf-205">불투명 v0.3.0</span><span class="sxs-lookup"><span data-stu-id="e2daf-205">Opaque v0.3.0</span></span>

| <span data-ttu-id="e2daf-206">Key</span><span class="sxs-lookup"><span data-stu-id="e2daf-206">Key</span></span>               | <span data-ttu-id="e2daf-207">값 (형식)</span><span class="sxs-lookup"><span data-stu-id="e2daf-207">Value (type)</span></span> | <span data-ttu-id="e2daf-208">설명</span><span class="sxs-lookup"><span data-stu-id="e2daf-208">Description</span></span> |
| ----------------- | ------------ | ----------- |
| <span data-ttu-id="e2daf-209">opaque.Version</span><span class="sxs-lookup"><span data-stu-id="e2daf-209">opaque.Version</span></span> | `String` |  |
| <span data-ttu-id="e2daf-210">opaque.Upgrade</span><span class="sxs-lookup"><span data-stu-id="e2daf-210">opaque.Upgrade</span></span> | `OpaqueUpgrade` | <span data-ttu-id="e2daf-211">참조 [대리자 시그니처](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span><span class="sxs-lookup"><span data-stu-id="e2daf-211">See [delegate signature](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span></span> |
| <span data-ttu-id="e2daf-212">opaque.Stream</span><span class="sxs-lookup"><span data-stu-id="e2daf-212">opaque.Stream</span></span> | `Stream` |  |
| <span data-ttu-id="e2daf-213">opaque.CallCancelled</span><span class="sxs-lookup"><span data-stu-id="e2daf-213">opaque.CallCancelled</span></span> | `CancellationToken` |  |


### <a name="websocket-v030"></a><span data-ttu-id="e2daf-214">WebSocket v0.3.0</span><span class="sxs-lookup"><span data-stu-id="e2daf-214">WebSocket v0.3.0</span></span>

| <span data-ttu-id="e2daf-215">Key</span><span class="sxs-lookup"><span data-stu-id="e2daf-215">Key</span></span>               | <span data-ttu-id="e2daf-216">값 (형식)</span><span class="sxs-lookup"><span data-stu-id="e2daf-216">Value (type)</span></span> | <span data-ttu-id="e2daf-217">설명</span><span class="sxs-lookup"><span data-stu-id="e2daf-217">Description</span></span> |
| ----------------- | ------------ | ----------- |
| <span data-ttu-id="e2daf-218">websocket.Version</span><span class="sxs-lookup"><span data-stu-id="e2daf-218">websocket.Version</span></span> | `String` |  |
| <span data-ttu-id="e2daf-219">websocket.Accept</span><span class="sxs-lookup"><span data-stu-id="e2daf-219">websocket.Accept</span></span> | `WebSocketAccept` | <span data-ttu-id="e2daf-220">참조 [대리자 시그니처](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span><span class="sxs-lookup"><span data-stu-id="e2daf-220">See [delegate signature](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span></span> |
| <span data-ttu-id="e2daf-221">websocket.AcceptAlt</span><span class="sxs-lookup"><span data-stu-id="e2daf-221">websocket.AcceptAlt</span></span> |  | <span data-ttu-id="e2daf-222">비-사양</span><span class="sxs-lookup"><span data-stu-id="e2daf-222">Non-spec</span></span> |
| <span data-ttu-id="e2daf-223">websocket.SubProtocol</span><span class="sxs-lookup"><span data-stu-id="e2daf-223">websocket.SubProtocol</span></span> | `String` | <span data-ttu-id="e2daf-224">참조 [RFC6455 섹션 4.2.2](https://tools.ietf.org/html/rfc6455#section-4.2.2) 5.5 단계</span><span class="sxs-lookup"><span data-stu-id="e2daf-224">See [RFC6455 Section 4.2.2](https://tools.ietf.org/html/rfc6455#section-4.2.2) Step 5.5</span></span> |
| <span data-ttu-id="e2daf-225">websocket.SendAsync</span><span class="sxs-lookup"><span data-stu-id="e2daf-225">websocket.SendAsync</span></span> | `WebSocketSendAsync` | <span data-ttu-id="e2daf-226">참조 [대리자 시그니처](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span><span class="sxs-lookup"><span data-stu-id="e2daf-226">See [delegate signature](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span></span>  |
| <span data-ttu-id="e2daf-227">websocket.ReceiveAsync</span><span class="sxs-lookup"><span data-stu-id="e2daf-227">websocket.ReceiveAsync</span></span> | `WebSocketReceiveAsync` | <span data-ttu-id="e2daf-228">참조 [대리자 시그니처](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span><span class="sxs-lookup"><span data-stu-id="e2daf-228">See [delegate signature](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span></span>  |
| <span data-ttu-id="e2daf-229">websocket.CloseAsync</span><span class="sxs-lookup"><span data-stu-id="e2daf-229">websocket.CloseAsync</span></span> | `WebSocketCloseAsync` | <span data-ttu-id="e2daf-230">참조 [대리자 시그니처](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span><span class="sxs-lookup"><span data-stu-id="e2daf-230">See [delegate signature](http://owin.org/spec/extensions/owin-SendFile-Extension-v0.3.0.htm)</span></span>  |
| <span data-ttu-id="e2daf-231">websocket.CallCancelled</span><span class="sxs-lookup"><span data-stu-id="e2daf-231">websocket.CallCancelled</span></span> | `CancellationToken` |  |
| <span data-ttu-id="e2daf-232">websocket.ClientCloseStatus</span><span class="sxs-lookup"><span data-stu-id="e2daf-232">websocket.ClientCloseStatus</span></span> | `int` | <span data-ttu-id="e2daf-233">Optional</span><span class="sxs-lookup"><span data-stu-id="e2daf-233">Optional</span></span> |
| <span data-ttu-id="e2daf-234">websocket.ClientCloseDescription</span><span class="sxs-lookup"><span data-stu-id="e2daf-234">websocket.ClientCloseDescription</span></span> | `String` | <span data-ttu-id="e2daf-235">Optional</span><span class="sxs-lookup"><span data-stu-id="e2daf-235">Optional</span></span> |


## <a name="additional-resources"></a><span data-ttu-id="e2daf-236">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="e2daf-236">Additional Resources</span></span>

* [<span data-ttu-id="e2daf-237">미들웨어</span><span class="sxs-lookup"><span data-stu-id="e2daf-237">Middleware</span></span>](middleware.md)

* [<span data-ttu-id="e2daf-238">서버</span><span class="sxs-lookup"><span data-stu-id="e2daf-238">Servers</span></span>](servers/index.md)
