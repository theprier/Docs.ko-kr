---
uid: whitepapers/aspnet4/overview
title: ASP.NET 4 및 Visual Studio 2010 웹 개발 개요 | Microsoft Docs
author: rick-anderson
description: 이 문서는.net Framework 4 및 Visual Studio 2010에 포함 된 ASP.NET에 대 한 다양 한 새 기능에 대 한 개요를 제공 합니다.
ms.author: riande
ms.date: 02/10/2010
ms.assetid: d7729af4-1eda-4ff2-8b61-dbbe4fc11d10
msc.legacyurl: /whitepapers/aspnet4
msc.type: content
ms.openlocfilehash: 775286df610df9040cbf04125b1742b6befa055b
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828668"
---
<a name="aspnet-4-and-visual-studio-2010-web-development-overview"></a><span data-ttu-id="3e862-103">ASP.NET 4 및 Visual Studio 2010 웹 개발 개요</span><span class="sxs-lookup"><span data-stu-id="3e862-103">ASP.NET 4 and Visual Studio 2010 Web Development Overview</span></span>
====================
> <span data-ttu-id="3e862-104">이 문서는.net Framework 4 및 Visual Studio 2010에 포함 된 ASP.NET에 대 한 다양 한 새 기능에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-104">This document provides an overview of many of the new features for ASP.NET that are included in the.NET Framework 4 and in Visual Studio 2010.</span></span>
> 
> [<span data-ttu-id="3e862-105">이 백서를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-105">Download This Whitepaper</span></span>](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_and_Visual_Studio_2010_Web_Development_Overview.pdf)


<span data-ttu-id="3e862-106">**목차**</span><span class="sxs-lookup"><span data-stu-id="3e862-106">**Contents**</span></span>

<span data-ttu-id="3e862-107">**[Core Services](#0.2__Toc253429238 "_Toc253429238")**</span><span class="sxs-lookup"><span data-stu-id="3e862-107">**[Core Services](#0.2__Toc253429238 "_Toc253429238")**</span></span>  
[<span data-ttu-id="3e862-108">Web.config 파일을 리팩터링</span><span class="sxs-lookup"><span data-stu-id="3e862-108">Web.config File Refactoring</span></span>](#0.2__Toc253429239 "_Toc253429239")  
[<span data-ttu-id="3e862-109">확장 가능한 출력 캐싱</span><span class="sxs-lookup"><span data-stu-id="3e862-109">Extensible Output Caching</span></span>](#0.2__Toc253429240 "_Toc253429240")  
[<span data-ttu-id="3e862-110">웹 응용 프로그램을 자동으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-110">Auto-Start Web Applications</span></span>](#0.2__Toc253429241 "_Toc253429241")  
[<span data-ttu-id="3e862-111">페이지를 영구적으로 리디렉션</span><span class="sxs-lookup"><span data-stu-id="3e862-111">Permanently Redirecting a Page</span></span>](#0.2__Toc253429242 "_Toc253429242")  
[<span data-ttu-id="3e862-112">세션 상태를 축소</span><span class="sxs-lookup"><span data-stu-id="3e862-112">Shrinking Session State</span></span>](#0.2__Toc253429243 "_Toc253429243")  
[<span data-ttu-id="3e862-113">허용 되는 Url의 범위를 확장</span><span class="sxs-lookup"><span data-stu-id="3e862-113">Expanding the Range of Allowable URLs</span></span>](#0.2__Toc253429244 "_Toc253429244")  
[<span data-ttu-id="3e862-114">확장 가능한 요청 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="3e862-114">Extensible Request Validation</span></span>](#0.2__Toc253429245 "_Toc253429245")  
[<span data-ttu-id="3e862-115">개체 캐싱 및 캐싱 확장성 개체</span><span class="sxs-lookup"><span data-stu-id="3e862-115">Object Caching and Object Caching Extensibility</span></span>](#0.2__Toc253429246 "_Toc253429246")  
[<span data-ttu-id="3e862-116">확장 가능한 HTML, URL 및 HTTP 헤더 인코딩을</span><span class="sxs-lookup"><span data-stu-id="3e862-116">Extensible HTML, URL, and HTTP Header Encoding</span></span>](#0.2__Toc253429247 "_Toc253429247")  
[<span data-ttu-id="3e862-117">단일 작업자 프로세스에서 개별 응용 프로그램 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="3e862-117">Performance Monitoring for Individual Applications in a Single Worker Process</span></span>](#0.2__Toc253429248 "_Toc253429248")  
[<span data-ttu-id="3e862-118">멀티 타기 팅</span><span class="sxs-lookup"><span data-stu-id="3e862-118">Multi-Targeting</span></span>](#0.2__Toc253429249 "_Toc253429249")

<span data-ttu-id="3e862-119">**[Ajax](#0.2__Toc253429250 "_Toc253429250")**</span><span class="sxs-lookup"><span data-stu-id="3e862-119">**[Ajax](#0.2__Toc253429250 "_Toc253429250")**</span></span>  
[<span data-ttu-id="3e862-120">Web Forms 및 MVC를 사용 하 여 포함 된 jQuery</span><span class="sxs-lookup"><span data-stu-id="3e862-120">jQuery Included with Web Forms and MVC</span></span>](#0.2__Toc253429251 "_Toc253429251")  
[<span data-ttu-id="3e862-121">콘텐츠 배달 네트워크 지원</span><span class="sxs-lookup"><span data-stu-id="3e862-121">Content Delivery Network Support</span></span>](#0.2__Toc253429252 "_Toc253429252")  
[<span data-ttu-id="3e862-122">명시적 스크립트 ScriptManager</span><span class="sxs-lookup"><span data-stu-id="3e862-122">ScriptManager Explicit Scripts</span></span>](#0.2__Toc253429253 "_Toc253429253")

<span data-ttu-id="3e862-123">**[Web Forms](#0.2__Toc253429256 "_Toc253429256")**</span><span class="sxs-lookup"><span data-stu-id="3e862-123">**[Web Forms](#0.2__Toc253429256 "_Toc253429256")**</span></span>  
[<span data-ttu-id="3e862-124">Page.MetaKeywords 및 Page.MetaDescription 속성을 사용 하 여 메타 태그를 설정</span><span class="sxs-lookup"><span data-stu-id="3e862-124">Setting Meta Tags with the Page.MetaKeywords and Page.MetaDescription Properties</span></span>](#0.2__Toc253429257 "_Toc253429257")  
[<span data-ttu-id="3e862-125">개별 컨트롤의 뷰 상태를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="3e862-125">Enabling View State for Individual Controls</span></span>](#0.2__Toc253429258 "_Toc253429258")  
[<span data-ttu-id="3e862-126">브라우저 기능 변경 내용</span><span class="sxs-lookup"><span data-stu-id="3e862-126">Changes to Browser Capabilities</span></span>](#0.2__Toc253429259 "_Toc253429259")  
[<span data-ttu-id="3e862-127">ASP.NET 4에서에서 라우팅</span><span class="sxs-lookup"><span data-stu-id="3e862-127">Routing in ASP.NET 4</span></span>](#0.2__Toc253429260 "_Toc253429260")  
[<span data-ttu-id="3e862-128">클라이언트 Id를 설정한</span><span class="sxs-lookup"><span data-stu-id="3e862-128">Setting Client IDs</span></span>](#0.2__Toc253429261 "_Toc253429261")  
[<span data-ttu-id="3e862-129">데이터 컨트롤에서 행 선택 보관</span><span class="sxs-lookup"><span data-stu-id="3e862-129">Persisting Row Selection in Data Controls</span></span>](#0.2__Toc253429262 "_Toc253429262")  
[<span data-ttu-id="3e862-130">ASP.NET 차트 컨트롤</span><span class="sxs-lookup"><span data-stu-id="3e862-130">ASP.NET Chart Control</span></span>](#0.2__Toc253429263 "_Toc253429263")  
[<span data-ttu-id="3e862-131">QueryExtender 컨트롤을 사용 하 여 데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="3e862-131">Filtering Data with the QueryExtender Control</span></span>](#0.2__Toc253429264 "_Toc253429264")  
[<span data-ttu-id="3e862-132">Html 인코딩된 코드 식을</span><span class="sxs-lookup"><span data-stu-id="3e862-132">Html Encoded Code Expressions</span></span>](#0.2__Toc253429265 "_Toc253429265")  
[<span data-ttu-id="3e862-133">프로젝트 템플릿 변경</span><span class="sxs-lookup"><span data-stu-id="3e862-133">Project Template Changes</span></span>](#0.2__Toc253429266 "_Toc253429266")  
[<span data-ttu-id="3e862-134">CSS 개선</span><span class="sxs-lookup"><span data-stu-id="3e862-134">CSS Improvements</span></span>](#0.2__Toc253429267 "_Toc253429267")  
[<span data-ttu-id="3e862-135">Div 숨겨진 필드 주위 요소 숨기기</span><span class="sxs-lookup"><span data-stu-id="3e862-135">Hiding div Elements Around Hidden Fields</span></span>](#0.2__Toc253429268 "_Toc253429268")  
[<span data-ttu-id="3e862-136">템플릿 기반 컨트롤에 대 한 외부 테이블을 렌더링</span><span class="sxs-lookup"><span data-stu-id="3e862-136">Rendering an Outer Table for Templated Controls</span></span>](#0.2__Toc253429269 "_Toc253429269")  
[<span data-ttu-id="3e862-137">향상 된 ListView 컨트롤</span><span class="sxs-lookup"><span data-stu-id="3e862-137">ListView Control Enhancements</span></span>](#0.2__Toc253429270 "_Toc253429270")  
[<span data-ttu-id="3e862-138">CheckBoxList 및 RadioButtonList 컨트롤 향상</span><span class="sxs-lookup"><span data-stu-id="3e862-138">CheckBoxList and RadioButtonList Control Enhancements</span></span>](#0.2__Toc253429271 "_Toc253429271")  
[<span data-ttu-id="3e862-139">메뉴 컨트롤 개선</span><span class="sxs-lookup"><span data-stu-id="3e862-139">Menu Control Improvements</span></span>](#0.2__Toc253429272 "_Toc253429272")  
[<span data-ttu-id="3e862-140">마법사 및 CreateUserWizard 컨트롤 56</span><span class="sxs-lookup"><span data-stu-id="3e862-140">Wizard and CreateUserWizard Controls 56</span></span>](#0.2__Toc253429273 "_Toc253429273")

<span data-ttu-id="3e862-141">**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**</span><span class="sxs-lookup"><span data-stu-id="3e862-141">**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**</span></span>  
[<span data-ttu-id="3e862-142">영역 지원을</span><span class="sxs-lookup"><span data-stu-id="3e862-142">Areas Support</span></span>](#0.2__Toc253429275 "_Toc253429275")  
[<span data-ttu-id="3e862-143">데이터 주석 특성 유효성 검사 지원을</span><span class="sxs-lookup"><span data-stu-id="3e862-143">Data-Annotation Attribute Validation Support</span></span>](#0.2__Toc253429276 "_Toc253429276")  
[<span data-ttu-id="3e862-144">템플릿 기반 도우미</span><span class="sxs-lookup"><span data-stu-id="3e862-144">Templated Helpers</span></span>](#0.2__Toc253429277 "_Toc253429277")

<span data-ttu-id="3e862-145">**[Dynamic Data](#0.2__Toc253429278 "_Toc253429278")**</span><span class="sxs-lookup"><span data-stu-id="3e862-145">**[Dynamic Data](#0.2__Toc253429278 "_Toc253429278")**</span></span>  
[<span data-ttu-id="3e862-146">기존 프로젝트에 대 한 동적 데이터를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="3e862-146">Enabling Dynamic Data for Existing Projects</span></span>](#0.2__Toc253429279 "_Toc253429279")  
[<span data-ttu-id="3e862-147">DynamicDataManager 컨트롤 선언 구문</span><span class="sxs-lookup"><span data-stu-id="3e862-147">Declarative DynamicDataManager Control Syntax</span></span>](#0.2__Toc253429280 "_Toc253429280")  
[<span data-ttu-id="3e862-148">엔터티 템플릿이</span><span class="sxs-lookup"><span data-stu-id="3e862-148">Entity Templates</span></span>](#0.2__Toc253429281 "_Toc253429281")  
[<span data-ttu-id="3e862-149">Url 및 전자 메일 주소에 대 한 새 필드 템플릿을</span><span class="sxs-lookup"><span data-stu-id="3e862-149">New Field Templates for URLs and E-mail Addresses</span></span>](#0.2__Toc253429282 "_Toc253429282")  
[<span data-ttu-id="3e862-150">DynamicHyperLink 컨트롤을 사용 하 여 링크를 만드는</span><span class="sxs-lookup"><span data-stu-id="3e862-150">Creating Links with the DynamicHyperLink Control</span></span>](#0.2__Toc253429283 "_Toc253429283")  
[<span data-ttu-id="3e862-151">데이터 모델의 상속에 대 한 지원을</span><span class="sxs-lookup"><span data-stu-id="3e862-151">Support for Inheritance in the Data Model</span></span>](#0.2__Toc253429284 "_Toc253429284")  
[<span data-ttu-id="3e862-152">다 대 다 관계 (Entity Framework에만 해당)에 대 한 지원을</span><span class="sxs-lookup"><span data-stu-id="3e862-152">Support for Many-to-Many Relationships (Entity Framework Only)</span></span>](#0.2__Toc253429285 "_Toc253429285")  
[<span data-ttu-id="3e862-153">컨트롤 표시 및 지원 열거형에 새 특성</span><span class="sxs-lookup"><span data-stu-id="3e862-153">New Attributes to Control Display and Support Enumerations</span></span>](#0.2__Toc253429286 "_Toc253429286")  
[<span data-ttu-id="3e862-154">필터에 대 한 지원이 향상 되었습니다</span><span class="sxs-lookup"><span data-stu-id="3e862-154">Enhanced Support for Filters</span></span>](#0.2__Toc253429287 "_Toc253429287")

<span data-ttu-id="3e862-155">**[Visual Studio 2010 웹 개발 개선](#0.2__Toc253429288 "_Toc253429288")**</span><span class="sxs-lookup"><span data-stu-id="3e862-155">**[Visual Studio 2010 Web Development Improvements](#0.2__Toc253429288 "_Toc253429288")**</span></span>  
[<span data-ttu-id="3e862-156">CSS 호환성 향상</span><span class="sxs-lookup"><span data-stu-id="3e862-156">Improved CSS Compatibility</span></span>](#0.2__Toc253429289 "_Toc253429289")  
[<span data-ttu-id="3e862-157">HTML 및 JavaScript 조각</span><span class="sxs-lookup"><span data-stu-id="3e862-157">HTML and JavaScript Snippets</span></span>](#0.2__Toc253429290 "_Toc253429290")  
[<span data-ttu-id="3e862-158">JavaScript IntelliSense 향상</span><span class="sxs-lookup"><span data-stu-id="3e862-158">JavaScript IntelliSense Enhancements</span></span>](#0.2__Toc253429291 "_Toc253429291")

<span data-ttu-id="3e862-159">**[Visual Studio 2010을 사용 하 여 응용 프로그램 배포 웹](#0.2__Toc253429292 "_Toc253429292")**</span><span class="sxs-lookup"><span data-stu-id="3e862-159">**[Web Application Deployment with Visual Studio 2010](#0.2__Toc253429292 "_Toc253429292")**</span></span>  
[<span data-ttu-id="3e862-160">웹 패키징</span><span class="sxs-lookup"><span data-stu-id="3e862-160">Web Packaging</span></span>](#0.2__Toc253429293 "_Toc253429293")  
[<span data-ttu-id="3e862-161">Web.config 변환</span><span class="sxs-lookup"><span data-stu-id="3e862-161">Web.config Transformation</span></span>](#0.2__Toc253429294 "_Toc253429294")  
[<span data-ttu-id="3e862-162">데이터베이스 배포</span><span class="sxs-lookup"><span data-stu-id="3e862-162">Database Deployment</span></span>](#0.2__Toc253429295 "_Toc253429295")  
[<span data-ttu-id="3e862-163">웹 응용 프로그램에 대 한 One-click 게시</span><span class="sxs-lookup"><span data-stu-id="3e862-163">One-Click Publish for Web Applications</span></span>](#0.2__Toc253429296 "_Toc253429296")  
[<span data-ttu-id="3e862-164">Resources</span><span class="sxs-lookup"><span data-stu-id="3e862-164">Resources</span></span>](#0.2__Toc253429297 "_Toc253429297")

<span data-ttu-id="3e862-165">**[Disclaimer](#0.2__Toc253429298 "_Toc253429298")**</span><span class="sxs-lookup"><span data-stu-id="3e862-165">**[Disclaimer](#0.2__Toc253429298 "_Toc253429298")**</span></span>

<a id="0.2__Toc224729018"></a><a id="0.2__Toc253429238"></a><a id="0.2__Toc243304612"></a>

## <a name="core-services"></a><span data-ttu-id="3e862-166">핵심 서비스</span><span class="sxs-lookup"><span data-stu-id="3e862-166">Core Services</span></span>

<span data-ttu-id="3e862-167">ASP.NET 4에는 다양을 한 출력 캐싱 및 세션 상태 저장소와 같은 핵심 ASP.NET 서비스를 개선 하는 기능이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-167">ASP.NET 4 introduces a number of features that improve core ASP.NET services such as output caching and session-state storage.</span></span>

<a id="0.2__Toc243304613"></a><a id="0.2__Toc253429239"></a><a id="0.2__Toc224729019"></a>

### <a name="webconfig-file-refactoring"></a><span data-ttu-id="3e862-168">리팩터링 하는 Web.config 파일</span><span class="sxs-lookup"><span data-stu-id="3e862-168">Web.config File Refactoring</span></span>

<span data-ttu-id="3e862-169">`Web.config` 웹 응용 프로그램의 규모가 상당히 지난 몇 가지 릴리스의.NET Framework를 통해 새 기능이 추가 되었습니다, Ajax와 같은 때에 대 한 구성이 포함 된 파일, 라우팅 및 IIS 7과 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-169">The `Web.config` file that contains the configuration for a Web application has grown considerably over the past few releases of the .NET Framework as new features have been added, such as Ajax, routing, and integration with IIS 7.</span></span> <span data-ttu-id="3e862-170">구성에 Visual Studio와 같은 도구 없이 새 웹 응용 프로그램을 시작 하기가 어려웠습니다에이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-170">This has made it harder to configure or start new Web applications without a tool like Visual Studio.</span></span> <span data-ttu-id="3e862-171">이.NET Framework 4의 주요 구성 요소를 이동 되었습니다는 `machine.config` 파일 및 응용 프로그램을 이제 이러한 설정을 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-171">In .the NET Framework 4, the major configuration elements have been moved to the `machine.config` file, and applications now inherit these settings.</span></span> <span data-ttu-id="3e862-172">따라서는 `Web.config` 비워 또는 Visual Studio에 대 한 응용 프로그램을 대상으로 하는 프레임 워크의 버전을 지정 하는 다음 줄만 포함 하도록 ASP.NET 4 응용 프로그램에서 파일:</span><span class="sxs-lookup"><span data-stu-id="3e862-172">This allows the `Web.config` file in ASP.NET 4 applications either to be empty or to contain just the following lines, which specify for Visual Studio what version of the framework the application is targeting:</span></span>

[!code-xml[Main](overview/samples/sample1.xml)]

<a id="0.2__Toc253429240"></a><a id="0.2__Toc243304614"></a>

### <a name="extensible-output-caching"></a><span data-ttu-id="3e862-173">확장 가능한 출력 캐싱</span><span class="sxs-lookup"><span data-stu-id="3e862-173">Extensible Output Caching</span></span>

<span data-ttu-id="3e862-174">ASP.NET 1.0 출시 된 이후로 출력 캐싱을 개발자가 메모리에서 페이지, 컨트롤 및 HTTP 응답의 생성된 된 출력을 저장할 수 있게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-174">Since the time that ASP.NET 1.0 was released, output caching has enabled developers to store the generated output of pages, controls, and HTTP responses in memory.</span></span> <span data-ttu-id="3e862-175">후속 웹 요청에 대해 ASP.NET 수 콘텐츠를 제공 보다 신속 하 게부터 출력을 다시 생성 하지 않고 메모리에서 생성된 된 출력을 검색 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-175">On subsequent Web requests, ASP.NET can serve content more quickly by retrieving the generated output from memory instead of regenerating the output from scratch.</span></span> <span data-ttu-id="3e862-176">그러나이 방법은 제한이-생성 되는 콘텐츠는 항상 메모리에 저장 해야 하 고 출력 캐싱을 사용 된 메모리 사용량이 발생 하는 서버에서 웹 응용 프로그램의 다른 부분에서 메모리 요구량을 사용 하 여 경쟁할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-176">However, this approach has a limitation — generated content always has to be stored in memory, and on servers that are experiencing heavy traffic, the memory consumed by output caching can compete with memory demands from other portions of a Web application.</span></span>

<span data-ttu-id="3e862-177">ASP.NET 4에는 하나 이상의 사용자 지정 출력 캐시 공급자를 구성할 수 있도록 출력 캐싱에 확장성 지점을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-177">ASP.NET 4 adds an extensibility point to output caching that enables you to configure one or more custom output-cache providers.</span></span> <span data-ttu-id="3e862-178">출력 캐시 공급자 모든 저장소 메커니즘을 사용 하 여 HTML 콘텐츠를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-178">Output-cache providers can use any storage mechanism to persist HTML content.</span></span> <span data-ttu-id="3e862-179">이 수 로컬 또는 원격 디스크를 포함 하는 다양 한 지 속성 메커니즘, 클라우드 저장소에 대 한 사용자 지정 출력 캐시 공급자를 만들 수 있도록 하 고 캐시 엔진을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-179">This makes it possible to create custom output-cache providers for diverse persistence mechanisms, which can include local or remote disks, cloud storage, and distributed cache engines.</span></span>

<span data-ttu-id="3e862-180">새에서 파생 된 클래스로 사용자 지정 출력 캐시 공급자를 만들면 *System.Web.Caching.OutputCacheProvider* 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-180">You create a custom output-cache provider as a class that derives from the new *System.Web.Caching.OutputCacheProvider* type.</span></span> <span data-ttu-id="3e862-181">공급자를 구성할 수 있습니다는 `Web.config` 새을 사용 하 여 파일 *공급자* 하위 섹션은 *outputCache* 요소를 다음 예제에서와 같이:</span><span class="sxs-lookup"><span data-stu-id="3e862-181">You can then configure the provider in the `Web.config` file by using the new *providers* subsection of the *outputCache* element, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample2.xml)]

<span data-ttu-id="3e862-182">ASP.NET 4에서 모든 HTTP 응답에는 기본적으로 렌더링 된 페이지 및 컨트롤 앞의 예에서 같이 메모리에 출력 캐시를 사용 하 여 위치를 *defaultProvider* 특성 AspNetInternalProvider로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-182">By default in ASP.NET 4, all HTTP responses, rendered pages, and controls use the in-memory output cache, as shown in the previous example, where the *defaultProvider* attribute is set to AspNetInternalProvider.</span></span> <span data-ttu-id="3e862-183">다른 공급자 이름을 지정 하 여 웹 응용 프로그램에 대 한 사용 하는 기본 출력 캐시 공급자를 변경할 수 있습니다 *defaultProvider*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-183">You can change the default output-cache provider used for a Web application by specifying a different provider name for *defaultProvider*.</span></span>

<span data-ttu-id="3e862-184">또한 컨트롤 및 요청에 따라 다양 한 출력 캐시 공급자를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-184">In addition, you can select different output-cache providers per control and per request.</span></span> <span data-ttu-id="3e862-185">다른 웹 사용자 컨트롤에 대 한 다양 한 출력 캐시 공급자를 선택 하는 가장 쉬운 방법은 new를 사용 하 여 선언적으로 작업을 수행 하는 것 *providerName* 제어 지시문을 다음 예제에서와 같이 특성:</span><span class="sxs-lookup"><span data-stu-id="3e862-185">The easiest way to choose a different output-cache provider for different Web user controls is to do so declaratively by using the new *providerName* attribute in a control directive, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample3.aspx)]

<span data-ttu-id="3e862-186">HTTP 요청에 대 한 다양 한 출력 캐시 공급자를 지정 하는 좀 더 많은 작업이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-186">Specifying a different output cache provider for an HTTP request requires a little more work.</span></span> <span data-ttu-id="3e862-187">새 재정의 공급자를 선언적으로 지정 하는 대신 *GetOuputCacheProviderName* 에서 메서드를 `Global.asax` 파일을 프로그래밍 방식으로 특정 요청에 사용할 공급자를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-187">Instead of declaratively specifying the provider, you override the new *GetOuputCacheProviderName* method in the `Global.asax` file to programmatically specify which provider to use for a specific request.</span></span> <span data-ttu-id="3e862-188">다음 예제에서는 이 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-188">The following example shows how to do this.</span></span>

[!code-csharp[Main](overview/samples/sample4.cs)]

<span data-ttu-id="3e862-189">ASP.NET 4에 출력 캐시 공급자 확장을 추가 하 여 지금 웹 사이트에 대 한 더욱 강력 하 고 더 지능적인 출력 캐싱 전략을 추진할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-189">With the addition of output-cache provider extensibility to ASP.NET 4, you can now pursue more aggressive and more intelligent output-caching strategies for your Web sites.</span></span> <span data-ttu-id="3e862-190">예를 들어, 페이지를 디스크에 낮은 트래픽을 받는 캐시 하는 동안 메모리에서 사이트의 "상위 10 개의" 페이지를 캐시할 수 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-190">For example, it is now possible to cache the "Top 10" pages of a site in memory, while caching pages that get lower traffic on disk.</span></span> <span data-ttu-id="3e862-191">또는 모든에서 다를 조합, 렌더링된 된 페이지에 대 한 캐시 수 있지만 메모리 사용량은 프런트 엔드 웹 서버에서 오프 로드 된 있도록 분산된 캐시를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-191">Alternatively, you can cache every vary-by combination for a rendered page, but use a distributed cache so that the memory consumption is offloaded from front-end Web servers.</span></span>

<a id="0.2__Toc224729020"></a><a id="0.2__Toc253429241"></a><a id="0.2__Toc243304615"></a>

### <a name="auto-start-web-applications"></a><span data-ttu-id="3e862-192">웹 응용 프로그램을 자동으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-192">Auto-Start Web Applications</span></span>

<span data-ttu-id="3e862-193">일부 웹 응용 프로그램은 많은 양의 데이터를 로드 하거나 첫 번째 요청을 처리 하기 전에 처리 하는 비용이 많이 드는 초기화를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-193">Some Web applications need to load large amounts of data or perform expensive initialization processing before serving the first request.</span></span> <span data-ttu-id="3e862-194">"절전" ASP.NET 응용 프로그램 및 다음 중 초기화 코드를 실행 하는 사용자 지정 방법으로 고안 했습니다 이러한 상황에 대 한 ASP.NET의 이전 버전에서의 *응용 프로그램\_부하* 의 메서드를 `Global.asax` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-194">In earlier versions of ASP.NET, for these situations you had to devise custom approaches to "wake up" an ASP.NET application and then run initialization code during the *Application\_Load* method in the `Global.asax` file.</span></span>

<span data-ttu-id="3e862-195">라는 새로운 확장성 기능 *자동 시작* 직접 주소가이 시나리오는 사용 가능한 경우 ASP.NET 4에서 실행 되도록 Windows Server 2008 R2에서 IIS 7.5입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-195">A new scalability feature named *auto-start* that directly addresses this scenario is available when ASP.NET 4 runs on IIS 7.5 on Windows Server 2008 R2.</span></span> <span data-ttu-id="3e862-196">자동 시작 기능에는 응용 프로그램 풀을 시작, ASP.NET 응용 프로그램을 초기화 한 다음 HTTP 요청을 받아들이기 위한 제어 되는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-196">The auto-start feature provides a controlled approach for starting up an application pool, initializing an ASP.NET application, and then accepting HTTP requests.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="3e862-197">IIS 7.5 용 IIS 응용 프로그램 준비 모듈</span><span class="sxs-lookup"><span data-stu-id="3e862-197">IIS Application Warm-Up Module for IIS 7.5</span></span>
> 
> <span data-ttu-id="3e862-198">IIS 팀 IIS 7.5 용 응용 프로그램 준비 모듈의 첫 번째 베타 테스트 버전을 출시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-198">The IIS team has released the first beta test version of the Application Warm-Up Module for IIS 7.5.</span></span> <span data-ttu-id="3e862-199">이렇게 하면 앞에서 설명한 것 보다 쉽게 응용 프로그램을 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-199">This makes warming up your applications even easier than previously described.</span></span> <span data-ttu-id="3e862-200">사용자 지정 코드를 작성 하는 대신 웹 응용 프로그램 네트워크의 요청을 수락 하기 전에 실행 리소스의 Url에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-200">Instead of writing custom code, you specify the URLs of resources to execute before the Web application accepts requests from the network.</span></span> <span data-ttu-id="3e862-201">IIS 서비스의 시작 하는 동안 발생이 준비 (IIS 응용 프로그램 풀을 구성 하는 경우 *AlwaysRunning*) 하 고 IIS 작업자 프로세스를 재활용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3e862-201">This warm-up occurs during startup of the IIS service (if you configured the IIS application pool as *AlwaysRunning*) and when an IIS worker process recycles.</span></span> <span data-ttu-id="3e862-202">이전 IIS 작업자 프로세스 재활용, 하는 동안 응용 프로그램 환경을 방해 하지 또는 다른 문제로 인해 unprimed 캐시를 새로 생성 된 작업자 프로세스를 완벽 하 게 준비 될 때까지 요청을 실행 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-202">During recycle, the old IIS worker process continues to execute requests until the newly spawned worker process is fully warmed up, so that applications experience no interruptions or other issues due to unprimed caches.</span></span> <span data-ttu-id="3e862-203">이 모듈 버전 2.0부터 ASP.NET의 모든 버전을 사용 하 여 작동 하는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-203">Note that this module works with any version of ASP.NET, starting with version 2.0.</span></span>
> 
> <span data-ttu-id="3e862-204">자세한 내용은 [응용 프로그램 웜 업을](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net) IIS.net 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-204">For more information, see [Application Warm-Up](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net) on the IIS.net Web site.</span></span> <span data-ttu-id="3e862-205">준비 기능을 사용 하는 방법을 보여 주는 연습을 참조 하세요 [Getting Started with IIS 7.5 응용 프로그램 준비 모듈](https://www.iis.net/learn/manage) IIS.net 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-205">For a walkthrough that illustrates how to use the warm-up feature, see [Getting Started with the IIS 7.5 Application Warm-Up Module](https://www.iis.net/learn/manage) on the IIS.net Web site.</span></span>


<span data-ttu-id="3e862-206">자동 시작 기능을 사용 하려면 IIS 관리자에서 다음 구성을 사용 하 여 자동으로 시작 되도록 IIS 7.5에서 응용 프로그램 풀을 설정 합니다 `applicationHost.config` 파일:</span><span class="sxs-lookup"><span data-stu-id="3e862-206">To use the auto-start feature, an IIS administrator sets an application pool in IIS 7.5 to be automatically started by using the following configuration in the `applicationHost.config` file:</span></span>

[!code-xml[Main](overview/samples/sample5.xml)]

<span data-ttu-id="3e862-207">개별 응용 프로그램에서 다음 구성을 사용 하 여 자동으로 시작 되도록 지정 하는 단일 응용 프로그램 풀에서 여러 응용 프로그램을 포함할 수 있으므로 `applicationHost.config` 파일:</span><span class="sxs-lookup"><span data-stu-id="3e862-207">Because a single application pool can contain multiple applications, you specify individual applications to be automatically started by using the following configuration in the `applicationHost.config` file:</span></span>

[!code-xml[Main](overview/samples/sample6.xml)]

<span data-ttu-id="3e862-208">IIS 7.5에서 정보를 사용 하는 경우 IIS 7.5 server가 콜드 시작 또는 개별 응용 프로그램 풀 재활용 될 때를 `applicationHost.config` 파일을 자동으로 시작 하는 웹 응용 프로그램 요구를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-208">When an IIS 7.5 server is cold-started or when an individual application pool is recycled, IIS 7.5 uses the information in the `applicationHost.config` file to determine which Web applications need to be automatically started.</span></span> <span data-ttu-id="3e862-209">IIS7.5 자동 시작 되도록 표시 된 각 응용 프로그램에 대 한 HTTP 요청 하는 동안 응용 프로그램이 일시적으로 받아들이지 않는 상태의 응용 프로그램을 시작 하려면 ASP.NET 4로 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-209">For each application that is marked for auto-start, IIS7.5 sends a request to ASP.NET 4 to start the application in a state during which the application temporarily does not accept HTTP requests.</span></span> <span data-ttu-id="3e862-210">ASP.NET에서 정의 된 형식을 인스턴스화하이 상태의 경우 합니다 *serviceAutoStartProvider* (이전 예제에 표시) 된 특성 및 해당 공용 진입점으로 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-210">When it is in this state, ASP.NET instantiates the type defined by the *serviceAutoStartProvider* attribute (as shown in the previous example) and calls into its public entry point.</span></span>

<span data-ttu-id="3e862-211">구현 하 여 필요한 진입점을 사용 하 여 관리 되는 자동으로 시작 형식을 만들 합니다 *IProcessHostPreloadClient* 다음 예제에서와 같이 인터페이스:</span><span class="sxs-lookup"><span data-stu-id="3e862-211">You create a managed auto-start type with the necessary entry point by implementing the *IProcessHostPreloadClient* interface, as shown in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample7.cs)]

<span data-ttu-id="3e862-212">초기화 후 코드에서 실행 합니다 *미리 로드* 메서드 및 메서드는 반환 ASP.NET 응용 프로그램 요청을 처리할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-212">After your initialization code runs in the *Preload* method and the method returns, the ASP.NET application is ready to process requests.</span></span>

<span data-ttu-id="3e862-213">.5 IIS 및 ASP.NET 4 자동 시작을 추가 하 여 이제 첫 번째 HTTP 요청을 처리 하기 전에 비용이 많이 드는 응용 프로그램 초기화를 수행 하기 위한 잘 정의 된 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-213">With the addition of auto-start to IIS .5 and ASP.NET 4, you now have a well-defined approach for performing expensive application initialization prior to processing the first HTTP request.</span></span> <span data-ttu-id="3e862-214">예를 들어, 응용 프로그램을 초기화 하 고 응용 프로그램 초기화 되었고 HTTP 트래픽을 허용 하도록 준비 하는 부하 분산 장치를 다음 신호를 새 자동 시작 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-214">For example, you can use the new auto-start feature to initialize an application and then signal a load-balancer that the application was initialized and ready to accept HTTP traffic.</span></span>

<a id="0.2__Toc224729021"></a><a id="0.2__Toc253429242"></a><a id="0.2__Toc243304616"></a>

### <a name="permanently-redirecting-a-page"></a><span data-ttu-id="3e862-215">페이지를 영구적으로 리디렉션</span><span class="sxs-lookup"><span data-stu-id="3e862-215">Permanently Redirecting a Page</span></span>

<span data-ttu-id="3e862-216">일반적으로 웹 응용 프로그램 페이지 및 관련 기타 콘텐츠 검색 엔진에서 오래 된 링크의 누적을 야기할 수 있는 시간이 지남에 따라 이동할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-216">It is common practice in Web applications to move pages and other content around over time, which can lead to an accumulation of stale links in search engines.</span></span> <span data-ttu-id="3e862-217">ASP.NET에서 개발자가 일반적으로 요청 이전 Url 사용 하 여 처리를 사용 하 여 합니다 *Response.Redirect* 새 URL로 요청을 전달 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-217">In ASP.NET, developers have traditionally handled requests to old URLs by using by using the *Response.Redirect* method to forward a request to the new URL.</span></span> <span data-ttu-id="3e862-218">그러나 합니다 *리디렉션* 메서드는 사용자가 이전 Url에 액세스 하려고 하면 왕복 추가 http 결과 HTTP 302 있음 (임시 리디렉션) 응답을 발급 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-218">However, the *Redirect* method issues an HTTP 302 Found (temporary redirect) response, which results in an extra HTTP round trip when users attempt to access the old URLs.</span></span>

<span data-ttu-id="3e862-219">ASP.NET 4를 새로 추가 *RedirectPermanent* 문제 HTTP 301 쉽게 하는 도우미 메서드는 다음 예제와 같이 응답을 영구적으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-219">ASP.NET 4 adds a new *RedirectPermanent* helper method that makes it easy to issue HTTP 301 Moved Permanently responses, as in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample8.cs)]

<span data-ttu-id="3e862-220">검색 엔진 및 영구 리디렉션을 인식 하는 다른 사용자 에이전트는 임시 리디렉션에 대 한 브라우저에서 불필요 한 왕복을 제거 하는 콘텐츠를 사용 하 여 연결 된 새 URL을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-220">Search engines and other user agents that recognize permanent redirects will store the new URL that is associated with the content, which eliminates the unnecessary round trip made by the browser for temporary redirects.</span></span>

<a id="0.2__Toc224729022"></a><a id="0.2__Toc253429243"></a><a id="0.2__Toc243304617"></a>

### <a name="shrinking-session-state"></a><span data-ttu-id="3e862-221">세션 상태를 축소합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-221">Shrinking Session State</span></span>

<span data-ttu-id="3e862-222">ASP.NET은 웹 팜에서 세션 상태를 저장 하기 위한 두 가지 기본 옵션을 제공 합니다.-out-of-process 세션 상태 서버를 사용 하는 호출 하는 세션 상태 공급자 및 Microsoft SQL Server 데이터베이스에 데이터를 저장 하는 세션 상태 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-222">ASP.NET provides two default options for storing session state across a Web farm: a session-state provider that invokes an out-of-process session-state server, and a session-state provider that stores data in a Microsoft SQL Server database.</span></span> <span data-ttu-id="3e862-223">두 옵션 모두 웹 응용 프로그램의 작업자 프로세스 외부 상태 정보가 저장 되므로, 세션 상태를 원격 저장소로 전송 되기 전에 직렬화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-223">Because both options involve storing state information outside a Web application's worker process, session state has to be serialized before it is sent to remote storage.</span></span> <span data-ttu-id="3e862-224">세션 상태에 저장 되는 얼 만큼의 정보에 따라 serialize 된 데이터의 크기가 상당히 커질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-224">Depending on how much information a developer saves in session state, the size of the serialized data can grow quite large.</span></span>

<span data-ttu-id="3e862-225">ASP.NET 4-out-of-process 세션 상태 공급자의 두 종류에 대 한 새 압축 옵션을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-225">ASP.NET 4 introduces a new compression option for both kinds of out-of-process session-state providers.</span></span> <span data-ttu-id="3e862-226">경우는 *compressionEnabled* 다음 예제와 같이 하는 구성 옵션이 설정 된 *true*, ASP.NET은 압축 (및 압축 풀기).NET Framework 를사용하여serialize된세션상태 *System.IO.Compression.GZipStream* 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-226">When the *compressionEnabled* configuration option shown in the following example is set to *true*, ASP.NET will compress (and decompress) serialized session state by using the .NET Framework *System.IO.Compression.GZipStream* class.</span></span>

[!code-xml[Main](overview/samples/sample9.xml)]

<span data-ttu-id="3e862-227">새 특성의 단순한 더하기를 사용 하 여는 `Web.config` 파일을 웹 서버의 예비 CPU 주기를 사용 하 여 응용 프로그램에는 serialize 된 세션 상태 데이터의 크기를 상당히 줄이는 실현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-227">With the simple addition of the new attribute to the `Web.config` file, applications with spare CPU cycles on Web servers can realize substantial reductions in the size of serialized session-state data.</span></span>

<a id="0.2__Toc253429244"></a><a id="0.2__Toc243304618"></a>

### <a name="expanding-the-range-of-allowable-urls"></a><span data-ttu-id="3e862-228">허용 되는 Url의 범위를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-228">Expanding the Range of Allowable URLs</span></span>

<span data-ttu-id="3e862-229">ASP.NET 4 응용 프로그램 Url의 크기를 확장 하는 것에 대 한 새 옵션을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-229">ASP.NET 4 introduces new options for expanding the size of application URLs.</span></span> <span data-ttu-id="3e862-230">이전 버전의 ASP.NET URL 경로 길이가 260 자, NTFS 파일 경로 제한에 따라 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-230">Previous versions of ASP.NET constrained URL path lengths to 260 characters, based on the NTFS file-path limit.</span></span> <span data-ttu-id="3e862-231">ASP.NET 4에는 옵션이 있습니다 (늘리거나 줄이려면)이이 제한을 응용 프로그램에 대해 적절 하 게 사용 하 여 두 개의 새 *httpRuntime* 구성 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-231">In ASP.NET 4, you have the option to increase (or decrease) this limit as appropriate for your applications, using two new *httpRuntime* configuration attributes.</span></span> <span data-ttu-id="3e862-232">다음 예제에서는 이러한 새 특성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-232">The following example shows these new attributes.</span></span>

[!code-xml[Main](overview/samples/sample10.xml)]

<span data-ttu-id="3e862-233">더 길거나 더 짧은 경로 (프로토콜, 서버 이름 및 쿼리 문자열을 포함 하지 않는 URL의 일부)를 허용 하려면 수정 된 *[maxUrlLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-233">To allow longer or shorter paths (the portion of the URL that does not include protocol, server name, and query string), modify the *[maxUrlLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* attribute.</span></span> <span data-ttu-id="3e862-234">길거나 짧은 쿼리 문자열을 허용 하려면 값을 수정 합니다 *[maxQueryStringLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-234">To allow longer or shorter query strings, modify the value of the *[maxQueryStringLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* attribute.</span></span>

<span data-ttu-id="3e862-235">ASP.NET 4에서는 URL 문자 검사에 사용 되는 문자를 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-235">ASP.NET 4 also enables you to configure the characters that are used by the URL character check.</span></span> <span data-ttu-id="3e862-236">ASP.NET URL의 경로 부분에 잘못 된 문자가 찾으면 요청을 거부 하 고 HTTP 400 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-236">When ASP.NET finds an invalid character in the path portion of a URL, it rejects the request and issues an HTTP 400 error.</span></span> <span data-ttu-id="3e862-237">이전 버전의 ASP.NET에서 URL 문자 검사 고정된 된 문자 집합으로 제한 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-237">In previous versions of ASP.NET, the URL character checks were limited to a fixed set of characters.</span></span> <span data-ttu-id="3e862-238">ASP.NET 4에서 사용 하 여 새 유효한 문자 집합이 사용자 지정할 수 있습니다 *requestPathInvalidChars* 특성을 *httpRuntime* 다음 예제에서와 같이 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="3e862-238">In ASP.NET 4, you can customize the set of valid characters using the new *requestPathInvalidChars* attribute of the *httpRuntime* configuration element, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample11.xml)]

<span data-ttu-id="3e862-239">기본적으로 <em>requestPathInvalidChars</em> 특성은 잘못 된 것으로 8 개의 문자를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-239">By default, the <em>requestPathInvalidChars</em> attribute defines eight characters as invalid.</span></span> <span data-ttu-id="3e862-240">(에 할당 되는 문자열에 <em>requestPathInvalidChars</em> 기본적으로<em>를</em>는 보다 작은 (&lt;), 보다 큼 (&gt;), 및 앰퍼샌드 (&amp;) 문자는 인코딩 되는 `Web.config` 파일은 XML 파일입니다.) 필요에 따라 잘못 된 문자 집합을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-240">(In the string that is assigned to <em>requestPathInvalidChars</em> by default<em>,</em>the less than (&lt;), greater than (&gt;), and ampersand (&amp;) characters are encoded, because the `Web.config` file is an XML file.) You can customize the set of invalid characters as needed.</span></span>

> [!NOTE]
> <span data-ttu-id="3e862-241">ASP.NET 4는 항상 문자 (0x00-0x1f, ASCII 범위에 포함 된 URL 경로 거부 IETF의 RFC 2396에 정의 된 대로 잘못 된 URL 문자는 참고 ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt)).</span><span class="sxs-lookup"><span data-stu-id="3e862-241">Note ASP.NET 4 always rejects URL paths that contain characters in the ASCII range of 0x00 to 0x1F, because those are invalid URL characters as defined in RFC 2396 of the IETF ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt)).</span></span> <span data-ttu-id="3e862-242">IIS 6을 실행 하는 버전의 Windows Server에서 또는 이상, http.sys 프로토콜 장치 드라이버를 자동으로 거부 Url 이러한 문자를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-242">On versions of Windows Server that run IIS 6 or higher, the http.sys protocol device driver automatically rejects URLs with these characters.</span></span>


<a id="0.2__Toc253429245"></a><a id="0.2__Toc243304619"></a>

### <a name="extensible-request-validation"></a><span data-ttu-id="3e862-243">확장 가능한 요청 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="3e862-243">Extensible Request Validation</span></span>

<span data-ttu-id="3e862-244">ASP.NET 요청 유효성 검사는 사이트 간 스크립팅 (XSS) 공격에 자주 사용 되는 문자열에 대 한 들어오는 HTTP 요청 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-244">ASP.NET request validation searches incoming HTTP request data for strings that are commonly used in cross-site scripting (XSS) attacks.</span></span> <span data-ttu-id="3e862-245">잠재적인 XSS 문자열이 발견 되 면 요청 유효성 검사는 주의 대상 문자열에 플래그를 지정 하 고 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-245">If potential XSS strings are found, request validation flags the suspect string and returns an error.</span></span> <span data-ttu-id="3e862-246">XSS 공격에 사용 되는 가장 일반적인 문자열을 발견 하는 경우에 기본 제공 요청 유효성 검사 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-246">The built-in request validation returns an error only when it finds the most common strings used in XSS attacks.</span></span> <span data-ttu-id="3e862-247">너무 많은 가양성 XSS 유효성 검사를 더 적극적으로 확인 하는 이전 하려고 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-247">Previous attempts to make the XSS validation more aggressive resulted in too many false positives.</span></span> <span data-ttu-id="3e862-248">그러나 고객은 특정 페이지 또는 특정 유형의 요청에 대 한 더 공격적으로 또는 반대로 할 의도적으로 XSS를 완화 하는 요청 유효성 검사 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-248">However, customers might want request validation that is more aggressive, or conversely might want to intentionally relax XSS checks for specific pages or for specific types of requests.</span></span>

<span data-ttu-id="3e862-249">ASP.NET 4에서 요청 유효성 검사 기능 내용이 확장할 수 있는 사용자 지정 요청 유효성 검사 논리를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-249">In ASP.NET 4, the request validation feature has been made extensible so that you can use custom request-validation logic.</span></span> <span data-ttu-id="3e862-250">새에서 파생 되는 클래스를 만들면 요청 유효성 검사를 확장 하려면 *System.Web.Util.RequestValidator* 유형 및 수에 응용 프로그램 구성 (에 *httpRuntime* 섹션의 `Web.config`파일) 사용자 지정 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-250">To extend request validation, you create a class that derives from the new *System.Web.Util.RequestValidator* type, and you configure the application (in the *httpRuntime* section of the `Web.config` file) to use the custom type.</span></span> <span data-ttu-id="3e862-251">다음 예제에서는 사용자 지정 요청 유효성 검사 클래스를 구성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-251">The following example shows how to configure a custom request-validation class:</span></span>

[!code-xml[Main](overview/samples/sample12.xml)]

<span data-ttu-id="3e862-252">새 *requestValidationType* 특성 사용자 지정 요청 유효성 검사를 제공 하는 클래스를 지정 하는 표준.NET Framework 형식 식별자 문자열이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-252">The new *requestValidationType* attribute requires a standard .NET Framework type identifier string that specifies the class that provides custom request validation.</span></span> <span data-ttu-id="3e862-253">각 요청에 대 한 ASP.NET 들어오는 HTTP 요청 데이터의 각 부분을 처리 하는 데 사용자 지정 형식을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-253">For each request, ASP.NET invokes the custom type to process each piece of incoming HTTP request data.</span></span> <span data-ttu-id="3e862-254">들어오는 URL, (쿠키 및 사용자 지정 헤더), 모든 HTTP 헤더 및 엔터티 본문을 다음 예와에서 같이 사용자 지정 요청 유효성 검사 클래스에 대 한 사용 가능한 모든 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-254">The incoming URL, all the HTTP headers (both cookies and custom headers), and the entity body are all available for inspection by a custom request validation class like that shown in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample13.cs)]

<span data-ttu-id="3e862-255">여기서 하지 않으려는 경우 들어오는 HTTP 데이터를 검사 하는 경우 요청 유효성 검사 클래스 대체할 수 ASP.NET 기본 요청 유효성 검사 호출 하 여 실행할 수 있도록 *기본입니다. IsValidRequestString 합니다.*</span><span class="sxs-lookup"><span data-stu-id="3e862-255">For cases where you do not want to inspect a piece of incoming HTTP data, the request-validation class can fall back to let the ASP.NET default request validation run by simply calling *base.IsValidRequestString.*</span></span>

<a id="0.2__Toc253429246"></a><a id="0.2__Toc243304620"></a>

### <a name="object-caching-and-object-caching-extensibility"></a><span data-ttu-id="3e862-256">개체 캐싱 및 캐싱 확장성 개체</span><span class="sxs-lookup"><span data-stu-id="3e862-256">Object Caching and Object Caching Extensibility</span></span>

<span data-ttu-id="3e862-257">ASP.NET는 강력한 메모리 내 개체 캐시를 포함 하는 데 해당 첫 번째 릴리스 이후 (*System.Web.Caching.Cache*).</span><span class="sxs-lookup"><span data-stu-id="3e862-257">Since its first release, ASP.NET has included a powerful in-memory object cache (*System.Web.Caching.Cache*).</span></span> <span data-ttu-id="3e862-258">캐시 구현이 비 웹 응용 프로그램에서 사용 된는 자주 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-258">The cache implementation has been so popular that it has been used in non-Web applications.</span></span> <span data-ttu-id="3e862-259">그러나이 작업은 까다롭습니다에 대 한 참조를 포함 하는 Windows Forms 또는 WPF 응용 프로그램에 대 한 `System.Web.dll` 를 ASP.NET 개체 캐시를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-259">However, it is awkward for a Windows Forms or WPF application to include a reference to `System.Web.dll` just to be able to use the ASP.NET object cache.</span></span>

<span data-ttu-id="3e862-260">캐싱을 사용할 수 있도록 모든 응용 프로그램,.NET Framework 4에서는 새 어셈블리, 새 네임 스페이스, 몇 가지 기본 형식 및 구체적인 구현 캐싱를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-260">To make caching available for all applications, the .NET Framework 4 introduces a new assembly, a new namespace, some base types, and a concrete caching implementation.</span></span> <span data-ttu-id="3e862-261">새 `System.Runtime.Caching.dll` 어셈블리에는 새 캐싱 API를 포함 합니다 *System.Runtime.Caching* 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-261">The new `System.Runtime.Caching.dll` assembly contains a new caching API in the *System.Runtime.Caching* namespace.</span></span> <span data-ttu-id="3e862-262">클래스의 두 가지 핵심 집합을 포함 하는 네임 스페이스:</span><span class="sxs-lookup"><span data-stu-id="3e862-262">The namespace contains two core sets of classes:</span></span>

- <span data-ttu-id="3e862-263">모든 유형의 사용자 지정 캐시 구현 작성 하기 위한 기초를 제공 하는 추상 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-263">Abstract types that provide the foundation for building any type of custom cache implementation.</span></span>
- <span data-ttu-id="3e862-264">구체적인 메모리 내 개체 캐시 구현 (합니다 *System.Runtime.Caching.MemoryCache* 클래스).</span><span class="sxs-lookup"><span data-stu-id="3e862-264">A concrete in-memory object cache implementation (the *System.Runtime.Caching.MemoryCache* class).</span></span>

<span data-ttu-id="3e862-265">새 *MemoryCache* ASP.NET cache 클래스와 비슷하게 모델링 됩니다 및 ASP.NET을 사용 하 여 내부 캐시 엔진 논리의 대부분을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-265">The new *MemoryCache* class is modeled closely on the ASP.NET cache, and it shares much of the internal cache engine logic with ASP.NET.</span></span> <span data-ttu-id="3e862-266">하지만의 캐싱 Api를 공개 *System.Runtime.Caching* ASP.NET을 사용한 경우, 사용자 지정 캐시 개발을 지원 하도록 업데이트 되었습니다 *캐시* 개체의 친숙 한 개념을 찾을 수 있습니다는 새 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-266">Although the public caching APIs in *System.Runtime.Caching* have been updated to support development of custom caches, if you have used the ASP.NET *Cache* object, you will find familiar concepts in the new APIs.</span></span>

<span data-ttu-id="3e862-267">자세한 내용은 새 *MemoryCache* 클래스 및 기본 Api를 지 원하는 전체 문서를 기준으로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-267">An in-depth discussion of the new *MemoryCache* class and supporting base APIs would require an entire document.</span></span> <span data-ttu-id="3e862-268">그러나 다음 예제에서는 사용 하면 새 캐시 API의 작동 방식을 파악 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-268">However, the following example gives you an idea of how the new cache API works.</span></span> <span data-ttu-id="3e862-269">예제에 대 한 종속성 없이 Windows Forms 응용 프로그램에 대 한 기록 된 `System.Web.dll`합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-269">The example was written for a Windows Forms application, without any dependency on `System.Web.dll`.</span></span>

[!code-csharp[Main](overview/samples/sample14.cs)]

<a id="0.2__Toc253429247"></a><a id="0.2__Toc243304621"></a>

### <a name="extensible-html-url-and-http-header-encoding"></a><span data-ttu-id="3e862-270">확장 가능한 HTML, URL 및 HTTP 헤더 인코딩</span><span class="sxs-lookup"><span data-stu-id="3e862-270">Extensible HTML, URL, and HTTP Header Encoding</span></span>

<span data-ttu-id="3e862-271">ASP.NET 4에서는 다음 일반 텍스트 인코딩 작업에 대 한 사용자 지정 인코딩 루틴을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-271">In ASP.NET 4, you can create custom encoding routines for the following common text-encoding tasks:</span></span>

- <span data-ttu-id="3e862-272">HTML 인코딩입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-272">HTML encoding.</span></span>
- <span data-ttu-id="3e862-273">URL 인코딩입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-273">URL encoding.</span></span>
- <span data-ttu-id="3e862-274">HTML 특성 인코딩입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-274">HTML attribute encoding.</span></span>
- <span data-ttu-id="3e862-275">아웃 바운드 HTTP 헤더를 인코딩입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-275">Encoding outbound HTTP headers.</span></span>

<span data-ttu-id="3e862-276">새에서 파생 하 여 사용자 지정 인코더를 만들 수 있습니다 *System.Web.Util.HttpEncoder* 형식 및 다음 ASP.NET 구성에서 사용자 지정 형식을 사용 하는 *httpRuntime* 섹션을 `Web.config` 파일인으로 다음 예제와 같이:</span><span class="sxs-lookup"><span data-stu-id="3e862-276">You can create a custom encoder by deriving from the new *System.Web.Util.HttpEncoder* type and then configuring ASP.NET to use the custom type in the *httpRuntime* section of the `Web.config` file, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample15.xml)]

<span data-ttu-id="3e862-277">사용자 지정 인코더를 구성한 후 ASP.NET 사용자 지정 인코딩 구현을 인코딩 방법의 공용 때마다를 자동으로 호출 합니다 *System.Web.HttpUtility* 또는 *System.Web.HttpServerUtility* 클래스 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-277">After a custom encoder has been configured, ASP.NET automatically calls the custom encoding implementation whenever public encoding methods of the *System.Web.HttpUtility* or *System.Web.HttpServerUtility* classes are called.</span></span> <span data-ttu-id="3e862-278">그러면 웹 개발 팀의 나머지 부분 공용 ASP.NET 인코딩 Api를 사용 하는 동안 적극적으로 문자 인코딩을 구현 하는 사용자 지정 인코더를 만드는 웹 개발 팀의 한 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-278">This lets one part of a Web development team create a custom encoder that implements aggressive character encoding, while the rest of the Web development team continues to use the public ASP.NET encoding APIs.</span></span> <span data-ttu-id="3e862-279">중앙에서 사용자 지정 인코더를 구성 하 여 합니다 *httpRuntime* 요소인 보장 됩니다 인코딩 Api 공개 ASP.NET의 모든 텍스트 인코딩 호출은 사용자 지정 인코더를 통해 라우팅될 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-279">By centrally configuring a custom encoder in the *httpRuntime* element, you are guaranteed that all text-encoding calls from the public ASP.NET encoding APIs are routed through the custom encoder.</span></span>

<a id="0.2__Toc253429248"></a><a id="0.2__Toc243304622"></a>

### <a name="performance-monitoring-for-individual-applications-in-a-single-worker-process"></a><span data-ttu-id="3e862-280">단일 작업자 프로세스에서 개별 응용 프로그램 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="3e862-280">Performance Monitoring for Individual Applications in a Single Worker Process</span></span>

<span data-ttu-id="3e862-281">단일 서버에서 호스팅될 수 있는 웹 사이트의 수를 증가 시키기 위해 여러 호스팅 서비스 공급자는 단일 작업자 프로세스에서 여러 ASP.NET 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-281">In order to increase the number of Web sites that can be hosted on a single server, many hosters run multiple ASP.NET applications in a single worker process.</span></span> <span data-ttu-id="3e862-282">그러나 여러 응용 프로그램에 단일 공유 작업자 프로세스를 사용 하는 경우 어렵습니다 문제가 발생 하는 개별 응용 프로그램을 식별 하는 서버 관리자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-282">However, if multiple applications use a single shared worker process, it is difficult for server administrators to identify an individual application that is experiencing problems.</span></span>

<span data-ttu-id="3e862-283">ASP.NET 4는 CLR에 의해 도입 된 새 리소스 모니터링 기능을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-283">ASP.NET 4 leverages new resource-monitoring functionality introduced by the CLR.</span></span> <span data-ttu-id="3e862-284">이 기능을 사용 하려면 다음 XML 구성 코드 조각을 추가할 수 있습니다는 `aspnet.config` 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-284">To enable this functionality, you can add the following XML configuration snippet to the `aspnet.config` configuration file.</span></span>

[!code-xml[Main](overview/samples/sample16.xml)]

> [!NOTE]
> <span data-ttu-id="3e862-285">참고는 `aspnet.config` 파일은.NET Framework를 설치한 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-285">Note The `aspnet.config` file is in the directory where the .NET Framework is installed.</span></span> <span data-ttu-id="3e862-286">있지는 `Web.config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-286">It is not the `Web.config` file.</span></span>


<span data-ttu-id="3e862-287">경우는 *appDomainResourceMonitoring* 기능이 설정 된, "ASP.NET 응용 프로그램" 성능 범주에서 사용할 수 있는 두 개의 새 성능 카운터: *관리 되는 프로세서 시간 백분율* 및  *관리 되는 메모리 사용*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-287">When the *appDomainResourceMonitoring* feature has been enabled, two new performance counters are available in the "ASP.NET Applications" performance category: *% Managed Processor Time* and *Managed Memory Used*.</span></span> <span data-ttu-id="3e862-288">이러한 성능 카운터 모두 예상된 CPU 시간 및 개별 ASP.NET 응용 프로그램의 관리 되는 메모리 사용률을 추적 하려면 새 CLR 응용 프로그램 도메인 리소스 관리 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-288">Both of these performance counters use the new CLR application-domain resource management feature to track estimated CPU time and managed memory utilization of individual ASP.NET applications.</span></span> <span data-ttu-id="3e862-289">따라서 ASP.NET 4를 사용 하 여 관리자가 이제 단일 작업자 프로세스에서 실행 하는 개별 응용 프로그램의 리소스 소비에 더욱 세부적인 보기를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-289">As a result, with ASP.NET 4, administrators now have a more granular view into the resource consumption of individual applications running in a single worker process.</span></span>

<a id="0.2__Toc253429249"></a><a id="0.2__Toc243304623"></a>

### <a name="multi-targeting"></a><span data-ttu-id="3e862-290">멀티 타기팅</span><span class="sxs-lookup"><span data-stu-id="3e862-290">Multi-Targeting</span></span>

<span data-ttu-id="3e862-291">.NET Framework의 특정 버전을 대상으로 하는 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-291">You can create an application that targets a specific version of the .NET Framework.</span></span> <span data-ttu-id="3e862-292">ASP.NET 4에서 새 특성에는 *컴파일* 의 요소는 `Web.config` 파일을 사용 하면.NET Framework 4 이상을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-292">In ASP.NET 4, a new attribute in the *compilation* element of the `Web.config` file lets you target the .NET Framework 4 and later.</span></span> <span data-ttu-id="3e862-293">.NET Framework 4를 명시적으로 대상 및에서 선택적 요소를 포함 하는 경우는 `Web.config` 파일에 대 한 항목 예: *system.codedom*, 이러한 요소는.NET Framework 4에 대 한 올바른 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-293">If you explicitly target the .NET Framework 4, and if you include optional elements in the `Web.config` file such as the entries for *system.codedom*, these elements must be correct for the .NET Framework 4.</span></span> <span data-ttu-id="3e862-294">(명시적으로 대상으로 하지는.NET Framework 4를 대상 프레임 워크에 있는 항목의 부재에서 유추 됩니다는 `Web.config` 파일입니다.)</span><span class="sxs-lookup"><span data-stu-id="3e862-294">(If you do not explicitly target the .NET Framework 4, the target framework is inferred from the lack of an entry in the `Web.config` file.)</span></span>

<span data-ttu-id="3e862-295">다음 예제에서는 사용을 보여 줍니다.는 *targetFramework* 특성을 *컴파일* 요소의 `Web.config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-295">The following example shows the use of the *targetFramework* attribute in the *compilation* element of the `Web.config` file.</span></span>

[!code-xml[Main](overview/samples/sample17.xml)]

<span data-ttu-id="3e862-296">.NET Framework의 특정 버전을 대상으로 하는 방법에 대 한 다음 note:</span><span class="sxs-lookup"><span data-stu-id="3e862-296">Note the following about targeting a specific version of the .NET Framework:</span></span>

- <span data-ttu-id="3e862-297">.NET Framework 4 응용 프로그램 풀을 ASP.NET 빌드 시스템 가정.NET Framework 4를 대상으로 하는 경우는 `Web.config` 파일에 포함 되지 않습니다 합니다 *targetFramework* 특성 또는 경우에는 `Web.config` 파일이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-297">In a .NET Framework 4 application pool, the ASP.NET build system assumes the .NET Framework 4 as a target if the `Web.config` file does not include the *targetFramework* attribute or if the `Web.config` file is missing.</span></span> <span data-ttu-id="3e862-298">(해야.NET Framework 4 하에서 실행 되도록 응용 프로그램에 대 한 코딩 변경 합니다.)</span><span class="sxs-lookup"><span data-stu-id="3e862-298">(You might have to make coding changes to your application to make it run under the .NET Framework 4.)</span></span>
- <span data-ttu-id="3e862-299">포함 하는 경우를 *targetFramework* 특성인 경우에 *system.codeDom* 요소에 정의 된를 `Web.config` 파일이이 파일은.NET Framework 4에 대 한 올바른 항목을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-299">If you do include the *targetFramework* attribute, and if the *system.codeDom* element is defined in the `Web.config` file, this file must contain the correct entries for the .NET Framework 4.</span></span>
- <span data-ttu-id="3e862-300">사용 중인 경우는 *aspnet\_컴파일러* 응용 프로그램 (예: 빌드 환경)를 미리 컴파일할 명령에 올바른 버전을 사용 해야 합니다 *aspnet\_컴파일러* 대상 프레임 워크에 대 한 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-300">If you are using the *aspnet\_compiler* command to precompile your application (such as in a build environment), you must use the correct version of the *aspnet\_compiler* command for the target framework.</span></span> <span data-ttu-id="3e862-301">.NET Framework 3.5 및 이전 버전에 대해 컴파일하 (%WINDIR%\Microsoft.NET\Framework\v2.0.50727)는.NET Framework 2.0을 사용 하 여 제공 되는 컴파일러를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-301">Use the compiler that shipped with the .NET Framework 2.0 (%WINDIR%\Microsoft.NET\Framework\v2.0.50727) to compile for the .NET Framework 3.5 and earlier versions.</span></span> <span data-ttu-id="3e862-302">.NET Framework 4를 사용 하 여 만든 응용 프로그램 프레임 워크를 사용 하 여 또는 이상 버전을 사용 하 여 컴파일하는 데 함께 제공 되는 컴파일러를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-302">Use the compiler that ships with the .NET Framework 4 to compile applications created using that framework or using later versions.</span></span>
- <span data-ttu-id="3e862-303">런타임 시 컴파일러는 컴퓨터에 설치 된 최신 프레임 워크 어셈블리를 사용 (및 따라서 GAC에).</span><span class="sxs-lookup"><span data-stu-id="3e862-303">At run time, the compiler uses the latest framework assemblies that are installed on the computer (and therefore in the GAC).</span></span> <span data-ttu-id="3e862-304">업데이트 하려고 하면 나중에 프레임 워크 (예를 들어 가상 버전 4.1이 설치 되어)에 프레임 워크의 최신 버전의 기능을 사용 하는 일을 할 수 있습니다는 *targetFramework* 더 낮은 버전을 대상으로 하는 특성 (4.0)로 설정과 같은 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-304">If an update is made later to the framework (for example, a hypothetical version 4.1 is installed), you will be able to use features in the newer version of the framework even though the *targetFramework* attribute targets a lower version (such as 4.0).</span></span> <span data-ttu-id="3e862-305">그러나 (Visual Studio 2010 또는 사용 하는 경우 디자인 타임 합니다 *aspnet\_컴파일러* 명령, 프레임 워크의 최신 기능을 사용 하면 컴파일러 오류).</span><span class="sxs-lookup"><span data-stu-id="3e862-305">(However, at design time in Visual Studio 2010 or when you use the *aspnet\_compiler* command, using newer features of the framework will cause compiler errors).</span></span>

<a id="0.2__Toc224729023"></a><a id="0.2__Toc253429250"></a><a id="0.2__Toc243304624"></a>

## <a name="ajax"></a><span data-ttu-id="3e862-306">Ajax</span><span class="sxs-lookup"><span data-stu-id="3e862-306">Ajax</span></span>

<a id="0.2__Toc253429251"></a><a id="0.2__Toc243304625"></a>

### <a name="jquery-included-with-web-forms-and-mvc"></a><span data-ttu-id="3e862-307">Web Forms 및 MVC를 사용 하 여 포함 된 jQuery</span><span class="sxs-lookup"><span data-stu-id="3e862-307">jQuery Included with Web Forms and MVC</span></span>

<span data-ttu-id="3e862-308">Web Forms 및 MVC 용 Visual Studio 템플릿에 오픈 소스 jQuery 라이브러리를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-308">The Visual Studio templates for both Web Forms and MVC include the open-source jQuery library.</span></span> <span data-ttu-id="3e862-309">새 웹 사이트 또는 프로젝트를 만든 경우 다음 3 개의 파일이 포함 된 스크립트 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-309">When you create a new website or project, a Scripts folder containing the following 3 files is created:</span></span>

- <span data-ttu-id="3e862-310">jQuery-1.4.1.js –는 사용자가 읽을 축소 되지 않은 jQuery 라이브러리의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-310">jQuery-1.4.1.js – The human-readable, unminified version of the jQuery library.</span></span>
- <span data-ttu-id="3e862-311">jQuery-14.1.min.js – jQuery 라이브러리의 축소 된 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-311">jQuery-14.1.min.js – The minified version of the jQuery library.</span></span>
- <span data-ttu-id="3e862-312">jQuery-1.4.1-vsdoc.js – jQuery 라이브러리에 대 한 Intellisense 설명서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-312">jQuery-1.4.1-vsdoc.js – The Intellisense documentation file for the jQuery library.</span></span>

<span data-ttu-id="3e862-313">응용 프로그램을 개발 하는 동안 jQuery의 축소 되지 않은 버전을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-313">Include the unminified version of jQuery while developing an application.</span></span> <span data-ttu-id="3e862-314">프로덕션 응용 프로그램에는 jQuery의 축소 된 버전을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-314">Include the minified version of jQuery for production applications.</span></span>

<span data-ttu-id="3e862-315">예를 들어, Web Forms 페이지는 jQuery를 사용 하 여 포커스를가지고 있을 때 노란색으로 ASP.NET TextBox 컨트롤의 배경색을 변경 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-315">For example, the following Web Forms page illustrates how you can use jQuery to change the background color of ASP.NET TextBox controls to yellow when they have focus.</span></span>

[!code-aspx[Main](overview/samples/sample18.aspx)]

<a id="0.2__Toc253429252"></a><a id="0.2__Toc243304626"></a>

### <a name="content-delivery-network-support"></a><span data-ttu-id="3e862-316">Content Delivery Network 지원</span><span class="sxs-lookup"><span data-stu-id="3e862-316">Content Delivery Network Support</span></span>

<span data-ttu-id="3e862-317">Microsoft Ajax 콘텐츠 배달 네트워크 (CDN)를 사용 하면 손쉽게 웹 응용 프로그램에 ASP.NET Ajax 및 jQuery 스크립트를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-317">The Microsoft Ajax Content Delivery Network (CDN) enables you to easily add ASP.NET Ajax and jQuery scripts to your Web applications.</span></span> <span data-ttu-id="3e862-318">JQuery 라이브러리를 사용 하 여 추가 하 여 시작할 수는 예를 들어, 한 `<script>` 같이 Ajax.microsoft.com 가리키는 페이지 태그:</span><span class="sxs-lookup"><span data-stu-id="3e862-318">For example, you can start using the jQuery library simply by adding a `<script>` tag to your page that points to Ajax.microsoft.com like this:</span></span>

[!code-html[Main](overview/samples/sample19.html)]

<span data-ttu-id="3e862-319">Microsoft Ajax CDN을 활용 하 여 Ajax 응용 프로그램의 성능을 크게 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-319">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="3e862-320">Microsoft Ajax CDN의 콘텐츠는 세계에 있는 서버에 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-320">The contents of the Microsoft Ajax CDN are cached on servers located around the world.</span></span> <span data-ttu-id="3e862-321">또한 Microsoft Ajax CDN에는 브라우저 서로 다른 도메인에 있는 웹 사이트에 대 한 캐시 된 JavaScript 파일을 다시 사용할 수 있도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-321">In addition, the Microsoft Ajax CDN enables browsers to reuse cached JavaScript files for Web sites that are located in different domains.</span></span>

<span data-ttu-id="3e862-322">Microsoft Ajax Content Delivery Network는 Secure Sockets Layer를 사용 하 여 웹 페이지를 처리 해야 하는 경우 SSL (HTTPS)을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-322">The Microsoft Ajax Content Delivery Network supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="3e862-323">CDN을 사용할 수 없는 경우는 대체 (fallback)를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-323">Implement a fallback when the CDN is unavailable.</span></span> <span data-ttu-id="3e862-324">대체를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-324">Test the fallback.</span></span>

<span data-ttu-id="3e862-325">Microsoft Ajax CDN에 대 한 자세한 내용은 다음 웹 사이트를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-325">To learn more about the Microsoft Ajax CDN, visit the following website:</span></span>

[https://www.asp.net/ajaxlibrary/CDN.ashx](../../ajax/cdn/overview.md)

<span data-ttu-id="3e862-326">ASP.NET ScriptManager는 Microsoft Ajax CDN을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-326">The ASP.NET ScriptManager supports the Microsoft Ajax CDN.</span></span> <span data-ttu-id="3e862-327">한 가지 속성만 설정, EnableCdn 속성 하면 CDN에서 모든 ASP.NET 프레임 워크 JavaScript 파일을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-327">Simply by setting one property, the EnableCdn property, you can retrieve all ASP.NET framework JavaScript files from the CDN:</span></span>

[!code-aspx[Main](overview/samples/sample20.aspx)]

<span data-ttu-id="3e862-328">EnableCdn 속성 값이 true를 설정 하면 ASP.NET framework 유효성 검사 및 UpdatePanel에 사용 되는 모든 JavaScript 파일을 포함 하 여 CDN에서 모든 ASP.NET 프레임 워크 JavaScript 파일을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-328">After you set the EnableCdn property to the value true, the ASP.NET framework will retrieve all ASP.NET framework JavaScript files from the CDN including all JavaScript files used for validation and the UpdatePanel.</span></span> <span data-ttu-id="3e862-329">이 하나의 속성을 설정할 웹 응용 프로그램의 성능에 상당한 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-329">Setting this one property can have a dramatic impact on the performance of your web application.</span></span>

<span data-ttu-id="3e862-330">웹 리소스의 특성을 사용 하 여 고유한 JavaScript 파일에 대 한의 CDN 경로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-330">You can set the CDN path for your own JavaScript files by using the WebResource attribute.</span></span> <span data-ttu-id="3e862-331">새 CdnPath 속성 값이 true에 EnableCdn 속성을 설정할 때 사용 하는 CDN에 대 한 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-331">The new CdnPath property specifies the path to the CDN used when you set the EnableCdn property to the value true:</span></span>

[!code-csharp[Main](overview/samples/sample21.cs)]

<a id="0.2__Toc253429253"></a><a id="0.2__Toc243304627"></a>

### <a name="scriptmanager-explicit-scripts"></a><span data-ttu-id="3e862-332">ScriptManager 명시적 스크립트</span><span class="sxs-lookup"><span data-stu-id="3e862-332">ScriptManager Explicit Scripts</span></span>

<span data-ttu-id="3e862-333">이전에 ASP.NET ScriptManger 사용 하는 경우 다음 해야 전체 모놀리식 ASP.NET Ajax 라이브러리를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-333">In the past, if you used the ASP.NET ScriptManger then you were required to load the entire monolithic ASP.NET Ajax Library.</span></span> <span data-ttu-id="3e862-334">새 ScriptManager.AjaxFrameworkMode 속성을 활용 하 여 ASP.NET Ajax 라이브러리의 구성 요소를 로드 하는 정확 하 게 제어할 수 있으며만 해야 하는 ASP.NET Ajax 라이브러리의 구성 요소를 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-334">By taking advantage of the new ScriptManager.AjaxFrameworkMode property, you can control exactly which components of the ASP.NET Ajax Library are loaded and load only the components of the ASP.NET Ajax Library that you need.</span></span>

<span data-ttu-id="3e862-335">ScriptManager.AjaxFrameworkMode 속성은 다음 값으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-335">The ScriptManager.AjaxFrameworkMode property can be set to the following values:</span></span>

- <span data-ttu-id="3e862-336">사용 가능--지정 ScriptManager 컨트롤에 자동으로 모든 핵심 프레임 워크 스크립트 (레거시 동작)의 결합 된 스크립트 파일인 MicrosoftAjax.js 스크립트 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-336">Enabled -- Specifies that the ScriptManager control automatically includes the MicrosoftAjax.js script file, which is a combined script file of every core framework script (legacy behavior).</span></span>
- <span data-ttu-id="3e862-337">사용 하지 않도록 설정-모든 Microsoft Ajax 스크립트 기능이 사용 하지 않도록 설정 됩니다 하며는 ScriptManager 컨트롤이 참조 하지 않으면 모든 스크립트가 자동으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-337">Disabled -- Specifies that all Microsoft Ajax script features are disabled and that the ScriptManager control does not reference any scripts automatically.</span></span>
- <span data-ttu-id="3e862-338">명시적-를 명시적으로 포함 페이지에서 필요로 하는 개별 프레임 워크 핵심 스크립트 파일에 대 한 스크립트 참조 및를 포함 하는 각 스크립트 파일에 필요한 종속성에 대 한 참조를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-338">Explicit -- Specifies that you will explicitly include script references to individual framework core script file that your page requires, and that you will include references to the dependencies that each script file requires.</span></span>

<span data-ttu-id="3e862-339">예를 들어 명시적 값으로 AjaxFrameworkMode 속성을 설정 해야 하는 특정 ASP.NET Ajax 구성 요소 스크립트 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-339">For example, if you set the AjaxFrameworkMode property to the value Explicit then you can specify the particular ASP.NET Ajax component scripts that you need:</span></span>

[!code-aspx[Main](overview/samples/sample22.aspx)]

<a id="0.2__The_DataView_Control"></a><a id="0.2__The_DataContext_and"></a><a id="0.2__Refactoring_the_Microsoft"></a><a id="0.2__Toc224729032"></a><a id="0.2__Toc253429256"></a><a id="0.2__Toc243304630"></a>

## <a name="web-forms"></a><span data-ttu-id="3e862-340">Web Forms</span><span class="sxs-lookup"><span data-stu-id="3e862-340">Web Forms</span></span>

<span data-ttu-id="3e862-341">Web Forms에 ASP.NET의 핵심 기능은 ASP.NET 1.0 릴리스 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-341">Web Forms has been a core feature in ASP.NET since the release of ASP.NET 1.0.</span></span> <span data-ttu-id="3e862-342">다음을 포함 하 여 ASP.NET 4에 대 한이 영역의 많은 부분이 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-342">Many enhancements have been in this area for ASP.NET 4, including the following:</span></span>

- <span data-ttu-id="3e862-343">설정 하는 기능이 *meta* 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-343">The ability to set *meta* tags.</span></span>
- <span data-ttu-id="3e862-344">뷰 상태를 보다 자세히 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-344">More control over view state.</span></span>
- <span data-ttu-id="3e862-345">브라우저 기능을 사용 하 여 작업을 편리 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-345">Easier ways to work with browser capabilities.</span></span>
- <span data-ttu-id="3e862-346">ASP.NET Web Forms를 사용 하 여 라우팅을 사용 하 여 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-346">Support for using ASP.NET routing with Web Forms.</span></span>
- <span data-ttu-id="3e862-347">생성 된 Id 보다 자세히 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-347">More control over generated IDs.</span></span>
- <span data-ttu-id="3e862-348">데이터 컨트롤에서 선택한 행을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-348">The ability to persist selected rows in data controls.</span></span>
- <span data-ttu-id="3e862-349">렌더링 된 HTML에서 보다 자세히 제어를 *FormView* 하 고 *ListView* 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-349">More control over rendered HTML in the *FormView* and *ListView* controls.</span></span>
- <span data-ttu-id="3e862-350">데이터 소스 컨트롤에 대 한 필터링 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-350">Filtering support for data source controls.</span></span>

<a id="0.2__Toc224729033"></a><a id="0.2__Toc253429257"></a><a id="0.2__Toc243304631"></a>

### <a name="setting-meta-tags-with-the-pagemetakeywords-and-pagemetadescription-properties"></a><span data-ttu-id="3e862-351">Page.MetaKeywords 및 Page.MetaDescription 속성을 사용 하 여 메타 태그를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-351">Setting Meta Tags with the Page.MetaKeywords and Page.MetaDescription Properties</span></span>

<span data-ttu-id="3e862-352">ASP.NET 4에서는 두 개의 속성을 추가 합니다 *페이지* 클래스 *MetaKeywords* 하 고 *MetaDescription*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-352">ASP.NET 4 adds two properties to the *Page* class, *MetaKeywords* and *MetaDescription*.</span></span> <span data-ttu-id="3e862-353">이러한 두 속성에 해당 나타냅니다 *meta* 다음 예제에서와 같이 페이지의 태그:</span><span class="sxs-lookup"><span data-stu-id="3e862-353">These two properties represent corresponding *meta* tags in your page, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample23.aspx)]

<span data-ttu-id="3e862-354">이러한 두 속성 동일 하 게 작동 방식으로 페이지의 *Title* 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-354">These two properties work the same way that the page's *Title* property does.</span></span> <span data-ttu-id="3e862-355">이러한 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-355">They follow these rules:</span></span>

1. <span data-ttu-id="3e862-356">없으면 없습니다 *메타* 태그를 *헤드* 속성 이름과 일치 하는 요소 (즉, 이름을 "키워드" = *Page.MetaKeywords* 이름과 = "description" 에대한 *Page.MetaDescription*, 이러한 속성을 설정 하지 않은 즉), *meta* 태그 렌더링 될 때 페이지에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-356">If there are no *meta* tags in the *head* element that match the property names (that is, name="keywords" for *Page.MetaKeywords* and name="description" for *Page.MetaDescription*, meaning that these properties have not been set), the *meta* tags will be added to the page when it is rendered.</span></span>
2. <span data-ttu-id="3e862-357">이미 있는 경우 *meta* 이러한 이름의 태그를 이러한 속성 프록시로 get 및 set 메서드는 기존 태그의 내용에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-357">If there are already *meta* tags with these names, these properties act as get and set methods for the contents of the existing tags.</span></span>

<span data-ttu-id="3e862-358">런타임에 데이터베이스 또는 다른 원본에서 콘텐츠를 가져올 수 있습니다 하 고 설명할 수 있도록 동적으로 태그를 설정할 수 있는 이러한 속성을 설정할 수 있습니다 특정 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-358">You can set these properties at run time, which lets you get the content from a database or other source, and which lets you set the tags dynamically to describe what a particular page is for.</span></span>

<span data-ttu-id="3e862-359">설정할 수도 있습니다는 *키워드* 및 *설명* 속성에는 *@ Page* Web Forms 페이지 태그는 다음 예제와 같이 맨 위에 있는 지시문:</span><span class="sxs-lookup"><span data-stu-id="3e862-359">You can also set the *Keywords* and *Description* properties in the *@ Page* directive at the top of the Web Forms page markup, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample24.aspx)]

<span data-ttu-id="3e862-360">이렇게 무시 되는 *메타* 태그 내용을 (있는 경우) 페이지에서 이미 선언 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-360">This will override the *meta* tag contents (if any) already declared in the page.</span></span>

<span data-ttu-id="3e862-361">설명의 내용을 *meta* 태그는 Google의 미리 보기를 나열 하는 검색 개선에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-361">The contents of the description *meta* tag are used for improving search listing previews in Google.</span></span> <span data-ttu-id="3e862-362">(세부 정보를 참조 하세요 [meta 설명 변경을 사용 하 여 조각 개선](http://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html) Google 웹 마스터 중앙 블로그.) Google 및 Windows Live Search를 사용 하지 키워드의 내용에 않지만 다른 검색 엔진 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-362">(For details, see [Improve snippets with a meta description makeover](http://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html) on the Google Webmaster Central blog.) Google and Windows Live Search do not use the contents of the keywords for anything, but other search engines might.</span></span> <span data-ttu-id="3e862-363">자세한 내용은 [Meta 키워드 조언을](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php) 검색 엔진 설명서 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-363">For more information, see [Meta Keywords Advice](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php) on the Search Engine Guide Web site.</span></span>

<span data-ttu-id="3e862-364">이러한 새 속성은 간단한 기능을 하지만 고유한 만드는 코드를 작성 또는 이러한 작업을 수동으로 추가 하는 요구 사항을에서 저장 하는 *meta* 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-364">These new properties are a simple feature, but they save you from the requirement to add these manually or from writing your own code to create the *meta* tags.</span></span>

<a id="0.2__Toc224729034"></a><a id="0.2__Toc253429258"></a><a id="0.2__Toc243304632"></a>

### <a name="enabling-view-state-for-individual-controls"></a><span data-ttu-id="3e862-365">개별 컨트롤의 뷰 상태를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="3e862-365">Enabling View State for Individual Controls</span></span>

<span data-ttu-id="3e862-366">기본적으로 각 컨트롤 페이지의 응용 프로그램에 대 한 필요가 없는 경우에 잠재적으로 뷰 상태를 저장 하는 결과 사용 하 여 페이지 보기 상태 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-366">By default, view state is enabled for the page, with the result that each control on the page potentially stores view state even if it is not required for the application.</span></span> <span data-ttu-id="3e862-367">뷰 상태 데이터는 페이지를 생성 한 클라이언트에 페이지를 보내고 다시 게시 하는 데 걸리는 시간의 증가 태그에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-367">View state data is included in the markup that a page generates and increases the amount of time it takes to send a page to the client and post it back.</span></span> <span data-ttu-id="3e862-368">필요한 것 보다 자세한 뷰 상태를 저장 하면 상당한 성능 저하가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-368">Storing more view state than is necessary can cause significant performance degradation.</span></span> <span data-ttu-id="3e862-369">ASP.NET의 이전 버전에서는 개발자 페이지 크기를 줄이기 위해 개별 컨트롤의 뷰 상태를 해제할 수 있지만 개별 컨트롤에 대 한 명시적 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-369">In earlier versions of ASP.NET, developers could disable view state for individual controls in order to reduce page size, but had to do so explicitly for individual controls.</span></span> <span data-ttu-id="3e862-370">ASP.NET 4에서 웹 서버 컨트롤에 포함 된 *ViewStateMode* 하면 기본적으로 상태 보기를 사용 하지 않도록 설정 하 고 다음 페이지에서 필요로 하는 컨트롤에 대해서만 사용 하도록 설정 하는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-370">In ASP.NET 4, Web server controls include a *ViewStateMode* property that lets you disable view state by default and then enable it only for the controls that require it in the page.</span></span>

<span data-ttu-id="3e862-371">*ViewStateMode* 속성은 세 가지 값이 포함 된 열거형: *Enabled*, *사용 안 함*, 및 *상속*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-371">The *ViewStateMode* property takes an enumeration that has three values: *Enabled*, *Disabled*, and *Inherit*.</span></span> <span data-ttu-id="3e862-372">*사용 하도록 설정* 로 설정 된 모든 자식 컨트롤에 대 한 상태로 해당 컨트롤의 뷰 *상속* 이거나는 아무 것도 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-372">*Enabled* enables view state for that control and for any child controls that are set to *Inherit* or that have nothing set.</span></span> <span data-ttu-id="3e862-373">*사용 안 함* 뷰 상태를 사용 하지 않도록 설정 및 *상속* 컨트롤을 사용 하도록 지정 합니다 *ViewStateMode* 부모 컨트롤에서 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-373">*Disabled* disables view state, and *Inherit* specifies that the control uses the *ViewStateMode* setting from the parent control.</span></span>

<span data-ttu-id="3e862-374">다음 예제와 방법을 *ViewStateMode* 속성 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-374">The following example shows how the *ViewStateMode* property works.</span></span> <span data-ttu-id="3e862-375">태그 및 코드 페이지의 제어에 대 한 값이 포함 된 *ViewStateMode* 속성:</span><span class="sxs-lookup"><span data-stu-id="3e862-375">The markup and code for the controls in the following page includes values for the *ViewStateMode* property:</span></span>

[!code-aspx[Main](overview/samples/sample25.aspx)]

<span data-ttu-id="3e862-376">알 수 있듯이 코드 PlaceHolder1 컨트롤의 뷰 상태를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-376">As you can see, the code disables view state for the PlaceHolder1 control.</span></span> <span data-ttu-id="3e862-377">이 속성 값 상속 되는 자식 label1 컨트롤 (*상속* 의 기본값은 *ViewStateMode* 컨트롤에 대 한) 따라서 뷰 상태가 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-377">The child label1 control inherits this property value (*Inherit* is the default value for *ViewStateMode* for controls.) and therefore saves no view state.</span></span> <span data-ttu-id="3e862-378">PlaceHolder2 컨트롤에서 *ViewStateMode* 로 설정 된 *Enabled*label2이이 속성을 상속 및 뷰 상태를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-378">In the PlaceHolder2 control, *ViewStateMode* is set to *Enabled*, so label2 inherits this property and saves view state.</span></span> <span data-ttu-id="3e862-379">페이지가 처음 로드 되 면 합니다 *텍스트* 속성이 모두 *레이블* 컨트롤 "[DynamicValue]" 문자열로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-379">When the page is first loaded, the *Text* property of both *Label* controls is set to the string "[DynamicValue]".</span></span>

<span data-ttu-id="3e862-380">이러한 설정의 효과 페이지를 처음으로 로드 하는 경우 브라우저에서 다음과 같은 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-380">The effect of these settings is that when the page loads the first time, the following output is displayed in the browser:</span></span>

<span data-ttu-id="3e862-381">사용 안 함 `: [DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="3e862-381">Disabled `: [DynamicValue]`</span></span>

<span data-ttu-id="3e862-382">사용 하도록 설정 합니다.`[DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="3e862-382">Enabled:`[DynamicValue]`</span></span>

<span data-ttu-id="3e862-383">다시 게시 한 후 단, 다음과 같은 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-383">After a postback, however, the following output is displayed:</span></span>

<span data-ttu-id="3e862-384">사용 안 함 `: [DeclaredValue]`</span><span class="sxs-lookup"><span data-stu-id="3e862-384">Disabled `: [DeclaredValue]`</span></span>

<span data-ttu-id="3e862-385">사용 하도록 설정 합니다.`[DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="3e862-385">Enabled:`[DynamicValue]`</span></span>

<span data-ttu-id="3e862-386">Label1 컨트롤 (입니다 *ViewStateMode* 값으로 설정 됩니다 *비활성*) 코드에서 설정 된 값이 유지 되지에 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-386">The label1 control (whose *ViewStateMode* value is set to *Disabled*) has not preserved the value that it was set to in code.</span></span> <span data-ttu-id="3e862-387">하지만 Label2는 제어 (입니다 *ViewStateMode* 값으로 설정 됩니다 *Enabled*) 해당 상태를 유지 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-387">However, the label2 control (whose *ViewStateMode* value is set to *Enabled*) has preserved its state.</span></span>

<span data-ttu-id="3e862-388">설정할 수도 있습니다 *ViewStateMode* 에 *@ Page* 다음 예제와 같이 지시문:</span><span class="sxs-lookup"><span data-stu-id="3e862-388">You can also set *ViewStateMode* in the *@ Page* directive, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample26.aspx)]

<span data-ttu-id="3e862-389">합니다 *페이지* 클래스는 다른 컨트롤, 페이지의 다른 모든 컨트롤에 대 한 부모 컨트롤로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-389">The *Page* class is just another control; it acts as the parent control for all the other controls in the page.</span></span> <span data-ttu-id="3e862-390">기본값인 *ViewStateMode* 됩니다 *Enabled* 에 대 한 인스턴스의 *페이지*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-390">The default value of *ViewStateMode* is *Enabled* for instances of *Page*.</span></span> <span data-ttu-id="3e862-391">컨트롤을 기본값으로 하기 때문에 *상속*, 컨트롤에 상속 됩니다는 *Enabled* 속성 값을 설정 하지 않으면 *ViewStateMode* 페이지나 컨트롤 수준에서.</span><span class="sxs-lookup"><span data-stu-id="3e862-391">Because controls default to *Inherit*, controls will inherit the *Enabled* property value unless you set *ViewStateMode* at page or control level.</span></span>

<span data-ttu-id="3e862-392">값을 *ViewStateMode* 경우에 뷰 상태를 유지 관리 하는 경우 속성에 따라 결정를 *EnableViewState* 속성이로 설정 되어 *true*.</span><span class="sxs-lookup"><span data-stu-id="3e862-392">The value of the *ViewStateMode* property determines if view state is maintained only if the *EnableViewState* property is set to *true*.</span></span> <span data-ttu-id="3e862-393">경우는 *EnableViewState* 속성이 *false*를 뷰 상태를 유지 하지 것입니다 경우에 *ViewStateMode* 로 설정 되어 *사용*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-393">If the *EnableViewState* property is set to *false*, view state will not be maintained even if *ViewStateMode* is set to *Enabled*.</span></span>

<span data-ttu-id="3e862-394">이 기능에 대 한 적절 하 게 사용 된 *ContentPlaceHolder* 컨트롤을 설정할 수 있는 마스터 페이지에서 *ViewStateMode* 하 *비활성화 된* 마스터에 대 한 페이지를 사용 하도록 설정한 에 대해 개별적으로 *ContentPlaceHolder* 필요한 컨트롤에 포함 된 컨트롤 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-394">A good use for this feature is with *ContentPlaceHolder* controls in master pages, where you can set *ViewStateMode* to *Disabled* for the master page and then enable it individually for *ContentPlaceHolder* controls that in turn contain controls that require view state.</span></span>

<a id="0.2__Toc224729035"></a><a id="0.2__Toc253429259"></a><a id="0.2__Toc243304633"></a>

### <a name="changes-to-browser-capabilities"></a><span data-ttu-id="3e862-395">브라우저 기능 변경</span><span class="sxs-lookup"><span data-stu-id="3e862-395">Changes to Browser Capabilities</span></span>

<span data-ttu-id="3e862-396">ASP.NET 사용자 라는 기능을 사용 하 여 사이트를 탐색 하는 데 사용 하는 브라우저의 기능을 결정 *브라우저 기능*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-396">ASP.NET determines the capabilities of the browser that a user is using to browse your site by using a feature called *browser capabilities*.</span></span> <span data-ttu-id="3e862-397">브라우저 기능으로 표시 됩니다는 *HttpBrowserCapabilities* 개체 (의해 노출 되는 *Request.Browser* 속성).</span><span class="sxs-lookup"><span data-stu-id="3e862-397">Browser capabilities are represented by the *HttpBrowserCapabilities* object (exposed by the *Request.Browser* property).</span></span> <span data-ttu-id="3e862-398">예를 들어 사용할 수 있습니다 합니다 *HttpBrowserCapabilities* 유형 및 버전 현재 브라우저의 JavaScript의 특정 버전을 지원 하는지 여부를 결정 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-398">For example, you can use the *HttpBrowserCapabilities* object to determine whether the type and version of the current browser supports a particular version of JavaScript.</span></span> <span data-ttu-id="3e862-399">또는 사용할 수는 *HttpBrowserCapabilities* 모바일 장치에서 요청이 시작 된 여부를 결정 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-399">Or, you can use the *HttpBrowserCapabilities* object to determine whether the request originated from a mobile device.</span></span>

<span data-ttu-id="3e862-400">합니다 *HttpBrowserCapabilities* 개체 브라우저 정의 파일 집합에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-400">The *HttpBrowserCapabilities* object is driven by a set of browser definition files.</span></span> <span data-ttu-id="3e862-401">이러한 파일 특정 브라우저의 기능에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-401">These files contain information about the capabilities of particular browsers.</span></span> <span data-ttu-id="3e862-402">ASP.NET 4에서는 이러한 브라우저 정의 파일 최근에 도입 된 브라우저 및 Google Chrome, 연구 등 동작 BlackBerry 스마트폰을 및 Apple iPhone 장치에 대 한 정보를 포함 하도록 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-402">In ASP.NET 4, these browser definition files have been updated to contain information about recently introduced browsers and devices such as Google Chrome, Research in Motion BlackBerry smartphones, and Apple iPhone.</span></span>

<span data-ttu-id="3e862-403">다음은 새로운 브라우저 정의 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-403">The following list shows new browser definition files:</span></span>

- <span data-ttu-id="3e862-404">*blackberry.browser*</span><span class="sxs-lookup"><span data-stu-id="3e862-404">*blackberry.browser*</span></span>
- <span data-ttu-id="3e862-405">*chrome.browser*</span><span class="sxs-lookup"><span data-stu-id="3e862-405">*chrome.browser*</span></span>
- <span data-ttu-id="3e862-406">*Default.browser*</span><span class="sxs-lookup"><span data-stu-id="3e862-406">*Default.browser*</span></span>
- <span data-ttu-id="3e862-407">*firefox.browser*</span><span class="sxs-lookup"><span data-stu-id="3e862-407">*firefox.browser*</span></span>
- <span data-ttu-id="3e862-408">*gateway.browser*</span><span class="sxs-lookup"><span data-stu-id="3e862-408">*gateway.browser*</span></span>
- <span data-ttu-id="3e862-409">*generic.browser*</span><span class="sxs-lookup"><span data-stu-id="3e862-409">*generic.browser*</span></span>
- <span data-ttu-id="3e862-410">*ie.browser*</span><span class="sxs-lookup"><span data-stu-id="3e862-410">*ie.browser*</span></span>
- <span data-ttu-id="3e862-411">*iemobile.browser*</span><span class="sxs-lookup"><span data-stu-id="3e862-411">*iemobile.browser*</span></span>
- <span data-ttu-id="3e862-412">*iphone.browser*</span><span class="sxs-lookup"><span data-stu-id="3e862-412">*iphone.browser*</span></span>
- <span data-ttu-id="3e862-413">*opera.browser*</span><span class="sxs-lookup"><span data-stu-id="3e862-413">*opera.browser*</span></span>
- <span data-ttu-id="3e862-414">*safari.browser*</span><span class="sxs-lookup"><span data-stu-id="3e862-414">*safari.browser*</span></span>

#### <a name="using-browser-capabilities-providers"></a><span data-ttu-id="3e862-415">브라우저 기능 공급자를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3e862-415">Using Browser Capabilities Providers</span></span>

<span data-ttu-id="3e862-416">Asp.net 버전 3.5 서비스 팩 1에서는 다음과 같은 방법으로 브라우저에 있는 기능을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-416">In ASP.NET version 3.5 Service Pack 1, you can define the capabilities that a browser has in the following ways:</span></span>

- <span data-ttu-id="3e862-417">컴퓨터 수준에서 만들거나 업데이트 한 `.browser` 다음 폴더에 XML 파일:</span><span class="sxs-lookup"><span data-stu-id="3e862-417">At the computer level, you create or update a `.browser` XML file in the following folder:</span></span>

- [!code-console[Main](overview/samples/sample27.cmd)]

- <span data-ttu-id="3e862-418">브라우저 기능을 정의한 후 브라우저 기능 어셈블리를 다시 작성 하 고 GAC에 추가 하기 위해 Visual Studio 명령 프롬프트에서 다음 명령을 실행 하면:</span><span class="sxs-lookup"><span data-stu-id="3e862-418">After you define the browser capability, you run the following command from the Visual Studio Command Prompt in order to rebuild the browser capabilities assembly and add it to the GAC:</span></span>

- [!code-console[Main](overview/samples/sample28.cmd)]

- <span data-ttu-id="3e862-419">만든 개별 응용 프로그램을 `.browser` 응용 프로그램에서 파일 `App_Browsers` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-419">For an individual application, you create a `.browser` file in the application's `App_Browsers` folder.</span></span>

<span data-ttu-id="3e862-420">이러한 접근 방식은 XML 파일을 변경 해야 하 고 컴퓨터 수준 변경에 대 한 다시 시작 해야 응용 프로그램 aspnet를 실행 한 후\_regbrowsers.exe 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-420">These approaches require you to change XML files, and for computer-level changes, you must restart the application after you run the aspnet\_regbrowsers.exe process.</span></span>

<span data-ttu-id="3e862-421">ASP.NET 4 라고 기능이 *브라우저 기능 공급자*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-421">ASP.NET 4 includes a feature referred to as *browser capabilities providers*.</span></span> <span data-ttu-id="3e862-422">이름에서 알 수 있듯이 차례로 수 있는 공급자를 구축할 수이 있습니다가 브라우저 기능을 확인 하려면 사용자 고유의 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-422">As the name suggests, this lets you build a provider that in turn lets you use your own code to determine browser capabilities.</span></span>

<span data-ttu-id="3e862-423">실제로 개발자가 자주 정의 하지 마십시오 사용자 지정 브라우저 기능.</span><span class="sxs-lookup"><span data-stu-id="3e862-423">In practice, developers often do not define custom browser capabilities.</span></span> <span data-ttu-id="3e862-424">브라우저 파일 업데이트 프로세스에 대 한 고 업데이트 하 여 매우 복잡 한 하기가 및에 대 한 XML 구문을 `.browser` 파일 사용 및 정의 하기가 복잡할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-424">Browser files are hard to update, the process for updating them is fairly complicated, and the XML syntax for `.browser` files can be complex to use and define.</span></span> <span data-ttu-id="3e862-425">항목은 훨씬 더 쉽게이 프로세스는 일반적인 브라우저 정의 구문 있다면 또는 최신 브라우저 정의 또는 이러한 데이터베이스에 대 한 웹 서비스까지 포함 된 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-425">What would make this process much easier is if there were a common browser definition syntax, or a database that contained up-to-date browser definitions, or even a Web service for such a database.</span></span> <span data-ttu-id="3e862-426">새 브라우저 기능 공급자 기능을 사용 하면 이러한 시나리오가 가능 하 고 유용 타사 개발자를 위한.</span><span class="sxs-lookup"><span data-stu-id="3e862-426">The new browser capabilities providers feature makes these scenarios possible and practical for third-party developers.</span></span>

<span data-ttu-id="3e862-427">두 가지 주요 새 ASP.NET 4 브라우저 기능 공급자 기능을 사용 합니다: 정의 기능을 ASP.NET 브라우저 기능을 확장 하거나 완전히 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-427">There are two main approaches for using the new ASP.NET 4 browser capabilities provider feature: extending the ASP.NET browser capabilities definition functionality, or totally replacing it.</span></span> <span data-ttu-id="3e862-428">다음 섹션에서는 먼저 기능을 대체 하는 방법을 차례로 확장 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-428">The following sections describe first how to replace the functionality, and then how to extend it.</span></span>

#### <a name="replacing-the-aspnet-browser-capabilities-functionality"></a><span data-ttu-id="3e862-429">ASP.NET 브라우저 기능 기능 대체</span><span class="sxs-lookup"><span data-stu-id="3e862-429">Replacing the ASP.NET Browser Capabilities Functionality</span></span>

<span data-ttu-id="3e862-430">ASP.NET 브라우저 기능 정의 기능을 완전히 대체 하려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-430">To replace the ASP.NET browser capabilities definition functionality completely, follow these steps:</span></span>

1. <span data-ttu-id="3e862-431">파생 되는 공급자 클래스를 만듭니다 *HttpCapabilitiesProvider* 를 재정의 합니다 *GetBrowserCapabilities* 다음 예제와 같이 메서드:</span><span class="sxs-lookup"><span data-stu-id="3e862-431">Create a provider class that derives from *HttpCapabilitiesProvider* and that overrides the *GetBrowserCapabilities* method, as in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample29.cs)]

    <span data-ttu-id="3e862-432">이 예제의 코드를 만듭니다 *HttpBrowserCapabilities* 개체, 브라우저 및 MyCustomBrowser 기능 설정을 라는 기능에만 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-432">The code in this example creates a new *HttpBrowserCapabilities* object, specifying only the capability named browser and setting that capability to MyCustomBrowser.</span></span>
2. <span data-ttu-id="3e862-433">응용 프로그램을 사용 하 여 공급자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-433">Register the provider with the application.</span></span> 

    <span data-ttu-id="3e862-434">응용 프로그램에서 공급자를 사용 하려면 추가 해야 합니다 *공급자* 특성을 *browserCaps* 섹션의 `Web.config` 또는 `Machine.config` 파일.</span><span class="sxs-lookup"><span data-stu-id="3e862-434">In order to use a provider with an application, you must add the *provider* attribute to the *browserCaps* section in the `Web.config` or `Machine.config` files.</span></span> <span data-ttu-id="3e862-435">(공급자 특성을 정의할 수도 있습니다는 *위치* 특정 모바일 장치에 대 한 폴더와 같이 응용 프로그램에서 특정 디렉터리에 대 한 요소입니다.) 다음 예제에서는 설정 하는 방법을 보여 줍니다 합니다 *공급자* 구성 파일의 특성:</span><span class="sxs-lookup"><span data-stu-id="3e862-435">(You can also define the provider attributes in a *location* element for specific directories in application, such as in a folder for a specific mobile device.) The following example shows how to set the *provider* attribute in a configuration file:</span></span>

    [!code-xml[Main](overview/samples/sample30.xml)]

    <span data-ttu-id="3e862-436">새 브라우저 기능 정의 등록 하는 또 다른 방법은 다음 예제에서와 같이 코드를 사용 하는 것:</span><span class="sxs-lookup"><span data-stu-id="3e862-436">Another way to register the new browser capability definition is to use code, as shown in the following example:</span></span>

    [!code-csharp[Main](overview/samples/sample31.cs)]

    <span data-ttu-id="3e862-437">이 코드에서 실행 해야 합니다는 *응용 프로그램\_시작* 이벤트는 `Global.asax` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-437">This code must run in the *Application\_Start* event of the `Global.asax` file.</span></span> <span data-ttu-id="3e862-438">변경 된 *BrowserCapabilitiesProvider* 클래스는 캐시에서 확인 된 유효한 상태의 유지 되는지 확인 하기 위해 응용 프로그램의 코드를 실행 하기 전에 있어야 합니다. *HttpCapabilitiesBase* 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-438">Any change to the *BrowserCapabilitiesProvider* class must occur before any code in the application executes, in order to make sure that the cache remains in a valid state for the resolved *HttpCapabilitiesBase* object.</span></span>

#### <a name="caching-the-httpbrowsercapabilities-object"></a><span data-ttu-id="3e862-439">HttpBrowserCapabilities 개체 캐싱</span><span class="sxs-lookup"><span data-stu-id="3e862-439">Caching the HttpBrowserCapabilities Object</span></span>

<span data-ttu-id="3e862-440">앞의 예제 코드를 얻기 위해 사용자 지정 공급자를 호출할 때마다 실행 하는 한 가지 문제에는 *HttpBrowserCapabilities* 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-440">The preceding example has one problem, which is that the code would run each time the custom provider is invoked in order to get the *HttpBrowserCapabilities* object.</span></span> <span data-ttu-id="3e862-441">이 하면 각 요청 하는 동안 여러 번 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-441">This can happen multiple times during each request.</span></span> <span data-ttu-id="3e862-442">예제에서는 공급자에 대 한 코드를 수행 하지 않습니다 대부분.</span><span class="sxs-lookup"><span data-stu-id="3e862-442">In the example, the code for the provider does not do much.</span></span> <span data-ttu-id="3e862-443">그러나 사용자 지정 공급자의 코드에서 중요 한 작업을 수행 하는 경우를 얻기 위해 합니다 *HttpBrowserCapabilities* 개체 성능에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-443">However, if the code in your custom provider performs significant work in order to get the *HttpBrowserCapabilities* object, this can affect performance.</span></span> <span data-ttu-id="3e862-444">이 방지 하기를 캐시할 수 있습니다 합니다 *HttpBrowserCapabilities* 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-444">To prevent this from happening, you can cache the *HttpBrowserCapabilities* object.</span></span> <span data-ttu-id="3e862-445">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-445">Follow these steps:</span></span>

1. <span data-ttu-id="3e862-446">파생 되는 클래스를 만듭니다 *HttpCapabilitiesProvider*, 다음 예제에서와 같은:</span><span class="sxs-lookup"><span data-stu-id="3e862-446">Create a class that derives from *HttpCapabilitiesProvider*, like the one in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample32.cs)]

    <span data-ttu-id="3e862-447">예제에서는 코드는 사용자 지정 BuildCacheKey 메서드를 호출 하 여 캐시 키를 생성 및 사용자 지정 GetCacheTime 메서드를 호출 하 여 캐시 기간을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-447">In the example, the code generates a cache key by calling a custom BuildCacheKey method, and it gets the length of time to cache by calling a custom GetCacheTime method.</span></span> <span data-ttu-id="3e862-448">코드를 다음 확인 된 추가 *HttpBrowserCapabilities* 캐시 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-448">The code then adds the resolved *HttpBrowserCapabilities* object to the cache.</span></span> <span data-ttu-id="3e862-449">개체를 캐시에서 검색에 다시 확인 하는 후속 요청 사용자 지정 공급자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-449">The object can be retrieved from the cache and reused on subsequent requests that make use of the custom provider.</span></span>
2. <span data-ttu-id="3e862-450">앞의 절차에 설명 된 대로 응용 프로그램을 사용 하 여 공급자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-450">Register the provider with the application as described in the preceding procedure.</span></span>

#### <a name="extending-aspnet-browser-capabilities-functionality"></a><span data-ttu-id="3e862-451">ASP.NET 브라우저 기능 기능 확장</span><span class="sxs-lookup"><span data-stu-id="3e862-451">Extending ASP.NET Browser Capabilities Functionality</span></span>

<span data-ttu-id="3e862-452">이전 섹션에는 새 하는 방법을 설명 *HttpBrowserCapabilities* ASP.NET 4에는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-452">The previous section described how to create a new *HttpBrowserCapabilities* object in ASP.NET 4.</span></span> <span data-ttu-id="3e862-453">또한 ASP.NET에 포함 되어 있는 항목에 새 브라우저 기능 정의 추가 하 여 ASP.NET 브라우저 기능 기능을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-453">You can also extend the ASP.NET browser capabilities functionality by adding new browser capabilities definitions to those that are already in ASP.NET.</span></span> <span data-ttu-id="3e862-454">XML 브라우저 정의 사용 하지 않고이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-454">You can do this without using the XML browser definitions.</span></span> <span data-ttu-id="3e862-455">다음 절차에 표시 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-455">The following procedure shows how.</span></span>

1. <span data-ttu-id="3e862-456">파생 되는 클래스를 만듭니다 *HttpCapabilitiesEvaluator* 를 재정의 합니다 *GetBrowserCapabilities* 메서드를 다음 예제에서와 같이:</span><span class="sxs-lookup"><span data-stu-id="3e862-456">Create a class that derives from *HttpCapabilitiesEvaluator* and that overrides the *GetBrowserCapabilities* method, as shown in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample33.cs)]

    <span data-ttu-id="3e862-457">이 코드는 먼저 브라우저를 확인 하기 위해 ASP.NET 브라우저 기능 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-457">This code first uses the ASP.NET browser capabilities functionality to try to identify the browser.</span></span> <span data-ttu-id="3e862-458">그러나 브라우저 없음이 확인 되 면 정보를 기반으로 요청에 정의 된 (즉, 합니다 *브라우저* 의 속성을 *HttpBrowserCapabilities* 개체는 문자열 "Unknown"), 호출 사용자 지정 공급자 (MyBrowserCapabilitiesEvaluator) 브라우저를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-458">However, if no browser is identified based on the information defined in the request (that is, if the *Browser* property of the *HttpBrowserCapabilities* object is the string "Unknown"), the code calls the custom provider (MyBrowserCapabilitiesEvaluator) to identify the browser.</span></span>
2. <span data-ttu-id="3e862-459">이전 예제에 설명 된 대로 응용 프로그램을 사용 하 여 공급자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-459">Register the provider with the application as described in the previous example.</span></span>

#### <a name="extending-browser-capabilities-functionality-by-adding-new-capabilities-to-existing-capabilities-definitions"></a><span data-ttu-id="3e862-460">기존 기능 정의에 새 기능을 추가 하 여 브라우저 기능 기능 확장</span><span class="sxs-lookup"><span data-stu-id="3e862-460">Extending Browser Capabilities Functionality by Adding New Capabilities to Existing Capabilities Definitions</span></span>

<span data-ttu-id="3e862-461">사용자 지정 브라우저 정의가 공급자를 만드는 것 외에도 하 고 새 브라우저 정의 동적으로 만드는 추가 기능을 사용 하 여 기존 브라우저 정의 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-461">In addition to creating a custom browser definition provider and to dynamically creating new browser definitions, you can extend existing browser definitions with additional capabilities.</span></span> <span data-ttu-id="3e862-462">이렇게 하면 원하는 근접 하지만 몇 가지 기능만 없는 정의 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-462">This lets you use a definition that is close to what you want but lacks only a few capabilities.</span></span> <span data-ttu-id="3e862-463">이렇게 하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-463">To do this, use the following steps.</span></span>

1. <span data-ttu-id="3e862-464">파생 되는 클래스를 만듭니다 *HttpCapabilitiesEvaluator* 를 재정의 합니다 *GetBrowserCapabilities* 메서드를 다음 예제에서와 같이:</span><span class="sxs-lookup"><span data-stu-id="3e862-464">Create a class that derives from *HttpCapabilitiesEvaluator* and that overrides the *GetBrowserCapabilities* method, as shown in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample34.cs)]

    <span data-ttu-id="3e862-465">예제 코드는 기존 ASP.NET 확장 *HttpCapabilitiesEvaluator* 클래스 및 가져옵니다 합니다 *HttpBrowserCapabilities* 현재 요청 정의 다음 코드를 사용 하 여 일치 하는 개체 :</span><span class="sxs-lookup"><span data-stu-id="3e862-465">The example code extends the existing ASP.NET *HttpCapabilitiesEvaluator* class and gets the *HttpBrowserCapabilities* object that matches the current request definition by using the following code:</span></span>

    [!code-csharp[Main](overview/samples/sample35.cs)]

    <span data-ttu-id="3e862-466">다음 코드를 추가 하거나이 브라우저에 대 한 기능을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-466">The code can then add or modify a capability for this browser.</span></span> <span data-ttu-id="3e862-467">두 가지 방법으로 새로운 브라우저 기능을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-467">There are two ways to specify a new browser capability:</span></span>

    - <span data-ttu-id="3e862-468">에 키/값 쌍을 추가 합니다 *IDictionary* 개체에서 노출 되는 *기능* 속성의는 *HttpCapabilitiesBase* 개체.</span><span class="sxs-lookup"><span data-stu-id="3e862-468">Add a key/value pair to the *IDictionary* object that is exposed by the *Capabilities* property of the *HttpCapabilitiesBase* object.</span></span> <span data-ttu-id="3e862-469">이전 예제에서는 코드의 값을 사용 하 여 다중 터치 라는 기능을 추가 *true*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-469">In the previous example, the code adds a capability named MultiTouch with a value of *true*.</span></span>
    - <span data-ttu-id="3e862-470">기존 속성을 설정 합니다 *HttpCapabilitiesBase* 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-470">Set existing properties of the *HttpCapabilitiesBase* object.</span></span> <span data-ttu-id="3e862-471">이전 예제에서 코드를 설정 합니다 *프레임* 속성을 *true*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-471">In the previous example, the code sets the *Frames* property to *true*.</span></span> <span data-ttu-id="3e862-472">이 속성은 단순히에 대 한 접근자를 *IDictionary* 에 의해 노출 되는 개체를 *기능* 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-472">This property is simply an accessor for the *IDictionary* object that is exposed by the *Capabilities* property.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="3e862-473">이 모델의 모든 속성에 적용 됩니다 *HttpBrowserCapabilities*를 컨트롤 어댑터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-473">Note This model applies to any property of *HttpBrowserCapabilities*, including control adapters.</span></span>
2. <span data-ttu-id="3e862-474">이전 절차에서 설명 된 대로 응용 프로그램을 사용 하 여 공급자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-474">Register the provider with the application as described in the earlier procedure.</span></span>

<a id="0.2__Toc224729036"></a><a id="0.2__Toc253429260"></a><a id="0.2__Toc243304634"></a>

### <a name="routing-in-aspnet-4"></a><span data-ttu-id="3e862-475">ASP.NET 4에서 라우팅</span><span class="sxs-lookup"><span data-stu-id="3e862-475">Routing in ASP.NET 4</span></span>

<span data-ttu-id="3e862-476">ASP.NET 4 Web Forms를 사용 하 여 라우팅을 사용 하는 것에 대 한 기본 제공 지원을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-476">ASP.NET 4 adds built-in support for using routing with Web Forms.</span></span> <span data-ttu-id="3e862-477">적용할 응용 프로그램을 구성 하는 라우팅 하면 실제 파일에 매핑되지 않는 Url을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-477">Routing lets you configure an application to accept request URLs that do not map to physical files.</span></span> <span data-ttu-id="3e862-478">대신, 라우팅 Url을 사용자에 게 의미 하 고 응용 프로그램에 대 한 검색 엔진 최적화 (SEO)를 사용 하 여 도움이 되는 정의를 사용할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-478">Instead, you can use routing to define URLs that are meaningful to users and that can help with search-engine optimization (SEO) for your application.</span></span> <span data-ttu-id="3e862-479">예를 들어 기존 응용 프로그램의 제품 범주를 표시 하는 페이지의 URL을 다음과 같이 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-479">For example, the URL for a page that displays product categories in an existing application might look like the following example:</span></span>

[!code-console[Main](overview/samples/sample36.cmd)]

<span data-ttu-id="3e862-480">라우팅를 사용 하 여 동일한 정보를 렌더링 하는 다음 URL을 허용 하도록 응용 프로그램을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-480">By using routing, you can configure the application to accept the following URL to render the same information:</span></span>

[!code-console[Main](overview/samples/sample37.cmd)]

<span data-ttu-id="3e862-481">라우팅 ASP.NET 3.5 SP1부터 제공 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-481">Routing has been available starting with ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="3e862-482">(ASP.NET 3.5 SP1의 라우팅을 사용 하는 방법의 예에 대 한 항목을 참조 하세요 [WebForms 사용 하 여 라우팅 사용 하 여](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "이 항목의 제목입니다.")</span><span class="sxs-lookup"><span data-stu-id="3e862-482">(For an example of how to use routing in ASP.NET 3.5 SP1, see the entry [Using Routing With WebForms](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "Title of this entry.")</span></span> <span data-ttu-id="3e862-483">Phil Haack의 블로그에서.) 그러나 ASP.NET 4는 다음과 같은 쉽게 라우팅을 사용 하는 몇 가지 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-483">on Phil Haack's blog.) However, ASP.NET 4 includes some features that make it easier to use routing, including the following:</span></span>

- <span data-ttu-id="3e862-484">합니다 *PageRouteHandler* 경로 정의할 때 사용 하는 간단한 HTTP 처리기 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-484">The *PageRouteHandler* class, which is a simple HTTP handler that you use when you define routes.</span></span> <span data-ttu-id="3e862-485">클래스는 요청으로 라우팅되는 페이지에 데이터를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-485">The class passes data to the page that the request is routed to.</span></span>
- <span data-ttu-id="3e862-486">새 속성 *HttpRequest.RequestContext* 하 고 *Page.RouteData* (에 대 한 프록시는 합니다 *HttpRequest.RequestContext.RouteData* 개체).</span><span class="sxs-lookup"><span data-stu-id="3e862-486">The new properties *HttpRequest.RequestContext* and *Page.RouteData* (which is a proxy for the *HttpRequest.RequestContext.RouteData* object).</span></span> <span data-ttu-id="3e862-487">이러한 속성 쉽게 경로에서 전달 되는 정보에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-487">These properties make it easier to access information that is passed from the route.</span></span>
- <span data-ttu-id="3e862-488">다음 새 식 작성기에 정의 된 *System.Web.Compilation.RouteUrlExpressionBuilder* 하 고 *System.Web.Compilation.RouteValueExpressionBuilder*:</span><span class="sxs-lookup"><span data-stu-id="3e862-488">The following new expression builders, which are defined in *System.Web.Compilation.RouteUrlExpressionBuilder* and *System.Web.Compilation.RouteValueExpressionBuilder*:</span></span>
- <span data-ttu-id="3e862-489">*RouteUrl*, ASP.NET 서버 컨트롤 내에서 경로 URL에 해당 하는 URL을 만드는 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-489">*RouteUrl*, which provides a simple way to create a URL that corresponds to a route URL within an ASP.NET server control.</span></span>
- <span data-ttu-id="3e862-490">*RouteValue*에서 정보를 추출 하는 간단한 방법을 제공 합니다 *RouteContext* 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-490">*RouteValue*, which provides a simple way to extract information from the *RouteContext* object.</span></span>
- <span data-ttu-id="3e862-491">합니다 *RouteParameter* 쉽게에 포함 된 데이터를 전달 하는 클래스를 *RouteContext* 개체 데이터 소스 컨트롤에 대 한 쿼리를 (비슷합니다 [ *FormParameter* ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)).</span><span class="sxs-lookup"><span data-stu-id="3e862-491">The *RouteParameter* class, which makes it easier to pass data contained in a *RouteContext* object to a query for a data source control (similar to [*FormParameter*](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)).</span></span>

#### <a name="routing-for-web-forms-pages"></a><span data-ttu-id="3e862-492">Web Forms 페이지에 대 한 라우팅</span><span class="sxs-lookup"><span data-stu-id="3e862-492">Routing for Web Forms Pages</span></span>

<span data-ttu-id="3e862-493">다음 예제에서는 새을 사용 하 여 Web Forms 경로 정의 하는 방법을 보여 줍니다 *MapPageRoute* 메서드는 *경로* 클래스:</span><span class="sxs-lookup"><span data-stu-id="3e862-493">The following example shows how to define a Web Forms route by using the new *MapPageRoute* method of the *Route* class:</span></span>

[!code-csharp[Main](overview/samples/sample38.cs)]

<span data-ttu-id="3e862-494">ASP.NET 4 소개 합니다 *MapPageRoute* 메서드.</span><span class="sxs-lookup"><span data-stu-id="3e862-494">ASP.NET 4 introduces the *MapPageRoute* method.</span></span> <span data-ttu-id="3e862-495">다음 예제에서는 이전 예에서 같이 SearchRoute 정의에 동일 하지만 사용 하 여 *PageRouteHandler* 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-495">The following example is equivalent to the SearchRoute definition shown in the previous example, but uses the *PageRouteHandler* class.</span></span>

[!code-csharp[Main](overview/samples/sample39.cs)]

<span data-ttu-id="3e862-496">예제에서 코드를 물리적 페이지에 경로 매핑합니다 (첫 번째 경로를 `~/search.aspx`).</span><span class="sxs-lookup"><span data-stu-id="3e862-496">The code in the example maps the route to a physical page (in the first route, to `~/search.aspx`).</span></span> <span data-ttu-id="3e862-497">첫 번째 경로 정의는 또한 searchterm 라는 매개 변수에 URL에서 추출 하는 페이지에 전달 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-497">The first route definition also specifies that the parameter named searchterm should be extracted from the URL and passed to the page.</span></span>

<span data-ttu-id="3e862-498">합니다 *MapPageRoute* 메서드는 다음 메서드 오버 로드를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-498">The *MapPageRoute* method supports the following method overloads:</span></span>

- <span data-ttu-id="3e862-499">*MapPageRoute (문자열 routeName, 문자열 routeUrl, 문자열 physicalFile, bool checkPhysicalUrlAccess)*</span><span class="sxs-lookup"><span data-stu-id="3e862-499">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess)*</span></span>
- <span data-ttu-id="3e862-500">*MapPageRoute (문자열 routeName, 문자열 routeUrl, 문자열 physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary 기본값)*</span><span class="sxs-lookup"><span data-stu-id="3e862-500">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary defaults)*</span></span>
- <span data-ttu-id="3e862-501">*MapPageRoute (문자열 routeName, 문자열 routeUrl, 문자열 physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary 기본값, RouteValueDictionary 제약 조건)*</span><span class="sxs-lookup"><span data-stu-id="3e862-501">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary defaults, RouteValueDictionary constraints)*</span></span>

<span data-ttu-id="3e862-502">합니다 *checkPhysicalUrlAccess* 매개 변수 경로으로 라우팅되지 물리적 페이지에 대 한 보안 권한을 확인 해야 하는지 여부를 지정 합니다 (이 예제의 경우 search.aspx) 들어오는 URL에 대 한 권한과 (이 경우 검색 / {searchterm}).</span><span class="sxs-lookup"><span data-stu-id="3e862-502">The *checkPhysicalUrlAccess* parameter specifies whether the route should check the security permissions for the physical page being routed to (in this case, search.aspx) and the permissions on the incoming URL (in this case, search/{searchterm}).</span></span> <span data-ttu-id="3e862-503">경우 값 *checkPhysicalUrlAccess* 됩니다 *false*, 들어오는 URL의 사용 권한만 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-503">If the value of *checkPhysicalUrlAccess* is *false*, only the permissions of the incoming URL will be checked.</span></span> <span data-ttu-id="3e862-504">에 정의 된 이러한 권한을 `Web.config` 다음과 같은 설정을 사용 하는 파일:</span><span class="sxs-lookup"><span data-stu-id="3e862-504">These permissions are defined in the `Web.config` file using settings such as the following:</span></span>

[!code-xml[Main](overview/samples/sample40.xml)]

<span data-ttu-id="3e862-505">예제 구성에서는 액세스가 거부 되었습니다 물리적 페이지에 `search.aspx` 관리자 역할이 있는 사용자를 제외한 모든 사용자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-505">In the example configuration, access is denied to the physical page `search.aspx` for all users except those who are in the admin role.</span></span> <span data-ttu-id="3e862-506">경우는 *checkPhysicalUrlAccess* 매개 변수는 설정 *true* (기본값) 인 관리 사용자만 액세스할 수 있습니다 URL /search/ {searchterm} 물리적 페이지 search.aspx 이므로 해당 역할의 사용자에 게 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-506">When the *checkPhysicalUrlAccess* parameter is set to *true* (which is its default value), only admin users are allowed to access the URL /search/{searchterm}, because the physical page search.aspx is restricted to users in that role.</span></span> <span data-ttu-id="3e862-507">하는 경우 *checkPhysicalUrlAccess* 로 설정 된 *false* 하 고 이전 예제와 같이 사이트를 구성 하 고 모든 인증 된 사용자 URL /search/ {searchterm}에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-507">If *checkPhysicalUrlAccess* is set to *false* and the site is configured as shown in the previous example, all authenticated users are allowed to access the URL /search/{searchterm}.</span></span>

#### <a name="reading-routing-information-in-a-web-forms-page"></a><span data-ttu-id="3e862-508">Web Forms 페이지에서 라우팅 정보 읽기</span><span class="sxs-lookup"><span data-stu-id="3e862-508">Reading Routing Information in a Web Forms Page</span></span>

<span data-ttu-id="3e862-509">Web Forms 물리적 페이지의 코드에서 URL에서 추출 된 라우팅 정보에 액세스할 수 있습니다 (또는 다른 개체를 추가 하는 기타 정보를 *RouteData* 개체) 두 개의 새로운 속성을 사용 하 여:  *HttpRequest.RequestContext* 하 고 *Page.RouteData*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-509">In the code of the Web Forms physical page, you can access the information that routing has extracted from the URL (or other information that another object has added to the *RouteData* object) by using two new properties: *HttpRequest.RequestContext* and *Page.RouteData*.</span></span> <span data-ttu-id="3e862-510">(*Page.RouteData* 래핑합니다 *HttpRequest.RequestContext.RouteData*.) 다음 예제에서는 사용 하는 방법을 보여 줍니다 *Page.RouteData*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-510">(*Page.RouteData* wraps *HttpRequest.RequestContext.RouteData*.) The following example shows how to use *Page.RouteData*.</span></span>

[!code-csharp[Main](overview/samples/sample41.cs)]

<span data-ttu-id="3e862-511">이전 예제에서는 경로에 정의 된 대로 지정 하려면 매개 변수에 전달 된 값을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-511">The code extracts the value that was passed for the searchterm parameter, as defined in the example route earlier.</span></span> <span data-ttu-id="3e862-512">다음 요청 URL을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-512">Consider the following request URL:</span></span>

[!code-console[Main](overview/samples/sample42.cmd)]

<span data-ttu-id="3e862-513">경우이 요청이 "scott"에서 렌더링할 수는 단어를 `search.aspx` 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-513">When this request is made, the word "scott" would be rendered in the `search.aspx` page.</span></span>

#### <a name="accessing-routing-information-in-markup"></a><span data-ttu-id="3e862-514">태그의 라우팅 정보에 액세스</span><span class="sxs-lookup"><span data-stu-id="3e862-514">Accessing Routing Information in Markup</span></span>

<span data-ttu-id="3e862-515">이전 섹션에서 설명 하는 방법을 Web Forms 페이지의 코드에서 경로 데이터를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-515">The method described in the previous section shows how to get route data in code in a Web Forms page.</span></span> <span data-ttu-id="3e862-516">또한 태그에서 같은 정보에 액세스할 수 있는 식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-516">You can also use expressions in markup that give you access to the same information.</span></span> <span data-ttu-id="3e862-517">식 작성기는 선언적 코드를 사용 하는 강력 하 고 세련 된 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-517">Expression builders are a powerful and elegant way to work with declarative code.</span></span> <span data-ttu-id="3e862-518">(자세한 내용은 항목을 참조 하세요 [Express 직접 사용 하 여 사용자 지정 식 작성기](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx) Phil Haack의 블로그에서.)</span><span class="sxs-lookup"><span data-stu-id="3e862-518">(For more information, see the entry [Express Yourself With Custom Expression Builders](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx) on Phil Haack's blog.)</span></span>

<span data-ttu-id="3e862-519">ASP.NET 4 Web Forms에 라우팅에 대 한 두 명의 새 식 작성기를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-519">ASP.NET 4 includes two new expression builders for Web Forms routing.</span></span> <span data-ttu-id="3e862-520">다음 예제에서는 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-520">The following example shows how to use them.</span></span>

[!code-aspx[Main](overview/samples/sample43.aspx)]

<span data-ttu-id="3e862-521">예에서는 *RouteUrl* 식은 경로 매개 변수를 기반으로 하는 URL을 정의 하는데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-521">In the example, the *RouteUrl* expression is used to define a URL that is based on a route parameter.</span></span> <span data-ttu-id="3e862-522">이 태그에 전체 URL 하드 코딩 하지 않아도 수를 저장 하 고이 링크를 변경 하지 않고도 URL 구조를 나중에 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-522">This saves you from having to hard-code the complete URL into the markup, and lets you change the URL structure later without requiring any change to this link.</span></span>

<span data-ttu-id="3e862-523">앞에서 정의한 경로 따라이 태그는 다음 URL을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-523">Based on the route defined earlier, this markup generates the following URL:</span></span>

[!code-console[Main](overview/samples/sample44.cmd)]

<span data-ttu-id="3e862-524">ASP.NET 올바른 경로 자동으로 작동 (즉, 올바른 URL을 생성) 입력된 매개 변수를 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-524">ASP.NET automatically works out the correct route (that is, it generates the correct URL) based on the input parameters.</span></span> <span data-ttu-id="3e862-525">또한를 사용 하 여에 대 한 경로 지정할 수 있는 식에서 경로 이름을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-525">You can also include a route name in the expression, which lets you specify a route to use.</span></span>

<span data-ttu-id="3e862-526">다음 예제에서는 사용 하는 방법을 보여 줍니다 합니다 *RouteValue* 식입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-526">The following example shows how to use the *RouteValue* expression.</span></span>

[!code-aspx[Main](overview/samples/sample45.aspx)]

<span data-ttu-id="3e862-527">이 컨트롤이 포함 된 페이지를 실행 하는 경우 "scott" 값이 레이블에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-527">When the page that contains this control runs, the value "scott" is displayed in the label.</span></span>

<span data-ttu-id="3e862-528">합니다 *RouteValue* 식 손쉽게 태그에서 경로 데이터를 사용 하 고 더 복잡 한 Page.RouteData["x 작업할 것을 방지 하기"] 태그의 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-528">The *RouteValue* expression makes it simple to use route data in markup, and it avoids having to work with the more complex Page.RouteData["x"] syntax in markup.</span></span>

#### <a name="using-route-data-for-data-source-control-parameters"></a><span data-ttu-id="3e862-529">경로 데이터를 사용 하 여 데이터 원본에 대 한 제어 매개 변수</span><span class="sxs-lookup"><span data-stu-id="3e862-529">Using Route Data for Data Source Control Parameters</span></span>

<span data-ttu-id="3e862-530">합니다 *RouteParameter* 클래스를 사용 하면 데이터 소스 컨트롤에서 쿼리에 대 한 매개 변수 값으로 경로 데이터를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-530">The *RouteParameter* class lets you specify route data as a parameter value for queries in a data source control.</span></span> <span data-ttu-id="3e862-531">것 [훨씬 처럼 작동 합니다](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx) 다음 예와에서 같이 클래스:</span><span class="sxs-lookup"><span data-stu-id="3e862-531">It [works much like the](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx) class, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample46.aspx)]

<span data-ttu-id="3e862-532">경로 매개 변수 지정 하려면 값에 사용할이 경우에 @companyname 에서 매개 변수를 <em>선택</em> 문입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-532">In this case, the value of the route parameter searchterm will be used for the @companyname parameter in the <em>Select</em> statement.</span></span>

<a id="0.2__Toc224729037"></a><a id="0.2__Toc253429261"></a><a id="0.2__Toc243304635"></a>

### <a name="setting-client-ids"></a><span data-ttu-id="3e862-533">클라이언트 Id를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-533">Setting Client IDs</span></span>

<span data-ttu-id="3e862-534">새 *ClientIDMode* ASP.NET에서 장기 문제를 해결 하는 속성 즉 만들려면 어떻게 해야 컨트롤을 *id* 렌더링 하는 요소에 대 한 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-534">The new *ClientIDMode* property addresses a long-standing issue in ASP.NET, namely how controls create the *id* attribute for elements that they render.</span></span> <span data-ttu-id="3e862-535">알면 합니다 *id* 렌더링 된 요소에 대 한 특성은 응용 프로그램에 이러한 요소를 참조 하는 클라이언트 스크립트를 포함 하는 경우에 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-535">Knowing the *id* attribute for rendered elements is important if your application includes client script that references these elements.</span></span>

<span data-ttu-id="3e862-536">합니다 *id* 웹 서버 컨트롤의 렌더링 된 HTML의 특성에 따라 생성 되는 *ClientID* 컨트롤의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-536">The *id* attribute in HTML that is rendered for Web server controls is generated based on the *ClientID* property of the control.</span></span> <span data-ttu-id="3e862-537">ASP.NET 4에서 생성 하는 알고리즘까지 합니다 *id* 에서 특성을 *ClientID* 속성 ID를 사용 하 여 및 (반복 된 컨트롤의 경우 (해당 되는 경우)의 명명 컨테이너를 연결 했습니다 데이터 컨트롤) 접두사 및 일련 번호를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-537">Until ASP.NET 4, the algorithm for generating the *id* attribute from the *ClientID* property has been to concatenate the naming container (if any) with the ID, and in the case of repeated controls (as in data controls), to add a prefix and a sequential number.</span></span> <span data-ttu-id="3e862-538">이 항상 보장 페이지에서 컨트롤의 Id는 고유 하는 동안 컨트롤 Id는 예측할 수 없습니다 및 클라이언트 스크립트에서 참조 하기 어려웠습니다 따라서 알고리즘이 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-538">While this has always guaranteed that the IDs of controls in the page are unique, the algorithm has resulted in control IDs that were not predictable, and were therefore difficult to reference in client script.</span></span>

<span data-ttu-id="3e862-539">새 *ClientIDMode* 속성을 사용 하면 클라이언트 ID가 컨트롤에 대 한 생성 하는 방법에 더 정확 하 게 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-539">The new *ClientIDMode* property lets you specify more precisely how the client ID is generated for controls.</span></span> <span data-ttu-id="3e862-540">설정할 수 있습니다 합니다 *ClientIDMode* 페이지에 대 한 포함 하는 모든 컨트롤에 대 한 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-540">You can set the *ClientIDMode* property for any control, including for the page.</span></span> <span data-ttu-id="3e862-541">가능한 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-541">Possible settings are the following:</span></span>

- <span data-ttu-id="3e862-542">*AutoID* – 생성 하는 알고리즘을 동일 *ClientID* 이전 버전의 ASP.NET에서 사용 된 속성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-542">*AutoID* – This is equivalent to the algorithm for generating *ClientID* property values that was used in earlier versions of ASP.NET.</span></span>
- <span data-ttu-id="3e862-543">*정적* –이 지정 된 *ClientID* 값 부모 명명 컨테이너의 Id를 연결 하지 않고 ID와 동일 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-543">*Static* – This specifies that the *ClientID* value will be the same as the ID without concatenating the IDs of parent naming containers.</span></span> <span data-ttu-id="3e862-544">이 웹 사용자 컨트롤에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-544">This can be useful in Web user controls.</span></span> <span data-ttu-id="3e862-545">웹 사용자 정의 컨트롤을 다른 컨테이너 컨트롤의 여러 페이지에 있는 수에 있기 때문에 어려울 수 있습니다 사용 하는 컨트롤에 대 한 클라이언트 스크립트를 작성 합니다 *AutoID* 알고리즘 ID 값을 예측할 수 없습니다. .</span><span class="sxs-lookup"><span data-stu-id="3e862-545">Because a Web user control can be located on different pages and in different container controls, it can be difficult to write client script for controls that use the *AutoID* algorithm because you cannot predict what the ID values will be.</span></span>
- <span data-ttu-id="3e862-546">*예측 가능한* –이 옵션은 주로 반복 템플릿을 사용 하는 데이터 컨트롤에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-546">*Predictable* – This option is primarily for use in data controls that use repeating templates.</span></span> <span data-ttu-id="3e862-547">하지만 생성 된 컨트롤의 명명 컨테이너의 ID 속성을 연결 *ClientID* 값 "ctlxxx"과 같은 문자열을 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-547">It concatenates the ID properties of the control's naming containers, but generated *ClientID* values do not contain strings like "ctlxxx".</span></span> <span data-ttu-id="3e862-548">이 설정을 사용 하 여 함께 작동 하는 *ClientIDRowSuffix* 컨트롤의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-548">This setting works in conjunction with the *ClientIDRowSuffix* property of the control.</span></span> <span data-ttu-id="3e862-549">설정 된 *ClientIDRowSuffix* 생성 된 속성 데이터 필드의 이름 및 해당 필드의 값을 접미사로 사용 됩니다 *ClientID* 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-549">You set the *ClientIDRowSuffix* property to the name of a data field, and the value of that field is used as the suffix for the generated *ClientID* value.</span></span> <span data-ttu-id="3e862-550">일반적으로 데이터 레코드의 기본 키 사용 합니다 *ClientIDRowSuffix* 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-550">Typically you would use the primary key of a data record as the *ClientIDRowSuffix* value.</span></span>
- <span data-ttu-id="3e862-551">*상속* –이 설정은 컨트롤에 대 한 기본 동작 이므로 컨트롤의 ID를 생성이 해당 부모와 동일한 지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-551">*Inherit* – This setting is the default behavior for controls; it specifies that a control's ID generation is the same as its parent.</span></span>

<span data-ttu-id="3e862-552">설정할 수 있습니다 합니다 *ClientIDMode* 페이지 수준 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-552">You can set the *ClientIDMode* property at the page level.</span></span> <span data-ttu-id="3e862-553">기본값 정의 *ClientIDMode* 현재 페이지에 있는 모든 컨트롤에 대 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-553">This defines the default *ClientIDMode* value for all controls in the current page.</span></span>

<span data-ttu-id="3e862-554">기본값 *ClientIDMode* 페이지 수준에서 값이 *AutoID*, 및 기본값 *ClientIDMode* 제어 수준에는 값은 *상속*.</span><span class="sxs-lookup"><span data-stu-id="3e862-554">The default *ClientIDMode* value at the page level is *AutoID*, and the default *ClientIDMode* value at the control level is *Inherit*.</span></span> <span data-ttu-id="3e862-555">결과적으로, 코드에서 아무 곳 이나이 속성을 설정 하지 않으면, 모든 컨트롤은 기본적으로 *AutoID* 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-555">As a result, if you do not set this property anywhere in your code, all controls will default to the *AutoID* algorithm.</span></span>

<span data-ttu-id="3e862-556">페이지 수준 값을 설정 합니다 *@ Page* 지시문을 다음 예와에서 같이:</span><span class="sxs-lookup"><span data-stu-id="3e862-556">You set the page-level value in the *@ Page* directive, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample47.aspx)]

<span data-ttu-id="3e862-557">설정할 수도 있습니다는 *ClientIDMode* 컴퓨터 수준 또는 응용 프로그램 수준 구성 파일의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-557">You can also set the *ClientIDMode* value in the configuration file, either at the computer (machine) level or at the application level.</span></span> <span data-ttu-id="3e862-558">기본값 정의 *ClientIDMode* 응용 프로그램의 모든 페이지에서 모든 컨트롤에 대 한 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-558">This defines the default *ClientIDMode* setting for all controls in all pages in the application.</span></span> <span data-ttu-id="3e862-559">기본 컴퓨터 수준에서 값을 설정 하는 경우 정의 *ClientIDMode* 해당 컴퓨터에서 모든 웹 사이트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-559">If you set the value at the computer level, it defines the default *ClientIDMode* setting for all Web sites on that computer.</span></span> <span data-ttu-id="3e862-560">다음 예제와 합니다 *ClientIDMode* 구성 파일에서 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-560">The following example shows the *ClientIDMode* setting in the configuration file:</span></span>

[!code-xml[Main](overview/samples/sample48.xml)]

<span data-ttu-id="3e862-561">값을 앞에서 설명한 대로 합니다 *ClientID* 속성은 컨트롤의 부모에 대 한 명명 컨테이너에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-561">As noted earlier, the value of the *ClientID* property is derived from the naming container for a control's parent.</span></span> <span data-ttu-id="3e862-562">마스터 페이지를 사용 하는 경우와 같은 일부 시나리오에서는 컨트롤 수 결국 Id를 사용 하 여 다음과 같은 HTML 렌더링:</span><span class="sxs-lookup"><span data-stu-id="3e862-562">In some scenarios, such as when you are using master pages, controls can end up with IDs like those in the following rendered HTML:</span></span>

[!code-html[Main](overview/samples/sample49.html)]

<span data-ttu-id="3e862-563">도 *입력* 태그에 표시 된 요소 (에서 *텍스트 상자* 컨트롤) 두 개의 명명 컨테이너는 페이지에서 심층 (중첩 된 *ContentPlaceholder* 컨트롤), 마스터 페이지를 처리 하는 방식으로 인해 최종 결과 다음과 같은 컨트롤 ID는:</span><span class="sxs-lookup"><span data-stu-id="3e862-563">Even though the *input* element shown in the markup (from a *TextBox* control) is only two naming containers deep in the page (the nested *ContentPlaceholder* controls), because of the way master pages are processed, the end result is a control ID like the following:</span></span>

[!code-console[Main](overview/samples/sample50.cmd)]

<span data-ttu-id="3e862-564">이 ID 페이지에서 고유성이 보장 됩니다 이지만 불필요 하 게 대부분의 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-564">This ID is guaranteed to be unique in the page, but is unnecessarily long for most purposes.</span></span> <span data-ttu-id="3e862-565">렌더링 된 ID의 길이를 줄이려면 ID 생성 되는 방식을 효과적으로 제어를 사용 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-565">Imagine that you want to reduce the length of the rendered ID, and to have more control over how the ID is generated.</span></span> <span data-ttu-id="3e862-566">(예를 들어, 하려는 "ctlxxx" 접두사를 제거 합니다.) 설정 된 경우이 작업을 수행 하는 가장 쉬운 방법은 합니다 *ClientIDMode* 다음 예와에서 같이 속성:</span><span class="sxs-lookup"><span data-stu-id="3e862-566">(For example, you want to eliminate "ctlxxx" prefixes.) The easiest way to achieve this is by setting the *ClientIDMode* property as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample51.aspx)]

<span data-ttu-id="3e862-567">이 샘플에서는 합니다 *ClientIDMode* 속성이로 설정 된 *정적* 바깥쪽에 대 한 *NamingPanel* 요소와 설정 *예측 가능* 내부 *NamingControl* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-567">In this sample, the *ClientIDMode* property is set to *Static* for the outermost *NamingPanel* element, and set to *Predictable* for the inner *NamingControl* element.</span></span> <span data-ttu-id="3e862-568">이러한 설정 (나머지 페이지 및 마스터 페이지는 이전 예제 에서처럼에서 동일한 것으로 간주 됩니다.) 다음 태그에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-568">These settings result in the following markup (the rest of the page and the master page is assumed to be the same as in the previous example):</span></span>

[!code-html[Main](overview/samples/sample52.html)]

<span data-ttu-id="3e862-569">합니다 *정적* 설정은 가장 바깥쪽 안의 모든 컨트롤에 대 한 명명 계층 구조를 다시 설정의 영향을 주지 *NamingPanel* 요소 및 제거는 *ContentPlaceHolder* 하 고 *MasterPage* Id는 생성 된 id입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-569">The *Static* setting has the effect of resetting the naming hierarchy for any controls inside the outermost *NamingPanel* element, and of eliminating the *ContentPlaceHolder* and *MasterPage* IDs from the generated ID.</span></span> <span data-ttu-id="3e862-570">(합니다 *이름을* 렌더링 된 요소의 특성에 영향을 받지 않습니다, 정상적인 ASP.NET 기능을 보존 되는 이벤트에 대 한 상태를 확인 하 고 등.) 부작용의 명명 계층 구조를 다시 설정 하는 태그를 이동 하는 경우에 합니다 *NamingPanel* 다른 요소 *ContentPlaceholder* 컨트롤을 렌더링 된 클라이언트 Id는 동일 하 게 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-570">(The *name* attribute of rendered elements is unaffected, so the normal ASP.NET functionality is retained for events, view state, and so on.) A side effect of resetting the naming hierarchy is that even if you move the markup for the *NamingPanel* elements to a different *ContentPlaceholder* control, the rendered client IDs remain the same.</span></span>

> [!NOTE]
> <span data-ttu-id="3e862-571">렌더링 된 컨트롤 Id는 고유 해야 하는 것을 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-571">Note It is up to you to make sure that the rendered control IDs are unique.</span></span> <span data-ttu-id="3e862-572">그렇지 않은 경우 클라이언트와 같은 개별 HTML 요소에 대 한 고유 Id를 필요로 하는 모든 기능을 중단할 수 있습니다 *document.getElementById* 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-572">If they are not, it can break any functionality that requires unique IDs for individual HTML elements, such as the client *document.getElementById* function.</span></span>


#### <a name="creating-predictable-client-ids-in-data-bound-controls"></a><span data-ttu-id="3e862-573">데이터 바인딩된 컨트롤에서 예측 가능한 클라이언트 Id 만들기</span><span class="sxs-lookup"><span data-stu-id="3e862-573">Creating Predictable Client IDs in Data-Bound Controls</span></span>

<span data-ttu-id="3e862-574">합니다 *ClientID* 레거시 알고리즘에서 데이터 바인딩된 목록 컨트롤의 컨트롤 수에 대해 생성 되는 값 하며를 실제로 예측할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-574">The *ClientID* values that are generated for controls in a data-bound list control by the legacy algorithm can be long and are not really predictable.</span></span> <span data-ttu-id="3e862-575">합니다 *ClientIDMode* 기능을 통해 이러한 Id를 통해 생성 된 제어를 강화할 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-575">The *ClientIDMode* functionality can help you have more control over how these IDs are generated.</span></span>

<span data-ttu-id="3e862-576">다음 예제에서 태그를 *ListView* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-576">The markup in the following example includes a *ListView* control:</span></span>

[!code-aspx[Main](overview/samples/sample53.aspx)]

<span data-ttu-id="3e862-577">이전 예에서 합니다 *ClientIDMode* 하 고 *RowClientIDRowSuffix* 속성 태그에서 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-577">In the previous example, the *ClientIDMode* and *RowClientIDRowSuffix* properties are set in markup.</span></span> <span data-ttu-id="3e862-578">합니다 *ClientIDRowSuffix* 속성을 데이터 바인딩된 컨트롤에만 사용할 수 있습니다 하 고 해당 동작은 사용 중인 컨트롤에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-578">The *ClientIDRowSuffix* property can be used only in data-bound controls, and its behavior differs depending on which control you are using.</span></span> <span data-ttu-id="3e862-579">차이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-579">The differences are these:</span></span>

- <span data-ttu-id="3e862-580">*GridView* 컨트롤-지정할 수 있습니다 하나 이상의 열 이름을 데이터 원본에서 런타임에 클라이언트 Id 생성에 결합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-580">*GridView* control — You can specify the name of one or more columns in the data source, which are combined at run time to create the client IDs.</span></span> <span data-ttu-id="3e862-581">예를 들어, 설정 하는 경우 *RowClientIDRowSuffix* "productname, ProductId" 렌더링 된 요소는 다음과 같은 형식을 갖습니다에 대 한 Id를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-581">For example, if you set *RowClientIDRowSuffix* to "ProductName, ProductId", control IDs for rendered elements will have a format like the following:</span></span>

- [!code-console[Main](overview/samples/sample54.cmd)]

- <span data-ttu-id="3e862-582">*ListView* 컨트롤-클라이언트 id와 같습니다. 추가 되는 데이터 원본에서 단일 열을 지정할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="3e862-582">*ListView* control — You can specify a single column in the data source that is appended to the client ID.</span></span> <span data-ttu-id="3e862-583">예를 들어 설정한 *ClientIDRowSuffix* 렌더링 된 컨트롤 Id는 다음과 같은 형식을 "productname" 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-583">For example, if you set *ClientIDRowSuffix* to "ProductName", the rendered control IDs will have a format like the following:</span></span>

- [!code-console[Main](overview/samples/sample55.cmd)]

- <span data-ttu-id="3e862-584">이 경우 후행 1은 현재 데이터 항목의 제품 ID에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-584">In this case the trailing 1 is derived from the product ID of the current data item.</span></span>

- <span data-ttu-id="3e862-585">*Repeater* 컨트롤-이 컨트롤을 지원 하지 않습니다 합니다 *ClientIDRowSuffix* 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-585">*Repeater* control— This control does not support the *ClientIDRowSuffix* property.</span></span> <span data-ttu-id="3e862-586">에 *Repeater* 컨트롤에 현재 행의 인덱스 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-586">In a *Repeater* control, the index of the current row is used.</span></span> <span data-ttu-id="3e862-587">ClientIDMode를 사용 하는 경우 = "예측 가능"를 *Repeater* 컨트롤 형식에 있는 클라이언트 Id가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-587">When you use ClientIDMode="Predictable" with a *Repeater* control, client IDs are generated that have the following format:</span></span>

- [!code-console[Main](overview/samples/sample56.cmd)]

- <span data-ttu-id="3e862-588">후행 0에는 현재 행의 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-588">The trailing 0 is the index of the current row.</span></span>

<span data-ttu-id="3e862-589">합니다 *FormView* 하 고 *DetailsView* 컨트롤을 지원 하지 않는 하므로 여러 행을 표시 하지 않습니다는 *ClientIDRowSuffix* 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-589">The *FormView* and *DetailsView* controls do not display multiple rows, so they do not support the *ClientIDRowSuffix* property.</span></span>

<a id="0.2__Toc224729038"></a><a id="0.2__Toc253429262"></a><a id="0.2__Toc243304636"></a>

### <a name="persisting-row-selection-in-data-controls"></a><span data-ttu-id="3e862-590">데이터 컨트롤에서 유지 행 선택</span><span class="sxs-lookup"><span data-stu-id="3e862-590">Persisting Row Selection in Data Controls</span></span>

<span data-ttu-id="3e862-591">합니다 *GridView* 하 고 *ListView* 컨트롤에는 사용자가 행을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-591">The *GridView* and *ListView* controls can let users select a row.</span></span> <span data-ttu-id="3e862-592">ASP.NET의 이전 버전에서는 선택을 기반으로 페이지의 행 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-592">In previous versions of ASP.NET, selection has been based on the row index on the page.</span></span> <span data-ttu-id="3e862-593">예를 들어 1 페이지에서 세 번째 항목을 선택 하 고 다음 2 페이지로 이동 하는 경우에 해당 페이지에서 세 번째 항목이 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-593">For example, if you select the third item on page 1 and then move to page 2, the third item on that page is selected.</span></span>

<span data-ttu-id="3e862-594">보관 된 선택 된 처음에.NET Framework 3.5 SP1의 동적 데이터 프로젝트 에서만에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-594">Persisted selection was initially supported only in Dynamic Data projects in the .NET Framework 3.5 SP1.</span></span> <span data-ttu-id="3e862-595">이 기능을 사용 하는 경우 현재 선택한 항목은 항목에 대 한 데이터 키를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-595">When this feature is enabled, the current selected item is based on the data key for the item.</span></span> <span data-ttu-id="3e862-596">이 1 페이지에서 세 번째 행을 선택 하 고 2 페이지로 이동 하는 경우 2 페이지에서 선택 된 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-596">This means that if you select the third row on page 1 and move to page 2, nothing is selected on page 2.</span></span> <span data-ttu-id="3e862-597">1 페이지로 다시 이동 하면 세 번째 행 선택 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-597">When you move back to page 1, the third row is still selected.</span></span> <span data-ttu-id="3e862-598">보관 된 선택에 지원 됩니다는 *GridView* 및 *ListView* 사용 하 여 모든 프로젝트에서 컨트롤을 *EnablePersistedSelection* 속성에 표시 된 대로 다음 예제:</span><span class="sxs-lookup"><span data-stu-id="3e862-598">Persisted selection is now supported for the *GridView* and *ListView* controls in all projects by using the *EnablePersistedSelection* property, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample57.aspx)]

<a id="0.2__Toc253429263"></a><a id="0.2__Toc243304637"></a>

### <a name="aspnet-chart-control"></a><span data-ttu-id="3e862-599">ASP.NET 차트 컨트롤</span><span class="sxs-lookup"><span data-stu-id="3e862-599">ASP.NET Chart Control</span></span>

<span data-ttu-id="3e862-600">ASP.NET *차트* 컨트롤이.NET Framework의 데이터 시각화 제품을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-600">The ASP.NET *Chart* control expands the data-visualization offerings in the .NET Framework.</span></span> <span data-ttu-id="3e862-601">사용 하는 *차트* 컨트롤, ASP.NET 페이지는 복잡 한 통계 또는 재무 분석을 위해 직관적 이며 시각적으로 우수한 차트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-601">Using the *Chart* control, you can create ASP.NET pages that have intuitive and visually compelling charts for complex statistical or financial analysis.</span></span> <span data-ttu-id="3e862-602">ASP.NET *차트* 컨트롤 소개 된 추가 기능으로.NET Framework 버전 3.5 SP1 릴리스 및.NET Framework 4 릴리스의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-602">The ASP.NET *Chart* control was introduced as an add-on to the .NET Framework version 3.5 SP1 release and is part of the .NET Framework 4 release.</span></span>

<span data-ttu-id="3e862-603">컨트롤에는 다음 기능이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-603">The control includes the following features:</span></span>

- <span data-ttu-id="3e862-604">35가지 개별 차트 종류</span><span class="sxs-lookup"><span data-stu-id="3e862-604">35 distinct chart types.</span></span>
- <span data-ttu-id="3e862-605">차트 영역, 제목, 범례 및 주석을의 무제한입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-605">An unlimited number of chart areas, titles, legends, and annotations.</span></span>
- <span data-ttu-id="3e862-606">다양 한 모든 차트 요소에 대 한 모양 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-606">A wide variety of appearance settings for all chart elements.</span></span>
- <span data-ttu-id="3e862-607">대부분의 차트 종류에 대 한 3 차원 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-607">3-D support for most chart types.</span></span>
- <span data-ttu-id="3e862-608">데이터 요소 주위에 자동으로 맞출 수 있는 스마트 데이터 레이블을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-608">Smart data labels that can automatically fit around data points.</span></span>
- <span data-ttu-id="3e862-609">줄무늬 선을, 배율 구분선 및 로그 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-609">Strip lines, scale breaks, and logarithmic scaling.</span></span>
- <span data-ttu-id="3e862-610">데이터 분석 및 변형을 위한 50개가 넘는 재무 및 통계 수식</span><span class="sxs-lookup"><span data-stu-id="3e862-610">More than 50 financial and statistical formulas for data analysis and transformation.</span></span>
- <span data-ttu-id="3e862-611">단순 바인딩 및 차트 데이터의 조작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-611">Simple binding and manipulation of chart data.</span></span>
- <span data-ttu-id="3e862-612">날짜, 시간 및 통화와 같은 일반적인 데이터 형식 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-612">Support for common data formats such as dates, times, and currency.</span></span>
- <span data-ttu-id="3e862-613">대화형 작업 및 클라이언트를 포함 하는 이벤트 기반 사용자 지정에 대 한 지원을 Ajax를 사용 하 여 이벤트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-613">Support for interactivity and event-driven customization, including client click events using Ajax.</span></span>
- <span data-ttu-id="3e862-614">상태 관리</span><span class="sxs-lookup"><span data-stu-id="3e862-614">State management.</span></span>
- <span data-ttu-id="3e862-615">이진 스트리밍</span><span class="sxs-lookup"><span data-stu-id="3e862-615">Binary streaming.</span></span>

<span data-ttu-id="3e862-616">다음 그림에서는 ASP.NET 차트 컨트롤에 의해 생성 되는 재무 차트의 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-616">The following figures show examples of financial charts that are produced by the ASP.NET Chart control.</span></span>

<a id="0.2_graphic17"></a>![](overview/_static/image1.png)

<span data-ttu-id="3e862-617">그림 2: ASP.NET 차트 컨트롤 예</span><span class="sxs-lookup"><span data-stu-id="3e862-617">Figure 2: ASP.NET Chart control examples</span></span>

<span data-ttu-id="3e862-618">ASP.NET 차트 컨트롤을 사용 하는 방법의 더 많은 예제에서 샘플 코드를 다운로드 합니다 [Microsoft Chart controls 예제 환경](https://go.microsoft.com/fwlink/?LinkId=128300) MSDN 웹 사이트의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-618">For more examples of how to use the ASP.NET Chart control, download the sample code on the [Samples Environment for Microsoft Chart Controls](https://go.microsoft.com/fwlink/?LinkId=128300) page on the MSDN Web site.</span></span> <span data-ttu-id="3e862-619">콘텐츠 커뮤니티의 많은 샘플을 찾을 수 있습니다 합니다 [차트 컨트롤 포럼](https://go.microsoft.com/fwlink/?LinkId=128713)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-619">You can find more samples of community content at the [Chart Control Forum](https://go.microsoft.com/fwlink/?LinkId=128713).</span></span>

#### <a name="adding-the-chart-control-to-an-aspnet-page"></a><span data-ttu-id="3e862-620">ASP.NET 페이지에 차트 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="3e862-620">Adding the Chart Control to an ASP.NET Page</span></span>

<span data-ttu-id="3e862-621">다음 예제에서는 추가 하는 방법을 보여 줍니다는 *차트* 태그를 사용 하 여 ASP.NET 페이지에는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-621">The following example shows how to add a *Chart* control to an ASP.NET page by using markup.</span></span> <span data-ttu-id="3e862-622">예에서는 *차트* 컨트롤에 정적 데이터 요소에 대 한 세로 막대형 차트를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-622">In the example, the *Chart* control produces a column chart for static data points.</span></span>

[!code-aspx[Main](overview/samples/sample58.aspx)]

#### <a name="using-3-d-charts"></a><span data-ttu-id="3e862-623">3 차원 차트를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3e862-623">Using 3-D Charts</span></span>

<span data-ttu-id="3e862-624">*차트* 컨트롤에는 *ChartAreas* 포함할 수 있는 컬렉션 *ChartArea* 차트 영역의 특성을 정의 하는 개체.</span><span class="sxs-lookup"><span data-stu-id="3e862-624">The *Chart* control contains a *ChartAreas* collection, which can contain *ChartArea* objects that define characteristics of chart areas.</span></span> <span data-ttu-id="3e862-625">예를 들어 3 차원 차트 영역에 대 한를 사용 하려면 사용 합니다 *있는 Area3DStyle* 다음 예제와 같이 속성:</span><span class="sxs-lookup"><span data-stu-id="3e862-625">For example, to use 3-D for a chart area, use the *Area3DStyle* property as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample59.aspx)]

<span data-ttu-id="3e862-626">아래 그림의 4 개 시리즈를 사용 하 여 3 차원 차트의 *표시줄* 차트 종류입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-626">The figure below shows a 3-D chart with four series of the *Bar* chart type.</span></span>

<a id="0.2_graphic18"></a>![](overview/_static/image2.png)

<span data-ttu-id="3e862-627">그림 3: 3 차원 가로 막대형 차트</span><span class="sxs-lookup"><span data-stu-id="3e862-627">Figure 3: 3-D Bar Chart</span></span>

#### <a name="using-scale-breaks-and-logarithmic-scales"></a><span data-ttu-id="3e862-628">배율 구분선 및 로그 눈금 간격 사용</span><span class="sxs-lookup"><span data-stu-id="3e862-628">Using Scale Breaks and Logarithmic Scales</span></span>

<span data-ttu-id="3e862-629">배율 구분선 눈금와 숙련도 차트에 추가할 추가 두 가지 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-629">Scale breaks and logarithmic scales are two additional ways to add sophistication to the chart.</span></span> <span data-ttu-id="3e862-630">이러한 기능은 각 차트 영역 축 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-630">These features are specific to each axis in a chart area.</span></span> <span data-ttu-id="3e862-631">예를 들어 차트 영역의 기본 Y 축에서 이러한 기능을 사용 하려면 사용 합니다 *AxisY.IsLogarithmic* 및 *ScaleBreakStyle* 속성에는 *ChartArea* 개체.</span><span class="sxs-lookup"><span data-stu-id="3e862-631">For example, to use these features on the primary Y axis of a chart area, use the *AxisY.IsLogarithmic* and *ScaleBreakStyle* properties in a *ChartArea* object.</span></span> <span data-ttu-id="3e862-632">다음 코드 조각은 기본 Y 축의 배율 구분선을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-632">The following snippet shows how to use scale breaks on the primary Y axis.</span></span>

[!code-aspx[Main](overview/samples/sample60.aspx)]

<span data-ttu-id="3e862-633">아래 그림에는 사용 하도록 설정 하는 배율 구분선을 사용 하 여 Y 축을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-633">The figure below shows the Y axis with scale breaks enabled.</span></span>

<a id="0.2_graphic19"></a>![](overview/_static/image3.png)

<span data-ttu-id="3e862-634">그림 4: 배율 구분선</span><span class="sxs-lookup"><span data-stu-id="3e862-634">Figure 4: Scale Breaks</span></span>

<a id="0.2__QueryExtender"></a><a id="0.2__Toc224729041"></a><a id="0.2__Toc253429264"></a><a id="0.2__Toc243304638"></a>

### <a name="filtering-data-with-the-queryextender-control"></a><span data-ttu-id="3e862-635">QueryExtender 컨트롤을 사용 하 여 데이터를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-635">Filtering Data with the QueryExtender Control</span></span>

<span data-ttu-id="3e862-636">데이터 기반 웹 페이지를 만드는 개발자를 위한 매우 일반적인 작업 데이터를 필터링 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-636">A very common task for developers who create data-driven Web pages is to filter data.</span></span> <span data-ttu-id="3e862-637">이 일반적으로 수행 된 빌드하여 *여기서* 절에서 데이터 소스 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-637">This traditionally has been performed by building *Where* clauses in data source controls.</span></span> <span data-ttu-id="3e862-638">이 방법은 복잡할 수 있습니다 및 일부 경우에는 *여기서* 구문 수 없다는 기본 데이터베이스의 전체 기능을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-638">This approach can be complicated, and in some cases the *Where* syntax does not let you take advantage of the full functionality of the underlying database.</span></span>

<span data-ttu-id="3e862-639">필터링을 더 쉽게 새 되도록 *QueryExtender* 컨트롤이 ASP.NET 4에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-639">To make filtering easier, a new *QueryExtender* control has been added in ASP.NET 4.</span></span> <span data-ttu-id="3e862-640">이 컨트롤을 추가할 수 있습니다 *EntityDataSource* 하거나 *LinqDataSource* 이러한 컨트롤에 의해 반환 되는 데이터를 필터링 하기 위해 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-640">This control can be added to *EntityDataSource* or *LinqDataSource* controls in order to filter the data returned by these controls.</span></span> <span data-ttu-id="3e862-641">때문에 합니다 *QueryExtender* LINQ에 의존 하 여, 데이터를 매우 효율적이 고 작업의 결과 페이지를에 전송 되기 전에 데이터베이스 서버에 필터가 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-641">Because the *QueryExtender* control relies on LINQ, the filter is applied on the database server before the data is sent to the page, which results in very efficient operations.</span></span>

<span data-ttu-id="3e862-642">합니다 *QueryExtender* 컨트롤은 다양 한 필터 옵션을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-642">The *QueryExtender* control supports a variety of filter options.</span></span> <span data-ttu-id="3e862-643">다음 섹션에서는 이러한 옵션을 설명 하 고 사용 하는 방법의 예제를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-643">The following sections describe these options and provide examples of how to use them.</span></span>

#### <a name="search"></a><span data-ttu-id="3e862-644">검색</span><span class="sxs-lookup"><span data-stu-id="3e862-644">Search</span></span>

<span data-ttu-id="3e862-645">검색 옵션에 대 한 합니다 *QueryExtender* 컨트롤 지정 된 필드에 검색을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-645">For the search option, the *QueryExtender* control performs a search in specified fields.</span></span> <span data-ttu-id="3e862-646">다음 예제에서는 컨트롤 사용 TextBoxSearch 컨트롤과 내용 검색에 입력 된 텍스트를 `ProductName` 하 고 `Supplier.CompanyName` 에서 반환 되는 데이터의 열을 *LinqDataSource* 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-646">In the following example, the control uses the text that is entered in the TextBoxSearch control and searches for its contents in the `ProductName` and `Supplier.CompanyName` columns in the data that is returned from the *LinqDataSource* control.</span></span>

[!code-aspx[Main](overview/samples/sample61.aspx)]

#### <a name="range"></a><span data-ttu-id="3e862-647">범위</span><span class="sxs-lookup"><span data-stu-id="3e862-647">Range</span></span>

<span data-ttu-id="3e862-648">범위 옵션 검색 옵션을 유사 하지만 범위를 정의 하는 값의 쌍을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-648">The range option is similar to the search option, but specifies a pair of values to define the range.</span></span> <span data-ttu-id="3e862-649">다음 예에서 *QueryExtender* 검색을 제어 합니다 `UnitPrice` 에서 반환 된 데이터의 열에에서는 *LinqDataSource* 컨트롤.</span><span class="sxs-lookup"><span data-stu-id="3e862-649">In the following example, the *QueryExtender* control searches the `UnitPrice` column in the data returned from the *LinqDataSource* control.</span></span> <span data-ttu-id="3e862-650">범위는 페이지의 TextBoxFrom 및 TextBoxTo 컨트롤에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-650">The range is read from the TextBoxFrom and TextBoxTo controls on the page.</span></span>

[!code-aspx[Main](overview/samples/sample62.aspx)]

#### <a name="propertyexpression"></a><span data-ttu-id="3e862-651">PropertyExpression</span><span class="sxs-lookup"><span data-stu-id="3e862-651">PropertyExpression</span></span>

<span data-ttu-id="3e862-652">속성 식 옵션 속성 값 비교를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-652">The property expression option lets you define a comparison to a property value.</span></span> <span data-ttu-id="3e862-653">식이 계산 되는 경우 *true*, 검사 되는 데이터가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-653">If the expression evaluates to *true*, the data that is being examined is returned.</span></span> <span data-ttu-id="3e862-654">다음 예제에서는 *QueryExtender* 컨트롤의 데이터를 비교 하 여 데이터를 필터링는 `Discontinued` 페이지 CheckBoxDiscontinued 컨트롤에서 열 값을 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-654">In the following example, the *QueryExtender* control filters data by comparing the data in the `Discontinued` column to the value from the CheckBoxDiscontinued control on the page.</span></span>

[!code-aspx[Main](overview/samples/sample63.aspx)]

#### <a name="customexpression"></a><span data-ttu-id="3e862-655">CustomExpression</span><span class="sxs-lookup"><span data-stu-id="3e862-655">CustomExpression</span></span>

<span data-ttu-id="3e862-656">마지막으로 사용 하 여 사용 하 여 사용자 지정 식을 지정할 수 있습니다 합니다 *QueryExtender* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-656">Finally, you can specify a custom expression to use with the *QueryExtender* control.</span></span> <span data-ttu-id="3e862-657">이 옵션을 통해 사용자 지정 필터 논리를 정의 하는 페이지에서 함수를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-657">This option lets you call a function in the page that defines custom filter logic.</span></span> <span data-ttu-id="3e862-658">다음 예제에서는 사용자 지정 식에 선언적으로 지정 하는 방법을 보여 줍니다 합니다 *QueryExtender* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-658">The following example shows how to declaratively specify a custom expression in the *QueryExtender* control.</span></span>

[!code-aspx[Main](overview/samples/sample64.aspx)]

<span data-ttu-id="3e862-659">다음 예제에서는 사용자 지정 함수에서 호출 하는 *QueryExtender* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-659">The following example shows the custom function that is invoked by the *QueryExtender* control.</span></span> <span data-ttu-id="3e862-660">포함 된 데이터베이스 쿼리를 사용 하는 대신이 경우에 *여기서* 절, 코드를 사용 하 여 LINQ 쿼리를 데이터를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-660">In this case, instead of using a database query that includes a *Where* clause, the code uses a LINQ query to filter the data.</span></span>

[!code-csharp[Main](overview/samples/sample65.cs)]

<span data-ttu-id="3e862-661">이러한 예제에서 사용 되는 식이 하나만 표시 합니다 *QueryExtender* 한 번에 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-661">These examples show only one expression being used in the *QueryExtender* control at a time.</span></span> <span data-ttu-id="3e862-662">그러나 내에서 여러 식을 포함할 수 있습니다 합니다 *QueryExtender* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-662">However, you can include multiple expressions inside the *QueryExtender* control.</span></span>

<a id="0.2__Toc253429265"></a><a id="0.2__Toc243304639"></a>

### <a name="html-encoded-code-expressions"></a><span data-ttu-id="3e862-663">Html 인코딩된 코드 식</span><span class="sxs-lookup"><span data-stu-id="3e862-663">Html Encoded Code Expressions</span></span>

<span data-ttu-id="3e862-664">(특히 ASP.NET MVC)와 함께 몇 가지 ASP.NET 사이트를 사용 하 여에 크게 의존 `<%` =  `expression %>` 구문 ("코드 너 깃"이 라고도 함) 응답에 일부 텍스트를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-664">Some ASP.NET sites (especially with ASP.NET MVC) rely heavily on using `<%`= `expression %>` syntax (often called "code nuggets") to write some text to the response.</span></span> <span data-ttu-id="3e862-665">코드 식을 사용 하면 텍스트를 사용자에서 제공 되는 경우 텍스트를 입력 하 고, 해당 페이지를 열어 놓을 수는 XSS (교차 사이트 스크립팅) 공격에 HTML로 인코딩합니다 잊기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-665">When you use code expressions, it is easy to forget to HTML-encode the text, If the text comes from user input, it can leave pages open to an XSS (Cross Site Scripting) attack.</span></span>

<span data-ttu-id="3e862-666">ASP.NET 4 코드 식에 대 한 새 구문을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-666">ASP.NET 4 introduces the following new syntax for code expressions:</span></span>

[!code-aspx[Main](overview/samples/sample66.aspx)]

<span data-ttu-id="3e862-667">이 구문은 HTML 응답을 쓸 때 기본적으로 인코딩을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-667">This syntax uses HTML encoding by default when writing to the response.</span></span> <span data-ttu-id="3e862-668">이 새 식 다음에 효과적으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-668">This new expression effectively translates to the following:</span></span>

[!code-aspx[Main](overview/samples/sample67.aspx)]

<span data-ttu-id="3e862-669">예를 들어 &lt;%: 요청 ["/userinput&gt"] %&gt; 의 값에 HTML 인코딩을 수행 *["/userinput&gt"] 요청*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-669">For example, &lt;%: Request["UserInput"] %&gt; performs HTML encoding on the value of *Request["UserInput"]*.</span></span>

<span data-ttu-id="3e862-670">이 기능의 목적은 모든 단계에서 사용할 항목을 결정 하지 않아도 됩니다 있도록 새 구문을 사용 하 여 이전 구문의 모든 인스턴스를 대체할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-670">The goal of this feature is to make it possible to replace all instances of the old syntax with the new syntax so that you are not forced to decide at every step which one to use.</span></span> <span data-ttu-id="3e862-671">그러나 가지 사례가 출력 되는 텍스트를 HTML 알 수 있도록 하거나 이미 인코딩된 있는 이중 인코딩으로 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-671">However, there are cases in which the text being output is meant to be HTML or is already encoded, in which case this could lead to double encoding.</span></span>

<span data-ttu-id="3e862-672">이러한 경우에 대 한 ASP.NET 4 소개 새로운 인터페이스인 *IHtmlString*, 구체적인 구현과 함께 *HtmlString*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-672">For those cases, ASP.NET 4 introduces a new interface, *IHtmlString*, along with a concrete implementation, *HtmlString*.</span></span> <span data-ttu-id="3e862-673">이러한 형식의 인스턴스를 사용 하는 반환 값 이미 올바르게 인코딩된 (이거나 그렇지 않으면 검사) HTML로 표시 하 고 따라서 값을 프로그램이 되지 않음을 HTML로 인코딩된 다시를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-673">Instances of these types let you indicate that the return value is already properly encoded (or otherwise examined) for displaying as HTML, and that therefore the value should not be HTML-encoded again.</span></span> <span data-ttu-id="3e862-674">예를 들어, 다음 안 됩니다 (아니며) HTML 인코딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-674">For example, the following should not be (and is not) HTML encoded:</span></span>

[!code-aspx[Main](overview/samples/sample68.aspx)]

<span data-ttu-id="3e862-675">ASP.NET MVC 2 도우미 메서드 ASP.NET 4를 실행 하는 경우이 새 구문을 사용 하 여 사용 하지 않은 이중 인코딩 되도록 업데이트 된만 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-675">ASP.NET MVC 2 helper methods have been updated to work with this new syntax so that they are not double encoded, but only when you are running ASP.NET 4.</span></span> <span data-ttu-id="3e862-676">이 새 구문은 ASP.NET 3.5 SP1을 사용 하 여 응용 프로그램을 실행 하는 경우 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-676">This new syntax does not work when you run an application using ASP.NET 3.5 SP1.</span></span>

<span data-ttu-id="3e862-677">이 XSS 공격 으로부터 보호를 보장 하지는 것을 염두에 두십시오.</span><span class="sxs-lookup"><span data-stu-id="3e862-677">Keep in mind that this does not guarantee protection from XSS attacks.</span></span> <span data-ttu-id="3e862-678">예를 들어 따옴표에 있지 않은 특성 값을 사용 하는 HTML 여전히 사용자 입력을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-678">For example, HTML that uses attribute values that are not in quotation marks can contain user input that is still susceptible.</span></span> <span data-ttu-id="3e862-679">Note ASP.NET 컨트롤 및 ASP.NET MVC 도우미 출력 항상 포함 특성 값 따옴표 안에 있는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-679">Note that the output of ASP.NET controls and ASP.NET MVC helpers always includes attribute values in quotation marks, which is the recommended approach.</span></span>

<span data-ttu-id="3e862-680">마찬가지로,이 구문은 사용자 입력을 기반으로 하는 JavaScript 문자열을 만들 때와 같은 JavaScript 인코딩을 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-680">Likewise, this syntax does not perform JavaScript encoding, such as when you create a JavaScript string based on user input.</span></span>

<a id="0.2__Toc253429266"></a><a id="0.2__Toc243304640"></a>

### <a name="project-template-changes"></a><span data-ttu-id="3e862-681">프로젝트 템플릿 변경</span><span class="sxs-lookup"><span data-stu-id="3e862-681">Project Template Changes</span></span>

<span data-ttu-id="3e862-682">ASP.NET의 이전 버전에서는 Visual Studio를 사용 하 여 새 웹 사이트 프로젝트 또는 웹 응용 프로그램 프로젝트를 만들 때 결과 프로젝트에 들어만 Default.aspx 페이지에서 기본값 `Web.config` 파일 및 `App_Data` 폴더 아래에 표시 된 것과 같이 그림:</span><span class="sxs-lookup"><span data-stu-id="3e862-682">In earlier versions of ASP.NET, when you use Visual Studio to create a new Web Site project or Web Application project, the resulting projects contain only a Default.aspx page, a default `Web.config` file, and the `App_Data` folder, as shown in the following illustration:</span></span>

<a id="0.2_graphic1A"></a>![](overview/_static/image4.png)

<span data-ttu-id="3e862-683">Visual Studio를 전혀 다음 그림에 나와 있는 것 처럼 파일이 없는 하는 빈 웹 사이트 프로젝트 형식을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-683">Visual Studio also supports an Empty Web Site project type, which contains no files at all, as shown in the following figure:</span></span>

<a id="0.2_graphic1B"></a>![](overview/_static/image5.png)

<span data-ttu-id="3e862-684">결과 있다는 점입니다 초보자를 위한에 대 한 지침이 거의 프로덕션 웹 응용 프로그램을 빌드하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-684">The result is that for the beginner, there is very little guidance on how to build a production Web application.</span></span> <span data-ttu-id="3e862-685">따라서 ASP.NET 4에서는 세 개의 새로운 템플릿이 고 빈 웹 응용 프로그램 프로젝트에 대 한 웹 응용 프로그램 및 웹 사이트 프로젝트에 대해 각각 1을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-685">Therefore, ASP.NET 4 introduces three new templates, one for an empty Web application project, and one each for a Web Application and Web Site project.</span></span>

#### <a name="empty-web-application-template"></a><span data-ttu-id="3e862-686">빈 웹 응용 프로그램 템플릿</span><span class="sxs-lookup"><span data-stu-id="3e862-686">Empty Web Application Template</span></span>

<span data-ttu-id="3e862-687">이름에서 알 수 있듯이 빈 웹 응용 프로그램 템플릿에 축소 된 기본 웹 응용 프로그램 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-687">As the name suggests, the Empty Web Application template is a stripped-down Web Application project.</span></span> <span data-ttu-id="3e862-688">다음 그림에 표시 된 것과 같이 Visual Studio 새 프로젝트 대화 상자에서이 프로젝트 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-688">You select this project template from the Visual Studio New Project dialog box, as shown in the following figure:</span></span>

[![](overview/_static/image7.png)](overview/_static/image6.png)

<span data-ttu-id="3e862-689">([클릭 하 여 큰 이미지 보기](overview/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="3e862-689">([Click to view full-size image](overview/_static/image8.png))</span></span>

<span data-ttu-id="3e862-690">빈 ASP.NET 웹 응용 프로그램을 만들면 Visual Studio는 다음 폴더의 레이아웃을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-690">When you create an Empty ASP.NET Web Application, Visual Studio creates the following folder layout:</span></span>

<a id="0.2_graphic1D"></a>![](overview/_static/image9.png)

<span data-ttu-id="3e862-691">이 한 가지 예외를 사용 하 여 이전 버전의 ASP.NET 빈 웹 사이트 레이아웃 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-691">This is similar to the Empty Web Site layout from earlier versions of ASP.NET, with one exception.</span></span> <span data-ttu-id="3e862-692">Visual Studio 2010에서 빈 웹 응용 프로그램 및 빈 웹 사이트 프로젝트는 최소한 다음 포함 `Web.config` 하는 데 Visual Studio에서 프로젝트 대상으로 하는 프레임 워크를 식별 하는 정보가 포함 된 파일:</span><span class="sxs-lookup"><span data-stu-id="3e862-692">In Visual Studio 2010, Empty Web Application and Empty Web Site projects contain the following minimal `Web.config` file that contains information used by Visual Studio to identify the framework that the project is targeting:</span></span>

<a id="0.2_graphic1E"></a>![](overview/_static/image10.png)

<span data-ttu-id="3e862-693">이렇게 하지 않으면 *targetFramework* 속성을 열면 이전 응용 프로그램 호환성을 유지 하기 위해.NET Framework 2.0을 대상으로 하려면 Visual Studio 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-693">Without this *targetFramework* property, Visual Studio defaults to targeting the .NET Framework 2.0 in order to preserve compatibility when opening older applications.</span></span>

#### <a name="web-application-and-web-site-project-templates"></a><span data-ttu-id="3e862-694">웹 응용 프로그램 및 웹 사이트 프로젝트 템플릿</span><span class="sxs-lookup"><span data-stu-id="3e862-694">Web Application and Web Site Project Templates</span></span>

<span data-ttu-id="3e862-695">다른 두 새 프로젝트 템플릿이 Visual Studio 2010과 함께 제공 되는 주요 변경 내용을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-695">The other two new project templates that are shipped with Visual Studio 2010 contain major changes.</span></span> <span data-ttu-id="3e862-696">다음 그림 새 웹 응용 프로그램 프로젝트를 만들 때 생성 되는 프로젝트 레이아웃을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-696">The following figure shows the project layout that is created when you create a new Web Application project.</span></span> <span data-ttu-id="3e862-697">(웹 사이트 프로젝트에 대 한 레이아웃은 거의 동일 합니다.)</span><span class="sxs-lookup"><span data-stu-id="3e862-697">(The layout for a Web Site project is virtually identical.)</span></span>

- <a id="0.2_graphic1F"></a>![](overview/_static/image11.png)

<span data-ttu-id="3e862-698">프로젝트는 이전 버전에서 생성 되지 않은 파일의 수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-698">The project includes a number of files that were not created in earlier versions.</span></span> <span data-ttu-id="3e862-699">또한 새 웹 응용 프로그램 프로젝트를 빠르게 새 응용 프로그램에 대 한 액세스를 보호 하기 시작할 수 있는 기본 멤버 자격 기능을 사용 하 여 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-699">In addition, the new Web Application project is configured with basic membership functionality, which lets you quickly get started in securing access to the new application.</span></span> <span data-ttu-id="3e862-700">이 포함 되어 있어는 `Web.config` 멤버 자격, 역할 및 프로필 구성에 사용 되는 항목을 포함 하는 새 프로젝트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-700">Because of this inclusion, the `Web.config` file for the new project includes entries that are used to configure membership, roles, and profiles.</span></span> <span data-ttu-id="3e862-701">다음 예제와 `Web.config` 새 웹 응용 프로그램 프로젝트에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-701">The following example shows the `Web.config` file for a new Web Application project.</span></span> <span data-ttu-id="3e862-702">(이 예에서 *roleManager* 을 사용할 수 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="3e862-702">(In this case, *roleManager* is disabled.)</span></span>

[![](overview/_static/image13.png)](overview/_static/image12.png)

<span data-ttu-id="3e862-703">([클릭 하 여 큰 이미지 보기](overview/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="3e862-703">([Click to view full-size image](overview/_static/image14.png))</span></span>

<span data-ttu-id="3e862-704">프로젝트에 두 번째도 포함 되어 있습니다 `Web.config` 파일을 `Account` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-704">The project also contains a second `Web.config` file in the `Account` directory.</span></span> <span data-ttu-id="3e862-705">두 번째 구성 파일을 비-로그인 한 사용자에 대 한 ChangePassword.aspx 페이지에 대 한 액세스를 보호 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-705">The second configuration file provides a way to secure access to the ChangePassword.aspx page for non-logged in users.</span></span> <span data-ttu-id="3e862-706">다음 예제에서는 두 번째 내용의 `Web.config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-706">The following example shows the contents of the second `Web.config` file.</span></span>

![](overview/_static/image15.png)

<span data-ttu-id="3e862-707">새 프로젝트 템플릿에 기본적으로 생성 하는 페이지에는 또한 이전 버전 보다 더 많은 내용을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-707">The pages created by default in the new project templates also contain more content than in previous versions.</span></span> <span data-ttu-id="3e862-708">프로젝트 기본 마스터 페이지 및 CSS 파일을 포함 하 고 기본 페이지 (Default.aspx)는 기본적으로 마스터 페이지를 사용 하도록 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-708">The project contains a default master page and CSS file, and the default page (Default.aspx) is configured to use the master page by default.</span></span> <span data-ttu-id="3e862-709">결과 웹 응용 프로그램 또는 웹 사이트를 처음 실행 하면 기본 (홈) 페이지는 이미 기능.</span><span class="sxs-lookup"><span data-stu-id="3e862-709">The result is that when you run the Web application or Web site for the first time, the default (home) page is already functional.</span></span> <span data-ttu-id="3e862-710">실제로 새 MVC 응용 프로그램을 시작할 때 표시 된 기본 페이지에 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-710">In fact, it is similar to the default page you see when you start up a new MVC application.</span></span>

[![](overview/_static/image17.png)](overview/_static/image16.png)

<span data-ttu-id="3e862-711">([클릭 하 여 큰 이미지 보기](overview/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="3e862-711">([Click to view full-size image](overview/_static/image18.png))</span></span>

<span data-ttu-id="3e862-712">프로젝트 템플릿에 이러한 변경의 의도 새 웹 응용 프로그램 빌드를 시작 하는 방법에 지침을 제공 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-712">The intention of these changes to the project templates is to provide guidance on how to start building a new Web application.</span></span> <span data-ttu-id="3e862-713">의미적으로, 엄격한 XHTML 1.0 규격 태그를 사용 하 여 및 CSS를 사용 하 여 지정 된 레이아웃을 사용 하 여 템플릿에 페이지는 ASP.NET 4 웹 응용 프로그램을 구축 하기 위한 모범 사례를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-713">With semantically correct, strict XHTML 1.0-compliant markup and with layout that is specified using CSS, the pages in the templates represent best practices for building ASP.NET 4 Web applications.</span></span> <span data-ttu-id="3e862-714">기본 페이지를 쉽게 사용자 지정할 수 있는 2 열 레이아웃을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-714">The default pages also have a two-column layout that you can easily customize.</span></span>

<span data-ttu-id="3e862-715">예를 들어 한다고 가정해 보겠습니다 새 웹 응용 프로그램에 대 한 색 중 일부를 변경 하 여 내 ASP.NET 응용 프로그램 로고 대신 회사 로고를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-715">For example, imagine that for a new Web Application you want to change some of the colors and insert your company logo in place of the My ASP.NET Application logo.</span></span> <span data-ttu-id="3e862-716">이 작업을 수행 하려면 아래 새 디렉터리를 만들어야 `Content` 로고 이미지를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-716">To do this, you create a new directory under `Content` to store your logo image:</span></span>

<a id="0.2_graphic23"></a>![](overview/_static/image19.png)

<span data-ttu-id="3e862-717">페이지에 이미지를 추가 하려면 다음 엽니다는 `Site.Master` 파일 찾기, 여기서 내 ASP.NET 응용 프로그램 텍스트를 정의로 바꿉니다는 *이미지* 요소입니다 *src* 특성이 새 로고로 설정 된 다음 예제와 같이 이미지:</span><span class="sxs-lookup"><span data-stu-id="3e862-717">To add the image to the page, you then open the `Site.Master` file, find where the My ASP.NET Application text is defined, and replace it with an *image* element whose *src* attribute is set to the new logo image, as in the following example:</span></span>

[![](overview/_static/image21.png)](overview/_static/image20.png)

<span data-ttu-id="3e862-718">([클릭 하 여 큰 이미지 보기](overview/_static/image22.png))</span><span class="sxs-lookup"><span data-stu-id="3e862-718">([Click to view full-size image](overview/_static/image22.png))</span></span>

<span data-ttu-id="3e862-719">그런 다음 Site.css 파일로 이동 하 고 페이지의 배경색 및 헤더를 변경 하는 CSS 클래스 정의 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-719">You can then go into the Site.css file and modify CSS class definitions to change the background color of the page as well as that of the header.</span></span>

<span data-ttu-id="3e862-720">이러한 변경의 결과 다음과 매우 간편 하 게 사용자 지정된 홈 페이지를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-720">The result of these changes is that you can display a customized home page with very little effort:</span></span>

[![](overview/_static/image24.png)](overview/_static/image23.png)

<span data-ttu-id="3e862-721">([클릭 하 여 큰 이미지 보기](overview/_static/image25.png))</span><span class="sxs-lookup"><span data-stu-id="3e862-721">([Click to view full-size image](overview/_static/image25.png))</span></span>

<a id="0.2__Toc253429267"></a><a id="0.2__Toc243304641"></a>

### <a name="css-improvements"></a><span data-ttu-id="3e862-722">향상 된 CSS 기능</span><span class="sxs-lookup"><span data-stu-id="3e862-722">CSS Improvements</span></span>

<span data-ttu-id="3e862-723">ASP.NET 4에는 작업의 주요 영역 중 하나는 최신 HTML 표준을 준수 하는 HTML을 렌더링 하는 데 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-723">One of the major areas of work in ASP.NET 4 has been to help render HTML that is compliant with the latest HTML standards.</span></span> <span data-ttu-id="3e862-724">ASP.NET 웹 서버 컨트롤에서 CSS 스타일을 사용 하는 방법에 대 한 변경 내용이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-724">This includes changes to how ASP.NET Web server controls use CSS styles.</span></span>

#### <a name="compatibility-setting-for-rendering"></a><span data-ttu-id="3e862-725">렌더링에 대 한 호환성 설정</span><span class="sxs-lookup"><span data-stu-id="3e862-725">Compatibility Setting for Rendering</span></span>

<span data-ttu-id="3e862-726">기본적으로 웹 응용 프로그램 또는 웹 사이트를.NET Framework 4를 대상으로 하는 경우는 *controlRenderingCompatibilityVersion* 특성을 *페이지* 요소 "4.0"으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-726">By default, when a Web application or Web site targets the .NET Framework 4, the *controlRenderingCompatibilityVersion* attribute of the *pages* element is set to "4.0".</span></span> <span data-ttu-id="3e862-727">컴퓨터 수준에서이 요소가 정의 `Web.config` 파일과 기본적으로 모든 ASP.NET 4 응용 프로그램에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-727">This element is defined in the machine-level `Web.config` file and by default applies to all ASP.NET 4 applications:</span></span>

[!code-xml[Main](overview/samples/sample69.xml)]

<span data-ttu-id="3e862-728">에 대 한 값 *controlRenderingCompatibility* 잠재적인 새 버전 정의 이후 릴리스에서 허용 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-728">The value for *controlRenderingCompatibility* is a string, which allows potential new version definitions in future releases.</span></span> <span data-ttu-id="3e862-729">현재 릴리스에서 다음 값이이 속성에 대 한 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-729">In the current release, the following values are supported for this property:</span></span>

- <span data-ttu-id="3e862-730">"3.5".</span><span class="sxs-lookup"><span data-stu-id="3e862-730">"3.5".</span></span> <span data-ttu-id="3e862-731">이 설정은 레거시 렌더링 및 태그를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-731">This setting indicates legacy rendering and markup.</span></span> <span data-ttu-id="3e862-732">컨트롤에서 렌더링 되는 태그는 100% 호환 및 설정 합니다 *xhtmlConformance* 속성이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-732">Markup rendered by controls is 100% backward compatible, and the setting of the *xhtmlConformance* property is honored.</span></span>
- <span data-ttu-id="3e862-733">"4.0".</span><span class="sxs-lookup"><span data-stu-id="3e862-733">"4.0".</span></span> <span data-ttu-id="3e862-734">속성에이 설정을 ASP.NET 웹 서버 컨트롤은 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-734">If the property has this setting, ASP.NET Web server controls do the following:</span></span>
- <span data-ttu-id="3e862-735">합니다 *xhtmlConformance* 속성은 항상 "Strict"으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-735">The *xhtmlConformance* property is always treated as "Strict".</span></span> <span data-ttu-id="3e862-736">결과적으로, 컨트롤 XHTML 1.0 Strict 태그를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-736">As a result, controls render XHTML 1.0 Strict markup.</span></span>
- <span data-ttu-id="3e862-737">잘못 된 스타일을 렌더링 비 입력 컨트롤을 더 이상 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-737">Disabling non-input controls no longer renders invalid styles.</span></span>
- <span data-ttu-id="3e862-738">*div* 숨겨진 필드 요소는 사용자가 만든 CSS 규칙을 사용 하 여 방해 하지 있도록 이제 스타일이 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-738">*div* elements around hidden fields are now styled so they do not interfere with user-created CSS rules.</span></span>
- <span data-ttu-id="3e862-739">메뉴 컨트롤에는 의미 체계가 올바르고 내게 필요한 옵션 지침을 사용 하 여 호환 되는 태그를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-739">Menu controls render markup that is semantically correct and compliant with accessibility guidelines.</span></span>
- <span data-ttu-id="3e862-740">유효성 검사 컨트롤 인라인 스타일을 렌더링 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-740">Validation controls do not render inline styles.</span></span>
- <span data-ttu-id="3e862-741">이전에 테두리를 렌더링 하는 제어 = "0" (ASP.NET에서 파생 된 컨트롤 *테이블* 컨트롤과 ASP.NET *이미지* 컨트롤) 더 이상이 특성을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-741">Controls that previously rendered border="0" (controls that derive from the ASP.NET *Table* control, and the ASP.NET *Image* control) no longer render this attribute.</span></span>

#### <a name="disabling-controls"></a><span data-ttu-id="3e862-742">컨트롤을 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="3e862-742">Disabling Controls</span></span>

<span data-ttu-id="3e862-743">ASP.NET 3.5 SP1 및 이전 버전의 프레임 워크는 다음과 같이 렌더링 됩니다. 합니다 *사용 하지 않도록 설정* 모든 컨트롤에 대 한 HTML 태그에 특성 *Enabled* 속성이로 설정 *false*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-743">In ASP.NET 3.5 SP1 and earlier versions, the framework renders the *disabled* attribute in the HTML markup for any control whose *Enabled* property set to *false*.</span></span> <span data-ttu-id="3e862-744">그러나 HTML 4.01 사양에 따라 *입력* 요소에는이 특성이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-744">However, according to the HTML 4.01 specification, only *input* elements should have this attribute.</span></span>

<span data-ttu-id="3e862-745">ASP.NET 4에서 설정할 수 있습니다 합니다 *controlRenderingCompatabilityVersion* "3.5" 다음 예제와 같이 속성:</span><span class="sxs-lookup"><span data-stu-id="3e862-745">In ASP.NET 4, you can set the *controlRenderingCompatabilityVersion* property to "3.5", as in the following example:</span></span>

[!code-xml[Main](overview/samples/sample70.xml)]

<span data-ttu-id="3e862-746">에 대 한 태그를 만들 수 있습니다는 *레이블* 컨트롤을 사용 하지 않도록 설정 하는 다음과 같은 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-746">You might create markup for a *Label* control like the following, which disables the control:</span></span>

[!code-aspx[Main](overview/samples/sample71.aspx)]

<span data-ttu-id="3e862-747">합니다 *레이블* 제어는 다음 HTML을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-747">The *Label* control would render the following HTML:</span></span>

[!code-html[Main](overview/samples/sample72.html)]

<span data-ttu-id="3e862-748">ASP.NET 4에서 설정할 수 있습니다 합니다 *controlRenderingCompatabilityVersion* "4.0"입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-748">In ASP.NET 4, you can set the *controlRenderingCompatabilityVersion* to "4.0".</span></span> <span data-ttu-id="3e862-749">이 경우 렌더링 되는 제어 *입력* 요소가 렌더링 됩니다는 *사용 하지 않도록 설정* 때 특성 컨트롤의 *사용* 속성이 *false* .</span><span class="sxs-lookup"><span data-stu-id="3e862-749">In that case, only controls that render *input* elements will render a *disabled* attribute when the control's *Enabled* property is set to *false*.</span></span> <span data-ttu-id="3e862-750">HTML 렌더링 되지 않는 컨트롤 *입력* 요소 대신 렌더링을 *클래스* 컨트롤에 대 한 비활성화 된 모양을 정의 하는 데 사용할 수 있는 CSS 클래스를 참조 하는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-750">Controls that do not render HTML *input* elements instead render a *class* attribute that references a CSS class that you can use to define a disabled look for the control.</span></span> <span data-ttu-id="3e862-751">예를 들어 합니다 *레이블* 앞의 예제에 표시 되는 컨트롤은 다음 태그를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-751">For example, the *Label* control shown in the earlier example would generate the following markup:</span></span>

[!code-html[Main](overview/samples/sample73.html)]

<span data-ttu-id="3e862-752">이 컨트롤에 대해 지정 하는 클래스에 대 한 기본값은 "aspNetDisabled"입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-752">The default value for the class that specified for this control is "aspNetDisabled".</span></span> <span data-ttu-id="3e862-753">그러나 정적 설정 하 여이 기본값을 변경할 수 있습니다 *DisabledCssClass* 의 정적 속성을 *WebControl* 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-753">However, you can change this default value by setting the static *DisabledCssClass* static property of the *WebControl* class.</span></span> <span data-ttu-id="3e862-754">컨트롤 개발자에 게 특정 컨트롤에 사용할 동작을 정의할 수도 있습니다를 사용 하 여 *SupportsDisabledAttribute* 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-754">For control developers, the behavior to use for a specific control can also be defined using the *SupportsDisabledAttribute* property.</span></span>

<a id="0.2__Toc253429268"></a><a id="0.2__Toc243304642"></a>

### <a name="hiding-div-elements-around-hidden-fields"></a><span data-ttu-id="3e862-755">Div 숨겨진 필드 주위 요소 숨기기</span><span class="sxs-lookup"><span data-stu-id="3e862-755">Hiding div Elements Around Hidden Fields</span></span>

<span data-ttu-id="3e862-756">ASP.NET 2.0 및 이후 버전에는 시스템 관련 숨겨진된 필드 렌더링 (같은 합니다 *숨겨진* 뷰 상태 정보를 저장 하는 데 사용 되는 요소) 내 *div* XHTML 표준을 준수 하기 위해 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-756">ASP.NET 2.0 and later versions render system-specific hidden fields (such as the *hidden* element used to store view state information) inside *div* element in order to comply with the XHTML standard.</span></span> <span data-ttu-id="3e862-757">그러나 CSS 규칙을 적용 하면 문제가 발생할 수 있습니다이 *div* 페이지의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-757">However, this can cause a problem when a CSS rule affects *div* elements on a page.</span></span> <span data-ttu-id="3e862-758">예를 들어 페이지에 표시 되는 1 픽셀 줄에서 발생할 수 있습니다 약 숨겨진 *div* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-758">For example, it can result in a one-pixel line appearing in the page around hidden *div* elements.</span></span> <span data-ttu-id="3e862-759">ASP.NET 4에서 *div* ASP.NET에서 생성 된 숨겨진된 필드를 포함 하는 요소는 다음 예제와 같이 CSS 클래스 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-759">In ASP.NET 4, *div* elements that enclose the hidden fields generated by ASP.NET add a CSS class reference as in the following example:</span></span>

[!code-html[Main](overview/samples/sample74.html)]

<span data-ttu-id="3e862-760">다음에 적용 되는 CSS 클래스를 정의할 수 있습니다 합니다 *숨겨진* 다음 예제와 같이 ASP.NET에서 생성 되는 요소:</span><span class="sxs-lookup"><span data-stu-id="3e862-760">You can then define a CSS class that applies only to the *hidden* elements that are generated by ASP.NET, as in the following example:</span></span>

[!code-css[Main](overview/samples/sample75.css)]

<a id="0.2__Toc253429269"></a><a id="0.2__Toc243304643"></a>

### <a name="rendering-an-outer-table-for-templated-controls"></a><span data-ttu-id="3e862-761">템플릿 기반 컨트롤에 대 한 외부 테이블을 렌더링</span><span class="sxs-lookup"><span data-stu-id="3e862-761">Rendering an Outer Table for Templated Controls</span></span>

<span data-ttu-id="3e862-762">기본적으로 템플릿을 지 원하는 다음 ASP.NET 웹 서버 컨트롤은 인라인 스타일을 적용 하는 데 사용 되는 외부 테이블에 자동으로 줄:</span><span class="sxs-lookup"><span data-stu-id="3e862-762">By default, the following ASP.NET Web server controls that support templates are automatically wrapped in an outer table that is used to apply inline styles:</span></span>

- <span data-ttu-id="3e862-763">*FormView*</span><span class="sxs-lookup"><span data-stu-id="3e862-763">*FormView*</span></span>
- <span data-ttu-id="3e862-764">*로그인*</span><span class="sxs-lookup"><span data-stu-id="3e862-764">*Login*</span></span>
- <span data-ttu-id="3e862-765">*PasswordRecovery*</span><span class="sxs-lookup"><span data-stu-id="3e862-765">*PasswordRecovery*</span></span>
- <span data-ttu-id="3e862-766">*ChangePassword*</span><span class="sxs-lookup"><span data-stu-id="3e862-766">*ChangePassword*</span></span>
- <span data-ttu-id="3e862-767">*마법사*</span><span class="sxs-lookup"><span data-stu-id="3e862-767">*Wizard*</span></span>
- <span data-ttu-id="3e862-768">*CreateUserWizard*</span><span class="sxs-lookup"><span data-stu-id="3e862-768">*CreateUserWizard*</span></span>

<span data-ttu-id="3e862-769">라는 새 속성을 *RenderOuterTable* 태그에서 제거할 외부 테이블을 허용 하는 이러한 컨트롤에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-769">A new property named *RenderOuterTable* has been added to these controls that allows the outer table to be removed from the markup.</span></span> <span data-ttu-id="3e862-770">예를 들어 다음 예제는 *FormView* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-770">For example, consider the following example of a *FormView* control:</span></span>

[!code-aspx[Main](overview/samples/sample76.aspx)]

<span data-ttu-id="3e862-771">이 태그에 다음 출력을 HTML 테이블을 포함 하는 페이지를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-771">This markup renders the following output to the page, which includes an HTML table:</span></span>

[!code-html[Main](overview/samples/sample77.html)]

<span data-ttu-id="3e862-772">테이블을 렌더링 되지 않도록 방지 하려면 설정할 수 있습니다 합니다 *FormView* 컨트롤의 *RenderOuterTable* 다음 예제와 같이 속성:</span><span class="sxs-lookup"><span data-stu-id="3e862-772">To prevent the table from being rendered, you can set the *FormView* control's *RenderOuterTable* property, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample78.aspx)]

<span data-ttu-id="3e862-773">앞의 예제 출력을 하지 않고 다음 렌더링 합니다 *테이블*를 *tr*, 및 *td* 요소:</span><span class="sxs-lookup"><span data-stu-id="3e862-773">The previous example renders the following output, without the *table*, *tr*, and *td* elements:</span></span>

> <span data-ttu-id="3e862-774">콘텐츠</span><span class="sxs-lookup"><span data-stu-id="3e862-774">Content</span></span>


<span data-ttu-id="3e862-775">이 향상 된이 기능 수 쉽게 스타일 CSS 사용 하 여 컨트롤의 콘텐츠 컨트롤에 의해 예기치 않은 태그가 렌더링 되기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-775">This enhancement can make it easier to style the content of the control with CSS, because no unexpected tags are rendered by the control.</span></span>

> [!NOTE]
> <span data-ttu-id="3e862-776">이 변경 때문에 더 이상 Visual Studio 2010 디자이너에서 자동 format 함수에 대 한 지원을 사용 하지 않도록 설정 하는 참고를 *테이블* 자동 서식 옵션에 의해 생성 되는 스타일 특성을 호스트할 수 있는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-776">Note This change disables support for the auto-format function in the Visual Studio 2010 designer, because there is no longer a *table* element that can host style attributes that are generated by the auto-format option.</span></span>


<a id="0.2__Toc253429270"></a><a id="0.2__Toc243304644"></a>

### <a name="listview-control-enhancements"></a><span data-ttu-id="3e862-777">향상 된 ListView 컨트롤</span><span class="sxs-lookup"><span data-stu-id="3e862-777">ListView Control Enhancements</span></span>

<span data-ttu-id="3e862-778">합니다 *ListView* 컨트롤 내용이 ASP.NET 4에서 사용 하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-778">The *ListView* control has been made easier to use in ASP.NET 4.</span></span> <span data-ttu-id="3e862-779">컨트롤의 이전 버전 알려진 id 서버 컨트롤을 포함 하는 레이아웃 템플릿을 지정 하는 데 필요한</span><span class="sxs-lookup"><span data-stu-id="3e862-779">The earlier version of the control required that you specify a layout template that contained a server control with a known ID.</span></span> <span data-ttu-id="3e862-780">다음 태그를 사용 하는 방법의 일반적인 예제는 *ListView* ASP.NET 3.5에서 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-780">The following markup shows a typical example of how to use the *ListView* control in ASP.NET 3.5.</span></span>

[!code-aspx[Main](overview/samples/sample79.aspx)]

<span data-ttu-id="3e862-781">ASP.NET 4에는 *ListView* 컨트롤의 레이아웃 템플릿이 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-781">In ASP.NET 4, the *ListView* control does not require a layout template.</span></span> <span data-ttu-id="3e862-782">이전 예에서 같이 태그에 다음 태그를 사용 하 여 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-782">The markup shown in the previous example can be replaced with the following markup:</span></span>

[!code-aspx[Main](overview/samples/sample80.aspx)]

<a id="0.2__Toc253429271"></a><a id="0.2__Toc243304645"></a>

### <a name="checkboxlist-and-radiobuttonlist-control-enhancements"></a><span data-ttu-id="3e862-783">CheckBoxList 및 RadioButtonList 컨트롤 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="3e862-783">CheckBoxList and RadioButtonList Control Enhancements</span></span>

<span data-ttu-id="3e862-784">ASP.NET 3.5에서에 대 한 레이아웃을 지정할 수 있습니다 합니다 *CheckBoxList* 하 고 *RadioButtonList* 다음 두 설정을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="3e862-784">In ASP.NET 3.5, you can specify layout for the *CheckBoxList* and *RadioButtonList* using the following two settings:</span></span>

- <span data-ttu-id="3e862-785">*흐름*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-785">*Flow*.</span></span> <span data-ttu-id="3e862-786">컨트롤 렌더링 *걸쳐* 해당 콘텐츠를 포함 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-786">The control renders *span* elements to contain its content.</span></span>
- <span data-ttu-id="3e862-787">*테이블*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-787">*Table*.</span></span> <span data-ttu-id="3e862-788">컨트롤 렌더링을 *테이블* 해당 콘텐츠를 포함 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-788">The control renders a *table* element to contain its content.</span></span>

<span data-ttu-id="3e862-789">다음 예제에서는 이러한 각 컨트롤에 대 한 태그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-789">The following example shows markup for each of these controls.</span></span>

[!code-aspx[Main](overview/samples/sample81.aspx)]

<span data-ttu-id="3e862-790">기본적으로 컨트롤을 렌더링 HTML 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-790">By default, the controls render HTML similar to the following:</span></span>

[!code-html[Main](overview/samples/sample82.html)]

<span data-ttu-id="3e862-791">HTML 목록을 사용 하 여 해당 콘텐츠를 렌더링 해야 이러한 컨트롤 의미적으로 HTML을 렌더링 하기 위한 항목 목록이 포함 되어 있으므로 (*li*) 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-791">Because these controls contain lists of items, to render semantically correct HTML, they should render their contents using HTML list (*li*) elements.</span></span> <span data-ttu-id="3e862-792">이렇게 하면 보조 기술을 사용 하 여 웹 페이지를 읽고 컨트롤을 더 쉽게 CSS를 사용 하 여 스타일을 사용자에 대해 쉽게 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-792">This makes it easier for users who read Web pages using assistive technology, and makes the controls easier to style using CSS.</span></span>

<span data-ttu-id="3e862-793">ASP.NET 4에는 *CheckBoxList* 및 *RadioButtonList* 컨트롤에 대 한 다음 새 값을 지원 합니다 *RepeatLayout* 속성:</span><span class="sxs-lookup"><span data-stu-id="3e862-793">In ASP.NET 4, the *CheckBoxList* and *RadioButtonList* controls support the following new values for the *RepeatLayout* property:</span></span>

- <span data-ttu-id="3e862-794">*OrderedList* –으로 콘텐츠를 렌더링할 *li* 내에서 요소를 *ol* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-794">*OrderedList* – The content is rendered as *li* elements within an *ol* element.</span></span>
- <span data-ttu-id="3e862-795">*UnorderedList* –으로 콘텐츠를 렌더링할 *li* 내에서 요소를 *ul* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-795">*UnorderedList* – The content is rendered as *li* elements within a *ul* element.</span></span>

<span data-ttu-id="3e862-796">다음 예제에서는 이러한 새 값을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-796">The following example shows how to use these new values.</span></span>

[!code-aspx[Main](overview/samples/sample83.aspx)]

<span data-ttu-id="3e862-797">위의 태그는 다음 HTML을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-797">The preceding markup generates the following HTML:</span></span>

[!code-html[Main](overview/samples/sample84.html)]

> [!NOTE]
> <span data-ttu-id="3e862-798">설정 하는 경우 *RepeatLayout* 하 *OrderedList* 또는 *UnorderedList*서 *RepeatDirection* 속성이 더 이상 사용할 수 있으며 됩니다 태그 또는 코드 내에서 속성을 설정한 경우 런타임 시 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-798">Note If you set *RepeatLayout* to *OrderedList* or *UnorderedList*, the *RepeatDirection* property can no longer be used and will throw an exception at run time if the property has been set within your markup or code.</span></span> <span data-ttu-id="3e862-799">CSS를 대신 사용 하 여 이러한 컨트롤의 시각적 레이아웃 정의 되어 있으므로 속성 값이 없는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-799">The property would have no value because the visual layout of these controls is defined using CSS instead.</span></span>


<a id="0.2__Toc253429272"></a><a id="0.2__Toc243304646"></a>

### <a name="menu-control-improvements"></a><span data-ttu-id="3e862-800">메뉴 제어 기능 향상</span><span class="sxs-lookup"><span data-stu-id="3e862-800">Menu Control Improvements</span></span>

<span data-ttu-id="3e862-801">ASP.NET 4 이전 합니다 *메뉴* 컨트롤이 일련의 HTML 테이블을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-801">Before ASP.NET 4, the *Menu* control rendered a series of HTML tables.</span></span> <span data-ttu-id="3e862-802">이 인라인 속성을 설정 하는 외부 CSS 스타일을 적용 하는 것이 어려울 수 및 없습니다. 또한 접근성 표준을 준수 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-802">This made it more difficult to apply CSS styles outside of setting inline properties and was also not compliant with accessibility standards.</span></span>

<span data-ttu-id="3e862-803">ASP.NET 4에서 컨트롤이 이제 순서 없는 목록 및 목록 요소 구성 된 의미 체계 태그를 사용 하 여 HTML을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-803">In ASP.NET 4, the control now renders HTML using semantic markup that consists of an unordered list and list elements.</span></span> <span data-ttu-id="3e862-804">다음 예제에 대 한 ASP.NET 페이지에서 태그를 보여 줍니다.는 *메뉴* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-804">The following example shows markup in an ASP.NET page for the *Menu* control.</span></span>

[!code-aspx[Main](overview/samples/sample85.aspx)]

<span data-ttu-id="3e862-805">페이지가 렌더링 하는 경우 컨트롤은 다음 HTML을 생성 하는 (합니다 *onclick* 코드 명확성을 위해 생략 됨):</span><span class="sxs-lookup"><span data-stu-id="3e862-805">When the page renders, the control produces the following HTML (the *onclick* code has been omitted for clarity):</span></span>

[!code-html[Main](overview/samples/sample86.html)]

<span data-ttu-id="3e862-806">렌더링 향상 된 메뉴의 키보드 탐색 기능이 향상 되었습니다 포커스 관리를 사용 하 여.</span><span class="sxs-lookup"><span data-stu-id="3e862-806">In addition to rendering improvements, keyboard navigation of the menu has been improved using focus management.</span></span> <span data-ttu-id="3e862-807">경우는 *메뉴* 컨트롤이 포커스를 받으면, 화살표 키를 사용 하 여 요소를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-807">When the *Menu* control gets focus, you can use the arrow keys to navigate elements.</span></span> <span data-ttu-id="3e862-808">*메뉴* 제어도 액세스할 수 있는 풍부한 인터넷 응용 프로그램 (ARIA) 역할을 연결 및 함 특성[wing 합니다](http://www.w3.org/TR/wai-aria-practices/#menu "메뉴 ARIA 지침")개선 내게 필요한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-808">The *Menu* control also now attaches accessible rich internet applications (ARIA) roles and attributes follo[wing the](http://www.w3.org/TR/wai-aria-practices/#menu "Menu ARIA guidelines")for improved accessibility.</span></span>

<span data-ttu-id="3e862-809">메뉴 컨트롤에 대 한 스타일을 스타일 블록의 맨 위에 있는 페이지 대신 렌더링 된 HTML 요소에 따라 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-809">Styles for the menu control are rendered in a style block at the top of the page, rather than in line with the rendered HTML elements.</span></span> <span data-ttu-id="3e862-810">컨트롤의 스타일을 통해 완전 한 제어 하려는 경우 설정할 수 있습니다 새 *IncludeStyleBlock* 속성을 *false*, 스타일 블록을 내보내지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="3e862-810">If you want to take full control over the styling for the control, you can set the new *IncludeStyleBlock* property to *false*, in which case the style block is not emitted.</span></span> <span data-ttu-id="3e862-811">이 속성을 사용 하는 한 가지 방법은 메뉴의 모양을 설정 하는 Visual Studio 디자이너에서 자동 서식 기능을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-811">One way to use this property is to use the auto-format feature in the Visual Studio designer to set the appearance of the menu.</span></span> <span data-ttu-id="3e862-812">다음 페이지를 실행, 페이지 원본을 열고 렌더링된 스타일 블록 외부 CSS 파일에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-812">You can then run the page, open the page source, and then copy the rendered style block to an external CSS file.</span></span> <span data-ttu-id="3e862-813">Visual Studio의 스타일 지정 및 집합 실행 취소 *IncludeStyleBlock* 하 *false*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-813">In Visual Studio, undo the styling and set *IncludeStyleBlock* to *false*.</span></span> <span data-ttu-id="3e862-814">결과 메뉴가 표시 스타일을 사용 하 여 외부 스타일 시트에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-814">The result is that the menu appearance is defined using styles in an external style sheet.</span></span>

<a id="0.2__Toc253429273"></a><a id="0.2__Toc243304647"></a>

### <a name="wizard-and-createuserwizard-controls"></a><span data-ttu-id="3e862-815">마법사 및 CreateUserWizard 컨트롤</span><span class="sxs-lookup"><span data-stu-id="3e862-815">Wizard and CreateUserWizard Controls</span></span>

<span data-ttu-id="3e862-816">ASP.NET *마법사* 하 고 *CreateUserWizard* 컨트롤을 렌더링 하는 HTML을 정의할 수 있는 템플릿을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-816">The ASP.NET *Wizard* and *CreateUserWizard* controls support templates that let you define the HTML that they render.</span></span> <span data-ttu-id="3e862-817">(*CreateUserWizard* 에서 파생 되 *마법사*.) 다음 예제에서는 완전히 템플릿 기반 태그를 보여 줍니다 *CreateUserWizard* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-817">(*CreateUserWizard* derives from *Wizard*.) The following example shows the markup for a fully templated *CreateUserWizard* control:</span></span>

[!code-aspx[Main](overview/samples/sample87.aspx)]

<span data-ttu-id="3e862-818">컨트롤 다음과 유사한 HTML을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-818">The control renders HTML similar to the following:</span></span>

[!code-html[Main](overview/samples/sample88.html)]

<span data-ttu-id="3e862-819">ASP.NET 3.5 sp1의 경우 템플릿 내용을 변경할 수 있지만 여전히 제한의 출력을 제어 합니다 *마법사* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-819">In ASP.NET 3.5 SP1, although you can change the template contents, you still have limited control over the output of the *Wizard* control.</span></span> <span data-ttu-id="3e862-820">ASP.NET 4에서 만들 수 있습니다를 *LayoutTemplate* 템플릿과 삽입 *자리 표시자* 방법을 지정할 수 있습니다 (예약 된 이름 사용)을 제어 합니다 *마법사 컨트롤* 렌더링 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-820">In ASP.NET 4, you can create a *LayoutTemplate* template and insert *PlaceHolder* controls (using reserved names) to specify how you want the *Wizard control* to render.</span></span> <span data-ttu-id="3e862-821">다음 예제에서는이 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-821">The following example shows this:</span></span>

[!code-aspx[Main](overview/samples/sample89.aspx)]

<span data-ttu-id="3e862-822">명명 된 자리 표시자에 다음을 포함 하는 예제는 *LayoutTemplate* 요소:</span><span class="sxs-lookup"><span data-stu-id="3e862-822">The example contains the following named placeholders in the *LayoutTemplate* element:</span></span>

- <span data-ttu-id="3e862-823">*headerPlaceholder* – 런타임 시이 바뀝니다 내용의 합니다 *머리글 템플릿의* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-823">*headerPlaceholder* – At run time, this is replaced by the contents of the *HeaderTemplate* element.</span></span>
- <span data-ttu-id="3e862-824">*sideBarPlaceholder* – 런타임 시이 바뀝니다 내용의 합니다 *SideBarTemplate* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-824">*sideBarPlaceholder* – At run time, this is replaced by the contents of the *SideBarTemplate* element.</span></span>
- <span data-ttu-id="3e862-825">*wizardStepPlaceHolder* – 런타임 시이 바뀝니다 내용의 합니다 *WizardStepTemplate* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-825">*wizardStepPlaceHolder* – At run time, this is replaced by the contents of the *WizardStepTemplate* element.</span></span>
- <span data-ttu-id="3e862-826">*navigationPlaceholder* – 런타임 시 정의 된 모든 탐색 템플릿에서 대체 됩니다이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-826">*navigationPlaceholder* – At run time, this is replaced by any navigation templates that you have defined.</span></span>

<span data-ttu-id="3e862-827">자리 표시자를 사용 하는 예제 태그 (실제로 템플릿에 정의 된 콘텐츠) 없이 다음 HTML을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-827">The markup in the example that uses placeholders renders the following HTML (without the content actually defined in the templates):</span></span>

[!code-html[Main](overview/samples/sample90.html)]

<span data-ttu-id="3e862-828">이제 정의 되지 않은 사용자-만 HTML이를 *걸쳐* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-828">The only HTML that is now not user-defined is a *span* element.</span></span> <span data-ttu-id="3e862-829">(릴리스에서 향후 예정 아무리 *s p a n* 요소 렌더링 되지 것입니다.) 이 구문은 이제에서 생성 되는 거의 모든 콘텐츠에 대 한 전체 권한을 제공 합니다 *마법사* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-829">(We anticipate that in future releases, even the *span* element will not be rendered.) This now gives you full control over virtually all the content that is generated by the *Wizard* control.</span></span>

<a id="0.2_dyndata"></a><a id="0.2__Toc253429274"></a><a id="0.2__Toc243304648"></a><a id="0.2__Toc224729042"></a>

## <a name="aspnet-mvc"></a><span data-ttu-id="3e862-830">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="3e862-830">ASP.NET MVC</span></span>

<span data-ttu-id="3e862-831">ASP.NET MVC 2009 년 3 월에에서는 추가 기능 프레임 워크로 ASP.NET 3.5 SP1에 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-831">ASP.NET MVC was introduced as an add-on framework to ASP.NET 3.5 SP1 in March 2009.</span></span> <span data-ttu-id="3e862-832">Visual Studio 2010 새로운 특징과 기능을 포함 하는 ASP.NET MVC 2를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-832">Visual Studio 2010 includes ASP.NET MVC 2, which includes new features and capabilities.</span></span>

<a id="0.2__Toc253429275"></a>

### <a name="areas-support"></a><span data-ttu-id="3e862-833">영역 지원</span><span class="sxs-lookup"><span data-stu-id="3e862-833">Areas Support</span></span>

<span data-ttu-id="3e862-834">영역을 사용 하면 다른 섹션에서 상대 격리에서 많은 응용 프로그램의 섹션으로 그룹 컨트롤러 및 보기.</span><span class="sxs-lookup"><span data-stu-id="3e862-834">Areas let you group controllers and views into sections of a large application in relative isolation from other sections.</span></span> <span data-ttu-id="3e862-835">각 영역으로 주 응용 프로그램에서 참조 될 수 있는 별도 ASP.NET MVC 프로젝트를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-835">Each area can be implemented as a separate ASP.NET MVC project that can then be referenced by the main application.</span></span> <span data-ttu-id="3e862-836">이 대규모 응용 프로그램을 빌드할 때 복잡성을 관리 하는 데 도움이 됩니다 하 고 쉽게 여러 팀이 단일 응용 프로그램에서 함께 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-836">This helps manage complexity when you build a large application and makes it easier for multiple teams to work together on a single application.</span></span>

<a id="0.2__Toc253429276"></a>

### <a name="data-annotation-attribute-validation-support"></a><span data-ttu-id="3e862-837">데이터 주석 특성의 유효성 검사 지원</span><span class="sxs-lookup"><span data-stu-id="3e862-837">Data-Annotation Attribute Validation Support</span></span>

<span data-ttu-id="3e862-838">*DataAnnotations* 특성 메타 데이터 특성을 사용 하 여 모델에 유효성 검사 논리를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-838">*DataAnnotations* attributes let you attach validation logic to a model by using metadata attributes.</span></span> <span data-ttu-id="3e862-839">*DataAnnotations* 특성 ASP.NET Dynamic Data ASP.NET 3.5 sp1에서에서 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-839">*DataAnnotations* attributes were introduced in ASP.NET Dynamic Data in ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="3e862-840">이러한 특성은 기본 모델 바인더에 통합 되었습니다 및 사용자 입력의 유효성을 검사 하는 메타 데이터 기반 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-840">These attributes have been integrated into the default model binder and provide a metadata-driven means to validate user input.</span></span>

<a id="0.2__Toc253429277"></a>

### <a name="templated-helpers"></a><span data-ttu-id="3e862-841">템플릿 기반 도우미</span><span class="sxs-lookup"><span data-stu-id="3e862-841">Templated Helpers</span></span>

<span data-ttu-id="3e862-842">자동으로 연결 편집 수 하 고 데이터 형식을 사용 하 여 템플릿을 표시 하는 템플릿 기반 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-842">Templated helpers let you automatically associate edit and display templates with data types.</span></span> <span data-ttu-id="3e862-843">예를 들어, 날짜 선택 UI 요소에 대해 자동으로 렌더링 되는 지정 하는 템플릿 도우미를 사용할 수 있습니다는 *System.DateTime* 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-843">For example, you can use a template helper to specify that a date-picker UI element is automatically rendered for a *System.DateTime* value.</span></span> <span data-ttu-id="3e862-844">ASP.NET Dynamic Data에 필드 템플릿에 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-844">This is similar to field templates in ASP.NET Dynamic Data.</span></span>

<span data-ttu-id="3e862-845">합니다 *Html.EditorFor* 하 고 *Html.DisplayFor* 여러 속성을 사용 하 여도 복잡 한 개체 형식 표준 데이터 렌더링에 대 한 도우미 메서드는 기본 제공 지원.</span><span class="sxs-lookup"><span data-stu-id="3e862-845">The *Html.EditorFor* and *Html.DisplayFor* helper methods have built-in support for rendering standard data types as well as complex objects with multiple properties.</span></span> <span data-ttu-id="3e862-846">또한 렌더링을 사용자 지정 데이터 주석 특성을 적용할 수 있도록 하 여 *DisplayName* 하 고 *ScaffoldColumn* 에 *ViewModel* 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-846">They also customize rendering by letting you apply data-annotation attributes like *DisplayName* and *ScaffoldColumn* to the *ViewModel* object.</span></span>

<span data-ttu-id="3e862-847">종종 하려는 UI 도우미 더욱에서 출력을 사용자 지정 및 완전히 제어 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-847">Often you want to customize the output from UI helpers even further and have complete control over what is generated.</span></span> <span data-ttu-id="3e862-848">합니다 *Html.EditorFor* 하 고 *Html.DisplayFor* 도우미 메서드를 지원이 재정의할 수 있는 외부 템플릿과 컨트롤 렌더링 된 출력을 정의할 수 있는 템플릿 메커니즘을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-848">The *Html.EditorFor* and *Html.DisplayFor* helper methods support this using a templating mechanism that lets you define external templates that can override and control the output rendered.</span></span> <span data-ttu-id="3e862-849">템플릿은 클래스에 대해 개별적으로 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-849">The templates can be rendered individually for a class.</span></span>

<a id="0.2__Toc253429278"></a><a id="0.2__Toc243304649"></a>

## <a name="dynamic-data"></a><span data-ttu-id="3e862-850">Dynamic Data</span><span class="sxs-lookup"><span data-stu-id="3e862-850">Dynamic Data</span></span>

<span data-ttu-id="3e862-851">동적 데이터 도입 2008 년 중순에.NET Framework 3.5 SP1 릴리스에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-851">Dynamic Data was introduced in the .NET Framework 3.5 SP1 release in mid-2008.</span></span> <span data-ttu-id="3e862-852">이 기능은 다음을 포함 하는 데이터 기반 응용 프로그램에 대 한 많은 향상 된 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-852">This feature provides many enhancements for creating data-driven applications, including the following:</span></span>

- <span data-ttu-id="3e862-853">데이터 기반 웹 사이트를 신속 하 게 빌드하기 위한 RAD 환경.</span><span class="sxs-lookup"><span data-stu-id="3e862-853">A RAD experience for quickly building a data-driven Web site.</span></span>
- <span data-ttu-id="3e862-854">데이터 모델에 정의 된 제약 조건을 기반으로 하는 자동 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="3e862-854">Automatic validation that is based on constraints defined in the data model.</span></span>
- <span data-ttu-id="3e862-855">필드에 대해 생성 되는 태그를 쉽게 변경할 수는 *GridView* 하 고 *DetailsView* 동적 데이터 프로젝트의 일부인 필드 템플릿을 사용 하 여 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-855">The ability to easily change the markup that is generated for fields in the *GridView* and *DetailsView* controls by using field templates that are part of your Dynamic Data project.</span></span>

> [!NOTE]
> <span data-ttu-id="3e862-856">자세한 내용은 참고를 참조 하십시오 합니다 [동적 데이터 설명서](https://msdn.microsoft.com/library/cc488545.aspx) MSDN 라이브러리에서.</span><span class="sxs-lookup"><span data-stu-id="3e862-856">Note For more information, see the [Dynamic Data documentation](https://msdn.microsoft.com/library/cc488545.aspx) in the MSDN Library.</span></span>


<span data-ttu-id="3e862-857">ASP.NET 4에 대 한 동적 데이터 신속 하 게 데이터 기반 웹 사이트를 구축 하기 위한 개발자에 게 더 많은 기능을 제공 하도록 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-857">For ASP.NET 4, Dynamic Data has been enhanced to give developers even more power for quickly building data-driven Web sites.</span></span>

<a id="0.2__Toc253429279"></a><a id="0.2__Toc243304650"></a>

### <a name="enabling-dynamic-data-for-existing-projects"></a><span data-ttu-id="3e862-858">기존 프로젝트에 대 한 동적 데이터를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="3e862-858">Enabling Dynamic Data for Existing Projects</span></span>

<span data-ttu-id="3e862-859">.NET Framework 3.5 SP1에서 제공 되는 동적 데이터 기능 상태가 다음과 같은 새로운 기능:</span><span class="sxs-lookup"><span data-stu-id="3e862-859">Dynamic Data features that shipped in the .NET Framework 3.5 SP1 brought new features such as the following:</span></span>

- <span data-ttu-id="3e862-860">필드 템플릿 – 데이터 바인딩된 컨트롤에 대 한 데이터 형식을 기반 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-860">Field templates – These provide data-type-based templates for data-bound controls.</span></span> <span data-ttu-id="3e862-861">필드 템플릿을 템플릿 필드를 사용 하 여 각 필드에 대 한 보다 데이터 컨트롤의 모양을 사용자 지정 하는 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-861">Field templates provide a simpler way to customize the look of data controls than using template fields for each field.</span></span>
- <span data-ttu-id="3e862-862">유효성 검사 – 동적 데이터에서 사용할 수 있습니다 특성 데이터 클래스 필수 필드, 범위 검사, 형식 검사, 패턴 일치, 정규식을 사용 하 여 일반적인 시나리오에 대 한 유효성 검사 및 사용자 지정 유효성 검사를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-862">Validation – Dynamic Data lets you use attributes on data classes to specify validation for common scenarios like required fields, range checking, type checking, pattern matching using regular expressions, and custom validation.</span></span> <span data-ttu-id="3e862-863">유효성 검사는 데이터 컨트롤에 의해 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-863">Validation is enforced by the data controls.</span></span>

<span data-ttu-id="3e862-864">그러나 이러한 기능에는 다음 요구 사항이 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-864">However, these features had the following requirements:</span></span>

- <span data-ttu-id="3e862-865">Entity Framework 또는 LINQ to SQL 기반으로 하는 데이터 액세스 계층이 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-865">The data-access layer had to be based on Entity Framework or LINQ to SQL.</span></span>
- <span data-ttu-id="3e862-866">유일한 데이터 소스 컨트롤과 이러한 기능에 대해 지원 되는 *EntityDataSource* 또는 *LinqDataSource* 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-866">The only data source controls supported for these features were the *EntityDataSource* or *LinqDataSource* controls.</span></span>
- <span data-ttu-id="3e862-867">기능에는 기능을 지원 해야 하는 모든 파일을 위해서는 동적 데이터 또는 동적 데이터 엔터티 템플릿을 사용 하 여 만든 웹 프로젝트를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-867">The features required a Web project that had been created using the Dynamic Data or Dynamic Data Entities templates in order to have all the files that were required to support the feature.</span></span>

<span data-ttu-id="3e862-868">ASP.NET 4에서 동적 데이터 지원의 주요 목표는 모든 ASP.NET 응용 프로그램에 대 한 동적 데이터의 새 기능.</span><span class="sxs-lookup"><span data-stu-id="3e862-868">A major goal of Dynamic Data support in ASP.NET 4 is to enable the new functionality of Dynamic Data for any ASP.NET application.</span></span> <span data-ttu-id="3e862-869">다음 예제에서는 기존 페이지에 Dynamic Data 기능을 사용할 수 있는 컨트롤에 대 한 태그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-869">The following example shows markup for controls that can take advantage of Dynamic Data functionality in an existing page.</span></span>

[!code-aspx[Main](overview/samples/sample91.aspx)]

<span data-ttu-id="3e862-870">페이지에 대 한 코드에서 이러한 컨트롤에 대 한 동적 데이터 지원을 사용 하도록 설정 하려면 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-870">In the code for the page, the following code must be added in order to enable Dynamic Data support for these controls:</span></span>

[!code-csharp[Main](overview/samples/sample92.cs)]

<span data-ttu-id="3e862-871">경우는 *GridView* 컨트롤이 편집 모드 인지, 동적 데이터를 자동으로 입력 한 데이터가 올바른 형식 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-871">When the *GridView* control is in edit mode, Dynamic Data automatically validates that the data entered is in the proper format.</span></span> <span data-ttu-id="3e862-872">없는 경우 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-872">If it is not, an error message is displayed.</span></span>

<span data-ttu-id="3e862-873">이 기능에도 다른 이점이, 값 삽입 모드 등 기본값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-873">This functionality also provides other benefits, such as being able to specify default values for insert mode.</span></span> <span data-ttu-id="3e862-874">동적 데이터 없이 필드에 대해 기본값을 구현 해야 합니다 이벤트에 연결 하십시오 컨트롤을 찾습니다 (사용 하 여 *FindControl*), 해당 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-874">Without Dynamic Data, to implement a default value for a field, you must attach to an event, locate the control (using *FindControl*), and set its value.</span></span> <span data-ttu-id="3e862-875">ASP.NET 4에서 합니다 *EnableDynamicData* 호출이 예와에서 같이 개체에서 모든 필드에 대 한 기본 값을 전달할 수 있도록 하는 두 번째 매개 변수를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-875">In ASP.NET 4, the *EnableDynamicData* call supports a second parameter that lets you pass default values for any field on the object, as shown in this example:</span></span>

[!code-csharp[Main](overview/samples/sample93.cs)]

<a id="0.2__Toc224729043"></a><a id="0.2__Toc253429280"></a><a id="0.2__Toc243304651"></a>

### <a name="declarative-dynamicdatamanager-control-syntax"></a><span data-ttu-id="3e862-876">DynamicDataManager 컨트롤 선언 구문</span><span class="sxs-lookup"><span data-stu-id="3e862-876">Declarative DynamicDataManager Control Syntax</span></span>

<span data-ttu-id="3e862-877">합니다 *DynamicDataManager* 선언적으로 구성할 수 있도록 제어 기능이 향상 되었습니다 마찬가지로 코드에서 하는 대신 ASP.NET에서 대부분의 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-877">The *DynamicDataManager* control has been enhanced so that you can configure it declaratively, as with most controls in ASP.NET, instead of only in code.</span></span> <span data-ttu-id="3e862-878">에 대 한 태그를 *DynamicDataManager* 컨트롤은 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-878">The markup for the *DynamicDataManager* control looks like the following example:</span></span>

[!code-aspx[Main](overview/samples/sample94.aspx)]

<span data-ttu-id="3e862-879">이 태그에서 참조 되는 GridView1 컨트롤에 대 한 동적 데이터 동작을 활성화 합니다 *다음* 부분을 *DynamicDataManager* 컨트롤.</span><span class="sxs-lookup"><span data-stu-id="3e862-879">This markup enables Dynamic Data behavior for the GridView1 control that is referenced in the *DataControls* section of the *DynamicDataManager* control.</span></span>

<a id="0.2__Toc224729044"></a><a id="0.2__Toc253429281"></a><a id="0.2__Toc243304652"></a>

### <a name="entity-templates"></a><span data-ttu-id="3e862-880">엔터티 템플릿</span><span class="sxs-lookup"><span data-stu-id="3e862-880">Entity Templates</span></span>

<span data-ttu-id="3e862-881">엔터티 템플릿을 사용자 지정 페이지 할 필요 없이 데이터의 레이아웃을 사용자 지정 하는 새로운 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-881">Entity templates offer a new way to customize the layout of data without requiring you to create a custom page.</span></span> <span data-ttu-id="3e862-882">템플릿을 사용 하 여 페이지의 *FormView* 컨트롤 (대신 합니다 *DetailsView* 동적 데이터의 이전 버전의 페이지 템플릿에서 사용 되는 컨트롤) 및 *DynamicEntity* 엔터티 템플릿이 렌더링 될 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-882">Page templates use the *FormView* control (instead of the *DetailsView* control, as used in page templates in earlier versions of Dynamic Data) and the *DynamicEntity* control to render Entity templates.</span></span> <span data-ttu-id="3e862-883">Dynamic Data에서 렌더링 되는 태그를 자세한 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-883">This gives you more control over the markup that is rendered by Dynamic Data.</span></span>

<span data-ttu-id="3e862-884">다음은 엔터티 템플릿이 포함 된 새 프로젝트 디렉터리 레이아웃을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-884">The following list shows the new project directory layout that contains entity templates:</span></span>

[!code-console[Main](overview/samples/sample95.cmd)]

<span data-ttu-id="3e862-885">`EntityTemplate` 디렉터리 데이터 모델 개체를 표시 하는 방법에 대 한 템플릿을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-885">The `EntityTemplate` directory contains templates for how to display data model objects.</span></span> <span data-ttu-id="3e862-886">기본적으로 개체를 사용 하 여 렌더링 됩니다는 `Default.ascx` 에서 만든 태그 처럼 보이는 태그를 제공 하는 템플릿 합니다 *DetailsView* ASP.NET 3.5 SP1에 Dynamic Data에서 사용 되는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-886">By default, objects are rendered by using the `Default.ascx` template, which provides markup that looks just like the markup created by the *DetailsView* control used by Dynamic Data in ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="3e862-887">다음 예제에서는 태그를 보여 줍니다.는 `Default.ascx` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-887">The following example shows the markup for the `Default.ascx` control:</span></span>

[!code-aspx[Main](overview/samples/sample96.aspx)]

<span data-ttu-id="3e862-888">전체 사이트에 대 한 디자인을 변경 하려면 기본 템플릿은 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-888">The default templates can be edited to change the look and feel for the entire site.</span></span> <span data-ttu-id="3e862-889">표시, 편집 및 삽입 작업에 대 한 템플릿이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-889">There are templates for display, edit, and insert operations.</span></span> <span data-ttu-id="3e862-890">새 템플릿은 추가할 수 있습니다 데이터 개체의 이름에 따라 한 가지 유형의 개체의 모양과 느낌을 변경 하려면.</span><span class="sxs-lookup"><span data-stu-id="3e862-890">New templates can be added based on the name of the data object in order to change the look and feel of just one type of object.</span></span> <span data-ttu-id="3e862-891">예를 들어 다음 템플릿을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-891">For example, you can add the following template:</span></span>

[!code-console[Main](overview/samples/sample97.cmd)]

<span data-ttu-id="3e862-892">서식 파일에 다음 태그를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-892">The template might contain the following markup:</span></span>

[!code-aspx[Main](overview/samples/sample98.aspx)]

<span data-ttu-id="3e862-893">새 엔터티 템플릿을 새을 사용 하 여 페이지에 표시 됩니다 *DynamicEntity* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-893">The new entity templates are displayed on a page by using the new *DynamicEntity* control.</span></span> <span data-ttu-id="3e862-894">런타임 시이 컨트롤은 엔터티 템플릿의 내용으로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-894">At run time, this control is replaced with the contents of the entity template.</span></span> <span data-ttu-id="3e862-895">에서는 다음 태그를 *FormView* 에서 제어할는 `Detail.aspx` 엔터티 템플릿을 사용 하는 페이지 템플릿.</span><span class="sxs-lookup"><span data-stu-id="3e862-895">The following markup shows the *FormView* control in the `Detail.aspx` page template that uses the entity template.</span></span> <span data-ttu-id="3e862-896">알림 합니다 *DynamicEntity* 태그의 요소에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-896">Notice the *DynamicEntity* element in the markup.</span></span>

[!code-aspx[Main](overview/samples/sample99.aspx)]

<a id="0.2__Toc224729045"></a><a id="0.2__Toc253429282"></a><a id="0.2__Toc243304653"></a>

### <a name="new-field-templates-for-urls-and-email-addresses"></a><span data-ttu-id="3e862-897">Url 및 전자 메일 주소에 대 한 새 필드 템플릿</span><span class="sxs-lookup"><span data-stu-id="3e862-897">New Field Templates for URLs and Email Addresses</span></span>

<span data-ttu-id="3e862-898">ASP.NET 4에서는 두 가지 새로운 기본 제공 필드 템플릿 `EmailAddress.ascx` 고 `Url.ascx`입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-898">ASP.NET 4 introduces two new built-in field templates, `EmailAddress.ascx` and `Url.ascx`.</span></span> <span data-ttu-id="3e862-899">로 표시 된 필드에 대 한 이러한 템플릿을 사용 하 *EmailAddress* 또는 *Url* 사용 하 여 합니다 *DataType* 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-899">These templates are used for fields that are marked as *EmailAddress* or *Url* with the *DataType* attribute.</span></span> <span data-ttu-id="3e862-900">에 대 한 *EmailAddress* 개체를 사용 하 여 만든 하이퍼링크로 필드가 표시 되는 *mailto:* 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-900">For *EmailAddress* objects, the field is displayed as a hyperlink that is created by using the *mailto:* protocol.</span></span> <span data-ttu-id="3e862-901">사용자가 링크를 클릭 하는 경우 사용자의 전자 메일 클라이언트 열리고 기본 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-901">When users click the link, it opens the user's email client and creates a skeleton message.</span></span> <span data-ttu-id="3e862-902">로 형식화 된 개체가 *Url* 일반 하이퍼링크로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-902">Objects typed as *Url* are displayed as ordinary hyperlinks.</span></span>

<span data-ttu-id="3e862-903">다음 예에서는 필드는 표시 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-903">The following example shows how fields would be marked.</span></span>

[!code-csharp[Main](overview/samples/sample100.cs)]

<a id="0.2__Toc224729046"></a><a id="0.2__Toc253429283"></a><a id="0.2__Toc243304654"></a>

### <a name="creating-links-with-the-dynamichyperlink-control"></a><span data-ttu-id="3e862-904">DynamicHyperLink 컨트롤을 사용 하 여 링크 만들기</span><span class="sxs-lookup"><span data-stu-id="3e862-904">Creating Links with the DynamicHyperLink Control</span></span>

<span data-ttu-id="3e862-905">동적 데이터 웹 사이트에 액세스할 때 최종 사용자에 게 표시 되는 Url을 제어 하려면.NET Framework 3.5 SP1에 추가 된 새로운 라우팅 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-905">Dynamic Data uses the new routing feature that was added in the .NET Framework 3.5 SP1 to control the URLs that end users see when they access the Web site.</span></span> <span data-ttu-id="3e862-906">새 *DynamicHyperLink* 컨트롤을 사용 하면 쉽게 Dynamic Data 사이트의 페이지에 대 한 링크를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-906">The new *DynamicHyperLink* control makes it easy to build links to pages in a Dynamic Data site.</span></span> <span data-ttu-id="3e862-907">다음 예제에서는 사용 하는 방법을 보여 줍니다 합니다 *DynamicHyperLink* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-907">The following example shows how to use the *DynamicHyperLink* control:</span></span>

[!code-aspx[Main](overview/samples/sample101.aspx)]

<span data-ttu-id="3e862-908">이 태그에 대 한 목록 페이지를 가리키는 링크를 만듭니다는 `Products` 테이블에 정의 된 경로에 따라는 `Global.asax` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-908">This markup creates a link that points to the List page for the `Products` table based on routes that are defined in the `Global.asax` file.</span></span> <span data-ttu-id="3e862-909">컨트롤에는 자동으로 동적 데이터 페이지를 기반으로 하는 기본 테이블 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-909">The control automatically uses the default table name that the Dynamic Data page is based on.</span></span>

<a id="0.2__Toc224729047"></a><a id="0.2__Toc253429284"></a><a id="0.2__Toc243304655"></a>

### <a name="support-for-inheritance-in-the-data-model"></a><span data-ttu-id="3e862-910">데이터 모델의 상속에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="3e862-910">Support for Inheritance in the Data Model</span></span>

<span data-ttu-id="3e862-911">Entity Framework 및 LINQ to SQL 해당 데이터 모델에서 상속을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-911">Both the Entity Framework and LINQ to SQL support inheritance in their data models.</span></span> <span data-ttu-id="3e862-912">이 예가 포함 된 데이터베이스 수는 `InsurancePolicy` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-912">An example of this might be a database that has an `InsurancePolicy` table.</span></span> <span data-ttu-id="3e862-913">포함할 수도 있습니다 `CarPolicy` 하 고 `HousePolicy` 와 동일한 필드가 있는 테이블 `InsurancePolicy` 다음 더 많은 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-913">It might also contain `CarPolicy` and `HousePolicy` tables that have the same fields as `InsurancePolicy` and then add more fields.</span></span> <span data-ttu-id="3e862-914">동적 데이터 데이터 모델에서 상속 된 개체를 이해 하 고 상속된 된 테이블에 대 한 스 캐 폴딩을 지원 하도록 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-914">Dynamic Data has been modified to understand inherited objects in the data model and to support scaffolding for the inherited tables.</span></span>

<a id="0.2__Toc224729048"></a><a id="0.2__Toc253429285"></a><a id="0.2__Toc243304656"></a>

### <a name="support-for-many-to-many-relationships-entity-framework-only"></a><span data-ttu-id="3e862-915">다 대 다 관계 (Entity Framework에만 해당)에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="3e862-915">Support for Many-to-Many Relationships (Entity Framework Only)</span></span>

<span data-ttu-id="3e862-916">Entity Framework에서 컬렉션으로 관계를 노출 하 여 구현 되는 테이블 간에 다 대 다 관계에 대 한 다양 한 지원에는 *엔터티* 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-916">The Entity Framework has rich support for many-to-many relationships between tables, which is implemented by exposing the relationship as a collection on an *Entity* object.</span></span> <span data-ttu-id="3e862-917">새 `ManyToMany.ascx` 고 `ManyToMany_Edit.ascx` 필드 템플릿을 추가한 다 대 다 관계에 관련 된 데이터 표시 및 편집에 대 한 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-917">New `ManyToMany.ascx` and `ManyToMany_Edit.ascx` field templates have been added to provide support for displaying and editing data that is involved in many-to-many relationships.</span></span>

<a id="0.2__Toc224729049"></a><a id="0.2__Toc253429286"></a><a id="0.2__Toc243304657"></a>

### <a name="new-attributes-to-control-display-and-support-enumerations"></a><span data-ttu-id="3e862-918">컨트롤 표시 및 지원 열거형에 새 특성</span><span class="sxs-lookup"><span data-stu-id="3e862-918">New Attributes to Control Display and Support Enumerations</span></span>

<span data-ttu-id="3e862-919">합니다 *DisplayAttribute* 통해 추가 필드가 표시 되는 방식을 제어할 수에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-919">The *DisplayAttribute* has been added to give you additional control over how fields are displayed.</span></span> <span data-ttu-id="3e862-920">합니다 *DisplayName* 특성이 이전 버전의 동적 데이터 필드에 대 한 캡션으로 사용 되는 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-920">The *DisplayName* attribute in earlier versions of Dynamic Data allowed you to change the name that is used as a caption for a field.</span></span> <span data-ttu-id="3e862-921">새 *DisplayAttribute* 클래스 필드를 필터로 사용 되는 필드를 사용할지 여부 및 필드가 표시 되는 순서와 같은 표시 옵션을 추가로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-921">The new *DisplayAttribute* class lets you specify more options for displaying a field, such as the order in which a field is displayed and whether a field will be used as a filter.</span></span> <span data-ttu-id="3e862-922">제공 독립적으로 제어의 레이블 지정에 사용 되는 이름 특성을 *GridView* 컨트롤에 사용할 이름을 *DetailsView* 필드 도움말 텍스트를 제어 및 워터 마크에 사용 되는 필드 (필드는 텍스트 입력을 받아들이는) 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-922">The attribute also provides independent control of the name used for the labels in a *GridView* control, the name used in a *DetailsView* control, the help text for the field, and the watermark used for the field (if the field accepts text input).</span></span>

<span data-ttu-id="3e862-923">합니다 *EnumDataTypeAttribute* 열거형 필드를 매핑할 수 있도록 클래스가 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-923">The *EnumDataTypeAttribute* class has been added to let you map fields to enumerations.</span></span> <span data-ttu-id="3e862-924">필드에이 특성을 적용 하면 열거형 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-924">When you apply this attribute to a field, you specify an enumeration type.</span></span> <span data-ttu-id="3e862-925">동적 데이터를 사용 하 여 새 `Enumeration.ascx` 필드 템플릿을 표시 하 고 열거형 값을 편집에 대 한 UI를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-925">Dynamic Data uses the new `Enumeration.ascx` field template to create UI for displaying and editing enumeration values.</span></span> <span data-ttu-id="3e862-926">템플릿을은 열거형의 이름에는 데이터베이스에서 값을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-926">The template maps the values from the database to the names in the enumeration.</span></span>

<a id="0.2__Toc224729050"></a><a id="0.2__Toc253429287"></a><a id="0.2__Toc243304658"></a>

### <a name="enhanced-support-for-filters"></a><span data-ttu-id="3e862-927">필터에 대 한 향상 된 지원</span><span class="sxs-lookup"><span data-stu-id="3e862-927">Enhanced Support for Filters</span></span>

<span data-ttu-id="3e862-928">동적 데이터 1.0 부울 열과 외래 키 열에 대 한 기본 제공 필터를 사용 하 여 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-928">Dynamic Data 1.0 shipped with built-in filters for Boolean columns and foreign-key columns.</span></span> <span data-ttu-id="3e862-929">필터 여부를 표시 하기 또는 표시 된 순서에서 지정을 허용 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-929">The filters did not allow you to specify whether they were displayed or in what order they were displayed.</span></span> <span data-ttu-id="3e862-930">새 *DisplayAttribute* 특성 주소 둘 다 제공 하 여 이러한 문제의 열 필터로 표시 되는지 여부 제어 및 순서에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-930">The new *DisplayAttribute* attribute addresses both of these issues by giving you control over whether a column is displayed as a filter and in what order it will be displayed.</span></span>

<span data-ttu-id="3e862-931">추가 향상은 필터링 지원 되었는지 다시[새 쓸](#0.2__QueryExtender "_QueryExtender") Web Forms의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-931">An additional enhancement is that filtering support has been re[written to use the new](#0.2__QueryExtender "_QueryExtender") feature of Web Forms.</span></span> <span data-ttu-id="3e862-932">이 필터를 사용 하 여 사용할 데이터 소스 컨트롤에 대 한 지식이 필요 없이 필터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-932">This lets you create filters without requiring knowledge of the data source control that the filters will be used with.</span></span> <span data-ttu-id="3e862-933">이러한 확장과 함께 필터도이 켜진 템플릿 컨트롤에 새 템플릿을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-933">Along with these extensions, filters have also been turned into template controls, which allows you to add new ones.</span></span> <span data-ttu-id="3e862-934">마지막으로, 합니다 *DisplayAttribute* 앞에서 언급 한 클래스를 통해 동일한 재정의 되도록 기본 필터 방식으로 *UIHint* 를 재정의할 수 열에 대 한 기본 필드 템플릿을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-934">Finally, the *DisplayAttribute* class mentioned earlier allows the default filter to be overridden, in the same way that *UIHint* allows the default field template for a column to be overridden.</span></span>

<a id="0.2__Toc224729051"></a><a id="0.2__Toc253429288"></a><a id="0.2__Toc243304659"></a>

## <a name="visual-studio-2010-web-development-improvements"></a><span data-ttu-id="3e862-935">Visual Studio 2010 웹 개발 향상</span><span class="sxs-lookup"><span data-stu-id="3e862-935">Visual Studio 2010 Web Development Improvements</span></span>

<span data-ttu-id="3e862-936">Visual Studio 2010의 웹 개발 큰 CSS 호환성을 위해 HTML 및 ASP.NET 태그 조각 및 새 동적 IntelliSense JavaScript를 통해 향상 된 생산성 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-936">Web development in Visual Studio 2010 has been enhanced for greater CSS compatibility, increased productivity through HTML and ASP.NET markup snippets and new dynamic IntelliSense JavaScript.</span></span>

<a id="0.2__Toc224729052"></a><a id="0.2__Toc253429289"></a><a id="0.2__Toc243304660"></a>

### <a name="improved-css-compatibility"></a><span data-ttu-id="3e862-937">향상 된 CSS 호환성</span><span class="sxs-lookup"><span data-stu-id="3e862-937">Improved CSS Compatibility</span></span>

<span data-ttu-id="3e862-938">Visual Studio 2010의 Visual Web Developer 디자이너를 사용 하는 CSS 2.1 표준 준수를 개선 하기 위해 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-938">The Visual Web Developer designer in Visual Studio 2010 has been updated to improve CSS 2.1 standards compliance.</span></span> <span data-ttu-id="3e862-939">더 잘 디자이너 HTML 소스의 무결성을 유지 하 고 이전 버전의 Visual Studio 보다 더 강력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-939">The designer better preserves integrity of the HTML source and is more robust than in previous versions of Visual Studio.</span></span> <span data-ttu-id="3e862-940">내부적으로 아키텍처도 향상 되었습니다 렌더링, 레이아웃 및 효율성의 이후 향상 기능을 향상 하도록 해당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-940">Under the hood, architectural improvements have also been made that will better enable future enhancements in rendering, layout, and serviceability.</span></span>

<a id="0.2__Toc224729053"></a><a id="0.2__Toc253429290"></a><a id="0.2__Toc243304661"></a>

### <a name="html-and-javascript-snippets"></a><span data-ttu-id="3e862-941">HTML 및 JavaScript 코드 조각</span><span class="sxs-lookup"><span data-stu-id="3e862-941">HTML and JavaScript Snippets</span></span>

<span data-ttu-id="3e862-942">HTML 편집기에서 IntelliSense 자동 완성 태그 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-942">In the HTML editor, IntelliSense auto-completes tag names.</span></span> <span data-ttu-id="3e862-943">IntelliSense 코드 조각 기능을 자동으로 완성 전체 태그 등입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-943">The IntelliSense Snippets feature auto-completes entire tags and more.</span></span> <span data-ttu-id="3e862-944">Visual Studio 2010과 함께 C# 및 Visual Basic, Visual Studio의 이전 버전에서 지원 되므로 JavaScript 용 IntelliSense 코드 조각 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-944">In Visual Studio 2010, IntelliSense snippets are supported for JavaScript, alongside C# and Visual Basic, which were supported in earlier versions of Visual Studio.</span></span>

<span data-ttu-id="3e862-945">Visual Studio 2010에는 자동 완성 일반적인 ASP.NET 및 HTML 태그를 필수 특성을 포함 하 여 도움이 되는 200 개 이상의 조각이 포함 되어 있습니다. (같은 runat = "server") 및 태그에 특정 공통 특성 (같은 *ID*,  *DataSourceID*하십시오 *ControlToValidate*, 및 *텍스트*).</span><span class="sxs-lookup"><span data-stu-id="3e862-945">Visual Studio 2010 includes over 200 snippets that help you auto-complete common ASP.NET and HTML tags, including required attributes (such as runat="server") and common attributes specific to a tag (such as *ID*, *DataSourceID*, *ControlToValidate*, and *Text*).</span></span>

<span data-ttu-id="3e862-946">추가 코드 조각을 다운로드 하거나 일반적인 작업에 대 한 사용자 또는 팀을 사용 하는 태그의 요소를 캡슐화 하는 사용자 고유의 코드 조각을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-946">You can download additional snippets, or you can write your own snippets that encapsulate the blocks of markup that you or your team use for common tasks.</span></span>

<a id="0.2__Toc224729054"></a><a id="0.2__Toc253429291"></a><a id="0.2__Toc243304662"></a>

### <a name="javascript-intellisense-enhancements"></a><span data-ttu-id="3e862-947">JavaScript IntelliSense 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="3e862-947">JavaScript IntelliSense Enhancements</span></span>

<span data-ttu-id="3e862-948">Visual 2010에서는 JavaScript IntelliSense는 풍부한 편집 환경을 제공 하기 위해 다시 디자인 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-948">In Visual 2010, JavaScript IntelliSense has been redesigned to provide an even richer editing experience.</span></span> <span data-ttu-id="3e862-949">IntelliSense는 이제 동적으로 생성 된 메서드에서 같은 개체 인식 *registerNamespace* 및 다른 JavaScript 프레임 워크에서 사용 하는 비슷한 기술을 통해.</span><span class="sxs-lookup"><span data-stu-id="3e862-949">IntelliSense now recognizes objects that have been dynamically generated by methods such as *registerNamespace* and by similar techniques used by other JavaScript frameworks.</span></span> <span data-ttu-id="3e862-950">스크립트의 대규모 라이브러리를 분석 하 고 IntelliSense를 거의 또는 전혀 처리 지연 표시 성능이 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-950">Performance has been improved to analyze large libraries of script and to display IntelliSense with little or no processing delay.</span></span> <span data-ttu-id="3e862-951">거의 모든 타사 라이브러리를 지원 하 고 다양 한 코딩 스타일을 지원 하도록 호환성 크게 증가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-951">Compatibility has been dramatically increased to support nearly all third-party libraries and to support diverse coding styles.</span></span> <span data-ttu-id="3e862-952">문서 주석은 입력 하 고 IntelliSense에서 즉시 활용은 이제 구문 분석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-952">Documentation comments are now parsed as you type and are immediately leveraged by IntelliSense.</span></span>

<a id="0.2__Toc224729055"></a><a id="0.2__Toc253429292"></a><a id="0.2__Toc243304663"></a>

## <a name="web-application-deployment-with-visual-studio-2010"></a><span data-ttu-id="3e862-953">Visual Studio 2010을 사용한 웹 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="3e862-953">Web Application Deployment with Visual Studio 2010</span></span>

<span data-ttu-id="3e862-954">ASP.NET 개발자는 웹 응용 프로그램을 배포 하는 경우 종종 어려워하는 다음과 같은 문제가 발생 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-954">When ASP.NET developers deploy a Web application, they often find that they encounter issues such as the following:</span></span>

- <span data-ttu-id="3e862-955">공유 호스팅 사이트 배포 속도가 느려질 수 있습니다는 FTP와 같은 기술 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-955">Deploying to a shared hosting site requires technologies such as FTP, which can be slow.</span></span> <span data-ttu-id="3e862-956">또한 수동으로 데이터베이스를 구성 하는 SQL 스크립트 실행과 같은 작업을 수행 해야 하 고 응용 프로그램으로 가상 디렉터리 폴더를 구성 하는 등의 IIS 설정을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-956">In addition, you must manually perform tasks such as running SQL scripts to configure a database and you must change IIS settings, such as configuring a virtual directory folder as an application.</span></span>
- <span data-ttu-id="3e862-957">엔터프라이즈 환경에서 웹 응용 프로그램 파일을 배포 하는 것 외에도 관리자 자주 수정 해야 ASP.NET 구성 파일과 IIS 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-957">In an enterprise environment, in addition to deploying the Web application files, administrators frequently must modify ASP.NET configuration files and IIS settings.</span></span> <span data-ttu-id="3e862-958">데이터베이스 관리자는 일련의 실행 중인 응용 프로그램 데이터베이스를 가져오려면 SQL 스크립트를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-958">Database administrators must run a series of SQL scripts to get the application database running.</span></span> <span data-ttu-id="3e862-959">이러한 설치는 많은 수동 작업, 완료 하는 데 시간이 걸릴 신중 하 게 문서화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-959">Such installations are labor intensive, often take hours to complete, and must be carefully documented.</span></span>

<span data-ttu-id="3e862-960">Visual Studio 2010에는 이러한 문제를 해결 하 고 웹 응용 프로그램에 원활 하 게 배포할 수 있는 기술이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-960">Visual Studio 2010 includes technologies that address these issues and that let you seamlessly deploy Web applications.</span></span> <span data-ttu-id="3e862-961">이러한 기술 중 하나에서 IIS 웹 배포 도구 (MsDeploy.exe)입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-961">One of these technologies is the IIS Web Deployment Tool (MsDeploy.exe).</span></span>

<span data-ttu-id="3e862-962">Visual Studio 2010의 웹 배포 기능에는 다음 주요 영역이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-962">Web deployment features in Visual Studio 2010 include the following major areas:</span></span>

- <span data-ttu-id="3e862-963">웹 패키징</span><span class="sxs-lookup"><span data-stu-id="3e862-963">Web packaging</span></span>
- <span data-ttu-id="3e862-964">Web.config 변환</span><span class="sxs-lookup"><span data-stu-id="3e862-964">Web.config transformation</span></span>
- <span data-ttu-id="3e862-965">데이터베이스 배포</span><span class="sxs-lookup"><span data-stu-id="3e862-965">Database deployment</span></span>
- <span data-ttu-id="3e862-966">웹 응용 프로그램에 대 한 one-click 게시</span><span class="sxs-lookup"><span data-stu-id="3e862-966">One-click publish for Web applications</span></span>

<span data-ttu-id="3e862-967">다음 섹션에서는 이러한 기능에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-967">The following sections provide details about these features.</span></span>

<a id="0.2__Toc224729056"></a><a id="0.2__Toc253429293"></a><a id="0.2__Toc243304664"></a>

### <a name="web-packaging"></a><span data-ttu-id="3e862-968">웹 패키징</span><span class="sxs-lookup"><span data-stu-id="3e862-968">Web Packaging</span></span>

<span data-ttu-id="3e862-969">Visual Studio 2010 MSDeploy 도구를 사용 하 여 응용 프로그램 이라고 하는 압축된 (.zip) 파일을 만들 하는 *웹 패키지*합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-969">Visual Studio 2010 uses the MSDeploy tool to create a compressed (.zip) file for your application, which is referred to as a *Web package*.</span></span> <span data-ttu-id="3e862-970">다음 콘텐츠 및 응용 프로그램에 대 한 메타 데이터를 포함 하는 패키지 파일:</span><span class="sxs-lookup"><span data-stu-id="3e862-970">The package file contains metadata about your application plus the following content:</span></span>

- <span data-ttu-id="3e862-971">응용 프로그램 풀 설정, 오류 페이지 설정 및 등을 포함 하는 IIS 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-971">IIS settings, which includes application pool settings, error page settings, and so on.</span></span>
- <span data-ttu-id="3e862-972">실제 웹 콘텐츠를 웹 페이지, 사용자 컨트롤, 정적 콘텐츠 (이미지 및 HTML 파일) 및 등을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-972">The actual Web content, which includes Web pages, user controls, static content (images and HTML files), and so on.</span></span>
- <span data-ttu-id="3e862-973">SQL Server 데이터베이스 스키마 및 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-973">SQL Server database schemas and data.</span></span>
- <span data-ttu-id="3e862-974">보안 인증서, GAC, 레지스트리 설정에서 설치할 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-974">Security certificates, components to install in the GAC, registry settings, and so on.</span></span>

<span data-ttu-id="3e862-975">웹 패키지를 서버에 복사 하 고 IIS 관리자를 사용 하 여 수동으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-975">A Web package can be copied to any server and then installed manually by using IIS Manager.</span></span> <span data-ttu-id="3e862-976">또는, 자동화 된 배포 패키지 또는 설치할 수 있습니다 명령줄 명령을 사용 하 여 배포 Api를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-976">Alternatively, for automated deployment, the package can be installed by using command-line commands or by using deployment APIs.</span></span>

<span data-ttu-id="3e862-977">MSBuild 작업 및 대상 웹 패키지를 만드는 기본 제공 visual Studio 2010 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-977">Visual Studio 2010 provides built in MSBuild tasks and targets to create Web packages.</span></span> <span data-ttu-id="3e862-978">자세한 내용은 [ASP.NET 웹 응용 프로그램 프로젝트 배포 개요](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx) MSDN 웹 사이트에서 및 [웹 패키지를 만들어야 하는 10 + 20 이유](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html) 인 Vishal Joshi의 블로그입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-978">For more information, see [ASP.NET Web Application Project Deployment Overview](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx) on the MSDN Web site and [10 + 20 reasons why you should create a Web Package](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729057"></a><a id="0.2__Toc253429294"></a><a id="0.2__Toc243304665"></a>

### <a name="webconfig-transformation"></a><span data-ttu-id="3e862-979">Web.config 변환</span><span class="sxs-lookup"><span data-stu-id="3e862-979">Web.config Transformation</span></span>

<span data-ttu-id="3e862-980">Visual Studio 2010 웹 응용 프로그램 배포에 대 한 소개 [문서 변환 XDT (XML)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)을 변형할 수 있는 기능인는 `Web.config` 개발 설정에서 파일을 프로덕션 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-980">For Web application deployment, Visual Studio 2010 introduces [XML Document Transform (XDT)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html), which is a feature that lets you transform a `Web.config` file from development settings to production settings.</span></span> <span data-ttu-id="3e862-981">변환 설정 이라는 변환 파일에 지정 된 `web.debug.config`, `web.release.config`등입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-981">Transformation settings are specified in transform files named `web.debug.config`, `web.release.config`, and so on.</span></span> <span data-ttu-id="3e862-982">(이러한 파일의 이름은 MSBuild 구성와 일치 합니다.) 변환 파일을 포함 하는 배포 해야 하는 변경 내용만 `Web.config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-982">(The names of these files match MSBuild configurations.) A transform file includes just the changes that you need to make to a deployed `Web.config` file.</span></span> <span data-ttu-id="3e862-983">간단한 구문을 사용 하 여 변경 내용을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-983">You specify the changes by using simple syntax.</span></span>

<span data-ttu-id="3e862-984">다음 예제에서는 부분을 `web.release.config` 릴리스 구성의 배포에 대 한 생성 될 수 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-984">The following example shows a portion of a `web.release.config` file that might be produced for deployment of your release configuration.</span></span> <span data-ttu-id="3e862-985">예제의 대체 키워드를 배포 하는 동안 지정 합니다 *connectionString* 에서 노드를 `Web.config` 파일 예제에 나와 있는 값으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-985">The Replace keyword in the example specifies that during deployment the *connectionString* node in the `Web.config` file will be replaced with the values that are listed in the example.</span></span>

[!code-xml[Main](overview/samples/sample102.xml)]

<span data-ttu-id="3e862-986">자세한 내용은 [웹 응용 프로그램 프로젝트 배포를 위한 Web.config 변환 구문](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx) msdn <a id="0.2_a"> </a> 웹 사이트 및[웹 배포: Web.Config 변환](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)인 Vishal Joshi의 블로그입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-986">For more information, see [Web.config Transformation Syntax for Web Application Project Deployment](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx) on the MSDN <a id="0.2_a"></a> Web site and[Web Deployment: Web.Config Transformation](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729058"></a><a id="0.2__Toc253429295"></a><a id="0.2__Toc243304666"></a>

### <a name="database-deployment"></a><span data-ttu-id="3e862-987">데이터베이스 배포</span><span class="sxs-lookup"><span data-stu-id="3e862-987">Database Deployment</span></span>

<span data-ttu-id="3e862-988">Visual Studio 2010 배포 패키지를 SQL Server 데이터베이스에 대 한 종속성을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-988">A Visual Studio 2010 deployment package can include dependencies on SQL Server databases.</span></span> <span data-ttu-id="3e862-989">패키지 정의의 일부로 원본 데이터베이스에 대 한 연결 문자열을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-989">As part of the package definition, you provide the connection string for your source database.</span></span> <span data-ttu-id="3e862-990">웹 패키지를 만들면 Visual Studio 2010 및 필요에 따라 데이터를 데이터베이스 스키마에 대 한 SQL 스크립트를 만들고 패키지에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-990">When you create the Web package, Visual Studio 2010 creates SQL scripts for the database schema and optionally for the data, and then adds these to the package.</span></span> <span data-ttu-id="3e862-991">또한 사용자 지정 SQL 스크립트를 제공 하 고 서버에서 실행 되도록 순서를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-991">You can also provide custom SQL scripts and specify the sequence in which they should run on the server.</span></span> <span data-ttu-id="3e862-992">대상 서버에 적절 한 연결 문자열을 제공 하면 배포 시에 배포 프로세스는 다음 데이터베이스 스키마를 만들고 데이터를 추가 하는 스크립트를 실행 하려면이 연결 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-992">At deployment time, you provide a connection string that is appropriate for the target server; the deployment process then uses this connection string to run the scripts that create the database schema and add the data.</span></span>

<span data-ttu-id="3e862-993">또한 한 번의 클릭을 사용 하 여 게시, 배포 응용 프로그램 원격 공유 호스팅 사이트에 게시 되 면 데이터베이스를 직접 게시를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-993">In addition, by using one-click publish, you can configure deployment to publish your database directly when the application is published to a remote shared hosting site.</span></span> <span data-ttu-id="3e862-994">자세한 내용은 참조 하세요. [방법:는 데이터베이스 프로젝트를 통해 웹 응용 프로그램을 배포](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx) MSDN 웹 사이트 및 [VS 2010을 사용 하 여 데이터베이스 배포](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) 인 Vishal Joshi의 블로그입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-994">For more information, see [How to: Deploy a Database With a Web Application Project](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx) on the MSDN Web site and [Database Deployment with VS 2010](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729059"></a><a id="0.2__Toc253429296"></a><a id="0.2__Toc243304667"></a>

### <a name="one-click-publish-for-web-applications"></a><span data-ttu-id="3e862-995">웹 응용 프로그램에 대 한 One-click 게시</span><span class="sxs-lookup"><span data-stu-id="3e862-995">One-Click Publish for Web Applications</span></span>

<span data-ttu-id="3e862-996">Visual Studio 2010에서는 IIS 원격 관리 서비스를 사용 하 여 원격 서버에 웹 응용 프로그램을 게시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-996">Visual Studio 2010 also lets you use the IIS remote management service to publish a Web application to a remote server.</span></span> <span data-ttu-id="3e862-997">호스팅 계정 또는 서버를 테스트 하거나 스테이징 서버에 대 한 게시 프로필을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-997">You can create a publish profile for your hosting account or for testing servers or staging servers.</span></span> <span data-ttu-id="3e862-998">각 프로필은 적절 한 자격 증명을 안전 하 게 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-998">Each profile can save appropriate credentials securely.</span></span> <span data-ttu-id="3e862-999">대상에 배포할 수 있습니다 웹 한 번의 클릭을 사용 하 여 한 번의 클릭을 사용 하 여 서버 도구 모음을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-999">You can then deploy to any of the target servers with one click by using the Web one-click publish toolbar.</span></span> <span data-ttu-id="3e862-1000">Visual Studio 2010을 사용 하 여 MSBuild 명령줄을 사용 하 여 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-1000">With Visual Studio 2010, you can also publish by using the MSBuild command line.</span></span> <span data-ttu-id="3e862-1001">이렇게 하면 연속 통합 모델의 게시를 포함 하도록 팀 빌드 환경을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-1001">This lets you configure your team build environment to include publishing in a continuous-integration model.</span></span>

<span data-ttu-id="3e862-1002">자세한 내용은 참조 하세요. [방법: 웹 응용 프로그램 프로젝트를 사용 하 여 One-click 게시 및 웹 배포 배포](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx) MSDN 웹 사이트 및 [VS 2010을 사용 하 여 원클릭 게시 웹](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html) 인 Vishal Joshi의 블로그입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-1002">For more information, see [How to: Deploy a Web Application Project Using One-Click Publish and Web Deploy](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx) on the MSDN Web site and [Web 1-Click Publish with VS 2010](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html) on Vishal Joshi's blog.</span></span> <span data-ttu-id="3e862-1003">Visual Studio 2010에서 웹 응용 프로그램 배포에 대 한 비디오 프레젠테이션을 보려면을 참조 하세요 [웹 개발자 미리 보기에 대 한 VS 2010](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html) 인 Vishal Joshi의 블로그입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-1003">To view video presentations about Web application deployment in Visual Studio 2010, see [VS 2010 for Web Developer Previews](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729060"></a><a id="0.2__Toc253429297"></a><a id="0.2__Toc243304668"></a>

### <a name="resources"></a><span data-ttu-id="3e862-1004">자료</span><span class="sxs-lookup"><span data-stu-id="3e862-1004">Resources</span></span>

<span data-ttu-id="3e862-1005">다음 웹 사이트는 ASP.NET 4 및 Visual Studio 2010에 대 한 추가 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-1005">The following Web sites provide additional information about ASP.NET 4 and Visual Studio 2010.</span></span>

- <span data-ttu-id="3e862-1006">[ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) -MSDN 웹 사이트에서 ASP.NET 4에 대 한 공식 설명서.</span><span class="sxs-lookup"><span data-stu-id="3e862-1006">[ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) — The official documentation for ASP.NET 4 on the MSDN Web site.</span></span>
- <span data-ttu-id="3e862-1007">[https://www.asp.net/](https://www.asp.net/) -ASP.NET 팀의 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-1007">[https://www.asp.net/](https://www.asp.net/) — The ASP.NET team's own Web site.</span></span>
- <span data-ttu-id="3e862-1008">[https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx) 및 [ASP.NET 동적 데이터 콘텐츠 맵](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx) -ASP.NET 팀 사이트에 ASP.NET Dynamic Data에 대 한 공식 설명서의 온라인 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-1008">[https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx) and [ASP.NET Dynamic Data Content Map](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx) — Online resources on the ASP.NET team site and in the official documentation for ASP.NET Dynamic Data.</span></span>
- <span data-ttu-id="3e862-1009">[https://www.asp.net/ajax/](../../ajax/index.md) ASP.NET Ajax 개발을 위한-주 웹 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-1009">[https://www.asp.net/ajax/](../../ajax/index.md) — The main Web resource for ASP.NET Ajax development.</span></span>
- <span data-ttu-id="3e862-1010">[https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/) Visual Studio 2010의 기능에 대 한 정보를 포함 하는-Visual Web Developer 팀 블로그입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-1010">[https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/) — The Visual Web Developer Team blog, which includes information about features in Visual Studio 2010.</span></span>
- <span data-ttu-id="3e862-1011">[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) -미리 보기 버전의 ASP.NET에 대 한 기본 웹 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-1011">[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) — The main Web resource for preview releases of ASP.NET.</span></span>

<a id="0.2__Toc224729061"></a><a id="0.2__Toc253429298"></a><a id="0.2__Toc243304669"></a>

## <a name="disclaimer"></a><span data-ttu-id="3e862-1012">고지 사항</span><span class="sxs-lookup"><span data-stu-id="3e862-1012">Disclaimer</span></span>

<span data-ttu-id="3e862-1013">본 문서는 예비 문서이며, 여기에 설명한 소프트웨어의 최종 상업적 출시 전에 크게 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-1013">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="3e862-1014">이 문서에 포함된 정보는 게시 날짜 현재 논의된 문제에 대한 Microsoft Corporation의 당시 관점을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-1014">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="3e862-1015">Microsoft는 변화하는 시장 상황에 부응해야 하므로, Microsoft의 일부에 대한 책임으로 해석되어서는 안되며, 게시 날짜 이후 소개된 정보의 정확성을 Microsoft가 보증할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-1015">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="3e862-1016">이 백서는 정보 제공만을 목적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-1016">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="3e862-1017">Microsoft는 이 문서에 있는 정보에 대한 명시적 또는 묵시적, 법적인 보증을 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-1017">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="3e862-1018">해당 저작권법을 준수하는 것은 사용자의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-1018">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="3e862-1019">저작권에서의 권리와는 별도로, 이 설명서의 어떠한 부분도 Microsoft의 명시적인 서면 승인 없이는 어떠한 형식이나 수단(전기적, 기계적, 복사기에 의한 복사, 디스크 복사 또는 다른 방법) 또는 목적으로도 복제되거나, 검색 시스템에 저장 또는 도입되거나, 전송될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-1019">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="3e862-1020">Microsoft가 이 설명서 본안에 관련된 특허권, 상표권, 저작권 또는 기타 지적 재산권 등을 보유할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-1020">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="3e862-1021">서면 사용권 계약에 따라 Microsoft로부터 귀하에게 명시적으로 제공된 권리 이외에, 이 문서의 제공은 귀하에게 이러한 특허권, 상표권, 저작권, 또는 기타 지적 소유권 등에 대한 어떠한 사용권도 허여하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-1021">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="3e862-1022">다른 언급이 없는 경우 예제 회사, 조직, 제품, 도메인 이름, 전자 메일 주소, 로고, 사람, 장소 및 이벤트 용례은 실제 데이터가 아닙니다 및 실제 회사, 조직, 제품, 도메인 이름, 전자 메일 연관 시킬 의도가 없으며 주소, 로고, 사람, 장소 또는 이벤트는 또는 유추 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-1022">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="3e862-1023">© 2009 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="3e862-1023">© 2009 Microsoft Corporation.</span></span> <span data-ttu-id="3e862-1024">All rights reserved.</span><span class="sxs-lookup"><span data-stu-id="3e862-1024">All rights reserved.</span></span>

<span data-ttu-id="3e862-1025">Microsoft 및 Windows는 미국 및/또는 기타 국가에서 Microsoft Corporation의 상표이거나 등록된 상표입니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-1025">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="3e862-1026">여기에 언급된 실제 회사와 제품의 이름은 각각 해당 소유자의 상표일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e862-1026">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>
