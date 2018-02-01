---
uid: mvc/overview/releases/whats-new-in-aspnet-mvc-52
title: "ASP.NET MVC 5.2의에서 새로운 기능 | Microsoft Docs"
author: microsoft
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/25/2014
ms.topic: article
ms.assetid: 97972587-2720-48b4-b158-f35f2e855fbf
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/releases/whats-new-in-aspnet-mvc-52
msc.type: authoredcontent
ms.openlocfilehash: 94f6131fdb86d1694c1f563c5f6806f119c71266
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="whats-new-in-aspnet-mvc-52"></a><span data-ttu-id="c8626-102">ASP.NET MVC 5.2의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="c8626-102">What’s New in ASP.NET MVC 5.2</span></span>
====================
<span data-ttu-id="c8626-103">여 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c8626-103">by [Microsoft](https://github.com/microsoft)</span></span>

<span data-ttu-id="c8626-104">이 항목에서는 ASP.NET MVC 5.2에 대 한 새로운 설명 [Microsoft.AspNet.MVC 5.2.2](#52) 및 [5.2.3 ASP.NET MVC 베타](#mvc523Beta)</span><span class="sxs-lookup"><span data-stu-id="c8626-104">This topic describes what's new for ASP.NET MVC 5.2, [Microsoft.AspNet.MVC 5.2.2](#52) and [ASP.NET MVC 5.2.3 Beta](#mvc523Beta)</span></span>

- [<span data-ttu-id="c8626-105">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="c8626-105">Software Requirements</span></span>](#softRequire)
- [<span data-ttu-id="c8626-106">다운로드</span><span class="sxs-lookup"><span data-stu-id="c8626-106">Download</span></span>](#download)
- [<span data-ttu-id="c8626-107">문서</span><span class="sxs-lookup"><span data-stu-id="c8626-107">Documentation</span></span>](#documentation)
- [<span data-ttu-id="c8626-108">ASP.NET MVC 5.2의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="c8626-108">New Features in ASP.NET MVC 5.2</span></span>](#new-features)

    - [<span data-ttu-id="c8626-109">라우팅 향상 된 기능 특성</span><span class="sxs-lookup"><span data-stu-id="c8626-109">Attribute routing improvements</span></span>](#attributerouting)
- [<span data-ttu-id="c8626-110">알려진된 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="c8626-110">Known Issues and Breaking Changes</span></span>](#knownbreakingchanges)
- [<span data-ttu-id="c8626-111">버그 수정</span><span class="sxs-lookup"><span data-stu-id="c8626-111">Bug Fixes</span></span>](#bug-fixes)
- [<span data-ttu-id="c8626-112">Microsoft.AspNet.MVC 5.2.2</span><span class="sxs-lookup"><span data-stu-id="c8626-112">Microsoft.AspNet.MVC 5.2.2</span></span>](#52)

<a id="softRequire"></a>
## <a name="software-requirements"></a><span data-ttu-id="c8626-113">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="c8626-113">Software Requirements</span></span>

- <span data-ttu-id="c8626-114">Visual Studio 2012: 다운로드 [ASP.NET 및 웹 도구 Visual Studio 2012 용 2013.1](https://go.microsoft.com/fwlink/?LinkId=390062)합니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-114">Visual Studio 2012: Download [ASP.NET and Web Tools 2013.1 for Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkId=390062).</span></span>
- <span data-ttu-id="c8626-115">Visual Studio 2013의 경우: 다운로드 [Visual Studio 2013 업데이트](https://go.microsoft.com/fwlink/?LinkId=390064) 이상.</span><span class="sxs-lookup"><span data-stu-id="c8626-115">Visual Studio 2013: Download [Visual Studio 2013 Update](https://go.microsoft.com/fwlink/?LinkId=390064) or higher.</span></span> <span data-ttu-id="c8626-116">ASP.NET MVC 5.2 Razor 뷰를 편집 하기 위해이 업데이트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-116">This update is needed for editing ASP.NET MVC 5.2 Razor Views.</span></span>

<a id="download"></a>
## <a name="download"></a><span data-ttu-id="c8626-117">다운로드</span><span class="sxs-lookup"><span data-stu-id="c8626-117">Download</span></span>

<span data-ttu-id="c8626-118">런타임 기능은 NuGet 갤러리에서 NuGet 패키지로 해제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-118">The runtime features are released as NuGet packages on the NuGet gallery.</span></span> <span data-ttu-id="c8626-119">모든 런타임 패키지에 따라는 [의미 체계 버전 관리](http://semver.org/) 사양입니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-119">All the runtime packages follow the [Semantic Versioning](http://semver.org/) specification.</span></span> <span data-ttu-id="c8626-120">최신 ASP.NET MVC 5.2 패키지에는 다음 버전: "5.2.0"입니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-120">The latest ASP.NET MVC 5.2 package has the following version: "5.2.0".</span></span> <span data-ttu-id="c8626-121">설치 또는 업데이트를 통해 이러한 패키지 [NuGet](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-121">You can install or update these packages through [NuGet](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/).</span></span> <span data-ttu-id="c8626-122">릴리스에 NuGet에 해당 지역화 된 패키지도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-122">The release also includes corresponding localized packages on NuGet.</span></span>

<span data-ttu-id="c8626-123">설치 하거나 NuGet 패키지 관리자 콘솔을 사용 하 여 출시 된 NuGet 패키지를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-123">You can install or update to the released NuGet packages by using the NuGet Package Manager Console:</span></span>

<span data-ttu-id="c8626-124">Install-package Microsoft.AspNet.Mvc-버전 5.2.0</span><span class="sxs-lookup"><span data-stu-id="c8626-124">Install-Package Microsoft.AspNet.Mvc -Version 5.2.0</span></span>

<a id="documentation"></a>
## <a name="documentation"></a><span data-ttu-id="c8626-125">설명서</span><span class="sxs-lookup"><span data-stu-id="c8626-125">Documentation</span></span>

<span data-ttu-id="c8626-126">ASP.NET 웹 사이트에서 사용할 수 있는 자습서 및 ASP.NET MVC 5.2에 대 한 기타 정보 ([https://www.asp.net/mvc](../../index.md)).</span><span class="sxs-lookup"><span data-stu-id="c8626-126">Tutorials and other information about ASP.NET MVC 5.2 are available from the ASP.NET web site ([https://www.asp.net/mvc](../../index.md)).</span></span>

<a id="new-features"></a>
## <a name="new-features-in-aspnet-mvc-52"></a><span data-ttu-id="c8626-127">ASP.NET MVC 5.2의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="c8626-127">New Features in ASP.NET MVC 5.2</span></span>

<a id="attributerouting"></a>
### <a name="attribute-routing-improvements"></a><span data-ttu-id="c8626-128">라우팅 향상 된 기능 특성</span><span class="sxs-lookup"><span data-stu-id="c8626-128">Attribute routing improvements</span></span>

<span data-ttu-id="c8626-129">특성 라우팅을 이제 호출 IDirectRouteProvider 특성 경로 검색 하 고 구성 하는 방식을 완전히 제어할 수 있는 확장성 지점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-129">Attribute Routing now provides an extensibility point called IDirectRouteProvider, which allows full control over how attribute routes are discovered and configured.</span></span> <span data-ttu-id="c8626-130">IDirectRouteProvider는 이러한 작업에 대 한 어떤 라우팅 구성이 가능 정확 하 게 지정 하려면 연결 된 경로 정보 함께 컨트롤러 및 작업의 목록을 제공 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-130">An IDirectRouteProvider is responsible for providing a list of actions and controllers along with associated route information to specify exactly what routing configuration is desired for those actions.</span></span> <span data-ttu-id="c8626-131">IDirectRouteProvider 구현은 MapAttributes/MapHttpAttributeRoutes를 호출할 때 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-131">An IDirectRouteProvider implementation may be specified when calling MapAttributes/MapHttpAttributeRoutes.</span></span>

<span data-ttu-id="c8626-132">IDirectRouteProvider 사용자 지정의 기본 구현에서는 DefaultDirectRouteProvider를 확장 하 여 가장 쉬운 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-132">Customizing IDirectRouteProvider will be easiest by extending our default implementation, DefaultDirectRouteProvider.</span></span> <span data-ttu-id="c8626-133">이 클래스는 특성 검색 경로 항목을 만들고 경로 접두사와 영역 접두사를 검색 하기 위한 논리를 변경 하는 별도 재정의 가능한 가상 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-133">This class provides separate overridable virtual methods to change the logic for discovering attributes, creating route entries, and discovering route prefix and area prefix.</span></span>

<span data-ttu-id="c8626-134">새 특성 라우팅의 확장성 IDirectRouteProvider와 사용자는 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-134">With the new attribute routing extensibility of IDirectRouteProvider, a user could do the following:</span></span>

1. <span data-ttu-id="c8626-135">특성 경로의 상속을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-135">Support Inheritance of attribute routes.</span></span> <span data-ttu-id="c8626-136">예를 들어 다음 시나리오에서는 BaseController에서 정의한에서 특성 경로 규칙 블로그 및 저장소 컨트롤러에 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-136">For example, in the following scenario Blog and Store controllers are using an attribute route convention that is defined by the BaseController.</span></span> 

    [!code-csharp[Main](whats-new-in-aspnet-mvc-52/samples/sample1.cs)]
2. <span data-ttu-id="c8626-137">특성 경로 대 한 경로 이름을 자동으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-137">Automatically generate route names for attribute routes.</span></span> 

    [!code-csharp[Main](whats-new-in-aspnet-mvc-52/samples/sample2.cs)]
3. <span data-ttu-id="c8626-138">경로 경로 테이블에 추가 하기 전에 단일 중앙 위치에서 경로 접두사를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-138">Modify route prefixes in one central place before the routes get added to the route table.</span></span>
4. <span data-ttu-id="c8626-139">검색할 특성 라우팅을 하려는 컨트롤러를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-139">Filter out the controllers on which you want the attribute routing to look for.</span></span> <span data-ttu-id="c8626-140">바랍니다 3 및 4에는 블로그에 곧.</span><span class="sxs-lookup"><span data-stu-id="c8626-140">We hope to blog on 3 and 4 soon.</span></span>

### <a name="facebook-fixes-for-changed-api-surface"></a><span data-ttu-id="c8626-141">변경 된 API 화면에 대 한 Facebook 수정</span><span class="sxs-lookup"><span data-stu-id="c8626-141">Facebook fixes for changed API surface</span></span>

<span data-ttu-id="c8626-142">MVC Facebook 패키지 [끊어졌습니다](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=v5.2%20RC&amp;assignedTo=All&amp;component=Facebook&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=All) Facebook에서 수행할 몇 가지 API 변경으로 인해 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-142">The MVC Facebook package [was broken](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=v5.2%20RC&amp;assignedTo=All&amp;component=Facebook&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=All) due to few API changes made by Facebook.</span></span> <span data-ttu-id="c8626-143">또한 새 Facebook 패키지 (Microsoft.AspNet.Facebook 1.0.0) 이러한 문제를 해결 하도록 공개 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-143">We are also releasing a new Facebook package (Microsoft.AspNet.Facebook 1.0.0) to fix these issues.</span></span>

<a id="knownbreakingchanges"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="c8626-144">알려진된 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="c8626-144">Known Issues and Breaking Changes</span></span>

### <a name="scaffolding-mvcweb-api-into-a-project-with-520-packages-results-in-512-packages-for-ones-that-dont-already-exist-in-the-project"></a><span data-ttu-id="c8626-145">5.2.0 사용 프로젝트에 스 캐 폴딩 MVC/웹 API 프로젝트에 이미 존재 하지 않는 것에 대 한 패키지 결과 5.1.2에서 패키지</span><span class="sxs-lookup"><span data-stu-id="c8626-145">Scaffolding MVC/Web API into a project with 5.2.0 packages results in 5.1.2 packages for ones that don't already exist in the project</span></span>

<span data-ttu-id="c8626-146">ASP.NET MVC 5.2.0에 대 한 NuGet 패키지를 업데이트 해도 ASP.NET 스 캐 폴딩 같은 Visual Studio 도구 또는 ASP.NET 웹 응용 프로그램 프로젝트 템플릿을 업데이트 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-146">Updating NuGet packages for ASP.NET MVC 5.2.0 does not update the Visual Studio tools such as ASP.NET scaffolding or the ASP.NET Web Application project template.</span></span> <span data-ttu-id="c8626-147">이전 버전의 ASP.NET 런타임 패키지 (예:: Update 2에서 5.1.2) 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-147">They use the previous version of the ASP.NET runtime packages (e.g. 5.1.2 in Update 2).</span></span> <span data-ttu-id="c8626-148">결과적으로, ASP.NET 스 캐 폴딩은 이미 프로젝트에서 사용할 수 없는 경우에 필요한 패키지의 이전 버전 (예:: Update 2에서 5.1.2)으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-148">As a result, the ASP.NET scaffolding will install the previous version (e.g. 5.1.2 in Update 2) of the required packages, if they are not already available in your projects.</span></span> <span data-ttu-id="c8626-149">그러나 Visual Studio 2013 RTM 또는 업데이트 1에서 ASP.NET 스 캐 폴딩을 프로젝트에서 최신 패키지를 덮어쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-149">However, the ASP.NET scaffolding in Visual Studio 2013 RTM or Update 1 does not overwrite the latest packages in your projects.</span></span> <span data-ttu-id="c8626-150">ASP.NET 웹 API 2.2 또는 ASP.NET MVC 5.2로 프로젝트의 패키지를 업데이트 한 후에 스 캐 폴딩을 사용 하는 경우에 버전의 웹 API 및 ASP.NET MVC 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-150">If you use ASP.NET scaffolding after updating the packages of your projects to Web API 2.2 or ASP.NET MVC 5.2, make sure the versions of Web API and ASP.NET MVC are consistent.</span></span>

### <a name="microsoftjqueryunobtrusivevalidation-nuget-package-installation-fails-because-it-is-unable-to-find-a-version-of-microsoftjqueryunobtrusivevalidation-compatible-to-jquery-141"></a><span data-ttu-id="c8626-151">JQuery 1.4.1 호환 Microsoft.jQuery.Unobtrusive.Validation의 버전을 찾을 수 없기 때문에 Microsoft.jQuery.Unobtrusive.Validation NuGet 패키지 설치 실패</span><span class="sxs-lookup"><span data-stu-id="c8626-151">Microsoft.jQuery.Unobtrusive.Validation NuGet package installation fails because it is unable to find a version of Microsoft.jQuery.Unobtrusive.Validation compatible to jQuery 1.4.1</span></span>

<span data-ttu-id="c8626-152">Microsoft.jQuery.Unobtrusive.Validation 필요 jQuery &gt;= 1.8 및 jQuery.Validation &gt;1.8 = 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-152">Microsoft.jQuery.Unobtrusive.Validation requires jQuery &gt;=1.8 and jQuery.Validation &gt;=1.8.</span></span> <span data-ttu-id="c8626-153">(1.8) But,jQuery.Validation jQuery 필요 (&#8805; 1.3.2 &amp; &amp; &#8804;1.6;).</span><span class="sxs-lookup"><span data-stu-id="c8626-153">But,jQuery.Validation (1.8) needs jQuery (&#8805; 1.3.2 &amp;&amp; &#8804; 1.6).</span></span> <span data-ttu-id="c8626-154">이 때문에 NuGet는 JQuery 1.8 및 jQuery.Validation 1.8 같은 시간에 설치 될 때 표시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-154">Because of this, when NuGet installs the JQuery 1.8 and jQuery.Validation 1.8 at the same time, it fails.</span></span> <span data-ttu-id="c8626-155">이 문제를 참조 하는 경우에 jQuery.Validation 버전 단순히 업데이트할 수 있습니다 &gt; =  [1.8.0.1](https://www.nuget.org/packages/jQuery.Validation/1.8.0.1) 고정 jQuery cap가 먼저 있어야를 설치 하려면 Microsoft.jQuery.Unobtrusive.Validation 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-155">When you see this issue, you can simply update the version of jQuery.Validation to &gt;= [1.8.0.1](https://www.nuget.org/packages/jQuery.Validation/1.8.0.1) which has the jQuery cap fixed first, you should be able to install Microsoft.jQuery.Unobtrusive.Validation.</span></span>

### <a name="the-jqueryvalidation-nuget-package-version-1130-does-not-recognize-some-international-email-addresses"></a><span data-ttu-id="c8626-156">Jquery 합니다. 유효성 검사 nuget 패키지 버전 1.13.0 일부 국제 전자 메일 주소를 인식 하지 않으므로</span><span class="sxs-lookup"><span data-stu-id="c8626-156">The jquery.Validation nuget package version 1.13.0 does not recognize some international email addresses</span></span>

<span data-ttu-id="c8626-157">1.11.1 jQuery.Validation nuget 패키지 버전에는 올바른 전자 메일 주소를 다음 인식는 마지막 알려진된 버전이입니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-157">jQuery.Validation nuget package version 1.11.1 is the last known version which recognizes following valid email addresses.</span></span> <span data-ttu-id="c8626-158">모든 이후 버전 인식 하도록 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-158">Any later versions might not be able to recognize them.</span></span> <span data-ttu-id="c8626-159">예:</span><span class="sxs-lookup"><span data-stu-id="c8626-159">For example:</span></span>

<span data-ttu-id="c8626-160">전자 메일 주소 국제화 (EAI) 표준 (예: [&#29992; &#25143;@domain.com ](mailto:&#29992;&#25143;@domain.com))</span><span class="sxs-lookup"><span data-stu-id="c8626-160">E-Mail Address Internationalization (EAI) standard (e.g., [&#29992;&#25143;@domain.com](mailto:&#29992;&#25143;@domain.com))</span></span>   
 <span data-ttu-id="c8626-161">EAI + 국제 리소스 식별자 (Iri) (예:., [&#29992; &#25143; @&#1076; &#1086; &#1084; &#1077; &#1085;. &#1088; &#1092; ](mailto:&#29992;&#25143;@&#1076;&#1086;&#1084;&#1077;&#1085;.&#1088;&#1092;))</span><span class="sxs-lookup"><span data-stu-id="c8626-161">EAI + Internationalized Resource Identifiers (IRIs) (eg., [&#29992;&#25143;@&#1076;&#1086;&#1084;&#1077;&#1085;.&#1088;&#1092;](mailto:&#29992;&#25143;@&#1076;&#1086;&#1084;&#1077;&#1085;.&#1088;&#1092;))</span></span>

<span data-ttu-id="c8626-162">문제가 보고 될 [https://github.com/jzaefferer/jquery-validation/issues/1222](https://github.com/jzaefferer/jquery-validation/issues/1222)</span><span class="sxs-lookup"><span data-stu-id="c8626-162">The issue is reported at [https://github.com/jzaefferer/jquery-validation/issues/1222](https://github.com/jzaefferer/jquery-validation/issues/1222)</span></span>

### <a name="syntax-highlighting-for-razor-views-in-visual-studio-2013"></a><span data-ttu-id="c8626-163">Visual Studio 2013에서 Razor 뷰의 구문 강조 표시</span><span class="sxs-lookup"><span data-stu-id="c8626-163">Syntax Highlighting for Razor Views in Visual Studio 2013</span></span>

<span data-ttu-id="c8626-164">Visual Studio 2013 업데이트 하지 않고 ASP.NET MVC 5.2을 업데이트 하는 경우에 하지 Razor 뷰를 편집 하는 동안 구문 강조 표시에 대 한 Visual Studio 편집기 지원을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-164">If you update to ASP.NET MVC 5.2 without updating Visual Studio 2013, you will not get Visual Studio editor support for syntax highlighting while editing the Razor views.</span></span> <span data-ttu-id="c8626-165">이 지원을 받기 위해 Visual Studio 2013 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-165">You will need to update Visual Studio 2013 to get this support.</span></span>

<a id="bug-fixes"></a>
## <a name="bug-fixes-and-minor-feature-updates"></a><span data-ttu-id="c8626-166">버그 수정 및 사소한 기능 업데이트</span><span class="sxs-lookup"><span data-stu-id="c8626-166">Bug Fixes and Minor feature updates</span></span>

<span data-ttu-id="c8626-167">이 릴리스에 여러 가지 버그 수정 및 사소한 기능에도 기능이 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-167">This release also includes several bug fixes and minor feature updates.</span></span> <span data-ttu-id="c8626-168">전체 목록은 여기를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-168">You can find the complete list here:</span></span>

- [<span data-ttu-id="c8626-169">5.2 패키지</span><span class="sxs-lookup"><span data-stu-id="c8626-169">5.2 package</span></span>](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2%20RC&amp;assignedTo=All&amp;component=MVC&amp;sortField=AssignedTo&amp;sortDirection=Ascending&amp;page=0&amp;reasonClosed=Fixed)

<a id="52"></a>
## <a name="microsoftaspnetmvc-522"></a><span data-ttu-id="c8626-170">Microsoft.AspNet.MVC 5.2.2</span><span class="sxs-lookup"><span data-stu-id="c8626-170">Microsoft.AspNet.MVC 5.2.2</span></span>

<span data-ttu-id="c8626-171">이 릴리스에서 MVC의 모든 새로운 기능 또는 버그 수정 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-171">This release doesn't have any new features or bug fixes in MVC.</span></span> <span data-ttu-id="c8626-172">내렸습니다는 [웹 페이지의 변경 내용](https://blogs.msdn.com/b/webdev/archive/2014/07/28/announcing-the-beta-release-of-web-pages-3-2-1.aspx) 성능이 크게 향상에 대 한 이후에 다른 종속 웹 페이지의이 새로운 버전에 따라 달라 지도록 소유 म 모든 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-172">We made a [change in Web Pages](https://blogs.msdn.com/b/webdev/archive/2014/07/28/announcing-the-beta-release-of-web-pages-3-2-1.aspx) for a significant performance improvement and have subsequently updated all other dependent packages we own to depend on this new version of Web Pages.</span></span>

<a id="mvc523Beta"></a>
## <a name="aspnet-mvc-523-beta"></a><span data-ttu-id="c8626-173">5.2.3 ASP.NET MVC 베타</span><span class="sxs-lookup"><span data-stu-id="c8626-173">ASP.NET MVC 5.2.3 Beta</span></span>

<span data-ttu-id="c8626-174">릴리스에 대 한 읽을 수 [여기](https://blogs.msdn.com/b/webdev/archive/2014/12/17/asp-net-mvc-5-2-3-web-pages-5-2-3-and-web-api-5-2-3-beta-releases.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-174">You can read about the release [here](https://blogs.msdn.com/b/webdev/archive/2014/12/17/asp-net-mvc-5-2-3-web-pages-5-2-3-and-web-api-5-2-3-beta-releases.aspx).</span></span> <span data-ttu-id="c8626-175">이 릴리스에 버그 수정만 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-175">This release contains only bug fixes.</span></span> <span data-ttu-id="c8626-176">사용할 수 있습니다 [이 쿼리](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2.3%20Beta&amp;assignedTo=All&amp;component=MVC&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=Fixed) 이 릴리스에서 수정 된 문제 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8626-176">You can use [this query](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2.3%20Beta&amp;assignedTo=All&amp;component=MVC&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=Fixed) to see the list of issues fixed in this release.</span></span>
