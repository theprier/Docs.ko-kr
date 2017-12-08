---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-cs
title: "반복 #1 – (C#) 응용 프로그램을 만들 | Microsoft Docs"
author: microsoft
description: "첫 번째 반복에서는 만듭니다 연락처 관리자에는 가장 간단한 방법은 가능한. 기본적인 데이터베이스 작업에 대 한 지원을 추가 하 여: 만들기, 읽기, 업데이트 및 D...."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2009
ms.topic: article
ms.assetid: db0f160b-901c-46d3-865e-7ab6cd4ed68d
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-cs
msc.type: authoredcontent
ms.openlocfilehash: 12927250595a8f3130328d2fe219280a13349787
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="iteration-1--create-the-application-c"></a><span data-ttu-id="2afc4-104">반복 #1 – 만드는 응용 프로그램 (C#)</span><span class="sxs-lookup"><span data-stu-id="2afc4-104">Iteration #1 – Create the Application (C#)</span></span>
====================
<span data-ttu-id="2afc4-105">여 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="2afc4-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="2afc4-106">코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="2afc4-106">Download Code</span></span>](iteration-1-create-the-application-cs/_static/contactmanager_1_cs1.zip)

> <span data-ttu-id="2afc4-107">첫 번째 반복에서는 만듭니다 연락처 관리자에는 가장 간단한 방법은 가능한.</span><span class="sxs-lookup"><span data-stu-id="2afc4-107">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="2afc4-108">기본적인 데이터베이스 작업에 대 한 지원을 추가 하 여: 만들기, 읽기, 업데이트 및 삭제 (CRUD).</span><span class="sxs-lookup"><span data-stu-id="2afc4-108">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a><span data-ttu-id="2afc4-109">연락처 관리 ASP.NET MVC 응용 프로그램 (VB) 빌드</span><span class="sxs-lookup"><span data-stu-id="2afc4-109">Building a Contact Management ASP.NET MVC Application (VB)</span></span>

<span data-ttu-id="2afc4-110">이 일련의 자습서에서는 전체 연락처 관리 응용을 프로그램의 시작 끝나기를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-110">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="2afc4-111">관리자에 게 문의 응용 프로그램을 사람 목록에 대 한 사용-이름, 전화 번호 및 전자 메일 주소-연락처 정보를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-111">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="2afc4-112">여러 반복을 통해에 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-112">We build the application over multiple iterations.</span></span> <span data-ttu-id="2afc4-113">각 반복에서 점진적으로 응용 프로그램을 개선 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-113">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="2afc4-114">이 여러 개의 반복 접근 방법의 목적은 각 변경의 이유를 이해 하는 데 사용할 수 있도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-114">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="2afc4-115">반복 #1-응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-115">Iteration #1 - Create the application.</span></span> <span data-ttu-id="2afc4-116">첫 번째 반복에서는 만듭니다 연락처 관리자에는 가장 간단한 방법은 가능한.</span><span class="sxs-lookup"><span data-stu-id="2afc4-116">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="2afc4-117">기본적인 데이터베이스 작업에 대 한 지원을 추가 하 여: 만들기, 읽기, 업데이트 및 삭제 (CRUD).</span><span class="sxs-lookup"><span data-stu-id="2afc4-117">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="2afc4-118">반복 #2-모양이 아닌 응용 프로그램을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-118">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="2afc4-119">이 반복에서 기본 ASP.NET MVC 뷰 마스터 페이지를 수정 및 스타일 시트를 연계 하 여 응용 프로그램의 모양을 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-119">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="2afc4-120">반복 #3-폼 유효성 검사를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-120">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="2afc4-121">세 번째 반복에서 기본적인 형태의 유효성 검사를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-121">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="2afc4-122">म 중이거나 사용자에서 필수 양식 필드를 완료 하지 않고 폼을 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-122">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="2afc4-123">또한 전자 메일 주소, 전화 번호를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-123">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="2afc4-124">반복 #4-느슨하게 결합 된 응용 프로그램을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-124">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="2afc4-125">이 세 번째 반복에서 우리 활용 여러 가지 소프트웨어 디자인 패턴을 쉽게 유지 관리 하 고 않아 응용 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-125">In this third iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="2afc4-126">예를 들어 리팩터링한 리포지토리 패턴 및 종속성 주입 패턴을 사용 하도록 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-126">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="2afc4-127">반복 #5-단위 테스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-127">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="2afc4-128">다섯 번째 반복에서 하도록 응용 프로그램이 쉽게 유지 관리 및 단위 테스트를 추가 하 여 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-128">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="2afc4-129">데이터 모델 클래스를 모의 하 고 우리의 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-129">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="2afc4-130">반복 6-테스트 기반 개발을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-130">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="2afc4-131">이 6 번째 반복에서에서는 새 기능을 추가할 응용 프로그램 먼저 단위 테스트를 작성 하 고 단위 테스트에 대해 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-131">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="2afc4-132">이 반복 메일 그룹을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-132">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="2afc4-133">반복 #7-Ajax 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-133">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="2afc4-134">일곱 번째 반복에서 개선할 응용 프로그램의 성능과 응답성 ajax 지원을 추가 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-134">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="2afc4-135">이 반복</span><span class="sxs-lookup"><span data-stu-id="2afc4-135">This Iteration</span></span>

<span data-ttu-id="2afc4-136">이 첫 번째 반복에서 기본적인 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-136">In this first iteration, we build the basic application.</span></span> <span data-ttu-id="2afc4-137">목표 가능한 빠르고 간편한 방식으로 연락처 관리자를 빌드하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-137">The goal is to build the Contact Manager in the fastest and simplest way possible.</span></span> <span data-ttu-id="2afc4-138">이후 반복에서 응용 프로그램의 디자인을 향상 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-138">In later iterations, we improve the design of the application.</span></span>

<span data-ttu-id="2afc4-139">않아 응용 프로그램은 기본 데이터베이스 기반 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="2afc4-139">The Contact Manager application is a basic database-driven application.</span></span> <span data-ttu-id="2afc4-140">새 연락처를 만들고 기존 연락처를 편집 하 고 연락처를 삭제 하는 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-140">You can use the application to create new contacts, edit existing contacts, and delete contacts.</span></span>

<span data-ttu-id="2afc4-141">이 반복에서 다음 단계를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-141">In this iteration, we complete the following steps:</span></span>

1. <span data-ttu-id="2afc4-142">ASP.NET MVC 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2afc4-142">ASP.NET MVC application</span></span>
2. <span data-ttu-id="2afc4-143">이 연락처를 저장 하기 위한 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="2afc4-143">Create a database to store our contacts</span></span>
3. <span data-ttu-id="2afc4-144">Microsoft Entity Framework와 함께 데이터베이스에 대 한 모델 클래스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-144">Generate a model class for our database with the Microsoft Entity Framework</span></span>
4. <span data-ttu-id="2afc4-145">컨트롤러 동작 및 모든 데이터베이스에 연락처를 나열할 수 있도록 하는 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="2afc4-145">Create a controller action and view that enables us to list all of the contacts in the database</span></span>
5. <span data-ttu-id="2afc4-146">컨트롤러 작업 및 데이터베이스에 새 연락처를 만들 수 있도록 하는 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="2afc4-146">Create controller actions and a view that enables us to create a new contact in the database</span></span>
6. <span data-ttu-id="2afc4-147">컨트롤러 작업 및 데이터베이스에 있는 기존 연락처를 편집할 수 있도록 해 주는 보기</span><span class="sxs-lookup"><span data-stu-id="2afc4-147">Create controller actions and a view that enables us to edit an existing contact in the database</span></span>
7. <span data-ttu-id="2afc4-148">컨트롤러 작업 및 데이터베이스에 있는 기존 연락처를 삭제할 수 있게 하는 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="2afc4-148">Create controller actions and a view that enables us to delete an existing contact in the database</span></span>

## <a name="software-prerequisites"></a><span data-ttu-id="2afc4-149">소프트웨어 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="2afc4-149">Software Prerequisites</span></span>

<span data-ttu-id="2afc4-150">ASP.NET MVC 응용 프로그램에서 Visual Studio 2008 또는 Visual Web Developer 2008 (Visual Web Developer는 Visual Studio의 고급 기능 중 일부가 포함 되지 않은 Visual Studio의 무료 버전) 컴퓨터에 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-150">In ASP.NET MVC applications, you must have either Visual Studio 2008 or Visual Web Developer 2008 installed on your computer (Visual Web Developer is a free version of Visual Studio that does not include all of the advanced features of Visual Studio).</span></span> <span data-ttu-id="2afc4-151">다음 주소에서 Visual Studio 2008의 평가판 버전 또는 Visual Web Developer를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-151">You can download either the trial version of Visual Studio 2008 or Visual Web Developer from the following address:</span></span>

