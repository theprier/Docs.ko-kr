---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
title: ASP.NET Web API 2.2 사용 하 여 OData v4 엔드포인트 만들기 | Microsoft Docs
author: MikeWasson
description: Open Data Protocol (OData)는 웹에 대 한 데이터 액세스 프로토콜. OData 쿼리 및 CRUD 작업을 통해 데이터 집합을 조작할 일관 된 방식으로 제공 하는 중...
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 1e1927c0-ded1-4752-80fd-a146628d2f09
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
msc.type: authoredcontent
ms.openlocfilehash: c6a4aa4eb563fd77d5afd9248175d5f5b7984d19
ms.sourcegitcommit: ed76cc752966c604a795fbc56d5a71d16ded0b58
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55667572"
---
# <a name="create-an-odata-v4-endpoint-using-aspnet-web-api"></a><span data-ttu-id="2d6fa-104">ASP.NET Web API를 사용 하 여 OData v4 엔드포인트 만들기</span><span class="sxs-lookup"><span data-stu-id="2d6fa-104">Create an OData v4 Endpoint Using ASP.NET Web API</span></span> 

> <span data-ttu-id="2d6fa-105">Open Data Protocol (OData)는 웹에 대 한 데이터 액세스 프로토콜.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-105">The Open Data Protocol (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="2d6fa-106">OData 쿼리 및 CRUD 작업을 통해 데이터 집합을 조작할 일관 된 방식으로 제공 (만들기, 읽기, 업데이트 및 삭제).</span><span class="sxs-lookup"><span data-stu-id="2d6fa-106">OData provides a uniform way to query and manipulate data sets through CRUD operations (create, read, update, and delete).</span></span>
>
> <span data-ttu-id="2d6fa-107">ASP.NET Web API v3 및 v4 프로토콜을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-107">ASP.NET Web API supports both v3 and v4 of the protocol.</span></span> <span data-ttu-id="2d6fa-108">Side-by-side-를 실행 하는 v4 엔드포인트 수도 v3 엔드포인트를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-108">You can even have a v4 endpoint that runs side-by-side with a v3 endpoint.</span></span>
>
> <span data-ttu-id="2d6fa-109">이 자습서에는 CRUD 작업을 지 원하는 OData v4 엔드포인트를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-109">This tutorial shows how to create an OData v4 endpoint that supports CRUD operations.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="2d6fa-110">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="2d6fa-110">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="2d6fa-111">Web API 5.2</span><span class="sxs-lookup"><span data-stu-id="2d6fa-111">Web API 5.2</span></span>
> - <span data-ttu-id="2d6fa-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="2d6fa-112">OData v4</span></span>
> - <span data-ttu-id="2d6fa-113">Visual Studio 2017 (Visual Studio 2017 다운로드 [여기](https://visualstudio.microsoft.com/downloads/))</span><span class="sxs-lookup"><span data-stu-id="2d6fa-113">Visual Studio 2017 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/))</span></span>
> - <span data-ttu-id="2d6fa-114">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="2d6fa-114">Entity Framework 6</span></span>
> - <span data-ttu-id="2d6fa-115">.NET 4.7.2</span><span class="sxs-lookup"><span data-stu-id="2d6fa-115">.NET 4.7.2</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="2d6fa-116">자습서 버전</span><span class="sxs-lookup"><span data-stu-id="2d6fa-116">Tutorial versions</span></span>
>
> <span data-ttu-id="2d6fa-117">OData 버전 3에 대 한 참조 [OData v3 엔드포인트 만들기](../odata-v3/creating-an-odata-endpoint.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-117">For the OData Version 3, see [Creating an OData v3 Endpoint](../odata-v3/creating-an-odata-endpoint.md).</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="2d6fa-118">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="2d6fa-118">Create the Visual Studio Project</span></span>

<span data-ttu-id="2d6fa-119">Visual Studio에서에서 합니다 **파일** 메뉴에서 **새로 만들기** &gt; **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-119">In Visual Studio, from the **File** menu, select **New** &gt; **Project**.</span></span>

<span data-ttu-id="2d6fa-120">확장 **설치 됨** &gt; **Visual C#**  &gt; **웹**를 선택 합니다 **ASP.NET 웹 응용 프로그램 (.NET Framework)**  템플릿.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-120">Expand **Installed** &gt; **Visual C#** &gt; **Web**, and select the **ASP.NET Web Application (.NET Framework)** template.</span></span> <span data-ttu-id="2d6fa-121">프로젝트 이름을 &quot;ProductService&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-121">Name the project &quot;ProductService&quot;.</span></span>

[![](create-an-odata-v4-endpoint/_static/image7.png)](create-an-odata-v4-endpoint/_static/image7.png)

<span data-ttu-id="2d6fa-122">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-122">Select **OK**.</span></span>



[![](create-an-odata-v4-endpoint/_static/image8.png)](create-an-odata-v4-endpoint/_static/image8.png)

<span data-ttu-id="2d6fa-123">선택 된 **빈** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-123">Select the **Empty** template.</span></span> <span data-ttu-id="2d6fa-124">아래 **폴더를 추가 하 고 핵심에 대 한 참조:** 를 선택 **Web API**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-124">Under **Add folders and core references for:**, select **Web API**.</span></span> <span data-ttu-id="2d6fa-125">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-125">Select **OK**.</span></span>

## <a name="install-the-odata-packages"></a><span data-ttu-id="2d6fa-126">OData 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="2d6fa-126">Install the OData packages</span></span>

<span data-ttu-id="2d6fa-127">**도구** 메뉴에서 **NuGet 패키지 관리자** &gt; **패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-127">From the **Tools** menu, select **NuGet Package Manager** &gt; **Package Manager Console**.</span></span> <span data-ttu-id="2d6fa-128">패키지 관리자 콘솔 창에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-128">In the Package Manager Console window, type:</span></span>

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample1.cmd)]

<span data-ttu-id="2d6fa-129">이 명령은 최신 OData NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-129">This command installs the latest OData NuGet packages.</span></span>

## <a name="add-a-model-class"></a><span data-ttu-id="2d6fa-130">모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="2d6fa-130">Add a model class</span></span>

<span data-ttu-id="2d6fa-131">A *모델* 는 응용 프로그램에서 데이터 엔터티를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-131">A *model* is an object that represents a data entity in your application.</span></span>

<span data-ttu-id="2d6fa-132">솔루션 탐색기에서 Models 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-132">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="2d6fa-133">상황에 맞는 메뉴에서 선택 **추가** &gt; **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-133">From the context menu, select **Add** &gt; **Class**.</span></span>

[![](create-an-odata-v4-endpoint/_static/image6.png)](create-an-odata-v4-endpoint/_static/image5.png)

> [!NOTE]
> <span data-ttu-id="2d6fa-134">규칙에 따라 모델 클래스는 Models 폴더에 배치 됩니다 있지만 사용자 고유의 프로젝트에서이 규칙에 따라 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-134">By convention, model classes are placed in the Models folder, but you don't have to follow this convention in your own projects.</span></span>


<span data-ttu-id="2d6fa-135">클래스 이름을 `Product`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-135">Name the class `Product`.</span></span> <span data-ttu-id="2d6fa-136">Product.cs 파일에서 다음을 사용 하 여 상용구 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-136">In the Product.cs file, replace the boilerplate code with the following:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample2.cs)]

