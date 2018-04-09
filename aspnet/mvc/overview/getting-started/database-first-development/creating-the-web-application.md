---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: 'ASP.NET MVC를 사용 하 여 먼저 EF 데이터베이스: 웹 응용 프로그램 및 데이터 모델 만들기 | Microsoft Docs'
author: tfitzmac
description: MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 seri 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/01/2014
ms.topic: article
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: 04ccc00fa48702608fdc7b5b00d73778985852f9
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="ef-database-first-with-aspnet-mvc-creating-the-web-application-and-data-models"></a><span data-ttu-id="ba15b-104">ASP.NET MVC를 사용 하 여 먼저 EF 데이터베이스: 웹 응용 프로그램 및 데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="ba15b-104">EF Database First with ASP.NET MVC: Creating the Web Application and Data Models</span></span>
====================
<span data-ttu-id="ba15b-105">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="ba15b-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="ba15b-106">MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-106">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="ba15b-107">이 자습서 시리즈 자동으로 표시, 편집를 만들 수 있도록 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-107">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="ba15b-108">생성 된 코드는 데이터베이스 테이블의 열에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-108">The generated code corresponds to the columns in the database table.</span></span>
> 
> <span data-ttu-id="ba15b-109">시리즈의이 부분에서는 웹 응용 프로그램을 만드는 하 고 데이터베이스 테이블 기반 데이터 모델을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-109">This part of the series focuses on creating the web application, and generating the data models based on your database tables.</span></span>


## <a name="create-a-new-aspnet-web-application"></a><span data-ttu-id="ba15b-110">새 ASP.NET 웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="ba15b-110">Create a new ASP.NET Web Application</span></span>

<span data-ttu-id="ba15b-111">새 솔루션 또는 데이터베이스 프로젝트와 동일한 솔루션에서 Visual Studio에서 새 프로젝트를 만들고 선택 된 **ASP.NET 웹 응용 프로그램** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="ba15b-111">In either a new solution or the same solution as the database project, create a new project in Visual Studio and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="ba15b-112">프로젝트 이름을 **ContosoSite**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-112">Name the project **ContosoSite**.</span></span>

![프로젝트 만들기](creating-the-web-application/_static/image1.png)

<span data-ttu-id="ba15b-114">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-114">Click **OK**.</span></span>

<span data-ttu-id="ba15b-115">새 ASP.NET 프로젝트 창에서 선택 된 **MVC** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="ba15b-115">In the New ASP.NET Project window, select the **MVC** template.</span></span> <span data-ttu-id="ba15b-116">지울 수는 **클라우드의 호스트에에서** 나중에 응용 프로그램을 클라우드에 배포한 때문에 당분간 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-116">You can clear the **Host in the cloud** option for now because you will deploy the application to the cloud later.</span></span> <span data-ttu-id="ba15b-117">클릭 **확인** 는 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-117">Click **OK** to create the application.</span></span>

![mvc 템플릿 선택](creating-the-web-application/_static/image2.png)

<span data-ttu-id="ba15b-119">기본 파일 및 폴더는 프로젝트 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-119">The project is created with the default files and folders.</span></span>

<span data-ttu-id="ba15b-120">이 자습서에서는 Entity Framework 6을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-120">In this tutorial, you will use Entity Framework 6.</span></span> <span data-ttu-id="ba15b-121">NuGet 패키지 관리 창을 통해 프로젝트의 버전의 Entity Framework를 다시 확인 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-121">You can double-check the version of Entity Framework in your project through the Manage NuGet Packages window.</span></span> <span data-ttu-id="ba15b-122">필요한 경우 Entity Framework의 버전을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-122">If necessary, update your version of Entity Framework.</span></span>

