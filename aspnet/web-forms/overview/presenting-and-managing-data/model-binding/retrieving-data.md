---
uid: web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
title: 검색 및 사용 하 여 데이터를 표시 합니다. 모델 바인딩 및 web forms | Microsoft Docs
author: tfitzmac
description: 이 자습서 시리즈 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩 데이터 상호 작용 하 게 더 많은 직선-중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/27/2014
ms.topic: article
ms.assetid: 9f24fb82-c7ac-48da-b8e2-51b3da17e365
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
msc.type: authoredcontent
ms.openlocfilehash: 26873efa5dbfdbdab39a52cfb9cfd5a65c8231a3
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30889097"
---
<a name="retrieving-and-displaying-data-with-model-binding-and-web-forms"></a><span data-ttu-id="2600e-104">검색 및 모델 바인딩 및 web forms를 사용 하 여 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-104">Retrieving and displaying data with model binding and web forms</span></span>
====================
<span data-ttu-id="2600e-105">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="2600e-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="2600e-106">이 자습서 시리즈 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="2600e-107">모델 바인딩 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource) 처리 하는 보다 간단한 것 보다 데이터 상호 작용 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="2600e-108">이 시리즈 소개 자료로 시작 하 고 이후의 자습서의 보다 발전된 된 개념 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="2600e-109">모델 바인딩 패턴은 모든 데이터 액세스 기술을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-109">The model binding pattern works with any data access technology.</span></span> <span data-ttu-id="2600e-110">이 자습서에서는 Entity Framework를 사용 하 여 하 이지만 가장 익숙한 데이터 액세스 기술에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-110">In this tutorial, you will use Entity Framework, but you could use the data access technology that is most familiar to you.</span></span> <span data-ttu-id="2600e-111">GridView, ListView, DetailsView, 또는 FormView 제어와 같은 데이터 바인딩된 서버 컨트롤에서 선택, 업데이트, 삭제 및 데이터 만들기에 대 한 사용 하는 방법의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-111">From a data-bound server control, such as a GridView, ListView, DetailsView, or FormView control, you specify the names of the methods to use for selecting, updating, deleting, and creating data.</span></span> <span data-ttu-id="2600e-112">이 자습서에서는 SelectMethod에 대 한 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-112">In this tutorial, you will specify a value for the SelectMethod.</span></span>
> 
> <span data-ttu-id="2600e-113">이 메서드 내에서 데이터를 검색 하기 위한 논리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-113">Within that method, you provide the logic for retrieving the data.</span></span> <span data-ttu-id="2600e-114">다음 자습서에서는 InsertMethod, UpdateMethod 및 DeleteMethod 한 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-114">In the next tutorial, you will set values for UpdateMethod, DeleteMethod and InsertMethod.</span></span>
> 
> <span data-ttu-id="2600e-115">있습니다 수 [다운로드](https://go.microsoft.com/fwlink/?LinkId=286116) C# 또는 VB. 전체 프로젝트</span><span class="sxs-lookup"><span data-stu-id="2600e-115">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="2600e-116">다운로드 가능한 코드는 Visual Studio 2012 또는 Visual Studio 2013과 함께 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-116">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="2600e-117">이 자습서에 표시 된 Visual Studio 2013 서식 파일 보다 약간 차이가 있는 Visual Studio 2012 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-117">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>
> 
> <span data-ttu-id="2600e-118">자습서에서 Visual Studio에서 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-118">In the tutorial you run the application in Visual Studio.</span></span> <span data-ttu-id="2600e-119">또한 가능 응용 프로그램 사용 가능한 인터넷을 통해 호스팅 공급자에 게 배포 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-119">You can also make the application available over the Internet by deploying it to a hosting provider.</span></span> <span data-ttu-id="2600e-120">Microsoft에서 제공 하는 최대 10 개의 웹 사이트의 무료 웹 호스팅는</span><span class="sxs-lookup"><span data-stu-id="2600e-120">Microsoft offers free web hosting for up to 10 web sites in a</span></span>  
>  <span data-ttu-id="2600e-121">[무료 Azure 평가판 계정](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-121">[free Azure trial account](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="2600e-122">Azure 앱 서비스 웹 앱에 Visual Studio 웹 프로젝트를 배포 하는 방법에 대 한 정보를 참조 하십시오.는 [Visual Studio를 사용 하 여 ASP.NET 웹 배포](../../deployment/visual-studio-web-deployment/introduction.md) 계열입니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-122">For information about how to deploy a Visual Studio web project to Azure App Service Web Apps, see the [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md) series.</span></span> <span data-ttu-id="2600e-123">또한 해당 자습서는 Azure SQL 데이터베이스로 SQL Server 데이터베이스를 배포 하려면 Entity Framework Code First 마이그레이션을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-123">That tutorial also shows how to use Entity Framework Code First Migrations to deploy your SQL Server database to Azure SQL Database.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="2600e-124">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="2600e-124">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="2600e-125">Microsoft Visual Studio 2013 또는 Microsoft Visual Studio Express 2013 for Web</span><span class="sxs-lookup"><span data-stu-id="2600e-125">Microsoft Visual Studio 2013 or Microsoft Visual Studio Express 2013 for Web</span></span>
>   
> 
> <span data-ttu-id="2600e-126">이 자습서에서는 Visual Studio 2012 에서도 작동 하지만 사용자 인터페이스와 프로젝트 템플릿에 차이가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-126">This tutorial also works with Visual Studio 2012 but there will be some differences in the user interface and project template.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="2600e-127">만들 것인지</span><span class="sxs-lookup"><span data-stu-id="2600e-127">What you'll build</span></span>

<span data-ttu-id="2600e-128">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-128">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="2600e-129">과목에 등록 하는 학습자와 함께 대학을 반영 하는 데이터 개체를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-129">Build data objects that reflect a university with students enrolled in courses</span></span>
2. <span data-ttu-id="2600e-130">빌드 개체에서 데이터베이스 테이블</span><span class="sxs-lookup"><span data-stu-id="2600e-130">Build database tables from the objects</span></span>
3. <span data-ttu-id="2600e-131">데이터베이스 테스트 데이터를 채우려면</span><span class="sxs-lookup"><span data-stu-id="2600e-131">Populate the database with test data</span></span>
4. <span data-ttu-id="2600e-132">Web form에 데이터 표시</span><span class="sxs-lookup"><span data-stu-id="2600e-132">Display data in a web form</span></span>

## <a name="set-up-project"></a><span data-ttu-id="2600e-133">프로젝트 설정</span><span class="sxs-lookup"><span data-stu-id="2600e-133">Set up project</span></span>

<span data-ttu-id="2600e-134">Visual Studio 2013에서 만들 새 **ASP.NET 웹 응용 프로그램** 호출 **ContosoUniversityModelBinding**합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-134">In Visual Studio 2013, create a new **ASP.NET Web Application** called **ContosoUniversityModelBinding**.</span></span>

![프로젝트 만들기](retrieving-data/_static/image2.png)

<span data-ttu-id="2600e-136">Web Forms 서식 파일을 선택 하 고에서 기본 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-136">Select the Web Forms template, and leave the other default options.</span></span> <span data-ttu-id="2600e-137">프로젝트를 설정 하는 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-137">Click OK to setup the project.</span></span>

![web forms를 선택 합니다.](retrieving-data/_static/image3.png)

<span data-ttu-id="2600e-139">첫째, 몇 가지 사이트의 모양을 사용자 지정 하려면 약간 변경 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-139">First, you will make a couple of small changes to customize the appearance of the site.</span></span> <span data-ttu-id="2600e-140">열기는 **Site.Master** 파일을 찾아 내 ASP.NET 응용 프로그램 대신 Contoso 대학 포함 하도록 제목을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-140">Open the **Site.Master** file, and change the title to include Contoso University instead of My ASP.NET Application.</span></span>

[!code-aspx[Main](retrieving-data/samples/sample1.aspx?highlight=1)]

<span data-ttu-id="2600e-141">그런 다음에서 머리글 텍스트를 변경 **응용 프로그램 이름** 를 **Contoso 대학**합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-141">Then, change the header text from **Application name** to **Contoso University**.</span></span>

[!code-aspx[Main](retrieving-data/samples/sample2.aspx?highlight=7)]

<span data-ttu-id="2600e-142">또한 Site.Master에서이 사이트와 관련이 있는 페이지에 반영 하기 위해 머리글에 표시 되는 탐색 링크를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-142">Also in Site.Master, change the navigation links that appear in the header to reflect the pages that are relevant to this site.</span></span> <span data-ttu-id="2600e-143">필요 하지 것입니다는 **에 대 한** 페이지 또는 **연락처** 페이지 되었으므로 해당 링크를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-143">You will not need either the **About** page or the **Contact** page so those links can be removed.</span></span> <span data-ttu-id="2600e-144">대신, 해야 라는 페이지에 대 한 링크 **학생**합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-144">Instead, you will need a link to a page called **Students**.</span></span> <span data-ttu-id="2600e-145">이 페이지 아직 만들지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-145">This page has not been created yet.</span></span>

[!code-aspx[Main](retrieving-data/samples/sample3.aspx)]

<span data-ttu-id="2600e-146">저장 하 고 Site.Master를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-146">Save and close Site.Master.</span></span>

<span data-ttu-id="2600e-147">이제 학생 데이터를 표시 하기 위해 web form을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-147">Now, you'll create the web form for displaying student data.</span></span> <span data-ttu-id="2600e-148">프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** 는 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-148">Right-click your project, and **Add** a **New Item**.</span></span> <span data-ttu-id="2600e-149">선택 된 **마스터 페이지가 있는 웹 폼** 서식 파일을 하 고 이름을 **Students.aspx**합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-149">Select the **Web Form with Master Page** template, and name it **Students.aspx**.</span></span>

![페이지 만들기](retrieving-data/_static/image5.png)

<span data-ttu-id="2600e-151">선택 **Site.Master** 새 web form에 대 한 마스터 페이지로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-151">Select **Site.Master** as the master page for the new web form.</span></span>

## <a name="create-the-data-models-and-database"></a><span data-ttu-id="2600e-152">데이터 모델 및 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="2600e-152">Create the data models and database</span></span>

<span data-ttu-id="2600e-153">개체 및 해당 데이터베이스 테이블을 만드는 Code First 마이그레이션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-153">You will use Code First Migrations to create objects and the corresponding database tables.</span></span> <span data-ttu-id="2600e-154">이러한 테이블에 학생과 해당 과정에 대 한 정보를 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-154">These tables will store information about the students and their courses.</span></span>

<span data-ttu-id="2600e-155">모델 폴더에서 이라는 새 클래스 추가 **UniversityModels.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-155">In the Models folder, add a new class named **UniversityModels.cs**.</span></span>

![모델 클래스 만들기](retrieving-data/_static/image7.png)

<span data-ttu-id="2600e-157">이 파일에 SchoolContext, 학생, 회사 포털 등록, 및 과정 클래스를 다음과 같이 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-157">In this file, define the SchoolContext, Student, Enrollment, and Course classes as follows:</span></span>

[!code-csharp[Main](retrieving-data/samples/sample4.cs)]

<span data-ttu-id="2600e-158">SchoolContext 클래스는 데이터베이스 연결 및 데이터의 변경 작업을 관리 하는 DbContext에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-158">The SchoolContext class derives from DbContext, which manages the database connection and changes in the data.</span></span>

<span data-ttu-id="2600e-159">Student 클래스에서 특성에 적용 된을 확인는 **FirstName**, **LastName**, 및 **연도** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-159">In the Student class, notice the attributes that have been applied to the **FirstName**, **LastName**, and **Year** properties.</span></span> <span data-ttu-id="2600e-160">이러한 특성은이 자습서의 데이터 유효성 검사에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-160">These attributes will be used for data validation in this tutorial.</span></span> <span data-ttu-id="2600e-161">이 데모 프로젝트에 대 한 코드를 간소화 하기 위해 이러한 속성에만 데이터 유효성 검사 특성으로 표시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-161">To simplify the code for this demonstration project, only these properties were marked with data-validation attributes.</span></span> <span data-ttu-id="2600e-162">실제 프로젝트에서 등록 및 과정 클래스의 속성 등의 유효성이 검사 된 데이터를 필요로 하는 모든 속성에 유효성 검사 특성을 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-162">In a real project, you would apply validation attributes to all properties that need validated data, such as properties in the Enrollment and Course classes.</span></span>

<span data-ttu-id="2600e-163">Save UniversityModels.cs.</span><span class="sxs-lookup"><span data-stu-id="2600e-163">Save UniversityModels.cs.</span></span>

<span data-ttu-id="2600e-164">이러한 클래스에 따라 데이터베이스를 설정 하려면 Code First 마이그레이션을 위한 도구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-164">You will use the tools for Code First Migrations to set up a database based on these classes.</span></span>

<span data-ttu-id="2600e-165">**패키지 관리자 콘솔**, 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-165">In **Package Manager Console**, run the command:</span></span>  
`enable-migrations -ContextTypeName ContosoUniversityModelBinding.Models.SchoolContext`

<span data-ttu-id="2600e-166">마이그레이션을 사용할 수 없다는 메시지가 나타납니다 명령이 성공적으로 완료 되는 경우</span><span class="sxs-lookup"><span data-stu-id="2600e-166">If the command completes successfully you will receive a message stating migrations have been enabled,</span></span>

![마이그레이션을 사용 하도록 설정](retrieving-data/_static/image8.png)

<span data-ttu-id="2600e-168">새 파일의 이름이 사라졌는지 **Configuration.cs** 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-168">Notice that a new file named **Configuration.cs** has been created.</span></span> <span data-ttu-id="2600e-169">Visual Studio에서이 파일을 만든 후 열 자동으로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-169">In Visual Studio, this file is automatically opened after it is created.</span></span> <span data-ttu-id="2600e-170">구성 클래스를 포함 한 **시드** 메서드 테스트 데이터로 데이터베이스 테이블을 미리 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-170">The Configuration class contains a **Seed** method which enables you to pre-populate the database tables with test data.</span></span>

<span data-ttu-id="2600e-171">Seed 메서드를 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-171">Add the following code to the Seed method.</span></span> <span data-ttu-id="2600e-172">추가 해야 합니다는 **를 사용 하 여** 문에 **ContosoUniversityModelBinding.Models** 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-172">You'll need to add a **using** statement for the **ContosoUniversityModelBinding.Models** namespace.</span></span>

[!code-csharp[Main](retrieving-data/samples/sample5.cs)]

<span data-ttu-id="2600e-173">Configuration.cs를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-173">Save Configuration.cs.</span></span>

<span data-ttu-id="2600e-174">패키지 관리자 콘솔에서 다음 명령을 실행 `add-migration initial`합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-174">In the Package Manager Console, run the command `add-migration initial`.</span></span>

<span data-ttu-id="2600e-175">그런 다음 명령을 실행 `update-database`합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-175">Then, run the command `update-database`.</span></span>

<span data-ttu-id="2600e-176">이 명령을 실행할 때 예외를 수신 경우 Seed 메서드 값에서 StudentID 및 CourseID 값에는 다양 한 수입니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-176">If you receive an exception when running this command, it is possible that the values for StudentID and CourseID have varied from the values in the Seed method.</span></span> <span data-ttu-id="2600e-177">데이터베이스에 해당 테이블을 열고 StudentID 및 CourseID에 대 한 기존 값을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-177">Open those tables in the database and find existing values for StudentID and CourseID.</span></span> <span data-ttu-id="2600e-178">등록 테이블 시드를 위해 코드에서 해당 값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-178">Add those values in the code for seeding the Enrollments table.</span></span>

<span data-ttu-id="2600e-179">데이터베이스 파일을 추가 되었지만 프로젝트에 숨겨져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-179">The database file has been added, but it is currently hidden in the project.</span></span> <span data-ttu-id="2600e-180">클릭 **모든 파일 표시** 파일을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-180">Click **Show All Files** to display the file.</span></span>

![모든 파일 표시](retrieving-data/_static/image10.png)

<span data-ttu-id="2600e-182">.Mdf 파일 이제 응용 프로그램에 나타납니다.\_데이터 폴더.</span><span class="sxs-lookup"><span data-stu-id="2600e-182">Notice the .mdf file now appears in the App\_Data folder.</span></span>

![데이터베이스 파일](retrieving-data/_static/image12.png)

<span data-ttu-id="2600e-184">.Mdf 파일을 두 번 클릭 하 고 서버 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-184">Double-click the .mdf file and open the Server Explorer.</span></span> <span data-ttu-id="2600e-185">이제 테이블 존재 하 고 데이터로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-185">The tables now exist and are populated with data.</span></span>

![데이터베이스 테이블](retrieving-data/_static/image14.png)

## <a name="display-data-from-students-and-related-tables"></a><span data-ttu-id="2600e-187">학생 및 관련된 테이블의 데이터 표시</span><span class="sxs-lookup"><span data-stu-id="2600e-187">Display data from Students and related tables</span></span>

<span data-ttu-id="2600e-188">데이터베이스의 데이터로 준비가 이제 해당 데이터를 검색 하 고 웹 페이지에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-188">With data in the database, you are now ready to retrieve that data and display it in a web page.</span></span> <span data-ttu-id="2600e-189">사용 하 여 한 **GridView** 컨트롤을 데이터 열과 행에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-189">You will use a **GridView** control to display the data in columns and rows.</span></span>

<span data-ttu-id="2600e-190">Students.aspx를 열고 찾습니다는 **MainContent** 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-190">Open Students.aspx, and locate the **MainContent** placeholder.</span></span> <span data-ttu-id="2600e-191">자리 표시자를 내 추가 **GridView** 다음 코드를 포함 하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-191">Within that placeholder, add a **GridView** control that includes the following code.</span></span>

[!code-aspx[Main](retrieving-data/samples/sample6.aspx)]

<span data-ttu-id="2600e-192">이 태그 코드를 감지 하는 데 중요 한 개념의 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-192">There are a couple of important concepts in this markup code for you to notice.</span></span> <span data-ttu-id="2600e-193">먼저, 값에 설정 되어 있는지 확인할 수는 **SelectMethod** GridView 요소의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-193">First, notice that a value is set for the **SelectMethod** property in the GridView element.</span></span> <span data-ttu-id="2600e-194">이 값에 GridView에 대 한 데이터를 검색 하기 위해 사용 되는 메서드의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-194">This value specifies the name of the method that is used for retrieving data for the GridView.</span></span> <span data-ttu-id="2600e-195">이 메서드는 다음 단계에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-195">You will create this method in the next step.</span></span> <span data-ttu-id="2600e-196">둘째, 여기서는 **ItemType** 앞에서 만든 Student 클래스 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-196">Second, notice that the **ItemType** property is set to the Student class that you created earlier.</span></span> <span data-ttu-id="2600e-197">이 값을 설정 하 여 태그 코드에 해당 클래스의 속성을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-197">By setting this value, you can refer to properties of that class in the markup code.</span></span> <span data-ttu-id="2600e-198">예를 들어 Student 클래스 등록 라는 컬렉션을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-198">For example, the Student class contains a collection named Enrollments.</span></span> <span data-ttu-id="2600e-199">사용할 수 있습니다 **Item.Enrollments** 를 해당 컬렉션을 검색 하 고 다음 LINQ 구문을 사용 하 여 각 학생에 대해 등록 된 크레딧의 합계를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-199">You can use **Item.Enrollments** to retrieve that collection and then use LINQ syntax to retrieve the sum of enrolled credits for each student.</span></span>

<span data-ttu-id="2600e-200">코드 숨김 파일에서에 대해 지정 된 메서드를 추가 해야는 **SelectMethod** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-200">In the code-behind file, you need to add the method that is specified for the **SelectMethod** value.</span></span> <span data-ttu-id="2600e-201">열기 **Students.aspx.cs**, 추가 **를 사용 하 여** 에 대 한 문을 **ContosoUniversityModelBinding.Models** 및 **System.Data.Entity**네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-201">Open **Students.aspx.cs**, and add **using** statements for the **ContosoUniversityModelBinding.Models** and **System.Data.Entity** namespaces.</span></span>

[!code-csharp[Main](retrieving-data/samples/sample7.cs)]

<span data-ttu-id="2600e-202">다음 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-202">Then, add the following method.</span></span> <span data-ttu-id="2600e-203">이 메서드의 이름을 SelectMethod에 대해 제공한 이름과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-203">Notice that the name of this method matches the name you provided for SelectMethod.</span></span>

[!code-csharp[Main](retrieving-data/samples/sample8.cs)]

<span data-ttu-id="2600e-204">**Include** 절이 쿼리의 성능이 향상 되지만 쿼리 작업을 위해 반드시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-204">The **Include** clause improves the performance of this query but is not essential for the query to work.</span></span> <span data-ttu-id="2600e-205">Include 절 없이 보내는 데이터베이스에 별도 쿼리가 각 시간 관련 데이터를 검색 하는 작업이 포함 된 지연 로드를 사용 하 여 데이터를 검색할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-205">Without the Include clause, the data would be retrieved using lazy loading, which involves sending a separate query to the database each time related data is retrieved.</span></span> <span data-ttu-id="2600e-206">또한 Include 절을 제공 하 여 데이터 관련된 데이터의 모든 데이터베이스의 단일 쿼리를 통해 검색 됩니다 즉 즉시 로드를 사용 하 여 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-206">By providing the Include clause, the data is retrieved using eager loading, which means all of the related data is retrieved through a single query of the database.</span></span> <span data-ttu-id="2600e-207">관련된 데이터의 대부분은 아닐 경우에 더 많은 데이터가 검색 되기 때문에 사용 되는, 즉시 로드 덜 효율적인 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-207">In cases where most of the related data is not be used, eager loading can be less efficient because more data is retrieved.</span></span> <span data-ttu-id="2600e-208">그러나이 경우 즉시 로드 최상의 성능을 제공 각 레코드에 대해 관련된 데이터 표시 되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-208">However, in this case, eager loading provides the best performance because the related data is displayed for each record.</span></span>

<span data-ttu-id="2600e-209">로드할 때 성능 고려 사항에 대 한 자세한 내용은 관련 데이터에 대 한 섹션을 참조 하세요. **Lazy, Eager, 및 관련 데이터의 명시적 로드** 에 [는 ASP에서 Entity Framework와 관련 된 데이터 읽기 .NET MVC 응용 프로그램](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-209">For more information about performance consideration when loading related data, see the section titled **Lazy, Eager, and Explicit Loading of Related Data** in the [Reading Related Data with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) topic.</span></span>

<span data-ttu-id="2600e-210">기본적으로 데이터 키로 표시 된 속성의 값에 따라 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-210">By default, the data is sorted by the values of the property marked as the key.</span></span> <span data-ttu-id="2600e-211">정렬에 대 한 다른 값을 지정 하려면 OrderBy 절을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-211">You can add an OrderBy clause to specify a different value for sorting.</span></span> <span data-ttu-id="2600e-212">이 예제에서는 기본 StudentID 속성이 정렬에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-212">In this example, the default StudentID property is used for sorting.</span></span> <span data-ttu-id="2600e-213">에 [정렬, 페이징, 및 데이터 필터링](sorting-paging-and-filtering-data.md) 항목 정렬에 대 한 열을 선택 하려면 사용자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-213">In the [Sorting, Paging, and Filtering Data](sorting-paging-and-filtering-data.md) topic, you will enable the user to select a column for sorting.</span></span>

<span data-ttu-id="2600e-214">웹 응용 프로그램을 실행 하 고 학생 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-214">Run your web application, and navigate to the Students page.</span></span> <span data-ttu-id="2600e-215">학생 페이지에는 다음 학생 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-215">The Students page displays the following student information.</span></span>

![데이터 표시](retrieving-data/_static/image16.png)

## <a name="automatic-generation-of-model-binding-methods"></a><span data-ttu-id="2600e-217">모델 바인딩 메서드를 자동으로 생성</span><span class="sxs-lookup"><span data-stu-id="2600e-217">Automatic generation of model binding methods</span></span>

<span data-ttu-id="2600e-218">이 자습서 시리즈를 작업할 때 프로젝트에 다음 자습서의 코드를 단순히 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-218">When working through this tutorial series, you can simply copy the code from the tutorial to your project.</span></span> <span data-ttu-id="2600e-219">그러나 한 가지이 접근 방법의 단점은 자동으로 모델 바인딩 방법에 대 한 코드를 생성 하기 위해 Visual Studio에서 제공 하는 기능의 사실을 인식 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-219">However, one disadvantage of this approach is that you may not become aware of the feature provided by Visual Studio to automatically generate code for model binding methods.</span></span> <span data-ttu-id="2600e-220">사용자의 프로젝트를 사용할 때 자동 코드 생성 하면 시간 및 도움말 작업을 구현 하는 방법의 의미를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-220">When working on your own projects, automatic code generation can save you time and help you gain a sense of how to implement an operation.</span></span> <span data-ttu-id="2600e-221">이 섹션에서는 자동 코드 생성 기능을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-221">This section describes the automatic code generation feature.</span></span> <span data-ttu-id="2600e-222">이 섹션에는 정보 제공만 고 프로젝트에 구현 하는 데 필요한 모든 코드가 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-222">This section is only informational and does not contain any code you need to implement in your project.</span></span>

<span data-ttu-id="2600e-223">에 대 한 값을 설정할 때의 **SelectMethod**, **UpdateMethod**, **InsertMethod**, 또는 **DeleteMethod** 태그 코드에서 속성 선택할 수는 **새 메서드 만들기** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-223">When setting a value for the **SelectMethod**, **UpdateMethod**, **InsertMethod**, or **DeleteMethod** properties in the markup code, you can select the **Create New Method** option.</span></span>

![새 메서드 만들기](retrieving-data/_static/image18.png)

<span data-ttu-id="2600e-225">Visual Studio 적절 한 서명 사용 하 여 코드 숨김의 메서드를 만들고 뿐만 아니라도 작업을 수행 해야 하는지 구현 코드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-225">Visual Studio not only creates a method in the code-behind with the proper signature, but also generates implementation code to assist you with performing the operation.</span></span> <span data-ttu-id="2600e-226">처음 설정 하는 경우는 **ItemType** 생성된 된 코드 자동 코드 생성 기능을 사용 하기 전에 속성을이 작업에 대 한 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-226">If you first set the **ItemType** property before using the automatic code generation feature, the generated code will use that type for the operations.</span></span> <span data-ttu-id="2600e-227">예를 들어, UpdateMethod 속성을 설정할 때 다음 코드가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-227">For example, when setting the UpdateMethod property, the following code is automatically generated:</span></span>

[!code-csharp[Main](retrieving-data/samples/sample9.cs)]

<span data-ttu-id="2600e-228">다시 위의 코드에서 프로젝트에 추가할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-228">Again, the above code does not need to be added to your project.</span></span> <span data-ttu-id="2600e-229">다음 자습서에서는 업데이트, 삭제 및 새 데이터를 추가 하기 위한 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-229">In the next tutorial, you will implement methods for updating, deleting and adding new data.</span></span>

## <a name="conclusion"></a><span data-ttu-id="2600e-230">결론</span><span class="sxs-lookup"><span data-stu-id="2600e-230">Conclusion</span></span>

<span data-ttu-id="2600e-231">이 자습서에서는 데이터 모델 클래스를 만들고 해당 클래스에서 데이터베이스를 생성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-231">In this tutorial, you created data model classes and generated a database from those classes.</span></span> <span data-ttu-id="2600e-232">테스트 데이터를 데이터베이스 테이블을 채울.</span><span class="sxs-lookup"><span data-stu-id="2600e-232">You filled the database tables with test data.</span></span> <span data-ttu-id="2600e-233">모델 바인딩 데이터베이스에서 데이터를 검색 한 다음는 GridView에 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-233">You used model binding to retrieve data from the database, and then displayed the data in a GridView.</span></span>

<span data-ttu-id="2600e-234">다음에서 [자습서](updating-deleting-and-creating-data.md) 이 시리즈의 업데이트, 삭제, 및 데이터를 만드는 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2600e-234">In the next [tutorial](updating-deleting-and-creating-data.md) in this series, you will enable updating, deleting, and creating data.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="2600e-235">다음</span><span class="sxs-lookup"><span data-stu-id="2600e-235">Next</span></span>](updating-deleting-and-creating-data.md)
