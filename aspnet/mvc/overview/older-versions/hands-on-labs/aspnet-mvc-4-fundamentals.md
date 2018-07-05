---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
title: ASP.NET MVC 4 기본 사항 | Microsoft Docs
author: rick-anderson
description: 이 실습 랩에서 MVC (Model View Controller) Music Store 자습서 응용 프로그램을 소개 하 고 ASP.NET MV를 사용 하는 방법을 단계별로 설명를 기반으로 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: b7dba543-73c3-4534-a9a0-ba70fa2c6a8a
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
msc.type: authoredcontent
ms.openlocfilehash: 3a282d02ba929eb86571e92f190550614962524d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37386577"
---
# <a name="aspnet-mvc-4-fundamentals"></a><span data-ttu-id="405d3-103">ASP.NET MVC 4 기본 사항</span><span class="sxs-lookup"><span data-stu-id="405d3-103">ASP.NET MVC 4 Fundamentals</span></span>

<span data-ttu-id="405d3-104">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="405d3-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="405d3-105">웹 캠프 학습 키트 다운로드</span><span class="sxs-lookup"><span data-stu-id="405d3-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="405d3-106">이 실습 랩에서 MVC (Model View Controller) Music Store 자습서 응용 프로그램을 소개 하 고 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 설명를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-106">This Hands-On Lab is based on MVC (Model View Controller) Music Store, a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio.</span></span> <span data-ttu-id="405d3-107">간단 하 게, 연구소에서 배웁니다 함께 이러한 기술을 사용 하는 아직 power 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-107">Throughout the lab you will learn the simplicity, yet power of using these technologies together.</span></span> <span data-ttu-id="405d3-108">간단한 응용 프로그램을 시작 하 고 모든 기능을 갖춘 ASP.NET MVC 4 웹 응용 프로그램을 수 있을 때까지 빌드합니다 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-108">You will start with a simple application and will build it until you have a fully functional ASP.NET MVC 4 Web Application.</span></span>

<span data-ttu-id="405d3-109">이 랩에서 ASP.NET MVC 4를 사용 하 여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-109">This Lab works with ASP.NET MVC 4.</span></span>

