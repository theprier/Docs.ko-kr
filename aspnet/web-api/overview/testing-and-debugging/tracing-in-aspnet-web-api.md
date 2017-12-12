---
uid: web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
title: "ASP.NET Web API 2의에서 추적 | Microsoft Docs"
author: MikeWasson
description: "ASP.NET Web API에서 추적을 설정 하는 방법을 보여 줍니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/25/2014
ms.topic: article
ms.assetid: 66a837e9-600b-4b72-97a9-19804231c64a
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: f35c8a10018ce796e2d905d6ee839ff09bb380a1
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="tracing-in-aspnet-web-api-2"></a><span data-ttu-id="852a7-103">ASP.NET Web API 2의 추적</span><span class="sxs-lookup"><span data-stu-id="852a7-103">Tracing in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="852a7-104">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="852a7-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="852a7-105">웹 기반 응용 프로그램을 디버깅 하려고 시도할 때 좋은 집합 추적 로그에 대 한 조치에는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-105">When you are trying to debug a web-based application, there is no substitute for a good set of trace logs.</span></span> <span data-ttu-id="852a7-106">이 자습서에는 ASP.NET Web API에서 추적을 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-106">This tutorial shows how to enable tracing in ASP.NET Web API.</span></span> <span data-ttu-id="852a7-107">Web API 프레임 워크 수행 하는 작업 전후의 컨트롤러를 호출 하기 전에 추적 하려면이 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-107">You can use this feature to trace what the Web API framework does before and after it invokes your controller.</span></span> <span data-ttu-id="852a7-108">사용자 고유의 코드를 추적에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-108">You can also use it to trace your own code.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="852a7-109">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="852a7-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="852a7-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/) (Visual Studio 2015와 함께 작동)</span><span class="sxs-lookup"><span data-stu-id="852a7-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/) (also works with Visual Studio 2015)</span></span>
> - <span data-ttu-id="852a7-111">Web API 2</span><span class="sxs-lookup"><span data-stu-id="852a7-111">Web API 2</span></span>
> - [<span data-ttu-id="852a7-112">Microsoft.AspNet.WebApi.Tracing</span><span class="sxs-lookup"><span data-stu-id="852a7-112">Microsoft.AspNet.WebApi.Tracing</span></span>](http://www.nuget.org/packages/Microsoft.AspNet.WebApi.Tracing)


## <a name="enable-systemdiagnostics-tracing-in-web-api"></a><span data-ttu-id="852a7-113">System.Diagnostics Web API에서에서 추적을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="852a7-113">Enable System.Diagnostics Tracing in Web API</span></span>

<span data-ttu-id="852a7-114">첫째, 새 ASP.NET 웹 응용 프로그램 프로젝트를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-114">First, we'll create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="852a7-115">Visual Studio에서에서 **파일** 메뉴 선택 **새로**, 다음 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-115">In Visual Studio, from the **File** menu, select **New**, then **Project**.</span></span> <span data-ttu-id="852a7-116">아래 **템플릿**, **웹**선택, **ASP.NET 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-116">Under **Templates**, **Web**, select **ASP.NET Web Application**.</span></span>

[![](tracing-in-aspnet-web-api/_static/image2.png)](tracing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="852a7-117">웹 API 프로젝트 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-117">Choose the Web API project template.</span></span>

[![](tracing-in-aspnet-web-api/_static/image4.png)](tracing-in-aspnet-web-api/_static/image3.png)

<span data-ttu-id="852a7-118">**도구** 메뉴 선택 **라이브러리 패키지 관리자**, 다음 **패키지 관리 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-118">From the **Tools** menu, select **Library Package Manager**, then **Package Manage Console**.</span></span>

<span data-ttu-id="852a7-119">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-119">In the Package Manager Console window, type the following commands.</span></span>

[!code-console[Main](tracing-in-aspnet-web-api/samples/sample1.cmd)]

<span data-ttu-id="852a7-120">첫 번째 명령은 최신 웹 API 추적 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-120">The first command installs the latest Web API tracing package.</span></span> <span data-ttu-id="852a7-121">또한 핵심 웹 API 패키지를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-121">It also updates the core Web API packages.</span></span> <span data-ttu-id="852a7-122">두 번째 명령은 WebApi.WebHost 패키지를 최신 버전으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-122">The second command updates the WebApi.WebHost package to the latest version.</span></span>

> [!NOTE]
> <span data-ttu-id="852a7-123">사용 하 여 Web API의 특정 버전을 대상으로 하려는 경우 추적 패키지를 설치할 때-버전 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-123">If you want to target a specific version of Web API, use the -Version flag when you install the tracing package.</span></span>


<span data-ttu-id="852a7-124">응용 프로그램에서 WebApiConfig.cs 파일을 열고\_시작 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-124">Open the file WebApiConfig.cs in the App\_Start folder.</span></span> <span data-ttu-id="852a7-125">다음 코드를 추가 하는 **등록** 메서드.</span><span class="sxs-lookup"><span data-stu-id="852a7-125">Add the following code to the **Register** method.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample2.cs?highlight=6)]

<span data-ttu-id="852a7-126">이 코드는 추가 [SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/en-us/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) Web API 파이프라인에는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-126">This code adds the [SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/en-us/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) class to the Web API pipeline.</span></span> <span data-ttu-id="852a7-127">**SystemDiagnosticsTraceWriter** 클래스에 추적 정보를 기록 [System.Diagnostics.Trace](https://msdn.microsoft.com/en-us/library/system.diagnostics.trace)합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-127">The **SystemDiagnosticsTraceWriter** class writes traces to [System.Diagnostics.Trace](https://msdn.microsoft.com/en-us/library/system.diagnostics.trace).</span></span>

<span data-ttu-id="852a7-128">추적을 보려면 디버거에서 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-128">To see the traces, run the application in the debugger.</span></span> <span data-ttu-id="852a7-129">브라우저에서로 이동 `/api/values`합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-129">In the browser, navigate to `/api/values`.</span></span>

![](tracing-in-aspnet-web-api/_static/image5.png)

<span data-ttu-id="852a7-130">Trace 문은 Visual Studio의 출력 창에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-130">The trace statements are written to the Output window in Visual Studio.</span></span> <span data-ttu-id="852a7-131">(에서 **보기** 메뉴 선택 **출력**).</span><span class="sxs-lookup"><span data-stu-id="852a7-131">(From the **View** menu, select **Output**).</span></span>

[![](tracing-in-aspnet-web-api/_static/image7.png)](tracing-in-aspnet-web-api/_static/image6.png)

<span data-ttu-id="852a7-132">때문에 **SystemDiagnosticsTraceWriter** 에 추적 정보를 기록 **System.Diagnostics.Trace**, 추가 추적 수신기를 등록할 수 있습니다; 예를 들어 쓸 추적 로그 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-132">Because **SystemDiagnosticsTraceWriter** writes traces to **System.Diagnostics.Trace**, you can register additional trace listeners; for example, to write traces to a log file.</span></span> <span data-ttu-id="852a7-133">추적 기록기에 대 한 자세한 내용은 참조는 [추적 수신기](https://msdn.microsoft.com/en-us/library/4y5y10s7.aspx) MSDN 항목.</span><span class="sxs-lookup"><span data-stu-id="852a7-133">For more information about trace writers, see the [Trace Listeners](https://msdn.microsoft.com/en-us/library/4y5y10s7.aspx) topic on MSDN.</span></span>

### <a name="configuring-systemdiagnosticstracewriter"></a><span data-ttu-id="852a7-134">SystemDiagnosticsTraceWriter를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-134">Configuring SystemDiagnosticsTraceWriter</span></span>

<span data-ttu-id="852a7-135">다음 코드에 추적 작성기를 구성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-135">The following code shows how to configure the trace writer.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="852a7-136">제어할 수 있는 두 가지 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-136">There are two settings that you can control:</span></span>

- <span data-ttu-id="852a7-137">IsVerbose: false 인 경우, 각 추적 최소한의 정보만을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-137">IsVerbose: If false, each trace contains minimal information.</span></span> <span data-ttu-id="852a7-138">True 이면 추적 추가 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-138">If true, traces include more information.</span></span>
- <span data-ttu-id="852a7-139">MinimumLevel: 최소 추적 수준을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-139">MinimumLevel: Sets the minimum trace level.</span></span> <span data-ttu-id="852a7-140">추적 수준을 순서, 디버그, 정보, 경고, 오류 및 치명적 됩니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-140">Trace levels, in order, are Debug, Info, Warn, Error, and Fatal.</span></span>

## <a name="adding-traces-to-your-web-api-application"></a><span data-ttu-id="852a7-141">Web API 응용 프로그램에 추적 추가</span><span class="sxs-lookup"><span data-stu-id="852a7-141">Adding Traces to Your Web API Application</span></span>

<span data-ttu-id="852a7-142">추가 추적 작성기에 액세스할 수 즉시 Web API 파이프라인 하 여 만든 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-142">Adding a trace writer gives you immediate access to the traces created by the Web API pipeline.</span></span> <span data-ttu-id="852a7-143">또한 사용자 고유의 코드를 추적 하려면 추적 기록기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-143">You can also use the trace writer to trace your own code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="852a7-144">추적 기록기를 얻기 위해 호출 **HttpConfiguration.Services.GetTraceWriter**합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-144">To get the trace writer, call **HttpConfiguration.Services.GetTraceWriter**.</span></span> <span data-ttu-id="852a7-145">이 메서드는 컨트롤러에서를 통해 액세스할 수는 **ApiController.Configuration** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-145">From a controller, this method is accessible through the **ApiController.Configuration** property.</span></span>

<span data-ttu-id="852a7-146">추적을 작성 하기 위해 호출할 수 있습니다는 **ITraceWriter.Trace** 메서드를 직접 되지만 [ITraceWriterExtensions](https://msdn.microsoft.com/en-us/library/system.web.http.tracing.itracewriterextensions.aspx) 클래스 더 친숙 한 있는 몇 가지 확장 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-146">To write a trace, you can call the **ITraceWriter.Trace** method directly, but the [ITraceWriterExtensions](https://msdn.microsoft.com/en-us/library/system.web.http.tracing.itracewriterextensions.aspx) class defines some extension methods that are more friendly.</span></span> <span data-ttu-id="852a7-147">예를 들어는 **정보** 메서드 위에 표시 된 추적 수준으로 추적을 만들 **정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-147">For example, the **Info** method shown above creates a trace with trace level **Info**.</span></span>

## <a name="web-api-tracing-infrastructure"></a><span data-ttu-id="852a7-148">Web API 추적 인프라</span><span class="sxs-lookup"><span data-stu-id="852a7-148">Web API Tracing Infrastructure</span></span>

<span data-ttu-id="852a7-149">이 섹션에서는 웹 API에 대 한 사용자 지정 추적 기록기를 작성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-149">This section describes how to write a custom trace writer for Web API.</span></span>

<span data-ttu-id="852a7-150">Microsoft.AspNet.WebApi.Tracing 패키지는 Web API에서 보다 일반적인 추적 인프라를 기반으로 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-150">The Microsoft.AspNet.WebApi.Tracing package is built on top of a more general tracing infrastructure in Web API.</span></span> <span data-ttu-id="852a7-151">Microsoft.AspNet.WebApi.Tracing를 사용 하지 않고 또한 연결 하 여 일부 다른 추적/로깅을 해제 라이브러리와 같은 [NLog](http://nlog-project.org/) 또는 [log4net](http://logging.apache.org/log4net/)합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-151">Instead of using Microsoft.AspNet.WebApi.Tracing, you can also plug in some other tracing/loggin library, such as [NLog](http://nlog-project.org/) or [log4net](http://logging.apache.org/log4net/).</span></span>

<span data-ttu-id="852a7-152">추적을 수집 하려면 구현 된 **ITraceWriter** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-152">To collect traces, implement the **ITraceWriter** interface.</span></span> <span data-ttu-id="852a7-153">간단한 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-153">Here is a simple example:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="852a7-154">**ITraceWriter.Trace** 메서드 추적을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-154">The **ITraceWriter.Trace** method creates a trace.</span></span> <span data-ttu-id="852a7-155">호출자에는 범주와 추적 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-155">The caller specifies a category and trace level.</span></span> <span data-ttu-id="852a7-156">범주에는 모든 사용자 정의 문자열일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-156">The category can be any user-defined string.</span></span> <span data-ttu-id="852a7-157">구현 **추적** 에서 다음을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-157">Your implementation of **Trace** should do the following:</span></span>

1. <span data-ttu-id="852a7-158">새 **TraceRecord**합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-158">Create a new **TraceRecord**.</span></span> <span data-ttu-id="852a7-159">표시 된 것 처럼 요청, 범주 및 추적 수준으로 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-159">Initialize it with the request, category, and trace level, as shown.</span></span> <span data-ttu-id="852a7-160">이러한 값은 호출자에 의해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-160">These values are provided by the caller.</span></span>
2. <span data-ttu-id="852a7-161">호출 된 *traceAction* 위임 합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-161">Invoke the *traceAction* delegate.</span></span> <span data-ttu-id="852a7-162">이 대리자 내 호출자의 나머지를 작성 하는 **TraceRecord**합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-162">Inside this delegate, the caller is expected to fill in the rest of the **TraceRecord**.</span></span>
3. <span data-ttu-id="852a7-163">쓰기는 **TraceRecord**, 사람에 해당 하는 로깅 기법을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-163">Write the **TraceRecord**, using any logging technique that you like.</span></span> <span data-ttu-id="852a7-164">이 예제를 단순히 호출 **System.Diagnostics.Trace**합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-164">The example shown here simply calls into **System.Diagnostics.Trace**.</span></span>

## <a name="setting-the-trace-writer"></a><span data-ttu-id="852a7-165">추적 기록기를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-165">Setting the Trace Writer</span></span>

<span data-ttu-id="852a7-166">추적을 사용 하려면 웹 API를 사용 하도록 구성 해야 프로그램 **ITraceWriter** 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-166">To enable tracing, you must configure Web API to use your **ITraceWriter** implementation.</span></span> <span data-ttu-id="852a7-167">통해이 작업은 **HttpConfiguration** 다음 코드와 같이 개체:</span><span class="sxs-lookup"><span data-stu-id="852a7-167">You do this through the **HttpConfiguration** object, as shown in the following code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="852a7-168">하나의 추적 기록기를 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-168">Only one trace writer can be active.</span></span> <span data-ttu-id="852a7-169">기본적으로 웹 API 설정는 &quot;아무&quot; 는 아무 작업도 수행 하는 추적 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-169">By default, Web API sets a &quot;no-op&quot; tracer that does nothing.</span></span> <span data-ttu-id="852a7-170">(의 &quot;아무&quot; 추적 프로그램 존재 추적 코드에서 추적 작성기 인지 확인 하지 않도록 **null** 추적을 작성 하기 전에.)</span><span class="sxs-lookup"><span data-stu-id="852a7-170">(The &quot;no-op&quot; tracer exists so that tracing code does not have to check whether the trace writer is **null** before writing a trace.)</span></span>

## <a name="how-web-api-tracing-works"></a><span data-ttu-id="852a7-171">API 추적 작동 방법 웹</span><span class="sxs-lookup"><span data-stu-id="852a7-171">How Web API Tracing Works</span></span>

<span data-ttu-id="852a7-172">웹 API 사용에 웹 API를 사용 하 여 추적 한 *외관* 패턴: Web API 추적을 사용 하는 경우 추적 호출을 수행 하는 클래스와 함께 요청 파이프라인의 다양 한 부분을 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-172">Tracing in Web API uses a in Web API uses a *facade* pattern: When tracing is enabled, Web API wraps various parts of the request pipeline with classes that perform trace calls.</span></span>

<span data-ttu-id="852a7-173">예를 들어 컨트롤러를 선택 하면 파이프라인 사용 하 여는 **IHttpControllerSelector** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-173">For example, when selecting a controller, the pipeline uses the **IHttpControllerSelector** interface.</span></span> <span data-ttu-id="852a7-174">사용 하도록 설정 하는 추적을 구현 하는 클래스는 pipleline 삽입 **IHttpControllerSelector** 하지만 실제 구현에 통해 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-174">With tracing enabled, the pipleline inserts a class that implements **IHttpControllerSelector** but calls through to the real implementation:</span></span>

![Web API 추적 외관 패턴을 사용 합니다.](tracing-in-aspnet-web-api/_static/image8.png)

<span data-ttu-id="852a7-176">이 디자인의 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-176">The benefits of this design include:</span></span>

- <span data-ttu-id="852a7-177">추적 기록기를 추가 하지 않으면 추적 구성 요소는 인스턴스화되지 않으며 성능 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-177">If you do not add a trace writer, the tracing components are not instantiated and have no performance impact.</span></span>
- <span data-ttu-id="852a7-178">와 같은 기본 서비스를 대체 하는 경우 **IHttpControllerSelector** 사용자 사용자 지정 구현으로 추적에 영향을 주지 추적 래퍼 개체에 의해 수행 되기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-178">If you replace default services such as **IHttpControllerSelector** with your own custom implementation, tracing is not affected, because tracing is done by the wrapper object.</span></span>

<span data-ttu-id="852a7-179">기본 대체 하 여 사용자 고유의 사용자 지정 framework를 사용 하는 전체 웹 API 추적 프레임 워크를 바꿀 수도 있습니다 **ITraceManager** 서비스:</span><span class="sxs-lookup"><span data-stu-id="852a7-179">You can also replace the entire Web API trace framework with your own custom framework, by replacing the default **ITraceManager** service:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="852a7-180">구현 **ITraceManager.Initialize** 추적 시스템을 초기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-180">Implement **ITraceManager.Initialize** to initialize your tracing system.</span></span> <span data-ttu-id="852a7-181">이 대체 유의 *전체* 추적 프레임 워크, 웹 API에 포함 된 추적 코드를 모두 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="852a7-181">Be aware that this replaces the *entire* trace framework, including all of the tracing code that is built into Web API.</span></span>
