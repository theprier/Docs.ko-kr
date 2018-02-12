---
uid: web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
title: "Entity Framework를 모의 때 단위 테스트 ASP.NET Web API 2 | Microsoft Docs"
author: tfitzmac
description: "이 지침과 응용 프로그램에는 Entity Framework를 사용 하는 Web API 2 응용 프로그램에 대 한 단위 테스트를 만드는 방법을 보여 줍니다. 수정 하는 방법을 보여 줍니다는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/13/2013
ms.topic: article
ms.assetid: cd844025-ccad-41ce-8694-595f1022a49f
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: abfde7edec85812de3560f4edefb110c3e374580
ms.sourcegitcommit: 016f4d58663bcd442930227022de23fb3abee0b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
<a name="mocking-entity-framework-when-unit-testing-aspnet-web-api-2"></a><span data-ttu-id="82791-104">Entity Framework를 모의 때 단위 테스트 ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="82791-104">Mocking Entity Framework when Unit Testing ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="82791-105">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="82791-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[<span data-ttu-id="82791-106">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-e2867d4d)

> <span data-ttu-id="82791-107">이 지침과 응용 프로그램에는 Entity Framework를 사용 하는 Web API 2 응용 프로그램에 대 한 단위 테스트를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="82791-107">This guidance and application demonstrate how to create unit tests for your Web API 2 application that uses the Entity Framework.</span></span> <span data-ttu-id="82791-108">테스트를 위해 컨텍스트 개체를 전달할 수 있도록 스 캐 폴드 컨트롤러를 수정 하는 방법과 Entity Framework와 함께 작동 하는 테스트 개체를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="82791-108">It shows how to modify the scaffolded controller to enable passing a context object for testing, and how to create test objects that work with Entity Framework.</span></span>
> 
> <span data-ttu-id="82791-109">ASP.NET Web API를 사용한 단위 테스트에 대 한 소개를 참조 하십시오. [ASP.NET Web API 2를 사용 하 여 단위 테스트](unit-testing-with-aspnet-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-109">For an introduction to unit testing with ASP.NET Web API, see [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md).</span></span>
> 
> <span data-ttu-id="82791-110">이 자습서에서는 ASP.NET Web API의 기본 개념에 익숙한 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-110">This tutorial assumes you are familiar with the basic concepts of ASP.NET Web API.</span></span> <span data-ttu-id="82791-111">있는 소개 자습서를 참조 하십시오. [ASP.NET Web API 2 시작](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-111">For an introductory tutorial, see [Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="82791-112">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="82791-112">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="82791-113">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="82791-113">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/)
> - <span data-ttu-id="82791-114">Web API 2</span><span class="sxs-lookup"><span data-stu-id="82791-114">Web API 2</span></span>


## <a name="in-this-topic"></a><span data-ttu-id="82791-115">항목 내용</span><span class="sxs-lookup"><span data-stu-id="82791-115">In this topic</span></span>

<span data-ttu-id="82791-116">이 항목에는 다음과 같은 단원이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82791-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="82791-117">필수 조건</span><span class="sxs-lookup"><span data-stu-id="82791-117">Prerequisites</span></span>](#prereqs)
- [<span data-ttu-id="82791-118">코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="82791-118">Download code</span></span>](#download)
- [<span data-ttu-id="82791-119">응용 프로그램 단위 테스트 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="82791-119">Create application with unit test project</span></span>](#appwithunittest)
- [<span data-ttu-id="82791-120">모델 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="82791-120">Create the model class</span></span>](#modelclass)
- [<span data-ttu-id="82791-121">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="82791-121">Add the controller</span></span>](#controller)
- [<span data-ttu-id="82791-122">추가 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="82791-122">Add dependency injection</span></span>](#dependency)
- [<span data-ttu-id="82791-123">테스트 프로젝트에서 NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-123">Install NuGet packages in test project</span></span>](#testpackages)
- [<span data-ttu-id="82791-124">테스트 컨텍스트 만들기</span><span class="sxs-lookup"><span data-stu-id="82791-124">Create test context</span></span>](#testcontext)
- [<span data-ttu-id="82791-125">테스트 만들기</span><span class="sxs-lookup"><span data-stu-id="82791-125">Create tests</span></span>](#tests)
- [<span data-ttu-id="82791-126">테스트 실행</span><span class="sxs-lookup"><span data-stu-id="82791-126">Run tests</span></span>](#runtests)

<span data-ttu-id="82791-127">단계를 이미 완료 한 경우 [ASP.NET Web API 2를 사용 하 여 단위 테스트](unit-testing-with-aspnet-web-api.md), 섹션으로 건너뛸 수 [컨트롤러 추가](#controller)합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-127">If you have already completed the steps in [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), you can skip to the section [Add the controller](#controller).</span></span>

<a id="prereqs"></a>
## <a name="prerequisites"></a><span data-ttu-id="82791-128">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="82791-128">Prerequisites</span></span>

<span data-ttu-id="82791-129">Visual Studio 2017 Community, Professional 또는 Enterprise edition</span><span class="sxs-lookup"><span data-stu-id="82791-129">Visual Studio 2017 Community, Professional or Enterprise edition</span></span>

<a id="download"></a>
## <a name="download-code"></a><span data-ttu-id="82791-130">코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="82791-130">Download code</span></span>

<span data-ttu-id="82791-131">다운로드는 [완료 된 프로젝트](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-131">Download the [completed project](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span></span> <span data-ttu-id="82791-132">및이 항목에 대 한 단위 테스트 코드를 포함 하는 다운로드 가능한 프로젝트는 [단위 테스트 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="82791-132">The downloadable project includes unit test code for this topic and for the [Unit Testing ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md) topic.</span></span>

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a><span data-ttu-id="82791-133">응용 프로그램 단위 테스트 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="82791-133">Create application with unit test project</span></span>

<span data-ttu-id="82791-134">응용 프로그램을 만들 때 단위 테스트 프로젝트를 만들 하거나 기존 응용 프로그램 단위 테스트 프로젝트를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82791-134">You can either create a unit test project when creating your application or add a unit test project to an existing application.</span></span> <span data-ttu-id="82791-135">이 자습서에서는 응용 프로그램을 만들 때 단위 테스트 프로젝트를 만드는 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-135">This tutorial shows creating a unit test project when creating the application.</span></span>

<span data-ttu-id="82791-136">라는 새 ASP.NET 웹 응용 프로그램 만들기 **StoreApp**합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-136">Create a new ASP.NET Web Application named **StoreApp**.</span></span>

<span data-ttu-id="82791-137">새 ASP.NET 프로젝트 창, 선택는 **빈** 템플릿 폴더를 추가 하 고 웹 API에 대 한 참조를 핵심입니다.</span><span class="sxs-lookup"><span data-stu-id="82791-137">In the New ASP.NET Project windows, select the **Empty** template and add folders and core references for Web API.</span></span> <span data-ttu-id="82791-138">선택 된 **단위 테스트 추가** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="82791-138">Select the **Add unit tests** option.</span></span> <span data-ttu-id="82791-139">단위 테스트 프로젝트의 이름이 자동으로 **StoreApp.Tests**합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-139">The unit test project is automatically named **StoreApp.Tests**.</span></span> <span data-ttu-id="82791-140">이 이름을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82791-140">You can keep this name.</span></span>

![단위 테스트 프로젝트 만들기](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image1.png)

<span data-ttu-id="82791-142">응용 프로그램을 만든 후 나타납니다-두 개의 프로젝트가 포함 된 **StoreApp** 및 **StoreApp.Tests**합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-142">After creating the application, you will see it contains two projects - **StoreApp** and **StoreApp.Tests**.</span></span>

<a id="modelclass"></a>
## <a name="create-the-model-class"></a><span data-ttu-id="82791-143">모델 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="82791-143">Create the model class</span></span>

<span data-ttu-id="82791-144">StoreApp 프로젝트에 클래스 파일을 추가 **모델** 라는 폴더 **Product.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-144">In your StoreApp project, add a class file to the **Models** folder named **Product.cs**.</span></span> <span data-ttu-id="82791-145">파일의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="82791-145">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample1.cs)]

<span data-ttu-id="82791-146">솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-146">Build the solution.</span></span>

<a id="controller"></a>
## <a name="add-the-controller"></a><span data-ttu-id="82791-147">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="82791-147">Add the controller</span></span>

<span data-ttu-id="82791-148">Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** 및 **스 캐 폴드 된 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-148">Right-click the Controllers folder and select **Add** and **New Scaffolded Item**.</span></span> <span data-ttu-id="82791-149">Entity Framework를 사용 하 여 동작이 포함 된 Web API 2 컨트롤러를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-149">Select Web API 2 Controller with actions, using Entity Framework.</span></span>

![새 컨트롤러 추가](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image2.png)

<span data-ttu-id="82791-151">다음 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-151">Set the following values:</span></span>

- <span data-ttu-id="82791-152">컨트롤러 이름: **ProductController**</span><span class="sxs-lookup"><span data-stu-id="82791-152">Controller name: **ProductController**</span></span>
- <span data-ttu-id="82791-153">모델 클래스: **제품**</span><span class="sxs-lookup"><span data-stu-id="82791-153">Model class: **Product**</span></span>
- <span data-ttu-id="82791-154">데이터 컨텍스트 클래스: [선택 **새 데이터 컨텍스트에** 아래 에서처럼 값을 입력 하는 단추]</span><span class="sxs-lookup"><span data-stu-id="82791-154">Data context class: [Select **New data context** button which fills in the values seen below]</span></span>

![컨트롤러를 지정 합니다.](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image3.png)

<span data-ttu-id="82791-156">클릭 **추가** 컨트롤러 자동으로 생성 된 코드를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-156">Click **Add** to create the controller with automatically-generated code.</span></span> <span data-ttu-id="82791-157">코드 생성, 검색, 업데이트 및 제품 클래스의 인스턴스를 삭제 하기 위한 메서드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-157">The code includes methods for creating, retrieving, updating and deleting instances of the Product class.</span></span> <span data-ttu-id="82791-158">다음 코드는 메서드를 보여 줍니다.에 대 한 제품을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-158">The following code shows the method for add a Product.</span></span> <span data-ttu-id="82791-159">메서드가의 인스턴스를 반환 한다고 확인 **IHttpActionResult**합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-159">Notice that the method returns an instance of **IHttpActionResult**.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample2.cs)]

<span data-ttu-id="82791-160">IHttpActionResult Web API 2의 새로운 기능 중 하나 이며 단위 테스트 개발을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-160">IHttpActionResult is one of the new features in Web API 2, and it simplifies unit test development.</span></span>

<span data-ttu-id="82791-161">다음 섹션에서 사용자 지정할 용이 하 게 생성 된 코드는 컨트롤러에 테스트 개체를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-161">In the next section, you will customize the generated code to facilitate passing test objects to the controller.</span></span>

<a id="dependency"></a>
## <a name="add-dependency-injection"></a><span data-ttu-id="82791-162">추가 종속성 주입</span><span class="sxs-lookup"><span data-stu-id="82791-162">Add dependency injection</span></span>

<span data-ttu-id="82791-163">현재 ProductController 클래스 StoreAppContext 클래스의 인스턴스를 사용 하도록 하드 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="82791-163">Currently, the ProductController class is hard-coded to use an instance of the StoreAppContext class.</span></span> <span data-ttu-id="82791-164">응용 프로그램을 수정 하 고 해당 하드 코드 된 종속성을 제거 하는 종속성 주입 이라는 패턴을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-164">You will use a pattern called dependency injection to modify your application and remove that hard-coded dependency.</span></span> <span data-ttu-id="82791-165">이 종속성을 끊음 으로써 테스트할 때 모의 개체에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82791-165">By breaking this dependency, you can pass in a mock object when testing.</span></span>

<span data-ttu-id="82791-166">마우스 오른쪽 단추로 클릭는 **모델** 폴더 라는 새 인터페이스를 추가 하 고 **IStoreAppContext**합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-166">Right-click the **Models** folder, and add a new interface named **IStoreAppContext**.</span></span>

<span data-ttu-id="82791-167">코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="82791-167">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample3.cs)]

<span data-ttu-id="82791-168">StoreAppContext.cs 파일을 열고 다음 강조 표시 된 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-168">Open the StoreAppContext.cs file and make the following highlighted changes.</span></span> <span data-ttu-id="82791-169">에 중요 한 변경이 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-169">The important changes to note are:</span></span>

- <span data-ttu-id="82791-170">StoreAppContext 클래스 IStoreAppContext 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-170">StoreAppContext class implements IStoreAppContext interface</span></span>
- <span data-ttu-id="82791-171">MarkAsModified 메서드는 구현</span><span class="sxs-lookup"><span data-stu-id="82791-171">MarkAsModified method is implemented</span></span>


[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample4.cs?highlight=6,14-17)]

<span data-ttu-id="82791-172">ProductController.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="82791-172">Open the ProductController.cs file.</span></span> <span data-ttu-id="82791-173">강조 표시 된 코드와 일치 하도록 기존 코드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-173">Change the existing code to match the highlighted code.</span></span> <span data-ttu-id="82791-174">이러한 변경 내용은 StoreAppContext에 종속성을 해제 하 고 상황에 맞는 클래스에 대 한 다른 개체에 전달 하는 다른 클래스를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-174">These changes break the dependency on StoreAppContext and enable other classes to pass in a different object for the context class.</span></span> <span data-ttu-id="82791-175">이렇게이 변경을 사용 하면 단위 테스트 중 테스트 컨텍스트에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82791-175">This change will enable you to pass in a test context during unit tests.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample5.cs?highlight=4,7-12)]

<span data-ttu-id="82791-176">ProductController에서 수행 해야 하는 한 가지 더 많은 변경이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82791-176">There is one more change you must make in ProductController.</span></span> <span data-ttu-id="82791-177">에 **PutProduct** 메서드, replace 엔터티 상태를 설정 하는 줄 MarkAsModified 메서드를 호출 하 여 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-177">In the **PutProduct** method, replace the line that sets the entity state to modified with a call to the MarkAsModified method.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample6.cs?highlight=14-15)]

<span data-ttu-id="82791-178">솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-178">Build the solution.</span></span>

<span data-ttu-id="82791-179">이제 테스트 프로젝트를 설정할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="82791-179">You are now ready to set up the test project.</span></span>

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a><span data-ttu-id="82791-180">테스트 프로젝트에서 NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-180">Install NuGet packages in test project</span></span>

<span data-ttu-id="82791-181">빈 서식 파일을 사용 하 여 응용 프로그램을 만들 때 단위 테스트 프로젝트 (StoreApp.Tests)는 모든 설치 된 NuGet 패키지를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="82791-181">When you use the Empty template to create an application, the unit test project (StoreApp.Tests) does not include any installed NuGet packages.</span></span> <span data-ttu-id="82791-182">단위 테스트 프로젝트에서 일부 NuGet 패키지를 포함 하는 Web API 템플릿 같은 다른 서식 파일.</span><span class="sxs-lookup"><span data-stu-id="82791-182">Other templates, such as the Web API template, include some NuGet packages in the unit test project.</span></span> <span data-ttu-id="82791-183">이 자습서에서는 Entity Framework packge와 테스트 프로젝트에 Microsoft ASP.NET Web API 2 Core 패키지를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-183">For this tutorial, you must include the Entity Framework packge and the Microsoft ASP.NET Web API 2 Core package to the test project.</span></span>

<span data-ttu-id="82791-184">StoreApp.Tests 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-184">Right-click the StoreApp.Tests project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="82791-185">해당 프로젝트에 패키지를 추가 하려면 StoreApp.Tests 프로젝트를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-185">You must select the StoreApp.Tests project to add the packages to that project.</span></span>

![패키지 관리](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image4.png)

<span data-ttu-id="82791-187">온라인 패키지를 찾아 EntityFramework 패키지 (버전 6.0 이상)를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-187">From the Online packages, find and install the EntityFramework package (version 6.0 or later).</span></span> <span data-ttu-id="82791-188">EntityFramework 패키지가 이미 설치 되어 있는지, 표시 되는 경우 StoreApp.Tests 프로젝트 대신 StoreApp 프로젝트를 선택 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82791-188">If it appears that the EntityFramework package is already installed, you may have selected the StoreApp project instead of the StoreApp.Tests project.</span></span>

![엔터티 프레임 워크 추가](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image5.png)

<span data-ttu-id="82791-190">찾기 및 Microsoft ASP.NET Web API 2 Core 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-190">Find and install Microsoft ASP.NET Web API 2 Core package.</span></span>

![web api core 패키지를 설치 합니다.](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image6.png)

<span data-ttu-id="82791-192">NuGet 패키지 관리 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="82791-192">Close the Manage NuGet Packages window.</span></span>

<a id="testcontext"></a>
## <a name="create-test-context"></a><span data-ttu-id="82791-193">테스트 컨텍스트 만들기</span><span class="sxs-lookup"><span data-stu-id="82791-193">Create test context</span></span>

<span data-ttu-id="82791-194">라는 클래스를 추가 **TestDbSet** 테스트 프로젝트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82791-194">Add a class named **TestDbSet** to the test project.</span></span> <span data-ttu-id="82791-195">이 클래스는 테스트 데이터 집합에 대 한 기본 클래스로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82791-195">This class serves as the base class for your test data set.</span></span> <span data-ttu-id="82791-196">코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="82791-196">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample7.cs)]

<span data-ttu-id="82791-197">라는 클래스를 추가 **TestProductDbSet** 다음 코드를 포함 하는 테스트 프로젝트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82791-197">Add a class named **TestProductDbSet** to the test project which contains the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample8.cs)]

<span data-ttu-id="82791-198">라는 클래스를 추가 **TestStoreAppContext** 기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="82791-198">Add a class named **TestStoreAppContext** and replace the existing code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample9.cs)]

<a id="tests"></a>
## <a name="create-tests"></a><span data-ttu-id="82791-199">테스트 만들기</span><span class="sxs-lookup"><span data-stu-id="82791-199">Create tests</span></span>

<span data-ttu-id="82791-200">기본적으로 테스트 프로젝트에 빈 테스트 파일인 **UnitTest1.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-200">By default, your test project includes an empty test file named **UnitTest1.cs**.</span></span> <span data-ttu-id="82791-201">이 파일을 사용 하면 테스트 메서드를 만들 특성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="82791-201">This file shows the attributes you use to create test methods.</span></span> <span data-ttu-id="82791-202">이 자습서에서는 새 테스트 클래스를 추가 하기 때문에이 파일을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82791-202">For this tutorial, you can delete this file because you will add a new test class.</span></span>

<span data-ttu-id="82791-203">라는 클래스를 추가 **TestProductController** 테스트 프로젝트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82791-203">Add a class named **TestProductController** to the test project.</span></span> <span data-ttu-id="82791-204">코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="82791-204">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample10.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a><span data-ttu-id="82791-205">테스트 실행</span><span class="sxs-lookup"><span data-stu-id="82791-205">Run tests</span></span>

<span data-ttu-id="82791-206">이제 테스트를 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="82791-206">You are now ready to run the tests.</span></span> <span data-ttu-id="82791-207">로 표시 된 메서드의 모든는 **TestMethod** 특성을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-207">All of the method that are marked with the **TestMethod** attribute will be tested.</span></span> <span data-ttu-id="82791-208">**테스트** 메뉴 항목을 테스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-208">From the **Test** menu item, run the tests.</span></span>

![테스트 실행](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image7.png)

<span data-ttu-id="82791-210">열기는 **테스트 탐색기** 창 테스트의 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="82791-210">Open the **Test Explorer** window, and notice the results of the tests.</span></span>

![테스트 결과](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image8.png)
