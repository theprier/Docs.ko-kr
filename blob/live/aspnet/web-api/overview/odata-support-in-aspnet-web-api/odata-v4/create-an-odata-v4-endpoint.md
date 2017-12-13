---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
title: "ASP.NET Web API 2.2 사용 하 여 OData v4 끝점을 만듭니다 | Microsoft Docs"
author: MikeWasson
description: "개방형 데이터 프로토콜 (OData)는 웹에 대 한 데이터 액세스 프로토콜입니다. OData는 일관 된 방식으로 쿼리 및 조작 CRUD 작업을 통해 데이터 집합을 제공..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/24/2014
ms.topic: article
ms.assetid: 1e1927c0-ded1-4752-80fd-a146628d2f09
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
msc.type: authoredcontent
ms.openlocfilehash: a3f94818f9674b0e1e9a45b2a6cc9455edc79726
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="create-an-odata-v4-endpoint-using-aspnet-web-api-22"></a><span data-ttu-id="0d130-104">ASP.NET Web API 2.2 사용 하 여 OData v4 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="0d130-104">Create an OData v4 Endpoint Using ASP.NET Web API 2.2</span></span>
====================
<span data-ttu-id="0d130-105">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0d130-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="0d130-106">개방형 데이터 프로토콜 (OData)는 웹에 대 한 데이터 액세스 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-106">The Open Data Protocol (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="0d130-107">OData는 쿼리하고 CRUD 작업을 통해 데이터 집합을 조작 하는 일관 된 방식으로 제공 (만들기, 읽기, 업데이트 및 삭제) 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-107">OData provides a uniform way to query and manipulate data sets through CRUD operations (create, read, update, and delete).</span></span>
> 
> <span data-ttu-id="0d130-108">ASP.NET Web API v3 및 v4 프로토콜을 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-108">ASP.NET Web API supports both v3 and v4 of the protocol.</span></span> <span data-ttu-id="0d130-109">나란히 실행 하는 v4 끝점 될 수도 있습니다 v3 끝점을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-109">You can even have a v4 endpoint that runs side-by-side with a v3 endpoint.</span></span>
> 
> <span data-ttu-id="0d130-110">이 자습서에는 CRUD 작업을 지 원하는 OData v4 끝점을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-110">This tutorial shows how to create an OData v4 endpoint that supports CRUD operations.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="0d130-111">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="0d130-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="0d130-112">Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="0d130-112">Web API 2.2</span></span>
> - <span data-ttu-id="0d130-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="0d130-113">OData v4</span></span>
> - [<span data-ttu-id="0d130-114">Visual Studio 2013 업데이트 2</span><span class="sxs-lookup"><span data-stu-id="0d130-114">Visual Studio 2013 Update 2</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs)
> - <span data-ttu-id="0d130-115">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="0d130-115">Entity Framework 6</span></span>
> - <span data-ttu-id="0d130-116">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="0d130-116">.NET 4.5</span></span>
> 
> 
> ## <a name="tutorial-versions"></a><span data-ttu-id="0d130-117">자습서 버전</span><span class="sxs-lookup"><span data-stu-id="0d130-117">Tutorial versions</span></span>
> 
> <span data-ttu-id="0d130-118">OData 버전 3에 대 한 참조 [OData v3 끝점을 만드는](../odata-v3/creating-an-odata-endpoint.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-118">For the OData Version 3, see [Creating an OData v3 Endpoint](../odata-v3/creating-an-odata-endpoint.md).</span></span>


## <a name="create-the-visual-studio-project"></a><span data-ttu-id="0d130-119">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="0d130-119">Create the Visual Studio Project</span></span>

<span data-ttu-id="0d130-120">Visual Studio에서에서 **파일** 메뉴 선택 **새로** &gt; **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-120">In Visual Studio, from the **File** menu, select **New** &gt; **Project**.</span></span>

<span data-ttu-id="0d130-121">확장 **설치 됨** &gt; **템플릿** &gt; **Visual C#** &gt; **웹**는 선택 **ASP.NET 웹 응용 프로그램** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="0d130-121">Expand **Installed** &gt; **Templates** &gt; **Visual C#** &gt; **Web**, and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="0d130-122">프로젝트 이름을 &quot;ProductService&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-122">Name the project &quot;ProductService&quot;.</span></span>

[![](create-an-odata-v4-endpoint/_static/image2.png)](create-an-odata-v4-endpoint/_static/image1.png)

<span data-ttu-id="0d130-123">에 **새 프로젝트** 대화 상자에서는 **빈** 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-123">In the **New Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="0d130-124">&quot;폴더 추가 및 핵심 참조 중... &quot;, 클릭 **웹 API**합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-124">Under &quot;Add folders and core references...&quot;, click **Web API**.</span></span> <span data-ttu-id="0d130-125">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-125">Click **OK**.</span></span>

[![](create-an-odata-v4-endpoint/_static/image4.png)](create-an-odata-v4-endpoint/_static/image3.png)

## <a name="install-the-odata-packages"></a><span data-ttu-id="0d130-126">OData 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="0d130-126">Install the OData Packages</span></span>

<span data-ttu-id="0d130-127">**도구** 메뉴 선택 **NuGet 패키지 관리자** &gt; **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-127">From the **Tools** menu, select **NuGet Package Manager** &gt; **Package Manager Console**.</span></span> <span data-ttu-id="0d130-128">패키지 관리자 콘솔 창에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-128">In the Package Manager Console window, type:</span></span>

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample1.cmd)]

