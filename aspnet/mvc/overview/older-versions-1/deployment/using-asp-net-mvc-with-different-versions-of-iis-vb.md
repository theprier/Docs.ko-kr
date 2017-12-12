---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
title: "ASP.NET MVC를 사용 하 여 서로 다른 버전의 IIS (VB) | Microsoft Docs"
author: microsoft
description: "이 자습서에서는 여러 가지 버전의 인터넷 정보 서비스 URL 라우팅 및 ASP.NET MVC를 사용 하는 방법에 설명 합니다. 배웁니다 다른 전략 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/19/2008
ms.topic: article
ms.assetid: 1c1283b2-6956-4937-b568-d30de432ce23
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-vb
msc.type: authoredcontent
ms.openlocfilehash: 57a729501d15ebf9a533716b2a1767766954bb4c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="using-aspnet-mvc-with-different-versions-of-iis-vb"></a><span data-ttu-id="58145-104">ASP.NET MVC를 사용 하 여 서로 다른 버전의 IIS (VB)</span><span class="sxs-lookup"><span data-stu-id="58145-104">Using ASP.NET MVC with Different Versions of IIS (VB)</span></span>
====================
<span data-ttu-id="58145-105">여 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="58145-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="58145-106">이 자습서에서는 여러 가지 버전의 인터넷 정보 서비스 URL 라우팅 및 ASP.NET MVC를 사용 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-106">In this tutorial, you learn how to use ASP.NET MVC, and URL Routing, with different versions of Internet Information Services.</span></span> <span data-ttu-id="58145-107">ASP.NET MVC를 사용 하 여 IIS 7.0 (기본 모드), IIS 6.0 및 이전 버전의 IIS에 대 한 여러 전략 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="58145-107">You learn different strategies for using ASP.NET MVC with IIS 7.0 (classic mode), IIS 6.0, and earlier versions of IIS.</span></span>


<span data-ttu-id="58145-108">ASP.NET MVC 프레임 워크 경로 브라우저 요청 컨트롤러 작업을 ASP.NET 라우팅에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="58145-108">The ASP.NET MVC framework depends on ASP.NET Routing to route browser requests to controller actions.</span></span> <span data-ttu-id="58145-109">ASP.NET 라우팅에서 활용 하려면 웹 서버에서 추가 구성 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-109">In order to take advantage of ASP.NET Routing, you might have to perform additional configuration steps on your web server.</span></span> <span data-ttu-id="58145-110">모든 버전의 인터넷 정보 서비스 (IIS) 및 처리 모드 응용 프로그램에 대 한 요청에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="58145-110">It all depends on the version of Internet Information Services (IIS) and the request processing mode for your application.</span></span>

<span data-ttu-id="58145-111">다음은 서로 다른 버전의 IIS에 대 한 요약이입니다.</span><span class="sxs-lookup"><span data-stu-id="58145-111">Here's a summary of the different versions of IIS:</span></span>

- <span data-ttu-id="58145-112">IIS 7.0 (통합된 모드)-ASP.NET 라우팅을 사용 하는 데 필요한 특별 한 구성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-112">IIS 7.0 (integrated mode) - No special configuration necessary to use ASP.NET Routing.</span></span>
- <span data-ttu-id="58145-113">IIS 7.0 (기본 모드)-ASP.NET 라우팅을 사용 하려면 특별 한 구성이 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-113">IIS 7.0 (classic mode) - You need to perform special configuration to use ASP.NET Routing.</span></span>
- <span data-ttu-id="58145-114">IIS 6.0 또는 아래-ASP.NET 라우팅을 사용 하려면 특별 한 구성 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-114">IIS 6.0 or below - You need to perform special configuration to use ASP.NET Routing.</span></span>

