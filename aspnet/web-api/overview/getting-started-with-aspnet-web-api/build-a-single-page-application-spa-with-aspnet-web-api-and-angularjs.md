---
uid: web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
title: '실습 랩: 빌드 ASP.NET Web API 및 Angular.js 단일 페이지 응용 프로그램 (SPA) | Microsoft Docs'
author: rick-anderson
description: 기존 웹 응용 프로그램에서 클라이언트 (브라우저) 페이지를 요청 하 여 서버와의 통신을 시작 합니다. 서버는 다음 요청을 처리 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/30/2015
ms.topic: article
ms.assetid: 719727b7-bef3-45ad-bfe9-ba5bcdb2305f
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
msc.type: authoredcontent
ms.openlocfilehash: 9a748628d53878be380869ac5327de0111d2284d
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "26507262"
---
<a name="hands-on-lab-build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs"></a><span data-ttu-id="b19e4-104">ASP.NET Web API 및 Angular.js 단일 페이지 응용 프로그램 (SPA)을 작성 하는 실습 랩:</span><span class="sxs-lookup"><span data-stu-id="b19e4-104">Hands On Lab: Build a Single Page Application (SPA) with ASP.NET Web API and Angular.js</span></span>
====================
<span data-ttu-id="b19e4-105">으로 [웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="b19e4-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="b19e4-106">웹 캠프 학습 키트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-106">Download Web Camps Training Kit</span></span>](http://aka.ms/webcamps-training-kit)

> <span data-ttu-id="b19e4-107">기존 웹 응용 프로그램에서 클라이언트 (브라우저) 페이지를 요청 하 여 서버와의 통신을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-107">In traditional web applications, the client (browser) initiates the communication with the server by requesting a page.</span></span> <span data-ttu-id="b19e4-108">그런 다음 서버는 요청을 처리 하 고 페이지의 HTML 클라이언트에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-108">The server then processes the request and sends the HTML of the page to the client.</span></span> <span data-ttu-id="b19e4-109">-예: 사용자 링크를 탐색 하거나 데이터를 사용 하 여 폼을 제출 – 페이지와 후속 상호 작용에서 새 요청을 서버에 전송 되 고는 흐름이 다시 시작: 서버가 요청을 처리 하 고 새 작업 요청에 대 한 응답으로 브라우저에 새 페이지 보냅니다 클라이언트에서 ed 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-109">In subsequent interactions with the page –e.g. the user navigates to a link or submits a form with data– a new request is sent to the server, and the flow starts again: the server processes the request and sends a new page to the browser in response to the new action requested by the client.</span></span>
> 
> <span data-ttu-id="b19e4-110">단일 페이지 응용 프로그램 (SPAs)에서 전체 페이지 로드 브라우저에서 초기 요청 후 되었지만 후속 상호 작용 Ajax 요청을 통해 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-110">In Single-Page Applications (SPAs) the entire page is loaded in the browser after the initial request, but subsequent interactions take place through Ajax requests.</span></span> <span data-ttu-id="b19e4-111">즉, 변경 된 페이지의 부분만 업데이트 하는 브라우저에 전체 페이지를 다시 로드 하지 않아도가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-111">This means that the browser has to update only the portion of the page that has changed; there is no need to reload the entire page.</span></span> <span data-ttu-id="b19e4-112">SPA 접근 방식을 시켜 더 강조 경험 하는 사용자 동작에 응답 하도록 응용 프로그램에서 사용한 시간을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-112">The SPA approach reduces the time taken by the application to respond to user actions, resulting in a more fluid experience.</span></span>
> 
> <span data-ttu-id="b19e4-113">SPA의 아키텍처는 기존 웹 응용 프로그램에 존재 하지 않는 특정 한 문제가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-113">The architecture of a SPA involves certain challenges that are not present in traditional web applications.</span></span> <span data-ttu-id="b19e4-114">그러나 CSS3에서 제공 하는 새 스타일 지정 기능 정말 쉽게 수 있도록 설계 및 구축 SPAs 및 ASP.NET Web API와 같은 기술을 발생 하 고, JavaScript 프레임 워크 같은 AngularJS 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-114">However, emerging technologies like ASP.NET Web API, JavaScript frameworks like AngularJS and new styling features provided by CSS3 make it really easy to design and build SPAs.</span></span>
> 
> <span data-ttu-id="b19e4-115">이 실습 랩에서 들은 퀴즈를 SPA 개념에 따라 trivia 웹 사이트를 구현 하는 이러한 기술 활용을 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-115">In this hand-on lab, you will take advantage of those technologies to implement Geek Quiz, a trivia website based on the SPA concept.</span></span> <span data-ttu-id="b19e4-116">먼저 ASP.NET 웹 api 퀴즈 질문을 검색 하 고 답을 저장할 필요한 끝점을 노출할 서비스 계층을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-116">You will first implement the service layer with ASP.NET Web API to expose the required endpoints to retrieve the quiz questions and store the answers.</span></span> <span data-ttu-id="b19e4-117">그런 다음, AngularJS 및 CSS3 변환 효과 사용 하 여 풍부 하 고 응답성이 뛰어난 UI를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-117">Then, you will build a rich and responsive UI using AngularJS and CSS3 transformation effects.</span></span>
> 
> <span data-ttu-id="b19e4-118">모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [ http://aka.ms/webcamps-training-kit ](http://aka.ms/webcamps-training-kit)합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-118">All sample code and snippets are included in the Web Camps Training Kit, available at [http://aka.ms/webcamps-training-kit](http://aka.ms/webcamps-training-kit).</span></span>


## <a name="overview"></a><span data-ttu-id="b19e4-119">개요</span><span class="sxs-lookup"><span data-stu-id="b19e4-119">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="b19e4-120">목표</span><span class="sxs-lookup"><span data-stu-id="b19e4-120">Objectives</span></span>

<span data-ttu-id="b19e4-121">이 실습 랩에서 배웁니다 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="b19e4-121">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="b19e4-122">JSON 데이터를 받거나 보내기 위해 ASP.NET 웹 API 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="b19e4-122">Create an ASP.NET Web API service to send and receive JSON data</span></span>
- <span data-ttu-id="b19e4-123">AngularJS를 사용 하 여 응답성이 뛰어난 UI 만들기</span><span class="sxs-lookup"><span data-stu-id="b19e4-123">Create a responsive UI using AngularJS</span></span>
- <span data-ttu-id="b19e4-124">CSS3 변형이 있는 기능의 UI 환경 향상</span><span class="sxs-lookup"><span data-stu-id="b19e4-124">Enhance the UI experience with CSS3 transformations</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="b19e4-125">전제 조건</span><span class="sxs-lookup"><span data-stu-id="b19e4-125">Prerequisites</span></span>

<span data-ttu-id="b19e4-126">다음은이 실습 랩을 완료 하려면 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-126">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="b19e4-127">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) 이상</span><span class="sxs-lookup"><span data-stu-id="b19e4-127">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="b19e4-128">설정</span><span class="sxs-lookup"><span data-stu-id="b19e4-128">Setup</span></span>

<span data-ttu-id="b19e4-129">이 실습 랩에서 연습을 실행 하려면 먼저 환경을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-129">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="b19e4-130">Windows 탐색기를 열고에 랩 찾아보기 **소스** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-130">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="b19e4-131">마우스 오른쪽 단추로 클릭 **Setup.cmd** 선택 **관리자 권한으로 실행** 환경을 구성 되며이 랩에 대 한 Visual Studio 코드 조각을 설치 하는 설치 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-131">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="b19e4-132">사용자 계정 컨트롤 대화 상자가 표시 되 면 계속 하려면 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-132">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="b19e4-133">설치 프로그램을 실행 하기 전에이 랩에 대 한 모든 종속성을 선택 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-133">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="b19e4-134">코드 조각을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b19e4-134">Using the Code Snippets</span></span>

<span data-ttu-id="b19e4-135">랩 문서를 통해 코드 블록을 삽입 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-135">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="b19e4-136">사용자 편의 위해이 코드의 대부분을 수동으로 추가할 필요가 없도록 하려면 Visual Studio 2013 내에서 액세스할 수 있는 Visual Studio 코드 조각으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-136">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="b19e4-137">각 연습에는 시작 솔루션 동반 되는 **시작** 개별적으로 각 연습에 따라 할 수 있는 작업의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-137">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="b19e4-138">주의 하십시오 연습 하는 동안 추가 된 코드 조각은 솔루션 시작이 항목에서 누락 되어 연습을 완료 될 때까지 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-138">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="b19e4-139">실행에 대 한 소스 코드에서 찾아볼 수 있습니다는 **끝** 해당 연습에서 단계를 완료 한 결과인 코드와 함께 Visual Studio 솔루션에 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-139">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="b19e4-140">이 실습 랩에서 진행할 때는 추가 도움이 필요한 경우 이러한 솔루션 가이드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-140">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>


* * *

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="b19e4-141">연습</span><span class="sxs-lookup"><span data-stu-id="b19e4-141">Exercises</span></span>

<span data-ttu-id="b19e4-142">이 실습 랩에서 다음 연습에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-142">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="b19e4-143">Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="b19e4-143">Creating a Web API</span></span>](#Exercise1)
2. [<span data-ttu-id="b19e4-144">SPA 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="b19e4-144">Creating a SPA Interface</span></span>](#Exercise2)

<span data-ttu-id="b19e4-145">예상 소요 시간: **60 분**</span><span class="sxs-lookup"><span data-stu-id="b19e4-145">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="b19e4-146">Visual Studio를 처음 시작 하면 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-146">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="b19e4-147">미리 정의 된 각 컬렉션 특정 개발 스타일에 맞게 설계 하 고 창 레이아웃, 편집기 동작, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-147">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="b19e4-148">이 랩의 절차를 사용 하는 경우 Visual Studio에서 지정 된 작업을 수행 하는 데 필요한 작업 설명에서 **일반 개발 설정** 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-148">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="b19e4-149">개발 환경에 대 한 서로 다른 설정 컬렉션을 선택 하면 고려해 야 하는 단계에 차이가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-149">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>


<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-web-api"></a><span data-ttu-id="b19e4-150">연습 1: Web API 만들기</span><span class="sxs-lookup"><span data-stu-id="b19e4-150">Exercise 1: Creating a Web API</span></span>

<span data-ttu-id="b19e4-151">SPA의 주요 부분 중 하나는 서비스 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-151">One of the key parts of a SPA is the service layer.</span></span> <span data-ttu-id="b19e4-152">UI 및 해당 호출에 대 한 응답에서 반환 데이터에서 보낸 Ajax 호출을 처리 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-152">It is responsible for processing the Ajax calls sent by the UI and returning data in response to that call.</span></span> <span data-ttu-id="b19e4-153">검색 된 데이터를 구문 분석 하 고 클라이언트에서 사용 하기 위해 컴퓨터가 읽을 수 있는 형식으로 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-153">The data retrieved should be presented in a machine-readable format in order to be parsed and consumed by the client.</span></span>

<span data-ttu-id="b19e4-154">Web API 프레임 워크는 ASP.NET 스택에서의 일부 이며은 쉽게 일반적으로 데이터 보내기 및 받기 JSON 또는 XML 형식 RESTful API를 통해 HTTP 서비스를 구현할 수 있도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-154">The Web API framework is part of the ASP.NET Stack and is designed to make it easy to implement HTTP services, generally sending and receiving JSON- or XML-formatted data through a RESTful API.</span></span> <span data-ttu-id="b19e4-155">이 연습에서는 들은 퀴즈 응용 프로그램을 호스트 하 고 백 엔드 서비스를 노출 하 고 ASP.NET Web API를 사용 하 여 퀴즈 데이터 유지를 구현 하려면 웹 사이트에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-155">In this exercise you will create the Web site to host the Geek Quiz application and then implement the back-end service to expose and persist the quiz data using ASP.NET Web API.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-the-initial-project-for-geek-quiz"></a><span data-ttu-id="b19e4-156">작업 1-들은 퀴즈에 대 한 초기 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="b19e4-156">Task 1 – Creating the Initial Project for Geek Quiz</span></span>

<span data-ttu-id="b19e4-157">이 작업에서는 먼저에 기반으로 하는 ASP.NET Web API를 지 원하는 새 ASP.NET MVC 프로젝트를 만드는 **One ASP.NET** 프로젝트 Visual Studio와 함께 제공 되는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-157">In this task you will start creating a new ASP.NET MVC project with support for ASP.NET Web API based on the **One ASP.NET** project type that comes with Visual Studio.</span></span> <span data-ttu-id="b19e4-158">**One ASP.NET** 모든 ASP.NET 기술을 통합 하 고는 혼합 하 고 원하는 대로 얻었으면이 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-158">**One ASP.NET** unifies all ASP.NET technologies and gives you the option to mix and match them as desired.</span></span> <span data-ttu-id="b19e4-159">Entity Framework 모델 클래스와 데이터베이스 initializator 퀴즈 질문을 삽입 하려면 다음 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-159">You will then add the Entity Framework's model classes and the database initializator to insert the quiz questions.</span></span>

1. <span data-ttu-id="b19e4-160">열기 **Visual Studio Express 2013 for Web** 선택 **파일 | 새 프로젝트...**  새 솔루션을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-160">Open **Visual Studio Express 2013 for Web** and select **File | New Project...** to start a new solution.</span></span>

    <span data-ttu-id="b19e4-161">![새 프로젝트를 만드는](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "새 프로젝트 만들기")</span><span class="sxs-lookup"><span data-stu-id="b19e4-161">![Creating a New Project](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "Creating a New Project")</span></span>

    <span data-ttu-id="b19e4-162">*새 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="b19e4-162">*Creating a New Project*</span></span>
2. <span data-ttu-id="b19e4-163">에 **새 프로젝트** 대화 상자에서 **ASP.NET 웹 응용 프로그램** 아래는 **Visual C# | 웹** 탭 합니다. 있는지 확인 **.NET Framework 4.5** 은 이름을 선택 하면 *GeekQuiz*, 선택는 **위치** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-163">In the **New Project** dialog box, select **ASP.NET Web Application** under the **Visual C# | Web** tab. Make sure **.NET Framework 4.5** is selected, name it *GeekQuiz*, choose a **Location** and click **OK**.</span></span>

    <span data-ttu-id="b19e4-164">![새 ASP.NET 웹 응용 프로그램 프로젝트를 만드는](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "새 ASP.NET 웹 응용 프로그램 프로젝트 만들기")</span><span class="sxs-lookup"><span data-stu-id="b19e4-164">![Creating a new ASP.NET Web Application project](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "Creating a new ASP.NET Web Application project")</span></span>

    <span data-ttu-id="b19e4-165">*새 ASP.NET 웹 응용 프로그램 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="b19e4-165">*Creating a new ASP.NET Web Application project*</span></span>
3. <span data-ttu-id="b19e4-166">에 **새 ASP.NET 프로젝트** 대화 상자는 **MVC** 템플릿과 선택은 **웹 API** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-166">In the **New ASP.NET Project** dialog box, select the **MVC** template and select the **Web API** option.</span></span> <span data-ttu-id="b19e4-167">또한 있는지 확인 하 고 **인증** 옵션을 설정 **개별 사용자 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-167">Also, make sure that the **Authentication** option is set to **Individual User Accounts**.</span></span> <span data-ttu-id="b19e4-168">계속하려면 **확인** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-168">Click **OK** to continue.</span></span>

    ![Web API 구성 요소를 포함 하 여 MVC 템플릿을 사용 하 여 새 프로젝트 만들기](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image3.png)

    <span data-ttu-id="b19e4-170">*Web API 구성 요소를 포함 하 여 MVC 템플릿을 사용 하 여 새 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="b19e4-170">*Creating a new project with the MVC template, including Web API components*</span></span>
4. <span data-ttu-id="b19e4-171">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **모델** 의 폴더는 **GeekQuiz** 프로젝트를 마우스 선택 **추가 | 기존 항목...** .</span><span class="sxs-lookup"><span data-stu-id="b19e4-171">In **Solution Explorer**, right-click the **Models** folder of the **GeekQuiz** project and select **Add | Existing Item...**.</span></span>

    <span data-ttu-id="b19e4-172">![기존 항목 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "기존 항목 추가")</span><span class="sxs-lookup"><span data-stu-id="b19e4-172">![Adding an existing item](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "Adding an existing item")</span></span>

    <span data-ttu-id="b19e4-173">*기존 항목 추가*</span><span class="sxs-lookup"><span data-stu-id="b19e4-173">*Adding an existing item*</span></span>
5. <span data-ttu-id="b19e4-174">에 **기존 항목 추가** 대화 상자에서 이동 하는 **소스/자산/모델** 폴더와 파일을 모두 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-174">In the **Add Existing Item** dialog box, navigate to the **Source/Assets/Models** folder and select all the files.</span></span> <span data-ttu-id="b19e4-175">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-175">Click **Add**.</span></span>

    <span data-ttu-id="b19e4-176">![모델 자산 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "모델 자산 추가")</span><span class="sxs-lookup"><span data-stu-id="b19e4-176">![Adding the model assets](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "Adding the model assets")</span></span>

    <span data-ttu-id="b19e4-177">*모델 자산 추가*</span><span class="sxs-lookup"><span data-stu-id="b19e4-177">*Adding the model assets*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b19e4-178">이러한 파일을 추가 하 여 데이터 모델, 엔터티 프레임 워크의 데이터베이스 컨텍스트 및 들은 퀴즈 응용 프로그램에 대 한 데이터베이스 이니셜라이저도 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-178">By adding these files, you are adding the data model, the Entity Framework's database context and the database initializer for the Geek Quiz application.</span></span>
    > 
    > <span data-ttu-id="b19e4-179">**Entity Framework (EF)** 관계형 저장소 스키마를 사용 하 여 직접 프로그래밍 하는 대신 개념적 응용 프로그램 모델을 사용 하 여 프로그래밍 하 여 데이터 액세스 응용 프로그램을 만들 수 있도록 하는 개체 관계형 매퍼 (ORM).</span><span class="sxs-lookup"><span data-stu-id="b19e4-179">**Entity Framework (EF)** is an object-relational mapper (ORM) that enables you to create data access applications by programming with a conceptual application model instead of programming directly using a relational storage schema.</span></span> <span data-ttu-id="b19e4-180">Entity Framework에 대 한 자세히 알아볼 수 있습니다 [여기](../../../entity-framework.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-180">You can learn more about Entity Framework [here](../../../entity-framework.md).</span></span>
    > 
    > <span data-ttu-id="b19e4-181">다음은 방금 추가한 클래스에 대 한 설명을입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-181">The following is a description of the classes you just added:</span></span>
    > 
    > - <span data-ttu-id="b19e4-182">**TriviaOption:** 퀴즈 질문에 연결 된 단일 옵션을 나타냅니다</span><span class="sxs-lookup"><span data-stu-id="b19e4-182">**TriviaOption:** represents a single option associated with a quiz question</span></span>
    > - <span data-ttu-id="b19e4-183">**TriviaQuestion:** 퀴즈 질문을 나타내며 연결된 옵션을 통해 노출 된 **옵션** 속성</span><span class="sxs-lookup"><span data-stu-id="b19e4-183">**TriviaQuestion:** represents a quiz question and exposes the associated options through the **Options** property</span></span>
    > - <span data-ttu-id="b19e4-184">**TriviaAnswer:** 퀴즈 질문에 대 한 응답으로 사용자가 선택한 옵션을 나타냅니다</span><span class="sxs-lookup"><span data-stu-id="b19e4-184">**TriviaAnswer:** represents the option selected by the user in response to a quiz question</span></span>
    > - <span data-ttu-id="b19e4-185">**TriviaContext:** 들은 퀴즈 응용 프로그램의 Entity Framework 데이터베이스 컨텍스트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-185">**TriviaContext:** represents the Entity Framework's database context of the Geek Quiz application.</span></span> <span data-ttu-id="b19e4-186">이 클래스에서 파생 **DContext** 노출 **DbSet** 위에서 설명한 엔터티 컬렉션을 나타내는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-186">This class derives from **DContext** and exposes **DbSet** properties that represent collections of the entities described above.</span></span>
    > - <span data-ttu-id="b19e4-187">**TriviaDatabaseInitializer:** 구현에 대 한 Entity Framework 이니셜라이저의 여 **TriviaContext** 클래스에서 상속 하는 **CreateDatabaseIfNotExists**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-187">**TriviaDatabaseInitializer:** the implementation of the Entity Framework initializer for the **TriviaContext** class which inherits from **CreateDatabaseIfNotExists**.</span></span> <span data-ttu-id="b19e4-188">에 지정 된 엔터티를 삽입 합니다.이 클래스의 기본 동작은 존재 하지 않는 경우에 데이터베이스를 만드는 것은 **시드** 메서드.</span><span class="sxs-lookup"><span data-stu-id="b19e4-188">The default behavior of this class is to create the database only if it does not exist, inserting the entities specified in the **Seed** method.</span></span>
6. <span data-ttu-id="b19e4-189">열기는 **Global.asax.cs** 파일을 다음 추가 문을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-189">Open the **Global.asax.cs** file and add the following using statement.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample1.cs)]
7. <span data-ttu-id="b19e4-190">맨 앞에 다음 코드를 추가 **응용 프로그램\_시작** 설정 하는 메서드는 **TriviaDatabaseInitializer** 데이터베이스 이니셜라이저로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-190">Add the following code at the beginning of the **Application\_Start** method to set the **TriviaDatabaseInitializer** as the database initializer.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample2.cs)]
8. <span data-ttu-id="b19e4-191">수정 된 **홈** 인증 된 사용자에 대 한 액세스를 제한 하는 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-191">Modify the **Home** controller to restrict access to authenticated users.</span></span> <span data-ttu-id="b19e4-192">이 위해 엽니다는 **HomeController.cs** 내 파일의 **컨트롤러** 폴더 추가 **Authorize** 특성을 **HomeController**클래스 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-192">To do this, open the **HomeController.cs** file inside the **Controllers** folder and add the **Authorize** attribute to the **HomeController** class definition.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample3.cs)]

    > [!NOTE]
    > <span data-ttu-id="b19e4-193">**Authorize** 를 사용자가 인증 하는 경우 확인을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-193">The **Authorize** filter checks to see if the user is authenticated.</span></span> <span data-ttu-id="b19e4-194">사용자 인증 되지 않은 경우 다음 작업을 호출 하지 않고 HTTP 상태 코드 401 (권한 없음)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-194">If the user is not authenticated, it returns HTTP status code 401 (Unauthorized) without invoking the action.</span></span> <span data-ttu-id="b19e4-195">컨트롤러 수준에서 전역적으로 또는 개별 작업 수준에서 필터를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-195">You can apply the filter globally, at the controller level, or at the level of individual actions.</span></span>
9. <span data-ttu-id="b19e4-196">이제 브랜딩 하 고 웹 페이지의 레이아웃을 사용자 지정할는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-196">You will now customize the layout of the web pages and the branding.</span></span> <span data-ttu-id="b19e4-197">이 작업을 수행 하려면 엽니다는  **\_Layout.cshtml** 내 파일의 **보기 | 공유** 폴더의 내용을 업데이트 하 고는 **&lt;제목&gt;** 대체 하 여 요소 *내 ASP.NET 응용 프로그램* 와 *들은 퀴즈* .</span><span class="sxs-lookup"><span data-stu-id="b19e4-197">To do this, open the **\_Layout.cshtml** file inside the **Views | Shared** folder and update the content of the **&lt;title&gt;** element by replacing *My ASP.NET Application* with *Geek Quiz*.</span></span>

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample4.cshtml)]
10. <span data-ttu-id="b19e4-198">같은 파일에서 제거 하 여 탐색 모음을 업데이트는 *에 대 한* 및 *연락처* 링크 및 이름 바꾸기는 *홈* 연결할 *재생*합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-198">In the same file, update the navigation bar by removing the *About* and *Contact* links and renaming the *Home* link to *Play*.</span></span> <span data-ttu-id="b19e4-199">이름도 변경는 *응용 프로그램 이름* 연결할 *들은 퀴즈*합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-199">Additionally, rename the *Application name* link to *Geek Quiz*.</span></span> <span data-ttu-id="b19e4-200">HTML 탐색 모음에 다음 코드와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-200">The HTML for the navigation bar should look like the following code.</span></span>

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample5.cshtml)]
11. <span data-ttu-id="b19e4-201">레이아웃 페이지의 바닥글을 대체 하 여 업데이트 *내 ASP.NET 응용 프로그램* 와 *들은 퀴즈*합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-201">Update the footer of the layout page by replacing *My ASP.NET Application* with *Geek Quiz*.</span></span> <span data-ttu-id="b19e4-202">이 위해의 내용을 대체는 **&lt;바닥글&gt;** 요소 강조 표시 된 다음 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-202">To do this, replace the content of the **&lt;footer&gt;** element with the following highlighted code.</span></span>

    [!code-html[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample6.html)]

