---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
title: ASP.NET MVC 4 기본 사항 | Microsoft Docs
author: rick-anderson
description: 이 실습 랩에서 MVC (모델 뷰 컨트롤러) 음악 스토어를 소개 하 고 ASP.NET MV를 사용 하는 방법을 단계별로 설명 하는 자습서 응용 프로그램을 기반으로...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: b7dba543-73c3-4534-a9a0-ba70fa2c6a8a
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
msc.type: authoredcontent
ms.openlocfilehash: a0dd32280321938aba84a2aed5273d80750ed774
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="aspnet-mvc-4-fundamentals"></a><span data-ttu-id="7bf69-103">ASP.NET MVC 4 기본 사항</span><span class="sxs-lookup"><span data-stu-id="7bf69-103">ASP.NET MVC 4 Fundamentals</span></span>

<span data-ttu-id="7bf69-104">으로 [웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="7bf69-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="7bf69-105">웹 캠프 학습 키트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="7bf69-106">이 실습 랩에서 MVC (모델 뷰 컨트롤러) 음악 스토어를 소개 하 고 ASP.NET MVC와 Visual Studio를 사용 하는 방법을 단계별로 설명 하는 자습서 응용 프로그램을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-106">This Hands-On Lab is based on MVC (Model View Controller) Music Store, a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio.</span></span> <span data-ttu-id="7bf69-107">랩 전체은 단순 하기 때문에 설명 합니다 함께 이러한 기술을 사용 하 여의 전원 아직 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-107">Throughout the lab you will learn the simplicity, yet power of using these technologies together.</span></span> <span data-ttu-id="7bf69-108">간단한 응용 프로그램으로 시작 하 고를 구성할 때까지 모든 기능을 갖춘 ASP.NET MVC 4 웹 응용 프로그램 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-108">You will start with a simple application and will build it until you have a fully functional ASP.NET MVC 4 Web Application.</span></span>

<span data-ttu-id="7bf69-109">이 랩에서 ASP.NET MVC 4에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-109">This Lab works with ASP.NET MVC 4.</span></span>

<span data-ttu-id="7bf69-110">찾을 수 자습서 응용 프로그램의 ASP.NET MVC 3 버전을 탐색 하려면 [MVC 음악 저장소](https://github.com/evilDave/MVC-Music-Store)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-110">If you wish to explore the ASP.NET MVC 3 version of the tutorial application, you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<span data-ttu-id="7bf69-111">이 실습 랩에서 개발자가의 HTML 및 JavaScript 등의 웹 개발 기술을 경험 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-111">This Hands-On Lab assumes that the developer has experience in Web development technologies, such as HTML and JavaScript.</span></span>

> [!NOTE]
> <span data-ttu-id="7bf69-112">모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [Microsoft-웹/WebCampTrainingKit 릴리스](https://aka.ms/webcamps-training-kit)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-112">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="7bf69-113">이 랩에 특정 프로젝트에서 사용할 수는 [ASP.NET MVC 4 기초](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-113">The project specific to this lab is available at [ASP.NET MVC 4 Fundamentals](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals).</span></span>

<a id="The_Music_Store_application"></a>
### <a name="the-music-store-application"></a><span data-ttu-id="7bf69-114">음악 스토어 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="7bf69-114">The Music Store application</span></span>

<span data-ttu-id="7bf69-115">이 랩에서 전체에서 빌드되는 음악 스토어 웹 응용 프로그램 세 부분으로 구성: 쇼핑, 체크 아웃, 및 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-115">The Music Store web application that will be built throughout this Lab comprises three main parts: shopping, checkout, and administration.</span></span> <span data-ttu-id="7bf69-116">방문자 장르별로 앨범 찾아보기, 앨범 자신의 카트에 추가 하 고, 선택 검토 하 고 마지막으로 로그인 하 고 주문을 완료할 체크 아웃을 계속 진행 하는 작업을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-116">Visitors will be able to browse albums by genre, add albums to their cart, review their selection and finally proceed to checkout to login and complete the order.</span></span> <span data-ttu-id="7bf69-117">또한 저장소 관리자가 사용할 수 있는 앨범 뿐 아니라 주 속성을 관리할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-117">Additionally, store administrators will be able to manage the available albums as well as their main properties.</span></span>

<span data-ttu-id="7bf69-118">![Music Store 화면](aspnet-mvc-4-fundamentals/_static/image1.png "Music Store 화면")</span><span class="sxs-lookup"><span data-stu-id="7bf69-118">![Music Store screens](aspnet-mvc-4-fundamentals/_static/image1.png "Music Store screens")</span></span>

<span data-ttu-id="7bf69-119">*Music Store 화면*</span><span class="sxs-lookup"><span data-stu-id="7bf69-119">*Music Store screens*</span></span>

<a id="ASPNET_MVC_4_Essentials"></a>
### <a name="aspnet-mvc-4-essentials"></a><span data-ttu-id="7bf69-120">ASP.NET MVC 4 Essentials</span><span class="sxs-lookup"><span data-stu-id="7bf69-120">ASP.NET MVC 4 Essentials</span></span>

<span data-ttu-id="7bf69-121">사용 하 여 음악 스토어 응용 프로그램을 작성 **컨트롤러 MVC (Model View)**, 응용 프로그램을 세 가지 주요 구성 요소를 구분 하는 아키텍처 패턴:</span><span class="sxs-lookup"><span data-stu-id="7bf69-121">Music Store application will be built using **Model View Controller (MVC)**, an architectural pattern that separates an application into three main components:</span></span>

- <span data-ttu-id="7bf69-122">**모델**: 모델 개체는 도메인 논리를 구현 하는 응용 프로그램의 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-122">**Models**: Model objects are the parts of the application that implement the domain logic.</span></span> <span data-ttu-id="7bf69-123">종종, 모델 개체도 검색 및 모델 상태를 데이터베이스에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-123">Often, model objects also retrieve and store model state in a database.</span></span>
- <span data-ttu-id="7bf69-124">**보기:** 뷰는 응용 프로그램의 UI (사용자 인터페이스)를 표시 하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-124">**Views:** Views are the components that display the application's user interface (UI).</span></span> <span data-ttu-id="7bf69-125">일반적으로이 UI는 모델 데이터에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-125">Typically, this UI is created from the model data.</span></span> <span data-ttu-id="7bf69-126">텍스트 상자 및 앨범 개체의 현재 상태에 따라 드롭 다운 목록을 표시 하는 앨범의 편집 뷰 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-126">An example would be the edit view of Albums that displays text boxes and a drop-down list based on the current state of an Album object.</span></span>
- <span data-ttu-id="7bf69-127">**컨트롤러의 경우:** 컨트롤러는 사용자 상호 작용 처리는 모델을 조작 하 고 궁극적으로 UI를 렌더링 하는 뷰를 선택 하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-127">**Controllers:** Controllers are the components that handle user interaction, manipulate the model, and ultimately select a view to render the UI.</span></span> <span data-ttu-id="7bf69-128">MVC 응용 프로그램에서 보기는 정보만 표시합니다. 컨트롤러가 사용자 입력 및 상호 작용을 처리하고 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-128">In an MVC application, the view only displays information; the controller handles and responds to user input and interaction.</span></span>

<span data-ttu-id="7bf69-129">MVC 패턴을 사용 하면 이러한 요소 간의 느슨한 결합을 제공 하는 동안 응용 프로그램 (입력된 논리, 비즈니스 논리 및 UI 논리)의 다양 한 측면을 구분 하는 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-129">The MVC pattern helps you to create applications that separate the different aspects of the application (input logic, business logic, and UI logic), while providing a loose coupling between these elements.</span></span> <span data-ttu-id="7bf69-130">이러한 분리 구현 시 한 번에 하나의 측면에 초점을 맞출 수 있으므로 응용 프로그램을 빌드할 때 복잡도 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-130">This separation helps you manage complexity when you build an application, as it allows you to focus on one aspect of the implementation at a time.</span></span> <span data-ttu-id="7bf69-131">또한 MVC 패턴을 사용 하면 쉽게도 응용 프로그램을 만들기 위한 테스트 기반 개발 (TDD) 사용을 권장 하는 응용 프로그램을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-131">In addition, the MVC pattern makes it easy to test applications, also encouraging the use of test-driven development (TDD) for creating applications.</span></span>

<span data-ttu-id="7bf69-132">**ASP.NET MVC** 프레임 워크는 ASP.NET MVC 기반 웹 응용 프로그램을 만들기 위한 ASP.NET Web Forms 패턴에 대 한 대안을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-132">The **ASP.NET MVC** framework provides an alternative to the ASP.NET Web Forms pattern for creating ASP.NET MVC-based Web applications.</span></span> <span data-ttu-id="7bf69-133">**ASP.NET MVC** 프레임 워크는 간단 하 고 테스트 하기 편리한 프레젠테이션 프레임 워크는 (웹 폼 기반 응용 프로그램와 마찬가지로) 마스터 페이지 및 멤버 자격을 기반으로 기존 ASP.NET 기능과 통합 되어 핵심.NET framework의 모든 기능을 얻게 되므로 인증입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-133">The **ASP.NET MVC** framework is a lightweight, highly testable presentation framework that (as with Web-forms-based applications) is integrated with existing ASP.NET features, such as master pages and membership-based authentication so you get all the power of the core .NET framework.</span></span> <span data-ttu-id="7bf69-134">이미 잘 알고 있다면 ASP.NET Web Forms 이미 사용 하는 모든 라이브러리도 ASP.NET MVC 4에서 사용할 수 있는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-134">This is useful if you are already familiar with ASP.NET Web Forms because all the libraries that you already use are available in ASP.NET MVC 4 as well.</span></span>

<span data-ttu-id="7bf69-135">또한 MVC 응용 프로그램의 세 가지 주요 구성 요소 간의 느슨한 결합 병렬 개발을 촉진 하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-135">In addition, the loose coupling between the three main components of an MVC application also promotes parallel development.</span></span> <span data-ttu-id="7bf69-136">예를 들어 한 개발자 보기에서 작업할 수 있습니다, 두 번째 개발자는 컨트롤러 논리에서 작업할 수 있습니다 및 세 번째 개발자는 모델의 비즈니스 논리에 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-136">For instance, one developer can work on the view, a second developer can work on the controller logic, and a third developer can focus on the business logic in the model.</span></span>

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="7bf69-137">목표</span><span class="sxs-lookup"><span data-stu-id="7bf69-137">Objectives</span></span>

<span data-ttu-id="7bf69-138">이 실습 랩에서 배우게 됩니다 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="7bf69-138">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="7bf69-139">음악 스토어 응용 프로그램 자습서를 기반으로 ASP.NET MVC 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="7bf69-139">Create an ASP.NET MVC application from scratch based on the Music Store Application tutorial</span></span>
- <span data-ttu-id="7bf69-140">사이트 및 검색의 주요 기능에 대 한 홈 페이지 Url을 처리 하기 위해 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="7bf69-140">Add Controllers to handle URLs to the Home page of the site and for browsing its main functionality</span></span>
- <span data-ttu-id="7bf69-141">노드 스타일 함께 표시 되는 콘텐츠를 사용자 지정 하는 뷰 추가</span><span class="sxs-lookup"><span data-stu-id="7bf69-141">Add a View to customize the content displayed along with its style</span></span>
- <span data-ttu-id="7bf69-142">모델 클래스를 포함 하 고 관리할 데이터 및 도메인 논리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-142">Add Model classes to contain and manage data and domain logic</span></span>
- <span data-ttu-id="7bf69-143">뷰 모델 패턴을 사용 하 여 컨트롤러 작업에서 정보 보기 템플릿을 전달</span><span class="sxs-lookup"><span data-stu-id="7bf69-143">Use View Model pattern to pass information from controller actions to the view templates</span></span>
- <span data-ttu-id="7bf69-144">인터넷 응용 프로그램에 대 한 ASP.NET MVC 4 새 서식 파일을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-144">Explore the ASP.NET MVC 4 new template for internet applications</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="7bf69-145">전제 조건</span><span class="sxs-lookup"><span data-stu-id="7bf69-145">Prerequisites</span></span>

<span data-ttu-id="7bf69-146">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-146">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="7bf69-147">[Visual Studio 2012 Express for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (읽기 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은)</span><span class="sxs-lookup"><span data-stu-id="7bf69-147">[Visual Studio 2012 Express for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (read [Appendix A](#AppendixA) for instructions on how to install it)</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="7bf69-148">설정</span><span class="sxs-lookup"><span data-stu-id="7bf69-148">Setup</span></span>

<span data-ttu-id="7bf69-149">**설치 하는 코드 조각**</span><span class="sxs-lookup"><span data-stu-id="7bf69-149">**Installing Code Snippets**</span></span>

<span data-ttu-id="7bf69-150">편의 위해는이 랩에 따라 관리 코드의 대부분 Visual Studio 코드 조각 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-150">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="7bf69-151">실행 코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-151">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="7bf69-152">이 문서에서 부록을 참조할 수 사용 하는 방법에 알아봅니다 사용 하 고 Visual Studio 코드 조각에 익숙한 경우 &quot; [부록 c:를 사용 하 여 코드 조각을](#AppendixC)&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-152">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="7bf69-153">연습</span><span class="sxs-lookup"><span data-stu-id="7bf69-153">Exercises</span></span>

<span data-ttu-id="7bf69-154">이 실습 랩에서 다음 연습으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-154">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="7bf69-155">연습 1: MusicStore ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="7bf69-155">Exercise 1: Creating MusicStore ASP.NET MVC Web Application Project</span></span>](#Exercise1)
2. [<span data-ttu-id="7bf69-156">연습 2: 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="7bf69-156">Exercise 2: Creating a Controller</span></span>](#Exercise2)
3. [<span data-ttu-id="7bf69-157">연습 3: 컨트롤러에 매개 변수 전달</span><span class="sxs-lookup"><span data-stu-id="7bf69-157">Exercise 3: Passing parameters to a Controller</span></span>](#Exercise3)
4. [<span data-ttu-id="7bf69-158">보기를 만드는 연습 4:</span><span class="sxs-lookup"><span data-stu-id="7bf69-158">Exercise 4: Creating a View</span></span>](#Exercise4)
5. [<span data-ttu-id="7bf69-159">연습 5: 뷰 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="7bf69-159">Exercise 5: Creating a View Model</span></span>](#Exercise5)
6. [<span data-ttu-id="7bf69-160">실습 6: 매개 변수를 보기에 사용</span><span class="sxs-lookup"><span data-stu-id="7bf69-160">Exercise 6: Using parameters in View</span></span>](#Exercise6)
7. [<span data-ttu-id="7bf69-161">7 연습: ASP.NET MVC 4 새 템플릿 주위 랩</span><span class="sxs-lookup"><span data-stu-id="7bf69-161">Exercise 7: A lap around ASP.NET MVC 4 New Template</span></span>](#Exercise7)

> [!NOTE]
> <span data-ttu-id="7bf69-162">각 연습 동반 되는 **끝** 연습을 완료 한 후 가져와야 생성 되는 솔루션에 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-162">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="7bf69-163">연습을 통해 작업 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-163">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="7bf69-164">예상 소요 시간: **60 분**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-164">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_MusicStore_ASPNET_MVC_Web_Application_Project"></a>
### <a name="exercise-1-creating-musicstore-aspnet-mvc-web-application-project"></a><span data-ttu-id="7bf69-165">연습 1: MusicStore ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="7bf69-165">Exercise 1: Creating MusicStore ASP.NET MVC Web Application Project</span></span>

<span data-ttu-id="7bf69-166">이 연습에서는 Visual Studio 2012 express의 주 폴더 조직와 함께 웹에 대 한 ASP.NET MVC 응용 프로그램을 만드는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-166">In this exercise, you will learn how to create an ASP.NET MVC application in Visual Studio 2012 Express for Web as well as its main folder organization.</span></span> <span data-ttu-id="7bf69-167">또한 새 컨트롤러를 추가 하 고 응용 프로그램의 홈 페이지에 단순 문자열을 표시 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-167">Additionally, you will learn how to add a new Controller and make it display a simple string in the application's home page.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_ASPNET_MVC_Web_Application_Project"></a>
#### <a name="task-1---creating-the-aspnet-mvc-web-application-project"></a><span data-ttu-id="7bf69-168">작업 1-ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="7bf69-168">Task 1 - Creating the ASP.NET MVC Web Application Project</span></span>

1. <span data-ttu-id="7bf69-169">이 태스크에서는 MVC Visual Studio 템플릿을 사용 하 여 빈 ASP.NET MVC 응용 프로그램 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-169">In this task, you will create an empty ASP.NET MVC application project using the MVC Visual Studio template.</span></span> <span data-ttu-id="7bf69-170">시작 **VS Express for Web**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-170">Start **VS Express for Web**.</span></span>
2. <span data-ttu-id="7bf69-171">**파일** 메뉴에서 **새 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-171">On the **File** menu, click **New Project**.</span></span>
3. <span data-ttu-id="7bf69-172">에 **새 프로젝트** 대화 상자 선택 된 **ASP.NET MVC 4 웹 응용 프로그램** 프로젝트 아래에 있는 형식을 **Visual C#** **웹** 서식 파일 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-172">In the **New Project** dialog box select the **ASP.NET MVC 4 Web Application** project type, located under **Visual C#,** **Web** template list.</span></span>
4. <span data-ttu-id="7bf69-173">변경 된 **이름** 를 *MvcMusicStore*합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-173">Change the **Name** to *MvcMusicStore*.</span></span>
5. <span data-ttu-id="7bf69-174">새 내부 솔루션의 위치를 설정할 **시작** 예를 들어가이 연습 원본 폴더에 폴더 **[귀하가 HOL 경로] \Source\Ex01-CreatingMusicStoreProject\Begin**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-174">Set the location of the solution inside a new **Begin** folder in this Exercise's Source folder, for example **[YOUR-HOL-PATH]\Source\Ex01-CreatingMusicStoreProject\Begin**.</span></span> <span data-ttu-id="7bf69-175">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-175">Click **OK**.</span></span>

    <span data-ttu-id="7bf69-176">![새 프로젝트 대화 상자 만들기](aspnet-mvc-4-fundamentals/_static/image2.png "새 프로젝트 대화 상자 만들기")</span><span class="sxs-lookup"><span data-stu-id="7bf69-176">![Create New Project Dialog Box](aspnet-mvc-4-fundamentals/_static/image2.png "Create New Project Dialog Box")</span></span>

    <span data-ttu-id="7bf69-177">*새 프로젝트 대화 상자 만들기*</span><span class="sxs-lookup"><span data-stu-id="7bf69-177">*Create New Project Dialog Box*</span></span>
6. <span data-ttu-id="7bf69-178">에 **새 ASP.NET MVC 4 프로젝트** 대화 상자 선택은 **기본** 템플릿 있는지 확인 하 고는 **뷰 엔진** 선택한 **Razor**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-178">In the **New ASP.NET MVC 4 Project** dialog box select the **Basic** template and make sure that the **View engine** selected is **Razor**.</span></span> <span data-ttu-id="7bf69-179">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-179">Click **OK**.</span></span>

    <span data-ttu-id="7bf69-180">![새 ASP.NET MVC 4 프로젝트 대화 상자](aspnet-mvc-4-fundamentals/_static/image3.png "새 ASP.NET MVC 4 프로젝트 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="7bf69-180">![New ASP.NET MVC 4 Project Dialog Box](aspnet-mvc-4-fundamentals/_static/image3.png "New ASP.NET MVC 4 Project Dialog Box")</span></span>

    <span data-ttu-id="7bf69-181">*새 ASP.NET MVC 4 프로젝트 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="7bf69-181">*New ASP.NET MVC 4 Project Dialog Box*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Exploring_the_Solution_Structure"></a>
#### <a name="task-2---exploring-the-solution-structure"></a><span data-ttu-id="7bf69-182">작업 2-솔루션 구조 탐색</span><span class="sxs-lookup"><span data-stu-id="7bf69-182">Task 2 - Exploring the Solution Structure</span></span>

<span data-ttu-id="7bf69-183">ASP.NET MVC 프레임 워크에는 MVC 패턴을 지 원하는 웹 응용 프로그램을 만들 때 도움이 되는 Visual Studio 프로젝트 템플릿이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-183">The ASP.NET MVC framework includes a Visual Studio project template that helps you create Web applications supporting the MVC pattern.</span></span> <span data-ttu-id="7bf69-184">이 템플릿은 필요한 폴더, 항목 템플릿 및 구성 파일 항목 새 ASP.NET MVC 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-184">This template creates a new ASP.NET MVC Web application with the required folders, item templates, and configuration-file entries.</span></span>

<span data-ttu-id="7bf69-185">이 작업에서는 포함 된 요소를 이해 하는 솔루션 구조 및 해당 관계를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-185">In this task, you will examine the solution structure to understand the elements that are involved and their relationships.</span></span> <span data-ttu-id="7bf69-186">기본적으로 ASP.NET MVC 프레임 워크를 사용 하기 때문에 모든 ASP.NET MVC 응용 프로그램에는 다음 폴더가 포함 된 한 &quot;구성의 관례&quot; 접근 방식 및 폴더 이름 지정에 따라 몇 가지 기본 사항을 가정 하면 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-186">The following folders are included in all the ASP.NET MVC application because the ASP.NET MVC framework by default uses a &quot;convention over configuration&quot; approach, and makes some default assumptions based on folder naming conventions.</span></span>

1. <span data-ttu-id="7bf69-187">프로젝트를 만든 후 오른쪽에 솔루션 탐색기에서 만든 폴더 구조를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-187">Once the project is created, review the folder structure that has been created in the Solution Explorer on the right side:</span></span>

    <span data-ttu-id="7bf69-188">![솔루션 탐색기에서 ASP.NET MVC 폴더 구조](aspnet-mvc-4-fundamentals/_static/image4.png "솔루션 탐색기에서 ASP.NET MVC 폴더 구조")</span><span class="sxs-lookup"><span data-stu-id="7bf69-188">![ASP.NET MVC Folder structure in Solution Explorer](aspnet-mvc-4-fundamentals/_static/image4.png "ASP.NET MVC Folder structure in Solution Explorer")</span></span>

    <span data-ttu-id="7bf69-189">*솔루션 탐색기에서 ASP.NET MVC 폴더 구조*</span><span class="sxs-lookup"><span data-stu-id="7bf69-189">*ASP.NET MVC Folder structure in Solution Explorer*</span></span>

   1. <span data-ttu-id="7bf69-190">**컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-190">**Controllers**.</span></span> <span data-ttu-id="7bf69-191">이 폴더는 컨트롤러 클래스가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-191">This folder will contain the controller classes.</span></span> <span data-ttu-id="7bf69-192">MVC 기반 응용 프로그램에서 컨트롤러는 최종 사용자 상호 작용을 처리 모델을 조작 하 고, 궁극적으로 UI를 렌더링 하는 뷰를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-192">In an MVC based application, controllers are responsible for handling end user interaction, manipulating the model, and ultimately choosing a view to render the UI.</span></span>

       > [!NOTE]
       > <span data-ttu-id="7bf69-193">MVC 프레임 워크를 위해서는 끝나야 모든 컨트롤러의 이름이 &quot;컨트롤러&quot;-예를 들어 HomeController, LoginController 또는 ProductController 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-193">The MVC framework requires the names of all controllers to end with &quot;Controller&quot;-for example, HomeController, LoginController, or ProductController.</span></span>
   2. <span data-ttu-id="7bf69-194">**모델**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-194">**Models**.</span></span> <span data-ttu-id="7bf69-195">이 폴더는 MVC 웹 응용 프로그램에 대 한 응용 프로그램 모델을 나타내는 클래스를 위해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-195">This folder is provided for classes that represent the application model for the MVC Web application.</span></span> <span data-ttu-id="7bf69-196">일반적으로 개체와 데이터 저장소와 상호 작용 하기 위한 논리를 정의 하는 코드가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-196">This usually includes code that defines objects and the logic for interacting with the data store.</span></span> <span data-ttu-id="7bf69-197">일반적으로 실제 모델 개체는 별도 클래스 라이브러리에 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-197">Typically, the actual model objects will be in separate class libraries.</span></span> <span data-ttu-id="7bf69-198">그러나 새 응용 프로그램을 만들 때 클래스를 포함 한 다음 개발 주기에서 나중에 별도 클래스 라이브러리로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-198">However, when you create a new application, you might include classes and then move them into separate class libraries at a later point in the development cycle.</span></span>
   3. <span data-ttu-id="7bf69-199">**뷰**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-199">**Views**.</span></span> <span data-ttu-id="7bf69-200">이 폴더에는 뷰, 응용 프로그램의 사용자 인터페이스를 표시 하는 일을 담당 하는 구성 요소에 대 한 권장된 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-200">This folder is the recommended location for views, the components responsible for displaying the application's user interface.</span></span> <span data-ttu-id="7bf69-201">보기 뷰 렌더링에 관련 된 다른 파일이.aspx,.ascx,.cshtml 및.master 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-201">Views use .aspx, .ascx, .cshtml and .master files, in addition to any other files that are related to rendering views.</span></span> <span data-ttu-id="7bf69-202">Views 폴더에는 각 컨트롤러;에 대 한 컨트롤러 이름 접두사가 포함 된 폴더의 이름은입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-202">Views folder contains a folder for each controller; the folder is named with the controller-name prefix.</span></span> <span data-ttu-id="7bf69-203">예를 들어, 라는 컨트롤러가 있으면 **HomeController**, Views 폴더에 Home 이라는 폴더가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-203">For example, if you have a controller named **HomeController**, the Views folder will contain a folder named Home.</span></span> <span data-ttu-id="7bf69-204">기본적으로 ASP.NET MVC 프레임 워크에서는 뷰를 찾습니다 Views\controllerName 폴더에 요청 된 뷰 이름으로.aspx 파일 (**[ControllerName] [작업] 보기.aspx**) 또는 (**뷰 [ControllerName] [작업].cshtml**) Razor 뷰의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-204">By default, when the ASP.NET MVC framework loads a view, it looks for an .aspx file with the requested view name in the Views\controllerName folder (**Views[ControllerName][Action].aspx**) or (**Views[ControllerName][Action].cshtml**) for Razor Views.</span></span>

      > [!NOTE]
      > <span data-ttu-id="7bf69-205">MVC 웹 응용 프로그램은 앞에서 설명한 폴더 외에도 사용 하 여는 **Global.asax** 전역 URL 라우팅 설정 하기 위해 파일 기본값을 사용 하는 **Web.config** 파일을 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-205">In addition to the folders listed previously, an MVC Web application uses the **Global.asax** file to set global URL routing defaults, and it uses the **Web.config** file to configure the application.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Adding_a_HomeController"></a>
#### <a name="task-3---adding-a-homecontroller"></a><span data-ttu-id="7bf69-206">작업 3-한 HomeController 추가</span><span class="sxs-lookup"><span data-stu-id="7bf69-206">Task 3 - Adding a HomeController</span></span>

<span data-ttu-id="7bf69-207">MVC 프레임 워크를 사용 하지 않는 ASP.NET 응용 프로그램에서 사용자 상호 작용을 발생 시키고 해당 페이지에서 이벤트를 처리 하 고 페이지를 중심 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-207">In ASP.NET applications that do not use the MVC framework, user interaction is organized around pages, and around raising and handling events from those pages.</span></span> <span data-ttu-id="7bf69-208">반면, ASP.NET MVC 응용 프로그램의 사용자 상호 컨트롤러 및 해당 작업 메서드를 중심으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-208">In contrast, user interaction with ASP.NET MVC applications is organized around controllers and their action methods.</span></span>

<span data-ttu-id="7bf69-209">반면에 ASP.NET MVC 프레임 워크는 컨트롤러로 참조 하는 클래스에 Url을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-209">On the other hand, ASP.NET MVC framework maps URLs to classes that are referred to as controllers.</span></span> <span data-ttu-id="7bf69-210">컨트롤러 들어오는 요청을 처리, 사용자 입력 및 상호 작용을 처리, 적절 한 응용 프로그램 논리를 실행 및 클라이언트에 다시 전송할 응답을 결정 (HTML을 표시, 파일을 다운로드, 등 다른 URL 리디렉션).</span><span class="sxs-lookup"><span data-stu-id="7bf69-210">Controllers process incoming requests, handle user input and interactions, execute appropriate application logic and determine the response to send back to the client (display HTML, download a file, redirect to a different URL, etc.).</span></span> <span data-ttu-id="7bf69-211">HTML을 표시 하는 경우 컨트롤러 클래스는 일반적으로 요청에 대 한 HTML 태그를 생성 하는 별도 뷰 구성 요소를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-211">In the case of displaying HTML, a controller class typically calls a separate view component to generate the HTML markup for the request.</span></span> <span data-ttu-id="7bf69-212">MVC 응용 프로그램에서 보기는 정보만 표시합니다. 컨트롤러가 사용자 입력 및 상호 작용을 처리하고 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-212">In an MVC application, the view only displays information; the controller handles and responds to user input and interaction.</span></span>

<span data-ttu-id="7bf69-213">이 태스크에서는 Music Store 사이트의 홈 페이지 Url을 처리 하는 컨트롤러 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-213">In this task, you will add a Controller class that will handle URLs to the Home page of the Music Store site.</span></span>

1. <span data-ttu-id="7bf69-214">마우스 오른쪽 단추로 클릭 **컨트롤러** 선택 솔루션 탐색기에서 폴더 **추가** 차례로 **컨트롤러** 명령:</span><span class="sxs-lookup"><span data-stu-id="7bf69-214">Right-click **Controllers** folder within the Solution Explorer, select **Add** and then **Controller** command:</span></span>

    <span data-ttu-id="7bf69-215">![컨트롤러 명령을 추가](aspnet-mvc-4-fundamentals/_static/image5.png "컨트롤러 명령 추가")</span><span class="sxs-lookup"><span data-stu-id="7bf69-215">![Add a Controller Command](aspnet-mvc-4-fundamentals/_static/image5.png "Add a Controller Command")</span></span>

    <span data-ttu-id="7bf69-216">*컨트롤러 명령 추가*</span><span class="sxs-lookup"><span data-stu-id="7bf69-216">*Add Controller Command*</span></span>
2. <span data-ttu-id="7bf69-217">**컨트롤러 추가** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-217">The **Add Controller** dialog appears.</span></span> <span data-ttu-id="7bf69-218">컨트롤러 이름을 *HomeController* 누릅니다 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-218">Name the controller *HomeController* and press **Add**.</span></span>

    <span data-ttu-id="7bf69-219">![컨트롤러 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image6.png "컨트롤러 추가 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="7bf69-219">![Add Controller Dialog](aspnet-mvc-4-fundamentals/_static/image6.png "Add Controller Dialog")</span></span>

    <span data-ttu-id="7bf69-220">*컨트롤러 추가 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="7bf69-220">*Add Controller Dialog*</span></span>
3. <span data-ttu-id="7bf69-221">파일 **HomeController.cs** 에서 만든는 **컨트롤러** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-221">The file **HomeController.cs** is created in the **Controllers** folder.</span></span> <span data-ttu-id="7bf69-222">가지려면는 **HomeController** 문자열을 반환 하는 인덱스 작업에서 교체는 **인덱스** 메서드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="7bf69-222">In order to have the **HomeController** return a string on its Index action, replace the **Index** method with the following code:</span></span>

    <span data-ttu-id="7bf69-223">(코드 조각- *기본 ASP.NET MVC 4-e x 1 HomeController 인덱스*)</span><span class="sxs-lookup"><span data-stu-id="7bf69-223">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex1 HomeController Index*)</span></span>


~~~
[!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample1.cs)]
~~~

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="7bf69-224">작업 4-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="7bf69-224">Task 4 - Running the Application</span></span>

<span data-ttu-id="7bf69-225">이 태스크에서는 웹 브라우저에서 응용 프로그램을 사용해 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-225">In this task, you will try out the Application in a web browser.</span></span>

1. <span data-ttu-id="7bf69-226">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-226">Press **F5** to run the Application.</span></span> <span data-ttu-id="7bf69-227">프로젝트를 컴파일할 하 고 로컬 IIS 웹 서버 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-227">The project is compiled and the local IIS Web Server starts.</span></span> <span data-ttu-id="7bf69-228">로컬 IIS 웹 서버는 웹 서버의 URL을 가리키는 웹 브라우저를 열고 자동으로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-228">The local IIS Web Server will automatically open a web browser pointing to the URL of the Web server.</span></span>

    <span data-ttu-id="7bf69-229">![웹 브라우저에서 실행 중인 응용 프로그램](aspnet-mvc-4-fundamentals/_static/image7.png "웹 브라우저에서 실행 중인 응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="7bf69-229">![Application running in a web browser](aspnet-mvc-4-fundamentals/_static/image7.png "Application running in a web browser")</span></span>

    <span data-ttu-id="7bf69-230">*웹 브라우저에서 실행 중인 응용 프로그램*</span><span class="sxs-lookup"><span data-stu-id="7bf69-230">*Application running in a web browser*</span></span>

    > [!NOTE]
    > <span data-ttu-id="7bf69-231">로컬 IIS 웹 서버는 임의의 가능한 포트 번호를에서 웹 사이트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-231">The local IIS Web Server will run the website on a random free port number.</span></span> <span data-ttu-id="7bf69-232">위 그림에는 사이트에서 실행 `http://localhost:50103/`, 50103 포트를 사용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-232">In the figure above, the site is running at `http://localhost:50103/`, so it's using port 50103.</span></span> <span data-ttu-id="7bf69-233">포트 번호가 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-233">Your port number may vary.</span></span>
2. <span data-ttu-id="7bf69-234">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-234">Close the browser.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Controller"></a>
### <a name="exercise-2-creating-a-controller"></a><span data-ttu-id="7bf69-235">연습 2: 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="7bf69-235">Exercise 2: Creating a Controller</span></span>

<span data-ttu-id="7bf69-236">이 연습에서는 음악 스토어 응용 프로그램의 간단한 기능을 구현 하는 컨트롤러를 업데이트 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-236">In this exercise, you will learn how to update the controller to implement simple functionality of the Music Store application.</span></span> <span data-ttu-id="7bf69-237">해당 컨트롤러는 각 다음과 같은 특정 요청을 처리 하는 작업 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-237">That controller will define action methods to handle each of the following specific requests:</span></span>

- <span data-ttu-id="7bf69-238">Music Store에서 음악 장르 목록 페이지</span><span class="sxs-lookup"><span data-stu-id="7bf69-238">A listing page of the music genres in the Music Store</span></span>
- <span data-ttu-id="7bf69-239">특정 장르에 대 한 음악 앨범을 모두 나열 하는 찾아보기 페이지</span><span class="sxs-lookup"><span data-stu-id="7bf69-239">A browse page that lists all of the music albums for a particular genre</span></span>
- <span data-ttu-id="7bf69-240">특정 음악 앨범에 대 한 정보를 표시 하는 세부 정보 페이지</span><span class="sxs-lookup"><span data-stu-id="7bf69-240">A details page that shows information about a specific music album</span></span>

<span data-ttu-id="7bf69-241">이 작업의 범위에 대해 단순히 해당 작업을 지금까지 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-241">For the scope of this exercise, those actions will simply return a string by now.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Adding_a_New_StoreController_Class"></a>
#### <a name="task-1---adding-a-new-storecontroller-class"></a><span data-ttu-id="7bf69-242">작업 1-새 StoreController 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="7bf69-242">Task 1 - Adding a New StoreController Class</span></span>

<span data-ttu-id="7bf69-243">이 태스크에서는 새 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-243">In this task, you will add a new Controller.</span></span>

1. <span data-ttu-id="7bf69-244">아직 열지 않은 경우 시작 **VS 2012 Web Express**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-244">If not already open, start **VS Express for Web 2012**.</span></span>
2. <span data-ttu-id="7bf69-245">에 **파일** 메뉴 선택 **프로젝트 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-245">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="7bf69-246">프로젝트 열기 대화 상자에서 찾은 **Source\Ex02 CreatingAController\Begin**선택, **Begin.sln** 클릭 **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-246">In the Open Project dialog, browse to **Source\Ex02-CreatingAController\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="7bf69-247">또는 계속 진행할 솔루션, 이전 연습을 완료 한 후 가져올 있음을 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-247">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="7bf69-248">제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면.</span><span class="sxs-lookup"><span data-stu-id="7bf69-248">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="7bf69-249">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-249">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="7bf69-250">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="7bf69-250">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="7bf69-251">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-251">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="7bf69-252">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-252">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="7bf69-253">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-253">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="7bf69-254">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-254">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="7bf69-255">새 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-255">Add the new controller.</span></span> <span data-ttu-id="7bf69-256">이렇게 하려면 마우스 오른쪽 단추로 클릭는 **컨트롤러** 선택 솔루션 탐색기에서 폴더 **추가** 차례로 **컨트롤러** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-256">To do this, right-click the **Controllers** folder within the Solution Explorer, select **Add** and then the **Controller** command.</span></span> <span data-ttu-id="7bf69-257">변경 된 **컨트롤러 이름** 를 *StoreController*를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-257">Change the **Controller Name** to *StoreController*, and click **Add**.</span></span>

    <span data-ttu-id="7bf69-258">![컨트롤러 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image8.png "컨트롤러 추가 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="7bf69-258">![Add Controller Dialog](aspnet-mvc-4-fundamentals/_static/image8.png "Add Controller Dialog")</span></span>

    <span data-ttu-id="7bf69-259">*컨트롤러 추가 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="7bf69-259">*Add Controller Dialog*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Modifying_the_StoreControllers_Actions"></a>
#### <a name="task-2---modifying-the-storecontrollers-actions"></a><span data-ttu-id="7bf69-260">작업 2-StoreController의 동작을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-260">Task 2 - Modifying the StoreController's Actions</span></span>

<span data-ttu-id="7bf69-261">이 작업을 호출 되는 컨트롤러 메서드를 수정 합니다 **동작**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-261">In this task, you will modify the Controller methods that are called **actions**.</span></span> <span data-ttu-id="7bf69-262">작업은 URL 요청을 처리 하 고 브라우저 또는 URL을 호출 하는 사용자에 게 다시 보내야 하는 내용을 결정 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-262">Actions are responsible for handling URL requests and determining the content that should be sent back to the browser or user that invoked the URL.</span></span>

1. <span data-ttu-id="7bf69-263">**StoreController** 클래스에 이미 있는 **인덱스** 메서드.</span><span class="sxs-lookup"><span data-stu-id="7bf69-263">The **StoreController** class already has an **Index** method.</span></span> <span data-ttu-id="7bf69-264">음악 스토어의 모든 장르 나열 되는 페이지를 구현 하려면이 랩에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-264">You will use it later in this Lab to implement the page that lists all genres of the music store.</span></span> <span data-ttu-id="7bf69-265">지금은 바꾸면는 **인덱스** 메서드는 문자열을 반환 하는 다음 코드를 &quot;Store.Index()에서 Hello&quot;:</span><span class="sxs-lookup"><span data-stu-id="7bf69-265">For now, just replace the **Index** method with the following code that returns a string &quot;Hello from Store.Index()&quot;:</span></span>

    <span data-ttu-id="7bf69-266">(코드 조각- *기본 ASP.NET MVC 4-e x 2 StoreController 인덱스*)</span><span class="sxs-lookup"><span data-stu-id="7bf69-266">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex2 StoreController Index*)</span></span>


~~~
[!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample2.cs)]
~~~
2. <span data-ttu-id="7bf69-267">추가 **찾아보기** 및 **세부 정보** 메서드.</span><span class="sxs-lookup"><span data-stu-id="7bf69-267">Add **Browse** and **Details** methods.</span></span> <span data-ttu-id="7bf69-268">이렇게 하려면 다음 코드를 추가 **StoreController**:</span><span class="sxs-lookup"><span data-stu-id="7bf69-268">To do this, add the following code to the **StoreController**:</span></span>

    <span data-ttu-id="7bf69-269">(코드 조각- *기본 ASP.NET MVC 4-e x 2 StoreController BrowseAndDetails*)</span><span class="sxs-lookup"><span data-stu-id="7bf69-269">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex2 StoreController BrowseAndDetails*)</span></span>


~~~
[!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample3.cs)]
~~~

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="7bf69-270">작업 3-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="7bf69-270">Task 3 - Running the Application</span></span>

<span data-ttu-id="7bf69-271">이 태스크에서는 웹 브라우저에서 응용 프로그램을 사용해 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-271">In this task, you will try out the Application in a web browser.</span></span>

1. <span data-ttu-id="7bf69-272">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-272">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="7bf69-273">프로젝트 시작 날짜는 **홈** 페이지.</span><span class="sxs-lookup"><span data-stu-id="7bf69-273">The project starts in the **Home** page.</span></span> <span data-ttu-id="7bf69-274">각 동작의 구현을 확인 하려면 URL을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-274">Change the URL to verify each action's implementation.</span></span>

    1. <span data-ttu-id="7bf69-275">**/ 저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-275">**/Store**.</span></span> <span data-ttu-id="7bf69-276">나타납니다  **&quot;Store.Index()에서 Hello&quot;**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-276">You will see **&quot;Hello from Store.Index()&quot;**.</span></span>
    2. <span data-ttu-id="7bf69-277">**/ 저장소/찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-277">**/Store/Browse**.</span></span> <span data-ttu-id="7bf69-278">나타납니다  **&quot;Store.Browse()에서 Hello&quot;**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-278">You will see **&quot;Hello from Store.Browse()&quot;**.</span></span>
    3. <span data-ttu-id="7bf69-279">**/ 저장소/세부 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-279">**/Store/Details**.</span></span> <span data-ttu-id="7bf69-280">나타납니다  **&quot;Store.Details()에서 Hello&quot;**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-280">You will see **&quot;Hello from Store.Details()&quot;**.</span></span>

        <span data-ttu-id="7bf69-281">![StoreBrowse 검색](aspnet-mvc-4-fundamentals/_static/image9.png "StoreBrowse 검색")</span><span class="sxs-lookup"><span data-stu-id="7bf69-281">![Browsing StoreBrowse](aspnet-mvc-4-fundamentals/_static/image9.png "Browsing StoreBrowse")</span></span>

        <span data-ttu-id="7bf69-282">*/Store/Browse 검색*</span><span class="sxs-lookup"><span data-stu-id="7bf69-282">*Browsing /Store/Browse*</span></span>
3. <span data-ttu-id="7bf69-283">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-283">Close the browser.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Passing_parameters_to_a_Controller"></a>
### <a name="exercise-3-passing-parameters-to-a-controller"></a><span data-ttu-id="7bf69-284">연습 3: 컨트롤러에 매개 변수 전달</span><span class="sxs-lookup"><span data-stu-id="7bf69-284">Exercise 3: Passing parameters to a Controller</span></span>

<span data-ttu-id="7bf69-285">지금까지 있습니다 있는 된 문자열을 반환 상수는 컨트롤러에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-285">Until now, you have been returning constant strings from the Controllers.</span></span> <span data-ttu-id="7bf69-286">이 연습에서는 컨트롤러의 URL과 쿼리 문자열을 사용 하 여 하 고 다음 브라우저에 텍스트를 사용 하 여 응답할 메서드 동작에 매개 변수를 전달 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-286">In this exercise you will learn how to pass parameters to a Controller using the URL and querystring, and then making the method actions respond with text to the browser.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Adding_Genre_Parameter_to_StoreController"></a>
#### <a name="task-1---adding-genre-parameter-to-storecontroller"></a><span data-ttu-id="7bf69-287">작업 1-StoreController 추가 장르 매개 변수</span><span class="sxs-lookup"><span data-stu-id="7bf69-287">Task 1 - Adding Genre Parameter to StoreController</span></span>

<span data-ttu-id="7bf69-288">이 작업을 사용 하 여는 **querystring** 매개 변수를 보낼는 **찾아보기** 의 동작 메서드에 **StoreController**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-288">In this task, you will use the **querystring** to send parameters to the **Browse** action method in the **StoreController**.</span></span>

1. <span data-ttu-id="7bf69-289">아직 열지 않은 경우 시작 **VS Express for Web**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-289">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="7bf69-290">에 **파일** 메뉴 선택 **프로젝트 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-290">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="7bf69-291">프로젝트 열기 대화 상자에서 찾은 **Source\Ex03 PassingParametersToAController\Begin**선택, **Begin.sln** 클릭 **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-291">In the Open Project dialog, browse to **Source\Ex03-PassingParametersToAController\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="7bf69-292">또는 계속 진행할 솔루션, 이전 연습을 완료 한 후 가져올 있음을 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-292">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="7bf69-293">제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면.</span><span class="sxs-lookup"><span data-stu-id="7bf69-293">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="7bf69-294">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-294">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="7bf69-295">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="7bf69-295">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="7bf69-296">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-296">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="7bf69-297">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-297">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="7bf69-298">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-298">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="7bf69-299">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-299">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="7bf69-300">열기 **StoreController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-300">Open **StoreController** class.</span></span> <span data-ttu-id="7bf69-301">이 수행 하는 **솔루션 탐색기**를 확장 하 고는 **컨트롤러** 폴더를 두 번 클릭 **StoreController.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-301">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
4. <span data-ttu-id="7bf69-302">변경 된 **찾아보기** 메서드를 특정 장르를 요청 하려면 문자열 매개 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-302">Change the **Browse** method, adding a string parameter to request for a specific genre.</span></span> <span data-ttu-id="7bf69-303">ASP.NET MVC 자동으로 모든 쿼리 문자열을 통과 또는 폼 게시 매개 변수 라는 **장르** 호출 될 때이 동작 메서드에 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-303">ASP.NET MVC will automatically pass any querystring or form post parameters named **genre** to this action method when invoked.</span></span> <span data-ttu-id="7bf69-304">이 작업을 수행 하려면 대체는 **찾아보기** 메서드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="7bf69-304">To do this, replace the **Browse** method with the following code:</span></span>

    <span data-ttu-id="7bf69-305">(코드 조각- *기본 ASP.NET MVC 4-Ex3 StoreController BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="7bf69-305">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex3 StoreController BrowseMethod*)</span></span>


~~~
[!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample4.cs)]

> [!NOTE]
> You are using the **HttpUtility.HtmlEncode** utility method to prevents users from injecting Javascript into the View with a link like **/Store/Browse?Genre=&lt;script&gt;window.location='[http://hackersite.com](http://hackersite.com)'&lt;/script&gt;**.
> 
> For further explanation, please visit [this msdn article](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx).
~~~

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="7bf69-306">작업 2-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="7bf69-306">Task 2 - Running the Application</span></span>

<span data-ttu-id="7bf69-307">이 작업은 웹 브라우저에서 응용 프로그램 사용을 하 여 사용 하는 **장르** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-307">In this task, you will try out the Application in a web browser and use the **genre** parameter.</span></span>

1. <span data-ttu-id="7bf69-308">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-308">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="7bf69-309">프로젝트 시작 날짜는 **홈** 페이지.</span><span class="sxs-lookup"><span data-stu-id="7bf69-309">The project starts in the **Home** page.</span></span> <span data-ttu-id="7bf69-310">URL을 변경 *찾아보기/저장 /? Genre Disco =* 동작 장르 매개 변수를 수신 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-310">Change the URL to */Store/Browse?Genre=Disco* to verify that the action receives the genre parameter.</span></span>

    <span data-ttu-id="7bf69-311">![StoreBrowseGenre 검색 Disco =](aspnet-mvc-4-fundamentals/_static/image10.png "StoreBrowseGenre 검색 Disco =")</span><span class="sxs-lookup"><span data-stu-id="7bf69-311">![Browsing StoreBrowseGenre=Disco](aspnet-mvc-4-fundamentals/_static/image10.png "Browsing StoreBrowseGenre=Disco")</span></span>

    <span data-ttu-id="7bf69-312">*검색 /Store/Browse? Genre Disco =*</span><span class="sxs-lookup"><span data-stu-id="7bf69-312">*Browsing /Store/Browse?Genre=Disco*</span></span>
3. <span data-ttu-id="7bf69-313">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-313">Close the browser.</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Adding_an_Id_Parameter_Embedded_in_the_URL"></a>
#### <a name="task-3---adding-an-id-parameter-embedded-in-the-url"></a><span data-ttu-id="7bf69-314">작업 3-URL에 포함 하는 Id 매개 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-314">Task 3 - Adding an Id Parameter Embedded in the URL</span></span>

<span data-ttu-id="7bf69-315">이 작업을 사용 하 여는 **URL** 전달 하는 **Id** 매개 변수는 **세부 정보** 의 동작 메서드는 **StoreController**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-315">In this task, you will use the **URL** to pass an **Id** parameter to the **Details** action method of the **StoreController**.</span></span> <span data-ttu-id="7bf69-316">ASP.NET MVC의 기본 매개 변수 이름으로 작업 메서드 이름 뒤에 오는 URL의 세그먼트를 처리 하는 라우팅 규칙 **Id**합니다. 작업 메서드에 매개 변수 Id 라는 경우 다음 ASP.NET MVC는 자동으로 URL 세그먼트를 매개 변수로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-316">ASP.NET MVC's default routing convention is to treat the segment of a URL after the action method name as a parameter named **Id**. If your action method has parameter named Id, then ASP.NET MVC will automatically pass the URL segment to you as a parameter.</span></span> <span data-ttu-id="7bf69-317">URL에서 **저장소/세부 정보/5**, **Id** 로 해석 됩니다 **5**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-317">In the URL **Store/Details/5**, **Id** will be interpreted as **5**.</span></span>

1. <span data-ttu-id="7bf69-318">변경 된 **세부 정보** 의 메서드는 **StoreController**추가는 **int** 라는 매개 변수 **id**합니다. 이 작업을 수행 하려면 대체는 **세부 정보** 메서드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="7bf69-318">Change the **Details** method of the **StoreController**, adding an **int** parameter called **id**. To do this, replace the **Details** method with the following code:</span></span>

    <span data-ttu-id="7bf69-319">(코드 조각- *기본 ASP.NET MVC 4-Ex3 StoreController DetailsMethod*)</span><span class="sxs-lookup"><span data-stu-id="7bf69-319">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex3 StoreController DetailsMethod*)</span></span>


~~~
[!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample5.cs)]
~~~

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="7bf69-320">작업 4-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="7bf69-320">Task 4 - Running the Application</span></span>

<span data-ttu-id="7bf69-321">이 작업은 웹 브라우저에서 응용 프로그램 사용을 하 여 사용 하는 **Id** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-321">In this task, you will try out the Application in a web browser and use the **Id** parameter.</span></span>

1. <span data-ttu-id="7bf69-322">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-322">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="7bf69-323">프로젝트 시작 날짜는 **홈** 페이지.</span><span class="sxs-lookup"><span data-stu-id="7bf69-323">The project starts in the **Home** page.</span></span> <span data-ttu-id="7bf69-324">URL을 변경 */Store/Details/5* 동작 id 매개 변수를 수신 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-324">Change the URL to */Store/Details/5* to verify that the action receives the id parameter.</span></span>

    <span data-ttu-id="7bf69-325">![StoreDetails5 검색](aspnet-mvc-4-fundamentals/_static/image11.png "StoreDetails5 검색")</span><span class="sxs-lookup"><span data-stu-id="7bf69-325">![Browsing StoreDetails5](aspnet-mvc-4-fundamentals/_static/image11.png "Browsing StoreDetails5")</span></span>

    <span data-ttu-id="7bf69-326">*/Store/Details/5 검색*</span><span class="sxs-lookup"><span data-stu-id="7bf69-326">*Browsing /Store/Details/5*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Creating_a_View"></a>
### <a name="exercise-4-creating-a-view"></a><span data-ttu-id="7bf69-327">보기를 만드는 연습 4:</span><span class="sxs-lookup"><span data-stu-id="7bf69-327">Exercise 4: Creating a View</span></span>

<span data-ttu-id="7bf69-328">지금까지 있습니다 있는 된 문자열에서에서 반환 컨트롤러 작업.</span><span class="sxs-lookup"><span data-stu-id="7bf69-328">So far you have been returning strings from controller actions.</span></span> <span data-ttu-id="7bf69-329">컨트롤러의 작동 방식을 이해 하는 데 도움이 되 이지만 실제 웹 응용 프로그램은 작성 하는 방법에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-329">Although that is a useful way of understanding how controllers work, it is not how your real Web applications are built.</span></span> <span data-ttu-id="7bf69-330">뷰는 다시 템플릿 파일을 사용 하 여 브라우저에 HTML을 생성 하기 위한 더 나은 방법은 제공 하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-330">Views are components that provide a better approach for generating HTML back to the browser with the use of template files.</span></span>

<span data-ttu-id="7bf69-331">이 연습에서는 공통 HTML 콘텐츠, 사이트 및 마지막으로 HomeController HTML을 반환할 수 있도록 뷰 템플릿을의 모양과 느낌을 개선 하는 스타일 시트에 대 한 템플릿을 설정 하는 레이아웃 마스터 페이지를 추가 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-331">In this exercise you will learn how to add a layout master page to setup a template for common HTML content, a StyleSheet to enhance the look and feel of the site and finally a View template to enable HomeController to return HTML.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Modifying_the_file__layoutcshtml"></a>
#### <a name="task-1---modifying-the-file-layoutcshtml"></a><span data-ttu-id="7bf69-332">작업 파일을 수정 하는 1- \_layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="7bf69-332">Task 1 - Modifying the file \_layout.cshtml</span></span>

<span data-ttu-id="7bf69-333">파일 **~/Views/Shared/\_layout.cshtml** 전체 웹 사이트에 대해 사용 하는 일반적인 HTML에 대 한 템플릿을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-333">The file **~/Views/Shared/\_layout.cshtml** allows you to setup a template for common HTML to use across the entire website.</span></span> <span data-ttu-id="7bf69-334">이 작업 홈 페이지 및 저장소 영역에 대 한 링크가 있는 일반적인 헤더로 레이아웃 마스터 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-334">In this task you will add a layout master page with a common header with links to the Home page and Store area.</span></span>

1. <span data-ttu-id="7bf69-335">아직 열지 않은 경우 시작 **VS Express for Web**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-335">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="7bf69-336">에 **파일** 메뉴 선택 **프로젝트 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-336">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="7bf69-337">프로젝트 열기 대화 상자에서 찾은 **Source\Ex04 CreatingAView\Begin**선택, **Begin.sln** 클릭 **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-337">In the Open Project dialog, browse to **Source\Ex04-CreatingAView\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="7bf69-338">또는 계속 진행할 솔루션, 이전 연습을 완료 한 후 가져올 있음을 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-338">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="7bf69-339">제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면.</span><span class="sxs-lookup"><span data-stu-id="7bf69-339">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="7bf69-340">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-340">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="7bf69-341">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="7bf69-341">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="7bf69-342">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-342">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="7bf69-343">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-343">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="7bf69-344">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-344">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="7bf69-345">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-345">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="7bf69-346">파일  <strong>\_layout.cshtml</strong> 사이트에 있는 모든 페이지에 대 한 HTML 컨테이너 레이아웃을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-346">The file <strong>\_layout.cshtml</strong> contains the HTML container layout for all pages on the site.</span></span> <span data-ttu-id="7bf69-347">여기에 포함 됩니다는 <strong>&lt;html&gt;</strong> HTML 응답에 대 한 요소와 <strong>&lt;h e a d&gt;</strong> 및 <strong>&lt;본문&gt;</strong> 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-347">It includes the <strong>&lt;html&gt;</strong> element for the HTML response, as well as the <strong>&lt;head&gt;</strong> and <strong>&lt;body&gt;</strong> elements.</span></span> <span data-ttu-id="7bf69-348"><strong>@RenderBody()</strong> HTML 내에서 본문 영역을 확인할 해당 보기 서식 파일은 동적 콘텐츠를 사용 하 여 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-348"><strong>@RenderBody()</strong> within the HTML body identify regions that view templates will be able to fill in with dynamic content.</span></span>
   <span data-ttu-id="7bf69-349">(C#)</span><span class="sxs-lookup"><span data-stu-id="7bf69-349">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample6.cshtml)]
4. <span data-ttu-id="7bf69-350">사이트의 모든 페이지에 홈 페이지 및 저장소 영역을 링크와 함께 공용 헤더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-350">Add a common header with links to the Home page and Store area on all pages in the site.</span></span> <span data-ttu-id="7bf69-351">파일을 수집 하려면 아래에 다음 코드를 추가 &lt;본문&gt; 문.</span><span class="sxs-lookup"><span data-stu-id="7bf69-351">In order to do that, add the following code below &lt;body&gt; statement.</span></span>
   <span data-ttu-id="7bf69-352">(C#)</span><span class="sxs-lookup"><span data-stu-id="7bf69-352">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample7.cshtml)]
5. <span data-ttu-id="7bf69-353">각 페이지의 본문 섹션을 렌더링 하는 div를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-353">Include a div to render the body section of each page.</span></span> <span data-ttu-id="7bf69-354">대체  <strong>@RenderBody()</strong> 다음 higlighted 코드로: (C#)</span><span class="sxs-lookup"><span data-stu-id="7bf69-354">Replace <strong>@RenderBody()</strong> with the following higlighted code: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample8.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="7bf69-355">알고 계십니까?</span><span class="sxs-lookup"><span data-stu-id="7bf69-355">Did you know?</span></span> <span data-ttu-id="7bf69-356">Visual Studio 2012는 HTML, 코드 파일의 자주 사용 되는 코드를 추가 하기 쉽도록 코드 조각을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-356">Visual Studio 2012 has snippets that make it easy to add commonly used code in HTML, code files and more!</span></span> <span data-ttu-id="7bf69-357">입력 하 여 확인해 **&lt;div&gt;** 한 키를 눌러 **탭** 전체 삽입을 두 번 **div** 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-357">Try it out by typing **&lt;div&gt;** and pressing **TAB** twice to insert a complete **div** tag.</span></span>

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_CSS_Stylesheet"></a>
#### <a name="task-2---adding-css-stylesheet"></a><span data-ttu-id="7bf69-358">작업 2-CSS 스타일 시트를 추가</span><span class="sxs-lookup"><span data-stu-id="7bf69-358">Task 2 - Adding CSS Stylesheet</span></span>

<span data-ttu-id="7bf69-359">빈 프로젝트 템플릿은 기본 형태 및 유효성 검사 메시지를 표시 하는 데 사용 되는 스타일을 포함 하는 매우 간소화 된 CSS 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-359">The empty project template includes a very streamlined CSS file which just includes styles used to display basic forms and validation messages.</span></span> <span data-ttu-id="7bf69-360">사이트의 모양과 느낌을 개선 하기 위해 추가 CSS 및 이미지 (잠재적으로 디자이너에서 제공)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-360">You will use additional CSS and images (potentially provided by a designer) in order to enhance the look and feel of the site.</span></span>

<span data-ttu-id="7bf69-361">이 태스크에서는 해당 사이트의 스타일을 정의 하는 CSS 스타일 시트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-361">In this task, you will add a CSS stylesheet to define the styles of the site.</span></span>

1. <span data-ttu-id="7bf69-362">CSS 파일 및 이미지에 포함 됩니다는 **Source\Assets\Content** 이 랩의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-362">The CSS file and images are included in the **Source\Assets\Content** folder of this Lab.</span></span> <span data-ttu-id="7bf69-363">응용 프로그램에 기호를 추가 하기 위해 자신의 콘텐츠를 끌어 한 **Windows 탐색기** 창에는 **솔루션 탐색기** Visual Studio express for Web을 아래와 같이:</span><span class="sxs-lookup"><span data-stu-id="7bf69-363">In order to add them to the application, drag their content from a **Windows Explorer** window into the **Solution Explorer** in Visual Studio Express for Web, as shown below:</span></span>

    <span data-ttu-id="7bf69-364">![스타일 내용을 끌어](aspnet-mvc-4-fundamentals/_static/image12.png "끌어 스타일 내용")</span><span class="sxs-lookup"><span data-stu-id="7bf69-364">![Dragging style contents](aspnet-mvc-4-fundamentals/_static/image12.png "Dragging style contents")</span></span>

    <span data-ttu-id="7bf69-365">*스타일 내용을 끌기*</span><span class="sxs-lookup"><span data-stu-id="7bf69-365">*Dragging style contents*</span></span>
2. <span data-ttu-id="7bf69-366">경고 대화 상자가 표시 됩니다, 대체할 것인지 확인 하 라는 **Site.css** 파일 및 일부 기존 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-366">A warning dialog will appear, asking for confirmation to replace **Site.css** file and some existing images.</span></span> <span data-ttu-id="7bf69-367">확인 **전체 적용** 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-367">Check **Apply to all items** and click **Yes**.</span></span>

<a id="Ex4Task3"></a>

<a id="Task_3_-_Adding_a_View_Template"></a>
#### <a name="task-3---adding-a-view-template"></a><span data-ttu-id="7bf69-368">작업 3-보기 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="7bf69-368">Task 3 - Adding a View Template</span></span>

<span data-ttu-id="7bf69-369">이 작업에서는 레이아웃 마스터 페이지를 사용 하 여 HTML 응답을 생성 하는 보기 템플릿을 추가한 하 고 CSS이이 연습에서는 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-369">In this task, you will add a View template to generate the HTML response that will use the layout master page and CSS added in this exercise.</span></span>

1. <span data-ttu-id="7bf69-370">사이트의 홈 페이지를 검색할 때 뷰 템플릿을 사용 하려면 먼저 해야 합니다는 문자열을 반환 하는 대신 있음을 **HomeController 인덱스** 메서드는 반환는 **보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-370">To use a View template when browsing the site's home page, you will first need to indicate that instead of returning a string, the **HomeController Index** method will return a **View**.</span></span> <span data-ttu-id="7bf69-371">열기 **HomeController** 클래스 및 변경의 **인덱스** 반환 하는 메서드는 **ActionResult**, 고 반환 하도록 **View()**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-371">Open **HomeController** class and change its **Index** method to return an **ActionResult**, and have it return **View()**.</span></span>

    <span data-ttu-id="7bf69-372">(코드 조각- *기본 ASP.NET MVC 4-Ex4 HomeController 인덱스*)</span><span class="sxs-lookup"><span data-stu-id="7bf69-372">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex4 HomeController Index*)</span></span>


~~~
[!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample9.cs)]
~~~
2. <span data-ttu-id="7bf69-373">이제는 적절 한 템플릿 보기를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-373">Now, you need to add an appropriate View template.</span></span> <span data-ttu-id="7bf69-374">이렇게 하려면 **마우스 오른쪽 단추로 클릭** 내는 **인덱스** 동작 메서드와 선택 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-374">To do this, **right-click** inside the **Index** action method and select **Add View**.</span></span> <span data-ttu-id="7bf69-375">그러면 표시 됩니다는 **뷰 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="7bf69-375">This will bring up the **Add View** dialog.</span></span>

    <span data-ttu-id="7bf69-376">![Index 메서드 내에서 뷰 추가](aspnet-mvc-4-fundamentals/_static/image13.png "인덱스 메서드 내에서 뷰를 추가 합니다.")</span><span class="sxs-lookup"><span data-stu-id="7bf69-376">![Adding a View from within the Index method](aspnet-mvc-4-fundamentals/_static/image13.png "Adding a View from within the Index method")</span></span>

    <span data-ttu-id="7bf69-377">*Index 메서드 내에서 뷰를 추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="7bf69-377">*Adding a View from within the Index method*</span></span>
3. <span data-ttu-id="7bf69-378">**뷰 추가** 보기 템플릿 파일을 생성 하려면 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-378">The **Add View** Dialog will appear to generate a View template file.</span></span> <span data-ttu-id="7bf69-379">기본적으로이 대화 상자 미리 채웁니다 보기 서식 파일의 이름을 사용 하 여 동작 메서드가 일치 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-379">By default, this dialog pre-populates the name of the View template so that it matches the action method that will use it.</span></span> <span data-ttu-id="7bf69-380">사용 했기 때문에 **뷰 추가** 내 상황에 맞는 메뉴는 **인덱스** 고 HomeController 내에서 작업 메서드는 **뷰 추가** 대화 상자에 기본 보기 이름으로 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-380">Because you used the **Add View** context menu within the **Index** action method within the HomeController, the **Add View** dialog has Index as the default view name.</span></span> <span data-ttu-id="7bf69-381">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-381">Click **Add**.</span></span>

    <span data-ttu-id="7bf69-382">![뷰 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image14.png "뷰 추가 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="7bf69-382">![Add View Dialog](aspnet-mvc-4-fundamentals/_static/image14.png "Add View Dialog")</span></span>

    <span data-ttu-id="7bf69-383">*뷰 추가 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="7bf69-383">*Add View Dialog*</span></span>
4. <span data-ttu-id="7bf69-384">Visual Studio에서 생성 한 **Index.cshtml** 내 템플릿 보기는 **Views\Home** 폴더를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-384">Visual Studio generates an **Index.cshtml** view template inside the **Views\Home** folder and then opens it.</span></span>

    <span data-ttu-id="7bf69-385">![생성 된 인덱스 뷰 홈](aspnet-mvc-4-fundamentals/_static/image15.png "홈 인덱스 뷰 생성")</span><span class="sxs-lookup"><span data-stu-id="7bf69-385">![Home Index view created](aspnet-mvc-4-fundamentals/_static/image15.png "Home Index view created")</span></span>

    <span data-ttu-id="7bf69-386">*만든 홈 인덱스 뷰*</span><span class="sxs-lookup"><span data-stu-id="7bf69-386">*Home Index view created*</span></span>

    > [!NOTE]
    > <span data-ttu-id="7bf69-387">이름 및 위치는 **Index.cshtml** 파일은 관련 되며 기본 ASP.NET MVC 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-387">name and location of the **Index.cshtml** file is relevant and follows the default ASP.NET MVC naming conventions.</span></span>
    > 
    > <span data-ttu-id="7bf69-388">폴더 \Views\**홈** 컨트롤러 이름과 일치 (**홈** 컨트롤러).</span><span class="sxs-lookup"><span data-stu-id="7bf69-388">The folder \Views\**Home** matches the controller name (**Home** Controller).</span></span> <span data-ttu-id="7bf69-389">보기 템플릿 이름 (**인덱스**), 보기를 표시 하는 컨트롤러 동작 메서드에 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-389">The View template name (**Index**), matches the controller action method which will be displaying the View.</span></span>
    > 
    > <span data-ttu-id="7bf69-390">이러한 방식으로 ASP.NET MVC는 뷰를 반환 하려면이 명명 규칙을 사용 하는 경우 이름 또는 뷰 서식 파일의 위치를 명시적으로 지정 하지 않아도 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-390">This way, ASP.NET MVC avoids having to explicitly specify the name or location of a View template when using this naming convention to return a View.</span></span>
5. <span data-ttu-id="7bf69-391">생성된 된 뷰 템플릿을 기반으로  **\_layout.cshtml** 템플릿을 이전에 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-391">The generated View template is based on the **\_layout.cshtml** template earlier defined.</span></span> <span data-ttu-id="7bf69-392">ViewBag.Title 속성을 업데이트 **홈**, 주 콘텐츠를 변경 하 고 **는 홈 페이지**아래 코드에 표시 된 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="7bf69-392">Update the ViewBag.Title property to **Home**, and change the main content to **This is the Home Page**, as shown in the code below:</span></span>


~~~
[!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample10.cshtml)]
~~~
6. <span data-ttu-id="7bf69-393">선택 **MvcMusicStore** 누릅니다 솔루션 탐색기에서 프로젝트 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-393">Select **MvcMusicStore** project in the Solution Explorer and Press **F5** to run the Application.</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_Verification"></a>
#### <a name="task-4-verification"></a><span data-ttu-id="7bf69-394">태스크 4: 확인</span><span class="sxs-lookup"><span data-stu-id="7bf69-394">Task 4: Verification</span></span>

<span data-ttu-id="7bf69-395">이전 연습에서 모든 단계를 올바르게 수행 했는지를 확인 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-395">In order to verify that you have correctly performed all the steps in the previous exercise, proceed as follows:</span></span>

<span data-ttu-id="7bf69-396">브라우저에서 열 응용 프로그램과 함께 있습니다 한다는 점에 유의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-396">With the application opened in a browser, you should note that:</span></span>

1. <span data-ttu-id="7bf69-397">HomeController의 Index 작업 메서드의 발견 하 고 표시 되는 **\Views\Home\Index.cshtml** 코드가 있더라도 서식 파일을 볼 **View() 반환**뒤에 템플릿 보기 때문에 표준 명명 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-397">The HomeController's Index action method found and displayed the **\Views\Home\Index.cshtml** View template, even though the code called **return View()**, because the View template followed the standard naming convention.</span></span>
2. <span data-ttu-id="7bf69-398">내에 정의 된 환영 메시지를 표시 하는 홈 페이지는 **\Views\Home\Index.cshtml** 템플릿 보기.</span><span class="sxs-lookup"><span data-stu-id="7bf69-398">The Home Page displays the welcome message defined within the **\Views\Home\Index.cshtml** view template.</span></span>
3. <span data-ttu-id="7bf69-399">홈 페이지를 사용 하 여  **\_layout.cshtml** 서식 파일을 시작 메시지 표준 사이트 HTML 레이아웃 내에 포함 되어 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-399">The Home Page is using the **\_layout.cshtml** template, and so the welcome message is contained within the standard site HTML layout.</span></span>

    <span data-ttu-id="7bf69-400">![정의 된 LayoutPage 및 스타일을 사용 하 여 인덱스 뷰 홈](aspnet-mvc-4-fundamentals/_static/image16.png "정의 LayoutPage 및 스타일을 사용 하 여 인덱스 뷰 홈")</span><span class="sxs-lookup"><span data-stu-id="7bf69-400">![Home Index View using the defined LayoutPage and style](aspnet-mvc-4-fundamentals/_static/image16.png "Home Index View using the defined LayoutPage and style")</span></span>

    <span data-ttu-id="7bf69-401">*정의 된 LayoutPage 및 스타일을 사용 하 여 홈 인덱스 뷰*</span><span class="sxs-lookup"><span data-stu-id="7bf69-401">*Home Index View using the defined LayoutPage and style*</span></span>

<a id="Exercise5"></a>

<a id="Exercise_5_Creating_a_View_Model"></a>
### <a name="exercise-5-creating-a-view-model"></a><span data-ttu-id="7bf69-402">연습 5: 뷰 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="7bf69-402">Exercise 5: Creating a View Model</span></span>

<span data-ttu-id="7bf69-403">지금까지 하드 코드 된 HTML을 표시 하 여 보기를 수행 하지만 동적 웹 응용 프로그램을 만들려면 템플릿 보기 받아야 정보 컨트롤러에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-403">So far, you made your Views display hardcoded HTML, but, in order to create dynamic web applications, the View template should receive information from the Controller.</span></span> <span data-ttu-id="7bf69-404">해당 용도로 사용할 일반적인 기술이 **ViewModel** 패턴을 적절 한 HTML 응답을 생성 하는 데 필요한 모든 정보를 패키지 하려면 컨트롤러가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-404">One common technique to be used for that purpose is the **ViewModel** pattern, which allows a Controller to package up all the information needed to generate the appropriate HTML response.</span></span>

<span data-ttu-id="7bf69-405">이 연습에서는 ViewModel 클래스를 만들고 필요한 속성을 추가 하는 방법을 배우게 됩니다: 저장소 및 해당 장르 목록에는 장르의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-405">In this exercise, you will learn how to create a ViewModel class and add the required properties: the number of genres in the store and a list of those genres.</span></span> <span data-ttu-id="7bf69-406">만든된 ViewModel 사용할 StoreController도 업데이트 됩니다 하 고 마지막으로 페이지에서 언급 한 속성을 표시 하는 새 보기 템플릿 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-406">You will also update the StoreController to use the created ViewModel, and finally, you will create a new View template that will display the mentioned properties in the page.</span></span>

<a id="Ex5Task1"></a>

<a id="Task_1_-_Creating_a_ViewModel_Class"></a>
#### <a name="task-1---creating-a-viewmodel-class"></a><span data-ttu-id="7bf69-407">작업 1-ViewModel 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="7bf69-407">Task 1 - Creating a ViewModel Class</span></span>

<span data-ttu-id="7bf69-408">이 작업은 저장소 장르 목록 시나리오를 구현 하는 ViewModel 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-408">In this task, you will create a ViewModel class that will implement the Store genre listing scenario.</span></span>

1. <span data-ttu-id="7bf69-409">아직 열지 않은 경우 시작 **VS Express for Web**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-409">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="7bf69-410">에 **파일** 메뉴 선택 **프로젝트 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-410">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="7bf69-411">프로젝트 열기 대화 상자에서 찾은 **Source\Ex05 CreatingAViewModel\Begin**선택, **Begin.sln** 클릭 **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-411">In the Open Project dialog, browse to **Source\Ex05-CreatingAViewModel\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="7bf69-412">또는 계속 진행할 솔루션, 이전 연습을 완료 한 후 가져올 있음을 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-412">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="7bf69-413">제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면.</span><span class="sxs-lookup"><span data-stu-id="7bf69-413">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="7bf69-414">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-414">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="7bf69-415">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="7bf69-415">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="7bf69-416">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-416">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="7bf69-417">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-417">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="7bf69-418">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-418">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="7bf69-419">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-419">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="7bf69-420">만들기는 **Viewmodel** ViewModel 보관할 폴더를 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-420">Create a **ViewModels** folder to hold the ViewModel.</span></span> <span data-ttu-id="7bf69-421">이렇게 하려면 마우스 오른쪽 단추로 클릭 최상위 **MvcMusicStore** 프로젝트를 **추가** 차례로 **새 폴더**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-421">To do this, right-click the top-level **MvcMusicStore** project, select **Add** and then **New Folder**.</span></span>

    <span data-ttu-id="7bf69-422">![새 폴더 추가](aspnet-mvc-4-fundamentals/_static/image17.png "새 폴더 추가")</span><span class="sxs-lookup"><span data-stu-id="7bf69-422">![Adding a new folder](aspnet-mvc-4-fundamentals/_static/image17.png "Adding a new folder")</span></span>

    <span data-ttu-id="7bf69-423">*새 폴더 추가*</span><span class="sxs-lookup"><span data-stu-id="7bf69-423">*Adding a new folder*</span></span>
4. <span data-ttu-id="7bf69-424">폴더 이름을 *Viewmodel*합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-424">Name the folder *ViewModels*.</span></span>

    <span data-ttu-id="7bf69-425">![솔루션 탐색기에서 폴더 Viewmodel](aspnet-mvc-4-fundamentals/_static/image18.png "솔루션 탐색기에서 Viewmodel 폴더")</span><span class="sxs-lookup"><span data-stu-id="7bf69-425">![ViewModels folder in Solution Explorer](aspnet-mvc-4-fundamentals/_static/image18.png "ViewModels folder in Solution Explorer")</span></span>

    <span data-ttu-id="7bf69-426">*솔루션 탐색기에서 Viewmodel 폴더*</span><span class="sxs-lookup"><span data-stu-id="7bf69-426">*ViewModels folder in Solution Explorer*</span></span>
5. <span data-ttu-id="7bf69-427">만들기는 **ViewModel** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-427">Create a **ViewModel** class.</span></span> <span data-ttu-id="7bf69-428">이렇게 하려면 마우스 오른쪽 단추로 클릭는 **Viewmodel** 최근에 만든 폴더를 선택 **추가** 차례로 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-428">To do this, right-click on the **ViewModels** folder recently created, select **Add** and then **New Item**.</span></span> <span data-ttu-id="7bf69-429">아래 **코드**, 선택는 **클래스** 항목 및 파일 이름을 *StoreIndexViewModel.cs*, 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-429">Under **Code**, choose the **Class** item and name the file *StoreIndexViewModel.cs*, then click **Add**.</span></span>

    <span data-ttu-id="7bf69-430">![새 클래스 추가](aspnet-mvc-4-fundamentals/_static/image19.png "새 클래스 추가")</span><span class="sxs-lookup"><span data-stu-id="7bf69-430">![Adding a new Class](aspnet-mvc-4-fundamentals/_static/image19.png "Adding a new Class")</span></span>

    <span data-ttu-id="7bf69-431">*새 클래스 추가*</span><span class="sxs-lookup"><span data-stu-id="7bf69-431">*Adding a new Class*</span></span>

    <span data-ttu-id="7bf69-432">![StoreIndexViewModel 클래스 만들기](aspnet-mvc-4-fundamentals/_static/image20.png "만드는 StoreIndexViewModel 클래스")</span><span class="sxs-lookup"><span data-stu-id="7bf69-432">![Creating StoreIndexViewModel class](aspnet-mvc-4-fundamentals/_static/image20.png "Creating StoreIndexViewModel class")</span></span>

    <span data-ttu-id="7bf69-433">*StoreIndexViewModel 클래스 만들기*</span><span class="sxs-lookup"><span data-stu-id="7bf69-433">*Creating StoreIndexViewModel class*</span></span>

<a id="Ex5Task2"></a>

<a id="Task_2_-_Adding_Properties_to_the_ViewModel_class"></a>
#### <a name="task-2---adding-properties-to-the-viewmodel-class"></a><span data-ttu-id="7bf69-434">작업 2-ViewModel 클래스에 속성 추가</span><span class="sxs-lookup"><span data-stu-id="7bf69-434">Task 2 - Adding Properties to the ViewModel class</span></span>

<span data-ttu-id="7bf69-435">두 매개 변수는 StoreController에서 예상 되는 HTML 응답을 생성 하기 위해 템플릿 보기를 전달 하도록: 저장소 및 해당 장르 목록에는 장르의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-435">There are two parameters to be passed from the StoreController to the View template in order to generate the expected HTML response: the number of genres in the store and a list of those genres.</span></span>

<span data-ttu-id="7bf69-436">이 작업에서는 이러한 2 속성을 추가 합니다는 **StoreIndexViewModel** 클래스: **NumberOfGenres** (정수) 및 **장르** (문자열의 목록).</span><span class="sxs-lookup"><span data-stu-id="7bf69-436">In this task, you will add those 2 properties to the **StoreIndexViewModel** class: **NumberOfGenres** (an integer) and **Genres** (a list of strings).</span></span>

1. <span data-ttu-id="7bf69-437">추가 **NumberOfGenres** 및 **장르** 속성을는 **StoreIndexViewModel** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-437">Add **NumberOfGenres** and **Genres** properties to the **StoreIndexViewModel** class.</span></span> <span data-ttu-id="7bf69-438">이 위해 클래스 정의에 다음 두 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-438">To do this, add the following 2 lines to the class definition:</span></span>

    <span data-ttu-id="7bf69-439">(코드 조각- *ASP.NET MVC 4 기본-Ex5 StoreIndexViewModel 속성*)</span><span class="sxs-lookup"><span data-stu-id="7bf69-439">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreIndexViewModel properties*)</span></span>


~~~
[!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample11.cs)]

> [!NOTE]
> The **{ get; set; }** notation makes use of C#'s auto-implemented properties feature. It provides the benefits of a property without requiring us to declare a backing field.
~~~

<a id="Ex5Task3"></a>

<a id="Task_3_-_Updating_StoreController_to_use_the_StoreIndexViewModel"></a>
#### <a name="task-3---updating-storecontroller-to-use-the-storeindexviewmodel"></a><span data-ttu-id="7bf69-440">작업 3-업데이트 StoreController는 StoreIndexViewModel 사용 하려면</span><span class="sxs-lookup"><span data-stu-id="7bf69-440">Task 3 - Updating StoreController to use the StoreIndexViewModel</span></span>

<span data-ttu-id="7bf69-441">**StoreIndexViewModel** 클래스에서 전달 하는 데 필요한 정보를 캡슐화 **StoreController**의 **인덱스** 보기 템플릿에 대 한 응답을 생성 하기 위해 메서드 .</span><span class="sxs-lookup"><span data-stu-id="7bf69-441">The **StoreIndexViewModel** class encapsulates the information needed to pass from **StoreController**'s **Index** method to a View template in order to generate a response.</span></span>

<span data-ttu-id="7bf69-442">이 태스크에서는 업데이트 됩니다는 **StoreController** 사용 하는 **StoreIndexViewModel**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-442">In this task, you will update the **StoreController** to use the **StoreIndexViewModel**.</span></span>

1. <span data-ttu-id="7bf69-443">열기 **StoreController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-443">Open **StoreController** class.</span></span>

    <span data-ttu-id="7bf69-444">![StoreController 클래스를 열고](aspnet-mvc-4-fundamentals/_static/image21.png "여 StoreController 클래스")</span><span class="sxs-lookup"><span data-stu-id="7bf69-444">![Opening StoreController class](aspnet-mvc-4-fundamentals/_static/image21.png "Opening StoreController class")</span></span>

    <span data-ttu-id="7bf69-445">*Opening StoreController 클래스*</span><span class="sxs-lookup"><span data-stu-id="7bf69-445">*Opening StoreController class*</span></span>
2. <span data-ttu-id="7bf69-446">사용 하려면는 **StoreIndexViewModel** 에서 클래스는 **StoreController**, 맨 위에 있는 다음 네임 스페이스 추가 **StoreController** 코드:</span><span class="sxs-lookup"><span data-stu-id="7bf69-446">In order to use the **StoreIndexViewModel** class from the **StoreController**, add the following namespace at the top of the **StoreController** code:</span></span>

    <span data-ttu-id="7bf69-447">(코드 조각- *ASP.NET MVC 4 기본-Viewmodel를 사용 하 여 Ex5 StoreIndexViewModel*)</span><span class="sxs-lookup"><span data-stu-id="7bf69-447">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreIndexViewModel using ViewModels*)</span></span>


~~~
[!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample12.cs)]
~~~
3. <span data-ttu-id="7bf69-448">변경 된 **StoreController**의 **인덱스** 를 만들고 채우는 동작 메서드는 **StoreIndexViewModel** 개체를 보기 서식 파일에 전달 함께 HTML 응답을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-448">Change the **StoreController**'s **Index** action method so that it creates and populates a **StoreIndexViewModel** object and then passes it off to a View template to generate an HTML response with it.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7bf69-449">랩에서 &quot;ASP.NET MVC 모델 및 데이터 액세스&quot; 저장소 장르 목록을 데이터베이스에서 검색 하는 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-449">In Lab &quot;ASP.NET MVC Models and Data Access&quot; you will write code that retrieves the list of store genres from a database.</span></span> <span data-ttu-id="7bf69-450">다음 코드에서는 만듭니다는 **목록** 채울 더미 데이터가 장르는 **StoreIndexViewModel**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-450">In the following code, you will create a **List** of dummy data genres that will populate the **StoreIndexViewModel**.</span></span>
    > 
    > <span data-ttu-id="7bf69-451">만들고 설정 후는 **StoreIndexViewModel** 개체에 대 한 인수로 전달 됩니다는 **보기** 메서드.</span><span class="sxs-lookup"><span data-stu-id="7bf69-451">After creating and setting up the **StoreIndexViewModel** object, it will be passed as an argument to the **View** method.</span></span> <span data-ttu-id="7bf69-452">이 템플릿 보기를 함께 HTML 응답을 생성 하려면 해당 개체를 사용 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-452">This indicates that the View template will use that object to generate an HTML response with it.</span></span>
4. <span data-ttu-id="7bf69-453">대체는 **인덱스** 메서드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="7bf69-453">Replace the **Index** method with the following code:</span></span>

    <span data-ttu-id="7bf69-454">(코드 조각- *ASP.NET MVC 4 기본-Ex5 StoreController 인덱스 메서드*)</span><span class="sxs-lookup"><span data-stu-id="7bf69-454">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreController Index method*)</span></span>


