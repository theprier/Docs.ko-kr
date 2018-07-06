---
uid: signalr/overview/older-versions/persistent-connection-authorization
title: SignalR 영구 연결 프로그램용 인증과 권한 부여 (SignalR 1.x) | Microsoft Docs
author: pfletcher
description: 이 항목에서는 영구 연결에 권한 부여를 적용 하는 방법을 설명 합니다. 보안 SignalR 응용 프로그램을 통합 하는 방법에 대 한 일반 정보에 대 한 중...
ms.author: aspnetcontent
ms.date: 10/21/2013
ms.assetid: c34bc627-41af-4c21-a817-e97a19a7f252
msc.legacyurl: /signalr/overview/older-versions/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 28984518346ef7e79c976a565dae5e5ab924b678
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37805329"
---
<a name="authentication-and-authorization-for-signalr-persistent-connections-signalr-1x"></a><span data-ttu-id="57531-104">SignalR 영구 연결 프로그램용 인증과 권한 부여 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="57531-104">Authentication and Authorization for SignalR Persistent Connections (SignalR 1.x)</span></span>
====================
<span data-ttu-id="57531-105">하 여 [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="57531-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="57531-106">이 항목에서는 영구 연결에 권한 부여를 적용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="57531-107">SignalR 응용 프로그램에 보안을 통합 하는 방법에 대 한 일반적인 정보를 참조 하세요 [보안 소개](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-107">For general information about integrating security into a SignalR application, see [Introduction to Security](index.md).</span></span>


## <a name="enforce-authorization"></a><span data-ttu-id="57531-108">권한 부여를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-108">Enforce authorization</span></span>

<span data-ttu-id="57531-109">사용 하는 경우 권한 부여 규칙을 적용 하는 [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) 재정의 해야 합니다는 `AuthorizeRequest` 메서드.</span><span class="sxs-lookup"><span data-stu-id="57531-109">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="57531-110">사용할 수 없습니다는 `Authorize` 영구 연결을 사용 하 여 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="57531-110">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="57531-111">`AuthorizeRequest` 사용자 요청된 작업을 수행할 권한이 있는지 확인 하는 모든 요청 전에 SignalR 프레임 워크에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57531-111">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="57531-112">`AuthorizeRequest` 응용 프로그램의 표준 인증 메커니즘을 통해 사용자를 인증 하는 대신; 메서드가 클라이언트에서 호출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57531-112">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="57531-113">아래 예제에서는 인증 된 사용자에 대 한 요청을 제한 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="57531-113">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="57531-114">AuthorizeRequest 메서드;에서 모든 사용자 지정된 권한 부여 논리를 추가할 수 있습니다. 와 같은 사용자 특정 역할에 속하는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="57531-114">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>