[<span data-ttu-id="2afc4-152">https://www.asp.net/downloads/essential/</span><span class="sxs-lookup"><span data-stu-id="2afc4-152">https://www.asp.net/downloads/essential/</span></span>](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> <span data-ttu-id="2afc4-153">Visual Web Developer와 ASP.NET MVC 응용 프로그램에 대 한 설치 된 Visual Web Developer 서비스 팩 1이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-153">For ASP.NET MVC applications with Visual Web Developer, you must have Visual Web Developer Service Pack 1 installed.</span></span> <span data-ttu-id="2afc4-154">서비스 팩 1 없이 웹 응용 프로그램 프로젝트를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-154">Without Service Pack 1, you cannot create Web Application Projects.</span></span>


<span data-ttu-id="2afc4-155">ASP.NET MVC 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-155">ASP.NET MVC framework.</span></span> <span data-ttu-id="2afc4-156">다음 주소에서 ASP.NET MVC 프레임 워크를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-156">You can download the ASP.NET MVC framework from the following address:</span></span>

[<span data-ttu-id="2afc4-157">https://www.asp.net/mvc</span><span class="sxs-lookup"><span data-stu-id="2afc4-157">https://www.asp.net/mvc</span></span>](../../../index.md)

<span data-ttu-id="2afc4-158">이 자습서에서는 데이터베이스에 액세스 하려면 Microsoft Entity Framework를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-158">In this tutorial, we use the Microsoft Entity Framework to access a database.</span></span> <span data-ttu-id="2afc4-159">Entity Framework는.NET Framework 3.5 서비스 팩 1 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-159">The Entity Framework is included with .NET Framework 3.5 Service Pack 1.</span></span> <span data-ttu-id="2afc4-160">다음 위치에서이 서비스 팩을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-160">You can download this service pack from the following location:</span></span>

[<span data-ttu-id="2afc4-161">https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;4a83-b309-53b7b77edf78&displaylang = en</span><span class="sxs-lookup"><span data-stu-id="2afc4-161">https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en</span></span>](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

<span data-ttu-id="2afc4-162">이러한 다운로드 한 각 수행 하는 대신, 웹 플랫폼 설치 관리자 (웹 PI)를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-162">As an alternative to performing each of these downloads one by one, you can take advantage of the Web Platform Installer (Web PI).</span></span> <span data-ttu-id="2afc4-163">다음 주소에서 웹 PI를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-163">You can download the Web PI from the following address:</span></span>

[<span data-ttu-id="2afc4-164">https://www.asp.net/downloads/essential/</span><span class="sxs-lookup"><span data-stu-id="2afc4-164">https://www.asp.net/downloads/essential/</span></span>](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a><span data-ttu-id="2afc4-165">ASP.NET MVC 프로젝트</span><span class="sxs-lookup"><span data-stu-id="2afc4-165">ASP.NET MVC Project</span></span>

<span data-ttu-id="2afc4-166">ASP.NET MVC 웹 응용 프로그램 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-166">ASP.NET MVC Web Application Project.</span></span> <span data-ttu-id="2afc4-167">Visual Studio를 시작 하 고 메뉴 옵션을 선택 **파일, 새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-167">Launch Visual Studio and select the menu option **File, New Project**.</span></span> <span data-ttu-id="2afc4-168">**새 프로젝트** (그림 1 참조) 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-168">The **New Project** dialog appears (see Figure 1).</span></span> <span data-ttu-id="2afc4-169">선택 된 **웹** 프로젝트 형식 및 **ASP.NET MVC 웹 응용 프로그램** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="2afc4-169">Select the **Web** project type and the **ASP.NET MVC Web Application** template.</span></span> <span data-ttu-id="2afc4-170">새 프로젝트 이름을 *ContactManager* 확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-170">Name your new project *ContactManager* and click the OK button.</span></span>


<span data-ttu-id="2afc4-171">.NET Framework 3.5가 맨 위에 있는 드롭다운 목록에서 선택 했는지 확인의 오른쪽은 **새 프로젝트** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="2afc4-171">Make sure that you have .NET Framework 3.5 selected from the dropdown list at the top right of the **New Project** dialog.</span></span> <span data-ttu-id="2afc4-172">그렇지 않으면 t 성공한 ASP.NET MVC 웹 응용 프로그램 템플릿을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-172">Otherwise, the ASP.NET MVC Web Application template won t appear.</span></span>


<span data-ttu-id="2afc4-173">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image1.jpg)](iteration-1-create-the-application-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-173">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image1.jpg)](iteration-1-create-the-application-cs/_static/image1.png)</span></span>

<span data-ttu-id="2afc4-174">**그림 01**:의 새 프로젝트 대화 상자 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-174">**Figure 01**: The New Project dialog([Click to view full-size image](iteration-1-create-the-application-cs/_static/image2.png))</span></span>


<span data-ttu-id="2afc4-175">ASP.NET MVC 응용 프로그램의 **단위 테스트 프로젝트 만들기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-175">ASP.NET MVC application, the **Create Unit Test Project** dialog appears.</span></span> <span data-ttu-id="2afc4-176">이 대화 상자를 만들고 ASP.NET MVC 응용 프로그램을 만들 때 솔루션에 단위 테스트 프로젝트를 추가 지정할 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-176">You can use this dialog to indicate that you want to create and add a unit test project to your solution when you create your ASP.NET MVC application.</span></span> <span data-ttu-id="2afc4-177">T 성공한 있지만이 반복의 단위 테스트를 작성 하는 옵션을 선택 해야 **예, 단위 테스트 프로젝트 만들기** 이후의 반복에서 단위 테스트 추가 계획 이기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-177">Although we won t be building unit tests in this iteration, you should select the option **Yes, create a unit test project** because we plan to add unit tests in a later iteration.</span></span> <span data-ttu-id="2afc4-178">새 ASP.NET MVC 프로젝트를 처음 만들 때 테스트 프로젝트를 추가 합니다. ASP.NET MVC 프로젝트를 만든 후에 테스트 프로젝트를 추가 하는 보다 훨씬 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-178">Adding a Test project when you first create a new ASP.NET MVC project is much easier than adding a Test project after the ASP.NET MVC project has been created.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="2afc4-179">Visual Web Developer에서 테스트 프로젝트를 지원 하지 않으므로 Visual Web Developer를 사용 하는 경우 단위 테스트 프로젝트 만들기 대화 상자를 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-179">Because Visual Web Developer does not support Test projects, you do not get the Create Unit Test Project dialog when using Visual Web Developer.</span></span>


<span data-ttu-id="2afc4-180">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image2.jpg)](iteration-1-create-the-application-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-180">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image2.jpg)](iteration-1-create-the-application-cs/_static/image3.png)</span></span>

<span data-ttu-id="2afc4-181">**그림 02**: The 단위 테스트 프로젝트 만들기 대화 상자 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-181">**Figure 02**: The Create Unit Test Project dialog ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image4.png))</span></span>


<span data-ttu-id="2afc4-182">ASP.NET MVC 응용 프로그램 Visual Studio 솔루션 탐색기 창에 표시 됩니다 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="2afc4-182">ASP.NET MVC application appears in the Visual Studio Solution Explorer window (see Figure 3).</span></span> <span data-ttu-id="2afc4-183">T don 메뉴 옵션을 선택 하 여이 창을 열 수 있습니다 다음 솔루션 탐색기 창 표시 **보기, 솔루션 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-183">If you don t see the Solution Explorer window then you can open this window by selecting the menu option **View, Solution Explorer**.</span></span> <span data-ttu-id="2afc4-184">두 개의 프로젝트가 솔루션에 공지: ASP.NET MVC 프로젝트와 테스트 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-184">Notice that the solution contains two projects: the ASP.NET MVC project and the Test project.</span></span> <span data-ttu-id="2afc4-185">ASP.NET MVC 프로젝트 ContactManager 이름이 하 고 테스트 프로젝트 이름은 ContactManager.Tests 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-185">The ASP.NET MVC project is named ContactManager and the Test project is named ContactManager.Tests.</span></span>


<span data-ttu-id="2afc4-186">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image3.jpg)](iteration-1-create-the-application-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-186">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image3.jpg)](iteration-1-create-the-application-cs/_static/image5.png)</span></span>

<span data-ttu-id="2afc4-187">**그림 03**: 솔루션 탐색기 창 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-187">**Figure 03**: The Solution Explorer window ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image6.png))</span></span>


## <a name="deleting-the-project-sample-files"></a><span data-ttu-id="2afc4-188">프로젝트 샘플 파일 삭제</span><span class="sxs-lookup"><span data-stu-id="2afc4-188">Deleting the Project Sample Files</span></span>

<span data-ttu-id="2afc4-189">ASP.NET MVC 프로젝트 템플릿은 컨트롤러 및 뷰에 대 한 샘플 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-189">The ASP.NET MVC project template includes sample files for controllers and views.</span></span> <span data-ttu-id="2afc4-190">새 ASP.NET MVC 응용 프로그램을 만들기 전에 이러한 파일을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-190">Before creating a new ASP.NET MVC application, you should delete these files.</span></span> <span data-ttu-id="2afc4-191">파일 또는 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 하 여 솔루션 탐색기 창에서 파일 및 폴더를 삭제할 수 있습니다 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-191">You can delete files and folders in the Solution Explorer window by right-clicking a file or folder and selecting the menu option **Delete**.</span></span>

<span data-ttu-id="2afc4-192">ASP.NET MVC 프로젝트에서 다음 파일을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-192">You need to delete the following files from the ASP.NET MVC project:</span></span>

- <span data-ttu-id="2afc4-193">\Controllers\HomeController.cs</span><span class="sxs-lookup"><span data-stu-id="2afc4-193">\Controllers\HomeController.cs</span></span>

- <span data-ttu-id="2afc4-194">\Views\Home\About.aspx</span><span class="sxs-lookup"><span data-stu-id="2afc4-194">\Views\Home\About.aspx</span></span>

- <span data-ttu-id="2afc4-195">\Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="2afc4-195">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="2afc4-196">및 테스트 프로젝트에서 다음 파일을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-196">And, you need to delete the following file from the Test project:</span></span>

<span data-ttu-id="2afc4-197">\Controllers\HomeControllerTest.cs</span><span class="sxs-lookup"><span data-stu-id="2afc4-197">\Controllers\HomeControllerTest.cs</span></span>

## <a name="creating-the-database"></a><span data-ttu-id="2afc4-198">데이터베이스를 만드는 중</span><span class="sxs-lookup"><span data-stu-id="2afc4-198">Creating the Database</span></span>

<span data-ttu-id="2afc4-199">않아 응용 프로그램은 데이터베이스 기반 웹 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="2afc4-199">The Contact Manager application is a database-driven web application.</span></span> <span data-ttu-id="2afc4-200">상점 연락처 정보를 위해 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-200">We use a database to store the contact information.</span></span>

<span data-ttu-id="2afc4-201">Microsoft SQL Server, Oracle, MySQL 및 IBM DB2 데이터베이스를 비롯 한 최신 데이터베이스와 ASP.NET MVC 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-201">The ASP.NET MVC framework with any modern database including Microsoft SQL Server, Oracle, MySQL, and IBM DB2 databases.</span></span> <span data-ttu-id="2afc4-202">이 자습서에서는 Microsoft SQL Server 데이터베이스를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-202">In this tutorial, we use a Microsoft SQL Server database.</span></span> <span data-ttu-id="2afc4-203">Visual Studio를 설치 하면 Microsoft SQL Server 데이터베이스의 무료 버전인 Microsoft SQL Server Express를 설치 하는 옵션이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-203">When you install Visual Studio, you are provided with the option of installing Microsoft SQL Server Express which is a free version of the Microsoft SQL Server database.</span></span>

<span data-ttu-id="2afc4-204">응용 프로그램을 마우스 오른쪽 단추로 클릭 하 여 새 데이터베이스를 만들\_메뉴 옵션을 선택 하 고 솔루션 탐색기 창에서 데이터 폴더 **추가, 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-204">Create a new database by right-clicking the App\_Data folder in the Solution Explorer window and selecting the menu option **Add, New Item**.</span></span> <span data-ttu-id="2afc4-205">에 **새 항목 추가** 대화 상자에서는 **데이터** 범주 및 **SQL Server 데이터베이스** 서식 파일 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="2afc4-205">In the **Add New Item** dialog, select the **Data** category and the **SQL Server Database** template (see Figure 4).</span></span> <span data-ttu-id="2afc4-206">ContactManagerDB.mdf 새 데이터베이스 이름을 지정 하 고 확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-206">Name the new database ContactManagerDB.mdf and click the OK button.</span></span>


<span data-ttu-id="2afc4-207">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image4.jpg)](iteration-1-create-the-application-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-207">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image4.jpg)](iteration-1-create-the-application-cs/_static/image7.png)</span></span>

<span data-ttu-id="2afc4-208">**그림 04**: 새 Microsoft SQL Server Express 데이터베이스 만들기 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-208">**Figure 04**: Creating a new Microsoft SQL Server Express database ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image8.png))</span></span>


<span data-ttu-id="2afc4-209">데이터베이스 응용 프로그램에 표시 되는 새 데이터베이스를 만든 후\_솔루션 탐색기 창에서 데이터 폴더.</span><span class="sxs-lookup"><span data-stu-id="2afc4-209">After you create the new database, the database appears in the App\_Data folder in the Solution Explorer window.</span></span> <span data-ttu-id="2afc4-210">서버 탐색기 창을 열고 데이터베이스에 연결 하려면 ContactManager.mdf 파일을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-210">Double-click the ContactManager.mdf file to open the Server Explorer window and connect to the database.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="2afc4-211">서버 탐색기 창에서 Microsoft Visual Web Developer의 경우 데이터베이스 탐색기 창에 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-211">The Server Explorer window is called the Database Explorer window in the case of Microsoft Visual Web Developer.</span></span>


<span data-ttu-id="2afc4-212">데이터베이스 테이블, 뷰, 트리거, 저장된 프로시저와 같은 새 데이터베이스 개체를 만들 서버 탐색기 창에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-212">You can use the Server Explorer window to create new database objects such as database tables, views, triggers, and stored procedures.</span></span> <span data-ttu-id="2afc4-213">테이블 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **새 테이블 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-213">Right-click the Tables folder and select the menu option **Add New Table**.</span></span> <span data-ttu-id="2afc4-214">데이터베이스 테이블 디자이너 (그림 5 참조)가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-214">The Database Table Designer appears (see Figure 5).</span></span>


<span data-ttu-id="2afc4-215">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image5.jpg)](iteration-1-create-the-application-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-215">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image5.jpg)](iteration-1-create-the-application-cs/_static/image9.png)</span></span>

<span data-ttu-id="2afc4-216">**그림 05**: 데이터베이스 테이블 디자이너 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-216">**Figure 05**: The Database Table Designer ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image10.png))</span></span>


<span data-ttu-id="2afc4-217">같은 열이 포함 된 테이블을 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-217">We need to create a table that contains the following columns:</span></span>

<a id="0.1_table01"></a>


| <span data-ttu-id="2afc4-218">**열 이름**</span><span class="sxs-lookup"><span data-stu-id="2afc4-218">**Column Name**</span></span> | <span data-ttu-id="2afc4-219">**데이터 형식**</span><span class="sxs-lookup"><span data-stu-id="2afc4-219">**Data Type**</span></span> | <span data-ttu-id="2afc4-220">**Null 허용**</span><span class="sxs-lookup"><span data-stu-id="2afc4-220">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2afc4-221">ID</span><span class="sxs-lookup"><span data-stu-id="2afc4-221">Id</span></span> | <span data-ttu-id="2afc4-222">int</span><span class="sxs-lookup"><span data-stu-id="2afc4-222">int</span></span> | <span data-ttu-id="2afc4-223">false</span><span class="sxs-lookup"><span data-stu-id="2afc4-223">false</span></span> |
| <span data-ttu-id="2afc4-224">FirstName</span><span class="sxs-lookup"><span data-stu-id="2afc4-224">FirstName</span></span> | <span data-ttu-id="2afc4-225">Nvarchar (50)</span><span class="sxs-lookup"><span data-stu-id="2afc4-225">nvarchar(50)</span></span> | <span data-ttu-id="2afc4-226">false</span><span class="sxs-lookup"><span data-stu-id="2afc4-226">false</span></span> |
| <span data-ttu-id="2afc4-227">LastName</span><span class="sxs-lookup"><span data-stu-id="2afc4-227">LastName</span></span> | <span data-ttu-id="2afc4-228">Nvarchar (50)</span><span class="sxs-lookup"><span data-stu-id="2afc4-228">nvarchar(50)</span></span> | <span data-ttu-id="2afc4-229">false</span><span class="sxs-lookup"><span data-stu-id="2afc4-229">false</span></span> |
| <span data-ttu-id="2afc4-230">전화 번호</span><span class="sxs-lookup"><span data-stu-id="2afc4-230">Phone</span></span> | <span data-ttu-id="2afc4-231">Nvarchar (50)</span><span class="sxs-lookup"><span data-stu-id="2afc4-231">nvarchar(50)</span></span> | <span data-ttu-id="2afc4-232">false</span><span class="sxs-lookup"><span data-stu-id="2afc4-232">false</span></span> |
| <span data-ttu-id="2afc4-233">메일</span><span class="sxs-lookup"><span data-stu-id="2afc4-233">Email</span></span> | <span data-ttu-id="2afc4-234">nvarchar (255)</span><span class="sxs-lookup"><span data-stu-id="2afc4-234">nvarchar(255)</span></span> | <span data-ttu-id="2afc4-235">false</span><span class="sxs-lookup"><span data-stu-id="2afc4-235">false</span></span> |


<span data-ttu-id="2afc4-236">첫 번째 열, Id 열은 특별 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-236">The first column, the Id column, is special.</span></span> <span data-ttu-id="2afc4-237">Id 열을 Id 열 및 기본 키 열으로 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-237">You need to mark the Id column as an Identity column and a Primary Key column.</span></span> <span data-ttu-id="2afc4-238">열 속성 (그림 6의 맨 아래에 검색)를 확장 하 고 Id 사양 속성 아래로 스크롤 하 여 열이 Identity 열 임을 나타낼 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-238">You indicate that a column is an Identity column by expanding Column Properites (look at the bottom of Figure 6) and scrolling down to the Identity Specification property.</span></span> <span data-ttu-id="2afc4-239">설정의 **(Id)** 속성 값을 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-239">Set the **(Is Identity)** property to the value **Yes**.</span></span>

<span data-ttu-id="2afc4-240">열을 선택 하는 키 아이콘이 있는 단추를 클릭 하 여 기본 키 열으로 열을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-240">You mark a column as a Primary Key column by selecting the column and clicking the button with the icon of a key.</span></span> <span data-ttu-id="2afc4-241">열은 기본 키 열으로 표시 되 면 키 아이콘이 열 옆에 나타납니다 (그림 6 참조).</span><span class="sxs-lookup"><span data-stu-id="2afc4-241">After a column is marked as a Primary Key column, an icon of a key appears next to the column (see Figure 6).</span></span>

<span data-ttu-id="2afc4-242">테이블 생성을 완료 한 후 새 테이블을 저장 하려면 저장 단추 (플로피의 아이콘이 있는 단추)를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-242">After you finish creating the table, click the Save button (the button with an icon of a floppy) to save the new table.</span></span> <span data-ttu-id="2afc4-243">새 테이블 이름을 *연락처*합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-243">Give your new table the name *Contacts*.</span></span>

<span data-ttu-id="2afc4-244">연락처 데이터베이스 테이블 만들기를 클릭 한 후 테이블에 일부 레코드를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-244">After finish creating the Contacts database table, you should add some records to the table.</span></span> <span data-ttu-id="2afc4-245">서버 탐색기 창에서 Contacts 테이블을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **테이블 데이터 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-245">Right-click the Contacts table in the Server Explorer window and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="2afc4-246">에 표시 된 표에서 하나 이상의 연락처를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-246">Enter one or more contacts in the grid that appears.</span></span>

## <a name="creating-the-data-model"></a><span data-ttu-id="2afc4-247">데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="2afc4-247">Creating the Data Model</span></span>

<span data-ttu-id="2afc4-248">ASP.NET MVC 응용 프로그램 모델, 뷰 및 컨트롤러 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-248">The ASP.NET MVC application consists of Models, Views, and Controllers.</span></span> <span data-ttu-id="2afc4-249">이전 섹션에서 만든 연락처 테이블을 나타내는 모델 클래스를 만들어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-249">We start by creating a Model class that represents the Contacts table that we created in the previous section.</span></span>

<span data-ttu-id="2afc4-250">이 자습서에서 사용 하 여 Microsoft Entity Framework 데이터베이스에서 모델 클래스를 자동으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-250">In this tutorial, we use the Microsoft Entity Framework to generate a model class from the database automatically.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="2afc4-251">ASP.NET MVC 프레임 워크는 어떤 방식으로든에서 Microsoft Entity Framework 연결 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-251">The ASP.NET MVC framework is not tied to the Microsoft Entity Framework in any way.</span></span> <span data-ttu-id="2afc4-252">ASP.NET MVC와 LINQ to SQL 또는 ADO.NET NHibernate를 포함 하 여 다른 데이터베이스 액세스 기술을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-252">You can use ASP.NET MVC with alternative database access technologies including NHibernate, LINQ to SQL, or ADO.NET.</span></span>


<span data-ttu-id="2afc4-253">데이터 모델 클래스를 만드는 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-253">Follow these steps to create the data model classes:</span></span>

1. <span data-ttu-id="2afc4-254">솔루션 탐색기 창에 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가, 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-254">Right-click the Models folder in the Solution Explorer window and select **Add, New Item**.</span></span> <span data-ttu-id="2afc4-255">**새 항목 추가** (그림 6 참조) 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-255">The **Add New Item** dialog appears (see Figure 6).</span></span>
2. <span data-ttu-id="2afc4-256">선택 된 **데이터** 범주 및 **ADO.NET 엔터티 데이터 모델** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="2afc4-256">Select the **Data** category and the **ADO.NET Entity Data Model** template.</span></span> <span data-ttu-id="2afc4-257">데이터 모델 이름을 *ContactManagerModel.edmx* 클릭는 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-257">Name your data model *ContactManagerModel.edmx* and click the **Add** button.</span></span> <span data-ttu-id="2afc4-258">엔터티 데이터 모델 마법사 (그림 7 참조)가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-258">The Entity Data Model wizard appears (see Figure 7).</span></span>
3. <span data-ttu-id="2afc4-259">에 **모델 콘텐츠 선택** 단계에서는 **데이터베이스에서 생성** (그림 7 참조).</span><span class="sxs-lookup"><span data-stu-id="2afc4-259">In the **Choose Model Contents** step, select **Generate from database** (see Figure 7).</span></span>
4. <span data-ttu-id="2afc4-260">에 **데이터 연결 선택** 단계 ContactManagerDB.mdf 데이터베이스를 선택 하 고 이름을 입력 *ContactManagerDBEntities* 엔터티 연결 설정 (그림 8 참조).</span><span class="sxs-lookup"><span data-stu-id="2afc4-260">In the **Choose Your Data Connection** step, select the ContactManagerDB.mdf database and enter the name *ContactManagerDBEntities* for the Entity Connection Settings (see Figure 8).</span></span>
5. <span data-ttu-id="2afc4-261">에 **데이터베이스 개체 선택** 단계, 테이블 (그림 9 참조) 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-261">In the **Choose Your Database Objects** step, select the checkbox labeled Tables (see Figure 9).</span></span> <span data-ttu-id="2afc4-262">데이터 모델 (에 하나 또는 Contacts 테이블) 데이터베이스에 포함 된 모든 테이블이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-262">The data model will include all tables contained in your database (there is just one, the Contacts table).</span></span> <span data-ttu-id="2afc4-263">네임 스페이스를 입력 *모델*합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-263">Enter the namespace *Models*.</span></span> <span data-ttu-id="2afc4-264">마법사를 완료 하려면 "마침" 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-264">Click the Finish button to complete the wizard.</span></span>


<span data-ttu-id="2afc4-265">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image6.jpg)](iteration-1-create-the-application-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-265">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image6.jpg)](iteration-1-create-the-application-cs/_static/image11.png)</span></span>

<span data-ttu-id="2afc4-266">**그림 06**: 새 항목 추가 대화 상자 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-266">**Figure 06**: The Add New Item dialog ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image12.png))</span></span>


<span data-ttu-id="2afc4-267">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image7.jpg)](iteration-1-create-the-application-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-267">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image7.jpg)](iteration-1-create-the-application-cs/_static/image13.png)</span></span>

<span data-ttu-id="2afc4-268">**그림 07**: Model 콘텐츠 선택 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-268">**Figure 07**: Choose Model Contents ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image14.png))</span></span>


<span data-ttu-id="2afc4-269">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image8.jpg)](iteration-1-create-the-application-cs/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-269">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image8.jpg)](iteration-1-create-the-application-cs/_static/image15.png)</span></span>

<span data-ttu-id="2afc4-270">**그림 08**: 데이터 연결 선택 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-270">**Figure 08**: Choose Your Data Connection ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image16.png))</span></span>


<span data-ttu-id="2afc4-271">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image9.jpg)](iteration-1-create-the-application-cs/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-271">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image9.jpg)](iteration-1-create-the-application-cs/_static/image17.png)</span></span>

<span data-ttu-id="2afc4-272">**그림 09**: 데이터베이스 개체 선택 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-272">**Figure 09**: Choose Your Database Objects ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image18.png))</span></span>


<span data-ttu-id="2afc4-273">엔터티 데이터 모델 마법사를 완료 한 후에 엔터티 데이터 모델 디자이너 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-273">After you complete the Entity Data Model Wizard, the Entity Data Model Designer appears.</span></span> <span data-ttu-id="2afc4-274">디자이너 모델링 되 고 각 테이블에 해당 하는 클래스를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-274">The designer displays a class that corresponds to each table being modeled.</span></span> <span data-ttu-id="2afc4-275">연락처 라는 하나의 클래스에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-275">You should see one class named Contacts.</span></span>

<span data-ttu-id="2afc4-276">엔터티 데이터 모델 마법사를 데이터베이스 테이블 이름에 따라 클래스 이름을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-276">The Entity Data Model wizard generates class names based on database table names.</span></span> <span data-ttu-id="2afc4-277">거의 항상 마법사에서 생성 되는 클래스의 이름을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-277">You almost always need to change the name of the class generated by the wizard.</span></span> <span data-ttu-id="2afc4-278">연락처 클래스 디자이너에서 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **이름 바꾸기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-278">Right-click the Contacts class in the designer and select the menu option **Rename**.</span></span> <span data-ttu-id="2afc4-279">클래스의 이름을 연락처 (복수)에서 연락처 (단 수)를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-279">Change the name of the class from Contacts (plural) to Contact (singular).</span></span> <span data-ttu-id="2afc4-280">클래스 이름을 변경 하 고 나면 그림 10과 같은 클래스가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-280">After you change the class name, the class should appear like Figure 10.</span></span>


<span data-ttu-id="2afc4-281">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image10.jpg)](iteration-1-create-the-application-cs/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-281">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image10.jpg)](iteration-1-create-the-application-cs/_static/image19.png)</span></span>

<span data-ttu-id="2afc4-282">**그림 10**: Contact The 클래스 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-282">**Figure 10**: The Contact class ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image20.png))</span></span>


<span data-ttu-id="2afc4-283">이 시점에서 예제의 데이터베이스 모델을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-283">At this point, we have created our database model.</span></span> <span data-ttu-id="2afc4-284">데이터베이스에 특정 연락처 레코드를 나타내기 위해 연락처 클래스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-284">We can use the Contact class to represent a particular contact record in our database.</span></span>

## <a name="creating-the-home-controller"></a><span data-ttu-id="2afc4-285">홈 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="2afc4-285">Creating the Home Controller</span></span>

<span data-ttu-id="2afc4-286">다음 단계는 우리의 Home 컨트롤러를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-286">The next step is to create our Home controller.</span></span> <span data-ttu-id="2afc4-287">Home 컨트롤러는 ASP.NET MVC 응용 프로그램에서 호출 되는 기본 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-287">The Home controller is the default controller invoked in an ASP.NET MVC application.</span></span>

<span data-ttu-id="2afc4-288">솔루션 탐색기 창에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 하 여 홈 컨트롤러 클래스 만들기 **추가, 컨트롤러** (11 그림 참조).</span><span class="sxs-lookup"><span data-stu-id="2afc4-288">Create the Home controller class by right-clicking the Controllers folder in the Solution Explorer window and selecting the menu option **Add, Controller** (see Figure 11).</span></span> <span data-ttu-id="2afc4-289">확인란 확인 **만들기, 업데이트 및 세부 정보 시나리오에 대 한 작업 메서드를 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-289">Notice the checkbox labeled **Add action methods for Create, Update, and Details scenarios**.</span></span> <span data-ttu-id="2afc4-290">클릭 하기 전에 선택 되어 있는지 확인은 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-290">Make sure that this checkbox is checked before clicking the **Add** button.</span></span>


<span data-ttu-id="2afc4-291">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image11.jpg)](iteration-1-create-the-application-cs/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-291">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image11.jpg)](iteration-1-create-the-application-cs/_static/image21.png)</span></span>

<span data-ttu-id="2afc4-292">**그림 11**: Home 컨트롤러를 추가 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image22.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-292">**Figure 11**: Adding the Home controller ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image22.png))</span></span>


<span data-ttu-id="2afc4-293">Home 컨트롤러를 만들 때에 목록 1의 클래스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-293">When you create the Home controller, you get the class in Listing 1.</span></span>

<span data-ttu-id="2afc4-294">**1-Controllers\HomeController.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="2afc4-294">**Listing 1 - Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample1.cs)]