<span data-ttu-id="405d3-110">자습서 응용 프로그램의 ASP.NET MVC 3 버전을 탐색 하려는 경우에서 찾을 수 있습니다 [MVC 음악 스토어](https://github.com/evilDave/MVC-Music-Store)합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-110">If you wish to explore the ASP.NET MVC 3 version of the tutorial application, you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<span data-ttu-id="405d3-111">이 실습에서는 개발자 HTML 및 JavaScript와 같은 웹 개발 기술을 환경에 있는지 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-111">This Hands-On Lab assumes that the developer has experience in Web development technologies, such as HTML and JavaScript.</span></span>

> [!NOTE]
> <span data-ttu-id="405d3-112">웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 됩니다 [Microsoft-웹/WebCampTrainingKit 릴리스](https://aka.ms/webcamps-training-kit)합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-112">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="405d3-113">이 랩에 특정 프로젝트에서 제공 됩니다 [ASP.NET MVC 4 기본 사항](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals)합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-113">The project specific to this lab is available at [ASP.NET MVC 4 Fundamentals](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals).</span></span>

<a id="The_Music_Store_application"></a>
### <a name="the-music-store-application"></a><span data-ttu-id="405d3-114">Music Store 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="405d3-114">The Music Store application</span></span>

<span data-ttu-id="405d3-115">이 랩에서 전체에서 빌드되는 Music Store 웹 응용 프로그램 구성 세 가지 주요 부분이: 쇼핑, 체크 아웃 및 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-115">The Music Store web application that will be built throughout this Lab comprises three main parts: shopping, checkout, and administration.</span></span> <span data-ttu-id="405d3-116">방문자 장르별로 앨범을 찾아보기, 앨범 자신의 카트에 추가 하 고, 선택 검토 하 고 마지막으로 로그인 하 고 순서를 완료 하는 결제로 진행 하는 일을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-116">Visitors will be able to browse albums by genre, add albums to their cart, review their selection and finally proceed to checkout to login and complete the order.</span></span> <span data-ttu-id="405d3-117">또한 저장소 관리자 주요 속성 뿐만 아니라 사용 가능한 앨범을 관리할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-117">Additionally, store administrators will be able to manage the available albums as well as their main properties.</span></span>

<span data-ttu-id="405d3-118">![Music Store 화면](aspnet-mvc-4-fundamentals/_static/image1.png "Music Store 화면")</span><span class="sxs-lookup"><span data-stu-id="405d3-118">![Music Store screens](aspnet-mvc-4-fundamentals/_static/image1.png "Music Store screens")</span></span>

<span data-ttu-id="405d3-119">*Music Store 화면*</span><span class="sxs-lookup"><span data-stu-id="405d3-119">*Music Store screens*</span></span>

<a id="ASPNET_MVC_4_Essentials"></a>
### <a name="aspnet-mvc-4-essentials"></a><span data-ttu-id="405d3-120">ASP.NET MVC 4 Essentials</span><span class="sxs-lookup"><span data-stu-id="405d3-120">ASP.NET MVC 4 Essentials</span></span>

<span data-ttu-id="405d3-121">Music Store 응용 프로그램이 사용 하 여 빌드됩니다 **컨트롤러 MVC (Model View)**, 응용 프로그램을 세 가지 주요 구성 요소를 구분 하는 아키텍처 패턴:</span><span class="sxs-lookup"><span data-stu-id="405d3-121">Music Store application will be built using **Model View Controller (MVC)**, an architectural pattern that separates an application into three main components:</span></span>

- <span data-ttu-id="405d3-122">**모델**: 모델 개체는 도메인 논리를 구현 하는 응용 프로그램의 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-122">**Models**: Model objects are the parts of the application that implement the domain logic.</span></span> <span data-ttu-id="405d3-123">종종 모델 개체도 검색 및 데이터베이스에서 모델 상태를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-123">Often, model objects also retrieve and store model state in a database.</span></span>
- <span data-ttu-id="405d3-124">**보기:** 뷰는 응용 프로그램의 UI (사용자 인터페이스)를 표시 하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-124">**Views:** Views are the components that display the application's user interface (UI).</span></span> <span data-ttu-id="405d3-125">일반적으로이 UI는 모델 데이터에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-125">Typically, this UI is created from the model data.</span></span> <span data-ttu-id="405d3-126">예로 앨범 개체의 현재 상태에 따라 드롭다운 목록과 텍스트 상자를 표시 하는 앨범의 편집 보기 것입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-126">An example would be the edit view of Albums that displays text boxes and a drop-down list based on the current state of an Album object.</span></span>
- <span data-ttu-id="405d3-127">**컨트롤러:** 컨트롤러는, 사용자 상호 작용을 처리 하 고, 모델을 조작 하 고, 궁극적으로 UI를 렌더링 하는 뷰를 선택 하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-127">**Controllers:** Controllers are the components that handle user interaction, manipulate the model, and ultimately select a view to render the UI.</span></span> <span data-ttu-id="405d3-128">MVC 응용 프로그램에서 보기는 정보만 표시합니다. 컨트롤러가 사용자 입력 및 상호 작용을 처리하고 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-128">In an MVC application, the view only displays information; the controller handles and responds to user input and interaction.</span></span>

<span data-ttu-id="405d3-129">MVC 패턴을 사용 하면 이러한 요소 간의 느슨한 결합을 제공 하는 동안 응용 프로그램 (입력된 논리, 비즈니스 논리 및 UI 논리)의 다양 한 측면을 구분 하는 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-129">The MVC pattern helps you to create applications that separate the different aspects of the application (input logic, business logic, and UI logic), while providing a loose coupling between these elements.</span></span> <span data-ttu-id="405d3-130">이러한 분리를 통해 한 번에 구현의 하나의 측면에 초점을 맞출 수 있도록 응용 프로그램을 빌드할 때 복잡성을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-130">This separation helps you manage complexity when you build an application, as it allows you to focus on one aspect of the implementation at a time.</span></span> <span data-ttu-id="405d3-131">또한 MVC 패턴에서는 또한 응용 프로그램을 만들기 위한 테스트 기반 개발 (TDD)을 사용 하도록 권장 하는 응용 프로그램을 테스트 하기가 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-131">In addition, the MVC pattern makes it easy to test applications, also encouraging the use of test-driven development (TDD) for creating applications.</span></span>

<span data-ttu-id="405d3-132">합니다 **ASP.NET MVC** 프레임 워크는 ASP.NET MVC 기반 웹 응용 프로그램을 만들기 위한 ASP.NET Web Forms 패턴에 대안을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-132">The **ASP.NET MVC** framework provides an alternative to the ASP.NET Web Forms pattern for creating ASP.NET MVC-based Web applications.</span></span> <span data-ttu-id="405d3-133">합니다 **ASP.NET MVC** 프레임 워크는 간단 하 고 가볍고 테스트가 용이한 프레젠테이션 프레임 워크는 (Web forms 기반 응용 프로그램과 마찬가지로)은 같은 마스터 페이지 및 멤버 자격 기반 기존 ASP.NET 기능과 통합 .NET core framework의 모든 기능을 얻게 되므로 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-133">The **ASP.NET MVC** framework is a lightweight, highly testable presentation framework that (as with Web-forms-based applications) is integrated with existing ASP.NET features, such as master pages and membership-based authentication so you get all the power of the core .NET framework.</span></span> <span data-ttu-id="405d3-134">이 이미 잘 알고 있다면 ASP.NET Web Forms를 사용 하 여 이미 사용 하는 모든 라이브러리도 ASP.NET MVC 4에서 사용할 수 있으므로 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-134">This is useful if you are already familiar with ASP.NET Web Forms because all the libraries that you already use are available in ASP.NET MVC 4 as well.</span></span>

<span data-ttu-id="405d3-135">또한 MVC 응용 프로그램의 세 가지 주요 구성 요소 간의 느슨한 결합은 병렬 개발을 촉진 하는 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-135">In addition, the loose coupling between the three main components of an MVC application also promotes parallel development.</span></span> <span data-ttu-id="405d3-136">예를 들어 한 개발자 보기에서 작업할 수 있습니다, 두 번째 개발자는 컨트롤러 논리를 작업할 수 있습니다 및 세 번째 개발자는 모델의 비즈니스 논리에 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-136">For instance, one developer can work on the view, a second developer can work on the controller logic, and a third developer can focus on the business logic in the model.</span></span>

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="405d3-137">목표</span><span class="sxs-lookup"><span data-stu-id="405d3-137">Objectives</span></span>

<span data-ttu-id="405d3-138">이 실습 랩에서 학습할 방법:</span><span class="sxs-lookup"><span data-stu-id="405d3-138">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="405d3-139">Music Store 응용 프로그램 자습서를 기반으로 하는 처음부터 ASP.NET MVC 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="405d3-139">Create an ASP.NET MVC application from scratch based on the Music Store Application tutorial</span></span>
- <span data-ttu-id="405d3-140">사이트 및 해당 주요 기능을 검색 하는 것에 대 한 홈 페이지 Url을 처리 하는 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="405d3-140">Add Controllers to handle URLs to the Home page of the site and for browsing its main functionality</span></span>
- <span data-ttu-id="405d3-141">해당 스타일과 함께 표시 되는 내용에 맞게 뷰 추가</span><span class="sxs-lookup"><span data-stu-id="405d3-141">Add a View to customize the content displayed along with its style</span></span>
- <span data-ttu-id="405d3-142">포함 하 고 데이터 및 도메인 논리를 관리할 모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="405d3-142">Add Model classes to contain and manage data and domain logic</span></span>
- <span data-ttu-id="405d3-143">뷰 모델 패턴을 사용 하 여 보기 템플릿은 컨트롤러 작업에서 정보를 전달</span><span class="sxs-lookup"><span data-stu-id="405d3-143">Use View Model pattern to pass information from controller actions to the view templates</span></span>
- <span data-ttu-id="405d3-144">인터넷 응용 프로그램에 대 한 ASP.NET MVC 4 새 템플릿 탐색</span><span class="sxs-lookup"><span data-stu-id="405d3-144">Explore the ASP.NET MVC 4 new template for internet applications</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="405d3-145">전제 조건</span><span class="sxs-lookup"><span data-stu-id="405d3-145">Prerequisites</span></span>

<span data-ttu-id="405d3-146">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-146">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="405d3-147">[Visual Studio 2012 Express for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (읽을 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은)</span><span class="sxs-lookup"><span data-stu-id="405d3-147">[Visual Studio 2012 Express for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (read [Appendix A](#AppendixA) for instructions on how to install it)</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="405d3-148">설정</span><span class="sxs-lookup"><span data-stu-id="405d3-148">Setup</span></span>

<span data-ttu-id="405d3-149">**설치 코드 조각**</span><span class="sxs-lookup"><span data-stu-id="405d3-149">**Installing Code Snippets**</span></span>

<span data-ttu-id="405d3-150">편의 위해이 랩에서 함께 관리 하려는 코드의 대부분 제품은 Visual Studio 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-150">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="405d3-151">설치를 실행 하는 코드 조각 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-151">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="405d3-152">이 문서의 부록 참조할 수 있습니다 사용 하는 방법을 알아보려면 원하는 고 Visual Studio 코드 조각을 사용 하 여 잘 모르는 경우 &quot; [부록 c:를 사용 하 여 코드 조각](#AppendixC)&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-152">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="405d3-153">연습</span><span class="sxs-lookup"><span data-stu-id="405d3-153">Exercises</span></span>

<span data-ttu-id="405d3-154">이 실습 랩에서 다음 연습으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-154">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="405d3-155">연습 1: MusicStore ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="405d3-155">Exercise 1: Creating MusicStore ASP.NET MVC Web Application Project</span></span>](#Exercise1)
2. [<span data-ttu-id="405d3-156">연습 2: 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="405d3-156">Exercise 2: Creating a Controller</span></span>](#Exercise2)
3. [<span data-ttu-id="405d3-157">연습 3: 컨트롤러에 매개 변수 전달</span><span class="sxs-lookup"><span data-stu-id="405d3-157">Exercise 3: Passing parameters to a Controller</span></span>](#Exercise3)
4. [<span data-ttu-id="405d3-158">실습 4: 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="405d3-158">Exercise 4: Creating a View</span></span>](#Exercise4)
5. [<span data-ttu-id="405d3-159">실습 5: 뷰 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="405d3-159">Exercise 5: Creating a View Model</span></span>](#Exercise5)
6. [<span data-ttu-id="405d3-160">실습 6:를 사용 하 여 매개 변수 보기</span><span class="sxs-lookup"><span data-stu-id="405d3-160">Exercise 6: Using parameters in View</span></span>](#Exercise6)
7. [<span data-ttu-id="405d3-161">실습 7: ASP.NET MVC 4에 대 한 새 템플릿 주위의 랩</span><span class="sxs-lookup"><span data-stu-id="405d3-161">Exercise 7: A lap around ASP.NET MVC 4 New Template</span></span>](#Exercise7)

> [!NOTE]
> <span data-ttu-id="405d3-162">각 실습 동반 되는 **최종** 연습을 완료 한 후 가져와야 결과 솔루션이 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-162">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="405d3-163">이 연습을 진행 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-163">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="405d3-164">이 랩을 완료 하기 위한 예상 시간: **60 분**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-164">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_MusicStore_ASPNET_MVC_Web_Application_Project"></a>
### <a name="exercise-1-creating-musicstore-aspnet-mvc-web-application-project"></a><span data-ttu-id="405d3-165">연습 1: MusicStore ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="405d3-165">Exercise 1: Creating MusicStore ASP.NET MVC Web Application Project</span></span>

<span data-ttu-id="405d3-166">이 연습에서는 해당 기본 폴더 조직 뿐만 아니라 웹에 대 한 Visual Studio 2012 Express에서 ASP.NET MVC 응용 프로그램을 만드는 방법에 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-166">In this exercise, you will learn how to create an ASP.NET MVC application in Visual Studio 2012 Express for Web as well as its main folder organization.</span></span> <span data-ttu-id="405d3-167">또한 새 컨트롤러를 추가 하 고 간단한 문자열을 응용 프로그램의 홈 페이지에 표시할 수 있도록 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-167">Additionally, you will learn how to add a new Controller and make it display a simple string in the application's home page.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_ASPNET_MVC_Web_Application_Project"></a>
#### <a name="task-1---creating-the-aspnet-mvc-web-application-project"></a><span data-ttu-id="405d3-168">작업 1-ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="405d3-168">Task 1 - Creating the ASP.NET MVC Web Application Project</span></span>

1. <span data-ttu-id="405d3-169">이 태스크에서는 MVC Visual Studio 템플릿을 사용 하 여 빈 ASP.NET MVC 응용 프로그램 프로젝트를 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-169">In this task, you will create an empty ASP.NET MVC application project using the MVC Visual Studio template.</span></span> <span data-ttu-id="405d3-170">시작 **VS Express for Web**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-170">Start **VS Express for Web**.</span></span>
2. <span data-ttu-id="405d3-171">**파일** 메뉴에서 **새 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-171">On the **File** menu, click **New Project**.</span></span>
3. <span data-ttu-id="405d3-172">에 **새 프로젝트** 대화 상자 선택 합니다 **ASP.NET MVC 4 웹 응용 프로그램** 프로젝트 아래에 있는 형식을 **Visual C#** **웹** 템플릿 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-172">In the **New Project** dialog box select the **ASP.NET MVC 4 Web Application** project type, located under **Visual C#,** **Web** template list.</span></span>
4. <span data-ttu-id="405d3-173">변경 된 **이름을** 하 *MvcMusicStore*합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-173">Change the **Name** to *MvcMusicStore*.</span></span>
5. <span data-ttu-id="405d3-174">새 내부 솔루션의 위치를 설정 **시작할** 예를 들어가 연습이에서는 원본 폴더의 폴더 **[YOUR HOL 경로] \Source\Ex01-CreatingMusicStoreProject\Begin**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-174">Set the location of the solution inside a new **Begin** folder in this Exercise's Source folder, for example **[YOUR-HOL-PATH]\Source\Ex01-CreatingMusicStoreProject\Begin**.</span></span> <span data-ttu-id="405d3-175">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-175">Click **OK**.</span></span>

    <span data-ttu-id="405d3-176">![새 프로젝트 대화 상자를 만듭니다](aspnet-mvc-4-fundamentals/_static/image2.png "새 프로젝트 대화 상자 만들기")</span><span class="sxs-lookup"><span data-stu-id="405d3-176">![Create New Project Dialog Box](aspnet-mvc-4-fundamentals/_static/image2.png "Create New Project Dialog Box")</span></span>

    <span data-ttu-id="405d3-177">*새 프로젝트 대화 상자 만들기*</span><span class="sxs-lookup"><span data-stu-id="405d3-177">*Create New Project Dialog Box*</span></span>
6. <span data-ttu-id="405d3-178">에 **새 ASP.NET MVC 4 프로젝트** 대화 상자 선택을 **기본** 템플릿 되어 있는지 확인 합니다 **뷰 엔진** 선택한 **Razor**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-178">In the **New ASP.NET MVC 4 Project** dialog box select the **Basic** template and make sure that the **View engine** selected is **Razor**.</span></span> <span data-ttu-id="405d3-179">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-179">Click **OK**.</span></span>

    <span data-ttu-id="405d3-180">![새 ASP.NET MVC 4 프로젝트 대화 상자](aspnet-mvc-4-fundamentals/_static/image3.png "새 ASP.NET MVC 4 프로젝트 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="405d3-180">![New ASP.NET MVC 4 Project Dialog Box](aspnet-mvc-4-fundamentals/_static/image3.png "New ASP.NET MVC 4 Project Dialog Box")</span></span>

    <span data-ttu-id="405d3-181">*새 ASP.NET MVC 4 프로젝트 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="405d3-181">*New ASP.NET MVC 4 Project Dialog Box*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Exploring_the_Solution_Structure"></a>
#### <a name="task-2---exploring-the-solution-structure"></a><span data-ttu-id="405d3-182">작업 2-솔루션 구조를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-182">Task 2 - Exploring the Solution Structure</span></span>

<span data-ttu-id="405d3-183">ASP.NET MVC 프레임 워크는 MVC 패턴을 지 원하는 웹 응용 프로그램을 만들 수 있도록 Visual Studio 프로젝트 템플릿이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-183">The ASP.NET MVC framework includes a Visual Studio project template that helps you create Web applications supporting the MVC pattern.</span></span> <span data-ttu-id="405d3-184">이 템플릿은 필요한 폴더, 항목 템플릿 및 구성 파일 항목을 사용 하 여 새 ASP.NET MVC 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-184">This template creates a new ASP.NET MVC Web application with the required folders, item templates, and configuration-file entries.</span></span>

<span data-ttu-id="405d3-185">이 작업에서는 관련 된 요소를 이해 하는 솔루션 구조 및 해당 관계를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-185">In this task, you will examine the solution structure to understand the elements that are involved and their relationships.</span></span> <span data-ttu-id="405d3-186">기본적으로 ASP.NET MVC 프레임 워크를 사용 하기 때문에 모든 ASP.NET MVC 응용 프로그램에 다음 폴더가 포함 된 &quot;구성 보다 규칙&quot; 방식과 몇 가지 기본 가정이 폴더 이름에 따라 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-186">The following folders are included in all the ASP.NET MVC application because the ASP.NET MVC framework by default uses a &quot;convention over configuration&quot; approach, and makes some default assumptions based on folder naming conventions.</span></span>

1. <span data-ttu-id="405d3-187">프로젝트가 생성 되 면 오른쪽에 있는 솔루션 탐색기에서 만든 폴더 구조를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-187">Once the project is created, review the folder structure that has been created in the Solution Explorer on the right side:</span></span>

    <span data-ttu-id="405d3-188">![솔루션 탐색기에서 ASP.NET MVC 폴더 구조](aspnet-mvc-4-fundamentals/_static/image4.png "솔루션 탐색기에서 ASP.NET MVC 폴더 구조")</span><span class="sxs-lookup"><span data-stu-id="405d3-188">![ASP.NET MVC Folder structure in Solution Explorer](aspnet-mvc-4-fundamentals/_static/image4.png "ASP.NET MVC Folder structure in Solution Explorer")</span></span>

    <span data-ttu-id="405d3-189">*솔루션 탐색기에서 ASP.NET MVC 폴더 구조*</span><span class="sxs-lookup"><span data-stu-id="405d3-189">*ASP.NET MVC Folder structure in Solution Explorer*</span></span>

   1. <span data-ttu-id="405d3-190">**컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-190">**Controllers**.</span></span> <span data-ttu-id="405d3-191">이 폴더는 컨트롤러 클래스가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-191">This folder will contain the controller classes.</span></span> <span data-ttu-id="405d3-192">MVC 기반 응용 프로그램에서 컨트롤러는 최종 사용자 상호 작용을 처리 하 고 모델을 조작 하 고 궁극적으로 UI를 렌더링 하는 뷰를 선택 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-192">In an MVC based application, controllers are responsible for handling end user interaction, manipulating the model, and ultimately choosing a view to render the UI.</span></span>

       > [!NOTE]
       > <span data-ttu-id="405d3-193">MVC 프레임 워크를 위해서는 끝나야 모든 컨트롤러의 이름이 &quot;컨트롤러&quot;-HomeController, LoginController 또는 ProductController 예를 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-193">The MVC framework requires the names of all controllers to end with &quot;Controller&quot;-for example, HomeController, LoginController, or ProductController.</span></span>
   2. <span data-ttu-id="405d3-194">**모델**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-194">**Models**.</span></span> <span data-ttu-id="405d3-195">이 폴더는 MVC 웹 응용 프로그램에 대 한 응용 프로그램 모델을 나타내는 클래스에 대 한 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-195">This folder is provided for classes that represent the application model for the MVC Web application.</span></span> <span data-ttu-id="405d3-196">일반적으로 개체 및 데이터 저장소와 상호 작용 하기 위한 논리를 정의 하는 코드가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-196">This usually includes code that defines objects and the logic for interacting with the data store.</span></span> <span data-ttu-id="405d3-197">일반적으로 실제 모델 개체는 별도 클래스 라이브러리에 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-197">Typically, the actual model objects will be in separate class libraries.</span></span> <span data-ttu-id="405d3-198">그러나 새 응용 프로그램을 만들면 클래스를 포함 하 고 개발 주기에서 나중에 별도 클래스 라이브러리로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-198">However, when you create a new application, you might include classes and then move them into separate class libraries at a later point in the development cycle.</span></span>
   3. <span data-ttu-id="405d3-199">**뷰**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-199">**Views**.</span></span> <span data-ttu-id="405d3-200">이 폴더에 보기를 응용 프로그램의 사용자 인터페이스를 표시 하는 일을 담당 하는 구성 요소에 대 한 권장 되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-200">This folder is the recommended location for views, the components responsible for displaying the application's user interface.</span></span> <span data-ttu-id="405d3-201">보기는.aspx,.ascx,.cshtml 및.master 파일 뷰 렌더링에 관련 된 다른 파일 외에도 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-201">Views use .aspx, .ascx, .cshtml and .master files, in addition to any other files that are related to rendering views.</span></span> <span data-ttu-id="405d3-202">각 컨트롤러에 대 한 폴더를 포함 하는 views 폴더 컨트롤러 이름 접두사를 사용 하 여 폴더의 이름은입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-202">Views folder contains a folder for each controller; the folder is named with the controller-name prefix.</span></span> <span data-ttu-id="405d3-203">예를 들어 라는 컨트롤러를 있다면 **HomeController**, Views 폴더에 Home 이라는 폴더가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-203">For example, if you have a controller named **HomeController**, the Views folder will contain a folder named Home.</span></span> <span data-ttu-id="405d3-204">기본적으로 ASP.NET MVC 프레임 워크에서는 뷰를 찾습니다 Views\controllerName 폴더에서 요청 된 뷰 이름 사용 하 여.aspx 파일 (**[ControllerName] [작업] 보기.aspx**) 또는 (**뷰 [ControllerName] [작업].cshtml**) Razor 보기에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-204">By default, when the ASP.NET MVC framework loads a view, it looks for an .aspx file with the requested view name in the Views\controllerName folder (**Views[ControllerName][Action].aspx**) or (**Views[ControllerName][Action].cshtml**) for Razor Views.</span></span>

      > [!NOTE]
      > <span data-ttu-id="405d3-205">MVC 웹 응용 프로그램을 사용 하 여 앞에서 설명한 폴더 외에도 합니다 **Global.asax** 전역 URL 라우팅 설정 하기 위해 파일의 기본값을 사용 하는 **Web.config** 응용 프로그램을 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-205">In addition to the folders listed previously, an MVC Web application uses the **Global.asax** file to set global URL routing defaults, and it uses the **Web.config** file to configure the application.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Adding_a_HomeController"></a>
#### <a name="task-3---adding-a-homecontroller"></a><span data-ttu-id="405d3-206">작업 3-HomeController를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-206">Task 3 - Adding a HomeController</span></span>

<span data-ttu-id="405d3-207">MVC 프레임 워크를 사용 하지 않는 ASP.NET 응용 프로그램에서 사용자 상호 작용이 발생 시키고 해당 페이지에서 이벤트를 처리 하 고 페이지를 중심으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-207">In ASP.NET applications that do not use the MVC framework, user interaction is organized around pages, and around raising and handling events from those pages.</span></span> <span data-ttu-id="405d3-208">반면, ASP.NET MVC 응용 프로그램을 사용 하 여 사용자 상호 작용은 컨트롤러 및 해당 작업 메서드 중심으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-208">In contrast, user interaction with ASP.NET MVC applications is organized around controllers and their action methods.</span></span>

<span data-ttu-id="405d3-209">반면에 ASP.NET MVC 프레임 워크는 컨트롤러 라고 하는 클래스에 Url을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-209">On the other hand, ASP.NET MVC framework maps URLs to classes that are referred to as controllers.</span></span> <span data-ttu-id="405d3-210">컨트롤러 들어오는 요청을 처리, 사용자 입력 및 상호 작용을 처리, 적절 한 응용 프로그램 논리를 실행 및 클라이언트에 다시 전송할 응답 결정 (HTML을 표시, 파일을 다운로드, 등 다른 URL 리디렉션).</span><span class="sxs-lookup"><span data-stu-id="405d3-210">Controllers process incoming requests, handle user input and interactions, execute appropriate application logic and determine the response to send back to the client (display HTML, download a file, redirect to a different URL, etc.).</span></span> <span data-ttu-id="405d3-211">HTML을 표시 하는 경우 컨트롤러 클래스는 일반적으로 요청에 대 한 HTML 태그를 생성 하는 별도 뷰 구성 요소를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-211">In the case of displaying HTML, a controller class typically calls a separate view component to generate the HTML markup for the request.</span></span> <span data-ttu-id="405d3-212">MVC 응용 프로그램에서 보기는 정보만 표시합니다. 컨트롤러가 사용자 입력 및 상호 작용을 처리하고 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-212">In an MVC application, the view only displays information; the controller handles and responds to user input and interaction.</span></span>

<span data-ttu-id="405d3-213">이 태스크에서는 Music Store 사이트의 홈 페이지 Url을 처리 하는 컨트롤러 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-213">In this task, you will add a Controller class that will handle URLs to the Home page of the Music Store site.</span></span>

1. <span data-ttu-id="405d3-214">마우스 오른쪽 단추로 클릭 **컨트롤러** 솔루션 탐색기에서 선택 내에서 폴더 **추가** 차례로 **컨트롤러** 명령:</span><span class="sxs-lookup"><span data-stu-id="405d3-214">Right-click **Controllers** folder within the Solution Explorer, select **Add** and then **Controller** command:</span></span>

    <span data-ttu-id="405d3-215">![컨트롤러는 명령을 추가](aspnet-mvc-4-fundamentals/_static/image5.png "컨트롤러 명령 추가")</span><span class="sxs-lookup"><span data-stu-id="405d3-215">![Add a Controller Command](aspnet-mvc-4-fundamentals/_static/image5.png "Add a Controller Command")</span></span>

    <span data-ttu-id="405d3-216">*컨트롤러 명령 추가*</span><span class="sxs-lookup"><span data-stu-id="405d3-216">*Add Controller Command*</span></span>
2. <span data-ttu-id="405d3-217">합니다 **컨트롤러 추가** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-217">The **Add Controller** dialog appears.</span></span> <span data-ttu-id="405d3-218">컨트롤러 이름을 *HomeController* 누릅니다 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-218">Name the controller *HomeController* and press **Add**.</span></span>

    <span data-ttu-id="405d3-219">![컨트롤러 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image6.png "컨트롤러 추가 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="405d3-219">![Add Controller Dialog](aspnet-mvc-4-fundamentals/_static/image6.png "Add Controller Dialog")</span></span>

    <span data-ttu-id="405d3-220">*컨트롤러 추가 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="405d3-220">*Add Controller Dialog*</span></span>
3. <span data-ttu-id="405d3-221">파일 **HomeController.cs** 만들어집니다 합니다 **컨트롤러** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-221">The file **HomeController.cs** is created in the **Controllers** folder.</span></span> <span data-ttu-id="405d3-222">위해서는 합니다 **HomeController** 대체, 해당 인덱스 작업에서 문자열을 반환 합니다 **인덱스** 메서드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="405d3-222">In order to have the **HomeController** return a string on its Index action, replace the **Index** method with the following code:</span></span>

    <span data-ttu-id="405d3-223">(코드 조각- *ASP.NET MVC 4 기본 사항-e x 1 HomeController 인덱스*)</span><span class="sxs-lookup"><span data-stu-id="405d3-223">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex1 HomeController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample1.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="405d3-224">작업 4-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="405d3-224">Task 4 - Running the Application</span></span>

<span data-ttu-id="405d3-225">이 작업에서는 웹 브라우저에서 응용 프로그램을 사용해 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-225">In this task, you will try out the Application in a web browser.</span></span>

1. <span data-ttu-id="405d3-226">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-226">Press **F5** to run the Application.</span></span> <span data-ttu-id="405d3-227">프로젝트를 컴파일할 하 고 로컬 IIS 웹 서버 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-227">The project is compiled and the local IIS Web Server starts.</span></span> <span data-ttu-id="405d3-228">로컬 IIS 웹 서버는 웹 서버의 URL을 가리키는 웹 브라우저를 열고 자동으로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-228">The local IIS Web Server will automatically open a web browser pointing to the URL of the Web server.</span></span>

    <span data-ttu-id="405d3-229">![웹 브라우저에서 실행 중인 응용 프로그램](aspnet-mvc-4-fundamentals/_static/image7.png "웹 브라우저에서 실행 중인 응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="405d3-229">![Application running in a web browser](aspnet-mvc-4-fundamentals/_static/image7.png "Application running in a web browser")</span></span>

    <span data-ttu-id="405d3-230">*웹 브라우저에서 실행 중인 응용 프로그램*</span><span class="sxs-lookup"><span data-stu-id="405d3-230">*Application running in a web browser*</span></span>

    > [!NOTE]
    > <span data-ttu-id="405d3-231">로컬 IIS 웹 서버에 임의 가능한 포트 번호를 웹 사이트를 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-231">The local IIS Web Server will run the website on a random free port number.</span></span> <span data-ttu-id="405d3-232">위의 그림에서는 사이트에서 실행 중인 `http://localhost:50103/`이므로 50103 포트를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-232">In the figure above, the site is running at `http://localhost:50103/`, so it's using port 50103.</span></span> <span data-ttu-id="405d3-233">포트 번호로 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-233">Your port number may vary.</span></span>
2. <span data-ttu-id="405d3-234">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-234">Close the browser.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Controller"></a>
### <a name="exercise-2-creating-a-controller"></a><span data-ttu-id="405d3-235">연습 2: 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="405d3-235">Exercise 2: Creating a Controller</span></span>

<span data-ttu-id="405d3-236">이 연습에서는 Music Store 응용 프로그램의 간단한 기능을 구현 하는 컨트롤러를 업데이트 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-236">In this exercise, you will learn how to update the controller to implement simple functionality of the Music Store application.</span></span> <span data-ttu-id="405d3-237">해당 컨트롤러의 각 다음 특정 요청을 처리할 작업 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-237">That controller will define action methods to handle each of the following specific requests:</span></span>

- <span data-ttu-id="405d3-238">Music Store에서 음악 장르 목록 페이지</span><span class="sxs-lookup"><span data-stu-id="405d3-238">A listing page of the music genres in the Music Store</span></span>
- <span data-ttu-id="405d3-239">특정 장르에 대 한 음악 앨범의 모든를 나열 하는 찾아보기 페이지</span><span class="sxs-lookup"><span data-stu-id="405d3-239">A browse page that lists all of the music albums for a particular genre</span></span>
- <span data-ttu-id="405d3-240">특정 음악 앨범에 대 한 정보를 보여 주는 세부 정보 페이지</span><span class="sxs-lookup"><span data-stu-id="405d3-240">A details page that shows information about a specific music album</span></span>

<span data-ttu-id="405d3-241">이 연습의 범위에 단순히 해당 작업을 이제 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-241">For the scope of this exercise, those actions will simply return a string by now.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Adding_a_New_StoreController_Class"></a>
#### <a name="task-1---adding-a-new-storecontroller-class"></a><span data-ttu-id="405d3-242">작업 1-새 StoreController 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="405d3-242">Task 1 - Adding a New StoreController Class</span></span>

<span data-ttu-id="405d3-243">이 태스크에서는 새 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-243">In this task, you will add a new Controller.</span></span>

1. <span data-ttu-id="405d3-244">아직 열지 않은 경우 시작 **VS Express for Web 2012**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-244">If not already open, start **VS Express for Web 2012**.</span></span>
2. <span data-ttu-id="405d3-245">에 **파일** 메뉴 선택 **프로젝트 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-245">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="405d3-246">이동할 프로젝트 열기 대화 상자에서 **Source\Ex02 CreatingAController\Begin**를 선택 **Begin.sln** 클릭 **열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-246">In the Open Project dialog, browse to **Source\Ex02-CreatingAController\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="405d3-247">또는 계속 진행할 솔루션 이전 연습을 완료 한 후 가져온 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-247">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="405d3-248">제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-248">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="405d3-249">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-249">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="405d3-250">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="405d3-250">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="405d3-251">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-251">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="405d3-252">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-252">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="405d3-253">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-253">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="405d3-254">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-254">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="405d3-255">새 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-255">Add the new controller.</span></span> <span data-ttu-id="405d3-256">이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **컨트롤러** 선택 솔루션 탐색기 내에서 폴더 **추가** 차례로 **컨트롤러** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-256">To do this, right-click the **Controllers** folder within the Solution Explorer, select **Add** and then the **Controller** command.</span></span> <span data-ttu-id="405d3-257">변경 된 **컨트롤러 이름** 에 *StoreController*, 클릭 **추가**.</span><span class="sxs-lookup"><span data-stu-id="405d3-257">Change the **Controller Name** to *StoreController*, and click **Add**.</span></span>

    <span data-ttu-id="405d3-258">![컨트롤러 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image8.png "컨트롤러 추가 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="405d3-258">![Add Controller Dialog](aspnet-mvc-4-fundamentals/_static/image8.png "Add Controller Dialog")</span></span>

    <span data-ttu-id="405d3-259">*컨트롤러 추가 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="405d3-259">*Add Controller Dialog*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Modifying_the_StoreControllers_Actions"></a>
#### <a name="task-2---modifying-the-storecontrollers-actions"></a><span data-ttu-id="405d3-260">작업 2-StoreController의 동작을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-260">Task 2 - Modifying the StoreController's Actions</span></span>

<span data-ttu-id="405d3-261">이 태스크에서는 호출 되는 컨트롤러 메서드를 수정 합니다 **작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-261">In this task, you will modify the Controller methods that are called **actions**.</span></span> <span data-ttu-id="405d3-262">작업은 URL 요청을 처리 하 고 브라우저 또는 URL을 호출 하는 사용자에 게 다시 보내야 하는 콘텐츠를 확인 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-262">Actions are responsible for handling URL requests and determining the content that should be sent back to the browser or user that invoked the URL.</span></span>

1. <span data-ttu-id="405d3-263">합니다 **StoreController** 클래스에 이미 있는 **인덱스** 메서드.</span><span class="sxs-lookup"><span data-stu-id="405d3-263">The **StoreController** class already has an **Index** method.</span></span> <span data-ttu-id="405d3-264">Music store의 모든 장르를 나열 하는 페이지를 구현 하려면이 랩에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-264">You will use it later in this Lab to implement the page that lists all genres of the music store.</span></span> <span data-ttu-id="405d3-265">지금은 바꾸기만 합니다 **인덱스** 메서드를 문자열로 반환 하는 다음 코드로 &quot;Hello Store.Index() from에서&quot;:</span><span class="sxs-lookup"><span data-stu-id="405d3-265">For now, just replace the **Index** method with the following code that returns a string &quot;Hello from Store.Index()&quot;:</span></span>

    <span data-ttu-id="405d3-266">(코드 조각- *ASP.NET MVC 4 기본 사항-e x 2 StoreController 인덱스*)</span><span class="sxs-lookup"><span data-stu-id="405d3-266">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex2 StoreController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample2.cs)]
2. <span data-ttu-id="405d3-267">추가 **찾아보기** 하 고 **세부 정보** 메서드.</span><span class="sxs-lookup"><span data-stu-id="405d3-267">Add **Browse** and **Details** methods.</span></span> <span data-ttu-id="405d3-268">이렇게 하려면 다음 코드를 추가 합니다 **StoreController**:</span><span class="sxs-lookup"><span data-stu-id="405d3-268">To do this, add the following code to the **StoreController**:</span></span>

    <span data-ttu-id="405d3-269">(코드 조각- *ASP.NET MVC 4 기본 사항-e x 2 StoreController BrowseAndDetails*)</span><span class="sxs-lookup"><span data-stu-id="405d3-269">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex2 StoreController BrowseAndDetails*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample3.cs)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="405d3-270">작업 3-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="405d3-270">Task 3 - Running the Application</span></span>

<span data-ttu-id="405d3-271">이 작업에서는 웹 브라우저에서 응용 프로그램을 사용해 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-271">In this task, you will try out the Application in a web browser.</span></span>

1. <span data-ttu-id="405d3-272">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-272">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="405d3-273">프로젝트에서 시작 합니다 **홈** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-273">The project starts in the **Home** page.</span></span> <span data-ttu-id="405d3-274">각 작업의 구현을 확인 하도록 URL을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-274">Change the URL to verify each action's implementation.</span></span>

    1. <span data-ttu-id="405d3-275">**/ 저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-275">**/Store**.</span></span> <span data-ttu-id="405d3-276">나타납니다  **&quot;Store.Index()에서 Hello&quot;** 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-276">You will see **&quot;Hello from Store.Index()&quot;**.</span></span>
    2. <span data-ttu-id="405d3-277">**/ 저장소/찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-277">**/Store/Browse**.</span></span> <span data-ttu-id="405d3-278">나타납니다  **&quot;Store.Browse()에서 Hello&quot;** 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-278">You will see **&quot;Hello from Store.Browse()&quot;**.</span></span>
    3. <span data-ttu-id="405d3-279">**/ 저장소/세부 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-279">**/Store/Details**.</span></span> <span data-ttu-id="405d3-280">나타납니다  **&quot;Store.Details()에서 Hello&quot;** 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-280">You will see **&quot;Hello from Store.Details()&quot;**.</span></span>

        <span data-ttu-id="405d3-281">![검색 StoreBrowse](aspnet-mvc-4-fundamentals/_static/image9.png "StoreBrowse 검색")</span><span class="sxs-lookup"><span data-stu-id="405d3-281">![Browsing StoreBrowse](aspnet-mvc-4-fundamentals/_static/image9.png "Browsing StoreBrowse")</span></span>

        <span data-ttu-id="405d3-282">*검색 /Store/Browse*</span><span class="sxs-lookup"><span data-stu-id="405d3-282">*Browsing /Store/Browse*</span></span>
3. <span data-ttu-id="405d3-283">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-283">Close the browser.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Passing_parameters_to_a_Controller"></a>
### <a name="exercise-3-passing-parameters-to-a-controller"></a><span data-ttu-id="405d3-284">연습 3: 컨트롤러에 매개 변수 전달</span><span class="sxs-lookup"><span data-stu-id="405d3-284">Exercise 3: Passing parameters to a Controller</span></span>

<span data-ttu-id="405d3-285">지금까지 사용자가 반환 해 왔습니다 상수 문자열 컨트롤러에서.</span><span class="sxs-lookup"><span data-stu-id="405d3-285">Until now, you have been returning constant strings from the Controllers.</span></span> <span data-ttu-id="405d3-286">이 연습에서는 컨트롤러 URL 및 쿼리 문자열을 사용 하 고 브라우저에 텍스트를 사용 하 여 응답 메서드 동작을 설정한 후에 매개 변수를 전달 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-286">In this exercise you will learn how to pass parameters to a Controller using the URL and querystring, and then making the method actions respond with text to the browser.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Adding_Genre_Parameter_to_StoreController"></a>
#### <a name="task-1---adding-genre-parameter-to-storecontroller"></a><span data-ttu-id="405d3-287">작업 1-StoreController 추가 장르 매개 변수</span><span class="sxs-lookup"><span data-stu-id="405d3-287">Task 1 - Adding Genre Parameter to StoreController</span></span>

<span data-ttu-id="405d3-288">이 작업을 사용 하 여는 **querystring** 매개 변수를 보낼를 **찾아보기** 에서 작업 메서드를 **StoreController**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-288">In this task, you will use the **querystring** to send parameters to the **Browse** action method in the **StoreController**.</span></span>

1. <span data-ttu-id="405d3-289">아직 열지 않은 경우 시작 **VS Express for Web**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-289">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="405d3-290">에 **파일** 메뉴 선택 **프로젝트 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-290">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="405d3-291">이동할 프로젝트 열기 대화 상자에서 **Source\Ex03 PassingParametersToAController\Begin**를 선택 **Begin.sln** 클릭 **열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-291">In the Open Project dialog, browse to **Source\Ex03-PassingParametersToAController\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="405d3-292">또는 계속 진행할 솔루션 이전 연습을 완료 한 후 가져온 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-292">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="405d3-293">제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-293">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="405d3-294">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-294">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="405d3-295">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="405d3-295">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="405d3-296">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-296">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="405d3-297">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-297">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="405d3-298">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-298">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="405d3-299">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-299">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="405d3-300">오픈 **StoreController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-300">Open **StoreController** class.</span></span> <span data-ttu-id="405d3-301">이 수행 하는 **솔루션 탐색기**를 확장 합니다 **컨트롤러** 폴더를 두 번 클릭 **StoreController.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-301">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
4. <span data-ttu-id="405d3-302">변경 된 **찾아보기** 메서드를 특정 장르를 요청 하려면 문자열 매개 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-302">Change the **Browse** method, adding a string parameter to request for a specific genre.</span></span> <span data-ttu-id="405d3-303">ASP.NET MVC는 자동으로 모든 쿼리 문자열을 전달 하거나 폼 게시 매개 변수 이름이 **장르** 호출 될 때이 동작 메서드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-303">ASP.NET MVC will automatically pass any querystring or form post parameters named **genre** to this action method when invoked.</span></span> <span data-ttu-id="405d3-304">이 작업을 수행 하려면 대체 합니다 **찾아보기** 메서드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="405d3-304">To do this, replace the **Browse** method with the following code:</span></span>

    <span data-ttu-id="405d3-305">(코드 조각- *ASP.NET MVC 4 기본 사항-Ex3 StoreController BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="405d3-305">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex3 StoreController BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="405d3-306">사용 중인 합니다 **HttpUtility.HtmlEncode** 유틸리티 메서드를 같은 링크를 사용 하 여 보기에 Javascript를 주입에서 사용자의 것을 금지   **/저장소/찾아보기? 장르 =&lt;스크립트&gt;window.location = '[http://hackersite.com](http://hackersite.com)'&lt;/script&gt;** 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-306">You are using the **HttpUtility.HtmlEncode** utility method to prevents users from injecting Javascript into the View with a link like **/Store/Browse?Genre=&lt;script&gt;window.location='[http://hackersite.com](http://hackersite.com)'&lt;/script&gt;**.</span></span>
> 
> <span data-ttu-id="405d3-307">설명은 참조 하세요 [이 msdn 문서](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-307">For further explanation, please visit [this msdn article](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx).</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="405d3-308">작업 2-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="405d3-308">Task 2 - Running the Application</span></span>

<span data-ttu-id="405d3-309">이 작업에서는 웹 브라우저에서 응용 프로그램을 사용해을 사용 합니다 **장르** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-309">In this task, you will try out the Application in a web browser and use the **genre** parameter.</span></span>

1. <span data-ttu-id="405d3-310">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-310">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="405d3-311">프로젝트에서 시작 합니다 **홈** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-311">The project starts in the **Home** page.</span></span> <span data-ttu-id="405d3-312">URL을 변경   */저장/찾아보기? 장르 Disco =* 작업 장르 매개 변수를 수신 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-312">Change the URL to */Store/Browse?Genre=Disco* to verify that the action receives the genre parameter.</span></span>

    <span data-ttu-id="405d3-313">![StoreBrowseGenre 검색 = Disco](aspnet-mvc-4-fundamentals/_static/image10.png "StoreBrowseGenre 검색 Disco =")</span><span class="sxs-lookup"><span data-stu-id="405d3-313">![Browsing StoreBrowseGenre=Disco](aspnet-mvc-4-fundamentals/_static/image10.png "Browsing StoreBrowseGenre=Disco")</span></span>

    <span data-ttu-id="405d3-314">*검색 /Store/Browse? 장르 Disco =*</span><span class="sxs-lookup"><span data-stu-id="405d3-314">*Browsing /Store/Browse?Genre=Disco*</span></span>
3. <span data-ttu-id="405d3-315">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-315">Close the browser.</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Adding_an_Id_Parameter_Embedded_in_the_URL"></a>
#### <a name="task-3---adding-an-id-parameter-embedded-in-the-url"></a><span data-ttu-id="405d3-316">작업 3-URL에 포함 하는 Id 매개 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-316">Task 3 - Adding an Id Parameter Embedded in the URL</span></span>

<span data-ttu-id="405d3-317">이 작업을 사용 하 여는 **URL** 전달 하는 **Id** 매개 변수를를 **세부 정보** 의 동작 메서드를 **StoreController**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-317">In this task, you will use the **URL** to pass an **Id** parameter to the **Details** action method of the **StoreController**.</span></span> <span data-ttu-id="405d3-318">ASP.NET MVC의 기본 명명 된 매개 변수로 작업 메서드 이름 뒤에 url 세그먼트를 처리 하는 라우팅 규칙 **Id**합니다. 동작 메서드에서 Id 라는 매개 변수가 있으면 다음 ASP.NET MVC는 자동으로 URL 세그먼트를 매개 변수로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-318">ASP.NET MVC's default routing convention is to treat the segment of a URL after the action method name as a parameter named **Id**. If your action method has parameter named Id, then ASP.NET MVC will automatically pass the URL segment to you as a parameter.</span></span> <span data-ttu-id="405d3-319">URL에 **저장소/세부 정보/5**를 **Id** 로 해석 됩니다 **5**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-319">In the URL **Store/Details/5**, **Id** will be interpreted as **5**.</span></span>

1. <span data-ttu-id="405d3-320">변경 합니다 **세부 정보** 메서드는 **StoreController**추가는 **int** 라는 매개 변수 **id**합니다. 이 작업을 수행 하려면 대체 합니다 **세부 정보** 메서드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="405d3-320">Change the **Details** method of the **StoreController**, adding an **int** parameter called **id**. To do this, replace the **Details** method with the following code:</span></span>

    <span data-ttu-id="405d3-321">(코드 조각- *ASP.NET MVC 4 기본 사항-Ex3 StoreController DetailsMethod*)</span><span class="sxs-lookup"><span data-stu-id="405d3-321">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex3 StoreController DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample5.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="405d3-322">작업 4-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="405d3-322">Task 4 - Running the Application</span></span>

<span data-ttu-id="405d3-323">이 작업에서는 웹 브라우저에서 응용 프로그램을 사용해을 사용 합니다 **Id** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-323">In this task, you will try out the Application in a web browser and use the **Id** parameter.</span></span>

1. <span data-ttu-id="405d3-324">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-324">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="405d3-325">프로젝트에서 시작 합니다 **홈** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-325">The project starts in the **Home** page.</span></span> <span data-ttu-id="405d3-326">URL을 변경 */Store/Details/5* 동작 id 매개 변수를 수신 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-326">Change the URL to */Store/Details/5* to verify that the action receives the id parameter.</span></span>

    <span data-ttu-id="405d3-327">![검색 StoreDetails5](aspnet-mvc-4-fundamentals/_static/image11.png "StoreDetails5 검색")</span><span class="sxs-lookup"><span data-stu-id="405d3-327">![Browsing StoreDetails5](aspnet-mvc-4-fundamentals/_static/image11.png "Browsing StoreDetails5")</span></span>

    <span data-ttu-id="405d3-328">*검색 /Store/Details/5*</span><span class="sxs-lookup"><span data-stu-id="405d3-328">*Browsing /Store/Details/5*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Creating_a_View"></a>
### <a name="exercise-4-creating-a-view"></a><span data-ttu-id="405d3-329">실습 4: 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="405d3-329">Exercise 4: Creating a View</span></span>

<span data-ttu-id="405d3-330">지금 있습니다가 된 문자열에서에서 반환 컨트롤러 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-330">So far you have been returning strings from controller actions.</span></span> <span data-ttu-id="405d3-331">컨트롤러의 작동 방식을 이해 하는 데 도움이 인 이지만 방식을 실제 웹 응용 프로그램은 빌드되지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-331">Although that is a useful way of understanding how controllers work, it is not how your real Web applications are built.</span></span> <span data-ttu-id="405d3-332">뷰는 템플릿 파일을 사용 하 여 브라우저로 HTML을 생성 하는 것에 대 한 더 나은 방법을 제공 하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-332">Views are components that provide a better approach for generating HTML back to the browser with the use of template files.</span></span>

<span data-ttu-id="405d3-333">이 연습에서는 일반 HTML 콘텐츠를 사이트 및 마지막으로 HTML을 반환 하는 HomeController를 사용 하도록 설정 하려면 보기 템플릿을의 모양과 느낌을 개선 하는 스타일 시트에 대 한 템플릿을 설정 하는 레이아웃 마스터 페이지를 추가 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-333">In this exercise you will learn how to add a layout master page to setup a template for common HTML content, a StyleSheet to enhance the look and feel of the site and finally a View template to enable HomeController to return HTML.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Modifying_the_file__layoutcshtml"></a>
#### <a name="task-1---modifying-the-file-layoutcshtml"></a><span data-ttu-id="405d3-334">작업 1-파일을 수정 \_layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="405d3-334">Task 1 - Modifying the file \_layout.cshtml</span></span>

<span data-ttu-id="405d3-335">파일 **~/Views/Shared/\_layout.cshtml** 전체 웹 사이트에서 사용 하기 위해 일반적인 HTML에 대 한 템플릿을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-335">The file **~/Views/Shared/\_layout.cshtml** allows you to setup a template for common HTML to use across the entire website.</span></span> <span data-ttu-id="405d3-336">이 태스크에서는 홈 페이지 및 저장소 영역에 대 한 링크를 사용 하 여 공용 헤더를 사용 하 여 레이아웃 마스터 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-336">In this task you will add a layout master page with a common header with links to the Home page and Store area.</span></span>

1. <span data-ttu-id="405d3-337">아직 열지 않은 경우 시작 **VS Express for Web**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-337">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="405d3-338">에 **파일** 메뉴 선택 **프로젝트 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-338">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="405d3-339">이동할 프로젝트 열기 대화 상자에서 **Source\Ex04 CreatingAView\Begin**를 선택 **Begin.sln** 클릭 **열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-339">In the Open Project dialog, browse to **Source\Ex04-CreatingAView\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="405d3-340">또는 계속 진행할 솔루션 이전 연습을 완료 한 후 가져온 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-340">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="405d3-341">제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-341">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="405d3-342">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-342">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="405d3-343">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="405d3-343">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="405d3-344">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-344">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="405d3-345">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-345">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="405d3-346">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-346">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="405d3-347">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-347">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="405d3-348">파일  <strong>\_layout.cshtml</strong> 사이트의 모든 페이지에 대 한 HTML 컨테이너 레이아웃을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-348">The file <strong>\_layout.cshtml</strong> contains the HTML container layout for all pages on the site.</span></span> <span data-ttu-id="405d3-349">여기에 <strong>&lt;html&gt;</strong> HTML 응답에 대 한 요소 뿐만 <strong>&lt;헤드&gt;</strong> 하 고 <strong>&lt;본문&gt;</strong> 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-349">It includes the <strong>&lt;html&gt;</strong> element for the HTML response, as well as the <strong>&lt;head&gt;</strong> and <strong>&lt;body&gt;</strong> elements.</span></span> <span data-ttu-id="405d3-350"><strong>@RenderBody()</strong> HTML 내 본문 영역을 확인할 해당 보기 템플릿은 동적 콘텐츠 채워지는 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-350"><strong>@RenderBody()</strong> within the HTML body identify regions that view templates will be able to fill in with dynamic content.</span></span>
   <span data-ttu-id="405d3-351">(C#)</span><span class="sxs-lookup"><span data-stu-id="405d3-351">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample6.cshtml)]
4. <span data-ttu-id="405d3-352">모든 페이지는 사이트의 홈 페이지 및 저장소 영역에 대 한 링크를 사용 하 여 공용 헤더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-352">Add a common header with links to the Home page and Store area on all pages in the site.</span></span> <span data-ttu-id="405d3-353">이 작업을 수행 하기 위해 아래 다음 코드를 추가 &lt;본문&gt; 문입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-353">In order to do that, add the following code below &lt;body&gt; statement.</span></span>
   <span data-ttu-id="405d3-354">(C#)</span><span class="sxs-lookup"><span data-stu-id="405d3-354">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample7.cshtml)]
5. <span data-ttu-id="405d3-355">각 페이지의 본문 섹션을 렌더링 하는 div를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-355">Include a div to render the body section of each page.</span></span> <span data-ttu-id="405d3-356">바꿉니다  <strong>@RenderBody()</strong> 다음 higlighted 코드로: (C#)</span><span class="sxs-lookup"><span data-stu-id="405d3-356">Replace <strong>@RenderBody()</strong> with the following higlighted code: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample8.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="405d3-357">알고 계세요?</span><span class="sxs-lookup"><span data-stu-id="405d3-357">Did you know?</span></span> <span data-ttu-id="405d3-358">Visual Studio 2012 HTML, 코드 파일에서 자주 사용 되는 코드를 추가할 수 있도록 하는 조각이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-358">Visual Studio 2012 has snippets that make it easy to add commonly used code in HTML, code files and more!</span></span> <span data-ttu-id="405d3-359">입력 하 여 시도해 **&lt;div&gt;** 키를 눌러 **탭** 완전 삽입 하려면 두 번 **div** 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-359">Try it out by typing **&lt;div&gt;** and pressing **TAB** twice to insert a complete **div** tag.</span></span>

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_CSS_Stylesheet"></a>
#### <a name="task-2---adding-css-stylesheet"></a><span data-ttu-id="405d3-360">작업 2-CSS 스타일 시트 추가</span><span class="sxs-lookup"><span data-stu-id="405d3-360">Task 2 - Adding CSS Stylesheet</span></span>

<span data-ttu-id="405d3-361">빈 프로젝트 템플릿을 기본 폼 및 유효성 검사 메시지를 표시 하는 데 사용 되는 스타일을 포함 하는 매우 간소화 된 CSS 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-361">The empty project template includes a very streamlined CSS file which just includes styles used to display basic forms and validation messages.</span></span> <span data-ttu-id="405d3-362">사이트의 모양과 느낌을 개선 하기 위해 추가 CSS 및 이미지 (잠재적으로 디자이너에서 제공)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-362">You will use additional CSS and images (potentially provided by a designer) in order to enhance the look and feel of the site.</span></span>

<span data-ttu-id="405d3-363">이 태스크에서는 사이트의 스타일을 정의 하는 CSS 스타일 시트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-363">In this task, you will add a CSS stylesheet to define the styles of the site.</span></span>

1. <span data-ttu-id="405d3-364">CSS 파일 및 이미지에 포함 되어는 **Source\Assets\Content** 이 랩의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-364">The CSS file and images are included in the **Source\Assets\Content** folder of this Lab.</span></span> <span data-ttu-id="405d3-365">응용 프로그램에 추가할 하기 위해 해당 콘텐츠를 끌어를 **Windows 탐색기** 창에는 **솔루션 탐색기** Visual Studio express for Web, 아래와 같이:</span><span class="sxs-lookup"><span data-stu-id="405d3-365">In order to add them to the application, drag their content from a **Windows Explorer** window into the **Solution Explorer** in Visual Studio Express for Web, as shown below:</span></span>

    <span data-ttu-id="405d3-366">![스타일 콘텐츠를 끌어](aspnet-mvc-4-fundamentals/_static/image12.png "스타일 콘텐츠를 끌어")</span><span class="sxs-lookup"><span data-stu-id="405d3-366">![Dragging style contents](aspnet-mvc-4-fundamentals/_static/image12.png "Dragging style contents")</span></span>

    <span data-ttu-id="405d3-367">*스타일 콘텐츠를 끌어*</span><span class="sxs-lookup"><span data-stu-id="405d3-367">*Dragging style contents*</span></span>
2. <span data-ttu-id="405d3-368">경고 대화 상자가 표시 됩니다, 대체를 확인 하 라고 묻는 **Site.css** 파일과 일부 기존 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-368">A warning dialog will appear, asking for confirmation to replace **Site.css** file and some existing images.</span></span> <span data-ttu-id="405d3-369">확인할 **모든 항목에 적용** 누릅니다 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-369">Check **Apply to all items** and click **Yes**.</span></span>

<a id="Ex4Task3"></a>

<a id="Task_3_-_Adding_a_View_Template"></a>
#### <a name="task-3---adding-a-view-template"></a><span data-ttu-id="405d3-370">작업 3-보기 템플릿을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-370">Task 3 - Adding a View Template</span></span>

<span data-ttu-id="405d3-371">이 태스크에서는 레이아웃 마스터 페이지를 사용 하는 HTML 응답을 생성 하기 위해 뷰 템플릿을 추가 하 고이 연습에서 CSS 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-371">In this task, you will add a View template to generate the HTML response that will use the layout master page and CSS added in this exercise.</span></span>

1. <span data-ttu-id="405d3-372">사이트의 홈 페이지를 검색할 때 보기 템플릿을 사용 하려면 먼저 문자열을 반환 하는 대신 나타내는 합니다 **HomeController 인덱스** 메서드는 반환을 **보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-372">To use a View template when browsing the site's home page, you will first need to indicate that instead of returning a string, the **HomeController Index** method will return a **View**.</span></span> <span data-ttu-id="405d3-373">열기 **HomeController** 클래스 및 변경 해당 **인덱스** 반환 하는 메서드는 **ActionResult**를 반환 하 **View()** 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-373">Open **HomeController** class and change its **Index** method to return an **ActionResult**, and have it return **View()**.</span></span>

    <span data-ttu-id="405d3-374">(코드 조각- *ASP.NET MVC 4 기본 사항-Ex4 HomeController 인덱스*)</span><span class="sxs-lookup"><span data-stu-id="405d3-374">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex4 HomeController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample9.cs)]
2. <span data-ttu-id="405d3-375">이제 적절 한 보기 템플릿을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-375">Now, you need to add an appropriate View template.</span></span> <span data-ttu-id="405d3-376">이렇게 하려면 **마우스 오른쪽 단추로 클릭** 내 합니다 **인덱스** 작업 메서드 및 선택 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-376">To do this, **right-click** inside the **Index** action method and select **Add View**.</span></span> <span data-ttu-id="405d3-377">그러면 합니다 **뷰 추가** 대화 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-377">This will bring up the **Add View** dialog.</span></span>

    <span data-ttu-id="405d3-378">![인덱스 메서드 내에서 뷰를 추가](aspnet-mvc-4-fundamentals/_static/image13.png "인덱스 메서드 내에서 뷰 추가")</span><span class="sxs-lookup"><span data-stu-id="405d3-378">![Adding a View from within the Index method](aspnet-mvc-4-fundamentals/_static/image13.png "Adding a View from within the Index method")</span></span>

    <span data-ttu-id="405d3-379">*인덱스 메서드 내에서 뷰 추가*</span><span class="sxs-lookup"><span data-stu-id="405d3-379">*Adding a View from within the Index method*</span></span>
3. <span data-ttu-id="405d3-380">합니다 **뷰 추가** 보기 템플릿 파일을 생성 하려면 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-380">The **Add View** Dialog will appear to generate a View template file.</span></span> <span data-ttu-id="405d3-381">기본적으로이 대화 상자 미리 채웁니다 보기 템플릿의 이름을 사용 하는 작업 메서드를 일치 시킬 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-381">By default, this dialog pre-populates the name of the View template so that it matches the action method that will use it.</span></span> <span data-ttu-id="405d3-382">사용 했기 때문에 **뷰 추가** 내 상황에 맞는 메뉴를 **인덱스** HomeController 내에서 작업 메서드를 **뷰 추가** 대화 상자에 기본 보기 이름으로 인덱스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-382">Because you used the **Add View** context menu within the **Index** action method within the HomeController, the **Add View** dialog has Index as the default view name.</span></span> <span data-ttu-id="405d3-383">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-383">Click **Add**.</span></span>

    <span data-ttu-id="405d3-384">![뷰 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image14.png "뷰 추가 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="405d3-384">![Add View Dialog](aspnet-mvc-4-fundamentals/_static/image14.png "Add View Dialog")</span></span>

    <span data-ttu-id="405d3-385">*뷰 추가 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="405d3-385">*Add View Dialog*</span></span>
4. <span data-ttu-id="405d3-386">Visual Studio에서 생성을 **Index.cshtml** 내에서 템플릿 보기는 **Views\Home** 폴더를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-386">Visual Studio generates an **Index.cshtml** view template inside the **Views\Home** folder and then opens it.</span></span>

    <span data-ttu-id="405d3-387">![만든 인덱스 뷰 홈](aspnet-mvc-4-fundamentals/_static/image15.png "만들어진 인덱스 홈 보기")</span><span class="sxs-lookup"><span data-stu-id="405d3-387">![Home Index view created](aspnet-mvc-4-fundamentals/_static/image15.png "Home Index view created")</span></span>

    <span data-ttu-id="405d3-388">*만든 홈 인덱스 보기*</span><span class="sxs-lookup"><span data-stu-id="405d3-388">*Home Index view created*</span></span>

    > [!NOTE]
    > <span data-ttu-id="405d3-389">이름 및 위치를 **Index.cshtml** 파일 관련 되며 기본 ASP.NET MVC 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-389">name and location of the **Index.cshtml** file is relevant and follows the default ASP.NET MVC naming conventions.</span></span>
    > 
    > <span data-ttu-id="405d3-390">폴더 \Views\**홈** 컨트롤러 이름과 일치 (**홈** 컨트롤러).</span><span class="sxs-lookup"><span data-stu-id="405d3-390">The folder \Views\**Home** matches the controller name (**Home** Controller).</span></span> <span data-ttu-id="405d3-391">보기 템플릿 이름 (**인덱스**), 보기를 표시 하는 컨트롤러 작업 메서드와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-391">The View template name (**Index**), matches the controller action method which will be displaying the View.</span></span>
    > 
    > <span data-ttu-id="405d3-392">이러한 방식으로 ASP.NET MVC 뷰를 반환 하려면이 명명 규칙을 사용 하는 경우 이름 또는 뷰 템플릿의 위치를 명시적으로 지정 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-392">This way, ASP.NET MVC avoids having to explicitly specify the name or location of a View template when using this naming convention to return a View.</span></span>
5. <span data-ttu-id="405d3-393">생성된 된 보기 템플릿을 기반으로 합니다  **\_layout.cshtml** 템플릿을 이전에 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-393">The generated View template is based on the **\_layout.cshtml** template earlier defined.</span></span> <span data-ttu-id="405d3-394">ViewBag.Title 속성을 업데이트 **홈**, 기본 콘텐츠를 변경 하 고 **홈 페이지**아래 코드에 표시 된 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="405d3-394">Update the ViewBag.Title property to **Home**, and change the main content to **This is the Home Page**, as shown in the code below:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample10.cshtml)]
6. <span data-ttu-id="405d3-395">선택 **MvcMusicStore** 누릅니다 솔루션 탐색기에서 프로젝트 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-395">Select **MvcMusicStore** project in the Solution Explorer and Press **F5** to run the Application.</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_Verification"></a>
#### <a name="task-4-verification"></a><span data-ttu-id="405d3-396">작업 4: 확인</span><span class="sxs-lookup"><span data-stu-id="405d3-396">Task 4: Verification</span></span>

<span data-ttu-id="405d3-397">이전 연습에서 단계를 올바르게 수행 했는지를 확인 하기 위해 다음과 같이 계속 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-397">In order to verify that you have correctly performed all the steps in the previous exercise, proceed as follows:</span></span>

<span data-ttu-id="405d3-398">브라우저에서 연 응용 프로그램에 유의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-398">With the application opened in a browser, you should note that:</span></span>

1. <span data-ttu-id="405d3-399">HomeController의 Index 작업 메서드에 찾아서 표시 합니다 **\Views\Home\Index.cshtml** 코드를 호출 하는 경우에 템플릿을 보려면 **View() 반환**이므로 뷰 템플릿을 표준 명명 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-399">The HomeController's Index action method found and displayed the **\Views\Home\Index.cshtml** View template, even though the code called **return View()**, because the View template followed the standard naming convention.</span></span>
2. <span data-ttu-id="405d3-400">홈 페이지 내에 정의 된 환영 메시지를 표시 합니다 **\Views\Home\Index.cshtml** 템플릿 보기.</span><span class="sxs-lookup"><span data-stu-id="405d3-400">The Home Page displays the welcome message defined within the **\Views\Home\Index.cshtml** view template.</span></span>
3. <span data-ttu-id="405d3-401">홈 페이지를 사용 하는  **\_layout.cshtml** 템플릿을 이므로 환영 메시지는 표준 사이트 HTML 레이아웃 내에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-401">The Home Page is using the **\_layout.cshtml** template, and so the welcome message is contained within the standard site HTML layout.</span></span>

    <span data-ttu-id="405d3-402">![인덱스 보기 정의 LayoutPage 및 스타일을 사용 하 여 홈](aspnet-mvc-4-fundamentals/_static/image16.png "정의 LayoutPage 및 스타일을 사용 하 여 인덱스 뷰 홈")</span><span class="sxs-lookup"><span data-stu-id="405d3-402">![Home Index View using the defined LayoutPage and style](aspnet-mvc-4-fundamentals/_static/image16.png "Home Index View using the defined LayoutPage and style")</span></span>

    <span data-ttu-id="405d3-403">*정의 된 LayoutPage 및 스타일을 사용 하 여 홈 인덱스 보기*</span><span class="sxs-lookup"><span data-stu-id="405d3-403">*Home Index View using the defined LayoutPage and style*</span></span>

<a id="Exercise5"></a>

<a id="Exercise_5_Creating_a_View_Model"></a>
### <a name="exercise-5-creating-a-view-model"></a><span data-ttu-id="405d3-404">실습 5: 뷰 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="405d3-404">Exercise 5: Creating a View Model</span></span>

<span data-ttu-id="405d3-405">지금 하드 코드 된 HTML을 표시 하 여 보기를 수행 하지만 동적 웹 응용 프로그램을 만들기 위해 보기 템플릿 받아야 정보 컨트롤러에서.</span><span class="sxs-lookup"><span data-stu-id="405d3-405">So far, you made your Views display hardcoded HTML, but, in order to create dynamic web applications, the View template should receive information from the Controller.</span></span> <span data-ttu-id="405d3-406">해당 용도에 사용 되는 일반적인 방법은 하나는 **ViewModel** 적절 한 HTML 응답을 생성 하는 데 필요한 모든 정보를 패키지 하는 컨트롤러를 허용 하는 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-406">One common technique to be used for that purpose is the **ViewModel** pattern, which allows a Controller to package up all the information needed to generate the appropriate HTML response.</span></span>

<span data-ttu-id="405d3-407">이 연습에서는 ViewModel 클래스를 만들고 필요한 속성을 추가 하는 방법을 배우게 됩니다: 저장소 및 해당 장르 목록에서 장르의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-407">In this exercise, you will learn how to create a ViewModel class and add the required properties: the number of genres in the store and a list of those genres.</span></span> <span data-ttu-id="405d3-408">만든된 ViewModel을 사용 하 여 StoreController 업데이트도 하 고 마지막으로 페이지에 언급 된 속성을 표시 하는 새 보기 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-408">You will also update the StoreController to use the created ViewModel, and finally, you will create a new View template that will display the mentioned properties in the page.</span></span>

<a id="Ex5Task1"></a>

<a id="Task_1_-_Creating_a_ViewModel_Class"></a>
#### <a name="task-1---creating-a-viewmodel-class"></a><span data-ttu-id="405d3-409">작업 1-ViewModel 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="405d3-409">Task 1 - Creating a ViewModel Class</span></span>

<span data-ttu-id="405d3-410">이 태스크에서는 저장소 장르 목록 시나리오를 구현 하는 ViewModel 클래스를 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-410">In this task, you will create a ViewModel class that will implement the Store genre listing scenario.</span></span>

1. <span data-ttu-id="405d3-411">아직 열지 않은 경우 시작 **VS Express for Web**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-411">If not already open, start **VS Express for Web**.</span></span>
2. <span data-ttu-id="405d3-412">에 **파일** 메뉴 선택 **프로젝트 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-412">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="405d3-413">이동할 프로젝트 열기 대화 상자에서 **Source\Ex05 CreatingAViewModel\Begin**를 선택 **Begin.sln** 클릭 **열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-413">In the Open Project dialog, browse to **Source\Ex05-CreatingAViewModel\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="405d3-414">또는 계속 진행할 솔루션 이전 연습을 완료 한 후 가져온 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-414">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="405d3-415">제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-415">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="405d3-416">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-416">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="405d3-417">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="405d3-417">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="405d3-418">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-418">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="405d3-419">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-419">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="405d3-420">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-420">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="405d3-421">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-421">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="405d3-422">만들기는 **Viewmodel** ViewModel을 보관할 폴더를 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-422">Create a **ViewModels** folder to hold the ViewModel.</span></span> <span data-ttu-id="405d3-423">이렇게 하려면 최상위을 마우스 오른쪽 단추로 **MvcMusicStore** 프로젝트 선택 **추가** 차례로 **새 폴더**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-423">To do this, right-click the top-level **MvcMusicStore** project, select **Add** and then **New Folder**.</span></span>

    <span data-ttu-id="405d3-424">![새 폴더 추가](aspnet-mvc-4-fundamentals/_static/image17.png "새 폴더를 추가 합니다.")</span><span class="sxs-lookup"><span data-stu-id="405d3-424">![Adding a new folder](aspnet-mvc-4-fundamentals/_static/image17.png "Adding a new folder")</span></span>

    <span data-ttu-id="405d3-425">*새 폴더를 추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="405d3-425">*Adding a new folder*</span></span>
4. <span data-ttu-id="405d3-426">폴더의 이름을 *Viewmodel*합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-426">Name the folder *ViewModels*.</span></span>

    <span data-ttu-id="405d3-427">![솔루션 탐색기에서 ViewModels 폴더](aspnet-mvc-4-fundamentals/_static/image18.png "솔루션 탐색기에서 ViewModels 폴더")</span><span class="sxs-lookup"><span data-stu-id="405d3-427">![ViewModels folder in Solution Explorer](aspnet-mvc-4-fundamentals/_static/image18.png "ViewModels folder in Solution Explorer")</span></span>

    <span data-ttu-id="405d3-428">*솔루션 탐색기에서 ViewModels 폴더*</span><span class="sxs-lookup"><span data-stu-id="405d3-428">*ViewModels folder in Solution Explorer*</span></span>
5. <span data-ttu-id="405d3-429">만들기는 **ViewModel** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-429">Create a **ViewModel** class.</span></span> <span data-ttu-id="405d3-430">이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **ViewModels** 최근에 만든 폴더를 선택 **추가** 차례로 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-430">To do this, right-click on the **ViewModels** folder recently created, select **Add** and then **New Item**.</span></span> <span data-ttu-id="405d3-431">아래 **코드**를 선택 합니다 **클래스** 항목 및 파일 이름을 *StoreIndexViewModel.cs*, 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-431">Under **Code**, choose the **Class** item and name the file *StoreIndexViewModel.cs*, then click **Add**.</span></span>

    <span data-ttu-id="405d3-432">![새 클래스를 추가](aspnet-mvc-4-fundamentals/_static/image19.png "새 클래스 추가")</span><span class="sxs-lookup"><span data-stu-id="405d3-432">![Adding a new Class](aspnet-mvc-4-fundamentals/_static/image19.png "Adding a new Class")</span></span>

    <span data-ttu-id="405d3-433">*새 클래스 추가*</span><span class="sxs-lookup"><span data-stu-id="405d3-433">*Adding a new Class*</span></span>

    <span data-ttu-id="405d3-434">![StoreIndexViewModel 클래스를 만들어](aspnet-mvc-4-fundamentals/_static/image20.png "만들기 StoreIndexViewModel 클래스")</span><span class="sxs-lookup"><span data-stu-id="405d3-434">![Creating StoreIndexViewModel class](aspnet-mvc-4-fundamentals/_static/image20.png "Creating StoreIndexViewModel class")</span></span>

    <span data-ttu-id="405d3-435">*StoreIndexViewModel 클래스 만들기*</span><span class="sxs-lookup"><span data-stu-id="405d3-435">*Creating StoreIndexViewModel class*</span></span>

<a id="Ex5Task2"></a>

<a id="Task_2_-_Adding_Properties_to_the_ViewModel_class"></a>
#### <a name="task-2---adding-properties-to-the-viewmodel-class"></a><span data-ttu-id="405d3-436">작업 2-ViewModel 클래스에 속성 추가</span><span class="sxs-lookup"><span data-stu-id="405d3-436">Task 2 - Adding Properties to the ViewModel class</span></span>

<span data-ttu-id="405d3-437">에서 전달할 수는 StoreController 보기 템플릿에서 예상 되는 HTML 응답을 생성 하기 위해 두 개의 매개 변수가: 저장소 및 해당 장르 목록에서 장르의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-437">There are two parameters to be passed from the StoreController to the View template in order to generate the expected HTML response: the number of genres in the store and a list of those genres.</span></span>

<span data-ttu-id="405d3-438">이 태스크에서는 이러한 2 속성을 추가 합니다 **StoreIndexViewModel** 클래스: **NumberOfGenres** (정수) 및 **장르** (문자열의 목록).</span><span class="sxs-lookup"><span data-stu-id="405d3-438">In this task, you will add those 2 properties to the **StoreIndexViewModel** class: **NumberOfGenres** (an integer) and **Genres** (a list of strings).</span></span>

1. <span data-ttu-id="405d3-439">추가 **NumberOfGenres** 하 고 **장르** 속성을 **StoreIndexViewModel** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-439">Add **NumberOfGenres** and **Genres** properties to the **StoreIndexViewModel** class.</span></span> <span data-ttu-id="405d3-440">이렇게 하려면 클래스 정의에 다음 두 줄 추가:</span><span class="sxs-lookup"><span data-stu-id="405d3-440">To do this, add the following 2 lines to the class definition:</span></span>

    <span data-ttu-id="405d3-441">(코드 조각- *ASP.NET MVC 4 기본 사항-Ex5 StoreIndexViewModel 속성*)</span><span class="sxs-lookup"><span data-stu-id="405d3-441">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreIndexViewModel properties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample11.cs)]

> [!NOTE]
> <span data-ttu-id="405d3-442">**{get; 설정;}**  표기법에서는 C#의 자동 구현 속성 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-442">The **{ get; set; }** notation makes use of C#'s auto-implemented properties feature.</span></span> <span data-ttu-id="405d3-443">지원 필드를 선언 하기를 요구 하지 않고 속성의 이점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-443">It provides the benefits of a property without requiring us to declare a backing field.</span></span>

<a id="Ex5Task3"></a>

<a id="Task_3_-_Updating_StoreController_to_use_the_StoreIndexViewModel"></a>
#### <a name="task-3---updating-storecontroller-to-use-the-storeindexviewmodel"></a><span data-ttu-id="405d3-444">작업 3-업데이트 StoreController StoreIndexViewModel를 사용 하려면</span><span class="sxs-lookup"><span data-stu-id="405d3-444">Task 3 - Updating StoreController to use the StoreIndexViewModel</span></span>

<span data-ttu-id="405d3-445">합니다 **StoreIndexViewModel** 에서 전달 하는 데 필요한 정보를 캡슐화 하는 클래스 **StoreController**의 **인덱스** 응답을 생성 하기 위해 템플릿 보기를 사용 하는 방법 .</span><span class="sxs-lookup"><span data-stu-id="405d3-445">The **StoreIndexViewModel** class encapsulates the information needed to pass from **StoreController**'s **Index** method to a View template in order to generate a response.</span></span>

<span data-ttu-id="405d3-446">이 태스크에서는 업데이트를 **StoreController** 사용 하는 **StoreIndexViewModel**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-446">In this task, you will update the **StoreController** to use the **StoreIndexViewModel**.</span></span>

1. <span data-ttu-id="405d3-447">오픈 **StoreController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-447">Open **StoreController** class.</span></span>

    <span data-ttu-id="405d3-448">![StoreController 클래스를 열고](aspnet-mvc-4-fundamentals/_static/image21.png "여 StoreController 클래스")</span><span class="sxs-lookup"><span data-stu-id="405d3-448">![Opening StoreController class](aspnet-mvc-4-fundamentals/_static/image21.png "Opening StoreController class")</span></span>

    <span data-ttu-id="405d3-449">*열기 StoreController 클래스*</span><span class="sxs-lookup"><span data-stu-id="405d3-449">*Opening StoreController class*</span></span>
2. <span data-ttu-id="405d3-450">사용 하기 위해를 **StoreIndexViewModel** 에서 클래스를 **StoreController**, 맨 위에 있는 다음 네임 스페이스를 추가 합니다 **StoreController** 코드:</span><span class="sxs-lookup"><span data-stu-id="405d3-450">In order to use the **StoreIndexViewModel** class from the **StoreController**, add the following namespace at the top of the **StoreController** code:</span></span>

    <span data-ttu-id="405d3-451">(코드 조각- *ASP.NET MVC 4 기본 사항-Viewmodel을 사용 하 여 Ex5 StoreIndexViewModel*)</span><span class="sxs-lookup"><span data-stu-id="405d3-451">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreIndexViewModel using ViewModels*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample12.cs)]
3. <span data-ttu-id="405d3-452">변경 된 **StoreController**의 **인덱스** 를 만들고 채우는 작업 메서드를 **StoreIndexViewModel** 개체 한 다음를 뷰 템플릿으로 전달 이 사용 하 여 HTML 응답을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-452">Change the **StoreController**'s **Index** action method so that it creates and populates a **StoreIndexViewModel** object and then passes it off to a View template to generate an HTML response with it.</span></span>

    > [!NOTE]
    > <span data-ttu-id="405d3-453">랩에서 &quot;ASP.NET MVC 모델 및 데이터 액세스&quot; 저장소 장르 목록을 데이터베이스에서 검색 하는 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-453">In Lab &quot;ASP.NET MVC Models and Data Access&quot; you will write code that retrieves the list of store genres from a database.</span></span> <span data-ttu-id="405d3-454">다음 코드를 만듭니다는 **목록** 채울 더미 데이터가 장르를 **StoreIndexViewModel**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-454">In the following code, you will create a **List** of dummy data genres that will populate the **StoreIndexViewModel**.</span></span>
    > 
    > <span data-ttu-id="405d3-455">만들기 및 설정 후 합니다 **StoreIndexViewModel** 개체를 인수로 전달 됩니다 합니다 **보기** 메서드.</span><span class="sxs-lookup"><span data-stu-id="405d3-455">After creating and setting up the **StoreIndexViewModel** object, it will be passed as an argument to the **View** method.</span></span> <span data-ttu-id="405d3-456">보기 템플릿에서 된 HTML 응답을 생성 하려면 해당 개체를 사용할지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-456">This indicates that the View template will use that object to generate an HTML response with it.</span></span>
4. <span data-ttu-id="405d3-457">대체는 **인덱스** 메서드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="405d3-457">Replace the **Index** method with the following code:</span></span>

    <span data-ttu-id="405d3-458">(코드 조각- *ASP.NET MVC 4 기본 사항-Ex5 StoreController 인덱스 메서드*)</span><span class="sxs-lookup"><span data-stu-id="405d3-458">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex5 StoreController Index method*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample13.cs)]

> [!NOTE]
> <span data-ttu-id="405d3-459">C#을 사용 하 여 잘 모르는 경우 사용 가정할 수 있습니다 **var** 함을 의미 합니다 **viewModel** 변수가 런타임에 바인딩된.</span><span class="sxs-lookup"><span data-stu-id="405d3-459">If you're unfamiliar with C#, you may assume that using **var** means that the **viewModel** variable is late-bound.</span></span> <span data-ttu-id="405d3-460">올바른-C# 컴파일러는 형식 유추를 변수에 할당 하는 항목에 따라 사용 하 여 확인 하는 없는 **viewModel** 유형의 **StoreIndexViewModel**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-460">That's not correct - the C# compiler is using type-inference based on what you assign to the variable to determine that **viewModel** is of type **StoreIndexViewModel**.</span></span> <span data-ttu-id="405d3-461">또한 로컬을 컴파일하여 **viewModel** 으로 변수를 **StoreIndexViewModel** 형식의 get 컴파일 타임 검사와 Visual Studio 코드 편집기 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-461">Also, by compiling the local **viewModel** variable as a **StoreIndexViewModel** type you get compile-time checking and Visual Studio code-editor support.</span></span>

<a id="Ex5Task4"></a>

<a id="Task_4_-_Creating_a_View_Template_that_Uses_StoreIndexViewModel"></a>
#### <a name="task-4---creating-a-view-template-that-uses-storeindexviewmodel"></a><span data-ttu-id="405d3-462">작업 4-StoreIndexViewModel를 사용 하는 보기 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="405d3-462">Task 4 - Creating a View Template that Uses StoreIndexViewModel</span></span>

<span data-ttu-id="405d3-463">이 태스크에서는 장르 목록을 표시 하려면 컨트롤러에서 전달 되는 StoreIndexViewModel 개체에서 사용할 보기 템플릿을 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-463">In this task, you will create a View template that will use a StoreIndexViewModel object passed from the Controller to display a list of genres.</span></span>

1. <span data-ttu-id="405d3-464">새 템플릿 보기를 만들기 전에 프로젝트를 빌드 해 보겠습니다 있도록를 **뷰 추가 대화 상자** 알고 합니다 **StoreIndexViewModel** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-464">Before creating the new View template, let's build the project so that the **Add View Dialog** knows about the **StoreIndexViewModel** class.</span></span> <span data-ttu-id="405d3-465">선택 하 여 프로젝트를 빌드할 합니다 **빌드** 메뉴 항목 차례로 **MvcMusicStore 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-465">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="405d3-466">![프로젝트를 빌드하면](aspnet-mvc-4-fundamentals/_static/image22.png "프로젝트 빌드")</span><span class="sxs-lookup"><span data-stu-id="405d3-466">![Building the project](aspnet-mvc-4-fundamentals/_static/image22.png "Building the project")</span></span>

    <span data-ttu-id="405d3-467">*프로젝트 빌드*</span><span class="sxs-lookup"><span data-stu-id="405d3-467">*Building the project*</span></span>
2. <span data-ttu-id="405d3-468">새 보기 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-468">Create a new View template.</span></span> <span data-ttu-id="405d3-469">이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **인덱스** 선택한 메서드 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-469">To do that, right-click inside the **Index** method and select **Add View**.</span></span>

    <span data-ttu-id="405d3-470">![뷰 추가](aspnet-mvc-4-fundamentals/_static/image23.png "뷰 추가")</span><span class="sxs-lookup"><span data-stu-id="405d3-470">![Adding a View](aspnet-mvc-4-fundamentals/_static/image23.png "Adding a View")</span></span>

    <span data-ttu-id="405d3-471">*보기 추가*</span><span class="sxs-lookup"><span data-stu-id="405d3-471">*Adding a View*</span></span>
3. <span data-ttu-id="405d3-472">때문에 **추가 보기 대화 상자** 에서 호출한를 **StoreController**, 템플릿 보기에는 기본적으로 추가 됩니다는 **\Views\Store\Index.cshtml** 파일.</span><span class="sxs-lookup"><span data-stu-id="405d3-472">Because the **Add View Dialog** was invoked from the **StoreController**, it will add the View template by default in a **\Views\Store\Index.cshtml** file.</span></span> <span data-ttu-id="405d3-473">확인 합니다 **는 강력한 형식의-뷰 만들기** 확인란을 선택한 후 **StoreIndexViewModel** 으로 **모델 클래스**.</span><span class="sxs-lookup"><span data-stu-id="405d3-473">Check the **Create a strongly-typed-view** checkbox and then select **StoreIndexViewModel** as the **Model class**.</span></span> <span data-ttu-id="405d3-474">또한 선택 하는 뷰 엔진이 인지를 확인 **Razor**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-474">Also, make sure that the View engine selected is **Razor**.</span></span> <span data-ttu-id="405d3-475">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-475">Click **Add**.</span></span>

    <span data-ttu-id="405d3-476">![뷰 추가 대화 상자](aspnet-mvc-4-fundamentals/_static/image24.png "뷰 추가 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="405d3-476">![Add View Dialog](aspnet-mvc-4-fundamentals/_static/image24.png "Add View Dialog")</span></span>

    <span data-ttu-id="405d3-477">*뷰 추가 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="405d3-477">*Add View Dialog*</span></span>

    <span data-ttu-id="405d3-478">합니다 **\Views\Store\Index.cshtml** 보기 템플릿 파일 만들어지고 열립니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-478">The **\Views\Store\Index.cshtml** View template file is created and opened.</span></span> <span data-ttu-id="405d3-479">에 제공 된 정보를 기반으로 **뷰 추가** 템플릿이 예상 하는 보기 마지막 단계에서는 대화를 **StoreIndexViewModel** 인스턴스로 데이터를 사용 하 여 HTML 응답을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-479">Based on the information provided to the **Add View** dialog in the last step, the View template will expect a **StoreIndexViewModel** instance as the data to use to generate an HTML response.</span></span> <span data-ttu-id="405d3-480">템플릿을 상속 하는 것을 알 수 있습니다는 `ViewPage<musicstore.viewmodels.storeindexviewmodel>` C#입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-480">You will notice that the template inherits a `ViewPage<musicstore.viewmodels.storeindexviewmodel>` in C#.</span></span>

<a id="Ex5Task5"></a>

<a id="Task_5_-_Updating_the_View_Template"></a>
#### <a name="task-5---updating-the-view-template"></a><span data-ttu-id="405d3-481">작업 5-템플릿 보기를 업데이트 하는 중</span><span class="sxs-lookup"><span data-stu-id="405d3-481">Task 5 - Updating the View Template</span></span>

<span data-ttu-id="405d3-482">이 태스크에서는 장르 및 페이지 내에서 해당 이름의 수를 검색 하려면 마지막 작업에서 만든 뷰 템플릿을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-482">In this task, you will update the View template created in the last task to retrieve the number of genres and their names within the page.</span></span>

> [!NOTE]
> <span data-ttu-id="405d3-483">@ 구문은 사용 하 여 (라고도 &quot;코드 너 깃&quot;) 템플릿 보기 내에서 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-483">You will use @ syntax (often referred to as &quot;code nuggets&quot;) to execute code within the View template.</span></span>

1. <span data-ttu-id="405d3-484">**Index.cshtml** 파일 내는 **저장소** 폴더를 해당 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-484">In the **Index.cshtml** file, within the **Store** folder, replace its code with the following:</span></span>

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
2. <span data-ttu-id="405d3-485">장르 목록 루프 **StoreIndexViewModel** HTML 만들어 **&lt;ul&gt;** 사용 하 여 목록을 **foreach** 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-485">Loop over the genre list in **StoreIndexViewModel** and create an HTML **&lt;ul&gt;** list using a **foreach** loop.</span></span>
   <span data-ttu-id="405d3-486">(C#)</span><span class="sxs-lookup"><span data-stu-id="405d3-486">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample15.cshtml)]
3. <span data-ttu-id="405d3-487">키를 눌러 **F5** 응용 프로그램을 실행 하 여 찾아보기 **스토어**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-487">Press **F5** to run the Application and browse **/Store**.</span></span> <span data-ttu-id="405d3-488">전달 하는 장르 목록을 표시 합니다 **StoreIndexViewModel** 에서 개체를 **StoreController** 보기 템플릿에 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-488">You will see the list of genres passed in the **StoreIndexViewModel** object from the **StoreController** to the View template.</span></span>

    <span data-ttu-id="405d3-489">![장르 목록을 표시 하는 보기](aspnet-mvc-4-fundamentals/_static/image26.png "장르 목록을 표시 하는 보기")</span><span class="sxs-lookup"><span data-stu-id="405d3-489">![View displaying a list of genres](aspnet-mvc-4-fundamentals/_static/image26.png "View displaying a list of genres")</span></span>

    <span data-ttu-id="405d3-490">*장르 목록을 표시 하는 보기*</span><span class="sxs-lookup"><span data-stu-id="405d3-490">*View displaying a list of genres*</span></span>
4. <span data-ttu-id="405d3-491">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-491">Close the browser.</span></span>

<a id="Exercise6"></a>

<a id="Exercise_6_Using_Parameters_in_View"></a>
### <a name="exercise-6-using-parameters-in-view"></a><span data-ttu-id="405d3-492">실습 6:를 사용 하 여 매개 변수 보기</span><span class="sxs-lookup"><span data-stu-id="405d3-492">Exercise 6: Using Parameters in View</span></span>

<span data-ttu-id="405d3-493">연습 3의 컨트롤러에 매개 변수를 전달 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-493">In Exercise 3 you learned how to pass parameters to the Controller.</span></span> <span data-ttu-id="405d3-494">이 연습에서는 보기 템플릿에서 이러한 매개 변수를 사용 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-494">In this exercise, you will learn how to use those parameters in the View template.</span></span> <span data-ttu-id="405d3-495">이 위해 소개 합니다 먼저 사용자 데이터 및 도메인 논리를 관리 하는 데 도움이 되는 모델 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-495">For that purpose, you will be introduced first to Model classes that will help you to manage your data and domain logic.</span></span> <span data-ttu-id="405d3-496">또한 인코딩 URL 경로 등의 걱정 없이 ASP.NET MVC 응용 프로그램 내 페이지의 링크를 만드는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-496">Additionally, you will learn how to create links to pages inside the ASP.NET MVC application without worrying of things like URL paths encoding.</span></span>

<a id="Ex6Task1"></a>

<a id="Task_1_-_Adding_Model_Classes"></a>
#### <a name="task-1---adding-model-classes"></a><span data-ttu-id="405d3-497">작업 1-모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="405d3-497">Task 1 - Adding Model Classes</span></span>

<span data-ttu-id="405d3-498">모델 클래스는 컨트롤러에서 보기로 정보를 전달 하기 위한 것 만들어지는 Viewmodel와 달리 포함 하 고 데이터 및 도메인 논리를 관리할에 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-498">Unlike ViewModels, which are created just to pass information from the Controller to the View, Model classes are built to contain and manage data and domain logic.</span></span> <span data-ttu-id="405d3-499">이 작업에서는 이러한 개념을 나타내기 위해 두 모델 클래스를 추가 합니다. **장르** 하 고 **앨범**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-499">In this task you will add two model classes to represent these concepts: **Genre** and **Album**.</span></span>

1. <span data-ttu-id="405d3-500">아직 열지 않은 경우 시작 **VS Express for Web**</span><span class="sxs-lookup"><span data-stu-id="405d3-500">If not already open, start **VS Express for Web**</span></span>
2. <span data-ttu-id="405d3-501">에 **파일** 메뉴 선택 **프로젝트 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-501">In the **File** menu, choose **Open Project**.</span></span> <span data-ttu-id="405d3-502">이동할 프로젝트 열기 대화 상자에서 **Source\Ex06 UsingParametersInView\Begin**를 선택 **Begin.sln** 클릭 **열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-502">In the Open Project dialog, browse to **Source\Ex06-UsingParametersInView\Begin**, select **Begin.sln** and click **Open**.</span></span> <span data-ttu-id="405d3-503">또는 계속 진행할 솔루션 이전 연습을 완료 한 후 가져온 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-503">Alternatively, you may continue with the solution that you obtained after completing the previous exercise.</span></span>

   1. <span data-ttu-id="405d3-504">제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-504">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="405d3-505">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-505">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="405d3-506">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="405d3-506">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="405d3-507">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-507">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="405d3-508">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-508">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="405d3-509">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-509">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="405d3-510">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-510">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
3. <span data-ttu-id="405d3-511">추가 된 **장르** 모델 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-511">Add a **Genre** Model class.</span></span> <span data-ttu-id="405d3-512">이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **모델** 폴더에는 **솔루션 탐색기**를 선택 **추가** 차례로 **새 항목** 옵션.</span><span class="sxs-lookup"><span data-stu-id="405d3-512">To do this, right-click the **Models** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="405d3-513">아래 **코드**를 선택 합니다 **클래스** 항목 및 파일 이름을 *Genre.cs*, 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-513">Under **Code**, choose the **Class** item and name the file *Genre.cs*, then click **Add**.</span></span>

    <span data-ttu-id="405d3-514">![클래스 추가](aspnet-mvc-4-fundamentals/_static/image27.png "클래스 추가")</span><span class="sxs-lookup"><span data-stu-id="405d3-514">![Adding a class](aspnet-mvc-4-fundamentals/_static/image27.png "Adding a class")</span></span>

    <span data-ttu-id="405d3-515">*새 항목 추가*</span><span class="sxs-lookup"><span data-stu-id="405d3-515">*Adding a new item*</span></span>

    <span data-ttu-id="405d3-516">![장르 모델 클래스 추가](aspnet-mvc-4-fundamentals/_static/image28.png "장르 모델 클래스 추가")</span><span class="sxs-lookup"><span data-stu-id="405d3-516">![Add Genre Model Class](aspnet-mvc-4-fundamentals/_static/image28.png "Add Genre Model Class")</span></span>

    <span data-ttu-id="405d3-517">*장르 모델 클래스 추가*</span><span class="sxs-lookup"><span data-stu-id="405d3-517">*Add Genre Model Class*</span></span>
4. <span data-ttu-id="405d3-518">추가 된 **이름** 장르 클래스 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-518">Add a **Name** property to the Genre class.</span></span> <span data-ttu-id="405d3-519">이렇게 하려면 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-519">To do this, add the following code:</span></span>

    <span data-ttu-id="405d3-520">(코드 조각- *ASP.NET MVC 4 기본 사항-Ex6 장르*)</span><span class="sxs-lookup"><span data-stu-id="405d3-520">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 Genre*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample16.cs)]
5. <span data-ttu-id="405d3-521">추가 이전으로 동일한 절차를 **앨범** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-521">Following the same procedure as before, add an **Album** class.</span></span> <span data-ttu-id="405d3-522">이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **모델** 폴더에는 **솔루션 탐색기**를 선택 **추가** 차례로 **새 항목** 옵션.</span><span class="sxs-lookup"><span data-stu-id="405d3-522">To do this, right-click the **Models** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="405d3-523">아래 **코드**를 선택 합니다 **클래스** 항목 및 파일 이름을 *Album.cs*, 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-523">Under **Code**, choose the **Class** item and name the file *Album.cs*, then click **Add**.</span></span>
6. <span data-ttu-id="405d3-524">앨범 클래스에 두 개의 속성을 추가 합니다. **장르** 하 고 **제목**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-524">Add two properties to the Album class: **Genre** and **Title**.</span></span> <span data-ttu-id="405d3-525">이렇게 하려면 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-525">To do this, add the following code:</span></span>

    <span data-ttu-id="405d3-526">(코드 조각- *ASP.NET MVC 4 기본 사항-Ex6 앨범*)</span><span class="sxs-lookup"><span data-stu-id="405d3-526">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 Album*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample17.cs)]

<a id="Ex6Task2"></a>

<a id="Task_2_-_Adding_a_StoreBrowseViewModel"></a>
#### <a name="task-2---adding-a-storebrowseviewmodel"></a><span data-ttu-id="405d3-527">작업 2-는 StoreBrowseViewModel 추가</span><span class="sxs-lookup"><span data-stu-id="405d3-527">Task 2 - Adding a StoreBrowseViewModel</span></span>

<span data-ttu-id="405d3-528">A **StoreBrowseViewModel** 선택한 장르가 일치 하는 앨범에 표시할이 작업에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-528">A **StoreBrowseViewModel** will be used in this task to show the Albums that match a selected Genre.</span></span> <span data-ttu-id="405d3-529">이 태스크에서는이 클래스 만들고 처리에 두 속성을 추가 합니다 **장르** 및 해당 **앨범**의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-529">In this task, you will create this class and then add two properties to handle the **Genre** and its **Album**'s List.</span></span>

1. <span data-ttu-id="405d3-530">추가 된 **StoreBrowseViewModel** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-530">Add a **StoreBrowseViewModel** class.</span></span> <span data-ttu-id="405d3-531">이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **Viewmodel** 폴더에는 **솔루션 탐색기**를 선택 **추가** 차례로 **새 항목** 옵션.</span><span class="sxs-lookup"><span data-stu-id="405d3-531">To do this, right-click the **ViewModels** folder in the **Solution Explorer**, select **Add** and then the **New Item** option.</span></span> <span data-ttu-id="405d3-532">아래 **코드**를 선택 합니다 **클래스** 항목 및 파일 이름을 *StoreBrowseViewModel.cs*, 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-532">Under **Code**, choose the **Class** item and name the file *StoreBrowseViewModel.cs*, then click **Add**.</span></span>
2. <span data-ttu-id="405d3-533">모델에 대 한 참조를 추가 **StoreBrowseViewModel** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-533">Add a reference to the Models in **StoreBrowseViewModel** class.</span></span> <span data-ttu-id="405d3-534">이 작업을 수행 하려면 다음 추가 네임 스페이스를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="405d3-534">To do this, add the following using namespace:</span></span>

    <span data-ttu-id="405d3-535">(코드 조각- *ASP.NET MVC 4 기본 사항-Ex6 UsingModel*)</span><span class="sxs-lookup"><span data-stu-id="405d3-535">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 UsingModel*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample18.cs)]
3. <span data-ttu-id="405d3-536">두 개의 속성을 추가 **StoreBrowseViewModel** 클래스: **장르** 하 고 **앨범**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-536">Add two properties to **StoreBrowseViewModel** class: **Genre** and **Albums**.</span></span> <span data-ttu-id="405d3-537">이렇게 하려면 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-537">To do this, add the following code:</span></span>

    <span data-ttu-id="405d3-538">(코드 조각- *ASP.NET MVC 4 기본 사항-Ex6 ModelProperties*)</span><span class="sxs-lookup"><span data-stu-id="405d3-538">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 ModelProperties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample19.cs)]

> [!NOTE]
> <span data-ttu-id="405d3-539">란 **목록&lt;앨범&gt;**  ?:이 정의 사용 하는 **목록&lt;T&gt;**  형식 여기서 **T** 제한 합니다 이 요소 형식을 **목록을** 여기서 속한 **앨범** (또는 해당 하위 항목 중 하나).</span><span class="sxs-lookup"><span data-stu-id="405d3-539">What is **List&lt;Album&gt;** ?: This definition is using the **List&lt;T&gt;** type, where **T** constrains the type to which elements of this **List** belong to, in this case **Album** (or any of its descendants).</span></span>
> 
> <span data-ttu-id="405d3-540">이 기능을 디자인 하는 클래스 또는 메서드 선언 및 기능은 C# 언어의 클라이언트 코드에서 인스턴스화할 때까지 하나 이상의 형식 사양을 따르는 클래스와 메서드 호출 **제네릭**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-540">This ability to design classes and methods that defer the specification of one or more types until the class or method is declared and instantiated by client code is a feature of the C# language called **Generics**.</span></span>
> 
> <span data-ttu-id="405d3-541">**목록&lt;T&gt;**  제네릭 동일 합니다 **ArrayList** 입력 하 고 사용할 수 있습니다 합니다 **System.Collections.Generic** 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-541">**List&lt;T&gt;** is the generic equivalent of the **ArrayList** type and is available in the **System.Collections.Generic** namespace.</span></span> <span data-ttu-id="405d3-542">사용의 이점 중 하나 **제네릭을** 는 지정 된 형식 이므로 필요가 없습니다 형식 검사에 요소를 캐스팅 하는 등의 작업을 처리 하는 **앨범** 를사용하여마찬가지로**ArrayList**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-542">One of the benefits of using **generics** is that since the type is specified, you do not need to take care of type checking operations such as casting the elements into **Album** as you would do with an **ArrayList**.</span></span>

<a id="Ex6Task3"></a>

<a id="Task_3_-_Using_the_New_ViewModel_in_the_StoreController"></a>
#### <a name="task-3---using-the-new-viewmodel-in-the-storecontroller"></a><span data-ttu-id="405d3-543">작업 3-는 StoreController에서 새 ViewModel을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="405d3-543">Task 3 - Using the New ViewModel in the StoreController</span></span>

<span data-ttu-id="405d3-544">이 태스크에서는 수정 합니다 **StoreController**의 **찾아보기** 하 고 **세부 정보** 작업 메서드를 사용 하도록 **StoreBrowseViewModel** .</span><span class="sxs-lookup"><span data-stu-id="405d3-544">In this task, you will modify the **StoreController**'s **Browse** and **Details** action methods to use the new **StoreBrowseViewModel**.</span></span>

1. <span data-ttu-id="405d3-545">Models 폴더에 대 한 참조를 추가 **StoreController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-545">Add a reference to the Models folder in **StoreController** class.</span></span> <span data-ttu-id="405d3-546">이 작업을 수행 하려면 확장 합니다 **컨트롤러** 폴더에는 **솔루션 탐색기** 연를 **StoreController** 클래스.</span><span class="sxs-lookup"><span data-stu-id="405d3-546">To do this, expand the **Controllers** folder in the **Solution Explorer** and open the **StoreController** class.</span></span> <span data-ttu-id="405d3-547">다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-547">Then add the following code:</span></span>

    <span data-ttu-id="405d3-548">(코드 조각- *ASP.NET MVC 4 기본 사항-Ex6 UsingModelInController*)</span><span class="sxs-lookup"><span data-stu-id="405d3-548">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 UsingModelInController*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample20.cs)]