<span data-ttu-id="0d130-129">이 명령은 최신 OData NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-129">This command installs the latest OData NuGet packages.</span></span>

## <a name="add-a-model-class"></a><span data-ttu-id="0d130-130">모델 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-130">Add a Model Class</span></span>

<span data-ttu-id="0d130-131">A *모델* 는 응용 프로그램에서 데이터 엔터티를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-131">A *model* is an object that represents a data entity in your application.</span></span>

<span data-ttu-id="0d130-132">솔루션 탐색기에서 모델 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-132">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="0d130-133">상황에 맞는 메뉴에서 선택 **추가** &gt; **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-133">From the context menu, select **Add** &gt; **Class**.</span></span>

[![](create-an-odata-v4-endpoint/_static/image6.png)](create-an-odata-v4-endpoint/_static/image5.png)

> [!NOTE]
> <span data-ttu-id="0d130-134">규칙에 따라 모델 폴더에 모델 클래스를 포함 하지만 실제 프로젝트에서이 규칙을 따르는 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-134">By convention, model classes are placed in the Models folder, but you don't have to follow this convention in your own projects.</span></span>


<span data-ttu-id="0d130-135">클래스 이름을 `Product`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-135">Name the class `Product`.</span></span> <span data-ttu-id="0d130-136">Product.cs 파일에서 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-136">In the Product.cs file, replace the boilerplate code with the following:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample2.cs)]

<span data-ttu-id="0d130-137">`Id` 속성은 엔터티 키입니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-137">The `Id` property is the entity key.</span></span> <span data-ttu-id="0d130-138">클라이언트는 키로 엔터티를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-138">Clients can query entities by key.</span></span> <span data-ttu-id="0d130-139">예를 들어 ID 5 인 제품을 가져오려면 URI는 `/Products(5)`합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-139">For example, to get the product with ID of 5, the URI is `/Products(5)`.</span></span> <span data-ttu-id="0d130-140">`Id` 속성 백 엔드 데이터베이스의 기본 키 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-140">The `Id` property will also be the primary key in the back-end database.</span></span>

## <a name="enable-entity-framework"></a><span data-ttu-id="0d130-141">Entity Framework를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="0d130-141">Enable Entity Framework</span></span>