## <a name="listing-the-contacts"></a><span data-ttu-id="2afc4-295">연락처를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-295">Listing the Contacts</span></span>

<span data-ttu-id="2afc4-296">연락처 데이터베이스 테이블에 레코드를 표시 하려면 index () 작업 및 인덱스 보기 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-296">In order to display the records in the Contacts database table, we need to create an Index() action and an Index view.</span></span>

<span data-ttu-id="2afc4-297">Home 컨트롤러 index () 작업을 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-297">The Home controller already contains an Index() action.</span></span> <span data-ttu-id="2afc4-298">이 메서드를 나열 하는 2의 모양 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-298">We need to modify this method so that it looks like Listing 2.</span></span>

<span data-ttu-id="2afc4-299">**2-Controllers\HomeController.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="2afc4-299">**Listing 2 - Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample2.cs)]

<span data-ttu-id="2afc4-300">목록 2의 홈 컨트롤러 클래스 라는 private 필드가 들어 \_엔터티.</span><span class="sxs-lookup"><span data-stu-id="2afc4-300">Notice that the Home controller class in Listing 2 contains a private field named \_entities.</span></span> <span data-ttu-id="2afc4-301">\_엔터티 필드의 데이터 모델에서 엔터티를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-301">The \_entities field represents the entities from the data model.</span></span> <span data-ttu-id="2afc4-302">사용 하 여는 \_엔터티 필드는 데이터베이스와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-302">We use the \_entities field to communicate with the database.</span></span>

