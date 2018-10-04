---
uid: web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
title: ASP.NET Web API 2 (C#)를 사용 하 여 시작
author: MikeWasson
description: HTTP를 단순히 웹 페이지를 제공 합니다. 서비스 및 데이터를 노출 하는 Api를 빌드하기 위한 강력한 플랫폼 이기도 합니다. HTTP에는 단순 하 고 유연 하 고 ubiq는 중...
ms.author: riande
ms.date: 11/28/2017
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
msc.type: authoredcontent
ms.openlocfilehash: 62e99a41ba935470c39476c9aea8ee4193543425
ms.sourcegitcommit: 7890dfb5a8f8c07d813f166d3ab0c263f893d0c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48795295"
---
<a name="get-started-with-aspnet-web-api-2-c"></a><span data-ttu-id="2df0e-105">ASP.NET Web API 2 (C#)를 사용 하 여 시작</span><span class="sxs-lookup"><span data-stu-id="2df0e-105">Get Started with ASP.NET Web API 2 (C#)</span></span>
====================
<span data-ttu-id="2df0e-106">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2df0e-106">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="2df0e-107">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="2df0e-107">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Sample-code-of-Getting-c56ccb28)

<span data-ttu-id="2df0e-108">HTTP를 단순히 웹 페이지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-108">HTTP is not just for serving up web pages.</span></span> <span data-ttu-id="2df0e-109">HTTP은 서비스 및 데이터를 노출 하는 Api를 빌드하기 위한 강력한 플랫폼 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-109">HTTP is also a powerful platform for building APIs that expose services and data.</span></span> <span data-ttu-id="2df0e-110">HTTP는 간단 하 고 유연 하며 유비쿼터스는입니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-110">HTTP is simple, flexible, and ubiquitous.</span></span> <span data-ttu-id="2df0e-111">생각할 수 있는 거의 모든 플랫폼에서 HTTP 라이브러리도 있으므로 HTTP 서비스는 광범위 한 브라우저, 모바일 장치 및 기존 데스크톱 응용 프로그램 등의 클라이언트를 확보할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-111">Almost any platform that you can think of has an HTTP library, so HTTP services can reach a broad range of clients, including browsers, mobile devices, and traditional desktop applications.</span></span>

<span data-ttu-id="2df0e-112">ASP.NET Web API는 web Api는.NET Framework를 빌드하기 위한 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-112">ASP.NET Web API is a framework for building web APIs on top of the .NET Framework.</span></span> <span data-ttu-id="2df0e-113">이 자습서에서는 제품의 목록을 반환 하는 web API를 만들려면 ASP.NET Web API를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-113">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span>

## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="2df0e-114">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="2df0e-114">Software versions used in the tutorial</span></span>

- [<span data-ttu-id="2df0e-115">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="2df0e-115">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
- <span data-ttu-id="2df0e-116">Web API 2</span><span class="sxs-lookup"><span data-stu-id="2df0e-116">Web API 2</span></span>

<span data-ttu-id="2df0e-117">참조 [ASP.NET Core 및 Windows에 대 한 Visual Studio를 사용 하 여 web API 만들기](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) 이 자습서의 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-117">See [Create a web API with ASP.NET Core and Visual Studio for Windows](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) for a newer version of this tutorial.</span></span>

## <a name="create-a-web-api-project"></a><span data-ttu-id="2df0e-118">웹 API 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="2df0e-118">Create a Web API Project</span></span>

<span data-ttu-id="2df0e-119">이 자습서에서는 제품의 목록을 반환 하는 web API를 만들려면 ASP.NET Web API를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-119">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span> <span data-ttu-id="2df0e-120">프런트 엔드 웹 페이지 결과 표시 하려면 jQuery를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-120">The front-end web page uses jQuery to display the results.</span></span>

![](tutorial-your-first-web-api/_static/image1.png)

<span data-ttu-id="2df0e-121">Visual Studio를 시작 하 고 선택 **새 프로젝트** 에서 합니다 **시작** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-121">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="2df0e-122">또는에서 **파일** 메뉴에서 **새로 만들기** 차례로 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-122">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="2df0e-123">에 **템플릿** 창 **설치 된 템플릿** 확장 하 고는 **Visual C#** 노드.</span><span class="sxs-lookup"><span data-stu-id="2df0e-123">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="2df0e-124">아래 **Visual C#** 를 선택 **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-124">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="2df0e-125">프로젝트 템플릿 목록에서 선택 **ASP.NET 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-125">In the list of project templates, select **ASP.NET Web Application**.</span></span> <span data-ttu-id="2df0e-126">"ProductsApp" 프로젝트 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-126">Name the project "ProductsApp" and click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image2.png)

<span data-ttu-id="2df0e-127">에 **새 ASP.NET 프로젝트** 대화 상자에서 선택 합니다 **빈** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="2df0e-127">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="2df0e-128">아래 &quot;폴더를 추가 하 고에 대 한 참조를 핵심&quot;, 확인 **Web API**합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-128">Under &quot;Add folders and core references for&quot;, check **Web API**.</span></span> <span data-ttu-id="2df0e-129">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-129">Click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="2df0e-130">사용 하 여 Web API 프로젝트를 만들 수도 있습니다는 &quot;Web API&quot; 템플릿.</span><span class="sxs-lookup"><span data-stu-id="2df0e-130">You can also create a Web API project using the &quot;Web API&quot; template.</span></span> <span data-ttu-id="2df0e-131">Web API 템플릿에서 ASP.NET MVC를 사용 하 여 API 도움말 페이지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-131">The Web API template uses ASP.NET MVC to provide API help pages.</span></span> <span data-ttu-id="2df0e-132">MVC 사용 하지 않고 웹 API를 표시 하려고 하기 때문에 빈 템플릿에이 자습서에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-132">I'm using the Empty template for this tutorial because I want to show Web API without MVC.</span></span> <span data-ttu-id="2df0e-133">일반적으로 ASP.NET MVC로 웹 API를 사용 하 여 알 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-133">In general, you don't need to know ASP.NET MVC to use Web API.</span></span>


## <a name="adding-a-model"></a><span data-ttu-id="2df0e-134">모델 추가</span><span class="sxs-lookup"><span data-stu-id="2df0e-134">Adding a Model</span></span>

<span data-ttu-id="2df0e-135">*모델*은 응용 프로그램에서 데이터를 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-135">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="2df0e-136">ASP.NET Web API는 자동으로 JSON, XML 또는 다른 형식으로 모델을 직렬화 하 고 HTTP 응답 메시지의 본문으로 serialize 된 데이터를 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-136">ASP.NET Web API can automatically serialize your model to JSON, XML, or some other format, and then write the serialized data into the body of the HTTP response message.</span></span> <span data-ttu-id="2df0e-137">클라이언트는 serialization 형식을 읽을 수 있습니다,으로 개체를 deserialize 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-137">As long as a client can read the serialization format, it can deserialize the object.</span></span> <span data-ttu-id="2df0e-138">대부분의 클라이언트에는 XML 또는 JSON 구문 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-138">Most clients can parse either XML or JSON.</span></span> <span data-ttu-id="2df0e-139">또한 클라이언트는 HTTP 요청 메시지의 Accept 헤더를 설정 하 여 하려고 하는 형식을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-139">Moreover, the client can indicate which format it wants by setting the Accept header in the HTTP request message.</span></span>

<span data-ttu-id="2df0e-140">제품을 나타내는 간단한 모델을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-140">Let's start by creating a simple model that represents a product.</span></span>

<span data-ttu-id="2df0e-141">솔루션 탐색기 표시 되지 않으면 클릭 합니다 **뷰** 선택한 메뉴 **솔루션 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-141">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="2df0e-142">솔루션 탐색기에서 Models 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-142">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="2df0e-143">상황에 맞는 메뉴에서 선택 **추가** 선택한 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-143">From the context menu, select **Add** then select **Class**.</span></span>

![](tutorial-your-first-web-api/_static/image4.png)

<span data-ttu-id="2df0e-144">클래스의 이름을 &quot;제품&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-144">Name the class &quot;Product&quot;.</span></span> <span data-ttu-id="2df0e-145">다음 속성을 추가 합니다 `Product` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-145">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample1.cs)]

## <a name="adding-a-controller"></a><span data-ttu-id="2df0e-146">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="2df0e-146">Adding a Controller</span></span>

<span data-ttu-id="2df0e-147">Web API에는 *컨트롤러* 는 HTTP 요청을 처리 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-147">In Web API, a *controller* is an object that handles HTTP requests.</span></span> <span data-ttu-id="2df0e-148">Id로 지정 된 단일 제품 또는 제품의 목록을 반환할 수 있는 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="2df0e-148">We'll add a controller that can return either a list of products or a single product specified by ID.</span></span>

> [!NOTE]
> <span data-ttu-id="2df0e-149">ASP.NET MVC를 사용한 경우 이미 잘 알고 있다면 컨트롤러를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-149">If you have used ASP.NET MVC, you are already familiar with controllers.</span></span> <span data-ttu-id="2df0e-150">Web API 컨트롤러는 MVC 컨트롤러 유사 하지만 상속 된 **ApiController** 클래스 대신 합니다 **컨트롤러** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-150">Web API controllers are similar to MVC controllers, but inherit the **ApiController** class instead of the **Controller** class.</span></span>

<span data-ttu-id="2df0e-151">**솔루션 탐색기**, Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-151">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="2df0e-152">선택 **추가** 선택한 후 **컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-152">Select **Add** and then select **Controller**.</span></span>

![](tutorial-your-first-web-api/_static/image5.png)

<span data-ttu-id="2df0e-153">에 **스 캐 폴드 추가** 대화 상자에서 **Web API 컨트롤러-비어 있음**합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-153">In the **Add Scaffold** dialog, select **Web API Controller - Empty**.</span></span> <span data-ttu-id="2df0e-154">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-154">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image6.png)

