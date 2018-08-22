---
uid: mvc/overview/releases/whats-new-in-aspnet-mvc-52
title: ASP.NET MVC 5.2의에서 새로운 기능 | Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 12/25/2014
ms.assetid: 97972587-2720-48b4-b158-f35f2e855fbf
msc.legacyurl: /mvc/overview/releases/whats-new-in-aspnet-mvc-52
msc.type: authoredcontent
ms.openlocfilehash: 8c3c5de55396635d2e7f2b7726f54be1c06bb691
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823816"
---
<a name="whats-new-in-aspnet-mvc-52"></a><span data-ttu-id="c5d3a-102">ASP.NET MVC 5.2의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="c5d3a-102">What’s New in ASP.NET MVC 5.2</span></span>
====================
<span data-ttu-id="c5d3a-103">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c5d3a-103">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="c5d3a-104">이 항목에서는 ASP.NET MVC 5.2의 새로운 기능에 대해 설명 합니다. [Microsoft.AspNet.MVC 5.2.2](#52) 고 [ASP.NET MVC 5.2.3 베타](#mvc523Beta)</span><span class="sxs-lookup"><span data-stu-id="c5d3a-104">This topic describes what's new for ASP.NET MVC 5.2, [Microsoft.AspNet.MVC 5.2.2](#52) and [ASP.NET MVC 5.2.3 Beta](#mvc523Beta)</span></span>

