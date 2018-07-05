---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
title: '반복 #1 – (VB) 응용 프로그램 만들기 | Microsoft Docs'
author: microsoft
description: '첫 번째 반복에서 연락처 관리자에서에서 만드는 가장 간단한 방법은 가능 합니다. 기본 데이터베이스 작업에 대 한 지원 추가: 만들기, 읽기, 업데이트 및 D....'
ms.author: aspnetcontent
ms.date: 02/20/2009
ms.assetid: 5b033582-1646-42c2-b20d-7edc8814e970
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
msc.type: authoredcontent
ms.openlocfilehash: aee177164293c178fa7d2d4acfb60f85dc98bb05
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37803008"
---
<a name="iteration-1--create-the-application-vb"></a><span data-ttu-id="3b182-104">반복 #1 – (VB) 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="3b182-104">Iteration #1 – Create the Application (VB)</span></span>
====================
<span data-ttu-id="3b182-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="3b182-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="3b182-106">코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="3b182-106">Download Code</span></span>](iteration-1-create-the-application-vb/_static/contactmanager_1_vb1.zip)

> <span data-ttu-id="3b182-107">첫 번째 반복에서 연락처 관리자에서에서 만드는 가장 간단한 방법은 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-107">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="3b182-108">기본 데이터베이스 작업에 대 한 지원 추가: 만들기, 읽기, 업데이트 및 삭제 (CRUD).</span><span class="sxs-lookup"><span data-stu-id="3b182-108">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a><span data-ttu-id="3b182-109">연락처 관리 ASP.NET MVC 응용 프로그램을 작성 (VB)</span><span class="sxs-lookup"><span data-stu-id="3b182-109">Building a Contact Management ASP.NET MVC Application (VB)</span></span>

<span data-ttu-id="3b182-110">이 시리즈의 자습서에서 전체 연락처 관리 응용을 프로그램 시작부터 완료를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-110">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="3b182-111">연락처 관리자 응용 프로그램에 사용자의 목록을 포함 된 상점 연락처 정보-이름, 전화 번호 및 전자 메일 주소-할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-111">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="3b182-112">여러 반복에 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-112">We build the application over multiple iterations.</span></span> <span data-ttu-id="3b182-113">각 반복에서 점진적으로 응용 프로그램을 개선 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-113">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="3b182-114">이렇게 여러 반복의 목표는 각 변경의 이유를 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-114">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="3b182-115">반복 #1-응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-115">Iteration #1 - Create the application.</span></span> <span data-ttu-id="3b182-116">첫 번째 반복에서 연락처 관리자에서에서 만드는 가장 간단한 방법은 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-116">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="3b182-117">기본 데이터베이스 작업에 대 한 지원 추가: 만들기, 읽기, 업데이트 및 삭제 (CRUD).</span><span class="sxs-lookup"><span data-stu-id="3b182-117">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="3b182-118">반복 #2-보기 좋게 응용 프로그램을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-118">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="3b182-119">이 반복에서 기본 ASP.NET MVC 보기 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-119">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="3b182-120">반복 #3-양식 유효성 검사를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-120">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="3b182-121">세 번째 반복에서는 기본 양식 유효성 검사를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-121">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="3b182-122">사용자를 방지할 수를 필요한 형식의 필드를 완료 하지 않고 폼을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-122">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="3b182-123">또한 전자 메일 주소 및 전화 번호 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-123">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="3b182-124">반복 #4-느슨하게 결합 된 응용 프로그램을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-124">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="3b182-125">이 세 번째 반복에서는 활용 쉽게 유지 관리 하 고 연락처 관리자 응용 프로그램을 수정 하려면 몇 가지 소프트웨어 디자인 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-125">In this third iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="3b182-126">예를 들어, 리포지토리 패턴 및 종속성 주입 패턴을 사용 하 여 응용 프로그램을 리팩터링 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-126">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="3b182-127">반복 #5-단위 테스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-127">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="3b182-128">다섯 번째 반복에서에서는 쉽게 응용 프로그램 유지 관리 하 고 단위 테스트를 추가 하 여 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-128">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="3b182-129">데이터 모델 클래스를 모의 하 고는 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-129">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="3b182-130">반복 #6-테스트 중심 개발을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-130">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="3b182-131">이 여섯 번째 반복에서는 추가 새로운 기능을 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대 한 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-131">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="3b182-132">이 반복에서는 메일 그룹을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-132">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="3b182-133">반복 #7 – Ajax 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-133">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="3b182-134">일곱 번째 반복에서 개선할 응용 프로그램의 성능과 응답성 Ajax에 대 한 지원을 추가 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-134">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="3b182-135">이 반복</span><span class="sxs-lookup"><span data-stu-id="3b182-135">This Iteration</span></span>

<span data-ttu-id="3b182-136">이 첫 번째 반복에서 기본 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-136">In this first iteration, we build the basic application.</span></span> <span data-ttu-id="3b182-137">목표 가능한 가장 빠르고 가장 간단한 방법으로 연락처 관리자를 빌드하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-137">The goal is to build the Contact Manager in the fastest and simplest way possible.</span></span> <span data-ttu-id="3b182-138">이후 반복에서 응용 프로그램의 디자인을 향상 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-138">In later iterations, we improve the design of the application.</span></span>

<span data-ttu-id="3b182-139">연락처 관리자 응용 프로그램은 기본 데이터베이스 중심 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-139">The Contact Manager application is a basic database-driven application.</span></span> <span data-ttu-id="3b182-140">새 연락처를 만들고 기존 연락처를 편집 하 고 연락처를 삭제 하는 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-140">You can use the application to create new contacts, edit existing contacts, and delete contacts.</span></span>

<span data-ttu-id="3b182-141">이 반복에서 다음 단계를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-141">In this iteration, we complete the following steps:</span></span>

1. <span data-ttu-id="3b182-142">ASP.NET MVC 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="3b182-142">ASP.NET MVC application</span></span>
2. <span data-ttu-id="3b182-143">이 연락처를 저장 하기 위한 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="3b182-143">Create a database to store our contacts</span></span>
3. <span data-ttu-id="3b182-144">Microsoft Entity Framework를 사용 하 여 데이터베이스에 대 한 모델 클래스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-144">Generate a model class for our database with the Microsoft Entity Framework</span></span>
4. <span data-ttu-id="3b182-145">컨트롤러 작업 및 모든 데이터베이스에 연락처를 나열할 수 있게 해 주는 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="3b182-145">Create a controller action and view that enables us to list all of the contacts in the database</span></span>
5. <span data-ttu-id="3b182-146">컨트롤러 작업을 만들고 데이터베이스에 새 연락처를 만들 수 있게 해 주는 보기</span><span class="sxs-lookup"><span data-stu-id="3b182-146">Create controller actions and a view that enables us to create a new contact in the database</span></span>
6. <span data-ttu-id="3b182-147">컨트롤러 작업을 만들고 데이터베이스에 있는 기존 연락처를 편집할 수 있게 해 주는 보기</span><span class="sxs-lookup"><span data-stu-id="3b182-147">Create controller actions and a view that enables us to edit an existing contact in the database</span></span>
7. <span data-ttu-id="3b182-148">컨트롤러 작업을 만들고 데이터베이스에 있는 기존 연락처를 삭제할 수 있게 해 주는 보기</span><span class="sxs-lookup"><span data-stu-id="3b182-148">Create controller actions and a view that enables us to delete an existing contact in the database</span></span>

## <a name="software-prerequisites"></a><span data-ttu-id="3b182-149">소프트웨어 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="3b182-149">Software Prerequisites</span></span>

<span data-ttu-id="3b182-150">ASP.NET MVC 응용 프로그램에서 Visual Studio 2008 또는 Visual Web Developer 2008 (Visual Web Developer는 모든 Visual Studio의 고급 기능을 포함 하지 않는 Visual Studio의 무료 버전) 컴퓨터에 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-150">In ASP.NET MVC applications, you must have either Visual Studio 2008 or Visual Web Developer 2008 installed on your computer (Visual Web Developer is a free version of Visual Studio that does not include all of the advanced features of Visual Studio).</span></span> <span data-ttu-id="3b182-151">다음 주소에서의 Visual Studio 2008 평가판 또는 Visual Web Developer를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-151">You can download either the trial version of Visual Studio 2008 or Visual Web Developer from the following address:</span></span>

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> <span data-ttu-id="3b182-152">Visual Web Developer를 사용 하 여 ASP.NET MVC 응용 프로그램에 대 한 설치 Visual Web Developer 서비스 팩 1 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-152">For ASP.NET MVC applications with Visual Web Developer, you must have Visual Web Developer Service Pack 1 installed.</span></span> <span data-ttu-id="3b182-153">서비스 팩 1 없이 웹 응용 프로그램 프로젝트를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-153">Without Service Pack 1, you cannot create Web Application Projects.</span></span>


<span data-ttu-id="3b182-154">ASP.NET MVC 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-154">ASP.NET MVC framework.</span></span> <span data-ttu-id="3b182-155">다음 주소에서 ASP.NET MVC 프레임 워크를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-155">You can download the ASP.NET MVC framework from the following address:</span></span>

