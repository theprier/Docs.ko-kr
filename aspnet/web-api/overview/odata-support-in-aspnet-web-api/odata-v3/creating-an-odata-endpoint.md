---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
title: Web API 2 OData v3 엔드포인트 만들기 | Microsoft Docs
author: MikeWasson
description: Open Data Protocol (OData)는 웹에 대 한 데이터 액세스 프로토콜. OData는 데이터 구조, 데이터를 쿼리 및 데이터를 조작 하는 일관 된 방식을 제공 하는 중...
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 262843d6-43a2-4f1c-82d9-0b90ae6df0cf
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
msc.type: authoredcontent
ms.openlocfilehash: 654f697c8d095d45ba31e2808c52f9ad24b606c8
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41836334"
---
<a name="creating-an-odata-v3-endpoint-with-web-api-2"></a><span data-ttu-id="b63fc-104">Web API 2 OData v3 엔드포인트 만들기</span><span class="sxs-lookup"><span data-stu-id="b63fc-104">Creating an OData v3 Endpoint with Web API 2</span></span>
====================
<span data-ttu-id="b63fc-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b63fc-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="b63fc-106">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="b63fc-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="b63fc-107">합니다 [개방형 데이터 프로토콜](http://www.odata.org/) 는 웹에 대 한 데이터 액세스 프로토콜 (OData).</span><span class="sxs-lookup"><span data-stu-id="b63fc-107">The [Open Data Protocol](http://www.odata.org/) (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="b63fc-108">OData는 데이터 구조, 데이터를 쿼리하고, CRUD 작업을 통해 데이터 집합을 조작 하는 일관 된 방식을 제공 (만들기, 읽기, 업데이트 및 삭제).</span><span class="sxs-lookup"><span data-stu-id="b63fc-108">OData provides a uniform way to structure data, query the data, and manipulate the data set through CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="b63fc-109">OData는 AtomPub (XML) 및 JSON 형식 모두를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-109">OData supports both AtomPub (XML) and JSON formats.</span></span> <span data-ttu-id="b63fc-110">OData는 데이터에 대 한 메타 데이터를 노출 하는 방법을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-110">OData also defines a way to expose metadata about the data.</span></span> <span data-ttu-id="b63fc-111">클라이언트 메타 데이터를 사용 하 여 형식 정보 및 데이터 집합에 대 한 관계를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-111">Clients can use the metadata to discover the type information and relationships for the data set.</span></span>
> 
> <span data-ttu-id="b63fc-112">ASP.NET Web API 쉽게 데이터 집합에 대 한 OData 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-112">ASP.NET Web API makes it easy to create an OData endpoint for a data set.</span></span> <span data-ttu-id="b63fc-113">끝점이 지 원하는 OData 작업 정확 하 게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-113">You can control exactly which OData operations the endpoint supports.</span></span> <span data-ttu-id="b63fc-114">비 OData 끝점와 함께 여러 OData 끝점을 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-114">You can host multiple OData endpoints, alongside non-OData endpoints.</span></span> <span data-ttu-id="b63fc-115">데이터 모델, 백 엔드 비즈니스 논리 및 데이터 계층을 통해 전체 제어를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-115">You have full control over your data model, back-end business logic, and data layer.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b63fc-116">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="b63fc-116">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="b63fc-117">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="b63fc-117">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="b63fc-118">Web API 2</span><span class="sxs-lookup"><span data-stu-id="b63fc-118">Web API 2</span></span>
> - <span data-ttu-id="b63fc-119">OData 버전 3</span><span class="sxs-lookup"><span data-stu-id="b63fc-119">OData Version 3</span></span>
> - <span data-ttu-id="b63fc-120">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="b63fc-120">Entity Framework 6</span></span>
> - [<span data-ttu-id="b63fc-121">Fiddler 웹 디버깅 프록시 (선택 사항)</span><span class="sxs-lookup"><span data-stu-id="b63fc-121">Fiddler Web Debugging Proxy (Optional)</span></span>](http://www.fiddler2.com)
> 
> <span data-ttu-id="b63fc-122">Web API OData 지원에서 추가한 [ASP.NET 및 Web Tools 2012.2 업데이트](https://go.microsoft.com/fwlink/?LinkId=282650)합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-122">Web API OData support was added in [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="b63fc-123">그러나이 자습서에서는 Visual Studio 2013에 추가 된 스 캐 폴딩 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-123">However, this tutorial uses scaffolding that was added in Visual Studio 2013.</span></span>


<span data-ttu-id="b63fc-124">이 자습서에서는 클라이언트가 쿼리할 수 있는 간단한 OData 끝점을 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-124">In this tutorial, you will create a simple OData endpoint that clients can query.</span></span> <span data-ttu-id="b63fc-125">또한 끝점에 대 한 C# 클라이언트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-125">You will also create a C# client for the endpoint.</span></span> <span data-ttu-id="b63fc-126">이 자습서를 완료 한 후 다음 일련의 자습서 엔터티 관계 작업을 포함 하 여 더 많은 기능을 추가 하는 방법을 표시 하 고 확장 하 고 $/ $선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-126">After you complete this tutorial, the next set of tutorials show how to add more functionality, including entity relations, actions, and $expand/$select.</span></span>

- [<span data-ttu-id="b63fc-127">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="b63fc-127">Create the Visual Studio Project</span></span>](#create-project)
- [<span data-ttu-id="b63fc-128">엔터티 모델 추가</span><span class="sxs-lookup"><span data-stu-id="b63fc-128">Add an Entity Model</span></span>](#add-model)
- [<span data-ttu-id="b63fc-129">OData 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="b63fc-129">Add an OData Controller</span></span>](#add-controller)
- [<span data-ttu-id="b63fc-130">EDM 및 경로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-130">Add the EDM and Route</span></span>](#edm)
- [<span data-ttu-id="b63fc-131">(선택 사항) 데이터베이스 시드</span><span class="sxs-lookup"><span data-stu-id="b63fc-131">Seed the Database (Optional)</span></span>](#seed-db)
- [<span data-ttu-id="b63fc-132">OData 끝점을 탐색</span><span class="sxs-lookup"><span data-stu-id="b63fc-132">Exploring the OData Endpoint</span></span>](#explore)
- [<span data-ttu-id="b63fc-133">OData 직렬화 형식</span><span class="sxs-lookup"><span data-stu-id="b63fc-133">OData Serialization Formats</span></span>](#formats)

<a id="create-project"></a>
## <a name="create-the-visual-studio-project"></a><span data-ttu-id="b63fc-134">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="b63fc-134">Create the Visual Studio Project</span></span>

<span data-ttu-id="b63fc-135">이 자습서에서는 기본 CRUD 작업을 지 원하는 OData 끝점에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-135">In this tutorial, you will create an OData endpoint that supports basic CRUD operations.</span></span> <span data-ttu-id="b63fc-136">끝점에는 제품 목록을 단일 리소스를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-136">The endpoint will expose a single resource, a list of products.</span></span> <span data-ttu-id="b63fc-137">나중에 자습서 더 많은 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-137">Later tutorials will add more features.</span></span>

<span data-ttu-id="b63fc-138">Visual Studio를 시작 하 고 선택 **새 프로젝트** 시작 페이지에서.</span><span class="sxs-lookup"><span data-stu-id="b63fc-138">Start Visual Studio and select **New Project** from the Start page.</span></span> <span data-ttu-id="b63fc-139">또는에서 **파일** 메뉴에서 **새로 만들기** 차례로 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-139">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="b63fc-140">에 **템플릿을** 창 **설치 된 템플릿** Visual C# 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-140">In the **Templates** pane, select **Installed Templates** and expand the Visual C# node.</span></span> <span data-ttu-id="b63fc-141">아래 **Visual C#** 를 선택 **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-141">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="b63fc-142">선택 **ASP.NET 웹 응용 프로그램** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="b63fc-142">Select **the ASP.NET Web Application** template.</span></span>

![](creating-an-odata-endpoint/_static/image1.png)

<span data-ttu-id="b63fc-143">에 **새 ASP.NET 프로젝트** 대화 상자에서 선택 합니다 **빈** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="b63fc-143">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="b63fc-144">아래 &quot;폴더를 추가 하 고 핵심에 대 한 참조 하는 중... &quot;를 확인 **Web API**합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-144">Under &quot;Add folders and core references for...&quot;, check **Web API**.</span></span> <span data-ttu-id="b63fc-145">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-145">Click **OK**.</span></span>

![](creating-an-odata-endpoint/_static/image2.png)

<a id="add-model"></a>
## <a name="add-an-entity-model"></a><span data-ttu-id="b63fc-146">엔터티 모델 추가</span><span class="sxs-lookup"><span data-stu-id="b63fc-146">Add an Entity Model</span></span>

<span data-ttu-id="b63fc-147">*모델*은 응용 프로그램에서 데이터를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-147">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="b63fc-148">이 자습서에서는 제품을 나타내는 모델이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-148">For this tutorial, we need a model that represents a product.</span></span> <span data-ttu-id="b63fc-149">모델 형식에 해당 하는 OData 엔터티.</span><span class="sxs-lookup"><span data-stu-id="b63fc-149">The model corresponds to our OData entity type.</span></span>

<span data-ttu-id="b63fc-150">솔루션 탐색기에서 Models 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-150">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="b63fc-151">상황에 맞는 메뉴에서 선택 **추가** 선택한 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-151">From the context menu, select **Add** then select **Class**.</span></span>

![](creating-an-odata-endpoint/_static/image3.png)

<span data-ttu-id="b63fc-152">에 **새로 추가** 항목 대화 상자, 클래스의 이름을 &quot;제품&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-152">In the **Add New** Item dialog, name the class &quot;Product&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image4.png)

> [!NOTE]
> <span data-ttu-id="b63fc-153">규칙에 따라 모델 클래스는 Models 폴더에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-153">By convention, model classes are placed in the Models folder.</span></span> <span data-ttu-id="b63fc-154">사용자의 프로젝트에서이 규칙을 따르는 없지만이 자습서로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-154">You don't have to follow this convention in your own projects, but we'll use it for this tutorial.</span></span>


<span data-ttu-id="b63fc-155">Product.cs 파일에서 다음 클래스 정의 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-155">In the Product.cs file, add the following class definition:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample1.cs)]

<span data-ttu-id="b63fc-156">ID 속성이 엔터티 키가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-156">The ID property will be the entity key.</span></span> <span data-ttu-id="b63fc-157">클라이언트 ID로 제품을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-157">Clients can query products by ID.</span></span> <span data-ttu-id="b63fc-158">이 필드는 백 엔드 데이터베이스의 기본 키 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-158">This field would also be the primary key in the back-end database.</span></span>

<span data-ttu-id="b63fc-159">이제 프로젝트를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="b63fc-159">Build the project now.</span></span> <span data-ttu-id="b63fc-160">다음 단계에서는 제품 형식을 찾기 위해 리플렉션을 사용 하는 몇 가지 Visual Studio 스 캐 폴딩을 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-160">In the next step, we'll use some Visual Studio scaffolding that uses reflection to find the Product type.</span></span>

<a id="add-controller"></a>
## <a name="add-an-odata-controller"></a><span data-ttu-id="b63fc-161">OData 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="b63fc-161">Add an OData Controller</span></span>

<span data-ttu-id="b63fc-162">A *컨트롤러* 는 HTTP 요청을 처리 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-162">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="b63fc-163">OData 서비스에서 설정 하는 각 엔터티에 대해 별도 컨트롤러를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-163">You define a separate controller for each entity set in you OData service.</span></span> <span data-ttu-id="b63fc-164">이 자습서에서는 단일 컨트롤러를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-164">In this tutorial, we'll create a single controller.</span></span>

<span data-ttu-id="b63fc-165">솔루션 탐색기에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-165">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="b63fc-166">선택 **추가** 선택한 후 **컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-166">Select **Add** and then select **Controller**.</span></span>

![](creating-an-odata-endpoint/_static/image5.png)

<span data-ttu-id="b63fc-167">에 **스 캐 폴드 추가** 대화 상자에서 &quot;Web API 2 OData 컨트롤러 작업을 사용 하 여 Entity Framework를 사용 하 여&quot;입니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-167">In the **Add Scaffold** dialog, select &quot;Web API 2 OData Controller with actions, using Entity Framework&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image6.png)

<span data-ttu-id="b63fc-168">에 **컨트롤러 추가** 대화 상자에서 이름 "ProductsController" 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-168">In the **Add Controller** dialog, name the controller "ProductsController".</span></span> <span data-ttu-id="b63fc-169">선택 된 &quot;비동기 컨트롤러 동작을 사용 하 여&quot; 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-169">Select the &quot;Use async controller actions&quot; checkbox.</span></span> <span data-ttu-id="b63fc-170">에 **모델** 드롭 다운 목록에서 Product 클래스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-170">In the **Model** drop-down list, select the Product class.</span></span>

![](creating-an-odata-endpoint/_static/image7.png)

<span data-ttu-id="b63fc-171">클릭 된 **새 데이터 컨텍스트...**  단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-171">Click the **New data context...** button.</span></span> <span data-ttu-id="b63fc-172">데이터 컨텍스트 형식에 대 한 기본 이름을 그대로 두고 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-172">Leave the default name for the data context type, and click **Add**.</span></span>

![](creating-an-odata-endpoint/_static/image8.png)

<span data-ttu-id="b63fc-173">컨트롤러를 추가 하려면 컨트롤러 추가 대화 상자에서 추가 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-173">Click Add in the Add Controller dialog to add the controller.</span></span>

![](creating-an-odata-endpoint/_static/image9.png)

<span data-ttu-id="b63fc-174">참고: 라는 오류 메시지가 표시 &quot;형식을 가져오는 동안 오류가 발생 했습니다... &quot;, Product 클래스를 추가한 후 Visual Studio 프로젝트를 빌드 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-174">Note: If you get an error message that says &quot;There was an error getting the type...&quot;, make sure that you built the Visual Studio project after you added the Product class.</span></span> <span data-ttu-id="b63fc-175">스 캐 폴딩의 리플렉션을 사용 하 여 클래스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-175">The scaffolding uses reflection to find the class.</span></span>

![](creating-an-odata-endpoint/_static/image10.png)

<span data-ttu-id="b63fc-176">스 캐 폴딩을 프로젝트에 두 개의 코드 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-176">The scaffolding adds two code files to the project:</span></span>

- <span data-ttu-id="b63fc-177">Products.cs는 OData 끝점을 구현 하는 Web API 컨트롤러를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-177">Products.cs defines the Web API controller that implements the OData endpoint.</span></span>
- <span data-ttu-id="b63fc-178">ProductServiceContext.cs는 Entity Framework를 사용 하 여 기본 데이터베이스를 쿼리 하는 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-178">ProductServiceContext.cs provides methods to query the underlying database, using Entity Framework.</span></span>

![](creating-an-odata-endpoint/_static/image11.png)

<a id="edm"></a>
## <a name="add-the-edm-and-route"></a><span data-ttu-id="b63fc-179">EDM 및 경로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-179">Add the EDM and Route</span></span>

<span data-ttu-id="b63fc-180">솔루션 탐색기에서 앱 확장\_폴더를 시작 하 고 WebApiConfig.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-180">In Solution Explorer, expand the App\_Start folder and open the file named WebApiConfig.cs.</span></span> <span data-ttu-id="b63fc-181">이 클래스는 웹 API에 대 한 구성 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-181">This class holds configuration code for Web API.</span></span> <span data-ttu-id="b63fc-182">이 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-182">Replace this code with the following:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample2.cs)]

<span data-ttu-id="b63fc-183">이 코드는 두 가지를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-183">This code does two things:</span></span>

- <span data-ttu-id="b63fc-184">OData 끝점에 대 한 엔터티 데이터 모델 (EDM)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-184">Creates an Entity Data Model (EDM) for the OData endpoint.</span></span>
- <span data-ttu-id="b63fc-185">끝점에 대 한 경로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-185">Adds a route for the endpoint.</span></span>

<span data-ttu-id="b63fc-186">EDM은 데이터의 추상적 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-186">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="b63fc-187">EDM 메타 데이터 문서를 만들고 서비스에 대 한 Uri를 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-187">The EDM is used to create the metadata document and define the URIs for the service.</span></span> <span data-ttu-id="b63fc-188">합니다 **ODataConventionModelBuilder** EDM 기본 명명 규칙의 집합을 사용 하 여 EDM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-188">The **ODataConventionModelBuilder** creates an EDM by using a set of default naming conventions EDM.</span></span> <span data-ttu-id="b63fc-189">이 방법은 최소한의 코드에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-189">This approach requires the least code.</span></span> <span data-ttu-id="b63fc-190">EDM 통해 더 많은 제어를 원하는 경우 사용할 수 있습니다 합니다 **된 ODataModelBuilder** 속성, 키 및 탐색 속성을 명시적으로 추가 하 여 EDM을 만들려면 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-190">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="b63fc-191">합니다 **EntitySet** 메서드는 엔터티 집합 EDM을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-191">The **EntitySet** method adds an entity set to the EDM:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample3.cs)]

<span data-ttu-id="b63fc-192">문자열 "제품" 엔터티 집합의 이름을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-192">The string "Products" defines the name of the entity set.</span></span> <span data-ttu-id="b63fc-193">컨트롤러의 이름에는 엔터티 집합의 이름과 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-193">The name of the controller must match the name of the entity set.</span></span> <span data-ttu-id="b63fc-194">이 자습서에서는 엔터티 집합 이름은 "제품" 및 컨트롤러 라는 `ProductsController`합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-194">In this tutorial, the entity set is named "Products" and the controller is named `ProductsController`.</span></span> <span data-ttu-id="b63fc-195">명명 된 엔터티 집합 "ProductSet", 컨트롤러 이름을 `ProductSetController`입니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-195">If you named the entity set "ProductSet", you would name the controller `ProductSetController`.</span></span> <span data-ttu-id="b63fc-196">끝점에 여러 엔터티 집합에 있을 수 있음을 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-196">Note that an endpoint can have multiple entity sets.</span></span> <span data-ttu-id="b63fc-197">호출 **EntitySet&lt;T&gt;**  각 엔터티에 대 한 설정 및 해당 컨트롤러를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-197">Call **EntitySet&lt;T&gt;** for each entity set, and then define a corresponding controller.</span></span>

<span data-ttu-id="b63fc-198">합니다 **MapODataRoute** 메서드 OData 끝점에 대 한 경로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-198">The **MapODataRoute** method adds a route for the OData endpoint.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample4.cs)]

<span data-ttu-id="b63fc-199">첫 번째 매개 변수는 경로의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-199">The first parameter is a friendly name for the route.</span></span> <span data-ttu-id="b63fc-200">서비스의 클라이언트가이 이름은 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-200">Clients of your service do not see this name.</span></span> <span data-ttu-id="b63fc-201">두 번째 매개 변수는 끝점에 대 한 URI 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-201">The second parameter is the URI prefix for the endpoint.</span></span> <span data-ttu-id="b63fc-202">이 코드를 지정 하는, Products 엔터티 집합에 대 한 URI가 http://<em>hostname</em>odata/제품입니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-202">Given this code, the URI for the Products entity set is http://<em>hostname</em>/odata/Products.</span></span> <span data-ttu-id="b63fc-203">응용 프로그램에 OData 끝점을 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-203">Your application can have more than one OData endpoint.</span></span> <span data-ttu-id="b63fc-204">각 끝점에 대 한 호출 <strong>MapODataRoute</strong> 고유 경로 이름 및 고유한 URI 접두사를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-204">For each endpoint, call <strong>MapODataRoute</strong> and provide a unique route name and a unique URI prefix.</span></span>

<a id="seed-db"></a>
## <a name="seed-the-database-optional"></a><span data-ttu-id="b63fc-205">(선택 사항) 데이터베이스 시드</span><span class="sxs-lookup"><span data-stu-id="b63fc-205">Seed the Database (Optional)</span></span>

<span data-ttu-id="b63fc-206">이 단계에서는 일부 테스트 데이터를 사용 하 여 데이터베이스를 시드하려면 Entity Framework를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-206">In this step, you will use Entity Framework to seed the database with some test data.</span></span> <span data-ttu-id="b63fc-207">이 단계는 선택 사항이 있지만 OData 끝점을 즉시 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-207">This step is optional, but it lets you test out your OData endpoint right away.</span></span>

<span data-ttu-id="b63fc-208">**도구** 메뉴에서 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-208">From the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="b63fc-209">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-209">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample5.cmd)]

<span data-ttu-id="b63fc-210">이 마이그레이션 및 Configuration.cs 라는 코드 파일 이라는 폴더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-210">This adds a folder named Migrations and a code file named Configuration.cs.</span></span>

![](creating-an-odata-endpoint/_static/image12.png)

<span data-ttu-id="b63fc-211">이 파일을 열고 다음 코드를 추가 합니다 `Configuration.Seed` 메서드.</span><span class="sxs-lookup"><span data-stu-id="b63fc-211">Open this file and add the following code to the `Configuration.Seed` method.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample6.cs)]

<span data-ttu-id="b63fc-212">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-212">In the Package Manager Console Window, enter the following commands:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample7.cmd)]

<span data-ttu-id="b63fc-213">이러한 명령은 데이터베이스를 만들고 다음 코드를 실행 하는 코드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-213">These commands generate code that creates the database, and then executes that code.</span></span>

<a id="explore"></a>
## <a name="exploring-the-odata-endpoint"></a><span data-ttu-id="b63fc-214">OData 끝점을 탐색</span><span class="sxs-lookup"><span data-stu-id="b63fc-214">Exploring the OData Endpoint</span></span>

<span data-ttu-id="b63fc-215">이 섹션에서는 사용 된 [Fiddler Web Debugging Proxy](http://www.fiddler2.com) 끝점에 요청을 보내고 응답 메시지를 검토 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-215">In this section, we'll use the [Fiddler Web Debugging Proxy](http://www.fiddler2.com) to send requests to the endpoint and examine the response messages.</span></span> <span data-ttu-id="b63fc-216">OData 끝점의 기능을 이해 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-216">This will help you to understand the capabilities of an OData endpoint.</span></span>

<span data-ttu-id="b63fc-217">Visual Studio에서 f5 키를 눌러 디버깅을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-217">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="b63fc-218">기본적으로 Visual Studio는 브라우저를 엽니다 `http://localhost:*port*`, 여기서 *포트* 프로젝트 설정에 구성 된 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-218">By default, Visual Studio opens your browser to `http://localhost:*port*`, where *port* is the port number configured in the project settings.</span></span>

<span data-ttu-id="b63fc-219">프로젝트 설정에서 포트 번호를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-219">You can change the port number in the project settings.</span></span> <span data-ttu-id="b63fc-220">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-220">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="b63fc-221">속성 창에서 선택 **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-221">In the properties window, select **Web**.</span></span> <span data-ttu-id="b63fc-222">아래의 포트 번호를 입력 **프로젝트 Url**합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-222">Enter the port number under **Project Url**.</span></span>

### <a name="service-document"></a><span data-ttu-id="b63fc-223">서비스 문서</span><span class="sxs-lookup"><span data-stu-id="b63fc-223">Service Document</span></span>

<span data-ttu-id="b63fc-224">합니다 *서비스 문서* OData 끝점에 대 한 엔터티 집합의 목록을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-224">The *service document* contains a list of the entity sets for the OData endpoint.</span></span> <span data-ttu-id="b63fc-225">서비스 문서를 가져오려면 서비스의 루트 URI에 GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-225">To get the service document, send a GET request to the root URI of the service.</span></span>

<span data-ttu-id="b63fc-226">Fiddler를 사용 하 여의 다음 URI를 입력 합니다 **작성기** 탭: `http://localhost:port/odata/`여기서 *포트* 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-226">Using Fiddler, enter the following URI in the **Composer** tab: `http://localhost:port/odata/`, where *port* is the port number.</span></span>

![](creating-an-odata-endpoint/_static/image13.png)

<span data-ttu-id="b63fc-227">클릭 합니다 **Execute** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-227">Click the **Execute** button.</span></span> <span data-ttu-id="b63fc-228">Fiddler는 응용 프로그램에 HTTP GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-228">Fiddler sends an HTTP GET request to your application.</span></span> <span data-ttu-id="b63fc-229">웹 세션 목록의 응답이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-229">You should see the response in the Web Sessions list.</span></span> <span data-ttu-id="b63fc-230">모든 것이 작동 하는 경우 상태 코드 200 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-230">If everything is working, the status code will be 200.</span></span>

![](creating-an-odata-endpoint/_static/image14.png)

<span data-ttu-id="b63fc-231">Inspectors 탭에서 응답 메시지의 세부 정보를 보려면 웹 세션 목록의 응답을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-231">Double-click the response in the Web Sessions list to see the details of the response message in the Inspectors tab.</span></span>

![](creating-an-odata-endpoint/_static/image15.png)

<span data-ttu-id="b63fc-232">원시 HTTP 응답 메시지는 다음과 비슷하게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-232">The raw HTTP response message should look similar to the following:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample8.cmd)]

<span data-ttu-id="b63fc-233">기본적으로 웹 API는 AtomPub 형식에서 서비스 문서를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-233">By default, Web API returns the service document in AtomPub format.</span></span> <span data-ttu-id="b63fc-234">JSON을 요청 하려면 HTTP 요청에 다음 헤더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-234">To request JSON, add the following header to the HTTP request:</span></span>

`Accept: application/json`

![](creating-an-odata-endpoint/_static/image16.png)

<span data-ttu-id="b63fc-235">이제 HTTP 응답에 JSON 페이로드를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-235">Now the HTTP response contains a JSON payload:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample9.cmd)]

### <a name="service-metadata-document"></a><span data-ttu-id="b63fc-236">서비스 메타 데이터 문서</span><span class="sxs-lookup"><span data-stu-id="b63fc-236">Service Metadata Document</span></span>

<span data-ttu-id="b63fc-237">합니다 *서비스 메타 데이터 문서* 개념적 스키마 정의 언어 (CSDL) 이라는 XML 언어를 사용 하 여 서비스의 데이터 모델을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-237">The *service metadata document* describes the data model of the service, using an XML language called the Conceptual Schema Definition Language (CSDL).</span></span> <span data-ttu-id="b63fc-238">메타 데이터 문서를 서비스에서 데이터의 구조를 표시 및 사용 하 여 클라이언트 코드를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-238">The metadata document shows the structure of the data in the service, and can be used to generate client code.</span></span>

<span data-ttu-id="b63fc-239">메타 데이터 문서를 가져오려면에 GET 요청을 보냄 `http://localhost:port/odata/$metadata`합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-239">To get the metadata document, send a GET request to `http://localhost:port/odata/$metadata`.</span></span> <span data-ttu-id="b63fc-240">이 자습서에 표시 된 끝점에 대 한 메타 데이터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-240">Here is the metadata for the endpoint shown in this tutorial.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample10.cmd)]

### <a name="entity-set"></a><span data-ttu-id="b63fc-241">엔터티 집합</span><span class="sxs-lookup"><span data-stu-id="b63fc-241">Entity Set</span></span>

<span data-ttu-id="b63fc-242">Products 엔터티 집합을 가져오려면에 GET 요청을 보냄 `http://localhost:port/odata/Products`합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-242">To get the Products entity set, send a GET request to `http://localhost:port/odata/Products`.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample11.cmd)]

### <a name="entity"></a><span data-ttu-id="b63fc-243">엔터티</span><span class="sxs-lookup"><span data-stu-id="b63fc-243">Entity</span></span>

<span data-ttu-id="b63fc-244">개별 제품을 가져오려면에 GET 요청을 보냄 `http://localhost:port/odata/Products(1)`, 여기서 "1"은 제품 id입니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-244">To get an individual product, send a GET request to `http://localhost:port/odata/Products(1)`, where "1" is the product ID.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample12.cmd)]

<a id="formats"></a>
## <a name="odata-serialization-formats"></a><span data-ttu-id="b63fc-245">OData 직렬화 형식</span><span class="sxs-lookup"><span data-stu-id="b63fc-245">OData Serialization Formats</span></span>

<span data-ttu-id="b63fc-246">OData는 몇 가지 직렬화 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-246">OData supports several serialization formats:</span></span>

- <span data-ttu-id="b63fc-247">Atom Pub (XML)</span><span class="sxs-lookup"><span data-stu-id="b63fc-247">Atom Pub (XML)</span></span>
- <span data-ttu-id="b63fc-248">JSON "light" (OData v3에 도입 됨)</span><span class="sxs-lookup"><span data-stu-id="b63fc-248">JSON "light" (introduced in OData v3)</span></span>
- <span data-ttu-id="b63fc-249">JSON "verbose" (OData v2)</span><span class="sxs-lookup"><span data-stu-id="b63fc-249">JSON "verbose" (OData v2)</span></span>

<span data-ttu-id="b63fc-250">기본적으로 웹 API AtomPubJSON "light" 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-250">By default, Web API uses AtomPubJSON "light" format.</span></span> 

<span data-ttu-id="b63fc-251">AtomPub 형식을 가져오려고 Accept 헤더를 "application/atom + xml"로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-251">To get AtomPub format, set the Accept header to "application/atom+xml".</span></span> <span data-ttu-id="b63fc-252">예제 응답 본문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-252">Here is an example response body:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample13.cmd)]

<span data-ttu-id="b63fc-253">Atom 형식의 가지 명백한 단점이 볼 수 있습니다: JSON light 보다 훨씬 더 자세 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-253">You can see one obvious disadvantage of the Atom format: It's a lot more verbose than the JSON light.</span></span> <span data-ttu-id="b63fc-254">그러나 AtomPub에서 인식할 수 있는 클라이언트에 있는 경우 클라이언트는 JSON을 통해 해당 형식의 선호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-254">However, if you have a client that understands AtomPub, the client might prefer that format over JSON.</span></span>

<span data-ttu-id="b63fc-255">다음은 동일한 엔터티의 JSON 라이트 버전이입니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-255">Here is the JSON light version of the same entity:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample14.cmd)]

<span data-ttu-id="b63fc-256">JSON light 형식 OData 프로토콜의 버전 3에에서 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-256">The JSON light format was introduced in version 3 of the OData protocol.</span></span> <span data-ttu-id="b63fc-257">이전 버전과 호환성을 위해 클라이언트는 이전 "verbose" JSON 형식으로 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-257">For backward compatibility, a client can request the older "verbose" JSON format.</span></span> <span data-ttu-id="b63fc-258">상세 JSON을 요청 하려면 Accept 헤더를 설정할 `application/json;odata=verbose`합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-258">To request verbose JSON, set the Accept header to `application/json;odata=verbose`.</span></span> <span data-ttu-id="b63fc-259">자세한 정보 버전은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-259">Here is the verbose version:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample15.cmd)]

<span data-ttu-id="b63fc-260">이 형식은 전체 세션을 통해 상당한 오버 헤드를 추가할 수 있는 응답 본문에 더 많은 메타 데이터를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-260">This format conveys more metadata in the response body, which can add considerable overhead over an entire session.</span></span> <span data-ttu-id="b63fc-261">또한 "d" 라는 속성에서 개체를 래핑하여 간접 참조 수준을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-261">Also, it adds a level of indirection by wrapping the object in a property named "d".</span></span>

## <a name="next-steps"></a><span data-ttu-id="b63fc-262">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b63fc-262">Next Steps</span></span>

- [<span data-ttu-id="b63fc-263">엔터티 관계 추가</span><span class="sxs-lookup"><span data-stu-id="b63fc-263">Add Entity Relations</span></span>](working-with-entity-relations.md)
- [<span data-ttu-id="b63fc-264">OData 작업 추가</span><span class="sxs-lookup"><span data-stu-id="b63fc-264">Add OData Actions</span></span>](odata-actions.md)
- [<span data-ttu-id="b63fc-265">.NET 클라이언트에서 OData 서비스를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b63fc-265">Call the OData Service From a .NET Client</span></span>](calling-an-odata-service-from-a-net-client.md)