<span data-ttu-id="2d6fa-137">`Id` 속성이 엔터티 키입니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-137">The `Id` property is the entity key.</span></span> <span data-ttu-id="2d6fa-138">클라이언트는 키로 엔터티를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-138">Clients can query entities by key.</span></span> <span data-ttu-id="2d6fa-139">예를 들어, ID가 5 인 제품을 얻으려면 URI는 `/Products(5)`합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-139">For example, to get the product with ID of 5, the URI is `/Products(5)`.</span></span> <span data-ttu-id="2d6fa-140">`Id` 속성 백 엔드 데이터베이스의 기본 키도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-140">The `Id` property will also be the primary key in the back-end database.</span></span>

## <a name="enable-entity-framework"></a><span data-ttu-id="2d6fa-141">Entity Framework를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="2d6fa-141">Enable Entity Framework</span></span>

<span data-ttu-id="2d6fa-142">이 자습서에서는 사용 하겠습니다 (EF) Entity Framework Code First 백 엔드 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-142">For this tutorial, we'll use Entity Framework (EF) Code First to create the back-end database.</span></span>

> [!NOTE]
> <span data-ttu-id="2d6fa-143">Web API OData EF가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-143">Web API OData does not require EF.</span></span> <span data-ttu-id="2d6fa-144">모델 데이터베이스 엔터티를 변환할 수 있는 모든 데이터 액세스 계층을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-144">Use any data-access layer that can translate database entities into models.</span></span>