[https://www.asp.net/mvc](../../../index.md)

<span data-ttu-id="3b182-156">이 자습서에서는 데이터베이스에 액세스 하려면 Microsoft Entity Framework 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-156">In this tutorial, we use the Microsoft Entity Framework to access a database.</span></span> <span data-ttu-id="3b182-157">Entity Framework는.NET Framework 3.5 서비스 팩 1 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-157">The Entity Framework is included with .NET Framework 3.5 Service Pack 1.</span></span> <span data-ttu-id="3b182-158">다음 위치에서이 서비스 팩을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-158">You can download this service pack from the following location:</span></span>

[<span data-ttu-id="3b182-159">https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&ampdisplaylang = en</span><span class="sxs-lookup"><span data-stu-id="3b182-159">https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en</span></span>](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

<span data-ttu-id="3b182-160">각이 다운로드 하나씩 수행 하는 대신, Web Platform Installer (Web PI)를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-160">As an alternative to performing each of these downloads one by one, you can take advantage of the Web Platform Installer (Web PI).</span></span> <span data-ttu-id="3b182-161">다음 주소에서 웹 PI를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-161">You can download the Web PI from the following address:</span></span>

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a><span data-ttu-id="3b182-162">ASP.NET MVC 프로젝트</span><span class="sxs-lookup"><span data-stu-id="3b182-162">ASP.NET MVC Project</span></span>

<span data-ttu-id="3b182-163">ASP.NET MVC 웹 응용 프로그램 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-163">ASP.NET MVC Web Application Project.</span></span> <span data-ttu-id="3b182-164">Visual Studio를 시작 하 고 메뉴 옵션을 선택 **파일, 새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-164">Launch Visual Studio and select the menu option **File, New Project**.</span></span> <span data-ttu-id="3b182-165">합니다 **새 프로젝트** 대화 상자가 나타납니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="3b182-165">The **New Project** dialog appears (see Figure 1).</span></span> <span data-ttu-id="3b182-166">선택 된 **웹** 프로젝트 형식 및 **ASP.NET MVC 웹 응용 프로그램** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="3b182-166">Select the **Web** project type and the **ASP.NET MVC Web Application** template.</span></span> <span data-ttu-id="3b182-167">새 프로젝트의 이름을 *ContactManager* 확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-167">Name your new project *ContactManager* and click the OK button.</span></span>


<span data-ttu-id="3b182-168">.NET Framework 3.5 맨 위에 있는 드롭다운 목록에서 선택 되어 있는지 확인의 오른쪽의 **새 프로젝트** 대화 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-168">Make sure that you have .NET Framework 3.5 selected from the dropdown list at the top right of the **New Project** dialog.</span></span> <span data-ttu-id="3b182-169">그렇지 않으면 t-이득 ASP.NET MVC 웹 응용 프로그램 템플릿이 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-169">Otherwise, the ASP.NET MVC Web Application template won t appear.</span></span>


<span data-ttu-id="3b182-170">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image1.jpg)](iteration-1-create-the-application-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-170">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image1.jpg)](iteration-1-create-the-application-vb/_static/image1.png)</span></span>

<span data-ttu-id="3b182-171">**그림 01**: 새 프로젝트 대화 상자 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-171">**Figure 01**: The New Project dialog([Click to view full-size image](iteration-1-create-the-application-vb/_static/image2.png))</span></span>


<span data-ttu-id="3b182-172">ASP.NET MVC 응용 프로그램을 **단위 테스트 프로젝트 만들기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-172">ASP.NET MVC application, the **Create Unit Test Project** dialog appears.</span></span> <span data-ttu-id="3b182-173">이 대화 상자를 만들고 ASP.NET MVC 응용 프로그램을 만들 때 솔루션에 단위 테스트 프로젝트를 추가할 것인지 나타내기 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-173">You can use this dialog to indicate that you want to create and add a unit test project to your solution when you create your ASP.NET MVC application.</span></span> <span data-ttu-id="3b182-174">T 땀 있지만이 반복에서 단위 테스트 빌드 옵션을 선택 해야 **예, 단위 테스트 프로젝트 만들기** 이후 반복에서 단위 테스트를 추가할 계획 이기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-174">Although we won t be building unit tests in this iteration, you should select the option **Yes, create a unit test project** because we plan to add unit tests in a later iteration.</span></span> <span data-ttu-id="3b182-175">새 ASP.NET MVC 프로젝트를 처음 만들 때 테스트 프로젝트를 추가 하는 것은 ASP.NET MVC 프로젝트를 만든 후 테스트 프로젝트를 추가 하는 것 보다 훨씬 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-175">Adding a Test project when you first create a new ASP.NET MVC project is much easier than adding a Test project after the ASP.NET MVC project has been created.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="3b182-176">Visual Web Developer는 테스트 프로젝트를 지원 하지 않으므로 얻지 못하는 단위 테스트 프로젝트 만들기 대화 상자 Visual Web Developer를 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3b182-176">Because Visual Web Developer does not support Test projects, you do not get the Create Unit Test Project dialog when using Visual Web Developer.</span></span>


<span data-ttu-id="3b182-177">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image2.jpg)](iteration-1-create-the-application-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-177">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image2.jpg)](iteration-1-create-the-application-vb/_static/image3.png)</span></span>

<span data-ttu-id="3b182-178">**그림 02**:의 단위 테스트 프로젝트 만들기 대화 상자 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-178">**Figure 02**: The Create Unit Test Project dialog ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image4.png))</span></span>


<span data-ttu-id="3b182-179">ASP.NET MVC 응용 프로그램 Visual Studio 솔루션 탐색기 창에 나타납니다 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="3b182-179">ASP.NET MVC application appears in the Visual Studio Solution Explorer window (see Figure 3).</span></span> <span data-ttu-id="3b182-180">Don t 메뉴 옵션을 선택 하 여이 창을 열 수 있습니다 다음 솔루션 탐색기 창 표시 **보기, 솔루션 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-180">If you don t see the Solution Explorer window then you can open this window by selecting the menu option **View, Solution Explorer**.</span></span> <span data-ttu-id="3b182-181">솔루션에 두 개의 프로젝트 알림: ASP.NET MVC 프로젝트와 테스트 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="3b182-181">Notice that the solution contains two projects: the ASP.NET MVC project and the Test project.</span></span> <span data-ttu-id="3b182-182">ASP.NET MVC 프로젝트 이름이 ContactManager 및 테스트 프로젝트 이름이 ContactManager.Tests 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-182">The ASP.NET MVC project is named ContactManager and the Test project is named ContactManager.Tests.</span></span>


<span data-ttu-id="3b182-183">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image3.jpg)](iteration-1-create-the-application-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-183">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image3.jpg)](iteration-1-create-the-application-vb/_static/image5.png)</span></span>

<span data-ttu-id="3b182-184">**그림 03**:의 솔루션 탐색기 창 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-184">**Figure 03**: The Solution Explorer window ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image6.png))</span></span>


## <a name="deleting-the-project-sample-files"></a><span data-ttu-id="3b182-185">프로젝트 샘플 파일 삭제</span><span class="sxs-lookup"><span data-stu-id="3b182-185">Deleting the Project Sample Files</span></span>

<span data-ttu-id="3b182-186">ASP.NET MVC 프로젝트 템플릿은 컨트롤러 및 뷰에 대 한 샘플 파일이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-186">The ASP.NET MVC project template includes sample files for controllers and views.</span></span> <span data-ttu-id="3b182-187">새 ASP.NET MVC 응용 프로그램을 만들기 전에 이러한 파일을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-187">Before creating a new ASP.NET MVC application, you should delete these files.</span></span> <span data-ttu-id="3b182-188">파일 또는 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 하 여 솔루션 탐색기 창에서 파일 및 폴더를 삭제할 수 있습니다 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-188">You can delete files and folders in the Solution Explorer window by right-clicking a file or folder and selecting the menu option **Delete**.</span></span>

<span data-ttu-id="3b182-189">ASP.NET MVC 프로젝트에서 다음 파일을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-189">You need to delete the following files from the ASP.NET MVC project:</span></span>

- <span data-ttu-id="3b182-190">\Controllers\HomeController.vb</span><span class="sxs-lookup"><span data-stu-id="3b182-190">\Controllers\HomeController.vb</span></span>

- <span data-ttu-id="3b182-191">\Views\Home\About.aspx</span><span class="sxs-lookup"><span data-stu-id="3b182-191">\Views\Home\About.aspx</span></span>

- <span data-ttu-id="3b182-192">\Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="3b182-192">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="3b182-193">및 테스트 프로젝트에서 다음 파일을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-193">And, you need to delete the following file from the Test project:</span></span>

<span data-ttu-id="3b182-194">\Controllers\HomeControllerTest.vb</span><span class="sxs-lookup"><span data-stu-id="3b182-194">\Controllers\HomeControllerTest.vb</span></span>

## <a name="creating-the-database"></a><span data-ttu-id="3b182-195">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="3b182-195">Creating the Database</span></span>

<span data-ttu-id="3b182-196">연락처 관리자 응용 프로그램은 데이터베이스 기반 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-196">The Contact Manager application is a database-driven web application.</span></span> <span data-ttu-id="3b182-197">연락처 정보를 저장할 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-197">We use a database to store the contact information.</span></span>

<span data-ttu-id="3b182-198">Microsoft SQL Server, Oracle, MySQL 및 IBM DB2 데이터베이스를 비롯 한 모든 최신 데이터베이스를 사용 하 여 ASP.NET MVC 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-198">The ASP.NET MVC framework with any modern database including Microsoft SQL Server, Oracle, MySQL, and IBM DB2 databases.</span></span> <span data-ttu-id="3b182-199">이 자습서에서는 Microsoft SQL Server 데이터베이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-199">In this tutorial, we use a Microsoft SQL Server database.</span></span> <span data-ttu-id="3b182-200">Visual Studio를 설치할 때 Microsoft SQL Server 데이터베이스의 무료 버전인 Microsoft SQL Server Express 설치 옵션으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-200">When you install Visual Studio, you are provided with the option of installing Microsoft SQL Server Express which is a free version of the Microsoft SQL Server database.</span></span>

<span data-ttu-id="3b182-201">앱을 마우스 오른쪽 단추로 클릭 하 여 새 데이터베이스를 만들\_솔루션 탐색기 창 및 메뉴 옵션을 선택 하면 데이터 폴더 **추가, 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-201">Create a new database by right-clicking the App\_Data folder in the Solution Explorer window and selecting the menu option **Add, New Item**.</span></span> <span data-ttu-id="3b182-202">에 **새 항목 추가** 대화 상자에서 선택 합니다 **데이터** 범주 및 **SQL Server 데이터베이스** 템플릿 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="3b182-202">In the **Add New Item** dialog, select the **Data** category and the **SQL Server Database** template (see Figure 4).</span></span> <span data-ttu-id="3b182-203">새 데이터베이스 ContactManagerDB.mdf 이름과 확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-203">Name the new database ContactManagerDB.mdf and click the OK button.</span></span>


<span data-ttu-id="3b182-204">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image4.jpg)](iteration-1-create-the-application-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-204">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image4.jpg)](iteration-1-create-the-application-vb/_static/image7.png)</span></span>

<span data-ttu-id="3b182-205">**그림 04**: 새 Microsoft SQL Server Express 데이터베이스를 만드는 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-205">**Figure 04**: Creating a new Microsoft SQL Server Express database ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image8.png))</span></span>


<span data-ttu-id="3b182-206">데이터베이스 응용 프로그램에 표시 되는 새 데이터베이스를 만든 후\_솔루션 탐색기 창에서 데이터 폴더.</span><span class="sxs-lookup"><span data-stu-id="3b182-206">After you create the new database, the database appears in the App\_Data folder in the Solution Explorer window.</span></span> <span data-ttu-id="3b182-207">서버 탐색기 창을 열고 데이터베이스에 연결 된 ContactManager.mdf 파일을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-207">Double-click the ContactManager.mdf file to open the Server Explorer window and connect to the database.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="3b182-208">서버 탐색기 창에는 Microsoft Visual Web Developer의 경우 데이터베이스 탐색기 창을 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-208">The Server Explorer window is called the Database Explorer window in the case of Microsoft Visual Web Developer.</span></span>


<span data-ttu-id="3b182-209">데이터베이스 테이블, 뷰, 트리거 및 저장된 프로시저와 같은 새 데이터베이스 개체를 만들려면 서버 탐색기 창에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-209">You can use the Server Explorer window to create new database objects such as database tables, views, triggers, and stored procedures.</span></span> <span data-ttu-id="3b182-210">테이블 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **새 테이블 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-210">Right-click the Tables folder and select the menu option **Add New Table**.</span></span> <span data-ttu-id="3b182-211">데이터베이스 테이블 디자이너 나타납니다 (그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="3b182-211">The Database Table Designer appears (see Figure 5).</span></span>


<span data-ttu-id="3b182-212">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image5.jpg)](iteration-1-create-the-application-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-212">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image5.jpg)](iteration-1-create-the-application-vb/_static/image9.png)</span></span>

<span data-ttu-id="3b182-213">**그림 05**: 데이터베이스 테이블 디자이너 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-213">**Figure 05**: The Database Table Designer ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image10.png))</span></span>


<span data-ttu-id="3b182-214">다음 열이 포함 된 테이블을 만들려고 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-214">We need to create a table that contains the following columns:</span></span>

<a id="0.2_table01"></a>


| <span data-ttu-id="3b182-215">**열 이름**</span><span class="sxs-lookup"><span data-stu-id="3b182-215">**Column Name**</span></span> | <span data-ttu-id="3b182-216">**데이터 형식**</span><span class="sxs-lookup"><span data-stu-id="3b182-216">**Data Type**</span></span> | <span data-ttu-id="3b182-217">**Null 허용**</span><span class="sxs-lookup"><span data-stu-id="3b182-217">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b182-218">ID</span><span class="sxs-lookup"><span data-stu-id="3b182-218">Id</span></span> | <span data-ttu-id="3b182-219">int</span><span class="sxs-lookup"><span data-stu-id="3b182-219">int</span></span> | <span data-ttu-id="3b182-220">False</span><span class="sxs-lookup"><span data-stu-id="3b182-220">false</span></span> |
| <span data-ttu-id="3b182-221">FirstName</span><span class="sxs-lookup"><span data-stu-id="3b182-221">FirstName</span></span> | <span data-ttu-id="3b182-222">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="3b182-222">nvarchar(50)</span></span> | <span data-ttu-id="3b182-223">False</span><span class="sxs-lookup"><span data-stu-id="3b182-223">false</span></span> |
| <span data-ttu-id="3b182-224">LastName</span><span class="sxs-lookup"><span data-stu-id="3b182-224">LastName</span></span> | <span data-ttu-id="3b182-225">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="3b182-225">nvarchar(50)</span></span> | <span data-ttu-id="3b182-226">False</span><span class="sxs-lookup"><span data-stu-id="3b182-226">false</span></span> |
| <span data-ttu-id="3b182-227">전화 번호</span><span class="sxs-lookup"><span data-stu-id="3b182-227">Phone</span></span> | <span data-ttu-id="3b182-228">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="3b182-228">nvarchar(50)</span></span> | <span data-ttu-id="3b182-229">False</span><span class="sxs-lookup"><span data-stu-id="3b182-229">false</span></span> |
| <span data-ttu-id="3b182-230">메일</span><span class="sxs-lookup"><span data-stu-id="3b182-230">Email</span></span> | <span data-ttu-id="3b182-231">nvarchar(255)</span><span class="sxs-lookup"><span data-stu-id="3b182-231">nvarchar(255)</span></span> | <span data-ttu-id="3b182-232">False</span><span class="sxs-lookup"><span data-stu-id="3b182-232">false</span></span> |


<span data-ttu-id="3b182-233">첫 번째 열, Id 열은 특별 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-233">The first column, the Id column, is special.</span></span> <span data-ttu-id="3b182-234">Id 열을 Id 열 및 기본 키 열으로 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-234">You need to mark the Id column as an Identity column and a Primary Key column.</span></span> <span data-ttu-id="3b182-235">열 속성 (그림 6의 맨 아래에서 확인)를 확장 하 고 Id 사양 속성까지 아래로 스크롤 하 여 열이 Identity 열 임을 나타낼 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-235">You indicate that a column is an Identity column by expanding Column Properites (look at the bottom of Figure 6) and scrolling down to the Identity Specification property.</span></span> <span data-ttu-id="3b182-236">설정 된 **(Id)** 속성을 값 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-236">Set the **(Is Identity)** property to the value **Yes**.</span></span>

<span data-ttu-id="3b182-237">열을 선택 하 고 키 아이콘이 있는 단추를 클릭 하 여 기본 키 열으로 열을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-237">You mark a column as a Primary Key column by selecting the column and clicking the button with the icon of a key.</span></span> <span data-ttu-id="3b182-238">열은 기본 키 열으로 표시 되 면 열 옆에 있는 키 아이콘이 나타납니다 (그림 6 참조).</span><span class="sxs-lookup"><span data-stu-id="3b182-238">After a column is marked as a Primary Key column, an icon of a key appears next to the column (see Figure 6).</span></span>

<span data-ttu-id="3b182-239">테이블 만들기를 마친 후 새 테이블을 저장 하려면 저장 단추 (플로피 아이콘이 포함 된 단추)를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-239">After you finish creating the table, click the Save button (the button with an icon of a floppy) to save the new table.</span></span> <span data-ttu-id="3b182-240">새 테이블 이름을 *연락처*합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-240">Give your new table the name *Contacts*.</span></span>

<span data-ttu-id="3b182-241">마침을 연락처 데이터베이스 테이블을 만든 후 테이블에 일부 레코드를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-241">After finish creating the Contacts database table, you should add some records to the table.</span></span> <span data-ttu-id="3b182-242">서버 탐색기 창에서 Contacts 테이블을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **테이블 데이터 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-242">Right-click the Contacts table in the Server Explorer window and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="3b182-243">표시 된 표에서 하나 이상의 연락처를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-243">Enter one or more contacts in the grid that appears.</span></span>

## <a name="creating-the-data-model"></a><span data-ttu-id="3b182-244">데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="3b182-244">Creating the Data Model</span></span>

<span data-ttu-id="3b182-245">ASP.NET MVC 응용 프로그램 모델, 뷰 및 컨트롤러 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-245">The ASP.NET MVC application consists of Models, Views, and Controllers.</span></span> <span data-ttu-id="3b182-246">이전 섹션에서 만든 Contacts 테이블을 나타내는 모델 클래스를 만들어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-246">We start by creating a Model class that represents the Contacts table that we created in the previous section.</span></span>

<span data-ttu-id="3b182-247">이 자습서에서는 데이터베이스에서 모델 클래스를 자동으로 생성 하는 Microsoft Entity Framework 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-247">In this tutorial, we use the Microsoft Entity Framework to generate a model class from the database automatically.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="3b182-248">ASP.NET MVC 프레임 워크는 어떤 방식으로 Microsoft Entity Framework는 관련이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-248">The ASP.NET MVC framework is not tied to the Microsoft Entity Framework in any way.</span></span> <span data-ttu-id="3b182-249">NHibernate, LINQ to SQL 또는 ADO.NET을 포함 하 여 다른 데이터베이스 액세스 기술을 사용 하 여 ASP.NET MVC를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-249">You can use ASP.NET MVC with alternative database access technologies including NHibernate, LINQ to SQL, or ADO.NET.</span></span>


<span data-ttu-id="3b182-250">데이터 모델 클래스를 만들려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-250">Follow these steps to create the data model classes:</span></span>

1. <span data-ttu-id="3b182-251">솔루션 탐색기 창에서 Models 폴더를 마우스 오른쪽 단추로 누르고 **추가, 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-251">Right-click the Models folder in the Solution Explorer window and select **Add, New Item**.</span></span> <span data-ttu-id="3b182-252">합니다 **새 항목 추가** 대화 상자가 나타납니다 (그림 6 참조).</span><span class="sxs-lookup"><span data-stu-id="3b182-252">The **Add New Item** dialog appears (see Figure 6).</span></span>
2. <span data-ttu-id="3b182-253">선택 된 **데이터** 범주 및 **ADO.NET Entity Data Model** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="3b182-253">Select the **Data** category and the **ADO.NET Entity Data Model** template.</span></span> <span data-ttu-id="3b182-254">데이터 모델의 이름을 *ContactManagerModel.edmx* 을 클릭 합니다 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-254">Name your data model *ContactManagerModel.edmx* and click the **Add** button.</span></span> <span data-ttu-id="3b182-255">엔터티 데이터 모델 마법사가 나타납니다 (그림 7 참조).</span><span class="sxs-lookup"><span data-stu-id="3b182-255">The Entity Data Model wizard appears (see Figure 7).</span></span>
3. <span data-ttu-id="3b182-256">에 **모델 콘텐츠 선택** 선택 단계 **데이터베이스에서 생성** (그림 7 참조).</span><span class="sxs-lookup"><span data-stu-id="3b182-256">In the **Choose Model Contents** step, select **Generate from database** (see Figure 7).</span></span>
4. <span data-ttu-id="3b182-257">에 **데이터 연결 선택** 단계 ContactManagerDB.mdf 데이터베이스를 선택 하 고 이름을 입력 합니다 *ContactManagerDBEntities* 엔터티 연결 설정 (그림 8 참조).</span><span class="sxs-lookup"><span data-stu-id="3b182-257">In the **Choose Your Data Connection** step, select the ContactManagerDB.mdf database and enter the name *ContactManagerDBEntities* for the Entity Connection Settings (see Figure 8).</span></span>
5. <span data-ttu-id="3b182-258">에 **데이터베이스 개체 선택** 단계 테이블 (그림 9 참조) 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-258">In the **Choose Your Database Objects** step, select the checkbox labeled Tables (see Figure 9).</span></span> <span data-ttu-id="3b182-259">데이터 모델 (에 하나만 Contacts 테이블) 데이터베이스에 포함 된 모든 테이블이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-259">The data model will include all tables contained in your database (there is just one, the Contacts table).</span></span> <span data-ttu-id="3b182-260">네임 스페이스를 입력 *모델*합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-260">Enter the namespace *Models*.</span></span> <span data-ttu-id="3b182-261">마법사를 완료 하려면 "마침" 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-261">Click the Finish button to complete the wizard.</span></span>


<span data-ttu-id="3b182-262">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image6.jpg)](iteration-1-create-the-application-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-262">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image6.jpg)](iteration-1-create-the-application-vb/_static/image11.png)</span></span>

<span data-ttu-id="3b182-263">**그림 06**: 새 항목 추가 대화 상자 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-263">**Figure 06**: The Add New Item dialog ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image12.png))</span></span>


<span data-ttu-id="3b182-264">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image7.jpg)](iteration-1-create-the-application-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-264">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image7.jpg)](iteration-1-create-the-application-vb/_static/image13.png)</span></span>

<span data-ttu-id="3b182-265">**그림 07**: Model 콘텐츠 선택 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-265">**Figure 07**: Choose Model Contents ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image14.png))</span></span>


<span data-ttu-id="3b182-266">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image8.jpg)](iteration-1-create-the-application-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-266">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image8.jpg)](iteration-1-create-the-application-vb/_static/image15.png)</span></span>

<span data-ttu-id="3b182-267">**그림 08**: 데이터 연결 선택 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-267">**Figure 08**: Choose Your Data Connection ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image16.png))</span></span>


<span data-ttu-id="3b182-268">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image9.jpg)](iteration-1-create-the-application-vb/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-268">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image9.jpg)](iteration-1-create-the-application-vb/_static/image17.png)</span></span>

<span data-ttu-id="3b182-269">**그림 09**: 데이터베이스 개체 선택 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-269">**Figure 09**: Choose Your Database Objects ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image18.png))</span></span>


<span data-ttu-id="3b182-270">엔터티 데이터 모델 마법사를 완료 하면 엔터티 데이터 모델 디자이너에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-270">After you complete the Entity Data Model Wizard, the Entity Data Model Designer appears.</span></span> <span data-ttu-id="3b182-271">디자이너를 모델링 하는 각 테이블에 해당 하는 클래스를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-271">The designer displays a class that corresponds to each table being modeled.</span></span> <span data-ttu-id="3b182-272">연락처 이라는 하나의 클래스에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-272">You should see one class named Contacts.</span></span>

<span data-ttu-id="3b182-273">엔터티 데이터 모델 마법사 기반 데이터베이스 테이블 이름으로 클래스 이름을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-273">The Entity Data Model wizard generates class names based on database table names.</span></span> <span data-ttu-id="3b182-274">거의 항상 마법사에서 생성 된 클래스의 이름을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-274">You almost always need to change the name of the class generated by the wizard.</span></span> <span data-ttu-id="3b182-275">디자이너에서 연락처 클래스를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **이름 바꾸기**합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-275">Right-click the Contacts class in the designer and select the menu option **Rename**.</span></span> <span data-ttu-id="3b182-276">(단일) 담당자에 게 연락처 (복수)에서 클래스의 이름을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-276">Change the name of the class from Contacts (plural) to Contact (singular).</span></span> <span data-ttu-id="3b182-277">클래스 이름으로 변경한 후 클래스는 그림 10 처럼 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-277">After you change the class name, the class should appear like Figure 10.</span></span>


<span data-ttu-id="3b182-278">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image10.jpg)](iteration-1-create-the-application-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-278">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image10.jpg)](iteration-1-create-the-application-vb/_static/image19.png)</span></span>

<span data-ttu-id="3b182-279">**그림 10**: The 연락처 클래스 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-279">**Figure 10**: The Contact class ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image20.png))</span></span>


<span data-ttu-id="3b182-280">이 시점에서 데이터베이스 모델을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-280">At this point, we have created our database model.</span></span> <span data-ttu-id="3b182-281">데이터베이스에서 특정 연락처 레코드를 나타내는 연락처 클래스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-281">We can use the Contact class to represent a particular contact record in our database.</span></span>

## <a name="creating-the-home-controller"></a><span data-ttu-id="3b182-282">홈 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="3b182-282">Creating the Home Controller</span></span>

<span data-ttu-id="3b182-283">다음 단계는 Home 컨트롤러를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-283">The next step is to create our Home controller.</span></span> <span data-ttu-id="3b182-284">Home 컨트롤러는 ASP.NET MVC 응용 프로그램에서 호출 되는 기본 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-284">The Home controller is the default controller invoked in an ASP.NET MVC application.</span></span>

<span data-ttu-id="3b182-285">솔루션 탐색기 창에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 하 여 홈 컨트롤러 클래스를 만듭니다 **추가, 컨트롤러** (그림 11 참조).</span><span class="sxs-lookup"><span data-stu-id="3b182-285">Create the Home controller class by right-clicking the Controllers folder in the Solution Explorer window and selecting the menu option **Add, Controller** (see Figure 11).</span></span> <span data-ttu-id="3b182-286">확인 확인란 **Create, Update 및 세부 정보 시나리오에 대 한 작업 메서드를 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-286">Notice the checkbox labeled **Add action methods for Create, Update, and Details scenarios**.</span></span> <span data-ttu-id="3b182-287">이 확인란을 클릭 하기 전에 선택 되어 있는지 확인 합니다 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-287">Make sure that this checkbox is checked before clicking the **Add** button.</span></span>


<span data-ttu-id="3b182-288">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image11.jpg)](iteration-1-create-the-application-vb/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-288">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image11.jpg)](iteration-1-create-the-application-vb/_static/image21.png)</span></span>

<span data-ttu-id="3b182-289">**그림 11**: Home 컨트롤러 추가 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image22.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-289">**Figure 11**: Adding the Home controller ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image22.png))</span></span>


<span data-ttu-id="3b182-290">Home 컨트롤러를 만들 때에 목록 1에서 클래스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-290">When you create the Home controller, you get the class in Listing 1.</span></span>

<span data-ttu-id="3b182-291">**1-Controllers\HomeController.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="3b182-291">**Listing 1 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample1.vb)]

