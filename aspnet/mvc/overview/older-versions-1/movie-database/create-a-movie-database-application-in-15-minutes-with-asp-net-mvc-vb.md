---
uid: mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb
title: ASP.NET MVC (VB)를 사용 하 여 15 분만에 영화 데이터베이스 응용 프로그램 만들기 | Microsoft Docs
author: StephenWalther
description: Stephen walther가 전체 데이터베이스 기반의 ASP.NET MVC 응용 프로그램 시작부터 완료를 빌드합니다. 이 자습서는 새로운는 사람들에 대 한 훌륭한 소개 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: e4ba9786-734c-4eb3-91bb-089793325d0d
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb
msc.type: authoredcontent
ms.openlocfilehash: a64d140eba4ebf489486af1a0be6269a8b904c13
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37372597"
---
<a name="create-a-movie-database-application-in-15-minutes-with-aspnet-mvc-vb"></a><span data-ttu-id="90c0c-104">ASP.NET MVC (VB)를 사용 하 여 15 분만에 영화 데이터베이스 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="90c0c-104">Create a Movie Database Application in 15 Minutes with ASP.NET MVC (VB)</span></span>
====================
<span data-ttu-id="90c0c-105">[Stephen walther가](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="90c0c-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="90c0c-106">코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="90c0c-106">Download Code</span></span>](http://download.microsoft.com/download/7/2/8/728F8794-E59A-4D18-9A56-7AD2DB05BD9D/MovieApp_VB.zip)

> <span data-ttu-id="90c0c-107">Stephen walther가 전체 데이터베이스 기반의 ASP.NET MVC 응용 프로그램 시작부터 완료를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-107">Stephen Walther builds an entire database-driven ASP.NET MVC application from start to finish.</span></span> <span data-ttu-id="90c0c-108">이 자습서는 ASP.NET MVC Framework를 처음 접하는 및 ASP.NET MVC 응용 프로그램을 구축 하는 과정 이해 하려는 사용자에 대 한 훌륭한 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-108">This tutorial is a great introduction for people who are new to the ASP.NET MVC Framework and who want to get a sense of the process of building an ASP.NET MVC application.</span></span>


<span data-ttu-id="90c0c-109">이 자습서의 목적은 "는 것은 어떤지에"의 의미를 제공 하는 ASP.NET MVC 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-109">The purpose of this tutorial is to give you a sense of "what it is like" to build an ASP.NET MVC application.</span></span> <span data-ttu-id="90c0c-110">이 자습서에서는 있습니까 무기를 발사 하는 전체 ASP.NET MVC 응용 프로그램 시작부터 완료를 구축 하는 과정입니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-110">In this tutorial, I blast through building an entire ASP.NET MVC application from start to finish.</span></span> <span data-ttu-id="90c0c-111">간단한 데이터베이스 중심 응용 프로그램을 작성 하는 방법을 나열, 만들기, 데이터베이스 레코드를 편집을 보여 주는 방법을 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-111">I show you how to build a simple database-driven application that illustrates how you can list, create, and edit database records.</span></span>

<span data-ttu-id="90c0c-112">응용 프로그램을 빌드하는 프로세스를 간소화 하기 위해 Visual Studio 2008의 스 캐 폴딩 기능에 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-112">To simplify the process of building our application, we'll take advantage of the scaffolding features of Visual Studio 2008.</span></span> <span data-ttu-id="90c0c-113">초기 코드 및 콘텐츠는 컨트롤러, 모델 및 뷰를 생성 하는 Visual Studio 알림이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-113">We'll let Visual Studio generate the initial code and content for our controllers, models, and views.</span></span>

<span data-ttu-id="90c0c-114">Active Server Pages와 ASP.NET 보았다면 다음 찾아야 ASP.NET MVC 매우 친숙 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-114">If you have worked with Active Server Pages or ASP.NET, then you should find ASP.NET MVC very familiar.</span></span> <span data-ttu-id="90c0c-115">ASP.NET MVC 뷰는 Active Server Pages 응용 프로그램의 페이지과 매우 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-115">ASP.NET MVC views are very much like the pages in an Active Server Pages application.</span></span> <span data-ttu-id="90c0c-116">및 기존의 ASP.NET Web Forms 응용 프로그램과 마찬가지로 ASP.NET MVC 사용 하면 다양 한 언어 및.NET framework에서 제공 하는 클래스에 대 한 전체 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-116">And, just like a traditional ASP.NET Web Forms application, ASP.NET MVC provides you with full access to the rich set of languages and classes provided by the .NET framework.</span></span>

<span data-ttu-id="90c0c-117">독자는이 자습서를 파악할 수 있도록 하는 방법을 ASP.NET MVC 응용 프로그램을 구축 하는 환경은 모두 유사한 것과 다르며 Active Server Pages 또는 ASP.NET Web Forms 응용 프로그램을 구축 하는 환경을의입니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-117">My hope is that this tutorial will give you a sense of how the experience of building an ASP.NET MVC application is both similar and different than the experience of building an Active Server Pages or ASP.NET Web Forms application.</span></span>

## <a name="overview-of-the-movie-database-application"></a><span data-ttu-id="90c0c-118">영화 데이터베이스 응용 프로그램 개요</span><span class="sxs-lookup"><span data-stu-id="90c0c-118">Overview of the Movie Database Application</span></span>

<span data-ttu-id="90c0c-119">간단 하 게 목표 이기 때문에 매우 간단한 영화 데이터베이스 응용 프로그램을 빌드할 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-119">Because our goal is to keep things simple, we'll build a very simple Movie Database application.</span></span> <span data-ttu-id="90c0c-120">간단한 영화 데이터베이스 응용 프로그램 수 있도록 세 가지를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-120">Our simple Movie Database application will allow us to do three things:</span></span>

1. <span data-ttu-id="90c0c-121">영화 데이터베이스 레코드 집합 나열</span><span class="sxs-lookup"><span data-stu-id="90c0c-121">List a set of movie database records</span></span>
2. <span data-ttu-id="90c0c-122">새 영화 데이터베이스 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="90c0c-122">Create a new movie database record</span></span>
3. <span data-ttu-id="90c0c-123">기존 영화 데이터베이스 레코드를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-123">Edit an existing movie database record</span></span>

<span data-ttu-id="90c0c-124">마찬가지로 간단 하 게 유지 하려는 것 이므로 알아보겠습니다 최소 수가 응용 프로그램을 빌드하는 데 필요한 ASP.NET MVC 프레임 워크의 기능 활용.</span><span class="sxs-lookup"><span data-stu-id="90c0c-124">Again, because we want to keep things simple, we'll take advantage of the minimum number of features of the ASP.NET MVC framework needed to build our application.</span></span> <span data-ttu-id="90c0c-125">예를 들어에서는 없습니다 활용 Test-Driven Development 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-125">For example, we won't be taking advantage of Test-Driven Development.</span></span>

<span data-ttu-id="90c0c-126">응용 프로그램을 만들기 위해 각 단계를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-126">In order to create our application, we need to complete each of the following steps:</span></span>

1. <span data-ttu-id="90c0c-127">ASP.NET MVC 웹 응용 프로그램 프로젝트를 만들려면</span><span class="sxs-lookup"><span data-stu-id="90c0c-127">Create the ASP.NET MVC Web Application Project</span></span>
2. <span data-ttu-id="90c0c-128">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="90c0c-128">Create the database</span></span>
3. <span data-ttu-id="90c0c-129">데이터베이스 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="90c0c-129">Create the database model</span></span>
4. <span data-ttu-id="90c0c-130">ASP.NET MVC 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="90c0c-130">Create the ASP.NET MVC controller</span></span>
5. <span data-ttu-id="90c0c-131">ASP.NET MVC 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="90c0c-131">Create the ASP.NET MVC views</span></span>

## <a name="preliminaries"></a><span data-ttu-id="90c0c-132">준비 단계</span><span class="sxs-lookup"><span data-stu-id="90c0c-132">Preliminaries</span></span>

<span data-ttu-id="90c0c-133">Visual Studio 2008 또는 Visual Web Developer 2008 Express는 ASP.NET MVC 응용 프로그램 빌드에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-133">You'll need either Visual Studio 2008 or Visual Web Developer 2008 Express to build an ASP.NET MVC application.</span></span> <span data-ttu-id="90c0c-134">ASP.NET MVC 프레임 워크를 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-134">You also need to download the ASP.NET MVC framework.</span></span>

<span data-ttu-id="90c0c-135">Visual Studio 2008을 소유 하지 않은, Visual Studio 2008 90 일 평가판이 웹이 사이트에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-135">If you don't own Visual Studio 2008, then you can download a 90 day trial version of Visual Studio 2008 from this website:</span></span>

[https://msdn.microsoft.com/vs2008/products/cc268305.aspx](https://msdn.microsoft.com/vs2008/products/cc268305.aspx)

<span data-ttu-id="90c0c-136">또는 만들면 ASP.NET MVC 응용 프로그램 Visual Web Developer Express 2008을 사용 하 여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-136">Alternatively, you can create ASP.NET MVC applications with Visual Web Developer Express 2008.</span></span> <span data-ttu-id="90c0c-137">Visual Web Developer Express를 사용 하려는 경우 다음 해야 서비스 팩 1을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-137">If you decide to use Visual Web Developer Express then you must have Service Pack 1 installed.</span></span> <span data-ttu-id="90c0c-138">Visual Web Developer 2008 Express 서비스 팩 1을 사용 하 여이 웹 사이트에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-138">You can download Visual Web Developer 2008 Express with Service Pack 1 from this website:</span></span>

[<span data-ttu-id="90c0c-139">https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&ampdisplaylang = en</span><span class="sxs-lookup"><span data-stu-id="90c0c-139">https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en</span></span>](https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en)

<span data-ttu-id="90c0c-140">Visual Studio 2008 또는 Visual Web Developer 2008을 설치한 후 ASP.NET MVC 프레임 워크를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-140">After you install either Visual Studio 2008 or Visual Web Developer 2008, you need to install the ASP.NET MVC framework.</span></span> <span data-ttu-id="90c0c-141">다음 웹 사이트에서 ASP.NET MVC 프레임 워크를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-141">You can download the ASP.NET MVC framework from the following website:</span></span>

[https://www.asp.net/mvc/](../../../index.md)

> [!NOTE] 
> 
> <span data-ttu-id="90c0c-142">ASP.NET 프레임 워크 및 ASP.NET MVC 프레임 워크를 개별적으로 다운로드 하는 대신 웹 플랫폼 설치 관리자를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-142">Instead of downloading the ASP.NET framework and the ASP.NET MVC framework individually, you can take advantage of the Web Platform Installer.</span></span> <span data-ttu-id="90c0c-143">웹 플랫폼 설치 관리자는 설치 된 응용 프로그램을 쉽게 관리할 수 있도록 하는 응용 프로그램 컴퓨터:</span><span class="sxs-lookup"><span data-stu-id="90c0c-143">The Web Platform Installer is an application that enables you to easily manage the installed applications are your computer:</span></span>
> 
> [https://www.microsoft.com/web/gallery/Install.aspx](https://www.microsoft.com/web/gallery/Install.aspx)


## <a name="creating-an-aspnet-mvc-web-application-project"></a><span data-ttu-id="90c0c-144">ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="90c0c-144">Creating an ASP.NET MVC Web Application Project</span></span>

<span data-ttu-id="90c0c-145">Visual Studio 2008에서 새 ASP.NET MVC 웹 응용 프로그램 프로젝트를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-145">Let's start by creating a new ASP.NET MVC Web Application project in Visual Studio 2008.</span></span> <span data-ttu-id="90c0c-146">메뉴 옵션을 선택 **파일, 새 프로젝트** 그림 1의 새 프로젝트 대화 상자를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-146">Select the menu option **File, New Project** and you will see the New Project dialog box in Figure 1.</span></span> <span data-ttu-id="90c0c-147">프로그래밍 언어와 Visual Basic을 선택 하 고 ASP.NET MVC 웹 응용 프로그램 프로젝트 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-147">Select Visual Basic as the programming language and select the ASP.NET MVC Web Application project template.</span></span> <span data-ttu-id="90c0c-148">프로젝트 이름을 MovieApp 제공 하 고 확인 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-148">Give your project the name MovieApp and click the OK button.</span></span>


<span data-ttu-id="90c0c-149">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="90c0c-149">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.png)</span></span>

<span data-ttu-id="90c0c-150">**그림 01**: 새 프로젝트 대화 상자 ([큰 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="90c0c-150">**Figure 01**: The New Project dialog box ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.png))</span></span>


<span data-ttu-id="90c0c-151">새 프로젝트 대화 상자의 맨 위에 있는 드롭다운 목록에서.NET Framework 3.5를 선택 하거나 ASP.NET MVC 웹 응용 프로그램 프로젝트 템플릿이 나타나지 않았는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-151">Make sure that you select .NET Framework 3.5 from the dropdown list at the top of the New Project dialog or the ASP.NET MVC Web Application project template won't appear.</span></span>


<span data-ttu-id="90c0c-152">새 MVC 웹 응용 프로그램 프로젝트를 만들 때마다 Visual Studio는 별도 단위 테스트 프로젝트를 만들 것인지 묻는 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-152">Whenever you create a new MVC Web Application project, Visual Studio prompts you to create a separate unit test project.</span></span> <span data-ttu-id="90c0c-153">그림 2에서 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-153">The dialog in Figure 2 appears.</span></span> <span data-ttu-id="90c0c-154">서 우리가 않습니다 만들 테스트가이 자습서에서는 시간 제약 조건으로 인해 (, 예에서는 해야 죄 잠시이 대 한) 선택 합니다 **No** 옵션을 클릭 합니다 **확인** 단추.</span><span class="sxs-lookup"><span data-stu-id="90c0c-154">Because we won't be creating tests in this tutorial because of time constraints (and, yes, we should feel a little guilty about this) select the **No** option and click the **OK** button.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="90c0c-155">Visual Web Developer는 테스트 프로젝트를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-155">Visual Web Developer does not support test projects.</span></span>


<span data-ttu-id="90c0c-156">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="90c0c-156">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.png)</span></span>

<span data-ttu-id="90c0c-157">**그림 02**:의 단위 테스트 프로젝트 만들기 대화 상자 ([큰 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="90c0c-157">**Figure 02**: The Create Unit Test Project dialog ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.png))</span></span>


<span data-ttu-id="90c0c-158">ASP.NET MVC 응용 프로그램 폴더의 표준 집합이: 모델, 뷰 및 컨트롤러 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-158">An ASP.NET MVC application has a standard set of folders: a Models, Views, and Controllers folder.</span></span> <span data-ttu-id="90c0c-159">솔루션 탐색기 창에서 폴더의이 표준 집합을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-159">You can see this standard set of folders in the Solution Explorer window.</span></span> <span data-ttu-id="90c0c-160">영화 데이터베이스 응용 프로그램을 구축 하기 위해 각 모델, 뷰 및 컨트롤러 폴더에 파일을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-160">We'll need to add files to each of the Models, Views, and Controllers folders in order to build our Movie Database application.</span></span>

<span data-ttu-id="90c0c-161">Visual Studio를 사용 하 여 새 MVC 응용 프로그램을 만든 경우 샘플 응용 프로그램을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-161">When you create a new MVC application with Visual Studio, you get a sample application.</span></span> <span data-ttu-id="90c0c-162">처음부터 새로 시작 하려는 것 이므로이 샘플 응용 프로그램에 대 한 콘텐츠를 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-162">Because we want to start from scratch, we need to delete the content for this sample application.</span></span> <span data-ttu-id="90c0c-163">다음 파일 및 폴더를 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-163">You need to delete the following file and the following folder:</span></span>

- <span data-ttu-id="90c0c-164">Controllers\HomeController.vb</span><span class="sxs-lookup"><span data-stu-id="90c0c-164">Controllers\HomeController.vb</span></span>
- <span data-ttu-id="90c0c-165">Views\Home</span><span class="sxs-lookup"><span data-stu-id="90c0c-165">Views\Home</span></span>

## <a name="creating-the-database"></a><span data-ttu-id="90c0c-166">데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="90c0c-166">Creating the Database</span></span>

<span data-ttu-id="90c0c-167">이 영화 데이터베이스 레코드를 보관할 데이터베이스를 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-167">We need to create a database to hold our movie database records.</span></span> <span data-ttu-id="90c0c-168">다행히 Visual Studio는 SQL Server Express 라는 무료 데이터베이스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-168">Luckily, Visual Studio includes a free database named SQL Server Express.</span></span> <span data-ttu-id="90c0c-169">데이터베이스를 만들려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-169">Follow these steps to create the database:</span></span>

1. <span data-ttu-id="90c0c-170">앱을 마우스 오른쪽 단추로 클릭\_메뉴 옵션을 선택 하는 솔루션 탐색기 창에서 데이터 폴더 **추가, 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-170">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="90c0c-171">선택 된 **데이터** 범주를 선택 합니다 **SQL Server 데이터베이스** 템플릿 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="90c0c-171">Select the **Data** category and select the **SQL Server Database** template (see Figure 3).</span></span>
3. <span data-ttu-id="90c0c-172">새 데이터베이스의 이름을 *MoviesDB.mdf* 을 클릭 합니다 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-172">Name your new database *MoviesDB.mdf* and click the **Add** button.</span></span>

<span data-ttu-id="90c0c-173">앱에 있는 MoviesDB.mdf 파일을 두 번 클릭 하 여 데이터베이스에 연결할 수 데이터베이스를 만든 후\_데이터 폴더.</span><span class="sxs-lookup"><span data-stu-id="90c0c-173">After you create your database, you can connect to the database by double-clicking the MoviesDB.mdf file located in the App\_Data folder.</span></span> <span data-ttu-id="90c0c-174">서버 탐색기 창을 엽니다 MoviesDB.mdf 파일을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-174">Double-clicking the MoviesDB.mdf file opens the Server Explorer window.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="90c0c-175">서버 탐색기 창에는 Visual Web Developer의 경우 데이터베이스 탐색기 창을 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-175">The Server Explorer window is named the Database Explorer window in the case of Visual Web Developer.</span></span>


<span data-ttu-id="90c0c-176">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="90c0c-176">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.png)</span></span>

<span data-ttu-id="90c0c-177">**그림 03**: Microsoft SQL Server 데이터베이스를 만드는 ([큰 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="90c0c-177">**Figure 03**: Creating a Microsoft SQL Server Database ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.png))</span></span>


<span data-ttu-id="90c0c-178">다음으로 새 데이터베이스 테이블을 만들고 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-178">Next, we need to create a new database table.</span></span> <span data-ttu-id="90c0c-179">서버 탐색기 창에서 테이블 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **새 테이블 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-179">From within the Sever Explorer window, right-click the Tables folder and select the menu option **Add New Table**.</span></span> <span data-ttu-id="90c0c-180">이 메뉴 옵션을 선택 하면 데이터베이스 테이블 디자이너를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-180">Selecting this menu option opens the database table designer.</span></span> <span data-ttu-id="90c0c-181">다음 데이터베이스 열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-181">Create the following database columns:</span></span>

<a id="0.2_table01"></a>


| <span data-ttu-id="90c0c-182">**열 이름**</span><span class="sxs-lookup"><span data-stu-id="90c0c-182">**Column Name**</span></span> | <span data-ttu-id="90c0c-183">**데이터 형식**</span><span class="sxs-lookup"><span data-stu-id="90c0c-183">**Data Type**</span></span> | <span data-ttu-id="90c0c-184">**Null 허용**</span><span class="sxs-lookup"><span data-stu-id="90c0c-184">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="90c0c-185">ID</span><span class="sxs-lookup"><span data-stu-id="90c0c-185">Id</span></span> | <span data-ttu-id="90c0c-186">Int</span><span class="sxs-lookup"><span data-stu-id="90c0c-186">Int</span></span> | <span data-ttu-id="90c0c-187">False</span><span class="sxs-lookup"><span data-stu-id="90c0c-187">False</span></span> |
| <span data-ttu-id="90c0c-188">제목</span><span class="sxs-lookup"><span data-stu-id="90c0c-188">Title</span></span> | <span data-ttu-id="90c0c-189">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="90c0c-189">Nvarchar(100)</span></span> | <span data-ttu-id="90c0c-190">False</span><span class="sxs-lookup"><span data-stu-id="90c0c-190">False</span></span> |
| <span data-ttu-id="90c0c-191">책임자</span><span class="sxs-lookup"><span data-stu-id="90c0c-191">Director</span></span> | <span data-ttu-id="90c0c-192">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="90c0c-192">Nvarchar(100)</span></span> | <span data-ttu-id="90c0c-193">False</span><span class="sxs-lookup"><span data-stu-id="90c0c-193">False</span></span> |
| <span data-ttu-id="90c0c-194">DateReleased</span><span class="sxs-lookup"><span data-stu-id="90c0c-194">DateReleased</span></span> | <span data-ttu-id="90c0c-195">DateTime</span><span class="sxs-lookup"><span data-stu-id="90c0c-195">DateTime</span></span> | <span data-ttu-id="90c0c-196">False</span><span class="sxs-lookup"><span data-stu-id="90c0c-196">False</span></span> |


<span data-ttu-id="90c0c-197">첫 번째 열, Id 열에 두 특수 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-197">The first column, the Id column, has two special properties.</span></span> <span data-ttu-id="90c0c-198">첫째, Id 열을 기본 키 열으로 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-198">First, you need to mark the Id column as the primary key column.</span></span> <span data-ttu-id="90c0c-199">Id 열을 선택한 후 클릭 합니다 **기본 키 설정** 단추 (예: 키 보이는 아이콘을 임).</span><span class="sxs-lookup"><span data-stu-id="90c0c-199">After selecting the Id column, click the **Set Primary Key** button (it is the icon that looks like a key).</span></span> <span data-ttu-id="90c0c-200">둘째, Id 열을 Id 열으로 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-200">Second, you need to mark the Id column as an Identity column.</span></span> <span data-ttu-id="90c0c-201">열 속성 창에서 Id 사양 섹션까지 아래로 스크롤하여 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-201">In the Column Properties window, scroll down to the Identity Specification section and expand it.</span></span> <span data-ttu-id="90c0c-202">변경 된 **Id** 속성을 값 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-202">Change the **Is Identity** property to the value **Yes**.</span></span> <span data-ttu-id="90c0c-203">작업을 완료 하는 경우 테이블은 그림 4와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-203">When you are finished, the table should look like Figure 4.</span></span>


<span data-ttu-id="90c0c-204">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="90c0c-204">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.png)</span></span>