<span data-ttu-id="2afc4-303">Index () 메서드를 나타내는 모든 연락처 연락처 데이터베이스 테이블 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-303">The Index() method returns a view that represents all of the contacts from the Contacts database table.</span></span> <span data-ttu-id="2afc4-304">식 \_엔터티. ContactSet.ToList() 제네릭 목록으로 연락처 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-304">The expression \_entities.ContactSet.ToList() returns the list of contacts as a generic list.</span></span>

<span data-ttu-id="2afc4-305">해당 म 것은 사용 이제 했습니다 인덱스 컨트롤러를 만든 다음 인덱스 뷰를 만들 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-305">Now that we ve created the Index controller, we next need to create the Index view.</span></span> <span data-ttu-id="2afc4-306">인덱스 뷰를 만들기 전에 메뉴 옵션을 선택 하 여 응용 프로그램을 컴파일하 **빌드, 솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-306">Before creating the Index view, compile your application by selecting the menu option **Build, Build Solution**.</span></span> <span data-ttu-id="2afc4-307">모델 클래스 목록에 표시 하려면 보기를 추가 하기 전에 프로젝트를 컴파일하여 항상는 **뷰 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="2afc4-307">You should always compile your project before adding a view in order for the list of model classes to be displayed in the **Add View** dialog.</span></span>

