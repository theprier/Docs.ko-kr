---
uid: signalr/overview/getting-started/supported-platforms
title: "지원 되는 플랫폼 | Microsoft Docs"
author: pfletcher
description: "이 문서에서는 어떤 클라이언트 및 서버는 SignalR에서 지원 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: eac31beb-0f46-4afa-9def-e80904dea4f0
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/getting-started/supported-platforms
msc.type: authoredcontent
ms.openlocfilehash: 1379b9fb638f67896d88d7aa4312d95280ef7318
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
<a name="supported-platforms"></a><span data-ttu-id="eaa87-103">지원되는 플랫폼</span><span class="sxs-lookup"><span data-stu-id="eaa87-103">Supported Platforms</span></span>
====================
<span data-ttu-id="eaa87-104">으로 [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="eaa87-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

> <span data-ttu-id="eaa87-105">이 문서에서는 어떤 클라이언트 및 서버는 SignalR에서 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-105">This article describes what clients and servers are supported by SignalR.</span></span> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="eaa87-106">질문이 나 의견이</span><span class="sxs-lookup"><span data-stu-id="eaa87-106">Questions and comments</span></span>
> 
> <span data-ttu-id="eaa87-107">이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="eaa87-107">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="eaa87-108">자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-108">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<span data-ttu-id="eaa87-109">SignalR은 다양 한 서버 및 클라이언트 구성에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-109">SignalR is supported under a variety of server and client configurations.</span></span> <span data-ttu-id="eaa87-110">또한 각 전송 옵션에는 자체;의 요구 사항 전송에 대 한 시스템 요구 사항에 사용할 수 없을 경우 SignalR 정상적으로 장애 조치를 다른 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-110">In addition, each transport option has a set of requirements of its own; if the system requirements for a transport are not available, SignalR will gracefully failover to other transports.</span></span> <span data-ttu-id="eaa87-111">SignalR을 지 원하는 전송에 대 한 자세한 내용은 참조 하십시오. [전송 및 대체](introduction-to-signalr.md#transports)합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-111">For more information on the transports that SignalR supports, see [Transports and Fallbacks](introduction-to-signalr.md#transports).</span></span>

## <a name="server-system-requirements"></a><span data-ttu-id="eaa87-112">서버 시스템 요구 사항</span><span class="sxs-lookup"><span data-stu-id="eaa87-112">Server system requirements</span></span>

<span data-ttu-id="eaa87-113">SignalR 서버 구성 요소는 다양 한 서버 구성에서 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-113">The SignalR server component can be hosted on a variety of server configurations.</span></span> <span data-ttu-id="eaa87-114">이 섹션에서는 지원 되는 버전의 운영 체제,.NET framework, 인터넷 정보 서버 및 기타 구성 요소에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-114">This section describes the supported versions of operating systems, .NET framework, Internet Information Server, and other components.</span></span>

### <a name="supported-server-operating-systems"></a><span data-ttu-id="eaa87-115">지원되는 서버 운영 체제</span><span class="sxs-lookup"><span data-stu-id="eaa87-115">Supported server operating systems</span></span>

<span data-ttu-id="eaa87-116">SignalR 서버 구성 요소는 다음과 같은 서버 또는 클라이언트 운영 체제에서 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-116">The SignalR server component can be hosted in the following server or client operating systems.</span></span> <span data-ttu-id="eaa87-117">Websocket을 사용 하는 SignalR에 대 한 Windows Server 2012 또는 Windows 8이 필요 (WebSocket 사용 가능 Windows Azure 웹 사이트에 사이트의.NET framework 버전 4.5로 설정 되어 있고 사이트의 구성 페이지에서 Websocket 사용 됨).</span><span class="sxs-lookup"><span data-stu-id="eaa87-117">Note that for SignalR to use WebSockets, Windows Server 2012 or Windows 8 is required (WebSocket can be used on Windows Azure Web Sites, as long as the site's .NET framework version is set to 4.5, and Web Sockets is enabled in the site's Configuration page).</span></span>

- <span data-ttu-id="eaa87-118">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="eaa87-118">Windows Server 2012</span></span>
- <span data-ttu-id="eaa87-119">Windows Server 2008 r2</span><span class="sxs-lookup"><span data-stu-id="eaa87-119">Windows Server 2008 r2</span></span>
- <span data-ttu-id="eaa87-120">Windows 10</span><span class="sxs-lookup"><span data-stu-id="eaa87-120">Windows 10</span></span>
- <span data-ttu-id="eaa87-121">Windows 8</span><span class="sxs-lookup"><span data-stu-id="eaa87-121">Windows 8</span></span>
- <span data-ttu-id="eaa87-122">Windows 7</span><span class="sxs-lookup"><span data-stu-id="eaa87-122">Windows 7</span></span>
- <span data-ttu-id="eaa87-123">Windows Azure</span><span class="sxs-lookup"><span data-stu-id="eaa87-123">Windows Azure</span></span>

### <a name="supported-server-net-framework-version"></a><span data-ttu-id="eaa87-124">지원 되는 서버.NET Framework 버전</span><span class="sxs-lookup"><span data-stu-id="eaa87-124">Supported server .NET Framework version</span></span>

<span data-ttu-id="eaa87-125">.NET Framework 4.5에서 SignalR 2만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-125">SignalR 2 is only supported on .NET Framework 4.5.</span></span> <span data-ttu-id="eaa87-126">참조는 [권장 업데이트](#updates) 안정성, 호환성, 안정성 및 성능을 개선 하는 업데이트에 대 한 섹션.</span><span class="sxs-lookup"><span data-stu-id="eaa87-126">See the [Recommended Updates](#updates) section for updates that enhance reliability, compatibility, stability, and performance.</span></span>

### <a name="supported-server-iis-versions"></a><span data-ttu-id="eaa87-127">지원 되는 서버 IIS 버전</span><span class="sxs-lookup"><span data-stu-id="eaa87-127">Supported server IIS versions</span></span>

<span data-ttu-id="eaa87-128">SignalR을 IIS에서 호스트 하는 경우에 다음 버전은 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-128">When SignalR is hosted in IIS, the following versions are supported.</span></span> <span data-ttu-id="eaa87-129">클라이언트 운영 체제를 사용 하는 경우와 같은 개발을 위한 전체 버전의 IIS 또는 Cassini (Windows 8 또는 Windows 7) 쓰일 수 없습니다, 연결 이후 매우 신속 하 게 연결할 수 있는 10 개의 동시 연결, 적용 된 제한이 있으므로 note 자주 다시 설정, 임시 및가 정리 되지 않은 즉시 시 더 이상 사용 되지 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-129">Note that if a client operating system is used, such as for development (Windows 8 or Windows 7), full versions of IIS or Cassini should not be used, since there will be a limit of 10 simultaneous connections imposed, which will be reached very quickly since connections are transient, frequently re-established, and are not disposed immediately upon no longer being used.</span></span> <span data-ttu-id="eaa87-130">클라이언트 운영 체제에서 IIS Express를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-130">IIS Express should be used on client operating systems.</span></span>

<span data-ttu-id="eaa87-131">WebSocket을 사용 하는 SignalR에 대 한 IIS 8 또는 IIS 8 Express를 사용 합니다, 서버에 Windows 8, Windows Server 2012 이상 사용 해야 합니다를 IIS에서 WebSocket을 사용할 수 있어야 note도 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-131">Also note that for SignalR to use WebSocket, IIS 8 or IIS 8 Express must be used, the server must be using Windows 8, Windows Server 2012, or later, and WebSocket must be enabled in IIS.</span></span> <span data-ttu-id="eaa87-132">IIS에서 WebSocket을 사용 하도록 설정 하는 방법에 대 한 정보를 참조 하십시오. [IIS 8.0 WebSocket 프로토콜을 지 원하는](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support)합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-132">For information on how to enable WebSocket in IIS, see [IIS 8.0 WebSocket Protocol Support](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support).</span></span>

- <span data-ttu-id="eaa87-133">IIS 8 또는 IIS 8 Express입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-133">IIS 8 or IIS 8 Express.</span></span>
- <span data-ttu-id="eaa87-134">IIS 7 및 7.5입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-134">IIS 7 and 7.5.</span></span> <span data-ttu-id="eaa87-135">에 대 한 지원 [확장명 없는 Url](https://support.microsoft.com/kb/980368) 가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-135">Support for [extensionless URLs](https://support.microsoft.com/kb/980368) is required.</span></span>
- <span data-ttu-id="eaa87-136">통합된 모드에서 IIS를 실행 해야 합니다. 클래식 모드가 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-136">IIS must be running in integrated mode; classic mode is not supported.</span></span> <span data-ttu-id="eaa87-137">최대 30 초의 메시지 지연 Server-Sent 이벤트 전송을 사용 하 여 클래식 모드에서 IIS를 실행 하는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-137">Message delays of up to 30 seconds may be experienced if IIS is run in classic mode using the Server-Sent Events transport.</span></span>
- <span data-ttu-id="eaa87-138">호스팅 응용 프로그램은 완전 신뢰 모드에서 실행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-138">The hosting application must be running in full trust mode.</span></span>

## <a name="client-system-requirements"></a><span data-ttu-id="eaa87-139">클라이언트 시스템 요구 사항</span><span class="sxs-lookup"><span data-stu-id="eaa87-139">Client system requirements</span></span>

<span data-ttu-id="eaa87-140">SignalR은 다양 한 클라이언트 플랫폼에에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-140">SignalR can be used in a variety of client platforms.</span></span> <span data-ttu-id="eaa87-141">이 섹션에서는 웹 브라우저, Windows 데스크톱 응용 프로그램, Silverlight 응용 프로그램 및 모바일 장치에서 SignalR을 사용 하기 위한 시스템 요구 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-141">This section describes the system requirements for using SignalR in web browsers, Windows desktop applications, Silverlight applications, and mobile devices.</span></span>

### <a name="web-browsers"></a><span data-ttu-id="eaa87-142">웹 브라우저</span><span class="sxs-lookup"><span data-stu-id="eaa87-142">Web browsers</span></span>

<span data-ttu-id="eaa87-143">SignalR을 다양 한 웹 브라우저에서에서 사용할 수 있지만 일반적으로 두 가지 최신 버전 에서만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-143">SignalR can be used in a variety of web browsers, but typically, only the latest two versions are supported.</span></span>

<span data-ttu-id="eaa87-144">브라우저에서 SignalR을 사용 하는 응용 프로그램 (예: 1.7.2, 1.8.2, 또는 1.9.1) 이후 주 버전 또는 jQuery 버전 1.6.4 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-144">Applications that use SignalR in browsers must use jQuery version 1.6.4 or major later versions (such as 1.7.2, 1.8.2, or 1.9.1).</span></span>

<span data-ttu-id="eaa87-145">SignalR은 브라우저에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-145">SignalR can be used in the following browsers:</span></span>

- <span data-ttu-id="eaa87-146">Microsoft Internet Explorer 버전 8, 9, 10 및 11</span><span class="sxs-lookup"><span data-stu-id="eaa87-146">Microsoft Internet Explorer versions 8, 9, 10, and 11.</span></span> <span data-ttu-id="eaa87-147">최신, 데스크톱 및 모바일 버전이 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-147">Modern, Desktop, and Mobile versions are supported.</span></span>
- <span data-ttu-id="eaa87-148">Mozilla Firefox: 현재 버전-1, Windows와 Mac 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-148">Mozilla Firefox: current version - 1, both Windows and Mac versions.</span></span>
- <span data-ttu-id="eaa87-149">Google Chrome: 현재 버전-1, Windows와 Mac 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-149">Google Chrome: current version - 1, both Windows and Mac versions.</span></span>
- <span data-ttu-id="eaa87-150">Safari: 현재 버전-1, Mac 및 iOS 버전 모두 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-150">Safari: current version - 1, both Mac and iOS versions.</span></span>
- <span data-ttu-id="eaa87-151">Opera: 현재 버전-1, Windows에만 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-151">Opera: current version - 1, Windows only.</span></span>
- <span data-ttu-id="eaa87-152">Android 브라우저</span><span class="sxs-lookup"><span data-stu-id="eaa87-152">Android browser</span></span>

<span data-ttu-id="eaa87-153">특정 브라우저 뿐만 아니라 SignalR을 사용 하는 여러 가지 전송에는 자체의 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-153">In addition to requiring certain browsers, the various transports that SignalR uses have requirements of their own.</span></span> <span data-ttu-id="eaa87-154">에서는 다음과 같은 전송은 다음 구성에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-154">The following transports are supported under the following configurations:</span></span>

<a id="browser"></a>

<span data-ttu-id="eaa87-155">**웹 브라우저에 대 한 전송 요구 사항**</span><span class="sxs-lookup"><span data-stu-id="eaa87-155">**Web Browser Transport Requirements**</span></span>

| <span data-ttu-id="eaa87-156">전송</span><span class="sxs-lookup"><span data-stu-id="eaa87-156">Transport</span></span> | <span data-ttu-id="eaa87-157">Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="eaa87-157">Internet Explorer</span></span> | <span data-ttu-id="eaa87-158">Chrome (Windows 또는 iOS)</span><span class="sxs-lookup"><span data-stu-id="eaa87-158">Chrome (Windows or iOS)</span></span> | <span data-ttu-id="eaa87-159">Firefox</span><span class="sxs-lookup"><span data-stu-id="eaa87-159">Firefox</span></span> | <span data-ttu-id="eaa87-160">Safari (OSX 또는 iOS)</span><span class="sxs-lookup"><span data-stu-id="eaa87-160">Safari (OSX or iOS)</span></span> | <span data-ttu-id="eaa87-161">Android</span><span class="sxs-lookup"><span data-stu-id="eaa87-161">Android</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="eaa87-162">WebSocket</span><span class="sxs-lookup"><span data-stu-id="eaa87-162">WebSockets</span></span> | <span data-ttu-id="eaa87-163">10+</span><span class="sxs-lookup"><span data-stu-id="eaa87-163">10+</span></span> | <span data-ttu-id="eaa87-164">현재-1</span><span class="sxs-lookup"><span data-stu-id="eaa87-164">current - 1</span></span> | <span data-ttu-id="eaa87-165">현재-1</span><span class="sxs-lookup"><span data-stu-id="eaa87-165">current - 1</span></span> | <span data-ttu-id="eaa87-166">현재-1</span><span class="sxs-lookup"><span data-stu-id="eaa87-166">current - 1</span></span> | <span data-ttu-id="eaa87-167">N/A</span><span class="sxs-lookup"><span data-stu-id="eaa87-167">N/A</span></span> |
| <span data-ttu-id="eaa87-168">서버에서 전송 이벤트</span><span class="sxs-lookup"><span data-stu-id="eaa87-168">Server-Sent Events</span></span> | <span data-ttu-id="eaa87-169">N/A</span><span class="sxs-lookup"><span data-stu-id="eaa87-169">N/A</span></span> | <span data-ttu-id="eaa87-170">현재-1</span><span class="sxs-lookup"><span data-stu-id="eaa87-170">current - 1</span></span> | <span data-ttu-id="eaa87-171">현재-1</span><span class="sxs-lookup"><span data-stu-id="eaa87-171">current - 1</span></span> | <span data-ttu-id="eaa87-172">현재-1</span><span class="sxs-lookup"><span data-stu-id="eaa87-172">current - 1</span></span> | <span data-ttu-id="eaa87-173">N/A</span><span class="sxs-lookup"><span data-stu-id="eaa87-173">N/A</span></span> |
| <span data-ttu-id="eaa87-174">ForeverFrame</span><span class="sxs-lookup"><span data-stu-id="eaa87-174">ForeverFrame</span></span> | <span data-ttu-id="eaa87-175">8+</span><span class="sxs-lookup"><span data-stu-id="eaa87-175">8+</span></span> | <span data-ttu-id="eaa87-176">N/A</span><span class="sxs-lookup"><span data-stu-id="eaa87-176">N/A</span></span> | <span data-ttu-id="eaa87-177">N/A</span><span class="sxs-lookup"><span data-stu-id="eaa87-177">N/A</span></span> | <span data-ttu-id="eaa87-178">N/A</span><span class="sxs-lookup"><span data-stu-id="eaa87-178">N/A</span></span> | <span data-ttu-id="eaa87-179">4.1</span><span class="sxs-lookup"><span data-stu-id="eaa87-179">4.1</span></span> |
| <span data-ttu-id="eaa87-180">긴 폴링</span><span class="sxs-lookup"><span data-stu-id="eaa87-180">Long Polling</span></span> | <span data-ttu-id="eaa87-181">8+</span><span class="sxs-lookup"><span data-stu-id="eaa87-181">8+</span></span> | <span data-ttu-id="eaa87-182">현재-1</span><span class="sxs-lookup"><span data-stu-id="eaa87-182">current - 1</span></span> | <span data-ttu-id="eaa87-183">현재-1</span><span class="sxs-lookup"><span data-stu-id="eaa87-183">current - 1</span></span> | <span data-ttu-id="eaa87-184">현재-1</span><span class="sxs-lookup"><span data-stu-id="eaa87-184">current - 1</span></span> | <span data-ttu-id="eaa87-185">4.1</span><span class="sxs-lookup"><span data-stu-id="eaa87-185">4.1</span></span> |

<span data-ttu-id="eaa87-186">\*: 6 + 완전 한 기능에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-186">\*: 6+ required for full functionality.</span></span>

#### <a name="unsupported-browsers"></a><span data-ttu-id="eaa87-187">지원 되지 않는 브라우저</span><span class="sxs-lookup"><span data-stu-id="eaa87-187">Unsupported Browsers</span></span>

<span data-ttu-id="eaa87-188">SignalR 동안 *수* 적극적으로 SignalR에 테스트 하지 않습니다 및 일반적으로 여기에 표시 될 수 있는 버그를 수정 하지 않는 이전 버전의 브라우저에서 주요 문제 없이 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-188">While SignalR *may* run without major issues in older browser versions, we do not actively test SignalR in them and generally do not fix bugs that may appear in them.</span></span>

### <a name="windows-desktop-and-silverlight-applications"></a><span data-ttu-id="eaa87-189">Windows 바탕 화면 및 Silverlight 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="eaa87-189">Windows Desktop and Silverlight Applications</span></span>

<span data-ttu-id="eaa87-190">웹 브라우저에서 실행 하는 것 외에도 SignalR 독립 실행형 Windows 클라이언트 또는 Silverlight 응용 프로그램에서 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-190">In addition to running in a web browser, SignalR can be hosted in standalone Windows client or Silverlight applications.</span></span> <span data-ttu-id="eaa87-191">Windows 바탕 화면 및 Silverlight SignalR 응용 프로그램에는 다음 시스템 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-191">Windows Desktop and Silverlight SignalR applications have the following system requirements.</span></span>

- <span data-ttu-id="eaa87-192">.NET 4를 사용 하 여 응용 프로그램은 Windows XP SP3 이상을 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-192">Applications using .NET 4 are supported on Windows XP SP3 or later.</span></span>
- <span data-ttu-id="eaa87-193">.NET Framework 4.5를 사용 하 여 응용 프로그램은 Windows Vista 이상을 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-193">Applications using .NET Framework 4.5 are supported on Windows Vista or later.</span></span>

<span data-ttu-id="eaa87-194">운영 체제 및.NET framework 요구 사항 외에도 SignalR을 사용할 수 있는 전송에는 자체의 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-194">In addition to operating system and .NET framework requirements, the transports available to SignalR have requirements of their own.</span></span> <span data-ttu-id="eaa87-195">에서는 다음과 같은 전송은 다음 구성에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-195">The following transports are supported under the following configurations:</span></span>

<span data-ttu-id="eaa87-196">**Windows 바탕 화면 및 Silverlight 전송 요구 사항**</span><span class="sxs-lookup"><span data-stu-id="eaa87-196">**Windows Desktop and Silverlight Transport Requirements**</span></span>

| <span data-ttu-id="eaa87-197">전송</span><span class="sxs-lookup"><span data-stu-id="eaa87-197">Transport</span></span> | <span data-ttu-id="eaa87-198">.NET 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="eaa87-198">.NET application</span></span> | <span data-ttu-id="eaa87-199">Silverlight</span><span class="sxs-lookup"><span data-stu-id="eaa87-199">Silverlight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eaa87-200">웹 소켓</span><span class="sxs-lookup"><span data-stu-id="eaa87-200">Web Sockets</span></span> | <span data-ttu-id="eaa87-201">Windows 8 + 및.NET 4.5 이상</span><span class="sxs-lookup"><span data-stu-id="eaa87-201">Windows 8+ and .NET 4.5+</span></span> | <span data-ttu-id="eaa87-202">N/A</span><span class="sxs-lookup"><span data-stu-id="eaa87-202">N/A</span></span> |
| <span data-ttu-id="eaa87-203">영원히 프레임</span><span class="sxs-lookup"><span data-stu-id="eaa87-203">Forever Frame</span></span> | <span data-ttu-id="eaa87-204">N/A</span><span class="sxs-lookup"><span data-stu-id="eaa87-204">N/A</span></span> | <span data-ttu-id="eaa87-205">N/A</span><span class="sxs-lookup"><span data-stu-id="eaa87-205">N/A</span></span> |
| <span data-ttu-id="eaa87-206">서버에서 전송 이벤트</span><span class="sxs-lookup"><span data-stu-id="eaa87-206">Server-Sent Events</span></span> | <span data-ttu-id="eaa87-207">.NET 4+</span><span class="sxs-lookup"><span data-stu-id="eaa87-207">.NET 4+</span></span> | <span data-ttu-id="eaa87-208">5+</span><span class="sxs-lookup"><span data-stu-id="eaa87-208">5+</span></span> |
| <span data-ttu-id="eaa87-209">긴 폴링</span><span class="sxs-lookup"><span data-stu-id="eaa87-209">Long Polling</span></span> | <span data-ttu-id="eaa87-210">.NET 4+</span><span class="sxs-lookup"><span data-stu-id="eaa87-210">.NET 4+</span></span> | <span data-ttu-id="eaa87-211">5+</span><span class="sxs-lookup"><span data-stu-id="eaa87-211">5+</span></span> |

<a id="android"></a>

### <a name="windows-store-and-windows-phone-applications"></a><span data-ttu-id="eaa87-212">Windows 스토어 및 Windows Phone 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="eaa87-212">Windows Store and Windows Phone Applications</span></span>

<span data-ttu-id="eaa87-213">SignalR은 Windows 스토어 응용 프로그램 및 Windows Phone 8 응용 프로그램에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-213">SignalR can be used in Windows Store applications and Windows Phone 8 applications.</span></span> <span data-ttu-id="eaa87-214">에서는 다음과 같은 전송은 다음 구성에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-214">The following transports are supported under the following configurations:</span></span>

<span data-ttu-id="eaa87-215">**Windows 스토어 및 Windows Phone 전송 요구 사항**</span><span class="sxs-lookup"><span data-stu-id="eaa87-215">**Windows Store and Windows Phone Transport Requirements**</span></span>

| <span data-ttu-id="eaa87-216">전송</span><span class="sxs-lookup"><span data-stu-id="eaa87-216">Transport</span></span> | <span data-ttu-id="eaa87-217">Windows 스토어 /.NET</span><span class="sxs-lookup"><span data-stu-id="eaa87-217">Windows Store/ .NET</span></span> | <span data-ttu-id="eaa87-218">Windows 스토어 / JavaScript</span><span class="sxs-lookup"><span data-stu-id="eaa87-218">Windows Store/ JavaScript</span></span> | <span data-ttu-id="eaa87-219">Windows Phone / IE</span><span class="sxs-lookup"><span data-stu-id="eaa87-219">Windows Phone/ IE</span></span> | <span data-ttu-id="eaa87-220">Windows Phone /.NET</span><span class="sxs-lookup"><span data-stu-id="eaa87-220">Windows Phone/ .NET</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="eaa87-221">WebSocket</span><span class="sxs-lookup"><span data-stu-id="eaa87-221">WebSockets</span></span> | <span data-ttu-id="eaa87-222">N/A</span><span class="sxs-lookup"><span data-stu-id="eaa87-222">N/A</span></span> | <span data-ttu-id="eaa87-223">Win8+</span><span class="sxs-lookup"><span data-stu-id="eaa87-223">Win8+</span></span> | <span data-ttu-id="eaa87-224">8+</span><span class="sxs-lookup"><span data-stu-id="eaa87-224">8+</span></span> | <span data-ttu-id="eaa87-225">N/A</span><span class="sxs-lookup"><span data-stu-id="eaa87-225">N/A</span></span> |
| <span data-ttu-id="eaa87-226">영원히 프레임</span><span class="sxs-lookup"><span data-stu-id="eaa87-226">Forever Frame</span></span> | <span data-ttu-id="eaa87-227">N/A</span><span class="sxs-lookup"><span data-stu-id="eaa87-227">N/A</span></span> | <span data-ttu-id="eaa87-228">Win8+</span><span class="sxs-lookup"><span data-stu-id="eaa87-228">Win8+</span></span> | <span data-ttu-id="eaa87-229">7.5+</span><span class="sxs-lookup"><span data-stu-id="eaa87-229">7.5+</span></span> | <span data-ttu-id="eaa87-230">N/A</span><span class="sxs-lookup"><span data-stu-id="eaa87-230">N/A</span></span> |
| <span data-ttu-id="eaa87-231">서버에서 전송 이벤트</span><span class="sxs-lookup"><span data-stu-id="eaa87-231">Server-Sent Events</span></span> | <span data-ttu-id="eaa87-232">Win8+</span><span class="sxs-lookup"><span data-stu-id="eaa87-232">Win8+</span></span> | <span data-ttu-id="eaa87-233">N/A</span><span class="sxs-lookup"><span data-stu-id="eaa87-233">N/A</span></span> | <span data-ttu-id="eaa87-234">N/A</span><span class="sxs-lookup"><span data-stu-id="eaa87-234">N/A</span></span> | <span data-ttu-id="eaa87-235">8+</span><span class="sxs-lookup"><span data-stu-id="eaa87-235">8+</span></span> |
| <span data-ttu-id="eaa87-236">긴 폴링</span><span class="sxs-lookup"><span data-stu-id="eaa87-236">Long Polling</span></span> | <span data-ttu-id="eaa87-237">Win8+</span><span class="sxs-lookup"><span data-stu-id="eaa87-237">Win8+</span></span> | <span data-ttu-id="eaa87-238">Win8+</span><span class="sxs-lookup"><span data-stu-id="eaa87-238">Win8+</span></span> | <span data-ttu-id="eaa87-239">7.5+</span><span class="sxs-lookup"><span data-stu-id="eaa87-239">7.5+</span></span> | <span data-ttu-id="eaa87-240">8+</span><span class="sxs-lookup"><span data-stu-id="eaa87-240">8+</span></span> |

<a id="updates"></a>

## <a name="recommended-updates"></a><span data-ttu-id="eaa87-241">권장 되는 업데이트</span><span class="sxs-lookup"><span data-stu-id="eaa87-241">Recommended Updates</span></span>

<span data-ttu-id="eaa87-242">SignalR의 서버에 대 한 다음 업데이트를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-242">The following updates are recommended for SignalR servers:</span></span>

- <span data-ttu-id="eaa87-243">.NET Framework 4.5에 대 한 업데이트를 사용할 수 [여기](https://support.microsoft.com/kb/2750149)합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-243">An update for .NET Framework 4.5 is available [here](https://support.microsoft.com/kb/2750149).</span></span>
- <span data-ttu-id="eaa87-244">Microsoft은 ASP.NET에 대 한 Qfe를 정기적으로 해제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-244">Microsoft will periodically release QFEs for ASP.NET.</span></span> <span data-ttu-id="eaa87-245">이 사용 가능으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa87-245">These should be applied as available.</span></span>