<span data-ttu-id="90c0c-205">**그림 04**: The 영화 데이터베이스 테이블 ([큰 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="90c0c-205">**Figure 04**: The Movies database table ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.png))</span></span>


<span data-ttu-id="90c0c-206">새 테이블을 저장 하는 최종 단계가입니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-206">The final step is to save the new table.</span></span> <span data-ttu-id="90c0c-207">저장 단추 (플로피 아이콘)를 클릭 하 고 새 테이블 이름을 영화를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-207">Click the Save button (the icon of the floppy) and give the new table the name Movies.</span></span>

<span data-ttu-id="90c0c-208">테이블 만들기를 마친 후 테이블에 일부 영화 레코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-208">After you finish creating the table, add some movie records to the table.</span></span> <span data-ttu-id="90c0c-209">서버 탐색기 창에서 동영상 테이블을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **테이블 데이터 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-209">Right-click the Movies table in the Server Explorer window and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="90c0c-210">(그림 5 참조) 즐겨 찾는 영화 목록을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-210">Enter a list of your favorite movies (see Figure 5).</span></span>


<span data-ttu-id="90c0c-211">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="90c0c-211">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.png)</span></span>

<span data-ttu-id="90c0c-212">**그림 05**: 영화 레코드 입력 ([큰 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="90c0c-212">**Figure 05**: Entering movie records ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.png))</span></span>


