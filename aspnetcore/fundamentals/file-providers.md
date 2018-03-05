---
title: "ASP.NET Core의 파일 공급자"
author: ardalis
description: "ASP.NET Core에서 파일 공급자를 사용하여 파일 시스템 액세스를 추상화하는 방법을 알아봅니다."
manager: wpickett
ms.author: riande
ms.date: 02/14/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/file-providers
ms.openlocfilehash: 06197f967e111d75531e9c3bcbcbdb971cb9f99b
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="file-providers-in-aspnet-core"></a><span data-ttu-id="638b4-103">ASP.NET Core의 파일 공급자</span><span class="sxs-lookup"><span data-stu-id="638b4-103">File Providers in ASP.NET Core</span></span>

<span data-ttu-id="638b4-104">작성자: [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="638b4-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="638b4-105">ASP.NET Core에서 파일 공급자를 사용하여 파일 시스템 액세스를 추상화합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-105">ASP.NET Core abstracts file system access through the use of File Providers.</span></span>

<span data-ttu-id="638b4-106">[예제 코드 보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/file-providers/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="638b4-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/file-providers/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="file-provider-abstractions"></a><span data-ttu-id="638b4-107">파일 공급자 추상화</span><span class="sxs-lookup"><span data-stu-id="638b4-107">File Provider abstractions</span></span>

<span data-ttu-id="638b4-108">파일 공급자는 파일 시스템에 대한 추상화로.</span><span class="sxs-lookup"><span data-stu-id="638b4-108">File Providers are an abstraction over file systems.</span></span> <span data-ttu-id="638b4-109">기본 인터페이스는 `IFileProvider`입니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-109">The main interface is `IFileProvider`.</span></span> <span data-ttu-id="638b4-110">`IFileProvider`는 파일 정보(`IFileInfo`)나 디렉터리 정보(`IDirectoryContents`)를 가져오고, 변경 알림을 설정(`IChangeToken` 을 사용) 하는 메서드를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-110">`IFileProvider` exposes methods to get file information (`IFileInfo`), directory information (`IDirectoryContents`), and to set up change notifications (using an `IChangeToken`).</span></span>

<span data-ttu-id="638b4-111">`IFileInfo`는 개별 파일 또는 디렉터리에 대한 메서드 및 속성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-111">`IFileInfo` provides methods and properties about individual files or directories.</span></span> <span data-ttu-id="638b4-112">두 개의 부울 속성, `Exists` 및 `IsDirectory`와 파일의 `Name`, `Length`(바이트) 및 `LastModified` 날짜를 설명하는 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-112">It has two boolean properties, `Exists` and `IsDirectory`, as well as properties describing the file's `Name`, `Length` (in bytes), and `LastModified` date.</span></span> <span data-ttu-id="638b4-113">해당 `CreateReadStream` 메서드를 사용하여 파일에서 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-113">You can read from the file using its `CreateReadStream` method.</span></span>

## <a name="file-provider-implementations"></a><span data-ttu-id="638b4-114">파일 공급자 구현</span><span class="sxs-lookup"><span data-stu-id="638b4-114">File Provider implementations</span></span>

<span data-ttu-id="638b4-115">`IFileProvider`의 세 가지 구현, 물리적, 포함 및 복합을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-115">Three implementations of `IFileProvider` are available: Physical, Embedded, and Composite.</span></span> <span data-ttu-id="638b4-116">물리적 공급자는 실제 시스템의 파일에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-116">The physical provider is used to access the actual system's files.</span></span> <span data-ttu-id="638b4-117">포함된 공급자는 어셈블리에 포함된 파일에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-117">The embedded provider is used to access files embedded in assemblies.</span></span> <span data-ttu-id="638b4-118">복합 공급자는 하나 이상의 다른 공급자에서 파일 및 디렉터리에 대한 결합된 액세스를 제공하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-118">The composite provider is used to provide combined access to files and directories from one or more other providers.</span></span>

### <a name="physicalfileprovider"></a><span data-ttu-id="638b4-119">PhysicalFileProvider</span><span class="sxs-lookup"><span data-stu-id="638b4-119">PhysicalFileProvider</span></span>

<span data-ttu-id="638b4-120">`PhysicalFileProvider`는 실제 파일 시스템에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-120">The `PhysicalFileProvider` provides access to the physical file system.</span></span> <span data-ttu-id="638b4-121">모든 경로를 디렉터리 및 해당 자식으로 범위를 지정하여 `System.IO.File` 형식(물리적 공급자용)을 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-121">It wraps the `System.IO.File` type (for the physical provider), scoping all paths to a directory and its children.</span></span> <span data-ttu-id="638b4-122">이 범위 지정은 이 경계 외부의 파일 시스템에 대한 액세스를 방지하여 특정 디렉터리 및 해당 자식에 대한 액세스를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-122">This scoping limits access to a certain directory and its children, preventing access to the file system outside of this boundary.</span></span> <span data-ttu-id="638b4-123">이 공급자를 인스턴스화할 때 이 공급자에 대해 만들어진 모든 요청에 대한 기본 경로로 제공하는(및 이 경로 외부의 액세스 제한) 디렉터리 경로와 함께 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-123">When instantiating this provider, you must provide it with a directory path, which serves as the base path for all requests made to this provider (and which restricts access outside of this path).</span></span> <span data-ttu-id="638b4-124">ASP.NET Core 앱에서 `PhysicalFileProvider` 공급자를 직접 인스턴스화하거나 [종속성 주입](dependency-injection.md)을 통해 컨트롤러 또는 서비스의 생성자에서 `IFileProvider`를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-124">In an ASP.NET Core app, you can instantiate a `PhysicalFileProvider` provider directly, or you can request an `IFileProvider` in a Controller or service's constructor through [dependency injection](dependency-injection.md).</span></span> <span data-ttu-id="638b4-125">후자의 방법은 일반적으로 보다 유연하고 테스트 가능한 솔루션을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-125">The latter approach will typically yield a more flexible and testable solution.</span></span>

<span data-ttu-id="638b4-126">아래 샘플에서는 `PhysicalFileProvider`를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-126">The sample below shows how to create a `PhysicalFileProvider`.</span></span>


```csharp
IFileProvider provider = new PhysicalFileProvider(applicationRoot);
IDirectoryContents contents = provider.GetDirectoryContents(""); // the applicationRoot contents
IFileInfo fileInfo = provider.GetFileInfo("wwwroot/js/site.js"); // a file under applicationRoot
```

<span data-ttu-id="638b4-127">해당 디렉터리 내용을 반복하거나 하위 경로를 제공하여 특정 파일의 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-127">You can iterate through its directory contents or get a specific file's information by providing a subpath.</span></span>

<span data-ttu-id="638b4-128">컨트롤러에서 공급자를 요청하려면 컨트롤러의 생성자에서 지정하고 로컬 필드에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-128">To request a provider from a controller, specify it in the controller's constructor and assign it to a local field.</span></span> <span data-ttu-id="638b4-129">작업 방법 중에서 로컬 인스턴스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-129">Use the local instance from your action methods:</span></span>

[!code-csharp[Main](file-providers/sample/src/FileProviderSample/Controllers/HomeController.cs?highlight=5,7,12&range=6-19)]

<span data-ttu-id="638b4-130">그런 다음, 앱의 `Startup` 클래스에서 공급자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-130">Then, create the provider in the app's `Startup` class:</span></span>

[!code-csharp[Main](file-providers/sample/src/FileProviderSample/Startup.cs?highlight=35,40&range=1-43)]

<span data-ttu-id="638b4-131">*Index.cshtml* 보기에서 제공된 `IDirectoryContents`를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-131">In the *Index.cshtml* view, iterate through the `IDirectoryContents` provided:</span></span>

[!code-html[Main](file-providers/sample/src/FileProviderSample/Views/Home/Index.cshtml?highlight=2,7,9,11,15)]

<span data-ttu-id="638b4-132">결과:</span><span class="sxs-lookup"><span data-stu-id="638b4-132">The result:</span></span>

![물리적 파일 및 폴더를 나열하는 파일 공급자 샘플 응용 프로그램](file-providers/_static/physical-directory-listing.png)

### <a name="embeddedfileprovider"></a><span data-ttu-id="638b4-134">EmbeddedFileProvider</span><span class="sxs-lookup"><span data-stu-id="638b4-134">EmbeddedFileProvider</span></span>

<span data-ttu-id="638b4-135">`EmbeddedFileProvider`는 어셈블리에 포함된 파일에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-135">The `EmbeddedFileProvider` is used to access files embedded in assemblies.</span></span> <span data-ttu-id="638b4-136">.NET Core에서 *.csproj* 파일의 `<EmbeddedResource>` 요소를 사용하여 어셈블리에 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-136">In .NET Core, you embed files in an assembly with the `<EmbeddedResource>` element in the *.csproj* file:</span></span>

[!code-json[Main](file-providers/sample/src/FileProviderSample/FileProviderSample.csproj?range=13-18)]

<span data-ttu-id="638b4-137">파일을 어셈블리에 포함하도록 지정할 때 [와일드카드 사용 패턴](#globbing-patterns)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-137">You can use [globbing patterns](#globbing-patterns) when specifying files to embed in the assembly.</span></span> <span data-ttu-id="638b4-138">하나 이상의 파일에 맞게 이러한 패턴을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-138">These patterns can be used to match one or more files.</span></span>

> [!NOTE]
> <span data-ttu-id="638b4-139">실제로 해당 어셈블리의 프로젝트에 모든 .js 파일을 포함하려고 할 가능성은 낮습니다. 위의 샘플은 데모 목적입니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-139">It's unlikely you would ever want to actually embed every .js file in your project in its assembly; the above sample is for demo purposes only.</span></span>

<span data-ttu-id="638b4-140">`EmbeddedFileProvider`를 만들 때 읽는 어셈블리를 해당 생성자에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-140">When creating an `EmbeddedFileProvider`, pass the assembly it will read to its constructor.</span></span>

```csharp
var embeddedProvider = new EmbeddedFileProvider(Assembly.GetEntryAssembly());
```

<span data-ttu-id="638b4-141">위의 코드 조각은 현재 실행 중인 어셈블리에 대한 액세스로 `EmbeddedFileProvider`를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-141">The snippet above demonstrates how to create an `EmbeddedFileProvider` with access to the currently executing assembly.</span></span>

<span data-ttu-id="638b4-142">`EmbeddedFileProvider`를 사용하도록 샘플 앱을 업데이트하면 다음 출력과 같은 결과가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-142">Updating the sample app to use an `EmbeddedFileProvider` results in the following output:</span></span>

![포함된 파일을 나열하는 파일 공급자 샘플 응용 프로그램](file-providers/_static/embedded-directory-listing.png)

> [!NOTE]
> <span data-ttu-id="638b4-144">포함된 리소스는 디렉터리를 공개하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-144">Embedded resources don't expose directories.</span></span> <span data-ttu-id="638b4-145">대신, 리소스에 대한 경로(해당 네임스페이스를 통해)는 `.` 구분 기호를 사용하여 해당 파일 이름에서 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-145">Rather, the path to the resource (via its namespace) is embedded in its filename using `.` separators.</span></span>

> [!TIP]
> <span data-ttu-id="638b4-146">`EmbeddedFileProvider` 생성자는 선택적 `baseNamespace` 매개 변수를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-146">The `EmbeddedFileProvider` constructor accepts an optional `baseNamespace` parameter.</span></span> <span data-ttu-id="638b4-147">이를 지정하면 `GetDirectoryContents`에 대한 호출을 제공된 네임스페이스 아래의 해당 리소스로 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-147">Specifying this will scope calls to `GetDirectoryContents` to those resources under the provided namespace.</span></span>

### <a name="compositefileprovider"></a><span data-ttu-id="638b4-148">CompositeFileProvider</span><span class="sxs-lookup"><span data-stu-id="638b4-148">CompositeFileProvider</span></span>

<span data-ttu-id="638b4-149">`CompositeFileProvider`는 여러 공급자에서 파일을 사용하기 위한 단일 인터페이스를 노출하여 `IFileProvider` 인스턴스를 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-149">The `CompositeFileProvider` combines `IFileProvider` instances, exposing a single interface for working with files from multiple providers.</span></span> <span data-ttu-id="638b4-150">`CompositeFileProvider`를 만들 때 하나 이상의 `IFileProvider` 인스턴스를 해당 생성자에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-150">When creating the `CompositeFileProvider`, you pass one or more `IFileProvider` instances to its constructor:</span></span>

[!code-csharp[Main](file-providers/sample/src/FileProviderSample/Startup.cs?highlight=3&range=35-37)]

<span data-ttu-id="638b4-151">이전에 구성된 물리적 및 포함된 공급자 모두를 포함하는 `CompositeFileProvider`를 사용하도록 샘플 앱을 업데이트하면 다음 출력과 같은 결과가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-151">Updating the sample app to use a `CompositeFileProvider` that includes both the physical and embedded providers configured previously, results in the following output:</span></span>

![물리적 파일 및 폴더와 포함된 파일을 나열하는 파일 공급자 샘플 응용 프로그램](file-providers/_static/composite-directory-listing.png)

## <a name="watching-for-changes"></a><span data-ttu-id="638b4-153">변경 내용 감시</span><span class="sxs-lookup"><span data-stu-id="638b4-153">Watching for changes</span></span>

<span data-ttu-id="638b4-154">`IFileProvider` `Watch` 메서드는 하나 이상의 파일 또는 디렉터리의 변경 내용을 감시하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-154">The `IFileProvider` `Watch` method provides a way to watch one or more files or directories for changes.</span></span> <span data-ttu-id="638b4-155">이 메서드는 [와일드카드 사용 패턴](#globbing-patterns)을 사용하여 여러 파일을 지정할 수 있는 경로 문자열을 허용하고, `IChangeToken`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-155">This method accepts a path string, which can use [globbing patterns](#globbing-patterns) to specify multiple files, and returns an `IChangeToken`.</span></span> <span data-ttu-id="638b4-156">이 토큰은 조사될 수 있는 `HasChanged` 속성 및 지정된 경로 문자열에 변경 내용이 발견될 때 호출되는 `RegisterChangeCallback` 메서드를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-156">This token exposes a `HasChanged` property that can be inspected, and a `RegisterChangeCallback` method that's called when changes are detected to the specified path string.</span></span> <span data-ttu-id="638b4-157">각 변경 토큰만 단일 변경에 대한 응답으로 연결된 해당 콜백을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-157">Note that each change token only calls its associated callback in response to a single change.</span></span> <span data-ttu-id="638b4-158">지속적인 모니터링을 활성화하기 위해 아래와 같이 `TaskCompletionSource`를 사용하거나 변경에 대한 응답으로 `IChangeToken` 인스턴스를 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-158">To enable constant monitoring, you can use a `TaskCompletionSource` as shown below, or re-create `IChangeToken` instances in response to changes.</span></span>

<span data-ttu-id="638b4-159">이 문서 샘플에서 콘솔 응용 프로그램은 텍스트 파일이 수정될 때마다 메시지를 표시하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-159">In this article's sample, a console application is configured to display a message whenever a text file is modified:</span></span>

[!code-csharp[Main](file-providers/sample/src/WatchConsole/Program.cs?name=snippet1&highlight=1-2,16,19-20)]

<span data-ttu-id="638b4-160">파일을 여러 번 저장한 후 결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-160">The result, after saving the file several times:</span></span>

![dotnet 실행을 실행한 후 명령 창은 변경 내용에 대한 quotes.txt 파일을 모니터링하는 응용 프로그램과 파일이 5번 변경된 것을 보여 줍니다.](file-providers/_static/watch-console.png)

> [!NOTE]
> <span data-ttu-id="638b4-162">Docker 컨테이너 및 네트워크 공유와 같은 일부 파일 시스템은 안정적으로 변경 알림을 보내지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-162">Some file systems, such as Docker containers and network shares, may not reliably send change notifications.</span></span> <span data-ttu-id="638b4-163">`DOTNET_USE_POLLINGFILEWATCHER` 환경 변수를 `1` 또는 `true`로 설정하여 4초마다 변경 내용에 대한 파일 시스템을 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-163">Set the `DOTNET_USE_POLLINGFILEWATCHER` environment variable to `1` or `true` to poll the file system for changes every 4 seconds.</span></span>

## <a name="globbing-patterns"></a><span data-ttu-id="638b4-164">와일드카드 사용 패턴</span><span class="sxs-lookup"><span data-stu-id="638b4-164">Globbing patterns</span></span>

<span data-ttu-id="638b4-165">파일 시스템 경로는 *와일드카드 사용 패턴*이라는 와일드카드 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-165">File system paths use wildcard patterns called *globbing patterns*.</span></span> <span data-ttu-id="638b4-166">이러한 단순한 패턴은 파일의 그룹을 지정하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-166">These simple patterns can be used to specify groups of files.</span></span> <span data-ttu-id="638b4-167">두 개의 와일드카드 문자는 `*` 및 `**`입니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-167">The two wildcard characters are `*` and `**`.</span></span>

**`*`**

   <span data-ttu-id="638b4-168">현재 폴더 수준의 모든 것 또는 모든 파일 이름 또는 모든 파일 확장명을 일치시킵니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-168">Matches anything at the current folder level, or any filename, or any file extension.</span></span> <span data-ttu-id="638b4-169">일치 항목은 파일 경로에서 `/` 및 `.` 문자로 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-169">Matches are terminated by `/` and `.` characters in the file path.</span></span>

<strong><code>**</code></strong>

   <span data-ttu-id="638b4-170">여러 디렉터리 수준에서 모든 것을 일치시킵니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-170">Matches anything across multiple directory levels.</span></span> <span data-ttu-id="638b4-171">디렉터리 계층 구조 내의 여러 파일과 일치시키는 데 재귀적으로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-171">Can be used to recursively match many files within a directory hierarchy.</span></span>

### <a name="globbing-pattern-examples"></a><span data-ttu-id="638b4-172">와일드카드 사용 패턴 예</span><span class="sxs-lookup"><span data-stu-id="638b4-172">Globbing pattern examples</span></span>

**`directory/file.txt`**

   <span data-ttu-id="638b4-173">특정 디렉터리에 있는 특정 파일을 일치시킵니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-173">Matches a specific file in a specific directory.</span></span>

**<code>directory/*.txt</code>**

   <span data-ttu-id="638b4-174">특정 디렉터리에서 `.txt` 확장명으로 모든 파일을 일치시킵니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-174">Matches all files with `.txt` extension in a specific directory.</span></span>

**`directory/*/bower.json`**

   <span data-ttu-id="638b4-175">`directory` 디렉터리보다 정확히 한 수준 아래의 디렉터리에서 모든 `bower.json` 파일을 일치시킵니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-175">Matches all `bower.json` files in directories exactly one level below the `directory` directory.</span></span>

**<code>directory/&#42;&#42;/&#42;.txt</code>**

   <span data-ttu-id="638b4-176">`directory` 디렉터리 아래의 모든 곳에서 찾은 모든 파일을 `.txt` 확장명으로 일치시킵니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-176">Matches all files with `.txt` extension found anywhere under the `directory` directory.</span></span>

## <a name="file-provider-usage-in-aspnet-core"></a><span data-ttu-id="638b4-177">ASP.NET Core에서 파일 공급자 사용</span><span class="sxs-lookup"><span data-stu-id="638b4-177">File Provider usage in ASP.NET Core</span></span>

<span data-ttu-id="638b4-178">ASP.NET Core의 여러 부분에서 파일 공급자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-178">Several parts of ASP.NET Core utilize file providers.</span></span> <span data-ttu-id="638b4-179">`IHostingEnvironment`는 `IFileProvider` 형식으로 앱의 콘텐츠 루트 및 웹 루트를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-179">`IHostingEnvironment` exposes the app's content root and web root as `IFileProvider` types.</span></span> <span data-ttu-id="638b4-180">정적 파일 미들웨어는 파일 공급자를 사용하여 정적 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-180">The static files middleware uses file providers to locate static files.</span></span> <span data-ttu-id="638b4-181">Razor는 보기 찾기에서 `IFileProvider`를 많이 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-181">Razor makes heavy use of `IFileProvider` in locating views.</span></span> <span data-ttu-id="638b4-182">Dotnet의 게시 기능은 파일 공급자 및 와일드카드 사용 패턴을 사용하여 게시되어야 하는 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-182">Dotnet's publish functionality uses file providers and globbing patterns to specify which files should be published.</span></span>

## <a name="recommendations-for-use-in-apps"></a><span data-ttu-id="638b4-183">앱에서 사용에 대한 권장 사항</span><span class="sxs-lookup"><span data-stu-id="638b4-183">Recommendations for use in apps</span></span>

<span data-ttu-id="638b4-184">ASP.NET Core 앱에 파일 시스템 액세스가 필요한 경우 종속성 주입을 통해 `IFileProvider`의 인스턴스를 요청한 다음, 이 샘플에 나와 있는 것처럼 해당 메서드를 사용하여 액세스를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-184">If your ASP.NET Core app requires file system access, you can request an instance of `IFileProvider` through dependency injection, and then use its methods to perform the access, as shown in this sample.</span></span> <span data-ttu-id="638b4-185">이를 통해 앱이 시작하고 앱이 인스턴스화하는 구현 형식의 수를 줄일 때 공급자를 한 번 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="638b4-185">This allows you to configure the provider once, when the app starts up, and reduces the number of implementation types your app instantiates.</span></span>
