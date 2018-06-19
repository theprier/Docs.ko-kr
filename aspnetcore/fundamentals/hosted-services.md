---
title: ASP.NET Core에서 호스팅되는 서비스를 사용하는 백그라운드 작업
author: guardrex
description: ASP.NET Core에서 호스팅되는 서비스를 사용하는 백그라운드 작업을 구현하는 방법을 배웁니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 02/15/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/hosted-services
ms.openlocfilehash: 89e595fb6ef38745d7377fdaaf1780c64320efe3
ms.sourcegitcommit: d43c84c4c80527c85e49d53691b293669557a79d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/20/2018
ms.locfileid: "29374693"
---
# <a name="background-tasks-with-hosted-services-in-aspnet-core"></a><span data-ttu-id="3b565-103">ASP.NET Core에서 호스팅되는 서비스를 사용하는 백그라운드 작업</span><span class="sxs-lookup"><span data-stu-id="3b565-103">Background tasks with hosted services in ASP.NET Core</span></span>

<span data-ttu-id="3b565-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="3b565-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="3b565-105">ASP.NET Core에서 백그라운드 작업은 *호스팅되는 서비스*로 구현될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-105">In ASP.NET Core, background tasks can be implemented as *hosted services*.</span></span> <span data-ttu-id="3b565-106">호스티드 서비스는 [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) 인터페이스를 구현하는 백그라운드 작업 논리가 있는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-106">A hosted service is a class with background task logic that implements the [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) interface.</span></span> <span data-ttu-id="3b565-107">이 토픽에서는 세 가지 호스팅되는 서비스 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-107">This topic provides three hosted service examples:</span></span>

* <span data-ttu-id="3b565-108">타이머에서 실행되는 백그라운드 작업.</span><span class="sxs-lookup"><span data-stu-id="3b565-108">Background task that runs on a timer.</span></span>
* <span data-ttu-id="3b565-109">범위가 지정된 서비스를 활성화하는 호스팅되는 서비스.</span><span class="sxs-lookup"><span data-stu-id="3b565-109">Hosted service that activates a scoped service.</span></span> <span data-ttu-id="3b565-110">범위가 지정된 서비스는 종속성 주입을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-110">The scoped service can use dependency injection.</span></span>
* <span data-ttu-id="3b565-111">순차적으로 실행되는 대기 중인 백그라운드 작업.</span><span class="sxs-lookup"><span data-stu-id="3b565-111">Queued background tasks that run sequentially.</span></span>

<span data-ttu-id="3b565-112">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/hosted-services/samples/2.x)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="3b565-112">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/hosted-services/samples/2.x) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="ihostedservice-interface"></a><span data-ttu-id="3b565-113">IHostedService 인터페이스</span><span class="sxs-lookup"><span data-stu-id="3b565-113">IHostedService interface</span></span>