<span data-ttu-id="2afc4-308">Index () 메서드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 하 여 인덱스 뷰를 만들면 **뷰 추가** (그림 12 참조).</span><span class="sxs-lookup"><span data-stu-id="2afc4-308">You create the Index view by right-clicking the Index() method and selecting the menu option **Add View** (see Figure 12).</span></span> <span data-ttu-id="2afc4-309">이 메뉴 옵션을 선택 하면 열립니다는 **뷰 추가** 대화 상자 (그림 13 참조).</span><span class="sxs-lookup"><span data-stu-id="2afc4-309">Selecting this menu option opens the **Add View** dialog (see Figure 13).</span></span>


<span data-ttu-id="2afc4-310">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image12.jpg)](iteration-1-create-the-application-cs/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-310">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image12.jpg)](iteration-1-create-the-application-cs/_static/image23.png)</span></span>

<span data-ttu-id="2afc4-311">**그림 12**: 인덱스 뷰 추가 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-311">**Figure 12**: Adding the Index view ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image24.png))</span></span>


<span data-ttu-id="2afc4-312">에 **뷰 추가** 대화 상자에서 확인란 확인 **강력한 형식의 뷰 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-312">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="2afc4-313">데이터 클래스 ContactManager.Models.Contact 보기와 보기 콘텐츠 목록을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-313">Select the View data class ContactManager.Models.Contact and the View content List.</span></span> <span data-ttu-id="2afc4-314">이러한 옵션을 선택 하면 연락처 레코드를 표시 하는 보기를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-314">Selecting these options generates a view that displays a list of Contact records.</span></span>


<span data-ttu-id="2afc4-315">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image13.jpg)](iteration-1-create-the-application-cs/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-315">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image13.jpg)](iteration-1-create-the-application-cs/_static/image25.png)</span></span>

<span data-ttu-id="2afc4-316">**그림 13**: 뷰 추가 대화 상자 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image26.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-316">**Figure 13**: The Add View dialog ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image26.png))</span></span>


<span data-ttu-id="2afc4-317">클릭는 **추가** 단추, 목록 3에서 인덱스 뷰 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-317">When you click the **Add** button, the Index view in Listing 3 is generated.</span></span> <span data-ttu-id="2afc4-318">공지는 &lt;% @ 페이지 %&gt; 지시문을 파일의 맨 위에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-318">Notice the &lt;%@ Page %&gt; directive that appears at the top of the file.</span></span> <span data-ttu-id="2afc4-319">인덱스 뷰는 ViewPage에서 상속&lt;IEnumerable&lt;ContactManager.Models.Contact&gt; &gt; 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-319">The Index view inherits from the ViewPage&lt;IEnumerable&lt;ContactManager.Models.Contact&gt;&gt; class.</span></span> <span data-ttu-id="2afc4-320">즉, 보기에서 모델 클래스 연락처 엔터티 목록을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-320">In other words, the Model class in the view represents a list of Contact entities.</span></span>

<span data-ttu-id="2afc4-321">인덱스 뷰의 본문 모델 클래스를 나타내는 연락처의 각 반복 하는 foreach 루프를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-321">The body of the Index view contains a foreach loop that iterates through each of the contacts represented by the Model class.</span></span> <span data-ttu-id="2afc4-322">연락처 클래스의 각 속성의 값은 HTML 테이블 내에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-322">The value of each property of the Contact class is displayed within an HTML table.</span></span>

<span data-ttu-id="2afc4-323">**3-Views\Home\Index.aspx (수정 되지 않은)를 나열 합니다.**</span><span class="sxs-lookup"><span data-stu-id="2afc4-323">**Listing 3 - Views\Home\Index.aspx (unmodified)**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample3.aspx)]

<span data-ttu-id="2afc4-324">가지 인덱스 뷰를 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-324">We need to make one modification to the Index view.</span></span> <span data-ttu-id="2afc4-325">세부 정보 보기를 만드는 하지 것 때문에 세부 정보 링크를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-325">Because we are not creating a Details view, we can remove the Details link.</span></span> <span data-ttu-id="2afc4-326">찾기 및 인덱스 보기에서 다음 코드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-326">Find and remove the following code from the Index view:</span></span>

<span data-ttu-id="2afc4-327">{id = 항목입니다. Id가}) %&gt;</span><span class="sxs-lookup"><span data-stu-id="2afc4-327">{ id=item.Id })%&gt;</span></span>

<span data-ttu-id="2afc4-328">인덱스 뷰를 수정한 후에 연락처 관리자 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-328">After you modify the Index view, you can run the Contact Manager application.</span></span> <span data-ttu-id="2afc4-329">디버깅 시작 메뉴 옵션 디버그을 선택 하거나 단순히 F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-329">Select the menu option Debug, Start Debugging or simply press F5.</span></span> <span data-ttu-id="2afc4-330">처음에 응용 프로그램을 실행할 때 얻게 대화 상자 그림 14에서입니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-330">The first time you run the application, you get the dialog in Figure 14.</span></span> <span data-ttu-id="2afc4-331">옵션을 선택 **디버깅할 수 있도록 Web.config 파일을 수정** 확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-331">Select the option **Modify the Web.config file to enable debugging** and click the OK button.</span></span>


<span data-ttu-id="2afc4-332">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image14.jpg)](iteration-1-create-the-application-cs/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-332">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image14.jpg)](iteration-1-create-the-application-cs/_static/image27.png)</span></span>

<span data-ttu-id="2afc4-333">**그림 14**: 디버깅 사용 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image28.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-333">**Figure 14**: Enabling debugging ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image28.png))</span></span>


<span data-ttu-id="2afc4-334">인덱스 뷰는 기본적으로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-334">The Index view is returned by default.</span></span> <span data-ttu-id="2afc4-335">이 보기의 모든 연락처 데이터베이스 테이블에서 데이터를 나열 합니다 (그림 15 참조).</span><span class="sxs-lookup"><span data-stu-id="2afc4-335">This view lists all of the data from the Contacts database table (see Figure 15).</span></span>


<span data-ttu-id="2afc4-336">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image15.jpg)](iteration-1-create-the-application-cs/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-336">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image15.jpg)](iteration-1-create-the-application-cs/_static/image29.png)</span></span>

<span data-ttu-id="2afc4-337">**그림 15**: The 인덱스 보기 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image30.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-337">**Figure 15**: The Index view ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image30.png))</span></span>


<span data-ttu-id="2afc4-338">인덱스 뷰 보기의 맨 아래에 새로 만들기를 레이블이 지정 된 링크가 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-338">Notice that the Index view includes a link labeled Create New at the bottom of the view.</span></span> <span data-ttu-id="2afc4-339">다음 섹션에서는 새 연락처를 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-339">In the next section, you learn how to create new contacts.</span></span>

## <a name="creating-new-contacts"></a><span data-ttu-id="2afc4-340">새 연락처 만들기</span><span class="sxs-lookup"><span data-stu-id="2afc4-340">Creating New Contacts</span></span>

<span data-ttu-id="2afc4-341">사용자가 새 연락처를 만들 수 있도록 홈 컨트롤러에 두 개의 create () 작업을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-341">To enable users to create new contacts, we need to add two Create() actions to the Home controller.</span></span> <span data-ttu-id="2afc4-342">새 연락처를 만들기 위한 HTML 폼을 반환 하는 하나의 create () 동작을 만들려면 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-342">We need to create one Create() action that returns an HTML form for creating a new contact.</span></span> <span data-ttu-id="2afc4-343">새 연락처의 실제 데이터베이스 삽입을 수행 하는 두 번째 create () 작업을 만들기 위해 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-343">We need to create a second Create() action that performs the actual database insert of the new contact.</span></span>

<span data-ttu-id="2afc4-344">홈 컨트롤러에 추가 해야 하는 새 create () 메서드 목록 4에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-344">The new Create() methods that we need to add to the Home controller are contained in Listing 4.</span></span>

<span data-ttu-id="2afc4-345">**4-Controllers\HomeController.cs (메서드로 만들기)를 나열합니다.**</span><span class="sxs-lookup"><span data-stu-id="2afc4-345">**Listing 4 - Controllers\HomeController.cs (with Create methods)**</span></span>

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample4.cs)]

