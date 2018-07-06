---
uid: signalr/overview/getting-started/supported-platforms
title: 지원 되는 플랫폼 | Microsoft Docs
author: pfletcher
description: 이 문서에서는 어떤 클라이언트 및 서버에 SignalR 지 설명 합니다.
ms.author: aspnetcontent
ms.date: 04/18/2018
ms.assetid: eac31beb-0f46-4afa-9def-e80904dea4f0
msc.legacyurl: /signalr/overview/getting-started/supported-platforms
msc.type: authoredcontent
ms.openlocfilehash: 5d77db71c5c6b0c297756921b5b7cb79add03998
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37805813"
---
<a name="supported-platforms"></a><span data-ttu-id="c755f-103">지원되는 플랫폼</span><span class="sxs-lookup"><span data-stu-id="c755f-103">Supported Platforms</span></span>
====================
<span data-ttu-id="c755f-104">[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="c755f-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

> <span data-ttu-id="c755f-105">이 문서에서는 어떤 클라이언트 및 서버에 SignalR 지 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-105">This article describes what clients and servers are supported by SignalR.</span></span> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="c755f-106">질문이 나 의견이 있으면</span><span class="sxs-lookup"><span data-stu-id="c755f-106">Questions and comments</span></span>
> 
> <span data-ttu-id="c755f-107">이 자습서를 연결 하는 방법 및 새로운 개선할 수 있습니다 페이지의 맨 아래에 의견에서에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="c755f-107">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="c755f-108">에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-108">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<span data-ttu-id="c755f-109">SignalR은 다양 한 서버 및 클라이언트 구성에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-109">SignalR is supported under a variety of server and client configurations.</span></span> <span data-ttu-id="c755f-110">또한 각 전송 옵션에는 고유한; 요구 사항 전송에 대 한 시스템 요구 사항에 사용할 수 없으면 SignalR 정상적으로 장애 조치 다른 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-110">In addition, each transport option has a set of requirements of its own; if the system requirements for a transport are not available, SignalR will gracefully failover to other transports.</span></span> <span data-ttu-id="c755f-111">SignalR을 지 원하는 전송에 대 한 자세한 내용은 참조 하세요. [전송과 대체](introduction-to-signalr.md#transports)합니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-111">For more information on the transports that SignalR supports, see [Transports and Fallbacks](introduction-to-signalr.md#transports).</span></span>

## <a name="server-system-requirements"></a><span data-ttu-id="c755f-112">서버 시스템 요구 사항</span><span class="sxs-lookup"><span data-stu-id="c755f-112">Server system requirements</span></span>

<span data-ttu-id="c755f-113">다양 한 서버 구성에서 SignalR 서버 구성 요소를 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-113">The SignalR server component can be hosted on a variety of server configurations.</span></span> <span data-ttu-id="c755f-114">이 섹션에서는 지원 되는 버전의 운영 체제,.NET framework, 인터넷 정보 서버 및 기타 구성 요소를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-114">This section describes the supported versions of operating systems, .NET framework, Internet Information Server, and other components.</span></span>

### <a name="supported-server-operating-systems"></a><span data-ttu-id="c755f-115">지원되는 서버 운영 체제</span><span class="sxs-lookup"><span data-stu-id="c755f-115">Supported server operating systems</span></span>

<span data-ttu-id="c755f-116">다음 서버 또는 클라이언트 운영 체제에서 SignalR 서버 구성 요소를 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-116">The SignalR server component can be hosted in the following server or client operating systems.</span></span> <span data-ttu-id="c755f-117">Websocket을 사용 하는 SignalR에 대 한 Windows Server 2012, Windows Server 2016 또는 Windows 8이 필요 (WebSocket 사용할 수 있습니다 Windows Azure 웹 사이트에서 사이트의.NET framework 버전 4.5로 설정 되어 있고 웹 소켓 사이트의 사용 가능 구성 페이지)입니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-117">Note that for SignalR to use WebSockets, Windows Server 2012, Windows Server 2016, or Windows 8 is required (WebSocket can be used on Windows Azure Web Sites, as long as the site's .NET framework version is set to 4.5, and Web Sockets is enabled in the site's Configuration page).</span></span>

- <span data-ttu-id="c755f-118">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="c755f-118">Windows Server 2016</span></span>
- <span data-ttu-id="c755f-119">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="c755f-119">Windows Server 2012</span></span>
- <span data-ttu-id="c755f-120">Windows Server 2008 r2</span><span class="sxs-lookup"><span data-stu-id="c755f-120">Windows Server 2008 r2</span></span>
- <span data-ttu-id="c755f-121">Windows 10</span><span class="sxs-lookup"><span data-stu-id="c755f-121">Windows 10</span></span>
- <span data-ttu-id="c755f-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="c755f-122">Windows 8</span></span>
- <span data-ttu-id="c755f-123">Windows 7</span><span class="sxs-lookup"><span data-stu-id="c755f-123">Windows 7</span></span>
- <span data-ttu-id="c755f-124">Windows Azure</span><span class="sxs-lookup"><span data-stu-id="c755f-124">Windows Azure</span></span>

### <a name="supported-server-net-framework-version"></a><span data-ttu-id="c755f-125">지원 되는 서버.NET Framework 버전</span><span class="sxs-lookup"><span data-stu-id="c755f-125">Supported server .NET Framework version</span></span>

<span data-ttu-id="c755f-126">.NET Framework 4.5에서 SignalR 2 에서만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-126">SignalR 2 is only supported on .NET Framework 4.5.</span></span> <span data-ttu-id="c755f-127">참조 된 [권장 업데이트](#updates) 안정성, 호환성, 안정성 및 성능을 향상 시키는 업데이트에 대 한 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-127">See the [Recommended Updates](#updates) section for updates that enhance reliability, compatibility, stability, and performance.</span></span>

### <a name="supported-server-iis-versions"></a><span data-ttu-id="c755f-128">지원 되는 서버 IIS 버전</span><span class="sxs-lookup"><span data-stu-id="c755f-128">Supported server IIS versions</span></span>

<span data-ttu-id="c755f-129">SignalR IIS에서 호스트 되는 경우 다음 버전은 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-129">When SignalR is hosted in IIS, the following versions are supported.</span></span> <span data-ttu-id="c755f-130">클라이언트 운영 체제를 사용 하는 경우와 같은 개발에 대 한 (Windows 8 또는 Windows 7)에서는 전체 버전의 IIS 또는 Cassini 쓰일 수 없습니다, 최대 연결 이후 아주 빨리 도달할 수 있는 10 개의 동시 연결에 적용 될 것 이므로 note 일시적이 지를 자주 다시 설정 되며 삭제 되지 않습니다 즉시 더 이상 사용 되지 시.</span><span class="sxs-lookup"><span data-stu-id="c755f-130">Note that if a client operating system is used, such as for development (Windows 8 or Windows 7), full versions of IIS or Cassini should not be used, since there will be a limit of 10 simultaneous connections imposed, which will be reached very quickly since connections are transient, frequently re-established, and are not disposed immediately upon no longer being used.</span></span> <span data-ttu-id="c755f-131">클라이언트 운영 체제에서 IIS Express를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-131">IIS Express should be used on client operating systems.</span></span>

<span data-ttu-id="c755f-132">또한 WebSocket을 사용 하는 SignalR에 대 한 IIS 8 또는 IIS 8 Express를 사용 해야 합니다, 서버를 Windows 8, Windows Server 2012 이상을 사용 해야 합니다을 IIS에서 WebSocket을 활성화 해야 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-132">Also note that for SignalR to use WebSocket, IIS 8 or IIS 8 Express must be used, the server must be using Windows 8, Windows Server 2012, or later, and WebSocket must be enabled in IIS.</span></span> <span data-ttu-id="c755f-133">IIS에서 WebSocket을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [IIS 8.0 WebSocket 프로토콜 지원](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support)합니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-133">For information on how to enable WebSocket in IIS, see [IIS 8.0 WebSocket Protocol Support](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support).</span></span>

- <span data-ttu-id="c755f-134">IIS 8 또는 IIS 8 Express입니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-134">IIS 8 or IIS 8 Express.</span></span>
- <span data-ttu-id="c755f-135">IIS 7 및 7.5입니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-135">IIS 7 and 7.5.</span></span> <span data-ttu-id="c755f-136">에 대 한 지원 [확장명 없는 Url](https://support.microsoft.com/kb/980368) 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-136">Support for [extensionless URLs](https://support.microsoft.com/kb/980368) is required.</span></span>
- <span data-ttu-id="c755f-137">IIS 통합된 모드에서 실행 되어야 합니다. 클래식 모드는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-137">IIS must be running in integrated mode; classic mode is not supported.</span></span> <span data-ttu-id="c755f-138">최대 30 초의 메시지 지연 Server-Sent 이벤트 전송을 사용 하 여 클래식 모드에서 IIS를 실행 하는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-138">Message delays of up to 30 seconds may be experienced if IIS is run in classic mode using the Server-Sent Events transport.</span></span>
- <span data-ttu-id="c755f-139">호스팅 응용 프로그램은 완전 신뢰 모드로 실행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-139">The hosting application must be running in full trust mode.</span></span>

## <a name="client-system-requirements"></a><span data-ttu-id="c755f-140">클라이언트 시스템 요구 사항</span><span class="sxs-lookup"><span data-stu-id="c755f-140">Client system requirements</span></span>

<span data-ttu-id="c755f-141">다양 한 클라이언트 플랫폼에서에서 SignalR은 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-141">SignalR can be used in a variety of client platforms.</span></span> <span data-ttu-id="c755f-142">이 섹션에는 SignalR을 사용 하 여 웹 브라우저, Windows 데스크톱 응용 프로그램, Silverlight 응용 프로그램 및 모바일 장치에 대 한 시스템 요구 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-142">This section describes the system requirements for using SignalR in web browsers, Windows desktop applications, Silverlight applications, and mobile devices.</span></span>

### <a name="web-browsers"></a><span data-ttu-id="c755f-143">웹 브라우저</span><span class="sxs-lookup"><span data-stu-id="c755f-143">Web browsers</span></span>

<span data-ttu-id="c755f-144">SignalR을 다양 한 웹 브라우저에서에서 사용할 수 있지만 일반적으로 최신 두 버전 에서만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-144">SignalR can be used in a variety of web browsers, but typically, only the latest two versions are supported.</span></span>

<span data-ttu-id="c755f-145">브라우저에서 SignalR을 사용 하는 응용 프로그램에는 jQuery 버전 1.6.4 또는 주 이상 버전 (예: 1.7.2, 1.8.2, 또는 1.9.1) 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-145">Applications that use SignalR in browsers must use jQuery version 1.6.4 or major later versions (such as 1.7.2, 1.8.2, or 1.9.1).</span></span>

<span data-ttu-id="c755f-146">다음 브라우저에서 SignalR은 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-146">SignalR can be used in the following browsers:</span></span>

- <span data-ttu-id="c755f-147">Microsoft Internet Explorer 버전 8, 9, 10 및 11입니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-147">Microsoft Internet Explorer versions 8, 9, 10, and 11.</span></span> <span data-ttu-id="c755f-148">최신 데스크톱 및 모바일 버전 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-148">Modern, Desktop, and Mobile versions are supported.</span></span>
- <span data-ttu-id="c755f-149">Mozilla Firefox: 현재 버전-1, Windows 및 Mac 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-149">Mozilla Firefox: current version - 1, both Windows and Mac versions.</span></span>
- <span data-ttu-id="c755f-150">Google Chrome: 현재 버전-1, Windows 및 Mac 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-150">Google Chrome: current version - 1, both Windows and Mac versions.</span></span>
- <span data-ttu-id="c755f-151">Safari: 현재 버전-1, Mac 및 iOS 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-151">Safari: current version - 1, both Mac and iOS versions.</span></span>
- <span data-ttu-id="c755f-152">Opera: 현재 버전-1, Windows에만 합니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-152">Opera: current version - 1, Windows only.</span></span>
- <span data-ttu-id="c755f-153">Android 브라우저</span><span class="sxs-lookup"><span data-stu-id="c755f-153">Android browser</span></span>

<span data-ttu-id="c755f-154">특정 브라우저에 요구 하는 것 외에도 SignalR을 사용 하는 다양 한 전송에는 자체의 요구 사항을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-154">In addition to requiring certain browsers, the various transports that SignalR uses have requirements of their own.</span></span> <span data-ttu-id="c755f-155">다음 전송 다음 구성에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-155">The following transports are supported under the following configurations:</span></span>

<a id="browser"></a>

<span data-ttu-id="c755f-156">**웹 브라우저에 대 한 전송 요구 사항**</span><span class="sxs-lookup"><span data-stu-id="c755f-156">**Web Browser Transport Requirements**</span></span>

| <span data-ttu-id="c755f-157">전송</span><span class="sxs-lookup"><span data-stu-id="c755f-157">Transport</span></span> | <span data-ttu-id="c755f-158">Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="c755f-158">Internet Explorer</span></span> | <span data-ttu-id="c755f-159">Chrome (Windows 또는 iOS)</span><span class="sxs-lookup"><span data-stu-id="c755f-159">Chrome (Windows or iOS)</span></span> | <span data-ttu-id="c755f-160">Firefox</span><span class="sxs-lookup"><span data-stu-id="c755f-160">Firefox</span></span> | <span data-ttu-id="c755f-161">Safari (OSX 또는 iOS)</span><span class="sxs-lookup"><span data-stu-id="c755f-161">Safari (OSX or iOS)</span></span> | <span data-ttu-id="c755f-162">Android</span><span class="sxs-lookup"><span data-stu-id="c755f-162">Android</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="c755f-163">WebSocket</span><span class="sxs-lookup"><span data-stu-id="c755f-163">WebSockets</span></span> | <span data-ttu-id="c755f-164">10+</span><span class="sxs-lookup"><span data-stu-id="c755f-164">10+</span></span> | <span data-ttu-id="c755f-165">1-현재</span><span class="sxs-lookup"><span data-stu-id="c755f-165">current - 1</span></span> | <span data-ttu-id="c755f-166">1-현재</span><span class="sxs-lookup"><span data-stu-id="c755f-166">current - 1</span></span> | <span data-ttu-id="c755f-167">1-현재</span><span class="sxs-lookup"><span data-stu-id="c755f-167">current - 1</span></span> | <span data-ttu-id="c755f-168">N/A</span><span class="sxs-lookup"><span data-stu-id="c755f-168">N/A</span></span> |
| <span data-ttu-id="c755f-169">서버에서 전송 이벤트</span><span class="sxs-lookup"><span data-stu-id="c755f-169">Server-Sent Events</span></span> | <span data-ttu-id="c755f-170">N/A</span><span class="sxs-lookup"><span data-stu-id="c755f-170">N/A</span></span> | <span data-ttu-id="c755f-171">1-현재</span><span class="sxs-lookup"><span data-stu-id="c755f-171">current - 1</span></span> | <span data-ttu-id="c755f-172">1-현재</span><span class="sxs-lookup"><span data-stu-id="c755f-172">current - 1</span></span> | <span data-ttu-id="c755f-173">1-현재</span><span class="sxs-lookup"><span data-stu-id="c755f-173">current - 1</span></span> | <span data-ttu-id="c755f-174">N/A</span><span class="sxs-lookup"><span data-stu-id="c755f-174">N/A</span></span> |
| <span data-ttu-id="c755f-175">ForeverFrame</span><span class="sxs-lookup"><span data-stu-id="c755f-175">ForeverFrame</span></span> | <span data-ttu-id="c755f-176">8+</span><span class="sxs-lookup"><span data-stu-id="c755f-176">8+</span></span> | <span data-ttu-id="c755f-177">N/A</span><span class="sxs-lookup"><span data-stu-id="c755f-177">N/A</span></span> | <span data-ttu-id="c755f-178">N/A</span><span class="sxs-lookup"><span data-stu-id="c755f-178">N/A</span></span> | <span data-ttu-id="c755f-179">N/A</span><span class="sxs-lookup"><span data-stu-id="c755f-179">N/A</span></span> | <span data-ttu-id="c755f-180">4.1</span><span class="sxs-lookup"><span data-stu-id="c755f-180">4.1</span></span> |
| <span data-ttu-id="c755f-181">긴 폴링</span><span class="sxs-lookup"><span data-stu-id="c755f-181">Long Polling</span></span> | <span data-ttu-id="c755f-182">8+</span><span class="sxs-lookup"><span data-stu-id="c755f-182">8+</span></span> | <span data-ttu-id="c755f-183">1-현재</span><span class="sxs-lookup"><span data-stu-id="c755f-183">current - 1</span></span> | <span data-ttu-id="c755f-184">1-현재</span><span class="sxs-lookup"><span data-stu-id="c755f-184">current - 1</span></span> | <span data-ttu-id="c755f-185">1-현재</span><span class="sxs-lookup"><span data-stu-id="c755f-185">current - 1</span></span> | <span data-ttu-id="c755f-186">4.1</span><span class="sxs-lookup"><span data-stu-id="c755f-186">4.1</span></span> |

<span data-ttu-id="c755f-187">\*: 6 이상 전체 기능에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-187">\*: 6+ required for full functionality.</span></span>

#### <a name="unsupported-browsers"></a><span data-ttu-id="c755f-188">지원 되지 않는 브라우저</span><span class="sxs-lookup"><span data-stu-id="c755f-188">Unsupported Browsers</span></span>

<span data-ttu-id="c755f-189">SignalR while *있습니다* 를 이전 버전의 브라우저에서 주요 문제 없이 실행에서 SignalR을 적극적으로 테스트 하지 마십시오 하 고 일반적으로에 나타날 수 있는 버그를 수정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-189">While SignalR *may* run without major issues in older browser versions, we do not actively test SignalR in them and generally do not fix bugs that may appear in them.</span></span>

### <a name="windows-desktop-and-silverlight-applications"></a><span data-ttu-id="c755f-190">Windows 데스크톱 및 Silverlight 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="c755f-190">Windows Desktop and Silverlight Applications</span></span>

<span data-ttu-id="c755f-191">웹 브라우저에서 실행 하는 것 외에도 SignalR 독립 실행형 Windows 클라이언트 또는 Silverlight 응용 프로그램에서 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-191">In addition to running in a web browser, SignalR can be hosted in standalone Windows client or Silverlight applications.</span></span> <span data-ttu-id="c755f-192">Windows 데스크톱 및 Silverlight SignalR 응용 프로그램 같은 시스템 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-192">Windows Desktop and Silverlight SignalR applications have the following system requirements.</span></span>

- <span data-ttu-id="c755f-193">.NET 4를 사용 하 여 응용 프로그램은 Windows XP SP3 이상을 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-193">Applications using .NET 4 are supported on Windows XP SP3 or later.</span></span>
- <span data-ttu-id="c755f-194">.NET Framework 4.5를 사용 하 여 응용 프로그램은 Windows Vista 이상을 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-194">Applications using .NET Framework 4.5 are supported on Windows Vista or later.</span></span>

<span data-ttu-id="c755f-195">운영 체제 및.NET framework 요구 사항 외에도 SignalR을 사용할 수 있는 전송에는 자체의 요구 사항을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-195">In addition to operating system and .NET framework requirements, the transports available to SignalR have requirements of their own.</span></span> <span data-ttu-id="c755f-196">다음 전송 다음 구성에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-196">The following transports are supported under the following configurations:</span></span>

<span data-ttu-id="c755f-197">**Windows 데스크톱 및 Silverlight 전송 요구 사항**</span><span class="sxs-lookup"><span data-stu-id="c755f-197">**Windows Desktop and Silverlight Transport Requirements**</span></span>

| <span data-ttu-id="c755f-198">전송</span><span class="sxs-lookup"><span data-stu-id="c755f-198">Transport</span></span> | <span data-ttu-id="c755f-199">.NET 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="c755f-199">.NET application</span></span> | <span data-ttu-id="c755f-200">Silverlight</span><span class="sxs-lookup"><span data-stu-id="c755f-200">Silverlight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c755f-201">웹 소켓</span><span class="sxs-lookup"><span data-stu-id="c755f-201">Web Sockets</span></span> | <span data-ttu-id="c755f-202">Windows 8 이상 및.NET 4.5 이상</span><span class="sxs-lookup"><span data-stu-id="c755f-202">Windows 8+ and .NET 4.5+</span></span> | <span data-ttu-id="c755f-203">N/A</span><span class="sxs-lookup"><span data-stu-id="c755f-203">N/A</span></span> |
| <span data-ttu-id="c755f-204">영원히 프레임</span><span class="sxs-lookup"><span data-stu-id="c755f-204">Forever Frame</span></span> | <span data-ttu-id="c755f-205">N/A</span><span class="sxs-lookup"><span data-stu-id="c755f-205">N/A</span></span> | <span data-ttu-id="c755f-206">N/A</span><span class="sxs-lookup"><span data-stu-id="c755f-206">N/A</span></span> |
| <span data-ttu-id="c755f-207">서버에서 전송 이벤트</span><span class="sxs-lookup"><span data-stu-id="c755f-207">Server-Sent Events</span></span> | <span data-ttu-id="c755f-208">.NET 4+</span><span class="sxs-lookup"><span data-stu-id="c755f-208">.NET 4+</span></span> | <span data-ttu-id="c755f-209">5+</span><span class="sxs-lookup"><span data-stu-id="c755f-209">5+</span></span> |
| <span data-ttu-id="c755f-210">긴 폴링</span><span class="sxs-lookup"><span data-stu-id="c755f-210">Long Polling</span></span> | <span data-ttu-id="c755f-211">.NET 4+</span><span class="sxs-lookup"><span data-stu-id="c755f-211">.NET 4+</span></span> | <span data-ttu-id="c755f-212">5+</span><span class="sxs-lookup"><span data-stu-id="c755f-212">5+</span></span> |

<a id="android"></a>

### <a name="windows-store-and-windows-phone-applications"></a><span data-ttu-id="c755f-213">Windows 스토어 및 Windows Phone 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="c755f-213">Windows Store and Windows Phone Applications</span></span>

<span data-ttu-id="c755f-214">Windows 스토어 응용 프로그램 및 Windows Phone 8 응용 프로그램에서 SignalR은 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-214">SignalR can be used in Windows Store applications and Windows Phone 8 applications.</span></span> <span data-ttu-id="c755f-215">다음 전송 다음 구성에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-215">The following transports are supported under the following configurations:</span></span>

<span data-ttu-id="c755f-216">**Windows 스토어 및 Windows Phone 전송 요구 사항**</span><span class="sxs-lookup"><span data-stu-id="c755f-216">**Windows Store and Windows Phone Transport Requirements**</span></span>

| <span data-ttu-id="c755f-217">전송</span><span class="sxs-lookup"><span data-stu-id="c755f-217">Transport</span></span> | <span data-ttu-id="c755f-218">Windows 스토어 /.NET</span><span class="sxs-lookup"><span data-stu-id="c755f-218">Windows Store/ .NET</span></span> | <span data-ttu-id="c755f-219">Windows 스토어 / JavaScript</span><span class="sxs-lookup"><span data-stu-id="c755f-219">Windows Store/ JavaScript</span></span> | <span data-ttu-id="c755f-220">Windows Phone / IE</span><span class="sxs-lookup"><span data-stu-id="c755f-220">Windows Phone/ IE</span></span> | <span data-ttu-id="c755f-221">Windows Phone /.NET</span><span class="sxs-lookup"><span data-stu-id="c755f-221">Windows Phone/ .NET</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="c755f-222">WebSocket</span><span class="sxs-lookup"><span data-stu-id="c755f-222">WebSockets</span></span> | <span data-ttu-id="c755f-223">N/A</span><span class="sxs-lookup"><span data-stu-id="c755f-223">N/A</span></span> | <span data-ttu-id="c755f-224">Win8 +</span><span class="sxs-lookup"><span data-stu-id="c755f-224">Win8+</span></span> | <span data-ttu-id="c755f-225">8+</span><span class="sxs-lookup"><span data-stu-id="c755f-225">8+</span></span> | <span data-ttu-id="c755f-226">N/A</span><span class="sxs-lookup"><span data-stu-id="c755f-226">N/A</span></span> |
| <span data-ttu-id="c755f-227">영원히 프레임</span><span class="sxs-lookup"><span data-stu-id="c755f-227">Forever Frame</span></span> | <span data-ttu-id="c755f-228">N/A</span><span class="sxs-lookup"><span data-stu-id="c755f-228">N/A</span></span> | <span data-ttu-id="c755f-229">Win8 +</span><span class="sxs-lookup"><span data-stu-id="c755f-229">Win8+</span></span> | <span data-ttu-id="c755f-230">7.5+</span><span class="sxs-lookup"><span data-stu-id="c755f-230">7.5+</span></span> | <span data-ttu-id="c755f-231">N/A</span><span class="sxs-lookup"><span data-stu-id="c755f-231">N/A</span></span> |
| <span data-ttu-id="c755f-232">서버에서 전송 이벤트</span><span class="sxs-lookup"><span data-stu-id="c755f-232">Server-Sent Events</span></span> | <span data-ttu-id="c755f-233">Win8 +</span><span class="sxs-lookup"><span data-stu-id="c755f-233">Win8+</span></span> | <span data-ttu-id="c755f-234">N/A</span><span class="sxs-lookup"><span data-stu-id="c755f-234">N/A</span></span> | <span data-ttu-id="c755f-235">N/A</span><span class="sxs-lookup"><span data-stu-id="c755f-235">N/A</span></span> | <span data-ttu-id="c755f-236">8+</span><span class="sxs-lookup"><span data-stu-id="c755f-236">8+</span></span> |
| <span data-ttu-id="c755f-237">긴 폴링</span><span class="sxs-lookup"><span data-stu-id="c755f-237">Long Polling</span></span> | <span data-ttu-id="c755f-238">Win8 +</span><span class="sxs-lookup"><span data-stu-id="c755f-238">Win8+</span></span> | <span data-ttu-id="c755f-239">Win8 +</span><span class="sxs-lookup"><span data-stu-id="c755f-239">Win8+</span></span> | <span data-ttu-id="c755f-240">7.5+</span><span class="sxs-lookup"><span data-stu-id="c755f-240">7.5+</span></span> | <span data-ttu-id="c755f-241">8+</span><span class="sxs-lookup"><span data-stu-id="c755f-241">8+</span></span> |

<a id="updates"></a>

## <a name="recommended-updates"></a><span data-ttu-id="c755f-242">권장 되는 업데이트</span><span class="sxs-lookup"><span data-stu-id="c755f-242">Recommended Updates</span></span>

<span data-ttu-id="c755f-243">SignalR 서버에 대 한 다음 업데이트를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-243">The following updates are recommended for SignalR servers:</span></span>

- <span data-ttu-id="c755f-244">.NET Framework 4.5에 대 한 업데이트를 사용할 수 있습니다 [여기](https://support.microsoft.com/kb/2750149)합니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-244">An update for .NET Framework 4.5 is available [here](https://support.microsoft.com/kb/2750149).</span></span>
- <span data-ttu-id="c755f-245">Microsoft은 ASP.NET 용 Qfe를 주기적으로 해제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-245">Microsoft will periodically release QFEs for ASP.NET.</span></span> <span data-ttu-id="c755f-246">이 사용 가능한 것으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c755f-246">These should be applied as available.</span></span>
