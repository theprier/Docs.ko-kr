---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: '자습서: 만들기는 웹 응용 프로그램 및 데이터 모델 EF에 대 한 ASP.NET MVC를 사용 하 여 첫 번째 데이터베이스'
description: 이 자습서는 웹 응용 프로그램을 만들고 데이터베이스 테이블 기반 데이터 모델 생성에 중점을 둡니다.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: dced55386c3f810e406c5c2b3f0071b45e3b2dbd
ms.sourcegitcommit: c47d7c131eebbcd8811e31edda210d64cf4b9d6b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55236369"
---
# <a name="tutorial-create-the-the-web-application-and-data-models-for-ef-database-first-with-aspnet-mvc"></a><span data-ttu-id="28602-103">자습서: 만들기는 웹 응용 프로그램 및 데이터 모델 EF에 대 한 ASP.NET MVC를 사용 하 여 첫 번째 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="28602-103">Tutorial: Create the the Web Application and Data Models for EF Database First with ASP.NET MVC</span></span>

 <span data-ttu-id="28602-104">MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28602-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="28602-105">이 자습서 시리즈에서는 자동으로 표시, 편집, 만들기, 사용자를 사용 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="28602-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="28602-106">생성된 된 코드는 데이터베이스 테이블의 열에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="28602-107">이 자습서는 웹 응용 프로그램을 만들고 데이터베이스 테이블 기반 데이터 모델 생성에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="28602-107">This tutorial focuses on creating the web application, and generating the data models based on your database tables.</span></span>

<span data-ttu-id="28602-108">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="28602-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="28602-109">ASP.NET 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="28602-109">Create an ASP.NET web app</span></span>
> * <span data-ttu-id="28602-110">모델 생성</span><span class="sxs-lookup"><span data-stu-id="28602-110">Generate the models</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28602-111">전제 조건</span><span class="sxs-lookup"><span data-stu-id="28602-111">Prerequisites</span></span>

* [<span data-ttu-id="28602-112">Entity Framework 6 Database First MVC 5를 사용 하 여 시작</span><span class="sxs-lookup"><span data-stu-id="28602-112">Getting started with Entity Framework 6 Database First using MVC 5</span></span>](setting-up-database.md)

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="28602-113">ASP.NET 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="28602-113">Create an ASP.NET web app</span></span>

<span data-ttu-id="28602-114">새 솔루션 또는 데이터베이스 프로젝트와 동일한 솔루션에서 Visual Studio에서 새 프로젝트 만들기 및 선택 합니다 **ASP.NET 웹 응용 프로그램** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="28602-114">In either a new solution or the same solution as the database project, create a new project in Visual Studio and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="28602-115">프로젝트 이름을 **ContosoSite**합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-115">Name the project **ContosoSite**.</span></span>

![프로젝트 만들기](creating-the-web-application/_static/image1.png)

<span data-ttu-id="28602-117">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-117">Click **OK**.</span></span>

<span data-ttu-id="28602-118">새 ASP.NET 프로젝트 창에서 선택 합니다 **MVC** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="28602-118">In the New ASP.NET Project window, select the **MVC** template.</span></span> <span data-ttu-id="28602-119">지울 수는 **클라우드에서 호스트** 나중에 응용 프로그램을 클라우드에 배포 하기 때문에 지금은 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="28602-119">You can clear the **Host in the cloud** option for now because you will deploy the application to the cloud later.</span></span> <span data-ttu-id="28602-120">클릭 **확인** 응용 프로그램을 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-120">Click **OK** to create the application.</span></span>

<span data-ttu-id="28602-121">프로젝트 기본 파일 및 폴더를 사용 하 여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="28602-121">The project is created with the default files and folders.</span></span>

<span data-ttu-id="28602-122">이 자습서에서는 Entity Framework 6을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-122">In this tutorial, you will use Entity Framework 6.</span></span> <span data-ttu-id="28602-123">NuGet 패키지 관리 창을 통해 프로젝트에서 Entity Framework의 버전을 다시 확인 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28602-123">You can double-check the version of Entity Framework in your project through the Manage NuGet Packages window.</span></span> <span data-ttu-id="28602-124">필요한 경우 Entity Framework의 버전을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-124">If necessary, update your version of Entity Framework.</span></span>