~~~
[!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample13.cs)]

> [!NOTE]
> If you're unfamiliar with C#, you may assume that using **var** means that the **viewModel** variable is late-bound. That's not correct - the C# compiler is using type-inference based on what you assign to the variable to determine that **viewModel** is of type **StoreIndexViewModel**. Also, by compiling the local **viewModel** variable as a **StoreIndexViewModel** type you get compile-time checking and Visual Studio code-editor support.
~~~

<a id="Ex5Task4"></a>

<a id="Task_4_-_Creating_a_View_Template_that_Uses_StoreIndexViewModel"></a>
#### <a name="task-4---creating-a-view-template-that-uses-storeindexviewmodel"></a><span data-ttu-id="7bf69-455">작업 4-StoreIndexViewModel를 사용 하는 보기 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="7bf69-455">Task 4 - Creating a View Template that Uses StoreIndexViewModel</span></span>

<span data-ttu-id="7bf69-456">이 작업에서는 장르의 목록을 표시 하려면 컨트롤러에서 전달 되는 StoreIndexViewModel 개체에서 사용할 보기 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-456">In this task, you will create a View template that will use a StoreIndexViewModel object passed from the Controller to display a list of genres.</span></span>

1. <span data-ttu-id="7bf69-457">새 보기 서식 파일을 만들기 전에 프로젝트를 제작 해 보겠습니다 있도록는 **보기 대화 상자 추가** 에 대해 알고는 **StoreIndexViewModel** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-457">Before creating the new View template, let's build the project so that the **Add View Dialog** knows about the **StoreIndexViewModel** class.</span></span> <span data-ttu-id="7bf69-458">선택 하 여 프로젝트를 빌드합니다는 **빌드** 메뉴 항목 차례로 **빌드 MvcMusicStore**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-458">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="7bf69-459">![프로젝트를 빌드하면](aspnet-mvc-4-fundamentals/_static/image22.png "프로젝트 빌드")</span><span class="sxs-lookup"><span data-stu-id="7bf69-459">![Building the project](aspnet-mvc-4-fundamentals/_static/image22.png "Building the project")</span></span>

    <span data-ttu-id="7bf69-460">*프로젝트 빌드*</span><span class="sxs-lookup"><span data-stu-id="7bf69-460">*Building the project*</span></span>
