---
title: ASP.NET Core를 사용하는 gRPC 서비스
author: juntaoluo
description: ASP.NET Core를 사용 하 여 gRPC 서비스를 작성 하는 경우에 기본 개념에 알아봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: johluo
ms.date: 03/08/2019
uid: grpc/aspnetcore
ms.openlocfilehash: 387c3134efc04bec740fc66a5ca4b84715264d35
ms.sourcegitcommit: 5f299daa7c8102d56a63b214b9a34cc4bc87bc42
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2019
ms.locfileid: "59515601"
---
# <a name="grpc-services-with-aspnet-core"></a><span data-ttu-id="967ec-103">ASP.NET Core를 사용하는 gRPC 서비스</span><span class="sxs-lookup"><span data-stu-id="967ec-103">gRPC services with ASP.NET Core</span></span>

<span data-ttu-id="967ec-104">이 문서에는 ASP.NET Core를 사용 하 여 gRPC 서비스를 사용 하 여 시작 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="967ec-104">This document shows how to get started with gRPC services using ASP.NET Core.</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-all-3.0.md)]

## <a name="get-started-with-grpc-service-in-aspnet-core"></a><span data-ttu-id="967ec-105">ASP.NET Core에서 gRPC 서비스 시작</span><span class="sxs-lookup"><span data-stu-id="967ec-105">Get started with gRPC service in ASP.NET Core</span></span>

[!INCLUDE[View or download sample code](~/includes/grpc/download.md)]

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="967ec-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="967ec-106">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="967ec-107">참조 [gRPC services 시작](xref:tutorials/grpc/grpc-start) gRPC 프로젝트를 만드는 방법에 대 한 자세한 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="967ec-107">See [Get started with gRPC services](xref:tutorials/grpc/grpc-start) for detailed instructions on how to create a gRPC project.</span></span>

# <a name="visual-studio-code--visual-studio-for-mactabvisual-studio-codevisual-studio-mac"></a>[<span data-ttu-id="967ec-108">Visual Studio Code / Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="967ec-108">Visual Studio Code / Visual Studio for Mac</span></span>](#tab/visual-studio-code+visual-studio-mac)

<span data-ttu-id="967ec-109">명령줄에서 `dotnet new grpc -o GrpcGreeter`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="967ec-109">Run `dotnet new grpc -o GrpcGreeter` from the command line.</span></span>

---

## <a name="add-grpc-services-to-an-aspnet-core-app"></a><span data-ttu-id="967ec-110">ASP.NET Core 앱에 gRPC 서비스 추가</span><span class="sxs-lookup"><span data-stu-id="967ec-110">Add gRPC services to an ASP.NET Core app</span></span>

<span data-ttu-id="967ec-111">gRPC는 다음 패키지가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="967ec-111">gRPC requires the following packages:</span></span>

