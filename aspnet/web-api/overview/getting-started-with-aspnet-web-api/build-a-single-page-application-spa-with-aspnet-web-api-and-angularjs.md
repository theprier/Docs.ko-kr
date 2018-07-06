---
uid: web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
title: '실습: ASP.NET Web API 및 Angular.js를 사용 하 여 단일 페이지 응용 프로그램 (SPA) 빌드 | Microsoft Docs'
author: rick-anderson
description: 기존 웹 응용 프로그램에서 클라이언트 (브라우저) 페이지를 요청 하 여 서버와의 통신을 시작 합니다. 서버는 다음 요청을 처리 하는 중...
ms.author: aspnetcontent
ms.date: 09/30/2015
ms.assetid: 719727b7-bef3-45ad-bfe9-ba5bcdb2305f
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
msc.type: authoredcontent
ms.openlocfilehash: 8e9cc082d982aec0a4385a3cefecd118c937e641
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37811522"
---
<a name="hands-on-lab-build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs"></a><span data-ttu-id="34394-104">실습: ASP.NET Web API 및 Angular.js를 사용 하 여 단일 페이지 응용 프로그램 (SPA) 빌드</span><span class="sxs-lookup"><span data-stu-id="34394-104">Hands On Lab: Build a Single Page Application (SPA) with ASP.NET Web API and Angular.js</span></span>
====================
<span data-ttu-id="34394-105">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="34394-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="34394-106">웹 캠프 학습 키트 다운로드</span><span class="sxs-lookup"><span data-stu-id="34394-106">Download Web Camps Training Kit</span></span>](http://aka.ms/webcamps-training-kit)

