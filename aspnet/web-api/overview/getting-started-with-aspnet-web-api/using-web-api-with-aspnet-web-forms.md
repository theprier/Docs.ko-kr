---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: "Web API를 사용 하 여 ASP.NET Web forms | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/03/2012
ms.topic: article
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: af918671a8bcc97a0050ea033ccd14dd96416e73
ms.sourcegitcommit: 037d3900f739dbaa2ba14158e3d7dc81478952ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2017
---
<a name="using-web-api-with-aspnet-web-forms"></a><span data-ttu-id="ba605-102">Web API를 사용 하 여 ASP.NET Web forms</span><span class="sxs-lookup"><span data-stu-id="ba605-102">Using Web API with ASP.NET Web Forms</span></span>
====================
<span data-ttu-id="ba605-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ba605-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="ba605-104">ASP.NET Web API는 ASP.NET MVC와 함께 패키지 되어, 하지만 기존 ASP.NET Web Forms 응용 프로그램에 Web API를 추가 하려면 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-104">Although ASP.NET Web API is packaged with ASP.NET MVC, it is easy to add Web API to a traditional ASP.NET Web Forms application.</span></span> <span data-ttu-id="ba605-105">이 자습서의 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-105">This tutorial walks you through the steps.</span></span>

## <a name="overview"></a><span data-ttu-id="ba605-106">개요</span><span class="sxs-lookup"><span data-stu-id="ba605-106">Overview</span></span>

<span data-ttu-id="ba605-107">Web Forms 응용 프로그램을 웹 API를 사용 하려면 두 가지 주요 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-107">To use Web API in a Web Forms application, there are two main steps:</span></span>

- <span data-ttu-id="ba605-108">파생 된 웹 API 컨트롤러 추가 **ApiController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-108">Add a Web API controller that derives from the **ApiController** class.</span></span>
- <span data-ttu-id="ba605-109">경로 테이블을 추가 하는 **응용 프로그램\_시작** 메서드.</span><span class="sxs-lookup"><span data-stu-id="ba605-109">Add a route table to the **Application\_Start** method.</span></span>

## <a name="create-a-web-forms-project"></a><span data-ttu-id="ba605-110">Web Forms 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="ba605-110">Create a Web Forms Project</span></span>

<span data-ttu-id="ba605-111">Visual Studio를 시작 하 고 선택 **새 프로젝트** 에서 **시작** 페이지.</span><span class="sxs-lookup"><span data-stu-id="ba605-111">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="ba605-112">또는에서 **파일** 메뉴 선택 **새로** 차례로 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-112">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="ba605-113">에 **템플릿** 창 선택 **설치 된 템플릿** 확장는 **Visual C#** 노드.</span><span class="sxs-lookup"><span data-stu-id="ba605-113">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="ba605-114">아래 **Visual C#**선택, **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-114">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="ba605-115">프로젝트 템플릿 목록에서 선택 **ASP.NET Web Forms 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-115">In the list of project templates, select **ASP.NET Web Forms Application**.</span></span> <span data-ttu-id="ba605-116">프로젝트에 대 한 이름을 입력 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-116">Enter a name for the project and click **OK**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="ba605-117">모델과 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="ba605-117">Create the Model and Controller</span></span>

