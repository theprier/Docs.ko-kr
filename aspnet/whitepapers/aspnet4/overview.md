---
uid: whitepapers/aspnet4/overview
title: ASP.NET 4 및 Visual Studio 2010 웹 개발 개요 | Microsoft Docs
author: rick-anderson
description: 이 문서에서는.net Framework 4 및 Visual Studio 2010에 포함 된 ASP.NET에 대 한 다양 한 새로운 기능에 대 한 개요를 제공 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2010
ms.topic: article
ms.assetid: d7729af4-1eda-4ff2-8b61-dbbe4fc11d10
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /whitepapers/aspnet4
msc.type: content
ms.openlocfilehash: 6ce52c387ff835eda46bc1882b8b974889e2d4af
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
---
<a name="aspnet-4-and-visual-studio-2010-web-development-overview"></a><span data-ttu-id="819ca-103">ASP.NET 4 및 Visual Studio 2010 웹 개발 개요</span><span class="sxs-lookup"><span data-stu-id="819ca-103">ASP.NET 4 and Visual Studio 2010 Web Development Overview</span></span>
====================
> <span data-ttu-id="819ca-104">이 문서에서는.net Framework 4 및 Visual Studio 2010에 포함 된 ASP.NET에 대 한 다양 한 새로운 기능에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-104">This document provides an overview of many of the new features for ASP.NET that are included in the.NET Framework 4 and in Visual Studio 2010.</span></span>
> 
> [<span data-ttu-id="819ca-105">이 백서를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-105">Download This Whitepaper</span></span>](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_and_Visual_Studio_2010_Web_Development_Overview.pdf)


<span data-ttu-id="819ca-106">**목차**</span><span class="sxs-lookup"><span data-stu-id="819ca-106">**Contents**</span></span>

<span data-ttu-id="819ca-107">**[Core Services](#0.2__Toc253429238 "_Toc253429238")**</span><span class="sxs-lookup"><span data-stu-id="819ca-107">**[Core Services](#0.2__Toc253429238 "_Toc253429238")**</span></span>  
[<span data-ttu-id="819ca-108">Web.config 파일 리팩터링</span><span class="sxs-lookup"><span data-stu-id="819ca-108">Web.config File Refactoring</span></span>](#0.2__Toc253429239 "_Toc253429239")  
[<span data-ttu-id="819ca-109">확장 가능한 출력 캐싱</span><span class="sxs-lookup"><span data-stu-id="819ca-109">Extensible Output Caching</span></span>](#0.2__Toc253429240 "_Toc253429240")  
[<span data-ttu-id="819ca-110">웹 응용 프로그램 자동 시작</span><span class="sxs-lookup"><span data-stu-id="819ca-110">Auto-Start Web Applications</span></span>](#0.2__Toc253429241 "_Toc253429241")  
[<span data-ttu-id="819ca-111">페이지를 영구적으로 리디렉션</span><span class="sxs-lookup"><span data-stu-id="819ca-111">Permanently Redirecting a Page</span></span>](#0.2__Toc253429242 "_Toc253429242")  
[<span data-ttu-id="819ca-112">세션 상태 축소</span><span class="sxs-lookup"><span data-stu-id="819ca-112">Shrinking Session State</span></span>](#0.2__Toc253429243 "_Toc253429243")  
[<span data-ttu-id="819ca-113">허용 가능한 Url의 범위</span><span class="sxs-lookup"><span data-stu-id="819ca-113">Expanding the Range of Allowable URLs</span></span>](#0.2__Toc253429244 "_Toc253429244")  
[<span data-ttu-id="819ca-114">확장 가능한 요청 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="819ca-114">Extensible Request Validation</span></span>](#0.2__Toc253429245 "_Toc253429245")  
[<span data-ttu-id="819ca-115">개체 캐싱 및 캐싱 확장성 개체</span><span class="sxs-lookup"><span data-stu-id="819ca-115">Object Caching and Object Caching Extensibility</span></span>](#0.2__Toc253429246 "_Toc253429246")  
[<span data-ttu-id="819ca-116">확장 가능한 HTML, URL 및 HTTP 헤더 인코딩을</span><span class="sxs-lookup"><span data-stu-id="819ca-116">Extensible HTML, URL, and HTTP Header Encoding</span></span>](#0.2__Toc253429247 "_Toc253429247")  
[<span data-ttu-id="819ca-117">단일 작업자 프로세스에서 개별 응용 프로그램에 대 한 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="819ca-117">Performance Monitoring for Individual Applications in a Single Worker Process</span></span>](#0.2__Toc253429248 "_Toc253429248")  
[<span data-ttu-id="819ca-118">멀티 타기 팅</span><span class="sxs-lookup"><span data-stu-id="819ca-118">Multi-Targeting</span></span>](#0.2__Toc253429249 "_Toc253429249")

<span data-ttu-id="819ca-119">**[Ajax](#0.2__Toc253429250 "_Toc253429250")**</span><span class="sxs-lookup"><span data-stu-id="819ca-119">**[Ajax](#0.2__Toc253429250 "_Toc253429250")**</span></span>  
[<span data-ttu-id="819ca-120">Web Forms 및 MVC에 포함 된 jQuery</span><span class="sxs-lookup"><span data-stu-id="819ca-120">jQuery Included with Web Forms and MVC</span></span>](#0.2__Toc253429251 "_Toc253429251")  
[<span data-ttu-id="819ca-121">콘텐츠 배달 네트워크 지원</span><span class="sxs-lookup"><span data-stu-id="819ca-121">Content Delivery Network Support</span></span>](#0.2__Toc253429252 "_Toc253429252")  
[<span data-ttu-id="819ca-122">ScriptManager 명시적 스크립트</span><span class="sxs-lookup"><span data-stu-id="819ca-122">ScriptManager Explicit Scripts</span></span>](#0.2__Toc253429253 "_Toc253429253")

<span data-ttu-id="819ca-123">**[Web Forms](#0.2__Toc253429256 "_Toc253429256")**</span><span class="sxs-lookup"><span data-stu-id="819ca-123">**[Web Forms](#0.2__Toc253429256 "_Toc253429256")**</span></span>  
[<span data-ttu-id="819ca-124">설정 된 Page.MetaKeywords 및 Page.MetaDescription 속성 메타 태그</span><span class="sxs-lookup"><span data-stu-id="819ca-124">Setting Meta Tags with the Page.MetaKeywords and Page.MetaDescription Properties</span></span>](#0.2__Toc253429257 "_Toc253429257")  
[<span data-ttu-id="819ca-125">개별 컨트롤의 뷰 상태 사용</span><span class="sxs-lookup"><span data-stu-id="819ca-125">Enabling View State for Individual Controls</span></span>](#0.2__Toc253429258 "_Toc253429258")  
[<span data-ttu-id="819ca-126">브라우저 기능으로 변경</span><span class="sxs-lookup"><span data-stu-id="819ca-126">Changes to Browser Capabilities</span></span>](#0.2__Toc253429259 "_Toc253429259")  
[<span data-ttu-id="819ca-127">ASP.NET 4에서에서의 라우팅</span><span class="sxs-lookup"><span data-stu-id="819ca-127">Routing in ASP.NET 4</span></span>](#0.2__Toc253429260 "_Toc253429260")  
[<span data-ttu-id="819ca-128">클라이언트 Id 설정</span><span class="sxs-lookup"><span data-stu-id="819ca-128">Setting Client IDs</span></span>](#0.2__Toc253429261 "_Toc253429261")  
[<span data-ttu-id="819ca-129">데이터 컨트롤에서 행 선택 보관</span><span class="sxs-lookup"><span data-stu-id="819ca-129">Persisting Row Selection in Data Controls</span></span>](#0.2__Toc253429262 "_Toc253429262")  
[<span data-ttu-id="819ca-130">ASP.NET Chart Control</span><span class="sxs-lookup"><span data-stu-id="819ca-130">ASP.NET Chart Control</span></span>](#0.2__Toc253429263 "_Toc253429263")  
[<span data-ttu-id="819ca-131">QueryExtender 제어를 사용 하 여 데이터를 필터링</span><span class="sxs-lookup"><span data-stu-id="819ca-131">Filtering Data with the QueryExtender Control</span></span>](#0.2__Toc253429264 "_Toc253429264")  
[<span data-ttu-id="819ca-132">Html 인코딩된 코드 식을</span><span class="sxs-lookup"><span data-stu-id="819ca-132">Html Encoded Code Expressions</span></span>](#0.2__Toc253429265 "_Toc253429265")  
[<span data-ttu-id="819ca-133">프로젝트 템플릿 변경</span><span class="sxs-lookup"><span data-stu-id="819ca-133">Project Template Changes</span></span>](#0.2__Toc253429266 "_Toc253429266")  
[<span data-ttu-id="819ca-134">CSS 개선</span><span class="sxs-lookup"><span data-stu-id="819ca-134">CSS Improvements</span></span>](#0.2__Toc253429267 "_Toc253429267")  
[<span data-ttu-id="819ca-135">Div 숨겨진 필드 주위 요소 숨기기</span><span class="sxs-lookup"><span data-stu-id="819ca-135">Hiding div Elements Around Hidden Fields</span></span>](#0.2__Toc253429268 "_Toc253429268")  
[<span data-ttu-id="819ca-136">템플릿 기반 컨트롤에 대 한 외부 테이블을 렌더링</span><span class="sxs-lookup"><span data-stu-id="819ca-136">Rendering an Outer Table for Templated Controls</span></span>](#0.2__Toc253429269 "_Toc253429269")  
[<span data-ttu-id="819ca-137">ListView 컨트롤의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="819ca-137">ListView Control Enhancements</span></span>](#0.2__Toc253429270 "_Toc253429270")  
[<span data-ttu-id="819ca-138">CheckBoxList 및 RadioButtonList 컨트롤 향상</span><span class="sxs-lookup"><span data-stu-id="819ca-138">CheckBoxList and RadioButtonList Control Enhancements</span></span>](#0.2__Toc253429271 "_Toc253429271")  
[<span data-ttu-id="819ca-139">메뉴 컨트롤 개선</span><span class="sxs-lookup"><span data-stu-id="819ca-139">Menu Control Improvements</span></span>](#0.2__Toc253429272 "_Toc253429272")  
[<span data-ttu-id="819ca-140">마법사 및 CreateUserWizard 컨트롤 56</span><span class="sxs-lookup"><span data-stu-id="819ca-140">Wizard and CreateUserWizard Controls 56</span></span>](#0.2__Toc253429273 "_Toc253429273")

<span data-ttu-id="819ca-141">**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**</span><span class="sxs-lookup"><span data-stu-id="819ca-141">**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**</span></span>  
[<span data-ttu-id="819ca-142">영역 지원</span><span class="sxs-lookup"><span data-stu-id="819ca-142">Areas Support</span></span>](#0.2__Toc253429275 "_Toc253429275")  
[<span data-ttu-id="819ca-143">데이터 주석을 특성 유효성 검사 지원을</span><span class="sxs-lookup"><span data-stu-id="819ca-143">Data-Annotation Attribute Validation Support</span></span>](#0.2__Toc253429276 "_Toc253429276")  
[<span data-ttu-id="819ca-144">템플릿 기반 도우미</span><span class="sxs-lookup"><span data-stu-id="819ca-144">Templated Helpers</span></span>](#0.2__Toc253429277 "_Toc253429277")

<span data-ttu-id="819ca-145">**[Dynamic Data](#0.2__Toc253429278 "_Toc253429278")**</span><span class="sxs-lookup"><span data-stu-id="819ca-145">**[Dynamic Data](#0.2__Toc253429278 "_Toc253429278")**</span></span>  
[<span data-ttu-id="819ca-146">기존 프로젝트에 대 한 동적 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="819ca-146">Enabling Dynamic Data for Existing Projects</span></span>](#0.2__Toc253429279 "_Toc253429279")  
[<span data-ttu-id="819ca-147">DynamicDataManager 컨트롤 선언적 구문</span><span class="sxs-lookup"><span data-stu-id="819ca-147">Declarative DynamicDataManager Control Syntax</span></span>](#0.2__Toc253429280 "_Toc253429280")  
[<span data-ttu-id="819ca-148">엔터티 템플릿에</span><span class="sxs-lookup"><span data-stu-id="819ca-148">Entity Templates</span></span>](#0.2__Toc253429281 "_Toc253429281")  
[<span data-ttu-id="819ca-149">Url 및 전자 메일 주소에 대 한 새 필드 템플릿을</span><span class="sxs-lookup"><span data-stu-id="819ca-149">New Field Templates for URLs and E-mail Addresses</span></span>](#0.2__Toc253429282 "_Toc253429282")  
[<span data-ttu-id="819ca-150">DynamicHyperLink 컨트롤을 사용 하 여 링크 만들기</span><span class="sxs-lookup"><span data-stu-id="819ca-150">Creating Links with the DynamicHyperLink Control</span></span>](#0.2__Toc253429283 "_Toc253429283")  
[<span data-ttu-id="819ca-151">데이터 모델의 상속에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="819ca-151">Support for Inheritance in the Data Model</span></span>](#0.2__Toc253429284 "_Toc253429284")  
[<span data-ttu-id="819ca-152">다 대 다 관계 (Entity Framework에만 해당)에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="819ca-152">Support for Many-to-Many Relationships (Entity Framework Only)</span></span>](#0.2__Toc253429285 "_Toc253429285")  
[<span data-ttu-id="819ca-153">새 특성을 제어 표시 및 지원 열거형</span><span class="sxs-lookup"><span data-stu-id="819ca-153">New Attributes to Control Display and Support Enumerations</span></span>](#0.2__Toc253429286 "_Toc253429286")  
[<span data-ttu-id="819ca-154">필터에 대 한 지원 강화</span><span class="sxs-lookup"><span data-stu-id="819ca-154">Enhanced Support for Filters</span></span>](#0.2__Toc253429287 "_Toc253429287")

<span data-ttu-id="819ca-155">**[Visual Studio 2010 웹 개발 기능 향상](#0.2__Toc253429288 "_Toc253429288")**</span><span class="sxs-lookup"><span data-stu-id="819ca-155">**[Visual Studio 2010 Web Development Improvements](#0.2__Toc253429288 "_Toc253429288")**</span></span>  
[<span data-ttu-id="819ca-156">CSS 호환성 향상</span><span class="sxs-lookup"><span data-stu-id="819ca-156">Improved CSS Compatibility</span></span>](#0.2__Toc253429289 "_Toc253429289")  
[<span data-ttu-id="819ca-157">HTML 및 JavaScript 코드 조각을</span><span class="sxs-lookup"><span data-stu-id="819ca-157">HTML and JavaScript Snippets</span></span>](#0.2__Toc253429290 "_Toc253429290")  
[<span data-ttu-id="819ca-158">JavaScript IntelliSense의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="819ca-158">JavaScript IntelliSense Enhancements</span></span>](#0.2__Toc253429291 "_Toc253429291")

<span data-ttu-id="819ca-159">**[웹 응용 프로그램 배포를 Visual Studio 2010](#0.2__Toc253429292 "_Toc253429292")**</span><span class="sxs-lookup"><span data-stu-id="819ca-159">**[Web Application Deployment with Visual Studio 2010](#0.2__Toc253429292 "_Toc253429292")**</span></span>  
[<span data-ttu-id="819ca-160">패키징 웹</span><span class="sxs-lookup"><span data-stu-id="819ca-160">Web Packaging</span></span>](#0.2__Toc253429293 "_Toc253429293")  
[<span data-ttu-id="819ca-161">Web.config 변환</span><span class="sxs-lookup"><span data-stu-id="819ca-161">Web.config Transformation</span></span>](#0.2__Toc253429294 "_Toc253429294")  
[<span data-ttu-id="819ca-162">데이터베이스 배포</span><span class="sxs-lookup"><span data-stu-id="819ca-162">Database Deployment</span></span>](#0.2__Toc253429295 "_Toc253429295")  
[<span data-ttu-id="819ca-163">웹 응용 프로그램에 대 한 One-click 게시</span><span class="sxs-lookup"><span data-stu-id="819ca-163">One-Click Publish for Web Applications</span></span>](#0.2__Toc253429296 "_Toc253429296")  
[<span data-ttu-id="819ca-164">Resources</span><span class="sxs-lookup"><span data-stu-id="819ca-164">Resources</span></span>](#0.2__Toc253429297 "_Toc253429297")

<span data-ttu-id="819ca-165">**[Disclaimer](#0.2__Toc253429298 "_Toc253429298")**</span><span class="sxs-lookup"><span data-stu-id="819ca-165">**[Disclaimer](#0.2__Toc253429298 "_Toc253429298")**</span></span>

<a id="0.2__Toc224729018"></a><a id="0.2__Toc253429238"></a><a id="0.2__Toc243304612"></a>

## <a name="core-services"></a><span data-ttu-id="819ca-166">핵심 서비스</span><span class="sxs-lookup"><span data-stu-id="819ca-166">Core Services</span></span>

<span data-ttu-id="819ca-167">ASP.NET 4에는 다양을 한 출력 캐싱 및 세션 상태 저장소와 같은 핵심 ASP.NET 서비스를 개선 하는 기능이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-167">ASP.NET 4 introduces a number of features that improve core ASP.NET services such as output caching and session-state storage.</span></span>

<a id="0.2__Toc243304613"></a><a id="0.2__Toc253429239"></a><a id="0.2__Toc224729019"></a>

### <a name="webconfig-file-refactoring"></a><span data-ttu-id="819ca-168">리팩터링 Web.config 파일</span><span class="sxs-lookup"><span data-stu-id="819ca-168">Web.config File Refactoring</span></span>

<span data-ttu-id="819ca-169">`Web.config` 웹 응용 프로그램의 규모가 상당히 지난 몇 차례의.NET Framework를 통해 새로운 기능이 추가 되었습니다, Ajax 등으로 대 한 구성이 포함 된 파일, 라우팅 및 IIS 7와 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-169">The `Web.config` file that contains the configuration for a Web application has grown considerably over the past few releases of the .NET Framework as new features have been added, such as Ajax, routing, and integration with IIS 7.</span></span> <span data-ttu-id="819ca-170">이로 인해 구성 하거나 Visual Studio와 같은 도구 없이 새 웹 응용 프로그램을 시작 하기 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-170">This has made it harder to configure or start new Web applications without a tool like Visual Studio.</span></span> <span data-ttu-id="819ca-171">이.NET Framework 4의 주요 구성 요소 이동 된는 `machine.config` 파일 및 응용 프로그램을 지금 이러한 설정을 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-171">In .the NET Framework 4, the major configuration elements have been moved to the `machine.config` file, and applications now inherit these settings.</span></span> <span data-ttu-id="819ca-172">이 통해는 `Web.config` 비어 있는 것으로 또는 Visual Studio에 대 한 응용 프로그램의 대상 프레임 워크의 버전을 지정 하는 다음 행만 포함 하는 ASP.NET 4 응용 프로그램에서 파일:</span><span class="sxs-lookup"><span data-stu-id="819ca-172">This allows the `Web.config` file in ASP.NET 4 applications either to be empty or to contain just the following lines, which specify for Visual Studio what version of the framework the application is targeting:</span></span>

[!code-xml[Main](overview/samples/sample1.xml)]

<a id="0.2__Toc253429240"></a><a id="0.2__Toc243304614"></a>

### <a name="extensible-output-caching"></a><span data-ttu-id="819ca-173">확장 가능한 출력 캐싱</span><span class="sxs-lookup"><span data-stu-id="819ca-173">Extensible Output Caching</span></span>

<span data-ttu-id="819ca-174">ASP.NET 1.0 출시 된 이후에 출력 캐싱을 메모리의 페이지, 컨트롤 및 HTTP 응답의 생성된 된 출력을 저장할 수 있게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-174">Since the time that ASP.NET 1.0 was released, output caching has enabled developers to store the generated output of pages, controls, and HTTP responses in memory.</span></span> <span data-ttu-id="819ca-175">후속 웹 요청에 ASP.NET 수 콘텐츠를 서비스 보다 신속 하 게 출력 처음부터 다시 생성 하는 대신 메모리에서 생성 된 출력을 검색 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-175">On subsequent Web requests, ASP.NET can serve content more quickly by retrieving the generated output from memory instead of regenerating the output from scratch.</span></span> <span data-ttu-id="819ca-176">그러나이 방법에는 제한 사항-생성 된 콘텐츠 항상 메모리에 저장할 수 있으며 웹 응용 프로그램의 다른 부분에서 메모리 요구가 원인와 경쟁 수 출력 캐싱을 사용 되는 메모리 사용량이 발생 하는 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-176">However, this approach has a limitation — generated content always has to be stored in memory, and on servers that are experiencing heavy traffic, the memory consumed by output caching can compete with memory demands from other portions of a Web application.</span></span>

<span data-ttu-id="819ca-177">ASP.NET 4에는 하나 이상의 사용자 지정 출력 캐시 공급자를 구성할 수 있도록 출력 캐싱에 확장성 지점을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-177">ASP.NET 4 adds an extensibility point to output caching that enables you to configure one or more custom output-cache providers.</span></span> <span data-ttu-id="819ca-178">출력 캐시 공급자 HTML 콘텐츠를 유지 하는 저장소 메커니즘을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-178">Output-cache providers can use any storage mechanism to persist HTML content.</span></span> <span data-ttu-id="819ca-179">이 클라우드 저장소에 로컬 또는 원격 디스크를 포함할 수 있는 다양 한 유지 메커니즘에 대 한 사용자 지정 출력 캐시 공급자를 만들 수 있으며 분산 캐시 엔진이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-179">This makes it possible to create custom output-cache providers for diverse persistence mechanisms, which can include local or remote disks, cloud storage, and distributed cache engines.</span></span>

<span data-ttu-id="819ca-180">새에서 파생 되는 클래스로 사용자 지정 출력 캐시 공급자를 만든 *System.Web.Caching.OutputCacheProvider* 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-180">You create a custom output-cache provider as a class that derives from the new *System.Web.Caching.OutputCacheProvider* type.</span></span> <span data-ttu-id="819ca-181">공급자를 구성할 수 있습니다는 `Web.config` new를 사용 하 여 파일 *공급자* 하위 섹션에서 *outputCache* 요소를 다음 예제와 같이:</span><span class="sxs-lookup"><span data-stu-id="819ca-181">You can then configure the provider in the `Web.config` file by using the new *providers* subsection of the *outputCache* element, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample2.xml)]

<span data-ttu-id="819ca-182">ASP.NET 4에서는 모든 HTTP 응답에에서는 기본적으로 렌더링 된 페이지 및 컨트롤 앞의 예에서 같이 메모리에 출력 캐시를 사용 하 여 여기서는 *defaultProvider* 특성은 AspNetInternalProvider로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-182">By default in ASP.NET 4, all HTTP responses, rendered pages, and controls use the in-memory output cache, as shown in the previous example, where the *defaultProvider* attribute is set to AspNetInternalProvider.</span></span> <span data-ttu-id="819ca-183">에 대 한 다른 공급자 이름을 지정 하 여 웹 응용 프로그램에 대해 사용 되는 기본 출력 캐시 공급자를 변경할 수 있습니다 *defaultProvider*합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-183">You can change the default output-cache provider used for a Web application by specifying a different provider name for *defaultProvider*.</span></span>

<span data-ttu-id="819ca-184">또한 각 컨트롤에 대해 요청에 따라 되는 서로 다른 출력 캐시 공급자를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-184">In addition, you can select different output-cache providers per control and per request.</span></span> <span data-ttu-id="819ca-185">New를 사용 하 여 선언적으로 작업을 수행 하는 웹 사용자 컨트롤에 대 한 다른 출력 캐시 공급자를 선택 하는 가장 쉬운 방법은 *providerName* 다음 예제와 같이 control 지시문에 특성:</span><span class="sxs-lookup"><span data-stu-id="819ca-185">The easiest way to choose a different output-cache provider for different Web user controls is to do so declaratively by using the new *providerName* attribute in a control directive, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample3.aspx)]

<span data-ttu-id="819ca-186">HTTP 요청에 대 한 다른 출력 캐시 공급자를 지정 하는 약간 더 많은 작업이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-186">Specifying a different output cache provider for an HTTP request requires a little more work.</span></span> <span data-ttu-id="819ca-187">새 재정의 공급자를 선언적으로 지정 하지 않고 *GetOuputCacheProviderName* 에서 메서드는 `Global.asax` 파일을 프로그래밍 방식으로 특정 요청에 사용할 공급자를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-187">Instead of declaratively specifying the provider, you override the new *GetOuputCacheProviderName* method in the `Global.asax` file to programmatically specify which provider to use for a specific request.</span></span> <span data-ttu-id="819ca-188">다음 예제에서는 이 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-188">The following example shows how to do this.</span></span>

[!code-csharp[Main](overview/samples/sample4.cs)]

<span data-ttu-id="819ca-189">출력 캐시 공급자 확장 ASP.NET 4에 추가 하 여 웹 사이트에 대 한 더욱 강력 하 고 보다 자동화 출력 캐싱 전략을 이제 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-189">With the addition of output-cache provider extensibility to ASP.NET 4, you can now pursue more aggressive and more intelligent output-caching strategies for your Web sites.</span></span> <span data-ttu-id="819ca-190">예를 들어, 페이지를 디스크에 더 낮은 트래픽을 캐시 하는 동안 메모리에 사이트의 "상위 10 개의" 페이지를 캐시할 수는 이제 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-190">For example, it is now possible to cache the "Top 10" pages of a site in memory, while caching pages that get lower traffic on disk.</span></span> <span data-ttu-id="819ca-191">또는 모든 다양 조합 렌더링된 된 페이지에 대 한 캐시 수 있지만 프런트 엔드 웹 서버에서 메모리 소비는 오프 로드 하도록 분산된 캐시를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-191">Alternatively, you can cache every vary-by combination for a rendered page, but use a distributed cache so that the memory consumption is offloaded from front-end Web servers.</span></span>

<a id="0.2__Toc224729020"></a><a id="0.2__Toc253429241"></a><a id="0.2__Toc243304615"></a>

### <a name="auto-start-web-applications"></a><span data-ttu-id="819ca-192">웹 응용 프로그램을 자동으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-192">Auto-Start Web Applications</span></span>

<span data-ttu-id="819ca-193">일부 웹 응용 프로그램이 많은 양의 데이터를 로드 하거나 첫 번째 요청을 처리 하기 전에 처리 비용의 초기화를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-193">Some Web applications need to load large amounts of data or perform expensive initialization processing before serving the first request.</span></span> <span data-ttu-id="819ca-194">"해제" ASP.NET 응용 프로그램을 다음 중 초기화 코드를 실행 하는 사용자 지정 방식 고안 해야 했습니다 이러한 상황에 대 한 이전 버전의 ASP.NET에는 *응용 프로그램\_부하* 에서 메서드는 `Global.asax` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-194">In earlier versions of ASP.NET, for these situations you had to devise custom approaches to "wake up" an ASP.NET application and then run initialization code during the *Application\_Load* method in the `Global.asax` file.</span></span>

<span data-ttu-id="819ca-195">라는 새로운 확장성 기능 *자동 시작* 직접 주소가이 시나리오는 사용 가능한 경우 ASP.NET 4에서 실행 되도록 Windows Server 2008 r 2에서 IIS 7.5입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-195">A new scalability feature named *auto-start* that directly addresses this scenario is available when ASP.NET 4 runs on IIS 7.5 on Windows Server 2008 R2.</span></span> <span data-ttu-id="819ca-196">자동 시작 기능에는 응용 프로그램 풀을 시작, ASP.NET 응용 프로그램을 초기화 한 다음 HTTP 요청을 받아들이기 위한 제어 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-196">The auto-start feature provides a controlled approach for starting up an application pool, initializing an ASP.NET application, and then accepting HTTP requests.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="819ca-197">IIS 7.5 용 IIS 응용 프로그램 준비 모듈</span><span class="sxs-lookup"><span data-stu-id="819ca-197">IIS Application Warm-Up Module for IIS 7.5</span></span>
> 
> <span data-ttu-id="819ca-198">IIS 팀 IIS 7.5 용 응용 프로그램 준비 모듈의 첫 번째 베타 테스트 버전을 출시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-198">The IIS team has released the first beta test version of the Application Warm-Up Module for IIS 7.5.</span></span> <span data-ttu-id="819ca-199">이렇게 하면 앞에서 설명한 것 보다 더 쉽게 응용 프로그램을 준비 하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-199">This makes warming up your applications even easier than previously described.</span></span> <span data-ttu-id="819ca-200">사용자 지정 코드를 작성 하는 대신 웹 응용 프로그램에 네트워크의 요청을 수락 하기 전에 실행 하는 Url 리소스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-200">Instead of writing custom code, you specify the URLs of resources to execute before the Web application accepts requests from the network.</span></span> <span data-ttu-id="819ca-201">이 준비는 IIS 서비스의 시작 중에 발생 (으로 IIS 응용 프로그램 풀을 구성한 경우 *AlwaysRunning*) 및 IIS 작업자 프로세스가 재생 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="819ca-201">This warm-up occurs during startup of the IIS service (if you configured the IIS application pool as *AlwaysRunning*) and when an IIS worker process recycles.</span></span> <span data-ttu-id="819ca-202">재활용을 하는 동안 이전 IIS 작업자 프로세스가 요청 때까지 계속 실행 새로 만든된 작업자 프로세스는 완전히 준비를 방해 하지 또는 다른 문제로 인해 unprimed 캐시 응용 프로그램에서 발생할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-202">During recycle, the old IIS worker process continues to execute requests until the newly spawned worker process is fully warmed up, so that applications experience no interruptions or other issues due to unprimed caches.</span></span> <span data-ttu-id="819ca-203">이 모듈의 버전 2.0 부터는 ASP.NET 모든 버전을 사용 하는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-203">Note that this module works with any version of ASP.NET, starting with version 2.0.</span></span>
> 
> <span data-ttu-id="819ca-204">자세한 내용은 참조 [응용 프로그램 웜 업을](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net) IIS.net 웹 사이트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-204">For more information, see [Application Warm-Up](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net) on the IIS.net Web site.</span></span> <span data-ttu-id="819ca-205">준비 기능을 사용 하는 방법을 보여 주는 연습을 참조 하십시오. [IIS 7.5 응용 프로그램 준비 모듈 시작](https://www.iis.net/learn/manage) IIS.net 웹 사이트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-205">For a walkthrough that illustrates how to use the warm-up feature, see [Getting Started with the IIS 7.5 Application Warm-Up Module](https://www.iis.net/learn/manage) on the IIS.net Web site.</span></span>


<span data-ttu-id="819ca-206">자동 시작 기능을 사용 하려면 IIS 관리자에서 다음 구성을 사용 하 여 자동으로 시작 되도록 IIS 7.5에서 응용 프로그램 풀을 설정의 `applicationHost.config` 파일:</span><span class="sxs-lookup"><span data-stu-id="819ca-206">To use the auto-start feature, an IIS administrator sets an application pool in IIS 7.5 to be automatically started by using the following configuration in the `applicationHost.config` file:</span></span>

[!code-xml[Main](overview/samples/sample5.xml)]

<span data-ttu-id="819ca-207">개별 응용 프로그램에 다음 구성을 사용 하 여 자동으로 시작 되도록 지정 하는 단일 응용 프로그램 풀에서 여러 응용 프로그램을 포함할 수 있으므로 `applicationHost.config` 파일:</span><span class="sxs-lookup"><span data-stu-id="819ca-207">Because a single application pool can contain multiple applications, you specify individual applications to be automatically started by using the following configuration in the `applicationHost.config` file:</span></span>

[!code-xml[Main](overview/samples/sample6.xml)]

<span data-ttu-id="819ca-208">IIS 7.5의 정보를 사용 하 여 IIS 7.5 서버는 콜드 시작 또는 개별 응용 프로그램 풀이 재생 되는 `applicationHost.config` 파일을 자동으로 시작 되도록 어떤 웹 응용 프로그램 요구를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-208">When an IIS 7.5 server is cold-started or when an individual application pool is recycled, IIS 7.5 uses the information in the `applicationHost.config` file to determine which Web applications need to be automatically started.</span></span> <span data-ttu-id="819ca-209">Iis 7.5 자동 시작에 대 한 표시 된 각 응용 프로그램에 대 한 HTTP 요청 상태는 응용 프로그램이 일시적으로 허용 하지 않습니다 응용 프로그램을 시작 하려면 ASP.NET 4로 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-209">For each application that is marked for auto-start, IIS7.5 sends a request to ASP.NET 4 to start the application in a state during which the application temporarily does not accept HTTP requests.</span></span> <span data-ttu-id="819ca-210">ASP.NET에 정의 된 형식을 인스턴스화하이 상태에 있을 때에 *serviceAutoStartProvider* 특성 (같이 이전 예에서) 및 해당 공용 진입점으로 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-210">When it is in this state, ASP.NET instantiates the type defined by the *serviceAutoStartProvider* attribute (as shown in the previous example) and calls into its public entry point.</span></span>

<span data-ttu-id="819ca-211">구현 하 여 필요한 진입점과 관리 되는 자동 시작 종류를 만들는 *(는) IProcessHostPreloadClient* 다음 예제와 같이 인터페이스:</span><span class="sxs-lookup"><span data-stu-id="819ca-211">You create a managed auto-start type with the necessary entry point by implementing the *IProcessHostPreloadClient* interface, as shown in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample7.cs)]

<span data-ttu-id="819ca-212">프로그램 초기화 된 후 코드에서 실행의 *미리 로드* 메서드 및 메서드는 반환, ASP.NET 응용 프로그램 요청을 처리할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-212">After your initialization code runs in the *Preload* method and the method returns, the ASP.NET application is ready to process requests.</span></span>

<span data-ttu-id="819ca-213">이제 자동 시작.5 IIS와 ASP.NET 4를 추가 하 여는 잘 정의 된 방식을 첫 번째 HTTP 요청을 처리 하기 전에 비용이 많이 드는 응용 프로그램 초기화를 수행 하기 위한 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-213">With the addition of auto-start to IIS .5 and ASP.NET 4, you now have a well-defined approach for performing expensive application initialization prior to processing the first HTTP request.</span></span> <span data-ttu-id="819ca-214">예를 들어 응용 프로그램 초기화는 응용 프로그램이 초기화 되었고 HTTP 트래픽을 허용 하도록 준비 하는 부하 분산 장치를 다음 신호를 보내는 데 새 자동 시작 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-214">For example, you can use the new auto-start feature to initialize an application and then signal a load-balancer that the application was initialized and ready to accept HTTP traffic.</span></span>

<a id="0.2__Toc224729021"></a><a id="0.2__Toc253429242"></a><a id="0.2__Toc243304616"></a>

### <a name="permanently-redirecting-a-page"></a><span data-ttu-id="819ca-215">페이지를 영구적으로 리디렉션</span><span class="sxs-lookup"><span data-stu-id="819ca-215">Permanently Redirecting a Page</span></span>

<span data-ttu-id="819ca-216">검색 엔진에서 유효 하지 않은 링크의 누적 될 수 있는 시간에 따라 페이지 및 콘텐츠에 주위를 이동할 수는 웹 응용 프로그램에서 일반적인이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-216">It is common practice in Web applications to move pages and other content around over time, which can lead to an accumulation of stale links in search engines.</span></span> <span data-ttu-id="819ca-217">Asp.net에서 개발자가 일반적으로 요청 이전 Url 사용 하 여 처리를 사용 하 여는 *Response.Redirect* 메서드를 새 URL로 요청을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-217">In ASP.NET, developers have traditionally handled requests to old URLs by using by using the *Response.Redirect* method to forward a request to the new URL.</span></span> <span data-ttu-id="819ca-218">그러나는 *리디렉션* 메서드 추가 http 왕복 이전 Url에 액세스 하려고 할 때 발생 하는 HTTP 302 찾을 (임시 리디렉션) 응답을 발급 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-218">However, the *Redirect* method issues an HTTP 302 Found (temporary redirect) response, which results in an extra HTTP round trip when users attempt to access the old URLs.</span></span>

<span data-ttu-id="819ca-219">ASP.NET 4를 새로 추가 *RedirectPermanent* HTTP 301 문제를 쉽게 도우미 메서드 다음 예제와 같이 응답을 영구적으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-219">ASP.NET 4 adds a new *RedirectPermanent* helper method that makes it easy to issue HTTP 301 Moved Permanently responses, as in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample8.cs)]

<span data-ttu-id="819ca-220">검색 엔진 및 영구 리디렉션을 인식 하는 다른 사용자 에이전트는 임시 리디렉션을 위해 브라우저에서 불필요 한 왕복을 제거 하는 콘텐츠의와 연결 된 새 URL을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-220">Search engines and other user agents that recognize permanent redirects will store the new URL that is associated with the content, which eliminates the unnecessary round trip made by the browser for temporary redirects.</span></span>

<a id="0.2__Toc224729022"></a><a id="0.2__Toc253429243"></a><a id="0.2__Toc243304617"></a>

### <a name="shrinking-session-state"></a><span data-ttu-id="819ca-221">세션 상태를 축소합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-221">Shrinking Session State</span></span>

<span data-ttu-id="819ca-222">ASP.NET 웹 팜 전체에서 세션 상태를 저장 하기 위한 두 가지 기본 옵션을 제공:-out-of-process 세션 상태 서버를 사용 하는 호출 하는 세션 상태 공급자 및 Microsoft SQL Server 데이터베이스에 데이터를 저장 하는 세션 상태 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-222">ASP.NET provides two default options for storing session state across a Web farm: a session-state provider that invokes an out-of-process session-state server, and a session-state provider that stores data in a Microsoft SQL Server database.</span></span> <span data-ttu-id="819ca-223">두 옵션 모두 웹 응용 프로그램의 작업자 프로세스 외부 상태 정보를 저장 되므로, 원격 저장소로 전송 하기 전에 serialize 할 세션 상태에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-223">Because both options involve storing state information outside a Web application's worker process, session state has to be serialized before it is sent to remote storage.</span></span> <span data-ttu-id="819ca-224">세션 상태에 저장 되는 정보의 양을에 따라 serialize 된 데이터의 크기가 상당히 커질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-224">Depending on how much information a developer saves in session state, the size of the serialized data can grow quite large.</span></span>

<span data-ttu-id="819ca-225">ASP.NET 4에서는 두 종류의-out-of-process 세션 상태 공급자에 대 한 새 압축 옵션을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-225">ASP.NET 4 introduces a new compression option for both kinds of out-of-process session-state providers.</span></span> <span data-ttu-id="819ca-226">경우는 *compressionEnabled* 다음 예제에 표시 된 구성 옵션 설정 되어 *true*, ASP.NET은 압축 (및 압축 풀기) .NETFramework를사용하여serialize된세션상태 *System.IO.Compression.GZipStream* 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-226">When the *compressionEnabled* configuration option shown in the following example is set to *true*, ASP.NET will compress (and decompress) serialized session state by using the .NET Framework *System.IO.Compression.GZipStream* class.</span></span>

[!code-xml[Main](overview/samples/sample9.xml)]

<span data-ttu-id="819ca-227">간단한 새 특성을 추가 하 여는 `Web.config` 파일, 응용 프로그램을 웹 서버에 배포할 예비 CPU 주기 serialize 세션 상태 데이터의 크기에 상당한 절감을 실현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-227">With the simple addition of the new attribute to the `Web.config` file, applications with spare CPU cycles on Web servers can realize substantial reductions in the size of serialized session-state data.</span></span>

<a id="0.2__Toc253429244"></a><a id="0.2__Toc243304618"></a>

### <a name="expanding-the-range-of-allowable-urls"></a><span data-ttu-id="819ca-228">허용 가능한 Url 범위를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-228">Expanding the Range of Allowable URLs</span></span>

<span data-ttu-id="819ca-229">ASP.NET 4 응용 프로그램 Url의 크기를 확장 하는 것에 대 한 새 옵션을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-229">ASP.NET 4 introduces new options for expanding the size of application URLs.</span></span> <span data-ttu-id="819ca-230">이전 버전의 ASP.NET URL 경로 길이가 260 자, NTFS 파일 경로 제한에 따라 제약을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-230">Previous versions of ASP.NET constrained URL path lengths to 260 characters, based on the NTFS file-path limit.</span></span> <span data-ttu-id="819ca-231">ASP.NET 4에는 옵션이 있습니다 (늘리거나) 응용 프로그램에 따라이 한도 사용 하 여 두 개의 새 *httpRuntime* 구성 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-231">In ASP.NET 4, you have the option to increase (or decrease) this limit as appropriate for your applications, using two new *httpRuntime* configuration attributes.</span></span> <span data-ttu-id="819ca-232">다음 예제에서는 이러한 새 특성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-232">The following example shows these new attributes.</span></span>

[!code-xml[Main](overview/samples/sample10.xml)]

<span data-ttu-id="819ca-233">더 길거나 더 짧은 경로 (프로토콜, 서버 이름 및 쿼리 문자열을 포함 하지 않는 URL의 일부)를 허용 하려면 수정 된 *[maxUrlLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-233">To allow longer or shorter paths (the portion of the URL that does not include protocol, server name, and query string), modify the *[maxUrlLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* attribute.</span></span> <span data-ttu-id="819ca-234">길거나 짧은 쿼리 문자열을 허용 하려면 값을 수정 된 *[maxQueryStringLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-234">To allow longer or shorter query strings, modify the value of the *[maxQueryStringLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* attribute.</span></span>

<span data-ttu-id="819ca-235">ASP.NET 4를 사용 하면 URL 문자 검사에서 사용 되는 문자를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-235">ASP.NET 4 also enables you to configure the characters that are used by the URL character check.</span></span> <span data-ttu-id="819ca-236">ASP.NET URL의 경로 부분에서 잘못 된 문자를 찾습니다, 요청을 거부 하 고 HTTP 400 오류를 발생 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-236">When ASP.NET finds an invalid character in the path portion of a URL, it rejects the request and issues an HTTP 400 error.</span></span> <span data-ttu-id="819ca-237">ASP.NET의 이전 버전에서는 URL 문자 검사 된 고정된 문자 집합으로 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-237">In previous versions of ASP.NET, the URL character checks were limited to a fixed set of characters.</span></span> <span data-ttu-id="819ca-238">ASP.NET 4에서 new를 사용 하는 유효한 문자 집합이 사용자 지정할 수 *requestPathInvalidChars* 특성에는 *httpRuntime* 다음 예제와 같이 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="819ca-238">In ASP.NET 4, you can customize the set of valid characters using the new *requestPathInvalidChars* attribute of the *httpRuntime* configuration element, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample11.xml)]

<span data-ttu-id="819ca-239">기본적으로는 <em>requestPathInvalidChars</em> 특성은 8 자 잘못 된 것으로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-239">By default, the <em>requestPathInvalidChars</em> attribute defines eight characters as invalid.</span></span> <span data-ttu-id="819ca-240">(에 할당 된 문자열에 <em>requestPathInvalidChars</em> 기본적으로<em>,</em>는 보다 작은 (&lt;), 보다 큼 (&gt;), 및 앰퍼샌드 (&amp;) 문자는 때문에 인코딩된는 `Web.config` 파일은 XML 파일입니다.) 필요에 따라 잘못 된 문자 집합을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-240">(In the string that is assigned to <em>requestPathInvalidChars</em> by default<em>,</em>the less than (&lt;), greater than (&gt;), and ampersand (&amp;) characters are encoded, because the `Web.config` file is an XML file.) You can customize the set of invalid characters as needed.</span></span>

> [!NOTE]
> <span data-ttu-id="819ca-241">참고의 IETF RFC 2396에 정의 된 대로 잘못 된 URL 문자는 항상 0x00-0x1f, ASCII 범위에 문자를 포함 하는 URL 경로 거부 ASP.NET 4 ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt)).</span><span class="sxs-lookup"><span data-stu-id="819ca-241">Note ASP.NET 4 always rejects URL paths that contain characters in the ASCII range of 0x00 to 0x1F, because those are invalid URL characters as defined in RFC 2396 of the IETF ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt)).</span></span> <span data-ttu-id="819ca-242">IIS 6을 실행 하는 버전의 Windows Server에서 또는 이상 http.sys 프로토콜 장치 드라이버 자동으로 거부 Url이 문자로 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-242">On versions of Windows Server that run IIS 6 or higher, the http.sys protocol device driver automatically rejects URLs with these characters.</span></span>


<a id="0.2__Toc253429245"></a><a id="0.2__Toc243304619"></a>

### <a name="extensible-request-validation"></a><span data-ttu-id="819ca-243">확장 가능한 요청 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="819ca-243">Extensible Request Validation</span></span>

<span data-ttu-id="819ca-244">ASP.NET 요청 유효성 검사는 사이트 간 스크립팅 (XSS) 공격에 자주 사용 되는 문자열에 대 한 들어오는 HTTP 요청 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-244">ASP.NET request validation searches incoming HTTP request data for strings that are commonly used in cross-site scripting (XSS) attacks.</span></span> <span data-ttu-id="819ca-245">잠재적인 XSS 문자열이 발견 되 면 요청 유효성 검사는 주의 대상 문자열에 플래그를 지정 하 고 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-245">If potential XSS strings are found, request validation flags the suspect string and returns an error.</span></span> <span data-ttu-id="819ca-246">XSS 공격에 사용 되는 가장 일반적인 문자열을 찾은 경우에 기본 제공 요청 유효성 검사 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-246">The built-in request validation returns an error only when it finds the most common strings used in XSS attacks.</span></span> <span data-ttu-id="819ca-247">너무 많은 긍정 XSS 유효성 검사를 보다 적극적으로 확인을 이전의 시도가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-247">Previous attempts to make the XSS validation more aggressive resulted in too many false positives.</span></span> <span data-ttu-id="819ca-248">하지만 고객 특정 페이지 또는 특정 유형의 요청에 대 한 보다 적극적으로 또는 반대로 할 수 의도적으로 XSS을 완화 하는 요청 유효성 검사를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-248">However, customers might want request validation that is more aggressive, or conversely might want to intentionally relax XSS checks for specific pages or for specific types of requests.</span></span>

<span data-ttu-id="819ca-249">ASP.NET 4에서 요청 유효성 검사 기능 이루어졌을 확장 가능한 사용자 지정 요청 유효성 검사 논리를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-249">In ASP.NET 4, the request validation feature has been made extensible so that you can use custom request-validation logic.</span></span> <span data-ttu-id="819ca-250">요청 유효성 검사를 확장 하려면 새에서 파생 되는 클래스를 만듭니다 *System.Web.Util.RequestValidator* 유형인, 응용 프로그램을 구성 합니다. (에 *httpRuntime* 는 의섹션`Web.config`파일)를 사용자 지정 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-250">To extend request validation, you create a class that derives from the new *System.Web.Util.RequestValidator* type, and you configure the application (in the *httpRuntime* section of the `Web.config` file) to use the custom type.</span></span> <span data-ttu-id="819ca-251">다음 예제에서는 사용자 지정 요청 유효성 검사 클래스를 구성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-251">The following example shows how to configure a custom request-validation class:</span></span>

[!code-xml[Main](overview/samples/sample12.xml)]

<span data-ttu-id="819ca-252">새 *requestValidationType* 특성에 사용자 지정 요청 유효성 검사를 제공 하는 클래스를 지정 하는 표준.NET Framework 형식 식별자 문자열이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-252">The new *requestValidationType* attribute requires a standard .NET Framework type identifier string that specifies the class that provides custom request validation.</span></span> <span data-ttu-id="819ca-253">각 요청에 대 한 ASP.NET 각 들어오는 HTTP 요청 데이터를 처리 하려면 사용자 지정 형식을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-253">For each request, ASP.NET invokes the custom type to process each piece of incoming HTTP request data.</span></span> <span data-ttu-id="819ca-254">들어오는 URL, (쿠키 및 사용자 지정 헤더), 모든 HTTP 헤더 및 엔터티 본문은 다음 예제에 표시 된 같은 사용자 지정 요청 유효성 검사 클래스에 대 한 모든 사용 가능한:</span><span class="sxs-lookup"><span data-stu-id="819ca-254">The incoming URL, all the HTTP headers (both cookies and custom headers), and the entity body are all available for inspection by a custom request validation class like that shown in the following example:</span></span>

[!code-csharp[Main](overview/samples/sample13.cs)]

<span data-ttu-id="819ca-255">여기서 하지 않으려는 경우 들어오는 HTTP 데이터를 검사 하는 경우 요청 유효성 검사 클래스 대체할 수 있습니다 ASP.NET 기본 요청 유효성 검사를 단순히 호출 하 여 실행할 수 있도록 *기본 합니다. IsValidRequestString 합니다.*</span><span class="sxs-lookup"><span data-stu-id="819ca-255">For cases where you do not want to inspect a piece of incoming HTTP data, the request-validation class can fall back to let the ASP.NET default request validation run by simply calling *base.IsValidRequestString.*</span></span>

<a id="0.2__Toc253429246"></a><a id="0.2__Toc243304620"></a>

### <a name="object-caching-and-object-caching-extensibility"></a><span data-ttu-id="819ca-256">개체 캐싱 및 캐싱 확장성 개체</span><span class="sxs-lookup"><span data-stu-id="819ca-256">Object Caching and Object Caching Extensibility</span></span>

<span data-ttu-id="819ca-257">ASP.NET가 강력한 메모리 내 개체 캐시의 첫 번째 릴리스 이후 포함 (*System.Web.Caching.Cache*).</span><span class="sxs-lookup"><span data-stu-id="819ca-257">Since its first release, ASP.NET has included a powerful in-memory object cache (*System.Web.Caching.Cache*).</span></span> <span data-ttu-id="819ca-258">캐시를 구현 하는 비 웹 응용 프로그램에서 사용 된는 자주 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-258">The cache implementation has been so popular that it has been used in non-Web applications.</span></span> <span data-ttu-id="819ca-259">그러나 것이에 대 한 참조를 포함 하는 Windows Forms 또는 WPF 응용 프로그램에 대 한 잘못 된 구문이 `System.Web.dll` 를 대비해 ASP.NET 개체 캐시를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-259">However, it is awkward for a Windows Forms or WPF application to include a reference to `System.Web.dll` just to be able to use the ASP.NET object cache.</span></span>

<span data-ttu-id="819ca-260">캐시를 사용 하려면 모든 응용 프로그램에 대 한.NET Framework 4에는 새 어셈블리, 새 네임 스페이스, 일부 기본 형식 및 구체적인 구현을 캐싱 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-260">To make caching available for all applications, the .NET Framework 4 introduces a new assembly, a new namespace, some base types, and a concrete caching implementation.</span></span> <span data-ttu-id="819ca-261">새 `System.Runtime.Caching.dll` 에 새로운 캐싱 API를 포함 하는 어셈블리는 *System.Runtime.Caching* 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-261">The new `System.Runtime.Caching.dll` assembly contains a new caching API in the *System.Runtime.Caching* namespace.</span></span> <span data-ttu-id="819ca-262">네임 스페이스는 두 가지 핵심 클래스 집합이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-262">The namespace contains two core sets of classes:</span></span>

- <span data-ttu-id="819ca-263">모든 유형의 사용자 지정 캐시 구현 작성 하기 위한 기초를 제공 하는 추상 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-263">Abstract types that provide the foundation for building any type of custom cache implementation.</span></span>
- <span data-ttu-id="819ca-264">구체적인 메모리에 개체 캐시 구현 (의 *System.Runtime.Caching.MemoryCache* 클래스).</span><span class="sxs-lookup"><span data-stu-id="819ca-264">A concrete in-memory object cache implementation (the *System.Runtime.Caching.MemoryCache* class).</span></span>

<span data-ttu-id="819ca-265">새 *MemoryCache* 클래스는 ASP.NET 캐시와 비슷하게 모델링 및 내부 캐시 엔진 논리의 대부분 ASP.NET와 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-265">The new *MemoryCache* class is modeled closely on the ASP.NET cache, and it shares much of the internal cache engine logic with ASP.NET.</span></span> <span data-ttu-id="819ca-266">하지만의 공용 캐싱 Api *System.Runtime.Caching* ASP.NET을 사용한 경우 개발 된 사용자 지정의 캐시를 지원 하도록 업데이트 되었습니다 *캐시* 개체에 익숙한 개념을 찾을 수 있습니다는 새 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-266">Although the public caching APIs in *System.Runtime.Caching* have been updated to support development of custom caches, if you have used the ASP.NET *Cache* object, you will find familiar concepts in the new APIs.</span></span>

<span data-ttu-id="819ca-267">자세한 내용은 새 *MemoryCache* 클래스 및 기본 Api를 지 원하는 전체 문서를 기준으로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-267">An in-depth discussion of the new *MemoryCache* class and supporting base APIs would require an entire document.</span></span> <span data-ttu-id="819ca-268">그러나 다음 예제에서는 제공 새 캐시 API의 작동 방식을 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-268">However, the following example gives you an idea of how the new cache API works.</span></span> <span data-ttu-id="819ca-269">이 예제에서는 모든 종속성 없이 Windows Forms 응용 프로그램에 대 한 작성 되었습니다 `System.Web.dll`합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-269">The example was written for a Windows Forms application, without any dependency on `System.Web.dll`.</span></span>

[!code-csharp[Main](overview/samples/sample14.cs)]

<a id="0.2__Toc253429247"></a><a id="0.2__Toc243304621"></a>

### <a name="extensible-html-url-and-http-header-encoding"></a><span data-ttu-id="819ca-270">확장 가능한 HTML, URL 및 HTTP 헤더 인코딩</span><span class="sxs-lookup"><span data-stu-id="819ca-270">Extensible HTML, URL, and HTTP Header Encoding</span></span>

<span data-ttu-id="819ca-271">ASP.NET 4에서 다음과 같은 일반적인 텍스트 인코딩 작업에 대 한 사용자 지정 인코딩 루틴을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-271">In ASP.NET 4, you can create custom encoding routines for the following common text-encoding tasks:</span></span>

- <span data-ttu-id="819ca-272">HTML 인코딩입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-272">HTML encoding.</span></span>
- <span data-ttu-id="819ca-273">URL 인코딩은 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-273">URL encoding.</span></span>
- <span data-ttu-id="819ca-274">HTML 특성 인코딩입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-274">HTML attribute encoding.</span></span>
- <span data-ttu-id="819ca-275">아웃 바운드 HTTP 헤더를 인코딩입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-275">Encoding outbound HTTP headers.</span></span>

<span data-ttu-id="819ca-276">새에서 파생 하 여 사용자 지정 인코더를 만들 수 있습니다 *System.Web.Util.HttpEncoder* 유형 및 다음 ASP.NET을 구성에서 사용자 지정 형식을 사용 하는 *httpRuntime* 의 섹션은 `Web.config` 파일을로 다음 예제에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-276">You can create a custom encoder by deriving from the new *System.Web.Util.HttpEncoder* type and then configuring ASP.NET to use the custom type in the *httpRuntime* section of the `Web.config` file, as shown in the following example:</span></span>

[!code-xml[Main](overview/samples/sample15.xml)]

<span data-ttu-id="819ca-277">ASP.NET 사용자 지정 인코딩 구현을 인코딩 방법의 공용 때마다 자동으로 호출 사용자 지정 인코더를 구성한 후의 *System.Web.HttpUtility* 또는 *System.Web.HttpServerUtility* 클래스 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-277">After a custom encoder has been configured, ASP.NET automatically calls the custom encoding implementation whenever public encoding methods of the *System.Web.HttpUtility* or *System.Web.HttpServerUtility* classes are called.</span></span> <span data-ttu-id="819ca-278">한 부분을 웹 개발 팀의 웹 개발 팀의 나머지 부분에서 계속 공용 ASP.NET 인코딩 Api를 사용 하는 동안 적극적인 문자 인코딩을 구현 하는 사용자 지정 인코더를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-278">This lets one part of a Web development team create a custom encoder that implements aggressive character encoding, while the rest of the Web development team continues to use the public ASP.NET encoding APIs.</span></span> <span data-ttu-id="819ca-279">사용자 지정 인코더를 중앙에서 구성 하 여는 *httpRuntime* 요소를 공용 ASP.NET 인코딩 Api의 모든 텍스트 인코딩 호출은 사용자 지정 인코더를 통해 라우팅될 수 있도록을 정렬 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-279">By centrally configuring a custom encoder in the *httpRuntime* element, you are guaranteed that all text-encoding calls from the public ASP.NET encoding APIs are routed through the custom encoder.</span></span>

<a id="0.2__Toc253429248"></a><a id="0.2__Toc243304622"></a>

### <a name="performance-monitoring-for-individual-applications-in-a-single-worker-process"></a><span data-ttu-id="819ca-280">단일 작업자 프로세스에서 개별 응용 프로그램에 대 한 성능 모니터링</span><span class="sxs-lookup"><span data-stu-id="819ca-280">Performance Monitoring for Individual Applications in a Single Worker Process</span></span>

<span data-ttu-id="819ca-281">단일 서버에서 호스팅할 수 있는 웹 사이트 수를 늘리기 위해 많은 호스팅 서비스 공급자의 단일 작업자 프로세스가 여러 ASP.NET 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-281">In order to increase the number of Web sites that can be hosted on a single server, many hosters run multiple ASP.NET applications in a single worker process.</span></span> <span data-ttu-id="819ca-282">그러나 여러 응용 프로그램에 단일 공유 작업자 프로세스를 사용 하는 경우 어렵습니다 문제가 발생 하는 개별 응용 프로그램을 식별 하는 서버 관리자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-282">However, if multiple applications use a single shared worker process, it is difficult for server administrators to identify an individual application that is experiencing problems.</span></span>

<span data-ttu-id="819ca-283">ASP.NET 4 CLR에 의해 도입 된 새 리소스 모니터링 기능을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-283">ASP.NET 4 leverages new resource-monitoring functionality introduced by the CLR.</span></span> <span data-ttu-id="819ca-284">이 기능을 활성화 하려면 다음 XML 구성 코드 조각에 추가할 수 있습니다는 `aspnet.config` 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-284">To enable this functionality, you can add the following XML configuration snippet to the `aspnet.config` configuration file.</span></span>

[!code-xml[Main](overview/samples/sample16.xml)]

> [!NOTE]
> <span data-ttu-id="819ca-285">참고는 `aspnet.config` 파일이.NET Framework를 설치한 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-285">Note The `aspnet.config` file is in the directory where the .NET Framework is installed.</span></span> <span data-ttu-id="819ca-286">없으면는 `Web.config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-286">It is not the `Web.config` file.</span></span>


<span data-ttu-id="819ca-287">경우는 *appDomainResourceMonitoring* 기능은, 두 개의 새로운 성능 카운터 "ASP.NET 응용 프로그램" 성능 범주에서 사용할 수 있는: *관리 되는 프로세서 시간 백분율* 및  *관리 되는 사용 되는 메모리*합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-287">When the *appDomainResourceMonitoring* feature has been enabled, two new performance counters are available in the "ASP.NET Applications" performance category: *% Managed Processor Time* and *Managed Memory Used*.</span></span> <span data-ttu-id="819ca-288">이러한 성능 카운터의 모두 예상된 CPU 시간 및 개별 ASP.NET 응용 프로그램의 관리 되는 메모리 사용률을 추적 하는 새로운 CLR 응용 프로그램 도메인 리소스 관리 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-288">Both of these performance counters use the new CLR application-domain resource management feature to track estimated CPU time and managed memory utilization of individual ASP.NET applications.</span></span> <span data-ttu-id="819ca-289">결과적으로, ASP.NET 4 관리자 생깁니다 단일 작업자 프로세스에서 실행 되는 개별 응용 프로그램의 리소스 소비량에 대 한 보다 세부적인 뷰.</span><span class="sxs-lookup"><span data-stu-id="819ca-289">As a result, with ASP.NET 4, administrators now have a more granular view into the resource consumption of individual applications running in a single worker process.</span></span>

<a id="0.2__Toc253429249"></a><a id="0.2__Toc243304623"></a>

### <a name="multi-targeting"></a><span data-ttu-id="819ca-290">멀티 타기팅</span><span class="sxs-lookup"><span data-stu-id="819ca-290">Multi-Targeting</span></span>

<span data-ttu-id="819ca-291">특정 버전의.NET Framework를 대상으로 하는 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-291">You can create an application that targets a specific version of the .NET Framework.</span></span> <span data-ttu-id="819ca-292">ASP.NET 4에서 새 특성에는 *컴파일* 의 요소는 `Web.config` 파일을 사용 하면.NET Framework 4 이상을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-292">In ASP.NET 4, a new attribute in the *compilation* element of the `Web.config` file lets you target the .NET Framework 4 and later.</span></span> <span data-ttu-id="819ca-293">.NET Framework 4를 명시적으로 대상 및에서 선택적 요소를 포함 하는 경우는 `Web.config` 파일에 대 한 항목 예: *system.codedom*, 이러한 요소는.NET Framework 4에 대 한 정확 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-293">If you explicitly target the .NET Framework 4, and if you include optional elements in the `Web.config` file such as the entries for *system.codedom*, these elements must be correct for the .NET Framework 4.</span></span> <span data-ttu-id="819ca-294">(.NET Framework 4를 명시적으로 대상 하지 않으면 대상 프레임 워크에 있는 항목의 부족에서 유추 됩니다는 `Web.config` 파일입니다.)</span><span class="sxs-lookup"><span data-stu-id="819ca-294">(If you do not explicitly target the .NET Framework 4, the target framework is inferred from the lack of an entry in the `Web.config` file.)</span></span>

<span data-ttu-id="819ca-295">다음 예제에서는 사용을 보여 줍니다.는 *targetFramework* 특성에 *컴파일* 의 요소는 `Web.config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-295">The following example shows the use of the *targetFramework* attribute in the *compilation* element of the `Web.config` file.</span></span>

[!code-xml[Main](overview/samples/sample17.xml)]

<span data-ttu-id="819ca-296">특정 버전의.NET Framework를 대상으로 지정 하는 방법에 대 한 다음 note:</span><span class="sxs-lookup"><span data-stu-id="819ca-296">Note the following about targeting a specific version of the .NET Framework:</span></span>

- <span data-ttu-id="819ca-297">.NET Framework 4 응용 프로그램 풀에서 ASP.NET 빌드 시스템 가정은.NET Framework 4를 대상으로 하는 경우는 `Web.config` 파일에 포함 되지 않습니다는 *targetFramework* 특성 또는 경우에는 `Web.config` 파일이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-297">In a .NET Framework 4 application pool, the ASP.NET build system assumes the .NET Framework 4 as a target if the `Web.config` file does not include the *targetFramework* attribute or if the `Web.config` file is missing.</span></span> <span data-ttu-id="819ca-298">(.NET Framework 4에서 실행 되도록 응용 프로그램을 코딩 변경 해야 할 수도 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="819ca-298">(You might have to make coding changes to your application to make it run under the .NET Framework 4.)</span></span>
- <span data-ttu-id="819ca-299">포함 하는 경우는 *targetFramework* 특성, 경우에 *system.codeDom* 요소에 정의 된는 `Web.config` 파일을이 파일은.NET Framework 4에 대 한 올바른 항목을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-299">If you do include the *targetFramework* attribute, and if the *system.codeDom* element is defined in the `Web.config` file, this file must contain the correct entries for the .NET Framework 4.</span></span>
- <span data-ttu-id="819ca-300">사용 하는 경우는 *aspnet\_컴파일러* 응용 프로그램 (예: 빌드 환경)를 미리 컴파일하 명령에서 올바른 버전의를 사용 해야 합니다는 *aspnet\_컴파일러* 대상 프레임 워크에 대 한 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-300">If you are using the *aspnet\_compiler* command to precompile your application (such as in a build environment), you must use the correct version of the *aspnet\_compiler* command for the target framework.</span></span> <span data-ttu-id="819ca-301">.NET Framework 3.5 및 이전 버전에 대 한 컴파일하는 데는.NET Framework 2.0 (%WINDIR%\Microsoft.NET\Framework\v2.0.50727)와 함께 제공 되는 컴파일러를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-301">Use the compiler that shipped with the .NET Framework 2.0 (%WINDIR%\Microsoft.NET\Framework\v2.0.50727) to compile for the .NET Framework 3.5 and earlier versions.</span></span> <span data-ttu-id="819ca-302">.NET Framework 4와 함께 제공 되는 컴파일러를 사용 하 여 만든 응용 프로그램 프레임 워크를 사용 하 여 또는 이후 버전을 사용 하 여 컴파일하는 데 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-302">Use the compiler that ships with the .NET Framework 4 to compile applications created using that framework or using later versions.</span></span>
- <span data-ttu-id="819ca-303">런타임 시 컴파일러는 컴퓨터에 설치 된 최신 프레임 워크 어셈블리 사용 (일부 이므로 GAC에).</span><span class="sxs-lookup"><span data-stu-id="819ca-303">At run time, the compiler uses the latest framework assemblies that are installed on the computer (and therefore in the GAC).</span></span> <span data-ttu-id="819ca-304">Framework에 대 한 업데이트를 나중에 수행 하는 경우 (예를 들어 가상의 버전 4.1이 설치 되어), 경우에 프레임 워크의 최신 버전의 기능을 사용할 수는 *targetFramework* 더 낮은 버전을 대상 특성 (4.0과 같은).</span><span class="sxs-lookup"><span data-stu-id="819ca-304">If an update is made later to the framework (for example, a hypothetical version 4.1 is installed), you will be able to use features in the newer version of the framework even though the *targetFramework* attribute targets a lower version (such as 4.0).</span></span> <span data-ttu-id="819ca-305">그러나 (디자인 타임에 Visual Studio 2010 또는 사용 하는 경우에 *aspnet\_컴파일러* 명령, 프레임 워크의 최신 기능을 사용 하면 컴파일러 오류).</span><span class="sxs-lookup"><span data-stu-id="819ca-305">(However, at design time in Visual Studio 2010 or when you use the *aspnet\_compiler* command, using newer features of the framework will cause compiler errors).</span></span>

<a id="0.2__Toc224729023"></a><a id="0.2__Toc253429250"></a><a id="0.2__Toc243304624"></a>

## <a name="ajax"></a><span data-ttu-id="819ca-306">Ajax</span><span class="sxs-lookup"><span data-stu-id="819ca-306">Ajax</span></span>

<a id="0.2__Toc253429251"></a><a id="0.2__Toc243304625"></a>

### <a name="jquery-included-with-web-forms-and-mvc"></a><span data-ttu-id="819ca-307">jQuery Web Forms 및 MVC와 함께 제공 됨</span><span class="sxs-lookup"><span data-stu-id="819ca-307">jQuery Included with Web Forms and MVC</span></span>

<span data-ttu-id="819ca-308">Web Forms 및 MVC 모두에 대 한 Visual Studio 템플릿 jQuery 오픈 소스 라이브러리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-308">The Visual Studio templates for both Web Forms and MVC include the open-source jQuery library.</span></span> <span data-ttu-id="819ca-309">새 웹 사이트 또는 프로젝트를 만들 때 다음과 같은 3 파일이 포함 된 스크립트 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-309">When you create a new website or project, a Scripts folder containing the following 3 files is created:</span></span>

- <span data-ttu-id="819ca-310">jQuery-1.4.1.js –는 사람이 읽을 수, 축소 되지 않은 버전의 jQuery 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-310">jQuery-1.4.1.js – The human-readable, unminified version of the jQuery library.</span></span>
- <span data-ttu-id="819ca-311">jQuery 14.1.min.js-축소 된 버전의 jQuery 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-311">jQuery-14.1.min.js – The minified version of the jQuery library.</span></span>
- <span data-ttu-id="819ca-312">jQuery-1.4.1-vsdoc.js – jQuery 라이브러리에 대 한 Intellisense 설명서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-312">jQuery-1.4.1-vsdoc.js – The Intellisense documentation file for the jQuery library.</span></span>

<span data-ttu-id="819ca-313">응용 프로그램을 개발 하는 동안 축소 되지 않은 버전의 jQuery 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-313">Include the unminified version of jQuery while developing an application.</span></span> <span data-ttu-id="819ca-314">축소 된 버전의 jQuery 프로덕션 응용 프로그램에 대 한 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-314">Include the minified version of jQuery for production applications.</span></span>

<span data-ttu-id="819ca-315">예를 들어 다음 Web Forms 페이지 jQuery를 사용 하 여 포커스를가지고 있을 때 노란색 ASP.NET TextBox 컨트롤의 배경색을 변경 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-315">For example, the following Web Forms page illustrates how you can use jQuery to change the background color of ASP.NET TextBox controls to yellow when they have focus.</span></span>

[!code-aspx[Main](overview/samples/sample18.aspx)]

<a id="0.2__Toc253429252"></a><a id="0.2__Toc243304626"></a>

### <a name="content-delivery-network-support"></a><span data-ttu-id="819ca-316">콘텐츠 배달 네트워크 지원</span><span class="sxs-lookup"><span data-stu-id="819ca-316">Content Delivery Network Support</span></span>

<span data-ttu-id="819ca-317">Microsoft Ajax CDN 콘텐츠 배달 네트워크 ()를 사용 하 여 웹 응용 프로그램을 ASP.NET Ajax 및 jQuery 스크립트를 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-317">The Microsoft Ajax Content Delivery Network (CDN) enables you to easily add ASP.NET Ajax and jQuery scripts to your Web applications.</span></span> <span data-ttu-id="819ca-318">JQuery 라이브러리를 사용 하 여 추가 하 여 시작할 수는 예를 들어 한 `<script>` 태그를 다음과 같이 Ajax.microsoft.com 가리키는 페이지:</span><span class="sxs-lookup"><span data-stu-id="819ca-318">For example, you can start using the jQuery library simply by adding a `<script>` tag to your page that points to Ajax.microsoft.com like this:</span></span>

[!code-html[Main](overview/samples/sample19.html)]

<span data-ttu-id="819ca-319">Microsoft Ajax CDN을 활용 하기 위해, Ajax 응용 프로그램의 성능을 크게 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-319">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="819ca-320">Microsoft Ajax CDN의 콘텐츠는 세계에 있는 서버에 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-320">The contents of the Microsoft Ajax CDN are cached on servers located around the world.</span></span> <span data-ttu-id="819ca-321">또한 Microsoft Ajax CDN에는 브라우저 서로 다른 도메인에 있는 웹 사이트에 대 한 캐시 된 JavaScript 파일을 다시 사용할 수 있도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-321">In addition, the Microsoft Ajax CDN enables browsers to reuse cached JavaScript files for Web sites that are located in different domains.</span></span>

<span data-ttu-id="819ca-322">Microsoft Ajax 콘텐츠 배달 네트워크 Secure Sockets Layer를 사용 하 여 웹 페이지를 처리 해야 하는 경우 SSL (HTTPS)을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-322">The Microsoft Ajax Content Delivery Network supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="819ca-323">CDN을 사용할 수 없는 경우에 대체를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-323">Implement a fallback when the CDN is unavailable.</span></span> <span data-ttu-id="819ca-324">대체 (fallback)를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-324">Test the fallback.</span></span>

<span data-ttu-id="819ca-325">Microsoft Ajax CDN에 대 한 자세한 내용은 다음 웹 사이트를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-325">To learn more about the Microsoft Ajax CDN, visit the following website:</span></span>

[https://www.asp.net/ajaxlibrary/CDN.ashx](../../ajax/cdn/overview.md)

<span data-ttu-id="819ca-326">ASP.NET ScriptManager Microsoft Ajax CDN을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-326">The ASP.NET ScriptManager supports the Microsoft Ajax CDN.</span></span> <span data-ttu-id="819ca-327">EnableCdn 속성 설정 하나의 속성에 따라 단순히 CDN에서 모든 ASP.NET 프레임 워크 JavaScript 파일을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-327">Simply by setting one property, the EnableCdn property, you can retrieve all ASP.NET framework JavaScript files from the CDN:</span></span>

[!code-aspx[Main](overview/samples/sample20.aspx)]

<span data-ttu-id="819ca-328">True 값으로는 EnableCdn 속성을 설정한 후 ASP.NET 프레임 워크는 유효성 검사 및 UpdatePanel에 사용 되는 모든 JavaScript 파일을 포함 하 여 CDN에서 모든 ASP.NET 프레임 워크 JavaScript 파일을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-328">After you set the EnableCdn property to the value true, the ASP.NET framework will retrieve all ASP.NET framework JavaScript files from the CDN including all JavaScript files used for validation and the UpdatePanel.</span></span> <span data-ttu-id="819ca-329">이 하나의 속성을 설정 웹 응용 프로그램의 성능에 큰 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-329">Setting this one property can have a dramatic impact on the performance of your web application.</span></span>

<span data-ttu-id="819ca-330">웹 리소스의 특성을 사용 하 여 사용자 고유의 JavaScript 파일에 대 한의 CDN 경로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-330">You can set the CDN path for your own JavaScript files by using the WebResource attribute.</span></span> <span data-ttu-id="819ca-331">새 CdnPath 속성 값이 true로는 EnableCdn 속성을 설정 하는 경우 사용 되는 CDN에 대 한 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-331">The new CdnPath property specifies the path to the CDN used when you set the EnableCdn property to the value true:</span></span>

[!code-csharp[Main](overview/samples/sample21.cs)]

<a id="0.2__Toc253429253"></a><a id="0.2__Toc243304627"></a>

### <a name="scriptmanager-explicit-scripts"></a><span data-ttu-id="819ca-332">ScriptManager 명시적 스크립트</span><span class="sxs-lookup"><span data-stu-id="819ca-332">ScriptManager Explicit Scripts</span></span>

<span data-ttu-id="819ca-333">이전에 ASP.NET ScriptManger 사용 하는 경우 다음 해야 했습니다 전체 모놀리식 ASP.NET Ajax 라이브러리를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-333">In the past, if you used the ASP.NET ScriptManger then you were required to load the entire monolithic ASP.NET Ajax Library.</span></span> <span data-ttu-id="819ca-334">새 ScriptManager.AjaxFrameworkMode 속성을 이용 ASP.NET Ajax 라이브러리의 구성 요소를 로드 하는 정확 하 게 제어 하 고만 해야 하는 ASP.NET Ajax 라이브러리의 구성 요소를 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-334">By taking advantage of the new ScriptManager.AjaxFrameworkMode property, you can control exactly which components of the ASP.NET Ajax Library are loaded and load only the components of the ASP.NET Ajax Library that you need.</span></span>

<span data-ttu-id="819ca-335">ScriptManager.AjaxFrameworkMode 속성은 다음 값으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-335">The ScriptManager.AjaxFrameworkMode property can be set to the following values:</span></span>

- <span data-ttu-id="819ca-336">사용 가능--ScriptManager 컨트롤에 자동으로 모든 핵심 프레임 워크 스크립트 (레거시 동작)의 조합 된 스크립트 파일의 MicrosoftAjax.js 스크립트 파일을 포함 하는 작업을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-336">Enabled -- Specifies that the ScriptManager control automatically includes the MicrosoftAjax.js script file, which is a combined script file of every core framework script (legacy behavior).</span></span>
- <span data-ttu-id="819ca-337">사용 하지 않도록 설정-모든 Microsoft Ajax 스크립트 기능이 해제 되 고 있는지 ScriptManager 컨트롤을 참조 하지 않는 모든 스크립트를 자동으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-337">Disabled -- Specifies that all Microsoft Ajax script features are disabled and that the ScriptManager control does not reference any scripts automatically.</span></span>
- <span data-ttu-id="819ca-338">명시적-스크립트 참조 페이지에서 필요로 하는 개별 프레임 워크 코어 스크립트 파일에 있는 명시적으로 포함 되도록 하 고 각 스크립트 파일에 필요한 종속성에 대 한 참조를 포함 합니다를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-338">Explicit -- Specifies that you will explicitly include script references to individual framework core script file that your page requires, and that you will include references to the dependencies that each script file requires.</span></span>

<span data-ttu-id="819ca-339">예를 들어 AjaxFrameworkMode 속성 명시적 값을 설정 하는 경우 필요한 특정 ASP.NET Ajax 구성 요소 스크립트 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-339">For example, if you set the AjaxFrameworkMode property to the value Explicit then you can specify the particular ASP.NET Ajax component scripts that you need:</span></span>

[!code-aspx[Main](overview/samples/sample22.aspx)]

<a id="0.2__The_DataView_Control"></a><a id="0.2__The_DataContext_and"></a><a id="0.2__Refactoring_the_Microsoft"></a><a id="0.2__Toc224729032"></a><a id="0.2__Toc253429256"></a><a id="0.2__Toc243304630"></a>

## <a name="web-forms"></a><span data-ttu-id="819ca-340">Web Forms</span><span class="sxs-lookup"><span data-stu-id="819ca-340">Web Forms</span></span>

<span data-ttu-id="819ca-341">Web Forms ASP.NET 1.0의 릴리스 이후 ASP.NET의 핵심 기능은 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-341">Web Forms has been a core feature in ASP.NET since the release of ASP.NET 1.0.</span></span> <span data-ttu-id="819ca-342">다음을 포함 하는 ASP.NET 4에 대 한이 영역에서 많은 부분이 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-342">Many enhancements have been in this area for ASP.NET 4, including the following:</span></span>

- <span data-ttu-id="819ca-343">설정 하는 기능 *메타* 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-343">The ability to set *meta* tags.</span></span>
- <span data-ttu-id="819ca-344">더 자세히 제어할 뷰 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-344">More control over view state.</span></span>
- <span data-ttu-id="819ca-345">브라우저 기능에 맞게 편리 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-345">Easier ways to work with browser capabilities.</span></span>
- <span data-ttu-id="819ca-346">ASP.NET Web forms 라우팅을 사용할 수 있도록 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-346">Support for using ASP.NET routing with Web Forms.</span></span>
- <span data-ttu-id="819ca-347">생성 된 Id를 보다 자세히 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-347">More control over generated IDs.</span></span>
- <span data-ttu-id="819ca-348">데이터 컨트롤에서 선택 된 행을 유지 하는 기능.</span><span class="sxs-lookup"><span data-stu-id="819ca-348">The ability to persist selected rows in data controls.</span></span>
- <span data-ttu-id="819ca-349">렌더링 된 HTML에 보다 자세히 제어는 *FormView* 및 *ListView* 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-349">More control over rendered HTML in the *FormView* and *ListView* controls.</span></span>
- <span data-ttu-id="819ca-350">데이터 소스 제어에 대 한 지원을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-350">Filtering support for data source controls.</span></span>

<a id="0.2__Toc224729033"></a><a id="0.2__Toc253429257"></a><a id="0.2__Toc243304631"></a>

### <a name="setting-meta-tags-with-the-pagemetakeywords-and-pagemetadescription-properties"></a><span data-ttu-id="819ca-351">Page.MetaDescription 속성과 Page.MetaKeywords 함께 메타 태그를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-351">Setting Meta Tags with the Page.MetaKeywords and Page.MetaDescription Properties</span></span>

<span data-ttu-id="819ca-352">두 개의 속성을 추가 하는 ASP.NET 4는 *페이지* 클래스 *MetaKeywords* 및 *MetaDescription*합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-352">ASP.NET 4 adds two properties to the *Page* class, *MetaKeywords* and *MetaDescription*.</span></span> <span data-ttu-id="819ca-353">이러한 두 속성에 해당 나타냅니다 *메타* 다음 예제에 표시 된 대로 페이지의 태그:</span><span class="sxs-lookup"><span data-stu-id="819ca-353">These two properties represent corresponding *meta* tags in your page, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample23.aspx)]

<span data-ttu-id="819ca-354">이러한 두 속성은 동일 하 게 작동 방식으로 페이지의 *제목* 속성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-354">These two properties work the same way that the page's *Title* property does.</span></span> <span data-ttu-id="819ca-355">이러한 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-355">They follow these rules:</span></span>

1. <span data-ttu-id="819ca-356">없는 경우 없는 *메타* 태그는 *h e a d* 속성 이름과 일치 하는 요소 (즉, 이름을 "키워드" = *Page.MetaKeywords* 및 이름 = "description" 에대한 *Page.MetaDescription*, 이러한 속성을 설정 하지 않은 의미), *메타* 태그 렌더링 된 페이지에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-356">If there are no *meta* tags in the *head* element that match the property names (that is, name="keywords" for *Page.MetaKeywords* and name="description" for *Page.MetaDescription*, meaning that these properties have not been set), the *meta* tags will be added to the page when it is rendered.</span></span>
2. <span data-ttu-id="819ca-357">이미 있을 경우 *메타* 이러한 이름으로 태그를 이러한 속성 역할을 get 및 set 메서드는 기존 태그의 내용에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-357">If there are already *meta* tags with these names, these properties act as get and set methods for the contents of the existing tags.</span></span>

<span data-ttu-id="819ca-358">런타임 시 데이터베이스 또는 다른 원본에서 콘텐츠를 가져올 수 있습니다 및 대상을 설명 하는 동적으로 태그를 설정할 수 있는 이러한 속성을 설정할 수에 대 한 특정 페이지가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-358">You can set these properties at run time, which lets you get the content from a database or other source, and which lets you set the tags dynamically to describe what a particular page is for.</span></span>

<span data-ttu-id="819ca-359">설정할 수도 있습니다는 *키워드* 및 *설명* 속성에는 *@ Page* Web Forms 페이지 태그는 다음 예제 에서처럼의 예외:</span><span class="sxs-lookup"><span data-stu-id="819ca-359">You can also set the *Keywords* and *Description* properties in the *@ Page* directive at the top of the Web Forms page markup, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample24.aspx)]

<span data-ttu-id="819ca-360">이렇게 하면 무시 됩니다는 *메타* 태그 내용을 (있는 경우)의 페이지에 이미 선언 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-360">This will override the *meta* tag contents (if any) already declared in the page.</span></span>

<span data-ttu-id="819ca-361">설명의 내용을 *메타* 태그는 Google의 미리 보기를 나열 하는 검색 개선에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-361">The contents of the description *meta* tag are used for improving search listing previews in Google.</span></span> <span data-ttu-id="819ca-362">(세부 정보를 참조 하십시오. [메타 설명 변경 된 조각 개선](http://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html) Google 웹 마스터 중앙 블로그.) Google 및 Windows Live Search 사용 하지 않고 키워드의 내용을, 이외에 그 다른 검색 엔진 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-362">(For details, see [Improve snippets with a meta description makeover](http://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html) on the Google Webmaster Central blog.) Google and Windows Live Search do not use the contents of the keywords for anything, but other search engines might.</span></span> <span data-ttu-id="819ca-363">자세한 내용은 참조 [메타 키워드 조언을](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php) 검색 엔진 설명서 웹 사이트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-363">For more information, see [Meta Keywords Advice](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php) on the Search Engine Guide Web site.</span></span>

<span data-ttu-id="819ca-364">이러한 새 속성은 간단한 기능 하지만를 만드는 코드는 직접 작성 또는에서 이러한 작업을 수동으로 추가할 필요 절약 됩니다는 *메타* 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-364">These new properties are a simple feature, but they save you from the requirement to add these manually or from writing your own code to create the *meta* tags.</span></span>

<a id="0.2__Toc224729034"></a><a id="0.2__Toc253429258"></a><a id="0.2__Toc243304632"></a>

### <a name="enabling-view-state-for-individual-controls"></a><span data-ttu-id="819ca-365">개별 컨트롤의 뷰 상태 사용</span><span class="sxs-lookup"><span data-stu-id="819ca-365">Enabling View State for Individual Controls</span></span>

<span data-ttu-id="819ca-366">기본적으로 뷰 상태 페이지에 있는 각 컨트롤 응용 프로그램에 대 한 필요 하지 않은 경우에 잠재적으로 뷰 상태를 저장 하는 결과와 페이지에 대 한 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-366">By default, view state is enabled for the page, with the result that each control on the page potentially stores view state even if it is not required for the application.</span></span> <span data-ttu-id="819ca-367">뷰 상태 데이터는 페이지를 생성 하 고 페이지를 클라이언트로 전송할 다시 게시 하는 데 걸리는 시간에는 늘어나지만 태그에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-367">View state data is included in the markup that a page generates and increases the amount of time it takes to send a page to the client and post it back.</span></span> <span data-ttu-id="819ca-368">필요한 것 보다 자세한 뷰 상태가 저장 심각한 성능 저하를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-368">Storing more view state than is necessary can cause significant performance degradation.</span></span> <span data-ttu-id="819ca-369">ASP.NET의 이전 버전에서 개발자는 페이지 크기를 줄이기 위해 개별 컨트롤에 대 한 뷰 상태를 해제할 수 있습니다 하지만 개별 컨트롤에 대 한 명시적 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-369">In earlier versions of ASP.NET, developers could disable view state for individual controls in order to reduce page size, but had to do so explicitly for individual controls.</span></span> <span data-ttu-id="819ca-370">웹 서버 컨트롤에는 ASP.NET 4에서는 *ViewStateMode* 기본적으로 상태 보기를 사용 하지 않도록 설정 하 고 다음 페이지에서 필요한 컨트롤을에 사용할 수 있는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-370">In ASP.NET 4, Web server controls include a *ViewStateMode* property that lets you disable view state by default and then enable it only for the controls that require it in the page.</span></span>

<span data-ttu-id="819ca-371">*ViewStateMode* 속성은 세 가지 값을 포함 하는 열거형을 사용: *Enabled*, *비활성화*, 및 *상속*합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-371">The *ViewStateMode* property takes an enumeration that has three values: *Enabled*, *Disabled*, and *Inherit*.</span></span> <span data-ttu-id="819ca-372">*활성화* 해당 컨트롤에 대 한 설정 된 모든 자식 컨트롤에 대 한 상태 뷰 *상속* 이거나는 아무 것도 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-372">*Enabled* enables view state for that control and for any child controls that are set to *Inherit* or that have nothing set.</span></span> <span data-ttu-id="819ca-373">*사용 안 함* 뷰 상태를 사용할 수 없습니다 및 *상속* 컨트롤을 사용 하도록 지정 된 *ViewStateMode* 부모 컨트롤에서 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-373">*Disabled* disables view state, and *Inherit* specifies that the control uses the *ViewStateMode* setting from the parent control.</span></span>

<span data-ttu-id="819ca-374">다음 예제와 방법을 *ViewStateMode* 속성의 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-374">The following example shows how the *ViewStateMode* property works.</span></span> <span data-ttu-id="819ca-375">한 값을 포함 하는 태그와 다음 페이지에 있는 컨트롤에 대 한 코드는 *ViewStateMode* 속성:</span><span class="sxs-lookup"><span data-stu-id="819ca-375">The markup and code for the controls in the following page includes values for the *ViewStateMode* property:</span></span>

[!code-aspx[Main](overview/samples/sample25.aspx)]

<span data-ttu-id="819ca-376">볼 수 있듯이 코드 PlaceHolder1 컨트롤 뷰 상태를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-376">As you can see, the code disables view state for the PlaceHolder1 control.</span></span> <span data-ttu-id="819ca-377">이 속성 값이 상속 되는 자식 label1 컨트롤 (*상속* 에 대 한 기본값은 *ViewStateMode* 컨트롤에 대 한) 하 고 따라서 뷰 상태가 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-377">The child label1 control inherits this property value (*Inherit* is the default value for *ViewStateMode* for controls.) and therefore saves no view state.</span></span> <span data-ttu-id="819ca-378">PlaceHolder2 컨트롤에서 *ViewStateMode* 로 설정 되어 *사용*이므로 label2이이 속성을 상속 하 고 뷰 상태를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-378">In the PlaceHolder2 control, *ViewStateMode* is set to *Enabled*, so label2 inherits this property and saves view state.</span></span> <span data-ttu-id="819ca-379">페이지가 처음으로 로드 하는 경우는 *텍스트* 모두의 속성이 *레이블* 컨트롤 문자열 "[DynamicValue]"로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-379">When the page is first loaded, the *Text* property of both *Label* controls is set to the string "[DynamicValue]".</span></span>

<span data-ttu-id="819ca-380">이러한 설정의 효과 페이지를 처음으로 로드 하는 경우 브라우저에 다음 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-380">The effect of these settings is that when the page loads the first time, the following output is displayed in the browser:</span></span>

<span data-ttu-id="819ca-381">사용 안 함 `: [DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="819ca-381">Disabled `: [DynamicValue]`</span></span>

<span data-ttu-id="819ca-382">사용 가능:`[DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="819ca-382">Enabled:`[DynamicValue]`</span></span>

<span data-ttu-id="819ca-383">하지만 포스트백 후 다음과 같은 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-383">After a postback, however, the following output is displayed:</span></span>

<span data-ttu-id="819ca-384">사용 안 함 `: [DeclaredValue]`</span><span class="sxs-lookup"><span data-stu-id="819ca-384">Disabled `: [DeclaredValue]`</span></span>

<span data-ttu-id="819ca-385">사용 가능:`[DynamicValue]`</span><span class="sxs-lookup"><span data-stu-id="819ca-385">Enabled:`[DynamicValue]`</span></span>

<span data-ttu-id="819ca-386">Label1 컨트롤 (해당 *ViewStateMode* 값으로 설정 되어 *비활성화 된*)에서 코드 설정 된 값은 유지 되지가 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-386">The label1 control (whose *ViewStateMode* value is set to *Disabled*) has not preserved the value that it was set to in code.</span></span> <span data-ttu-id="819ca-387">그러나는 label2 제어할 (해당 *ViewStateMode* 값으로 설정 됩니다 *Enabled*)의 상태를 유지 했습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-387">However, the label2 control (whose *ViewStateMode* value is set to *Enabled*) has preserved its state.</span></span>

<span data-ttu-id="819ca-388">설정할 수도 있습니다 *ViewStateMode* 에 *@ Page* 다음 예제와 같이 지시문:</span><span class="sxs-lookup"><span data-stu-id="819ca-388">You can also set *ViewStateMode* in the *@ Page* directive, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample26.aspx)]

<span data-ttu-id="819ca-389">*페이지* 클래스는 다른 컨트롤, 역할 페이지에 있는 모든 컨트롤에 대 한 부모 컨트롤을 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-389">The *Page* class is just another control; it acts as the parent control for all the other controls in the page.</span></span> <span data-ttu-id="819ca-390">기본값 *ViewStateMode* 은 *Enabled* 에 대 한 인스턴스의 *페이지*합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-390">The default value of *ViewStateMode* is *Enabled* for instances of *Page*.</span></span> <span data-ttu-id="819ca-391">컨트롤의 기본 설정 되므로 *상속*, 컨트롤에 상속 됩니다는 *Enabled* 속성 값을 설정 하지 않으면 *ViewStateMode* 페이지 또는 제어 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-391">Because controls default to *Inherit*, controls will inherit the *Enabled* property value unless you set *ViewStateMode* at page or control level.</span></span>

<span data-ttu-id="819ca-392">값은 *ViewStateMode* 속성 결정 경우에 뷰 상태를 유지 관리 하는 경우는 *EnableViewState* 속성이로 설정 되어 *true*합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-392">The value of the *ViewStateMode* property determines if view state is maintained only if the *EnableViewState* property is set to *true*.</span></span> <span data-ttu-id="819ca-393">경우는 *EnableViewState* 속성이 *false*, 뷰 상태를 유지 하지 것입니다 경우에 *ViewStateMode* 로 설정 된 *Enabled*합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-393">If the *EnableViewState* property is set to *false*, view state will not be maintained even if *ViewStateMode* is set to *Enabled*.</span></span>

<span data-ttu-id="819ca-394">이 기능에 대 한 적절 하 게 사용 된 *ContentPlaceHolder* 을 설정할 수 있는 마스터 페이지에서 컨트롤 *ViewStateMode* 를 *비활성화* 마스터에 대 한 페이지 하 고 다음 사용 하도록 설정 에 대해 개별적으로 *ContentPlaceHolder* 차례로 필요로 하는 컨트롤을 포함 하는 컨트롤 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-394">A good use for this feature is with *ContentPlaceHolder* controls in master pages, where you can set *ViewStateMode* to *Disabled* for the master page and then enable it individually for *ContentPlaceHolder* controls that in turn contain controls that require view state.</span></span>

<a id="0.2__Toc224729035"></a><a id="0.2__Toc253429259"></a><a id="0.2__Toc243304633"></a>

### <a name="changes-to-browser-capabilities"></a><span data-ttu-id="819ca-395">브라우저 기능에 대 한 변경</span><span class="sxs-lookup"><span data-stu-id="819ca-395">Changes to Browser Capabilities</span></span>

<span data-ttu-id="819ca-396">사용자는 이라는 기능을 사용 하 여 사이트를 탐색 하는 데 사용 하는 브라우저의 기능을 결정 하는 ASP.NET *브라우저 기능*합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-396">ASP.NET determines the capabilities of the browser that a user is using to browse your site by using a feature called *browser capabilities*.</span></span> <span data-ttu-id="819ca-397">브라우저 기능으로 표시 됩니다는 *HttpBrowserCapabilities* 개체 (에 의해 노출 된 *Request.Browser* 속성).</span><span class="sxs-lookup"><span data-stu-id="819ca-397">Browser capabilities are represented by the *HttpBrowserCapabilities* object (exposed by the *Request.Browser* property).</span></span> <span data-ttu-id="819ca-398">예를 들어, 사용할 수는 *HttpBrowserCapabilities* 개체 유형 및 버전 현재 브라우저의 특정 버전의 JavaScript 지원 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-398">For example, you can use the *HttpBrowserCapabilities* object to determine whether the type and version of the current browser supports a particular version of JavaScript.</span></span> <span data-ttu-id="819ca-399">또는 사용할 수는 *HttpBrowserCapabilities* 해당 요청이 모바일 장치에서 시작 하는지 여부를 결정 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-399">Or, you can use the *HttpBrowserCapabilities* object to determine whether the request originated from a mobile device.</span></span>

<span data-ttu-id="819ca-400">*HttpBrowserCapabilities* 브라우저 정의 파일 집합에 의해 개체 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-400">The *HttpBrowserCapabilities* object is driven by a set of browser definition files.</span></span> <span data-ttu-id="819ca-401">이러한 파일의 특정 브라우저 기능에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-401">These files contain information about the capabilities of particular browsers.</span></span> <span data-ttu-id="819ca-402">ASP.NET 4에서 최근에 도입 된 브라우저 및 Google Chrome, 리서치 등 동작 BlackBerry 스마트폰 및 Apple iPhone에서 장치에 대 한 정보를 포함 하도록 이러한 브라우저 정의 파일 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-402">In ASP.NET 4, these browser definition files have been updated to contain information about recently introduced browsers and devices such as Google Chrome, Research in Motion BlackBerry smartphones, and Apple iPhone.</span></span>

<span data-ttu-id="819ca-403">다음 목록에는 새 브라우저 정의 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-403">The following list shows new browser definition files:</span></span>

- <span data-ttu-id="819ca-404">*blackberry.browser*</span><span class="sxs-lookup"><span data-stu-id="819ca-404">*blackberry.browser*</span></span>
- <span data-ttu-id="819ca-405">*chrome.browser*</span><span class="sxs-lookup"><span data-stu-id="819ca-405">*chrome.browser*</span></span>
- <span data-ttu-id="819ca-406">*Default.browser*</span><span class="sxs-lookup"><span data-stu-id="819ca-406">*Default.browser*</span></span>
- <span data-ttu-id="819ca-407">*firefox.browser*</span><span class="sxs-lookup"><span data-stu-id="819ca-407">*firefox.browser*</span></span>
- <span data-ttu-id="819ca-408">*gateway.browser*</span><span class="sxs-lookup"><span data-stu-id="819ca-408">*gateway.browser*</span></span>
- <span data-ttu-id="819ca-409">*generic.browser*</span><span class="sxs-lookup"><span data-stu-id="819ca-409">*generic.browser*</span></span>
- <span data-ttu-id="819ca-410">*ie.browser*</span><span class="sxs-lookup"><span data-stu-id="819ca-410">*ie.browser*</span></span>
- <span data-ttu-id="819ca-411">*iemobile.browser*</span><span class="sxs-lookup"><span data-stu-id="819ca-411">*iemobile.browser*</span></span>
- <span data-ttu-id="819ca-412">*iphone.browser*</span><span class="sxs-lookup"><span data-stu-id="819ca-412">*iphone.browser*</span></span>
- <span data-ttu-id="819ca-413">*opera.browser*</span><span class="sxs-lookup"><span data-stu-id="819ca-413">*opera.browser*</span></span>
- <span data-ttu-id="819ca-414">*safari.browser*</span><span class="sxs-lookup"><span data-stu-id="819ca-414">*safari.browser*</span></span>

#### <a name="using-browser-capabilities-providers"></a><span data-ttu-id="819ca-415">브라우저 기능 공급자를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="819ca-415">Using Browser Capabilities Providers</span></span>

<span data-ttu-id="819ca-416">Asp.net 버전 3.5 서비스 팩 1에서는 다음과 같은 방법으로 브라우저에 기능을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-416">In ASP.NET version 3.5 Service Pack 1, you can define the capabilities that a browser has in the following ways:</span></span>

- <span data-ttu-id="819ca-417">컴퓨터 수준에서 만들거나 업데이트 한 `.browser` 다음 폴더에 XML 파일:</span><span class="sxs-lookup"><span data-stu-id="819ca-417">At the computer level, you create or update a `.browser` XML file in the following folder:</span></span>

- [!code-console[Main](overview/samples/sample27.cmd)]

- <span data-ttu-id="819ca-418">브라우저 기능을 정의한 후 브라우저 기능 어셈블리를 다시 작성 하 고 GAC에 추가 하기 위해 Visual Studio 명령 프롬프트에서 다음 명령을 실행 하면:</span><span class="sxs-lookup"><span data-stu-id="819ca-418">After you define the browser capability, you run the following command from the Visual Studio Command Prompt in order to rebuild the browser capabilities assembly and add it to the GAC:</span></span>

- [!code-console[Main](overview/samples/sample28.cmd)]

- <span data-ttu-id="819ca-419">만드는 각 응용 프로그램에 대 한 한 `.browser` 응용 프로그램의 파일 `App_Browsers` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-419">For an individual application, you create a `.browser` file in the application's `App_Browsers` folder.</span></span>

<span data-ttu-id="819ca-420">이러한 접근 방식은 요구 XML 파일을 변경 하 고 컴퓨터 수준 변경에 대 한 다시 시작 해야 응용 프로그램 aspnet를 실행 한 후\_regbrowsers.exe 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-420">These approaches require you to change XML files, and for computer-level changes, you must restart the application after you run the aspnet\_regbrowsers.exe process.</span></span>

<span data-ttu-id="819ca-421">ASP.NET 4 라고도 하는 기능에 포함 되어 *브라우저 기능 공급자*합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-421">ASP.NET 4 includes a feature referred to as *browser capabilities providers*.</span></span> <span data-ttu-id="819ca-422">이름에서 알 수 있듯이 차례로 수 있는 공급자를 작성할 수이 있습니다 브라우저 기능을 확인 하려면 사용자 고유의 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-422">As the name suggests, this lets you build a provider that in turn lets you use your own code to determine browser capabilities.</span></span>

<span data-ttu-id="819ca-423">실제로, 개발자가 자주 정의 하지 않습니다 사용자 지정 브라우저 기능.</span><span class="sxs-lookup"><span data-stu-id="819ca-423">In practice, developers often do not define custom browser capabilities.</span></span> <span data-ttu-id="819ca-424">브라우저 파일은 프로세스를 업데이트, 업데이트 하는 매우 복잡 한 하드과 XML 구문을 `.browser` 파일을 사용 및 정의 복잡할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-424">Browser files are hard to update, the process for updating them is fairly complicated, and the XML syntax for `.browser` files can be complex to use and define.</span></span> <span data-ttu-id="819ca-425">훨씬 쉽게이 수행할 수 있도록는 어떤 일반적인 브라우저 정의 구문 있는 경우 또는 최신 브라우저 정의 또는 이러한 데이터베이스에 대 한 웹 서비스도 포함 된 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-425">What would make this process much easier is if there were a common browser definition syntax, or a database that contained up-to-date browser definitions, or even a Web service for such a database.</span></span> <span data-ttu-id="819ca-426">새 브라우저 기능 공급자 기능을 사용 하면 이러한 시나리오가 가능 하 고 유용 타사 개발자를 위한 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-426">The new browser capabilities providers feature makes these scenarios possible and practical for third-party developers.</span></span>

<span data-ttu-id="819ca-427">두 가지 주요 새로운 ASP.NET 4 브라우저 기능 공급자 기능을 사용 하기 위한: ASP.NET 브라우저 기능 정의 기능을 확장 하거나 완전히 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-427">There are two main approaches for using the new ASP.NET 4 browser capabilities provider feature: extending the ASP.NET browser capabilities definition functionality, or totally replacing it.</span></span> <span data-ttu-id="819ca-428">다음 섹션에서는 기능을 대체 하는 방법을 차례로 확장 하는 방법을 먼저 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-428">The following sections describe first how to replace the functionality, and then how to extend it.</span></span>

#### <a name="replacing-the-aspnet-browser-capabilities-functionality"></a><span data-ttu-id="819ca-429">ASP.NET 브라우저 기능 기능 대체</span><span class="sxs-lookup"><span data-stu-id="819ca-429">Replacing the ASP.NET Browser Capabilities Functionality</span></span>

<span data-ttu-id="819ca-430">ASP.NET 브라우저 기능 정의 기능을 완전히 대체 하려면 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="819ca-430">To replace the ASP.NET browser capabilities definition functionality completely, follow these steps:</span></span>

1. <span data-ttu-id="819ca-431">파생 되는 공급자 클래스를 만듭니다 *HttpCapabilitiesProvider* 를 재정의 *GetBrowserCapabilities* 다음 예제와 같이 메서드:</span><span class="sxs-lookup"><span data-stu-id="819ca-431">Create a provider class that derives from *HttpCapabilitiesProvider* and that overrides the *GetBrowserCapabilities* method, as in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample29.cs)]

    <span data-ttu-id="819ca-432">이 예제의 코드에서는 새 *HttpBrowserCapabilities* 개체만 명명 된 브라우저 및 MyCustomBrowser에 해당 기능을 설정 하는 기능을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-432">The code in this example creates a new *HttpBrowserCapabilities* object, specifying only the capability named browser and setting that capability to MyCustomBrowser.</span></span>
2. <span data-ttu-id="819ca-433">응용 프로그램에서 공급자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-433">Register the provider with the application.</span></span> 

    <span data-ttu-id="819ca-434">응용 프로그램으로 공급자를 사용 하려면 추가 해야 합니다는 *공급자* 특성을 *browserCaps* 섹션은 `Web.config` 또는 `Machine.config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-434">In order to use a provider with an application, you must add the *provider* attribute to the *browserCaps* section in the `Web.config` or `Machine.config` files.</span></span> <span data-ttu-id="819ca-435">(공급자 특성을 정의할 수 있습니다는 *위치* 특정 모바일 장치에 대 한 폴더와 같이 응용 프로그램에서 특정 디렉터리에 대 한 요소입니다.) 설정 하는 방법을 보여 주는 다음 예제는 *공급자* 구성 파일의 특성:</span><span class="sxs-lookup"><span data-stu-id="819ca-435">(You can also define the provider attributes in a *location* element for specific directories in application, such as in a folder for a specific mobile device.) The following example shows how to set the *provider* attribute in a configuration file:</span></span>

    [!code-xml[Main](overview/samples/sample30.xml)]

    <span data-ttu-id="819ca-436">다음 예제에 표시 된 것과 같이 코드를 사용 하 여 새 브라우저 기능 정의 등록 하는 다른 방법은입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-436">Another way to register the new browser capability definition is to use code, as shown in the following example:</span></span>

    [!code-csharp[Main](overview/samples/sample31.cs)]

    <span data-ttu-id="819ca-437">이 코드 실행 해야 합니다는 *응용 프로그램\_시작* 의 이벤트는 `Global.asax` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-437">This code must run in the *Application\_Start* event of the `Global.asax` file.</span></span> <span data-ttu-id="819ca-438">변경 된 *BrowserCapabilitiesProvider* 클래스는 캐시는 적용 된에 대 한 유효한 상태 유지 하는지 확인 하기 위해 응용 프로그램의 모든 코드를 실행 하기 전에 발생 해야 *HttpCapabilitiesBase* 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-438">Any change to the *BrowserCapabilitiesProvider* class must occur before any code in the application executes, in order to make sure that the cache remains in a valid state for the resolved *HttpCapabilitiesBase* object.</span></span>

#### <a name="caching-the-httpbrowsercapabilities-object"></a><span data-ttu-id="819ca-439">HttpBrowserCapabilities 개체 캐싱</span><span class="sxs-lookup"><span data-stu-id="819ca-439">Caching the HttpBrowserCapabilities Object</span></span>

<span data-ttu-id="819ca-440">앞의 예제 코드는 얻기 위해 사용자 지정 공급자를 호출할 때마다 실행 하는 한 가지 문제에는 *HttpBrowserCapabilities* 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-440">The preceding example has one problem, which is that the code would run each time the custom provider is invoked in order to get the *HttpBrowserCapabilities* object.</span></span> <span data-ttu-id="819ca-441">각 요청 하는 동안 여러 번 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-441">This can happen multiple times during each request.</span></span> <span data-ttu-id="819ca-442">예제에서는 공급자에 대 한 코드는 하지 효과가 그다지 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-442">In the example, the code for the provider does not do much.</span></span> <span data-ttu-id="819ca-443">그러나 사용자 지정 공급자의 코드에서 많은 작업을 수행 하는 경우를 얻기 위해는 *HttpBrowserCapabilities* 개체 성능에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-443">However, if the code in your custom provider performs significant work in order to get the *HttpBrowserCapabilities* object, this can affect performance.</span></span> <span data-ttu-id="819ca-444">이 방지 하기를 캐시할 수 있습니다는 *HttpBrowserCapabilities* 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-444">To prevent this from happening, you can cache the *HttpBrowserCapabilities* object.</span></span> <span data-ttu-id="819ca-445">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-445">Follow these steps:</span></span>

1. <span data-ttu-id="819ca-446">파생 되는 클래스를 만듭니다 *HttpCapabilitiesProvider*, 다음 예제에서와 같은:</span><span class="sxs-lookup"><span data-stu-id="819ca-446">Create a class that derives from *HttpCapabilitiesProvider*, like the one in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample32.cs)]

    <span data-ttu-id="819ca-447">예제에서는 코드는 사용자 지정 BuildCacheKey 메서드를 호출 하 여 캐시 키를 생성 하 고 사용자 지정 GetCacheTime 메서드를 호출 하 여 캐시에 있는 시간의 길이 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-447">In the example, the code generates a cache key by calling a custom BuildCacheKey method, and it gets the length of time to cache by calling a custom GetCacheTime method.</span></span> <span data-ttu-id="819ca-448">그런 다음 추가 코드는 적용 된 *HttpBrowserCapabilities* 개체를 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-448">The code then adds the resolved *HttpBrowserCapabilities* object to the cache.</span></span> <span data-ttu-id="819ca-449">개체를 캐시에서 검색 및에서 다시 사용할 수 있도록 후속 요청은 사용자 지정 공급자의 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-449">The object can be retrieved from the cache and reused on subsequent requests that make use of the custom provider.</span></span>
2. <span data-ttu-id="819ca-450">앞의 절차에 설명 된 대로 응용 프로그램과 함께 공급자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-450">Register the provider with the application as described in the preceding procedure.</span></span>

#### <a name="extending-aspnet-browser-capabilities-functionality"></a><span data-ttu-id="819ca-451">ASP.NET 브라우저 기능 기능 확장</span><span class="sxs-lookup"><span data-stu-id="819ca-451">Extending ASP.NET Browser Capabilities Functionality</span></span>

<span data-ttu-id="819ca-452">이전 섹션에 새 하는 방법을 설명 *HttpBrowserCapabilities* ASP.NET 4에는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-452">The previous section described how to create a new *HttpBrowserCapabilities* object in ASP.NET 4.</span></span> <span data-ttu-id="819ca-453">또한 ASP.NET에 이미 있는 새 브라우저 기능 정의 추가 하 여 ASP.NET 브라우저 기능 기능을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-453">You can also extend the ASP.NET browser capabilities functionality by adding new browser capabilities definitions to those that are already in ASP.NET.</span></span> <span data-ttu-id="819ca-454">XML 브라우저 정의 사용 하지 않고이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-454">You can do this without using the XML browser definitions.</span></span> <span data-ttu-id="819ca-455">다음 절차에 표시 된 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-455">The following procedure shows how.</span></span>

1. <span data-ttu-id="819ca-456">파생 되는 클래스를 만듭니다 *HttpCapabilitiesEvaluator* 를 재정의 *GetBrowserCapabilities* 메서드를 다음 예제와 같이:</span><span class="sxs-lookup"><span data-stu-id="819ca-456">Create a class that derives from *HttpCapabilitiesEvaluator* and that overrides the *GetBrowserCapabilities* method, as shown in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample33.cs)]

    <span data-ttu-id="819ca-457">이 코드는 먼저 브라우저를 식별 하려면 ASP.NET 브라우저 기능 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-457">This code first uses the ASP.NET browser capabilities functionality to try to identify the browser.</span></span> <span data-ttu-id="819ca-458">그러나 브라우저가 없으므로 식별 되는 경우에 따라 요청에 정의 되어 있는 정보 (즉는 *브라우저* 속성은 *HttpBrowserCapabilities* 개체는 "알 수 없음" 문자열), 코드 호출 사용자 지정 공급자 (MyBrowserCapabilitiesEvaluator) 브라우저를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-458">However, if no browser is identified based on the information defined in the request (that is, if the *Browser* property of the *HttpBrowserCapabilities* object is the string "Unknown"), the code calls the custom provider (MyBrowserCapabilitiesEvaluator) to identify the browser.</span></span>
2. <span data-ttu-id="819ca-459">앞의 예제에 설명 된 대로 응용 프로그램과 함께 공급자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-459">Register the provider with the application as described in the previous example.</span></span>

#### <a name="extending-browser-capabilities-functionality-by-adding-new-capabilities-to-existing-capabilities-definitions"></a><span data-ttu-id="819ca-460">기존 기능 정의에 새로운 기능을 추가 하 여 브라우저 기능 기능 확장</span><span class="sxs-lookup"><span data-stu-id="819ca-460">Extending Browser Capabilities Functionality by Adding New Capabilities to Existing Capabilities Definitions</span></span>

<span data-ttu-id="819ca-461">사용자 지정 브라우저 정의 공급자를 만들 뿐만 아니라 및 새 브라우저 정의 동적으로 만드는 추가 기능을 가진 기존 브라우저 정의 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-461">In addition to creating a custom browser definition provider and to dynamically creating new browser definitions, you can extend existing browser definitions with additional capabilities.</span></span> <span data-ttu-id="819ca-462">이 대상에 근접 하는 있지만 몇 가지 기능만 없는 하는 정의 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-462">This lets you use a definition that is close to what you want but lacks only a few capabilities.</span></span> <span data-ttu-id="819ca-463">이렇게 하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-463">To do this, use the following steps.</span></span>

1. <span data-ttu-id="819ca-464">파생 되는 클래스를 만듭니다 *HttpCapabilitiesEvaluator* 를 재정의 *GetBrowserCapabilities* 메서드를 다음 예제와 같이:</span><span class="sxs-lookup"><span data-stu-id="819ca-464">Create a class that derives from *HttpCapabilitiesEvaluator* and that overrides the *GetBrowserCapabilities* method, as shown in the following example:</span></span> 

    [!code-csharp[Main](overview/samples/sample34.cs)]

    <span data-ttu-id="819ca-465">예제 코드를 확장 하는 기존 ASP.NET *HttpCapabilitiesEvaluator* 클래스 및 가져옵니다는 *HttpBrowserCapabilities* 다음 코드를 사용 하 여 현재 요청 정의 일치 하는 개체 :</span><span class="sxs-lookup"><span data-stu-id="819ca-465">The example code extends the existing ASP.NET *HttpCapabilitiesEvaluator* class and gets the *HttpBrowserCapabilities* object that matches the current request definition by using the following code:</span></span>

    [!code-csharp[Main](overview/samples/sample35.cs)]

    <span data-ttu-id="819ca-466">다음 코드는 추가 하거나이 브라우저에 대 한 기능을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-466">The code can then add or modify a capability for this browser.</span></span> <span data-ttu-id="819ca-467">새 브라우저 기능을 지정 하는 방법은 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-467">There are two ways to specify a new browser capability:</span></span>

    - <span data-ttu-id="819ca-468">에 키/값 쌍을 추가 *IDictionary* 의해 노출 되는 개체는 *기능* 의 속성은 *HttpCapabilitiesBase* 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-468">Add a key/value pair to the *IDictionary* object that is exposed by the *Capabilities* property of the *HttpCapabilitiesBase* object.</span></span> <span data-ttu-id="819ca-469">코드는 이전 예에서 다중 터치의 값이 지정 하는 기능을 추가 *true*합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-469">In the previous example, the code adds a capability named MultiTouch with a value of *true*.</span></span>
    - <span data-ttu-id="819ca-470">기존 속성을 설정는 *HttpCapabilitiesBase* 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-470">Set existing properties of the *HttpCapabilitiesBase* object.</span></span> <span data-ttu-id="819ca-471">이전 예제에서 코드에서는 설정 된 *프레임* 속성을 *true*합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-471">In the previous example, the code sets the *Frames* property to *true*.</span></span> <span data-ttu-id="819ca-472">이 속성은 대 한 접근자는 *IDictionary* 의해 노출 되는 개체는 *기능* 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-472">This property is simply an accessor for the *IDictionary* object that is exposed by the *Capabilities* property.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="819ca-473">이 모델의 모든 속성에 적용 됩니다. *HttpBrowserCapabilities*, 컨트롤 어댑터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-473">Note This model applies to any property of *HttpBrowserCapabilities*, including control adapters.</span></span>
2. <span data-ttu-id="819ca-474">이전 절차에서 설명한 대로 응용 프로그램과 함께 공급자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-474">Register the provider with the application as described in the earlier procedure.</span></span>

<a id="0.2__Toc224729036"></a><a id="0.2__Toc253429260"></a><a id="0.2__Toc243304634"></a>

### <a name="routing-in-aspnet-4"></a><span data-ttu-id="819ca-475">ASP.NET 4에서에서의 라우팅</span><span class="sxs-lookup"><span data-stu-id="819ca-475">Routing in ASP.NET 4</span></span>

<span data-ttu-id="819ca-476">ASP.NET 4 Web forms 라우팅을 사용 하 여에 대 한 기본 제공 지원을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-476">ASP.NET 4 adds built-in support for using routing with Web Forms.</span></span> <span data-ttu-id="819ca-477">라우팅에서는 허용 하도록 응용 프로그램을 구성할 수 요청 Url에서 물리적 파일에 매핑되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-477">Routing lets you configure an application to accept request URLs that do not map to physical files.</span></span> <span data-ttu-id="819ca-478">대신, 라우팅 Url을 사용자에 게 의미 이며 응용 프로그램에 대 한 검색 엔진 최적화 (SEO) 도움이 될 수 있는 정의를 사용할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-478">Instead, you can use routing to define URLs that are meaningful to users and that can help with search-engine optimization (SEO) for your application.</span></span> <span data-ttu-id="819ca-479">예를 들어 다음 예제에서는 같은 기존 응용 프로그램에 제품 범주를 표시 하는 페이지에 대 한 URL 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-479">For example, the URL for a page that displays product categories in an existing application might look like the following example:</span></span>

[!code-console[Main](overview/samples/sample36.cmd)]

<span data-ttu-id="819ca-480">라우팅를 사용 하 여 동일한 정보를 렌더링할 URL을 허용 하도록 응용 프로그램을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-480">By using routing, you can configure the application to accept the following URL to render the same information:</span></span>

[!code-console[Main](overview/samples/sample37.cmd)]

<span data-ttu-id="819ca-481">라우팅 ASP.NET 3.5 s p 1부터 제공 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-481">Routing has been available starting with ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="819ca-482">(ASP.NET 3.5 s p 1의 라우팅을 사용 하는 방법의 예를 들어 항목을 참조 하십시오. [WebForms와 라우팅를 사용 하 여](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "이 항목의 제목입니다.")</span><span class="sxs-lookup"><span data-stu-id="819ca-482">(For an example of how to use routing in ASP.NET 3.5 SP1, see the entry [Using Routing With WebForms](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "Title of this entry.")</span></span> <span data-ttu-id="819ca-483">Phil Haack의 블로그에서.) 그러나 ASP.NET 4는 다음과 같은 기능 라우팅에 사용 하기 쉽도록을 포함:</span><span class="sxs-lookup"><span data-stu-id="819ca-483">on Phil Haack's blog.) However, ASP.NET 4 includes some features that make it easier to use routing, including the following:</span></span>

- <span data-ttu-id="819ca-484">*PageRouteHandler* 클래스 경로 정의할 때 사용 하는 간단한 HTTP 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-484">The *PageRouteHandler* class, which is a simple HTTP handler that you use when you define routes.</span></span> <span data-ttu-id="819ca-485">클래스에 라우팅 된다고 요청 하는 페이지에 데이터를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-485">The class passes data to the page that the request is routed to.</span></span>
- <span data-ttu-id="819ca-486">새 속성 *HttpRequest.RequestContext* 및 *Page.RouteData* (변수인에 대 한 프록시는 *HttpRequest.RequestContext.RouteData* 개체).</span><span class="sxs-lookup"><span data-stu-id="819ca-486">The new properties *HttpRequest.RequestContext* and *Page.RouteData* (which is a proxy for the *HttpRequest.RequestContext.RouteData* object).</span></span> <span data-ttu-id="819ca-487">이러한 속성 쉽게 경로에서 전달 되는 정보에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-487">These properties make it easier to access information that is passed from the route.</span></span>
- <span data-ttu-id="819ca-488">다음과 같은 새 식 작성기에에 정의 된 *System.Web.Compilation.RouteUrlExpressionBuilder* 및 *System.Web.Compilation.RouteValueExpressionBuilder*:</span><span class="sxs-lookup"><span data-stu-id="819ca-488">The following new expression builders, which are defined in *System.Web.Compilation.RouteUrlExpressionBuilder* and *System.Web.Compilation.RouteValueExpressionBuilder*:</span></span>
- <span data-ttu-id="819ca-489">*RouteUrl*, ASP.NET 서버 컨트롤 내에서 경로 URL에 해당 하는 URL을 만드는 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-489">*RouteUrl*, which provides a simple way to create a URL that corresponds to a route URL within an ASP.NET server control.</span></span>
- <span data-ttu-id="819ca-490">*RouteValue*에서 정보를 추출 하는 간단한 방법을 제공 하는 *RouteContext* 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-490">*RouteValue*, which provides a simple way to extract information from the *RouteContext* object.</span></span>
- <span data-ttu-id="819ca-491">*RouteParameter* 쉽게에 포함 된 데이터를 전달 하는 클래스는 *RouteContext* 개체 데이터 소스 제어에 대 한 쿼리를 (비슷합니다 [ *FormParameter* ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)).</span><span class="sxs-lookup"><span data-stu-id="819ca-491">The *RouteParameter* class, which makes it easier to pass data contained in a *RouteContext* object to a query for a data source control (similar to [*FormParameter*](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)).</span></span>

#### <a name="routing-for-web-forms-pages"></a><span data-ttu-id="819ca-492">Web Forms 페이지에 대 한 라우팅</span><span class="sxs-lookup"><span data-stu-id="819ca-492">Routing for Web Forms Pages</span></span>

<span data-ttu-id="819ca-493">다음 예제에서는 new를 사용 하 여 Web Forms 경로 정의 하는 방법을 보여 줍니다. *MapPageRoute* 의 메서드는 *경로* 클래스:</span><span class="sxs-lookup"><span data-stu-id="819ca-493">The following example shows how to define a Web Forms route by using the new *MapPageRoute* method of the *Route* class:</span></span>

[!code-csharp[Main](overview/samples/sample38.cs)]

<span data-ttu-id="819ca-494">ASP.NET 4에 도입 된 *MapPageRoute* 메서드.</span><span class="sxs-lookup"><span data-stu-id="819ca-494">ASP.NET 4 introduces the *MapPageRoute* method.</span></span> <span data-ttu-id="819ca-495">다음 예제에서는 이전 예에서 같이 SearchRoute 정의에 해당 하지만 사용 하 여는 *PageRouteHandler* 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-495">The following example is equivalent to the SearchRoute definition shown in the previous example, but uses the *PageRouteHandler* class.</span></span>

[!code-csharp[Main](overview/samples/sample39.cs)]

<span data-ttu-id="819ca-496">예제에서 코드에서는 물리적 페이지에 경로 매핑합니다 (첫 번째 경로에서 `~/search.aspx`).</span><span class="sxs-lookup"><span data-stu-id="819ca-496">The code in the example maps the route to a physical page (in the first route, to `~/search.aspx`).</span></span> <span data-ttu-id="819ca-497">첫 번째 경로 정의는 또한 매개 변수에 지정 하려면 URL에서 추출 하는 페이지에 전달 하 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-497">The first route definition also specifies that the parameter named searchterm should be extracted from the URL and passed to the page.</span></span>

<span data-ttu-id="819ca-498">*MapPageRoute* 메서드는 다음 메서드 오버 로드를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-498">The *MapPageRoute* method supports the following method overloads:</span></span>

- <span data-ttu-id="819ca-499">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess)*</span><span class="sxs-lookup"><span data-stu-id="819ca-499">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess)*</span></span>
- <span data-ttu-id="819ca-500">*MapPageRoute (문자열 routeName, 문자열 routeUrl, physicalFile string, bool checkPhysicalUrlAccess, RouteValueDictionary 기본값)*</span><span class="sxs-lookup"><span data-stu-id="819ca-500">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary defaults)*</span></span>
- <span data-ttu-id="819ca-501">*MapPageRoute (문자열 routeName, 문자열 routeUrl, 문자열 physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary 기본값, RouteValueDictionary 제약 조건)*</span><span class="sxs-lookup"><span data-stu-id="819ca-501">*MapPageRoute(string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary defaults, RouteValueDictionary constraints)*</span></span>

<span data-ttu-id="819ca-502">*checkPhysicalUrlAccess* 매개 변수를 경로 라우팅이 물리적 페이지에 대 한 보안 권한을 확인 해야 하는지 여부를 지정 (이 경우 search.aspx)와 받는 URL에 대 한 권한을 (이 경우 검색 / {지정 하려면}).</span><span class="sxs-lookup"><span data-stu-id="819ca-502">The *checkPhysicalUrlAccess* parameter specifies whether the route should check the security permissions for the physical page being routed to (in this case, search.aspx) and the permissions on the incoming URL (in this case, search/{searchterm}).</span></span> <span data-ttu-id="819ca-503">하는 경우의 값 *checkPhysicalUrlAccess* 은 *false*, 받는 URL의 사용 권한만 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-503">If the value of *checkPhysicalUrlAccess* is *false*, only the permissions of the incoming URL will be checked.</span></span> <span data-ttu-id="819ca-504">이러한 사용 권한은에 정의 된는 `Web.config` 에서는 다음과 같은 설정을 사용 하 여 파일:</span><span class="sxs-lookup"><span data-stu-id="819ca-504">These permissions are defined in the `Web.config` file using settings such as the following:</span></span>

[!code-xml[Main](overview/samples/sample40.xml)]

<span data-ttu-id="819ca-505">물리적 페이지에 액세스가 거부 되 구성 예에서는 `search.aspx` 관리자 역할에 있는 것을 제외한 모든 사용자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-505">In the example configuration, access is denied to the physical page `search.aspx` for all users except those who are in the admin role.</span></span> <span data-ttu-id="819ca-506">경우는 *checkPhysicalUrlAccess* 로 설정 된 *true* (기본값) 인 관리자가 사용자만 액세스할 수 있습니다 {지정 하려면} URL /search/ 물리적 페이지 search.aspx 이므로 해당 역할의 사용자가 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-506">When the *checkPhysicalUrlAccess* parameter is set to *true* (which is its default value), only admin users are allowed to access the URL /search/{searchterm}, because the physical page search.aspx is restricted to users in that role.</span></span> <span data-ttu-id="819ca-507">경우 *checkPhysicalUrlAccess* 로 설정 된 *false* 앞의 예제와 같이 사이트를 구성 하 고, 모든 인증 된 사용자가 URL /search/ {지정 하려면} 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-507">If *checkPhysicalUrlAccess* is set to *false* and the site is configured as shown in the previous example, all authenticated users are allowed to access the URL /search/{searchterm}.</span></span>

#### <a name="reading-routing-information-in-a-web-forms-page"></a><span data-ttu-id="819ca-508">Web Forms 페이지에서 라우팅 정보 읽기</span><span class="sxs-lookup"><span data-stu-id="819ca-508">Reading Routing Information in a Web Forms Page</span></span>

<span data-ttu-id="819ca-509">Web Forms 물리적 페이지의 코드에서는 URL 라우팅을 추출에 정보에 액세스할 수 있습니다 (또는 다른 개체를 추가 하는 기타 정보는 *RouteData* 개체) 두 가지 새 속성을 사용 하 여:  *HttpRequest.RequestContext* 및 *Page.RouteData*합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-509">In the code of the Web Forms physical page, you can access the information that routing has extracted from the URL (or other information that another object has added to the *RouteData* object) by using two new properties: *HttpRequest.RequestContext* and *Page.RouteData*.</span></span> <span data-ttu-id="819ca-510">(*Page.RouteData* 래핑합니다 *HttpRequest.RequestContext.RouteData*.) 다음 예제에서는 사용 하는 방법을 보여 줍니다. *Page.RouteData*합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-510">(*Page.RouteData* wraps *HttpRequest.RequestContext.RouteData*.) The following example shows how to use *Page.RouteData*.</span></span>

[!code-csharp[Main](overview/samples/sample41.cs)]

<span data-ttu-id="819ca-511">이전 예제에서는 경로에 정의 된 대로 지정 하려면 매개 변수에 대해 전달 된 값을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-511">The code extracts the value that was passed for the searchterm parameter, as defined in the example route earlier.</span></span> <span data-ttu-id="819ca-512">다음 요청 URL을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-512">Consider the following request URL:</span></span>

[!code-console[Main](overview/samples/sample42.cmd)]

<span data-ttu-id="819ca-513">때이 요청이 "scott" 있기에서 렌더링 단어는 `search.aspx` 페이지.</span><span class="sxs-lookup"><span data-stu-id="819ca-513">When this request is made, the word "scott" would be rendered in the `search.aspx` page.</span></span>

#### <a name="accessing-routing-information-in-markup"></a><span data-ttu-id="819ca-514">태그의 라우팅 정보에 액세스</span><span class="sxs-lookup"><span data-stu-id="819ca-514">Accessing Routing Information in Markup</span></span>

<span data-ttu-id="819ca-515">이전 섹션에서 설명 하는 방법을 Web Forms 페이지의 코드에서 경로 데이터를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-515">The method described in the previous section shows how to get route data in code in a Web Forms page.</span></span> <span data-ttu-id="819ca-516">또한 태그에서 같은 정보에 액세스 권한을 제공 하는 식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-516">You can also use expressions in markup that give you access to the same information.</span></span> <span data-ttu-id="819ca-517">식 작성기는 선언적 코드를 사용 하는 강력 하 고 세련 된 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-517">Expression builders are a powerful and elegant way to work with declarative code.</span></span> <span data-ttu-id="819ca-518">(자세한 내용은 항목을 참조 하십시오. [Express 직접와 사용자 지정 식 작성기](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx) Phil Haack의 블로그에서.)</span><span class="sxs-lookup"><span data-stu-id="819ca-518">(For more information, see the entry [Express Yourself With Custom Expression Builders](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx) on Phil Haack's blog.)</span></span>

<span data-ttu-id="819ca-519">ASP.NET 4 Web Forms 라우팅에 대 한 두 명의 새 식 작성기 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-519">ASP.NET 4 includes two new expression builders for Web Forms routing.</span></span> <span data-ttu-id="819ca-520">다음 예제에서는 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-520">The following example shows how to use them.</span></span>

[!code-aspx[Main](overview/samples/sample43.aspx)]

<span data-ttu-id="819ca-521">예제에서는 *RouteUrl* 식은 경로 매개 변수를 기반으로 하는 URL을 정의 하는데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-521">In the example, the *RouteUrl* expression is used to define a URL that is based on a route parameter.</span></span> <span data-ttu-id="819ca-522">이 태그에 전체 URL 하드 코딩 하지 않아도 절감 하 고이 링크의 모든 변경 내용이 필요 없이 나중에 URL의 구조를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-522">This saves you from having to hard-code the complete URL into the markup, and lets you change the URL structure later without requiring any change to this link.</span></span>

<span data-ttu-id="819ca-523">이 태그 앞에서 정의한 경로에 따라, 다음 URL을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-523">Based on the route defined earlier, this markup generates the following URL:</span></span>

[!code-console[Main](overview/samples/sample44.cmd)]

<span data-ttu-id="819ca-524">ASP.NET이 자동으로 올바른 경로 작동 (즉, 올바른 URL 생성) 입력된 매개 변수를 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-524">ASP.NET automatically works out the correct route (that is, it generates the correct URL) based on the input parameters.</span></span> <span data-ttu-id="819ca-525">사용에 대 한 경로 지정할 수 있도록 하는 식에서 경로 이름을 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-525">You can also include a route name in the expression, which lets you specify a route to use.</span></span>

<span data-ttu-id="819ca-526">사용 하는 방법을 보여 주는 다음 예제는 *RouteValue* 식입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-526">The following example shows how to use the *RouteValue* expression.</span></span>

[!code-aspx[Main](overview/samples/sample45.aspx)]

<span data-ttu-id="819ca-527">이 컨트롤을 포함 하는 페이지를 실행 하는 경우 값 "scott" 레이블에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-527">When the page that contains this control runs, the value "scott" is displayed in the label.</span></span>

<span data-ttu-id="819ca-528">*RouteValue* 식을 사용 하면 쉽게 태그에서 경로 데이터를 사용할 수 있으며 더 복잡 한 Page.RouteData["x을 고치지 사용 되지 않습니다"] 태그에는 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-528">The *RouteValue* expression makes it simple to use route data in markup, and it avoids having to work with the more complex Page.RouteData["x"] syntax in markup.</span></span>

#### <a name="using-route-data-for-data-source-control-parameters"></a><span data-ttu-id="819ca-529">데이터 소스 제어 매개 변수에 대 한 경로 데이터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="819ca-529">Using Route Data for Data Source Control Parameters</span></span>

<span data-ttu-id="819ca-530">*RouteParameter* 클래스를 사용 하면 데이터 소스 제어에서 쿼리에 대 한 매개 변수 값으로 경로 데이터를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-530">The *RouteParameter* class lets you specify route data as a parameter value for queries in a data source control.</span></span> <span data-ttu-id="819ca-531">그 [작동과 거의 동일한는](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx) 다음 예제와 같이 클래스:</span><span class="sxs-lookup"><span data-stu-id="819ca-531">It [works much like the](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx) class, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample46.aspx)]

<span data-ttu-id="819ca-532">경로 매개 변수 지정 하려면 값에 사용할 경우에 @companyname 에서 매개 변수는 <em>선택</em> 문.</span><span class="sxs-lookup"><span data-stu-id="819ca-532">In this case, the value of the route parameter searchterm will be used for the @companyname parameter in the <em>Select</em> statement.</span></span>

<a id="0.2__Toc224729037"></a><a id="0.2__Toc253429261"></a><a id="0.2__Toc243304635"></a>

### <a name="setting-client-ids"></a><span data-ttu-id="819ca-533">클라이언트 Id 설정</span><span class="sxs-lookup"><span data-stu-id="819ca-533">Setting Client IDs</span></span>

<span data-ttu-id="819ca-534">새 *ClientIDMode* asp.net에서 오래 된 문제를 해결 하는 속성 즉 만들려면 어떻게 해야 컨트롤은 *id* 렌더링 하는 요소에 대 한 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-534">The new *ClientIDMode* property addresses a long-standing issue in ASP.NET, namely how controls create the *id* attribute for elements that they render.</span></span> <span data-ttu-id="819ca-535">알고 있으면는 *id* 렌더링 된 요소에 대 한 특성은 응용 프로그램이 이러한 요소를 참조 하는 클라이언트 스크립트를 포함 하는 경우에 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-535">Knowing the *id* attribute for rendered elements is important if your application includes client script that references these elements.</span></span>

<span data-ttu-id="819ca-536">*id* 웹 서버 컨트롤에 대 한 렌더링 된 html에서 특성에 따라 생성 되는 *ClientID* 컨트롤의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-536">The *id* attribute in HTML that is rendered for Web server controls is generated based on the *ClientID* property of the control.</span></span> <span data-ttu-id="819ca-537">ASP.NET 4를 생성 하기 위한 알고리즘까지는 *id* 에서 특성의 *ClientID* 속성 ID로, 및 (에서 같이 반복 된 컨트롤의 경우 (있는 경우)의 명명 컨테이너를 연결 하는 것 이었습니다 데이터 컨트롤)는 접두사와 일련 번호를 추가 하려면.</span><span class="sxs-lookup"><span data-stu-id="819ca-537">Until ASP.NET 4, the algorithm for generating the *id* attribute from the *ClientID* property has been to concatenate the naming container (if any) with the ID, and in the case of repeated controls (as in data controls), to add a prefix and a sequential number.</span></span> <span data-ttu-id="819ca-538">이 페이지에 컨트롤의 Id는 고유 보장 항상, 동안 알고리즘은 예측 가능 값과 클라이언트 스크립트에서 참조 하기 어려웠습니다 따라서 되는 컨트롤 Id로 인해 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-538">While this has always guaranteed that the IDs of controls in the page are unique, the algorithm has resulted in control IDs that were not predictable, and were therefore difficult to reference in client script.</span></span>

<span data-ttu-id="819ca-539">새 *ClientIDMode* 속성을 사용 하면 클라이언트 ID 컨트롤에 대해 생성 되는 방식을 보다 정확 하 게 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-539">The new *ClientIDMode* property lets you specify more precisely how the client ID is generated for controls.</span></span> <span data-ttu-id="819ca-540">설정할 수 있습니다는 *ClientIDMode* 속성 페이지에 대 한 포함 하는 모든 컨트롤에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-540">You can set the *ClientIDMode* property for any control, including for the page.</span></span> <span data-ttu-id="819ca-541">가능한 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-541">Possible settings are the following:</span></span>

- <span data-ttu-id="819ca-542">*AutoID* – 생성 하기 위한 알고리즘을 동일 *ClientID* 이전 버전의 ASP.NET에서 사용 된 속성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-542">*AutoID* – This is equivalent to the algorithm for generating *ClientID* property values that was used in earlier versions of ASP.NET.</span></span>
- <span data-ttu-id="819ca-543">*정적* –이 지정 하는 *ClientID* 값 부모 명명 컨테이너의 Id를 연결 하지 않고 ID와 동일 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-543">*Static* – This specifies that the *ClientID* value will be the same as the ID without concatenating the IDs of parent naming containers.</span></span> <span data-ttu-id="819ca-544">이 웹 사용자 컨트롤에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-544">This can be useful in Web user controls.</span></span> <span data-ttu-id="819ca-545">웹 사용자 정의 컨트롤 일 수 있으므로 서로 다른 페이지와 다른 컨테이너 컨트롤에서 사용 하는 컨트롤에 대 한 클라이언트 스크립트를 작성 하기 어려울 수 있습니다는 *AutoID* 알고리즘 됩니다 ID 값을 예측할 수 없으므로 .</span><span class="sxs-lookup"><span data-stu-id="819ca-545">Because a Web user control can be located on different pages and in different container controls, it can be difficult to write client script for controls that use the *AutoID* algorithm because you cannot predict what the ID values will be.</span></span>
- <span data-ttu-id="819ca-546">*예측 가능한* –이 옵션은 반복 템플릿을 사용 하는 데이터 컨트롤에서 사용 하기 위해 주로 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-546">*Predictable* – This option is primarily for use in data controls that use repeating templates.</span></span> <span data-ttu-id="819ca-547">하지만 생성 된 컨트롤의 명명 컨테이너의 ID 속성을 연결 *ClientID* 값 "ctlxxx"과 같은 문자열에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-547">It concatenates the ID properties of the control's naming containers, but generated *ClientID* values do not contain strings like "ctlxxx".</span></span> <span data-ttu-id="819ca-548">이 설정은와 함께 작동 하는 *ClientIDRowSuffix* 컨트롤의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-548">This setting works in conjunction with the *ClientIDRowSuffix* property of the control.</span></span> <span data-ttu-id="819ca-549">설정한는 *ClientIDRowSuffix* 생성 된 항목에 대 한 속성 데이터 필드의 이름 및 해당 필드의 값을 접미사로 사용할 *ClientID* 값입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-549">You set the *ClientIDRowSuffix* property to the name of a data field, and the value of that field is used as the suffix for the generated *ClientID* value.</span></span> <span data-ttu-id="819ca-550">로 데이터 레코드의 기본 키를 사용는 일반적으로 *ClientIDRowSuffix* 값입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-550">Typically you would use the primary key of a data record as the *ClientIDRowSuffix* value.</span></span>
- <span data-ttu-id="819ca-551">*상속* –이 설정은 컨트롤에 대 한 기본 동작으로, 컨트롤의 ID 생성 부모와 동일한 지 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-551">*Inherit* – This setting is the default behavior for controls; it specifies that a control's ID generation is the same as its parent.</span></span>

<span data-ttu-id="819ca-552">설정할 수 있습니다는 *ClientIDMode* 페이지 수준에서 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-552">You can set the *ClientIDMode* property at the page level.</span></span> <span data-ttu-id="819ca-553">기본값을 정의 합니다. *ClientIDMode* 현재 페이지의 모든 컨트롤에 대 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-553">This defines the default *ClientIDMode* value for all controls in the current page.</span></span>

<span data-ttu-id="819ca-554">기본 *ClientIDMode* 페이지 수준에서 값은 *AutoID*, 및 기본 *ClientIDMode* 제어 수준 값은 *상속*.</span><span class="sxs-lookup"><span data-stu-id="819ca-554">The default *ClientIDMode* value at the page level is *AutoID*, and the default *ClientIDMode* value at the control level is *Inherit*.</span></span> <span data-ttu-id="819ca-555">결과적으로, 코드에서 아무 곳 이나이 속성을 설정 하지 않으면, 모든 컨트롤이 기본적으로 *AutoID* 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-555">As a result, if you do not set this property anywhere in your code, all controls will default to the *AutoID* algorithm.</span></span>

<span data-ttu-id="819ca-556">페이지 수준 값을 설정할는 *@ Page* 지시문, 다음 예제와 같이:</span><span class="sxs-lookup"><span data-stu-id="819ca-556">You set the page-level value in the *@ Page* directive, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample47.aspx)]

<span data-ttu-id="819ca-557">설정할 수도 있습니다는 *ClientIDMode* 컴퓨터 (컴퓨터) 수준에서 또는 응용 프로그램 수준에서 구성 파일의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-557">You can also set the *ClientIDMode* value in the configuration file, either at the computer (machine) level or at the application level.</span></span> <span data-ttu-id="819ca-558">기본값을 정의 합니다. *ClientIDMode* 응용 프로그램의 모든 페이지의 모든 컨트롤에 대 한 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-558">This defines the default *ClientIDMode* setting for all controls in all pages in the application.</span></span> <span data-ttu-id="819ca-559">기본 컴퓨터 수준에서 값을 설정 하면 정의 *ClientIDMode* 해당 컴퓨터에서 모든 웹 사이트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-559">If you set the value at the computer level, it defines the default *ClientIDMode* setting for all Web sites on that computer.</span></span> <span data-ttu-id="819ca-560">다음 예제와 *ClientIDMode* 구성 파일에서 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-560">The following example shows the *ClientIDMode* setting in the configuration file:</span></span>

[!code-xml[Main](overview/samples/sample48.xml)]

<span data-ttu-id="819ca-561">값의 앞에서 설명한 것 처럼는 *ClientID* 컨트롤의 부모에 대 한 속성의 명명 컨테이너에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-561">As noted earlier, the value of the *ClientID* property is derived from the naming container for a control's parent.</span></span> <span data-ttu-id="819ca-562">마스터 페이지를 사용 하는 경우와 같은 일부 시나리오에서는 컨트롤은 결국 Id를 가진 다음에서 같이 렌더링 된 HTML:</span><span class="sxs-lookup"><span data-stu-id="819ca-562">In some scenarios, such as when you are using master pages, controls can end up with IDs like those in the following rendered HTML:</span></span>

[!code-html[Main](overview/samples/sample49.html)]

<span data-ttu-id="819ca-563">경우에는 *입력* 태그에 표시 된 요소 (에서 *TextBox* 컨트롤) 두 개의 명명 컨테이너는 페이지에서 (중첩 된 *ContentPlaceholder* 컨트롤), 마스터 페이지를 처리 하는 방식으로 인해 최종 결과 다음과 같은 컨트롤 ID는:</span><span class="sxs-lookup"><span data-stu-id="819ca-563">Even though the *input* element shown in the markup (from a *TextBox* control) is only two naming containers deep in the page (the nested *ContentPlaceholder* controls), because of the way master pages are processed, the end result is a control ID like the following:</span></span>

[!code-console[Main](overview/samples/sample50.cmd)]

<span data-ttu-id="819ca-564">이 ID는 페이지에서 고유 하 게 보장 하지만 대부분의 용도 대해 불필요 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-564">This ID is guaranteed to be unique in the page, but is unnecessarily long for most purposes.</span></span> <span data-ttu-id="819ca-565">렌더링 된 ID의 길이를 줄이려면 및 ID 생성 되는 방식을 보다 자세하게 제어를 사용 한다고 가정해 보세요.</span><span class="sxs-lookup"><span data-stu-id="819ca-565">Imagine that you want to reduce the length of the rendered ID, and to have more control over how the ID is generated.</span></span> <span data-ttu-id="819ca-566">(예를 들어 하려는 "ctlxxx" 접두사를 제거 합니다.) 설정 하 여이 작업을 수행할 수는 가장 쉬운 방법은는 *ClientIDMode* 다음 예제와 같이 속성:</span><span class="sxs-lookup"><span data-stu-id="819ca-566">(For example, you want to eliminate "ctlxxx" prefixes.) The easiest way to achieve this is by setting the *ClientIDMode* property as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample51.aspx)]

<span data-ttu-id="819ca-567">이 샘플에는 *ClientIDMode* 속성이 *정적* 가장 바깥쪽에 대 한 *NamingPanel* 요소 및로 설정 *예측 가능* 내부에 대 한 *NamingControl* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-567">In this sample, the *ClientIDMode* property is set to *Static* for the outermost *NamingPanel* element, and set to *Predictable* for the inner *NamingControl* element.</span></span> <span data-ttu-id="819ca-568">이러한 설정은 다음 태그 (이전 예제에서와 동일 하 게 페이지와 마스터 페이지의 나머지 부분 가정)에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-568">These settings result in the following markup (the rest of the page and the master page is assumed to be the same as in the previous example):</span></span>

[!code-html[Main](overview/samples/sample52.html)]

<span data-ttu-id="819ca-569">*정적* 설정이 가장 바깥쪽 안의 모든 컨트롤에 대 한 명명 계층 구조를 다시 설정할 때의 효과 갖고 *NamingPanel* 요소를 제거 하 고는 *ContentPlaceHolder* 및 *MasterPage* Id에서 생성 된 id입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-569">The *Static* setting has the effect of resetting the naming hierarchy for any controls inside the outermost *NamingPanel* element, and of eliminating the *ContentPlaceHolder* and *MasterPage* IDs from the generated ID.</span></span> <span data-ttu-id="819ca-570">(의 *이름* 렌더링 된 요소의 특성은 영향을 이벤트에 대 한 일반 ASP.NET 기능 유지 하도록 뷰 상태를 하 고, 합니다.) 에 대 한 태그를 이동 하는 경우에 있는 명명 계층 구조를 다시 설정할 때의 부작용은는 *NamingPanel* 요소를 사용 하 여 다른 *ContentPlaceholder* 컨트롤을 렌더링 된 클라이언트 Id는 동일 하 게 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-570">(The *name* attribute of rendered elements is unaffected, so the normal ASP.NET functionality is retained for events, view state, and so on.) A side effect of resetting the naming hierarchy is that even if you move the markup for the *NamingPanel* elements to a different *ContentPlaceholder* control, the rendered client IDs remain the same.</span></span>

> [!NOTE]
> <span data-ttu-id="819ca-571">Note 렌더링 된 컨트롤 Id 고유한 지 확인 하기 위해 사용자가 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-571">Note It is up to you to make sure that the rendered control IDs are unique.</span></span> <span data-ttu-id="819ca-572">그러지 않은 경우 클라이언트와 같은 개별 HTML 요소에 대 한 고유 Id를 필요로 하는 모든 기능을 중단할 수 있습니다 *document.getElementById* 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-572">If they are not, it can break any functionality that requires unique IDs for individual HTML elements, such as the client *document.getElementById* function.</span></span>


#### <a name="creating-predictable-client-ids-in-data-bound-controls"></a><span data-ttu-id="819ca-573">데이터 바인딩된 컨트롤에서 예측 가능한 클라이언트 Id 만들기</span><span class="sxs-lookup"><span data-stu-id="819ca-573">Creating Predictable Client IDs in Data-Bound Controls</span></span>

<span data-ttu-id="819ca-574">*ClientID* 수 레거시 알고리즘에서 데이터 바인딩된 목록 컨트롤에서 컨트롤에 대해 생성 된 값을 하며는 실제로 예측할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-574">The *ClientID* values that are generated for controls in a data-bound list control by the legacy algorithm can be long and are not really predictable.</span></span> <span data-ttu-id="819ca-575">*ClientIDMode* 있으세요 어떻게 이러한 Id를 통해 생성 된 제어 기능 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-575">The *ClientIDMode* functionality can help you have more control over how these IDs are generated.</span></span>

<span data-ttu-id="819ca-576">다음 예제에서 태그를 포함 한 *ListView* 제어:</span><span class="sxs-lookup"><span data-stu-id="819ca-576">The markup in the following example includes a *ListView* control:</span></span>

[!code-aspx[Main](overview/samples/sample53.aspx)]

<span data-ttu-id="819ca-577">이전 예에서 *ClientIDMode* 및 *RowClientIDRowSuffix* 속성 태그에서 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-577">In the previous example, the *ClientIDMode* and *RowClientIDRowSuffix* properties are set in markup.</span></span> <span data-ttu-id="819ca-578">*ClientIDRowSuffix* 속성 데이터 바인딩된 컨트롤에만 사용할 수 있으며 해당 동작은 사용 하는 컨트롤에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-578">The *ClientIDRowSuffix* property can be used only in data-bound controls, and its behavior differs depending on which control you are using.</span></span> <span data-ttu-id="819ca-579">차이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-579">The differences are these:</span></span>

- <span data-ttu-id="819ca-580">*GridView* 컨트롤-지정할 수 있습니다 하나 이상의 열 이름을 데이터 원본에서 런타임에 클라이언트 Id 생성에 결합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-580">*GridView* control — You can specify the name of one or more columns in the data source, which are combined at run time to create the client IDs.</span></span> <span data-ttu-id="819ca-581">예를 들어, 설정한 경우 *RowClientIDRowSuffix* "ProductName, ProductId"를 컨트롤에 대 한 렌더링 된 요소는 다음과 같은 형식 Id:</span><span class="sxs-lookup"><span data-stu-id="819ca-581">For example, if you set *RowClientIDRowSuffix* to "ProductName, ProductId", control IDs for rendered elements will have a format like the following:</span></span>

- [!code-console[Main](overview/samples/sample54.cmd)]

- <span data-ttu-id="819ca-582">*ListView* 컨트롤-클라이언트 id와 같습니다. 추가 되는 데이터 원본에서 단일 열을 지정할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="819ca-582">*ListView* control — You can specify a single column in the data source that is appended to the client ID.</span></span> <span data-ttu-id="819ca-583">예를 들어, 설정한 경우 *ClientIDRowSuffix* "ProductName" 렌더링 된 컨트롤 Id는 다음과 같은 형식이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-583">For example, if you set *ClientIDRowSuffix* to "ProductName", the rendered control IDs will have a format like the following:</span></span>

- [!code-console[Main](overview/samples/sample55.cmd)]

- <span data-ttu-id="819ca-584">이 경우 후행 1은 현재 데이터 항목의 제품 ID에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-584">In this case the trailing 1 is derived from the product ID of the current data item.</span></span>

- <span data-ttu-id="819ca-585">*반복기* 컨트롤-이 컨트롤을 지원 하지 않습니다는 *ClientIDRowSuffix* 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-585">*Repeater* control— This control does not support the *ClientIDRowSuffix* property.</span></span> <span data-ttu-id="819ca-586">에 *반복기* 제어, 현재 행의 인덱스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-586">In a *Repeater* control, the index of the current row is used.</span></span> <span data-ttu-id="819ca-587">ClientIDMode를 사용 하는 경우 "예측 가능" =는 *반복기* 를 다음과 같은 형식의 Id가 생성 하는 클라이언트를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-587">When you use ClientIDMode="Predictable" with a *Repeater* control, client IDs are generated that have the following format:</span></span>

- [!code-console[Main](overview/samples/sample56.cmd)]

- <span data-ttu-id="819ca-588">후행 0에는 현재 행의 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-588">The trailing 0 is the index of the current row.</span></span>

<span data-ttu-id="819ca-589">*FormView* 및 *DetailsView* 컨트롤 지원 하지 않는 여러 행을 표시 하지 않습니다는 *ClientIDRowSuffix* 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-589">The *FormView* and *DetailsView* controls do not display multiple rows, so they do not support the *ClientIDRowSuffix* property.</span></span>

<a id="0.2__Toc224729038"></a><a id="0.2__Toc253429262"></a><a id="0.2__Toc243304636"></a>

### <a name="persisting-row-selection-in-data-controls"></a><span data-ttu-id="819ca-590">데이터 컨트롤에서 행 선택 보관</span><span class="sxs-lookup"><span data-stu-id="819ca-590">Persisting Row Selection in Data Controls</span></span>

<span data-ttu-id="819ca-591">*GridView* 및 *ListView* 컨트롤에는 사용자가 행을 선택 하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-591">The *GridView* and *ListView* controls can let users select a row.</span></span> <span data-ttu-id="819ca-592">이전 버전의 ASP.NET에서는 선택 페이지에서 행 인덱스에 따라 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-592">In previous versions of ASP.NET, selection has been based on the row index on the page.</span></span> <span data-ttu-id="819ca-593">예를 들어 1 페이지에서 세 번째 항목을 선택 하 고 다음 2 페이지로 이동 하는 경우에 해당 페이지에서 세 번째 항목이 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-593">For example, if you select the third item on page 1 and then move to page 2, the third item on that page is selected.</span></span>

<span data-ttu-id="819ca-594">처음 지속형된 선택 된.NET Framework 3.5 s p 1에서 동적 데이터 프로젝트에만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-594">Persisted selection was initially supported only in Dynamic Data projects in the .NET Framework 3.5 SP1.</span></span> <span data-ttu-id="819ca-595">이 기능을 사용 하는 경우 현재 선택한 항목은 항목에 대 한 데이터 키를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-595">When this feature is enabled, the current selected item is based on the data key for the item.</span></span> <span data-ttu-id="819ca-596">즉, 1 페이지에서 세 번째 행을 선택 하 고 2 페이지로 이동 하는 경우는 선택한 항목이 없음을 2 페이지.</span><span class="sxs-lookup"><span data-stu-id="819ca-596">This means that if you select the third row on page 1 and move to page 2, nothing is selected on page 2.</span></span> <span data-ttu-id="819ca-597">1 페이지로 다시 이동 하면 세 번째 행이 여전히 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-597">When you move back to page 1, the third row is still selected.</span></span> <span data-ttu-id="819ca-598">보관 된 선택에 지원 됩니다는 *GridView* 및 *ListView* 를 사용 하 여 모든 프로젝트에서 컨트롤의 *EnablePersistedSelection* 속성에 표시 된 대로 다음 예제:</span><span class="sxs-lookup"><span data-stu-id="819ca-598">Persisted selection is now supported for the *GridView* and *ListView* controls in all projects by using the *EnablePersistedSelection* property, as shown in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample57.aspx)]

<a id="0.2__Toc253429263"></a><a id="0.2__Toc243304637"></a>

### <a name="aspnet-chart-control"></a><span data-ttu-id="819ca-599">ASP.NET의 차트 컨트롤</span><span class="sxs-lookup"><span data-stu-id="819ca-599">ASP.NET Chart Control</span></span>

<span data-ttu-id="819ca-600">ASP.NET *차트* 컨트롤은.NET Framework의 데이터 시각화 기능 확장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-600">The ASP.NET *Chart* control expands the data-visualization offerings in the .NET Framework.</span></span> <span data-ttu-id="819ca-601">사용 하는 *차트* 컨트롤, ASP.NET 페이지에 복잡 한 통계 또는 재무 분석을 위해 직관적 이며 시각적으로 우수한 차트는 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-601">Using the *Chart* control, you can create ASP.NET pages that have intuitive and visually compelling charts for complex statistical or financial analysis.</span></span> <span data-ttu-id="819ca-602">ASP.NET *차트* 제어.NET Framework 버전 3.5 SP1 릴리스를 추가 기능으로 도입 되었으며.NET Framework 4 버전의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-602">The ASP.NET *Chart* control was introduced as an add-on to the .NET Framework version 3.5 SP1 release and is part of the .NET Framework 4 release.</span></span>

<span data-ttu-id="819ca-603">컨트롤에는 다음과 같은 기능이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-603">The control includes the following features:</span></span>

- <span data-ttu-id="819ca-604">35가지 개별 차트 종류</span><span class="sxs-lookup"><span data-stu-id="819ca-604">35 distinct chart types.</span></span>
- <span data-ttu-id="819ca-605">차트 영역, 제목, 범례 및 주석을의 무제한입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-605">An unlimited number of chart areas, titles, legends, and annotations.</span></span>
- <span data-ttu-id="819ca-606">다양 한 모든 차트 요소에 대 한 모양 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-606">A wide variety of appearance settings for all chart elements.</span></span>
- <span data-ttu-id="819ca-607">대부분의 차트 종류에 대 한 3 차원 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-607">3-D support for most chart types.</span></span>
- <span data-ttu-id="819ca-608">데이터 요소 주위에 자동으로 맞출 수 있는 스마트 데이터 레이블을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-608">Smart data labels that can automatically fit around data points.</span></span>
- <span data-ttu-id="819ca-609">줄무늬 선을, 배율 구분선 및 로그 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-609">Strip lines, scale breaks, and logarithmic scaling.</span></span>
- <span data-ttu-id="819ca-610">데이터 분석 및 변형을 위한 50개가 넘는 재무 및 통계 수식</span><span class="sxs-lookup"><span data-stu-id="819ca-610">More than 50 financial and statistical formulas for data analysis and transformation.</span></span>
- <span data-ttu-id="819ca-611">단순 바인딩 및 차트 데이터의 조작입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-611">Simple binding and manipulation of chart data.</span></span>
- <span data-ttu-id="819ca-612">에 날짜, 시간 및 통화와 같은 일반적인 데이터 형식 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-612">Support for common data formats such as dates, times, and currency.</span></span>
- <span data-ttu-id="819ca-613">대화형 작업 및 클라이언트를 포함 하는 이벤트 기반 사용자 지정에 대 한 지원 Ajax를 사용 하 여 이벤트를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-613">Support for interactivity and event-driven customization, including client click events using Ajax.</span></span>
- <span data-ttu-id="819ca-614">상태 관리</span><span class="sxs-lookup"><span data-stu-id="819ca-614">State management.</span></span>
- <span data-ttu-id="819ca-615">이진 스트리밍</span><span class="sxs-lookup"><span data-stu-id="819ca-615">Binary streaming.</span></span>

<span data-ttu-id="819ca-616">다음 그림에서는 ASP.NET의 차트 컨트롤에 의해 생성 되는 재무 차트의 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-616">The following figures show examples of financial charts that are produced by the ASP.NET Chart control.</span></span>

<a id="0.2_graphic17"></a>![](overview/_static/image1.png)

<span data-ttu-id="819ca-617">그림 2: ASP.NET 차트 컨트롤 예</span><span class="sxs-lookup"><span data-stu-id="819ca-617">Figure 2: ASP.NET Chart control examples</span></span>

<span data-ttu-id="819ca-618">샘플 코드를 다운로드 하는 추가 예제는 ASP.NET의 차트 컨트롤을 사용 하는 방법에 대 한는 [Microsoft 차트 컨트롤에 대 한 예제 환경](https://go.microsoft.com/fwlink/?LinkId=128300) MSDN 웹 사이트의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-618">For more examples of how to use the ASP.NET Chart control, download the sample code on the [Samples Environment for Microsoft Chart Controls](https://go.microsoft.com/fwlink/?LinkId=128300) page on the MSDN Web site.</span></span> <span data-ttu-id="819ca-619">콘텐츠 커뮤니티의 더 많은 샘플을 확인할 수 있습니다는 [차트 컨트롤 포럼](https://go.microsoft.com/fwlink/?LinkId=128713)합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-619">You can find more samples of community content at the [Chart Control Forum](https://go.microsoft.com/fwlink/?LinkId=128713).</span></span>

#### <a name="adding-the-chart-control-to-an-aspnet-page"></a><span data-ttu-id="819ca-620">ASP.NET 페이지에 차트 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="819ca-620">Adding the Chart Control to an ASP.NET Page</span></span>

<span data-ttu-id="819ca-621">추가 하는 방법을 보여 주는 다음 예제는 *차트* 태그를 사용 하 여 ASP.NET 페이지를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-621">The following example shows how to add a *Chart* control to an ASP.NET page by using markup.</span></span> <span data-ttu-id="819ca-622">예제에서는 *차트* 정적 데이터 요소에 대 한 세로 막대형 차트 컨트롤을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-622">In the example, the *Chart* control produces a column chart for static data points.</span></span>

[!code-aspx[Main](overview/samples/sample58.aspx)]

#### <a name="using-3-d-charts"></a><span data-ttu-id="819ca-623">3 차원 차트를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="819ca-623">Using 3-D Charts</span></span>

<span data-ttu-id="819ca-624">*차트* 컨트롤에 포함 되어는 *ChartAreas* 컬렉션을 포함할 수 있는 *ChartArea* 특징 차트의 차트 영역을 정의 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-624">The *Chart* control contains a *ChartAreas* collection, which can contain *ChartArea* objects that define characteristics of chart areas.</span></span> <span data-ttu-id="819ca-625">예를 들어 3 차원 차트 영역에 대 한를 사용 하려면 사용 하 여 *Area3DStyle* 다음 예제와 같이 속성:</span><span class="sxs-lookup"><span data-stu-id="819ca-625">For example, to use 3-D for a chart area, use the *Area3DStyle* property as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample59.aspx)]

<span data-ttu-id="819ca-626">아래 그림 4 개의 일련의 3 차원 차트는 *모음* 차트 종류입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-626">The figure below shows a 3-D chart with four series of the *Bar* chart type.</span></span>

<a id="0.2_graphic18"></a>![](overview/_static/image2.png)

<span data-ttu-id="819ca-627">그림 3: 3 차원 가로 막대형 차트</span><span class="sxs-lookup"><span data-stu-id="819ca-627">Figure 3: 3-D Bar Chart</span></span>

#### <a name="using-scale-breaks-and-logarithmic-scales"></a><span data-ttu-id="819ca-628">배율 구분선 및 로그 눈금 간격 사용</span><span class="sxs-lookup"><span data-stu-id="819ca-628">Using Scale Breaks and Logarithmic Scales</span></span>

<span data-ttu-id="819ca-629">배율 구분선 및 로그 눈금 간격은 두 가지 추가 숙련도 차트를 추가 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-629">Scale breaks and logarithmic scales are two additional ways to add sophistication to the chart.</span></span> <span data-ttu-id="819ca-630">이러한 기능은 특정 차트 영역에 있는 각 축에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-630">These features are specific to each axis in a chart area.</span></span> <span data-ttu-id="819ca-631">예를 들어 차트 영역의 기본 Y 축에 이러한 기능을 사용 하려면 사용 된 *AxisY.IsLogarithmic* 및 *ScaleBreakStyle* 속성에는 *ChartArea* 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-631">For example, to use these features on the primary Y axis of a chart area, use the *AxisY.IsLogarithmic* and *ScaleBreakStyle* properties in a *ChartArea* object.</span></span> <span data-ttu-id="819ca-632">다음 코드 조각은 기본 Y 축에 배율 구분선을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-632">The following snippet shows how to use scale breaks on the primary Y axis.</span></span>

[!code-aspx[Main](overview/samples/sample60.aspx)]

<span data-ttu-id="819ca-633">아래 그림에는 사용 하도록 설정 하는 배율 구분선이 있는 Y 축을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-633">The figure below shows the Y axis with scale breaks enabled.</span></span>

<a id="0.2_graphic19"></a>![](overview/_static/image3.png)

<span data-ttu-id="819ca-634">그림 4: 배율 구분선</span><span class="sxs-lookup"><span data-stu-id="819ca-634">Figure 4: Scale Breaks</span></span>

<a id="0.2__QueryExtender"></a><a id="0.2__Toc224729041"></a><a id="0.2__Toc253429264"></a><a id="0.2__Toc243304638"></a>

### <a name="filtering-data-with-the-queryextender-control"></a><span data-ttu-id="819ca-635">QueryExtender 컨트롤을 사용 하 여 데이터를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-635">Filtering Data with the QueryExtender Control</span></span>

<span data-ttu-id="819ca-636">데이터 기반 웹 페이지를 만드는 개발자를 위해는 가장 일반적인 작업 데이터를 필터링 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-636">A very common task for developers who create data-driven Web pages is to filter data.</span></span> <span data-ttu-id="819ca-637">이 일반적으로 수행 된 만들어서 *여기서* 절을 데이터 소스 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-637">This traditionally has been performed by building *Where* clauses in data source controls.</span></span> <span data-ttu-id="819ca-638">이 방법은 복잡할 수 및 일부 경우에는 *여기서* 구문 사용 하는 기본 데이터베이스의 모든 기능을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-638">This approach can be complicated, and in some cases the *Where* syntax does not let you take advantage of the full functionality of the underlying database.</span></span>

<span data-ttu-id="819ca-639">필터링을 더 쉽게 새 있도록 *QueryExtender* 컨트롤이 ASP.NET 4에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-639">To make filtering easier, a new *QueryExtender* control has been added in ASP.NET 4.</span></span> <span data-ttu-id="819ca-640">이 컨트롤에 추가할 수 있습니다 *EntityDataSource* 또는 *LinqDataSource* 컨트롤 이러한 컨트롤에 의해 반환 되는 데이터를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-640">This control can be added to *EntityDataSource* or *LinqDataSource* controls in order to filter the data returned by these controls.</span></span> <span data-ttu-id="819ca-641">때문에 *QueryExtender* LINQ에 의존 하 여, 매우 효율적이 고 작업으로 인해 페이지와 데이터를 보내기 전에 데이터베이스 서버에 필터가 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-641">Because the *QueryExtender* control relies on LINQ, the filter is applied on the database server before the data is sent to the page, which results in very efficient operations.</span></span>

<span data-ttu-id="819ca-642">*QueryExtender* 컨트롤에서는 다양 한 필터 옵션을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-642">The *QueryExtender* control supports a variety of filter options.</span></span> <span data-ttu-id="819ca-643">다음 섹션에서는 이러한 옵션에 설명 하 고 사용 하는 방법의 예를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-643">The following sections describe these options and provide examples of how to use them.</span></span>

#### <a name="search"></a><span data-ttu-id="819ca-644">검색</span><span class="sxs-lookup"><span data-stu-id="819ca-644">Search</span></span>

<span data-ttu-id="819ca-645">검색 옵션에 대 한는 *QueryExtender* 컨트롤 지정 된 필드에서 검색을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-645">For the search option, the *QueryExtender* control performs a search in specified fields.</span></span> <span data-ttu-id="819ca-646">다음 예제에서는 컨트롤 사용 하 여 TextBoxSearch 제어 및 검색에 내용 입력 한 텍스트는 `ProductName` 및 `Supplier.CompanyName` 에서 반환 되는 데이터의에서 열에는 *LinqDataSource* 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-646">In the following example, the control uses the text that is entered in the TextBoxSearch control and searches for its contents in the `ProductName` and `Supplier.CompanyName` columns in the data that is returned from the *LinqDataSource* control.</span></span>

[!code-aspx[Main](overview/samples/sample61.aspx)]

#### <a name="range"></a><span data-ttu-id="819ca-647">범위</span><span class="sxs-lookup"><span data-stu-id="819ca-647">Range</span></span>

<span data-ttu-id="819ca-648">범위 옵션 검색 옵션과 유사 하지만 범위를 정의 하는 값의 쌍을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-648">The range option is similar to the search option, but specifies a pair of values to define the range.</span></span> <span data-ttu-id="819ca-649">다음 예제에서는 *QueryExtender* 검색 제어는 `UnitPrice` 에서 반환 된 데이터의 열에에서는 *LinqDataSource* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-649">In the following example, the *QueryExtender* control searches the `UnitPrice` column in the data returned from the *LinqDataSource* control.</span></span> <span data-ttu-id="819ca-650">범위는 페이지 TextBoxFrom 및 TextBoxTo 컨트롤에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-650">The range is read from the TextBoxFrom and TextBoxTo controls on the page.</span></span>

[!code-aspx[Main](overview/samples/sample62.aspx)]

#### <a name="propertyexpression"></a><span data-ttu-id="819ca-651">PropertyExpression</span><span class="sxs-lookup"><span data-stu-id="819ca-651">PropertyExpression</span></span>

<span data-ttu-id="819ca-652">속성 식 옵션 속성 값 비교를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-652">The property expression option lets you define a comparison to a property value.</span></span> <span data-ttu-id="819ca-653">식이 계산 되는 경우 *true*, 검사 되 고 데이터가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-653">If the expression evaluates to *true*, the data that is being examined is returned.</span></span> <span data-ttu-id="819ca-654">다음 예제에서는 *QueryExtender* 컨트롤의 데이터를 비교 하 여 데이터를 필터링는 `Discontinued` 페이지 CheckBoxDiscontinued 컨트롤에서 열 값을 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-654">In the following example, the *QueryExtender* control filters data by comparing the data in the `Discontinued` column to the value from the CheckBoxDiscontinued control on the page.</span></span>

[!code-aspx[Main](overview/samples/sample63.aspx)]

#### <a name="customexpression"></a><span data-ttu-id="819ca-655">CustomExpression</span><span class="sxs-lookup"><span data-stu-id="819ca-655">CustomExpression</span></span>

<span data-ttu-id="819ca-656">마지막으로을 사용 하면 사용자 지정 식을 지정할 수 있습니다는 *QueryExtender* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-656">Finally, you can specify a custom expression to use with the *QueryExtender* control.</span></span> <span data-ttu-id="819ca-657">이 옵션에는 사용자 지정 필터 논리를 정의 하는 페이지에는 함수를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-657">This option lets you call a function in the page that defines custom filter logic.</span></span> <span data-ttu-id="819ca-658">다음 예제에서는 사용자 지정 식에 선언적으로 지정 하는 *QueryExtender* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-658">The following example shows how to declaratively specify a custom expression in the *QueryExtender* control.</span></span>

[!code-aspx[Main](overview/samples/sample64.aspx)]

<span data-ttu-id="819ca-659">다음 예제에서는 사용자 지정 함수에서 호출 하는 *QueryExtender* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-659">The following example shows the custom function that is invoked by the *QueryExtender* control.</span></span> <span data-ttu-id="819ca-660">포함 하는 데이터베이스 쿼리를 사용 하는 대신이 경우에 *여기서* 절, 코드를 사용 하 여 LINQ 쿼리에 데이터를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-660">In this case, instead of using a database query that includes a *Where* clause, the code uses a LINQ query to filter the data.</span></span>

[!code-csharp[Main](overview/samples/sample65.cs)]

<span data-ttu-id="819ca-661">이러한 예와 하나의 식에 사용 되는 *QueryExtender* 한 번에 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-661">These examples show only one expression being used in the *QueryExtender* control at a time.</span></span> <span data-ttu-id="819ca-662">그러나 안에 여러 개의 식을 포함할 수 있습니다는 *QueryExtender* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-662">However, you can include multiple expressions inside the *QueryExtender* control.</span></span>

<a id="0.2__Toc253429265"></a><a id="0.2__Toc243304639"></a>

### <a name="html-encoded-code-expressions"></a><span data-ttu-id="819ca-663">Html 인코딩된 코드 식</span><span class="sxs-lookup"><span data-stu-id="819ca-663">Html Encoded Code Expressions</span></span>

<span data-ttu-id="819ca-664">일부 ASP.NET 사이트 (특히 ASP.NET MVC)와 함께 사용 하 여에 크게 의존 `<%` =  `expression %>` 구문 ("코드 너"이 라고도 함)를 응답에 일부 텍스트를 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-664">Some ASP.NET sites (especially with ASP.NET MVC) rely heavily on using `<%`= `expression %>` syntax (often called "code nuggets") to write some text to the response.</span></span> <span data-ttu-id="819ca-665">코드 식을 사용 하면 HTML 인코딩할 텍스트 사용자에서 제공 하는 경우 텍스트를 입력 하는 경우이 페이지를 열어 놓을 수 XSS (교차 사이트 스크립팅) 공격에 잊기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-665">When you use code expressions, it is easy to forget to HTML-encode the text, If the text comes from user input, it can leave pages open to an XSS (Cross Site Scripting) attack.</span></span>

<span data-ttu-id="819ca-666">ASP.NET 4 아래 코드 식에 대 한 다음 새 구문을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-666">ASP.NET 4 introduces the following new syntax for code expressions:</span></span>

[!code-aspx[Main](overview/samples/sample66.aspx)]

<span data-ttu-id="819ca-667">이 구문은 응답에 쓸 때 기본적으로 HTML 인코딩을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-667">This syntax uses HTML encoding by default when writing to the response.</span></span> <span data-ttu-id="819ca-668">이 새 식 다음에 효과적으로 변환.</span><span class="sxs-lookup"><span data-stu-id="819ca-668">This new expression effectively translates to the following:</span></span>

[!code-aspx[Main](overview/samples/sample67.aspx)]

<span data-ttu-id="819ca-669">예를 들어 &lt;%: ["UserInput"] 요청 %&gt; 의 값에 HTML 인코딩을 수행 *["UserInput"] 요청*합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-669">For example, &lt;%: Request["UserInput"] %&gt; performs HTML encoding on the value of *Request["UserInput"]*.</span></span>

<span data-ttu-id="819ca-670">이 기능의 목표를 사용할 모든 단계에서 결정 하는로 강제 되지 않습니다 새 구문을 사용 하 여 이전 구문의 모든 인스턴스를 바꾸려면 수 있게 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-670">The goal of this feature is to make it possible to replace all instances of the old syntax with the new syntax so that you are not forced to decide at every step which one to use.</span></span> <span data-ttu-id="819ca-671">그러나 경우가 있습니다 출력 하 고 있는 텍스트 HTML 알 수 있도록 또는 이미 인코딩된 이중 인코딩으로 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-671">However, there are cases in which the text being output is meant to be HTML or is already encoded, in which case this could lead to double encoding.</span></span>

<span data-ttu-id="819ca-672">이러한 경우에 대 한 ASP.NET 4에서는 새로운 인터페이스 *IHtmlString*, 구체적 구현 함께 *HtmlString*합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-672">For those cases, ASP.NET 4 introduces a new interface, *IHtmlString*, along with a concrete implementation, *HtmlString*.</span></span> <span data-ttu-id="819ca-673">이러한 형식의 인스턴스를 사용 하는 반환 값은 이미 올바르게 인코딩되지 (또는 검사 하 고, 그렇지)를 HTML로 표시 하며 따라서 값 해야 하지 HTML로 인코딩된 다시 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-673">Instances of these types let you indicate that the return value is already properly encoded (or otherwise examined) for displaying as HTML, and that therefore the value should not be HTML-encoded again.</span></span> <span data-ttu-id="819ca-674">예를 들어 다음 수 없습니다 (아니며) 인코딩된 HTML:</span><span class="sxs-lookup"><span data-stu-id="819ca-674">For example, the following should not be (and is not) HTML encoded:</span></span>

[!code-aspx[Main](overview/samples/sample68.aspx)]

<span data-ttu-id="819ca-675">ASP.NET MVC 2 도우미 메서드가 ASP.NET 4를 실행 하는 경우에이 새 구문을 함께 사용 없는 이중 인코딩된, 되도록 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-675">ASP.NET MVC 2 helper methods have been updated to work with this new syntax so that they are not double encoded, but only when you are running ASP.NET 4.</span></span> <span data-ttu-id="819ca-676">ASP.NET 3.5 s p 1을 사용 하 여 응용 프로그램을 실행 하는 경우에이 새로운 구문의 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-676">This new syntax does not work when you run an application using ASP.NET 3.5 SP1.</span></span>

<span data-ttu-id="819ca-677">XSS 공격 으로부터 보호 보장 하지 않습니다이 염두에서에 둬야 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-677">Keep in mind that this does not guarantee protection from XSS attacks.</span></span> <span data-ttu-id="819ca-678">예를 들어 따옴표에 없는 특성 값을 사용 하는 HTML 여전히 취약 않은 사용자 입력을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-678">For example, HTML that uses attribute values that are not in quotation marks can contain user input that is still susceptible.</span></span> <span data-ttu-id="819ca-679">Note는 ASP.NET 컨트롤 및 ASP.NET MVC 도우미의 출력 항상가 포함 됩니다 특성 값 따옴표에서 방법이 권장된 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-679">Note that the output of ASP.NET controls and ASP.NET MVC helpers always includes attribute values in quotation marks, which is the recommended approach.</span></span>

<span data-ttu-id="819ca-680">마찬가지로,이 구문을 사용자 입력을 기반으로 하는 JavaScript 문자열을 만들 때와 같은 JavaScript 인코딩을 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-680">Likewise, this syntax does not perform JavaScript encoding, such as when you create a JavaScript string based on user input.</span></span>

<a id="0.2__Toc253429266"></a><a id="0.2__Toc243304640"></a>

### <a name="project-template-changes"></a><span data-ttu-id="819ca-681">프로젝트 템플릿 변경 사항</span><span class="sxs-lookup"><span data-stu-id="819ca-681">Project Template Changes</span></span>

<span data-ttu-id="819ca-682">이전 버전의 ASP.NET에서는 Visual Studio를 사용 하 여 새 웹 사이트 프로젝트 또는 웹 응용 프로그램 프로젝트를 만들 때 결과 프로젝트가 포함 되어는 Default.aspx 페이지만 기본 `Web.config` 파일 및 `App_Data` 폴더 아래에 나와 있는 것 처럼 그림:</span><span class="sxs-lookup"><span data-stu-id="819ca-682">In earlier versions of ASP.NET, when you use Visual Studio to create a new Web Site project or Web Application project, the resulting projects contain only a Default.aspx page, a default `Web.config` file, and the `App_Data` folder, as shown in the following illustration:</span></span>

<a id="0.2_graphic1A"></a>![](overview/_static/image4.png)

<span data-ttu-id="819ca-683">Visual Studio는 전혀, 다음 그림에 나와 있는 것 처럼 없는 파일을 포함 하는 빈 웹 사이트 프로젝트 형식을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-683">Visual Studio also supports an Empty Web Site project type, which contains no files at all, as shown in the following figure:</span></span>

<a id="0.2_graphic1B"></a>![](overview/_static/image5.png)

<span data-ttu-id="819ca-684">결과 초보자를 위한에 대 한 지침이 거의에 있는지 프로덕션 웹 응용 프로그램을 작성 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="819ca-684">The result is that for the beginner, there is very little guidance on how to build a production Web application.</span></span> <span data-ttu-id="819ca-685">따라서 ASP.NET 4에는 세 개의 새로운 템플릿이, 빈 웹 응용 프로그램 프로젝트 및 각 웹 응용 프로그램 및 웹 사이트 프로젝트에 대 한 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-685">Therefore, ASP.NET 4 introduces three new templates, one for an empty Web application project, and one each for a Web Application and Web Site project.</span></span>

#### <a name="empty-web-application-template"></a><span data-ttu-id="819ca-686">빈 웹 응용 프로그램 템플릿</span><span class="sxs-lookup"><span data-stu-id="819ca-686">Empty Web Application Template</span></span>

<span data-ttu-id="819ca-687">이름에서 알 수 있듯이 빈 웹 응용 프로그램 템플릿은 축소 웹 응용 프로그램 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-687">As the name suggests, the Empty Web Application template is a stripped-down Web Application project.</span></span> <span data-ttu-id="819ca-688">다음 그림에 나와 있는 것 처럼 Visual Studio 새 프로젝트 대화 상자에서이 프로젝트 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-688">You select this project template from the Visual Studio New Project dialog box, as shown in the following figure:</span></span>

[![](overview/_static/image7.png)](overview/_static/image6.png)

<span data-ttu-id="819ca-689">([전체 크기 이미지를 보려면 클릭](overview/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="819ca-689">([Click to view full-size image](overview/_static/image8.png))</span></span>

<span data-ttu-id="819ca-690">빈 ASP.NET 웹 응용 프로그램을 만들 때 Visual Studio는 다음 폴더의 레이아웃을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-690">When you create an Empty ASP.NET Web Application, Visual Studio creates the following folder layout:</span></span>

<a id="0.2_graphic1D"></a>![](overview/_static/image9.png)

<span data-ttu-id="819ca-691">이 한 가지 예외로 이전 버전의 ASP.NET 빈 웹 사이트 레이아웃 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-691">This is similar to the Empty Web Site layout from earlier versions of ASP.NET, with one exception.</span></span> <span data-ttu-id="819ca-692">빈 웹 응용 프로그램 및 빈 웹 사이트 프로젝트를 Visual Studio 2010에서 최소한의 다음을 포함 `Web.config` 는 프로젝트의 대상 프레임 워크를 식별 하려면 Visual Studio에서 사용 하는 정보가 포함 된 파일:</span><span class="sxs-lookup"><span data-stu-id="819ca-692">In Visual Studio 2010, Empty Web Application and Empty Web Site projects contain the following minimal `Web.config` file that contains information used by Visual Studio to identify the framework that the project is targeting:</span></span>

<a id="0.2_graphic1E"></a>![](overview/_static/image10.png)

<span data-ttu-id="819ca-693">이렇게 하지 않으면 *targetFramework* 속성, 이전 응용 프로그램을 열 때 호환성을 유지 하기 위해.NET Framework 2.0을 대상으로 Visual Studio 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-693">Without this *targetFramework* property, Visual Studio defaults to targeting the .NET Framework 2.0 in order to preserve compatibility when opening older applications.</span></span>

#### <a name="web-application-and-web-site-project-templates"></a><span data-ttu-id="819ca-694">웹 응용 프로그램 및 웹 사이트 프로젝트 템플릿</span><span class="sxs-lookup"><span data-stu-id="819ca-694">Web Application and Web Site Project Templates</span></span>

<span data-ttu-id="819ca-695">다른 두 개의 새 프로젝트 템플릿이 Visual Studio 2010과 함께 제공 되는 주요 변경을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-695">The other two new project templates that are shipped with Visual Studio 2010 contain major changes.</span></span> <span data-ttu-id="819ca-696">다음 그림은 새 웹 응용 프로그램 프로젝트를 만들 때 만들어지는 프로젝트 레이아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-696">The following figure shows the project layout that is created when you create a new Web Application project.</span></span> <span data-ttu-id="819ca-697">(웹 사이트 프로젝트에 대 한 레이아웃은 거의 동일 합니다.)</span><span class="sxs-lookup"><span data-stu-id="819ca-697">(The layout for a Web Site project is virtually identical.)</span></span>

- <a id="0.2_graphic1F"></a>![](overview/_static/image11.png)

<span data-ttu-id="819ca-698">프로젝트에 이전 버전에서 생성 되지 않은 파일의 수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-698">The project includes a number of files that were not created in earlier versions.</span></span> <span data-ttu-id="819ca-699">또한 새 웹 응용 프로그램 프로젝트 신속 하 게 새 응용 프로그램에 대 한 액세스를 보호 하기 시작 하면 기본 회원 기능을 통해 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-699">In addition, the new Web Application project is configured with basic membership functionality, which lets you quickly get started in securing access to the new application.</span></span> <span data-ttu-id="819ca-700">이 포함 되어 있어는 `Web.config` 멤버 자격, 역할 및 프로필을 구성 하는 데 사용 되는 항목을 포함 하는 새 프로젝트에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-700">Because of this inclusion, the `Web.config` file for the new project includes entries that are used to configure membership, roles, and profiles.</span></span> <span data-ttu-id="819ca-701">다음 예제와 `Web.config` 새 웹 응용 프로그램 프로젝트에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-701">The following example shows the `Web.config` file for a new Web Application project.</span></span> <span data-ttu-id="819ca-702">(이 경우 *roleManager* 을 사용할 수 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="819ca-702">(In this case, *roleManager* is disabled.)</span></span>

[![](overview/_static/image13.png)](overview/_static/image12.png)

<span data-ttu-id="819ca-703">([전체 크기 이미지를 보려면 클릭](overview/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="819ca-703">([Click to view full-size image](overview/_static/image14.png))</span></span>

<span data-ttu-id="819ca-704">두 번째 프로젝트에도 포함 되어 `Web.config` 파일에 `Account` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-704">The project also contains a second `Web.config` file in the `Account` directory.</span></span> <span data-ttu-id="819ca-705">두 번째 구성 파일 로그 되지 않은 사용자에서에 대 한 ChangePassword.aspx 페이지에 대 한 액세스를 보호 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-705">The second configuration file provides a way to secure access to the ChangePassword.aspx page for non-logged in users.</span></span> <span data-ttu-id="819ca-706">다음 예제에서는 두 번째의 내용을 `Web.config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-706">The following example shows the contents of the second `Web.config` file.</span></span>

![](overview/_static/image15.png)

<span data-ttu-id="819ca-707">새 프로젝트 템플릿이 기본적으로 생성 페이지도 이전 버전에서 보다 더 많은 콘텐츠를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-707">The pages created by default in the new project templates also contain more content than in previous versions.</span></span> <span data-ttu-id="819ca-708">기본 마스터 페이지 및 CSS 파일을 포함 하는 프로젝트 및 기본 페이지 (Default.aspx)는 기본적으로 마스터 페이지를 사용 하도록 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-708">The project contains a default master page and CSS file, and the default page (Default.aspx) is configured to use the master page by default.</span></span> <span data-ttu-id="819ca-709">결과 처음에 대 한 웹 응용 프로그램 또는 웹 사이트를 실행할 때 기본 (홈) 페이지를 이미 기능.</span><span class="sxs-lookup"><span data-stu-id="819ca-709">The result is that when you run the Web application or Web site for the first time, the default (home) page is already functional.</span></span> <span data-ttu-id="819ca-710">사실, 표시, 새 MVC 응용 프로그램을 시작 하면 기본 페이지로 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-710">In fact, it is similar to the default page you see when you start up a new MVC application.</span></span>

[![](overview/_static/image17.png)](overview/_static/image16.png)

<span data-ttu-id="819ca-711">([전체 크기 이미지를 보려면 클릭](overview/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="819ca-711">([Click to view full-size image](overview/_static/image18.png))</span></span>

<span data-ttu-id="819ca-712">프로젝트 템플릿에 대 한 이러한 변경의 의도 새 웹 응용 프로그램 작성을 시작 하는 방법에 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-712">The intention of these changes to the project templates is to provide guidance on how to start building a new Web application.</span></span> <span data-ttu-id="819ca-713">엄격한 XHTML 1.0 호환 의미적 태그와 함께 및 CSS를 사용 하 여 지정 된 레이아웃 페이지 서식 파일에 ASP.NET 4 웹 응용 프로그램을 구축 하기 위한 모범 사례를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-713">With semantically correct, strict XHTML 1.0-compliant markup and with layout that is specified using CSS, the pages in the templates represent best practices for building ASP.NET 4 Web applications.</span></span> <span data-ttu-id="819ca-714">기본 페이지는 쉽게 사용자 지정할 수 있는 2 열 레이아웃을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-714">The default pages also have a two-column layout that you can easily customize.</span></span>

<span data-ttu-id="819ca-715">예를 들어 새 웹 응용 프로그램에 대 한 고 가정 하는 색 중 일부를 변경 하 고 내 ASP.NET 응용 프로그램 로고가 대신 회사 로고를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-715">For example, imagine that for a new Web Application you want to change some of the colors and insert your company logo in place of the My ASP.NET Application logo.</span></span> <span data-ttu-id="819ca-716">아래에 새 디렉터리를 만들면이 위해 `Content` 로고 이미지를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-716">To do this, you create a new directory under `Content` to store your logo image:</span></span>

<a id="0.2_graphic23"></a>![](overview/_static/image19.png)

<span data-ttu-id="819ca-717">페이지에 이미지를 추가 하려면 다음 엽니다는 `Site.Master` 파일, 내 ASP.NET 응용 프로그램 텍스트 정의 된 위치와 사용 하 여 대체 위치 찾기는 *이미지* 요소 인 *src* 특성은 새 로고로 설정 다음 예제와 같이 이미지:</span><span class="sxs-lookup"><span data-stu-id="819ca-717">To add the image to the page, you then open the `Site.Master` file, find where the My ASP.NET Application text is defined, and replace it with an *image* element whose *src* attribute is set to the new logo image, as in the following example:</span></span>

[![](overview/_static/image21.png)](overview/_static/image20.png)

<span data-ttu-id="819ca-718">([전체 크기 이미지를 보려면 클릭](overview/_static/image22.png))</span><span class="sxs-lookup"><span data-stu-id="819ca-718">([Click to view full-size image](overview/_static/image22.png))</span></span>

<span data-ttu-id="819ca-719">그런 다음 Site.css 파일로 이동 하 고 페이지의 배경색 및 헤더를 변경 하는 CSS 클래스 정의 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-719">You can then go into the Site.css file and modify CSS class definitions to change the background color of the page as well as that of the header.</span></span>

<span data-ttu-id="819ca-720">이러한 변경의 결과 매우 적은 노력으로 사용자 지정된 홈 페이지를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-720">The result of these changes is that you can display a customized home page with very little effort:</span></span>

[![](overview/_static/image24.png)](overview/_static/image23.png)

<span data-ttu-id="819ca-721">([전체 크기 이미지를 보려면 클릭](overview/_static/image25.png))</span><span class="sxs-lookup"><span data-stu-id="819ca-721">([Click to view full-size image](overview/_static/image25.png))</span></span>

<a id="0.2__Toc253429267"></a><a id="0.2__Toc243304641"></a>

### <a name="css-improvements"></a><span data-ttu-id="819ca-722">CSS 개선 사항</span><span class="sxs-lookup"><span data-stu-id="819ca-722">CSS Improvements</span></span>

<span data-ttu-id="819ca-723">최신 HTML 표준을 준수 하는 HTML을 렌더링 하는 데 도움이 되었습니다 ASP.NET 4에는 작업의 주요 영역 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-723">One of the major areas of work in ASP.NET 4 has been to help render HTML that is compliant with the latest HTML standards.</span></span> <span data-ttu-id="819ca-724">ASP.NET 웹 서버 컨트롤에서 CSS 스타일을 사용 하는 방법에 대 한 변경 내용이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-724">This includes changes to how ASP.NET Web server controls use CSS styles.</span></span>

#### <a name="compatibility-setting-for-rendering"></a><span data-ttu-id="819ca-725">렌더링에 대 한 호환성 설정</span><span class="sxs-lookup"><span data-stu-id="819ca-725">Compatibility Setting for Rendering</span></span>

<span data-ttu-id="819ca-726">웹 응용 프로그램 또는 웹 사이트는.NET Framework 4를 대상으로 하는 경우 기본적으로는 *controlRenderingCompatibilityVersion* 특성에는 *페이지* "4.0"로 설정 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-726">By default, when a Web application or Web site targets the .NET Framework 4, the *controlRenderingCompatibilityVersion* attribute of the *pages* element is set to "4.0".</span></span> <span data-ttu-id="819ca-727">이 요소는 컴퓨터 수준에 정의 된 `Web.config` 파일을 기본적으로 모든 ASP.NET 4 응용 프로그램에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-727">This element is defined in the machine-level `Web.config` file and by default applies to all ASP.NET 4 applications:</span></span>

[!code-xml[Main](overview/samples/sample69.xml)]

<span data-ttu-id="819ca-728">에 대 한 값 *controlRenderingCompatibility* 는 새 버전의 잠재적인 정의 이후 릴리스에서 수 있는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-728">The value for *controlRenderingCompatibility* is a string, which allows potential new version definitions in future releases.</span></span> <span data-ttu-id="819ca-729">현재 릴리스에서 다음 값이이 속성에 대해 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-729">In the current release, the following values are supported for this property:</span></span>

- <span data-ttu-id="819ca-730">"3.5".</span><span class="sxs-lookup"><span data-stu-id="819ca-730">"3.5".</span></span> <span data-ttu-id="819ca-731">이 설정은 레거시 렌더링 및 태그를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-731">This setting indicates legacy rendering and markup.</span></span> <span data-ttu-id="819ca-732">컨트롤에서 렌더링 되는 태그는 100% 호환 및 설정의는 *xhtmlConformance* 속성은 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-732">Markup rendered by controls is 100% backward compatible, and the setting of the *xhtmlConformance* property is honored.</span></span>
- <span data-ttu-id="819ca-733">"4.0".</span><span class="sxs-lookup"><span data-stu-id="819ca-733">"4.0".</span></span> <span data-ttu-id="819ca-734">속성에 있는 경우이 설정은, ASP.NET 웹 서버 컨트롤은 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-734">If the property has this setting, ASP.NET Web server controls do the following:</span></span>
- <span data-ttu-id="819ca-735">*xhtmlConformance* 속성은 항상 "Strict"으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-735">The *xhtmlConformance* property is always treated as "Strict".</span></span> <span data-ttu-id="819ca-736">결과적으로, 컨트롤 XHTML 1.0 Strict 태그를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-736">As a result, controls render XHTML 1.0 Strict markup.</span></span>
- <span data-ttu-id="819ca-737">잘못 된 스타일을 렌더링 비 입력 컨트롤을 더 이상 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-737">Disabling non-input controls no longer renders invalid styles.</span></span>
- <span data-ttu-id="819ca-738">*div* 숨겨진된 필드 주위 요소는 사용자가 만든 CSS 규칙을 방해 하지 않도록 이제 스타일이 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-738">*div* elements around hidden fields are now styled so they do not interfere with user-created CSS rules.</span></span>
- <span data-ttu-id="819ca-739">메뉴 컨트롤에 의미가 올바르고 내게 필요한 옵션 지침과 호환 되는 태그를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-739">Menu controls render markup that is semantically correct and compliant with accessibility guidelines.</span></span>
- <span data-ttu-id="819ca-740">유효성 검사 컨트롤에는 인라인 스타일 렌더링 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-740">Validation controls do not render inline styles.</span></span>
- <span data-ttu-id="819ca-741">이전에 테두리를 렌더링 하는 제어 = "0" (ASP.NET에서 파생 된 컨트롤 *테이블* 컨트롤과 ASP.NET *이미지* 컨트롤) 더 이상이 특성을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-741">Controls that previously rendered border="0" (controls that derive from the ASP.NET *Table* control, and the ASP.NET *Image* control) no longer render this attribute.</span></span>

#### <a name="disabling-controls"></a><span data-ttu-id="819ca-742">컨트롤을 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="819ca-742">Disabling Controls</span></span>

<span data-ttu-id="819ca-743">ASP.NET 3.5 SP1 및 이전 버전의 프레임 워크 렌더링는 *비활성화* 모든 컨트롤에 대 한 HTML 태그에서 특성 *Enabled* 속성이로 설정 *false*합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-743">In ASP.NET 3.5 SP1 and earlier versions, the framework renders the *disabled* attribute in the HTML markup for any control whose *Enabled* property set to *false*.</span></span> <span data-ttu-id="819ca-744">그러나 HTML 4.01 사양에 따라 *입력* 요소는이 특성이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-744">However, according to the HTML 4.01 specification, only *input* elements should have this attribute.</span></span>

<span data-ttu-id="819ca-745">ASP.NET 4에서 설정할 수 있습니다는 *controlRenderingCompatabilityVersion* "3.5" 다음 예제와 같이 속성:</span><span class="sxs-lookup"><span data-stu-id="819ca-745">In ASP.NET 4, you can set the *controlRenderingCompatabilityVersion* property to "3.5", as in the following example:</span></span>

[!code-xml[Main](overview/samples/sample70.xml)]

<span data-ttu-id="819ca-746">에 대 한 태그를 만들 수 있습니다는 *레이블* 컨트롤을 해제 하는 다음과 같은 제어:</span><span class="sxs-lookup"><span data-stu-id="819ca-746">You might create markup for a *Label* control like the following, which disables the control:</span></span>

[!code-aspx[Main](overview/samples/sample71.aspx)]

<span data-ttu-id="819ca-747">*레이블* 컨트롤 다음 HTML을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-747">The *Label* control would render the following HTML:</span></span>

[!code-html[Main](overview/samples/sample72.html)]

<span data-ttu-id="819ca-748">ASP.NET 4에서 설정할 수 있습니다는 *controlRenderingCompatabilityVersion* 을 "4.0"입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-748">In ASP.NET 4, you can set the *controlRenderingCompatabilityVersion* to "4.0".</span></span> <span data-ttu-id="819ca-749">이 경우에 렌더링 되는 컨트롤 해당 *입력* 요소가 렌더링 됩니다는 *비활성화* 특성 컨트롤의 *Enabled* 속성이로 설정 되어 *false* .</span><span class="sxs-lookup"><span data-stu-id="819ca-749">In that case, only controls that render *input* elements will render a *disabled* attribute when the control's *Enabled* property is set to *false*.</span></span> <span data-ttu-id="819ca-750">HTML 렌더링 되지 않는 컨트롤 *입력* 요소 대신 렌더링 한 *클래스* 컨트롤에 대 한 비활성화 된 모양을 정의 하는 데 사용할 수 있는 CSS 클래스를 참조 하는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-750">Controls that do not render HTML *input* elements instead render a *class* attribute that references a CSS class that you can use to define a disabled look for the control.</span></span> <span data-ttu-id="819ca-751">예를 들어는 *레이블* 컨트롤 앞의 예에 표시 된 다음 태그를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-751">For example, the *Label* control shown in the earlier example would generate the following markup:</span></span>

[!code-html[Main](overview/samples/sample73.html)]

<span data-ttu-id="819ca-752">이 컨트롤에 대해 지정 하는 클래스에 대 한 기본값은 "aspnetdisabled 로" 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-752">The default value for the class that specified for this control is "aspNetDisabled".</span></span> <span data-ttu-id="819ca-753">그러나 정적 설정 하 여이 기본값을 변경할 수 있습니다 *DisabledCssClass* 의 정적 속성은 *WebControl* 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-753">However, you can change this default value by setting the static *DisabledCssClass* static property of the *WebControl* class.</span></span> <span data-ttu-id="819ca-754">컨트롤 개발자가 사용할 특정 컨트롤에 대 한 동작을 정의할 수도 있습니다를 사용 하 여 *SupportsDisabledAttribute* 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-754">For control developers, the behavior to use for a specific control can also be defined using the *SupportsDisabledAttribute* property.</span></span>

<a id="0.2__Toc253429268"></a><a id="0.2__Toc243304642"></a>

### <a name="hiding-div-elements-around-hidden-fields"></a><span data-ttu-id="819ca-755">Div 숨겨진 필드 주위 요소 숨기기</span><span class="sxs-lookup"><span data-stu-id="819ca-755">Hiding div Elements Around Hidden Fields</span></span>

<span data-ttu-id="819ca-756">ASP.NET 2.0 및 이후 버전에는 시스템 관련 숨겨진된 필드 렌더링 (같은 *숨겨진* 뷰 상태 정보를 저장 하는 데 사용 되는 요소) 내 *div* XHTML 표준을 준수 하기 위해 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-756">ASP.NET 2.0 and later versions render system-specific hidden fields (such as the *hidden* element used to store view state information) inside *div* element in order to comply with the XHTML standard.</span></span> <span data-ttu-id="819ca-757">그러나 CSS 규칙에 영향을 주는 문제가 발생할 수이 *div* 페이지의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-757">However, this can cause a problem when a CSS rule affects *div* elements on a page.</span></span> <span data-ttu-id="819ca-758">예를 들어 1 픽셀 선이 페이지에 표시 될 수 있습니다 약 숨겨진 *div* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-758">For example, it can result in a one-pixel line appearing in the page around hidden *div* elements.</span></span> <span data-ttu-id="819ca-759">ASP.NET 4에서 *div* ASP.NET에서 생성 된 숨겨진된 필드를 포함 하는 요소는 다음 예제와 같이 CSS 클래스 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-759">In ASP.NET 4, *div* elements that enclose the hidden fields generated by ASP.NET add a CSS class reference as in the following example:</span></span>

[!code-html[Main](overview/samples/sample74.html)]

<span data-ttu-id="819ca-760">다음에 적용 되는 CSS 클래스를 정의할 수 있습니다는 *숨겨진* 다음 예제와 같이 ASP.NET에서 생성 된 요소:</span><span class="sxs-lookup"><span data-stu-id="819ca-760">You can then define a CSS class that applies only to the *hidden* elements that are generated by ASP.NET, as in the following example:</span></span>

[!code-css[Main](overview/samples/sample75.css)]

<a id="0.2__Toc253429269"></a><a id="0.2__Toc243304643"></a>

### <a name="rendering-an-outer-table-for-templated-controls"></a><span data-ttu-id="819ca-761">템플릿 기반 컨트롤에 대 한 외부 테이블을 렌더링</span><span class="sxs-lookup"><span data-stu-id="819ca-761">Rendering an Outer Table for Templated Controls</span></span>

<span data-ttu-id="819ca-762">기본적으로 템플릿을 지 원하는 다음 ASP.NET 웹 서버 컨트롤은 인라인 스타일을 적용 하는 데 사용 되는 외부 테이블에 자동으로 줄:</span><span class="sxs-lookup"><span data-stu-id="819ca-762">By default, the following ASP.NET Web server controls that support templates are automatically wrapped in an outer table that is used to apply inline styles:</span></span>

- <span data-ttu-id="819ca-763">*FormView*</span><span class="sxs-lookup"><span data-stu-id="819ca-763">*FormView*</span></span>
- <span data-ttu-id="819ca-764">*Login*</span><span class="sxs-lookup"><span data-stu-id="819ca-764">*Login*</span></span>
- <span data-ttu-id="819ca-765">*PasswordRecovery*</span><span class="sxs-lookup"><span data-stu-id="819ca-765">*PasswordRecovery*</span></span>
- <span data-ttu-id="819ca-766">*ChangePassword*</span><span class="sxs-lookup"><span data-stu-id="819ca-766">*ChangePassword*</span></span>
- <span data-ttu-id="819ca-767">*마법사*</span><span class="sxs-lookup"><span data-stu-id="819ca-767">*Wizard*</span></span>
- <span data-ttu-id="819ca-768">*CreateUserWizard*</span><span class="sxs-lookup"><span data-stu-id="819ca-768">*CreateUserWizard*</span></span>

<span data-ttu-id="819ca-769">라는 새 속성이 *RenderOuterTable* 외부 테이블에서 태그를 제거할 수 있도록 이러한 컨트롤에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-769">A new property named *RenderOuterTable* has been added to these controls that allows the outer table to be removed from the markup.</span></span> <span data-ttu-id="819ca-770">예를 들어 다음의 예제는 *FormView* 제어:</span><span class="sxs-lookup"><span data-stu-id="819ca-770">For example, consider the following example of a *FormView* control:</span></span>

[!code-aspx[Main](overview/samples/sample76.aspx)]

<span data-ttu-id="819ca-771">이 태그는 HTML 테이블을 포함 하는 페이지에는 다음과 같은 출력을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-771">This markup renders the following output to the page, which includes an HTML table:</span></span>

[!code-html[Main](overview/samples/sample77.html)]

<span data-ttu-id="819ca-772">테이블을 렌더링 되지 않도록 방지 하려면 설정할 수 있습니다는 *FormView* 컨트롤의 *RenderOuterTable* 다음 예제와 같이 속성:</span><span class="sxs-lookup"><span data-stu-id="819ca-772">To prevent the table from being rendered, you can set the *FormView* control's *RenderOuterTable* property, as in the following example:</span></span>

[!code-aspx[Main](overview/samples/sample78.aspx)]

<span data-ttu-id="819ca-773">앞의 예제는 다음과 같은 출력 없이 렌더링 된 *테이블*, *tr*, 및 *td* 요소:</span><span class="sxs-lookup"><span data-stu-id="819ca-773">The previous example renders the following output, without the *table*, *tr*, and *td* elements:</span></span>

> <span data-ttu-id="819ca-774">콘텐츠</span><span class="sxs-lookup"><span data-stu-id="819ca-774">Content</span></span>


<span data-ttu-id="819ca-775">이 향상 된이 기능 쉽게 만들 수 css 컨트롤의 콘텐츠 스타일을 컨트롤에 의해 태그가 없습니다. 예기치 않은 렌더링 되기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-775">This enhancement can make it easier to style the content of the control with CSS, because no unexpected tags are rendered by the control.</span></span>

> [!NOTE]
> <span data-ttu-id="819ca-776">이 변경은 더 이상 없기 때문에 Visual Studio 2010 디자이너에서 자동 format 함수에 대 한 지원을 사용 하지 않도록 설정 하는 참고는 *테이블* 자동 서식 옵션에 의해 생성 되는 스타일 특성을 호스팅할 수 있는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-776">Note This change disables support for the auto-format function in the Visual Studio 2010 designer, because there is no longer a *table* element that can host style attributes that are generated by the auto-format option.</span></span>


<a id="0.2__Toc253429270"></a><a id="0.2__Toc243304644"></a>

### <a name="listview-control-enhancements"></a><span data-ttu-id="819ca-777">ListView 컨트롤의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="819ca-777">ListView Control Enhancements</span></span>

<span data-ttu-id="819ca-778">*ListView* 컨트롤이 쉽게 ASP.NET 4에 사용할 수 있게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-778">The *ListView* control has been made easier to use in ASP.NET 4.</span></span> <span data-ttu-id="819ca-779">컨트롤의 이전 버전 알려진 id 서버 컨트롤이 포함 된 레이아웃 템플릿을 지정 하는 데 필요한</span><span class="sxs-lookup"><span data-stu-id="819ca-779">The earlier version of the control required that you specify a layout template that contained a server control with a known ID.</span></span> <span data-ttu-id="819ca-780">다음 태그를 사용 하는 방법의 일반적인 예를 보여 줍니다.는 *ListView* ASP.NET 3.5에서 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-780">The following markup shows a typical example of how to use the *ListView* control in ASP.NET 3.5.</span></span>

[!code-aspx[Main](overview/samples/sample79.aspx)]

<span data-ttu-id="819ca-781">ASP.NET 4에서는 *ListView* 컨트롤 레이아웃 템플릿에 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-781">In ASP.NET 4, the *ListView* control does not require a layout template.</span></span> <span data-ttu-id="819ca-782">앞의 예제에 나와 있는 태그를 다음 태그로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-782">The markup shown in the previous example can be replaced with the following markup:</span></span>

[!code-aspx[Main](overview/samples/sample80.aspx)]

<a id="0.2__Toc253429271"></a><a id="0.2__Toc243304645"></a>

### <a name="checkboxlist-and-radiobuttonlist-control-enhancements"></a><span data-ttu-id="819ca-783">CheckBoxList 및 RadioButtonList 컨트롤 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="819ca-783">CheckBoxList and RadioButtonList Control Enhancements</span></span>

<span data-ttu-id="819ca-784">ASP.NET 3.5에서에 대 한 레이아웃을 지정할 수 있습니다는 *CheckBoxList* 및 *RadioButtonList* 다음 두 가지 설정을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="819ca-784">In ASP.NET 3.5, you can specify layout for the *CheckBoxList* and *RadioButtonList* using the following two settings:</span></span>

- <span data-ttu-id="819ca-785">*흐름*합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-785">*Flow*.</span></span> <span data-ttu-id="819ca-786">컨트롤 렌더링 *걸쳐* 요소를 사용 하는 콘텐츠를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-786">The control renders *span* elements to contain its content.</span></span>
- <span data-ttu-id="819ca-787">*테이블*합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-787">*Table*.</span></span> <span data-ttu-id="819ca-788">컨트롤 렌더링을 *테이블* 해당 콘텐츠를 포함 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-788">The control renders a *table* element to contain its content.</span></span>

<span data-ttu-id="819ca-789">다음 예제에서는 이러한 각 컨트롤에 대 한 태그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-789">The following example shows markup for each of these controls.</span></span>

[!code-aspx[Main](overview/samples/sample81.aspx)]

<span data-ttu-id="819ca-790">기본적으로 컨트롤을 렌더링 HTML 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-790">By default, the controls render HTML similar to the following:</span></span>

[!code-html[Main](overview/samples/sample82.html)]

<span data-ttu-id="819ca-791">HTML 목록을 사용 하 여 해당 콘텐츠를 렌더링 해야 이러한 컨트롤 의미적으로 HTML을 렌더링할 항목의 목록이 포함 되어 있으므로 (*li*) 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-791">Because these controls contain lists of items, to render semantically correct HTML, they should render their contents using HTML list (*li*) elements.</span></span> <span data-ttu-id="819ca-792">이렇게 하면 보조 기술을 사용 하 여 웹 페이지를 읽고 컨트롤을 더 쉽게 스타일 CSS를 사용할 수 있는 사용자에 대 한 쉽게 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-792">This makes it easier for users who read Web pages using assistive technology, and makes the controls easier to style using CSS.</span></span>

<span data-ttu-id="819ca-793">ASP.NET 4에서는 *CheckBoxList* 및 *RadioButtonList* 컨트롤 지원에 대 한 다음 새 값은 *RepeatLayout* 속성:</span><span class="sxs-lookup"><span data-stu-id="819ca-793">In ASP.NET 4, the *CheckBoxList* and *RadioButtonList* controls support the following new values for the *RepeatLayout* property:</span></span>

- <span data-ttu-id="819ca-794">*OrderedList* –으로 콘텐츠는 *li* 내에서 요소는 *ol* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-794">*OrderedList* – The content is rendered as *li* elements within an *ol* element.</span></span>
- <span data-ttu-id="819ca-795">*UnorderedList* –으로 콘텐츠는 *li* 내에서 요소는 *ul* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-795">*UnorderedList* – The content is rendered as *li* elements within a *ul* element.</span></span>

<span data-ttu-id="819ca-796">다음 예제에서는 이러한 새 값을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-796">The following example shows how to use these new values.</span></span>

[!code-aspx[Main](overview/samples/sample83.aspx)]

<span data-ttu-id="819ca-797">위의 태그에서는 다음 HTML을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-797">The preceding markup generates the following HTML:</span></span>

[!code-html[Main](overview/samples/sample84.html)]

> [!NOTE]
> <span data-ttu-id="819ca-798">설정할 경우 *RepeatLayout* 를 *OrderedList* 또는 *UnorderedList*, *RepeatDirection* 속성이 더 이상 사용할 수 있으며 됩니다 태그 또는 코드 내에서 속성이 설정 된 경우 런타임 시 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-798">Note If you set *RepeatLayout* to *OrderedList* or *UnorderedList*, the *RepeatDirection* property can no longer be used and will throw an exception at run time if the property has been set within your markup or code.</span></span> <span data-ttu-id="819ca-799">이러한 컨트롤의 시각적 레이아웃은 CSS를 대신 사용 하 여 정의 되었기 때문에 속성 값이 없는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-799">The property would have no value because the visual layout of these controls is defined using CSS instead.</span></span>


<a id="0.2__Toc253429272"></a><a id="0.2__Toc243304646"></a>

### <a name="menu-control-improvements"></a><span data-ttu-id="819ca-800">메뉴 컨트롤 향상 기능</span><span class="sxs-lookup"><span data-stu-id="819ca-800">Menu Control Improvements</span></span>

<span data-ttu-id="819ca-801">ASP.NET 4 하기 전에 *메뉴* 컨트롤이 일련의 HTML 테이블을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-801">Before ASP.NET 4, the *Menu* control rendered a series of HTML tables.</span></span> <span data-ttu-id="819ca-802">이 인라인 속성을 설정 하는 외부 CSS 스타일을 적용 하려면 어려웠습니다 있고 없기도 내게 필요한 옵션 표준 규격인 펌웨어.</span><span class="sxs-lookup"><span data-stu-id="819ca-802">This made it more difficult to apply CSS styles outside of setting inline properties and was also not compliant with accessibility standards.</span></span>

<span data-ttu-id="819ca-803">컨트롤은 ASP.NET 4에서 이제 목록 요소 및 순서가 지정 되지 않은 목록으로 구성 된 의미 체계 태그를 사용 하 여 HTML을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-803">In ASP.NET 4, the control now renders HTML using semantic markup that consists of an unordered list and list elements.</span></span> <span data-ttu-id="819ca-804">다음 예제에 대 한 ASP.NET 페이지의 태그를 보여 줍니다.는 *메뉴* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-804">The following example shows markup in an ASP.NET page for the *Menu* control.</span></span>

[!code-aspx[Main](overview/samples/sample85.aspx)]

<span data-ttu-id="819ca-805">컨트롤 다음 HTML 페이지가 렌더링 되 면 생성 (의 *onclick* 명확성에 대 한 코드는 생략):</span><span class="sxs-lookup"><span data-stu-id="819ca-805">When the page renders, the control produces the following HTML (the *onclick* code has been omitted for clarity):</span></span>

[!code-html[Main](overview/samples/sample86.html)]

<span data-ttu-id="819ca-806">렌더링 개선 사항 외에도 키보드 탐색 메뉴의 늘었습니다 포커스 관리를 사용 하 여.</span><span class="sxs-lookup"><span data-stu-id="819ca-806">In addition to rendering improvements, keyboard navigation of the menu has been improved using focus management.</span></span> <span data-ttu-id="819ca-807">경우는 *메뉴* 컨트롤에 포커스를 받을 경우 요소를 이동 하려면 화살표 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-807">When the *Menu* control gets focus, you can use the arrow keys to navigate elements.</span></span> <span data-ttu-id="819ca-808">*메뉴* 컨트롤 이제 액세스할 수 있는 리치 인터넷 응용 프로그램 (ARIA) 역할을 연결 및 특성을 앞[측 벽의](http://www.w3.org/TR/wai-aria-practices/#menu "메뉴 ARIA 지침")를 개선 하기 위해 액세스 가능성입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-808">The *Menu* control also now attaches accessible rich internet applications (ARIA) roles and attributes follo[wing the](http://www.w3.org/TR/wai-aria-practices/#menu "Menu ARIA guidelines")for improved accessibility.</span></span>

<span data-ttu-id="819ca-809">메뉴 컨트롤에 스타일을 스타일 블록에서 맨 위쪽에 렌더링 된 HTML 요소와 같은 줄이 아닌는 페이지의 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-809">Styles for the menu control are rendered in a style block at the top of the page, rather than in line with the rendered HTML elements.</span></span> <span data-ttu-id="819ca-810">컨트롤에 대 한 스타일 지정을 통해 완전히 제어 하려는 경우 새 설정할 수 *IncludeStyleBlock* 속성을 *false*, 스타일 블록 내보내지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="819ca-810">If you want to take full control over the styling for the control, you can set the new *IncludeStyleBlock* property to *false*, in which case the style block is not emitted.</span></span> <span data-ttu-id="819ca-811">이 속성을 사용 하는 한 가지 방법은 메뉴의 모양을 설정 하는 Visual Studio 디자이너에서 자동 서식 기능을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-811">One way to use this property is to use the auto-format feature in the Visual Studio designer to set the appearance of the menu.</span></span> <span data-ttu-id="819ca-812">페이지를 실행 하 고 페이지 소스를 열어 다음 외부 CSS 파일에 렌더링 된 스타일 블록을 복사 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-812">You can then run the page, open the page source, and then copy the rendered style block to an external CSS file.</span></span> <span data-ttu-id="819ca-813">Visual Studio에서 실행 취소 스타일 지정 및 집합 *IncludeStyleBlock* 를 *false*합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-813">In Visual Studio, undo the styling and set *IncludeStyleBlock* to *false*.</span></span> <span data-ttu-id="819ca-814">결과 메뉴가 표시 되도록 외부 스타일 시트에 스타일을 사용 하 여 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-814">The result is that the menu appearance is defined using styles in an external style sheet.</span></span>

<a id="0.2__Toc253429273"></a><a id="0.2__Toc243304647"></a>

### <a name="wizard-and-createuserwizard-controls"></a><span data-ttu-id="819ca-815">마법사 및 CreateUserWizard 컨트롤</span><span class="sxs-lookup"><span data-stu-id="819ca-815">Wizard and CreateUserWizard Controls</span></span>

<span data-ttu-id="819ca-816">ASP.NET *마법사* 및 *CreateUserWizard* 컨트롤 렌더링 하는 HTML을 정의할 수 있는 서식 파일을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-816">The ASP.NET *Wizard* and *CreateUserWizard* controls support templates that let you define the HTML that they render.</span></span> <span data-ttu-id="819ca-817">(*CreateUserWizard* 에서 파생 *마법사*.) 다음 예제에서는 완벽 하 게 템플릿 기반에 대 한 태그 *CreateUserWizard* 제어:</span><span class="sxs-lookup"><span data-stu-id="819ca-817">(*CreateUserWizard* derives from *Wizard*.) The following example shows the markup for a fully templated *CreateUserWizard* control:</span></span>

[!code-aspx[Main](overview/samples/sample87.aspx)]

<span data-ttu-id="819ca-818">컨트롤 다음과 유사한 HTML을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-818">The control renders HTML similar to the following:</span></span>

[!code-html[Main](overview/samples/sample88.html)]

<span data-ttu-id="819ca-819">ASP.NET 3.5 s p 1에서 템플릿 내용을 변경할 수 있지만 여전히 제한의 출력에 대 한 제어는 *마법사* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-819">In ASP.NET 3.5 SP1, although you can change the template contents, you still have limited control over the output of the *Wizard* control.</span></span> <span data-ttu-id="819ca-820">ASP.NET 4에서 만들 수 있습니다는 *LayoutTemplate* 템플릿과 삽입 *자리 표시자* 방법을 지정할 수 있습니다 (예약 된 이름 사용)을 제어는 *Wizard 컨트롤* 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-820">In ASP.NET 4, you can create a *LayoutTemplate* template and insert *PlaceHolder* controls (using reserved names) to specify how you want the *Wizard control* to render.</span></span> <span data-ttu-id="819ca-821">다음 예제에서는이 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-821">The following example shows this:</span></span>

[!code-aspx[Main](overview/samples/sample89.aspx)]

<span data-ttu-id="819ca-822">이 예제에서는 명명 된 자리 표시자에는 다음이 포함 된 *LayoutTemplate* 요소:</span><span class="sxs-lookup"><span data-stu-id="819ca-822">The example contains the following named placeholders in the *LayoutTemplate* element:</span></span>

- <span data-ttu-id="819ca-823">*headerPlaceholder* – 실행 시의 내용으로 대체 됩니다이 *HeaderTemplate* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-823">*headerPlaceholder* – At run time, this is replaced by the contents of the *HeaderTemplate* element.</span></span>
- <span data-ttu-id="819ca-824">*sideBarPlaceholder* – 실행 시의 내용으로 대체 됩니다이 *SideBarTemplate* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-824">*sideBarPlaceholder* – At run time, this is replaced by the contents of the *SideBarTemplate* element.</span></span>
- <span data-ttu-id="819ca-825">*wizardStepPlaceHolder* – 실행 시의 내용으로 대체 됩니다이 *WizardStepTemplate* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-825">*wizardStepPlaceHolder* – At run time, this is replaced by the contents of the *WizardStepTemplate* element.</span></span>
- <span data-ttu-id="819ca-826">*navigationPlaceholder* – 런타임 시 사용자가 정의한 모든 탐색 템플릿에 의해 대체 됩니다이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-826">*navigationPlaceholder* – At run time, this is replaced by any navigation templates that you have defined.</span></span>

<span data-ttu-id="819ca-827">자리 표시자를 사용 하는 예에서는 태그 (실제로 템플릿에 정의 된 콘텐츠) 없이 다음 HTML을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-827">The markup in the example that uses placeholders renders the following HTML (without the content actually defined in the templates):</span></span>

[!code-html[Main](overview/samples/sample90.html)]

<span data-ttu-id="819ca-828">이제 사용자 정의 문자열이 아닌지만 HTML이는 *걸쳐* 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-828">The only HTML that is now not user-defined is a *span* element.</span></span> <span data-ttu-id="819ca-829">(예상는 이후 릴리스에서도 *걸쳐* 요소 렌더링 되지 것입니다.) 이 구문은 이제에서 생성 되는 거의 모든 콘텐츠에 대 한 모든 권한을 제공는 *마법사* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-829">(We anticipate that in future releases, even the *span* element will not be rendered.) This now gives you full control over virtually all the content that is generated by the *Wizard* control.</span></span>

<a id="0.2_dyndata"></a><a id="0.2__Toc253429274"></a><a id="0.2__Toc243304648"></a><a id="0.2__Toc224729042"></a>

## <a name="aspnet-mvc"></a><span data-ttu-id="819ca-830">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="819ca-830">ASP.NET MVC</span></span>

<span data-ttu-id="819ca-831">ASP.NET MVC 2009 년 3 월에에서 추가 기능 프레임 워크로 ASP.NET 3.5 s p 1에 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-831">ASP.NET MVC was introduced as an add-on framework to ASP.NET 3.5 SP1 in March 2009.</span></span> <span data-ttu-id="819ca-832">Visual Studio 2010 새로운 특징과 기능을 포함 하는 ASP.NET MVC 2를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-832">Visual Studio 2010 includes ASP.NET MVC 2, which includes new features and capabilities.</span></span>

<a id="0.2__Toc253429275"></a>

### <a name="areas-support"></a><span data-ttu-id="819ca-833">영역 지원</span><span class="sxs-lookup"><span data-stu-id="819ca-833">Areas Support</span></span>

<span data-ttu-id="819ca-834">영역을 사용 하면 다른 섹션에서 상대 격리 상태에서 대형 응용 프로그램의 섹션으로 그룹 컨트롤러와 뷰 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-834">Areas let you group controllers and views into sections of a large application in relative isolation from other sections.</span></span> <span data-ttu-id="819ca-835">각 영역으로 주 응용 프로그램에서 참조 될 수 있는 별도 ASP.NET MVC 프로젝트를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-835">Each area can be implemented as a separate ASP.NET MVC project that can then be referenced by the main application.</span></span> <span data-ttu-id="819ca-836">대형 응용 프로그램을 빌드할 때 복잡해 지지 않도록 관리 고 여러 팀의 단일 응용 프로그램에서 함께 작동을 보다 쉽게 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-836">This helps manage complexity when you build a large application and makes it easier for multiple teams to work together on a single application.</span></span>

<a id="0.2__Toc253429276"></a>

### <a name="data-annotation-attribute-validation-support"></a><span data-ttu-id="819ca-837">데이터 주석을 특성 유효성 검사 지원</span><span class="sxs-lookup"><span data-stu-id="819ca-837">Data-Annotation Attribute Validation Support</span></span>

<span data-ttu-id="819ca-838">*DataAnnotations* 특성을 사용 하는 메타 데이터 특성을 사용 하 여 유효성 검사 논리 모델에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-838">*DataAnnotations* attributes let you attach validation logic to a model by using metadata attributes.</span></span> <span data-ttu-id="819ca-839">*DataAnnotations* 특성 ASP.NET Dynamic Data ASP.NET 3.5 s p 1에서에서 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-839">*DataAnnotations* attributes were introduced in ASP.NET Dynamic Data in ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="819ca-840">이러한 특성 기본 모델 바인더에 통합 되 고 사용자 입력의 유효성을 검사 하는 메타 데이터 기반 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-840">These attributes have been integrated into the default model binder and provide a metadata-driven means to validate user input.</span></span>

<a id="0.2__Toc253429277"></a>

### <a name="templated-helpers"></a><span data-ttu-id="819ca-841">템플릿 기반 도우미</span><span class="sxs-lookup"><span data-stu-id="819ca-841">Templated Helpers</span></span>

<span data-ttu-id="819ca-842">템플릿 기반 도우미 사용 하 여 자동으로 연결 편집 및 데이터 유형과 서식 파일을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-842">Templated helpers let you automatically associate edit and display templates with data types.</span></span> <span data-ttu-id="819ca-843">예를 들어 날짜 선택 UI 요소에 대 한 자동으로 렌더링 됨을 지정 하는 템플릿 도우미를 사용할 수 있습니다는 *System.DateTime* 값입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-843">For example, you can use a template helper to specify that a date-picker UI element is automatically rendered for a *System.DateTime* value.</span></span> <span data-ttu-id="819ca-844">ASP.NET Dynamic Data에 필드 템플릿에 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-844">This is similar to field templates in ASP.NET Dynamic Data.</span></span>

<span data-ttu-id="819ca-845">*Html.EditorFor* 및 *Html.DisplayFor* 여러 속성을 가진도 같이 복잡 한 개체 형식 표준 데이터 렌더링에 대 한 도우미 메서드는 기본 제공 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-845">The *Html.EditorFor* and *Html.DisplayFor* helper methods have built-in support for rendering standard data types as well as complex objects with multiple properties.</span></span> <span data-ttu-id="819ca-846">또한 렌더링을 사용자 지정와 같은 데이터 주석을 특성을 적용할 수 있도록 하 여 *DisplayName* 및 *ScaffoldColumn* 에 *ViewModel* 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-846">They also customize rendering by letting you apply data-annotation attributes like *DisplayName* and *ScaffoldColumn* to the *ViewModel* object.</span></span>

<span data-ttu-id="819ca-847">종종 하려는 UI 도우미를 더욱 해소에서 출력을 사용자 지정 생성 내용을 완전히 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-847">Often you want to customize the output from UI helpers even further and have complete control over what is generated.</span></span> <span data-ttu-id="819ca-848">*Html.EditorFor* 및 *Html.DisplayFor* 도우미 메서드를 지원이 재정의할 수 있는 외부 서식 파일 및 렌더링 된 출력 제어를 정의할 수 있는 템플릿 메커니즘을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-848">The *Html.EditorFor* and *Html.DisplayFor* helper methods support this using a templating mechanism that lets you define external templates that can override and control the output rendered.</span></span> <span data-ttu-id="819ca-849">클래스에 대 한 서식 파일을 개별적으로 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-849">The templates can be rendered individually for a class.</span></span>

<a id="0.2__Toc253429278"></a><a id="0.2__Toc243304649"></a>

## <a name="dynamic-data"></a><span data-ttu-id="819ca-850">Dynamic Data</span><span class="sxs-lookup"><span data-stu-id="819ca-850">Dynamic Data</span></span>

<span data-ttu-id="819ca-851">동적 데이터 도입 된 중순 2008의.NET Framework 3.5 SP1 릴리스에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-851">Dynamic Data was introduced in the .NET Framework 3.5 SP1 release in mid-2008.</span></span> <span data-ttu-id="819ca-852">이 기능은 다음을 포함 하는 데이터 기반 응용 프로그램을 만들기 위한 많은 향상 된 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-852">This feature provides many enhancements for creating data-driven applications, including the following:</span></span>

- <span data-ttu-id="819ca-853">데이터 기반 웹 사이트를 신속 하 게 빌드하기 위한 RAD 경험 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-853">A RAD experience for quickly building a data-driven Web site.</span></span>
- <span data-ttu-id="819ca-854">데이터 모델에 정의 된 제약 조건에 따라 자동 유효성 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-854">Automatic validation that is based on constraints defined in the data model.</span></span>
- <span data-ttu-id="819ca-855">필드에 대해 생성 되는 태그를 쉽게 변경할 수는 *GridView* 및 *DetailsView* 동적 데이터 프로젝트의 일부인 필드 템플릿을 사용 하 여 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-855">The ability to easily change the markup that is generated for fields in the *GridView* and *DetailsView* controls by using field templates that are part of your Dynamic Data project.</span></span>

> [!NOTE]
> <span data-ttu-id="819ca-856">자세한 내용은 참고를 참조 하십시오는 [동적 데이터 설명서](https://msdn.microsoft.com/library/cc488545.aspx) MSDN 라이브러리에서.</span><span class="sxs-lookup"><span data-stu-id="819ca-856">Note For more information, see the [Dynamic Data documentation](https://msdn.microsoft.com/library/cc488545.aspx) in the MSDN Library.</span></span>


<span data-ttu-id="819ca-857">ASP.NET 4에 대 한 동적 데이터 신속 하 게 데이터 기반 웹 사이트를 구축 하기 위한 개발자에 게 더 많은 전원을 제공 하도록 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-857">For ASP.NET 4, Dynamic Data has been enhanced to give developers even more power for quickly building data-driven Web sites.</span></span>

<a id="0.2__Toc253429279"></a><a id="0.2__Toc243304650"></a>

### <a name="enabling-dynamic-data-for-existing-projects"></a><span data-ttu-id="819ca-858">기존 프로젝트에 대 한 동적 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="819ca-858">Enabling Dynamic Data for Existing Projects</span></span>

<span data-ttu-id="819ca-859">.NET Framework 3.5 s p 1에서 제공 되는 동적 데이터 기능 다음과 같은 새로운 기능으로 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-859">Dynamic Data features that shipped in the .NET Framework 3.5 SP1 brought new features such as the following:</span></span>

- <span data-ttu-id="819ca-860">필드 템플릿 – 데이터 바인딩된 컨트롤에 대 한 데이터 형식을 기반으로 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-860">Field templates – These provide data-type-based templates for data-bound controls.</span></span> <span data-ttu-id="819ca-861">필드 템플릿은 템플릿 필드를 사용 하 여 각 필드에 대 한 보다 데이터 컨트롤의 모양을 사용자 지정 하는 보다 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-861">Field templates provide a simpler way to customize the look of data controls than using template fields for each field.</span></span>
- <span data-ttu-id="819ca-862">유효성 검사-동적 데이터 사용 하면 특성 데이터 클래스에 필수 필드, 범위 검사, 형식 검사, 패턴 정규식을 사용 하 여 일치와 같은 일반적인 시나리오에 대 한 유효성 검사 및 사용자 지정 유효성 검사를 지정 하려면.</span><span class="sxs-lookup"><span data-stu-id="819ca-862">Validation – Dynamic Data lets you use attributes on data classes to specify validation for common scenarios like required fields, range checking, type checking, pattern matching using regular expressions, and custom validation.</span></span> <span data-ttu-id="819ca-863">유효성 검사는 데이터 컨트롤에 의해 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-863">Validation is enforced by the data controls.</span></span>

<span data-ttu-id="819ca-864">그러나 이러한 기능에는 다음 요구 사항이 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-864">However, these features had the following requirements:</span></span>

- <span data-ttu-id="819ca-865">데이터 액세스 계층 Entity Framework 또는 LINQ to SQL 기반으로 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-865">The data-access layer had to be based on Entity Framework or LINQ to SQL.</span></span>
- <span data-ttu-id="819ca-866">유일한 데이터 원본 이러한 기능에 대해 지원 되는 컨트롤의 *EntityDataSource* 또는 *LinqDataSource* 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-866">The only data source controls supported for these features were the *EntityDataSource* or *LinqDataSource* controls.</span></span>
- <span data-ttu-id="819ca-867">기능으로 만들어진 동적 데이터 또는 동적 데이터 엔터티 서식 파일을 사용 하 여 기능을 지원 해야 하는 모든 파일을 가지려면 웹 프로젝트를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-867">The features required a Web project that had been created using the Dynamic Data or Dynamic Data Entities templates in order to have all the files that were required to support the feature.</span></span>

<span data-ttu-id="819ca-868">ASP.NET 4에서 동적 데이터 지원의 주요 목표는 모든 ASP.NET 응용 프로그램에 대 한 동적 데이터의 새 기능을 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-868">A major goal of Dynamic Data support in ASP.NET 4 is to enable the new functionality of Dynamic Data for any ASP.NET application.</span></span> <span data-ttu-id="819ca-869">다음 예제에서는 기존 페이지의 동적 데이터 기능을 사용할 수 있는 컨트롤에 대 한 태그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-869">The following example shows markup for controls that can take advantage of Dynamic Data functionality in an existing page.</span></span>

[!code-aspx[Main](overview/samples/sample91.aspx)]

<span data-ttu-id="819ca-870">페이지에 대 한 코드를에서 이러한 컨트롤에 대 한 동적 데이터 지원 사용 하기 위해 다음 코드를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-870">In the code for the page, the following code must be added in order to enable Dynamic Data support for these controls:</span></span>

[!code-csharp[Main](overview/samples/sample92.cs)]

<span data-ttu-id="819ca-871">경우는 *GridView* 컨트롤 편집 모드에 있으면 동적 데이터를 자동으로 입력 한 데이터가 올바른 형식 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-871">When the *GridView* control is in edit mode, Dynamic Data automatically validates that the data entered is in the proper format.</span></span> <span data-ttu-id="819ca-872">그렇지 않은 경우 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-872">If it is not, an error message is displayed.</span></span>

<span data-ttu-id="819ca-873">삽입 모드를 값에 대 한 기본값을 지정할 수 있는 등,이 기능은 또한의 기타 유용한 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-873">This functionality also provides other benefits, such as being able to specify default values for insert mode.</span></span> <span data-ttu-id="819ca-874">동적 데이터 없이 필드에 대 한 기본값을 구현 하 있습니다 해야 이벤트에, 연결 컨트롤 찾기 (사용 하 여 *FindControl*), 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-874">Without Dynamic Data, to implement a default value for a field, you must attach to an event, locate the control (using *FindControl*), and set its value.</span></span> <span data-ttu-id="819ca-875">ASP.NET 4에서는 *EnableDynamicData* 호출이이 예제에 나와 있는 것 처럼 개체에서 모든 필드에 대 한 기본 값을 전달할 수 있도록 하는 두 번째 매개 변수를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-875">In ASP.NET 4, the *EnableDynamicData* call supports a second parameter that lets you pass default values for any field on the object, as shown in this example:</span></span>

[!code-csharp[Main](overview/samples/sample93.cs)]

<a id="0.2__Toc224729043"></a><a id="0.2__Toc253429280"></a><a id="0.2__Toc243304651"></a>

### <a name="declarative-dynamicdatamanager-control-syntax"></a><span data-ttu-id="819ca-876">DynamicDataManager 컨트롤 선언적 구문</span><span class="sxs-lookup"><span data-stu-id="819ca-876">Declarative DynamicDataManager Control Syntax</span></span>

<span data-ttu-id="819ca-877">*DynamicDataManager* 선언적으로 구성할 수 있도록 개선 되었습니다 컨트롤 코드 에서만 대신 asp.net에서 대부분의 컨트롤와 마찬가지로 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-877">The *DynamicDataManager* control has been enhanced so that you can configure it declaratively, as with most controls in ASP.NET, instead of only in code.</span></span> <span data-ttu-id="819ca-878">에 대 한 태그는 *DynamicDataManager* 제어는 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-878">The markup for the *DynamicDataManager* control looks like the following example:</span></span>

[!code-aspx[Main](overview/samples/sample94.aspx)]

<span data-ttu-id="819ca-879">참조 되는 GridView1 컨트롤에 대 한 동적 데이터 동작을 사용 하는이 태그는 *DataControls* 의 섹션에서 *DynamicDataManager* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-879">This markup enables Dynamic Data behavior for the GridView1 control that is referenced in the *DataControls* section of the *DynamicDataManager* control.</span></span>

<a id="0.2__Toc224729044"></a><a id="0.2__Toc253429281"></a><a id="0.2__Toc243304652"></a>

### <a name="entity-templates"></a><span data-ttu-id="819ca-880">엔터티 서식 파일</span><span class="sxs-lookup"><span data-stu-id="819ca-880">Entity Templates</span></span>

<span data-ttu-id="819ca-881">엔터티 서식 파일을 사용자 지정 페이지를 만들 필요 없이 데이터의 레이아웃을 사용자 지정 하는 새로운 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-881">Entity templates offer a new way to customize the layout of data without requiring you to create a custom page.</span></span> <span data-ttu-id="819ca-882">템플릿을 사용 하 여 페이지는 *FormView* 컨트롤 (대신는 *DetailsView* 동적 데이터의 이전 버전의 페이지 서식 파일에서 사용 되는 제어) 및 *DynamicEntity* 엔터티 서식 파일을 렌더링 하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-882">Page templates use the *FormView* control (instead of the *DetailsView* control, as used in page templates in earlier versions of Dynamic Data) and the *DynamicEntity* control to render Entity templates.</span></span> <span data-ttu-id="819ca-883">동적 데이터를 통해 렌더링 되는 태그를 더 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-883">This gives you more control over the markup that is rendered by Dynamic Data.</span></span>

<span data-ttu-id="819ca-884">다음 목록에는 엔터티 템플릿에 포함 된 새 프로젝트 디렉터리 레이아웃을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-884">The following list shows the new project directory layout that contains entity templates:</span></span>

[!code-console[Main](overview/samples/sample95.cmd)]

<span data-ttu-id="819ca-885">`EntityTemplate` 디렉터리 데이터 모델 개체를 표시 하는 방법에 대 한 템플릿을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-885">The `EntityTemplate` directory contains templates for how to display data model objects.</span></span> <span data-ttu-id="819ca-886">기본적으로 개체를 사용 하 여 렌더링는 `Default.ascx` 가 만든 피드백과 같은 태그를 제공 하는 서식 파일은 *DetailsView* ASP.NET 3.5 s p 1에 동적 데이터를 사용 하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-886">By default, objects are rendered by using the `Default.ascx` template, which provides markup that looks just like the markup created by the *DetailsView* control used by Dynamic Data in ASP.NET 3.5 SP1.</span></span> <span data-ttu-id="819ca-887">다음 예제에 대 한 태그는 `Default.ascx` 제어:</span><span class="sxs-lookup"><span data-stu-id="819ca-887">The following example shows the markup for the `Default.ascx` control:</span></span>

[!code-aspx[Main](overview/samples/sample96.aspx)]

<span data-ttu-id="819ca-888">전체 사이트에 대 한 디자인을 변경 하려면 기본 템플릿은 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-888">The default templates can be edited to change the look and feel for the entire site.</span></span> <span data-ttu-id="819ca-889">표시, 편집 및 삽입 작업에 대 한 템플릿이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-889">There are templates for display, edit, and insert operations.</span></span> <span data-ttu-id="819ca-890">새 템플릿은 추가할 수 있습니다는 데이터 개체의 이름에 따라 한 가지 유형의 개체의 모양과 느낌을 변경 하려면.</span><span class="sxs-lookup"><span data-stu-id="819ca-890">New templates can be added based on the name of the data object in order to change the look and feel of just one type of object.</span></span> <span data-ttu-id="819ca-891">예를 들어 다음 템플릿을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-891">For example, you can add the following template:</span></span>

[!code-console[Main](overview/samples/sample97.cmd)]

<span data-ttu-id="819ca-892">서식 파일에 다음 태그를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-892">The template might contain the following markup:</span></span>

[!code-aspx[Main](overview/samples/sample98.aspx)]

<span data-ttu-id="819ca-893">새 엔터티 템플릿에 새를 사용 하 여 한 페이지에 표시 됩니다 *DynamicEntity* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-893">The new entity templates are displayed on a page by using the new *DynamicEntity* control.</span></span> <span data-ttu-id="819ca-894">런타임 시이 컨트롤은 엔터티 서식 파일의 내용으로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-894">At run time, this control is replaced with the contents of the entity template.</span></span> <span data-ttu-id="819ca-895">에서는 다음 태그는 *FormView* 컨트롤에 `Detail.aspx` 엔터티 서식 파일을 사용 하는 페이지 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-895">The following markup shows the *FormView* control in the `Detail.aspx` page template that uses the entity template.</span></span> <span data-ttu-id="819ca-896">공지는 *DynamicEntity* 태그 요소에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-896">Notice the *DynamicEntity* element in the markup.</span></span>

[!code-aspx[Main](overview/samples/sample99.aspx)]

<a id="0.2__Toc224729045"></a><a id="0.2__Toc253429282"></a><a id="0.2__Toc243304653"></a>

### <a name="new-field-templates-for-urls-and-email-addresses"></a><span data-ttu-id="819ca-897">Url 및 전자 메일 주소에 대 한 새 필드 템플릿</span><span class="sxs-lookup"><span data-stu-id="819ca-897">New Field Templates for URLs and Email Addresses</span></span>

<span data-ttu-id="819ca-898">ASP.NET 4에서는 두 개의 새로운 기본 제공 필드 템플릿을 `EmailAddress.ascx` 및 `Url.ascx`합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-898">ASP.NET 4 introduces two new built-in field templates, `EmailAddress.ascx` and `Url.ascx`.</span></span> <span data-ttu-id="819ca-899">이러한 템플릿은으로 표시 된 필드에 사용 됩니다 *EmailAddress* 또는 *Url* 와 *DataType* 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-899">These templates are used for fields that are marked as *EmailAddress* or *Url* with the *DataType* attribute.</span></span> <span data-ttu-id="819ca-900">에 대 한 *EmailAddress* 개체를 사용 하 여 만든 하이퍼링크로 필드가 표시 됩니다는 *mailto:* 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-900">For *EmailAddress* objects, the field is displayed as a hyperlink that is created by using the *mailto:* protocol.</span></span> <span data-ttu-id="819ca-901">사용자가 링크를 클릭 하면 사용자의 전자 메일 클라이언트 열리고 기본 메시지가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-901">When users click the link, it opens the user's email client and creates a skeleton message.</span></span> <span data-ttu-id="819ca-902">로 형식화 된 개체가 *Url* 일반 하이퍼링크로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-902">Objects typed as *Url* are displayed as ordinary hyperlinks.</span></span>

<span data-ttu-id="819ca-903">다음 예제에서는 필드가 표시 되는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-903">The following example shows how fields would be marked.</span></span>

[!code-csharp[Main](overview/samples/sample100.cs)]

<a id="0.2__Toc224729046"></a><a id="0.2__Toc253429283"></a><a id="0.2__Toc243304654"></a>

### <a name="creating-links-with-the-dynamichyperlink-control"></a><span data-ttu-id="819ca-904">DynamicHyperLink 컨트롤을 사용 하 여 링크 만들기</span><span class="sxs-lookup"><span data-stu-id="819ca-904">Creating Links with the DynamicHyperLink Control</span></span>

<span data-ttu-id="819ca-905">Dynamic Data 웹 사이트에 액세스할 때 최종 사용자에 게 표시 하는 Url을 제어 하려면.NET Framework 3.5 SP1에서 추가 된 새 라우팅 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-905">Dynamic Data uses the new routing feature that was added in the .NET Framework 3.5 SP1 to control the URLs that end users see when they access the Web site.</span></span> <span data-ttu-id="819ca-906">새 *DynamicHyperLink* 컨트롤을 사용 하면 손쉽게 데이터 동적 사이트의 페이지에 대 한 링크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-906">The new *DynamicHyperLink* control makes it easy to build links to pages in a Dynamic Data site.</span></span> <span data-ttu-id="819ca-907">사용 하는 방법을 보여 주는 다음 예제는 *DynamicHyperLink* 제어:</span><span class="sxs-lookup"><span data-stu-id="819ca-907">The following example shows how to use the *DynamicHyperLink* control:</span></span>

[!code-aspx[Main](overview/samples/sample101.aspx)]

<span data-ttu-id="819ca-908">이 태그에 대 한 목록 페이지를 가리키는 링크를 만듭니다.는 `Products` 테이블에 정의 된 경로에 따라는 `Global.asax` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-908">This markup creates a link that points to the List page for the `Products` table based on routes that are defined in the `Global.asax` file.</span></span> <span data-ttu-id="819ca-909">컨트롤에는 자동으로 동적 데이터 페이지를 기반으로 하는 기본 테이블 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-909">The control automatically uses the default table name that the Dynamic Data page is based on.</span></span>

<a id="0.2__Toc224729047"></a><a id="0.2__Toc253429284"></a><a id="0.2__Toc243304655"></a>

### <a name="support-for-inheritance-in-the-data-model"></a><span data-ttu-id="819ca-910">데이터 모델의 상속에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="819ca-910">Support for Inheritance in the Data Model</span></span>

<span data-ttu-id="819ca-911">Entity Framework와 LINQ to SQL 해당 데이터 모델에서 상속을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-911">Both the Entity Framework and LINQ to SQL support inheritance in their data models.</span></span> <span data-ttu-id="819ca-912">이러한 예에 있는 데이터베이스 수 있습니다는 `InsurancePolicy` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-912">An example of this might be a database that has an `InsurancePolicy` table.</span></span> <span data-ttu-id="819ca-913">들어 있을 수도 있습니다 `CarPolicy` 및 `HousePolicy` 동일한 필드를이 있는 테이블 `InsurancePolicy` 다음 더 많은 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-913">It might also contain `CarPolicy` and `HousePolicy` tables that have the same fields as `InsurancePolicy` and then add more fields.</span></span> <span data-ttu-id="819ca-914">동적 데이터 데이터 모델에서 상속 된 개체를 이해 하 고 상속된 된 테이블에 대 한 스 캐 폴딩을 지원 하도록 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-914">Dynamic Data has been modified to understand inherited objects in the data model and to support scaffolding for the inherited tables.</span></span>

<a id="0.2__Toc224729048"></a><a id="0.2__Toc253429285"></a><a id="0.2__Toc243304656"></a>

### <a name="support-for-many-to-many-relationships-entity-framework-only"></a><span data-ttu-id="819ca-915">다 대 다 관계 (Entity Framework에만 해당)에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="819ca-915">Support for Many-to-Many Relationships (Entity Framework Only)</span></span>

<span data-ttu-id="819ca-916">Entity Framework에서 컬렉션으로 관계를 노출 하 여 구현 하는 테이블 간에 다 대 다 관계에 대 한 다양 한 지원에는 *엔터티* 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-916">The Entity Framework has rich support for many-to-many relationships between tables, which is implemented by exposing the relationship as a collection on an *Entity* object.</span></span> <span data-ttu-id="819ca-917">새 `ManyToMany.ascx` 및 `ManyToMany_Edit.ascx` 지원을 제공 하기 위해 다 대 다 관계에 관련 데이터 표시 및 편집에 대 한 필드 템플릿이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-917">New `ManyToMany.ascx` and `ManyToMany_Edit.ascx` field templates have been added to provide support for displaying and editing data that is involved in many-to-many relationships.</span></span>

<a id="0.2__Toc224729049"></a><a id="0.2__Toc253429286"></a><a id="0.2__Toc243304657"></a>

### <a name="new-attributes-to-control-display-and-support-enumerations"></a><span data-ttu-id="819ca-918">새 특성을 제어 표시 및 지원 열거형</span><span class="sxs-lookup"><span data-stu-id="819ca-918">New Attributes to Control Display and Support Enumerations</span></span>

<span data-ttu-id="819ca-919">*DisplayAttribute* 하 게 추가 필드가 표시 되는 방식을 제어에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-919">The *DisplayAttribute* has been added to give you additional control over how fields are displayed.</span></span> <span data-ttu-id="819ca-920">*DisplayName* 특성 이전 버전의 동적 데이터 필드에 대 한 캡션으로 사용 되는 이름을 변경 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-920">The *DisplayName* attribute in earlier versions of Dynamic Data allowed you to change the name that is used as a caption for a field.</span></span> <span data-ttu-id="819ca-921">새 *DisplayAttribute* 클래스 필드를 필터로 사용 되는지 여부 및 필드가 표시 되는 순서와 같은 필드를 표시 하기 위한 옵션을 추가로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-921">The new *DisplayAttribute* class lets you specify more options for displaying a field, such as the order in which a field is displayed and whether a field will be used as a filter.</span></span> <span data-ttu-id="819ca-922">특성의 레이블에 사용 되는 이름의 독립적으로 제어할 제공는 *GridView* 제어에 사용 된은 *DetailsView* 는 필드에 대 한 도움말 텍스트를 제어 하 고에 사용 되는 워터 마크는 필드 (텍스트 입력 필드에서 허용) 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-922">The attribute also provides independent control of the name used for the labels in a *GridView* control, the name used in a *DetailsView* control, the help text for the field, and the watermark used for the field (if the field accepts text input).</span></span>

<span data-ttu-id="819ca-923">*EnumDataTypeAttribute* 클래스 필드 열거형에 매핑할 수 있도록에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-923">The *EnumDataTypeAttribute* class has been added to let you map fields to enumerations.</span></span> <span data-ttu-id="819ca-924">필드에이 특성을 적용 하는 경우 열거형 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-924">When you apply this attribute to a field, you specify an enumeration type.</span></span> <span data-ttu-id="819ca-925">동적 데이터를 사용 하 여 새 `Enumeration.ascx` 필드 템플릿을 표시 하 고 열거형 값을 편집에 대 한 UI를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-925">Dynamic Data uses the new `Enumeration.ascx` field template to create UI for displaying and editing enumeration values.</span></span> <span data-ttu-id="819ca-926">서식 파일 열거형의 이름으로 데이터베이스에서 값을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-926">The template maps the values from the database to the names in the enumeration.</span></span>

<a id="0.2__Toc224729050"></a><a id="0.2__Toc253429287"></a><a id="0.2__Toc243304658"></a>

### <a name="enhanced-support-for-filters"></a><span data-ttu-id="819ca-927">필터에 대 한 향상 된 지원</span><span class="sxs-lookup"><span data-stu-id="819ca-927">Enhanced Support for Filters</span></span>

<span data-ttu-id="819ca-928">동적 데이터 1.0 부울 열과 외래 키 열에 대 한 기본 제공 필터와 함께 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-928">Dynamic Data 1.0 shipped with built-in filters for Boolean columns and foreign-key columns.</span></span> <span data-ttu-id="819ca-929">필터가 있는지 여부를 표시 하기 또는 표시 된 순서에서를 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-929">The filters did not allow you to specify whether they were displayed or in what order they were displayed.</span></span> <span data-ttu-id="819ca-930">새 *DisplayAttribute* 특성 모두의 주소 제공 하 여 이러한 문제를 필터로 열 표시 되는지 여부를 통해 제어 하 고 순서에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-930">The new *DisplayAttribute* attribute addresses both of these issues by giving you control over whether a column is displayed as a filter and in what order it will be displayed.</span></span>

<span data-ttu-id="819ca-931">향상 된 추가 기능 지원 필터링 되었는지 다시은[새을 사용 하도록 작성](#0.2__QueryExtender "_QueryExtender") Web Forms의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-931">An additional enhancement is that filtering support has been re[written to use the new](#0.2__QueryExtender "_QueryExtender") feature of Web Forms.</span></span> <span data-ttu-id="819ca-932">이 필터는 함께 사용 될 데이터 소스 컨트롤의 한 지식 없이 필터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-932">This lets you create filters without requiring knowledge of the data source control that the filters will be used with.</span></span> <span data-ttu-id="819ca-933">이러한 확장과 함께 필터 변환 되었으므로 템플릿 컨트롤로 새로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-933">Along with these extensions, filters have also been turned into template controls, which allows you to add new ones.</span></span> <span data-ttu-id="819ca-934">마지막으로 *DisplayAttribute* 앞에서 언급 한 클래스를 통해 동일한에서 재정의 되도록 기본 필터 방식으로 *UIHint* 를 재정의할 수 열에 대 한 기본 필드 템플릿이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-934">Finally, the *DisplayAttribute* class mentioned earlier allows the default filter to be overridden, in the same way that *UIHint* allows the default field template for a column to be overridden.</span></span>

<a id="0.2__Toc224729051"></a><a id="0.2__Toc253429288"></a><a id="0.2__Toc243304659"></a>

## <a name="visual-studio-2010-web-development-improvements"></a><span data-ttu-id="819ca-935">Visual Studio 2010 웹 개발 기능 향상</span><span class="sxs-lookup"><span data-stu-id="819ca-935">Visual Studio 2010 Web Development Improvements</span></span>

<span data-ttu-id="819ca-936">Visual Studio 2010에서 웹 개발 CSS 호환성, HTML 및 ASP.NET 마크업 코드 조각 및 새 동적 IntelliSense JavaScript를 통해 생산성 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-936">Web development in Visual Studio 2010 has been enhanced for greater CSS compatibility, increased productivity through HTML and ASP.NET markup snippets and new dynamic IntelliSense JavaScript.</span></span>

<a id="0.2__Toc224729052"></a><a id="0.2__Toc253429289"></a><a id="0.2__Toc243304660"></a>

### <a name="improved-css-compatibility"></a><span data-ttu-id="819ca-937">향상 된 CSS 호환성</span><span class="sxs-lookup"><span data-stu-id="819ca-937">Improved CSS Compatibility</span></span>

<span data-ttu-id="819ca-938">Visual Studio 2010의 Visual Web Developer 디자이너 CSS 2.1 표준 준수를 개선 하기 위해 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-938">The Visual Web Developer designer in Visual Studio 2010 has been updated to improve CSS 2.1 standards compliance.</span></span> <span data-ttu-id="819ca-939">더 잘 디자이너의 HTML 소스의 무결성을 유지 하 고 이전 버전의 Visual Studio 보다 더 강력 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-939">The designer better preserves integrity of the HTML source and is more robust than in previous versions of Visual Studio.</span></span> <span data-ttu-id="819ca-940">내부적으로 아키텍처도 향상 되었습니다 렌더링, 레이아웃 및 서비스 효율성의 이후 향상 된 가능 하도록 해당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-940">Under the hood, architectural improvements have also been made that will better enable future enhancements in rendering, layout, and serviceability.</span></span>

<a id="0.2__Toc224729053"></a><a id="0.2__Toc253429290"></a><a id="0.2__Toc243304661"></a>

### <a name="html-and-javascript-snippets"></a><span data-ttu-id="819ca-941">HTML 및 JavaScript 코드 조각</span><span class="sxs-lookup"><span data-stu-id="819ca-941">HTML and JavaScript Snippets</span></span>

<span data-ttu-id="819ca-942">HTML 편집기에서 IntelliSense 자동 완성 태그 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-942">In the HTML editor, IntelliSense auto-completes tag names.</span></span> <span data-ttu-id="819ca-943">IntelliSense 코드 조각 기능 자동 완성 전체 태그 등입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-943">The IntelliSense Snippets feature auto-completes entire tags and more.</span></span> <span data-ttu-id="819ca-944">Visual Studio 2010의 IntelliSense 코드 조각 javascript, C# 및 Visual Basic의 경우 이전 버전의 Visual Studio에서 지원 되므로 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-944">In Visual Studio 2010, IntelliSense snippets are supported for JavaScript, alongside C# and Visual Basic, which were supported in earlier versions of Visual Studio.</span></span>

<span data-ttu-id="819ca-945">Visual Studio 2010 자동 완성 일반적인 ASP.NET 및 HTML 태그를 필수 특성을 포함 하는 데 도움이 되는 200 개가 넘는 코드 조각을 포함 (같은 runat = "server") 및 특정 태그에 공통 특성 (같은 *ID*,  *DataSourceID*, *ControlToValidate*, 및 *텍스트*).</span><span class="sxs-lookup"><span data-stu-id="819ca-945">Visual Studio 2010 includes over 200 snippets that help you auto-complete common ASP.NET and HTML tags, including required attributes (such as runat="server") and common attributes specific to a tag (such as *ID*, *DataSourceID*, *ControlToValidate*, and *Text*).</span></span>

<span data-ttu-id="819ca-946">코드 조각 추가, 다운로드 하거나 일반적인 작업에 대 한 사용자 또는 팀에서 사용 하는 태그의 블록을 캡슐화 하는 사용자 고유의 조각을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-946">You can download additional snippets, or you can write your own snippets that encapsulate the blocks of markup that you or your team use for common tasks.</span></span>

<a id="0.2__Toc224729054"></a><a id="0.2__Toc253429291"></a><a id="0.2__Toc243304662"></a>

### <a name="javascript-intellisense-enhancements"></a><span data-ttu-id="819ca-947">JavaScript IntelliSense의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="819ca-947">JavaScript IntelliSense Enhancements</span></span>

<span data-ttu-id="819ca-948">Visual 2010에서는 JavaScript IntelliSense도 다양 한 편집 환경을 제공할 수 있도록 다시 디자인 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-948">In Visual 2010, JavaScript IntelliSense has been redesigned to provide an even richer editing experience.</span></span> <span data-ttu-id="819ca-949">IntelliSense에서 동적으로 생성 된 메서드를 통해와 같은 개체를 이제 인식 *registerNamespace* 유사한 방법을 다른 JavaScript 프레임 워크에서 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-949">IntelliSense now recognizes objects that have been dynamically generated by methods such as *registerNamespace* and by similar techniques used by other JavaScript frameworks.</span></span> <span data-ttu-id="819ca-950">대용량 스크립트 라이브러리를 분석 하 고 IntelliSense를 거의 또는 전혀 처리 지연 표시 성능이 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-950">Performance has been improved to analyze large libraries of script and to display IntelliSense with little or no processing delay.</span></span> <span data-ttu-id="819ca-951">거의 모든 타사 라이브러리를 지원 하 고 다양 한 코딩 스타일을 지원 하도록 호환성 크게 증가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-951">Compatibility has been dramatically increased to support nearly all third-party libraries and to support diverse coding styles.</span></span> <span data-ttu-id="819ca-952">문서 주석은 입력 하 고 즉시 IntelliSense에서 활용 됩니다 이제 구문 분석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-952">Documentation comments are now parsed as you type and are immediately leveraged by IntelliSense.</span></span>

<a id="0.2__Toc224729055"></a><a id="0.2__Toc253429292"></a><a id="0.2__Toc243304663"></a>

## <a name="web-application-deployment-with-visual-studio-2010"></a><span data-ttu-id="819ca-953">Visual Studio 2010 웹 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="819ca-953">Web Application Deployment with Visual Studio 2010</span></span>

<span data-ttu-id="819ca-954">ASP.NET 개발자는 웹 응용 프로그램을 배포 하는 경우 종종을 찾게 나올 하면 다음과 같은 문제:</span><span class="sxs-lookup"><span data-stu-id="819ca-954">When ASP.NET developers deploy a Web application, they often find that they encounter issues such as the following:</span></span>

- <span data-ttu-id="819ca-955">공유 호스팅 사이트에 배포 하려면 느릴 수 있는 FTP 등의 기술 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-955">Deploying to a shared hosting site requires technologies such as FTP, which can be slow.</span></span> <span data-ttu-id="819ca-956">또한 데이터베이스를 구성 하는 SQL 스크립트를 실행 하는 등 작업을 수동으로 수행 해야 하 고 응용 프로그램으로 가상 디렉터리 폴더를 구성 하는 등의 IIS 설정을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-956">In addition, you must manually perform tasks such as running SQL scripts to configure a database and you must change IIS settings, such as configuring a virtual directory folder as an application.</span></span>
- <span data-ttu-id="819ca-957">웹 응용 프로그램 파일을 배포 하는 것 외에도, 엔터프라이즈 환경에서 관리자가 자주 해야 ASP.NET 구성 파일 및 IIS 설정을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-957">In an enterprise environment, in addition to deploying the Web application files, administrators frequently must modify ASP.NET configuration files and IIS settings.</span></span> <span data-ttu-id="819ca-958">데이터베이스 관리자는 일련의 실행 중인 응용 프로그램 데이터베이스를 가져올 SQL 스크립트를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-958">Database administrators must run a series of SQL scripts to get the application database running.</span></span> <span data-ttu-id="819ca-959">이러한 설치는 많은 수동 작업, 종종를 완료 하는 데 시간이 걸릴 신중 하 게 문서화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-959">Such installations are labor intensive, often take hours to complete, and must be carefully documented.</span></span>

<span data-ttu-id="819ca-960">Visual Studio 2010에는 이러한 문제를 해결 하 고 웹 응용 프로그램을 원활 하 게 배포할 수 있는 기술이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-960">Visual Studio 2010 includes technologies that address these issues and that let you seamlessly deploy Web applications.</span></span> <span data-ttu-id="819ca-961">이러한 기술 중 하나는 IIS 웹 배포 도구 (MsDeploy.exe)입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-961">One of these technologies is the IIS Web Deployment Tool (MsDeploy.exe).</span></span>

<span data-ttu-id="819ca-962">Visual Studio 2010의 웹 배포 기능에는 다음과 같은 주요 영역이 포함:</span><span class="sxs-lookup"><span data-stu-id="819ca-962">Web deployment features in Visual Studio 2010 include the following major areas:</span></span>

- <span data-ttu-id="819ca-963">웹 패키징</span><span class="sxs-lookup"><span data-stu-id="819ca-963">Web packaging</span></span>
- <span data-ttu-id="819ca-964">Web.config 변환</span><span class="sxs-lookup"><span data-stu-id="819ca-964">Web.config transformation</span></span>
- <span data-ttu-id="819ca-965">데이터베이스 배포</span><span class="sxs-lookup"><span data-stu-id="819ca-965">Database deployment</span></span>
- <span data-ttu-id="819ca-966">웹 응용 프로그램에 대 한 one-click 게시</span><span class="sxs-lookup"><span data-stu-id="819ca-966">One-click publish for Web applications</span></span>

<span data-ttu-id="819ca-967">다음 섹션에서는 이러한 기능에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-967">The following sections provide details about these features.</span></span>

<a id="0.2__Toc224729056"></a><a id="0.2__Toc253429293"></a><a id="0.2__Toc243304664"></a>

### <a name="web-packaging"></a><span data-ttu-id="819ca-968">웹 패키징</span><span class="sxs-lookup"><span data-stu-id="819ca-968">Web Packaging</span></span>

<span data-ttu-id="819ca-969">Visual Studio 2010가 MSDeploy 도구를 사용 하 여 응용 프로그램으로 참조 되는 압축된 (.zip) 파일을 만듭니다는 *웹 패키지*합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-969">Visual Studio 2010 uses the MSDeploy tool to create a compressed (.zip) file for your application, which is referred to as a *Web package*.</span></span> <span data-ttu-id="819ca-970">다음 콘텐츠 및 응용 프로그램에 대 한 메타 데이터를 포함 하는 패키지 파일:</span><span class="sxs-lookup"><span data-stu-id="819ca-970">The package file contains metadata about your application plus the following content:</span></span>

- <span data-ttu-id="819ca-971">응용 프로그램 풀 설정, 오류 페이지 설정 및에 포함 된 IIS 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-971">IIS settings, which includes application pool settings, error page settings, and so on.</span></span>
- <span data-ttu-id="819ca-972">실제 웹 콘텐츠: 웹 페이지, 사용자 정의 컨트롤, 정적 콘텐츠 (이미지 및 HTML 파일) 및 등을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-972">The actual Web content, which includes Web pages, user controls, static content (images and HTML files), and so on.</span></span>
- <span data-ttu-id="819ca-973">SQL Server 데이터베이스 스키마 및 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-973">SQL Server database schemas and data.</span></span>
- <span data-ttu-id="819ca-974">보안 인증서, GAC, 레지스트리 설정, 및 등에서 설치할 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-974">Security certificates, components to install in the GAC, registry settings, and so on.</span></span>

<span data-ttu-id="819ca-975">웹 패키지 모든 서버에 복사 하 고 IIS 관리자를 사용 하 여 수동으로 설치 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-975">A Web package can be copied to any server and then installed manually by using IIS Manager.</span></span> <span data-ttu-id="819ca-976">또는 자동화 된 배포 명령줄 명령을 사용 하 여 또는 배포 Api를 사용 하 여 패키지 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-976">Alternatively, for automated deployment, the package can be installed by using command-line commands or by using deployment APIs.</span></span>

<span data-ttu-id="819ca-977">Visual Studio 2010 기본 제공 웹 패키지를 만들 대상 및 MSBuild 작업을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-977">Visual Studio 2010 provides built in MSBuild tasks and targets to create Web packages.</span></span> <span data-ttu-id="819ca-978">자세한 내용은 참조 [ASP.NET 웹 응용 프로그램 프로젝트 배포 개요](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx) MSDN 웹 사이트 및 [웹 패키지를 만들어야 하면 10 + 20 이유](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html) Vishal Joshi 블로그.</span><span class="sxs-lookup"><span data-stu-id="819ca-978">For more information, see [ASP.NET Web Application Project Deployment Overview](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx) on the MSDN Web site and [10 + 20 reasons why you should create a Web Package](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729057"></a><a id="0.2__Toc253429294"></a><a id="0.2__Toc243304665"></a>

### <a name="webconfig-transformation"></a><span data-ttu-id="819ca-979">Web.config 변환</span><span class="sxs-lookup"><span data-stu-id="819ca-979">Web.config Transformation</span></span>

<span data-ttu-id="819ca-980">Visual Studio 2010 웹 응용 프로그램 배포에 대 한 소개 [XML 문서 변환 (XDT)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html), 변형할 수 있는 한 기능인는 `Web.config` 개발 설정에서 파일을 프로덕션 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-980">For Web application deployment, Visual Studio 2010 introduces [XML Document Transform (XDT)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html), which is a feature that lets you transform a `Web.config` file from development settings to production settings.</span></span> <span data-ttu-id="819ca-981">변환 설정은 명명 된 변환 파일에 지정 되어 `web.debug.config`, `web.release.config`등입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-981">Transformation settings are specified in transform files named `web.debug.config`, `web.release.config`, and so on.</span></span> <span data-ttu-id="819ca-982">(이러한 파일의 이름은 MSBuild 구성과 일치 합니다.) 변환 파일 포함 하는 배포 된을 해야 하는 변경 내용을 `Web.config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-982">(The names of these files match MSBuild configurations.) A transform file includes just the changes that you need to make to a deployed `Web.config` file.</span></span> <span data-ttu-id="819ca-983">간단한 구문을 사용 하 여 변경 내용을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-983">You specify the changes by using simple syntax.</span></span>

<span data-ttu-id="819ca-984">다음 예제에서는의 일부는 `web.release.config` 릴리스 구성의 배포에 대 한 파일 생성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-984">The following example shows a portion of a `web.release.config` file that might be produced for deployment of your release configuration.</span></span> <span data-ttu-id="819ca-985">대체 키워드 예에서 배포 하는 동안 지정는 *connectionString* 의 노드는 `Web.config` 파일 예제에 나와 있는 값으로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-985">The Replace keyword in the example specifies that during deployment the *connectionString* node in the `Web.config` file will be replaced with the values that are listed in the example.</span></span>

[!code-xml[Main](overview/samples/sample102.xml)]

<span data-ttu-id="819ca-986">자세한 내용은 참조 [웹 응용 프로그램 프로젝트 배포에 대 한 Web.config 변환 구문은](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx) msdn <a id="0.2_a"> </a> 웹 사이트 및[웹 배포: Web.Config 변환](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)Vishal Joshi 블로그.</span><span class="sxs-lookup"><span data-stu-id="819ca-986">For more information, see [Web.config Transformation Syntax for Web Application Project Deployment](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx) on the MSDN <a id="0.2_a"></a> Web site and[Web Deployment: Web.Config Transformation](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729058"></a><a id="0.2__Toc253429295"></a><a id="0.2__Toc243304666"></a>

### <a name="database-deployment"></a><span data-ttu-id="819ca-987">데이터베이스 배포</span><span class="sxs-lookup"><span data-stu-id="819ca-987">Database Deployment</span></span>

<span data-ttu-id="819ca-988">Visual Studio 2010 배포 패키지를 SQL Server 데이터베이스에 대 한 종속성을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-988">A Visual Studio 2010 deployment package can include dependencies on SQL Server databases.</span></span> <span data-ttu-id="819ca-989">패키지 정의의 일부로 원본 데이터베이스에 대 한 연결 문자열을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-989">As part of the package definition, you provide the connection string for your source database.</span></span> <span data-ttu-id="819ca-990">웹 패키지를 만들 때 Visual Studio 2010와 필요에 따라 데이터를 데이터베이스 스키마에 대 한 SQL 스크립트 생성 및 패키지에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-990">When you create the Web package, Visual Studio 2010 creates SQL scripts for the database schema and optionally for the data, and then adds these to the package.</span></span> <span data-ttu-id="819ca-991">사용자 지정 SQL 스크립트를 제공 하 고 서버에서 실행 해야 하는 순서를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-991">You can also provide custom SQL scripts and specify the sequence in which they should run on the server.</span></span> <span data-ttu-id="819ca-992">대상 서버에 대 한 적절 한 연결 문자열로 제공 하는 배포 시 배포 프로세스는 다음이 연결 문자열 사용 하 여 데이터베이스 스키마를 만들고 데이터를 추가 하는 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-992">At deployment time, you provide a connection string that is appropriate for the target server; the deployment process then uses this connection string to run the scripts that create the database schema and add the data.</span></span>

<span data-ttu-id="819ca-993">또한 한 번의 클릭을 사용 하 여 게시, 배포 응용 프로그램 원격 공유 호스팅 사이트에 게시 되 면 데이터베이스를 직접 게시할 수를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-993">In addition, by using one-click publish, you can configure deployment to publish your database directly when the application is published to a remote shared hosting site.</span></span> <span data-ttu-id="819ca-994">자세한 내용은 참조 [하는 방법: 한 데이터베이스와 웹 응용 프로그램 프로젝트를 배포](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx) MSDN 웹 사이트에서 및 [VS 2010에 데이터베이스 배포](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) Vishal Joshi 블로그.</span><span class="sxs-lookup"><span data-stu-id="819ca-994">For more information, see [How to: Deploy a Database With a Web Application Project](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx) on the MSDN Web site and [Database Deployment with VS 2010](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729059"></a><a id="0.2__Toc253429296"></a><a id="0.2__Toc243304667"></a>

### <a name="one-click-publish-for-web-applications"></a><span data-ttu-id="819ca-995">웹 응용 프로그램에 대 한 One-click 게시</span><span class="sxs-lookup"><span data-stu-id="819ca-995">One-Click Publish for Web Applications</span></span>

<span data-ttu-id="819ca-996">Visual Studio 2010에서는 IIS 원격 관리 서비스를 사용 하 여 원격 서버에 웹 응용 프로그램을 게시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-996">Visual Studio 2010 also lets you use the IIS remote management service to publish a Web application to a remote server.</span></span> <span data-ttu-id="819ca-997">또는 테스트 서버 / 스테이징 서버 호스팅 계정에 대 한 게시 프로필을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-997">You can create a publish profile for your hosting account or for testing servers or staging servers.</span></span> <span data-ttu-id="819ca-998">각 프로필은 적절 한 자격 증명을 안전 하 게 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-998">Each profile can save appropriate credentials securely.</span></span> <span data-ttu-id="819ca-999">다음에 대상 중 하나에 배포할 수 웹 한 번의 클릭을 사용 하 여 한 번의 클릭 서버 도구 모음을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-999">You can then deploy to any of the target servers with one click by using the Web one-click publish toolbar.</span></span> <span data-ttu-id="819ca-1000">Visual Studio 2010과 함께 MSBuild 명령줄을 사용 하 여 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-1000">With Visual Studio 2010, you can also publish by using the MSBuild command line.</span></span> <span data-ttu-id="819ca-1001">이렇게 하면 연속 통합 모델에 게시를 포함 하도록 팀 빌드 환경을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-1001">This lets you configure your team build environment to include publishing in a continuous-integration model.</span></span>

<span data-ttu-id="819ca-1002">자세한 내용은 참조 [하는 방법: 웹 응용 프로그램 프로젝트를 사용 하 여 한 번의 클릭 게시 및 웹 배포 배포](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx) MSDN 웹 사이트 및 [VS 2010 원클릭 게시 웹](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html) Vishal Joshi 블로그.</span><span class="sxs-lookup"><span data-stu-id="819ca-1002">For more information, see [How to: Deploy a Web Application Project Using One-Click Publish and Web Deploy](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx) on the MSDN Web site and [Web 1-Click Publish with VS 2010](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html) on Vishal Joshi's blog.</span></span> <span data-ttu-id="819ca-1003">Visual Studio 2010에서 웹 응용 프로그램 배포에 대 한 비디오 프레젠테이션을 보려면 참조 [VS 2010 웹 개발자 미리 보기에 대 한](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html) Vishal Joshi 블로그.</span><span class="sxs-lookup"><span data-stu-id="819ca-1003">To view video presentations about Web application deployment in Visual Studio 2010, see [VS 2010 for Web Developer Previews](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html) on Vishal Joshi's blog.</span></span>

<a id="0.2__Toc224729060"></a><a id="0.2__Toc253429297"></a><a id="0.2__Toc243304668"></a>

### <a name="resources"></a><span data-ttu-id="819ca-1004">자료</span><span class="sxs-lookup"><span data-stu-id="819ca-1004">Resources</span></span>

<span data-ttu-id="819ca-1005">다음 웹 사이트는 ASP.NET 4 및 Visual Studio 2010에 대 한 추가 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-1005">The following Web sites provide additional information about ASP.NET 4 and Visual Studio 2010.</span></span>

- <span data-ttu-id="819ca-1006">[ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) -MSDN 웹 사이트에서 ASP.NET 4에 대 한 공식 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-1006">[ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) — The official documentation for ASP.NET 4 on the MSDN Web site.</span></span>
- <span data-ttu-id="819ca-1007">[https://www.asp.net/](https://www.asp.net/) -ASP.NET 팀의 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-1007">[https://www.asp.net/](https://www.asp.net/) — The ASP.NET team's own Web site.</span></span>
- <span data-ttu-id="819ca-1008">[https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx) 및 [ASP.NET 동적 데이터 콘텐츠 맵](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx) -ASP.NET 팀 사이트 및 ASP.NET Dynamic Data에 대 한 공식 설명서의 온라인 리소스.</span><span class="sxs-lookup"><span data-stu-id="819ca-1008">[https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx) and [ASP.NET Dynamic Data Content Map](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx) — Online resources on the ASP.NET team site and in the official documentation for ASP.NET Dynamic Data.</span></span>
- <span data-ttu-id="819ca-1009">[https://www.asp.net/ajax/](../../ajax/index.md) ASP.NET Ajax 개발 — 주 웹 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-1009">[https://www.asp.net/ajax/](../../ajax/index.md) — The main Web resource for ASP.NET Ajax development.</span></span>
- <span data-ttu-id="819ca-1010">[https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/) Visual Studio 2010의 기능에 대 한 정보를 포함 하는 — Visual Web Developer 팀 블로그.</span><span class="sxs-lookup"><span data-stu-id="819ca-1010">[https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/) — The Visual Web Developer Team blog, which includes information about features in Visual Studio 2010.</span></span>
- <span data-ttu-id="819ca-1011">[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) -ASP.NET의 미리 보기 릴리스에 대 한 기본 웹 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-1011">[ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) — The main Web resource for preview releases of ASP.NET.</span></span>

<a id="0.2__Toc224729061"></a><a id="0.2__Toc253429298"></a><a id="0.2__Toc243304669"></a>

## <a name="disclaimer"></a><span data-ttu-id="819ca-1012">고지 사항</span><span class="sxs-lookup"><span data-stu-id="819ca-1012">Disclaimer</span></span>

<span data-ttu-id="819ca-1013">본 문서는 예비 문서이며, 여기에 설명한 소프트웨어의 최종 상업적 출시 전에 크게 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-1013">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="819ca-1014">이 문서에 포함된 정보는 게시 날짜 현재 논의된 문제에 대한 Microsoft Corporation의 당시 관점을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-1014">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="819ca-1015">Microsoft는 변화하는 시장 상황에 부응해야 하므로, Microsoft의 일부에 대한 책임으로 해석되어서는 안되며, 게시 날짜 이후 소개된 정보의 정확성을 Microsoft가 보증할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-1015">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="819ca-1016">이 백서는 정보 제공만을 목적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-1016">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="819ca-1017">Microsoft는 이 문서에 있는 정보에 대한 명시적 또는 묵시적, 법적인 보증을 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-1017">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="819ca-1018">해당 저작권법을 준수하는 것은 사용자의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-1018">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="819ca-1019">저작권에서의 권리와는 별도로, 이 설명서의 어떠한 부분도 Microsoft의 명시적인 서면 승인 없이는 어떠한 형식이나 수단(전기적, 기계적, 복사기에 의한 복사, 디스크 복사 또는 다른 방법) 또는 목적으로도 복제되거나, 검색 시스템에 저장 또는 도입되거나, 전송될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-1019">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="819ca-1020">Microsoft가 이 설명서 본안에 관련된 특허권, 상표권, 저작권 또는 기타 지적 재산권 등을 보유할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-1020">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="819ca-1021">서면 사용권 계약에 따라 Microsoft로부터 귀하에게 명시적으로 제공된 권리 이외에, 이 문서의 제공은 귀하에게 이러한 특허권, 상표권, 저작권, 또는 기타 지적 소유권 등에 대한 어떠한 사용권도 허여하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-1021">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="819ca-1022">다른 설명이 없는 한 예제 회사, 조직, 제품, 도메인 이름, 전자 메일 주소, 로고, 사람, 장소 및 이벤트 용례은 실제 데이터가 아닙니다과 연결 된 실제 회사, 조직, 제품, 도메인 이름, 전자 메일 주소, 로고, 사람, 장소 또는 이벤트 해서도 그렇게 유추 해서도 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-1022">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="819ca-1023">© 2009 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="819ca-1023">© 2009 Microsoft Corporation.</span></span> <span data-ttu-id="819ca-1024">All rights reserved.</span><span class="sxs-lookup"><span data-stu-id="819ca-1024">All rights reserved.</span></span>

<span data-ttu-id="819ca-1025">Microsoft 및 Windows는 미국 및/또는 기타 국가에서 Microsoft Corporation의 상표이거나 등록된 상표입니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-1025">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="819ca-1026">여기에 언급된 실제 회사와 제품의 이름은 각각 해당 소유자의 상표일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="819ca-1026">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>