> <span data-ttu-id="34394-107">기존 웹 응용 프로그램에서 클라이언트 (브라우저) 페이지를 요청 하 여 서버와의 통신을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-107">In traditional web applications, the client (browser) initiates the communication with the server by requesting a page.</span></span> <span data-ttu-id="34394-108">그런 다음 서버는 요청을 처리 하 고 페이지의 HTML 클라이언트에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="34394-108">The server then processes the request and sends the HTML of the page to the client.</span></span> <span data-ttu-id="34394-109">– 예를 들어 사용자 링크에 이동 하거나 데이터를 사용 하 여 폼을 전송 – 페이지를 사용 하 여 후속 상호 작용에서 새 요청을 서버로 전송 되 고 흐름이 다시 시작: 서버가 요청을 처리 하 고 새 작업 요청에 대 한 응답으로 브라우저에 새 페이지를 보냅니다 클라이언트에서 ed 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-109">In subsequent interactions with the page –e.g. the user navigates to a link or submits a form with data– a new request is sent to the server, and the flow starts again: the server processes the request and sends a new page to the browser in response to the new action requested by the client.</span></span>
> 
> <span data-ttu-id="34394-110">단일 페이지 응용 프로그램 (Spa)에서 전체 페이지 로드 브라우저에서 초기 요청 후 되었지만 후속 상호 작용 Ajax 요청을 통해 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-110">In Single-Page Applications (SPAs) the entire page is loaded in the browser after the initial request, but subsequent interactions take place through Ajax requests.</span></span> <span data-ttu-id="34394-111">즉, 브라우저가 변경 되었으면 하는 페이지의 부분만 업데이트 해야 합니다. 전체 페이지를 로드할 필요가 없습니다 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34394-111">This means that the browser has to update only the portion of the page that has changed; there is no need to reload the entire page.</span></span> <span data-ttu-id="34394-112">SPA 접근 방식은 유연한 환경을 사용자 동작에 응답 하도록 응용 프로그램에서 소요 된 시간을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-112">The SPA approach reduces the time taken by the application to respond to user actions, resulting in a more fluid experience.</span></span>
> 
> <span data-ttu-id="34394-113">SPA의 아키텍처는 기존 웹 응용 프로그램에 존재 하지 않는 몇 가지 문제에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34394-113">The architecture of a SPA involves certain challenges that are not present in traditional web applications.</span></span> <span data-ttu-id="34394-114">그러나 ASP.NET Web API와 같은 신기술을 JavaScript 프레임 워크 AngularJS 등 CSS3에서 제공 하는 새 스타일 기능 쉽게 디자인 하 고 Spa를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-114">However, emerging technologies like ASP.NET Web API, JavaScript frameworks like AngularJS and new styling features provided by CSS3 make it really easy to design and build SPAs.</span></span>
> 
> <span data-ttu-id="34394-115">이 실습 랩에서 Geek 퀴즈, SPA 개념을 기반으로 하는 기타 정보 웹 사이트를 구현 하는 이러한 기술 활용을 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="34394-115">In this hand-on lab, you will take advantage of those technologies to implement Geek Quiz, a trivia website based on the SPA concept.</span></span> <span data-ttu-id="34394-116">먼저 퀴즈 질문을 검색 하 고 답변을 저장할 필요한 끝점을 노출할 ASP.NET Web API를 사용 하 여 서비스 계층을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-116">You will first implement the service layer with ASP.NET Web API to expose the required endpoints to retrieve the quiz questions and store the answers.</span></span> <span data-ttu-id="34394-117">그런 다음, AngularJS 및 CSS3 변환 효과 사용 하 여 풍부 하 고 응답성이 뛰어난 UI를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34394-117">Then, you will build a rich and responsive UI using AngularJS and CSS3 transformation effects.</span></span>
> 
> <span data-ttu-id="34394-118">웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 됩니다 [ http://aka.ms/webcamps-training-kit ](http://aka.ms/webcamps-training-kit)합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-118">All sample code and snippets are included in the Web Camps Training Kit, available at [http://aka.ms/webcamps-training-kit](http://aka.ms/webcamps-training-kit).</span></span>


## <a name="overview"></a><span data-ttu-id="34394-119">개요</span><span class="sxs-lookup"><span data-stu-id="34394-119">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="34394-120">목표</span><span class="sxs-lookup"><span data-stu-id="34394-120">Objectives</span></span>

<span data-ttu-id="34394-121">이 실습 랩에서 학습할 방법:</span><span class="sxs-lookup"><span data-stu-id="34394-121">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="34394-122">JSON 데이터를 수신 하는 ASP.NET Web API 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="34394-122">Create an ASP.NET Web API service to send and receive JSON data</span></span>
- <span data-ttu-id="34394-123">AngularJS를 사용 하 여 반응 형 UI 만들기</span><span class="sxs-lookup"><span data-stu-id="34394-123">Create a responsive UI using AngularJS</span></span>
- <span data-ttu-id="34394-124">CSS3 변환 사용 하 여 UI 환경을 향상합니다</span><span class="sxs-lookup"><span data-stu-id="34394-124">Enhance the UI experience with CSS3 transformations</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="34394-125">전제 조건</span><span class="sxs-lookup"><span data-stu-id="34394-125">Prerequisites</span></span>

<span data-ttu-id="34394-126">다음는이 실습을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-126">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="34394-127">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) 이상</span><span class="sxs-lookup"><span data-stu-id="34394-127">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="34394-128">설정</span><span class="sxs-lookup"><span data-stu-id="34394-128">Setup</span></span>

<span data-ttu-id="34394-129">이 실습에서는 연습을 실행 하려면 먼저 환경 설정을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-129">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="34394-130">Windows 탐색기를 열고 실습용 **원본** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-130">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="34394-131">마우스 오른쪽 단추로 클릭 **Setup.cmd** 선택한 **관리자 권한으로 실행** 환경을 구성 하 고이 랩에 대 한 Visual Studio 코드 조각을 설치는 설치 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-131">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="34394-132">사용자 계정 컨트롤 대화 상자를 표시 하는 경우 계속 하려면 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-132">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="34394-133">설치 프로그램을 실행 하기 전에이 랩에 대 한 모든 종속성을 선택 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-133">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="34394-134">코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="34394-134">Using the Code Snippets</span></span>

<span data-ttu-id="34394-135">랩 문서 전체에서 코드 블록을 삽입할 지시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34394-135">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="34394-136">사용자 편의 위해이 코드의 대부분은 수동으로 추가할 필요가 없도록 하려면 Visual Studio 2013 내에서 액세스할 수 있는 Visual Studio 코드 조각으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34394-136">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="34394-137">각 실습에 시작 솔루션을 함께 표시 됩니다는 **시작** 다른 독립적으로 각 연습에 따라 할 수 있는 연습 하는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-137">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="34394-138">주의 하십시오 연습 하는 동안 추가 되는 코드 조각은 솔루션부터 이러한 누락 되어 연습을 완료 될 때까지 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34394-138">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="34394-139">연습에 대 한 소스 코드 안에 있습니다.는 **최종** 해당 연습에서 단계를 완료 합니다. 결과로 생성 되는 코드를 사용 하 여 Visual Studio 솔루션에 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-139">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="34394-140">이 실습을 통해 작업 하는 동안 추가 도움이 필요한 경우 지침으로 이러한 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34394-140">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>


* * *

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="34394-141">연습</span><span class="sxs-lookup"><span data-stu-id="34394-141">Exercises</span></span>

<span data-ttu-id="34394-142">이 실습 랩에서 다음 연습에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34394-142">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="34394-143">Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="34394-143">Creating a Web API</span></span>](#Exercise1)
2. [<span data-ttu-id="34394-144">SPA 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="34394-144">Creating a SPA Interface</span></span>](#Exercise2)

<span data-ttu-id="34394-145">이 랩을 완료 하기 위한 예상 시간: **60 분**</span><span class="sxs-lookup"><span data-stu-id="34394-145">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="34394-146">Visual Studio를 처음 시작 하면 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-146">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="34394-147">미리 정의 된 각 컬렉션에는 특정 개발 스타일에 맞게 설계 되었습니다 및 창 레이아웃, 동작 편집기, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-147">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="34394-148">이 랩의 절차에서는 사용 하는 경우 Visual Studio에서 지정된 된 태스크를 수행 하는 데 필요한 작업을 설명 합니다 **일반 개발 설정** 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-148">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="34394-149">개발 환경에 대 한 다양 한 설정 컬렉션을 선택 하는 경우를 고려해 야 하는 단계에 차이가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34394-149">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>


<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-web-api"></a><span data-ttu-id="34394-150">연습 1: Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="34394-150">Exercise 1: Creating a Web API</span></span>

<span data-ttu-id="34394-151">SPA의 주요 부분 중 하나는 서비스 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-151">One of the key parts of a SPA is the service layer.</span></span> <span data-ttu-id="34394-152">이 UI와 해당 호출에 응답 반환 데이터를 보낸 Ajax 호출을 처리 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-152">It is responsible for processing the Ajax calls sent by the UI and returning data in response to that call.</span></span> <span data-ttu-id="34394-153">검색 데이터를 구문 분석 하 고 클라이언트에서 사용 하기 위해 컴퓨터가 읽을 수 있는 형식으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-153">The data retrieved should be presented in a machine-readable format in order to be parsed and consumed by the client.</span></span>

<span data-ttu-id="34394-154">Web API 프레임 워크 ASP.NET 스택에의 일부 이며는 쉽게 일반적으로 데이터 보내기 및 받기 JSON 또는 XML 형식 RESTful API를 통해 HTTP 서비스를 구현 하도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="34394-154">The Web API framework is part of the ASP.NET Stack and is designed to make it easy to implement HTTP services, generally sending and receiving JSON- or XML-formatted data through a RESTful API.</span></span> <span data-ttu-id="34394-155">이 연습에서 Geek 퀴즈 응용 프로그램을 호스트 하 고 다음 백 엔드 서비스를 노출 하 고 ASP.NET Web API를 사용 하 여 퀴즈 데이터 유지를 구현 하는 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="34394-155">In this exercise you will create the Web site to host the Geek Quiz application and then implement the back-end service to expose and persist the quiz data using ASP.NET Web API.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-the-initial-project-for-geek-quiz"></a><span data-ttu-id="34394-156">작업 1-Geek 퀴즈에 대 한 초기 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="34394-156">Task 1 – Creating the Initial Project for Geek Quiz</span></span>

<span data-ttu-id="34394-157">이 태스크에서는 먼저 기반으로 하는 ASP.NET Web API에 대 한 지원을 사용 하 여 새 ASP.NET MVC 프로젝트 만들기를 **One ASP.NET** 프로젝트 Visual Studio와 함께 제공 되는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-157">In this task you will start creating a new ASP.NET MVC project with support for ASP.NET Web API based on the **One ASP.NET** project type that comes with Visual Studio.</span></span> <span data-ttu-id="34394-158">**One ASP.NET** 를 모든 ASP.NET 기술을 통합 하 고 혼합 하 고 필요에 따라 일치 하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34394-158">**One ASP.NET** unifies all ASP.NET technologies and gives you the option to mix and match them as desired.</span></span> <span data-ttu-id="34394-159">다음 Entity Framework의 모델 클래스와 데이터베이스 initializator 퀴즈 질문에 삽입할 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-159">You will then add the Entity Framework's model classes and the database initializator to insert the quiz questions.</span></span>

1. <span data-ttu-id="34394-160">오픈 **Visual Studio Express 2013 for Web** 선택한 **파일 | 새 프로젝트...**  새 솔루션을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-160">Open **Visual Studio Express 2013 for Web** and select **File | New Project...** to start a new solution.</span></span>

    <span data-ttu-id="34394-161">![새 프로젝트를 만드는](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "새 프로젝트 만들기")</span><span class="sxs-lookup"><span data-stu-id="34394-161">![Creating a New Project](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "Creating a New Project")</span></span>

    <span data-ttu-id="34394-162">*새 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="34394-162">*Creating a New Project*</span></span>
2. <span data-ttu-id="34394-163">에 **새 프로젝트** 대화 상자에서 **ASP.NET 웹 응용 프로그램** 아래에서 **Visual C# | 웹** 탭 합니다. 있는지 **.NET Framework 4.5** 는 이름을 선택 *GeekQuiz*, 선택는 **위치** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-163">In the **New Project** dialog box, select **ASP.NET Web Application** under the **Visual C# | Web** tab. Make sure **.NET Framework 4.5** is selected, name it *GeekQuiz*, choose a **Location** and click **OK**.</span></span>

    <span data-ttu-id="34394-164">![새 ASP.NET 웹 응용 프로그램 프로젝트를 만드는](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "새 ASP.NET 웹 응용 프로그램 프로젝트 만들기")</span><span class="sxs-lookup"><span data-stu-id="34394-164">![Creating a new ASP.NET Web Application project](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "Creating a new ASP.NET Web Application project")</span></span>

    <span data-ttu-id="34394-165">*새 ASP.NET 웹 응용 프로그램 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="34394-165">*Creating a new ASP.NET Web Application project*</span></span>
3. <span data-ttu-id="34394-166">에 **새 ASP.NET 프로젝트** 대화 상자에서를 **MVC** 템플릿을 선택한 합니다 **Web API** 옵션.</span><span class="sxs-lookup"><span data-stu-id="34394-166">In the **New ASP.NET Project** dialog box, select the **MVC** template and select the **Web API** option.</span></span> <span data-ttu-id="34394-167">또한 있는지 확인 합니다 **인증** 옵션을 설정 **개별 사용자 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-167">Also, make sure that the **Authentication** option is set to **Individual User Accounts**.</span></span> <span data-ttu-id="34394-168">계속하려면 **확인** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-168">Click **OK** to continue.</span></span>

    ![Web API 구성 요소를 포함 하 여 MVC 템플릿을 사용 하 여 새 프로젝트 만들기](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image3.png)

    <span data-ttu-id="34394-170">*Web API 구성 요소를 포함 하 여 MVC 템플릿을 사용 하 여 새 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="34394-170">*Creating a new project with the MVC template, including Web API components*</span></span>
4. <span data-ttu-id="34394-171">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **모델** 폴더를 **GeekQuiz** 프로젝트를 마우스 **추가 | 기존 항목...** .</span><span class="sxs-lookup"><span data-stu-id="34394-171">In **Solution Explorer**, right-click the **Models** folder of the **GeekQuiz** project and select **Add | Existing Item...**.</span></span>

    <span data-ttu-id="34394-172">![기존 항목 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "기존 항목 추가")</span><span class="sxs-lookup"><span data-stu-id="34394-172">![Adding an existing item](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "Adding an existing item")</span></span>

    <span data-ttu-id="34394-173">*기존 항목 추가*</span><span class="sxs-lookup"><span data-stu-id="34394-173">*Adding an existing item*</span></span>
5. <span data-ttu-id="34394-174">에 **기존 항목 추가** 대화 상자에서 **소스/자산/모델** 폴더 및 파일을 모두 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-174">In the **Add Existing Item** dialog box, navigate to the **Source/Assets/Models** folder and select all the files.</span></span> <span data-ttu-id="34394-175">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-175">Click **Add**.</span></span>

    <span data-ttu-id="34394-176">![모델 자산 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "모델 자산 추가")</span><span class="sxs-lookup"><span data-stu-id="34394-176">![Adding the model assets](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "Adding the model assets")</span></span>

    <span data-ttu-id="34394-177">*모델 자산 추가*</span><span class="sxs-lookup"><span data-stu-id="34394-177">*Adding the model assets*</span></span>

    > [!NOTE]
    > <span data-ttu-id="34394-178">이러한 파일에 추가 하 여 데이터 모델, Entity Framework의 데이터베이스 컨텍스트 및 Geek 퀴즈 응용 프로그램에 대 한 데이터베이스 이니셜라이저 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34394-178">By adding these files, you are adding the data model, the Entity Framework's database context and the database initializer for the Geek Quiz application.</span></span>
    > 
    > <span data-ttu-id="34394-179">**Entity Framework (EF)** 는 관계형 저장소 스키마를 사용 하 여 직접 프로그래밍 하는 대신 개념적 응용 프로그램 모델을 사용 하 여 프로그래밍 하 여 데이터 액세스 응용 프로그램을 만들 수 있도록 개체 관계형 매퍼 (ORM).</span><span class="sxs-lookup"><span data-stu-id="34394-179">**Entity Framework (EF)** is an object-relational mapper (ORM) that enables you to create data access applications by programming with a conceptual application model instead of programming directly using a relational storage schema.</span></span> <span data-ttu-id="34394-180">Entity Framework에 대 한 자세히 알아볼 수 있습니다 [여기](../../../entity-framework.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-180">You can learn more about Entity Framework [here](../../../entity-framework.md).</span></span>
    > 
    > <span data-ttu-id="34394-181">다음은 방금 추가한 클래스의 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-181">The following is a description of the classes you just added:</span></span>
    > 
    > - <span data-ttu-id="34394-182">**TriviaOption:** 퀴즈 질문을 사용 하 여 연결 된 단일 옵션을 나타냅니다</span><span class="sxs-lookup"><span data-stu-id="34394-182">**TriviaOption:** represents a single option associated with a quiz question</span></span>
    > - <span data-ttu-id="34394-183">**: TriviaQuestion** 퀴즈 질문을 나타내며를 통해 연결된 옵션을 제공 합니다 **옵션** 속성</span><span class="sxs-lookup"><span data-stu-id="34394-183">**TriviaQuestion:** represents a quiz question and exposes the associated options through the **Options** property</span></span>
    > - <span data-ttu-id="34394-184">**TriviaAnswer:** 퀴즈 질문에 대 한 응답에서 사용자가 선택한 옵션을 나타냅니다</span><span class="sxs-lookup"><span data-stu-id="34394-184">**TriviaAnswer:** represents the option selected by the user in response to a quiz question</span></span>
    > - <span data-ttu-id="34394-185">**TriviaContext:** Geek 퀴즈 응용 프로그램의 Entity Framework의 데이터베이스 컨텍스트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="34394-185">**TriviaContext:** represents the Entity Framework's database context of the Geek Quiz application.</span></span> <span data-ttu-id="34394-186">이 클래스에서 파생 됩니다 **DContext** 노출 **DbSet** 위에 설명 된 엔터티의 컬렉션을 나타내는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-186">This class derives from **DContext** and exposes **DbSet** properties that represent collections of the entities described above.</span></span>
    > - <span data-ttu-id="34394-187">**TriviaDatabaseInitializer:** 에 대 한 Entity Framework 이니셜라이저 구현의 합니다 **TriviaContext** 클래스에서 상속 하는 **CreateDatabaseIfNotExists**합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-187">**TriviaDatabaseInitializer:** the implementation of the Entity Framework initializer for the **TriviaContext** class which inherits from **CreateDatabaseIfNotExists**.</span></span> <span data-ttu-id="34394-188">에 지정 된 엔터티를 삽입 합니다.이 클래스의 기본 동작은 존재 하지 않는 경우에 데이터베이스를 만들려고 합니다는 **시드** 메서드.</span><span class="sxs-lookup"><span data-stu-id="34394-188">The default behavior of this class is to create the database only if it does not exist, inserting the entities specified in the **Seed** method.</span></span>
6. <span data-ttu-id="34394-189">엽니다는 **Global.asax.cs** 파일을 추가한 다음 문을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-189">Open the **Global.asax.cs** file and add the following using statement.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample1.cs)]
7. <span data-ttu-id="34394-190">시작 부분에 다음 코드를 추가 합니다 **응용 프로그램\_시작** 설정 하는 방법의 **TriviaDatabaseInitializer** 데이터베이스 이니셜라이저를 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-190">Add the following code at the beginning of the **Application\_Start** method to set the **TriviaDatabaseInitializer** as the database initializer.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample2.cs)]
8. <span data-ttu-id="34394-191">수정 된 **홈** 인증 된 사용자에 대 한 액세스를 제한 하는 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-191">Modify the **Home** controller to restrict access to authenticated users.</span></span> <span data-ttu-id="34394-192">이 위해 엽니다는 **HomeController.cs** 파일을 **컨트롤러** 폴더 추가 **권한 부여** 특성을 **HomeController**클래스 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-192">To do this, open the **HomeController.cs** file inside the **Controllers** folder and add the **Authorize** attribute to the **HomeController** class definition.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample3.cs)]

    > [!NOTE]
    > <span data-ttu-id="34394-193">합니다 **권한 부여** 사용자가 인증 하는 경우 확인을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-193">The **Authorize** filter checks to see if the user is authenticated.</span></span> <span data-ttu-id="34394-194">사용자 인증 되지 않은 경우 다음 작업을 호출 하지 않고 HTTP 상태 코드 401 (권한 없음)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-194">If the user is not authenticated, it returns HTTP status code 401 (Unauthorized) without invoking the action.</span></span> <span data-ttu-id="34394-195">컨트롤러 수준에서 전역으로 또는 개별 작업 수준에서 필터를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34394-195">You can apply the filter globally, at the controller level, or at the level of individual actions.</span></span>
9. <span data-ttu-id="34394-196">이제 웹 페이지 및 브랜딩 레이아웃을 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-196">You will now customize the layout of the web pages and the branding.</span></span> <span data-ttu-id="34394-197">이 작업을 수행 하려면 엽니다는  **\_Layout.cshtml** 파일을 **뷰 | 공유** 폴더의 콘텐츠를 업데이트 합니다 **&lt;title&gt;** 대체 하 여 요소 *내 ASP.NET 응용 프로그램* 사용 하 여 *Geek 퀴즈* .</span><span class="sxs-lookup"><span data-stu-id="34394-197">To do this, open the **\_Layout.cshtml** file inside the **Views | Shared** folder and update the content of the **&lt;title&gt;** element by replacing *My ASP.NET Application* with *Geek Quiz*.</span></span>

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample4.cshtml)]
10. <span data-ttu-id="34394-198">동일한 파일에서 제거 하 여 탐색 모음을 업데이트 합니다 *에 대 한* 및 *연락처* 링크 및 이름 바꾸기는 *홈* 연결할 *재생*합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-198">In the same file, update the navigation bar by removing the *About* and *Contact* links and renaming the *Home* link to *Play*.</span></span> <span data-ttu-id="34394-199">또한 이름 바꾸기는 *응용 프로그램 이름* 연결할 *매니아 퀴즈*합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-199">Additionally, rename the *Application name* link to *Geek Quiz*.</span></span> <span data-ttu-id="34394-200">HTML 탐색 모음에 다음 코드와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="34394-200">The HTML for the navigation bar should look like the following code.</span></span>

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample5.cshtml)]
11. <span data-ttu-id="34394-201">대체 하 여 레이아웃 페이지의 바닥글 업데이트 *내 ASP.NET 응용 프로그램* 사용 하 여 *매니아 퀴즈*합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-201">Update the footer of the layout page by replacing *My ASP.NET Application* with *Geek Quiz*.</span></span> <span data-ttu-id="34394-202">이 위해의 콘텐츠를 대체 합니다 **&lt;바닥글&gt;** 요소를 다음 강조 표시 된 코드로.</span><span class="sxs-lookup"><span data-stu-id="34394-202">To do this, replace the content of the **&lt;footer&gt;** element with the following highlighted code.</span></span>

    [!code-html[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample6.html)]