<a id="Ex1Task2"></a>
#### <a name="task-2--creating-the-triviacontroller-web-api"></a><span data-ttu-id="b19e4-203">작업 2-TriviaController 웹 API 만들기</span><span class="sxs-lookup"><span data-stu-id="b19e4-203">Task 2 – Creating the TriviaController Web API</span></span>

<span data-ttu-id="b19e4-204">이전 태스크에서 웹 응용 프로그램 들은 퀴즈의 초기 구조를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-204">In the previous task, you created the initial structure of the Geek Quiz web application.</span></span> <span data-ttu-id="b19e4-205">이제 퀴즈 데이터 모델과 상호 작용 하 고 다음 작업을 노출 하는 간단한 웹 API 서비스를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-205">You will now build a simple Web API service that interacts with the quiz data model and exposes the following actions:</span></span>

- <span data-ttu-id="b19e4-206">**GET/api/trivia**: 인증 된 사용자가 대답 해야 할 퀴즈 목록에서 다음 질문을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-206">**GET /api/trivia**: Retrieves the next question from the quiz list to be answered by the authenticated user.</span></span>
- <span data-ttu-id="b19e4-207">**POST/api/trivia**: 인증 된 사용자가 지정한 퀴즈 답변을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-207">**POST /api/trivia**: Stores the quiz answer specified by the authenticated user.</span></span>