2. <span data-ttu-id="405d3-549">대체는 **찾아보기** 사용 하는 작업 메서드는 **StoreViewBrowseController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-549">Replace the **Browse** action method to use the **StoreViewBrowseController** class.</span></span> <span data-ttu-id="405d3-550">더미 데이터를 사용 하 여 두 가지 새로운 앨범 개체 및 장르를 만듭니다 (다음 실습 랩에서 사용 데이터베이스의 실제 데이터).</span><span class="sxs-lookup"><span data-stu-id="405d3-550">You will create a Genre and two new Albums objects with dummy data (in the next Hands-on Lab you will consume real data from a database).</span></span> <span data-ttu-id="405d3-551">이 작업을 수행 하려면 대체 합니다 **찾아보기** 메서드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="405d3-551">To do this, replace the **Browse** method with the following code:</span></span>

    <span data-ttu-id="405d3-552">(코드 조각- *ASP.NET MVC 4 기본 사항-Ex6 BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="405d3-552">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample21.cs)]
3. <span data-ttu-id="405d3-553">대체는 **세부 정보** 사용 하는 작업 메서드는 **StoreViewBrowseController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-553">Replace the **Details** action method to use the **StoreViewBrowseController** class.</span></span> <span data-ttu-id="405d3-554">새로 만든 **앨범** 가 반환 될 개체를 **보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-554">You will create a new **Album** object to be returned to the **View**.</span></span> <span data-ttu-id="405d3-555">이 작업을 수행 하려면 대체 합니다 **세부 정보** 메서드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="405d3-555">To do this, replace the **Details** method with the following code:</span></span>

    <span data-ttu-id="405d3-556">(코드 조각- *ASP.NET MVC 4 기본 사항-Ex6 DetailsMethod*)</span><span class="sxs-lookup"><span data-stu-id="405d3-556">(Code Snippet - *ASP.NET MVC 4 Fundamentals - Ex6 DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample22.cs)]