2. <span data-ttu-id="7bf69-461">새 보기 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-461">Create a new View template.</span></span> <span data-ttu-id="7bf69-462">이렇게 하려면 마우스 오른쪽 단추로 클릭는 **인덱스** 메서드와 선택 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-462">To do that, right-click inside the **Index** method and select **Add View**.</span></span>

    <span data-ttu-id="7bf69-463">![뷰 추가](aspnet-mvc-4-fundamentals/_static/image23.png "뷰 추가")</span><span class="sxs-lookup"><span data-stu-id="7bf69-463">![Adding a View](aspnet-mvc-4-fundamentals/_static/image23.png "Adding a View")</span></span>

    <span data-ttu-id="7bf69-464">*보기 추가*</span><span class="sxs-lookup"><span data-stu-id="7bf69-464">*Adding a View*</span></span>
3. <span data-ttu-id="7bf69-465">때문에 **보기 대화 상자 추가** 에서 호출 되었습니다는 **StoreController**, 템플릿 보기에 기본적으로 추가 되는 **\Views\Store\Index.cshtml** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-465">Because the **Add View Dialog** was invoked from the **StoreController**, it will add the View template by default in a **\Views\Store\Index.cshtml** file.</span></span> <span data-ttu-id="7bf69-466">확인은 **보기를 만들 강력한-입력 한-** 확인란을 선택한 후 **StoreIndexViewModel** 으로 **모델 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-466">Check the **Create a strongly-typed-view** checkbox and then select **StoreIndexViewModel** as the **Model class**.</span></span> <span data-ttu-id="7bf69-467">또한 선택한 뷰 엔진을 반드시 **Razor**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-467">Also, make sure that the View engine selected is **Razor**.</span></span> <span data-ttu-id="7bf69-468">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-468">Click **Add**.</span></span>

    <span data-ttu-id="7bf69-469">![뷰 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image24.png "뷰 추가 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="7bf69-469">![Add View Dialog](aspnet-mvc-4-fundamentals/_static/image24.png "Add View Dialog")</span></span>

    <span data-ttu-id="7bf69-470">*뷰 추가 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="7bf69-470">*Add View Dialog*</span></span>

    <span data-ttu-id="7bf69-471">**\Views\Store\Index.cshtml** 보기 템플릿 파일을 만들고 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-471">The **\Views\Store\Index.cshtml** View template file is created and opened.</span></span> <span data-ttu-id="7bf69-472">에 제공 된 정보에 따라는 **뷰 추가** 대화 상자는 마지막 단계 템플릿을 증명 보기에에서는 **StoreIndexViewModel** HTML 응답을 생성 하는 데 데이터로 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="7bf69-472">Based on the information provided to the **Add View** dialog in the last step, the View template will expect a **StoreIndexViewModel** instance as the data to use to generate an HTML response.</span></span> <span data-ttu-id="7bf69-473">서식 파일의 상속 함을 알 수는 `ViewPage<musicstore.viewmodels.storeindexviewmodel>` C#입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-473">You will notice that the template inherits a `ViewPage<musicstore.viewmodels.storeindexviewmodel>` in C#.</span></span>

<a id="Ex5Task5"></a>

<a id="Task_5_-_Updating_the_View_Template"></a>
#### <a name="task-5---updating-the-view-template"></a><span data-ttu-id="7bf69-474">작업 5-보기 템플릿 업데이트</span><span class="sxs-lookup"><span data-stu-id="7bf69-474">Task 5 - Updating the View Template</span></span>

<span data-ttu-id="7bf69-475">이 태스크에서는 장르 및 페이지 내에서 이름을의 수를 검색 하려면 마지막 작업에서 만든 보기 서식 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-475">In this task, you will update the View template created in the last task to retrieve the number of genres and their names within the page.</span></span>

> [!NOTE]
> <span data-ttu-id="7bf69-476">@ 구문을 사용 합니다 (이 라 불리 &quot;코드 너&quot;) 보기 템플릿 내에서 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-476">You will use @ syntax (often referred to as &quot;code nuggets&quot;) to execute code within the View template.</span></span>


1. <span data-ttu-id="7bf69-477">에 **Index.cshtml** 파일 내에서 **저장소** 폴더를 해당 코드를 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-477">In the **Index.cshtml** file, within the **Store** folder, replace its code with the following:</span></span>


~~~
[!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample14.cshtml)]

