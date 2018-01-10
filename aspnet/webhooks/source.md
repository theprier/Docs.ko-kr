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
ms.openlocfilehash: 733a0839c77bcfc96214bdf235ce8fe22ee2d3cf
ms.sourcegitcommit: 2d23ea501e0213bbacf65298acf1c8bd17209540
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a><span data-ttu-id="80bf6-103">ASP.NET Webhook 소스 코드와 NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="80bf6-103">ASP.NET WebHooks source code and NuGet packages</span></span>

<span data-ttu-id="80bf6-104">Microsoft ASP.NET Webhook 모듈의 Microsoft ASP.NET 제품군의 일부 이며으로 호스트 되는 [GitHub의 소스 프로젝트 열기](https://github.com/aspnet/WebHooks)합니다.</span><span class="sxs-lookup"><span data-stu-id="80bf6-104">Microsoft ASP.NET WebHooks is part of the Microsoft ASP.NET family of modules and is hosted as an [Open Source Project on GitHub](https://github.com/aspnet/WebHooks).</span></span> <span data-ttu-id="80bf6-105">즉, 기여한 내용을 수락 म 있지만 살펴본는 [기여 지침](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) 끌어오기 요청을 제출 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="80bf6-105">This means that we accept contributions, but please look at the [Contribution Guidelines](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) before submitting a pull request.</span></span>

<span data-ttu-id="80bf6-106">이 온라인 설명서를 읽고 있는 이제도으로 호스트 [GitHub의 오픈 소스](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) 하 고 또한 기여를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="80bf6-106">This online documentation which you are reading now is also hosted as [Open Source on GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) and also accepts contributions.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="80bf6-107">NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="80bf6-107">NuGet packages</span></span>

<span data-ttu-id="80bf6-108">[NuGet 패키지](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) 세 부분으로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="80bf6-108">The [NuGet packages](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) are divided into three parts:</span></span>

* <span data-ttu-id="80bf6-109">[일반적인](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): 발신자와 수신자 간에 공유 되는 일반적인 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="80bf6-109">[Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): A common package that is shared between senders and receivers.</span></span>

* <span data-ttu-id="80bf6-110">[보낸 사람](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): 다른 사용자에 게 고유한 Webhook을 보내는 지 원하는 패키지 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80bf6-110">[Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): A set of packages supporting sending your own WebHooks to others.</span></span> <span data-ttu-id="80bf6-111">Webhook을 보내기 위한 기능은에 보다 자세히 설명 되어 [보내는 Webhook](sending/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="80bf6-111">The functionality for sending WebHooks is described in more detail in [Sending WebHooks](sending/index.md).</span></span>

* <span data-ttu-id="80bf6-112">[수신기](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): Webhook을 다른 사용자 로부터 수신 지원 패키지 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80bf6-112">[Receivers](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): A set of packages supporting receiving WebHooks from others.</span></span> <span data-ttu-id="80bf6-113">Webhook을 수신 하기 위한 기능에서 더 자세하게에서 설명 [받는 Webhook](receiving/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="80bf6-113">The functionality for receiving WebHooks is described in more detail in [Receiving WebHooks](receiving/index.md).</span></span>
