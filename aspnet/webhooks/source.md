---
uid: webhooks/source
title: "ASP.NET Webhook 소스 코드와 NuGet 패키지가 | Microsoft Docs"
author: rick-anderson
description: "ASP.NET Webhook 소스 코드와 NuGet 패키지에 대 한 링크"
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/17/2012
ms.topic: article
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.technology: 
ms.prod: .net-framework
ms.openlocfilehash: ab5eaaa32a8f678b2aa4e2a0b30b674dbd6d6e9c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a>ASP.NET Webhook 소스 코드와 NuGet 패키지

Microsoft ASP.NET Webhook 모듈의 Microsoft ASP.NET 제품군의 일부 이며으로 호스트 되는 [GitHub의 소스 프로젝트 열기](https://github.com/aspnet/WebHooks)합니다. 즉, 기여한 내용을 수락 म 있지만 살펴본는 [기여 지침](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) 끌어오기 요청을 제출 하기 전에.

이 온라인 설명서를 읽고 있는 이제도으로 호스트 [GitHub의 오픈 소스](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) 하 고 또한 기여를 허용 합니다.

## <a name="nuget-packages"></a>Nuget 패키지

Microsoft ASP.NET Webhook을 보려면 Visual Studio에서 미리 보기 플래그를 선택 해야 한다는 의미는 Nuget 패키지를 미리 볼 때 사용할 수도 있습니다.

[Nuget 패키지](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) 세 부분으로 devided:

* [일반적인](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): 발신자와 수신자 간에 공유 되는 일반적인 패키지 합니다.

* [보낸 사람](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): 다른 사용자에 게 고유한 Webhook을 보내는 지 원하는 패키지 집합이 있습니다. Webhook을 보내기 위한 기능은에 보다 자세히 설명 되어 [보내는 Webhook](sending/index.md)합니다.

* [수신기](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): Webhook을 다른 사용자 로부터 수신 지원 패키지 집합이 있습니다. Webhook을 수신 하기 위한 기능에서 더 자세하게에서 설명 [받는 Webhook](receiving/index.md)합니다.