<span data-ttu-id="0d130-142">이 자습서에서는 Entity Framework (EF) Code First 백 엔드 데이터베이스를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-142">For this tutorial, we'll use Entity Framework (EF) Code First to create the back-end database.</span></span>

> [!NOTE]
> <span data-ttu-id="0d130-143">Web API OData EF가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-143">Web API OData does not require EF.</span></span> <span data-ttu-id="0d130-144">데이터베이스 엔터티 모델로 변환할 수 있는 모든 데이터 액세스 계층을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-144">Use any data-access layer that can translate database entities into models.</span></span>


<span data-ttu-id="0d130-145">먼저, EF에 대 한 NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-145">First, install the NuGet package for EF.</span></span> <span data-ttu-id="0d130-146">**도구** 메뉴 선택 **NuGet 패키지 관리자** &gt; **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-146">From the **Tools** menu, select **NuGet Package Manager** &gt; **Package Manager Console**.</span></span> <span data-ttu-id="0d130-147">패키지 관리자 콘솔 창에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-147">In the Package Manager Console window, type:</span></span>

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample3.cmd)]

<span data-ttu-id="0d130-148">내부 다음 섹션을 추가 하 고 Web.config 파일을 열고는 **구성** 요소 이후에 **configSections** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-148">Open the Web.config file, and add the following section inside the **configuration** element, after the **configSections** element.</span></span>

[!code-xml[Main](create-an-odata-v4-endpoint/samples/sample4.xml?highlight=6)]

<span data-ttu-id="0d130-149">이 설정은 LocalDB 데이터베이스에 대 한 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-149">This setting adds a connection string for a LocalDB database.</span></span> <span data-ttu-id="0d130-150">이 데이터베이스는 응용 프로그램을 로컬로 실행할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-150">This database will be used when you run the app locally.</span></span>

<span data-ttu-id="0d130-151">다음으로 라는 클래스를 추가 `ProductsContext` 모델 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-151">Next, add a class named `ProductsContext` to the Models folder:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample5.cs)]

<span data-ttu-id="0d130-152">생성자에서 `"name=ProductsContext"` 연결 문자열의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-152">In the constructor, `"name=ProductsContext"` gives the name of the connection string.</span></span>

## <a name="configure-the-odata-endpoint"></a><span data-ttu-id="0d130-153">OData 끝점을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-153">Configure the OData Endpoint</span></span>

<span data-ttu-id="0d130-154">응용 프로그램 파일을 열고\_Start/WebApiConfig.cs 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-154">Open the file App\_Start/WebApiConfig.cs.</span></span> <span data-ttu-id="0d130-155">다음 추가 **를 사용 하 여** 문:</span><span class="sxs-lookup"><span data-stu-id="0d130-155">Add the following **using** statements:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample6.cs)]

<span data-ttu-id="0d130-156">다음 코드를 다음 추가 **등록** 메서드:</span><span class="sxs-lookup"><span data-stu-id="0d130-156">Then add the following code to the **Register** method:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample7.cs)]

<span data-ttu-id="0d130-157">이 코드는 두 가지 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-157">This code does two things:</span></span>

- <span data-ttu-id="0d130-158">엔터티 데이터 모델 (EDM)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-158">Creates an Entity Data Model (EDM).</span></span>
- <span data-ttu-id="0d130-159">경로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-159">Adds a route.</span></span>