<span data-ttu-id="ba605-118">이 자습서로 동일한 모델 및 컨트롤러 클래스를 사용 하 여 [시작](tutorial-your-first-web-api.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-118">This tutorial uses the same model and controller classes as the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="ba605-119">먼저, 모델 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-119">First, add a model class.</span></span> <span data-ttu-id="ba605-120">**솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **클래스 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-120">In **Solution Explorer**, right-click the project and select **Add Class**.</span></span> <span data-ttu-id="ba605-121">제품 클래스 이름을 지정 하 고 다음 구현을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-121">Name the class Product, and add the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

<span data-ttu-id="ba605-122">다음으로 프로젝트에, A Web API 컨트롤러 추가 *컨트롤러* 웹 API에 대 한 HTTP 요청을 처리 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-122">Next, add a Web API controller to the project., A *controller* is the object that handles HTTP requests for Web API.</span></span>

<span data-ttu-id="ba605-123">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-123">In **Solution Explorer**, right-click the project.</span></span> <span data-ttu-id="ba605-124">선택 **새 항목 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-124">Select **Add New Item**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

<span data-ttu-id="ba605-125">아래 **설치 된 템플릿**를 확장 하 고 **Visual C#** 선택 **웹**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-125">Under **Installed Templates**, expand **Visual C#** and select **Web**.</span></span> <span data-ttu-id="ba605-126">다음 템플릿 목록에서 선택 **Web API 컨트롤러 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-126">Then, from the list of templates, select **Web API Controller Class**.</span></span> <span data-ttu-id="ba605-127">"ProductsController" 컨트롤러 이름을 지정 하 고 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-127">Name the controller "ProductsController" and click **Add**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

<span data-ttu-id="ba605-128">**새 항목 추가** 마법사 ProductsController.cs 라는 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-128">The **Add New Item** wizard will create a file named ProductsController.cs.</span></span> <span data-ttu-id="ba605-129">마법사를 포함 하는 메서드를 삭제 하 고 다음 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-129">Delete the methods that the wizard included and add the following methods:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

<span data-ttu-id="ba605-130">이 컨트롤러에 코드에 대 한 자세한 내용은 참조는 [시작](tutorial-your-first-web-api.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-130">For more information about the code in this controller, see the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

## <a name="add-routing-information"></a><span data-ttu-id="ba605-131">라우팅 정보를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-131">Add Routing Information</span></span>

<span data-ttu-id="ba605-132">다음으로 추가 URI 경로 이므로 형식의 해당 Uri &quot;/api/제품/&quot; 컨트롤러에 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-132">Next, we'll add a URI route so that URIs of the form &quot;/api/products/&quot; are routed to the controller.</span></span>

<span data-ttu-id="ba605-133">**솔루션 탐색기**, Global.asax Global.asax.cs 코드 숨김 파일을 열 수를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-133">In **Solution Explorer**, double-click Global.asax to open the code-behind file Global.asax.cs.</span></span> <span data-ttu-id="ba605-134">다음 추가 **를 사용 하 여** 문.</span><span class="sxs-lookup"><span data-stu-id="ba605-134">Add the following **using** statement.</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

<span data-ttu-id="ba605-135">다음 코드를 다음 추가 **응용 프로그램\_시작** 메서드:</span><span class="sxs-lookup"><span data-stu-id="ba605-135">Then add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

<span data-ttu-id="ba605-136">라우팅 테이블에 대 한 자세한 내용은 참조 [ASP.NET Web API에서 라우팅](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-136">For more information about routing tables, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="add-client-side-ajax"></a><span data-ttu-id="ba605-137">클라이언트 쪽 AJAX를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-137">Add Client-Side AJAX</span></span>

<span data-ttu-id="ba605-138">웹 클라이언트가 액세스할 수 있는 API를 만드는 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-138">That's all you need to create a web API that clients can access.</span></span> <span data-ttu-id="ba605-139">이제 jQuery를 사용 하 여 API를 호출 하는 HTML 페이지를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-139">Now let's add an HTML page that uses jQuery to call the API.</span></span>

<span data-ttu-id="ba605-140">마스터 페이지에 있는지 확인 (예를 들어 *Site.Master*)를 포함 한 `ContentPlaceHolder` 와 `ID="HeadContent"`:</span><span class="sxs-lookup"><span data-stu-id="ba605-140">Make sure your master page (for example, *Site.Master*) includes a `ContentPlaceHolder` with `ID="HeadContent"`:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

<span data-ttu-id="ba605-141">Default.aspx 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-141">Open the file Default.aspx.</span></span> <span data-ttu-id="ba605-142">표시 된 것 처럼 주 콘텐츠 섹션에 있는 상용구 텍스트를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-142">Replace the boilerplate text that is in the main content section, as shown:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

<span data-ttu-id="ba605-143">다음으로에서 jQuery 소스 파일에 대 한 참조를 추가 `HeaderContent` 섹션:</span><span class="sxs-lookup"><span data-stu-id="ba605-143">Next, add a reference to the jQuery source file in the `HeaderContent` section:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

<span data-ttu-id="ba605-144">참고: 쉽게 추가할 수 있습니다 스크립트 참조에서 파일을 끌어다 **솔루션 탐색기** 코드 편집기 창에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-144">Note: You can easily add the script reference by dragging and dropping the file from **Solution Explorer** into the code editor window.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

<span data-ttu-id="ba605-145">JQuery 스크립트 태그 아래 다음과 같은 스크립트 블록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-145">Below the jQuery script tag, add the following script block:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

<span data-ttu-id="ba605-146">이 스크립트는 AJAX 요청을 사용 하면 문서 로드 될 때 &quot;api/제품&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-146">When the document loads, this script makes an AJAX request to &quot;api/products&quot;.</span></span> <span data-ttu-id="ba605-147">요청이는 JSON 형식으로 제품 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-147">The request returns a list of products in JSON format.</span></span> <span data-ttu-id="ba605-148">스크립트는 HTML 테이블에는 제품 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-148">The script adds the product information to the HTML table.</span></span>

<span data-ttu-id="ba605-149">응용 프로그램을 실행 하면 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba605-149">When you run the application, it should look like this:</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
