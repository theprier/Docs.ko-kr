---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: "ASP.NET MVC 실행 프로세스를 이해 | Microsoft Docs"
author: microsoft
description: "ASP.NET MVC 프레임 워크에서 단계별 브라우저 요청을 처리 하는 방법에 대해 알아봅니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 5837c6e49709d6b86ee52cd88ffd4759c1850544
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="understanding-the-aspnet-mvc-execution-process"></a><span data-ttu-id="eb469-103">ASP.NET MVC 실행 프로세스 이해</span><span class="sxs-lookup"><span data-stu-id="eb469-103">Understanding the ASP.NET MVC Execution Process</span></span>
====================
<span data-ttu-id="eb469-104">여 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="eb469-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="eb469-105">ASP.NET MVC 프레임 워크에서 단계별 브라우저 요청을 처리 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-105">Learn how the ASP.NET MVC framework processes a browser request step-by-step.</span></span>


<span data-ttu-id="eb469-106">ASP.NET MVC 기반 웹 응용 프로그램 요청을 통과 하는 **UrlRoutingModule** 개체 HTTP 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-106">Requests to an ASP.NET MVC-based Web application first pass through the **UrlRoutingModule** object, which is an HTTP module.</span></span> <span data-ttu-id="eb469-107">이 모듈에서 요청을 구문 분석 하 고 경로 선택을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-107">This module parses the request and performs route selection.</span></span> <span data-ttu-id="eb469-108">**UrlRoutingModule** 개체가 현재 요청과 일치 하는 첫 번째 경로 개체를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-108">The **UrlRoutingModule** object selects the first route object that matches the current request.</span></span> <span data-ttu-id="eb469-109">(경로 개체를 구현 하는 클래스는 **RouteBase**, 이며 일반적으로의 인스턴스는 **경로** 클래스입니다.) 일치 하는 경로가 없을 경우는 **UrlRoutingModule** 개체 작업이 없으며 요청이 처리 다시 일반 ASP.NET 또는 IIS 요청을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-109">(A route object is a class that implements **RouteBase**, and is typically an instance of the **Route** class.) If no routes match, the **UrlRoutingModule** object does nothing and lets the request fall back to the regular ASP.NET or IIS request processing.</span></span>

<span data-ttu-id="eb469-110">선택한 **경로** 개체는 **UrlRoutingModule** 개체를 가져옵니다는 **IRouteHandler** 연결 된 개체에는 **경로**개체입니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-110">From the selected **Route** object, the **UrlRoutingModule** object obtains the **IRouteHandler** object that is associated with the **Route** object.</span></span> <span data-ttu-id="eb469-111">일반적으로 MVC 응용 프로그램에서이 프로그램의 인스턴스가 될 **MvcRouteHandler**합니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-111">Typically, in an MVC application, this will be an instance of **MvcRouteHandler**.</span></span> <span data-ttu-id="eb469-112">**IRouteHandler** 인스턴스를 만듭니다는 **IHttpHandler** 개체 하 고 전달 된 **IHttpContext** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-112">The **IRouteHandler** instance creates an **IHttpHandler** object and passes it the **IHttpContext** object.</span></span> <span data-ttu-id="eb469-113">기본적으로는 **IHttpHandler** MVC에 대 한 인스턴스는 **MvcHandler** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-113">By default, the **IHttpHandler** instance for MVC is the **MvcHandler** object.</span></span> <span data-ttu-id="eb469-114">**MvcHandler** 개체 다음 최종적으로 요청을 처리 하는 컨트롤러를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-114">The **MvcHandler** object then selects the controller that will ultimately handle the request.</span></span>

> [!NOTE]
> <span data-ttu-id="eb469-115">ASP.NET MVC 웹 응용 프로그램 IIS 7.0에서 실행 되 면 파일 이름 확장명이 없는 MVC 프로젝트에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-115">When an ASP.NET MVC Web application runs in IIS 7.0, no file name extension is required for MVC projects.</span></span> <span data-ttu-id="eb469-116">그러나 IIS 6.0에서는 처리기 해야.mvc 파일 이름 확장명을 ASP.NET ISAPI DLL에 매핑하는.</span><span class="sxs-lookup"><span data-stu-id="eb469-116">However, in IIS 6.0, the handler requires that you map the .mvc file name extension to the ASP.NET ISAPI DLL.</span></span>


<span data-ttu-id="eb469-117">모듈 및 이벤트 처리기는 ASP.NET MVC 프레임 워크에 있는 진입점입니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-117">The module and handler are the entry points to the ASP.NET MVC framework.</span></span> <span data-ttu-id="eb469-118">다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-118">They perform the following actions:</span></span>