<span data-ttu-id="0d130-160">EDM은 데이터의 추상 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-160">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="0d130-161">EDM은 서비스 메타 데이터 문서를 만드는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-161">The EDM is used to create the service metadata document.</span></span> <span data-ttu-id="0d130-162">**ODataConventionModelBuilder** 클래스는 EDM 기본 명명 규칙을 사용 하 여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-162">The **ODataConventionModelBuilder** class creates an EDM by using default naming conventions.</span></span> <span data-ttu-id="0d130-163">이 방법을 사용 하려면 최소 코드가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-163">This approach requires the least code.</span></span> <span data-ttu-id="0d130-164">EDM 통해 더 많은 제어를 원하는 경우 사용할 수 있습니다는 **된** EDM 속성, 키 및 탐색 속성을 명시적으로 추가 하 여 만들 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-164">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="0d130-165">A *경로* Web API 끝점에 HTTP 요청을 라우팅하는 방법을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-165">A *route* tells Web API how to route HTTP requests to the endpoint.</span></span> <span data-ttu-id="0d130-166">OData v4 경로 만들려면 호출는 **MapODataServiceRoute** 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="0d130-166">To create an OData v4 route, call the **MapODataServiceRoute** extension method.</span></span>

<span data-ttu-id="0d130-167">응용 프로그램에 여러 OData 끝점 각각에 대해 별도 경로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-167">If your application has multiple OData endpoints, create a separate route for each.</span></span> <span data-ttu-id="0d130-168">에 고유 경로 이름 및 접두사 각 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-168">Give each route a unique route name and prefix.</span></span>

## <a name="add-the-odata-controller"></a><span data-ttu-id="0d130-169">OData 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="0d130-169">Add the OData Controller</span></span>

<span data-ttu-id="0d130-170">A *컨트롤러* 는 HTTP 요청을 처리 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-170">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="0d130-171">OData 서비스에서 설정 하는 각 엔터티에 대 한 별도 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="0d130-171">You create a separate controller for each entity set in your OData service.</span></span> <span data-ttu-id="0d130-172">이 자습서에서는 만듭니다 컨트롤러 하나에 대 한는 `Product` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="0d130-172">In this tutorial, you will create one controller, for the `Product` entity.</span></span>

<span data-ttu-id="0d130-173">솔루션 탐색기에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** &gt; **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-173">In Solution Explorer, right-click the Controllers folder and select **Add** &gt; **Class**.</span></span> <span data-ttu-id="0d130-174">클래스 이름을 `ProductsController`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-174">Name the class `ProductsController`.</span></span>

> [!NOTE]
> <span data-ttu-id="0d130-175">OData v3 사용에 대 한이 자습서의 버전은 **컨트롤러 추가** 스 캐 폴딩 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-175">The version of this tutorial for OData v3 uses the **Add Controller** scaffolding.</span></span> <span data-ttu-id="0d130-176">현재로 서는 OData v 4에 대 한 스 캐 폴딩이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-176">Currently, there is no scaffolding for OData v4.</span></span>


<span data-ttu-id="0d130-177">ProductsController.cs에 상용구 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-177">Replace the boilerplate code in ProductsController.cs with the following.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample8.cs)]

<span data-ttu-id="0d130-178">컨트롤러 사용 하 여는 `ProductsContext` EF를 사용 하 여 데이터베이스에 액세스 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-178">The controller uses the `ProductsContext` class to access the database using EF.</span></span> <span data-ttu-id="0d130-179">컨트롤러를 재정의 하는 통지는 **Dispose** 메서드를 삭제 하는 **ProductsContext**합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-179">Notice that the controller overrides the **Dispose** method to dispose of the **ProductsContext**.</span></span>

<span data-ttu-id="0d130-180">컨트롤러에 대 한 시작 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-180">This is the starting point for the controller.</span></span> <span data-ttu-id="0d130-181">다음으로, 모든 CRUD 작업에 대 한 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-181">Next, we'll add methods for all of the CRUD operations.</span></span>

## <a name="querying-the-entity-set"></a><span data-ttu-id="0d130-182">엔터티 집합 쿼리</span><span class="sxs-lookup"><span data-stu-id="0d130-182">Querying the Entity Set</span></span>

<span data-ttu-id="0d130-183">다음 메서드를 추가 `ProductsController`합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-183">Add the following methods to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample9.cs)]

