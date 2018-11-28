---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
title: ASP.NET 4.5 Web Forms 및 Visual Studio 2013 시작 하기 | Microsoft Docs
author: Erikre
description: 이 단계별 자습서 시리즈는 ASP.NET 4.5와 Microsoft Visual Studio Expres를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 하는 중...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 9b96eaa1-8ef0-4338-a2e8-e0f970bfaf68
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
msc.type: authoredcontent
ms.openlocfilehash: b9ed6ce4ac13f047f53c56e183433cbd038ea15c
ms.sourcegitcommit: e9b99854b0a8021dafabee0db5e1338067f250a9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52450686"
---
<a name="getting-started-with-aspnet-45-web-forms-and-visual-studio-2013"></a><span data-ttu-id="a4dfe-103">ASP.NET 4.5 Web Forms 및 Visual Studio 2013 시작</span><span class="sxs-lookup"><span data-stu-id="a4dfe-103">Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013</span></span>
====================
<span data-ttu-id="a4dfe-104">[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="a4dfe-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="a4dfe-105">[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF) 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="a4dfe-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

<span data-ttu-id="a4dfe-106">이 단계별 자습서 시리즈는 ASP.NET 4.5와 Microsoft Visual Studio Express 2013 for Web 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-106">This step-by-step tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> 

## <a name="introduction"></a><span data-ttu-id="a4dfe-107">소개</span><span class="sxs-lookup"><span data-stu-id="a4dfe-107">Introduction</span></span>

<span data-ttu-id="a4dfe-108">이 자습서 시리즈에서는 Visual Studio Express 2013을 사용 하 여 웹 및 ASP.NET 4.5에 대 한 ASP.NET Web Forms 응용 프로그램을 만드는 데 필요한 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-108">This series of tutorials guides you through the steps required to create an ASP.NET Web Forms application using Visual Studio Express 2013 for Web and ASP.NET 4.5.</span></span>

<span data-ttu-id="a4dfe-109">만든 응용 프로그램의 이름이 **Wingtip Toys**합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-109">The application you'll create is named **Wingtip Toys**.</span></span> <span data-ttu-id="a4dfe-110">온라인 항목을 판매 하는 프런트 스토어 웹 사이트의 간단한 예 이며</span><span class="sxs-lookup"><span data-stu-id="a4dfe-110">It's a simplified example of a store front web site that sells items online.</span></span> <span data-ttu-id="a4dfe-111">이 자습서 시리즈 ASP.NET 4.5의 새로운 기능을 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-111">This tutorial series highlights new features available in ASP.NET 4.5.</span></span>

<span data-ttu-id="a4dfe-112">주석은 환영 해 의견에 따라이 자습서 시리즈를 업데이트 하기 위해 모든 노력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-112">Comments are welcome, and we'll make every effort to update this tutorial series based on your suggestions.</span></span>

### <a name="download-completed-project"></a><span data-ttu-id="a4dfe-113">다운로드가 완료 된 프로젝트</span><span class="sxs-lookup"><span data-stu-id="a4dfe-113">Download completed project</span></span>

<span data-ttu-id="a4dfe-114">완성된 된 자습서를 포함 하는 C# 프로젝트를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-114">You can download a C# project that contains the completed tutorial.</span></span>

- <span data-ttu-id="a4dfe-115">[Getting Started with ASP.NET 4.5 Web Forms 및 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span><span class="sxs-lookup"><span data-stu-id="a4dfe-115">[Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span></span>

### <a name="review-the-content-by-taking-the-related-aspnet-web-forms-quiz"></a><span data-ttu-id="a4dfe-116">ASP.NET Web Forms 관련된 퀴즈를 수행 하 여 콘텐츠를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-116">Review the content by taking the related ASP.NET Web Forms quiz</span></span>

<span data-ttu-id="a4dfe-117">이 자습서를 완료 하면 지식을 테스트 하 고 수행 하 여 주요 개념을 보강 합니다 [ASP.NET Web Forms 퀴즈](http://quizapp.cloudapp.net/?quiz=ASP.NET&cdn_id=2014-01-17-001)합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-117">After you complete this tutorial, test your knowledge and reinforce key concepts by taking the [ASP.NET Web Forms Quiz](http://quizapp.cloudapp.net/?quiz=ASP.NET&cdn_id=2014-01-17-001).</span></span> <span data-ttu-id="a4dfe-118">이 자습서 시리즈에 포함 된 콘텐츠에서이 퀴즈 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-118">This quiz was specifically designed from content contained in this tutorial series.</span></span> <span data-ttu-id="a4dfe-119">각 질문 퀴즈에 대 한 추가 지침에 대 한 링크와 함께 설명이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-119">Each question in the quiz provides an explanation along with links to additional guidance.</span></span>

- [<span data-ttu-id="a4dfe-120">ASP.NET Web Forms 퀴즈</span><span class="sxs-lookup"><span data-stu-id="a4dfe-120">ASP.NET Web Forms Quiz</span></span>](http://quizapp.cloudapp.net/?quiz=ASP.NET)

### <a name="audience"></a><span data-ttu-id="a4dfe-121">대상 사용자</span><span class="sxs-lookup"><span data-stu-id="a4dfe-121">Audience</span></span>

<span data-ttu-id="a4dfe-122">이 자습서 시리즈의 사용자는 ASP.NET Web Forms에는 숙련 된 개발자.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-122">The intended audience of this tutorial series is experienced developers who are new to ASP.NET Web Forms.</span></span> <span data-ttu-id="a4dfe-123">이 자습서 시리즈에서 관심이 있는 개발자는 다음 기술이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-123">A developer interested in this tutorial series should have the following skills:</span></span>

- <span data-ttu-id="a4dfe-124">친숙 한 개체 지향 프로그래밍 (OOP) 언어</span><span class="sxs-lookup"><span data-stu-id="a4dfe-124">Familiar with an object oriented programming (OOP) language</span></span>
- <span data-ttu-id="a4dfe-125">익숙한 웹 개발 개념 (HTML, CSS, JavaScript)</span><span class="sxs-lookup"><span data-stu-id="a4dfe-125">Familiar with Web development concepts (HTML, CSS, JavaScript)</span></span>
- <span data-ttu-id="a4dfe-126">관계형 데이터베이스 개념을 잘 알고</span><span class="sxs-lookup"><span data-stu-id="a4dfe-126">Familiar with relational database concepts</span></span>
- <span data-ttu-id="a4dfe-127">N 계층 아키텍처 개념을 잘 알고</span><span class="sxs-lookup"><span data-stu-id="a4dfe-127">Familiar with n-tier architecture concepts</span></span>

<span data-ttu-id="a4dfe-128">위에 나열 된 영역을 검토 하려는 경우 다음 콘텐츠를 검토 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-128">If you are interested in reviewing the areas listed above, consider reviewing the following content:</span></span>

- [<span data-ttu-id="a4dfe-129">Visual C# 시작</span><span class="sxs-lookup"><span data-stu-id="a4dfe-129">Getting Started with Visual C#</span></span>](https://msdn.microsoft.com/library/a72418yk.aspx)
- <span data-ttu-id="a4dfe-130">[웹 개발](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, PHP, JQuery](http://w3schools.com/)</span><span class="sxs-lookup"><span data-stu-id="a4dfe-130">[Web Development](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, PHP, JQuery](http://w3schools.com/)</span></span>
- [<span data-ttu-id="a4dfe-131">관계형 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="a4dfe-131">Relational database</span></span>](http://en.wikipedia.org/wiki/Relational_database)
- [<span data-ttu-id="a4dfe-132">다중 계층 아키텍처</span><span class="sxs-lookup"><span data-stu-id="a4dfe-132">Multitier architecture</span></span>](http://en.wikipedia.org/wiki/Multitier_architecture)

### <a name="application-features"></a><span data-ttu-id="a4dfe-133">응용 프로그램 기능</span><span class="sxs-lookup"><span data-stu-id="a4dfe-133">Application Features</span></span>

<span data-ttu-id="a4dfe-134">이 시리즈에 제공 된 ASP.NET Web Form 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-134">The ASP.NET Web Form features presented in this series include:</span></span>

- <span data-ttu-id="a4dfe-135">웹 응용 프로그램 프로젝트 (웹 사이트 프로젝트가 아닌)</span><span class="sxs-lookup"><span data-stu-id="a4dfe-135">The Web Application Project (not Web Site Project)</span></span>
- <span data-ttu-id="a4dfe-136">Web Forms</span><span class="sxs-lookup"><span data-stu-id="a4dfe-136">Web Forms</span></span>
- <span data-ttu-id="a4dfe-137">마스터 페이지, 구성</span><span class="sxs-lookup"><span data-stu-id="a4dfe-137">Master Pages, Configuration</span></span>
- <span data-ttu-id="a4dfe-138">부트스트랩</span><span class="sxs-lookup"><span data-stu-id="a4dfe-138">Bootstrap</span></span>
- <span data-ttu-id="a4dfe-139">Entity Framework 코드 먼저 LocalDB</span><span class="sxs-lookup"><span data-stu-id="a4dfe-139">Entity Framework Code First, LocalDB</span></span>
- <span data-ttu-id="a4dfe-140">요청 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="a4dfe-140">Request Validation</span></span>
- <span data-ttu-id="a4dfe-141">모델 바인딩, 데이터 주석 및 공급자 값 강력한 형식의 데이터 컨트롤</span><span class="sxs-lookup"><span data-stu-id="a4dfe-141">Strongly Typed Data Controls, Model Binding, Data Annotations, and Value Providers</span></span>
- <span data-ttu-id="a4dfe-142">SSL 및 OAuth</span><span class="sxs-lookup"><span data-stu-id="a4dfe-142">SSL and OAuth</span></span>
- <span data-ttu-id="a4dfe-143">ASP.NET Id, 구성 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="a4dfe-143">ASP.NET Identity, Configuration, and Authorization</span></span>
- <span data-ttu-id="a4dfe-144">비간섭 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="a4dfe-144">Unobtrusive Validation</span></span>
- <span data-ttu-id="a4dfe-145">라우팅</span><span class="sxs-lookup"><span data-stu-id="a4dfe-145">Routing</span></span>
- <span data-ttu-id="a4dfe-146">ASP.NET 오류 처리</span><span class="sxs-lookup"><span data-stu-id="a4dfe-146">ASP.NET Error Handling</span></span>

### <a name="application-scenarios-and-tasks"></a><span data-ttu-id="a4dfe-147">응용 프로그램 시나리오 및 작업</span><span class="sxs-lookup"><span data-stu-id="a4dfe-147">Application Scenarios and Tasks</span></span>

<span data-ttu-id="a4dfe-148">이 시리즈에 설명 된 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-148">Tasks demonstrated in this series include:</span></span>

- <span data-ttu-id="a4dfe-149">만들기, 검토 및 새 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-149">Creating, reviewing and running the new project</span></span>
- <span data-ttu-id="a4dfe-150">데이터베이스 구조 만들기</span><span class="sxs-lookup"><span data-stu-id="a4dfe-150">Creating the database structure</span></span>
- <span data-ttu-id="a4dfe-151">초기화 및 데이터베이스 시 딩</span><span class="sxs-lookup"><span data-stu-id="a4dfe-151">Initializing and seeding the database</span></span>
- <span data-ttu-id="a4dfe-152">스타일, 그래픽 및 마스터 페이지를 사용 하 여 UI 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="a4dfe-152">Customizing the UI using styles, graphics and a master page</span></span>
- <span data-ttu-id="a4dfe-153">페이지 및 탐색 기능 추가</span><span class="sxs-lookup"><span data-stu-id="a4dfe-153">Adding pages and navigation</span></span>
- <span data-ttu-id="a4dfe-154">메뉴 세부 정보 및 제품 데이터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-154">Displaying menu details and product data</span></span>
- <span data-ttu-id="a4dfe-155">쇼핑 카트 만들기</span><span class="sxs-lookup"><span data-stu-id="a4dfe-155">Creating a shopping cart</span></span>
- <span data-ttu-id="a4dfe-156">추가 SSL 및 OAuth 지원</span><span class="sxs-lookup"><span data-stu-id="a4dfe-156">Adding SSL and OAuth support</span></span>
- <span data-ttu-id="a4dfe-157">지불 방법 추가</span><span class="sxs-lookup"><span data-stu-id="a4dfe-157">Adding a payment method</span></span>
- <span data-ttu-id="a4dfe-158">관리자 역할 및 응용 프로그램에 사용자를 포함 하 여</span><span class="sxs-lookup"><span data-stu-id="a4dfe-158">Including an administrator role and a user to the application</span></span>
- <span data-ttu-id="a4dfe-159">특정 페이지 및 폴더에 대 한 액세스 제한</span><span class="sxs-lookup"><span data-stu-id="a4dfe-159">Restricting access to specific pages and folder</span></span>
- <span data-ttu-id="a4dfe-160">웹 응용 프로그램 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-160">Uploading a file to the web application</span></span>
- <span data-ttu-id="a4dfe-161">입력된 유효성 검사 구현</span><span class="sxs-lookup"><span data-stu-id="a4dfe-161">Implementing input validation</span></span>
- <span data-ttu-id="a4dfe-162">웹 응용 프로그램에 대 한 경로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-162">Registering routes for the web application</span></span>
- <span data-ttu-id="a4dfe-163">오류 처리 및 오류 로깅 구현</span><span class="sxs-lookup"><span data-stu-id="a4dfe-163">Implementing error handling and error logging</span></span>

## <a name="overview"></a><span data-ttu-id="a4dfe-164">개요</span><span class="sxs-lookup"><span data-stu-id="a4dfe-164">Overview</span></span>

<span data-ttu-id="a4dfe-165">ASP.NET Web Forms를 처음 접하는 경우 있 프로그래밍 개념 사용 경험, 오른쪽이 자습서를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-165">If you are new to ASP.NET Web Forms but have familiarity with programming concepts, you have the right tutorial.</span></span> <span data-ttu-id="a4dfe-166">ASP.NET Web Forms에 익숙한 경우 ASP.NET 4.5의 새로운 기능으로이 자습서 시리즈에서 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-166">If you are already familiar with ASP.NET Web Forms, you can benefit from this tutorial series by the new features available in ASP.NET 4.5.</span></span> <span data-ttu-id="a4dfe-167">프로그래밍 개념 및 ASP.NET Web Forms에 익숙한 경우에 Web Forms에 제공 된 추가 자습서를 참조 하세요 [Getting Started](../../../index.md) ASP.NET 웹 사이트의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-167">If you are unfamiliar with programming concepts and ASP.NET Web Forms, see the additional tutorials provided in the Web Forms [Getting Started](../../../index.md) section on the ASP.NET Web site.</span></span>

<span data-ttu-id="a4dfe-168">특정 **최신** ASP.NET 4.5 기능 제공이 Web Forms에서 자습서 시리즈에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-168">The specific **latest** ASP.NET 4.5 features provided in this Web Forms tutorial series include the following:</span></span>

- <span data-ttu-id="a4dfe-169">만들기 위한 간단한 UI를 제공 하는 프로젝트 [여러 ASP.NET 프레임 워크에 대 한 지원](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) (Web Forms, MVC 및 Web API).</span><span class="sxs-lookup"><span data-stu-id="a4dfe-169">A simple UI for creating projects that offer [support for multiple ASP.NET frameworks](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) (Web Forms, MVC, and Web API).</span></span>
- <span data-ttu-id="a4dfe-170">[부트스트랩](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), 응답성이 뛰어난 디자인 및 테마 기능을 제공 하는 레이아웃 및 테마 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-170">[Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), a layout and theming framework that provides responsive design and theming capabilities.</span></span>
- <span data-ttu-id="a4dfe-171">[ASP.NET Id](../../../../identity/index.md), 웹 호스팅 IIS 외에 소프트웨어를 사용 하 여 모든 ASP.NET 프레임 워크와에서 동일 하 게 작동 하는 새로운 ASP.NET 멤버 자격 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-171">[ASP.NET Identity](../../../../identity/index.md), a new ASP.NET membership system that works the same in all ASP.NET frameworks and works with web hosting software other than IIS.</span></span>
- <span data-ttu-id="a4dfe-172">[Entity Framework 6](https://msdn.microsoft.com/data/ef.aspx)형식의 개체를 검색 하 고 강력 하 게 데이터를 조작할 수 있는 Entity Framework에 대 한 업데이트, 비동기적으로 일시적인 연결 오류 처리 및 SQL 문을 로그 데이터에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-172">[Entity Framework 6](https://msdn.microsoft.com/data/ef.aspx), an update to the Entity Framework which allows you retrieve and manipulate data as strongly typed objects, access data asynchronously, handle transient connection faults, and log SQL statements.</span></span>

<span data-ttu-id="a4dfe-173">ASP.NET 4.5 기능의 전체 목록은 참조 하세요 [ASP.NET 및 Web Tools for Visual Studio 2013 릴리스 정보](../../../../visual-studio/overview/2013/release-notes.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-173">For a complete list of ASP.NET 4.5 features, see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](../../../../visual-studio/overview/2013/release-notes.md).</span></span>

### <a name="the-wingtip-toys-sample-application"></a><span data-ttu-id="a4dfe-174">Wingtip Toys 샘플 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="a4dfe-174">The Wingtip Toys Sample Application</span></span>

<span data-ttu-id="a4dfe-175">다음 스크린샷은이 자습서 시리즈에서 만든 ASP.NET Web forms 응용 프로그램의 빠른 보기를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-175">The following screen shots provide a quick view of the ASP.NET Web forms application that you will create in this tutorial series.</span></span> <span data-ttu-id="a4dfe-176">Visual Studio Express 2013 for Web에서에서 응용 프로그램을 실행 하는 경우 다음 웹 홈 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-176">When you run the application from Visual Studio Express 2013 for Web, you will see the following web Home page.</span></span>

![Wingtip Toys-기본 페이지](introduction-and-overview/_static/image1.png)

<span data-ttu-id="a4dfe-178">새 사용자로 등록 하거나 기존 사용자로 로그인 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-178">You can register as a new user, or log in as an existing user.</span></span> <span data-ttu-id="a4dfe-179">탐색은 데이터베이스에서 사용할 수 있는 제품을 검색 하 여 맨 위에 있는 각 제품 범주에 대해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-179">Navigation is provided at the top for each product category by retrieving the available products from the database.</span></span>

<span data-ttu-id="a4dfe-180">제품 링크를 선택 하면 모든 사용 가능한 제품 목록을 보려면 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-180">By selecting the Products link, you will be able to see a list of all available products.</span></span>

![Wingtip Toys-제품](introduction-and-overview/_static/image2.png)

<span data-ttu-id="a4dfe-182">또한 나열된 된 제품 중 하나를 선택 하 여 개별 제품 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-182">You can also see individual product details by selecting any of the listed products.</span></span>

![Wingtip Toys-제품 세부 정보](introduction-and-overview/_static/image3.png)

<span data-ttu-id="a4dfe-184">사용자로 등록 한 Web Forms 템플릿의 기본 기능을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-184">As a user, you can register and log in using the default functionality of the Web Forms template.</span></span> <span data-ttu-id="a4dfe-185">이 자습서에는 또한 기존 Gmail 계정을 사용 하 여 로그인 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-185">This tutorial also explains how to login using an existing Gmail account.</span></span> <span data-ttu-id="a4dfe-186">또한 추가 하 고 데이터베이스에서 제품을 제거 하려면 관리자 권한으로 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-186">Additionally, you can login as the administrator to add and remove products from the database.</span></span>

![Wingtip Toys-로그인](introduction-and-overview/_static/image4.png)

<span data-ttu-id="a4dfe-188">사용자로 로그인 하면, PayPal로 체크 아웃을 쇼핑 카트에 제품을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-188">Once you have logged in as a user, you can add products to the shopping cart and checkout with PayPal.</span></span> <span data-ttu-id="a4dfe-189">이 샘플 응용 프로그램은 PayPal의 개발자 샌드박스를 사용 하 여 작동 하도록 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-189">Note that this sample application is designed to function with PayPal's developer sandbox.</span></span> <span data-ttu-id="a4dfe-190">실제 비용 트랜잭션이 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-190">No actual money transaction will take place.</span></span>

![Wingtip Toys-쇼핑 카트](introduction-and-overview/_static/image5.png)

<span data-ttu-id="a4dfe-192">PayPal는 사용자 계정, 순서 및 결제 정보를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-192">PayPal will confirm your account, order, and payment information.</span></span>

![Wingtip Toys-PayPal](introduction-and-overview/_static/image6.png)

<span data-ttu-id="a4dfe-194">PayPal에서 반환한 검토 하 고 주문을 완료 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-194">After returning from PayPal, you can review and complete your order.</span></span>

![Wingtip Toys-주문 검토](introduction-and-overview/_static/image7.png)

## <a name="prerequisites"></a><span data-ttu-id="a4dfe-196">전제 조건</span><span class="sxs-lookup"><span data-stu-id="a4dfe-196">Prerequisites</span></span>

<span data-ttu-id="a4dfe-197">시작 하기 전에 다음 소프트웨어를 컴퓨터에 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-197">Before you start, make sure that you have the following software installed on your computer:</span></span>

- <span data-ttu-id="a4dfe-198">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) 나 [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-198">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) or [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="a4dfe-199">.NET Framework는 자동으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-199">The .NET Framework is installed automatically.</span></span>

<span data-ttu-id="a4dfe-200">이 자습서 시리즈에서는 Microsoft Visual Studio Express 2013 for Web</span><span class="sxs-lookup"><span data-stu-id="a4dfe-200">This tutorial series uses Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="a4dfe-201">이 자습서 시리즈를 완료 하려면 Microsoft Visual Studio Express 2013 for Web 또는 Microsoft Visual Studio 2013을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-201">You can use either Microsoft Visual Studio Express 2013 for Web or Microsoft Visual Studio 2013 to complete this tutorial series.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="a4dfe-202">Microsoft Visual Studio 2013 및 Microsoft Visual Studio Express 2013 for Web은 종종 라고 Visual Studio이 자습서 시리즈 전체.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-202">Microsoft Visual Studio 2013 and Microsoft Visual Studio Express 2013 for Web will often be referred to as Visual Studio throughout this tutorial series.</span></span>


<span data-ttu-id="a4dfe-203">설치는 Visual Studio 버전에 이미 있는 경우 설치 프로세스는 기존 버전 옆에 있는 Visual Studio 2013 또는 Microsoft Visual Studio Express 2013 for Web 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-203">If you already have a Visual Studio version installed, the installation process will install Visual Studio 2013 or Microsoft Visual Studio Express 2013 for Web next to the existing version.</span></span> <span data-ttu-id="a4dfe-204">이전 버전에서 만든 사이트 Visual Studio 2013에서 열 수 및 이전 버전에서 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-204">Sites that you created in earlier versions can be opened in Visual Studio 2013 and continue to open in previous versions.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="a4dfe-205">이 연습을 선택 했다고 가정 합니다 *웹 개발* 설정 모음을 처음으로 Visual Studio를 시작 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-205">This walkthrough assumes that you selected the *Web Development* collection of settings the first time that you started Visual Studio.</span></span> <span data-ttu-id="a4dfe-206">자세한 내용은 [방법: 웹 개발 환경 설정 선택](https://msdn.microsoft.com/library/ff521558.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-206">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>


## <a name="download-the-sample-application"></a><span data-ttu-id="a4dfe-207">샘플 응용 프로그램 다운로드</span><span class="sxs-lookup"><span data-stu-id="a4dfe-207">Download the Sample Application</span></span>

<span data-ttu-id="a4dfe-208">필수 구성 요소를 설치한 후이 자습서 시리즈에서 제공 되는 새 웹 프로젝트 만들기를 시작 하려면 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-208">After installing the prerequisites, you are ready to begin creating the new Web project that is presented in this tutorial series.</span></span> <span data-ttu-id="a4dfe-209">원하는 경우 **필요에 따라** 이 자습서 시리즈에서 만든 샘플 응용 프로그램을 실행 하면 해당 사이트에서 다운로드할 수는 MSDN 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-209">If you would like to **optionally** run the sample application that this tutorial series creates, you can download it from the MSDN Samples site.</span></span> <span data-ttu-id="a4dfe-210">이 다운로드에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-210">This download contains the following:</span></span>

- <span data-ttu-id="a4dfe-211">샘플 응용 프로그램을 *WingtipToys* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-211">The sample application in the *WingtipToys* folder.</span></span>
- <span data-ttu-id="a4dfe-212">샘플 응용 프로그램을 만들려면 사용 하는 리소스를 *WingtipToys 자산* 폴더에는 *WingtipToys* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-212">The resources used to create the sample application in the *WingtipToys-Assets* folder in the *WingtipToys* folder.</span></span>

#### <a name="download-the-file-from-msdn-samples-site"></a><span data-ttu-id="a4dfe-213">MSDN 샘플 사이트에서 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-213">Download the file from MSDN Samples site:</span></span>

<span data-ttu-id="a4dfe-214">[Getting Started with ASP.NET 4.5 Web Forms 및 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span><span class="sxs-lookup"><span data-stu-id="a4dfe-214">[Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span></span> 

<span data-ttu-id="a4dfe-215">다운로드 되는 <em>.zip</em> 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-215">The download is a <em>.zip</em> file.</span></span> <span data-ttu-id="a4dfe-216">이 자습서 시리즈에서 만든 완료 된 프로젝트, 찾기 및 선택 합니다 <em>C#</em>폴더에는 <em>.zip</em> 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-216">To see the completed project that this tutorial series creates, find and select the <em>C#</em>folder in the <em>.zip</em> file.</span></span> <span data-ttu-id="a4dfe-217">저장 된 <em>C#</em> folderto Visual Studio 2013 프로젝트를 사용 하는 데 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-217">Save the <em>C#</em> folderto the folder you use to work with Visual Studio 2013 projects.</span></span> <span data-ttu-id="a4dfe-218">기본적으로 Visual Studio 2013 프로젝트 폴더는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-218">By default, the Visual Studio 2013 projects folder is the following:</span></span>

<span data-ttu-id="a4dfe-219"><strong>C:\Users&#92;</strong><strong><em>&lt;username&gt;</em></strong><strong>\Documents\Visual Studio 2013\Projects</strong></span><span class="sxs-lookup"><span data-stu-id="a4dfe-219"><strong>C:\Users&#92;</strong><strong><em>&lt;username&gt;</em></strong><strong>\Documents\Visual Studio 2013\Projects</strong></span></span>

<span data-ttu-id="a4dfe-220">이름 바꾸기는 ***C#*** 폴더 ***WingtipToys***합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-220">Rename the ***C#*** folder to ***WingtipToys***.</span></span>

> [!NOTE]
> <span data-ttu-id="a4dfe-221">라는 폴더를 이미 있다면 *WingtipToys* 에 프로젝트 폴더의 이름을 일시적으로 기존 폴더 이름을 바꾸기 전에 *C#* 폴더를 *WingtipToys*합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-221">If you already have a folder named *WingtipToys* in your Projects folder, temporarily rename that existing folder before renaming the *C#* folder to *WingtipToys*.</span></span>


<span data-ttu-id="a4dfe-222">완료 된 프로젝트를 실행 하려면 엽니다는 *WingtipToys* 폴더를 두 번 클릭 합니다 *WingtipToys.sln* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-222">To run the completed project, open the *WingtipToys* folder and double-click the *WingtipToys.sln* file.</span></span> <span data-ttu-id="a4dfe-223">Visual Studio 2013 프로젝트를 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-223">Visual Studio 2013 will open the project.</span></span> <span data-ttu-id="a4dfe-224">그런 다음 마우스 오른쪽 단추로 클릭 합니다 *Default.aspx* 솔루션 탐색기 창에서 파일을 마우스 오른쪽 단추 클릭 메뉴에서 브라우저에서 보기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-224">Next, right-click the *Default.aspx* file in the Solution Explorer window and click View In Browser from the right-click menu.</span></span>

### <a name="tutorial-support-and-comments"></a><span data-ttu-id="a4dfe-225">자습서 지원 및 주석</span><span class="sxs-lookup"><span data-stu-id="a4dfe-225">Tutorial Support and Comments</span></span>

<span data-ttu-id="a4dfe-226">포함 된 질문과 대답 섹션을 사용 합니다 [Getting Started with ASP.NET 4.5 Web Forms 및 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 질문이 나 의견에 대 한 샘플 (C#).</span><span class="sxs-lookup"><span data-stu-id="a4dfe-226">Use the Q AND A section included with the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample for any questions or comments.</span></span>

<span data-ttu-id="a4dfe-227">이 자습서 시리즈에 대 한 의견을 기다리겠습니다를 하 고이 자습서 시리즈에서 업데이트 되 면 노력 됩니다 계정 수정 또는 제안 자습서 주석에서 제공 되는 향상 된 기능에 대 한 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-227">Comments on this tutorial series are welcome, and when this tutorial series is updated every effort will be made to take into account corrections or suggestions for improvements that are provided in the tutorial comments.</span></span>

<span data-ttu-id="a4dfe-228">개발 하는 동안 오류가 발생 하거나 웹 사이트가 올바르게 실행 되지 않은 경우 오류 메시지가 문제의 소스에 복잡 한 단서를 제공할 수 있습니다 또는 해결 하는 방법에 설명 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-228">When an error happens during development, or if the Web site does not run correctly, the error messages may give complex clues to the source of the problem or might not explain how to fix it.</span></span> <span data-ttu-id="a4dfe-229">몇 가지 일반적인 문제 시나리오를 사용 하 여 도움이 사용할 수도 있습니다는 [ASP.NET 포럼](https://forums.asp.net/) 또는 포함 된 질문과 대답 섹션의 [Getting Started with ASP.NET 4.5 Web Forms 및 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) ( C#) 샘플.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-229">To help you with some common problem scenarios, you can also use the [ASP.NET forums](https://forums.asp.net/) or the Q AND A section included with the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample.</span></span> <span data-ttu-id="a4dfe-230">오류 메시지를 가져오거나 자습서를 진행할 때 작동 하지 않는 경우에 위의 위치를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4dfe-230">If you get an error message or something doesn't work as you go through the tutorials, be sure to check the above locations.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a4dfe-231">다음</span><span class="sxs-lookup"><span data-stu-id="a4dfe-231">Next</span></span>](create-the-project.md)