<span data-ttu-id="b19e4-208">Web API 컨트롤러 클래스에 대 한 기준을 만드는 데 Visual Studio에서 제공 하는 ASP.NET 스 캐 폴딩 도구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-208">You will use the ASP.NET Scaffolding tools provided by Visual Studio to create the baseline for the Web API controller class.</span></span>

1. <span data-ttu-id="b19e4-209">열기는 **WebApiConfig.cs** 내 파일의 **앱\_시작** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-209">Open the **WebApiConfig.cs** file inside the **App\_Start** folder.</span></span> <span data-ttu-id="b19e4-210">이 파일에는 경로 Web API 컨트롤러 작업에 매핑하는 방식을 같은 웹 API 서비스의 구성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-210">This file defines the configuration of the Web API service, like how routes are mapped to Web API controller actions.</span></span>
2. <span data-ttu-id="b19e4-211">다음 추가 문을 사용 하 여 파일의 시작 부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-211">Add the following using statement at the beginning of the file.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample7.cs)]
3. <span data-ttu-id="b19e4-212">다음 강조 표시 된 코드를 추가 하는 **등록** 웹 API 작업 메서드에 의해 검색 되는 JSON 데이터에 대 한 포맷터를 전역적으로 구성 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="b19e4-212">Add the following highlighted code to the **Register** method to globally configure the formatter for the JSON data retrieved by the Web API action methods.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample8.cs)]

    > [!NOTE]
    > <span data-ttu-id="b19e4-213">**CamelCasePropertyNamesContractResolver** 속성 이름을 자동으로 변환 *카멜식* 경우 JavaScript에서 속성 이름에 대 한 일반 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-213">The **CamelCasePropertyNamesContractResolver** automatically converts property names to *camel* case, which is the general convention for property names in JavaScript.</span></span>
