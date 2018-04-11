---
uid: whitepapers/mvc3-release-notes
title: ASP.NET MVC 3 | Microsoft Docs
author: rick-anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/06/2010
ms.topic: article
ms.assetid: f44c166e-7e91-48a0-a6f8-d9285f3594e5
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /whitepapers/mvc3-release-notes
msc.type: content
ms.openlocfilehash: 0bfe9cdc215226457ccfafff2b85ace87325b91b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
---
<a name="aspnet-mvc-3"></a><span data-ttu-id="4ad3e-102">ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="4ad3e-102">ASP.NET MVC 3</span></span>
====================
- [<span data-ttu-id="4ad3e-103">개요</span><span class="sxs-lookup"><span data-stu-id="4ad3e-103">Overview</span></span>](#overview)
- [<span data-ttu-id="4ad3e-104">설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="4ad3e-104">Installation Notes</span></span>](#installation-notes)
- [<span data-ttu-id="4ad3e-105">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="4ad3e-105">Software Requirements</span></span>](#software-requirements)
- [<span data-ttu-id="4ad3e-106">문서</span><span class="sxs-lookup"><span data-stu-id="4ad3e-106">Documentation</span></span>](#documentation)
- [<span data-ttu-id="4ad3e-107">지원</span><span class="sxs-lookup"><span data-stu-id="4ad3e-107">Support</span></span>](#support)
- [<span data-ttu-id="4ad3e-108">ASP.NET MVC 2 프로젝트 업그레이드 하는 ASP.NET mvc 3 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="4ad3e-108">Upgrading an ASP.NET MVC 2 Project to ASP.NET MVC 3 Tools Update</span></span>](#upgrading)
- [<span data-ttu-id="4ad3e-109">ASP.NET MVC 3 도구 업데이트 (2011 년 4 월 12 일)</span><span class="sxs-lookup"><span data-stu-id="4ad3e-109">ASP.NET MVC 3 Tools Update (April 12, 2011)</span></span>](#tu-changes)

    - [<span data-ttu-id="4ad3e-110">"컨트롤러 추가" 대화 상자에 컨트롤러를 뷰 및 데이터 액세스 코드와 함께 스 캐 폴딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-110">"Add Controller" dialog box can now scaffold controllers with views and data access code</span></span>](#tu-AddControllerDialog)
    - [<span data-ttu-id="4ad3e-111">향상 된 기능에서 "ASP.NET MVC 3 새 프로젝트" 대화 상자</span><span class="sxs-lookup"><span data-stu-id="4ad3e-111">Improvements to the "ASP.NET MVC 3 New Project" Dialog Box</span></span>](#tu-ImprovementsNewDialogBox)
    - [<span data-ttu-id="4ad3e-112">프로젝트 템플릿에 Modernizr 1.7이 포함</span><span class="sxs-lookup"><span data-stu-id="4ad3e-112">Project templates now include Modernizr 1.7</span></span>](#tu-Modernizr)
    - [<span data-ttu-id="4ad3e-113">프로젝트 템플릿에 jQuery, jQuery UI 및 jQuery의 업데이트 된 버전이 포함 되어 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="4ad3e-113">Project templates include updated versions of jQuery, jQuery UI, and jQuery Validation</span></span>](#tu-UpdatedJQuery)
    - [<span data-ttu-id="4ad3e-114">프로젝트 템플릿에 이제 ADO.NET Entity Framework 4.1 사전 설치 NuGet 패키지로 포함</span><span class="sxs-lookup"><span data-stu-id="4ad3e-114">Project templates now include ADO.NET Entity Framework 4.1 as a pre-installed NuGet package</span></span>](#tu-EF)
    - [<span data-ttu-id="4ad3e-115">프로젝트 템플릿에 JavaScript 라이브러리를 사전 설치 된 NuGet 패키지로 포함</span><span class="sxs-lookup"><span data-stu-id="4ad3e-115">Project templates include JavaScript libraries as pre-installed NuGet packages</span></span>](#tu-JavaScriptLibsNuget)
    - [<span data-ttu-id="4ad3e-116">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="4ad3e-116">Known Issues</span></span>](#tu-KI)
- [<span data-ttu-id="4ad3e-117">ASP.NET MVC 3 RTM (2011 년 1 월 13 일)</span><span class="sxs-lookup"><span data-stu-id="4ad3e-117">ASP.NET MVC 3 RTM (January 13, 2011)</span></span>](#MVC3RTM)

    - [<span data-ttu-id="4ad3e-118">변경 사항: 1.8.7 버전의 jQuery UI 업데이트</span><span class="sxs-lookup"><span data-stu-id="4ad3e-118">Change: Updated the version of jQuery UI to 1.8.7</span></span>](#RTM-1)
    - [<span data-ttu-id="4ad3e-119">ModelMetadataProvider DataAnnotationsModelMetadataProvider로 다시 기본값을 변경 하는 변경 사항:</span><span class="sxs-lookup"><span data-stu-id="4ad3e-119">Change: Changed the default ModelMetadataProvider back to DataAnnotationsModelMetadataProvider</span></span>](#RTM-2)
    - [<span data-ttu-id="4ad3e-120">공백 결과 거꾸로를 포함 하는 Razor 식의 일부를 붙여 넣는 방법 문제가 해결 됨</span><span class="sxs-lookup"><span data-stu-id="4ad3e-120">Fixed: Pasting part of a Razor expression that contains whitespace results in it being reversed</span></span>](#RTM-3)
    - [<span data-ttu-id="4ad3e-121">구문 색 지정 및 IntelliSense 고정: 편집기에서 열려 있는 Razor 파일의 이름 바꾸기 해제</span><span class="sxs-lookup"><span data-stu-id="4ad3e-121">Fixed: Renaming a Razor file that is opened in the editor disables syntax colorization and IntelliSense</span></span>](#RTM-4)
    - [<span data-ttu-id="4ad3e-122">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="4ad3e-122">Known Issues</span></span>](#RTM-KI)
    - [<span data-ttu-id="4ad3e-123">주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="4ad3e-123">Breaking Changes</span></span>](#RTM-BC)
- [<span data-ttu-id="4ad3e-124">ASP.NET MVC 3 Release Candidate 2 (2010 년 12 월 10 일)</span><span class="sxs-lookup"><span data-stu-id="4ad3e-124">ASP.NET MVC 3 Release Candidate 2 (December 10, 2010)</span></span>](#_Toc2)

    - [<span data-ttu-id="4ad3e-125">프로젝트 템플릿이 1.4.4 jQuery, jQuery 유효성 검사 1.7 및 jQuery UI 1.8.6y UI 1.8.6 포함 하도록 변경</span><span class="sxs-lookup"><span data-stu-id="4ad3e-125">Project Templates Changed to Include jQuery 1.4.4, jQuery Validation 1.7, and jQuery UI 1.8.6y UI 1.8.6</span></span>](#_Toc2_1)
    - [<span data-ttu-id="4ad3e-126">추가 된 "AdditionalMetadataAttribute" 클래스</span><span class="sxs-lookup"><span data-stu-id="4ad3e-126">Added "AdditionalMetadataAttribute" Class</span></span>](#_Toc2_2)
    - [<span data-ttu-id="4ad3e-127">향상 된 보기 스 캐 폴딩</span><span class="sxs-lookup"><span data-stu-id="4ad3e-127">Improved View Scaffolding</span></span>](#_Toc2_3)
    - [<span data-ttu-id="4ad3e-128">추가 된 Html.Raw 메서드</span><span class="sxs-lookup"><span data-stu-id="4ad3e-128">Added Html.Raw Method</span></span>](#_Toc2_3)
    - [<span data-ttu-id="4ad3e-129">이름이 바뀐된 "Controller.ViewModel" 속성과 "ViewBag"을 "보기" 속성</span><span class="sxs-lookup"><span data-stu-id="4ad3e-129">Renamed "Controller.ViewModel" Property and the "View" Property To "ViewBag"</span></span>](#_Toc2_4)
    - [<span data-ttu-id="4ad3e-130">이름이 바뀐된 "ControllerSessionStateAttribute" 클래스 "SessionStateAttribute"를</span><span class="sxs-lookup"><span data-stu-id="4ad3e-130">Renamed "ControllerSessionStateAttribute" Class to "SessionStateAttribute"</span></span>](#_Toc2_5)
    - [<span data-ttu-id="4ad3e-131">이름이 바뀐된 RemoteAttribute "Fields" 속성을 "AdditionalFields"</span><span class="sxs-lookup"><span data-stu-id="4ad3e-131">Renamed RemoteAttribute "Fields" Property to "AdditionalFields"</span></span>](#_Toc2_6)
    - [<span data-ttu-id="4ad3e-132">"AllowHtmlAttribute"를 "SkipRequestValidationAttribute" 이름이 변경</span><span class="sxs-lookup"><span data-stu-id="4ad3e-132">Renamed "SkipRequestValidationAttribute" to "AllowHtmlAttribute"</span></span>](#_Toc2_7)
    - [<span data-ttu-id="4ad3e-133">첫 번째 유용한 오류 메시지를 표시 하려면 변경 된 "Html.ValidationMessage" 메서드</span><span class="sxs-lookup"><span data-stu-id="4ad3e-133">Changed "Html.ValidationMessage" Method to Display the First Useful Error Message</span></span>](#_Toc2_8)
    - [<span data-ttu-id="4ad3e-134">고정 @model 문서에 공백을 추가 하지 않는 선언</span><span class="sxs-lookup"><span data-stu-id="4ad3e-134">Fixed @model Declaration to not Add Whitespace to the Document</span></span>](#_Toc2_9)
    - [<span data-ttu-id="4ad3e-135">엔진-특정 파일 이름을 지원 하도록 뷰 엔진에 추가 된 "FileExtensions" 속성</span><span class="sxs-lookup"><span data-stu-id="4ad3e-135">Added "FileExtensions" Property to View Engines to Support Engine-Specific File Names</span></span>](#_Toc2_10)
    - [<span data-ttu-id="4ad3e-136">"For" 특성에 대 한 올바른 값을 내보내는 데 고정된 "LabelFor" 도우미</span><span class="sxs-lookup"><span data-stu-id="4ad3e-136">Fixed "LabelFor" Helper to Emit the Correct Value for the "For" Attribute</span></span>](#_Toc2_11)
    - [<span data-ttu-id="4ad3e-137">모델 바인딩 중 명시적 값 우선 순위 RenderAction"고정된" 메서드</span><span class="sxs-lookup"><span data-stu-id="4ad3e-137">Fixed "RenderAction" Method to Give Explicit Values Precedence During Model Binding</span></span>](#_Toc2_12)
    - [<span data-ttu-id="4ad3e-138">주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="4ad3e-138">Breaking Changes</span></span>](#_Toc2_BC)
    - [<span data-ttu-id="4ad3e-139">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="4ad3e-139">Known Issues</span></span>](#_Toc2_KI)
- [<span data-ttu-id="4ad3e-140">ASP.NET MVC 3 릴리스 후보 (2010 년 11 월 9 일)</span><span class="sxs-lookup"><span data-stu-id="4ad3e-140">ASP.NET MVC 3 Release Candidate (Nov 9, 2010)</span></span>](#TOC_ASP_NET_3_RC)

    - [<span data-ttu-id="4ad3e-141">ASP.NET MVC 3 RC의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="4ad3e-141">New Features in ASP.NET MVC 3 RC</span></span>](#_Toc276711785)
    - [<span data-ttu-id="4ad3e-142">NuGet 패키지 관리자</span><span class="sxs-lookup"><span data-stu-id="4ad3e-142">NuGet Package Manager</span></span>](#_Toc276711786)
    - [<span data-ttu-id="4ad3e-143">향상 "새 프로젝트" 대화 상자</span><span class="sxs-lookup"><span data-stu-id="4ad3e-143">Improved "New Project" Dialog Box</span></span>](#_Toc276711787)
    - [<span data-ttu-id="4ad3e-144">Sessionless 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="4ad3e-144">Sessionless Controllers</span></span>](#_Toc276711788)
    - [<span data-ttu-id="4ad3e-145">새 유효성 검사 특성</span><span class="sxs-lookup"><span data-stu-id="4ad3e-145">New Validation Attributes</span></span>](#_Toc276711789)
    - [<span data-ttu-id="4ad3e-146">"LabelFor" 및 "LabelForModel" 메서드에 대 한 새 오버 로드</span><span class="sxs-lookup"><span data-stu-id="4ad3e-146">New Overloads for "LabelFor" and "LabelForModel" Methods</span></span>](#_Toc276711790)
    - [<span data-ttu-id="4ad3e-147">자식 동작 출력 캐싱</span><span class="sxs-lookup"><span data-stu-id="4ad3e-147">Child Action Output Caching</span></span>](#_Toc276711791)
    - [<span data-ttu-id="4ad3e-148">"뷰 추가" 대화 상자 개선 사항</span><span class="sxs-lookup"><span data-stu-id="4ad3e-148">"Add View" Dialog Box Improvements</span></span>](#_Toc276711792)
    - [<span data-ttu-id="4ad3e-149">Granular Request Validation</span><span class="sxs-lookup"><span data-stu-id="4ad3e-149">Granular Request Validation</span></span>](#_Toc276711793)
    - [<span data-ttu-id="4ad3e-150">주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="4ad3e-150">Breaking Changes</span></span>](#_Toc276711794)
    - [<span data-ttu-id="4ad3e-151">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="4ad3e-151">Known Issues</span></span>](#_Toc276711795)
- [<span data-ttu-id="4ad3e-152">ASP입니다. MVC 3 베타 정보 (2010 년 10 월 6 일)</span><span class="sxs-lookup"><span data-stu-id="4ad3e-152">ASP.MVC 3 Beta Notes (Oct 6, 2010)</span></span>](#TOC_ASP_NET_3_Beta)

    - [<span data-ttu-id="4ad3e-153">ASP.NET MVC 3 베타의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="4ad3e-153">New Features in ASP.NET MVC 3 Beta</span></span>](#0.1__Toc274034215)
    - [<span data-ttu-id="4ad3e-154">NuPack 패키지 관리자</span><span class="sxs-lookup"><span data-stu-id="4ad3e-154">NuPack Package Manager</span></span>](#0.1__Toc274034216)
    - [<span data-ttu-id="4ad3e-155">향상 된 새 프로젝트 대화 상자</span><span class="sxs-lookup"><span data-stu-id="4ad3e-155">Improved New Project Dialog Box</span></span>](#0.1__Toc274034217)
    - [<span data-ttu-id="4ad3e-156">강력 하 게 지정 하는 간단한 방법은 입력 Razor 뷰 모델</span><span class="sxs-lookup"><span data-stu-id="4ad3e-156">Simplified Way to Specify Strongly Typed Models in Razor Views</span></span>](#0.1__Toc274034218)
    - [<span data-ttu-id="4ad3e-157">새 ASP.NET 웹 페이지에 대 한 도우미 메서드를 지원</span><span class="sxs-lookup"><span data-stu-id="4ad3e-157">Support for New ASP.NET Web Pages Helper Methods</span></span>](#0.1__Toc274034219)
    - [<span data-ttu-id="4ad3e-158">추가 종속성 주입 지원</span><span class="sxs-lookup"><span data-stu-id="4ad3e-158">Additional Dependency Injection Support</span></span>](#0.1__Toc274034220)
    - [<span data-ttu-id="4ad3e-159">비 가시적인 jQuery 기반 Ajax에 대 한 새로운 지원</span><span class="sxs-lookup"><span data-stu-id="4ad3e-159">New Support for Unobtrusive jQuery-Based Ajax</span></span>](#0.1__Toc274034221)
    - [<span data-ttu-id="4ad3e-160">비 가시적인 jQuery 유효성 검사에 대 한 새로운 지원</span><span class="sxs-lookup"><span data-stu-id="4ad3e-160">New Support for Unobtrusive jQuery Validation</span></span>](#0.1__Toc274034222)
    - [<span data-ttu-id="4ad3e-161">클라이언트 유효성 검사 및 비간섭 JavaScript에 대 한 새 응용 프로그램 수준 플래그</span><span class="sxs-lookup"><span data-stu-id="4ad3e-161">New Application-Wide Flags for Client Validation and Unobtrusive JavaScript</span></span>](#0.1__Toc274034223)
    - [<span data-ttu-id="4ad3e-162">뷰를 실행 하기 전에 실행 되는 코드에 대 한 새로운 지원</span><span class="sxs-lookup"><span data-stu-id="4ad3e-162">New Support for Code that Runs Before Views Run</span></span>](#0.1__Toc274034224)
    - [<span data-ttu-id="4ad3e-163">VBHTML Razor 구문에 대 한 새로운 지원</span><span class="sxs-lookup"><span data-stu-id="4ad3e-163">New Support for the VBHTML Razor Syntax</span></span>](#0.1__Toc274034225)
    - [<span data-ttu-id="4ad3e-164">ValidateInputAttribute 보다 세부적으로 제어</span><span class="sxs-lookup"><span data-stu-id="4ad3e-164">More Granular Control over ValidateInputAttribute</span></span>](#0.1__Toc274034226)
    - [<span data-ttu-id="4ad3e-165">도우미 밑줄 하이픈에 대 한 변환 익명 개체를 사용 하 여 지정 된 HTML 특성 이름</span><span class="sxs-lookup"><span data-stu-id="4ad3e-165">Helpers Convert Underscores to Hyphens for HTML Attribute Names Specified Using Anonymous Objects</span></span>](#0.1__Toc274034227)
    - [<span data-ttu-id="4ad3e-166">버그 수정</span><span class="sxs-lookup"><span data-stu-id="4ad3e-166">Bug Fixes</span></span>](#0.1__Toc274034228)
    - [<span data-ttu-id="4ad3e-167">주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="4ad3e-167">Breaking Changes</span></span>](#0.1__Toc274034229)
    - [<span data-ttu-id="4ad3e-168">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="4ad3e-168">Known Issues</span></span>](#0.1__Toc274034230)
- [<span data-ttu-id="4ad3e-169">고 지 사항</span><span class="sxs-lookup"><span data-stu-id="4ad3e-169">Disclaimer</span></span>](#0.1__Toc274034231)

<a id="overview"></a>
## <a name="overview"></a><span data-ttu-id="4ad3e-170">개요</span><span class="sxs-lookup"><span data-stu-id="4ad3e-170">Overview</span></span>

<span data-ttu-id="4ad3e-171">이 문서에서는 Visual Studio 2010 용 ASP.NET MVC 3 rtm 릴리스를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-171">This document describes the release of ASP.NET MVC 3 RTM for Visual Studio 2010.</span></span> <span data-ttu-id="4ad3e-172">ASP.NET MVC는 모델-뷰-컨트롤러 (MVC) 패턴을 사용 하는 웹 응용 프로그램을 개발 하기 위한 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-172">ASP.NET MVC is a framework for developing Web applications that uses the Model-View-Controller (MVC) pattern.</span></span> <span data-ttu-id="4ad3e-173">ASP.NET MVC 3 설치 관리자는 다음 구성 요소가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-173">The ASP.NET MVC 3 installer includes the following components:</span></span>

- <span data-ttu-id="4ad3e-174">ASP.NET MVC 3 런타임 구성 요소</span><span class="sxs-lookup"><span data-stu-id="4ad3e-174">ASP.NET MVC 3 runtime components</span></span>
- <span data-ttu-id="4ad3e-175">ASP.NET MVC 3 Visual Studio 2010 도구</span><span class="sxs-lookup"><span data-stu-id="4ad3e-175">ASP.NET MVC 3 Visual Studio 2010 tools</span></span>
- <span data-ttu-id="4ad3e-176">ASP.NET 웹 페이지 런타임 구성 요소</span><span class="sxs-lookup"><span data-stu-id="4ad3e-176">ASP.NET Web Pages run-time components</span></span>
- <span data-ttu-id="4ad3e-177">ASP.NET 웹 페이지 Visual Studio 2010 도구</span><span class="sxs-lookup"><span data-stu-id="4ad3e-177">ASP.NET Web Pages Visual Studio 2010 tools</span></span>
- <span data-ttu-id="4ad3e-178">.NET (NuGet) 용 Microsoft 패키지 관리자</span><span class="sxs-lookup"><span data-stu-id="4ad3e-178">Microsoft Package Manager for .NET (NuGet)</span></span>
- <span data-ttu-id="4ad3e-179">Razor 구문에 대 한 지원을 활성화 하는 Visual Studio 2010에 대 한 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-179">An update for Visual Studio 2010 that enables support for Razor syntax.</span></span> <span data-ttu-id="4ad3e-180">(세부 정보를 기술 자료 문서 2483190 참조).</span><span class="sxs-lookup"><span data-stu-id="4ad3e-180">(For details, see KnowledgeBase article 2483190.)</span></span>

<span data-ttu-id="4ad3e-181">다음 URL의 ASP.NET 웹 사이트에서 ASP.NET MVC 3의 시험판 버전 각각에 대 한 릴리스 정보의 전체 집합을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-181">The full set of release notes for each pre-release version of ASP.NET MVC 3 can be found on the ASP.NET website at the following URL:</span></span>

https://www.asp.net/learn/whitepapers/mvc3-release-notes

<a id="installation-notes"></a>
## <a name="installation-notes"></a><span data-ttu-id="4ad3e-182">설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="4ad3e-182">Installation Notes</span></span>

<span data-ttu-id="4ad3e-183">ASP.NET MVC 3 RTM 웹 플랫폼 설치 관리자 (웹 PI)를 사용 하 여를 설치 하려면 다음 페이지를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-183">To install ASP.NET MVC 3 RTM using the Web Platform Installer (Web PI), visit the following page:</span></span>

[https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3](https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3)

<span data-ttu-id="4ad3e-184">또는 다음 페이지에서 Visual Studio 2010 용 ASP.NET MVC 3 RTM 용 설치 관리자를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-184">Alternatively, you can download the installer for ASP.NET MVC 3 RTM for Visual Studio 2010 from the following page:</span></span>

https://go.microsoft.com/fwlink/?LinkID=208140

<span data-ttu-id="4ad3e-185">ASP.NET MVC 3 설치할 수 있고-함께 실행할 수 있는 ASP.NET MVC 2입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-185">ASP.NET MVC 3 can be installed and can run side-by-side with ASP.NET MVC 2.</span></span>

<a id="software-requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="4ad3e-186">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="4ad3e-186">Software Requirements</span></span>

<span data-ttu-id="4ad3e-187">ASP.NET MVC 3 런타임 구성 요소는 다음과 같은 소프트웨어가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-187">The ASP.NET MVC 3 run-time components require the following software:</span></span>

- <span data-ttu-id="4ad3e-188">.NET framework 버전 4입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-188">.NET Framework version 4.</span></span> 

    <span data-ttu-id="4ad3e-189">ASP.NET MVC 3 Visual Studio 2010 도구에는 다음과 같은 소프트웨어가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-189">ASP.NET MVC 3 Visual Studio 2010 tools require the following software:</span></span>
- <span data-ttu-id="4ad3e-190">Visual Studio 2010 또는 Visual Web Developer 2010 Express입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-190">Visual Studio 2010 or Visual Web Developer 2010 Express.</span></span>

<a id="documentation"></a>
## <a name="documentation"></a><span data-ttu-id="4ad3e-191">설명서</span><span class="sxs-lookup"><span data-stu-id="4ad3e-191">Documentation</span></span>

<span data-ttu-id="4ad3e-192">ASP.NET MVC에 대 한 설명서는 다음 URL에서 MSDN 웹 사이트에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-192">Documentation for ASP.NET MVC is available on the MSDN Web site at the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkId=205717](https://go.microsoft.com/fwlink/?LinkId=205717)

<span data-ttu-id="4ad3e-193">자습서 및 ASP.NET MVC에 대 한 기타 정보는 다음 URL에서 ASP.NET 웹 사이트의 MVC 페이지에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-193">Tutorials and other information about ASP.NET MVC are available on the MVC page of the ASP.NET Web site at the following URL:</span></span>

[https://www.asp.net/mvc/](../mvc/index.md)

<a id="support"></a>
## <a name="support"></a><span data-ttu-id="4ad3e-194">Support(지원)</span><span class="sxs-lookup"><span data-stu-id="4ad3e-194">Support</span></span>

<span data-ttu-id="4ad3e-195">이 완전히 지원 되는 릴리스입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-195">This is a fully supported release.</span></span> <span data-ttu-id="4ad3e-196">기술 지원을 받는 방법에 대 한 정보를 찾을 수 있습니다는 [Microsoft 지원 웹 사이트](https://support.microsoft.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-196">Information about getting technical support can be found at the [Microsoft Support website](https://support.microsoft.com/).</span></span>

<span data-ttu-id="4ad3e-197">또한 자유롭게 ASP.NET 커뮤니티의 구성원은 자주 비공식적인 지원을 제공할 수 있는 ASP.NET MVC 포럼에이 릴리스에 대 한 질문을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-197">Also feel free to post questions about this release to the ASP.NET MVC forum, where members of the ASP.NET community are frequently able to provide informal support:</span></span>

[https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)

<a id="upgrading"></a>
## <a name="upgrading-an-aspnet-mvc-2-project-to-aspnet-mvc-3-tools-update"></a><span data-ttu-id="4ad3e-198">ASP.NET MVC 2 프로젝트 업그레이드 하는 ASP.NET mvc 3 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="4ad3e-198">Upgrading an ASP.NET MVC 2 Project to ASP.NET MVC 3 Tools Update</span></span>

<span data-ttu-id="4ad3e-199">ASP.NET MVC 3 ASP.NET MVC 3을 ASP.NET MVC 2 응용 프로그램을 업그레이드 하는 시기 선택에 유연성을 제공 하 여 동일한 컴퓨터에 ASP.NET MVC 2와 함께 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-199">ASP.NET MVC 3 can be installed side by side with ASP.NET MVC 2 on the same computer, which gives you flexibility in choosing when to upgrade an ASP.NET MVC 2 application to ASP.NET MVC 3.</span></span>

<span data-ttu-id="4ad3e-200">기존 ASP.NET MVC 2 응용 프로그램 버전 3를 수동으로 업그레이드 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-200">To manually upgrade an existing ASP.NET MVC 2 application to version 3, do the following:</span></span>

1. <span data-ttu-id="4ad3e-201">컴퓨터에 비어 있는 새 ASP.NET MVC 3 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-201">Create a new empty ASP.NET MVC 3 project on your computer.</span></span> <span data-ttu-id="4ad3e-202">이 프로젝트는 업그레이드에 필요한 일부 파일을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-202">This project will contain some files that are required for the upgrade.</span></span>
2. <span data-ttu-id="4ad3e-203">ASP.NET MVC 3 프로젝트에서 ASP.NET MVC 2 프로젝트의 해당 위치에 다음 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-203">Copy the following files from the ASP.NET MVC 3 project into the corresponding location of your ASP.NET MVC 2 project.</span></span> <span data-ttu-id="4ad3e-204">새 파일 이름 (jquery-1.5.1.js)을 설명 하기 위해 jQuery 라이브러리에 대 한 참조를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-204">You'll need to update any references to the jQuery library to account for the new filename ( jQuery-1.5.1.js):</span></span> 

    - <span data-ttu-id="4ad3e-205">/Views/Web.config</span><span class="sxs-lookup"><span data-stu-id="4ad3e-205">/Views/Web.config</span></span>
    - <span data-ttu-id="4ad3e-206">/packages.config</span><span class="sxs-lookup"><span data-stu-id="4ad3e-206">/packages.config</span></span>
    - <span data-ttu-id="4ad3e-207">/scripts/\*.js</span><span class="sxs-lookup"><span data-stu-id="4ad3e-207">/scripts/\*.js</span></span>
    - <span data-ttu-id="4ad3e-208">/Content/themes/\*.\*</span><span class="sxs-lookup"><span data-stu-id="4ad3e-208">/Content/themes/\*.\*</span></span>
3. <span data-ttu-id="4ad3e-209">복사는 *패키지* 솔루션의.sln 파일이 있는 디렉터리에 있는 솔루션의 루트에 빈 ASP.NET MVC 3 프로젝트 솔루션의 루트에는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-209">Copy the *packages* folder in the root of the empty ASP.NET MVC 3 project solution into the root of your solution, which is in the directory where the solution's .sln file is located.</span></span>
4. <span data-ttu-id="4ad3e-210">ASP.NET MVC 2 프로젝트에 영역이 포함 된, 경우 /Views/Web.config 파일을 복사는 *뷰* 각 영역의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-210">If your ASP.NET MVC 2 project contains any areas, copy the /Views/Web.config file to the *Views* folder of each area.</span></span>
5. <span data-ttu-id="4ad3e-211">ASP.NET MVC 2 프로젝트에서 두 Web.config 파일에서 검색 하 고 ASP.NET MVC 버전이 대체 되는 전역적으로.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-211">In both Web.config files in the ASP.NET MVC 2 project, globally search and replace the ASP.NET MVC version.</span></span> <span data-ttu-id="4ad3e-212">다음을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-212">Find the following:</span></span> 

    [!code-console[Main](mvc3-release-notes/samples/sample1.cmd)]

    <span data-ttu-id="4ad3e-213">다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-213">Replace it with the following:</span></span>

    [!code-console[Main](mvc3-release-notes/samples/sample2.cmd)]
6. <span data-ttu-id="4ad3e-214">솔루션 탐색기에서 삭제에 대 한 참조 *System.Web.Mvc* (점을 DLL 버전 2), 다음에 대 한 참조를 추가 *System.Web.Mvc* (v3.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="4ad3e-214">In Solution Explorer, delete the reference to *System.Web.Mvc* (which points to the DLL from version 2), then add a reference to *System.Web.Mvc* (v3.0.0.0).</span></span>
7. <span data-ttu-id="4ad3e-215">System.Web.WebPages.dll 및 System.Web.Helpers.dll에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-215">Add a reference to System.Web.WebPages.dll and System.Web.Helpers.dll.</span></span> <span data-ttu-id="4ad3e-216">이러한 어셈블리는 다음 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-216">These assemblies are located in the following folders:</span></span> 

    - <span data-ttu-id="4ad3e-217">%ProgramFiles%\ Microsoft ASP.NET\ASP.NET MVC 3\Assemblies</span><span class="sxs-lookup"><span data-stu-id="4ad3e-217">%ProgramFiles%\ Microsoft ASP.NET\ASP.NET MVC 3\Assemblies</span></span>
    - <span data-ttu-id="4ad3e-218">%ProgramFiles%\ Microsoft ASP.NET\ASP.NET 웹 Pages\v1.0\Assemblies</span><span class="sxs-lookup"><span data-stu-id="4ad3e-218">%ProgramFiles%\ Microsoft ASP.NET\ASP.NET Web Pages\v1.0\Assemblies</span></span>
8. <span data-ttu-id="4ad3e-219">솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 프로젝트 언로드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-219">In Solution Explorer, right-click the project name and select Unload Project.</span></span> <span data-ttu-id="4ad3e-220">그런 다음 프로젝트 이름을 다시 마우스 오른쪽 단추로 클릭 하 고 편집 선택 *ProjectName*.csproj 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-220">Then right-click the project name again and select Edit *ProjectName*.csproj.</span></span>
9. <span data-ttu-id="4ad3e-221">찾을 *ProjectTypeGuids* 요소 및 {F85E285D-A4E0-4152-9332-AB1D724D3325} {E53F8FEA-EAE0-44A6-8774-FFD645390401}로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-221">Locate the *ProjectTypeGuids* element and replace {F85E285D-A4E0-4152-9332-AB1D724D3325} with {E53F8FEA-EAE0-44A6-8774-FFD645390401}.</span></span>
10. <span data-ttu-id="4ad3e-222">변경 내용을 저장, 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 프로젝트 다시 로드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-222">Save the changes, right-click the project, and then select Reload Project.</span></span>
11. <span data-ttu-id="4ad3e-223">응용 프로그램의 루트 Web.config 파일에 추가 하려면 다음 설정의 *어셈블리* 섹션.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-223">In the application's root Web.config file, add the following settings to the *assemblies* section.</span></span> 

    [!code-xml[Main](mvc3-release-notes/samples/sample3.xml)]
12. <span data-ttu-id="4ad3e-224">ASP.NET MVC 2를 사용 하 여 컴파일되는 모든 타사 라이브러리를 프로젝트에서 참조 하는 경우 강조 표시 된 다음 추가 *bindingRedirect* 응용 프로그램 루트에 있는 Web.config 파일에는 요소는 * 구성* 섹션:</span><span class="sxs-lookup"><span data-stu-id="4ad3e-224">If the project references any third-party libraries that are compiled using ASP.NET MVC 2, add the following highlighted *bindingRedirect* element to the Web.config file in the application root under the *configuration* section:</span></span> 

    [!code-xml[Main](mvc3-release-notes/samples/sample4.xml)]

<a id="tu-changes"></a>
## <a name="changes-in-aspnet-mvc-3-tools-update"></a><span data-ttu-id="4ad3e-225">변경 내용을 in ASP.NET MVC 3 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="4ad3e-225">Changes in ASP.NET MVC 3 Tools Update</span></span>

<span data-ttu-id="4ad3e-226">이 섹션에서는 ASP.NET MVC 3 RTM 릴리스 이후의 ASP.NET MVC 3 도구 업데이트 릴리스에서 변경에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-226">This section describes changes made in the ASP.NET MVC 3 Tools Update release since the ASP.NET MVC 3 RTM release.</span></span>

<a id="tu-AddControllerDialog"></a>
### <a name="add-controller-dialog-box-can-now-scaffold-controllers-with-views-and-data-access-code"></a><span data-ttu-id="4ad3e-227">"컨트롤러 추가" 대화 상자에 컨트롤러를 뷰 및 데이터 액세스 코드와 함께 스 캐 폴딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-227">"Add Controller" dialog box can now scaffold controllers with views and data access code</span></span>

<span data-ttu-id="4ad3e-228">스 캐 폴딩은 방법은 응용 프로그램에 대 한 뷰와 컨트롤러를 신속 하 게 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-228">Scaffolding is a way of quickly generating a controller and views for your application.</span></span> <span data-ttu-id="4ad3e-229">코드 생성 된 후 프로젝트의 요구 사항에 맞게 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-229">After the code has been generated, you can edit it to meet your project's requirements.</span></span>

<span data-ttu-id="4ad3e-230">시작 하는 *컨트롤러 추가* 대화 상자에서 ASP.NET MVC 3 마우스 오른쪽 단추로 클릭는 *컨트롤러* 폴더에 *솔루션 탐색기*, 클릭 *추가*, 클릭 하 고 *컨트롤러*합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-230">To launch the *Add Controller* dialog box in ASP.NET MVC 3, right-click the *Controllers* folder in *Solution Explorer*, click *Add*, and then click *Controller*.</span></span> <span data-ttu-id="4ad3e-231">대화 상자 추가적인 스 캐 폴딩 옵션을 제공 하도록 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-231">The dialog box has been enhanced to offer additional scaffolding options.</span></span>

![](mvc3-release-notes/_static/image1.png)

<span data-ttu-id="4ad3e-232">기본적으로 사용 가능한 세 개의 스 캐 폴딩 템플릿이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-232">There are three scaffolding templates available by default.</span></span>

#### <a name="empty-controller"></a><span data-ttu-id="4ad3e-233">빈 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="4ad3e-233">Empty Controller</span></span>

<span data-ttu-id="4ad3e-234">이 템플릿은 빈 컨트롤러 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-234">This template generates an empty controller file.</span></span> <span data-ttu-id="4ad3e-235">이 템플릿을 선택 하지 않는 것 같습니다. *만들기, 편집, 세부 정보에 대 한 작업을 추가, 삭제 시나리오* 이전 버전의 ASP.NET MVC에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-235">This template is equivalent to not checking *Add actions for create, edit, details, delete scenarios* in previous versions of ASP.NET MVC.</span></span> <span data-ttu-id="4ad3e-236">이 선택 하면 없습니다 추가 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-236">If you choose this, no further options are available.</span></span>

#### <a name="controller-with-empty-readwrite-actions"></a><span data-ttu-id="4ad3e-237">빈 읽기/쓰기 동작이 포함 된 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="4ad3e-237">Controller with empty read/write actions</span></span>

<span data-ttu-id="4ad3e-238">이 템플릿은 방법의 모든 필요한 동작 메서드에 구현 코드가 없는 되어 있는 컨트롤러 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-238">This template generates a controller file that has all the required action methods but no implementation code in the methods.</span></span> <span data-ttu-id="4ad3e-239">이 템플릿을 확인 하는 것 *만들기, 편집, 세부 정보에 대 한 작업을 추가, 삭제 시나리오* 이전 버전의 ASP.NET MVC에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-239">This template is equivalent to checking *Add actions for create, edit, details, delete scenarios* in previous versions of ASP.NET MVC.</span></span> <span data-ttu-id="4ad3e-240">이 선택 하면 없습니다 추가 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-240">If you choose this, no further options are available.</span></span>

#### <a name="controller-with-readwrite-actions-and-views-using-entity-framework"></a><span data-ttu-id="4ad3e-241">읽기/쓰기 동작 및 Entity Framework를 사용 하 여 뷰, 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="4ad3e-241">Controller with read/write actions and views, using Entity Framework</span></span>

<span data-ttu-id="4ad3e-242">이 서식 파일을 사용 하면 신속 하 게 작업 데이터 입력 사용자 인터페이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-242">This template enables you to quickly create a working data-entry user interface.</span></span> <span data-ttu-id="4ad3e-243">다양 한 일반 요구 사항 및 다음과 같은 시나리오를 처리 하는 코드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-243">It generates code that handles a range of common requirements and scenarios, such as the following:</span></span>

- <span data-ttu-id="4ad3e-244">*데이터 액세스*합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-244">*Data access*.</span></span> <span data-ttu-id="4ad3e-245">생성 된 코드를 읽고 엔터티는 데이터베이스에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-245">The generated code reads and writes entities in a database.</span></span> <span data-ttu-id="4ad3e-246">기존 데이터 컨텍스트 클래스를 선택 하거나 템플릿에서 새 생성 하도록 하면 Entity Framework Code First 접근 방식으로 작동 *DbContext* 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-246">It works with the Entity Framework Code First approach if you choose an existing data context class or if you let the template generate a new *DbContext* class.</span></span> <span data-ttu-id="4ad3e-247">기존 선택도 Entity Framework Database First 또는 Model First 접근 방식으로 작동 *ObjectContext* 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-247">It also works with the Entity Framework Database First or Model First approach if you choose an existing *ObjectContext* class.</span></span>
- <span data-ttu-id="4ad3e-248">*유효성 검사*합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-248">*Validation*.</span></span> <span data-ttu-id="4ad3e-249">생성 된 코드 모델 클래스에 선언 된 규칙에 따라 폼 전송의 유효성이 검사 됩니다 되도록 ASP.NET MVC 모델 바인딩 및 메타 데이터 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-249">The generated code uses ASP.NET MVC model binding and metadata features so that form submissions are validated according to rules declared on your model class.</span></span> <span data-ttu-id="4ad3e-250">같은 기본 제공 유효성 검사 규칙이 포함 됩니다는 *필요한* 및 *StringLength* 특성 및 사용자 지정 유효성 검사 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-250">This includes built-in validation rules, such as the *Required* and *StringLength* attributes, and custom validation rules.</span></span>
- <span data-ttu-id="4ad3e-251">*1 대 다 관계*합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-251">*One-to-many relationships*.</span></span> <span data-ttu-id="4ad3e-252">모델 클래스 간에 일대다에 외래 키 관계를 정의 하면 생성된 된 코드는 관련된 엔터티를 선택 하기 위한 드롭 다운 목록을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-252">If you define one-to-many foreign-key relationships between your model classes, the generated code will produce drop-down lists for selecting related entities.</span></span> <span data-ttu-id="4ad3e-253">예를 들어, Entity Framework Code First 규칙을 따르는 다음과 같은 모델 클래스를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-253">For example, you might define the following model classes following Entity Framework Code First conventions:</span></span> 

    [!code-csharp[Main](mvc3-release-notes/samples/sample5.cs)]

    <span data-ttu-id="4ad3e-254">경우 다음 스 캐 폴드 할에 대 한 컨트롤러는 *제품* 클래스, 해당 뷰를 통해 사용자가 선택할 수는 *범주* 각각에 대 한 개체 *제품* 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-254">When you then scaffold a controller for the *Product* class, its views will allow users to choose a *Category* object for each *Product* instance.</span></span>

    <span data-ttu-id="4ad3e-255">이 서식 파일의 추가 옵션을 사용 하면는 *컨트롤러 추가* 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-255">This template enables additional options in the *Add Controller* dialog box.</span></span> <span data-ttu-id="4ad3e-256">에 대 한 *모델 클래스*, 사용자가을 만들거나 편집할 수 있는 데이터 형식을 결정 하는 솔루션의 모든 모델 클래스를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-256">For *Model class*, you can choose any model class in your solution, which determines the type of data that users will be able to create or edit:</span></span>
- <span data-ttu-id="4ad3e-257">Entity Framework Code First를 사용 하려는 경우 아무 모델 클래스나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-257">If you want to use Entity Framework Code First, you can choose any model class.</span></span>
- <span data-ttu-id="4ad3e-258">Entity Framework Database First 또는 Entity Framework Model First를 사용 하는 경우 개념적 모델에 정의 된 엔터티 클래스를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-258">If you are using Entity Framework Database First or Entity Framework Model First, be sure to choose an entity class defined in your conceptual model.</span></span>

<span data-ttu-id="4ad3e-259">에 대 한 *데이터 컨텍스트 클래스*, 이러한 선택 항목을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-259">For *Data Context class*, you can make these choices:</span></span>

- <span data-ttu-id="4ad3e-260">Code First 사용 하 여 않으며 없는 기존 데이터 컨텍스트 클래스를 선택 하려는 경우 * * 새 데이터 컨텍스트에 * *입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-260">If you want to use Code First and have no existing data context class, choose **New data context **.</span></span> <span data-ttu-id="4ad3e-261">데이터 컨텍스트 클래스를 다음 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-261">A data context class will then be generated for you.</span></span>
- <span data-ttu-id="4ad3e-262">Code First를 사용 하 여 기존 데이터 컨텍스트 클래스가 하려는 경우 여기에서 선택한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-262">If you want to use Code First and have an existing data context class, choose it here.</span></span> <span data-ttu-id="4ad3e-263">선택한 모델 클래스를 유지 하도록 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-263">It will be updated to persist the model class you have selected.</span></span>
- <span data-ttu-id="4ad3e-264">Database First 또는 Model First를 사용 하는 경우 여기서 개체 컨텍스트 클래스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-264">If you are using Database First or Model First, choose your object context class here.</span></span>

<span data-ttu-id="4ad3e-265">뷰를 사용 하려는 뷰 엔진을 선택 하거나 모든 뷰를 스 캐 폴드 하려면 없음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-265">For Views, choose the view engine you want to use, or choose None if you don't want to scaffold any views.</span></span>

<span data-ttu-id="4ad3e-266">고급 하려면을 선택 하면 추가 생성 된 뷰에 대 한 옵션을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-266">You can select Advanced Optionsto specify further options for the generated views.</span></span> <span data-ttu-id="4ad3e-267">예를 들어 레이아웃 또는 마스터 페이지를 사용 하 여 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-267">For example, you can choose the layout or master page to use.</span></span>

<a id="tu-ImprovementsNewDialogBox"></a>
### <a name="improvements-to-the-aspnet-mvc-3-new-project-dialog-box"></a><span data-ttu-id="4ad3e-268">향상 된 기능에서 "ASP.NET MVC 3 새 프로젝트" 대화 상자</span><span class="sxs-lookup"><span data-stu-id="4ad3e-268">Improvements to the "ASP.NET MVC 3 New Project" Dialog Box</span></span>

<span data-ttu-id="4ad3e-269">새 ASP.NET MVC 3 프로젝트를 만드는 데 사용 하 여 대화 상자 아래에 나열 된 향상 된 여러 기능이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-269">The dialog box you use to create new ASP.NET MVC 3 projects includes multiple improvements, as listed below.</span></span>

![](mvc3-release-notes/_static/image2.png)

#### <a name="new-intranet-project-template"></a><span data-ttu-id="4ad3e-270">새 "인트라넷 프로젝트" 템플릿</span><span class="sxs-lookup"><span data-stu-id="4ad3e-270">New "Intranet Project" Template</span></span>

<span data-ttu-id="4ad3e-271">프로젝트 템플릿 목록에는 새 인트라넷 응용 프로그램 템플릿이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-271">The Project Template list includes a new Intranet Application template.</span></span> <span data-ttu-id="4ad3e-272">이 템플릿에 폼 인증 대신 Windows 인증을 사용 하 여 웹 응용 프로그램에 대 한 설정을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-272">This template contains settings for building a web application using Windows authentication instead of forms authentication.</span></span> <span data-ttu-id="4ad3e-273">인트라넷 응용 프로그램 프로젝트 템플릿에서 캡슐화 할 수 없는 일부 IIS 설정이 필요로 하므로 서식 파일에는 추가 정보 파일을 IIS에서 프로젝트 템플릿을 만드는 방법에 대 한 지침이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-273">Because an intranet application requires some IIS settings that can't be encapsulated in a project template, the template includes a readme file with instructions for how to make the project template work in IIS.</span></span> <span data-ttu-id="4ad3e-274">에 대 한 설명서는 새 인트라넷 응용 프로그램 서식 파일은 다음 URL의 MSDN 웹 사이트에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-274">Documentation for the a new Intranet Application template is available on the MSDN website at the following URL:</span></span>

[https://msdn.microsoft.com/library/gg703322(VS.98).aspx](https://msdn.microsoft.com/library/gg703322(VS.98).aspx)

#### <a name="project-templates-are-now-html5-enabled"></a><span data-ttu-id="4ad3e-275">프로젝트 템플릿에 HTML5 사용 하도록 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-275">Project templates are now HTML5 enabled</span></span>

<span data-ttu-id="4ad3e-276">새 프로젝트 대화 상자에 이제 프로젝트 템플릿에 HTML5 특정 기능을 추가할 수 있는 옵션이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-276">The new-project dialog box now contains an option to add HTML5-specific features to the project templates.</span></span> <span data-ttu-id="4ad3e-277">옵션을 선택 하면 새 HTML5를 포함 하는 뷰가 생성 될 `<header>`, `<footer>`, 및 `<navigation>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-277">Selecting the option causes views to be generated that contain the new HTML5 `<header>`, `<footer>`, and `<navigation>` elements.</span></span>

<span data-ttu-id="4ad3e-278">참고가 이전 버전의 브라우저 HTML5 특정 태그를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-278">Note that earlier versions of browsers do not support HTML5-specific tags.</span></span> <span data-ttu-id="4ad3e-279">이 한계를 해결 하기 위해 HTML5 프로젝트 템플릿에 Modernizr 라이브러리에 대 한 참조를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-279">To address this limitation, the HTML5 project templates include a reference to the Modernizr library.</span></span> <span data-ttu-id="4ad3e-280">(다음 섹션 참조).</span><span class="sxs-lookup"><span data-stu-id="4ad3e-280">(See the next section.)</span></span>

<a id="tu-Modernizr"></a>
### <a name="project-templates-now-include-modernizr-17"></a><span data-ttu-id="4ad3e-281">프로젝트 템플릿에 Modernizr 1.7이 포함</span><span class="sxs-lookup"><span data-stu-id="4ad3e-281">Project templates now include Modernizr 1.7</span></span>

<span data-ttu-id="4ad3e-282">Modernizr은 아직 이러한 기능을 지원 하지 않는 브라우저에서 CSS 3 및 HTML5 지원이 가능한 JavaScript 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-282">Modernizr is a JavaScript library that enables support for CSS 3 and HTML5 in browsers that do not yet support these features.</span></span> <span data-ttu-id="4ad3e-283">이 라이브러리는 ASP.NET MVC 3 프로젝트용 템플릿에 사전 설치 NuGet 패키지로 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-283">This library is included as a pre-installed NuGet package in templates for ASP.NET MVC 3 projects.</span></span> <span data-ttu-id="4ad3e-284">Modernizr에 대 한 자세한 내용은 참조 [ http://www.modernizr.com/ ](http://www.modernizr.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-284">For more information about Modernizr, see [http://www.modernizr.com/](http://www.modernizr.com/).</span></span>

<a id="tu-UpdatedJQuery"></a>
### <a name="project-templates-include-updated-versions-of-jquery-jquery-ui-and-jquery-validation"></a><span data-ttu-id="4ad3e-285">프로젝트 템플릿에 jQuery, jQuery UI 및 jQuery의 업데이트 된 버전이 포함 되어 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="4ad3e-285">Project templates include updated versions of jQuery, jQuery UI, and jQuery Validation</span></span>

<span data-ttu-id="4ad3e-286">프로젝트 템플릿에 jQuery 스크립트의 다음 버전 포함:</span><span class="sxs-lookup"><span data-stu-id="4ad3e-286">The project templates now include the following versions of the jQuery scripts:</span></span>

- <span data-ttu-id="4ad3e-287">1.5.1 jQuery</span><span class="sxs-lookup"><span data-stu-id="4ad3e-287">jQuery 1.5.1</span></span>
- <span data-ttu-id="4ad3e-288">jQuery 유효성 검사 1.8</span><span class="sxs-lookup"><span data-stu-id="4ad3e-288">jQuery Validation 1.8</span></span>
- <span data-ttu-id="4ad3e-289">jQuery UI 1.8.11</span><span class="sxs-lookup"><span data-stu-id="4ad3e-289">jQuery UI 1.8.11</span></span>

<span data-ttu-id="4ad3e-290">이러한 라이브러리는 사전 설치 된 NuGet 패키지로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-290">These libraries are included as pre-installed NuGet packages.</span></span>

<a id="tu-EF"></a>
### <a name="project-templates-now-include-adonet-entity-framework-41-as-a-pre-installed-nuget-package"></a><span data-ttu-id="4ad3e-291">프로젝트 템플릿에 이제 ADO.NET Entity Framework 4.1 사전 설치 NuGet 패키지로 포함</span><span class="sxs-lookup"><span data-stu-id="4ad3e-291">Project templates now include ADO.NET Entity Framework 4.1 as a pre-installed NuGet package</span></span>

<span data-ttu-id="4ad3e-292">ADO.NET Entity Framework 4.1 Code First 기능이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-292">The ADO.NET Entity Framework 4.1 includes the Code First feature.</span></span> <span data-ttu-id="4ad3e-293">코드는 먼저 기존 Database First 및 Model First 패턴에 대 한 대안을 제공 하는 ADO.NET Entity Framework에 대 한 새로운 개발 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-293">Code First is a new development pattern for the ADO.NET Entity Framework that provides an alternative to the existing Database First and Model First patterns.</span></span>

<span data-ttu-id="4ad3e-294">코드 먼저은 집중 Visual Basic 또는 C#에서 작성 된 POCO 클래스 ("일반 이전 CLR 개체")를 사용 하 여 모델을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-294">Code First is focused around defining your model using POCO classes ("plain old CLR objects") written in Visual Basic or C#.</span></span> <span data-ttu-id="4ad3e-295">이러한 클래스 다음 기존 데이터베이스에 매핑할 수 있습니다 또는 데이터베이스 스키마를 생성 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-295">These classes can then be mapped to an existing database or be used to generate a database schema.</span></span> <span data-ttu-id="4ad3e-296">사용 하 여 추가 구성을 제공 될 수 있습니다 *DataAnnotations* 특성 또는 fluent Api를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-296">Additional configuration can be supplied using *DataAnnotations* attributes or using fluent APIs.</span></span>

<span data-ttu-id="4ad3e-297">코드 Firstwith ASP.NET MVC를 사용 하 여에 대 한 설명서는 다음 Url에서 ASP.NET 웹 사이트에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-297">Documentation for using Code Firstwith ASP.NET MVC is available on the ASP.NET website at the following URLs:</span></span>

<span data-ttu-id="4ad3e-298">[https://www.asp.net/mvc/tutorials/getting-started-with-mvc3-part1-cs](../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [https://www.asp.net/entity-framework/tutorials/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="4ad3e-298">[https://www.asp.net/mvc/tutorials/getting-started-with-mvc3-part1-cs](../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [https://www.asp.net/entity-framework/tutorials/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)</span></span>

<a id="tu-JavaScriptLibsNuget"></a>
### <a name="project-templates-include-javascript-libraries-as-pre-installed-nuget-packages"></a><span data-ttu-id="4ad3e-299">프로젝트 템플릿에 JavaScript 라이브러리를 사전 설치 된 NuGet 패키지로 포함</span><span class="sxs-lookup"><span data-stu-id="4ad3e-299">Project templates include JavaScript libraries as pre-installed NuGet packages</span></span>

<span data-ttu-id="4ad3e-300">프로젝트에 설치 하 여 앞에서 언급 한 JavaScript 파일 (예: Modernizr 라이브러리)을 포함 하는 새 ASP.NET MVC 3 프로젝트를 만들면 직접 프로젝트 템플릿에 있는 스크립트 폴더에 스크립트를 추가 하는 대신 NuGet을 사용 하 여 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-300">When you create a new ASP.NET MVC 3 project, the project includes the JavaScript files mentioned previously (for example, the Modernizr library) by installing them using NuGet instead of directly adding the scripts to the Scripts folder in the project template contents.</span></span> <span data-ttu-id="4ad3e-301">따라서 NuGet을 사용 하 여 스크립트의 새 버전이 릴리스되면 최신 버전으로 스크립트를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-301">This enables you to use NuGet to update the scripts to the latest version when new versions of the scripts are released.</span></span>

<span data-ttu-id="4ad3e-302">예를 들어 새 jQuery 릴리스 빈도가 제공 프로젝트 템플릿에 포함 된 jQuery 버전은 특정 시점에 됩니다 만료.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-302">For example, given the frequency of new jQuery releases, the version of jQuery included in the project template will at some point be out of date.</span></span> <span data-ttu-id="4ad3e-303">그러나 jQuery가 설치 된 NuGet 패키지로 포함 하기 때문에 알려 NuGet 대화 상자에서 최신 버전의 jQuery 사용할 수 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-303">However, because jQuery is included as an installed NuGet package, you will be notified in the NuGet dialog box when newer versions of jQuery are available.</span></span>

<span data-ttu-id="4ad3e-304">JQuery 파일 이름에 버전 번호를 포함 하므로 jQuery를 최신 버전으로 업데이트 하려면 업데이트 해야는 `<script>` 새 파일 이름을 사용 하기 위해 jQuery 파일을 참조 하는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-304">Because jQuery includes the version number in the file name, updating jQuery to the latest version also requires updating the `<script>` tag that references the jQuery file to use the new file name.</span></span> <span data-ttu-id="4ad3e-305">다른 포함된 스크립트 라이브러리 스크립트 이름을 할 버전 번호를 포함 하지 않으므로 최신 버전으로 더 쉽게 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-305">Other included script libraries do not include the version number in the script name, so they can be more easily updated to their latest versions.</span></span>

<a id="tu-KI"></a>
## <a name="known-issues"></a><span data-ttu-id="4ad3e-306">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="4ad3e-306">Known Issues</span></span>

- <span data-ttu-id="4ad3e-307">일부 경우에는 오류 메시지 "설치 실패 오류 코드 (0x80070643)"으로 설치가 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-307">In some cases, installation may fail with the error message "Installation failed with error code (0x80070643)".</span></span> <span data-ttu-id="4ad3e-308">이 문제를 해결 하는 방법에 대 한 정보를 참조 하십시오. [기술 자료 문서 2531566](https://support.microsoft.com/kb/2531566)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-308">For information about how to work around this issue, see [KnowledgeBase article 2531566](https://support.microsoft.com/kb/2531566).</span></span>
- <span data-ttu-id="4ad3e-309">컨트롤러 추가 대 한 스 캐 폴딩 Entity Framework에서 엔터티 상속 지원 기능을 활용 하는 엔터티 스 캐 폴딩 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-309">The scaffolding for adding a controller does not scaffold entities that take advantage of entity inheritance support within Entity Framework.</span></span> <span data-ttu-id="4ad3e-310">예를 들어 기본 제공 *사람* 클래스에 상속 되는 *학생* 클래스를 스 캐 폴딩는 *학생* 클래스 컴파일되지 않습니다. 생성 된 코드에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-310">For example, given a base *Person* class that's inherited by a *Student* class, scaffolding the *Student* class will result in generated code that does not compile.</span></span>
- <span data-ttu-id="4ad3e-311">원인을 솔루션 폴더에서 새 ASP.NET MVC 3 프로젝트를 만들기는 *NullReferenceException* 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-311">Creating a new ASP.NET MVC 3 project within a solution folder causes a *NullReferenceException* error.</span></span> <span data-ttu-id="4ad3e-312">해결 방법은 솔루션의 루트에 ASP.NET MVC 3 프로젝트를 만들고 다음 솔루션 폴더로 이동 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-312">The workaround is to create the ASP.NET MVC 3 project in the root of the solution and then move it into the solution folder.</span></span>
- <span data-ttu-id="4ad3e-313">ReSharper가 설치 된 경우에 IntelliSense for Razor 구문 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-313">IntelliSense for Razor syntax does not work when ReSharper is installed.</span></span> <span data-ttu-id="4ad3e-314">ReSharper가 설치 되어 ASP.NET MVC 3의 Razor IntelliSense 지원을 활용 하려고 하는 경우 항목을 참조 [Razor Intellisense and ReSharper](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) Hadi Hariri 블로그에서 함께 사용 하는 방법을 설명 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-314">If you have ReSharper installed and want to take advantage of the Razor IntelliSense support in ASP.NET MVC 3, see the entry [Razor Intellisense and ReSharper](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) on Hadi Hariri's blog, which discusses ways to use them together today.</span></span>
- <span data-ttu-id="4ad3e-315">설치 하는 동안 EULA 동의 대화 상자 예정 보다 작은 창에서 사용 약관을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-315">During installation, the EULA acceptance dialog box displays the license terms in a window that is smaller than intended.</span></span>
- <span data-ttu-id="4ad3e-316">Razor 뷰를 편집할 때 (.cshtml 또는.* vbhtml* 파일), 뷰.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-316">When you are editing a Razor view (.cshtml or .*vbhtml* file), views.</span></span> <span data-ttu-id="4ad3e-317">ASP.NET MVC 3 Razor 뷰의 코드 조각이 포함 되지 않습니다. ASP.NET MVC 용 코드 조각 aspxselecting 조각이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-317">ASP.NET MVC 3 does not include any snippets for Razor views..aspxselecting a code snippet for ASP.NET MVC will show snippets for</span></span>
- <span data-ttu-id="4ad3e-318">여기서 Visual Studio 설치 되지 않은 컴퓨터에 Visual Web Developer Express에 대 한 ASP.NET MVC 3을 설치 하 고 다음 나중에 Visual Studio를 설치 하는 경우에 ASP.NET MVC 3를 다시 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-318">If you install ASP.NET MVC 3 for Visual Web Developer Express on a computer where Visual Studio is not installed, and then later install Visual Studio, you must reinstall ASP.NET MVC 3.</span></span> <span data-ttu-id="4ad3e-319">Visual Studio 및 Visual Web Developer Express는 ASP.NET MVC 3 설치 관리자가 업그레이드 하는 구성 요소를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-319">Visual Studio and Visual Web Developer Express share components that are upgraded by the ASP.NET MVC 3 installer.</span></span> <span data-ttu-id="4ad3e-320">Visual Web Developer Express가 되지 않으며 다음 나중에 Visual Web Developer Express를 설치 하는 컴퓨터에서 Visual Studio에 대 한 ASP.NET MVC 3을 설치 하는 경우 동일한 문제에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-320">The same issue applies if you install ASP.NET MVC 3 for Visual Studio on a computer that does not have Visual Web Developer Express and then later install Visual Web Developer Express.</span></span>

<a id="MVC3RTM"></a>
## <a name="changes-in-aspnet-mvc-3-rtm"></a><span data-ttu-id="4ad3e-321">ASP.NET MVC 3 RTM의 변경 내용</span><span class="sxs-lookup"><span data-stu-id="4ad3e-321">Changes in ASP.NET MVC 3 RTM</span></span>

<span data-ttu-id="4ad3e-322">이 섹션에서는 RC2 릴리스 이후의 ASP.NET MVC 3 RTM 릴리스에서 만든 버그 수정 및 변경 내용을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-322">This section describes changes and bug fixes made in the ASP.NET MVC 3 RTM release since the RC2 release.</span></span>

<a id="RTM-1"></a>
### <a name="change-updated-the-version-of-jquery-ui-to-187"></a><span data-ttu-id="4ad3e-323">변경 사항: 1.8.7 버전의 jQuery UI 업데이트</span><span class="sxs-lookup"><span data-stu-id="4ad3e-323">Change: Updated the version of jQuery UI to 1.8.7</span></span>

<span data-ttu-id="4ad3e-324">ASP.NET MVC 프로젝트 템플릿은 Visual Studio에 대 한 최신 버전의 jQuery UI 라이브러리를 포함 하도록 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-324">The ASP.NET MVC project templates for Visual Studio were updated to include the latest version of the jQuery UI library.</span></span> <span data-ttu-id="4ad3e-325">템플릿에 jQuery UI 관련된 CSS 및 이미지 파일과 같은 필요한 리소스 파일의 최소 집합도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-325">The templates also include the minimal set of resource files required by jQuery UI, such as the associated CSS and image files.</span></span>

<a id="RTM-2"></a>
### <a name="change-changed-the-default-modelmetadataprovider-back-to-dataannotationsmodelmetadataprovider"></a><span data-ttu-id="4ad3e-326">ModelMetadataProvider DataAnnotationsModelMetadataProvider로 다시 기본값을 변경 하는 변경 사항:</span><span class="sxs-lookup"><span data-stu-id="4ad3e-326">Change: Changed the default ModelMetadataProvider back to DataAnnotationsModelMetadataProvider</span></span>

<span data-ttu-id="4ad3e-327">도입 된 ASP.NET MVC 3의 RC2 릴리스는 *CachedDataAnnotationsMetadataProvider* 는 제공 된 기존 위에 캐싱 클래스 *DataAnnotationsModelMetadataProvider* 으로 클래스는 성능이 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-327">The RC2 release of ASP.NET MVC 3 introduced a *CachedDataAnnotationsMetadataProvider* class that provided caching on top of the existing *DataAnnotationsModelMetadataProvider* class as a performance improvement.</span></span> <span data-ttu-id="4ad3e-328">그러나 몇 가지 버그 된 보고이 프로세스를 구현 하므로 변경 내용이 되돌릴 되었으며에서 제공 되는 MVC 미래 프로젝트로 이동할 [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-328">However, some bugs were reported with this implementation, so the change has been reverted and moved into the MVC Futures project, which is available at [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack).</span></span>

<a id="RTM-3"></a>
### <a name="fixed-pasting-part-of-a-razor-expression-that-contains-whitespace-results-in-it-being-reversed"></a><span data-ttu-id="4ad3e-329">공백 결과 거꾸로를 포함 하는 Razor 식의 일부를 붙여 넣는 방법 문제가 해결 됨</span><span class="sxs-lookup"><span data-stu-id="4ad3e-329">Fixed: Pasting part of a Razor expression that contains whitespace results in it being reversed</span></span>

<span data-ttu-id="4ad3e-330">ASP.NET MVC 3의 시험판 버전에서는 Razor 파일에 공백이 포함 된 Razor 식의 부분을 붙여 넣을 때 결과 식 속도가 반대로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-330">In pre-release versions of ASP.NET MVC 3, when you paste a part of a Razor expression that contains whitespace into a Razor file, the resulting expression is reversed.</span></span> <span data-ttu-id="4ad3e-331">예를 들어, 다음 Razor 코드 블록을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-331">For example, consider the following Razor code block:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample6.cshtml)]

<span data-ttu-id="4ad3e-332">첫 번째 방법은 "첫 번째 param" 텍스트를 선택 하 고 두 번째 방법에 대 한 인수로 붙여 경우 결과 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-332">If you select the text "first param" in the first method and paste it as an argument into the second method, the result is as follows:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample7.cshtml)]

<span data-ttu-id="4ad3e-333">정확한 동작은 붙여넣기 작업 다음에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-333">The correct behavior is that the paste operation should result in the following:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample8.cshtml)]

<span data-ttu-id="4ad3e-334">붙여넣기 작업 동안 식이 제대로 유지 되도록 RTM 릴리스에서이 문제가 해결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-334">This issue has been fixed in the RTM release so that the expression is correctly preserved during the paste operation.</span></span>

<a id="RTM-4"></a>
### <a name="fixed-renaming-a-razor-file-that-is-opened-in-the-editor-disables-syntax-colorization-and-intellisense"></a><span data-ttu-id="4ad3e-335">구문 색 지정 및 IntelliSense 고정: 편집기에서 열려 있는 Razor 파일의 이름 바꾸기 해제</span><span class="sxs-lookup"><span data-stu-id="4ad3e-335">Fixed: Renaming a Razor file that is opened in the editor disables syntax colorization and IntelliSense</span></span>

<span data-ttu-id="4ad3e-336">구문 강조 표시 및 IntelliSense 해당 파일에 대 한 작동을 중지 하면 편집기 창에서 파일이 열릴 때 솔루션 탐색기를 사용 하 여 Razor 파일의 이름을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-336">Renaming a Razor file using Solution Explorer while the file is opened in the editor window causes syntax highlighting and IntelliSense to stop working for that file.</span></span> <span data-ttu-id="4ad3e-337">이 강조 표시 되도록 고정 및 IntelliSense는 이름 바꾸기 후 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-337">This has been fixed so that highlighting and IntelliSense are maintained after a rename.</span></span>

<a id="RTM-KI"></a>
## <a name="known-issues"></a><span data-ttu-id="4ad3e-338">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="4ad3e-338">Known Issues</span></span>

- <span data-ttu-id="4ad3e-339">NuGet 패키지 관리자 콘솔이 열려 있는 동안 Visual Studio 2010 SP1 베타를 닫으면 Visual Studio가 충돌 하 고 다시 시작 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-339">If you close Visual Studio 2010 SP1 Beta while the NuGet Package Manager Console is open, Visual Studio crashes and attempts to restart.</span></span> <span data-ttu-id="4ad3e-340">이 문제가 해결 RTM 버전의 Visual Studio 2010 s p 1입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-340">This will be fixed in the RTM release of Visual Studio 2010 SP1.</span></span>
- <span data-ttu-id="4ad3e-341">ASP.NET MVC 3 설치 프로그램은 초기 버전의 NuGet 패키지 관리자를 설치할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-341">The ASP.NET MVC 3 installer is only able to install an initial version of the NuGet package manager.</span></span> <span data-ttu-id="4ad3e-342">초기 버전을 설치한 후 NuGet을 설치할 수 있고 Visual Studio 확장 관리자를 사용 하 여 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-342">After you have installed the initial version, NuGet can be installed and updated using Visual Studio Extension Manager.</span></span> <span data-ttu-id="4ad3e-343">NuGet이 설치를 이미 있는 경우 NuGet의 최신 버전으로 업데이트 하려면 Visual Studio 확장 갤러리로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-343">If you already have NuGet installed, go to the Visual Studio Extension Gallery to update to the latest version of NuGet.</span></span>
- <span data-ttu-id="4ad3e-344">원인을 솔루션 폴더에서 새 ASP.NET MVC 3 프로젝트를 만들기는 *NullReferenceException* 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-344">Creating a new ASP.NET MVC 3 project within a solution folder causes a *NullReferenceException* error.</span></span> <span data-ttu-id="4ad3e-345">해결 방법은 솔루션의 루트에 ASP.NET MVC 3 프로젝트를 만들고 다음 솔루션 폴더로 이동 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-345">The workaround is to create the ASP.NET MVC 3 project in the root of the solution and then move it into the solution folder.</span></span>
- <span data-ttu-id="4ad3e-346">설치 관리자는 이전 버전의 ASP.NET MVC를 완료 하려면 보다 훨씬 더 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-346">The installer might take much longer than previous versions of ASP.NET MVC to complete.</span></span> <span data-ttu-id="4ad3e-347">Visual Studio 2010의 구성 요소를 업데이트 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-347">This is because it updates components of Visual Studio 2010.</span></span>
- <span data-ttu-id="4ad3e-348">ReSharper가 설치 된 경우에 IntelliSense for Razor 구문 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-348">IntelliSense for Razor syntax does not work when ReSharper is installed.</span></span> <span data-ttu-id="4ad3e-349">ReSharper가 설치 되어 ASP.NET MVC 3의 Razor IntelliSense 지원을 활용 하려고 하는 경우 항목을 참조 [Razor Intellisense and ReSharper](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) Hadi Hariri 블로그에서 함께 사용 하는 방법을 설명 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-349">If you have ReSharper installed and want to take advantage of the Razor IntelliSense support in ASP.NET MVC 3, see the entry [Razor Intellisense and ReSharper](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) on Hadi Hariri's blog, which discusses ways to use them together today.</span></span>
- <span data-ttu-id="4ad3e-350">ASP.NET MVC 3의 베타 버전을 사용 하 여 만든 CCSHTML 및 VBHTML 뷰 빌드 작업이 제대로 설정 하지 않은, 이러한 보기에서 결과로 형식 프로젝트를 게시할 때 생략 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-350">CCSHTML and VBHTML views created with the Beta version of ASP.NET MVC 3 do not have their build action set correctly, with the result that these view types are omitted when the project is published.</span></span> <span data-ttu-id="4ad3e-351">이러한 파일에 대 한 빌드 작업 값 "콘텐츠"를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-351">The Build Action value for these files should be set to "Content".</span></span> <span data-ttu-id="4ad3e-352">ASP.NET MVC 3 RTM 새 파일에 대해이 문제를 해결할 수 있지만 시험판 버전을 사용 하 여 만든 프로젝트에 대 한 기존 파일에 대 한 설정을 수정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-352">ASP.NET MVC 3 RTM fixes this issue for new files, but doesn't correct the setting for existing files for a project created with prerelease versions.</span></span>
- ![](mvc3-release-notes/_static/image3.png)
- <span data-ttu-id="4ad3e-353">설치 하는 동안 EULA 동의 대화 상자 예정 보다 작은 창에서 사용 약관을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-353">During installation, the EULA acceptance dialog box displays the license terms in a window that is smaller than intended.</span></span>
- <span data-ttu-id="4ad3e-354">Razor 뷰 (.cshtml 파일)를 편집 하는 경우 Visual Studio에서 컨트롤러 이동 메뉴 항목을 사용할 수 없으며 되며 코드 조각이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-354">When you are editing a Razor view (.cshtml file), the Go To Controller menu item in Visual Studio will not be available, and there are no code snippets.</span></span>
- <span data-ttu-id="4ad3e-355">여기서 Visual Studio 설치 되지 않은 컴퓨터에 Visual Web Developer Express에 대 한 ASP.NET MVC 3을 설치 하 고 다음 나중에 Visual Studio를 설치 하는 경우에 ASP.NET MVC 3를 다시 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-355">If you install ASP.NET MVC 3 for Visual Web Developer Express on a computer where Visual Studio is not installed, and then later install Visual Studio, you must reinstall ASP.NET MVC 3.</span></span> <span data-ttu-id="4ad3e-356">Visual Studio 및 Visual Web Developer Express는 ASP.NET MVC 3 설치 관리자가 업그레이드 하는 구성 요소를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-356">Visual Studio and Visual Web Developer Express share components that are upgraded by the ASP.NET MVC 3 installer.</span></span> <span data-ttu-id="4ad3e-357">Visual Web Developer Express가 되지 않으며 다음 나중에 Visual Web Developer Express를 설치 하는 컴퓨터에서 Visual Studio에 대 한 ASP.NET MVC 3을 설치 하는 경우 동일한 문제에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-357">The same issue applies if you install ASP.NET MVC 3 for Visual Studio on a computer that does not have Visual Web Developer Express and then later install Visual Web Developer Express.</span></span>

<a id="RTM-BC"></a>
## <a name="breaking-changes"></a><span data-ttu-id="4ad3e-358">주요 변경 사항</span><span class="sxs-lookup"><span data-stu-id="4ad3e-358">Breaking Changes</span></span>

- <span data-ttu-id="4ad3e-359">이전 버전의 ASP.NET MVC에서는 작업 필터는 몇 가지 경우에서를 제외 하 고 요청에 따라 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-359">In previous versions of ASP.NET MVC, action filters are create per request except in a few cases.</span></span> <span data-ttu-id="4ad3e-360">이 동작은 되지 보장 된 동작은 하지만 단순히 구현 정보 이며 필터에 대 한 계약 상태 비저장 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-360">This behavior was never a guaranteed behavior but merely an implementation detail and the contract for filters was to consider them stateless.</span></span> <span data-ttu-id="4ad3e-361">ASP.NET MVC 3에서 필터는 보다 적극적으로 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-361">In ASP.NET MVC 3, filters are cached more aggressively.</span></span> <span data-ttu-id="4ad3e-362">따라서 잘못 인스턴스 상태를 저장 하는 모든 사용자 지정 작업 필터는 손상 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-362">Therefore, any custom action filters which improperly store instance state might be broken.</span></span>
- <span data-ttu-id="4ad3e-363">동일한 예외 필터에 대 한 예외 필터에 대 한 실행 순서가 변경 된 *순서* 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-363">The order of execution for exception filters has changed for exception filters that have the same *Order* value.</span></span> <span data-ttu-id="4ad3e-364">예외 필터 동일한 컨트롤러에서 ASP.NET MVC 2 및 이전 버전에서는 *순서* 값의 동작 메서드는 작업 메서드의 예외 필터 전에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-364">In ASP.NET MVC 2 and earlier, exception filters on the controller that have the same *Order* value as those on an action method are executed before the exception filters on the action method.</span></span> <span data-ttu-id="4ad3e-365">일반적으로 경우가이 예외가 필터가 적용 된 경우 지정 된 없이 *순서* 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-365">This would typically be the case when exception filters are applied without a specified *Order* value.</span></span> <span data-ttu-id="4ad3e-366">ASP.NET MVC 3에서이 순서가 반대로 변경 되었습니다 가장 구체적인 예외 처리기는 먼저 실행 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-366">In ASP.NET MVC 3, this order has been reversed so that the most specific exception handler executes first.</span></span> <span data-ttu-id="4ad3e-367">이전 버전과 달리 하는 경우는 *순서* 속성을 명시적으로 지정, 필터는 지정 된 순서로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-367">As in earlier versions, if the *Order* property is explicitly specified, the filters are run in the specified order.</span></span>
- <span data-ttu-id="4ad3e-368">라는 새 속성이 *FileExtensions* 에 추가 된는 *VirtualPathProviderViewEngine* 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-368">A new property named *FileExtensions* was added to the *VirtualPathProviderViewEngine* base class.</span></span> <span data-ttu-id="4ad3e-369">ASP.NET에서는 보기를 경로 의해 (이름)가 아니라을 때 뷰만이 새 속성으로 지정 된 목록에 포함 된 파일 확장명으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-369">When ASP.NET looks up a view by path (not by name), only views with a file extension contained in the list specified by this new property are considered.</span></span> <span data-ttu-id="4ad3e-370">웹 폼 보기에 대 한 사용자 지정 파일 확장명을 사용 하도록 설정 하려면 사용자 지정 빌드 공급자가 등록 된와 공급자는 이름이 아니라 전체 경로 사용 하 여 이러한 뷰를 참조 하는 경우 응용 프로그램의 주요 변경 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-370">This is a breaking change in applications where a custom build provider is registered in order to enable a custom file extension for Web Form views and where the provider references those views by using a full path rather than a name.</span></span> <span data-ttu-id="4ad3e-371">해결 하는 값을 수정 하는 *FileExtensions* 속성을 사용자 지정 파일 확장명을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-371">The workaround is to modify the value of the *FileExtensions* property to include the custom file extension.</span></span>
- <span data-ttu-id="4ad3e-372">직접 구현 하는 사용자 지정 컨트롤러 팩터리 구현을 *IControllerFactory* 인터페이스의 새 구현을 제공 해야 *GetControllerSessionBehavior* 했던 메서드 이 릴리스에서 인터페이스에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-372">Custom controller factory implementations that directly implement the *IControllerFactory* interface must provide an implementation of the new *GetControllerSessionBehavior* method that was added to the interface in this release.</span></span> <span data-ttu-id="4ad3e-373">일반적으로 것이 좋습니다 수행 하지이 인터페이스를 직접 구현 하는 대신에서 클래스를 파생 *DefaultControllerFactory*합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-373">In general, it is recommended that you do not implement this interface directly and instead derive your class from *DefaultControllerFactory*.</span></span>

<a id="_Toc2"></a>
## <a name="changes-in-aspnet-mvc-3-rc2"></a><span data-ttu-id="4ad3e-374">ASP.NET MVC 3 r c 2의 변경 내용</span><span class="sxs-lookup"><span data-stu-id="4ad3e-374">Changes in ASP.NET MVC 3 RC2</span></span>

<span data-ttu-id="4ad3e-375">이 섹션에서는 변경 (새로운 기능 및 버그 수정) RC 릴리스 이후의 ASP.NET MVC 3 RC2 릴리스에서 내용을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-375">This section describes changes (new features and bug fixes) made in the ASP.NET MVC 3 RC2 release since the RC release.</span></span>

<a id="_Toc2_1"></a>
### <a name="project-templates-changed-to-include-jquery-144-jquery-validation-17-and-jquery-ui-186"></a><span data-ttu-id="4ad3e-376">프로젝트 템플릿이 1.4.4 jQuery, jQuery 유효성 검사 1.7 및 jQuery UI 1.8.6 포함 하도록 변경</span><span class="sxs-lookup"><span data-stu-id="4ad3e-376">Project Templates Changed to Include jQuery 1.4.4, jQuery Validation 1.7, and jQuery UI 1.8.6</span></span>

<span data-ttu-id="4ad3e-377">ASP.NET MVC 3 용 프로젝트 템플릿을 포함 최신 버전의 jQuery, jQuery 유효성 검사 및 jQuery UI입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-377">The project templates for ASP.NET MVC 3 now include the latest versions of jQuery, jQuery Validation, and jQuery UI.</span></span> <span data-ttu-id="4ad3e-378">jQuery UI 프로젝트 템플릿을 새로 추가 하 고 유용한 사용자 인터페이스 도구를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-378">jQuery UI is a new addition to the project templates and provides useful user interface widgets.</span></span> <span data-ttu-id="4ad3e-379">JQuery UI에 대 한 자세한 내용은 참조의 홈 페이지: [ http://jqueryui.com/ ](http://jqueryui.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-379">For more information about jQuery UI, visit their homepage: [http://jqueryui.com/](http://jqueryui.com/).</span></span>

<a id="_Toc2_2"></a>
### <a name="added-additionalmetadataattribute-class"></a><span data-ttu-id="4ad3e-380">추가 된 "AdditionalMetadataAttribute" 클래스</span><span class="sxs-lookup"><span data-stu-id="4ad3e-380">Added "AdditionalMetadataAttribute" Class</span></span>

<span data-ttu-id="4ad3e-381">사용할 수는 *AdditionalMetadataAttribute* 를 채우는 클래스는 *ModelMetadata.AdditionalValues* 모델 속성에 대 한 사전입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-381">You can use the *AdditionalMetadataAttribute* class to populate the *ModelMetadata.AdditionalValues* dictionary for a model property.</span></span>

<span data-ttu-id="4ad3e-382">예를 들어 뷰 모델에만 관리자에 게 표시 되어야 하는 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-382">For example, suppose a view model has properties that should be displayed only to an administrator.</span></span> <span data-ttu-id="4ad3e-383">해당 모델 키와 true로 AdminOnly를 사용 하 여 다음 예제와 같이 값으로 새 특성으로 주석을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-383">That model can be annotated with the new attribute using AdminOnly as the key and true as the value, as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample9.cs)]

<span data-ttu-id="4ad3e-384">이 메타 데이터를 사용할 수 있는 표시 또는 편집기 템플릿을 제품 보기 모델을 렌더링 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-384">This metadata is made available to any display or editor template when a product view model is rendered.</span></span> <span data-ttu-id="4ad3e-385">이 프로토콜은 사용자의 책임으로 응용 프로그램 개발자가 메타 데이터 정보를 해석 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-385">It is up to you as application developer to interpret the metadata information.</span></span>

<a id="_Toc2_3"></a>
### <a name="improved-view-scaffolding"></a><span data-ttu-id="4ad3e-386">향상 된 보기 스 캐 폴딩</span><span class="sxs-lookup"><span data-stu-id="4ad3e-386">Improved View Scaffolding</span></span>

<span data-ttu-id="4ad3e-387">뷰에 사용 되는 스 캐 폴딩 이제 T4 템플릿 템플릿 도우미 메서드를 호출을와 같은 생성 *EditorFor* 와 같은 도우미 대신 *TextBoxFor*합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-387">The T4 templates used for scaffolding views now generate calls to template helper methods such as *EditorFor* instead of helpers such as *TextBoxFor*.</span></span> <span data-ttu-id="4ad3e-388">이 변경 개선 뷰 추가 대화 상자는 뷰를 생성할 때 데이터 주석 특성의 형태로 모델에 대 한 메타 데이터에 대 한 지원이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-388">This change improves support for metadata on the model in the form of data annotation attributes when the Add View dialog box generates a view.</span></span>

<span data-ttu-id="4ad3e-389">뷰 추가 스 캐 폴딩 규칙에 따라 모델에 기본 키 정보의 사용 및 향상 된 검색에도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-389">The Add View scaffolding also includes improved detection and usage of primary key information on the model, based on convention.</span></span> <span data-ttu-id="4ad3e-390">예를 들어 뷰 추가 대화 상자는이 정보를 사용 하 여는 기본 키 값은 하지 스 캐 폴드 된 편집 가능한 폼 필드와 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-390">For example, the Add View dialog box uses this information to ensure that the primary key value is not scaffolded as an editable form field.</span></span>

<span data-ttu-id="4ad3e-391">기본 편집 및 템플릿 만들기 클라이언트 유효성 검사에 필요한 jQuery 스크립트에 대 한 참조를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-391">The default Edit and Create templates include references to the jQuery scripts needed for client validation.</span></span>

<a id="_Toc2_4"></a>
### <a name="added-htmlraw-method"></a><span data-ttu-id="4ad3e-392">추가 된 Html.Raw 메서드</span><span class="sxs-lookup"><span data-stu-id="4ad3e-392">Added Html.Raw Method</span></span>

<span data-ttu-id="4ad3e-393">기본적으로 Razor 모든 값을 HTML로 인코딩하고 엔진을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-393">By default, the Razor view engine HTML-encodes all values.</span></span> <span data-ttu-id="4ad3e-394">와 페이지에 표시 되도록 다음 코드 조각의 인사말 변수 내부 HTML를 인코딩하는 예를 들어 `<strong>Hello World!</strong>`합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-394">For example, the following code snippet encodes the HTML inside the greeting variable so that it is displayed in the page as `<strong>Hello World!</strong>`.</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample10.cshtml)]

<span data-ttu-id="4ad3e-395">새 *Html.Raw* 메서드 콘텐츠가 안전한 것으로 알려져 있는 경우 인코딩되지 않은 HTML을 표시 하는 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-395">The new *Html.Raw* method provides a simple way of displaying unencoded HTML when the content is known to be safe.</span></span> <span data-ttu-id="4ad3e-396">다음 예제에서는 동일한 문자열을 표시 하지만 문자열 태그로 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-396">The following example displays the same string, but the string is rendered as markup:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample11.cshtml)]

<a id="_Toc2_5"></a>
### <a name="renamed-controllerviewmodel-property-and-the-view-property-to-viewbag"></a><span data-ttu-id="4ad3e-397">이름이 바뀐된 "Controller.ViewModel" 속성과 "ViewBag"을 "보기" 속성</span><span class="sxs-lookup"><span data-stu-id="4ad3e-397">Renamed "Controller.ViewModel" Property and the "View" Property To "ViewBag"</span></span>

<span data-ttu-id="4ad3e-398">이전에 *ViewModel* 속성 *컨트롤러* 에 상응는 *보기* 보기의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-398">Previously, the *ViewModel* property of *Controller* corresponded to the *View* property of a view.</span></span> <span data-ttu-id="4ad3e-399">액세스 값의 하는 방법을 제공 두이 속성 모두는 *ViewDataDictionary* 동적 속성 접근자 구문을 사용 하 여 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-399">Both of these properties provide a way to access values of the *ViewDataDictionary* object using dynamic property-accessor syntax.</span></span> <span data-ttu-id="4ad3e-400">두 속성이 동일 하 게 혼동을 피하기 위해와 보다 일치 하도록 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-400">Both properties have been renamed to be the same in order to avoid confusion and to be more consistent.</span></span>

<a id="_Toc2_6"></a>
### <a name="renamed-controllersessionstateattribute-class-to-sessionstateattribute"></a><span data-ttu-id="4ad3e-401">이름이 바뀐된 "ControllerSessionStateAttribute" 클래스 "SessionStateAttribute"를</span><span class="sxs-lookup"><span data-stu-id="4ad3e-401">Renamed "ControllerSessionStateAttribute" Class to "SessionStateAttribute"</span></span>

<span data-ttu-id="4ad3e-402">*ControllerSessionStateAttribute* 클래스는 ASP.NET MVC 3의 RC 버전에서 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-402">The *ControllerSessionStateAttribute* class was introduced in the RC release of ASP.NET MVC 3.</span></span> <span data-ttu-id="4ad3e-403">더 간결한 되도록 속성 이름이 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-403">The property was renamed to be more succinct.</span></span>

<a id="_Toc2_7"></a>
### <a name="renamed-remoteattribute-fields-property-to-additionalfields"></a><span data-ttu-id="4ad3e-404">이름이 바뀐된 RemoteAttribute "Fields" 속성을 "AdditionalFields"</span><span class="sxs-lookup"><span data-stu-id="4ad3e-404">Renamed RemoteAttribute "Fields" Property to "AdditionalFields"</span></span>

<span data-ttu-id="4ad3e-405">*RemoteAttribute* 클래스의 *필드* 속성 사용자 간에 일부 혼란이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-405">The *RemoteAttribute* class's *Fields* property caused some confusion among users.</span></span> <span data-ttu-id="4ad3e-406">이 속성을 이름 바꾸기 *AdditionalFields* 의도 된을 명확히 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-406">Renaming this property to *AdditionalFields* clarifies its intent.</span></span>

<a id="_Toc2_8"></a>
### <a name="renamed-skiprequestvalidationattribute-to-allowhtmlattribute"></a><span data-ttu-id="4ad3e-407">"AllowHtmlAttribute"를 "SkipRequestValidationAttribute" 이름이 변경</span><span class="sxs-lookup"><span data-stu-id="4ad3e-407">Renamed "SkipRequestValidationAttribute" to "AllowHtmlAttribute"</span></span>

<span data-ttu-id="4ad3e-408">*SkipRequestValidationAttribute* 특성으로 변경 되어 *AllowHtmlAttribute* 해당 용도 더 잘 나타내기 위해.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-408">The *SkipRequestValidationAttribute* attribute was renamed to *AllowHtmlAttribute* to better represent its intended usage.</span></span>

<a id="_Toc2_9"></a>
### <a name="changed-htmlvalidationmessage-method-to-display-the-first-useful-error-message"></a><span data-ttu-id="4ad3e-409">첫 번째 유용한 오류 메시지를 표시 하려면 변경 된 "Html.ValidationMessage" 메서드</span><span class="sxs-lookup"><span data-stu-id="4ad3e-409">Changed "Html.ValidationMessage" Method to Display the First Useful Error Message</span></span>

<span data-ttu-id="4ad3e-410">*Html.ValidationMessage* 메서드는 단순히 첫 번째 오류를 표시 하는 대신 첫 번째 유용한 오류 메시지를 표시 하도록 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-410">The *Html.ValidationMessage* method was fixed to show the first useful error message instead of simply displaying the first error.</span></span>

<span data-ttu-id="4ad3e-411">모델 바인딩 중에서 *ModelState* 사전 모델 자체를 포함 하는 속성에 대 한 오류 메시지와 함께 여러 소스에서 채울 수 있습니다 (구현 하는 경우 *IValidatableObject* )를 속성에 적용 되는 유효성 검사 특성 및 속성을 액세스 하는 동안 발생 한 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-411">During model binding, the *ModelState* dictionary can be populated from multiple sources with error messages about the property, including from the model itself (if it implements *IValidatableObject*), from validation attributes applied to the property, and from exceptions thrown while the property is being accessed.</span></span>

<span data-ttu-id="4ad3e-412">경우는 *Html.ValidationMessage* 유효성 검사 메시지를 표시 하는 메서드, 아니기 때문에이 일반적으로 최종 사용자에 대 한 예외를 포함 하는 모델 상태 항목을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-412">When the *Html.ValidationMessage* method displays a validation message, it skips model-state entries that include an exception, because these are generally not intended for the end user.</span></span> <span data-ttu-id="4ad3e-413">대신, 메서드는 예외와 연결 되지 않으며 해당 메시지를 표시 하는 첫 번째 유효성 검사 메시지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-413">Instead, the method looks for the first validation message that is not associated with an exception and displays that message.</span></span> <span data-ttu-id="4ad3e-414">이러한 메시지가 없는 항목이 있으면 첫 번째 예외와 관련 된 일반 오류 메시지에 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-414">If no such message is found, it defaults to a generic error message that is associated with the first exception.</span></span>

<a id="_Toc2_10"></a>
### <a name="fixed-model-declaration-to-not-add-whitespace-to-the-document"></a><span data-ttu-id="4ad3e-415">고정 @model 문서에 공백을 추가 하지 않는 선언</span><span class="sxs-lookup"><span data-stu-id="4ad3e-415">Fixed @model Declaration to not Add Whitespace to the Document</span></span>

<span data-ttu-id="4ad3e-416">이전 릴리스에서 <em> @model </em> 보기의 맨 위에 선언은 렌더링된 된 HTML 출력에 빈 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-416">In earlier releases, the <em>@model</em> declaration at the top of a view added a blank line to the rendered HTML output.</span></span> <span data-ttu-id="4ad3e-417">이 선언에 공백이 발생 하지 않도록 있도록 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-417">This has been fixed so that the declaration does not introduce whitespace.</span></span>

<a id="_Toc2_11"></a>
### <a name="added-fileextensions-property-to-view-engines-to-support-engine-specific-file-names"></a><span data-ttu-id="4ad3e-418">엔진-특정 파일 이름을 지원 하도록 뷰 엔진에 추가 된 "FileExtensions" 속성</span><span class="sxs-lookup"><span data-stu-id="4ad3e-418">Added "FileExtensions" Property to View Engines to Support Engine-Specific File Names</span></span>

<span data-ttu-id="4ad3e-419">뷰 엔진 다음 예제와 같이 명시적 뷰 경로 사용 하는 보기를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-419">A view engine can return a view using an explicit view path as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample12.cs)]

<span data-ttu-id="4ad3e-420">뷰를 렌더링 하는 첫 번째 뷰 엔진이 항상 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-420">The first view engine always attempts to render the view.</span></span> <span data-ttu-id="4ad3e-421">기본적으로 Web Forms 뷰 엔진은 첫 번째 뷰 엔진입니다. Web Forms 엔진 Razor 뷰를 렌더링할 수 없으면 때문에 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-421">By default, the Web Forms view engine is the first view engine; because the Web Forms engine cannot render a Razor view, an error occurs.</span></span> <span data-ttu-id="4ad3e-422">뷰 엔진 생깁니다는 *FileExtensions* 지 원하는 파일 확장명을 지정 하는 데 사용 되는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-422">View engines now have a *FileExtensions* property that is used to specify which file extensions they support.</span></span> <span data-ttu-id="4ad3e-423">ASP.NET 뷰 엔진 파일을 렌더링할 수 있는지 여부를 결정 하는 경우이 속성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-423">This property is checked when ASP.NET determines whether a view engine can render a file.</span></span> <span data-ttu-id="4ad3e-424">이 주요 변경 내용 및에 포함 된 자세한 세부 정보는 [주요 변경 내용](#_Toc2_BC) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-424">This is a breaking change and more details are included in the [Breaking Changes](#_Toc2_BC) section of this document.</span></span>

<a id="_Toc2_12"></a>
### <a name="fixed-labelfor-helper-to-emit-the-correct-value-for-the-for-attribute"></a><span data-ttu-id="4ad3e-425">"For" 특성에 대 한 올바른 값을 내보내는 데 고정된 "LabelFor" 도우미</span><span class="sxs-lookup"><span data-stu-id="4ad3e-425">Fixed "LabelFor" Helper to Emit the Correct Value for the "For" Attribute</span></span>

<span data-ttu-id="4ad3e-426">버그 수정 위치는 *LabelFor* 렌더링 하는 메서드는 *에 대 한* 일치 하는 특성의 *입력* 요소의 *이름* 특성을 대신 ID</span><span class="sxs-lookup"><span data-stu-id="4ad3e-426">A bug was fixed where the *LabelFor* method rendered a *for* attribute that matches the *input* element's *name* attribute instead of its ID.</span></span> <span data-ttu-id="4ad3e-427">W3C에 따라는 *에 대 한* 특성이 일치 해야는 *입력* 요소의 id입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-427">According to the W3C, the *for* attribute should match the *input* element's ID.</span></span>

<a id="_Toc2_13"></a>
### <a name="fixed-renderaction-method-to-give-explicit-values-precedence-during-model-binding"></a><span data-ttu-id="4ad3e-428">모델 바인딩 중 명시적 값 우선 순위 RenderAction"고정된" 메서드</span><span class="sxs-lookup"><span data-stu-id="4ad3e-428">Fixed "RenderAction" Method to Give Explicit Values Precedence During Model Binding</span></span>

<span data-ttu-id="4ad3e-429">이전 버전에서는에 전달 된 명시적 값은 *RenderAction* 메서드는 자식 작업 내 모델 바인딩 중 현재 폼 값 무시 되 고 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-429">In earlier versions, explicit values that were passed to the *RenderAction* method were being ignored in favor of the current form values during model binding inside a child action.</span></span> <span data-ttu-id="4ad3e-430">수정이 반영 명시적 값 모델 바인딩 중 우선 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-430">The fix ensures that explicit values take precedence during model binding.</span></span>

<a id="_Toc2_BC"></a>
## <a name="breaking-changes"></a><span data-ttu-id="4ad3e-431">주요 변경 사항</span><span class="sxs-lookup"><span data-stu-id="4ad3e-431">Breaking Changes</span></span>

- <span data-ttu-id="4ad3e-432">이전 버전의 ASP.NET MVC에서는 작업 필터 몇 가지 경우에서를 제외 하 고 요청에 따라 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-432">In previous versions of ASP.NET MVC, action filters were created per request except in a few cases.</span></span> <span data-ttu-id="4ad3e-433">이 동작은 되지 보장 된 동작은 하지만 단순히 구현 정보 이며 필터에 대 한 계약 상태 비저장 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-433">This behavior was never a guaranteed behavior but merely an implementation detail and the contract for filters was to consider them stateless.</span></span> <span data-ttu-id="4ad3e-434">ASP.NET MVC 3에서 필터는 보다 적극적으로 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-434">In ASP.NET MVC 3, filters are cached more aggressively.</span></span> <span data-ttu-id="4ad3e-435">따라서 잘못 인스턴스 상태를 저장 하는 모든 사용자 지정 작업 필터는 손상 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-435">Therefore, any custom action filters which improperly store instance state might be broken.</span></span>
- <span data-ttu-id="4ad3e-436">동일한 예외 필터에 대 한 예외 필터에 대 한 실행 순서가 변경 된 *순서* 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-436">The order of execution for exception filters has changed for exception filters that have the same *Order* value.</span></span> <span data-ttu-id="4ad3e-437">예외 필터를 동일한 컨트롤러에서 ASP.NET MVC 2 및 이전 버전에서는 *순서* 는 작업 메서드의 예외 필터 전에 실행의 동작 메서드 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-437">In ASP.NET MVC 2 and earlier, exception filters on the controller that had the same *Order* value as those on an action method were executed before the exception filters on the action method.</span></span> <span data-ttu-id="4ad3e-438">일반적으로 경우가이 예외가 필터가 적용 된 경우 지정 된 없이 *순서* 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-438">This would typically be the case when exception filters were applied without a specified *Order* value.</span></span> <span data-ttu-id="4ad3e-439">ASP.NET MVC 3에서이 순서가 반대로 변경 되었습니다 가장 구체적인 예외 처리기는 먼저 실행 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-439">In ASP.NET MVC 3, this order has been reversed so that the most specific exception handler executes first.</span></span> <span data-ttu-id="4ad3e-440">이전 버전과 달리 하는 경우는 *순서* 속성을 명시적으로 지정, 필터는 지정 된 순서로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-440">As in earlier versions, if the *Order* property is explicitly specified, the filters are run in the specified order.</span></span>
- <span data-ttu-id="4ad3e-441">라는 새 속성이 *FileExtensions* 에 추가 된는 *VirtualPathProviderViewEngine* 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-441">A new property named *FileExtensions* was added to the *VirtualPathProviderViewEngine* base class.</span></span> <span data-ttu-id="4ad3e-442">ASP.NET에서는 보기를 경로 의해 (이름)가 아니라을 때 뷰만이 새 속성으로 지정 된 목록에 포함 된 파일 확장명으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-442">When ASP.NET looks up a view by path (not by name), only views with a file extension contained in the list specified by this new property are considered.</span></span> <span data-ttu-id="4ad3e-443">웹 폼 보기에 대 한 사용자 지정 파일 확장명을 사용 하도록 설정 하려면 사용자 지정 빌드 공급자가 등록 된와 공급자는 이름이 아니라 전체 경로 사용 하 여 이러한 뷰를 참조 하는 경우 응용 프로그램의 주요 변경 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-443">This is a breaking change in applications where a custom build provider is registered in order to enable a custom file extension for Web Form views and where the provider references those views by using a full path rather than a name.</span></span> <span data-ttu-id="4ad3e-444">해결 하는 값을 수정 하는 *FileExtensions* 속성을 사용자 지정 파일 확장명을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-444">The workaround is to modify the value of the *FileExtensions* property to include the custom file extension.</span></span>
- <span data-ttu-id="4ad3e-445">직접 구현 하는 사용자 지정 컨트롤러 팩터리 구현을 <em>IControllerFactory</em> 인터페이스의 새 구현을 제공 해야 <em>GetControllerSessionBehavior</em> <em> 이 릴리스에서 인터페이스에 추가 된 메서드</em>합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-445">Custom controller factory implementations that directly implement the <em>IControllerFactory</em> interface must provide an implementation of the new <em>GetControllerSessionBehavior</em><em>method that was added to the interface in this release</em>.</span></span> <span data-ttu-id="4ad3e-446">일반적으로 것이 좋습니다 수행 하지이 인터페이스를 직접 구현 하는 대신에서 클래스를 파생 <em>DefaultControllerFactory</em>합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-446">In general, it is recommended that you do not implement this interface directly and instead derive your class from <em>DefaultControllerFactory</em>.</span></span>

<a id="_Toc2_KI"></a>
## <a name="known-issues"></a><span data-ttu-id="4ad3e-447">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="4ad3e-447">Known Issues</span></span>

- <span data-ttu-id="4ad3e-448">ASP.NET MVC 3 설치 프로그램은 초기 버전의 NuGet 패키지 관리자를 설치할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-448">The ASP.NET MVC 3 installer is only able to install an initial version of the NuGet package manager.</span></span> <span data-ttu-id="4ad3e-449">초기 버전을 설치한 후 NuGet을 설치할 수 있고 Visual Studio 확장 관리자를 사용 하 여 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-449">After you have installed the initial version, NuGet can be installed and updated using Visual Studio Extension Manager.</span></span> <span data-ttu-id="4ad3e-450">NuGet이 설치를 이미 있는 경우 NuGet의 최신 버전으로 업데이트 하려면 Visual Studio 확장 갤러리로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-450">If you already have NuGet installed, go to the Visual Studio Extension Gallery to update to the latest version of NuGet.</span></span>
- <span data-ttu-id="4ad3e-451">원인을 솔루션 폴더에서 새 ASP.NET MVC 3 프로젝트를 만들기는 *NullReferenceException* 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-451">Creating a new ASP.NET MVC 3 project within a solution folder causes a *NullReferenceException* error.</span></span> <span data-ttu-id="4ad3e-452">해결 방법은 솔루션의 루트에 ASP.NET MVC 3 프로젝트를 만들고 다음 솔루션 폴더로 이동 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-452">The workaround is to create the ASP.NET MVC 3 project in the root of the solution and then move it into the solution folder.</span></span>
- <span data-ttu-id="4ad3e-453">설치 관리자는 이전 버전의 ASP.NET MVC를 완료 하려면 보다 훨씬 더 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-453">The installer might take much longer than previous versions of ASP.NET MVC to complete.</span></span> <span data-ttu-id="4ad3e-454">Visual Studio 2010의 구성 요소를 업데이트 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-454">This is because it updates components of Visual Studio 2010.</span></span>
- <span data-ttu-id="4ad3e-455">ReSharper가 설치 된 경우에 IntelliSense for Razor 구문 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-455">IntelliSense for Razor syntax does not work when ReSharper is installed.</span></span> <span data-ttu-id="4ad3e-456">ReSharper가 설치 되어 ASP.NET MVC 3 r c 2의 Razor IntelliSense 지원을 활용 하려고 하는 경우 항목을 참조 [Razor Intellisense and ReSharper](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) Hadi Hariri 블로그에서 함께 사용 하는 방법을 설명 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-456">If you have ReSharper installed and want to take advantage of the Razor IntelliSense support in ASP.NET MVC 3 RC2, see the entry [Razor Intellisense and ReSharper](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) on Hadi Hariri's blog, which discusses ways to use them together today.</span></span>
- <span data-ttu-id="4ad3e-457">ASP.NET MVC 3의 베타 버전을 사용 하 여 만든 CSHTML 및 VBHTML 뷰 빌드 작업이 제대로 설정 하지 않은, 이러한 보기에서 결과로 형식 프로젝트를 게시할 때 생략 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-457">CSHTML and VBHTML views created with the Beta version of ASP.NET MVC 3 do not have their build action set correctly, with the result that these view types are omitted when the project is published.</span></span> <span data-ttu-id="4ad3e-458">*빌드 작업* 콘텐츠를 설정 해야 이러한 파일에 대 한 값 "입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-458">The *Build Action* value for these files should be set to Content".</span></span> <span data-ttu-id="4ad3e-459">ASP.NET MVC 3 RC2 새 파일에 대해이 문제를 해결할 수 있지만 베타 버전을 사용 하 여 만든 프로젝트에 대 한 기존 파일에 대 한 설정을 수정 하지 않습니다.![](mvc3-release-notes/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="4ad3e-459">ASP.NET MVC 3 RC2 fixes this issue for new files, but doesn't correct the setting for existing files for a project created with the Beta version.![](mvc3-release-notes/_static/image4.png)</span></span>
- <span data-ttu-id="4ad3e-460">설치 하는 동안 EULA 동의 대화 상자 예정 보다 작은 창에서 사용 약관을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-460">During installation, the EULA acceptance dialog box displays the license terms in a window that is smaller than intended.</span></span>
- <span data-ttu-id="4ad3e-461">Razor 뷰 (.cshtml 파일)를 편집 하는 경우 Visual Studio에서 컨트롤러 이동 메뉴 항목을 사용할 수 없으며 되며 코드 조각이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-461">When you are editing a Razor view (.cshtml file), the Go To Controller menu item in Visual Studio will not be available, and there are no code snippets.</span></span>
- <span data-ttu-id="4ad3e-462">여기서 Visual Studio 설치 되지 않은 컴퓨터에 Visual Web Developer Express에 대 한 ASP.NET MVC 3을 설치 하 고 다음 나중에 Visual Studio를 설치 하는 경우에 ASP.NET MVC 3를 다시 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-462">If you install ASP.NET MVC 3 for Visual Web Developer Express on a computer where Visual Studio is not installed, and then later install Visual Studio, you must reinstall ASP.NET MVC 3.</span></span> <span data-ttu-id="4ad3e-463">Visual Studio 및 Visual Web Developer Express는 ASP.NET MVC 3 설치 관리자가 업그레이드 하는 구성 요소를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-463">Visual Studio and Visual Web Developer Express share components that are upgraded by the ASP.NET MVC 3 installer.</span></span> <span data-ttu-id="4ad3e-464">Visual Web Developer Express가 되지 않으며 다음 나중에 Visual Web Developer Express를 설치 하는 컴퓨터에서 Visual Studio에 대 한 ASP.NET MVC 3을 설치 하는 경우 동일한 문제에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-464">The same issue applies if you install ASP.NET MVC 3 for Visual Studio on a computer that does not have Visual Web Developer Express and then later install Visual Web Developer Express.</span></span>
- <span data-ttu-id="4ad3e-465">ASP.NET MVC 3 RC 2를 설치 합니다. 이미 설치 되어 있는 경우 NuGet을 업데이트 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-465">Installing ASP.NET MVC 3 RC 2 does not update NuGet if you already have it installed.</span></span> <span data-ttu-id="4ad3e-466">NuGet을 업그레이드 하는 Visual Studio 확장 관리자으로 이동 하세요.으로 표시 되어야 사용 가능한 업데이트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-466">To upgrade NuGet, go to the Visual Studio Extension manager and it should show up as an available update.</span></span> <span data-ttu-id="4ad3e-467">NuGet에서에서 최신 버전으로 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-467">You can upgrade NuGet to the latest release from there.</span></span>

<a id="TOC_ASP_NET_3_RC"></a>
## <a name="aspnet-mvc-3-release-candidate"></a><span data-ttu-id="4ad3e-468">ASP.NET MVC 3 릴리스 후보</span><span class="sxs-lookup"><span data-stu-id="4ad3e-468">ASP.NET MVC 3 Release Candidate</span></span>

<span data-ttu-id="4ad3e-469">ASP.NET MVC 릴리스 후보는 2010 년 11 월 9 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-469">ASP.NET MVC Release Candidate was released on November 9, 2010.</span></span>

<a id="_Toc276711785"></a>
## <a name="new-features-in-aspnet-mvc-3-rc"></a><span data-ttu-id="4ad3e-470">ASP.NET MVC 3 RC의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="4ad3e-470">New Features in ASP.NET MVC 3 RC</span></span>

<span data-ttu-id="4ad3e-471">이 섹션에 도입 된 기능에 설명에서 베타 릴리스 이후의 ASP.NET MVC 3 RC 릴리스 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-471">This section describes features that have been introduced in the ASP.NET MVC 3 RC release since the Beta release.</span></span>

<a id="_Toc276711786"></a>
### <a name="nuget-package-manager"></a><span data-ttu-id="4ad3e-472">NuGet 패키지 관리자</span><span class="sxs-lookup"><span data-stu-id="4ad3e-472">NuGet Package Manager</span></span>

<span data-ttu-id="4ad3e-473">ASP.NET MVC 3에는 NuGet 패키지 관리자 (이전의 NuPack)는 Visual Studio 프로젝트에 라이브러리와 도구를 추가 하기 위한 통합된 패키지 관리 도구에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-473">ASP.NET MVC 3 includes the NuGet Package Manager (formerly known as NuPack), which is an integrated package management tool for adding libraries and tools to Visual Studio projects.</span></span> <span data-ttu-id="4ad3e-474">이 도구는 개발자가 해당 원본 트리로 라이브러리를 지금 수행 하는 단계를 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-474">This tool automates the steps that developers take today to get a library into their source tree.</span></span>

<span data-ttu-id="4ad3e-475">NuGet 명령줄 도구, Visual Studio 상황에 맞는 메뉴에서 Visual Studio 2010 내는 통합된 콘솔 창 및 PowerShell cmdlet 집합으로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-475">You can work with NuGet as a command-line tool, as an integrated console window inside Visual Studio 2010, from the Visual Studio context menu, and as a set of PowerShell cmdlets.</span></span>

<span data-ttu-id="4ad3e-476">NuGet에 대 한 자세한 내용은 참조는 [Nuget 설명서](https://docs.microsoft.com/nuget/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-476">For more information about NuGet, read the [Nuget Documentation](https://docs.microsoft.com/nuget/).</span></span>

<a id="_Toc276711787"></a>
### <a name="improved-new-project-dialog-box"></a><span data-ttu-id="4ad3e-477">향상 "새 프로젝트" 대화 상자</span><span class="sxs-lookup"><span data-stu-id="4ad3e-477">Improved "New Project" Dialog Box</span></span>

<span data-ttu-id="4ad3e-478">새 프로젝트를 만들 때 새 프로젝트 대화 상자 이제 수 있습니다는 뷰 엔진이 뿐만 아니라 ASP.NET MVC 프로젝트 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-478">When you create a new project, the New Project dialog box now lets you specify the view engine as well as an ASP.NET MVC project type.</span></span>

![](mvc3-release-notes/_static/image5.png)

<span data-ttu-id="4ad3e-479">이 릴리스에서 템플릿과 보기 대화 상자에 나열 된 엔진의 목록을 수정에 대 한 지원이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-479">Support for modifying the list of templates and view engines listed in the dialog box is included in this release.</span></span>

<span data-ttu-id="4ad3e-480">기본 템플릿에 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-480">The default templates are the following:</span></span>

<span data-ttu-id="4ad3e-481">빈 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-481">Empty.</span></span> <span data-ttu-id="4ad3e-482">ASP.NET MVC 스타일, 기본 및 기본 JavaScript 파일을 포함 하는 스크립트 디렉터리를 포함 하는 Site.css 파일 ASP.NET MVC 프로젝트에 대 한 기본 디렉터리 구조를 포함 하 여 ASP.NET MVC 프로젝트에 대 한 파일의 최소 집합을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-482">Contains a minimal set of files for an ASP.NET MVC project, including the default directory structure for ASP.NET MVC projects, a Site.css file that contains the default ASP.NET MVC styles, and a Scripts directory that contains the default JavaScript files.</span></span>

<span data-ttu-id="4ad3e-483">인터넷 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-483">Internet Application.</span></span> <span data-ttu-id="4ad3e-484">ASP.NET MVC와 함께 멤버 자격 공급자를 사용 하는 방법을 보여 주는 샘플 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-484">Contains sample functionality that demonstrates how to use the membership provider with ASP.NET MVC.</span></span>

<span data-ttu-id="4ad3e-485">대화 상자에 표시 되는 프로젝트 템플릿 목록에서 Windows 레지스트리가에 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-485">The list of project templates that is displayed in the dialog box is specified in the Windows registry.</span></span>

<a id="_Toc276711788"></a>
### <a name="sessionless-controllers"></a><span data-ttu-id="4ad3e-486">Sessionless 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="4ad3e-486">Sessionless Controllers</span></span>

<span data-ttu-id="4ad3e-487">새 *ControllerSessionStateAttribute* 더 제어할 세션 상태 동작을 통해 컨트롤러에 대 한 지정 하 여 한 [System.Web.SessionState.SessionStateBehavior](https://msdn.microsoft.com/library/system.web.sessionstate.sessionstatebehavior.aspx) 열거형 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-487">The new *ControllerSessionStateAttribute* gives you more control over session-state behavior for controllers by specifying a [System.Web.SessionState.SessionStateBehavior](https://msdn.microsoft.com/library/system.web.sessionstate.sessionstatebehavior.aspx) enumeration value.</span></span>

<span data-ttu-id="4ad3e-488">다음 예제에는 컨트롤러에 대 한 모든 요청에 대 한 세션 상태를 해제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-488">The following example shows how to turn off session state for all requests to a controller.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample13.cs)]

<span data-ttu-id="4ad3e-489">다음 예제에서는 컨트롤러에 대 한 모든 요청에 대 한 읽기 전용 세션 상태를 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-489">The following example shows how to set read-only session state for all requests to a controller.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample14.cs)]

<a id="_Toc276711789"></a>
### <a name="new-validation-attributes"></a><span data-ttu-id="4ad3e-490">새 유효성 검사 특성</span><span class="sxs-lookup"><span data-stu-id="4ad3e-490">New Validation Attributes</span></span>

#### <a name="compareattribute"></a><span data-ttu-id="4ad3e-491">CompareAttribute</span><span class="sxs-lookup"><span data-stu-id="4ad3e-491">CompareAttribute</span></span>

<span data-ttu-id="4ad3e-492">새 *CompareAttribute* 유효성 검사 특성을 사용 하면 모델의 두 가지 다른 속성의 값을 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-492">The new *CompareAttribute* validation attribute lets you compare the values of two different properties of a model.</span></span> <span data-ttu-id="4ad3e-493">다음 예제에서는 *ComparePassword* 속성 일치 해야 합니다는 *암호* 필드 유효화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-493">In the following example, the *ComparePassword* property must match the *Password* field in order to be valid.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample15.cs)]

#### <a name="remoteattribute"></a><span data-ttu-id="4ad3e-494">RemoteAttribute</span><span class="sxs-lookup"><span data-stu-id="4ad3e-494">RemoteAttribute</span></span>

<span data-ttu-id="4ad3e-495">새 *RemoteAttribute* 유효성 검사 특성에서는 클라이언트 쪽 유효성 검사 메서드를 호출 하는 실제 유효성 검사 논리를 수행 하는 서버에 매핑함으로써 jQuery 유효성 검사 플러그 인의 원격 검사기 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-495">The new *RemoteAttribute* validation attribute takes advantage of the jQuery Validation plug-in's remote validator, which enables client-side validation to call a method on the server that performs the actual validation logic.</span></span>

<span data-ttu-id="4ad3e-496">다음 예제에서는 *UserName* 속성에는 *RemoteAttribute* 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-496">In the following example, the *UserName* property has the *RemoteAttribute* applied.</span></span> <span data-ttu-id="4ad3e-497">클라이언트 유효성 검사는 작업을 호출 합니다 편집 보기에서이 속성을 편집할 때 *UserNameAvailable* 에 *UsersController* 이 필드의 유효성을 검사 하기 위해 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-497">When editing this property in an Edit view, client validation will call an action named *UserNameAvailable* on the *UsersController* class in order to validate this field.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample16.cs)]

<span data-ttu-id="4ad3e-498">다음 예제에서는 해당 컨트롤러를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-498">The following example shows the corresponding controller.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample17.cs)]

<span data-ttu-id="4ad3e-499">기본적으로 특성에 적용 되는 속성 이름 쿼리 문자열 매개 변수로 작업 메서드에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-499">By default, the property name that the attribute is applied to is sent to the action method as a query-string parameter.</span></span>

<a id="_Toc276711790"></a>
### <a name="new-overloads-for-labelfor-and-labelformodel-methods"></a><span data-ttu-id="4ad3e-500">"LabelFor" 및 "LabelForModel" 메서드에 대 한 새 오버 로드</span><span class="sxs-lookup"><span data-stu-id="4ad3e-500">New Overloads for "LabelFor" and "LabelForModel" Methods</span></span>

<span data-ttu-id="4ad3e-501">에 대 한 추가 된 새 오버 로드는 *LabelFor* 및 *LabelForModel* 레이블 텍스트를 지정할 수 있는 메서드.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-501">New overloads have been added for the *LabelFor* and *LabelForModel* methods that let you specify the label text.</span></span> <span data-ttu-id="4ad3e-502">다음 예제에서는 이러한 오버 로드를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-502">The following example shows how to use these overloads.</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample18.cshtml)]

<a id="_Toc276711791"></a>
### <a name="child-action-output-caching"></a><span data-ttu-id="4ad3e-503">자식 동작 출력 캐싱</span><span class="sxs-lookup"><span data-stu-id="4ad3e-503">Child Action Output Caching</span></span>

<span data-ttu-id="4ad3e-504">*OutputCacheAttribute* 자식 작업을 사용 하 여 호출의 출력 캐싱을 지원는 *Html.RenderAction* 또는 *Html.Action* 도우미 메서드.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-504">The *OutputCacheAttribute* supports output caching of child actions that are called by using the *Html.RenderAction* or *Html.Action* helper methods.</span></span> <span data-ttu-id="4ad3e-505">다음 예제에서는 다른 작업을 호출 하는 뷰를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-505">The following example shows a view that calls another action.</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample19.cshtml)]

<span data-ttu-id="4ad3e-506">*GetDate* 동작으로 주석이 추가 된 *OutputCacheAttribute*:</span><span class="sxs-lookup"><span data-stu-id="4ad3e-506">The *GetDate* action is annotated with the *OutputCacheAttribute*:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample20.cs)]

<span data-ttu-id="4ad3e-507">이 코드를 실행 하는 경우 Html.Action("GetDate")에 대 한 호출의 결과 100 초 동안 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-507">When this code runs, the result of the call to Html.Action("GetDate") is cached for 100 seconds.</span></span>

<a id="_Toc276711792"></a>
### <a name="add-view-dialog-box-improvements"></a><span data-ttu-id="4ad3e-508">"뷰 추가" 대화 상자 개선 사항</span><span class="sxs-lookup"><span data-stu-id="4ad3e-508">"Add View" Dialog Box Improvements</span></span>

<span data-ttu-id="4ad3e-509">강력한 형식의 뷰를 추가 하면 보기 추가 대화 상자를 이제 많은 코어.NET Framework 형식과 같은 이전 릴리스에서 보다 더 많은 적용 되지 형식을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-509">When you add a strongly typed view, the Add View dialog box now filters out more non-applicable types than in previous releases, such as many core .NET Framework types.</span></span> <span data-ttu-id="4ad3e-510">또한 목록 클래스 이름으로 더욱 쉽게 형식을 찾을 정규화 된 형식 이름으로 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-510">Also, the list is now sorted by the class name and not by the fully qualified type name, which makes it easier to find types.</span></span> <span data-ttu-id="4ad3e-511">예를 들어 유형 이름 다음 예제와 같이 이제 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-511">For example, the type name is now displayed as in the following example:</span></span>

<span data-ttu-id="4ad3e-512">응용 프로그램 이름 (네임 스페이스)</span><span class="sxs-lookup"><span data-stu-id="4ad3e-512">ClassName (namespace)</span></span>

<span data-ttu-id="4ad3e-513">이전 릴리스에서이 되어 표시 된 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-513">In earlier releases, this would have been displayed as the following:</span></span>

<span data-ttu-id="4ad3e-514">Namespace.ClassName</span><span class="sxs-lookup"><span data-stu-id="4ad3e-514">Namespace.ClassName</span></span>

<a id="_Toc276711793"></a>
### <a name="granular-request-validation"></a><span data-ttu-id="4ad3e-515">Granular Request Validation</span><span class="sxs-lookup"><span data-stu-id="4ad3e-515">Granular Request Validation</span></span>

<span data-ttu-id="4ad3e-516">*제외* 속성 *ValidateInputAttribute* 더 이상 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-516">The *Exclude* property of *ValidateInputAttribute* no longer exists.</span></span> <span data-ttu-id="4ad3e-517">대신, 모델 바인딩 중에 모델의 특정 속성에 대 한 생략 요청 유효성 검사를 사용 하 여 새 *SkipRequestValidationAttribute*합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-517">Instead, to have request validation skipped for specific properties of a model during model binding, use the new *SkipRequestValidationAttribute*.</span></span>

<span data-ttu-id="4ad3e-518">예를 들어 동작 메서드가 블로그 게시물을 편집 하는 데는 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-518">For example, suppose an action method is used to edit a blog post:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample21.cs)]

<span data-ttu-id="4ad3e-519">다음 예제는 블로그 게시물에 대 한 뷰 모델을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-519">The following example shows the view model for a blog post.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample22.cs)]

<span data-ttu-id="4ad3e-520">사용자가 Description 속성에 대 한 일부 태그, 모델 바인딩 요청 유효성 검사로 인해 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-520">When a user submits some markup for the Description property, model binding will fail due to request validation.</span></span> <span data-ttu-id="4ad3e-521">블로그 게시물 설명에 대 한 모델 바인딩 중 요청 유효성 검사를 사용 하지 않으려면 적용 된 *SkipRequpestValidationAttribute* 이 예제에 나와 있는 것 처럼 속성에: 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-521">To disable request validation during model binding for the blog post Description, apply the *SkipRequpestValidationAttribute* to the property, as shown in this example:.</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample23.cs)]

<span data-ttu-id="4ad3e-522">모델의 모든 속성에 대 한 요청 유효성 검사를 해제 하려면 적용 해도 *ValidateInputAttribute* 값 *false* 동작 메서드에:</span><span class="sxs-lookup"><span data-stu-id="4ad3e-522">Alternatively, to turn off request validation for every property of the model, apply *ValidateInputAttribute* with a value of *false* to the action method:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample24.cs)]

<a id="_Toc276711794"></a>
## <a name="breaking-changes"></a><span data-ttu-id="4ad3e-523">주요 변경 사항</span><span class="sxs-lookup"><span data-stu-id="4ad3e-523">Breaking Changes</span></span>

- <span data-ttu-id="4ad3e-524">동일한 예외 필터에 대 한 예외 필터에 대 한 실행 순서가 변경 된 *순서* 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-524">The order of execution for exception filters has changed for exception filters that have the same *Order* value.</span></span> <span data-ttu-id="4ad3e-525">예외 필터를 동일한 컨트롤러에서 ASP.NET MVC 2 및 이전 버전에서는 *순서* 는 작업 메서드의 예외 필터 전에 실행의 동작 메서드 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-525">In ASP.NET MVC 2 and earlier, exception filters on the controller that had the same *Order* as those on an action method were executed before the exception filters on the action method.</span></span> <span data-ttu-id="4ad3e-526">일반적으로 경우가이 예외가 필터가 적용 된 경우 지정 된 없이 *순서* 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-526">This would typically be the case when exception filters were applied without a specified *Order* value.</span></span> <span data-ttu-id="4ad3e-527">ASP.NET MVC 3에서이 순서가 반대로 변경 되었습니다 가장 구체적인 예외 처리기는 먼저 실행 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-527">In ASP.NET MVC 3, this order has been reversed so that the most specific exception handler executes first.</span></span> <span data-ttu-id="4ad3e-528">이전 버전과 달리 하는 경우는 *순서* 속성을 명시적으로 지정, 필터는 지정 된 순서로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-528">As in earlier versions, if the *Order* property is explicitly specified, the filters are run in the specified order.</span></span>
- <span data-ttu-id="4ad3e-529">라는 새 속성이 추가 *FileExtensions* 에 *VirtualPathProviderViewEngine* 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-529">Added a new property named *FileExtensions* to the *VirtualPathProviderViewEngine* base class.</span></span> <span data-ttu-id="4ad3e-530">조회할 때 뷰 경로 의해 (및 이름으로)에 포함 된 파일 확장명을 가진 뷰만이 새 속성으로 지정 된 목록으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-530">When looking up a view by path (and not by name), only views with a file extension contained in the list specified by this new property is considered.</span></span> <span data-ttu-id="4ad3e-531">사용자에 게 웹 폼 보기에 대 한 사용자 지정 파일 확장명을 사용 하도록 설정 하려면 사용자 지정 빌드 공급자를 등록 하 고 이름을 아닌 전체 경로 사용 하 여 해당 뷰를 참조 하는 주요 변경 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-531">This is a breaking change for those who register a custom build provider to enable a custom file extension for web form views and are referencing those views by using a full path rather than a name.</span></span> <span data-ttu-id="4ad3e-532">해결 하는 값을 수정 하는 *FileExtensions* 속성을 사용자 지정 파일 확장명을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-532">The workaround is to modify the value of the *FileExtensions* property to include the custom file extension.</span></span>

<a id="_Toc276711795"></a>
## <a name="known-issues"></a><span data-ttu-id="4ad3e-533">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="4ad3e-533">Known Issues</span></span>

- <span data-ttu-id="4ad3e-534">설치 관리자는 이전 버전의 Visual Studio 2010의 구성 요소를 업데이트 하기 때문에 완료 하려면 ASP.NET MVC 보다 훨씬 더 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-534">The installer may take much longer than previous versions of ASP.NET MVC to complete because it updates components of Visual Studio 2010.</span></span>
- <span data-ttu-id="4ad3e-535">뷰 추가 폴딩을 astrongly를 선택 하는 경우 스 캐 폴드 쓰기 전용 속성 보기를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-535">The Add View scaffolding when selecting astrongly typed view scaffolds write-only properties.</span></span> <span data-ttu-id="4ad3e-536">이러한 항상에서 무시할 스 캐 폴딩 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-536">These should always be ignored by scaffolding.</span></span> <span data-ttu-id="4ad3e-537">뷰 추가 대화 상자도 스 캐 폴드 읽기 전용 속성 "Edit" 또는 "만들기" 보기를 생성 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-537">The Add View dialog also scaffolds read-only properties when generating an "Edit" or "Create" view.</span></span> <span data-ttu-id="4ad3e-538">읽기 전용 속성 표시 및 목록 보기에 대 한 스 캐 폴드 수만 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-538">Read-only properties should only be scaffolded for the Display and List views.</span></span>
- <span data-ttu-id="4ad3e-539">디버깅 ASP.NET MVC 3 비동기 CTP와 함께 설치 된 경우 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-539">Debugging doesn't work when ASP.NET MVC 3 is installed alongside the Async CTP.</span></span> <span data-ttu-id="4ad3e-540">ASP.NET MVC 3 비동기 CTP와 함께 설치할된 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-540">ASP.NET MVC 3 cannot be installed side-by-side with the Async CTP.</span></span> <span data-ttu-id="4ad3e-541">디버깅을 복구 하려면 비동기 CTP를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-541">Uninstall the Async CTP to repair debugging.</span></span> <span data-ttu-id="4ad3e-542">자세한 내용은 읽기 [이 블로그 게시물](http://drew-prog.blogspot.com/2010/11/how-to-uninstall-microsoft-aspnet-mvc-3.html) ASP.NET MVC 3 RC의 모든 조각을 제거에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-542">For more details, read [this blog post](http://drew-prog.blogspot.com/2010/11/how-to-uninstall-microsoft-aspnet-mvc-3.html) about uninstalling all the pieces of ASP.NET MVC 3 RC.</span></span>
- <span data-ttu-id="4ad3e-543">Resharper가 설치 된 경우에 razor Intellisense 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-543">Razor Intellisense does not work when Resharper is installed.</span></span> <span data-ttu-id="4ad3e-544">ReSharper가 설치 되어 읽으십시오 ASP.NET MVC 3 RC의 Razor intellisense 지원을 활용 하려고 하는 경우 [이 블로그 게시물](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) 에서 JetBrains를 함께 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-544">If you have ReSharper installed and want to take advantage of the Razor intellisense support in ASP.NET MVC 3 RC, please read [this blog post](http://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) from JetBrains which discusses ways to use them together today.</span></span>
- <span data-ttu-id="4ad3e-545">ASP.NET MVC 3 베타를 사용 하 여 만든 CSHTML 및 VBHTML 뷰 없는 빌드 작업이 제대로 게시에서이 생략 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-545">CSHTML and VBHTML views created with Beta of ASP.NET MVC 3 do not have their build action correctly which omits them from publishing.</span></span> <span data-ttu-id="4ad3e-546">*빌드 작업* 에 이러한 파일을 "콘텐츠"로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-546">The *Build Action* for these files should be set to "Content".</span></span> <span data-ttu-id="4ad3e-547">ASP.NET MVC 3 RC의 새로운 파일을이 문제를 해결할 수 있지만 베타 버전을 사용 하 여 만든 프로젝트에 대 한 기존 파일에 대 한 설정을 수정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-547">ASP.NET MVC 3 RC fixes this issue for new files, but doesn't correct the setting for existing files for a project created with the Beta.</span></span>
- <span data-ttu-id="4ad3e-548">설치 관리자는 이전 버전의 Visual Studio 2010의 구성 요소를 업데이트 하기 때문에 완료 하려면 ASP.NET MVC 보다 훨씬 더 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-548">The installer may take much longer than previous versions of ASP.NET MVC to complete because it updates components of Visual Studio 2010.</span></span>
- <span data-ttu-id="4ad3e-549">뷰 추가 폴딩을 보기 스 캐 폴드 입력 강력한 "Edit"를 선택 했을 때 읽기 전용 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-549">The Add View scaffolding when selecting an "Edit" strongly typed view scaffolds read only properties.</span></span> <span data-ttu-id="4ad3e-550">마찬가지로, 쓰기 전용 속성은 "" 보기에 대 한 스 캐 폴드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-550">Likewise, write-only properties are scaffolded for "Display" views.</span></span>
- <span data-ttu-id="4ad3e-551">설치 하는 동안 EULA 동의 대화 상자 예정 보다 작은 창에서 사용 약관을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-551">During installation, the EULA acceptance dialog box displays the license terms in a window that is smaller than intended.</span></span>
- <span data-ttu-id="4ad3e-552">ASP.NET MVC 3 도구 설치의 일부분으로 포함 된 Razor 릴리스로 충돌이 발생 Visual Studio 비동기 CTP를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-552">Installing the Visual Studio Async CTP causes a conflict with the Razor release that is included as part of the ASP.NET MVC 3 tooling installation.</span></span> <span data-ttu-id="4ad3e-553">Visual Studio 비동기 CTP와 Razor 릴리스를 모두 동일한 컴퓨터에 설치 하려고 하지 마십시오 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-553">Make sure that you do not try to install both the Visual Studio Async CTP and the Razor release on the same machine.</span></span>
- <span data-ttu-id="4ad3e-554">Razor 뷰 (.cshtml 파일)를 편집 하는 경우 Visual Studio에서 컨트롤러 이동 메뉴 항목을 사용할 수 없으며 되며 코드 조각이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-554">When you are editing a Razor view (.cshtml file), the Go To Controller menu item in Visual Studio will not be available, and there are no code snippets.</span></span>

<a id="TOC_ASP_NET_3_Beta"></a>
## <a name="aspnet-mvc-3-beta"></a><span data-ttu-id="4ad3e-555">ASP.NET MVC 3 베타</span><span class="sxs-lookup"><span data-stu-id="4ad3e-555">ASP.NET MVC 3 Beta</span></span>

<span data-ttu-id="4ad3e-556">ASP.NET MVC 3 베타는 2010 년 10 월 6 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-556">ASP.NET MVC 3 Beta was released on October 6, 2010.</span></span> <span data-ttu-id="4ad3e-557">다음 내용은 베타 릴리스 버전 관련 되어 있으며 업데이트 또는 위의 ASP.NET MVC 3 릴리스 후보 섹션에서 참조 하는 변경 사항이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-557">The following notes are specific to the Beta release, and are subject to any updates or changes referenced in the ASP.NET MVC 3 Release Candidate section above.</span></span>

## <a id="0.1__Toc274034215"></a>  <span data-ttu-id="4ad3e-558">새 Featuresin ASP.NET MVC 3 베타</span><span class="sxs-lookup"><span data-stu-id="4ad3e-558">New Featuresin ASP.NET MVC 3 Beta</span></span>

<a id="0.1__Default_validation_system"></a><span data-ttu-id="4ad3e-559">이 섹션에 도입 된 기능에 설명 ASP.NET MVC 3 베타 릴리스 버전에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-559">This section describes features that have been introduced in the ASP.NET MVC 3 Beta release.</span></span>

### <a id="0.1__Toc274034216"></a>  <span data-ttu-id="4ad3e-560">NuGet 패키지 관리자</span><span class="sxs-lookup"><span data-stu-id="4ad3e-560">NuGet Package Manager</span></span>

<span data-ttu-id="4ad3e-561">ASP.NET MVC 3 추가 라이브러리는 통합된 패키지 관리 도구 및 Visual Studio 프로젝트에는 도구는 NuGet 패키지 관리자를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-561">ASP.NET MVC 3 includes NuGet Package Manager, which is an integrated package management tool for adding libraries and tools to Visual Studio projects.</span></span> <span data-ttu-id="4ad3e-562">대부분의 경우 개발자가 해당 원본 트리로 라이브러리를 지금 수행 하는 단계를 자동화 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-562">For the most part, it automates the steps that developers take today to get a library into their source tree.</span></span>

<span data-ttu-id="4ad3e-563">NuGet 명령줄 도구, Visual Studio 상황에 맞는 메뉴에서 Visual Studio 2010 내는 통합된 콘솔 창 및 PowerShell cmdlet 집합을 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-563">You can work with NuGet as a command line tool, as an integrated console window inside Visual Studio 2010, from the Visual Studio context menu, and as set of PowerShell cmdlets.</span></span>

<span data-ttu-id="4ad3e-564">NuGet에 대 한 자세한 내용은 참조는 [NuGet 설명서](https://docs.microsoft.com/nuget/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-564">For more information about NuGet, read the [NuGet Documentation](https://docs.microsoft.com/nuget/).</span></span>

### <a id="0.1__Toc274034217"></a>  <span data-ttu-id="4ad3e-565">향상 된 새 프로젝트 대화 상자</span><span class="sxs-lookup"><span data-stu-id="4ad3e-565">Improved New Project Dialog Box</span></span>

<span data-ttu-id="4ad3e-566">새 프로젝트를 만들 때 새 프로젝트 대화 상자 이제 수 있습니다는 뷰 엔진이 뿐만 아니라 ASP.NET MVC 프로젝트 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-566">When you create a new project, the New Project dialog box now lets you specify the view engine as well as an ASP.NET MVC project type.</span></span>

![](mvc3-release-notes/_static/image6.png)

<span data-ttu-id="4ad3e-567">이 릴리스에서 템플릿과 보기 대화 상자에 나열 된 엔진의 목록을 수정에 대 한 지원이 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-567">Support for modifying the list of templates and view engines listed in the dialog box is not included in this release.</span></span>

<span data-ttu-id="4ad3e-568">기본 템플릿에 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-568">The default templates are the following:</span></span>

<span data-ttu-id="4ad3e-569">빈 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-569">Empty.</span></span> <span data-ttu-id="4ad3e-570">ASP.NET MVC 스타일, 기본 및 기본 JavaScript 파일을 포함 하는 스크립트 디렉터리를 포함 하는 작은 Site.css 파일 ASP.NET MVC 프로젝트에 대 한 기본 디렉터리 구조를 포함 하 여 ASP.NET MVC 프로젝트에 대 한 파일의 최소 집합을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-570">Contains a minimal set of files for an ASP.NET MVC project, including the default directory structure for ASP.NET MVC projects, a small Site.css file that contains the default ASP.NET MVC styles, and a Scripts directory that contains the default JavaScript files.</span></span>

<span data-ttu-id="4ad3e-571">인터넷 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-571">Internet Application.</span></span> <span data-ttu-id="4ad3e-572">ASP.NET MVC 내에서 멤버 자격 공급자를 사용 하는 방법을 보여 주는 샘플 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-572">Contains sample functionality that demonstrates how to use the membership provider within ASP.NET MVC.</span></span>

### <a id="0.1__Toc274034218"></a>  <span data-ttu-id="4ad3e-573">강력 하 게 지정 하는 간단한 방법은 입력 Razor 뷰 모델</span><span class="sxs-lookup"><span data-stu-id="4ad3e-573">Simplified Way to Specify Strongly Typed Models in Razor Views</span></span>

<span data-ttu-id="4ad3e-574">강력한 형식의 Razor 뷰의 모델 유형을 지정 하는 방법은 new를 사용 하 여 간단해졌습니다 @model CSHTML 뷰에 대 한 지시문 및 @ModelType VBHTML 뷰에 대 한 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-574">The way to specify the model type for strongly typed Razor views has been simplified by using the new @model directive for CSHTML views and @ModelType directive for VBHTML views.</span></span> <span data-ttu-id="4ad3e-575">이전 버전의 ASP.NET MVC에서는 Razor에 대 한 강력한 형식의 모델에는 이러한 방식으로 뷰를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-575">In earlier versions of ASP.NET MVC, you would specify a strongly typed model for Razor views this way:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample25.cshtml)]

<span data-ttu-id="4ad3e-576">이 릴리스에서 다음 구문을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-576">In this release, you can use the following syntax:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample26.cshtml)]

### <a id="0.1__Toc274034219"></a>  <span data-ttu-id="4ad3e-577">새 ASP.NET 웹 페이지에 대 한 도우미 메서드를 지원</span><span class="sxs-lookup"><span data-stu-id="4ad3e-577">Support for New ASP.NET Web Pages Helper Methods</span></span>

<span data-ttu-id="4ad3e-578">새 ASP.NET 웹 페이지 기술을 뷰 및 컨트롤러에 일반적으로 사용 되는 기능을 추가 하는 데 도움이 되는 도우미 메서드 집합이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-578">The new ASP.NET Web Pages technology includes a set of helper methods that are useful for adding commonly used functionality to views and controllers.</span></span> <span data-ttu-id="4ad3e-579">ASP.NET MVC 3에서는 이러한 도우미 메서드를 컨트롤러와 뷰 내에서 사용할 수 (필요한 경우).</span><span class="sxs-lookup"><span data-stu-id="4ad3e-579">ASP.NET MVC 3 supports using these helper methods within controllers and views (where appropriate).</span></span> <span data-ttu-id="4ad3e-580">이러한 메서드는 System.Web.Helpers 어셈블리에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-580">These methods are contained in the System.Web.Helpers assembly.</span></span> <span data-ttu-id="4ad3e-581">다음 표에서 몇 가지 ASP.NET 웹 페이지 도우미 메서드를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-581">The following table lists a few of the ASP.NET Web Pages helper methods.</span></span>

| <span data-ttu-id="4ad3e-582">**도우미**</span><span class="sxs-lookup"><span data-stu-id="4ad3e-582">**Helper**</span></span> | <span data-ttu-id="4ad3e-583">**설명**</span><span class="sxs-lookup"><span data-stu-id="4ad3e-583">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="4ad3e-584">차트</span><span class="sxs-lookup"><span data-stu-id="4ad3e-584">Chart</span></span> | <span data-ttu-id="4ad3e-585">보기 내에서 차트를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-585">Renders a chart within a view.</span></span> <span data-ttu-id="4ad3e-586">Chart.ToWebImage, Chart.Save, Chart.Write 등 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-586">Contains methods such as Chart.ToWebImage, Chart.Save, and Chart.Write.</span></span> |
| <span data-ttu-id="4ad3e-587">암호화</span><span class="sxs-lookup"><span data-stu-id="4ad3e-587">Crypto</span></span> | <span data-ttu-id="4ad3e-588">해시를 올바르게 만들려면 알고리즘을 사용 하 여 솔트된 및 해시 된 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-588">Uses hashing algorithms to create properly salted and hashed passwords.</span></span> |
| <span data-ttu-id="4ad3e-589">WebGrid</span><span class="sxs-lookup"><span data-stu-id="4ad3e-589">WebGrid</span></span> | <span data-ttu-id="4ad3e-590">그리드로 개체 (일반적으로 데이터베이스의 데이터)의 컬렉션을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-590">Renders a collection of objects (typically, data from a database) as a grid.</span></span> <span data-ttu-id="4ad3e-591">페이징 및 정렬을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-591">Supports paging and sorting.</span></span> |
| <span data-ttu-id="4ad3e-592">WebImage</span><span class="sxs-lookup"><span data-stu-id="4ad3e-592">WebImage</span></span> | <span data-ttu-id="4ad3e-593">이미지를 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-593">Renders an image.</span></span> |
| <span data-ttu-id="4ad3e-594">WebMail</span><span class="sxs-lookup"><span data-stu-id="4ad3e-594">WebMail</span></span> | <span data-ttu-id="4ad3e-595">이메일 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-595">Sends an email message.</span></span> |

<span data-ttu-id="4ad3e-596">도우미와 기본 구문을 나열 하는 빠른 참조 항목을 사용할 수는 다음 URL에서 ASP.NET Razor 구문 문서의 일부로:</span><span class="sxs-lookup"><span data-stu-id="4ad3e-596">A quick reference topic that lists the helpers and basic syntax is available as part of the ASP.NET Razor syntax documentation at the following URL:</span></span>

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-api-reference](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)

### <a id="0.1__Toc274034220"></a>  <span data-ttu-id="4ad3e-597">추가 종속성 주입 지원</span><span class="sxs-lookup"><span data-stu-id="4ad3e-597">Additional Dependency Injection Support</span></span>

<span data-ttu-id="4ad3e-598">현재 버전을 ASP.NET MVC 3 Preview 1 릴리스를 기반으로 구축 두 개의 새로운 서비스 및 4 개의 기존 서비스에 대 한 지원 추가 및 종속성 확인 및 공통 서비스 로케이터에 대 한 향상 된 지원 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-598">Building on the ASP.NET MVC 3 Preview 1 release, the current release includes added support for two new services and four existing services, and improved support for dependency resolution and the Common Service Locator.</span></span>

#### <a name="new-icontrolleractivator-interface-for-fine-grained-controller-instantiation"></a><span data-ttu-id="4ad3e-599">세분화 된 컨트롤러 인스턴스화에 대 한 새로운 IControllerActivator 인터페이스</span><span class="sxs-lookup"><span data-stu-id="4ad3e-599">New IControllerActivator Interface for Fine-Grained Controller Instantiation</span></span>

<span data-ttu-id="4ad3e-600">새 IControllerActivator 인터페이스는 종속성 주입을 통해 컨트롤러를 인스턴스화하기 하는 방법을 보다 세부적으로 제어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-600">The new IControllerActivator interface provides more fine-grained control over how controllers are instantiated via dependency injection.</span></span> <span data-ttu-id="4ad3e-601">다음 예제에서는 인터페이스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-601">The following example shows the interface:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample27.cs)]

<span data-ttu-id="4ad3e-602">이와 반대로 컨트롤러 팩터리 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-602">Contrast this to the role of the controller factory.</span></span> <span data-ttu-id="4ad3e-603">컨트롤러 팩터리는 해당 컨트롤러 형식의 인스턴스를 인스턴스화하고를 고 컨트롤러 종류를 찾기 위한 IControllerFactory 인터페이스의 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-603">A controller factory is an implementation of the IControllerFactory interface, which is responsible both for locating a controller type and for instantiating an instance of that controller type.</span></span>

<span data-ttu-id="4ad3e-604">컨트롤러 활성기는 컨트롤러 형식의 인스턴스를 인스턴스화하고 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-604">Controller activators are responsible only for instantiating an instance of a controller type.</span></span> <span data-ttu-id="4ad3e-605">컨트롤러 유형 조회를 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-605">They do not perform the controller type lookup.</span></span> <span data-ttu-id="4ad3e-606">찾은 후에 적절 한 컨트롤러 종류, 컨트롤러 팩터리 IControllerActivator 인스턴스에 컨트롤러의 실제 인스턴스에 처리를 위임 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-606">After locating a proper controller type, controller factories should delegate to an instance of IControllerActivator to handle the actual instantiation of the controller.</span></span>

<span data-ttu-id="4ad3e-607">DefaultControllerFactory 클래스 IControllerFactory 인스턴스를 허용 하는 새 생성자를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-607">The DefaultControllerFactory class has a new constructor that accepts an IControllerFactory instance.</span></span> <span data-ttu-id="4ad3e-608">이 기본 컨트롤러 형식 조회 동작을 재정의 하지 않고 컨트롤러 만들기의 이러한 측면을 관리 하는 종속성 주입을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-608">This lets you apply Dependency Injection to manage this aspect of controller creation without having to override the default controller-type lookup behavior.</span></span>

#### <a name="iservicelocator-interface-replaced-with-idependencyresolver"></a><span data-ttu-id="4ad3e-609">IServiceLocator 인터페이스 되며 IDependencyResolver로 대체</span><span class="sxs-lookup"><span data-stu-id="4ad3e-609">IServiceLocator Interface Replaced with IDependencyResolver</span></span>

<span data-ttu-id="4ad3e-610">커뮤니티 피드백에 따라 ASP.NET MVC 3 베타 릴리스 버전은 대체 IServiceLocator 인터페이스를 사용 하는 ASP.NET MVC의 요구에 맞게 맞춤화 되며 IDependencyResolver 인터페이스 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-610">Based on community feedback, the ASP.NET MVC 3 Beta release has replaced the use of the IServiceLocator interface with a slimmed-down IDependencyResolver interface specific to the needs of ASP.NET MVC.</span></span> <span data-ttu-id="4ad3e-611">다음 예제에서는 새 인터페이스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-611">The following example shows the new interface:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample28.cs)]

<span data-ttu-id="4ad3e-612">또한이 변경의 일부로 ServiceLocator 클래스 DependencyResolver 클래스 대체 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-612">As part of this change, the ServiceLocator class was also replaced with the DependencyResolver class.</span></span> <span data-ttu-id="4ad3e-613">종속성 확인자를 등록 하는 것은 이전 버전의 ASP.NET MVC 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-613">Registration of a dependency resolver is similar to earlier versions of ASP.NET MVC:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample29.cs)]

<span data-ttu-id="4ad3e-614">이 인터페이스의 구현 하기만 하면 요청된 된 형식에 대 한 등록 된 서비스 제공 하기 위해 기본 종속성 주입 컨테이너를 위임 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-614">Implementations of this interface should simply delegate to the underlying dependency injection container to provide the registered service for the requested type.</span></span>

<span data-ttu-id="4ad3e-615">요청 된 형식의 등록 된 서비스 때 ASP.NET MVC에서는 GetService에서 null을 반환 하 고 GetServices에서 빈 컬렉션을 반환 하려면이 인터페이스의 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-615">When there are no registered services of the requested type, ASP.NET MVC expects implementations of this interface to return null from GetService and to return an empty collection from GetServices.</span></span>

<span data-ttu-id="4ad3e-616">새 DependencyResolver 클래스를 사용 하면 새 되며 IDependencyResolver 인터페이스 또는 공통 서비스 로케이터 인터페이스 (IServiceLocator)를 구현 하는 클래스를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-616">The new DependencyResolver class lets you register classes that implement either the new IDependencyResolver interface or the Common Service Locator interface (IServiceLocator).</span></span> <span data-ttu-id="4ad3e-617">공통 서비스 로케이터에 대 한 자세한 내용은 참조 [GitHub에서 CommonServiceLocator](https://github.com/unitycontainer/commonservicelocator)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-617">For more information about Common Service Locator, see [CommonServiceLocator on GitHub](https://github.com/unitycontainer/commonservicelocator).</span></span>

<a id="0.1__Breaking_Changes"></a>

#### <a name="new-iviewactivator-interface-for-fine-grained-view-page-instantiation"></a><span data-ttu-id="4ad3e-618">세분화 된 뷰 페이지 인스턴스화에 대 한 새로운 IViewActivator 인터페이스</span><span class="sxs-lookup"><span data-stu-id="4ad3e-618">New IViewActivator Interface for Fine-Grained View Page Instantiation</span></span>

<span data-ttu-id="4ad3e-619">새 IViewPageActivator 인터페이스는 종속성 주입을 통해 페이지 보기를 인스턴스화하기 하는 방법을 보다 세부적으로 제어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-619">The new IViewPageActivator interface provides more fine-grained control over how view pages are instantiated via dependency injection.</span></span> <span data-ttu-id="4ad3e-620">이 WebFormView 인스턴스와 RazorView 인스턴스 모두에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-620">This applies to both WebFormView instances and RazorView instances.</span></span> <span data-ttu-id="4ad3e-621">다음 예제에서는 새 인터페이스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-621">The following example shows the new interface:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample30.cs)]

<span data-ttu-id="4ad3e-622">이러한 클래스는 이제 ViewPage, ViewUserControl, 및 WebViewPage 형식이 인스턴스화되고 방법을 제어 하려면 종속성 주입을 사용할 수 있는 IViewPageActivator 생성자 인수를 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-622">These classes now accept an IViewPageActivator constructor argument, which lets you use dependency injection to control how the ViewPage, ViewUserControl, and WebViewPage types are instantiated.</span></span>

#### <a name="new-dependency-resolver-support-for-existing-services"></a><span data-ttu-id="4ad3e-623">기존 서비스에 대 한 새 종속성 확인자 지원</span><span class="sxs-lookup"><span data-stu-id="4ad3e-623">New Dependency Resolver Support for Existing Services</span></span>

<span data-ttu-id="4ad3e-624">새 릴리스는 다음과 같은 서비스에 대 한 종속성 확인 지원을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-624">The new release includes dependency resolution support for the following services:</span></span>

- <span data-ttu-id="4ad3e-625">모델 유효성 검사 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-625">Model validation providers.</span></span> <span data-ttu-id="4ad3e-626">ModelValidatorProvider를 구현 하는 클래스를 종속성 확인자에 등록할 수 있으며 시스템 클라이언트 및 서버 쪽 유효성 검사를 지 원하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-626">Classes that implement ModelValidatorProvider can be registered in the dependency resolver, and the system will use them to support client- and server-side validation.</span></span>
- <span data-ttu-id="4ad3e-627">모델 메타 데이터 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-627">Model metadata provider.</span></span> <span data-ttu-id="4ad3e-628">ModelMetadataProvider를 구현 하는 단일 클래스를 종속성 확인자에 등록할 수 있으며 시스템에서이 파일 템플릿 및 유효성 검사 시스템에 대 한 메타 데이터를 제공 하 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-628">A single class that implements ModelMetadataProvider can be registered in the dependency resolver, and the system will use it to provide metadata for the templating and validation systems.</span></span>
- <span data-ttu-id="4ad3e-629">값 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-629">Value providers.</span></span> <span data-ttu-id="4ad3e-630">ValueProviderFactory를 구현 하는 클래스를 종속성 확인자에 등록할 수 있으며 시스템 컨트롤러에 의해 및 모델 바인딩 중에 사용 되는 값 공급자를 만드는 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-630">Classes that implement ValueProviderFactory can be registered in the dependency resolver, and the system will use them to create value providers that are consumed by the controller and during model binding.</span></span>
- <span data-ttu-id="4ad3e-631">모델 바인더입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-631">Model binders.</span></span> <span data-ttu-id="4ad3e-632">IModelBinderProvider를 구현 하는 클래스를 종속성 확인자에 등록할 수 있으며 시스템 모델 바인딩 시스템에서 사용 하는 모델 바인더를 만드는 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-632">Classes that implement IModelBinderProvider can be registered in the dependency resolver, and the system will use them to create model binders that are consumed by the model binding system.</span></span>

### <a id="0.1__Toc274034221"></a>  <span data-ttu-id="4ad3e-633">비 가시적인 jQuery 기반 Ajax에 대 한 새로운 지원</span><span class="sxs-lookup"><span data-stu-id="4ad3e-633">New Support for Unobtrusive jQuery-Based Ajax</span></span>

<span data-ttu-id="4ad3e-634">ASP.NET MVC Ajax 도우미 메서드를 다음과 같은 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-634">ASP.NET MVC includes Ajax helper methods such as the following:</span></span>

- <span data-ttu-id="4ad3e-635">Ajax.ActionLink</span><span class="sxs-lookup"><span data-stu-id="4ad3e-635">Ajax.ActionLink</span></span>
- <span data-ttu-id="4ad3e-636">Ajax.RouteLink</span><span class="sxs-lookup"><span data-stu-id="4ad3e-636">Ajax.RouteLink</span></span>
- <span data-ttu-id="4ad3e-637">Ajax.BeginForm</span><span class="sxs-lookup"><span data-stu-id="4ad3e-637">Ajax.BeginForm</span></span>
- <span data-ttu-id="4ad3e-638">Ajax.BeginRouteForm</span><span class="sxs-lookup"><span data-stu-id="4ad3e-638">Ajax.BeginRouteForm</span></span>

<span data-ttu-id="4ad3e-639">이러한 메서드는 JavaScript를 사용 하 여 전체 포스트백을 사용 하는 대신 서버에서 작업 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-639">These methods use JavaScript to invoke an action method on the server rather than using a full postback.</span></span> <span data-ttu-id="4ad3e-640">이 기능은 방식으로 비 가시적인 jQuery을 활용 하려면 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-640">This functionality has been updated to take advantage of jQuery in an unobtrusive manner.</span></span> <span data-ttu-id="4ad3e-641">영향을 주지 않고 내보내기 인라인 클라이언트 스크립트 하는 대신 이러한 도우미 메서드 동작에서에서 분리 태그를 사용 하 여 HTML5 특성을 생성 함으로써는 *데이터 ajax* 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-641">Rather than intrusively emitting inline client scripts, these helper methods separate the behavior from the markup by emitting HTML5 attributes using the *data-ajax* prefix.</span></span> <span data-ttu-id="4ad3e-642">동작에서는 적절 한 JavaScript 파일을 참조 하 여 태그에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-642">Behavior is then applied to the markup by referencing the appropriate JavaScript files.</span></span> <span data-ttu-id="4ad3e-643">다음 JavaScript 파일이 참조 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-643">Make sure that the following JavaScript files are referenced:</span></span>

- <span data-ttu-id="4ad3e-644">jquery-1.4.1.js</span><span class="sxs-lookup"><span data-stu-id="4ad3e-644">jquery-1.4.1.js</span></span>
- <span data-ttu-id="4ad3e-645">jquery.unobtrusive.ajax.js</span><span class="sxs-lookup"><span data-stu-id="4ad3e-645">jquery.unobtrusive.ajax.js</span></span>

<span data-ttu-id="4ad3e-646">이 기능은 ASP.NET MVC 3 새 프로젝트 템플릿이에서 Web.config 파일에서 기본적으로 설정 되어 있지만 기존 프로젝트에 기본적으로 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-646">This feature is enabled by default in the Web.config file in the ASP.NET MVC 3 new project templates, but is disabled by default for existing projects.</span></span> <span data-ttu-id="4ad3e-647">자세한 내용은 참조 [클라이언트 유효성 검사 및 비간섭 JavaScript에 대 한 응용 프로그램 수준 플래그를 추가](#0.1_AddedApplicationWideFlagsForClientValida) 이 문서의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-647">For more information, see [Added application-wide flags for client validation and unobtrusive JavaScript](#0.1_AddedApplicationWideFlagsForClientValida) later in this document.</span></span>

### <a id="0.1__Toc274034222"></a>  <span data-ttu-id="4ad3e-648">비 가시적인 jQuery 유효성 검사에 대 한 새로운 지원</span><span class="sxs-lookup"><span data-stu-id="4ad3e-648">New Support for Unobtrusive jQuery Validation</span></span>

<span data-ttu-id="4ad3e-649">기본적으로 ASP.NET MVC 3 베타 방식으로 비 가시적인 jQuery 유효성 검사 클라이언트 쪽 유효성 검사를 수행 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-649">By default, ASP.NET MVC 3 Beta uses jQuery validation in an unobtrusive manner in order to perform client-side validation.</span></span> <span data-ttu-id="4ad3e-650">비 가시적인 클라이언트 유효성 검사를 사용 하려면 보기 내에서 다음와 같은 호출을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-650">To enable unobtrusive client validation, make a call like the following from within a view:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample31.cs)]

<span data-ttu-id="4ad3e-651">그러려면 ViewContext.UnobtrusiveJavaScriptEnabled 속성이 다음 호출 하 여 수행할 수 있는 true로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-651">This requires that ViewContext.UnobtrusiveJavaScriptEnabled property is set to true, which you can do by making the following call:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample32.cs)]

<span data-ttu-id="4ad3e-652">또한 다음 JavaScript 파일이 참조를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-652">Also make sure the following JavaScript files are referenced.</span></span>

- <span data-ttu-id="4ad3e-653">jquery-1.4.1.js</span><span class="sxs-lookup"><span data-stu-id="4ad3e-653">jquery-1.4.1.js</span></span>
- <span data-ttu-id="4ad3e-654">jquery.validate.js</span><span class="sxs-lookup"><span data-stu-id="4ad3e-654">jquery.validate.js</span></span>
- <span data-ttu-id="4ad3e-655">jquery.validate.unobtrusive.js</span><span class="sxs-lookup"><span data-stu-id="4ad3e-655">jquery.validate.unobtrusive.js</span></span>

<span data-ttu-id="4ad3e-656">이 기능은 ASP.NET MVC 3 새 프로젝트 템플릿이에서 Web.config 파일에서 기본적으로에서 사용 되지만 기존 프로젝트에 기본적으로 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-656">This feature is enabled on by default in the Web.config file in the ASP.NET MVC 3 new project templates, but is disabled by default for existing projects.</span></span> <span data-ttu-id="4ad3e-657">자세한 내용은 참조 [클라이언트 유효성 검사 및 비간섭 JavaScript에 대 한 새 응용 프로그램 수준 플래그](#0.1_AddedApplicationWideFlagsForClientValida) 이 문서의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-657">For more information, see [New application-wide flags for client validation and unobtrusive JavaScript](#0.1_AddedApplicationWideFlagsForClientValida) later in this document.</span></span>

<a id="0.1__Toc274034223"></a>

### <a id="0.1_AddedApplicationWideFlagsForClientValida"></a>  <span data-ttu-id="4ad3e-658">클라이언트 유효성 검사 및 비간섭 JavaScript에 대 한 새 응용 프로그램 수준 플래그</span><span class="sxs-lookup"><span data-stu-id="4ad3e-658">New Application-Wide Flags for Client Validation and Unobtrusive JavaScript</span></span>

<span data-ttu-id="4ad3e-659">클라이언트 유효성 검사 및 전체적으로 다음 예제와 같이 HtmlHelper 클래스의 정적 멤버를 사용 하 여 비간섭 JavaScript를 사용 하지 않도록 설정 하거나 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-659">You can enable or disable client validation and unobtrusive JavaScript globally using static members of the HtmlHelper class, as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample33.cs)]

<span data-ttu-id="4ad3e-660">기본적으로 비간섭 JavaScript를 사용 하는 기본 프로젝트 템플릿.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-660">The default project templates enable unobtrusive JavaScript by default.</span></span> <span data-ttu-id="4ad3e-661">또한 다음 설정을 사용 하 여 응용 프로그램의 루트 Web.config 파일에서 이러한 기능을 사용 하지 않도록 설정 하거나 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-661">You can also enable or disable these features in the root Web.config file of your application using the following settings:</span></span>

[!code-xml[Main](mvc3-release-notes/samples/sample34.xml)]

<span data-ttu-id="4ad3e-662">기본적으로 이러한 기능을 활성화할 수 있습니다, 때문에 새 오버 로드는 다음 예제에 나와 있는 것 처럼 기본 설정을 재정의할 수 있도록 하는 HtmlHelper 클래스에 도입 된:</span><span class="sxs-lookup"><span data-stu-id="4ad3e-662">Because you can enable these features by default, new overloads were introduced to the HtmlHelper class that let you override the default settings, as shown in the following examples:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample35.cs)]

<span data-ttu-id="4ad3e-663">이전 버전과 호환성을 위해 이러한 기능은 모두 기본적으로 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-663">For backward compatibility, both of these features are disabled by default.</span></span>

### <a id="0.1__Toc274034224"></a>  <span data-ttu-id="4ad3e-664">뷰를 실행 하기 전에 실행 되는 코드에 대 한 새로운 지원</span><span class="sxs-lookup"><span data-stu-id="4ad3e-664">New Support for Code that Runs Before Views Run</span></span>

<span data-ttu-id="4ad3e-665">이제 라는 파일을 넣을 수 있습니다 \_viewstart.cshtml (또는 \_viewstart.vbhtml) Views 디렉터리의 코드를 해당 디렉터리와 하위 디렉터리에 있는 여러 뷰 간에 공유 되는 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-665">You can now put a file named \_viewstart.cshtml (or \_viewstart.vbhtml) in the Views directory and add code to it that will be shared among multiple views in that directory and its subdirectories.</span></span> <span data-ttu-id="4ad3e-666">예를 들어에 다음 코드를 넣을 수 있습니다는 \_viewstart.cshtml 페이지 ~/Views 폴더에서:</span><span class="sxs-lookup"><span data-stu-id="4ad3e-666">For example, you might put the following code into the \_viewstart.cshtml page in the ~/Views folder:</span></span>

[!code-cshtml[Main](mvc3-release-notes/samples/sample36.cshtml)]

<span data-ttu-id="4ad3e-667">Views 폴더 내의 모든 보기 및 모든 해당 하위 폴더를 재귀적으로 대 한 레이아웃 페이지를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-667">This sets the layout page for every view within the Views folder and all its subfolders recursively.</span></span> <span data-ttu-id="4ad3e-668">경우 뷰 렌더링 되는 코드에는 \_코드 보기를 실행 하기 전에 viewstart.cshtml 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-668">When a view is being rendered, the code in the \_viewstart.cshtml file runs before the view code runs.</span></span> <span data-ttu-id="4ad3e-669">\_viewstart.cshtml 코드에 해당 폴더의 모든 뷰에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-669">The \_viewstart.cshtml code applies to every view in that folder.</span></span>

<span data-ttu-id="4ad3e-670">기본적으로의 코드는 \_viewstart.cshtml 파일 하위 폴더에 보기에도 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-670">By default, the code in the \_viewstart.cshtml file also applies to views in any subfolder.</span></span> <span data-ttu-id="4ad3e-671">그러나 개별 하위 폴더의 고유 버전을 포함할 수는 \_viewstart.cshtml 파일의 경우 로컬 버전이 우선 한다는 점에서;.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-671">However, individual subfolders can have their own version of the \_viewstart.cshtml file; in that case, the local version takes precedence.</span></span> <span data-ttu-id="4ad3e-672">예를 들어 HomeController에 대 한 모든 뷰에 공통 되는 코드를 실행 하려면 배치는 \_viewstart.cshtml 파일 ~/Views/Home 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-672">For example, to run code that is common to all views for the HomeController, put a \_viewstart.cshtml file in the ~/Views/Home folder.</span></span>

### <a id="0.1__Toc274034225"></a>  <span data-ttu-id="4ad3e-673">VBHTML Razor 구문에 대 한 새로운 지원</span><span class="sxs-lookup"><span data-stu-id="4ad3e-673">New Support for the VBHTML Razor Syntax</span></span>

<span data-ttu-id="4ad3e-674">이전 ASP.NET MVC 미리 보기에는 Razor 구문을 기반으로 C#을 사용 하 여 보기에 대 한 지원이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-674">The previous ASP.NET MVC preview included support for views using Razor syntax based on C#.</span></span> <span data-ttu-id="4ad3e-675">이러한 뷰는.cshtml 파일 확장명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-675">These views use the .cshtml file extension.</span></span> <span data-ttu-id="4ad3e-676">Razor를 지원 하기 위해 진행 중인 작업의 일환으로, ASP.NET MVC 3 베타에서는.vbhtml 파일 확장명을 사용 하 여 Visual Basic의 경우에 Razor 구문 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-676">As part of ongoing work to support Razor, the ASP.NET MVC 3 Beta introduces support for the Razor syntax in Visual Basic, which uses the .vbhtml file extension.</span></span>

<span data-ttu-id="4ad3e-677">에 대 한 소개를 Visual Basic 구문의 VBHTML 페이지에서 사용 하는 다음 URL에서 자습서를 참조:</span><span class="sxs-lookup"><span data-stu-id="4ad3e-677">For an introduction to using Visual Basic syntax in VBHTML pages, see the tutorial at the following URL:</span></span>

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-visual-basic](../web-pages/overview/getting-started/introducing-razor-syntax-vb.md)

### <a id="0.1__Toc274034226"></a>  <span data-ttu-id="4ad3e-678">ValidateInputAttribute 보다 세부적으로 제어</span><span class="sxs-lookup"><span data-stu-id="4ad3e-678">More Granular Control over ValidateInputAttribute</span></span>

<span data-ttu-id="4ad3e-679">ASP.NET MVC에는 항상 들어오는 요청에 악의적인 입력 포함 되어 있지 않은지를 핵심 ASP.NET 요청 유효성 검사 인프라를 호출 하는 ValidateInputAttribute 클래스를 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-679">ASP.NET MVC has always included the ValidateInputAttribute class, which invokes the core ASP.NET request validation infrastructure to make sure that the incoming request does not contain potentially malicious input.</span></span> <span data-ttu-id="4ad3e-680">입력된 유효성 검사는 기본적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-680">By default, input validation is enabled.</span></span> <span data-ttu-id="4ad3e-681">다음 예제와 같이 ValidateInputAttribute 특성을 사용 하 여 요청 유효성 검사를 비활성화 하는 것이 불가능:</span><span class="sxs-lookup"><span data-stu-id="4ad3e-681">It is possible to disable request validation by using the ValidateInputAttribute attribute, as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample37.cs)]

<span data-ttu-id="4ad3e-682">그러나 많은 웹 응용 프로그램 할 나머지 필드 하지 않아야 하는 동안 HTML을 허용 해야 하는 개별 양식 필드.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-682">However, many web applications have individual form fields that need to allow HTML, while the remaining fields should not.</span></span> <span data-ttu-id="4ad3e-683">이제 ValidateInputAttribute 클래스 요청 유효성 검사에 포함 되지 않아야 하는 필드 목록을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-683">The ValidateInputAttribute class now lets you specify a list of fields that should not be included in request validation.</span></span>

<span data-ttu-id="4ad3e-684">예를 들어 블로그 엔진을 개발 하는 경우 본문 및 요약 필드에 태그를 허용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-684">For example, if you are developing a blog engine, you might want to allow markup in the Body and Summary fields.</span></span> <span data-ttu-id="4ad3e-685">이러한 필드는 각각 속성 이름 ("Body" 및 "요약")에 해당 하는 name 특성이 있는 두 개의 입력된 요소에 의해 표현 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-685">These fields might be represented by two input element, each with a name attribute corresponding to the property name ("Body" and "Summary").</span></span> <span data-ttu-id="4ad3e-686">요청을 사용 하지 않도록 설정 하려면 이러한 필드에 대 한 유효성 검사 (쉼표로 구분) 다음 예제와 같이 ValidateInput 클래스의 제외 속성에 이름 으로만 지정:</span><span class="sxs-lookup"><span data-stu-id="4ad3e-686">To disable request validation for these fields only, specify the names (comma-separated) in the Exclude property of the ValidateInput class, as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample38.cs)]

### <a id="0.1__Toc274034227"></a>  <span data-ttu-id="4ad3e-687">도우미 밑줄 하이픈에 대 한 변환 익명 개체를 사용 하 여 지정 된 HTML 특성 이름</span><span class="sxs-lookup"><span data-stu-id="4ad3e-687">Helpers Convert Underscores to Hyphens for HTML Attribute Names Specified Using Anonymous Objects</span></span>

<span data-ttu-id="4ad3e-688">도우미 메서드는 다음 예제 처럼 익명 개체를 사용 하 여 특성 이름/값 쌍을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-688">Helper methods let you specify attribute name/value pairs using an anonymous object, as in the following example:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample39.cs)]

<span data-ttu-id="4ad3e-689">ASP.NET에서 속성 이름에 대 한 하이픈을 사용할 수 없으므로이 접근 방식을 특성 이름에서 하이픈을 사용 하 여 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-689">This approach doesn't let you use hyphens in the attribute name, because a hyphen cannot be used for a property name in ASP.NET.</span></span> <span data-ttu-id="4ad3e-690">그러나 하이픈은 사용자 지정 HTML5 특성;에 대 한 중요 한 예를 들어 HTML5 "데이터-" 접두사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-690">However, hyphens are important for custom HTML5 attributes; for example, HTML5 uses the "data-" prefix.</span></span>

<span data-ttu-id="4ad3e-691">같은 시간에 밑줄 html에서 특성 이름에 대 한 사용할 수 없지만 속성 이름 내에서 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-691">At the same time, underscores cannot be used for attribute names in HTML, but are valid within property names.</span></span> <span data-ttu-id="4ad3e-692">따라서 익명 개체를 사용 하 여 특성을 지정 하는 경우 및 특성 이름에 밑줄을 포함 하는 경우, 도우미 메서드는 하이픈을 밑줄을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-692">Therefore, if you specify attributes using an anonymous object, and if the attribute names include an underscore,, helper methods will convert the underscores to hyphens.</span></span> <span data-ttu-id="4ad3e-693">예를 들어 다음 도우미 구문을 밑줄을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-693">For example, the following helper syntax uses an underscore:</span></span>

[!code-csharp[Main](mvc3-release-notes/samples/sample40.cs)]

<span data-ttu-id="4ad3e-694">앞의 예제 도우미를 실행할 때 다음 태그를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-694">The previous example renders the following markup when the helper runs:</span></span>

[!code-html[Main](mvc3-release-notes/samples/sample41.html)]

## <a id="0.1__Toc274034228"></a>  <span data-ttu-id="4ad3e-695">버그 수정</span><span class="sxs-lookup"><span data-stu-id="4ad3e-695">Bug Fixes</span></span>

<span data-ttu-id="4ad3e-696">EditorFor 및 DisplayFor 템플릿 도우미에 대 한 기본 개체 템플릿을 이제 DisplayAttribute.Order 속성에 지정 된 순서 지정을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-696">The default object template for the EditorFor and DisplayFor template helpers now supports the ordering specified in the DisplayAttribute.Order property.</span></span> <span data-ttu-id="4ad3e-697">(이전 버전에서는 순서 설정을 사용 하지 않았습니다.)</span><span class="sxs-lookup"><span data-stu-id="4ad3e-697">(In previous versions, the Order setting was not used.)</span></span>

<span data-ttu-id="4ad3e-698">클라이언트 유효성 검사는 이제 유효성 검사 특성이 적용 하는 재정의 된 속성의 유효성 검사를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-698">Client validation now supports validation of overridden properties that have validation attributes applied.</span></span>

<span data-ttu-id="4ad3e-699">JsonValueProviderFactory은 이제 기본적으로 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-699">JsonValueProviderFactory is now registered by default.</span></span>

## <a id="0.1__Toc274034229"></a>  <span data-ttu-id="4ad3e-700">주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="4ad3e-700">Breaking Changes</span></span>

<span data-ttu-id="4ad3e-701">예외 필터에 대 한 실행 순서 값이 동일한 예외 필터에 대 한 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-701">The order of execution for exception filters has changed for exception filters that have the same Order value.</span></span> <span data-ttu-id="4ad3e-702">ASP.NET MVC 2 및 이전 버전에서는 예외는 작업 메서드의 예외 필터 전에 실행 된 동작 메서드에 따라 동일한 순서를 가진 컨트롤러에서 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-702">In ASP.NET MVC 2 and earlier, exception filters on the controller with the same Order as those on an action method were executed before the exception filters on the action method.</span></span> <span data-ttu-id="4ad3e-703">지정된 된 순서 값 없이 예외 필터가 적용 된 경우의 경우 일반적으로 것 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-703">This would typically be the case when exception filters were applied without a specified Order value.</span></span> <span data-ttu-id="4ad3e-704">ASP.NET MVC 3에서이 순서가 반대로 변경 되었습니다 가장 구체적인 예외 처리기는 먼저 실행 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-704">In ASP.NET MVC 3, this order has been reversed so that the most specific exception handler executes first.</span></span> <span data-ttu-id="4ad3e-705">이전 버전에서와 Order 속성을 명시적으로 지정 하는 경우 필터가 지정 된 순서로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-705">As in earlier versions, if the Order property is explicitly specified, the filters are run in the specified order.</span></span>

## <a id="0.1__Toc274034230"></a>  <span data-ttu-id="4ad3e-706">알려진된 문제</span><span class="sxs-lookup"><span data-stu-id="4ad3e-706">Known Issues</span></span>

<span data-ttu-id="4ad3e-707">설치 하는 동안 EULA 동의 대화 상자 예정 보다 작은 창에서 사용 약관을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-707">During installation, the EULA acceptance dialog box displays the license terms in a window that is smaller than intended.</span></span>

<span data-ttu-id="4ad3e-708">Razor 뷰 구문 강조 표시 및 IntelliSense 지원이 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-708">Razor views do not have IntelliSense support nor syntax highlighting.</span></span> <span data-ttu-id="4ad3e-709">Visual Studio에서 Razor 구문에 대 한 지원을 이후 버전의 일부로 포함 된다는 것으로 예상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-709">It is anticipated that support for Razor syntax in Visual Studio will be included as part of a later release.</span></span>

<span data-ttu-id="4ad3e-710">Razor 뷰 (CSHTML 파일)를 편집 하는 경우는 <a id="0.1__Toc224729061"> </a> <a id="0.1__Toc238051347"> </a> Visual Studio에서 메뉴 항목 이동에 컨트롤러를 사용할 수 없으며 되며 코드 조각이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-710">When you are editing a Razor view (CSHTML file), the <a id="0.1__Toc224729061"></a><a id="0.1__Toc238051347"></a> Go To Controller menu item in Visual Studio will not be available, and there are no code snippets.</span></span>

<span data-ttu-id="4ad3e-711">사용 하는 경우는 @model 강력한 형식의 CSHTML 지정 하려면 다음 구문을 사용 보기, 형식에 대 한 언어별 바로 가기를 인식 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-711">When using the @model syntax to specify a strongly typed CSHTML view, language-specific shortcuts for types are not recognized.</span></span> <span data-ttu-id="4ad3e-712">예를 들어 @model int 작동 하지 것입니다 되지만 @model Int32 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-712">For example, @model int will not work, but @model Int32 will work.</span></span> <span data-ttu-id="4ad3e-713">이 버그에 대 한 해결 방법은 모델 유형을 지정 하는 경우 실제 형식 이름을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-713">The workaround for this bug is to use the actual type name when you specify the model type.</span></span>

<span data-ttu-id="4ad3e-714">사용 하는 경우는 @model 강력한 형식의 CSHTML 뷰를 지정 하는 구문 (또는 @ModelType VBHTML 강력한 형식의 뷰를 지정 하려면), nullable 형식 및 배열 선언과 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-714">When using the @model syntax to specify a strongly typed CSHTML view (or @ModelType to specify a strongly typed VBHTML view), nullable types and array declarations are not supported.</span></span> <span data-ttu-id="4ad3e-715">예를 들어 @model int? 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-715">For example, @model int? is not supported.</span></span> <span data-ttu-id="4ad3e-716">대신를 사용 하 여 `@model Nullable<Int32>`합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-716">Instead, use `@model Nullable<Int32>`.</span></span> <span data-ttu-id="4ad3e-717">구문을 @model string 지원 되지 않습니다; 대신, `@model IList<string>`합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-717">The syntax @model string[] is also not supported; instead, use `@model IList<string>`.</span></span>

<span data-ttu-id="4ad3e-718">ASP.NET MVC 2 프로젝트를 ASP.NET MVC 3으로 업그레이드 하는 경우에 다음 Web.config 파일의 appSettings 섹션을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-718">When you upgrade an ASP.NET MVC 2 project to ASP.NET MVC 3, make sure to add the following to the appSettings section of the Web.config file:</span></span>

[!code-xml[Main](mvc3-release-notes/samples/sample42.xml)]

<span data-ttu-id="4ad3e-719">폼 인증을 항상 Web.config에 사용 되는 폼 인증 설정 무시 ~/Account/로그인에 인증 되지 않은 사용자를 리디렉션 시키는 알려진된 문제가 있습니다. 이를 해결 하려면 다음 응용 프로그램 설정을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-719">There's a known issue that causes Forms Authentication to always redirect unauthenticated users to ~/Account/Login, ignoring the forms authentication setting used in Web.config. The workaround is to add the following app setting.</span></span>

[!code-xml[Main](mvc3-release-notes/samples/sample43.xml)]

## <a id="0.1__Toc274034231"></a>  <span data-ttu-id="4ad3e-720">Disclaimer</span><span class="sxs-lookup"><span data-stu-id="4ad3e-720">Disclaimer</span></span>

<span data-ttu-id="4ad3e-721">© 2011 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-721">© 2011 Microsoft Corporation.</span></span> <span data-ttu-id="4ad3e-722">All rights reserved.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-722">All rights reserved.</span></span> <span data-ttu-id="4ad3e-723">이 설명서는 제공 "로-됩니다."</span><span class="sxs-lookup"><span data-stu-id="4ad3e-723">This document is provided "as-is."</span></span> <span data-ttu-id="4ad3e-724">URL 및 기타 인터넷 웹 사이트 참조를 포함 한이 문서의 내용과 관점은 예 고 없이 변경 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-724">Information and views expressed in this document, including URL and other Internet Web site references, may change without notice.</span></span> <span data-ttu-id="4ad3e-725">정보의 사용으로 발생하는 위험은 귀하의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-725">You bear the risk of using it.</span></span>

<span data-ttu-id="4ad3e-726">이 문서는 귀하에게 Microsoft 제품의 어떠한 지적 재산에 대한 법적 권리도 부여하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-726">This document does not provide you with any legal rights to any intellectual property in any Microsoft product.</span></span> <span data-ttu-id="4ad3e-727">귀하는 참조를 위해 내부적으로 이 문서를 복사하고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad3e-727">You may copy and use this document for your internal, reference purposes.</span></span>
