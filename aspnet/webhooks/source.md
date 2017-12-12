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
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a><span data-ttu-id="b0405-103">ASP.NET Webhook 소스 코드와 NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="b0405-103">ASP.NET WebHooks source code and NuGet packages</span></span>

<span data-ttu-id="b0405-104">Microsoft ASP.NET Webhook 모듈의 Microsoft ASP.NET 제품군의 일부 이며으로 호스트 되는 [GitHub의 소스 프로젝트 열기](https://github.com/aspnet/WebHooks)합니다.</span><span class="sxs-lookup"><span data-stu-id="b0405-104">Microsoft ASP.NET WebHooks is part of the Microsoft ASP.NET family of modules and is hosted as an [Open Source Project on GitHub](https://github.com/aspnet/WebHooks).</span></span> <span data-ttu-id="b0405-105">즉, 기여한 내용을 수락 म 있지만 살펴본는 [기여 지침](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) 끌어오기 요청을 제출 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="b0405-105">This means that we accept contributions, but please look at the [Contribution Guidelines](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) before submitting a pull request.</span></span>

<span data-ttu-id="b0405-106">이 온라인 설명서를 읽고 있는 이제도으로 호스트 [GitHub의 오픈 소스](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) 하 고 또한 기여를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0405-106">This online documentation which you are reading now is also hosted as [Open Source on GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) and also accepts contributions.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="b0405-107">Nuget 패키지</span><span class="sxs-lookup"><span data-stu-id="b0405-107">Nuget Packages</span></span>

<span data-ttu-id="b0405-108">Microsoft ASP.NET Webhook을 보려면 Visual Studio에서 미리 보기 플래그를 선택 해야 한다는 의미는 Nuget 패키지를 미리 볼 때 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0405-108">Microsoft ASP.NET WebHooks is also available as preview Nuget packages which means that you have to select the Preview flag in Visual Studio in order to see them.</span></span>

<span data-ttu-id="b0405-109">[Nuget 패키지](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) 세 부분으로 devided:</span><span class="sxs-lookup"><span data-stu-id="b0405-109">The [Nuget packages](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) are devided into three parts:</span></span>

* <span data-ttu-id="b0405-110">[일반적인](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): 발신자와 수신자 간에 공유 되는 일반적인 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0405-110">[Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): A common package that is shared between senders and receivers.</span></span>

* <span data-ttu-id="b0405-111">[보낸 사람](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): 다른 사용자에 게 고유한 Webhook을 보내는 지 원하는 패키지 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0405-111">[Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): A set of packages supporting sending your own WebHooks to others.</span></span> <span data-ttu-id="b0405-112">Webhook을 보내기 위한 기능은에 보다 자세히 설명 되어 [보내는 Webhook](sending/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b0405-112">The functionality for sending WebHooks is described in more detail in [Sending WebHooks](sending/index.md).</span></span>

* <span data-ttu-id="b0405-113">[수신기](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): Webhook을 다른 사용자 로부터 수신 지원 패키지 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0405-113">[Receivers](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): A set of packages supporting receiving WebHooks from others.</span></span> <span data-ttu-id="b0405-114">Webhook을 수신 하기 위한 기능에서 더 자세하게에서 설명 [받는 Webhook](receiving/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b0405-114">The functionality for receiving WebHooks is described in more detail in [Receiving WebHooks](receiving/index.md).</span></span>
