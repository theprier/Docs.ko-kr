---
title: ASP.NET Core SignalR의 지원 되는 플랫폼
author: tdykstra
description: ASP.NET Core SignalR에 대 한 지원 되는 플랫폼
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 09/26/2018
uid: signalr/supported-platforms
ms.openlocfilehash: d6d74a55d35ddb34a6f66a171bfe3f343dd61b63
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48577628"
---
# <a name="aspnet-core-signalr-supported-platforms"></a><span data-ttu-id="538b3-103">ASP.NET Core SignalR의 지원 되는 플랫폼</span><span class="sxs-lookup"><span data-stu-id="538b3-103">ASP.NET Core SignalR supported platforms</span></span>

## <a name="server-system-requirements"></a><span data-ttu-id="538b3-104">서버 시스템 요구 사항</span><span class="sxs-lookup"><span data-stu-id="538b3-104">Server system requirements</span></span>

<span data-ttu-id="538b3-105">ASP.NET core SignalR은 ASP.NET Core에서 지 원하는 모든 서버 플랫폼을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="538b3-105">SignalR for ASP.NET Core supports any server platform ASP.NET Core supports.</span></span>

## <a name="javascript-client"></a><span data-ttu-id="538b3-106">JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="538b3-106">JavaScript client</span></span>

<span data-ttu-id="538b3-107">합니다 [JavaScript 클라이언트](https://www.npmjs.com/package/@aspnet/signalr) NodeJS 8 및 이후 버전 및 다음 브라우저에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="538b3-107">The [JavaScript client](https://www.npmjs.com/package/@aspnet/signalr) runs on NodeJS 8 and later versions and the following browsers:</span></span>

| <span data-ttu-id="538b3-108">브라우저</span><span class="sxs-lookup"><span data-stu-id="538b3-108">Browser</span></span> | <span data-ttu-id="538b3-109">버전</span><span class="sxs-lookup"><span data-stu-id="538b3-109">Version</span></span> |
| ------- | ------- |
| <span data-ttu-id="538b3-110">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="538b3-110">Microsoft Edge</span></span> | <span data-ttu-id="538b3-111">현재</span><span class="sxs-lookup"><span data-stu-id="538b3-111">current</span></span> |
| <span data-ttu-id="538b3-112">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="538b3-112">Mozilla Firefox</span></span> | <span data-ttu-id="538b3-113">현재</span><span class="sxs-lookup"><span data-stu-id="538b3-113">current</span></span> |
| <span data-ttu-id="538b3-114">Google Chrome; Android를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="538b3-114">Google Chrome; includes Android</span></span> | <span data-ttu-id="538b3-115">현재</span><span class="sxs-lookup"><span data-stu-id="538b3-115">current</span></span> |
| <span data-ttu-id="538b3-116">Safari; iOS를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="538b3-116">Safari; includes iOS</span></span> | <span data-ttu-id="538b3-117">현재</span><span class="sxs-lookup"><span data-stu-id="538b3-117">current</span></span> |
| <span data-ttu-id="538b3-118">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="538b3-118">Microsoft Internet Explorer</span></span> | <span data-ttu-id="538b3-119">11</span><span class="sxs-lookup"><span data-stu-id="538b3-119">11</span></span> |
 
## <a name="net-client"></a><span data-ttu-id="538b3-120">.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="538b3-120">.NET client</span></span>

<span data-ttu-id="538b3-121">합니다 [.NET 클라이언트](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/) ASP.NET Core에서 지 원하는 서버 플랫폼에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="538b3-121">The [.NET client](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/) runs on any server platform supported by ASP.NET Core.</span></span>

<span data-ttu-id="538b3-122">서버에서 IIS를 실행 하는 경우 Websocket 전송이 이상 Windows Server 2012에서 IIS 8.0 이상이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="538b3-122">When the server runs IIS, the WebSockets transport requires IIS 8.0 or higher, on Windows Server 2012 or higher.</span></span> <span data-ttu-id="538b3-123">다른 전송 모든 플랫폼에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="538b3-123">Other transports are supported on all platforms.</span></span>

## <a name="java-client"></a><span data-ttu-id="538b3-124">Java 클라이언트</span><span class="sxs-lookup"><span data-stu-id="538b3-124">Java client</span></span>

<span data-ttu-id="538b3-125">합니다 [Java 클라이언트](https://search.maven.org/artifact/com.microsoft.aspnet/signalr) Java 8 및 이후 버전을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="538b3-125">The [Java client](https://search.maven.org/artifact/com.microsoft.aspnet/signalr) supports Java 8 and later versions.</span></span>

## <a name="unsupported-clients"></a><span data-ttu-id="538b3-126">지원 되지 않는 클라이언트</span><span class="sxs-lookup"><span data-stu-id="538b3-126">Unsupported clients</span></span>

<span data-ttu-id="538b3-127">다음 클라이언트는 사용할 수 있지만 실험적 또는 비공식 됩니다.</span><span class="sxs-lookup"><span data-stu-id="538b3-127">The following clients are available but are experimental or unofficial.</span></span> <span data-ttu-id="538b3-128">이제 지원 되지 않으며 적이 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="538b3-128">They are not supported now and may not ever be supported.</span></span>

* [<span data-ttu-id="538b3-129">C + + 클라이언트</span><span class="sxs-lookup"><span data-stu-id="538b3-129">C++ client</span></span>](https://github.com/aspnet/SignalR/tree/master/clients/cpp)

* [<span data-ttu-id="538b3-130">Swift 클라이언트</span><span class="sxs-lookup"><span data-stu-id="538b3-130">Swift client</span></span>](https://github.com/moozzyk/SignalR-Client-Swift)
