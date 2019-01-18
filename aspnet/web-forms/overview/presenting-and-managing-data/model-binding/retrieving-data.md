---
uid: web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
title: 검색 하 고 사용 하 여 데이터 모델 바인딩 및 web forms | Microsoft Docs
author: Rick-Anderson
description: 이 자습서 시리즈에서는 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩을 통해 데이터 상호 작용 자세한 직선-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 9f24fb82-c7ac-48da-b8e2-51b3da17e365
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
msc.type: authoredcontent
ms.openlocfilehash: c53c27f4852eab9813bd917315111e7cd3b04953
ms.sourcegitcommit: 184ba5b44d1c393076015510ac842b77bc9d4d93
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2019
ms.locfileid: "54396287"
---
<a name="retrieving-and-displaying-data-with-model-binding-and-web-forms"></a><span data-ttu-id="8dacf-104">모델 바인딩 및 web forms를 사용 하 여 데이터 검색 및 표시</span><span class="sxs-lookup"><span data-stu-id="8dacf-104">Retrieving and displaying data with model binding and web forms</span></span>
====================

> <span data-ttu-id="8dacf-105">이 자습서 시리즈에서는 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-105">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="8dacf-106">모델 바인딩 보다 직관적인 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource) 처리 하는 보다 데이터 상호 작용 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-106">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="8dacf-107">이 시리즈 소개 자료를 사용 하 여 시작 하 고 나중에 자습서에서 고급 개념을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-107">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
>  <span data-ttu-id="8dacf-108">모델 바인딩 패턴은 모든 데이터 액세스 기술을 사용 하 여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-108">The model binding pattern works with any data access technology.</span></span> <span data-ttu-id="8dacf-109">이 자습서에서는 Entity Framework를 사용 하는 하지만 가장 익숙한 데이터 액세스 기술을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-109">In this tutorial, you will use Entity Framework, but you could use the data access technology that is most familiar to you.</span></span> <span data-ttu-id="8dacf-110">GridView, ListView, DetailsView 또는 FormView 컨트롤과 같은 데이터 바인딩된 서버 컨트롤에서 선택, 업데이트, 삭제 및 데이터 만들기에 대 한 사용 하는 방법의 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-110">From a data-bound server control, such as a GridView, ListView, DetailsView, or FormView control, you specify the names of the methods to use for selecting, updating, deleting, and creating data.</span></span> <span data-ttu-id="8dacf-111">이 자습서에서는 SelectMethod에 대 한 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-111">In this tutorial, you will specify a value for the SelectMethod.</span></span> 
> 
> <span data-ttu-id="8dacf-112">이 메서드 내에서 데이터를 검색 하기 위한 논리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-112">Within that method, you provide the logic for retrieving the data.</span></span> <span data-ttu-id="8dacf-113">다음 자습서에서는 DeleteMethod UpdateMethod, InsertMethod 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-113">In the next tutorial, you will set values for UpdateMethod, DeleteMethod and InsertMethod.</span></span>
>
> <span data-ttu-id="8dacf-114">할 수 있습니다 [다운로드](https://go.microsoft.com/fwlink/?LinkId=286116) 전체 프로젝트에서 C# 또는 Visual Basic입니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-114">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or Visual Basic.</span></span> <span data-ttu-id="8dacf-115">다운로드 가능한 코드는 Visual Studio 2012 이상에 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-115">The downloadable code works with Visual Studio 2012 and later.</span></span> <span data-ttu-id="8dacf-116">이 자습서에 나와 있는 Visual Studio 2017 템플릿은 약간 다른 Visual Studio 2012 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-116">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2017 template shown in this tutorial.</span></span>
> 
> <span data-ttu-id="8dacf-117">이 자습서에서 Visual Studio에서 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-117">In the tutorial you run the application in Visual Studio.</span></span> <span data-ttu-id="8dacf-118">호스팅 공급자에 응용 프로그램을 배포 하 고 인터넷을 통해 사용할 수 있도록 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-118">You can also deploy the application to a hosting provider and make it available over the internet.</span></span> <span data-ttu-id="8dacf-119">Microsoft에서 제공 하는 무료 웹 호스팅에 최대 10 개의 웹 사이트를</span><span class="sxs-lookup"><span data-stu-id="8dacf-119">Microsoft offers free web hosting for up to 10 web sites in a</span></span>  
>  <span data-ttu-id="8dacf-120">[무료 Azure 평가판 계정](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-120">[free Azure trial account](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="8dacf-121">Visual Studio 웹 프로젝트를 Azure App Service Web Apps를 배포 하는 방법에 대 한 내용은 참조는 [Visual Studio를 사용 하 여 ASP.NET 웹 배포](../../deployment/visual-studio-web-deployment/introduction.md) 시리즈입니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-121">For information about how to deploy a Visual Studio web project to Azure App Service Web Apps, see the [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md) series.</span></span> <span data-ttu-id="8dacf-122">이 자습서에는 Azure SQL Database로 SQL Server 데이터베이스를 배포 하려면 Entity Framework Code First 마이그레이션을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-122">That tutorial also shows how to use Entity Framework Code First Migrations to deploy your SQL Server database to Azure SQL Database.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="8dacf-123">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="8dacf-123">Software versions used in the tutorial</span></span>
> 
> - <span data-ttu-id="8dacf-124">Microsoft Visual Studio 2017 또는 Microsoft Visual Studio Community 2017</span><span class="sxs-lookup"><span data-stu-id="8dacf-124">Microsoft Visual Studio 2017 or Microsoft Visual Studio Community 2017</span></span>
>   
> <span data-ttu-id="8dacf-125">이 자습서는 Visual Studio 2012와 Visual Studio 2013 에서도 작동 하지만 사용자 인터페이스 및 프로젝트 템플릿에서 약간의 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-125">This tutorial also works with Visual Studio 2012 and Visual Studio 2013, but there are some differences in the user interface and project template.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="8dacf-126">만들 내용</span><span class="sxs-lookup"><span data-stu-id="8dacf-126">What you'll build</span></span>

<span data-ttu-id="8dacf-127">이 자습서에서는 다음을 수행 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-127">In this tutorial, you'll:</span></span>

* <span data-ttu-id="8dacf-128">대학의 학생 과정에 등록을 사용 하 여 반영 하는 데이터 개체 작성</span><span class="sxs-lookup"><span data-stu-id="8dacf-128">Build data objects that reflect a university with students enrolled in courses</span></span>
* <span data-ttu-id="8dacf-129">빌드 개체에서 데이터베이스 테이블</span><span class="sxs-lookup"><span data-stu-id="8dacf-129">Build database tables from the objects</span></span>
* <span data-ttu-id="8dacf-130">테스트 데이터로 데이터베이스를 채우는</span><span class="sxs-lookup"><span data-stu-id="8dacf-130">Populate the database with test data</span></span>
* <span data-ttu-id="8dacf-131">웹 폼에서 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-131">Display data in a web form</span></span>

## <a name="create-the-project"></a><span data-ttu-id="8dacf-132">프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-132">Create the project</span></span>

1. <span data-ttu-id="8dacf-133">Visual Studio 2017에서 만들기를 **ASP.NET 웹 응용 프로그램 (.NET Framework)** 라는 프로젝트 **ContosoUniversityModelBinding**합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-133">In Visual Studio 2017, create a **ASP.NET Web Application (.NET Framework)** project called **ContosoUniversityModelBinding**.</span></span>

   ![프로젝트 만들기](retrieving-data/_static/image19.png)

2. <span data-ttu-id="8dacf-135">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-135">Select **OK**.</span></span> <span data-ttu-id="8dacf-136">템플릿을 선택 하려면 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-136">The dialog box to select a template appears.</span></span>

   ![web forms를 선택 합니다.](retrieving-data/_static/image3.png)

3. <span data-ttu-id="8dacf-138">선택 된 **Web Forms** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="8dacf-138">Select the **Web Forms** template.</span></span> 

4. <span data-ttu-id="8dacf-139">필요한 경우 변경에 대 한 인증 **개별 사용자 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-139">If necessary, change the authentication to **Individual User Accounts**.</span></span> 

5. <span data-ttu-id="8dacf-140">**확인**을 선택하여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-140">Select **OK** to create the project.</span></span>

## <a name="modify-site-appearance"></a><span data-ttu-id="8dacf-141">사이트 모양 수정</span><span class="sxs-lookup"><span data-stu-id="8dacf-141">Modify site appearance</span></span>

   <span data-ttu-id="8dacf-142">사이트 모양을 사용자 지정 하는 몇 가지 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-142">Make a few changes to customize site appearance.</span></span> 
   
   1. <span data-ttu-id="8dacf-143">Site.Master 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-143">Open the Site.Master file.</span></span>
   
   2. <span data-ttu-id="8dacf-144">표시할 제목을 변경할 **Contoso University** 아니라 **내 ASP.NET 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-144">Change the title to display **Contoso University** and not **My ASP.NET Application**.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample1.aspx?highlight=1)]

   3. <span data-ttu-id="8dacf-145">머리글 텍스트를 변경 **응용 프로그램 이름** 하 **Contoso University**합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-145">Change the header text from **Application name** to **Contoso University**.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample2.aspx?highlight=7)]

   4. <span data-ttu-id="8dacf-146">적절 하 게 사이트 탐색 헤더 링크를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-146">Change the navigation header links to site appropriate ones.</span></span> 
   
      <span data-ttu-id="8dacf-147">에 대 한 링크를 제거 **에 대 한** 및 **연락처** 하 고, 대신에 연결을 **학생** 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-147">Remove the links for **About** and **Contact** and, instead, link to a **Students** page, which you will create.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample3.aspx)]

   5. <span data-ttu-id="8dacf-148">Save Site.Master.</span><span class="sxs-lookup"><span data-stu-id="8dacf-148">Save Site.Master.</span></span>

## <a name="add-a-web-form-to-display-student-data"></a><span data-ttu-id="8dacf-149">학생 데이터를 표시 하는 web form 추가</span><span class="sxs-lookup"><span data-stu-id="8dacf-149">Add a web form to display student data</span></span>

   1. <span data-ttu-id="8dacf-150">**솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭, 선택 **추가** 차례로 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-150">In **Solution Explorer**, right-click your project, select **Add** and then **New Item**.</span></span> 
   
   2. <span data-ttu-id="8dacf-151">**새 항목 추가** 대화 상자를 선택 합니다 **웹 폼 마스터 페이지를 사용 하 여** 템플릿 하 고 이름을 **Students.aspx**합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-151">In the **Add New Item** dialog box, select the **Web Form with Master Page** template and name it **Students.aspx**.</span></span>

      ![페이지 만들기](retrieving-data/_static/image5.png)

   3. <span data-ttu-id="8dacf-153">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-153">Select **Add**.</span></span>
   
   4. <span data-ttu-id="8dacf-154">웹 폼 마스터 페이지 선택 **Site.Master**합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-154">For the web form's master page, select **Site.Master**.</span></span>
   
   5. <span data-ttu-id="8dacf-155">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-155">Select **OK**.</span></span>
   

## <a name="add-the-data-model"></a><span data-ttu-id="8dacf-156">데이터 모델 추가</span><span class="sxs-lookup"><span data-stu-id="8dacf-156">Add the data model</span></span>

<span data-ttu-id="8dacf-157">에 **모델** 폴더를 라는 클래스를 추가 **UniversityModels.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-157">In the **Models** folder, add a class named **UniversityModels.cs**.</span></span>

   1. <span data-ttu-id="8dacf-158">마우스 오른쪽 단추로 클릭 **모델**를 선택 **추가**를 차례로 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-158">Right-click **Models**, select **Add**, and then **New Item**.</span></span> <span data-ttu-id="8dacf-159">**새 항목 추가** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-159">The **Add New Item** dialog box appears.</span></span>

   2. <span data-ttu-id="8dacf-160">왼쪽된 탐색 메뉴에서 선택 **코드**, 한 다음 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-160">From the left navigation menu, select **Code**, then **Class**.</span></span>

      ![모델 클래스 만들기](retrieving-data/_static/image20.png)

   3. <span data-ttu-id="8dacf-162">클래스의 이름을 **UniversityModels.cs** 선택한 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-162">Name the class **UniversityModels.cs** and select **Add**.</span></span>

      <span data-ttu-id="8dacf-163">이 파일에 정의 된 `SchoolContext`, `Student`, `Enrollment`, 및 `Course` 다음과 같이 클래스:</span><span class="sxs-lookup"><span data-stu-id="8dacf-163">In this file, define the `SchoolContext`, `Student`, `Enrollment`, and `Course` classes as follows:</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample4.cs)]

      <span data-ttu-id="8dacf-164">합니다 `SchoolContext` 클래스에서 파생 되며 `DbContext`, 데이터베이스 연결을 관리 하며 데이터의 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-164">The `SchoolContext` class derives from `DbContext`, which manages the database connection and changes in the data.</span></span>

      <span data-ttu-id="8dacf-165">에 `Student` 클래스에 적용 되는 특성을 확인할 수 있습니다 합니다 `FirstName`, `LastName`, 및 `Year` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-165">In the `Student` class, notice the attributes applied to the `FirstName`, `LastName`, and `Year` properties.</span></span> <span data-ttu-id="8dacf-166">이 자습서에서는 데이터 유효성 검사에 대 한 이러한 특성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-166">This tutorial uses these attributes for data validation.</span></span> <span data-ttu-id="8dacf-167">코드 단순화 하기 위해, 데이터 유효성 검사 특성을 사용 하 여 이러한 속성만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-167">To simplify the code, only these properties are marked with data-validation attributes.</span></span> <span data-ttu-id="8dacf-168">실제 프로젝트에서 유효성 검사 특성 유효성 검사를 필요로 하는 모든 속성에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-168">In a real project, you would apply validation attributes to all properties needing validation.</span></span>

   4. <span data-ttu-id="8dacf-169">Save UniversityModels.cs.</span><span class="sxs-lookup"><span data-stu-id="8dacf-169">Save UniversityModels.cs.</span></span>