4. <span data-ttu-id="b19e4-214">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **컨트롤러** 의 폴더는 **GeekQuiz** 프로젝트를 마우스 선택 **추가 | 새 스 캐 폴드 항목...** .</span><span class="sxs-lookup"><span data-stu-id="b19e4-214">In **Solution Explorer**, right-click the **Controllers** folder of the **GeekQuiz** project and select **Add | New Scaffolded Item...**.</span></span>

    <span data-ttu-id="b19e4-215">![새 스 캐 폴드 항목을 만드는](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "스 캐 폴드 새 항목 만들기")</span><span class="sxs-lookup"><span data-stu-id="b19e4-215">![Creating a new scaffolded item](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "Creating a new scaffolded item")</span></span>

    <span data-ttu-id="b19e4-216">*새 스 캐 폴드 항목 만들기*</span><span class="sxs-lookup"><span data-stu-id="b19e4-216">*Creating a new scaffolded item*</span></span>
5. <span data-ttu-id="b19e4-217">에 **스 캐 폴드를 추가** 대화 상자에서 다음 사항을 확인는 **일반적인** 왼쪽된 창에서 노드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-217">In the **Add Scaffold** dialog box, make sure that the **Common** node is selected in the left pane.</span></span> <span data-ttu-id="b19e4-218">그런 다음 선택에서 **Web API 2 컨트롤러-비어 있지** 클릭 확인 하 고 가운데 창에서 템플릿을 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-218">Then, select the **Web API 2 Controller - Empty** template in the center pane and click **Add**.</span></span>

    <span data-ttu-id="b19e4-219">![Web API 2 컨트롤러 빈 템플릿을 선택 하면](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "Web API 2 컨트롤러 빈 템플릿 선택")</span><span class="sxs-lookup"><span data-stu-id="b19e4-219">![Selecting the Web API 2 Controller Empty template](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "Selecting the Web API 2 Controller Empty template")</span></span>

    <span data-ttu-id="b19e4-220">*Web API 2 컨트롤러 빈 템플릿 선택*</span><span class="sxs-lookup"><span data-stu-id="b19e4-220">*Selecting the Web API 2 Controller Empty template*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b19e4-221">**ASP.NET 스 캐 폴딩** 는 ASP.NET 웹 응용 프로그램에 대 한 코드 생성 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-221">**ASP.NET Scaffolding** is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="b19e4-222">Visual Studio 2013 MVC 및 Web API 프로젝트에 대 한 사전 설치 된 코드 생성기를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-222">Visual Studio 2013 includes pre-installed code generators for MVC and Web API projects.</span></span> <span data-ttu-id="b19e4-223">신속 하 게 표준 데이터 작업을 개발 하는 데 필요한 시간을 줄이기 위해 데이터 모델과 상호 작용 하는 코드를 추가 하려면 프로젝트에 스 캐 폴딩을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-223">You should use scaffolding in your project when you want to quickly add code that interacts with data models in order to reduce the amount of time required to develop standard data operations.</span></span>
    > 
    > <span data-ttu-id="b19e4-224">스 캐 폴딩 프로세스는 또한 모든 필요한 종속 프로젝트에 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-224">The scaffolding process also ensures that all the required dependencies are installed in the project.</span></span> <span data-ttu-id="b19e4-225">예를 들어 빈 ASP.NET 프로젝트 시작 다음 스 캐 폴딩을 사용 하 여 Web API 컨트롤러를 추가 하는 경우 필요한 웹 API NuGet 패키지와 참조를 프로젝트에 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-225">For example, if you start with an empty ASP.NET project and then use scaffolding to add a Web API controller, the required Web API NuGet packages and references are added to your project automatically.</span></span>
6. <span data-ttu-id="b19e4-226">에 **컨트롤러 추가** 대화 상자에서 *TriviaController* 에 **컨트롤러 이름** 텍스트 상자 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-226">In the **Add Controller** dialog box, type *TriviaController* in the **Controller name** text box and click **Add**.</span></span>

    <span data-ttu-id="b19e4-227">![Trivia 컨트롤러 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "Trivia 컨트롤러 추가")</span><span class="sxs-lookup"><span data-stu-id="b19e4-227">![Adding the Trivia Controller](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "Adding the Trivia Controller")</span></span>

    <span data-ttu-id="b19e4-228">*Trivia 컨트롤러 추가*</span><span class="sxs-lookup"><span data-stu-id="b19e4-228">*Adding the Trivia Controller*</span></span>
7. <span data-ttu-id="b19e4-229">**TriviaController.cs** 파일에 추가 됩니다는 **컨트롤러** 의 폴더는 **GeekQuiz** 비어 있는 포함 된 프로젝트 **TriviaController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-229">The **TriviaController.cs** file is then added to the **Controllers** folder of the **GeekQuiz** project, containing an empty **TriviaController** class.</span></span> <span data-ttu-id="b19e4-230">다음 추가 문을 사용 하 여 파일의 시작 부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-230">Add the following using statements at the beginning of the file.</span></span>

    <span data-ttu-id="b19e4-231">(코드 조각- *AspNetWebApiSpa e x-1-TriviaControllerUsings*)</span><span class="sxs-lookup"><span data-stu-id="b19e4-231">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerUsings*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample9.cs)]
8. <span data-ttu-id="b19e4-232">맨 앞에 다음 코드를 추가 **TriviaController** 정의 초기화 및 삭제 하는 클래스는 **TriviaContext** 컨트롤러의 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="b19e4-232">Add the following code at the beginning of the **TriviaController** class to define, initialize and dispose the **TriviaContext** instance in the controller.</span></span>

    <span data-ttu-id="b19e4-233">(코드 조각- *AspNetWebApiSpa e x-1-TriviaControllerContext*)</span><span class="sxs-lookup"><span data-stu-id="b19e4-233">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerContext*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample10.cs)]

    > [!NOTE]
    > <span data-ttu-id="b19e4-234">**Dispose** 방식의 **TriviaController** 호출는 **Dispose** 의 메서드는 **TriviaContext** 인스턴스를 사용 하면 모든 컨텍스트 개체에서 사용 하는 리소스가 해제 때는 **TriviaContext** 인스턴스를 삭제 하거나 가비지 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-234">The **Dispose** method of **TriviaController** invokes the **Dispose** method of the **TriviaContext** instance, which ensures that all the resources used by the context object are released when the **TriviaContext** instance is disposed or garbage-collected.</span></span> <span data-ttu-id="b19e4-235">Entity Framework에서 연 모든 데이터베이스 연결을 닫는 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-235">This includes closing all database connections opened by Entity Framework.</span></span>
9. <span data-ttu-id="b19e4-236">끝에 다음 도우미 메서드를 추가 합니다.는 **TriviaController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-236">Add the following helper method at the end of the **TriviaController** class.</span></span> <span data-ttu-id="b19e4-237">이 메서드는 지정된 된 사용자가 대답 해야 할 데이터베이스에서 다음 질문의 퀴즈를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-237">This method retrieves the following quiz question from the database to be answered by the specified user.</span></span>

    <span data-ttu-id="b19e4-238">(코드 조각- *AspNetWebApiSpa e x-1-TriviaControllerNextQuestion*)</span><span class="sxs-lookup"><span data-stu-id="b19e4-238">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerNextQuestion*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample11.cs)]
10. <span data-ttu-id="b19e4-239">다음 추가 **가져오기** 동작 메서드의 **TriviaController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-239">Add the following **Get** action method to the **TriviaController** class.</span></span> <span data-ttu-id="b19e4-240">이 작업 메서드를 호출는 **NextQuestionAsync** 인증된 된 사용자에 대 한 다음 질문을 검색 하는 이전 단계에 정의 된 도우미 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-240">This action method calls the **NextQuestionAsync** helper method defined in the previous step to retrieve the next question for the authenticated user.</span></span>

    <span data-ttu-id="b19e4-241">(코드 조각- *AspNetWebApiSpa e x-1-TriviaControllerGetAction*)</span><span class="sxs-lookup"><span data-stu-id="b19e4-241">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerGetAction*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample12.cs)]
11. <span data-ttu-id="b19e4-242">끝에 다음 도우미 메서드를 추가 합니다.는 **TriviaController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-242">Add the following helper method at the end of the **TriviaController** class.</span></span> <span data-ttu-id="b19e4-243">이 메서드는 데이터베이스에 지정한 응답을 저장 하 고 답이 맞으면 여부를 나타내는 부울 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-243">This method stores the specified answer in the database and returns a Boolean value indicating whether or not the answer is correct.</span></span>

    <span data-ttu-id="b19e4-244">(코드 조각- *AspNetWebApiSpa e x-1-TriviaControllerStoreAsync*)</span><span class="sxs-lookup"><span data-stu-id="b19e4-244">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerStoreAsync*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample13.cs)]