<span data-ttu-id="2d6fa-145">첫째, EF에 대 한 NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-145">First, install the NuGet package for EF.</span></span> <span data-ttu-id="2d6fa-146">**도구** 메뉴에서 **NuGet 패키지 관리자** &gt; **패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-146">From the **Tools** menu, select **NuGet Package Manager** &gt; **Package Manager Console**.</span></span> <span data-ttu-id="2d6fa-147">패키지 관리자 콘솔 창에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-147">In the Package Manager Console window, type:</span></span>

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample3.cmd)]

<span data-ttu-id="2d6fa-148">Web.config 파일을 열고 내에서 다음 섹션을 추가 합니다 **구성** 요소 후 합니다 **configSections** 요소.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-148">Open the Web.config file, and add the following section inside the **configuration** element, after the **configSections** element.</span></span>

[!code-xml[Main](create-an-odata-v4-endpoint/samples/sample4.xml?highlight=6)]

<span data-ttu-id="2d6fa-149">이 설정은 LocalDB 데이터베이스에 대 한 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-149">This setting adds a connection string for a LocalDB database.</span></span> <span data-ttu-id="2d6fa-150">이 데이터베이스는 앱을 로컬로 실행할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-150">This database will be used when you run the app locally.</span></span>

<span data-ttu-id="2d6fa-151">다음으로, 라는 클래스를 추가 `ProductsContext` 모델 폴더:</span><span class="sxs-lookup"><span data-stu-id="2d6fa-151">Next, add a class named `ProductsContext` to the Models folder:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample5.cs)]

<span data-ttu-id="2d6fa-152">생성자에서 `"name=ProductsContext"` 연결 문자열의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-152">In the constructor, `"name=ProductsContext"` gives the name of the connection string.</span></span>

## <a name="configure-the-odata-endpoint"></a><span data-ttu-id="2d6fa-153">OData 끝점 구성</span><span class="sxs-lookup"><span data-stu-id="2d6fa-153">Configure the OData endpoint</span></span>

<span data-ttu-id="2d6fa-154">앱 파일을 열고\_Start/WebApiConfig.cs 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-154">Open the file App\_Start/WebApiConfig.cs.</span></span> <span data-ttu-id="2d6fa-155">다음을 추가 합니다 **를 사용 하 여** 문:</span><span class="sxs-lookup"><span data-stu-id="2d6fa-155">Add the following **using** statements:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample6.cs)]

<span data-ttu-id="2d6fa-156">다음 코드를 추가 합니다 **등록** 메서드:</span><span class="sxs-lookup"><span data-stu-id="2d6fa-156">Then add the following code to the **Register** method:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample7.cs)]

<span data-ttu-id="2d6fa-157">이 코드는 두 가지를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-157">This code does two things:</span></span>

- <span data-ttu-id="2d6fa-158">EDM (엔터티 데이터 모델)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-158">Creates an Entity Data Model (EDM).</span></span>
- <span data-ttu-id="2d6fa-159">경로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-159">Adds a route.</span></span>

