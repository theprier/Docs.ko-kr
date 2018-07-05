---
uid: webhooks/receiving/dependencies
title: ASP.NET 웹 후크 수신기 종속성 | Microsoft Docs
author: rick-anderson
description: 수신기 종속성 및 ASP.NET Webhook의 종속성 주입 합니다.
ms.author: aspnetcontent
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: 05dcfac121e7974fd83c5b3736616479574944a1
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37817839"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a>ASP.NET 웹 후크 수신기 종속성

Microsoft ASP.NET 웹 후크는 염두에서 종속성 주입을 사용 하 여 설계 되었습니다. 대부분의 종속성 시스템에서 종속성 주입 엔진을 사용 하는 대체 구현으로 바꿀 수 있습니다.

참조 하세요 [DependencyScopeExtensions](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) 수신기 종속성 목록은 합니다. 종속성 없이 등록 하는 경우에 기본 구현을 사용 됩니다. 참조 하세요 [ReceiverServices](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) 목록은 기본 구현입니다.