<span data-ttu-id="2afc4-346">HTTP POST에서만 두 번째 create () 메서드를 호출할 수 있습니다 하는 동안 HTTP GET와 첫 번째 create () 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-346">The first Create() method can be invoked with an HTTP GET while the second Create() method can be invoked only by an HTTP POST.</span></span> <span data-ttu-id="2afc4-347">즉, HTML 폼 게시 하는 경우에 두 번째 create () 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-347">In other words, the second Create() method can be invoked only when posting an HTML form.</span></span> <span data-ttu-id="2afc4-348">첫 번째 create () 메서드는 단순히 새 연락처를 만들기 위한 HTML 폼을 포함 하는 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-348">The first Create() method simply returns a view that contains the HTML form for creating a new contact.</span></span> <span data-ttu-id="2afc4-349">두 번째 create () 메서드는 훨씬 더 흥미로운: 데이터베이스에 새 연락처를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-349">The second Create() method is much more interesting: it adds the new contact to the database.</span></span>

<span data-ttu-id="2afc4-350">공지를 두 번째 create () 메서드는 연락처 클래스의 인스턴스를 허용 하도록 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-350">Notice that the second Create() method has been modified to accept an instance of the Contact class.</span></span> <span data-ttu-id="2afc4-351">HTML 양식 으로부터 게시 된 양식 값은 자동으로 ASP.NET MVC 프레임 워크에서이 연락처 클래스에 바인딩된 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-351">The form values posted from the HTML form are bound to this Contact class by the ASP.NET MVC framework automatically.</span></span> <span data-ttu-id="2afc4-352">양식 HTML 만들기에서 각 양식 필드의 연락처 매개 변수 속성에 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-352">Each form field from the HTML Create form is assigned to a property of the Contact parameter.</span></span>

<span data-ttu-id="2afc4-353">연락처 매개 변수 [바인드] 특성으로 데코레이팅되 어 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-353">Notice that the Contact parameter is decorated with a [Bind] attribute.</span></span> <span data-ttu-id="2afc4-354">바인딩에서 연락처 Id 속성을 제외 하려면 [Bind] 속성 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-354">The [Bind] attribute is used to exclude the Contact Id property from binding.</span></span> <span data-ttu-id="2afc4-355">Id 속성 Identity 속성을 나타내므로 Id 속성을 설정 하려면 원하지를 않는 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-355">Because the Id property represents an Identity property, we don t want to set the Id property.</span></span>

<span data-ttu-id="2afc4-356">Create () 메서드 본문에서 Entity Framework 데이터베이스에 새 연락처 삽입에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-356">In the body of the Create() method, the Entity Framework is used to insert the new Contact into the database.</span></span> <span data-ttu-id="2afc4-357">새 연락처가 연락처의 기존 세트에 추가 하 고 savechanges () 메서드를 호출 기본 데이터베이스에 이러한 변경 내용 다시 적용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-357">The new Contact is added to the existing set of Contacts and the SaveChanges() method is called to push these changes back to the underlying database.</span></span>

<span data-ttu-id="2afc4-358">두 create () 방법 중 하나를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 하 여 새 연락처 만들기에 대 한 HTML 폼을 생성할 수 있습니다 **뷰 추가** (16 그림 참조).</span><span class="sxs-lookup"><span data-stu-id="2afc4-358">You can generate an HTML form for creating new Contacts by right-clicking either of the two Create() methods and selecting the menu option **Add View** (see Figure 16).</span></span>


<span data-ttu-id="2afc4-359">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image16.jpg)](iteration-1-create-the-application-cs/_static/image31.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-359">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image16.jpg)](iteration-1-create-the-application-cs/_static/image31.png)</span></span>

<span data-ttu-id="2afc4-360">**그림 16**: 만들기 뷰 추가 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image32.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-360">**Figure 16**: Adding the Create view ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image32.png))</span></span>


<span data-ttu-id="2afc4-361">에 **뷰 추가** 대화 상자에서는 **ContactManager.Models.Contact** 클래스 및 **만들기** 콘텐츠 보기에 대 한 옵션 (그림 17 참조).</span><span class="sxs-lookup"><span data-stu-id="2afc4-361">In the **Add View** dialog, select the **ContactManager.Models.Contact** class and the **Create** option for view content (see Figure 17).</span></span> <span data-ttu-id="2afc4-362">클릭는 **추가** 단추는 Create view 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-362">When you click the **Add** button, a Create view is generated automatically.</span></span>


<span data-ttu-id="2afc4-363">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image17.jpg)](iteration-1-create-the-application-cs/_static/image33.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-363">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image17.jpg)](iteration-1-create-the-application-cs/_static/image33.png)</span></span>

<span data-ttu-id="2afc4-364">**그림 17**: 분해 페이지가 표시 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image34.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-364">**Figure 17**: Seeing a page explode ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image34.png))</span></span>


<span data-ttu-id="2afc4-365">만들기 뷰는 각 연락처 클래스의 속성에 대 한 양식 필드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-365">The Create view contains form fields for each of the properties of the Contact class.</span></span> <span data-ttu-id="2afc4-366">뷰 만들기에 대 한 코드 목록 5에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-366">The code for the Create view is included in Listing 5.</span></span>

<span data-ttu-id="2afc4-367">**5-Views\Home\Create.aspx 나열**</span><span class="sxs-lookup"><span data-stu-id="2afc4-367">**Listing 5 - Views\Home\Create.aspx**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample5.aspx)]

<span data-ttu-id="2afc4-368">Create () 메서드를 수정 하 고 만들기 뷰 추가 후에 연락처 Manger 응용 프로그램을 실행 하 고 새 연락처를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-368">After you modify the Create() methods and add the Create view, you can run the Contact Manger application and create new contacts.</span></span> <span data-ttu-id="2afc4-369">클릭는 **새로 만들기** 만들기 보기로 이동 하도록 인덱스 보기에 표시 되는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-369">Click the **Create New** link that appears in the Index view to navigate to the Create view.</span></span> <span data-ttu-id="2afc4-370">그림 18에서 보기를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-370">You should see the view in Figure 18.</span></span>


<span data-ttu-id="2afc4-371">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image18.jpg)](iteration-1-create-the-application-cs/_static/image35.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-371">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image18.jpg)](iteration-1-create-the-application-cs/_static/image35.png)</span></span>

<span data-ttu-id="2afc4-372">**그림 18**: The Create View ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image36.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-372">**Figure 18**: The Create View ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image36.png))</span></span>


## <a name="editing-contacts"></a><span data-ttu-id="2afc4-373">연락처를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-373">Editing Contacts</span></span>

<span data-ttu-id="2afc4-374">연락처 레코드를 편집 하기 위한 기능 추가 기능 새 연락처 레코드를 만들기 위한 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-374">Adding the functionality for editing a contact record is very similar to adding the functionality for creating new contact records.</span></span> <span data-ttu-id="2afc4-375">먼저, 홈 컨트롤러 클래스에 두 개의 새 편집 메서드를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-375">First, we need to add two new Edit methods to the Home controller class.</span></span> <span data-ttu-id="2afc4-376">이러한 새 Edit() 메서드 목록 6에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-376">These new Edit() methods are contained in Listing 6.</span></span>

<span data-ttu-id="2afc4-377">**6-Controllers\HomeController.cs (메서드로 편집)를 나열합니다.**</span><span class="sxs-lookup"><span data-stu-id="2afc4-377">**Listing 6 - Controllers\HomeController.cs (with Edit methods)**</span></span>

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample6.cs)]

<span data-ttu-id="2afc4-378">첫 번째 Edit() 메서드는 HTTP GET 작업에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-378">The first Edit() method is invoked by an HTTP GET operation.</span></span> <span data-ttu-id="2afc4-379">Id 매개 변수를 편집 하 고 연락처 레코드의 Id를 나타내는이 메서드에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-379">An Id parameter is passed to this method which represents the Id of the contact record being edited.</span></span> <span data-ttu-id="2afc4-380">Entity Framework는 id와 일치 하는 연락처를 검색 하는 데 사용 됩니다. 레코드 편집에 대 한 HTML 폼을 포함 하는 뷰 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-380">The Entity Framework is used to retrieve a contact that matches the Id. A view that contains an HTML form for editing a record is returned.</span></span>

