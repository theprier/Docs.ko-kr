---
uid: web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
title: 단위 테스트 ASP.NET Web API 2 | Microsoft Docs
author: Rick-Anderson
description: 이 지침과 응용 프로그램에는 Web API 2 응용 프로그램에 대 한 간단한 단위 테스트를 만드는 방법을 보여 줍니다. 이 자습서에서는 단위 테스트 프로젝트를 포함 하는 방법을 보여 줍니다...
ms.author: riande
ms.date: 06/05/2014
ms.assetid: bf20f78d-ff91-48be-abd1-88e23dcc70ba
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 915610e6646ebe86dd8f16f290ecabd36bf7f48d
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51020834"
---
<a name="unit-testing-aspnet-web-api-2"></a><span data-ttu-id="e9d0b-104">단위 테스트 ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="e9d0b-104">Unit Testing ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="e9d0b-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="e9d0b-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[<span data-ttu-id="e9d0b-106">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="e9d0b-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> <span data-ttu-id="e9d0b-107">이 지침과 응용 프로그램에는 Web API 2 응용 프로그램에 대 한 간단한 단위 테스트를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-107">This guidance and application demonstrate how to create simple unit tests for your Web API 2 application.</span></span> <span data-ttu-id="e9d0b-108">이 자습서에서는 솔루션에 단위 테스트 프로젝트를 포함 하 고 컨트롤러 메서드에서 반환된 된 값을 확인 하는 테스트 메서드를 작성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-108">This tutorial shows how to include a unit test project in your solution, and write test methods that check the returned values from a controller method.</span></span>
>
> <span data-ttu-id="e9d0b-109">이 자습서에서는 ASP.NET Web API의 기본 개념에 익숙하다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-109">This tutorial assumes you are familiar with the basic concepts of ASP.NET Web API.</span></span> <span data-ttu-id="e9d0b-110">입문 용 자습서는를 참조 하세요 [ASP.NET Web API 2 시작](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-110">For an introductory tutorial, see [Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>
>
> <span data-ttu-id="e9d0b-111">이 항목의 단위 테스트를 간단한 데이터 시나리오를 의도적으로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-111">The unit tests in this topic are intentionally limited to simple data scenarios.</span></span> <span data-ttu-id="e9d0b-112">고급 데이터 시나리오를 테스트 하는 장치에 대 한 참조 [Entity Framework 머킹 때 단위 테스트 ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-112">For unit testing more advanced data scenarios, see [Mocking Entity Framework when Unit Testing ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e9d0b-113">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="e9d0b-113">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="e9d0b-114">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="e9d0b-114">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="e9d0b-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="e9d0b-115">Web API 2</span></span>

## <a name="in-this-topic"></a><span data-ttu-id="e9d0b-116">항목 내용</span><span class="sxs-lookup"><span data-stu-id="e9d0b-116">In this topic</span></span>

<span data-ttu-id="e9d0b-117">이 항목에는 다음과 같은 단원이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-117">This topic contains the following sections:</span></span>

- [<span data-ttu-id="e9d0b-118">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="e9d0b-118">Prerequisites</span></span>](#prereqs)
- [<span data-ttu-id="e9d0b-119">코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="e9d0b-119">Download code</span></span>](#download)
- [<span data-ttu-id="e9d0b-120">단위 테스트 프로젝트를 사용 하 여 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="e9d0b-120">Create application with unit test project</span></span>](#appwithunittest)
    - [<span data-ttu-id="e9d0b-121">응용 프로그램을 만들 때 단위 테스트 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="e9d0b-121">Add unit test project when creating the application</span></span>](#whencreate)
    - [<span data-ttu-id="e9d0b-122">기존 응용 프로그램에 단위 테스트 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="e9d0b-122">Add unit test project to an existing application</span></span>](#addtoexisting)
- [<span data-ttu-id="e9d0b-123">Web API 2 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="e9d0b-123">Set up the Web API 2 application</span></span>](#setupproject)
- [<span data-ttu-id="e9d0b-124">테스트 프로젝트에서 NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-124">Install NuGet packages in test project</span></span>](#testpackages)
- [<span data-ttu-id="e9d0b-125">테스트 만들기</span><span class="sxs-lookup"><span data-stu-id="e9d0b-125">Create tests</span></span>](#tests)
- [<span data-ttu-id="e9d0b-126">테스트 실행</span><span class="sxs-lookup"><span data-stu-id="e9d0b-126">Run tests</span></span>](#runtests)

<a id="prereqs"></a>
## <a name="prerequisites"></a><span data-ttu-id="e9d0b-127">전제 조건</span><span class="sxs-lookup"><span data-stu-id="e9d0b-127">Prerequisites</span></span>

<span data-ttu-id="e9d0b-128">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional 또는 Enterprise edition</span><span class="sxs-lookup"><span data-stu-id="e9d0b-128">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional or Enterprise edition</span></span>

<a id="download"></a>
## <a name="download-code"></a><span data-ttu-id="e9d0b-129">코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="e9d0b-129">Download code</span></span>

<span data-ttu-id="e9d0b-130">다운로드 합니다 [완성 된 프로젝트](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-130">Download the [completed project](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span></span> <span data-ttu-id="e9d0b-131">다운로드 가능한 프로젝트 및이 항목에 대 한 단위 테스트 코드를 포함 합니다 [Entity Framework 머킹 때 단위 테스트 ASP.NET Web API](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-131">The downloadable project includes unit test code for this topic and for the [Mocking Entity Framework when Unit Testing ASP.NET Web API](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md) topic.</span></span>

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a><span data-ttu-id="e9d0b-132">단위 테스트 프로젝트를 사용 하 여 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="e9d0b-132">Create application with unit test project</span></span>

<span data-ttu-id="e9d0b-133">응용 프로그램을 만들 때 단위 테스트 프로젝트 만들기 또는 기존 응용 프로그램에 단위 테스트 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-133">You can either create a unit test project when creating your application or add a unit test project to an existing application.</span></span> <span data-ttu-id="e9d0b-134">이 자습서에는 단위 테스트 프로젝트를 만드는 방법을 모두 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-134">This tutorial shows both methods for creating a unit test project.</span></span> <span data-ttu-id="e9d0b-135">이 자습서를 수행 하려면 방법 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-135">To follow this tutorial, you can use either approach.</span></span>

<a id="whencreate"></a>
### <a name="add-unit-test-project-when-creating-the-application"></a><span data-ttu-id="e9d0b-136">응용 프로그램을 만들 때 단위 테스트 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="e9d0b-136">Add unit test project when creating the application</span></span>

<span data-ttu-id="e9d0b-137">명명 된 새 ASP.NET 웹 응용 프로그램 만들기 **StoreApp**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-137">Create a new ASP.NET Web Application named **StoreApp**.</span></span>

![프로젝트 만들기](unit-testing-with-aspnet-web-api/_static/image1.png)

<span data-ttu-id="e9d0b-139">새 ASP.NET 프로젝트 창에서 선택 합니다 **빈** 템플릿 폴더를 추가 하 고 웹 API에 대 한 참조를 핵심입니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-139">In the New ASP.NET Project windows, select the **Empty** template and add folders and core references for Web API.</span></span> <span data-ttu-id="e9d0b-140">선택 된 **단위 테스트 추가** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-140">Select the **Add unit tests** option.</span></span> <span data-ttu-id="e9d0b-141">단위 테스트 프로젝트 이름은 자동으로 **StoreApp.Tests**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-141">The unit test project is automatically named **StoreApp.Tests**.</span></span> <span data-ttu-id="e9d0b-142">이 이름을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-142">You can keep this name.</span></span>

![단위 테스트 프로젝트 만들기](unit-testing-with-aspnet-web-api/_static/image2.png)

<span data-ttu-id="e9d0b-144">응용 프로그램을 만든 후 두 개의 프로젝트가 포함 된 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-144">After creating the application, you will see it contains two projects.</span></span>

![두 프로젝트](unit-testing-with-aspnet-web-api/_static/image3.png)

<a id="addtoexisting"></a>
### <a name="add-unit-test-project-to-an-existing-application"></a><span data-ttu-id="e9d0b-146">기존 응용 프로그램에 단위 테스트 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="e9d0b-146">Add unit test project to an existing application</span></span>

<span data-ttu-id="e9d0b-147">응용 프로그램을 만들 때에 단위 테스트 프로젝트를 만들지 않은, 경우 언제 든 지 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-147">If you did not create the unit test project when you created your application, you can add one at any time.</span></span> <span data-ttu-id="e9d0b-148">예를 들어 이미 StoreApp, 명명 된 응용 프로그램 및 단위 테스트를 추가.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-148">For example, suppose you already have an application named StoreApp, and you want to add unit tests.</span></span> <span data-ttu-id="e9d0b-149">단위 테스트 프로젝트를 추가 하려면 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** 하 고 **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-149">To add a unit test project, right-click your solution and select **Add** and **New Project**.</span></span>

![솔루션에 새 프로젝트 추가](unit-testing-with-aspnet-web-api/_static/image4.png)

<span data-ttu-id="e9d0b-151">선택 **테스트** 선택한 왼쪽된 창의 **단위 테스트 프로젝트** 프로젝트 형식에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-151">Select **Test** in the left pane, and select **Unit Test Project** for the project type.</span></span> <span data-ttu-id="e9d0b-152">프로젝트 이름을 **StoreApp.Tests**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-152">Name the project **StoreApp.Tests**.</span></span>

![단위 테스트 프로젝트 추가](unit-testing-with-aspnet-web-api/_static/image5.png)

<span data-ttu-id="e9d0b-154">솔루션에 단위 테스트 프로젝트가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-154">You will see the unit test project in your solution.</span></span>

<span data-ttu-id="e9d0b-155">단위 테스트 프로젝트에서 원래 프로젝트에 대 한 프로젝트 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-155">In the unit test project, add a project reference to the original project.</span></span>

<a id="setupproject"></a>
## <a name="set-up-the-web-api-2-application"></a><span data-ttu-id="e9d0b-156">Web API 2 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="e9d0b-156">Set up the Web API 2 application</span></span>

<span data-ttu-id="e9d0b-157">StoreApp 프로젝트에서 클래스 파일을 추가 합니다 **모델** 폴더가 **Product.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-157">In your StoreApp project, add a class file to the **Models** folder named **Product.cs**.</span></span> <span data-ttu-id="e9d0b-158">파일의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-158">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="e9d0b-159">솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-159">Build the solution.</span></span>

<span data-ttu-id="e9d0b-160">컨트롤러 폴더를 마우스 오른쪽 단추로 누르고 **추가** 하 고 **새 스 캐 폴드 된 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-160">Right-click the Controllers folder and select **Add** and **New Scaffolded Item**.</span></span> <span data-ttu-id="e9d0b-161">선택 **Web API 2 컨트롤러-비어 있음을**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-161">Select **Web API 2 Controller - Empty**.</span></span>

![새 컨트롤러 추가](unit-testing-with-aspnet-web-api/_static/image6.png)

<span data-ttu-id="e9d0b-163">컨트롤러 이름으로 설정할 **SimpleProductController**, 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-163">Set the controller name to **SimpleProductController**, and click **Add**.</span></span>

![컨트롤러를 지정 합니다.](unit-testing-with-aspnet-web-api/_static/image7.png)

<span data-ttu-id="e9d0b-165">기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-165">Replace the existing code with the following code.</span></span> <span data-ttu-id="e9d0b-166">를 간소화 하기 위해이 예제 데이터는 데이터베이스 보다는 목록에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-166">To simplify this example, the data is stored in a list rather than a database.</span></span> <span data-ttu-id="e9d0b-167">이 클래스에 정의 된 목록에는 프로덕션 데이터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-167">The list defined in this class represents the production data.</span></span> <span data-ttu-id="e9d0b-168">컨트롤러 제품 개체의 목록이 매개 변수로 사용 하는 생성자에 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-168">Notice that the controller includes a constructor that takes as a parameter a list of Product objects.</span></span> <span data-ttu-id="e9d0b-169">이 생성자를 사용 하면 테스트 데이터를 전달할 때 단위 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-169">This constructor enables you to pass test data when unit testing.</span></span> <span data-ttu-id="e9d0b-170">컨트롤러는 또한 두 개의 **비동기** 비동기 메서드를 테스트 하는 단위를 설명 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-170">The controller also includes two **async** methods to illustrate unit testing asynchronous methods.</span></span> <span data-ttu-id="e9d0b-171">이러한 비동기 메서드를 호출 하 여 구현한 **Task.FromResult** 불필요 한 코드 이지만, 일반적으로 메서드를 최소화 하기 위해 리소스 집약적 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-171">These async methods were implemented by calling **Task.FromResult** to minimize extraneous code, but normally the methods would include resource-intensive operations.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="e9d0b-172">GetProduct 메서드의 인스턴스를 반환 합니다 **IHttpActionResult** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-172">The GetProduct method returns an instance of the **IHttpActionResult** interface.</span></span> <span data-ttu-id="e9d0b-173">IHttpActionResult을 사용 하면 Web API 2의 새로운 기능 중 하나인 및 단위 테스트 개발을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-173">IHttpActionResult is one of the new features in Web API 2, and it simplifies unit test development.</span></span> <span data-ttu-id="e9d0b-174">IHttpActionResult 인터페이스를 구현 하는 클래스에서 발견 되는 [System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx) 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-174">Classes that implement the IHttpActionResult interface are found in the [System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx) namespace.</span></span> <span data-ttu-id="e9d0b-175">이러한 클래스는 작업 요청 으로부터 가능한 응답 나타내고 HTTP 상태 코드에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-175">These classes represent possible responses from an action request, and they correspond to HTTP status codes.</span></span>

<span data-ttu-id="e9d0b-176">솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-176">Build the solution.</span></span>

<span data-ttu-id="e9d0b-177">이제 테스트 프로젝트를 설정할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-177">You are now ready to set up the test project.</span></span>

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a><span data-ttu-id="e9d0b-178">테스트 프로젝트에서 NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-178">Install NuGet packages in test project</span></span>

<span data-ttu-id="e9d0b-179">빈 템플릿을 사용 하 여 응용 프로그램을 만들 때 단위 테스트 프로젝트 (StoreApp.Tests)는 설치 된 모든 NuGet 패키지를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-179">When you use the Empty template to create an application, the unit test project (StoreApp.Tests) does not include any installed NuGet packages.</span></span> <span data-ttu-id="e9d0b-180">Web API 템플릿과 같은 다른 템플릿을 단위 테스트 프로젝트에 일부 NuGet 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-180">Other templates, such as the Web API template, include some NuGet packages in the unit test project.</span></span> <span data-ttu-id="e9d0b-181">이 자습서에서는 Microsoft ASP.NET 웹 API 2 코어 패키지를 테스트 프로젝트를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-181">For this tutorial, you must include the Microsoft ASP.NET Web API 2 Core package to the test project.</span></span>

<span data-ttu-id="e9d0b-182">StoreApp.Tests 프로젝트를 마우스 오른쪽 단추로 누르고 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-182">Right-click the StoreApp.Tests project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="e9d0b-183">해당 프로젝트에 패키지를 추가 하려면 StoreApp.Tests 프로젝트를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-183">You must select the StoreApp.Tests project to add the packages to that project.</span></span>

![패키지 관리](unit-testing-with-aspnet-web-api/_static/image8.png)

<span data-ttu-id="e9d0b-185">찾기 및 Microsoft ASP.NET 웹 API 2 코어 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-185">Find and install Microsoft ASP.NET Web API 2 Core package.</span></span>

![웹 api core 패키지를 설치 합니다.](unit-testing-with-aspnet-web-api/_static/image9.png)

<span data-ttu-id="e9d0b-187">NuGet 패키지 관리 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-187">Close the Manage NuGet Packages window.</span></span>

<a id="tests"></a>
## <a name="create-tests"></a><span data-ttu-id="e9d0b-188">테스트 만들기</span><span class="sxs-lookup"><span data-stu-id="e9d0b-188">Create tests</span></span>

<span data-ttu-id="e9d0b-189">테스트 프로젝트는 기본적으로 UnitTest1.cs 이라는 빈 테스트 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-189">By default, your test project includes an empty test file named UnitTest1.cs.</span></span> <span data-ttu-id="e9d0b-190">이 파일을 사용 하면 테스트 메서드를 만들 특성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-190">This file shows the attributes you use to create test methods.</span></span> <span data-ttu-id="e9d0b-191">단위 테스트에 대 한이 파일을 사용 하거나 사용자 고유의 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-191">For your unit tests, you can either use this file or create your own file.</span></span>

![UnitTest1](unit-testing-with-aspnet-web-api/_static/image10.png)

<span data-ttu-id="e9d0b-193">이 자습서에서는 사용자 고유의 테스트 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-193">For this tutorial, you will create your own test class.</span></span> <span data-ttu-id="e9d0b-194">UnitTest1.cs 파일을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-194">You can delete the UnitTest1.cs file.</span></span> <span data-ttu-id="e9d0b-195">라는 클래스를 추가 **TestSimpleProductController.cs**, 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-195">Add a class named **TestSimpleProductController.cs**, and replace the code with the following code.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample3.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a><span data-ttu-id="e9d0b-196">테스트 실행</span><span class="sxs-lookup"><span data-stu-id="e9d0b-196">Run tests</span></span>

<span data-ttu-id="e9d0b-197">이제 테스트를 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-197">You are now ready to run the tests.</span></span> <span data-ttu-id="e9d0b-198">로 표시 되는 메서드의 모든 합니다 **TestMethod** 특성을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-198">All of the method that are marked with the **TestMethod** attribute will be tested.</span></span> <span data-ttu-id="e9d0b-199">**테스트** 메뉴 항목, 테스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-199">From the **Test** menu item, run the tests.</span></span>

![테스트 실행](unit-testing-with-aspnet-web-api/_static/image11.png)

<span data-ttu-id="e9d0b-201">열기는 **테스트 탐색기** 창 테스트의 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-201">Open the **Test Explorer** window, and notice the results of the tests.</span></span>

![테스트 결과](unit-testing-with-aspnet-web-api/_static/image12.png)

## <a name="summary"></a><span data-ttu-id="e9d0b-203">요약</span><span class="sxs-lookup"><span data-stu-id="e9d0b-203">Summary</span></span>

<span data-ttu-id="e9d0b-204">이 자습서를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-204">You have completed this tutorial.</span></span> <span data-ttu-id="e9d0b-205">이 자습서의 데이터는 단위 테스트 조건에 초점을 맞춰 의도적으로 단순화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-205">The data in this tutorial was intentionally simplified to focus on unit testing conditions.</span></span> <span data-ttu-id="e9d0b-206">고급 데이터 시나리오를 테스트 하는 장치에 대 한 참조 [Entity Framework 머킹 때 단위 테스트 ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9d0b-206">For unit testing more advanced data scenarios, see [Mocking Entity Framework when Unit Testing ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span></span>
