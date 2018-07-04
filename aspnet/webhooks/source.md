---
uid: webhooks/source
title: ASP.NET 웹 후크 소스 코드와 NuGet 패키지 | Microsoft Docs
author: rick-anderson
description: ASP.NET 웹 후크 소스 코드와 NuGet 패키지에 대 한 링크
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/17/2012
ms.topic: article
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.technology: ''
ms.openlocfilehash: 49a6d3e92e8d6365bea6594a616922aff9d0b4ac
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37375851"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a><span data-ttu-id="e5478-103">ASP.NET 웹 후크 소스 코드와 NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="e5478-103">ASP.NET WebHooks source code and NuGet packages</span></span>

<span data-ttu-id="e5478-104">Microsoft ASP.NET 웹 후크 모듈의 Microsoft ASP.NET 제품군의 일부 이며로 호스트 되는 [GitHub에서 오픈 소스 프로젝트](https://github.com/aspnet/WebHooks)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5478-104">Microsoft ASP.NET WebHooks is part of the Microsoft ASP.NET family of modules and is hosted as an [Open Source Project on GitHub](https://github.com/aspnet/WebHooks).</span></span> <span data-ttu-id="e5478-105">즉, 참여를 허용 하지만 살펴보세요 해 합니다 [기여 지침](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) 끌어오기 요청을 제출 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5478-105">This means that we accept contributions, but please look at the [Contribution Guidelines](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) before submitting a pull request.</span></span>

<span data-ttu-id="e5478-106">이 온라인 설명서를 읽어 나갈는 이제는 또한으로 호스팅됩니다 [GitHub에서 오픈 소스](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) 도 기여를 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5478-106">This online documentation which you are reading now is also hosted as [Open Source on GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) and also accepts contributions.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="e5478-107">NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="e5478-107">NuGet packages</span></span>

<span data-ttu-id="e5478-108">합니다 [NuGet 패키지](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) 세 부분으로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="e5478-108">The [NuGet packages](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) are divided into three parts:</span></span>

* <span data-ttu-id="e5478-109">[일반적인](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): 발신자와 수신자 간에 공유 되는 일반적인 패키지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5478-109">[Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): A common package that is shared between senders and receivers.</span></span>

* <span data-ttu-id="e5478-110">[보낸 사람](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): 고유한 웹 후크를 다른 보내기 지원 패키지 집합이.</span><span class="sxs-lookup"><span data-stu-id="e5478-110">[Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): A set of packages supporting sending your own WebHooks to others.</span></span> <span data-ttu-id="e5478-111">웹 후크를 보내는 기능에서 더 자세히 설명 되어 [웹 후크에 보낼](sending/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5478-111">The functionality for sending WebHooks is described in more detail in [Sending WebHooks](sending/index.md).</span></span>

* <span data-ttu-id="e5478-112">[수신기](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): 다른 사용자의 웹 후크를 받는 지원 패키지 집합이.</span><span class="sxs-lookup"><span data-stu-id="e5478-112">[Receivers](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): A set of packages supporting receiving WebHooks from others.</span></span> <span data-ttu-id="e5478-113">웹 후크를 수신 하기 위한 기능에서 더 자세히 설명 되어 [수신 웹 후크](receiving/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5478-113">The functionality for receiving WebHooks is described in more detail in [Receiving WebHooks](receiving/index.md).</span></span>