<a id="Ex6Task4"></a>

<a id="Task_4_-_Adding_a_Browse_View_Template"></a>
#### <a name="task-4---adding-a-browse-view-template"></a><span data-ttu-id="405d3-557">작업 4-찾아보기 보기 템플릿을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-557">Task 4 - Adding a Browse View Template</span></span>

<span data-ttu-id="405d3-558">이 태스크에서는 추가 된 **찾아보기** 특정 장르에 앨범을 표시 하도록 보기.</span><span class="sxs-lookup"><span data-stu-id="405d3-558">In this task, you will add a **Browse** View to show the Albums found for a specific Genre.</span></span>

1. <span data-ttu-id="405d3-559">새 템플릿 보기를 만들기 전에 프로젝트를 작성 해야 있도록를 **뷰 추가** 대화에 대해 알고 합니다 **ViewModel** 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-559">Before creating the new View template, you should build the project so that the **Add View** Dialog knows about the **ViewModel** class to use.</span></span> <span data-ttu-id="405d3-560">선택 하 여 프로젝트를 빌드할 합니다 **빌드** 메뉴 항목 차례로 **MvcMusicStore 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-560">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>
2. <span data-ttu-id="405d3-561">추가 된 **찾아보기** 보기.</span><span class="sxs-lookup"><span data-stu-id="405d3-561">Add a **Browse** View.</span></span> <span data-ttu-id="405d3-562">이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **찾아보기** 의 동작 메서드는 **StoreController** 클릭 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-562">To do this, right-click in the **Browse** action method of the **StoreController** and click **Add View**.</span></span>
3. <span data-ttu-id="405d3-563">에 **뷰 추가** 대화 상자에서 보기 이름 인지 확인 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-563">In the **Add View** dialog box, verify that the View Name is **Browse**.</span></span> <span data-ttu-id="405d3-564">확인 합니다 **강력한 형식의 뷰를 만들** 확인란을 선택한 **StoreBrowseViewModel** 에서 **모델 클래스** 드롭다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-564">Check the **Create a strongly-typed view** checkbox and select **StoreBrowseViewModel** from the **Model class** dropdown.</span></span> <span data-ttu-id="405d3-565">다른 필드는 기본값으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-565">Leave the other fields with their default value.</span></span> <span data-ttu-id="405d3-566">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-566">Then click **Add**.</span></span>

    <span data-ttu-id="405d3-567">![찾아보기 뷰 추가](aspnet-mvc-4-fundamentals/_static/image29.png "찾아보기 뷰 추가")</span><span class="sxs-lookup"><span data-stu-id="405d3-567">![Adding a Browse View](aspnet-mvc-4-fundamentals/_static/image29.png "Adding a Browse View")</span></span>

    <span data-ttu-id="405d3-568">*찾아보기 뷰 추가*</span><span class="sxs-lookup"><span data-stu-id="405d3-568">*Adding a Browse View*</span></span>