* [<span data-ttu-id="967ec-112">Grpc.AspNetCore.Server</span><span class="sxs-lookup"><span data-stu-id="967ec-112">Grpc.AspNetCore.Server</span></span>](https://www.nuget.org/packages/Grpc.AspNetCore.Server)
* <span data-ttu-id="967ec-113">[Google.Protobuf](https://www.nuget.org/packages/Google.Protobuf/) protobuf 메시지 Api.</span><span class="sxs-lookup"><span data-stu-id="967ec-113">[Google.Protobuf](https://www.nuget.org/packages/Google.Protobuf/) for protobuf message APIs.</span></span>
* [<span data-ttu-id="967ec-114">Grpc.Tools</span><span class="sxs-lookup"><span data-stu-id="967ec-114">Grpc.Tools</span></span>](https://www.nuget.org/packages/Grpc.Tools/)

### <a name="configure-grpc"></a><span data-ttu-id="967ec-115">GRPC를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="967ec-115">Configure gRPC</span></span>

<span data-ttu-id="967ec-116">gRPC 사용 하도록 설정 되었는지는 `AddGrpc` 메서드:</span><span class="sxs-lookup"><span data-stu-id="967ec-116">gRPC is enabled with the `AddGrpc` method:</span></span>

[!code-cs[](~/tutorials/grpc/grpc-start/samples/GrpcStart/GrpcGreeter.Server/Startup.cs?name=snippet&highlight=5)]

<span data-ttu-id="967ec-117">각 gRPC 서비스를 통해 라우팅 파이프라인에 추가 되는 `MapGrpcService` 메서드:</span><span class="sxs-lookup"><span data-stu-id="967ec-117">Each gRPC service is added to the routing pipeline through the `MapGrpcService` method:</span></span>

[!code-cs[](~/tutorials/grpc/grpc-start/samples/GrpcStart/GrpcGreeter.Server/Startup.cs?name=snippet&highlight=16-19)]

<span data-ttu-id="967ec-118">ASP.NET Core 미들웨어 및 기능 공유 라우팅 파이프라인, 따라서 추가 요청 처리기를 제공 하는 앱을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="967ec-118">ASP.NET Core middlewares and features share the routing pipeline, therefore an app can be configured to serve additional request handlers.</span></span> <span data-ttu-id="967ec-119">예: MVC 컨트롤러 추가 요청 처리기 구성된 gRPC 서비스를 사용 하 여 병렬로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="967ec-119">The additional request handlers, such as MVC controllers, work in parallel with the configured gRPC services.</span></span>

## <a name="integration-with-aspnet-core-apis"></a><span data-ttu-id="967ec-120">ASP.NET Core Api와 통합</span><span class="sxs-lookup"><span data-stu-id="967ec-120">Integration with ASP.NET Core APIs</span></span>

<span data-ttu-id="967ec-121">gRPC 서비스 전체 기능에 액세스할 수는 ASP.NET Core와 같은 [종속성 주입](xref:fundamentals/dependency-injection) (DI) 및 [로깅](xref:fundamentals/logging/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="967ec-121">gRPC services have full access to the ASP.NET Core features such as [Dependency Injection](xref:fundamentals/dependency-injection) (DI) and [Logging](xref:fundamentals/logging/index).</span></span> <span data-ttu-id="967ec-122">예를 들어, 서비스 구현에는 생성자를 통해 DI 컨테이너에서로 거 서비스를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="967ec-122">For example, the service implementation can resolve a logger service from the DI container via the constructor:</span></span>

```csharp
public class GreeterService : Greeter.GreeterBase
{
    public GreeterService(ILogger<GreeterService> logger)
    {
    }
}
```

<span data-ttu-id="967ec-123">기본적으로 gRPC 서비스 구현의 모든 수명 (단일, Scoped, 또는 일시적)를 사용 하 여 다른 di를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="967ec-123">By default, the gRPC service implementation can resolve other DI services with any lifetime (Singleton, Scoped, or Transient).</span></span>

### <a name="resolve-httpcontext-in-grpc-methods"></a><span data-ttu-id="967ec-124">GRPC 메서드에서 HttpContext 해결</span><span class="sxs-lookup"><span data-stu-id="967ec-124">Resolve HttpContext in gRPC methods</span></span>

<span data-ttu-id="967ec-125">GRPC API 메서드, 호스트, 헤더 및 트레일러와 같은 일부 HTTP/2 메시지 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="967ec-125">The gRPC API provides access to some HTTP/2 message data, such as the method, host, header, and trailers.</span></span> <span data-ttu-id="967ec-126">통해 액세스 된 `ServerCallContext` 각 gRPC 메서드에 전달 된 인수:</span><span class="sxs-lookup"><span data-stu-id="967ec-126">Access is through the `ServerCallContext` argument passed to each gRPC method:</span></span>

[!code-cs[](~/tutorials/grpc/grpc-start/samples/GrpcStart/GrpcGreeter.Server/Services/GreeterService.cs?highlight=3-4&name=snippet)]

<span data-ttu-id="967ec-127">`ServerCallContext` 에 대 한 전체 액세스를 제공 하지 않습니다 `HttpContext` 모든 ASP.NET api에서.</span><span class="sxs-lookup"><span data-stu-id="967ec-127">`ServerCallContext` does not provide full access to `HttpContext` in all ASP.NET APIs.</span></span> <span data-ttu-id="967ec-128">합니다 `GetHttpContext` 에 대 한 전체 액세스를 제공 하는 확장 메서드는 `HttpContext` ASP.NET Api에서 기본 HTTP/2 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="967ec-128">The `GetHttpContext` extension method provides full access to the `HttpContext` representing the underlying HTTP/2 message in ASP.NET APIs:</span></span>

[!code-cs[](~/tutorials/grpc/grpc-start/samples/GrpcStart/GrpcGreeter.Server/Services/GreeterService.cs?name=snippet1)]

### <a name="request-body-data-rate-limit"></a><span data-ttu-id="967ec-129">요청 본문 데이터 속도 제한</span><span class="sxs-lookup"><span data-stu-id="967ec-129">Request body data rate limit</span></span>

<span data-ttu-id="967ec-130">기본적으로 Kestrel 서버 적용을 [최소 요청 본문 데이터 속도](
<xref:Microsoft.AspNetCore.Server.Kestrel.Core.KestrelServerLimits.MinRequestBodyDataRate>)합니다.</span><span class="sxs-lookup"><span data-stu-id="967ec-130">By default, the Kestrel server imposes a [minimum request body data rate](
<xref:Microsoft.AspNetCore.Server.Kestrel.Core.KestrelServerLimits.MinRequestBodyDataRate>).</span></span> <span data-ttu-id="967ec-131">스트리밍 호출이 이중와 스트리밍 클라이언트에 대 한이 속도 충족할 수 있습니다 하 고 연결 시간이 초과 될 수 있습니다. 최소 요청 본문 데이터 속도 제한 gRPC 서비스 스트리밍 클라이언트 및 이중 교환 패턴 스트리밍 호출이 포함 된 경우 비활성화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="967ec-131">For client streaming and duplex streaming calls, this rate may not be satisfied and the connection may be timed out. The minimum request body data rate limit must be disabled when the gRPC service includes client streaming and duplex streaming calls:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateHostBuilder(args).Build().Run();
    }

    public static IHostBuilder CreateHostBuilder(string[] args) =>
         Host.CreateDefaultBuilder(args)
    .ConfigureWebHostDefaults(webBuilder =>
    {
        webBuilder.UseStartup<Startup>();
        webBuilder.ConfigureKestrel((context, options) =>
        {
            options.Limits.MinRequestBodyDataRate = null;
        });
    });
}
```

## <a name="additional-resources"></a><span data-ttu-id="967ec-132">추가 자료</span><span class="sxs-lookup"><span data-stu-id="967ec-132">Additional resources</span></span>

* <xref:tutorials/grpc/grpc-start>
* <xref:grpc/index>
* <xref:grpc/basics>
* <xref:grpc/migration>
