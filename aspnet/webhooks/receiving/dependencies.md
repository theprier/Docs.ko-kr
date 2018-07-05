---
uid: webhooks/receiving/dependencies
title: ASP.NET 웹 후크 수신기 종속성 | Microsoft Docs
author: rick-anderson
description: 수신기 종속성 및 ASP.NET Webhook의 종속성 주입 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/17/2012
ms.topic: article
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.technology: ''
ms.openlocfilehash: cf45e3d2e45e4b7882b42d9aa0931e18c08f76b5
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37401188"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a><span data-ttu-id="4df61-103">ASP.NET 웹 후크 수신기 종속성</span><span class="sxs-lookup"><span data-stu-id="4df61-103">ASP.NET WebHooks receiver dependencies</span></span>

<span data-ttu-id="4df61-104">Microsoft ASP.NET 웹 후크는 염두에서 종속성 주입을 사용 하 여 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4df61-104">Microsoft ASP.NET WebHooks is designed with dependency injection in mind.</span></span> <span data-ttu-id="4df61-105">대부분의 종속성 시스템에서 종속성 주입 엔진을 사용 하는 대체 구현으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4df61-105">Most dependencies in the system can be replaced with alternative implementations using a dependency injection engine.</span></span>

<span data-ttu-id="4df61-106">참조 하세요 [DependencyScopeExtensions](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) 수신기 종속성 목록은 합니다.</span><span class="sxs-lookup"><span data-stu-id="4df61-106">Please see [DependencyScopeExtensions](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) for a list of receiver dependencies.</span></span> <span data-ttu-id="4df61-107">종속성 없이 등록 하는 경우에 기본 구현을 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4df61-107">If no dependency has been registered, a default implementation is used.</span></span> <span data-ttu-id="4df61-108">참조 하세요 [ReceiverServices](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) 목록은 기본 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="4df61-108">Please see [ReceiverServices](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) for a list of default implementations.</span></span>
