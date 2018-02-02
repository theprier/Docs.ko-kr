---
title: "HTTP 처리기 및 ASP.NET Core 미들웨어 모듈을 마이그레이션하는 방법"
author: rick-anderson
description: 
manager: wpickett
ms.author: tdykstra
ms.date: 12/07/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: migration/http-modules
ms.openlocfilehash: 8aac6c649b22dc8f6cfc916aa78d56efad7821a0
ms.sourcegitcommit: f2a11a89037471a77ad68a67533754b7bb8303e2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="migrating-http-handlers-and-modules-to-aspnet-core-middleware"></a><span data-ttu-id="5aa3f-102">HTTP 처리기 및 ASP.NET Core 미들웨어 모듈을 마이그레이션하는 방법</span><span class="sxs-lookup"><span data-stu-id="5aa3f-102">Migrating HTTP handlers and modules to ASP.NET Core middleware</span></span> 

<span data-ttu-id="5aa3f-103">으로 [Matt Perdeck](https://www.linkedin.com/in/mattperdeck)</span><span class="sxs-lookup"><span data-stu-id="5aa3f-103">By [Matt Perdeck](https://www.linkedin.com/in/mattperdeck)</span></span>

<span data-ttu-id="5aa3f-104">이 문서에서는 기존 ASP.NET 마이그레이션하는 방법을 보여 줍니다. [HTTP 모듈 및 처리기 system.webserver에서](https://docs.microsoft.com/iis/configuration/system.webserver/) ASP.NET Core로 [미들웨어](xref:fundamentals/middleware/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-104">This article shows how to migrate existing ASP.NET [HTTP modules and handlers from system.webserver](https://docs.microsoft.com/iis/configuration/system.webserver/) to ASP.NET Core [middleware](xref:fundamentals/middleware/index).</span></span>

## <a name="modules-and-handlers-revisited"></a><span data-ttu-id="5aa3f-105">모듈 및 revisited 처리기</span><span class="sxs-lookup"><span data-stu-id="5aa3f-105">Modules and handlers revisited</span></span>

<span data-ttu-id="5aa3f-106">ASP.NET Core 미들웨어를 계속 하기 전에 먼저 요약해 보면 HTTP 모듈 및 처리기의 작동 방식:</span><span class="sxs-lookup"><span data-stu-id="5aa3f-106">Before proceeding to ASP.NET Core middleware, let's first recap how HTTP modules and handlers work:</span></span>

![모듈 처리기](http-modules/_static/moduleshandlers.png)

<span data-ttu-id="5aa3f-108">**처리기는:**</span><span class="sxs-lookup"><span data-stu-id="5aa3f-108">**Handlers are:**</span></span>

   * <span data-ttu-id="5aa3f-109">구현 하는 클래스 [IHttpHandler](https://docs.microsoft.com/dotnet/api/system.web.ihttphandler)</span><span class="sxs-lookup"><span data-stu-id="5aa3f-109">Classes that implement [IHttpHandler](https://docs.microsoft.com/dotnet/api/system.web.ihttphandler)</span></span>

   * <span data-ttu-id="5aa3f-110">와 같은 지정 된 파일 이름이 나 확장명을 사용 하 여 요청을 처리 하는 데 사용 *보고서*</span><span class="sxs-lookup"><span data-stu-id="5aa3f-110">Used to handle requests with a given file name or extension, such as *.report*</span></span>

   * <span data-ttu-id="5aa3f-111">[구성 된](https://docs.microsoft.com//iis/configuration/system.webserver/handlers/) 에 *Web.config*</span><span class="sxs-lookup"><span data-stu-id="5aa3f-111">[Configured](https://docs.microsoft.com//iis/configuration/system.webserver/handlers/) in *Web.config*</span></span>

<span data-ttu-id="5aa3f-112">**모듈은:**</span><span class="sxs-lookup"><span data-stu-id="5aa3f-112">**Modules are:**</span></span>

   * <span data-ttu-id="5aa3f-113">구현 하는 클래스 [IHttpModule](https://docs.microsoft.com/dotnet/api/system.web.ihttpmodule)</span><span class="sxs-lookup"><span data-stu-id="5aa3f-113">Classes that implement [IHttpModule](https://docs.microsoft.com/dotnet/api/system.web.ihttpmodule)</span></span>

   * <span data-ttu-id="5aa3f-114">모든 요청에 대해 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-114">Invoked for every request</span></span>

   * <span data-ttu-id="5aa3f-115">(이후 처리를 중지 요청) 단락 (short-circuit) 수</span><span class="sxs-lookup"><span data-stu-id="5aa3f-115">Able to short-circuit (stop further processing of a request)</span></span>

   * <span data-ttu-id="5aa3f-116">HTTP 응답에 추가 하거나 직접 만들 수</span><span class="sxs-lookup"><span data-stu-id="5aa3f-116">Able to add to the HTTP response, or create their own</span></span>

   * <span data-ttu-id="5aa3f-117">[구성 된](https://docs.microsoft.com//iis/configuration/system.webserver/modules/) 에 *Web.config*</span><span class="sxs-lookup"><span data-stu-id="5aa3f-117">[Configured](https://docs.microsoft.com//iis/configuration/system.webserver/modules/) in *Web.config*</span></span>

<span data-ttu-id="5aa3f-118">**모듈에는 들어오는 요청을 처리 하는 순서는 의해 결정 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="5aa3f-118">**The order in which modules process incoming requests is determined by:**</span></span>

   1. <span data-ttu-id="5aa3f-119">[응용 프로그램 수명 주기](https://msdn.microsoft.com/library/ms227673.aspx), ASP.NET에서 발생 하는 계열 이벤트 변수인: [BeginRequest](https://docs.microsoft.com/dotnet/api/system.web.httpapplication.beginrequest), [AuthenticateRequest](https://docs.microsoft.com/dotnet/api/system.web.httpapplication.authenticaterequest)등입니다. 각 모듈 하나 이상의 이벤트에 대 한 처리기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-119">The [application life cycle](https://msdn.microsoft.com/library/ms227673.aspx), which is a series events fired by ASP.NET: [BeginRequest](https://docs.microsoft.com/dotnet/api/system.web.httpapplication.beginrequest), [AuthenticateRequest](https://docs.microsoft.com/dotnet/api/system.web.httpapplication.authenticaterequest), etc. Each module can create a handler for one or more events.</span></span>

   2. <span data-ttu-id="5aa3f-120">동일한 이벤트에서 구성 하는 순서에 대 한 *Web.config*합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-120">For the same event, the order in which they're configured in *Web.config*.</span></span>

<span data-ttu-id="5aa3f-121">모듈을 외에도 수명 주기 이벤트에 대 한 처리기를 추가할 수 있습니다 프로그램 *Global.asax.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-121">In addition to modules, you can add handlers for the life cycle events to your *Global.asax.cs* file.</span></span> <span data-ttu-id="5aa3f-122">이러한 처리기는 구성 된 모듈의 처리기 후 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-122">These handlers run after the handlers in the configured modules.</span></span>

## <a name="from-handlers-and-modules-to-middleware"></a><span data-ttu-id="5aa3f-123">처리기와 미들웨어 모듈에서</span><span class="sxs-lookup"><span data-stu-id="5aa3f-123">From handlers and modules to middleware</span></span>

<span data-ttu-id="5aa3f-124">**미들웨어는 HTTP 모듈 및 처리기 보다 간단 합니다.**</span><span class="sxs-lookup"><span data-stu-id="5aa3f-124">**Middleware are simpler than HTTP modules and handlers:**</span></span>

   * <span data-ttu-id="5aa3f-125">모듈, 처리기, *Global.asax.cs*, *Web.config* (제외 IIS 구성) 및 응용 프로그램 수명 주기 사라지게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-125">Modules, handlers, *Global.asax.cs*, *Web.config* (except for IIS configuration) and the application life cycle are gone</span></span>

   * <span data-ttu-id="5aa3f-126">미들웨어를 하나씩 수행 된 모듈과 처리기의 역할</span><span class="sxs-lookup"><span data-stu-id="5aa3f-126">The roles of both modules and handlers have been taken over by middleware</span></span>

   * <span data-ttu-id="5aa3f-127">코드를 사용 하 여 미들웨어 구성 대신 *Web.config*</span><span class="sxs-lookup"><span data-stu-id="5aa3f-127">Middleware are configured using code rather than in *Web.config*</span></span>

   * <span data-ttu-id="5aa3f-128">[파이프라인 분기](xref:fundamentals/middleware/index#middleware-run-map-use) 뿐만 아니라 요청 헤더, 쿼리 문자열 등에서 뿐만 아니라 URL을 기반으로 하는 특정 미들웨어에 요청을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-128">[Pipeline branching](xref:fundamentals/middleware/index#middleware-run-map-use) lets you send requests to specific middleware, based on not only the URL but also on request headers, query strings, etc.</span></span>

<span data-ttu-id="5aa3f-129">**미들웨어 모듈 매우 비슷합니다.**</span><span class="sxs-lookup"><span data-stu-id="5aa3f-129">**Middleware are very similar to modules:**</span></span>

   * <span data-ttu-id="5aa3f-130">모든 요청에 대해 원칙적으로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-130">Invoked in principle for every request</span></span>

   * <span data-ttu-id="5aa3f-131">단락 (short-circuit)는 요청으로 할 [다음 미들웨어에서 요청을 전달 하지 않을 경우](#http-modules-shortcircuiting-middleware)</span><span class="sxs-lookup"><span data-stu-id="5aa3f-131">Able to short-circuit a request, by [not passing the request to the next middleware](#http-modules-shortcircuiting-middleware)</span></span>

   * <span data-ttu-id="5aa3f-132">HTTP 응답을 만들 수</span><span class="sxs-lookup"><span data-stu-id="5aa3f-132">Able to create their own HTTP response</span></span>

<span data-ttu-id="5aa3f-133">**미들웨어와 모듈은 다른 순서로 처리 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="5aa3f-133">**Middleware and modules are processed in a different order:**</span></span>

   * <span data-ttu-id="5aa3f-134">미들웨어의 순서는 있는 삽입할 요청 파이프라인, 모듈의 순서는 주로 기반으로 하는 동안 순서에 따라 [응용 프로그램 수명 주기](https://msdn.microsoft.com/library/ms227673.aspx) 이벤트</span><span class="sxs-lookup"><span data-stu-id="5aa3f-134">Order of middleware is based on the order in which they're inserted into the request pipeline, while order of modules is mainly based on [application life cycle](https://msdn.microsoft.com/library/ms227673.aspx) events</span></span>

   * <span data-ttu-id="5aa3f-135">응답에 대 한 미들웨어의 순서는 모듈의 순서는 요청 및 응답에 대해 동일 하 게 하는 동안 요청에 대 한는 반대</span><span class="sxs-lookup"><span data-stu-id="5aa3f-135">Order of middleware for responses is the reverse from that for requests, while order of modules is the same for requests and responses</span></span>

   * <span data-ttu-id="5aa3f-136">참조 [IApplicationBuilder 미들웨어 파이프라인 만들기](xref:fundamentals/middleware/index#creating-a-middleware-pipeline-with-iapplicationbuilder)</span><span class="sxs-lookup"><span data-stu-id="5aa3f-136">See [Creating a middleware pipeline with IApplicationBuilder](xref:fundamentals/middleware/index#creating-a-middleware-pipeline-with-iapplicationbuilder)</span></span>

![미들웨어](http-modules/_static/middleware.png)

<span data-ttu-id="5aa3f-138">어떻게 요청 short-circuited 인증 미들웨어 위의 그림에서 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-138">Note how in the image above, the authentication middleware short-circuited the request.</span></span>

## <a name="migrating-module-code-to-middleware"></a><span data-ttu-id="5aa3f-139">미들웨어 모듈 코드 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="5aa3f-139">Migrating module code to middleware</span></span>

<span data-ttu-id="5aa3f-140">기존 HTTP 모듈은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-140">An existing HTTP module will look similar to this:</span></span>

[!code-csharp[Main](../migration/http-modules/sample/Asp.Net4/Asp.Net4/Modules/MyModule.cs?highlight=6,8,24,31)]

<span data-ttu-id="5aa3f-141">에 나와 있는 것 처럼는 [미들웨어](xref:fundamentals/middleware/index) 페이지, ASP.NET Core 미들웨어는 노출 하는 클래스는 `Invoke` 메서드 만들기는 `HttpContext` 반환 하 고는 `Task`합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-141">As shown in the [Middleware](xref:fundamentals/middleware/index) page, an ASP.NET Core middleware is a class that exposes an `Invoke` method taking an `HttpContext` and returning a `Task`.</span></span> <span data-ttu-id="5aa3f-142">새 미들웨어는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-142">Your new middleware will look like this:</span></span>

<a name="http-modules-usemiddleware"></a>

[!code-csharp[Main](../migration/http-modules/sample/Asp.Net.Core/Middleware/MyMiddleware.cs?highlight=9,13,20,24,28,30,32)]

<span data-ttu-id="5aa3f-143">이전 미들웨어 템플릿 섹션에서 만들어졌다면 [미들웨어를 작성](xref:fundamentals/middleware/index#middleware-writing-middleware)합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-143">The preceding middleware template was taken from the section on [writing middleware](xref:fundamentals/middleware/index#middleware-writing-middleware).</span></span>

<span data-ttu-id="5aa3f-144">*MyMiddlewareExtensions* 도우미 클래스를 사용 하면 쉽게에 미들웨어를 구성 하 여 `Startup` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-144">The *MyMiddlewareExtensions* helper class makes it easier to configure your middleware in your `Startup` class.</span></span> <span data-ttu-id="5aa3f-145">`UseMyMiddleware` 메서드 요청 파이프라인에 미들웨어 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-145">The `UseMyMiddleware` method adds your middleware class to the request pipeline.</span></span> <span data-ttu-id="5aa3f-146">미들웨어에서 필요한 서비스 미들웨어의 생성자에 지정 된 가져오기.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-146">Services required by the middleware get injected in the middleware's constructor.</span></span>

<a name="http-modules-shortcircuiting-middleware"></a>

<span data-ttu-id="5aa3f-147">모듈에는 예를 들어 사용자에 게 권한이 없는 경우 요청을 종료 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-147">Your module might terminate a request, for example if the user isn't authorized:</span></span>

[!code-csharp[Main](../migration/http-modules/sample/Asp.Net4/Asp.Net4/Modules/MyTerminatingModule.cs?highlight=9,10,11,12,13&name=snippet_Terminate)]

<span data-ttu-id="5aa3f-148">미들웨어는이 호출 하지 않음으로써 처리 `Invoke` 파이프라인의 다음 미들웨어에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-148">A middleware handles this by not calling `Invoke` on the next middleware in the pipeline.</span></span> <span data-ttu-id="5aa3f-149">이전 middlewares 응답 파이프라인을 통해 다시 때에 호출 될 때문에 완벽 하 게 요청을 종료 하지 않는이 염두에서에 둬야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-149">Keep in mind that this doesn't fully terminate the request, because previous middlewares will still be invoked when the response makes its way back through the pipeline.</span></span>

[!code-csharp[Main](../migration/http-modules/sample/Asp.Net.Core/Middleware/MyTerminatingMiddleware.cs?highlight=7,8&name=snippet_Terminate)]

<span data-ttu-id="5aa3f-150">새 미들웨어를 모듈의 기능을 마이그레이션할 때 때문에 코드가 컴파일되지 않습니다 알 수 있습니다는 `HttpContext` 클래스 ASP.NET Core에서 크게 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-150">When you migrate your module's functionality to your new middleware, you may find that your code doesn't compile because the `HttpContext` class has significantly changed in ASP.NET Core.</span></span> <span data-ttu-id="5aa3f-151">[나중에](#migrating-to-the-new-httpcontext), 새 ASP.NET Core HttpContext를 마이그레이션하는 방법에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-151">[Later on](#migrating-to-the-new-httpcontext), you'll see how to migrate to the new ASP.NET Core HttpContext.</span></span>

## <a name="migrating-module-insertion-into-the-request-pipeline"></a><span data-ttu-id="5aa3f-152">마이그레이션 모듈 삽입 요청 파이프라인</span><span class="sxs-lookup"><span data-stu-id="5aa3f-152">Migrating module insertion into the request pipeline</span></span>

<span data-ttu-id="5aa3f-153">HTTP 모듈은 일반적으로 사용 하 여 요청 파이프라인에 추가 됩니다 *Web.config*:</span><span class="sxs-lookup"><span data-stu-id="5aa3f-153">HTTP modules are typically added to the request pipeline using *Web.config*:</span></span>

[!code-xml[Main](../migration/http-modules/sample/Asp.Net4/Asp.Net4/Web.config?highlight=6&range=1-3,32-33,36,43,50,101)]

<span data-ttu-id="5aa3f-154">이 변환 [새 미들웨어를 추가](xref:fundamentals/middleware/index#creating-a-middleware-pipeline-with-iapplicationbuilder) 요청 파이프라인에 프로그램 `Startup` 클래스:</span><span class="sxs-lookup"><span data-stu-id="5aa3f-154">Convert this by [adding your new middleware](xref:fundamentals/middleware/index#creating-a-middleware-pipeline-with-iapplicationbuilder) to the request pipeline in your `Startup` class:</span></span>

[!code-csharp[Main](../migration/http-modules/sample/Asp.Net.Core/Startup.cs?name=snippet_Configure&highlight=16)]

<span data-ttu-id="5aa3f-155">새 미들웨어를 삽입 하면 파이프라인에서 정확한 지점 모듈로 처리 하는 이벤트에 따라 달라 집니다 (`BeginRequest`, `EndRequest`등)의 모듈 목록에서 해당 순서 및 *Web.config*합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-155">The exact spot in the pipeline where you insert your new middleware depends on the event that it handled as a module (`BeginRequest`, `EndRequest`, etc.) and its order in your list of modules in *Web.config*.</span></span>

<span data-ttu-id="5aa3f-156">이전에 ASP.NET Core에 없는 응용 프로그램 수명 주기는 명시 하는 미들웨어에서 응답을 처리 하는 순서 모듈에 의해 사용 되는 순서와에서 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-156">As previously stated, there's no application life cycle in ASP.NET Core and the order in which responses are processed by middleware differs from the order used by modules.</span></span> <span data-ttu-id="5aa3f-157">이 정렬 결정 좀 더 어렵습니다를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-157">This could make your ordering decision more challenging.</span></span>

<span data-ttu-id="5aa3f-158">순서 지정 문제가 되 면 독립적으로 주문할 수 있습니다. 여러 미들웨어 구성 요소에 모듈을 분할할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-158">If ordering becomes a problem, you could split your module into multiple middleware components that can be ordered independently.</span></span>

## <a name="migrating-handler-code-to-middleware"></a><span data-ttu-id="5aa3f-159">미들웨어 처리기 코드 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="5aa3f-159">Migrating handler code to middleware</span></span>

<span data-ttu-id="5aa3f-160">HTTP 처리기는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-160">An HTTP handler looks something like this:</span></span>

[!code-csharp[Main](../migration/http-modules/sample/Asp.Net4/Asp.Net4/HttpHandlers/ReportHandler.cs?highlight=5,7,13,14,15,16)]

<span data-ttu-id="5aa3f-161">ASP.NET Core 프로젝트에는 번역할이 다음과 유사 하 게 되는 미들웨어:</span><span class="sxs-lookup"><span data-stu-id="5aa3f-161">In your ASP.NET Core project, you would translate this to a middleware similar to this:</span></span>

[!code-csharp[Main](../migration/http-modules/sample/Asp.Net.Core/Middleware/ReportHandlerMiddleware.cs?highlight=7,9,13,20,21,22,23,40,42,44)]

<span data-ttu-id="5aa3f-162">이 미들웨어는 모듈에 해당 하는 미들웨어와 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-162">This middleware is very similar to the middleware corresponding to modules.</span></span> <span data-ttu-id="5aa3f-163">유일한 차이점은 다음과 같습니다에 대 한 호출이 `_next.Invoke(context)`합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-163">The only real difference is that here there's no call to `_next.Invoke(context)`.</span></span> <span data-ttu-id="5aa3f-164">지도록 관점에서 처리기가 요청 파이프라인의 끝에가 있으므로 호출할 다음 미들웨어 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-164">That makes sense, because the handler is at the end of the request pipeline, so there will be no next middleware to invoke.</span></span>

## <a name="migrating-handler-insertion-into-the-request-pipeline"></a><span data-ttu-id="5aa3f-165">마이그레이션 처리기 삽입 요청 파이프라인</span><span class="sxs-lookup"><span data-stu-id="5aa3f-165">Migrating handler insertion into the request pipeline</span></span>

<span data-ttu-id="5aa3f-166">HTTP 처리기 구성 의해 이루어진다는 *Web.config* 다음과 같은 및:</span><span class="sxs-lookup"><span data-stu-id="5aa3f-166">Configuring an HTTP handler is done in *Web.config* and looks something like this:</span></span>

[!code-xml[Main](../migration/http-modules/sample/Asp.Net4/Asp.Net4/Web.config?highlight=6&range=1-3,32,46-48,50,101)]

<span data-ttu-id="5aa3f-167">새 처리기 미들웨어에서 요청 파이프라인에 추가 하 여 변환할 수 있습니다 프로그램 `Startup` 클래스, 모듈에서 변환 하는 미들웨어와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-167">You could convert this by adding your new handler middleware to the request pipeline in your `Startup` class, similar to middleware converted from modules.</span></span> <span data-ttu-id="5aa3f-168">이 방법의 문제 새 처리기 미들웨어에 대 한 모든 요청을 보내는 것과 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-168">The problem with that approach is that it would send all requests to your new handler middleware.</span></span> <span data-ttu-id="5aa3f-169">그러나만 원하는 미들웨어 연결할 지정된 된 확장 프로그램으로 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-169">However, you only want requests with a given extension to reach your middleware.</span></span> <span data-ttu-id="5aa3f-170">HTTP 처리기로 사용 했던 동일한 기능을 가질 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-170">That would give you the same functionality you had with your HTTP handler.</span></span>

<span data-ttu-id="5aa3f-171">한 가지 해결 방법은 지정된 된 확장 프로그램을 사용 하 여 요청에 대 한 파이프라인 분기를 사용 하 여는 `MapWhen` 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-171">One solution is to branch the pipeline for requests with a given extension, using the `MapWhen` extension method.</span></span> <span data-ttu-id="5aa3f-172">이렇게 하면 동일한 `Configure` 다른 미들웨어를 추가 하는 메서드:</span><span class="sxs-lookup"><span data-stu-id="5aa3f-172">You do this in the same `Configure` method where you add the other middleware:</span></span>

[!code-csharp[Main](../migration/http-modules/sample/Asp.Net.Core/Startup.cs?name=snippet_Configure&highlight=27-34)]

<span data-ttu-id="5aa3f-173">`MapWhen`이러한 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-173">`MapWhen` takes these parameters:</span></span>

1. <span data-ttu-id="5aa3f-174">람다는는 `HttpContext` 반환 `true` 여 분기 요청이 전달 해야 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-174">A lambda that takes the `HttpContext` and returns `true` if the request should go down the branch.</span></span> <span data-ttu-id="5aa3f-175">즉, 뿐 아니라 해당 확장명에 있지만 요청 헤더, 쿼리 문자열 매개 변수 등을 따라 요청을 분기할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-175">This means you can branch requests not just based on their extension, but also on request headers, query string parameters, etc.</span></span>

2. <span data-ttu-id="5aa3f-176">사용 하는 람다는 `IApplicationBuilder` 분기에 대 한 모든 미들웨어를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-176">A lambda that takes an `IApplicationBuilder` and adds all the middleware for the branch.</span></span> <span data-ttu-id="5aa3f-177">즉, 처리기 미들웨어 앞에 추가 미들웨어 분기에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-177">This means you can add additional middleware to the branch in front of your handler middleware.</span></span>

<span data-ttu-id="5aa3f-178">분기는 모든 요청;에서 호출 됩니다. 전에 파이프라인에 미들웨어 추가 분기에 영향을 주어 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-178">Middleware added to the pipeline before the branch will be invoked on all requests; the branch will have no impact on them.</span></span>

## <a name="loading-middleware-options-using-the-options-pattern"></a><span data-ttu-id="5aa3f-179">로드 옵션 패턴을 사용 하 여 미들웨어 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-179">Loading middleware options using the options pattern</span></span>

<span data-ttu-id="5aa3f-180">일부 모듈과 처리기에 저장 되어 있는 구성 옵션을 사용할 *Web.config*합니다. 그러나 ASP.NET Core에는 새 구성 모델이 사용 됩니다 대신 *Web.config*합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-180">Some modules and handlers have configuration options that are stored in *Web.config*. However, in ASP.NET Core a new configuration model is used in place of *Web.config*.</span></span>

<span data-ttu-id="5aa3f-181">새 [구성 시스템](xref:fundamentals/configuration/index) 이 문제를 해결 하려면 다음이 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-181">The new [configuration system](xref:fundamentals/configuration/index) gives you these options to solve this:</span></span>

* <span data-ttu-id="5aa3f-182">에 표시 된 대로 미들웨어에 대 한 옵션을 직접 삽입는 [절로](#loading-middleware-options-through-direct-injection)합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-182">Directly inject the options into the middleware, as shown in the [next section](#loading-middleware-options-through-direct-injection).</span></span>

* <span data-ttu-id="5aa3f-183">사용 하 여 [옵션 패턴](xref:fundamentals/configuration/options):</span><span class="sxs-lookup"><span data-stu-id="5aa3f-183">Use the [options pattern](xref:fundamentals/configuration/options):</span></span>

1.  <span data-ttu-id="5aa3f-184">예를 들어 미들웨어 옵션을 저장 하는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-184">Create a class to hold your middleware options, for example:</span></span>

    [!code-csharp[Main](http-modules/sample/Asp.Net.Core/Middleware/MyMiddlewareWithParams.cs?name=snippet_Options)]

2.  <span data-ttu-id="5aa3f-185">옵션 값을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-185">Store the option values</span></span>

    <span data-ttu-id="5aa3f-186">구성 시스템을 사용 하면 옵션 아무 곳 이나 원하는 값을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-186">The configuration system allows you to store option values anywhere you want.</span></span> <span data-ttu-id="5aa3f-187">그러나 사용 하 여 가장 사이트 *appsettings.json*이므로 해당 접근 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-187">However, most sites use *appsettings.json*, so we'll take that approach:</span></span>

    [!code-json[Main](http-modules/sample/Asp.Net.Core/appsettings.json?range=1,14-18)]

    <span data-ttu-id="5aa3f-188">*MyMiddlewareOptionsSection* 섹션 이름에는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-188">*MyMiddlewareOptionsSection* here is a section name.</span></span> <span data-ttu-id="5aa3f-189">옵션 클래스의 이름이 같이 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-189">It doesn't have to be the same as the name of your options class.</span></span>

3. <span data-ttu-id="5aa3f-190">옵션 클래스 옵션 값에 연결</span><span class="sxs-lookup"><span data-stu-id="5aa3f-190">Associate the option values with the options class</span></span>

    <span data-ttu-id="5aa3f-191">옵션 패턴 ASP.NET Core 종속성 주입 프레임 워크를 사용 하 여 연결 옵션의 유형을 (같은 `MyMiddlewareOptions`)와 `MyMiddlewareOptions` 실제 옵션이 있는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-191">The options pattern uses ASP.NET Core's dependency injection framework to associate the options type (such as `MyMiddlewareOptions`) with a `MyMiddlewareOptions` object that has the actual options.</span></span>

    <span data-ttu-id="5aa3f-192">업데이트 프로그램 `Startup` 클래스:</span><span class="sxs-lookup"><span data-stu-id="5aa3f-192">Update your `Startup` class:</span></span>

    1.  <span data-ttu-id="5aa3f-193">사용 중인 경우 *appsettings.json*의 구성 작성기에 추가 `Startup` 생성자:</span><span class="sxs-lookup"><span data-stu-id="5aa3f-193">If you're using *appsettings.json*, add it to the configuration builder in the `Startup` constructor:</span></span>

      [!code-csharp[Main](../migration/http-modules/sample/Asp.Net.Core/Startup.cs?name=snippet_Ctor&highlight=5-6)]

    2.  <span data-ttu-id="5aa3f-194">옵션 서비스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-194">Configure the options service:</span></span>

      [!code-csharp[Main](../migration/http-modules/sample/Asp.Net.Core/Startup.cs?name=snippet_ConfigureServices&highlight=4)]

    3.  <span data-ttu-id="5aa3f-195">옵션 클래스 옵션을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-195">Associate your options with your options class:</span></span>

      [!code-csharp[Main](../migration/http-modules/sample/Asp.Net.Core/Startup.cs?name=snippet_ConfigureServices&highlight=6-8)]

4.  <span data-ttu-id="5aa3f-196">미들웨어 생성자에 대 한 옵션을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-196">Inject the options into your middleware constructor.</span></span> <span data-ttu-id="5aa3f-197">컨트롤러에 대 한 옵션을 삽입 하는 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-197">This is similar to injecting options into a controller.</span></span>

  [!code-csharp[Main](../migration/http-modules/sample/Asp.Net.Core/Middleware/MyMiddlewareWithParams.cs?name=snippet_MiddlewareWithParams&highlight=4,7,10,15-16)]

  <span data-ttu-id="5aa3f-198">[UseMiddleware](#http-modules-usemiddleware) 미들웨어를 추가 하는 확장 메서드는 `IApplicationBuilder` 종속성 주입 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-198">The [UseMiddleware](#http-modules-usemiddleware) extension method that adds your middleware to the `IApplicationBuilder` takes care of dependency injection.</span></span>

  <span data-ttu-id="5aa3f-199">이에 제한 되지 않습니다 `IOptions` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-199">This isn't limited to `IOptions` objects.</span></span> <span data-ttu-id="5aa3f-200">미들웨어 해야 하는 다른 개체에는 이러한 방식으로 삽입 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-200">Any other object that your middleware requires can be injected this way.</span></span>

## <a name="loading-middleware-options-through-direct-injection"></a><span data-ttu-id="5aa3f-201">로드를 통해 직접 삽입 미들웨어 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-201">Loading middleware options through direct injection</span></span>

<span data-ttu-id="5aa3f-202">옵션 패턴에 낮은 옵션 값와 소비자 사이 결합은 생성 되는 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-202">The options pattern has the advantage that it creates loose coupling between options values and their consumers.</span></span> <span data-ttu-id="5aa3f-203">실제 옵션 값에는 옵션 클래스 연결한, 되 면 다른 클래스 종속성 주입 프레임 워크를 통해 옵션에 대 한 액세스를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-203">Once you've associated an options class with the actual options values, any other class can get access to the options through the dependency injection framework.</span></span> <span data-ttu-id="5aa3f-204">옵션 값 전달 않아도가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-204">There's no need to pass around options values.</span></span>

<span data-ttu-id="5aa3f-205">그러면 분할 하지만 여러 가지 옵션을 같은 미들웨어를 두 번 사용 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-205">This breaks down though if you want to use the same middleware twice, with different options.</span></span> <span data-ttu-id="5aa3f-206">예를 들어는 권한 부여 미들웨어 다양 한 역할을 허용 하는 서로 다른 분기에서 사용 되는입니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-206">For example an authorization middleware used in different branches allowing different roles.</span></span> <span data-ttu-id="5aa3f-207">하나의 옵션 클래스와 두 개의 서로 다른 옵션 개체를 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-207">You can't associate two different options objects with the one options class.</span></span>

<span data-ttu-id="5aa3f-208">실제 옵션 값과 옵션 개체를 가져오는 데 솔루션은 프로그램 `Startup` 클래스 미들웨어의 각 인스턴스에 확인란을 직접 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-208">The solution is to get the options objects with the actual options values in your `Startup` class and pass those directly to each instance of your middleware.</span></span>

1.  <span data-ttu-id="5aa3f-209">두 번째 키를 추가 *appsettings.json*</span><span class="sxs-lookup"><span data-stu-id="5aa3f-209">Add a second key to *appsettings.json*</span></span>

    <span data-ttu-id="5aa3f-210">옵션 중 두 번째 집합을 추가 하려면는 *appsettings.json* 파일을 고유 하 게 식별 하는 데 새 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-210">To add a second set of options to the *appsettings.json* file, use a new key to uniquely identify it:</span></span>

    [!code-json[Main](http-modules/sample/Asp.Net.Core/appsettings.json?range=1,10-18&highlight=2-5)]

2.  <span data-ttu-id="5aa3f-211">옵션 값을 검색 하 고 미들웨어에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-211">Retrieve options values and pass them to middleware.</span></span> <span data-ttu-id="5aa3f-212">`Use...` (파이프라인에 미들웨어를 추가)는 확장 메서드는 옵션 값을 전달할 수 있는 논리적 위치:</span><span class="sxs-lookup"><span data-stu-id="5aa3f-212">The `Use...` extension method (which adds your middleware to the pipeline) is a logical place to pass in the option values:</span></span> 

    [!code-csharp[Main](http-modules/sample/Asp.Net.Core/Startup.cs?name=snippet_Configure&highlight=20-23)]

4.  <span data-ttu-id="5aa3f-213">미들웨어 옵션 매개 변수를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-213">Enable middleware to take an options parameter.</span></span> <span data-ttu-id="5aa3f-214">오버 로드를 제공 된 `Use...` 확장 메서드 (옵션 매개 변수를 사용 하 고로 전달 `UseMiddleware`).</span><span class="sxs-lookup"><span data-stu-id="5aa3f-214">Provide an overload of the `Use...` extension method (that takes the options parameter and passes it to `UseMiddleware`).</span></span> <span data-ttu-id="5aa3f-215">때 `UseMiddleware` 라고 매개 변수와 함께 전달 매개 변수 미들웨어 생성자에 미들웨어 개체를 인스턴스화할 때.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-215">When `UseMiddleware` is called with parameters, it passes the parameters to your middleware constructor when it instantiates the middleware object.</span></span>

    [!code-csharp[Main](../migration/http-modules/sample/Asp.Net.Core/Middleware/MyMiddlewareWithParams.cs?name=snippet_Extensions&highlight=9-14)]

    <span data-ttu-id="5aa3f-216">이 옵션 개체에 배치 되는 방법을 확인 프로그램 `OptionsWrapper` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-216">Note how this wraps the options object in an `OptionsWrapper` object.</span></span> <span data-ttu-id="5aa3f-217">이 구현 `IOptions`미들웨어 생성자가 예상 대로, 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-217">This implements `IOptions`, as expected by the middleware constructor.</span></span>

## <a name="migrating-to-the-new-httpcontext"></a><span data-ttu-id="5aa3f-218">새 HttpContext로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="5aa3f-218">Migrating to the new HttpContext</span></span>

<span data-ttu-id="5aa3f-219">앞에서 본 하는 `Invoke` 형식의 매개 변수를 사용 하는 미들웨어에서 메서드 `HttpContext`:</span><span class="sxs-lookup"><span data-stu-id="5aa3f-219">You saw earlier that the `Invoke` method in your middleware takes a parameter of type `HttpContext`:</span></span>

```csharp
public async Task Invoke(HttpContext context)
```

<span data-ttu-id="5aa3f-220">`HttpContext`ASP.NET Core 크게 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-220">`HttpContext` has significantly changed in ASP.NET Core.</span></span> <span data-ttu-id="5aa3f-221">이 섹션에서는의 가장 일반적으로 사용 되는 속성으로 변환 하는 방법을 보여 줍니다. [System.Web.HttpContext](https://docs.microsoft.com/dotnet/api/system.web.httpcontext) 새 `Microsoft.AspNetCore.Http.HttpContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-221">This section shows how to translate the most commonly used properties of [System.Web.HttpContext](https://docs.microsoft.com/dotnet/api/system.web.httpcontext) to the new `Microsoft.AspNetCore.Http.HttpContext`.</span></span>

### <a name="httpcontext"></a><span data-ttu-id="5aa3f-222">HttpContext</span><span class="sxs-lookup"><span data-stu-id="5aa3f-222">HttpContext</span></span>

<span data-ttu-id="5aa3f-223">**HttpContext.Items** 로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-223">**HttpContext.Items** translates to:</span></span>

[!code-csharp[Main](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Items)]

<span data-ttu-id="5aa3f-224">**고유한 요청 ID (System.Web.HttpContext 해당)**</span><span class="sxs-lookup"><span data-stu-id="5aa3f-224">**Unique request ID (no System.Web.HttpContext counterpart)**</span></span>

<span data-ttu-id="5aa3f-225">각 요청에 대 한 고유 id을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-225">Gives you a unique id for each request.</span></span> <span data-ttu-id="5aa3f-226">로그에 포함 하는 데 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-226">Very useful to include in your logs.</span></span>

[!code-csharp[Main](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Trace)]

### <a name="httpcontextrequest"></a><span data-ttu-id="5aa3f-227">HttpContext.Request</span><span class="sxs-lookup"><span data-stu-id="5aa3f-227">HttpContext.Request</span></span>

<span data-ttu-id="5aa3f-228">**HttpContext.Request.HttpMethod** 로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-228">**HttpContext.Request.HttpMethod** translates to:</span></span>

[!code-csharp[Main](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Method)]

<span data-ttu-id="5aa3f-229">**HttpContext.Request.QueryString** 로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-229">**HttpContext.Request.QueryString** translates to:</span></span>

[!code-csharp[Main](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Query)]

<span data-ttu-id="5aa3f-230">**HttpContext.Request.Url** 및 **HttpContext.Request.RawUrl** 로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-230">**HttpContext.Request.Url** and **HttpContext.Request.RawUrl** translate to:</span></span>

[!code-csharp[Main](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Url)]

<span data-ttu-id="5aa3f-231">**HttpContext.Request.IsSecureConnection** 로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-231">**HttpContext.Request.IsSecureConnection** translates to:</span></span>

[!code-csharp[Main](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Secure)]

<span data-ttu-id="5aa3f-232">**HttpContext.Request.UserHostAddress** 로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-232">**HttpContext.Request.UserHostAddress** translates to:</span></span>

[!code-csharp[Main](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Host)]

<span data-ttu-id="5aa3f-233">**HttpContext.Request.Cookies** 로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-233">**HttpContext.Request.Cookies** translates to:</span></span>

[!code-csharp[Main](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Cookies)]

<span data-ttu-id="5aa3f-234">**HttpContext.Request.RequestContext.RouteData** 로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-234">**HttpContext.Request.RequestContext.RouteData** translates to:</span></span>

[!code-csharp[Main](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Route)]

<span data-ttu-id="5aa3f-235">**HttpContext.Request.Headers** 로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-235">**HttpContext.Request.Headers** translates to:</span></span>

[!code-csharp[Main](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Headers)]

<span data-ttu-id="5aa3f-236">**HttpContext.Request.UserAgent** 로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-236">**HttpContext.Request.UserAgent** translates to:</span></span>

[!code-csharp[Main](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Agent)]

<span data-ttu-id="5aa3f-237">**HttpContext.Request.UrlReferrer** 로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-237">**HttpContext.Request.UrlReferrer** translates to:</span></span>

[!code-csharp[Main](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Referrer)]

<span data-ttu-id="5aa3f-238">**HttpContext.Request.ContentType** 로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-238">**HttpContext.Request.ContentType** translates to:</span></span>

[!code-csharp[Main](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Type)]

<span data-ttu-id="5aa3f-239">**HttpContext.Request.Form** 로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-239">**HttpContext.Request.Form** translates to:</span></span>

[!code-csharp[Main](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Form)]

> [!WARNING]
> <span data-ttu-id="5aa3f-240">콘텐츠 하위 형식이 경우 양식 값을 읽기 *x-www-형식-urlencoded* 또는 *양식 데이터*합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-240">Read form values only if the content sub type is *x-www-form-urlencoded* or *form-data*.</span></span>

<span data-ttu-id="5aa3f-241">**HttpContext.Request.InputStream** 로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-241">**HttpContext.Request.InputStream** translates to:</span></span>

[!code-csharp[Main](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Input)]

> [!WARNING]
> <span data-ttu-id="5aa3f-242">이 코드는 파이프라인의 끝에 처리기 형식 미들웨어, 에서만 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-242">Use this code only in a handler type middleware, at the end of a pipeline.</span></span>
>
><span data-ttu-id="5aa3f-243">요청당 한 번만 위와 같이 원시 본문을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-243">You can read the raw body as shown above only once per request.</span></span> <span data-ttu-id="5aa3f-244">미들웨어를 첫 번째 읽기 후 본문을 읽는 동안에 빈 본문이 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-244">Middleware trying to read the body after the first read will read an empty body.</span></span>
>
><span data-ttu-id="5aa3f-245">이 버퍼에서 수행 되기 때문에 앞에서 표시 된 것 처럼 폼 읽는 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-245">This doesn't apply to reading a form as shown earlier, because that's done from a buffer.</span></span>

### <a name="httpcontextresponse"></a><span data-ttu-id="5aa3f-246">HttpContext.Response</span><span class="sxs-lookup"><span data-stu-id="5aa3f-246">HttpContext.Response</span></span>

<span data-ttu-id="5aa3f-247">**HttpContext.Response.Status** 및 **HttpContext.Response.StatusDescription** 로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-247">**HttpContext.Response.Status** and **HttpContext.Response.StatusDescription** translate to:</span></span>

[!code-csharp[Main](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Status)]

<span data-ttu-id="5aa3f-248">**HttpContext.Response.ContentEncoding** 및 **HttpContext.Response.ContentType** 로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-248">**HttpContext.Response.ContentEncoding** and **HttpContext.Response.ContentType** translate to:</span></span>

[!code-csharp[Main](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_RespType)]

<span data-ttu-id="5aa3f-249">**HttpContext.Response.ContentType** 에 자체도로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-249">**HttpContext.Response.ContentType** on its own also translates to:</span></span>

[!code-csharp[Main](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_RespTypeOnly)]

<span data-ttu-id="5aa3f-250">**HttpContext.Response.Output** 로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-250">**HttpContext.Response.Output** translates to:</span></span>

[!code-csharp[Main](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Output)]

<span data-ttu-id="5aa3f-251">**HttpContext.Response.TransmitFile**</span><span class="sxs-lookup"><span data-stu-id="5aa3f-251">**HttpContext.Response.TransmitFile**</span></span>

<span data-ttu-id="5aa3f-252">파일을 서비스 설명 [여기](../fundamentals/request-features.md#middleware-and-request-features)합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-252">Serving up a file is discussed [here](../fundamentals/request-features.md#middleware-and-request-features).</span></span>

<span data-ttu-id="5aa3f-253">**HttpContext.Response.Headers**</span><span class="sxs-lookup"><span data-stu-id="5aa3f-253">**HttpContext.Response.Headers**</span></span>

<span data-ttu-id="5aa3f-254">때문에 복잡는 보내는 응답 헤더를 설정할 경우 응답 본문에 아무 것도 기록 된 후은 전송 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-254">Sending response headers is complicated by the fact that if you set them after anything has been written to the response body, they will not be sent.</span></span>

<span data-ttu-id="5aa3f-255">솔루션 응답 시작에 쓰기 전에 오른쪽 호출 될 콜백 메서드를 설정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-255">The solution is to set a callback method that will be called right before writing to the response starts.</span></span> <span data-ttu-id="5aa3f-256">시작 부분에 가장 잘 이렇게는 `Invoke` 미들웨어에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-256">This is best done at the start of the `Invoke` method in your middleware.</span></span> <span data-ttu-id="5aa3f-257">응답 헤더를 설정 하는이 콜백 메서드는</span><span class="sxs-lookup"><span data-stu-id="5aa3f-257">It's this callback method that sets your response headers.</span></span>

<span data-ttu-id="5aa3f-258">다음 코드에서는 호출 하는 콜백 메서드 설정 `SetHeaders`:</span><span class="sxs-lookup"><span data-stu-id="5aa3f-258">The following code sets a callback method called `SetHeaders`:</span></span>

```csharp
public async Task Invoke(HttpContext httpContext)
{
    // ...
    httpContext.Response.OnStarting(SetHeaders, state: httpContext);
```

<span data-ttu-id="5aa3f-259">`SetHeaders` 콜백 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-259">The `SetHeaders` callback method would look like this:</span></span>

[!code-csharp[Main](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_SetHeaders)]

<span data-ttu-id="5aa3f-260">**HttpContext.Response.Cookies**</span><span class="sxs-lookup"><span data-stu-id="5aa3f-260">**HttpContext.Response.Cookies**</span></span>

<span data-ttu-id="5aa3f-261">브라우저에서 쿠키 여행는 *Set-cookie* 응답 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-261">Cookies travel to the browser in a *Set-Cookie* response header.</span></span> <span data-ttu-id="5aa3f-262">결과적으로, 쿠키 보내기를 응답 헤더를 보내는 데 사용 된 것과 동일한 콜백 함수가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-262">As a result, sending cookies requires the same callback as used for sending response headers:</span></span>

```csharp
public async Task Invoke(HttpContext httpContext)
{
    // ...
    httpContext.Response.OnStarting(SetCookies, state: httpContext);
    httpContext.Response.OnStarting(SetHeaders, state: httpContext);
```

<span data-ttu-id="5aa3f-263">`SetCookies` 콜백 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5aa3f-263">The `SetCookies` callback method would look like the following:</span></span>

[!code-csharp[Main](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_SetCookies)]

## <a name="additional-resources"></a><span data-ttu-id="5aa3f-264">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5aa3f-264">Additional resources</span></span>

* [<span data-ttu-id="5aa3f-265">HTTP 처리기 및 HTTP 모듈 개요</span><span class="sxs-lookup"><span data-stu-id="5aa3f-265">HTTP Handlers and HTTP Modules Overview</span></span>](/iis/configuration/system.webserver/)
* [<span data-ttu-id="5aa3f-266">구성</span><span class="sxs-lookup"><span data-stu-id="5aa3f-266">Configuration</span></span>](xref:fundamentals/configuration/index)
* [<span data-ttu-id="5aa3f-267">응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="5aa3f-267">Application Startup</span></span>](xref:fundamentals/startup)
* [<span data-ttu-id="5aa3f-268">미들웨어</span><span class="sxs-lookup"><span data-stu-id="5aa3f-268">Middleware</span></span>](xref:fundamentals/middleware/index)