![버전 표시](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a><span data-ttu-id="28602-126">모델 생성</span><span class="sxs-lookup"><span data-stu-id="28602-126">Generate the models</span></span>

<span data-ttu-id="28602-127">이제 데이터베이스 테이블에서 Entity Framework 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28602-127">You will now create Entity Framework models from the database tables.</span></span> <span data-ttu-id="28602-128">이러한 모델은 데이터를 사용 하 여 작업을 사용 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="28602-128">These models are classes that you will use to work with the data.</span></span> <span data-ttu-id="28602-129">각 모델 미러 데이터베이스의 테이블 및 테이블의 열에 해당 하는 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-129">Each model mirrors a table in the database and contains properties that correspond to the columns in the table.</span></span>

<span data-ttu-id="28602-130">마우스 오른쪽 단추로 클릭 합니다 **모델** 폴더를 선택한 **추가** 하 고 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-130">Right-click the **Models** folder, and select **Add** and **New Item**.</span></span>

<span data-ttu-id="28602-131">새 항목 추가 창에서 선택 **데이터** 왼쪽된 창에서 및 **ADO.NET Entity Data Model** 가운데 창에 있는 옵션에서입니다.</span><span class="sxs-lookup"><span data-stu-id="28602-131">In the Add New Item window, select **Data** in the left pane and **ADO.NET Entity Data Model** from the options in the center pane.</span></span> <span data-ttu-id="28602-132">새 모델 파일의 이름을 **ContosoModel**합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-132">Name the new model file **ContosoModel**.</span></span>

<span data-ttu-id="28602-133">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-133">Click **Add**.</span></span>

<span data-ttu-id="28602-134">엔터티 데이터 모델 마법사에서 선택 **데이터베이스의 EF 디자이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-134">In the Entity Data Model Wizard, select **EF Designer from database**.</span></span>

<span data-ttu-id="28602-135">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-135">Click **Next**.</span></span>

<span data-ttu-id="28602-136">개발 환경 내에 정의 된 데이터베이스 연결에 있는 경우 미리 선택이 연결 중 하나가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28602-136">If you have database connections defined within your development environment, you may see one of these connections pre-selected.</span></span> <span data-ttu-id="28602-137">그러나이 자습서의 첫 번째 부분에서 만든 데이터베이스에 새 연결을 만들려고 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28602-137">However, you want to create a new connection to the database you created in the first part of this tutorial.</span></span> <span data-ttu-id="28602-138">클릭 합니다 **새 연결** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="28602-138">Click the **New Connection** button.</span></span>

<span data-ttu-id="28602-139">연결 속성 창에서 데이터베이스에 만들어진 로컬 서버의 이름을 제공 합니다 (이 예제의 **(localdb) \Projects13**).</span><span class="sxs-lookup"><span data-stu-id="28602-139">In the Connection Properties window, provide the name of the local server where your database was created (in this case **(localdb)\Projects13**).</span></span> <span data-ttu-id="28602-140">서버 이름을 입력 한 후 사용 가능한 데이터베이스에서의 ContosoUniversityData를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-140">After providing the server name, select the ContosoUniversityData from the available databases.</span></span>

![연결 속성 설정](creating-the-web-application/_static/image8.png)

<span data-ttu-id="28602-142">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-142">Click **OK**.</span></span>

<span data-ttu-id="28602-143">올바른 연결 속성 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28602-143">The correct connection properties are now displayed.</span></span> <span data-ttu-id="28602-144">Web.Config 파일에서 연결에 대 한 기본 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28602-144">You can use the default name for connection in the Web.Config file.</span></span>

<span data-ttu-id="28602-145">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-145">Click **Next**.</span></span>

<span data-ttu-id="28602-146">Entity Framework의 최신 버전을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-146">Select the latest version of Entity Framework.</span></span>

<span data-ttu-id="28602-147">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-147">Click **Next**.</span></span>

<span data-ttu-id="28602-148">선택 **테이블** 세 테이블 모두에 대 한 모델을 생성 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-148">Select **Tables** to generate models for all three tables.</span></span>

<span data-ttu-id="28602-149">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-149">Click **Finish**.</span></span>

<span data-ttu-id="28602-150">보안 경고를 받은 경우 선택할 **확인** 템플릿 실행을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-150">If you receive a security warning, select **OK** to continue running the template.</span></span>

<span data-ttu-id="28602-151">데이터베이스 테이블에서 생성 되어 및 속성 및 테이블 간의 관계를 보여 주는 다이어그램 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28602-151">The models are generated from the database tables, and a diagram is displayed that shows the properties and relationships between the tables.</span></span>

![모델의 다이어그램](creating-the-web-application/_static/image11.png)

<span data-ttu-id="28602-153">Models 폴더에는 이제 데이터베이스에서 생성 된 모델에 관련 된 많은 새 파일이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28602-153">The Models folder now includes many new files related to the models that were generated from the database.</span></span>

<span data-ttu-id="28602-154">**ContosoModel.Context.cs** 파일에서 파생 된 클래스를 포함 합니다 **DbContext** 클래스 및 데이터베이스 테이블에 해당 하는 각 모델 클래스에 대 한 속성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-154">The **ContosoModel.Context.cs** file contains a class that derives from the **DbContext** class, and provides a property for each model class that corresponds to a database table.</span></span> <span data-ttu-id="28602-155">합니다 **Course.cs**, **Enrollment.cs**, 및 **Student.cs** 파일 데이터베이스 테이블을 나타내는 모델 클래스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-155">The **Course.cs**, **Enrollment.cs**, and **Student.cs** files contain the model classes that represent the databases tables.</span></span> <span data-ttu-id="28602-156">스 캐 폴딩을 사용 하는 경우 컨텍스트 클래스와 모델 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-156">You will use both the context class and the model classes when working with scaffolding.</span></span>

<span data-ttu-id="28602-157">이 자습서를 진행 하기 전에 프로젝트를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="28602-157">Before proceeding with this tutorial, build the project.</span></span> <span data-ttu-id="28602-158">다음 섹션에서는 섹션에는 프로젝트가 빌드되지 않은 경우 작동 하지 것입니다 하지만 데이터 모델을 기반으로 하는 코드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-158">In the next section, you will generate code based on the data models, but that section will not work if the project has not been built.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28602-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="28602-159">Next steps</span></span>

<span data-ttu-id="28602-160">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="28602-160">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="28602-161">ASP.NET 웹 앱을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-161">Created an ASP.NET web app</span></span>
> * <span data-ttu-id="28602-162">모델 생성</span><span class="sxs-lookup"><span data-stu-id="28602-162">Generated the models</span></span>

<span data-ttu-id="28602-163">데이터 모델을 기반으로 하는 코드를 생성 하는 만드는 방법에 알아보려면 다음 자습서로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="28602-163">Advance to the next tutorial to learn how to create generate code based on the data models.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="28602-164">뷰 생성</span><span class="sxs-lookup"><span data-stu-id="28602-164">Generating views</span></span>](generating-views.md)