---
title: ASP.NET Core에 로그인
author: ardalis
description: ASP.NET Core의 로깅 프레임워크에 대해 알아봅니다. 기본 제공 로깅 공급자를 살펴보고 인기 있는 타사 공급자에 대해 알아봅니다.
manager: wpickett
ms.author: tdykstra
ms.date: 12/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/logging/index
ms.openlocfilehash: 7e2a4657211b0142ec87fd792d013f7ef397de2b
ms.sourcegitcommit: 9bc34b8269d2a150b844c3b8646dcb30278a95ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/12/2018
---
# <a name="logging-in-aspnet-core"></a><span data-ttu-id="dee36-104">ASP.NET Core에 로그인</span><span class="sxs-lookup"><span data-stu-id="dee36-104">Logging in ASP.NET Core</span></span>

<span data-ttu-id="dee36-105">작성자: [Steve Smith](https://ardalis.com/) 및 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="dee36-105">By [Steve Smith](https://ardalis.com/) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="dee36-106">ASP.NET Core는 다양한 로깅 공급자를 사용하는 로깅 API를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-106">ASP.NET Core supports a logging API that works with a variety of logging providers.</span></span> <span data-ttu-id="dee36-107">기본 공급자를 통해 하나 이상의 대상에 로그를 보낼 수 있으며, 타사 로깅 프레임워크를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-107">Built-in providers let you send logs to one or more destinations, and you can plug in a third-party logging framework.</span></span> <span data-ttu-id="dee36-108">이 문서에서는 코드에 기본 제공 로깅 API 및 공급자를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-108">This article shows how to use the built-in logging API and providers in your code.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="dee36-109">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="dee36-109">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="dee36-110">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/index/sample2)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="dee36-110">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/index/sample2) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="dee36-111">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="dee36-111">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="dee36-112">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/index/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="dee36-112">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/index/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

---

## <a name="how-to-create-logs"></a><span data-ttu-id="dee36-113">로그를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="dee36-113">How to create logs</span></span>

<span data-ttu-id="dee36-114">로그를 만들려면 [종속성 주입](xref:fundamentals/dependency-injection) 컨테이너에서 `ILogger` 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-114">To create logs, get an `ILogger` object from the [dependency injection](xref:fundamentals/dependency-injection) container:</span></span>

[!code-csharp[](index/sample/Controllers/TodoController.cs?name=snippet_LoggerDI&highlight=7)]

<span data-ttu-id="dee36-115">그런 다음 해당 로거 개체에 대해 로깅 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-115">Then call logging methods on that logger object:</span></span>

[!code-csharp[](index/sample/Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

<span data-ttu-id="dee36-116">이 예에서는 *범주*로 `TodoController` 클래스를 사용하여 로그를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-116">This example creates logs with the `TodoController` class as the *category*.</span></span> <span data-ttu-id="dee36-117">범주는 [이 문서의 뒷부분](#log-category)에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-117">Categories are explained [later in this article](#log-category).</span></span>

<span data-ttu-id="dee36-118">ASP.NET Core는 비동기 로거 메서드를 제공하지 않습니다. 비동기를 사용할 필요가 없도록 로깅 속도가 아주 빠르기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-118">ASP.NET Core doesn't provide async logger methods because logging should be so fast that it isn't worth the cost of using async.</span></span> <span data-ttu-id="dee36-119">로깅 속도가 빠르지 않은 경우 로깅 방식을 변경하는 방안을 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="dee36-119">If you're in a situation where that's not true, consider changing the way you log.</span></span> <span data-ttu-id="dee36-120">데이터 저장소가 느리면 로그 메시지를 빠른 저장소에 먼저 쓴 후 나중에 느린 저장소로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-120">If your data store is slow, write the log messages to a fast store first, then move them to a slow store later.</span></span> <span data-ttu-id="dee36-121">예를 들어 다른 프로세스에서 읽고 지속하는 느린 저장소인 메시지 큐에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-121">For example, log to a message queue that's read and persisted to slow storage by another process.</span></span>

## <a name="how-to-add-providers"></a><span data-ttu-id="dee36-122">공급자를 추가하는 방법</span><span class="sxs-lookup"><span data-stu-id="dee36-122">How to add providers</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="dee36-123">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="dee36-123">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="dee36-124">로깅 공급자는 개발자가 `ILogger` 개체를 사용하여 만든 메시지를 가져와서 표시하거나 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-124">A logging provider takes the messages that you create with an `ILogger` object and displays or stores them.</span></span> <span data-ttu-id="dee36-125">예를 들어 콘솔 공급자는 콘솔에 메시지를 표시하고, Azure App Service 공급자는 메시지를 Azure BLOB 저장소에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-125">For example, the Console provider displays messages on the console, and the Azure App Service provider can store them in Azure blob storage.</span></span>

<span data-ttu-id="dee36-126">공급자를 사용하려면 *Program.cs*에서 공급자의 `Add<ProviderName>` 확장 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-126">To use a provider, call the provider's `Add<ProviderName>` extension method in *Program.cs*:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_ExpandDefault&highlight=16,17)]

<span data-ttu-id="dee36-127">기본 프로젝트 템플릿을 사용하면 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder?view=aspnetcore-2.0#Microsoft_AspNetCore_WebHost_CreateDefaultBuilder_System_String___) 메서드를 사용하여 로깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-127">The default project template enables logging with the [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder?view=aspnetcore-2.0#Microsoft_AspNetCore_WebHost_CreateDefaultBuilder_System_String___) method:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_TemplateCode&highlight=7)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="dee36-128">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="dee36-128">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="dee36-129">로깅 공급자는 개발자가 `ILogger` 개체를 사용하여 만든 메시지를 가져와서 표시하거나 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-129">A logging provider takes the messages that you create with an `ILogger` object and displays or stores them.</span></span> <span data-ttu-id="dee36-130">예를 들어 콘솔 공급자는 콘솔에 메시지를 표시하고, Azure App Service 공급자는 메시지를 Azure BLOB 저장소에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-130">For example, the Console provider displays messages on the console, and the Azure App Service provider can store them in Azure blob storage.</span></span>

<span data-ttu-id="dee36-131">공급자를 사용하려면 다음 예제처럼 NuGet 패키지를 설치하고 `ILoggerFactory` 인스턴스에 대한 공급자의 확장 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-131">To use a provider, install its NuGet package and call the provider's extension method on an instance of `ILoggerFactory`, as shown in the following example.</span></span>

[!code-csharp[](index/sample//Startup.cs?name=snippet_AddConsoleAndDebug&highlight=3,5-7)]

<span data-ttu-id="dee36-132">ASP.NET Core [DI(종속성 주입](xref:fundamentals/dependency-injection))는 `ILoggerFactory` 인스턴스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-132">ASP.NET Core [dependency injection](xref:fundamentals/dependency-injection) (DI) provides the `ILoggerFactory` instance.</span></span> <span data-ttu-id="dee36-133">`AddConsole` 및 `AddDebug` 확장 메서드는 [Microsoft.Extensions.Logging.Console](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Console/) 및 [Microsoft.Extensions.Logging.Debug](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Debug/) 패키지에 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-133">The `AddConsole` and `AddDebug` extension methods are defined in the [Microsoft.Extensions.Logging.Console](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Console/) and [Microsoft.Extensions.Logging.Debug](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Debug/) packages.</span></span> <span data-ttu-id="dee36-134">각 확장 메서드는 `ILoggerFactory.AddProvider` 메서드를 호출하고, 공급자 인스턴스를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-134">Each extension method calls the `ILoggerFactory.AddProvider` method, passing in an instance of the provider.</span></span> 

> [!NOTE]
> <span data-ttu-id="dee36-135">이 문서의 응용 프로그램 예제에서는 `Startup` 클래스의 `Configure` 메서드에 로깅을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-135">The sample application for this article adds logging providers in the `Configure` method of the `Startup` class.</span></span> <span data-ttu-id="dee36-136">먼저 실행되는 코드의 로그 출력을 가져오려면, 그 대신 `Startup` 클래스 생성자에서 로깅 공급자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-136">If you want to get log output from code that executes earlier, add logging providers in the `Startup` class constructor instead.</span></span> 

---

<span data-ttu-id="dee36-137">각 [기본 제공 로깅 공급자](#built-in-logging-providers)에 대한 정보와 [타사 로깅 공급자](#third-party-logging-providers)의 링크는 문서의 뒷부분에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-137">You'll find information about each [built-in logging provider](#built-in-logging-providers) and links to [third-party logging providers](#third-party-logging-providers) later in the article.</span></span>

## <a name="sample-logging-output"></a><span data-ttu-id="dee36-138">샘플 로깅 출력</span><span class="sxs-lookup"><span data-stu-id="dee36-138">Sample logging output</span></span>

<span data-ttu-id="dee36-139">이전 섹션에 나와 있는 샘플 코드를 사용하는 경우 명령줄에서 실행하면 콘솔에 로그가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-139">With the sample code shown in the preceding section, you'll see logs in the console when you run from the command line.</span></span> <span data-ttu-id="dee36-140">다음은 콘솔 출력의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-140">Here's an example of console output:</span></span>

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

<span data-ttu-id="dee36-141">이러한 로그는 `http://localhost:5000/api/todo/0`으로 이동하여 생성되었으며, 이는 이전 섹션에서 나온 두 `ILogger` 호출의 실행을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-141">These logs were created by going to `http://localhost:5000/api/todo/0`, which triggers execution of both `ILogger` calls shown in the preceding section.</span></span>

<span data-ttu-id="dee36-142">다음은 Visual Studio에서 응용 프로그램 예제를 실행하면 디버그 창에 표시되는 동일한 로그의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-142">Here's an example of the same logs as they appear in the Debug window when you run the sample application in Visual Studio:</span></span>

```console
Microsoft.AspNetCore.Hosting.Internal.WebHost:Information: Request starting HTTP/1.1 GET http://localhost:53104/api/todo/0  
Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker:Information: Executing action method TodoApi.Controllers.TodoController.GetById (TodoApi) with arguments (0) - ModelState is Valid
TodoApi.Controllers.TodoController:Information: Getting item 0
TodoApi.Controllers.TodoController:Warning: GetById(0) NOT FOUND
Microsoft.AspNetCore.Mvc.StatusCodeResult:Information: Executing HttpStatusCodeResult, setting HTTP status code 404
Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker:Information: Executed action TodoApi.Controllers.TodoController.GetById (TodoApi) in 152.5657ms
Microsoft.AspNetCore.Hosting.Internal.WebHost:Information: Request finished in 316.3195ms 404 
```

<span data-ttu-id="dee36-143">이전 섹션에서 `ILogger` 호출을 통해 생성된 로그는 "TodoApi.Controllers.TodoController"로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-143">The logs that were created by the `ILogger` calls shown in the preceding section begin with "TodoApi.Controllers.TodoController".</span></span> <span data-ttu-id="dee36-144">"Microsoft" 범주로 시작하는 로그는 ASP.NET Core에서 온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-144">The logs that begin with "Microsoft" categories are from ASP.NET Core.</span></span> <span data-ttu-id="dee36-145">ASP.NET Core 자체와 응용 프로그램 코드는 동일한 로깅 API와 동일한 로깅 공급자 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-145">ASP.NET Core itself and your application code are using the same logging API and the same logging providers.</span></span>

<span data-ttu-id="dee36-146">이 문서의 나머지 부분에서는 로깅에 대한 일부 세부 정보 및 옵션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-146">The remainder of this article explains some details and options for logging.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="dee36-147">NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="dee36-147">NuGet packages</span></span>

<span data-ttu-id="dee36-148">`ILogger` 및 `ILoggerFactory` 인터페이스는 [Microsoft.Extensions.Logging.Abstractions](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Abstractions/)에 있으며, 두 인터페이스의 기본 구현은 [Microsoft.Extensions.Logging](https://www.nuget.org/packages/microsoft.extensions.logging/)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-148">The `ILogger` and `ILoggerFactory` interfaces are in [Microsoft.Extensions.Logging.Abstractions](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Abstractions/), and default implementations for them are in [Microsoft.Extensions.Logging](https://www.nuget.org/packages/microsoft.extensions.logging/).</span></span>

## <a name="log-category"></a><span data-ttu-id="dee36-149">로그 범주</span><span class="sxs-lookup"><span data-stu-id="dee36-149">Log category</span></span>

<span data-ttu-id="dee36-150">*범주*는 개발자가 만드는 각 로그와 함께 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-150">A *category* is included with each log that you create.</span></span> <span data-ttu-id="dee36-151">개발자는 `ILogger` 개체를 만들 때 범주를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-151">You specify the category when you create an `ILogger` object.</span></span> <span data-ttu-id="dee36-152">모든 문자열을 범주로 사용할 수 있지만, 로그가 작성되는 클래스의 정규화된 이름을 사용해야 하는 규칙이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-152">The category may be any string, but a convention is to use the fully qualified name of the class from which the logs are written.</span></span> <span data-ttu-id="dee36-153">"TodoApi.Controllers.TodoController"를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-153">For example: "TodoApi.Controllers.TodoController".</span></span>

<span data-ttu-id="dee36-154">범주를 문자열로 지정하거나 형식에서 범주가 파생되는 확장 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-154">You can specify the category as a string or use an extension method that derives the category from the type.</span></span> <span data-ttu-id="dee36-155">범주를 문자열로 지정하려면 아래와 같이 `ILoggerFactory` 인스턴스에 대해 `CreateLogger`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-155">To specify the category as a string, call `CreateLogger` on an `ILoggerFactory` instance, as shown below.</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_CreateLogger&highlight=7,10)]

<span data-ttu-id="dee36-156">대부분의 경우 다음 예제와 같이 `ILogger<T>`를 사용하는 편이 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-156">Most of the time, it will be easier to use `ILogger<T>`, as in the following example.</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_LoggerDI&highlight=7)]

<span data-ttu-id="dee36-157">이것은 정규화된 형식 이름 `T`를 사용하여 `CreateLogger`를 호출하는 것과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-157">This is equivalent to calling `CreateLogger` with the fully qualified type name of `T`.</span></span>

## <a name="log-level"></a><span data-ttu-id="dee36-158">로그 수준</span><span class="sxs-lookup"><span data-stu-id="dee36-158">Log level</span></span>

<span data-ttu-id="dee36-159">로그를 쓸 때마다 [LogLevel](/dotnet/api/microsoft.extensions.logging.logLevel)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-159">Each time you write a log, you specify its [LogLevel](/dotnet/api/microsoft.extensions.logging.logLevel).</span></span> <span data-ttu-id="dee36-160">로그 수준은 심각도 또는 중요도 수준을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-160">The log level indicates the degree of severity or importance.</span></span> <span data-ttu-id="dee36-161">예를 들어 메서드가 정상적으로 종료되면 `Information` 로그를 쓰고, 메서드가 404 반환 코드를 반환하면 `Warning` 로그를 쓰고, 예기치 않은 예외를 catch하면 `Error` 로그를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-161">For example, you might write an `Information` log when a method ends normally, a `Warning` log when a method returns a 404 return code, and an `Error` log when you catch an unexpected exception.</span></span>

<span data-ttu-id="dee36-162">다음 코드 예제에서 메서드 이름(예: `LogWarning`)은 로그 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-162">In the following code example, the names of the methods (for example, `LogWarning`) specify the log level.</span></span> <span data-ttu-id="dee36-163">첫 번째 매개 변수는 [Log event ID](#log-event-id)입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-163">The first parameter is the [Log event ID](#log-event-id).</span></span> <span data-ttu-id="dee36-164">두 번째 매개 변수는 [message template](#log-message-template)으로, 나머지 메서드 매개 변수에서 인수 값에 대한 자리 표시자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-164">The second parameter is a [message template](#log-message-template) with placeholders for argument values provided by the remaining method parameters.</span></span> <span data-ttu-id="dee36-165">메서드 매개 변수는 이 문서의 뒷부분에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-165">The method parameters are explained in more detail later in this article.</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

<span data-ttu-id="dee36-166">메서드 이름에 수준을 포함하는 로그 메서드는 [ILogger에 대한 확장 메서드](/dotnet/api/microsoft.extensions.logging.loggerextensions)입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-166">Log methods that include the level in the method name are [extension methods for ILogger](/dotnet/api/microsoft.extensions.logging.loggerextensions).</span></span> <span data-ttu-id="dee36-167">백그라운드에서 이러한 메서드는 `LogLevel` 매개 변수를 사용하는 `Log` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-167">Behind the scenes, these methods call a `Log` method that takes a `LogLevel` parameter.</span></span> <span data-ttu-id="dee36-168">이러한 확장 메서드 중 하나를 호출하는 대신 `Log` 메서드를 직접 호출할 수 있지만, 구문이 비교적 복잡합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-168">You can call the `Log` method directly rather than one of these extension methods, but the syntax is relatively complicated.</span></span> <span data-ttu-id="dee36-169">자세한 내용은 [ILogger 인터페이스](/dotnet/api/microsoft.extensions.logging.ilogger) 및 [로거 확장 소스 코드](https://github.com/aspnet/Logging/blob/master/src/Microsoft.Extensions.Logging.Abstractions/LoggerExtensions.cs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dee36-169">For more information, see the [ILogger interface](/dotnet/api/microsoft.extensions.logging.ilogger) and the [logger extensions source code](https://github.com/aspnet/Logging/blob/master/src/Microsoft.Extensions.Logging.Abstractions/LoggerExtensions.cs).</span></span>

<span data-ttu-id="dee36-170">ASP.NET Core는 다음 [로그 수준](/dotnet/api/microsoft.extensions.logging.loglevel)을 정의하며, 여기에 가장 낮은 심각도에서 가장 높은 심각도 순으로 정렬됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-170">ASP.NET Core defines the following [log levels](/dotnet/api/microsoft.extensions.logging.loglevel), ordered here from least to highest severity.</span></span>

* <span data-ttu-id="dee36-171">추적 = 0</span><span class="sxs-lookup"><span data-stu-id="dee36-171">Trace = 0</span></span>

  <span data-ttu-id="dee36-172">문제를 디버깅하는 개발자에게만 중요한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-172">For information that's valuable only to a developer debugging an issue.</span></span> <span data-ttu-id="dee36-173">이러한 메시지는 중요한 응용 프로그램 데이터를 포함할 수 있으므로 프로덕션 환경에서 사용하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-173">These messages may contain sensitive application data and so shouldn't be enabled in a production environment.</span></span> <span data-ttu-id="dee36-174">*기본적으로 사용하지 않도록 설정됩니다.*</span><span class="sxs-lookup"><span data-stu-id="dee36-174">*Disabled by default.*</span></span> <span data-ttu-id="dee36-175">예: `Credentials: {"User":"someuser", "Password":"P@ssword"}`</span><span class="sxs-lookup"><span data-stu-id="dee36-175">Example: `Credentials: {"User":"someuser", "Password":"P@ssword"}`</span></span>

* <span data-ttu-id="dee36-176">디버그 = 1</span><span class="sxs-lookup"><span data-stu-id="dee36-176">Debug = 1</span></span>

  <span data-ttu-id="dee36-177">개발 및 디버깅하는 동안 단기적으로 유용한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-177">For information that has short-term usefulness during development and debugging.</span></span> <span data-ttu-id="dee36-178">예: 로그 볼륨이 크기 때문에 문제를 해결하려는 경우 외에는 프로덕션 환경에서 `Entering method Configure with flag set to true.`일반적으로 수준 로그를 사용하지 않습니다`Debug`.</span><span class="sxs-lookup"><span data-stu-id="dee36-178">Example: `Entering method Configure with flag set to true.` You typically wouldn't enable `Debug` level logs in production unless you are troubleshooting, due to the high volume of logs.</span></span>

* <span data-ttu-id="dee36-179">정보 = 2</span><span class="sxs-lookup"><span data-stu-id="dee36-179">Information = 2</span></span>

  <span data-ttu-id="dee36-180">응용 프로그램의 일반적인 흐름을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-180">For tracking the general flow of the application.</span></span> <span data-ttu-id="dee36-181">이러한 로그는 일반적으로 장기적인 가치가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-181">These logs typically have some long-term value.</span></span> <span data-ttu-id="dee36-182">예: `Request received for path /api/todo`</span><span class="sxs-lookup"><span data-stu-id="dee36-182">Example: `Request received for path /api/todo`</span></span>

* <span data-ttu-id="dee36-183">경고 = 3</span><span class="sxs-lookup"><span data-stu-id="dee36-183">Warning = 3</span></span>

  <span data-ttu-id="dee36-184">응용 프로그램 흐름에 비정상적인 또는 예기치 않은 이벤트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-184">For abnormal or unexpected events in the application flow.</span></span> <span data-ttu-id="dee36-185">응용 프로그램을 중지하지는 않지만 조사할 필요가 있는 오류 또는 기타 조건도 여기에 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-185">These may include errors or other conditions that don't cause the application to stop, but which may need to be investigated.</span></span> <span data-ttu-id="dee36-186">처리된 예외는 `Warning` 로그 수준을 사용하는 일반적인 장소입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-186">Handled exceptions are a common place to use the `Warning` log level.</span></span> <span data-ttu-id="dee36-187">예: `FileNotFoundException for file quotes.txt.`</span><span class="sxs-lookup"><span data-stu-id="dee36-187">Example: `FileNotFoundException for file quotes.txt.`</span></span>

* <span data-ttu-id="dee36-188">오류 = 4</span><span class="sxs-lookup"><span data-stu-id="dee36-188">Error = 4</span></span>

  <span data-ttu-id="dee36-189">처리할 수 없는 오류 및 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-189">For errors and exceptions that cannot be handled.</span></span> <span data-ttu-id="dee36-190">이러한 메시지는 전체 응용 프로그램 오류가 아닌 현재 동작 또는 작업(예: 현재 HTTP 요청)의 오류를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-190">These messages indicate a failure in the current activity or operation (such as the current HTTP request), not an application-wide failure.</span></span> <span data-ttu-id="dee36-191">예제 로그 메시지: `Cannot insert record due to duplicate key violation.`</span><span class="sxs-lookup"><span data-stu-id="dee36-191">Example log message: `Cannot insert record due to duplicate key violation.`</span></span>

* <span data-ttu-id="dee36-192">중요 = 5</span><span class="sxs-lookup"><span data-stu-id="dee36-192">Critical = 5</span></span>

  <span data-ttu-id="dee36-193">즉각적인 대응이 필요한 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-193">For failures that require immediate attention.</span></span> <span data-ttu-id="dee36-194">예: 데이터 손실 시나리오, 디스크 공간 부족.</span><span class="sxs-lookup"><span data-stu-id="dee36-194">Examples: data loss scenarios, out of disk space.</span></span>

<span data-ttu-id="dee36-195">로그 수준을 사용하여 특정 저장 매체 또는 디스플레이 창에 기록되는 로그 출력의 양을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-195">You can use the log level to control how much log output is written to a particular storage medium or display window.</span></span> <span data-ttu-id="dee36-196">예를 들어 프로덕션 환경에서 `Information` 수준 이하의 모든 로그는 볼륨 데이터 저장소로 이동하고, `Warning` 수준 이상의 모든 로그는 가치 데이터 저장소로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-196">For example, in production you might want all logs of `Information` level and lower to go to a volume data store, and all logs of `Warning` level and higher to go to a value data store.</span></span> <span data-ttu-id="dee36-197">개발하는 동안 심각도가 `Warning` 이상인 로그는 일반적으로 콘솔로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-197">During development, you might normally send logs of `Warning` or higher severity to the console.</span></span> <span data-ttu-id="dee36-198">문제를 해결해야 하는 상황이 오면 `Debug` 수준을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-198">Then when you need to troubleshoot, you can add `Debug` level.</span></span> <span data-ttu-id="dee36-199">이 문서의 뒷부분에 나오는 [로그 필터링](#log-filtering) 섹션에서는 공급자가 처리하는 로그 수준을 제어하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-199">The [Log filtering](#log-filtering) section later in this article explains how to control which log levels a provider handles.</span></span>

<span data-ttu-id="dee36-200">ASP.NET Core 프레임워크는 프레임워크 이벤트에 대한 `Debug` 수준 로그를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-200">The ASP.NET Core framework writes `Debug` level logs for framework events.</span></span> <span data-ttu-id="dee36-201">이 문서 앞부분에 나온 로그 예제는 `Information` 수준 미만 로그를 제외했기 때문에 `Debug` 수준 로그가 하나도 표시되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-201">The log examples earlier in this article excluded logs below `Information` level, so no `Debug` level logs were shown.</span></span> <span data-ttu-id="dee36-202">다음은 콘솔 공급자에 대해 `Debug` 이상 로그를 표시하도록 구성된 응용 프로그램 예제를 실행할 경우의 콘솔 로그 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-202">Here's an example of console logs if you run the sample application configured to show `Debug` and higher logs for the console provider.</span></span>

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

## <a name="log-event-id"></a><span data-ttu-id="dee36-203">로그 이벤트 ID</span><span class="sxs-lookup"><span data-stu-id="dee36-203">Log event ID</span></span>

<span data-ttu-id="dee36-204">로그를 쓸 때마다 *이벤트 ID*를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-204">Each time you write a log, you can specify an *event ID*.</span></span> <span data-ttu-id="dee36-205">샘플 앱은 로컬로 정의된 `LoggingEvents` 클래스를 사용하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-205">The sample app does this by using a locally-defined `LoggingEvents` class:</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

[!code-csharp[](index/sample//Core/LoggingEvents.cs?name=snippet_LoggingEvents)]

<span data-ttu-id="dee36-206">이벤트 ID는 로깅된 이벤트 집합을 서로 연결하는 데 사용할 수 있는 정수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-206">An event ID is an integer value that you can use to associate a set of logged events with one another.</span></span> <span data-ttu-id="dee36-207">예를 들어 장바구니에 항목 추가에 대한 로그는 이벤트 ID 1000이고 구매 완료에 대한 로그는 이벤트 ID 1001입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-207">For instance, a log for adding an item to a shopping cart could be event ID 1000 and a log for completing a purchase could be event ID 1001.</span></span>

<span data-ttu-id="dee36-208">로깅 출력에서 이벤트 ID는 공급자에 따라 필드에 저장되거나 텍스트 메시지에 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-208">In logging output, the event ID may be stored in a field or included in the text message, depending on the provider.</span></span> <span data-ttu-id="dee36-209">디버그 공급자는 이벤트 ID를 표시하지 않지만, 콘솔 공급자는 범주 뒤에서 대괄호 안에 이벤트 ID를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-209">The Debug provider doesn't show event IDs, but the console provider shows them in brackets after the category:</span></span>

```console
info: TodoApi.Controllers.TodoController[1002]
      Getting item invalidid
warn: TodoApi.Controllers.TodoController[4000]
      GetById(invalidid) NOT FOUND
```

## <a name="log-message-template"></a><span data-ttu-id="dee36-210">로그 메시지 템플릿</span><span class="sxs-lookup"><span data-stu-id="dee36-210">Log message template</span></span>

<span data-ttu-id="dee36-211">로그 메시지를 쓸 때마다 메시지 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-211">Each time you write a log message, you provide a message template.</span></span> <span data-ttu-id="dee36-212">메시지 템플릿은 문자열일 수도 있고, 인수 값이 배치되는 명명된 자리 표시자를 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-212">The message template can be a string or it can contain named placeholders into which argument values are placed.</span></span> <span data-ttu-id="dee36-213">템플릿은 형식 문자열이 아니고, 자리 표시자는 번호가 아닌 이름이 지정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-213">The template isn't a format string, and placeholders should be named, not numbered.</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

<span data-ttu-id="dee36-214">값을 제공하는 데 사용되는 매개 변수를 결정하는 것은 자리 표시자의 번호가 아닌 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-214">The order of placeholders, not their names, determines which parameters are used to provide their values.</span></span> <span data-ttu-id="dee36-215">다음과 같은 코드를 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-215">If you have the following code:</span></span>

```csharp
string p1 = "parm1";
string p2 = "parm2";
_logger.LogInformation("Parameter values: {p2}, {p1}", p1, p2);
```

<span data-ttu-id="dee36-216">결과로 만들어진 로그 메시지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-216">The resulting log message looks like this:</span></span>

```
Parameter values: parm1, parm2
```

<span data-ttu-id="dee36-217">로깅 프레임워크는 이 방식으로 메시지를 포맷하여 로깅 공급자가 [구조적 로깅이라고도 하는 의미 체계 로깅](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging)을 구현할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-217">The logging framework does message formatting in this way to make it possible for logging providers to implement [semantic logging, also known as structured logging](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging).</span></span> <span data-ttu-id="dee36-218">인수 자체는 포맷된 메시지 템플릿이 아닌 로깅 시스템으로 전달되기 때문에 로깅 공급자가 메시지 템플릿 외에도 매개 변수 값을 필드로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-218">Because the arguments themselves are passed to the logging system, not just the formatted message template, logging providers can store the parameter values as fields in addition to the message template.</span></span> <span data-ttu-id="dee36-219">로그 출력을 Azure Table Storage로 전달하는 경우 로거 메서드 호출은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-219">If you're directing your log output to Azure Table Storage and your logger method call looks like this:</span></span>

```csharp
_logger.LogInformation("Getting item {ID} at {RequestTime}", id, DateTime.Now);
```

<span data-ttu-id="dee36-220">각 Azure Table 엔터티는 로그 데이터에 대한 쿼리를 간소화하는 `ID` 및 `RequestTime` 속성을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-220">Each Azure Table entity can have `ID` and `RequestTime` properties, which simplifies queries on log data.</span></span> <span data-ttu-id="dee36-221">문자 메시지의 시간 초과를 구문 분석할 필요 없이 특정 `RequestTime` 범위 내에서 모든 로그를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-221">You can find all logs within a particular `RequestTime` range without the need to parse the time out of the text message.</span></span>

## <a name="logging-exceptions"></a><span data-ttu-id="dee36-222">로깅 처리</span><span class="sxs-lookup"><span data-stu-id="dee36-222">Logging exceptions</span></span>

<span data-ttu-id="dee36-223">로거 메서드는 다음 예제와 같이 예외를 전달할 수 있는 오버로드를 갖고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-223">The logger methods have overloads that let you pass in an exception, as in the following example:</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_LogException&highlight=3)]

<span data-ttu-id="dee36-224">공급자들은 다양한 방식으로 예외 정보를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-224">Different providers handle the exception information in different ways.</span></span> <span data-ttu-id="dee36-225">다음은 위에서 보여드린 코드의 디버그 공급자 출력의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-225">Here's an example of Debug provider output from the code shown above.</span></span>

```
TodoApi.Controllers.TodoController:Warning: GetById(036dd898-fb01-47e8-9a65-f92eb73cf924) NOT FOUND

System.Exception: Item not found exception.
 at TodoApi.Controllers.TodoController.GetById(String id) in C:\logging\sample\src\TodoApi\Controllers\TodoController.cs:line 226
```

## <a name="log-filtering"></a><span data-ttu-id="dee36-226">로깅 필터링</span><span class="sxs-lookup"><span data-stu-id="dee36-226">Log filtering</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="dee36-227">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="dee36-227">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="dee36-228">특정 공급자 및 범주 또는 모든 공급자나 모든 범주의 최소 로그 수준을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-228">You can specify a minimum log level for a specific provider and category or for all providers or all categories.</span></span> <span data-ttu-id="dee36-229">최소 수준 미만인 로그는 해당 공급자에게 전달되지 않으므로 표시되거나 저장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-229">Any logs below the minimum level aren't passed to that provider, so they don't get displayed or stored.</span></span> 

<span data-ttu-id="dee36-230">모든 로그를 표시하지 않으려면 최소 로그 수준으로 `LogLevel.None`을 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-230">If you want to suppress all logs, you can specify `LogLevel.None` as the minimum log level.</span></span> <span data-ttu-id="dee36-231">`LogLevel.None`의 정수 값은 `LogLevel.Critical`(5)보다 높은 6입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-231">The integer value of `LogLevel.None` is 6, which is higher than `LogLevel.Critical` (5).</span></span>

<span data-ttu-id="dee36-232">**구성에서 필터 규칙 만들기**</span><span class="sxs-lookup"><span data-stu-id="dee36-232">**Create filter rules in configuration**</span></span>

<span data-ttu-id="dee36-233">프로젝트 템플릿은 콘솔 및 디버그 공급자에 대한 로깅을 설정하는 `CreateDefaultBuilder`를 호출하는 코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-233">The project templates create code that calls `CreateDefaultBuilder` to set up logging for the Console and Debug providers.</span></span> <span data-ttu-id="dee36-234">또한 `CreateDefaultBuilder` 메서드는 다음과 같은 코드를 사용하여 `Logging` 섹션에서 구성을 조회하는 로깅을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-234">The `CreateDefaultBuilder` method also sets up logging to look for configuration in a `Logging` section, using code like the following:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_ExpandDefault&highlight=15)]

<span data-ttu-id="dee36-235">구성 데이터는 다음 예제와 같이 공급자 및 범주별로 최소 로그 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-235">The configuration data specifies minimum log levels by provider and category, as in the following example:</span></span>

[!code-json[](index/sample2/appsettings.json)]

<span data-ttu-id="dee36-236">이 JSON은 6개의 필터 규칙을 만드는데, 하나는 디버그 공급자용이고, 4개는 콘솔 공급자용이고, 나머지 하나는 모든 공급자에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-236">This JSON creates six filter rules, one for the Debug provider, four for the Console provider, and one that applies to all providers.</span></span> <span data-ttu-id="dee36-237">`ILogger` 개체가 생성될 때 각 공급자에 대해 이러한 규칙 중 하나를 선택하는 방법은 나중에 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-237">You'll see later how just one of these rules is chosen for each provider when an `ILogger` object is created.</span></span>

<span data-ttu-id="dee36-238">**코드의 필터 규칙**</span><span class="sxs-lookup"><span data-stu-id="dee36-238">**Filter rules in code**</span></span>

<span data-ttu-id="dee36-239">다음 예제와 같이 코드에서 필터 규칙을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-239">You can register filter rules in code, as shown in the following example:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_FilterInCode&highlight=4-5)]

<span data-ttu-id="dee36-240">두 번째 `AddFilter`는 형식 이름을 사용하여 디버그 공급자를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-240">The second `AddFilter` specifies the Debug provider by using its type name.</span></span> <span data-ttu-id="dee36-241">첫 번째 `AddFilter`는 공급자 형식을 지정하지 않으며, 따라서 모든 공급자에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-241">The first `AddFilter` applies to all providers because it doesn't specify a provider type.</span></span>

<span data-ttu-id="dee36-242">**필터링 규칙 적용 방식**</span><span class="sxs-lookup"><span data-stu-id="dee36-242">**How filtering rules are applied**</span></span>

<span data-ttu-id="dee36-243">이전 예제의 구성 데이터 및 `AddFilter` 코드는 다음 표에 표시된 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-243">The configuration data and the `AddFilter` code shown in the preceding examples create the rules shown in the following table.</span></span> <span data-ttu-id="dee36-244">처음 6개는 구성 예제에서 가져온 것이고 마지막 2개는 코드 예제에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-244">The first six come from the configuration example and the last two come from the code example.</span></span>

| <span data-ttu-id="dee36-245">수</span><span class="sxs-lookup"><span data-stu-id="dee36-245">Number</span></span> | <span data-ttu-id="dee36-246">공급자</span><span class="sxs-lookup"><span data-stu-id="dee36-246">Provider</span></span>      | <span data-ttu-id="dee36-247">다음으로 시작하는 범주...</span><span class="sxs-lookup"><span data-stu-id="dee36-247">Categories that begin with ...</span></span>          | <span data-ttu-id="dee36-248">최소 로그 수준</span><span class="sxs-lookup"><span data-stu-id="dee36-248">Minimum log level</span></span> |
| :----: | ------------- | --------------------------------------- | ----------------- |
| <span data-ttu-id="dee36-249">1</span><span class="sxs-lookup"><span data-stu-id="dee36-249">1</span></span>      | <span data-ttu-id="dee36-250">디버그</span><span class="sxs-lookup"><span data-stu-id="dee36-250">Debug</span></span>         | <span data-ttu-id="dee36-251">모든 범주</span><span class="sxs-lookup"><span data-stu-id="dee36-251">All categories</span></span>                          | <span data-ttu-id="dee36-252">정보</span><span class="sxs-lookup"><span data-stu-id="dee36-252">Information</span></span>       |
| <span data-ttu-id="dee36-253">2</span><span class="sxs-lookup"><span data-stu-id="dee36-253">2</span></span>      | <span data-ttu-id="dee36-254">콘솔</span><span class="sxs-lookup"><span data-stu-id="dee36-254">Console</span></span>       | <span data-ttu-id="dee36-255">Microsoft.AspNetCore.Mvc.Razor.Internal</span><span class="sxs-lookup"><span data-stu-id="dee36-255">Microsoft.AspNetCore.Mvc.Razor.Internal</span></span> | <span data-ttu-id="dee36-256">경고</span><span class="sxs-lookup"><span data-stu-id="dee36-256">Warning</span></span>           |
| <span data-ttu-id="dee36-257">3</span><span class="sxs-lookup"><span data-stu-id="dee36-257">3</span></span>      | <span data-ttu-id="dee36-258">콘솔</span><span class="sxs-lookup"><span data-stu-id="dee36-258">Console</span></span>       | <span data-ttu-id="dee36-259">Microsoft.AspNetCore.Mvc.Razor.Razor</span><span class="sxs-lookup"><span data-stu-id="dee36-259">Microsoft.AspNetCore.Mvc.Razor.Razor</span></span>    | <span data-ttu-id="dee36-260">디버그</span><span class="sxs-lookup"><span data-stu-id="dee36-260">Debug</span></span>             |
| <span data-ttu-id="dee36-261">4</span><span class="sxs-lookup"><span data-stu-id="dee36-261">4</span></span>      | <span data-ttu-id="dee36-262">콘솔</span><span class="sxs-lookup"><span data-stu-id="dee36-262">Console</span></span>       | <span data-ttu-id="dee36-263">Microsoft.AspNetCore.Mvc.Razor</span><span class="sxs-lookup"><span data-stu-id="dee36-263">Microsoft.AspNetCore.Mvc.Razor</span></span>          | <span data-ttu-id="dee36-264">Error</span><span class="sxs-lookup"><span data-stu-id="dee36-264">Error</span></span>             |
| <span data-ttu-id="dee36-265">5</span><span class="sxs-lookup"><span data-stu-id="dee36-265">5</span></span>      | <span data-ttu-id="dee36-266">콘솔</span><span class="sxs-lookup"><span data-stu-id="dee36-266">Console</span></span>       | <span data-ttu-id="dee36-267">모든 범주</span><span class="sxs-lookup"><span data-stu-id="dee36-267">All categories</span></span>                          | <span data-ttu-id="dee36-268">정보</span><span class="sxs-lookup"><span data-stu-id="dee36-268">Information</span></span>       |
| <span data-ttu-id="dee36-269">6</span><span class="sxs-lookup"><span data-stu-id="dee36-269">6</span></span>      | <span data-ttu-id="dee36-270">모든 공급자</span><span class="sxs-lookup"><span data-stu-id="dee36-270">All providers</span></span> | <span data-ttu-id="dee36-271">모든 범주</span><span class="sxs-lookup"><span data-stu-id="dee36-271">All categories</span></span>                          | <span data-ttu-id="dee36-272">디버그</span><span class="sxs-lookup"><span data-stu-id="dee36-272">Debug</span></span>             |
| <span data-ttu-id="dee36-273">7</span><span class="sxs-lookup"><span data-stu-id="dee36-273">7</span></span>      | <span data-ttu-id="dee36-274">모든 공급자</span><span class="sxs-lookup"><span data-stu-id="dee36-274">All providers</span></span> | <span data-ttu-id="dee36-275">시스템</span><span class="sxs-lookup"><span data-stu-id="dee36-275">System</span></span>                                  | <span data-ttu-id="dee36-276">디버그</span><span class="sxs-lookup"><span data-stu-id="dee36-276">Debug</span></span>             |
| <span data-ttu-id="dee36-277">8</span><span class="sxs-lookup"><span data-stu-id="dee36-277">8</span></span>      | <span data-ttu-id="dee36-278">디버그</span><span class="sxs-lookup"><span data-stu-id="dee36-278">Debug</span></span>         | <span data-ttu-id="dee36-279">Microsoft</span><span class="sxs-lookup"><span data-stu-id="dee36-279">Microsoft</span></span>                               | <span data-ttu-id="dee36-280">추적</span><span class="sxs-lookup"><span data-stu-id="dee36-280">Trace</span></span>             |

<span data-ttu-id="dee36-281">로그를 쓰는 `ILogger` 개체를 만들 때 `ILoggerFactory` 개체는 공급자마다 해당 로거에 적용할 단일 규칙을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-281">When you create an `ILogger` object to write logs with, the `ILoggerFactory` object selects a single rule per provider to apply to that logger.</span></span> <span data-ttu-id="dee36-282">`ILogger` 개체를 통해 작성된 모든 메시지는 선택한 규칙을 기반으로 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-282">All messages written by that `ILogger` object are filtered based on the selected rules.</span></span> <span data-ttu-id="dee36-283">사용 가능한 규칙 중에서 각 공급자 및 범주 쌍에 적용 가능한 가장 구체적인 규칙이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-283">The most specific rule possible for each provider and category pair is selected from the available rules.</span></span>

<span data-ttu-id="dee36-284">지정된 범주에 대한 `ILogger`가 생성되면 다음 알고리즘이 각 공급자에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-284">The following algorithm is used for each provider when an `ILogger` is created for a given category:</span></span>

* <span data-ttu-id="dee36-285">공급자 또는 공급자의 별칭과 일치하는 모든 규칙을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-285">Select all rules that match the provider or its alias.</span></span> <span data-ttu-id="dee36-286">일치 항목이 없는 경우 빈 공급자와 함께 모든 규칙을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-286">If none are found, select all rules with an empty provider.</span></span>
* <span data-ttu-id="dee36-287">앞 단계의 결과에서 일치하는 범주 접두사가 가장 긴 규칙을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-287">From the result of the preceding step, select rules with longest matching category prefix.</span></span> <span data-ttu-id="dee36-288">일치 항목이 없는 경우 범주를 지정하지 않는 규칙을 모두 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-288">If none are found, select all rules that don't specify a category.</span></span>
* <span data-ttu-id="dee36-289">여러 규칙을 선택하는 경우 **마지막** 규칙을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-289">If multiple rules are selected take the **last** one.</span></span>
* <span data-ttu-id="dee36-290">규칙을 선택하지 않는 경우 `MinimumLevel`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-290">If no rules are selected, use `MinimumLevel`.</span></span>

<span data-ttu-id="dee36-291">예를 들어 이전 단계의 규칙 목록을 갖고 있고 "Microsoft.AspNetCore.Mvc.Razor.RazorViewEngine" 범주에 대한 `ILogger` 개체를 만든다고 가정해 봅시다.</span><span class="sxs-lookup"><span data-stu-id="dee36-291">For example, suppose you have the preceding list of rules and you create an `ILogger` object for category "Microsoft.AspNetCore.Mvc.Razor.RazorViewEngine":</span></span>

* <span data-ttu-id="dee36-292">디버그 공급자에게는 규칙 1, 6, 8이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-292">For the Debug provider, rules 1, 6, and 8 apply.</span></span> <span data-ttu-id="dee36-293">규칙 8이 가장 구체적이므로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-293">Rule 8 is most specific, so that's the one selected.</span></span>
* <span data-ttu-id="dee36-294">콘솔 공급자에게는 규칙 3, 4, 5, 6이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-294">For the Console provider, rules 3, 4, 5, and 6 apply.</span></span> <span data-ttu-id="dee36-295">규칙 3이 가장 구체적입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-295">Rule 3 is most specific.</span></span>

<span data-ttu-id="dee36-296">`ILogger`를 사용하여 "Microsoft.AspNetCore.Mvc.Razor.RazorViewEngine" 범주에 대한 로그를 만들 때 수준 `Trace` 이상의 로그는 디버그 공급자로 이동하고 수준 `Debug` 이상의 로그는 콘솔 공급자로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-296">When you create logs with an `ILogger` for category "Microsoft.AspNetCore.Mvc.Razor.RazorViewEngine", logs of `Trace` level and above will go to the Debug provider, and logs of `Debug` level and above will go to the Console provider.</span></span>

<span data-ttu-id="dee36-297">**공급자 별칭**</span><span class="sxs-lookup"><span data-stu-id="dee36-297">**Provider aliases**</span></span>

<span data-ttu-id="dee36-298">형식 이름을 사용하여 구성에서 공급자를 지정할 수 있지만, 각 공급자는 길이가 짧아 사용하기 간편한 *별칭*을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-298">You can use the type name to specify a provider in configuration, but each provider defines a shorter *alias* that's easier to use.</span></span> <span data-ttu-id="dee36-299">기본 공급자의 경우 다음 별칭을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-299">For the built-in providers, use the following aliases:</span></span>

- <span data-ttu-id="dee36-300">콘솔</span><span class="sxs-lookup"><span data-stu-id="dee36-300">Console</span></span>
- <span data-ttu-id="dee36-301">디버그</span><span class="sxs-lookup"><span data-stu-id="dee36-301">Debug</span></span>
- <span data-ttu-id="dee36-302">EventLog</span><span class="sxs-lookup"><span data-stu-id="dee36-302">EventLog</span></span>
- <span data-ttu-id="dee36-303">AzureAppServices</span><span class="sxs-lookup"><span data-stu-id="dee36-303">AzureAppServices</span></span>
- <span data-ttu-id="dee36-304">TraceSource</span><span class="sxs-lookup"><span data-stu-id="dee36-304">TraceSource</span></span>
- <span data-ttu-id="dee36-305">EventSource</span><span class="sxs-lookup"><span data-stu-id="dee36-305">EventSource</span></span>

<span data-ttu-id="dee36-306">**기본 최소 수준**</span><span class="sxs-lookup"><span data-stu-id="dee36-306">**Default minimum level**</span></span>

<span data-ttu-id="dee36-307">특정 공급자 및 범주에 대한 구성 또는 코드의 규칙이 적용되지 않는 경우에만 효력이 있는 최소 수준 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-307">There's a minimum level setting that takes effect only if no rules from configuration or code apply for a given provider and category.</span></span> <span data-ttu-id="dee36-308">다음 예제는 최소 수준을 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-308">The following example shows how to set the minimum level:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_MinLevel&highlight=3)]

<span data-ttu-id="dee36-309">최소 수준을 명시적으로 설정하지 않으면 `Trace` 및 `Debug` 로그를 무시하는 `Information`이 기본값으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-309">If you don't explicitly set the minimum level, the default value is `Information`, which means that `Trace` and `Debug` logs are ignored.</span></span>

<span data-ttu-id="dee36-310">**필터 함수**</span><span class="sxs-lookup"><span data-stu-id="dee36-310">**Filter functions**</span></span>

<span data-ttu-id="dee36-311">필터 함수에서 필터링 규칙을 적용할 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-311">You can write code in a filter function to apply filtering rules.</span></span> <span data-ttu-id="dee36-312">필터 함수는 구성 또는 코드를 통해 규칙이 할당되지 않은 모든 공급자와 범주에 대해 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-312">A filter function is invoked for all providers and categories that don't have rules assigned to them by configuration or code.</span></span> <span data-ttu-id="dee36-313">함수의 코드는 공급자 형식, 범주 및 로그 수준에 액세스하여 메시지를 기록할 것인지 여부를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-313">Code in the function has access to the provider type, category, and log level to decide whether or not a message should be logged.</span></span> <span data-ttu-id="dee36-314">예:</span><span class="sxs-lookup"><span data-stu-id="dee36-314">For example:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_FilterFunction&highlight=5-13)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="dee36-315">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="dee36-315">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="dee36-316">일부 로깅 공급자는 로그 수준 및 범주에 따라 로그를 저장 매체에 기록할 것인지 아니면 무시할 것인지를 개발자가 지정할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-316">Some logging providers let you specify when logs should be written to a storage medium or ignored based on log level and category.</span></span>

<span data-ttu-id="dee36-317">`AddConsole` 및 `AddDebug` 확장 메서드는 필터링 조건을 전달할 수 있는 오버로드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-317">The `AddConsole` and `AddDebug` extension methods provide overloads that let you pass in filtering criteria.</span></span> <span data-ttu-id="dee36-318">다음 샘플 코드는 콘솔 공급자가 `Warning` 수준 미만의 로그를 무시하게 만들고, 디버그 공급자는 프레임워크에서 만드는 로그를 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-318">The following sample code causes the console provider to ignore logs below `Warning` level, while the Debug provider ignores logs that the framework creates.</span></span>

[!code-csharp[](index/sample/Startup.cs?name=snippet_AddConsoleAndDebugWithFilter&highlight=6-7)]

<span data-ttu-id="dee36-319">`AddEventLog` 메서드는 `EventLogSettings` 인스턴스를 사용하는 오버로드를 갖고 있으며, 이 인스턴스의 `Filter` 속성에는 필터링 함수가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-319">The `AddEventLog` method has an overload that takes an `EventLogSettings` instance, which may contain a filtering function in its `Filter` property.</span></span> <span data-ttu-id="dee36-320">TraceSource 공급자는 오버로드를 제공하지 않습니다. 로깅 수준 및 기타 매개 변수가 사용하는 `SourceSwitch` 및 `TraceListener`를 기반으로 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-320">The TraceSource provider doesn't provide any of those overloads, since its logging level and other parameters are based on the `SourceSwitch` and `TraceListener` it uses.</span></span>

<span data-ttu-id="dee36-321">`WithFilter` 확장 메서드를 사용하여 `ILoggerFactory` 인스턴스에 등록된 모든 공급자에 대한 필터링 규칙을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-321">You can set filtering rules for all providers that are registered with an `ILoggerFactory` instance by using the `WithFilter` extension method.</span></span> <span data-ttu-id="dee36-322">아래 예제는 프레임워크 로그(범주가 "Microsoft" 또는 "시스템"으로 시작)를 경고로 제한하고 디버그 수준에서 앱 로그를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-322">The example below limits framework logs (category begins with "Microsoft" or "System") to warnings while letting the app log at debug level.</span></span>

[!code-csharp[](index/sample/Startup.cs?name=snippet_FactoryFilter&highlight=6-11)]

<span data-ttu-id="dee36-323">필터링을 사용하여 특정 범주에 대한 로그를 기록하지 못하게 하려면 해당 범주의 최소 로그 수준으로 `LogLevel.None`을 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-323">If you want to use filtering to prevent all logs from being written for a particular category, you can specify `LogLevel.None` as the minimum log level for that category.</span></span> <span data-ttu-id="dee36-324">`LogLevel.None`의 정수 값은 `LogLevel.Critical`(5)보다 높은 6입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-324">The integer value of `LogLevel.None` is 6, which is higher than `LogLevel.Critical` (5).</span></span>

<span data-ttu-id="dee36-325">`WithFilter` 확장 메서드는 [Microsoft.Extensions.Logging.Filter](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Filter) NuGet 패키지에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-325">The `WithFilter` extension method is provided by the [Microsoft.Extensions.Logging.Filter](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Filter) NuGet package.</span></span> <span data-ttu-id="dee36-326">이 메서드는 등록된 모든 로거 공급자로 전달되는 메시지를 필터링하는 새로운 `ILoggerFactory` 인스턴스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-326">The method returns a new `ILoggerFactory` instance that will filter the log messages passed to all logger providers registered with it.</span></span> <span data-ttu-id="dee36-327">원래 `ILoggerFactory` 인스턴스를 포함하여 어떤 `ILoggerFactory` 인스턴스에도 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-327">It doesn't affect any other `ILoggerFactory` instances, including the original `ILoggerFactory` instance.</span></span>

---

## <a name="log-scopes"></a><span data-ttu-id="dee36-328">로그 점수</span><span class="sxs-lookup"><span data-stu-id="dee36-328">Log scopes</span></span>

<span data-ttu-id="dee36-329">*범위* 내의 논리적 작업 집합을 그룹화하여 동일한 데이터를 해당 집합의 일부로 생성된 각 로그에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-329">You can group a set of logical operations within a *scope* in order to attach the same data to each log that's created as part of that set.</span></span> <span data-ttu-id="dee36-330">예를 들어 트랜잭션 처리의 일부로 생성되는 모든 로그가 트랜잭션 ID를 포함하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-330">For example, you might want every log created as part of processing a transaction to include the transaction ID.</span></span>

<span data-ttu-id="dee36-331">범위는 `ILogger.BeginScope<TState>` 메서드에서 반환하는 `IDisposable` 형식이며 삭제될 때까지 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-331">A scope is an `IDisposable` type that's returned by the `ILogger.BeginScope<TState>` method and lasts until it's disposed.</span></span> <span data-ttu-id="dee36-332">다음과 같이 로거 호출을 `using` 블록에 래핑하여 범위를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-332">You use a scope by wrapping your logger calls in a `using` block, as shown here:</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_Scopes&highlight=4-5,13)]

<span data-ttu-id="dee36-333">다음은 콘솔 공급자에 대한 범위를 사용하도록 설정하는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-333">The following code enables scopes for the console provider:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="dee36-334">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="dee36-334">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="dee36-335">*Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="dee36-335">In *Program.cs*:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_Scopes&highlight=4)]

> [!NOTE]
> <span data-ttu-id="dee36-336">범위 기반 로깅을 사용하려면 `IncludeScopes` 콘솔 로거 옵션을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-336">Configuring the `IncludeScopes` console logger option is required to enable scope-based logging.</span></span> <span data-ttu-id="dee36-337">*appsettings* 구성 파일을 사용하여 `IncludeScopes`를 구성하는 기능은 ASP.NET Core 2.1 릴리스에서 제공될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-337">Configuration of `IncludeScopes` using *appsettings* configuration files will be available with the release of ASP.NET Core 2.1.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="dee36-338">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="dee36-338">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="dee36-339">*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="dee36-339">In *Startup.cs*:</span></span>

[!code-csharp[](index/sample/Startup.cs?name=snippet_Scopes&highlight=6)]

---

<span data-ttu-id="dee36-340">각 로그 메시지는 범위 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-340">Each log message includes the scoped information:</span></span>

```
info: TodoApi.Controllers.TodoController[1002]
      => RequestId:0HKV9C49II9CK RequestPath:/api/todo/0 => TodoApi.Controllers.TodoController.GetById (TodoApi) => Message attached to logs created in the using block
      Getting item 0
warn: TodoApi.Controllers.TodoController[4000]
      => RequestId:0HKV9C49II9CK RequestPath:/api/todo/0 => TodoApi.Controllers.TodoController.GetById (TodoApi) => Message attached to logs created in the using block
      GetById(0) NOT FOUND
```

## <a name="built-in-logging-providers"></a><span data-ttu-id="dee36-341">기본 로깅 공급자</span><span class="sxs-lookup"><span data-stu-id="dee36-341">Built-in logging providers</span></span>

<span data-ttu-id="dee36-342">ASP.NET Core는 다음 공급자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-342">ASP.NET Core ships the following providers:</span></span>

* [<span data-ttu-id="dee36-343">콘솔</span><span class="sxs-lookup"><span data-stu-id="dee36-343">Console</span></span>](#console)
* [<span data-ttu-id="dee36-344">디버그</span><span class="sxs-lookup"><span data-stu-id="dee36-344">Debug</span></span>](#debug)
* [<span data-ttu-id="dee36-345">EventSource</span><span class="sxs-lookup"><span data-stu-id="dee36-345">EventSource</span></span>](#eventsource)
* [<span data-ttu-id="dee36-346">EventLog</span><span class="sxs-lookup"><span data-stu-id="dee36-346">EventLog</span></span>](#eventlog)
* [<span data-ttu-id="dee36-347">TraceSource</span><span class="sxs-lookup"><span data-stu-id="dee36-347">TraceSource</span></span>](#tracesource)
* [<span data-ttu-id="dee36-348">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="dee36-348">Azure App Service</span></span>](#appservice)

<a id="console"></a>
### <a name="the-console-provider"></a><span data-ttu-id="dee36-349">콘솔 공급자</span><span class="sxs-lookup"><span data-stu-id="dee36-349">The console provider</span></span>

<span data-ttu-id="dee36-350">[Microsoft.Extensions.Logging.Console](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Console) 공급자 패키지는 콘솔에 로그 출력을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-350">The [Microsoft.Extensions.Logging.Console](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Console) provider package sends log output to the console.</span></span> 

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="dee36-351">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="dee36-351">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

```csharp
logging.AddConsole()
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="dee36-352">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="dee36-352">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

```csharp
loggerFactory.AddConsole()
```

<span data-ttu-id="dee36-353">[AddConsole 오버로드](/dotnet/api/microsoft.extensions.logging.consoleloggerextensions)를 사용하여 최소 로그 수준, 필터 함수 및 범위 지원 여부를 나타내는 부울을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-353">[AddConsole overloads](/dotnet/api/microsoft.extensions.logging.consoleloggerextensions) let you pass in an a minimum log level, a filter function, and a boolean that indicates whether scopes are supported.</span></span> <span data-ttu-id="dee36-354">다른 옵션으로는 `IConfiguration` 개체를 전달할 수 있으며, 이 개체는 범위 지원 및 로깅 수준을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-354">Another option is to pass in an `IConfiguration` object, which can specify scopes support and logging levels.</span></span> 

<span data-ttu-id="dee36-355">프로덕션 환경에서 콘솔 공급자를 사용하려고 생각 중인 경우 성능에 상당한 영향이 있다는 점에 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-355">If you are considering the console provider for use in production, be aware that it has a significant impact on performance.</span></span>

<span data-ttu-id="dee36-356">Visual Studio에서 새 프로젝트를 만들면 `AddConsole` 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-356">When you create a new project in Visual Studio, the `AddConsole` method looks like this:</span></span>

```csharp
loggerFactory.AddConsole(Configuration.GetSection("Logging"));
```

<span data-ttu-id="dee36-357">이 코드는 *appSettings.json* 파일의 `Logging` 섹션을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-357">This code refers to the `Logging` section of the *appSettings.json* file:</span></span>

[!code-json[](index/sample//appsettings.json)]

<span data-ttu-id="dee36-358">[로그 필터링](#log-filtering) 섹션에서 설명했듯이, 제한 프레임워크를 표시한 설정은 경고에 기록되는 한편 앱이 디버그 수준에서 기록하는 것을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-358">The settings shown limit framework logs to warnings while allowing the app to log at debug level, as explained in the [Log filtering](#log-filtering) section.</span></span> <span data-ttu-id="dee36-359">자세한 내용은 [구성](xref:fundamentals/configuration/index)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-359">For more information, see [Configuration](xref:fundamentals/configuration/index).</span></span>

---

<a id="debug"></a>
### <a name="the-debug-provider"></a><span data-ttu-id="dee36-360">디버그 공급자</span><span class="sxs-lookup"><span data-stu-id="dee36-360">The Debug provider</span></span>

<span data-ttu-id="dee36-361">[Microsoft.Extensions.Logging.Debug](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Debug) 공급자 패키지는 [System.Diagnostics.Debug](/dotnet/api/system.diagnostics.debug) 클래스(`Debug.WriteLine` 메서드 호출)를 사용하여 로그 출력을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-361">The [Microsoft.Extensions.Logging.Debug](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Debug) provider package writes log output by using the [System.Diagnostics.Debug](/dotnet/api/system.diagnostics.debug) class (`Debug.WriteLine` method calls).</span></span>

<span data-ttu-id="dee36-362">Linux에서 이 공급자는 */var/log/message*에 로그를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-362">On Linux, this provider writes logs to */var/log/message*.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="dee36-363">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="dee36-363">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
logging.AddDebug()
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="dee36-364">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="dee36-364">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
loggerFactory.AddDebug()
```

<span data-ttu-id="dee36-365">[AddDebug 오버로드](/dotnet/api/microsoft.extensions.logging.debugloggerfactoryextensions)를 사용하여 최소 수준 로그 또는 필터 함수를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-365">[AddDebug overloads](/dotnet/api/microsoft.extensions.logging.debugloggerfactoryextensions) let you pass in a minimum log level or a filter function.</span></span>

---

<a id="eventsource"></a>
### <a name="the-eventsource-provider"></a><span data-ttu-id="dee36-366">EventSource 공급자</span><span class="sxs-lookup"><span data-stu-id="dee36-366">The EventSource provider</span></span>

<span data-ttu-id="dee36-367">ASP.NET Core 1.1.0을 대상으로 하는 앱의 경우 [Microsoft.Extensions.Logging.EventSource](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventSource) 공급자 패키지가 이벤트 추적을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-367">For apps that target ASP.NET Core 1.1.0 or higher, the [Microsoft.Extensions.Logging.EventSource](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventSource) provider package can implement event tracing.</span></span> <span data-ttu-id="dee36-368">Windows에서는 [ETW](https://msdn.microsoft.com/library/windows/desktop/bb968803)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-368">On Windows, it uses [ETW](https://msdn.microsoft.com/library/windows/desktop/bb968803).</span></span> <span data-ttu-id="dee36-369">플랫폼 간 공급자이지만 이벤트를 수집하지 않으며 Linux 또는 macOS용 도구를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-369">The provider is cross-platform, but there are no event collection and display tools yet for Linux or macOS.</span></span> 

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="dee36-370">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="dee36-370">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
logging.AddEventSourceLogger()
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="dee36-371">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="dee36-371">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
loggerFactory.AddEventSourceLogger()
```

---

<span data-ttu-id="dee36-372">로그를 수집하고 보는 좋은 방법은 [PerfView 유틸리티](https://www.microsoft.com/download/details.aspx?id=28567)를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-372">A good way to collect and view logs is to use the [PerfView utility](https://www.microsoft.com/download/details.aspx?id=28567).</span></span> <span data-ttu-id="dee36-373">ETW 로그를 보는 다른 도구가 있지만, PerfView는 ASP.NET에서 내보내는 ETW 이벤트를 처리하기에 가장 좋은 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-373">There are other tools for viewing ETW logs, but PerfView provides the best experience for working with the ETW events emitted by ASP.NET.</span></span> 

<span data-ttu-id="dee36-374">이 공급자가 기록한 이벤트를 수집하도록 PerfView를 구성하려면 **추가 공급자** 목록에 `*Microsoft-Extensions-Logging` 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-374">To configure PerfView for collecting events logged by this provider, add the string `*Microsoft-Extensions-Logging` to the **Additional Providers** list.</span></span> <span data-ttu-id="dee36-375">(문자열의 시작 부분에 별표를 누락하지 마세요.)</span><span class="sxs-lookup"><span data-stu-id="dee36-375">(Don't miss the asterisk at the start of the string.)</span></span>

![Perfview 추가 공급자](index/_static/perfview-additional-providers.png)

<a id="eventlog"></a>
### <a name="the-windows-eventlog-provider"></a><span data-ttu-id="dee36-377">Windows EventLog 공급자</span><span class="sxs-lookup"><span data-stu-id="dee36-377">The Windows EventLog provider</span></span>

<span data-ttu-id="dee36-378">[Microsoft.Extensions.Logging.EventLog](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventLog) 공급자 패키지는 Windows 이벤트 로그에 로그 출력을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-378">The [Microsoft.Extensions.Logging.EventLog](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventLog) provider package sends log output to the Windows Event Log.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="dee36-379">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="dee36-379">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
logging.AddEventLog()
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="dee36-380">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="dee36-380">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
loggerFactory.AddEventLog()
```

<span data-ttu-id="dee36-381">[AddEventLog 오버로드](/dotnet/api/microsoft.extensions.logging.eventloggerfactoryextensions)를 사용하여 `EventLogSettings` 또는 최소 로그 수준을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-381">[AddEventLog overloads](/dotnet/api/microsoft.extensions.logging.eventloggerfactoryextensions) let you pass in `EventLogSettings` or a minimum log level.</span></span>

---

<a id="tracesource"></a>
### <a name="the-tracesource-provider"></a><span data-ttu-id="dee36-382">TraceSource 공급자</span><span class="sxs-lookup"><span data-stu-id="dee36-382">The TraceSource provider</span></span>

<span data-ttu-id="dee36-383">[Microsoft.Extensions.Logging.TraceSource](https://www.nuget.org/packages/Microsoft.Extensions.Logging.TraceSource) 공급자 패키지는 [System.Diagnostics.TraceSource](/dotnet/api/system.diagnostics.tracesource) 라이브러리 및 공급자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-383">The [Microsoft.Extensions.Logging.TraceSource](https://www.nuget.org/packages/Microsoft.Extensions.Logging.TraceSource) provider package uses the [System.Diagnostics.TraceSource](/dotnet/api/system.diagnostics.tracesource) libraries and providers.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="dee36-384">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="dee36-384">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
logging.AddTraceSource(sourceSwitchName);
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="dee36-385">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="dee36-385">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
loggerFactory.AddTraceSource(sourceSwitchName);
```

---

<span data-ttu-id="dee36-386">[AddTraceSource 오버로드](/dotnet/api/microsoft.extensions.logging.tracesourcefactoryextensions)를 사용하여 원본 스위치 및 추적 수신기를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-386">[AddTraceSource overloads](/dotnet/api/microsoft.extensions.logging.tracesourcefactoryextensions) let you pass in a source switch and a trace listener.</span></span>

<span data-ttu-id="dee36-387">이 공급자를 사용하려면 응용 프로그램이 .NET Framework(.NET Core가 아닌)에서 실행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-387">To use this provider, an application has to run on the .NET Framework (rather than .NET Core).</span></span> <span data-ttu-id="dee36-388">공급자를 통해 응용 프로그램 예제에 사용된 [TextWriterTraceListener](/dotnet/api/system.diagnostics.textwritertracelistenerr)처럼 다양한 [수신기](/dotnet/framework/debug-trace-profile/trace-listeners)로 메시지를 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-388">The provider lets you route messages to a variety of [listeners](/dotnet/framework/debug-trace-profile/trace-listeners), such as the [TextWriterTraceListener](/dotnet/api/system.diagnostics.textwritertracelistenerr) used in the sample application.</span></span>

<span data-ttu-id="dee36-389">다음은 `Warning` 이상 메시지를 콘솔 창에 기록하는 `TraceSource` 공급자를 구성하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-389">The following example configures a `TraceSource` provider that logs `Warning` and higher messages to the console window.</span></span>

[!code-csharp[](index/sample/Startup.cs?name=snippet_TraceSource&highlight=9-12)]

<a id="appservice"></a>
### <a name="the-azure-app-service-provider"></a><span data-ttu-id="dee36-390">Azure App Service 공급자</span><span class="sxs-lookup"><span data-stu-id="dee36-390">The Azure App Service provider</span></span>

<span data-ttu-id="dee36-391">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices) 공급자 패키지는 Azure App Service 앱의 파일 시스템과 Azure Storage 계정의 [BLOB 저장소](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/#what-is-blob-storage)에 텍스트 파일을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-391">The [Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices) provider package writes logs to text files in an Azure App Service app's file system and to [blob storage](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/#what-is-blob-storage) in an Azure Storage account.</span></span> <span data-ttu-id="dee36-392">공급자는 ASP.NET Core 1.1.0을 대상으로 하는 앱에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-392">The provider is available only for apps that target ASP.NET Core 1.1.0 or higher.</span></span> 

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="dee36-393">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="dee36-393">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="dee36-394">.NET Core를 대상으로 지정하는 경우 공급자 패키지를 설치하거나 명시적으로 `AddAzureWebAppDiagnostics`을 호출하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-394">If targeting .NET Core, you don't have to install the provider package or explicitly call `AddAzureWebAppDiagnostics`.</span></span> <span data-ttu-id="dee36-395">Azure App Service에 앱을 배포하면 자동으로 앱에 공급자가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-395">The provider is automatically available to your app when you deploy the app to Azure App Service.</span></span>

<span data-ttu-id="dee36-396">.NET Framework를 대상으로 지정하는 경우 패키지 공급자를 프로젝트에 추가하고 `AddAzureWebAppDiagnostics`을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-396">If targeting .NET Framework, add the provider package to your project and invoke `AddAzureWebAppDiagnostics`:</span></span>

```csharp
logging.AddAzureWebAppDiagnostics();
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="dee36-397">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="dee36-397">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
loggerFactory.AddAzureWebAppDiagnostics();
```

<span data-ttu-id="dee36-398">`AddAzureWebAppDiagnostics` 오버로드를 사용하여 로깅 출력 템플릿, BLOB 이름, 파일 크기 제한 등의 기본 설정을 재정의하는 데 사용할 수 있는 [AzureAppServicesDiagnosticsSettings](https://github.com/aspnet/Logging/blob/c7d0b1b88668ff4ef8a86ea7d2ebb5ca7f88d3e0/src/Microsoft.Extensions.Logging.AzureAppServices/AzureAppServicesDiagnosticsSettings.cs)를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-398">An `AddAzureWebAppDiagnostics` overload lets you pass in [AzureAppServicesDiagnosticsSettings](https://github.com/aspnet/Logging/blob/c7d0b1b88668ff4ef8a86ea7d2ebb5ca7f88d3e0/src/Microsoft.Extensions.Logging.AzureAppServices/AzureAppServicesDiagnosticsSettings.cs) with which you can override default settings such as the logging output template, blob name, and file size limit.</span></span> <span data-ttu-id="dee36-399">(*출력 템플릿*은 `ILogger` 메서드를 호출할 때 제공하는 로그를 기반으로 모든 로그에 적용되는 메시지 템플릿입니다.)</span><span class="sxs-lookup"><span data-stu-id="dee36-399">(*Output template* is a message template that's applied to all logs on top of the one that you provide when you call an `ILogger` method.)</span></span>

---

<span data-ttu-id="dee36-400">App Service 앱에 배포할 때 응용 프로그램은 Azure Portal **App Service** 페이지의 [진단 로그](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/#enablediag) 섹션에 있는 설정을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-400">When you deploy to an App Service app, your application honors the settings in the [Diagnostic Logs](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/#enablediag) section of the **App Service** page of the Azure portal.</span></span> <span data-ttu-id="dee36-401">이러한 설정을 변경하면 앱을 다시 시작하거나 코드를 다시 배포할 필요 없이 변경 내용이 즉시 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-401">When you change those settings, the changes take effect immediately without requiring that you restart the app or redeploy code to it.</span></span> 

![Azure 로깅 설정](index/_static/azure-logging-settings.png)

<span data-ttu-id="dee36-403">로그 파일의 기본 위치는 *D:\\home\\LogFiles\\Application* 폴더이며, 기본 파일 이름은 *diagnostics-yyyymmdd.txt*입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-403">The default location for log files is in the *D:\\home\\LogFiles\\Application* folder, and the default file name is *diagnostics-yyyymmdd.txt*.</span></span> <span data-ttu-id="dee36-404">기본 파일 크기 제한은 10MB이고, 보존되는 기본 최대 파일 수는 2입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-404">The default file size limit is 10 MB, and the default maximum number of files retained is 2.</span></span> <span data-ttu-id="dee36-405">기본 BLOB 이름은 *{app-name}{timestamp}/yyyy/mm/dd/hh/{guid}-applicationLog.txt*입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-405">The default blob name is *{app-name}{timestamp}/yyyy/mm/dd/hh/{guid}-applicationLog.txt*.</span></span> <span data-ttu-id="dee36-406">기본 동작에 대한 자세한 내용은 [AzureAppServicesDiagnosticsSettings](https://github.com/aspnet/Logging/blob/c7d0b1b88668ff4ef8a86ea7d2ebb5ca7f88d3e0/src/Microsoft.Extensions.Logging.AzureAppServices/AzureAppServicesDiagnosticsSettings.cs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dee36-406">For more information about default behavior, see [AzureAppServicesDiagnosticsSettings](https://github.com/aspnet/Logging/blob/c7d0b1b88668ff4ef8a86ea7d2ebb5ca7f88d3e0/src/Microsoft.Extensions.Logging.AzureAppServices/AzureAppServicesDiagnosticsSettings.cs).</span></span>

<span data-ttu-id="dee36-407">공급자는 프로젝트가 Azure 환경에서 실행되는 경우에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-407">The provider only works when your project runs in the Azure environment.</span></span> <span data-ttu-id="dee36-408">로컬로 실행하는 경우에는 아무 영향도 없습니다. Blob에 대한 로컬 파일 또는 로컬 개발 저장소에 기록하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-408">It has no effect when you run locally &mdash; it doesn't write to local files or local development storage for blobs.</span></span>

## <a name="third-party-logging-providers"></a><span data-ttu-id="dee36-409">타사 로깅 공급자</span><span class="sxs-lookup"><span data-stu-id="dee36-409">Third-party logging providers</span></span>

<span data-ttu-id="dee36-410">다음은 ASP.NET Core와 호환되는 일부 타사 로깅 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-410">Here are some third-party logging frameworks that work with ASP.NET Core:</span></span>

* <span data-ttu-id="dee36-411">[elmah.io](https://github.com/elmahio/Elmah.Io.Extensions.Logging) - Elmah.Io 서비스의 공급자</span><span class="sxs-lookup"><span data-stu-id="dee36-411">[elmah.io](https://github.com/elmahio/Elmah.Io.Extensions.Logging) - provider for the Elmah.Io service</span></span>

* <span data-ttu-id="dee36-412">[JSNLog](http://jsnlog.com) - 서버 쪽 로그에 JavaScript 예외 및 기타 클라이언트 쪽 이벤트를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-412">[JSNLog](http://jsnlog.com) - logs JavaScript exceptions and other client-side events in your server-side log.</span></span>

* <span data-ttu-id="dee36-413">[Loggr](https://github.com/imobile3/Loggr.Extensions.Logging) - Loggr 서비스의 공급자</span><span class="sxs-lookup"><span data-stu-id="dee36-413">[Loggr](https://github.com/imobile3/Loggr.Extensions.Logging) - provider for the Loggr service</span></span>

* <span data-ttu-id="dee36-414">[NLog](https://github.com/NLog/NLog.Extensions.Logging) - NLog 라이브러리의 공급자</span><span class="sxs-lookup"><span data-stu-id="dee36-414">[NLog](https://github.com/NLog/NLog.Extensions.Logging) - provider for the NLog library</span></span>

* <span data-ttu-id="dee36-415">[Serilog](https://github.com/serilog/serilog-extensions-logging) - Serilog 라이브러리의 공급자</span><span class="sxs-lookup"><span data-stu-id="dee36-415">[Serilog](https://github.com/serilog/serilog-extensions-logging) - provider for the Serilog library</span></span>

<span data-ttu-id="dee36-416">일부 타사 프레임워크는 [구조적 로깅이라고도 하는 의미 체계 로깅](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging)을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-416">Some third-party frameworks can do [semantic logging, also known as structured logging](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging).</span></span>

<span data-ttu-id="dee36-417">타사 프레임워크를 사용하는 방법은 기본 공급자 중 하나를 사용하는 방법과 비슷합니다. 프로젝트에 NuGet 패키지를 추가하고 `ILoggerFactory`에 대한 확장 메서드를 호출하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-417">Using a third-party framework is similar to using one of the built-in providers: add a NuGet package to your project and call an extension method on `ILoggerFactory`.</span></span> <span data-ttu-id="dee36-418">자세한 내용은 각 프레임워크의 설명서를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="dee36-418">For more information, see each framework's documentation.</span></span>

## <a name="azure-log-streaming"></a><span data-ttu-id="dee36-419">Azure 로그 스트리밍</span><span class="sxs-lookup"><span data-stu-id="dee36-419">Azure log streaming</span></span>

<span data-ttu-id="dee36-420">Azure 로그 스트리밍을 통해 로그 작업을 실시간으로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-420">Azure log streaming enables you to view log activity in real time from:</span></span> 

* <span data-ttu-id="dee36-421">응용 프로그램 서버</span><span class="sxs-lookup"><span data-stu-id="dee36-421">The application server</span></span> 
* <span data-ttu-id="dee36-422">웹 서버</span><span class="sxs-lookup"><span data-stu-id="dee36-422">The web server</span></span>
* <span data-ttu-id="dee36-423">실패한 요청 추적</span><span class="sxs-lookup"><span data-stu-id="dee36-423">Failed request tracing</span></span> 

<span data-ttu-id="dee36-424">Azure 로그 스트리밍을 구성하려면:</span><span class="sxs-lookup"><span data-stu-id="dee36-424">To configure Azure log streaming:</span></span> 

* <span data-ttu-id="dee36-425">응용 프로그램의 포털 페이지에서 **진단 로그** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-425">Navigate to the **Diagnostics Logs** page from your application's portal page</span></span>
* <span data-ttu-id="dee36-426">**응용 프로그램 로깅(파일 시스템)** 을 켭니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-426">Set **Application Logging (Filesystem)** to on.</span></span> 

![Azure Portal 진단 로그 페이지](index/_static/azure-diagnostic-logs.png)

<span data-ttu-id="dee36-428">**로그 스트리밍** 페이지로 이동하여 응용 프로그램 메시지를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-428">Navigate to the **Log Streaming** page to view application messages.</span></span> <span data-ttu-id="dee36-429">응용 프로그램이 `ILogger` 인터페이스를 통해 기록한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dee36-429">They're logged by application through the `ILogger` interface.</span></span> 

![Azure Portal 응용 프로그램 로그 스트리밍](index/_static/azure-log-streaming.png)


## <a name="see-also"></a><span data-ttu-id="dee36-431">참고 항목</span><span class="sxs-lookup"><span data-stu-id="dee36-431">See also</span></span>

[<span data-ttu-id="dee36-432">LoggerMessage를 사용한 고성능 로깅</span><span class="sxs-lookup"><span data-stu-id="dee36-432">High-performance logging with LoggerMessage</span></span>](xref:fundamentals/logging/loggermessage)