## <a name="listing-the-contacts"></a><span data-ttu-id="3b182-292">연락처 나열</span><span class="sxs-lookup"><span data-stu-id="3b182-292">Listing the Contacts</span></span>

<span data-ttu-id="3b182-293">연락처 데이터베이스 테이블에 레코드를 표시 하려면 index () 작업 및 인덱스 뷰를 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-293">In order to display the records in the Contacts database table, we need to create an Index() action and an Index view.</span></span>

<span data-ttu-id="3b182-294">Home 컨트롤러 index () 작업을 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-294">The Home controller already contains an Index() action.</span></span> <span data-ttu-id="3b182-295">목록 2와 같은 표시 되도록이 메서드를 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-295">We need to modify this method so that it looks like Listing 2.</span></span>

<span data-ttu-id="3b182-296">**Listing 2 - Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="3b182-296">**Listing 2 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample2.vb)]

<span data-ttu-id="3b182-297">라는 private 필드 2 목록에서 홈 컨트롤러 클래스를 포함 하는 알림 \_엔터티.</span><span class="sxs-lookup"><span data-stu-id="3b182-297">Notice that the Home controller class in Listing 2 contains a private field named \_entities.</span></span> <span data-ttu-id="3b182-298">\_엔터티 필드 데이터 모델에서 엔터티를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-298">The \_entities field represents the entities from the data model.</span></span> <span data-ttu-id="3b182-299">사용 하 여는 \_엔터티 필드는 데이터베이스와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-299">We use the \_entities field to communicate with the database.</span></span>