## <a name="creating-the-model"></a><span data-ttu-id="90c0c-213">모델 만들기</span><span class="sxs-lookup"><span data-stu-id="90c0c-213">Creating the Model</span></span>

<span data-ttu-id="90c0c-214">다음 데이터베이스를 표현 하는 클래스 집합을 만드는 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-214">We next need to create a set of classes to represent our database.</span></span> <span data-ttu-id="90c0c-215">데이터베이스 모델을 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-215">We need to create a database model.</span></span> <span data-ttu-id="90c0c-216">데이터베이스 모델의 클래스를 자동으로 생성 하는 Microsoft Entity Framework의 이점은 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-216">We'll take advantage of the Microsoft Entity Framework to generate the classes for our database model automatically.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="90c0c-217">ASP.NET MVC 프레임 워크는 Microsoft Entity Framework는 관련이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-217">The ASP.NET MVC framework is not tied to the Microsoft Entity Framework.</span></span> <span data-ttu-id="90c0c-218">다양 한 개체 관계형 매핑을 사용 하 여 데이터베이스 모델 클래스를 만들 수 있습니다 (또는 / M) LINQ to SQL, Subsonic 및 NHibernate 포함 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-218">You can create your database model classes by taking advantage of a variety of Object Relational Mapping (OR/M) tools including LINQ to SQL, Subsonic, and NHibernate.</span></span>


