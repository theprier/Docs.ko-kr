---
title: ASP.NET Core SignalR 지원 플랫폼
author: bradygaster
description: ASP.NET Core SignalR에 대 한 지원 되는 플랫폼에 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: bradyg
ms.custom: mvc
ms.date: 11/12/2018
uid: signalr/supported-platforms
ms.openlocfilehash: e4e84baf0120036b473eac256107b46a4accfe37
ms.sourcegitcommit: ebf4e5a7ca301af8494edf64f85d4a8deb61d641
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54837717"
---
# <a name="aspnet-core-signalr-supported-platforms"></a><span data-ttu-id="fd8dc-103">ASP.NET Core SignalR 지원 플랫폼</span><span class="sxs-lookup"><span data-stu-id="fd8dc-103">ASP.NET Core SignalR supported platforms</span></span>

## <a name="server-system-requirements"></a><span data-ttu-id="fd8dc-104">서버 시스템 요구 사항</span><span class="sxs-lookup"><span data-stu-id="fd8dc-104">Server system requirements</span></span>

<span data-ttu-id="fd8dc-105">ASP.NET core SignalR은 ASP.NET Core에서 지 원하는 서버 플랫폼을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dc-105">SignalR for ASP.NET Core supports any server platform that ASP.NET Core supports.</span></span>

## <a name="javascript-client"></a><span data-ttu-id="fd8dc-106">JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="fd8dc-106">JavaScript client</span></span>

<span data-ttu-id="fd8dc-107">[JavaScript 클라이언트](https://www.npmjs.com/package/@aspnet/signalr)는 NodeJS 8 이상의 버전과 다음 브라우저에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dc-107">The [JavaScript client](https://www.npmjs.com/package/@aspnet/signalr) runs on NodeJS 8 and later versions and the following browsers:</span></span>

| <span data-ttu-id="fd8dc-108">브라우저</span><span class="sxs-lookup"><span data-stu-id="fd8dc-108">Browser</span></span>                         | <span data-ttu-id="fd8dc-109">버전</span><span class="sxs-lookup"><span data-stu-id="fd8dc-109">Version</span></span> |
| ------------------------------- | ------- |
| <span data-ttu-id="fd8dc-110">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="fd8dc-110">Microsoft Edge</span></span>                  | <span data-ttu-id="fd8dc-111">현재</span><span class="sxs-lookup"><span data-stu-id="fd8dc-111">current</span></span> |
| <span data-ttu-id="fd8dc-112">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="fd8dc-112">Mozilla Firefox</span></span>                 | <span data-ttu-id="fd8dc-113">현재</span><span class="sxs-lookup"><span data-stu-id="fd8dc-113">current</span></span> |
| <span data-ttu-id="fd8dc-114">Google Chrome(Android 포함)</span><span class="sxs-lookup"><span data-stu-id="fd8dc-114">Google Chrome; includes Android</span></span> | <span data-ttu-id="fd8dc-115">현재</span><span class="sxs-lookup"><span data-stu-id="fd8dc-115">current</span></span> |
| <span data-ttu-id="fd8dc-116">Safari(iOS 포함)</span><span class="sxs-lookup"><span data-stu-id="fd8dc-116">Safari; includes iOS</span></span>            | <span data-ttu-id="fd8dc-117">현재</span><span class="sxs-lookup"><span data-stu-id="fd8dc-117">current</span></span> |
| <span data-ttu-id="fd8dc-118">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="fd8dc-118">Microsoft Internet Explorer</span></span>     | <span data-ttu-id="fd8dc-119">11</span><span class="sxs-lookup"><span data-stu-id="fd8dc-119">11</span></span>      |
 
## <a name="net-client"></a><span data-ttu-id="fd8dc-120">.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="fd8dc-120">.NET client</span></span>

<span data-ttu-id="fd8dc-121">합니다 [.NET 클라이언트](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/) ASP.NET Core에서 지 원하는 모든 플랫폼에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dc-121">The [.NET client](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/) runs on any platform supported by ASP.NET Core.</span></span> <span data-ttu-id="fd8dc-122">예를 들어 [Xamarin 개발자 SignalR을 사용 하 여](https://github.com/aspnet/Announcements/issues/305) 8.4.0.1 Xamarin.Android를 사용 하 여 Android 앱을 빌드하기 위한 나중 및 11.14.0.4 Xamarin.iOS를 사용 하 여 iOS 앱 이상.</span><span class="sxs-lookup"><span data-stu-id="fd8dc-122">For example, [Xamarin developers can use SignalR](https://github.com/aspnet/Announcements/issues/305) for building Android apps using Xamarin.Android 8.4.0.1 and later and iOS apps using Xamarin.iOS 11.14.0.4 and later.</span></span>

<span data-ttu-id="fd8dc-123">서버에서 IIS를 실행 하는 경우 Websocket 전송이 IIS 8.0 또는 Windows Server 2012에서 더 이상 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dc-123">If the server runs IIS, the WebSockets transport requires IIS 8.0 or higher on Windows Server 2012 or higher.</span></span> <span data-ttu-id="fd8dc-124">다른 전송 방식들은 모든 플랫폼에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dc-124">Other transports are supported on all platforms.</span></span>

## <a name="java-client"></a><span data-ttu-id="fd8dc-125">Java 클라이언트</span><span class="sxs-lookup"><span data-stu-id="fd8dc-125">Java client</span></span>

<span data-ttu-id="fd8dc-126">[Java 클라이언트](https://search.maven.org/artifact/com.microsoft.aspnet/signalr)는 Java 8 이상의 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dc-126">The [Java client](https://search.maven.org/artifact/com.microsoft.aspnet/signalr) supports Java 8 and later versions.</span></span>

## <a name="unsupported-clients"></a><span data-ttu-id="fd8dc-127">지원되지 않는 클라이언트</span><span class="sxs-lookup"><span data-stu-id="fd8dc-127">Unsupported clients</span></span>

<span data-ttu-id="fd8dc-128">다음 클라이언트는 사용할 수는 있지만 실험적이거나 비공식적입니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dc-128">The following clients are available but are experimental or unofficial.</span></span> <span data-ttu-id="fd8dc-129">현재 지원 되지 않으며 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd8dc-129">They aren't currently supported and may never be.</span></span>

* [<span data-ttu-id="fd8dc-130">C++ 클라이언트</span><span class="sxs-lookup"><span data-stu-id="fd8dc-130">C++ client</span></span>](https://github.com/aspnet/SignalR/tree/master/clients/cpp)

* [<span data-ttu-id="fd8dc-131">Swift 클라이언트</span><span class="sxs-lookup"><span data-stu-id="fd8dc-131">Swift client</span></span>](https://github.com/moozzyk/SignalR-Client-Swift)