12. <span data-ttu-id="b19e4-245">다음 추가 **Post** 동작 메서드의 **TriviaController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-245">Add the following **Post** action method to the **TriviaController** class.</span></span> <span data-ttu-id="b19e4-246">이 동작 메서드에 연결 인증 된 사용자 및 호출에 대 한 대답은 **StoreAsync** 도우미 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-246">This action method associates the answer to the authenticated user and calls the **StoreAsync** helper method.</span></span> <span data-ttu-id="b19e4-247">그런 다음 도우미 메서드에 의해 반환 된 부울 값으로 응답을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-247">Then, it sends a response with the Boolean value returned by the helper method.</span></span>

    <span data-ttu-id="b19e4-248">(코드 조각- *AspNetWebApiSpa e x-1-TriviaControllerPostAction*)</span><span class="sxs-lookup"><span data-stu-id="b19e4-248">(Code Snippet - *AspNetWebApiSpa - Ex1 - TriviaControllerPostAction*)</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample14.cs)]
13. <span data-ttu-id="b19e4-249">수정 Web API 컨트롤러를 추가 하 여 인증 된 사용자 에게만 액세스를 제한 하는 **Authorize** 특성을 **TriviaController** 클래스 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-249">Modify the Web API controller to restrict access to authenticated users by adding the **Authorize** attribute to the **TriviaController** class definition.</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample15.cs)]

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="b19e4-250">작업 3 – 솔루션 실행</span><span class="sxs-lookup"><span data-stu-id="b19e4-250">Task 3 – Running the Solution</span></span>

<span data-ttu-id="b19e4-251">이 작업에서는 이전 태스크에서 작성 된 웹 API 서비스가 예상 대로 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-251">In this task you will verify that the Web API service you built in the previous task is working as expected.</span></span> <span data-ttu-id="b19e4-252">Internet Explorer를 사용 합니다 **F12 개발자 도구** 네트워크 트래픽을 캡처하고 웹 API 서비스의 전체 응답을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-252">You will use the Internet Explorer **F12 Developer Tools** to capture the network traffic and inspect the full response from the Web API service.</span></span>

> [!NOTE]
> <span data-ttu-id="b19e4-253">다음 사항을 확인 **Internet Explorer** 에서 선택한는 **시작** 단추 Visual Studio 도구 모음에 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-253">Make sure that **Internet Explorer** is selected in the **Start** button located on the Visual Studio toolbar.</span></span>
> 
> ![Internet Explorer 옵션](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image9.png)


1. <span data-ttu-id="b19e4-255">키를 눌러 **F5** 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-255">Press **F5** to run the solution.</span></span> <span data-ttu-id="b19e4-256">**로그인** 페이지가 브라우저에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-256">The **Log in** page should appear in the browser.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b19e4-257">응용 프로그램이 시작 되 면 기본 MVC 경로 트리거된에 매핑되는 기본적으로는 **인덱스** 의 동작에서 **HomeController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-257">When the application starts, the default MVC route is triggered, which by default is mapped to the **Index** action of the **HomeController** class.</span></span> <span data-ttu-id="b19e4-258">이후 **HomeController** 인증 된 사용자 에게만 부여 됩니다 (해당 클래스와 데코 레이트 된 기억는 **Authorize** 연습 1의 특성) 되어 있으므로 사용자가 인증 아직 응용 프로그램 로그인 페이지에 원래 요청을 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-258">Since **HomeController** is restricted to authenticated users (remember that you decorated that class with the **Authorize** attribute in Exercise 1) and there is no user authenticated yet, the application redirects the original request to the log in page.</span></span>

    <span data-ttu-id="b19e4-259">![솔루션을 실행](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "솔루션 실행")</span><span class="sxs-lookup"><span data-stu-id="b19e4-259">![Running the solution](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "Running the solution")</span></span>

    <span data-ttu-id="b19e4-260">*솔루션을 실행*</span><span class="sxs-lookup"><span data-stu-id="b19e4-260">*Running the solution*</span></span>
2. <span data-ttu-id="b19e4-261">클릭 **등록** 새 사용자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-261">Click **Register** to create a new user.</span></span>

    <span data-ttu-id="b19e4-262">![새 사용자 등록](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "새 사용자를 등록 하는 중")</span><span class="sxs-lookup"><span data-stu-id="b19e4-262">![Registering a new user](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "Registering a new user")</span></span>

    <span data-ttu-id="b19e4-263">*새 사용자를 등록 하는 중*</span><span class="sxs-lookup"><span data-stu-id="b19e4-263">*Registering a new user*</span></span>
3. <span data-ttu-id="b19e4-264">에 **등록** 페이지에서 입력 한 **사용자 이름** 및 **암호**, 클릭 하 고 **등록**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-264">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    <span data-ttu-id="b19e4-265">![등록 페이지](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "등록 페이지")</span><span class="sxs-lookup"><span data-stu-id="b19e4-265">![Register page](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "Register page")</span></span>

    <span data-ttu-id="b19e4-266">*등록 페이지*</span><span class="sxs-lookup"><span data-stu-id="b19e4-266">*Register page*</span></span>
4. <span data-ttu-id="b19e4-267">응용 프로그램에서 새 계정을 등록 하 고 사용자가 인증 되 고 홈 페이지로 다시 리디렉션되 며 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-267">The application registers the new account and the user is authenticated and redirected back to the home page.</span></span>

    <span data-ttu-id="b19e4-268">![사용자가 인증](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "인증 된 사용자")</span><span class="sxs-lookup"><span data-stu-id="b19e4-268">![User is authenticated](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "User authenticated")</span></span>

    <span data-ttu-id="b19e4-269">*사용자가 인증*</span><span class="sxs-lookup"><span data-stu-id="b19e4-269">*User is authenticated*</span></span>
5. <span data-ttu-id="b19e4-270">키를 눌러 브라우저에서 **F12** 열려는 **개발자 도구** 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-270">In the browser, press **F12** to open the **Developer Tools** panel.</span></span> <span data-ttu-id="b19e4-271">키를 누릅니다 **CTRL + 4** 하거나 클릭 하 고 **네트워크** 네트워크 트래픽 캡처를 시작 하 고 녹색 화살표 단추 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-271">Press **CTRL + 4** or click the **Network** icon, and then click the green arrow button to begin capturing network traffic.</span></span>

    <span data-ttu-id="b19e4-272">![웹 API 네트워크 캡처를 시작](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "Web API 시작 네트워크 캡처")</span><span class="sxs-lookup"><span data-stu-id="b19e4-272">![Initiating Web API network capture](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "Initiating Web API network capture")</span></span>

    <span data-ttu-id="b19e4-273">*웹 API 네트워크 캡처를 시작합니다.*</span><span class="sxs-lookup"><span data-stu-id="b19e4-273">*Initiating Web API network capture*</span></span>
6. <span data-ttu-id="b19e4-274">추가 **api/trivia** 브라우저의 주소 표시줄에 URL을 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-274">Append **api/trivia** to the URL in the browser's address bar.</span></span> <span data-ttu-id="b19e4-275">응답의 세부 정보를 이제 검사 하는 **가져오기** 의 동작 메서드에 **TriviaController**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-275">You will now inspect the details of the response from the **Get** action method in **TriviaController**.</span></span>

    <span data-ttu-id="b19e4-276">![웹 API를 통해 다음 질문 데이터 검색](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "웹 API를 통해 다음 질문 데이터 검색")</span><span class="sxs-lookup"><span data-stu-id="b19e4-276">![Retrieving the next question data through Web API](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "Retrieving the next question data through Web API")</span></span>

    <span data-ttu-id="b19e4-277">*웹 API를 통해 다음 질문 데이터 검색*</span><span class="sxs-lookup"><span data-stu-id="b19e4-277">*Retrieving the next question data through Web API*</span></span>

    > [!NOTE]
    > <span data-ttu-id="b19e4-278">다운로드를 완료 한 후에 다운로드 한 파일 작업으로 설정할 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-278">Once the download finishes, you will be prompted to make an action with the downloaded file.</span></span> <span data-ttu-id="b19e4-279">대화 상자를 개발자 도구 창을 통해 응답 콘텐츠를 볼 수 있도록 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-279">Leave the dialog box open in order to be able to watch the response content through the Developers Tool window.</span></span>