<span data-ttu-id="90c0c-219">엔터티 데이터 모델 마법사를 시작 하려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-219">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="90c0c-220">메뉴 옵션을 선택 하 고 솔루션 탐색기 창에서 Models 폴더를 마우스 오른쪽 단추로 클릭 **추가, 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-220">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="90c0c-221">선택 된 **데이터** 범주를 선택 합니다 **ADO.NET 엔터티 데이터 모델** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="90c0c-221">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="90c0c-222">데이터 모델의 이름을 *MoviesDBModel.edmx* 을 클릭 합니다 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-222">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="90c0c-223">추가 단추를 클릭 하면 엔터티 데이터 모델 마법사 나타납니다 (그림 6 참조).</span><span class="sxs-lookup"><span data-stu-id="90c0c-223">After you click the Add button, the Entity Data Model Wizard appears (see Figure 6).</span></span> <span data-ttu-id="90c0c-224">마법사를 완료 하려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-224">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="90c0c-225">에 **Model 콘텐츠 선택** 단계를 선택 합니다 **데이터베이스에서 생성** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-225">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="90c0c-226">에 **데이터 연결 선택** 단계를 사용 하 여 합니다 *MoviesDB.mdf* 데이터 연결 및 이름 *MoviesDBEntities* 연결 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-226">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="90c0c-227">클릭 합니다 **다음** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-227">Click the **Next** button.</span></span>
3. <span data-ttu-id="90c0c-228">에 **데이터베이스 개체 선택** 단계, 테이블 노드를 확장 한 다음 동영상 테이블을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-228">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="90c0c-229">네임 스페이스를 입력 *MovieApp.Models* 을 클릭 합니다 **마침** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-229">Enter the namespace *MovieApp.Models* and click the **Finish** button.</span></span>


