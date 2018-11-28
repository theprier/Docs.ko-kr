---
title: 확장을 위해 ASP.NET Core SignalR 백플레인으로 redis
author: tdykstra
description: Redis 백플레인 ASP.NET Core SignalR 앱에 대 한 확장을 사용 하도록 설정 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 11/28/2018
uid: signalr/redis-backplane
ms.openlocfilehash: c8b09c0d482da344b54d167c0c9757167eaa6186
ms.sourcegitcommit: e9b99854b0a8021dafabee0db5e1338067f250a9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52452986"
---
# <a name="set-up-a-redis-backplane-for-aspnet-core-signalr-scale-out"></a><span data-ttu-id="96876-103">ASP.NET Core SignalR 확장에 대 한를 Redis 백플레인으로 설정</span><span class="sxs-lookup"><span data-stu-id="96876-103">Set up a Redis backplane for ASP.NET Core SignalR scale-out</span></span>

<span data-ttu-id="96876-104">하 여 [Andrew Stanton-nurse](https://twitter.com/anurse)하십시오 [Brady Gaster](https://twitter.com/bradygaster), 및 [Tom Dykstra](https://github.com/tdykstra),</span><span class="sxs-lookup"><span data-stu-id="96876-104">By [Andrew Stanton-Nurse](https://twitter.com/anurse), [Brady Gaster](https://twitter.com/bradygaster), and [Tom Dykstra](https://github.com/tdykstra),</span></span>

<span data-ttu-id="96876-105">이 문서에서는 설정의 SignalR 특정 측면을 설명 된 [Redis](https://redis.io/) 는 ASP.NET Core SignalR 앱 크기 조정에 사용할 서버를 합니다.</span><span class="sxs-lookup"><span data-stu-id="96876-105">This article explains SignalR-specific aspects of setting up a [Redis](https://redis.io/) server to use for scaling out an ASP.NET Core SignalR app.</span></span>

## <a name="set-up-a-redis-backplane"></a><span data-ttu-id="96876-106">Redis 백플레인 설정</span><span class="sxs-lookup"><span data-stu-id="96876-106">Set up a Redis backplane</span></span>

* <span data-ttu-id="96876-107">Redis 서버를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="96876-107">Deploy a Redis server.</span></span>

  <span data-ttu-id="96876-108">프로덕션 사용에 대 한 Redis 백플레인 온-프레미스 인프라에만 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96876-108">For production use, a Redis backplane is recommended only for on-premises infrastructure.</span></span> <span data-ttu-id="96876-109">대기 시간을 최소화 하려면 Redis 서버가 SignalR 앱과 동일한 데이터 센터에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96876-109">To minimize latency, the Redis server should be in the same data center as the SignalR app.</span></span> <span data-ttu-id="96876-110">SignalR 앱은 Azure 클라우드에서 실행 중인 경우 Azure SignalR Service를 Redis 백플레인으로 대신 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="96876-110">If your SignalR app is running in the Azure cloud, we recommend Azure SignalR Service instead of a Redis backplane.</span></span> <span data-ttu-id="96876-111">Azure Redis Cache Service를 사용 하 여 개발 및 테스트 환경 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96876-111">You can use the Azure Redis Cache Service for development and test environments.</span></span> <span data-ttu-id="96876-112">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="96876-112">For more information, see the following resources:</span></span>

  * <xref:signalr/scale>
  * [<span data-ttu-id="96876-113">Redis 설명서</span><span class="sxs-lookup"><span data-stu-id="96876-113">Redis documentation</span></span>](https://redis.io/)
  * [<span data-ttu-id="96876-114">Azure Redis Cache 설명서</span><span class="sxs-lookup"><span data-stu-id="96876-114">Azure Redis Cache documentation</span></span>](https://docs.microsoft.com/en-us/azure/redis-cache/)

::: moniker range="= aspnetcore-2.1"

* <span data-ttu-id="96876-115">SignalR 앱을 설치 합니다 `Microsoft.AspNetCore.SignalR.Redis` NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="96876-115">In the SignalR app, install the `Microsoft.AspNetCore.SignalR.Redis` NuGet package.</span></span>

* <span data-ttu-id="96876-116">에 `Startup.ConfigureServices` 메서드를 호출 `AddRedis` 후 `AddSignalR`:</span><span class="sxs-lookup"><span data-stu-id="96876-116">In the `Startup.ConfigureServices` method, call `AddRedis` after `AddSignalR`:</span></span>

  ```csharp
  services.AddSignalR().AddRedis("<your_Redis_connection_string>");
  ```

* <span data-ttu-id="96876-117">필요에 따라 옵션을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="96876-117">Configure options as needed:</span></span>
 
  <span data-ttu-id="96876-118">연결 문자열 또는 대부분의 옵션을 설정할 수 있습니다 합니다 [ConfigurationOptions](https://stackexchange.github.io/StackExchange.Redis/Configuration#configuration-options) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="96876-118">Most options can be set in the connection string or in the [ConfigurationOptions](https://stackexchange.github.io/StackExchange.Redis/Configuration#configuration-options) object.</span></span> <span data-ttu-id="96876-119">에 지정 된 옵션 `ConfigurationOptions` 연결 문자열에 설정 하는 것을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="96876-119">Options specified in `ConfigurationOptions` override the ones set in the connection string.</span></span>

  <span data-ttu-id="96876-120">다음 예제에서 옵션을 설정 하는 방법을 보여 줍니다는 `ConfigurationOptions` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="96876-120">The following example shows how to set options in the `ConfigurationOptions` object.</span></span> <span data-ttu-id="96876-121">이 예제에서는 채널 접두사를 여러 앱에서 동일한 Redis 인스턴스를 공유할 수 있도록 다음 단계에 설명 된 대로</span><span class="sxs-lookup"><span data-stu-id="96876-121">This example adds a channel prefix so that multiple apps can share the same Redis instance, as explained in the following step.</span></span>

  ```csharp
  services.AddSignalR()
    .AddRedis(connectionString, options => {
        options.Configuration.ChannelPrefix = "MyApp";
    });
  ```

  <span data-ttu-id="96876-122">위의 코드에서 `options.Configuration` 연결 문자열에 지정 된 항목으로 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96876-122">In the preceding code, `options.Configuration` is initialized with whatever was specified in the connection string.</span></span>

::: moniker-end

::: moniker range="> aspnetcore-2.1"

* <span data-ttu-id="96876-123">SignalR 앱을 설치 합니다 `Microsoft.AspNetCore.SignalR.StackExchangeRedis` NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="96876-123">In the SignalR app, install the `Microsoft.AspNetCore.SignalR.StackExchangeRedis` NuGet package.</span></span>

* <span data-ttu-id="96876-124">에 `Startup.ConfigureServices` 메서드를 호출 `AddStackExchangeRedis` 후 `AddSignalR`:</span><span class="sxs-lookup"><span data-stu-id="96876-124">In the `Startup.ConfigureServices` method, call `AddStackExchangeRedis` after `AddSignalR`:</span></span>

  ```csharp
  services.AddSignalR().AddStackExchangeRedis("<your_Redis_connection_string>");
  ```

* <span data-ttu-id="96876-125">필요에 따라 옵션을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="96876-125">Configure options as needed:</span></span>
 
  <span data-ttu-id="96876-126">연결 문자열 또는 대부분의 옵션을 설정할 수 있습니다 합니다 [ConfigurationOptions](https://stackexchange.github.io/StackExchange.Redis/Configuration#configuration-options) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="96876-126">Most options can be set in the connection string or in the [ConfigurationOptions](https://stackexchange.github.io/StackExchange.Redis/Configuration#configuration-options) object.</span></span> <span data-ttu-id="96876-127">에 지정 된 옵션 `ConfigurationOptions` 연결 문자열에 설정 하는 것을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="96876-127">Options specified in `ConfigurationOptions` override the ones set in the connection string.</span></span>

  <span data-ttu-id="96876-128">다음 예제에서 옵션을 설정 하는 방법을 보여 줍니다는 `ConfigurationOptions` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="96876-128">The following example shows how to set options in the `ConfigurationOptions` object.</span></span> <span data-ttu-id="96876-129">이 예제에서는 채널 접두사를 여러 앱에서 동일한 Redis 인스턴스를 공유할 수 있도록 다음 단계에 설명 된 대로</span><span class="sxs-lookup"><span data-stu-id="96876-129">This example adds a channel prefix so that multiple apps can share the same Redis instance, as explained in the following step.</span></span>

  ```csharp
  services.AddSignalR()
    .AddStackExchangeRedis(connectionString, options => {
        options.Configuration.ChannelPrefix = "MyApp";
    });
  ```

  <span data-ttu-id="96876-130">위의 코드에서 `options.Configuration` 연결 문자열에 지정 된 항목으로 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96876-130">In the preceding code, `options.Configuration` is initialized with whatever was specified in the connection string.</span></span>

  <span data-ttu-id="96876-131">Redis 옵션에 대 한 자세한 내용은 참조는 [StackExchange Redis 설명서](https://stackexchange.github.io/StackExchange.Redis/Configuration.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="96876-131">For information about Redis options, see the [StackExchange Redis documentation](https://stackexchange.github.io/StackExchange.Redis/Configuration.html).</span></span>

::: moniker-end

* <span data-ttu-id="96876-132">Redis 서버 하나를 여러 SignalR 앱에 대 한 사용 하는 경우 각 SignalR 앱에 대 한 다양 한 채널 접두사를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="96876-132">If you're using one Redis server for multiple SignalR apps, use a different channel prefix for each SignalR app.</span></span>

  <span data-ttu-id="96876-133">다른 채널 접두사를 사용 하는 다른 사용자 로부터 하나의 SignalR 앱을 격리 채널 접두사를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="96876-133">Setting a channel prefix isolates one SignalR app from others that use different channel prefixes.</span></span> <span data-ttu-id="96876-134">서로 다른 접두사를 할당 하지 않으면, 모든 자체 클라이언트로 하나의 앱에서 보낸 메시지를 백플레인으로 Redis 서버를 사용 하는 모든 앱의 모든 클라이언트에 전환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96876-134">If you don't assign different prefixes, a message sent from one app to all of its own clients will go to all clients of all apps that use the Redis server as a backplane.</span></span>

* <span data-ttu-id="96876-135">서버 팜 부하 분산 고정 세션에 대 한 소프트웨어를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="96876-135">Configure your server farm load balancing software for sticky sessions.</span></span> <span data-ttu-id="96876-136">그렇게 하는 방법에 대 한 설명서의 몇 가지 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="96876-136">Here are some examples of documentation on how to do that:</span></span>

  * [<span data-ttu-id="96876-137">IIS</span><span class="sxs-lookup"><span data-stu-id="96876-137">IIS</span></span>](/iis/extensions/configuring-application-request-routing-arr/http-load-balancing-using-application-request-routing)
  * [<span data-ttu-id="96876-138">HAProxy</span><span class="sxs-lookup"><span data-stu-id="96876-138">HAProxy</span></span>](https://www.haproxy.com/blog/load-balancing-affinity-persistence-sticky-sessions-what-you-need-to-know/)
  * [<span data-ttu-id="96876-139">Nginx</span><span class="sxs-lookup"><span data-stu-id="96876-139">Nginx</span></span>](https://docs.nginx.com/nginx/admin-guide/load-balancer/http-load-balancer/#sticky)
  * [<span data-ttu-id="96876-140">pfSense</span><span class="sxs-lookup"><span data-stu-id="96876-140">pfSense</span></span>](https://www.netgate.com/docs/pfsense/loadbalancing/inbound-load-balancing.html#sticky-connections)

## <a name="redis-server-errors"></a><span data-ttu-id="96876-141">Redis 서버 오류</span><span class="sxs-lookup"><span data-stu-id="96876-141">Redis server errors</span></span>

<span data-ttu-id="96876-142">Redis 서버 다운 되 면 SignalR 메시지를 배달할 수 없습니다를 나타내는 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="96876-142">When a Redis server goes down, SignalR throws exceptions that indicate messages won't be delivered.</span></span> <span data-ttu-id="96876-143">몇 가지 일반적인 예외 메시지:</span><span class="sxs-lookup"><span data-stu-id="96876-143">Some typical exception messages:</span></span>

* <span data-ttu-id="96876-144">*실패 한 쓰기 메시지*</span><span class="sxs-lookup"><span data-stu-id="96876-144">*Failed writing message*</span></span>
* <span data-ttu-id="96876-145">*'MethodName' 허브 메서드를 호출 하지 못했습니다.*</span><span class="sxs-lookup"><span data-stu-id="96876-145">*Failed to invoke hub method 'MethodName'*</span></span>
* <span data-ttu-id="96876-146">*Redis에 연결 하지 못했습니다.*</span><span class="sxs-lookup"><span data-stu-id="96876-146">*Connection to Redis failed*</span></span>

<span data-ttu-id="96876-147">SignalR은 서버가 다시 작동 하는 경우 보낼 메시지를 버퍼링 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96876-147">SignalR doesn't buffer messages to send them when the server comes back up.</span></span> <span data-ttu-id="96876-148">Redis 서버가 다운 된 동안 전송 된 모든 메시지는 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96876-148">Any messages sent while the Redis server is down are lost.</span></span>

<span data-ttu-id="96876-149">SignalR에는 Redis 서버를 다시 사용할 때 자동으로 다시 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="96876-149">SignalR automatically reconnects when the Redis server is available again.</span></span>

### <a name="custom-behavior-for-connection-failures"></a><span data-ttu-id="96876-150">연결 실패에 대 한 사용자 지정 동작</span><span class="sxs-lookup"><span data-stu-id="96876-150">Custom behavior for connection failures</span></span>

<span data-ttu-id="96876-151">Redis 연결 실패 이벤트를 처리 하는 방법을 보여 주는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="96876-151">Here's an example that shows how to handle Redis connection failure events.</span></span>

::: moniker range="= aspnetcore-2.1"

```csharp
services.AddSignalR()
        .AddRedis(o =>
        {
            o.ConnectionFactory = async writer =>
            {
                var config = new ConfigurationOptions
                {
                    AbortOnConnectFail = false
                };
                config.EndPoints.Add(IPAddress.Loopback, 0);
                config.SetDefaultPorts();
                var connection = await ConnectionMultiplexer.ConnectAsync(config, writer);
                connection.ConnectionFailed += (_, e) =>
                {
                    Console.WriteLine("Connection to Redis failed.");
                };

                if (!connection.IsConnected)
                {
                    Console.WriteLine("Did not connect to Redis.");
                }

                return connection;
            };
        });
```

::: moniker-end

::: moniker range="> aspnetcore-2.1"

```csharp
services.AddSignalR()
        .AddMessagePackProtocol()
        .AddStackExchangeRedis(o =>
        {
            o.ConnectionFactory = async writer =>
            {
                var config = new ConfigurationOptions
                {
                    AbortOnConnectFail = false
                };
                config.EndPoints.Add(IPAddress.Loopback, 0);
                config.SetDefaultPorts();
                var connection = await ConnectionMultiplexer.ConnectAsync(config, writer);
                connection.ConnectionFailed += (_, e) =>
                {
                    Console.WriteLine("Connection to Redis failed.");
                };

                if (!connection.IsConnected)
                {
                    Console.WriteLine("Did not connect to Redis.");
                }

                return connection;
            };
        });
```

::: moniker-end

## <a name="clustering"></a><span data-ttu-id="96876-152">클러스터링</span><span class="sxs-lookup"><span data-stu-id="96876-152">Clustering</span></span>

<span data-ttu-id="96876-153">클러스터링은 여러 Redis 서버를 사용 하 여 고가용성을 달성 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="96876-153">Clustering is a method for achieving high availability by using multiple Redis servers.</span></span> <span data-ttu-id="96876-154">공식적으로 지원 되지 않으면 클러스터링 하지만 작동 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96876-154">Clustering isn't officially supported, but it might work.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96876-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="96876-155">Next steps</span></span>

<span data-ttu-id="96876-156">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="96876-156">For more information, see the following resources:</span></span>

* <xref:signalr/scale>
* [<span data-ttu-id="96876-157">Redis 설명서</span><span class="sxs-lookup"><span data-stu-id="96876-157">Redis documentation</span></span>](https://redis.io/documentation)
* [<span data-ttu-id="96876-158">StackExchange Redis 설명서</span><span class="sxs-lookup"><span data-stu-id="96876-158">StackExchange Redis documentation</span></span>](https://stackexchange.github.io/StackExchange.Redis/)
* [<span data-ttu-id="96876-159">Azure Redis Cache 설명서</span><span class="sxs-lookup"><span data-stu-id="96876-159">Azure Redis Cache documentation</span></span>](https://docs.microsoft.com/en-us/azure/redis-cache/)
