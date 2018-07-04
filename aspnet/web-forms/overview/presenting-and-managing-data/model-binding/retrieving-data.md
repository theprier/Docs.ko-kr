---
uid: web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
title: 검색 하 고 사용 하 여 데이터 모델 바인딩 및 web forms | Microsoft Docs
author: tfitzmac
description: 이 자습서 시리즈에서는 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩을 통해 데이터 상호 작용 자세한 직선-...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/27/2014
ms.topic: article
ms.assetid: 9f24fb82-c7ac-48da-b8e2-51b3da17e365
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
msc.type: authoredcontent
ms.openlocfilehash: 4a76fcfd2620eb0789b7a6a23990037a1eebaf4c
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37378497"
---
<a name="retrieving-and-displaying-data-with-model-binding-and-web-forms"></a><span data-ttu-id="e03aa-104">모델 바인딩 및 web forms를 사용 하 여 데이터 검색 및 표시</span><span class="sxs-lookup"><span data-stu-id="e03aa-104">Retrieving and displaying data with model binding and web forms</span></span>
====================
<span data-ttu-id="e03aa-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="e03aa-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="e03aa-106">이 자습서 시리즈에서는 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="e03aa-107">모델 바인딩 보다 직관적인 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource) 처리 하는 보다 데이터 상호 작용 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="e03aa-108">이 시리즈 소개 자료를 사용 하 여 시작 하 고 나중에 자습서에서 고급 개념을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="e03aa-109">모델 바인딩 패턴은 모든 데이터 액세스 기술을 사용 하 여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-109">The model binding pattern works with any data access technology.</span></span> <span data-ttu-id="e03aa-110">이 자습서에서는 Entity Framework를 사용 하는 하지만 가장 익숙한 데이터 액세스 기술을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-110">In this tutorial, you will use Entity Framework, but you could use the data access technology that is most familiar to you.</span></span> <span data-ttu-id="e03aa-111">GridView, ListView, DetailsView 또는 FormView 컨트롤과 같은 데이터 바인딩된 서버 컨트롤에서 선택, 업데이트, 삭제 및 데이터 만들기에 대 한 사용 하는 방법의 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-111">From a data-bound server control, such as a GridView, ListView, DetailsView, or FormView control, you specify the names of the methods to use for selecting, updating, deleting, and creating data.</span></span> <span data-ttu-id="e03aa-112">이 자습서에서는 SelectMethod에 대 한 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-112">In this tutorial, you will specify a value for the SelectMethod.</span></span>
> 
> <span data-ttu-id="e03aa-113">이 메서드 내에서 데이터를 검색 하기 위한 논리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-113">Within that method, you provide the logic for retrieving the data.</span></span> <span data-ttu-id="e03aa-114">다음 자습서에서는 DeleteMethod UpdateMethod, InsertMethod 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-114">In the next tutorial, you will set values for UpdateMethod, DeleteMethod and InsertMethod.</span></span>
> 
> <span data-ttu-id="e03aa-115">할 수 있습니다 [다운로드](https://go.microsoft.com/fwlink/?LinkId=286116) C# 또는 VB. 전체 프로젝트</span><span class="sxs-lookup"><span data-stu-id="e03aa-115">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="e03aa-116">다운로드 가능한 코드를 Visual Studio 2012 또는 Visual Studio 2013을 사용 하 여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-116">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="e03aa-117">이 자습서에 표시 된 Visual Studio 2013 서식 파일 보다 약간 다른 Visual Studio 2012 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-117">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>
> 
> <span data-ttu-id="e03aa-118">이 자습서에서 Visual Studio에서 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-118">In the tutorial you run the application in Visual Studio.</span></span> <span data-ttu-id="e03aa-119">또한 가능 응용 프로그램 사용 가능한 인터넷을 통해 호스팅 공급자에 배포 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-119">You can also make the application available over the Internet by deploying it to a hosting provider.</span></span> <span data-ttu-id="e03aa-120">Microsoft에서 제공 하는 무료 웹 호스팅에 최대 10 개의 웹 사이트를</span><span class="sxs-lookup"><span data-stu-id="e03aa-120">Microsoft offers free web hosting for up to 10 web sites in a</span></span>  
>  <span data-ttu-id="e03aa-121">[무료 Azure 평가판 계정](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-121">[free Azure trial account](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="e03aa-122">Visual Studio 웹 프로젝트를 Azure App Service Web Apps를 배포 하는 방법에 대 한 내용은 참조는 [Visual Studio를 사용 하 여 ASP.NET 웹 배포](../../deployment/visual-studio-web-deployment/introduction.md) 시리즈입니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-122">For information about how to deploy a Visual Studio web project to Azure App Service Web Apps, see the [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md) series.</span></span> <span data-ttu-id="e03aa-123">이 자습서에는 Azure SQL Database로 SQL Server 데이터베이스를 배포 하려면 Entity Framework Code First 마이그레이션을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-123">That tutorial also shows how to use Entity Framework Code First Migrations to deploy your SQL Server database to Azure SQL Database.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e03aa-124">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="e03aa-124">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="e03aa-125">Microsoft Visual Studio 2013 또는 Microsoft Visual Studio Express 2013 for Web</span><span class="sxs-lookup"><span data-stu-id="e03aa-125">Microsoft Visual Studio 2013 or Microsoft Visual Studio Express 2013 for Web</span></span>
>   
> 
> <span data-ttu-id="e03aa-126">이 자습서는 Visual Studio 2012 에서도 작동 하지만 사용자 인터페이스 및 프로젝트 템플릿에서 몇 가지 차이점이 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-126">This tutorial also works with Visual Studio 2012 but there will be some differences in the user interface and project template.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="e03aa-127">만들 내용</span><span class="sxs-lookup"><span data-stu-id="e03aa-127">What you'll build</span></span>

<span data-ttu-id="e03aa-128">이 자습서에서는 다음을 수행 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-128">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="e03aa-129">대학의 학생 과정에 등록을 사용 하 여 반영 하는 데이터 개체 작성</span><span class="sxs-lookup"><span data-stu-id="e03aa-129">Build data objects that reflect a university with students enrolled in courses</span></span>
2. <span data-ttu-id="e03aa-130">빌드 개체에서 데이터베이스 테이블</span><span class="sxs-lookup"><span data-stu-id="e03aa-130">Build database tables from the objects</span></span>
3. <span data-ttu-id="e03aa-131">테스트 데이터로 데이터베이스를 채우는</span><span class="sxs-lookup"><span data-stu-id="e03aa-131">Populate the database with test data</span></span>
4. <span data-ttu-id="e03aa-132">웹 폼에서 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-132">Display data in a web form</span></span>

## <a name="set-up-project"></a><span data-ttu-id="e03aa-133">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="e03aa-133">Set up project</span></span>

<span data-ttu-id="e03aa-134">Visual Studio 2013에서 새로 만듭니다 **ASP.NET 웹 응용 프로그램** 호출 **ContosoUniversityModelBinding**합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-134">In Visual Studio 2013, create a new **ASP.NET Web Application** called **ContosoUniversityModelBinding**.</span></span>

![프로젝트 만들기](retrieving-data/_static/image2.png)

<span data-ttu-id="e03aa-136">Web Forms 템플릿을 선택 하 고 다른 기본 옵션은 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-136">Select the Web Forms template, and leave the other default options.</span></span> <span data-ttu-id="e03aa-137">프로젝트를 설정 하는 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-137">Click OK to setup the project.</span></span>

![web forms를 선택 합니다.](retrieving-data/_static/image3.png)

<span data-ttu-id="e03aa-139">먼저 몇 가지 사이트의 모양을 사용자 지정 하려면 약간 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-139">First, you will make a couple of small changes to customize the appearance of the site.</span></span> <span data-ttu-id="e03aa-140">엽니다는 **Site.Master** 파일 및 제목을 포함 내 ASP.NET 응용 프로그램 대신 Contoso University로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-140">Open the **Site.Master** file, and change the title to include Contoso University instead of My ASP.NET Application.</span></span>

[!code-aspx[Main](retrieving-data/samples/sample1.aspx?highlight=1)]

<span data-ttu-id="e03aa-141">그런 다음의 헤더 텍스트를 변경 **응용 프로그램 이름** 하 **Contoso University**합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-141">Then, change the header text from **Application name** to **Contoso University**.</span></span>

[!code-aspx[Main](retrieving-data/samples/sample2.aspx?highlight=7)]

<span data-ttu-id="e03aa-142">또한 Site.Master에서이 사이트에 관련 된 페이지에 맞게 머리글에 표시 되는 탐색 링크를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-142">Also in Site.Master, change the navigation links that appear in the header to reflect the pages that are relevant to this site.</span></span> <span data-ttu-id="e03aa-143">필요 하지 것입니다 합니다 **에 대 한** 페이지 또는 **연락처** 페이지 되었으므로 해당 링크를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-143">You will not need either the **About** page or the **Contact** page so those links can be removed.</span></span> <span data-ttu-id="e03aa-144">대신 라는 페이지에 대 한 링크를 해야 **학생**합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-144">Instead, you will need a link to a page called **Students**.</span></span> <span data-ttu-id="e03aa-145">이 페이지는 아직 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-145">This page has not been created yet.</span></span>

[!code-aspx[Main](retrieving-data/samples/sample3.aspx)]

<span data-ttu-id="e03aa-146">저장 하 고 Site.Master를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-146">Save and close Site.Master.</span></span>

<span data-ttu-id="e03aa-147">이제 학생 데이터를 표시 하기 위한 web form을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-147">Now, you'll create the web form for displaying student data.</span></span> <span data-ttu-id="e03aa-148">프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** 는 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-148">Right-click your project, and **Add** a **New Item**.</span></span> <span data-ttu-id="e03aa-149">선택 합니다 **마스터 페이지를 사용 하 여 Web Form** 템플릿을 하 고 이름을 **Students.aspx**합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-149">Select the **Web Form with Master Page** template, and name it **Students.aspx**.</span></span>

![페이지 만들기](retrieving-data/_static/image5.png)

<span data-ttu-id="e03aa-151">선택 **Site.Master** 새 web form에 대 한 마스터 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-151">Select **Site.Master** as the master page for the new web form.</span></span>

## <a name="create-the-data-models-and-database"></a><span data-ttu-id="e03aa-152">데이터 모델 및 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="e03aa-152">Create the data models and database</span></span>

<span data-ttu-id="e03aa-153">Code First 마이그레이션을 사용 하 여 개체 및 해당 데이터베이스 테이블을 만들려면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-153">You will use Code First Migrations to create objects and the corresponding database tables.</span></span> <span data-ttu-id="e03aa-154">이러한 테이블 학생 및 해당 과정에 대 한 정보를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-154">These tables will store information about the students and their courses.</span></span>

<span data-ttu-id="e03aa-155">Models 폴더에서 라는 새 클래스 추가 **UniversityModels.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-155">In the Models folder, add a new class named **UniversityModels.cs**.</span></span>

![모델 클래스 만들기](retrieving-data/_static/image7.png)

<span data-ttu-id="e03aa-157">이 파일에서 SchoolContext, 학생, 등록 및 과정 클래스를 다음과 같이 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-157">In this file, define the SchoolContext, Student, Enrollment, and Course classes as follows:</span></span>

[!code-csharp[Main](retrieving-data/samples/sample4.cs)]

<span data-ttu-id="e03aa-158">SchoolContext 클래스는 데이터베이스 연결 및 데이터의 변경 내용을 관리 하는 DbContext에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-158">The SchoolContext class derives from DbContext, which manages the database connection and changes in the data.</span></span>

<span data-ttu-id="e03aa-159">Student 클래스에서 특성에 적용 된을 확인 합니다 **FirstName**, **LastName**, 및 **연도** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-159">In the Student class, notice the attributes that have been applied to the **FirstName**, **LastName**, and **Year** properties.</span></span> <span data-ttu-id="e03aa-160">이러한 특성은이 자습서에서는 데이터 유효성 검사에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-160">These attributes will be used for data validation in this tutorial.</span></span> <span data-ttu-id="e03aa-161">이 데모 프로젝트에 대 한 코드를 단순화 하기 위해 이러한 속성만 데이터 유효성 검사 특성을 사용 하 여로 표시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-161">To simplify the code for this demonstration project, only these properties were marked with data-validation attributes.</span></span> <span data-ttu-id="e03aa-162">실제 프로젝트에서는 등록 및 강좌 클래스의 속성 등의 유효성이 검사 된 데이터를 필요로 하는 모든 속성에 유효성 검사 특성을 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-162">In a real project, you would apply validation attributes to all properties that need validated data, such as properties in the Enrollment and Course classes.</span></span>

<span data-ttu-id="e03aa-163">UniversityModels.cs를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-163">Save UniversityModels.cs.</span></span>

<span data-ttu-id="e03aa-164">이러한 클래스를 기반으로 데이터베이스를 설정 하려면 Code First 마이그레이션에 대 한 도구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-164">You will use the tools for Code First Migrations to set up a database based on these classes.</span></span>

<span data-ttu-id="e03aa-165">**패키지 관리자 콘솔**, 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-165">In **Package Manager Console**, run the command:</span></span>  
`enable-migrations -ContextTypeName ContosoUniversityModelBinding.Models.SchoolContext`

<span data-ttu-id="e03aa-166">마이그레이션을 사용 된 메시지가 받게 명령이 성공적으로 완료 된 경우</span><span class="sxs-lookup"><span data-stu-id="e03aa-166">If the command completes successfully you will receive a message stating migrations have been enabled,</span></span>

![마이그레이션을 사용 하도록 설정](retrieving-data/_static/image8.png)

<span data-ttu-id="e03aa-168">새 파일의 이름이 되었다는 **Configuration.cs** 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-168">Notice that a new file named **Configuration.cs** has been created.</span></span> <span data-ttu-id="e03aa-169">이 파일이 Visual Studio에서 생성 된 후 자동으로 열려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-169">In Visual Studio, this file is automatically opened after it is created.</span></span> <span data-ttu-id="e03aa-170">구성 클래스를 포함 한 **초기값** 메서드 테스트 데이터로 데이터베이스 테이블을 미리 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-170">The Configuration class contains a **Seed** method which enables you to pre-populate the database tables with test data.</span></span>

<span data-ttu-id="e03aa-171">Seed 메서드를 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-171">Add the following code to the Seed method.</span></span> <span data-ttu-id="e03aa-172">추가 해야는 **를 사용 하 여** 문을 합니다 **ContosoUniversityModelBinding.Models** 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-172">You'll need to add a **using** statement for the **ContosoUniversityModelBinding.Models** namespace.</span></span>

[!code-csharp[Main](retrieving-data/samples/sample5.cs)]

<span data-ttu-id="e03aa-173">Configuration.cs를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-173">Save Configuration.cs.</span></span>

<span data-ttu-id="e03aa-174">패키지 관리자 콘솔에서 명령을 실행 `add-migration initial`합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-174">In the Package Manager Console, run the command `add-migration initial`.</span></span>

<span data-ttu-id="e03aa-175">그런 다음 명령을 실행 `update-database`합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-175">Then, run the command `update-database`.</span></span>

<span data-ttu-id="e03aa-176">이 명령을 실행 하는 경우 예외를 수신 하면 경우 CourseID 및 StudentID 값에는 시드 메서드 값에서 다양 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-176">If you receive an exception when running this command, it is possible that the values for StudentID and CourseID have varied from the values in the Seed method.</span></span> <span data-ttu-id="e03aa-177">데이터베이스에서 해당 테이블을 열고 CourseID 및 StudentID에 대 한 기존 값을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-177">Open those tables in the database and find existing values for StudentID and CourseID.</span></span> <span data-ttu-id="e03aa-178">등록은 시드를 위해 코드에서 이러한 값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-178">Add those values in the code for seeding the Enrollments table.</span></span>

<span data-ttu-id="e03aa-179">데이터베이스 파일에 추가한 있지만 프로젝트에 숨겨져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-179">The database file has been added, but it is currently hidden in the project.</span></span> <span data-ttu-id="e03aa-180">클릭 **모든 파일 표시** 파일을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-180">Click **Show All Files** to display the file.</span></span>

![모든 파일 표시](retrieving-data/_static/image10.png)

<span data-ttu-id="e03aa-182">.Mdf 파일을 앱에서 이제 나타납니다\_데이터 폴더.</span><span class="sxs-lookup"><span data-stu-id="e03aa-182">Notice the .mdf file now appears in the App\_Data folder.</span></span>

![데이터베이스 파일](retrieving-data/_static/image12.png)

<span data-ttu-id="e03aa-184">.Mdf 파일을 두 번 클릭 하 고 서버 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-184">Double-click the .mdf file and open the Server Explorer.</span></span> <span data-ttu-id="e03aa-185">이제 테이블 존재 하 고 데이터로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-185">The tables now exist and are populated with data.</span></span>

![데이터베이스 테이블](retrieving-data/_static/image14.png)

## <a name="display-data-from-students-and-related-tables"></a><span data-ttu-id="e03aa-187">학생 및 관련된 테이블에서 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-187">Display data from Students and related tables</span></span>

<span data-ttu-id="e03aa-188">데이터베이스의 데이터로 준비가 이제 해당 데이터를 검색 하 고 웹 페이지에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-188">With data in the database, you are now ready to retrieve that data and display it in a web page.</span></span> <span data-ttu-id="e03aa-189">사용 하 여는 **GridView** 열과 행에 있는 데이터를 표시 하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-189">You will use a **GridView** control to display the data in columns and rows.</span></span>

<span data-ttu-id="e03aa-190">Students.aspx를 열고 찾습니다 합니다 **MainContent** 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-190">Open Students.aspx, and locate the **MainContent** placeholder.</span></span> <span data-ttu-id="e03aa-191">자리 표시자를 추가 된 **GridView** 다음 코드를 포함 하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-191">Within that placeholder, add a **GridView** control that includes the following code.</span></span>

[!code-aspx[Main](retrieving-data/samples/sample6.aspx)]

<span data-ttu-id="e03aa-192">이 태그 코드를 감지 하는 데에 중요 한 개념 중 몇 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-192">There are a couple of important concepts in this markup code for you to notice.</span></span> <span data-ttu-id="e03aa-193">먼저, 값에 대 한 설정 되어 있는지를 확인 합니다 **SelectMethod** GridView 요소의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-193">First, notice that a value is set for the **SelectMethod** property in the GridView element.</span></span> <span data-ttu-id="e03aa-194">이 값에는 GridView에 대 한 데이터를 검색에 사용 되는 메서드의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-194">This value specifies the name of the method that is used for retrieving data for the GridView.</span></span> <span data-ttu-id="e03aa-195">이 메서드는 다음 단계에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-195">You will create this method in the next step.</span></span> <span data-ttu-id="e03aa-196">둘째, 있음을 합니다 **ItemType** 앞서 만든 Student 클래스 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-196">Second, notice that the **ItemType** property is set to the Student class that you created earlier.</span></span> <span data-ttu-id="e03aa-197">이 값으로 설정 된 태그 코드에서 해당 클래스의 속성을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-197">By setting this value, you can refer to properties of that class in the markup code.</span></span> <span data-ttu-id="e03aa-198">예를 들어 Student 클래스 등록 라는 컬렉션을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-198">For example, the Student class contains a collection named Enrollments.</span></span> <span data-ttu-id="e03aa-199">사용할 수 있습니다 **Item.Enrollments** 를 해당 컬렉션을 검색 하 여 다음 LINQ 구문을 사용 하 여 각 학생에 대 한 등록 된 크레딧의 합계를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-199">You can use **Item.Enrollments** to retrieve that collection and then use LINQ syntax to retrieve the sum of enrolled credits for each student.</span></span>

<span data-ttu-id="e03aa-200">코드 숨김 파일에 지정 된 메서드를 추가 해야 합니다 **SelectMethod** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-200">In the code-behind file, you need to add the method that is specified for the **SelectMethod** value.</span></span> <span data-ttu-id="e03aa-201">열기 **Students.aspx.cs**, 추가한 **사용 하 여** 문 합니다 **ContosoUniversityModelBinding.Models** 및 **System.Data.Entity**네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-201">Open **Students.aspx.cs**, and add **using** statements for the **ContosoUniversityModelBinding.Models** and **System.Data.Entity** namespaces.</span></span>

[!code-csharp[Main](retrieving-data/samples/sample7.cs)]

<span data-ttu-id="e03aa-202">다음 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-202">Then, add the following method.</span></span> <span data-ttu-id="e03aa-203">이 메서드의 이름을 SelectMethod에 대해 제공한 이름과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-203">Notice that the name of this method matches the name you provided for SelectMethod.</span></span>

[!code-csharp[Main](retrieving-data/samples/sample8.cs)]

<span data-ttu-id="e03aa-204">합니다 **Include** 절이 쿼리의 성능을 개선 하지 않으면이 작동 하려면 쿼리에 대 한 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-204">The **Include** clause improves the performance of this query but is not essential for the query to work.</span></span> <span data-ttu-id="e03aa-205">Include 절 없이 데이터베이스에 별도 쿼리가 각 시간 관련 데이터를 검색할를 보내야 하는 지연 로드를 사용 하 여 데이터를 검색할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-205">Without the Include clause, the data would be retrieved using lazy loading, which involves sending a separate query to the database each time related data is retrieved.</span></span> <span data-ttu-id="e03aa-206">Include 절에 제공 하 여 데이터를 데이터베이스의 단일 쿼리를 통해 검색은 모든 관련된 데이터 즉 즉시 로드를 사용 하 여 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-206">By providing the Include clause, the data is retrieved using eager loading, which means all of the related data is retrieved through a single query of the database.</span></span> <span data-ttu-id="e03aa-207">관련된 데이터의 대부분은 아닐 경우에 더 많은 데이터 검색 되기 때문에 사용 되는, 즉시 로드 덜 효율적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-207">In cases where most of the related data is not be used, eager loading can be less efficient because more data is retrieved.</span></span> <span data-ttu-id="e03aa-208">그러나이 경우 선행 로딩과 최상의 성능을 제공 각 레코드에 대 한 관련된 데이터 표시 되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-208">However, in this case, eager loading provides the best performance because the related data is displayed for each record.</span></span>

<span data-ttu-id="e03aa-209">로드 시 성능 고려 사항에 대 한 자세한 내용은 관련 데이터에 대 한 섹션을 참조 하세요 **지연, 즉시, 및 관련 데이터의 명시적 로드** 에 [는 ASP에서 Entity Framework를 사용 하 여 관련 데이터 읽기 .NET MVC 응용 프로그램](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-209">For more information about performance consideration when loading related data, see the section titled **Lazy, Eager, and Explicit Loading of Related Data** in the [Reading Related Data with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) topic.</span></span>

<span data-ttu-id="e03aa-210">기본적으로 데이터를 키로 표시 된 속성의 값을 기준으로 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-210">By default, the data is sorted by the values of the property marked as the key.</span></span> <span data-ttu-id="e03aa-211">정렬에 대 한 다른 값을 지정 하려면 OrderBy 절을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-211">You can add an OrderBy clause to specify a different value for sorting.</span></span> <span data-ttu-id="e03aa-212">이 예제에서는 기본 StudentID 속성은 정렬에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-212">In this example, the default StudentID property is used for sorting.</span></span> <span data-ttu-id="e03aa-213">에 [정렬, 페이징 및 필터링 데이터](sorting-paging-and-filtering-data.md) 항목 정렬에 대 한 열을 선택 하면 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-213">In the [Sorting, Paging, and Filtering Data](sorting-paging-and-filtering-data.md) topic, you will enable the user to select a column for sorting.</span></span>

<span data-ttu-id="e03aa-214">웹 응용 프로그램을 실행 하 고 학생 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-214">Run your web application, and navigate to the Students page.</span></span> <span data-ttu-id="e03aa-215">학생 페이지는 다음과 같은 학생 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-215">The Students page displays the following student information.</span></span>

![데이터를 표시 합니다.](retrieving-data/_static/image16.png)

## <a name="automatic-generation-of-model-binding-methods"></a><span data-ttu-id="e03aa-217">모델 바인딩 메서드를 자동으로 생성</span><span class="sxs-lookup"><span data-stu-id="e03aa-217">Automatic generation of model binding methods</span></span>

<span data-ttu-id="e03aa-218">이 자습서 시리즈를 진행할 때 프로젝트에 자습서에서 코드를 단순히 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-218">When working through this tutorial series, you can simply copy the code from the tutorial to your project.</span></span> <span data-ttu-id="e03aa-219">그러나 하나이 방식의 단점은 없게 되어 자동으로 코드를 생성할 모델 바인딩 메서드는 Visual Studio에서 제공 하는 기능을 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-219">However, one disadvantage of this approach is that you may not become aware of the feature provided by Visual Studio to automatically generate code for model binding methods.</span></span> <span data-ttu-id="e03aa-220">사용자 고유의 프로젝트를 사용할 때 자동 코드 생성 및 저장할 수 있습니다 시간 도움말 작업을 구현 하는 방법의 이해를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-220">When working on your own projects, automatic code generation can save you time and help you gain a sense of how to implement an operation.</span></span> <span data-ttu-id="e03aa-221">이 섹션에서는 자동 코드 생성 기능을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-221">This section describes the automatic code generation feature.</span></span> <span data-ttu-id="e03aa-222">이 섹션에서는 정보 제공 용 이므로 전용 이며 프로젝트에서 구현 해야 할 코드는 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-222">This section is only informational and does not contain any code you need to implement in your project.</span></span>

<span data-ttu-id="e03aa-223">에 대 한 값을 설정 하는 경우는 **SelectMethod**, **UpdateMethod**합니다 **InsertMethod**, 또는 **DeleteMethod** 태그 코드에서 속성 선택할 수 있습니다 합니다 **새 메서드 만들기** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-223">When setting a value for the **SelectMethod**, **UpdateMethod**, **InsertMethod**, or **DeleteMethod** properties in the markup code, you can select the **Create New Method** option.</span></span>

![새 메서드 만들기](retrieving-data/_static/image18.png)

<span data-ttu-id="e03aa-225">Visual Studio 적절 한 서명 사용 하 여 코드 숨김의 메서드를 만듭니다 뿐 아니라도 작업을 수행을 지원 하기 위한 구현 코드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-225">Visual Studio not only creates a method in the code-behind with the proper signature, but also generates implementation code to assist you with performing the operation.</span></span> <span data-ttu-id="e03aa-226">먼저 설정 하는 경우는 **ItemType** 작업에 대 한 자동 코드 생성 기능을 생성된 된 코드를 사용 하기 전에 속성에서는 유형을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-226">If you first set the **ItemType** property before using the automatic code generation feature, the generated code will use that type for the operations.</span></span> <span data-ttu-id="e03aa-227">예를 들어, UpdateMethod 속성을 설정할 때 다음 코드를 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-227">For example, when setting the UpdateMethod property, the following code is automatically generated:</span></span>

[!code-csharp[Main](retrieving-data/samples/sample9.cs)]

<span data-ttu-id="e03aa-228">다시 위의 코드 프로젝트에 추가할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-228">Again, the above code does not need to be added to your project.</span></span> <span data-ttu-id="e03aa-229">다음 자습서에서는 업데이트, 삭제 및 새 데이터를 추가 하기 위한 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-229">In the next tutorial, you will implement methods for updating, deleting and adding new data.</span></span>

## <a name="conclusion"></a><span data-ttu-id="e03aa-230">결론</span><span class="sxs-lookup"><span data-stu-id="e03aa-230">Conclusion</span></span>

<span data-ttu-id="e03aa-231">이 자습서에서는 데이터 모델 클래스를 생성 하 고 해당 클래스에서 데이터베이스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-231">In this tutorial, you created data model classes and generated a database from those classes.</span></span> <span data-ttu-id="e03aa-232">테스트 데이터를 사용 하 여 데이터베이스 테이블을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-232">You filled the database tables with test data.</span></span> <span data-ttu-id="e03aa-233">데이터베이스에서 데이터를 검색할 모델 바인딩을 사용 하 고 GridView에 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-233">You used model binding to retrieve data from the database, and then displayed the data in a GridView.</span></span>

<span data-ttu-id="e03aa-234">다음에 [자습서](updating-deleting-and-creating-data.md) 이 시리즈에서는 업데이트, 삭제 및 만드는 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e03aa-234">In the next [tutorial](updating-deleting-and-creating-data.md) in this series, you will enable updating, deleting, and creating data.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="e03aa-235">다음</span><span class="sxs-lookup"><span data-stu-id="e03aa-235">Next</span></span>](updating-deleting-and-creating-data.md)