<span data-ttu-id="90c0c-230">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="90c0c-230">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.png)</span></span>

<span data-ttu-id="90c0c-231">**그림 06**: 엔터티 데이터 모델 마법사를 사용 하 여 데이터베이스 모델 생성 ([큰 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="90c0c-231">**Figure 06**: Generating a database model with the Entity Data Model Wizard ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.png))</span></span>


<span data-ttu-id="90c0c-232">엔터티 데이터 모델 마법사를 완료 한 후 엔터티 데이터 모델 디자이너가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-232">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="90c0c-233">디자이너에 영화 데이터베이스 테이블에 표시 됩니다 (그림 7 참조).</span><span class="sxs-lookup"><span data-stu-id="90c0c-233">The Designer should display the Movies database table (see Figure 7).</span></span>


<span data-ttu-id="90c0c-234">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="90c0c-234">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.png)</span></span>

<span data-ttu-id="90c0c-235">**그림 07**:은 엔터티 데이터 모델 디자이너 ([큰 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="90c0c-235">**Figure 07**: The Entity Data Model Designer ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.png))</span></span>


<span data-ttu-id="90c0c-236">계속 하기 전에 하나의 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-236">We need to make one change before we continue.</span></span> <span data-ttu-id="90c0c-237">엔터티 데이터 마법사 영화 데이터베이스 테이블을 나타내는 이라는 영화 모델 클래스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-237">The Entity Data Wizard generates a model class named Movies that represents the Movies database table.</span></span> <span data-ttu-id="90c0c-238">클래스의 이름을 수정 하려면 먼저 특정 영화를 나타내는 영화 클래스를 사용 해야, 하므로 *영화* of *영화* (단일 아니라 복수).</span><span class="sxs-lookup"><span data-stu-id="90c0c-238">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="90c0c-239">디자이너 화면의 클래스의 이름을 두 번 클릭 하 고 영화 Movies에서 클래스의 이름을 변경 하십시오.</span><span class="sxs-lookup"><span data-stu-id="90c0c-239">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="90c0c-240">이렇게 변경한 후 다음을 클릭 합니다 **저장** 단추 (플로피 디스크 아이콘) 동영상 클래스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-240">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="creating-the-aspnet-mvc-controller"></a><span data-ttu-id="90c0c-241">ASP.NET MVC 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="90c0c-241">Creating the ASP.NET MVC Controller</span></span>

<span data-ttu-id="90c0c-242">다음 단계는 ASP.NET MVC 컨트롤러를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-242">The next step is to create the ASP.NET MVC controller.</span></span> <span data-ttu-id="90c0c-243">컨트롤러는 ASP.NET MVC 응용 프로그램을 사용 하 여 사용자 상호 작용 하는 방법을 제어 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-243">A controller is responsible for controlling how a user interacts with an ASP.NET MVC application.</span></span>

<span data-ttu-id="90c0c-244">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-244">Follow these steps:</span></span>

1. <span data-ttu-id="90c0c-245">솔루션 탐색기 창에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **추가, 컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-245">In the Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller**.</span></span>
2. <span data-ttu-id="90c0c-246">컨트롤러 추가 대화 상자에서 이름을 입력 *HomeController* 레이블이 지정 된 확인란 **만들기, 업데이트 및 세부 정보 시나리오에 대 한 작업 메서드를 추가** (그림 8 참조).</span><span class="sxs-lookup"><span data-stu-id="90c0c-246">In the Add Controller dialog, enter the name *HomeController* and check the checkbox labeled **Add action methods for Create, Update, and Details scenarios** (see Figure 8).</span></span>
3. <span data-ttu-id="90c0c-247">클릭 합니다 **추가** 프로젝트에 새 컨트롤러를 추가 하려면 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-247">Click the **Add** button to add the new controller to your project.</span></span>

<span data-ttu-id="90c0c-248">다음이 단계를 완료 한 후 목록 1에서 컨트롤러 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-248">After you complete these steps, the controller in Listing 1 is created.</span></span> <span data-ttu-id="90c0c-249">인덱스 세부 정보를 만들기, 명명 된 메서드에 포함 되어 있는지 확인할 수 있습니다 하 고 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-249">Notice that it contains methods named Index, Details, Create, and Edit.</span></span> <span data-ttu-id="90c0c-250">다음 섹션에서는 이러한 메서드가 작동 하기를 가져오려고 하는 데 필요한 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-250">In the following sections, we'll add the necessary code to get these methods to work.</span></span>


<span data-ttu-id="90c0c-251">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="90c0c-251">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image15.png)</span></span>

<span data-ttu-id="90c0c-252">**그림 08**: 새 ASP.NET MVC 컨트롤러 추가 ([큰 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="90c0c-252">**Figure 08**: Adding a new ASP.NET MVC Controller ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image16.png))</span></span>


<span data-ttu-id="90c0c-253">**1 – Controllers\HomeController.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="90c0c-253">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample1.vb)]

## <a name="listing-database-records"></a><span data-ttu-id="90c0c-254">데이터베이스 레코드 목록</span><span class="sxs-lookup"><span data-stu-id="90c0c-254">Listing Database Records</span></span>

<span data-ttu-id="90c0c-255">Home 컨트롤러의 index () 메서드는 ASP.NET MVC 응용 프로그램에 대 한 기본 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-255">The Index() method of the Home controller is the default method for an ASP.NET MVC application.</span></span> <span data-ttu-id="90c0c-256">ASP.NET MVC 응용 프로그램을 실행 하는 경우 index () 메서드는 호출 되는 첫 번째 컨트롤러 메서드.</span><span class="sxs-lookup"><span data-stu-id="90c0c-256">When you run an ASP.NET MVC application, the Index() method is the first controller method that is called.</span></span>

<span data-ttu-id="90c0c-257">영화 데이터베이스 테이블에서 레코드 목록을 표시할 index () 메서드를 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-257">We'll use the Index() method to display the list of records from the Movies database table.</span></span> <span data-ttu-id="90c0c-258">알아보겠습니다 데이터베이스의 이점은 앞에서 만든 index () 메서드를 사용 하 여 영화 데이터베이스 레코드를 검색 하는 모델 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-258">We'll take advantage of the database model classes that we created earlier to retrieve the movie database records with the Index() method.</span></span>