> [!NOTE]
> As soon as you finish typing the period after the word **Model**, Visual Studio's Intellisense will show a list of possible properties and methods to choose from.
> 
> ![](aspnet-mvc-4-fundamentals/_static/image25.png)
> 
> *Getting Model properties and methods with Visual Studio's IntelliSense*
> 
> The **Model** property references the **StoreIndexViewModel** object that the Controller passed to the View template. This means that you can access all of the data passed from the Controller to the View template via the **Model** property, and format it into an appropriate HTML response within the View template.
> 
> You can just select the **NumberOfGenres** property from the Intellisense list rather than typing it in and then it will auto-complete it by pressing the **tab key**.
~~~
2. <span data-ttu-id="7bf69-478">장르 목록에 대해 루프 **StoreIndexViewModel** HTML 만들고 **&lt;ul&gt;** 사용 하 여 나열는 **foreach** 루프 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-478">Loop over the genre list in **StoreIndexViewModel** and create an HTML **&lt;ul&gt;** list using a **foreach** loop.</span></span>
   <span data-ttu-id="7bf69-479">(C#)</span><span class="sxs-lookup"><span data-stu-id="7bf69-479">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample15.cshtml)]
3. <span data-ttu-id="7bf69-480">키를 눌러 **F5** 하는 응용 프로그램을 실행 하 고 찾아볼 **/저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-480">Press **F5** to run the Application and browse **/Store**.</span></span> <span data-ttu-id="7bf69-481">전달 된 장르 목록이 표시 됩니다는 **StoreIndexViewModel** 에서 개체는 **StoreController** 템플릿 보기에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-481">You will see the list of genres passed in the **StoreIndexViewModel** object from the **StoreController** to the View template.</span></span>

    <span data-ttu-id="7bf69-482">![장르의 목록을 표시 하는 보기](aspnet-mvc-4-fundamentals/_static/image26.png "보기 장르 목록 표시")</span><span class="sxs-lookup"><span data-stu-id="7bf69-482">![View displaying a list of genres](aspnet-mvc-4-fundamentals/_static/image26.png "View displaying a list of genres")</span></span>

    <span data-ttu-id="7bf69-483">*보기 장르 목록 표시*</span><span class="sxs-lookup"><span data-stu-id="7bf69-483">*View displaying a list of genres*</span></span>
4. <span data-ttu-id="7bf69-484">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-484">Close the browser.</span></span>

<a id="Exercise6"></a>

<a id="Exercise_6_Using_Parameters_in_View"></a>
### <a name="exercise-6-using-parameters-in-view"></a><span data-ttu-id="7bf69-485">실습 6: 매개 변수를 보기에 사용</span><span class="sxs-lookup"><span data-stu-id="7bf69-485">Exercise 6: Using Parameters in View</span></span>

<span data-ttu-id="7bf69-486">연습 3에서 컨트롤러에 매개 변수를 전달 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-486">In Exercise 3 you learned how to pass parameters to the Controller.</span></span> <span data-ttu-id="7bf69-487">이 연습에서는 뷰 템플릿에 이러한 매개 변수를 사용 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-487">In this exercise, you will learn how to use those parameters in the View template.</span></span> <span data-ttu-id="7bf69-488">이 위해 있습니다 도입 될 것 먼저를 사용자 데이터 및 도메인 논리를 관리 하는 데 도움이 되는 모델 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-488">For that purpose, you will be introduced first to Model classes that will help you to manage your data and domain logic.</span></span> <span data-ttu-id="7bf69-489">또한 인코딩 URL 경로 등의 걱정 하지 않고 ASP.NET MVC 응용 프로그램 내 페이지 링크를 만드는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-489">Additionally, you will learn how to create links to pages inside the ASP.NET MVC application without worrying of things like URL paths encoding.</span></span>

<a id="Ex6Task1"></a>

<a id="Task_1_-_Adding_Model_Classes"></a>
#### <a name="task-1---adding-model-classes"></a><span data-ttu-id="7bf69-490">작업 1-모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="7bf69-490">Task 1 - Adding Model Classes</span></span>

<span data-ttu-id="7bf69-491">보기에는 컨트롤러에서 정보를 전달 하기 위한 것 만들어진 Viewmodel 달리 모델 클래스를 포함 하 고 데이터 및 도메인 논리를 관리할 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-491">Unlike ViewModels, which are created just to pass information from the Controller to the View, Model classes are built to contain and manage data and domain logic.</span></span> <span data-ttu-id="7bf69-492">이 작업에서는 이러한 개념을 표현 하는 두 개의 모델 클래스를 추가 합니다: **장르** 및 **앨범**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-492">In this task you will add two model classes to represent these concepts: **Genre** and **Album**.</span></span>

1. <span data-ttu-id="7bf69-493">아직 열지 않은 경우 시작 **VS Express for Web**</span><span class="sxs-lookup"><span data-stu-id="7bf69-493">If not already open, start **VS Express for Web**</span></span>
2. <span data-ttu-id="7bf69-494">에 **파일** 메뉴 선택 **프로젝트 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-494">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="7bf69-495">프로젝트 열기 대화 상자에서 찾은 **Source\Ex06 UsingParametersInView\Begin**선택, **Begin.sln** 클릭 **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-495">In the Open Project dialog, browse to **Source\Ex06-UsingParametersInView\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="7bf69-496">또는 계속 진행할 솔루션, 이전 연습을 완료 한 후 가져올 있음을 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-496">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="7bf69-497">제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면.</span><span class="sxs-lookup"><span data-stu-id="7bf69-497">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="7bf69-498">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-498">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="7bf69-499">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="7bf69-499">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="7bf69-500">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-500">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="7bf69-501">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-501">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="7bf69-502">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-502">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="7bf69-503">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-503">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="7bf69-504">추가 **장르** 모델 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-504">Add a **Genre** Model class.</span></span> <span data-ttu-id="7bf69-505">이렇게 하려면 마우스 오른쪽 단추로 클릭는 **모델** 폴더에는 **솔루션 탐색기**선택, **추가** 차례로 **새 항목** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-505">To do this, right-click the **Models** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="7bf69-506">아래 **코드**, 선택는 **클래스** 항목 및 파일 이름을 *Genre.cs*, 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-506">Under **Code**, choose the **Class** item and name the file *Genre.cs*, then click **Add**.</span></span>

    <span data-ttu-id="7bf69-507">![클래스 추가](aspnet-mvc-4-fundamentals/_static/image27.png "클래스 추가")</span><span class="sxs-lookup"><span data-stu-id="7bf69-507">![Adding a class](aspnet-mvc-4-fundamentals/_static/image27.png "Adding a class")</span></span>

    <span data-ttu-id="7bf69-508">*새 항목 추가*</span><span class="sxs-lookup"><span data-stu-id="7bf69-508">*Adding a new item*</span></span>

    <span data-ttu-id="7bf69-509">![Genre 모델 클래스를 추가](aspnet-mvc-4-fundamentals/_static/image28.png "장르 모델 클래스를 추가 합니다.")</span><span class="sxs-lookup"><span data-stu-id="7bf69-509">![Add Genre Model Class](aspnet-mvc-4-fundamentals/_static/image28.png "Add Genre Model Class")</span></span>

    <span data-ttu-id="7bf69-510">*Genre 모델 클래스를 추가 합니다.*</span><span class="sxs-lookup"><span data-stu-id="7bf69-510">*Add Genre Model Class*</span></span>
4. <span data-ttu-id="7bf69-511">추가 **이름** 장르 클래스에 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-511">Add a **Name** property to the Genre class.</span></span> <span data-ttu-id="7bf69-512">이렇게 하려면 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-512">To do this, add the following code:</span></span>

    <span data-ttu-id="7bf69-513">(코드 조각- *기본 ASP.NET MVC 4-Ex6 장르*)</span><span class="sxs-lookup"><span data-stu-id="7bf69-513">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 Genre*)</span></span>


