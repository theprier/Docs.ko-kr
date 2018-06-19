---
uid: webhooks/receiving/dependencies
title: ASP.NET Webhook 수신기 종속성 | Microsoft Docs
author: rick-anderson
description: 수신기 종속성 및 ASP.NET Webhook의 종속성 주입 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/17/2012
ms.topic: article
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.technology: ''
ms.prod: .net-framework
ms.openlocfilehash: f9726c746c8934594e26f2871f9b867c192374bb
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
ms.locfileid: "26529912"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a>ASP.NET Webhook 수신기 종속성

Microsoft ASP.NET Webhook은 염두에서 종속성 주입 설계 되었습니다. 시스템에 종속성이 대부분 종속성 주입 엔진을 사용 하 여 대체 구현을 바꿀 수 있습니다.

참조 하십시오 [DependencyScopeExtensions](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) 수신기 종속성 목록에 대 한 합니다. 의존 하지 않고에 등록 된 경우에 기본 구현이 사용 됩니다. 참조 하십시오 [ReceiverServices](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) 목록은 기본 구현입니다.
