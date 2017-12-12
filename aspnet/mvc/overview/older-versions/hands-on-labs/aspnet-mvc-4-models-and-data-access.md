---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
title: "ASP.NET MVC 4 모델 및 데이터 액세스 | Microsoft Docs"
author: rick-anderson
description: "참고:이 실습 랩 ASP.NET MVC에 대 한 기본 지식이 있다고 가정 합니다. 하기 전에 ASP.NET MVC를 사용 하지 않은 경우 좋습니다 ASP.NET MVC 4를 초과할 수 있습니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 634ea84b-f904-4afe-b71b-49cccef4d9cc
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
msc.type: authoredcontent
ms.openlocfilehash: bf4bb5c6f9ad8339c3597b0d6666c7077ac476e0
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-mvc-4-models-and-data-access"></a><span data-ttu-id="043ba-104">ASP.NET MVC 4 모델 및 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="043ba-104">ASP.NET MVC 4 Models and Data Access</span></span>
====================
<span data-ttu-id="043ba-105">으로 [웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="043ba-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> [!NOTE]
> <span data-ttu-id="043ba-106">이 실습 랩 대 한 기본 지식이 있다고 가정 하 고 **ASP.NET MVC**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-106">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="043ba-107">사용 하지 않은 경우 **ASP.NET MVC** 를 권장 앞, **ASP.NET MVC 4 기초** 실습 랩입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-107">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>
> 
> <span data-ttu-id="043ba-108">이 랩에서 원본 폴더에 제공 된 샘플 웹 응용 프로그램에 사소한 변경 내용을 적용 하 여 이전에 설명 된 새로운 기능 및 향상 된 기능을 통해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-108">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>
> 
> <span data-ttu-id="043ba-109">모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [https://www.microsoft.com/en-us/download/29843](https://www.microsoft.com/en-us/download/29843)합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-109">All sample code and snippets are included in the Web Camps Training Kit, available at [https://www.microsoft.com/en-us/download/29843](https://www.microsoft.com/en-us/download/29843).</span></span>


<span data-ttu-id="043ba-110">**ASP.NET MVC의 기본 사항** 실습 랩 있습니다 전달 했기 하드 코드 된 데이터는 컨트롤러에서 템플릿 보기에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-110">In **ASP.NET MVC Fundamentals** Hands-on Lab, you have been passing hard-coded data from the Controllers to the View templates.</span></span> <span data-ttu-id="043ba-111">그러나 실제 웹 응용 프로그램을 작성 하기 위해 실제 데이터베이스를 사용 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-111">But, in order to build a real Web application, you might want to use a real database.</span></span>

<span data-ttu-id="043ba-112">이 실습 랩 음악 스토어 응용 프로그램에 필요한 데이터 저장 및 검색 하기 위해 데이터베이스 엔진을 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-112">This Hands-on Lab will show you how to use a database engine in order to store and retrieve the data needed for the Music Store application.</span></span> <span data-ttu-id="043ba-113">이를 위해 기존 데이터베이스를 시작 쿼리하고에서 엔터티 데이터 모델을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-113">To accomplish that, you will start with an existing database and create the Entity Data Model from it.</span></span> <span data-ttu-id="043ba-114">이 랩의 경우 전체에서 해결할 지는 **Database First** 접근 방식으로 **Code First** 접근 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-114">Throughout this lab, you will meet the **Database First** approach as well as the **Code First** approach.</span></span>

<span data-ttu-id="043ba-115">그러나 사용할 수도 있습니다는 **Model First** 접근 방식, 도구를 사용 하는 동일한 모델을 만들 및 다음에서 데이터베이스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-115">However, you can also use the **Model First** approach, create the same model using the tools, and then generate the database from it.</span></span>

<span data-ttu-id="043ba-116">![데이터베이스의 첫 번째 vs입니다. 첫 번째 모델](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs. 먼저 모델")</span><span class="sxs-lookup"><span data-stu-id="043ba-116">![Database First vs. Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs. Model First")</span></span>

<span data-ttu-id="043ba-117">*데이터베이스의 첫 번째 vs입니다. 먼저 모델*</span><span class="sxs-lookup"><span data-stu-id="043ba-117">*Database First vs. Model First*</span></span>

<span data-ttu-id="043ba-118">모델을 생성 하 고 나면 StoreController 하드 코드 된 데이터를 사용 하는 대신 데이터베이스에서 가져온 데이터와 함께 저장소 보기를 제공 하기에 적절 한 조정 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-118">After generating the Model, you will make the proper adjustments in the StoreController to provide the Store Views with the data taken from the database, instead of using hard-coded data.</span></span> <span data-ttu-id="043ba-119">어떠한 변경 템플릿 보기에는 StoreController 반품할 동일한 Viewmodel 보기 템플릿 때문에이 시간 데이터가 데이터베이스에서 나올지 있지만 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-119">You will not need to make any change to the View templates because the StoreController will be returning the same ViewModels to the View templates, although this time the data will come from the database.</span></span>

<span data-ttu-id="043ba-120">**코드의 첫 번째 방법인**</span><span class="sxs-lookup"><span data-stu-id="043ba-120">**The Code First Approach**</span></span>

<span data-ttu-id="043ba-121">Code First 접근 방식은 일반적으로 프레임 워크와 연결 되어 있는 클래스를 생성 하지 않고 코드에서 모델을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-121">The Code First approach allows us to define the model from the code without generating classes that are generally coupled with the framework.</span></span>

<span data-ttu-id="043ba-122">코드에서 먼저, 모델 개체도 정의 됩니다 POCOs, &quot;일반 이전 CLR 개체&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-122">In code first, model objects are defined with POCOs, &quot;Plain Old CLR Objects&quot;.</span></span> <span data-ttu-id="043ba-123">POCOs는 간단한 일반 클래스 없는 상속을 포함 하 고 인터페이스를 구현 하지 않는입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-123">POCOs are simple plain classes that have no inheritance and do not implement interfaces.</span></span> <span data-ttu-id="043ba-124">데이터베이스에서, 자동으로 생성할 수 또는 기존 데이터베이스를 코드에서 클래스 매핑을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-124">We can automatically generate the database from them, or we can use an existing database and generate the class mapping from the code.</span></span>

<span data-ttu-id="043ba-125">이 접근 방식을 사용의 이점에는 모델 유지 됩니다 (이 경우 Entity Framework)의 지 속성 프레임 워크와 독립적인 POCOs 클래스 매핑 프레임 워크와 연결 되어 있지는입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-125">The benefits of using this approach is that the Model remains independent from the persistence framework (in this case, Entity Framework), as the POCOs classes are not coupled with the mapping framework.</span></span>

> [!NOTE]
> <span data-ttu-id="043ba-126">이 랩에서 ASP.NET MVC 4에 근거 하며 버전 Music Store 샘플 응용 프로그램의 사용자 지정 하 고이 실습 랩에 표시 된 기능에 맞게 최소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-126">This Lab is based on ASP.NET MVC 4 and a version of the Music Store sample application customized and minimized to fit only the features shown in this Hands-On Lab.</span></span>
> 
> <span data-ttu-id="043ba-127">전체 탐색 하려는 경우 **Music Store** 자습서 응용 프로그램에서 찾을 수 [MVC 음악 저장소](https://github.com/evilDave/MVC-Music-Store)합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-127">If you wish to explore the whole **Music Store** tutorial application you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>


<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="043ba-128">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="043ba-128">Prerequisites</span></span>

<span data-ttu-id="043ba-129">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-129">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="043ba-130">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽기 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).</span><span class="sxs-lookup"><span data-stu-id="043ba-130">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="043ba-131">설정</span><span class="sxs-lookup"><span data-stu-id="043ba-131">Setup</span></span>

<span data-ttu-id="043ba-132">**설치 하는 코드 조각**</span><span class="sxs-lookup"><span data-stu-id="043ba-132">**Installing Code Snippets**</span></span>

<span data-ttu-id="043ba-133">편의 위해는이 랩에 따라 관리 코드의 대부분 Visual Studio 코드 조각 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-133">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="043ba-134">실행 코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-134">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="043ba-135">이 문서에서 부록을 참조할 수 사용 하는 방법에 알아봅니다 사용 하 고 Visual Studio 코드 조각에 익숙한 경우 &quot; [부록 c:를 사용 하 여 코드 조각을](#AppendixC)&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-135">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="043ba-136">연습</span><span class="sxs-lookup"><span data-stu-id="043ba-136">Exercises</span></span>

<span data-ttu-id="043ba-137">이 실습 랩에서 다음 연습으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-137">This Hands-on Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="043ba-138">연습 1: 데이터베이스 추가</span><span class="sxs-lookup"><span data-stu-id="043ba-138">Exercise 1: Adding a Database</span></span>](#Exercise1)
2. [<span data-ttu-id="043ba-139">연습 2: Code First를 사용 하 여 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="043ba-139">Exercise 2: Creating a Database using Code First</span></span>](#Exercise2)
3. [<span data-ttu-id="043ba-140">매개 변수를 사용 하 여 데이터베이스를 쿼리 하는 연습 3:</span><span class="sxs-lookup"><span data-stu-id="043ba-140">Exercise 3: Querying the Database with Parameters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="043ba-141">각 연습 동반 되는 **끝** 연습을 완료 한 후 가져와야 생성 되는 솔루션에 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-141">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="043ba-142">연습을 통해 작업 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-142">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="043ba-143">예상 소요 시간: **35 분**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-143">Estimated time to complete this lab: **35 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Adding_a_Database"></a>
### <a name="exercise-1-adding-a-database"></a><span data-ttu-id="043ba-144">연습 1: 데이터베이스 추가</span><span class="sxs-lookup"><span data-stu-id="043ba-144">Exercise 1: Adding a Database</span></span>

<span data-ttu-id="043ba-145">이 연습에서는 해당 데이터를 처리 하기 위해 솔루션에 MusicStore 응용 프로그램의 테이블이 포함 된 데이터베이스를 추가 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-145">In this exercise, you will learn how to add a database with the tables of the MusicStore application to the solution in order to consume its data.</span></span> <span data-ttu-id="043ba-146">데이터베이스 모델을 사용 하 여 생성 되 고 솔루션에 추가 되 면 하드 코드 된 값을 사용 하는 대신 데이터베이스에서 가져온 데이터와 함께 템플릿 보기를 제공 하기 위해 StoreController 클래스를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-146">Once the database is generated with the model, and added to the solution, you will modify the StoreController class to provide the View template with the data taken from the database, instead of using hard-coded values.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Adding_a_Database"></a>
#### <a name="task-1---adding-a-database"></a><span data-ttu-id="043ba-147">작업 1-데이터베이스 추가</span><span class="sxs-lookup"><span data-stu-id="043ba-147">Task 1 - Adding a Database</span></span>

<span data-ttu-id="043ba-148">이 작업에서는 솔루션 MusicStore 응용 프로그램의 주 테이블을 사용 하 여 이미 생성된 된 데이터베이스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-148">In this task, you will add an already created database with the main tables of the MusicStore application to the solution.</span></span>

1. <span data-ttu-id="043ba-149">열기는 **시작** 솔루션에 있는 **소스/e x 1-AddingADatabaseDBFirst/시작/** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-149">Open the **Begin** solution located at **Source/Ex1-AddingADatabaseDBFirst/Begin/** folder.</span></span>

    1. <span data-ttu-id="043ba-150">일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 전에 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-150">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="043ba-151">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-151">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="043ba-152">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="043ba-152">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="043ba-153">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-153">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="043ba-154">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-154">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="043ba-155">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-155">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="043ba-156">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-156">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="043ba-157">추가 **MvcMusicStore** 데이터베이스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-157">Add **MvcMusicStore** database file.</span></span> <span data-ttu-id="043ba-158">이 실습 랩을 사용 하 여 호출 하는 이미 만들어진된 데이터베이스 **MvcMusicStore.mdf**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-158">In this Hands-on Lab, you will use an already created database called **MvcMusicStore.mdf**.</span></span> <span data-ttu-id="043ba-159">이렇게 하려면 마우스 오른쪽 단추로 클릭 **앱\_데이터** 폴더를 가리키도록 **추가** 클릭 하 고 **기존 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-159">To do that, right-click **App\_Data** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="043ba-160">찾아 **\Source\Assets** 선택 하 고는 **MvcMusicStore.mdf** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-160">Browse to **\Source\Assets** and select the **MvcMusicStore.mdf** file.</span></span>

    <span data-ttu-id="043ba-161">![기존 항목 추가](aspnet-mvc-4-models-and-data-access/_static/image2.png "기존 항목 추가")</span><span class="sxs-lookup"><span data-stu-id="043ba-161">![Adding an Existing Item](aspnet-mvc-4-models-and-data-access/_static/image2.png "Adding an Existing Item")</span></span>

    <span data-ttu-id="043ba-162">*기존 항목 추가*</span><span class="sxs-lookup"><span data-stu-id="043ba-162">*Adding an Existing Item*</span></span>

    <span data-ttu-id="043ba-163">![데이터베이스 파일 MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore.mdf 데이터베이스 파일")</span><span class="sxs-lookup"><span data-stu-id="043ba-163">![MvcMusicStore.mdf database file](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore.mdf database file")</span></span>

    <span data-ttu-id="043ba-164">*MvcMusicStore.mdf 데이터베이스 파일*</span><span class="sxs-lookup"><span data-stu-id="043ba-164">*MvcMusicStore.mdf database file*</span></span>

    <span data-ttu-id="043ba-165">데이터베이스는 프로젝트에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-165">The database has been added to the project.</span></span> <span data-ttu-id="043ba-166">솔루션 내에서 데이터베이스가 하는 경우에 쿼리 하 고 다른 데이터베이스 서버에서 호스트 되는 대로 업데이트 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-166">Even when the database is located inside the solution, you can query and update it as it was hosted in a different database server.</span></span>

    <span data-ttu-id="043ba-167">![솔루션 탐색기에서 데이터베이스 MvcMusicStore](aspnet-mvc-4-models-and-data-access/_static/image4.png "솔루션 탐색기에서 MvcMusicStore 데이터베이스")</span><span class="sxs-lookup"><span data-stu-id="043ba-167">![MvcMusicStore database in Solution Explorer](aspnet-mvc-4-models-and-data-access/_static/image4.png "MvcMusicStore database in Solution Explorer")</span></span>

    <span data-ttu-id="043ba-168">*솔루션 탐색기에서 MvcMusicStore 데이터베이스*</span><span class="sxs-lookup"><span data-stu-id="043ba-168">*MvcMusicStore database in Solution Explorer*</span></span>
3. <span data-ttu-id="043ba-169">데이터베이스에 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-169">Verify the connection to the database.</span></span> <span data-ttu-id="043ba-170">이 작업을 수행 하려면 두 번 클릭 **MvcMusicStore.mdf** 는 연결을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-170">To do this, double-click **MvcMusicStore.mdf** to establish a connection.</span></span>

    <span data-ttu-id="043ba-171">![MvcMusicStore.mdf 연결할](aspnet-mvc-4-models-and-data-access/_static/image5.png "MvcMusicStore.mdf에 연결")</span><span class="sxs-lookup"><span data-stu-id="043ba-171">![Connecting to MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "Connecting to MvcMusicStore.mdf")</span></span>

    <span data-ttu-id="043ba-172">*MvcMusicStore.mdf에 연결*</span><span class="sxs-lookup"><span data-stu-id="043ba-172">*Connecting to MvcMusicStore.mdf*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_a_Data_Model"></a>
#### <a name="task-2---creating-a-data-model"></a><span data-ttu-id="043ba-173">작업 2-데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="043ba-173">Task 2 - Creating a Data Model</span></span>

<span data-ttu-id="043ba-174">이 작업에서는 이전 태스크에서 추가 데이터베이스와 상호 작용 하는 데이터 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-174">In this task, you will create a data model to interact with the database added in the previous task.</span></span>

1. <span data-ttu-id="043ba-175">데이터베이스를 나타내는 데이터 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-175">Create a data model that will represent the database.</span></span> <span data-ttu-id="043ba-176">솔루션 탐색기 오른쪽 클릭에서이 작업을 수행 하는 **모델** 폴더를 가리키도록 **추가** 클릭 하 고 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-176">To do this, in Solution Explorer right-click the **Models** folder, point to **Add** and then click **New Item**.</span></span> <span data-ttu-id="043ba-177">에 **새 항목 추가** 대화 상자에서는 **데이터** 템플릿을 차례로 **ADO.NET 엔터티 데이터 모델** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-177">In the **Add New Item** dialog, select the **Data** template and then the **ADO.NET Entity Data Model** item.</span></span> <span data-ttu-id="043ba-178">데이터 모델 이름을 **StoreDB.edmx** 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-178">Change the data model name to **StoreDB.edmx** and click **Add**.</span></span>

    <span data-ttu-id="043ba-179">![StoreDB ADO.NET 엔터티 데이터 모델 추가](aspnet-mvc-4-models-and-data-access/_static/image6.png "StoreDB ADO.NET 엔터티 데이터 모델 추가")</span><span class="sxs-lookup"><span data-stu-id="043ba-179">![Adding the StoreDB ADO.NET Entity Data Model](aspnet-mvc-4-models-and-data-access/_static/image6.png "Adding the StoreDB ADO.NET Entity Data Model")</span></span>

    <span data-ttu-id="043ba-180">*StoreDB ADO.NET 엔터티 데이터 모델 추가*</span><span class="sxs-lookup"><span data-stu-id="043ba-180">*Adding the StoreDB ADO.NET Entity Data Model*</span></span>
2. <span data-ttu-id="043ba-181">**엔터티 데이터 모델 마법사** 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-181">The **Entity Data Model Wizard** will appear.</span></span> <span data-ttu-id="043ba-182">이 마법사에서는 모델 계층을 만드는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-182">This wizard will guide you through the creation of the model layer.</span></span> <span data-ttu-id="043ba-183">선택 모델 만들어야 할 추가 기존 데이터베이스 recentyl에 따라 이후 **데이터베이스에서 생성** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-183">Since the model should be created based on the existing database recentyl added, select **Generate from database** and click **Next**.</span></span>

    <span data-ttu-id="043ba-184">![모델 콘텐츠 선택](aspnet-mvc-4-models-and-data-access/_static/image7.png "모델 콘텐츠 선택")</span><span class="sxs-lookup"><span data-stu-id="043ba-184">![Choosing the model content](aspnet-mvc-4-models-and-data-access/_static/image7.png "Choosing the model content")</span></span>

    <span data-ttu-id="043ba-185">*모델 콘텐츠 선택*</span><span class="sxs-lookup"><span data-stu-id="043ba-185">*Choosing the model content*</span></span>
3. <span data-ttu-id="043ba-186">데이터베이스에서 모델을 생성 하는 이후 사용에 대 한 연결을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-186">Since you are generating a model from a database, you will need to specify the connection to use.</span></span> <span data-ttu-id="043ba-187">클릭 **새 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-187">Click **New Connection**.</span></span>
4. <span data-ttu-id="043ba-188">선택 **Microsoft SQL Server 데이터베이스 파일** 클릭 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-188">Select **Microsoft SQL Server Database File** and click **Continue**.</span></span>

    <span data-ttu-id="043ba-189">![데이터 원본 선택](aspnet-mvc-4-models-and-data-access/_static/image8.png "데이터 원본 선택")</span><span class="sxs-lookup"><span data-stu-id="043ba-189">![Choose data source](aspnet-mvc-4-models-and-data-access/_static/image8.png "Choose data source")</span></span>

    <span data-ttu-id="043ba-190">*데이터 원본 대화 상자를 선택 합니다.*</span><span class="sxs-lookup"><span data-stu-id="043ba-190">*Choose data source dialog*</span></span>
5. <span data-ttu-id="043ba-191">클릭 **찾아보기** 데이터베이스를 선택 하 고 **MvcMusicStore.mdf** 에 있는 **앱\_데이터** 폴더 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-191">Click **Browse** and select the database **MvcMusicStore.mdf** you located in the **App\_Data** folder and click **OK**.</span></span>

    <span data-ttu-id="043ba-192">![연결 속성](aspnet-mvc-4-models-and-data-access/_static/image9.png "연결 속성")</span><span class="sxs-lookup"><span data-stu-id="043ba-192">![Connection properties](aspnet-mvc-4-models-and-data-access/_static/image9.png "Connection properties")</span></span>

    <span data-ttu-id="043ba-193">*연결 속성*</span><span class="sxs-lookup"><span data-stu-id="043ba-193">*Connection properties*</span></span>
6. <span data-ttu-id="043ba-194">생성 된 클래스 엔터티 연결 문자열 이름이 같은, 따라서 해당 이름을 변경 해야 **MusicStoreEntities** 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-194">The generated class should have the same name as the entity connection string, so change its name to **MusicStoreEntities** and click **Next**.</span></span>

    <span data-ttu-id="043ba-195">![데이터 연결 선택](aspnet-mvc-4-models-and-data-access/_static/image10.png "데이터 연결 선택")</span><span class="sxs-lookup"><span data-stu-id="043ba-195">![Choosing the data connection](aspnet-mvc-4-models-and-data-access/_static/image10.png "Choosing the data connection")</span></span>

    <span data-ttu-id="043ba-196">*데이터 연결 선택*</span><span class="sxs-lookup"><span data-stu-id="043ba-196">*Choosing the data connection*</span></span>
7. <span data-ttu-id="043ba-197">데이터베이스 개체를 사용 하 여 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-197">Choose the database objects to use.</span></span> <span data-ttu-id="043ba-198">엔터티 모델만 데이터베이스의 테이블을 사용 하는 경우 선택 된 **테이블** 옵션을 선택한 다음 사항을 확인는 **모델에 외래 키 열을 포함할** 및 **복수화 또는 단 수 화 생성 개체 이름** 옵션 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-198">As the Entity Model will use just the database's tables, select the **Tables** option, and make sure that the **Include foreign key columns in the model** and **Pluralize or singularize generated object names** options are also selected.</span></span> <span data-ttu-id="043ba-199">변경 하려면 모델 Namespace **MvcMusicStore.Model** 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-199">Change the Model Namespace to **MvcMusicStore.Model** and click **Finish**.</span></span>

    <span data-ttu-id="043ba-200">![데이터베이스 개체 선택](aspnet-mvc-4-models-and-data-access/_static/image11.png "데이터베이스 개체 선택")</span><span class="sxs-lookup"><span data-stu-id="043ba-200">![Choosing the database objects](aspnet-mvc-4-models-and-data-access/_static/image11.png "Choosing the database objects")</span></span>

    <span data-ttu-id="043ba-201">*데이터베이스 개체 선택*</span><span class="sxs-lookup"><span data-stu-id="043ba-201">*Choosing the database objects*</span></span>

    > [!NOTE]
    > <span data-ttu-id="043ba-202">보안 경고 대화 상자가 표시 되 면 클릭 **확인** 하 여 템플릿을 실행 하 고 모델 엔터티에 대 한 클래스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-202">If a Security Warning dialog is shown, click **OK** to run the template and generate the classes for the model entities.</span></span>
8. <span data-ttu-id="043ba-203">데이터베이스에 각 테이블을 매핑하는 별도 클래스를 만들 수는 동안 데이터베이스는 엔터티 다이어그램이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-203">An entity diagram for the database will appear, while a separate class that maps each table to the database will be created.</span></span> <span data-ttu-id="043ba-204">예를 들어는 **앨범** 테이블으로 표현 됩니다는 **앨범** 클래스, 클래스 속성 테이블의 각 열이 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-204">For example, the **Albums** table will be represented by an **Album** class, where each column in the table will map to a class property.</span></span> <span data-ttu-id="043ba-205">이렇게 하면 쿼리 및 데이터베이스의 행을 나타내는 개체를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-205">This will allow you to query and work with objects that represent rows in the database.</span></span>

    <span data-ttu-id="043ba-206">![엔터티 다이어그램](aspnet-mvc-4-models-and-data-access/_static/image12.png "엔터티 다이어그램")</span><span class="sxs-lookup"><span data-stu-id="043ba-206">![Entity diagram](aspnet-mvc-4-models-and-data-access/_static/image12.png "Entity diagram")</span></span>

    <span data-ttu-id="043ba-207">*엔터티 다이어그램*</span><span class="sxs-lookup"><span data-stu-id="043ba-207">*Entity diagram*</span></span>

> [!NOTE]
> <span data-ttu-id="043ba-208">T4 템플릿 (.tt) 엔터티 클래스를 생성 하는 코드를 실행 하 고 같은 이름의 기존 클래스를 덮어쓰게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-208">The T4 templates (.tt) run code to generate the entities classes and will overwrite the existing classes with the same name.</span></span> <span data-ttu-id="043ba-209">이 예제에서는 클래스 &quot;앨범&quot;, &quot;장르&quot; 및 &quot;아티스트&quot; 생성 된 코드와 덮어쓴 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-209">In this example, the classes &quot;Album&quot;, &quot;Genre&quot; and &quot;Artist&quot; were overwritten with the generated code.</span></span>


<a id="Ex1Task3"></a>

<a id="Task_3_-_Building_the_Application"></a>
#### <a name="task-3---building-the-application"></a><span data-ttu-id="043ba-210">작업 3-응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="043ba-210">Task 3 - Building the Application</span></span>

<span data-ttu-id="043ba-211">이 작업을 검사 해야는 모델 생성이 제거 되지만 **앨범**, **장르** 및 **아티스트** 모델 클래스는 프로젝트 빌드 성공적으로 사용 하 여 새 데이터 모델 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-211">In this task, you will check that, although the model generation have removed the **Album**, **Genre** and **Artist** model classes, the project builds successfully by using the new data model classes.</span></span>

1. <span data-ttu-id="043ba-212">선택 하 여 프로젝트를 빌드합니다는 **빌드** 메뉴 항목 차례로 **빌드 MvcMusicStore**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-212">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="043ba-213">![프로젝트를 빌드하면](aspnet-mvc-4-models-and-data-access/_static/image13.png "프로젝트 빌드")</span><span class="sxs-lookup"><span data-stu-id="043ba-213">![Building the project](aspnet-mvc-4-models-and-data-access/_static/image13.png "Building the project")</span></span>

    <span data-ttu-id="043ba-214">*프로젝트 빌드*</span><span class="sxs-lookup"><span data-stu-id="043ba-214">*Building the project*</span></span>
2. <span data-ttu-id="043ba-215">프로젝트가는 성공적으로 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-215">The project builds successfully.</span></span> <span data-ttu-id="043ba-216">이유 여전히 작동 합니까?</span><span class="sxs-lookup"><span data-stu-id="043ba-216">Why does it still work?</span></span> <span data-ttu-id="043ba-217">데이터베이스 테이블에 있는 필드를 제거 하는 클래스에 사용 된 속성을 포함 하기 때문에 작동 **앨범** 및 **장르**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-217">It works because the database tables have fields that include the properties that you were using in the removed classes **Album** and **Genre**.</span></span>

    <span data-ttu-id="043ba-218">![빌드 성공](aspnet-mvc-4-models-and-data-access/_static/image14.png "빌드 성공")</span><span class="sxs-lookup"><span data-stu-id="043ba-218">![Builds succeeded](aspnet-mvc-4-models-and-data-access/_static/image14.png "Builds succeeded")</span></span>

    <span data-ttu-id="043ba-219">*빌드 성공*</span><span class="sxs-lookup"><span data-stu-id="043ba-219">*Builds succeeded*</span></span>
3. <span data-ttu-id="043ba-220">엔터티를 다이어그램 형태로 표시 하는 디자이너, C# 클래스는 실제로 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-220">While the designer displays the entities in a diagram format, they are really C# classes.</span></span> <span data-ttu-id="043ba-221">확장의 **StoreDB.edmx** 솔루션 탐색기에서 노드 차례로 **StoreDB.tt**생성된 한 새 엔터티 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-221">Expand the **StoreDB.edmx** node in the Solution Explorer and then **StoreDB.tt**, you will see the new generated entities.</span></span>

    <span data-ttu-id="043ba-222">![생성 된 파일](aspnet-mvc-4-models-and-data-access/_static/image15.png "생성 된 파일")</span><span class="sxs-lookup"><span data-stu-id="043ba-222">![Generated files](aspnet-mvc-4-models-and-data-access/_static/image15.png "Generated files")</span></span>

    <span data-ttu-id="043ba-223">*생성 된 파일*</span><span class="sxs-lookup"><span data-stu-id="043ba-223">*Generated files*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="043ba-224">작업 4-데이터베이스 쿼리</span><span class="sxs-lookup"><span data-stu-id="043ba-224">Task 4 - Querying the Database</span></span>

<span data-ttu-id="043ba-225">이 태스크에서는 하드 코드 된 데이터를 사용 하는 대신 쿼리 하는 데이터베이스 정보를 검색할 수 있도록 StoreController 클래스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-225">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will query the database to retrieve the information.</span></span>

1. <span data-ttu-id="043ba-226">열기 **Controllers\StoreController.cs** 의 인스턴스를 저장 하는 클래스에 다음 필드를 추가 하 고는 **MusicStoreEntities** 라는 클래스를 **storeDB**:</span><span class="sxs-lookup"><span data-stu-id="043ba-226">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="043ba-227">(코드 조각- *모델 데이터 액세스 및-e x 1 storeDB*)</span><span class="sxs-lookup"><span data-stu-id="043ba-227">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample1.cs)]
2. <span data-ttu-id="043ba-228">**MusicStoreEntities** 클래스는 데이터베이스의 각 테이블에 대 한 컬렉션 속성을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-228">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="043ba-229">업데이트 **찾아보기** 모든 장르를 가져오려는 작업 메서드는 **앨범**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-229">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="043ba-230">(코드 조각- *모델 및 데이터 액세스-e x 1 저장소 찾아보기*)</span><span class="sxs-lookup"><span data-stu-id="043ba-230">(Code Snippet - *Models And Data Access - Ex1 Store Browse*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample2.cs)]

    > [!NOTE]
    > <span data-ttu-id="043ba-231">.NET 호출의 기능을 사용 하는 **LINQ** 프로그래밍할 수 있습니다 (통합 언어 쿼리)-이 데이터베이스에 대해 코드를 실행 하 고 반환 하는 이러한 컬렉션에 대 한 강력한 형식의 쿼리 식을 작성 하 개체 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-231">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="043ba-232">LINQ에 대 한 자세한 내용은 참조 하십시오는 [msdn 사이트](https://msdn.microsoft.com/en-us/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-232">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/en-us/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx).</span></span>
3. <span data-ttu-id="043ba-233">업데이트 **인덱스** 동작 메서드를 모든 장르를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-233">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="043ba-234">(코드 조각- *모델 및 데이터 액세스-e x 1 저장소 인덱스*)</span><span class="sxs-lookup"><span data-stu-id="043ba-234">(Code Snippet - *Models And Data Access - Ex1 Store Index*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample3.cs)]
4. <span data-ttu-id="043ba-235">업데이트 **인덱스** 동작 메서드의 모든 장르를 검색 하 고 목록에 컬렉션을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-235">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="043ba-236">(코드 조각- *모델 및 데이터 액세스-e x 1 저장소 GenreMenu*)</span><span class="sxs-lookup"><span data-stu-id="043ba-236">(Code Snippet - *Models And Data Access - Ex1 Store GenreMenu*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample4.cs)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="043ba-237">5-응용 프로그램 실행 작업</span><span class="sxs-lookup"><span data-stu-id="043ba-237">Task 5 - Running the Application</span></span>

<span data-ttu-id="043ba-238">이 작업에서는 저장소 인덱스 페이지에 하드 코드 된 것 대신 데이터베이스에 저장 된 장르 표시 이제 됩니다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-238">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="043ba-239">하기 때문에 템플릿 보기를 변경할 필요가 없습니다는 **StoreController** 되는 동일한 엔터티 반환 이전 처럼 있지만이 이번 데이터 데이터베이스에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-239">There is no need to change the View template because the **StoreController** is returning the same entities as before, although this time the data will come from the database.</span></span>

1. <span data-ttu-id="043ba-240">솔루션 및 키를 눌러 다시 빌드 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-240">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="043ba-241">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-241">The project starts in the Home page.</span></span> <span data-ttu-id="043ba-242">확인의 메뉴 **장르** 는 더 이상 하드 코드 된 목록 및 데이터는 데이터베이스에서 직접 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-242">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image16.png)

    <span data-ttu-id="043ba-244">*데이터베이스에서 검색 장르*</span><span class="sxs-lookup"><span data-stu-id="043ba-244">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="043ba-245">이제 모든 장르로 이동 하 고 데이터베이스에서 앨범 채워집니다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-245">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="043ba-246">![데이터베이스에서 앨범 검색](aspnet-mvc-4-models-and-data-access/_static/image17.png "앨범을 데이터베이스에서 검색")</span><span class="sxs-lookup"><span data-stu-id="043ba-246">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image17.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="043ba-247">*데이터베이스에서 검색 앨범*</span><span class="sxs-lookup"><span data-stu-id="043ba-247">*Browsing Albums from the database*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Database_Using_Code_First"></a>
### <a name="exercise-2-creating-a-database-using-code-first"></a><span data-ttu-id="043ba-248">연습 2: 먼저 코드를 사용 하 여 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="043ba-248">Exercise 2: Creating a Database Using Code First</span></span>

<span data-ttu-id="043ba-249">이 연습에서는 MusicStore 응용 프로그램의 테이블을 사용 하 여 데이터베이스를 만들려면 Code First 접근 방식을 사용 하는 방법과 해당 데이터를 액세스 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-249">In this exercise, you will learn how to use the Code First approach to create a database with the tables of the MusicStore application, and how to access its data.</span></span>

<span data-ttu-id="043ba-250">모델 생성 되 면에 하드 코드 된 값을 사용 하는 대신 데이터베이스에서 가져온 데이터 템플릿 보기를 제공 하려면 StoreController 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-250">Once the model is generated, you will modify the StoreController to provide the View template with the data taken from the database, instead of using hardcoded values.</span></span>

> [!NOTE]
> <span data-ttu-id="043ba-251">연습 1 완료 이미 Database First 접근 방식으로 작업을 수행 하는 경우 이제 다른 프로세스와 동일한 결과를 얻는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-251">If you have completed Exercise 1 and have already worked with the Database First approach, you will now learn how to get the same results with a different process.</span></span> <span data-ttu-id="043ba-252">연습 1과 마찬가지로 포함 된 태스크는 읽는 쉽게 수행할 수 있도록 표시 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-252">The tasks that are in common with Exercise 1 have been marked to make your reading easier.</span></span> <span data-ttu-id="043ba-253">실습 1 완료 되지 않은 하지만 자세한 Code First 접근 방식으로이 연습에서 시작를 항목의 전체 범위를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-253">If you have not completed Exercise 1 but would like to learn the Code First approach, you can start from this exercise and get a full coverage of the topic.</span></span>


<a id="Ex2Task1"></a>

<a id="Task_1_-_Populating_Sample_Data"></a>
#### <a name="task-1---populating-sample-data"></a><span data-ttu-id="043ba-254">작업 1-샘플 데이터를 구성</span><span class="sxs-lookup"><span data-stu-id="043ba-254">Task 1 - Populating Sample Data</span></span>

<span data-ttu-id="043ba-255">이 작업에서는 코드 중심을 사용 하 여 intially 만들어질 때 데이터베이스를 샘플 데이터로 있습니다 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-255">In this task, you will populate the database with sample data when it is intially created using Code-First.</span></span>

1. <span data-ttu-id="043ba-256">열기는 **시작** 솔루션에 있는 **소스/e x 2-CreatingADatabaseCodeFirst/시작/** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-256">Open the **Begin** solution located at **Source/Ex2-CreatingADatabaseCodeFirst/Begin/** folder.</span></span> <span data-ttu-id="043ba-257">그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-257">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="043ba-258">제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면.</span><span class="sxs-lookup"><span data-stu-id="043ba-258">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="043ba-259">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-259">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="043ba-260">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="043ba-260">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="043ba-261">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-261">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="043ba-262">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-262">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="043ba-263">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-263">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="043ba-264">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-264">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="043ba-265">추가 **SampleData.cs** 파일을 여 **모델** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-265">Add the **SampleData.cs** file to the **Models** folder.</span></span> <span data-ttu-id="043ba-266">이렇게 하려면 마우스 오른쪽 단추로 클릭 **모델** 폴더를 가리키도록 **추가** 클릭 하 고 **기존 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-266">To do that, right-click **Models** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="043ba-267">찾아 **\Source\Assets** 선택 하 고는 **SampleData.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-267">Browse to **\Source\Assets** and select the **SampleData.cs** file.</span></span>

    <span data-ttu-id="043ba-268">![예제 데이터 코드를 채우는](aspnet-mvc-4-models-and-data-access/_static/image18.png "예제 데이터 코드 채우기")</span><span class="sxs-lookup"><span data-stu-id="043ba-268">![Sample data populate code](aspnet-mvc-4-models-and-data-access/_static/image18.png "Sample data populate code")</span></span>

    <span data-ttu-id="043ba-269">*예제 데이터 코드 채우기*</span><span class="sxs-lookup"><span data-stu-id="043ba-269">*Sample data populate code*</span></span>
3. <span data-ttu-id="043ba-270">열기는 **Global.asax.cs** 파일을 다음 추가 *를 사용 하 여* 문.</span><span class="sxs-lookup"><span data-stu-id="043ba-270">Open the **Global.asax.cs** file and add the following *using* statements.</span></span>

    <span data-ttu-id="043ba-271">(코드 조각- *모델 및 데이터 액세스-e x 2 글로벌 Asax Using*)</span><span class="sxs-lookup"><span data-stu-id="043ba-271">(Code Snippet - *Models And Data Access - Ex2 Global Asax Usings*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample5.cs)]
4. <span data-ttu-id="043ba-272">에 **응용 프로그램\_start ()** 메서드 데이터베이스 이니셜라이저를 설정 하려면 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-272">In the **Application\_Start()** method add the following line to set the database initializer.</span></span>

    <span data-ttu-id="043ba-273">(코드 조각- *모델 및 데이터 액세스-e x 2 글로벌 Asax SetInitializer*)</span><span class="sxs-lookup"><span data-stu-id="043ba-273">(Code Snippet - *Models And Data Access - Ex2 Global Asax SetInitializer*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample6.cs)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Configuring_the_connection_to_the_Database"></a>
#### <a name="task-2---configuring-the-connection-to-the-database"></a><span data-ttu-id="043ba-274">작업 2-데이터베이스 연결 구성</span><span class="sxs-lookup"><span data-stu-id="043ba-274">Task 2 - Configuring the connection to the Database</span></span>

<span data-ttu-id="043ba-275">이 프로젝트에 데이터베이스를 이미 추가한 했으므로에서 작성할는 **Web.config** 파일 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-275">Now that you have already added a database to our project, you will write in the **Web.config** file the connection string.</span></span>

1. <span data-ttu-id="043ba-276">연결 문자열에 추가 **Web.config**합니다. 이러한 파일을 열고 **Web.config** 프로젝트 루트 및 연결 문자열에서이 줄 DefaultConnection 라는 replace는  **&lt;connectionStrings&gt;**  섹션:</span><span class="sxs-lookup"><span data-stu-id="043ba-276">Add a connection string at **Web.config**. To do that, open **Web.config** at project root and replace the connection string named DefaultConnection with this line in the **&lt;connectionStrings&gt;** section:</span></span>

    <span data-ttu-id="043ba-277">![Web.config 파일 위치](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config 파일 위치")</span><span class="sxs-lookup"><span data-stu-id="043ba-277">![Web.config file location](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config file location")</span></span>

    <span data-ttu-id="043ba-278">*Web.config 파일 위치*</span><span class="sxs-lookup"><span data-stu-id="043ba-278">*Web.config file location*</span></span>


    [!code-xml[Main](aspnet-mvc-4-models-and-data-access/samples/sample7.xml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Working_with_the_Model"></a>
#### <a name="task-3---working-with-the-model"></a><span data-ttu-id="043ba-279">작업 3-모델 작업</span><span class="sxs-lookup"><span data-stu-id="043ba-279">Task 3 - Working with the Model</span></span>

<span data-ttu-id="043ba-280">이미 데이터베이스에 연결을 구성 했으므로 데이터베이스 테이블을 사용 하 여 모델을 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-280">Now that you have already configured the connection to the database, you will link the model with the database tables.</span></span> <span data-ttu-id="043ba-281">이 태스크에서는 Code First로 데이터베이스에 연결할 수 있는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-281">In this task, you will create a class that will be linked to the database with Code First.</span></span> <span data-ttu-id="043ba-282">수정 해야 하는 기존 POCO 모델 클래스 임을 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-282">Remember that there is an existent POCO model class that should be modified.</span></span>

> [!NOTE]
> <span data-ttu-id="043ba-283">연습 1을 완료 한 경우이 단계는 마법사에 의해 수행 된를 언급 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-283">If you completed Exercise 1, you will note that this step was performed by a wizard.</span></span> <span data-ttu-id="043ba-284">Code First를 통해 수동으로 데이터 엔터티에 연결 하는 클래스 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-284">By doing Code First, you will manually create classes that will be linked to data entities.</span></span>


1. <span data-ttu-id="043ba-285">POCO 모델 클래스를 열고 **장르** 에서 **모델** 폴더를 프로젝트 및 ID를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-285">Open the POCO model class **Genre** from **Models** project folder and include an ID.</span></span> <span data-ttu-id="043ba-286">Int 속성 이름으로 사용 하 여 **GenreId**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-286">Use an int property with the name **GenreId**.</span></span>

    <span data-ttu-id="043ba-287">(코드 조각- *모델 및 데이터 액세스-e x 2 코드 첫 번째 장르*)</span><span class="sxs-lookup"><span data-stu-id="043ba-287">(Code Snippet - *Models And Data Access - Ex2 Code First Genre*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample8.cs)]

    > [!NOTE]
    > <span data-ttu-id="043ba-288">Code First 규칙을 사용 하려면 Genre 클래스에 자동으로 검색 하는 기본 키 속성이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-288">To work with Code First conventions, the class Genre must have a primary key property that will be automatically detected.</span></span>
    > 
    > <span data-ttu-id="043ba-289">자세한 내용은이 코드의 첫 번째 규칙에 대 한 [msdn 문서](https://msdn.microsoft.com/en-us/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-289">You can read more about Code First Conventions in this [msdn article](https://msdn.microsoft.com/en-us/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx).</span></span>
2. <span data-ttu-id="043ba-290">이제는 POCO 모델 클래스를 열 **앨범** 에서 **모델** 폴더를 프로젝트 및 외래 키를 포함를 이름으로 속성을 만들 **GenreId** 및  **ArtistId**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-290">Now, open the POCO model class **Album** from **Models** project folder and include the foreign keys, create properties with the names **GenreId** and **ArtistId**.</span></span> <span data-ttu-id="043ba-291">가 이미이 클래스는 **GenreId** 기본 키에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-291">This class already have the **GenreId** for the primary key.</span></span>

    <span data-ttu-id="043ba-292">(코드 조각- *모델 및 데이터 액세스-e x 2 코드 첫 번째 앨범*)</span><span class="sxs-lookup"><span data-stu-id="043ba-292">(Code Snippet - *Models And Data Access - Ex2 Code First Album*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample9.cs)]
3. <span data-ttu-id="043ba-293">POCO 모델 클래스를 열고 **아티스트** 포함는 **ArtistId** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-293">Open the POCO model class **Artist** and include the **ArtistId** property.</span></span>

    <span data-ttu-id="043ba-294">(코드 조각- *모델 및 데이터 액세스-e x 2 코드 첫 번째 아티스트*)</span><span class="sxs-lookup"><span data-stu-id="043ba-294">(Code Snippet - *Models And Data Access - Ex2 Code First Artist*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample10.cs)]
4. <span data-ttu-id="043ba-295">마우스 오른쪽 단추로 클릭는 **모델** 프로젝트 폴더를 선택 **추가 | 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-295">Right-click the **Models** project folder and select **Add | Class**.</span></span> <span data-ttu-id="043ba-296">파일 이름을 **MusicStoreEntities.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-296">Name the file **MusicStoreEntities.cs**.</span></span> <span data-ttu-id="043ba-297">클릭 **추가 합니다.**</span><span class="sxs-lookup"><span data-stu-id="043ba-297">Then, click **Add.**</span></span>

    <span data-ttu-id="043ba-298">![클래스 추가](aspnet-mvc-4-models-and-data-access/_static/image20.png "클래스 추가")</span><span class="sxs-lookup"><span data-stu-id="043ba-298">![Adding a class](aspnet-mvc-4-models-and-data-access/_static/image20.png "Adding a class")</span></span>

    <span data-ttu-id="043ba-299">*새 항목 추가*</span><span class="sxs-lookup"><span data-stu-id="043ba-299">*Adding a new item*</span></span>

    <span data-ttu-id="043ba-300">![추가 class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "는 class2 추가")</span><span class="sxs-lookup"><span data-stu-id="043ba-300">![Adding a class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "Adding a class2")</span></span>

    <span data-ttu-id="043ba-301">*클래스 추가*</span><span class="sxs-lookup"><span data-stu-id="043ba-301">*Adding a class*</span></span>
5. <span data-ttu-id="043ba-302">방금 만든 클래스를 열고 **MusicStoreEntities.cs**, 네임 스페이스를 포함 하 고 **System.Data.Entity** 및 **System.Data.Entity.Infrastructure**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-302">Open the class you have just created, **MusicStoreEntities.cs**, and include the namespaces **System.Data.Entity** and **System.Data.Entity.Infrastructure**.</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample11.cs)]
6. <span data-ttu-id="043ba-303">확장 하는 클래스 선언 대신는 **DbContext** 클래스: 공용 선언 **DBSet** 재정의 **OnModelCreating** 메서드.</span><span class="sxs-lookup"><span data-stu-id="043ba-303">Replace the class declaration to extend the **DbContext** class: declare a public **DBSet** and override **OnModelCreating** method.</span></span> <span data-ttu-id="043ba-304">이 단계에서는 Entity Framework를 사용 하 여 모델을 연결 하는 도메인 클래스를 받아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-304">After this step you will get a domain class that will link your model with the Entity Framework.</span></span> <span data-ttu-id="043ba-305">파일을 수집 하려면 클래스 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-305">In order to do that, replace the class code with the following:</span></span>

    <span data-ttu-id="043ba-306">(코드 조각- *모델 및 데이터 액세스-e x 2 코드 첫 번째 MusicStoreEntities*)</span><span class="sxs-lookup"><span data-stu-id="043ba-306">(Code Snippet - *Models And Data Access - Ex2 Code First MusicStoreEntities*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample12.cs)]

    > [!NOTE]
    > <span data-ttu-id="043ba-307">Entity Framework와 함께 **DbContext** 및 **DBSet** POCO 클래스 장르를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-307">With Entity Framework **DbContext** and **DBSet** you will be able to query the POCO class Genre.</span></span> <span data-ttu-id="043ba-308">확장 하 여 **OnModelCreating** 에서 지정 하는 메서드를는 **코드** 데이터베이스 테이블에 장르 매핑할 수는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-308">By extending **OnModelCreating** method, you are specifying in the **code** how Genre will be mapped to a database table.</span></span> <span data-ttu-id="043ba-309">이 msdn 문서에서 DBContext 및 DBSet에 대 한 자세한 정보를 찾을 수 있습니다: [링크](https://msdn.microsoft.com/en-us/library/system.data.entity.dbcontext(v=vs.103).aspx)</span><span class="sxs-lookup"><span data-stu-id="043ba-309">You can find more information about DBContext and DBSet in this msdn article: [link](https://msdn.microsoft.com/en-us/library/system.data.entity.dbcontext(v=vs.103).aspx)</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="043ba-310">작업 4-데이터베이스 쿼리</span><span class="sxs-lookup"><span data-stu-id="043ba-310">Task 4 - Querying the Database</span></span>

<span data-ttu-id="043ba-311">이 태스크에서는 하드 코드 된 데이터를 사용 하는 대신를 검색 하는 데이터베이스에서 있도록 StoreController 클래스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-311">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will retrieve it from the database.</span></span>

> [!NOTE]
> <span data-ttu-id="043ba-312">연습 1과 마찬가지로이 작업이입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-312">This task is in common with Exercise 1.</span></span>
> 
> <span data-ttu-id="043ba-313">연습 1을 완료 한 경우 이러한 단계는 두 방법 모두 동일 하 게 기록 됩니다 (처음에 데이터베이스 또는 Code first).</span><span class="sxs-lookup"><span data-stu-id="043ba-313">If you completed Exercise 1 you will note these steps are the same in both approaches (Database first or Code first).</span></span> <span data-ttu-id="043ba-314">데이터가 모델에 연결 어떻게 다른 지 하지만 데이터 엔터티에 대 한 액세스는 컨트롤러에서 투명 아직 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-314">They are different in how the data is linked with the model, but the access to data entities is yet transparent from the controller.</span></span>


1. <span data-ttu-id="043ba-315">열기 **Controllers\StoreController.cs** 의 인스턴스를 저장 하는 클래스에 다음 필드를 추가 하 고는 **MusicStoreEntities** 라는 클래스를 **storeDB**:</span><span class="sxs-lookup"><span data-stu-id="043ba-315">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="043ba-316">(코드 조각- *모델 데이터 액세스 및-e x 1 storeDB*)</span><span class="sxs-lookup"><span data-stu-id="043ba-316">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample13.cs)]
2. <span data-ttu-id="043ba-317">**MusicStoreEntities** 클래스는 데이터베이스의 각 테이블에 대 한 컬렉션 속성을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-317">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="043ba-318">업데이트 **찾아보기** 모든 장르를 가져오려는 작업 메서드는 **앨범**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-318">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="043ba-319">(코드 조각- *모델 및 데이터 액세스-e x 2 저장소 찾아보기*)</span><span class="sxs-lookup"><span data-stu-id="043ba-319">(Code Snippet - *Models And Data Access - Ex2 Store Browse*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="043ba-320">.NET 호출의 기능을 사용 하는 **LINQ** 프로그래밍할 수 있습니다 (통합 언어 쿼리)-이 데이터베이스에 대해 코드를 실행 하 고 반환 하는 이러한 컬렉션에 대 한 강력한 형식의 쿼리 식을 작성 하 개체 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-320">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="043ba-321">LINQ에 대 한 자세한 내용은 참조 하십시오는 [msdn 사이트](https://msdn.microsoft.com/en-us/library/bb397926(v=vs.110).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-321">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/en-us/library/bb397926(v=vs.110).aspx).</span></span>
3. <span data-ttu-id="043ba-322">업데이트 **인덱스** 동작 메서드를 모든 장르를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-322">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="043ba-323">(코드 조각- *모델 및 데이터 액세스-e x 2 저장소 인덱스*)</span><span class="sxs-lookup"><span data-stu-id="043ba-323">(Code Snippet - *Models And Data Access - Ex2 Store Index*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample15.cs)]
4. <span data-ttu-id="043ba-324">업데이트 **인덱스** 동작 메서드의 모든 장르를 검색 하 고 목록에 컬렉션을 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-324">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="043ba-325">(코드 조각- *모델 및 데이터 액세스-e x 2 저장소 GenreMenu*)</span><span class="sxs-lookup"><span data-stu-id="043ba-325">(Code Snippet - *Models And Data Access - Ex2 Store GenreMenu*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample16.cs)]

<a id="Ex2Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="043ba-326">5-응용 프로그램 실행 작업</span><span class="sxs-lookup"><span data-stu-id="043ba-326">Task 5 - Running the Application</span></span>

<span data-ttu-id="043ba-327">이 작업에서는 저장소 인덱스 페이지에 하드 코드 된 것 대신 데이터베이스에 저장 된 장르 표시 이제 됩니다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-327">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="043ba-328">하기 때문에 템플릿 보기를 변경할 필요가 없습니다는 **StoreController** 동일한 반환 **StoreIndexViewModel** 이전 처럼 하지만이 이번에는 데이터는 데이터베이스에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-328">There is no need to change the View template because the **StoreController** is returning the same **StoreIndexViewModel** as before, but this time the data will come from the database.</span></span>

1. <span data-ttu-id="043ba-329">솔루션 및 키를 눌러 다시 빌드 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-329">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="043ba-330">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-330">The project starts in the Home page.</span></span> <span data-ttu-id="043ba-331">확인의 메뉴 **장르** 는 더 이상 하드 코드 된 목록 및 데이터는 데이터베이스에서 직접 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-331">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image22.png)

    <span data-ttu-id="043ba-333">*데이터베이스에서 검색 장르*</span><span class="sxs-lookup"><span data-stu-id="043ba-333">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="043ba-334">이제 모든 장르로 이동 하 고 데이터베이스에서 앨범 채워집니다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-334">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="043ba-335">![데이터베이스에서 앨범 검색](aspnet-mvc-4-models-and-data-access/_static/image23.png "앨범을 데이터베이스에서 검색")</span><span class="sxs-lookup"><span data-stu-id="043ba-335">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image23.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="043ba-336">*데이터베이스에서 검색 앨범*</span><span class="sxs-lookup"><span data-stu-id="043ba-336">*Browsing Albums from the database*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Querying_the_Database_with_Parameters"></a>
### <a name="exercise-3-querying-the-database-with-parameters"></a><span data-ttu-id="043ba-337">매개 변수를 사용 하 여 데이터베이스를 쿼리 하는 연습 3:</span><span class="sxs-lookup"><span data-stu-id="043ba-337">Exercise 3: Querying the Database with Parameters</span></span>

<span data-ttu-id="043ba-338">이 연습에서는 매개 변수를 사용 하 여 데이터베이스를 쿼리 하는 방법 및 쿼리 결과 모양 지정을 사용 하는 방법에 설명 합니다, 그리고 번호 데이터베이스 감소 하는 기능에 더 효율적으로 검색 하는 동안 데이터에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-338">In this exercise, you will learn how to query the database using parameters, and how to use Query Result Shaping, a feature that reduces the number database accesses retrieving data in a more efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="043ba-339">쿼리 결과 모양 지정에 자세한 내용은 다음을 방문 [msdn 문서](https://msdn.microsoft.com/en-us/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-339">For further information on Query Result Shaping, visit the following [msdn article](https://msdn.microsoft.com/en-us/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx).</span></span>


<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_StoreController_to_Retrieve_Albums_from_Database"></a>
#### <a name="task-1---modifying-storecontroller-to-retrieve-albums-from-database"></a><span data-ttu-id="043ba-340">작업 1-수정 StoreController 앨범 데이터베이스에서 검색 하려면</span><span class="sxs-lookup"><span data-stu-id="043ba-340">Task 1 - Modifying StoreController to Retrieve Albums from Database</span></span>

<span data-ttu-id="043ba-341">이 작업에서는 변경 됩니다는 **StoreController** 앨범 특정 장르에서 검색할 데이터베이스에 액세스 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-341">In this task, you will change the **StoreController** class to access the database to retrieve albums from a specific genre.</span></span>

1. <span data-ttu-id="043ba-342">열기는 **시작** 솔루션에 있는 **Source\Ex3 QueryingTheDatabaseWithParametersCodeFirst\Begin** 코드 중심 접근 방식을 사용 하려는 경우 폴더 또는 **Source\ Ex3 QueryingTheDatabaseWithParametersDBFirst\Begin** 폴더 데이터베이스 중심 접근 방식을 사용 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="043ba-342">Open the **Begin** solution located at the **Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin** folder if you want to use Code-First approach or **Source\Ex3-QueryingTheDatabaseWithParametersDBFirst\Begin** folder if you want to use Database-First approach.</span></span> <span data-ttu-id="043ba-343">그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-343">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="043ba-344">제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면.</span><span class="sxs-lookup"><span data-stu-id="043ba-344">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="043ba-345">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-345">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="043ba-346">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="043ba-346">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="043ba-347">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-347">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="043ba-348">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-348">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="043ba-349">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-349">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="043ba-350">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-350">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="043ba-351">열기는 **StoreController** 변경 하는 클래스는 **찾아보기** 동작 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-351">Open the **StoreController** class to change the **Browse** action method.</span></span> <span data-ttu-id="043ba-352">이 수행 하는 **솔루션 탐색기**를 확장 하 고는 **컨트롤러** 폴더를 두 번 클릭 **StoreController.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-352">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
3. <span data-ttu-id="043ba-353">변경 된 **찾아보기** 동작 메서드를 앨범 특정 장르에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-353">Change the **Browse** action method to retrieve albums for a specific genre.</span></span> <span data-ttu-id="043ba-354">이렇게 하려면 다음 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-354">To do this, replace the following code:</span></span>

    <span data-ttu-id="043ba-355">(코드 조각- *모델 및 데이터 액세스-Ex3 StoreController BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="043ba-355">(Code Snippet - *Models And Data Access - Ex3 StoreController BrowseMethod*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample17.cs)]

    > [!NOTE]
    > <span data-ttu-id="043ba-356">엔터티 컬렉션을 채우려면 사용 해야는 **Include** 너무 앨범을 검색 하려면를 지정 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="043ba-356">To populate a collection of the entity, you need to use the **Include** method to specify you want to retrieve the albums too.</span></span> <span data-ttu-id="043ba-357">사용할 수는 있습니다. **Single()** linq에서 확장 때문이 경우 하나의 장르 앨범에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-357">You can use the .**Single()** extension in LINQ because in this case only one genre is expected for an album.</span></span> <span data-ttu-id="043ba-358">**Single()** 메서드는이 경우 이름이 정의 된 값과 일치 되도록 단일 장르 개체를 지정 하는 매개 변수로 람다 식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-358">The **Single()** method takes a Lambda expression as a parameter, which in this case specifies a single Genre object such that its name matches the value defined.</span></span>
    > 
    > <span data-ttu-id="043ba-359">장르 개체를 검색할 때도 로드를 원하는 다른 관련된 엔터티를 나타낼 수 있도록 하는 기능을 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-359">You will take advantage of a feature that allows you to indicate other related entities you want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="043ba-360">라는이 기능은 **쿼리 결과 셰이핑**, 정보를 검색할 데이터베이스에 액세스 하는 데 필요한 시간 수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-360">This feature is called **Query Result Shaping**, and enables you to reduce the number of times needed to access the database to retrieve information.</span></span> <span data-ttu-id="043ba-361">이 시나리오에서는 검색할 장르에 대 한 앨범을 프리페치 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-361">In this scenario, you will want to pre-fetch the Albums for the Genre you retrieve.</span></span>
    > 
    > <span data-ttu-id="043ba-362">쿼리에 포함 된 **Genres.Include (&quot;앨범&quot;)** 관련된 앨범도 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-362">The query includes **Genres.Include(&quot;Albums&quot;)** to indicate that you want related albums as well.</span></span> <span data-ttu-id="043ba-363">이 값은 단일 데이터베이스 요청에서 Genre 및 앨범 모두 데이터를 검색 하므로 보다 효율적인 응용 프로그램에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-363">This will result in a more efficient application, since it will retrieve both Genre and Album data in a single database request.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="043ba-364">작업 2-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="043ba-364">Task 2 - Running the Application</span></span>

<span data-ttu-id="043ba-365">이 작업에서는 응용 프로그램을 실행 하 고 데이터베이스에서 특정 genre의 앨범을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-365">In this task, you will run the application and retrieve albums of a specific genre from the database.</span></span>

1. <span data-ttu-id="043ba-366">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-366">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="043ba-367">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-367">The project starts in the Home page.</span></span> <span data-ttu-id="043ba-368">URL을 변경 **/저장소/찾아보기? 장르 Pop =** 데이터베이스에서 결과 가져오는 중 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-368">Change the URL to **/Store/Browse?genre=Pop** to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="043ba-369">![장르별로 검색](aspnet-mvc-4-models-and-data-access/_static/image24.png "장르별로 검색")</span><span class="sxs-lookup"><span data-stu-id="043ba-369">![Browsing by genre](aspnet-mvc-4-models-and-data-access/_static/image24.png "Browsing by genre")</span></span>

    <span data-ttu-id="043ba-370">*검색/저장소/찾아보기? 장르 Pop =*</span><span class="sxs-lookup"><span data-stu-id="043ba-370">*Browsing /Store/Browse?genre=Pop*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Accessing_Albums_by_Id"></a>
#### <a name="task-3---accessing-albums-by-id"></a><span data-ttu-id="043ba-371">작업 3-Id로 앨범에 액세스</span><span class="sxs-lookup"><span data-stu-id="043ba-371">Task 3 - Accessing Albums by Id</span></span>

<span data-ttu-id="043ba-372">이 태스크에서는 앨범 자신의 id를 가져올 이전 절차를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-372">In this task, you will repeat the previous procedure to get albums by their Id.</span></span>

1. <span data-ttu-id="043ba-373">Visual Studio로 반환 하는 데 필요한 경우 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-373">Close the browser if needed, to return to Visual Studio.</span></span> <span data-ttu-id="043ba-374">열기는 **StoreController** 변경 하는 클래스는 **세부 정보** 동작 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-374">Open the **StoreController** class to change the **Details** action method.</span></span> <span data-ttu-id="043ba-375">이 수행 하는 **솔루션 탐색기**를 확장 하 고는 **컨트롤러** 폴더를 두 번 클릭 **StoreController.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-375">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
2. <span data-ttu-id="043ba-376">변경 된 **세부 정보** 앨범 세부 정보를 검색할 작업 메서드를 기반으로 해당 **Id**합니다. 이렇게 하려면 다음 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-376">Change the **Details** action method to retrieve albums details based on their **Id**. To do this, replace the following code:</span></span>

    <span data-ttu-id="043ba-377">(코드 조각- *모델 및 데이터 액세스-Ex3 StoreController DetailsMethod*)</span><span class="sxs-lookup"><span data-stu-id="043ba-377">(Code Snippet - *Models And Data Access - Ex3 StoreController DetailsMethod*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample18.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="043ba-378">작업 4-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="043ba-378">Task 4 - Running the Application</span></span>

<span data-ttu-id="043ba-379">이 태스크에서는 웹 브라우저에서 응용 프로그램을 실행 및 해당 id 앨범 세부 정보를 가져올 됩니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-379">In this task, you will run the Application in a web browser and obtain album details by their Id.</span></span>

1. <span data-ttu-id="043ba-380">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-380">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="043ba-381">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-381">The project starts in the Home page.</span></span> <span data-ttu-id="043ba-382">URL을 변경 **/Store/Details/51** 하거나 장르 찾은 앨범 데이터베이스에서 결과 가져오는 중 확인을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-382">Change the URL to **/Store/Details/51** or browse the genres and select an album to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="043ba-383">![세부 정보를 검색](aspnet-mvc-4-models-and-data-access/_static/image25.png "세부 정보를 검색 합니다.")</span><span class="sxs-lookup"><span data-stu-id="043ba-383">![Browsing Details](aspnet-mvc-4-models-and-data-access/_static/image25.png "Browsing Details")</span></span>

    <span data-ttu-id="043ba-384">*/Store/Details/51 검색*</span><span class="sxs-lookup"><span data-stu-id="043ba-384">*Browsing /Store/Details/51*</span></span>

> [!NOTE]
> <span data-ttu-id="043ba-385">다음 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수는 또한 [부록 b: 게시 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램](#AppendixB)합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-385">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>


* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="043ba-386">요약</span><span class="sxs-lookup"><span data-stu-id="043ba-386">Summary</span></span>

<span data-ttu-id="043ba-387">ASP.NET MVC 모델 및 데이터 액세스의 기본적인 사항을 배웠습니다 실습 랩이 완료, 사용 하 여는 **Database First** 접근 방식으로 **Code First** 접근 방식:</span><span class="sxs-lookup"><span data-stu-id="043ba-387">By completing this Hands-on Lab you have learned the fundamentals of ASP.NET MVC Models and Data Access, using the **Database First** approach as well as the **Code First** Approach:</span></span>

- <span data-ttu-id="043ba-388">해당 데이터를 처리 하기 위해 솔루션에 데이터베이스를 추가 하는 방법</span><span class="sxs-lookup"><span data-stu-id="043ba-388">How to add a database to the solution in order to consume its data</span></span>
- <span data-ttu-id="043ba-389">대신 하드 코드 된 데이터베이스에서 가져온 데이터와 함께 템플릿 보기를 제공 하기 위해 컨트롤러를 업데이트 하는 방법</span><span class="sxs-lookup"><span data-stu-id="043ba-389">How to update Controllers to provide View templates with the data taken from the database instead of hard-coded one</span></span>
- <span data-ttu-id="043ba-390">매개 변수를 사용 하 여 데이터베이스를 쿼리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="043ba-390">How to query the database using parameters</span></span>
- <span data-ttu-id="043ba-391">쿼리 결과 셰이핑, 데이터베이스 액세스의 수를 줄이는 기능 데이터를 더욱 효율적으로 검색을 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="043ba-391">How to use the Query Result Shaping, a feature that reduces the number of database accesses, retrieving data in a more efficient way</span></span>
- <span data-ttu-id="043ba-392">모델 데이터베이스에 연결할 Microsoft Entity framework에서 Database First 및 Code First 접근 방식을 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="043ba-392">How to use both Database First and Code First approaches in Microsoft Entity Framework to link the database with the model</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="043ba-393">부록 a: 설치 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="043ba-393">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="043ba-394">설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 버전을 사용 하 여  **[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="043ba-394">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="043ba-395">다음 지침을 설치 하는 데 필요한 단계를 안내 하 *Visual studio Express 2012 for Web* 를 사용 하 여 *Microsoft 웹 플랫폼 설치 관리자*합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-395">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="043ba-396">로 이동 [ [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-396">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="043ba-397">또는 이미 설치 된 웹 플랫폼 설치 관리자를 열 수 있습니다 및 제품에 대 한 검색 &quot; *Visual Studio Express 2012 for Web Windows Azure SDK와*&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-397">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;*Visual Studio Express 2012 for Web with Windows Azure SDK*&quot;.</span></span>
2. <span data-ttu-id="043ba-398">클릭 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-398">Click on **Install Now**.</span></span> <span data-ttu-id="043ba-399">없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-399">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="043ba-400">한 번 **웹 플랫폼 설치 관리자** 열려 클릭 **설치** 는 설치 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-400">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="043ba-401">![Visual Studio Express 설치](aspnet-mvc-4-models-and-data-access/_static/image26.png "Visual Studio Express 설치")</span><span class="sxs-lookup"><span data-stu-id="043ba-401">![Install Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="043ba-402">*Visual Studio Express 설치*</span><span class="sxs-lookup"><span data-stu-id="043ba-402">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="043ba-403">모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-403">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건 동의](aspnet-mvc-4-models-and-data-access/_static/image27.png)

    <span data-ttu-id="043ba-405">*사용 조건 동의*</span><span class="sxs-lookup"><span data-stu-id="043ba-405">*Accepting the license terms*</span></span>
5. <span data-ttu-id="043ba-406">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-406">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](aspnet-mvc-4-models-and-data-access/_static/image28.png)

    <span data-ttu-id="043ba-408">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="043ba-408">*Installation progress*</span></span>
6. <span data-ttu-id="043ba-409">설치가 완료 되 면 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-409">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](aspnet-mvc-4-models-and-data-access/_static/image29.png)

    <span data-ttu-id="043ba-411">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="043ba-411">*Installation completed*</span></span>
7. <span data-ttu-id="043ba-412">클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-412">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="043ba-413">Visual Studio Express for Web을 열려면로 이동는 **시작** 화면를 쓰기 시작할 &quot; **VS Express**&quot;, 클릭는 **VS Express for Web** 바둑판식 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-413">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![웹 타일에 대 한 VS Express](aspnet-mvc-4-models-and-data-access/_static/image30.png)

    <span data-ttu-id="043ba-415">*웹 타일에 대 한 VS Express*</span><span class="sxs-lookup"><span data-stu-id="043ba-415">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="043ba-416">부록 b: 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="043ba-416">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="043ba-417">이 부록에서는 Windows Azure 관리 포털에서 새 웹 사이트를 만들고 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하기 위해 랩에서 수행 하 여 가져온 응용 프로그램을 게시 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-417">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="043ba-418">작업 1-Windows에서 새 웹 사이트를 만드는 Azure 포털</span><span class="sxs-lookup"><span data-stu-id="043ba-418">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="043ba-419">이동 하 여 [Windows Azure 관리 포털](https://manage.windowsazure.com/) 구독에 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-419">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="043ba-420">Windows Azure를 무료로 10 개 ASP.NET 웹 사이트를 호스트 하 고 트래픽이 증가 됨을 확장 한 다음 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-420">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="043ba-421">등록할 수 [여기](http://aka.ms/aspnet-hol-azure)합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-421">You can sign up [here](http://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="043ba-422">![Windows Azure 포털에 로그온](aspnet-mvc-4-models-and-data-access/_static/image31.png "Windows Azure 포털에 로그인")</span><span class="sxs-lookup"><span data-stu-id="043ba-422">![Log on to Windows Azure portal](aspnet-mvc-4-models-and-data-access/_static/image31.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="043ba-423">*Windows Azure 관리 포털에 로그온*</span><span class="sxs-lookup"><span data-stu-id="043ba-423">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="043ba-424">클릭 **새로** 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-424">Click **New** on the command bar.</span></span>

    <span data-ttu-id="043ba-425">![새 웹 사이트를 만드는](aspnet-mvc-4-models-and-data-access/_static/image32.png "새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="043ba-425">![Creating a new Web Site](aspnet-mvc-4-models-and-data-access/_static/image32.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="043ba-426">*새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="043ba-426">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="043ba-427">클릭 **계산** | **웹 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-427">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="043ba-428">그런 다음 선택 **빠른 생성** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-428">Then select **Quick Create** option.</span></span> <span data-ttu-id="043ba-429">새 웹 사이트에 대 한 사용 가능한 URL을 입력 하 고 클릭 **웹 사이트 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-429">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="043ba-430">Windows Azure 웹 사이트는 호스트를 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-430">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="043ba-431">빨리 만들기 옵션을 사용 하면 완성 된 웹 응용 프로그램을 Windows Azure 웹 사이트에서 포털 외부에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-431">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="043ba-432">데이터베이스를 설정 하기 위한 단계는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-432">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="043ba-433">![빠른 생성을 사용 하 여 새 웹 사이트를 만드는](aspnet-mvc-4-models-and-data-access/_static/image33.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="043ba-433">![Creating a new Web Site using Quick Create](aspnet-mvc-4-models-and-data-access/_static/image33.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="043ba-434">*빠른 생성을 사용 하 여 새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="043ba-434">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="043ba-435">새 될 때까지 기다렸다가 **웹 사이트** 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-435">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="043ba-436">웹 사이트가 만들어지면 아래 링크를 클릭 하 고 **URL** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-436">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="043ba-437">새 웹 사이트가 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-437">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="043ba-438">![새 웹 사이트를 찾아](aspnet-mvc-4-models-and-data-access/_static/image34.png "새 웹 사이트를 검색 합니다.")</span><span class="sxs-lookup"><span data-stu-id="043ba-438">![Browsing to the new web site](aspnet-mvc-4-models-and-data-access/_static/image34.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="043ba-439">*새 웹 사이트를 검색합니다.*</span><span class="sxs-lookup"><span data-stu-id="043ba-439">*Browsing to the new web site*</span></span>

    <span data-ttu-id="043ba-440">![실행 중인 웹 사이트](aspnet-mvc-4-models-and-data-access/_static/image35.png "실행 중인 웹 사이트")</span><span class="sxs-lookup"><span data-stu-id="043ba-440">![Web site running](aspnet-mvc-4-models-and-data-access/_static/image35.png "Web site running")</span></span>

    <span data-ttu-id="043ba-441">*실행 중인 웹 사이트*</span><span class="sxs-lookup"><span data-stu-id="043ba-441">*Web site running*</span></span>
6. <span data-ttu-id="043ba-442">포털로 돌아가서 아래에서 웹 사이트의 이름을 클릭는 **이름** 관리 페이지를 표시 하는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-442">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="043ba-443">![웹 사이트 관리 페이지 열기](aspnet-mvc-4-models-and-data-access/_static/image36.png "웹 사이트 관리 페이지 열기")</span><span class="sxs-lookup"><span data-stu-id="043ba-443">![Opening the web site management pages](aspnet-mvc-4-models-and-data-access/_static/image36.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="043ba-444">*웹 사이트 관리 페이지 열기*</span><span class="sxs-lookup"><span data-stu-id="043ba-444">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="043ba-445">에 **대시보드** 페이지의 **눈에 보는** 섹션에서 클릭는 **게시 프로필 다운로드** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-445">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="043ba-446">*게시 프로필* 각각의 활성화 된 게시 방법에 대 한 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 하는 데 필요한 정보가 모두 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-446">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="043ba-447">게시 프로필에는 Url, 사용자 자격 증명 및 연결 하 고 각 게시 메서드를 사용할 수 있는 끝점에 대해 인증 하는 데 필요한 데이터베이스 문자열이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-447">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="043ba-448">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 읽는 지원 하기 위해 게시 프로필에 대 한 이러한 프로그램의 구성을 자동화 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-448">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="043ba-449">![게시 프로필 다운로드 웹 사이트](aspnet-mvc-4-models-and-data-access/_static/image37.png "게시 프로필 다운로드 웹 사이트")</span><span class="sxs-lookup"><span data-stu-id="043ba-449">![Downloading the web site publish profile](aspnet-mvc-4-models-and-data-access/_static/image37.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="043ba-450">*게시 프로필 다운로드 웹 사이트*</span><span class="sxs-lookup"><span data-stu-id="043ba-450">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="043ba-451">알려진된 위치에 게시 프로필 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-451">Download the publish profile file to a known location.</span></span> <span data-ttu-id="043ba-452">더 이상이 연습에서는 Visual Studio에서 웹 응용 프로그램 Windows Azure 웹 사이트를 게시 하려면이 파일을 사용 하는 방법을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-452">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="043ba-453">![게시 프로필 파일을 저장](aspnet-mvc-4-models-and-data-access/_static/image38.png "게시 프로필 저장")</span><span class="sxs-lookup"><span data-stu-id="043ba-453">![Saving the publish profile file](aspnet-mvc-4-models-and-data-access/_static/image38.png "Saving the publish profile")</span></span>

    <span data-ttu-id="043ba-454">*게시 프로필 파일을 저장합니다.*</span><span class="sxs-lookup"><span data-stu-id="043ba-454">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="043ba-455">작업 2-데이터베이스 서버 구성</span><span class="sxs-lookup"><span data-stu-id="043ba-455">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="043ba-456">응용 프로그램에서 SQL Server를 활용 하는 경우 데이터베이스를 SQL 데이터베이스 서버 만들기 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-456">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="043ba-457">SQL Server를 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 태스크를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-457">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="043ba-458">응용 프로그램 데이터베이스를 저장 하기 위해 SQL 데이터베이스 서버를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-458">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="043ba-459">Windows Azure 관리 포털에서 구독의 SQL 데이터베이스 서버를 볼 수 있습니다 **Sql 데이터베이스** | **서버** | **서버 대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-459">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="043ba-460">만든 서버 없는 경우 수행 하 여 만들 수 있습니다는 **추가** 명령 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-460">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="043ba-461">기록해는 **서버 이름 및 URL, 관리자 로그인 이름 및 암호**, 다음 작업에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-461">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="043ba-462">만들지 마십시오 데이터베이스 아직 대로 이후 단계에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-462">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="043ba-463">![SQL 데이터베이스 서버 대시보드](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL 데이터베이스 서버 대시보드")</span><span class="sxs-lookup"><span data-stu-id="043ba-463">![SQL Database Server Dashboard](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="043ba-464">*SQL 데이터베이스 서버 대시보드*</span><span class="sxs-lookup"><span data-stu-id="043ba-464">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="043ba-465">다음 태스크에서는 서버 목록에 사용자의 로컬 IP 주소를 포함 해야 이러한 이유로 Visual Studio에서 데이터베이스 연결을 테스트 **허용 IP 주소**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-465">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="043ba-466">작업을 수행 하려면 **구성**에서 IP 주소를 선택 **현재 클라이언트 IP 주소** 에 붙여넣습니다는 **시작 IP 주소** 및 **끝IP주소** 클릭 하 고 텍스트 상자는 ![add-client-ip-address-ok-button](aspnet-mvc-4-models-and-data-access/_static/image40.png) 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-466">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-models-and-data-access/_static/image40.png) button.</span></span>

    ![클라이언트 IP 주소를 추가합니다.](aspnet-mvc-4-models-and-data-access/_static/image41.png)

    <span data-ttu-id="043ba-468">*클라이언트 IP 주소를 추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="043ba-468">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="043ba-469">한 번는 **클라이언트 IP 주소** 허용된 된 IP 주소에 추가 됩니다 목록에서 클릭 **저장** 하 여 변경 사항을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-469">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![변경 확인](aspnet-mvc-4-models-and-data-access/_static/image42.png)

    <span data-ttu-id="043ba-471">*변경 확인*</span><span class="sxs-lookup"><span data-stu-id="043ba-471">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="043ba-472">작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="043ba-472">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="043ba-473">ASP.NET MVC 4 솔루션으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-473">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="043ba-474">에 **솔루션 탐색기**웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-474">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="043ba-475">![응용 프로그램을 게시](aspnet-mvc-4-models-and-data-access/_static/image43.png "응용 프로그램을 게시")</span><span class="sxs-lookup"><span data-stu-id="043ba-475">![Publishing the Application](aspnet-mvc-4-models-and-data-access/_static/image43.png "Publishing the Application")</span></span>

    <span data-ttu-id="043ba-476">*웹 사이트를 게시*</span><span class="sxs-lookup"><span data-stu-id="043ba-476">*Publishing the web site*</span></span>
2. <span data-ttu-id="043ba-477">첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-477">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="043ba-478">![게시 프로필 가져오기](aspnet-mvc-4-models-and-data-access/_static/image44.png "게시 프로필 가져오기")</span><span class="sxs-lookup"><span data-stu-id="043ba-478">![Importing the publish profile](aspnet-mvc-4-models-and-data-access/_static/image44.png "Importing the publish profile")</span></span>

    <span data-ttu-id="043ba-479">*게시 프로필 가져오기*</span><span class="sxs-lookup"><span data-stu-id="043ba-479">*Importing publish profile*</span></span>
3. <span data-ttu-id="043ba-480">클릭 **연결 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-480">Click **Validate Connection**.</span></span> <span data-ttu-id="043ba-481">유효성 검사가 완료 되 면 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-481">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="043ba-482">연결 유효성 검사 단추 옆에 표시 녹색 확인 표시가 표시 되 면 유효성 검사가 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-482">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="043ba-483">![연결 유효성 검사](aspnet-mvc-4-models-and-data-access/_static/image45.png "연결 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="043ba-483">![Validating connection](aspnet-mvc-4-models-and-data-access/_static/image45.png "Validating connection")</span></span>

    <span data-ttu-id="043ba-484">*연결 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="043ba-484">*Validating connection*</span></span>
4. <span data-ttu-id="043ba-485">에 **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆의 단추 클릭 (즉, **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="043ba-485">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="043ba-486">![웹 배포 구성](aspnet-mvc-4-models-and-data-access/_static/image46.png "웹 배포 구성")</span><span class="sxs-lookup"><span data-stu-id="043ba-486">![Web deploy configuration](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web deploy configuration")</span></span>

    <span data-ttu-id="043ba-487">*웹 배포 구성*</span><span class="sxs-lookup"><span data-stu-id="043ba-487">*Web deploy configuration*</span></span>
5. <span data-ttu-id="043ba-488">다음과 같이 데이터베이스 연결을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-488">Configure the database connection as follows:</span></span>

    - <span data-ttu-id="043ba-489">에 **서버 이름** SQL 데이터베이스 서버 URL 사용 하 여 입력 된 *tcp:* 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-489">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
    - <span data-ttu-id="043ba-490">**사용자 이름** 서버 관리자 로그인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-490">In **User name** type your server administrator login name.</span></span>
    - <span data-ttu-id="043ba-491">**암호** 서버 관리자 로그인 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-491">In **Password** type your server administrator login password.</span></span>
    - <span data-ttu-id="043ba-492">새 데이터베이스 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-492">Type a new database name.</span></span>

    <span data-ttu-id="043ba-493">![대상 연결 문자열 구성](aspnet-mvc-4-models-and-data-access/_static/image47.png "대상 연결 문자열 구성")</span><span class="sxs-lookup"><span data-stu-id="043ba-493">![Configuring destination connection string](aspnet-mvc-4-models-and-data-access/_static/image47.png "Configuring destination connection string")</span></span>

    <span data-ttu-id="043ba-494">*대상 연결 문자열 구성*</span><span class="sxs-lookup"><span data-stu-id="043ba-494">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="043ba-495">그런 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-495">Then click **OK**.</span></span> <span data-ttu-id="043ba-496">데이터베이스를 만들려는 대화 상자가 나타나면 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-496">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="043ba-497">![데이터베이스를 만드는](aspnet-mvc-4-models-and-data-access/_static/image48.png "데이터베이스 문자열 만들기")</span><span class="sxs-lookup"><span data-stu-id="043ba-497">![Creating the database](aspnet-mvc-4-models-and-data-access/_static/image48.png "Creating the database string")</span></span>

    <span data-ttu-id="043ba-498">*데이터베이스를 만드는 중*</span><span class="sxs-lookup"><span data-stu-id="043ba-498">*Creating the database*</span></span>
7. <span data-ttu-id="043ba-499">Windows azure에서 SQL 데이터베이스에 연결 하기 위해 사용할 연결 문자열은 기본 연결 텍스트 상자 내에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-499">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="043ba-500">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-500">Then click **Next**.</span></span>

    <span data-ttu-id="043ba-501">![SQL 데이터베이스를 가리키는 연결 문자열](aspnet-mvc-4-models-and-data-access/_static/image49.png "SQL 데이터베이스를 가리키는 연결 문자열")</span><span class="sxs-lookup"><span data-stu-id="043ba-501">![Connection string pointing to SQL Database](aspnet-mvc-4-models-and-data-access/_static/image49.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="043ba-502">*SQL 데이터베이스를 가리키는 연결 문자열*</span><span class="sxs-lookup"><span data-stu-id="043ba-502">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="043ba-503">에 **미리 보기** 페이지 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-503">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="043ba-504">![웹 응용 프로그램을 게시](aspnet-mvc-4-models-and-data-access/_static/image50.png "웹 응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="043ba-504">![Publishing the web application](aspnet-mvc-4-models-and-data-access/_static/image50.png "Publishing the web application")</span></span>

    <span data-ttu-id="043ba-505">*웹 응용 프로그램 게시*</span><span class="sxs-lookup"><span data-stu-id="043ba-505">*Publishing the web application*</span></span>
9. <span data-ttu-id="043ba-506">게시 프로세스가 완료 되 면 게시 된 웹 사이트 기본 브라우저가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-506">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="043ba-507">부록 c: 코드 조각을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="043ba-507">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="043ba-508">코드 조각 바로 쉽게 얻습니다 필요한 코드를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-508">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="043ba-509">랩 문서는 알려 정확 하 게 사용 가능 시기, 다음 그림에 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-509">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="043ba-510">![Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여](aspnet-mvc-4-models-and-data-access/_static/image51.png "Visual Studio를 사용 하 여 코드 조각을 프로젝트에 코드를 삽입 하려면")</span><span class="sxs-lookup"><span data-stu-id="043ba-510">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-models-and-data-access/_static/image51.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="043ba-511">*Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여*</span><span class="sxs-lookup"><span data-stu-id="043ba-511">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="043ba-512">***키보드 (C#만)를 사용 하 여 코드 조각을 추가 하려면***</span><span class="sxs-lookup"><span data-stu-id="043ba-512">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="043ba-513">코드를 삽입 하려는 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-513">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="043ba-514">공백 또는 하이픈만) (없이 코드 조각 이름을 입력 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-514">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="043ba-515">IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-515">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="043ba-516">올바른 코드 조각 선택 (또는 전체 코드 조각이 이름이 선택 될 때까지 입력 유지).</span><span class="sxs-lookup"><span data-stu-id="043ba-516">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="043ba-517">커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-517">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="043ba-518">![코드 조각 이름을 입력 하기 시작](aspnet-mvc-4-models-and-data-access/_static/image52.png "조각 이름을 입력 하기 시작")</span><span class="sxs-lookup"><span data-stu-id="043ba-518">![Start typing the snippet name](aspnet-mvc-4-models-and-data-access/_static/image52.png "Start typing the snippet name")</span></span>

<span data-ttu-id="043ba-519">*코드 조각 이름을 입력 하기 시작*</span><span class="sxs-lookup"><span data-stu-id="043ba-519">*Start typing the snippet name*</span></span>

<span data-ttu-id="043ba-520">![Tab 키를 눌러 강조 표시 된 코드 조각 선택](aspnet-mvc-4-models-and-data-access/_static/image53.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")</span><span class="sxs-lookup"><span data-stu-id="043ba-520">![Press Tab to select the highlighted snippet](aspnet-mvc-4-models-and-data-access/_static/image53.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="043ba-521">*Tab 키를 눌러 강조 표시 된 코드 조각 선택*</span><span class="sxs-lookup"><span data-stu-id="043ba-521">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="043ba-522">![확장 하 고 Tab 키를 눌러 다시 코드 조각](aspnet-mvc-4-models-and-data-access/_static/image54.png "확장 하 고 Tab 키를 눌러 다시 코드 조각")</span><span class="sxs-lookup"><span data-stu-id="043ba-522">![Press Tab again and the snippet will expand](aspnet-mvc-4-models-and-data-access/_static/image54.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="043ba-523">*확장 하 고 Tab 키를 눌러 다시 코드 조각*</span><span class="sxs-lookup"><span data-stu-id="043ba-523">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="043ba-524">***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1입니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-524">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="043ba-525">코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-525">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="043ba-526">선택 **조각 삽입** 이어서 **내 코드 조각**합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-526">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="043ba-527">클릭 하 여 목록에서 관련 조각을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="043ba-527">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="043ba-528">![코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭](aspnet-mvc-4-models-and-data-access/_static/image55.png "코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추 클릭")</span><span class="sxs-lookup"><span data-stu-id="043ba-528">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-models-and-data-access/_static/image55.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="043ba-529">*코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭*</span><span class="sxs-lookup"><span data-stu-id="043ba-529">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="043ba-530">![클릭 하 여 목록에서 관련 조각을 선택](aspnet-mvc-4-models-and-data-access/_static/image56.png "클릭 하 여 목록에서 관련 조각을 선택")</span><span class="sxs-lookup"><span data-stu-id="043ba-530">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-models-and-data-access/_static/image56.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="043ba-531">*클릭 하 여 목록에서 관련 조각을 선택합니다*</span><span class="sxs-lookup"><span data-stu-id="043ba-531">*Pick the relevant snippet from the list, by clicking on it*</span></span>