~~~
[!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample16.cs)]
~~~
5. <span data-ttu-id="7bf69-514">추가 적으로 동일한 절차는 **앨범** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-514">Following the same procedure as before, add an **Album** class.</span></span> <span data-ttu-id="7bf69-515">이렇게 하려면 마우스 오른쪽 단추로 클릭는 **모델** 폴더에는 **솔루션 탐색기**선택, **추가** 차례로 **새 항목** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-515">To do this, right-click the **Models** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="7bf69-516">아래 **코드**, 선택는 **클래스** 항목 및 파일 이름을 *Album.cs*, 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-516">Under **Code**, choose the **Class** item and name the file *Album.cs*, then click **Add**.</span></span>
6. <span data-ttu-id="7bf69-517">앨범 클래스에 두 개의 속성 추가: **장르** 및 **제목**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-517">Add two properties to the Album class: **Genre** and **Title**.</span></span> <span data-ttu-id="7bf69-518">이렇게 하려면 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-518">To do this, add the following code:</span></span>

    <span data-ttu-id="7bf69-519">(코드 조각- *기본 ASP.NET MVC 4-Ex6 앨범*)</span><span class="sxs-lookup"><span data-stu-id="7bf69-519">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 Album*)</span></span>


~~~
[!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample17.cs)]
~~~

<a id="Ex6Task2"></a>

<a id="Task_2_-_Adding_a_StoreBrowseViewModel"></a>
#### <a name="task-2---adding-a-storebrowseviewmodel"></a><span data-ttu-id="7bf69-520">작업 2-는 StoreBrowseViewModel 추가</span><span class="sxs-lookup"><span data-stu-id="7bf69-520">Task 2 - Adding a StoreBrowseViewModel</span></span>

<span data-ttu-id="7bf69-521">A **StoreBrowseViewModel** 선택한 장르와 일치 하는 앨범 표시 하려면이 작업에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-521">A **StoreBrowseViewModel** will be used in this task to show the Albums that match a selected Genre.</span></span> <span data-ttu-id="7bf69-522">이 작업에서는이 클래스 만들고 처리 하는 두 개의 속성을 추가 합니다는 **장르** 및 해당 **앨범**의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-522">In this task, you will create this class and then add two properties to handle the **Genre** and its **Album**'s List.</span></span>

1. <span data-ttu-id="7bf69-523">추가 **StoreBrowseViewModel** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-523">Add a **StoreBrowseViewModel** class.</span></span> <span data-ttu-id="7bf69-524">이렇게 하려면 마우스 오른쪽 단추로 클릭는 **Viewmodel** 폴더에는 **솔루션 탐색기**선택, **추가** 차례로 **새 항목** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-524">To do this, right-click the **ViewModels** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="7bf69-525">아래 **코드**, 선택는 **클래스** 항목 및 파일 이름을 *StoreBrowseViewModel.cs*, 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-525">Under **Code**, choose the **Class** item and name the file *StoreBrowseViewModel.cs*, then click **Add**.</span></span>
2. <span data-ttu-id="7bf69-526">모델에 대 한 참조를 추가 **StoreBrowseViewModel** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-526">Add a reference to the Models in **StoreBrowseViewModel** class.</span></span> <span data-ttu-id="7bf69-527">이 작업을 수행 하려면 다음 추가 네임 스페이스를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="7bf69-527">To do this, add the following using namespace:</span></span>

    <span data-ttu-id="7bf69-528">(코드 조각- *기본 ASP.NET MVC 4-Ex6 UsingModel*)</span><span class="sxs-lookup"><span data-stu-id="7bf69-528">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 UsingModel*)</span></span>


~~~
[!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample18.cs)]
~~~
3. <span data-ttu-id="7bf69-529">두 속성을 추가 **StoreBrowseViewModel** 클래스: **장르** 및 **앨범**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-529">Add two properties to **StoreBrowseViewModel** class: **Genre** and **Albums**.</span></span> <span data-ttu-id="7bf69-530">이렇게 하려면 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-530">To do this, add the following code:</span></span>

    <span data-ttu-id="7bf69-531">(코드 조각- *기본 ASP.NET MVC 4-Ex6 ModelProperties*)</span><span class="sxs-lookup"><span data-stu-id="7bf69-531">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 ModelProperties*)</span></span>


~~~
[!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample19.cs)]

> [!NOTE]
> What is **List&lt;Album&gt;** ?: This definition is using the **List&lt;T&gt;** type, where **T** constrains the type to which elements of this **List** belong to, in this case **Album** (or any of its descendants).
> 
> This ability to design classes and methods that defer the specification of one or more types until the class or method is declared and instantiated by client code is a feature of the C# language called **Generics**.
> 
> **List&lt;T&gt;** is the generic equivalent of the **ArrayList** type and is available in the **System.Collections.Generic** namespace. One of the benefits of using **generics** is that since the type is specified, you do not need to take care of type checking operations such as casting the elements into **Album** as you would do with an **ArrayList**.
~~~

<a id="Ex6Task3"></a>

<a id="Task_3_-_Using_the_New_ViewModel_in_the_StoreController"></a>
#### <a name="task-3---using-the-new-viewmodel-in-the-storecontroller"></a><span data-ttu-id="7bf69-532">작업 3-새 ViewModel는 StoreController에서 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="7bf69-532">Task 3 - Using the New ViewModel in the StoreController</span></span>

<span data-ttu-id="7bf69-533">이 작업에서 수정 됩니다는 **StoreController**의 **찾아보기** 및 **세부 정보** 작업 메서드를 사용 하 여 새 **StoreBrowseViewModel** .</span><span class="sxs-lookup"><span data-stu-id="7bf69-533">In this task, you will modify the **StoreController**'s **Browse** and **Details** action methods to use the new **StoreBrowseViewModel**.</span></span>

1. <span data-ttu-id="7bf69-534">모델 폴더에 대 한 참조를 추가 **StoreController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-534">Add a reference to the Models folder in **StoreController** class.</span></span> <span data-ttu-id="7bf69-535">이 작업을 수행 하려면 확장 된 **컨트롤러** 폴더에는 **솔루션 탐색기** 엽니다는 **StoreController** 클래스.</span><span class="sxs-lookup"><span data-stu-id="7bf69-535">To do this, expand the **Controllers** folder in the **Solution Explorer** and open the **StoreController** class.</span></span> <span data-ttu-id="7bf69-536">다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-536">Then add the following code:</span></span>

    <span data-ttu-id="7bf69-537">(코드 조각- *기본 ASP.NET MVC 4-Ex6 UsingModelInController*)</span><span class="sxs-lookup"><span data-stu-id="7bf69-537">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 UsingModelInController*)</span></span>


~~~
[!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample20.cs)]
~~~
2. <span data-ttu-id="7bf69-538">대체는 **찾아보기** 사용 하도록 동작 메서드는 **StoreViewBrowseController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-538">Replace the **Browse** action method to use the **StoreViewBrowseController** class.</span></span> <span data-ttu-id="7bf69-539">더미 데이터로 장르와 두 개의 새로운 앨범 개체 만듭니다 (다음 실습 랩에는 사용 데이터베이스의 실제 데이터).</span><span class="sxs-lookup"><span data-stu-id="7bf69-539">You will create a Genre and two new Albums objects with dummy data (in the next Hands-on Lab you will consume real data from a database).</span></span> <span data-ttu-id="7bf69-540">이 작업을 수행 하려면 대체는 **찾아보기** 메서드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="7bf69-540">To do this, replace the **Browse** method with the following code:</span></span>

    <span data-ttu-id="7bf69-541">(코드 조각- *기본 ASP.NET MVC 4-Ex6 BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="7bf69-541">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 BrowseMethod*)</span></span>


~~~
[!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample21.cs)]
~~~
3. <span data-ttu-id="7bf69-542">대체는 **세부 정보** 사용 하도록 동작 메서드는 **StoreViewBrowseController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-542">Replace the **Details** action method to use the **StoreViewBrowseController** class.</span></span> <span data-ttu-id="7bf69-543">새 만들려는 **앨범** 에 반환 되는 개체는 **보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-543">You will create a new **Album** object to be returned to the **View**.</span></span> <span data-ttu-id="7bf69-544">이 작업을 수행 하려면 대체는 **세부 정보** 메서드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="7bf69-544">To do this, replace the **Details** method with the following code:</span></span>

    <span data-ttu-id="7bf69-545">(코드 조각- *기본 ASP.NET MVC 4-Ex6 DetailsMethod*)</span><span class="sxs-lookup"><span data-stu-id="7bf69-545">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 DetailsMethod*)</span></span>