<span data-ttu-id="2df0e-155">에 **컨트롤러 추가** 대화 상자에서 컨트롤러 이름 &quot;ProductsController&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-155">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="2df0e-156">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-156">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image7.png)

<span data-ttu-id="2df0e-157">스 캐 폴딩을 ProductsController.cs Controllers 폴더에서 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-157">The scaffolding creates a file named ProductsController.cs in the Controllers folder.</span></span>

![](tutorial-your-first-web-api/_static/image8.png)

> [!NOTE]
> <span data-ttu-id="2df0e-158">컨트롤러 라는 폴더에는 컨트롤러 넣이 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-158">You don't need to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="2df0e-159">폴더 이름은 원본 파일을 구성 하는 편리한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-159">The folder name is just a convenient way to organize your source files.</span></span>


<span data-ttu-id="2df0e-160">이 파일이 열려 있지 않으면 이미를 열려는 파일을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-160">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="2df0e-161">이 파일의 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-161">Replace the code in this file with the following:</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample2.cs)]

<span data-ttu-id="2df0e-162">예제를 단순하게 유지 하기 제품 고정 된 배열을 컨트롤러 클래스 내에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-162">To keep the example simple, products are stored in a fixed array inside the controller class.</span></span> <span data-ttu-id="2df0e-163">물론 실제 응용 프로그램에서 데이터베이스 쿼리 하거나를 일부 기타 외부 데이터 원본을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-163">Of course, in a real application, you would query a database or use some other external data source.</span></span>