- [<span data-ttu-id="c5d3a-105">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="c5d3a-105">Software Requirements</span></span>](#softRequire)
- [<span data-ttu-id="c5d3a-106">다운로드</span><span class="sxs-lookup"><span data-stu-id="c5d3a-106">Download</span></span>](#download)
- [<span data-ttu-id="c5d3a-107">문서</span><span class="sxs-lookup"><span data-stu-id="c5d3a-107">Documentation</span></span>](#documentation)
- [<span data-ttu-id="c5d3a-108">ASP.NET MVC 5.2의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="c5d3a-108">New Features in ASP.NET MVC 5.2</span></span>](#new-features)

    - [<span data-ttu-id="c5d3a-109">특성 라우팅 기능 향상</span><span class="sxs-lookup"><span data-stu-id="c5d3a-109">Attribute routing improvements</span></span>](#attributerouting)
- [<span data-ttu-id="c5d3a-110">알려진된 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="c5d3a-110">Known Issues and Breaking Changes</span></span>](#knownbreakingchanges)
- [<span data-ttu-id="c5d3a-111">버그 수정</span><span class="sxs-lookup"><span data-stu-id="c5d3a-111">Bug Fixes</span></span>](#bug-fixes)
- [<span data-ttu-id="c5d3a-112">Microsoft.AspNet.MVC 5.2.2</span><span class="sxs-lookup"><span data-stu-id="c5d3a-112">Microsoft.AspNet.MVC 5.2.2</span></span>](#52)

<a id="softRequire"></a>
## <a name="software-requirements"></a><span data-ttu-id="c5d3a-113">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="c5d3a-113">Software Requirements</span></span>

- <span data-ttu-id="c5d3a-114">Visual Studio 2012: 다운로드 [ASP.NET 및 웹 도구 2013.1 Visual Studio 2012 용](https://go.microsoft.com/fwlink/?LinkId=390062)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-114">Visual Studio 2012: Download [ASP.NET and Web Tools 2013.1 for Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkId=390062).</span></span>
- <span data-ttu-id="c5d3a-115">Visual Studio 2013: 다운로드 [Visual Studio 2013 업데이트](https://go.microsoft.com/fwlink/?LinkId=390064) 이상.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-115">Visual Studio 2013: Download [Visual Studio 2013 Update](https://go.microsoft.com/fwlink/?LinkId=390064) or higher.</span></span> <span data-ttu-id="c5d3a-116">이 업데이트는 ASP.NET MVC 5.2 Razor 뷰를 편집 하기 위해 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-116">This update is needed for editing ASP.NET MVC 5.2 Razor Views.</span></span>

<a id="download"></a>
## <a name="download"></a><span data-ttu-id="c5d3a-117">다운로드</span><span class="sxs-lookup"><span data-stu-id="c5d3a-117">Download</span></span>

<span data-ttu-id="c5d3a-118">NuGet 갤러리에서 NuGet 패키지로 런타임 기능 해제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-118">The runtime features are released as NuGet packages on the NuGet gallery.</span></span> <span data-ttu-id="c5d3a-119">모든 런타임 패키지를 수행 합니다 [유의 적 버전](http://semver.org/) 사양입니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-119">All the runtime packages follow the [Semantic Versioning](http://semver.org/) specification.</span></span> <span data-ttu-id="c5d3a-120">다음 버전이 최신 ASP.NET MVC 5.2 패키지: "5.2.0"입니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-120">The latest ASP.NET MVC 5.2 package has the following version: "5.2.0".</span></span> <span data-ttu-id="c5d3a-121">설치 하거나 이러한 패키지를 통해 업데이트할 수 있습니다 [NuGet](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-121">You can install or update these packages through [NuGet](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/).</span></span> <span data-ttu-id="c5d3a-122">릴리스에 NuGet의 해당 지역화 된 패키지도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-122">The release also includes corresponding localized packages on NuGet.</span></span>

<span data-ttu-id="c5d3a-123">설치 하거나 NuGet 패키지 관리자 콘솔을 사용 하 여 릴리스된 NuGet 패키지를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-123">You can install or update to the released NuGet packages by using the NuGet Package Manager Console:</span></span>

<span data-ttu-id="c5d3a-124">Install-package Microsoft.AspNet.Mvc-버전 5.2.0</span><span class="sxs-lookup"><span data-stu-id="c5d3a-124">Install-Package Microsoft.AspNet.Mvc -Version 5.2.0</span></span>

<a id="documentation"></a>
## <a name="documentation"></a><span data-ttu-id="c5d3a-125">설명서</span><span class="sxs-lookup"><span data-stu-id="c5d3a-125">Documentation</span></span>

<span data-ttu-id="c5d3a-126">자습서 및 ASP.NET MVC 5.2에 대 한 다른 정보는 ASP.NET 웹 사이트에서 사용할 수 있습니다 ([https://www.asp.net/mvc](../../index.md)).</span><span class="sxs-lookup"><span data-stu-id="c5d3a-126">Tutorials and other information about ASP.NET MVC 5.2 are available from the ASP.NET web site ([https://www.asp.net/mvc](../../index.md)).</span></span>

<a id="new-features"></a>
## <a name="new-features-in-aspnet-mvc-52"></a><span data-ttu-id="c5d3a-127">ASP.NET MVC 5.2의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="c5d3a-127">New Features in ASP.NET MVC 5.2</span></span>

<a id="attributerouting"></a>
### <a name="attribute-routing-improvements"></a><span data-ttu-id="c5d3a-128">특성 라우팅 기능 향상</span><span class="sxs-lookup"><span data-stu-id="c5d3a-128">Attribute routing improvements</span></span>

<span data-ttu-id="c5d3a-129">특성 라우팅은 이제 호출 IDirectRouteProvider 특성 경로 검색 하 고 구성 하는 방법을 완전히 제어할 수 있는 확장성 지점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-129">Attribute Routing now provides an extensibility point called IDirectRouteProvider, which allows full control over how attribute routes are discovered and configured.</span></span> <span data-ttu-id="c5d3a-130">IDirectRouteProvider는 작업 및 해당 작업에 대 한 라우팅 구성이 필요한 정확 하 게 지정 하려면 연결 된 경로 정보와 함께 컨트롤러의 목록을 제공 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-130">An IDirectRouteProvider is responsible for providing a list of actions and controllers along with associated route information to specify exactly what routing configuration is desired for those actions.</span></span> <span data-ttu-id="c5d3a-131">IDirectRouteProvider 구현은 MapAttributes/MapHttpAttributeRoutes를 호출할 때 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-131">An IDirectRouteProvider implementation may be specified when calling MapAttributes/MapHttpAttributeRoutes.</span></span>

<span data-ttu-id="c5d3a-132">IDirectRouteProvider 사용자 지정이 기본 구현 DefaultDirectRouteProvider를 확장 하 여 가장 쉬운 방법은 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-132">Customizing IDirectRouteProvider will be easiest by extending our default implementation, DefaultDirectRouteProvider.</span></span> <span data-ttu-id="c5d3a-133">이 클래스는 특성을 검색, 경로 항목을 만들고, 경로 접두사 및 영역 접두사 검색에 대 한 논리를 변경 하는 별도 재정의 가능한 가상 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-133">This class provides separate overridable virtual methods to change the logic for discovering attributes, creating route entries, and discovering route prefix and area prefix.</span></span>

<span data-ttu-id="c5d3a-134">새 특성 라우팅의 확장성 IDirectRouteProvider 사용 하 여 사용자 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-134">With the new attribute routing extensibility of IDirectRouteProvider, a user could do the following:</span></span>

1. <span data-ttu-id="c5d3a-135">특성 경로 상속을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-135">Support Inheritance of attribute routes.</span></span> <span data-ttu-id="c5d3a-136">예를 들어, 다음 시나리오에서는 BaseController 정의한는 특성 경로 규칙 블로그 및 저장소 컨트롤러에 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-136">For example, in the following scenario Blog and Store controllers are using an attribute route convention that is defined by the BaseController.</span></span> 

    [!code-csharp[Main](whats-new-in-aspnet-mvc-52/samples/sample1.cs)]
2. <span data-ttu-id="c5d3a-137">특성 경로 대 한 경로 이름을 자동으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-137">Automatically generate route names for attribute routes.</span></span> 

    [!code-csharp[Main](whats-new-in-aspnet-mvc-52/samples/sample2.cs)]
3. <span data-ttu-id="c5d3a-138">경로 경로 테이블에 추가 되기 전에 하나의 중앙 위치에서 경로 접두사를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-138">Modify route prefixes in one central place before the routes get added to the route table.</span></span>
4. <span data-ttu-id="c5d3a-139">검색할 특성 라우팅 하려는 컨트롤러를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-139">Filter out the controllers on which you want the attribute routing to look for.</span></span> <span data-ttu-id="c5d3a-140">바랍니다 3 및 4에 대 한 블로그를 곧.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-140">We hope to blog on 3 and 4 soon.</span></span>

### <a name="facebook-fixes-for-changed-api-surface"></a><span data-ttu-id="c5d3a-141">Facebook은 API 화면 변경된에 대 한 수정</span><span class="sxs-lookup"><span data-stu-id="c5d3a-141">Facebook fixes for changed API surface</span></span>

<span data-ttu-id="c5d3a-142">MVC Facebook 패키지 [끊기기](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=v5.2%20RC&amp;assignedTo=All&amp;component=Facebook&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=All) Facebook에서 몇 가지 API 변경으로 인해 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-142">The MVC Facebook package [was broken](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=v5.2%20RC&amp;assignedTo=All&amp;component=Facebook&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=All) due to few API changes made by Facebook.</span></span> <span data-ttu-id="c5d3a-143">새 Facebook 패키지 (Microsoft.AspNet.Facebook 1.0.0) 이러한 문제를 해결 하려면 릴리스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-143">We are also releasing a new Facebook package (Microsoft.AspNet.Facebook 1.0.0) to fix these issues.</span></span>

<a id="knownbreakingchanges"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="c5d3a-144">알려진된 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="c5d3a-144">Known Issues and Breaking Changes</span></span>

### <a name="scaffolding-mvcweb-api-into-a-project-with-520-packages-results-in-512-packages-for-ones-that-dont-already-exist-in-the-project"></a><span data-ttu-id="c5d3a-145">5.2.0 사용 하 여 프로젝트에 스 캐 폴딩 MVC/웹 API 프로젝트에 이미 존재 하지 않는 것에 대 한 5.1.2에서 패키지가 결과 패키지</span><span class="sxs-lookup"><span data-stu-id="c5d3a-145">Scaffolding MVC/Web API into a project with 5.2.0 packages results in 5.1.2 packages for ones that don't already exist in the project</span></span>

<span data-ttu-id="c5d3a-146">ASP.NET MVC 5.2.0에 대 한 NuGet 패키지를 업데이트 해도 ASP.NET 스 캐 폴딩와 같은 Visual Studio 도구 또는 ASP.NET 웹 응용 프로그램 프로젝트 템플릿을 업데이트 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-146">Updating NuGet packages for ASP.NET MVC 5.2.0 does not update the Visual Studio tools such as ASP.NET scaffolding or the ASP.NET Web Application project template.</span></span> <span data-ttu-id="c5d3a-147">이전 버전의 ASP.NET 런타임 패키지 (예: 업데이트 2에서 5.1.2)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-147">They use the previous version of the ASP.NET runtime packages (e.g. 5.1.2 in Update 2).</span></span> <span data-ttu-id="c5d3a-148">결과적으로, ASP.NET 스 캐 폴딩은 이미 프로젝트에서 사용할 수 없는 경우에 필요한 패키지의 이전 버전 (예: 업데이트 2에서 5.1.2)으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-148">As a result, the ASP.NET scaffolding will install the previous version (e.g. 5.1.2 in Update 2) of the required packages, if they are not already available in your projects.</span></span> <span data-ttu-id="c5d3a-149">그러나 Visual Studio 2013 RTM 또는 업데이트 1에서 ASP.NET 스 캐 폴딩 프로젝트에서 최신 패키지를 덮어쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-149">However, the ASP.NET scaffolding in Visual Studio 2013 RTM or Update 1 does not overwrite the latest packages in your projects.</span></span> <span data-ttu-id="c5d3a-150">ASP.NET Web API 2.2에 ASP.NET MVC 5.2 프로젝트의 패키지를 업데이트 한 후에 스 캐 폴딩을 사용 하는 경우 Web API 및 ASP.NET MVC의 버전이 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-150">If you use ASP.NET scaffolding after updating the packages of your projects to Web API 2.2 or ASP.NET MVC 5.2, make sure the versions of Web API and ASP.NET MVC are consistent.</span></span>

### <a name="microsoftjqueryunobtrusivevalidation-nuget-package-installation-fails-because-it-is-unable-to-find-a-version-of-microsoftjqueryunobtrusivevalidation-compatible-to-jquery-141"></a><span data-ttu-id="c5d3a-151">JQuery 1.4.1 호환 Microsoft.jQuery.Unobtrusive.Validation의 버전을 찾을 수 없기 때문에 Microsoft.jQuery.Unobtrusive.Validation NuGet 패키지 설치 실패</span><span class="sxs-lookup"><span data-stu-id="c5d3a-151">Microsoft.jQuery.Unobtrusive.Validation NuGet package installation fails because it is unable to find a version of Microsoft.jQuery.Unobtrusive.Validation compatible to jQuery 1.4.1</span></span>

<span data-ttu-id="c5d3a-152">Microsoft.jQuery.Unobtrusive.Validation 필요한 jQuery &gt;1.8 및 jQuery.Validation = &gt;1.8 =.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-152">Microsoft.jQuery.Unobtrusive.Validation requires jQuery &gt;=1.8 and jQuery.Validation &gt;=1.8.</span></span> <span data-ttu-id="c5d3a-153">But,jQuery.Validation (1.8) 필요한 jQuery (&#8805; 1.3.2 &amp; &amp; &#8804; 1.6).</span><span class="sxs-lookup"><span data-stu-id="c5d3a-153">But,jQuery.Validation (1.8) needs jQuery (&#8805; 1.3.2 &amp;&amp; &#8804; 1.6).</span></span> <span data-ttu-id="c5d3a-154">이 인해 NuGet 동시에, JQuery 1.8 및 jQuery.Validation 1.8 설치 하는 경우 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-154">Because of this, when NuGet installs the JQuery 1.8 and jQuery.Validation 1.8 at the same time, it fails.</span></span> <span data-ttu-id="c5d3a-155">이 문제를 표시 하는 경우에 jQuery.Validation 버전 간단히 업데이트할 수 있습니다 &gt; =  [1.8.0.1](https://www.nuget.org/packages/jQuery.Validation/1.8.0.1) 고정 jQuery cap가 먼저 있어야 설치 하려면 Microsoft.jQuery.Unobtrusive.Validation 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-155">When you see this issue, you can simply update the version of jQuery.Validation to &gt;= [1.8.0.1](https://www.nuget.org/packages/jQuery.Validation/1.8.0.1) which has the jQuery cap fixed first, you should be able to install Microsoft.jQuery.Unobtrusive.Validation.</span></span>

### <a name="the-jqueryvalidation-nuget-package-version-1130-does-not-recognize-some-international-email-addresses"></a><span data-ttu-id="c5d3a-156">Jquery 합니다. 유효성 검사 nuget 패키지 버전 1.13.0 일부 국제 전자 메일 주소를 인식 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-156">The jquery.Validation nuget package version 1.13.0 does not recognize some international email addresses</span></span>

<span data-ttu-id="c5d3a-157">1.11.1 jQuery.Validation nuget 패키지 버전에 따라 유효한 전자 메일 주소를 인식 하는 마지막 알려진된 버전이입니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-157">jQuery.Validation nuget package version 1.11.1 is the last known version which recognizes following valid email addresses.</span></span> <span data-ttu-id="c5d3a-158">모든 이후 버전에서 인식할 수 있도록 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-158">Any later versions might not be able to recognize them.</span></span> <span data-ttu-id="c5d3a-159">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="c5d3a-159">For example:</span></span>

<span data-ttu-id="c5d3a-160">전자 메일 주소 국제화 EAI () 표준 (예를 들어 [ &#29992; &#25143; @domain.com ](mailto:&#29992;&#25143;@domain.com))</span><span class="sxs-lookup"><span data-stu-id="c5d3a-160">E-Mail Address Internationalization (EAI) standard (e.g., [&#29992;&#25143;@domain.com](mailto:&#29992;&#25143;@domain.com))</span></span>   
 <span data-ttu-id="c5d3a-161">EAI + 국제 리소스 식별자 (IRIs) (예:., [ &#29992; &#25143;@&#1076;&#1086;&#1084;&#1077;&#1085;.&#1088; &#1092;](mailto:&#29992;&#25143;@&#1076;&#1086;&#1084;&#1077;&#1085;.&#1088;&#1092;))</span><span class="sxs-lookup"><span data-stu-id="c5d3a-161">EAI + Internationalized Resource Identifiers (IRIs) (eg., [&#29992;&#25143;@&#1076;&#1086;&#1084;&#1077;&#1085;.&#1088;&#1092;](mailto:&#29992;&#25143;@&#1076;&#1086;&#1084;&#1077;&#1085;.&#1088;&#1092;))</span></span>

<span data-ttu-id="c5d3a-162">문제에 보고 됩니다. [https://github.com/jzaefferer/jquery-validation/issues/1222](https://github.com/jzaefferer/jquery-validation/issues/1222)</span><span class="sxs-lookup"><span data-stu-id="c5d3a-162">The issue is reported at [https://github.com/jzaefferer/jquery-validation/issues/1222](https://github.com/jzaefferer/jquery-validation/issues/1222)</span></span>

### <a name="syntax-highlighting-for-razor-views-in-visual-studio-2013"></a><span data-ttu-id="c5d3a-163">Visual Studio 2013의 Razor 보기에 대 한 구문 강조 표시</span><span class="sxs-lookup"><span data-stu-id="c5d3a-163">Syntax Highlighting for Razor Views in Visual Studio 2013</span></span>

<span data-ttu-id="c5d3a-164">Visual Studio 2013 업데이트 하지 않고 ASP.NET MVC 5.2를 업데이트 하는 경우 Razor 뷰를 편집 하는 동안 구문 강조 표시에 대 한 Visual Studio 편집기 지원이 제공 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-164">If you update to ASP.NET MVC 5.2 without updating Visual Studio 2013, you will not get Visual Studio editor support for syntax highlighting while editing the Razor views.</span></span> <span data-ttu-id="c5d3a-165">이 지원을 받으려면 Visual Studio 2013 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-165">You will need to update Visual Studio 2013 to get this support.</span></span>

<a id="bug-fixes"></a>
## <a name="bug-fixes-and-minor-feature-updates"></a><span data-ttu-id="c5d3a-166">버그 수정 및 사소한 기능 업데이트</span><span class="sxs-lookup"><span data-stu-id="c5d3a-166">Bug Fixes and Minor feature updates</span></span>

<span data-ttu-id="c5d3a-167">여러 버그 수정 및 사소한 기능에도이 릴리스에서 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-167">This release also includes several bug fixes and minor feature updates.</span></span> <span data-ttu-id="c5d3a-168">여기서 전체 목록을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-168">You can find the complete list here:</span></span>

- [<span data-ttu-id="c5d3a-169">5.2 패키지</span><span class="sxs-lookup"><span data-stu-id="c5d3a-169">5.2 package</span></span>](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2%20RC&amp;assignedTo=All&amp;component=MVC&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=Fixed)

<a id="52"></a>
## <a name="microsoftaspnetmvc-522"></a><span data-ttu-id="c5d3a-170">Microsoft.AspNet.MVC 5.2.2</span><span class="sxs-lookup"><span data-stu-id="c5d3a-170">Microsoft.AspNet.MVC 5.2.2</span></span>

<span data-ttu-id="c5d3a-171">이 릴리스에 MVC의 모든 새로운 기능이 나 버그 수정은 포함 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-171">This release doesn't have any new features or bug fixes in MVC.</span></span> <span data-ttu-id="c5d3a-172">했습니다를 [웹 페이지의 변경 내용](https://blogs.msdn.com/b/webdev/archive/2014/07/28/announcing-the-beta-release-of-web-pages-3-2-1.aspx) 성능이 크게 향상에 대 한 모든 기타 종속 패키지가 웹 페이지의이 새 버전에 따라 달라 집니다 소유한 것 이후에 업데이트.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-172">We made a [change in Web Pages](https://blogs.msdn.com/b/webdev/archive/2014/07/28/announcing-the-beta-release-of-web-pages-3-2-1.aspx) for a significant performance improvement and have subsequently updated all other dependent packages we own to depend on this new version of Web Pages.</span></span>

<a id="mvc523Beta"></a>
## <a name="aspnet-mvc-523-beta"></a><span data-ttu-id="c5d3a-173">ASP.NET MVC 5.2.3 베타</span><span class="sxs-lookup"><span data-stu-id="c5d3a-173">ASP.NET MVC 5.2.3 Beta</span></span>

<span data-ttu-id="c5d3a-174">릴리스에 대 한 읽을 수 있습니다 [여기](https://blogs.msdn.com/b/webdev/archive/2014/12/17/asp-net-mvc-5-2-3-web-pages-5-2-3-and-web-api-5-2-3-beta-releases.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-174">You can read about the release [here](https://blogs.msdn.com/b/webdev/archive/2014/12/17/asp-net-mvc-5-2-3-web-pages-5-2-3-and-web-api-5-2-3-beta-releases.aspx).</span></span> <span data-ttu-id="c5d3a-175">이 릴리스에 버그 수정만 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-175">This release contains only bug fixes.</span></span> <span data-ttu-id="c5d3a-176">사용할 수 있습니다 [이 쿼리](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2.3%20Beta&amp;assignedTo=All&amp;component=MVC&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=Fixed) 이 릴리스에서 해결 된 문제 목록을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5d3a-176">You can use [this query](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2.3%20Beta&amp;assignedTo=All&amp;component=MVC&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=Fixed) to see the list of issues fixed in this release.</span></span>
