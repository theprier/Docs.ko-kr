---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: ASP.NET 4.5 및 Visual Studio 2012의 새로운 기능 | Microsoft Docs
author: rick-anderson
description: 이 문서에서는 새로운 기능과 향상 된 ASP.NET 4.5에서 도입 되는 설명 합니다. 웹 개발에 대해 수행 되는 향상 된 기능에 대해서도 설명 하는 중...
ms.author: aspnetcontent
ms.date: 02/29/2012
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: cfe9b1a7f05b43d5eb638c8fa7cb581d1edac9d5
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37835815"
---
<a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a><span data-ttu-id="11205-104">ASP.NET 4.5 및 Visual Studio 2012의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="11205-104">What's New in ASP.NET 4.5 and Visual Studio 2012</span></span>
====================
> <span data-ttu-id="11205-105">이 문서에서는 새로운 기능과 향상 된 ASP.NET 4.5에서 도입 되는 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-105">This document describes new features and enhancements that are being introduced in ASP.NET 4.5.</span></span> <span data-ttu-id="11205-106">또한 향상이 되 고 Visual Studio 2012에서 웹 개발에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-106">It also describes improvements being made for web development in Visual Studio 2012.</span></span> <span data-ttu-id="11205-107">이 문서를 2012 년 2 월 29 일에 처음 게시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-107">This document was originally published on February 29, 2012.</span></span>