<span data-ttu-id="3b182-300">Index () 메서드를 연락처 데이터베이스 테이블에서 모든 연락처를 나타내는 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-300">The Index() method returns a view that represents all of the contacts from the Contacts database table.</span></span> <span data-ttu-id="3b182-301">식 \_엔터티. ContactSet.ToList() 제네릭 목록으로 연락처 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-301">The expression \_entities.ContactSet.ToList() returns the list of contacts as a generic list.</span></span>

<span data-ttu-id="3b182-302">이제는 우리 ve 인덱스 컨트롤러를 만든 다음 인덱스 뷰를 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-302">Now that we ve created the Index controller, we next need to create the Index view.</span></span> <span data-ttu-id="3b182-303">인덱스 뷰를 만들기 전에 메뉴 옵션을 선택 하 여 응용 프로그램을 컴파일합니다 **빌드, 솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-303">Before creating the Index view, compile your application by selecting the menu option **Build, Build Solution**.</span></span> <span data-ttu-id="3b182-304">항상이 모델 클래스 목록 표시 하려면에서 보기를 추가 하기 전에 프로젝트를 컴파일해야 합니다 **뷰 추가** 대화 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-304">You should always compile your project before adding a view in order for the list of model classes to be displayed in the **Add View** dialog.</span></span>

