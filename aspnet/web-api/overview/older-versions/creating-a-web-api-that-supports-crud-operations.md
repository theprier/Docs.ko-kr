---
uid: web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
title: "ASP.NET Web API 1의에서 CRUD 작업을 사용 하도록 설정 | Microsoft Docs"
author: MikeWasson
description: "이 자습서에는 ASP.NET Web API를 사용 하 여 HTTP 서비스의 CRUD 작업을 지 원하는 방법을 보여 줍니다. 자습서 Visual Studio 2012 웹 AP에 사용 되는 소프트웨어 버전 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/28/2012
ms.topic: article
ms.assetid: c125ca47-606a-4d6f-a1fc-1fc62928af93
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
msc.type: authoredcontent
ms.openlocfilehash: 69b7d5453b6ff36d6e28a69428b016cb8cfd06e9
ms.sourcegitcommit: 016f4d58663bcd442930227022de23fb3abee0b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
<a name="enabling-crud-operations-in-aspnet-web-api-1"></a><span data-ttu-id="e38c1-104">ASP.NET Web API 1의에서 CRUD 작업을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="e38c1-104">Enabling CRUD Operations in ASP.NET Web API 1</span></span>
====================
<span data-ttu-id="e38c1-105">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="e38c1-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="e38c1-106">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-c4761894)

> <span data-ttu-id="e38c1-107">이 자습서에는 ASP.NET Web API를 사용 하 여 HTTP 서비스의 CRUD 작업을 지 원하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-107">This tutorial shows how to support CRUD operations in an HTTP service using ASP.NET Web API.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e38c1-108">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="e38c1-108">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="e38c1-109">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="e38c1-109">Visual Studio 2012</span></span>
> - <span data-ttu-id="e38c1-110">Web API 1 (도 Web API 2와 작동)</span><span class="sxs-lookup"><span data-stu-id="e38c1-110">Web API 1 (also works with Web API 2)</span></span>


<span data-ttu-id="e38c1-111">에 대 한 CRUD stands &quot;만들기, 읽기, 업데이트 및 삭제,&quot; 는 네 가지 기본적인 데이터베이스 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-111">CRUD stands for &quot;Create, Read, Update, and Delete,&quot; which are the four basic database operations.</span></span> <span data-ttu-id="e38c1-112">또한 많은 HTTP 서비스 REST 또는 유사한 REST Api를 통해 CRUD 작업을 모델링합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-112">Many HTTP services also model CRUD operations through REST or REST-like APIs.</span></span>

<span data-ttu-id="e38c1-113">이 자습서에서는 매우 간단한 웹 제품 목록을 관리 하는 API를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-113">In this tutorial, you will build a very simple web API to manage a list of products.</span></span> <span data-ttu-id="e38c1-114">각 제품 이름, 가격 및 범주에 포함 됩니다 (예: &quot;toys&quot; 또는 &quot;하드웨어&quot;), 및 제품 id입니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-114">Each product will contain a name, price, and category (such as &quot;toys&quot; or &quot;hardware&quot;), plus a product ID.</span></span>

<span data-ttu-id="e38c1-115">제품 API는 다음 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-115">The products API will expose following methods.</span></span>