<span data-ttu-id="0d130-184">매개 변수가 없는 버전의는 `Get` 메서드 전체 제품 컬렉션을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-184">The parameterless version of the `Get` method returns the entire Products collection.</span></span> <span data-ttu-id="0d130-185">`Get` 메서드는 *키* 매개 변수가 해당 키에 따라 제품을 찾습니다 (이 경우는 `Id` 속성).</span><span class="sxs-lookup"><span data-stu-id="0d130-185">The `Get` method with a *key* parameter looks up a product by its key (in this case, the `Id` property).</span></span>

<span data-ttu-id="0d130-186">**[EnableQuery]** 특성을 사용 하면 클라이언트가 $filter, $sort, 및 $page 등의 쿼리 옵션을 사용 하 여 쿼리를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-186">The **[EnableQuery]** attribute enables clients to modify the query, by using query options such as $filter, $sort, and $page.</span></span> <span data-ttu-id="0d130-187">자세한 내용은 참조 [OData 쿼리 옵션을 지 원하는](../supporting-odata-query-options.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-187">For more information, see [Supporting OData Query Options](../supporting-odata-query-options.md).</span></span>

## <a name="adding-an-entity-to-the-entity-set"></a><span data-ttu-id="0d130-188">엔터티 집합에 엔터티 추가</span><span class="sxs-lookup"><span data-stu-id="0d130-188">Adding an Entity to the Entity Set</span></span>

<span data-ttu-id="0d130-189">데이터베이스에 새 제품을 추가 하는 클라이언트를 사용 하려면 다음 메서드를 추가 `ProductsController`합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-189">To enable clients to add a new product to the database, add the following method to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample10.cs)]

## <a name="updating-an-entity"></a><span data-ttu-id="0d130-190">엔터티 업데이트</span><span class="sxs-lookup"><span data-stu-id="0d130-190">Updating an Entity</span></span>

<span data-ttu-id="0d130-191">OData는 엔터티, PATCH 및 PUT를 업데이트 하기 위한 두 개의 서로 다른 의미 체계를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-191">OData supports two different semantics for updating an entity, PATCH and PUT.</span></span>

- <span data-ttu-id="0d130-192">패치 부분 업데이트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-192">PATCH performs a partial update.</span></span> <span data-ttu-id="0d130-193">클라이언트에만 업데이트할 속성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-193">The client specifies just the properties to update.</span></span>
- <span data-ttu-id="0d130-194">PUT 전체 엔터티를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-194">PUT replaces the entire entity.</span></span>

<span data-ttu-id="0d130-195">PUT의 단점은 클라이언트를 변경 하지 않는 값을 포함 하는 엔터티의 모든 속성에 대 한 값을 전송 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-195">The disadvantage of PUT is that the client must send values for all of the properties in the entity, including values that are not changing.</span></span> <span data-ttu-id="0d130-196">[OData 사양을](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) 패치 기본 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-196">The [OData spec](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) states that PATCH is preferred.</span></span>

<span data-ttu-id="0d130-197">어떤 경우 든, 다음은 PATCH 및 PUT 모두 메서드에 대 한 코드가입니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-197">In any case, here is the code for both PATCH and PUT methods:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample11.cs)]

<span data-ttu-id="0d130-198">컨트롤러 사용 PATCH의 경우는 **델타&lt;T&gt;**  변경 내용을 추적 하는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-198">In the case of PATCH, the controller uses the **Delta&lt;T&gt;** type to track the changes.</span></span>

## <a name="deleting-an-entity"></a><span data-ttu-id="0d130-199">엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="0d130-199">Deleting an Entity</span></span>

<span data-ttu-id="0d130-200">데이터베이스에서 제품을 삭제 하는 클라이언트를 사용 하려면 다음 메서드를 추가 `ProductsController`합니다.</span><span class="sxs-lookup"><span data-stu-id="0d130-200">To enable clients to delete a product from the database, add the following method to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample12.cs)]