<span data-ttu-id="3b182-305">Index () 메서드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 하 여 인덱스 뷰를 만든 **뷰 추가** (그림 12 참조).</span><span class="sxs-lookup"><span data-stu-id="3b182-305">You create the Index view by right-clicking the Index() method and selecting the menu option **Add View** (see Figure 12).</span></span> <span data-ttu-id="3b182-306">이 메뉴 옵션을 선택 하면 열립니다는 **뷰 추가** 대화 상자 (그림 13 참조).</span><span class="sxs-lookup"><span data-stu-id="3b182-306">Selecting this menu option opens the **Add View** dialog (see Figure 13).</span></span>


<span data-ttu-id="3b182-307">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image12.jpg)](iteration-1-create-the-application-vb/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-307">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image12.jpg)](iteration-1-create-the-application-vb/_static/image23.png)</span></span>

<span data-ttu-id="3b182-308">**그림 12**: 인덱스 뷰 추가 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-308">**Figure 12**: Adding the Index view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image24.png))</span></span>


<span data-ttu-id="3b182-309">에 **뷰 추가** 대화 상자에서 레이블이 지정 된 확인란 **강력한 형식의 뷰를 만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-309">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="3b182-310">데이터 클래스 ContactManager.Contact 보기 및 콘텐츠 목록 보기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-310">Select the View data class ContactManager.Contact and the View content List.</span></span> <span data-ttu-id="3b182-311">이러한 옵션을 선택 하면 연락처 레코드의 목록을 표시 하는 보기를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-311">Selecting these options generates a view that displays a list of Contact records.</span></span>


<span data-ttu-id="3b182-312">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image13.jpg)](iteration-1-create-the-application-vb/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-312">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image13.jpg)](iteration-1-create-the-application-vb/_static/image25.png)</span></span>

<span data-ttu-id="3b182-313">**그림 13**: 뷰 추가 대화 상자 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image26.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-313">**Figure 13**: The Add View dialog ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image26.png))</span></span>


<span data-ttu-id="3b182-314">클릭할 때 합니다 **추가** 단추, 목록 3 인덱스 뷰 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-314">When you click the **Add** button, the Index view in Listing 3 is generated.</span></span> <span data-ttu-id="3b182-315">알림 합니다 &lt;% @ 페이지 %&gt; 파일의 위쪽에 표시 되는 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-315">Notice the &lt;%@ Page %&gt; directive that appears at the top of the file.</span></span> <span data-ttu-id="3b182-316">인덱스 보기 ViewPage에서 상속&lt;IEnumerable&lt;ContactManager.Models.Contact&gt; &gt; 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-316">The Index view inherits from the ViewPage&lt;IEnumerable&lt;ContactManager.Models.Contact&gt;&gt; class.</span></span> <span data-ttu-id="3b182-317">즉, 뷰에서 모델 클래스에는 연락처 엔터티 목록을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-317">In other words, the Model class in the view represents a list of Contact entities.</span></span>

<span data-ttu-id="3b182-318">인덱스 뷰의 본문 모델 클래스를 나타내는 연락처의 각 반복 되는 foreach 루프를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-318">The body of the Index view contains a foreach loop that iterates through each of the contacts represented by the Model class.</span></span> <span data-ttu-id="3b182-319">연락처 클래스의 각 속성의 값은 HTML 표 내의 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-319">The value of each property of the Contact class is displayed within an HTML table.</span></span>

<span data-ttu-id="3b182-320">**3-Views\Home\Index.aspx (수정 되지 않은)를 나열 합니다.**</span><span class="sxs-lookup"><span data-stu-id="3b182-320">**Listing 3 - Views\Home\Index.aspx (unmodified)**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample3.aspx)]

<span data-ttu-id="3b182-321">하나의 인덱스 보기 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-321">We need to make one modification to the Index view.</span></span> <span data-ttu-id="3b182-322">세부 정보 보기를 만들지 않는 것을 하기 때문에 세부 정보 링크를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-322">Because we are not creating a Details view, we can remove the Details link.</span></span> <span data-ttu-id="3b182-323">검색 하 고 인덱스 보기에서 다음 코드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-323">Find and remove the following code from the Index view:</span></span>

<span data-ttu-id="3b182-324">{.id = item.Id})%&gt;</span><span class="sxs-lookup"><span data-stu-id="3b182-324">{.id = item.Id})%&gt;</span></span>

<span data-ttu-id="3b182-325">인덱스 보기를 수정한 후에 연락처 관리자 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-325">After you modify the Index view, you can run the Contact Manager application.</span></span> <span data-ttu-id="3b182-326">디버깅 시작 메뉴 옵션 디버그을 선택 하거나 간단히 f5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-326">Select the menu option Debug, Start Debugging or simply press F5.</span></span> <span data-ttu-id="3b182-327">처음으로 응용 프로그램을 실행 하면 대화 상자를 그림 14에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-327">The first time you run the application, you get the dialog in Figure 14.</span></span> <span data-ttu-id="3b182-328">옵션을 선택 **디버깅을 사용 하려면 Web.config 파일 수정** 확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-328">Select the option **Modify the Web.config file to enable debugging** and click the OK button.</span></span>


<span data-ttu-id="3b182-329">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image14.jpg)](iteration-1-create-the-application-vb/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-329">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image14.jpg)](iteration-1-create-the-application-vb/_static/image27.png)</span></span>

<span data-ttu-id="3b182-330">**그림 14**: 디버깅 사용 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image28.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-330">**Figure 14**: Enabling debugging ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image28.png))</span></span>


<span data-ttu-id="3b182-331">인덱스 보기는 기본적으로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-331">The Index view is returned by default.</span></span> <span data-ttu-id="3b182-332">이 보기 연락처 데이터베이스 테이블에서 데이터의 모든를 나열 합니다 (그림 15 참조).</span><span class="sxs-lookup"><span data-stu-id="3b182-332">This view lists all of the data from the Contacts database table (see Figure 15).</span></span>


<span data-ttu-id="3b182-333">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image15.jpg)](iteration-1-create-the-application-vb/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-333">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image15.jpg)](iteration-1-create-the-application-vb/_static/image29.png)</span></span>

<span data-ttu-id="3b182-334">**그림 15**: The 인덱스 보기 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image30.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-334">**Figure 15**: The Index view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image30.png))</span></span>


<span data-ttu-id="3b182-335">인덱스 보기 보기의 맨 아래에서 새로 만들기를 레이블이 지정 된 링크가 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-335">Notice that the Index view includes a link labeled Create New at the bottom of the view.</span></span> <span data-ttu-id="3b182-336">다음 섹션에서는 새 연락처를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-336">In the next section, you learn how to create new contacts.</span></span>

## <a name="creating-new-contacts"></a><span data-ttu-id="3b182-337">새 연락처 만들기</span><span class="sxs-lookup"><span data-stu-id="3b182-337">Creating New Contacts</span></span>

<span data-ttu-id="3b182-338">사용자가 새 연락처를 만들 수 있도록 홈 컨트롤러에 두 create () 작업을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-338">To enable users to create new contacts, we need to add two Create() actions to the Home controller.</span></span> <span data-ttu-id="3b182-339">새 연락처 만들기에 대 한 HTML 폼을 반환 하는 하나의 create () 작업을 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-339">We need to create one Create() action that returns an HTML form for creating a new contact.</span></span> <span data-ttu-id="3b182-340">새 연락처의 실제 데이터베이스 삽입을 수행 하는 두 번째 create () 작업을 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-340">We need to create a second Create() action that performs the actual database insert of the new contact.</span></span>

<span data-ttu-id="3b182-341">홈 컨트롤러에 추가 해야 하는 새로운 create () 메서드는 목록 4에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-341">The new Create() methods that we need to add to the Home controller are contained in Listing 4.</span></span>

<span data-ttu-id="3b182-342">**4-Controllers\HomeController.vb (메서드로 만들기)를 나열합니다.**</span><span class="sxs-lookup"><span data-stu-id="3b182-342">**Listing 4 - Controllers\HomeController.vb (with Create methods)**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample4.vb)]

