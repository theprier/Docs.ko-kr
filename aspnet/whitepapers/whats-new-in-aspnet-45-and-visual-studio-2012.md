---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: ASP.NET 4.5 및 Visual Studio 2012의 새로운 기능 | Microsoft Docs
author: rick-anderson
description: 이 문서에서는 새로운 기능 및 ASP.NET 4.5에서 도입 된 향상 된 기능을 설명 합니다. 웹 개발을 위해 수행 하는 향상 된 기능에 대해서도 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/29/2012
ms.topic: article
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: 16a2fa4b1b6617430703853543cbf29e18ba1103
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
ms.locfileid: "28886444"
---
<a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a><span data-ttu-id="7d3c6-104">ASP.NET 4.5 및 Visual Studio 2012의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="7d3c6-104">What's New in ASP.NET 4.5 and Visual Studio 2012</span></span>
====================
> <span data-ttu-id="7d3c6-105">이 문서에서는 새로운 기능 및 ASP.NET 4.5에서 도입 된 향상 된 기능을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-105">This document describes new features and enhancements that are being introduced in ASP.NET 4.5.</span></span> <span data-ttu-id="7d3c6-106">또한 Visual Studio 2012에서 웹 개발에 대해 수행 되는 향상 된 기능을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-106">It also describes improvements being made for web development in Visual Studio 2012.</span></span> <span data-ttu-id="7d3c6-107">이 문서를 2012 년 2 월 29 일에 원래 게시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-107">This document was originally published on February 29, 2012.</span></span>


