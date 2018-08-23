---
uid: webhooks/receiving/dependencies
title: ASP.NET 웹 후크 수신기 종속성 | Microsoft Docs
author: rick-anderson
description: 수신기 종속성 및 ASP.NET Webhook의 종속성 주입 합니다.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: c44cfe3ed310aa728a989b108c410e8786e4f514
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833309"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a>ASP.NET 웹 후크 수신기 종속성

Microsoft ASP.NET 웹 후크는 염두에서 종속성 주입을 사용 하 여 설계 되었습니다. 대부분의 종속성 시스템에서 종속성 주입 엔진을 사용 하는 대체 구현으로 바꿀 수 있습니다.

참조 하세요 [DependencyScopeExtensions](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) 수신기 종속성 목록은 합니다. 종속성 없이 등록 하는 경우에 기본 구현을 사용 됩니다. 참조 하세요 [ReceiverServices](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) 목록은 기본 구현입니다.
