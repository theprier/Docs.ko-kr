---
uid: mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
title: 프로 파일링 및 디버깅 Glimpse 사용해 ASP.NET MVC 앱 | Microsoft Docs
author: Rick-Anderson
description: Glimpse은 번성 하 고 자세한 성능을 제공 하는 오픈 소스 NuGet 패키지의 제품군 증가, 디버깅 및 ASP.NET에 대 한 진단 정보는 중...
ms.author: aspnetcontent
ms.date: 03/26/2015
ms.assetid: c205805f-efdd-4fa7-9616-f26eab180611
msc.legacyurl: /mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
msc.type: authoredcontent
ms.openlocfilehash: 4d044217d6c33594b39747a765165b8702338027
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37808543"
---
<a name="profile-and-debug-your-aspnet-mvc-app-with-glimpse"></a><span data-ttu-id="73f86-103">프로 파일링 및 디버깅 Glimpse 사용해 ASP.NET MVC 앱</span><span class="sxs-lookup"><span data-stu-id="73f86-103">Profile and debug your ASP.NET MVC app with Glimpse</span></span>
====================
<span data-ttu-id="73f86-104">[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="73f86-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="73f86-105">Glimpse는 번성 하 고 자세한 성능을 제공 하는 오픈 소스 NuGet 패키지의 제품군 증가, 디버깅 및 ASP.NET 앱에 대 한 진단 정보.</span><span class="sxs-lookup"><span data-stu-id="73f86-105">Glimpse is a thriving and growing family of open source NuGet packages that provides detailed performance, debugging and diagnostic information for ASP.NET apps.</span></span> <span data-ttu-id="73f86-106">설치가 간단 간단 하 고 매우 빠른 이며 모든 페이지의 맨 아래에 주요 성능 메트릭을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-106">It's trivial to install, lightweight, ultra-fast, and displays key performance metrics at the bottom of every page.</span></span> <span data-ttu-id="73f86-107">서버 진행 상황을 찾아야 할 때 앱에 드릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-107">It allows you to drill down into your app when you need to find out what's going on at the server.</span></span> <span data-ttu-id="73f86-108">Glimpse Azure 테스트 환경을 포함 하 여 개발 주기 전체에서 사용 하는 것이 좋습니다는 훨씬 중요 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-108">Glimpse provides so much valuable information we recommend you use it throughout your development cycle, including your Azure test environment.</span></span> <span data-ttu-id="73f86-109">하는 동안 [Fiddler](http://www.telerik.com/fiddler) 하며 [F-12 개발 도구](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx) 제공 클라이언트 쪽 보기 Glimpse 서버의 상세 보기를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-109">While [Fiddler](http://www.telerik.com/fiddler) and the [F-12 development tools](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx) provide a client side view, Glimpse provides a detailed view from the server.</span></span> <span data-ttu-id="73f86-110">이 자습서는 간략 한 ASP.NET MVC 및 EF 패키지를 사용 하 여 중점 되지만 다른 많은 패키지 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-110">This tutorial will focus on using the Glimpse ASP.NET MVC and EF packages, but many other packages are available.</span></span> <span data-ttu-id="73f86-111">가능한 경우 적절 한 연결 됩니다 [docs 슬라이드](http://getglimpse.com/Docs/) 유지 관리할 수 있도록 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-111">Where possible I will link to the appropriate [Glimpse docs](http://getglimpse.com/Docs/) which I help maintain.</span></span> <span data-ttu-id="73f86-112">Glimpse는 오픈 소스 프로젝트, 너무 기여할 수 있는 소스 코드 및 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-112">Glimpse is an open source project, you too can contribute to the source code and the docs.</span></span>


- [<span data-ttu-id="73f86-113">Glimpse를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-113">Installing Glimpse</span></span>](#ig)
- [<span data-ttu-id="73f86-114">Localhost에 대 한 이해를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="73f86-114">Enable Glimpse for localhost</span></span>](#eg)
- [<span data-ttu-id="73f86-115">타임 라인 탭</span><span class="sxs-lookup"><span data-stu-id="73f86-115">The Timeline tab</span></span>](#Time)
- [<span data-ttu-id="73f86-116">모델 바인딩</span><span class="sxs-lookup"><span data-stu-id="73f86-116">Model Binding</span></span>](#mb)
- [<span data-ttu-id="73f86-117">경로</span><span class="sxs-lookup"><span data-stu-id="73f86-117">Routes</span></span>](#route)
- [<span data-ttu-id="73f86-118">Glimpse를 사용 하 여 Azure에서</span><span class="sxs-lookup"><span data-stu-id="73f86-118">Using Glimpse on Azure</span></span>](#da)
- [<span data-ttu-id="73f86-119">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="73f86-119">Additional Resources</span></span>](#addRes)

<a id="ig"></a>
## <a name="installing-glimpse"></a><span data-ttu-id="73f86-120">Glimpse를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-120">Installing Glimpse</span></span>

<span data-ttu-id="73f86-121">NuGet 패키지 관리자 콘솔에서 또는 Glimpse를 설치할 수 있습니다 합니다 **NuGet 패키지 관리** 콘솔.</span><span class="sxs-lookup"><span data-stu-id="73f86-121">You can install Glimpse from the NuGet package manager console or from the **Manage NuGet Packages** console.</span></span> <span data-ttu-id="73f86-122">이 데모에서는 Mvc5 및 EF6 패키지를 설치 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-122">For this demo, I'll install the Mvc5 and EF6 packages:</span></span>

![Glimpse NuGet 대화 상자에서 설치](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image1.png)

<span data-ttu-id="73f86-124">검색할 *Glimpse.EF*</span><span class="sxs-lookup"><span data-stu-id="73f86-124">Search for *Glimpse.EF*</span></span>

![NuGet 설치 대화 상자에서 Glimpse.EF](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image2.png)

<span data-ttu-id="73f86-126">선택 하 여 **설치 된 패키지**, 간략 한 종속 모듈 설치를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-126">By selecting **Installed packages**, you can see the Glimpse dependent modules installed:</span></span>

![대화 상자에서 Glimpse 패키지 설치](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image3.png)

<span data-ttu-id="73f86-128">다음 명령을 패키지 관리자 콘솔에서 간략 한 MVC5 및 EF6 모듈을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-128">The following commands install Glimpse MVC5 and EF6 modules from the package manager console:</span></span>

[!code-console[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample1.cmd)]

<a id="eg"></a>
## <a name="enable-glimpse-for-localhost"></a><span data-ttu-id="73f86-129">Localhost에 대 한 이해를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="73f86-129">Enable Glimpse for localhost</span></span>

<span data-ttu-id="73f86-130">이동할 http://localhost:&lt; 포트 번호&gt;/glimpse.axd를 클릭 합니다 <strong>Glimpse 켜기</strong> 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-130">Navigate to http://localhost:&lt;port #&gt;/glimpse.axd and click the <strong>Turn Glimpse On</strong> button.</span></span>

![Glimpse axd 페이지](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image4.png)

<span data-ttu-id="73f86-132">표시 즐겨찾기 모음에 있는 경우 있습니다 수 Glimpse 단추 끌어서 bookmarklets로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-132">If you have your favorites bar displayed, you can drag and drop the Glimpse buttons and add them as bookmarklets:</span></span>

![Glimpse boookmarklets IE](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image5.png)

<span data-ttu-id="73f86-134">이제 앱을 탐색할 수 있습니다 및 **표시를 헤드** (hud가) 페이지의 맨 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-134">You can now navigate your app, and the **Heads Up Display** (HUD) is shown at the bottom of the page.</span></span>

![HUD 사용 하 여 contact Manager 페이지](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image6.png)

<span data-ttu-id="73f86-136">합니다 [Glimpse HUD 페이지](http://getglimpse.com/Docs/Heads-up-Display) 위에 표시 되는 타이밍 정보를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-136">The [Glimpse HUD page](http://getglimpse.com/Docs/Heads-up-Display) details the timing information shown above.</span></span> <span data-ttu-id="73f86-137">비간섭 성능에 표시 되는 데이터 HUD 알릴 수 문제의 즉시 테스트 사이클에 도달 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-137">The unobtrusive performance data the HUD displays can notify you of a problem immediately - before you get to the test cycle.</span></span> <span data-ttu-id="73f86-138">클릭 하는 &quot;g&quot; Glimpse 패널의 오른쪽 아래 모서리에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-138">Clicking on the &quot;g&quot; in the lower right corner brings up the Glimpse panel:</span></span>

![Glimpse 패널](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image7.png)

<span data-ttu-id="73f86-140">위의 이미지에는 [실행 탭](http://getglimpse.com/Docs/Execution-Tab) 을 선택 하면 파이프라인에서 작업 및 필터의 타이밍 정보를 보여 주는 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-140">In the image above, the [Execution tab](http://getglimpse.com/Docs/Execution-Tab) is selected, which shows timing details of the actions and filters in the pipeline.</span></span> <span data-ttu-id="73f86-141">볼 수 있습니다 내 [조사식 중지 필터 타이머](http://www.nuget.org/packages/StopWatch/) 파이프라인의 6 단계를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-141">You can see my [Stop Watch filter timer](http://www.nuget.org/packages/StopWatch/) start at stage 6 of the pipeline.</span></span> <span data-ttu-id="73f86-142">내 간단한 타이머를 제공할 수 있지만 뷰를 렌더링 하 고 권한 부여에 소요 된 시간 모든 누락 데이터 프로필/시간으로 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-142">While my light weight timer can provide useful profile/timing data, it misses all the time spent in authorization and rendering the view.</span></span> <span data-ttu-id="73f86-143">내 타이머를 확인할 수 있습니다 [프로 파일링 하 고 Azure에 ASP.NET MVC 앱 시간](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-143">You can read about my timer at [Profile and Time your ASP.NET MVC app all the way to Azure](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx).</span></span> <span data-ttu-id="73f86-144">합니다 [탭](http://getglimpse.com/Docs/Tabs) 페이지 각 탭에서 자세한 정보 링크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-144">The [Tabs](http://getglimpse.com/Docs/Tabs) page provides links to detailed information on each tab.</span></span>

<a id="Time"></a>
## <a name="the-timeline-tab"></a><span data-ttu-id="73f86-145">타임 라인 탭</span><span class="sxs-lookup"><span data-stu-id="73f86-145">The Timeline tab</span></span>

<span data-ttu-id="73f86-146">Tom Dykstra 수정 했지만 미해결 [EF 6/MVC 5 자습서](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) 를 다음 코드로 강사 컨트롤러를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-146">I've modified Tom Dykstra's outstanding [EF 6/MVC 5 tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) with the following code change to the instructors controller:</span></span>

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample2.cs?highlight=1,20-31)]

<span data-ttu-id="73f86-147">위의 코드 쿼리 문자열에 전달할 수 있습니다 (`eager`) 즉시 또는 명시적 컨트롤에 데이터 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-147">The code above allows me to pass in query string (`eager`) to control eager or explicit loading of data.</span></span> <span data-ttu-id="73f86-148">아래 이미지에서 명시적 로딩 사용 되 고 타이밍이 페이지에 로드 된 각 등록에 표시 된 `Index` 작업 메서드:</span><span class="sxs-lookup"><span data-stu-id="73f86-148">In the image below, explicit loading is used and the timing page shows each enrollment loaded in the `Index` action method:</span></span>

![명시적 로드(explicit loading)](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image8.png)

<span data-ttu-id="73f86-150">다음 코드를 즉시를 지정 하 고 각 등록 후 인출 되는 `Index` 라는:</span><span class="sxs-lookup"><span data-stu-id="73f86-150">In the following code, eager is specified, and each enrollment is fetched after the `Index` view is called:</span></span>

![eager 지정](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image9.png)

<span data-ttu-id="73f86-152">자세한 타이밍 정보를 가져올 시간 세그먼트 위로 가져가면 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-152">You can hover over a time segment to get detailed timing information:</span></span>

![자세한 타이밍을 보려면 가리키기](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image10.png)

<a id="mb"></a>
## <a name="model-binding"></a><span data-ttu-id="73f86-154">모델 바인딩</span><span class="sxs-lookup"><span data-stu-id="73f86-154">Model Binding</span></span>

<span data-ttu-id="73f86-155">합니다 [모델 바인딩 탭](http://getglimpse.com/Docs/Model-Binding-Tab) 는 다양 한 폼 변수는 바인딩하는 방법 및 이유는 일부 바인딩되지 않은 예상한 대로 이해 하는 데 유용한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-155">The [model binding tab](http://getglimpse.com/Docs/Model-Binding-Tab) provides a wealth of information to help you understand how your form variables are bound and why some are not bound as would expect.</span></span> <span data-ttu-id="73f86-156">아래 이미지는 **?**</span><span class="sxs-lookup"><span data-stu-id="73f86-156">The image below shows the **?**</span></span> <span data-ttu-id="73f86-157">아이콘에 해당 기능에 대 한 간략 한 도움말을 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-157">icon, which you can click on to bring up the glimpse help page for that feature.</span></span>

![모델 바인딩 뷰 기능 개요](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image11.png)

<a id="route"></a>
## <a name="routes"></a><span data-ttu-id="73f86-159">경로</span><span class="sxs-lookup"><span data-stu-id="73f86-159">Routes</span></span>

 <span data-ttu-id="73f86-160">Glimpse 경로 탭은 도움이 될 수 있습니다 디버그 및 라우팅 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-160">The Glimpse Routes tab will can help you debug and understand routing.</span></span> <span data-ttu-id="73f86-161">아래 이미지에서 제품 경로가 선택 됩니다 (및 간략 한 규칙을 녹색으로 표시).</span><span class="sxs-lookup"><span data-stu-id="73f86-161">In the image below, the product route is selected (and it shows in green, a Glimpse convention).</span></span> <span data-ttu-id="73f86-162">![선택한 제품 이름을](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) 경로 제약 조건, 영역 및 데이터 토큰에도 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-162">![product name selected](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) Route constraints, Areas and data tokens are also displayed.</span></span> <span data-ttu-id="73f86-163">참조 [Glimpse 경로](http://getglimpse.com/Docs/Routes-Tab) 하 고 [ASP.NET MVC 5의 특성 라우팅](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx) 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-163">See [Glimpse Routes](http://getglimpse.com/Docs/Routes-Tab) and [Attribute Routing in ASP.NET MVC 5](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx) for more information.</span></span> 

<a id="da"></a>
## <a name="using-glimpse-on-azure"></a><span data-ttu-id="73f86-164">Glimpse를 사용 하 여 Azure에서</span><span class="sxs-lookup"><span data-stu-id="73f86-164">Using Glimpse on Azure</span></span>

<span data-ttu-id="73f86-165">간략 한 기본 보안 정책을 이해 표시할 데이터를 로컬 호스트에서 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-165">The Glimpse default security policy only allows Glimpse data to be displayed from local host.</span></span> <span data-ttu-id="73f86-166">원격 서버 (예: Azure에서 웹 앱)에서이 데이터를 볼 수 있도록이 보안 정책을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-166">You can change this security policy so you can view this data on a remote server (such as a web app on Azure).</span></span> <span data-ttu-id="73f86-167">Azure에서 테스트 환경에 대 한 아래쪽까지 강조 표시를 추가 합니다 *web.confg* 눈에 볼 수 있도록 파일:</span><span class="sxs-lookup"><span data-stu-id="73f86-167">For test environments on Azure, add the highlighted mark up to the bottom of the *web.confg* file to enable Glimpse:</span></span>

[!code-xml[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample3.xml?highlight=2-6)]

<span data-ttu-id="73f86-168">모든 사용자만이 변경으로 원격 사이트에 간략 한 데이터를 볼 수입니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-168">With this change alone, any user can see your Glimpse data on a remote site.</span></span> <span data-ttu-id="73f86-169">에 배포할 수 있도록 적용 된 게시 프로필 (예를 들어 사용자 Azure 테스트 proifle.)를 사용 하는 경우 게시 프로필에 위의 태그를 추가 하는 것이 좋습니다. 간략 한 데이터를 제한 하려면 추가 `canViewGlimpseData` 역할만 간략 한 데이터를 보려면이 역할의 사용자를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-169">Consider adding the markup above to a publish profile so it's only deployed an applyed when you use that publish profile (for example, your Azure test proifle.) To restrict Glimpse data, we will add the `canViewGlimpseData` role and only allow users in this role to view Glimpse data.</span></span>

<span data-ttu-id="73f86-170">주석을 제거 합니다 *GlimpseSecurityPolicy.cs* 파일을 변경 합니다 [IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx) 에서 호출 `Administrator` 에 `canViewGlimpseData` 역할:</span><span class="sxs-lookup"><span data-stu-id="73f86-170">Remove the comments from the *GlimpseSecurityPolicy.cs* file and change the [IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx) call from `Administrator` to the `canViewGlimpseData` role:</span></span>

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample4.cs?highlight=6)]

> [!WARNING]
> <span data-ttu-id="73f86-171">보안-Glimpse이 제공한 다양 한 데이터에는 앱의 보안을 노출 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-171">Security - The rich data provided by Glimpse could expose the security of your app.</span></span> <span data-ttu-id="73f86-172">프로덕션 앱에서 사용 하기 위해 Microsoft Glimpse의 보안 감사를 수행 하지.</span><span class="sxs-lookup"><span data-stu-id="73f86-172">Microsoft has not performed a security audit of Glimpse for use on productions apps.</span></span>


<span data-ttu-id="73f86-173">추가 역할에 대 한 정보를 참조 하세요. 필자의 [멤버 자격, OAuth 및 SQL Database를 사용 하 여 보안 ASP.NET MVC 5 웹 앱을 Azure에 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-173">For information on adding roles, see my [Deploy a Secure ASP.NET MVC 5 web app with Membership, OAuth, and SQL Database to Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) tutorial.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="73f86-174">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="73f86-174">Additional Resources</span></span>

- [<span data-ttu-id="73f86-175">멤버 자격, OAuth 및 SQL Database를 사용 하 여 보안 ASP.NET MVC 5 앱을 Azure에 배포</span><span class="sxs-lookup"><span data-stu-id="73f86-175">Deploy a Secure ASP.NET MVC 5 app with Membership, OAuth, and SQL Database to Azure</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)
- <span data-ttu-id="73f86-176">[구성에 간략하게](http://getglimpse.com/Docs/Configuration) -Doc 페이지 탭, 런타임 정책, 로깅 등을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="73f86-176">[Glimpse Configuration](http://getglimpse.com/Docs/Configuration) - Doc page on configuring tabs, runtime policy, logging and more.</span></span>