4. <span data-ttu-id="405d3-569">수정 합니다 **Browse.cshtml** 장르의 정보를 표시 하에 액세스 하는 **StoreBrowseViewModel** 템플릿 보기에 전달 되는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-569">Modify the **Browse.cshtml** to display the Genre's information, accessing the **StoreBrowseViewModel** object that is passed to the view template.</span></span> <span data-ttu-id="405d3-570">이 위해 콘텐츠를 다음으로 바꿉니다. (C#)</span><span class="sxs-lookup"><span data-stu-id="405d3-570">To do this, replace the content with the following: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample23.cshtml)]

<a id="Ex6Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="405d3-571">작업 5-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="405d3-571">Task 5 - Running the Application</span></span>

<span data-ttu-id="405d3-572">이 작업을 테스트 하는 합니다 **찾아보기** 앨범에서를 검색 하는 메서드는 **찾아보기** 메서드 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-572">In this task, you will test that the **Browse** method retrieves Albums from the **Browse** method action.</span></span>

1. <span data-ttu-id="405d3-573">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-573">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="405d3-574">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-574">The project starts in the Home page.</span></span> <span data-ttu-id="405d3-575">URL을 변경   **/저장/찾아보기? 장르 Disco =** 두 앨범을 반환 하는 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-575">Change the URL to **/Store/Browse?Genre=Disco** to verify that the action returns two Albums.</span></span>

    <span data-ttu-id="405d3-576">![Disco 앨범 저장소 찾아보기](aspnet-mvc-4-fundamentals/_static/image30.png "Disco 앨범 저장소를 검색 합니다.")</span><span class="sxs-lookup"><span data-stu-id="405d3-576">![Browsing Store Disco Albums](aspnet-mvc-4-fundamentals/_static/image30.png "Browsing Store Disco Albums")</span></span>

    <span data-ttu-id="405d3-577">*Disco 앨범 저장소를 검색합니다.*</span><span class="sxs-lookup"><span data-stu-id="405d3-577">*Browsing Store Disco Albums*</span></span>