<span data-ttu-id="58145-115">최신 버전의 IIS 버전 7.5 (Win7)에 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-115">The latest version of IIS is version 7.5 (on Win7).</span></span> <span data-ttu-id="58145-116">IIS의 IIS 7 이상 포함 된 Windows Server 2008 AND VISTA/s p 1은 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-116">IIS 7 of IIS is included with Windows Server 2008 AND VISTA/SP1 and higher.</span></span> <span data-ttu-id="58145-117">또한 Home Basic 제외 하 고 Vista 운영 체제의 모든 버전에 IIS 7.0를 설치할 수 있습니다 (참조 [https://technet.microsoft.com/en-us/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/en-us/library/cc731179%28WS.10%29.aspx)).</span><span class="sxs-lookup"><span data-stu-id="58145-117">You also can install IIS 7.0 on any version of the Vista operating system except Home Basic (see [https://technet.microsoft.com/en-us/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/en-us/library/cc731179%28WS.10%29.aspx)).</span></span>

<span data-ttu-id="58145-118">IIS 7.0 요청 처리를 위한 두 가지 모드를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-118">IIS 7.0 supports two modes for processing requests.</span></span> <span data-ttu-id="58145-119">통합된 모드 또는 클래식 모드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-119">You can use integrated mode or classic mode.</span></span> <span data-ttu-id="58145-120">통합된 모드의 IIS 7.0을 사용 하는 경우 특수 구성 단계를 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-120">You don't need to perform any special configuration steps when using IIS 7.0 in integrated mode.</span></span> <span data-ttu-id="58145-121">클래식 모드에서 IIS 7.0을 사용 하는 경우 추가 구성을 수행할 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-121">However, you do need to perform additional configuration when using IIS 7.0 in classic mode.</span></span>

<span data-ttu-id="58145-122">Microsoft Windows Server 2003에 IIS 6.0에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58145-122">Microsoft Windows Server 2003 includes IIS 6.0.</span></span> <span data-ttu-id="58145-123">Windows Server 2003 운영 체제를 사용 하는 경우 IIS 7.0으로 IIS 6.0을 업그레이드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-123">You cannot upgrade IIS 6.0 to IIS 7.0 when using the Windows Server 2003 operating system.</span></span> <span data-ttu-id="58145-124">IIS 6.0을 사용 하는 경우에 추가 구성 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-124">You must perform additional configuration steps when using IIS 6.0.</span></span>

<span data-ttu-id="58145-125">Microsoft Windows XP Professional IIS 5.1을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-125">Microsoft Windows XP Professional includes IIS 5.1.</span></span> <span data-ttu-id="58145-126">IIS 5.1을 사용 하는 경우에 추가 구성 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-126">You must perform additional configuration steps when using IIS 5.1.</span></span>

<span data-ttu-id="58145-127">마지막으로, Microsoft Windows 2000 및 Microsoft Windows 2000 Professional IIS 5.0에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58145-127">Finally, Microsoft Windows 2000 and Microsoft Windows 2000 Professional includes IIS 5.0.</span></span> <span data-ttu-id="58145-128">IIS 5.0을 사용 하는 경우에 추가 구성 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-128">You must perform additional configuration steps when using IIS 5.0.</span></span>

## <a name="integrated-versus-classic-mode"></a><span data-ttu-id="58145-129">클래식 모드와 통합</span><span class="sxs-lookup"><span data-stu-id="58145-129">Integrated versus Classic Mode</span></span>

<span data-ttu-id="58145-130">IIS 7.0 두 가지 다른 요청 처리 모드를 사용 하 여 요청을 처리할 수 있습니다: 클래식 고 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-130">IIS 7.0 can process requests using two different request processing modes: integrated and classic.</span></span> <span data-ttu-id="58145-131">통합된 모드는 더 나은 성능과 더 많은 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-131">Integrated mode provides better performance and more features.</span></span> <span data-ttu-id="58145-132">클래식 모드에 대 한 이전 버전과 포함 된 이전 버전의 IIS와의 호환성.</span><span class="sxs-lookup"><span data-stu-id="58145-132">Classic mode is included for backwards compatibility with earlier versions of IIS.</span></span>

<span data-ttu-id="58145-133">요청 처리 모드는 응용 프로그램 풀에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58145-133">The request processing mode is determined by the application pool.</span></span> <span data-ttu-id="58145-134">응용 프로그램과 관련 된 응용 프로그램 풀을 확인 하 여 어떤 처리 모드가 특정 웹 응용 프로그램에서 사용 되 고 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-134">You can determine which processing mode is being used by a particular web application by determining the application pool associated with the application.</span></span> <span data-ttu-id="58145-135">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-135">Follow these steps:</span></span>

1. <span data-ttu-id="58145-136">인터넷 정보 서비스 관리자를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-136">Launch the Internet Information Services Manager</span></span>
2. <span data-ttu-id="58145-137">연결 창에서 응용 프로그램 선택</span><span class="sxs-lookup"><span data-stu-id="58145-137">In the Connections window, select an application</span></span>
3. <span data-ttu-id="58145-138">작업 창에서 클릭 된 **기본 설정** 응용 프로그램 편집 대화 상자를 열려면 링크 상자 (그림 1 참조)</span><span class="sxs-lookup"><span data-stu-id="58145-138">In the Actions window, click the **Basic Settings** link to open the Edit Application dialog box (see Figure 1)</span></span>
4. <span data-ttu-id="58145-139">선택한 응용 프로그램 풀을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="58145-139">Take note of the Application pool selected.</span></span>

<span data-ttu-id="58145-140">기본적으로 IIS가 두 개의 응용 프로그램 풀을 지원 하도록 구성: **DefaultAppPool** 및 **클래식.NET AppPool**합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-140">By default, IIS is configured to support two application pools: **DefaultAppPool** and **Classic .NET AppPool**.</span></span> <span data-ttu-id="58145-141">DefaultAppPool을 선택 하면 응용 프로그램 통합된 요청 처리 모드에서 실행 중인 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-141">If DefaultAppPool is selected, then your application is running in integrated request processing mode.</span></span> <span data-ttu-id="58145-142">클래식.NET AppPool을 선택 하면 응용 프로그램은 클래식 요청 처리 모드에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58145-142">If Classic .NET AppPool is selected, your application is running in classic request processing mode.</span></span>


<span data-ttu-id="58145-143">[![새 프로젝트 대화 상자](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="58145-143">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image1.png)</span></span>

<span data-ttu-id="58145-144">**그림 1**: 검색 요청 처리 모드 ([전체 크기 이미지를 보려면 클릭](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="58145-144">**Figure 1**: Detecting the request processing mode([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.png))</span></span>


<span data-ttu-id="58145-145">응용 프로그램 편집 대화 상자 내에서 요청 처리 모드를 수정할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-145">Notice that you can modify the request processing mode within the Edit Application dialog box.</span></span> <span data-ttu-id="58145-146">선택 단추를 클릭 하 고 응용 프로그램과 관련 응용 프로그램 풀을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-146">Click the Select button and change the application pool associated with the application.</span></span> <span data-ttu-id="58145-147">통합된 모드를 클래식에서 ASP.NET 응용 프로그램을 변경 하는 경우 호환성 문제가 지 실현 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-147">Realize that there are compatibility issues when changing an ASP.NET application from classic to integrated mode.</span></span> <span data-ttu-id="58145-148">자세한 내용은 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58145-148">For more information, see the following articles:</span></span>

- <span data-ttu-id="58145-149">Windows Vista 및 Windows Server 2008-IIS 7.0으로 업그레이드 하는 ASP.NET 1.1 [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)</span><span class="sxs-lookup"><span data-stu-id="58145-149">Upgrading ASP.NET 1.1 to IIS 7.0 on Windows Vista and Windows Server 2008 -- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)</span></span>

- <span data-ttu-id="58145-150">IIS 7.0-ASP.NET 통합 [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)</span><span class="sxs-lookup"><span data-stu-id="58145-150">ASP.NET Integration With IIS 7.0 - [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)</span></span>


<span data-ttu-id="58145-151">ASP.NET 응용 프로그램 하면 DefaultAppPool이를 사용 하는 경우 ASP.NET 라우팅에서 (및 따라서 ASP.NET MVC)에서 실행 되도록 추가 단계를 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-151">If an ASP.NET application is using the DefaultAppPool, then you don't need to perform any additional steps to get ASP.NET Routing (and therefore ASP.NET MVC) to work.</span></span> <span data-ttu-id="58145-152">그러나 ASP.NET 응용 프로그램은 클래식.NET AppPool을 사용 하 여 다음 계속 읽어 하도록 구성 된, 더 많은 작업을 수행 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-152">However, if the ASP.NET application is configured to use the Classic .NET AppPool then keep reading, you have more work to do.</span></span>

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a><span data-ttu-id="58145-153">이전 버전의 IIS와 ASP.NET MVC를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-153">Using ASP.NET MVC with Older Versions of IIS</span></span>

<span data-ttu-id="58145-154">IIS 7.0 이전 버전의 IIS와 ASP.NET MVC를 사용 해야 하거나 클래식 모드에서 IIS 7.0을 사용 하려면, 다음 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-154">If you need to use ASP.NET MVC with an older version of IIS than IIS 7.0, or you need to use IIS 7.0 in classic mode, then you have two options.</span></span> <span data-ttu-id="58145-155">첫째, 파일 확장명을 사용 하려면 경로 테이블을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-155">First, you can modify the route table to use file extensions.</span></span> <span data-ttu-id="58145-156">예를 들어 /Store/Details 같은 URL을 요청 하는 대신 /Store.aspx/Details 같은 URL을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-156">For example, instead of requesting a URL like /Store/Details, you would request a URL like /Store.aspx/Details.</span></span>

<span data-ttu-id="58145-157">두 번째 방법은 라는 항목을 만드는 한 *와일드 카드 스크립트 매핑*합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-157">The second option is to create something called a *wildcard script map*.</span></span> <span data-ttu-id="58145-158">와일드 카드 스크립트 매핑을 사용 하면 ASP.NET 프레임 워크에 대 한 모든 요청을 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-158">A wildcard script map enables you to map every request into the ASP.NET framework.</span></span>

<span data-ttu-id="58145-159">웹 서버 (예를 들어 응용 프로그램 인터넷 서비스 공급자에서 호스팅하는 ASP.NET MVC)에 대 한 사용 권한이 첫 번째 옵션을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-159">If you don't have access to your web server (for example, your ASP.NET MVC application is being hosted by an Internet Service Provider) then you'll need to use the first option.</span></span> <span data-ttu-id="58145-160">Url의 모양을 수정 하려면 웹 서버에 액세스할 수 있는 경우 두 번째 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-160">If you don't want to modify the appearance of your URLs, and you have access to your web server, then you can use the second option.</span></span>

<span data-ttu-id="58145-161">다음 섹션에서 자세히 각 옵션을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-161">We explore each option in detail in the following sections.</span></span>

## <a name="adding-extensions-to-the-route-table"></a><span data-ttu-id="58145-162">경로 테이블에 확장을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-162">Adding Extensions to the Route Table</span></span>

<span data-ttu-id="58145-163">이전 버전의 IIS 사용 하려면 ASP.NET 라우팅이 얻으려고 하는 가장 쉬운 방법은 Global.asax 파일에 경로 테이블을 수정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="58145-163">The easiest way to get ASP.NET Routing to work with older versions of IIS is to modify your route table in the Global.asax file.</span></span> <span data-ttu-id="58145-164">기본 목록 1의 수정 되지 않은 Global.asax 파일 기본 경로 라는 하나의 경로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-164">The default and unmodified Global.asax file in Listing 1 configures one route named the Default route.</span></span>

<span data-ttu-id="58145-165">**1-Global.asax (수정 되지 않은)를 나열 합니다.**</span><span class="sxs-lookup"><span data-stu-id="58145-165">**Listing 1 - Global.asax (unmodified)**</span></span>

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample1.vb)]

<span data-ttu-id="58145-166">목록 1에 구성 된 기본 경로 다음과 같은 경로 Url에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-166">The Default route configured in Listing 1 enables you to route URLs that look like this:</span></span>

<span data-ttu-id="58145-167">/ Home/Index</span><span class="sxs-lookup"><span data-stu-id="58145-167">/Home/Index</span></span>

<span data-ttu-id="58145-168">/ 제품/세부 정보/3</span><span class="sxs-lookup"><span data-stu-id="58145-168">/Product/Details/3</span></span>

<span data-ttu-id="58145-169">/ 제품</span><span class="sxs-lookup"><span data-stu-id="58145-169">/Product</span></span>

<span data-ttu-id="58145-170">그러나 이전 버전의 IIS는 ASP.NET 프레임 워크를 이러한 요청을 전달 하지 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-170">Unfortunately, older versions of IIS won't pass these requests to the ASP.NET framework.</span></span> <span data-ttu-id="58145-171">따라서 이러한 요청은 컨트롤러에 라우트되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-171">Therefore, these requests won't get routed to a controller.</span></span> <span data-ttu-id="58145-172">예를 들어 URL /Home/인덱스에 대 한 브라우저 요청을 수행 하는 경우 다음 얻게 됩니다 오류 페이지에는 그림 2.</span><span class="sxs-lookup"><span data-stu-id="58145-172">For example, if you make a browser request for the URL /Home/Index then you'll get the error page in Figure 2.</span></span>


<span data-ttu-id="58145-173">[![새 프로젝트 대화 상자](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="58145-173">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.png)</span></span>

<span data-ttu-id="58145-174">**그림 2**: 404 찾을 수 없음 오류를 받는다면 ([전체 크기 이미지를 보려면 클릭](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="58145-174">**Figure 2**: Receiving a 404 Not Found error([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.png))</span></span>


<span data-ttu-id="58145-175">이전 버전의 IIS는 ASP.NET framework에 대 한 특정 요청을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-175">Older versions of IIS only map certain requests to the ASP.NET framework.</span></span> <span data-ttu-id="58145-176">올바른 파일 확장명을 포함 하는 URL에 대 한 요청을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-176">The request must be for a URL with the right file extension.</span></span> <span data-ttu-id="58145-177">예를 들어 /SomePage.aspx에 대 한 요청이 ASP.NET 프레임 워크에 매핑됩니다 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="58145-177">For example, a request for /SomePage.aspx gets mapped to the ASP.NET framework.</span></span> <span data-ttu-id="58145-178">그러나 /SomePage.htm에 대 한 요청 준수 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-178">However, a request for /SomePage.htm does not.</span></span>

<span data-ttu-id="58145-179">따라서에서 실행 되도록 ASP.NET 라우팅이 얻으려고 했습니다 수정 해야 기본 경로 ASP.NET 프레임 워크에 매핑되는 파일 확장명이 포함 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-179">Therefore, to get ASP.NET Routing to work, we must modify the Default route so that it includes a file extension that is mapped to the ASP.NET framework.</span></span>

<span data-ttu-id="58145-180">이 작업은 수행 라는 스크립트를 사용 하 여 `registermvc.wsf`합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-180">This is done using a script named `registermvc.wsf`.</span></span> <span data-ttu-id="58145-181">에 ASP.NET MVC 1 릴리스에 포함 된 `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`, ASP.NET 2를 기준으로이 스크립트 이동에 사용할 수 있는 ASP.NET 미래에 [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978)합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-181">It was included with the ASP.NET MVC 1 release in `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`, but as of ASP.NET 2 this script has been moved to the ASP.NET Futures, available at [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978).</span></span>

<span data-ttu-id="58145-182">이 스크립트를 실행 하는 새.mvc 확장 IIS에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-182">Executing this script registers a new .mvc extension with IIS.</span></span> <span data-ttu-id="58145-183">.Mvc 확장명을 등록 하면.mvc 확장명을 사용 하는 경로 Global.asax 파일의 프로그램 경로 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-183">After you register the .mvc extension, you can modify your routes in the Global.asax file so that the routes use the .mvc extension.</span></span>

<span data-ttu-id="58145-184">수정된 된 Global.asax 파일 목록 2의 이전 버전의 IIS 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-184">The modified Global.asax file in Listing 2 works with older versions of IIS.</span></span>

<span data-ttu-id="58145-185">**2-Global.asax (확장명이 수정 됨)를 나열 합니다.**</span><span class="sxs-lookup"><span data-stu-id="58145-185">**Listing 2 - Global.asax (modified with extensions)**</span></span>

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample2.vb)]


<span data-ttu-id="58145-186">중요: 해야 Global.asax 파일을 변경 하는 후에 다시 ASP.NET MVC 응용 프로그램을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-186">Important: remember to build your ASP.NET MVC Application again after changing the Global.asax file.</span></span>


<span data-ttu-id="58145-187">Global.asax 파일 목록 2의 두 가지 중요 한 변경 내용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-187">There are two important changes to the Global.asax file in Listing 2.</span></span> <span data-ttu-id="58145-188">Global.asax에 정의 된 두 개의 경로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58145-188">There are now two routes defined in the Global.asax.</span></span> <span data-ttu-id="58145-189">기본 경로 첫 번째 경로 대 한 URL 패턴 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="58145-189">The URL pattern for the Default route, the first route, now looks like:</span></span>

<span data-ttu-id="58145-190">{controller}.mvc/{action}/{id}</span><span class="sxs-lookup"><span data-stu-id="58145-190">{controller}.mvc/{action}/{id}</span></span>

<span data-ttu-id="58145-191">ASP.NET 라우팅 모듈을 가로채는 파일의 종류를 변경 하는.mvc 확장명 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-191">The addition of the .mvc extension changes the type of files that the ASP.NET Routing module intercepts.</span></span> <span data-ttu-id="58145-192">ASP.NET MVC 응용 프로그램을 지금는 이러한 변경으로 인해 다음과 같은 요청을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-192">With this change, the ASP.NET MVC application now routes requests like the following:</span></span>

<span data-ttu-id="58145-193">/Home.mvc/Index/</span><span class="sxs-lookup"><span data-stu-id="58145-193">/Home.mvc/Index/</span></span>

<span data-ttu-id="58145-194">/Product.mvc/Details/3</span><span class="sxs-lookup"><span data-stu-id="58145-194">/Product.mvc/Details/3</span></span>

<span data-ttu-id="58145-195">/Product.mvc/</span><span class="sxs-lookup"><span data-stu-id="58145-195">/Product.mvc/</span></span>

<span data-ttu-id="58145-196">두 번째 경로 루트 경로 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="58145-196">The second route, the Root route, is new.</span></span> <span data-ttu-id="58145-197">루트 경로 대 한이 URL 패턴은 빈 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="58145-197">This URL pattern for the Root route is an empty string.</span></span> <span data-ttu-id="58145-198">이 경로가 일치 응용 프로그램의 루트에 대 한 요청에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-198">This route is necessary for matching requests made against the root of your application.</span></span> <span data-ttu-id="58145-199">예를 들어 루트 경로 다음과 같은 요청을 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-199">For example, the Root route will match a request that looks like this:</span></span>

[<span data-ttu-id="58145-200">http://www.YourApplication.com/</span><span class="sxs-lookup"><span data-stu-id="58145-200">http://www.YourApplication.com/</span></span>](http://www.YourApplication.com/)

<span data-ttu-id="58145-201">경로 테이블에 이러한 수정에 확인 한 후 모든 응용 프로그램에서 링크의 이러한 새 URL 패턴과 호환 되는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-201">After making these modifications to your route table, you'll need to make sure that all of the links in your application are compatible with these new URL patterns.</span></span> <span data-ttu-id="58145-202">즉,.mvc 확장명을 포함 하는 모든 링크 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-202">In other words, make sure that all of your links include the .mvc extension.</span></span> <span data-ttu-id="58145-203">Html.ActionLink() 도우미 메서드를 사용 하 여 링크를 생성 하는 경우 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-203">If you use the Html.ActionLink() helper method to generate your links, then you should not need to make any changes.</span></span>


<span data-ttu-id="58145-204">Registermvc.wcf 스크립트를 사용 하지 않고 ASP.NET 프레임 워크에 직접 매핑되는 IIS에 새 확장을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-204">Instead of using the registermvc.wcf script, you can add a new extension to IIS that is mapped to the ASP.NET framework by hand.</span></span> <span data-ttu-id="58145-205">새 확장을 직접 추가 하는 경우 확인란 레이블이 지정 되었는지 확인 **파일이 있는지 확인** 확인 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-205">When adding a new extension yourself, make sure that the checkbox labeled **Verify that file exists** is not checked.</span></span>


## <a name="hosted-server"></a><span data-ttu-id="58145-206">호스트 된 서버</span><span class="sxs-lookup"><span data-stu-id="58145-206">Hosted Server</span></span>

<span data-ttu-id="58145-207">웹 서버에 항상 액세스할을 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-207">You don't always have access to your web server.</span></span> <span data-ttu-id="58145-208">예를 들어 인터넷 호스팅 공급자를 사용 하 여 ASP.NET MVC 응용 프로그램을 호스팅하는 경우 다음 반드시 않아도 IIS에 대 한 액세스.</span><span class="sxs-lookup"><span data-stu-id="58145-208">For example, if you are hosting your ASP.NET MVC application using an Internet Hosting Provider, then you won't necessarily have access to IIS.</span></span>

<span data-ttu-id="58145-209">이 경우 ASP.NET 프레임 워크에 매핑되는 기존 파일 확장명 중 하나를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-209">In that case, you should use one of the existing file extensions that are mapped to the ASP.NET framework.</span></span> <span data-ttu-id="58145-210">Asp 파일 확장명의 예로.aspx,.axd, 및.ashx 확장을 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-210">Examples of file extensions mapped to ASP.NET include the .aspx, .axd, and .ashx extensions.</span></span>

<span data-ttu-id="58145-211">예를 들어 목록 3에서 수정된 된 Global.asax 파일.mvc 확장명 대신.aspx 확장을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-211">For example, the modified Global.asax file in Listing 3 uses the .aspx extension instead of the .mvc extension.</span></span>

<span data-ttu-id="58145-212">**3-Global.asax (.aspx 확장과 함께 수정 됨)를 나열 합니다.**</span><span class="sxs-lookup"><span data-stu-id="58145-212">**Listing 3 - Global.asax (modified with .aspx extensions)**</span></span>

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample3.vb)]

<span data-ttu-id="58145-213">보기 3의 Global.asax 파일 확장명이.aspx.mvc 확장명 대신 사용 팩트를 제외 하 고 이전 Global.asax 파일와 정확히 같습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-213">The Global.asax file in Listing 3 is exactly the same as the previous Global.asax file except for the fact that it uses the .aspx extension instead of the .mvc extension.</span></span> <span data-ttu-id="58145-214">.Aspx 확장을 사용 하려면 원격 웹 서버에서 설정을 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-214">You don't have to perform any setup on your remote web server to use the .aspx extension.</span></span>

## <a name="creating-a-wildcard-script-map"></a><span data-ttu-id="58145-215">와일드 카드 스크립트 매핑 만들기</span><span class="sxs-lookup"><span data-stu-id="58145-215">Creating a Wildcard Script Map</span></span>

<span data-ttu-id="58145-216">ASP.NET MVC 응용 프로그램에 대 한 Url을 수정 하려면 웹 서버에 액세스할 수 있는 경우 추가로 선택할을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-216">If you don't want to modify the URLs for your ASP.NET MVC application, and you have access to your web server, then you have an additional option.</span></span> <span data-ttu-id="58145-217">ASP.NET 프레임 워크를 웹 서버에 대 한 모든 요청을 매핑하는 와일드 카드 스크립트 맵을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-217">You can create a wildcard script map that maps all requests to the web server to the ASP.NET framework.</span></span> <span data-ttu-id="58145-218">이런 방식으로 (기본 모드)에서 IIS 7.0 또는 IIS 6.0 기본 ASP.NET MVC 경로 테이블을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-218">That way, you can use the default ASP.NET MVC route table with IIS 7.0 (in classic mode) or IIS 6.0.</span></span>

<span data-ttu-id="58145-219">이 옵션은 IIS 웹 서버에 대 한 모든 요청을 가로챌 수 있는지 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-219">Be aware that this option causes IIS to intercept every request made against the web server.</span></span> <span data-ttu-id="58145-220">이미지, 클래식 ASP 페이지 및 HTML 페이지에 대 한 요청이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58145-220">This includes requests for images, classic ASP pages, and HTML pages.</span></span> <span data-ttu-id="58145-221">따라서 와일드 카드를 사용 하면 asp.net 스크립트 맵을 성능에 미치는 영향입니다.</span><span class="sxs-lookup"><span data-stu-id="58145-221">Therefore, enabling a wildcard script map to ASP.NET does have performance implications.</span></span>

<span data-ttu-id="58145-222">IIS 7.0에 대 한 와일드 카드 스크립트 매핑 설정 방법 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-222">Here's how you enable a wildcard script map for IIS 7.0:</span></span>

1. <span data-ttu-id="58145-223">연결 창에서 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-223">Select your application in the Connections window</span></span>
2. <span data-ttu-id="58145-224">다음 사항을 확인는 **기능** 뷰 선택</span><span class="sxs-lookup"><span data-stu-id="58145-224">Make sure that the **Features** view is selected</span></span>
3. <span data-ttu-id="58145-225">두 번 클릭 하 여 **처리기 매핑** 단추</span><span class="sxs-lookup"><span data-stu-id="58145-225">Double-click the **Handler Mappings** button</span></span>
4. <span data-ttu-id="58145-226">클릭는 **와일드 카드 스크립트 매핑 추가** 링크 (그림 3 참조)</span><span class="sxs-lookup"><span data-stu-id="58145-226">Click the **Add Wildcard Script Map** link (see Figure 3)</span></span>
5. <span data-ttu-id="58145-227">경로를 aspnet 입력\_isapi.dll – 파일 (에서 복사할 수 있습니다이 경로 PageHandlerFactory 스크립트 매핑)</span><span class="sxs-lookup"><span data-stu-id="58145-227">Enter the path to the aspnet\_isapi.dll file (You can copy this path from the PageHandlerFactory script map)</span></span>
6. <span data-ttu-id="58145-228">MVC 이름 입력</span><span class="sxs-lookup"><span data-stu-id="58145-228">Enter the name MVC</span></span>
7. <span data-ttu-id="58145-229">클릭는 **확인** 단추</span><span class="sxs-lookup"><span data-stu-id="58145-229">Click the **OK** button</span></span>


<span data-ttu-id="58145-230">[![새 프로젝트 대화 상자](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="58145-230">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.png)</span></span>

<span data-ttu-id="58145-231">**그림 3**: IIS 7.0을 사용 하 여 와일드 카드 스크립트 매핑 만들기 ([전체 크기 이미지를 보려면 클릭](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="58145-231">**Figure 3**: Creating a wildcard script map with IIS 7.0([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image6.png))</span></span>


<span data-ttu-id="58145-232">IIS 6.0을 사용 하 여 와일드 카드 스크립트 매핑을 만들려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-232">Follow these steps to create a wildcard script map with IIS 6.0:</span></span>

1. <span data-ttu-id="58145-233">웹 사이트를 마우스 오른쪽 단추로 클릭 하 고 속성을 선택</span><span class="sxs-lookup"><span data-stu-id="58145-233">Right-click a website and select Properties</span></span>
2. <span data-ttu-id="58145-234">선택 된 **홈 디렉터리** 탭</span><span class="sxs-lookup"><span data-stu-id="58145-234">Select the **Home Directory** tab</span></span>
3. <span data-ttu-id="58145-235">클릭는 **구성** 단추</span><span class="sxs-lookup"><span data-stu-id="58145-235">Click the **Configuration** button</span></span>
4. <span data-ttu-id="58145-236">선택 된 **매핑** 탭</span><span class="sxs-lookup"><span data-stu-id="58145-236">Select the **Mappings** tab</span></span>
5. <span data-ttu-id="58145-237">클릭는 **삽입** 단추 (그림 4 참조)</span><span class="sxs-lookup"><span data-stu-id="58145-237">Click the **Insert** button (see Figure 4)</span></span>
6. <span data-ttu-id="58145-238">Aspnet에 대 한 경로 붙여\_isapi.dll – 실행 파일 (.aspx 파일의 스크립트 맵을에서이 경로 복사할 수) 필드에</span><span class="sxs-lookup"><span data-stu-id="58145-238">Paste the path to the aspnet\_isapi.dll into the Executable field (you can copy this path from the script map for .aspx files)</span></span>
7. <span data-ttu-id="58145-239">확인란의 선택을 취소 **파일이 있는지 확인**</span><span class="sxs-lookup"><span data-stu-id="58145-239">Uncheck the checkbox labeled **Verify that file exists**</span></span>
8. <span data-ttu-id="58145-240">클릭는 **확인** 단추</span><span class="sxs-lookup"><span data-stu-id="58145-240">Click the **OK** button</span></span>


<span data-ttu-id="58145-241">[![새 프로젝트 대화 상자](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="58145-241">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image7.png)</span></span>

<span data-ttu-id="58145-242">**그림 4**: IIS 6.0을 사용 하 여 와일드 카드 스크립트 매핑 만들기 ([전체 크기 이미지를 보려면 클릭](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="58145-242">**Figure 4**: Creating a wildcard script map with IIS 6.0([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image8.png))</span></span>


<span data-ttu-id="58145-243">와일드 카드 스크립트 매핑 사용 하도록 설정 하면 루트 경로 포함 하도록 Global.asax 파일에 경로 테이블을 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58145-243">After you enable wildcard script maps, you need to modify the route table in the Global.asax file so that it includes a Root route.</span></span> <span data-ttu-id="58145-244">그렇지 않으면 응용 프로그램의 루트 페이지에 대 한 요청을 수행 하는 경우 그림 5에 오류 페이지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-244">Otherwise, you'll get the error page in Figure 5 when you make a request for the root page of your application.</span></span> <span data-ttu-id="58145-245">수정된 된 Global.asax 파일 목록 4에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-245">You can use the modified Global.asax file in Listing 4.</span></span>


<span data-ttu-id="58145-246">[![새 프로젝트 대화 상자](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="58145-246">[![The New Project dialog box](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image9.png)</span></span>

<span data-ttu-id="58145-247">**그림 5**: 누락 된 루트 경로 오류 ([전체 크기 이미지를 보려면 클릭](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="58145-247">**Figure 5**: Missing Root route error([Click to view full-size image](using-asp-net-mvc-with-different-versions-of-iis-vb/_static/image10.png))</span></span>


<span data-ttu-id="58145-248">**4-Global.asax (루트 경로와 수정 됨)를 나열 합니다.**</span><span class="sxs-lookup"><span data-stu-id="58145-248">**Listing 4 - Global.asax (modified with Root route)**</span></span>

[!code-vb[Main](using-asp-net-mvc-with-different-versions-of-iis-vb/samples/sample4.vb)]

<span data-ttu-id="58145-249">IIS 7.0 또는 IIS 6.0에 대 한 와일드 카드 스크립트 매핑을 사용 하도록 설정한 후에 다음과 같은 기본 경로 테이블을 사용 하는 요청을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-249">After you enable a wildcard script map for either IIS 7.0 or IIS 6.0, you can make requests that work with the default route table that look like this:</span></span>

/

<span data-ttu-id="58145-250">/ Home/Index</span><span class="sxs-lookup"><span data-stu-id="58145-250">/Home/Index</span></span>

<span data-ttu-id="58145-251">/ 제품/세부 정보/3</span><span class="sxs-lookup"><span data-stu-id="58145-251">/Product/Details/3</span></span>

<span data-ttu-id="58145-252">/ 제품</span><span class="sxs-lookup"><span data-stu-id="58145-252">/Product</span></span>

## <a name="summary"></a><span data-ttu-id="58145-253">요약</span><span class="sxs-lookup"><span data-stu-id="58145-253">Summary</span></span>

<span data-ttu-id="58145-254">이 자습서의 목표는 이전 버전의 IIS (또는 클래식 모드에서 IIS 7.0)를 사용 하는 경우 ASP.NET MVC에 사용 하는 방법을 설명 하는 것 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-254">The goal of this tutorial was to explain how you can use ASP.NET MVC when using an older version of IIS (or IIS 7.0 in classic mode).</span></span> <span data-ttu-id="58145-255">이전 버전의 IIS 사용 하려면 ASP.NET 라우팅이 가져오는 두 가지 방법을 설명한: 기본 경로 테이블을 수정 하거나 와일드 카드 스크립트 맵을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58145-255">We discussed two methods of getting ASP.NET Routing to work with older versions of IIS: Modify the default route table or create a wildcard script map.</span></span>

<span data-ttu-id="58145-256">첫 번째 옵션을 사용 하려면 ASP.NET MVC 응용 프로그램에서 사용 되는 Url을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-256">The first option requires you to modify the URLs used in your ASP.NET MVC application.</span></span> <span data-ttu-id="58145-257">이 첫 번째 옵션의 매우 중요 한 장점 중 하나는 경로 테이블을 수정 하려면 웹 서버에 대 한 액세스를 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-257">One very significant advantage of this first option is that you do not need access to a web server in order to modify the route table.</span></span> <span data-ttu-id="58145-258">즉, 경우에 인터넷을 사용 하 여 ASP.NET MVC 응용 프로그램을 호스팅하는 경우에이 첫 번째 옵션을 사용할 수 있는 호스팅 업체.</span><span class="sxs-lookup"><span data-stu-id="58145-258">That means that you can use this first option even when hosting your ASP.NET MVC application with an Internet hosting company.</span></span>

<span data-ttu-id="58145-259">두 번째 옵션은 와일드 카드 스크립트 매핑 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="58145-259">The second option is to create a wildcard script map.</span></span> <span data-ttu-id="58145-260">이 두 번째 옵션의 장점은입니다 Url을 수정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-260">The advantage of this second option is that you do not need to modify your URLs.</span></span> <span data-ttu-id="58145-261">이 두 번째 옵션의 단점은 ASP.NET MVC 응용 프로그램의 성능 영향을 줄 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58145-261">The disadvantage of this second option is that it can impact the performance of your ASP.NET MVC application.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="58145-262">이전</span><span class="sxs-lookup"><span data-stu-id="58145-262">Previous</span></span>](using-asp-net-mvc-with-different-versions-of-iis-cs.md)
