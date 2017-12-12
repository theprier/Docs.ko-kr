---
uid: web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
title: "단위 테스트 ASP.NET Web API 2 | Microsoft Docs"
author: tfitzmac
description: "이 지침과 응용 프로그램에는 Web API 2 응용 프로그램에 대 한 간단한 단위 테스트를 만드는 방법을 보여 줍니다. 단위 테스트 프로젝트를 포함 하는 방법을 보여 주는이 자습서 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/05/2014
ms.topic: article
ms.assetid: bf20f78d-ff91-48be-abd1-88e23dcc70ba
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 13211ee4543e17a4bfb2f83495f4041880f37df2
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="unit-testing-aspnet-web-api-2"></a><span data-ttu-id="a89d1-104">단위 테스트 ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="a89d1-104">Unit Testing ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="a89d1-105">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="a89d1-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[<span data-ttu-id="a89d1-106">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-e2867d4d)

> <span data-ttu-id="a89d1-107">이 지침과 응용 프로그램에는 Web API 2 응용 프로그램에 대 한 간단한 단위 테스트를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-107">This guidance and application demonstrate how to create simple unit tests for your Web API 2 application.</span></span> <span data-ttu-id="a89d1-108">이 자습서, 솔루션의 단위 테스트 프로젝트를 포함 하 고 컨트롤러 메서드에서 반환 된 값을 확인 하는 테스트 메서드를 작성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-108">This tutorial shows how to include a unit test project in your solution, and write test methods that check the returned values from a controller method.</span></span>
> 
> <span data-ttu-id="a89d1-109">이 자습서에서는 ASP.NET Web API의 기본 개념에 익숙한 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-109">This tutorial assumes you are familiar with the basic concepts of ASP.NET Web API.</span></span> <span data-ttu-id="a89d1-110">있는 소개 자습서를 참조 하십시오. [ASP.NET Web API 2 시작](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-110">For an introductory tutorial, see [Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>
> 
> <span data-ttu-id="a89d1-111">이 항목의 단위 테스트는 의도적으로 간단한 데이터 시나리오로 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-111">The unit tests in this topic are intentionally limited to simple data scenarios.</span></span> <span data-ttu-id="a89d1-112">단위 테스트 고급 데이터 시나리오에 대 한 참조 [Entity Framework 모의 때 단위 테스트 ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-112">For unit testing more advanced data scenarios, see [Mocking Entity Framework when Unit Testing ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a89d1-113">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="a89d1-113">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="a89d1-114">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="a89d1-114">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/)
> - <span data-ttu-id="a89d1-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="a89d1-115">Web API 2</span></span>


## <a name="in-this-topic"></a><span data-ttu-id="a89d1-116">항목 내용</span><span class="sxs-lookup"><span data-stu-id="a89d1-116">In this topic</span></span>

<span data-ttu-id="a89d1-117">이 항목에는 다음과 같은 단원이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-117">This topic contains the following sections:</span></span>

- [<span data-ttu-id="a89d1-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a89d1-118">Prerequisites</span></span>](#prereqs)
- [<span data-ttu-id="a89d1-119">코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="a89d1-119">Download code</span></span>](#download)
- [<span data-ttu-id="a89d1-120">응용 프로그램 단위 테스트 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="a89d1-120">Create application with unit test project</span></span>](#appwithunittest)

    - [<span data-ttu-id="a89d1-121">응용 프로그램을 만들 때 단위 테스트 프로젝트에 추가</span><span class="sxs-lookup"><span data-stu-id="a89d1-121">Add unit test project when creating the application</span></span>](#whencreate)
    - [<span data-ttu-id="a89d1-122">기존 응용 프로그램에 단위 테스트 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="a89d1-122">Add unit test project to an existing application</span></span>](#addtoexisting)
- [<span data-ttu-id="a89d1-123">Web API 2 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="a89d1-123">Set up the Web API 2 application</span></span>](#setupproject)
- [<span data-ttu-id="a89d1-124">테스트 프로젝트에서 NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-124">Install NuGet packages in test project</span></span>](#testpackages)
- [<span data-ttu-id="a89d1-125">테스트 만들기</span><span class="sxs-lookup"><span data-stu-id="a89d1-125">Create tests</span></span>](#tests)
- [<span data-ttu-id="a89d1-126">테스트 실행</span><span class="sxs-lookup"><span data-stu-id="a89d1-126">Run tests</span></span>](#runtests)

<a id="prereqs"></a>
## <a name="prerequisites"></a><span data-ttu-id="a89d1-127">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="a89d1-127">Prerequisites</span></span>

<span data-ttu-id="a89d1-128">Visual Studio 2017 Community, Professional 또는 Enterprise edition</span><span class="sxs-lookup"><span data-stu-id="a89d1-128">Visual Studio 2017 Community, Professional or Enterprise edition</span></span>

<a id="download"></a>
## <a name="download-code"></a><span data-ttu-id="a89d1-129">코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="a89d1-129">Download code</span></span>

<span data-ttu-id="a89d1-130">다운로드는 [완료 된 프로젝트](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-130">Download the [completed project](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span></span> <span data-ttu-id="a89d1-131">및이 항목에 대 한 단위 테스트 코드를 포함 하는 다운로드 가능한 프로젝트는 [Entity Framework 모의 때 단위 테스트 ASP.NET Web API](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-131">The downloadable project includes unit test code for this topic and for the [Mocking Entity Framework when Unit Testing ASP.NET Web API](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md) topic.</span></span>

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a><span data-ttu-id="a89d1-132">응용 프로그램 단위 테스트 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="a89d1-132">Create application with unit test project</span></span>

<span data-ttu-id="a89d1-133">응용 프로그램을 만들 때 단위 테스트 프로젝트를 만들 하거나 기존 응용 프로그램 단위 테스트 프로젝트를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-133">You can either create a unit test project when creating your application or add a unit test project to an existing application.</span></span> <span data-ttu-id="a89d1-134">이 자습서에는 단위 테스트 프로젝트를 만들기 위한 두 메서드 모두 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-134">This tutorial shows both methods for creating a unit test project.</span></span> <span data-ttu-id="a89d1-135">이 자습서를 수행 하려면 방법 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-135">To follow this tutorial, you can use either approach.</span></span>

<a id="whencreate"></a>
### <a name="add-unit-test-project-when-creating-the-application"></a><span data-ttu-id="a89d1-136">응용 프로그램을 만들 때 단위 테스트 프로젝트에 추가</span><span class="sxs-lookup"><span data-stu-id="a89d1-136">Add unit test project when creating the application</span></span>

<span data-ttu-id="a89d1-137">라는 새 ASP.NET 웹 응용 프로그램 만들기 **StoreApp**합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-137">Create a new ASP.NET Web Application named **StoreApp**.</span></span>

![프로젝트 만들기](unit-testing-with-aspnet-web-api/_static/image1.png)

<span data-ttu-id="a89d1-139">새 ASP.NET 프로젝트 창, 선택는 **빈** 템플릿 폴더를 추가 하 고 웹 API에 대 한 참조를 핵심입니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-139">In the New ASP.NET Project windows, select the **Empty** template and add folders and core references for Web API.</span></span> <span data-ttu-id="a89d1-140">선택 된 **단위 테스트 추가** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-140">Select the **Add unit tests** option.</span></span> <span data-ttu-id="a89d1-141">단위 테스트 프로젝트의 이름이 자동으로 **StoreApp.Tests**합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-141">The unit test project is automatically named **StoreApp.Tests**.</span></span> <span data-ttu-id="a89d1-142">이 이름을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-142">You can keep this name.</span></span>

![단위 테스트 프로젝트 만들기](unit-testing-with-aspnet-web-api/_static/image2.png)

<span data-ttu-id="a89d1-144">응용 프로그램을 만든 후 두 개의 프로젝트가 포함 된 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-144">After creating the application, you will see it contains two projects.</span></span>

![두 개의 프로젝트](unit-testing-with-aspnet-web-api/_static/image3.png)

<a id="addtoexisting"></a>
### <a name="add-unit-test-project-to-an-existing-application"></a><span data-ttu-id="a89d1-146">기존 응용 프로그램에 단위 테스트 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="a89d1-146">Add unit test project to an existing application</span></span>

<span data-ttu-id="a89d1-147">응용 프로그램을 만들 때 단위 테스트 프로젝트를 만들지 않은, 언제 든 지 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-147">If you did not create the unit test project when you created your application, you can add one at any time.</span></span> <span data-ttu-id="a89d1-148">예를 들어 StoreApp, 이라는 응용 프로그램에 이미 있는데 단위 테스트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-148">For example, suppose you already have an application named StoreApp, and you want to add unit tests.</span></span> <span data-ttu-id="a89d1-149">단위 테스트 프로젝트를 추가 하려면 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** 및 **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-149">To add a unit test project, right-click your solution and select **Add** and **New Project**.</span></span>

![새 프로젝트를 솔루션에 추가](unit-testing-with-aspnet-web-api/_static/image4.png)

<span data-ttu-id="a89d1-151">선택 **테스트** 고 왼쪽된 창에서 **단위 테스트 프로젝트** 프로젝트 형식에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-151">Select **Test** in the left pane, and select **Unit Test Project** for the project type.</span></span> <span data-ttu-id="a89d1-152">프로젝트 이름을 **StoreApp.Tests**합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-152">Name the project **StoreApp.Tests**.</span></span>

![단위 테스트 프로젝트에 추가](unit-testing-with-aspnet-web-api/_static/image5.png)

<span data-ttu-id="a89d1-154">솔루션에 단위 테스트 프로젝트에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-154">You will see the unit test project in your solution.</span></span>

<span data-ttu-id="a89d1-155">단위 테스트 프로젝트에서 원래 프로젝트에 대 한 프로젝트 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-155">In the unit test project, add a project reference to the original project.</span></span>

<a id="setupproject"></a>
## <a name="set-up-the-web-api-2-application"></a><span data-ttu-id="a89d1-156">Web API 2 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="a89d1-156">Set up the Web API 2 application</span></span>

<span data-ttu-id="a89d1-157">StoreApp 프로젝트에 클래스 파일을 추가 **모델** 라는 폴더 **Product.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-157">In your StoreApp project, add a class file to the **Models** folder named **Product.cs**.</span></span> <span data-ttu-id="a89d1-158">파일의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-158">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="a89d1-159">솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-159">Build the solution.</span></span>

<span data-ttu-id="a89d1-160">Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** 및 **스 캐 폴드 된 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-160">Right-click the Controllers folder and select **Add** and **New Scaffolded Item**.</span></span> <span data-ttu-id="a89d1-161">선택 **Web API 2 컨트롤러-빈**합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-161">Select **Web API 2 Controller - Empty**.</span></span>

![새 컨트롤러 추가](unit-testing-with-aspnet-web-api/_static/image6.png)

<span data-ttu-id="a89d1-163">컨트롤러 이름을 설정 **SimpleProductController**를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-163">Set the controller name to **SimpleProductController**, and click **Add**.</span></span>

![컨트롤러를 지정 합니다.](unit-testing-with-aspnet-web-api/_static/image7.png)

<span data-ttu-id="a89d1-165">기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-165">Replace the existing code with the following code.</span></span> <span data-ttu-id="a89d1-166">를 간소화 하기 위해이 예에서는 데이터는 데이터베이스 보다는 목록에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-166">To simplify this example, the data is stored in a list rather than a database.</span></span> <span data-ttu-id="a89d1-167">이 클래스에 정의 된 목록이 프로덕션 데이터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-167">The list defined in this class represents the production data.</span></span> <span data-ttu-id="a89d1-168">제품 개체 목록을 매개 변수로 사용 하는 생성자를 포함 하는 컨트롤러를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-168">Notice that the controller includes a constructor that takes as a parameter a list of Product objects.</span></span> <span data-ttu-id="a89d1-169">이 생성자를 사용 하면 테스트 데이터를 전달 하는 경우 단위 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-169">This constructor enables you to pass test data when unit testing.</span></span> <span data-ttu-id="a89d1-170">컨트롤러도 두 개의 **비동기** 단위 테스트 비동기 메서드를 설명 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="a89d1-170">The controller also includes two **async** methods to illustrate unit testing asynchronous methods.</span></span> <span data-ttu-id="a89d1-171">이러한 비동기 메서드를 호출 하 여 구현 된 **Task.FromResult** 불필요 한 코드 있지만 일반적으로 메서드를 최소화 하기 위해 리소스 중심 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-171">These async methods were implemented by calling **Task.FromResult** to minimize extraneous code, but normally the methods would include resource-intensive operations.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="a89d1-172">인스턴스를 반환 하는 GetProduct 메서드는 **IHttpActionResult** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-172">The GetProduct method returns an instance of the **IHttpActionResult** interface.</span></span> <span data-ttu-id="a89d1-173">IHttpActionResult Web API 2의 새로운 기능 중 하나 이며 단위 테스트 개발을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-173">IHttpActionResult is one of the new features in Web API 2, and it simplifies unit test development.</span></span> <span data-ttu-id="a89d1-174">IHttpActionResult 인터페이스를 구현 하는 클래스에서 발견 되는 [System.Web.Http.Results](https://msdn.microsoft.com/en-us/library/system.web.http.results.aspx) 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-174">Classes that implement the IHttpActionResult interface are found in the [System.Web.Http.Results](https://msdn.microsoft.com/en-us/library/system.web.http.results.aspx) namespace.</span></span> <span data-ttu-id="a89d1-175">이러한 클래스 동작 요청에 대 한 가능한 응답을 나타내고 HTTP 상태 코드에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-175">These classes represent possible responses from an action request, and they correspond to HTTP status codes.</span></span>

<span data-ttu-id="a89d1-176">솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-176">Build the solution.</span></span>

<span data-ttu-id="a89d1-177">이제 테스트 프로젝트를 설정할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-177">You are now ready to set up the test project.</span></span>

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a><span data-ttu-id="a89d1-178">테스트 프로젝트에서 NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-178">Install NuGet packages in test project</span></span>

<span data-ttu-id="a89d1-179">빈 서식 파일을 사용 하 여 응용 프로그램을 만들 때 단위 테스트 프로젝트 (StoreApp.Tests)는 모든 설치 된 NuGet 패키지를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-179">When you use the Empty template to create an application, the unit test project (StoreApp.Tests) does not include any installed NuGet packages.</span></span> <span data-ttu-id="a89d1-180">단위 테스트 프로젝트에서 일부 NuGet 패키지를 포함 하는 Web API 템플릿 같은 다른 서식 파일.</span><span class="sxs-lookup"><span data-stu-id="a89d1-180">Other templates, such as the Web API template, include some NuGet packages in the unit test project.</span></span> <span data-ttu-id="a89d1-181">이 자습서에서는 Microsoft ASP.NET Web API 2 코어 패키지 테스트 프로젝트를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-181">For this tutorial, you must include the Microsoft ASP.NET Web API 2 Core package to the test project.</span></span>

<span data-ttu-id="a89d1-182">StoreApp.Tests 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-182">Right-click the StoreApp.Tests project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="a89d1-183">해당 프로젝트에 패키지를 추가 하려면 StoreApp.Tests 프로젝트를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-183">You must select the StoreApp.Tests project to add the packages to that project.</span></span>

![패키지 관리](unit-testing-with-aspnet-web-api/_static/image8.png)

<span data-ttu-id="a89d1-185">찾기 및 Microsoft ASP.NET Web API 2 Core 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-185">Find and install Microsoft ASP.NET Web API 2 Core package.</span></span>

![web api core 패키지를 설치 합니다.](unit-testing-with-aspnet-web-api/_static/image9.png)

<span data-ttu-id="a89d1-187">NuGet 패키지 관리 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-187">Close the Manage NuGet Packages window.</span></span>

<a id="tests"></a>
## <a name="create-tests"></a><span data-ttu-id="a89d1-188">테스트 만들기</span><span class="sxs-lookup"><span data-stu-id="a89d1-188">Create tests</span></span>

<span data-ttu-id="a89d1-189">기본적으로 테스트 프로젝트 UnitTest1.cs 라는 빈 테스트 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-189">By default, your test project includes an empty test file named UnitTest1.cs.</span></span> <span data-ttu-id="a89d1-190">이 파일을 사용 하면 테스트 메서드를 만들 특성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-190">This file shows the attributes you use to create test methods.</span></span> <span data-ttu-id="a89d1-191">단위 테스트에 대 한이 파일을 사용 하거나 직접 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-191">For your unit tests, you can either use this file or create your own file.</span></span>

![UnitTest1](unit-testing-with-aspnet-web-api/_static/image10.png)

<span data-ttu-id="a89d1-193">이 자습서에서는 사용자 고유의 테스트 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-193">For this tutorial, you will create your own test class.</span></span> <span data-ttu-id="a89d1-194">UnitTest1.cs 파일을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-194">You can delete the UnitTest1.cs file.</span></span> <span data-ttu-id="a89d1-195">라는 클래스를 추가 **TestSimpleProductController.cs**, 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-195">Add a class named **TestSimpleProductController.cs**, and replace the code with the following code.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample3.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a><span data-ttu-id="a89d1-196">테스트 실행</span><span class="sxs-lookup"><span data-stu-id="a89d1-196">Run tests</span></span>

<span data-ttu-id="a89d1-197">이제 테스트를 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-197">You are now ready to run the tests.</span></span> <span data-ttu-id="a89d1-198">로 표시 된 메서드의 모든는 **TestMethod** 특성을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-198">All of the method that are marked with the **TestMethod** attribute will be tested.</span></span> <span data-ttu-id="a89d1-199">**테스트** 메뉴 항목을 테스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-199">From the **Test** menu item, run the tests.</span></span>

![테스트 실행](unit-testing-with-aspnet-web-api/_static/image11.png)

<span data-ttu-id="a89d1-201">열기는 **테스트 탐색기** 창 테스트의 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-201">Open the **Test Explorer** window, and notice the results of the tests.</span></span>

![테스트 결과](unit-testing-with-aspnet-web-api/_static/image12.png)

## <a name="summary"></a><span data-ttu-id="a89d1-203">요약</span><span class="sxs-lookup"><span data-stu-id="a89d1-203">Summary</span></span>

<span data-ttu-id="a89d1-204">이 자습서를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-204">You have completed this tutorial.</span></span> <span data-ttu-id="a89d1-205">이 자습서의 데이터는 단위 테스트 조건에 초점을 의도적으로 단순화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-205">The data in this tutorial was intentionally simplified to focus on unit testing conditions.</span></span> <span data-ttu-id="a89d1-206">단위 테스트 고급 데이터 시나리오에 대 한 참조 [Entity Framework 모의 때 단위 테스트 ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a89d1-206">For unit testing more advanced data scenarios, see [Mocking Entity Framework when Unit Testing ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span></span>