<a id="Ex1Task2"></a>
#### <a name="task-2--creating-the-triviacontroller-web-api"></a><span data-ttu-id="34394-203">작업 2-TriviaController Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="34394-203">Task 2 – Creating the TriviaController Web API</span></span>

<span data-ttu-id="34394-204">이전 작업에서는 Geek 퀴즈 웹 응용 프로그램의 초기 구조를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="34394-204">In the previous task, you created the initial structure of the Geek Quiz web application.</span></span> <span data-ttu-id="34394-205">이제 퀴즈 데이터 모델과 상호 작용 하 고 다음 작업을 노출 하는 간단한 Web API 서비스를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-205">You will now build a simple Web API service that interacts with the quiz data model and exposes the following actions:</span></span>

- <span data-ttu-id="34394-206">**GET/api/퀴즈**: 인증 된 사용자가 대답할 수 퀴즈 목록에서 다음 질문을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-206">**GET /api/trivia**: Retrieves the next question from the quiz list to be answered by the authenticated user.</span></span>
- <span data-ttu-id="34394-207">**POST/api/퀴즈**: 인증 된 사용자 지정 퀴즈 답변을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-207">**POST /api/trivia**: Stores the quiz answer specified by the authenticated user.</span></span>

<span data-ttu-id="34394-208">Web API 컨트롤러 클래스에 대 한 초기 계획을 만들려면 Visual Studio에서 제공 하는 ASP.NET 스 캐 폴딩 도구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-208">You will use the ASP.NET Scaffolding tools provided by Visual Studio to create the baseline for the Web API controller class.</span></span>