<span data-ttu-id="3b565-114">호스팅되는 서비스는 [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-114">Hosted services implement the [IHostedService](/dotnet/api/microsoft.extensions.hosting.ihostedservice) interface.</span></span> <span data-ttu-id="3b565-115">인터페이스는 호스트에 의해 관리되는 개체에 대한 두 가지 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-115">The interface defines two methods for objects that are managed by the host:</span></span>

* <span data-ttu-id="3b565-116">[StartAsync(CancellationToken)](/dotnet/api/microsoft.extensions.hosting.ihostedservice.startasync) - 서버가 시작되고 [IApplicationLifetime.ApplicationStarted](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.applicationstarted)가 트리거된 후에 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-116">[StartAsync(CancellationToken)](/dotnet/api/microsoft.extensions.hosting.ihostedservice.startasync) - Called after the server has started and [IApplicationLifetime.ApplicationStarted](/dotnet/api/microsoft.aspnetcore.hosting.iapplicationlifetime.applicationstarted) is triggered.</span></span> <span data-ttu-id="3b565-117">`StartAsync`에는 백그라운드 작업을 시작하는 논리가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-117">`StartAsync` contains the logic to start the background task.</span></span>

* <span data-ttu-id="3b565-118">[StopAsync(CancellationToken)](/dotnet/api/microsoft.extensions.hosting.ihostedservice.stopasync) - 호스트가 정상적으로 종료될 때 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-118">[StopAsync(CancellationToken)](/dotnet/api/microsoft.extensions.hosting.ihostedservice.stopasync) - Triggered when the host is performing a graceful shutdown.</span></span> <span data-ttu-id="3b565-119">`StopAsync`에는 백그라운드 작업을 종료하고 관리되지 않는 리소스를 삭제하는 논리가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-119">`StopAsync` contains the logic to end the background task and dispose of any unmanaged resources.</span></span> <span data-ttu-id="3b565-120">앱이 예기치 않게 종료된 경우(예: 앱의 프로세스가 실패한 경우), `StopAsync`가 호출되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-120">If the app shuts down unexpectedly (for example, the app's process fails), `StopAsync` might not be called.</span></span>

<span data-ttu-id="3b565-121">호스팅되는 서비스는 앱 시작 시 한 번 활성화되고 앱 종료 시 정상적으로 종료되는 싱글톤입니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-121">The hosted service is a singleton that's activated once at app startup and gracefully shutdown at app shutdown.</span></span> <span data-ttu-id="3b565-122">[IDisposable](/dotnet/api/system.idisposable)이 구현되면 서비스 컨테이너가 삭제될 때 리소스가 삭제될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-122">When [IDisposable](/dotnet/api/system.idisposable) is implemented, resources can be disposed when the service container is disposed.</span></span> <span data-ttu-id="3b565-123">백그라운드 작업을 실행하는 동안 오류가 발생하면 `StopAsync`가 호출되지 않아도 `Dispose`를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-123">If an error is thrown during background task execution, `Dispose` should be called even if `StopAsync` isn't called.</span></span>

## <a name="timed-background-tasks"></a><span data-ttu-id="3b565-124">시간이 지정된 백그라운드 작업</span><span class="sxs-lookup"><span data-stu-id="3b565-124">Timed background tasks</span></span>

<span data-ttu-id="3b565-125">시간이 지정된 백그라운드 작업은 [System.Threading.Timer](/dotnet/api/system.threading.timer) 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-125">A timed background task makes use of the [System.Threading.Timer](/dotnet/api/system.threading.timer) class.</span></span> <span data-ttu-id="3b565-126">타이머가 작업의 `DoWork` 메서드를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-126">The timer triggers the task's `DoWork` method.</span></span> <span data-ttu-id="3b565-127">서비스 컨테이너가 `Dispose`에서 삭제될 때 `StopAsync`에서 타이머가 비활성화되고 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-127">The timer is disabled on `StopAsync` and disposed when the service container is disposed on `Dispose`:</span></span>

[!code-csharp[](hosted-services/samples/2.x/Services/TimedHostedService.cs?name=snippet1&highlight=15-16,30,37)]

<span data-ttu-id="3b565-128">서비스는 `Startup.ConfigureServices`에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-128">The service is registered in `Startup.ConfigureServices`:</span></span>

[!code-csharp[](hosted-services/samples/2.x/Startup.cs?name=snippet1)]

## <a name="consuming-a-scoped-service-in-a-background-task"></a><span data-ttu-id="3b565-129">백그라운드 작업에서 범위가 지정된 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="3b565-129">Consuming a scoped service in a background task</span></span>

<span data-ttu-id="3b565-130">`IHostedService` 내에서 범위가 지정된 서비스를 사용하려면 범위를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-130">To use scoped services within an `IHostedService`, create a scope.</span></span> <span data-ttu-id="3b565-131">기본적으로 호스팅되는 서비스에 대한 범위는 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-131">No scope is created for a hosted service by default.</span></span>

<span data-ttu-id="3b565-132">범위가 지정된 백그라운드 작업 서비스에는 백그라운드 작업의 논리가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-132">The scoped background task service contains the background task's logic.</span></span> <span data-ttu-id="3b565-133">다음 예에서는 [ILogger](/dotnet/api/microsoft.extensions.logging.ilogger)가 서비스에 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-133">In the following example, [ILogger](/dotnet/api/microsoft.extensions.logging.ilogger) is injected into the service:</span></span>

[!code-csharp[](hosted-services/samples/2.x/Services/ScopedProcessingService.cs?name=snippet1)]

<span data-ttu-id="3b565-134">호스팅되는 서비스는 범위가 지정된 백그라운드 작업 서비스를 해결하여 `DoWork` 메서드를 호출하는 범위를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-134">The hosted service creates a scope to resolve the scoped background task service to call its `DoWork` method:</span></span>

[!code-csharp[](hosted-services/samples/2.x/Services/ConsumeScopedServiceHostedService.cs?name=snippet1&highlight=29-36)]

<span data-ttu-id="3b565-135">서비스는 `Startup.ConfigureServices`에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-135">The services are registered in `Startup.ConfigureServices`:</span></span>

[!code-csharp[](hosted-services/samples/2.x/Startup.cs?name=snippet2)]

## <a name="queued-background-tasks"></a><span data-ttu-id="3b565-136">대기 중인 백그라운드 작업</span><span class="sxs-lookup"><span data-stu-id="3b565-136">Queued background tasks</span></span>

<span data-ttu-id="3b565-137">백그라운드 작업 큐는 .NET 4.x [QueueBackgroundWorkItem](/dotnet/api/system.web.hosting.hostingenvironment.queuebackgroundworkitem)([ASP.NET Core 2.2용으로 기본 제공될 예정](https://github.com/aspnet/Hosting/issues/1280))을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-137">A background task queue is based on the .NET 4.x [QueueBackgroundWorkItem](/dotnet/api/system.web.hosting.hostingenvironment.queuebackgroundworkitem) ([tentatively scheduled to be built-in for ASP.NET Core 2.2](https://github.com/aspnet/Hosting/issues/1280)):</span></span>

[!code-csharp[](hosted-services/samples/2.x/Services/BackgroundTaskQueue.cs?name=snippet1)]

<span data-ttu-id="3b565-138">`QueueHostedService`에서 큐의 백그라운드 작업(`workItem`)이 큐에서 제거되고 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-138">In `QueueHostedService`, background tasks (`workItem`) in the queue are dequeued and executed:</span></span>

[!code-csharp[](hosted-services/samples/2.x/Services/QueuedHostedService.cs?name=snippet1&highlight=30-31,35)]

<span data-ttu-id="3b565-139">서비스는 `Startup.ConfigureServices`에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-139">The services are registered in `Startup.ConfigureServices`:</span></span>

[!code-csharp[](hosted-services/samples/2.x/Startup.cs?name=snippet3)]

<span data-ttu-id="3b565-140">인덱스 페이지 모델 클래스에서 `IBackgroundTaskQueue`가 생성자로 삽입되고 `Queue`에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-140">In the Index page model class, the `IBackgroundTaskQueue` is injected into the constructor and assigned to `Queue`:</span></span>

[!code-csharp[](hosted-services/samples/2.x/Pages/Index.cshtml.cs?name=snippet1)]

<span data-ttu-id="3b565-141">인덱스 페이지에서 **작업 추가** 단추를 선택하면 `OnPostAddTask` 메서드가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-141">When the **Add Task** button is selected on the Index page, the `OnPostAddTask` method is executed.</span></span> <span data-ttu-id="3b565-142">`QueueBackgroundWorkItem`이 호출되어 작업 항목을 큐에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3b565-142">`QueueBackgroundWorkItem` is called to enqueue the work item:</span></span>

[!code-csharp[](hosted-services/samples/2.x/Pages/Index.cshtml.cs?name=snippet2)]

## <a name="additional-resources"></a><span data-ttu-id="3b565-143">추가 자료</span><span class="sxs-lookup"><span data-stu-id="3b565-143">Additional resources</span></span>

* [<span data-ttu-id="3b565-144">IHostedService 및 BackgroundService 클래스를 사용하여 마이크로 서비스에서 백그라운드 작업 구현</span><span class="sxs-lookup"><span data-stu-id="3b565-144">Implement background tasks in microservices with IHostedService and the BackgroundService class</span></span>](/dotnet/standard/microservices-architecture/multi-container-microservice-net-applications/background-tasks-with-ihostedservice)
* [<span data-ttu-id="3b565-145">System.Threading.Timer</span><span class="sxs-lookup"><span data-stu-id="3b565-145">System.Threading.Timer</span></span>](/dotnet/api/system.threading.timer)