- [<span data-ttu-id="7d3c6-108">ASP.NET Core 런타임 및 프레임 워크</span><span class="sxs-lookup"><span data-stu-id="7d3c6-108">ASP.NET Core Runtime and Framework</span></span>](#_Toc318097372)

    - [<span data-ttu-id="7d3c6-109">비동기적으로 읽고 쓰는 HTTP 요청 및 응답</span><span class="sxs-lookup"><span data-stu-id="7d3c6-109">Asynchronously Reading and Writing HTTP Requests and Responses</span></span>](#_Toc318097373)
    - [<span data-ttu-id="7d3c6-110">HttpRequest 처리의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="7d3c6-110">Improvements to HttpRequest handling</span></span>](#_Toc318097374)
    - [<span data-ttu-id="7d3c6-111">응답을 비동기적으로 플러시</span><span class="sxs-lookup"><span data-stu-id="7d3c6-111">Asynchronously flushing a response</span></span>](#_Toc318097375)
    - [<span data-ttu-id="7d3c6-112">에 대 한 지원 *await* 및 *작업*-기반 비동기 모듈과 처리기</span><span class="sxs-lookup"><span data-stu-id="7d3c6-112">Support for *await* and *Task*-Based Asynchronous Modules and Handlers</span></span>](#_Toc318097376)
    - [<span data-ttu-id="7d3c6-113">비동기 HTTP 모듈</span><span class="sxs-lookup"><span data-stu-id="7d3c6-113">Asynchronous HTTP modules</span></span>](#_Toc318097377)
    - [<span data-ttu-id="7d3c6-114">비동기 HTTP 처리기</span><span class="sxs-lookup"><span data-stu-id="7d3c6-114">Asynchronous HTTP handlers</span></span>](#_Toc318097378)
    - [<span data-ttu-id="7d3c6-115">새 ASP.NET 요청 유효성 검사 기능</span><span class="sxs-lookup"><span data-stu-id="7d3c6-115">New ASP.NET Request Validation Features</span></span>](#_Toc318097379)
    - [<span data-ttu-id="7d3c6-116">("지연") 요청 유효성 검사를 지연합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-116">Deferred ("lazy") request validation</span></span>](#_Toc318097380)
    - [<span data-ttu-id="7d3c6-117">유효성이 검사 되지 않은 요청에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="7d3c6-117">Support for unvalidated requests</span></span>](#_Toc318097381)
    - [<span data-ttu-id="7d3c6-118">AntiXSS 라이브러리</span><span class="sxs-lookup"><span data-stu-id="7d3c6-118">AntiXSS Library</span></span>](#_Toc318097382)
    - [<span data-ttu-id="7d3c6-119">Websocket 프로토콜에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="7d3c6-119">Support for WebSockets Protocol</span></span>](#_Toc318097383)
    - [<span data-ttu-id="7d3c6-120">묶음 및 축소</span><span class="sxs-lookup"><span data-stu-id="7d3c6-120">Bundling and Minification</span></span>](#_Toc318097384)
    - [<span data-ttu-id="7d3c6-121">웹 호스팅에 대 한 성능 향상</span><span class="sxs-lookup"><span data-stu-id="7d3c6-121">Performance Improvements for Web Hosting</span></span>](#_Toc_perf)

        - [<span data-ttu-id="7d3c6-122">핵심 성능 요소</span><span class="sxs-lookup"><span data-stu-id="7d3c6-122">Key Performance Factors</span></span>](#_Toc_perf_1)
        - [<span data-ttu-id="7d3c6-123">새로운 성능 기능에 대 한 요구 사항</span><span class="sxs-lookup"><span data-stu-id="7d3c6-123">Requirements for New Performance Features</span></span>](#_Toc_perf_2)
        - [<span data-ttu-id="7d3c6-124">일반적인 어셈블리 공유</span><span class="sxs-lookup"><span data-stu-id="7d3c6-124">Sharing Common Assemblies</span></span>](#_Toc_perf_3)
        - [<span data-ttu-id="7d3c6-125">빠른 시작에 대 한 멀티 코어 JIT 컴파일을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="7d3c6-125">Using multi-Core JIT compilation for faster startup</span></span>](#_Toc_perf_4)
        - [<span data-ttu-id="7d3c6-126">가비지 수집을 최적화 하기 위해 메모리를 튜닝 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-126">Tuning garbage collection to optimize for memory</span></span>](#_Toc_perf_5)
        - [<span data-ttu-id="7d3c6-127">웹 응용 프로그램 프리페치</span><span class="sxs-lookup"><span data-stu-id="7d3c6-127">Prefetching for web applications</span></span>](#_Toc_perf_6)
- [<span data-ttu-id="7d3c6-128">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="7d3c6-128">ASP.NET Web Forms</span></span>](#_Toc318097385)

    - [<span data-ttu-id="7d3c6-129">강력한 형식의 데이터 컨트롤</span><span class="sxs-lookup"><span data-stu-id="7d3c6-129">Strongly Typed Data Controls</span></span>](#_Toc318097386)
    - [<span data-ttu-id="7d3c6-130">모델 바인딩</span><span class="sxs-lookup"><span data-stu-id="7d3c6-130">Model Binding</span></span>](#_Toc318097387)

        - [<span data-ttu-id="7d3c6-131">데이터 선택</span><span class="sxs-lookup"><span data-stu-id="7d3c6-131">Selecting data</span></span>](#_Toc318097388)
        - [<span data-ttu-id="7d3c6-132">값 공급자</span><span class="sxs-lookup"><span data-stu-id="7d3c6-132">Value providers</span></span>](#_Toc318097389)
        - [<span data-ttu-id="7d3c6-133">컨트롤의 값으로 필터링</span><span class="sxs-lookup"><span data-stu-id="7d3c6-133">Filtering by values from a control</span></span>](#_Toc318097390)
    - [<span data-ttu-id="7d3c6-134">HTML로 인코딩된 데이터 바인딩 식</span><span class="sxs-lookup"><span data-stu-id="7d3c6-134">HTML Encoded Data-Binding Expressions</span></span>](#_Toc318097391)
    - [<span data-ttu-id="7d3c6-135">비 가시적인 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="7d3c6-135">Unobtrusive Validation</span></span>](#_Toc318097392)
    - [<span data-ttu-id="7d3c6-136">HTML5 업데이트</span><span class="sxs-lookup"><span data-stu-id="7d3c6-136">HTML5 Updates</span></span>](#_Toc318097393)
- [<span data-ttu-id="7d3c6-137">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="7d3c6-137">ASP.NET MVC 4</span></span>](#_Toc318097394)
- [<span data-ttu-id="7d3c6-138">ASP.NET 웹 페이지 2</span><span class="sxs-lookup"><span data-stu-id="7d3c6-138">ASP.NET Web Pages 2</span></span>](#_Toc318097395)
- [<span data-ttu-id="7d3c6-139">Visual Studio 2012 릴리스 후보</span><span class="sxs-lookup"><span data-stu-id="7d3c6-139">Visual Studio 2012 Release Candidate</span></span>](#_Toc318097396)

    - [<span data-ttu-id="7d3c6-140">Visual Studio 2010 및 Visual Studio 2012 릴리스 후보 (프로젝트 호환성) 간 공유 되는 프로젝트</span><span class="sxs-lookup"><span data-stu-id="7d3c6-140">Project Sharing Between Visual Studio 2010 and Visual Studio 2012 Release Candidate (Project Compatibility)</span></span>](#project-compatibility)
    - [<span data-ttu-id="7d3c6-141">ASP.NET 4.5 웹 사이트 템플릿의 구성 변경 내용</span><span class="sxs-lookup"><span data-stu-id="7d3c6-141">Configuration Changes in ASP.NET 4.5 Website Templates</span></span>](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [<span data-ttu-id="7d3c6-142">ASP.NET 라우팅에 대 한 IIS 7에서에서 기본적으로 지원</span><span class="sxs-lookup"><span data-stu-id="7d3c6-142">Native Support in IIS 7 for ASP.NET Routing</span></span>](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [<span data-ttu-id="7d3c6-143">HTML 편집기</span><span class="sxs-lookup"><span data-stu-id="7d3c6-143">HTML Editor</span></span>](#_Toc318097397)

        - [<span data-ttu-id="7d3c6-144">스마트 작업</span><span class="sxs-lookup"><span data-stu-id="7d3c6-144">Smart Tasks</span></span>](#_Toc318097398)
        - [<span data-ttu-id="7d3c6-145">WAI ARIA 지원</span><span class="sxs-lookup"><span data-stu-id="7d3c6-145">WAI-ARIA support</span></span>](#_Toc318097399)
        - [<span data-ttu-id="7d3c6-146">새 HTML5 조각</span><span class="sxs-lookup"><span data-stu-id="7d3c6-146">New HTML5 snippets</span></span>](#_Toc318097400)
        - [<span data-ttu-id="7d3c6-147">사용자 정의 컨트롤로 추출</span><span class="sxs-lookup"><span data-stu-id="7d3c6-147">Extract to user control</span></span>](#_Toc318097401)
        - [<span data-ttu-id="7d3c6-148">특성에 중요 코드에 대 한 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="7d3c6-148">IntelliSense for code nuggets in attributes</span></span>](#_Toc318097402)
        - [<span data-ttu-id="7d3c6-149">태그를 일치 하는 여는 태그 또는 닫는 태그의 이름을 바꾸면의 자동 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="7d3c6-149">Automatic renaming of matching tag when you rename an opening or closing tag</span></span>](#_Toc318097403)
        - [<span data-ttu-id="7d3c6-150">이벤트 처리기 생성</span><span class="sxs-lookup"><span data-stu-id="7d3c6-150">Event handler generation</span></span>](#_Toc318097404)
        - [<span data-ttu-id="7d3c6-151">스마트 들여쓰기</span><span class="sxs-lookup"><span data-stu-id="7d3c6-151">Smart indent</span></span>](#_Toc318097405)
        - [<span data-ttu-id="7d3c6-152">문 완성 자동 감소</span><span class="sxs-lookup"><span data-stu-id="7d3c6-152">Auto-reduce statement completion</span></span>](#_Toc318097406)
    - [<span data-ttu-id="7d3c6-153">JavaScript 편집기</span><span class="sxs-lookup"><span data-stu-id="7d3c6-153">JavaScript Editor</span></span>](#_Toc318097407)

        - [<span data-ttu-id="7d3c6-154">코드 개요</span><span class="sxs-lookup"><span data-stu-id="7d3c6-154">Code outlining</span></span>](#_Toc318097408)
        - [<span data-ttu-id="7d3c6-155">중괄호 일치</span><span class="sxs-lookup"><span data-stu-id="7d3c6-155">Brace matching</span></span>](#_Toc318097409)
        - [<span data-ttu-id="7d3c6-156">정의로 이동</span><span class="sxs-lookup"><span data-stu-id="7d3c6-156">Go to Definition</span></span>](#_Toc318097410)
        - [<span data-ttu-id="7d3c6-157">ECMAScript5 지원</span><span class="sxs-lookup"><span data-stu-id="7d3c6-157">ECMAScript5 support</span></span>](#_Toc318097411)
        - [<span data-ttu-id="7d3c6-158">DOM IntelliSense</span><span class="sxs-lookup"><span data-stu-id="7d3c6-158">DOM IntelliSense</span></span>](#_Toc318097412)
        - [<span data-ttu-id="7d3c6-159">VSDOC 서명이 오버 로드</span><span class="sxs-lookup"><span data-stu-id="7d3c6-159">VSDOC signature overloads</span></span>](#_Toc318097413)
        - [<span data-ttu-id="7d3c6-160">암시적 참조</span><span class="sxs-lookup"><span data-stu-id="7d3c6-160">Implicit references</span></span>](#_Toc318097414)
    - [<span data-ttu-id="7d3c6-161">CSS 편집기</span><span class="sxs-lookup"><span data-stu-id="7d3c6-161">CSS Editor</span></span>](#_Toc318097415)

        - [<span data-ttu-id="7d3c6-162">문 완성 자동 감소</span><span class="sxs-lookup"><span data-stu-id="7d3c6-162">Auto-reduce statement completion</span></span>](#_Toc318097416)
        - [<span data-ttu-id="7d3c6-163">계층적 들여쓰기입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-163">Hierarchical indentation.</span></span>](#_Toc318097417)
        - [<span data-ttu-id="7d3c6-164">CSS 해킹 지원</span><span class="sxs-lookup"><span data-stu-id="7d3c6-164">CSS hacks support</span></span>](#_Toc318097418)
        - [<span data-ttu-id="7d3c6-165">공급 업체 특정 스키마 (-moz-,-webkit)</span><span class="sxs-lookup"><span data-stu-id="7d3c6-165">Vendor specific schemas (-moz-,-webkit)</span></span>](#_Toc318097419)
        - [<span data-ttu-id="7d3c6-166">주석 및 주석 처리를 제거 지원</span><span class="sxs-lookup"><span data-stu-id="7d3c6-166">Commenting and uncommenting support</span></span>](#_Toc318097420)
        - [<span data-ttu-id="7d3c6-167">색 선택</span><span class="sxs-lookup"><span data-stu-id="7d3c6-167">Color picker</span></span>](#_Toc318097421)
        - [<span data-ttu-id="7d3c6-168">조각</span><span class="sxs-lookup"><span data-stu-id="7d3c6-168">Snippets</span></span>](#_Toc318097422)
        - [<span data-ttu-id="7d3c6-169">사용자 지정 영역</span><span class="sxs-lookup"><span data-stu-id="7d3c6-169">Custom regions</span></span>](#_Toc318097423)
    - [<span data-ttu-id="7d3c6-170">페이지 검사기</span><span class="sxs-lookup"><span data-stu-id="7d3c6-170">Page Inspector</span></span>](#_Toc318097424)
    - [<span data-ttu-id="7d3c6-171">Publishing</span><span class="sxs-lookup"><span data-stu-id="7d3c6-171">Publishing</span></span>](#_Toc318097425)

        - [<span data-ttu-id="7d3c6-172">게시 프로필</span><span class="sxs-lookup"><span data-stu-id="7d3c6-172">Publish profiles</span></span>](#_Toc318097426)
        - [<span data-ttu-id="7d3c6-173">ASP.NET 미리 컴파일 및 병합</span><span class="sxs-lookup"><span data-stu-id="7d3c6-173">ASP.NET precompilation and merge</span></span>](#_Toc318097427)
- [<span data-ttu-id="7d3c6-174">IIS Express</span><span class="sxs-lookup"><span data-stu-id="7d3c6-174">IIS Express</span></span>](#_Toc318097428)
- [<span data-ttu-id="7d3c6-175">Disclaimer</span><span class="sxs-lookup"><span data-stu-id="7d3c6-175">Disclaimer</span></span>](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a><span data-ttu-id="7d3c6-176">ASP.NET Core 런타임 및 프레임 워크</span><span class="sxs-lookup"><span data-stu-id="7d3c6-176">ASP.NET Core Runtime and Framework</span></span>

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a><span data-ttu-id="7d3c6-177">비동기적으로 읽고 쓰는 HTTP 요청 및 응답</span><span class="sxs-lookup"><span data-stu-id="7d3c6-177">Asynchronously Reading and Writing HTTP Requests and Responses</span></span>

<span data-ttu-id="7d3c6-178">ASP.NET 4로 사용 하 여 스트림의 HTTP 요청 엔터티를 읽을 수 있는 기능이 도입 된 *HttpRequest.GetBufferlessInputStream* 메서드.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-178">ASP.NET 4 introduced the ability to read an HTTP request entity as a stream using the *HttpRequest.GetBufferlessInputStream* method.</span></span> <span data-ttu-id="7d3c6-179">이 메서드는 요청 엔터티에 대 한 스트리밍 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-179">This method provided streaming access to the request entity.</span></span> <span data-ttu-id="7d3c6-180">그러나이 동기적으로 실행에서 스레드를 요청 기간에 대 한 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-180">However, it executed synchronously, which tied up a thread for the duration of a request.</span></span>

<span data-ttu-id="7d3c6-181">ASP.NET 4.5는 HTTP 요청 엔터티를 비동기적으로 스트림을 읽을 수 있으며 비동기적으로 플러시할 수를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-181">ASP.NET 4.5 supports the ability to read streams asynchronously on an HTTP request entity, and the ability to flush asynchronously.</span></span> <span data-ttu-id="7d3c6-182">ASP.NET 4.5 더블 버퍼 컨트롤러.aspx 페이지 처리기 및 ASP.NET MVC와 같은 다운스트림 HTTP 처리기와 쉽게 통합을 제공 하는 HTTP 요청 엔터티 수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-182">ASP.NET 4.5 also gives you the ability to double-buffer an HTTP request entity, which provides easier integration with downstream HTTP handlers such as .aspx page handlers and ASP.NET MVC controllers.</span></span>

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a><span data-ttu-id="7d3c6-183">HttpRequest 처리의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="7d3c6-183">Improvements to HttpRequest handling</span></span>

<span data-ttu-id="7d3c6-184">ASP.NET 4.5에 의해 반환 되는 스트림 참조 *HttpRequest.GetBufferlessInputStream* 동기 및 비동기 읽기 메서드를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-184">The Stream reference returned by ASP.NET 4.5 from *HttpRequest.GetBufferlessInputStream* supports both synchronous and asynchronous read methods.</span></span> <span data-ttu-id="7d3c6-185">*스트림* 에서 반환 된 개체 *GetBufferlessInputStream* 이제 BeginRead와 EndRead 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-185">The *Stream* object returned from *GetBufferlessInputStream* now implements both the BeginRead and EndRead methods.</span></span> <span data-ttu-id="7d3c6-186">비동기 *스트림* 메서드를 통해 ASP.NET 읽기는 비동기 루프의 각 반복 사이 현재 스레드를 해제 하는 동안 청크를 요청 엔터티를 비동기적으로 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-186">The asynchronous *Stream* methods let you asynchronously read the request entity in chunks, while ASP.NET releases the current thread between each iteration of an asynchronous read loop.</span></span>

<span data-ttu-id="7d3c6-187">ASP.NET 4.5에 버퍼링 된 방식으로 요청 엔터티를 읽기 위한 도우미 메서드 추가: *HttpRequest.GetBufferedInputStream*합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-187">ASP.NET 4.5 has also added a companion method for reading the request entity in a buffered way: *HttpRequest.GetBufferedInputStream*.</span></span> <span data-ttu-id="7d3c6-188">이 새 오버 로드와 비슷하게 작동 *GetBufferlessInputStream*, 동기 및 비동기 읽기를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-188">This new overload works like *GetBufferlessInputStream*, supporting both synchronous and asynchronous reads.</span></span> <span data-ttu-id="7d3c6-189">그러나, 읽으면서, *GetBufferedInputStream* 도 다운스트림 모듈과 처리기 요청 엔터티가 액세스할 여전히 수 있도록 엔터티 바이트 ASP.NET 내부 버퍼를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-189">However, as it reads, *GetBufferedInputStream* also copies the entity bytes into ASP.NET internal buffers so that downstream modules and handlers can still access the request entity.</span></span> <span data-ttu-id="7d3c6-190">예를 들어 일부 업스트림 파이프라인의 코드를 이미 읽은 사용 하 여 요청 엔터티 *GetBufferedInputStream*를 계속 사용할 수 있습니다 *HttpRequest.Form* 또는 *HttpRequest.Files*.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-190">For example, if some upstream code in the pipeline has already read the request entity using *GetBufferedInputStream*, you can still use *HttpRequest.Form* or *HttpRequest.Files*.</span></span> <span data-ttu-id="7d3c6-191">이렇게 하면 (예: 데이터베이스에 큰 파일 업로드를 스트리밍), 요청에서 비동기 처리를 수행 하지만 여전히 실행된.aspx 페이지 및 ASP.NET MVC controllers 나중에.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-191">This lets you perform asynchronous processing on a request (for example, streaming a large file upload to a database), but still run .aspx pages and MVC ASP.NET controllers afterward.</span></span>

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a><span data-ttu-id="7d3c6-192">응답을 비동기적으로 플러시</span><span class="sxs-lookup"><span data-stu-id="7d3c6-192">Asynchronously flushing a response</span></span>

<span data-ttu-id="7d3c6-193">HTTP 클라이언트에 대 한 응답을 보내는 클라이언트 멀리 떨어져 또는 낮은 대역폭 연결의 경우 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-193">Sending responses to an HTTP client can take considerable time when the client is far away or has a low-bandwidth connection.</span></span> <span data-ttu-id="7d3c6-194">일반적으로 ASP.NET 응용 프로그램에 의해 만들어지면 응답 바이트를 버퍼링 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-194">Normally ASP.NET buffers the response bytes as they are created by an application.</span></span> <span data-ttu-id="7d3c6-195">ASP.NET 요청 처리의 거의 마지막 계산 된 버퍼를 단일 전송 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-195">ASP.NET then performs a single send operation of the accrued buffers at the very end of request processing.</span></span>

<span data-ttu-id="7d3c6-196">주기적으로 호출 해야 버퍼링 된 응답 (예: 큰 파일을 클라이언트로 스트리밍) 크면 *HttpResponse.Flush* 클라이언트에 버퍼링 된 출력을 보내기 위해 메모리 사용을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-196">If the buffered response is large (for example, streaming a large file to a client), you must periodically call *HttpResponse.Flush* to send buffered output to the client and keep memory usage under control.</span></span> <span data-ttu-id="7d3c6-197">그러나 때문에 *플러시* 반복적으로 호출 하는 동기 호출 *플러시* 여전히 실행 시간이 긴 요청 중에 스레드를 소비 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-197">However, because *Flush* is a synchronous call, iteratively calling *Flush* still consumes a thread for the duration of potentially long-running requests.</span></span>

<span data-ttu-id="7d3c6-198">ASP.NET 4.5를 사용 하 여 비동기적으로 플러시합니다 수행에 대 한 지원을 추가 *BeginFlush* 및 *EndFlush* 의 메서드는 *HttpResponse* 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-198">ASP.NET 4.5 adds support for performing flushes asynchronously using the *BeginFlush* and *EndFlush* methods of the *HttpResponse* class.</span></span> <span data-ttu-id="7d3c6-199">이러한 메서드를 사용 하 여 비동기 모듈 및 증분 방식으로 데이터를 보내는 클라이언트에 운영 체제 스레드에 연결 하지 않고도 비동기 처리기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-199">Using these methods, you can create asynchronous modules and asynchronous handlers that incrementally send data to a client without tying up operating-system threads.</span></span> <span data-ttu-id="7d3c6-200">사이 *BeginFlush* 및 *EndFlush* 호출, ASP.NET 현재 스레드를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-200">In between *BeginFlush* and *EndFlush* calls, ASP.NET releases the current thread.</span></span> <span data-ttu-id="7d3c6-201">이 장기 실행 HTTP 다운로드를 지원 하기 위해 필요한 활성 스레드의 총 수를 크게 저하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-201">This substantially reduces the total number of active threads that are needed in order to support long-running HTTP downloads.</span></span>

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a><span data-ttu-id="7d3c6-202">에 대 한 지원 *await* 및 *작업* -기반 비동기 모듈과 처리기</span><span class="sxs-lookup"><span data-stu-id="7d3c6-202">Support for *await* and *Task* - Based Asynchronous Modules and Handlers</span></span>

<span data-ttu-id="7d3c6-203">.NET Framework 4 라고 하는 비동기 프로그래밍 개념을 도입는 *작업*합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-203">The .NET Framework 4 introduced an asynchronous programming concept referred to as a *task*.</span></span> <span data-ttu-id="7d3c6-204">작업으로 표시 됩니다는 *작업* 유형과 관련 된 형식을 *System.Threading.Tasks* 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-204">Tasks are represented by the *Task* type and related types in the *System.Threading.Tasks* namespace.</span></span> <span data-ttu-id="7d3c6-205">.NET Framework 4.5 작업할 수 있게 컴파일러 기능이 향상 된이 빌드 *작업* 개체 단순 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-205">The .NET Framework 4.5 builds on this with compiler enhancements that make working with *Task* objects simple.</span></span> <span data-ttu-id="7d3c6-206">.NET Framework 4.5에서 컴파일러는 두 개의 새로운 키워드를 지원: *await* 및 *비동기*합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-206">In the .NET Framework 4.5, the compilers support two new keywords: *await* and *async*.</span></span> <span data-ttu-id="7d3c6-207">*await* 키워드 구문의 줄임 표기를 나타내는 코드를 코드의 다른 부분에서 비동기적으로 대기 해야 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-207">The *await* keyword is syntactical shorthand for indicating that a piece of code should asynchronously wait on some other piece of code.</span></span> <span data-ttu-id="7d3c6-208">*비동기* 키워드 작업 기반 비동기 메서드로 메서드를 표시 하는 데 사용할 수 있는 힌트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-208">The *async* keyword represents a hint that you can use to mark methods as task-based asynchronous methods.</span></span>

<span data-ttu-id="7d3c6-209">조합의 *await*, *비동기*, 및 *작업* 개체를 사용 하면 훨씬 쉽게.NET 4.5에서 비동기 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-209">The combination of *await*, *async*, and the *Task* object makes it much easier for you to write asynchronous code in .NET 4.5.</span></span> <span data-ttu-id="7d3c6-210">ASP.NET 4.5 비동기 HTTP 모듈 및 향상 된 새 컴파일러를 사용 하 여 비동기 HTTP 처리기를 작성할 수 있는 새 Api와 이러한 단순화를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-210">ASP.NET 4.5 supports these simplifications with new APIs that let you write asynchronous HTTP modules and asynchronous HTTP handlers using the new compiler enhancements.</span></span>

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a><span data-ttu-id="7d3c6-211">비동기 HTTP 모듈</span><span class="sxs-lookup"><span data-stu-id="7d3c6-211">Asynchronous HTTP modules</span></span>

<span data-ttu-id="7d3c6-212">반환 하는 메서드 내에서 비동기 작업을 수행 하려는 경우는 *작업* 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-212">Suppose that you want to perform asynchronous work within a method that returns a *Task* object.</span></span> <span data-ttu-id="7d3c6-213">다음 코드 예제에서는 Microsoft 홈 페이지를 다운로드 하려면 비동기 호출을 실행 하는 비동기 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-213">The following code example defines an asynchronous method that makes an asynchronous call to download the Microsoft home page.</span></span> <span data-ttu-id="7d3c6-214">사용은 *비동기* 메서드 서명에 있는 키워드 및 *await* 에 대 한 호출 *DownloadStringTaskAsync*합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-214">Notice the use of the *async* keyword in the method signature and the *await* call to *DownloadStringTaskAsync*.</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

<span data-ttu-id="7d3c6-215">작성 해야 할 그-.NET Framework를 완료 하려면 다운로드를 기다리는 수 있을 뿐만 아니라 다운로드가 완료 된 후 호출 스택을 자동으로 복원 하는 동안 호출 스택 해제를 자동으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-215">That's all you have to write — the .NET Framework will automatically handle unwinding the call stack while waiting for the download to complete, as well as automatically restoring the call stack after the download is done.</span></span>

<span data-ttu-id="7d3c6-216">이제이 비동기 메서드를 사용 하 여 비동기 ASP.NET HTTP 모듈에서 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-216">Now suppose that you want to use this asynchronous method in an asynchronous ASP.NET HTTP module.</span></span> <span data-ttu-id="7d3c6-217">ASP.NET 4.5에는 도우미 메서드가 포함 되어 (*EventHandlerTaskAsyncHelper*) 및 새로운 대리자 형식 (*TaskEventHandler*)와 이전 작업 기반 비동기 메서드를 통합 하는 데 사용할 수 있는 비동기 프로그래밍 모델을 ASP.NET HTTP 파이프라인에 의해 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-217">ASP.NET 4.5 includes a helper method (*EventHandlerTaskAsyncHelper*) and a new delegate type (*TaskEventHandler*) that you can use to integrate task-based asynchronous methods with the older asynchronous programming model exposed by the ASP.NET HTTP pipeline.</span></span> <span data-ttu-id="7d3c6-218">이 예에서는 어떻게:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-218">This example shows how:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a><span data-ttu-id="7d3c6-219">비동기 HTTP 처리기</span><span class="sxs-lookup"><span data-stu-id="7d3c6-219">Asynchronous HTTP handlers</span></span>

<span data-ttu-id="7d3c6-220">ASP.NET에서 비동기 처리기를 작성 하는 일반적인 방법을 구현 하는 것은 *IHttpAsyncHandler* 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-220">The traditional approach to writing asynchronous handlers in ASP.NET is to implement the *IHttpAsyncHandler* interface.</span></span> <span data-ttu-id="7d3c6-221">ASP.NET 4.5 소개는 *HttpTaskAsyncHandler* 비동기 기본 형식에서 파생 될 수 있는 더욱 쉽게 비동기 처리기를 작성할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-221">ASP.NET 4.5 introduces the *HttpTaskAsyncHandler* asynchronous base type that you can derive from, which makes it much easier to write asynchronous handlers.</span></span>

<span data-ttu-id="7d3c6-222">*HttpTaskAsyncHandler* 형식이 추상 이며 재정의 해야는 *ProcessRequestAsync* 메서드.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-222">The *HttpTaskAsyncHandler* type is abstract and requires you to override the *ProcessRequestAsync* method.</span></span> <span data-ttu-id="7d3c6-223">내부적으로 ASP.NET을 맡고 반환 서명 통합 (한 *작업* 개체)의 *ProcessRequestAsync* ASP.NET 파이프라인에서 사용 하는 오래 된 비동기 프로그래밍 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-223">Internally ASP.NET takes care of integrating the return signature (a *Task* object) of *ProcessRequestAsync* with the older asynchronous programming model used by the ASP.NET pipeline.</span></span>

<span data-ttu-id="7d3c6-224">다음 예제에서는 사용 하는 방법을 보여 줍니다. *작업* 및 *await* 의 비동기 HTTP 처리기 구현의 일부로:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-224">The following example shows how you can use *Task* and *await* as part of the implementation of an asynchronous HTTP handler:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a><span data-ttu-id="7d3c6-225">새 ASP.NET 요청 유효성 검사 기능</span><span class="sxs-lookup"><span data-stu-id="7d3c6-225">New ASP.NET Request Validation Features</span></span>

<span data-ttu-id="7d3c6-226">기본적으로 ASP.NET 요청 유효성 검사를 수행-태그 또는 필드, 머리글, 쿠키 및 등의 스크립트에 대 한 요청을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-226">By default, ASP.NET performs request validation — it examines requests to look for markup or script in fields, headers, cookies, and so on.</span></span> <span data-ttu-id="7d3c6-227">검색 된 ASP.NET 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-227">If any is detected, ASP.NET throws an exception.</span></span> <span data-ttu-id="7d3c6-228">이 잠재적인 교차 사이트 스크립팅 공격을 막는 최전방의 첫 번째 줄으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-228">This acts as a first line of defense against potential cross-site scripting attacks.</span></span>

<span data-ttu-id="7d3c6-229">ASP.NET 4.5를 사용 하면 쉽게 선택적으로 유효성이 검사 되지 않은 요청 데이터를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-229">ASP.NET 4.5 makes it easy to selectively read unvalidated request data.</span></span> <span data-ttu-id="7d3c6-230">ASP.NET 4.5에는 또한 외부 라이브러리 였던 하는 인기 있는 AntiXSS 라이브러리를 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-230">ASP.NET 4.5 also integrates the popular AntiXSS library, which was formerly an external library.</span></span>

<span data-ttu-id="7d3c6-231">개발자가 응용 프로그램에 대 한 요청 유효성 검사를 선택적으로 해제 하는 기능에 대 한 질문과 대답가입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-231">Developers have frequently asked for the ability to selectively turn off request validation for their applications.</span></span> <span data-ttu-id="7d3c6-232">예를 들어 포럼 소프트웨어 응용 프로그램을 사용 하는 경우 사용자가 다른 모든 요청 유효성 검사는 하는지 여부를 확인 하지만 HTML 형식의 포럼 게시물 및 의견을 제출 하도록 허용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-232">For example, if your application is forum software, you might want to allow users to submit HTML-formatted forum posts and comments, but still make sure that request validation is checking everything else.</span></span>

<span data-ttu-id="7d3c6-233">ASP.NET 4.5 쉽게 유효성이 검사 되지 않은 입력을 선택 하 여 작업할 수 있도록 하는 두 가지 기능을 소개: ("지연") 요청 유효성 검사 및 유효성이 검사 되지 않은 요청 데이터에 대 한 액세스를 지연 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-233">ASP.NET 4.5 introduces two features that make it easy for you to selectively work with unvalidated input: deferred ("lazy") request validation and access to unvalidated request data.</span></span>

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a><span data-ttu-id="7d3c6-234">("지연") 요청 유효성 검사를 지연합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-234">Deferred ("lazy") request validation</span></span>

<span data-ttu-id="7d3c6-235">ASP.NET 4.5에서 기본적으로 모든 요청 데이터를 요청 유효성 검사가 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-235">In ASP.NET 4.5, by default all request data is subject to request validation.</span></span> <span data-ttu-id="7d3c6-236">그러나 응용 프로그램 요청 데이터를 실제로 액세스 될 때까지 요청 유효성 검사를 연기을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-236">However, you can configure the application to defer request validation until you actually access request data.</span></span> <span data-ttu-id="7d3c6-237">(이 라고도 지연 요청 유효성 검사를 특정 데이터 시나리오에 대 한 지연 로딩이 등의 용어를 기반으로 합니다.) 지연 된 유효성 검사를 설정 하 여 Web.config 파일에서 사용 하는 응용 프로그램을 구성할 수 있습니다는 *requestValidationMode* 특성에서 4.5로는 *httpRUntime* 다음 예제와 같이 요소:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-237">(This is sometimes referred to as lazy request validation, based on terms like lazy loading for certain data scenarios.) You can configure the application to use deferred validation in the Web.config file by setting the *requestValidationMode* attribute to 4.5 in the *httpRUntime* element, as in the following example:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

<span data-ttu-id="7d3c6-238">요청 유효성 검사 모드 4.5로 설정 되 면 요청 유효성 검사는 특정 요청 값에 대해서만 하 고 코드 해당 값에 액세스 하는 경우에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-238">When request validation mode is set to 4.5, request validation is triggered only for a specific request value and only when your code accesses that value.</span></span> <span data-ttu-id="7d3c6-239">예를 들어, 코드 Request.Form["forum의 값을 설정 하는 경우\_게시"], 폼 컬렉션의 해당 요소에 대 한 요청 유효성 검사를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-239">For example, if your code gets the value of Request.Form["forum\_post"], request validation is invoked only for that element in the form collection.</span></span> <span data-ttu-id="7d3c6-240">다른 요소는 *양식* 컬렉션에 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-240">None of the other elements in the *Form* collection are validated.</span></span> <span data-ttu-id="7d3c6-241">이전 버전의 ASP.NET에서는 요청 유효성 검사 컬렉션에 있는 모든 요소를 액세스 하는 경우에 전체 요청 컬렉션에 대 한 트리거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-241">In previous versions of ASP.NET, request validation was triggered for the entire request collection when any element in the collection was accessed.</span></span> <span data-ttu-id="7d3c6-242">새 동작을 통해 다른 응용 프로그램 구성 요소를 다른 부분에 대해 요청 유효성 검사를 트리거하지 않고 요청 데이터의 다양 한 요소를 살펴보는 쉽게 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-242">The new behavior makes it easier for different application components to look at different pieces of request data without triggering request validation on other pieces.</span></span>

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a><span data-ttu-id="7d3c6-243">유효성이 검사 되지 않은 요청에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="7d3c6-243">Support for unvalidated requests</span></span>

<span data-ttu-id="7d3c6-244">지연 된 요청 유효성 검사만 선택적으로 요청 유효성 검사를 생략의 문제를 해결 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-244">Deferred request validation alone doesn't solve the problem of selectively bypassing request validation.</span></span> <span data-ttu-id="7d3c6-245">Request.Form["forum에 대 한 호출\_게시"] 트리거 해당 특정 요청 값에 대 한 유효성 검사를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-245">The call to Request.Form["forum\_post"] still triggers request validation for that specific request value.</span></span> <span data-ttu-id="7d3c6-246">그러나 다음 해당 필드에 태그를 허용 하려고 하기 때문에 유효성 검사를 트리거하지 않고이 필드에 액세스 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-246">However, you might want to access this field without triggering validation because you want to allow markup in that field.</span></span>

<span data-ttu-id="7d3c6-247">이 허용 하려면 ASP.NET 4.5 이제 요청 데이터에 대 한 유효성이 검사 되지 않은 액세스를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-247">To allow this, ASP.NET 4.5 now supports unvalidated access to request data.</span></span> <span data-ttu-id="7d3c6-248">ASP.NET 4.5 포함 새 *Unvalidated* 컬렉션 속성에는 *HttpRequest* 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-248">ASP.NET 4.5 includes a new *Unvalidated* collection property in the *HttpRequest* class.</span></span> <span data-ttu-id="7d3c6-249">이 컬렉션의 모든 요청 데이터의 공통 값에 대 한 액세스를 같은 제공 *양식*, *QueryString*, *쿠키*, 및 *Url*합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-249">This collection provides access to all of the common values of request data, like *Form*, *QueryString*, *Cookies*, and *Url*.</span></span>

<span data-ttu-id="7d3c6-250">포럼 예제를 사용 하 여 유효성이 검사 되지 않은 요청 데이터를 읽을 수를 먼저 구성 해야 새 요청 유효성 검사 모드를 사용 하도록 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-250">Using the forum example, to be able to read unvalidated request data, you first need to configure the application to use the new request validation mode:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

<span data-ttu-id="7d3c6-251">그런 다음 사용할 수는 *HttpRequest.Unvalidated* 유효성이 검사 되지 않은 폼 값을 읽을 속성:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-251">You can then use the *HttpRequest.Unvalidated* property to read the unvalidated form value:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]


> [!WARNING]
> <span data-ttu-id="7d3c6-252">보안- *주의 하 여 유효성이 검사 되지 않은 요청 데이터를 사용 하 여!*</span><span class="sxs-lookup"><span data-stu-id="7d3c6-252">Security - *Use unvalidated request data with care!*</span></span> <span data-ttu-id="7d3c6-253">ASP.NET 4.5 유효성이 검사 되지 않은 요청 속성과 쉽게 매우 구체적인 유효성이 검사 되지 않은 요청 데이터에 액세스할 수 있도록 컬렉션에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-253">ASP.NET 4.5 added the unvalidated request properties and collections to make it easier for you to access very specific unvalidated request data.</span></span> <span data-ttu-id="7d3c6-254">그러나 여전히 사용자 지정 유효성 검사에서는 원시 요청 데이터를 사용자에 게 위험한 텍스트 렌더링 되지 않습니다에서 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-254">However, you must still perform custom validation on the raw request data to ensure that dangerous text is not rendered to users.</span></span>


<a id="_Toc318097382"></a>
### <a name="antixss-library"></a><span data-ttu-id="7d3c6-255">AntiXSS 라이브러리</span><span class="sxs-lookup"><span data-stu-id="7d3c6-255">AntiXSS Library</span></span>

<span data-ttu-id="7d3c6-256">Microsoft AntiXSS 라이브러리의 인기도 인해 이제 ASP.NET 4.5 버전 4.0 해당 라이브러리에서 core 인코딩 루틴에 통합 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-256">Due to the popularity of the Microsoft AntiXSS Library, ASP.NET 4.5 now incorporates core encoding routines from version 4.0 of that library.</span></span>

<span data-ttu-id="7d3c6-257">인코딩 루틴에서 구현 되는 *AntiXssEncoder* 새 형식 *System.Web.Security.AntiXss* 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-257">The encoding routines are implemented by the *AntiXssEncoder* type in the new *System.Web.Security.AntiXss* namespace.</span></span> <span data-ttu-id="7d3c6-258">사용할 수는 *AntiXssEncoder* 형식에서 구현 되는 인코딩 정적 메서드 중 하나를 호출 하 여 직접 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-258">You can use the *AntiXssEncoder* type directly by calling any of the static encoding methods that are implemented in the type.</span></span> <span data-ttu-id="7d3c6-259">그러나 새 앤티 XSS 루틴을 사용 하기 위한 가장 쉬운 방법을 사용 하도록 ASP.NET 응용 프로그램을 구성 하는 것은 *AntiXssEncoder* 기본적으로 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-259">However, the easiest approach for using the new anti-XSS routines is to configure an ASP.NET application to use the *AntiXssEncoder* class by default.</span></span> <span data-ttu-id="7d3c6-260">이 위해 Web.config 파일에 다음 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-260">To do this, add the following attribute to the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

<span data-ttu-id="7d3c6-261">때는 *encoderType* 특성은 사용 하도록 설정 되는 *AntiXssEncoder* 유형, 모든 출력을 새 인코딩 루틴을 사용 하 여 ASP.NET에서 자동으로 인코딩.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-261">When the *encoderType* attribute is set to use the *AntiXssEncoder* type, all output encoding in ASP.NET automatically uses the new encoding routines.</span></span>

<span data-ttu-id="7d3c6-262">다음은 외부 AntiXSS 라이브러리 부분에 ASP.NET 4.5에 통합 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-262">These are the portions of the external AntiXSS library that have been incorporated into ASP.NET 4.5:</span></span>

- <span data-ttu-id="7d3c6-263">*HtmlEncode*, *HtmlFormUrlEncode*, 및 *HtmlAttributeEncode*</span><span class="sxs-lookup"><span data-stu-id="7d3c6-263">*HtmlEncode*, *HtmlFormUrlEncode*, and *HtmlAttributeEncode*</span></span>
- <span data-ttu-id="7d3c6-264">*XmlAttributeEncode* 및 *XmlEncode*</span><span class="sxs-lookup"><span data-stu-id="7d3c6-264">*XmlAttributeEncode* and *XmlEncode*</span></span>
- <span data-ttu-id="7d3c6-265">*UrlEncode* 및 *UrlPathEncode* (새로 만들기)</span><span class="sxs-lookup"><span data-stu-id="7d3c6-265">*UrlEncode* and *UrlPathEncode* (new)</span></span>
- <span data-ttu-id="7d3c6-266">*CssEncode*</span><span class="sxs-lookup"><span data-stu-id="7d3c6-266">*CssEncode*</span></span>

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a><span data-ttu-id="7d3c6-267">Websocket 프로토콜에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="7d3c6-267">Support for WebSockets Protocol</span></span>

<span data-ttu-id="7d3c6-268">Websocket 프로토콜은 HTTP를 통해 클라이언트와 서버 간의 안전 하 고 실시간 양방향 통신을 설정 하는 방법을 정의 하는 표준 기반 네트워크 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-268">WebSockets protocol is a standards-based network protocol that defines how to establish secure, real-time bidirectional communications between a client and a server over HTTP.</span></span> <span data-ttu-id="7d3c6-269">Microsoft는 IETF와 W3C 표준 기관 프로토콜을 정의할 수 있도록와 협력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-269">Microsoft has worked with both the IETF and W3C standards bodies to help define the protocol.</span></span> <span data-ttu-id="7d3c6-270">Websocket 프로토콜은 클라이언트와 모바일 운영 체제 모두에서 Websocket 프로토콜을 지 원하는 많은 리소스를 투자 하는 Microsoft와 모든 클라이언트 (뿐 아니라 브라우저)에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-270">The WebSockets protocol is supported by any client (not just browsers), with Microsoft investing substantial resources supporting WebSockets protocol on both client and mobile operating systems.</span></span>

<span data-ttu-id="7d3c6-271">Websocket 프로토콜을 사용 하면 훨씬 쉽게는 클라이언트와 서버 간에 실행 시간이 긴 데이터 전송을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-271">WebSockets protocol makes it much easier to create long-running data transfers between a client and a server.</span></span> <span data-ttu-id="7d3c6-272">예를 들어, 채팅 응용 프로그램을 작성 되므로 훨씬 더 쉽게 클라이언트와 서버 간의 true 실행 시간이 긴 연결을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-272">For example, writing a chat application is much easier because you can establish a true long-running connection between a client and a server.</span></span> <span data-ttu-id="7d3c6-273">정기 폴링을 또는 HTTP 긴 폴링 소켓의 동작을 시뮬레이션할과 같은 대안을 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-273">You do not have to resort to workarounds like periodic polling or HTTP long-polling to simulate the behavior of a socket.</span></span>

<span data-ttu-id="7d3c6-274">ASP.NET 4.5 및 IIS 8 사용 등이 부분적으로 Websocket 지원, ASP.NET 개발자가 비동기적으로 읽고 문자열 및 이진 데이터를 모두 Websocket 개체에 쓰기 위한 관리 되는 Api를 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-274">ASP.NET 4.5 and IIS 8 include low-level WebSockets support, enabling ASP.NET developers to use managed APIs for asynchronously reading and writing both string and binary data on a WebSockets object.</span></span> <span data-ttu-id="7d3c6-275">ASP.NET 4.5는 새 *System.Web.WebSockets* Websocket 프로토콜을 사용 하기 위한 형식이 포함 된 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-275">For ASP.NET 4.5, there is a new *System.Web.WebSockets* namespace that contains types for working with WebSockets protocol.</span></span>

<span data-ttu-id="7d3c6-276">DOM을 만들어 Websocket 연결을 설정 하는 브라우저 클라이언트가 *WebSocket* 다음 예제와 같이 ASP.NET 응용 프로그램에서 URL을 가리키는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-276">A browser client establishes a WebSockets connection by creating a DOM *WebSocket* object that points to a URL in an ASP.NET application, as in the following example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

<span data-ttu-id="7d3c6-277">모든 종류의 모듈 또는 처리기를 사용 하 여 ASP.NET에서 Websocket 끝점을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-277">You can create WebSockets endpoints in ASP.NET using any kind of module or handler.</span></span> <span data-ttu-id="7d3c6-278">앞의 예에서.ashx 파일 처리기를 만들 수는 신속 하 게 되므로.ashx 파일 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-278">In the previous example, an .ashx file was used, because .ashx files are a quick way to create a handler.</span></span>

<span data-ttu-id="7d3c6-279">Websocket 프로토콜에 따라 ASP.NET 응용 프로그램을 요청 해야으로 업그레이드할 수 HTTP GET 요청 으로부터 Websocket 요청을 지정 하 여 클라이언트의 Websocket 요청을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-279">According to the WebSockets protocol, an ASP.NET application accepts a client's WebSockets request by indicating that the request should be upgraded from an HTTP GET request to a WebSockets request.</span></span> <span data-ttu-id="7d3c6-280">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-280">Here's an example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

<span data-ttu-id="7d3c6-281">*AcceptWebSocketRequest* ASP.NET 현재 HTTP 요청을 해제 하 고 다음 제어 하는 함수 대리자를 전달 하기 때문에 메서드는 함수 대리자를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-281">The *AcceptWebSocketRequest* method accepts a function delegate because ASP.NET unwinds the current HTTP request and then transfers control to the function delegate.</span></span> <span data-ttu-id="7d3c6-282">개념적으로이 방법은 사용 하는 방법에 비슷한 *System.Threading.Thread*, 여기서는 백그라운드에서 수행 되는 작업이 스레드 시작 대리자를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-282">Conceptually this approach is similar to how you use *System.Threading.Thread*, where you define a thread-start delegate in which background work is performed.</span></span>

<span data-ttu-id="7d3c6-283">ASP.NET 및 클라이언트 Websocket 핸드셰이크 성공적으로 완료, 사용자 대리자를 호출 하는 ASP.NET 및 Websocket 응용 프로그램 실행을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-283">After ASP.NET and the client have successfully completed a WebSockets handshake, ASP.NET calls your delegate and the WebSockets application starts running.</span></span> <span data-ttu-id="7d3c6-284">다음 코드 예제에서는 기본 Websocket 지원에는 ASP.NET에서 사용 하는 간단한 에코 응용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-284">The following code example shows a simple echo application that uses the built-in WebSockets support in ASP.NET:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

<span data-ttu-id="7d3c6-285">지원에 대 한.NET 4.5에는 *await* 키워드 및 작업 기반 비동기 작업은 적합 한 Websocket 응용 프로그램을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-285">The support in .NET 4.5 for the *await* keyword and asynchronous task-based operations is a natural fit for writing WebSockets applications.</span></span> <span data-ttu-id="7d3c6-286">코드 예제에서는 ASP.NET 내부 Websocket 요청을 완전히 비동기적으로 실행 되는지 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-286">The code example shows that a WebSockets request runs completely asynchronously inside ASP.NET.</span></span> <span data-ttu-id="7d3c6-287">응용 프로그램을 호출 하 여 클라이언트에서 전송 될 메시지를 비동기적으로 기다립니다. *소켓을 기다립니다. ReceiveAsync*합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-287">The application waits asynchronously for a message to be sent from a client by calling *await socket.ReceiveAsync*.</span></span> <span data-ttu-id="7d3c6-288">호출 하 여 클라이언트를 비동기 메시지를 보낼 수는 마찬가지로, *소켓을 기다립니다. SendAsync*합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-288">Similarly, you can send an asynchronous message to a client by calling *await socket.SendAsync*.</span></span>

<span data-ttu-id="7d3c6-289">브라우저에서 응용 프로그램을 통해 Websocket 메시지를 받는 *onmessage* 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-289">In the browser, an application receives WebSockets messages through an *onmessage* function.</span></span> <span data-ttu-id="7d3c6-290">호출 브라우저에서 메시지를 보내려고는 *보낼* 의 메서드는 *WebSocket* 이 예제에 나와 있는 것 처럼 DOM 유형:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-290">To send a message from a browser, you call the *send* method of the *WebSocket* DOM type, as shown in this example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

<span data-ttu-id="7d3c6-291">나중에이 추상 자리를 비울 하위 수준 코딩 즉 중 일부에 필요한이 기능을이 릴리스 WebSockets에 대 한 응용 프로그램에 대 한 업데이트 출시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-291">In the future, we might release updates to this functionality that abstract away some of the low-level coding that is required in this release for WebSockets applications.</span></span>

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a><span data-ttu-id="7d3c6-292">묶음 및 축소</span><span class="sxs-lookup"><span data-stu-id="7d3c6-292">Bundling and Minification</span></span>

<span data-ttu-id="7d3c6-293">번들로 단일 파일 처럼 처리 될 수 있는 번들에서 개별 JavaScript 및 CSS 파일 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-293">Bundling lets you combine individual JavaScript and CSS files into a bundle that can be treated like a single file.</span></span> <span data-ttu-id="7d3c6-294">축소 공백 및 필요 하지 않은 다른 문자를 제거 하 여 JavaScript 및 CSS 파일을 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-294">Minification condenses JavaScript and CSS files by removing whitespace and other characters that are not required.</span></span> <span data-ttu-id="7d3c6-295">이러한 기능은 웹 페이지, Web Forms 및 ASP.NET MVC와 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-295">These features work with Web Forms, ASP.NET MVC, and Web Pages.</span></span>

<span data-ttu-id="7d3c6-296">번들 번들 클래스 또는 해당 자식 클래스, ScriptBundle 및 StyleBundle 중 하나를 사용 하 여 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-296">Bundles are created using the Bundle class or one of its child classes, ScriptBundle and StyleBundle.</span></span> <span data-ttu-id="7d3c6-297">번들의 인스턴스를 구성 했으면 번들 전역 BundleCollection 인스턴스를 추가 하기만 하면에 들어오는 요청에 사용할이 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-297">After configuring an instance of a bundle, the bundle is made available to incoming requests by simply adding it to a global BundleCollection instance.</span></span> <span data-ttu-id="7d3c6-298">기본 서식 파일에 번들 구성은 BundleConfig 파일에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-298">In the default templates, bundle configuration is performed in a BundleConfig file.</span></span> <span data-ttu-id="7d3c6-299">이 기본 구성의 모든 핵심 스크립트 및 템플릿을 사용 하는 css 파일에 대 한 번들을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-299">This default configuration creates bundles for all of the core scripts and css files used by the templates.</span></span>

<span data-ttu-id="7d3c6-300">번들은 몇 가지 가능한 도우미 메서드 중 하나를 사용 하 여 뷰 내에서 참조 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-300">Bundles are referenced from within views by using one of a couple possible helper methods.</span></span> <span data-ttu-id="7d3c6-301">디버그와 릴리스 모드에서에서 번들에 대 한 다른 태그 렌더링을 지원 하기 위해 ScriptBundle 및 StyleBundle 클래스에는 도우미 메서드를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-301">In order to support rendering different markup for a bundle when in debug vs. release mode, the ScriptBundle and StyleBundle classes have the helper method, Render.</span></span> <span data-ttu-id="7d3c6-302">디버그 모드일 때는 렌더링에서 번들의 각 리소스에 대 한 태그를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-302">When in debug mode, Render will generate markup for each resource in the bundle.</span></span> <span data-ttu-id="7d3c6-303">릴리스 모드에서 렌더링 전체 번들에 대 한 단일 태그 요소를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-303">When in release mode, Render will generate a single markup element for the entire bundle.</span></span> <span data-ttu-id="7d3c6-304">설정/해제 디버그 및 릴리스 간의 모드 아래와 같이 web.config에서 컴파일 요소의 디버그 특성을 수정 하 여 구현 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-304">Toggling between debug and release mode can be accomplished by modifying the debug attribute of the compilation element in web.config as shown below:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

<span data-ttu-id="7d3c6-305">또한 활성화 또는 비활성화 최적화 BundleTable.EnableOptimizations 속성을 통해 직접 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-305">Additionally, enabling or disabling optimization can be set directly via the BundleTable.EnableOptimizations property.</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

<span data-ttu-id="7d3c6-306">파일을 번들로 제공 되는 경우 먼저 알파벳 순서로 (에 표시 되는 방식을 **솔루션 탐색기**).</span><span class="sxs-lookup"><span data-stu-id="7d3c6-306">When files are bundled, they are first sorted alphabetically (the way they are displayed in **Solution Explorer**).</span></span> <span data-ttu-id="7d3c6-307">다음 구성 된 라이브러리를 알 수 있도록 하 고 해당 사용자 지정 확장 프로그램 (예: jQuery, MooTools, Dojo) 가장 먼저 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-307">They are then organized so that known libraries and their custom extensions (such as jQuery, MooTools, and Dojo) are loaded first.</span></span> <span data-ttu-id="7d3c6-308">예를 들어 위와 같이 Scripts 폴더의 번들에 대 한 최종 순서가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-308">For example, the final order for the bundling of the Scripts folder as shown above will be:</span></span>

1. <span data-ttu-id="7d3c6-309">jquery-1.6.2.js</span><span class="sxs-lookup"><span data-stu-id="7d3c6-309">jquery-1.6.2.js</span></span>
2. <span data-ttu-id="7d3c6-310">jquery-ui.js</span><span class="sxs-lookup"><span data-stu-id="7d3c6-310">jquery-ui.js</span></span>
3. <span data-ttu-id="7d3c6-311">jquery.tools.js</span><span class="sxs-lookup"><span data-stu-id="7d3c6-311">jquery.tools.js</span></span>
4. <span data-ttu-id="7d3c6-312">a.js</span><span class="sxs-lookup"><span data-stu-id="7d3c6-312">a.js</span></span>

<span data-ttu-id="7d3c6-313">CSS 파일도 사전순으로 정렬 되며 다음 reset.css 및 normalize.css 다른 파일 앞에 야 있도록 다시 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-313">CSS files are also sorted alphabetically and then reorganized so that reset.css and normalize.css come before any other file.</span></span> <span data-ttu-id="7d3c6-314">위에 표시 된 Styles 폴더의 번들의 최종 정렬이이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-314">The final sorting of the bundling of the Styles folder shown above will be this:</span></span>

1. <span data-ttu-id="7d3c6-315">reset.css</span><span class="sxs-lookup"><span data-stu-id="7d3c6-315">reset.css</span></span>
2. <span data-ttu-id="7d3c6-316">content.css</span><span class="sxs-lookup"><span data-stu-id="7d3c6-316">content.css</span></span>
3. <span data-ttu-id="7d3c6-317">forms.css</span><span class="sxs-lookup"><span data-stu-id="7d3c6-317">forms.css</span></span>
4. <span data-ttu-id="7d3c6-318">globals.css</span><span class="sxs-lookup"><span data-stu-id="7d3c6-318">globals.css</span></span>
5. <span data-ttu-id="7d3c6-319">menu.css</span><span class="sxs-lookup"><span data-stu-id="7d3c6-319">menu.css</span></span>
6. <span data-ttu-id="7d3c6-320">styles.css</span><span class="sxs-lookup"><span data-stu-id="7d3c6-320">styles.css</span></span>

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a><span data-ttu-id="7d3c6-321">웹 호스팅에 대 한 성능 향상</span><span class="sxs-lookup"><span data-stu-id="7d3c6-321">Performance Improvements for Web Hosting</span></span>

<span data-ttu-id="7d3c6-322">.NET Framework 4.5 및 Windows 8 웹 서버 워크 로드에 대 한 상당한 성능 향상을 달성 하는 데 도움이 되는 기능을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-322">The .NET Framework 4.5 and Windows 8 introduce features that can help you achieve a significant performance boost for web-server workloads.</span></span> <span data-ttu-id="7d3c6-323">여기에 감소 (최대 35%) 모두 시작 시간 및 웹 호스팅 ASP.NET을 사용 하는 사이트의 메모리 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-323">This includes a reduction (up to 35%) in both startup time and in the memory footprint of web hosting sites that use ASP.NET.</span></span>

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a><span data-ttu-id="7d3c6-324">핵심 성능 요소</span><span class="sxs-lookup"><span data-stu-id="7d3c6-324">Key performance factors</span></span>

<span data-ttu-id="7d3c6-325">이상적으로 모든 웹 사이트는 활성화 해야 합니다. 않았으며 다음 요청에 대 한 빠른 응답을 메모리에 때마다 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-325">Ideally, all websites should be active and in memory to assure quick response to the next request, whenever it comes.</span></span> <span data-ttu-id="7d3c6-326">사이트 응답성에 영향을 줄 수 있는 요인은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-326">Factors that can affect site responsiveness include:</span></span>

- <span data-ttu-id="7d3c6-327">사이트에서 응용 프로그램 풀을 재활용 후에 다시 시작 소요 되는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-327">The time it takes for a site to restart after an app pool recycles.</span></span> <span data-ttu-id="7d3c6-328">메모리에 더 이상 사이트 어셈블리 때 사이트에 대 한 웹 서버 프로세스를 시작 하는 데 걸리는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-328">This is the time it takes to launch a web server process for the site when the site assemblies are no longer in memory.</span></span> <span data-ttu-id="7d3c6-329">(플랫폼 어셈블리 되므로 메모리에 여전히 다른 사이트에서 사용 하는입니다.) 이 경우 "콜드 사이트, 웜 프레임 워크 시작" 라고 또는 방금 "콜드 사이트를 시작 합니다."</span><span class="sxs-lookup"><span data-stu-id="7d3c6-329">(The platform assemblies are still in memory, since they are used by other sites.) This situation is referred to as "cold site, warm framework startup" or just "cold site startup."</span></span>
- <span data-ttu-id="7d3c6-330">메모리의 양을 사이트를 차지합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-330">How much memory the site occupies.</span></span> <span data-ttu-id="7d3c6-331">이 용어는 "사이트 간 메모리 소비" 또는 "작업 집합을 해제 합니다."</span><span class="sxs-lookup"><span data-stu-id="7d3c6-331">Terms for this are "per-site memory consumption" or "unshared working set."</span></span>

<span data-ttu-id="7d3c6-332">새 성능 향상을 이끌어 두이 요소가 모두에 집중합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-332">The new performance improvements focus on both of these factors.</span></span>

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a><span data-ttu-id="7d3c6-333">새로운 성능 기능에 대 한 요구 사항</span><span class="sxs-lookup"><span data-stu-id="7d3c6-333">Requirements for New Performance Features</span></span>

<span data-ttu-id="7d3c6-334">새로운 기능에 대 한 요구 사항은 이러한 범주로 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-334">The requirements for the new features can be broken down into these categories:</span></span>

- <span data-ttu-id="7d3c6-335">.NET Framework 4에서 실행 되는 개선 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-335">Improvements that run on the .NET Framework 4.</span></span>
- <span data-ttu-id="7d3c6-336">.NET Framework 4.5를 필요 하지만 모든 버전의 Windows에서 실행할 수 있는 향상 된 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-336">Improvements that require the .NET Framework 4.5 but can run on any version of Windows.</span></span>
- <span data-ttu-id="7d3c6-337">Windows 8에서 실행 되는.NET Framework 4.5에만 사용할 수 있는 향상 된 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-337">Improvements that are available only with .NET Framework 4.5 running on Windows 8.</span></span>

<span data-ttu-id="7d3c6-338">성능 향상 사용 하도록 설정할 수 있는의 각 수준에 따라 카운터가 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-338">Performance increases with each level of improvement that you are able to enable.</span></span>

<span data-ttu-id="7d3c6-339">개선 된.NET Framework 4.5 기능에도 다른 시나리오에 적용 되는 광범위 한 성능 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-339">Some of the .NET Framework 4.5 improvements take advantage of broader performance features that apply to other scenarios as well.</span></span>

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a><span data-ttu-id="7d3c6-340">일반적인 어셈블리 공유</span><span class="sxs-lookup"><span data-stu-id="7d3c6-340">Sharing Common Assemblies</span></span>

<span data-ttu-id="7d3c6-341">**요구 사항**:.NET Framework 4 및 Visual Studio 11 개발자 미리 보기 SDK</span><span class="sxs-lookup"><span data-stu-id="7d3c6-341">**Requirement**: .NET Framework 4 and Visual Studio 11 Developer Preview SDK</span></span>

<span data-ttu-id="7d3c6-342">서버에서 다른 사이트는 종종 동일한 도우미 어셈블리 (예: 시작 키트 또는 샘플 응용 프로그램에서 어셈블리)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-342">Different sites on a server often use the same helper assemblies (for example, assemblies from a starter kit or sample application).</span></span> <span data-ttu-id="7d3c6-343">각 사이트의 Bin 디렉터리에서 이러한 어셈블리의 자체 복사본을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-343">Each site has its own copy of these assemblies in its Bin directory.</span></span> <span data-ttu-id="7d3c6-344">어셈블리에 대 한 개체 코드는 동일 하지만 각 어셈블리는 콜드 사이트 시작 하는 동안 개별적으로 읽을 수 있도록 물리적으로 별도 어셈블리를 하 고 메모리에 개별적으로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-344">Even though the object code for the assemblies is identical, they're physically separate assemblies, so each assembly has to be read separately during cold site startup and kept separately in memory.</span></span>

<span data-ttu-id="7d3c6-345">새로운 인턴 지정 기능 이러한 비효율성을 해결 하 고 모두 RAM 요구 사항 및 부하를 줄일 수 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-345">The new interning functionality solves this inefficiency and reduces both RAM requirements and load time.</span></span> <span data-ttu-id="7d3c6-346">인터닝 수 있습니다 Windows 파일 시스템에 각 어셈블리의 단일 복사본을 유지 하 고 단일 복사본에 대 한 기호화 된 링크와 사이트 Bin 폴더에 개별 어셈블리가 교체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-346">Interning lets Windows keep a single copy of each assembly in the file system, and individual assemblies in the site Bin folders are replaced with symbolic links to the single copy.</span></span> <span data-ttu-id="7d3c6-347">개별 사이트에서 서로 다른 버전의 어셈블리를 필요로 한다면 기호화 된 링크는은 어셈블리의 새 버전으로 대체 되 고 해당 사이트에만 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-347">If an individual site needs a distinct version of the assembly, the symbolic link is replaced by the new version of the assembly, and only that site is affected.</span></span>

<span data-ttu-id="7d3c6-348">Aspnet 이라는 새 장치가 필요한 기호화 된 링크를 사용 하 여 어셈블리를 공유\_intern.exe 만들고 인턴 지정된 어셈블리가의 저장소를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-348">Sharing assemblies using symbolic links requires a new tool named aspnet\_intern.exe, which lets you create and manage the store of interned assemblies.</span></span> <span data-ttu-id="7d3c6-349">Visual Studio 11 개발자 미리 보기 SDK의 일부분으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-349">It is provided as a part of the Visual Studio 11 Developer Preview SDK.</span></span> <span data-ttu-id="7d3c6-350">그러나 (만.NET Framework 4 설치 된 최신 기능을 설치한 것으로 가정 된 시스템에서 작동 합니다 [업데이트](https://support.microsoft.com/kb/2468871).)</span><span class="sxs-lookup"><span data-stu-id="7d3c6-350">(However, it will work on a system that has only the .NET Framework 4 installed, assuming you have installed the latest [update](https://support.microsoft.com/kb/2468871).)</span></span>

<span data-ttu-id="7d3c6-351">Aspnet 모든 적격 어셈블리 인턴 되었습니다 하기 실행\_intern.exe 주기적으로 (예: 예약된 된 태스크로 일주일에 한 번).</span><span class="sxs-lookup"><span data-stu-id="7d3c6-351">To make sure all eligible assemblies have been interned, you run aspnet\_intern.exe periodically (for example, once a week as a scheduled task).</span></span> <span data-ttu-id="7d3c6-352">일반적인 용도 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-352">A typical use is as follows:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

<span data-ttu-id="7d3c6-353">모든 옵션을 보려면 하려면 인수 없이 도구를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-353">To see all options, run the tool with no arguments.</span></span>

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a><span data-ttu-id="7d3c6-354">빠른 시작에 대 한 멀티 코어 JIT 컴파일을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="7d3c6-354">Using multi-Core JIT compilation for faster startup</span></span>

<span data-ttu-id="7d3c6-355">**요구 사항**:.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="7d3c6-355">**Requirement**: .NET Framework 4.5</span></span>

<span data-ttu-id="7d3c6-356">콜드 사이트 시작을 위한 어셈블리 필요가 디스크에서 읽은 뿐만 아니라 JIT 컴파일된 사이트 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-356">For a cold site startup, not only do assemblies have to be read from disk, but the site must be JIT-compiled.</span></span> <span data-ttu-id="7d3c6-357">복잡 한 사이트가 지연을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-357">For a complex site, this can add significant delays.</span></span> <span data-ttu-id="7d3c6-358">.NET Framework 4.5의 새로운 범용 기술으로 사용할 수 있는 프로세서 코어 JIT 컴파일 분배 하 여 이러한 지연을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-358">A new general-purpose technique in the .NET Framework 4.5 reduces these delays by spreading JIT-compilation across available processor cores.</span></span> <span data-ttu-id="7d3c6-359">만큼이 작업을 수행 하 고 최대한 일찍 도중 수집 된 정보를 사용 하 여 이전 시작 사이트의.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-359">It does this as much and as early as possible by using information gathered during previous launches of the site.</span></span> <span data-ttu-id="7d3c6-360">이 기능에 의해 구현 된 [System.Runtime.ProfileOptimization.StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) 메서드.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-360">This functionality implemented by the [System.Runtime.ProfileOptimization.StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) method.</span></span>

<span data-ttu-id="7d3c6-361">JIT 컴파일 여러 코어를 사용 하 여 되므로이 기능을 활용 하기 위해 아무 작업도 수행 하지 않고도 asp.net에서는 기본적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-361">JIT-compiling using multiple cores is enabled by default in ASP.NET, so you do not need to do anything to take advantage of this feature.</span></span> <span data-ttu-id="7d3c6-362">이 기능을 사용 하지 않도록 설정 하려면 Web.config 파일에서 다음 설정을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-362">If you want to disable this feature, make the following setting in the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a><span data-ttu-id="7d3c6-363">가비지 수집을 최적화 하기 위해 메모리를 튜닝 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-363">Tuning garbage collection to optimize for memory</span></span>

<span data-ttu-id="7d3c6-364">**요구 사항**:.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="7d3c6-364">**Requirement**: .NET Framework 4.5</span></span>

<span data-ttu-id="7d3c6-365">사이트를 실행 하 고, 가비지 수집기 (GC) 힙에서 사용 하는 메모리 소비에 중요 한 요소가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-365">Once a site is running, its use of the garbage-collector (GC) heap can be a significant factor in its memory consumption.</span></span> <span data-ttu-id="7d3c6-366">모든 가비지 수집기와 같은.NET Framework GC CPU 시간 (빈도 significance는 컬렉션의) 및 메모리 사용 (새, 확보, 또는 자유 수 없는 개체에 사용 되는 추가 공간이) 간 균형을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-366">Like any garbage collector, the .NET Framework GC makes tradeoffs between CPU time (frequency and significance of collections) and memory consumption (extra space that is used for new, freed, or free-able objects).</span></span> <span data-ttu-id="7d3c6-367">이전 릴리스에 대 한 적절 한 균형을 달성 하기 위해 GC를 구성 하는 방법에 지침 제공 된 (예를 들어 참조 [ASP.NET 2.0/3.5 공유 호스팅 구성](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)).</span><span class="sxs-lookup"><span data-stu-id="7d3c6-367">For previous releases, we have provided guidance on how to configure the GC to achieve the right balance (for example, see [ASP.NET 2.0/3.5 Shared Hosting Configuration](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)).</span></span>

<span data-ttu-id="7d3c6-368">.NET Framework 4.5 작업 정의 된 구성 설정은 여러 독립 실행형 설정 대신 사용할 수 없으면 수 있게 해 주는 모든에서는 이전에 권장 되는 GC 설정으로 새 튜닝의 각 사이트에 대 한 추가 성능을 제공 하는 작업 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-368">For the .NET Framework 4.5, instead of multiple standalone settings, a workload-defined configuration setting is available that enables all of the previously recommended GC settings as well as new tuning that delivers additional performance for the per-site working set.</span></span>

<span data-ttu-id="7d3c6-369">튜닝 GC 메모리를 사용 하려면 다음 설정을 Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config 파일에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-369">To enable GC memory tuning, add the following setting to the Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

<span data-ttu-id="7d3c6-370">(변경 내용에 대 한 이전 지침 aspnet.config 알고 인 경우이 설정은 이전 설정을 대체 참고-예를 들어 gcServer, gcConcurrent 등을 설정 하지 않아도 됩니다. 않아도 이전 설정을 제거 합니다.)</span><span class="sxs-lookup"><span data-stu-id="7d3c6-370">(If you're familiar with the previous guidance for changes to aspnet.config, note that this setting replaces the old settings — for example, there is no need to set gcServer, gcConcurrent, etc. You do not have to remove the old settings.)</span></span>

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a><span data-ttu-id="7d3c6-371">웹 응용 프로그램 프리페치</span><span class="sxs-lookup"><span data-stu-id="7d3c6-371">Prefetching for web applications</span></span>

<span data-ttu-id="7d3c6-372">**요구 사항**: Windows 8에서 실행 되는.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="7d3c6-372">**Requirement**: .NET Framework 4.5 running on Windows 8</span></span>

<span data-ttu-id="7d3c6-373">Windows가 기술을 통해을 포함 하는 데 몇 번의 릴리스에서 대 한는 [prefetcher](http://en.wikipedia.org/wiki/Prefetcher) 하는 응용 프로그램 시작의 디스크 읽기 비용을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-373">For several releases, Windows has included a technology known as the [prefetcher](http://en.wikipedia.org/wiki/Prefetcher) that reduces the disk-read cost of application startup.</span></span> <span data-ttu-id="7d3c6-374">콜드 시작 클라이언트 응용 프로그램에 주로 문제가 이기 때문에이 기술은 하지 하는 서버에 필요한 구성 요소만 포함 하는 Windows Server에 포함 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-374">Because cold startup is a problem predominantly for client applications, this technology has not been included in Windows Server, which includes only components that are essential to a server.</span></span> <span data-ttu-id="7d3c6-375">프리페치는 최신 버전의 Windows Server에서 개별 웹 사이트의 시작을 최적화할 수 있다는 것에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-375">Prefetching is now available in the latest version of Windows Server, where it can optimize the launch of individual websites.</span></span>

<span data-ttu-id="7d3c6-376">Windows Server는 prefetcher 기본적으로 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-376">For Windows Server, the prefetcher is not enabled by default.</span></span> <span data-ttu-id="7d3c6-377">을 사용 하려면 구성 고밀도 웹 호스팅을 위한 prefetcher 명령줄에서 명령 집합을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-377">To enable and configure the prefetcher for high-density web hosting, run the following set of commands at the command line:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

<span data-ttu-id="7d3c6-378">그런 다음는 prefetcher ASP.NET 응용 프로그램을 통합 하려면 다음 Web.config 파일에 추가:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-378">Then, to integrate the prefetcher with ASP.NET applications, add the following to the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="7d3c6-379">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="7d3c6-379">ASP.NET Web Forms</span></span>

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a><span data-ttu-id="7d3c6-380">강력한 형식의 데이터 컨트롤</span><span class="sxs-lookup"><span data-stu-id="7d3c6-380">Strongly Typed Data Controls</span></span>

<span data-ttu-id="7d3c6-381">ASP.NET 4.5 Web Forms 데이터로 작업 하기 위한 몇 가지 향상 된 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-381">In ASP.NET 4.5, Web Forms includes some improvements for working with data.</span></span> <span data-ttu-id="7d3c6-382">첫 번째 개선은 강력한 형식의 데이터를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-382">The first improvement is strongly typed data controls.</span></span> <span data-ttu-id="7d3c6-383">이전 버전의 ASP.NET Web Forms 컨트롤에 표시할 있습니다 사용 하 여 데이터 바인딩된 값 *Eval* 및 데이터 바인딩 식:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-383">For Web Forms controls in previous versions of ASP.NET, you display a data-bound value using *Eval* and a data-binding expression:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

<span data-ttu-id="7d3c6-384">양방향 데이터 바인딩을 사용 하 여 있습니다 *바인딩할*:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-384">For two-way data binding, you use *Bind*:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

<span data-ttu-id="7d3c6-385">런타임 시 이러한 호출은 리플렉션을 사용 하 여 지정된 된 멤버의 값을 읽고 태그에 결과 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-385">At run time, these calls use reflection to read the value of the specified member and then display the result in the markup.</span></span> <span data-ttu-id="7d3c6-386">이 접근 방식을 쉽게 임의의 unshaped 데이터에 대 한 데이터 바인딩이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-386">This approach makes it easy to data bind against arbitrary, unshaped data.</span></span>

<span data-ttu-id="7d3c6-387">그러나 다음과 같은 데이터 바인딩 식 멤버 이름, (예: 정의로 이동), 탐색 또는 컴파일 타임 이러한 이름에 대 한 검사에 대 한 IntelliSense와 같은 기능을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-387">However, data-binding expressions like this don't support features like IntelliSense for member names, navigation (like Go To Definition), or compile-time checking for these names.</span></span>

<span data-ttu-id="7d3c6-388">이 문제를 해결 하기 위해 ASP.NET 4.5 컨트롤에 바인딩되는 데이터의 데이터 형식을 선언 하는 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-388">To address this issue, ASP.NET 4.5 adds the ability to declare the data type of the data that a control is bound to.</span></span> <span data-ttu-id="7d3c6-389">이렇게 하면 새를 사용 하 여 *ItemType* 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-389">You do this using the new *ItemType* property.</span></span> <span data-ttu-id="7d3c6-390">데이터 바인딩 식의 범위에 두 개의 새 형식화 된 변수는 사용할 수 있는이 속성을 설정 하는 경우: *항목* 및 *BindItem*합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-390">When you set this property, two new typed variables are available in the scope of data-binding expressions: *Item* and *BindItem*.</span></span> <span data-ttu-id="7d3c6-391">변수는 강력한 형식 때문에 Visual Studio 개발 환경의 모든 혜택을 얻을 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-391">Because the variables are strongly typed, you get the full benefits of the Visual Studio development experience.</span></span>


<span data-ttu-id="7d3c6-392">사용 하 여 양방향 데이터 바인딩 식에 대 한는 *BindItem* 변수:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-392">For two-way data-binding expressions, use the *BindItem* variable:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]


<span data-ttu-id="7d3c6-393">데이터 바인딩을 지 원하는 대부분 ASP.NET Web Forms 프레임 워크 컨트롤을 지원 하도록 업데이트 되었습니다는 *ItemType* 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-393">Most controls in the ASP.NET Web Forms framework that support data binding have been updated to support the *ItemType* property.</span></span>

<a id="_Toc318097387"></a>
### <a name="model-binding"></a><span data-ttu-id="7d3c6-394">모델 바인딩</span><span class="sxs-lookup"><span data-stu-id="7d3c6-394">Model Binding</span></span>

<span data-ttu-id="7d3c6-395">모델 바인딩 코드 중심의 데이터 액세스를 사용 하려면 ASP.NET Web Forms 컨트롤의 데이터 바인딩을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-395">Model binding extends data binding in ASP.NET Web Forms controls to work with code-focused data access.</span></span> <span data-ttu-id="7d3c6-396">개념을 통합 하는 *ObjectDataSource* 컨트롤 및 ASP.NET mvc에서 모델 바인딩의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-396">It incorporates concepts from the *ObjectDataSource* control and from model binding in ASP.NET MVC.</span></span>

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a><span data-ttu-id="7d3c6-397">데이터 선택</span><span class="sxs-lookup"><span data-stu-id="7d3c6-397">Selecting data</span></span>

<span data-ttu-id="7d3c6-398">컨트롤의 데이터를 선택 하려면 모델 바인딩을 사용 하도록 데이터 제어를 구성 하려면 설정 *SelectMethod* 속성 페이지의 코드에 있는 메서드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-398">To configure a data control to use model binding to select data, you set the control's *SelectMethod* property to the name of a method in the page's code.</span></span> <span data-ttu-id="7d3c6-399">데이터 컨트롤 페이지 수명 주기의 적절 한 시간에 메서드를 호출 하 고 자동으로 반환된 된 데이터를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-399">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="7d3c6-400">명시적으로 호출할 필요가 없습니다는 *DataBind* 메서드.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-400">There's no need to explicitly call the *DataBind* method.</span></span>

<span data-ttu-id="7d3c6-401">다음 예제에서는 *GridView* 제어 라는 메서드를 사용 하도록 구성 된 *GetCategories*:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-401">In the following example, the *GridView* control is configured to use a method named *GetCategories*:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

<span data-ttu-id="7d3c6-402">만들는 *GetCategories* 페이지의 코드에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-402">You create the *GetCategories* method in the page's code.</span></span> <span data-ttu-id="7d3c6-403">단순한 select 작업에 대 한 메서드 매개 변수 없이 필요 하 고 반환 해야는 *IEnumerable* 또는 *IQueryable* 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-403">For a simple select operation, the method needs no parameters and should return an *IEnumerable* or *IQueryable* object.</span></span> <span data-ttu-id="7d3c6-404">하는 경우 새 *ItemType* 속성이 설정 되어 (있도록 하는 강력한 데이터 바인딩 식을 형식에 설명 된 대로 [데이터 컨트롤 강력한 형식의](#_Toc318097386) 이전 버전), 이러한 인터페이스의 제네릭 버전 반환 되어야- *IEnumerable&lt;T&gt;*  또는 *IQueryable&lt;T&gt;* 와 *T* 매개 변수 형식과 일치 하는 *ItemType* 속성 (예를 들어 *IQueryable&lt;범주&gt;*).</span><span class="sxs-lookup"><span data-stu-id="7d3c6-404">If the new *ItemType* property is set (which enables strongly typed data-binding expressions, as explained under [Strongly Typed Data Controls](#_Toc318097386) earlier), the generic versions of these interfaces should be returned — *IEnumerable&lt;T&gt;* or *IQueryable&lt;T&gt;*, with the *T* parameter matching the type of the *ItemType* property (for example, *IQueryable&lt;Category&gt;*).</span></span>

<span data-ttu-id="7d3c6-405">다음 예제에 대 한 코드는 *GetCategories* 메서드.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-405">The following example shows the code for a *GetCategories* method.</span></span> <span data-ttu-id="7d3c6-406">이 예제에서는 Northwind 샘플 데이터베이스에서 Entity Framework Code First 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-406">This example uses the Entity Framework Code First model with the Northwind sample database.</span></span> <span data-ttu-id="7d3c6-407">코드에서는 쿼리를 통해 범주별 관련된 제품의 세부 정보를 반환 하는지 확인는 *Include* 메서드.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-407">The code makes sure that the query returns details of the related products for each category by way of the *Include* method.</span></span> <span data-ttu-id="7d3c6-408">(이렇게 하면는 *TemplateField* 태그 요소에에서 필요 없이 각 범주에서 제품의 수를 표시 한 [n + 1 선택](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem).)</span><span class="sxs-lookup"><span data-stu-id="7d3c6-408">(This ensures that the *TemplateField* element in the markup displays the count of products in each category without requiring an [n+1 select](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem).)</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

<span data-ttu-id="7d3c6-409">페이지 실행 하는 경우, *GridView* 컨트롤을 호출은 *GetCategories* 메서드 자동으로 구성 된 필드를 사용 하 여 반환 된 데이터를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-409">When the page runs, the *GridView* control calls the *GetCategories* method automatically and renders the returned data using the configured fields:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

<span data-ttu-id="7d3c6-410">Select 메서드 반환 하기 때문에 *IQueryable* 개체는 *GridView* 컨트롤 실행 되기 전에 쿼리를 추가로 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-410">Because the select method returns an *IQueryable* object, the *GridView* control can further manipulate the query before executing it.</span></span> <span data-ttu-id="7d3c6-411">예를 들어는 *GridView* 컨트롤 정렬 및 반환 된 페이징에 대 한 쿼리 식을 추가할 수 있습니다 *IQueryable* 실행 하기 전에 개체를 해당 작업은 내부에서 수행 LINQ 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-411">For example, the *GridView* control can add query expressions for sorting and paging to the returned *IQueryable* object before it is executed, so that those operations are performed by the underlying LINQ provider.</span></span> <span data-ttu-id="7d3c6-412">이 경우 Entity Framework를 사용 하는 데이터베이스에 해당 작업이 수행 됩니다 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-412">In this case, Entity Framework will ensure those operations are performed in the database.</span></span>

<span data-ttu-id="7d3c6-413">다음 예제와 *GridView* 컨트롤 정렬 및 페이징을 사용 하도록 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-413">The following example shows the *GridView* control modified to allow sorting and paging:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

<span data-ttu-id="7d3c6-414">이제 페이지를 실행할 때 컨트롤 데이터의 현재 페이지에만 표시 되 고 선택한 열에 의해 정렬 된 있는지 확인 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-414">Now when the page runs, the control can make sure that only the current page of data is displayed and that it's ordered by the selected column:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

<span data-ttu-id="7d3c6-415">반환 된 데이터를 필터링 하려면 매개 변수를 select 메서드에 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-415">To filter the returned data, parameters have to be added to the select method.</span></span> <span data-ttu-id="7d3c6-416">이러한 매개 변수를 실행 하는 모델 바인딩에서 채워지며 쿼리 데이터를 반환 하기 전에 변경에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-416">These parameters will be populated by the model binding at run time, and you can use them to alter the query before returning the data.</span></span>

<span data-ttu-id="7d3c6-417">예를 들어 쿼리 문자열에 키워드를 입력 하 여 사용자가 제품 필터를 사용 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-417">For example, assume that you want to let users filter products by entering a keyword in the query string.</span></span> <span data-ttu-id="7d3c6-418">메서드 매개 변수를 추가 하 고 매개 변수 값을 사용 하도록 코드를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-418">You can add a parameter to the method and update the code to use the parameter value:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

<span data-ttu-id="7d3c6-419">이 코드를 포함 한 *여기서* 식에 값이 제공 하는 경우 *키워드* 쿼리 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-419">This code includes a *Where* expression if a value is provided for *keyword* and then returns the query results.</span></span>

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a><span data-ttu-id="7d3c6-420">값 공급자</span><span class="sxs-lookup"><span data-stu-id="7d3c6-420">Value providers</span></span>

<span data-ttu-id="7d3c6-421">앞의 예제에서 위치에 대 한 특정 없습니다에 대 한 값은 *키워드* 매개 변수에서 생성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-421">The previous example was not specific about where the value for the *keyword* parameter was coming from.</span></span> <span data-ttu-id="7d3c6-422">이 정보를 나타내려면 매개 변수 특성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-422">To indicate this information, you can use a parameter attribute.</span></span> <span data-ttu-id="7d3c6-423">이 예에서는 사용할 수 있습니다는 *QueryStringAttribute* 에 있는 클래스는 *System.Web.ModelBinding* 네임 스페이스:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-423">For this example, you can use the *QueryStringAttribute* class that's in the *System.Web.ModelBinding* namespace:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

<span data-ttu-id="7d3c6-424">이렇게 하면 모델을 쿼리 문자열에서 값을 연결할 하려고을 바인딩하는 *키워드* 실행 시 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-424">This instructs model binding to try to bind a value from the query string to the *keyword* parameter at run time.</span></span> <span data-ttu-id="7d3c6-425">(여기 형식 변환을 수행 하지만 경우 하지 않습니다.) 값을 제공할 수 없습니다 형식이 nullable이 아닌 경우 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-425">(This might involve performing type conversion, although it doesn't in this case.) If a value cannot be provided and the type is non-nullable, an exception is thrown.</span></span>

<span data-ttu-id="7d3c6-426">이러한 방법에 대 한 값의 소스는 값 공급자 라고 하 고를 사용 하는 값 공급자를 나타내는 매개 변수 특성 값 공급자 특성으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-426">The sources of values for these methods are referred to as value providers, and the parameter attributes that indicate which value provider to use are referred to as value provider attributes.</span></span> <span data-ttu-id="7d3c6-427">Web Forms에는 Web Forms 응용 프로그램의 쿼리 문자열, 쿠키, 폼 값, 컨트롤, 상태 보기, 세션 상태 프로필 속성 등의 모든 사용자 입력의 일반적인 원본에 대 한 값 공급자 및 해당 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-427">Web Forms will include value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application, such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="7d3c6-428">사용자 지정 값 공급자를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-428">You can also write custom value providers.</span></span>

<span data-ttu-id="7d3c6-429">기본적으로 매개 변수 이름 값 공급자 컬렉션에 값을 찾을 키로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-429">By default, the parameter name is used as the key to find a value in the value provider collection.</span></span> <span data-ttu-id="7d3c6-430">예제에서는 코드 키워드를 명명 된 쿼리 문자열 값에 대 한 표시 됩니다 (예를 들어 ~ / default.aspx?keyword=chef).</span><span class="sxs-lookup"><span data-stu-id="7d3c6-430">In the example, the code will look for a query-string value named keyword (for example, ~/default.aspx?keyword=chef).</span></span> <span data-ttu-id="7d3c6-431">매개 변수 특성에 대 한 인수로 전달 하 여 사용자 지정 키를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-431">You can specify a custom key by passing it as an argument to the parameter attribute.</span></span> <span data-ttu-id="7d3c6-432">예를 들어 q 명명 된 쿼리 문자열 변수의 값을 사용 하려면이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-432">For example, to use the value of the query-string variable named q, you could do this:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

<span data-ttu-id="7d3c6-433">이러한 방법은 페이지의 코드에 사용자가 쿼리 문자열을 사용 하는 키워드를 전달 하 여 결과 필터링 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-433">If this method is in the page's code, users can filter the results by passing a keyword using the query string:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

<span data-ttu-id="7d3c6-434">직접 코드를 작성 하려면 해야 하는 많은 작업을 수행 하는 모델 바인딩: 값을 읽기, null 값을 확인 하는, 적절 한 형식으로 변환 하는 동안은 변환이 성공 했는지 여부를 확인 및의 값을 사용 하 여 마지막으로 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-434">Model binding accomplishes many tasks that you would otherwise have to code by hand: reading the value, checking for a null value, attempting to convert it to the appropriate type, checking whether the conversion was successful, and finally, using the value in the query.</span></span> <span data-ttu-id="7d3c6-435">훨씬 더 적을 코드와 응용 프로그램 전체에서 기능을 다시 사용할 수 있는 결과 바인딩을 모델링 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-435">Model binding results in far less code and in the ability to reuse the functionality throughout your application.</span></span>

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a><span data-ttu-id="7d3c6-436">컨트롤의 값으로 필터링</span><span class="sxs-lookup"><span data-stu-id="7d3c6-436">Filtering by values from a control</span></span>

<span data-ttu-id="7d3c6-437">드롭다운 목록에서 필터 값을 선택할 수 있도록 예제 확장 하려면 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-437">Suppose you want to extend the example to let the user choose a filter value from a drop-down list.</span></span> <span data-ttu-id="7d3c6-438">다음 드롭 다운 목록 태그를 추가 하 고 해당 데이터를 사용 하 여 다른 메서드를 가져오기 위해 구성 된 *SelectMethod* 속성:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-438">Add the following drop-down list to the markup and configure it to get its data from another method using the *SelectMethod* property:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

<span data-ttu-id="7d3c6-439">일반적으로 추가할 수도 있습니다는 *emptydatatemplate이* 요소를는 *GridView* 컨트롤에서는 일치 하는 제품이 발견 되 면 메시지를 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-439">Typically you would also add an *EmptyDataTemplate* element to the *GridView* control so that the control will display a message if no matching products are found:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

<span data-ttu-id="7d3c6-440">페이지 코드에서 새 선택 드롭다운 목록에 대 한 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-440">In the page code, add the new select method for the drop-down list:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

<span data-ttu-id="7d3c6-441">마지막으로 업데이트는 *GetProducts* 드롭 다운 목록에서 선택된 된 범주 ID가 포함 된 새 매개 변수를 사용 하는 방법 선택:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-441">Finally, update the *GetProducts* select method to take a new parameter that contains the ID of the selected category from the drop-down list:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

<span data-ttu-id="7d3c6-442">이제 페이지를 실행 하는 경우 사용자가 드롭다운 목록에서 범주를 선택할 수 및 *GridView* 컨트롤은 필터링 된 데이터를 표시 하도록 자동으로 다시 바인딩.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-442">Now when the page runs, users can select a category from the drop-down list, and the *GridView* control is automatically re-bound to show the filtered data.</span></span> <span data-ttu-id="7d3c6-443">모델 바인딩 선택 방법에 대 한 매개 변수 값을 추적 하 고 모든 매개 변수 값을 다시 게시 한 후 변경 되었는지 여부를 검색 하기 때문에 이것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-443">This is possible because model binding tracks the values of parameters for select methods and detects whether any parameter value has changed after a postback.</span></span> <span data-ttu-id="7d3c6-444">이 경우 모델 바인딩 관련된 된 데이터 컨트롤에 데이터를 다시 바인딩할 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-444">If so, model binding forces the associated data control to re-bind to the data.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a><span data-ttu-id="7d3c6-445">HTML로 인코딩된 데이터 바인딩 식</span><span class="sxs-lookup"><span data-stu-id="7d3c6-445">HTML Encoded Data-Binding Expressions</span></span>

<span data-ttu-id="7d3c6-446">있습니다 수 이제 HTML 인코딩할 데이터 바인딩 식의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-446">You can now HTML-encode the result of data-binding expressions.</span></span> <span data-ttu-id="7d3c6-447">콜론 (:)의 끝에 추가 &lt;데이터 바인딩 식을 표시 하는 % # 접두사:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-447">Add a colon (:) to the end of the &lt;%# prefix that marks the data-binding expression:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a><span data-ttu-id="7d3c6-448">비 가시적인 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="7d3c6-448">Unobtrusive Validation</span></span>

<span data-ttu-id="7d3c6-449">이제 클라이언트 쪽 유효성 검사 논리에 대 한 비 가시적인 JavaScript를 사용 하도록 기본 제공 유효성 검사 컨트롤을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-449">You can now configure the built-in validator controls to use unobtrusive JavaScript for client-side validation logic.</span></span> <span data-ttu-id="7d3c6-450">이 크게 JavaScript 페이지 태그에 인라인으로 렌더링할지 줄일 수 및 전체 페이지 크기를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-450">This significantly reduces the amount of JavaScript rendered inline in the page markup and reduces the overall page size.</span></span> <span data-ttu-id="7d3c6-451">비간섭 JavaScript 유효성 검사 컨트롤에 대 한 이러한 방법 중 하나로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-451">You can configure unobtrusive JavaScript for validator controls in any of these ways:</span></span>

- <span data-ttu-id="7d3c6-452">다음 설정을 추가 하 여 전역적으로  *&lt;appSettings&gt;*  Web.config 파일의 요소:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-452">Globally by adding the following setting to the *&lt;appSettings&gt;* element in the Web.config file:</span></span> 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- <span data-ttu-id="7d3c6-453">정적 설정 하 여 전역적으로 *System.Web.UI.ValidationSettings.UnobtrusiveValidationMode* 속성을 *UnobtrusiveValidationMode.WebForms* (일반적으로 *응용 프로그램 \_시작* Global.asax 파일에는 메서드).</span><span class="sxs-lookup"><span data-stu-id="7d3c6-453">Globally by setting the static *System.Web.UI.ValidationSettings.UnobtrusiveValidationMode* property to *UnobtrusiveValidationMode.WebForms* (typically in the *Application\_Start* method in the Global.asax file).</span></span>
- <span data-ttu-id="7d3c6-454">새 설정 하 여 페이지에 대해 개별적으로 *UnobtrusiveValidationMode* 의 속성은 *페이지* 클래스를 *UnobtrusiveValidationMode.WebForms*합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-454">Individually for a page by setting the new *UnobtrusiveValidationMode* property of the *Page* class to *UnobtrusiveValidationMode.WebForms*.</span></span>

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a><span data-ttu-id="7d3c6-455">HTML5 업데이트</span><span class="sxs-lookup"><span data-stu-id="7d3c6-455">HTML5 Updates</span></span>

<span data-ttu-id="7d3c6-456">몇 가지 향상 된 기능에 적용 된 Web Forms 서버 컨트롤 HTML5의 새로운 기능을 활용 하려면:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-456">Some improvements have been made to Web Forms server controls to take advantage of new features of HTML5:</span></span>

- <span data-ttu-id="7d3c6-457">*TextMode* 의 속성은 *TextBox* 제어와 같은 새로운 HTML5 입력된 형식을 지원 하도록 업데이트 되었습니다 *전자 메일*, *datetime*, 및 에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-457">The *TextMode* property of the *TextBox* control has been updated to support the new HTML5 input types like *email*, *datetime*, and so on.</span></span>
- <span data-ttu-id="7d3c6-458">*파일 업로드* 지원이 HTML5 기능을 지 원하는 브라우저에서 여러 파일 업로드를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-458">The *FileUpload* control now supports multiple file uploads from browsers that support this HTML5 feature.</span></span>
- <span data-ttu-id="7d3c6-459">유효성 검사기는 이제 지원의 유효성을 검사할 HTML5 입력된 요소를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-459">Validator controls now support validating HTML5 input elements.</span></span>
- <span data-ttu-id="7d3c6-460">이제 URL을 나타내는 특성이 있는 새 HTML5 요소 지원 runat = "server"입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-460">New HTML5 elements that have attributes that represent a URL now support runat="server".</span></span> <span data-ttu-id="7d3c6-461">결과적으로, 사용할 수 있습니다 ASP.NET 규칙 URL 경로에 ~를 나타내는 응용 프로그램 루트 연산자 (예를 들어 &lt;비디오 runat = "server" src="~/myVideo.wmv" /&gt;).</span><span class="sxs-lookup"><span data-stu-id="7d3c6-461">As a result, you can use ASP.NET conventions in URL paths, like the ~ operator to represent the application root (for example, &lt;video runat="server" src="~/myVideo.wmv" /&gt;).</span></span>
- <span data-ttu-id="7d3c6-462">*UpdatePanel* 컨트롤 게시 HTML5 입력된 필드를 지원 하도록 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-462">The *UpdatePanel* control has been fixed to support posting HTML5 input fields.</span></span>

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a><span data-ttu-id="7d3c6-463">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="7d3c6-463">ASP.NET MVC 4</span></span>

<span data-ttu-id="7d3c6-464">ASP.NET MVC 4 베타는 이제 Visual Studio 11 베타에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-464">ASP.NET MVC 4 Beta is now included with Visual Studio 11 Beta.</span></span> <span data-ttu-id="7d3c6-465">ASP.NET MVC는 매우 테스트 가능 하 고 유지 관리 가능한 웹 응용 프로그램 모델-뷰-컨트롤러 (MVC) 패턴을 활용 하 여 개발 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-465">ASP.NET MVC is a framework for developing highly testable and maintainable Web applications by leveraging the Model-View-Controller (MVC) pattern.</span></span> <span data-ttu-id="7d3c6-466">ASP.NET MVC 4 쉽게 모바일 웹 응용 프로그램을 개발 하 고 모든 장치에 연결할 수 있는 HTTP 서비스를 작성 하는 데 도움이 되는 ASP.NET Web API를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-466">ASP.NET MVC 4 makes it easy to build applications for the mobile Web and includes ASP.NET Web API, which helps you build HTTP services that can reach any device.</span></span> <span data-ttu-id="7d3c6-467">자세한 내용은 참조는 [ASP.NET MVC 4 릴리스 정보](mvc4-release-notes.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-467">For more information, see the [ASP.NET MVC 4 Release Notes](mvc4-release-notes.md).</span></span>

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a><span data-ttu-id="7d3c6-468">ASP.NET 웹 페이지 2</span><span class="sxs-lookup"><span data-stu-id="7d3c6-468">ASP.NET Web Pages 2</span></span>

<span data-ttu-id="7d3c6-469">새로운 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-469">New features include the following:</span></span>

- <span data-ttu-id="7d3c6-470">새로운 또는 업데이트 된 사이트 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-470">New and updated site templates.</span></span>
- <span data-ttu-id="7d3c6-471">서버 쪽 및 클라이언트 쪽 유효성 검사를 사용 하 여 추가 된 *유효성 검사* 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-471">Adding server-side and client-side validation using the *Validation* helper.</span></span>
- <span data-ttu-id="7d3c6-472">자산 관리자를 사용 하 여 스크립트를 등록 하는 기능.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-472">The ability to register scripts using an assets manager.</span></span>
- <span data-ttu-id="7d3c6-473">Facebook 및 OAuth 및 OpenID를 사용 하 여 다른 사이트에서의 로그인을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-473">Enabling logins from Facebook and other sites using OAuth and OpenID.</span></span>
- <span data-ttu-id="7d3c6-474">사용 하 여 추가 매핑됩니다는 *매핑합니다* 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-474">Adding maps using the *Maps* helper.</span></span>
- <span data-ttu-id="7d3c6-475">웹 페이지 응용 프로그램에서-병렬 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-475">Running Web Pages applications side-by-side.</span></span>
- <span data-ttu-id="7d3c6-476">모바일 장치에 대 한 페이지를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-476">Rendering pages for mobile devices.</span></span>

<span data-ttu-id="7d3c6-477">이러한 기능 및 전체 페이지 코드 예제에 대 한 자세한 내용은 참조 [웹 페이지 2 베타의 The Top 기능](https://go.microsoft.com/fwlink/?LinkID=227824)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-477">For more information about these features and full-page code examples, see [The Top Features in Web Pages 2 Beta](https://go.microsoft.com/fwlink/?LinkID=227824).</span></span>

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a><span data-ttu-id="7d3c6-478">Visual Web Developer 11 베타</span><span class="sxs-lookup"><span data-stu-id="7d3c6-478">Visual Web Developer 11 Beta</span></span>

<span data-ttu-id="7d3c6-479">이 섹션에서는 Visual Web Developer 11 베타 및 Visual Studio 2012 릴리스 후보에서 웹 개발에 대 한 향상 된 기능에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-479">This section provides information about improvements for web development in Visual Web Developer 11 Beta and Visual Studio 2012 Release Candidate.</span></span>

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a><span data-ttu-id="7d3c6-480">Visual Studio 2010 및 Visual Studio 2012 릴리스 후보 (프로젝트 호환성) 간 공유 되는 프로젝트</span><span class="sxs-lookup"><span data-stu-id="7d3c6-480">Project Sharing Between Visual Studio 2010 and Visual Studio 2012 Release Candidate (Project Compatibility)</span></span>

<span data-ttu-id="7d3c6-481">Visual Studio 2012 릴리스 후보 될 때까지 새 버전의 Visual Studio에서 기존 프로젝트를 열기 변환 마법사를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-481">Until Visual Studio 2012 Release Candidate, opening an existing project in a newer version of Visual Studio launched the Conversion Wizard.</span></span> <span data-ttu-id="7d3c6-482">솔루션 및 프로젝트의 콘텐츠 (자산)를 업그레이드 하는 이전 버전과 호환 되지 않은 새로운 형식에 강제로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-482">This forced an upgrade of the content (assets) of a project and solution to new formats that were not backward compatible.</span></span> <span data-ttu-id="7d3c6-483">따라서 변환 후 있습니다 열 수 없습니다 프로젝트는 이전 버전의 Visual Studio에서.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-483">Therefore, after the conversion you could not open the project in the older version of Visual Studio.</span></span>

<span data-ttu-id="7d3c6-484">많은 고객 되었다는 적합 한 접근 방식의 없음을 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-484">Many customers have told us that this was not the right approach.</span></span> <span data-ttu-id="7d3c6-485">Visual Studio 11 베타에서 이제 Visual Studio 2010 s p 1을 사용 하 여 솔루션 및 프로젝트를 공유를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-485">In Visual Studio 11 Beta, we now support sharing projects and solutions with Visual Studio 2010 SP1.</span></span> <span data-ttu-id="7d3c6-486">이 Visual Studio 2012 릴리스 후보에서 2010 프로젝트를 열면은 여전히 Visual Studio 2010 s p 1에서 프로젝트를 열 수를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-486">This means that if you open a 2010 project in Visual Studio 2012 Release Candidate, you will still be able to open the project in Visual Studio 2010 SP1.</span></span>

> [!NOTE]
> <span data-ttu-id="7d3c6-487">몇 가지 형식의 프로젝트는 Visual Studio 2010 SP1 및 Visual Studio 2012 릴리스 후보 간에 공유할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-487">A few types of projects cannot be shared between Visual Studio 2010 SP1 and Visual Studio 2012 Release Candidate.</span></span> <span data-ttu-id="7d3c6-488">여기 일부 (예: ASP.NET MVC 2 프로젝트) 이전 프로젝트 또는 프로젝트 (예: 설치 프로젝트의 경우) 특수 목적을 위해 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-488">These include some older projects (such as ASP.NET MVC 2 projects) or projects for special purposes (such as Setup projects).</span></span>

<span data-ttu-id="7d3c6-489">Visual Studio 11 베타에서 처음으로 Visual Studio 2010 SP1 웹 프로젝트를 열 때 다음과 같은 속성이 프로젝트 파일에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-489">When you open a Visual Studio 2010 SP1 Web project for the first time in Visual Studio 11 Beta, the following properties are added to the project file:</span></span>

- <span data-ttu-id="7d3c6-490">FileUpgradeFlags</span><span class="sxs-lookup"><span data-stu-id="7d3c6-490">FileUpgradeFlags</span></span>
- <span data-ttu-id="7d3c6-491">UpgradeBackupLocation</span><span class="sxs-lookup"><span data-stu-id="7d3c6-491">UpgradeBackupLocation</span></span>
- <span data-ttu-id="7d3c6-492">OldToolsVersion</span><span class="sxs-lookup"><span data-stu-id="7d3c6-492">OldToolsVersion</span></span>
- <span data-ttu-id="7d3c6-493">VisualStudioVersion</span><span class="sxs-lookup"><span data-stu-id="7d3c6-493">VisualStudioVersion</span></span>
- <span data-ttu-id="7d3c6-494">VSToolsPath</span><span class="sxs-lookup"><span data-stu-id="7d3c6-494">VSToolsPath</span></span>

<span data-ttu-id="7d3c6-495">FileUpgradeFlags, UpgradeBackupLocation, 및 OldToolsVersion 프로젝트 파일 업그레이드 프로세스에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-495">FileUpgradeFlags, UpgradeBackupLocation, and OldToolsVersion are used by the process that upgrades the project file.</span></span> <span data-ttu-id="7d3c6-496">Visual Studio 2010에서 프로젝트 작업에 영향을 주지 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-496">They have no impact on working with the project in Visual Studio 2010.</span></span>

<span data-ttu-id="7d3c6-497">VisualStudioVersion에 현재 프로젝트에 대 한 Visual Studio의 버전을 나타내는 MSBuild 4.5에서 사용 하는 새 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-497">VisualStudioVersion is a new property used by MSBuild 4.5 that indicates the version of Visual Studio for the current project.</span></span> <span data-ttu-id="7d3c6-498">MSBuild 4.0 (Visual Studio 2010 s p 1을 사용 하는 MSBuild의 버전)이이 속성에 존재 하지 않은 때문에 삽입 합니다. 기본값은 프로젝트 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-498">Because this property didn't exist in MSBuild 4.0 (the version of MSBuild that Visual Studio 2010 SP1 uses), we inject a default value into the project file.</span></span>

<span data-ttu-id="7d3c6-499">VSToolsPath 속성 MSBuildExtensionsPath32 설정에 의해 표시 된 경로에서 가져올 올바른.targets 파일 확인에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-499">The VSToolsPath property is used to determine the correct .targets file to import from the path represented by the MSBuildExtensionsPath32 setting.</span></span>

<span data-ttu-id="7d3c6-500">Import 요소와 관련 된 몇 가지 변경 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-500">There are also some changes related to Import elements.</span></span> <span data-ttu-id="7d3c6-501">이러한 변경이 Visual Studio의 두 버전 간의 호환성을 지원 하기 위해 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-501">These changes are required in order to support compatibility between both versions of Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="7d3c6-502">프로젝트는 두 개의 서로 다른 컴퓨터에 Visual Studio 2010 SP1 및 Visual Studio 11 베타 간에 공유 되 고 하 고 프로젝트에 응용 프로그램에서 로컬 데이터베이스를 포함 하는 경우\_데이터 폴더를 확인 해야 데이터베이스에 사용 되는 SQL Server 버전이 두 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-502">If a project is being shared between Visual Studio 2010 SP1 and Visual Studio 11 Beta on two different computers, and if the project includes a local database in the App\_Data folder, you must make sure that the version of SQL Server used by the database is installed on both computers.</span></span>

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a><span data-ttu-id="7d3c6-503">ASP.NET 4.5 웹 사이트 템플릿의 구성 변경 내용</span><span class="sxs-lookup"><span data-stu-id="7d3c6-503">Configuration Changes in ASP.NET 4.5 Website Templates</span></span>

<span data-ttu-id="7d3c6-504">다음과 같이 변경 기본값에 적용 된 *Web.config* Visual Studio 2012 릴리스 후보에서 웹 사이트 템플릿을 사용 하 여 만든 사이트에 대 한 파일:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-504">The following changes have been made to the default *Web.config* file for site that are created using website templates in Visual Studio 2012 Release Candidate:</span></span>

- <span data-ttu-id="7d3c6-505">에 `<httpRuntime>` 요소는 `encoderType` 특성은 이제 ASP.NET에 추가 된 AntiXSS 형식을 사용 하도록 기본값으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-505">In the `<httpRuntime>` element, the `encoderType` attribute is now set by default to use the AntiXSS types that were added to ASP.NET.</span></span> <span data-ttu-id="7d3c6-506">자세한 내용은 참조 [AntiXSS 라이브러리](#_Toc318097382)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-506">For details, see [AntiXSS Library](#_Toc318097382).</span></span>
- <span data-ttu-id="7d3c6-507">또한는 `<httpRuntime>` 요소는 `requestValidationMode` 특성을 "4.5"로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-507">Also in the `<httpRuntime>` element, the `requestValidationMode` attribute is set to "4.5".</span></span> <span data-ttu-id="7d3c6-508">즉, 기본적으로 지연된 ("지연") 유효성 검사를 사용 하도록 요청 유효성 검사 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-508">This means that by default, request validation is configured to use deferred ("lazy") validation.</span></span> <span data-ttu-id="7d3c6-509">자세한 내용은 참조 [새로운 ASP.NET 요청 유효성 검사 기능](#_Toc318097379)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-509">For details, see [New ASP.NET Request Validation Features](#_Toc318097379).</span></span>
- <span data-ttu-id="7d3c6-510">`<modules>` 의 요소는 `<system.webServer>` 섹션에 포함 되어 있지 않습니다는 `runAllManagedModulesForAllRequests` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-510">The `<modules>` element of the `<system.webServer>` section does not contain a `runAllManagedModulesForAllRequests` attribute.</span></span> <span data-ttu-id="7d3c6-511">(기본값은 false입니다.) 즉, s p 1로 업데이트 되지 않은 IIS 7의 버전을 사용 하는 경우 새 사이트에서의 라우팅 문제를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-511">(Its default value is false.) This means that if you are using a version of IIS 7 that has not been updated to SP1, you might have issues with routing in a new site.</span></span> <span data-ttu-id="7d3c6-512">자세한 내용은 참조 [ASP.NET 라우팅에 대 한 IIS 7에서 기본적으로 지원](#Native_Support_In_IIS7_For_ASPNET_Routine)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-512">For more information, see [Native Support in IIS 7 for ASP.NET Routing](#Native_Support_In_IIS7_For_ASPNET_Routine).</span></span>

<span data-ttu-id="7d3c6-513">이러한 변경 내용은 기존 응용 프로그램 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-513">These changes do not affect existing applications.</span></span> <span data-ttu-id="7d3c6-514">그러나 기존 웹 사이트 및 새 템플릿을 사용 하 여 ASP.NET 4.5에 대해 만드는 새 웹 사이트 간 동작의 차이 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-514">However, they might represent a difference in behavior between existing websites and new websites that you create for ASP.NET 4.5 using the new templates.</span></span>

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a><span data-ttu-id="7d3c6-515">ASP.NET 라우팅에 대 한 IIS 7에서에서 기본적으로 지원</span><span class="sxs-lookup"><span data-stu-id="7d3c6-515">Native Support in IIS 7 for ASP.NET Routing</span></span>

<span data-ttu-id="7d3c6-516">이것은 ASP.NET에 대 한 변경 이므로 아니며 SP1 업데이트 적용에 있던 IIS 7의 버전을 작업 하는 경우 영향을 주는 새 웹 사이트 프로젝트에 대 한 템플릿 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-516">This is not a change to ASP.NET as such, but a change in templates for new website projects that can affect you if you are working a version of IIS 7 that has not had the SP1 update applied.</span></span>

<span data-ttu-id="7d3c6-517">Asp.net에서는 다음 구성 설정의 라우팅을 지원 하기 위해 응용 프로그램에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-517">In ASP.NET, you can add the following configuration setting to applications in order to support routing:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

<span data-ttu-id="7d3c6-518">때 **runAllManagedModulesForAllRequests** true, 같은 URL은 `http://mysite/myapp/home` 있다 하더라도 ASP.NET에서로 이동 없습니다 *.aspx*, *.mvc*, 또는 유사한 확장에는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-518">When **runAllManagedModulesForAllRequests** is true, a URL like `http://mysite/myapp/home` goes to ASP.NET, even though there is no *.aspx*, *.mvc*, or similar extension on the URL.</span></span>

<span data-ttu-id="7d3c6-519">IIS 7에 수행한 업데이트는 **runAllManagedModulesForAllRequests** 불필요 한 설정 및 ASP.NET 라우팅은 고유 하 게 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-519">An update that was made to IIS 7 makes the **runAllManagedModulesForAllRequests** setting unnecessary and supports ASP.NET routing natively.</span></span> <span data-ttu-id="7d3c6-520">(업데이트에 대 한 내용은 Microsoft 지원 문서를 참조 하십시오. [업데이트가 사용 하도록 설정 된 Url의 요청을 처리 하는 IIS 7.0 또는 IIS 7.5 처리기 특정 마침표로 끝나지 않는 제공 되 고](https://support.microsoft.com/kb/980368).)</span><span class="sxs-lookup"><span data-stu-id="7d3c6-520">(For information about the update, see the Microsoft Support article [An update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).)</span></span>

<span data-ttu-id="7d3c6-521">웹 사이트는 IIS 7에서 실행 되 고 설정 해야 할 경우 IIS가 업데이트 된 하지 **runAllManagedModulesForAllRequests** true로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-521">If your website is running on IIS 7 and if IIS has been updated, you do not need to set **runAllManagedModulesForAllRequests** to true.</span></span> <span data-ttu-id="7d3c6-522">사실, true로 설정 좋지 않습니다, 불필요 한 처리 오버 헤드가 요청에 추가 하기 때문에.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-522">In fact, setting it to true is not recommended, because it adds unnecessary processing overhead to request.</span></span> <span data-ttu-id="7d3c6-523">이 설정은 true를 포함 하 여 요청을 모두 *.htm*, *.jpg*, 다른 정적 파일에도 ASP.NET 요청 파이프라인을 통해 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-523">When this setting is true, all requests, including those for *.htm*, *.jpg*, and other static files, also go through the ASP.NET request pipeline.</span></span>

<span data-ttu-id="7d3c6-524">Visual Studio 2012 RC에 제공 되는 템플릿을 사용 하 여 새 ASP.NET 4.5 웹 사이트를 만들 경우 웹 사이트에 대 한 구성을 포함 되지 않습니다는 **runAllManagedModulesForAllRequests** 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-524">If you create a new ASP.NET 4.5 website using the templates that are provided in Visual Studio 2012 RC, the configuration for the website does not include the **runAllManagedModulesForAllRequests** setting.</span></span> <span data-ttu-id="7d3c6-525">즉, 기본적으로 설정이 임을 false.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-525">This means that by default the setting is false.</span></span>

<span data-ttu-id="7d3c6-526">실행 하면 웹 사이트에서 Windows 7 s p 1을 설치 하지 않고, IIS 7 필요한 업데이트를 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-526">If you then run the website on Windows 7 without SP1 installed, IIS 7 will not include the required update.</span></span> <span data-ttu-id="7d3c6-527">결과적으로 라우팅이 작동 하지 않습니다 및 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-527">As a consequence, routing will not work and you will see errors.</span></span> <span data-ttu-id="7d3c6-528">문제가 있습니다. 여기서 라우팅이 작동 하지 않습니다, 다음 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-528">If you have a problem where routing does not work, you can do either the following:</span></span>

- <span data-ttu-id="7d3c6-529">Windows 7 s p 1에서는 IIS 7에 업데이트를 추가 하는 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-529">Update Windows 7 to SP1, which will add the update to IIS 7.</span></span>
- <span data-ttu-id="7d3c6-530">앞에 나열 된 Microsoft 지원 문서에서 설명 하는 업데이트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-530">Install the update that's described in the Microsoft Support article listed previously.</span></span>
- <span data-ttu-id="7d3c6-531">설정 **runAllManagedModulesForAllRequests** 해당 웹 사이트의 Web.config 파일에서 true로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-531">Set **runAllManagedModulesForAllRequests** to true in that website's Web.config file.</span></span> <span data-ttu-id="7d3c6-532">요청에 약간의 오버 헤드를 추가 합니다이 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-532">Note that this will add some overhead to requests.</span></span>

<a id="_Toc318097397"></a>
### <a name="html-editor"></a><span data-ttu-id="7d3c6-533">HTML 편집기</span><span class="sxs-lookup"><span data-stu-id="7d3c6-533">HTML Editor</span></span>

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a><span data-ttu-id="7d3c6-534">스마트 작업</span><span class="sxs-lookup"><span data-stu-id="7d3c6-534">Smart Tasks</span></span>

<span data-ttu-id="7d3c6-535">디자인 뷰에서 종종에 서버 컨트롤의 복잡 한 속성 대화 상자와 마법사 쉽게 설정할 수 있도록 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-535">In Design view, complex properties of server controls often have associated dialog boxes and wizards to make it easy to set them.</span></span> <span data-ttu-id="7d3c6-536">예를 들어 데이터 소스를 추가 하려면 특별 한 대화 상자를 사용할 수는 *반복기* 제어 하거나 열을 추가 하는 *GridView* 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-536">For example, you can use a special dialog box to add a data source to a *Repeater* control or add columns to a *GridView* control.</span></span>

<span data-ttu-id="7d3c6-537">그러나이 유형의 복잡 한 속성에 대 한 UI 도움말 소스 뷰에서 제공 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-537">However, this type of UI help for complex properties has not been available in Source view.</span></span> <span data-ttu-id="7d3c6-538">따라서 Visual Studio 11에서는 소스 뷰에 대 한 스마트 작업을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-538">Therefore, Visual Studio 11 introduces Smart Tasks for Source view.</span></span> <span data-ttu-id="7d3c6-539">스마트 작업은 C# 및 Visual Basic 편집기에서 일반적으로 사용 되는 기능에 대 한 바로 가기 키를 컨텍스트 인식 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-539">Smart Tasks are context-aware shortcuts for commonly used features in the C# and Visual Basic editors.</span></span>

<span data-ttu-id="7d3c6-540">ASP.NET Web Forms 컨트롤에 대 한 스마트 작업이 전자 메일 서버 태그에 작은 문자 모양 요소 안에 삽입 지점이 있을 경우:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-540">For ASP.NET Web Forms controls, Smart Tasks appear on server tags as a small glyph when the insertion point is inside the element:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

<span data-ttu-id="7d3c6-541">스마트 작업 문자 모양을 클릭 하거나 CTRL + 때 확장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-541">The Smart Task expands when you click the glyph or press CTRL+.</span></span> <span data-ttu-id="7d3c6-542">(점), 코드 편집기에서와 마찬가지로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-542">(dot), just as in the code editors.</span></span> <span data-ttu-id="7d3c6-543">디자인 뷰의 스마트 작업과 유사 하 게 되는 바로 가기를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-543">It then displays shortcuts that are similar to the Smart Tasks in Design view.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

<span data-ttu-id="7d3c6-544">예를 들어 위의 그림에서 스마트 작업 GridView 작업 옵션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-544">For example, the Smart Task in the previous illustration shows the GridView Tasks options.</span></span> <span data-ttu-id="7d3c6-545">열 편집을 선택 하는 경우 다음과 같은 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-545">If you choose Edit Columns, the following dialog box is displayed:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

<span data-ttu-id="7d3c6-546">대화 상자 집합의 동일한 속성을 채우는 디자인 보기에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-546">Filling in the dialog box sets the same properties you can set in Design view.</span></span> <span data-ttu-id="7d3c6-547">확인을 클릭 하면 컨트롤에 대 한 태그 새 설정으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-547">When you click OK, the markup for the control is updated with the new settings:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a><span data-ttu-id="7d3c6-548">WAI ARIA 지원</span><span class="sxs-lookup"><span data-stu-id="7d3c6-548">WAI-ARIA support</span></span>

<span data-ttu-id="7d3c6-549">액세스할 수 있는 웹 사이트 작성 점점 더 중요 해지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-549">Writing accessible websites is becoming increasingly important.</span></span> <span data-ttu-id="7d3c6-550">[WAI ARIA 내게 필요한 옵션 표준](http://www.w3.org/WAI/intro/aria) 개발자 해야 액세스할 수 있는 웹 사이트를 작성 하는 방법을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-550">The [WAI-ARIA accessibility standard](http://www.w3.org/WAI/intro/aria) defines how developers should write accessible websites.</span></span> <span data-ttu-id="7d3c6-551">이제이 표준 Visual Studio에서 완전히 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-551">This standard is now fully supported in Visual Studio.</span></span>

<span data-ttu-id="7d3c6-552">예를 들어는 *역할* 특성에는 이제 전체 IntelliSense에:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-552">For example, the *role* attribute now has full IntelliSense:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

<span data-ttu-id="7d3c6-553">WAI ARIA 표준 접두사로 사용 하는 특성은 또한 제공 *aria-* HTML5 문서 의미 체계를 추가할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-553">The WAI-ARIA standard also introduces attributes that are prefixed with *aria-* that let you add semantics to an HTML5 document.</span></span> <span data-ttu-id="7d3c6-554">Visual Studio에 이러한 항목을 완전히 지원 *aria-* 특성:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-554">Visual Studio also fully supports these *aria-* attributes:</span></span>

<span data-ttu-id="7d3c6-555">![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="7d3c6-555">![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)</span></span>

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a><span data-ttu-id="7d3c6-556">새 HTML5 조각</span><span class="sxs-lookup"><span data-stu-id="7d3c6-556">New HTML5 snippets</span></span>

<span data-ttu-id="7d3c6-557">자주 사용 되는 HTML5 태그를 작성을 쉽고 빠르게을 하려면 Visual Studio에 조각의 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-557">To make it faster and easier to write commonly used HTML5 markup, Visual Studio includes a number of snippets.</span></span> <span data-ttu-id="7d3c6-558">예는 비디오 조각을.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-558">An example is the video snippet:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

<span data-ttu-id="7d3c6-559">코드 조각으로 호출 하려면 tab 키를 누른 채 IntelliSense에서 요소를 선택 하는 경우에 두 번:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-559">To invoke the snippet, press Tab twice when the element is selected in IntelliSense:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

<span data-ttu-id="7d3c6-560">사용자 지정할 수 있는 코드 조각을 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-560">This produces a snippet that you can customize.</span></span>

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a><span data-ttu-id="7d3c6-561">사용자 정의 컨트롤로 추출</span><span class="sxs-lookup"><span data-stu-id="7d3c6-561">Extract to user control</span></span>

<span data-ttu-id="7d3c6-562">큰 웹 페이지에서 개별 조각을 사용자 정의 컨트롤로 이동 하는 것이 좋습니다 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-562">In large web pages, it can be a good idea to move individual pieces into user controls.</span></span> <span data-ttu-id="7d3c6-563">이러한 형태의 리팩터링 페이지의 가독성을 높일 수 있습니다 및 페이지 구조를 단순화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-563">This form of refactoring can help increase the readability of the page and can simplify the page structure.</span></span>

<span data-ttu-id="7d3c6-564">간단 하 게 하려면이 소스 뷰에서 Web Forms 페이지를 편집할 때 있습니다 수 이제 페이지에 텍스트를 선택, 마우스 오른쪽 단추로 클릭 한 다음 사용자 정의 컨트롤로 추출.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-564">To make this easier, when you edit Web Forms pages in Source view, you can now select text in a page, right-click it, and then choose Extract to User Control:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a><span data-ttu-id="7d3c6-565">특성에 중요 코드에 대 한 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="7d3c6-565">IntelliSense for code nuggets in attributes</span></span>

<span data-ttu-id="7d3c6-566">Visual Studio는 항상 모든 페이지 또는 제어에 서버 쪽 코드 조각에 대 한 IntelliSense를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-566">Visual Studio has always provided IntelliSense for server-side code nuggets in any page or control.</span></span> <span data-ttu-id="7d3c6-567">이제 Visual Studio에서 HTML 특성에도 코드 조각에 대 한 IntelliSense를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-567">Now Visual Studio includes IntelliSense for code nuggets in HTML attributes as well.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

<span data-ttu-id="7d3c6-568">이렇게 하면 데이터 바인딩 식을 만드는 쉽게:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-568">This makes it easier to create data-binding expressions:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a><span data-ttu-id="7d3c6-569">태그를 일치 하는 여는 태그 또는 닫는 태그의 이름을 바꾸면의 자동 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="7d3c6-569">Automatic renaming of matching tag when you rename an opening or closing tag</span></span>

<span data-ttu-id="7d3c6-570">HTML 요소의 이름을 바꾸는 경우 (변경 하는 예를 들어는 *div* 되도록 태그는 *헤더* 태그), 해당를 열거나 닫는 태그를 실시간으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-570">If you rename an HTML element (for example, you change a *div* tag to be a *header* tag), the corresponding opening or closing tag also changes in real time.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

<span data-ttu-id="7d3c6-571">이 잘못 변경 하거나 닫는 태그를 변경 하 시겠습니까 오류를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-571">This helps avoid the error where you forget to change a closing tag or change the wrong one.</span></span>

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a><span data-ttu-id="7d3c6-572">이벤트 처리기 생성</span><span class="sxs-lookup"><span data-stu-id="7d3c6-572">Event handler generation</span></span>

<span data-ttu-id="7d3c6-573">이제 visual Studio 이벤트 처리기를 작성 하 고 수동으로 바인딩할 수 있도록 소스 뷰에서 기능이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-573">Visual Studio now includes features in Source view to help you write event handlers and bind them manually.</span></span> <span data-ttu-id="7d3c6-574">소스 뷰에서 이벤트 이름을 편집 하는 경우 IntelliSense 표시 &lt;새 이벤트 만들&gt;, 올바른 서명이 있는 이벤트 처리기에서에서 만들 페이지의 코드를:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-574">If you are editing an event name in Source view, IntelliSense displays &lt;Create New Event&gt;, which will create an event handler in the page's code that has the right signature:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

<span data-ttu-id="7d3c6-575">기본적으로 이벤트 처리기의 이벤트 처리 메서드 이름에 대 한 컨트롤의 ID를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-575">By default, the event handler will use the control's ID for the name of the event-handling method:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

<span data-ttu-id="7d3c6-576">결과 이벤트 처리기는이 예제의 C#에서 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-576">The resulting event handler will look like this (in this case, in C#):</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a><span data-ttu-id="7d3c6-577">스마트 들여쓰기</span><span class="sxs-lookup"><span data-stu-id="7d3c6-577">Smart indent</span></span>

<span data-ttu-id="7d3c6-578">빈 HTML 요소 내부에 있는 동안 Enter 키를 누를 때 편집기 적절 한 위치에 삽입 포인터를 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-578">When you press Enter while inside an empty HTML element, the editor will put the insertion point in the right place:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

<span data-ttu-id="7d3c6-579">Enter 키를 눌러이 위치에 닫는 태그가 아래로 이동이 고 여는 태그와 일치 하도록 들여씁니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-579">If you press Enter in this location, the closing tag is moved down and indented to match the opening tag.</span></span> <span data-ttu-id="7d3c6-580">삽입 지점이 들여쓰기 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-580">The insertion point is also indented:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a><span data-ttu-id="7d3c6-581">문 완성 자동 감소</span><span class="sxs-lookup"><span data-stu-id="7d3c6-581">Auto-reduce statement completion</span></span>

<span data-ttu-id="7d3c6-582">Visual Studio 지금 필터만 관련 옵션 표시 되도록 입력 내용에 따라 IntelliSense 목록:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-582">The IntelliSense list in Visual Studio now filters based on what you type so that it displays only relevant options:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

<span data-ttu-id="7d3c6-583">IntelliSense 필터 또한 IntelliSense 목록에는 개별 단어의 제목 대/소문자에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-583">IntelliSense also filters based on the title case of the individual words in the IntelliSense list.</span></span> <span data-ttu-id="7d3c6-584">예를 들어 "dl"를 입력 하면 dl 및 asp DataList 모두 표시 됩니다.:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-584">For example, if you type "dl", both dl and asp:DataList are displayed:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

<span data-ttu-id="7d3c6-585">이 기능을 사용 하면 더 빠르게 알려진된 요소에 대 한 문 완성을 얻으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-585">This feature makes it faster to get statement completion for known elements.</span></span>

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a><span data-ttu-id="7d3c6-586">JavaScript 편집기</span><span class="sxs-lookup"><span data-stu-id="7d3c6-586">JavaScript Editor</span></span>

<span data-ttu-id="7d3c6-587">Visual Studio 2012 릴리스 후보의 JavaScript 편집기는 완전히 새로운 기능이 며 Visual Studio에서 JavaScript를 사용 하는 환경을 크게 높여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-587">The JavaScript editor in Visual Studio 2012 Release Candidate is completely new and it greatly improves the experience of working with JavaScript in Visual Studio.</span></span>

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a><span data-ttu-id="7d3c6-588">코드 개요</span><span class="sxs-lookup"><span data-stu-id="7d3c6-588">Code outlining</span></span>

<span data-ttu-id="7d3c6-589">이제 개요 영역 현재 포커스와 관련이 없는 일부 파일을 축소할 수 있도록 하는 모든 함수에 대해 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-589">Outlining regions are now automatically created for all functions, allowing you to collapse parts of the file that aren't pertinent to your current focus.</span></span>

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a><span data-ttu-id="7d3c6-590">중괄호 일치</span><span class="sxs-lookup"><span data-stu-id="7d3c6-590">Brace matching</span></span>

<span data-ttu-id="7d3c6-591">중괄호와 닫는 중괄호에 삽입 포인터를 놓으면 나와 일치 하는 편집기에서 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-591">When you put the insertion point on an opening or closing brace, the editor highlights the matching one.</span></span>

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a><span data-ttu-id="7d3c6-592">정의로 이동</span><span class="sxs-lookup"><span data-stu-id="7d3c6-592">Go to Definition</span></span>

<span data-ttu-id="7d3c6-593">로 이동 명령 정의 사용 하면 함수 또는 변수에 대 한 소스로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-593">The Go to Definition command lets you jump to the source for a function or variable.</span></span>

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a><span data-ttu-id="7d3c6-594">ECMAScript5 지원</span><span class="sxs-lookup"><span data-stu-id="7d3c6-594">ECMAScript5 support</span></span>

<span data-ttu-id="7d3c6-595">편집기 ECMAScript5, JavaScript 언어에 설명 하는 표준의 최신 버전의에서 새로운 구문 및 Api를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-595">The editor supports the new syntax and APIs in ECMAScript5, the latest version of the standard that describes the JavaScript language.</span></span>

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a><span data-ttu-id="7d3c6-596">DOM IntelliSense</span><span class="sxs-lookup"><span data-stu-id="7d3c6-596">DOM IntelliSense</span></span>

<span data-ttu-id="7d3c6-597">DOM Api에 대 한 IntelliSense 기능이 개선 되어 비롯 한 많은 새 HTML5 Api를 지 원하는 *querySelector*, DOM 저장, 교차 문서 메시징 및 *캔버스*합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-597">IntelliSense for DOM APIs has been improved, with support for many new HTML5 APIs including *querySelector*, DOM Storage, cross-document messaging, and *canvas*.</span></span> <span data-ttu-id="7d3c6-598">이제 DOM IntelliSense는 네이티브 형식 라이브러리 정의 아니라 단일 단순한 JavaScript 파일에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-598">DOM IntelliSense is now driven by a single simple JavaScript file, rather than by a native type library definition.</span></span> <span data-ttu-id="7d3c6-599">따라서 쉽게 확장 하거나 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-599">This makes it easy to extend or replace.</span></span>

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a><span data-ttu-id="7d3c6-600">VSDOC 서명이 오버 로드</span><span class="sxs-lookup"><span data-stu-id="7d3c6-600">VSDOC signature overloads</span></span>

<span data-ttu-id="7d3c6-601">자세한 IntelliSense 설명이 이제 선언할 수 JavaScript 함수의 별도 오버 로드에 대 한 새 사용 하 여  *&lt;서명&gt;*  요소를이 예제에 나와 있는 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-601">Detailed IntelliSense comments can now be declared for separate overloads of JavaScript functions by using the new *&lt;signature&gt;* element, as shown in this example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a><span data-ttu-id="7d3c6-602">암시적 참조</span><span class="sxs-lookup"><span data-stu-id="7d3c6-602">Implicit references</span></span>

<span data-ttu-id="7d3c6-603">이제 암시적으로 포함 될 파일의 목록에 지정 된 JavaScript 파일 또는 블록 참조 수 있음을 의미가 해당 내용에 대 한 IntelliSense를 얻을 수 중앙 목록에 JavaScript 파일을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-603">You can now add JavaScript files to a central list that will be implicitly included in the list of files that any given JavaScript file or block references, meaning you'll get IntelliSense for its contents.</span></span> <span data-ttu-id="7d3c6-604">예를 들어, jQuery 파일의 파일을 중앙 목록에 추가할 수 있습니다 및 얻게 됩니다 IntelliSense jQuery 함수에 대 한 파일의 모든 JavaScript 블록에서 명시적으로 참조 한 여부 (/ / /를 사용 하 여 &lt;참조 /&gt;) 여부.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-604">For example, you can add jQuery files to the central list of files, and you'll get IntelliSense for jQuery functions in any JavaScript block of file, whether you've referenced it explicitly (using /// &lt;reference /&gt;) or not.</span></span>

<a id="_Toc318097415"></a>
### <a name="css-editor"></a><span data-ttu-id="7d3c6-605">CSS 편집기</span><span class="sxs-lookup"><span data-stu-id="7d3c6-605">CSS Editor</span></span>

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a><span data-ttu-id="7d3c6-606">문 완성 자동 감소</span><span class="sxs-lookup"><span data-stu-id="7d3c6-606">Auto-reduce statement completion</span></span>

<span data-ttu-id="7d3c6-607">CSS 속성을 기반으로 하는 CSS 지금 필터 및 선택한 스키마에서 지 원하는 값에 대 한 IntelliSense 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-607">The IntelliSense list for CSS now filters based on the CSS properties and values supported by the selected schema.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

<span data-ttu-id="7d3c6-608">IntelliSense는 또한 제목 사례 검색을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-608">IntelliSense also supports title case searches:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a><span data-ttu-id="7d3c6-609">계층적 들여쓰기</span><span class="sxs-lookup"><span data-stu-id="7d3c6-609">Hierarchical indentation</span></span>

<span data-ttu-id="7d3c6-610">CSS 편집기를 사용 하 여 들여쓰기 계층적 규칙을 표시 한 연계 규칙은 논리적으로 구성 하는 방식을 간략하게 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-610">The CSS editor uses indentation to display hierarchical rules, which gives you an overview of how the cascading rules are logically organized.</span></span> <span data-ttu-id="7d3c6-611">다음 예제에서는 #list 선택 기가 목록의 연계 자식 이며 따라서 들여쓰기 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-611">In the following example, the #list a selector is a cascading child of list and is therefore indented.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

<span data-ttu-id="7d3c6-612">다음 예제에서는 보다 복잡 한 상속을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-612">The following example shows more complex inheritance:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

<span data-ttu-id="7d3c6-613">규칙의 들여쓰기는 해당 부모 규칙에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-613">The indentation of a rule is determined by its parent rules.</span></span> <span data-ttu-id="7d3c6-614">계층적 들여쓰기는 기본적으로 사용 하도록 설정 하지만 (도구, 메뉴 모음에서 옵션) 옵션 대화 상자를 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-614">Hierarchical indentation is enabled by default, but you can disable it the Options dialog box (Tools, Options from the menu bar):</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a><span data-ttu-id="7d3c6-615">CSS 해킹 지원</span><span class="sxs-lookup"><span data-stu-id="7d3c6-615">CSS hacks support</span></span>

<span data-ttu-id="7d3c6-616">수백 대의 실제 CSS 파일 분석 CSS 핵 (hack)은 매우 일반적인 및 가장 널리 사용 되는 것과 Visual Studio에서 지원 되는 이제 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-616">Analysis of hundreds of real-world CSS files shows that CSS hacks are very common, and now Visual Studio supports the most widely used ones.</span></span> <span data-ttu-id="7d3c6-617">이 지원에는 IntelliSense 및 유효성 검사 핫스폿에 포함 됩니다 (\*) 및 밑줄 (\_) 속성 핵 (hack):</span><span class="sxs-lookup"><span data-stu-id="7d3c6-617">This support includes IntelliSense and validation of the star (\*) and underscore (\_) property hacks:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

<span data-ttu-id="7d3c6-618">일반적인 선택기 해킹 적용 될 때에 계층적 들여쓰기 유지 되도록도 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-618">Typical selector hacks are also supported so that hierarchical indentation is maintained even when they are applied.</span></span> <span data-ttu-id="7d3c6-619">Internet Explorer 7을 대상으로 사용 되는 일반적인 선택기 해킹 된 선택기 앞에 추가 하는 것  *\*: 첫 번째 자식 + html*합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-619">A typical selector hack used to target Internet Explorer 7 is to prepend a selector with *\*:first-child + html*.</span></span> <span data-ttu-id="7d3c6-620">해당 규칙을 사용 하 여 계층적 들여쓰기를 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-620">Using that rule will maintain the hierarchical indentation:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a><span data-ttu-id="7d3c6-621">공급 업체 특정 스키마 (-moz--webkit)</span><span class="sxs-lookup"><span data-stu-id="7d3c6-621">Vendor specific schemas (-moz-, -webkit)</span></span>

<span data-ttu-id="7d3c6-622">CSS3 서로 다른 시간에 다른 브라우저에서 구현 된 많은 속성을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-622">CSS3 introduces many properties that have been implemented by different browsers at different times.</span></span> <span data-ttu-id="7d3c6-623">이 이전에 공급 업체 특정 구문을 사용 하 여 개발자가 특정 브라우저에 대 한 코드를을 강제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-623">This previously forced developers to code for specific browsers by using vendor-specific syntax.</span></span> <span data-ttu-id="7d3c6-624">이러한 브라우저와 관련 속성은 이제 IntelliSense에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-624">These browser-specific properties are now included in IntelliSense.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a><span data-ttu-id="7d3c6-625">주석 및 주석 처리를 제거 지원</span><span class="sxs-lookup"><span data-stu-id="7d3c6-625">Commenting and uncommenting support</span></span>

<span data-ttu-id="7d3c6-626">이제 주석 처리 하 고 (Ctrl + K, 메모로 C 및 Ctrl + K, 주석 처리를 제거 하 여) 코드 편집기에서 사용 하는 동일한 바로 가기 키를 사용 하 여 CSS 규칙을 주석 처리 제거 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-626">You can now comment and uncomment CSS rules using the same shortcuts that you use in the code editor (Ctrl+K,C to comment and Ctrl+K,U to uncomment).</span></span>

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a><span data-ttu-id="7d3c6-627">색 선택</span><span class="sxs-lookup"><span data-stu-id="7d3c6-627">Color picker</span></span>

<span data-ttu-id="7d3c6-628">이전 버전의 Visual Studio에서는 IntelliSense 색상 관련 특성에 대 한 명명 된 색 값의 드롭다운 목록으로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-628">In previous versions of Visual Studio, IntelliSense for color-related attributes consisted of a drop-down list of named color values.</span></span> <span data-ttu-id="7d3c6-629">해당 목록에 모든 기능을 갖춘 색 선택 하 여 대체 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-629">That list has been replaced by a full-featured color picker.</span></span>

<span data-ttu-id="7d3c6-630">색 값을 입력 하면 색 선택 자동으로 표시 되 고 뒤에 기본 색 색상표에 따라 이전에 사용한 색 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-630">When you enter a color value, the color picker is displayed automatically and presents a list of previously used colors followed by a default color palette.</span></span> <span data-ttu-id="7d3c6-631">마우스나 키보드를 사용 하 여 색을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-631">You can select a color using the mouse or the keyboard.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

<span data-ttu-id="7d3c6-632">목록 전체 색상 선택기 구조로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-632">The list can be expanded into a complete color picker.</span></span> <span data-ttu-id="7d3c6-633">고 선택기 불투명도 슬라이더를 움직이면 RGBA를 색을 자동으로 변환 하 여 알파 채널을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-633">The picker lets you control the alpha channel by automatically converting any color into RGBA when you move the opacity slider:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a><span data-ttu-id="7d3c6-634">코드 조각</span><span class="sxs-lookup"><span data-stu-id="7d3c6-634">Snippets</span></span>

<span data-ttu-id="7d3c6-635">CSS 편집기에서 코드 조각을 더 쉽고 빠르게 교차 브라우저 스타일을 만들 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-635">Snippets in the CSS editor make it easier and faster to create cross-browser styles.</span></span> <span data-ttu-id="7d3c6-636">이제 브라우저별 설정 해야 하는 많은 CSS3 속성 조각으로 롤백 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-636">Many CSS3 properties that require browser-specific settings have now been rolled into snippets.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

<span data-ttu-id="7d3c6-637">CSS 조각에서 기호를 입력 하 여 (예: CSS3 미디어 쿼리) 고급 시나리오를 지원 합니다 (@), IntelliSense 목록 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-637">CSS snippets support advanced scenarios (like CSS3 media queries) by typing the at-symbol (@), which shows the IntelliSense list.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

<span data-ttu-id="7d3c6-638">선택 하는 경우 @media 값 및 Tab 키를 눌러, CSS 편집기에 다음 코드 조각 삽입:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-638">When you select @media value and press Tab, the CSS editor inserts the following snippet:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

<span data-ttu-id="7d3c6-639">코드 조각에서와 마찬가지로 사용자 고유의 CSS 조각을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-639">As with snippets for code, you can create your own CSS snippets.</span></span>

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a><span data-ttu-id="7d3c6-640">사용자 지정 영역</span><span class="sxs-lookup"><span data-stu-id="7d3c6-640">Custom regions</span></span>

<span data-ttu-id="7d3c6-641">이미에서 사용할 수 있는 코드 편집기에서 코드 영역을 명명 된 CSS 편집을 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-641">Named code regions, which are already available in the code editor, are now available for CSS editing.</span></span> <span data-ttu-id="7d3c6-642">이렇게 하면 관련된 스타일 블록을 쉽게 그룹화 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-642">This lets you easily group related style blocks.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

<span data-ttu-id="7d3c6-643">영역이 축소 된 영역의 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-643">When a region is collapsed it displays the name of the region:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a><span data-ttu-id="7d3c6-644">페이지 검사기</span><span class="sxs-lookup"><span data-stu-id="7d3c6-644">Page Inspector</span></span>

<span data-ttu-id="7d3c6-645">페이지 검사기는 Visual Studio IDE에서 웹 페이지 (HTML, Web Forms, ASP.NET MVC 또는 웹 페이지)를 렌더링 하 고 소스 코드와 출력 결과 살펴볼 수 있습니다 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-645">Page Inspector is a tool that renders a web page (HTML, Web Forms, ASP.NET MVC, or Web Pages) in the Visual Studio IDE and lets you examine both the source code and the resulting output.</span></span> <span data-ttu-id="7d3c6-646">페이지 검사기는 ASP.NET 페이지에 대 한 서버 쪽 코드는 브라우저에 렌더링 하는 HTML 태그에서 발생을 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-646">For ASP.NET pages, Page Inspector lets you determine which server-side code has produced the HTML markup that is rendered to the browser.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

<span data-ttu-id="7d3c6-647">페이지 검사기에 대 한 자세한 내용은 다음 자습서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-647">For more information about Page Inspector, please see the following tutorials:</span></span>

- <span data-ttu-id="7d3c6-648">페이지 검사기를 사용 하 여 [ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)</span><span class="sxs-lookup"><span data-stu-id="7d3c6-648">Using Page Inspector in [ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)</span></span>
- <span data-ttu-id="7d3c6-649">페이지 검사기를 사용 하 여 [ASP.NET Web Forms](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)</span><span class="sxs-lookup"><span data-stu-id="7d3c6-649">Using Page Inspector in [ASP.NET Web Forms](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)</span></span>

<a id="_Toc318097425"></a>
### <a name="publishing"></a><span data-ttu-id="7d3c6-650">게시</span><span class="sxs-lookup"><span data-stu-id="7d3c6-650">Publishing</span></span>

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a><span data-ttu-id="7d3c6-651">게시 프로필</span><span class="sxs-lookup"><span data-stu-id="7d3c6-651">Publish profiles</span></span>

<span data-ttu-id="7d3c6-652">Visual Studio 2010에서 웹 응용 프로그램 프로젝트에 대 한 정보를 게시 하는 버전 제어에 저장 되지 않습니다 되며 다른 사용자와 공유 하는 데 설계 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-652">In Visual Studio 2010, publishing information for Web application projects is not stored in version control and is not designed for sharing with others.</span></span> <span data-ttu-id="7d3c6-653">Visual Studio 2012 릴리스 후보에서 게시 프로필의 형식이 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-653">In Visual Studio 2012 Release Candidate, the format of the publish profile has been changed.</span></span> <span data-ttu-id="7d3c6-654">팀 아티팩트를 향상 되었습니다 및 MSBuild에 따라 빌드에서 활용 하 여 이제 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-654">It has been made a team artifact, and it is now easy to leverage from builds based on MSBuild.</span></span> <span data-ttu-id="7d3c6-655">빌드 구성 정보는 게시 대화 상자에서 되므로 게시 하기 전에 빌드 구성을 쉽게 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-655">Build configuration information is in the Publish dialog box so that you can easily switch build configurations before publishing.</span></span>

<span data-ttu-id="7d3c6-656">게시 프로필 PublishProfiles 폴더에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-656">Publish profiles are stored in the PublishProfiles folder.</span></span> <span data-ttu-id="7d3c6-657">폴더의 위치에 따라 달라 집니다 사용 중인 프로그래밍 언어에:</span><span class="sxs-lookup"><span data-stu-id="7d3c6-657">The location of the folder depends on what programming language you are using:</span></span>

- <span data-ttu-id="7d3c6-658">C#: Properties\PublishProfiles</span><span class="sxs-lookup"><span data-stu-id="7d3c6-658">C#: Properties\PublishProfiles</span></span>
- <span data-ttu-id="7d3c6-659">Visual Basic: My Project\PublishProfiles</span><span class="sxs-lookup"><span data-stu-id="7d3c6-659">Visual Basic: My Project\PublishProfiles</span></span>

<span data-ttu-id="7d3c6-660">각 프로필은 MSBuild 파일.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-660">Each profile is an MSBuild file.</span></span> <span data-ttu-id="7d3c6-661">게시 중 프로젝트의 MSBuild 파일에이 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-661">During publishing, this file is imported into the project's MSBuild file.</span></span> <span data-ttu-id="7d3c6-662">Visual Studio 2010에서 게시 또는 패키지 프로세스에 변경 하려는 경우 해야 라는 파일에 사용자 지정 배치 **ProjectName**. wpp.targets 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-662">In Visual Studio 2010, if you want to make changes to the publish or package process, you have to put your customizations in a file named **ProjectName**.wpp.targets.</span></span> <span data-ttu-id="7d3c6-663">이것은 현재 지원 하지만 자체 게시 프로필에 이제 사용자 지정 항목을 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-663">This is still supported, but you can now put your customizations in the publish profile itself.</span></span> <span data-ttu-id="7d3c6-664">이런 방식으로 해당 프로필에 대 한 사용자 지정이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-664">That way, the customizations will be used only for that profile.</span></span>

<span data-ttu-id="7d3c6-665">이제 활용 하 여 MSBuild에서 프로필을 게시할 수도 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-665">You can now also leverage publish profiles from MSBuild.</span></span> <span data-ttu-id="7d3c6-666">이렇게 하려면 프로젝트를 빌드할 때 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-666">To do so, use the following command when you build the project:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

<span data-ttu-id="7d3c6-667">Project.csproj 값은 프로젝트의 경로 이며 ProfileName 게시 프로필의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-667">The project.csproj value is the path of the project, and ProfileName is the name of the profile to publish.</span></span> <span data-ttu-id="7d3c6-668">에 대 한 프로필 이름을 전달 하는 대신에 또는 *PublishProfile* 속성에 전달할 수 있습니다 전체 경로에 게시 프로필.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-668">Alternatively, instead of passing the profile name for the *PublishProfile* property, you can pass in the full path to the publish profile.</span></span>

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a><span data-ttu-id="7d3c6-669">ASP.NET 미리 컴파일 및 병합</span><span class="sxs-lookup"><span data-stu-id="7d3c6-669">ASP.NET precompilation and merge</span></span>

<span data-ttu-id="7d3c6-670">웹 응용 프로그램 프로젝트에 대 한 Visual Studio 2012 릴리스 후보 사이트의 콘텐츠를 게시 하는 경우 또는 패키지 프로젝트를 병합 하 고 미리 컴파일할 수 있는 웹 패키지 및 게시 속성 페이지에 대 한 옵션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-670">For Web application projects, Visual Studio 2012 Release Candidate adds an option on the Package/Publish Web properties page that lets you precompile and merge your site's content when you publish or package the project.</span></span> <span data-ttu-id="7d3c6-671">이러한 옵션을 보려면 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 속성을 선택한 다음 패키지/게시 웹 속성 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-671">To see these options, right-click the project in Solution Explorer, choose Properties, and then choose the Package/Publish Web property page.</span></span> <span data-ttu-id="7d3c6-672">다음 그림은 Precompile 옵션을 게시 하기 전에이 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-672">The following illustration shows the Precompile this application before publishing option.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

<span data-ttu-id="7d3c6-673">이 옵션을 선택 하면 Visual Studio 미리를 게시할 때마다 응용 프로그램 또는 웹 응용 프로그램 패키지를 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-673">When this option is selected, Visual Studio precompiles the application whenever you publish or package the web application.</span></span> <span data-ttu-id="7d3c6-674">사이트 미리 컴파일된 또는 어셈블리를 병합 하는 방법을 제어 하려면 이러한 옵션을 구성 하려면 고급 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-674">If you want to control how the site is precompiled or how assemblies are merged, click the Advanced button to configure those options.</span></span>

<a id="_Toc318097428"></a>
### <a name="iis-express"></a><span data-ttu-id="7d3c6-675">IIS Express</span><span class="sxs-lookup"><span data-stu-id="7d3c6-675">IIS Express</span></span>

<span data-ttu-id="7d3c6-676">Visual Studio에서 테스트 웹 프로젝트에 대 한 기본 웹 서버 IIS Express 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-676">The default web server for testing web projects in Visual Studio is now IIS Express.</span></span> <span data-ttu-id="7d3c6-677">Visual Studio 개발 서버를 개발 하는 동안 로컬 웹 서버에 대 한 옵션 하지만 IIS Express는 이제 권장 되는 서버.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-677">The Visual Studio Development Server is still an option for local web server during development, but IIS Express is now the recommended server.</span></span> <span data-ttu-id="7d3c6-678">IIS Express에서 Visual Studio 11 베타 사용 경험을 사용 하 여 Visual Studio 2010 s p 1에서과 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-678">The experience of using IIS Express in Visual Studio 11 Beta is very similar to using it in Visual Studio 2010 SP1.</span></span>

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a><span data-ttu-id="7d3c6-679">고지 사항</span><span class="sxs-lookup"><span data-stu-id="7d3c6-679">Disclaimer</span></span>

<span data-ttu-id="7d3c6-680">본 문서는 예비 문서이며, 여기에 설명한 소프트웨어의 최종 상업적 출시 전에 크게 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-680">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="7d3c6-681">이 문서에 포함된 정보는 게시 날짜 현재 논의된 문제에 대한 Microsoft Corporation의 당시 관점을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-681">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="7d3c6-682">Microsoft는 변화하는 시장 상황에 부응해야 하므로, Microsoft의 일부에 대한 책임으로 해석되어서는 안되며, 게시 날짜 이후 소개된 정보의 정확성을 Microsoft가 보증할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-682">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="7d3c6-683">이 백서는 정보 제공만을 목적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-683">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="7d3c6-684">Microsoft는 이 문서에 있는 정보에 대한 명시적 또는 묵시적, 법적인 보증을 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-684">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="7d3c6-685">해당 저작권법을 준수하는 것은 사용자의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-685">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="7d3c6-686">저작권에서의 권리와는 별도로, 이 설명서의 어떠한 부분도 Microsoft의 명시적인 서면 승인 없이는 어떠한 형식이나 수단(전기적, 기계적, 복사기에 의한 복사, 디스크 복사 또는 다른 방법) 또는 목적으로도 복제되거나, 검색 시스템에 저장 또는 도입되거나, 전송될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-686">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="7d3c6-687">Microsoft가 이 설명서 본안에 관련된 특허권, 상표권, 저작권 또는 기타 지적 재산권 등을 보유할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-687">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="7d3c6-688">서면 사용권 계약에 따라 Microsoft로부터 귀하에게 명시적으로 제공된 권리 이외에, 이 문서의 제공은 귀하에게 이러한 특허권, 상표권, 저작권, 또는 기타 지적 소유권 등에 대한 어떠한 사용권도 허여하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-688">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="7d3c6-689">다른 설명이 없는 한 예제 회사, 조직, 제품, 도메인 이름, 전자 메일 주소, 로고, 사람, 장소 및 이벤트 용례은 실제 데이터가 아닙니다과 연결 된 실제 회사, 조직, 제품, 도메인 이름, 전자 메일 주소, 로고, 사람, 장소 또는 이벤트 해서도 그렇게 유추 해서도 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-689">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="7d3c6-690">© 2012 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-690">© 2012 Microsoft Corporation.</span></span> <span data-ttu-id="7d3c6-691">All rights reserved.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-691">All rights reserved.</span></span>

<span data-ttu-id="7d3c6-692">Microsoft 및 Windows는 미국 및/또는 기타 국가에서 Microsoft Corporation의 상표이거나 등록된 상표입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-692">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="7d3c6-693">여기에 언급된 실제 회사와 제품의 이름은 각각 해당 소유자의 상표일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3c6-693">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>