<span data-ttu-id="90c0c-259">HomeController 클래스 목록 2에서 라는 새 private 필드 포함 되도록 수정 했지만 \_db입니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-259">I've modified the HomeController class in Listing 2 so that it contains a new private field named \_db.</span></span> <span data-ttu-id="90c0c-260">MoviesDBEntities 클래스가 나타내는 데이터베이스 모델 및이 클래스는 데이터베이스와 통신 하는 데 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-260">The MoviesDBEntities class represents our database model and we'll use this class to communicate with our database.</span></span>

<span data-ttu-id="90c0c-261">또한 목록 2에서 index () 메서드를 수정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-261">I've also modified the Index() method in Listing 2.</span></span> <span data-ttu-id="90c0c-262">Index () 메서드는 MoviesDBEntities 클래스를 사용 하 여 영화 데이터베이스 테이블에서 모든 영화 레코드를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-262">The Index() method uses the MoviesDBEntities class to retrieve all of the movie records from the Movies database table.</span></span> <span data-ttu-id="90c0c-263">식을  *\_db입니다. MovieSet.ToList()* 영화 데이터베이스 테이블에서 모든 영화 레코드 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-263">The expression *\_db.MovieSet.ToList()* returns a list of all of the movie records from the Movies database table.</span></span>

<span data-ttu-id="90c0c-264">동영상 목록 보기에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-264">The list of movies is passed to the view.</span></span> <span data-ttu-id="90c0c-265">뷰 데이터와 뷰에 전달 가져옵니다 View() 메서드에 전달 되는 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-265">Anything that gets passed to the View() method gets passed to the view as view data.</span></span>

<span data-ttu-id="90c0c-266">**2 – Controllers/HomeController.vb (수정 된 인덱스 메서드)를 나열 합니다.**</span><span class="sxs-lookup"><span data-stu-id="90c0c-266">**Listing 2 – Controllers/HomeController.vb (modified Index method)**</span></span>

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample2.vb)]

<span data-ttu-id="90c0c-267">Index () 메서드 Index 라는 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-267">The Index() method returns a view named Index.</span></span> <span data-ttu-id="90c0c-268">영화 데이터베이스 레코드의 목록을 표시 하려면이 보기를 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-268">We need to create this view to display the list of movie database records.</span></span> <span data-ttu-id="90c0c-269">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-269">Follow these steps:</span></span>


<span data-ttu-id="90c0c-270">프로젝트를 빌드하면 해야 (메뉴 옵션을 선택 **빌드, 솔루션 빌드**) 열기 전에 **뷰 추가** 대화 상자 또는 없는 클래스에 표시 됩니다는 **데이터 클래스 보기** 드롭다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-270">You should build your project (select the menu option **Build, Build Solution**) before opening the **Add View** dialog or no classes will appear in the **View data class** dropdown list.</span></span>


1. <span data-ttu-id="90c0c-271">코드 편집기에서 index () 메서드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **뷰 추가** (그림 9 참조).</span><span class="sxs-lookup"><span data-stu-id="90c0c-271">Right-click the Index() method in the code editor and select the menu option **Add View** (see Figure 9).</span></span>
2. <span data-ttu-id="90c0c-272">뷰 추가 대화 상자에서 레이블이 지정 된 확인란을 확인 하십시오 **강력한 형식의 뷰를 만들** 확인란이 선택 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-272">In the Add View dialog, verify that the checkbox labeled **Create a strongly-typed view** is checked.</span></span>
3. <span data-ttu-id="90c0c-273">**콘텐츠 보기** 드롭다운 목록에서 값을 선택 *목록*합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-273">From the **View content** dropdown list, select the value *List*.</span></span>
4. <span data-ttu-id="90c0c-274">**데이터 클래스를 보려면** 드롭다운 목록에서 값을 선택 *MovieApp.Movie*합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-274">From the **View data class** dropdown list, select the value *MovieApp.Movie*.</span></span>
5. <span data-ttu-id="90c0c-275">만들 새 추가 단추를 클릭 (그림 10 참조)를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-275">Click the Add button to create the new view (see Figure 10).</span></span>

<span data-ttu-id="90c0c-276">다음이 단계를 완료 하면 Index.aspx 라는 새 뷰 Views\Home 폴더에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-276">After you complete these steps, a new view named Index.aspx is added to the Views\Home folder.</span></span> <span data-ttu-id="90c0c-277">인덱스 뷰의 내용은 목록 3에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-277">The contents of the Index view are included in Listing 3.</span></span>


<span data-ttu-id="90c0c-278">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="90c0c-278">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image17.png)</span></span>

<span data-ttu-id="90c0c-279">**그림 09**: 뷰 컨트롤러 작업에서 추가 ([큰 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="90c0c-279">**Figure 09**: Adding a view from a controller action ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image18.png))</span></span>


<span data-ttu-id="90c0c-280">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="90c0c-280">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image19.png)</span></span>

<span data-ttu-id="90c0c-281">**그림 10**: 뷰 추가 대화 상자를 사용 하 여 새 보기 만들기 ([큰 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="90c0c-281">**Figure 10**: Creating a new view with the Add View dialog ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image20.png))</span></span>


[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample3.aspx)]

<span data-ttu-id="90c0c-282">인덱스 보기에는 모든 HTML 표 내의 영화 데이터베이스 테이블에서 영화 레코드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-282">The Index view displays all of the movie records from the Movies database table within an HTML table.</span></span> <span data-ttu-id="90c0c-283">뷰에 For ViewData.Model 속성으로 표현 하는 각 영화를 반복 하는 각 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-283">The view contains a For Each loop that iterates through each movie represented by the ViewData.Model property.</span></span> <span data-ttu-id="90c0c-284">그런 다음 F5 키를 눌러 응용 프로그램을 실행 하면 그림 11에서 웹 페이지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-284">If you run your application by hitting the F5 key, then you'll see the web page in Figure 11.</span></span>


<span data-ttu-id="90c0c-285">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="90c0c-285">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image21.png)</span></span>

<span data-ttu-id="90c0c-286">**그림 11**: The 인덱스 보기 ([큰 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image22.png))</span><span class="sxs-lookup"><span data-stu-id="90c0c-286">**Figure 11**: The Index view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image22.png))</span></span>


## <a name="creating-new-database-records"></a><span data-ttu-id="90c0c-287">새 데이터베이스 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="90c0c-287">Creating New Database Records</span></span>

<span data-ttu-id="90c0c-288">이전 섹션에서 만든 인덱스 보기에 새 데이터베이스 레코드를 만들기 위한 링크가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-288">The Index view that we created in the previous section includes a link for creating new database records.</span></span> <span data-ttu-id="90c0c-289">보겠습니다 논리를 구현 하 고 새 영화 데이터베이스 레코드를 만드는 데 필요한 보기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-289">Let's go ahead and implement the logic and create the view necessary for creating new movie database records.</span></span>

