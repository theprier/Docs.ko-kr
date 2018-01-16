---
title: "ASP.NET Core에 로그인"
author: ardalis
description: "ASP.NET Core의 로깅 프레임워크에 대해 알아봅니다. 기본 제공 로깅 공급자를 살펴보고 인기 있는 타사 공급자에 대해 알아봅니다."
keywords: "ASP.NET Core,로깅,로깅 공급자,Microsoft.Extensions.Logging,ILogger,ILoggerFactory,LogLevel,WithFilter,TraceSource,EventLog,EventSource,범위"
ms.author: tdykstra
manager: wpickett
ms.date: 12/15/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/logging/index
ms.openlocfilehash: 3eb167c961b8d089d508ef5622db6ae1cdd99088
ms.sourcegitcommit: 12e5194936b7e820efc5505a2d5d4f84e88eb5ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/11/2018
---
# <a name="introduction-to-logging-in-aspnet-core"></a><span data-ttu-id="9768d-105">ASP.NET Core에 로그인 소개</span><span class="sxs-lookup"><span data-stu-id="9768d-105">Introduction to logging in ASP.NET Core</span></span>

<span data-ttu-id="9768d-106">작성자: [Steve Smith](https://ardalis.com/) 및 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="9768d-106">By [Steve Smith](https://ardalis.com/) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="9768d-107">ASP.NET Core는 다양한 로깅 공급자를 사용하는 로깅 API를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-107">ASP.NET Core supports a logging API that works with a variety of logging providers.</span></span> <span data-ttu-id="9768d-108">기본 공급자를 통해 하나 이상의 대상에 로그를 보낼 수 있으며, 타사 로깅 프레임워크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-108">Built-in providers let you send logs to one or more destinations, and you can plug in a third-party logging framework.</span></span> <span data-ttu-id="9768d-109">이 문서에서는 코드에 기본 제공 로깅 API 및 공급자를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-109">This article shows how to use the built-in logging API and providers in your code.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9768d-110">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9768d-110">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="9768d-111">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/index/sample2)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="9768d-111">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/index/sample2) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9768d-112">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9768d-112">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="9768d-113">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/index/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="9768d-113">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/index/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

---

## <a name="how-to-create-logs"></a><span data-ttu-id="9768d-114">로그를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="9768d-114">How to create logs</span></span>

<span data-ttu-id="9768d-115">로그를 만들려면 [종속성 주입](xref:fundamentals/dependency-injection) 컨테이너에서 `ILogger` 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-115">To create logs, get an `ILogger` object from the [dependency injection](xref:fundamentals/dependency-injection) container:</span></span>

[!code-csharp[](index/sample/Controllers/TodoController.cs?name=snippet_LoggerDI&highlight=7)]

<span data-ttu-id="9768d-116">그런 다음 해당 로거 개체에 대해 로깅 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-116">Then call logging methods on that logger object:</span></span>

[!code-csharp[](index/sample/Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

<span data-ttu-id="9768d-117">이 예에서는 *범주*로 `TodoController` 클래스를 사용하여 로그를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-117">This example creates logs with the `TodoController` class as the *category*.</span></span> <span data-ttu-id="9768d-118">범주는 [이 문서의 뒷부분](#log-category)에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-118">Categories are explained [later in this article](#log-category).</span></span>

<span data-ttu-id="9768d-119">ASP.NET Core는 비동기 로거 메서드를 제공하지 않습니다. 비동기를 사용할 필요가 없도록 로깅 속도가 아주 빠르기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-119">ASP.NET Core does not provide async logger methods because logging should be so fast that it isn't worth the cost of using async.</span></span> <span data-ttu-id="9768d-120">로깅 속도가 빠르지 않은 경우 로깅 방식을 변경하는 방안을 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="9768d-120">If you're in a situation where that's not true, consider changing the way you log.</span></span> <span data-ttu-id="9768d-121">데이터 저장소가 느리면 로그 메시지를 빠른 저장소에 먼저 쓴 후 나중에 느린 저장소로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-121">If your data store is slow, write the log messages to a fast store first, then move them to a slow store later.</span></span> <span data-ttu-id="9768d-122">예를 들어 다른 프로세스에서 읽고 지속하는 느린 저장소인 메시지 큐에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-122">For example, log to a message queue that is read and persisted to slow storage by another process.</span></span>

## <a name="how-to-add-providers"></a><span data-ttu-id="9768d-123">공급자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="9768d-123">How to add providers</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9768d-124">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9768d-124">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="9768d-125">로깅 공급자는 개발자가 `ILogger` 개체를 사용하여 만든 메시지를 가져와서 표시하거나 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-125">A logging provider takes the messages that you create with an `ILogger` object and displays or stores them.</span></span> <span data-ttu-id="9768d-126">예를 들어 콘솔 공급자는 콘솔에 메시지를 표시하고, Azure App Service 공급자는 메시지를 Azure BLOB 저장소에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-126">For example, the Console provider displays messages on the console, and the Azure App Service provider can store them in Azure blob storage.</span></span>

<span data-ttu-id="9768d-127">공급자를 사용하려면 *Program.cs*에서 공급자의 `Add<ProviderName>` 확장 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-127">To use a provider, call the provider's `Add<ProviderName>` extension method in *Program.cs*:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_ExpandDefault&highlight=16,17)]

<span data-ttu-id="9768d-128">기본 프로젝트 템플릿을 사용하면 [CreateDefaultBuilder](https://docs.microsoft.com/ dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder?view=aspnetcore-2.0#Microsoft_AspNetCore_WebHost_CreateDefaultBuilder_System_String___) 메서드를 사용하여 로깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-128">The default project template enables logging with the [CreateDefaultBuilder](https://docs.microsoft.com/ dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder?view=aspnetcore-2.0#Microsoft_AspNetCore_WebHost_CreateDefaultBuilder_System_String___) method:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_TemplateCode&highlight=7)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9768d-129">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9768d-129">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="9768d-130">로깅 공급자는 개발자가 `ILogger` 개체를 사용하여 만든 메시지를 가져와서 표시하거나 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-130">A logging provider takes the messages that you create with an `ILogger` object and displays or stores them.</span></span> <span data-ttu-id="9768d-131">예를 들어 콘솔 공급자는 콘솔에 메시지를 표시하고, Azure App Service 공급자는 메시지를 Azure BLOB 저장소에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-131">For example, the Console provider displays messages on the console, and the Azure App Service provider can store them in Azure blob storage.</span></span>

<span data-ttu-id="9768d-132">공급자를 사용하려면 다음 예제처럼 NuGet 패키지를 설치하고 `ILoggerFactory` 인스턴스에 대한 공급자의 확장 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-132">To use a provider, install its NuGet package and call the provider's extension method on an instance of `ILoggerFactory`, as shown in the following example.</span></span>

[!code-csharp[](index/sample//Startup.cs?name=snippet_AddConsoleAndDebug&highlight=3,5-7)]

<span data-ttu-id="9768d-133">ASP.NET Core [DI(종속성 주입](xref:fundamentals/dependency-injection))는 `ILoggerFactory` 인스턴스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-133">ASP.NET Core [dependency injection](xref:fundamentals/dependency-injection) (DI) provides the `ILoggerFactory` instance.</span></span> <span data-ttu-id="9768d-134">`AddConsole` 및 `AddDebug` 확장 메서드는 [Microsoft.Extensions.Logging.Console](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Console/) 및 [Microsoft.Extensions.Logging.Debug](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Debug/) 패키지에 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-134">The `AddConsole` and `AddDebug` extension methods are defined in the [Microsoft.Extensions.Logging.Console](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Console/) and [Microsoft.Extensions.Logging.Debug](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Debug/) packages.</span></span> <span data-ttu-id="9768d-135">각 확장 메서드는 `ILoggerFactory.AddProvider` 메서드를 호출하고, 공급자 인스턴스를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-135">Each extension method calls the `ILoggerFactory.AddProvider` method, passing in an instance of the provider.</span></span> 

> [!NOTE]
> <span data-ttu-id="9768d-136">이 문서의 응용 프로그램 예제에서는 `Startup` 클래스의 `Configure` 메서드에 로깅을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-136">The sample application for this article adds logging providers in the `Configure` method of the `Startup` class.</span></span> <span data-ttu-id="9768d-137">먼저 실행되는 코드의 로그 출력을 가져오려면, 그 대신 `Startup` 클래스 생성자에서 로깅 공급자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-137">If you want to get log output from code that executes earlier, add logging providers in the `Startup` class constructor instead.</span></span> 

---

<span data-ttu-id="9768d-138">각 [기본 제공 로깅 공급자](#built-in-logging-providers)에 대한 정보와 [타사 로깅 공급자](#third-party-logging-providers)의 링크는 문서의 뒷부분에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-138">You'll find information about each [built-in logging provider](#built-in-logging-providers) and links to [third-party logging providers](#third-party-logging-providers) later in the article.</span></span>

## <a name="sample-logging-output"></a><span data-ttu-id="9768d-139">샘플 로깅 출력</span><span class="sxs-lookup"><span data-stu-id="9768d-139">Sample logging output</span></span>

<span data-ttu-id="9768d-140">이전 섹션에 나와 있는 샘플 코드를 사용하는 경우 명령줄에서 실행하면 콘솔에 로그가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-140">With the sample code shown in the preceding section, you'll see logs in the console when you run from the command line.</span></span> <span data-ttu-id="9768d-141">다음은 콘솔 출력의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-141">Here's an example of console output:</span></span>

```console
info: Microsoft.AspNetCore.Hosting.Internal.WebHost[1]
      Request starting HTTP/1.1 GET http://localhost:5000/api/todo/0
info: Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker[1]
      Executing action method TodoApi.Controllers.TodoController.GetById (TodoApi) with arguments (0) - ModelState is Valid
info: TodoApi.Controllers.TodoController[1002]
      Getting item 0
warn: TodoApi.Controllers.TodoController[4000]
      GetById(0) NOT FOUND
info: Microsoft.AspNetCore.Mvc.StatusCodeResult[1]
      Executing HttpStatusCodeResult, setting HTTP status code 404
info: Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker[2]
      Executed action TodoApi.Controllers.TodoController.GetById (TodoApi) in 42.9286ms
info: Microsoft.AspNetCore.Hosting.Internal.WebHost[2]
      Request finished in 148.889ms 404
```
 
<span data-ttu-id="9768d-142">이러한 로그는 `http://localhost:5000/api/todo/0`으로 이동하여 생성되었으며, 이는 이전 섹션에서 나온 두 `ILogger` 호출의 실행을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-142">These logs were created by going to `http://localhost:5000/api/todo/0`, which triggers execution of both `ILogger` calls shown in the preceding section.</span></span>

<span data-ttu-id="9768d-143">다음은 Visual Studio에서 응용 프로그램 예제를 실행하면 디버그 창에 표시되는 동일한 로그의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-143">Here's an example of the same logs as they appear in the Debug window when you run the sample application in Visual Studio:</span></span>

```console
Microsoft.AspNetCore.Hosting.Internal.WebHost:Information: Request starting HTTP/1.1 GET http://localhost:53104/api/todo/0  
Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker:Information: Executing action method TodoApi.Controllers.TodoController.GetById (TodoApi) with arguments (0) - ModelState is Valid
TodoApi.Controllers.TodoController:Information: Getting item 0
TodoApi.Controllers.TodoController:Warning: GetById(0) NOT FOUND
Microsoft.AspNetCore.Mvc.StatusCodeResult:Information: Executing HttpStatusCodeResult, setting HTTP status code 404
Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker:Information: Executed action TodoApi.Controllers.TodoController.GetById (TodoApi) in 152.5657ms
Microsoft.AspNetCore.Hosting.Internal.WebHost:Information: Request finished in 316.3195ms 404 
```

<span data-ttu-id="9768d-144">이전 섹션에서 `ILogger` 호출을 통해 생성된 로그는 "TodoApi.Controllers.TodoController"로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-144">The logs that were created by the `ILogger` calls shown in the preceding section begin with "TodoApi.Controllers.TodoController".</span></span> <span data-ttu-id="9768d-145">"Microsoft" 범주로 시작하는 로그는 ASP.NET Core에서 온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-145">The logs that begin with "Microsoft" categories are from ASP.NET Core.</span></span> <span data-ttu-id="9768d-146">ASP.NET Core 자체와 응용 프로그램 코드는 동일한 로깅 API와 동일한 로깅 공급자 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-146">ASP.NET Core itself and your application code are using the same logging API and the same logging providers.</span></span>

<span data-ttu-id="9768d-147">이 문서의 나머지 부분에서는 로깅에 대한 일부 세부 정보 및 옵션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-147">The remainder of this article explains some details and options for logging.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="9768d-148">NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="9768d-148">NuGet packages</span></span>

<span data-ttu-id="9768d-149">`ILogger` 및 `ILoggerFactory` 인터페이스는 [Microsoft.Extensions.Logging.Abstractions](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Abstractions/)에 있으며, 두 인터페이스의 기본 구현은 [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-149">The `ILogger` and `ILoggerFactory` interfaces are in [Microsoft.Extensions.Logging.Abstractions](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Abstractions/), and default implementations for them are in [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/).</span></span>

## <a name="log-category"></a><span data-ttu-id="9768d-150">로그 범주</span><span class="sxs-lookup"><span data-stu-id="9768d-150">Log category</span></span>

<span data-ttu-id="9768d-151">*범주*는 개발자가 만드는 각 로그와 함께 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-151">A *category* is included with each log that you create.</span></span> <span data-ttu-id="9768d-152">개발자는 `ILogger` 개체를 만들 때 범주를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-152">You specify the category when you create an `ILogger` object.</span></span> <span data-ttu-id="9768d-153">모든 문자열을 범주로 사용할 수 있지만, 로그가 작성되는 클래스의 정규화된 이름을 사용해야 하는 규칙이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-153">The category may be any string, but a convention is to use the fully qualified name of the class from which the logs are written.</span></span> <span data-ttu-id="9768d-154">"TodoApi.Controllers.TodoController"를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-154">For example: "TodoApi.Controllers.TodoController".</span></span>

<span data-ttu-id="9768d-155">범주를 문자열로 지정하거나 형식에서 범주가 파생되는 확장 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-155">You can specify the category as a string or use an extension method that derives the category from the type.</span></span> <span data-ttu-id="9768d-156">범주를 문자열로 지정하려면 아래와 같이 `ILoggerFactory` 인스턴스에 대해 `CreateLogger`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-156">To specify the category as a string, call `CreateLogger` on an `ILoggerFactory` instance, as shown below.</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_CreateLogger&highlight=7,10)]

<span data-ttu-id="9768d-157">대부분의 경우 다음 예제와 같이 `ILogger<T>`를 사용하는 편이 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-157">Most of the time, it will be easier to use `ILogger<T>`, as in the following example.</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_LoggerDI&highlight=7)]

<span data-ttu-id="9768d-158">이것은 정규화된 형식 이름 `T`를 사용하여 `CreateLogger`를 호출하는 것과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-158">This is equivalent to calling `CreateLogger` with the fully qualified type name of `T`.</span></span>

## <a name="log-level"></a><span data-ttu-id="9768d-159">로그 수준</span><span class="sxs-lookup"><span data-stu-id="9768d-159">Log level</span></span>

<span data-ttu-id="9768d-160">로그를 쓸 때마다 [LogLevel](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.loglevel)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-160">Each time you write a log, you specify its [LogLevel](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.loglevel).</span></span> <span data-ttu-id="9768d-161">로그 수준은 심각도 또는 중요도 수준을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-161">The log level indicates the degree of severity or importance.</span></span> <span data-ttu-id="9768d-162">예를 들어 메서드가 정상적으로 종료되면 `Information` 로그를 쓰고, 메서드가 404 반환 코드를 반환하면 `Warning` 로그를 쓰고, 예기치 않은 예외를 catch하면 `Error` 로그를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-162">For example, you might write an `Information` log when a method ends normally, a `Warning` log when a method returns a 404 return code, and an `Error` log when you catch an unexpected exception.</span></span>

<span data-ttu-id="9768d-163">다음 코드 예제에서 메서드 이름(예: `LogWarning`)은 로그 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-163">In the following code example, the names of the methods (for example, `LogWarning`) specify the log level.</span></span> <span data-ttu-id="9768d-164">첫 번째 매개 변수는 [Log event ID](#log-event-id)입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-164">The first parameter is the [Log event ID](#log-event-id).</span></span> <span data-ttu-id="9768d-165">두 번째 매개 변수는 [message template](#log-message-template)으로, 나머지 메서드 매개 변수에서 인수 값에 대한 자리 표시자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-165">The second parameter is a [message template](#log-message-template) with placeholders for argument values provided by the remaining method parameters.</span></span> <span data-ttu-id="9768d-166">메서드 매개 변수는 이 문서의 뒷부분에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-166">The method parameters are explained in more detail later in this article.</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

<span data-ttu-id="9768d-167">메서드 이름에 수준을 포함하는 로그 메서드는 [ILogger에 대한 확장 메서드](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.loggerextensions)입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-167">Log methods that include the level in the method name are [extension methods for ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.loggerextensions).</span></span> <span data-ttu-id="9768d-168">백그라운드에서 이러한 메서드는 `LogLevel` 매개 변수를 사용하는 `Log` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-168">Behind the scenes, these methods call a `Log` method that takes a `LogLevel` parameter.</span></span> <span data-ttu-id="9768d-169">이러한 확장 메서드 중 하나를 호출하는 대신 `Log` 메서드를 직접 호출할 수 있지만, 구문이 비교적 복잡합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-169">You can call the `Log` method directly rather than one of these extension methods, but the syntax is relatively complicated.</span></span> <span data-ttu-id="9768d-170">자세한 내용은 [ILogger 인터페이스](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) 및 [로거 확장 소스 코드](https://github.com/aspnet/Logging/blob/master/src/Microsoft.Extensions.Logging.Abstractions/LoggerExtensions.cs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9768d-170">For more information, see the [ILogger interface](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) and the [logger extensions source code](https://github.com/aspnet/Logging/blob/master/src/Microsoft.Extensions.Logging.Abstractions/LoggerExtensions.cs).</span></span>

<span data-ttu-id="9768d-171">ASP.NET Core는 다음 [로그 수준](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.loglevel)을 정의하며, 여기에 가장 낮은 심각도에서 가장 높은 심각도 순으로 정렬됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-171">ASP.NET Core defines the following [log levels](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.loglevel), ordered here from least to highest severity.</span></span>

* <span data-ttu-id="9768d-172">추적 = 0</span><span class="sxs-lookup"><span data-stu-id="9768d-172">Trace = 0</span></span>

  <span data-ttu-id="9768d-173">문제를 디버깅하는 개발자에게만 중요한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-173">For information that is valuable only to a developer debugging an issue.</span></span> <span data-ttu-id="9768d-174">이러한 메시지는 중요한 응용 프로그램 데이터를 포함할 수 있으므로 프로덕션 환경에서 사용하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-174">These messages may contain sensitive application data and so should not be enabled in a production environment.</span></span> <span data-ttu-id="9768d-175">*기본적으로 사용하지 않도록 설정됩니다.*</span><span class="sxs-lookup"><span data-stu-id="9768d-175">*Disabled by default.*</span></span> <span data-ttu-id="9768d-176">예: `Credentials: {"User":"someuser", "Password":"P@ssword"}`</span><span class="sxs-lookup"><span data-stu-id="9768d-176">Example: `Credentials: {"User":"someuser", "Password":"P@ssword"}`</span></span>

* <span data-ttu-id="9768d-177">디버그 = 1</span><span class="sxs-lookup"><span data-stu-id="9768d-177">Debug = 1</span></span>

  <span data-ttu-id="9768d-178">개발 및 디버깅하는 동안 단기적으로 유용한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-178">For information that has short-term usefulness during development and debugging.</span></span> <span data-ttu-id="9768d-179">예: 로그 볼륨이 크기 때문에 문제를 해결하려는 경우 외에는 프로덕션 환경에서 `Entering method Configure with flag set to true.`일반적으로 수준 로그를 사용하지 않습니다`Debug`.</span><span class="sxs-lookup"><span data-stu-id="9768d-179">Example: `Entering method Configure with flag set to true.` You typically would not enable `Debug` level logs in production unless you are troubleshooting, due to the high volume of logs.</span></span>

* <span data-ttu-id="9768d-180">정보 = 2</span><span class="sxs-lookup"><span data-stu-id="9768d-180">Information = 2</span></span>

  <span data-ttu-id="9768d-181">응용 프로그램의 일반적인 흐름을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-181">For tracking the general flow of the application.</span></span> <span data-ttu-id="9768d-182">이러한 로그는 일반적으로 장기적인 가치가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-182">These logs typically have some long-term value.</span></span> <span data-ttu-id="9768d-183">예: `Request received for path /api/todo`</span><span class="sxs-lookup"><span data-stu-id="9768d-183">Example: `Request received for path /api/todo`</span></span>

* <span data-ttu-id="9768d-184">경고 = 3</span><span class="sxs-lookup"><span data-stu-id="9768d-184">Warning = 3</span></span>

  <span data-ttu-id="9768d-185">응용 프로그램 흐름에 비정상적인 또는 예기치 않은 이벤트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-185">For abnormal or unexpected events in the application flow.</span></span> <span data-ttu-id="9768d-186">응용 프로그램을 중지하지는 않지만 조사할 필요가 있는 오류 또는 기타 조건도 여기에 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-186">These may include errors or other conditions that do not cause the application to stop, but which may need to be investigated.</span></span> <span data-ttu-id="9768d-187">처리된 예외는 `Warning` 로그 수준을 사용하는 일반적인 장소입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-187">Handled exceptions are a common place to use the `Warning` log level.</span></span> <span data-ttu-id="9768d-188">예: `FileNotFoundException for file quotes.txt.`</span><span class="sxs-lookup"><span data-stu-id="9768d-188">Example: `FileNotFoundException for file quotes.txt.`</span></span>

* <span data-ttu-id="9768d-189">오류 = 4</span><span class="sxs-lookup"><span data-stu-id="9768d-189">Error = 4</span></span>

  <span data-ttu-id="9768d-190">처리할 수 없는 오류 및 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-190">For errors and exceptions that cannot be handled.</span></span> <span data-ttu-id="9768d-191">이러한 메시지는 전체 응용 프로그램 오류가 아닌 현재 동작 또는 작업(예: 현재 HTTP 요청)의 오류를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-191">These messages indicate a failure in the current activity or operation (such as the current HTTP request), not an application-wide failure.</span></span> <span data-ttu-id="9768d-192">예제 로그 메시지: `Cannot insert record due to duplicate key violation.`</span><span class="sxs-lookup"><span data-stu-id="9768d-192">Example log message: `Cannot insert record due to duplicate key violation.`</span></span>

* <span data-ttu-id="9768d-193">중요 = 5</span><span class="sxs-lookup"><span data-stu-id="9768d-193">Critical = 5</span></span>

  <span data-ttu-id="9768d-194">즉각적인 대응이 필요한 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-194">For failures that require immediate attention.</span></span> <span data-ttu-id="9768d-195">예: 데이터 손실 시나리오, 디스크 공간 부족.</span><span class="sxs-lookup"><span data-stu-id="9768d-195">Examples: data loss scenarios, out of disk space.</span></span>

<span data-ttu-id="9768d-196">로그 수준을 사용하여 특정 저장 매체 또는 디스플레이 창에 기록되는 로그 출력의 양을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-196">You can use the log level to control how much log output is written to a particular storage medium or display window.</span></span> <span data-ttu-id="9768d-197">예를 들어 프로덕션 환경에서 `Information` 수준 이하의 모든 로그는 볼륨 데이터 저장소로 이동하고, `Warning` 수준 이상의 모든 로그는 가치 데이터 저장소로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-197">For example, in production you might want all logs of `Information` level and lower to go to a volume data store, and all logs of `Warning` level and higher to go to a value data store.</span></span> <span data-ttu-id="9768d-198">개발하는 동안 심각도가 `Warning` 이상인 로그는 일반적으로 콘솔로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-198">During development, you might normally send logs of `Warning` or higher severity to the console.</span></span> <span data-ttu-id="9768d-199">문제를 해결해야 하는 상황이 오면 `Debug` 수준을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-199">Then when you need to troubleshoot, you can add `Debug` level.</span></span> <span data-ttu-id="9768d-200">이 문서의 뒷부분에 나오는 [로그 필터링](#log-filtering) 섹션에서는 공급자가 처리하는 로그 수준을 제어하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-200">The [Log filtering](#log-filtering) section later in this article explains how to control which log levels a provider handles.</span></span>

<span data-ttu-id="9768d-201">ASP.NET Core 프레임워크는 프레임워크 이벤트에 대한 `Debug` 수준 로그를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-201">The ASP.NET Core framework writes `Debug` level logs for framework events.</span></span> <span data-ttu-id="9768d-202">이 문서 앞부분에 나온 로그 예제는 `Information` 수준 미만 로그를 제외했기 때문에 `Debug` 수준 로그가 하나도 표시되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-202">The log examples earlier in this article excluded logs below `Information` level, so no `Debug` level logs were shown.</span></span> <span data-ttu-id="9768d-203">다음은 콘솔 공급자에 대해 `Debug` 이상 로그를 표시하도록 구성된 응용 프로그램 예제를 실행할 경우의 콘솔 로그 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-203">Here's an example of console logs if you run the sample application configured to show `Debug` and higher logs for the console provider.</span></span>

```console
info: Microsoft.AspNetCore.Hosting.Internal.WebHost[1]
      Request starting HTTP/1.1 GET http://localhost:62555/api/todo/0
dbug: Microsoft.AspNetCore.Routing.Tree.TreeRouter[1]
      Request successfully matched the route with name 'GetTodo' and template 'api/Todo/{id}'.
dbug: Microsoft.AspNetCore.Mvc.Internal.ActionSelector[2]
      Action 'TodoApi.Controllers.TodoController.Update (TodoApi)' with id '089d59b6-92ec-472d-b552-cc613dfd625d' did not match the constraint 'Microsoft.AspNetCore.Mvc.Internal.HttpMethodActionConstraint'
dbug: Microsoft.AspNetCore.Mvc.Internal.ActionSelector[2]
      Action 'TodoApi.Controllers.TodoController.Delete (TodoApi)' with id 'f3476abe-4bd9-4ad3-9261-3ead09607366' did not match the constraint 'Microsoft.AspNetCore.Mvc.Internal.HttpMethodActionConstraint'
dbug: Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker[1]
      Executing action TodoApi.Controllers.TodoController.GetById (TodoApi)
info: Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker[1]
      Executing action method TodoApi.Controllers.TodoController.GetById (TodoApi) with arguments (0) - ModelState is Valid
info: TodoApi.Controllers.TodoController[1002]
      Getting item 0
warn: TodoApi.Controllers.TodoController[4000]
      GetById(0) NOT FOUND
dbug: Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker[2]
      Executed action method TodoApi.Controllers.TodoController.GetById (TodoApi), returned result Microsoft.AspNetCore.Mvc.NotFoundResult.
info: Microsoft.AspNetCore.Mvc.StatusCodeResult[1]
      Executing HttpStatusCodeResult, setting HTTP status code 404
info: Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker[2]
      Executed action TodoApi.Controllers.TodoController.GetById (TodoApi) in 0.8788ms
dbug: Microsoft.AspNetCore.Server.Kestrel[9]
      Connection id "0HL6L7NEFF2QD" completed keep alive response.
info: Microsoft.AspNetCore.Hosting.Internal.WebHost[2]
      Request finished in 2.7286ms 404
```

## <a name="log-event-id"></a><span data-ttu-id="9768d-204">로그 이벤트 ID</span><span class="sxs-lookup"><span data-stu-id="9768d-204">Log event ID</span></span>

<span data-ttu-id="9768d-205">로그를 쓸 때마다 *이벤트 ID*를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-205">Each time you write a log, you can specify an *event ID*.</span></span> <span data-ttu-id="9768d-206">샘플 앱은 로컬로 정의된 `LoggingEvents` 클래스를 사용하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-206">The sample app does this by using a locally-defined `LoggingEvents` class:</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

[!code-csharp[](index/sample//Core/LoggingEvents.cs?name=snippet_LoggingEvents)]

<span data-ttu-id="9768d-207">이벤트 ID는 로깅된 이벤트 집합을 서로 연결하는 데 사용할 수 있는 정수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-207">An event ID is an integer value that you can use to associate a set of logged events with one another.</span></span> <span data-ttu-id="9768d-208">예를 들어 장바구니에 항목 추가에 대한 로그는 이벤트 ID 1000이고 구매 완료에 대한 로그는 이벤트 ID 1001입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-208">For instance, a log for adding an item to a shopping cart could be event ID 1000 and a log for completing a purchase could be event ID 1001.</span></span>

<span data-ttu-id="9768d-209">로깅 출력에서 이벤트 ID는 공급자에 따라 필드에 저장되거나 텍스트 메시지에 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-209">In logging output, the event ID may be stored in a field or included in the text message, depending on the provider.</span></span> <span data-ttu-id="9768d-210">디버그 공급자는 이벤트 ID를 표시하지 않지만, 콘솔 공급자는 범주 뒤에서 대괄호 안에 이벤트 ID를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-210">The Debug provider doesn't show event IDs, but the console provider shows them in brackets after the category:</span></span>

```console
info: TodoApi.Controllers.TodoController[1002]
      Getting item invalidid
warn: TodoApi.Controllers.TodoController[4000]
      GetById(invalidid) NOT FOUND
```

## <a name="log-message-template"></a><span data-ttu-id="9768d-211">로그 메시지 템플릿</span><span class="sxs-lookup"><span data-stu-id="9768d-211">Log message template</span></span>

<span data-ttu-id="9768d-212">로그 메시지를 쓸 때마다 메시지 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-212">Each time you write a log message, you provide a message template.</span></span> <span data-ttu-id="9768d-213">메시지 템플릿은 문자열일 수도 있고, 인수 값이 배치되는 명명된 자리 표시자를 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-213">The message template can be a string or it can contain named placeholders into which argument values are placed.</span></span> <span data-ttu-id="9768d-214">템플릿은 형식 문자열이 아니고, 자리 표시자는 번호가 아닌 이름이 지정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-214">The template isn't a format string, and placeholders should be named, not numbered.</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

<span data-ttu-id="9768d-215">값을 제공하는 데 사용되는 매개 변수를 결정하는 것은 자리 표시자의 번호가 아닌 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-215">The order of placeholders, not their names, determines which parameters are used to provide their values.</span></span> <span data-ttu-id="9768d-216">다음과 같은 코드를 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-216">If you have the following code:</span></span>

```csharp
string p1 = "parm1";
string p2 = "parm2";
_logger.LogInformation("Parameter values: {p2}, {p1}", p1, p2);
```

<span data-ttu-id="9768d-217">결과로 만들어진 로그 메시지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-217">The resulting log message looks like this:</span></span>

```
Parameter values: parm1, parm2
```

<span data-ttu-id="9768d-218">로깅 프레임워크는 이 방식으로 메시지를 포맷하여 로깅 공급자가 [구조적 로깅이라고도 하는 의미 체계 로깅](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging)을 구현할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-218">The logging framework does message formatting in this way to make it possible for logging providers to implement [semantic logging, also known as structured logging](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging).</span></span> <span data-ttu-id="9768d-219">인수 자체는 포맷된 메시지 템플릿이 아닌 로깅 시스템으로 전달되기 때문에 로깅 공급자가 메시지 템플릿 외에도 매개 변수 값을 필드로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-219">Because the arguments themselves are passed to the logging system, not just the formatted message template, logging providers can store the parameter values as fields in addition to the message template.</span></span> <span data-ttu-id="9768d-220">로그 출력을 Azure Table Storage로 전달하는 경우 로거 메서드 호출은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-220">If you're directing your log output to Azure Table Storage and your logger method call looks like this:</span></span>

```csharp
_logger.LogInformation("Getting item {ID} at {RequestTime}", id, DateTime.Now);
```

<span data-ttu-id="9768d-221">각 Azure Table 엔터티는 로그 데이터에 대한 쿼리를 간소화하는 `ID` 및 `RequestTime` 속성을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-221">Each Azure Table entity can have `ID` and `RequestTime` properties, which simplifies queries on log data.</span></span> <span data-ttu-id="9768d-222">문자 메시지의 시간 초과를 구문 분석할 필요 없이 특정 `RequestTime` 범위 내에서 모든 로그를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-222">You can find all logs within a particular `RequestTime` range without the need to parse the time out of the text message.</span></span>

## <a name="logging-exceptions"></a><span data-ttu-id="9768d-223">로깅 처리</span><span class="sxs-lookup"><span data-stu-id="9768d-223">Logging exceptions</span></span>

<span data-ttu-id="9768d-224">로거 메서드는 다음 예제와 같이 예외를 전달할 수 있는 오버로드를 갖고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-224">The logger methods have overloads that let you pass in an exception, as in the following example:</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_LogException&highlight=3)]

<span data-ttu-id="9768d-225">공급자들은 다양한 방식으로 예외 정보를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-225">Different providers handle the exception information in different ways.</span></span> <span data-ttu-id="9768d-226">다음은 위에서 보여드린 코드의 디버그 공급자 출력의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-226">Here's an example of Debug provider output from the code shown above.</span></span>

```
TodoApi.Controllers.TodoController:Warning: GetById(036dd898-fb01-47e8-9a65-f92eb73cf924) NOT FOUND

System.Exception: Item not found exception.
 at TodoApi.Controllers.TodoController.GetById(String id) in C:\logging\sample\src\TodoApi\Controllers\TodoController.cs:line 226
```

## <a name="log-filtering"></a><span data-ttu-id="9768d-227">로깅 필터링</span><span class="sxs-lookup"><span data-stu-id="9768d-227">Log filtering</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9768d-228">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9768d-228">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="9768d-229">특정 공급자 및 범주 또는 모든 공급자나 모든 범주의 최소 로그 수준을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-229">You can specify a minimum log level for a specific provider and category or for all providers or all categories.</span></span> <span data-ttu-id="9768d-230">최소 수준 미만인 로그는 해당 공급자에게 전달되지 않으므로 표시되거나 저장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-230">Any logs below the minimum level aren't passed to that provider, so they don't get displayed or stored.</span></span> 

<span data-ttu-id="9768d-231">모든 로그를 표시하지 않으려면 최소 로그 수준으로 `LogLevel.None`을 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-231">If you want to suppress all logs, you can specify `LogLevel.None` as the minimum log level.</span></span> <span data-ttu-id="9768d-232">`LogLevel.None`의 정수 값은 `LogLevel.Critical`(5)보다 높은 6입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-232">The integer value of `LogLevel.None` is 6, which is higher than `LogLevel.Critical` (5).</span></span>

<span data-ttu-id="9768d-233">**구성에서 필터 규칙 만들기**</span><span class="sxs-lookup"><span data-stu-id="9768d-233">**Create filter rules in configuration**</span></span>

<span data-ttu-id="9768d-234">프로젝트 템플릿은 콘솔 및 디버그 공급자에 대한 로깅을 설정하는 `CreateDefaultBuilder`를 호출하는 코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-234">The project templates create code that calls `CreateDefaultBuilder` to set up logging for the Console and Debug providers.</span></span> <span data-ttu-id="9768d-235">또한 `CreateDefaultBuilder` 메서드는 다음과 같은 코드를 사용하여 `Logging` 섹션에서 구성을 조회하는 로깅을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-235">The `CreateDefaultBuilder` method also sets up logging to look for configuration in a `Logging` section, using code like the following:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_ExpandDefault&highlight=15)]

<span data-ttu-id="9768d-236">구성 데이터는 다음 예제와 같이 공급자 및 범주별로 최소 로그 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-236">The configuration data specifies minimum log levels by provider and category, as in the following example:</span></span>

[!code-json[](index/sample2/appsettings.json)]

<span data-ttu-id="9768d-237">이 JSON은 6개의 필터 규칙을 만드는데, 하나는 디버그 공급자용이고, 4개는 콘솔 공급자용이고, 나머지 하나는 모든 공급자에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-237">This JSON creates six filter rules, one for the Debug provider, four for the Console provider, and one that applies to all providers.</span></span> <span data-ttu-id="9768d-238">`ILogger` 개체가 생성될 때 각 공급자에 대해 이러한 규칙 중 하나를 선택하는 방법은 나중에 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-238">You'll see later how just one of these rules is chosen for each provider when an `ILogger` object is created.</span></span>

<span data-ttu-id="9768d-239">**코드의 필터 규칙**</span><span class="sxs-lookup"><span data-stu-id="9768d-239">**Filter rules in code**</span></span>

<span data-ttu-id="9768d-240">다음 예제와 같이 코드에서 필터 규칙을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-240">You can register filter rules in code, as shown in the following example:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_FilterInCode&highlight=4-5)]

<span data-ttu-id="9768d-241">두 번째 `AddFilter`는 형식 이름을 사용하여 디버그 공급자를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-241">The second `AddFilter` specifies the Debug provider by using its type name.</span></span> <span data-ttu-id="9768d-242">첫 번째 `AddFilter`는 공급자 형식을 지정하지 않으며, 따라서 모든 공급자에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-242">The first `AddFilter` applies to all providers because it doesn't specify a provider type.</span></span>

<span data-ttu-id="9768d-243">**필터링 규칙 적용 방식**</span><span class="sxs-lookup"><span data-stu-id="9768d-243">**How filtering rules are applied**</span></span>

<span data-ttu-id="9768d-244">이전 예제의 구성 데이터 및 `AddFilter` 코드는 다음 표에 표시된 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-244">The configuration data and the `AddFilter` code shown in the preceding examples create the rules shown in the following table.</span></span> <span data-ttu-id="9768d-245">처음 6개는 구성 예제에서 가져온 것이고 마지막 2개는 코드 예제에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-245">The first six come from the configuration example and the last two come from the code example.</span></span>

| <span data-ttu-id="9768d-246">수</span><span class="sxs-lookup"><span data-stu-id="9768d-246">Number</span></span> | <span data-ttu-id="9768d-247">공급자</span><span class="sxs-lookup"><span data-stu-id="9768d-247">Provider</span></span>      | <span data-ttu-id="9768d-248">다음으로 시작하는 범주...</span><span class="sxs-lookup"><span data-stu-id="9768d-248">Categories that begin with ...</span></span>          | <span data-ttu-id="9768d-249">최소 로그 수준</span><span class="sxs-lookup"><span data-stu-id="9768d-249">Minimum log level</span></span> |
| :----: | ------------- | --------------------------------------- | ----------------- |
| <span data-ttu-id="9768d-250">1</span><span class="sxs-lookup"><span data-stu-id="9768d-250">1</span></span>      | <span data-ttu-id="9768d-251">디버그</span><span class="sxs-lookup"><span data-stu-id="9768d-251">Debug</span></span>         | <span data-ttu-id="9768d-252">모든 범주</span><span class="sxs-lookup"><span data-stu-id="9768d-252">All categories</span></span>                          | <span data-ttu-id="9768d-253">정보</span><span class="sxs-lookup"><span data-stu-id="9768d-253">Information</span></span>       |
| <span data-ttu-id="9768d-254">2</span><span class="sxs-lookup"><span data-stu-id="9768d-254">2</span></span>      | <span data-ttu-id="9768d-255">콘솔</span><span class="sxs-lookup"><span data-stu-id="9768d-255">Console</span></span>       | <span data-ttu-id="9768d-256">Microsoft.AspNetCore.Mvc.Razor.Internal</span><span class="sxs-lookup"><span data-stu-id="9768d-256">Microsoft.AspNetCore.Mvc.Razor.Internal</span></span> | <span data-ttu-id="9768d-257">경고</span><span class="sxs-lookup"><span data-stu-id="9768d-257">Warning</span></span>           |
| <span data-ttu-id="9768d-258">3</span><span class="sxs-lookup"><span data-stu-id="9768d-258">3</span></span>      | <span data-ttu-id="9768d-259">콘솔</span><span class="sxs-lookup"><span data-stu-id="9768d-259">Console</span></span>       | <span data-ttu-id="9768d-260">Microsoft.AspNetCore.Mvc.Razor.Razor</span><span class="sxs-lookup"><span data-stu-id="9768d-260">Microsoft.AspNetCore.Mvc.Razor.Razor</span></span>    | <span data-ttu-id="9768d-261">디버그</span><span class="sxs-lookup"><span data-stu-id="9768d-261">Debug</span></span>             |
| <span data-ttu-id="9768d-262">4</span><span class="sxs-lookup"><span data-stu-id="9768d-262">4</span></span>      | <span data-ttu-id="9768d-263">콘솔</span><span class="sxs-lookup"><span data-stu-id="9768d-263">Console</span></span>       | <span data-ttu-id="9768d-264">Microsoft.AspNetCore.Mvc.Razor</span><span class="sxs-lookup"><span data-stu-id="9768d-264">Microsoft.AspNetCore.Mvc.Razor</span></span>          | <span data-ttu-id="9768d-265">Error</span><span class="sxs-lookup"><span data-stu-id="9768d-265">Error</span></span>             |
| <span data-ttu-id="9768d-266">5</span><span class="sxs-lookup"><span data-stu-id="9768d-266">5</span></span>      | <span data-ttu-id="9768d-267">콘솔</span><span class="sxs-lookup"><span data-stu-id="9768d-267">Console</span></span>       | <span data-ttu-id="9768d-268">모든 범주</span><span class="sxs-lookup"><span data-stu-id="9768d-268">All categories</span></span>                          | <span data-ttu-id="9768d-269">정보</span><span class="sxs-lookup"><span data-stu-id="9768d-269">Information</span></span>       |
| <span data-ttu-id="9768d-270">6</span><span class="sxs-lookup"><span data-stu-id="9768d-270">6</span></span>      | <span data-ttu-id="9768d-271">모든 공급자</span><span class="sxs-lookup"><span data-stu-id="9768d-271">All providers</span></span> | <span data-ttu-id="9768d-272">모든 범주</span><span class="sxs-lookup"><span data-stu-id="9768d-272">All categories</span></span>                          | <span data-ttu-id="9768d-273">디버그</span><span class="sxs-lookup"><span data-stu-id="9768d-273">Debug</span></span>             |
| <span data-ttu-id="9768d-274">7</span><span class="sxs-lookup"><span data-stu-id="9768d-274">7</span></span>      | <span data-ttu-id="9768d-275">모든 공급자</span><span class="sxs-lookup"><span data-stu-id="9768d-275">All providers</span></span> | <span data-ttu-id="9768d-276">시스템</span><span class="sxs-lookup"><span data-stu-id="9768d-276">System</span></span>                                  | <span data-ttu-id="9768d-277">디버그</span><span class="sxs-lookup"><span data-stu-id="9768d-277">Debug</span></span>             |
| <span data-ttu-id="9768d-278">8</span><span class="sxs-lookup"><span data-stu-id="9768d-278">8</span></span>      | <span data-ttu-id="9768d-279">디버그</span><span class="sxs-lookup"><span data-stu-id="9768d-279">Debug</span></span>         | <span data-ttu-id="9768d-280">Microsoft</span><span class="sxs-lookup"><span data-stu-id="9768d-280">Microsoft</span></span>                               | <span data-ttu-id="9768d-281">추적</span><span class="sxs-lookup"><span data-stu-id="9768d-281">Trace</span></span>             |

<span data-ttu-id="9768d-282">로그를 쓰는 `ILogger` 개체를 만들 때 `ILoggerFactory` 개체는 공급자마다 해당 로거에 적용할 단일 규칙을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-282">When you create an `ILogger` object to write logs with, the `ILoggerFactory` object selects a single rule per provider to apply to that logger.</span></span> <span data-ttu-id="9768d-283">`ILogger` 개체를 통해 작성된 모든 메시지는 선택한 규칙을 기반으로 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-283">All messages written by that `ILogger` object are filtered based on the selected rules.</span></span> <span data-ttu-id="9768d-284">사용 가능한 규칙 중에서 각 공급자 및 범주 쌍에 적용 가능한 가장 구체적인 규칙이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-284">The most specific rule possible for each provider and category pair is selected from the available rules.</span></span>

<span data-ttu-id="9768d-285">지정된 범주에 대한 `ILogger`가 생성되면 다음 알고리즘이 각 공급자에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-285">The following algorithm is used for each provider when an `ILogger` is created for a given category:</span></span>

* <span data-ttu-id="9768d-286">공급자 또는 공급자의 별칭과 일치하는 모든 규칙을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-286">Select all rules that match the provider or its alias.</span></span> <span data-ttu-id="9768d-287">일치 항목이 없는 경우 빈 공급자와 함께 모든 규칙을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-287">If none are found, select all rules with an empty provider.</span></span>
* <span data-ttu-id="9768d-288">앞 단계의 결과에서 일치하는 범주 접두사가 가장 긴 규칙을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-288">From the result of the preceding step, select rules with longest matching category prefix.</span></span> <span data-ttu-id="9768d-289">일치 항목이 없는 경우 범주를 지정하지 않는 규칙을 모두 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-289">If none are found, select all rules that don't specify a category.</span></span>
* <span data-ttu-id="9768d-290">여러 규칙을 선택하는 경우 **마지막** 규칙을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-290">If multiple rules are selected take the **last** one.</span></span>
* <span data-ttu-id="9768d-291">규칙을 선택하지 않는 경우 `MinimumLevel`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-291">If no rules are selected, use `MinimumLevel`.</span></span>
 
<span data-ttu-id="9768d-292">예를 들어 이전 단계의 규칙 목록을 갖고 있고 "Microsoft.AspNetCore.Mvc.Razor.RazorViewEngine" 범주에 대한 `ILogger` 개체를 만든다고 가정해 봅시다.</span><span class="sxs-lookup"><span data-stu-id="9768d-292">For example, suppose you have the preceding list of rules and you create an `ILogger` object for category "Microsoft.AspNetCore.Mvc.Razor.RazorViewEngine":</span></span>

* <span data-ttu-id="9768d-293">디버그 공급자에게는 규칙 1, 6, 8이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-293">For the Debug provider, rules 1, 6, and 8 apply.</span></span> <span data-ttu-id="9768d-294">규칙 8이 가장 구체적이므로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-294">Rule 8 is most specific, so that's the one selected.</span></span>
* <span data-ttu-id="9768d-295">콘솔 공급자에게는 규칙 3, 4, 5, 6이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-295">For the Console provider, rules 3, 4, 5, and 6 apply.</span></span> <span data-ttu-id="9768d-296">규칙 3이 가장 구체적입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-296">Rule 3 is most specific.</span></span>

<span data-ttu-id="9768d-297">`ILogger`를 사용하여 "Microsoft.AspNetCore.Mvc.Razor.RazorViewEngine" 범주에 대한 로그를 만들 때 수준 `Trace` 이상의 로그는 디버그 공급자로 이동하고 수준 `Debug` 이상의 로그는 콘솔 공급자로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-297">When you create logs with an `ILogger` for category "Microsoft.AspNetCore.Mvc.Razor.RazorViewEngine", logs of `Trace` level and above will go to the Debug provider, and logs of `Debug` level and above will go to the Console provider.</span></span>

<span data-ttu-id="9768d-298">**공급자 별칭**</span><span class="sxs-lookup"><span data-stu-id="9768d-298">**Provider aliases**</span></span>

<span data-ttu-id="9768d-299">형식 이름을 사용하여 구성에서 공급자를 지정할 수 있지만, 각 공급자는 길이가 짧아 사용하기 간편한 *별칭*을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-299">You can use the type name to specify a provider in configuration, but each provider defines a shorter *alias* that is easier to use.</span></span> <span data-ttu-id="9768d-300">기본 공급자의 경우 다음 별칭을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-300">For the built-in providers, use the following aliases:</span></span>

- <span data-ttu-id="9768d-301">콘솔</span><span class="sxs-lookup"><span data-stu-id="9768d-301">Console</span></span>
- <span data-ttu-id="9768d-302">디버그</span><span class="sxs-lookup"><span data-stu-id="9768d-302">Debug</span></span>
- <span data-ttu-id="9768d-303">EventLog</span><span class="sxs-lookup"><span data-stu-id="9768d-303">EventLog</span></span>
- <span data-ttu-id="9768d-304">AzureAppServices</span><span class="sxs-lookup"><span data-stu-id="9768d-304">AzureAppServices</span></span>
- <span data-ttu-id="9768d-305">TraceSource</span><span class="sxs-lookup"><span data-stu-id="9768d-305">TraceSource</span></span>
- <span data-ttu-id="9768d-306">EventSource</span><span class="sxs-lookup"><span data-stu-id="9768d-306">EventSource</span></span>

<span data-ttu-id="9768d-307">**기본 최소 수준**</span><span class="sxs-lookup"><span data-stu-id="9768d-307">**Default minimum level**</span></span>

<span data-ttu-id="9768d-308">특정 공급자 및 범주에 대한 구성 또는 코드의 규칙이 적용되지 않는 경우에만 효력이 있는 최소 수준 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-308">There is a minimum level setting that takes effect only if no rules from configuration or code apply for a given provider and category.</span></span> <span data-ttu-id="9768d-309">다음 예제는 최소 수준을 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-309">The following example shows how to set the minimum level:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_MinLevel&highlight=3)]

<span data-ttu-id="9768d-310">최소 수준을 명시적으로 설정하지 않으면 `Trace` 및 `Debug` 로그를 무시하는 `Information`이 기본값으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-310">If you don't explicitly set the minimum level, the default value is `Information`, which means that `Trace` and `Debug` logs are ignored.</span></span>

<span data-ttu-id="9768d-311">**필터 함수**</span><span class="sxs-lookup"><span data-stu-id="9768d-311">**Filter functions**</span></span>

<span data-ttu-id="9768d-312">필터 함수에서 필터링 규칙을 적용할 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-312">You can write code in a filter function to apply filtering rules.</span></span> <span data-ttu-id="9768d-313">필터 함수는 구성 또는 코드를 통해 규칙이 할당되지 않은 모든 공급자와 범주에 대해 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-313">A filter function is invoked for all providers and categories that do not have rules assigned to them by configuration or code.</span></span> <span data-ttu-id="9768d-314">함수의 코드는 공급자 형식, 범주 및 로그 수준에 액세스하여 메시지를 기록할 것인지 여부를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-314">Code in the function has access to the provider type, category, and log level to decide whether or not a message should be logged.</span></span> <span data-ttu-id="9768d-315">예:</span><span class="sxs-lookup"><span data-stu-id="9768d-315">For example:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_FilterFunction&highlight=5-13)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9768d-316">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9768d-316">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="9768d-317">일부 로깅 공급자는 로그 수준 및 범주에 따라 로그를 저장 매체에 기록할 것인지 아니면 무시할 것인지를 개발자가 지정할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-317">Some logging providers let you specify when logs should be written to a storage medium or ignored based on log level and category.</span></span>

<span data-ttu-id="9768d-318">`AddConsole` 및 `AddDebug` 확장 메서드는 필터링 조건을 전달할 수 있는 오버로드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-318">The `AddConsole` and `AddDebug` extension methods provide overloads that let you pass in filtering criteria.</span></span> <span data-ttu-id="9768d-319">다음 샘플 코드는 콘솔 공급자가 `Warning` 수준 미만의 로그를 무시하게 만들고, 디버그 공급자는 프레임워크에서 만드는 로그를 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-319">The following sample code causes the console provider to ignore logs below `Warning` level, while the Debug provider ignores logs that the framework creates.</span></span>

[!code-csharp[](index/sample/Startup.cs?name=snippet_AddConsoleAndDebugWithFilter&highlight=6-7)]

<span data-ttu-id="9768d-320">`AddEventLog` 메서드는 `EventLogSettings` 인스턴스를 사용하는 오버로드를 갖고 있으며, 이 인스턴스의 `Filter` 속성에는 필터링 함수가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-320">The `AddEventLog` method has an overload that takes an `EventLogSettings` instance, which may contain a filtering function in its `Filter` property.</span></span> <span data-ttu-id="9768d-321">TraceSource 공급자는 오버로드를 제공하지 않습니다. 로깅 수준 및 기타 매개가 사용하는 `SourceSwitch` 및 `TraceListener`를 기반으로 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-321">The TraceSource provider does not provide any of those overloads, since its logging level and other parameters are based on the `SourceSwitch` and `TraceListener` it uses.</span></span>

<span data-ttu-id="9768d-322">`WithFilter` 확장 메서드를 사용하여 `ILoggerFactory` 인스턴스에 등록된 모든 공급자에 대한 필터링 규칙을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-322">You can set filtering rules for all providers that are registered with an `ILoggerFactory` instance by using the `WithFilter` extension method.</span></span> <span data-ttu-id="9768d-323">아래 예제는 프레임워크 로그(범주가 "Microsoft" 또는 "시스템"으로 시작)를 경고로 제한하고 디버그 수준에서 앱 로그를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-323">The example below limits framework logs (category begins with "Microsoft" or "System") to warnings while letting the app log at debug level.</span></span>

[!code-csharp[](index/sample/Startup.cs?name=snippet_FactoryFilter&highlight=6-11)]

<span data-ttu-id="9768d-324">필터링을 사용하여 특정 범주에 대한 로그를 기록하지 못하게 하려면 해당 범주의 최소 로그 수준으로 `LogLevel.None`을 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-324">If you want to use filtering to prevent all logs from being written for a particular category, you can specify `LogLevel.None` as the minimum log level for that category.</span></span> <span data-ttu-id="9768d-325">`LogLevel.None`의 정수 값은 `LogLevel.Critical`(5)보다 높은 6입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-325">The integer value of `LogLevel.None` is 6, which is higher than `LogLevel.Critical` (5).</span></span>

<span data-ttu-id="9768d-326">`WithFilter` 확장 메서드는 [Microsoft.Extensions.Logging.Filter](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Filter) NuGet 패키지에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-326">The `WithFilter` extension method is provided by the [Microsoft.Extensions.Logging.Filter](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Filter) NuGet package.</span></span> <span data-ttu-id="9768d-327">이 메서드는 등록된 모든 로거 공급자로 전달되는 메시지를 필터링하는 새로운 `ILoggerFactory` 인스턴스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-327">The method returns a new `ILoggerFactory` instance that will filter the log messages passed to all logger providers registered with it.</span></span> <span data-ttu-id="9768d-328">원래 `ILoggerFactory` 인스턴스를 포함하여 어떤 `ILoggerFactory` 인스턴스에도 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-328">It does not affect any other `ILoggerFactory` instances, including the original `ILoggerFactory` instance.</span></span>

---

## <a name="log-scopes"></a><span data-ttu-id="9768d-329">로그 점수</span><span class="sxs-lookup"><span data-stu-id="9768d-329">Log scopes</span></span>

<span data-ttu-id="9768d-330">*범위* 내의 논리적 작업 집합을 그룹화하여 동일한 데이터를 해당 집합의 일부로 생성된 각 로그에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-330">You can group a set of logical operations within a *scope* in order to attach the same data to each log that is created as part of that set.</span></span> <span data-ttu-id="9768d-331">예를 들어 트랜잭션 처리의 일부로 생성되는 모든 로그가 트랜잭션 ID를 포함하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-331">For example, you might want every log created as part of processing a transaction to include the transaction ID.</span></span>

<span data-ttu-id="9768d-332">범위는 `ILogger.BeginScope<TState>` 메서드에서 반환하는 `IDisposable` 형식이며 삭제될 때까지 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-332">A scope is an `IDisposable` type that is returned by the `ILogger.BeginScope<TState>` method and lasts until it is disposed.</span></span> <span data-ttu-id="9768d-333">다음과 같이 로거 호출을 `using` 블록에 래핑하여 범위를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-333">You use a scope by wrapping your logger calls in a `using` block, as shown here:</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_Scopes&highlight=4-5,13)]

<span data-ttu-id="9768d-334">다음은 콘솔 공급자에 대한 범위를 사용하도록 설정하는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-334">The following code enables scopes for the console provider:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9768d-335">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9768d-335">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="9768d-336">*Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="9768d-336">In *Program.cs*:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_Scopes&highlight=4)]

> [!NOTE]
> <span data-ttu-id="9768d-337">범위 기반 로깅을 사용하려면 `IncludeScopes` 콘솔 로거 옵션을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-337">Configuring the `IncludeScopes` console logger option is required to enable scope-based logging.</span></span> <span data-ttu-id="9768d-338">*appsettings* 구성 파일을 사용하여 `IncludeScopes`를 구성하는 기능은 ASP.NET Core 2.1 릴리스에서 제공될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-338">Configuration of `IncludeScopes` using *appsettings* configuration files will be available with the release of ASP.NET Core 2.1.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9768d-339">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9768d-339">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="9768d-340">*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="9768d-340">In *Startup.cs*:</span></span>

[!code-csharp[](index/sample/Startup.cs?name=snippet_Scopes&highlight=6)]

---

<span data-ttu-id="9768d-341">각 로그 메시지는 범위 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-341">Each log message includes the scoped information:</span></span>

```
info: TodoApi.Controllers.TodoController[1002]
      => RequestId:0HKV9C49II9CK RequestPath:/api/todo/0 => TodoApi.Controllers.TodoController.GetById (TodoApi) => Message attached to logs created in the using block
      Getting item 0
warn: TodoApi.Controllers.TodoController[4000]
      => RequestId:0HKV9C49II9CK RequestPath:/api/todo/0 => TodoApi.Controllers.TodoController.GetById (TodoApi) => Message attached to logs created in the using block
      GetById(0) NOT FOUND
```

## <a name="built-in-logging-providers"></a><span data-ttu-id="9768d-342">기본 로깅 공급자</span><span class="sxs-lookup"><span data-stu-id="9768d-342">Built-in logging providers</span></span>

<span data-ttu-id="9768d-343">ASP.NET Core는 다음 공급자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-343">ASP.NET Core ships the following providers:</span></span>

* [<span data-ttu-id="9768d-344">콘솔</span><span class="sxs-lookup"><span data-stu-id="9768d-344">Console</span></span>](#console)
* [<span data-ttu-id="9768d-345">디버그</span><span class="sxs-lookup"><span data-stu-id="9768d-345">Debug</span></span>](#debug)
* [<span data-ttu-id="9768d-346">EventSource</span><span class="sxs-lookup"><span data-stu-id="9768d-346">EventSource</span></span>](#eventsource)
* [<span data-ttu-id="9768d-347">EventLog</span><span class="sxs-lookup"><span data-stu-id="9768d-347">EventLog</span></span>](#eventlog)
* [<span data-ttu-id="9768d-348">TraceSource</span><span class="sxs-lookup"><span data-stu-id="9768d-348">TraceSource</span></span>](#tracesource)
* [<span data-ttu-id="9768d-349">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="9768d-349">Azure App Service</span></span>](#appservice)

<a id="console"></a>
### <a name="the-console-provider"></a><span data-ttu-id="9768d-350">콘솔 공급자</span><span class="sxs-lookup"><span data-stu-id="9768d-350">The console provider</span></span>

<span data-ttu-id="9768d-351">[Microsoft.Extensions.Logging.Console](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Console) 공급자 패키지는 콘솔에 로그 출력을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-351">The [Microsoft.Extensions.Logging.Console](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Console) provider package sends log output to the console.</span></span> 

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9768d-352">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9768d-352">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
logging.AddConsole()
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9768d-353">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9768d-353">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
loggerFactory.AddConsole()
```

<span data-ttu-id="9768d-354">[AddConsole 오버로드](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.consoleloggerextensions)를 사용하여 최소 로그 수준, 필터 함수 및 범위 지원 여부를 나타내는 부울을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-354">[AddConsole overloads](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.consoleloggerextensions) let you pass in an a minimum log level, a filter function, and a boolean that indicates whether scopes are supported.</span></span> <span data-ttu-id="9768d-355">다른 옵션으로는 `IConfiguration` 개체를 전달할 수 있으며, 이 개체는 범위 지원 및 로깅 수준을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-355">Another option is to pass in an `IConfiguration` object, which can specify scopes support and logging levels.</span></span> 

<span data-ttu-id="9768d-356">프로덕션 환경에서 콘솔 공급자를 사용하려고 생각 중인 경우 성능에 상당한 영향이 있다는 점에 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-356">If you are considering the console provider for use in production, be aware that it has a significant impact on performance.</span></span>

<span data-ttu-id="9768d-357">Visual Studio에서 새 프로젝트를 만들면 `AddConsole` 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-357">When you create a new project in Visual Studio, the `AddConsole` method looks like this:</span></span>

```csharp
loggerFactory.AddConsole(Configuration.GetSection("Logging"));
```

<span data-ttu-id="9768d-358">이 코드는 *appSettings.json* 파일의 `Logging` 섹션을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-358">This code refers to the `Logging` section of the *appSettings.json* file:</span></span>

[!code-json[](index/sample//appsettings.json)]

<span data-ttu-id="9768d-359">[로그 필터링](#log-filtering) 섹션에서 설명했듯이, 제한 프레임워크를 표시한 설정은 경고에 기록되는 한편 앱이 디버그 수준에서 기록하는 것을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-359">The settings shown limit framework logs to warnings while allowing the app to log at debug level, as explained in the [Log filtering](#log-filtering) section.</span></span> <span data-ttu-id="9768d-360">자세한 내용은 [구성](xref:fundamentals/configuration/index)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9768d-360">For more information, see [Configuration](xref:fundamentals/configuration/index).</span></span>

---

<a id="debug"></a>
### <a name="the-debug-provider"></a><span data-ttu-id="9768d-361">디버그 공급자</span><span class="sxs-lookup"><span data-stu-id="9768d-361">The Debug provider</span></span>

<span data-ttu-id="9768d-362">[Microsoft.Extensions.Logging.Debug](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Debug) 공급자 패키지는 [System.Diagnostics.Debug](https://docs.microsoft.com/dotnet/core/api/system.diagnostics.debug#System_Diagnostics_Debug) 클래스(`Debug.WriteLine` 메서드 호출)를 사용하여 로그 출력을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-362">The [Microsoft.Extensions.Logging.Debug](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Debug) provider package writes log output by using the [System.Diagnostics.Debug](https://docs.microsoft.com/dotnet/core/api/system.diagnostics.debug#System_Diagnostics_Debug) class (`Debug.WriteLine` method calls).</span></span>

<span data-ttu-id="9768d-363">Linux에서 이 공급자는 */var/log/message*에 로그를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-363">On Linux, this provider writes logs to */var/log/message*.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9768d-364">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9768d-364">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
logging.AddDebug()
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9768d-365">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9768d-365">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
loggerFactory.AddDebug()
```

<span data-ttu-id="9768d-366">[AddDebug 오버로드](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.debugloggerfactoryextensions)를 사용하여 최소 수준 로그 또는 필터 함수를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-366">[AddDebug overloads](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.debugloggerfactoryextensions) let you pass in a minimum log level or a filter function.</span></span>

---

<a id="eventsource"></a>
### <a name="the-eventsource-provider"></a><span data-ttu-id="9768d-367">EventSource 공급자</span><span class="sxs-lookup"><span data-stu-id="9768d-367">The EventSource provider</span></span>

<span data-ttu-id="9768d-368">ASP.NET Core 1.1.0을 대상으로 하는 앱의 경우 [Microsoft.Extensions.Logging.EventSource](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventSource) 공급자 패키지가 이벤트 추적을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-368">For apps that target ASP.NET Core 1.1.0 or higher, the [Microsoft.Extensions.Logging.EventSource](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventSource) provider package can implement event tracing.</span></span> <span data-ttu-id="9768d-369">Windows에서는 [ETW](https://msdn.microsoft.com/library/windows/desktop/bb968803)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-369">On Windows, it uses [ETW](https://msdn.microsoft.com/library/windows/desktop/bb968803).</span></span> <span data-ttu-id="9768d-370">플랫폼 간 공급자이지만 이벤트를 수집하지 않으며 Linux 또는 macOS용 도구를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-370">The provider is cross-platform, but there are no event collection and display tools yet for Linux or macOS.</span></span> 

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9768d-371">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9768d-371">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
logging.AddEventSourceLogger()
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9768d-372">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9768d-372">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
loggerFactory.AddEventSourceLogger()
```

---

<span data-ttu-id="9768d-373">로그를 수집하고 보는 좋은 방법은 [PerfView 유틸리티](https://www.microsoft.com/download/details.aspx?id=28567)를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-373">A good way to collect and view logs is to use the [PerfView utility](https://www.microsoft.com/download/details.aspx?id=28567).</span></span> <span data-ttu-id="9768d-374">ETW 로그를 보는 다른 도구가 있지만, PerfView는 ASP.NET에서 내보내는 ETW 이벤트를 처리하기에 가장 좋은 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-374">There are other tools for viewing ETW logs, but PerfView provides the best experience for working with the ETW events emitted by ASP.NET.</span></span> 

<span data-ttu-id="9768d-375">이 공급자가 기록한 이벤트를 수집하도록 PerfView를 구성하려면 **추가 공급자** 목록에 `*Microsoft-Extensions-Logging` 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-375">To configure PerfView for collecting events logged by this provider, add the string `*Microsoft-Extensions-Logging` to the **Additional Providers** list.</span></span> <span data-ttu-id="9768d-376">(문자열의 시작 부분에 별표를 누락하지 마세요.)</span><span class="sxs-lookup"><span data-stu-id="9768d-376">(Don't miss the asterisk at the start of the string.)</span></span>

![Perfview 추가 공급자](index/_static/perfview-additional-providers.png)

<span data-ttu-id="9768d-378">Nano Server에서 이벤트를 캡처하려면 몇 가지 추가 설정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-378">Capturing events on Nano Server requires some additional setup:</span></span>

* <span data-ttu-id="9768d-379">PowerShell 원격 기능을 Nano Server에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-379">Connect PowerShell remoting to the Nano Server:</span></span>

  ```powershell
  Enter-PSSession [name]
  ```

* <span data-ttu-id="9768d-380">ETW 세션을 만합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-380">Create an ETW session:</span></span>

  ```powershell
  New-EtwTraceSession -Name "MyAppTrace" -LocalFilePath C:\trace.etl
  ```

* <span data-ttu-id="9768d-381">필요에 따라 [CLR](https://docs.microsoft.com/dotnet/framework/performance/clr-etw-providers), ASP.NET Core 등에 대한 ETW 공급자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-381">Add ETW providers for [CLR](https://docs.microsoft.com/dotnet/framework/performance/clr-etw-providers), ASP.NET Core, and others as needed.</span></span> <span data-ttu-id="9768d-382">ASP.NET Core 공급자 GUID는 `3ac73b97-af73-50e9-0822-5da4367920d0`입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-382">The ASP.NET Core provider GUID is `3ac73b97-af73-50e9-0822-5da4367920d0`.</span></span> 

  ```powershell
  Add-EtwTraceProvider -Guid "{e13c0d23-ccbc-4e12-931b-d9cc2eee27e4}" -SessionName MyAppTrace
  Add-EtwTraceProvider -Guid "{3ac73b97-af73-50e9-0822-5da4367920d0}" -SessionName MyAppTrace
  ```

* <span data-ttu-id="9768d-383">사이트를 실행하고 추적 정보에 대한 원하는 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-383">Run the site and do whatever actions you want tracing information for.</span></span>

* <span data-ttu-id="9768d-384">작업을 마쳤으면 추적 세션을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-384">Stop the tracing session when you're finished:</span></span>

  ```powershell
  Stop-EtwTraceSession -Name "MyAppTrace"
  ```

<span data-ttu-id="9768d-385">다른 Windows 버전에서 하듯이, 실행 결과로 얻은 *C:\trace.etl* 파일을 PerfView로 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-385">The resulting *C:\trace.etl* file can be analyzed with PerfView as on other editions of Windows.</span></span>

<a id="eventlog"></a>
### <a name="the-windows-eventlog-provider"></a><span data-ttu-id="9768d-386">Windows EventLog 공급자</span><span class="sxs-lookup"><span data-stu-id="9768d-386">The Windows EventLog provider</span></span>

<span data-ttu-id="9768d-387">[Microsoft.Extensions.Logging.EventLog](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventLog) 공급자 패키지는 Windows 이벤트 로그에 로그 출력을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-387">The [Microsoft.Extensions.Logging.EventLog](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventLog) provider package sends log output to the Windows Event Log.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9768d-388">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9768d-388">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
logging.AddEventLog()
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9768d-389">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9768d-389">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
loggerFactory.AddEventLog()
```

<span data-ttu-id="9768d-390">[AddEventLog 오버로드](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.eventloggerfactoryextensions)를 사용하여 `EventLogSettings` 또는 최소 로그 수준을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-390">[AddEventLog overloads](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.eventloggerfactoryextensions) let you pass in `EventLogSettings` or a minimum log level.</span></span>

---

<a id="tracesource"></a>
### <a name="the-tracesource-provider"></a><span data-ttu-id="9768d-391">TraceSource 공급자</span><span class="sxs-lookup"><span data-stu-id="9768d-391">The TraceSource provider</span></span>

<span data-ttu-id="9768d-392">[Microsoft.Extensions.Logging.TraceSource](https://www.nuget.org/packages/Microsoft.Extensions.Logging.TraceSource) 공급자 패키지는 [System.Diagnostics.TraceSource](https://docs.microsoft.com/dotnet/api/system.diagnostics.tracesource) 라이브러리 및 공급자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-392">The [Microsoft.Extensions.Logging.TraceSource](https://www.nuget.org/packages/Microsoft.Extensions.Logging.TraceSource) provider package uses the [System.Diagnostics.TraceSource](https://docs.microsoft.com/dotnet/api/system.diagnostics.tracesource) libraries and providers.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9768d-393">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9768d-393">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
logging.AddTraceSource(sourceSwitchName);
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9768d-394">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9768d-394">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
loggerFactory.AddTraceSource(sourceSwitchName);
```

---

<span data-ttu-id="9768d-395">[AddTraceSource 오버로드](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.tracesourcefactoryextensions)를 사용하여 원본 스위치 및 추적 수신기를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-395">[AddTraceSource overloads](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.tracesourcefactoryextensions) let you pass in a source switch and a trace listener.</span></span>

<span data-ttu-id="9768d-396">이 공급자를 사용하려면 응용 프로그램이 .NET Framework(.NET Core가 아닌)에서 실행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-396">To use this provider, an application has to run on the .NET Framework (rather than .NET Core).</span></span> <span data-ttu-id="9768d-397">공급자를 통해 응용 프로그램 예제에 사용된 [TextWriterTraceListener](https://docs.microsoft.com/dotnet/api/system.diagnostics.textwritertracelistenerr)처럼 다양한 [수신기](https://docs.microsoft.com/dotnet/framework/debug-trace-profile/trace-listeners)로 메시지를 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-397">The provider lets you route messages to a variety of [listeners](https://docs.microsoft.com/dotnet/framework/debug-trace-profile/trace-listeners), such as the [TextWriterTraceListener](https://docs.microsoft.com/dotnet/api/system.diagnostics.textwritertracelistenerr) used in the sample application.</span></span>

<span data-ttu-id="9768d-398">다음은 `Warning` 이상 메시지를 콘솔 창에 기록하는 `TraceSource` 공급자를 구성하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-398">The following example configures a `TraceSource` provider that logs `Warning` and higher messages to the console window.</span></span>

[!code-csharp[](index/sample/Startup.cs?name=snippet_TraceSource&highlight=9-12)]

<a id="appservice"></a>
### <a name="the-azure-app-service-provider"></a><span data-ttu-id="9768d-399">Azure App Service 공급자</span><span class="sxs-lookup"><span data-stu-id="9768d-399">The Azure App Service provider</span></span>

<span data-ttu-id="9768d-400">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices) 공급자 패키지는 Azure App Service 앱의 파일 시스템과 Azure Storage 계정의 [BLOB 저장소](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/#what-is-blob-storage)에 텍스트 파일을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-400">The [Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices) provider package writes logs to text files in an Azure App Service app's file system and to [blob storage](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/#what-is-blob-storage) in an Azure Storage account.</span></span> <span data-ttu-id="9768d-401">공급자는 ASP.NET Core 1.1.0을 대상으로 하는 앱에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-401">The provider is available only for apps that target ASP.NET Core 1.1.0 or higher.</span></span> 

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9768d-402">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9768d-402">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="9768d-403">.NET Core를 대상으로 지정하는 경우 공급자 패키지를 설치하거나 명시적으로 `AddAzureWebAppDiagnostics`을 호출하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-403">If targeting .NET Core, you don't have to install the provider package or explicitly call `AddAzureWebAppDiagnostics`.</span></span> <span data-ttu-id="9768d-404">Azure App Service에 앱을 배포하면 자동으로 앱에 공급자가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-404">The provider is automatically available to your app when you deploy the app to Azure App Service.</span></span>

<span data-ttu-id="9768d-405">.NET Framework를 대상으로 지정하는 경우 패키지 공급자를 프로젝트에 추가하고 `AddAzureWebAppDiagnostics`을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-405">If targeting .NET Framework, add the provider package to your project and invoke `AddAzureWebAppDiagnostics`:</span></span>

```csharp
logging.AddAzureWebAppDiagnostics();
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9768d-406">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9768d-406">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
loggerFactory.AddAzureWebAppDiagnostics();
```

<span data-ttu-id="9768d-407">`AddAzureWebAppDiagnostics` 오버로드를 사용하여 로깅 출력 템플릿, BLOB 이름, 파일 크기 제한 등의 기본 설정을 재정의하는 데 사용할 수 있는 [AzureAppServicesDiagnosticsSettings](https://github.com/aspnet/Logging/blob/c7d0b1b88668ff4ef8a86ea7d2ebb5ca7f88d3e0/src/Microsoft.Extensions.Logging.AzureAppServices/AzureAppServicesDiagnosticsSettings.cs)를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-407">An `AddAzureWebAppDiagnostics` overload lets you pass in [AzureAppServicesDiagnosticsSettings](https://github.com/aspnet/Logging/blob/c7d0b1b88668ff4ef8a86ea7d2ebb5ca7f88d3e0/src/Microsoft.Extensions.Logging.AzureAppServices/AzureAppServicesDiagnosticsSettings.cs) with which you can override default settings such as the logging output template, blob name, and file size limit.</span></span> <span data-ttu-id="9768d-408">(*출력 템플릿*은 `ILogger` 메서드를 호출할 때 제공하는 로그를 기반으로 모든 로그에 적용되는 메시지 템플릿입니다.)</span><span class="sxs-lookup"><span data-stu-id="9768d-408">(*Output template* is a message template that's applied to all logs on top of the one that you provide when you call an `ILogger` method.)</span></span>

---

<span data-ttu-id="9768d-409">App Service 앱에 배포할 때 응용 프로그램은 Azure Portal **App Service** 페이지의 [진단 로그](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/#enablediag) 섹션에 있는 설정을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-409">When you deploy to an App Service app, your application honors the settings in the [Diagnostic Logs](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/#enablediag) section of the **App Service** page of the Azure portal.</span></span> <span data-ttu-id="9768d-410">이러한 설정을 변경하면 앱을 다시 시작하거나 코드를 다시 배포할 필요 없이 변경 내용이 즉시 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-410">When you change those settings, the changes take effect immediately without requiring that you restart the app or redeploy code to it.</span></span> 

![Azure 로깅 설정](index/_static/azure-logging-settings.png)

<span data-ttu-id="9768d-412">로그 파일의 기본 위치는 *D:\\home\\LogFiles\\Application* 폴더이며, 기본 파일 이름은 *diagnostics-yyyymmdd.txt*입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-412">The default location for log files is in the *D:\\home\\LogFiles\\Application* folder, and the default file name is *diagnostics-yyyymmdd.txt*.</span></span> <span data-ttu-id="9768d-413">기본 파일 크기 제한은 10MB이고, 보존되는 기본 최대 파일 수는 2입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-413">The default file size limit is 10 MB, and the default maximum number of files retained is 2.</span></span> <span data-ttu-id="9768d-414">기본 BLOB 이름은 *{app-name}{timestamp}/yyyy/mm/dd/hh/{guid}-applicationLog.txt*입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-414">The default blob name is *{app-name}{timestamp}/yyyy/mm/dd/hh/{guid}-applicationLog.txt*.</span></span> <span data-ttu-id="9768d-415">기본 동작에 대한 자세한 내용은 [AzureAppServicesDiagnosticsSettings](https://github.com/aspnet/Logging/blob/c7d0b1b88668ff4ef8a86ea7d2ebb5ca7f88d3e0/src/Microsoft.Extensions.Logging.AzureAppServices/AzureAppServicesDiagnosticsSettings.cs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9768d-415">For more information about default behavior, see [AzureAppServicesDiagnosticsSettings](https://github.com/aspnet/Logging/blob/c7d0b1b88668ff4ef8a86ea7d2ebb5ca7f88d3e0/src/Microsoft.Extensions.Logging.AzureAppServices/AzureAppServicesDiagnosticsSettings.cs).</span></span>

<span data-ttu-id="9768d-416">공급자는 프로젝트가 Azure 환경에서 실행되는 경우에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-416">The provider only works when your project runs in the Azure environment.</span></span> <span data-ttu-id="9768d-417">로컬로 실행하는 경우에는 아무 영향도 없습니다. BLOB에 대한 로컬 파일 또는 로컬 개발 저장소에 기록하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-417">It has no effect when you run locally &mdash; it does not write to local files or local development storage for blobs.</span></span>

## <a name="third-party-logging-providers"></a><span data-ttu-id="9768d-418">타사 로깅 공급자</span><span class="sxs-lookup"><span data-stu-id="9768d-418">Third-party logging providers</span></span>

<span data-ttu-id="9768d-419">다음은 ASP.NET Core와 호환되는 일부 타사 로깅 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-419">Here are some third-party logging frameworks that work with ASP.NET Core:</span></span>

* <span data-ttu-id="9768d-420">[elmah.io](https://github.com/elmahio/Elmah.Io.Extensions.Logging) - Elmah.Io 서비스의 공급자</span><span class="sxs-lookup"><span data-stu-id="9768d-420">[elmah.io](https://github.com/elmahio/Elmah.Io.Extensions.Logging) - provider for the Elmah.Io service</span></span>

* <span data-ttu-id="9768d-421">[JSNLog](http://jsnlog.com) - 서버 쪽 로그에 JavaScript 예외 및 기타 클라이언트 쪽 이벤트를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-421">[JSNLog](http://jsnlog.com) - logs JavaScript exceptions and other client-side events in your server-side log.</span></span>

* <span data-ttu-id="9768d-422">[Loggr](https://github.com/imobile3/Loggr.Extensions.Logging) - Loggr 서비스의 공급자</span><span class="sxs-lookup"><span data-stu-id="9768d-422">[Loggr](https://github.com/imobile3/Loggr.Extensions.Logging) - provider for the Loggr service</span></span>

* <span data-ttu-id="9768d-423">[NLog](https://github.com/NLog/NLog.Extensions.Logging) - NLog 라이브러리의 공급자</span><span class="sxs-lookup"><span data-stu-id="9768d-423">[NLog](https://github.com/NLog/NLog.Extensions.Logging) - provider for the NLog library</span></span>

* <span data-ttu-id="9768d-424">[Serilog](https://github.com/serilog/serilog-extensions-logging) - Serilog 라이브러리의 공급자</span><span class="sxs-lookup"><span data-stu-id="9768d-424">[Serilog](https://github.com/serilog/serilog-extensions-logging) - provider for the Serilog library</span></span>

<span data-ttu-id="9768d-425">일부 타사 프레임워크는 [구조적 로깅이라고도 하는 의미 체계 로깅](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging)을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-425">Some third-party frameworks can do [semantic logging, also known as structured logging](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging).</span></span>

<span data-ttu-id="9768d-426">타사 프레임워크를 사용하는 방법은 기본 공급자 중 하나를 사용하는 방법과 비슷합니다. 프로젝트에 NuGet 패키지를 추가하고 `ILoggerFactory`에 대한 확장 메서드를 호출하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-426">Using a third-party framework is similar to using one of the built-in providers: add a NuGet package to your project and call an extension method on `ILoggerFactory`.</span></span> <span data-ttu-id="9768d-427">자세한 내용은 각 프레임워크의 설명서를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="9768d-427">For more information, see each framework's documentation.</span></span>

<span data-ttu-id="9768d-428">다른 로깅 프레임워크 또는 개발자 고유의 로깅 요구 사항을 지원하는 사용자 지정 공급자를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-428">You can create your own custom providers as well, to support other logging frameworks or your own logging requirements.</span></span>

## <a name="azure-log-streaming"></a><span data-ttu-id="9768d-429">Azure 로그 스트리밍</span><span class="sxs-lookup"><span data-stu-id="9768d-429">Azure log streaming</span></span>

<span data-ttu-id="9768d-430">Azure 로그 스트리밍을 통해 로그 작업을 실시간으로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-430">Azure log streaming enables you to view log activity in real time from:</span></span> 

* <span data-ttu-id="9768d-431">응용 프로그램 서버</span><span class="sxs-lookup"><span data-stu-id="9768d-431">The application server</span></span> 
* <span data-ttu-id="9768d-432">웹 서버</span><span class="sxs-lookup"><span data-stu-id="9768d-432">The web server</span></span>
* <span data-ttu-id="9768d-433">실패한 요청 추적</span><span class="sxs-lookup"><span data-stu-id="9768d-433">Failed request tracing</span></span> 

<span data-ttu-id="9768d-434">Azure 로그 스트리밍을 구성하려면:</span><span class="sxs-lookup"><span data-stu-id="9768d-434">To configure Azure log streaming:</span></span> 

* <span data-ttu-id="9768d-435">응용 프로그램의 포털 페이지에서 **진단 로그** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-435">Navigate to the **Diagnostics Logs** page from your application's portal page</span></span>
* <span data-ttu-id="9768d-436">**응용 프로그램 로깅(파일 시스템)**을 켭니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-436">Set **Application Logging (Filesystem)** to on.</span></span> 

![Azure Portal 진단 로그 페이지](index/_static/azure-diagnostic-logs.png)

<span data-ttu-id="9768d-438">**로그 스트리밍** 페이지로 이동하여 응용 프로그램 메시지를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-438">Navigate to the **Log Streaming** page to view application messages.</span></span> <span data-ttu-id="9768d-439">응용 프로그램이 `ILogger` 인터페이스를 통해 기록한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9768d-439">They are logged by application through the `ILogger` interface.</span></span> 

![Azure Portal 응용 프로그램 로그 스트리밍](index/_static/azure-log-streaming.png)


## <a name="see-also"></a><span data-ttu-id="9768d-441">참고 항목</span><span class="sxs-lookup"><span data-stu-id="9768d-441">See also</span></span>

[<span data-ttu-id="9768d-442">LoggerMessage를 사용한 고성능 로깅</span><span class="sxs-lookup"><span data-stu-id="9768d-442">High-performance logging with LoggerMessage</span></span>](xref:fundamentals/logging/loggermessage)