<span data-ttu-id="2afc4-381">두 번째 Edit() 메서드는 데이터베이스에 대 한 실제 업데이트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-381">The second Edit() method performs the actual update to the database.</span></span> <span data-ttu-id="2afc4-382">이 메서드는 연락처 클래스의 인스턴스를 매개 변수로 받아들입니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-382">This method accepts an instance of the Contact class as a parameter.</span></span> <span data-ttu-id="2afc4-383">ASP.NET MVC 프레임 워크가 바인딩합니다 양식 필드 편집 폼에서이 클래스에 자동으로.</span><span class="sxs-lookup"><span data-stu-id="2afc4-383">The ASP.NET MVC framework binds the form fields from the Edit form to this class automatically.</span></span> <span data-ttu-id="2afc4-384">T 않으려는 공지 (Id 속성의 값 필요) 연락처를 편집할 때 [바인드] 특성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-384">Notice that you don t include the[Bind] attribute when editing a Contact (we need the value of the Id property).</span></span>

<span data-ttu-id="2afc4-385">Entity Framework는 수정 된 연락처 데이터베이스에 저장 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-385">The Entity Framework is used to save the modified Contact to the database.</span></span> <span data-ttu-id="2afc4-386">원래 연락처를 데이터베이스에서 먼저 검색 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-386">The original Contact must be retrieved from the database first.</span></span> <span data-ttu-id="2afc4-387">다음으로, Entity Framework ApplyPropertyChanges() 메서드 연락처에 변경 내용을 기록할 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-387">Next, the Entity Framework ApplyPropertyChanges() method is called to record the changes to the Contact.</span></span> <span data-ttu-id="2afc4-388">마지막으로, Entity Framework savechanges () 메서드는 기본 데이터베이스에 변경 내용을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-388">Finally, the Entity Framework SaveChanges() method is called to persist the changes to the underlying database.</span></span>

<span data-ttu-id="2afc4-389">Edit() 메서드를 마우스 오른쪽 단추로 클릭 하 고 추가 보기 메뉴 옵션을 선택 하 여 편집 폼을 포함 하는 보기를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-389">You can generate the view that contains the Edit form by right-clicking the Edit() method and selecting the menu option Add View.</span></span> <span data-ttu-id="2afc4-390">뷰 추가 대화 상자에서 선택 된 **ContactManager.Models.Contact** 클래스 및 **편집** 콘텐츠를 볼 (그림 19 참조).</span><span class="sxs-lookup"><span data-stu-id="2afc4-390">In the Add View dialog, select the **ContactManager.Models.Contact** class and the **Edit** view content (see Figure 19).</span></span>


<span data-ttu-id="2afc4-391">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image19.jpg)](iteration-1-create-the-application-cs/_static/image37.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-391">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image19.jpg)](iteration-1-create-the-application-cs/_static/image37.png)</span></span>

<span data-ttu-id="2afc4-392">**그림 19**: 편집 뷰 추가 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image38.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-392">**Figure 19**: Adding an Edit View ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image38.png))</span></span>


<span data-ttu-id="2afc4-393">추가 단추를 클릭 하면 새 편집 뷰를 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-393">When you click the Add button, a new Edit view is generated automatically.</span></span> <span data-ttu-id="2afc4-394">생성 되는 HTML 폼에는 각 연락처 클래스 (참조 목록 7)의 속성에 해당 하는 필드가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-394">The HTML form that is generated contains fields that correspond to each of the properties of the Contact class (see Listing 7).</span></span>

<span data-ttu-id="2afc4-395">**7-Views\Home\Edit.aspx 나열**</span><span class="sxs-lookup"><span data-stu-id="2afc4-395">**Listing 7 - Views\Home\Edit.aspx**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample7.aspx)]

## <a name="deleting-contacts"></a><span data-ttu-id="2afc4-396">연락처 삭제</span><span class="sxs-lookup"><span data-stu-id="2afc4-396">Deleting Contacts</span></span>

<span data-ttu-id="2afc4-397">연락처를 삭제 하려면 홈 컨트롤러 클래스에 두 개의 delete () 작업을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-397">If you want to delete contacts then you need to add two Delete() actions to the Home controller class.</span></span> <span data-ttu-id="2afc4-398">첫 번째 delete () 작업 삭제 확인 폼이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-398">The first Delete() action displays a delete confirmation form.</span></span> <span data-ttu-id="2afc4-399">두 번째 delete () 동작 실제 삭제를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-399">The second Delete() action performs the actual delete.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="2afc4-400">이상 버전에서는 반복 #7에서는 Contact Manager 되도록 수정 Ajax 삭제 한 단계를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-400">Later, in Iteration #7, we modify the Contact Manager so that it supports a one step Ajax delete.</span></span>


<span data-ttu-id="2afc4-401">두 개의 새 delete () 메서드 목록 8에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-401">The two new Delete() methods are contained in Listing 8.</span></span>

<span data-ttu-id="2afc4-402">**8-Controllers\HomeController.cs (삭제 메서드)를 나열합니다.**</span><span class="sxs-lookup"><span data-stu-id="2afc4-402">**Listing 8 - Controllers\HomeController.cs (Delete methods)**</span></span>

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample8.cs)]

<span data-ttu-id="2afc4-403">데이터베이스에서 연락처 레코드를 삭제 하기 위한 확인 형태를 반환 하는 첫 번째 delete () 메서드 (Figure20 참조).</span><span class="sxs-lookup"><span data-stu-id="2afc4-403">The first Delete() method returns a confirmation form for deleting a contact record from the database (see Figure20).</span></span> <span data-ttu-id="2afc4-404">두 번째 delete () 메서드는 데이터베이스에 대해 실제 삭제 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-404">The second Delete() method performs the actual delete operation against the database.</span></span> <span data-ttu-id="2afc4-405">데이터베이스에서 검색 되 면 원래 연락처 후 데이터베이스 삭제 작업을 수행 Entity Framework DeleteObject() 및 savechanges () 메서드 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-405">After the original contact has been retrieved from the database, the Entity Framework DeleteObject() and SaveChanges() methods are called to perform the database delete.</span></span>