<a id="Ex6Task6"></a>

<a id="Task_6_-_Displaying_information_About_a_Specific_Album"></a>
#### <a name="task-6---displaying-information-about-a-specific-album"></a><span data-ttu-id="405d3-578">태스크 6-정보는 특정 앨범 표시</span><span class="sxs-lookup"><span data-stu-id="405d3-578">Task 6 - Displaying information About a Specific Album</span></span>

<span data-ttu-id="405d3-579">이 작업을 구현 합니다 **저장소/세부 정보** 특정 앨범에 대 한 정보를 표시 하려면 보기.</span><span class="sxs-lookup"><span data-stu-id="405d3-579">In this task, you will implement the **Store/Details** view to display information about a specific album.</span></span> <span data-ttu-id="405d3-580">이 실습 랩에서 앨범에 대 한 표시는 모든 항목에 이미 포함 되어는 **보기** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="405d3-580">In this Hands-on Lab, everything you will display about the album is already contained in the **View** template.</span></span> <span data-ttu-id="405d3-581">새로 만드는 대신이 **StoreDetailsViewModel** 클래스를 현재 사용 하 여 **StoreBrowseViewModel** 앨범 전달할 템플릿.</span><span class="sxs-lookup"><span data-stu-id="405d3-581">So, instead of creating a **StoreDetailsViewModel** class, you will use the current **StoreBrowseViewModel** template passing the Album to it.</span></span>

1. <span data-ttu-id="405d3-582">Visual Studio 창으로 돌아가려면 필요한 경우 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-582">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="405d3-583">새 **세부 정보** 에 대 한 보기를 **StoreController**의 **세부 정보** 작업 메서드.</span><span class="sxs-lookup"><span data-stu-id="405d3-583">Add a new **Details** view for the **StoreController**'s **Details** action method.</span></span> <span data-ttu-id="405d3-584">이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **세부 정보** 에서 메서드는 **StoreController** 클래스 및 클릭 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-584">To do this, right-click the **Details** method in the **StoreController** class and click **Add View**.</span></span>
2. <span data-ttu-id="405d3-585">에 **뷰 추가** 대화 상자에서 되어 있는지 확인 합니다 **뷰 이름** 는 **세부 정보**.</span><span class="sxs-lookup"><span data-stu-id="405d3-585">In the **Add View** dialog, verify that the **View Name** is **Details**.</span></span> <span data-ttu-id="405d3-586">확인 합니다 **강력한 형식의 뷰를 만들** 확인란을 선택한 **앨범** 에서 **모델 클래스** 드롭다운 목록.</span><span class="sxs-lookup"><span data-stu-id="405d3-586">Check the **Create a strongly-typed view** checkbox and select **Album** from the **Model class** drop-down.</span></span> <span data-ttu-id="405d3-587">다른 필드는 기본값으로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-587">Leave the other fields with their default value.</span></span> <span data-ttu-id="405d3-588">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-588">Then click **Add**.</span></span> <span data-ttu-id="405d3-589">이 만들고 엽니다는 **\Views\Store\Details.cshtml** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-589">This will create and open a **\Views\Store\Details.cshtml** file.</span></span>

    <span data-ttu-id="405d3-590">![추가 세부 정보 보기](aspnet-mvc-4-fundamentals/_static/image31.png "세부 정보 보기 추가")</span><span class="sxs-lookup"><span data-stu-id="405d3-590">![Adding a Details View](aspnet-mvc-4-fundamentals/_static/image31.png "Adding a Details View")</span></span>

    <span data-ttu-id="405d3-591">*세부 정보 보기 추가*</span><span class="sxs-lookup"><span data-stu-id="405d3-591">*Adding a Details View*</span></span>
3. <span data-ttu-id="405d3-592">수정 합니다 **Details.cshtml** 앨범의 정보를 표시 하는 파일에 액세스 하는 **앨범** 템플릿 보기에 전달 되는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-592">Modify the **Details.cshtml** file to display the Album's information, accessing the **Album** object that is passed to the view template.</span></span> <span data-ttu-id="405d3-593">이 위해 콘텐츠를 다음으로 바꿉니다. (C#)</span><span class="sxs-lookup"><span data-stu-id="405d3-593">To do this, replace the content with the following: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample24.cshtml)]

<a id="Ex6Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a><span data-ttu-id="405d3-594">태스크 7-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="405d3-594">Task 7 - Running the Application</span></span>

<span data-ttu-id="405d3-595">이 작업을 테스트 하는 합니다 **세부 정보** 보기에서 앨범의 정보를 검색 합니다 **작업 세부 정보** 메서드.</span><span class="sxs-lookup"><span data-stu-id="405d3-595">In this task, you will test that the **Details** View retrieves Album's information from the **Details action** method.</span></span>

1. <span data-ttu-id="405d3-596">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-596">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="405d3-597">프로젝트에서 시작 합니다 **홈** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-597">The project starts in the **Home** page.</span></span> <span data-ttu-id="405d3-598">URL을 변경 **/Store/Details/5** 앨범의 정보를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-598">Change the URL to **/Store/Details/5** to verify the album's information.</span></span>

    <span data-ttu-id="405d3-599">![앨범 세부 정보를 검색](aspnet-mvc-4-fundamentals/_static/image32.png "앨범 세부 정보를 검색 합니다.")</span><span class="sxs-lookup"><span data-stu-id="405d3-599">![Browsing Albums Detail](aspnet-mvc-4-fundamentals/_static/image32.png "Browsing Albums Detail")</span></span>

    <span data-ttu-id="405d3-600">*앨범의 세부 정보를 검색합니다.*</span><span class="sxs-lookup"><span data-stu-id="405d3-600">*Browsing Album's Detail*</span></span>

<a id="Ex6Task8"></a>

<a id="Task_8_-_Adding_Links_Between_Pages"></a>
#### <a name="task-8---adding-links-between-pages"></a><span data-ttu-id="405d3-601">태스크 8-페이지 간 링크 추가</span><span class="sxs-lookup"><span data-stu-id="405d3-601">Task 8 - Adding Links Between Pages</span></span>

<span data-ttu-id="405d3-602">이 태스크에서는 적절 한 모든 장르 이름에 링크가 있습니다 저장소 뷰에서 링크를 추가 합니다 **/저장소/찾아보기** URL입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-602">In this task, you will add a link in the Store View to have a link in every Genre name to the appropriate **/Store/Browse** URL.</span></span> <span data-ttu-id="405d3-603">이 이렇게 하면 예를 들어 장르를 클릭 **Disco**로 이동 됩니다 **/저장소/찾아보기? 장르 Disco =** URL입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-603">This way, when you click on a Genre, for instance **Disco**, it will navigate to **/Store/Browse?genre=Disco** URL.</span></span>

1. <span data-ttu-id="405d3-604">Visual Studio 창으로 돌아가려면 필요한 경우 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-604">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="405d3-605">업데이트를 **인덱스** 에 대 한 링크를 추가 하려면 페이지의 **찾아보기** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-605">Update the **Index** page to add a link to the **Browse** page.</span></span> <span data-ttu-id="405d3-606">이 수행 하는 **솔루션 탐색기** 확장를 **뷰** 폴더를 해당 **저장소** 폴더를 두 번 클릭 합니다 **Index.cshtml** 페이지.</span><span class="sxs-lookup"><span data-stu-id="405d3-606">To do this, in the **Solution Explorer** expand the **Views** folder, then the **Store** folder and double-click the **Index.cshtml** page.</span></span>
2. <span data-ttu-id="405d3-607">선택한 장르를 나타내는 찾아보기 보기에 대 한 링크를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-607">Add a link to the Browse view indicating the genre selected.</span></span> <span data-ttu-id="405d3-608">이렇게 하려면 다음 강조 표시 된 코드를 대체 합니다 **&lt;li&gt;** 태그: (C#)</span><span class="sxs-lookup"><span data-stu-id="405d3-608">To do this, replace the following highlighted code within the **&lt;li&gt;** tags: (C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample25.cshtml)]

   > [!NOTE]
   > <span data-ttu-id="405d3-609">또 다른 방법은 다음과 같은 코드를 사용 하 여 페이지에 직접 연결할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-609">another approach would be linking directly to the page, with a code like the following:</span></span>
   > 
   > <span data-ttu-id="405d3-610">&lt;a href=&quot;/Store/Browse?genre=@genreName&quot;&gt;@genreName&lt;/a&gt;</span><span class="sxs-lookup"><span data-stu-id="405d3-610">&lt;a href=&quot;/Store/Browse?genre=@genreName&quot;&gt;@genreName&lt;/a&gt;</span></span>
   > 
   > <span data-ttu-id="405d3-611">이 방법은 작동 하지만 하드 코드 된 문자열에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-611">Although this approach works, it depends on a hardcoded string.</span></span> <span data-ttu-id="405d3-612">나중에 컨트롤러를 바꾸면를 사용 하는 경우에이 명령이 수동으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-612">If you later rename the Controller, you will have to change this instruction manually.</span></span> <span data-ttu-id="405d3-613">더 나은 방법은 사용 하는 **HTML 도우미** 메서드.</span><span class="sxs-lookup"><span data-stu-id="405d3-613">A better alternative is to use an **HTML Helper** method.</span></span> <span data-ttu-id="405d3-614">ASP.NET MVC에는 이러한 작업에 사용할 수 있는 HTML 도우미 메서드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-614">ASP.NET MVC includes an HTML Helper method which is available for such tasks.</span></span> <span data-ttu-id="405d3-615">**Html.ActionLink()** 도우미 메서드를 사용 하면 손쉽게 HTML 만들 **&lt;를&gt;** 링크, URL 경로 URL로 인코딩된 제대로 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-615">The **Html.ActionLink()** helper method makes it easy to build HTML **&lt;a&gt;** links, making sure URL paths are properly URL encoded.</span></span>
   > 
   > <span data-ttu-id="405d3-616">Htlm.ActionLink 여러 오버 로드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-616">Htlm.ActionLink has several overloads.</span></span> <span data-ttu-id="405d3-617">이 연습의 세 매개 변수를 사용 하는 것을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-617">In this exercise you will use one that takes three parameters:</span></span>
   > 
   > 1. <span data-ttu-id="405d3-618">장르 이름을 표시 하는 링크 텍스트</span><span class="sxs-lookup"><span data-stu-id="405d3-618">Link text, which will display the Genre name</span></span>
   > 2. <span data-ttu-id="405d3-619">컨트롤러 작업 이름 (**찾아보기**)</span><span class="sxs-lookup"><span data-stu-id="405d3-619">Controller action name (**Browse**)</span></span>
   > 3. <span data-ttu-id="405d3-620">경로 매개 변수 값, 두 이름을 지정 (**장르**)과 값 (**장르 이름**)</span><span class="sxs-lookup"><span data-stu-id="405d3-620">Route parameter values, specifying both the name (**Genre**) and the value (**Genre name**)</span></span>

<a id="Ex6Task9"></a>

<a id="Task_9_-_Running_the_Application"></a>
#### <a name="task-9---running-the-application"></a><span data-ttu-id="405d3-621">태스크 9-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="405d3-621">Task 9 - Running the Application</span></span>

<span data-ttu-id="405d3-622">이 태스크에서는 테스트할 장르별로 적절 한 링크와 함께 표시 되도록 **/저장소/찾아보기** URL입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-622">In this task, you will test that each Genre is displayed with a link to the appropriate **/Store/Browse** URL.</span></span>

1. <span data-ttu-id="405d3-623">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-623">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="405d3-624">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-624">The project starts in the Home page.</span></span> <span data-ttu-id="405d3-625">URL을 변경 **스토어** 장르별로 적절 한 링크를 확인 하려면 **/저장소/찾아보기** URL입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-625">Change the URL to **/Store** to verify that each Genre links to the appropriate **/Store/Browse** URL.</span></span>

    <span data-ttu-id="405d3-626">![찾아보기 페이지에 대 한 링크를 사용 하 여 장르를 찾는](aspnet-mvc-4-fundamentals/_static/image33.png "찾아보기 페이지에 대 한 링크를 사용 하 여 장르 검색")</span><span class="sxs-lookup"><span data-stu-id="405d3-626">![Browsing Genres with links to Browse page](aspnet-mvc-4-fundamentals/_static/image33.png "Browsing Genres with links to Browse page")</span></span>

    <span data-ttu-id="405d3-627">*찾아보기 페이지에 대 한 링크를 사용 하 여 장르를 검색*</span><span class="sxs-lookup"><span data-stu-id="405d3-627">*Browsing Genres with links to Browse page*</span></span>

<a id="Ex6Task10"></a>

<a id="Task_10_-_Using_Dynamic_ViewModel_Collection_to_Pass_Values"></a>
#### <a name="task-10---using-dynamic-viewmodel-collection-to-pass-values"></a><span data-ttu-id="405d3-628">태스크 10-를 사용 하 여 동적 ViewModel 컬렉션 값 전달</span><span class="sxs-lookup"><span data-stu-id="405d3-628">Task 10 - Using Dynamic ViewModel Collection to Pass Values</span></span>

<span data-ttu-id="405d3-629">이 태스크에서는 모델에서 변경 하지 않고 컨트롤러와 뷰 간에 값을 전달 하는 단순 하면서도 강력한 메서드를 배우게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-629">In this task, you will learn a simple and powerful method to pass values between the Controller and the View without making any changes in the Model.</span></span> <span data-ttu-id="405d3-630">컬렉션을 제공 하는 ASP.NET MVC 4 &quot;ViewModel&quot;, 동적 값으로 할당 및 컨트롤러 및 보기도 내에서 액세스할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-630">ASP.NET MVC 4 provides the collection &quot;ViewModel&quot;, which can be assigned to any dynamic value and accessed inside controllers and views as well.</span></span>

<span data-ttu-id="405d3-631">이제 ViewBag 동적 컬렉션 목록을 전달 하는 데 사용할 &quot; **장르 별표 표시** &quot; 뷰 컨트롤러에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-631">You will now use the ViewBag dynamic collection to pass a list of &quot;**Starred genres**&quot; from the controller to the view.</span></span> <span data-ttu-id="405d3-632">저장소 인덱스 보기에 액세스 하는 **ViewModel** 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-632">The Store Index view will access to **ViewModel** and display the information.</span></span>

1. <span data-ttu-id="405d3-633">Visual Studio 창으로 돌아가려면 필요한 경우 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-633">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="405d3-634">오픈 **StoreController.cs** 수정할 **인덱스** 목록을 만드는 메서드를 ViewModel 컬렉션에 장르를 별표 표시:</span><span class="sxs-lookup"><span data-stu-id="405d3-634">Open **StoreController.cs** and modify **Index** method to create a list of starred genres into ViewModel collection :</span></span>

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample26.cs)]

    > [!NOTE]
    > <span data-ttu-id="405d3-635">구문을 사용할 수도 있습니다 **ViewBag [&quot;Starred&quot;]** 속성에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-635">You could also use the syntax **ViewBag[&quot;Starred&quot;]** to access the properties.</span></span>
2. <span data-ttu-id="405d3-636">별 모양 아이콘 **&quot;starred.png&quot;** 에 포함 되는 **Source\Assets\Images** 이 랩의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-636">The star icon **&quot;starred.png&quot;** is included in the **Source\Assets\Images** folder of this lab.</span></span> <span data-ttu-id="405d3-637">응용 프로그램을 추가 하려면 해당 콘텐츠를 끌어를 **Windows 탐색기** 창에는 **솔루션 탐색기** Visual Web Developer Express를 아래와 같이에서:</span><span class="sxs-lookup"><span data-stu-id="405d3-637">In order to add it to the application, drag their content from a **Windows Explorer** window into the **Solution Explorer** in Visual Web Developer Express, as shown below:</span></span>

    <span data-ttu-id="405d3-638">![솔루션 별 이미지 추가](aspnet-mvc-4-fundamentals/_static/image34.png "솔루션 별 이미지 추가")</span><span class="sxs-lookup"><span data-stu-id="405d3-638">![Adding star image to the solution](aspnet-mvc-4-fundamentals/_static/image34.png "Adding star image to the solution")</span></span>

    <span data-ttu-id="405d3-639">*솔루션 별 이미지 추가*</span><span class="sxs-lookup"><span data-stu-id="405d3-639">*Adding star image to the solution*</span></span>
