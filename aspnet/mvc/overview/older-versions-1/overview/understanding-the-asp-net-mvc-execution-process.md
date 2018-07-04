---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: ASP.NET MVC 실행 프로세스 이해 | Microsoft Docs
author: microsoft
description: ASP.NET MVC 프레임 워크에서 단계별 브라우저 요청을 처리 하는 방법에 대해 알아봅니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: d94fcedb6e0ec6134bdbd69729abf1f875fac420
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37378273"
---
<a name="understanding-the-aspnet-mvc-execution-process"></a><span data-ttu-id="98505-103">ASP.NET MVC 실행 프로세스 이해</span><span class="sxs-lookup"><span data-stu-id="98505-103">Understanding the ASP.NET MVC Execution Process</span></span>
====================
<span data-ttu-id="98505-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="98505-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="98505-105">ASP.NET MVC 프레임 워크에서 단계별 브라우저 요청을 처리 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="98505-105">Learn how the ASP.NET MVC framework processes a browser request step-by-step.</span></span>


<span data-ttu-id="98505-106">ASP.NET MVC 기반 웹 응용 프로그램에 대 한 요청을 통해 먼저 전달 합니다 **UrlRoutingModule** 개체는 HTTP 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="98505-106">Requests to an ASP.NET MVC-based Web application first pass through the **UrlRoutingModule** object, which is an HTTP module.</span></span> <span data-ttu-id="98505-107">이 모듈 요청을 구문 분석 하 고 경로 선택을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="98505-107">This module parses the request and performs route selection.</span></span> <span data-ttu-id="98505-108">합니다 **UrlRoutingModule** 개체가 현재 요청과 일치 하는 첫 번째 경로 개체를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="98505-108">The **UrlRoutingModule** object selects the first route object that matches the current request.</span></span> <span data-ttu-id="98505-109">(경로 개체는 구현 하는 클래스 **RouteBase**, 이며 인스턴스는 일반적으로 **경로** 클래스입니다.) 경로가 일치 하는 경우는 **UrlRoutingModule** 개체 아무 작업도 수행 하지 및 대체 일반 ASP.NET 또는 IIS 요청 처리 요청을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98505-109">(A route object is a class that implements **RouteBase**, and is typically an instance of the **Route** class.) If no routes match, the **UrlRoutingModule** object does nothing and lets the request fall back to the regular ASP.NET or IIS request processing.</span></span>

<span data-ttu-id="98505-110">선택한 **경로** 개체를 **UrlRoutingModule** 개체를 가져옵니다 합니다 **IRouteHandler** 연관 된 개체는 **경로**개체입니다.</span><span class="sxs-lookup"><span data-stu-id="98505-110">From the selected **Route** object, the **UrlRoutingModule** object obtains the **IRouteHandler** object that is associated with the **Route** object.</span></span> <span data-ttu-id="98505-111">일반적으로 MVC 응용 프로그램에서이의 인스턴스여야 **MvcRouteHandler**합니다.</span><span class="sxs-lookup"><span data-stu-id="98505-111">Typically, in an MVC application, this will be an instance of **MvcRouteHandler**.</span></span> <span data-ttu-id="98505-112">합니다 **IRouteHandler** 인스턴스를 만듭니다를 **IHttpHandler** 개체를 전달 합니다 **IHttpContext** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="98505-112">The **IRouteHandler** instance creates an **IHttpHandler** object and passes it the **IHttpContext** object.</span></span> <span data-ttu-id="98505-113">기본적으로 **IHttpHandler** MVC에 대 한 인스턴스를 **MvcHandler** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="98505-113">By default, the **IHttpHandler** instance for MVC is the **MvcHandler** object.</span></span> <span data-ttu-id="98505-114">합니다 **MvcHandler** 개체에는 다음 최종적으로 요청을 처리 하는 컨트롤러를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="98505-114">The **MvcHandler** object then selects the controller that will ultimately handle the request.</span></span>

> [!NOTE]
> <span data-ttu-id="98505-115">ASP.NET MVC 웹 응용 프로그램을 IIS 7.0에서 실행 되 면 파일 이름 확장명이 없는 경우 MVC 프로젝트에 필요 하므로</span><span class="sxs-lookup"><span data-stu-id="98505-115">When an ASP.NET MVC Web application runs in IIS 7.0, no file name extension is required for MVC projects.</span></span> <span data-ttu-id="98505-116">그러나 IIS 6.0에서는 처리기가 ASP.NET ISAPI DLL에 따라.mvc 파일 확장명에 매핑하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="98505-116">However, in IIS 6.0, the handler requires that you map the .mvc file name extension to the ASP.NET ISAPI DLL.</span></span>


<span data-ttu-id="98505-117">모듈 및 처리기는 ASP.NET MVC 프레임 워크에 대 한 진입점입니다.</span><span class="sxs-lookup"><span data-stu-id="98505-117">The module and handler are the entry points to the ASP.NET MVC framework.</span></span> <span data-ttu-id="98505-118">다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="98505-118">They perform the following actions:</span></span>