![버전이 표시 됨](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a><span data-ttu-id="ba15b-124">모델 생성</span><span class="sxs-lookup"><span data-stu-id="ba15b-124">Generate the models</span></span>

<span data-ttu-id="ba15b-125">이제 데이터베이스 테이블에서 Entity Framework 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-125">You will now create Entity Framework models from the database tables.</span></span> <span data-ttu-id="ba15b-126">이러한 모델은 데이터를 사용 하는 데 사용할 수 있는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-126">These models are classes that you will use to work with the data.</span></span> <span data-ttu-id="ba15b-127">각 모델 미러 데이터베이스의 테이블 및 테이블의 열에 해당 하는 속성이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-127">Each model mirrors a table in the database and contains properties that correspond to the columns in the table.</span></span>

<span data-ttu-id="ba15b-128">마우스 오른쪽 단추로 클릭는 **모델** 폴더를 찾아 선택 **추가** 및 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-128">Right-click the **Models** folder, and select **Add** and **New Item**.</span></span>

![새 항목 추가](creating-the-web-application/_static/image4.png)

<span data-ttu-id="ba15b-130">새 항목 추가 창에서 선택한 **데이터** 왼쪽된 창에서 및 **ADO.NET 엔터티 데이터 모델** 가운데 창에 있는 옵션에서입니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-130">In the Add New Item window, select **Data** in the left pane and **ADO.NET Entity Data Model** from the options in the center pane.</span></span> <span data-ttu-id="ba15b-131">새 모델 파일 이름을 **ContosoModel**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-131">Name the new model file **ContosoModel**.</span></span>

![모델 만들기](creating-the-web-application/_static/image5.png)

<span data-ttu-id="ba15b-133">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-133">Click **Add**.</span></span>

<span data-ttu-id="ba15b-134">엔터티 데이터 모델 마법사에서 선택 **데이터베이스의 EF 디자이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-134">In the Entity Data Model Wizard, select **EF Designer from database**.</span></span>

![데이터베이스에서 생성](creating-the-web-application/_static/image6.png)

<span data-ttu-id="ba15b-136">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-136">Click **Next**.</span></span>

<span data-ttu-id="ba15b-137">개발 환경 내에서 정의 된 데이터베이스 연결을 사용 하는 경우에 미리 선택 된 이러한 연결 중 하나가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-137">If you have database connections defined within your development environment, you may see one of these connections pre-selected.</span></span> <span data-ttu-id="ba15b-138">그러나이 자습서의 첫 번째 단계에서 만든 데이터베이스에 새 연결을 만들려면 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-138">However, you want to create a new connection to the database you created in the first part of this tutorial.</span></span> <span data-ttu-id="ba15b-139">클릭는 **새 연결** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-139">Click the **New Connection** button.</span></span>

![데이터베이스에 연결](creating-the-web-application/_static/image7.png)

<span data-ttu-id="ba15b-141">연결 속성 창에서 데이터베이스가 만들어 졌는 로컬 서버 이름을 제공 합니다 (이 경우 **(localdb) \ProjectsV12**).</span><span class="sxs-lookup"><span data-stu-id="ba15b-141">In the Connection Properties window, provide the name of the local server where your database was created (in this case **(localdb)\ProjectsV12**).</span></span> <span data-ttu-id="ba15b-142">입력 한 후 서버 이름을, 사용 가능한 데이터베이스에서의 ContosoUniversityData를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-142">After providing the server name, select the ContosoUniversityData from the available databases.</span></span>

![연결 속성 설정](creating-the-web-application/_static/image8.png)

<span data-ttu-id="ba15b-144">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-144">Click **OK**.</span></span>

<span data-ttu-id="ba15b-145">올바른 연결 속성이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-145">The correct connection properties are now displayed.</span></span> <span data-ttu-id="ba15b-146">연결에 대 한 기본 이름을 사용 하 여 Web.Config 파일에서</span><span class="sxs-lookup"><span data-stu-id="ba15b-146">You can use the default name for connection in the Web.Config file</span></span>

![연결 설정](creating-the-web-application/_static/image9.png)

<span data-ttu-id="ba15b-148">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-148">Click **Next**.</span></span>

<span data-ttu-id="ba15b-149">선택 **테이블** 세 테이블에 대 한 모델을 생성 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-149">Select **Tables** to generate models for all three tables.</span></span>

![테이블 선택](creating-the-web-application/_static/image10.png)

<span data-ttu-id="ba15b-151">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-151">Click **Finish**.</span></span>

<span data-ttu-id="ba15b-152">보안 경고가 표시 되 면 선택 **확인** 계속 서식 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-152">If you receive a security warning, select **OK** to continue running the template.</span></span>

<span data-ttu-id="ba15b-153">데이터베이스 테이블에서 생성 되어 및 속성 및 테이블 간의 관계를 보여 주는 다이어그램 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-153">The models are generated from the database tables, and a diagram is displayed that shows the properties and relationships between the tables.</span></span>

![모델의 다이어그램](creating-the-web-application/_static/image11.png)

<span data-ttu-id="ba15b-155">이제 모델 폴더에는 데이터베이스에서 생성 된 모델과 관련 된 많은 새 파일이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-155">The Models folder now includes many new files related to the models that were generated from the database.</span></span>

![새 모델 파일 표시](creating-the-web-application/_static/image12.png)

<span data-ttu-id="ba15b-157">**ContosoModel.Context.cs** 에서 파생 되는 클래스를 포함 하는 파일의 **DbContext** 클래스를 데이터베이스 테이블에 해당 하는 각 모델 클래스에 대 한 속성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-157">The **ContosoModel.Context.cs** file contains a class that derives from the **DbContext** class, and provides a property for each model class that corresponds to a database table.</span></span> <span data-ttu-id="ba15b-158">**Course.cs**, **Enrollment.cs**, 및 **Student.cs** 파일 데이터베이스 테이블을 나타내는 모델 클래스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-158">The **Course.cs**, **Enrollment.cs**, and **Student.cs** files contain the model classes that represent the databases tables.</span></span> <span data-ttu-id="ba15b-159">스 캐 폴딩 작업할 때 컨텍스트 클래스와 모델 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-159">You will use both the context class and the model classes when working with scaffolding.</span></span>

<span data-ttu-id="ba15b-160">이 자습서와 함께 계속 하기 전에 프로젝트를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="ba15b-160">Before proceeding with this tutorial, build the project.</span></span> <span data-ttu-id="ba15b-161">다음 섹션에는 프로젝트가 빌드되지 않은 경우 작동 하지 것입니다 하지만 데이터 모델을 기반으로 하는 코드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba15b-161">In the next section, you will generate code based on the data models, but that section will not work if the project has not been built.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ba15b-162">[이전](setting-up-database.md)
> [다음](generating-views.md)</span><span class="sxs-lookup"><span data-stu-id="ba15b-162">[Previous](setting-up-database.md)
[Next](generating-views.md)</span></span>