1. <span data-ttu-id="34394-209">엽니다는 **WebApiConfig.cs** 파일을 **앱\_시작** 폴더.</span><span class="sxs-lookup"><span data-stu-id="34394-209">Open the **WebApiConfig.cs** file inside the **App\_Start** folder.</span></span> <span data-ttu-id="34394-210">이 파일 경로 Web API 컨트롤러 작업에 매핑되는 방식을 같은 Web API 서비스의 구성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-210">This file defines the configuration of the Web API service, like how routes are mapped to Web API controller actions.</span></span>
2. <span data-ttu-id="34394-211">다음 추가 문을 사용 하 여 파일의 시작 부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34394-211">Add the following using statement at the beginning of the file.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample7.cs)]
3. <span data-ttu-id="34394-212">다음 강조 표시 된 코드를 추가 합니다 **등록** 전역적으로 Web API 작업 메서드에 의해 검색 되는 JSON 데이터에 대 한 포맷터를 구성 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-212">Add the following highlighted code to the **Register** method to globally configure the formatter for the JSON data retrieved by the Web API action methods.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample8.cs)]

    > [!NOTE]
    > <span data-ttu-id="34394-213">**CamelCasePropertyNamesContractResolver** 자동으로 속성 이름을 변환 *카멜식 대 /* 사례는 JavaScript의 속성 이름에 대 한 일반 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-213">The **CamelCasePropertyNamesContractResolver** automatically converts property names to *camel* case, which is the general convention for property names in JavaScript.</span></span>
4. <span data-ttu-id="34394-214">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **컨트롤러** 폴더를 **GeekQuiz** 프로젝트를 마우스 **추가 | 스 캐 폴드 된 새 항목...** .</span><span class="sxs-lookup"><span data-stu-id="34394-214">In **Solution Explorer**, right-click the **Controllers** folder of the **GeekQuiz** project and select **Add | New Scaffolded Item...**.</span></span>

    <span data-ttu-id="34394-215">![새 스 캐 폴드 된 항목을 만드는](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "스 캐 폴드 된 새 항목 만들기")</span><span class="sxs-lookup"><span data-stu-id="34394-215">![Creating a new scaffolded item](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "Creating a new scaffolded item")</span></span>

    <span data-ttu-id="34394-216">*새 스 캐 폴드 된 항목 만들기*</span><span class="sxs-lookup"><span data-stu-id="34394-216">*Creating a new scaffolded item*</span></span>
5. <span data-ttu-id="34394-217">에 **스 캐 폴드 추가** 대화 상자에서 확인를 **일반적인** 왼쪽된 창에서 노드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-217">In the **Add Scaffold** dialog box, make sure that the **Common** node is selected in the left pane.</span></span> <span data-ttu-id="34394-218">다음을 선택 합니다 **Web API 2 컨트롤러-비어 있음** 클릭 확인 하 고 가운데 창에서 템플릿을 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-218">Then, select the **Web API 2 Controller - Empty** template in the center pane and click **Add**.</span></span>

    <span data-ttu-id="34394-219">![웹 API 2 컨트롤러 빈 템플릿을 선택 하](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "웹 API 2 컨트롤러 빈 템플릿 선택")</span><span class="sxs-lookup"><span data-stu-id="34394-219">![Selecting the Web API 2 Controller Empty template](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "Selecting the Web API 2 Controller Empty template")</span></span>

    <span data-ttu-id="34394-220">*웹 API 2 컨트롤러 빈 템플릿 선택*</span><span class="sxs-lookup"><span data-stu-id="34394-220">*Selecting the Web API 2 Controller Empty template*</span></span>

    > [!NOTE]
    > <span data-ttu-id="34394-221">**ASP.NET 스 캐 폴딩** 는 ASP.NET 웹 응용 프로그램에 대 한 코드 생성 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-221">**ASP.NET Scaffolding** is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="34394-222">Visual Studio 2013 MVC 및 Web API 프로젝트에 대 한 사전 설치 된 코드 생성기를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-222">Visual Studio 2013 includes pre-installed code generators for MVC and Web API projects.</span></span> <span data-ttu-id="34394-223">신속 하 게 표준 데이터 작업을 개발 하는 데 필요한 시간을 줄이기 위해 데이터 모델과 상호 작용 하는 코드를 추가 하려는 경우 프로젝트에서 스 캐 폴딩을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-223">You should use scaffolding in your project when you want to quickly add code that interacts with data models in order to reduce the amount of time required to develop standard data operations.</span></span>
    > 
    > <span data-ttu-id="34394-224">스 캐 폴딩 프로세스 하면 필요한 모든 종속성을 프로젝트에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34394-224">The scaffolding process also ensures that all the required dependencies are installed in the project.</span></span> <span data-ttu-id="34394-225">예를 들어, 빈 ASP.NET 프로젝트를 시작 하 고 다음 스 캐 폴딩을 사용 하 여 Web API 컨트롤러를 추가할 경우 필요한 웹 API NuGet 패키지와 참조를 프로젝트에 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34394-225">For example, if you start with an empty ASP.NET project and then use scaffolding to add a Web API controller, the required Web API NuGet packages and references are added to your project automatically.</span></span>
6. <span data-ttu-id="34394-226">에 **컨트롤러 추가** 대화 상자에서 *TriviaController* 에 **컨트롤러 이름** 입력란을 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-226">In the **Add Controller** dialog box, type *TriviaController* in the **Controller name** text box and click **Add**.</span></span>

    <span data-ttu-id="34394-227">![기타 정보 컨트롤러 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "퀴즈 컨트롤러 추가")</span><span class="sxs-lookup"><span data-stu-id="34394-227">![Adding the Trivia Controller](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "Adding the Trivia Controller")</span></span>

    <span data-ttu-id="34394-228">*기타 정보 컨트롤러 추가*</span><span class="sxs-lookup"><span data-stu-id="34394-228">*Adding the Trivia Controller*</span></span>
7. <span data-ttu-id="34394-229">**TriviaController.cs** 파일에 추가 됩니다 합니다 **컨트롤러** 폴더를 **GeekQuiz** 빈 포함 된 프로젝트 **TriviaController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-229">The **TriviaController.cs** file is then added to the **Controllers** folder of the **GeekQuiz** project, containing an empty **TriviaController** class.</span></span> <span data-ttu-id="34394-230">다음 추가 using 문을 파일의 시작 부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34394-230">Add the following using statements at the beginning of the file.</span></span>

    <span data-ttu-id="34394-231">(코드 조각- *AspNetWebApiSpa-e x 1-TriviaControllerUsings*)</span><span class="sxs-lookup"><span data-stu-id="34394-231">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerUsings*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample9.cs)]
8. <span data-ttu-id="34394-232">시작 부분에 다음 코드를 추가 합니다 **TriviaController** 정의 초기화 및 삭제 하는 클래스는 **TriviaContext** 컨트롤러의 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="34394-232">Add the following code at the beginning of the **TriviaController** class to define, initialize and dispose the **TriviaContext** instance in the controller.</span></span>

    <span data-ttu-id="34394-233">(코드 조각- *AspNetWebApiSpa-e x 1-TriviaControllerContext*)</span><span class="sxs-lookup"><span data-stu-id="34394-233">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerContext*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample10.cs)]

    > [!NOTE]
    > <span data-ttu-id="34394-234">**Dispose** 메서드의 **TriviaController** 를 호출 하는 **Dispose** 메서드의 **TriviaContext** 하도록 하는 경우 모든 컨텍스트 개체에서 사용 하는 리소스가 해제 됩니다 때 합니다 **TriviaContext** 인스턴스가 삭제 되거나 가비지 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-234">The **Dispose** method of **TriviaController** invokes the **Dispose** method of the **TriviaContext** instance, which ensures that all the resources used by the context object are released when the **TriviaContext** instance is disposed or garbage-collected.</span></span> <span data-ttu-id="34394-235">Entity Framework에서 연 모든 데이터베이스 연결을 닫는 것이 여기 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34394-235">This includes closing all database connections opened by Entity Framework.</span></span>
9. <span data-ttu-id="34394-236">끝에 다음 도우미 메서드를 추가 합니다 **TriviaController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-236">Add the following helper method at the end of the **TriviaController** class.</span></span> <span data-ttu-id="34394-237">이 메서드는 다음 퀴즈 질문에 응답 하도록 지정된 된 사용자 데이터베이스에서 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-237">This method retrieves the following quiz question from the database to be answered by the specified user.</span></span>

    <span data-ttu-id="34394-238">(코드 조각- *AspNetWebApiSpa-e x 1-TriviaControllerNextQuestion*)</span><span class="sxs-lookup"><span data-stu-id="34394-238">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerNextQuestion*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample11.cs)]
10. <span data-ttu-id="34394-239">다음을 추가 합니다 **가져오기** 하는 작업 메서드는 **TriviaController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-239">Add the following **Get** action method to the **TriviaController** class.</span></span> <span data-ttu-id="34394-240">이 작업 메서드를 호출 합니다 **NextQuestionAsync** 인증된 된 사용자에 대 한 다음 질문을 검색 하는 이전 단계에서 정의 하는 도우미 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-240">This action method calls the **NextQuestionAsync** helper method defined in the previous step to retrieve the next question for the authenticated user.</span></span>

    <span data-ttu-id="34394-241">(코드 조각- *AspNetWebApiSpa-e x 1-TriviaControllerGetAction*)</span><span class="sxs-lookup"><span data-stu-id="34394-241">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerGetAction*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample12.cs)]
11. <span data-ttu-id="34394-242">끝에 다음 도우미 메서드를 추가 합니다 **TriviaController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-242">Add the following helper method at the end of the **TriviaController** class.</span></span> <span data-ttu-id="34394-243">이 메서드는 데이터베이스에 지정 된 응답을 저장 하 고 답이 맞으면 여부 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-243">This method stores the specified answer in the database and returns a Boolean value indicating whether or not the answer is correct.</span></span>

    <span data-ttu-id="34394-244">(코드 조각- *AspNetWebApiSpa-e x 1-TriviaControllerStoreAsync*)</span><span class="sxs-lookup"><span data-stu-id="34394-244">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerStoreAsync*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample13.cs)]
12. <span data-ttu-id="34394-245">다음을 추가 합니다 **게시물** 하는 작업 메서드는 **TriviaController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-245">Add the following **Post** action method to the **TriviaController** class.</span></span> <span data-ttu-id="34394-246">이 동작 메서드에 인증 된 사용자 및 호출에 대 한 답을 연결 합니다 **StoreAsync** 도우미 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-246">This action method associates the answer to the authenticated user and calls the **StoreAsync** helper method.</span></span> <span data-ttu-id="34394-247">그런 다음 도우미 메서드에 의해 반환 되는 부울 값을 사용 하 여 응답을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="34394-247">Then, it sends a response with the Boolean value returned by the helper method.</span></span>

    <span data-ttu-id="34394-248">(코드 조각- *AspNetWebApiSpa-e x 1-TriviaControllerPostAction*)</span><span class="sxs-lookup"><span data-stu-id="34394-248">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerPostAction*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample14.cs)]
13. <span data-ttu-id="34394-249">추가 하 여 인증 된 사용자에 게 액세스를 제한 하는 Web API 컨트롤러를 수정 합니다 **권한 부여** 특성을 합니다 **TriviaController** 클래스 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-249">Modify the Web API controller to restrict access to authenticated users by adding the **Authorize** attribute to the **TriviaController** class definition.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample15.cs)]

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="34394-250">작업 3 – 솔루션 실행</span><span class="sxs-lookup"><span data-stu-id="34394-250">Task 3 – Running the Solution</span></span>

<span data-ttu-id="34394-251">이 작업에서는 이전 태스크에서 만든 웹 API 서비스를 예상 대로 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-251">In this task you will verify that the Web API service you built in the previous task is working as expected.</span></span> <span data-ttu-id="34394-252">Internet Explorer를 사용할지 **F12 개발자 도구** 네트워크 트래픽 캡처 및 Web API 서비스의 전체 응답을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-252">You will use the Internet Explorer **F12 Developer Tools** to capture the network traffic and inspect the full response from the Web API service.</span></span>

> [!NOTE]
> <span data-ttu-id="34394-253">했는지 **Internet Explorer** 가 선택 합니다 **시작** Visual Studio 도구 모음에 있는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-253">Make sure that **Internet Explorer** is selected in the **Start** button located on the Visual Studio toolbar.</span></span>
> 
> ![Internet Explorer 옵션](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image9.png)


1. <span data-ttu-id="34394-255">키를 눌러 **F5** 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-255">Press **F5** to run the solution.</span></span> <span data-ttu-id="34394-256">합니다 **로그인** 페이지가 브라우저에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34394-256">The **Log in** page should appear in the browser.</span></span>

    > [!NOTE]
    > <span data-ttu-id="34394-257">응용 프로그램이 시작 되 면 기본 MVC 경로 트리거될에 매핑되는 기본적으로는 **인덱스** 작업을 **HomeController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-257">When the application starts, the default MVC route is triggered, which by default is mapped to the **Index** action of the **HomeController** class.</span></span> <span data-ttu-id="34394-258">하므로 **HomeController** 인증 된 사용자 에게만 부여 됩니다 (기억 사용 하 여 해당 클래스를 데코 레이트 하는 **권한 부여** 실습 1에서 특성) 인증 사용자 아직 응용 프로그램 이며 로그인 페이지를 원래 요청을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-258">Since **HomeController** is restricted to authenticated users (remember that you decorated that class with the **Authorize** attribute in Exercise 1) and there is no user authenticated yet, the application redirects the original request to the log in page.</span></span>

    <span data-ttu-id="34394-259">![솔루션을 실행](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "솔루션 실행")</span><span class="sxs-lookup"><span data-stu-id="34394-259">![Running the solution](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "Running the solution")</span></span>

    <span data-ttu-id="34394-260">*솔루션 실행*</span><span class="sxs-lookup"><span data-stu-id="34394-260">*Running the solution*</span></span>
2. <span data-ttu-id="34394-261">클릭 **등록** 새 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="34394-261">Click **Register** to create a new user.</span></span>

    <span data-ttu-id="34394-262">![새 사용자를 등록](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "새 사용자 등록")</span><span class="sxs-lookup"><span data-stu-id="34394-262">![Registering a new user](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "Registering a new user")</span></span>

    <span data-ttu-id="34394-263">*새 사용자 등록*</span><span class="sxs-lookup"><span data-stu-id="34394-263">*Registering a new user*</span></span>
3. <span data-ttu-id="34394-264">에 **등록** 페이지에서 입력을 **사용자 이름** 및 **암호**를 클릭 하 고 **등록**합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-264">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    <span data-ttu-id="34394-265">![등록 페이지](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "등록 페이지")</span><span class="sxs-lookup"><span data-stu-id="34394-265">![Register page](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "Register page")</span></span>

    <span data-ttu-id="34394-266">*등록 페이지*</span><span class="sxs-lookup"><span data-stu-id="34394-266">*Register page*</span></span>
4. <span data-ttu-id="34394-267">응용 프로그램에 새 계정을 등록 하 고 사용자가 인증 하 고 홈 페이지로 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="34394-267">The application registers the new account and the user is authenticated and redirected back to the home page.</span></span>

    <span data-ttu-id="34394-268">![사용자가 인증](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "인증 된 사용자")</span><span class="sxs-lookup"><span data-stu-id="34394-268">![User is authenticated](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "User authenticated")</span></span>

    <span data-ttu-id="34394-269">*사용자가 인증*</span><span class="sxs-lookup"><span data-stu-id="34394-269">*User is authenticated*</span></span>
5. <span data-ttu-id="34394-270">키를 눌러 브라우저에서 **F12** 열려는 합니다 **개발자 도구** 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-270">In the browser, press **F12** to open the **Developer Tools** panel.</span></span> <span data-ttu-id="34394-271">키를 눌러 **CTRL + 4** 누르거나를 **네트워크** 아이콘을 한 다음 단추를 클릭 하 고 녹색 화살표 네트워크 트래픽 캡처를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-271">Press **CTRL + 4** or click the **Network** icon, and then click the green arrow button to begin capturing network traffic.</span></span>

    <span data-ttu-id="34394-272">![Web API 네트워크 캡처를 시작](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "Web API 시작 네트워크 캡처")</span><span class="sxs-lookup"><span data-stu-id="34394-272">![Initiating Web API network capture](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "Initiating Web API network capture")</span></span>

    <span data-ttu-id="34394-273">*Web API 네트워크 캡처를 시작합니다.*</span><span class="sxs-lookup"><span data-stu-id="34394-273">*Initiating Web API network capture*</span></span>
6. <span data-ttu-id="34394-274">추가 **api/퀴즈** 브라우저의 주소 표시줄에서 URL로 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-274">Append **api/trivia** to the URL in the browser's address bar.</span></span> <span data-ttu-id="34394-275">이제 응답의 세부 정보를 검사 하는 합니다 **가져옵니다** 의 동작 메서드에 **TriviaController**합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-275">You will now inspect the details of the response from the **Get** action method in **TriviaController**.</span></span>

    <span data-ttu-id="34394-276">![웹 API를 통해 다음 질문 데이터를 검색할](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "웹 API를 통해 다음 질문 데이터를 검색 합니다.")</span><span class="sxs-lookup"><span data-stu-id="34394-276">![Retrieving the next question data through Web API](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "Retrieving the next question data through Web API")</span></span>

    <span data-ttu-id="34394-277">*웹 API를 통해 다음 질문 데이터를 검색합니다.*</span><span class="sxs-lookup"><span data-stu-id="34394-277">*Retrieving the next question data through Web API*</span></span>

    > [!NOTE]
    > <span data-ttu-id="34394-278">다운로드가 완료 되 면 다운로드 한 파일을 사용 하 여 작업을 할 수 있도록 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="34394-278">Once the download finishes, you will be prompted to make an action with the downloaded file.</span></span> <span data-ttu-id="34394-279">대화 상자는 개발자 도구 창을 통해 응답 콘텐츠를 볼 수 있도록 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="34394-279">Leave the dialog box open in order to be able to watch the response content through the Developers Tool window.</span></span>
7. <span data-ttu-id="34394-280">이제는 응답의 본문을 조사 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-280">Now you will inspect the body of the response.</span></span> <span data-ttu-id="34394-281">이렇게 하려면 클릭 합니다 **세부 정보** 탭을 클릭 한 다음 **응답 본문**합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-281">To do this, click the **Details** tab and then click **Response body**.</span></span> <span data-ttu-id="34394-282">다운로드 한 데이터 속성을 사용 하 여 개체를 확인할 수 있습니다 **옵션** (의 목록인 **TriviaOption** 개체), **id** 및 **제목** 에 해당 하는 **TriviaQuestion** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-282">You can check that the downloaded data is an object with the properties **options** (which is a list of **TriviaOption** objects), **id** and **title** that correspond to the **TriviaQuestion** class.</span></span>

    <span data-ttu-id="34394-283">![웹 API 응답 본문을 보는](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "웹 API 응답 본문 보기")</span><span class="sxs-lookup"><span data-stu-id="34394-283">![Viewing the Web API Response Body](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "Viewing the Web API Response Body")</span></span>

    <span data-ttu-id="34394-284">*웹 API 응답 본문 보기*</span><span class="sxs-lookup"><span data-stu-id="34394-284">*Viewing Web API Response Body*</span></span>
8. <span data-ttu-id="34394-285">Visual Studio 및 키를 눌러도 돌아가 **shift+f5** 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-285">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-creating-the-spa-interface"></a><span data-ttu-id="34394-286">연습 2: SPA 인터페이스를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="34394-286">Exercise 2: Creating the SPA Interface</span></span>

<span data-ttu-id="34394-287">이 연습에서는 먼저 빌드합니다 Geek 퀴즈의 웹 프런트 엔드 부분을 사용 하 여 단일 페이지 응용 프로그램 상호 작용에 집중 **AngularJS**합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-287">In this exercise you will first build the web front-end portion of Geek Quiz, focusing on the Single-Page Application interaction using **AngularJS**.</span></span> <span data-ttu-id="34394-288">풍부한 애니메이션을 수행 하 고 다음 질문 중 하나에서 전환 하는 경우 하면 컨텍스트 전환을 활용 시각 효과 제공 하는 CSS3 사용 하 여 사용자 환경을 개선 다음 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34394-288">You will then enhance the user experience with CSS3 to perform rich animations and provide a visual effect of context switching when transitioning from one question to the next.</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-the-spa-interface-using-angularjs"></a><span data-ttu-id="34394-289">작업 1-AngularJS를 사용 하 여 SPA 인터페이스를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="34394-289">Task 1 – Creating the SPA Interface Using AngularJS</span></span>

<span data-ttu-id="34394-290">이 작업에서는 사용 하 여 **AngularJS** Geek 퀴즈 응용 프로그램의 클라이언트 쪽을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-290">In this task you will use **AngularJS** to implement the client side of the Geek Quiz application.</span></span> <span data-ttu-id="34394-291">**AngularJS** 는 브라우저 기반 응용 프로그램을 확대 하는 오픈 소스 JavaScript 프레임 워크 *모델-뷰-컨트롤러* (MVC) 기능을 모두 개발을 촉진 하 고 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-291">**AngularJS** is an open-source JavaScript framework that augments browser-based applications with *Model-View-Controller* (MVC) capability, facilitating both development and testing.</span></span>

<span data-ttu-id="34394-292">Visual Studio의 패키지 관리자 콘솔에서 AngularJS를 설치 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-292">You will start by installing AngularJS from Visual Studio's Package Manager Console.</span></span> <span data-ttu-id="34394-293">그런 다음 퀴즈 질문 및 답변에서 AngularJS 템플릿 엔진을 사용 하 여 렌더링할 뷰 Geek 퀴즈 앱의 동작을 제공 하도록 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="34394-293">Then, you will create the controller to provide the behavior of the Geek Quiz app and the view to render the quiz questions and answers using the AngularJS template engine.</span></span>

> [!NOTE]
> <span data-ttu-id="34394-294">AngularJS에 대 한 자세한 내용은 참조 [ [ http://angularjs.org/ ](http://angularjs.org/) ](http://angularjs.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-294">For more information about AngularJS, refer to [[http://angularjs.org/](http://angularjs.org/)](http://angularjs.org/).</span></span>


1. <span data-ttu-id="34394-295">엽니다 **Visual Studio Express 2013 for Web** 연 합니다 **GeekQuiz.sln** 솔루션을 **소스/e x 2-CreatingASPAInterface/시작** 폴더.</span><span class="sxs-lookup"><span data-stu-id="34394-295">Open **Visual Studio Express 2013 for Web** and open the **GeekQuiz.sln** solution located in the **Source/Ex2-CreatingASPAInterface/Begin** folder.</span></span> <span data-ttu-id="34394-296">또는 계속할 수 있습니다 솔루션을 사용 하 여 이전 연습에서 얻은.</span><span class="sxs-lookup"><span data-stu-id="34394-296">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="34394-297">엽니다는 **패키지 관리자 콘솔** 에서 **도구** | **라이브러리 패키지 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-297">Open the **Package Manager Console** from **Tools** | **Library Package Manager**.</span></span> <span data-ttu-id="34394-298">설치 하려면 다음 명령을 입력 합니다 **AngularJS.Core** NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="34394-298">Type the following command to install the **AngularJS.Core** NuGet package.</span></span>

    [!code-powershell[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample16.ps1)]
3. <span data-ttu-id="34394-299">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **스크립트** 폴더를 **GeekQuiz** 프로젝트를 마우스 **추가 | 새 폴더**합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-299">In **Solution Explorer**, right-click the **Scripts** folder of the **GeekQuiz** project and select **Add | New Folder**.</span></span> <span data-ttu-id="34394-300">폴더의 이름을 **앱** 누릅니다 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-300">Name the folder **app** and press **Enter**.</span></span>
4. <span data-ttu-id="34394-301">마우스 오른쪽 단추로 클릭 합니다 **앱** 폴더 바로 전에 만들고 선택 **추가 | JavaScript 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-301">Right-click the **app** folder you just created and select **Add | JavaScript File**.</span></span>

    ![새 JavaScript 파일 만들기](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image17.png)

    <span data-ttu-id="34394-303">*새 JavaScript 파일 만들기*</span><span class="sxs-lookup"><span data-stu-id="34394-303">*Creating a new JavaScript file*</span></span>
5. <span data-ttu-id="34394-304">에 **항목에 대 한 이름 지정** 대화 상자에서 *퀴즈 컨트롤러* 에 **항목 이름** 입력란을 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-304">In the **Specify Name for Item** dialog box, type *quiz-controller* in the **Item name** text box and click **OK**.</span></span>

    ![새 JavaScript 파일 이름 지정](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image18.png)

    <span data-ttu-id="34394-306">*새 JavaScript 파일 이름 지정*</span><span class="sxs-lookup"><span data-stu-id="34394-306">*Naming the new JavaScript file*</span></span>
6. <span data-ttu-id="34394-307">에 **퀴즈 controller.js** 파일을 다음 코드를 선언 하 고 초기화 AngularJS 추가 **QuizCtrl** 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-307">In the **quiz-controller.js** file, add the following code to declare and initialize the AngularJS **QuizCtrl** controller.</span></span>

    <span data-ttu-id="34394-308">(코드 조각- *AspNetWebApiSpa-e x 2-AngularQuizController*)</span><span class="sxs-lookup"><span data-stu-id="34394-308">(Code Snippet - *AspNetWebApiSpa - Ex2 - AngularQuizController*)</span></span>

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample17.js)]

    > [!NOTE]
    > <span data-ttu-id="34394-309">생성자 함수는 **QuizCtrl** 컨트롤러 라는 injectable 매개 변수를 예상 **$scope**합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-309">The constructor function of the **QuizCtrl** controller expects an injectable parameter named **$scope**.</span></span> <span data-ttu-id="34394-310">범위의 초기 상태를 설정 해야 생성자 함수에서 속성을 연결 하 여 합니다 **$scope** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-310">The initial state of the scope should be set up in the constructor function by attaching properties to the **$scope** object.</span></span> <span data-ttu-id="34394-311">속성을 포함 합니다 **뷰 모델**, 및 컨트롤러를 등록할 때 서식 파일에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34394-311">The properties contain the **view model**, and will be accessible to the template when the controller is registered.</span></span>
    > 
    > <span data-ttu-id="34394-312">합니다 **QuizCtrl** 컨트롤러 라는 모듈 내에서 정의 됩니다 **QuizApp**합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-312">The **QuizCtrl** controller is defined inside a module named **QuizApp**.</span></span> <span data-ttu-id="34394-313">모듈은 별도 구성 요소에 응용 프로그램 중단할 수 있는 작업 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-313">Modules are units of work that let you break your application into separate components.</span></span> <span data-ttu-id="34394-314">모듈을 사용 하는 데 필요한 주요 이점은 코드를 이해 하기 쉬운 단위 테스트, 재사용 및 유지 관리를 용이 하 게 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-314">The main advantages of using modules is that the code is easier to understand and facilitates unit testing, reusability and maintainability.</span></span>
7. <span data-ttu-id="34394-315">이제 보기에서 트리거되는 이벤트에 대응 하기 위해 범위에 동작을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-315">You will now add behavior to the scope in order to react to events triggered from the view.</span></span> <span data-ttu-id="34394-316">끝에 다음 코드를 추가 합니다 **QuizCtrl** 정의 하는 컨트롤러를 **nextQuestion** 함수를 **$scope** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-316">Add the following code at the end of the **QuizCtrl** controller to define the **nextQuestion** function in the **$scope** object.</span></span>

    <span data-ttu-id="34394-317">(코드 조각- *AspNetWebApiSpa-e x 2-AngularQuizControllerNextQuestion*)</span><span class="sxs-lookup"><span data-stu-id="34394-317">(Code Snippet - *AspNetWebApiSpa - Ex2 - AngularQuizControllerNextQuestion*)</span></span>

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample18.js)]

    > [!NOTE]
    > <span data-ttu-id="34394-318">이 함수에서 다음 질문을 검색 합니다는 **퀴즈** Web API는 이전 연습에서 만든 및 질문 데이터를 연결 합니다 **$scope** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-318">This function retrieves the next question from the **Trivia** Web API created in the previous exercise and attaches the question data to the **$scope** object.</span></span>
8. <span data-ttu-id="34394-319">끝에 다음 코드를 삽입 합니다 **QuizCtrl** 정의 하는 컨트롤러를 **sendAnswer** 함수를 **$scope** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-319">Insert the following code at the end of the **QuizCtrl** controller to define the **sendAnswer** function in the **$scope** object.</span></span>

    <span data-ttu-id="34394-320">(코드 조각- *AspNetWebApiSpa-e x 2-AngularQuizControllerSendAnswer*)</span><span class="sxs-lookup"><span data-stu-id="34394-320">(Code Snippet - *AspNetWebApiSpa - Ex2 - AngularQuizControllerSendAnswer*)</span></span>

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample19.js)]

    > [!NOTE]
    > <span data-ttu-id="34394-321">이 함수를 사용자가 선택한 응답을 보냅니다 합니다 **퀴즈** Web API에서 여부 답이 맞으면 – 하는 경우 – 즉, 결과 저장 하 고는 **$scope** 개체.</span><span class="sxs-lookup"><span data-stu-id="34394-321">This function sends the answer selected by the user to the **Trivia** Web API and stores the result –i.e. if the answer is correct or not– in the **$scope** object.</span></span>
    > 
    > <span data-ttu-id="34394-322">**nextQuestion** 하 고 **sendAnswer** AngularJS를 사용 하 여 위의 함수 **$http** XMLHttpRequest 통해 웹 API와의 통신을 추상화 하는 개체 브라우저에서 JavaScript 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-322">The **nextQuestion** and **sendAnswer** functions from above use the AngularJS **$http** object to abstract the communication with the Web API via the XMLHttpRequest JavaScript object from the browser.</span></span> <span data-ttu-id="34394-323">AngularJS 더 높은 수준의 RESTful Api를 통해 리소스에 대 한 CRUD 작업을 수행 하는 추상화를 제공 하는 다른 서비스를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-323">AngularJS supports another service that brings a higher level of abstraction to perform CRUD operations against a resource through RESTful APIs.</span></span> <span data-ttu-id="34394-324">AngularJS **$resource** 개체에 상호 작용 하지 않고도 높은 수준의 동작을 제공 하는 작업 메서드는 **$http** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-324">The AngularJS **$resource** object has action methods which provide high-level behaviors without the need to interact with the **$http** object.</span></span> <span data-ttu-id="34394-325">사용 하는 것이 좋습니다 합니다 **$resource** CRUD 모델을 해야 하는 시나리오에서 개체 ((영문) 정보를 참조 합니다 [$resource 설명서](https://docs.angularjs.org/api/ngResource/service/$resource)).</span><span class="sxs-lookup"><span data-stu-id="34394-325">Consider using the **$resource** object in scenarios that requires the CRUD model (fore information, see the [$resource documentation](https://docs.angularjs.org/api/ngResource/service/$resource)).</span></span>
9. <span data-ttu-id="34394-326">다음 단계 퀴즈에 대 한 보기를 정의 하는 AngularJS 템플릿을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-326">The next step is to create the AngularJS template that defines the view for the quiz.</span></span> <span data-ttu-id="34394-327">이 작업을 수행 하려면 엽니다는 **Index.cshtml** 파일을 **뷰 | 홈** 폴더 및 내용 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="34394-327">To do this, open the **Index.cshtml** file inside the **Views | Home** folder and replace the content with the following code.</span></span>

    <span data-ttu-id="34394-328">(코드 조각- *AspNetWebApiSpa-e x 2-GeekQuizView*)</span><span class="sxs-lookup"><span data-stu-id="34394-328">(Code Snippet - *AspNetWebApiSpa - Ex2 - GeekQuizView*)</span></span>

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample20.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="34394-329">AngularJS 템플릿은 모델 및 컨트롤러의 정보를 사용 하 여 브라우저에서 사용자에 게 동적 보기에 정적 태그를 변환 하는 선언적 사양입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-329">The AngularJS template is a declarative specification that uses information from the model and the controller to transform static markup into the dynamic view that the user sees in the browser.</span></span> <span data-ttu-id="34394-330">다음은 AngularJS 요소 및 템플릿에서 사용할 수 있는 요소 특성의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-330">The following are examples of AngularJS elements and element attributes that can be used in a template:</span></span>
    > 
    > - <span data-ttu-id="34394-331">합니다 **ng 앱** 지시문은 AngularJS 응용 프로그램의 루트 요소를 나타내는 DOM 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-331">The **ng-app** directive tells AngularJS the DOM element that represents the root element of the application.</span></span>
    > - <span data-ttu-id="34394-332">합니다 **ng-컨트롤러** 지시문 지점 지시문 선언 된 위치에서 DOM에 컨트롤러를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-332">The **ng-controller** directive attaches a controller to the DOM at the point where the directive is declared.</span></span>
    > - <span data-ttu-id="34394-333">중괄호 표기법 **{{}}** 컨트롤러에 정의 된 범위 속성에 대 한 바인딩을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="34394-333">The curly brace notation **{{ }}** denotes bindings to the scope properties defined in the controller.</span></span>
    > - <span data-ttu-id="34394-334">합니다 **ng 원클릭** 지시문 사용에 대 한 응답 사용자가 클릭할 때 범위에 정의 된 함수를 호출 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-334">The **ng-click** directive is used to invoke the functions defined in the scope in response to user clicks.</span></span>
10. <span data-ttu-id="34394-335">열기는 **Site.css** 파일을 **콘텐츠** 폴더 퀴즈 뷰에 대 한 모양 및 느낌을 제공 하는 파일의 끝에 다음 강조 표시 된 스타일을 추가 하 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-335">Open the **Site.css** file inside the **Content** folder and add the following highlighted styles at the end of the file to provide a look and feel for the quiz view.</span></span>

    <span data-ttu-id="34394-336">(코드 조각- *AspNetWebApiSpa-e x 2-GeekQuizStyles*)</span><span class="sxs-lookup"><span data-stu-id="34394-336">(Code Snippet - *AspNetWebApiSpa - Ex2 - GeekQuizStyles*)</span></span>

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample21.css)]

<a id="Ex2Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="34394-337">작업 2-솔루션 실행</span><span class="sxs-lookup"><span data-stu-id="34394-337">Task 2 – Running the Solution</span></span>

<span data-ttu-id="34394-338">실행 하는이 태스크에서는 새 사용자를 사용 하 여 솔루션 일부의 퀴즈 질문에 대답 하는 AngularJS를 사용 하 여 빌드한 있습니다 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-338">In this task you will execute the solution using the new user interface you built with AngularJS to answer some of the quiz questions.</span></span>

1. <span data-ttu-id="34394-339">키를 눌러 **F5** 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-339">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="34394-340">새 사용자 계정을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-340">Register a new user account.</span></span> <span data-ttu-id="34394-341">이 위해 연습 1, 작업 3에서에서 설명한 등록 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-341">To do this, follow the registration steps described in Exercise 1, Task 3.</span></span>

    > [!NOTE]
    > <span data-ttu-id="34394-342">이전 연습에서 솔루션을 사용 하는 경우에 이전에 만든 사용자 계정으로 로그인 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34394-342">If you are using the solution from the previous exercise, you can log in with the user account you created before.</span></span>
3. <span data-ttu-id="34394-343">합니다 **홈** 퀴즈의 첫 번째 질문을 보여 주는 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34394-343">The **Home** page should appear, showing the first question of the quiz.</span></span> <span data-ttu-id="34394-344">옵션 중 하나를 클릭 하 여 질문에 대답 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-344">Answer the question by clicking one of the options.</span></span> <span data-ttu-id="34394-345">이 트리거됩니다 합니다 **sendAnswer** 선택된 옵션은 전송 하는 앞에서 정의한 함수를 **퀴즈** Web API입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-345">This will trigger the **sendAnswer** function defined earlier, which sends the selected option to the **Trivia** Web API.</span></span>

    <span data-ttu-id="34394-346">![정보를 파악 하기가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "질문에 대답")</span><span class="sxs-lookup"><span data-stu-id="34394-346">![Answering a question](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "Answering a question")</span></span>

    <span data-ttu-id="34394-347">*질문에 대답*</span><span class="sxs-lookup"><span data-stu-id="34394-347">*Answering a question*</span></span>
4. <span data-ttu-id="34394-348">단추 중 하나를 클릭 한 후 답변 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34394-348">After clicking one of the buttons, the answer should appear.</span></span> <span data-ttu-id="34394-349">클릭 **다음 질문** 다음 질문을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-349">Click **Next Question** to show the following question.</span></span> <span data-ttu-id="34394-350">이렇게 하면 트리거됩니다 합니다 **nextQuestion** 컨트롤러에 정의 된 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-350">This will trigger the **nextQuestion** function defined in the controller.</span></span>

    <span data-ttu-id="34394-351">![다음 질문을 요청](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "다음 질문을 요청 합니다.")</span><span class="sxs-lookup"><span data-stu-id="34394-351">![Requesting the next question](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "Requesting the next question")</span></span>

    <span data-ttu-id="34394-352">*다음 질문을 요청합니다.*</span><span class="sxs-lookup"><span data-stu-id="34394-352">*Requesting the next question*</span></span>
5. <span data-ttu-id="34394-353">다음 질문에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="34394-353">The next question should appear.</span></span> <span data-ttu-id="34394-354">원하는 횟수 만큼 질문에 응답을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-354">Continue answering questions as many times as you want.</span></span> <span data-ttu-id="34394-355">모든 질문을 완료 한 후 첫 번째 질문을 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-355">After completing all the questions you should return to the first question.</span></span>

    <span data-ttu-id="34394-356">![다른 질문](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "또 다른 문제")</span><span class="sxs-lookup"><span data-stu-id="34394-356">![Another question](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "Another question")</span></span>

    <span data-ttu-id="34394-357">*다음 질문*</span><span class="sxs-lookup"><span data-stu-id="34394-357">*Next question*</span></span>
6. <span data-ttu-id="34394-358">Visual Studio 및 키를 눌러도 돌아가 **shift+f5** 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-358">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--creating-a-flip-animation-using-css3"></a><span data-ttu-id="34394-359">작업 3-만드는 Css3 애니메이션을 대칭 이동</span><span class="sxs-lookup"><span data-stu-id="34394-359">Task 3 – Creating a Flip Animation Using CSS3</span></span>

<span data-ttu-id="34394-360">이 작업에서 질문에 답변 하는 경우 및 다음 질문을 검색할 때 플립 효과 추가 하 여 다양 한 애니메이션을 수행 하려면 CSS3 속성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-360">In this task you will use CSS3 properties to perform rich animations by adding a flip effect when a question is answered and when the next question is retrieved.</span></span>

1. <span data-ttu-id="34394-361">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **콘텐츠** 폴더를 **GeekQuiz** 프로젝트를 마우스 **추가 | 기존 항목...** .</span><span class="sxs-lookup"><span data-stu-id="34394-361">In **Solution Explorer**, right-click the **Content** folder of the **GeekQuiz** project and select **Add | Existing Item...**.</span></span>

    <span data-ttu-id="34394-362">![콘텐츠 폴더에 기존 항목 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "콘텐츠 폴더에 기존 항목 추가")</span><span class="sxs-lookup"><span data-stu-id="34394-362">![Adding an existing item to the Content folder](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "Adding an existing item to the Content folder")</span></span>

    <span data-ttu-id="34394-363">*콘텐츠 폴더에 기존 항목 추가*</span><span class="sxs-lookup"><span data-stu-id="34394-363">*Adding an existing item to the Content folder*</span></span>
2. <span data-ttu-id="34394-364">에 **기존 항목 추가** 대화 상자에서 **원본/자산** 폴더를 선택 **Flip.css**합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-364">In the **Add Existing Item** dialog box, navigate to the **Source/Assets** folder and select **Flip.css**.</span></span> <span data-ttu-id="34394-365">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-365">Click **Add**.</span></span>

    <span data-ttu-id="34394-366">![자산에서 Flip.css 파일 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "자산에서 Flip.css 파일 추가")</span><span class="sxs-lookup"><span data-stu-id="34394-366">![Adding the Flip.css file from Assets](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "Adding the Flip.css file from Assets")</span></span>

    <span data-ttu-id="34394-367">*자산에서 Flip.css 파일 추가*</span><span class="sxs-lookup"><span data-stu-id="34394-367">*Adding the Flip.css file from Assets*</span></span>
3. <span data-ttu-id="34394-368">엽니다는 **Flip.css** 방금 추가한 파일 및 해당 내용을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-368">Open the **Flip.css** file you just added and inspect its content.</span></span>
4. <span data-ttu-id="34394-369">찾을 합니다 **변환 대칭** 주석입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-369">Locate the **flip transformation** comment.</span></span> <span data-ttu-id="34394-370">CSS를 사용 하 여 해당 주석에 아래의 스타일 **관점** 및 **rotateY** 생성 하는 변환을 &quot;대칭 이동 후 카드&quot; 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-370">The styles below that comment use the CSS **perspective** and **rotateY** transformations to generate a &quot;card flip&quot; effect.</span></span>

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample22.css)]
5. <span data-ttu-id="34394-371">찾을 합니다 **대칭 이동 시의 창 숨기기** 주석입니다.</span><span class="sxs-lookup"><span data-stu-id="34394-371">Locate the **hide back of pane during flip** comment.</span></span> <span data-ttu-id="34394-372">설정 하 여 뷰어에서 떨어져 직면 하는 경우 해당 주석에 아래 스타일 중 백 쪽을 숨깁니다 합니다 **뒷면 가시성** CSS 속성을 *숨겨진*합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-372">The style below that comment hides the back-side of the faces when they are facing away from the viewer by setting the **backface-visibility** CSS property to *hidden*.</span></span>

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample23.css)]
6. <span data-ttu-id="34394-373">열기는 **BundleConfig.cs** 파일을 **앱\_시작** 폴더에 대 한 참조를 추가 하 고는 **Flip.css** 파일는 **&quot;~/Content/css&quot;** 스타일 번들</span><span class="sxs-lookup"><span data-stu-id="34394-373">Open the **BundleConfig.cs** file inside the **App\_Start** folder and add the reference to the **Flip.css** file in the **&quot;~/Content/css&quot;** style bundle</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample24.cs)]
7. <span data-ttu-id="34394-374">키를 눌러 **F5** 솔루션 및 자격 증명으로 로그인을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-374">Press **F5** to run the solution and log in with your credentials.</span></span>
8. <span data-ttu-id="34394-375">옵션 중 하나를 클릭 하 여 질문에 대답 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-375">Answer a question by clicking one of the options.</span></span> <span data-ttu-id="34394-376">뷰 간에 전환할 때 플립 효과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-376">Notice the flip effect when transitioning between views.</span></span>

    <span data-ttu-id="34394-377">![전환 효과 사용 하 여 질문에 답하려면](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "플립 효과 사용 하 여 질문에 대답")</span><span class="sxs-lookup"><span data-stu-id="34394-377">![Answering a question with the flip effect](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "Answering a question with the flip effect")</span></span>

    <span data-ttu-id="34394-378">*전환 효과 사용 하 여 질문에 대답*</span><span class="sxs-lookup"><span data-stu-id="34394-378">*Answering a question with the flip effect*</span></span>
9. <span data-ttu-id="34394-379">클릭 **의문이** 다음 질문을 검색 하려면.</span><span class="sxs-lookup"><span data-stu-id="34394-379">Click **Next Question** to retrieve the following question.</span></span> <span data-ttu-id="34394-380">전환 효과 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34394-380">The flip effect should appear again.</span></span>

    <span data-ttu-id="34394-381">![전환 효과 사용 하 여 다음 질문을 검색](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "플립 효과 사용 하 여 다음 질문을 검색 합니다.")</span><span class="sxs-lookup"><span data-stu-id="34394-381">![Retrieving the following question with the flip effect](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "Retrieving the following question with the flip effect")</span></span>

    <span data-ttu-id="34394-382">*전환 효과 사용 하 여 다음 질문을 검색합니다.*</span><span class="sxs-lookup"><span data-stu-id="34394-382">*Retrieving the following question with the flip effect*</span></span>

* * *

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="34394-383">요약</span><span class="sxs-lookup"><span data-stu-id="34394-383">Summary</span></span>

<span data-ttu-id="34394-384">이 실습을 완료 하 여 배웠습니다 방법:</span><span class="sxs-lookup"><span data-stu-id="34394-384">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="34394-385">ASP.NET 스 캐 폴딩을 사용 하는 ASP.NET Web API 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="34394-385">Create an ASP.NET Web API controller using ASP.NET Scaffolding</span></span>
- <span data-ttu-id="34394-386">다음 퀴즈 질문을 검색 하는 웹 API 가져오기 작업을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-386">Implement a Web API Get action to retrieve the next quiz question</span></span>
- <span data-ttu-id="34394-387">구현에 퀴즈의 답을 저장 하는 Web API 게시 작업</span><span class="sxs-lookup"><span data-stu-id="34394-387">Implement a Web API Post action to store the quiz answers</span></span>
- <span data-ttu-id="34394-388">Visual Studio 패키지 관리자 콘솔에서 AngularJS를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-388">Install AngularJS from the Visual Studio Package Manager Console</span></span>
- <span data-ttu-id="34394-389">AngularJS 템플릿 구현 및 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="34394-389">Implement AngularJS templates and controllers</span></span>
- <span data-ttu-id="34394-390">사용 하 여 CSS3 전환 애니메이션 효과 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="34394-390">Use CSS3 transitions to perform animation effects</span></span>