## <a name="set-up-the-database-based-on-classes"></a><span data-ttu-id="8dacf-170">클래스를 기반으로 데이터베이스를 설정</span><span class="sxs-lookup"><span data-stu-id="8dacf-170">Set up the database based on classes</span></span>

<span data-ttu-id="8dacf-171">이 자습서에서는 [Code First 마이그레이션을](https://docs.microsoft.com/en-us/ef/ef6/modeling/code-first/migrations/) 개체를 만들고 데이터베이스 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-171">This tutorial uses [Code First Migrations](https://docs.microsoft.com/en-us/ef/ef6/modeling/code-first/migrations/) to create objects and database tables.</span></span> <span data-ttu-id="8dacf-172">이러한 테이블 학생 및 해당 과정에 대 한 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-172">These tables store information about the students and their courses.</span></span>

   1. <span data-ttu-id="8dacf-173">선택 **도구가** > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-173">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

   2. <span data-ttu-id="8dacf-174">**패키지 관리자 콘솔**,이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-174">In **Package Manager Console**, run this command:</span></span>  
      `enable-migrations -ContextTypeName ContosoUniversityModelBinding.Models.SchoolContext`

      <span data-ttu-id="8dacf-175">명령을 성공적으로 완료 되 면 마이그레이션을 사용할 수 있게 되었다는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-175">If the command completes successfully, a message stating migrations have been enabled appears.</span></span>

      ![마이그레이션을 사용 하도록 설정](retrieving-data/_static/image8.png)

      <span data-ttu-id="8dacf-177">이라는 파일이 되었다는 *Configuration.cs* 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-177">Notice that a file named *Configuration.cs* has been created.</span></span> <span data-ttu-id="8dacf-178">합니다 `Configuration` 클래스에는 `Seed` 메서드를 테스트 데이터를 사용 하 여 데이터베이스 테이블을 미리 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-178">The `Configuration` class has a `Seed` method, which can pre-populate the database tables with test data.</span></span>

## <a name="pre-populate-the-database"></a><span data-ttu-id="8dacf-179">데이터베이스를 미리 채우기</span><span class="sxs-lookup"><span data-stu-id="8dacf-179">Pre-populate the database</span></span>

   1. <span data-ttu-id="8dacf-180">Configuration.cs를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-180">Open Configuration.cs.</span></span>
   
   2. <span data-ttu-id="8dacf-181">`Seed` 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-181">Add the following code to the `Seed` method.</span></span> <span data-ttu-id="8dacf-182">또한 추가 `using` 에 대 한 문의 `ContosoUniversityModelBinding. Models` 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-182">Also, add a `using` statement for the `ContosoUniversityModelBinding. Models` namespace.</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample5.cs)]

   3. <span data-ttu-id="8dacf-183">Configuration.cs를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-183">Save Configuration.cs.</span></span>

   4. <span data-ttu-id="8dacf-184">패키지 관리자 콘솔에서 명령을 실행 **추가 마이그레이션 초기**합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-184">In the Package Manager Console, run the command **add-migration initial**.</span></span>

   5. <span data-ttu-id="8dacf-185">명령을 실행 **데이터베이스 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-185">Run the command **update-database**.</span></span>

      <span data-ttu-id="8dacf-186">이 명령을 실행 하는 경우 예외를 수신 하는 경우는 `StudentID` 하 고 `CourseID` 값이 다를 수 있습니다는 `Seed` 메서드 값입니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-186">If you receive an exception when running this command, the `StudentID` and `CourseID` values might be different from the `Seed` method values.</span></span> <span data-ttu-id="8dacf-187">에 대 한 기존 값을 찾고 해당 데이터베이스 테이블을 엽니다 `StudentID` 고 `CourseID`입니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-187">Open those database tables and find existing values for `StudentID` and `CourseID`.</span></span> <span data-ttu-id="8dacf-188">시드를 위해 코드에 해당 값을 추가 합니다 `Enrollments` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-188">Add those values to the code for seeding the `Enrollments` table.</span></span>