<span data-ttu-id="2d6fa-160">EDM은 데이터의 추상적 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-160">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="2d6fa-161">EDM은 서비스 메타 데이터 문서를 만드는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-161">The EDM is used to create the service metadata document.</span></span> <span data-ttu-id="2d6fa-162">합니다 **ODataConventionModelBuilder** 클래스 기본 명명 규칙을 사용 하 여 EDM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-162">The **ODataConventionModelBuilder** class creates an EDM by using default naming conventions.</span></span> <span data-ttu-id="2d6fa-163">이 방법은 최소한의 코드에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-163">This approach requires the least code.</span></span> <span data-ttu-id="2d6fa-164">EDM 통해 더 많은 제어를 원하는 경우 사용할 수 있습니다 합니다 **된 ODataModelBuilder** 속성, 키 및 탐색 속성을 명시적으로 추가 하 여 EDM을 만들려면 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-164">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="2d6fa-165">A *경로* Web API 끝점에 HTTP 요청을 라우팅하는 방법을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-165">A *route* tells Web API how to route HTTP requests to the endpoint.</span></span> <span data-ttu-id="2d6fa-166">OData v4 경로 만들려면 다음을 호출 합니다 **MapODataServiceRoute** 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-166">To create an OData v4 route, call the **MapODataServiceRoute** extension method.</span></span>

<span data-ttu-id="2d6fa-167">응용 프로그램의 OData 끝점을 여러 개 있으면 각각에 대해 별도 경로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-167">If your application has multiple OData endpoints, create a separate route for each.</span></span> <span data-ttu-id="2d6fa-168">고유 경로 이름 및 접두사에는 각 경로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-168">Give each route a unique route name and prefix.</span></span>

## <a name="add-the-odata-controller"></a><span data-ttu-id="2d6fa-169">OData 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="2d6fa-169">Add the OData controller</span></span>

<span data-ttu-id="2d6fa-170">A *컨트롤러* 는 HTTP 요청을 처리 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-170">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="2d6fa-171">OData 서비스에서 설정 하는 각 엔터티에 대해 별도 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="2d6fa-171">You create a separate controller for each entity set in your OData service.</span></span> <span data-ttu-id="2d6fa-172">이 자습서에서는 만들려는 하나의 컨트롤러에 대 한는 `Product` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-172">In this tutorial, you will create one controller, for the `Product` entity.</span></span>

<span data-ttu-id="2d6fa-173">솔루션 탐색기에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** &gt; **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-173">In Solution Explorer, right-click the Controllers folder and select **Add** &gt; **Class**.</span></span> <span data-ttu-id="2d6fa-174">클래스 이름을 `ProductsController`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-174">Name the class `ProductsController`.</span></span>

> [!NOTE]
> <span data-ttu-id="2d6fa-175">OData v3 사용에 대 한이 자습서의 버전을 **컨트롤러 추가** 스 캐 폴딩 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-175">The version of this tutorial for OData v3 uses the **Add Controller** scaffolding.</span></span> <span data-ttu-id="2d6fa-176">현재는 OData v4에 대 한 스 캐 폴딩 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-176">Currently, there is no scaffolding for OData v4.</span></span>


<span data-ttu-id="2d6fa-177">다음 ProductsController.cs의 상용구 코드를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-177">Replace the boilerplate code in ProductsController.cs with the following.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample8.cs)]

<span data-ttu-id="2d6fa-178">컨트롤러에서 사용 하 여 `ProductsContext` EF를 사용 하 여 데이터베이스에 액세스 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-178">The controller uses the `ProductsContext` class to access the database using EF.</span></span> <span data-ttu-id="2d6fa-179">컨트롤러를 재정의 하는 **Dispose** 삭제 하는 방법을 **ProductsContext**합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-179">Notice that the controller overrides the **Dispose** method to dispose of the **ProductsContext**.</span></span>

<span data-ttu-id="2d6fa-180">컨트롤러에 대 한 시작 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-180">This is the starting point for the controller.</span></span> <span data-ttu-id="2d6fa-181">다음으로, 모든 CRUD 작업에 대 한 메서드를 추가 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-181">Next, we'll add methods for all of the CRUD operations.</span></span>

## <a name="query-the-entity-set"></a><span data-ttu-id="2d6fa-182">엔터티 집합 쿼리</span><span class="sxs-lookup"><span data-stu-id="2d6fa-182">Query the entity set</span></span>

