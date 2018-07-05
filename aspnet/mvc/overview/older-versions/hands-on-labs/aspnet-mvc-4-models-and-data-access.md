---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
title: ASP.NET MVC 4 모델 및 데이터 액세스 | Microsoft Docs
author: rick-anderson
description: 참고:이 실습 랩에서 ASP.NET MVC에 대 한 기본 지식이 있다고 가정 합니다. 전에 ASP.NET MVC에서 사용 하지 않은 경우 좋습니다 ASP.NET MVC 4를 초과 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 634ea84b-f904-4afe-b71b-49cccef4d9cc
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
msc.type: authoredcontent
ms.openlocfilehash: afc03d87431632bbb3ab59241de0edb4bb7af12d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37371131"
---
# <a name="aspnet-mvc-4-models-and-data-access"></a><span data-ttu-id="d1043-104">ASP.NET MVC 4 모델 및 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="d1043-104">ASP.NET MVC 4 Models and Data Access</span></span>

<span data-ttu-id="d1043-105">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="d1043-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="d1043-106">웹 캠프 학습 키트 다운로드</span><span class="sxs-lookup"><span data-stu-id="d1043-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="d1043-107">이 실습 랩 기본 지식이 있다고 가정 **ASP.NET MVC**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-107">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="d1043-108">사용 하지 않은 경우 **ASP.NET MVC** 이전 좋습니다 이동해 **ASP.NET MVC 4 기본 사항** 실습 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-108">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>

<span data-ttu-id="d1043-109">이 실습을 이용 하면 향상 된 기능 및 원본 폴더에 제공 된 샘플 웹 응용 프로그램에 사소한 변경 내용을 적용 하 여 이전에 설명 된 새 기능을 통해 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-109">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>