## <a name="add-a-gridview-control"></a><span data-ttu-id="8dacf-189">GridView 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-189">Add a GridView control</span></span>

<span data-ttu-id="8dacf-190">채워진된 데이터베이스 데이터를 사용 하 여 이제 해당 데이터를 검색 하 고이 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-190">With populated database data, you're now ready to retrieve that data and display it.</span></span> 

1. <span data-ttu-id="8dacf-191">Students.aspx를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-191">Open Students.aspx.</span></span>

2. <span data-ttu-id="8dacf-192">찾을 `MainContent` 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-192">Locate the `MainContent` placeholder.</span></span> <span data-ttu-id="8dacf-193">자리 표시자를 추가 된 **GridView** 이 코드를 포함 하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-193">Within that placeholder, add a **GridView** control that includes this code.</span></span>

   [!code-aspx-csharp[Main](retrieving-data/samples/sample6.aspx)]

   <span data-ttu-id="8dacf-194">유의 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-194">Things to note:</span></span>
   * <span data-ttu-id="8dacf-195">값이 설정에 대 한 공지를 `SelectMethod` GridView 요소의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-195">Notice the value set for the `SelectMethod` property in the GridView element.</span></span> <span data-ttu-id="8dacf-196">이 값에는 다음 단계에서 만든 GridView 데이터를 검색 하는 데 사용 하는 메서드를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-196">This value specifies the method used to retrieve GridView data, which you create in the next step.</span></span> 
   
   * <span data-ttu-id="8dacf-197">합니다 `ItemType` 속성을 `Student` 앞에서 만든 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-197">The `ItemType` property is set to the `Student` class created earlier.</span></span> <span data-ttu-id="8dacf-198">이 설정을 통해 태그에 대 한 클래스 속성을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-198">This setting allows you to reference class properties in the markup.</span></span> <span data-ttu-id="8dacf-199">예를 들어, 합니다 `Student` 클래스에는 명명 된 컬렉션이 `Enrollments`합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-199">For example, the `Student` class has a collection named `Enrollments`.</span></span> <span data-ttu-id="8dacf-200">사용할 수 있습니다 `Item.Enrollments` 해당 컬렉션을 검색 한 다음 사용 하 [LINQ 구문](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) 의 각 학생 검색할 크레딧 합계 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-200">You can use `Item.Enrollments` to retrieve that collection and then use [LINQ syntax](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) to retrieve each student's enrolled credits sum.</span></span>
   
