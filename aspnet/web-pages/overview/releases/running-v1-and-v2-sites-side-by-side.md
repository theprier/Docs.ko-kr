---
uid: web-pages/overview/releases/running-v1-and-v2-sites-side-by-side
title: 다른 버전의 ASP.NET 웹 페이지 (Razor) Side-by-side 실행 | Microsoft Docs
author: tfitzmac
description: 이 문서에서는 웹 사이트는 서로 다른 버전을 사용 하도록 구성 된 경우 동일한 컴퓨터 또는 서버에서 ASP.NET Web Pages (Razor) 웹 사이트를 실행 하는 방법에 설명 하는 중...
ms.author: riande
ms.date: 02/10/2014
ms.assetid: a861409b-4ae6-4868-9e09-87edfac3535f
msc.legacyurl: /web-pages/overview/releases/running-v1-and-v2-sites-side-by-side
msc.type: authoredcontent
ms.openlocfilehash: 9021f9b7a68b8b20f7f2fbcd5649cc7226401a1b
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834743"
---
<a name="running-different-versions-of-aspnet-web-pages-razor-side-by-side"></a><span data-ttu-id="4951e-103">ASP.NET 웹 페이지 (Razor)의 다른 버전을 나란히 실행</span><span class="sxs-lookup"><span data-stu-id="4951e-103">Running Different Versions of ASP.NET Web Pages (Razor) Side by Side</span></span>
====================
<span data-ttu-id="4951e-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="4951e-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="4951e-105">이 문서에서는 웹 사이트는 서로 다른 버전의 ASP.NET 웹 페이지를 사용 하도록 구성 된 경우 동일한 컴퓨터 또는 서버에서 ASP.NET Web Pages (Razor) 웹 사이트를 실행 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4951e-105">This article explains how to run ASP.NET Web Pages (Razor) websites on the same computer or server when the websites are configured to use different versions of ASP.NET Web Pages.</span></span>
> 
> <span data-ttu-id="4951e-106">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="4951e-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="4951e-107">기본 동작 이란 ASP.NET에서 ASP.NET 웹 페이지를 사용 하 여 구축 된 사이트에 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="4951e-107">What the default behavior is in ASP.NET when you have sites built with ASP.NET Web Pages.</span></span>
> - <span data-ttu-id="4951e-108">이전 버전의 ASP.NET 웹 페이지를 사용 하 여 실행 하려면 새 사이트를 구성 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="4951e-108">How to configure a new site to run with an older version of ASP.NET Web Pages.</span></span>
>   
> 
> <span data-ttu-id="4951e-109">문서에 도입 된 ASP.NET 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4951e-109">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="4951e-110">`webPages:Version` 구성 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="4951e-110">The `webPages:Version` configuration setting.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="4951e-111">소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="4951e-111">Software versions</span></span>
> 
> 
> - <span data-ttu-id="4951e-112">ASP.NET Web Pages (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="4951e-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="4951e-113">이 자습서는 또한 ASP.NET 웹 페이지 2 및 ASP.NET 웹 페이지 1.0과 함께 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="4951e-113">This tutorial also works with ASP.NET Web Pages 2 and ASP.NET Web Pages 1.0.</span></span>


<span data-ttu-id="4951e-114">ASP.NET 웹 페이지를 함께 웹 사이트를 실행 하는 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4951e-114">ASP.NET Web Pages supports the ability to run websites side by side.</span></span> <span data-ttu-id="4951e-115">이렇게 하면 계속 이전 ASP.NET Web Pages 응용 프로그램을 실행, 새 ASP.NET 웹 페이지 응용 프로그램을 빌드 및 모두 동일한 컴퓨터에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4951e-115">This lets you continue to run your older ASP.NET Web Pages applications, build new ASP.NET Web Pages applications, and run all of them on the same computer.</span></span>

<span data-ttu-id="4951e-116">WebMatrix를 사용 하 여 웹 페이지를 설치할 때 기억해 야 할 몇 가지 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4951e-116">Here are some things to remember when you install the Web Pages with WebMatrix:</span></span>

- <span data-ttu-id="4951e-117">기본적으로 기존 웹 페이지 응용 프로그램은 컴퓨터에 최신 버전으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4951e-117">By default, existing Web Pages applications will run as the latest version on your computer.</span></span> <span data-ttu-id="4951e-118">(어셈블리가 전역 어셈블리 캐시 (GAC)에 설치 되 고 자동으로 사용 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="4951e-118">(The assemblies are installed in the global assembly cache (GAC) and are used automatically.)</span></span>
- <span data-ttu-id="4951e-119">다른 버전의 ASP.NET 웹 페이지를 사용 하 여 사이트를 실행 하려는 경우에 작업을 수행 하는 사이트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4951e-119">If you want to run a site using a different version of ASP.NET Web Pages, you can configure the site to do that.</span></span> <span data-ttu-id="4951e-120">사이트에 아직 없는 경우는 *web.config* 사이트의 루트에 파일, 새로 만들고, 기존 콘텐츠를 덮어씁니다를 다음 XML을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="4951e-120">If your site doesn't already have a *web.config* file in the root of the site, create a new one and copy the following XML into it, overwriting the existing content.</span></span> <span data-ttu-id="4951e-121">해당 사이트에 이미 포함 하는 경우는 *web.config* 파일을 추가 `<appSettings>` 에 다음과 같은 요소는 `<configuration>` 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="4951e-121">If the site already contains a *web.config* file, add an `<appSettings>` element like the following one to the `<configuration>` section.</span></span>

    [!code-xml[Main](running-v1-and-v2-sites-side-by-side/samples/sample1.xml)]
  <span data-ttu-id="4951e-122">'-의 버전을 지정 하지 않으면 경우는 *web.config* 사이트 파일은 최신 버전으로 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4951e-122">\`- If you do not specify a version in the *web.config* file, a site is deployed as the latest version.</span></span> <span data-ttu-id="4951e-123">(어셈블리 복사 되는 *bin* 배포 된 사이트의 폴더입니다.)</span><span class="sxs-lookup"><span data-stu-id="4951e-123">(The assemblies are copied to the *bin* folder in the deployed site.)</span></span>
- <span data-ttu-id="4951e-124">사이트의 웹 페이지 버전 어셈블리를 포함 하는 Web Matrix에서 사이트 템플릿을 사용 하 여 만드는 새 응용 프로그램 *bin* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4951e-124">New applications that you create using the site templates in Web Matrix include the Web Pages version assemblies in the site's *bin* folder.</span></span>

<span data-ttu-id="4951e-125">일반적으로 제어할 수 있습니다. 항상 웹 페이지 사이트에 적절 한 어셈블리를 설치 하려면 NuGet을 사용 하 여 사이트를 사용 하는 버전 *bin* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4951e-125">In general, you can always control which version of Web Pages to use with your site by using NuGet to install the appropriate assemblies into the site's *bin* folder.</span></span> <span data-ttu-id="4951e-126">패키지를 방문 [NuGet.org](http://NuGet.org)합니다.</span><span class="sxs-lookup"><span data-stu-id="4951e-126">To find packages, visit [NuGet.org](http://NuGet.org).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4951e-127">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="4951e-127">Additional Resources</span></span>

[<span data-ttu-id="4951e-128">ASP.NET 웹 페이지 2의에서 주요 기능</span><span class="sxs-lookup"><span data-stu-id="4951e-128">The Top Features in ASP.NET Web Pages 2</span></span>](top-features-in-web-pages-2.md)
