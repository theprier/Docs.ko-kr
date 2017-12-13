---
uid: webhooks/receiving/dependencies
title: "ASP.NET Webhook 수신기 종속성 | Microsoft Docs"
author: rick-anderson
description: "수신기 종속성 및 ASP.NET Webhook의 종속성 주입 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/17/2012
ms.topic: article
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.technology: 
ms.prod: .net-framework
ms.openlocfilehash: f9726c746c8934594e26f2871f9b867c192374bb
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
# <a name="aspnet-webhooks-receiver-dependencies"></a><span data-ttu-id="e42c5-103">ASP.NET Webhook 수신기 종속성</span><span class="sxs-lookup"><span data-stu-id="e42c5-103">ASP.NET WebHooks receiver dependencies</span></span>

<span data-ttu-id="e42c5-104">Microsoft ASP.NET Webhook은 염두에서 종속성 주입 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c5-104">Microsoft ASP.NET WebHooks is designed with dependency injection in mind.</span></span> <span data-ttu-id="e42c5-105">시스템에 종속성이 대부분 종속성 주입 엔진을 사용 하 여 대체 구현을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e42c5-105">Most dependencies in the system can be replaced with alternative implementations using a dependency injection engine.</span></span>

<span data-ttu-id="e42c5-106">참조 하십시오 [DependencyScopeExtensions](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) 수신기 종속성 목록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e42c5-106">Please see [DependencyScopeExtensions](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) for a list of receiver dependencies.</span></span> <span data-ttu-id="e42c5-107">의존 하지 않고에 등록 된 경우에 기본 구현이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e42c5-107">If no dependency has been registered, a default implementation is used.</span></span> <span data-ttu-id="e42c5-108">참조 하십시오 [ReceiverServices](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) 목록은 기본 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="e42c5-108">Please see [ReceiverServices](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) for a list of default implementations.</span></span>