<span data-ttu-id="2df0e-164">제품을 반환 하는 두 메서드를 정의 하는 컨트롤러:</span><span class="sxs-lookup"><span data-stu-id="2df0e-164">The controller defines two methods that return products:</span></span>

- <span data-ttu-id="2df0e-165">합니다 `GetAllProducts` 제품의 전체 목록을 반환는 **IEnumerable&lt;제품&gt;**  형식입니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-165">The `GetAllProducts` method returns the entire list of products as an **IEnumerable&lt;Product&gt;** type.</span></span>
- <span data-ttu-id="2df0e-166">`GetProduct` 메서드를 해당 ID로 단일 제품 조회</span><span class="sxs-lookup"><span data-stu-id="2df0e-166">The `GetProduct` method looks up a single product by its ID.</span></span>

<span data-ttu-id="2df0e-167">정말 간단하죠.</span><span class="sxs-lookup"><span data-stu-id="2df0e-167">That's it!</span></span> <span data-ttu-id="2df0e-168">Web API 작업 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-168">You have a working web API.</span></span> <span data-ttu-id="2df0e-169">컨트롤러에서 각 메서드는 하나 이상의 Uri에 해당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-169">Each method on the controller corresponds to one or more URIs:</span></span>

| <span data-ttu-id="2df0e-170">컨트롤러 메서드</span><span class="sxs-lookup"><span data-stu-id="2df0e-170">Controller Method</span></span> | <span data-ttu-id="2df0e-171">URI</span><span class="sxs-lookup"><span data-stu-id="2df0e-171">URI</span></span> |
| --- | --- |
| <span data-ttu-id="2df0e-172">GetAllProducts</span><span class="sxs-lookup"><span data-stu-id="2df0e-172">GetAllProducts</span></span> | <span data-ttu-id="2df0e-173">api 제품</span><span class="sxs-lookup"><span data-stu-id="2df0e-173">/api/products</span></span> |
| <span data-ttu-id="2df0e-174">GetProduct</span><span class="sxs-lookup"><span data-stu-id="2df0e-174">GetProduct</span></span> | <span data-ttu-id="2df0e-175">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="2df0e-175">/api/products/*id*</span></span> |

<span data-ttu-id="2df0e-176">에 대 한 합니다 `GetProduct` 메서드를 *id* URI에는 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-176">For the `GetProduct` method, the *id* in the URI is a placeholder.</span></span> <span data-ttu-id="2df0e-177">예를 들어, ID가 5 인 제품을 얻으려면 URI는 `api/products/5`합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-177">For example, to get the product with ID of 5, the URI is `api/products/5`.</span></span>

<span data-ttu-id="2df0e-178">Web API 컨트롤러 메서드를 HTTP 요청을 라우팅하 하는 방법에 대 한 자세한 내용은 참조 하세요. [ASP.NET Web API에서 라우팅](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-178">For more information about how Web API routes HTTP requests to controller methods, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="calling-the-web-api-with-javascript-and-jquery"></a><span data-ttu-id="2df0e-179">Javascript와 jQuery를 사용한 Web API를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-179">Calling the Web API with Javascript and jQuery</span></span>

<span data-ttu-id="2df0e-180">이 섹션에서는 AJAX를 사용 하 여 web API를 호출 하는 HTML 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-180">In this section, we'll add an HTML page that uses AJAX to call the web API.</span></span> <span data-ttu-id="2df0e-181">AJAX 호출을 수행 하 고 결과 사용 하 여 페이지를 업데이트 하려면 jQuery를 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-181">We'll use jQuery to make the AJAX calls and also to update the page with the results.</span></span>

<span data-ttu-id="2df0e-182">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가**을 선택한 후 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-182">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span>

![](tutorial-your-first-web-api/_static/image9.png)

<span data-ttu-id="2df0e-183">에 **새 항목 추가** 대화 상자에서를 **웹** 노드에서 **Visual C#** 를 선택한 후는 **HTML 페이지** 항목.</span><span class="sxs-lookup"><span data-stu-id="2df0e-183">In the **Add New Item** dialog, select the **Web** node under **Visual C#**, and then select the **HTML Page** item.</span></span> <span data-ttu-id="2df0e-184">페이지의 이름을 &quot;index.html&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-184">Name the page &quot;index.html&quot;.</span></span>

![](tutorial-your-first-web-api/_static/image10.png)

<span data-ttu-id="2df0e-185">다음을 사용 하 여이 파일의 모든 항목을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-185">Replace everything in this file with the following:</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample3.html)]

<span data-ttu-id="2df0e-186">여러 가지 방법으로 jQuery를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-186">There are several ways to get jQuery.</span></span> <span data-ttu-id="2df0e-187">이 예에서 사용 된 [Microsoft Ajax CDN](../../../ajax/cdn/overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-187">In this example, I used the [Microsoft Ajax CDN](../../../ajax/cdn/overview.md).</span></span> <span data-ttu-id="2df0e-188">다운로드할 수도 있습니다 [ http://jquery.com/ ](http://jquery.com/), 및 "웹 API" ASP.NET 프로젝트 템플릿에 jQuery도 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-188">You can also download it from [http://jquery.com/](http://jquery.com/), and the ASP.NET "Web API" project template includes jQuery as well.</span></span>

### <a name="getting-a-list-of-products"></a><span data-ttu-id="2df0e-189">제품의 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="2df0e-189">Getting a List of Products</span></span>

<span data-ttu-id="2df0e-190">제품 목록을 가져오려고로 HTTP GET 요청을 보낼 &quot;/api/제품&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-190">To get a list of products, send an HTTP GET request to &quot;/api/products&quot;.</span></span>

<span data-ttu-id="2df0e-191">JQuery [getJSON](http://api.jquery.com/jQuery.getJSON/) 함수 AJAX 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-191">The jQuery [getJSON](http://api.jquery.com/jQuery.getJSON/) function sends an AJAX request.</span></span> <span data-ttu-id="2df0e-192">응답에 대 한 JSON 개체 배열을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-192">For response contains array of JSON objects.</span></span> <span data-ttu-id="2df0e-193">`done` 함수 요청이 성공 하는 경우 호출 되는 콜백을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-193">The `done` function specifies a callback that is called if the request succeeds.</span></span> <span data-ttu-id="2df0e-194">콜백 DOM 제품 정보를 사용 하 여 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-194">In the callback, we update the DOM with the product information.</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample4.html)]

### <a name="getting-a-product-by-id"></a><span data-ttu-id="2df0e-195">제품 ID 별로 가져오기</span><span class="sxs-lookup"><span data-stu-id="2df0e-195">Getting a Product By ID</span></span>

<span data-ttu-id="2df0e-196">제품 ID 가져오려면로 HTTP GET 요청을 보낼 &quot;/a p i/제품/*id*&quot;여기서 *id* 제품 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-196">To get a product by ID, send an HTTP GET request to &quot;/api/products/*id*&quot;, where *id* is the product ID.</span></span>

[!code-javascript[Main](tutorial-your-first-web-api/samples/sample5.js)]

<span data-ttu-id="2df0e-197">여전히 호출 `getJSON` AJAX 요청이 이번에 보낼 요청 URI에서에서 ID를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-197">We still call `getJSON` to send the AJAX request, but this time we put the ID in the request URI.</span></span> <span data-ttu-id="2df0e-198">이 요청의 응답에는 단일 제품의 JSON 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-198">The response from this request is a JSON representation of a single product.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="2df0e-199">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="2df0e-199">Running the Application</span></span>

<span data-ttu-id="2df0e-200">F5 키를 눌러 응용 프로그램 디버깅을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-200">Press F5 to start debugging the application.</span></span> <span data-ttu-id="2df0e-201">웹 페이지는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-201">The web page should look like the following:</span></span>

![](tutorial-your-first-web-api/_static/image11.png)

<span data-ttu-id="2df0e-202">제품 ID 별로 가져오기 ID를 입력 하 고 검색을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-202">To get a product by ID, enter the ID and click Search:</span></span>

![](tutorial-your-first-web-api/_static/image12.png)

<span data-ttu-id="2df0e-203">잘못 된 ID를 입력 하면 서버에 HTTP 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-203">If you enter an invalid ID, the server returns an HTTP error:</span></span>

![](tutorial-your-first-web-api/_static/image13.png)

## <a name="using-f12-to-view-the-http-request-and-response"></a><span data-ttu-id="2df0e-204">F12 키를 사용 하 여 HTTP 요청 및 응답을 보려면</span><span class="sxs-lookup"><span data-stu-id="2df0e-204">Using F12 to View the HTTP Request and Response</span></span>

<span data-ttu-id="2df0e-205">HTTP 서비스를 사용 하 여 작업 하는 경우 HTTP 요청 및 요청 메시지에 매우 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-205">When you are working with an HTTP service, it can be very useful to see the HTTP request and request messages.</span></span> <span data-ttu-id="2df0e-206">Internet Explorer 9의 F12 개발자 도구를 사용 하 여이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-206">You can do this by using the F12 developer tools in Internet Explorer 9.</span></span> <span data-ttu-id="2df0e-207">Internet Explorer 9에서 누릅니다 **F12** 는 도구를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-207">From Internet Explorer 9, press **F12** to open the tools.</span></span> <span data-ttu-id="2df0e-208">클릭 합니다 **네트워크** 누릅니다 탭 **캡처 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-208">Click the **Network** tab and press **Start Capturing**.</span></span> <span data-ttu-id="2df0e-209">이제 돌아가서 웹 페이지 및 키를 눌러 **F5** 웹 페이지를 다시 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-209">Now go back to the web page and press **F5** to reload the web page.</span></span> <span data-ttu-id="2df0e-210">Internet Explorer는 브라우저와 웹 서버 간에 HTTP 트래픽을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-210">Internet Explorer will capture the HTTP traffic between the browser and the web server.</span></span> <span data-ttu-id="2df0e-211">요약 보기 페이지의 모든 네트워크 트래픽을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-211">The summary view shows all the network traffic for a page:</span></span>

![](tutorial-your-first-web-api/_static/image14.png)

<span data-ttu-id="2df0e-212">상대 URI에 대 한 항목을 찾습니다 "api/제품 /"입니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-212">Locate the entry for the relative URI "api/products/".</span></span> <span data-ttu-id="2df0e-213">이 항목을 선택 하 고 클릭 **자세한 보기로 이동**합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-213">Select this entry and click **Go to detailed view**.</span></span> <span data-ttu-id="2df0e-214">세부 정보 뷰에서 요청 및 응답 헤더 및 본문을 보려면 탭이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-214">In the detail view, there are tabs to view the request and response headers and bodies.</span></span> <span data-ttu-id="2df0e-215">예를 들어를 클릭 하면 합니다 **요청 헤더** 탭에는 클라이언트 요청을 볼 수 있습니다 &quot;application/json&quot; Accept 헤더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-215">For example, if you click the **Request headers** tab, you can see that the client requested &quot;application/json&quot; in the Accept header.</span></span>

![](tutorial-your-first-web-api/_static/image15.png)

<span data-ttu-id="2df0e-216">응답 본문 탭을 클릭 하면 제품 목록을 JSON으로 serialize 된 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-216">If you click the Response body tab, you can see how the product list was serialized to JSON.</span></span> <span data-ttu-id="2df0e-217">다른 브라우저에 비슷한 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-217">Other browsers have similar functionality.</span></span> <span data-ttu-id="2df0e-218">또 다른 유용한 도구는 [Fiddler](http://www.fiddler2.com/fiddler2/), 웹 디버깅 프록시입니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-218">Another useful tool is [Fiddler](http://www.fiddler2.com/fiddler2/), a web debugging proxy.</span></span> <span data-ttu-id="2df0e-219">사용할 수 있습니다 Fiddler HTTP 트래픽의 보려는 및 HTTP 요청을 작성 요청에서 HTTP 헤더에 대 한 모든 권한을 제공 하는.</span><span class="sxs-lookup"><span data-stu-id="2df0e-219">You can use Fiddler to view your HTTP traffic, and also to compose HTTP requests, which gives you full control over the HTTP headers in the request.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="2df0e-220">Azure에서 실행 되는이 앱 참조</span><span class="sxs-lookup"><span data-stu-id="2df0e-220">See this App Running on Azure</span></span>

<span data-ttu-id="2df0e-221">라이브 웹 앱으로 실행 하는 완성 된 사이트를 참조 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="2df0e-221">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="2df0e-222">다음 단추를 클릭 하 여 Azure 계정에 앱의 전체 버전을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-222">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://deploy.azure.com/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebAPI-ProductsApp#/form/setup)

<span data-ttu-id="2df0e-223">이 솔루션을 Azure에 배포 하려면 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-223">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="2df0e-224">계정이 아직 없는 경우 다음 옵션:</span><span class="sxs-lookup"><span data-stu-id="2df0e-224">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="2df0e-225">[Azure 계정을 무료로 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -크레딧을 받게 사용 하면 유료 Azure 서비스를 사용해볼 수 있습니다 하 고 사용한 후에 계정을 유지 하면 최대 사용 하 여 무료 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-225">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="2df0e-226">[MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -MSDN 구독은 크레딧을 매달 제공 유료 Azure 서비스에 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-226">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2df0e-227">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2df0e-227">Next Steps</span></span>

- <span data-ttu-id="2df0e-228">POST, PUT 및 DELETE 작업을 지원 하 고 데이터베이스에 기록 하는 HTTP 서비스의 자세한 예제를 보려면 [Entity Framework 6을 사용 하 여 Web API 2를 사용 하 여](../data/using-web-api-with-entity-framework/part-1.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-228">For a more complete example of an HTTP service that supports POST, PUT, and DELETE actions and writes to a database, see [Using Web API 2 with Entity Framework 6](../data/using-web-api-with-entity-framework/part-1.md).</span></span>
- <span data-ttu-id="2df0e-229">HTTP 서비스를 기반으로 유동성 및 응답성이 뛰어난 웹 응용 프로그램 만들기에 대 한 자세한 내용은 참조 하십시오 [ASP.NET 단일 페이지 응용 프로그램](../../../single-page-application/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-229">For more about creating fluid and responsive web applications on top of an HTTP service, see [ASP.NET Single Page Application](../../../single-page-application/index.md).</span></span>
- <span data-ttu-id="2df0e-230">Azure App Service에 Visual Studio 웹 프로젝트를 배포 하는 방법에 대 한 정보를 참조 하세요 [Azure App Service에서 ASP.NET 웹 앱 만들기](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2df0e-230">For information about how to deploy a Visual Studio web project to Azure App Service, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>