<span data-ttu-id="90c0c-290">Home 컨트롤러 create () 라는 두 개의 메서드도 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-290">The Home controller contains two methods named Create().</span></span> <span data-ttu-id="90c0c-291">첫 번째 create () 메서드 매개 변수가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-291">The first Create() method has no parameters.</span></span> <span data-ttu-id="90c0c-292">Create () 메서드의이 오버 로드는 새 영화 데이터베이스 레코드를 만들기 위한 HTML 폼을 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-292">This overload of the Create() method is used to display the HTML form for creating a new movie database record.</span></span>

<span data-ttu-id="90c0c-293">두 번째 create () 메서드가 FormCollection 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-293">The second Create() method has a FormCollection parameter.</span></span> <span data-ttu-id="90c0c-294">Create () 메서드의이 오버 로드는 서버에 새 영화를 만들기 위한 HTML 폼 게시 될 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-294">This overload of the Create() method is called when the HTML form for creating a new movie is posted to the server.</span></span> <span data-ttu-id="90c0c-295">이 두 번째 create () 메서드 메서드가 HTTP Post 작업을 수행 하지 않으면 호출 되는 것을 방지 하는 AcceptVerbs 특성에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-295">Notice that this second Create() method has an AcceptVerbs attribute that prevents the method from being called unless an HTTP Post operation is performed.</span></span>

<span data-ttu-id="90c0c-296">이 두 번째 create () 메서드 4의 업데이트 된 HomeController 클래스에서 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-296">This second Create() method has been modified in the updated HomeController class in Listing 4.</span></span> <span data-ttu-id="90c0c-297">새 버전의 create () 메서드 영화 매개 변수를 허용 하 고 영화 데이터베이스 테이블에 새 영화를 삽입 하기 위한 논리가 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-297">The new version of the Create() method accepts a Movie parameter and contains the logic for inserting a new movie into the Movies database table.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="90c0c-298">바인딩 특성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-298">Notice the Bind attribute.</span></span> <span data-ttu-id="90c0c-299">HTML 양식에서 영화 Id 속성을 업데이트 하려고 하지 때문에이 속성을 명시적으로 제외 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-299">Because we don't want to update the Movie Id property from HTML form, we need to explicitly exclude this property.</span></span>


<span data-ttu-id="90c0c-300">**4-Controllers\HomeController.vb (수정 된 Create 메서드)를 나열 합니다.**</span><span class="sxs-lookup"><span data-stu-id="90c0c-300">**Listing 4 – Controllers\HomeController.vb (modified Create method)**</span></span>

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample4.vb)]

<span data-ttu-id="90c0c-301">Visual Studio를 사용 하면 쉽게 새 동영상 데이터베이스를 만들기 위한 양식 만들 (그림 12 참조)를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-301">Visual Studio makes it easy to create the form for creating a new movie database record (see Figure 12).</span></span> <span data-ttu-id="90c0c-302">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-302">Follow these steps:</span></span>

1. <span data-ttu-id="90c0c-303">코드 편집기에서 create () 메서드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-303">Right-click the Create() method in the code editor and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="90c0c-304">레이블이 지정 된 확인란을 확인 하십시오 **강력한 형식의 뷰를 만들** 확인란이 선택 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-304">Verify that the checkbox labeled **Create a strongly-typed view** is checked.</span></span>
3. <span data-ttu-id="90c0c-305">**콘텐츠 보기** 드롭다운 목록에서 값을 선택 *만들기*합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-305">From the **View content** dropdown list, select the value *Create*.</span></span>
4. <span data-ttu-id="90c0c-306">**데이터 클래스를 보려면** 드롭다운 목록에서 값을 선택 *MovieApp.Movie*합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-306">From the **View data class** dropdown list, select the value *MovieApp.Movie*.</span></span>
5. <span data-ttu-id="90c0c-307">클릭 합니다 **추가** 새 뷰를 만들려면 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-307">Click the **Add** button to create the new view.</span></span>


<span data-ttu-id="90c0c-308">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="90c0c-308">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image23.png)</span></span>

<span data-ttu-id="90c0c-309">**그림 12**: 만들기 뷰 추가 ([큰 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="90c0c-309">**Figure 12**: Adding the Create view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image24.png))</span></span>


<span data-ttu-id="90c0c-310">Visual Studio에서 자동으로 목록 5에서 뷰를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-310">Visual Studio generates the view in Listing 5 automatically.</span></span> <span data-ttu-id="90c0c-311">이 뷰는 각 영화 클래스의 속성에 해당 하는 필드를 포함 하는 HTML 폼을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-311">This view contains an HTML form that includes fields that correspond to each of the properties of the Movie class.</span></span>

<span data-ttu-id="90c0c-312">**5-Views\Home\Create.aspx 나열**</span><span class="sxs-lookup"><span data-stu-id="90c0c-312">**Listing 5 – Views\Home\Create.aspx**</span></span>

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample5.aspx)]

> [!NOTE] 
> 
> <span data-ttu-id="90c0c-313">뷰 추가 대화 상자에서 생성 된 HTML 양식 Id 양식 필드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-313">The HTML form generated by the Add View dialog generates an Id form field.</span></span> <span data-ttu-id="90c0c-314">Id 열이 Id 열 이기 때문에이 양식 필드가 필요 하지 않습니다 하 고 안전 하 게 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-314">Because the Id column is an Identity column, we don't need this form field and you can safely remove it.</span></span>


<span data-ttu-id="90c0c-315">만들기 뷰를 추가한 후에 데이터베이스에 새 영화 레코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-315">After you add the Create view, you can add new Movie records to the database.</span></span> <span data-ttu-id="90c0c-316">F5 키를 눌러 응용 프로그램을 실행 하 고 그림 13에서 양식을 보려면 새로 만들기 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-316">Run your application by pressing the F5 key and click the Create New link to see the form in Figure 13.</span></span> <span data-ttu-id="90c0c-317">완료 하 고 양식을 제출 하는 경우 새 영화 데이터베이스 레코드가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-317">If you complete and submit the form, a new movie database record is created.</span></span>

<span data-ttu-id="90c0c-318">표시 양식 유효성 검사를 자동으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-318">Notice that you get form validation automatically.</span></span> <span data-ttu-id="90c0c-319">동영상, 릴리스 날짜를 입력 하는 것을 잊은 또는 잘못 된 릴리스 날짜를 입력할 경우 그런 다음 양식을 다시 표시 됩니다 하 고 릴리스 날짜 필드를 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-319">If you neglect to enter a release date for a movie, or you enter an invalid release date, then the form is redisplayed and the release date field is highlighted.</span></span>


<span data-ttu-id="90c0c-320">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="90c0c-320">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image25.png)</span></span>

<span data-ttu-id="90c0c-321">**그림 13**: 새 영화 데이터베이스 레코드를 만드는 ([큰 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image26.png))</span><span class="sxs-lookup"><span data-stu-id="90c0c-321">**Figure 13**: Creating a new movie database record ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image26.png))</span></span>


