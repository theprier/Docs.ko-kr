---
uid: web-api/overview/advanced/configuring-aspnet-web-api
title: "ASP.NET Web API 2 구성 | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2014
ms.topic: article
ms.assetid: 9e10a700-8d91-4d2e-a31e-b8b569fe867c
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/advanced/configuring-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 1c007c4c327b7cde6ff52c6b0022acdff3c9b137
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="configuring-aspnet-web-api-2"></a><span data-ttu-id="4101e-102">ASP.NET Web API 2 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-102">Configuring ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="4101e-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="4101e-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="4101e-104">이 항목에서는 ASP.NET Web API를 구성 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-104">This topic describes how to configure ASP.NET Web API.</span></span>

- [<span data-ttu-id="4101e-105">구성 설정</span><span class="sxs-lookup"><span data-stu-id="4101e-105">Configuration Settings</span></span>](#settings)
- [<span data-ttu-id="4101e-106">ASP.NET 호스팅와 Web API 구성</span><span class="sxs-lookup"><span data-stu-id="4101e-106">Configuring Web API with ASP.NET Hosting</span></span>](#webhost)
- [<span data-ttu-id="4101e-107">Web API OWIN 자체 호스팅을 사용 구성</span><span class="sxs-lookup"><span data-stu-id="4101e-107">Configuring Web API with OWIN Self-Hosting</span></span>](#selfhost)
- [<span data-ttu-id="4101e-108">전역 웹 API 서비스</span><span class="sxs-lookup"><span data-stu-id="4101e-108">Global Web API Services</span></span>](#services)
- [<span data-ttu-id="4101e-109">-컨트롤러 구성</span><span class="sxs-lookup"><span data-stu-id="4101e-109">Per-Controller Configuration</span></span>](#percontrollerconfig)

<a id="settings"></a>
## <a name="configuration-settings"></a><span data-ttu-id="4101e-110">구성 설정</span><span class="sxs-lookup"><span data-stu-id="4101e-110">Configuration Settings</span></span>

<span data-ttu-id="4101e-111">구성 설정은 웹 API에 정의 된는 [HttpConfiguration](https://msdn.microsoft.com/en-us/library/system.web.http.httpconfiguration.aspx) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-111">Web API configuration setttings are defined in the [HttpConfiguration](https://msdn.microsoft.com/en-us/library/system.web.http.httpconfiguration.aspx) class.</span></span>

| <span data-ttu-id="4101e-112">멤버</span><span class="sxs-lookup"><span data-stu-id="4101e-112">Member</span></span> | <span data-ttu-id="4101e-113">설명</span><span class="sxs-lookup"><span data-stu-id="4101e-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4101e-114">**DependencyResolver**</span><span class="sxs-lookup"><span data-stu-id="4101e-114">**DependencyResolver**</span></span> | <span data-ttu-id="4101e-115">컨트롤러에 대 한 종속성 주입을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-115">Enables dependency injection for controllers.</span></span> <span data-ttu-id="4101e-116">참조 [Web API 종속성 확인자를 사용 하 여](dependency-injection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-116">See [Using the Web API Dependency Resolver](dependency-injection.md).</span></span> |
| <span data-ttu-id="4101e-117">**필터**</span><span class="sxs-lookup"><span data-stu-id="4101e-117">**Filters**</span></span> | <span data-ttu-id="4101e-118">작업 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-118">Action filters.</span></span> |
| <span data-ttu-id="4101e-119">**포맷터**</span><span class="sxs-lookup"><span data-stu-id="4101e-119">**Formatters**</span></span> | <span data-ttu-id="4101e-120">[미디어 유형 포맷터](../formats-and-model-binding/media-formatters.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-120">[Media-type formatters](../formats-and-model-binding/media-formatters.md).</span></span> |
| <span data-ttu-id="4101e-121">**IncludeErrorDetailPolicy**</span><span class="sxs-lookup"><span data-stu-id="4101e-121">**IncludeErrorDetailPolicy**</span></span> | <span data-ttu-id="4101e-122">서버 HTTP 응답 메시지에 예외 메시지, 스택 추적 등의 오류 정보를 포함할지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-122">Specifies whether the server should include error details, such as exception messages and stack traces, in HTTP response messages.</span></span> <span data-ttu-id="4101e-123">참조 [IncludeErrorDetailPolicy](https://msdn.microsoft.com/en-us/library/system.web.http.includeerrordetailpolicy(v=vs.108))합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-123">See [IncludeErrorDetailPolicy](https://msdn.microsoft.com/en-us/library/system.web.http.includeerrordetailpolicy(v=vs.108)).</span></span> |
| <span data-ttu-id="4101e-124">**이니셜라이저**</span><span class="sxs-lookup"><span data-stu-id="4101e-124">**Initializer**</span></span> | <span data-ttu-id="4101e-125">최종 초기화를 수행 하는 함수는 **HttpConfiguration**합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-125">A function that performs final initialization of the **HttpConfiguration**.</span></span> |
| <span data-ttu-id="4101e-126">**MessageHandlers**</span><span class="sxs-lookup"><span data-stu-id="4101e-126">**MessageHandlers**</span></span> | <span data-ttu-id="4101e-127">[HTTP 메시지 처리기](http-message-handlers.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-127">[HTTP message handlers](http-message-handlers.md).</span></span> |
| <span data-ttu-id="4101e-128">**ParameterBindingRules**</span><span class="sxs-lookup"><span data-stu-id="4101e-128">**ParameterBindingRules**</span></span> | <span data-ttu-id="4101e-129">바인딩 매개 변수에서 컨트롤러 작업에 대 한 규칙의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-129">A collection of rules for binding parameters on controller actions.</span></span> |
| <span data-ttu-id="4101e-130">**속성**</span><span class="sxs-lookup"><span data-stu-id="4101e-130">**Properties**</span></span> | <span data-ttu-id="4101e-131">일반 속성 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-131">A generic property bag.</span></span> |
| <span data-ttu-id="4101e-132">**경로**</span><span class="sxs-lookup"><span data-stu-id="4101e-132">**Routes**</span></span> | <span data-ttu-id="4101e-133">경로의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-133">The collection of routes.</span></span> <span data-ttu-id="4101e-134">참조 [ASP.NET Web API의에서 라우팅](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-134">See [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="4101e-135">**서비스**</span><span class="sxs-lookup"><span data-stu-id="4101e-135">**Services**</span></span> | <span data-ttu-id="4101e-136">서비스의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-136">The collection of services.</span></span> <span data-ttu-id="4101e-137">참조 [서비스](#services)합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-137">See [Services](#services).</span></span> |


## <a name="prerequisites"></a><span data-ttu-id="4101e-138">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="4101e-138">Prerequisites</span></span>

<span data-ttu-id="4101e-139">[Visual Studio 2017](https://www.visualstudio.com/vs/) Community, Professional 또는 Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="4101e-139">[Visual Studio 2017](https://www.visualstudio.com/vs/) Community, Professional, or Enterprise Edition.</span></span>

<a id="webhost"></a>
## <a name="configuring-web-api-with-aspnet-hosting"></a><span data-ttu-id="4101e-140">ASP.NET 호스팅와 Web API 구성</span><span class="sxs-lookup"><span data-stu-id="4101e-140">Configuring Web API with ASP.NET Hosting</span></span>

<span data-ttu-id="4101e-141">ASP.NET 응용 프로그램에서 Web API를 호출 하 여 구성 [GlobalConfiguration.Configure](https://msdn.microsoft.com/en-us/library/system.web.http.globalconfiguration.configure.aspx) 에 **응용 프로그램\_시작** 메서드.</span><span class="sxs-lookup"><span data-stu-id="4101e-141">In an ASP.NET application, configure Web API by calling [GlobalConfiguration.Configure](https://msdn.microsoft.com/en-us/library/system.web.http.globalconfiguration.configure.aspx) in the **Application\_Start** method.</span></span> <span data-ttu-id="4101e-142">**구성** 형식의 단일 매개 변수를 사용 하 여 대리자 메서드를 사용 하며 **HttpConfiguration**합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-142">The **Configure** method takes a delegate with a single parameter of type **HttpConfiguration**.</span></span> <span data-ttu-id="4101e-143">대리자 내 구성 프로그램을 모두 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-143">Perform all of your configuation inside the delegate.</span></span>

<span data-ttu-id="4101e-144">익명 대리자를 사용 하는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-144">Here is an example using an anonymous delegate:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="4101e-145">Visual Studio 2017 년에서 "ASP.NET 웹 응용 프로그램" 프로젝트 템플릿을 자동으로 설정 구성 코드에서 "웹 API"를 선택 하는 경우는 **새 ASP.NET 프로젝트** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="4101e-145">In Visual Studio 2017, the "ASP.NET Web Application" project template automatically sets up the configuration code, if you select "Web API" in the **New ASP.NET Project** dialog.</span></span>

[![](configuring-aspnet-web-api/_static/image2.png)](configuring-aspnet-web-api/_static/image1.png)

<span data-ttu-id="4101e-146">프로젝트 템플릿은 응용 프로그램 안에 WebApiConfig.cs 라는 파일을 만듭니다\_시작 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-146">The project template creates a file named WebApiConfig.cs inside the App\_Start folder.</span></span> <span data-ttu-id="4101e-147">이 코드 파일 Web API 구성 코드를 입력 해야 하는 대리자를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-147">This code file defines the delegate where you should put your Web API configuration code.</span></span>

![](configuring-aspnet-web-api/_static/image3.png)

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample2.cs?highlight=12)]

<span data-ttu-id="4101e-148">프로젝트 템플릿에 또한에서 대리자를 호출 하는 코드 추가 **응용 프로그램\_시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-148">The project template also adds the code that calls the delegate from **Application\_Start**.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample3.cs?highlight=5)]

<a id="selfhost"></a>
## <a name="configuring-web-api-with-owin-self-hosting"></a><span data-ttu-id="4101e-149">Web API OWIN 자체 호스팅을 사용 구성</span><span class="sxs-lookup"><span data-stu-id="4101e-149">Configuring Web API with OWIN Self-Hosting</span></span>

<span data-ttu-id="4101e-150">경우 OWIN과 자체 호스트를 만들 새 **HttpConfiguration** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="4101e-150">If you are self-hosting with OWIN, create a new **HttpConfiguration** instance.</span></span> <span data-ttu-id="4101e-151">이 인스턴스에서 구성을 수행 하 고 그런 다음 인스턴스를는 **Owin.UseWebApi** 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="4101e-151">Perform any configuration on this instance, and then pass the instance to the **Owin.UseWebApi** extension method.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="4101e-152">자습서 [Self-Host ASP.NET Web API 2를 사용 하 여 OWIN](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md) 전체 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-152">The tutorial [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md) shows the complete steps.</span></span>

<a id="services"></a>
## <a name="global-web-api-services"></a><span data-ttu-id="4101e-153">전역 웹 API 서비스</span><span class="sxs-lookup"><span data-stu-id="4101e-153">Global Web API Services</span></span>

<span data-ttu-id="4101e-154">**HttpConfiguration.Services** 컬렉션 Web API 컨트롤러 선택 및 콘텐츠 협상 등의 다양 한 작업을 수행 하기 위해 사용 하는 글로벌 서비스의 집합을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-154">The **HttpConfiguration.Services** collection contains a set of global services that Web API uses to perform various tasks, such as controller selection and content negotiation.</span></span>

> [!NOTE]
> <span data-ttu-id="4101e-155">**서비스** 컬렉션 서비스 검색 또는 종속성 주입을 위한 일반 용도의 메커니즘은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-155">The **Services** collection is not a general-purpose mechanism for service discovery or dependency injection.</span></span> <span data-ttu-id="4101e-156">Web API 프레임 워크에 알려진 서비스 종류를 저장 하기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-156">It only stores service types that are known to the Web API framework.</span></span>


<span data-ttu-id="4101e-157">**서비스** 컬렉션 서비스의 기본 집합으로 초기화 되 고 사용자 고유의 사용자 지정 구현을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-157">The **Services** collection is initialized with a default set of services, and you can provide your own custom implementations.</span></span> <span data-ttu-id="4101e-158">인스턴스가 하나만 있을 수 있지만 다른 일부 서비스에서 여러 인스턴스를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-158">Some services support multiple instances, while others can have only one instance.</span></span> <span data-ttu-id="4101e-159">그러나 (컨트롤러 수준에서 서비스를 제공할 수도 있습니다; 참조 [-컨트롤러 구성](#percontrollerconfig)합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-159">(However, you can also provide services at the controller level; see [Per-Controller Configuration](#percontrollerconfig).</span></span>

<span data-ttu-id="4101e-160">단일 인스턴스 서비스</span><span class="sxs-lookup"><span data-stu-id="4101e-160">Single-Instance Services</span></span>


| <span data-ttu-id="4101e-161">서비스</span><span class="sxs-lookup"><span data-stu-id="4101e-161">Service</span></span> | <span data-ttu-id="4101e-162">설명</span><span class="sxs-lookup"><span data-stu-id="4101e-162">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4101e-163">**IActionValueBinder**</span><span class="sxs-lookup"><span data-stu-id="4101e-163">**IActionValueBinder**</span></span> | <span data-ttu-id="4101e-164">매개 변수 바인딩을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-164">Gets a binding for a parameter.</span></span> |
| <span data-ttu-id="4101e-165">**IApiExplorer**</span><span class="sxs-lookup"><span data-stu-id="4101e-165">**IApiExplorer**</span></span> | <span data-ttu-id="4101e-166">응용 프로그램에 의해 노출 된 Api의 설명을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-166">Gets descriptions of the APIs exposed by the application.</span></span> <span data-ttu-id="4101e-167">참조 [웹 API에 대 한 도움말 페이지를 만드는](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-167">See [Creating a Help Page for a Web API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md).</span></span> |
| <span data-ttu-id="4101e-168">**IAssembliesResolver**</span><span class="sxs-lookup"><span data-stu-id="4101e-168">**IAssembliesResolver**</span></span> | <span data-ttu-id="4101e-169">응용 프로그램에 대 한 어셈블리의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-169">Gets a list of the assemblies for the application.</span></span> <span data-ttu-id="4101e-170">참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-170">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="4101e-171">**IBodyModelValidator**</span><span class="sxs-lookup"><span data-stu-id="4101e-171">**IBodyModelValidator**</span></span> | <span data-ttu-id="4101e-172">미디어 유형 포맷터는 요청 본문에서 읽을 수 있는 모델의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-172">Validates a model that is read from the request body by a media-type formatter.</span></span> |
| <span data-ttu-id="4101e-173">**IContentNegotiator**</span><span class="sxs-lookup"><span data-stu-id="4101e-173">**IContentNegotiator**</span></span> | <span data-ttu-id="4101e-174">콘텐츠 협상을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-174">Performs content negotiation.</span></span> |
| <span data-ttu-id="4101e-175">**IDocumentationProvider**</span><span class="sxs-lookup"><span data-stu-id="4101e-175">**IDocumentationProvider**</span></span> | <span data-ttu-id="4101e-176">Api에 대 한 설명서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-176">Provides documentation for APIs.</span></span> <span data-ttu-id="4101e-177">기본값은 **null**합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-177">The default is **null**.</span></span> <span data-ttu-id="4101e-178">참조 [웹 API에 대 한 도움말 페이지를 만드는](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-178">See [Creating a Help Page for a Web API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md).</span></span> |
| <span data-ttu-id="4101e-179">**IHostBufferPolicySelector**</span><span class="sxs-lookup"><span data-stu-id="4101e-179">**IHostBufferPolicySelector**</span></span> | <span data-ttu-id="4101e-180">호스트 HTTP 메시지의 엔터티 본문을 버퍼링 해야 하는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-180">Indicates whether the host should buffer HTTP message entity bodies.</span></span> |
| <span data-ttu-id="4101e-181">**IHttpActionInvoker**</span><span class="sxs-lookup"><span data-stu-id="4101e-181">**IHttpActionInvoker**</span></span> | <span data-ttu-id="4101e-182">컨트롤러 동작을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-182">Invokes a controller action.</span></span> <span data-ttu-id="4101e-183">참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-183">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="4101e-184">**IHttpActionSelector**</span><span class="sxs-lookup"><span data-stu-id="4101e-184">**IHttpActionSelector**</span></span> | <span data-ttu-id="4101e-185">컨트롤러 동작을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-185">Selects a controller action.</span></span> <span data-ttu-id="4101e-186">참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-186">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="4101e-187">**IHttpControllerActivator**</span><span class="sxs-lookup"><span data-stu-id="4101e-187">**IHttpControllerActivator**</span></span> | <span data-ttu-id="4101e-188">컨트롤러를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-188">Activates a controller.</span></span> <span data-ttu-id="4101e-189">참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-189">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="4101e-190">**IHttpControllerSelector**</span><span class="sxs-lookup"><span data-stu-id="4101e-190">**IHttpControllerSelector**</span></span> | <span data-ttu-id="4101e-191">컨트롤러를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-191">Selects a controller.</span></span> <span data-ttu-id="4101e-192">참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-192">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="4101e-193">**IHttpControllerTypeResolver**</span><span class="sxs-lookup"><span data-stu-id="4101e-193">**IHttpControllerTypeResolver**</span></span> | <span data-ttu-id="4101e-194">응용 프로그램에서 Web API 컨트롤러 형식의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-194">Provides a list of the Web API controller types in the application.</span></span> <span data-ttu-id="4101e-195">참조 [라우팅 및 작업 선택](../web-api-routing-and-actions/routing-and-action-selection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-195">See [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span> |
| <span data-ttu-id="4101e-196">**ITraceManager**</span><span class="sxs-lookup"><span data-stu-id="4101e-196">**ITraceManager**</span></span> | <span data-ttu-id="4101e-197">추적 프레임 워크를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-197">Initializes the tracing framework.</span></span> <span data-ttu-id="4101e-198">참조 [ASP.NET Web API의에서 추적](../testing-and-debugging/tracing-in-aspnet-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-198">See [Tracing in ASP.NET Web API](../testing-and-debugging/tracing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="4101e-199">**ITraceWriter**</span><span class="sxs-lookup"><span data-stu-id="4101e-199">**ITraceWriter**</span></span> | <span data-ttu-id="4101e-200">추적 기록기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-200">Provides a trace writer.</span></span> <span data-ttu-id="4101e-201">기본값은 "아무" 추적 기록기입니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-201">The default is a "no-op" trace writer.</span></span> <span data-ttu-id="4101e-202">참조 [ASP.NET Web API의에서 추적](../testing-and-debugging/tracing-in-aspnet-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-202">See [Tracing in ASP.NET Web API](../testing-and-debugging/tracing-in-aspnet-web-api.md).</span></span> |
| <span data-ttu-id="4101e-203">**IModelValidatorCache**</span><span class="sxs-lookup"><span data-stu-id="4101e-203">**IModelValidatorCache**</span></span> | <span data-ttu-id="4101e-204">모델 유효성 검사기의 캐시를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-204">Provides a cache of model validators.</span></span> |

<span data-ttu-id="4101e-205">다중 인스턴스 서비스</span><span class="sxs-lookup"><span data-stu-id="4101e-205">Multiple-Instance Services</span></span>


| <span data-ttu-id="4101e-206">서비스</span><span class="sxs-lookup"><span data-stu-id="4101e-206">Service</span></span> | <span data-ttu-id="4101e-207">설명</span><span class="sxs-lookup"><span data-stu-id="4101e-207">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4101e-208">**IFilterProvider**</span><span class="sxs-lookup"><span data-stu-id="4101e-208">**IFilterProvider**</span></span> | <span data-ttu-id="4101e-209">컨트롤러 작업에 대 한 필터의 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-209">Returns a list of filters for a controller action.</span></span> |
| <span data-ttu-id="4101e-210">**ModelBinderProvider**</span><span class="sxs-lookup"><span data-stu-id="4101e-210">**ModelBinderProvider**</span></span> | <span data-ttu-id="4101e-211">지정된 된 형식에 대 한 모델 바인더를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-211">Returns a model binder for a given type.</span></span> |
| <span data-ttu-id="4101e-212">**ModelMetadataProvider**</span><span class="sxs-lookup"><span data-stu-id="4101e-212">**ModelMetadataProvider**</span></span> | <span data-ttu-id="4101e-213">모델에 대 한 메타 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-213">Provides metadata for a model.</span></span> |
| <span data-ttu-id="4101e-214">**ModelValidatorProvider**</span><span class="sxs-lookup"><span data-stu-id="4101e-214">**ModelValidatorProvider**</span></span> | <span data-ttu-id="4101e-215">모델 유효성 검사기를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-215">Provides a validator for a model.</span></span> |
| <span data-ttu-id="4101e-216">**ValueProviderFactory**</span><span class="sxs-lookup"><span data-stu-id="4101e-216">**ValueProviderFactory**</span></span> | <span data-ttu-id="4101e-217">값 공급자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-217">Creates a value provider.</span></span> <span data-ttu-id="4101e-218">자세한 내용은 Mike Stall 블로그 게시물을 참조 하십시오. [WebAPI에 사용자 지정 값 공급자를 만드는 방법](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)</span><span class="sxs-lookup"><span data-stu-id="4101e-218">For more information, see Mike Stall's blog post [How to create a custom value provider in WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)</span></span> |<span data-ttu-id="4101e-219">입니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-219">.</span></span>

<span data-ttu-id="4101e-220">여러 인스턴스 서비스에 사용자 지정 구현을 추가 하려면 **추가** 또는 **삽입** 에 **서비스** 컬렉션:</span><span class="sxs-lookup"><span data-stu-id="4101e-220">To add a custom implementation to a multi-instance service, call **Add** or **Insert** on the **Services** collection:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="4101e-221">단일 인스턴스 서비스 사용자 지정 구현으로 교체 하려면 호출 **대체** 에 **서비스** 컬렉션:</span><span class="sxs-lookup"><span data-stu-id="4101e-221">To replace a single-instance service with a custom implementation, call **Replace** on the **Services** collection:</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample6.cs)]

<a id="percontrollerconfig"></a>
## <a name="per-controller-configuration"></a><span data-ttu-id="4101e-222">-컨트롤러 구성</span><span class="sxs-lookup"><span data-stu-id="4101e-222">Per-Controller Configuration</span></span>

<span data-ttu-id="4101e-223">-컨트롤러 별로 다음 설정을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-223">You can override the following settings on a per-controller basis:</span></span>

- <span data-ttu-id="4101e-224">미디어 유형 포맷터</span><span class="sxs-lookup"><span data-stu-id="4101e-224">Media-type formatters</span></span>
- <span data-ttu-id="4101e-225">매개 변수 바인딩 규칙</span><span class="sxs-lookup"><span data-stu-id="4101e-225">Parameter binding rules</span></span>
- <span data-ttu-id="4101e-226">서비스</span><span class="sxs-lookup"><span data-stu-id="4101e-226">Services</span></span>

<span data-ttu-id="4101e-227">이렇게 하려면 사용자 지정 특성을 구현 하는 정의 **IControllerConfiguration** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-227">To do so, define a custom attribute that implements the **IControllerConfiguration** interface.</span></span> <span data-ttu-id="4101e-228">컨트롤러에 특성을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-228">Then apply the attribute to the controller.</span></span>

<span data-ttu-id="4101e-229">다음 예제에서는 사용자 지정 포맷터와 기본 미디어 유형 포맷터를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-229">The following example replaces the default media-type formatters with a custom formatter.</span></span>

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="4101e-230">**IControllerConfiguration.Initialize** 메서드는 두 개의 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-230">The **IControllerConfiguration.Initialize** method takes two parameters:</span></span>

- <span data-ttu-id="4101e-231">**HttpControllerSettings** 개체</span><span class="sxs-lookup"><span data-stu-id="4101e-231">An **HttpControllerSettings** object</span></span>
- <span data-ttu-id="4101e-232">**HttpControllerDescriptor** 개체</span><span class="sxs-lookup"><span data-stu-id="4101e-232">An **HttpControllerDescriptor** object</span></span>

<span data-ttu-id="4101e-233">**HttpControllerDescriptor** 정보 제공 목적으로 (예를 들어 두 명의 컨트롤러를 구분 하기 위해)를 검사할 수 있습니다는 컨트롤러에 대 한 설명을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-233">The **HttpControllerDescriptor** contains a description of the controller, which you can examine for informational purposes (say, to distinguish between two controllers).</span></span>

<span data-ttu-id="4101e-234">사용 하 여 **HttpControllerSettings** 컨트롤러를 구성 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-234">Use the **HttpControllerSettings** object to configure the controller.</span></span> <span data-ttu-id="4101e-235">이 개체의 구성 매개 변수-컨트롤러 별로 재정의할 수 있는 하위 집합을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-235">This object contains the subset of configuration parameters that you can override on a per-controller basis.</span></span> <span data-ttu-id="4101e-236">모든 설정을 변경 하지 않으면 기본적으로 전역 **HttpConfiguration** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="4101e-236">Any settings that you don't change default to the global **HttpConfiguration** object.</span></span>