7. <span data-ttu-id="b19e4-280">이제는 응답의 본문을 조사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-280">Now you will inspect the body of the response.</span></span> <span data-ttu-id="b19e4-281">이 작업을 수행 하려면는 **세부 정보** 탭을 클릭 한 다음 **응답 본문**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-281">To do this, click the **Details** tab and then click **Response body**.</span></span> <span data-ttu-id="b19e4-282">다운로드 한 데이터 속성을 가진 개체를 확인할 수 있습니다 **옵션** (의 목록인 **TriviaOption** 개체), **id** 및 **제목** 에 해당 하는 **TriviaQuestion** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-282">You can check that the downloaded data is an object with the properties **options** (which is a list of **TriviaOption** objects), **id** and **title** that correspond to the **TriviaQuestion** class.</span></span>

    <span data-ttu-id="b19e4-283">![웹 API 응답 본문을 보기](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "웹 API 응답 본문을 보기")</span><span class="sxs-lookup"><span data-stu-id="b19e4-283">![Viewing the Web API Response Body](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "Viewing the Web API Response Body")</span></span>

    <span data-ttu-id="b19e4-284">*보기 웹 API 응답 본문*</span><span class="sxs-lookup"><span data-stu-id="b19e4-284">*Viewing Web API Response Body*</span></span>
8. <span data-ttu-id="b19e4-285">Visual Studio 및 키를 눌러로 돌아가서 **SHIFT + f 5를 눌러** 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-285">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-creating-the-spa-interface"></a><span data-ttu-id="b19e4-286">연습 2: SPA 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="b19e4-286">Exercise 2: Creating the SPA Interface</span></span>

<span data-ttu-id="b19e4-287">이 연습에서는 먼저 빌드합니다 웹 프런트 엔드 부분 들은 퀴즈를 사용 하 여 단일 페이지 응용 프로그램 상호 작용에 중점을 두기 **AngularJS**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-287">In this exercise you will first build the web front-end portion of Geek Quiz, focusing on the Single-Page Application interaction using **AngularJS**.</span></span> <span data-ttu-id="b19e4-288">다음 컨텍스트 전환 질문 중 하나에서 다음 전환할 때의 시각적 효과 고 풍부한 애니메이션을 수행 하기 위한 CSS3 만들어 사용자 환경을 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-288">You will then enhance the user experience with CSS3 to perform rich animations and provide a visual effect of context switching when transitioning from one question to the next.</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-the-spa-interface-using-angularjs"></a><span data-ttu-id="b19e4-289">작업 1 – AngularJS를 사용 하 여 SPA 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="b19e4-289">Task 1 – Creating the SPA Interface Using AngularJS</span></span>

<span data-ttu-id="b19e4-290">이 작업을 사용 하 여 **AngularJS** 들은 퀴즈 응용 프로그램의 클라이언트 쪽을 구현 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-290">In this task you will use **AngularJS** to implement the client side of the Geek Quiz application.</span></span> <span data-ttu-id="b19e4-291">**AngularJS** 브라우저 기반 응용 프로그램을 보완 하는 오픈 소스 JavaScript 프레임 워크는 *모델-뷰-컨트롤러* (MVC) 기능을 모두 개발을 촉진 하 고 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-291">**AngularJS** is an open-source JavaScript framework that augments browser-based applications with *Model-View-Controller* (MVC) capability, facilitating both development and testing.</span></span>

<span data-ttu-id="b19e4-292">Visual Studio의 패키지 관리자 콘솔에서 AngularJS를 설치 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-292">You will start by installing AngularJS from Visual Studio's Package Manager Console.</span></span> <span data-ttu-id="b19e4-293">그런 다음 들은 퀴즈 응용 프로그램 및 퀴즈 질문 및 답변은 AngularJS 템플릿 엔진을 사용 하 여 렌더링 하는 보기의 동작을 제공 하도록 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-293">Then, you will create the controller to provide the behavior of the Geek Quiz app and the view to render the quiz questions and answers using the AngularJS template engine.</span></span>

> [!NOTE]
> <span data-ttu-id="b19e4-294">AngularJS에 대 한 자세한 내용은를 참조 [ [ http://angularjs.org/ ](http://angularjs.org/) ](http://angularjs.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-294">For more information about AngularJS, refer to [[http://angularjs.org/](http://angularjs.org/)](http://angularjs.org/).</span></span>


1. <span data-ttu-id="b19e4-295">열고 **Visual Studio Express 2013 for Web** 엽니다는 **GeekQuiz.sln** 솔루션에 있는 **소스/e x 2-CreatingASPAInterface/시작** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-295">Open **Visual Studio Express 2013 for Web** and open the **GeekQuiz.sln** solution located in the **Source/Ex2-CreatingASPAInterface/Begin** folder.</span></span> <span data-ttu-id="b19e4-296">또는 계속할 수 있습니다 솔루션으로, 이전 연습에서 가져올 있음을.</span><span class="sxs-lookup"><span data-stu-id="b19e4-296">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="b19e4-297">열기는 **패키지 관리자 콘솔** 에서 **도구** | **라이브러리 패키지 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-297">Open the **Package Manager Console** from **Tools** | **Library Package Manager**.</span></span> <span data-ttu-id="b19e4-298">설치 하려면 다음 명령을 입력 하 고 **AngularJS.Core** NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-298">Type the following command to install the **AngularJS.Core** NuGet package.</span></span>

    [!code-powershell[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample16.ps1)]
3. <span data-ttu-id="b19e4-299">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **스크립트** 의 폴더는 **GeekQuiz** 프로젝트를 마우스 선택 **추가 | 새 폴더**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-299">In **Solution Explorer**, right-click the **Scripts** folder of the **GeekQuiz** project and select **Add | New Folder**.</span></span> <span data-ttu-id="b19e4-300">폴더 이름을 **앱** 누릅니다 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-300">Name the folder **app** and press **Enter**.</span></span>
4. <span data-ttu-id="b19e4-301">마우스 오른쪽 단추로 클릭는 **앱** 폴더 바로 전에 만들고 선택 **추가 | JavaScript 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-301">Right-click the **app** folder you just created and select **Add | JavaScript File**.</span></span>

    ![새 JavaScript 파일 만들기](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image17.png)

    <span data-ttu-id="b19e4-303">*새 JavaScript 파일 만들기*</span><span class="sxs-lookup"><span data-stu-id="b19e4-303">*Creating a new JavaScript file*</span></span>
5. <span data-ttu-id="b19e4-304">에 **항목에 대 한 이름 지정** 대화 상자에서 *퀴즈 컨트롤러* 에 **항목 이름** 텍스트 상자 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-304">In the **Specify Name for Item** dialog box, type *quiz-controller* in the **Item name** text box and click **OK**.</span></span>

    ![새 JavaScript 파일 이름 지정](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image18.png)

    <span data-ttu-id="b19e4-306">*새 JavaScript 파일 이름 지정*</span><span class="sxs-lookup"><span data-stu-id="b19e4-306">*Naming the new JavaScript file*</span></span>
6. <span data-ttu-id="b19e4-307">에 **퀴즈 controller.js** 파일에서 다음 코드를 선언 하 고 초기화 AngularJS 추가 **QuizCtrl** 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-307">In the **quiz-controller.js** file, add the following code to declare and initialize the AngularJS **QuizCtrl** controller.</span></span>

    <span data-ttu-id="b19e4-308">(코드 조각- *AspNetWebApiSpa-e x 2-AngularQuizController*)</span><span class="sxs-lookup"><span data-stu-id="b19e4-308">(Code Snippet - *AspNetWebApiSpa - Ex2 - AngularQuizController*)</span></span>

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample17.js)]

    > [!NOTE]
    > <span data-ttu-id="b19e4-309">생성자 함수는 **QuizCtrl** 컨트롤러에서는 라는 injectable 매개 변수는 **$scope**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-309">The constructor function of the **QuizCtrl** controller expects an injectable parameter named **$scope**.</span></span> <span data-ttu-id="b19e4-310">범위의 초기 상태를 설정 해야 생성자 함수에서 속성을 연결 하 여는 **$scope** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-310">The initial state of the scope should be set up in the constructor function by attaching properties to the **$scope** object.</span></span> <span data-ttu-id="b19e4-311">속성 포함 되는 **뷰 모델**, 하는 컨트롤러를 등록 하는 경우 서식 파일에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-311">The properties contain the **view model**, and will be accessible to the template when the controller is registered.</span></span>
    > 
    > <span data-ttu-id="b19e4-312">**QuizCtrl** 컨트롤러가 라는 모듈 내에 정의 되어 **QuizApp**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-312">The **QuizCtrl** controller is defined inside a module named **QuizApp**.</span></span> <span data-ttu-id="b19e4-313">모듈은 수 있는 작업 단위를 개별 구성 요소로 분해 합니다. 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-313">Modules are units of work that let you break your application into separate components.</span></span> <span data-ttu-id="b19e4-314">모듈을 사용 하는 주요 이점은 코드 이해 하기 쉬우며 이며 단위 테스트, 재사용 및 유지 관리를 용이 하 게 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-314">The main advantages of using modules is that the code is easier to understand and facilitates unit testing, reusability and maintainability.</span></span>
7. <span data-ttu-id="b19e4-315">이제 보기에서 트리거되는 이벤트에 대응 하기 위해 범위에 동작을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-315">You will now add behavior to the scope in order to react to events triggered from the view.</span></span> <span data-ttu-id="b19e4-316">끝에 다음 코드를 추가 **QuizCtrl** 정의 하는 컨트롤러는 **nextQuestion** 함수는 **$scope** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-316">Add the following code at the end of the **QuizCtrl** controller to define the **nextQuestion** function in the **$scope** object.</span></span>

    <span data-ttu-id="b19e4-317">(코드 조각- *AspNetWebApiSpa-e x 2-AngularQuizControllerNextQuestion*)</span><span class="sxs-lookup"><span data-stu-id="b19e4-317">(Code Snippet - *AspNetWebApiSpa - Ex2 - AngularQuizControllerNextQuestion*)</span></span>

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample18.js)]

    > [!NOTE]
    > <span data-ttu-id="b19e4-318">이 함수에서 다음 질문을 검색 합니다.는 **퀴즈** Web API 이전 연습에서 만든 및 질문 데이터를 연결 된 **$scope** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-318">This function retrieves the next question from the **Trivia** Web API created in the previous exercise and attaches the question data to the **$scope** object.</span></span>