<span data-ttu-id="3b182-343">두 번째 create () 메서드는 HTTP POST를 통해서만 호출할 수 있지만 HTTP GET을 사용 하 여 첫 번째 create () 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-343">The first Create() method can be invoked with an HTTP GET while the second Create() method can be invoked only by an HTTP POST.</span></span> <span data-ttu-id="3b182-344">즉, HTML 폼 게시 하는 경우에 두 번째 create () 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-344">In other words, the second Create() method can be invoked only when posting an HTML form.</span></span> <span data-ttu-id="3b182-345">첫 번째 create () 메서드는 단순히 새 연락처를 만들기 위한 HTML 양식을 포함 하는 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-345">The first Create() method simply returns a view that contains the HTML form for creating a new contact.</span></span> <span data-ttu-id="3b182-346">두 번째 create () 메서드는 훨씬 더 흥미로운: 데이터베이스에 새 연락처를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-346">The second Create() method is much more interesting: it adds the new contact to the database.</span></span>

<span data-ttu-id="3b182-347">두 번째 create () 메서드 담당자 클래스의 인스턴스를 허용 하도록 수정 되었다는 사실을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-347">Notice that the second Create() method has been modified to accept an instance of the Contact class.</span></span> <span data-ttu-id="3b182-348">HTML 폼 게시 된 양식 값은 자동으로 ASP.NET MVC 프레임 워크에서이 연락처 클래스에 바인딩된 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-348">The form values posted from the HTML form are bound to this Contact class by the ASP.NET MVC framework automatically.</span></span> <span data-ttu-id="3b182-349">만들 HTML 폼에서 각 폼 필드 연락처 매개 변수의 속성에 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-349">Each form field from the HTML Create form is assigned to a property of the Contact parameter.</span></span>

<span data-ttu-id="3b182-350">문의 매개 변수 [바인딩] 특성으로 데코 레이트 된 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-350">Notice that the Contact parameter is decorated with a [Bind] attribute.</span></span> <span data-ttu-id="3b182-351">[바인딩] 특성은 바인딩에서 연락처 Id 속성을 제외 하려면 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-351">The [Bind] attribute is used to exclude the Contact Id property from binding.</span></span> <span data-ttu-id="3b182-352">Id 속성 Identity 속성을 나타내기 때문에 Id 속성을 설정 하려면 t 하지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-352">Because the Id property represents an Identity property, we don t want to set the Id property.</span></span>

<span data-ttu-id="3b182-353">Create () 메서드의 본문에 새 연락처 데이터베이스에 삽입 하는 Entity Framework 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-353">In the body of the Create() method, the Entity Framework is used to insert the new Contact into the database.</span></span> <span data-ttu-id="3b182-354">새 연락처가 연락처의 기존 집합에 추가 하 고 기본 데이터베이스에 이러한 변경 내용을 다시 푸시할 savechanges () 메서드는 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-354">The new Contact is added to the existing set of Contacts and the SaveChanges() method is called to push these changes back to the underlying database.</span></span>

<span data-ttu-id="3b182-355">두 create () 메서드 중 하나를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 하 여 새 연락처 만들기에 대 한 HTML 폼을 생성할 수 있습니다 **뷰 추가** (그림 16 참조).</span><span class="sxs-lookup"><span data-stu-id="3b182-355">You can generate an HTML form for creating new Contacts by right-clicking either of the two Create() methods and selecting the menu option **Add View** (see Figure 16).</span></span>


<span data-ttu-id="3b182-356">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image16.jpg)](iteration-1-create-the-application-vb/_static/image31.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-356">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image16.jpg)](iteration-1-create-the-application-vb/_static/image31.png)</span></span>

<span data-ttu-id="3b182-357">**그림 16**: 만들기 뷰 추가 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image32.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-357">**Figure 16**: Adding the Create view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image32.png))</span></span>


<span data-ttu-id="3b182-358">에 **뷰 추가** 대화 상자에서 선택 합니다 **ContactManager.Contact** 클래스 및 **만들기** 콘텐츠 보기에 대 한 옵션 (그림 17 참조).</span><span class="sxs-lookup"><span data-stu-id="3b182-358">In the **Add View** dialog, select the **ContactManager.Contact** class and the **Create** option for view content (see Figure 17).</span></span> <span data-ttu-id="3b182-359">클릭할 때 합니다 **추가** 보기를 자동으로 생성 하는 만들기 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-359">When you click the **Add** button, a Create view is generated automatically.</span></span>


<span data-ttu-id="3b182-360">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image17.jpg)](iteration-1-create-the-application-vb/_static/image33.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-360">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image17.jpg)](iteration-1-create-the-application-vb/_static/image33.png)</span></span>

<span data-ttu-id="3b182-361">**그림 17**: 분해 하는 페이지가 표시 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image34.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-361">**Figure 17**: Seeing a page explode ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image34.png))</span></span>


<span data-ttu-id="3b182-362">만들기 뷰는 각 연락처 클래스의 속성에 대 한 양식 필드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-362">The Create view contains form fields for each of the properties of the Contact class.</span></span> <span data-ttu-id="3b182-363">뷰 만들기에 대 한 코드 목록 5에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-363">The code for the Create view is included in Listing 5.</span></span>

<span data-ttu-id="3b182-364">**5-Views\Home\Create.aspx 나열**</span><span class="sxs-lookup"><span data-stu-id="3b182-364">**Listing 5 - Views\Home\Create.aspx**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample5.aspx)]

<span data-ttu-id="3b182-365">Create () 메서드를 수정 하 고 만들기 뷰 추가 후에 연락처 관리자 응용 프로그램을 실행 하 고 새 연락처를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-365">After you modify the Create() methods and add the Create view, you can run the Contact Manger application and create new contacts.</span></span> <span data-ttu-id="3b182-366">클릭 합니다 **새로 만들기** 만들기 뷰를 이동할 인덱스 보기에 표시 되는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-366">Click the **Create New** link that appears in the Index view to navigate to the Create view.</span></span> <span data-ttu-id="3b182-367">그림 18에서 보기가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-367">You should see the view in Figure 18.</span></span>


<span data-ttu-id="3b182-368">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image18.jpg)](iteration-1-create-the-application-vb/_static/image35.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-368">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image18.jpg)](iteration-1-create-the-application-vb/_static/image35.png)</span></span>

<span data-ttu-id="3b182-369">**그림 18**: The Create View ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image36.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-369">**Figure 18**: The Create View ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image36.png))</span></span>


## <a name="editing-contacts"></a><span data-ttu-id="3b182-370">연락처를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-370">Editing Contacts</span></span>

<span data-ttu-id="3b182-371">연락처 레코드를 편집 하기 위한 기능을 추가 하는 것은 새 연락처 레코드를 만들기 위한 기능 추가 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-371">Adding the functionality for editing a contact record is very similar to adding the functionality for creating new contact records.</span></span> <span data-ttu-id="3b182-372">먼저, 홈 컨트롤러 클래스에 두 개의 새 편집 메서드를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-372">First, we need to add two new Edit methods to the Home controller class.</span></span> <span data-ttu-id="3b182-373">이러한 새 되 메서드 목록 6에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-373">These new Edit() methods are contained in Listing 6.</span></span>

<span data-ttu-id="3b182-374">**6-Controllers\HomeController.vb (메서드로 편집)를 나열합니다.**</span><span class="sxs-lookup"><span data-stu-id="3b182-374">**Listing 6 - Controllers\HomeController.vb (with Edit methods)**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample6.vb)]

<span data-ttu-id="3b182-375">첫 번째 되 메서드는 HTTP GET 작업에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-375">The first Edit() method is invoked by an HTTP GET operation.</span></span> <span data-ttu-id="3b182-376">Id 매개 변수를 편집 하 고 연락처 레코드의 Id를 나타내는이 메서드에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-376">An Id parameter is passed to this method which represents the Id of the contact record being edited.</span></span> <span data-ttu-id="3b182-377">Entity Framework id와 일치 하는 연락처를 검색 하는 레코드 편집에 대 한 HTML 폼을 포함 하는 보기 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-377">The Entity Framework is used to retrieve a contact that matches the Id. A view that contains an HTML form for editing a record is returned.</span></span>