## <a name="editing-existing-database-records"></a><span data-ttu-id="90c0c-322">기존 데이터베이스 레코드를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-322">Editing Existing Database Records</span></span>

<span data-ttu-id="90c0c-323">이전 섹션에서 나열 하 고 새 데이터베이스 레코드를 만들 수 있습니다 하는 방법을 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-323">In the previous sections, we discussed how you can list and create new database records.</span></span> <span data-ttu-id="90c0c-324">이 최종 섹션에서는 기존 데이터베이스 레코드를 편집할 수는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-324">In this final section, we discuss how you can edit existing database records.</span></span>

<span data-ttu-id="90c0c-325">먼저 편집 양식 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-325">First, we need to generate the Edit form.</span></span> <span data-ttu-id="90c0c-326">Visual Studio에서 편집 폼에 자동으로 생성 되므로이 단계는 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-326">This step is easy since Visual Studio will generate the Edit form for us automatically.</span></span> <span data-ttu-id="90c0c-327">Visual Studio code 편집기에서 HomeController.vb 클래스를 열고이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-327">Open the HomeController.vb class in the Visual Studio code editor and follow these steps:</span></span>

1. <span data-ttu-id="90c0c-328">코드 편집기에서 되 메서드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **뷰 추가** (그림 14 참조).</span><span class="sxs-lookup"><span data-stu-id="90c0c-328">Right-click the Edit() method in the code editor and select the menu option **Add View** (see Figure 14).</span></span>
2. <span data-ttu-id="90c0c-329">레이블이 지정 된 확인란 **강력한 형식의 뷰를 만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-329">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
3. <span data-ttu-id="90c0c-330">**콘텐츠 보기** 드롭다운 목록에서 값을 선택 *편집*합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-330">From the **View content** dropdown list, select the value *Edit*.</span></span>
4. <span data-ttu-id="90c0c-331">**데이터 클래스를 보려면** 드롭다운 목록에서 값을 선택 *MovieApp.Movie*합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-331">From the **View data class** dropdown list, select the value *MovieApp.Movie*.</span></span>
5. <span data-ttu-id="90c0c-332">클릭 합니다 **추가** 새 뷰를 만들려면 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-332">Click the **Add** button to create the new view.</span></span>

<span data-ttu-id="90c0c-333">Views\Home 폴더 Edit.aspx 라는 새 뷰를 추가이 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-333">Completing these steps adds a new view named Edit.aspx to the Views\Home folder.</span></span> <span data-ttu-id="90c0c-334">이 뷰는 영화 레코드 편집에 대 한 HTML 폼을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-334">This view contains an HTML form for editing a movie record.</span></span>


<span data-ttu-id="90c0c-335">[![새 프로젝트 대화 상자](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="90c0c-335">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image27.png)</span></span>

<span data-ttu-id="90c0c-336">**그림 14**: 편집 뷰 추가 ([큰 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image28.png))</span><span class="sxs-lookup"><span data-stu-id="90c0c-336">**Figure 14**: Adding the Edit view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image28.png))</span></span>


> [!NOTE] 
> 
> <span data-ttu-id="90c0c-337">편집 보기 영화 Id 속성에 해당 하는 HTML 폼 필드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-337">The Edit view contains an HTML form field that corresponds to the Movie Id property.</span></span> <span data-ttu-id="90c0c-338">Id 속성의 값을 편집 하는 사람들이 않으려고 하기 때문에이 양식 필드를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-338">Because you don't want people editing the value of the Id property, you should remove this form field.</span></span>


<span data-ttu-id="90c0c-339">마지막으로, 데이터베이스 레코드를 편집을 지원 하도록 해당 Home 컨트롤러를 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-339">Finally, we need to modify the Home controller so that it supports editing a database record.</span></span> <span data-ttu-id="90c0c-340">업데이트 된 HomeController 클래스 목록 6에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-340">The updated HomeController class is contained in Listing 6.</span></span>

<span data-ttu-id="90c0c-341">**6-Controllers\HomeController.vb (편집 메서드)를 나열합니다.**</span><span class="sxs-lookup"><span data-stu-id="90c0c-341">**Listing 6 – Controllers\HomeController.vb (Edit methods)**</span></span>

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample6.vb)]

<span data-ttu-id="90c0c-342">6 목록에 추가 논리가 되 메서드의 두 오버 로드를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-342">In Listing 6, I've added additional logic to both overloads of the Edit() method.</span></span> <span data-ttu-id="90c0c-343">첫 번째 되 메서드 메서드에 전달 된 Id 매개 변수에 해당 하는 영화 데이터베이스 레코드를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-343">The first Edit() method returns the movie database record that corresponds to the Id parameter passed to the method.</span></span> <span data-ttu-id="90c0c-344">데이터베이스에서 동영상 레코드 업데이트를 수행 하는 두 번째 오버 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-344">The second overload performs the updates to a movie record in the database.</span></span>

<span data-ttu-id="90c0c-345">알림 원본 동영상을 검색 하 고 데이터베이스의 기존 영화를 업데이트 하려면 ApplyPropertyChanges() 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-345">Notice that you must retrieve the original movie, and then call ApplyPropertyChanges(), to update the existing movie in the database.</span></span>

## <a name="summary"></a><span data-ttu-id="90c0c-346">요약</span><span class="sxs-lookup"><span data-stu-id="90c0c-346">Summary</span></span>

<span data-ttu-id="90c0c-347">이 자습서의 목적은 ASP.NET MVC 응용 프로그램을 구축 하는 환경을 파악할 수 있도록 하는 것 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-347">The purpose of this tutorial was to give you a sense of the experience of building an ASP.NET MVC application.</span></span> <span data-ttu-id="90c0c-348">ASP.NET MVC 웹 응용 프로그램을 구축 하는 Active Server Pages 또는 ASP.NET 응용 프로그램을 구축 하는 환경을 매우 비슷합니다는 검색 하는 것이 좋겠습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-348">I hope that you discovered that building an ASP.NET MVC web application is very similar to the experience of building an Active Server Pages or ASP.NET application.</span></span>

<span data-ttu-id="90c0c-349">이 자습서에서는 ASP.NET MVC framework의 가장 기본적인 기능만 검사 했습니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-349">In this tutorial, we examined only the most basic features of the ASP.NET MVC framework.</span></span> <span data-ttu-id="90c0c-350">이후 자습서에서에서는 심층 탐구 컨트롤러, 컨트롤러 작업, 보기, 데이터 보기 및 HTML 도우미와 같은 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="90c0c-350">In future tutorials, we dive deeper into topics such as controllers, controller actions, views, view data, and HTML helpers.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="90c0c-351">이전</span><span class="sxs-lookup"><span data-stu-id="90c0c-351">Previous</span></span>](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs.md)