<span data-ttu-id="2d6fa-183">다음 메서드를 추가 `ProductsController`합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-183">Add the following methods to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample9.cs)]

<span data-ttu-id="2d6fa-184">매개 변수가 없는 버전은 `Get` 메서드 전체 제품 컬렉션을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-184">The parameterless version of the `Get` method returns the entire Products collection.</span></span> <span data-ttu-id="2d6fa-185">`Get` 메서드를 *키* 매개 변수는 키로 제품 조회 (이 경우는 `Id` 속성).</span><span class="sxs-lookup"><span data-stu-id="2d6fa-185">The `Get` method with a *key* parameter looks up a product by its key (in this case, the `Id` property).</span></span>

<span data-ttu-id="2d6fa-186">합니다 **[EnableQuery]** 특성 $filter와 $sort, $page 쿼리 옵션을 사용 하 여 쿼리를 수정 하는 클라이언트를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-186">The **[EnableQuery]** attribute enables clients to modify the query, by using query options such as $filter, $sort, and $page.</span></span> <span data-ttu-id="2d6fa-187">자세한 내용은 [OData 쿼리 옵션 지원](../supporting-odata-query-options.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-187">For more information, see [Supporting OData Query Options](../supporting-odata-query-options.md).</span></span>

## <a name="add-an-entity-to-the-entity-set"></a><span data-ttu-id="2d6fa-188">엔터티 집합에 엔터티 추가</span><span class="sxs-lookup"><span data-stu-id="2d6fa-188">Add an entity to the entity set</span></span>

<span data-ttu-id="2d6fa-189">데이터베이스에 새 제품을 추가 하려면 클라이언트를 사용 하려면 다음 메서드를 추가 `ProductsController`합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-189">To enable clients to add a new product to the database, add the following method to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample10.cs)]

## <a name="update-an-entity"></a><span data-ttu-id="2d6fa-190">엔터티 업데이트</span><span class="sxs-lookup"><span data-stu-id="2d6fa-190">Update an entity</span></span>

<span data-ttu-id="2d6fa-191">OData는 엔터티, PATCH 및 PUT 업데이트를 위해 두 개의 서로 다른 의미 체계를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-191">OData supports two different semantics for updating an entity, PATCH and PUT.</span></span>

- <span data-ttu-id="2d6fa-192">패치를 부분적으로 업데이트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-192">PATCH performs a partial update.</span></span> <span data-ttu-id="2d6fa-193">클라이언트를 업데이트 하는 속성만 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-193">The client specifies just the properties to update.</span></span>
- <span data-ttu-id="2d6fa-194">PUT는 전체 엔터티를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-194">PUT replaces the entire entity.</span></span>

<span data-ttu-id="2d6fa-195">PUT의 단점은 클라이언트 변경 하지 않는 하는 값을 포함 하 여 엔터티의 모든 속성의 값을 송신 해야 함을입니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-195">The disadvantage of PUT is that the client must send values for all of the properties in the entity, including values that are not changing.</span></span> <span data-ttu-id="2d6fa-196">합니다 [OData 사양을](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) 패치는 기본 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-196">The [OData spec](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) states that PATCH is preferred.</span></span>

<span data-ttu-id="2d6fa-197">어떤 경우 든, PATCH 및 PUT 메서드에 대 한 코드가 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-197">In any case, here is the code for both PATCH and PUT methods:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample11.cs)]

<span data-ttu-id="2d6fa-198">PATCH의 경우 컨트롤러를 사용 하는 **델타&lt;T&gt;**  변경 내용을 추적 하는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-198">In the case of PATCH, the controller uses the **Delta&lt;T&gt;** type to track the changes.</span></span>

## <a name="delete-an-entity"></a><span data-ttu-id="2d6fa-199">엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="2d6fa-199">Delete an entity</span></span>

<span data-ttu-id="2d6fa-200">데이터베이스에서 제품을 삭제 하도록 클라이언트를 사용 하려면 다음 메서드를 추가 `ProductsController`합니다.</span><span class="sxs-lookup"><span data-stu-id="2d6fa-200">To enable clients to delete a product from the database, add the following method to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample12.cs)]