<span data-ttu-id="3b182-378">두 번째 되 방법은 데이터베이스에 실제 업데이트를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-378">The second Edit() method performs the actual update to the database.</span></span> <span data-ttu-id="3b182-379">이 메서드는 매개 변수로 연락처 클래스의 인스턴스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-379">This method accepts an instance of the Contact class as a parameter.</span></span> <span data-ttu-id="3b182-380">ASP.NET MVC 프레임 워크를 바인딩합니다 양식 필드 편집 양식에서이 클래스에 자동으로.</span><span class="sxs-lookup"><span data-stu-id="3b182-380">The ASP.NET MVC framework binds the form fields from the Edit form to this class automatically.</span></span> <span data-ttu-id="3b182-381">인할 통지 연락처 (에서는 Id 속성의 값이 필요)를 편집 하는 경우 [바인딩] 특성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-381">Notice that you don t include the[Bind] attribute when editing a Contact (we need the value of the Id property).</span></span>

<span data-ttu-id="3b182-382">Entity Framework는 수정 된 연락처 데이터베이스에 저장 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-382">The Entity Framework is used to save the modified Contact to the database.</span></span> <span data-ttu-id="3b182-383">먼저 원래 연락처 데이터베이스에서 검색 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-383">The original Contact must be retrieved from the database first.</span></span> <span data-ttu-id="3b182-384">다음으로, Entity Framework ApplyPropertyChanges() 메서드 담당자에 게 변경 내용을 기록 하 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-384">Next, the Entity Framework ApplyPropertyChanges() method is called to record the changes to the Contact.</span></span> <span data-ttu-id="3b182-385">마지막으로, Entity Framework savechanges () 메서드는 기본 데이터베이스에 변경 내용을 유지 하려면 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-385">Finally, the Entity Framework SaveChanges() method is called to persist the changes to the underlying database.</span></span>

<span data-ttu-id="3b182-386">편집 양식 되 메서드를 마우스 오른쪽 단추로 클릭 하 고 추가 보기 메뉴 옵션을 선택 하 여 포함 하는 뷰를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-386">You can generate the view that contains the Edit form by right-clicking the Edit() method and selecting the menu option Add View.</span></span> <span data-ttu-id="3b182-387">뷰 추가 대화 상자에서 선택 합니다 **ContactManager.Models.Contact** 클래스와 **편집** 콘텐츠 보기 (그림 19 참조).</span><span class="sxs-lookup"><span data-stu-id="3b182-387">In the Add View dialog, select the **ContactManager.Models.Contact** class and the **Edit** view content (see Figure 19).</span></span>


<span data-ttu-id="3b182-388">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image19.jpg)](iteration-1-create-the-application-vb/_static/image37.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-388">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image19.jpg)](iteration-1-create-the-application-vb/_static/image37.png)</span></span>

<span data-ttu-id="3b182-389">**그림 19**:는 편집 뷰 추가 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image38.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-389">**Figure 19**: Adding an Edit View ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image38.png))</span></span>


<span data-ttu-id="3b182-390">추가 단추를 클릭 하면 새 편집 뷰를 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-390">When you click the Add button, a new Edit view is generated automatically.</span></span> <span data-ttu-id="3b182-391">생성 되는 HTML 폼의 각 연락처 클래스 (참조 코드 7)의 속성에 해당 하는 필드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-391">The HTML form that is generated contains fields that correspond to each of the properties of the Contact class (see Listing 7).</span></span>

<span data-ttu-id="3b182-392">**Listing 7 - Views\Home\Edit.aspx**</span><span class="sxs-lookup"><span data-stu-id="3b182-392">**Listing 7 - Views\Home\Edit.aspx**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample7.aspx)]

## <a name="deleting-contacts"></a><span data-ttu-id="3b182-393">연락처 삭제</span><span class="sxs-lookup"><span data-stu-id="3b182-393">Deleting Contacts</span></span>

<span data-ttu-id="3b182-394">연락처를 삭제 하려는 경우 홈 컨트롤러 클래스에 두 delete () 작업을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-394">If you want to delete contacts then you need to add two Delete() actions to the Home controller class.</span></span> <span data-ttu-id="3b182-395">첫 번째 delete () 작업 삭제 확인 양식을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-395">The first Delete() action displays a delete confirmation form.</span></span> <span data-ttu-id="3b182-396">두 번째 delete () 작업을 실제 삭제를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-396">The second Delete() action performs the actual delete.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="3b182-397">나중에 반복 #7에서는 수정 Contact Manager Ajax 삭제 한 단계를 지원 하도록 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-397">Later, in Iteration #7, we modify the Contact Manager so that it supports a one step Ajax delete.</span></span>


<span data-ttu-id="3b182-398">두 개의 새 delete () 메서드는 목록 8에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-398">The two new Delete() methods are contained in Listing 8.</span></span>

<span data-ttu-id="3b182-399">**8-Controllers\HomeController.vb (삭제 메서드)를 나열합니다.**</span><span class="sxs-lookup"><span data-stu-id="3b182-399">**Listing 8 - Controllers\HomeController.vb (Delete methods)**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample8.vb)]

<span data-ttu-id="3b182-400">첫 번째 delete () 메서드는 데이터베이스에서 연락처 레코드를 삭제 하는 확인 형태를 반환 합니다. (Figure20 참조).</span><span class="sxs-lookup"><span data-stu-id="3b182-400">The first Delete() method returns a confirmation form for deleting a contact record from the database (see Figure20).</span></span> <span data-ttu-id="3b182-401">두 번째 delete () 메서드는 데이터베이스에 대해 실제 삭제 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-401">The second Delete() method performs the actual delete operation against the database.</span></span> <span data-ttu-id="3b182-402">원래 연락처 데이터베이스에서 검색 되 면 데이터베이스 삭제 하는 데 Entity Framework DeleteObject() 및 savechanges () 메서드를 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-402">After the original contact has been retrieved from the database, the Entity Framework DeleteObject() and SaveChanges() methods are called to perform the database delete.</span></span>


<span data-ttu-id="3b182-403">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image20.jpg)](iteration-1-create-the-application-vb/_static/image39.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-403">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image20.jpg)](iteration-1-create-the-application-vb/_static/image39.png)</span></span>

<span data-ttu-id="3b182-404">**그림 20**: 삭제 확인 보기로 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image40.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-404">**Figure 20**: The delete confirmation view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image40.png))</span></span>


<span data-ttu-id="3b182-405">(그림 21 참조) 하는 연락처 레코드를 삭제 하는 것에 대 한 링크 포함 되도록 인덱스 뷰를 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-405">We need to modify the Index view so that it contains a link for deleting contact records (see Figure 21).</span></span> <span data-ttu-id="3b182-406">편집 링크를 포함 하는 동일한 테이블 셀에 다음 코드를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-406">You need to add the following code to the same table cell that contains the Edit link:</span></span>

<span data-ttu-id="3b182-407">{.id = item.Id})%&gt;</span><span class="sxs-lookup"><span data-stu-id="3b182-407">{.id = item.Id})%&gt;</span></span>