~~~
[!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample22.cs)]
~~~

<a id="Ex6Task4"></a>

<a id="Task_4_-_Adding_a_Browse_View_Template"></a>
#### <a name="task-4---adding-a-browse-view-template"></a><span data-ttu-id="7bf69-546">작업 4-찾아보기 보기 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="7bf69-546">Task 4 - Adding a Browse View Template</span></span>

<span data-ttu-id="7bf69-547">이 태스크에서는 추가한는 **찾아보기** 특정 장르에 대 한 앨범 표시 하도록 보기.</span><span class="sxs-lookup"><span data-stu-id="7bf69-547">In this task, you will add a **Browse** View to show the Albums found for a specific Genre.</span></span>

1. <span data-ttu-id="7bf69-548">새 보기 서식 파일을 만들기 전에 프로젝트를 작성 해야 하는 **뷰 추가** 대화에 대해 알고는 **ViewModel** 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-548">Before creating the new View template, you should build the project so that the **Add View** Dialog knows about the **ViewModel** class to use.</span></span> <span data-ttu-id="7bf69-549">선택 하 여 프로젝트를 빌드합니다는 **빌드** 메뉴 항목 차례로 **빌드 MvcMusicStore**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-549">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>
2. <span data-ttu-id="7bf69-550">추가 **찾아보기** 보기.</span><span class="sxs-lookup"><span data-stu-id="7bf69-550">Add a **Browse** View.</span></span> <span data-ttu-id="7bf69-551">이렇게 하려면 마우스 오른쪽 단추로 클릭는 **찾아보기** 의 동작 메서드는 **StoreController** 클릭 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-551">To do this, right-click in the **Browse** action method of the **StoreController** and click **Add View**.</span></span>
3. <span data-ttu-id="7bf69-552">에 **뷰 추가** 대화 상자, 뷰 이름 인지 확인 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-552">In the **Add View** dialog box, verify that the View Name is **Browse**.</span></span> <span data-ttu-id="7bf69-553">확인의 **강력한 형식의 뷰 만들기** 확인란을 선택 하 고 **StoreBrowseViewModel** 에서 **모델 클래스** 드롭다운입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-553">Check the **Create a strongly-typed view** checkbox and select **StoreBrowseViewModel** from the **Model class** dropdown.</span></span> <span data-ttu-id="7bf69-554">다른 필드를 기본값으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-554">Leave the other fields with their default value.</span></span> <span data-ttu-id="7bf69-555">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-555">Then click **Add**.</span></span>

    <span data-ttu-id="7bf69-556">![브라우저 보기 추가](aspnet-mvc-4-fundamentals/_static/image29.png "찾아보기 뷰 추가")</span><span class="sxs-lookup"><span data-stu-id="7bf69-556">![Adding a Browse View](aspnet-mvc-4-fundamentals/_static/image29.png "Adding a Browse View")</span></span>

    <span data-ttu-id="7bf69-557">*브라우저 보기를 추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="7bf69-557">*Adding a Browse View*</span></span>
4. <span data-ttu-id="7bf69-558">수정 된 **Browse.cshtml** Genre의 정보를 표시 하에 액세스 하는 **StoreBrowseViewModel** 템플릿 보기에 전달 되는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-558">Modify the **Browse.cshtml** to display the Genre's information, accessing the **StoreBrowseViewModel** object that is passed to the view template.</span></span> <span data-ttu-id="7bf69-559">이 위해 콘텐츠를 다음과 같이 바꿉니다: (C#)</span><span class="sxs-lookup"><span data-stu-id="7bf69-559">To do this, replace the content with the following: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample23.cshtml)]

<a id="Ex6Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="7bf69-560">5-응용 프로그램 실행 작업</span><span class="sxs-lookup"><span data-stu-id="7bf69-560">Task 5 - Running the Application</span></span>

<span data-ttu-id="7bf69-561">에서는이 작업을 테스트 하는 **찾아보기** 메서드 앨범에서 검색 된 **찾아보기** 메서드 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-561">In this task, you will test that the **Browse** method retrieves Albums from the **Browse** method action.</span></span>

1. <span data-ttu-id="7bf69-562">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-562">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="7bf69-563">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-563">The project starts in the Home page.</span></span> <span data-ttu-id="7bf69-564">URL을 변경 **찾아보기/저장 /? Genre Disco =** 동작 두 앨범을 반환 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-564">Change the URL to **/Store/Browse?Genre=Disco** to verify that the action returns two Albums.</span></span>

    <span data-ttu-id="7bf69-565">![저장소 디스코 앨범 검색](aspnet-mvc-4-fundamentals/_static/image30.png "디스코 앨범 저장소를 검색 합니다.")</span><span class="sxs-lookup"><span data-stu-id="7bf69-565">![Browsing Store Disco Albums](aspnet-mvc-4-fundamentals/_static/image30.png "Browsing Store Disco Albums")</span></span>

    <span data-ttu-id="7bf69-566">*저장소 디스코 앨범 찾아보기*</span><span class="sxs-lookup"><span data-stu-id="7bf69-566">*Browsing Store Disco Albums*</span></span>

<a id="Ex6Task6"></a>

<a id="Task_6_-_Displaying_information_About_a_Specific_Album"></a>
#### <a name="task-6---displaying-information-about-a-specific-album"></a><span data-ttu-id="7bf69-567">태스크 6-정보는 특정 앨범 표시</span><span class="sxs-lookup"><span data-stu-id="7bf69-567">Task 6 - Displaying information About a Specific Album</span></span>

<span data-ttu-id="7bf69-568">이 작업을 구현 합니다는 **저장소/세부 정보** 특정 앨범에 대 한 정보를 표시 하는 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-568">In this task, you will implement the **Store/Details** view to display information about a specific album.</span></span> <span data-ttu-id="7bf69-569">이 실습 랩에서 앨범에 대 한 표시는 모든 항목에 이미 포함 되어는 **보기** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="7bf69-569">In this Hands-on Lab, everything you will display about the album is already contained in the **View** template.</span></span> <span data-ttu-id="7bf69-570">따라서 만드는 대신 한 **StoreDetailsViewModel** 클래스 현재 사용 하 여 **StoreBrowseViewModel** 앨범을 전달 하는 서식 파일.</span><span class="sxs-lookup"><span data-stu-id="7bf69-570">So, instead of creating a **StoreDetailsViewModel** class, you will use the current **StoreBrowseViewModel** template passing the Album to it.</span></span>

1. <span data-ttu-id="7bf69-571">Visual Studio 창에 반환 하는 데 필요한 경우 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-571">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="7bf69-572">새로 추가 **세부 정보** 에 대 한 보기 된 **StoreController**의 **세부 정보** 동작 메서드.</span><span class="sxs-lookup"><span data-stu-id="7bf69-572">Add a new **Details** view for the **StoreController**'s **Details** action method.</span></span> <span data-ttu-id="7bf69-573">이렇게 하려면 마우스 오른쪽 단추로 클릭는 **세부 정보** 에서 메서드는 **StoreController** 클래스 및 클릭 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-573">To do this, right-click the **Details** method in the **StoreController** class and click **Add View**.</span></span>
2. <span data-ttu-id="7bf69-574">에 **뷰 추가** 대화 상자에서 되어 있는지 확인은 **뷰 이름** 은 **세부 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-574">In the **Add View** dialog, verify that the **View Name** is **Details**.</span></span> <span data-ttu-id="7bf69-575">확인의 **강력한 형식의 뷰 만들기** 확인란을 선택 하 고 **앨범** 에서 **모델 클래스** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-575">Check the **Create a strongly-typed view** checkbox and select **Album** from the **Model class** drop-down.</span></span> <span data-ttu-id="7bf69-576">다른 필드를 기본값으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-576">Leave the other fields with their default value.</span></span> <span data-ttu-id="7bf69-577">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-577">Then click **Add**.</span></span> <span data-ttu-id="7bf69-578">만들고 열려면는 **\Views\Store\Details.cshtml** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-578">This will create and open a **\Views\Store\Details.cshtml** file.</span></span>

    <span data-ttu-id="7bf69-579">![세부 정보 뷰 추가](aspnet-mvc-4-fundamentals/_static/image31.png "추가 세부 정보 보기")</span><span class="sxs-lookup"><span data-stu-id="7bf69-579">![Adding a Details View](aspnet-mvc-4-fundamentals/_static/image31.png "Adding a Details View")</span></span>

    <span data-ttu-id="7bf69-580">*추가 세부 정보 보기*</span><span class="sxs-lookup"><span data-stu-id="7bf69-580">*Adding a Details View*</span></span>
3. <span data-ttu-id="7bf69-581">수정 된 **Details.cshtml** 앨범의 정보를 표시 하는 파일에 액세스 하는 **앨범** 템플릿 보기에 전달 되는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-581">Modify the **Details.cshtml** file to display the Album's information, accessing the **Album** object that is passed to the view template.</span></span> <span data-ttu-id="7bf69-582">이 위해 콘텐츠를 다음과 같이 바꿉니다: (C#)</span><span class="sxs-lookup"><span data-stu-id="7bf69-582">To do this, replace the content with the following: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample24.cshtml)]

<a id="Ex6Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a><span data-ttu-id="7bf69-583">7-응용 프로그램 실행 작업</span><span class="sxs-lookup"><span data-stu-id="7bf69-583">Task 7 - Running the Application</span></span>

<span data-ttu-id="7bf69-584">에서는이 작업을 테스트 하는 **세부 정보** 에서 앨범의 정보를 검색 하는 보기는 **동작에 자세히 설명** 메서드.</span><span class="sxs-lookup"><span data-stu-id="7bf69-584">In this task, you will test that the **Details** View retrieves Album's information from the **Details action** method.</span></span>

1. <span data-ttu-id="7bf69-585">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-585">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="7bf69-586">프로젝트 시작 날짜는 **홈** 페이지.</span><span class="sxs-lookup"><span data-stu-id="7bf69-586">The project starts in the **Home** page.</span></span> <span data-ttu-id="7bf69-587">URL을 변경 **/Store/Details/5** 앨범의 정보를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-587">Change the URL to **/Store/Details/5** to verify the album's information.</span></span>

    <span data-ttu-id="7bf69-588">![앨범 세부 정보를 검색](aspnet-mvc-4-fundamentals/_static/image32.png "앨범 세부 정보를 검색 합니다.")</span><span class="sxs-lookup"><span data-stu-id="7bf69-588">![Browsing Albums Detail](aspnet-mvc-4-fundamentals/_static/image32.png "Browsing Albums Detail")</span></span>

    <span data-ttu-id="7bf69-589">*앨범 세부 정보를 검색합니다.*</span><span class="sxs-lookup"><span data-stu-id="7bf69-589">*Browsing Album's Detail*</span></span>

<a id="Ex6Task8"></a>

<a id="Task_8_-_Adding_Links_Between_Pages"></a>
#### <a name="task-8---adding-links-between-pages"></a><span data-ttu-id="7bf69-590">태스크 8-페이지 간 링크 추가</span><span class="sxs-lookup"><span data-stu-id="7bf69-590">Task 8 - Adding Links Between Pages</span></span>

<span data-ttu-id="7bf69-591">이 작업을 적절 한 모든 장르 이름에 링크가 있으며이를 저장소 보기의 링크를 추가 합니다 **/저장소/찾아보기** URL입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-591">In this task, you will add a link in the Store View to have a link in every Genre name to the appropriate **/Store/Browse** URL.</span></span> <span data-ttu-id="7bf69-592">이런 방식이으로, 예를 들어는 장르에서 클릭 **Disco**, 검색을 시작 합니다 **/저장소/찾아보기? 장르 Disco =** URL입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-592">This way, when you click on a Genre, for instance **Disco**, it will navigate to **/Store/Browse?genre=Disco** URL.</span></span>

1. <span data-ttu-id="7bf69-593">Visual Studio 창에 반환 하는 데 필요한 경우 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-593">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="7bf69-594">업데이트는 **인덱스** 페이지에 대 한 링크를 추가 하는 **찾아보기** 페이지.</span><span class="sxs-lookup"><span data-stu-id="7bf69-594">Update the **Index** page to add a link to the **Browse** page.</span></span> <span data-ttu-id="7bf69-595">이 수행 하는 **솔루션 탐색기** 확장는 **뷰** 폴더를 하면 **저장소** 폴더를 두 번 클릭은 **Index.cshtml** 페이지.</span><span class="sxs-lookup"><span data-stu-id="7bf69-595">To do this, in the **Solution Explorer** expand the **Views** folder, then the **Store** folder and double-click the **Index.cshtml** page.</span></span>
2. <span data-ttu-id="7bf69-596">선택한 장르를 나타내는 찾아보기 보기에 대 한 링크를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-596">Add a link to the Browse view indicating the genre selected.</span></span> <span data-ttu-id="7bf69-597">이 작업을 수행 하려면 내에서 강조 표시 된 다음 코드를 대체는 **&lt;li&gt;** 태그: (C#)</span><span class="sxs-lookup"><span data-stu-id="7bf69-597">To do this, replace the following highlighted code within the **&lt;li&gt;** tags: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample25.cshtml)]

   > [!NOTE]
   > <span data-ttu-id="7bf69-598">또 다른 방법은 다음과 같은 코드 페이지에 직접 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-598">another approach would be linking directly to the page, with a code like the following:</span></span>
   > 
   > <span data-ttu-id="7bf69-599">&lt;a href=&quot;/Store/Browse?genre=@genreName&quot;&gt;@genreName&lt;/a&gt;</span><span class="sxs-lookup"><span data-stu-id="7bf69-599">&lt;a href=&quot;/Store/Browse?genre=@genreName&quot;&gt;@genreName&lt;/a&gt;</span></span>
   > 
   > <span data-ttu-id="7bf69-600">이 방법은 작동 하지만 하드 코드 된 문자열에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-600">Although this approach works, it depends on a hardcoded string.</span></span> <span data-ttu-id="7bf69-601">나중에 컨트롤러를 바꾸면이 명령을 수동으로 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-601">If you later rename the Controller, you will have to change this instruction manually.</span></span> <span data-ttu-id="7bf69-602">사용 하는 것이 더 좋은 것는 **HTML 도우미** 메서드.</span><span class="sxs-lookup"><span data-stu-id="7bf69-602">A better alternative is to use an **HTML Helper** method.</span></span> <span data-ttu-id="7bf69-603">ASP.NET MVC 등의 작업에 사용할 수 있는 HTML 도우미 메서드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-603">ASP.NET MVC includes an HTML Helper method which is available for such tasks.</span></span> <span data-ttu-id="7bf69-604">**Html.ActionLink()** 도우미 메서드를 사용 하면 HTML 만들려는 쉽게 **&lt;는&gt;** 링크, URL 경로 URL로 인코딩된 제대로 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-604">The **Html.ActionLink()** helper method makes it easy to build HTML **&lt;a&gt;** links, making sure URL paths are properly URL encoded.</span></span>
   > 
   > <span data-ttu-id="7bf69-605">Htlm.ActionLink 여러 오버 로드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-605">Htlm.ActionLink has several overloads.</span></span> <span data-ttu-id="7bf69-606">이 연습에서는 세 개의 매개 변수 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-606">In this exercise you will use one that takes three parameters:</span></span>
   > 
   > 1. <span data-ttu-id="7bf69-607">링크 텍스트는 장르 이름이 표시 됩니다</span><span class="sxs-lookup"><span data-stu-id="7bf69-607">Link text, which will display the Genre name</span></span>
   > 2. <span data-ttu-id="7bf69-608">컨트롤러 동작 이름 (**찾아보기**)</span><span class="sxs-lookup"><span data-stu-id="7bf69-608">Controller action name (**Browse**)</span></span>
   > 3. <span data-ttu-id="7bf69-609">경로 이름을 둘 다 지정 하는 매개 변수 값 (**장르**)과 값 (**장르 이름**)</span><span class="sxs-lookup"><span data-stu-id="7bf69-609">Route parameter values, specifying both the name (**Genre**) and the value (**Genre name**)</span></span>

<a id="Ex6Task9"></a>

<a id="Task_9_-_Running_the_Application"></a>
#### <a name="task-9---running-the-application"></a><span data-ttu-id="7bf69-610">태스크 9-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="7bf69-610">Task 9 - Running the Application</span></span>

<span data-ttu-id="7bf69-611">에서는이 작업을 테스트 각각 적절 한 링크와 함께 표시 되도록 **/저장소/찾아보기** URL입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-611">In this task, you will test that each Genre is displayed with a link to the appropriate **/Store/Browse** URL.</span></span>

1. <span data-ttu-id="7bf69-612">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-612">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="7bf69-613">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-613">The project starts in the Home page.</span></span> <span data-ttu-id="7bf69-614">URL을 변경 **/저장소** 각각을 적절 한 링크를 확인 하려면 **/저장소/찾아보기** URL입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-614">Change the URL to **/Store** to verify that each Genre links to the appropriate **/Store/Browse** URL.</span></span>

    <span data-ttu-id="7bf69-615">![찾아보기 페이지에 대 한 링크와 장르 검색](aspnet-mvc-4-fundamentals/_static/image33.png "찾아보기 페이지에 대 한 링크와 장르 검색")</span><span class="sxs-lookup"><span data-stu-id="7bf69-615">![Browsing Genres with links to Browse page](aspnet-mvc-4-fundamentals/_static/image33.png "Browsing Genres with links to Browse page")</span></span>

    <span data-ttu-id="7bf69-616">*찾아보기 페이지에 대 한 링크와 장르 검색*</span><span class="sxs-lookup"><span data-stu-id="7bf69-616">*Browsing Genres with links to Browse page*</span></span>

<a id="Ex6Task10"></a>

<a id="Task_10_-_Using_Dynamic_ViewModel_Collection_to_Pass_Values"></a>
#### <a name="task-10---using-dynamic-viewmodel-collection-to-pass-values"></a><span data-ttu-id="7bf69-617">태스크 10-값을 전달 하기를 사용 하 여 동적 ViewModel 컬렉션</span><span class="sxs-lookup"><span data-stu-id="7bf69-617">Task 10 - Using Dynamic ViewModel Collection to Pass Values</span></span>

<span data-ttu-id="7bf69-618">이 작업에서는 값을 전달 하는 컨트롤러와 뷰 간에 모델에 변경 하지 않고 단순 하 고 강력한 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-618">In this task, you will learn a simple and powerful method to pass values between the Controller and the View without making any changes in the Model.</span></span> <span data-ttu-id="7bf69-619">컬렉션을 제공 하는 ASP.NET MVC 4 &quot;ViewModel&quot;, 모든 동적 값에 할당 및 컨트롤러와도 뷰 내에서 액세스할 수 있으며 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-619">ASP.NET MVC 4 provides the collection &quot;ViewModel&quot;, which can be assigned to any dynamic value and accessed inside controllers and views as well.</span></span>

<span data-ttu-id="7bf69-620">ViewBag 동적 컬렉션의 목록을 전달 하는 데 사용할 이제 &quot; **장르 별모양** &quot; 보기로 컨트롤러에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-620">You will now use the ViewBag dynamic collection to pass a list of &quot;**Starred genres**&quot; from the controller to the view.</span></span> <span data-ttu-id="7bf69-621">인덱스 저장소 보기를 액세스할 **ViewModel** 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-621">The Store Index view will access to **ViewModel** and display the information.</span></span>

1. <span data-ttu-id="7bf69-622">Visual Studio 창에 반환 하는 데 필요한 경우 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-622">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="7bf69-623">열기 **StoreController.cs** 수정 **인덱스** 목록을 만드는 메서드를 ViewModel 컬렉션으로 장르 별모양:</span><span class="sxs-lookup"><span data-stu-id="7bf69-623">Open **StoreController.cs** and modify **Index** method to create a list of starred genres into ViewModel collection :</span></span>


~~~
[!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample26.cs)]

> [!NOTE]
> You could also use the syntax **ViewBag[&quot;Starred&quot;]** to access the properties.
~~~
2. <span data-ttu-id="7bf69-624">별표 아이콘 **&quot;starred.png&quot;** 에 포함 된 **Source\Assets\Images** 이 랩의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-624">The star icon **&quot;starred.png&quot;** is included in the **Source\Assets\Images** folder of this lab.</span></span> <span data-ttu-id="7bf69-625">응용 프로그램을 추가 하기 위해 자신의 콘텐츠를 끌어 한 **Windows 탐색기** 창에는 **솔루션 탐색기** Visual Web Developer Express, 아래와 같이에서:</span><span class="sxs-lookup"><span data-stu-id="7bf69-625">In order to add it to the application, drag their content from a **Windows Explorer** window into the **Solution Explorer** in Visual Web Developer Express, as shown below:</span></span>

    <span data-ttu-id="7bf69-626">![솔루션에 추가 별 이미지](aspnet-mvc-4-fundamentals/_static/image34.png "솔루션 별 이미지 추가")</span><span class="sxs-lookup"><span data-stu-id="7bf69-626">![Adding star image to the solution](aspnet-mvc-4-fundamentals/_static/image34.png "Adding star image to the solution")</span></span>

    <span data-ttu-id="7bf69-627">*솔루션에 별 이미지 추가*</span><span class="sxs-lookup"><span data-stu-id="7bf69-627">*Adding star image to the solution*</span></span>