| <span data-ttu-id="e38c1-116">작업</span><span class="sxs-lookup"><span data-stu-id="e38c1-116">Action</span></span> | <span data-ttu-id="e38c1-117">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="e38c1-117">HTTP method</span></span> | <span data-ttu-id="e38c1-118">상대 URI</span><span class="sxs-lookup"><span data-stu-id="e38c1-118">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e38c1-119">모든 제품 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="e38c1-119">Get a list of all products</span></span> | <span data-ttu-id="e38c1-120">가져오기</span><span class="sxs-lookup"><span data-stu-id="e38c1-120">GET</span></span> | <span data-ttu-id="e38c1-121">/ api/제품</span><span class="sxs-lookup"><span data-stu-id="e38c1-121">/api/products</span></span> |
| <span data-ttu-id="e38c1-122">제품을 ID 별로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-122">Get a product by ID</span></span> | <span data-ttu-id="e38c1-123">가져오기</span><span class="sxs-lookup"><span data-stu-id="e38c1-123">GET</span></span> | <span data-ttu-id="e38c1-124">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="e38c1-124">/api/products/*id*</span></span> |
| <span data-ttu-id="e38c1-125">제품 범주별으로 가져오기</span><span class="sxs-lookup"><span data-stu-id="e38c1-125">Get a product by category</span></span> | <span data-ttu-id="e38c1-126">가져오기</span><span class="sxs-lookup"><span data-stu-id="e38c1-126">GET</span></span> | <span data-ttu-id="e38c1-127">/api/products?category=*category*</span><span class="sxs-lookup"><span data-stu-id="e38c1-127">/api/products?category=*category*</span></span> |
| <span data-ttu-id="e38c1-128">새 제품 만들기</span><span class="sxs-lookup"><span data-stu-id="e38c1-128">Create a new product</span></span> | <span data-ttu-id="e38c1-129">올리기</span><span class="sxs-lookup"><span data-stu-id="e38c1-129">POST</span></span> | <span data-ttu-id="e38c1-130">/ api/제품</span><span class="sxs-lookup"><span data-stu-id="e38c1-130">/api/products</span></span> |
| <span data-ttu-id="e38c1-131">제품 업데이트</span><span class="sxs-lookup"><span data-stu-id="e38c1-131">Update a product</span></span> | <span data-ttu-id="e38c1-132">PUT</span><span class="sxs-lookup"><span data-stu-id="e38c1-132">PUT</span></span> | <span data-ttu-id="e38c1-133">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="e38c1-133">/api/products/*id*</span></span> |
| <span data-ttu-id="e38c1-134">제품 삭제</span><span class="sxs-lookup"><span data-stu-id="e38c1-134">Delete a product</span></span> | <span data-ttu-id="e38c1-135">Delete</span><span class="sxs-lookup"><span data-stu-id="e38c1-135">DELETE</span></span> | <span data-ttu-id="e38c1-136">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="e38c1-136">/api/products/*id*</span></span> |

<span data-ttu-id="e38c1-137">경로 있는 제품 ID를 포함 된 Uri의 일부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-137">Notice that some of the URIs include the product ID in path.</span></span> <span data-ttu-id="e38c1-138">예를 들어 제품 ID가 28을 가져오려면 클라이언트 보냅니다 GET 요청에 대 한 `http://hostname/api/products/28`합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-138">For example, to get the product whose ID is 28, the client sends a GET request for `http://hostname/api/products/28`.</span></span>

### <a name="resources"></a><span data-ttu-id="e38c1-139">리소스</span><span class="sxs-lookup"><span data-stu-id="e38c1-139">Resources</span></span>

<span data-ttu-id="e38c1-140">API 제품 두 개의 리소스 유형에 대 한 Uri를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-140">The products API defines URIs for two resource types:</span></span>

| <span data-ttu-id="e38c1-141">리소스</span><span class="sxs-lookup"><span data-stu-id="e38c1-141">Resource</span></span> | <span data-ttu-id="e38c1-142">URI</span><span class="sxs-lookup"><span data-stu-id="e38c1-142">URI</span></span> |
| --- | --- |
| <span data-ttu-id="e38c1-143">모든 제품의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-143">The list of all the products.</span></span> | <span data-ttu-id="e38c1-144">/ api/제품</span><span class="sxs-lookup"><span data-stu-id="e38c1-144">/api/products</span></span> |
| <span data-ttu-id="e38c1-145">개별 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-145">An individual product.</span></span> | <span data-ttu-id="e38c1-146">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="e38c1-146">/api/products/*id*</span></span> |

### <a name="methods"></a><span data-ttu-id="e38c1-147">메서드</span><span class="sxs-lookup"><span data-stu-id="e38c1-147">Methods</span></span>

<span data-ttu-id="e38c1-148">네 가지 주요 HTTP 메서드 (GET, PUT, POST 및 DELETE)는 다음과 같이 CRUD 작업에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-148">The four main HTTP methods (GET, PUT, POST, and DELETE) can be mapped to CRUD operations as follows:</span></span>

- <span data-ttu-id="e38c1-149">GET 검색 지정된 된 URI에 리소스를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-149">GET retrieves the representation of the resource at a specified URI.</span></span> <span data-ttu-id="e38c1-150">서버에서 GET에 파생 작업이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-150">GET should have no side effects on the server.</span></span>
- <span data-ttu-id="e38c1-151">PUT 지정된 된 URI에 리소스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-151">PUT updates a resource at a specified URI.</span></span> <span data-ttu-id="e38c1-152">이 서버에 새 Uri를 지정 하는 클라이언트에서는 PUT 지정된 된 URI에 새 리소스를 만드는 데도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-152">PUT can also be used to create a new resource at a specified URI, if the server allows clients to specify new URIs.</span></span> <span data-ttu-id="e38c1-153">이 자습서에서는 API는 PUT 통해 생성을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-153">For this tutorial, the API will not support creation through PUT.</span></span>
- <span data-ttu-id="e38c1-154">게시는 새 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-154">POST creates a new resource.</span></span> <span data-ttu-id="e38c1-155">서버는 새 개체에 대 한 URI를 할당 하 고 응답 메시지의 일부로이 URI를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-155">The server assigns the URI for the new object and returns this URI as part of the response message.</span></span>
- <span data-ttu-id="e38c1-156">삭제 지정된 된 URI에 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-156">DELETE deletes a resource at a specified URI.</span></span>

<span data-ttu-id="e38c1-157">참고: PUT 메서드는 전체 제품 엔터티를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-157">Note: The PUT method replaces the entire product entity.</span></span> <span data-ttu-id="e38c1-158">즉, 클라이언트는 업데이트 된 제품의 전체 표현을 전송 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-158">That is, the client is expected to send a complete representation of the updated product.</span></span> <span data-ttu-id="e38c1-159">부분 업데이트를 지원 하려는 경우 PATCH 메서드를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-159">If you want to support partial updates, the PATCH method is preferred.</span></span> <span data-ttu-id="e38c1-160">이 자습서는 패치를 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-160">This tutorial does not implement PATCH.</span></span>

## <a name="create-a-new-web-api-project"></a><span data-ttu-id="e38c1-161">새 웹 API 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="e38c1-161">Create a New Web API Project</span></span>

<span data-ttu-id="e38c1-162">Visual Studio를 실행 하 여 시작 하 고 선택 **새 프로젝트** 에서 **시작** 페이지.</span><span class="sxs-lookup"><span data-stu-id="e38c1-162">Start by running Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="e38c1-163">또는에서 **파일** 메뉴 선택 **새로** 차례로 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-163">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="e38c1-164">에 **템플릿** 창 선택 **설치 된 템플릿** 확장는 **Visual C#** 노드.</span><span class="sxs-lookup"><span data-stu-id="e38c1-164">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="e38c1-165">아래 **Visual C#**선택, **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-165">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="e38c1-166">프로젝트 템플릿 목록에서 선택 **ASP.NET MVC 4 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-166">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="e38c1-167">프로젝트 이름을 &quot;ProductStore&quot; 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-167">Name the project &quot;ProductStore&quot; and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image1.png)

<span data-ttu-id="e38c1-168">에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **웹 API** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-168">In the **New ASP.NET MVC 4 Project** dialog, select **Web API** and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image2.png)

## <a name="adding-a-model"></a><span data-ttu-id="e38c1-169">모델 추가</span><span class="sxs-lookup"><span data-stu-id="e38c1-169">Adding a Model</span></span>

<span data-ttu-id="e38c1-170">*모델*은 응용 프로그램에서 데이터를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-170">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="e38c1-171">ASP.NET Web API에서 강력한 형식의 CLR 개체 모델을 사용할 수 있습니다 및은 자동으로 직렬화 됩니다 XML 또는 JSON을 클라이언트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-171">In ASP.NET Web API, you can use strongly typed CLR objects as models, and they will automatically be serialized to XML or JSON for the client.</span></span>

<span data-ttu-id="e38c1-172">ProductStore API에 대 한 데이터 이루어지며, 제품의 라는 새 클래스를 만들겠습니다 `Product`합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-172">For the ProductStore API, our data consists of products, so we'll create a new class named `Product`.</span></span>

<span data-ttu-id="e38c1-173">솔루션 탐색기 표시 되지 않는 경우 클릭는 **보기** 메뉴와 선택 **솔루션 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-173">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="e38c1-174">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭는 **모델** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-174">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="e38c1-175">상황에 맞는 meny에서 선택 **추가**을 선택한 후 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-175">From the context meny, select **Add**, then select **Class**.</span></span> <span data-ttu-id="e38c1-176">클래스의 이름을 &quot;제품&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-176">Name the class &quot;Product&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image3.png)

<span data-ttu-id="e38c1-177">다음 속성을 추가 `Product` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-177">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample1.cs)]

## <a name="adding-a-repository"></a><span data-ttu-id="e38c1-178">리포지토리 추가</span><span class="sxs-lookup"><span data-stu-id="e38c1-178">Adding a Repository</span></span>

<span data-ttu-id="e38c1-179">제품 컬렉션을 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-179">We need to store a collection of products.</span></span> <span data-ttu-id="e38c1-180">서비스 구현에서 컬렉션을 분리 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-180">It's a good idea to separate the collection from our service implementation.</span></span> <span data-ttu-id="e38c1-181">이런 방식으로 백업 저장소 서비스 클래스를 다시 작성 하지 않고 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-181">That way, we can change the backing store without rewriting the service class.</span></span> <span data-ttu-id="e38c1-182">이러한 유형의 설계 라고는 *리포지토리* 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-182">This type of design is called the *repository* pattern.</span></span> <span data-ttu-id="e38c1-183">저장소에 대 한 제네릭 인터페이스를 정의 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-183">Start by defining a generic interface for the repository.</span></span>

<span data-ttu-id="e38c1-184">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭는 **모델** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-184">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="e38c1-185">선택 **추가**을 선택한 후 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-185">Select **Add**, then select **New Item**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image4.png)

<span data-ttu-id="e38c1-186">에 **템플릿** 창 선택 **설치 된 템플릿** C# 노드를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-186">In the **Templates** pane, select **Installed Templates** and expand the C# node.</span></span> <span data-ttu-id="e38c1-187">C#에서 선택 **코드**합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-187">Under C#, select **Code**.</span></span> <span data-ttu-id="e38c1-188">코드 서식 파일의 목록에서 선택 **인터페이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-188">In the list of code templates, select **Interface**.</span></span> <span data-ttu-id="e38c1-189">인터페이스 이름을 &quot;IProductRepository&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-189">Name the interface &quot;IProductRepository&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image5.png)

<span data-ttu-id="e38c1-190">다음과 같은 구현을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-190">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample2.cs)]

<span data-ttu-id="e38c1-191">이제 명명 된 모델 폴더에 다른 클래스를 추가할 &quot;ProductRepository 합니다.&quot; 이 클래스는 `IProductRespository` 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-191">Now add another class to the Models folder, named &quot;ProductRepository.&quot; This class will implement the `IProductRespository` interface.</span></span> <span data-ttu-id="e38c1-192">다음과 같은 구현을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-192">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample3.cs)]

<span data-ttu-id="e38c1-193">저장소는 목록 로컬 메모리에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-193">The repository keeps the list in local memory.</span></span> <span data-ttu-id="e38c1-194">자습서의 경우이 정상 되지만 실제 응용 프로그램에서 데이터 외부적으로 두 데이터베이스를 저장할 수 있습니다 또는 클라우드 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-194">This is OK for a tutorial, but in a real application, you would store the data externally, either a database or in cloud storage.</span></span> <span data-ttu-id="e38c1-195">리포지토리 패턴 구현을 변경 합니다. 나중에 쉽게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-195">The repository pattern will make it easier to change the implementation later.</span></span>

## <a name="adding-a-web-api-controller"></a><span data-ttu-id="e38c1-196">웹 API 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="e38c1-196">Adding a Web API Controller</span></span>

<span data-ttu-id="e38c1-197">ASP.NET MVC와 함께 작업 하는 경우 다음 이미 잘 알고 있다면 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-197">If you have worked with ASP.NET MVC, then you are already familiar with controllers.</span></span> <span data-ttu-id="e38c1-198">ASP.NET Web API에는 *컨트롤러* 클라이언트로부터 HTTP 요청을 처리 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-198">In ASP.NET Web API, a *controller* is a class that handles HTTP requests from the client.</span></span> <span data-ttu-id="e38c1-199">새 프로젝트 마법사 프로젝트를 만들 때 사용자에 대 한 두 명의 컨트롤러를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-199">The New Project wizard created two controllers for you when it created the project.</span></span> <span data-ttu-id="e38c1-200">내용을 보려면 솔루션 탐색기에서 Controllers 폴더를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-200">To see them, expand the Controllers folder in Solution Explorer.</span></span>

- <span data-ttu-id="e38c1-201">HomeController 기존의 ASP.NET MVC 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-201">HomeController is a traditional ASP.NET MVC controller.</span></span> <span data-ttu-id="e38c1-202">사이트에 대 한 HTML 페이지를 서비스 하 고 웹 API 직접 관련이 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-202">It is responsible for serving HTML pages for the site, and is not directly related to our web API.</span></span>
- <span data-ttu-id="e38c1-203">ValuesController에는 예제 WebAPI 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-203">ValuesController is an example WebAPI controller.</span></span>

<span data-ttu-id="e38c1-204">솔루션 탐색기에서 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 ValuesController, 삭제 **삭제 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e38c1-204">Go ahead and delete ValuesController, by right-clicking the file in Solution Explorer and selecting **Delete.**</span></span> <span data-ttu-id="e38c1-205">이제 다음과 같이 새로운 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-205">Now add a new controller, as follows:</span></span>

<span data-ttu-id="e38c1-206">**솔루션 탐색기**, Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-206">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="e38c1-207">선택 **추가** 선택한 후 **컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-207">Select **Add** and then select **Controller**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image6.png)

<span data-ttu-id="e38c1-208">에 **컨트롤러 추가** 마법사, 컨트롤러 이름 &quot;ProductsController&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-208">In the **Add Controller** wizard, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="e38c1-209">에 **템플릿** 드롭 다운 목록 **빈 API 컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-209">In the **Template** drop-down list, select **Empty API Controller**.</span></span> <span data-ttu-id="e38c1-210">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-210">Then click **Add**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="e38c1-211">프로그램 contollers 컨트롤러 이라는 폴더에 배치할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-211">It is not necessary to put your contollers into a folder named Controllers.</span></span> <span data-ttu-id="e38c1-212">폴더 이름은 중요 하지 않습니다. 단순히 소스 파일을 구성 하는 편리한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-212">The folder name is not important; it is simply a convenient way to organize your source files.</span></span>


<span data-ttu-id="e38c1-213">**컨트롤러 추가** 마법사 라는 ProductsController.cs Controllers 폴더의 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-213">The **Add Controller** wizard will create a file named ProductsController.cs in the Controllers folder.</span></span> <span data-ttu-id="e38c1-214">이 파일이 열려 있지 않으면 이미 열려는 파일을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-214">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="e38c1-215">다음 추가 **를 사용 하 여** 문:</span><span class="sxs-lookup"><span data-stu-id="e38c1-215">Add the following **using** statement:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample4.cs)]

<span data-ttu-id="e38c1-216">추가 포함 하는 필드는 **IProductRepository** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="e38c1-216">Add a field that holds an **IProductRepository** instance.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample5.cs)]

> [!NOTE]
> <span data-ttu-id="e38c1-217">호출 `new ProductRepository()` 컨트롤러에 없는 가장 좋은 디자인 컨트롤러의 특정 구현에 있어 유연성이 `IProductRepository`합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-217">Calling `new ProductRepository()` in the controller is not the best design, because it ties the controller to a particular implementation of `IProductRepository`.</span></span> <span data-ttu-id="e38c1-218">더 나은 방법은 참조 하십시오. [웹 API 종속성 확인자를 사용 하 여](../advanced/dependency-injection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-218">For a better approach, see [Using the Web API Dependency Resolver](../advanced/dependency-injection.md).</span></span>


## <a name="getting-a-resource"></a><span data-ttu-id="e38c1-219">리소스 가져오기</span><span class="sxs-lookup"><span data-stu-id="e38c1-219">Getting a Resource</span></span>

<span data-ttu-id="e38c1-220">ProductStore API 몇 가지를 노출 하는 &quot;읽을&quot; HTTP GET 메서드로 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-220">The ProductStore API will expose several &quot;read&quot; actions as HTTP GET methods.</span></span> <span data-ttu-id="e38c1-221">각 동작의 메서드에 해당 됩니다는 `ProductsController` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-221">Each action will correspond to a method in the `ProductsController` class.</span></span>

| <span data-ttu-id="e38c1-222">작업</span><span class="sxs-lookup"><span data-stu-id="e38c1-222">Action</span></span> | <span data-ttu-id="e38c1-223">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="e38c1-223">HTTP method</span></span> | <span data-ttu-id="e38c1-224">상대 URI</span><span class="sxs-lookup"><span data-stu-id="e38c1-224">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e38c1-225">모든 제품 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="e38c1-225">Get a list of all products</span></span> | <span data-ttu-id="e38c1-226">가져오기</span><span class="sxs-lookup"><span data-stu-id="e38c1-226">GET</span></span> | <span data-ttu-id="e38c1-227">/ api/제품</span><span class="sxs-lookup"><span data-stu-id="e38c1-227">/api/products</span></span> |
| <span data-ttu-id="e38c1-228">제품을 ID 별로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-228">Get a product by ID</span></span> | <span data-ttu-id="e38c1-229">가져오기</span><span class="sxs-lookup"><span data-stu-id="e38c1-229">GET</span></span> | <span data-ttu-id="e38c1-230">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="e38c1-230">/api/products/*id*</span></span> |
| <span data-ttu-id="e38c1-231">제품 범주별으로 가져오기</span><span class="sxs-lookup"><span data-stu-id="e38c1-231">Get a product by category</span></span> | <span data-ttu-id="e38c1-232">가져오기</span><span class="sxs-lookup"><span data-stu-id="e38c1-232">GET</span></span> | <span data-ttu-id="e38c1-233">/api/products?category=*category*</span><span class="sxs-lookup"><span data-stu-id="e38c1-233">/api/products?category=*category*</span></span> |

<span data-ttu-id="e38c1-234">모든 제품의 목록을 얻으려면 추가 하려면이 메서드는 `ProductsController` 클래스:</span><span class="sxs-lookup"><span data-stu-id="e38c1-234">To get the list of all products, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample6.cs)]

<span data-ttu-id="e38c1-235">메서드 이름으로 시작 &quot;가져오기&quot;이므로 규칙으로 GET 요청에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-235">The method name starts with &quot;Get&quot;, so by convention it maps to GET requests.</span></span> <span data-ttu-id="e38c1-236">또한 메서드가 매개 변수 없이 이기 때문에 매핑될 포함 하지 않는 URI는  *&quot;id&quot;*  는 경로의 세그먼트입니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-236">Also, because the method has no parameters, it maps to a URI that does not contain an *&quot;id&quot;* segment in the path.</span></span>

<span data-ttu-id="e38c1-237">ID 별로 제품을 가져오려면 추가 하려면이 메서드는 `ProductsController` 클래스:</span><span class="sxs-lookup"><span data-stu-id="e38c1-237">To get a product by ID, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample7.cs)]

<span data-ttu-id="e38c1-238">이 메서드 이름이로 시작 &quot;가져오기&quot;, 메서드가 명명 된 매개 변수가 있지만 *id*합니다. 이 매개 변수는 매핑됩니다는 &quot;id&quot; 의 URI 경로 세그먼트입니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-238">This method name also starts with &quot;Get&quot;, but the method has a parameter named *id*. This parameter is mapped to the &quot;id&quot; segment of the URI path.</span></span> <span data-ttu-id="e38c1-239">ASP.NET Web API 프레임 워크를 올바른 데이터 형식 ID를 자동으로 변환 (**int**) 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-239">The ASP.NET Web API framework automatically converts the ID to the correct data type (**int**) for the parameter.</span></span>

<span data-ttu-id="e38c1-240">GetProduct 메서드에서 형식의 예외를 throw **HttpResponseException** 경우 *id* 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-240">The GetProduct method throws an exception of type **HttpResponseException** if *id* is not valid.</span></span> <span data-ttu-id="e38c1-241">이 예외는 404 (찾을 수 없음) 오류에 프레임 워크에 의해 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-241">This exception will be translated by the framework into a 404 (Not Found) error.</span></span>

<span data-ttu-id="e38c1-242">마지막으로 제품 범주별으로 검색 하려면 메서드 추가:</span><span class="sxs-lookup"><span data-stu-id="e38c1-242">Finally, add a method to find products by category:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample8.cs)]

<span data-ttu-id="e38c1-243">요청에 있는 경우 URI 쿼리 문자열을 Web API 컨트롤러 메서드의 매개 변수를 쿼리 매개 변수와 일치 하려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-243">If the request URI has a query string, Web API tries to match the query parameters to parameters on the controller method.</span></span> <span data-ttu-id="e38c1-244">따라서 폼의 URI "api/제품? category =*범주*"이 메서드에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-244">Therefore, a URI of the form "api/products?category=*category*" will map to this method.</span></span>

## <a name="creating-a-resource"></a><span data-ttu-id="e38c1-245">리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="e38c1-245">Creating a Resource</span></span>

<span data-ttu-id="e38c1-246">메서드를 추가 하겠습니다 다음으로 `ProductsController` 새 제품을 만드는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-246">Next, we'll add a method to the `ProductsController` class to create a new product.</span></span> <span data-ttu-id="e38c1-247">메서드의 간단한 구현을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-247">Here is a simple implementation of the method:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample9.cs)]

<span data-ttu-id="e38c1-248">이 메서드에 대 한 두 참고 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-248">Note two things about this method:</span></span>

- <span data-ttu-id="e38c1-249">메서드 이름으로 시작 &quot;게시물 중... &quot;.</span><span class="sxs-lookup"><span data-stu-id="e38c1-249">The method name starts with &quot;Post...&quot;.</span></span> <span data-ttu-id="e38c1-250">클라이언트는 새 제품을 만들려면 HTTP POST 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-250">To create a new product, the client sends an HTTP POST request.</span></span>
- <span data-ttu-id="e38c1-251">메서드는 제품 형식의 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-251">The method takes a parameter of type Product.</span></span> <span data-ttu-id="e38c1-252">Web API에서 복합 형식으로 매개 변수는 요청 본문에서 deserialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-252">In Web API, parameters with complex types are deserialized from the request body.</span></span> <span data-ttu-id="e38c1-253">따라서 클라이언트를 product 개체의 직렬화 된 표현 XML 또는 JSON 형식으로 보낼 것으로 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-253">Therefore, we expect the client to send a serialized representation of a product object, in either XML or JSON format.</span></span>

<span data-ttu-id="e38c1-254">이 구현은 작동 하지만, 매우 완료 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-254">This implementation will work, but it is not quite complete.</span></span> <span data-ttu-id="e38c1-255">이상적으로 다음을 포함 하도록 HTTP 응답을 싶습니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-255">Ideally, we would like the HTTP response to include the following:</span></span>

- <span data-ttu-id="e38c1-256">**응답 코드가:** 응답 상태 코드 200 (정상)를 Web API 프레임 워크 기본적으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-256">**Response code:** By default, the Web API framework sets the response status code to 200 (OK).</span></span> <span data-ttu-id="e38c1-257">하지만 HTTP/1.1 프로토콜에 따라 POST 요청 리소스를 만들 때 발생 하는 경우 서버 응답 해야 상태의 201 (만들어짐).</span><span class="sxs-lookup"><span data-stu-id="e38c1-257">But according to the HTTP/1.1 protocol, when a POST request results in the creation of a resource, the server should reply with status 201 (Created).</span></span>
- <span data-ttu-id="e38c1-258">**위치:** 응답의 Location 헤더의 새 리소스의 URI는 리소스를 만들 때 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-258">**Location:** When the server creates a resource, it should include the URI of the new resource in the Location header of the response.</span></span>

<span data-ttu-id="e38c1-259">ASP.NET Web API를 사용 하면 쉽게 HTTP 응답 메시지를 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-259">ASP.NET Web API makes it easy to manipulate the HTTP response message.</span></span> <span data-ttu-id="e38c1-260">다음은 향상 된 구현이입니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-260">Here is the improved implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample10.cs)]

<span data-ttu-id="e38c1-261">메서드 반환 형식은 이제 **HttpResponseMessage**합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-261">Notice that the method return type is now **HttpResponseMessage**.</span></span> <span data-ttu-id="e38c1-262">반환 하 여 프로그램 **HttpResponseMessage** 제품을 대신 상태 코드 및 Location 헤더를 포함 하 여 HTTP 응답 메시지의 세부 정보를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-262">By returning an **HttpResponseMessage** instead of a Product, we can control the details of the HTTP response message, including the status code and the Location header.</span></span>

<span data-ttu-id="e38c1-263">**CreateResponse** 메서드 만듭니다는 **HttpResponseMessage** 하 고 자동으로 본문에는 Product 개체의 직렬화 된 표현을 기록 fo 응답 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-263">The **CreateResponse** method creates an **HttpResponseMessage** and automatically writes a serialized representation of the Product object into the body fo the response message.</span></span>

> [!NOTE]
> <span data-ttu-id="e38c1-264">이 예에서는 유효성을 검사 하지 않습니다는 `Product`합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-264">This example does not validate the `Product`.</span></span> <span data-ttu-id="e38c1-265">모델 유효성 검사에 대 한 정보를 참조 하십시오. [ASP.NET Web API에서 모델 유효성 검사](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-265">For information about model validation, see [Model Validation in ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span></span>


## <a name="updating-a-resource"></a><span data-ttu-id="e38c1-266">리소스를 업데이트 하면</span><span class="sxs-lookup"><span data-stu-id="e38c1-266">Updating a Resource</span></span>

<span data-ttu-id="e38c1-267">Put 제품 업데이트는 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-267">Updating a product with PUT is straightforward:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample11.cs)]

<span data-ttu-id="e38c1-268">메서드 이름으로 시작 &quot;저장 중... &quot;이므로 PUT 요청을 웹 API와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-268">The method name starts with &quot;Put...&quot;, so Web API matches it to PUT requests.</span></span> <span data-ttu-id="e38c1-269">메서드는 두 개의 매개 변수, 제품 ID 및 업데이트 된 제품을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-269">The method takes two parameters, the product ID and the updated product.</span></span> <span data-ttu-id="e38c1-270">*id* 매개 변수는 URI 경로에서 가져온 것 및 *제품* 매개 변수는 요청 본문에서 deserialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-270">The *id* parameter is taken from the URI path, and the *product* parameter is deserialized from the request body.</span></span> <span data-ttu-id="e38c1-271">기본적으로 ASP.NET Web API 프레임 워크는 경로에서 단순 매개 변수 형식 및 요청 본문에서 복합 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-271">By default, the ASP.NET Web API framework takes simple parameter types from the route and complex types from the request body.</span></span>

## <a name="deleting-a-resource"></a><span data-ttu-id="e38c1-272">리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-272">Deleting a Resource</span></span>

<span data-ttu-id="e38c1-273">resourse를 삭제 하려면 "삭제..." 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e38c1-273">To delete a resourse, define a "Delete..." method.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample12.cs)]

<span data-ttu-id="e38c1-274">상태를 설명 하는 엔터티 본문이 있는 200 (정상) 상태를 반환할 수 삭제 요청에 성공 하면 상태 202 (수락) 삭제는 여전히 보류 중입니다. 또는 상태 엔터티 본문이 204 (콘텐츠 없음).</span><span class="sxs-lookup"><span data-stu-id="e38c1-274">If a DELETE request succeeds, it can return status 200 (OK) with an entity-body that describes the status; status 202 (Accepted) if the deletion is still pending; or status 204 (No Content) with no entity body.</span></span> <span data-ttu-id="e38c1-275">이 경우에 `DeleteProduct` 메서드에 `void` 반환 형식, 하므로 ASP.NET Web API 자동으로로 변환 상태 코드 204 (콘텐츠 없음).</span><span class="sxs-lookup"><span data-stu-id="e38c1-275">In this case, the `DeleteProduct` method has a `void` return type, so ASP.NET Web API automatically translates this into status code 204 (No Content).</span></span>