8. <span data-ttu-id="b19e4-319">끝에 다음 코드를 삽입는 **QuizCtrl** 정의 하는 컨트롤러는 **sendAnswer** 함수는 **$scope** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-319">Insert the following code at the end of the **QuizCtrl** controller to define the **sendAnswer** function in the **$scope** object.</span></span>

    <span data-ttu-id="b19e4-320">(코드 조각- *AspNetWebApiSpa-e x 2-AngularQuizControllerSendAnswer*)</span><span class="sxs-lookup"><span data-stu-id="b19e4-320">(Code Snippet - *AspNetWebApiSpa - Ex2 - AngularQuizControllerSendAnswer*)</span></span>

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample19.js)]

    > [!NOTE]
    > <span data-ttu-id="b19e4-321">이 함수를 사용자가 선택한 응답을 보냅니다는 **퀴즈** Web API에서-즉, 대답 한 경우 올바른 여부-결과 저장 하는 **$scope** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-321">This function sends the answer selected by the user to the **Trivia** Web API and stores the result –i.e. if the answer is correct or not– in the **$scope** object.</span></span>
    > 
    > <span data-ttu-id="b19e4-322">**nextQuestion** 및 **sendAnswer** 위에서 함수는 AngularJS를 사용 하 여 **$http** 는 XMLHttpRequest 통해 웹 API와의 통신을 추상화 하는 개체 브라우저에서 JavaScript 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-322">The **nextQuestion** and **sendAnswer** functions from above use the AngularJS **$http** object to abstract the communication with the Web API via the XMLHttpRequest JavaScript object from the browser.</span></span> <span data-ttu-id="b19e4-323">AngularJS 더 높은 수준의 RESTful Api를 통해 리소스에 대해 CRUD 작업을 수행 하는 추상화를 제공 하는 다른 서비스를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-323">AngularJS supports another service that brings a higher level of abstraction to perform CRUD operations against a resource through RESTful APIs.</span></span> <span data-ttu-id="b19e4-324">AngularJS **$resource** 개체의 상호 작용 하지 않고도 높은 수준의 동작을 제공 하는 작업 메서드는 **$http** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-324">The AngularJS **$resource** object has action methods which provide high-level behaviors without the need to interact with the **$http** object.</span></span> <span data-ttu-id="b19e4-325">사용 하는 것이 좋습니다는 **$resource** CRUD 모델을 필요로 하는 시나리오에서 개체 (전경 정보 참조는 [$resource 설명서](https://docs.angularjs.org/api/ngResource/service/$resource)).</span><span class="sxs-lookup"><span data-stu-id="b19e4-325">Consider using the **$resource** object in scenarios that requires the CRUD model (fore information, see the [$resource documentation](https://docs.angularjs.org/api/ngResource/service/$resource)).</span></span>
9. <span data-ttu-id="b19e4-326">다음 단계에서는 퀴즈에 대 한 뷰를 정의 하는 AngularJS 템플릿입니다를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-326">The next step is to create the AngularJS template that defines the view for the quiz.</span></span> <span data-ttu-id="b19e4-327">이 작업을 수행 하려면 엽니다는 **Index.cshtml** 내 파일의 **보기 | 홈** 폴더 및 콘텐츠를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-327">To do this, open the **Index.cshtml** file inside the **Views | Home** folder and replace the content with the following code.</span></span>

    <span data-ttu-id="b19e4-328">(코드 조각- *AspNetWebApiSpa-e x 2-GeekQuizView*)</span><span class="sxs-lookup"><span data-stu-id="b19e4-328">(Code Snippet - *AspNetWebApiSpa - Ex2 - GeekQuizView*)</span></span>

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample20.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="b19e4-329">AngularJS 템플릿은 static 태그 브라우저에 표시 되는 동적 뷰를 변환할 모델과 컨트롤러의 정보를 사용 하는 선언적 지정입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-329">The AngularJS template is a declarative specification that uses information from the model and the controller to transform static markup into the dynamic view that the user sees in the browser.</span></span> <span data-ttu-id="b19e4-330">다음은 AngularJS 요소 고 서식 파일에 사용할 수 있는 특성의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-330">The following are examples of AngularJS elements and element attributes that can be used in a template:</span></span>
    > 
    > - <span data-ttu-id="b19e4-331">**ng 앱** 지시문 AngularJS 응용 프로그램의 루트 요소를 나타내는 DOM 요소를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-331">The **ng-app** directive tells AngularJS the DOM element that represents the root element of the application.</span></span>
    > - <span data-ttu-id="b19e4-332">**ng 컨트롤러** 지시문의 지시문이 선언 된 지점에서 DOM에는 컨트롤러를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-332">The **ng-controller** directive attaches a controller to the DOM at the point where the directive is declared.</span></span>
    > - <span data-ttu-id="b19e4-333">중괄호 표기법 **{{}}** 컨트롤러에 정의 된 범위 속성에 대 한 바인딩을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-333">The curly brace notation **{{ }}** denotes bindings to the scope properties defined in the controller.</span></span>
    > - <span data-ttu-id="b19e4-334">**ng 클릭** 지시문을 사용 하 여을 사용자가 클릭에 대 한 응답에는 범위에 정의 된 함수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-334">The **ng-click** directive is used to invoke the functions defined in the scope in response to user clicks.</span></span>
10. <span data-ttu-id="b19e4-335">열기는 **Site.css** 내 파일의 **콘텐츠** 폴더 고 퀴즈 보기에 대 한 모양 및 느낌을 제공 하는 파일의 끝에 다음 강조 표시 된 스타일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-335">Open the **Site.css** file inside the **Content** folder and add the following highlighted styles at the end of the file to provide a look and feel for the quiz view.</span></span>

    <span data-ttu-id="b19e4-336">(코드 조각- *AspNetWebApiSpa-e x 2-GeekQuizStyles*)</span><span class="sxs-lookup"><span data-stu-id="b19e4-336">(Code Snippet - *AspNetWebApiSpa - Ex2 - GeekQuizStyles*)</span></span>

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample21.css)]

<a id="Ex2Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="b19e4-337">작업 2-솔루션 실행</span><span class="sxs-lookup"><span data-stu-id="b19e4-337">Task 2 – Running the Solution</span></span>

<span data-ttu-id="b19e4-338">이 태스크를 실행 합니다 새 사용자를 사용 하 여 솔루션 인터페이스인 일부의 퀴즈 질문에 답변 하는 AngularJS를 사용 하 여 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-338">In this task you will execute the solution using the new user interface you built with AngularJS to answer some of the quiz questions.</span></span>

1. <span data-ttu-id="b19e4-339">키를 눌러 **F5** 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-339">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="b19e4-340">새 사용자 계정을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-340">Register a new user account.</span></span> <span data-ttu-id="b19e4-341">이 작업을 수행 하려면 연습 1, 작업 3에에서 설명 된 등록 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-341">To do this, follow the registration steps described in Exercise 1, Task 3.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b19e4-342">이전 연습에서 솔루션을 사용 하는 경우에 이전에 만든 사용자 계정으로 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-342">If you are using the solution from the previous exercise, you can log in with the user account you created before.</span></span>
3. <span data-ttu-id="b19e4-343">**홈** 퀴즈의 첫 번째 질문을 보여 주는 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-343">The **Home** page should appear, showing the first question of the quiz.</span></span> <span data-ttu-id="b19e4-344">옵션 중 하나를 클릭 하 여 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-344">Answer the question by clicking one of the options.</span></span> <span data-ttu-id="b19e4-345">이 트리거하는 **sendAnswer** 선택 된 옵션을 전송 하는 이전에 정의 된 함수는 **퀴즈** 웹 API입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-345">This will trigger the **sendAnswer** function defined earlier, which sends the selected option to the **Trivia** Web API.</span></span>

    <span data-ttu-id="b19e4-346">![질문에 대답](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "질문에 대답")</span><span class="sxs-lookup"><span data-stu-id="b19e4-346">![Answering a question](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "Answering a question")</span></span>

    <span data-ttu-id="b19e4-347">*질문에 대답*</span><span class="sxs-lookup"><span data-stu-id="b19e4-347">*Answering a question*</span></span>