<span data-ttu-id="3b182-408">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image21.jpg)](iteration-1-create-the-application-vb/_static/image41.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-408">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image21.jpg)](iteration-1-create-the-application-vb/_static/image41.png)</span></span>

<span data-ttu-id="3b182-409">**그림 21**: 인덱스 편집 링크를 사용 하 여 뷰 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image42.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-409">**Figure 21**: Index view with Edit link ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image42.png))</span></span>


<span data-ttu-id="3b182-410">다음으로, 삭제 확인 보기로 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-410">Next, we need to create the delete confirmation view.</span></span> <span data-ttu-id="3b182-411">홈 컨트롤러 클래스의 delete () 메서드를 마우스 오른쪽 단추로 클릭 하 고 추가 보기 메뉴 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-411">Right-click the Delete() method in the Home controller class and select the menu option Add View.</span></span> <span data-ttu-id="3b182-412">뷰 추가 대화 상자가 나타납니다 (그림 22 참조).</span><span class="sxs-lookup"><span data-stu-id="3b182-412">The Add View dialog appears (see Figure 22).</span></span>

<span data-ttu-id="3b182-413">와 달리 목록, 만들기 및 편집 보기의 경우 뷰 추가 대화 상자에 삭제 뷰를 만드는 옵션</span><span class="sxs-lookup"><span data-stu-id="3b182-413">Unlike in the case of the List, Create, and Edit views, the Add View dialog does not contain an option to create a Delete view.</span></span> <span data-ttu-id="3b182-414">대신 선택 합니다 **ContactManager.Models.Contact** 데이터 클래스 및 **빈** 콘텐츠 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-414">Instead, select the **ContactManager.Models.Contact** data class and the **Empty** view content.</span></span> <span data-ttu-id="3b182-415">콘텐츠 옵션 뷰를 직접 만들 필요는 빈 뷰를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-415">Selecting the Empty view content option will require us to create the view ourselves.</span></span>


<span data-ttu-id="3b182-416">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image22.jpg)](iteration-1-create-the-application-vb/_static/image43.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-416">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image22.jpg)](iteration-1-create-the-application-vb/_static/image43.png)</span></span>

<span data-ttu-id="3b182-417">**그림 22**: 삭제 확인 보기로 추가 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image44.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-417">**Figure 22**: Adding the delete confirmation view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image44.png))</span></span>


<span data-ttu-id="3b182-418">삭제 보기의 내용은 나열 하는 9에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-418">The content of the Delete view is contained in Listing 9.</span></span> <span data-ttu-id="3b182-419">이 보기에 확인 하는 양식이 있습니다 (그림 21을 참조 하는 경우)를 삭제 하는 특정 연락처를 여부를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-419">This view contains a form that confirms whether or not a particular contact should be deleted (see Figure 21).</span></span>

<span data-ttu-id="3b182-420">**Listing 9 - Views\Home\Delete.aspx**</span><span class="sxs-lookup"><span data-stu-id="3b182-420">**Listing 9 - Views\Home\Delete.aspx**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a><span data-ttu-id="3b182-421">기본 컨트롤러의 이름 변경</span><span class="sxs-lookup"><span data-stu-id="3b182-421">Changing the Name of the Default Controller</span></span>

<span data-ttu-id="3b182-422">이 연락처를 사용 하 여 작업에 대 한 컨트롤러 클래스의 이름은 HomeController 클래스를 지정 하 고는 문제 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-422">It might bother you that the name of our controller class for working with contacts is named the HomeController class.</span></span> <span data-ttu-id="3b182-423">해서는 t 컨트롤러 contact ¡© Controller 이름은?</span><span class="sxs-lookup"><span data-stu-id="3b182-423">Shouldn t the controller be named ContactController?</span></span>

<span data-ttu-id="3b182-424">이 문제는 쉽게 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-424">This issue is easy enough to fix.</span></span> <span data-ttu-id="3b182-425">첫째, Home 컨트롤러의 이름을 리팩터링 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-425">First, we need to refactor the name of the Home controller.</span></span> <span data-ttu-id="3b182-426">HomeController 클래스 Visual Studio 코드 편집기에서 열고, 클래스의 이름을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **이름 바꾸기**합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-426">Open the HomeController class in the Visual Studio Code Editor, right click the name of the class and select the menu option **Rename**.</span></span> <span data-ttu-id="3b182-427">이 메뉴 옵션을 선택 하면 이름 바꾸기 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-427">Selecting this menu option opens the Rename dialog.</span></span>


<span data-ttu-id="3b182-428">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image23.jpg)](iteration-1-create-the-application-vb/_static/image45.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-428">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image23.jpg)](iteration-1-create-the-application-vb/_static/image45.png)</span></span>

<span data-ttu-id="3b182-429">**그림 23**: 컨트롤러 이름 리팩터링 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image46.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-429">**Figure 23**: Refactoring a controller name ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image46.png))</span></span>


<span data-ttu-id="3b182-430">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image24.jpg)](iteration-1-create-the-application-vb/_static/image47.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-430">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image24.jpg)](iteration-1-create-the-application-vb/_static/image47.png)</span></span>

<span data-ttu-id="3b182-431">**그림 24**: 이름 바꾸기 대화 상자를 사용 하 여 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image48.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-431">**Figure 24**: Using the Rename dialog ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image48.png))</span></span>


<span data-ttu-id="3b182-432">컨트롤러 클래스의 이름을 바꾸면 Visual Studio의 Views 폴더의 폴더 이름을 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-432">If you rename your controller class, Visual Studio will update the name of the folder in the Views folder as well.</span></span> <span data-ttu-id="3b182-433">Visual Studio는 \Views\Contact 폴더로 \Views\Home 폴더를 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-433">Visual Studio will rename the \Views\Home folder to the \Views\Contact folder.</span></span>

<span data-ttu-id="3b182-434">이 변경을 수행한 후 응용 프로그램은 더 이상 Home 컨트롤러를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-434">After you make this change, your application will no longer have a Home controller.</span></span> <span data-ttu-id="3b182-435">응용 프로그램을 실행 하면 그림 25에서 오류 페이지를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-435">When you run your application, you'll get the error page in Figure 25.</span></span>


<span data-ttu-id="3b182-436">[![새 프로젝트 대화 상자](iteration-1-create-the-application-vb/_static/image25.jpg)](iteration-1-create-the-application-vb/_static/image49.png)</span><span class="sxs-lookup"><span data-stu-id="3b182-436">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image25.jpg)](iteration-1-create-the-application-vb/_static/image49.png)</span></span>

<span data-ttu-id="3b182-437">**그림 25**: 기본 컨트롤러 없음 ([큰 이미지를 보려면 클릭](iteration-1-create-the-application-vb/_static/image50.png))</span><span class="sxs-lookup"><span data-stu-id="3b182-437">**Figure 25**: No default controller ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image50.png))</span></span>


<span data-ttu-id="3b182-438">홈 컨트롤러 대신 연락처 컨트롤러를 사용 하려면 Global.asax 파일의 기본 경로 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-438">We need to update the default route in the Global.asax file to use the Contact controller instead of the Home controller.</span></span> <span data-ttu-id="3b182-439">Global.asax 파일을 열고 기본 경로 (참조 코드 10)에 의해 사용 되는 기본 컨트롤러를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-439">Open the Global.asax file and modify the default controller used by the default route (see Listing 10).</span></span>

<span data-ttu-id="3b182-440">**10-Global.asax.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="3b182-440">**Listing 10 - Global.asax.vb**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample10.vb)]

<span data-ttu-id="3b182-441">이러한 변경을 수행한 후 Contact Manager 올바르게 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-441">After you make these changes, the Contact Manager will run correctly.</span></span> <span data-ttu-id="3b182-442">이제 연락처 컨트롤러 클래스 기본 컨트롤러로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-442">Now, it will use the Contact controller class as the default controller.</span></span>

## <a name="summary"></a><span data-ttu-id="3b182-443">요약</span><span class="sxs-lookup"><span data-stu-id="3b182-443">Summary</span></span>

<span data-ttu-id="3b182-444">이 첫 번째 반복에서 기본 연락처 관리자 응용 프로그램에서에서 만든 가장 빠른 방법은 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-444">In this first iteration, we created a basic Contact Manager application in the fastest way possible.</span></span> <span data-ttu-id="3b182-445">이 컨트롤러 및 뷰에 대 한 초기 코드를 자동으로 생성 하려면 Visual Studio를 활용을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-445">We took advantage of Visual Studio to generate the initial code for our controllers and views automatically.</span></span> <span data-ttu-id="3b182-446">데이터베이스 모델 클래스를 자동으로 생성 하려면 엔터티 프레임 워크를 활용을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-446">We also took advantage of the Entity Framework to generate our database model classes automatically.</span></span>

<span data-ttu-id="3b182-447">현재에서는 수 목록, 만들기, 편집 및 연락처 관리자 응용 프로그램을 사용 하 여 연락처 레코드를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-447">Currently, we can list, create, edit, and delete contact records with the Contact Manager application.</span></span> <span data-ttu-id="3b182-448">즉, 모든 데이터베이스 기반 웹 응용 프로그램에 필요한 기본 데이터베이스 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-448">In other words, we can perform all of the basic database operations required by a database-driven web application.</span></span>

<span data-ttu-id="3b182-449">그러나 응용 프로그램에 몇 가지 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-449">Unfortunately, our application has some problems.</span></span> <span data-ttu-id="3b182-450">첫 번째 고 언제 든 지이 인정, 연락처 관리자 응용 프로그램의 가장 매력적인 응용 프로그램이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-450">First and I hesitate to admit this, the Contact Manager application is not the most attractive application.</span></span> <span data-ttu-id="3b182-451">일부 디자인 작업을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-451">It needs some design work.</span></span> <span data-ttu-id="3b182-452">다음 반복에서 기본 보기 마스터 페이지 및 응용 프로그램의 모양을 개선 하기 위해 연계 스타일 시트를 변경할 수 있습니다 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-452">In the next iteration, we'll look at how we can change the default view master page and cascading style sheet to improve the appearance of the application.</span></span>

<span data-ttu-id="3b182-453">둘째, 양식 유효성 검사를 구현 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-453">Second, we have not implemented any form validation.</span></span> <span data-ttu-id="3b182-454">예를 들어 없는 양식 필드에 대 한 값을 입력 하지 않고 만들기 연락처 양식을 제출 하지 못하도록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-454">For example, there is nothing to prevent you from submitting the Create contact form without entering values for any of the form fields.</span></span> <span data-ttu-id="3b182-455">또한 잘못 된 전화 번호 및 전자 메일 주소를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-455">Furthermore, you can enter invalid phone numbers and email addresses.</span></span> <span data-ttu-id="3b182-456">반복 # 3에서에서 양식 유효성 검사의 문제를 해결 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-456">We start to tackle the problem of form validation in iteration #3.</span></span>

<span data-ttu-id="3b182-457">마지막으로, 가장 중요 한 점은 연락처 관리자 응용 프로그램의 현재 반복 하거나 수 없습니다 쉽게 수정 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-457">Finally, and most importantly, the current iteration of the Contact Manager application cannot be easily modified or maintained.</span></span> <span data-ttu-id="3b182-458">예를 들어, 데이터베이스 액세스 논리는 컨트롤러 작업에 오른쪽을 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-458">For example, the database access logic is baked right into the controller actions.</span></span> <span data-ttu-id="3b182-459">이 컨트롤러를 수정 하지 않고 데이터 액세스 코드를 수정할 수 없습니다 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-459">This means that we cannot modify our data access code without modifying our controllers.</span></span> <span data-ttu-id="3b182-460">이후 반복에서는 복원 력을 연락처 관리자를 변경 하려면를 구현할 수 있습니다 하는 소프트웨어 디자인 패턴을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3b182-460">In later iterations, we explore software design patterns that we can implement to make the Contact Manager more resilient to change.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3b182-461">[이전](iteration-7-add-ajax-functionality-cs.md)
> [다음](iteration-2-make-the-application-look-nice-vb.md)</span><span class="sxs-lookup"><span data-stu-id="3b182-461">[Previous](iteration-7-add-ajax-functionality-cs.md)
[Next](iteration-2-make-the-application-look-nice-vb.md)</span></span>