- <span data-ttu-id="eb469-119">MVC 웹 응용 프로그램에서 적절 한 컨트롤러를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-119">Select the appropriate controller in an MVC Web application.</span></span>
- <span data-ttu-id="eb469-120">특정 컨트롤러 인스턴스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-120">Obtain a specific controller instance.</span></span>
- <span data-ttu-id="eb469-121">컨트롤러의 호출 **Execute** 메서드.</span><span class="sxs-lookup"><span data-stu-id="eb469-121">Call the controller's **Execute** method.</span></span>

<span data-ttu-id="eb469-122">다음은 MVC 웹 프로젝트에 대 한 실행 단계에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-122">The following lists the stages of execution for an MVC Web project:</span></span>

- <span data-ttu-id="eb469-123">응용 프로그램에 대 한 첫 번째 요청 받기</span><span class="sxs-lookup"><span data-stu-id="eb469-123">Receive first request for the application</span></span> 

    - <span data-ttu-id="eb469-124">Global.asax 파일에 **경로** 개체에 추가 되는 **RouteTable** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-124">In the Global.asax file, **Route** objects are added to the **RouteTable** object.</span></span>
- <span data-ttu-id="eb469-125">라우팅 수행</span><span class="sxs-lookup"><span data-stu-id="eb469-125">Perform routing</span></span> 

    - <span data-ttu-id="eb469-126">**UrlRoutingModule** 모듈에 일치 하는 첫 번째 사용 **경로** 개체에 **RouteTable** 만들 컬렉션의 **RouteData** 개체를 사용 하 여 만들려는 **RequestContext** (**IHttpContext**) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-126">The **UrlRoutingModule** module uses the first matching **Route** object in the **RouteTable** collection to create the **RouteData** object, which it then uses to create a **RequestContext** (**IHttpContext**) object.</span></span>
- <span data-ttu-id="eb469-127">MVC 요청 처리기 만들기</span><span class="sxs-lookup"><span data-stu-id="eb469-127">Create MVC request handler</span></span> 

    - <span data-ttu-id="eb469-128">**MvcRouteHandler** 개체의 인스턴스를 만듭니다는 **MvcHandler** 클래스 하 고 전달 된 **RequestContext** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="eb469-128">The **MvcRouteHandler** object creates an instance of the **MvcHandler** class and passes it the **RequestContext** instance.</span></span>
- <span data-ttu-id="eb469-129">컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="eb469-129">Create controller</span></span> 

    - <span data-ttu-id="eb469-130">**MvcHandler** 개체에서 사용 하는 **RequestContext** 인스턴스를 식별 하는 **IControllerFactory** 개체 (일반적으로의 인스턴스는  **DefaultControllerFactory** 클래스) 컨트롤러 인스턴스를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-130">The **MvcHandler** object uses the **RequestContext** instance to identify the **IControllerFactory** object (typically an instance of the **DefaultControllerFactory** class) to create the controller instance with.</span></span>
- <span data-ttu-id="eb469-131">Execute 컨트롤러-는 **MvcHandler** 인스턴스를 호출 하는 컨트롤러 s **Execute** 메서드.</span><span class="sxs-lookup"><span data-stu-id="eb469-131">Execute controller - The **MvcHandler** instance calls the controller s **Execute** method.</span></span> |
- <span data-ttu-id="eb469-132">작업 호출</span><span class="sxs-lookup"><span data-stu-id="eb469-132">Invoke action</span></span> 

    - <span data-ttu-id="eb469-133">상속 하는 대부분의 컨트롤러는 **컨트롤러** 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-133">Most controllers inherit from the **Controller** base class.</span></span> <span data-ttu-id="eb469-134">이렇게 하는 컨트롤러에 대 한는 **ControllerActionInvoker** 컨트롤러와 연결 된 개체를 호출 하려면 컨트롤러 클래스의 동작 방법을 결정 한 다음 해당 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-134">For controllers that do so, the **ControllerActionInvoker** object that is associated with the controller determines which action method of the controller class to call, and then calls that method.</span></span>
- <span data-ttu-id="eb469-135">결과 실행</span><span class="sxs-lookup"><span data-stu-id="eb469-135">Execute result</span></span> 

    - <span data-ttu-id="eb469-136">일반적인 동작 메서드에 사용자 입력을 받을 수 있습니다, 그리고 적절 한 응답 데이터를 준비 하 고 결과 형식을 반환 하 여 결과 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-136">A typical action method might receive user input, prepare the appropriate response data, and then execute the result by returning a result type.</span></span> <span data-ttu-id="eb469-137">실행 될 수 있는 기본 제공 결과 형식은 다음과 같습니다: **ViewResult** (뷰를 렌더링 하 고 있는 가장 자주 사용 되는 결과 형식), **RedirectToRouteResult**,  **된 RedirectResult**, **ContentResult**, **JsonResult**, 및 **EmptyResult**합니다.</span><span class="sxs-lookup"><span data-stu-id="eb469-137">The built-in result types that can be executed include the following: **ViewResult** (which renders a view and is the most-often used result type), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**, and **EmptyResult**.</span></span>