- <span data-ttu-id="98505-119">MVC 웹 응용 프로그램에서 적절 한 컨트롤러를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="98505-119">Select the appropriate controller in an MVC Web application.</span></span>
- <span data-ttu-id="98505-120">특정 컨트롤러 인스턴스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="98505-120">Obtain a specific controller instance.</span></span>
- <span data-ttu-id="98505-121">컨트롤러의 호출 **Execute** 메서드.</span><span class="sxs-lookup"><span data-stu-id="98505-121">Call the controller's **Execute** method.</span></span>

<span data-ttu-id="98505-122">다음은 MVC 웹 프로젝트에 대 한 실행의 모든 단계에 대 한 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="98505-122">The following lists the stages of execution for an MVC Web project:</span></span>

- <span data-ttu-id="98505-123">응용 프로그램에 대 한 첫 번째 요청 받기</span><span class="sxs-lookup"><span data-stu-id="98505-123">Receive first request for the application</span></span> 

    - <span data-ttu-id="98505-124">Global.asax 파일에서 **경로** 개체에 추가 되는 **RouteTable** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="98505-124">In the Global.asax file, **Route** objects are added to the **RouteTable** object.</span></span>
- <span data-ttu-id="98505-125">라우팅 수행</span><span class="sxs-lookup"><span data-stu-id="98505-125">Perform routing</span></span> 

    - <span data-ttu-id="98505-126">**UrlRoutingModule** 모듈의 첫 번째 일치를 사용 **경로** 개체를 **RouteTable** 만들려는 컬렉션의 **RouteData** 그런 다음 만들기를 사용 하는 개체를 **RequestContext** (**IHttpContext**) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="98505-126">The **UrlRoutingModule** module uses the first matching **Route** object in the **RouteTable** collection to create the **RouteData** object, which it then uses to create a **RequestContext** (**IHttpContext**) object.</span></span>
- <span data-ttu-id="98505-127">MVC 요청 처리기 만들기</span><span class="sxs-lookup"><span data-stu-id="98505-127">Create MVC request handler</span></span> 

    - <span data-ttu-id="98505-128">**MvcRouteHandler** 개체의 인스턴스를 만듭니다 합니다 **MvcHandler** 클래스를 전달 합니다 **RequestContext** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="98505-128">The **MvcRouteHandler** object creates an instance of the **MvcHandler** class and passes it the **RequestContext** instance.</span></span>
- <span data-ttu-id="98505-129">컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="98505-129">Create controller</span></span> 

    - <span data-ttu-id="98505-130">**MvcHandler** 개체에서 사용 하는 **RequestContext** 인스턴스를 식별 하는 **IControllerFactory** 개체 (일반적으로 인스턴스를  **DefaultControllerFactory** 클래스)를 사용 하 여 컨트롤러 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98505-130">The **MvcHandler** object uses the **RequestContext** instance to identify the **IControllerFactory** object (typically an instance of the **DefaultControllerFactory** class) to create the controller instance with.</span></span>
- <span data-ttu-id="98505-131">Execute 컨트롤러-합니다 **MvcHandler** s 컨트롤러를 호출 하는 인스턴스 **Execute** 메서드.</span><span class="sxs-lookup"><span data-stu-id="98505-131">Execute controller - The **MvcHandler** instance calls the controller s **Execute** method.</span></span> |
- <span data-ttu-id="98505-132">작업 호출</span><span class="sxs-lookup"><span data-stu-id="98505-132">Invoke action</span></span> 

    - <span data-ttu-id="98505-133">대부분의 컨트롤러에서 상속 된 **컨트롤러** 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="98505-133">Most controllers inherit from the **Controller** base class.</span></span> <span data-ttu-id="98505-134">이렇게 하는 컨트롤러에 대 한 합니다 **ControllerActionInvoker** 컨트롤러와 연결 된 개체를 호출 하려면 컨트롤러 클래스의 동작 방법을 결정 합니다. 해당 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="98505-134">For controllers that do so, the **ControllerActionInvoker** object that is associated with the controller determines which action method of the controller class to call, and then calls that method.</span></span>
- <span data-ttu-id="98505-135">결과 실행</span><span class="sxs-lookup"><span data-stu-id="98505-135">Execute result</span></span> 

    - <span data-ttu-id="98505-136">일반적인 동작 메서드를 사용자 입력을 받을 수 있습니다, 그리고 적절 한 응답 데이터 준비 및 결과 형식을 반환 하 여 결과 실행 한 다음</span><span class="sxs-lookup"><span data-stu-id="98505-136">A typical action method might receive user input, prepare the appropriate response data, and then execute the result by returning a result type.</span></span> <span data-ttu-id="98505-137">실행할 수 있는 기본 제공 결과 형식은 다음과 같습니다: **ViewResult** 는 뷰를 렌더링과 가장 자주 사용 되는 결과 형식입니다 **RedirectToRouteResult**,  **된 RedirectResult**, **ContentResult**합니다 **JsonResult**, 및 **EmptyResult**합니다.</span><span class="sxs-lookup"><span data-stu-id="98505-137">The built-in result types that can be executed include the following: **ViewResult** (which renders a view and is the most-often used result type), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**, and **EmptyResult**.</span></span>
