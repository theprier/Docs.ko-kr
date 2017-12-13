---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
title: "ASP.NET 4.5 Web Forms 및 Visual Studio 2013 시작 | Microsoft Docs"
author: Erikre
description: "이 단계별 자습서 시리즈 ASP.NET 4.5 및 Microsoft Visual Studio Expres를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 9b96eaa1-8ef0-4338-a2e8-e0f970bfaf68
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
msc.type: authoredcontent
ms.openlocfilehash: 6ee3e244c4ed29384d11c7acc1440692d3f9b23e
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="getting-started-with-aspnet-45-web-forms-and-visual-studio-2013"></a><span data-ttu-id="c1993-103">ASP.NET 4.5 Web Forms 및 Visual Studio 2013 시작</span><span class="sxs-lookup"><span data-stu-id="c1993-103">Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013</span></span>
====================
<span data-ttu-id="c1993-104">으로 [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="c1993-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="c1993-105">[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF)를 다운로드 합니다.](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="c1993-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="c1993-106">이 단계별 자습서 시리즈 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 웹에 대 한 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-106">This step-by-step tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> [<span data-ttu-id="c1993-107">ASP.NET Web Forms 퀴즈</span><span class="sxs-lookup"><span data-stu-id="c1993-107">ASP.NET Web Forms Quiz</span></span>](http://quizapp.cloudapp.net/?quiz=ASP.NET)  
> <span data-ttu-id="c1993-108">사용자가 모르는 테스트 하 고 ASP.NET Web Forms 퀴즈를 수행 하 여 주요 개념을 강화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-108">Test your knowledge and reinforce key concepts by taking the ASP.NET Web Forms Quiz.</span></span> <span data-ttu-id="c1993-109">이 퀴즈가 자습서 시리즈에 포함 된 콘텐츠에서 특별히 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-109">This quiz was specifically designed from content contained in this tutorial series.</span></span> <span data-ttu-id="c1993-110">각 질문 퀴즈에 설명 된 추가 지침에 대 한 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-110">Each question in the quiz provides an explanation along with links to additional guidance.</span></span>


## <a name="introduction"></a><span data-ttu-id="c1993-111">소개</span><span class="sxs-lookup"><span data-stu-id="c1993-111">Introduction</span></span>

<span data-ttu-id="c1993-112">이 일련의 자습서에서는 웹 및 ASP.NET 4.5 용 Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 데 필요한 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-112">This series of tutorials guides you through the steps required to create an ASP.NET Web Forms application using Visual Studio Express 2013 for Web and ASP.NET 4.5.</span></span>

<span data-ttu-id="c1993-113">만들게 응용 프로그램의 이름이 **Wingtip Toys**합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-113">The application you'll create is named **Wingtip Toys**.</span></span> <span data-ttu-id="c1993-114">온라인 항목을 판매 하는 전면 스토어 웹 사이트의 간단한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-114">It's a simplified example of a store front web site that sells items online.</span></span> <span data-ttu-id="c1993-115">이 자습서 시리즈 ASP.NET 4.5의 새로운 기능을 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-115">This tutorial series highlights new features available in ASP.NET 4.5.</span></span>

<span data-ttu-id="c1993-116">주석은, 설정이 및 제안 사항에 따라이 자습서 시리즈를 업데이트 하기 위한 모든 작업 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-116">Comments are welcome, and we'll make every effort to update this tutorial series based on your suggestions.</span></span>

### <a name="download-completed-project"></a><span data-ttu-id="c1993-117">다운로드가 완료 프로젝트</span><span class="sxs-lookup"><span data-stu-id="c1993-117">Download completed project</span></span>

<span data-ttu-id="c1993-118">완성 된 자습서를 포함 하는 C# 프로젝트를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-118">You can download a C# project that contains the completed tutorial.</span></span>

- <span data-ttu-id="c1993-119">[ASP.NET 4.5 Web Forms 및 Visual Studio 2013-Wingtip Toys 시작](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span><span class="sxs-lookup"><span data-stu-id="c1993-119">[Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span></span>

### <a name="review-the-content-by-taking-the-related-aspnet-web-forms-quiz"></a><span data-ttu-id="c1993-120">ASP.NET Web Forms 퀴즈 관련 하 여 콘텐츠 검토</span><span class="sxs-lookup"><span data-stu-id="c1993-120">Review the content by taking the related ASP.NET Web Forms quiz</span></span>

<span data-ttu-id="c1993-121">이 자습서를 완료 한 후 사용자가 모르는 테스트 하 고 주요 개념을 수행 하 여 강화할는 [ASP.NET Web Forms 퀴즈](http://quizapp.cloudapp.net/?quiz=ASP.NET&cdn_id=2014-01-17-001)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-121">After you complete this tutorial, test your knowledge and reinforce key concepts by taking the [ASP.NET Web Forms Quiz](http://quizapp.cloudapp.net/?quiz=ASP.NET&cdn_id=2014-01-17-001).</span></span> <span data-ttu-id="c1993-122">이 퀴즈가 자습서 시리즈에 포함 된 콘텐츠에서 특별히 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-122">This quiz was specifically designed from content contained in this tutorial series.</span></span> <span data-ttu-id="c1993-123">각 질문 퀴즈에 설명 된 추가 지침에 대 한 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-123">Each question in the quiz provides an explanation along with links to additional guidance.</span></span>

- [<span data-ttu-id="c1993-124">ASP.NET Web Forms 퀴즈</span><span class="sxs-lookup"><span data-stu-id="c1993-124">ASP.NET Web Forms Quiz</span></span>](http://quizapp.cloudapp.net/?quiz=ASP.NET)

### <a name="audience"></a><span data-ttu-id="c1993-125">대상 사용자</span><span class="sxs-lookup"><span data-stu-id="c1993-125">Audience</span></span>

<span data-ttu-id="c1993-126">이 자습서 시리즈의 사용자는 ASP.NET Web Forms를 처음 접하는 숙련 된 개발자.</span><span class="sxs-lookup"><span data-stu-id="c1993-126">The intended audience of this tutorial series is experienced developers who are new to ASP.NET Web Forms.</span></span> <span data-ttu-id="c1993-127">이 자습서 시리즈의 관심 있는 개발자는 다음과 같은 기술 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-127">A developer interested in this tutorial series should have the following skills:</span></span>

- <span data-ttu-id="c1993-128">친숙 한 개체 지향 프로그래밍 (OOP) 언어</span><span class="sxs-lookup"><span data-stu-id="c1993-128">Familiar with an object oriented programming (OOP) language</span></span>
- <span data-ttu-id="c1993-129">익숙한 웹 개발 개념 (HTML, CSS, JavaScript)</span><span class="sxs-lookup"><span data-stu-id="c1993-129">Familiar with Web development concepts (HTML, CSS, JavaScript)</span></span>
- <span data-ttu-id="c1993-130">관계형 데이터베이스 개념을 이해</span><span class="sxs-lookup"><span data-stu-id="c1993-130">Familiar with relational database concepts</span></span>
- <span data-ttu-id="c1993-131">N 계층 아키텍처 개념을 이해</span><span class="sxs-lookup"><span data-stu-id="c1993-131">Familiar with n-tier architecture concepts</span></span>

<span data-ttu-id="c1993-132">위에 나열 된 영역을 검토 하려는 경우 다음 콘텐츠를 검토 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-132">If you are interested in reviewing the areas listed above, consider reviewing the following content:</span></span>

- [<span data-ttu-id="c1993-133">Visual C# 시작</span><span class="sxs-lookup"><span data-stu-id="c1993-133">Getting Started with Visual C#</span></span>](https://msdn.microsoft.com/library/a72418yk.aspx)
- <span data-ttu-id="c1993-134">[웹 개발](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, PHP, JQuery](http://w3schools.com/)</span><span class="sxs-lookup"><span data-stu-id="c1993-134">[Web Development](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, PHP, JQuery](http://w3schools.com/)</span></span>
- [<span data-ttu-id="c1993-135">관계형 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="c1993-135">Relational database</span></span>](http://en.wikipedia.org/wiki/Relational_database)
- [<span data-ttu-id="c1993-136">다중 계층 아키텍처</span><span class="sxs-lookup"><span data-stu-id="c1993-136">Multitier architecture</span></span>](http://en.wikipedia.org/wiki/Multitier_architecture)

### <a name="application-features"></a><span data-ttu-id="c1993-137">응용 프로그램 기능</span><span class="sxs-lookup"><span data-stu-id="c1993-137">Application Features</span></span>

<span data-ttu-id="c1993-138">이 시리즈에 ASP.NET Web Form 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-138">The ASP.NET Web Form features presented in this series include:</span></span>

- <span data-ttu-id="c1993-139">웹 응용 프로그램 프로젝트 (웹 사이트 프로젝트가 아닌)</span><span class="sxs-lookup"><span data-stu-id="c1993-139">The Web Application Project (not Web Site Project)</span></span>
- <span data-ttu-id="c1993-140">Web Forms</span><span class="sxs-lookup"><span data-stu-id="c1993-140">Web Forms</span></span>
- <span data-ttu-id="c1993-141">마스터 페이지, 구성</span><span class="sxs-lookup"><span data-stu-id="c1993-141">Master Pages, Configuration</span></span>
- <span data-ttu-id="c1993-142">부트스트랩</span><span class="sxs-lookup"><span data-stu-id="c1993-142">Bootstrap</span></span>
- <span data-ttu-id="c1993-143">Entity Framework Code First,를 LocalDB</span><span class="sxs-lookup"><span data-stu-id="c1993-143">Entity Framework Code First, LocalDB</span></span>
- <span data-ttu-id="c1993-144">요청 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="c1993-144">Request Validation</span></span>
- <span data-ttu-id="c1993-145">강력한 형식의 데이터 컨트롤 바인딩, 데이터 주석 모델 및 공급자 값</span><span class="sxs-lookup"><span data-stu-id="c1993-145">Strongly Typed Data Controls, Model Binding, Data Annotations, and Value Providers</span></span>
- <span data-ttu-id="c1993-146">OAuth 및 SSL</span><span class="sxs-lookup"><span data-stu-id="c1993-146">SSL and OAuth</span></span>
- <span data-ttu-id="c1993-147">ASP.NET Id, 구성 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="c1993-147">ASP.NET Identity, Configuration, and Authorization</span></span>
- <span data-ttu-id="c1993-148">비 가시적인 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="c1993-148">Unobtrusive Validation</span></span>
- <span data-ttu-id="c1993-149">라우팅</span><span class="sxs-lookup"><span data-stu-id="c1993-149">Routing</span></span>
- <span data-ttu-id="c1993-150">ASP.NET 오류 처리</span><span class="sxs-lookup"><span data-stu-id="c1993-150">ASP.NET Error Handling</span></span>

### <a name="application-scenarios-and-tasks"></a><span data-ttu-id="c1993-151">응용 프로그램 시나리오 및 작업</span><span class="sxs-lookup"><span data-stu-id="c1993-151">Application Scenarios and Tasks</span></span>

<span data-ttu-id="c1993-152">이 시리즈에 설명 된 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-152">Tasks demonstrated in this series include:</span></span>

- <span data-ttu-id="c1993-153">새 프로젝트를 실행 하 고 생성, 검토</span><span class="sxs-lookup"><span data-stu-id="c1993-153">Creating, reviewing and running the new project</span></span>
- <span data-ttu-id="c1993-154">데이터베이스 구조 만들기</span><span class="sxs-lookup"><span data-stu-id="c1993-154">Creating the database structure</span></span>
- <span data-ttu-id="c1993-155">초기화 하 고 데이터베이스 시드</span><span class="sxs-lookup"><span data-stu-id="c1993-155">Initializing and seeding the database</span></span>
- <span data-ttu-id="c1993-156">스타일, 그래픽 및 마스터 페이지를 사용 하 여 UI를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="c1993-156">Customizing the UI using styles, graphics and a master page</span></span>
- <span data-ttu-id="c1993-157">페이지 및 탐색 추가</span><span class="sxs-lookup"><span data-stu-id="c1993-157">Adding pages and navigation</span></span>
- <span data-ttu-id="c1993-158">메뉴 세부 정보 및 제품 데이터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-158">Displaying menu details and product data</span></span>
- <span data-ttu-id="c1993-159">쇼핑 카트 만들기</span><span class="sxs-lookup"><span data-stu-id="c1993-159">Creating a shopping cart</span></span>
- <span data-ttu-id="c1993-160">추가 SSL 및 OAuth 지원</span><span class="sxs-lookup"><span data-stu-id="c1993-160">Adding SSL and OAuth support</span></span>
- <span data-ttu-id="c1993-161">결제 방법을 추가</span><span class="sxs-lookup"><span data-stu-id="c1993-161">Adding a payment method</span></span>
- <span data-ttu-id="c1993-162">관리자 역할 및 응용 프로그램에 사용자를 포함 하 여</span><span class="sxs-lookup"><span data-stu-id="c1993-162">Including an administrator role and a user to the application</span></span>
- <span data-ttu-id="c1993-163">특정 페이지와 폴더에 대 한 액세스 제한</span><span class="sxs-lookup"><span data-stu-id="c1993-163">Restricting access to specific pages and folder</span></span>
- <span data-ttu-id="c1993-164">웹 응용 프로그램에 파일을 업로드 하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-164">Uploading a file to the web application</span></span>
- <span data-ttu-id="c1993-165">입력된 유효성 검사를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-165">Implementing input validation</span></span>
- <span data-ttu-id="c1993-166">웹 응용 프로그램에 대 한 경로 등록 하는 중</span><span class="sxs-lookup"><span data-stu-id="c1993-166">Registering routes for the web application</span></span>
- <span data-ttu-id="c1993-167">오류 처리 및 오류 로깅 구현</span><span class="sxs-lookup"><span data-stu-id="c1993-167">Implementing error handling and error logging</span></span>

## <a name="overview"></a><span data-ttu-id="c1993-168">개요</span><span class="sxs-lookup"><span data-stu-id="c1993-168">Overview</span></span>

<span data-ttu-id="c1993-169">ASP.NET Web Forms을 처음 접하는 경우 있지만 프로그래밍 개념에 익숙한 저마다를 오른쪽 자습서를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-169">If you are new to ASP.NET Web Forms but have familiarity with programming concepts, you have the right tutorial.</span></span> <span data-ttu-id="c1993-170">ASP.NET Web Forms에 익숙한 경우 ASP.NET 4.5의 새로운 기능으로이 자습서 시리즈에서 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-170">If you are already familiar with ASP.NET Web Forms, you can benefit from this tutorial series by the new features available in ASP.NET 4.5.</span></span> <span data-ttu-id="c1993-171">프로그래밍 개념 및 ASP.NET Web Forms에 익숙한 경우 참조는 Web Forms에 제공 된 추가 자습서 [시작](../../../index.md) ASP.NET 웹 사이트에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="c1993-171">If you are unfamiliar with programming concepts and ASP.NET Web Forms, see the additional tutorials provided in the Web Forms [Getting Started](../../../index.md) section on the ASP.NET Web site.</span></span>

<span data-ttu-id="c1993-172">특정 **최신** 자습서 시리즈가 Web Forms에는 다음이 포함 된 ASP.NET 4.5 기능:</span><span class="sxs-lookup"><span data-stu-id="c1993-172">The specific **latest** ASP.NET 4.5 features provided in this Web Forms tutorial series include the following:</span></span>

- <span data-ttu-id="c1993-173">간단한 UI를 만들기 위한 프로젝트 해당 제품 [여러 ASP.NET 프레임 워크에 대 한 지원](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) (Web Forms, MVC 및 Web API).</span><span class="sxs-lookup"><span data-stu-id="c1993-173">A simple UI for creating projects that offer [support for multiple ASP.NET frameworks](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) (Web Forms, MVC, and Web API).</span></span>
- <span data-ttu-id="c1993-174">[부트스트랩](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), 반응 형 디자인 및 테마 설정 기능을 제공 하는 레이아웃 및 테마 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-174">[Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), a layout and theming framework that provides responsive design and theming capabilities.</span></span>
- <span data-ttu-id="c1993-175">[ASP.NET Identity](../../../../identity/index.md)를 웹 호스팅 IIS가 아닌 다른 소프트웨어와 모든 ASP.NET 프레임 워크와 작동에 동일 하 게 작동 하는 새로운 ASP.NET 멤버 자격 시스템.</span><span class="sxs-lookup"><span data-stu-id="c1993-175">[ASP.NET Identity](../../../../identity/index.md), a new ASP.NET membership system that works the same in all ASP.NET frameworks and works with web hosting software other than IIS.</span></span>
- <span data-ttu-id="c1993-176">[Entity Framework 6](https://msdn.microsoft.com/data/ef.aspx)형식의 개체를 검색 하 고 강력 하 게 데이터를 조작할 수 있는 Entity Framework에 대 한 업데이트, 비동기적으로 일시적인 연결 오류 처리 및 SQL 문을 로그 데이터에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-176">[Entity Framework 6](https://msdn.microsoft.com/data/ef.aspx), an update to the Entity Framework which allows you retrieve and manipulate data as strongly typed objects, access data asynchronously, handle transient connection faults, and log SQL statements.</span></span>

<span data-ttu-id="c1993-177">ASP.NET 4.5 기능의 전체 목록은 참조 하십시오. [ASP.NET 및 Web Tools for Visual Studio 2013 릴리스 정보](../../../../visual-studio/overview/2013/release-notes.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-177">For a complete list of ASP.NET 4.5 features, see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](../../../../visual-studio/overview/2013/release-notes.md).</span></span>

### <a name="the-wingtip-toys-sample-application"></a><span data-ttu-id="c1993-178">Wingtip Toys 샘플 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="c1993-178">The Wingtip Toys Sample Application</span></span>

<span data-ttu-id="c1993-179">다음 스크린샷은이 자습서 시리즈의 만들 ASP.NET Web forms 응용 프로그램의 빠른 보기를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-179">The following screen shots provide a quick view of the ASP.NET Web forms application that you will create in this tutorial series.</span></span> <span data-ttu-id="c1993-180">Visual Studio Express 2013 for Web에서에서 응용 프로그램을 실행 하는 경우 다음 웹 홈 페이지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-180">When you run the application from Visual Studio Express 2013 for Web, you will see the following web Home page.</span></span>

![기본 페이지-: wingtip Toys](introduction-and-overview/_static/image1.png)

<span data-ttu-id="c1993-182">새 사용자로 등록 하거나 기존 사용자로 로그인 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-182">You can register as a new user, or log in as an existing user.</span></span> <span data-ttu-id="c1993-183">탐색은 데이터베이스에서 사용할 수 있는 제품을 검색 하 여 각 제품 범주에 대 한 최상위에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-183">Navigation is provided at the top for each product category by retrieving the available products from the database.</span></span>

<span data-ttu-id="c1993-184">제품 링크를 선택 하면 모든 사용 가능한 제품의 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-184">By selecting the Products link, you will be able to see a list of all available products.</span></span>

![Wingtip Toys-제품](introduction-and-overview/_static/image2.png)

<span data-ttu-id="c1993-186">또한 나열 된 제품 중 하나를 선택 하 여 개별 제품 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-186">You can also see individual product details by selecting any of the listed products.</span></span>

![Wingtip Toys-제품 세부 정보](introduction-and-overview/_static/image3.png)

<span data-ttu-id="c1993-188">사용자로 등록 한 Web Forms 서식 파일의 기본 기능을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-188">As a user, you can register and log in using the default functionality of the Web Forms template.</span></span> <span data-ttu-id="c1993-189">이 자습서에는 기존 Gmail 계정을 사용 하 여 로그인 하는 방법도 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-189">This tutorial also explains how to login using an existing Gmail account.</span></span> <span data-ttu-id="c1993-190">또한 추가 하 고 데이터베이스에서 제품을 제거 하려면 관리자 권한으로 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-190">Additionally, you can login as the administrator to add and remove products from the database.</span></span>

![Wingtip Toys-로그인](introduction-and-overview/_static/image4.png)

<span data-ttu-id="c1993-192">사용자로 로그인 하면 PayPal으로 체크 아웃을 쇼핑 카트에 제품을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-192">Once you have logged in as a user, you can add products to the shopping cart and checkout with PayPal.</span></span> <span data-ttu-id="c1993-193">이 샘플 응용 프로그램 PayPal의 개발자 샌드박스 에서만 작동 하도록 되어 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-193">Note that this sample application is designed to function with PayPal's developer sandbox.</span></span> <span data-ttu-id="c1993-194">실제 금액 트랜잭션이 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-194">No actual money transaction will take place.</span></span>

![쇼핑 카트: wingtip Toys-](introduction-and-overview/_static/image5.png)

<span data-ttu-id="c1993-196">PayPal는 계정, 순서 및 지불 정보를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-196">PayPal will confirm your account, order, and payment information.</span></span>

![Wingtip Toys-PayPal](introduction-and-overview/_static/image6.png)

<span data-ttu-id="c1993-198">PayPal을 통한 반환한 검토 하 고 주문을 완료 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-198">After returning from PayPal, you can review and complete your order.</span></span>

![Wingtip Toys-순서 검토](introduction-and-overview/_static/image7.png)

## <a name="prerequisites"></a><span data-ttu-id="c1993-200">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="c1993-200">Prerequisites</span></span>

<span data-ttu-id="c1993-201">시작 하기 전에 다음 소프트웨어가 컴퓨터에 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-201">Before you start, make sure that you have the following software installed on your computer:</span></span>

- <span data-ttu-id="c1993-202">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/en-us/downloads#vs) 또는 [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/en-us/downloads#express-web)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-202">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/en-us/downloads#vs) or [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/en-us/downloads#express-web).</span></span> <span data-ttu-id="c1993-203">.NET Framework는 자동으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-203">The .NET Framework is installed automatically.</span></span>

<span data-ttu-id="c1993-204">이 자습서 시리즈 웹에 대 한 Microsoft Visual Studio Express 2013을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-204">This tutorial series uses Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="c1993-205">이 자습서 시리즈를 완료 하려면 Microsoft Visual Studio Express 2013 for Web 또는 Microsoft Visual Studio 2013을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-205">You can use either Microsoft Visual Studio Express 2013 for Web or Microsoft Visual Studio 2013 to complete this tutorial series.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="c1993-206">Microsoft Visual Studio 2013 및 Microsoft Visual Studio Express 2013 for Web은 종종로 간주 Visual Studio이 자습서 시리즈 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-206">Microsoft Visual Studio 2013 and Microsoft Visual Studio Express 2013 for Web will often be referred to as Visual Studio throughout this tutorial series.</span></span>


<span data-ttu-id="c1993-207">이미 Visual Studio 버전이 설치 되어 있으면 설치 프로세스는 기존 버전 옆에 있는 Visual Studio 2013 또는 Microsoft Visual Studio Express 2013 for Web 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-207">If you already have a Visual Studio version installed, the installation process will install Visual Studio 2013 or Microsoft Visual Studio Express 2013 for Web next to the existing version.</span></span> <span data-ttu-id="c1993-208">이전 버전에서 만든 사이트 Visual Studio 2013에서 열 수 및 이전 버전에서 열을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-208">Sites that you created in earlier versions can be opened in Visual Studio 2013 and continue to open in previous versions.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="c1993-209">이 연습에서는 선택 했다고 가정은 *웹 개발* 설정의 컬렉션 서 처음으로 Visual Studio를 시작 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-209">This walkthrough assumes that you selected the *Web Development* collection of settings the first time that you started Visual Studio.</span></span> <span data-ttu-id="c1993-210">자세한 내용은 참조 [하는 방법: 웹 개발 환경 설정 선택](https://msdn.microsoft.com/en-us/library/ff521558.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-210">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/en-us/library/ff521558.aspx).</span></span>


## <a name="download-the-sample-application"></a><span data-ttu-id="c1993-211">샘플 응용 프로그램 다운로드</span><span class="sxs-lookup"><span data-stu-id="c1993-211">Download the Sample Application</span></span>

<span data-ttu-id="c1993-212">필수 구성 요소를 설치한 후 했으면 이제이 자습서 시리즈에 제공 되는 새 웹 프로젝트 만들기를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-212">After installing the prerequisites, you are ready to begin creating the new Web project that is presented in this tutorial series.</span></span> <span data-ttu-id="c1993-213">원하는 경우 **필요에 따라** 이 자습서 시리즈 만듭니다 샘플 응용 프로그램을 실행 하면에서 다운로드할 수 MSDN 샘플 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-213">If you would like to **optionally** run the sample application that this tutorial series creates, you can download it from the MSDN Samples site.</span></span> <span data-ttu-id="c1993-214">이 다운로드에는 다음이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-214">This download contains the following:</span></span>

- <span data-ttu-id="c1993-215">예제 응용 프로그램에는 *WingtipToys* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-215">The sample application in the *WingtipToys* folder.</span></span>
- <span data-ttu-id="c1993-216">샘플 응용 프로그램을 만드는 사용 되는 리소스는 *WingtipToys 자산* 폴더에는 *WingtipToys* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-216">The resources used to create the sample application in the *WingtipToys-Assets* folder in the *WingtipToys* folder.</span></span>

#### <a name="download-the-file-from-msdn-samples-site"></a><span data-ttu-id="c1993-217">MSDN 샘플 사이트에서 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-217">Download the file from MSDN Samples site:</span></span>

<span data-ttu-id="c1993-218">[ASP.NET 4.5 Web Forms 및 Visual Studio 2013-Wingtip Toys 시작](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span><span class="sxs-lookup"><span data-stu-id="c1993-218">[Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span></span> 

<span data-ttu-id="c1993-219">다운로드 되는 *.zip* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-219">The download is a *.zip* file.</span></span> <span data-ttu-id="c1993-220">이 자습서 시리즈 만듭니다 완료 된 프로젝트, 찾기 및 선택은 *C#*폴더에는 *.zip* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-220">To see the completed project that this tutorial series creates, find and select the *C#*folder in the *.zip* file.</span></span> <span data-ttu-id="c1993-221">저장 된 *C#* folderto Visual Studio 2013 프로젝트 작업에 사용할 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-221">Save the *C#* folderto the folder you use to work with Visual Studio 2013 projects.</span></span> <span data-ttu-id="c1993-222">기본적으로 Visual Studio 2013 프로젝트 폴더는 다음입니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-222">By default, the Visual Studio 2013 projects folder is the following:</span></span>

<span data-ttu-id="c1993-223">**C:\Users\*****&lt;username&gt;* * * \Documents\Visual Studio 2013\Projects**</span><span class="sxs-lookup"><span data-stu-id="c1993-223">**C:\Users\*****&lt;username&gt;*****\Documents\Visual Studio 2013\Projects**</span></span>

<span data-ttu-id="c1993-224">이름 바꾸기는 ***C#*** 폴더를 ***WingtipToys***합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-224">Rename the ***C#*** folder to ***WingtipToys***.</span></span>

> [!NOTE]
> <span data-ttu-id="c1993-225">라는 폴더가 이미 있는 경우 *WingtipToys* 프로젝트 폴더의 이름을 임시로 바꾸거나 기존 폴더 이름을 바꾸기 전에 *C#* 폴더를 *WingtipToys*합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-225">If you already have a folder named *WingtipToys* in your Projects folder, temporarily rename that existing folder before renaming the *C#* folder to *WingtipToys*.</span></span>


<span data-ttu-id="c1993-226">완료 된 프로젝트를 실행 하려면 열고는 *WingtipToys* 폴더를 두 번 클릭은 *WingtipToys.sln* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-226">To run the completed project, open the *WingtipToys* folder and double-click the *WingtipToys.sln* file.</span></span> <span data-ttu-id="c1993-227">Visual Studio 2013 프로젝트를 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-227">Visual Studio 2013 will open the project.</span></span> <span data-ttu-id="c1993-228">그런 다음 마우스 오른쪽 단추로 클릭는 *Default.aspx* 솔루션 탐색기 창에서 파일을 브라우저에서 보기의 오른쪽 클릭 메뉴에서를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-228">Next, right-click the *Default.aspx* file in the Solution Explorer window and click View In Browser from the right-click menu.</span></span>

### <a name="tutorial-support-and-comments"></a><span data-ttu-id="c1993-229">자습서 지원 및 주석</span><span class="sxs-lookup"><span data-stu-id="c1993-229">Tutorial Support and Comments</span></span>

<span data-ttu-id="c1993-230">에 포함 된 Q &AMP; A 섹션을 사용 하는 [ASP.NET 4.5 Web Forms 및 Visual Studio 2013-Wingtip Toys 시작](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 한 질문이 나 의견에 대 한 샘플 (C#).</span><span class="sxs-lookup"><span data-stu-id="c1993-230">Use the Q AND A section included with the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample for any questions or comments.</span></span>

<span data-ttu-id="c1993-231">이 자습서 시리즈에 대 한 의견을 기다리겠습니다, 하 고이 자습서 시리즈 업데이트 될 때 모든 노력 됩니다 계정 수정 또는 제안이 자습서 주석에서 제공 되는 향상 된 기능에 대 한 고려 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-231">Comments on this tutorial series are welcome, and when this tutorial series is updated every effort will be made to take into account corrections or suggestions for improvements that are provided in the tutorial comments.</span></span>

<span data-ttu-id="c1993-232">개발 하는 동안 오류가 발생 하거나 웹 사이트가 올바르게 실행 되지 않은 경우 오류 메시지가 문제의 소스에 복잡 한 단서를 제공할 수 있습니다 또는 해결 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-232">When an error happens during development, or if the Web site does not run correctly, the error messages may give complex clues to the source of the problem or might not explain how to fix it.</span></span> <span data-ttu-id="c1993-233">몇 가지 일반적인 문제 시나리오 연결해보세요를 사용할 수도 있습니다는 [ASP.NET 포럼](https://forums.asp.net/) 또는에 포함 된 Q &AMP; A 섹션의 [ASP.NET 4.5 Web Forms 및 Visual Studio 2013-Wingtip Toys 시작](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 드 ( C#) 샘플.</span><span class="sxs-lookup"><span data-stu-id="c1993-233">To help you with some common problem scenarios, you can also use the [ASP.NET forums](https://forums.asp.net/) or the Q AND A section included with the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample.</span></span> <span data-ttu-id="c1993-234">오류 메시지가 자습서를 진행할 때 작동 하지 않는 경우에 위의 위치를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1993-234">If you get an error message or something doesn't work as you go through the tutorials, be sure to check the above locations.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="c1993-235">다음</span><span class="sxs-lookup"><span data-stu-id="c1993-235">Next</span></span>](create-the-project.md)