3. <span data-ttu-id="7bf69-628">보기를 열 **Store/Index.cshtml** 콘텐츠를 수정 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-628">Open the view **Store/Index.cshtml** and modify the content.</span></span> <span data-ttu-id="7bf69-629">읽기 합니다는 &quot;별모양&quot; 속성에는 **ViewBag** 컬렉션 현재 장르 이름이 목록에 게 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-629">You will read the &quot;starred&quot; property in the **ViewBag** collection, and ask if the current genre name is in the list.</span></span> <span data-ttu-id="7bf69-630">이 경우 장르 링크 오른쪽에서 별 모양 아이콘을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-630">In that case you will show a star icon right to the genre link.</span></span>
   <span data-ttu-id="7bf69-631">(C#)</span><span class="sxs-lookup"><span data-stu-id="7bf69-631">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample27.cshtml)]

<a id="Ex6Task11"></a>

<a id="Task_11_-_Running_the_Application"></a>
#### <a name="task-11---running-the-application"></a><span data-ttu-id="7bf69-632">태스크 11-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="7bf69-632">Task 11 - Running the Application</span></span>

<span data-ttu-id="7bf69-633">이 작업에서는 별표 장르 별 모양 아이콘을 표시를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-633">In this task, you will test that the starred genres display a star icon.</span></span>

1. <span data-ttu-id="7bf69-634">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-634">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="7bf69-635">프로젝트 시작 날짜는 **홈** 페이지.</span><span class="sxs-lookup"><span data-stu-id="7bf69-635">The project starts in the **Home** page.</span></span> <span data-ttu-id="7bf69-636">URL을 변경 **/저장소** 각 기능 갖춘된 장르 respecting 레이블에 있는지 확인 하려면:</span><span class="sxs-lookup"><span data-stu-id="7bf69-636">Change the URL to **/Store** to verify that each featured genre has the respecting label:</span></span>

    <span data-ttu-id="7bf69-637">![찾아보기 장르 별표 요소 기능이](aspnet-mvc-4-fundamentals/_static/image35.png "별표 요소와 장르 검색")</span><span class="sxs-lookup"><span data-stu-id="7bf69-637">![Browsing Genres with starred elements](aspnet-mvc-4-fundamentals/_static/image35.png "Browsing Genres with starred elements")</span></span>

    <span data-ttu-id="7bf69-638">*장르 별표 요소 검색*</span><span class="sxs-lookup"><span data-stu-id="7bf69-638">*Browsing Genres with starred elements*</span></span>

<a id="Exercise7"></a>

<a id="Exercise_7_A_lap_around_ASPNET_MVC_4_new_template"></a>
### <a name="exercise-7-a-lap-around-aspnet-mvc-4-new-template"></a><span data-ttu-id="7bf69-639">7 연습: ASP.NET MVC 4 새 템플릿 주위 랩</span><span class="sxs-lookup"><span data-stu-id="7bf69-639">Exercise 7: A lap around ASP.NET MVC 4 new template</span></span>

<span data-ttu-id="7bf69-640">이 연습에서는 탐색 ASP.NET MVC 4 프로젝트 템플릿, 향상 된 새 서식 파일의 가장 관련 기능 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-640">In this exercise, you will explore the enhancements in the ASP.NET MVC 4 project templates, taking a look at the most relevant features of the new template.</span></span>

<a id="Ex7Task1"></a>

<a id="Task_1_Exploring_the_ASPNET_MVC_4_Internet_Application_Template"></a>
#### <a name="task-1-exploring-the-aspnet-mvc-4-internet-application-template"></a><span data-ttu-id="7bf69-641">작업 1: 탐색 ASP.NET MVC 4 인터넷 응용 프로그램 템플릿</span><span class="sxs-lookup"><span data-stu-id="7bf69-641">Task 1: Exploring the ASP.NET MVC 4 Internet Application Template</span></span>

1. <span data-ttu-id="7bf69-642">아직 열지 않은 경우 시작 **VS Express for Web**</span><span class="sxs-lookup"><span data-stu-id="7bf69-642">If not already open, start **VS Express for Web**</span></span>
2. <span data-ttu-id="7bf69-643">선택 된 **파일 | 새로 만들기 | 프로젝트** 메뉴 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-643">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="7bf69-644">에 **새 프로젝트** 대화 상자에서 선택 된 **Visual C# | 웹** 서식 파일의 왼쪽된 창에서 트리를 선택 하 고는 **ASP.NET MVC 4 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-644">In the **New Project** dialog, select the **Visual C#|Web** template on the left pane tree, and choose the **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="7bf69-645">**이름** 프로젝트 *MusicStore* 하 고 업데이트는 **솔루션 이름** 를 *시작*, 다음 위치를 선택 (또는 기본값을 그대로 적용)를 클릭 하 고 **확인** .</span><span class="sxs-lookup"><span data-stu-id="7bf69-645">**Name** the project *MusicStore* and update the **solution name** to *Begin*, then select a location (or leave the default) and click **OK**.</span></span>

    <span data-ttu-id="7bf69-646">![새 ASP.NET MVC 4 프로젝트를 만드는](aspnet-mvc-4-fundamentals/_static/image36.png "새 ASP.NET MVC 4 프로젝트 만들기")</span><span class="sxs-lookup"><span data-stu-id="7bf69-646">![Creating a new ASP.NET MVC 4 Project](aspnet-mvc-4-fundamentals/_static/image36.png "Creating a new ASP.NET MVC 4 Project")</span></span>

    <span data-ttu-id="7bf69-647">*새 ASP.NET MVC 4 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="7bf69-647">*Creating a new ASP.NET MVC 4 Project*</span></span>
3. <span data-ttu-id="7bf69-648">에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서는 **인터넷 응용 프로그램** 프로젝트 템플릿과 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-648">In the **New ASP.NET MVC 4 Project** dialog, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="7bf69-649">표시 뷰 엔진으로 Razor 또는 ASPX 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-649">Notice you can select either Razor or ASPX as the view engine.</span></span>

    <span data-ttu-id="7bf69-650">![새 ASP.NET MVC 4 인터넷 응용 프로그램을 만드는](aspnet-mvc-4-fundamentals/_static/image37.png "새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기")</span><span class="sxs-lookup"><span data-stu-id="7bf69-650">![Creating a new ASP.NET MVC 4 Internet Application](aspnet-mvc-4-fundamentals/_static/image37.png "Creating a new ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="7bf69-651">*새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기*</span><span class="sxs-lookup"><span data-stu-id="7bf69-651">*Creating a new ASP.NET MVC 4 Internet Application*</span></span>

    > [!NOTE]
    > <span data-ttu-id="7bf69-652">ASP.NET MVC 3에서 razor 구문이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-652">Razor syntax has been introduced in ASP.NET MVC 3.</span></span> <span data-ttu-id="7bf69-653">목표의 문자 및 fast 및 워크플로 코딩 하는 유체 파일에 필요한 키 입력의 수를 최소화 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-653">Its goal is to minimize the number of characters and keystrokes required in a file, enabling a fast and fluid coding workflow.</span></span> <span data-ttu-id="7bf69-654">기존 C# /VB 또는 다른 razor 활용 하 여 언어 기술을 놀라운 HTML 생성 워크플로 수 있도록 하는 템플릿 태그 구문을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-654">Razor leverages existing C#/VB (or other) language skills and delivers a template markup syntax that enables an awesome HTML construction workflow.</span></span>
4. <span data-ttu-id="7bf69-655">키를 눌러 **F5** 솔루션을 실행 하 고 갱신 된 서식 파일을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-655">Press **F5** to run the solution and see the renewed template.</span></span> <span data-ttu-id="7bf69-656">다음 기능을 사용해 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-656">You can check out the following features:</span></span>

    1. <span data-ttu-id="7bf69-657">**최신 스타일 템플릿**</span><span class="sxs-lookup"><span data-stu-id="7bf69-657">**Modern-style templates**</span></span>

        <span data-ttu-id="7bf69-658">서식 파일 갱신 된, 더 많은 현대 수준의 스타일을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-658">The templates have been renewed, providing more modern-looking styles.</span></span>

        <span data-ttu-id="7bf69-659">![ASP.NET MVC 4 맞게 스타일을 다시 템플릿](aspnet-mvc-4-fundamentals/_static/image38.png "맞게 템플릿 스타일을 다시 ASP.NET MVC 4")</span><span class="sxs-lookup"><span data-stu-id="7bf69-659">![ASP.NET MVC 4 restyled templates](aspnet-mvc-4-fundamentals/_static/image38.png "ASP.NET MVC 4 restyled templates")</span></span>

        <span data-ttu-id="7bf69-660">*ASP.NET MVC 4 맞게 스타일을 다시 템플릿*</span><span class="sxs-lookup"><span data-stu-id="7bf69-660">*ASP.NET MVC 4 restyled templates*</span></span>
    2. <span data-ttu-id="7bf69-661">**자동 선택 렌더링**</span><span class="sxs-lookup"><span data-stu-id="7bf69-661">**Adaptive Rendering**</span></span>

        <span data-ttu-id="7bf69-662">체크 아웃 브라우저 창 크기 조정 고 페이지 레이아웃 새 창 크기를 동적으로 반응 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-662">Check out resizing the browser window and notice how the page layout dynamically adapts to the new window size.</span></span> <span data-ttu-id="7bf69-663">이러한 템플릿은 자동 선택 렌더링 기술을 사용 하 여 사용자 지정 하지 않고 데스크톱 및 모바일 플랫폼에서 모두 올바르게 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-663">These templates use the adaptive rendering technique to render properly in both desktop and mobile platforms without any customization.</span></span>

        <span data-ttu-id="7bf69-664">![다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿에서](aspnet-mvc-4-fundamentals/_static/image39.png "다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿")</span><span class="sxs-lookup"><span data-stu-id="7bf69-664">![ASP.NET MVC 4 project template in different browser sizes](aspnet-mvc-4-fundamentals/_static/image39.png "ASP.NET MVC 4 project template in different browser sizes")</span></span>

        <span data-ttu-id="7bf69-665">*다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿*</span><span class="sxs-lookup"><span data-stu-id="7bf69-665">*ASP.NET MVC 4 project template in different browser sizes*</span></span>
5. <span data-ttu-id="7bf69-666">디버거를 중지 하려면 Visual Studio로 되돌아가려면 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-666">Close the browser to stop the debugger and return to Visual Studio.</span></span>
6. <span data-ttu-id="7bf69-667">이제 솔루션을 탐색 하 고 체크 아웃 프로젝트 템플릿에 있는 ASP.NET MVC 4에서 도입 된 새로운 기능 중 일부를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-667">Now you are able to explore the solution and check out some of the new features introduced by ASP.NET MVC 4 in the project template.</span></span>

    <span data-ttu-id="7bf69-668">![ASP.NET mvc 4-인터넷-응용 프로그램-프로젝트-템플릿을](aspnet-mvc-4-fundamentals/_static/image40.png "ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿을")</span><span class="sxs-lookup"><span data-stu-id="7bf69-668">![ASP.NET MVC4-internet-application-project-template](aspnet-mvc-4-fundamentals/_static/image40.png "The ASP.NET MVC 4 Internet Application Project Template")</span></span>

    <span data-ttu-id="7bf69-669">*ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿*</span><span class="sxs-lookup"><span data-stu-id="7bf69-669">*The ASP.NET MVC 4 Internet Application Project Template*</span></span>

   1. <span data-ttu-id="7bf69-670">**HTML5 태그**</span><span class="sxs-lookup"><span data-stu-id="7bf69-670">**HTML5 markup**</span></span>

       <span data-ttu-id="7bf69-671">예를 들어 열린 새 테마 마크업 알아보려면 템플릿 보기 찾아보기 **About.cshtml** 내의 볼 **홈** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-671">Browse template views to find out the new theme markup, for example open **About.cshtml** view within **Home** folder.</span></span>

       <span data-ttu-id="7bf69-672">![Razor 및 HTML5 태그를 사용 하 여 새로운 템플릿을](aspnet-mvc-4-fundamentals/_static/image41.png "Razor 및 HTML5 태그를 사용 하 여 새 서식 파일")</span><span class="sxs-lookup"><span data-stu-id="7bf69-672">![New template, using Razor and HTML5 markup](aspnet-mvc-4-fundamentals/_static/image41.png "New template, using Razor and HTML5 markup")</span></span>

       <span data-ttu-id="7bf69-673">*Razor 및 HTML5 태그를 사용 하 여 새 서식 파일*</span><span class="sxs-lookup"><span data-stu-id="7bf69-673">*New template, using Razor and HTML5 markup*</span></span>
   2. <span data-ttu-id="7bf69-674">**포함 된 JavaScript 라이브러리**</span><span class="sxs-lookup"><span data-stu-id="7bf69-674">**JavaScript libraries included**</span></span>

      1. <span data-ttu-id="7bf69-675">**jQuery**: jQuery HTML 문서 통과, 이벤트 처리, 애니메이션, 및 Ajax 상호 작용을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-675">**jQuery**: jQuery simplifies HTML document traversing, event handling, animating, and Ajax interactions.</span></span>
      2. <span data-ttu-id="7bf69-676">**jQuery UI**:이 라이브러리는 낮은 수준의 상호 작용 및 애니메이션 효과 고급 및 스타일 widgets, jQuery JavaScript 라이브러리를 기반으로 빌드된에 대 한 추상화를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-676">**jQuery UI**: This library provides abstractions for low-level interaction and animation, advanced effects and themeable widgets, built on top of the jQuery JavaScript Library.</span></span>

         > [!NOTE]
         > <span data-ttu-id="7bf69-677">JQuery 및 jQuery UI에 대해 알아볼 수 있습니다에 [ [ http://docs.jquery.com/ ](http://docs.jquery.com/) ](http://docs.jquery.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-677">You can learn about jQuery and jQuery UI in [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span></span>
      3. <span data-ttu-id="7bf69-678">**KnockoutJS**: ASP.NET MVC 4의 기본 서식 파일에 포함 되어 이제 **KnockoutJS**, JavaScript 및 HTML을 사용 하 여 풍부 하 고 응답성 높은 웹 응용 프로그램을 만들 수 있는 JavaScript MVVM 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-678">**KnockoutJS**: The ASP.NET MVC 4 default template now includes **KnockoutJS**, a JavaScript MVVM framework that lets you create rich and highly responsive web applications using JavaScript and HTML.</span></span> <span data-ttu-id="7bf69-679">와 같은 ASP.NET MVC 3, jQuery 및 jQuery UI 라이브러리에에서도 나와 ASP.NET MVC 4입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-679">Like in ASP.NET MVC 3, jQuery and jQuery UI libraries are also included in ASP.NET MVC 4.</span></span>

          > [!NOTE]
          > <span data-ttu-id="7bf69-680">이 링크에 KnockOutJS 라이브러리에 대 한 자세한 정보를 얻을 수 있습니다: [ http://learn.knockoutjs.com/ ](http://learn.knockoutjs.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-680">You can get more information about KnockOutJS library in this link: [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/).</span></span>
      4. <span data-ttu-id="7bf69-681">**Modernizr**:이 라이브러리에서는 호환성이 사이트 이전 브라우저 HTML5 및 CSS3 기술을 사용할 때 자동으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-681">**Modernizr**: This library runs automatically, making your site compatible with older browsers when using HTML5 and CSS3 technologies.</span></span>

          > [!NOTE]
          > <span data-ttu-id="7bf69-682">이 링크에 Modernizr 라이브러리에 대 한 자세한 정보를 얻을 수 있습니다: [ http://www.modernizr.com/ ](http://www.modernizr.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-682">You can get more information about Modernizr library in this link: [http://www.modernizr.com/](http://www.modernizr.com/).</span></span>
   3. <span data-ttu-id="7bf69-683">**SimpleMembership 솔루션에 포함**</span><span class="sxs-lookup"><span data-stu-id="7bf69-683">**SimpleMembership included in the solution**</span></span>

       <span data-ttu-id="7bf69-684">SimpleMembership는 이전 ASP.NET 역할 및 멤버 자격 공급자 시스템에 대 한 대체 값으로 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-684">SimpleMembership has been designed as a replacement for the previous ASP.NET Role and Membership provider system.</span></span> <span data-ttu-id="7bf69-685">도와 주는 개발자가 보안 웹 페이지를 보다 융통성 있는 방식으로 여러 가지 새로운 기능이 있음</span><span class="sxs-lookup"><span data-stu-id="7bf69-685">It has many new features that make it easier for the developer to secure web pages in a more flexible way.</span></span>

       <span data-ttu-id="7bf69-686">인터넷 템플릿을 이미 설정한 SimpleMembership를 통합 하는 몇 가지, OAuthWebSecurity (에 대 한 OAuth 계정 등록, 로그인, 관리, 등) 및 웹 보안을 사용 하 여 AccountController 준비 예를 들어 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-686">The Internet template already has set up a few things to integrate SimpleMembership, for example, the AccountController is prepared to use OAuthWebSecurity (for OAuth account registration, login, management, etc.) and Web Security.</span></span>

       <span data-ttu-id="7bf69-687">![솔루션에 포함 된 SimpleMembership](aspnet-mvc-4-fundamentals/_static/image42.png "SimpleMembership 솔루션에 포함")</span><span class="sxs-lookup"><span data-stu-id="7bf69-687">![SimpleMembership Included in the solution](aspnet-mvc-4-fundamentals/_static/image42.png "SimpleMembership Included in the solution")</span></span>

       <span data-ttu-id="7bf69-688">*SimpleMembership 솔루션에 포함*</span><span class="sxs-lookup"><span data-stu-id="7bf69-688">*SimpleMembership Included in the solution*</span></span>

       > [!NOTE]
       > <span data-ttu-id="7bf69-689">에 대 한 자세한 내용을 보려면 [OAuthWebSecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) MSDN에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-689">Find more information about [OAuthWebSecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) in MSDN.</span></span>

> [!NOTE]
> <span data-ttu-id="7bf69-690">다음 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수는 또한 [부록 b: 게시 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램](#AppendixB)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-690">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>


* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="7bf69-691">요약</span><span class="sxs-lookup"><span data-stu-id="7bf69-691">Summary</span></span>

<span data-ttu-id="7bf69-692">이 실습 랩을 완료 하 여 ASP.NET MVC의 기본적인 사항을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-692">By completing this Hands-On Lab you have learned the fundamentals of ASP.NET MVC:</span></span>

- <span data-ttu-id="7bf69-693">MVC 응용 프로그램 및 조작 방법을의 핵심 요소</span><span class="sxs-lookup"><span data-stu-id="7bf69-693">The core elements of an MVC application and how they interact</span></span>
- <span data-ttu-id="7bf69-694">ASP.NET MVC 응용 프로그램을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="7bf69-694">How to create an ASP.NET MVC Application</span></span>
- <span data-ttu-id="7bf69-695">URL 및 쿼리 문자열을 통해 전달 된 추가 하 고 매개 변수를 처리 하기 위해 컨트롤러를 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="7bf69-695">How to add and configure Controllers to handle parameters passed through the URL and querystring</span></span>
- <span data-ttu-id="7bf69-696">공통 HTML 콘텐츠, 모양 및 HTML 콘텐츠를 표시 하려면 보기 서식 파일을 개선 하는 스타일 시트에 대 한 템플릿을 설정 하는 레이아웃 마스터 페이지를 추가 하는 방법</span><span class="sxs-lookup"><span data-stu-id="7bf69-696">How to add a layout master page to setup a template for common HTML content, a StyleSheet to enhance the look and feel and a View template to display HTML content</span></span>
- <span data-ttu-id="7bf69-697">동적 정보를 표시 하려면 템플릿 보기에 속성을 전달 하기 위한 ViewModel 패턴을 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="7bf69-697">How to use the ViewModel pattern for passing properties to the View template to display dynamic information</span></span>
- <span data-ttu-id="7bf69-698">템플릿 보기에서에서 컨트롤러에 전달 된 매개 변수를 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="7bf69-698">How to use parameters passed to Controllers in the View template</span></span>
- <span data-ttu-id="7bf69-699">ASP.NET MVC 응용 프로그램 내 페이지에 대 한 링크를 추가 하는 방법</span><span class="sxs-lookup"><span data-stu-id="7bf69-699">How to add links to pages inside the ASP.NET MVC application</span></span>
- <span data-ttu-id="7bf69-700">추가 하 고 보기에서 동적 속성을 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="7bf69-700">How to add and use dynamic properties in a View</span></span>
- <span data-ttu-id="7bf69-701">ASP.NET MVC 4 프로젝트 템플릿의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="7bf69-701">The enhancements in the ASP.NET MVC 4 project templates</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="7bf69-702">부록 a: 설치 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="7bf69-702">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="7bf69-703">설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 버전을 사용 하 여 **[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="7bf69-703">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="7bf69-704">다음 지침을 설치 하는 데 필요한 단계를 안내 하 *Visual studio Express 2012 for Web* 를 사용 하 여 *Microsoft 웹 플랫폼 설치 관리자*합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-704">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="7bf69-705">로 이동 [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-705">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="7bf69-706">또는 이미 설치 된 웹 플랫폼 설치 관리자를 열 수 있습니다 및 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Web Windows Azure SDK와</em>&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-706">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="7bf69-707">클릭 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-707">Click on **Install Now**.</span></span> <span data-ttu-id="7bf69-708">없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-708">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="7bf69-709">한 번 **웹 플랫폼 설치 관리자** 열려 클릭 **설치** 는 설치 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-709">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="7bf69-710">![Visual Studio Express 설치](aspnet-mvc-4-fundamentals/_static/image43.png "Visual Studio Express 설치")</span><span class="sxs-lookup"><span data-stu-id="7bf69-710">![Install Visual Studio Express](aspnet-mvc-4-fundamentals/_static/image43.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="7bf69-711">*Visual Studio Express 설치*</span><span class="sxs-lookup"><span data-stu-id="7bf69-711">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="7bf69-712">모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-712">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건 동의](aspnet-mvc-4-fundamentals/_static/image44.png)

    <span data-ttu-id="7bf69-714">*사용 조건 동의*</span><span class="sxs-lookup"><span data-stu-id="7bf69-714">*Accepting the license terms*</span></span>
5. <span data-ttu-id="7bf69-715">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-715">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](aspnet-mvc-4-fundamentals/_static/image45.png)

    <span data-ttu-id="7bf69-717">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="7bf69-717">*Installation progress*</span></span>
6. <span data-ttu-id="7bf69-718">설치가 완료 되 면 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-718">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](aspnet-mvc-4-fundamentals/_static/image46.png)

    <span data-ttu-id="7bf69-720">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="7bf69-720">*Installation completed*</span></span>
7. <span data-ttu-id="7bf69-721">클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-721">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="7bf69-722">Visual Studio Express for Web을 열려면로 이동는 **시작** 화면를 쓰기 시작할 &quot; **VS Express**&quot;, 클릭는 **VS Express for Web** 바둑판식 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-722">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![웹 타일에 대 한 VS Express](aspnet-mvc-4-fundamentals/_static/image47.png)

    <span data-ttu-id="7bf69-724">*웹 타일에 대 한 VS Express*</span><span class="sxs-lookup"><span data-stu-id="7bf69-724">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="7bf69-725">부록 b: 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="7bf69-725">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="7bf69-726">이 부록에서는 Windows Azure 관리 포털에서 새 웹 사이트를 만들고 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하기 위해 랩에서 수행 하 여 가져온 응용 프로그램을 게시 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-726">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="7bf69-727">작업 1-Windows에서 새 웹 사이트를 만드는 Azure 포털</span><span class="sxs-lookup"><span data-stu-id="7bf69-727">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="7bf69-728">이동 하 여 [Windows Azure 관리 포털](https://manage.windowsazure.com/) 구독에 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-728">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7bf69-729">Windows Azure를 무료로 10 개 ASP.NET 웹 사이트를 호스트 하 고 트래픽이 증가 됨을 확장 한 다음 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-729">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="7bf69-730">등록할 수 [여기](http://aka.ms/aspnet-hol-azure)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-730">You can sign up [here](http://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="7bf69-731">![Windows Azure 포털에 로그온](aspnet-mvc-4-fundamentals/_static/image48.png "Windows Azure 포털에 로그인")</span><span class="sxs-lookup"><span data-stu-id="7bf69-731">![Log on to Windows Azure portal](aspnet-mvc-4-fundamentals/_static/image48.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="7bf69-732">*Windows Azure 관리 포털에 로그온*</span><span class="sxs-lookup"><span data-stu-id="7bf69-732">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="7bf69-733">클릭 **새로** 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-733">Click **New** on the command bar.</span></span>

    <span data-ttu-id="7bf69-734">![새 웹 사이트를 만드는](aspnet-mvc-4-fundamentals/_static/image49.png "새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="7bf69-734">![Creating a new Web Site](aspnet-mvc-4-fundamentals/_static/image49.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="7bf69-735">*새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="7bf69-735">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="7bf69-736">클릭 **계산** | **웹 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-736">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="7bf69-737">그런 다음 선택 **빠른 생성** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-737">Then select **Quick Create** option.</span></span> <span data-ttu-id="7bf69-738">새 웹 사이트에 대 한 사용 가능한 URL을 입력 하 고 클릭 **웹 사이트 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-738">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7bf69-739">Windows Azure 웹 사이트는 호스트를 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-739">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="7bf69-740">빨리 만들기 옵션을 사용 하면 완성 된 웹 응용 프로그램을 Windows Azure 웹 사이트에서 포털 외부에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-740">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="7bf69-741">데이터베이스를 설정 하기 위한 단계는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-741">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="7bf69-742">![빠른 생성을 사용 하 여 새 웹 사이트를 만드는](aspnet-mvc-4-fundamentals/_static/image50.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="7bf69-742">![Creating a new Web Site using Quick Create](aspnet-mvc-4-fundamentals/_static/image50.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="7bf69-743">*빠른 생성을 사용 하 여 새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="7bf69-743">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="7bf69-744">새 될 때까지 기다렸다가 **웹 사이트** 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-744">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="7bf69-745">웹 사이트가 만들어지면 아래 링크를 클릭 하 고 **URL** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-745">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="7bf69-746">새 웹 사이트가 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-746">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="7bf69-747">![새 웹 사이트를 찾아](aspnet-mvc-4-fundamentals/_static/image51.png "새 웹 사이트를 검색 합니다.")</span><span class="sxs-lookup"><span data-stu-id="7bf69-747">![Browsing to the new web site](aspnet-mvc-4-fundamentals/_static/image51.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="7bf69-748">*새 웹 사이트를 검색합니다.*</span><span class="sxs-lookup"><span data-stu-id="7bf69-748">*Browsing to the new web site*</span></span>

    <span data-ttu-id="7bf69-749">![실행 중인 웹 사이트](aspnet-mvc-4-fundamentals/_static/image52.png "실행 중인 웹 사이트")</span><span class="sxs-lookup"><span data-stu-id="7bf69-749">![Web site running](aspnet-mvc-4-fundamentals/_static/image52.png "Web site running")</span></span>

    <span data-ttu-id="7bf69-750">*실행 중인 웹 사이트*</span><span class="sxs-lookup"><span data-stu-id="7bf69-750">*Web site running*</span></span>
6. <span data-ttu-id="7bf69-751">포털로 돌아가서 아래에서 웹 사이트의 이름을 클릭는 **이름** 관리 페이지를 표시 하는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-751">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="7bf69-752">![웹 사이트 관리 페이지 열기](aspnet-mvc-4-fundamentals/_static/image53.png "웹 사이트 관리 페이지 열기")</span><span class="sxs-lookup"><span data-stu-id="7bf69-752">![Opening the web site management pages](aspnet-mvc-4-fundamentals/_static/image53.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="7bf69-753">*웹 사이트 관리 페이지 열기*</span><span class="sxs-lookup"><span data-stu-id="7bf69-753">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="7bf69-754">에 **대시보드** 페이지의 **눈에 보는** 섹션에서 클릭는 **게시 프로필 다운로드** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-754">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7bf69-755">*게시 프로필* 각각의 활성화 된 게시 방법에 대 한 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 하는 데 필요한 정보가 모두 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-755">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="7bf69-756">게시 프로필에는 Url, 사용자 자격 증명 및 연결 하 고 각 게시 메서드를 사용할 수 있는 끝점에 대해 인증 하는 데 필요한 데이터베이스 문자열이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-756">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="7bf69-757">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 읽는 지원 하기 위해 게시 프로필에 대 한 이러한 프로그램의 구성을 자동화 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-757">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="7bf69-758">![게시 프로필 다운로드 웹 사이트](aspnet-mvc-4-fundamentals/_static/image54.png "게시 프로필 다운로드 웹 사이트")</span><span class="sxs-lookup"><span data-stu-id="7bf69-758">![Downloading the web site publish profile](aspnet-mvc-4-fundamentals/_static/image54.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="7bf69-759">*게시 프로필 다운로드 웹 사이트*</span><span class="sxs-lookup"><span data-stu-id="7bf69-759">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="7bf69-760">알려진된 위치에 게시 프로필 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-760">Download the publish profile file to a known location.</span></span> <span data-ttu-id="7bf69-761">더 이상이 연습에서는 Visual Studio에서 웹 응용 프로그램 Windows Azure 웹 사이트를 게시 하려면이 파일을 사용 하는 방법을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-761">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="7bf69-762">![게시 프로필 파일을 저장](aspnet-mvc-4-fundamentals/_static/image55.png "게시 프로필 저장")</span><span class="sxs-lookup"><span data-stu-id="7bf69-762">![Saving the publish profile file](aspnet-mvc-4-fundamentals/_static/image55.png "Saving the publish profile")</span></span>

    <span data-ttu-id="7bf69-763">*게시 프로필 파일을 저장합니다.*</span><span class="sxs-lookup"><span data-stu-id="7bf69-763">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="7bf69-764">작업 2-데이터베이스 서버 구성</span><span class="sxs-lookup"><span data-stu-id="7bf69-764">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="7bf69-765">응용 프로그램에서 SQL Server를 활용 하는 경우 데이터베이스를 SQL 데이터베이스 서버 만들기 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-765">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="7bf69-766">SQL Server를 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 태스크를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-766">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="7bf69-767">응용 프로그램 데이터베이스를 저장 하기 위해 SQL 데이터베이스 서버를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-767">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="7bf69-768">Windows Azure 관리 포털에서 구독의 SQL 데이터베이스 서버를 볼 수 있습니다 **Sql 데이터베이스** | **서버** | **서버 대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-768">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="7bf69-769">만든 서버 없는 경우 수행 하 여 만들 수 있습니다는 **추가** 명령 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-769">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="7bf69-770">기록해는 **서버 이름 및 URL, 관리자 로그인 이름 및 암호**, 다음 작업에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-770">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="7bf69-771">만들지 마십시오 데이터베이스 아직 대로 이후 단계에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-771">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="7bf69-772">![SQL 데이터베이스 서버 대시보드](aspnet-mvc-4-fundamentals/_static/image56.png "SQL 데이터베이스 서버 대시보드")</span><span class="sxs-lookup"><span data-stu-id="7bf69-772">![SQL Database Server Dashboard](aspnet-mvc-4-fundamentals/_static/image56.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="7bf69-773">*SQL 데이터베이스 서버 대시보드*</span><span class="sxs-lookup"><span data-stu-id="7bf69-773">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="7bf69-774">다음 태스크에서는 서버 목록에 사용자의 로컬 IP 주소를 포함 해야 이러한 이유로 Visual Studio에서 데이터베이스 연결을 테스트 **허용 IP 주소**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-774">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="7bf69-775">작업을 수행 하려면 **구성**에서 IP 주소를 선택 **현재 클라이언트 IP 주소** 에 붙여넣습니다는 **시작 IP 주소** 및 **끝IP주소** 클릭 하 고 텍스트 상자는 ![add-client-ip-address-ok-button](aspnet-mvc-4-fundamentals/_static/image57.png) 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-775">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-fundamentals/_static/image57.png) button.</span></span>

    ![클라이언트 IP 주소를 추가합니다.](aspnet-mvc-4-fundamentals/_static/image58.png)

    <span data-ttu-id="7bf69-777">*클라이언트 IP 주소를 추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="7bf69-777">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="7bf69-778">한 번는 **클라이언트 IP 주소** 허용된 된 IP 주소에 추가 됩니다 목록에서 클릭 **저장** 하 여 변경 사항을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-778">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![변경 확인](aspnet-mvc-4-fundamentals/_static/image59.png)

    <span data-ttu-id="7bf69-780">*변경 확인*</span><span class="sxs-lookup"><span data-stu-id="7bf69-780">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="7bf69-781">작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="7bf69-781">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="7bf69-782">ASP.NET MVC 4 솔루션으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-782">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="7bf69-783">에 **솔루션 탐색기**웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-783">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="7bf69-784">![응용 프로그램을 게시](aspnet-mvc-4-fundamentals/_static/image60.png "응용 프로그램을 게시")</span><span class="sxs-lookup"><span data-stu-id="7bf69-784">![Publishing the Application](aspnet-mvc-4-fundamentals/_static/image60.png "Publishing the Application")</span></span>

    <span data-ttu-id="7bf69-785">*웹 사이트를 게시*</span><span class="sxs-lookup"><span data-stu-id="7bf69-785">*Publishing the web site*</span></span>
2. <span data-ttu-id="7bf69-786">첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-786">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="7bf69-787">![게시 프로필 가져오기](aspnet-mvc-4-fundamentals/_static/image61.png "게시 프로필 가져오기")</span><span class="sxs-lookup"><span data-stu-id="7bf69-787">![Importing the publish profile](aspnet-mvc-4-fundamentals/_static/image61.png "Importing the publish profile")</span></span>

    <span data-ttu-id="7bf69-788">*게시 프로필 가져오기*</span><span class="sxs-lookup"><span data-stu-id="7bf69-788">*Importing publish profile*</span></span>
3. <span data-ttu-id="7bf69-789">클릭 **연결 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-789">Click **Validate Connection**.</span></span> <span data-ttu-id="7bf69-790">유효성 검사가 완료 되 면 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-790">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7bf69-791">연결 유효성 검사 단추 옆에 표시 녹색 확인 표시가 표시 되 면 유효성 검사가 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-791">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="7bf69-792">![연결 유효성 검사](aspnet-mvc-4-fundamentals/_static/image62.png "연결 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="7bf69-792">![Validating connection](aspnet-mvc-4-fundamentals/_static/image62.png "Validating connection")</span></span>

    <span data-ttu-id="7bf69-793">*연결 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="7bf69-793">*Validating connection*</span></span>
4. <span data-ttu-id="7bf69-794">에 **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆의 단추 클릭 (즉, **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="7bf69-794">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="7bf69-795">![웹 배포 구성](aspnet-mvc-4-fundamentals/_static/image63.png "웹 배포 구성")</span><span class="sxs-lookup"><span data-stu-id="7bf69-795">![Web deploy configuration](aspnet-mvc-4-fundamentals/_static/image63.png "Web deploy configuration")</span></span>

    <span data-ttu-id="7bf69-796">*웹 배포 구성*</span><span class="sxs-lookup"><span data-stu-id="7bf69-796">*Web deploy configuration*</span></span>
5. <span data-ttu-id="7bf69-797">다음과 같이 데이터베이스 연결을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-797">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="7bf69-798">에 **서버 이름** SQL 데이터베이스 서버 URL 사용 하 여 입력 된 *tcp:* 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-798">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="7bf69-799">**사용자 이름** 서버 관리자 로그인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-799">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="7bf69-800">**암호** 서버 관리자 로그인 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-800">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="7bf69-801">예를 들어 새 데이터베이스 이름 입력: *MVC4SampleDB*합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-801">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="7bf69-802">![대상 연결 문자열 구성](aspnet-mvc-4-fundamentals/_static/image64.png "대상 연결 문자열 구성")</span><span class="sxs-lookup"><span data-stu-id="7bf69-802">![Configuring destination connection string](aspnet-mvc-4-fundamentals/_static/image64.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="7bf69-803">*대상 연결 문자열 구성*</span><span class="sxs-lookup"><span data-stu-id="7bf69-803">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="7bf69-804">그런 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-804">Then click **OK**.</span></span> <span data-ttu-id="7bf69-805">데이터베이스를 만들려는 대화 상자가 나타나면 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-805">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="7bf69-806">![데이터베이스를 만드는](aspnet-mvc-4-fundamentals/_static/image65.png "데이터베이스 문자열 만들기")</span><span class="sxs-lookup"><span data-stu-id="7bf69-806">![Creating the database](aspnet-mvc-4-fundamentals/_static/image65.png "Creating the database string")</span></span>

    <span data-ttu-id="7bf69-807">*데이터베이스를 만드는 중*</span><span class="sxs-lookup"><span data-stu-id="7bf69-807">*Creating the database*</span></span>
7. <span data-ttu-id="7bf69-808">Windows azure에서 SQL 데이터베이스에 연결 하기 위해 사용할 연결 문자열은 기본 연결 텍스트 상자 내에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-808">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="7bf69-809">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-809">Then click **Next**.</span></span>

    <span data-ttu-id="7bf69-810">![SQL 데이터베이스를 가리키는 연결 문자열](aspnet-mvc-4-fundamentals/_static/image66.png "SQL 데이터베이스를 가리키는 연결 문자열")</span><span class="sxs-lookup"><span data-stu-id="7bf69-810">![Connection string pointing to SQL Database](aspnet-mvc-4-fundamentals/_static/image66.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="7bf69-811">*SQL 데이터베이스를 가리키는 연결 문자열*</span><span class="sxs-lookup"><span data-stu-id="7bf69-811">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="7bf69-812">에 **미리 보기** 페이지 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-812">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="7bf69-813">![웹 응용 프로그램을 게시](aspnet-mvc-4-fundamentals/_static/image67.png "웹 응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="7bf69-813">![Publishing the web application](aspnet-mvc-4-fundamentals/_static/image67.png "Publishing the web application")</span></span>

    <span data-ttu-id="7bf69-814">*웹 응용 프로그램 게시*</span><span class="sxs-lookup"><span data-stu-id="7bf69-814">*Publishing the web application*</span></span>
9. <span data-ttu-id="7bf69-815">게시 프로세스가 완료 되 면 게시 된 웹 사이트 기본 브라우저가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-815">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="7bf69-816">![Windows Azure에 게시 된 응용 프로그램](aspnet-mvc-4-fundamentals/_static/image68.png "Windows Azure에 게시 된 응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="7bf69-816">![Application published to Windows Azure](aspnet-mvc-4-fundamentals/_static/image68.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="7bf69-817">*Windows Azure에 게시 된 응용 프로그램*</span><span class="sxs-lookup"><span data-stu-id="7bf69-817">*Application published to Windows Azure*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="7bf69-818">부록 c: 코드 조각을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="7bf69-818">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="7bf69-819">코드 조각 바로 쉽게 얻습니다 필요한 코드를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-819">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="7bf69-820">랩 문서는 알려 정확 하 게 사용 가능 시기, 다음 그림에 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-820">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="7bf69-821">![Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여](aspnet-mvc-4-fundamentals/_static/image69.png "Visual Studio를 사용 하 여 코드 조각을 프로젝트에 코드를 삽입 하려면")</span><span class="sxs-lookup"><span data-stu-id="7bf69-821">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-fundamentals/_static/image69.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="7bf69-822">*Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여*</span><span class="sxs-lookup"><span data-stu-id="7bf69-822">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="7bf69-823">***키보드 (C#만)를 사용 하 여 코드 조각을 추가 하려면***</span><span class="sxs-lookup"><span data-stu-id="7bf69-823">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="7bf69-824">코드를 삽입 하려는 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-824">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="7bf69-825">공백 또는 하이픈만) (없이 코드 조각 이름을 입력 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-825">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="7bf69-826">IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-826">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="7bf69-827">올바른 코드 조각 선택 (또는 전체 코드 조각이 이름이 선택 될 때까지 입력 유지).</span><span class="sxs-lookup"><span data-stu-id="7bf69-827">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="7bf69-828">커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-828">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="7bf69-829">![코드 조각 이름을 입력 하기 시작](aspnet-mvc-4-fundamentals/_static/image70.png "조각 이름을 입력 하기 시작")</span><span class="sxs-lookup"><span data-stu-id="7bf69-829">![Start typing the snippet name](aspnet-mvc-4-fundamentals/_static/image70.png "Start typing the snippet name")</span></span>

<span data-ttu-id="7bf69-830">*코드 조각 이름을 입력 하기 시작*</span><span class="sxs-lookup"><span data-stu-id="7bf69-830">*Start typing the snippet name*</span></span>

<span data-ttu-id="7bf69-831">![Tab 키를 눌러 강조 표시 된 코드 조각 선택](aspnet-mvc-4-fundamentals/_static/image71.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")</span><span class="sxs-lookup"><span data-stu-id="7bf69-831">![Press Tab to select the highlighted snippet](aspnet-mvc-4-fundamentals/_static/image71.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="7bf69-832">*Tab 키를 눌러 강조 표시 된 코드 조각 선택*</span><span class="sxs-lookup"><span data-stu-id="7bf69-832">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="7bf69-833">![확장 하 고 Tab 키를 눌러 다시 코드 조각](aspnet-mvc-4-fundamentals/_static/image72.png "확장 하 고 Tab 키를 눌러 다시 코드 조각")</span><span class="sxs-lookup"><span data-stu-id="7bf69-833">![Press Tab again and the snippet will expand](aspnet-mvc-4-fundamentals/_static/image72.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="7bf69-834">*확장 하 고 Tab 키를 눌러 다시 코드 조각*</span><span class="sxs-lookup"><span data-stu-id="7bf69-834">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="7bf69-835">***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-835">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="7bf69-836">코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-836">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="7bf69-837">선택 **조각 삽입** 이어서 **내 코드 조각**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-837">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="7bf69-838">클릭 하 여 목록에서 관련 조각을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf69-838">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="7bf69-839">![코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭](aspnet-mvc-4-fundamentals/_static/image73.png "코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추 클릭")</span><span class="sxs-lookup"><span data-stu-id="7bf69-839">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-fundamentals/_static/image73.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="7bf69-840">*코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭*</span><span class="sxs-lookup"><span data-stu-id="7bf69-840">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="7bf69-841">![클릭 하 여 목록에서 관련 조각을 선택](aspnet-mvc-4-fundamentals/_static/image74.png "클릭 하 여 목록에서 관련 조각을 선택")</span><span class="sxs-lookup"><span data-stu-id="7bf69-841">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-fundamentals/_static/image74.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="7bf69-842">*클릭 하 여 목록에서 관련 조각을 선택합니다*</span><span class="sxs-lookup"><span data-stu-id="7bf69-842">*Pick the relevant snippet from the list, by clicking on it*</span></span>
