---
uid: signalr/overview/security/persistent-connection-authorization
title: SignalR 영구 연결 프로그램용 인증과 권한 부여 | Microsoft Docs
author: pfletcher
description: 이 항목에서는 영구 연결에 권한 부여를 적용 하는 방법을 설명 합니다. 보안 SignalR 응용 프로그램을 통합 하는 방법에 대 한 일반 정보에 대 한 중...
ms.author: riande
ms.date: 06/10/2014
ms.assetid: e264677b-9c01-47ec-94f9-3cd8f08f94af
msc.legacyurl: /signalr/overview/security/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: bbbcb5593fb265eca4fb261d378532047d53e674
ms.sourcegitcommit: 74e3be25ea37b5fc8b4b433b0b872547b4b99186
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2018
ms.locfileid: "53287392"
---
<a name="authentication-and-authorization-for-signalr-persistent-connections"></a><span data-ttu-id="2e60a-104">SignalR 영구 연결 프로그램용 인증과 권한 부여</span><span class="sxs-lookup"><span data-stu-id="2e60a-104">Authentication and Authorization for SignalR Persistent Connections</span></span>
====================
<span data-ttu-id="2e60a-105">하 여 [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="2e60a-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="2e60a-106">이 항목에서는 영구 연결에 권한 부여를 적용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e60a-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="2e60a-107">SignalR 응용 프로그램에 보안을 통합 하는 방법에 대 한 일반적인 정보를 참조 하세요 [보안 소개](introduction-to-security.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e60a-107">For general information about integrating security into a SignalR application, see [Introduction to Security](introduction-to-security.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="2e60a-108">이 항목에서 사용 하는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="2e60a-108">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="2e60a-109">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="2e60a-109">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="2e60a-110">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="2e60a-110">.NET 4.5</span></span>
> - <span data-ttu-id="2e60a-111">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="2e60a-111">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="2e60a-112">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="2e60a-112">Previous versions of this topic</span></span>
>
> <span data-ttu-id="2e60a-113">이전 버전의 SignalR에 대 한 정보를 참조 하세요 [SignalR 이전 버전](../older-versions/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e60a-113">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="2e60a-114">질문이 나 의견이 있으면</span><span class="sxs-lookup"><span data-stu-id="2e60a-114">Questions and comments</span></span>
>
> <span data-ttu-id="2e60a-115">이 자습서를 연결 하는 방법 및 새로운 개선할 수 있습니다 페이지의 맨 아래에 의견에서에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="2e60a-115">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="2e60a-116">에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e60a-116">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="enforce-authorization"></a><span data-ttu-id="2e60a-117">권한 부여를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e60a-117">Enforce authorization</span></span>

<span data-ttu-id="2e60a-118">사용 하는 경우 권한 부여 규칙을 적용 하는 [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) 재정의 해야 합니다는 `AuthorizeRequest` 메서드.</span><span class="sxs-lookup"><span data-stu-id="2e60a-118">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="2e60a-119">사용할 수 없습니다는 `Authorize` 영구 연결을 사용 하 여 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="2e60a-119">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="2e60a-120">`AuthorizeRequest` 사용자 요청된 작업을 수행할 권한이 있는지 확인 하는 모든 요청 전에 SignalR 프레임 워크에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e60a-120">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="2e60a-121">`AuthorizeRequest` 응용 프로그램의 표준 인증 메커니즘을 통해 사용자를 인증 하는 대신; 메서드가 클라이언트에서 호출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2e60a-121">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="2e60a-122">아래 예제에서는 인증 된 사용자에 대 한 요청을 제한 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2e60a-122">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="2e60a-123">AuthorizeRequest 메서드;에서 모든 사용자 지정된 권한 부여 논리를 추가할 수 있습니다. 와 같은 사용자 특정 역할에 속하는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e60a-123">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>