3. <span data-ttu-id="405d3-640">보기를 엽니다 **Store/Index.cshtml** 및 콘텐츠를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-640">Open the view **Store/Index.cshtml** and modify the content.</span></span> <span data-ttu-id="405d3-641">읽기는 &quot;별표 표시&quot; 속성에는 **ViewBag** 컬렉션 현재 장르 이름이 목록에 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-641">You will read the &quot;starred&quot; property in the **ViewBag** collection, and ask if the current genre name is in the list.</span></span> <span data-ttu-id="405d3-642">이 경우 장르 링크를 오른쪽에서 별 모양 아이콘을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-642">In that case you will show a star icon right to the genre link.</span></span>
   <span data-ttu-id="405d3-643">(C#)</span><span class="sxs-lookup"><span data-stu-id="405d3-643">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample27.cshtml)]

<a id="Ex6Task11"></a>

<a id="Task_11_-_Running_the_Application"></a>
#### <a name="task-11---running-the-application"></a><span data-ttu-id="405d3-644">태스크 11-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="405d3-644">Task 11 - Running the Application</span></span>

<span data-ttu-id="405d3-645">이 태스크에서는 별점이 부여 된 장르 별 모양 아이콘 표시를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-645">In this task, you will test that the starred genres display a star icon.</span></span>

1. <span data-ttu-id="405d3-646">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-646">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="405d3-647">프로젝트에서 시작 합니다 **홈** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-647">The project starts in the **Home** page.</span></span> <span data-ttu-id="405d3-648">URL을 변경 **스토어** 주요 장르별로 respecting 레이블이 있는지 확인 하려면:</span><span class="sxs-lookup"><span data-stu-id="405d3-648">Change the URL to **/Store** to verify that each featured genre has the respecting label:</span></span>

    <span data-ttu-id="405d3-649">![별점이 부여 된 요소를 사용 하 여 장르를 찾는](aspnet-mvc-4-fundamentals/_static/image35.png "별점이 부여 된 요소를 사용 하 여 장르 검색")</span><span class="sxs-lookup"><span data-stu-id="405d3-649">![Browsing Genres with starred elements](aspnet-mvc-4-fundamentals/_static/image35.png "Browsing Genres with starred elements")</span></span>

    <span data-ttu-id="405d3-650">*별점이 부여 된 요소를 사용 하 여 장르를 검색*</span><span class="sxs-lookup"><span data-stu-id="405d3-650">*Browsing Genres with starred elements*</span></span>

<a id="Exercise7"></a>

<a id="Exercise_7_A_lap_around_ASPNET_MVC_4_new_template"></a>
### <a name="exercise-7-a-lap-around-aspnet-mvc-4-new-template"></a><span data-ttu-id="405d3-651">실습 7: ASP.NET MVC 4 새 템플릿 주위의 랩</span><span class="sxs-lookup"><span data-stu-id="405d3-651">Exercise 7: A lap around ASP.NET MVC 4 new template</span></span>

<span data-ttu-id="405d3-652">이 연습에서는 탐색에서 ASP.NET MVC 4 프로젝트 템플릿, 향상 된 기능 가장 관련 된 기능의 새 템플릿 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-652">In this exercise, you will explore the enhancements in the ASP.NET MVC 4 project templates, taking a look at the most relevant features of the new template.</span></span>

<a id="Ex7Task1"></a>

<a id="Task_1_Exploring_the_ASPNET_MVC_4_Internet_Application_Template"></a>
#### <a name="task-1-exploring-the-aspnet-mvc-4-internet-application-template"></a><span data-ttu-id="405d3-653">작업 1: ASP.NET MVC 4 인터넷 응용 프로그램 템플릿 탐색</span><span class="sxs-lookup"><span data-stu-id="405d3-653">Task 1: Exploring the ASP.NET MVC 4 Internet Application Template</span></span>

1. <span data-ttu-id="405d3-654">아직 열지 않은 경우 시작 **VS Express for Web**</span><span class="sxs-lookup"><span data-stu-id="405d3-654">If not already open, start **VS Express for Web**</span></span>
2. <span data-ttu-id="405d3-655">선택 된 **파일 | 새 | 프로젝트** 메뉴 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-655">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="405d3-656">에 **새 프로젝트** 대화 상자에서 선택 된 **Visual C# | 웹** 왼쪽된 창에서 템플릿을 선택한 트리의 합니다 **ASP.NET MVC 4 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-656">In the **New Project** dialog, select the **Visual C#|Web** template on the left pane tree, and choose the **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="405d3-657">**이름** 프로젝트 *MusicStore* 하 고 업데이트를 **솔루션 이름** 에 *시작*, 다음 위치를 선택 (또는 기본값을 그대로 두고) 클릭 하 고 **확인** .</span><span class="sxs-lookup"><span data-stu-id="405d3-657">**Name** the project *MusicStore* and update the **solution name** to *Begin*, then select a location (or leave the default) and click **OK**.</span></span>

    <span data-ttu-id="405d3-658">![새 ASP.NET MVC 4 프로젝트를 만드는](aspnet-mvc-4-fundamentals/_static/image36.png "새 ASP.NET MVC 4 프로젝트 만들기")</span><span class="sxs-lookup"><span data-stu-id="405d3-658">![Creating a new ASP.NET MVC 4 Project](aspnet-mvc-4-fundamentals/_static/image36.png "Creating a new ASP.NET MVC 4 Project")</span></span>

    <span data-ttu-id="405d3-659">*새 ASP.NET MVC 4 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="405d3-659">*Creating a new ASP.NET MVC 4 Project*</span></span>
3. <span data-ttu-id="405d3-660">에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 선택 합니다 **인터넷 응용 프로그램** 프로젝트 템플릿 및 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-660">In the **New ASP.NET MVC 4 Project** dialog, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="405d3-661">ASPX 또는 Razor 보기 엔진으로 선택할 수 있습니다를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-661">Notice you can select either Razor or ASPX as the view engine.</span></span>

    <span data-ttu-id="405d3-662">![새 ASP.NET MVC 4 인터넷 응용 프로그램을 만드는](aspnet-mvc-4-fundamentals/_static/image37.png "새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기")</span><span class="sxs-lookup"><span data-stu-id="405d3-662">![Creating a new ASP.NET MVC 4 Internet Application](aspnet-mvc-4-fundamentals/_static/image37.png "Creating a new ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="405d3-663">*새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기*</span><span class="sxs-lookup"><span data-stu-id="405d3-663">*Creating a new ASP.NET MVC 4 Internet Application*</span></span>

    > [!NOTE]
    > <span data-ttu-id="405d3-664">ASP.NET MVC 3에서 razor 구문이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-664">Razor syntax has been introduced in ASP.NET MVC 3.</span></span> <span data-ttu-id="405d3-665">해당 목표 문자와 유체 워크플로 코딩을 빠르게 사용 하도록 설정 하면 파일에 필요한 키 입력 횟수를 최소화 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-665">Its goal is to minimize the number of characters and keystrokes required in a file, enabling a fast and fluid coding workflow.</span></span> <span data-ttu-id="405d3-666">기존 C# /VB (또는 기타)을 활용 하는 razor 언어 실력 하 고 멋진 HTML 생성 워크플로 가능 하 게 하는 템플릿 태그 구문을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-666">Razor leverages existing C#/VB (or other) language skills and delivers a template markup syntax that enables an awesome HTML construction workflow.</span></span>
4. <span data-ttu-id="405d3-667">키를 눌러 **F5** 솔루션을 실행 하 여 갱신 된 템플릿을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="405d3-667">Press **F5** to run the solution and see the renewed template.</span></span> <span data-ttu-id="405d3-668">다음 기능을 사용해 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-668">You can check out the following features:</span></span>

    1. <span data-ttu-id="405d3-669">**최신 스타일 템플릿**</span><span class="sxs-lookup"><span data-stu-id="405d3-669">**Modern-style templates**</span></span>

        <span data-ttu-id="405d3-670">템플릿은 갱신 되 었어야, 더 많은 최신 스타일을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-670">The templates have been renewed, providing more modern-looking styles.</span></span>

        <span data-ttu-id="405d3-671">![ASP.NET MVC 4 맞게 스타일을 다시 템플릿을](aspnet-mvc-4-fundamentals/_static/image38.png "맞게 템플릿 스타일을 다시 ASP.NET MVC 4")</span><span class="sxs-lookup"><span data-stu-id="405d3-671">![ASP.NET MVC 4 restyled templates](aspnet-mvc-4-fundamentals/_static/image38.png "ASP.NET MVC 4 restyled templates")</span></span>

        <span data-ttu-id="405d3-672">*ASP.NET MVC 4 맞게 스타일을 다시 템플릿*</span><span class="sxs-lookup"><span data-stu-id="405d3-672">*ASP.NET MVC 4 restyled templates*</span></span>
    2. <span data-ttu-id="405d3-673">**적응형 렌더링**</span><span class="sxs-lookup"><span data-stu-id="405d3-673">**Adaptive Rendering**</span></span>

        <span data-ttu-id="405d3-674">브라우저 창의 크기를 조정 확인 하 고 페이지 레이아웃 새 창 크기를 동적으로 조정 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-674">Check out resizing the browser window and notice how the page layout dynamically adapts to the new window size.</span></span> <span data-ttu-id="405d3-675">이러한 템플릿은 적응형 렌더링 기술의 사용 하 여 사용자 지정 하지 않고 데스크톱 및 모바일 플랫폼에서 올바르게 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-675">These templates use the adaptive rendering technique to render properly in both desktop and mobile platforms without any customization.</span></span>

        <span data-ttu-id="405d3-676">![다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿은](aspnet-mvc-4-fundamentals/_static/image39.png "다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿")</span><span class="sxs-lookup"><span data-stu-id="405d3-676">![ASP.NET MVC 4 project template in different browser sizes](aspnet-mvc-4-fundamentals/_static/image39.png "ASP.NET MVC 4 project template in different browser sizes")</span></span>

        <span data-ttu-id="405d3-677">*다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿*</span><span class="sxs-lookup"><span data-stu-id="405d3-677">*ASP.NET MVC 4 project template in different browser sizes*</span></span>
5. <span data-ttu-id="405d3-678">디버거를 중지 하 고 Visual Studio로 돌아가서 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-678">Close the browser to stop the debugger and return to Visual Studio.</span></span>
6. <span data-ttu-id="405d3-679">이제 솔루션을 탐색 하 고 일부의 프로젝트 템플릿에서 ASP.NET MVC 4에서 도입 된 새로운 기능 확인 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-679">Now you are able to explore the solution and check out some of the new features introduced by ASP.NET MVC 4 in the project template.</span></span>

    <span data-ttu-id="405d3-680">![ASP.NET mvc 4-인터넷-응용 프로그램-프로젝트-템플릿을](aspnet-mvc-4-fundamentals/_static/image40.png "ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿")</span><span class="sxs-lookup"><span data-stu-id="405d3-680">![ASP.NET MVC4-internet-application-project-template](aspnet-mvc-4-fundamentals/_static/image40.png "The ASP.NET MVC 4 Internet Application Project Template")</span></span>

    <span data-ttu-id="405d3-681">*ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿*</span><span class="sxs-lookup"><span data-stu-id="405d3-681">*The ASP.NET MVC 4 Internet Application Project Template*</span></span>

   1. <span data-ttu-id="405d3-682">**HTML5 태그**</span><span class="sxs-lookup"><span data-stu-id="405d3-682">**HTML5 markup**</span></span>

       <span data-ttu-id="405d3-683">예를 들어 열린 새 테마 태그를 확인 하려면 템플릿 보기 찾아보기 **About.cshtml** 내에서 보려면 **홈** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-683">Browse template views to find out the new theme markup, for example open **About.cshtml** view within **Home** folder.</span></span>

       <span data-ttu-id="405d3-684">![HTML5 및 Razor 태그를 사용 하 여 새 템플릿을](aspnet-mvc-4-fundamentals/_static/image41.png "HTML5 및 Razor 태그를 사용 하 여 새 템플릿")</span><span class="sxs-lookup"><span data-stu-id="405d3-684">![New template, using Razor and HTML5 markup](aspnet-mvc-4-fundamentals/_static/image41.png "New template, using Razor and HTML5 markup")</span></span>

       <span data-ttu-id="405d3-685">*HTML5 및 Razor 태그를 사용 하 여 새 템플릿*</span><span class="sxs-lookup"><span data-stu-id="405d3-685">*New template, using Razor and HTML5 markup*</span></span>
   2. <span data-ttu-id="405d3-686">**JavaScript 라이브러리가 포함**</span><span class="sxs-lookup"><span data-stu-id="405d3-686">**JavaScript libraries included**</span></span>

      1. <span data-ttu-id="405d3-687">**jQuery**: jQuery HTML 문서 통과, 이벤트 처리, 애니메이션 효과 적용, 및 Ajax 상호 작용을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-687">**jQuery**: jQuery simplifies HTML document traversing, event handling, animating, and Ajax interactions.</span></span>
      2. <span data-ttu-id="405d3-688">**jQuery UI**:이 라이브러리는 낮은 수준의 상호 작용 및 애니메이션 효과 고급 themeable widgets, jQuery JavaScript 라이브러리를 기반으로 구축 된 추상화를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-688">**jQuery UI**: This library provides abstractions for low-level interaction and animation, advanced effects and themeable widgets, built on top of the jQuery JavaScript Library.</span></span>

         > [!NOTE]
         > <span data-ttu-id="405d3-689">JQuery 및 jQuery UI 알아볼 수 있습니다에 [ [ http://docs.jquery.com/ ](http://docs.jquery.com/) ](http://docs.jquery.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-689">You can learn about jQuery and jQuery UI in [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span></span>
      3. <span data-ttu-id="405d3-690">**KnockoutJS**: 이제는 ASP.NET MVC 4 기본 템플릿을 **KnockoutJS**, JavaScript 및 HTML을 사용 하 여 풍부 하 고 응답성이 뛰어난 웹 응용 프로그램을 만들 수 있는 JavaScript MVVM 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-690">**KnockoutJS**: The ASP.NET MVC 4 default template now includes **KnockoutJS**, a JavaScript MVVM framework that lets you create rich and highly responsive web applications using JavaScript and HTML.</span></span> <span data-ttu-id="405d3-691">같은 ASP.NET MVC 3, jQuery 및 jQuery UI 라이브러리도 포함 되어 ASP.NET MVC 4입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-691">Like in ASP.NET MVC 3, jQuery and jQuery UI libraries are also included in ASP.NET MVC 4.</span></span>

          > [!NOTE]
          > <span data-ttu-id="405d3-692">이 링크에 KnockOutJS 라이브러리에 대 한 자세한 정보를 얻을 수 있습니다: [ http://learn.knockoutjs.com/ ](http://learn.knockoutjs.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-692">You can get more information about KnockOutJS library in this link: [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/).</span></span>
      4. <span data-ttu-id="405d3-693">**Modernizr**: HTML5 및 CSS3 기술을 사용 하는 경우 사이트를 이전 버전의 브라우저와 호환 하이 라이브러리를 자동으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-693">**Modernizr**: This library runs automatically, making your site compatible with older browsers when using HTML5 and CSS3 technologies.</span></span>

          > [!NOTE]
          > <span data-ttu-id="405d3-694">이 링크에 Modernizr 라이브러리에 대 한 자세한 정보를 얻을 수 있습니다: [ http://www.modernizr.com/ ](http://www.modernizr.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-694">You can get more information about Modernizr library in this link: [http://www.modernizr.com/](http://www.modernizr.com/).</span></span>
   3. <span data-ttu-id="405d3-695">**SimpleMembership 솔루션에 포함**</span><span class="sxs-lookup"><span data-stu-id="405d3-695">**SimpleMembership included in the solution**</span></span>

       <span data-ttu-id="405d3-696">이전 ASP.NET 역할 및 멤버 자격 공급자 시스템의 대체로 SimpleMembership 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-696">SimpleMembership has been designed as a replacement for the previous ASP.NET Role and Membership provider system.</span></span> <span data-ttu-id="405d3-697">쉽게 보안 웹 페이지 개발자를 위한 더 유연 하 게에서 하는 여러 가지 새로운 기능에</span><span class="sxs-lookup"><span data-stu-id="405d3-697">It has many new features that make it easier for the developer to secure web pages in a more flexible way.</span></span>

       <span data-ttu-id="405d3-698">인터넷 템플릿은 이미 설정한 SimpleMembership를 통합 하는 몇 가지, OAuthWebSecurity (에 대 한 OAuth 계정 등록, 로그인, 관리, 등) 및 웹 보안을 사용 하는 AccountController 준비 되는 예를 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-698">The Internet template already has set up a few things to integrate SimpleMembership, for example, the AccountController is prepared to use OAuthWebSecurity (for OAuth account registration, login, management, etc.) and Web Security.</span></span>

       <span data-ttu-id="405d3-699">![솔루션에 포함 된 SimpleMembership](aspnet-mvc-4-fundamentals/_static/image42.png "SimpleMembership 솔루션에 포함")</span><span class="sxs-lookup"><span data-stu-id="405d3-699">![SimpleMembership Included in the solution](aspnet-mvc-4-fundamentals/_static/image42.png "SimpleMembership Included in the solution")</span></span>

       <span data-ttu-id="405d3-700">*SimpleMembership 솔루션에 포함*</span><span class="sxs-lookup"><span data-stu-id="405d3-700">*SimpleMembership Included in the solution*</span></span>

       > [!NOTE]
       > <span data-ttu-id="405d3-701">에 대 한 자세한 정보를 찾을 [OAuthWebSecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) MSDN에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-701">Find more information about [OAuthWebSecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) in MSDN.</span></span>

> [!NOTE]
> <span data-ttu-id="405d3-702">또한 다음 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수 있습니다 [부록 b: 게시 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램](#AppendixB)합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-702">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>


* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="405d3-703">요약</span><span class="sxs-lookup"><span data-stu-id="405d3-703">Summary</span></span>

<span data-ttu-id="405d3-704">이 실습을 완료 하 여 ASP.NET MVC의 기본 사항을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-704">By completing this Hands-On Lab you have learned the fundamentals of ASP.NET MVC:</span></span>

- <span data-ttu-id="405d3-705">MVC 응용 프로그램 및 이들이 어떻게 상호 작용의 핵심 요소</span><span class="sxs-lookup"><span data-stu-id="405d3-705">The core elements of an MVC application and how they interact</span></span>
- <span data-ttu-id="405d3-706">ASP.NET MVC 응용 프로그램을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="405d3-706">How to create an ASP.NET MVC Application</span></span>
- <span data-ttu-id="405d3-707">URL 및 쿼리 문자열을 통해 전달 된 추가 하 고 매개 변수를 처리 하는 컨트롤러를 구성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="405d3-707">How to add and configure Controllers to handle parameters passed through the URL and querystring</span></span>
- <span data-ttu-id="405d3-708">공통 HTML 콘텐츠, 모양 및 느낌 및 HTML 콘텐츠를 표시 하려면 보기 템플릿을 개선 하는 스타일 시트에 대 한 템플릿을 설정 하는 레이아웃 마스터 페이지를 추가 하는 방법</span><span class="sxs-lookup"><span data-stu-id="405d3-708">How to add a layout master page to setup a template for common HTML content, a StyleSheet to enhance the look and feel and a View template to display HTML content</span></span>
- <span data-ttu-id="405d3-709">동적 정보를 표시 하려면 템플릿 보기에 속성을 전달 하는 것에 대 한 ViewModel 패턴을 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="405d3-709">How to use the ViewModel pattern for passing properties to the View template to display dynamic information</span></span>
- <span data-ttu-id="405d3-710">보기 템플릿은 컨트롤러에 전달 된 매개 변수를 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="405d3-710">How to use parameters passed to Controllers in the View template</span></span>
- <span data-ttu-id="405d3-711">ASP.NET MVC 응용 프로그램 내에서 페이지에 대 한 링크를 추가 하는 방법</span><span class="sxs-lookup"><span data-stu-id="405d3-711">How to add links to pages inside the ASP.NET MVC application</span></span>
- <span data-ttu-id="405d3-712">추가 보기에서 동적 속성을 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="405d3-712">How to add and use dynamic properties in a View</span></span>
- <span data-ttu-id="405d3-713">ASP.NET MVC 4 프로젝트 템플릿에서 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="405d3-713">The enhancements in the ASP.NET MVC 4 project templates</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="405d3-714">부록 a: 설치 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="405d3-714">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="405d3-715">설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 사용 하 여 버전을 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="405d3-715">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="405d3-716">다음 지침을 설치 하는 데 필요한 단계를 안내 *Visual studio Express 2012 for Web* 사용 하 여 *Microsoft Web Platform Installer*합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-716">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="405d3-717">로 이동 [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-717">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="405d3-718">또는, 이미 설치한 경우 웹 플랫폼 설치 관리자를 열 수 있습니다 하 고 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Windows Azure SDK를 사용 하 여 Web</em>&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-718">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="405d3-719">클릭할 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-719">Click on **Install Now**.</span></span> <span data-ttu-id="405d3-720">없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-720">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="405d3-721">한 번 **웹 플랫폼 설치 관리자** 열려 있는 경우 클릭 **설치** 는 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-721">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="405d3-722">![Visual Studio Express를 설치](aspnet-mvc-4-fundamentals/_static/image43.png "Visual Studio Express를 설치 합니다.")</span><span class="sxs-lookup"><span data-stu-id="405d3-722">![Install Visual Studio Express](aspnet-mvc-4-fundamentals/_static/image43.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="405d3-723">*Visual Studio Express를 설치 합니다.*</span><span class="sxs-lookup"><span data-stu-id="405d3-723">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="405d3-724">모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-724">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건에 동의](aspnet-mvc-4-fundamentals/_static/image44.png)

    <span data-ttu-id="405d3-726">*사용 조건에 동의*</span><span class="sxs-lookup"><span data-stu-id="405d3-726">*Accepting the license terms*</span></span>
5. <span data-ttu-id="405d3-727">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-727">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](aspnet-mvc-4-fundamentals/_static/image45.png)

    <span data-ttu-id="405d3-729">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="405d3-729">*Installation progress*</span></span>
6. <span data-ttu-id="405d3-730">설치가 완료 되 면 클릭 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-730">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](aspnet-mvc-4-fundamentals/_static/image46.png)

    <span data-ttu-id="405d3-732">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="405d3-732">*Installation completed*</span></span>
7. <span data-ttu-id="405d3-733">클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-733">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="405d3-734">로 Visual Studio Express for Web을 열려면 합니다 **시작** 화면 및 쓰기를 시작 &quot; **VS Express**&quot;를 클릭 합니다 **VS Express for Web** 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-734">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 타일](aspnet-mvc-4-fundamentals/_static/image47.png)

    <span data-ttu-id="405d3-736">*VS Express for Web 타일*</span><span class="sxs-lookup"><span data-stu-id="405d3-736">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="405d3-737">부록 b: 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="405d3-737">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="405d3-738">이 부록은 Windows Azure 관리 포털에서 새 웹 사이트를 만들고 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하 고 랩에 따라 얻은 응용 프로그램을 게시 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-738">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="405d3-739">작업 1-Windows에서 새 웹 사이트를 만드는 Azure Portal</span><span class="sxs-lookup"><span data-stu-id="405d3-739">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="405d3-740">로 이동 합니다 [Windows Azure 관리 포털](https://manage.windowsazure.com/) 구독과 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-740">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="405d3-741">Windows Azure를 사용 하 여 10 개의 ASP.NET 웹 사이트를 무료로 호스트할 수 있으며 다음 트래픽 증가 따라 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-741">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="405d3-742">등록할 수 있습니다 [여기](http://aka.ms/aspnet-hol-azure)합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-742">You can sign up [here](http://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="405d3-743">![Windows Azure 포털에 로그온](aspnet-mvc-4-fundamentals/_static/image48.png "Windows Azure 포털에 로그온")</span><span class="sxs-lookup"><span data-stu-id="405d3-743">![Log on to Windows Azure portal](aspnet-mvc-4-fundamentals/_static/image48.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="405d3-744">*Windows Azure 관리 포털에 로그온*</span><span class="sxs-lookup"><span data-stu-id="405d3-744">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="405d3-745">클릭 **새로 만들기** 명령 모음에서.</span><span class="sxs-lookup"><span data-stu-id="405d3-745">Click **New** on the command bar.</span></span>

    <span data-ttu-id="405d3-746">![새 웹 사이트를 만드는](aspnet-mvc-4-fundamentals/_static/image49.png "새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="405d3-746">![Creating a new Web Site](aspnet-mvc-4-fundamentals/_static/image49.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="405d3-747">*새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="405d3-747">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="405d3-748">클릭 **계산** | **웹 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-748">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="405d3-749">선택한 **빨리 만들기** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-749">Then select **Quick Create** option.</span></span> <span data-ttu-id="405d3-750">새 웹 사이트를 사용할 수 있는 URL을 제공 하 고 클릭 **웹 사이트 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-750">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="405d3-751">Windows Azure 웹 사이트는 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램에 대 한 호스트.</span><span class="sxs-lookup"><span data-stu-id="405d3-751">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="405d3-752">빠른 생성 옵션을 사용 하면 완료 된 웹 응용 프로그램을 Windows Azure에서 웹 사이트 포털 외부에서 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-752">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="405d3-753">데이터베이스를 설정 하기 위한 단계는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-753">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="405d3-754">![빠른 생성을 사용 하 여 새 웹 사이트를 만드는](aspnet-mvc-4-fundamentals/_static/image50.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="405d3-754">![Creating a new Web Site using Quick Create](aspnet-mvc-4-fundamentals/_static/image50.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="405d3-755">*빠른 생성을 사용 하 여 새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="405d3-755">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="405d3-756">새 될 때까지 기다렸다가 **웹 사이트** 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-756">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="405d3-757">웹 사이트를 만든 후 아래의 링크를 클릭 합니다 **URL** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-757">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="405d3-758">새 웹 사이트가 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-758">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="405d3-759">![새 웹 사이트를 찾아](aspnet-mvc-4-fundamentals/_static/image51.png "새 웹 사이트를 검색 합니다.")</span><span class="sxs-lookup"><span data-stu-id="405d3-759">![Browsing to the new web site](aspnet-mvc-4-fundamentals/_static/image51.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="405d3-760">*새 웹 사이트를 검색합니다.*</span><span class="sxs-lookup"><span data-stu-id="405d3-760">*Browsing to the new web site*</span></span>

    <span data-ttu-id="405d3-761">![실행 중인 웹 사이트](aspnet-mvc-4-fundamentals/_static/image52.png "실행 중인 웹 사이트")</span><span class="sxs-lookup"><span data-stu-id="405d3-761">![Web site running](aspnet-mvc-4-fundamentals/_static/image52.png "Web site running")</span></span>

    <span data-ttu-id="405d3-762">*실행 중인 웹 사이트*</span><span class="sxs-lookup"><span data-stu-id="405d3-762">*Web site running*</span></span>
6. <span data-ttu-id="405d3-763">포털로 돌아가서에서 웹 사이트의 이름을 클릭 합니다 **이름을** 관리 페이지를 표시 하는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-763">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="405d3-764">![웹 사이트 관리 페이지를 열어](aspnet-mvc-4-fundamentals/_static/image53.png "웹 사이트 관리 페이지 열기")</span><span class="sxs-lookup"><span data-stu-id="405d3-764">![Opening the web site management pages](aspnet-mvc-4-fundamentals/_static/image53.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="405d3-765">*웹 사이트 관리 페이지 열기*</span><span class="sxs-lookup"><span data-stu-id="405d3-765">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="405d3-766">**대시보드** 페이지의 **간략 상태** 섹션을 클릭 합니다 **게시 프로필 다운로드** 링크.</span><span class="sxs-lookup"><span data-stu-id="405d3-766">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="405d3-767">합니다 *게시 프로필* 모든 각각의 설정 된 게시 방법에 대 한 Windows Azure 웹 사이트를 웹 응용 프로그램을 게시 하는 데 필요한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-767">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="405d3-768">게시 프로필에는 Url, 사용자 자격 증명 및 연결 하 고 각 게시 메서드를 사용할 수 있는 끝점에 대해 인증 하는 데 필요한 데이터베이스 문자열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-768">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="405d3-769">**Microsoft WebMatrix 2**하십시오 **Microsoft Visual Studio Express for Web** 하 고 **Microsoft Visual Studio 2012** 읽기 지원 하기 위해 게시 프로필에 대 한 이러한 프로그램의 구성을 자동화할 Windows Azure websites에 웹 응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-769">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="405d3-770">![게시 프로필 다운로드 웹 사이트](aspnet-mvc-4-fundamentals/_static/image54.png "게시 프로필 다운로드 웹 사이트")</span><span class="sxs-lookup"><span data-stu-id="405d3-770">![Downloading the web site publish profile](aspnet-mvc-4-fundamentals/_static/image54.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="405d3-771">*게시 프로필 다운로드 웹 사이트*</span><span class="sxs-lookup"><span data-stu-id="405d3-771">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="405d3-772">알려진된 위치에 게시 프로필 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-772">Download the publish profile file to a known location.</span></span> <span data-ttu-id="405d3-773">추가이 연습에서이 파일을 사용 하 여 Visual Studio에서 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하는 방법을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-773">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="405d3-774">![게시 프로필 파일을 저장](aspnet-mvc-4-fundamentals/_static/image55.png "게시 프로필 저장")</span><span class="sxs-lookup"><span data-stu-id="405d3-774">![Saving the publish profile file](aspnet-mvc-4-fundamentals/_static/image55.png "Saving the publish profile")</span></span>

    <span data-ttu-id="405d3-775">*게시 프로필 파일을 저장 하는 중*</span><span class="sxs-lookup"><span data-stu-id="405d3-775">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="405d3-776">작업 2-데이터베이스 서버 구성</span><span class="sxs-lookup"><span data-stu-id="405d3-776">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="405d3-777">응용 프로그램에서 SQL 서버를 사용할 경우 데이터베이스를 SQL Database 서버 만들기 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-777">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="405d3-778">SQL Server를 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-778">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="405d3-779">응용 프로그램 데이터베이스를 저장 하는 것에 대 한 SQL Database 서버를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-779">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="405d3-780">Windows Azure 관리 포털에서 구독의 SQL Database 서버를 볼 수 있습니다 **Sql Database** | **서버** | **서버 대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-780">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="405d3-781">만든 서버가 없는 경우 하나를 사용 하 여 만들 수 있습니다 합니다 **추가** 명령 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-781">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="405d3-782">기록해는 **서버 이름 및 URL, 관리자 로그인 이름 및 암호**처럼 다음 작업에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-782">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="405d3-783">만들지 마십시오 데이터베이스 아직 이후 단계에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-783">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="405d3-784">![SQL Database 서버 대시보드](aspnet-mvc-4-fundamentals/_static/image56.png "SQL Database 서버 대시보드")</span><span class="sxs-lookup"><span data-stu-id="405d3-784">![SQL Database Server Dashboard](aspnet-mvc-4-fundamentals/_static/image56.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="405d3-785">*SQL Database 서버 대시보드*</span><span class="sxs-lookup"><span data-stu-id="405d3-785">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="405d3-786">다음 태스크에서는 테스트 Visual Studio에서 데이터베이스 연결 서버 목록에 로컬 IP 주소를 포함 해야 하는 이유로 **허용 된 IP 주소**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-786">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="405d3-787">이렇게 하려면 클릭 **구성**에서 IP 주소를 선택 **현재 클라이언트 IP 주소** 에 붙여 넣습니다 합니다 **시작 IP 주소** 및 **끝IP주소** 입력란을 클릭 합니다 ![add-client-ip-address-ok-button](aspnet-mvc-4-fundamentals/_static/image57.png) 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-787">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-fundamentals/_static/image57.png) button.</span></span>

    ![클라이언트 IP 주소를 추가합니다.](aspnet-mvc-4-fundamentals/_static/image58.png)

    <span data-ttu-id="405d3-789">*클라이언트 IP 주소를 추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="405d3-789">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="405d3-790">한 번 합니다 **클라이언트 IP 주소** 허용 된 IP 주소에 추가 됩니다 목록에서 클릭 **저장** 변경을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-790">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![변경 확인](aspnet-mvc-4-fundamentals/_static/image59.png)

    <span data-ttu-id="405d3-792">*변경 확인*</span><span class="sxs-lookup"><span data-stu-id="405d3-792">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="405d3-793">작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="405d3-793">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="405d3-794">ASP.NET MVC 4 솔루션 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-794">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="405d3-795">에 **솔루션 탐색기**, 웹 사이트 프로젝트를 마우스 오른쪽 단추로 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-795">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="405d3-796">![응용 프로그램 게시](aspnet-mvc-4-fundamentals/_static/image60.png "응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="405d3-796">![Publishing the Application](aspnet-mvc-4-fundamentals/_static/image60.png "Publishing the Application")</span></span>

    <span data-ttu-id="405d3-797">*웹 사이트를 게시합니다.*</span><span class="sxs-lookup"><span data-stu-id="405d3-797">*Publishing the web site*</span></span>
2. <span data-ttu-id="405d3-798">첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-798">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="405d3-799">![게시 프로필 가져오기](aspnet-mvc-4-fundamentals/_static/image61.png "게시 프로필 가져오기")</span><span class="sxs-lookup"><span data-stu-id="405d3-799">![Importing the publish profile](aspnet-mvc-4-fundamentals/_static/image61.png "Importing the publish profile")</span></span>

    <span data-ttu-id="405d3-800">*게시 프로필 가져오기*</span><span class="sxs-lookup"><span data-stu-id="405d3-800">*Importing publish profile*</span></span>
3. <span data-ttu-id="405d3-801">클릭 **연결의 유효성을 검사**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-801">Click **Validate Connection**.</span></span> <span data-ttu-id="405d3-802">유효성 검사가 완료 되 면 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-802">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="405d3-803">연결 유효성 검사 단추 옆에 나타나는 녹색 확인 표시가 표시 되 면 유효성 검사가 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-803">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="405d3-804">![연결 유효성 검사](aspnet-mvc-4-fundamentals/_static/image62.png "연결 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="405d3-804">![Validating connection](aspnet-mvc-4-fundamentals/_static/image62.png "Validating connection")</span></span>

    <span data-ttu-id="405d3-805">*연결 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="405d3-805">*Validating connection*</span></span>
4. <span data-ttu-id="405d3-806">에 **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆의 단추를 클릭 (즉 **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="405d3-806">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="405d3-807">![웹 배포 구성](aspnet-mvc-4-fundamentals/_static/image63.png "웹 배포 구성")</span><span class="sxs-lookup"><span data-stu-id="405d3-807">![Web deploy configuration](aspnet-mvc-4-fundamentals/_static/image63.png "Web deploy configuration")</span></span>

    <span data-ttu-id="405d3-808">*웹 배포 구성*</span><span class="sxs-lookup"><span data-stu-id="405d3-808">*Web deploy configuration*</span></span>
5. <span data-ttu-id="405d3-809">데이터베이스 연결을 다음과 같이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-809">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="405d3-810">에 **서버 이름** SQL Database 서버 URL 사용 하 여 입력 합니다 *tcp:* 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-810">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="405d3-811">**사용자 이름** 서버 관리자 로그인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-811">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="405d3-812">**암호** 서버 관리자 로그인 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-812">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="405d3-813">예를 들어 새 데이터베이스 이름을 입력 합니다. *MVC4SampleDB*합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-813">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="405d3-814">![대상 연결 문자열 구성](aspnet-mvc-4-fundamentals/_static/image64.png "대상 연결 문자열 구성")</span><span class="sxs-lookup"><span data-stu-id="405d3-814">![Configuring destination connection string](aspnet-mvc-4-fundamentals/_static/image64.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="405d3-815">*대상 연결 문자열 구성*</span><span class="sxs-lookup"><span data-stu-id="405d3-815">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="405d3-816">그런 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-816">Then click **OK**.</span></span> <span data-ttu-id="405d3-817">데이터베이스를 만들라는 메시지가 나오면 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-817">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="405d3-818">![데이터베이스를 만드는](aspnet-mvc-4-fundamentals/_static/image65.png "데이터베이스 문자열 만들기")</span><span class="sxs-lookup"><span data-stu-id="405d3-818">![Creating the database](aspnet-mvc-4-fundamentals/_static/image65.png "Creating the database string")</span></span>

    <span data-ttu-id="405d3-819">*데이터베이스 만들기*</span><span class="sxs-lookup"><span data-stu-id="405d3-819">*Creating the database*</span></span>
7. <span data-ttu-id="405d3-820">기본 연결 텍스트 상자 내에서 사용 하 여 Windows Azure에서 SQL Database에 연결 하는 연결 문자열 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-820">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="405d3-821">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-821">Then click **Next**.</span></span>

    <span data-ttu-id="405d3-822">![SQL Database를 가리키는 연결 문자열](aspnet-mvc-4-fundamentals/_static/image66.png "SQL 데이터베이스를 가리키는 연결 문자열")</span><span class="sxs-lookup"><span data-stu-id="405d3-822">![Connection string pointing to SQL Database](aspnet-mvc-4-fundamentals/_static/image66.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="405d3-823">*SQL Database를 가리키는 연결 문자열*</span><span class="sxs-lookup"><span data-stu-id="405d3-823">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="405d3-824">에 **미리 보기** 페이지에서 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-824">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="405d3-825">![웹 응용 프로그램 게시](aspnet-mvc-4-fundamentals/_static/image67.png "웹 응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="405d3-825">![Publishing the web application](aspnet-mvc-4-fundamentals/_static/image67.png "Publishing the web application")</span></span>

    <span data-ttu-id="405d3-826">*웹 응용 프로그램 게시*</span><span class="sxs-lookup"><span data-stu-id="405d3-826">*Publishing the web application*</span></span>
9. <span data-ttu-id="405d3-827">게시 프로세스가 완료 되 면 게시 된 웹 사이트 기본 브라우저가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-827">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="405d3-828">![Windows Azure에 응용 프로그램 게시](aspnet-mvc-4-fundamentals/_static/image68.png "응용 프로그램이 Windows Azure에 게시")</span><span class="sxs-lookup"><span data-stu-id="405d3-828">![Application published to Windows Azure](aspnet-mvc-4-fundamentals/_static/image68.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="405d3-829">*Windows Azure에 게시 하는 응용 프로그램*</span><span class="sxs-lookup"><span data-stu-id="405d3-829">*Application published to Windows Azure*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="405d3-830">부록 c: 코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="405d3-830">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="405d3-831">코드 조각을 사용 하 여 결정적인 순간에 필요한 모든 코드를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-831">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="405d3-832">랩 문서가 알려줍니다 정확 하 게 사용할 수 있는 시기를 다음 그림과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-832">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="405d3-833">![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드를 삽입할](aspnet-mvc-4-fundamentals/_static/image69.png "프로젝트에 코드를 삽입 하는 Visual Studio를 사용 하 여 코드 조각을")</span><span class="sxs-lookup"><span data-stu-id="405d3-833">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-fundamentals/_static/image69.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="405d3-834">*프로젝트에 코드를 삽입 하려면 Visual Studio 코드 조각 사용*</span><span class="sxs-lookup"><span data-stu-id="405d3-834">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="405d3-835">***키보드 (C#만 해당)를 사용 하 여 코드 조각을 추가 하려면***</span><span class="sxs-lookup"><span data-stu-id="405d3-835">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="405d3-836">코드를 삽입 하려는 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-836">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="405d3-837">시작 (공백 없이 하이픈) 조각 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-837">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="405d3-838">IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-838">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="405d3-839">올바른 코드 조각을 선택 합니다 (또는 전체 코드 조각 이름을 선택 될 때까지 입력 유지).</span><span class="sxs-lookup"><span data-stu-id="405d3-839">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="405d3-840">커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-840">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="405d3-841">![코드 조각 이름을 입력](aspnet-mvc-4-fundamentals/_static/image70.png "조각 이름을 입력 하기 시작")</span><span class="sxs-lookup"><span data-stu-id="405d3-841">![Start typing the snippet name](aspnet-mvc-4-fundamentals/_static/image70.png "Start typing the snippet name")</span></span>

<span data-ttu-id="405d3-842">*코드 조각 이름을 입력 하기 시작*</span><span class="sxs-lookup"><span data-stu-id="405d3-842">*Start typing the snippet name*</span></span>

<span data-ttu-id="405d3-843">![Tab 키를 눌러 강조 표시 된 코드 조각을](aspnet-mvc-4-fundamentals/_static/image71.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")</span><span class="sxs-lookup"><span data-stu-id="405d3-843">![Press Tab to select the highlighted snippet](aspnet-mvc-4-fundamentals/_static/image71.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="405d3-844">*Tab 키를 눌러 강조 표시 된 코드 조각 선택*</span><span class="sxs-lookup"><span data-stu-id="405d3-844">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="405d3-845">![Tab 키를 다시 코드 조각 확장 됩니다](aspnet-mvc-4-fundamentals/_static/image72.png "다시 Tab 키를 누릅니다 하 고 코드 조각에서는 확장")</span><span class="sxs-lookup"><span data-stu-id="405d3-845">![Press Tab again and the snippet will expand](aspnet-mvc-4-fundamentals/_static/image72.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="405d3-846">*Tab 키를 다시 및 코드 조각에서는 확장*</span><span class="sxs-lookup"><span data-stu-id="405d3-846">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="405d3-847">***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가할*** 1입니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-847">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="405d3-848">코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-848">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="405d3-849">선택 **코드 조각 삽입** 뒤 **내 코드 조각**합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-849">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="405d3-850">클릭 하 여 목록에서 관련 코드 조각을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="405d3-850">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="405d3-851">![코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭](aspnet-mvc-4-fundamentals/_static/image73.png "코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭")</span><span class="sxs-lookup"><span data-stu-id="405d3-851">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-fundamentals/_static/image73.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="405d3-852">*코드 조각을 삽입할 선택한 코드 조각 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭*</span><span class="sxs-lookup"><span data-stu-id="405d3-852">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="405d3-853">![클릭 하 여 목록에서 관련 코드 조각 선택](aspnet-mvc-4-fundamentals/_static/image74.png "클릭 하 여 목록에서 관련 코드 조각 선택")</span><span class="sxs-lookup"><span data-stu-id="405d3-853">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-fundamentals/_static/image74.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="405d3-854">*클릭 하 여 목록에서 관련 코드 조각 선택*</span><span class="sxs-lookup"><span data-stu-id="405d3-854">*Pick the relevant snippet from the list, by clicking on it*</span></span>