- [<span data-ttu-id="11205-108">ASP.NET Core 런타임 및 프레임 워크</span><span class="sxs-lookup"><span data-stu-id="11205-108">ASP.NET Core Runtime and Framework</span></span>](#_Toc318097372)

    - [<span data-ttu-id="11205-109">비동기적으로 읽고 쓰는 HTTP 요청 및 응답</span><span class="sxs-lookup"><span data-stu-id="11205-109">Asynchronously Reading and Writing HTTP Requests and Responses</span></span>](#_Toc318097373)
    - [<span data-ttu-id="11205-110">HttpRequest 처리의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="11205-110">Improvements to HttpRequest handling</span></span>](#_Toc318097374)
    - [<span data-ttu-id="11205-111">응답을 비동기적으로 플러시</span><span class="sxs-lookup"><span data-stu-id="11205-111">Asynchronously flushing a response</span></span>](#_Toc318097375)
    - [<span data-ttu-id="11205-112">에 대 한 지원 *await* 하 고 *태스크*-기반 비동기 모듈과 처리기</span><span class="sxs-lookup"><span data-stu-id="11205-112">Support for *await* and *Task*-Based Asynchronous Modules and Handlers</span></span>](#_Toc318097376)
    - [<span data-ttu-id="11205-113">비동기 HTTP 모듈</span><span class="sxs-lookup"><span data-stu-id="11205-113">Asynchronous HTTP modules</span></span>](#_Toc318097377)
    - [<span data-ttu-id="11205-114">비동기 HTTP 처리기</span><span class="sxs-lookup"><span data-stu-id="11205-114">Asynchronous HTTP handlers</span></span>](#_Toc318097378)
    - [<span data-ttu-id="11205-115">새 ASP.NET 요청 유효성 검사 기능</span><span class="sxs-lookup"><span data-stu-id="11205-115">New ASP.NET Request Validation Features</span></span>](#_Toc318097379)
    - [<span data-ttu-id="11205-116">("지연") 요청 유효성 검사를 지연합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-116">Deferred ("lazy") request validation</span></span>](#_Toc318097380)
    - [<span data-ttu-id="11205-117">유효성이 검사 되지 않은 요청에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="11205-117">Support for unvalidated requests</span></span>](#_Toc318097381)
    - [<span data-ttu-id="11205-118">AntiXSS 라이브러리</span><span class="sxs-lookup"><span data-stu-id="11205-118">AntiXSS Library</span></span>](#_Toc318097382)
    - [<span data-ttu-id="11205-119">WebSockets 프로토콜에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="11205-119">Support for WebSockets Protocol</span></span>](#_Toc318097383)
    - [<span data-ttu-id="11205-120">묶음 및 축소</span><span class="sxs-lookup"><span data-stu-id="11205-120">Bundling and Minification</span></span>](#_Toc318097384)
    - [<span data-ttu-id="11205-121">웹 호스팅에 대 한 성능 향상</span><span class="sxs-lookup"><span data-stu-id="11205-121">Performance Improvements for Web Hosting</span></span>](#_Toc_perf)

        - [<span data-ttu-id="11205-122">핵심 성능 요소</span><span class="sxs-lookup"><span data-stu-id="11205-122">Key Performance Factors</span></span>](#_Toc_perf_1)
        - [<span data-ttu-id="11205-123">새로운 성능 기능에 대 한 요구 사항</span><span class="sxs-lookup"><span data-stu-id="11205-123">Requirements for New Performance Features</span></span>](#_Toc_perf_2)
        - [<span data-ttu-id="11205-124">공용 어셈블리를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-124">Sharing Common Assemblies</span></span>](#_Toc_perf_3)
        - [<span data-ttu-id="11205-125">빠른 시작에 대 한 다중 코어 JIT 컴파일을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="11205-125">Using multi-Core JIT compilation for faster startup</span></span>](#_Toc_perf_4)
        - [<span data-ttu-id="11205-126">메모리 최적화 하기 위해 가비지 수집 튜닝</span><span class="sxs-lookup"><span data-stu-id="11205-126">Tuning garbage collection to optimize for memory</span></span>](#_Toc_perf_5)
        - [<span data-ttu-id="11205-127">웹 응용 프로그램 프리페치</span><span class="sxs-lookup"><span data-stu-id="11205-127">Prefetching for web applications</span></span>](#_Toc_perf_6)
- [<span data-ttu-id="11205-128">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="11205-128">ASP.NET Web Forms</span></span>](#_Toc318097385)

    - [<span data-ttu-id="11205-129">강력한 형식의 데이터 컨트롤</span><span class="sxs-lookup"><span data-stu-id="11205-129">Strongly Typed Data Controls</span></span>](#_Toc318097386)
    - [<span data-ttu-id="11205-130">모델 바인딩</span><span class="sxs-lookup"><span data-stu-id="11205-130">Model Binding</span></span>](#_Toc318097387)

        - [<span data-ttu-id="11205-131">데이터 선택</span><span class="sxs-lookup"><span data-stu-id="11205-131">Selecting data</span></span>](#_Toc318097388)
        - [<span data-ttu-id="11205-132">값 공급자</span><span class="sxs-lookup"><span data-stu-id="11205-132">Value providers</span></span>](#_Toc318097389)
        - [<span data-ttu-id="11205-133">컨트롤에서 값으로 필터링</span><span class="sxs-lookup"><span data-stu-id="11205-133">Filtering by values from a control</span></span>](#_Toc318097390)
    - [<span data-ttu-id="11205-134">HTML 인코딩된 데이터 바인딩 식</span><span class="sxs-lookup"><span data-stu-id="11205-134">HTML Encoded Data-Binding Expressions</span></span>](#_Toc318097391)
    - [<span data-ttu-id="11205-135">비간섭 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="11205-135">Unobtrusive Validation</span></span>](#_Toc318097392)
    - [<span data-ttu-id="11205-136">HTML5 업데이트</span><span class="sxs-lookup"><span data-stu-id="11205-136">HTML5 Updates</span></span>](#_Toc318097393)
- [<span data-ttu-id="11205-137">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="11205-137">ASP.NET MVC 4</span></span>](#_Toc318097394)
- [<span data-ttu-id="11205-138">ASP.NET 웹 페이지 2</span><span class="sxs-lookup"><span data-stu-id="11205-138">ASP.NET Web Pages 2</span></span>](#_Toc318097395)
- [<span data-ttu-id="11205-139">Visual Studio 2012 Release Candidate</span><span class="sxs-lookup"><span data-stu-id="11205-139">Visual Studio 2012 Release Candidate</span></span>](#_Toc318097396)

    - [<span data-ttu-id="11205-140">Visual Studio 2010 및 Visual Studio 2012 Release Candidate (프로젝트 호환성) 간에 공유 프로젝트</span><span class="sxs-lookup"><span data-stu-id="11205-140">Project Sharing Between Visual Studio 2010 and Visual Studio 2012 Release Candidate (Project Compatibility)</span></span>](#project-compatibility)
    - [<span data-ttu-id="11205-141">ASP.NET 4.5 웹 사이트 템플릿의 구성 변경</span><span class="sxs-lookup"><span data-stu-id="11205-141">Configuration Changes in ASP.NET 4.5 Website Templates</span></span>](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [<span data-ttu-id="11205-142">ASP.NET 라우팅에 대 한 IIS 7에서에서 기본적으로 지원</span><span class="sxs-lookup"><span data-stu-id="11205-142">Native Support in IIS 7 for ASP.NET Routing</span></span>](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [<span data-ttu-id="11205-143">HTML 편집기</span><span class="sxs-lookup"><span data-stu-id="11205-143">HTML Editor</span></span>](#_Toc318097397)

        - [<span data-ttu-id="11205-144">스마트 작업</span><span class="sxs-lookup"><span data-stu-id="11205-144">Smart Tasks</span></span>](#_Toc318097398)
        - [<span data-ttu-id="11205-145">WAI ARIA 지원</span><span class="sxs-lookup"><span data-stu-id="11205-145">WAI-ARIA support</span></span>](#_Toc318097399)
        - [<span data-ttu-id="11205-146">새 HTML5 조각</span><span class="sxs-lookup"><span data-stu-id="11205-146">New HTML5 snippets</span></span>](#_Toc318097400)
        - [<span data-ttu-id="11205-147">사용자 정의 컨트롤로 추출</span><span class="sxs-lookup"><span data-stu-id="11205-147">Extract to user control</span></span>](#_Toc318097401)
        - [<span data-ttu-id="11205-148">코드 너 깃 특성에서에 대 한 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="11205-148">IntelliSense for code nuggets in attributes</span></span>](#_Toc318097402)
        - [<span data-ttu-id="11205-149">태그 또는 닫는 태그 이름을 바꾸는 경우 일치 하는 태그의 자동 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="11205-149">Automatic renaming of matching tag when you rename an opening or closing tag</span></span>](#_Toc318097403)
        - [<span data-ttu-id="11205-150">이벤트 처리기 생성</span><span class="sxs-lookup"><span data-stu-id="11205-150">Event handler generation</span></span>](#_Toc318097404)
        - [<span data-ttu-id="11205-151">스마트 들여쓰기</span><span class="sxs-lookup"><span data-stu-id="11205-151">Smart indent</span></span>](#_Toc318097405)
        - [<span data-ttu-id="11205-152">문 자동 줄임 완성</span><span class="sxs-lookup"><span data-stu-id="11205-152">Auto-reduce statement completion</span></span>](#_Toc318097406)
    - [<span data-ttu-id="11205-153">JavaScript 편집기</span><span class="sxs-lookup"><span data-stu-id="11205-153">JavaScript Editor</span></span>](#_Toc318097407)

        - [<span data-ttu-id="11205-154">코드 개요</span><span class="sxs-lookup"><span data-stu-id="11205-154">Code outlining</span></span>](#_Toc318097408)
        - [<span data-ttu-id="11205-155">중괄호 일치</span><span class="sxs-lookup"><span data-stu-id="11205-155">Brace matching</span></span>](#_Toc318097409)
        - [<span data-ttu-id="11205-156">정의로 이동</span><span class="sxs-lookup"><span data-stu-id="11205-156">Go to Definition</span></span>](#_Toc318097410)
        - [<span data-ttu-id="11205-157">ECMAScript5 지원</span><span class="sxs-lookup"><span data-stu-id="11205-157">ECMAScript5 support</span></span>](#_Toc318097411)
        - [<span data-ttu-id="11205-158">DOM IntelliSense</span><span class="sxs-lookup"><span data-stu-id="11205-158">DOM IntelliSense</span></span>](#_Toc318097412)
        - [<span data-ttu-id="11205-159">VSDOC 서명이 오버 로드</span><span class="sxs-lookup"><span data-stu-id="11205-159">VSDOC signature overloads</span></span>](#_Toc318097413)
        - [<span data-ttu-id="11205-160">암시적 참조</span><span class="sxs-lookup"><span data-stu-id="11205-160">Implicit references</span></span>](#_Toc318097414)
    - [<span data-ttu-id="11205-161">CSS 편집기</span><span class="sxs-lookup"><span data-stu-id="11205-161">CSS Editor</span></span>](#_Toc318097415)

        - [<span data-ttu-id="11205-162">문 자동 줄임 완성</span><span class="sxs-lookup"><span data-stu-id="11205-162">Auto-reduce statement completion</span></span>](#_Toc318097416)
        - [<span data-ttu-id="11205-163">계층적 들여쓰기입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-163">Hierarchical indentation.</span></span>](#_Toc318097417)
        - [<span data-ttu-id="11205-164">CSS 해킹 지원</span><span class="sxs-lookup"><span data-stu-id="11205-164">CSS hacks support</span></span>](#_Toc318097418)
        - [<span data-ttu-id="11205-165">공급 업체 특정 스키마 (-설정-,-webkit)</span><span class="sxs-lookup"><span data-stu-id="11205-165">Vendor specific schemas (-moz-,-webkit)</span></span>](#_Toc318097419)
        - [<span data-ttu-id="11205-166">주석 처리 및 주석 처리 제거 지원</span><span class="sxs-lookup"><span data-stu-id="11205-166">Commenting and uncommenting support</span></span>](#_Toc318097420)
        - [<span data-ttu-id="11205-167">색 선택</span><span class="sxs-lookup"><span data-stu-id="11205-167">Color picker</span></span>](#_Toc318097421)
        - [<span data-ttu-id="11205-168">조각</span><span class="sxs-lookup"><span data-stu-id="11205-168">Snippets</span></span>](#_Toc318097422)
        - [<span data-ttu-id="11205-169">사용자 지정 영역</span><span class="sxs-lookup"><span data-stu-id="11205-169">Custom regions</span></span>](#_Toc318097423)
    - [<span data-ttu-id="11205-170">페이지 검사기</span><span class="sxs-lookup"><span data-stu-id="11205-170">Page Inspector</span></span>](#_Toc318097424)
    - [<span data-ttu-id="11205-171">게시</span><span class="sxs-lookup"><span data-stu-id="11205-171">Publishing</span></span>](#_Toc318097425)

        - [<span data-ttu-id="11205-172">게시 프로필</span><span class="sxs-lookup"><span data-stu-id="11205-172">Publish profiles</span></span>](#_Toc318097426)
        - [<span data-ttu-id="11205-173">ASP.NET 미리 컴파일 및 병합</span><span class="sxs-lookup"><span data-stu-id="11205-173">ASP.NET precompilation and merge</span></span>](#_Toc318097427)
- [<span data-ttu-id="11205-174">IIS Express</span><span class="sxs-lookup"><span data-stu-id="11205-174">IIS Express</span></span>](#_Toc318097428)
- [<span data-ttu-id="11205-175">고 지 사항</span><span class="sxs-lookup"><span data-stu-id="11205-175">Disclaimer</span></span>](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a><span data-ttu-id="11205-176">ASP.NET Core 런타임 및 프레임 워크</span><span class="sxs-lookup"><span data-stu-id="11205-176">ASP.NET Core Runtime and Framework</span></span>

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a><span data-ttu-id="11205-177">비동기적으로 읽고 쓰는 HTTP 요청 및 응답</span><span class="sxs-lookup"><span data-stu-id="11205-177">Asynchronously Reading and Writing HTTP Requests and Responses</span></span>

<span data-ttu-id="11205-178">ASP.NET 4를 사용 하 여 스트림을 HTTP 요청 엔터티를 읽는 기능을 도입 합니다 *HttpRequest.GetBufferlessInputStream* 메서드.</span><span class="sxs-lookup"><span data-stu-id="11205-178">ASP.NET 4 introduced the ability to read an HTTP request entity as a stream using the *HttpRequest.GetBufferlessInputStream* method.</span></span> <span data-ttu-id="11205-179">이 메서드는 요청 엔터티에 대 한 스트리밍 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-179">This method provided streaming access to the request entity.</span></span> <span data-ttu-id="11205-180">그러나이 동기적으로 실행에서 스레드를 요청 기간에 대 한 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-180">However, it executed synchronously, which tied up a thread for the duration of a request.</span></span>

<span data-ttu-id="11205-181">ASP.NET 4.5는 HTTP 요청 엔터티를 비동기적으로 스트림을 읽을 수 및 비동기적으로 플러시할 수 있는 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-181">ASP.NET 4.5 supports the ability to read streams asynchronously on an HTTP request entity, and the ability to flush asynchronously.</span></span> <span data-ttu-id="11205-182">또한 ASP.NET 4.5는 이중 컨트롤러.aspx 페이지 처리기 및 ASP.NET MVC와 같은 다운스트림 HTTP 처리기를 사용 하 여 보다 쉽게 통합을 제공 하는 HTTP 요청 엔터티, 버퍼 수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-182">ASP.NET 4.5 also gives you the ability to double-buffer an HTTP request entity, which provides easier integration with downstream HTTP handlers such as .aspx page handlers and ASP.NET MVC controllers.</span></span>

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a><span data-ttu-id="11205-183">HttpRequest 처리의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="11205-183">Improvements to HttpRequest handling</span></span>

<span data-ttu-id="11205-184">ASP.NET 4.5에서 반환한 Stream 참조 *HttpRequest.GetBufferlessInputStream* 동기 및 비동기 읽기 메서드를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-184">The Stream reference returned by ASP.NET 4.5 from *HttpRequest.GetBufferlessInputStream* supports both synchronous and asynchronous read methods.</span></span> <span data-ttu-id="11205-185">합니다 *Stream* 에서 반환 된 개체 *GetBufferlessInputStream* 이제 BeginRead 및 EndRead 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-185">The *Stream* object returned from *GetBufferlessInputStream* now implements both the BeginRead and EndRead methods.</span></span> <span data-ttu-id="11205-186">비동기 *Stream* 메서드를 사용 하면 ASP.NET 비동기 읽기 루프의 각 반복 간에 현재 스레드를 해제 하는 동안 청크를 요청 엔터티를 비동기적으로 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-186">The asynchronous *Stream* methods let you asynchronously read the request entity in chunks, while ASP.NET releases the current thread between each iteration of an asynchronous read loop.</span></span>

<span data-ttu-id="11205-187">ASP.NET 4.5에도 버퍼링 방식으로 요청 엔터티를 읽는 데 필요한 도우미 메서드를 추가 합니다. *HttpRequest.GetBufferedInputStream*합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-187">ASP.NET 4.5 has also added a companion method for reading the request entity in a buffered way: *HttpRequest.GetBufferedInputStream*.</span></span> <span data-ttu-id="11205-188">이 새 오버 로드 생김 *GetBufferlessInputStream*, 동기 및 비동기 읽기를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-188">This new overload works like *GetBufferlessInputStream*, supporting both synchronous and asynchronous reads.</span></span> <span data-ttu-id="11205-189">단, 읽고, *GetBufferedInputStream* 다운스트림 모듈 및 처리기 요청 엔터티가 이용할 수 있도록 엔터티 바이트를 ASP.NET 내부 버퍼로 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-189">However, as it reads, *GetBufferedInputStream* also copies the entity bytes into ASP.NET internal buffers so that downstream modules and handlers can still access the request entity.</span></span> <span data-ttu-id="11205-190">예를 들어, 일부 업스트림 파이프라인의 코드가 이미 읽은 사용 하 여 요청 엔터티 *GetBufferedInputStream*를 계속 사용할 수 있습니다 *HttpRequest.Form* 또는 *HttpRequest.Files*.</span><span class="sxs-lookup"><span data-stu-id="11205-190">For example, if some upstream code in the pipeline has already read the request entity using *GetBufferedInputStream*, you can still use *HttpRequest.Form* or *HttpRequest.Files*.</span></span> <span data-ttu-id="11205-191">이렇게 하면 (예를 들어 데이터베이스에 큰 파일 업로드를 스트리밍), 요청에 비동기 처리를 수행 하지만 여전히 실행된.aspx 페이지 및 ASP.NET MVC 컨트롤러 나중에.</span><span class="sxs-lookup"><span data-stu-id="11205-191">This lets you perform asynchronous processing on a request (for example, streaming a large file upload to a database), but still run .aspx pages and MVC ASP.NET controllers afterward.</span></span>

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a><span data-ttu-id="11205-192">응답을 비동기적으로 플러시</span><span class="sxs-lookup"><span data-stu-id="11205-192">Asynchronously flushing a response</span></span>

<span data-ttu-id="11205-193">HTTP 클라이언트에 대 한 응답을 보내는 클라이언트 멀리 떨어져 또는 낮은 대역폭 연결이 면 상당한 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-193">Sending responses to an HTTP client can take considerable time when the client is far away or has a low-bandwidth connection.</span></span> <span data-ttu-id="11205-194">일반적으로 ASP.NET 응용 프로그램에서 만들어지는 경우 응답 바이트를 버퍼링 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-194">Normally ASP.NET buffers the response bytes as they are created by an application.</span></span> <span data-ttu-id="11205-195">ASP.NET 요청 처리의 끝에서 계산 된 버퍼의 단일 전송 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-195">ASP.NET then performs a single send operation of the accrued buffers at the very end of request processing.</span></span>

<span data-ttu-id="11205-196">주기적으로 호출 해야 합니다 (예: 클라이언트에 큰 파일 스트리밍) 버퍼링 된 응답에 크면 *HttpResponse.Flush* 버퍼링 된 출력을 클라이언트에 보내고 메모리 사용을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-196">If the buffered response is large (for example, streaming a large file to a client), you must periodically call *HttpResponse.Flush* to send buffered output to the client and keep memory usage under control.</span></span> <span data-ttu-id="11205-197">그러나 때문 *플러시* 반복적으로 호출 하는 동기 호출 *플러시* 여전히 실행 시간이 긴 요청 기간에 대 한 스레드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-197">However, because *Flush* is a synchronous call, iteratively calling *Flush* still consumes a thread for the duration of potentially long-running requests.</span></span>

<span data-ttu-id="11205-198">ASP.NET 4.5를 사용 하 여 비동기적으로 플러시합니다 수행에 대 한 지원을 추가 합니다 *BeginFlush* 및 *EndFlush* 메서드를 *HttpResponse* 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-198">ASP.NET 4.5 adds support for performing flushes asynchronously using the *BeginFlush* and *EndFlush* methods of the *HttpResponse* class.</span></span> <span data-ttu-id="11205-199">이러한 메서드를 사용 하 여 비동기 모듈과 증분 방식으로 운영 체제 스레드를 묶어 두지 않고서도 클라이언트에 데이터를 전송 하는 비동기 처리기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-199">Using these methods, you can create asynchronous modules and asynchronous handlers that incrementally send data to a client without tying up operating-system threads.</span></span> <span data-ttu-id="11205-200">사이 *BeginFlush* 하 고 *EndFlush* 호출 ASP.NET는 현재 스레드를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-200">In between *BeginFlush* and *EndFlush* calls, ASP.NET releases the current thread.</span></span> <span data-ttu-id="11205-201">이 실질적으로 장기 실행 HTTP 다운로드를 지원 하기 위해 필요한 활성 스레드의 총 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-201">This substantially reduces the total number of active threads that are needed in order to support long-running HTTP downloads.</span></span>

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a><span data-ttu-id="11205-202">에 대 한 지원 *await* 하 고 *태스크* -기반 비동기 모듈과 처리기</span><span class="sxs-lookup"><span data-stu-id="11205-202">Support for *await* and *Task* - Based Asynchronous Modules and Handlers</span></span>

<span data-ttu-id="11205-203">.NET Framework 4 라고 하는 비동기 프로그래밍 개념을 도입 된 *태스크*합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-203">The .NET Framework 4 introduced an asynchronous programming concept referred to as a *task*.</span></span> <span data-ttu-id="11205-204">작업으로 표시 됩니다는 *태스크* 형식과 관련 된 형식을 합니다 *System.Threading.Tasks* 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-204">Tasks are represented by the *Task* type and related types in the *System.Threading.Tasks* namespace.</span></span> <span data-ttu-id="11205-205">.NET Framework 4.5를 사용 하는 향상 된 컴파일러를 사용 하 여이 빌드 *태스크* 개체 단순 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-205">The .NET Framework 4.5 builds on this with compiler enhancements that make working with *Task* objects simple.</span></span> <span data-ttu-id="11205-206">.NET Framework 4.5에서 컴파일러는 두 개의 새 키워드를 지원 합니다. *await* 하 고 *비동기*합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-206">In the .NET Framework 4.5, the compilers support two new keywords: *await* and *async*.</span></span> <span data-ttu-id="11205-207">합니다 *await* 키워드는 코드 조각의 코드의 다른 부분에서 비동기적으로 대기 해야 하는 구문 축약형 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-207">The *await* keyword is syntactical shorthand for indicating that a piece of code should asynchronously wait on some other piece of code.</span></span> <span data-ttu-id="11205-208">합니다 *비동기* 키워드에는 작업 기반 비동기 메서드로 메서드를 표시 하는 데 사용할 수 있는 힌트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="11205-208">The *async* keyword represents a hint that you can use to mark methods as task-based asynchronous methods.</span></span>

<span data-ttu-id="11205-209">조합 *await*를 *비동기*, 및 *태스크* 개체를 사용 하면 훨씬 쉽게.NET 4.5에서 비동기 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-209">The combination of *await*, *async*, and the *Task* object makes it much easier for you to write asynchronous code in .NET 4.5.</span></span> <span data-ttu-id="11205-210">ASP.NET 4.5 비동기 HTTP 모듈 및 향상 된 새 컴파일러를 사용 하 여 비동기 HTTP 처리기를 작성할 수 있는 새로운 Api 사용 하 여 이러한 단순화를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-210">ASP.NET 4.5 supports these simplifications with new APIs that let you write asynchronous HTTP modules and asynchronous HTTP handlers using the new compiler enhancements.</span></span>

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a><span data-ttu-id="11205-211">비동기 HTTP 모듈</span><span class="sxs-lookup"><span data-stu-id="11205-211">Asynchronous HTTP modules</span></span>

<span data-ttu-id="11205-212">반환 하는 메서드 내에서 비동기 작업을 수행 하 려 한다고 가정 된 *태스크* 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-212">Suppose that you want to perform asynchronous work within a method that returns a *Task* object.</span></span> <span data-ttu-id="11205-213">다음 코드 예제에서는 Microsoft 홈 페이지를 다운로드 하는 비동기 호출 하는 비동기 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-213">The following code example defines an asynchronous method that makes an asynchronous call to download the Microsoft home page.</span></span> <span data-ttu-id="11205-214">사용 하 여 합니다 *비동기* 메서드 시그니처의 키워드 및 *await* 호출 *DownloadStringTaskAsync*합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-214">Notice the use of the *async* keyword in the method signature and the *await* call to *DownloadStringTaskAsync*.</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

<span data-ttu-id="11205-215">작성 해야 할 모든-.NET Framework 다운로드 작업이 완료 되 면 호출 스택 자동으로 복원할 수 있을 뿐만 아니라 다운로드를 완료를 대기 하는 동안 호출 스택 해제를 자동으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-215">That's all you have to write — the .NET Framework will automatically handle unwinding the call stack while waiting for the download to complete, as well as automatically restoring the call stack after the download is done.</span></span>

<span data-ttu-id="11205-216">이제 비동기 ASP.NET HTTP 모듈에이 비동기 메서드를 사용 하려면 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-216">Now suppose that you want to use this asynchronous method in an asynchronous ASP.NET HTTP module.</span></span> <span data-ttu-id="11205-217">ASP.NET 4.5에는 도우미 메서드가 포함 되어 있습니다. (*EventHandlerTaskAsyncHelper*) 및 새 대리자 형식을 (*TaskEventHandler*) 이전 비동기 메서드가 작업 기반 통합에 사용할 수 있는 비동기 프로그래밍 모델을 ASP.NET HTTP 파이프라인에 의해 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-217">ASP.NET 4.5 includes a helper method (*EventHandlerTaskAsyncHelper*) and a new delegate type (*TaskEventHandler*) that you can use to integrate task-based asynchronous methods with the older asynchronous programming model exposed by the ASP.NET HTTP pipeline.</span></span> <span data-ttu-id="11205-218">이 예제에서는 어떻게:</span><span class="sxs-lookup"><span data-stu-id="11205-218">This example shows how:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a><span data-ttu-id="11205-219">비동기 HTTP 처리기</span><span class="sxs-lookup"><span data-stu-id="11205-219">Asynchronous HTTP handlers</span></span>

<span data-ttu-id="11205-220">ASP.NET에서 비동기 처리기를 작성 하는 일반적인 방법을 구현 하는 것은 *IHttpAsyncHandler* 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-220">The traditional approach to writing asynchronous handlers in ASP.NET is to implement the *IHttpAsyncHandler* interface.</span></span> <span data-ttu-id="11205-221">ASP.NET 4.5에서 도입 된 *HttpTaskAsyncHandler* 비동기 기본 형식에서 파생 시킬 수 있는 훨씬 쉽게 비동기 처리기를 작성 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-221">ASP.NET 4.5 introduces the *HttpTaskAsyncHandler* asynchronous base type that you can derive from, which makes it much easier to write asynchronous handlers.</span></span>

<span data-ttu-id="11205-222">합니다 *HttpTaskAsyncHandler* 형식은 추상 이며 재정의 해야 합니다 *ProcessRequestAsync* 메서드.</span><span class="sxs-lookup"><span data-stu-id="11205-222">The *HttpTaskAsyncHandler* type is abstract and requires you to override the *ProcessRequestAsync* method.</span></span> <span data-ttu-id="11205-223">ASP.NET 반환 시그니처를 통합 하는 내부적으로 알아서 (을 *태스크* 개체)의 *ProcessRequestAsync* ASP.NET 파이프라인에 의해 사용 되는 이전 비동기 프로그래밍 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-223">Internally ASP.NET takes care of integrating the return signature (a *Task* object) of *ProcessRequestAsync* with the older asynchronous programming model used by the ASP.NET pipeline.</span></span>

<span data-ttu-id="11205-224">다음 예제에서는 사용 하는 방법을 보여 줍니다 *태스크* 하 고 *await* 비동기 HTTP 처리기 구현의 일부로:</span><span class="sxs-lookup"><span data-stu-id="11205-224">The following example shows how you can use *Task* and *await* as part of the implementation of an asynchronous HTTP handler:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a><span data-ttu-id="11205-225">새 ASP.NET 요청 유효성 검사 기능</span><span class="sxs-lookup"><span data-stu-id="11205-225">New ASP.NET Request Validation Features</span></span>

<span data-ttu-id="11205-226">기본적으로 ASP.NET 요청 유효성 검사를 수행-태그 또는 필드, 헤더, 쿠키 및 등의 스크립트를 검색 하는 요청을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-226">By default, ASP.NET performs request validation — it examines requests to look for markup or script in fields, headers, cookies, and so on.</span></span> <span data-ttu-id="11205-227">모든 검색 되 면 ASP.NET 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-227">If any is detected, ASP.NET throws an exception.</span></span> <span data-ttu-id="11205-228">이 잠재적인 교차 사이트 스크립팅 공격에 대 한 첫 번째 방어선으로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-228">This acts as a first line of defense against potential cross-site scripting attacks.</span></span>

<span data-ttu-id="11205-229">ASP.NET 4.5 쉽게 선택적으로 유효성이 검사 되지 않은 요청 데이터를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-229">ASP.NET 4.5 makes it easy to selectively read unvalidated request data.</span></span> <span data-ttu-id="11205-230">ASP.NET 4.5에는 외부 라이브러리 이었음 널리 사용 되 AntiXSS 라이브러리에 통합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-230">ASP.NET 4.5 also integrates the popular AntiXSS library, which was formerly an external library.</span></span>

<span data-ttu-id="11205-231">개발자가 자주 응용 프로그램에 대 한 요청 유효성 검사를 선택적으로 해제 하는 기능에 대 한 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-231">Developers have frequently asked for the ability to selectively turn off request validation for their applications.</span></span> <span data-ttu-id="11205-232">예를 들어 포럼 소프트웨어 응용 프로그램을 사용 하는 경우 사용자가 HTML 형식의 포럼 게시물과 의견을 제출 하지만 나머지 요청 유효성 검사는 하는지 여부를 확인 하도록 허용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-232">For example, if your application is forum software, you might want to allow users to submit HTML-formatted forum posts and comments, but still make sure that request validation is checking everything else.</span></span>

<span data-ttu-id="11205-233">ASP.NET 4.5에 쉽게 유효성이 검사 되지 않은 입력을 선택 하 여 작업할 수 있도록 하는 두 가지 기능을 소개 합니다. ("지연") 요청 유효성 검사 및 유효성이 검사 되지 않은 요청 데이터에 대 한 액세스를 지연 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-233">ASP.NET 4.5 introduces two features that make it easy for you to selectively work with unvalidated input: deferred ("lazy") request validation and access to unvalidated request data.</span></span>

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a><span data-ttu-id="11205-234">("지연") 요청 유효성 검사를 지연합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-234">Deferred ("lazy") request validation</span></span>

<span data-ttu-id="11205-235">ASP.NET 4.5에서 기본적으로 모든 요청 데이터는 요청 유효성 검사 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-235">In ASP.NET 4.5, by default all request data is subject to request validation.</span></span> <span data-ttu-id="11205-236">그러나 요청 데이터를 실제로 액세스 될 때까지 요청 유효성 검사를 연기 하는 응용 프로그램을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-236">However, you can configure the application to defer request validation until you actually access request data.</span></span> <span data-ttu-id="11205-237">(이 경우에 따라 라고 지연 요청 유효성 검사를 특정 데이터 시나리오에 대 한 지연 로드와 같은 용어를 기반으로 합니다.) Web.config 파일에서 지연 된 유효성 검사를 사용 하 여 설정 하 여 응용 프로그램을 구성할 수 있습니다 합니다 *requestValidationMode* 에서 4.5로 특성을 *httpRUntime* 다음 예제와 같이 요소:</span><span class="sxs-lookup"><span data-stu-id="11205-237">(This is sometimes referred to as lazy request validation, based on terms like lazy loading for certain data scenarios.) You can configure the application to use deferred validation in the Web.config file by setting the *requestValidationMode* attribute to 4.5 in the *httpRUntime* element, as in the following example:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

<span data-ttu-id="11205-238">요청 유효성 검사 모드를 4.5로 설정 되 면 요청 유효성 검사는 특정 요청 값에 대해서만 하 고 코드에 해당 값에 액세스 하는 경우에 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-238">When request validation mode is set to 4.5, request validation is triggered only for a specific request value and only when your code accesses that value.</span></span> <span data-ttu-id="11205-239">예를 들어 코드 Request.Form["forum의 값을 가져옵니다\_게시"], 폼 컬렉션의 해당 요소에만 요청 유효성 검사를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-239">For example, if your code gets the value of Request.Form["forum\_post"], request validation is invoked only for that element in the form collection.</span></span> <span data-ttu-id="11205-240">다른 요소가 하나도 합니다 *폼* 컬렉션 유효성이 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-240">None of the other elements in the *Form* collection are validated.</span></span> <span data-ttu-id="11205-241">이전 버전의 ASP.NET에서는 요청 유효성 검사는 컬렉션의 모든 요소를 액세스 하는 경우 전체 요청 컬렉션에 대 한 트리거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-241">In previous versions of ASP.NET, request validation was triggered for the entire request collection when any element in the collection was accessed.</span></span> <span data-ttu-id="11205-242">새 동작을 쉽게 다른 응용 프로그램 구성 요소의 다른 부분에서 요청 유효성 검사를 트리거하지 않고 요청 데이터의 다른 부분을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-242">The new behavior makes it easier for different application components to look at different pieces of request data without triggering request validation on other pieces.</span></span>

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a><span data-ttu-id="11205-243">유효성이 검사 되지 않은 요청에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="11205-243">Support for unvalidated requests</span></span>

<span data-ttu-id="11205-244">지연 된 요청 유효성 검사를 단독으로 선택적으로 요청 유효성 검사를 무시 하 고 문제를 해결 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-244">Deferred request validation alone doesn't solve the problem of selectively bypassing request validation.</span></span> <span data-ttu-id="11205-245">Request.Form["forum 호출\_게시"] 트리거는 특정 요청 값에 대 한 유효성 검사를 요청 하는 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-245">The call to Request.Form["forum\_post"] still triggers request validation for that specific request value.</span></span> <span data-ttu-id="11205-246">그러나 다음 해당 필드의 태그를 허용 하기 때문에 유효성 검사를 트리거하지 않고이 필드에 액세스 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-246">However, you might want to access this field without triggering validation because you want to allow markup in that field.</span></span>

<span data-ttu-id="11205-247">이 위해 ASP.NET 4.5 이제 요청 데이터에 대 한 유효성이 검사 되지 않은 액세스를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-247">To allow this, ASP.NET 4.5 now supports unvalidated access to request data.</span></span> <span data-ttu-id="11205-248">새 ASP.NET 4.5에 포함 되어 *Unvalidated* 에서 컬렉션 속성을 *HttpRequest* 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-248">ASP.NET 4.5 includes a new *Unvalidated* collection property in the *HttpRequest* class.</span></span> <span data-ttu-id="11205-249">이 컬렉션의 모든 요청 데이터의 일반적인 값에 대 한 액세스를 같은 제공 *폼*를 *QueryString*에 *쿠키*, 및 *Url*합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-249">This collection provides access to all of the common values of request data, like *Form*, *QueryString*, *Cookies*, and *Url*.</span></span>

<span data-ttu-id="11205-250">포럼 예제를 사용 하 여 유효성이 검사 되지 않은 요청 데이터를 읽을 수 있으려면, 먼저 해야 새 요청 유효성 검사 모드를 사용 하도록 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-250">Using the forum example, to be able to read unvalidated request data, you first need to configure the application to use the new request validation mode:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

<span data-ttu-id="11205-251">사용할 수는 *HttpRequest.Unvalidated* 유효성이 검사 되지 않은 폼 값을 읽을 수 있는 속성:</span><span class="sxs-lookup"><span data-stu-id="11205-251">You can then use the *HttpRequest.Unvalidated* property to read the unvalidated form value:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]


> [!WARNING]
> <span data-ttu-id="11205-252">보안- *유효성이 검사 되지 않은 요청 데이터를 사용 하 여 신중 하 게!*</span><span class="sxs-lookup"><span data-stu-id="11205-252">Security - *Use unvalidated request data with care!*</span></span> <span data-ttu-id="11205-253">ASP.NET 4.5 유효성이 검사 되지 않은 요청 속성과 매우 구체적인 유효성이 검사 되지 않은 요청 데이터를 액세스 하기 위한 쉽게 수행할 수 있도록 컬렉션에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-253">ASP.NET 4.5 added the unvalidated request properties and collections to make it easier for you to access very specific unvalidated request data.</span></span> <span data-ttu-id="11205-254">그러나 여전히 사용자 지정 유효성 검사에서는 원시 요청 데이터를 사용자에 게 위험한 텍스트 렌더링 되지 않습니다에서 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-254">However, you must still perform custom validation on the raw request data to ensure that dangerous text is not rendered to users.</span></span>


<a id="_Toc318097382"></a>
### <a name="antixss-library"></a><span data-ttu-id="11205-255">AntiXSS 라이브러리</span><span class="sxs-lookup"><span data-stu-id="11205-255">AntiXSS Library</span></span>

<span data-ttu-id="11205-256">ASP.NET 4.5에는 Microsoft AntiXSS 라이브러리의 인기도,으로 인해 해당 라이브러리의 4.0 버전에서 주요 인코딩 루틴은 이제 통합 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-256">Due to the popularity of the Microsoft AntiXSS Library, ASP.NET 4.5 now incorporates core encoding routines from version 4.0 of that library.</span></span>

<span data-ttu-id="11205-257">인코딩 루틴에서 구현 되는 *AntiXssEncoder* 새 형식 *System.Web.Security.AntiXss* 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-257">The encoding routines are implemented by the *AntiXssEncoder* type in the new *System.Web.Security.AntiXss* namespace.</span></span> <span data-ttu-id="11205-258">사용할 수는 *AntiXssEncoder* 형식에서 구현 되는 인코딩 정적 메서드 중 하나를 호출 하 여 직접 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-258">You can use the *AntiXssEncoder* type directly by calling any of the static encoding methods that are implemented in the type.</span></span> <span data-ttu-id="11205-259">그러나 새 ANTI-XSS 루틴을 사용 하는 가장 쉬운 방법은 ASP.NET 응용 프로그램을 구성 하는 *AntiXssEncoder* 기본적으로 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-259">However, the easiest approach for using the new anti-XSS routines is to configure an ASP.NET application to use the *AntiXssEncoder* class by default.</span></span> <span data-ttu-id="11205-260">이 위해 Web.config 파일에 다음 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-260">To do this, add the following attribute to the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

<span data-ttu-id="11205-261">경우는 *encoderType* 특성 사용 하도록 설정 되어 합니다 *AntiXssEncoder* 새 인코딩 루틴을 사용 하 여 ASP.NET에서 자동으로 인코딩 출력 형식에 모든.</span><span class="sxs-lookup"><span data-stu-id="11205-261">When the *encoderType* attribute is set to use the *AntiXssEncoder* type, all output encoding in ASP.NET automatically uses the new encoding routines.</span></span>

<span data-ttu-id="11205-262">ASP.NET 4.5에 통합 되어 있는 외부 AntiXSS 라이브러리의 일부는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-262">These are the portions of the external AntiXSS library that have been incorporated into ASP.NET 4.5:</span></span>

- <span data-ttu-id="11205-263">*HtmlEncode*하십시오 *HtmlFormUrlEncode*, 및 *HtmlAttributeEncode*</span><span class="sxs-lookup"><span data-stu-id="11205-263">*HtmlEncode*, *HtmlFormUrlEncode*, and *HtmlAttributeEncode*</span></span>
- <span data-ttu-id="11205-264">*XmlAttributeEncode* 고 *XmlEncode*</span><span class="sxs-lookup"><span data-stu-id="11205-264">*XmlAttributeEncode* and *XmlEncode*</span></span>
- <span data-ttu-id="11205-265">*UrlEncode* 하 고 *UrlPathEncode* (신규)</span><span class="sxs-lookup"><span data-stu-id="11205-265">*UrlEncode* and *UrlPathEncode* (new)</span></span>
- <span data-ttu-id="11205-266">*CssEncode*</span><span class="sxs-lookup"><span data-stu-id="11205-266">*CssEncode*</span></span>

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a><span data-ttu-id="11205-267">WebSockets 프로토콜에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="11205-267">Support for WebSockets Protocol</span></span>

<span data-ttu-id="11205-268">Websocket 프로토콜은 HTTP를 통해 클라이언트와 서버 간의 안전 하 고 실시간 양방향 통신을 설정 하는 방법을 정의 하는 표준 기반 네트워크 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-268">WebSockets protocol is a standards-based network protocol that defines how to establish secure, real-time bidirectional communications between a client and a server over HTTP.</span></span> <span data-ttu-id="11205-269">Microsoft는 IETF 및 W3C 표준 본문의 프로토콜을 정의 하는 데 사용 하 여 작업 했습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-269">Microsoft has worked with both the IETF and W3C standards bodies to help define the protocol.</span></span> <span data-ttu-id="11205-270">Websocket 프로토콜은 클라이언트와 모바일 운영 체제 모두에서 Websocket 프로토콜을 지 원하는 많은 리소스를 투자 하는 Microsoft를 사용 하 여 모든 클라이언트 (뿐 아니라 브라우저)에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-270">The WebSockets protocol is supported by any client (not just browsers), with Microsoft investing substantial resources supporting WebSockets protocol on both client and mobile operating systems.</span></span>

<span data-ttu-id="11205-271">Websocket 프로토콜을 사용 하면 훨씬 쉽게 클라이언트와 서버 간에 장기 실행 데이터 전송을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-271">WebSockets protocol makes it much easier to create long-running data transfers between a client and a server.</span></span> <span data-ttu-id="11205-272">예를 들어, 채팅 응용 프로그램을 작성 되므로 훨씬 더 쉽게 클라이언트와 서버 간에 true 실행 시간이 긴 연결을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-272">For example, writing a chat application is much easier because you can establish a true long-running connection between a client and a server.</span></span> <span data-ttu-id="11205-273">예: 정기 폴링을 또는 HTTP 긴 폴링을 소켓의 동작을 시뮬레이션 하는 대안에 의존 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-273">You do not have to resort to workarounds like periodic polling or HTTP long-polling to simulate the behavior of a socket.</span></span>

<span data-ttu-id="11205-274">ASP.NET 4.5 및 IIS 8 하위 수준 Websocket 지원에 비동기적으로 읽고 Websocket 개체의 문자열 및 이진 데이터를 쓰기 위한 관리 되는 Api를 사용 하는 ASP.NET 개발자가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-274">ASP.NET 4.5 and IIS 8 include low-level WebSockets support, enabling ASP.NET developers to use managed APIs for asynchronously reading and writing both string and binary data on a WebSockets object.</span></span> <span data-ttu-id="11205-275">ASP.NET 4.5에 대해 새로운 *System.Web.WebSockets* Websocket 프로토콜을 사용 하 여 작업 하기 위한 형식을 포함 하는 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-275">For ASP.NET 4.5, there is a new *System.Web.WebSockets* namespace that contains types for working with WebSockets protocol.</span></span>

<span data-ttu-id="11205-276">DOM을 만들어 Websocket 연결을 설정 하는 브라우저 클라이언트가 *WebSocket* 다음 예제와 같이 ASP.NET 응용 프로그램에 URL을 가리키는 개체:</span><span class="sxs-lookup"><span data-stu-id="11205-276">A browser client establishes a WebSockets connection by creating a DOM *WebSocket* object that points to a URL in an ASP.NET application, as in the following example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

<span data-ttu-id="11205-277">모든 종류의 모듈 또는 처리기를 사용 하 여 ASP.NET에서 Websocket 끝점을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-277">You can create WebSockets endpoints in ASP.NET using any kind of module or handler.</span></span> <span data-ttu-id="11205-278">앞의 예에서.ashx 파일 처리기를 만들 수는 신속 하 게 되므로.ashx 파일 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-278">In the previous example, an .ashx file was used, because .ashx files are a quick way to create a handler.</span></span>

<span data-ttu-id="11205-279">WebSockets 프로토콜에 따라 ASP.NET 응용 프로그램 요청을 Websocket 요청에 HTTP GET 요청 으로부터 업그레이드 해야 한다는 것을 지정 하 여 클라이언트의 Websocket 요청을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-279">According to the WebSockets protocol, an ASP.NET application accepts a client's WebSockets request by indicating that the request should be upgraded from an HTTP GET request to a WebSockets request.</span></span> <span data-ttu-id="11205-280">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-280">Here's an example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

<span data-ttu-id="11205-281">합니다 *AcceptWebSocketRequest* ASP.NET 현재 HTTP 요청을 해제 하 고 다음 제어 함수 대리자를 전달 하기 때문에 메서드는 함수 대리자를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-281">The *AcceptWebSocketRequest* method accepts a function delegate because ASP.NET unwinds the current HTTP request and then transfers control to the function delegate.</span></span> <span data-ttu-id="11205-282">개념적으로이 방법은 사용 하는 방법과 유사한 *System.Threading.Thread*, 작업 수행 되는 백그라운드 스레드가 시작 대리자를 정의 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-282">Conceptually this approach is similar to how you use *System.Threading.Thread*, where you define a thread-start delegate in which background work is performed.</span></span>

<span data-ttu-id="11205-283">ASP.NET 및 클라이언트 Websocket 핸드셰이크를 성공적으로 완료, 대리자를 호출 하는 ASP.NET 후 Websocket 응용 프로그램 실행을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-283">After ASP.NET and the client have successfully completed a WebSockets handshake, ASP.NET calls your delegate and the WebSockets application starts running.</span></span> <span data-ttu-id="11205-284">다음 코드 예제에서는 ASP.NET에서 기본 제공 Websocket 지원을 사용 하는 간단한 에코 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="11205-284">The following code example shows a simple echo application that uses the built-in WebSockets support in ASP.NET:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

<span data-ttu-id="11205-285">.NET 4.5에 대 한 지원 합니다 *await* 키워드 및 작업 기반 비동기 작업은 자연스럽 게 WebSockets 응용 프로그램을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-285">The support in .NET 4.5 for the *await* keyword and asynchronous task-based operations is a natural fit for writing WebSockets applications.</span></span> <span data-ttu-id="11205-286">코드 예제에서는 ASP.NET 내부에서 Websocket 요청을 완전히 비동기적으로 실행 되는지 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="11205-286">The code example shows that a WebSockets request runs completely asynchronously inside ASP.NET.</span></span> <span data-ttu-id="11205-287">응용 프로그램 호출 하 여 클라이언트에서 보내는 메시지를 비동기적으로 기다립니다. *소켓을 기다립니다. ReceiveAsync*합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-287">The application waits asynchronously for a message to be sent from a client by calling *await socket.ReceiveAsync*.</span></span> <span data-ttu-id="11205-288">호출 하 여 클라이언트에 비동기 메시지를 보낼 수는 마찬가지로 *소켓을 기다립니다. SendAsync*합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-288">Similarly, you can send an asynchronous message to a client by calling *await socket.SendAsync*.</span></span>

<span data-ttu-id="11205-289">브라우저에서 응용 프로그램을 통해 Websocket 메시지를 수신 된 *onmessage* 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-289">In the browser, an application receives WebSockets messages through an *onmessage* function.</span></span> <span data-ttu-id="11205-290">호출 브라우저에서 메시지를 보내려고 합니다 *보낼* 메서드를 *WebSocket* 이 예제와 같이 DOM 유형으로:</span><span class="sxs-lookup"><span data-stu-id="11205-290">To send a message from a browser, you call the *send* method of the *WebSocket* DOM type, as shown in this example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

<span data-ttu-id="11205-291">나중에이 추상 떨어진 일부는 낮은 수준의 코딩에 필요한이 기능을이 릴리스에서 Websocket에 대 한 응용 프로그램에 대 한 업데이트 출시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-291">In the future, we might release updates to this functionality that abstract away some of the low-level coding that is required in this release for WebSockets applications.</span></span>

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a><span data-ttu-id="11205-292">묶음 및 축소</span><span class="sxs-lookup"><span data-stu-id="11205-292">Bundling and Minification</span></span>

<span data-ttu-id="11205-293">묶음 개별 JavaScript 및 CSS 파일을 단일 파일과 마찬가지로 취급 될 수 있는 번들 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-293">Bundling lets you combine individual JavaScript and CSS files into a bundle that can be treated like a single file.</span></span> <span data-ttu-id="11205-294">축소는 필요 하지 않은 다른 문자와 공백을 제거 하 여 JavaScript 및 CSS 파일을 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-294">Minification condenses JavaScript and CSS files by removing whitespace and other characters that are not required.</span></span> <span data-ttu-id="11205-295">이러한 기능은 Web Forms, ASP.NET MVC 및 웹 페이지를 사용 하 여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-295">These features work with Web Forms, ASP.NET MVC, and Web Pages.</span></span>

<span data-ttu-id="11205-296">번들은 번들 클래스 또는 해당 자식 클래스, ScriptBundle, StyleBundle 중 하나를 사용 하 여 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-296">Bundles are created using the Bundle class or one of its child classes, ScriptBundle and StyleBundle.</span></span> <span data-ttu-id="11205-297">번들의 인스턴스를 구성한 후 전역 BundleCollection 인스턴스를 추가 하기만 하면 번들 들어오는 요청에 사용할 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-297">After configuring an instance of a bundle, the bundle is made available to incoming requests by simply adding it to a global BundleCollection instance.</span></span> <span data-ttu-id="11205-298">기본 템플릿은 번들 구성 BundleConfig 파일에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-298">In the default templates, bundle configuration is performed in a BundleConfig file.</span></span> <span data-ttu-id="11205-299">이 기본 구성은 모든 핵심 스크립트 및 템플릿을 사용 하는 css 파일에 대 한 번들을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11205-299">This default configuration creates bundles for all of the core scripts and css files used by the templates.</span></span>

<span data-ttu-id="11205-300">번들은 몇 가지 가능한 도우미 메서드 중 하나를 사용 하 여 뷰 내에서 참조 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-300">Bundles are referenced from within views by using one of a couple possible helper methods.</span></span> <span data-ttu-id="11205-301">디버그와 릴리스 모드에서에서 번들에 대 한 다른 태그를 렌더링을 지원 하기 위해 ScriptBundle 및 StyleBundle 클래스에는 도우미 메서드를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-301">In order to support rendering different markup for a bundle when in debug vs. release mode, the ScriptBundle and StyleBundle classes have the helper method, Render.</span></span> <span data-ttu-id="11205-302">디버그 모드에 있을 때 렌더링은 번들의 각 리소스에 대 한 태그를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-302">When in debug mode, Render will generate markup for each resource in the bundle.</span></span> <span data-ttu-id="11205-303">릴리스 모드에 있을 때 렌더링 전체 번들에 대 한 단일 태그 요소를 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-303">When in release mode, Render will generate a single markup element for the entire bundle.</span></span> <span data-ttu-id="11205-304">설정/해제 디버그와 릴리스 간에 모드 아래와 같이 web.config에 있는 컴파일 요소의 debug 특성을 수정 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-304">Toggling between debug and release mode can be accomplished by modifying the debug attribute of the compilation element in web.config as shown below:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

<span data-ttu-id="11205-305">또한 활성화 또는 비활성화 최적화 BundleTable.EnableOptimizations 속성을 통해 직접 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-305">Additionally, enabling or disabling optimization can be set directly via the BundleTable.EnableOptimizations property.</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

<span data-ttu-id="11205-306">파일을 번들로 제공 되는 경우 먼저 알파벳 순서로 (에 표시 되는 방식을 **솔루션 탐색기**).</span><span class="sxs-lookup"><span data-stu-id="11205-306">When files are bundled, they are first sorted alphabetically (the way they are displayed in **Solution Explorer**).</span></span> <span data-ttu-id="11205-307">라이브러리를 알 수 있도록 다음 구성 및 사용자 지정 확장 (예: jQuery, MooTools, Dojo) 가장 먼저 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-307">They are then organized so that known libraries and their custom extensions (such as jQuery, MooTools, and Dojo) are loaded first.</span></span> <span data-ttu-id="11205-308">예를 들어 위에 표시 된 대로 스크립트 폴더의 번들에 대 한 최종 순서가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-308">For example, the final order for the bundling of the Scripts folder as shown above will be:</span></span>

1. <span data-ttu-id="11205-309">jquery-1.6.2.js</span><span class="sxs-lookup"><span data-stu-id="11205-309">jquery-1.6.2.js</span></span>
2. <span data-ttu-id="11205-310">jquery-ui.js</span><span class="sxs-lookup"><span data-stu-id="11205-310">jquery-ui.js</span></span>
3. <span data-ttu-id="11205-311">jquery.tools.js</span><span class="sxs-lookup"><span data-stu-id="11205-311">jquery.tools.js</span></span>
4. <span data-ttu-id="11205-312">a.js</span><span class="sxs-lookup"><span data-stu-id="11205-312">a.js</span></span>

<span data-ttu-id="11205-313">CSS 파일 또한 사전순으로 정렬 되며 그런 다음 다른 파일을 앞으로 reset.css 및 normalize.css 되도록 다시 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-313">CSS files are also sorted alphabetically and then reorganized so that reset.css and normalize.css come before any other file.</span></span> <span data-ttu-id="11205-314">위에 표시 된 Styles 폴더의 번들의 최종 정렬이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-314">The final sorting of the bundling of the Styles folder shown above will be this:</span></span>

1. <span data-ttu-id="11205-315">reset.css</span><span class="sxs-lookup"><span data-stu-id="11205-315">reset.css</span></span>
2. <span data-ttu-id="11205-316">content.css</span><span class="sxs-lookup"><span data-stu-id="11205-316">content.css</span></span>
3. <span data-ttu-id="11205-317">forms.css</span><span class="sxs-lookup"><span data-stu-id="11205-317">forms.css</span></span>
4. <span data-ttu-id="11205-318">globals.css</span><span class="sxs-lookup"><span data-stu-id="11205-318">globals.css</span></span>
5. <span data-ttu-id="11205-319">menu.css</span><span class="sxs-lookup"><span data-stu-id="11205-319">menu.css</span></span>
6. <span data-ttu-id="11205-320">styles.css</span><span class="sxs-lookup"><span data-stu-id="11205-320">styles.css</span></span>

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a><span data-ttu-id="11205-321">웹 호스팅에 대 한 성능 향상</span><span class="sxs-lookup"><span data-stu-id="11205-321">Performance Improvements for Web Hosting</span></span>

<span data-ttu-id="11205-322">.NET Framework 4.5 및 Windows 8 웹 서버 워크 로드에 대 한 상당한 성능 향상을 달성 하는 데 도움이 되는 기능을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-322">The .NET Framework 4.5 and Windows 8 introduce features that can help you achieve a significant performance boost for web-server workloads.</span></span> <span data-ttu-id="11205-323">여기에 감소 (최대 35%) 모두 시작 시간 및 ASP.NET을 사용 하는 사이트를 호스트 하는 웹의 메모리 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-323">This includes a reduction (up to 35%) in both startup time and in the memory footprint of web hosting sites that use ASP.NET.</span></span>

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a><span data-ttu-id="11205-324">핵심 성능 요소</span><span class="sxs-lookup"><span data-stu-id="11205-324">Key performance factors</span></span>

<span data-ttu-id="11205-325">이상적으로 모든 웹 사이트 해야 활성 상태 이며 다음 요청에 대 한 빠른 응답을 수행 하기 위해 메모리에 때마다 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-325">Ideally, all websites should be active and in memory to assure quick response to the next request, whenever it comes.</span></span> <span data-ttu-id="11205-326">사이트 응답성에 영향을 줄 수 있는 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-326">Factors that can affect site responsiveness include:</span></span>

- <span data-ttu-id="11205-327">사이트는 응용 프로그램 풀 재활용 후에 다시 시작 하는 데 걸리는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-327">The time it takes for a site to restart after an app pool recycles.</span></span> <span data-ttu-id="11205-328">사이트 어셈블리를 메모리에 더 이상 때 사이트에 대 한 웹 서버 프로세스를 시작 하는 데 걸리는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-328">This is the time it takes to launch a web server process for the site when the site assemblies are no longer in memory.</span></span> <span data-ttu-id="11205-329">(플랫폼 어셈블리는 아직 메모리에 다른 사이트에서 사용 하기 때문입니다.) 이 경우는 "콜드 사이트, 웜 framework 시작" 이라고 또는 방금 "콜드 사이트를 시작 합니다."</span><span class="sxs-lookup"><span data-stu-id="11205-329">(The platform assemblies are still in memory, since they are used by other sites.) This situation is referred to as "cold site, warm framework startup" or just "cold site startup."</span></span>
- <span data-ttu-id="11205-330">메모리의 양을 사이트를 차지합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-330">How much memory the site occupies.</span></span> <span data-ttu-id="11205-331">이 용어는 "사이트당 메모리 소비" 또는 "작업 집합을 공유 해제 합니다."</span><span class="sxs-lookup"><span data-stu-id="11205-331">Terms for this are "per-site memory consumption" or "unshared working set."</span></span>

<span data-ttu-id="11205-332">새 성능 향상 두이 요소가 모두에 집중합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-332">The new performance improvements focus on both of these factors.</span></span>

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a><span data-ttu-id="11205-333">새로운 성능 기능에 대 한 요구 사항</span><span class="sxs-lookup"><span data-stu-id="11205-333">Requirements for New Performance Features</span></span>

<span data-ttu-id="11205-334">새로운 기능에 대 한 요구 사항은 다음 범주로 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-334">The requirements for the new features can be broken down into these categories:</span></span>

- <span data-ttu-id="11205-335">.NET Framework 4에서 실행 되는 개선 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-335">Improvements that run on the .NET Framework 4.</span></span>
- <span data-ttu-id="11205-336">.NET Framework 4.5를 필요로 하지만 모든 버전의 Windows에서 실행할 수 있는 향상 된 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-336">Improvements that require the .NET Framework 4.5 but can run on any version of Windows.</span></span>
- <span data-ttu-id="11205-337">Windows 8을 실행 하는.NET Framework 4.5와 함께만 사용할 수 있는 향상 된 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-337">Improvements that are available only with .NET Framework 4.5 running on Windows 8.</span></span>

<span data-ttu-id="11205-338">각 수준을 사용 하도록 설정할 수 있는 향상 된 기능을 사용 하 여 성능이 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-338">Performance increases with each level of improvement that you are able to enable.</span></span>

<span data-ttu-id="11205-339">다른 시나리오에 적용 되는 광범위 한 성능 기능 활용 향상 된.NET Framework 4.5 기능 중 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-339">Some of the .NET Framework 4.5 improvements take advantage of broader performance features that apply to other scenarios as well.</span></span>

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a><span data-ttu-id="11205-340">공용 어셈블리를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-340">Sharing Common Assemblies</span></span>

<span data-ttu-id="11205-341">**요구 사항**:.NET Framework 4 및 Visual Studio 11 Developer Preview SDK</span><span class="sxs-lookup"><span data-stu-id="11205-341">**Requirement**: .NET Framework 4 and Visual Studio 11 Developer Preview SDK</span></span>

<span data-ttu-id="11205-342">서버에서 다른 사이트에는 종종 동일한 도우미 어셈블리 (예: 시작 키트 또는 샘플 응용 프로그램에서 어셈블리)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-342">Different sites on a server often use the same helper assemblies (for example, assemblies from a starter kit or sample application).</span></span> <span data-ttu-id="11205-343">각 사이트에 해당 Bin 디렉터리에서 이러한 어셈블리의 자체 복사본이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-343">Each site has its own copy of these assemblies in its Bin directory.</span></span> <span data-ttu-id="11205-344">어셈블리에 대 한 개체 코드가 동일 하지만 물리적으로 별도 어셈블리를 각 어셈블리는 콜드 사이트 시작 하는 동안 개별적으로 읽을 수 있도록 하 고 메모리에 별도로 보관.</span><span class="sxs-lookup"><span data-stu-id="11205-344">Even though the object code for the assemblies is identical, they're physically separate assemblies, so each assembly has to be read separately during cold site startup and kept separately in memory.</span></span>

<span data-ttu-id="11205-345">새 interning 기능은 이러한 비효율성을 해결 하 고 부하 및 RAM 요구 사항을 줄입니다 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-345">The new interning functionality solves this inefficiency and reduces both RAM requirements and load time.</span></span> <span data-ttu-id="11205-346">있습니다 인터닝 Windows 파일 시스템에서 각 어셈블리의 단일 복사본을 유지 하 고 단일 복사본에 대 한 기호화 된 링크를 사용 하 여 사이트 Bin 폴더에서 개별 어셈블리가 교체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-346">Interning lets Windows keep a single copy of each assembly in the file system, and individual assemblies in the site Bin folders are replaced with symbolic links to the single copy.</span></span> <span data-ttu-id="11205-347">개별 사이트를 고유한 버전의 어셈블리에 필요한 기호화 된 링크를 어셈블리의 새 버전으로 대체 되 고 해당 사이트에만 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-347">If an individual site needs a distinct version of the assembly, the symbolic link is replaced by the new version of the assembly, and only that site is affected.</span></span>

<span data-ttu-id="11205-348">Aspnet 라는 새 도구 필요 기호화 된 링크를 사용 하 여 어셈블리를 공유\_intern.exe 만들고 인턴 지정된 어셈블리의 저장소를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-348">Sharing assemblies using symbolic links requires a new tool named aspnet\_intern.exe, which lets you create and manage the store of interned assemblies.</span></span> <span data-ttu-id="11205-349">Visual Studio 11 개발자 미리 보기 SDK의 일부로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-349">It is provided as a part of the Visual Studio 11 Developer Preview SDK.</span></span> <span data-ttu-id="11205-350">그러나 (만.NET Framework 4 설치 설치한 경우 최신 시스템에서 작동 한다는 [업데이트](https://support.microsoft.com/kb/2468871).)</span><span class="sxs-lookup"><span data-stu-id="11205-350">(However, it will work on a system that has only the .NET Framework 4 installed, assuming you have installed the latest [update](https://support.microsoft.com/kb/2468871).)</span></span>

<span data-ttu-id="11205-351">Aspnet를 실행 하면 모든 적격 어셈블리가 인턴 지정 되어 있는지,\_intern.exe 주기적으로 (예: 예약된 된 태스크로 일주일에 한 번).</span><span class="sxs-lookup"><span data-stu-id="11205-351">To make sure all eligible assemblies have been interned, you run aspnet\_intern.exe periodically (for example, once a week as a scheduled task).</span></span> <span data-ttu-id="11205-352">일반적인 용도 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-352">A typical use is as follows:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

<span data-ttu-id="11205-353">모든 옵션을 표시 인수 없이 도구를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-353">To see all options, run the tool with no arguments.</span></span>

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a><span data-ttu-id="11205-354">빠른 시작에 대 한 다중 코어 JIT 컴파일을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="11205-354">Using multi-Core JIT compilation for faster startup</span></span>

<span data-ttu-id="11205-355">**요구 사항**:.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="11205-355">**Requirement**: .NET Framework 4.5</span></span>

<span data-ttu-id="11205-356">콜드 사이트 신생 기업의 어셈블리 필요가 디스크에서 읽을 수 뿐만 아니라 JIT 컴파일 사이트 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-356">For a cold site startup, not only do assemblies have to be read from disk, but the site must be JIT-compiled.</span></span> <span data-ttu-id="11205-357">복잡 한 사이트에이 상당한 지연이 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-357">For a complex site, this can add significant delays.</span></span> <span data-ttu-id="11205-358">.NET Framework 4.5의 새로운 범용 기법 사용 가능한 프로세서 코어 JIT 컴파일 분배 하 여 이러한 지연을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-358">A new general-purpose technique in the .NET Framework 4.5 reduces these delays by spreading JIT-compilation across available processor cores.</span></span> <span data-ttu-id="11205-359">만큼이 작업을 수행 하 고 최대한 빨리 도중 수집 된 정보를 사용 하 여 이전 시작 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-359">It does this as much and as early as possible by using information gathered during previous launches of the site.</span></span> <span data-ttu-id="11205-360">이 기능에 의해 구현 된 [System.Runtime.ProfileOptimization.StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) 메서드.</span><span class="sxs-lookup"><span data-stu-id="11205-360">This functionality implemented by the [System.Runtime.ProfileOptimization.StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) method.</span></span>

<span data-ttu-id="11205-361">JIT 컴파일 다중 코어를 사용 하 여이 기능을 활용 하기 위해 아무것도 할 필요가 없습니다 있도록 ASP.NET에서 기본으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-361">JIT-compiling using multiple cores is enabled by default in ASP.NET, so you do not need to do anything to take advantage of this feature.</span></span> <span data-ttu-id="11205-362">이 기능을 사용 하지 않도록 설정 하려는 경우 Web.config 파일에서 다음 설정을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-362">If you want to disable this feature, make the following setting in the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a><span data-ttu-id="11205-363">메모리 최적화 하기 위해 가비지 수집 튜닝</span><span class="sxs-lookup"><span data-stu-id="11205-363">Tuning garbage collection to optimize for memory</span></span>

<span data-ttu-id="11205-364">**요구 사항**:.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="11205-364">**Requirement**: .NET Framework 4.5</span></span>

<span data-ttu-id="11205-365">사이트 실행 되 면 중요 한 요인으로 메모리 소비가-GC (가비지 수집기) 힙의 사용 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-365">Once a site is running, its use of the garbage-collector (GC) heap can be a significant factor in its memory consumption.</span></span> <span data-ttu-id="11205-366">모든 가비지 수집기와 같은.NET Framework GC CPU 시간 (빈도 및 컬렉션의 의미) 및 메모리 사용 (새, 확보, 또는 무료 가능 개체에 사용 되는 추가 공백) 사이 균형을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="11205-366">Like any garbage collector, the .NET Framework GC makes tradeoffs between CPU time (frequency and significance of collections) and memory consumption (extra space that is used for new, freed, or free-able objects).</span></span> <span data-ttu-id="11205-367">이전 릴리스에 대 한 적절 한 균형을 달성 하기 위해 GC를 구성 하는 방법에 지침 제공 된 (예를 들어, 참조 [ASP.NET 2.0/3.5 공유 호스팅 구성](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)).</span><span class="sxs-lookup"><span data-stu-id="11205-367">For previous releases, we have provided guidance on how to configure the GC to achieve the right balance (for example, see [ASP.NET 2.0/3.5 Shared Hosting Configuration](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration)).</span></span>

<span data-ttu-id="11205-368">여러 독립 실행형 설정, 작업 정의 구성 설정 하는 대신.NET Framework 4.5에서 사용할 수 있습니다 수 있게 해 주는 모든는 이전에 권장 되는 GC 뿐만 설정을 새 튜닝 당 사이트에 대 한 추가 성능 제공 작업 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-368">For the .NET Framework 4.5, instead of multiple standalone settings, a workload-defined configuration setting is available that enables all of the previously recommended GC settings as well as new tuning that delivers additional performance for the per-site working set.</span></span>

<span data-ttu-id="11205-369">튜닝 GC 메모리를 사용 하려면 Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config 파일에 다음 설정을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-369">To enable GC memory tuning, add the following setting to the Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

<span data-ttu-id="11205-370">(Aspnet.config에 변경 내용에 대 한 이전 지침을 사용 하 여 친숙 한 경우이 설정은 이전 설정을 대체는 참고-예를 들어 gcServer, gcConcurrent 등을 설정 하지 않아도 됩니다. 필요가 없습니다 이전 설정을 제거 합니다.)</span><span class="sxs-lookup"><span data-stu-id="11205-370">(If you're familiar with the previous guidance for changes to aspnet.config, note that this setting replaces the old settings — for example, there is no need to set gcServer, gcConcurrent, etc. You do not have to remove the old settings.)</span></span>

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a><span data-ttu-id="11205-371">웹 응용 프로그램 프리페치</span><span class="sxs-lookup"><span data-stu-id="11205-371">Prefetching for web applications</span></span>

<span data-ttu-id="11205-372">**요구 사항**: Windows 8을 실행 하는.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="11205-372">**Requirement**: .NET Framework 4.5 running on Windows 8</span></span>

<span data-ttu-id="11205-373">몇 번의 릴리스에서 Windows 기술을 통해 포함 된 합니다 [prefetcher](http://en.wikipedia.org/wiki/Prefetcher) 응용 프로그램 시작 디스크 읽기 비용을 줄일 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-373">For several releases, Windows has included a technology known as the [prefetcher](http://en.wikipedia.org/wiki/Prefetcher) that reduces the disk-read cost of application startup.</span></span> <span data-ttu-id="11205-374">콜드 시작 클라이언트 응용 프로그램에 주로 문제 이기 때문에이 기술에는 서버에 필요한 구성 요소만 포함 하는 Windows Server에 포함 되지 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-374">Because cold startup is a problem predominantly for client applications, this technology has not been included in Windows Server, which includes only components that are essential to a server.</span></span> <span data-ttu-id="11205-375">프리페치는 최신 버전의 Windows Server에서 개별 웹 사이트의 출시를 최적화할 수 있다는 것에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-375">Prefetching is now available in the latest version of Windows Server, where it can optimize the launch of individual websites.</span></span>

<span data-ttu-id="11205-376">Windows server는 prefetcher 기본적으로 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-376">For Windows Server, the prefetcher is not enabled by default.</span></span> <span data-ttu-id="11205-377">를 사용 하도록 설정 및 고밀도 웹 호스팅을 위한 prefetcher를 구성 하려면 명령줄에서 다음 명령 집합을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-377">To enable and configure the prefetcher for high-density web hosting, run the following set of commands at the command line:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

<span data-ttu-id="11205-378">그런 다음는 prefetcher ASP.NET 응용 프로그램에 통합 하려면 다음 Web.config 파일에 추가:</span><span class="sxs-lookup"><span data-stu-id="11205-378">Then, to integrate the prefetcher with ASP.NET applications, add the following to the Web.config file:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="11205-379">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="11205-379">ASP.NET Web Forms</span></span>

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a><span data-ttu-id="11205-380">강력한 형식의 데이터 컨트롤</span><span class="sxs-lookup"><span data-stu-id="11205-380">Strongly Typed Data Controls</span></span>

<span data-ttu-id="11205-381">ASP.NET 4.5 Web Forms는 데이터로 작업 하기 위한 몇 가지 향상 된 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-381">In ASP.NET 4.5, Web Forms includes some improvements for working with data.</span></span> <span data-ttu-id="11205-382">첫 번째 향상은 강력한 형식의 데이터를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-382">The first improvement is strongly typed data controls.</span></span> <span data-ttu-id="11205-383">이전 버전의 ASP.NET Web Forms 컨트롤에 표시할 있습니다 사용 하 여 데이터 바인딩된 값 *Eval* 및 데이터 바인딩 식:</span><span class="sxs-lookup"><span data-stu-id="11205-383">For Web Forms controls in previous versions of ASP.NET, you display a data-bound value using *Eval* and a data-binding expression:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

<span data-ttu-id="11205-384">양방향 데이터 바인딩을 사용 하 여 있습니다 *바인딩할*:</span><span class="sxs-lookup"><span data-stu-id="11205-384">For two-way data binding, you use *Bind*:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

<span data-ttu-id="11205-385">런타임 시 이러한 호출은 리플렉션을 사용 하 여 지정된 된 멤버의 값을 읽고 다음 태그에서 결과 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-385">At run time, these calls use reflection to read the value of the specified member and then display the result in the markup.</span></span> <span data-ttu-id="11205-386">이 접근 방식을 쉽게 unshaped 임의의 데이터에 대 한 데이터 바인딩.</span><span class="sxs-lookup"><span data-stu-id="11205-386">This approach makes it easy to data bind against arbitrary, unshaped data.</span></span>

<span data-ttu-id="11205-387">그러나 데이터 바인딩 식을 다음과 같이 멤버 이름, 탐색 (정의로 이동 등), 또는 이러한 이름에 대 한 확인 하는 컴파일 타임에 대 한 IntelliSense와 같은 기능을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-387">However, data-binding expressions like this don't support features like IntelliSense for member names, navigation (like Go To Definition), or compile-time checking for these names.</span></span>

<span data-ttu-id="11205-388">이 문제를 해결 하기 위해 ASP.NET 4.5 컨트롤에 바인딩되는 데이터의 데이터 형식을 선언 하는 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-388">To address this issue, ASP.NET 4.5 adds the ability to declare the data type of the data that a control is bound to.</span></span> <span data-ttu-id="11205-389">이렇게 하면 새 *ItemType* 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-389">You do this using the new *ItemType* property.</span></span> <span data-ttu-id="11205-390">데이터 바인딩 식의 범위에 두 개의 새 형식화 된 변수를 사용할 수 있습니다이 속성을 설정 하는 경우: *항목* 하 고 *binditem을*입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-390">When you set this property, two new typed variables are available in the scope of data-binding expressions: *Item* and *BindItem*.</span></span> <span data-ttu-id="11205-391">변수는 강력한 형식 이므로 Visual Studio 개발 환경의 모든 혜택을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-391">Because the variables are strongly typed, you get the full benefits of the Visual Studio development experience.</span></span>


<span data-ttu-id="11205-392">양방향 데이터 바인딩 식을 사용 합니다 *binditem을* 변수:</span><span class="sxs-lookup"><span data-stu-id="11205-392">For two-way data-binding expressions, use the *BindItem* variable:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]


<span data-ttu-id="11205-393">대부분의 ASP.NET Web Forms 프레임 워크에서 지 원하는 컨트롤에 데이터 바인딩을 지원 하도록 업데이트 되었습니다 합니다 *ItemType* 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-393">Most controls in the ASP.NET Web Forms framework that support data binding have been updated to support the *ItemType* property.</span></span>

<a id="_Toc318097387"></a>
### <a name="model-binding"></a><span data-ttu-id="11205-394">모델 바인딩</span><span class="sxs-lookup"><span data-stu-id="11205-394">Model Binding</span></span>

<span data-ttu-id="11205-395">모델 바인딩을 코드에 초점을 맞춘 데이터 액세스를 사용 하 여 작업 하기 위해 ASP.NET Web Forms 컨트롤에서 데이터 바인딩을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-395">Model binding extends data binding in ASP.NET Web Forms controls to work with code-focused data access.</span></span> <span data-ttu-id="11205-396">개념을 통합 하는 *ObjectDataSource* 컨트롤 및 ASP.NET MVC의 모델 바인딩에서.</span><span class="sxs-lookup"><span data-stu-id="11205-396">It incorporates concepts from the *ObjectDataSource* control and from model binding in ASP.NET MVC.</span></span>

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a><span data-ttu-id="11205-397">데이터 선택</span><span class="sxs-lookup"><span data-stu-id="11205-397">Selecting data</span></span>

<span data-ttu-id="11205-398">컨트롤의 모델 바인딩을 사용 하 여 데이터를 선택 하도록 데이터 컨트롤을 구성 하려면 설정 *SelectMethod* 속성 페이지의 코드에 있는 메서드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-398">To configure a data control to use model binding to select data, you set the control's *SelectMethod* property to the name of a method in the page's code.</span></span> <span data-ttu-id="11205-399">데이터 컨트롤의 페이지 수명 주기의 적절 한 시간에 메서드를 호출 하 고 자동으로 반환된 된 데이터를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-399">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="11205-400">명시적으로 호출 하지 않아도 됩니다 합니다 *DataBind* 메서드.</span><span class="sxs-lookup"><span data-stu-id="11205-400">There's no need to explicitly call the *DataBind* method.</span></span>

<span data-ttu-id="11205-401">다음 예제에서는 *GridView* 제어 라는 메서드를 사용 하도록 구성 되어 *GetCategories*:</span><span class="sxs-lookup"><span data-stu-id="11205-401">In the following example, the *GridView* control is configured to use a method named *GetCategories*:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

<span data-ttu-id="11205-402">만든 합니다 *GetCategories* 페이지의 코드에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="11205-402">You create the *GetCategories* method in the page's code.</span></span> <span data-ttu-id="11205-403">간단한 select 작업에 대 한 메서드 매개 변수 없이 필요 하 고 반환 해야 합니다는 *IEnumerable* 하거나 *IQueryable* 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-403">For a simple select operation, the method needs no parameters and should return an *IEnumerable* or *IQueryable* object.</span></span> <span data-ttu-id="11205-404">하는 경우 새 *ItemType* 속성은 (는 강력한 데이터 바인딩 식에서 설명 했 듯이 [강력한 형식의 데이터 컨트롤](#_Toc318097386) 이전), 이러한 인터페이스의 제네릭 버전 반환 되어야- *IEnumerable&lt;T&gt;*  하거나 *IQueryable&lt;T&gt;* 를 사용 하 여 합니다 *T* 매개 변수 형식과 일치 하는 *ItemType* 속성 (예를 들어 *IQueryable&lt;범주&gt;*).</span><span class="sxs-lookup"><span data-stu-id="11205-404">If the new *ItemType* property is set (which enables strongly typed data-binding expressions, as explained under [Strongly Typed Data Controls](#_Toc318097386) earlier), the generic versions of these interfaces should be returned — *IEnumerable&lt;T&gt;* or *IQueryable&lt;T&gt;*, with the *T* parameter matching the type of the *ItemType* property (for example, *IQueryable&lt;Category&gt;*).</span></span>

<span data-ttu-id="11205-405">다음 예제에서는 코드를 *GetCategories* 메서드.</span><span class="sxs-lookup"><span data-stu-id="11205-405">The following example shows the code for a *GetCategories* method.</span></span> <span data-ttu-id="11205-406">이 예제에서는 Northwind 샘플 데이터베이스를 사용 하 여 Entity Framework Code First 모델을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-406">This example uses the Entity Framework Code First model with the Northwind sample database.</span></span> <span data-ttu-id="11205-407">코드에서는 쿼리에서의 방식으로 각 범주에 대 한 관련 된 제품의 세부 정보를 반환 하는지 확인 합니다 *Include* 메서드.</span><span class="sxs-lookup"><span data-stu-id="11205-407">The code makes sure that the query returns details of the related products for each category by way of the *Include* method.</span></span> <span data-ttu-id="11205-408">(이렇게 합니다 *TemplateField* 태그의 요소에에서 필요 없이 각 범주에서 제품의 개수를 표시를 [n + 1 선택](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem).)</span><span class="sxs-lookup"><span data-stu-id="11205-408">(This ensures that the *TemplateField* element in the markup displays the count of products in each category without requiring an [n+1 select](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem).)</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

<span data-ttu-id="11205-409">페이지를 실행 하는 경우, *GridView* 컨트롤을 호출 합니다 *GetCategories* 메서드 자동으로 구성 된 필드를 사용 하 여 반환 된 데이터를 렌더링:</span><span class="sxs-lookup"><span data-stu-id="11205-409">When the page runs, the *GridView* control calls the *GetCategories* method automatically and renders the returned data using the configured fields:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

<span data-ttu-id="11205-410">Select 메서드 반환 하기 때문에 *IQueryable* 개체를 *GridView* 컨트롤 실행 하기 전에 쿼리를 추가로 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-410">Because the select method returns an *IQueryable* object, the *GridView* control can further manipulate the query before executing it.</span></span> <span data-ttu-id="11205-411">예를 들어 합니다 *GridView* 컨트롤에는 반환 된 페이징 및 정렬에 대 한 쿼리 식을 추가할 수 있습니다 *IQueryable* 실행 하기 전에 이러한 작업 내부에서 수행 되도록 개체 LINQ 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-411">For example, the *GridView* control can add query expressions for sorting and paging to the returned *IQueryable* object before it is executed, so that those operations are performed by the underlying LINQ provider.</span></span> <span data-ttu-id="11205-412">이 경우 Entity Framework 데이터베이스에서 이러한 작업은 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-412">In this case, Entity Framework will ensure those operations are performed in the database.</span></span>

<span data-ttu-id="11205-413">다음 예제와 합니다 *GridView* 컨트롤 정렬 및 페이징을 허용 하도록 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-413">The following example shows the *GridView* control modified to allow sorting and paging:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

<span data-ttu-id="11205-414">이제 페이지를 실행 하는 경우 컨트롤은 데이터의 현재 페이지에 대해서만 표시 되 고 선택한 열을 기준으로 정렬 된 가능:</span><span class="sxs-lookup"><span data-stu-id="11205-414">Now when the page runs, the control can make sure that only the current page of data is displayed and that it's ordered by the selected column:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

<span data-ttu-id="11205-415">반환된 된 데이터를 필터링 하려면 매개 변수는 select 메서드를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-415">To filter the returned data, parameters have to be added to the select method.</span></span> <span data-ttu-id="11205-416">이러한 매개 변수는 실행 시 모델 바인딩에서 채워지고 데이터를 반환 하기 전에 쿼리를 변경 하려면 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-416">These parameters will be populated by the model binding at run time, and you can use them to alter the query before returning the data.</span></span>

<span data-ttu-id="11205-417">예를 들어, 쿼리 문자열에 키워드를 입력 하 여 사용자가 제품 필터를 사용 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-417">For example, assume that you want to let users filter products by entering a keyword in the query string.</span></span> <span data-ttu-id="11205-418">메서드 매개 변수를 추가 하 고 매개 변수 값을 사용 하도록 코드를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-418">You can add a parameter to the method and update the code to use the parameter value:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

<span data-ttu-id="11205-419">이 코드에 포함 되어는 *여기서* 식에 대 한 값이 제공 하는 경우 *키워드* 다음 쿼리 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-419">This code includes a *Where* expression if a value is provided for *keyword* and then returns the query results.</span></span>

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a><span data-ttu-id="11205-420">값 공급자</span><span class="sxs-lookup"><span data-stu-id="11205-420">Value providers</span></span>

<span data-ttu-id="11205-421">이전 예제에서는 위치에 대 한 특정 없습니다. 값을 *키워드* 매개 변수에서 제공 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-421">The previous example was not specific about where the value for the *keyword* parameter was coming from.</span></span> <span data-ttu-id="11205-422">이 정보를 나타내기 매개 변수 특성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-422">To indicate this information, you can use a parameter attribute.</span></span> <span data-ttu-id="11205-423">예를 들어 사용할 수 있습니다 합니다 *QueryStringAttribute* 에 있는 클래스는 *System.Web.ModelBinding* 네임 스페이스:</span><span class="sxs-lookup"><span data-stu-id="11205-423">For this example, you can use the *QueryStringAttribute* class that's in the *System.Web.ModelBinding* namespace:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

<span data-ttu-id="11205-424">이렇게 하면 모델 바인딩 값을 바인딩하는 쿼리 문자열을 시도 하는 *키워드* 런타임에 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-424">This instructs model binding to try to bind a value from the query string to the *keyword* parameter at run time.</span></span> <span data-ttu-id="11205-425">(할 형식 변환을 수행 하지만 경우 그렇지 않습니다.) 값을 제공할 수 없습니다 하 고 형식이 nullable이 아닌 경우 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-425">(This might involve performing type conversion, although it doesn't in this case.) If a value cannot be provided and the type is non-nullable, an exception is thrown.</span></span>

<span data-ttu-id="11205-426">이러한 메서드는 값의 소스는 값 공급자 라고도 하며 사용 하는 값 공급자를 나타내는 매개 변수 특성 값 공급자 특성으로 참조 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-426">The sources of values for these methods are referred to as value providers, and the parameter attributes that indicate which value provider to use are referred to as value provider attributes.</span></span> <span data-ttu-id="11205-427">Web Forms는 Web Forms 응용 프로그램을 쿼리 문자열, 쿠키, 폼 값, 컨트롤, 상태 보기, 세션 상태, 프로필 속성 등의 모든 사용자 입력의 일반적인 원본에 대 한 값 공급자 및 해당 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-427">Web Forms will include value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application, such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="11205-428">또한 사용자 지정 값 공급자를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-428">You can also write custom value providers.</span></span>

<span data-ttu-id="11205-429">기본적으로 매개 변수 이름 값 공급자 컬렉션에서 값을 찾을 키로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-429">By default, the parameter name is used as the key to find a value in the value provider collection.</span></span> <span data-ttu-id="11205-430">코드 예제에서는 키워드를 명명 된 쿼리 문자열 값에 대 한 표시 됩니다 (예를 들어, ~ / default.aspx?keyword=chef).</span><span class="sxs-lookup"><span data-stu-id="11205-430">In the example, the code will look for a query-string value named keyword (for example, ~/default.aspx?keyword=chef).</span></span> <span data-ttu-id="11205-431">매개 변수 특성에 인수로 전달 하 여 사용자 지정 키를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-431">You can specify a custom key by passing it as an argument to the parameter attribute.</span></span> <span data-ttu-id="11205-432">예를 들어 질문 및 답변을 명명 된 쿼리 문자열 변수의 값을 사용 하려면이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-432">For example, to use the value of the query-string variable named q, you could do this:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

<span data-ttu-id="11205-433">이 방법은 페이지의 코드에서 사용자 쿼리 문자열을 사용 하 여 키워드를 전달 하 여 결과 필터링 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-433">If this method is in the page's code, users can filter the results by passing a keyword using the query string:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

<span data-ttu-id="11205-434">모델 바인딩을 직접 코딩 하는 것이 고, 그렇지는 많은 작업을 수행 합니다: 값을 읽기, null 값을 확인 하는, 적절 한 형식으로 변환 하는 동안, 변환 성공 여부를 확인 및 마지막으로 값을 사용 하 여는 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-434">Model binding accomplishes many tasks that you would otherwise have to code by hand: reading the value, checking for a null value, attempting to convert it to the appropriate type, checking whether the conversion was successful, and finally, using the value in the query.</span></span> <span data-ttu-id="11205-435">바인딩 결과 훨씬 적은 코드 및 응용 프로그램 전체에서 기능을 재사용할 수 있는 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-435">Model binding results in far less code and in the ability to reuse the functionality throughout your application.</span></span>

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a><span data-ttu-id="11205-436">컨트롤에서 값으로 필터링</span><span class="sxs-lookup"><span data-stu-id="11205-436">Filtering by values from a control</span></span>

<span data-ttu-id="11205-437">드롭다운 목록에서 필터 값을 선택할 수 있도록 예제를 확장 하려고 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-437">Suppose you want to extend the example to let the user choose a filter value from a drop-down list.</span></span> <span data-ttu-id="11205-438">태그에 다음 드롭다운 목록 추가 하 고 다른 방법을 사용 하 여 해당 데이터를 가져오기 위해 구성 합니다 *SelectMethod* 속성:</span><span class="sxs-lookup"><span data-stu-id="11205-438">Add the following drop-down list to the markup and configure it to get its data from another method using the *SelectMethod* property:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

<span data-ttu-id="11205-439">일반적으로 추가할 수도 있습니다는 *있도록 EmptyDataTemplate* 요소를 *GridView* 컨트롤을 일치 하는 제품은 없습니다 발견 되 면 컨트롤 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-439">Typically you would also add an *EmptyDataTemplate* element to the *GridView* control so that the control will display a message if no matching products are found:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

<span data-ttu-id="11205-440">페이지 코드를 새 선택 드롭다운 목록에 대 한 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-440">In the page code, add the new select method for the drop-down list:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

<span data-ttu-id="11205-441">마지막으로 업데이트 합니다 *GetProducts* 드롭 다운 목록에서 선택한 범주 ID를 포함 하는 새 매개 변수를 사용 하는 방법 선택:</span><span class="sxs-lookup"><span data-stu-id="11205-441">Finally, update the *GetProducts* select method to take a new parameter that contains the ID of the selected category from the drop-down list:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

<span data-ttu-id="11205-442">이제 페이지를 실행 하는 경우 사용자가 드롭다운 목록에서 범주를 선택할 수 및 *GridView* 컨트롤은 자동으로 다시 바인딩되어 필터링된 된 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-442">Now when the page runs, users can select a category from the drop-down list, and the *GridView* control is automatically re-bound to show the filtered data.</span></span> <span data-ttu-id="11205-443">모델 바인딩 선택 방법에 대 한 매개 변수 값을 추적 하 고 모든 매개 변수 값을 다시 게시 한 후 변경 되었는지 여부를 검색 하기 때문에 이것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-443">This is possible because model binding tracks the values of parameters for select methods and detects whether any parameter value has changed after a postback.</span></span> <span data-ttu-id="11205-444">그렇다면 모델 바인딩에 연결된 된 데이터 컨트롤에 데이터를 다시 바인딩할 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-444">If so, model binding forces the associated data control to re-bind to the data.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a><span data-ttu-id="11205-445">HTML 인코딩된 데이터 바인딩 식</span><span class="sxs-lookup"><span data-stu-id="11205-445">HTML Encoded Data-Binding Expressions</span></span>

<span data-ttu-id="11205-446">이제 HTML 인코딩 데이터 바인딩 식의 결과를 것 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-446">You can now HTML-encode the result of data-binding expressions.</span></span> <span data-ttu-id="11205-447">콜론 (:)의 끝에 추가 된 &lt;% # 데이터 바인딩 식을 표시 하는 접두사:</span><span class="sxs-lookup"><span data-stu-id="11205-447">Add a colon (:) to the end of the &lt;%# prefix that marks the data-binding expression:</span></span>

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a><span data-ttu-id="11205-448">비간섭 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="11205-448">Unobtrusive Validation</span></span>

<span data-ttu-id="11205-449">이제 클라이언트 쪽 유효성 검사 논리에 대 한 비간섭 JavaScript를 사용 하는 기본 제공 유효성 검사기 컨트롤을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-449">You can now configure the built-in validator controls to use unobtrusive JavaScript for client-side validation logic.</span></span> <span data-ttu-id="11205-450">이 크게 줄어듭니다 페이지 태그에 인라인으로 렌더링 하는 JavaScript 및 전체 페이지 크기를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-450">This significantly reduces the amount of JavaScript rendered inline in the page markup and reduces the overall page size.</span></span> <span data-ttu-id="11205-451">이러한 방법 중 하나로 유효성 검사기 컨트롤에 대 한 비간섭 JavaScript를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-451">You can configure unobtrusive JavaScript for validator controls in any of these ways:</span></span>

- <span data-ttu-id="11205-452">에 다음 설정을 추가 하 여 전 세계 합니다 *&lt;appSettings&gt;* Web.config 파일의 요소:</span><span class="sxs-lookup"><span data-stu-id="11205-452">Globally by adding the following setting to the *&lt;appSettings&gt;* element in the Web.config file:</span></span> 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- <span data-ttu-id="11205-453">정적을 설정 하는 여 전 세계 *System.Web.UI.ValidationSettings.UnobtrusiveValidationMode* 속성을 *UnobtrusiveValidationMode.WebForms* (일반적으로 *응용 프로그램 \_시작* Global.asax 파일에는 메서드).</span><span class="sxs-lookup"><span data-stu-id="11205-453">Globally by setting the static *System.Web.UI.ValidationSettings.UnobtrusiveValidationMode* property to *UnobtrusiveValidationMode.WebForms* (typically in the *Application\_Start* method in the Global.asax file).</span></span>
- <span data-ttu-id="11205-454">새 설정 하 여 페이지에 대해 개별적으로 *UnobtrusiveValidationMode* 의 속성을 *페이지* 클래스를 *UnobtrusiveValidationMode.WebForms*합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-454">Individually for a page by setting the new *UnobtrusiveValidationMode* property of the *Page* class to *UnobtrusiveValidationMode.WebForms*.</span></span>

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a><span data-ttu-id="11205-455">HTML5 업데이트</span><span class="sxs-lookup"><span data-stu-id="11205-455">HTML5 Updates</span></span>

<span data-ttu-id="11205-456">몇 가지 개선이 이루어졌습니다 Web forms 서버 컨트롤 HTML5의 새로운 기능을 활용 하려면:</span><span class="sxs-lookup"><span data-stu-id="11205-456">Some improvements have been made to Web Forms server controls to take advantage of new features of HTML5:</span></span>

- <span data-ttu-id="11205-457">*TextMode* 의 속성을 *텍스트 상자에 붙여넣습니다* 제어와 같은 새로운 HTML5 입력된 형식을 지원 하도록 업데이트 되었습니다 *전자 메일*, *datetime*, 및 등등입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-457">The *TextMode* property of the *TextBox* control has been updated to support the new HTML5 input types like *email*, *datetime*, and so on.</span></span>
- <span data-ttu-id="11205-458">합니다 *FileUpload* 이 HTML5 기능을 지 원하는 브라우저에서 여러 파일 업로드 지원 이제를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-458">The *FileUpload* control now supports multiple file uploads from browsers that support this HTML5 feature.</span></span>
- <span data-ttu-id="11205-459">유효성 검사기는 이제 지원 유효성 검사 HTML5 입력된 요소를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-459">Validator controls now support validating HTML5 input elements.</span></span>
- <span data-ttu-id="11205-460">이제 URL을 나타내는 특성이 있는 새 HTML5 요소 지원 runat = "server"입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-460">New HTML5 elements that have attributes that represent a URL now support runat="server".</span></span> <span data-ttu-id="11205-461">결과적으로 같은 사용할 수 있습니다 ASP.NET 규칙 URL 경로에 ~를 나타내는 응용 프로그램 루트 연산자 (예를 들어 &lt;비디오 runat = "server" src="~/myVideo.wmv" /&gt;).</span><span class="sxs-lookup"><span data-stu-id="11205-461">As a result, you can use ASP.NET conventions in URL paths, like the ~ operator to represent the application root (for example, &lt;video runat="server" src="~/myVideo.wmv" /&gt;).</span></span>
- <span data-ttu-id="11205-462">합니다 *UpdatePanel* 컨트롤 게시 HTML5 입력된 필드를 지원 하도록 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-462">The *UpdatePanel* control has been fixed to support posting HTML5 input fields.</span></span>

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a><span data-ttu-id="11205-463">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="11205-463">ASP.NET MVC 4</span></span>

<span data-ttu-id="11205-464">ASP.NET MVC 4 베타는 이제 Visual Studio 11 Beta를 사용 하 여 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-464">ASP.NET MVC 4 Beta is now included with Visual Studio 11 Beta.</span></span> <span data-ttu-id="11205-465">ASP.NET MVC는 모델-뷰-컨트롤러 (MVC) 패턴을 활용 하 여 항상 테스트 가능 하 고 유지 관리 가능한 웹 응용 프로그램을 개발 하기 위한 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-465">ASP.NET MVC is a framework for developing highly testable and maintainable Web applications by leveraging the Model-View-Controller (MVC) pattern.</span></span> <span data-ttu-id="11205-466">ASP.NET MVC 4는 손쉽게 모바일 웹 응용 프로그램을 개발 하 고 모든 장치를 연결할 수 있는 HTTP 서비스를 작성할 수 있는 ASP.NET Web API를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-466">ASP.NET MVC 4 makes it easy to build applications for the mobile Web and includes ASP.NET Web API, which helps you build HTTP services that can reach any device.</span></span> <span data-ttu-id="11205-467">자세한 내용은 참조는 [ASP.NET MVC 4 릴리스](mvc4-release-notes.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-467">For more information, see the [ASP.NET MVC 4 Release Notes](mvc4-release-notes.md).</span></span>

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a><span data-ttu-id="11205-468">ASP.NET 웹 페이지 2</span><span class="sxs-lookup"><span data-stu-id="11205-468">ASP.NET Web Pages 2</span></span>

<span data-ttu-id="11205-469">새 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-469">New features include the following:</span></span>

- <span data-ttu-id="11205-470">신규 및 업데이트 된 사이트 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-470">New and updated site templates.</span></span>
- <span data-ttu-id="11205-471">서버 쪽 및 클라이언트 쪽 유효성 검사를 사용 하 여 추가 합니다 *유효성 검사* 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-471">Adding server-side and client-side validation using the *Validation* helper.</span></span>
- <span data-ttu-id="11205-472">자산 관리자를 사용 하 여 스크립트를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-472">The ability to register scripts using an assets manager.</span></span>
- <span data-ttu-id="11205-473">Facebook OAuth 및 OpenID를 사용 하 여 다른 사이트에서 로그인을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-473">Enabling logins from Facebook and other sites using OAuth and OpenID.</span></span>
- <span data-ttu-id="11205-474">맵 추가 합니다 *매핑합니다* 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-474">Adding maps using the *Maps* helper.</span></span>
- <span data-ttu-id="11205-475">웹 페이지 응용 프로그램에서 함께 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-475">Running Web Pages applications side-by-side.</span></span>
- <span data-ttu-id="11205-476">모바일 장치에 대 한 페이지를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-476">Rendering pages for mobile devices.</span></span>

<span data-ttu-id="11205-477">이러한 기능 및 전체 페이지 코드 예제에 대 한 자세한 내용은 참조 하세요. [웹 페이지 2 Beta의 주요 기능](https://go.microsoft.com/fwlink/?LinkID=227824)합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-477">For more information about these features and full-page code examples, see [The Top Features in Web Pages 2 Beta](https://go.microsoft.com/fwlink/?LinkID=227824).</span></span>

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a><span data-ttu-id="11205-478">Visual Web Developer 11 베타</span><span class="sxs-lookup"><span data-stu-id="11205-478">Visual Web Developer 11 Beta</span></span>

<span data-ttu-id="11205-479">이 섹션에서는 Visual Web Developer 11 베타 및 Visual Studio 2012 Release Candidate의 웹 개발에 대 한 향상 된 기능에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-479">This section provides information about improvements for web development in Visual Web Developer 11 Beta and Visual Studio 2012 Release Candidate.</span></span>

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a><span data-ttu-id="11205-480">Visual Studio 2010 및 Visual Studio 2012 Release Candidate (프로젝트 호환성) 간에 공유 프로젝트</span><span class="sxs-lookup"><span data-stu-id="11205-480">Project Sharing Between Visual Studio 2010 and Visual Studio 2012 Release Candidate (Project Compatibility)</span></span>

<span data-ttu-id="11205-481">Visual Studio 2012 Release Candidate 될 때까지 기존 프로젝트를 최신 버전의 Visual Studio에서 열기 변환 마법사를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-481">Until Visual Studio 2012 Release Candidate, opening an existing project in a newer version of Visual Studio launched the Conversion Wizard.</span></span> <span data-ttu-id="11205-482">이 이전 버전과 호환 되지 않는 새로운 형식으로 콘텐츠 (자산) 프로젝트 및 솔루션 업그레이드를 강제 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-482">This forced an upgrade of the content (assets) of a project and solution to new formats that were not backward compatible.</span></span> <span data-ttu-id="11205-483">따라서 변환 후 있습니다 열지 못했습니다 프로젝트 Visual Studio의 이전 버전에서.</span><span class="sxs-lookup"><span data-stu-id="11205-483">Therefore, after the conversion you could not open the project in the older version of Visual Studio.</span></span>

<span data-ttu-id="11205-484">많은 고객이 말했습니다이 없음을 올바른 접근 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-484">Many customers have told us that this was not the right approach.</span></span> <span data-ttu-id="11205-485">Visual Studio 11 Beta에서 이제 공유 프로젝트와 Visual Studio 2010 SP1을 사용 하 여 솔루션 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-485">In Visual Studio 11 Beta, we now support sharing projects and solutions with Visual Studio 2010 SP1.</span></span> <span data-ttu-id="11205-486">이 Visual Studio 2012 Release Candidate에서 2010 프로젝트를 열면 해야 Visual Studio 2010 SP1에서 프로젝트를 열 수를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-486">This means that if you open a 2010 project in Visual Studio 2012 Release Candidate, you will still be able to open the project in Visual Studio 2010 SP1.</span></span>

> [!NOTE]
> <span data-ttu-id="11205-487">Visual Studio 2010 SP1 및 Visual Studio 2012 Release Candidate 간의 몇 가지 형식의 프로젝트를 공유할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-487">A few types of projects cannot be shared between Visual Studio 2010 SP1 and Visual Studio 2012 Release Candidate.</span></span> <span data-ttu-id="11205-488">여기 몇 가지 이전 프로젝트 (예: ASP.NET MVC 2 프로젝트) 또는 프로젝트 (예: 설치 프로젝트) 특수 목적을 위해 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-488">These include some older projects (such as ASP.NET MVC 2 projects) or projects for special purposes (such as Setup projects).</span></span>

<span data-ttu-id="11205-489">처음으로 Visual Studio 11 Beta의 Visual Studio 2010 SP1 웹 프로젝트를 열면 다음 속성을 프로젝트 파일에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-489">When you open a Visual Studio 2010 SP1 Web project for the first time in Visual Studio 11 Beta, the following properties are added to the project file:</span></span>

- <span data-ttu-id="11205-490">FileUpgradeFlags</span><span class="sxs-lookup"><span data-stu-id="11205-490">FileUpgradeFlags</span></span>
- <span data-ttu-id="11205-491">UpgradeBackupLocation</span><span class="sxs-lookup"><span data-stu-id="11205-491">UpgradeBackupLocation</span></span>
- <span data-ttu-id="11205-492">OldToolsVersion</span><span class="sxs-lookup"><span data-stu-id="11205-492">OldToolsVersion</span></span>
- <span data-ttu-id="11205-493">VisualStudioVersion</span><span class="sxs-lookup"><span data-stu-id="11205-493">VisualStudioVersion</span></span>
- <span data-ttu-id="11205-494">VSToolsPath</span><span class="sxs-lookup"><span data-stu-id="11205-494">VSToolsPath</span></span>

<span data-ttu-id="11205-495">FileUpgradeFlags, UpgradeBackupLocation, 및 OldToolsVersion 프로젝트 파일을 업그레이드 하는 프로세스에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-495">FileUpgradeFlags, UpgradeBackupLocation, and OldToolsVersion are used by the process that upgrades the project file.</span></span> <span data-ttu-id="11205-496">영향을 미치지 않습니다 Visual Studio 2010에서 프로젝트를 사용 하 여 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-496">They have no impact on working with the project in Visual Studio 2010.</span></span>

<span data-ttu-id="11205-497">VisualStudioVersion에는 현재 프로젝트에 대 한 Visual Studio의 버전을 나타내는 MSBuild 4.5에서 사용 하는 새 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-497">VisualStudioVersion is a new property used by MSBuild 4.5 that indicates the version of Visual Studio for the current project.</span></span> <span data-ttu-id="11205-498">이 속성은 MSBuild 4.0 (Visual Studio 2010 SP1을 사용 하는 MSBuild의 버전)에 존재 하지, 때문에 프로젝트 파일에 기본값을 삽입 했습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-498">Because this property didn't exist in MSBuild 4.0 (the version of MSBuild that Visual Studio 2010 SP1 uses), we inject a default value into the project file.</span></span>

<span data-ttu-id="11205-499">VSToolsPath 속성 MSBuildExtensionsPath32 설정에 의해 표현 된 경로에서 가져올 올바른.targets 파일 확인에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-499">The VSToolsPath property is used to determine the correct .targets file to import from the path represented by the MSBuildExtensionsPath32 setting.</span></span>

<span data-ttu-id="11205-500">Import 요소와 관련 된 일부 변경 내용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-500">There are also some changes related to Import elements.</span></span> <span data-ttu-id="11205-501">이러한 변경은 Visual Studio의 두 버전 간의 호환성을 지원 하기 위해 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-501">These changes are required in order to support compatibility between both versions of Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="11205-502">프로젝트를 서로 다른 두 컴퓨터에서 Visual Studio 2010 SP1 및 Visual Studio 11 Beta 간에 공유 되는 경우 및 프로젝트에는 앱에서 로컬 데이터베이스를 포함 하는 경우\_데이터 폴더 해야 데이터베이스에서 사용 된 SQL Server 버전이 두 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-502">If a project is being shared between Visual Studio 2010 SP1 and Visual Studio 11 Beta on two different computers, and if the project includes a local database in the App\_Data folder, you must make sure that the version of SQL Server used by the database is installed on both computers.</span></span>

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a><span data-ttu-id="11205-503">ASP.NET 4.5 웹 사이트 템플릿의 구성 변경</span><span class="sxs-lookup"><span data-stu-id="11205-503">Configuration Changes in ASP.NET 4.5 Website Templates</span></span>

<span data-ttu-id="11205-504">기본값에는 다음 변경 사항이 생겼는지 *Web.config* Visual Studio 2012 Release Candidate에서 웹 사이트 템플릿을 사용 하 여 만든 사이트에 대 한 파일:</span><span class="sxs-lookup"><span data-stu-id="11205-504">The following changes have been made to the default *Web.config* file for site that are created using website templates in Visual Studio 2012 Release Candidate:</span></span>

- <span data-ttu-id="11205-505">에 `<httpRuntime>` 요소는 `encoderType` 특성은 이제 ASP.NET에 추가 된 AntiXSS 형식을 사용 하 여 기본적으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-505">In the `<httpRuntime>` element, the `encoderType` attribute is now set by default to use the AntiXSS types that were added to ASP.NET.</span></span> <span data-ttu-id="11205-506">자세한 내용은 참조 하세요 [AntiXSS 라이브러리](#_Toc318097382)합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-506">For details, see [AntiXSS Library](#_Toc318097382).</span></span>
- <span data-ttu-id="11205-507">또한 합니다 `<httpRuntime>` 요소는 `requestValidationMode` 특성을 "4.5"로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-507">Also in the `<httpRuntime>` element, the `requestValidationMode` attribute is set to "4.5".</span></span> <span data-ttu-id="11205-508">즉, 기본적으로 지연된 ("지연") 유효성 검사를 사용 하도록 요청 유효성 검사 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-508">This means that by default, request validation is configured to use deferred ("lazy") validation.</span></span> <span data-ttu-id="11205-509">자세한 내용은 참조 하세요 [새로운 ASP.NET 요청 유효성 검사 기능](#_Toc318097379)합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-509">For details, see [New ASP.NET Request Validation Features](#_Toc318097379).</span></span>
- <span data-ttu-id="11205-510">`<modules>` 의 요소를 `<system.webServer>` 섹션에 없는 `runAllManagedModulesForAllRequests` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-510">The `<modules>` element of the `<system.webServer>` section does not contain a `runAllManagedModulesForAllRequests` attribute.</span></span> <span data-ttu-id="11205-511">(기본값은 false입니다.) 즉, SP1로 업데이트 되지 않은 IIS 7의 버전을 사용 하는 경우 새 사이트에서 라우팅 문제가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-511">(Its default value is false.) This means that if you are using a version of IIS 7 that has not been updated to SP1, you might have issues with routing in a new site.</span></span> <span data-ttu-id="11205-512">자세한 내용은 [ASP.NET 라우팅에 대 한 IIS 7의 기본 지원을](#Native_Support_In_IIS7_For_ASPNET_Routine)합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-512">For more information, see [Native Support in IIS 7 for ASP.NET Routing](#Native_Support_In_IIS7_For_ASPNET_Routine).</span></span>

<span data-ttu-id="11205-513">이러한 변경 내용은 기존 응용 프로그램을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-513">These changes do not affect existing applications.</span></span> <span data-ttu-id="11205-514">그러나 이러한 기존 웹 사이트 및 새 템플릿을 사용 하 여 ASP.NET 4.5에 대해 만든 새 웹 사이트 간의 동작에서 차이 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-514">However, they might represent a difference in behavior between existing websites and new websites that you create for ASP.NET 4.5 using the new templates.</span></span>

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a><span data-ttu-id="11205-515">ASP.NET 라우팅에 대 한 IIS 7에서에서 기본적으로 지원</span><span class="sxs-lookup"><span data-stu-id="11205-515">Native Support in IIS 7 for ASP.NET Routing</span></span>

<span data-ttu-id="11205-516">따라서 ASP.NET 변경 하지만 SP1 업데이트는 적용 되지 않은 포함 된 IIS 7의 버전을 작업 하는 경우 영향을 주는 새 웹 사이트 프로젝트에 대 한 템플릿 변경 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="11205-516">This is not a change to ASP.NET as such, but a change in templates for new website projects that can affect you if you are working a version of IIS 7 that has not had the SP1 update applied.</span></span>

<span data-ttu-id="11205-517">ASP.NET에서 라우팅을 지원 하기 위해 응용 프로그램에 다음 구성 설정을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-517">In ASP.NET, you can add the following configuration setting to applications in order to support routing:</span></span>

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

<span data-ttu-id="11205-518">때 **runAllManagedModulesForAllRequests** 과 같은 URL true는 `http://mysite/myapp/home` 있다 하더라도 ASP.NET에서 이동 없습니다 *.aspx*, *.mvc*, 또는 유사한 확장에는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-518">When **runAllManagedModulesForAllRequests** is true, a URL like `http://mysite/myapp/home` goes to ASP.NET, even though there is no *.aspx*, *.mvc*, or similar extension on the URL.</span></span>

<span data-ttu-id="11205-519">IIS 7 하려고 하는 업데이트 하면 합니다 **runAllManagedModulesForAllRequests** 불필요 한을 설정 하 고 ASP.NET 라우팅은 고유 하 게 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-519">An update that was made to IIS 7 makes the **runAllManagedModulesForAllRequests** setting unnecessary and supports ASP.NET routing natively.</span></span> <span data-ttu-id="11205-520">(업데이트에 대 한 내용은 Microsoft 지원 문서를 참조 하세요 [업데이트를 사용할 수 있도록 특정 Url을 요청 하는 IIS 7.0 또는 IIS 7.5 처리기를 처리 하는 마침표로 끝나지 않는](https://support.microsoft.com/kb/980368).)</span><span class="sxs-lookup"><span data-stu-id="11205-520">(For information about the update, see the Microsoft Support article [An update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).)</span></span>

<span data-ttu-id="11205-521">웹 사이트는 IIS 7에서 실행 중인 경우 IIS가 업데이트 된 경우 설정 필요가 없습니다 **runAllManagedModulesForAllRequests** true로 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-521">If your website is running on IIS 7 and if IIS has been updated, you do not need to set **runAllManagedModulesForAllRequests** to true.</span></span> <span data-ttu-id="11205-522">사실, true로 설정 권장 되지 않습니다, 불필요 한 처리 오버 헤드가 요청에 추가 하기 때문에.</span><span class="sxs-lookup"><span data-stu-id="11205-522">In fact, setting it to true is not recommended, because it adds unnecessary processing overhead to request.</span></span> <span data-ttu-id="11205-523">이 설정은 참인 경우, 모든 요청을 비롯 한 *.htm*, *.jpg*, 기타 정적 파일에도 ASP.NET 요청 파이프라인을 통해 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-523">When this setting is true, all requests, including those for *.htm*, *.jpg*, and other static files, also go through the ASP.NET request pipeline.</span></span>

<span data-ttu-id="11205-524">Visual Studio 2012 RC에서 제공 되는 템플릿을 사용 하 여 새 ASP.NET 4.5 웹 사이트를 만들 경우 웹 사이트에 대 한 구성을 포함 하지 않습니다 합니다 **runAllManagedModulesForAllRequests** 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-524">If you create a new ASP.NET 4.5 website using the templates that are provided in Visual Studio 2012 RC, the configuration for the website does not include the **runAllManagedModulesForAllRequests** setting.</span></span> <span data-ttu-id="11205-525">즉 기본적으로 설정을 false입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-525">This means that by default the setting is false.</span></span>

<span data-ttu-id="11205-526">실행 하면 웹 사이트에서 Windows 7 SP1이 설치 되지 않은, IIS 7에 필요한 업데이트를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-526">If you then run the website on Windows 7 without SP1 installed, IIS 7 will not include the required update.</span></span> <span data-ttu-id="11205-527">결과적으로 라우팅이 작동 하지 않습니다 하 고 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-527">As a consequence, routing will not work and you will see errors.</span></span> <span data-ttu-id="11205-528">문제가 발생 하면 여기서 라우팅이 작동 하지 않습니다, 경우 다음 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-528">If you have a problem where routing does not work, you can do either the following:</span></span>

- <span data-ttu-id="11205-529">IIS 7로 업데이트를 추가 하는 sp1, Windows 7을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-529">Update Windows 7 to SP1, which will add the update to IIS 7.</span></span>
- <span data-ttu-id="11205-530">이전에 나열 된 Microsoft 지원 문서에 설명 된 업데이트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-530">Install the update that's described in the Microsoft Support article listed previously.</span></span>
- <span data-ttu-id="11205-531">설정할 **runAllManagedModulesForAllRequests** 해당 웹 사이트의 Web.config 파일에 true로 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-531">Set **runAllManagedModulesForAllRequests** to true in that website's Web.config file.</span></span> <span data-ttu-id="11205-532">요청에 약간의 오버 헤드를 추가 합니다이 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-532">Note that this will add some overhead to requests.</span></span>

<a id="_Toc318097397"></a>
### <a name="html-editor"></a><span data-ttu-id="11205-533">HTML 편집기</span><span class="sxs-lookup"><span data-stu-id="11205-533">HTML Editor</span></span>

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a><span data-ttu-id="11205-534">스마트 작업</span><span class="sxs-lookup"><span data-stu-id="11205-534">Smart Tasks</span></span>

<span data-ttu-id="11205-535">디자인 뷰에서 종종 서버 컨트롤의 복잡 한 속성 대화 상자 및 마법사 쉽게 설정할 수 있도록 연결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-535">In Design view, complex properties of server controls often have associated dialog boxes and wizards to make it easy to set them.</span></span> <span data-ttu-id="11205-536">데이터 소스를 추가 하려면 특별 한 대화 상자를 사용할 수는 예를 들어를 *반복기* 제어 하거나 열을 추가 하는 *GridView* 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-536">For example, you can use a special dialog box to add a data source to a *Repeater* control or add columns to a *GridView* control.</span></span>

<span data-ttu-id="11205-537">그러나이 유형의 복잡 한 속성에 대 한 UI 도움말 소스 뷰에서 사용할 수 있는 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-537">However, this type of UI help for complex properties has not been available in Source view.</span></span> <span data-ttu-id="11205-538">따라서 Visual Studio 11 원본 뷰에 대 한 스마트 작업을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-538">Therefore, Visual Studio 11 introduces Smart Tasks for Source view.</span></span> <span data-ttu-id="11205-539">스마트 작업은 C# 및 Visual Basic 편집기에서 자주 사용 되는 기능에 대 한 컨텍스트 인식 바로 가기입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-539">Smart Tasks are context-aware shortcuts for commonly used features in the C# and Visual Basic editors.</span></span>

<span data-ttu-id="11205-540">ASP.NET Web Forms 컨트롤에 대 한 스마트 작업 나타나나요 서버 태그 작은 문자 모양으로 요소 안에 삽입 지점이 있을 경우:</span><span class="sxs-lookup"><span data-stu-id="11205-540">For ASP.NET Web Forms controls, Smart Tasks appear on server tags as a small glyph when the insertion point is inside the element:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

<span data-ttu-id="11205-541">스마트 작업 문자 모양을 클릭 하거나 CTRL +를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-541">The Smart Task expands when you click the glyph or press CTRL+.</span></span> <span data-ttu-id="11205-542">(점), 코드 편집기와 마찬가지로 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-542">(dot), just as in the code editors.</span></span> <span data-ttu-id="11205-543">디자인 뷰의 스마트 작업과 유사한 된 바로 가기 키를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-543">It then displays shortcuts that are similar to the Smart Tasks in Design view.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

<span data-ttu-id="11205-544">예를 들어 앞의 그림에 스마트 태그는 GridView 작업 옵션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="11205-544">For example, the Smart Task in the previous illustration shows the GridView Tasks options.</span></span> <span data-ttu-id="11205-545">열 편집을 선택 하면 다음 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-545">If you choose Edit Columns, the following dialog box is displayed:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

<span data-ttu-id="11205-546">대화 상자 집합의 동일한 속성을 채우는 디자인 보기에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-546">Filling in the dialog box sets the same properties you can set in Design view.</span></span> <span data-ttu-id="11205-547">확인을 클릭 하면 태그 컨트롤에 대 한 새 설정으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-547">When you click OK, the markup for the control is updated with the new settings:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a><span data-ttu-id="11205-548">WAI ARIA 지원</span><span class="sxs-lookup"><span data-stu-id="11205-548">WAI-ARIA support</span></span>

<span data-ttu-id="11205-549">액세스할 수 있는 웹 사이트 작성 점점 더 중요 해지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-549">Writing accessible websites is becoming increasingly important.</span></span> <span data-ttu-id="11205-550">합니다 [WAI ARIA 내게 필요한 옵션 표준](http://www.w3.org/WAI/intro/aria) 개발자가 액세스할 수 있는 웹 사이트를 작성 해야 하는 방법을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-550">The [WAI-ARIA accessibility standard](http://www.w3.org/WAI/intro/aria) defines how developers should write accessible websites.</span></span> <span data-ttu-id="11205-551">이제이 표준 Visual Studio에서 완전히 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-551">This standard is now fully supported in Visual Studio.</span></span>

<span data-ttu-id="11205-552">예를 들어 합니다 *역할* 특성에는 이제 완전 한 IntelliSense에:</span><span class="sxs-lookup"><span data-stu-id="11205-552">For example, the *role* attribute now has full IntelliSense:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

<span data-ttu-id="11205-553">WAI ARIA 표준 폴더도 접두사로 사용 하는 특성 *aria-* 데 사용 되는 HTML5 문서에 의미 체계를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-553">The WAI-ARIA standard also introduces attributes that are prefixed with *aria-* that let you add semantics to an HTML5 document.</span></span> <span data-ttu-id="11205-554">Visual Studio에 이러한 항목을 완벽 하 게 지원 *aria-* 특성:</span><span class="sxs-lookup"><span data-stu-id="11205-554">Visual Studio also fully supports these *aria-* attributes:</span></span>

<span data-ttu-id="11205-555">![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="11205-555">![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)</span></span>

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a><span data-ttu-id="11205-556">새 HTML5 조각</span><span class="sxs-lookup"><span data-stu-id="11205-556">New HTML5 snippets</span></span>

<span data-ttu-id="11205-557">빠르고 쉽게 자주 사용 되는 HTML5 태그를 작성할 수 있도록, 하려면 Visual Studio 코드 조각 수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-557">To make it faster and easier to write commonly used HTML5 markup, Visual Studio includes a number of snippets.</span></span> <span data-ttu-id="11205-558">예로 비디오 조각:</span><span class="sxs-lookup"><span data-stu-id="11205-558">An example is the video snippet:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

<span data-ttu-id="11205-559">코드 조각으로 호출 하려면 IntelliSense에서 요소를 선택 하는 경우에 두 번 tab 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="11205-559">To invoke the snippet, press Tab twice when the element is selected in IntelliSense:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

<span data-ttu-id="11205-560">사용자 지정할 수 있는 코드 조각을 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-560">This produces a snippet that you can customize.</span></span>

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a><span data-ttu-id="11205-561">사용자 정의 컨트롤로 추출</span><span class="sxs-lookup"><span data-stu-id="11205-561">Extract to user control</span></span>

<span data-ttu-id="11205-562">큰 웹 페이지에서 개별 조각을 사용자 정의 컨트롤로 이동 하는 것이 좋습니다 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-562">In large web pages, it can be a good idea to move individual pieces into user controls.</span></span> <span data-ttu-id="11205-563">이러한 형태의 리팩터링 페이지의 가독성을 높일 수 있습니다 및 페이지 구조를 간소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-563">This form of refactoring can help increase the readability of the page and can simplify the page structure.</span></span>

<span data-ttu-id="11205-564">쉽게 하기 위해이 소스 뷰에서 Web Forms 페이지를 편집할 때, 이제는 페이지에서 텍스트를 선택, 마우스 오른쪽 단추로 클릭 하 수 선택한 다음 사용자 정의 컨트롤로 추출:</span><span class="sxs-lookup"><span data-stu-id="11205-564">To make this easier, when you edit Web Forms pages in Source view, you can now select text in a page, right-click it, and then choose Extract to User Control:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a><span data-ttu-id="11205-565">코드 너 깃 특성에서에 대 한 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="11205-565">IntelliSense for code nuggets in attributes</span></span>

<span data-ttu-id="11205-566">Visual Studio는 항상 모든 페이지 또는 컨트롤에서 서버 쪽 코드 너 깃에 대 한 IntelliSense를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-566">Visual Studio has always provided IntelliSense for server-side code nuggets in any page or control.</span></span> <span data-ttu-id="11205-567">이제 Visual Studio에서 HTML 특성에도 코드 너 깃에 대 한 IntelliSense를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-567">Now Visual Studio includes IntelliSense for code nuggets in HTML attributes as well.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

<span data-ttu-id="11205-568">이렇게 하면 쉽게 데이터 바인딩 식을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-568">This makes it easier to create data-binding expressions:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a><span data-ttu-id="11205-569">태그 또는 닫는 태그 이름을 바꾸는 경우 일치 하는 태그의 자동 이름 바꾸기</span><span class="sxs-lookup"><span data-stu-id="11205-569">Automatic renaming of matching tag when you rename an opening or closing tag</span></span>

<span data-ttu-id="11205-570">HTML 요소의 이름을 바꾸면 (변경 하는 예를 들어를 *div* 사용할 태그입니다는 *헤더* 태그), 해당 열거나 닫는 태그도 실시간으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-570">If you rename an HTML element (for example, you change a *div* tag to be a *header* tag), the corresponding opening or closing tag also changes in real time.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

<span data-ttu-id="11205-571">이 닫는 태그를 변경 하거나 잘못 된 것을 변경 하려면 잊은 오류를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-571">This helps avoid the error where you forget to change a closing tag or change the wrong one.</span></span>

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a><span data-ttu-id="11205-572">이벤트 처리기 생성</span><span class="sxs-lookup"><span data-stu-id="11205-572">Event handler generation</span></span>

<span data-ttu-id="11205-573">이제 visual Studio는 소스 뷰의 이벤트 처리기를 작성 하 고 수동으로 바인딩할 수 있도록 기능이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-573">Visual Studio now includes features in Source view to help you write event handlers and bind them manually.</span></span> <span data-ttu-id="11205-574">소스 뷰에서 이벤트 이름을 편집 하는 경우 IntelliSense에 표시 됩니다 &lt;새 이벤트 만들기&gt;에 올바른 서명이 만드는 이벤트 처리기는 페이지의 코드는:</span><span class="sxs-lookup"><span data-stu-id="11205-574">If you are editing an event name in Source view, IntelliSense displays &lt;Create New Event&gt;, which will create an event handler in the page's code that has the right signature:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

<span data-ttu-id="11205-575">기본적으로 이벤트 처리기는 이벤트 처리 메서드 이름에 대 한 컨트롤의 ID을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-575">By default, the event handler will use the control's ID for the name of the event-handling method:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

<span data-ttu-id="11205-576">결과 이벤트 처리기 (이 경우에 C#)이 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-576">The resulting event handler will look like this (in this case, in C#):</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a><span data-ttu-id="11205-577">스마트 들여쓰기</span><span class="sxs-lookup"><span data-stu-id="11205-577">Smart indent</span></span>

<span data-ttu-id="11205-578">빈 HTML 요소 내부에 있는 동안 Enter를 누르면 편집기 적절 한 위치에 커서를 둡니다 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-578">When you press Enter while inside an empty HTML element, the editor will put the insertion point in the right place:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

<span data-ttu-id="11205-579">Enter 키를 눌러이 위치에서 닫는 태그의 아래로 이동할 이며이 여는 태그와 일치 하도록 들여씁니다.</span><span class="sxs-lookup"><span data-stu-id="11205-579">If you press Enter in this location, the closing tag is moved down and indented to match the opening tag.</span></span> <span data-ttu-id="11205-580">삽입 지점 또한 들여쓰기 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-580">The insertion point is also indented:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a><span data-ttu-id="11205-581">문 자동 줄임 완성</span><span class="sxs-lookup"><span data-stu-id="11205-581">Auto-reduce statement completion</span></span>

<span data-ttu-id="11205-582">IntelliSense 목록만 관련 옵션 표시 유형을 기반으로 하는 Visual Studio 현재 필터:</span><span class="sxs-lookup"><span data-stu-id="11205-582">The IntelliSense list in Visual Studio now filters based on what you type so that it displays only relevant options:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

<span data-ttu-id="11205-583">또한 IntelliSense 목록에는 개별 단어 제목 대/소문자에 따라 필터링 된 IntelliSense 기능.</span><span class="sxs-lookup"><span data-stu-id="11205-583">IntelliSense also filters based on the title case of the individual words in the IntelliSense list.</span></span> <span data-ttu-id="11205-584">예를 들어, "dl"를 입력 하면 dl 및 asp DataList를 모두 표시 됩니다.:</span><span class="sxs-lookup"><span data-stu-id="11205-584">For example, if you type "dl", both dl and asp:DataList are displayed:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

<span data-ttu-id="11205-585">이 기능을 사용 하면 더 빠르게 알려진된 요소에 대 한 문 완성을 가져오려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-585">This feature makes it faster to get statement completion for known elements.</span></span>

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a><span data-ttu-id="11205-586">JavaScript 편집기</span><span class="sxs-lookup"><span data-stu-id="11205-586">JavaScript Editor</span></span>

<span data-ttu-id="11205-587">Visual Studio 2012 Release Candidate의 JavaScript 편집기는 완전히 새로운 이며 Visual Studio에서 JavaScript를 사용 하는 환경을 크게 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-587">The JavaScript editor in Visual Studio 2012 Release Candidate is completely new and it greatly improves the experience of working with JavaScript in Visual Studio.</span></span>

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a><span data-ttu-id="11205-588">코드 개요</span><span class="sxs-lookup"><span data-stu-id="11205-588">Code outlining</span></span>

<span data-ttu-id="11205-589">이제 개요 영역 파일의 현재 포커스와 관련이 없는 파트를 축소할 수 있도록 하는 모든 함수에 대해 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-589">Outlining regions are now automatically created for all functions, allowing you to collapse parts of the file that aren't pertinent to your current focus.</span></span>

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a><span data-ttu-id="11205-590">중괄호 일치</span><span class="sxs-lookup"><span data-stu-id="11205-590">Brace matching</span></span>

<span data-ttu-id="11205-591">태그 또는 닫는 중괄호에 삽입점을 배치 하면 일치 하는 것 편집기에서 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-591">When you put the insertion point on an opening or closing brace, the editor highlights the matching one.</span></span>

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a><span data-ttu-id="11205-592">정의로 이동</span><span class="sxs-lookup"><span data-stu-id="11205-592">Go to Definition</span></span>

<span data-ttu-id="11205-593">로 이동 명령 정의 사용 하면 함수 또는 변수에 대 한 소스로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-593">The Go to Definition command lets you jump to the source for a function or variable.</span></span>

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a><span data-ttu-id="11205-594">ECMAScript5 지원</span><span class="sxs-lookup"><span data-stu-id="11205-594">ECMAScript5 support</span></span>

<span data-ttu-id="11205-595">편집기는 ECMAScript5, JavaScript 언어를 설명 하는 표준의 최신 버전의에서 새 구문 및 Api를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-595">The editor supports the new syntax and APIs in ECMAScript5, the latest version of the standard that describes the JavaScript language.</span></span>

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a><span data-ttu-id="11205-596">DOM IntelliSense</span><span class="sxs-lookup"><span data-stu-id="11205-596">DOM IntelliSense</span></span>

<span data-ttu-id="11205-597">DOM Api에 대 한 IntelliSense 향상 되었습니다 비롯 한 많은 새 HTML5 Api에 대 한 지원과 *querySelector*, DOM 저장소, 문서 간 메시징, 및 *캔버스*합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-597">IntelliSense for DOM APIs has been improved, with support for many new HTML5 APIs including *querySelector*, DOM Storage, cross-document messaging, and *canvas*.</span></span> <span data-ttu-id="11205-598">DOM IntelliSense는 이제 단일 간단한 JavaScript 파일이 아닌 네이티브 형식 라이브러리 정의 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-598">DOM IntelliSense is now driven by a single simple JavaScript file, rather than by a native type library definition.</span></span> <span data-ttu-id="11205-599">이렇게 하면 쉽게 확장 하거나 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-599">This makes it easy to extend or replace.</span></span>

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a><span data-ttu-id="11205-600">VSDOC 서명이 오버 로드</span><span class="sxs-lookup"><span data-stu-id="11205-600">VSDOC signature overloads</span></span>

<span data-ttu-id="11205-601">자세한 IntelliSense 주석을 이제 선언할 수 있습니다 JavaScript 함수는 별도 오버 로드에 대 한 새 *&lt;서명을&gt;* 이 예와 같이 요소:</span><span class="sxs-lookup"><span data-stu-id="11205-601">Detailed IntelliSense comments can now be declared for separate overloads of JavaScript functions by using the new *&lt;signature&gt;* element, as shown in this example:</span></span>

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a><span data-ttu-id="11205-602">암시적 참조</span><span class="sxs-lookup"><span data-stu-id="11205-602">Implicit references</span></span>

<span data-ttu-id="11205-603">이제 암시적으로 포함 될 파일 목록에서 지정 된 JavaScript 블록 또는 파일 참조가 것을 의미 하므로 그 내용에 대해 IntelliSense를 얻게는 중앙 목록에 JavaScript 파일을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-603">You can now add JavaScript files to a central list that will be implicitly included in the list of files that any given JavaScript file or block references, meaning you'll get IntelliSense for its contents.</span></span> <span data-ttu-id="11205-604">예를 들어 파일의 중앙 목록에 jQuery 파일을 추가할 수 있습니다 및 얻게 IntelliSense jQuery 함수에 대 한 파일의 모든 JavaScript 블록에 명시적으로 참조 한 여부 (사용 하 여 / / / &lt;참조 /&gt;) 여부.</span><span class="sxs-lookup"><span data-stu-id="11205-604">For example, you can add jQuery files to the central list of files, and you'll get IntelliSense for jQuery functions in any JavaScript block of file, whether you've referenced it explicitly (using /// &lt;reference /&gt;) or not.</span></span>

<a id="_Toc318097415"></a>
### <a name="css-editor"></a><span data-ttu-id="11205-605">CSS 편집기</span><span class="sxs-lookup"><span data-stu-id="11205-605">CSS Editor</span></span>

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a><span data-ttu-id="11205-606">문 자동 줄임 완성</span><span class="sxs-lookup"><span data-stu-id="11205-606">Auto-reduce statement completion</span></span>

<span data-ttu-id="11205-607">CSS 속성을 기반으로 하는 CSS 이제 필터 및 선택한 스키마에 의해 지원 되는 값에 대 한 IntelliSense 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-607">The IntelliSense list for CSS now filters based on the CSS properties and values supported by the selected schema.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

<span data-ttu-id="11205-608">IntelliSense에는 제목 사례 검색을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-608">IntelliSense also supports title case searches:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a><span data-ttu-id="11205-609">계층적 들여쓰기</span><span class="sxs-lookup"><span data-stu-id="11205-609">Hierarchical indentation</span></span>

<span data-ttu-id="11205-610">CSS 편집기를 사용 하 여 들여쓰기 계층 규칙을 표시 계단식 규칙이 논리적으로 구성 되는 방법과 개요를 제공 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-610">The CSS editor uses indentation to display hierarchical rules, which gives you an overview of how the cascading rules are logically organized.</span></span> <span data-ttu-id="11205-611">다음 예제에서는 #list 선택기를 목록의 연계 자식 이며 따라서 들여쓰기 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-611">In the following example, the #list a selector is a cascading child of list and is therefore indented.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

<span data-ttu-id="11205-612">다음 예제에서는 보다 복잡 한 상속을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="11205-612">The following example shows more complex inheritance:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

<span data-ttu-id="11205-613">규칙의 들여쓰기는 부모 규칙에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-613">The indentation of a rule is determined by its parent rules.</span></span> <span data-ttu-id="11205-614">계층적 들여쓰기는 기본적으로 활성화 되어 있지만 옵션 대화 상자 (도구, 메뉴 모음에서 옵션)을 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-614">Hierarchical indentation is enabled by default, but you can disable it the Options dialog box (Tools, Options from the menu bar):</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a><span data-ttu-id="11205-615">CSS 해킹 지원</span><span class="sxs-lookup"><span data-stu-id="11205-615">CSS hacks support</span></span>

<span data-ttu-id="11205-616">수백 개의 실제 CSS 파일의 분석 CSS 해킹은 매우 일반적인을 이제 Visual Studio 지원 가장 널리 사용 되는 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="11205-616">Analysis of hundreds of real-world CSS files shows that CSS hacks are very common, and now Visual Studio supports the most widely used ones.</span></span> <span data-ttu-id="11205-617">IntelliSense 및 유효성 검사 별 포함 됩니다 (\*) 및 밑줄 (\_) 속성 해킹:</span><span class="sxs-lookup"><span data-stu-id="11205-617">This support includes IntelliSense and validation of the star (\*) and underscore (\_) property hacks:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

<span data-ttu-id="11205-618">일반적인 선택기 해킹 적용 되는 경우에 계층적 들여쓰기 유지 되도록 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-618">Typical selector hacks are also supported so that hierarchical indentation is maintained even when they are applied.</span></span> <span data-ttu-id="11205-619">Internet Explorer 7 대상 하는 데 사용 하는 일반적인 선택기 hack 선택기를 사용 하 여 앞에 추가 하는 것  *\*: 첫 번째 자식 + html*합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-619">A typical selector hack used to target Internet Explorer 7 is to prepend a selector with *\*:first-child + html*.</span></span> <span data-ttu-id="11205-620">해당 규칙을 사용 하 여 계층적 들여쓰기를 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-620">Using that rule will maintain the hierarchical indentation:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a><span data-ttu-id="11205-621">공급 업체 특정 스키마 (-설정--webkit)</span><span class="sxs-lookup"><span data-stu-id="11205-621">Vendor specific schemas (-moz-, -webkit)</span></span>

<span data-ttu-id="11205-622">CSS3 서로 다른 시간에 다른 브라우저에서 구현 된 많은 속성을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-622">CSS3 introduces many properties that have been implemented by different browsers at different times.</span></span> <span data-ttu-id="11205-623">이 이전에 공급 업체 특정 구문을 사용 하 여 개발자가 특정 브라우저에 대 한 코드를을 강제 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-623">This previously forced developers to code for specific browsers by using vendor-specific syntax.</span></span> <span data-ttu-id="11205-624">이러한 브라우저 전용 속성은 이제 IntelliSense에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-624">These browser-specific properties are now included in IntelliSense.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a><span data-ttu-id="11205-625">주석 처리 및 주석 처리 제거 지원</span><span class="sxs-lookup"><span data-stu-id="11205-625">Commenting and uncommenting support</span></span>

<span data-ttu-id="11205-626">이제 주석 처리 하 고 코드 편집기 (Ctrl + K, 주석에 C 및 Ctrl + K, 주석 처리를 제거 하)에서 사용 하는 동일한 바로 가기 키를 사용 하 여 CSS 규칙을 주석 처리 제거 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-626">You can now comment and uncomment CSS rules using the same shortcuts that you use in the code editor (Ctrl+K,C to comment and Ctrl+K,U to uncomment).</span></span>

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a><span data-ttu-id="11205-627">색 선택</span><span class="sxs-lookup"><span data-stu-id="11205-627">Color picker</span></span>

<span data-ttu-id="11205-628">Visual Studio의 이전 버전에서는 색 관련 특성에 대 한 IntelliSense 명명 된 색 값의 드롭다운 목록으로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-628">In previous versions of Visual Studio, IntelliSense for color-related attributes consisted of a drop-down list of named color values.</span></span> <span data-ttu-id="11205-629">해당 목록에 모든 기능을 갖춘 색 선택 하 여 대체 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-629">That list has been replaced by a full-featured color picker.</span></span>

<span data-ttu-id="11205-630">색 값을 입력 하면 색 선택은 자동으로 표시 됩니다 하 고 뒤에 기본 색 색상표를 이전에 사용 되는 색 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-630">When you enter a color value, the color picker is displayed automatically and presents a list of previously used colors followed by a default color palette.</span></span> <span data-ttu-id="11205-631">마우스나 키보드를 사용 하 여 색을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-631">You can select a color using the mouse or the keyboard.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

<span data-ttu-id="11205-632">목록 전체 색 선택기를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-632">The list can be expanded into a complete color picker.</span></span> <span data-ttu-id="11205-633">선택기는 불투명도 슬라이더를 이동 하면 RGBA를 색을 자동으로 변환 하 여 알파 채널을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-633">The picker lets you control the alpha channel by automatically converting any color into RGBA when you move the opacity slider:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a><span data-ttu-id="11205-634">코드 조각</span><span class="sxs-lookup"><span data-stu-id="11205-634">Snippets</span></span>

<span data-ttu-id="11205-635">CSS 편집기에서 코드 조각을 사용 하면 쉽고 빠르게 브라우저 간 스타일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-635">Snippets in the CSS editor make it easier and faster to create cross-browser styles.</span></span> <span data-ttu-id="11205-636">브라우저별 설정 해야 하는 많은 CSS3 속성 내용이 이제 조각에 롤백 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-636">Many CSS3 properties that require browser-specific settings have now been rolled into snippets.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

<span data-ttu-id="11205-637">CSS 코드 조각에서 기호를 입력 하 여 고급 시나리오 (예: CSS3 미디어 쿼리)를 지원 합니다 (@), IntelliSense 목록 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="11205-637">CSS snippets support advanced scenarios (like CSS3 media queries) by typing the at-symbol (@), which shows the IntelliSense list.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

<span data-ttu-id="11205-638">선택 하면 @media 값 및 키를 눌러, CSS 편집기에 다음 코드 조각 삽입:</span><span class="sxs-lookup"><span data-stu-id="11205-638">When you select @media value and press Tab, the CSS editor inserts the following snippet:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

<span data-ttu-id="11205-639">코드 조각에서와 같이 사용자 고유의 CSS 코드 조각을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-639">As with snippets for code, you can create your own CSS snippets.</span></span>

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a><span data-ttu-id="11205-640">사용자 지정 영역</span><span class="sxs-lookup"><span data-stu-id="11205-640">Custom regions</span></span>

<span data-ttu-id="11205-641">이미 사용할 수 있는 코드 편집기에서 코드 영역을 명명 된 CSS 편집을 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-641">Named code regions, which are already available in the code editor, are now available for CSS editing.</span></span> <span data-ttu-id="11205-642">이 관련된 스타일 요소를 쉽게 그룹화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-642">This lets you easily group related style blocks.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

<span data-ttu-id="11205-643">영역 축소 된 영역의 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-643">When a region is collapsed it displays the name of the region:</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a><span data-ttu-id="11205-644">페이지 검사기</span><span class="sxs-lookup"><span data-stu-id="11205-644">Page Inspector</span></span>

<span data-ttu-id="11205-645">페이지 검사기는 도구는 Visual Studio IDE에서 웹 페이지 (HTML, Web Forms, ASP.NET MVC 또는 웹 페이지)를 렌더링 하 고 소스 코드 및 결과 출력을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-645">Page Inspector is a tool that renders a web page (HTML, Web Forms, ASP.NET MVC, or Web Pages) in the Visual Studio IDE and lets you examine both the source code and the resulting output.</span></span> <span data-ttu-id="11205-646">페이지 검사기는 ASP.NET 페이지에 대 한 브라우저에 렌더링 되는 HTML 태그를 생성 한 서버 쪽 코드를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-646">For ASP.NET pages, Page Inspector lets you determine which server-side code has produced the HTML markup that is rendered to the browser.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

<span data-ttu-id="11205-647">페이지 검사기에 대 한 자세한 내용은 다음 자습서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="11205-647">For more information about Page Inspector, please see the following tutorials:</span></span>

- <span data-ttu-id="11205-648">페이지 검사기를 사용 하 여 [ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)</span><span class="sxs-lookup"><span data-stu-id="11205-648">Using Page Inspector in [ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)</span></span>
- <span data-ttu-id="11205-649">페이지 검사기를 사용 하 여 [ASP.NET Web Forms](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)</span><span class="sxs-lookup"><span data-stu-id="11205-649">Using Page Inspector in [ASP.NET Web Forms](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)</span></span>

<a id="_Toc318097425"></a>
### <a name="publishing"></a><span data-ttu-id="11205-650">게시</span><span class="sxs-lookup"><span data-stu-id="11205-650">Publishing</span></span>

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a><span data-ttu-id="11205-651">게시 프로필</span><span class="sxs-lookup"><span data-stu-id="11205-651">Publish profiles</span></span>

<span data-ttu-id="11205-652">Visual Studio 2010에서 웹 응용 프로그램 프로젝트에 대 한 정보를 게시 하는 버전 제어에 저장 되지 않습니다 되며 다른 사용자와 공유 하는 것에 대 한 설계 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-652">In Visual Studio 2010, publishing information for Web application projects is not stored in version control and is not designed for sharing with others.</span></span> <span data-ttu-id="11205-653">Visual Studio 2012 Release Candidate에서 게시 프로필의 형식을 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-653">In Visual Studio 2012 Release Candidate, the format of the publish profile has been changed.</span></span> <span data-ttu-id="11205-654">팀 아티팩트에 대 한 및 MSBuild를 기반으로 빌드에서 활용 하 여 이제 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-654">It has been made a team artifact, and it is now easy to leverage from builds based on MSBuild.</span></span> <span data-ttu-id="11205-655">빌드 구성 정보는 게시 대화 상자에서 되므로 게시 하기 전에 빌드 구성을 쉽게 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-655">Build configuration information is in the Publish dialog box so that you can easily switch build configurations before publishing.</span></span>

<span data-ttu-id="11205-656">게시 프로필 PublishProfiles 폴더에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-656">Publish profiles are stored in the PublishProfiles folder.</span></span> <span data-ttu-id="11205-657">폴더의 위치에 따라 달라 집니다 사용 중인 프로그래밍 언어에:</span><span class="sxs-lookup"><span data-stu-id="11205-657">The location of the folder depends on what programming language you are using:</span></span>

- <span data-ttu-id="11205-658">C#: Properties\PublishProfiles</span><span class="sxs-lookup"><span data-stu-id="11205-658">C#: Properties\PublishProfiles</span></span>
- <span data-ttu-id="11205-659">Visual Basic: Project\PublishProfiles</span><span class="sxs-lookup"><span data-stu-id="11205-659">Visual Basic: My Project\PublishProfiles</span></span>

<span data-ttu-id="11205-660">각 프로필은 MSBuild 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-660">Each profile is an MSBuild file.</span></span> <span data-ttu-id="11205-661">게시 중 프로젝트의 MSBuild 파일에이 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="11205-661">During publishing, this file is imported into the project's MSBuild file.</span></span> <span data-ttu-id="11205-662">Visual Studio 2010에 게시 또는 패키지 프로세스를 변경 하려는 경우 라는 파일에 사용자 지정 항목을 삽입할 **ProjectName**. wpp.targets 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-662">In Visual Studio 2010, if you want to make changes to the publish or package process, you have to put your customizations in a file named **ProjectName**.wpp.targets.</span></span> <span data-ttu-id="11205-663">이 계속 지원 되지만 게시 프로필 자체에 이제 사용자 지정 항목을 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-663">This is still supported, but you can now put your customizations in the publish profile itself.</span></span> <span data-ttu-id="11205-664">이런 방식으로 사용자 지정 프로필에 대해서만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11205-664">That way, the customizations will be used only for that profile.</span></span>

<span data-ttu-id="11205-665">이제 활용 하 여 MSBuild에서 프로필을 게시할 수도 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-665">You can now also leverage publish profiles from MSBuild.</span></span> <span data-ttu-id="11205-666">이렇게 하려면 프로젝트를 빌드할 때 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-666">To do so, use the following command when you build the project:</span></span>

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

<span data-ttu-id="11205-667">Project.csproj 값은 프로젝트의 경로 이며, ProfileName 게시 프로필의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-667">The project.csproj value is the path of the project, and ProfileName is the name of the profile to publish.</span></span> <span data-ttu-id="11205-668">프로필 이름을 전달 하는 대신에 또는 합니다 *PublishProfile* 속성을 전달할 수의 전체 경로에서 게시 프로필.</span><span class="sxs-lookup"><span data-stu-id="11205-668">Alternatively, instead of passing the profile name for the *PublishProfile* property, you can pass in the full path to the publish profile.</span></span>

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a><span data-ttu-id="11205-669">ASP.NET 미리 컴파일 및 병합</span><span class="sxs-lookup"><span data-stu-id="11205-669">ASP.NET precompilation and merge</span></span>

<span data-ttu-id="11205-670">웹 응용 프로그램 프로젝트에 대 한 Visual Studio 2012 Release Candidate 미리 컴파일을 하 고 사이트의 콘텐츠를 게시할 때 또는 프로젝트 패키지 병합 수 있도록 웹 패키지 및 게시 속성 페이지에서 옵션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-670">For Web application projects, Visual Studio 2012 Release Candidate adds an option on the Package/Publish Web properties page that lets you precompile and merge your site's content when you publish or package the project.</span></span> <span data-ttu-id="11205-671">이러한 옵션을 보려면 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 속성을 선택한 다음 웹 패키지 및 게시 속성 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-671">To see these options, right-click the project in Solution Explorer, choose Properties, and then choose the Package/Publish Web property page.</span></span> <span data-ttu-id="11205-672">다음 그림은 미리 컴파일 옵션을 게시 하기 전에이 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="11205-672">The following illustration shows the Precompile this application before publishing option.</span></span>

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

<span data-ttu-id="11205-673">이 옵션을 선택 하면 Visual Studio를 게시할 때마다 응용 프로그램 또는 웹 응용 프로그램 패키지를 미리 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-673">When this option is selected, Visual Studio precompiles the application whenever you publish or package the web application.</span></span> <span data-ttu-id="11205-674">사이트 미리 컴파일 되었는지 어떻게 또는 어셈블리 병합 되는 방법을 제어 하려는 경우 해당 옵션을 구성 하려면 고급 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-674">If you want to control how the site is precompiled or how assemblies are merged, click the Advanced button to configure those options.</span></span>

<a id="_Toc318097428"></a>
### <a name="iis-express"></a><span data-ttu-id="11205-675">IIS Express</span><span class="sxs-lookup"><span data-stu-id="11205-675">IIS Express</span></span>

<span data-ttu-id="11205-676">Visual Studio에서 테스트 웹 프로젝트에 대 한 기본 웹 서버 IIS Express 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-676">The default web server for testing web projects in Visual Studio is now IIS Express.</span></span> <span data-ttu-id="11205-677">Visual Studio 개발 서버를 계속 개발 하는 동안 로컬 웹 서버에 대 한 옵션 이지만 IIS Express가 이제 권장 되는 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-677">The Visual Studio Development Server is still an option for local web server during development, but IIS Express is now the recommended server.</span></span> <span data-ttu-id="11205-678">Visual Studio 11 Beta의 IIS Express를 사용 하는 환경을 사용 하 여 Visual Studio 2010 sp1에서과 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-678">The experience of using IIS Express in Visual Studio 11 Beta is very similar to using it in Visual Studio 2010 SP1.</span></span>

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a><span data-ttu-id="11205-679">고지 사항</span><span class="sxs-lookup"><span data-stu-id="11205-679">Disclaimer</span></span>

<span data-ttu-id="11205-680">본 문서는 예비 문서이며, 여기에 설명한 소프트웨어의 최종 상업적 출시 전에 크게 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-680">This is a preliminary document and may be changed substantially prior to final commercial release of the software described herein.</span></span>

<span data-ttu-id="11205-681">이 문서에 포함된 정보는 게시 날짜 현재 논의된 문제에 대한 Microsoft Corporation의 당시 관점을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="11205-681">The information contained in this document represents the current view of Microsoft Corporation on the issues discussed as of the date of publication.</span></span> <span data-ttu-id="11205-682">Microsoft는 변화하는 시장 상황에 부응해야 하므로, Microsoft의 일부에 대한 책임으로 해석되어서는 안되며, 게시 날짜 이후 소개된 정보의 정확성을 Microsoft가 보증할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-682">Because Microsoft must respond to changing market conditions, it should not be interpreted to be a commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented after the date of publication.</span></span>

<span data-ttu-id="11205-683">이 백서는 정보 제공만을 목적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-683">This White Paper is for informational purposes only.</span></span> <span data-ttu-id="11205-684">Microsoft는 이 문서에 있는 정보에 대한 명시적 또는 묵시적, 법적인 보증을 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-684">MICROSOFT MAKES NO WARRANTIES, EXPRESS, IMPLIED OR STATUTORY, AS TO THE INFORMATION IN THIS DOCUMENT.</span></span>

<span data-ttu-id="11205-685">해당 저작권법을 준수하는 것은 사용자의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-685">Complying with all applicable copyright laws is the responsibility of the user.</span></span> <span data-ttu-id="11205-686">저작권에서의 권리와는 별도로, 이 설명서의 어떠한 부분도 Microsoft의 명시적인 서면 승인 없이는 어떠한 형식이나 수단(전기적, 기계적, 복사기에 의한 복사, 디스크 복사 또는 다른 방법) 또는 목적으로도 복제되거나, 검색 시스템에 저장 또는 도입되거나, 전송될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-686">Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.</span></span>

<span data-ttu-id="11205-687">Microsoft가 이 설명서 본안에 관련된 특허권, 상표권, 저작권 또는 기타 지적 재산권 등을 보유할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-687">Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document.</span></span> <span data-ttu-id="11205-688">서면 사용권 계약에 따라 Microsoft로부터 귀하에게 명시적으로 제공된 권리 이외에, 이 문서의 제공은 귀하에게 이러한 특허권, 상표권, 저작권, 또는 기타 지적 소유권 등에 대한 어떠한 사용권도 허여하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-688">Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.</span></span>

<span data-ttu-id="11205-689">다른 언급이 없는 경우 예제 회사, 조직, 제품, 도메인 이름, 전자 메일 주소, 로고, 사람, 장소 및 이벤트 용례은 실제 데이터가 아닙니다 및 실제 회사, 조직, 제품, 도메인 이름, 전자 메일 연관 시킬 의도가 없으며 주소, 로고, 사람, 장소 또는 이벤트는 또는 유추 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="11205-689">Unless otherwise noted, the example companies, organizations, products, domain names, email addresses, logos, people, places and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, email address, logo, person, place or event is intended or should be inferred.</span></span>

<span data-ttu-id="11205-690">© 2012 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="11205-690">© 2012 Microsoft Corporation.</span></span> <span data-ttu-id="11205-691">All rights reserved.</span><span class="sxs-lookup"><span data-stu-id="11205-691">All rights reserved.</span></span>

<span data-ttu-id="11205-692">Microsoft 및 Windows는 미국 및/또는 기타 국가에서 Microsoft Corporation의 상표이거나 등록된 상표입니다.</span><span class="sxs-lookup"><span data-stu-id="11205-692">Microsoft and Windows are either registered trademarks or trademarks of Microsoft Corporation in the United States and/or other countries.</span></span>

<span data-ttu-id="11205-693">여기에 언급된 실제 회사와 제품의 이름은 각각 해당 소유자의 상표일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11205-693">The names of actual companies and products mentioned herein may be the trademarks of their respective owners.</span></span>