4. <span data-ttu-id="b19e4-348">단추 중 하나를 클릭 한 후에 대답 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-348">After clicking one of the buttons, the answer should appear.</span></span> <span data-ttu-id="b19e4-349">클릭 **다음 질문** 다음과 같은 질문을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-349">Click **Next Question** to show the following question.</span></span> <span data-ttu-id="b19e4-350">이 트리거하는 **nextQuestion** 컨트롤러에 정의 된 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-350">This will trigger the **nextQuestion** function defined in the controller.</span></span>

    <span data-ttu-id="b19e4-351">![다음 질문을 요청](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "다음 질문을 요청 합니다.")</span><span class="sxs-lookup"><span data-stu-id="b19e4-351">![Requesting the next question](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "Requesting the next question")</span></span>

    <span data-ttu-id="b19e4-352">*다음 질문을 요청합니다.*</span><span class="sxs-lookup"><span data-stu-id="b19e4-352">*Requesting the next question*</span></span>
5. <span data-ttu-id="b19e4-353">다음 질문 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-353">The next question should appear.</span></span> <span data-ttu-id="b19e4-354">원하는 횟수 만큼 질문에 응답을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-354">Continue answering questions as many times as you want.</span></span> <span data-ttu-id="b19e4-355">모든 질문을 완료 한 후 첫 번째 질문을 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-355">After completing all the questions you should return to the first question.</span></span>

    <span data-ttu-id="b19e4-356">![다른 질문](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "다른 질문")</span><span class="sxs-lookup"><span data-stu-id="b19e4-356">![Another question](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "Another question")</span></span>

    <span data-ttu-id="b19e4-357">*다음 질문*</span><span class="sxs-lookup"><span data-stu-id="b19e4-357">*Next question*</span></span>
6. <span data-ttu-id="b19e4-358">Visual Studio 및 키를 눌러로 돌아가서 **SHIFT + f 5를 눌러** 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-358">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--creating-a-flip-animation-using-css3"></a><span data-ttu-id="b19e4-359">작업 3 – CSS3를 사용 하 여 플립 애니메이션 만들기</span><span class="sxs-lookup"><span data-stu-id="b19e4-359">Task 3 – Creating a Flip Animation Using CSS3</span></span>

<span data-ttu-id="b19e4-360">이 작업에서 애니메이션을 수행 하 다양 한 질문에 대답할 및 다음 질문을 검색할 때 플립 효과 추가 하 여 CSS3 속성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-360">In this task you will use CSS3 properties to perform rich animations by adding a flip effect when a question is answered and when the next question is retrieved.</span></span>

1. <span data-ttu-id="b19e4-361">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **콘텐츠** 의 폴더는 **GeekQuiz** 프로젝트를 마우스 선택 **추가 | 기존 항목...** .</span><span class="sxs-lookup"><span data-stu-id="b19e4-361">In **Solution Explorer**, right-click the **Content** folder of the **GeekQuiz** project and select **Add | Existing Item...**.</span></span>

    <span data-ttu-id="b19e4-362">![콘텐츠 폴더에 기존 항목 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "콘텐츠 폴더에 기존 항목 추가")</span><span class="sxs-lookup"><span data-stu-id="b19e4-362">![Adding an existing item to the Content folder](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "Adding an existing item to the Content folder")</span></span>

    <span data-ttu-id="b19e4-363">*콘텐츠 폴더에 기존 항목 추가*</span><span class="sxs-lookup"><span data-stu-id="b19e4-363">*Adding an existing item to the Content folder*</span></span>
2. <span data-ttu-id="b19e4-364">에 **기존 항목 추가** 대화 상자에서 이동 하는 **소스/자산의** 폴더를 선택 **Flip.css**합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-364">In the **Add Existing Item** dialog box, navigate to the **Source/Assets** folder and select **Flip.css**.</span></span> <span data-ttu-id="b19e4-365">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-365">Click **Add**.</span></span>

    <span data-ttu-id="b19e4-366">![자산 중에서 Flip.css 파일을 추가](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "자산 중에서 Flip.css 파일을 추가 합니다.")</span><span class="sxs-lookup"><span data-stu-id="b19e4-366">![Adding the Flip.css file from Assets](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "Adding the Flip.css file from Assets")</span></span>

    <span data-ttu-id="b19e4-367">*자산 중에서 Flip.css 파일을 추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="b19e4-367">*Adding the Flip.css file from Assets*</span></span>
3. <span data-ttu-id="b19e4-368">열기는 **Flip.css** 방금 추가한 파일 및 해당 내용을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-368">Open the **Flip.css** file you just added and inspect its content.</span></span>
4. <span data-ttu-id="b19e4-369">찾을 **변환 대칭** 메모 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-369">Locate the **flip transformation** comment.</span></span> <span data-ttu-id="b19e4-370">CSS를 사용 하 여 해당 의견 아래의 스타일 **관점** 및 **rotateY** 변환을 생성 하는 &quot;대칭 이동 카드&quot; 효과입니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-370">The styles below that comment use the CSS **perspective** and **rotateY** transformations to generate a &quot;card flip&quot; effect.</span></span>

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample22.css)]
5. <span data-ttu-id="b19e4-371">찾을 **대칭 이동 하는 동안 창 뒷면 숨깁니다** 메모 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-371">Locate the **hide back of pane during flip** comment.</span></span> <span data-ttu-id="b19e4-372">설정 하 여 뷰어에서 직면 하는 경우 해당 의견 아래의 스타일 숨깁니다 얼굴 백 측은 **뒷면 가시성** CSS 속성을 *숨겨진*합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-372">The style below that comment hides the back-side of the faces when they are facing away from the viewer by setting the **backface-visibility** CSS property to *hidden*.</span></span>

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample23.css)]
6. <span data-ttu-id="b19e4-373">열기는 **BundleConfig.cs** 내 파일의 **앱\_시작** 폴더에 대 한 참조를 추가 하 고는 **Flip.css** 파일에 **&quot;~/Content/css&quot;** 스타일 번들</span><span class="sxs-lookup"><span data-stu-id="b19e4-373">Open the **BundleConfig.cs** file inside the **App\_Start** folder and add the reference to the **Flip.css** file in the **&quot;~/Content/css&quot;** style bundle</span></span>

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample24.cs)]
7. <span data-ttu-id="b19e4-374">키를 눌러 **F5** 솔루션 및 자격 증명을 사용 하 여 로그를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-374">Press **F5** to run the solution and log in with your credentials.</span></span>
8. <span data-ttu-id="b19e4-375">옵션 중 하나를 클릭 하 여 질문에 대답 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-375">Answer a question by clicking one of the options.</span></span> <span data-ttu-id="b19e4-376">뷰 간에 전환할 때 플립 효과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-376">Notice the flip effect when transitioning between views.</span></span>

    <span data-ttu-id="b19e4-377">![플립 영향을 주지 않고 질문에 대답](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "플립 효과 함께 질문에 대답")</span><span class="sxs-lookup"><span data-stu-id="b19e4-377">![Answering a question with the flip effect](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "Answering a question with the flip effect")</span></span>

    <span data-ttu-id="b19e4-378">*플립 효과 함께 질문에 대답*</span><span class="sxs-lookup"><span data-stu-id="b19e4-378">*Answering a question with the flip effect*</span></span>
9. <span data-ttu-id="b19e4-379">클릭 **다음 질문** 를 다음과 같은 질문을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-379">Click **Next Question** to retrieve the following question.</span></span> <span data-ttu-id="b19e4-380">플립 효과 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-380">The flip effect should appear again.</span></span>

    <span data-ttu-id="b19e4-381">![플립 효과 함께 다음 질문의 검색](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "플립 효과 함께 다음 질문을 검색 합니다.")</span><span class="sxs-lookup"><span data-stu-id="b19e4-381">![Retrieving the following question with the flip effect](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "Retrieving the following question with the flip effect")</span></span>

    <span data-ttu-id="b19e4-382">*플립 효과 함께 다음과 같은 질문을 검색합니다.*</span><span class="sxs-lookup"><span data-stu-id="b19e4-382">*Retrieving the following question with the flip effect*</span></span>

* * *

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="b19e4-383">요약</span><span class="sxs-lookup"><span data-stu-id="b19e4-383">Summary</span></span>

<span data-ttu-id="b19e4-384">이 실습 랩을 완료 하 여 배웠습니다 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="b19e4-384">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="b19e4-385">ASP.NET 스 캐 폴딩을 사용 하 여 ASP.NET Web API 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="b19e4-385">Create an ASP.NET Web API controller using ASP.NET Scaffolding</span></span>
- <span data-ttu-id="b19e4-386">다음 퀴즈 질문을 검색 하는 웹 API 가져오기 작업을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="b19e4-386">Implement a Web API Get action to retrieve the next quiz question</span></span>
- <span data-ttu-id="b19e4-387">답을 저장 하는 웹 API Post 작업 구현</span><span class="sxs-lookup"><span data-stu-id="b19e4-387">Implement a Web API Post action to store the quiz answers</span></span>
- <span data-ttu-id="b19e4-388">Visual Studio 패키지 관리자 콘솔에서 AngularJS 설치</span><span class="sxs-lookup"><span data-stu-id="b19e4-388">Install AngularJS from the Visual Studio Package Manager Console</span></span>
- <span data-ttu-id="b19e4-389">AngularJS 템플릿 구현 및 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="b19e4-389">Implement AngularJS templates and controllers</span></span>
- <span data-ttu-id="b19e4-390">사용 하 여 CSS3 애니메이션 효과 수행 하려면 전환</span><span class="sxs-lookup"><span data-stu-id="b19e4-390">Use CSS3 transitions to perform animation effects</span></span>
