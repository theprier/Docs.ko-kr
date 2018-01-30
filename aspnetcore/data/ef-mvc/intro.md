---
title: "ASP.NET Core MVC Entity Framework 코어 자습서 1 / 10 인"
author: tdykstra
description: 
manager: wpickett
ms.author: tdykstra
ms.date: 03/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: data/ef-mvc/intro
ms.openlocfilehash: 7de43a390ee0e11f6eda811b0774343ab330c53b
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="getting-started-with-aspnet-core-mvc-and-entity-framework-core-using-visual-studio-1-of-10"></a><span data-ttu-id="c15e3-102">Visual Studio (1 / 10)을 사용 하 여 Entity Framework Core 및 ASP.NET Core MVC 시작</span><span class="sxs-lookup"><span data-stu-id="c15e3-102">Getting started with ASP.NET Core MVC and Entity Framework Core using Visual Studio (1 of 10)</span></span>

<span data-ttu-id="c15e3-103">여 [Tom Dykstra](https://github.com/tdykstra) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="c15e3-103">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="c15e3-104">이 자습서의 Razor 페이지 버전을 사용할 수 [여기](xref:data/ef-rp/intro)합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-104">A Razor Pages version of this tutorial is available [here](xref:data/ef-rp/intro).</span></span> <span data-ttu-id="c15e3-105">Razor 페이지 버전은 좀 더 쉽게 따라 할 수 있으며 더 많은 EF 기능을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-105">The Razor Pages version is easier to follow and covers more EF features.</span></span> <span data-ttu-id="c15e3-106">따라야 하는 것이 좋습니다는 [이 자습서의 Razor 페이지 버전](xref:data/ef-rp/intro)합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-106">We recommend you follow the [Razor Pages version of this tutorial](xref:data/ef-rp/intro).</span></span>

<span data-ttu-id="c15e3-107">Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework (EF) 코어 2.0 및 Visual Studio 2017을 사용 하 여 ASP.NET 코어 2.0 MVC 웹 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-107">The Contoso University sample web application demonstrates how to create ASP.NET Core 2.0 MVC web applications using Entity Framework (EF) Core 2.0 and Visual Studio 2017.</span></span>

<span data-ttu-id="c15e3-108">샘플 응용 프로그램은 웹 사이트 가상 Contoso 대학입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-108">The sample application is a web site for a fictional Contoso University.</span></span> <span data-ttu-id="c15e3-109">학생 진입, 과정 만들기 및 강사 할당 등의 기능을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-109">It includes functionality such as student admission, course creation, and instructor assignments.</span></span> <span data-ttu-id="c15e3-110">처음부터 Contoso 대학 샘플 응용 프로그램을 빌드하는 방법을 설명 하는 자습서 시리즈의 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-110">This is the first in a series of tutorials that explain how to build the Contoso University sample application from scratch.</span></span>

[<span data-ttu-id="c15e3-111">다운로드 하거나 완성 된 응용 프로그램을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-111">Download or view the completed application.</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final)

<span data-ttu-id="c15e3-112">EF 코어 2.0 최신 버전의 EF 이지만 EF의 모든 기능에 아직 없는 6.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-112">EF Core 2.0 is the latest version of EF but doesn't yet have all the features of EF 6.x.</span></span> <span data-ttu-id="c15e3-113">EF 선택 하는 방법에 대 한 내용은 6.x 및 EF 코어 참조 [EF 코어 vs. EF6.x](https://docs.microsoft.com/ef/efcore-and-ef6/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-113">For information about how to choose between EF 6.x and EF Core, see [EF Core vs. EF6.x](https://docs.microsoft.com/ef/efcore-and-ef6/).</span></span> <span data-ttu-id="c15e3-114">EF를 선택 하는 경우 6.x 참조 [이 자습서 시리즈의 이전 버전](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-114">If you choose EF 6.x, see [the previous version of this tutorial series](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

> [!NOTE]
> * <span data-ttu-id="c15e3-115">이 자습서의 ASP.NET Core 1.1 버전에 대 한 참조는 [PDF 형식으로이 자습서의 VS 2017 업데이트 2 버전](https://github.com/aspnet/Docs/blob/master/aspnetcore/data/ef-mvc/intro/_static/efmvc1.1.pdf)합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-115">For the ASP.NET Core 1.1 version of this tutorial, see the [VS 2017 Update 2 version of this tutorial in PDF format](https://github.com/aspnet/Docs/blob/master/aspnetcore/data/ef-mvc/intro/_static/efmvc1.1.pdf).</span></span>
> * <span data-ttu-id="c15e3-116">이 자습서의 Visual Studio 2015 버전을 보려면 [VS 2015 version of ASP.NET Core documentation in PDF format](https://github.com/aspnet/Docs/blob/master/aspnetcore/common/_static/aspnet-core-project-json.pdf)(ASP.NET Core의 VS 2015 버전 설명서(PDF 형식))을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c15e3-116">For the Visual Studio 2015 version of this tutorial, see the [VS 2015 version of ASP.NET Core documentation in PDF format](https://github.com/aspnet/Docs/blob/master/aspnetcore/common/_static/aspnet-core-project-json.pdf).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c15e3-117">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="c15e3-117">Prerequisites</span></span>

[!INCLUDE[install 2.0](../../includes/install2.0.md)]

## <a name="troubleshooting"></a><span data-ttu-id="c15e3-118">문제 해결</span><span class="sxs-lookup"><span data-stu-id="c15e3-118">Troubleshooting</span></span>

<span data-ttu-id="c15e3-119">솔루션에 코드를 비교 하 여 일반적으로 찾을 수 문제를 해결할 수 없는 실행 하는 경우는 [완료 된 프로젝트](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final)합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-119">If you run into a problem you can't resolve, you can generally find the solution by comparing your code to the [completed project](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-mvc/intro/samples/cu-final).</span></span> <span data-ttu-id="c15e3-120">일반적인 오류 및 해결 방법을 목록은 참조 하십시오. [계열의 마지막 자습서의 문제 해결 섹션](advanced.md#common-errors)합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-120">For a list of common errors and how to solve them, see [the Troubleshooting section of the last tutorial in the series](advanced.md#common-errors).</span></span> <span data-ttu-id="c15e3-121">에 대 한 StackOverflow.com에 질문을 게시할 수 필요한 있습니다을 찾지 못한 경우 [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) 또는 [EF 코어](https://stackoverflow.com/questions/tagged/entity-framework-core)합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-121">If you don't find what you need there, you can post a question to StackOverflow.com for [ASP.NET Core](https://stackoverflow.com/questions/tagged/asp.net-core) or [EF Core](https://stackoverflow.com/questions/tagged/entity-framework-core).</span></span>

> [!TIP] 
> <span data-ttu-id="c15e3-122">각각 이전 자습서에서 수행 되는 동작과 기반으로 하는 일련의 10 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-122">This is a series of 10 tutorials, each of which builds on what is done in earlier tutorials.</span></span> <span data-ttu-id="c15e3-123">각 자습서 완료 후 프로젝트의 복사본을 저장 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-123">Consider saving a copy of the project after each successful tutorial completion.</span></span> <span data-ttu-id="c15e3-124">문제를 실행 하는 경우에 전체 계열의 시작 부분으로 다시 이동 하지 않고도 이전 자습서에서를 통해 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-124">Then if you run into problems, you can start over from the previous tutorial instead of going back to the beginning of the whole series.</span></span>

## <a name="the-contoso-university-web-application"></a><span data-ttu-id="c15e3-125">Contoso 대학 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="c15e3-125">The Contoso University web application</span></span>

<span data-ttu-id="c15e3-126">이 자습서에를 작성 하는 응용 프로그램은 간단한 대학 웹 사이트.</span><span class="sxs-lookup"><span data-stu-id="c15e3-126">The application you'll be building in these tutorials is a simple university web site.</span></span>

<span data-ttu-id="c15e3-127">사용자가 볼 수 있으며 학생과에서는 강사 정보 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-127">Users can view and update student, course, and instructor information.</span></span> <span data-ttu-id="c15e3-128">다음은 몇 화면을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-128">Here are a few of the screens you'll create.</span></span>

![학생 인덱스 페이지](intro/_static/students-index.png)

![학생 편집 페이지](intro/_static/student-edit.png)

<span data-ttu-id="c15e3-131">이 자습서는 Entity Framework를 사용 하는 방법에 주로 초점을 맞출 수 있도록이 사이트의 사용자 인터페이스 스타일은 기본 제공 템플릿에서 생성 내용을 가까운 유지 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-131">The UI style of this site has been kept close to what's generated by the built-in templates, so that the tutorial can focus mainly on how to use the Entity Framework.</span></span>

## <a name="create-an-aspnet-core-mvc-web-application"></a><span data-ttu-id="c15e3-132">ASP.NET Core MVC 웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c15e3-132">Create an ASP.NET Core MVC web application</span></span>

<span data-ttu-id="c15e3-133">Visual Studio를 열고 ASP.NET Core C# 웹 라는 새 프로젝트 "ContosoUniversity"를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-133">Open Visual Studio and create a new ASP.NET Core C# web project named "ContosoUniversity".</span></span>

* <span data-ttu-id="c15e3-134">**파일** 메뉴 선택 **새로 만들기 > 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-134">From the **File** menu, select **New > Project**.</span></span>

* <span data-ttu-id="c15e3-135">왼쪽된 창에서 선택 **설치 > Visual C# > 웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-135">From the left pane, select **Installed > Visual C# > Web**.</span></span>

* <span data-ttu-id="c15e3-136">**ASP.NET Core 웹 응용 프로그램** 프로젝트 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-136">Select the **ASP.NET Core Web Application** project template.</span></span>

* <span data-ttu-id="c15e3-137">입력 **ContosoUniversity** 이름과 클릭으로 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-137">Enter **ContosoUniversity** as the name and click **OK**.</span></span>

  ![새 프로젝트 대화 상자](intro/_static/new-project.png)

* <span data-ttu-id="c15e3-139">에 대 한 대기는 **새 ASP.NET Core 웹 응용 프로그램 (.NET Core)** 대화 상자를 표시</span><span class="sxs-lookup"><span data-stu-id="c15e3-139">Wait for the **New ASP.NET Core Web Application (.NET Core)** dialog to appear</span></span>

* <span data-ttu-id="c15e3-140">선택 **ASP.NET 코어 2.0** 및 **웹 응용 프로그램 (모델-뷰-컨트롤러)** 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-140">Select **ASP.NET Core 2.0** and the **Web Application (Model-View-Controller)** template.</span></span>

  <span data-ttu-id="c15e3-141">**참고:** ASP.NET 코어 2.0 및 EF 코어 2.0 이상-있는지 확인 하는이 자습서에서는 **ASP.NET Core 1.1** 선택 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-141">**Note:** This tutorial requires ASP.NET Core 2.0 and EF Core 2.0 or later -- make sure that **ASP.NET Core 1.1** isn't selected.</span></span>

* <span data-ttu-id="c15e3-142">확인 **인증** 로 설정 된 **인증 안 함**합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-142">Make sure **Authentication** is set to **No Authentication**.</span></span>

* <span data-ttu-id="c15e3-143"> **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-143">Click **OK**</span></span>

  ![새 ASP.NET 프로젝트 대화 상자](intro/_static/new-aspnet.png)

## <a name="set-up-the-site-style"></a><span data-ttu-id="c15e3-145">사이트 스타일 설정</span><span class="sxs-lookup"><span data-stu-id="c15e3-145">Set up the site style</span></span>

<span data-ttu-id="c15e3-146">몇 가지 간단한 변경 사항이 사이트 메뉴, 레이아웃 및 홈 페이지를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-146">A few simple changes will set up the site menu, layout, and home page.</span></span>

<span data-ttu-id="c15e3-147">열기 *Views/Shared/_Layout.cshtml* 다음과 같이 변경 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-147">Open *Views/Shared/_Layout.cshtml* and make the following changes:</span></span>

* <span data-ttu-id="c15e3-148">"ContosoUniversity"의 "Contoso 대학"으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-148">Change each occurrence of "ContosoUniversity" to "Contoso University".</span></span> <span data-ttu-id="c15e3-149">다음과 같은 세 가지 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-149">There are three occurrences.</span></span>

* <span data-ttu-id="c15e3-150">메뉴 항목에 대 한 추가 **학생**, **Courses**, **강사**, 및 **부서**, 및 삭제는 **연락처** 메뉴 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-150">Add menu entries for **Students**, **Courses**, **Instructors**, and **Departments**, and delete the **Contact** menu entry.</span></span>

<span data-ttu-id="c15e3-151">변경 내용은 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-151">The changes are highlighted.</span></span>

[!code-cshtml[](intro/samples/cu/Views/Shared/_Layout.cshtml?highlight=6,30,36-39,48)]

<span data-ttu-id="c15e3-152">*Views/Home/Index.cshtml*, 파일의 내용을이 응용 프로그램에 대 한 텍스트도 ASP.NET MVC에 대 한 텍스트를 바꾸려면 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-152">In *Views/Home/Index.cshtml*, replace the contents of the file with the following code to replace the text about ASP.NET and MVC with text about this application:</span></span>

[!code-cshtml[](intro/samples/cu/Views/Home/Index.cshtml)]

<span data-ttu-id="c15e3-153">CTRL + f5 키를 눌러 프로젝트를 실행 하거나 선택할 **디버그 > 디버깅 하지 않고 시작** 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-153">Press CTRL+F5 to run the project or choose **Debug > Start Without Debugging** from the menu.</span></span> <span data-ttu-id="c15e3-154">이 자습서에서 만드는 페이지에 대 한 탭이 포함 된 홈 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-154">You see the home page with tabs for the pages you'll create in these tutorials.</span></span>

![Contoso 대학 홈 페이지](intro/_static/home-page.png)

## <a name="entity-framework-core-nuget-packages"></a><span data-ttu-id="c15e3-156">Entity Framework Core NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="c15e3-156">Entity Framework Core NuGet packages</span></span>

<span data-ttu-id="c15e3-157">EF 핵심 지원에는 프로젝트를 추가 하려면 대상으로 지정할 데이터베이스 공급자를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-157">To add EF Core support to a project, install the database provider that you want to target.</span></span> <span data-ttu-id="c15e3-158">이 자습서에서는 SQL Server, 사용 및 공급자 패키지는 [Microsoft.EntityFrameworkCore.SqlServer](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.SqlServer/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-158">This tutorial uses SQL Server, and the provider package is [Microsoft.EntityFrameworkCore.SqlServer](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.SqlServer/).</span></span> <span data-ttu-id="c15e3-159">이 패키지에 포함 되어는 [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) metapackage, 하므로 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-159">This package is included in the [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) metapackage, so you don't have to install it.</span></span>

<span data-ttu-id="c15e3-160">이 패키지 및 해당 종속성 (`Microsoft.EntityFrameworkCore` 및 `Microsoft.EntityFrameworkCore.Relational`) EF에 대 한 런타임 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-160">This package and its dependencies (`Microsoft.EntityFrameworkCore` and `Microsoft.EntityFrameworkCore.Relational`) provide runtime support for EF.</span></span> <span data-ttu-id="c15e3-161">도구 패키지를 추가 합니다의 뒷부분에 나오는 [마이그레이션](migrations.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-161">You'll add a tooling package later, in the [Migrations](migrations.md) tutorial.</span></span> 

<span data-ttu-id="c15e3-162">Entity Framework Core에 사용할 수 있는 다른 데이터베이스 공급자에 대 한 정보를 참조 하십시오. [데이터베이스 공급자](https://docs.microsoft.com/ef/core/providers/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-162">For information about other database providers that are available for Entity Framework Core, see [Database providers](https://docs.microsoft.com/ef/core/providers/).</span></span>

## <a name="create-the-data-model"></a><span data-ttu-id="c15e3-163">데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="c15e3-163">Create the data model</span></span>

<span data-ttu-id="c15e3-164">다음 Contoso 대학교 응용 프로그램에 대 한 엔터티 클래스 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-164">Next you'll create entity classes for the Contoso University application.</span></span> <span data-ttu-id="c15e3-165">다음 세 가지 엔터티부터 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-165">You'll start with the following three entities.</span></span>

![학생-등록 과정-데이터 모델 다이어그램](intro/_static/data-model-diagram.png)

<span data-ttu-id="c15e3-167">간의 일 대 다 관계가 `Student` 및 `Enrollment` 엔터티 간의 일 대 다 관계 이며 `Course` 및 `Enrollment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c15e3-167">There's a one-to-many relationship between `Student` and `Enrollment` entities, and there's a one-to-many relationship between `Course` and `Enrollment` entities.</span></span> <span data-ttu-id="c15e3-168">즉, 학생 과정을 개수에 관계 없이 등록 될 수 있습니다 및 과정에 학생에 등록 여러 개가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-168">In other words, a student can be enrolled in any number of courses, and a course can have any number of students enrolled in it.</span></span>

<span data-ttu-id="c15e3-169">다음 섹션에서는 각각에 대 한 이러한 엔터티의 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-169">In the following sections you'll create a class for each one of these entities.</span></span>

### <a name="the-student-entity"></a><span data-ttu-id="c15e3-170">학생 엔터티</span><span class="sxs-lookup"><span data-stu-id="c15e3-170">The Student entity</span></span>

![학생 엔터티 다이어그램](intro/_static/student-entity.png)

<span data-ttu-id="c15e3-172">에 *모델* 폴더를 라는 클래스 파일을 만들어 *Student.cs* 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-172">In the *Models* folder, create a class file named *Student.cs* and replace the template code with the following code.</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_Intro)]

<span data-ttu-id="c15e3-173">`ID` 속성이이 클래스에 해당 하는 데이터베이스 테이블의 기본 키 열이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-173">The `ID` property will become the primary key column of the database table that corresponds to this class.</span></span> <span data-ttu-id="c15e3-174">Entity Framework를 기본적으로 명명 된 속성을 해석 `ID` 또는 `classnameID` 기본 키로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-174">By default, the Entity Framework interprets a property that's named `ID` or `classnameID` as the primary key.</span></span>

<span data-ttu-id="c15e3-175">`Enrollments` 속성은 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-175">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="c15e3-176">이 엔터티와 관련 된 다른 엔터티와 탐색 속성을 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-176">Navigation properties hold other entities that are related to this entity.</span></span> <span data-ttu-id="c15e3-177">이 경우는 `Enrollments` 속성의는 `Student entity` 를 모두 보유할는 `Enrollment` 엔터티는 관련 된 `Student` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c15e3-177">In this case, the `Enrollments` property of a `Student entity` will hold all of the `Enrollment` entities that are related to that `Student` entity.</span></span> <span data-ttu-id="c15e3-178">즉, 하는 경우 데이터베이스의 지정된 된 학생 행에 두 개의 관련 된 등록 행 (해당 StudentID 외래 키 열에 해당 학생의 기본 키 값을 포함 하는 행)는 `Student` 엔터티의 `Enrollments` 탐색 속성은 포함 하는 것 두 개의 `Enrollment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c15e3-178">In other words, if a given Student row in the database has two related Enrollment rows (rows that contain that student's primary key value in their StudentID foreign key column), that `Student` entity's `Enrollments` navigation property will contain those two `Enrollment` entities.</span></span>

<span data-ttu-id="c15e3-179">해당 형식은 항목 추가, 삭제 및 업데이트와 같은 될 수 있는 목록 이어야 합니다는 탐색 속성 (예: 다 대 다 또는 일 대 다 관계) 여러 엔터티를 보유할 수, 하는 경우 `ICollection<T>`합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-179">If a navigation property can hold multiple entities (as in many-to-many or one-to-many relationships), its type must be a list in which entries can be added, deleted, and updated, such as `ICollection<T>`.</span></span> <span data-ttu-id="c15e3-180">지정할 수 있습니다 `ICollection<T>` 또는 형식으로 `List<T>` 또는 `HashSet<T>`합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-180">You can specify `ICollection<T>` or a type such as `List<T>` or `HashSet<T>`.</span></span> <span data-ttu-id="c15e3-181">지정 하는 경우 `ICollection<T>`, EF 만듭니다는 `HashSet<T>` 기본적으로 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-181">If you specify `ICollection<T>`, EF creates a `HashSet<T>` collection by default.</span></span>

### <a name="the-enrollment-entity"></a><span data-ttu-id="c15e3-182">등록 엔터티</span><span class="sxs-lookup"><span data-stu-id="c15e3-182">The Enrollment entity</span></span>

![등록 엔터티 다이어그램](intro/_static/enrollment-entity.png)

<span data-ttu-id="c15e3-184">에 *모델* 폴더를 만들 *Enrollment.cs* 기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-184">In the *Models* folder, create *Enrollment.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Enrollment.cs?name=snippet_Intro)]

<span data-ttu-id="c15e3-185">`EnrollmentID` 속성은 기본 키를 됩니다;이 엔터티 사용는 `classnameID` 대신 패턴 `ID` 에서 본 것 처럼 자체적으로 `Student` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c15e3-185">The `EnrollmentID` property will be the primary key; this entity uses the `classnameID` pattern instead of `ID` by itself as you saw in the `Student` entity.</span></span> <span data-ttu-id="c15e3-186">일반적으로 한 패턴을 선택 하는 데이터 모델 전체에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-186">Ordinarily you would choose one pattern and use it throughout your data model.</span></span> <span data-ttu-id="c15e3-187">여기서는 변형 패턴 중 하나를 사용할 수 있는 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-187">Here, the variation illustrates that you can use either pattern.</span></span> <span data-ttu-id="c15e3-188">에 [이후의 자습서](inheritance.md), 어떻게 ID를 사용 하 여 응용 프로그램 이름 없이 쉽게 상속을 구현 하려면 데이터 모델에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-188">In a [later tutorial](inheritance.md), you'll see how using ID without classname makes it easier to implement inheritance in the data model.</span></span>

<span data-ttu-id="c15e3-189">`Grade` 속성은 한 `enum`합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-189">The `Grade` property is an `enum`.</span></span> <span data-ttu-id="c15e3-190">다음 매개 변수는 `Grade` 형식 선언을 나타냅니다는 `Grade` 속성은 null을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-190">The question mark after the `Grade` type declaration indicates that the `Grade` property is nullable.</span></span> <span data-ttu-id="c15e3-191">Null이 등급은 0 개 등급 다릅니다-null 의미는 등급 알려진 또는 아직 할당 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-191">A grade that's null is different from a zero grade -- null means a grade isn't known or hasn't been assigned yet.</span></span>

<span data-ttu-id="c15e3-192">`StudentID` 속성은 외래 키 및 해당 탐색 속성은 `Student`합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-192">The `StudentID` property is a foreign key, and the corresponding navigation property is `Student`.</span></span> <span data-ttu-id="c15e3-193">`Enrollment` 엔터티는 하 나와 연결 `Student` 엔터티, 속성에는 단일만 포함할 수 있으므로 `Student` 엔터티 (달리는 `Student.Enrollments` 탐색 속성 했 듯이, 여러을 보유할 수 있는 `Enrollment` 엔터티)입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-193">An `Enrollment` entity is associated with one `Student` entity, so the property can only hold a single `Student` entity (unlike the `Student.Enrollments` navigation property you saw earlier, which can hold multiple `Enrollment` entities).</span></span>

<span data-ttu-id="c15e3-194">`CourseID` 속성은 외래 키 및 해당 탐색 속성은 `Course`합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-194">The `CourseID` property is a foreign key, and the corresponding navigation property is `Course`.</span></span> <span data-ttu-id="c15e3-195">`Enrollment` 엔터티는 하 나와 연결 `Course` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c15e3-195">An `Enrollment` entity is associated with one `Course` entity.</span></span>

<span data-ttu-id="c15e3-196">Entity Framework 라고 하는 경우 외래 키 속성으로 속성을 해석 `<navigation property name><primary key property name>` (예를 들어 `StudentID` 에 대 한는 `Student` 이후 탐색 속성에서 `Student` 엔터티의 기본 키가 `ID`).</span><span class="sxs-lookup"><span data-stu-id="c15e3-196">Entity Framework interprets a property as a foreign key property if it's named `<navigation property name><primary key property name>` (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="c15e3-197">외래 키 속성은 단순히 또한 이름은 수 `<primary key property name>` (예를 들어 `CourseID` 이후는 `Course` 엔터티의 기본 키가 `CourseID`).</span><span class="sxs-lookup"><span data-stu-id="c15e3-197">Foreign key properties can also be named simply `<primary key property name>` (for example, `CourseID` since the `Course` entity's primary key is `CourseID`).</span></span>

### <a name="the-course-entity"></a><span data-ttu-id="c15e3-198">과정 엔터티</span><span class="sxs-lookup"><span data-stu-id="c15e3-198">The Course entity</span></span>

![과정 엔터티 다이어그램](intro/_static/course-entity.png)

<span data-ttu-id="c15e3-200">에 *모델* 폴더를 만들 *Course.cs* 기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-200">In the *Models* folder, create *Course.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Course.cs?name=snippet_Intro)]

<span data-ttu-id="c15e3-201">`Enrollments` 속성은 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-201">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="c15e3-202">A `Course` 개수에 관계 없이 관련 될 수 있는 엔터티 `Enrollment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c15e3-202">A `Course` entity can be related to any number of `Enrollment` entities.</span></span>

<span data-ttu-id="c15e3-203">에 대 한 내용은 라고는 `DatabaseGenerated` 특성에 [이후의 자습서](complex-data-model.md) 이 시리즈의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-203">We'll say more about the `DatabaseGenerated` attribute in a [later tutorial](complex-data-model.md) in this series.</span></span> <span data-ttu-id="c15e3-204">기본적으로,이 특성 과정 대신 생성 하는 데이터베이스에 대 한 기본 키를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-204">Basically, this attribute lets you enter the primary key for the course rather than having the database generate it.</span></span>

## <a name="create-the-database-context"></a><span data-ttu-id="c15e3-205">데이터베이스 컨텍스트 만들기</span><span class="sxs-lookup"><span data-stu-id="c15e3-205">Create the Database Context</span></span>

<span data-ttu-id="c15e3-206">지정된 된 데이터 모델에 대 한 Entity Framework 기능을 조정 하는 기본 클래스는 데이터베이스 컨텍스트 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-206">The main class that coordinates Entity Framework functionality for a given data model is the database context class.</span></span> <span data-ttu-id="c15e3-207">`Microsoft.EntityFrameworkCore.DbContext` 클래스에서 파생시키는 방식으로 이 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-207">You create this class by deriving from the `Microsoft.EntityFrameworkCore.DbContext` class.</span></span> <span data-ttu-id="c15e3-208">코드에서 데이터 모델에 포함 된 엔터티 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-208">In your code you specify which entities are included in the data model.</span></span> <span data-ttu-id="c15e3-209">특정 Entity Framework 동작을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-209">You can also customize certain Entity Framework behavior.</span></span> <span data-ttu-id="c15e3-210">이 프로젝트에 클래스 이름은 `SchoolContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-210">In this project, the class is named `SchoolContext`.</span></span>

<span data-ttu-id="c15e3-211">프로젝트 폴더에 라는 폴더를 만듭니다 *데이터*합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-211">In the project folder, create a folder named *Data*.</span></span>

<span data-ttu-id="c15e3-212">에 *데이터* 폴더 라는 새 클래스 파일을 만들 *SchoolContext.cs*, 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-212">In the *Data* folder create a new class file named *SchoolContext.cs*, and replace the template code with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_Intro)]

<span data-ttu-id="c15e3-213">이 코드에서는 `DbSet` 각 엔터티 집합에 대 한 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-213">This code creates a `DbSet` property for each entity set.</span></span> <span data-ttu-id="c15e3-214">Entity Framework 용어에서 엔터티 집합은 일반적으로 데이터베이스 테이블에 해당하고 엔터티는 테이블의 행에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-214">In Entity Framework terminology, an entity set typically corresponds to a database table, and an entity corresponds to a row in the table.</span></span>

<span data-ttu-id="c15e3-215">생략 한 하면는 `DbSet<Enrollment>` 및 `DbSet<Course>` 문과 것은 동일 하 게 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-215">You could've omitted the `DbSet<Enrollment>` and `DbSet<Course>` statements and it would work the same.</span></span> <span data-ttu-id="c15e3-216">Entity Framework 하기 때문에 암시적으로 해당 포함 됩니다는 `Student` 엔터티 참조는 `Enrollment` 엔터티 및 `Enrollment` 엔터티 참조는 `Course` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c15e3-216">The Entity Framework would include them implicitly because the `Student` entity references the `Enrollment` entity and the `Enrollment` entity references the `Course` entity.</span></span>

<span data-ttu-id="c15e3-217">EF는 데이터베이스를 만들 때 같은 이름을 갖는 테이블을 만듭니다는 `DbSet` 속성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-217">When the database is created, EF creates tables that have names the same as the `DbSet` property names.</span></span> <span data-ttu-id="c15e3-218">컬렉션에 대 한 속성 이름에는 일반적으로 (학생을 하지 않고 학생) 복수형 하지만 개발자 또는 테이블 이름을 복수화 여부에 대 한 동의.</span><span class="sxs-lookup"><span data-stu-id="c15e3-218">Property names for collections are typically plural (Students rather than Student), but developers disagree about whether table names should be pluralized or not.</span></span> <span data-ttu-id="c15e3-219">이 자습서에 대 한 DbContext 단 수 테이블 이름을 지정 하 여 기본 동작을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-219">For these tutorials you'll override the default behavior by specifying singular table names in the DbContext.</span></span> <span data-ttu-id="c15e3-220">이렇게 하려면 마지막 DbSet 속성 뒤 다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-220">To do that, add the following highlighted code after the last DbSet property.</span></span>

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_TableNames&highlight=16-21)]

## <a name="register-the-context-with-dependency-injection"></a><span data-ttu-id="c15e3-221">종속성 주입 컨텍스트 등록</span><span class="sxs-lookup"><span data-stu-id="c15e3-221">Register the context with dependency injection</span></span>

<span data-ttu-id="c15e3-222">ASP.NET Core 구현 [종속성 주입](../../fundamentals/dependency-injection.md) 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-222">ASP.NET Core implements [dependency injection](../../fundamentals/dependency-injection.md) by default.</span></span> <span data-ttu-id="c15e3-223">서비스 (예: EF 데이터베이스 컨텍스트) 종속성 주입 응용 프로그램 시작 중에 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-223">Services (such as the EF database context) are registered with dependency injection during application startup.</span></span> <span data-ttu-id="c15e3-224">이러한 서비스 (예: MVC 컨트롤러)에 필요한 구성 요소를 생성자 매개 변수를 통해 이러한 서비스 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-224">Components that require these services (such as MVC controllers) are provided these services via constructor parameters.</span></span> <span data-ttu-id="c15e3-225">이 자습서의 뒷부분에 나오는 컨텍스트 인스턴스를 가져오는 컨트롤러 생성자 코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-225">You'll see the controller constructor code that gets a context instance later in this tutorial.</span></span>

<span data-ttu-id="c15e3-226">등록 하려면 `SchoolContext` 서비스를 열고 *Startup.cs*, 강조 표시 된 줄을 추가 하 고는 `ConfigureServices` 메서드.</span><span class="sxs-lookup"><span data-stu-id="c15e3-226">To register `SchoolContext` as a service, open *Startup.cs*, and add the highlighted lines to the `ConfigureServices` method.</span></span>

[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_SchoolContext&highlight=3-4)]

<span data-ttu-id="c15e3-227">연결 문자열의 이름에는 메서드를 호출 하 여 컨텍스트에 전달 됩니다는 `DbContextOptionsBuilder` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-227">The name of the connection string is passed in to the context by calling a method on a `DbContextOptionsBuilder` object.</span></span> <span data-ttu-id="c15e3-228">로컬 개발에 대 한는 [ASP.NET Core 구성 시스템](xref:fundamentals/configuration/index) 는 연결 문자열에서 *appsettings.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-228">For local development, the [ASP.NET Core configuration system](xref:fundamentals/configuration/index) reads the connection string from the *appsettings.json* file.</span></span>

<span data-ttu-id="c15e3-229">추가 `using` 에 대 한 문을 `ContosoUniversity.Data` 및 `Microsoft.EntityFrameworkCore` 네임 스페이스에 다음 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-229">Add `using` statements for `ContosoUniversity.Data` and `Microsoft.EntityFrameworkCore` namespaces, and then build the project.</span></span>

[!code-csharp[Main](intro/samples/cu/Startup.cs?name=snippet_Usings)]

<span data-ttu-id="c15e3-230">열기는 *appsettings.json* 파일을 다음 예제와 같이 연결 문자열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-230">Open the *appsettings.json* file and add a connection string as shown in the following example.</span></span>

[!code-json[](./intro/samples/cu/appsettings1.json?highlight=2-4)]

### <a name="sql-server-express-localdb"></a><span data-ttu-id="c15e3-231">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="c15e3-231">SQL Server Express LocalDB</span></span>

<span data-ttu-id="c15e3-232">연결 문자열은 SQL Server LocalDB 데이터베이스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-232">The connection string specifies a SQL Server LocalDB database.</span></span> <span data-ttu-id="c15e3-233">LocalDB는 SQL Server Express 데이터베이스 엔진의 경량 버전 하며 응용 프로그램 개발의 경우 프로덕션 환경에서 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-233">LocalDB is a lightweight version of the SQL Server Express Database Engine and is intended for application development, not production use.</span></span> <span data-ttu-id="c15e3-234">LocalDB 요청 시 시작 하 고 사용자 모드에서 실행 되므로 복잡 한 구성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-234">LocalDB starts on demand and runs in user mode, so there's no complex configuration.</span></span> <span data-ttu-id="c15e3-235">기본적으로 LocalDB 만듭니다 *.mdf* 데이터베이스 파일에는 `C:/Users/<user>` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-235">By default, LocalDB creates *.mdf* database files in the `C:/Users/<user>` directory.</span></span>

## <a name="add-code-to-initialize-the-database-with-test-data"></a><span data-ttu-id="c15e3-236">테스트 데이터로 데이터베이스를 초기화 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-236">Add code to initialize the database with test data</span></span>

<span data-ttu-id="c15e3-237">Entity Framework에서 빈 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-237">The Entity Framework will create an empty database for you.</span></span> <span data-ttu-id="c15e3-238">이 섹션에서는 테스트 데이터로 채우기 위해 데이터베이스를 만든 후 호출 되는 메서드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-238">In this section, you write a method that's called after the database is created in order to populate it with test data.</span></span>

<span data-ttu-id="c15e3-239">사용 하 여 여기에서 `EnsureCreated` 방법을 자동으로 데이터베이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-239">Here you'll use the `EnsureCreated` method to automatically create the database.</span></span> <span data-ttu-id="c15e3-240">에 [이후의 자습서](migrations.md) 삭제 하 고 데이터베이스를 다시 작성 하는 대신 데이터베이스 스키마를 변경 하려면 Code First 마이그레이션을 사용 하 여 모델 변경 내용을 처리 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-240">In a [later tutorial](migrations.md) you'll see how to handle model changes by using Code First Migrations to change the database schema instead of dropping and re-creating the database.</span></span>

<span data-ttu-id="c15e3-241">에 *데이터* 폴더 라는 새 클래스 파일을 만들 *DbInitializer.cs* 템플릿 코드 필요할 때 만들 데이터베이스를 다음 코드로 대체 하 고 부하 테스트 새 데이터 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-241">In the *Data* folder, create a new class file named *DbInitializer.cs* and replace the template code with the following code, which causes a database to be created when needed and loads test data into the new database.</span></span>

[!code-csharp[Main](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Intro)]

<span data-ttu-id="c15e3-242">코드는 데이터베이스의 어떤 학생 되는 경우 데이터베이스는 새로운 클래스 이며 테스트 데이터로 시드할 해야 하는 경우를 가정 그렇지 않은 경우를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-242">The code checks if there are any students in the database, and if not, it assumes the database is new and needs to be seeded with test data.</span></span> <span data-ttu-id="c15e3-243">배열에 테스트 데이터를 로드 하지 않고 `List<T>` 성능을 최적화 하는 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-243">It loads test data into arrays rather than `List<T>` collections to optimize performance.</span></span>

<span data-ttu-id="c15e3-244">*Program.cs*, 수정 된 `Main` 응용 프로그램 시작 시에 다음을 수행 하는 메서드:</span><span class="sxs-lookup"><span data-stu-id="c15e3-244">In *Program.cs*, modify the `Main` method to do the following on application startup:</span></span>

* <span data-ttu-id="c15e3-245">종속성 주입 컨테이너에서 데이터베이스 컨텍스트 인스턴스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-245">Get a database context instance from the dependency injection container.</span></span>
* <span data-ttu-id="c15e3-246">컨텍스트를 전달 하는 초기값 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-246">Call the seed method, passing to it the context.</span></span>
* <span data-ttu-id="c15e3-247">Seed 메서드 수행 되는 경우 컨텍스트를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-247">Dispose the context when the seed method is done.</span></span>

[!code-csharp[Main](intro/samples/cu/Program.cs?name=snippet_Seed&highlight=3-20)]

<span data-ttu-id="c15e3-248">추가 `using` 문:</span><span class="sxs-lookup"><span data-stu-id="c15e3-248">Add `using` statements:</span></span>

[!code-csharp[Main](intro/samples/cu/Program.cs?name=snippet_Usings)]

<span data-ttu-id="c15e3-249">이전 자습서에서 유사한 코드를 볼 수 있습니다는 `Configure` 메서드에서 *Startup.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-249">In older tutorials, you may see similar code in the `Configure` method in *Startup.cs*.</span></span> <span data-ttu-id="c15e3-250">사용 하는 것이 좋습니다는 `Configure` 요청 파이프라인을 설정할 때만 메서드.</span><span class="sxs-lookup"><span data-stu-id="c15e3-250">We recommend that you use the `Configure` method only to set up the request pipeline.</span></span> <span data-ttu-id="c15e3-251">응용 프로그램 시작 코드에 속하는 `Main` 메서드.</span><span class="sxs-lookup"><span data-stu-id="c15e3-251">Application startup code belongs in the `Main` method.</span></span>

<span data-ttu-id="c15e3-252">이제 처음 응용 프로그램을 실행 하면 데이터베이스 생성 되며 테스트 데이터를 사용 하 여 시드할 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-252">Now the first time you run the application, the database will be created and seeded with test data.</span></span> <span data-ttu-id="c15e3-253">데이터 모델을 변경할 때마다 데이터베이스를 삭제 하 고, 시드 메서드를 업데이트 하 고, 동일한 방식으로 새 데이터베이스로 후 새로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-253">Whenever you change your data model, you can delete the database, update your seed method, and start afresh with a new database the same way.</span></span> <span data-ttu-id="c15e3-254">이후의 자습서에서는 데이터 모델이 변경, 삭제 및 다시 만들기 없이 때 데이터베이스를 수정 하는 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-254">In later tutorials, you'll see how to modify the database when the data model changes, without deleting and re-creating it.</span></span>

## <a name="create-a-controller-and-views"></a><span data-ttu-id="c15e3-255">컨트롤러와 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="c15e3-255">Create a controller and views</span></span>

<span data-ttu-id="c15e3-256">다음으로, MVC 컨트롤러 및 EF 데이터를 저장 하 고 쿼리를 사용 하 여 뷰를 추가 하려면 Visual Studio의 스 캐 폴딩 엔진을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-256">Next, you'll use the scaffolding engine in Visual Studio to add an MVC controller and views that will use EF to query and save data.</span></span>

<span data-ttu-id="c15e3-257">자동 생성의 CRUD 작업 메서드와 뷰를 스 캐 폴딩 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-257">The automatic creation of CRUD action methods and views is known as scaffolding.</span></span> <span data-ttu-id="c15e3-258">스 캐 폴딩 스 캐 폴드 코드는 일반적으로 생성 된 코드를 수정 하지 마십시오 하는 반면 사용자 고유의 요구 사항에 맞게 수정할 수 있는 시작 지점을 점에서 코드 생성와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-258">Scaffolding differs from code generation in that the scaffolded code is a starting point that you can modify to suit your own requirements, whereas you typically don't modify generated code.</span></span> <span data-ttu-id="c15e3-259">생성 된 코드를 사용자 지정 해야 하는 경우 partial 클래스를 사용 하거나 항목이 변경 될 때 코드를 다시 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-259">When you need to customize generated code, you use partial classes or you regenerate the code when things change.</span></span>

* <span data-ttu-id="c15e3-260">마우스 오른쪽 단추로 클릭는 **컨트롤러** 폴더에 **솔루션 탐색기** 선택 **추가 > 스 캐 폴드 된 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-260">Right-click the **Controllers** folder in **Solution Explorer** and select **Add > New Scaffolded Item**.</span></span>

<span data-ttu-id="c15e3-261">**MVC 종속성 추가** 대화 상자가 나타나는 경우:</span><span class="sxs-lookup"><span data-stu-id="c15e3-261">If the **Add MVC Dependencies** dialog appears:</span></span>

* <span data-ttu-id="c15e3-262">[Visual Studio를 최신 버전으로 업데이트합니다](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c15e3-262">[Update Visual Studio to the latest version](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="c15e3-263">Visual Studio 15.5 이전 버전이 이 대화 상자를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-263">Visual Studio versions prior to 15.5 show this dialog.</span></span>
* <span data-ttu-id="c15e3-264">업데이트할 수 없는 경우 **추가**를 선택한 다음 컨트롤러 추가 단계를 다시 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-264">If you can't update, select **ADD**, and then follow the add controller steps again.</span></span>

* <span data-ttu-id="c15e3-265">에 **추가 스 캐 폴드** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="c15e3-265">In the **Add Scaffold** dialog box:</span></span>

  * <span data-ttu-id="c15e3-266">선택 **뷰, Entity Framework를 사용 하 여 포함 된 MVC 컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-266">Select **MVC controller with views, using Entity Framework**.</span></span>

  * <span data-ttu-id="c15e3-267">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-267">Click **Add**.</span></span>

* <span data-ttu-id="c15e3-268">에 **컨트롤러 추가** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="c15e3-268">In the **Add Controller** dialog box:</span></span>

  * <span data-ttu-id="c15e3-269">**모델 클래스** 선택 **학생**합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-269">In **Model class** select **Student**.</span></span>

  * <span data-ttu-id="c15e3-270">**데이터 컨텍스트 클래스가** 선택 **SchoolContext**합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-270">In **Data context class** select **SchoolContext**.</span></span>

  * <span data-ttu-id="c15e3-271">기본값을 적용 **StudentsController** 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-271">Accept the default **StudentsController** as the name.</span></span>

  * <span data-ttu-id="c15e3-272">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-272">Click **Add**.</span></span>

  ![스 캐 폴드 학생](intro/_static/scaffold-student.png)

  <span data-ttu-id="c15e3-274">클릭할 때 **추가**, Visual Studio 스 캐 폴딩 엔진 만듭니다는 *StudentsController.cs* 파일과 뷰 집합 (*.cshtml* 파일)는 컨트롤러와 작동 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-274">When you click **Add**, the Visual Studio scaffolding engine creates a *StudentsController.cs* file and a set of views (*.cshtml* files) that work with the controller.</span></span>

<span data-ttu-id="c15e3-275">(스 캐 폴딩 엔진 만들 수도 데이터베이스 컨텍스트를 수동으로 만들지 않는 경우 먼저이 자습서에 대 한 예전 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-275">(The scaffolding engine can also create the database context for you if you don't create it manually first as you did earlier for this tutorial.</span></span> <span data-ttu-id="c15e3-276">새 컨텍스트 클래스를 지정할 수는 **컨트롤러 추가** 상자 오른쪽에 있는 더하기 기호를 클릭 하 여 **데이터 컨텍스트 클래스가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-276">You can specify a new context class in the **Add Controller** box by clicking the plus sign to the right of **Data context class**.</span></span>  <span data-ttu-id="c15e3-277">그런 다음 visual Studio를 만듭니다 프로그램 `DbContext` 클래스 뿐만 아니라 컨트롤러와 뷰.)</span><span class="sxs-lookup"><span data-stu-id="c15e3-277">Visual Studio will then create your `DbContext` class as well as the controller and views.)</span></span>

<span data-ttu-id="c15e3-278">컨트롤러를 사용 한다고 보면는 `SchoolContext` 를 생성자 매개 변수로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-278">You'll notice that the controller takes a `SchoolContext` as a constructor parameter.</span></span>

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_Context&highlight=5,7,9)]

<span data-ttu-id="c15e3-279">인스턴스를 전달 하는 ASP.NET 종속성 주입 하므로 `SchoolContext` 컨트롤러에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-279">ASP.NET dependency injection will take care of passing an instance of `SchoolContext` into the controller.</span></span> <span data-ttu-id="c15e3-280">구성에서 *Startup.cs* 이전 파일.</span><span class="sxs-lookup"><span data-stu-id="c15e3-280">You configured that in the *Startup.cs* file earlier.</span></span>

<span data-ttu-id="c15e3-281">컨트롤러를 포함 한 `Index` 데이터베이스의 모든 학생을 표시 하는 작업 메서드.</span><span class="sxs-lookup"><span data-stu-id="c15e3-281">The controller contains an `Index` action method, which displays all students in the database.</span></span> <span data-ttu-id="c15e3-282">메서드 읽어 설정 학생 엔터티에서 학생의 목록을 가져오고는 `Students` 데이터베이스 컨텍스트 인스턴스의 속성:</span><span class="sxs-lookup"><span data-stu-id="c15e3-282">The method gets a list of students from the Students entity set by reading the `Students` property of the database context instance:</span></span>

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_ScaffoldedIndex&highlight=3)]

<span data-ttu-id="c15e3-283">이 자습서의 뒷부분에 나오는이 코드에서 비동기 프로그래밍 요소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-283">You'll learn about the asynchronous programming elements in this code later in the tutorial.</span></span>

<span data-ttu-id="c15e3-284">*Views/Students/Index.cshtml* 보기 테이블에이 목록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-284">The *Views/Students/Index.cshtml* view displays this list in a table:</span></span>

[!code-cshtml[](intro/samples/cu/Views/Students/Index1.cshtml)]

<span data-ttu-id="c15e3-285">CTRL + f5 키를 눌러 프로젝트를 실행 하거나 선택할 **디버그 > 디버깅 하지 않고 시작** 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-285">Press CTRL+F5 to run the project or choose **Debug > Start Without Debugging** from the menu.</span></span>

<span data-ttu-id="c15e3-286">테스트 데이터를 보려면 학생 탭을 클릭 하 고 `DbInitializer.Initialize` 삽입 메서드.</span><span class="sxs-lookup"><span data-stu-id="c15e3-286">Click the Students tab to see the test data that the `DbInitializer.Initialize` method inserted.</span></span> <span data-ttu-id="c15e3-287">브라우저 창이 되 면 표시 최소에 따라는 `Student` 탭 페이지의 맨 위에 링크의 링크를 보려면 오른쪽 맨 위에 탐색 아이콘을 클릭 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-287">Depending on how narrow your browser window is, you'll see the `Student` tab link at the top of the page or you'll have to click the navigation icon in the upper right corner to see the link.</span></span>

![좁은 Contoso 대학 홈 페이지](intro/_static/home-page-narrow.png)

![학생 인덱스 페이지](intro/_static/students-index.png)

## <a name="view-the-database"></a><span data-ttu-id="c15e3-290">데이터베이스 보기</span><span class="sxs-lookup"><span data-stu-id="c15e3-290">View the Database</span></span>

<span data-ttu-id="c15e3-291">응용 프로그램을 시작 했을 때의 `DbInitializer.Initialize` 메서드 호출 `EnsureCreated`합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-291">When you started the application, the `DbInitializer.Initialize` method calls `EnsureCreated`.</span></span> <span data-ttu-id="c15e3-292">EF 보여 준다는 사실을 알았습니다 데이터베이스가 없습니다. 했습니다 및 없으므로, 다음의 나머지 부분에서는 생성 된 `Initialize` 메서드 코드는 데이터베이스 데이터로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-292">EF saw that there was no database and so it created one, then the remainder of the `Initialize` method code populated the database with data.</span></span> <span data-ttu-id="c15e3-293">사용할 수 있습니다 **SQL Server 개체 탐색기** (SSOX) Visual Studio에서 데이터베이스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-293">You can use **SQL Server Object Explorer** (SSOX) to view the database in Visual Studio.</span></span>

<span data-ttu-id="c15e3-294">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-294">Close the browser.</span></span>

<span data-ttu-id="c15e3-295">SSOX 창이 열려 있지 않은 경우 선택에서 **보기** Visual Studio에서 메뉴.</span><span class="sxs-lookup"><span data-stu-id="c15e3-295">If the SSOX window isn't already open, select it from the **View** menu in Visual Studio.</span></span>

<span data-ttu-id="c15e3-296">SSOX, 클릭 **(localdb) \MSSQLLocalDB > 데이터베이스**, 다음의 연결 문자열에 있는 데이터베이스 이름에 대 한 항목을 클릭 하 고 프로그램 *appsettings.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-296">In SSOX, click **(localdb)\MSSQLLocalDB > Databases**, and then click the entry for the database name that's in the connection string in your *appsettings.json* file.</span></span>

<span data-ttu-id="c15e3-297">확장은 **테이블** 노드에서 데이터베이스의 테이블을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-297">Expand the **Tables** node to see the tables in your database.</span></span>

![SSOX의 테이블](intro/_static/ssox-tables.png)

<span data-ttu-id="c15e3-299">마우스 오른쪽 단추로 클릭는 **학생** 테이블 마우스 클릭 **데이터 보기** 생성 된 열과 테이블에 삽입 된 행을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-299">Right-click the **Student** table and click **View Data** to see the columns that were created and the rows that were inserted into the table.</span></span>

![학생 표에 SSOX](intro/_static/ssox-student-table.png)

<span data-ttu-id="c15e3-301">*.mdf* 및 *.ldf* 데이터베이스 파일은는 *C:\Users\<yourusername >* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-301">The *.mdf* and *.ldf* database files are in the *C:\Users\<yourusername>* folder.</span></span>

<span data-ttu-id="c15e3-302">호출 하는 것 때문에 `EnsureCreated` 이니셜라이저 메서드의 백그라운드에서 작업에서 실행 하면 이제 만들 수에 대 한 변경의 `Student` 클래스, 데이터베이스를 삭제 하 고, 응용 프로그램을 다시 실행 하 고 데이터베이스는 자동으로 변경 내용을 맞게 다시 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-302">Because you're calling `EnsureCreated` in the initializer method that runs on app start, you could now make a change to the `Student` class, delete the database, run the application again, and the database would automatically be re-created to match your change.</span></span> <span data-ttu-id="c15e3-303">예를 들어, 추가 하는 경우는 `EmailAddress` 속성을는 `Student` 클래스 표시 새 `EmailAddress` 다시 만든된 테이블의 열입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-303">For example, if you add an `EmailAddress` property to the `Student` class, you'll see a new `EmailAddress` column in the re-created table.</span></span>

## <a name="conventions"></a><span data-ttu-id="c15e3-304">규칙</span><span class="sxs-lookup"><span data-stu-id="c15e3-304">Conventions</span></span>

<span data-ttu-id="c15e3-305">규칙 또는 Entity Framework에서는 가정을 사용 되기 때문에 전체 데이터베이스를 만들 수도 수 있게 되기를 Entity Framework에 대 한 순서 대로 작성 해야 했습니다 코드의 양을 최소화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-305">The amount of code you had to write in order for the Entity Framework to be able to create a complete database for you is minimal because of the use of conventions, or assumptions that the Entity Framework makes.</span></span>

* <span data-ttu-id="c15e3-306">이름을 `DbSet` 속성 테이블 이름으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-306">The names of `DbSet` properties are used as table names.</span></span> <span data-ttu-id="c15e3-307">엔터티에 의해 참조 되지 않는 한 `DbSet` 속성, 엔터티 클래스 이름이 테이블 이름으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-307">For entities not referenced by a `DbSet` property, entity class names are used as table names.</span></span>

* <span data-ttu-id="c15e3-308">엔터티 속성 이름은 열 이름에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-308">Entity property names are used for column names.</span></span>

* <span data-ttu-id="c15e3-309">ID 또는 classnameID 명명 된 엔터티 속성은 기본 키 속성으로 인식 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-309">Entity properties that are named ID or classnameID are recognized as primary key properties.</span></span>

* <span data-ttu-id="c15e3-310">라고 하는 경우 외래 키 속성으로는 속성을 해석 * <navigation property name> <primary key property name> * (예를 들어 `StudentID` 에 대 한는 `Student` 이후 탐색 속성은 `Student` 엔터티의 기본 키가 `ID`).</span><span class="sxs-lookup"><span data-stu-id="c15e3-310">A property is interpreted as a foreign key property if it's named *<navigation property name><primary key property name>* (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="c15e3-311">외래 키 속성은 단순히 또한 이름은 수 * <primary key property name> * (예를 들어 `EnrollmentID` 이후는 `Enrollment` 엔터티의 기본 키가 `EnrollmentID`).</span><span class="sxs-lookup"><span data-stu-id="c15e3-311">Foreign key properties can also be named simply *<primary key property name>* (for example, `EnrollmentID` since the `Enrollment` entity's primary key is `EnrollmentID`).</span></span>

<span data-ttu-id="c15e3-312">기본 동작을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-312">Conventional behavior can be overridden.</span></span> <span data-ttu-id="c15e3-313">예를 들어이 자습서의 앞부분에서 본 것 처럼 테이블 이름에 지정할 수 명시적으로.</span><span class="sxs-lookup"><span data-stu-id="c15e3-313">For example, you can explicitly specify table names, as you saw earlier in this tutorial.</span></span> <span data-ttu-id="c15e3-314">열 이름을 설정할 수 있으며에서 볼 수 있듯이 기본 키 또는 외래 키 속성을 설정 하 고는 [이후의 자습서](complex-data-model.md) 이 시리즈의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-314">And you can set column names and set any property as primary key or foreign key, as you'll see in a [later tutorial](complex-data-model.md) in this series.</span></span>

## <a name="asynchronous-code"></a><span data-ttu-id="c15e3-315">비동기 코드</span><span class="sxs-lookup"><span data-stu-id="c15e3-315">Asynchronous code</span></span>

<span data-ttu-id="c15e3-316">비동기 프로그래밍은 ASP.NET 코어 및 EF 코어에 대 한 기본 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-316">Asynchronous programming is the default mode for ASP.NET Core and EF Core.</span></span>

<span data-ttu-id="c15e3-317">웹 서버를 사용할 수 있는 스레드 수가 제한에 및 로드 양이 많으면 상황에서 모든 사용 가능한 스레드 수 사용.</span><span class="sxs-lookup"><span data-stu-id="c15e3-317">A web server has a limited number of threads available, and in high load situations all of the available threads might be in use.</span></span> <span data-ttu-id="c15e3-318">이 경우 서버를 스레드가 해제 될 때까지 새 요청을 처리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-318">When that happens, the server can't process new requests until the threads are freed up.</span></span> <span data-ttu-id="c15e3-319">I/O가 완료를 대기 하 고 있으므로 작업을 실제로 수행 되지 않습니다은 동안 많은 스레드가 동기 코드와 함께 하느라 정체 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-319">With synchronous code, many threads may be tied up while they aren't actually doing any work because they're waiting for I/O to complete.</span></span> <span data-ttu-id="c15e3-320">비동기 코드로 i/o가 완료를 대기 하는 프로세스 스레드에서 다른 요청을 처리에 사용할 서버에 대해 해제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-320">With asynchronous code, when a process is waiting for I/O to complete, its thread is freed up for the server to use for processing other requests.</span></span> <span data-ttu-id="c15e3-321">따라서 비동기 코드 서버 리소스를 보다 효율적으로 사용할 수 있으며 특정가 지연 없이 더 많은 트래픽을 처리 하도록 서버를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-321">As a result, asynchronous code enables server resources to be used more efficiently, and the server is enabled to handle more traffic without delays.</span></span>

<span data-ttu-id="c15e3-322">비동기 코드는 런타임 시 약간의 오버 헤드를 도입 하지만 성능에 미치는 영향은 매우 적습니다, 하는 동안 트래픽이 많은 상황에 대 한 트래픽이 적은 상황에 맞는 잠재적 성능 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-322">Asynchronous code does introduce a small amount of overhead at run time, but for low traffic situations the performance hit is negligible, while for high traffic situations, the potential performance improvement is substantial.</span></span>

<span data-ttu-id="c15e3-323">다음 코드에서는 `async` 키워드를 `Task<T>` 값을 반환 `await` 키워드 및 `ToListAsync` 메서드를 비동기적으로 실행 하는 코드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-323">In the following code, the `async` keyword, `Task<T>` return value, `await` keyword, and `ToListAsync` method make the code execute asynchronously.</span></span>

[!code-csharp[Main](intro/samples/cu/Controllers/StudentsController.cs?name=snippet_ScaffoldedIndex)]

* <span data-ttu-id="c15e3-324">`async` 키워드가 있으면 컴파일러 메서드 본문의 부분에 대 한 콜백을 생성 하 고 자동으로 만들 수는 `Task<IActionResult>` 반환 되는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-324">The `async` keyword tells the compiler to generate callbacks for parts of the method body and to automatically create the `Task<IActionResult>` object that's returned.</span></span>

* <span data-ttu-id="c15e3-325">반환 형식은 `Task<IActionResult>` 형식의 결과 함께 진행 중인 작업을 나타내는 `IActionResult`합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-325">The return type `Task<IActionResult>` represents ongoing work with a result of type `IActionResult`.</span></span>

* <span data-ttu-id="c15e3-326">`await` 키워드는 컴파일러에 메서드가 두 부분으로 분할 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-326">The `await` keyword causes the compiler to split the method into two parts.</span></span> <span data-ttu-id="c15e3-327">첫 번째 부분은 비동기적으로 시작 된 작업을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-327">The first part ends with the operation that's started asynchronously.</span></span> <span data-ttu-id="c15e3-328">두 번째 부분은 작업이 완료 될 때 호출 되는 콜백 메서드에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-328">The second part is put into a callback method that's called when the operation completes.</span></span>

* <span data-ttu-id="c15e3-329">`ToListAsync`비동기 버전의 `ToList` 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="c15e3-329">`ToListAsync` is the asynchronous version of the `ToList` extension method.</span></span>

<span data-ttu-id="c15e3-330">Entity Framework를 사용 하는 비동기 코드를 작성할 때 알아두어야 할 일부의 원인:</span><span class="sxs-lookup"><span data-stu-id="c15e3-330">Some things to be aware of when you are writing asynchronous code that uses the Entity Framework:</span></span>

* <span data-ttu-id="c15e3-331">쿼리 또는 데이터베이스에 보낼 명령을 발생 하는 명령문만 비동기적으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-331">Only statements that cause queries or commands to be sent to the database are executed asynchronously.</span></span> <span data-ttu-id="c15e3-332">예를 들어 포함 된 `ToListAsync`, `SingleOrDefaultAsync`, 및 `SaveChangesAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-332">That includes, for example, `ToListAsync`, `SingleOrDefaultAsync`, and `SaveChangesAsync`.</span></span> <span data-ttu-id="c15e3-333">포함 되지 않습니다, 예를 들어 변경 하는 문에 `IQueryable`와 같은 `var students = context.Students.Where(s => s.LastName == "Davolio")`합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-333">It doesn't include, for example, statements that just change an `IQueryable`, such as `var students = context.Students.Where(s => s.LastName == "Davolio")`.</span></span>

* <span data-ttu-id="c15e3-334">EF 컨텍스트 스레드로부터 안전 하지: 동시에 여러 작업을 수행 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c15e3-334">An EF context isn't thread safe: don't try to do multiple operations in parallel.</span></span> <span data-ttu-id="c15e3-335">비동기 EF 메서드를 호출 하는 경우 항상 사용는 `await` 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-335">When you call any async EF method, always use the `await` keyword.</span></span>

* <span data-ttu-id="c15e3-336">페이징 등 사용 중인 비동기 코드의 성능 이점을 활용, 라이브러리는 패키지에 있는지 확인 하려는 경우, 또한 비동기 때문에 쿼리가 데이터베이스에 전송 하는 Entity Framework 메서드를 호출 하는 경우 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-336">If you want to take advantage of the performance benefits of async code, make sure that any library packages that you're using (such as for paging), also use async if they call any Entity Framework methods that cause queries to be sent to the database.</span></span>

<span data-ttu-id="c15e3-337">.NET의 비동기 프로그래밍에 대 한 자세한 내용은 참조 [비동기 개요](https://docs.microsoft.com/dotnet/articles/standard/async)합니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-337">For more information about asynchronous programming in .NET, see [Async Overview](https://docs.microsoft.com/dotnet/articles/standard/async).</span></span>

## <a name="summary"></a><span data-ttu-id="c15e3-338">요약</span><span class="sxs-lookup"><span data-stu-id="c15e3-338">Summary</span></span>

<span data-ttu-id="c15e3-339">이제 Entity Framework Core 및 SQL Server Express LocalDB를 사용 하 여 저장 하 고 데이터를 표시 하는 간단한 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-339">You've now created a simple application that uses the Entity Framework Core and SQL Server Express LocalDB to store and display data.</span></span> <span data-ttu-id="c15e3-340">다음 자습서에서는 기본 CRUD 수행 하는 방법을 배우게 됩니다 (만들기, 읽기, 업데이트, 삭제) 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="c15e3-340">In the following tutorial, you'll learn how to perform basic CRUD (create, read, update, delete) operations.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="c15e3-341">다음</span><span class="sxs-lookup"><span data-stu-id="c15e3-341">Next</span></span>](crud.md)
