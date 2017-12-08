---
uid: mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
title: "프로 파일링 하 고 Glimpse 사용해 ASP.NET MVC 응용 프로그램 디버그 | Microsoft Docs"
author: Rick-Anderson
description: "Glimpse은 활발히 및 자세한 성능을 제공 하는 오픈 소스 NuGet 패키지의 제품군 증가 하 고, 디버깅 및 ASP.NET에 대 한 진단 정보는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/26/2015
ms.topic: article
ms.assetid: c205805f-efdd-4fa7-9616-f26eab180611
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
msc.type: authoredcontent
ms.openlocfilehash: 98b21a54ba00a8c82c3be7ba4e39d44041ed42c6
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="profile-and-debug-your-aspnet-mvc-app-with-glimpse"></a><span data-ttu-id="7d543-103">프로 파일링 하 고 Glimpse 사용해 ASP.NET MVC 응용 프로그램 디버그</span><span class="sxs-lookup"><span data-stu-id="7d543-103">Profile and debug your ASP.NET MVC app with Glimpse</span></span>
====================
<span data-ttu-id="7d543-104">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="7d543-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="7d543-105">Glimpse은 활발히 및 자세한 성능을 제공 하는 오픈 소스 NuGet 패키지의 제품군 증가 하 고, 디버깅 및 ASP.NET 앱에 대 한 진단 정보.</span><span class="sxs-lookup"><span data-stu-id="7d543-105">Glimpse is a thriving and growing family of open source NuGet packages that provides detailed performance, debugging and diagnostic information for ASP.NET apps.</span></span> <span data-ttu-id="7d543-106">설치가 간단 간단 하 고 엄청나게 빠른 이며 모든 페이지의 맨 아래에 주요 성능 메트릭을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-106">It's trivial to install, lightweight, ultra-fast, and displays key performance metrics at the bottom of every page.</span></span> <span data-ttu-id="7d543-107">드릴 다운 하려면 응용 프로그램 서버에서의 진행 상황 확인 해야 할 때 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-107">It allows you to drill down into your app when you need to find out what's going on at the server.</span></span> <span data-ttu-id="7d543-108">Glimpse Azure 테스트 환경을 포함 하 여 개발 주기 전체에서 사용 하는 것이 좋습니다는 훨씬 중요 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-108">Glimpse provides so much valuable information we recommend you use it throughout your development cycle, including your Azure test environment.</span></span> <span data-ttu-id="7d543-109">반면 [Fiddler](http://www.telerik.com/fiddler) 및 [F-12 개발 도구](https://msdn.microsoft.com/en-us/library/ie/gg589512(v=vs.85).aspx) 클라이언트 쪽 제공 보기 Glimpse 서버에서 자세히 보기를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-109">While [Fiddler](http://www.telerik.com/fiddler) and the [F-12 development tools](https://msdn.microsoft.com/en-us/library/ie/gg589512(v=vs.85).aspx) provide a client side view, Glimpse provides a detailed view from the server.</span></span> <span data-ttu-id="7d543-110">이 자습서는 간략 ASP.NET MVC와 EF 패키지를 사용 하 여 중점적 하지만 사용할 수 있는 다른 여러 패키지.</span><span class="sxs-lookup"><span data-stu-id="7d543-110">This tutorial will focus on using the Glimpse ASP.NET MVC and EF packages, but many other packages are available.</span></span> <span data-ttu-id="7d543-111">가능한 경우을 적절 한에 연결 됩니다 [docs 슬라이드](http://getglimpse.com/Docs/) 유지 관리할 수 있도록입니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-111">Where possible I will link to the appropriate [Glimpse docs](http://getglimpse.com/Docs/) which I help maintain.</span></span> <span data-ttu-id="7d543-112">눈에 볼 수 있는 오픈 소스 프로젝트를 너무 기여할 수 있는 소스 코드와 문서.</span><span class="sxs-lookup"><span data-stu-id="7d543-112">Glimpse is an open source project, you too can contribute to the source code and the docs.</span></span>


- [<span data-ttu-id="7d543-113">Glimpse를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-113">Installing Glimpse</span></span>](#ig)
- [<span data-ttu-id="7d543-114">로컬 호스트에 대 한 이해를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="7d543-114">Enable Glimpse for localhost</span></span>](#eg)
- [<span data-ttu-id="7d543-115">타임 라인 탭</span><span class="sxs-lookup"><span data-stu-id="7d543-115">The Timeline tab</span></span>](#Time)
- [<span data-ttu-id="7d543-116">모델 바인딩</span><span class="sxs-lookup"><span data-stu-id="7d543-116">Model Binding</span></span>](#mb)
- [<span data-ttu-id="7d543-117">경로</span><span class="sxs-lookup"><span data-stu-id="7d543-117">Routes</span></span>](#route)
- [<span data-ttu-id="7d543-118">Glimpse를 사용 하 여 Azure에서</span><span class="sxs-lookup"><span data-stu-id="7d543-118">Using Glimpse on Azure</span></span>](#da)
- [<span data-ttu-id="7d543-119">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7d543-119">Additional Resources</span></span>](#addRes)

<a id="ig"></a>
## <a name="installing-glimpse"></a><span data-ttu-id="7d543-120">Glimpse를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-120">Installing Glimpse</span></span>

<span data-ttu-id="7d543-121">NuGet 패키지 관리자 콘솔에서 또는 Glimpse를 설치할 수는 **NuGet 패키지 관리** 콘솔.</span><span class="sxs-lookup"><span data-stu-id="7d543-121">You can install Glimpse from the NuGet package manager console or from the **Manage NuGet Packages** console.</span></span> <span data-ttu-id="7d543-122">이 데모에서는 m v c 5 및 EF6 패키지 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-122">For this demo, I'll install the Mvc5 and EF6 packages:</span></span>

![Glimpse NuGet 대화 상자에서 설치](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image1.png)

<span data-ttu-id="7d543-124">검색할 *Glimpse.EF*</span><span class="sxs-lookup"><span data-stu-id="7d543-124">Search for *Glimpse.EF*</span></span>

![NuGet 설치 대화 상자에서 Glimpse.EF](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image2.png)

<span data-ttu-id="7d543-126">선택 하 여 **설치 된 패키지**, 설치 된 Glimpse 종속 모듈을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-126">By selecting **Installed packages**, you can see the Glimpse dependent modules installed:</span></span>

![대화 상자에서 Glimpse 패키지 설치](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image3.png)

<span data-ttu-id="7d543-128">다음 명령을 패키지 관리자 콘솔에서 Glimpse m v c 5 및 EF6 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-128">The following commands install Glimpse MVC5 and EF6 modules from the package manager console:</span></span>

[!code-console[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample1.cmd)]

<a id="eg"></a>
## <a name="enable-glimpse-for-localhost"></a><span data-ttu-id="7d543-129">로컬 호스트에 대 한 이해를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="7d543-129">Enable Glimpse for localhost</span></span>

<span data-ttu-id="7d543-130">Http://localhost로 이동:&lt;포트 번호&gt;/glimpse.axd 누른는 **Glimpse 켜기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-130">Navigate to http://localhost:&lt;port #&gt;/glimpse.axd and click the **Turn Glimpse On** button.</span></span>

![Glimpse axd 페이지](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image4.png)

<span data-ttu-id="7d543-132">즐겨찾기 모음 표시를 설정한 경우 있습니다 수 및 Glimpse 단추 끌어서 bookmarklets로 추가:</span><span class="sxs-lookup"><span data-stu-id="7d543-132">If you have your favorites bar displayed, you can drag and drop the Glimpse buttons and add them as bookmarklets:</span></span>

![IE Glimpse boookmarklets와](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image5.png)

<span data-ttu-id="7d543-134">이제 응용 프로그램을 탐색할 수 있습니다 및 **헤드를 디스플레이** (HUD) 페이지의 맨 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-134">You can now navigate your app, and the **Heads Up Display** (HUD) is shown at the bottom of the page.</span></span>

![HUD 있는 연락처 관리자 페이지](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image6.png)

<span data-ttu-id="7d543-136">[Glimpse HUD 페이지](http://getglimpse.com/Docs/Heads-up-Display) 위에 표시 된 타이밍 정보에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-136">The [Glimpse HUD page](http://getglimpse.com/Docs/Heads-up-Display) details the timing information shown above.</span></span> <span data-ttu-id="7d543-137">비 가시적인 성능에 표시 되는 데이터는 HUD에 알릴 수 있습니다 문제 즉시-테스트 사이클에 도달 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="7d543-137">The unobtrusive performance data the HUD displays can notify you of a problem immediately - before you get to the test cycle.</span></span> <span data-ttu-id="7d543-138">클릭 하 고 &quot;g&quot; Glimpse 패널의 오른쪽 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-138">Clicking on the &quot;g&quot; in the lower right corner brings up the Glimpse panel:</span></span>

![Glimpse 패널](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image7.png)

<span data-ttu-id="7d543-140">위의 그림에는 [실행 탭](http://getglimpse.com/Docs/Execution-Tab) 을 선택 하면 파이프라인에서 작업 및 필터의 타이밍 정보를 보여 주는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-140">In the image above, the [Execution tab](http://getglimpse.com/Docs/Execution-Tab) is selected, which shows timing details of the actions and filters in the pipeline.</span></span> <span data-ttu-id="7d543-141">볼 수 있습니다 내 [중지 조사식 필터 타이머](http://www.nuget.org/packages/StopWatch/) 파이프라인의 6 단계에서 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-141">You can see my [Stop Watch filter timer](http://www.nuget.org/packages/StopWatch/) start at stage 6 of the pipeline.</span></span> <span data-ttu-id="7d543-142">내 경량 타이머를 제공 하는 동안 데이터 프로필/타이밍으로 유용한 것 누락 수 항상 권한 부여에 소요 된 및 뷰를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-142">While my light weight timer can provide useful profile/timing data, it misses all the time spent in authorization and rendering the view.</span></span> <span data-ttu-id="7d543-143">내 타이머를 참고할 수 [프로 파일링 하 고 Azure으로 ASP.NET MVC 응용 프로그램 시간](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-143">You can read about my timer at [Profile and Time your ASP.NET MVC app all the way to Azure](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx).</span></span> <span data-ttu-id="7d543-144">[탭](http://getglimpse.com/Docs/Tabs) 페이지에서는 각 탭에서 자세한 정보에 대 한 링크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-144">The [Tabs](http://getglimpse.com/Docs/Tabs) page provides links to detailed information on each tab.</span></span>

<a id="Time"></a>
## <a name="the-timeline-tab"></a><span data-ttu-id="7d543-145">타임 라인 탭</span><span class="sxs-lookup"><span data-stu-id="7d543-145">The Timeline tab</span></span>

<span data-ttu-id="7d543-146">Tom Dykstra 수정 했지만 미해결 [EF 6/MVC 5 자습서](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) 를 다음 코드로 강사 컨트롤러에 변경:</span><span class="sxs-lookup"><span data-stu-id="7d543-146">I've modified Tom Dykstra's outstanding [EF 6/MVC 5 tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) with the following code change to the instructors controller:</span></span>

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample2.cs?highlight=1,20-31)]

<span data-ttu-id="7d543-147">위의 코드 쿼리 문자열에 전달할 수 있습니다 (`eager`) eager 또는 명시적 컨트롤에 데이터 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-147">The code above allows me to pass in query string (`eager`) to control eager or explicit loading of data.</span></span> <span data-ttu-id="7d543-148">아래 그림에서는 명시적 로드를 사용 하 고 타이밍 페이지에 로드 된 각 등록에 표시 된 `Index` 동작 메서드:</span><span class="sxs-lookup"><span data-stu-id="7d543-148">In the image below, explicit loading is used and the timing page shows each enrollment loaded in the `Index` action method:</span></span>

![명시적 로드(explicit loading)](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image8.png)

<span data-ttu-id="7d543-150">다음 코드에서는 eager를 지정 하 고 각 등록 후 인출 되는 `Index` 보기에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-150">In the following code, eager is specified, and each enrollment is fetched after the `Index` view is called:</span></span>

![eager 지정](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image9.png)

<span data-ttu-id="7d543-152">자세한 타이밍 정보를 가져올 시간 세그먼트를 가리키면 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-152">You can hover over a time segment to get detailed timing information:</span></span>

![가리켜 자세한 타이밍을 확인 합니다.](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image10.png)

<a id="mb"></a>
## <a name="model-binding"></a><span data-ttu-id="7d543-154">모델 바인딩</span><span class="sxs-lookup"><span data-stu-id="7d543-154">Model Binding</span></span>

<span data-ttu-id="7d543-155">[모델 바인딩 탭](http://getglimpse.com/Docs/Model-Binding-Tab) 다양 한 폼 변수 방법을 알아둡니다 및 이유 일부 바인딩되지 않은 짐작할 이해를 돕는 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-155">The [model binding tab](http://getglimpse.com/Docs/Model-Binding-Tab) provides a wealth of information to help you understand how your form variables are bound and why some are not bound as would expect.</span></span> <span data-ttu-id="7d543-156">다음 이미지는 **?**</span><span class="sxs-lookup"><span data-stu-id="7d543-156">The image below shows the **?**</span></span> <span data-ttu-id="7d543-157">아이콘에 해당 기능에 대 한 간략 도움말 페이지를 열고 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-157">icon, which you can click on to bring up the glimpse help page for that feature.</span></span>

![glimpse 모델 뷰 바인딩](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image11.png)

<a id="route"></a>
## <a name="routes"></a><span data-ttu-id="7d543-159">경로</span><span class="sxs-lookup"><span data-stu-id="7d543-159">Routes</span></span>

 <span data-ttu-id="7d543-160">Glimpse 경로 탭 수 할 디버그 라우팅 이해 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-160">The Glimpse Routes tab will can help you debug and understand routing.</span></span> <span data-ttu-id="7d543-161">아래 그림에서는 제품 경로가 선택 됩니다 (및 녹색, Glimpse 규칙으로에서 표시).</span><span class="sxs-lookup"><span data-stu-id="7d543-161">In the image below, the product route is selected (and it shows in green, a Glimpse convention).</span></span> <span data-ttu-id="7d543-162">![선택 된 제품 이름을](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) 경로 제약 조건, 영역 및 데이터 토큰에도 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-162">![product name selected](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) Route constraints, Areas and data tokens are also displayed.</span></span> <span data-ttu-id="7d543-163">참조 [Glimpse 경로](http://getglimpse.com/Docs/Routes-Tab) 및 [ASP.NET MVC 5에서 특성 라우팅을](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-163">See [Glimpse Routes](http://getglimpse.com/Docs/Routes-Tab) and [Attribute Routing in ASP.NET MVC 5](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx) for more information.</span></span> 

<a id="da"></a>
## <a name="using-glimpse-on-azure"></a><span data-ttu-id="7d543-164">Glimpse를 사용 하 여 Azure에서</span><span class="sxs-lookup"><span data-stu-id="7d543-164">Using Glimpse on Azure</span></span>

<span data-ttu-id="7d543-165">Glimpse 기본 보안 정책을 이해 표시할 데이터를 로컬 호스트에서 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-165">The Glimpse default security policy only allows Glimpse data to be displayed from local host.</span></span> <span data-ttu-id="7d543-166">원격 서버 (예: Azure에서 웹 응용 프로그램)에이 데이터를 볼 수 있도록이 보안 정책을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-166">You can change this security policy so you can view this data on a remote server (such as a web app on Azure).</span></span> <span data-ttu-id="7d543-167">Azure에서 테스트 환경용의 맨 아래까지 강조 표시 된 표시를 추가 *web.confg* 눈에 볼 수 있도록 파일:</span><span class="sxs-lookup"><span data-stu-id="7d543-167">For test environments on Azure, add the highlighted mark up to the bottom of the *web.confg* file to enable Glimpse:</span></span>

[!code-xml[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample3.xml?highlight=2-6)]

<span data-ttu-id="7d543-168">모든 사용자만 이러한 변경으로 인해 원격 사이트에 눈에 볼 수 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-168">With this change alone, any user can see your Glimpse data on a remote site.</span></span> <span data-ttu-id="7d543-169">에 배포 된 적용 된 게시 프로필 (예를 들어 프로그램 Azure 테스트 proifle.)을 사용 하는 경우 위의 태그 게시 프로필에 추가 하는 것이 좋습니다. 추가 될 Glimpse 데이터를 제한 하려면는 `canViewGlimpseData` 역할만 Glimpse 데이터를 보려면이 역할의 사용자가 허용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-169">Consider adding the markup above to a publish profile so it's only deployed an applyed when you use that publish profile (for example, your Azure test proifle.) To restrict Glimpse data, we will add the `canViewGlimpseData` role and only allow users in this role to view Glimpse data.</span></span>

<span data-ttu-id="7d543-170">주석을 제거는 *GlimpseSecurityPolicy.cs* 파일을 변경는 [IsInRole](https://msdn.microsoft.com/en-us/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx) 에서 호출할 `Administrator` 에 `canViewGlimpseData` 역할:</span><span class="sxs-lookup"><span data-stu-id="7d543-170">Remove the comments from the *GlimpseSecurityPolicy.cs* file and change the [IsInRole](https://msdn.microsoft.com/en-us/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx) call from `Administrator` to the `canViewGlimpseData` role:</span></span>

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample4.cs?highlight=6)]

> [!WARNING]
> <span data-ttu-id="7d543-171">보안-Glimpse에서 제공 되는 다양 한 데이터는 응용 프로그램의 보안을 노출 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-171">Security - The rich data provided by Glimpse could expose the security of your app.</span></span> <span data-ttu-id="7d543-172">Microsoft은 프로덕션 앱에서 사용 하기 위해 Glimpse의 보안 감사를 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-172">Microsoft has not performed a security audit of Glimpse for use on productions apps.</span></span>


<span data-ttu-id="7d543-173">추가 역할에 대 한 정보를 참조 하세요. 내 [멤버 자격, OAuth, SQL 데이터베이스와 Secure ASP.NET MVC 5 웹 응용 프로그램을 Azure에 배포](https://azure.microsoft.com/en-us/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-173">For information on adding roles, see my [Deploy a Secure ASP.NET MVC 5 web app with Membership, OAuth, and SQL Database to Azure](https://azure.microsoft.com/en-us/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) tutorial.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="7d543-174">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7d543-174">Additional Resources</span></span>

- [<span data-ttu-id="7d543-175">멤버 자격, OAuth, SQL 데이터베이스와 보안 ASP.NET MVC 5 앱을 Azure에 배포</span><span class="sxs-lookup"><span data-stu-id="7d543-175">Deploy a Secure ASP.NET MVC 5 app with Membership, OAuth, and SQL Database to Azure</span></span>](https://azure.microsoft.com/en-us/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)
- <span data-ttu-id="7d543-176">[구성 슬라이드](http://getglimpse.com/Docs/Configuration) -Doc 페이지 탭, 런타임 정책을, 로깅 등을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d543-176">[Glimpse Configuration](http://getglimpse.com/Docs/Configuration) - Doc page on configuring tabs, runtime policy, logging and more.</span></span>