> [!NOTE]
> <span data-ttu-id="d1043-110">웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 됩니다 [Microsoft-웹/WebCampTrainingKit 릴리스](https://aka.ms/webcamps-training-kit)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-110">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="d1043-111">이 랩에 특정 프로젝트에서 제공 됩니다 [ASP.NET MVC 4 모델 및 데이터 액세스](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-111">The project specific to this lab is available at [ASP.NET MVC 4 Models and Data Access](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess).</span></span>

<span data-ttu-id="d1043-112">**ASP.NET MVC 기본 사항** 실습 랩 있습니다 전달 했기 하드 코드 된 데이터는 컨트롤러에서 템플릿 보기에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-112">In **ASP.NET MVC Fundamentals** Hands-on Lab, you have been passing hard-coded data from the Controllers to the View templates.</span></span> <span data-ttu-id="d1043-113">그러나 실제 웹 응용 프로그램을 구축 하기 위해 실제 데이터베이스를 사용 하려는.</span><span class="sxs-lookup"><span data-stu-id="d1043-113">But, in order to build a real Web application, you might want to use a real database.</span></span>

<span data-ttu-id="d1043-114">이 실습 랩에서 Music Store 응용 프로그램에 필요한 데이터 저장 및 검색 하기 위해 데이터베이스 엔진을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-114">This Hands-on Lab will show you how to use a database engine in order to store and retrieve the data needed for the Music Store application.</span></span> <span data-ttu-id="d1043-115">이렇게 하려면 기존 데이터베이스를 사용 하 여 시작 하 고 여기에서 엔터티 데이터 모델을 만듭니다 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-115">To accomplish that, you will start with an existing database and create the Entity Data Model from it.</span></span> <span data-ttu-id="d1043-116">이 실습에서는 전체 충족 됩니다는 **Database First** 접근 방식을 뿐만 **Code First** 접근 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-116">Throughout this lab, you will meet the **Database First** approach as well as the **Code First** approach.</span></span>

<span data-ttu-id="d1043-117">그러나 사용할 수도 있습니다는 **Model First** 접근 하 고 도구를 사용 하 여 동일한 모델을 만들 다음에서 데이터베이스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-117">However, you can also use the **Model First** approach, create the same model using the tools, and then generate the database from it.</span></span>

<span data-ttu-id="d1043-118">![첫 번째 및 데이터베이스 Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs. 먼저 모델")</span><span class="sxs-lookup"><span data-stu-id="d1043-118">![Database First vs. Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs. Model First")</span></span>

<span data-ttu-id="d1043-119">*첫 번째 및 데이터베이스 먼저 모델*</span><span class="sxs-lookup"><span data-stu-id="d1043-119">*Database First vs. Model First*</span></span>

<span data-ttu-id="d1043-120">모델을 생성 한 다음 적절 한 조정 하드 코드 된 데이터를 사용 하는 대신 데이터베이스에서 가져온 데이터를 사용 하 여 저장소 보기를 제공 하는 StoreController에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-120">After generating the Model, you will make the proper adjustments in the StoreController to provide the Store Views with the data taken from the database, instead of using hard-coded data.</span></span> <span data-ttu-id="d1043-121">어떠한 변경 보기 템플릿에 StoreController 반환할 동일한 Viewmodel 보기 템플릿에 때문에 데이터를 데이터베이스에서 가져옵니다이 이번 있지만 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-121">You will not need to make any change to the View templates because the StoreController will be returning the same ViewModels to the View templates, although this time the data will come from the database.</span></span>

<span data-ttu-id="d1043-122">**Code First 접근 방식**</span><span class="sxs-lookup"><span data-stu-id="d1043-122">**The Code First Approach**</span></span>

<span data-ttu-id="d1043-123">Code First 접근 방식 사용 하면 프레임 워크와 함께 일반적으로 클래스를 생성 하지 않고 코드에서 모델을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-123">The Code First approach allows us to define the model from the code without generating classes that are generally coupled with the framework.</span></span>

<span data-ttu-id="d1043-124">코드에서 먼저 모델 개체는 정의 된 Poco를 사용 하 여 &quot;Plain Old CLR Objects&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-124">In code first, model objects are defined with POCOs, &quot;Plain Old CLR Objects&quot;.</span></span> <span data-ttu-id="d1043-125">Poco는 간단한 일반 클래스 상속 하지 있고 인터페이스를 구현 하지 않는입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-125">POCOs are simple plain classes that have no inheritance and do not implement interfaces.</span></span> <span data-ttu-id="d1043-126">데이터베이스에서 자동으로 생성할 수 있습니다 또는 수 기존 데이터베이스를 사용 하 고 코드에서 클래스 매핑을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-126">We can automatically generate the database from them, or we can use an existing database and generate the class mapping from the code.</span></span>

<span data-ttu-id="d1043-127">이 방법을 사용 하는 이점은 모델 유지 됩니다 (이 예제의 경우 Entity Framework), 지 속성 프레임 워크에서 독립 Poco 클래스 매핑 프레임 워크와 결합 되어 있지는입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-127">The benefits of using this approach is that the Model remains independent from the persistence framework (in this case, Entity Framework), as the POCOs classes are not coupled with the mapping framework.</span></span>

> [!NOTE]
> <span data-ttu-id="d1043-128">ASP.NET MVC 4를 기반으로 하는이 랩이 고 Music Store 샘플 응용 프로그램의 버전을 사용자 지정이 실습 랩에 표시 된 기능만 맞게 최소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-128">This Lab is based on ASP.NET MVC 4 and a version of the Music Store sample application customized and minimized to fit only the features shown in this Hands-On Lab.</span></span>
> 
> <span data-ttu-id="d1043-129">전체를 탐색 하려는 경우 **Music Store** 자습서 응용 프로그램에서 찾을 수 있습니다 [MVC 음악 스토어](https://github.com/evilDave/MVC-Music-Store)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-129">If you wish to explore the whole **Music Store** tutorial application you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>


<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="d1043-130">전제 조건</span><span class="sxs-lookup"><span data-stu-id="d1043-130">Prerequisites</span></span>

<span data-ttu-id="d1043-131">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-131">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="d1043-132">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽을 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).</span><span class="sxs-lookup"><span data-stu-id="d1043-132">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="d1043-133">설정</span><span class="sxs-lookup"><span data-stu-id="d1043-133">Setup</span></span>

<span data-ttu-id="d1043-134">**설치 코드 조각**</span><span class="sxs-lookup"><span data-stu-id="d1043-134">**Installing Code Snippets**</span></span>

<span data-ttu-id="d1043-135">편의 위해이 랩에서 함께 관리 하려는 코드의 대부분 제품은 Visual Studio 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-135">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="d1043-136">설치를 실행 하는 코드 조각 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-136">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="d1043-137">이 문서의 부록 참조할 수 있습니다 사용 하는 방법을 알아보려면 원하는 고 Visual Studio 코드 조각을 사용 하 여 잘 모르는 경우 &quot; [부록 c:를 사용 하 여 코드 조각](#AppendixC)&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-137">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="d1043-138">연습</span><span class="sxs-lookup"><span data-stu-id="d1043-138">Exercises</span></span>

<span data-ttu-id="d1043-139">이 실습 랩에서 다음 연습으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-139">This Hands-on Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="d1043-140">연습 1: 데이터베이스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-140">Exercise 1: Adding a Database</span></span>](#Exercise1)
2. [<span data-ttu-id="d1043-141">연습 2: Code First를 사용 하 여 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="d1043-141">Exercise 2: Creating a Database using Code First</span></span>](#Exercise2)
3. [<span data-ttu-id="d1043-142">매개 변수를 사용 하 여 데이터베이스를 쿼리 하는 연습 3:</span><span class="sxs-lookup"><span data-stu-id="d1043-142">Exercise 3: Querying the Database with Parameters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="d1043-143">각 실습 동반 되는 **최종** 연습을 완료 한 후 가져와야 결과 솔루션이 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-143">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="d1043-144">이 연습을 진행 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-144">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="d1043-145">이 랩을 완료 하기 위한 예상 시간: **35 분**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-145">Estimated time to complete this lab: **35 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Adding_a_Database"></a>
### <a name="exercise-1-adding-a-database"></a><span data-ttu-id="d1043-146">연습 1: 데이터베이스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-146">Exercise 1: Adding a Database</span></span>

<span data-ttu-id="d1043-147">이 연습에서는 해당 데이터를 사용 하기 위해 솔루션에 MusicStore 응용 프로그램의 테이블이 있는 데이터베이스를 추가 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-147">In this exercise, you will learn how to add a database with the tables of the MusicStore application to the solution in order to consume its data.</span></span> <span data-ttu-id="d1043-148">데이터베이스 모델을 사용 하 여 생성 되 고 솔루션에 추가 되 면 하드 코드 된 값을 사용 하는 대신 데이터베이스에서 가져온 데이터를 사용 하 여 템플릿 보기를 제공 하기 위해 StoreController 클래스를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-148">Once the database is generated with the model, and added to the solution, you will modify the StoreController class to provide the View template with the data taken from the database, instead of using hard-coded values.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Adding_a_Database"></a>
#### <a name="task-1---adding-a-database"></a><span data-ttu-id="d1043-149">작업 1-데이터베이스 추가</span><span class="sxs-lookup"><span data-stu-id="d1043-149">Task 1 - Adding a Database</span></span>

<span data-ttu-id="d1043-150">이 작업에서는 솔루션 MusicStore 응용 프로그램의 주 테이블을 사용 하 여 이미 만들어진된 데이터베이스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-150">In this task, you will add an already created database with the main tables of the MusicStore application to the solution.</span></span>

1. <span data-ttu-id="d1043-151">엽니다는 **시작할** 솔루션에 있는 **소스/e x 1-AddingADatabaseDBFirst/시작/** 폴더.</span><span class="sxs-lookup"><span data-stu-id="d1043-151">Open the **Begin** solution located at **Source/Ex1-AddingADatabaseDBFirst/Begin/** folder.</span></span>

   1. <span data-ttu-id="d1043-152">일부 누락 된 NuGet 패키지를 다운로드 해야 하기 전에 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-152">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="d1043-153">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-153">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="d1043-154">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="d1043-154">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="d1043-155">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-155">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="d1043-156">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-156">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="d1043-157">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-157">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="d1043-158">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-158">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="d1043-159">추가 **MvcMusicStore** 데이터베이스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-159">Add **MvcMusicStore** database file.</span></span> <span data-ttu-id="d1043-160">이 실습 랩에서 라는 이미 만들어진된 데이터베이스를 사용할지 **MvcMusicStore.mdf**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-160">In this Hands-on Lab, you will use an already created database called **MvcMusicStore.mdf**.</span></span> <span data-ttu-id="d1043-161">이렇게 하려면 마우스 오른쪽 단추로 클릭 **앱\_데이터** 폴더를 가리키고 **추가** 을 클릭 한 다음 **기존 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-161">To do that, right-click **App\_Data** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="d1043-162">이동할 **\Source\Assets** 선택 합니다 **MvcMusicStore.mdf** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-162">Browse to **\Source\Assets** and select the **MvcMusicStore.mdf** file.</span></span>

    <span data-ttu-id="d1043-163">![기존 항목 추가](aspnet-mvc-4-models-and-data-access/_static/image2.png "기존 항목 추가")</span><span class="sxs-lookup"><span data-stu-id="d1043-163">![Adding an Existing Item](aspnet-mvc-4-models-and-data-access/_static/image2.png "Adding an Existing Item")</span></span>

    <span data-ttu-id="d1043-164">*기존 항목 추가*</span><span class="sxs-lookup"><span data-stu-id="d1043-164">*Adding an Existing Item*</span></span>

    <span data-ttu-id="d1043-165">![데이터베이스 파일 MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore.mdf 데이터베이스 파일")</span><span class="sxs-lookup"><span data-stu-id="d1043-165">![MvcMusicStore.mdf database file](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore.mdf database file")</span></span>

    <span data-ttu-id="d1043-166">*MvcMusicStore.mdf 데이터베이스 파일*</span><span class="sxs-lookup"><span data-stu-id="d1043-166">*MvcMusicStore.mdf database file*</span></span>

    <span data-ttu-id="d1043-167">데이터베이스는 프로젝트에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-167">The database has been added to the project.</span></span> <span data-ttu-id="d1043-168">경우에 데이터베이스는 솔루션 내에서 쿼리 수 있으며 다른 데이터베이스 서버에 호스트 된 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-168">Even when the database is located inside the solution, you can query and update it as it was hosted in a different database server.</span></span>

    <span data-ttu-id="d1043-169">![솔루션 탐색기에서 데이터베이스 MvcMusicStore](aspnet-mvc-4-models-and-data-access/_static/image4.png "솔루션 탐색기에서 MvcMusicStore 데이터베이스")</span><span class="sxs-lookup"><span data-stu-id="d1043-169">![MvcMusicStore database in Solution Explorer](aspnet-mvc-4-models-and-data-access/_static/image4.png "MvcMusicStore database in Solution Explorer")</span></span>

    <span data-ttu-id="d1043-170">*솔루션 탐색기에서 MvcMusicStore 데이터베이스*</span><span class="sxs-lookup"><span data-stu-id="d1043-170">*MvcMusicStore database in Solution Explorer*</span></span>
3. <span data-ttu-id="d1043-171">데이터베이스에 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-171">Verify the connection to the database.</span></span> <span data-ttu-id="d1043-172">이 작업을 수행 하려면 두 번 클릭 **MvcMusicStore.mdf** 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-172">To do this, double-click **MvcMusicStore.mdf** to establish a connection.</span></span>

    <span data-ttu-id="d1043-173">![MvcMusicStore.mdf 연결할](aspnet-mvc-4-models-and-data-access/_static/image5.png "MvcMusicStore.mdf에 연결")</span><span class="sxs-lookup"><span data-stu-id="d1043-173">![Connecting to MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "Connecting to MvcMusicStore.mdf")</span></span>

    <span data-ttu-id="d1043-174">*MvcMusicStore.mdf에 연결*</span><span class="sxs-lookup"><span data-stu-id="d1043-174">*Connecting to MvcMusicStore.mdf*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_a_Data_Model"></a>
#### <a name="task-2---creating-a-data-model"></a><span data-ttu-id="d1043-175">작업 2-데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="d1043-175">Task 2 - Creating a Data Model</span></span>

<span data-ttu-id="d1043-176">이 작업에서는 이전 태스크에서 추가 데이터베이스 상호 작용 데이터 모델을 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-176">In this task, you will create a data model to interact with the database added in the previous task.</span></span>

1. <span data-ttu-id="d1043-177">데이터베이스를 나타내는 데이터 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-177">Create a data model that will represent the database.</span></span> <span data-ttu-id="d1043-178">솔루션 탐색기를 마우스 오른쪽 단추 클릭에서이 작업을 수행 하는 **모델** 폴더를 가리킵니다 **추가** 클릭 하 고 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-178">To do this, in Solution Explorer right-click the **Models** folder, point to **Add** and then click **New Item**.</span></span> <span data-ttu-id="d1043-179">에 **새 항목 추가** 대화 상자에서를 **데이터** 템플릿을 차례로 **ADO.NET 엔터티 데이터 모델** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-179">In the **Add New Item** dialog, select the **Data** template and then the **ADO.NET Entity Data Model** item.</span></span> <span data-ttu-id="d1043-180">데이터 모델 이름을 **StoreDB.edmx** 누릅니다 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-180">Change the data model name to **StoreDB.edmx** and click **Add**.</span></span>

    <span data-ttu-id="d1043-181">![StoreDB ADO.NET 엔터티 데이터 모델을 추가](aspnet-mvc-4-models-and-data-access/_static/image6.png "StoreDB ADO.NET 엔터티 데이터 모델 추가")</span><span class="sxs-lookup"><span data-stu-id="d1043-181">![Adding the StoreDB ADO.NET Entity Data Model](aspnet-mvc-4-models-and-data-access/_static/image6.png "Adding the StoreDB ADO.NET Entity Data Model")</span></span>

    <span data-ttu-id="d1043-182">*StoreDB ADO.NET 엔터티 데이터 모델 추가*</span><span class="sxs-lookup"><span data-stu-id="d1043-182">*Adding the StoreDB ADO.NET Entity Data Model*</span></span>
2. <span data-ttu-id="d1043-183">합니다 **엔터티 데이터 모델 마법사** 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-183">The **Entity Data Model Wizard** will appear.</span></span> <span data-ttu-id="d1043-184">이 마법사는 모델 계층의 생성 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-184">This wizard will guide you through the creation of the model layer.</span></span> <span data-ttu-id="d1043-185">모델을 추가 하는 기존 데이터베이스 recentyl 기반을 만들어야 하므로 선택 **데이터베이스에서 생성** 누릅니다 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-185">Since the model should be created based on the existing database recentyl added, select **Generate from database** and click **Next**.</span></span>

    <span data-ttu-id="d1043-186">![모델 콘텐츠 선택](aspnet-mvc-4-models-and-data-access/_static/image7.png "모델 콘텐츠 선택")</span><span class="sxs-lookup"><span data-stu-id="d1043-186">![Choosing the model content](aspnet-mvc-4-models-and-data-access/_static/image7.png "Choosing the model content")</span></span>

    <span data-ttu-id="d1043-187">*모델 콘텐츠 선택*</span><span class="sxs-lookup"><span data-stu-id="d1043-187">*Choosing the model content*</span></span>
3. <span data-ttu-id="d1043-188">데이터베이스에서 모델을 생성 하는 하므로 사용 하 여 연결을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-188">Since you are generating a model from a database, you will need to specify the connection to use.</span></span> <span data-ttu-id="d1043-189">클릭 **새 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-189">Click **New Connection**.</span></span>
4. <span data-ttu-id="d1043-190">선택 **Microsoft SQL Server 데이터베이스 파일** 누릅니다 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-190">Select **Microsoft SQL Server Database File** and click **Continue**.</span></span>

    <span data-ttu-id="d1043-191">![데이터 원본 선택](aspnet-mvc-4-models-and-data-access/_static/image8.png "데이터 원본 선택")</span><span class="sxs-lookup"><span data-stu-id="d1043-191">![Choose data source](aspnet-mvc-4-models-and-data-access/_static/image8.png "Choose data source")</span></span>

    <span data-ttu-id="d1043-192">*데이터 원본 대화 상자를 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="d1043-192">*Choose data source dialog*</span></span>
5. <span data-ttu-id="d1043-193">클릭 **찾아보기** 데이터베이스를 선택 하 고 **MvcMusicStore.mdf** 거주 하시는 **앱\_데이터** 폴더를 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-193">Click **Browse** and select the database **MvcMusicStore.mdf** you located in the **App\_Data** folder and click **OK**.</span></span>

    <span data-ttu-id="d1043-194">![연결 속성](aspnet-mvc-4-models-and-data-access/_static/image9.png "연결 속성")</span><span class="sxs-lookup"><span data-stu-id="d1043-194">![Connection properties](aspnet-mvc-4-models-and-data-access/_static/image9.png "Connection properties")</span></span>

    <span data-ttu-id="d1043-195">*연결 속성*</span><span class="sxs-lookup"><span data-stu-id="d1043-195">*Connection properties*</span></span>
6. <span data-ttu-id="d1043-196">생성된 된 클래스는 엔터티 연결 문자열 이름이 같은 해당 이름을 변경 하십시오 **MusicStoreEntities** 누릅니다 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-196">The generated class should have the same name as the entity connection string, so change its name to **MusicStoreEntities** and click **Next**.</span></span>

    <span data-ttu-id="d1043-197">![데이터 연결 선택](aspnet-mvc-4-models-and-data-access/_static/image10.png "데이터 연결 선택")</span><span class="sxs-lookup"><span data-stu-id="d1043-197">![Choosing the data connection](aspnet-mvc-4-models-and-data-access/_static/image10.png "Choosing the data connection")</span></span>

    <span data-ttu-id="d1043-198">*데이터 연결 선택*</span><span class="sxs-lookup"><span data-stu-id="d1043-198">*Choosing the data connection*</span></span>
7. <span data-ttu-id="d1043-199">데이터베이스 개체를 사용 하 여 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-199">Choose the database objects to use.</span></span> <span data-ttu-id="d1043-200">엔터티 모델만 데이터베이스의 테이블을 사용 하는 경우 선택 합니다 **테이블** 옵션을 확인 합니다 **모델에 외래 키 열을 포함할** 및 **복수화 또는 단 수 화 생성 개체 이름** 옵션 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-200">As the Entity Model will use just the database's tables, select the **Tables** option, and make sure that the **Include foreign key columns in the model** and **Pluralize or singularize generated object names** options are also selected.</span></span> <span data-ttu-id="d1043-201">변경 하려면 모델 Namespace **MvcMusicStore.Model** 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-201">Change the Model Namespace to **MvcMusicStore.Model** and click **Finish**.</span></span>

    <span data-ttu-id="d1043-202">![데이터베이스 개체 선택](aspnet-mvc-4-models-and-data-access/_static/image11.png "데이터베이스 개체 선택")</span><span class="sxs-lookup"><span data-stu-id="d1043-202">![Choosing the database objects](aspnet-mvc-4-models-and-data-access/_static/image11.png "Choosing the database objects")</span></span>

    <span data-ttu-id="d1043-203">*데이터베이스 개체 선택*</span><span class="sxs-lookup"><span data-stu-id="d1043-203">*Choosing the database objects*</span></span>

    > [!NOTE]
    > <span data-ttu-id="d1043-204">보안 경고 대화 상자가 표시 되며, 클릭 **확인** 템플릿을 실행 하 고 모델 엔터티에 대 한 클래스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-204">If a Security Warning dialog is shown, click **OK** to run the template and generate the classes for the model entities.</span></span>
8. <span data-ttu-id="d1043-205">데이터베이스에 각 테이블에 매핑하는 별도 클래스를 만들 수는 있지만 데이터베이스에 대 한 엔터티 다이어그램 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-205">An entity diagram for the database will appear, while a separate class that maps each table to the database will be created.</span></span> <span data-ttu-id="d1043-206">예를 들어 합니다 **앨범** 테이블으로 표시 됩니다는 **앨범** 클래스, 클래스 속성 표의 각 열은 매핑할 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-206">For example, the **Albums** table will be represented by an **Album** class, where each column in the table will map to a class property.</span></span> <span data-ttu-id="d1043-207">이렇게 하면 쿼리 및 데이터베이스의 행을 나타내는 개체를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-207">This will allow you to query and work with objects that represent rows in the database.</span></span>

    <span data-ttu-id="d1043-208">![엔터티 다이어그램](aspnet-mvc-4-models-and-data-access/_static/image12.png "엔터티 다이어그램")</span><span class="sxs-lookup"><span data-stu-id="d1043-208">![Entity diagram](aspnet-mvc-4-models-and-data-access/_static/image12.png "Entity diagram")</span></span>

    <span data-ttu-id="d1043-209">*엔터티 다이어그램*</span><span class="sxs-lookup"><span data-stu-id="d1043-209">*Entity diagram*</span></span>

    > [!NOTE]
    > <span data-ttu-id="d1043-210">T4 템플릿 (.tt)는 엔터티 클래스를 생성 하는 코드를 실행 하 고 동일한 이름의 기존 클래스를 덮어쓰게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-210">The T4 templates (.tt) run code to generate the entities classes and will overwrite the existing classes with the same name.</span></span> <span data-ttu-id="d1043-211">이 예제에서는 클래스 &quot;앨범&quot;, &quot;장르&quot; 하 고 &quot;Artist&quot; 생성된 된 코드를 사용 하 여 덮어썼습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-211">In this example, the classes &quot;Album&quot;, &quot;Genre&quot; and &quot;Artist&quot; were overwritten with the generated code.</span></span>


<a id="Ex1Task3"></a>

<a id="Task_3_-_Building_the_Application"></a>
#### <a name="task-3---building-the-application"></a><span data-ttu-id="d1043-212">작업 3-응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="d1043-212">Task 3 - Building the Application</span></span>

<span data-ttu-id="d1043-213">이 태스크에서는 확인, 모델 생성을 제거 하지만 합니다 **앨범**, **장르** 하 고 **Artist** 모델 클래스는 프로젝트가 성공적으로 빌드되면를 사용 하 여 새 데이터 모델 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-213">In this task, you will check that, although the model generation have removed the **Album**, **Genre** and **Artist** model classes, the project builds successfully by using the new data model classes.</span></span>

1. <span data-ttu-id="d1043-214">선택 하 여 프로젝트를 빌드할 합니다 **빌드** 메뉴 항목 차례로 **MvcMusicStore 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-214">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="d1043-215">![프로젝트를 빌드하면](aspnet-mvc-4-models-and-data-access/_static/image13.png "프로젝트 빌드")</span><span class="sxs-lookup"><span data-stu-id="d1043-215">![Building the project](aspnet-mvc-4-models-and-data-access/_static/image13.png "Building the project")</span></span>

    <span data-ttu-id="d1043-216">*프로젝트 빌드*</span><span class="sxs-lookup"><span data-stu-id="d1043-216">*Building the project*</span></span>
2. <span data-ttu-id="d1043-217">프로젝트가는 성공적으로 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-217">The project builds successfully.</span></span> <span data-ttu-id="d1043-218">이유는 계속 작동 합니까?</span><span class="sxs-lookup"><span data-stu-id="d1043-218">Why does it still work?</span></span> <span data-ttu-id="d1043-219">데이터베이스 테이블 제거 클래스에서 사용 하는 속성을 포함 하는 필드에 있으므로 작동 **앨범** 하 고 **장르**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-219">It works because the database tables have fields that include the properties that you were using in the removed classes **Album** and **Genre**.</span></span>

    <span data-ttu-id="d1043-220">![빌드 성공](aspnet-mvc-4-models-and-data-access/_static/image14.png "빌드 성공")</span><span class="sxs-lookup"><span data-stu-id="d1043-220">![Builds succeeded](aspnet-mvc-4-models-and-data-access/_static/image14.png "Builds succeeded")</span></span>

    <span data-ttu-id="d1043-221">*빌드 성공*</span><span class="sxs-lookup"><span data-stu-id="d1043-221">*Builds succeeded*</span></span>
3. <span data-ttu-id="d1043-222">디자이너 엔터티에 다이어그램 형식으로 표시 하는 동안 C# 클래스는 실제로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-222">While the designer displays the entities in a diagram format, they are really C# classes.</span></span> <span data-ttu-id="d1043-223">확장 된 **StoreDB.edmx** 솔루션 탐색기에서 노드 차례로 **StoreDB.tt**, 생성 된 새 엔터티가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-223">Expand the **StoreDB.edmx** node in the Solution Explorer and then **StoreDB.tt**, you will see the new generated entities.</span></span>

    <span data-ttu-id="d1043-224">![파일을 생성](aspnet-mvc-4-models-and-data-access/_static/image15.png "파일 생성")</span><span class="sxs-lookup"><span data-stu-id="d1043-224">![Generated files](aspnet-mvc-4-models-and-data-access/_static/image15.png "Generated files")</span></span>

    <span data-ttu-id="d1043-225">*생성 된 파일*</span><span class="sxs-lookup"><span data-stu-id="d1043-225">*Generated files*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="d1043-226">작업 4-데이터베이스 쿼리</span><span class="sxs-lookup"><span data-stu-id="d1043-226">Task 4 - Querying the Database</span></span>

<span data-ttu-id="d1043-227">이 태스크에서는 하드 코드 된 데이터를 사용 하는 대신 쿼리 하는 데이터베이스 정보를 검색할 수 있도록 StoreController 클래스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-227">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will query the database to retrieve the information.</span></span>

1. <span data-ttu-id="d1043-228">열기 **Controllers\StoreController.cs** 의 인스턴스를 보관할 클래스에 다음 필드를 추가 합니다 **MusicStoreEntities** 이라는 클래스가 **storeDB**:</span><span class="sxs-lookup"><span data-stu-id="d1043-228">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="d1043-229">(코드 조각- *모델 및 데이터 액세스-e x 1 storeDB*)</span><span class="sxs-lookup"><span data-stu-id="d1043-229">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample1.cs)]
2. <span data-ttu-id="d1043-230">합니다 **MusicStoreEntities** 클래스는 데이터베이스의 각 테이블에 대 한 컬렉션 속성을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-230">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="d1043-231">업데이트 **찾아보기** 모든 장르를 검색 하는 작업 메서드는 **앨범**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-231">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="d1043-232">(코드 조각- *모델과 데이터 액세스-e x 1 저장소 찾아보기*)</span><span class="sxs-lookup"><span data-stu-id="d1043-232">(Code Snippet - *Models And Data Access - Ex1 Store Browse*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample2.cs)]

    > [!NOTE]
    > <span data-ttu-id="d1043-233">호출 하는.NET의 기능을 사용 하는 **LINQ** 프로그래밍할 수 있습니다 (언어 통합 쿼리) 이러한 컬렉션-데이터베이스에 대해 코드를 실행 하 고 반환에 대해 강력한 형식의 쿼리 식을 쓸 개체 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-233">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="d1043-234">LINQ에 대 한 자세한 내용은 참조 하십시오 합니다 [msdn 사이트](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-234">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx).</span></span>
3. <span data-ttu-id="d1043-235">업데이트 **인덱스** 모든 장르를 검색 하는 작업 메서드.</span><span class="sxs-lookup"><span data-stu-id="d1043-235">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="d1043-236">(코드 조각- *모델과 데이터 액세스-e x 1 저장소 인덱스가*)</span><span class="sxs-lookup"><span data-stu-id="d1043-236">(Code Snippet - *Models And Data Access - Ex1 Store Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample3.cs)]
4. <span data-ttu-id="d1043-237">업데이트 **인덱스** 모든 장르를 검색 하 고 컬렉션 목록으로 변환 하는 작업 메서드.</span><span class="sxs-lookup"><span data-stu-id="d1043-237">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="d1043-238">(코드 조각- *모델과 데이터 액세스-e x 1 저장소 GenreMenu*)</span><span class="sxs-lookup"><span data-stu-id="d1043-238">(Code Snippet - *Models And Data Access - Ex1 Store GenreMenu*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample4.cs)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="d1043-239">작업 5-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d1043-239">Task 5 - Running the Application</span></span>

<span data-ttu-id="d1043-240">이 태스크에서는 저장소 인덱스 페이지는 하드 코드 된 것 대신 데이터베이스에 저장 하는 장르 표시 됩니다는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-240">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="d1043-241">보기 템플릿은 변경 하지 않아도 됩니다는 **StoreController** 반환 하는 것과 동일한 엔터티 이전과 마찬가지로 있지만이 이번에 데이터를 데이터베이스에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-241">There is no need to change the View template because the **StoreController** is returning the same entities as before, although this time the data will come from the database.</span></span>

1. <span data-ttu-id="d1043-242">솔루션 및 키를 눌러 다시 빌드 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-242">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="d1043-243">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-243">The project starts in the Home page.</span></span> <span data-ttu-id="d1043-244">확인의 메뉴가 **장르** 는 더 이상 하드 코드 된 목록 및 데이터를 데이터베이스에서 직접 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-244">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image16.png)

    <span data-ttu-id="d1043-246">*데이터베이스에서 장르를 검색*</span><span class="sxs-lookup"><span data-stu-id="d1043-246">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="d1043-247">이제 모든 장르를 이동 하 고 데이터베이스에서 앨범 채워집니다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-247">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="d1043-248">![앨범 데이터베이스에서 검색](aspnet-mvc-4-models-and-data-access/_static/image17.png "앨범을 데이터베이스에서 검색")</span><span class="sxs-lookup"><span data-stu-id="d1043-248">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image17.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="d1043-249">*데이터베이스에서 검색 앨범*</span><span class="sxs-lookup"><span data-stu-id="d1043-249">*Browsing Albums from the database*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Database_Using_Code_First"></a>
### <a name="exercise-2-creating-a-database-using-code-first"></a><span data-ttu-id="d1043-250">연습 2: 코드를 처음 사용 하 여 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="d1043-250">Exercise 2: Creating a Database Using Code First</span></span>

<span data-ttu-id="d1043-251">이 연습에서는 데이터에 액세스 하는 방법과 MusicStore 응용 프로그램의 테이블을 사용 하 여 데이터베이스를 만들려는 Code First 방식을 사용 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-251">In this exercise, you will learn how to use the Code First approach to create a database with the tables of the MusicStore application, and how to access its data.</span></span>

<span data-ttu-id="d1043-252">모델 생성 되 면 하드 코드 된 값을 사용 하는 대신 데이터베이스에서 가져온 데이터를 사용 하 여 보기 템플릿이 제공 StoreController를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-252">Once the model is generated, you will modify the StoreController to provide the View template with the data taken from the database, instead of using hardcoded values.</span></span>

> [!NOTE]
> <span data-ttu-id="d1043-253">연습 1 완료 하 고 이미 Database First 접근 방식으로 작업을 수행 하는 경우 이제 다른 프로세스를 사용 하 여 동일한 결과를 얻는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-253">If you have completed Exercise 1 and have already worked with the Database First approach, you will now learn how to get the same results with a different process.</span></span> <span data-ttu-id="d1043-254">연습 1 공통 된 된 작업에 읽기 쉽게 표시 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-254">The tasks that are in common with Exercise 1 have been marked to make your reading easier.</span></span> <span data-ttu-id="d1043-255">실습 1 완료 되지 않은 하지만 경우 Code First 접근 방식에 알아보려면이 연습에서 시작할 수 있으며 항목의 전체 검사를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-255">If you have not completed Exercise 1 but would like to learn the Code First approach, you can start from this exercise and get a full coverage of the topic.</span></span>


<a id="Ex2Task1"></a>

<a id="Task_1_-_Populating_Sample_Data"></a>
#### <a name="task-1---populating-sample-data"></a><span data-ttu-id="d1043-256">작업 1-샘플 데이터를 채우고</span><span class="sxs-lookup"><span data-stu-id="d1043-256">Task 1 - Populating Sample Data</span></span>

<span data-ttu-id="d1043-257">이 태스크에서는 코드 중심을 사용 하 여 먼저 만들어질 때 샘플 데이터를 사용 하 여 데이터베이스를 채울는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-257">In this task, you will populate the database with sample data when it is intially created using Code-First.</span></span>

1. <span data-ttu-id="d1043-258">엽니다는 **시작할** 솔루션에 있는 **소스/e x 2-CreatingADatabaseCodeFirst/시작/** 폴더.</span><span class="sxs-lookup"><span data-stu-id="d1043-258">Open the **Begin** solution located at **Source/Ex2-CreatingADatabaseCodeFirst/Begin/** folder.</span></span> <span data-ttu-id="d1043-259">그렇지 않은 경우 계속 사용할 수도 있습니다는 **최종** 이전 연습을 완료 하 여 가져온 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-259">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="d1043-260">제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-260">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="d1043-261">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-261">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="d1043-262">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="d1043-262">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="d1043-263">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-263">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="d1043-264">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-264">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="d1043-265">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-265">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="d1043-266">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-266">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="d1043-267">추가 된 **SampleData.cs** 파일을 합니다 **모델** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-267">Add the **SampleData.cs** file to the **Models** folder.</span></span> <span data-ttu-id="d1043-268">이렇게 하려면 마우스 오른쪽 단추로 클릭 **모델** 폴더를 가리키고 **추가** 을 클릭 한 다음 **기존 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-268">To do that, right-click **Models** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="d1043-269">이동할 **\Source\Assets** 선택 합니다 **SampleData.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-269">Browse to **\Source\Assets** and select the **SampleData.cs** file.</span></span>

    <span data-ttu-id="d1043-270">![예제 데이터 코드를 채우는](aspnet-mvc-4-models-and-data-access/_static/image18.png "예제 데이터 코드 채우기")</span><span class="sxs-lookup"><span data-stu-id="d1043-270">![Sample data populate code](aspnet-mvc-4-models-and-data-access/_static/image18.png "Sample data populate code")</span></span>

    <span data-ttu-id="d1043-271">*예제 데이터 코드 채우기*</span><span class="sxs-lookup"><span data-stu-id="d1043-271">*Sample data populate code*</span></span>
3. <span data-ttu-id="d1043-272">엽니다는 **Global.asax.cs** 파일을 추가한 다음 *를 사용 하 여* 문.</span><span class="sxs-lookup"><span data-stu-id="d1043-272">Open the **Global.asax.cs** file and add the following *using* statements.</span></span>

    <span data-ttu-id="d1043-273">(코드 조각- *모델과 데이터 액세스-e x 2 전역 Asax Using*)</span><span class="sxs-lookup"><span data-stu-id="d1043-273">(Code Snippet - *Models And Data Access - Ex2 Global Asax Usings*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample5.cs)]
4. <span data-ttu-id="d1043-274">에 **응용 프로그램\_start ()** 메서드 데이터베이스 이니셜라이저를 설정 하려면 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-274">In the **Application\_Start()** method add the following line to set the database initializer.</span></span>

    <span data-ttu-id="d1043-275">(코드 조각- *모델과 데이터 액세스-e x 2 전역 Asax SetInitializer*)</span><span class="sxs-lookup"><span data-stu-id="d1043-275">(Code Snippet - *Models And Data Access - Ex2 Global Asax SetInitializer*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample6.cs)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Configuring_the_connection_to_the_Database"></a>
#### <a name="task-2---configuring-the-connection-to-the-database"></a><span data-ttu-id="d1043-276">작업 2-데이터베이스 연결 구성</span><span class="sxs-lookup"><span data-stu-id="d1043-276">Task 2 - Configuring the connection to the Database</span></span>

<span data-ttu-id="d1043-277">이제 프로젝트에 데이터베이스를 이미 추가한를 작성 하는 합니다 **Web.config** 파일 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-277">Now that you have already added a database to our project, you will write in the **Web.config** file the connection string.</span></span>

1. <span data-ttu-id="d1043-278">런타임에 연결 문자열을 추가 **Web.config**합니다. 이렇게 하려면 엽니다 **Web.config** 연결 문자열에서이 줄 이라는 DefaultConnection 바꾸고 프로젝트 루트에는 **&lt;connectionStrings&gt;** 섹션:</span><span class="sxs-lookup"><span data-stu-id="d1043-278">Add a connection string at **Web.config**. To do that, open **Web.config** at project root and replace the connection string named DefaultConnection with this line in the **&lt;connectionStrings&gt;** section:</span></span>

    <span data-ttu-id="d1043-279">![Web.config 파일 위치](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config 파일 위치")</span><span class="sxs-lookup"><span data-stu-id="d1043-279">![Web.config file location](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config file location")</span></span>

    <span data-ttu-id="d1043-280">*Web.config 파일 위치*</span><span class="sxs-lookup"><span data-stu-id="d1043-280">*Web.config file location*</span></span>

    [!code-xml[Main](aspnet-mvc-4-models-and-data-access/samples/sample7.xml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Working_with_the_Model"></a>
#### <a name="task-3---working-with-the-model"></a><span data-ttu-id="d1043-281">작업 3-모델 사용</span><span class="sxs-lookup"><span data-stu-id="d1043-281">Task 3 - Working with the Model</span></span>

<span data-ttu-id="d1043-282">데이터베이스에 연결을 이미 구성한 했으므로 데이터베이스 테이블을 사용 하 여 모델을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-282">Now that you have already configured the connection to the database, you will link the model with the database tables.</span></span> <span data-ttu-id="d1043-283">이 태스크에서는 Code First를 사용 하 여 데이터베이스에 연결 되는 클래스를 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-283">In this task, you will create a class that will be linked to the database with Code First.</span></span> <span data-ttu-id="d1043-284">수정 해야 하는 기존 POCO 모델 클래스 임을 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-284">Remember that there is an existent POCO model class that should be modified.</span></span>

> [!NOTE]
> <span data-ttu-id="d1043-285">연습 1에서 완료 한 경우 마법사에서이 단계를 수행한는 기록해둔 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-285">If you completed Exercise 1, you will note that this step was performed by a wizard.</span></span> <span data-ttu-id="d1043-286">Code First를 통해 수동으로 데이터 엔터티에 연결 되는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-286">By doing Code First, you will manually create classes that will be linked to data entities.</span></span>

1. <span data-ttu-id="d1043-287">POCO 모델 클래스를 엽니다 **장르** 에서 **모델** 프로젝트 폴더 및 ID를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-287">Open the POCO model class **Genre** from **Models** project folder and include an ID.</span></span> <span data-ttu-id="d1043-288">Int 속성을 사용 하 여 이름이 **GenreId**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-288">Use an int property with the name **GenreId**.</span></span>

    <span data-ttu-id="d1043-289">(코드 조각- *모델과 데이터 액세스-e x 2 코드 첫 번째 장르*)</span><span class="sxs-lookup"><span data-stu-id="d1043-289">(Code Snippet - *Models And Data Access - Ex2 Code First Genre*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample8.cs)]

    > [!NOTE]
    > <span data-ttu-id="d1043-290">Code First 규칙을 사용 하려면 클래스 장르에 자동으로 검색 되는 기본 키 속성이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-290">To work with Code First conventions, the class Genre must have a primary key property that will be automatically detected.</span></span>
    > 
    > <span data-ttu-id="d1043-291">자세한 내용은이 코드의 첫 번째 규칙에 대 한 [msdn 문서](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-291">You can read more about Code First Conventions in this [msdn article](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx).</span></span>
2. <span data-ttu-id="d1043-292">이제 POCO 모델 클래스를 엽니다 **앨범** 에서 **모델** 고 프로젝트 폴더를 포함 하는 외래 키 속성 이름의 만들기 **GenreId** 고  **ArtistId**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-292">Now, open the POCO model class **Album** from **Models** project folder and include the foreign keys, create properties with the names **GenreId** and **ArtistId**.</span></span> <span data-ttu-id="d1043-293">이미이 클래스는 **GenreId** 기본 키에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-293">This class already have the **GenreId** for the primary key.</span></span>

    <span data-ttu-id="d1043-294">(코드 조각- *모델과 데이터 액세스-e x 2 코드 첫 번째 앨범*)</span><span class="sxs-lookup"><span data-stu-id="d1043-294">(Code Snippet - *Models And Data Access - Ex2 Code First Album*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample9.cs)]
3. <span data-ttu-id="d1043-295">POCO 모델 클래스를 엽니다 **음악가** 포함 된 **ArtistId** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-295">Open the POCO model class **Artist** and include the **ArtistId** property.</span></span>

    <span data-ttu-id="d1043-296">(코드 조각- *모델과 데이터 액세스-e x 2 코드 첫 번째 Artist*)</span><span class="sxs-lookup"><span data-stu-id="d1043-296">(Code Snippet - *Models And Data Access - Ex2 Code First Artist*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample10.cs)]
4. <span data-ttu-id="d1043-297">마우스 오른쪽 단추로 클릭 합니다 **모델** 선택한 프로젝트 폴더 **추가 | 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-297">Right-click the **Models** project folder and select **Add | Class**.</span></span> <span data-ttu-id="d1043-298">파일 이름을 **MusicStoreEntities.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-298">Name the file **MusicStoreEntities.cs**.</span></span> <span data-ttu-id="d1043-299">클릭 **추가 합니다.**</span><span class="sxs-lookup"><span data-stu-id="d1043-299">Then, click **Add.**</span></span>

    <span data-ttu-id="d1043-300">![클래스 추가](aspnet-mvc-4-models-and-data-access/_static/image20.png "클래스 추가")</span><span class="sxs-lookup"><span data-stu-id="d1043-300">![Adding a class](aspnet-mvc-4-models-and-data-access/_static/image20.png "Adding a class")</span></span>

    <span data-ttu-id="d1043-301">*새 항목 추가*</span><span class="sxs-lookup"><span data-stu-id="d1043-301">*Adding a new item*</span></span>

    <span data-ttu-id="d1043-302">![추가 된 class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "를 class2 추가")</span><span class="sxs-lookup"><span data-stu-id="d1043-302">![Adding a class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "Adding a class2")</span></span>

    <span data-ttu-id="d1043-303">*클래스 추가*</span><span class="sxs-lookup"><span data-stu-id="d1043-303">*Adding a class*</span></span>
5. <span data-ttu-id="d1043-304">방금 만든 클래스를 엽니다 **MusicStoreEntities.cs**, 네임 스페이스를 포함 하 고 **System.Data.Entity** 하 고 **System.Data.Entity.Infrastructure**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-304">Open the class you have just created, **MusicStoreEntities.cs**, and include the namespaces **System.Data.Entity** and **System.Data.Entity.Infrastructure**.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample11.cs)]
6. <span data-ttu-id="d1043-305">확장 하려면 클래스 선언을 다음으로 **DbContext** 클래스: 공용 선언 **DBSet** 시키고 **OnModelCreating** 메서드.</span><span class="sxs-lookup"><span data-stu-id="d1043-305">Replace the class declaration to extend the **DbContext** class: declare a public **DBSet** and override **OnModelCreating** method.</span></span> <span data-ttu-id="d1043-306">이 단계를 수행한 후에 Entity Framework를 사용 하 여 모델을 연결 하는 도메인 클래스를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-306">After this step you will get a domain class that will link your model with the Entity Framework.</span></span> <span data-ttu-id="d1043-307">이 작업을 수행 하기 위해 클래스 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-307">In order to do that, replace the class code with the following:</span></span>

    <span data-ttu-id="d1043-308">(코드 조각- *모델과 데이터 액세스-e x 2 코드 첫 번째 MusicStoreEntities*)</span><span class="sxs-lookup"><span data-stu-id="d1043-308">(Code Snippet - *Models And Data Access - Ex2 Code First MusicStoreEntities*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="d1043-309">Entity Framework와 함께 **DbContext** 하 고 **DBSet** POCO 클래스 장르를 쿼리 하는 일을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-309">With Entity Framework **DbContext** and **DBSet** you will be able to query the POCO class Genre.</span></span> <span data-ttu-id="d1043-310">확장 하 여 **OnModelCreating** 에서 지정 하는 메서드는 **코드** 데이터베이스 테이블에 장르 매핑될 방법을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-310">By extending **OnModelCreating** method, you are specifying in the **code** how Genre will be mapped to a database table.</span></span> <span data-ttu-id="d1043-311">이 msdn 문서에서 DBContext 및 DBSet에 대 한 자세한 정보를 찾을 수 있습니다: [링크](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)</span><span class="sxs-lookup"><span data-stu-id="d1043-311">You can find more information about DBContext and DBSet in this msdn article: [link](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="d1043-312">작업 4-데이터베이스 쿼리</span><span class="sxs-lookup"><span data-stu-id="d1043-312">Task 4 - Querying the Database</span></span>

<span data-ttu-id="d1043-313">이 태스크에서는 하드 코드 된 데이터를 사용 하는 대신를 검색 하는 데이터베이스에서 있도록 StoreController 클래스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-313">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will retrieve it from the database.</span></span>

> [!NOTE]
> <span data-ttu-id="d1043-314">연습 1 공통 된이 작업이입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-314">This task is in common with Exercise 1.</span></span>
> 
> <span data-ttu-id="d1043-315">연습 1을 완료 하는 경우 이러한 단계는 두 방법 모두 동일 하 게 기록 됩니다 (먼저 데이터베이스 Code first 또는).</span><span class="sxs-lookup"><span data-stu-id="d1043-315">If you completed Exercise 1 you will note these steps are the same in both approaches (Database first or Code first).</span></span> <span data-ttu-id="d1043-316">데이터 모델을 사용 하면 연결 된 어떻게 서로 이지만 데이터 엔터티에 액세스 컨트롤러에서 투명 한 아직 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-316">They are different in how the data is linked with the model, but the access to data entities is yet transparent from the controller.</span></span>


1. <span data-ttu-id="d1043-317">열기 **Controllers\StoreController.cs** 의 인스턴스를 보관할 클래스에 다음 필드를 추가 합니다 **MusicStoreEntities** 이라는 클래스가 **storeDB**:</span><span class="sxs-lookup"><span data-stu-id="d1043-317">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="d1043-318">(코드 조각- *모델 및 데이터 액세스-e x 1 storeDB*)</span><span class="sxs-lookup"><span data-stu-id="d1043-318">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample13.cs)]
2. <span data-ttu-id="d1043-319">합니다 **MusicStoreEntities** 클래스는 데이터베이스의 각 테이블에 대 한 컬렉션 속성을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-319">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="d1043-320">업데이트 **찾아보기** 모든 장르를 검색 하는 작업 메서드는 **앨범**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-320">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="d1043-321">(코드 조각- *모델과 데이터 액세스-e x 2 저장소 찾아보기*)</span><span class="sxs-lookup"><span data-stu-id="d1043-321">(Code Snippet - *Models And Data Access - Ex2 Store Browse*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="d1043-322">호출 하는.NET의 기능을 사용 하는 **LINQ** 프로그래밍할 수 있습니다 (언어 통합 쿼리) 이러한 컬렉션-데이터베이스에 대해 코드를 실행 하 고 반환에 대해 강력한 형식의 쿼리 식을 쓸 개체 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-322">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="d1043-323">LINQ에 대 한 자세한 내용은 참조 하십시오 합니다 [msdn 사이트](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-323">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx).</span></span>
3. <span data-ttu-id="d1043-324">업데이트 **인덱스** 모든 장르를 검색 하는 작업 메서드.</span><span class="sxs-lookup"><span data-stu-id="d1043-324">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="d1043-325">(코드 조각- *모델과 데이터 액세스-e x 2 저장소 인덱스가*)</span><span class="sxs-lookup"><span data-stu-id="d1043-325">(Code Snippet - *Models And Data Access - Ex2 Store Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample15.cs)]
4. <span data-ttu-id="d1043-326">업데이트 **인덱스** 모든 장르를 검색 하 고 컬렉션 목록으로 변환 하는 작업 메서드.</span><span class="sxs-lookup"><span data-stu-id="d1043-326">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="d1043-327">(코드 조각- *모델과 데이터 액세스-e x 2 저장소 GenreMenu*)</span><span class="sxs-lookup"><span data-stu-id="d1043-327">(Code Snippet - *Models And Data Access - Ex2 Store GenreMenu*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample16.cs)]

<a id="Ex2Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="d1043-328">작업 5-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d1043-328">Task 5 - Running the Application</span></span>

<span data-ttu-id="d1043-329">이 태스크에서는 저장소 인덱스 페이지는 하드 코드 된 것 대신 데이터베이스에 저장 하는 장르 표시 됩니다는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-329">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="d1043-330">보기 템플릿을 변경 하지 않아도 됩니다 합니다 **StoreController** 반환 하는 동일한 **StoreIndexViewModel** 이전과 마찬가지로 이번 데이터 데이터베이스에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-330">There is no need to change the View template because the **StoreController** is returning the same **StoreIndexViewModel** as before, but this time the data will come from the database.</span></span>

1. <span data-ttu-id="d1043-331">솔루션 및 키를 눌러 다시 빌드 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-331">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="d1043-332">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-332">The project starts in the Home page.</span></span> <span data-ttu-id="d1043-333">확인의 메뉴가 **장르** 는 더 이상 하드 코드 된 목록 및 데이터를 데이터베이스에서 직접 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-333">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image22.png)

    <span data-ttu-id="d1043-335">*데이터베이스에서 장르를 검색*</span><span class="sxs-lookup"><span data-stu-id="d1043-335">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="d1043-336">이제 모든 장르를 이동 하 고 데이터베이스에서 앨범 채워집니다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-336">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="d1043-337">![앨범 데이터베이스에서 검색](aspnet-mvc-4-models-and-data-access/_static/image23.png "앨범을 데이터베이스에서 검색")</span><span class="sxs-lookup"><span data-stu-id="d1043-337">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image23.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="d1043-338">*데이터베이스에서 검색 앨범*</span><span class="sxs-lookup"><span data-stu-id="d1043-338">*Browsing Albums from the database*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Querying_the_Database_with_Parameters"></a>
### <a name="exercise-3-querying-the-database-with-parameters"></a><span data-ttu-id="d1043-339">매개 변수를 사용 하 여 데이터베이스를 쿼리 하는 연습 3:</span><span class="sxs-lookup"><span data-stu-id="d1043-339">Exercise 3: Querying the Database with Parameters</span></span>

<span data-ttu-id="d1043-340">이 연습에서는 매개 변수를 사용 하 여 데이터베이스를 쿼리 하는 방법 및 쿼리 결과 셰이핑를 사용 하는 방법을 배우게 됩니다, 그리고를 숫자 데이터베이스를 줄이는 기능을 더 효율적인 방식으로 검색 하는 동안 데이터에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-340">In this exercise, you will learn how to query the database using parameters, and how to use Query Result Shaping, a feature that reduces the number database accesses retrieving data in a more efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="d1043-341">다음을 방문에 대 한 자세한 내용은 쿼리 결과 셰이핑 [msdn 문서](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-341">For further information on Query Result Shaping, visit the following [msdn article](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx).</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_StoreController_to_Retrieve_Albums_from_Database"></a>
#### <a name="task-1---modifying-storecontroller-to-retrieve-albums-from-database"></a><span data-ttu-id="d1043-342">작업 1-앨범 데이터베이스에서 검색할 수정 StoreController</span><span class="sxs-lookup"><span data-stu-id="d1043-342">Task 1 - Modifying StoreController to Retrieve Albums from Database</span></span>

<span data-ttu-id="d1043-343">이 작업을 변경 하는 **StoreController** 앨범에서 특정 장르를 검색 하는 데이터베이스에 액세스 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-343">In this task, you will change the **StoreController** class to access the database to retrieve albums from a specific genre.</span></span>

1. <span data-ttu-id="d1043-344">엽니다는 **시작** 솔루션에 있는 합니다 **Source\Ex3 QueryingTheDatabaseWithParametersCodeFirst\Begin** 코드 중심 접근 방식을 사용 하려는 경우 폴더 또는 **Source\ Ex3 QueryingTheDatabaseWithParametersDBFirst\Begin** 폴더 Database-first 접근 방식을 사용 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="d1043-344">Open the **Begin** solution located at the **Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin** folder if you want to use Code-First approach or **Source\Ex3-QueryingTheDatabaseWithParametersDBFirst\Begin** folder if you want to use Database-First approach.</span></span> <span data-ttu-id="d1043-345">그렇지 않은 경우 계속 사용할 수도 있습니다는 **최종** 이전 연습을 완료 하 여 가져온 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-345">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="d1043-346">제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-346">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="d1043-347">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-347">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="d1043-348">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="d1043-348">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="d1043-349">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-349">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="d1043-350">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-350">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="d1043-351">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-351">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="d1043-352">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-352">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="d1043-353">엽니다는 **StoreController** 변경 하는 클래스는 **찾아보기** 작업 메서드.</span><span class="sxs-lookup"><span data-stu-id="d1043-353">Open the **StoreController** class to change the **Browse** action method.</span></span> <span data-ttu-id="d1043-354">이 수행 하는 **솔루션 탐색기**를 확장 합니다 **컨트롤러** 폴더를 두 번 클릭 **StoreController.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-354">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
3. <span data-ttu-id="d1043-355">변경 된 **찾아보기** 앨범에 대 한 특정 장르를 검색 하는 작업 메서드.</span><span class="sxs-lookup"><span data-stu-id="d1043-355">Change the **Browse** action method to retrieve albums for a specific genre.</span></span> <span data-ttu-id="d1043-356">이 작업을 수행 하려면 다음 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-356">To do this, replace the following code:</span></span>

    <span data-ttu-id="d1043-357">(코드 조각- *모델과 데이터 액세스-Ex3 StoreController BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="d1043-357">(Code Snippet - *Models And Data Access - Ex3 StoreController BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample17.cs)]

> [!NOTE]
> <span data-ttu-id="d1043-358">엔터티의 컬렉션을 채우는 데 사용 해야 합니다 **Include** 너무 앨범을 검색 하려면를 지정 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-358">To populate a collection of the entity, you need to use the **Include** method to specify you want to retrieve the albums too.</span></span> <span data-ttu-id="d1043-359">사용할 수는 있습니다. **Single()** linq에서 확장 때문이 경우 하나의 장르 앨범에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-359">You can use the .**Single()** extension in LINQ because in this case only one genre is expected for an album.</span></span> <span data-ttu-id="d1043-360">합니다 **Single()** 메서드는이 경우 해당 이름에 정의 된 값과 일치 되도록 단일 장르 개체를 지정 하는 매개 변수로 람다 식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-360">The **Single()** method takes a Lambda expression as a parameter, which in this case specifies a single Genre object such that its name matches the value defined.</span></span>
> 
> <span data-ttu-id="d1043-361">장르 개체를 검색할 때도 로드 하려는 다른 관련된 엔터티를 나타낼 수 있도록 하는 기능 활용을 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-361">You will take advantage of a feature that allows you to indicate other related entities you want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="d1043-362">이 기능은 이라고 **쿼리 결과 셰이핑**, 정보를 검색할 데이터베이스에 액세스 하는 데 필요한 횟수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-362">This feature is called **Query Result Shaping**, and enables you to reduce the number of times needed to access the database to retrieve information.</span></span> <span data-ttu-id="d1043-363">이 시나리오에서는 검색 장르에 대 한 앨범을 프리페치 하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-363">In this scenario, you will want to pre-fetch the Albums for the Genre you retrieve.</span></span>
> 
> <span data-ttu-id="d1043-364">쿼리에 **Genres.Include (&quot;앨범&quot;)** 관련된 앨범도 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-364">The query includes **Genres.Include(&quot;Albums&quot;)** to indicate that you want related albums as well.</span></span> <span data-ttu-id="d1043-365">이렇게 하면 보다 효율적인 응용 프로그램에서 요청을 단일 데이터베이스의 데이터를 앨범 및 장르를 검색 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-365">This will result in a more efficient application, since it will retrieve both Genre and Album data in a single database request.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="d1043-366">작업 2-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d1043-366">Task 2 - Running the Application</span></span>

<span data-ttu-id="d1043-367">이 작업에서는 응용 프로그램을 실행 한 데이터베이스에서 앨범을 특정 장르를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-367">In this task, you will run the application and retrieve albums of a specific genre from the database.</span></span>

1. <span data-ttu-id="d1043-368">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-368">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="d1043-369">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-369">The project starts in the Home page.</span></span> <span data-ttu-id="d1043-370">URL을 변경 **/저장소/찾아보기? 장르 Pop =** 데이터베이스에서 결과 가져오는 중 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-370">Change the URL to **/Store/Browse?genre=Pop** to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="d1043-371">![장르별 검색](aspnet-mvc-4-models-and-data-access/_static/image24.png "장르별 검색")</span><span class="sxs-lookup"><span data-stu-id="d1043-371">![Browsing by genre](aspnet-mvc-4-models-and-data-access/_static/image24.png "Browsing by genre")</span></span>

    <span data-ttu-id="d1043-372">*검색/저장소/찾아보기? 장르 Pop =*</span><span class="sxs-lookup"><span data-stu-id="d1043-372">*Browsing /Store/Browse?genre=Pop*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Accessing_Albums_by_Id"></a>
#### <a name="task-3---accessing-albums-by-id"></a><span data-ttu-id="d1043-373">작업 3-Id로 앨범에 액세스</span><span class="sxs-lookup"><span data-stu-id="d1043-373">Task 3 - Accessing Albums by Id</span></span>

<span data-ttu-id="d1043-374">이 태스크에서는 해당 id는 앨범을 가져오려면 이전 절차를 반복 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-374">In this task, you will repeat the previous procedure to get albums by their Id.</span></span>

1. <span data-ttu-id="d1043-375">Visual Studio로 반환 하는 데 필요한 경우 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-375">Close the browser if needed, to return to Visual Studio.</span></span> <span data-ttu-id="d1043-376">엽니다는 **StoreController** 변경 하는 클래스는 **세부 정보** 작업 메서드.</span><span class="sxs-lookup"><span data-stu-id="d1043-376">Open the **StoreController** class to change the **Details** action method.</span></span> <span data-ttu-id="d1043-377">이 수행 하는 **솔루션 탐색기**를 확장 합니다 **컨트롤러** 폴더를 두 번 클릭 **StoreController.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-377">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
2. <span data-ttu-id="d1043-378">변경 된 **세부 정보** 앨범 세부 정보를 검색 하는 작업 메서드를 기반으로 해당 **Id**합니다. 이 작업을 수행 하려면 다음 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-378">Change the **Details** action method to retrieve albums details based on their **Id**. To do this, replace the following code:</span></span>

    <span data-ttu-id="d1043-379">(코드 조각- *모델과 데이터 액세스-Ex3 StoreController DetailsMethod*)</span><span class="sxs-lookup"><span data-stu-id="d1043-379">(Code Snippet - *Models And Data Access - Ex3 StoreController DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample18.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="d1043-380">작업 4-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="d1043-380">Task 4 - Running the Application</span></span>

<span data-ttu-id="d1043-381">이 작업에서는 웹 브라우저에서 응용 프로그램을 실행 및 해당 id로 앨범 세부 정보를 가져올 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-381">In this task, you will run the Application in a web browser and obtain album details by their Id.</span></span>

1. <span data-ttu-id="d1043-382">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-382">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="d1043-383">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-383">The project starts in the Home page.</span></span> <span data-ttu-id="d1043-384">URL을 변경 **/Store/Details/51** 장르 찾아보기 및 앨범 데이터베이스에서 결과 가져오는 중 확인을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-384">Change the URL to **/Store/Details/51** or browse the genres and select an album to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="d1043-385">![세부 정보를 검색](aspnet-mvc-4-models-and-data-access/_static/image25.png "세부 정보를 검색 합니다.")</span><span class="sxs-lookup"><span data-stu-id="d1043-385">![Browsing Details](aspnet-mvc-4-models-and-data-access/_static/image25.png "Browsing Details")</span></span>

    <span data-ttu-id="d1043-386">*검색 /Store/Details/51*</span><span class="sxs-lookup"><span data-stu-id="d1043-386">*Browsing /Store/Details/51*</span></span>

> [!NOTE]
> <span data-ttu-id="d1043-387">또한 다음 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수 있습니다 [부록 b: 게시 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램](#AppendixB)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-387">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="d1043-388">요약</span><span class="sxs-lookup"><span data-stu-id="d1043-388">Summary</span></span>

<span data-ttu-id="d1043-389">ASP.NET MVC 모델 및 데이터 액세스의 기본 사항을 익 혔 실습 랩이 완료를 사용 하 여 합니다 **Database First** 접근 방식 뿐만 **Code First** 접근 방식:</span><span class="sxs-lookup"><span data-stu-id="d1043-389">By completing this Hands-on Lab you have learned the fundamentals of ASP.NET MVC Models and Data Access, using the **Database First** approach as well as the **Code First** Approach:</span></span>

- <span data-ttu-id="d1043-390">해당 데이터를 사용 하기 위해 솔루션에 데이터베이스를 추가 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d1043-390">How to add a database to the solution in order to consume its data</span></span>
- <span data-ttu-id="d1043-391">대신 하드 코드 된 데이터베이스에서 가져온 데이터를 사용 하 여 템플릿 보기를 제공 하는 컨트롤러를 업데이트 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d1043-391">How to update Controllers to provide View templates with the data taken from the database instead of hard-coded one</span></span>
- <span data-ttu-id="d1043-392">매개 변수를 사용 하 여 데이터베이스를 쿼리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d1043-392">How to query the database using parameters</span></span>
- <span data-ttu-id="d1043-393">쿼리 결과 셰이핑, 데이터베이스 액세스의 수를 줄이는 기능 보다 효율적인 방식으로 데이터를 검색을 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d1043-393">How to use the Query Result Shaping, a feature that reduces the number of database accesses, retrieving data in a more efficient way</span></span>
- <span data-ttu-id="d1043-394">모델을 사용 하 여 데이터베이스에 연결할 Microsoft Entity Framework Database First 및 Code First 접근 방식을 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="d1043-394">How to use both Database First and Code First approaches in Microsoft Entity Framework to link the database with the model</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="d1043-395">부록 a: 설치 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="d1043-395">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="d1043-396">설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 사용 하 여 버전을 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="d1043-396">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="d1043-397">다음 지침을 설치 하는 데 필요한 단계를 안내 *Visual studio Express 2012 for Web* 사용 하 여 *Microsoft Web Platform Installer*합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-397">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="d1043-398">로 이동 [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-398">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="d1043-399">또는, 이미 설치한 경우 웹 플랫폼 설치 관리자를 열 수 있습니다 하 고 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Windows Azure SDK를 사용 하 여 Web</em>&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-399">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="d1043-400">클릭할 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-400">Click on **Install Now**.</span></span> <span data-ttu-id="d1043-401">없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-401">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="d1043-402">한 번 **웹 플랫폼 설치 관리자** 열려 있는 경우 클릭 **설치** 는 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-402">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="d1043-403">![Visual Studio Express를 설치](aspnet-mvc-4-models-and-data-access/_static/image26.png "Visual Studio Express를 설치 합니다.")</span><span class="sxs-lookup"><span data-stu-id="d1043-403">![Install Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="d1043-404">*Visual Studio Express를 설치 합니다.*</span><span class="sxs-lookup"><span data-stu-id="d1043-404">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="d1043-405">모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-405">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건에 동의](aspnet-mvc-4-models-and-data-access/_static/image27.png)

    <span data-ttu-id="d1043-407">*사용 조건에 동의*</span><span class="sxs-lookup"><span data-stu-id="d1043-407">*Accepting the license terms*</span></span>
5. <span data-ttu-id="d1043-408">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-408">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](aspnet-mvc-4-models-and-data-access/_static/image28.png)

    <span data-ttu-id="d1043-410">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="d1043-410">*Installation progress*</span></span>
6. <span data-ttu-id="d1043-411">설치가 완료 되 면 클릭 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-411">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](aspnet-mvc-4-models-and-data-access/_static/image29.png)

    <span data-ttu-id="d1043-413">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="d1043-413">*Installation completed*</span></span>
7. <span data-ttu-id="d1043-414">클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-414">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="d1043-415">로 Visual Studio Express for Web을 열려면 합니다 **시작** 화면 및 쓰기를 시작 &quot; **VS Express**&quot;를 클릭 합니다 **VS Express for Web** 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-415">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 타일](aspnet-mvc-4-models-and-data-access/_static/image30.png)

    <span data-ttu-id="d1043-417">*VS Express for Web 타일*</span><span class="sxs-lookup"><span data-stu-id="d1043-417">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="d1043-418">부록 b: 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="d1043-418">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="d1043-419">이 부록은 Windows Azure 관리 포털에서 새 웹 사이트를 만들고 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하 고 랩에 따라 얻은 응용 프로그램을 게시 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-419">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="d1043-420">작업 1-Windows에서 새 웹 사이트를 만드는 Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d1043-420">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="d1043-421">로 이동 합니다 [Windows Azure 관리 포털](https://manage.windowsazure.com/) 구독과 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-421">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d1043-422">Windows Azure를 사용 하 여 10 개의 ASP.NET 웹 사이트를 무료로 호스트할 수 있으며 다음 트래픽 증가 따라 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-422">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="d1043-423">등록할 수 있습니다 [여기](http://aka.ms/aspnet-hol-azure)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-423">You can sign up [here](http://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="d1043-424">![Windows Azure 포털에 로그온](aspnet-mvc-4-models-and-data-access/_static/image31.png "Windows Azure 포털에 로그온")</span><span class="sxs-lookup"><span data-stu-id="d1043-424">![Log on to Windows Azure portal](aspnet-mvc-4-models-and-data-access/_static/image31.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="d1043-425">*Windows Azure 관리 포털에 로그온*</span><span class="sxs-lookup"><span data-stu-id="d1043-425">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="d1043-426">클릭 **새로 만들기** 명령 모음에서.</span><span class="sxs-lookup"><span data-stu-id="d1043-426">Click **New** on the command bar.</span></span>

    <span data-ttu-id="d1043-427">![새 웹 사이트를 만드는](aspnet-mvc-4-models-and-data-access/_static/image32.png "새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="d1043-427">![Creating a new Web Site](aspnet-mvc-4-models-and-data-access/_static/image32.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="d1043-428">*새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="d1043-428">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="d1043-429">클릭 **계산** | **웹 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-429">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="d1043-430">선택한 **빨리 만들기** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-430">Then select **Quick Create** option.</span></span> <span data-ttu-id="d1043-431">새 웹 사이트를 사용할 수 있는 URL을 제공 하 고 클릭 **웹 사이트 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-431">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d1043-432">Windows Azure 웹 사이트는 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램에 대 한 호스트.</span><span class="sxs-lookup"><span data-stu-id="d1043-432">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="d1043-433">빠른 생성 옵션을 사용 하면 완료 된 웹 응용 프로그램을 Windows Azure에서 웹 사이트 포털 외부에서 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-433">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="d1043-434">데이터베이스를 설정 하기 위한 단계는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-434">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="d1043-435">![빠른 생성을 사용 하 여 새 웹 사이트를 만드는](aspnet-mvc-4-models-and-data-access/_static/image33.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="d1043-435">![Creating a new Web Site using Quick Create](aspnet-mvc-4-models-and-data-access/_static/image33.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="d1043-436">*빠른 생성을 사용 하 여 새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="d1043-436">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="d1043-437">새 될 때까지 기다렸다가 **웹 사이트** 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-437">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="d1043-438">웹 사이트를 만든 후 아래의 링크를 클릭 합니다 **URL** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-438">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="d1043-439">새 웹 사이트가 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-439">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="d1043-440">![새 웹 사이트를 찾아](aspnet-mvc-4-models-and-data-access/_static/image34.png "새 웹 사이트를 검색 합니다.")</span><span class="sxs-lookup"><span data-stu-id="d1043-440">![Browsing to the new web site](aspnet-mvc-4-models-and-data-access/_static/image34.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="d1043-441">*새 웹 사이트를 검색합니다.*</span><span class="sxs-lookup"><span data-stu-id="d1043-441">*Browsing to the new web site*</span></span>

    <span data-ttu-id="d1043-442">![실행 중인 웹 사이트](aspnet-mvc-4-models-and-data-access/_static/image35.png "실행 중인 웹 사이트")</span><span class="sxs-lookup"><span data-stu-id="d1043-442">![Web site running](aspnet-mvc-4-models-and-data-access/_static/image35.png "Web site running")</span></span>

    <span data-ttu-id="d1043-443">*실행 중인 웹 사이트*</span><span class="sxs-lookup"><span data-stu-id="d1043-443">*Web site running*</span></span>
6. <span data-ttu-id="d1043-444">포털로 돌아가서에서 웹 사이트의 이름을 클릭 합니다 **이름을** 관리 페이지를 표시 하는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-444">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="d1043-445">![웹 사이트 관리 페이지를 열어](aspnet-mvc-4-models-and-data-access/_static/image36.png "웹 사이트 관리 페이지 열기")</span><span class="sxs-lookup"><span data-stu-id="d1043-445">![Opening the web site management pages](aspnet-mvc-4-models-and-data-access/_static/image36.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="d1043-446">*웹 사이트 관리 페이지 열기*</span><span class="sxs-lookup"><span data-stu-id="d1043-446">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="d1043-447">**대시보드** 페이지의 **간략 상태** 섹션을 클릭 합니다 **게시 프로필 다운로드** 링크.</span><span class="sxs-lookup"><span data-stu-id="d1043-447">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d1043-448">합니다 *게시 프로필* 모든 각각의 설정 된 게시 방법에 대 한 Windows Azure 웹 사이트를 웹 응용 프로그램을 게시 하는 데 필요한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-448">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="d1043-449">게시 프로필에는 Url, 사용자 자격 증명 및 연결 하 고 각 게시 메서드를 사용할 수 있는 끝점에 대해 인증 하는 데 필요한 데이터베이스 문자열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-449">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="d1043-450">**Microsoft WebMatrix 2**하십시오 **Microsoft Visual Studio Express for Web** 하 고 **Microsoft Visual Studio 2012** 읽기 지원 하기 위해 게시 프로필에 대 한 이러한 프로그램의 구성을 자동화할 Windows Azure websites에 웹 응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-450">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="d1043-451">![게시 프로필 다운로드 웹 사이트](aspnet-mvc-4-models-and-data-access/_static/image37.png "게시 프로필 다운로드 웹 사이트")</span><span class="sxs-lookup"><span data-stu-id="d1043-451">![Downloading the web site publish profile](aspnet-mvc-4-models-and-data-access/_static/image37.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="d1043-452">*게시 프로필 다운로드 웹 사이트*</span><span class="sxs-lookup"><span data-stu-id="d1043-452">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="d1043-453">알려진된 위치에 게시 프로필 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-453">Download the publish profile file to a known location.</span></span> <span data-ttu-id="d1043-454">추가이 연습에서이 파일을 사용 하 여 Visual Studio에서 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하는 방법을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-454">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="d1043-455">![게시 프로필 파일을 저장](aspnet-mvc-4-models-and-data-access/_static/image38.png "게시 프로필 저장")</span><span class="sxs-lookup"><span data-stu-id="d1043-455">![Saving the publish profile file](aspnet-mvc-4-models-and-data-access/_static/image38.png "Saving the publish profile")</span></span>

    <span data-ttu-id="d1043-456">*게시 프로필 파일을 저장 하는 중*</span><span class="sxs-lookup"><span data-stu-id="d1043-456">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="d1043-457">작업 2-데이터베이스 서버 구성</span><span class="sxs-lookup"><span data-stu-id="d1043-457">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="d1043-458">응용 프로그램에서 SQL 서버를 사용할 경우 데이터베이스를 SQL Database 서버 만들기 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-458">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="d1043-459">SQL Server를 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-459">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="d1043-460">응용 프로그램 데이터베이스를 저장 하는 것에 대 한 SQL Database 서버를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-460">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="d1043-461">Windows Azure 관리 포털에서 구독의 SQL Database 서버를 볼 수 있습니다 **Sql Database** | **서버** | **서버 대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-461">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="d1043-462">만든 서버가 없는 경우 하나를 사용 하 여 만들 수 있습니다 합니다 **추가** 명령 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-462">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="d1043-463">기록해는 **서버 이름 및 URL, 관리자 로그인 이름 및 암호**처럼 다음 작업에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-463">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="d1043-464">만들지 마십시오 데이터베이스 아직 이후 단계에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-464">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="d1043-465">![SQL Database 서버 대시보드](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database 서버 대시보드")</span><span class="sxs-lookup"><span data-stu-id="d1043-465">![SQL Database Server Dashboard](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="d1043-466">*SQL Database 서버 대시보드*</span><span class="sxs-lookup"><span data-stu-id="d1043-466">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="d1043-467">다음 태스크에서는 테스트 Visual Studio에서 데이터베이스 연결 서버 목록에 로컬 IP 주소를 포함 해야 하는 이유로 **허용 된 IP 주소**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-467">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="d1043-468">이렇게 하려면 클릭 **구성**에서 IP 주소를 선택 **현재 클라이언트 IP 주소** 에 붙여 넣습니다 합니다 **시작 IP 주소** 및 **끝IP주소** 입력란을 클릭 합니다 ![add-client-ip-address-ok-button](aspnet-mvc-4-models-and-data-access/_static/image40.png) 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-468">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-models-and-data-access/_static/image40.png) button.</span></span>

    ![클라이언트 IP 주소를 추가합니다.](aspnet-mvc-4-models-and-data-access/_static/image41.png)

    <span data-ttu-id="d1043-470">*클라이언트 IP 주소를 추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="d1043-470">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="d1043-471">한 번 합니다 **클라이언트 IP 주소** 허용 된 IP 주소에 추가 됩니다 목록에서 클릭 **저장** 변경을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-471">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![변경 확인](aspnet-mvc-4-models-and-data-access/_static/image42.png)

    <span data-ttu-id="d1043-473">*변경 확인*</span><span class="sxs-lookup"><span data-stu-id="d1043-473">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="d1043-474">작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="d1043-474">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="d1043-475">ASP.NET MVC 4 솔루션 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-475">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="d1043-476">에 **솔루션 탐색기**, 웹 사이트 프로젝트를 마우스 오른쪽 단추로 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-476">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="d1043-477">![응용 프로그램 게시](aspnet-mvc-4-models-and-data-access/_static/image43.png "응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="d1043-477">![Publishing the Application](aspnet-mvc-4-models-and-data-access/_static/image43.png "Publishing the Application")</span></span>

    <span data-ttu-id="d1043-478">*웹 사이트를 게시합니다.*</span><span class="sxs-lookup"><span data-stu-id="d1043-478">*Publishing the web site*</span></span>
2. <span data-ttu-id="d1043-479">첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-479">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="d1043-480">![게시 프로필 가져오기](aspnet-mvc-4-models-and-data-access/_static/image44.png "게시 프로필 가져오기")</span><span class="sxs-lookup"><span data-stu-id="d1043-480">![Importing the publish profile](aspnet-mvc-4-models-and-data-access/_static/image44.png "Importing the publish profile")</span></span>

    <span data-ttu-id="d1043-481">*게시 프로필 가져오기*</span><span class="sxs-lookup"><span data-stu-id="d1043-481">*Importing publish profile*</span></span>
3. <span data-ttu-id="d1043-482">클릭 **연결의 유효성을 검사**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-482">Click **Validate Connection**.</span></span> <span data-ttu-id="d1043-483">유효성 검사가 완료 되 면 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-483">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d1043-484">연결 유효성 검사 단추 옆에 나타나는 녹색 확인 표시가 표시 되 면 유효성 검사가 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-484">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="d1043-485">![연결 유효성 검사](aspnet-mvc-4-models-and-data-access/_static/image45.png "연결 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="d1043-485">![Validating connection](aspnet-mvc-4-models-and-data-access/_static/image45.png "Validating connection")</span></span>

    <span data-ttu-id="d1043-486">*연결 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="d1043-486">*Validating connection*</span></span>
4. <span data-ttu-id="d1043-487">에 **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆의 단추를 클릭 (즉 **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="d1043-487">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="d1043-488">![웹 배포 구성](aspnet-mvc-4-models-and-data-access/_static/image46.png "웹 배포 구성")</span><span class="sxs-lookup"><span data-stu-id="d1043-488">![Web deploy configuration](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web deploy configuration")</span></span>

    <span data-ttu-id="d1043-489">*웹 배포 구성*</span><span class="sxs-lookup"><span data-stu-id="d1043-489">*Web deploy configuration*</span></span>
5. <span data-ttu-id="d1043-490">데이터베이스 연결을 다음과 같이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-490">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="d1043-491">에 **서버 이름** SQL Database 서버 URL 사용 하 여 입력 합니다 *tcp:* 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-491">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="d1043-492">**사용자 이름** 서버 관리자 로그인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-492">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="d1043-493">**암호** 서버 관리자 로그인 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-493">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="d1043-494">새 데이터베이스 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-494">Type a new database name.</span></span>

     <span data-ttu-id="d1043-495">![대상 연결 문자열 구성](aspnet-mvc-4-models-and-data-access/_static/image47.png "대상 연결 문자열 구성")</span><span class="sxs-lookup"><span data-stu-id="d1043-495">![Configuring destination connection string](aspnet-mvc-4-models-and-data-access/_static/image47.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="d1043-496">*대상 연결 문자열 구성*</span><span class="sxs-lookup"><span data-stu-id="d1043-496">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="d1043-497">그런 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-497">Then click **OK**.</span></span> <span data-ttu-id="d1043-498">데이터베이스를 만들라는 메시지가 나오면 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-498">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="d1043-499">![데이터베이스를 만드는](aspnet-mvc-4-models-and-data-access/_static/image48.png "데이터베이스 문자열 만들기")</span><span class="sxs-lookup"><span data-stu-id="d1043-499">![Creating the database](aspnet-mvc-4-models-and-data-access/_static/image48.png "Creating the database string")</span></span>

    <span data-ttu-id="d1043-500">*데이터베이스 만들기*</span><span class="sxs-lookup"><span data-stu-id="d1043-500">*Creating the database*</span></span>
7. <span data-ttu-id="d1043-501">기본 연결 텍스트 상자 내에서 사용 하 여 Windows Azure에서 SQL Database에 연결 하는 연결 문자열 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-501">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="d1043-502">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-502">Then click **Next**.</span></span>

    <span data-ttu-id="d1043-503">![SQL Database를 가리키는 연결 문자열](aspnet-mvc-4-models-and-data-access/_static/image49.png "SQL 데이터베이스를 가리키는 연결 문자열")</span><span class="sxs-lookup"><span data-stu-id="d1043-503">![Connection string pointing to SQL Database](aspnet-mvc-4-models-and-data-access/_static/image49.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="d1043-504">*SQL Database를 가리키는 연결 문자열*</span><span class="sxs-lookup"><span data-stu-id="d1043-504">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="d1043-505">에 **미리 보기** 페이지에서 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-505">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="d1043-506">![웹 응용 프로그램 게시](aspnet-mvc-4-models-and-data-access/_static/image50.png "웹 응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="d1043-506">![Publishing the web application](aspnet-mvc-4-models-and-data-access/_static/image50.png "Publishing the web application")</span></span>

    <span data-ttu-id="d1043-507">*웹 응용 프로그램 게시*</span><span class="sxs-lookup"><span data-stu-id="d1043-507">*Publishing the web application*</span></span>
9. <span data-ttu-id="d1043-508">게시 프로세스가 완료 되 면 게시 된 웹 사이트 기본 브라우저가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-508">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="d1043-509">부록 c: 코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="d1043-509">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="d1043-510">코드 조각을 사용 하 여 결정적인 순간에 필요한 모든 코드를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-510">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="d1043-511">랩 문서가 알려줍니다 정확 하 게 사용할 수 있는 시기를 다음 그림과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-511">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="d1043-512">![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드를 삽입할](aspnet-mvc-4-models-and-data-access/_static/image51.png "프로젝트에 코드를 삽입 하는 Visual Studio를 사용 하 여 코드 조각을")</span><span class="sxs-lookup"><span data-stu-id="d1043-512">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-models-and-data-access/_static/image51.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="d1043-513">*프로젝트에 코드를 삽입 하려면 Visual Studio 코드 조각 사용*</span><span class="sxs-lookup"><span data-stu-id="d1043-513">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="d1043-514">***키보드 (C#만 해당)를 사용 하 여 코드 조각을 추가 하려면***</span><span class="sxs-lookup"><span data-stu-id="d1043-514">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="d1043-515">코드를 삽입 하려는 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-515">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="d1043-516">시작 (공백 없이 하이픈) 조각 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-516">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="d1043-517">IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-517">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="d1043-518">올바른 코드 조각을 선택 합니다 (또는 전체 코드 조각 이름을 선택 될 때까지 입력 유지).</span><span class="sxs-lookup"><span data-stu-id="d1043-518">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="d1043-519">커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-519">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="d1043-520">![코드 조각 이름을 입력](aspnet-mvc-4-models-and-data-access/_static/image52.png "조각 이름을 입력 하기 시작")</span><span class="sxs-lookup"><span data-stu-id="d1043-520">![Start typing the snippet name](aspnet-mvc-4-models-and-data-access/_static/image52.png "Start typing the snippet name")</span></span>

<span data-ttu-id="d1043-521">*코드 조각 이름을 입력 하기 시작*</span><span class="sxs-lookup"><span data-stu-id="d1043-521">*Start typing the snippet name*</span></span>

<span data-ttu-id="d1043-522">![Tab 키를 눌러 강조 표시 된 코드 조각을](aspnet-mvc-4-models-and-data-access/_static/image53.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")</span><span class="sxs-lookup"><span data-stu-id="d1043-522">![Press Tab to select the highlighted snippet](aspnet-mvc-4-models-and-data-access/_static/image53.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="d1043-523">*Tab 키를 눌러 강조 표시 된 코드 조각 선택*</span><span class="sxs-lookup"><span data-stu-id="d1043-523">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="d1043-524">![Tab 키를 다시 코드 조각 확장 됩니다](aspnet-mvc-4-models-and-data-access/_static/image54.png "다시 Tab 키를 누릅니다 하 고 코드 조각에서는 확장")</span><span class="sxs-lookup"><span data-stu-id="d1043-524">![Press Tab again and the snippet will expand](aspnet-mvc-4-models-and-data-access/_static/image54.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="d1043-525">*Tab 키를 다시 및 코드 조각에서는 확장*</span><span class="sxs-lookup"><span data-stu-id="d1043-525">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="d1043-526">***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가할*** 1입니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-526">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="d1043-527">코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-527">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="d1043-528">선택 **코드 조각 삽입** 뒤 **내 코드 조각**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-528">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="d1043-529">클릭 하 여 목록에서 관련 코드 조각을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1043-529">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="d1043-530">![코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭](aspnet-mvc-4-models-and-data-access/_static/image55.png "코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭")</span><span class="sxs-lookup"><span data-stu-id="d1043-530">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-models-and-data-access/_static/image55.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="d1043-531">*코드 조각을 삽입할 선택한 코드 조각 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭*</span><span class="sxs-lookup"><span data-stu-id="d1043-531">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="d1043-532">![클릭 하 여 목록에서 관련 코드 조각 선택](aspnet-mvc-4-models-and-data-access/_static/image56.png "클릭 하 여 목록에서 관련 코드 조각 선택")</span><span class="sxs-lookup"><span data-stu-id="d1043-532">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-models-and-data-access/_static/image56.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="d1043-533">*클릭 하 여 목록에서 관련 코드 조각 선택*</span><span class="sxs-lookup"><span data-stu-id="d1043-533">*Pick the relevant snippet from the list, by clicking on it*</span></span>
