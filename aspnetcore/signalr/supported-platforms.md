---
title: ASP.NET Core SignalR 지원 플랫폼
author: tdykstra
description: ASP.NET Core SignalR에 대 한 지원 되는 플랫폼에 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 10/31/2018
uid: signalr/supported-platforms
ms.openlocfilehash: 773f6c020dbb2982911e177b55855473c750d52a
ms.sourcegitcommit: fc2486ddbeb15ab4969168d99b3fe0fbe91e8661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/01/2018
ms.locfileid: "50758182"
---
# <a name="aspnet-core-signalr-supported-platforms"></a><span data-ttu-id="96a50-103">ASP.NET Core SignalR 지원 플랫폼</span><span class="sxs-lookup"><span data-stu-id="96a50-103">ASP.NET Core SignalR supported platforms</span></span>

## <a name="server-system-requirements"></a><span data-ttu-id="96a50-104">서버 시스템 요구 사항</span><span class="sxs-lookup"><span data-stu-id="96a50-104">Server system requirements</span></span>

<span data-ttu-id="96a50-105">ASP.NET core SignalR은 ASP.NET Core에서 지 원하는 서버 플랫폼을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="96a50-105">SignalR for ASP.NET Core supports any server platform that ASP.NET Core supports.</span></span>

## <a name="javascript-client"></a><span data-ttu-id="96a50-106">JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="96a50-106">JavaScript client</span></span>

<span data-ttu-id="96a50-107">[JavaScript 클라이언트](https://www.npmjs.com/package/@aspnet/signalr)는 NodeJS 8 이상의 버전과 다음 브라우저에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="96a50-107">The [JavaScript client](https://www.npmjs.com/package/@aspnet/signalr) runs on NodeJS 8 and later versions and the following browsers:</span></span>

| <span data-ttu-id="96a50-108">브라우저</span><span class="sxs-lookup"><span data-stu-id="96a50-108">Browser</span></span>                         | <span data-ttu-id="96a50-109">버전</span><span class="sxs-lookup"><span data-stu-id="96a50-109">Version</span></span> |
| ------------------------------- | ------- |
| <span data-ttu-id="96a50-110">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="96a50-110">Microsoft Edge</span></span>                  | <span data-ttu-id="96a50-111">현재</span><span class="sxs-lookup"><span data-stu-id="96a50-111">current</span></span> |
| <span data-ttu-id="96a50-112">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="96a50-112">Mozilla Firefox</span></span>                 | <span data-ttu-id="96a50-113">현재</span><span class="sxs-lookup"><span data-stu-id="96a50-113">current</span></span> |
| <span data-ttu-id="96a50-114">Google Chrome(Android 포함)</span><span class="sxs-lookup"><span data-stu-id="96a50-114">Google Chrome; includes Android</span></span> | <span data-ttu-id="96a50-115">현재</span><span class="sxs-lookup"><span data-stu-id="96a50-115">current</span></span> |
| <span data-ttu-id="96a50-116">Safari(iOS 포함)</span><span class="sxs-lookup"><span data-stu-id="96a50-116">Safari; includes iOS</span></span>            | <span data-ttu-id="96a50-117">현재</span><span class="sxs-lookup"><span data-stu-id="96a50-117">current</span></span> |
| <span data-ttu-id="96a50-118">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="96a50-118">Microsoft Internet Explorer</span></span>     | <span data-ttu-id="96a50-119">11</span><span class="sxs-lookup"><span data-stu-id="96a50-119">11</span></span>      |
 
## <a name="net-client"></a><span data-ttu-id="96a50-120">.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="96a50-120">.NET client</span></span>

<span data-ttu-id="96a50-121">[.NET 클라이언트](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/)는 ASP.NET Core가 지원하는 모든 서버 플랫폼에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="96a50-121">The [.NET client](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/) runs on any server platform supported by ASP.NET Core.</span></span>

<span data-ttu-id="96a50-122">서버에서 IIS를 실행 하는 경우 Websocket 전송이 IIS 8.0 또는 Windows Server 2012에서 더 이상 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="96a50-122">If the server runs IIS, the WebSockets transport requires IIS 8.0 or higher on Windows Server 2012 or higher.</span></span> <span data-ttu-id="96a50-123">다른 전송 방식들은 모든 플랫폼에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="96a50-123">Other transports are supported on all platforms.</span></span>

## <a name="java-client"></a><span data-ttu-id="96a50-124">Java 클라이언트</span><span class="sxs-lookup"><span data-stu-id="96a50-124">Java client</span></span>

<span data-ttu-id="96a50-125">[Java 클라이언트](https://search.maven.org/artifact/com.microsoft.aspnet/signalr)는 Java 8 이상의 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="96a50-125">The [Java client](https://search.maven.org/artifact/com.microsoft.aspnet/signalr) supports Java 8 and later versions.</span></span>

## <a name="unsupported-clients"></a><span data-ttu-id="96a50-126">지원되지 않는 클라이언트</span><span class="sxs-lookup"><span data-stu-id="96a50-126">Unsupported clients</span></span>

<span data-ttu-id="96a50-127">다음 클라이언트는 사용할 수는 있지만 실험적이거나 비공식적입니다.</span><span class="sxs-lookup"><span data-stu-id="96a50-127">The following clients are available but are experimental or unofficial.</span></span> <span data-ttu-id="96a50-128">현재 지원 되지 않으며 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96a50-128">They aren't currently supported and may never be.</span></span>

* [<span data-ttu-id="96a50-129">C++ 클라이언트</span><span class="sxs-lookup"><span data-stu-id="96a50-129">C++ client</span></span>](https://github.com/aspnet/SignalR/tree/master/clients/cpp)

* [<span data-ttu-id="96a50-130">Swift 클라이언트</span><span class="sxs-lookup"><span data-stu-id="96a50-130">Swift client</span></span>](https://github.com/moozzyk/SignalR-Client-Swift)
