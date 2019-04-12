---
title: Razor 구성 요소 호스팅 모델
author: guardrex
description: 클라이언트 쪽 Blazor 및 서버 쪽 ASP.NET Core Razor 구성 요소 호스팅 모델을 이해 합니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 03/28/2019
uid: razor-components/hosting-models
ms.openlocfilehash: 8ed70117c94bf1a3e4c208f70310bbf0473bae44
ms.sourcegitcommit: 6bde1fdf686326c080a7518a6725e56e56d8886e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59515647"
---
# <a name="razor-components-hosting-models"></a><span data-ttu-id="b6a63-103">Razor 구성 요소 호스팅 모델</span><span class="sxs-lookup"><span data-stu-id="b6a63-103">Razor Components hosting models</span></span>

<span data-ttu-id="b6a63-104">[Daniel Roth](https://github.com/danroth27)</span><span class="sxs-lookup"><span data-stu-id="b6a63-104">By [Daniel Roth](https://github.com/danroth27)</span></span>

<span data-ttu-id="b6a63-105">Razor 구성 요소는 클라이언트 쪽에서 실행 하도록 설계 하는 웹 프레임 워크의 브라우저에는 [WebAssembly](http://webassembly.org/)-.NET 런타임 기반 (*Blazor*) 또는 ASP.NET Core에서 서버 쪽 (*ASP.NET Core Razor 구성 요소*).</span><span class="sxs-lookup"><span data-stu-id="b6a63-105">Razor Components is a web framework designed to run client-side in the browser on a [WebAssembly](http://webassembly.org/)-based .NET runtime (*Blazor*) or server-side in ASP.NET Core (*ASP.NET Core Razor Components*).</span></span> <span data-ttu-id="b6a63-106">호스팅 모델, 앱 및 구성 요소 모델에 관계 없이 *동일 하 게 유지*합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-106">Regardless of the hosting model, the app and component models *remain the same*.</span></span> <span data-ttu-id="b6a63-107">이 문서에서는 사용 가능한 호스팅 모델을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-107">This article discusses the available hosting models:</span></span>

* [<span data-ttu-id="b6a63-108">클라이언트 쪽 Blazor</span><span class="sxs-lookup"><span data-stu-id="b6a63-108">Client-side Blazor</span></span>](#client-side-hosting-model)
* [<span data-ttu-id="b6a63-109">서버 쪽 ASP.NET Core Razor 구성 요소</span><span class="sxs-lookup"><span data-stu-id="b6a63-109">Server-side ASP.NET Core Razor Components</span></span>](#server-side-hosting-model)

## <a name="client-side-hosting-model"></a><span data-ttu-id="b6a63-110">클라이언트 쪽 호스팅 모델</span><span class="sxs-lookup"><span data-stu-id="b6a63-110">Client-side hosting model</span></span>

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

<span data-ttu-id="b6a63-111">Blazor의 주 호스팅 모델은 WebAssembly 브라우저에서 실행 중인 클라이언트 쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-111">The principal hosting model for Blazor is running client-side in the browser on WebAssembly.</span></span> <span data-ttu-id="b6a63-112">Blazor 앱, 해당 앱의 종속성 및 .NET 런타임이 브라우저에 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-112">The Blazor app, its dependencies, and the .NET runtime are downloaded to the browser.</span></span> <span data-ttu-id="b6a63-113">해당 앱은 브라우저 UI 스레드에서 직접 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-113">The app is executed directly on the browser UI thread.</span></span> <span data-ttu-id="b6a63-114">이벤트 처리의 UI 업데이트와 동일한 프로세스 내에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-114">UI updates and event handling occur within the same process.</span></span> <span data-ttu-id="b6a63-115">앱의 자산을 처리할 수 있는 정적 콘텐츠를 클라이언트에 서비스 웹 서버에 정적 파일로 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-115">The app's assets are deployed as static files to a web server or service capable of serving static content to clients.</span></span>

![Blazor 클라이언트 측: Blazor 앱 브라우저 내에서 UI 스레드에서 실행 됩니다.](hosting-models/_static/client-side.png)

<span data-ttu-id="b6a63-117">클라이언트 쪽 호스팅 모델을 사용 하는 Blazor 앱을 만들려면 다음 템플릿 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-117">To create a Blazor app using the client-side hosting model, use either of the following templates:</span></span>

* <span data-ttu-id="b6a63-118">**Blazor** ([dotnet 새 blazor](/dotnet/core/tools/dotnet-new)) &ndash; 정적 파일의 집합으로 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-118">**Blazor** ([dotnet new blazor](/dotnet/core/tools/dotnet-new)) &ndash; Deployed as a set of static files.</span></span>
* <span data-ttu-id="b6a63-119">**(ASP.NET Core 호스팅) Blazor** ([dotnet 새 blazorhosted](/dotnet/core/tools/dotnet-new)) &ndash; ASP.NET Core 서버에서 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-119">**Blazor (ASP.NET Core Hosted)** ([dotnet new blazorhosted](/dotnet/core/tools/dotnet-new)) &ndash; Hosted by an ASP.NET Core server.</span></span> <span data-ttu-id="b6a63-120">ASP.NET Core 앱 Blazor 앱 클라이언트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-120">The ASP.NET Core app serves the Blazor app to clients.</span></span> <span data-ttu-id="b6a63-121">웹 API 호출을 사용 하 여 네트워크를 통해 클라이언트 쪽 Blazor 앱 서버와 상호 작용할 수 또는 [SignalR](xref:signalr/introduction)합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-121">The client-side Blazor app can interact with the server over the network using web API calls or [SignalR](xref:signalr/introduction).</span></span>

<span data-ttu-id="b6a63-122">템플릿을 포함 합니다 *components.webassembly.js* 처리 하는 스크립트:</span><span class="sxs-lookup"><span data-stu-id="b6a63-122">The templates include the *components.webassembly.js* script that handles:</span></span>

* <span data-ttu-id="b6a63-123">.NET 런타임, 앱 및 앱의 종속성을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-123">Downloading the .NET runtime, the app, and the app's dependencies.</span></span>
* <span data-ttu-id="b6a63-124">앱을 실행 하려면 런타임 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-124">Initialization of the runtime to run the app.</span></span>

<span data-ttu-id="b6a63-125">클라이언트 쪽 호스팅 모델에는 몇 가지 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-125">The client-side hosting model offers several benefits.</span></span> <span data-ttu-id="b6a63-126">클라이언트 쪽 Blazor:</span><span class="sxs-lookup"><span data-stu-id="b6a63-126">Client-side Blazor:</span></span>

* <span data-ttu-id="b6a63-127">.NET 서버 쪽 종속성을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-127">Has no .NET server-side dependency.</span></span>
* <span data-ttu-id="b6a63-128">클라이언트 리소스 및 기능을 최대한 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-128">Fully leverages client resources and capabilities.</span></span>
* <span data-ttu-id="b6a63-129">오프 로드 서버에서 클라이언트로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-129">Offloads work from the server to the client.</span></span>
* <span data-ttu-id="b6a63-130">오프 라인 시나리오를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-130">Supports offline scenarios.</span></span>

<span data-ttu-id="b6a63-131">클라이언트 쪽 호스팅에 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-131">There are downsides to client-side hosting.</span></span> <span data-ttu-id="b6a63-132">클라이언트 쪽 Blazor:</span><span class="sxs-lookup"><span data-stu-id="b6a63-132">Client-side Blazor:</span></span>

* <span data-ttu-id="b6a63-133">브라우저의 기능으로 앱을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-133">Restricts the app to the capabilities of the browser.</span></span>
* <span data-ttu-id="b6a63-134">지원 되는 클라이언트 하드웨어 및 소프트웨어 (예를 들어, WebAssembly 지원)에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-134">Requires capable client hardware and software (for example, WebAssembly support).</span></span>
* <span data-ttu-id="b6a63-135">로드 시간 더 오래 앱을 더 큰 다운로드 크기에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-135">Has a larger download size and longer app load time.</span></span>
* <span data-ttu-id="b6a63-136">.NET 런타임 및 도구 지원 성숙 적습니다 (예를 들어, 제한 사항 [.NET Standard](/dotnet/standard/net-standard) 지원 및 디버깅) 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-136">Has less mature .NET runtime and tooling support (for example, limitations in [.NET Standard](/dotnet/standard/net-standard) support and debugging).</span></span>

## <a name="server-side-hosting-model"></a><span data-ttu-id="b6a63-137">서버 쪽 호스팅 모델</span><span class="sxs-lookup"><span data-stu-id="b6a63-137">Server-side hosting model</span></span>

<span data-ttu-id="b6a63-138">ASP.NET Core Razor 구성 요소 서버 쪽 호스팅 모델을 사용 하 여 응용 프로그램 서버에서 ASP.NET Core 앱 내에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-138">With the ASP.NET Core Razor Components server-side hosting model, the app is executed on the server from within an ASP.NET Core app.</span></span> <span data-ttu-id="b6a63-139">UI 업데이트, 이벤트 처리 및 JavaScript 호출을 통해 처리 되는 [SignalR](xref:signalr/introduction) 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-139">UI updates, event handling, and JavaScript calls are handled over a [SignalR](xref:signalr/introduction) connection.</span></span>

![ASP.NET Core Razor 구성 요소 서버 측: 브라우저와 상호 작용 (ASP.NET Core 앱 내에서 호스팅) 앱 서버에서 SignalR 연결을 통해.](hosting-models/_static/server-side.png)

<span data-ttu-id="b6a63-141">ASP.NET Core를 사용 하 여 서버 쪽 호스팅 모델을 사용 하는 구성 요소 Razor 앱을 만들려면 **구성 요소 Razor** 템플릿 ([dotnet 새 razorcomponents](/dotnet/core/tools/dotnet-new)).</span><span class="sxs-lookup"><span data-stu-id="b6a63-141">To create a Razor Components app using the server-side hosting model, use the ASP.NET Core **Razor Components** template ([dotnet new razorcomponents](/dotnet/core/tools/dotnet-new)).</span></span> <span data-ttu-id="b6a63-142">ASP.NET Core 앱 Razor 구성 요소 서버 쪽 앱을 호스트 하 고 클라이언트가 연결 된 SignalR 끝점을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-142">The ASP.NET Core app hosts the Razor Components server-side app and sets up the SignalR endpoint where clients connect.</span></span> <span data-ttu-id="b6a63-143">앱의를 참조 하는 ASP.NET Core 앱 `Startup` 추가할 클래스:</span><span class="sxs-lookup"><span data-stu-id="b6a63-143">The ASP.NET Core app references the app's `Startup` class to add:</span></span>

* <span data-ttu-id="b6a63-144">서버 쪽 구성 요소 Razor 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-144">Server-side Razor Components services.</span></span>
* <span data-ttu-id="b6a63-145">요청 처리 파이프라인에 대 한 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-145">The app to the request handling pipeline.</span></span>

[!code-csharp[](hosting-models/samples_snapshot/Startup.cs?highlight=5,27)]

<span data-ttu-id="b6a63-146">합니다 *components.server.js* 스크립트&dagger; 클라이언트 연결을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-146">The *components.server.js* script&dagger; establishes the client connection.</span></span> <span data-ttu-id="b6a63-147">것은 앱의 책임 (예를 들어 네트워크 연결이) 발생할 경우 필요에 따라 앱 상태를 유지 및 복원입니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-147">It's the app's responsibility to persist and restore app state as required (for example, in the event of a lost network connection).</span></span>

<span data-ttu-id="b6a63-148">서버 쪽 호스팅 모델에는 몇 가지 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-148">The server-side hosting model offers several benefits.</span></span> <span data-ttu-id="b6a63-149">서버 쪽 Razor 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="b6a63-149">Server-side Razor Components:</span></span>

* <span data-ttu-id="b6a63-150">클라이언트 쪽 Blazor 앱을 보다 훨씬 작은 앱 크기가 있고 훨씬 빠르게 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-150">Have a significantly smaller app size than a client-side Blazor app and load much faster.</span></span>
* <span data-ttu-id="b6a63-151">모든.NET Core 호환 되는 Api를 사용 하는 등 서버 기능의 활용을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-151">Can take full advantage of server capabilities, including using any .NET Core compatible APIs.</span></span>
* <span data-ttu-id="b6a63-152">도구, 디버깅와 같은 기존.NET 예상 대로 작동 하므로.NET Core에 서버에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-152">Run on .NET Core on the server, so existing .NET tooling, such as debugging, works as expected.</span></span>
* <span data-ttu-id="b6a63-153">씬 클라이언트와 함께 (예: 브라우저 WebAssembly 및 리소스를 지원 하지 않는 제한 된 장치).</span><span class="sxs-lookup"><span data-stu-id="b6a63-153">Works with thin clients (for example, browsers that don't support WebAssembly and resource constrained devices).</span></span>
* <span data-ttu-id="b6a63-154">.NET /C# 앱의 구성 요소 코드를 포함 하 여 코드 베이스를 클라이언트에 제공 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-154">.NET/C# code base, including the app's component code, isn't served to clients.</span></span>

<span data-ttu-id="b6a63-155">서버 쪽 호스팅에 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-155">There are downsides to server-side hosting.</span></span> <span data-ttu-id="b6a63-156">서버 쪽 Razor 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="b6a63-156">Server-side Razor Components:</span></span>

* <span data-ttu-id="b6a63-157">대기를 시간이 길어집니다. 모든 사용자 상호 작용을 네트워크 홉이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-157">Have higher latency: Every user interaction involves a network hop.</span></span>
* <span data-ttu-id="b6a63-158">없는 오프 라인 지원을 제공 합니다. 클라이언트 연결에 실패 하면 앱 작동이 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-158">Offer no offline support: If the client connection fails, the app stops working.</span></span>
* <span data-ttu-id="b6a63-159">확장성이 저하. 서버는 여러 클라이언트 연결을 관리 하 고 클라이언트 상태를 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-159">Have reduced scalability: The server must manage multiple client connections and handle client state.</span></span>
* <span data-ttu-id="b6a63-160">앱을 제공 하는 ASP.NET Core 서버가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-160">Require an ASP.NET Core server to serve the app.</span></span> <span data-ttu-id="b6a63-161">(예: CDN)에서 서버 없이 배포 할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-161">Deployment without a server (for example, from a CDN) isn't possible.</span></span>

<span data-ttu-id="b6a63-162">&dagger;합니다 *components.server.js* 스크립트는 다음 경로에 게시 됩니다. *bin / {디버그 | 릴리스} / {대상 프레임 워크} /publish/ {응용 프로그램 이름}. 앱/배포/_framework*합니다.</span><span class="sxs-lookup"><span data-stu-id="b6a63-162">&dagger;The *components.server.js* script is published to the following path: *bin/{Debug|Release}/{TARGET FRAMEWORK}/publish/{APPLICATION NAME}.App/dist/_framework*.</span></span>