3. <span data-ttu-id="8dacf-201">Students.aspx를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-201">Save Students.aspx.</span></span>

## <a name="add-code-to-retrieve-data"></a><span data-ttu-id="8dacf-202">데이터를 검색 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-202">Add code to retrieve data</span></span>

   <span data-ttu-id="8dacf-203">Students.aspx 코드 숨김 파일에서에 대 한 지정 된 메서드를 추가 합니다 `SelectMethod` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-203">In the Students.aspx code-behind file, add the method specified for the `SelectMethod` value.</span></span> 
   
   1. <span data-ttu-id="8dacf-204">Students.aspx.cs를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-204">Open Students.aspx.cs.</span></span>
   
   2. <span data-ttu-id="8dacf-205">추가 `using` 에 대 한 문을 합니다 `ContosoUniversityModelBinding. Models` 및 `System.Data.Entity` 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-205">Add `using` statements for the `ContosoUniversityModelBinding. Models` and `System.Data.Entity` namespaces.</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample7.cs)]

   3. <span data-ttu-id="8dacf-206">에 대 한 지정 된 메서드를 추가 `SelectMethod`:</span><span class="sxs-lookup"><span data-stu-id="8dacf-206">Add the method you specified for `SelectMethod`:</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample8.cs)]

      <span data-ttu-id="8dacf-207">`Include` 절 쿼리 성능이 향상 되지만 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-207">The `Include` clause improves query performance but isn't required.</span></span> <span data-ttu-id="8dacf-208">없이 합니다 `Include` 절에서 데이터를 사용 하 여 검색 됩니다 [ *지연 로드*](https://en.wikipedia.org/wiki/Lazy_loading), 데이터를 검색 하는 관련 된 될 때마다 데이터베이스에 별도 쿼리를 전송 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-208">Without the `Include` clause, the data is retrieved using [*lazy loading*](https://en.wikipedia.org/wiki/Lazy_loading), which involves sending a separate query to the database each time related data is retrieved.</span></span> <span data-ttu-id="8dacf-209">사용 하 여는 `Include` 절에서 데이터를 사용 하 여 검색 됩니다 *선행 로딩과*, 즉, 단일 데이터베이스 쿼리를 관련 된 모든 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-209">With the `Include` clause, data is retrieved using *eager loading*, which means a single database query retrieves all related data.</span></span> <span data-ttu-id="8dacf-210">관련된 데이터를 사용 하지 않는 경우 더 많은 데이터 검색 되기 때문에 선행 로딩과 덜 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-210">If related data isn't used, eager loading is less efficient because more data is retrieved.</span></span> <span data-ttu-id="8dacf-211">그러나이 경우 즉시 로드 하면 최상의 성능을 각 레코드에 대 한 관련된 데이터 표시 되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-211">However, in this case, eager loading gives you the best performance because the related data is displayed for each record.</span></span>

      <span data-ttu-id="8dacf-212">로드 시 성능 고려 사항에 대 한 자세한 내용은 관련 데이터에 대 한 참조를 **지연, 즉시, 및 관련 데이터의 명시적 로드** 섹션을 [ASP.NET에서 Entity Framework를 사용 하 여 관련 데이터 읽기 MVC 응용 프로그램](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="8dacf-212">For more information about performance considerations when loading related data, see the **Lazy, Eager, and Explicit Loading of Related Data** section in the [Reading Related Data with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) article.</span></span>

      <span data-ttu-id="8dacf-213">기본적으로 데이터를 키로 표시 된 속성의 값을 기준으로 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-213">By default, the data is sorted by the values of the property marked as the key.</span></span> <span data-ttu-id="8dacf-214">추가할 수 있습니다는 `OrderBy` 절 다른 정렬 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-214">You can add an `OrderBy` clause to specify a different sort value.</span></span> <span data-ttu-id="8dacf-215">이 예제에서는 기본 `StudentID` 속성은 정렬에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-215">In this example, the default `StudentID` property is used for sorting.</span></span> <span data-ttu-id="8dacf-216">에 [정렬, 페이징 및 필터링 데이터](sorting-paging-and-filtering-data.md) 사용자 문서에서는 정렬할 열을 선택 수입니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-216">In the [Sorting, Paging, and Filtering Data](sorting-paging-and-filtering-data.md) article, the user is enabled to select a column for sorting.</span></span>
 
   4. <span data-ttu-id="8dacf-217">Students.aspx.cs를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-217">Save Students.aspx.cs.</span></span>

## <a name="run-your-application"></a><span data-ttu-id="8dacf-218">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="8dacf-218">Run your application</span></span> 

<span data-ttu-id="8dacf-219">웹 응용 프로그램을 실행 (**F5**)로 이동 합니다 **학생** 페이지에서 다음을 표시 하는:</span><span class="sxs-lookup"><span data-stu-id="8dacf-219">Run your web application (**F5**) and navigate to the **Students** page, which displays the following:</span></span>

   ![데이터를 표시 합니다.](retrieving-data/_static/image16.png)

## <a name="automatic-generation-of-model-binding-methods"></a><span data-ttu-id="8dacf-221">모델 바인딩 메서드를 자동으로 생성</span><span class="sxs-lookup"><span data-stu-id="8dacf-221">Automatic generation of model binding methods</span></span>

<span data-ttu-id="8dacf-222">이 자습서 시리즈를 진행할 때 프로젝트에 자습서에서 코드를 단순히 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-222">When working through this tutorial series, you can simply copy the code from the tutorial to your project.</span></span> <span data-ttu-id="8dacf-223">그러나 하나이 방식의 단점은 없게 되어 자동으로 코드를 생성할 모델 바인딩 메서드는 Visual Studio에서 제공 하는 기능을 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-223">However, one disadvantage of this approach is that you may not become aware of the feature provided by Visual Studio to automatically generate code for model binding methods.</span></span> <span data-ttu-id="8dacf-224">사용자 고유의 프로젝트를 사용할 때 자동 코드 생성 및 저장할 수 있습니다 시간 도움말 작업을 구현 하는 방법의 이해를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-224">When working on your own projects, automatic code generation can save you time and help you gain a sense of how to implement an operation.</span></span> <span data-ttu-id="8dacf-225">이 섹션에서는 자동 코드 생성 기능을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-225">This section describes the automatic code generation feature.</span></span> <span data-ttu-id="8dacf-226">이 섹션에서는 정보 제공 용 이므로 전용 이며 프로젝트에서 구현 해야 할 코드는 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-226">This section is only informational and does not contain any code you need to implement in your project.</span></span> 

<span data-ttu-id="8dacf-227">에 대 한 값을 설정 하는 경우는 `SelectMethod`, `UpdateMethod`, `InsertMethod`, 또는 `DeleteMethod` 태그 코드에서 속성을 선택할 수 있습니다 합니다 **새 메서드 만들기** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-227">When setting a value for the `SelectMethod`, `UpdateMethod`, `InsertMethod`, or `DeleteMethod` properties in the markup code, you can select the **Create New Method** option.</span></span>

![메서드 만들기](retrieving-data/_static/image18.png)

<span data-ttu-id="8dacf-229">Visual Studio는 적절 한 서명 사용 하 여 코드 숨김의 메서드를 만듭니다 뿐 아니라도 작업을 수행 하기 위한 구현 코드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-229">Visual Studio not only creates a method in the code-behind with the proper signature, but also generates implementation code to perform the operation.</span></span> <span data-ttu-id="8dacf-230">먼저 설정 하는 경우는 `ItemType` 자동 코드 생성을 사용 하기 전에 속성 기능을 작업에 대 한 생성 된 코드는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-230">If you first set the `ItemType` property before using the automatic code generation feature, the generated code uses that type for the operations.</span></span> <span data-ttu-id="8dacf-231">예를 들어, 설정 하는 경우는 `UpdateMethod` 속성을 다음 코드를 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-231">For example, when setting the `UpdateMethod` property, the following code is automatically generated:</span></span>

[!code-csharp[Main](retrieving-data/samples/sample9.cs)]

<span data-ttu-id="8dacf-232">마찬가지로이 코드는 프로젝트에 추가할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-232">Again, this code doesn't need to be added to your project.</span></span> <span data-ttu-id="8dacf-233">다음 자습서에서는 업데이트, 삭제 및 새 데이터를 추가 하기 위한 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-233">In the next tutorial, you'll implement methods for updating, deleting, and adding new data.</span></span>

## <a name="summary"></a><span data-ttu-id="8dacf-234">요약</span><span class="sxs-lookup"><span data-stu-id="8dacf-234">Summary</span></span>

<span data-ttu-id="8dacf-235">이 자습서에서는 데이터 모델 클래스를 생성 하 고 해당 클래스에서 데이터베이스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-235">In this tutorial, you created data model classes and generated a database from those classes.</span></span> <span data-ttu-id="8dacf-236">테스트 데이터를 사용 하 여 데이터베이스 테이블을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-236">You filled the database tables with test data.</span></span> <span data-ttu-id="8dacf-237">데이터베이스에서 데이터를 검색할 모델 바인딩을 사용 하 고 GridView에 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-237">You used model binding to retrieve data from the database, and then displayed the data in a GridView.</span></span>

<span data-ttu-id="8dacf-238">다음에 [자습서](updating-deleting-and-creating-data.md) 이 시리즈에서는 업데이트, 삭제 및 만드는 데이터를 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8dacf-238">In the next [tutorial](updating-deleting-and-creating-data.md) in this series, you'll enable updating, deleting, and creating data.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="8dacf-239">다음</span><span class="sxs-lookup"><span data-stu-id="8dacf-239">Next</span></span>](updating-deleting-and-creating-data.md)