<span data-ttu-id="2afc4-406">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image20.jpg)](iteration-1-create-the-application-cs/_static/image39.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-406">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image20.jpg)](iteration-1-create-the-application-cs/_static/image39.png)</span></span>

<span data-ttu-id="2afc4-407">**그림 20**: 삭제 확인 뷰 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image40.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-407">**Figure 20**: The delete confirmation view ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image40.png))</span></span>


<span data-ttu-id="2afc4-408">(그림 21 참조) 연락처 레코드를 삭제 하기 위한 링크를 포함 하도록 인덱스 뷰를 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-408">We need to modify the Index view so that it contains a link for deleting contact records (see Figure 21).</span></span> <span data-ttu-id="2afc4-409">편집 링크를 포함 하는 동일한 테이블 셀에 다음 코드를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-409">You need to add the following code to the same table cell that contains the Edit link:</span></span>

<span data-ttu-id="2afc4-410">Html.ActionLink ({id = 항목입니다. Id가}) %&gt;</span><span class="sxs-lookup"><span data-stu-id="2afc4-410">Html.ActionLink( { id=item.Id }) %&gt;</span></span>


<span data-ttu-id="2afc4-411">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image21.jpg)](iteration-1-create-the-application-cs/_static/image41.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-411">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image21.jpg)](iteration-1-create-the-application-cs/_static/image41.png)</span></span>

<span data-ttu-id="2afc4-412">**그림 21**: 편집 링크가 있는 뷰 인덱스 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image42.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-412">**Figure 21**: Index view with Edit link ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image42.png))</span></span>


<span data-ttu-id="2afc4-413">다음으로, 삭제 확인 뷰를 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-413">Next, we need to create the delete confirmation view.</span></span> <span data-ttu-id="2afc4-414">홈 컨트롤러 클래스에서 delete () 메서드를 마우스 오른쪽 단추로 클릭 하 고 추가 보기 메뉴 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-414">Right-click the Delete() method in the Home controller class and select the menu option Add View.</span></span> <span data-ttu-id="2afc4-415">뷰 추가 대화 상자가 나타나면 (그림 22 참조).</span><span class="sxs-lookup"><span data-stu-id="2afc4-415">The Add View dialog appears (see Figure 22).</span></span>

<span data-ttu-id="2afc4-416">와 달리 목록, 만들기 및 편집 보기의 경우 뷰 추가 대화 상자에 삭제 뷰를 만드는 옵션을</span><span class="sxs-lookup"><span data-stu-id="2afc4-416">Unlike in the case of the List, Create, and Edit views, the Add View dialog does not contain an option to create a Delete view.</span></span> <span data-ttu-id="2afc4-417">대신, 선택는 **ContactManager.Models.Contact** 데이터 클래스 및 **빈** 콘텐츠를 볼 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-417">Instead, select the **ContactManager.Models.Contact** data class and the **Empty** view content.</span></span> <span data-ttu-id="2afc4-418">에서는 콘텐츠 옵션 보기를 직접 만들 수 빈 뷰를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-418">Selecting the Empty view content option will require us to create the view ourselves.</span></span>


<span data-ttu-id="2afc4-419">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image22.jpg)](iteration-1-create-the-application-cs/_static/image43.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-419">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image22.jpg)](iteration-1-create-the-application-cs/_static/image43.png)</span></span>

<span data-ttu-id="2afc4-420">**그림 22**: 삭제 확인 뷰 추가 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image44.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-420">**Figure 22**: Adding the delete confirmation view ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image44.png))</span></span>


<span data-ttu-id="2afc4-421">Delete 보기의 내용은 목록 9에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-421">The content of the Delete view is contained in Listing 9.</span></span> <span data-ttu-id="2afc4-422">이 뷰를 확인 하는 양식을 포함 여부는 특정 연락처 해야 삭제할 (그림 21 참조).</span><span class="sxs-lookup"><span data-stu-id="2afc4-422">This view contains a form that confirms whether or not a particular contact should be deleted (see Figure 21).</span></span>

<span data-ttu-id="2afc4-423">**9-Views\Home\Delete.aspx 나열**</span><span class="sxs-lookup"><span data-stu-id="2afc4-423">**Listing 9 - Views\Home\Delete.aspx**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a><span data-ttu-id="2afc4-424">기본 컨트롤러의 이름 변경</span><span class="sxs-lookup"><span data-stu-id="2afc4-424">Changing the Name of the Default Controller</span></span>

<span data-ttu-id="2afc4-425">그 연락처를 사용 하기 위한 컨트롤러 클래스의 이름은 HomeController 클래스 이름이 이라고 문제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-425">It might bother you that the name of our controller class for working with contacts is named the HomeController class.</span></span> <span data-ttu-id="2afc4-426">이내에 사용 해야 t 컨트롤러 ContactController 이름은?</span><span class="sxs-lookup"><span data-stu-id="2afc4-426">Shouldn t the controller be named ContactController?</span></span>

<span data-ttu-id="2afc4-427">이 문제는 쉽게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-427">This issue is easy enough to fix.</span></span> <span data-ttu-id="2afc4-428">먼저, Home 컨트롤러의 이름을 리팩터링 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-428">First, we need to refactor the name of the Home controller.</span></span> <span data-ttu-id="2afc4-429">HomeController 클래스에 Visual Studio 코드 편집기에서 열고 클래스의 이름을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **이름 바꾸기 리팩터링**합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-429">Open the HomeController class in the Visual Studio Code Editor, right click the name of the class and select the menu option **Refactor, Rename**.</span></span> <span data-ttu-id="2afc4-430">이 메뉴 옵션을 선택 하면 이름 바꾸기 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-430">Selecting this menu option opens the Rename dialog.</span></span>


<span data-ttu-id="2afc4-431">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image23.jpg)](iteration-1-create-the-application-cs/_static/image45.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-431">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image23.jpg)](iteration-1-create-the-application-cs/_static/image45.png)</span></span>

<span data-ttu-id="2afc4-432">**그림 23**: 컨트롤러 이름 리팩터링 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image46.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-432">**Figure 23**: Refactoring a controller name ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image46.png))</span></span>


<span data-ttu-id="2afc4-433">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image24.jpg)](iteration-1-create-the-application-cs/_static/image47.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-433">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image24.jpg)](iteration-1-create-the-application-cs/_static/image47.png)</span></span>

<span data-ttu-id="2afc4-434">**그림 24**: 이름 바꾸기 대화 상자를 사용 하 여 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image48.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-434">**Figure 24**: Using the Rename dialog ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image48.png))</span></span>


<span data-ttu-id="2afc4-435">컨트롤러 클래스의 이름을 바꾸면 하는 경우 Visual Studio도 뷰 폴더에 폴더 이름을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-435">If you rename your controller class, Visual Studio will update the name of the folder in the Views folder as well.</span></span> <span data-ttu-id="2afc4-436">Visual Studio \Views\Contact 폴더로 \Views\Home 폴더를 이름은지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-436">Visual Studio will rename the \Views\Home folder to the \Views\Contact folder.</span></span>

<span data-ttu-id="2afc4-437">이 변경을 수행한 후 응용 프로그램은 더 이상 Home 컨트롤러를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-437">After you make this change, your application will no longer have a Home controller.</span></span> <span data-ttu-id="2afc4-438">응용 프로그램을 실행 하는 경우에 그림 25에서 오류 페이지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-438">When you run your application, you'll get the error page in Figure 25.</span></span>


<span data-ttu-id="2afc4-439">[![새 프로젝트 대화 상자](iteration-1-create-the-application-cs/_static/image25.jpg)](iteration-1-create-the-application-cs/_static/image49.png)</span><span class="sxs-lookup"><span data-stu-id="2afc4-439">[![The New Project dialog box](iteration-1-create-the-application-cs/_static/image25.jpg)](iteration-1-create-the-application-cs/_static/image49.png)</span></span>

<span data-ttu-id="2afc4-440">**그림 25**: 기본 컨트롤러 없음 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image50.png))</span><span class="sxs-lookup"><span data-stu-id="2afc4-440">**Figure 25**: No default controller ([Click to view full-size image](iteration-1-create-the-application-cs/_static/image50.png))</span></span>


<span data-ttu-id="2afc4-441">홈 컨트롤러 대신 연락처 컨트롤러를 사용 하도록 Global.asax 파일에 기본 경로 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-441">We need to update the default route in the Global.asax file to use the Contact controller instead of the Home controller.</span></span> <span data-ttu-id="2afc4-442">Global.asax 파일을 열고 기본 경로 (참조 목록 10)에 의해 사용 되는 기본 컨트롤러를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-442">Open the Global.asax file and modify the default controller used by the default route (see Listing 10).</span></span>

<span data-ttu-id="2afc4-443">**10-Global.asax.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="2afc4-443">**Listing 10 - Global.asax.cs**</span></span>

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample10.cs)]

<span data-ttu-id="2afc4-444">이러한 변경을 수행한 후 Contact Manager 제대로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-444">After you make these changes, the Contact Manager will run correctly.</span></span> <span data-ttu-id="2afc4-445">이제, 연락처 컨트롤러 클래스 기본 컨트롤러도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-445">Now, it will use the Contact controller class as the default controller.</span></span>

## <a name="summary"></a><span data-ttu-id="2afc4-446">요약</span><span class="sxs-lookup"><span data-stu-id="2afc4-446">Summary</span></span>

<span data-ttu-id="2afc4-447">이 첫 번째 반복에서 기본적인 않아 응용 프로그램에서에서 만든는 가장 빠른 방법은 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-447">In this first iteration, we created a basic Contact Manager application in the fastest way possible.</span></span> <span data-ttu-id="2afc4-448">이 컨트롤러 및 뷰에 대 한 초기 코드를 자동으로 생성 하도록 Visual Studio의 순서로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-448">We took advantage of Visual Studio to generate the initial code for our controllers and views automatically.</span></span> <span data-ttu-id="2afc4-449">데이터베이스 모델 클래스를 자동으로 생성 하려면 Entity Framework의 순서로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-449">We also took advantage of the Entity Framework to generate our database model classes automatically.</span></span>

<span data-ttu-id="2afc4-450">현재 나열 하 고 만들기 하 고 편집 수 있으며 관리자에 게 문의 응용 프로그램에 대 한 연락처 레코드를 삭제 수 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-450">Currently, we can list, create, edit, and delete contact records with the Contact Manager application.</span></span> <span data-ttu-id="2afc4-451">즉, 모든 데이터베이스 기반 웹 응용 프로그램에 필요한 기본 데이터베이스 작업은 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-451">In other words, we can perform all of the basic database operations required by a database-driven web application.</span></span>

<span data-ttu-id="2afc4-452">그러나 응용 프로그램에 몇 가지 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-452">Unfortunately, our application has some problems.</span></span> <span data-ttu-id="2afc4-453">이를 원하는 대로 첫 번째와 I, 않아 응용 프로그램 가장 매력적인 응용 프로그램이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-453">First and I hesitate to admit this, the Contact Manager application is not the most attractive application.</span></span> <span data-ttu-id="2afc4-454">몇 가지 디자인 작업을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-454">It needs some design work.</span></span> <span data-ttu-id="2afc4-455">다음 반복에는 기본 뷰 마스터 페이지 및 응용 프로그램의 모양을 향상 시킬 연계 스타일 시트 변경할 수 있습니다 어떻게 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-455">In the next iteration, we'll look at how we can change the default view master page and cascading style sheet to improve the appearance of the application.</span></span>

<span data-ttu-id="2afc4-456">둘째, 폼 유효성 검사를 구현 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-456">Second, we have not implemented any form validation.</span></span> <span data-ttu-id="2afc4-457">예를 들어 없는 연락처 양식 만들기 폼 필드에 대해 값을 입력 하지 않고 제출 하는 것을 방지 하기 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-457">For example, there is nothing to prevent you from submitting the Create contact form without entering values for any of the form fields.</span></span> <span data-ttu-id="2afc4-458">또한 잘못 된 전화 번호 및 전자 메일 주소를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-458">Furthermore, you can enter invalid phone numbers and email addresses.</span></span> <span data-ttu-id="2afc4-459">반복 # 3에서에서 폼 유효성 검사 문제를 해결 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-459">We start to tackle the problem of form validation in iteration #3.</span></span>

<span data-ttu-id="2afc4-460">마지막으로, 가장 중요 한 점은 않아 응용 프로그램의 현재 반복 하거나 수 없습니다 쉽게 수정 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-460">Finally, and most importantly, the current iteration of the Contact Manager application cannot be easily modified or maintained.</span></span> <span data-ttu-id="2afc4-461">예를 들어 데이터베이스 액세스 논리 컨트롤러 작업에 오른쪽을 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-461">For example, the database access logic is baked right into the controller actions.</span></span> <span data-ttu-id="2afc4-462">이이 컨트롤러를 수정 하지 않고 데이터 액세스 코드를 수정할 수 없습니다 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-462">This means that we cannot modify our data access code without modifying our controllers.</span></span> <span data-ttu-id="2afc4-463">이후 반복에서 연락처 관리자를 변경 하려면 복원 성도 뛰어납니다 확인 하기 위해 구현할 수 있습니다 하는 소프트웨어 디자인 패턴을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="2afc4-463">In later iterations, we explore software design patterns that we can implement to make the Contact Manager more resilient to change.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="2afc4-464">다음</span><span class="sxs-lookup"><span data-stu-id="2afc4-464">Next</span></span>](iteration-2-make-the-application-look-nice-cs.md)
