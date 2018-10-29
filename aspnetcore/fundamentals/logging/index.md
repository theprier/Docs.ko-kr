---
title: ASP.NET Core에 로그인
author: tdykstra
description: ASP.NET Core의 로깅 프레임워크에 대해 알아봅니다. 기본 제공 로깅 공급자를 살펴보고 인기 있는 타사 공급자에 대해 알아봅니다.
ms.author: tdykstra
ms.custom: mvc
ms.date: 10/11/2018
uid: fundamentals/logging/index
ms.openlocfilehash: f7cfb3823a188f28398d59e0d009e9ddc159dc32
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50207578"
---
# <a name="logging-in-aspnet-core"></a><span data-ttu-id="84ec3-104">ASP.NET Core에 로그인</span><span class="sxs-lookup"><span data-stu-id="84ec3-104">Logging in ASP.NET Core</span></span>

<span data-ttu-id="84ec3-105">작성자: [Steve Smith](https://ardalis.com/) 및 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="84ec3-105">By [Steve Smith](https://ardalis.com/) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="84ec3-106">ASP.NET Core는 다양한 기본 제공 및 타사 로깅 공급자와 함께 작동하는 로깅 API를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-106">ASP.NET Core supports a logging API that works with a variety of built-in and third-party logging providers.</span></span> <span data-ttu-id="84ec3-107">이 문서에서는 기본 제공 공급자에서 로깅 API를 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-107">This article shows how to use the logging API with built-in providers.</span></span>

<span data-ttu-id="84ec3-108">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/index/samples)([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="84ec3-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/index/samples) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="add-providers"></a><span data-ttu-id="84ec3-109">공급자 추가</span><span class="sxs-lookup"><span data-stu-id="84ec3-109">Add providers</span></span>

<span data-ttu-id="84ec3-110">로깅 공급자는 로그를 표시하거나 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-110">A logging provider displays or stores logs.</span></span> <span data-ttu-id="84ec3-111">예를 들어 콘솔 공급자는 콘솔에 로그를 표시하고 Azure Application Insights 공급자는 이를 Azure Application Insights에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-111">For example, the Console provider displays logs on the console, and the Azure Application Insights provider stores them in Azure Application Insights.</span></span> <span data-ttu-id="84ec3-112">여러 공급자를 추가하여 로그를 여러 대상으로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-112">Logs can be sent to multiple destinations by adding multiple providers.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="84ec3-113">공급자를 추가하려면 *Program.cs*에서 공급자의 `Add{provider name}` 확장 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-113">To add a provider, call the provider's `Add{provider name}` extension method in *Program.cs*:</span></span>

[!code-csharp[](index/samples/2.x/TodoApiSample/Program.cs?name=snippet_ExpandDefault&highlight=17-19)]

<span data-ttu-id="84ec3-114">기본 프로젝트 템플릿은 <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder%2A> 확장 메서드를 호출하여 다음 로깅 공급자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-114">The default project template calls the <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder%2A> extension method, which adds the following logging providers:</span></span>

* <span data-ttu-id="84ec3-115">콘솔</span><span class="sxs-lookup"><span data-stu-id="84ec3-115">Console</span></span>
* <span data-ttu-id="84ec3-116">디버그</span><span class="sxs-lookup"><span data-stu-id="84ec3-116">Debug</span></span>
* <span data-ttu-id="84ec3-117">EventSource(ASP.NET Core 2.2에서 시작)</span><span class="sxs-lookup"><span data-stu-id="84ec3-117">EventSource (starting in ASP.NET Core 2.2)</span></span>

[!code-csharp[](index/samples/2.x/TodoApiSample/Program.cs?name=snippet_TemplateCode&highlight=7)]

<span data-ttu-id="84ec3-118">`CreateDefaultBuilder`를 사용하는 경우 기본 제공자를 사용자가 선택한 대로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-118">If you use `CreateDefaultBuilder`, you can replace the default providers with your own choices.</span></span> <span data-ttu-id="84ec3-119"><xref:Microsoft.Extensions.Logging.LoggingBuilderExtensions.ClearProviders%2A>를 호출하여 원하는 공급자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-119">Call <xref:Microsoft.Extensions.Logging.LoggingBuilderExtensions.ClearProviders%2A>, and add the providers you want.</span></span>

[!code-csharp[](index/samples/2.x/TodoApiSample/Program.cs?name=snippet_LogFromMain&highlight=18-22)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="84ec3-120">공급자를 사용하려면 해당 NuGet 패키지를 설치하고 <xref:Microsoft.Extensions.Logging.ILoggerFactory> 인스턴스에서 공급자의 확장 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-120">To use a provider, install its NuGet package and call the provider's extension method on an instance of <xref:Microsoft.Extensions.Logging.ILoggerFactory>:</span></span>

[!code-csharp[](index/samples/1.x/TodoApiSample//Startup.cs?name=snippet_AddConsoleAndDebug&highlight=3,5-7)]

<span data-ttu-id="84ec3-121">ASP.NET Core [DI(종속성 주입](xref:fundamentals/dependency-injection))는 `ILoggerFactory` 인스턴스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-121">ASP.NET Core [dependency injection (DI)](xref:fundamentals/dependency-injection) provides the `ILoggerFactory` instance.</span></span> <span data-ttu-id="84ec3-122">`AddConsole` 및 `AddDebug` 확장 메서드는 [Microsoft.Extensions.Logging.Console](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Console/) 및 [Microsoft.Extensions.Logging.Debug](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Debug/) 패키지에 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-122">The `AddConsole` and `AddDebug` extension methods are defined in the [Microsoft.Extensions.Logging.Console](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Console/) and [Microsoft.Extensions.Logging.Debug](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Debug/) packages.</span></span> <span data-ttu-id="84ec3-123">각 확장 메서드는 `ILoggerFactory.AddProvider` 메서드를 호출하고, 공급자 인스턴스를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-123">Each extension method calls the `ILoggerFactory.AddProvider` method, passing in an instance of the provider.</span></span>

> [!NOTE]
> <span data-ttu-id="84ec3-124">[샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/index/samples/1.x)은 `Startup.Configure` 메서드에서 로그 공급자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-124">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/index/samples/1.x) adds logging providers in the `Startup.Configure` method.</span></span> <span data-ttu-id="84ec3-125">먼저 실행되는 코드의 로그 출력을 가져오려면 `Startup` 클래스 생성자에 로그 공급자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-125">To obtain log output from code that executes earlier, add logging providers in the `Startup` class constructor.</span></span>

::: moniker-end

<span data-ttu-id="84ec3-126">문서의 뒷부분에 나오는 [기본 제공 로깅 공급자](#built-in-logging-providers) 및 [타사 로깅 공급자](#third-party-logging-providers)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-126">Learn more about [built-in logging providers](#built-in-logging-providers) and [third-party logging providers](#third-party-logging-providers) later in the article.</span></span>

## <a name="create-logs"></a><span data-ttu-id="84ec3-127">로그 만들기</span><span class="sxs-lookup"><span data-stu-id="84ec3-127">Create logs</span></span>

<span data-ttu-id="84ec3-128">DI에서 <xref:Microsoft.Extensions.Logging.ILogger`1> 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-128">Get an <xref:Microsoft.Extensions.Logging.ILogger`1> object from DI.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="84ec3-129">다음 컨트롤러 예제에서는 `Information` 및 `Warning` 로그를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-129">The following controller example creates `Information` and `Warning` logs.</span></span> <span data-ttu-id="84ec3-130">*범주*는 `TodoApiSample.Controllers.TodoController`(샘플 앱에서 `TodoController`의 정규화된 클래스 이름 샘플)입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-130">The *category* is `TodoApiSample.Controllers.TodoController` (the fully qualified class name of `TodoController` in the sample app):</span></span>

[!code-csharp[](index/samples/2.x/TodoApiSample/Controllers/TodoController.cs?name=snippet_LoggerDI&highlight=4,7)]

[!code-csharp[](index/samples/2.x/TodoApiSample/Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

<span data-ttu-id="84ec3-131">다음 Razor Pages 예제에서는 `Information`을 *수준*으로, `TodoApiSample.Pages.AboutModel`을 *범주*로 사용하는 로그를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-131">The following Razor Pages example creates logs with `Information` as the *level* and `TodoApiSample.Pages.AboutModel` as the *category*:</span></span>

[!code-csharp[](index/samples/2.x/TodoApiSample/Pages/About.cshtml.cs?name=snippet_LoggerDI&highlight=3, 7)]

[!code-csharp[](index/samples/2.x/TodoApiSample/Pages/About.cshtml.cs?name=snippet_CallLogMethods&highlight=4)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/TodoApiSample/Controllers/TodoController.cs?name=snippet_LoggerDI&highlight=7)]

[!code-csharp[](index/samples/1.x/TodoApiSample/Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

<span data-ttu-id="84ec3-132">앞의 예제에서는 `Information` 및 `Warning`을 *수준*으로, `TodoController` 클래스를 *범주*로 사용하는 로그를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-132">The preceding example creates logs with `Information` and `Warning` as the *level* and `TodoController` class as the *category*.</span></span> 

::: moniker-end

<span data-ttu-id="84ec3-133">로그 *수준*은 기록된 이벤트의 심각도를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-133">The Log *level* indicates the severity of the logged event.</span></span> <span data-ttu-id="84ec3-134">로그 *범주*는 각 로그와 연결된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-134">The log *category* is a string that is associated with each log.</span></span> <span data-ttu-id="84ec3-135">`ILogger<T>` 인스턴스는 `T` 형식의 정규화된 이름을 가진 로그를 범주로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-135">The `ILogger<T>` instance creates logs that have the fully qualified name of type `T` as the category.</span></span> <span data-ttu-id="84ec3-136">[수준](#log-level) 및 [범주](#log-category)는 이 문서의 뒷부분에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-136">[Levels](#log-level) and [categories](#log-category) are explained in more detail later in this article.</span></span> 

::: moniker range=">= aspnetcore-2.0"

### <a name="create-logs-in-startup"></a><span data-ttu-id="84ec3-137">시작 시 로그 만들기</span><span class="sxs-lookup"><span data-stu-id="84ec3-137">Create logs in Startup</span></span>

<span data-ttu-id="84ec3-138">`Startup` 클래스에 로그를 작성하려면 생성자 시그니처에 `ILogger` 매개 변수를 포함시킵니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-138">To write logs in the `Startup` class, include an `ILogger` parameter in the constructor signature:</span></span>

[!code-csharp[](index/samples/2.x/TodoApiSample/Startup.cs?name=snippet_Startup&highlight=3,5,8,19,26)]

### <a name="create-logs-in-program"></a><span data-ttu-id="84ec3-139">프로그램에 로그 만들기</span><span class="sxs-lookup"><span data-stu-id="84ec3-139">Create logs in Program</span></span>

<span data-ttu-id="84ec3-140">`Program` 클래스에 로그를 작성하려면 DI에서 `ILogger` 인스턴스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-140">To write logs in the `Program` class, get an `ILogger` instance from DI:</span></span>

[!code-csharp[](index/samples/2.x/TodoApiSample/Program.cs?name=snippet_LogFromMain&highlight=9,10)]

::: moniker-end

### <a name="no-asynchronous-logger-methods"></a><span data-ttu-id="84ec3-141">비동기 로거 메서드 없음</span><span class="sxs-lookup"><span data-stu-id="84ec3-141">No asynchronous logger methods</span></span>

<span data-ttu-id="84ec3-142">로깅은 매우 빨라서 비동기 코드의 성능 비용을 들일 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-142">Logging should be so fast that it isn't worth the performance cost of asynchronous code.</span></span> <span data-ttu-id="84ec3-143">로깅 데이터 저장소가 느린 경우 직접 작성하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="84ec3-143">If your logging data store is slow, don't write to it directly.</span></span> <span data-ttu-id="84ec3-144">로그 메시지를 처음에 빠른 저장소에 작성한 다음, 나중에 느린 저장소로 이동하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-144">Consider writing the log messages to a fast store initially, then move them to the slow store later.</span></span> <span data-ttu-id="84ec3-145">예를 들어 다른 프로세스에서 읽고 지속하는 느린 저장소인 메시지 큐에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-145">For example, log to a message queue that's read and persisted to slow storage by another process.</span></span>

## <a name="configuration"></a><span data-ttu-id="84ec3-146">구성</span><span class="sxs-lookup"><span data-stu-id="84ec3-146">Configuration</span></span>

<span data-ttu-id="84ec3-147">로깅 공급자 구성은 하나 이상의 구성 공급자에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-147">Logging provider configuration is provided by one or more configuration providers:</span></span>

* <span data-ttu-id="84ec3-148">파일 형식(INI, JSON 및 XML).</span><span class="sxs-lookup"><span data-stu-id="84ec3-148">File formats (INI, JSON, and XML).</span></span>
* <span data-ttu-id="84ec3-149">명령줄 인수.</span><span class="sxs-lookup"><span data-stu-id="84ec3-149">Command-line arguments.</span></span>
* <span data-ttu-id="84ec3-150">환경 변수.</span><span class="sxs-lookup"><span data-stu-id="84ec3-150">Environment variables.</span></span>
* <span data-ttu-id="84ec3-151">메모리 내 .NET 개체.</span><span class="sxs-lookup"><span data-stu-id="84ec3-151">In-memory .NET objects.</span></span>
* <span data-ttu-id="84ec3-152">암호화되지 않은 [암호 관리자](xref:security/app-secrets) 저장소.</span><span class="sxs-lookup"><span data-stu-id="84ec3-152">The unencrypted [Secret Manager](xref:security/app-secrets) storage.</span></span>
* <span data-ttu-id="84ec3-153">암호화된 사용자 저장소(예:[Azure Key Vault](xref:security/key-vault-configuration)).</span><span class="sxs-lookup"><span data-stu-id="84ec3-153">An encrypted user store, such as [Azure Key Vault](xref:security/key-vault-configuration).</span></span>
* <span data-ttu-id="84ec3-154">사용자 지정 공급자(설치 또는 생성된).</span><span class="sxs-lookup"><span data-stu-id="84ec3-154">Custom providers (installed or created).</span></span>

<span data-ttu-id="84ec3-155">예를 들어 로깅 구성은 일반적으로 앱 설정 파일의 `Logging` 섹션에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-155">For example, logging configuration is commonly provided by the `Logging` section of app settings files.</span></span> <span data-ttu-id="84ec3-156">다음 예제에서는 일반적인 *appsettings.Development.json* 파일의 콘텐츠를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-156">The following example shows the contents of a typical *appsettings.Development.json* file:</span></span>

::: moniker range=">= aspnetcore-2.1"

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Debug",
      "System": "Information",
      "Microsoft": "Information"
    },
    "Console":
    {
      "IncludeScopes": true
    }
  }
}
```

<span data-ttu-id="84ec3-157">`Logging` 속성은 `LogLevel` 및 로그 공급자 속성을 포함할 수 있습니다(콘솔이 표시됨).</span><span class="sxs-lookup"><span data-stu-id="84ec3-157">The `Logging` property can have `LogLevel` and log provider properties (Console is shown).</span></span>

<span data-ttu-id="84ec3-158">`Logging` 아래의 `LogLevel` 속성은 선택한 범주에 대해 로그할 최소 [수준](#log-level)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-158">The `LogLevel` property under `Logging` specifies the minimum [level](#log-level) to log for selected categories.</span></span> <span data-ttu-id="84ec3-159">이 예제에서는 `System` 및 `Microsoft` 범주는 `Information` 수준으로 로그되고 다른 모든 범주는 `Debug` 수준으로 로그됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-159">In the example, `System` and `Microsoft` categories log at `Information` level, and all others log at `Debug` level.</span></span>

<span data-ttu-id="84ec3-160">`Logging` 아래의 다른 속성은 로깅 공급자를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-160">Other properties under `Logging` specify logging providers.</span></span> <span data-ttu-id="84ec3-161">이 예제는 콘솔 공급자를 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-161">The example is for the Console provider.</span></span> <span data-ttu-id="84ec3-162">공급자가 [로그 범위](#log-scopes)를 지원하는 경우 `IncludeScopes`는 사용 가능 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-162">If a provider supports [log scopes](#log-scopes), `IncludeScopes` indicates whether they're enabled.</span></span> <span data-ttu-id="84ec3-163">공급자 속성(예: 예제에서 `Console`)은 `LogLevel` 속성을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-163">A provider property (such as `Console` in the example) may also specify a `LogLevel` property.</span></span> <span data-ttu-id="84ec3-164">공급자 아래의 `LogLevel`은 해당 공급자에 대한 로그 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-164">`LogLevel` under a provider specifies levels to log for that provider.</span></span>

<span data-ttu-id="84ec3-165">수준이 `Logging.{providername}.LogLevel`에 지정된 경우 `Logging.LogLevel`에 설정된 모든 수준을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-165">If levels are specified in `Logging.{providername}.LogLevel`, they override anything set in `Logging.LogLevel`.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.1"

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Debug",
      "System": "Information",
      "Microsoft": "Information"
    }
  }
}
```

<span data-ttu-id="84ec3-166">`LogLevel` 키는 로그 이름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-166">`LogLevel` keys represent log names.</span></span> <span data-ttu-id="84ec3-167">`Default` 키는 명시적으로 나열되지 않은 로그에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-167">The `Default` key applies to logs not explicitly listed.</span></span> <span data-ttu-id="84ec3-168">값은 지정된 로그에 적용된 [로그 수준](#log-level)을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-168">The value represents the [log level](#log-level) applied to the given log.</span></span>

::: moniker-end

<span data-ttu-id="84ec3-169">구성 공급자 구현에 대한 자세한 내용은 <xref:fundamentals/configuration/index>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="84ec3-169">For information on implementing configuration providers, see <xref:fundamentals/configuration/index>.</span></span>

## <a name="sample-logging-output"></a><span data-ttu-id="84ec3-170">샘플 로깅 출력</span><span class="sxs-lookup"><span data-stu-id="84ec3-170">Sample logging output</span></span>

<span data-ttu-id="84ec3-171">이전 섹션에 나와 있는 샘플 코드를 사용하면 명령줄에서 앱을 실행할 때 콘솔에 로그가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-171">With the sample code shown in the preceding section, logs appear in the console when the app is run from the command line.</span></span> <span data-ttu-id="84ec3-172">다음은 콘솔 출력의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-172">Here's an example of console output:</span></span>

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

<span data-ttu-id="84ec3-173">이전 로그는 `http://localhost:5000/api/todo/0`의 샘플 앱에 HTTP Get 요청을 하여 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-173">The preceding logs were generated by making an HTTP Get request to the sample app at `http://localhost:5000/api/todo/0`.</span></span>

<span data-ttu-id="84ec3-174">다음은 Visual Studio에서 샘플 앱을 실행할 때 디버그 창에 나타나는 것과 동일한 로그의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-174">Here's an example of the same logs as they appear in the Debug window when you run the sample app in Visual Studio:</span></span>


```console
Microsoft.AspNetCore.Hosting.Internal.WebHost:Information: Request starting HTTP/1.1 GET http://localhost:53104/api/todo/0  
Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker:Information: Executing action method TodoApi.Controllers.TodoController.GetById (TodoApi) with arguments (0) - ModelState is Valid
TodoApi.Controllers.TodoController:Information: Getting item 0
TodoApi.Controllers.TodoController:Warning: GetById(0) NOT FOUND
Microsoft.AspNetCore.Mvc.StatusCodeResult:Information: Executing HttpStatusCodeResult, setting HTTP status code 404
Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker:Information: Executed action TodoApi.Controllers.TodoController.GetById (TodoApi) in 152.5657ms
Microsoft.AspNetCore.Hosting.Internal.WebHost:Information: Request finished in 316.3195ms 404
```

<span data-ttu-id="84ec3-175">이전 섹션에 표시된 `ILogger` 호출을 통해 생성된 로그는 "TodoApi.Controllers.TodoController"로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-175">The logs that are created by the `ILogger` calls shown in the preceding section begin with "TodoApi.Controllers.TodoController".</span></span> <span data-ttu-id="84ec3-176">"Microsoft" 범주로 시작하는 로그는 ASP.NET Core 프레임워크 코드에서 온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-176">The logs that begin with "Microsoft" categories are from ASP.NET Core framework code.</span></span> <span data-ttu-id="84ec3-177">ASP.NET Core 및 응용 프로그램 코드는 동일한 로깅 API와 공급자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-177">ASP.NET Core and application code are using the same logging API and providers.</span></span>

<span data-ttu-id="84ec3-178">이 문서의 나머지 부분에서는 로깅에 대한 일부 세부 정보 및 옵션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-178">The remainder of this article explains some details and options for logging.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="84ec3-179">NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="84ec3-179">NuGet packages</span></span>

<span data-ttu-id="84ec3-180">`ILogger` 및 `ILoggerFactory` 인터페이스는 [Microsoft.Extensions.Logging.Abstractions](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Abstractions/)에 있으며, 두 인터페이스의 기본 구현은 [Microsoft.Extensions.Logging](https://www.nuget.org/packages/microsoft.extensions.logging/)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-180">The `ILogger` and `ILoggerFactory` interfaces are in [Microsoft.Extensions.Logging.Abstractions](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Abstractions/), and default implementations for them are in [Microsoft.Extensions.Logging](https://www.nuget.org/packages/microsoft.extensions.logging/).</span></span>

## <a name="log-category"></a><span data-ttu-id="84ec3-181">로그 범주</span><span class="sxs-lookup"><span data-stu-id="84ec3-181">Log category</span></span>

<span data-ttu-id="84ec3-182">`ILogger` 개체가 생성되면 개체에 대한 *범주*가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-182">When an `ILogger` object is created, a *category* is specified for it.</span></span> <span data-ttu-id="84ec3-183">해당 범주는 `Ilogger`의 해당 인스턴스에서 만든 각 로그 메시지에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-183">That category is included with each log message created by that instance of `Ilogger`.</span></span> <span data-ttu-id="84ec3-184">범주는 문자열일 수 있지만 "TodoApi.Controllers.TodoController"와 같은 클래스 이름을 사용하는 것이 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-184">The category may be any string, but the convention is to use the class name, such as "TodoApi.Controllers.TodoController".</span></span>

<span data-ttu-id="84ec3-185">`ILogger<T>`를 사용하여 `T`의 정규화된 형식 이름을 범주로 사용하는 `ILogger` 인스턴스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-185">Use `ILogger<T>` to get an `ILogger` instance that uses the fully qualified type name of `T` as the category:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/TodoApiSample/Controllers/TodoController.cs?name=snippet_LoggerDI&highlight=7)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/TodoApiSample/Controllers/TodoController.cs?name=snippet_LoggerDI&highlight=7)]

::: moniker-end

<span data-ttu-id="84ec3-186">범주를 명시적으로 지정하려면 `ILoggerFactory.CreateLogger`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-186">To explicitly specify the category, call `ILoggerFactory.CreateLogger`:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/TodoApiSample/Controllers/TodoController.cs?name=snippet_CreateLogger&highlight=7,10)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/TodoApiSample/Controllers/TodoController.cs?name=snippet_CreateLogger&highlight=7,10)]

::: moniker-end

<span data-ttu-id="84ec3-187">`ILogger<T>`는 `T`의 정규화된 형식 이름으로 `CreateLogger`를 호출하는 것과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-187">`ILogger<T>` is equivalent to calling `CreateLogger` with the fully qualified type name of `T`.</span></span>

## <a name="log-level"></a><span data-ttu-id="84ec3-188">로그 수준</span><span class="sxs-lookup"><span data-stu-id="84ec3-188">Log level</span></span>

<span data-ttu-id="84ec3-189">모든 로그는 <xref:Microsoft.Extensions.Logging.LogLevel> 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-189">Every log specifies a <xref:Microsoft.Extensions.Logging.LogLevel> value.</span></span> <span data-ttu-id="84ec3-190">로그 수준은 심각도 또는 중요도를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-190">The log level indicates the severity or importance.</span></span> <span data-ttu-id="84ec3-191">예를 들어 메서드가 정상적으로 종료되면 `Information` 로그를 작성하고 메서드가 *404 찾을 수 없음* 상태 코드를 반환할 때 `Warning` 로그를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-191">For example, you might write an `Information` log when a method ends normally and a `Warning` log when a method returns a *404 Not Found* status code.</span></span>

<span data-ttu-id="84ec3-192">다음 코드에서는 `Information` 및 `Warning` 코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-192">The following code creates `Information` and `Warning` logs:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/TodoApiSample/Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/TodoApiSample/Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

::: moniker-end

<span data-ttu-id="84ec3-193">이전 코드에서 첫 번째 매개 변수는 [로그 이벤트 ID](#log-event-id)입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-193">In the preceding code, the first parameter is the [Log event ID](#log-event-id).</span></span> <span data-ttu-id="84ec3-194">두 번째 매개 변수는 나머지 메서드 매개 변수가 제공하는 인수 값에 대한 자리 표시자가 있는 메시지 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-194">The second parameter is a message template with placeholders for argument values provided by the remaining method parameters.</span></span> <span data-ttu-id="84ec3-195">메서드 매개 변수는 이 문서의 뒷부분에 있는 [메시지 템플릿 섹션](#log-message-template)에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-195">The method parameters are explained in the [message template section](#log-message-template) later in this article.</span></span>

<span data-ttu-id="84ec3-196">메서드 이름(예: `LogInformation` 및 `LogWarning`)의 수준을 포함하는 로그 메서드는 [ILogger에 대한 확장 메서드](xref:Microsoft.Extensions.Logging.LoggerExtensions)입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-196">Log methods that include the level in the method name (for example, `LogInformation` and `LogWarning`) are [extension methods for ILogger](xref:Microsoft.Extensions.Logging.LoggerExtensions).</span></span> <span data-ttu-id="84ec3-197">이러한 메서드는 `LogLevel` 매개 변수를 사용하는 `Log` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-197">These methods call a `Log` method that takes a `LogLevel` parameter.</span></span> <span data-ttu-id="84ec3-198">이러한 확장 메서드 중 하나를 호출하는 대신 `Log` 메서드를 직접 호출할 수 있지만, 구문이 비교적 복잡합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-198">You can call the `Log` method directly rather than one of these extension methods, but the syntax is relatively complicated.</span></span> <span data-ttu-id="84ec3-199">자세한 내용은 <xref:Microsoft.Extensions.Logging.ILogger> 및 [로거 확장 소스 코드](https://github.com/aspnet/Logging/blob/master/src/Microsoft.Extensions.Logging.Abstractions/LoggerExtensions.cs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="84ec3-199">For more information, see <xref:Microsoft.Extensions.Logging.ILogger> and the [logger extensions source code](https://github.com/aspnet/Logging/blob/master/src/Microsoft.Extensions.Logging.Abstractions/LoggerExtensions.cs).</span></span>

<span data-ttu-id="84ec3-200">ASP.NET Core는 다음 로그 수준을 정의하며, 여기에 가장 낮은 심각도에서 가장 높은 심각도 순으로 정렬됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-200">ASP.NET Core defines the following log levels, ordered here from lowest to highest severity.</span></span>

* <span data-ttu-id="84ec3-201">추적 = 0</span><span class="sxs-lookup"><span data-stu-id="84ec3-201">Trace = 0</span></span>

  <span data-ttu-id="84ec3-202">일반적으로 디버깅에만 유용한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-202">For information that's typically valuable only for debugging.</span></span> <span data-ttu-id="84ec3-203">이러한 메시지는 중요한 응용 프로그램 데이터를 포함할 수 있으므로 프로덕션 환경에서 사용하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-203">These messages may contain sensitive application data and so shouldn't be enabled in a production environment.</span></span> <span data-ttu-id="84ec3-204">*기본적으로 사용하지 않도록 설정됩니다.*</span><span class="sxs-lookup"><span data-stu-id="84ec3-204">*Disabled by default.*</span></span>

* <span data-ttu-id="84ec3-205">디버그 = 1</span><span class="sxs-lookup"><span data-stu-id="84ec3-205">Debug = 1</span></span>

  <span data-ttu-id="84ec3-206">개발 및 디버깅에 유용할 수 있는 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-206">For information that may be useful in development and debugging.</span></span> <span data-ttu-id="84ec3-207">예: `Entering method Configure with flag set to true.` 로그 볼륨이 크기 때문에 문제 해결 시에만 `Debug` 수준 로그를 프로덕션 환경에서 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-207">Example: `Entering method Configure with flag set to true.` Enable `Debug` level logs in production only when troubleshooting, due to the high volume of logs.</span></span>

* <span data-ttu-id="84ec3-208">정보 = 2</span><span class="sxs-lookup"><span data-stu-id="84ec3-208">Information = 2</span></span>

  <span data-ttu-id="84ec3-209">앱의 일반적인 흐름을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-209">For tracking the general flow of the app.</span></span> <span data-ttu-id="84ec3-210">이러한 로그는 일반적으로 장기적인 가치가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-210">These logs typically have some long-term value.</span></span> <span data-ttu-id="84ec3-211">예: `Request received for path /api/todo`</span><span class="sxs-lookup"><span data-stu-id="84ec3-211">Example: `Request received for path /api/todo`</span></span>

* <span data-ttu-id="84ec3-212">경고 = 3</span><span class="sxs-lookup"><span data-stu-id="84ec3-212">Warning = 3</span></span>

  <span data-ttu-id="84ec3-213">앱 흐름에 비정상적이거나 예기치 않은 이벤트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-213">For abnormal or unexpected events in the app flow.</span></span> <span data-ttu-id="84ec3-214">앱이 중지되지 않지만 조사해야 하는 오류 또는 기타 조건이 여기에 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-214">These may include errors or other conditions that don't cause the app to stop but might need to be investigated.</span></span> <span data-ttu-id="84ec3-215">처리된 예외는 `Warning` 로그 수준을 사용하는 일반적인 장소입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-215">Handled exceptions are a common place to use the `Warning` log level.</span></span> <span data-ttu-id="84ec3-216">예: `FileNotFoundException for file quotes.txt.`</span><span class="sxs-lookup"><span data-stu-id="84ec3-216">Example: `FileNotFoundException for file quotes.txt.`</span></span>

* <span data-ttu-id="84ec3-217">오류 = 4</span><span class="sxs-lookup"><span data-stu-id="84ec3-217">Error = 4</span></span>

  <span data-ttu-id="84ec3-218">처리할 수 없는 오류 및 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-218">For errors and exceptions that cannot be handled.</span></span> <span data-ttu-id="84ec3-219">이러한 메시지는 전체 앱 오류가 아닌 현재 동작 또는 작업(예: 현재 HTTP 요청)의 오류를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-219">These messages indicate a failure in the current activity or operation (such as the current HTTP request), not an app-wide failure.</span></span> <span data-ttu-id="84ec3-220">예제 로그 메시지: `Cannot insert record due to duplicate key violation.`</span><span class="sxs-lookup"><span data-stu-id="84ec3-220">Example log message: `Cannot insert record due to duplicate key violation.`</span></span>

* <span data-ttu-id="84ec3-221">중요 = 5</span><span class="sxs-lookup"><span data-stu-id="84ec3-221">Critical = 5</span></span>

  <span data-ttu-id="84ec3-222">즉각적인 대응이 필요한 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-222">For failures that require immediate attention.</span></span> <span data-ttu-id="84ec3-223">예: 데이터 손실 시나리오, 디스크 공간 부족.</span><span class="sxs-lookup"><span data-stu-id="84ec3-223">Examples: data loss scenarios, out of disk space.</span></span>

<span data-ttu-id="84ec3-224">로그 수준을 사용하여 특정 저장 매체 또는 디스플레이 창에 기록되는 로그 출력의 양을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-224">Use the log level to control how much log output is written to a particular storage medium or display window.</span></span> <span data-ttu-id="84ec3-225">예:</span><span class="sxs-lookup"><span data-stu-id="84ec3-225">For example:</span></span>

* <span data-ttu-id="84ec3-226">프로덕션 환경에서 `Trace` ~ `Information` 수준을 볼륨 데이터 저장소로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-226">In production, send `Trace` through `Information` level to a volume data store.</span></span> <span data-ttu-id="84ec3-227">값 데이터 저장소에 `Warning` ~ `Critical`을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-227">Send `Warning` through `Critical` to a value data store.</span></span>
* <span data-ttu-id="84ec3-228">개발 중에 `Warning` ~ `Critical`을 콘솔에 보내고 문제 해결 시 `Trace` ~ `Information`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-228">During development, send `Warning` through `Critical` to the console, and add `Trace` through `Information` when troubleshooting.</span></span>

<span data-ttu-id="84ec3-229">이 문서의 뒷부분에 나오는 [로그 필터링](#log-filtering) 섹션에서는 공급자가 처리하는 로그 수준을 제어하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-229">The [Log filtering](#log-filtering) section later in this article explains how to control which log levels a provider handles.</span></span>

<span data-ttu-id="84ec3-230">ASP.NET Core는 프레임워크 이벤트에 대한 로그를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-230">ASP.NET Core writes logs for framework events.</span></span> <span data-ttu-id="84ec3-231">이 문서 앞부분에 나온 로그 예제는 `Information` 수준 미만 로그를 제외했기 때문에 `Debug` 또는 `Trace` 수준 로그가 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-231">The log examples earlier in this article excluded logs below `Information` level, so no `Debug` or `Trace` level logs were created.</span></span> <span data-ttu-id="84ec3-232">다음은 `Debug` 로그를 표시하도록 구성된 샘플 앱을 실행하여 생성된 콘솔 로그의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-232">Here's an example of console logs produced by running the sample app configured to show `Debug` logs:</span></span>

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

## <a name="log-event-id"></a><span data-ttu-id="84ec3-233">로그 이벤트 ID</span><span class="sxs-lookup"><span data-stu-id="84ec3-233">Log event ID</span></span>

<span data-ttu-id="84ec3-234">각 로그는 *이벤트 ID*를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-234">Each log can specify an *event ID*.</span></span> <span data-ttu-id="84ec3-235">샘플 앱은 로컬로 정의된 `LoggingEvents` 클래스를 사용하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-235">The sample app does this by using a locally defined `LoggingEvents` class:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/TodoApiSample/Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

[!code-csharp[](index/samples/2.x/TodoApiSample/Core/LoggingEvents.cs?name=snippet_LoggingEvents)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/TodoApiSample/Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

[!code-csharp[](index/samples/1.x/TodoApiSample/Core/LoggingEvents.cs?name=snippet_LoggingEvents)]

::: moniker-end

<span data-ttu-id="84ec3-236">이벤트 ID는 이벤트 집합을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-236">An event ID associates a set of events.</span></span> <span data-ttu-id="84ec3-237">예를 들어 페이지에서 항목 목록을 표시하는 것과 관련된 모든 로그는 1001일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-237">For example, all logs related to displaying a list of items on a page might be 1001.</span></span>

<span data-ttu-id="84ec3-238">로깅 공급자는 이벤트 ID를 ID 필드, 로그 메시지에 저장하거나 전혀 저장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-238">The logging provider may store the event ID in an ID field, in the logging message, or not at all.</span></span> <span data-ttu-id="84ec3-239">디버그 공급자는 이벤트 ID를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-239">The Debug provider doesn't show event IDs.</span></span> <span data-ttu-id="84ec3-240">콘솔 공급자는 범주 뒤에 대괄호로 이벤트 ID를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-240">The console provider shows event IDs in brackets after the category:</span></span>

```console
info: TodoApi.Controllers.TodoController[1002]
      Getting item invalidid
warn: TodoApi.Controllers.TodoController[4000]
      GetById(invalidid) NOT FOUND
```

## <a name="log-message-template"></a><span data-ttu-id="84ec3-241">로그 메시지 템플릿</span><span class="sxs-lookup"><span data-stu-id="84ec3-241">Log message template</span></span>

<span data-ttu-id="84ec3-242">각 로그는 메시지 템플릿을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-242">Each log specifies a message template.</span></span> <span data-ttu-id="84ec3-243">메시지 템플릿에는 인수가 제공되는 자리 표시자를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-243">The message template can contain placeholders for which arguments are provided.</span></span> <span data-ttu-id="84ec3-244">숫자가 아니라 자리 표시자의 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-244">Use names for the placeholders, not numbers.</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/TodoApiSample/Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/TodoApiSample/Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

::: moniker-end

<span data-ttu-id="84ec3-245">값을 제공하는 데 사용되는 매개 변수를 결정하는 것은 자리 표시자의 번호가 아닌 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-245">The order of placeholders, not their names, determines which parameters are used to provide their values.</span></span> <span data-ttu-id="84ec3-246">다음 코드에서는 매개 변수 이름이 메시지 템플릿 순서를 벗어났습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-246">In the following code, notice that the parameter names are out of sequence in the message template:</span></span>

```csharp
string p1 = "parm1";
string p2 = "parm2";
_logger.LogInformation("Parameter values: {p2}, {p1}", p1, p2);
```

<span data-ttu-id="84ec3-247">이 코드는 매개 변수 값을 순서대로 사용하여 로그 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-247">This code creates a log message with the parameter values in sequence:</span></span>

```
Parameter values: parm1, parm2
```

<span data-ttu-id="84ec3-248">로깅 프레임워크는 로깅 공급자가 [구조화된 로깅이라고도 하는 의미 체계 로깅](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging)을 구현할 수 있도록 이 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-248">The logging framework works this way so that logging providers can implement [semantic logging, also known as structured logging](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging).</span></span> <span data-ttu-id="84ec3-249">인수 자체는 서식이 지정된 메시지 템플릿뿐만 아니라 로깅 시스템에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-249">The arguments themselves are passed to the logging system, not just the formatted message template.</span></span> <span data-ttu-id="84ec3-250">이 정보를 통해 로깅 공급자는 매개 변수 값을 필드로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-250">This information enables logging providers to store the parameter values as fields.</span></span> <span data-ttu-id="84ec3-251">예를 들어 로거 메서드 호출이 다음과 같다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-251">For example, suppose logger method calls look like this:</span></span>

```csharp
_logger.LogInformation("Getting item {ID} at {RequestTime}", id, DateTime.Now);
```

<span data-ttu-id="84ec3-252">Azure Table Storage에 로그를 보내는 경우 각 Azure Table 엔터티는 로그 데이터에 대한 쿼리를 간소화하는 `ID` 및 `RequestTime` 속성을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-252">If you're sending the logs to Azure Table Storage, each Azure Table entity can have `ID` and `RequestTime` properties, which simplifies queries on log data.</span></span> <span data-ttu-id="84ec3-253">쿼리는 문자 메시지의 시간 초과를 구문 분석하지 않고 특정 `RequestTime` 범위 내의 모든 로그를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-253">A query can find all logs within a particular `RequestTime` range without parsing the time out of the text message.</span></span>

## <a name="logging-exceptions"></a><span data-ttu-id="84ec3-254">로깅 처리</span><span class="sxs-lookup"><span data-stu-id="84ec3-254">Logging exceptions</span></span>

<span data-ttu-id="84ec3-255">로거 메서드는 다음 예제와 같이 예외를 전달할 수 있는 오버로드를 갖고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-255">The logger methods have overloads that let you pass in an exception, as in the following example:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/TodoApiSample/Controllers/TodoController.cs?name=snippet_LogException&highlight=3)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/TodoApiSample/Controllers/TodoController.cs?name=snippet_LogException&highlight=3)]

::: moniker-end

<span data-ttu-id="84ec3-256">공급자들은 다양한 방식으로 예외 정보를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-256">Different providers handle the exception information in different ways.</span></span> <span data-ttu-id="84ec3-257">다음은 위에서 보여드린 코드의 디버그 공급자 출력의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-257">Here's an example of Debug provider output from the code shown above.</span></span>

```
TodoApi.Controllers.TodoController:Warning: GetById(036dd898-fb01-47e8-9a65-f92eb73cf924) NOT FOUND

System.Exception: Item not found exception.
 at TodoApi.Controllers.TodoController.GetById(String id) in C:\logging\sample\src\TodoApi\Controllers\TodoController.cs:line 226
```

## <a name="log-filtering"></a><span data-ttu-id="84ec3-258">로깅 필터링</span><span class="sxs-lookup"><span data-stu-id="84ec3-258">Log filtering</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="84ec3-259">특정 공급자 및 범주 또는 모든 공급자나 모든 범주의 최소 로그 수준을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-259">You can specify a minimum log level for a specific provider and category or for all providers or all categories.</span></span> <span data-ttu-id="84ec3-260">최소 수준 미만인 로그는 해당 공급자에게 전달되지 않으므로 표시되거나 저장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-260">Any logs below the minimum level aren't passed to that provider, so they don't get displayed or stored.</span></span>

<span data-ttu-id="84ec3-261">모든 로그를 표시하지 않으려면 `LogLevel.None`을 최소 로그 수준으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-261">To suppress all logs, specify `LogLevel.None` as the minimum log level.</span></span> <span data-ttu-id="84ec3-262">`LogLevel.None`의 정수 값은 `LogLevel.Critical`(5)보다 높은 6입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-262">The integer value of `LogLevel.None` is 6, which is higher than `LogLevel.Critical` (5).</span></span>

### <a name="create-filter-rules-in-configuration"></a><span data-ttu-id="84ec3-263">구성에서 필터 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="84ec3-263">Create filter rules in configuration</span></span>

<span data-ttu-id="84ec3-264">프로젝트 템플릿 코드는 `CreateDefaultBuilder`를 호출하여 콘솔 및 디버그 공급자에 대한 로깅을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-264">The project template code calls `CreateDefaultBuilder` to set up logging for the Console and Debug providers.</span></span> <span data-ttu-id="84ec3-265">또한 `CreateDefaultBuilder` 메서드는 다음과 같은 코드를 사용하여 `Logging` 섹션에서 구성을 조회하는 로깅을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-265">The `CreateDefaultBuilder` method also sets up logging to look for configuration in a `Logging` section, using code like the following:</span></span>

[!code-csharp[](index/samples/2.x/TodoApiSample/Program.cs?name=snippet_ExpandDefault&highlight=16)]

<span data-ttu-id="84ec3-266">구성 데이터는 다음 예제와 같이 공급자 및 범주별로 최소 로그 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-266">The configuration data specifies minimum log levels by provider and category, as in the following example:</span></span>

[!code-json[](index/samples/2.x/TodoApiSample/appsettings.json)]

<span data-ttu-id="84ec3-267">이 JSON은 6개의 필터 규칙을 만드는데, 하나는 디버그 공급자용이고, 4개는 콘솔 공급자용이고, 나머지 하나는 모든 공급자용입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-267">This JSON creates six filter rules: one for the Debug provider, four for the Console provider, and one for all providers.</span></span> <span data-ttu-id="84ec3-268">`ILogger` 개체가 생성될 때 각 공급자에 대해 단일 규칙이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-268">A single rule is chosen for each provider when an `ILogger` object is created.</span></span>

### <a name="filter-rules-in-code"></a><span data-ttu-id="84ec3-269">코드의 필터 규칙</span><span class="sxs-lookup"><span data-stu-id="84ec3-269">Filter rules in code</span></span>

<span data-ttu-id="84ec3-270">다음 예제에서는 코드에 필터 규칙을 등록하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-270">The following example shows how to register filter rules in code:</span></span>

[!code-csharp[](index/samples/2.x/TodoApiSample/Program.cs?name=snippet_FilterInCode&highlight=4-5)]

<span data-ttu-id="84ec3-271">두 번째 `AddFilter`는 형식 이름을 사용하여 디버그 공급자를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-271">The second `AddFilter` specifies the Debug provider by using its type name.</span></span> <span data-ttu-id="84ec3-272">첫 번째 `AddFilter`는 공급자 형식을 지정하지 않으며, 따라서 모든 공급자에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-272">The first `AddFilter` applies to all providers because it doesn't specify a provider type.</span></span>

### <a name="how-filtering-rules-are-applied"></a><span data-ttu-id="84ec3-273">필터링 규칙 적용 방식</span><span class="sxs-lookup"><span data-stu-id="84ec3-273">How filtering rules are applied</span></span>

<span data-ttu-id="84ec3-274">이전 예제의 구성 데이터 및 `AddFilter` 코드는 다음 표에 표시된 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-274">The configuration data and the `AddFilter` code shown in the preceding examples create the rules shown in the following table.</span></span> <span data-ttu-id="84ec3-275">처음 6개는 구성 예제에서 가져온 것이고 마지막 2개는 코드 예제에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-275">The first six come from the configuration example and the last two come from the code example.</span></span>

| <span data-ttu-id="84ec3-276">수</span><span class="sxs-lookup"><span data-stu-id="84ec3-276">Number</span></span> | <span data-ttu-id="84ec3-277">공급자</span><span class="sxs-lookup"><span data-stu-id="84ec3-277">Provider</span></span>      | <span data-ttu-id="84ec3-278">다음으로 시작하는 범주...</span><span class="sxs-lookup"><span data-stu-id="84ec3-278">Categories that begin with ...</span></span>          | <span data-ttu-id="84ec3-279">최소 로그 수준</span><span class="sxs-lookup"><span data-stu-id="84ec3-279">Minimum log level</span></span> |
| :----: | ------------- | --------------------------------------- | ----------------- |
| <span data-ttu-id="84ec3-280">1</span><span class="sxs-lookup"><span data-stu-id="84ec3-280">1</span></span>      | <span data-ttu-id="84ec3-281">디버그</span><span class="sxs-lookup"><span data-stu-id="84ec3-281">Debug</span></span>         | <span data-ttu-id="84ec3-282">모든 범주</span><span class="sxs-lookup"><span data-stu-id="84ec3-282">All categories</span></span>                          | <span data-ttu-id="84ec3-283">정보</span><span class="sxs-lookup"><span data-stu-id="84ec3-283">Information</span></span>       |
| <span data-ttu-id="84ec3-284">2</span><span class="sxs-lookup"><span data-stu-id="84ec3-284">2</span></span>      | <span data-ttu-id="84ec3-285">콘솔</span><span class="sxs-lookup"><span data-stu-id="84ec3-285">Console</span></span>       | <span data-ttu-id="84ec3-286">Microsoft.AspNetCore.Mvc.Razor.Internal</span><span class="sxs-lookup"><span data-stu-id="84ec3-286">Microsoft.AspNetCore.Mvc.Razor.Internal</span></span> | <span data-ttu-id="84ec3-287">경고</span><span class="sxs-lookup"><span data-stu-id="84ec3-287">Warning</span></span>           |
| <span data-ttu-id="84ec3-288">3</span><span class="sxs-lookup"><span data-stu-id="84ec3-288">3</span></span>      | <span data-ttu-id="84ec3-289">콘솔</span><span class="sxs-lookup"><span data-stu-id="84ec3-289">Console</span></span>       | <span data-ttu-id="84ec3-290">Microsoft.AspNetCore.Mvc.Razor.Razor</span><span class="sxs-lookup"><span data-stu-id="84ec3-290">Microsoft.AspNetCore.Mvc.Razor.Razor</span></span>    | <span data-ttu-id="84ec3-291">디버그</span><span class="sxs-lookup"><span data-stu-id="84ec3-291">Debug</span></span>             |
| <span data-ttu-id="84ec3-292">4</span><span class="sxs-lookup"><span data-stu-id="84ec3-292">4</span></span>      | <span data-ttu-id="84ec3-293">콘솔</span><span class="sxs-lookup"><span data-stu-id="84ec3-293">Console</span></span>       | <span data-ttu-id="84ec3-294">Microsoft.AspNetCore.Mvc.Razor</span><span class="sxs-lookup"><span data-stu-id="84ec3-294">Microsoft.AspNetCore.Mvc.Razor</span></span>          | <span data-ttu-id="84ec3-295">Error</span><span class="sxs-lookup"><span data-stu-id="84ec3-295">Error</span></span>             |
| <span data-ttu-id="84ec3-296">5</span><span class="sxs-lookup"><span data-stu-id="84ec3-296">5</span></span>      | <span data-ttu-id="84ec3-297">콘솔</span><span class="sxs-lookup"><span data-stu-id="84ec3-297">Console</span></span>       | <span data-ttu-id="84ec3-298">모든 범주</span><span class="sxs-lookup"><span data-stu-id="84ec3-298">All categories</span></span>                          | <span data-ttu-id="84ec3-299">정보</span><span class="sxs-lookup"><span data-stu-id="84ec3-299">Information</span></span>       |
| <span data-ttu-id="84ec3-300">6</span><span class="sxs-lookup"><span data-stu-id="84ec3-300">6</span></span>      | <span data-ttu-id="84ec3-301">모든 공급자</span><span class="sxs-lookup"><span data-stu-id="84ec3-301">All providers</span></span> | <span data-ttu-id="84ec3-302">모든 범주</span><span class="sxs-lookup"><span data-stu-id="84ec3-302">All categories</span></span>                          | <span data-ttu-id="84ec3-303">디버그</span><span class="sxs-lookup"><span data-stu-id="84ec3-303">Debug</span></span>             |
| <span data-ttu-id="84ec3-304">7</span><span class="sxs-lookup"><span data-stu-id="84ec3-304">7</span></span>      | <span data-ttu-id="84ec3-305">모든 공급자</span><span class="sxs-lookup"><span data-stu-id="84ec3-305">All providers</span></span> | <span data-ttu-id="84ec3-306">시스템</span><span class="sxs-lookup"><span data-stu-id="84ec3-306">System</span></span>                                  | <span data-ttu-id="84ec3-307">디버그</span><span class="sxs-lookup"><span data-stu-id="84ec3-307">Debug</span></span>             |
| <span data-ttu-id="84ec3-308">8</span><span class="sxs-lookup"><span data-stu-id="84ec3-308">8</span></span>      | <span data-ttu-id="84ec3-309">디버그</span><span class="sxs-lookup"><span data-stu-id="84ec3-309">Debug</span></span>         | <span data-ttu-id="84ec3-310">Microsoft</span><span class="sxs-lookup"><span data-stu-id="84ec3-310">Microsoft</span></span>                               | <span data-ttu-id="84ec3-311">추적</span><span class="sxs-lookup"><span data-stu-id="84ec3-311">Trace</span></span>             |

<span data-ttu-id="84ec3-312">`ILogger` 개체를 만들 때 `ILoggerFactory` 개체는 공급자마다 해당 로거에 적용할 단일 규칙을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-312">When an `ILogger` object is created, the `ILoggerFactory` object selects a single rule per provider to apply to that logger.</span></span> <span data-ttu-id="84ec3-313">`ILogger` 인스턴스에서 작성된 모든 메시지는 선택한 규칙에 따라 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-313">All messages written by an `ILogger` instance are filtered based on the selected rules.</span></span> <span data-ttu-id="84ec3-314">사용 가능한 규칙 중에서 각 공급자 및 범주 쌍에 적용 가능한 가장 구체적인 규칙이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-314">The most specific rule possible for each provider and category pair is selected from the available rules.</span></span>

<span data-ttu-id="84ec3-315">지정된 범주에 대한 `ILogger`가 생성되면 다음 알고리즘이 각 공급자에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-315">The following algorithm is used for each provider when an `ILogger` is created for a given category:</span></span>

* <span data-ttu-id="84ec3-316">공급자 또는 공급자의 별칭과 일치하는 모든 규칙을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-316">Select all rules that match the provider or its alias.</span></span> <span data-ttu-id="84ec3-317">일치하는 규칙이 없는 경우 빈 공급자가 있는 모든 규칙을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-317">If no match is found, select all rules with an empty provider.</span></span>
* <span data-ttu-id="84ec3-318">앞 단계의 결과에서 일치하는 범주 접두사가 가장 긴 규칙을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-318">From the result of the preceding step, select rules with longest matching category prefix.</span></span> <span data-ttu-id="84ec3-319">일치하는 규칙이 없는 경우 범주를 지정하지 않는 규칙을 모두 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-319">If no match is found, select all rules that don't specify a category.</span></span>
* <span data-ttu-id="84ec3-320">여러 규칙을 선택하는 경우 **마지막** 규칙을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-320">If multiple rules are selected, take the **last** one.</span></span>
* <span data-ttu-id="84ec3-321">규칙을 선택하지 않는 경우 `MinimumLevel`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-321">If no rules are selected, use `MinimumLevel`.</span></span>

<span data-ttu-id="84ec3-322">앞의 규칙 목록을 통해 "Microsoft.AspNetCore.Mvc.Razor.RazorViewEngine" 범주에 대한 `ILogger` 개체를 만든다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-322">With the preceding list of rules, suppose you create an `ILogger` object for category "Microsoft.AspNetCore.Mvc.Razor.RazorViewEngine":</span></span>

* <span data-ttu-id="84ec3-323">디버그 공급자에게는 규칙 1, 6, 8이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-323">For the Debug provider, rules 1, 6, and 8 apply.</span></span> <span data-ttu-id="84ec3-324">규칙 8이 가장 구체적이므로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-324">Rule 8 is most specific, so that's the one selected.</span></span>
* <span data-ttu-id="84ec3-325">콘솔 공급자에게는 규칙 3, 4, 5, 6이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-325">For the Console provider, rules 3, 4, 5, and 6 apply.</span></span> <span data-ttu-id="84ec3-326">규칙 3이 가장 구체적입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-326">Rule 3 is most specific.</span></span>

<span data-ttu-id="84ec3-327">결과 `ILogger` 인스턴스는 `Trace` 수준 이상의 로그를 디버그 공급자에게 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-327">The resulting `ILogger` instance sends logs of `Trace` level and above to the Debug provider.</span></span> <span data-ttu-id="84ec3-328">`Debug` 수준 이상의 로그가 콘솔 공급자에게 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-328">Logs of `Debug` level and above are sent to the Console provider.</span></span>

### <a name="provider-aliases"></a><span data-ttu-id="84ec3-329">공급자 별칭</span><span class="sxs-lookup"><span data-stu-id="84ec3-329">Provider aliases</span></span>

<span data-ttu-id="84ec3-330">각 공급자는 정규화된 형식 이름 대신 구성에서 사용할 수 있는 *별칭*을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-330">Each provider defines an *alias* that can be used in configuration in place of the fully qualified type name.</span></span>  <span data-ttu-id="84ec3-331">기본 공급자의 경우 다음 별칭을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-331">For the built-in providers, use the following aliases:</span></span>

* <span data-ttu-id="84ec3-332">콘솔</span><span class="sxs-lookup"><span data-stu-id="84ec3-332">Console</span></span>
* <span data-ttu-id="84ec3-333">디버그</span><span class="sxs-lookup"><span data-stu-id="84ec3-333">Debug</span></span>
* <span data-ttu-id="84ec3-334">EventLog</span><span class="sxs-lookup"><span data-stu-id="84ec3-334">EventLog</span></span>
* <span data-ttu-id="84ec3-335">AzureAppServices</span><span class="sxs-lookup"><span data-stu-id="84ec3-335">AzureAppServices</span></span>
* <span data-ttu-id="84ec3-336">TraceSource</span><span class="sxs-lookup"><span data-stu-id="84ec3-336">TraceSource</span></span>
* <span data-ttu-id="84ec3-337">EventSource</span><span class="sxs-lookup"><span data-stu-id="84ec3-337">EventSource</span></span>

### <a name="default-minimum-level"></a><span data-ttu-id="84ec3-338">기본 최소 수준</span><span class="sxs-lookup"><span data-stu-id="84ec3-338">Default minimum level</span></span>

<span data-ttu-id="84ec3-339">특정 공급자 및 범주에 대한 구성 또는 코드의 규칙이 적용되지 않는 경우에만 효력이 있는 최소 수준 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-339">There's a minimum level setting that takes effect only if no rules from configuration or code apply for a given provider and category.</span></span> <span data-ttu-id="84ec3-340">다음 예제는 최소 수준을 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-340">The following example shows how to set the minimum level:</span></span>

[!code-csharp[](index/samples/2.x/TodoApiSample/Program.cs?name=snippet_MinLevel&highlight=3)]

<span data-ttu-id="84ec3-341">최소 수준을 명시적으로 설정하지 않으면 `Trace` 및 `Debug` 로그를 무시하는 `Information`이 기본값으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-341">If you don't explicitly set the minimum level, the default value is `Information`, which means that `Trace` and `Debug` logs are ignored.</span></span>

### <a name="filter-functions"></a><span data-ttu-id="84ec3-342">필터 함수</span><span class="sxs-lookup"><span data-stu-id="84ec3-342">Filter functions</span></span>

<span data-ttu-id="84ec3-343">필터 함수는 구성 또는 코드를 통해 규칙이 할당되지 않은 모든 공급자와 범주에 대해 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-343">A filter function is invoked for all providers and categories that don't have rules assigned to them by configuration or code.</span></span> <span data-ttu-id="84ec3-344">함수의 코드는 공급자 형식, 범주 및 로그 수준에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-344">Code in the function has access to the provider type, category, and log level.</span></span> <span data-ttu-id="84ec3-345">예:</span><span class="sxs-lookup"><span data-stu-id="84ec3-345">For example:</span></span>

[!code-csharp[](index/samples/2.x/TodoApiSample/Program.cs?name=snippet_FilterFunction&highlight=5-13)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="84ec3-346">일부 로깅 공급자는 로그 수준 및 범주에 따라 로그를 저장 매체에 기록할 것인지 아니면 무시할 것인지를 개발자가 지정할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-346">Some logging providers let you specify when logs should be written to a storage medium or ignored based on log level and category.</span></span>

<span data-ttu-id="84ec3-347">`AddConsole` 및 `AddDebug` 확장 메서드는 필터링 조건을 허용하는 오버로드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-347">The `AddConsole` and `AddDebug` extension methods provide overloads that accept filtering criteria.</span></span> <span data-ttu-id="84ec3-348">다음 샘플 코드는 콘솔 공급자가 `Warning` 수준 미만의 로그를 무시하게 만들고, 디버그 공급자는 프레임워크에서 만드는 로그를 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-348">The following sample code causes the console provider to ignore logs below `Warning` level, while the Debug provider ignores logs that the framework creates.</span></span>

[!code-csharp[](index/samples/1.x/TodoApiSample/Startup.cs?name=snippet_AddConsoleAndDebugWithFilter&highlight=6-7)]

<span data-ttu-id="84ec3-349">`AddEventLog` 메서드는 `EventLogSettings` 인스턴스를 사용하는 오버로드를 갖고 있으며, 이 인스턴스의 `Filter` 속성에는 필터링 함수가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-349">The `AddEventLog` method has an overload that takes an `EventLogSettings` instance, which may contain a filtering function in its `Filter` property.</span></span> <span data-ttu-id="84ec3-350">TraceSource 공급자는 오버로드를 제공하지 않습니다. 로깅 수준 및 기타 매개 변수가 사용하는 `SourceSwitch` 및 `TraceListener`를 기반으로 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-350">The TraceSource provider doesn't provide any of those overloads, since its logging level and other parameters are based on the `SourceSwitch` and `TraceListener` it uses.</span></span>

<span data-ttu-id="84ec3-351">`ILoggerFactory` 인스턴스에 등록된 모든 공급자에 대한 필터링 규칙을 설정하려면 `WithFilter` 확장 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-351">To set filtering rules for all providers that are registered with an `ILoggerFactory` instance, use the `WithFilter` extension method.</span></span> <span data-ttu-id="84ec3-352">아래 예제는 앱 코드로 생성된 로그에 대한 디버그 수준에서 로깅하는 동안 프레임워크 로그(범주가 "Microsoft" 또는 "시스템"으로 시작)를 경고로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-352">The example below limits framework logs (category begins with "Microsoft" or "System") to warnings while logging at debug level for logs created by application code.</span></span>

[!code-csharp[](index/samples/1.x/TodoApiSample/Startup.cs?name=snippet_FactoryFilter&highlight=6-11)]

<span data-ttu-id="84ec3-353">로그가 기록되지 않도록 하려면 `LogLevel.None`을 최소 로그 수준으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-353">To prevent any logs from being written, specify `LogLevel.None` as the minimum log level.</span></span> <span data-ttu-id="84ec3-354">`LogLevel.None`의 정수 값은 `LogLevel.Critical`(5)보다 높은 6입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-354">The integer value of `LogLevel.None` is 6, which is higher than `LogLevel.Critical` (5).</span></span>

<span data-ttu-id="84ec3-355">`WithFilter` 확장 메서드는 [Microsoft.Extensions.Logging.Filter](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Filter) NuGet 패키지에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-355">The `WithFilter` extension method is provided by the [Microsoft.Extensions.Logging.Filter](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Filter) NuGet package.</span></span> <span data-ttu-id="84ec3-356">이 메서드는 등록된 모든 로거 공급자로 전달되는 메시지를 필터링하는 새로운 `ILoggerFactory` 인스턴스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-356">The method returns a new `ILoggerFactory` instance that will filter the log messages passed to all logger providers registered with it.</span></span> <span data-ttu-id="84ec3-357">원래 `ILoggerFactory` 인스턴스를 포함하여 어떤 `ILoggerFactory` 인스턴스에도 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-357">It doesn't affect any other `ILoggerFactory` instances, including the original `ILoggerFactory` instance.</span></span>

::: moniker-end

## <a name="system-categories-and-levels"></a><span data-ttu-id="84ec3-358">시스템 범주 및 수준</span><span class="sxs-lookup"><span data-stu-id="84ec3-358">System categories and levels</span></span>

<span data-ttu-id="84ec3-359">다음은 ASP.NET Core 및 Entity Framework Core에서 사용되는 몇 가지 범주로, 예상되는 로그에 대한 참고 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-359">Here are some categories used by ASP.NET Core and Entity Framework Core, with notes about what logs to expect from them:</span></span>

| <span data-ttu-id="84ec3-360">범주</span><span class="sxs-lookup"><span data-stu-id="84ec3-360">Category</span></span>                            | <span data-ttu-id="84ec3-361">노트</span><span class="sxs-lookup"><span data-stu-id="84ec3-361">Notes</span></span> |
| ----------------------------------- | ----- |
| <span data-ttu-id="84ec3-362">Microsoft.AspNetCore</span><span class="sxs-lookup"><span data-stu-id="84ec3-362">Microsoft.AspNetCore</span></span>                | <span data-ttu-id="84ec3-363">일반 ASP.NET Core 진단.</span><span class="sxs-lookup"><span data-stu-id="84ec3-363">General ASP.NET Core diagnostics.</span></span> |
| <span data-ttu-id="84ec3-364">Microsoft.AspNetCore.DataProtection</span><span class="sxs-lookup"><span data-stu-id="84ec3-364">Microsoft.AspNetCore.DataProtection</span></span> | <span data-ttu-id="84ec3-365">고려되고, 발견되고, 사용된 키.</span><span class="sxs-lookup"><span data-stu-id="84ec3-365">Which keys were considered, found, and used.</span></span> |
| <span data-ttu-id="84ec3-366">Microsoft.AspNetCore.HostFiltering</span><span class="sxs-lookup"><span data-stu-id="84ec3-366">Microsoft.AspNetCore.HostFiltering</span></span>  | <span data-ttu-id="84ec3-367">호스트가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-367">Hosts allowed.</span></span> |
| <span data-ttu-id="84ec3-368">Microsoft.AspNetCore.Hosting</span><span class="sxs-lookup"><span data-stu-id="84ec3-368">Microsoft.AspNetCore.Hosting</span></span>        | <span data-ttu-id="84ec3-369">HTTP 요청을 완료하는 데 걸린 시간과 시작 시간.</span><span class="sxs-lookup"><span data-stu-id="84ec3-369">How long HTTP requests took to complete and what time they started.</span></span> <span data-ttu-id="84ec3-370">로드된 호스팅 시작 어셈블리.</span><span class="sxs-lookup"><span data-stu-id="84ec3-370">Which hosting startup assemblies were loaded.</span></span> |
| <span data-ttu-id="84ec3-371">Microsoft.AspNetCore.Mvc</span><span class="sxs-lookup"><span data-stu-id="84ec3-371">Microsoft.AspNetCore.Mvc</span></span>            | <span data-ttu-id="84ec3-372">MVC 및 Razor 진단.</span><span class="sxs-lookup"><span data-stu-id="84ec3-372">MVC and Razor diagnostics.</span></span> <span data-ttu-id="84ec3-373">모델 바인딩, 필터 실행, 뷰 컴파일 작업 선택.</span><span class="sxs-lookup"><span data-stu-id="84ec3-373">Model binding, filter execution, view compilation, action selection.</span></span> |
| <span data-ttu-id="84ec3-374">Microsoft.AspNetCore.Routing</span><span class="sxs-lookup"><span data-stu-id="84ec3-374">Microsoft.AspNetCore.Routing</span></span>        | <span data-ttu-id="84ec3-375">경로 일치 정보.</span><span class="sxs-lookup"><span data-stu-id="84ec3-375">Route matching information.</span></span> |
| <span data-ttu-id="84ec3-376">Microsoft.AspNetCore.Server</span><span class="sxs-lookup"><span data-stu-id="84ec3-376">Microsoft.AspNetCore.Server</span></span>         | <span data-ttu-id="84ec3-377">연결 시작, 중지 및 활성 응답 유지.</span><span class="sxs-lookup"><span data-stu-id="84ec3-377">Connection start, stop, and keep alive responses.</span></span> <span data-ttu-id="84ec3-378">HTTPS 인증서 정보.</span><span class="sxs-lookup"><span data-stu-id="84ec3-378">HTTPS certificate information.</span></span> |
| <span data-ttu-id="84ec3-379">Microsoft.AspNetCore.StaticFiles</span><span class="sxs-lookup"><span data-stu-id="84ec3-379">Microsoft.AspNetCore.StaticFiles</span></span>    | <span data-ttu-id="84ec3-380">파일이 제공되었습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-380">Files served.</span></span> |
| <span data-ttu-id="84ec3-381">Microsoft.EntityFrameworkCore</span><span class="sxs-lookup"><span data-stu-id="84ec3-381">Microsoft.EntityFrameworkCore</span></span>       | <span data-ttu-id="84ec3-382">일반 Entity Framework Core 진단.</span><span class="sxs-lookup"><span data-stu-id="84ec3-382">General Entity Framework Core diagnostics.</span></span> <span data-ttu-id="84ec3-383">데이터베이스 작업 및 구성, 변경 내용 검색, 마이그레이션.</span><span class="sxs-lookup"><span data-stu-id="84ec3-383">Database activity and configuration, change detection, migrations.</span></span> |

## <a name="log-scopes"></a><span data-ttu-id="84ec3-384">로그 점수</span><span class="sxs-lookup"><span data-stu-id="84ec3-384">Log scopes</span></span>

 <span data-ttu-id="84ec3-385">*범위*는 논리적 작업 집합을 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-385">A *scope* can group a set of logical operations.</span></span> <span data-ttu-id="84ec3-386">이 그룹화는 집합의 일부로 생성된 각 로그에 동일한 데이터를 연결하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-386">This grouping can be used to attach the same data to each log that's created as part of a set.</span></span> <span data-ttu-id="84ec3-387">예를 들어 트랜잭션 처리의 일부로 생성되는 모든 로그에는 트랜잭션 ID가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-387">For example, every log created as part of processing a transaction can include the transaction ID.</span></span>

<span data-ttu-id="84ec3-388">범위는 <xref:Microsoft.Extensions.Logging.ILogger.BeginScope*> 메서드에서 반환하는 `IDisposable` 형식이며 삭제될 때까지 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-388">A scope is an `IDisposable` type that's returned by the <xref:Microsoft.Extensions.Logging.ILogger.BeginScope*> method and lasts until it's disposed.</span></span> <span data-ttu-id="84ec3-389">`using` 블록에 로거 호출을 래핑하여 범위를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-389">Use a scope by wrapping logger calls in a `using` block:</span></span>

[!code-csharp[](index/samples/1.x/TodoApiSample/Controllers/TodoController.cs?name=snippet_Scopes&highlight=4-5,13)]

<span data-ttu-id="84ec3-390">다음은 콘솔 공급자에 대한 범위를 사용하도록 설정하는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-390">The following code enables scopes for the console provider:</span></span>

::: moniker range="> aspnetcore-2.0"

<span data-ttu-id="84ec3-391">*Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="84ec3-391">*Program.cs*:</span></span>

[!code-csharp[](index/samples/2.x/TodoApiSample/Program.cs?name=snippet_Scopes&highlight=4)]

> [!NOTE]
> <span data-ttu-id="84ec3-392">범위 기반 로깅을 사용하려면 `IncludeScopes` 콘솔 로거 옵션을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-392">Configuring the `IncludeScopes` console logger option is required to enable scope-based logging.</span></span>
>
> <span data-ttu-id="84ec3-393">구성에 대한 자세한 내용은 [구성](#configuration) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="84ec3-393">For information on configuration, see the [Configuration](#configuration) section.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="84ec3-394">*Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="84ec3-394">*Program.cs*:</span></span>

[!code-csharp[](index/samples/2.x/TodoApiSample/Program.cs?name=snippet_Scopes&highlight=4)]

> [!NOTE]
> <span data-ttu-id="84ec3-395">범위 기반 로깅을 사용하려면 `IncludeScopes` 콘솔 로거 옵션을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-395">Configuring the `IncludeScopes` console logger option is required to enable scope-based logging.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="84ec3-396">*Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="84ec3-396">*Startup.cs*:</span></span>

[!code-csharp[](index/samples/1.x/TodoApiSample/Startup.cs?name=snippet_Scopes&highlight=6)]

::: moniker-end

<span data-ttu-id="84ec3-397">각 로그 메시지는 범위 정보를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-397">Each log message includes the scoped information:</span></span>

```
info: TodoApi.Controllers.TodoController[1002]
      => RequestId:0HKV9C49II9CK RequestPath:/api/todo/0 => TodoApi.Controllers.TodoController.GetById (TodoApi) => Message attached to logs created in the using block
      Getting item 0
warn: TodoApi.Controllers.TodoController[4000]
      => RequestId:0HKV9C49II9CK RequestPath:/api/todo/0 => TodoApi.Controllers.TodoController.GetById (TodoApi) => Message attached to logs created in the using block
      GetById(0) NOT FOUND
```

## <a name="built-in-logging-providers"></a><span data-ttu-id="84ec3-398">기본 로깅 공급자</span><span class="sxs-lookup"><span data-stu-id="84ec3-398">Built-in logging providers</span></span>

<span data-ttu-id="84ec3-399">ASP.NET Core는 다음 공급자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-399">ASP.NET Core ships the following providers:</span></span>

* [<span data-ttu-id="84ec3-400">콘솔</span><span class="sxs-lookup"><span data-stu-id="84ec3-400">Console</span></span>](#console-provider)
* [<span data-ttu-id="84ec3-401">디버그</span><span class="sxs-lookup"><span data-stu-id="84ec3-401">Debug</span></span>](#debug-provider)
* [<span data-ttu-id="84ec3-402">EventSource</span><span class="sxs-lookup"><span data-stu-id="84ec3-402">EventSource</span></span>](#eventsource-provider)
* [<span data-ttu-id="84ec3-403">EventLog</span><span class="sxs-lookup"><span data-stu-id="84ec3-403">EventLog</span></span>](#windows-eventlog-provider)
* [<span data-ttu-id="84ec3-404">TraceSource</span><span class="sxs-lookup"><span data-stu-id="84ec3-404">TraceSource</span></span>](#tracesource-provider)

<span data-ttu-id="84ec3-405">[Azure에서 로깅](#logging-in-azure)에 대한 옵션은 이 문서의 뒷부분에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-405">Options for [Logging in Azure](#logging-in-azure) are covered later in this article.</span></span>

<span data-ttu-id="84ec3-406">stdout 로깅에 대한 자세한 내용은 <xref:host-and-deploy/iis/troubleshoot#aspnet-core-module-stdout-log> 및 <xref:host-and-deploy/azure-apps/troubleshoot#aspnet-core-module-stdout-log>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="84ec3-406">For information about stdout logging, see <xref:host-and-deploy/iis/troubleshoot#aspnet-core-module-stdout-log> and <xref:host-and-deploy/azure-apps/troubleshoot#aspnet-core-module-stdout-log>.</span></span>

### <a name="console-provider"></a><span data-ttu-id="84ec3-407">콘솔 공급자</span><span class="sxs-lookup"><span data-stu-id="84ec3-407">Console provider</span></span>

<span data-ttu-id="84ec3-408">[Microsoft.Extensions.Logging.Console](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Console) 공급자 패키지는 콘솔에 로그 출력을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-408">The [Microsoft.Extensions.Logging.Console](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Console) provider package sends log output to the console.</span></span> 

::: moniker range=">= aspnetcore-2.0"

```csharp
logging.AddConsole();
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
loggerFactory.AddConsole();
```

<span data-ttu-id="84ec3-409">[AddConsole 오버로드](xref:Microsoft.Extensions.Logging.ConsoleLoggerExtensions)를 사용하여 최소 로그 수준, 필터 함수 및 범위 지원 여부를 나타내는 부울을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-409">[AddConsole overloads](xref:Microsoft.Extensions.Logging.ConsoleLoggerExtensions) let you pass in a minimum log level, a filter function, and a boolean that indicates whether scopes are supported.</span></span> <span data-ttu-id="84ec3-410">다른 옵션으로는 `IConfiguration` 개체를 전달할 수 있으며, 이 개체는 범위 지원 및 로깅 수준을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-410">Another option is to pass in an `IConfiguration` object, which can specify scopes support and logging levels.</span></span>

<span data-ttu-id="84ec3-411">콘솔 공급자는 성능에 상당한 영향을 미치며 일반적으로 프로덕션 환경에서 사용하기에 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-411">The console provider has a significant impact on performance and is generally not appropriate for use in production.</span></span>

<span data-ttu-id="84ec3-412">Visual Studio에서 새 프로젝트를 만들면 `AddConsole` 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-412">When you create a new project in Visual Studio, the `AddConsole` method looks like this:</span></span>

```csharp
loggerFactory.AddConsole(Configuration.GetSection("Logging"));
```

<span data-ttu-id="84ec3-413">이 코드는 *appSettings.json* 파일의 `Logging` 섹션을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-413">This code refers to the `Logging` section of the *appSettings.json* file:</span></span>

[!code-json[](index/samples/1.x/TodoApiSample//appsettings.json)]

<span data-ttu-id="84ec3-414">[로그 필터링](#log-filtering) 섹션에서 설명했듯이, 제한 프레임워크를 표시한 설정은 경고에 기록되는 한편 앱이 디버그 수준에서 기록하는 것을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-414">The settings shown limit framework logs to warnings while allowing the app to log at debug level, as explained in the [Log filtering](#log-filtering) section.</span></span> <span data-ttu-id="84ec3-415">자세한 내용은 [구성](xref:fundamentals/configuration/index)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-415">For more information, see [Configuration](xref:fundamentals/configuration/index).</span></span>

::: moniker-end

<span data-ttu-id="84ec3-416">콘솔 로깅 출력을 보려면 프로젝트 폴더에서 명령 프롬프트를 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-416">To see console logging output, open a command prompt in the project folder and run the following command:</span></span>

```console
dotnet run
```

### <a name="debug-provider"></a><span data-ttu-id="84ec3-417">디버그 공급자</span><span class="sxs-lookup"><span data-stu-id="84ec3-417">Debug provider</span></span>

<span data-ttu-id="84ec3-418">[Microsoft.Extensions.Logging.Debug](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Debug) 공급자 패키지는 [System.Diagnostics.Debug](/dotnet/api/system.diagnostics.debug) 클래스(`Debug.WriteLine` 메서드 호출)를 사용하여 로그 출력을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-418">The [Microsoft.Extensions.Logging.Debug](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Debug) provider package writes log output by using the [System.Diagnostics.Debug](/dotnet/api/system.diagnostics.debug) class (`Debug.WriteLine` method calls).</span></span>

<span data-ttu-id="84ec3-419">Linux에서 이 공급자는 */var/log/message*에 로그를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-419">On Linux, this provider writes logs to */var/log/message*.</span></span>

::: moniker range=">= aspnetcore-2.0"

```csharp
logging.AddDebug();
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
loggerFactory.AddDebug();
```

<span data-ttu-id="84ec3-420">[AddDebug 오버로드](xref:Microsoft.Extensions.Logging.DebugLoggerFactoryExtensions)를 사용하여 최소 수준 로그 또는 필터 함수를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-420">[AddDebug overloads](xref:Microsoft.Extensions.Logging.DebugLoggerFactoryExtensions) let you pass in a minimum log level or a filter function.</span></span>

::: moniker-end

### <a name="eventsource-provider"></a><span data-ttu-id="84ec3-421">EventSource 공급자</span><span class="sxs-lookup"><span data-stu-id="84ec3-421">EventSource provider</span></span>

<span data-ttu-id="84ec3-422">ASP.NET Core 1.1.0 이상을 대상으로 하는 앱의 경우 [Microsoft.Extensions.Logging.EventSource](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventSource) 공급자 패키지가 이벤트 추적을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-422">For apps that target ASP.NET Core 1.1.0 or later, the [Microsoft.Extensions.Logging.EventSource](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventSource) provider package can implement event tracing.</span></span> <span data-ttu-id="84ec3-423">Windows에서는 [ETW](https://msdn.microsoft.com/library/windows/desktop/bb968803)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-423">On Windows, it uses [ETW](https://msdn.microsoft.com/library/windows/desktop/bb968803).</span></span> <span data-ttu-id="84ec3-424">플랫폼 간 공급자이지만 이벤트를 수집하지 않으며 Linux 또는 macOS용 도구를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-424">The provider is cross-platform, but there are no event collection and display tools yet for Linux or macOS.</span></span>

::: moniker range=">= aspnetcore-2.0"

```csharp
logging.AddEventSourceLogger();
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
loggerFactory.AddEventSourceLogger();
```

::: moniker-end

<span data-ttu-id="84ec3-425">로그를 수집하고 보는 좋은 방법은 [PerfView 유틸리티](https://github.com/Microsoft/perfview)를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-425">A good way to collect and view logs is to use the [PerfView utility](https://github.com/Microsoft/perfview).</span></span> <span data-ttu-id="84ec3-426">ETW 로그를 보는 다른 도구가 있지만, PerfView는 ASP.NET에서 내보내는 ETW 이벤트를 처리하기에 가장 좋은 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-426">There are other tools for viewing ETW logs, but PerfView provides the best experience for working with the ETW events emitted by ASP.NET.</span></span>

<span data-ttu-id="84ec3-427">이 공급자가 기록한 이벤트를 수집하도록 PerfView를 구성하려면 **추가 공급자** 목록에 `*Microsoft-Extensions-Logging` 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-427">To configure PerfView for collecting events logged by this provider, add the string `*Microsoft-Extensions-Logging` to the **Additional Providers** list.</span></span> <span data-ttu-id="84ec3-428">(문자열의 시작 부분에 별표를 누락하지 마세요.)</span><span class="sxs-lookup"><span data-stu-id="84ec3-428">(Don't miss the asterisk at the start of the string.)</span></span>

![Perfview 추가 공급자](index/_static/perfview-additional-providers.png)

### <a name="windows-eventlog-provider"></a><span data-ttu-id="84ec3-430">Windows EventLog 공급자</span><span class="sxs-lookup"><span data-stu-id="84ec3-430">Windows EventLog provider</span></span>

<span data-ttu-id="84ec3-431">[Microsoft.Extensions.Logging.EventLog](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventLog) 공급자 패키지는 Windows 이벤트 로그에 로그 출력을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-431">The [Microsoft.Extensions.Logging.EventLog](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventLog) provider package sends log output to the Windows Event Log.</span></span>

::: moniker range=">= aspnetcore-2.0"

```csharp
logging.AddEventLog();
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
loggerFactory.AddEventLog();
```

<span data-ttu-id="84ec3-432">[AddEventLog 오버로드](xref:Microsoft.Extensions.Logging.EventLoggerFactoryExtensions)를 사용하여 `EventLogSettings` 또는 최소 로그 수준을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-432">[AddEventLog overloads](xref:Microsoft.Extensions.Logging.EventLoggerFactoryExtensions) let you pass in `EventLogSettings` or a minimum log level.</span></span>

::: moniker-end

### <a name="tracesource-provider"></a><span data-ttu-id="84ec3-433">TraceSource 공급자</span><span class="sxs-lookup"><span data-stu-id="84ec3-433">TraceSource provider</span></span>

<span data-ttu-id="84ec3-434">[Microsoft.Extensions.Logging.TraceSource](https://www.nuget.org/packages/Microsoft.Extensions.Logging.TraceSource) 공급자 패키지는 <xref:System.Diagnostics.TraceSource> 라이브러리 및 공급자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-434">The [Microsoft.Extensions.Logging.TraceSource](https://www.nuget.org/packages/Microsoft.Extensions.Logging.TraceSource) provider package uses the <xref:System.Diagnostics.TraceSource> libraries and providers.</span></span>

::: moniker range=">= aspnetcore-2.0"

```csharp
logging.AddTraceSource(sourceSwitchName);
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
loggerFactory.AddTraceSource(sourceSwitchName);
```

::: moniker-end

<span data-ttu-id="84ec3-435">[AddTraceSource 오버로드](xref:Microsoft.Extensions.Logging.TraceSourceFactoryExtensions)를 사용하여 원본 스위치 및 추적 수신기를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-435">[AddTraceSource overloads](xref:Microsoft.Extensions.Logging.TraceSourceFactoryExtensions) let you pass in a source switch and a trace listener.</span></span>

<span data-ttu-id="84ec3-436">이 공급자를 사용하려면 앱이 .NET Framework(.NET Core가 아닌)에서 실행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-436">To use this provider, an app has to run on the .NET Framework (rather than .NET Core).</span></span> <span data-ttu-id="84ec3-437">공급자는 샘플 앱에 사용된 <xref:System.Diagnostics.TextWriterTraceListener>와 같은 다양한 [수신기](/dotnet/framework/debug-trace-profile/trace-listeners)로 메시지를 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-437">The provider can route messages to a variety of [listeners](/dotnet/framework/debug-trace-profile/trace-listeners), such as the <xref:System.Diagnostics.TextWriterTraceListener> used in the sample app.</span></span>

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="84ec3-438">다음은 `Warning` 이상 메시지를 콘솔 창에 기록하는 `TraceSource` 공급자를 구성하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-438">The following example configures a `TraceSource` provider that logs `Warning` and higher messages to the console window.</span></span>

[!code-csharp[](index/samples/1.x/TodoApiSample/Startup.cs?name=snippet_TraceSource&highlight=9-12)]

::: moniker-end

## <a name="logging-in-azure"></a><span data-ttu-id="84ec3-439">Azure에서 로깅</span><span class="sxs-lookup"><span data-stu-id="84ec3-439">Logging in Azure</span></span>

<span data-ttu-id="84ec3-440">Azure에서 로깅에 대한 자세한 내용은 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="84ec3-440">For information about logging in Azure, see the following sections:</span></span>

* [<span data-ttu-id="84ec3-441">Azure App Service 공급자</span><span class="sxs-lookup"><span data-stu-id="84ec3-441">Azure App Service provider</span></span>](#azure-app-service-provider)
* [<span data-ttu-id="84ec3-442">Azure 로그 스트리밍</span><span class="sxs-lookup"><span data-stu-id="84ec3-442">Azure log streaming</span></span>](#azure-log-streaming)

::: moniker range=">= aspnetcore-1.1"

* [<span data-ttu-id="84ec3-443">Azure Application Insights 추적 로깅</span><span class="sxs-lookup"><span data-stu-id="84ec3-443">Azure Application Insights trace logging</span></span>](#azure-application-insights-trace-logging)

::: moniker-end

### <a name="azure-app-service-provider"></a><span data-ttu-id="84ec3-444">Azure App Service 공급자</span><span class="sxs-lookup"><span data-stu-id="84ec3-444">Azure App Service provider</span></span>

<span data-ttu-id="84ec3-445">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices) 공급자 패키지는 Azure App Service 앱의 파일 시스템과 Azure Storage 계정의 [BLOB 저장소](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/#what-is-blob-storage)에 텍스트 파일을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-445">The [Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices) provider package writes logs to text files in an Azure App Service app's file system and to [blob storage](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/#what-is-blob-storage) in an Azure Storage account.</span></span> <span data-ttu-id="84ec3-446">공급자 패키지는 .NET Core 1.1 이상을 대상으로 하는 앱에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-446">The provider package is available for apps targeting .NET Core 1.1 or later.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="84ec3-447">.NET Core를 대상으로 하는 경우 다음 사항에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-447">If targeting .NET Core, note the following points:</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

* <span data-ttu-id="84ec3-448">공급자 패키지는 ASP.NET Core [Microsoft.AspNetCore.All 메타패키지](xref:fundamentals/metapackage)에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-448">The provider package is included in the ASP.NET Core [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage).</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

* <span data-ttu-id="84ec3-449">공급자 패키지는 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)에 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-449">The provider package isn't included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span> <span data-ttu-id="84ec3-450">공급자를 사용하려면 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-450">To use the provider, install the package.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

* <span data-ttu-id="84ec3-451">명시적으로 <xref:Microsoft.Extensions.Logging.AzureAppServicesLoggerFactoryExtensions.AddAzureWebAppDiagnostics*>를 호출하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="84ec3-451">Don't explicitly call <xref:Microsoft.Extensions.Logging.AzureAppServicesLoggerFactoryExtensions.AddAzureWebAppDiagnostics*>.</span></span> <span data-ttu-id="84ec3-452">Azure App Service에 앱을 배포하면 공급자가 자동으로 앱에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-452">The provider is automatically made available to the app when the app is deployed to Azure App Service.</span></span>

<span data-ttu-id="84ec3-453">.NET Framework를 대상으로 지정하거나 `Microsoft.AspNetCore.App` 메타패키지를 참조하는 경우 패키지 공급자를 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-453">If targeting .NET Framework or referencing the `Microsoft.AspNetCore.App` metapackage, add the provider package to the project.</span></span> <span data-ttu-id="84ec3-454"><xref:Microsoft.Extensions.Logging.ILoggerFactory> 인스턴스에서 `AddAzureWebAppDiagnostics` 호출:</span><span class="sxs-lookup"><span data-stu-id="84ec3-454">Invoke `AddAzureWebAppDiagnostics` on an <xref:Microsoft.Extensions.Logging.ILoggerFactory> instance:</span></span>

```csharp
logging.AddAzureWebAppDiagnostics();
```

::: moniker-end

::: moniker range="= aspnetcore-1.1"

```csharp
loggerFactory.AddAzureWebAppDiagnostics();
```

::: moniker-end

::: moniker range=">= aspnetcore-1.1"

<span data-ttu-id="84ec3-455"><xref:Microsoft.Extensions.Logging.AzureAppServicesLoggerFactoryExtensions.AddAzureWebAppDiagnostics*> 오버로드로 <xref:Microsoft.Extensions.Logging.AzureAppServices.AzureAppServicesDiagnosticsSettings>를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-455">An <xref:Microsoft.Extensions.Logging.AzureAppServicesLoggerFactoryExtensions.AddAzureWebAppDiagnostics*> overload lets you pass in <xref:Microsoft.Extensions.Logging.AzureAppServices.AzureAppServicesDiagnosticsSettings>.</span></span> <span data-ttu-id="84ec3-456">설정 개체는 로깅 출력 템플릿, BLOB 이름, 파일 크기 제한과 같은 기본 설정을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-456">The settings object can override default settings, such as the logging output template, blob name, and file size limit.</span></span> <span data-ttu-id="84ec3-457">(*출력 템플릿*은 `ILogger` 메서드를 호출과 함께 제공되는 것 이외에 모든 로그에 적용되는 메시지 템플릿입니다.)</span><span class="sxs-lookup"><span data-stu-id="84ec3-457">(*Output template* is a message template that's applied to all logs in addition to what's provided with an `ILogger` method call.)</span></span>

<span data-ttu-id="84ec3-458">App Service 앱에 배포할 때 응용 프로그램은 Azure Portal **App Service** 페이지의 [진단 로그](/azure/app-service/web-sites-enable-diagnostic-log/#enablediag) 섹션에 있는 설정을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-458">When you deploy to an App Service app, the application honors the settings in the [Diagnostic Logs](/azure/app-service/web-sites-enable-diagnostic-log/#enablediag) section of the **App Service** page of the Azure portal.</span></span> <span data-ttu-id="84ec3-459">이러한 설정을 업데이트하는 경우 앱을 다시 시작하거나 재배포하지 않아도 변경 내용은 즉시 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-459">When these settings are updated, the changes take effect immediately without requiring a restart or redeployment of the app.</span></span>

![Azure 로깅 설정](index/_static/azure-logging-settings.png)

<span data-ttu-id="84ec3-461">로그 파일의 기본 위치는 *D:\\home\\LogFiles\\Application* 폴더이며, 기본 파일 이름은 *diagnostics-yyyymmdd.txt*입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-461">The default location for log files is in the *D:\\home\\LogFiles\\Application* folder, and the default file name is *diagnostics-yyyymmdd.txt*.</span></span> <span data-ttu-id="84ec3-462">기본 파일 크기 제한은 10MB이고, 보존되는 기본 최대 파일 수는 2입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-462">The default file size limit is 10 MB, and the default maximum number of files retained is 2.</span></span> <span data-ttu-id="84ec3-463">기본 BLOB 이름은 *{app-name}{timestamp}/yyyy/mm/dd/hh/{guid}-applicationLog.txt*입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-463">The default blob name is *{app-name}{timestamp}/yyyy/mm/dd/hh/{guid}-applicationLog.txt*.</span></span> <span data-ttu-id="84ec3-464">기본 동작에 대한 자세한 내용은 <xref:Microsoft.Extensions.Logging.AzureAppServices.AzureAppServicesDiagnosticsSettings>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="84ec3-464">For more information about default behavior, see <xref:Microsoft.Extensions.Logging.AzureAppServices.AzureAppServicesDiagnosticsSettings>.</span></span>

<span data-ttu-id="84ec3-465">공급자는 프로젝트가 Azure 환경에서 실행되는 경우에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-465">The provider only works when the project runs in the Azure environment.</span></span> <span data-ttu-id="84ec3-466">프로젝트를 로컬로 실행하는 경우에는 아무 영향도 없습니다&mdash;Blob에 대한 로컬 파일 또는 로컬 개발 저장소에 기록하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-466">It has no effect when the project is run locally&mdash;it doesn't write to local files or local development storage for blobs.</span></span>

::: moniker-end

### <a name="azure-log-streaming"></a><span data-ttu-id="84ec3-467">Azure 로그 스트리밍</span><span class="sxs-lookup"><span data-stu-id="84ec3-467">Azure log streaming</span></span>

<span data-ttu-id="84ec3-468">Azure 로그 스트리밍을 통해 로그 작업을 실시간으로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-468">Azure log streaming lets you view log activity in real time from:</span></span>

* <span data-ttu-id="84ec3-469">앱 서버</span><span class="sxs-lookup"><span data-stu-id="84ec3-469">The app server</span></span>
* <span data-ttu-id="84ec3-470">웹 서버</span><span class="sxs-lookup"><span data-stu-id="84ec3-470">The web server</span></span>
* <span data-ttu-id="84ec3-471">실패한 요청 추적</span><span class="sxs-lookup"><span data-stu-id="84ec3-471">Failed request tracing</span></span>

<span data-ttu-id="84ec3-472">Azure 로그 스트리밍을 구성하려면:</span><span class="sxs-lookup"><span data-stu-id="84ec3-472">To configure Azure log streaming:</span></span>

* <span data-ttu-id="84ec3-473">앱의 포털 페이지에서 **진단 로그** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-473">Navigate to the **Diagnostics Logs** page from your app's portal page.</span></span>
* <span data-ttu-id="84ec3-474">**응용 프로그램 로깅(파일 시스템)** 을 **On**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-474">Set **Application Logging (Filesystem)** to **On**.</span></span>

![Azure Portal 진단 로그 페이지](index/_static/azure-diagnostic-logs.png)

<span data-ttu-id="84ec3-476">**로그 스트리밍** 페이지로 이동하여 앱 메시지를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-476">Navigate to the **Log Streaming** page to view app messages.</span></span> <span data-ttu-id="84ec3-477">앱이 `ILogger` 인터페이스를 통해 기록한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-477">They're logged by the app through the `ILogger` interface.</span></span>

![Azure Portal 응용 프로그램 로그 스트리밍](index/_static/azure-log-streaming.png)

::: moniker range=">= aspnetcore-1.1"

### <a name="azure-application-insights-trace-logging"></a><span data-ttu-id="84ec3-479">Azure Application Insights 추적 로깅</span><span class="sxs-lookup"><span data-stu-id="84ec3-479">Azure Application Insights trace logging</span></span>

<span data-ttu-id="84ec3-480">Application Insights SDK는 ASP.NET Core 로깅 인프라에 생성된 로그를 수집하고 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-480">The Application Insights SDK can collect and report logs generated by the ASP.NET Core logging infrastructure.</span></span> <span data-ttu-id="84ec3-481">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="84ec3-481">For more information, see the following resources:</span></span>

* [<span data-ttu-id="84ec3-482">Application Insights 개요</span><span class="sxs-lookup"><span data-stu-id="84ec3-482">Application Insights overview</span></span>](/azure/application-insights/app-insights-overview)
* [<span data-ttu-id="84ec3-483">ASP.NET Core용 Application Insights</span><span class="sxs-lookup"><span data-stu-id="84ec3-483">Application Insights for ASP.NET Core</span></span>](/azure/application-insights/app-insights-asp-net-core)
* <span data-ttu-id="84ec3-484">[Microsoft/ApplicationInsights-aspnetcore Wiki: Logging](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Logging).</span><span class="sxs-lookup"><span data-stu-id="84ec3-484">[Microsoft/ApplicationInsights-aspnetcore Wiki: Logging](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Logging).</span></span>

::: moniker-end

## <a name="third-party-logging-providers"></a><span data-ttu-id="84ec3-485">타사 로깅 공급자</span><span class="sxs-lookup"><span data-stu-id="84ec3-485">Third-party logging providers</span></span>

<span data-ttu-id="84ec3-486">ASP.NET Core와 호환되는 타사 로깅 프레임워크는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-486">Third-party logging frameworks that work with ASP.NET Core:</span></span>

* <span data-ttu-id="84ec3-487">[elmah.io](https://elmah.io/)([GitHub 리포지토리](https://github.com/elmahio/Elmah.Io.Extensions.Logging))</span><span class="sxs-lookup"><span data-stu-id="84ec3-487">[elmah.io](https://elmah.io/) ([GitHub repo](https://github.com/elmahio/Elmah.Io.Extensions.Logging))</span></span>
* <span data-ttu-id="84ec3-488">[Gelf](http://docs.graylog.org/en/2.3/pages/gelf.html) ([GitHub 리포지토리](https://github.com/mattwcole/gelf-extensions-logging))</span><span class="sxs-lookup"><span data-stu-id="84ec3-488">[Gelf](http://docs.graylog.org/en/2.3/pages/gelf.html) ([GitHub repo](https://github.com/mattwcole/gelf-extensions-logging))</span></span>
* <span data-ttu-id="84ec3-489">[JSNLog](http://jsnlog.com/)([GitHub 리포지토리](https://github.com/mperdeck/jsnlog))</span><span class="sxs-lookup"><span data-stu-id="84ec3-489">[JSNLog](http://jsnlog.com/) ([GitHub repo](https://github.com/mperdeck/jsnlog))</span></span>
* <span data-ttu-id="84ec3-490">[KissLog.net](https://kisslog.net/)([GitHub 리포지토리](https://github.com/catalingavan/KissLog-net))</span><span class="sxs-lookup"><span data-stu-id="84ec3-490">[KissLog.net](https://kisslog.net/) ([GitHub repo](https://github.com/catalingavan/KissLog-net))</span></span>
* <span data-ttu-id="84ec3-491">[Loggr](http://loggr.net/)([GitHub 리포지토리](https://github.com/imobile3/Loggr.Extensions.Logging))</span><span class="sxs-lookup"><span data-stu-id="84ec3-491">[Loggr](http://loggr.net/) ([GitHub repo](https://github.com/imobile3/Loggr.Extensions.Logging))</span></span>
* <span data-ttu-id="84ec3-492">[NLog](http://nlog-project.org/)([GitHub 리포지토리](https://github.com/NLog/NLog.Extensions.Logging))</span><span class="sxs-lookup"><span data-stu-id="84ec3-492">[NLog](http://nlog-project.org/) ([GitHub repo](https://github.com/NLog/NLog.Extensions.Logging))</span></span>
* <span data-ttu-id="84ec3-493">[Sentry](https://sentry.io/welcome/) ([GitHub repo](https://github.com/getsentry/sentry-dotnet))</span><span class="sxs-lookup"><span data-stu-id="84ec3-493">[Sentry](https://sentry.io/welcome/) ([GitHub repo](https://github.com/getsentry/sentry-dotnet))</span></span>
* <span data-ttu-id="84ec3-494">[Serilog](https://serilog.net/)([GitHub 리포지토리](https://github.com/serilog/serilog-extensions-logging))</span><span class="sxs-lookup"><span data-stu-id="84ec3-494">[Serilog](https://serilog.net/) ([GitHub repo](https://github.com/serilog/serilog-extensions-logging))</span></span>
* <span data-ttu-id="84ec3-495">[Stackdriver](https://cloud.google.com/dotnet/docs/stackdriver#logging)([Github 리포지토리](https://github.com/googleapis/google-cloud-dotnet))</span><span class="sxs-lookup"><span data-stu-id="84ec3-495">[Stackdriver](https://cloud.google.com/dotnet/docs/stackdriver#logging) ([Github repo](https://github.com/googleapis/google-cloud-dotnet))</span></span>

<span data-ttu-id="84ec3-496">일부 타사 프레임워크는 [구조적 로깅이라고 하는 의미 체계 로깅](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging)을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-496">Some third-party frameworks can perform [semantic logging, also known as structured logging](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging).</span></span>

<span data-ttu-id="84ec3-497">타사 프레임워크를 사용하는 방법은 다음과 같이 기본 공급자 중 하나를 사용하는 방법과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-497">Using a third-party framework is similar to using one of the built-in providers:</span></span>

1. <span data-ttu-id="84ec3-498">프로젝트에 NuGet 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-498">Add a NuGet package to your project.</span></span>
1. <span data-ttu-id="84ec3-499">`ILoggerFactory`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-499">Call an `ILoggerFactory`.</span></span>

<span data-ttu-id="84ec3-500">자세한 내용은 각 공급자의 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="84ec3-500">For more information, see each provider's documentation.</span></span> <span data-ttu-id="84ec3-501">타사 로깅 공급자는 Microsoft에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84ec3-501">Third-party logging providers aren't supported by Microsoft.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="84ec3-502">추가 자료</span><span class="sxs-lookup"><span data-stu-id="84ec3-502">Additional resources</span></span>

* <xref:fundamentals/logging/loggermessage>
