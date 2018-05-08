---
title: ASP.NET Core의 파일 공급자
author: ardalis
description: ASP.NET Core에서 파일 공급자를 사용하여 파일 시스템 액세스를 추상화하는 방법을 알아봅니다.
manager: wpickett
ms.author: riande
ms.date: 02/14/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/file-providers
ms.openlocfilehash: cdbffdadd9616fe941809d67dc2c0bbd52149561
ms.sourcegitcommit: 7ac15eaae20b6d70e65f3650af050a7880115cbf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2018
---
# <a name="file-providers-in-aspnet-core"></a><span data-ttu-id="44a13-103">ASP.NET Core의 파일 공급자</span><span class="sxs-lookup"><span data-stu-id="44a13-103">File Providers in ASP.NET Core</span></span>

<span data-ttu-id="44a13-104">작성자: [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="44a13-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="44a13-105">ASP.NET Core에서 파일 공급자를 사용하여 파일 시스템 액세스를 추상화합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-105">ASP.NET Core abstracts file system access through the use of File Providers.</span></span>

<span data-ttu-id="44a13-106">[예제 코드 보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/file-providers/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="44a13-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/file-providers/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="file-provider-abstractions"></a><span data-ttu-id="44a13-107">파일 공급자 추상화</span><span class="sxs-lookup"><span data-stu-id="44a13-107">File Provider abstractions</span></span>

<span data-ttu-id="44a13-108">파일 공급자는 파일 시스템에 대한 추상화로.</span><span class="sxs-lookup"><span data-stu-id="44a13-108">File Providers are an abstraction over file systems.</span></span> <span data-ttu-id="44a13-109">기본 인터페이스는 `IFileProvider`입니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-109">The main interface is `IFileProvider`.</span></span> <span data-ttu-id="44a13-110">`IFileProvider`는 파일 정보(`IFileInfo`)나 디렉터리 정보(`IDirectoryContents`)를 가져오고, 변경 알림을 설정(`IChangeToken` 을 사용) 하는 메서드를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-110">`IFileProvider` exposes methods to get file information (`IFileInfo`), directory information (`IDirectoryContents`), and to set up change notifications (using an `IChangeToken`).</span></span>

<span data-ttu-id="44a13-111">`IFileInfo`는 개별 파일 및 디렉터리에 대한 메서드와 속성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-111">`IFileInfo` provides methods and properties about individual files or directories.</span></span> <span data-ttu-id="44a13-112">두 가지 불리언 속성인 `Exists` 속성과 `IsDirectory`속성을 비롯해서 파일 이름(`Name`), 크기(`Length`, 바이트) 및 마지막 수정 날짜(`LastModified`)를 기술하는 속성들을 갖고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-112">It has two boolean properties, `Exists` and `IsDirectory`, as well as properties describing the file's `Name`, `Length` (in bytes), and `LastModified` date.</span></span> <span data-ttu-id="44a13-113">`CreateReadStream` 메서드를 사용해서 파일을 읽을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-113">You can read from the file using its `CreateReadStream` method.</span></span>

## <a name="file-provider-implementations"></a><span data-ttu-id="44a13-114">파일 공급자 구현</span><span class="sxs-lookup"><span data-stu-id="44a13-114">File Provider implementations</span></span>

<span data-ttu-id="44a13-115">`IFileProvider` 의 구현으로 물리적 공급자, 임베디드 공급자 그리고 복합 공급자의 세 가지 공급자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-115">Three implementations of `IFileProvider` are available: Physical, Embedded, and Composite.</span></span> <span data-ttu-id="44a13-116">물리적 공급자는 시스템의 실제 파일에 접근하기 위해서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-116">The physical provider is used to access the actual system's files.</span></span> <span data-ttu-id="44a13-117">그리고 임베디드 공급자는 어셈블리에 포함된 파일에 접근하기 위해서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-117">The embedded provider is used to access files embedded in assemblies.</span></span> <span data-ttu-id="44a13-118">마지막으로 복합 공급자는 하나 이상의 개별 공급자로부터 얻어진 파일 및 디렉터리에 대한 복합적인 접근을 지원하기 위해서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-118">The composite provider is used to provide combined access to files and directories from one or more other providers.</span></span>

### <a name="physicalfileprovider"></a><span data-ttu-id="44a13-119">PhysicalFileProvider</span><span class="sxs-lookup"><span data-stu-id="44a13-119">PhysicalFileProvider</span></span>

<span data-ttu-id="44a13-120">`PhysicalFileProvider` 는 실제 파일 시스템에 대한 접근을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-120">The `PhysicalFileProvider` provides access to the physical file system.</span></span> <span data-ttu-id="44a13-121">`System.IO.File` 형식을 (물리적 공급자에 대해) 래핑하고, 특정 디렉터리와 그 하위 자식들에 대한 모든 경로를 대상 범위로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-121">It wraps the `System.IO.File` type (for the physical provider), scoping all paths to a directory and its children.</span></span> <span data-ttu-id="44a13-122">이렇게 범위를 지정함으로써 특정 디렉터리 및 그 하위 자식들에 대한 접근만 허용해서 경계 외부의 파일 시스템에 대한 접근을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-122">This scoping limits access to a certain directory and its children, preventing access to the file system outside of this boundary.</span></span> <span data-ttu-id="44a13-123">이 공급자의 인스턴스를 생성하려면 이 공급자를 대상으로 하는 모든 요청에 대해 기본 경로 역할을 하는 (그리고 해당 경로 외부에 대한 접근은 차단하는) 디렉터리 경로를 반드시 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-123">When instantiating this provider, you must provide it with a directory path, which serves as the base path for all requests made to this provider (and which restricts access outside of this path).</span></span> <span data-ttu-id="44a13-124">ASP.NET Core 응용 프로그램에서는 `PhysicalFileProvider` 공급자의 인스턴스를 직접 생성하거나, 컨트롤러 또는 서비스의 생성자에서 `IFileProvider`종속성 주입[ 을 통해서 ](dependency-injection.md) 를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-124">In an ASP.NET Core app, you can instantiate a `PhysicalFileProvider` provider directly, or you can request an `IFileProvider` in a Controller or service's constructor through [dependency injection](dependency-injection.md).</span></span> <span data-ttu-id="44a13-125">일반적으로 후자의 접근 방식이 보다 유연하고 테스트 가능한 솔루션을 만들어줍니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-125">The latter approach will typically yield a more flexible and testable solution.</span></span>

<span data-ttu-id="44a13-126">다음 예제는 `PhysicalFileProvider` 를 생성하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-126">The sample below shows how to create a `PhysicalFileProvider`.</span></span>


```csharp
IFileProvider provider = new PhysicalFileProvider(applicationRoot);
IDirectoryContents contents = provider.GetDirectoryContents(""); // the applicationRoot contents
IFileInfo fileInfo = provider.GetFileInfo("wwwroot/js/site.js"); // a file under applicationRoot
```

<span data-ttu-id="44a13-127">하위 경로를 지정해서 디렉터리의 내용을 반복 조회하거나 특정 파일의 정보를 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-127">You can iterate through its directory contents or get a specific file's information by providing a subpath.</span></span>

<span data-ttu-id="44a13-128">컨트롤러에서 공급자를 사용하려면 공급자를 컨트롤러의 생성자 매개 변수로 지정한 다음, 전달받은 공급자 개체를 필드에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-128">To request a provider from a controller, specify it in the controller's constructor and assign it to a local field.</span></span> <span data-ttu-id="44a13-129">그리고 액션 메서드에서는 이 로컬 인스턴스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-129">Use the local instance from your action methods:</span></span>

[!code-csharp[](file-providers/sample/src/FileProviderSample/Controllers/HomeController.cs?highlight=5,7,12&range=6-19)]

<span data-ttu-id="44a13-130">그런 다음, 응용 프로그램의 `Startup` 클래스에서 공급자를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-130">Then, create the provider in the app's `Startup` class:</span></span>

[!code-csharp[](file-providers/sample/src/FileProviderSample/Startup.cs?highlight=35,40&range=1-43)]

<span data-ttu-id="44a13-131">다음 *Index.cshtml* 뷰는 전달된 `IDirectoryContents` 를 반복 조회합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-131">In the *Index.cshtml* view, iterate through the `IDirectoryContents` provided:</span></span>

[!code-html[](file-providers/sample/src/FileProviderSample/Views/Home/Index.cshtml?highlight=2,7,9,11,15)]

<span data-ttu-id="44a13-132">그 결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-132">The result:</span></span>

![파일 공급자 예제 응용 프로그램이 실제 파일 및 폴더의 목록을 출력합니다.](file-providers/_static/physical-directory-listing.png)

### <a name="embeddedfileprovider"></a><span data-ttu-id="44a13-134">EmbeddedFileProvider</span><span class="sxs-lookup"><span data-stu-id="44a13-134">EmbeddedFileProvider</span></span>

<span data-ttu-id="44a13-135">`EmbeddedFileProvider` 는 어셈블리에 포함된 파일에 접근하기 위한 용도로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-135">The `EmbeddedFileProvider` is used to access files embedded in assemblies.</span></span> <span data-ttu-id="44a13-136">.NET Core에서는 *.csproj* 파일의 `<EmbeddedResource>` 요소에 지정된 파일들이 어셈블리에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-136">In .NET Core, you embed files in an assembly with the `<EmbeddedResource>` element in the *.csproj* file:</span></span>

[!code-json[](file-providers/sample/src/FileProviderSample/FileProviderSample.csproj?range=13-18)]

<span data-ttu-id="44a13-137">어셈블리에 포함시킬 파일들을 지정할 때, [Globbing 패턴](#globbing-patterns) 을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-137">You can use [globbing patterns](#globbing-patterns) when specifying files to embed in the assembly.</span></span> <span data-ttu-id="44a13-138">이 패턴을 사용하면 하나 이상의 파일을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-138">These patterns can be used to match one or more files.</span></span>

> [!NOTE]
> <span data-ttu-id="44a13-139">실제로 프로젝트의 모든 .js 파일을 어셈블리에 포함시키는 일은 거의 없습니다. 위 예제는 단지 설명을 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-139">It's unlikely you would ever want to actually embed every .js file in your project in its assembly; the above sample is for demo purposes only.</span></span>

<span data-ttu-id="44a13-140">`EmbeddedFileProvider` 를 생성할 때, 생성자에게 읽고자 하는 어셈블리를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-140">When creating an `EmbeddedFileProvider`, pass the assembly it will read to its constructor.</span></span>

```csharp
var embeddedProvider = new EmbeddedFileProvider(Assembly.GetEntryAssembly());
```

<span data-ttu-id="44a13-141">위의 코드 조각은 현재 실행 중인 어셈블리에 접근하는 `EmbeddedFileProvider` 를 생성하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-141">The snippet above demonstrates how to create an `EmbeddedFileProvider` with access to the currently executing assembly.</span></span>

<span data-ttu-id="44a13-142">앞의 예제 응용 프로그램을 `EmbeddedFileProvider` 를 사용하도록 업데이트하면 다음과 같은 결과가 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-142">Updating the sample app to use an `EmbeddedFileProvider` results in the following output:</span></span>

![파일 공급자 예제 응용 프로그램이 임베디드 파일들의 목록을 출력합니다.](file-providers/_static/embedded-directory-listing.png)

> [!NOTE]
> <span data-ttu-id="44a13-144">어셈블리에 포함된 리소스는 디렉터리를 노출하지 않는 반면.</span><span class="sxs-lookup"><span data-stu-id="44a13-144">Embedded resources don't expose directories.</span></span> <span data-ttu-id="44a13-145">대신, 리소스에 대한 경로(해당 네임스페이스를 통해)는 `.` 구분 기호를 사용하여 해당 파일 이름에서 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-145">Rather, the path to the resource (via its namespace) is embedded in its filename using `.` separators.</span></span>

> [!TIP]
> <span data-ttu-id="44a13-146">`EmbeddedFileProvider` 생성자는 선택적 `baseNamespace` 매개 변수를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-146">The `EmbeddedFileProvider` constructor accepts an optional `baseNamespace` parameter.</span></span> <span data-ttu-id="44a13-147">이를 지정하면 `GetDirectoryContents`에 대한 호출을 제공된 네임스페이스 아래의 해당 리소스로 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-147">Specifying this will scope calls to `GetDirectoryContents` to those resources under the provided namespace.</span></span>

### <a name="compositefileprovider"></a><span data-ttu-id="44a13-148">CompositeFileProvider</span><span class="sxs-lookup"><span data-stu-id="44a13-148">CompositeFileProvider</span></span>

<span data-ttu-id="44a13-149">`CompositeFileProvider` 는 `IFileProvider` 의 인스턴스들을 결합해서 다수의 공급자를 이용한 파일 작업을 처리할 수 있는 단일 인터페이스를 제공합니다. </span><span class="sxs-lookup"><span data-stu-id="44a13-149">The `CompositeFileProvider` combines `IFileProvider` instances, exposing a single interface for working with files from multiple providers.</span></span> <span data-ttu-id="44a13-150">`CompositeFileProvider` 를 생성할 때는 생성자에 하나 이상의 `IFileProvider` 인스턴스를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-150">When creating the `CompositeFileProvider`, you pass one or more `IFileProvider` instances to its constructor:</span></span>

[!code-csharp[](file-providers/sample/src/FileProviderSample/Startup.cs?highlight=3&range=35-37)]

<span data-ttu-id="44a13-151">이전에 구성된 물리적 및 포함된 공급자 모두를 포함하는 `CompositeFileProvider`를 사용하도록 샘플 앱을 업데이트하면 다음 출력과 같은 결과가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-151">Updating the sample app to use a `CompositeFileProvider` that includes both the physical and embedded providers configured previously, results in the following output:</span></span>

![물리적 파일 및 폴더와 포함된 파일을 나열하는 파일 공급자 샘플 응용 프로그램](file-providers/_static/composite-directory-listing.png)

## <a name="watching-for-changes"></a><span data-ttu-id="44a13-153">변경 내용 감시하기</span><span class="sxs-lookup"><span data-stu-id="44a13-153">Watching for changes</span></span>

<span data-ttu-id="44a13-154">`IFileProvider`의 `Watch` 메서드를 이용하면 여러 파일 및 디렉터리의 변경 사항을 감지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-154">The `IFileProvider` `Watch` method provides a way to watch one or more files or directories for changes.</span></span> <span data-ttu-id="44a13-155">이 메서드는 [Globbing 패턴](#globbing-patterns)을 이용해서 복수의 파일을 지정할 수 있는 경로 문자열을 전달받고 `IChangeToken`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-155">This method accepts a path string, which can use [globbing patterns](#globbing-patterns) to specify multiple files, and returns an `IChangeToken`.</span></span> <span data-ttu-id="44a13-156">이 토큰은 변경 여부 확인에 사용할 수 있는 `HasChanged` 속성과, 지정된 경로 문자열에서 변경 내용이 감지되면 호출되는 `RegisterChangeCallback` 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-156">This token exposes a `HasChanged` property that can be inspected, and a `RegisterChangeCallback` method that's called when changes are detected to the specified path string.</span></span> <span data-ttu-id="44a13-157">각 변경 토큰은 단일 변경에 대한 응답으로 자신과 연결된 콜백만 호출한다는 점에 주의하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-157">Note that each change token only calls its associated callback in response to a single change.</span></span> <span data-ttu-id="44a13-158">모니터링을 지속적으로 수행하기 위해서는 다음 예제처럼 `TaskCompletionSource`를 활용하거나 변경 사항에 대한 응답에서 다시 `IChangeToken` 인스턴스를 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-158">To enable constant monitoring, you can use a `TaskCompletionSource` as shown below, or re-create `IChangeToken` instances in response to changes.</span></span>

<span data-ttu-id="44a13-159">이 문서 샘플에서 콘솔 응용 프로그램은 텍스트 파일이 수정될 때마다 메시지를 표시하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-159">In this article's sample, a console application is configured to display a message whenever a text file is modified:</span></span>

[!code-csharp[](file-providers/sample/src/WatchConsole/Program.cs?name=snippet1&highlight=1-2,16,19-20)]

<span data-ttu-id="44a13-160">파일을 여러 번 저장한 후 결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-160">The result, after saving the file several times:</span></span>

![dotnet 실행을 실행한 후 명령 창은 변경 내용에 대한 quotes.txt 파일을 모니터링하는 응용 프로그램과 파일이 5번 변경된 것을 보여 줍니다.](file-providers/_static/watch-console.png)

> [!NOTE]
> <span data-ttu-id="44a13-162">Docker 컨테이너나 네트워크 공유 같은 일부 파일 시스템은 변경 알림을 안정적으로 전송할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-162">Some file systems, such as Docker containers and network shares, may not reliably send change notifications.</span></span> <span data-ttu-id="44a13-163">그러나 `DOTNET_USE_POLLINGFILEWATCHER` 환경 변수를 `1`이나 `true`로 설정하면 파일 시스템이 4초마다 폴링됩니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-163">Set the `DOTNET_USE_POLLINGFILEWATCHER` environment variable to `1` or `true` to poll the file system for changes every 4 seconds.</span></span>

## <a name="globbing-patterns"></a><span data-ttu-id="44a13-164">Globbing 패턴</span><span class="sxs-lookup"><span data-stu-id="44a13-164">Globbing patterns</span></span>

<span data-ttu-id="44a13-165">파일 시스템 경로는 *Globbing 패턴*이라고도 부르는 와일드 카드 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-165">File system paths use wildcard patterns called *globbing patterns*.</span></span> <span data-ttu-id="44a13-166">이 단순 패턴을 이용해서 파일 그룹을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-166">These simple patterns can be used to specify groups of files.</span></span> <span data-ttu-id="44a13-167">두 개의 와일드 카드 문자는 `*`와 `**`입니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-167">The two wildcard characters are `*` and `**`.</span></span>

**`*`**

   <span data-ttu-id="44a13-168">현재 폴더 수준의 모든 항목, 모든 파일명 또는 모든 파일 확장자를 찾습니다</span><span class="sxs-lookup"><span data-stu-id="44a13-168">Matches anything at the current folder level, or any filename, or any file extension.</span></span> <span data-ttu-id="44a13-169">파일 경로의 `/` 및 `.` 문자에 의해서 일치가 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-169">Matches are terminated by `/` and `.` characters in the file path.</span></span>

<strong><code>**</code></strong>

   <span data-ttu-id="44a13-170">여러 디렉터리 수준에서 모든 것을 일치시킵니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-170">Matches anything across multiple directory levels.</span></span> <span data-ttu-id="44a13-171">디렉터리 계층 구조 내의 여러 파일과 일치시키는 데 재귀적으로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-171">Can be used to recursively match many files within a directory hierarchy.</span></span>

### <a name="globbing-pattern-examples"></a><span data-ttu-id="44a13-172">Globbing 패턴 예제</span><span class="sxs-lookup"><span data-stu-id="44a13-172">Globbing pattern examples</span></span>

**`directory/file.txt`**

   <span data-ttu-id="44a13-173">특정 디렉터리에 있는 특정 파일을 일치시킵니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-173">Matches a specific file in a specific directory.</span></span>

**<code>directory/*.txt</code>**

   <span data-ttu-id="44a13-174">특정 디렉터리에서 `.txt` 확장명으로 모든 파일을 일치시킵니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-174">Matches all files with `.txt` extension in a specific directory.</span></span>

**`directory/*/bower.json`**

   <span data-ttu-id="44a13-175">`directory` 디렉터리보다 정확히 한 수준 아래의 디렉터리에서 모든 `bower.json` 파일을 일치시킵니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-175">Matches all `bower.json` files in directories exactly one level below the `directory` directory.</span></span>

**<code>directory/&#42;&#42;/&#42;.txt</code>**

   <span data-ttu-id="44a13-176">`directory` 디렉터리 아래의 모든 곳에서 찾은 모든 파일을 `.txt` 확장명으로 일치시킵니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-176">Matches all files with `.txt` extension found anywhere under the `directory` directory.</span></span>

## <a name="file-provider-usage-in-aspnet-core"></a><span data-ttu-id="44a13-177">ASP.NET Core에서 파일 공급자 사용</span><span class="sxs-lookup"><span data-stu-id="44a13-177">File Provider usage in ASP.NET Core</span></span>

<span data-ttu-id="44a13-178">ASP.NET Core는 다양한 부분에서 파일 공급자를 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-178">Several parts of ASP.NET Core utilize file providers.</span></span> <span data-ttu-id="44a13-179">예를 들어,`IHostingEnvironment`는 응용 프로그램의 콘텐츠 루트와 웹 루트를 `IFileProvider` 형식으로 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-179">`IHostingEnvironment` exposes the app's content root and web root as `IFileProvider` types.</span></span> <span data-ttu-id="44a13-180">정적 파일 미들웨어는 파일 공급자를 이용해서 정적 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-180">The static files middleware uses file providers to locate static files.</span></span> <span data-ttu-id="44a13-181">Razor는 뷰를 찾기 위해 `IFileProvider`를 빈번히 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-181">Razor makes heavy use of `IFileProvider` in locating views.</span></span> <span data-ttu-id="44a13-182">Dotnet의 게시 기능은 파일 공급자와 Globbing 패턴을 사용해서 게시해야 할 파일들을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-182">Dotnet's publish functionality uses file providers and globbing patterns to specify which files should be published.</span></span>

## <a name="recommendations-for-use-in-apps"></a><span data-ttu-id="44a13-183">앱에서 사용에 대한 권장 사항</span><span class="sxs-lookup"><span data-stu-id="44a13-183">Recommendations for use in apps</span></span>

<span data-ttu-id="44a13-184">ASP.NET Core 앱에 파일 시스템 액세스가 필요한 경우 종속성 주입을 통해 `IFileProvider`의 인스턴스를 요청한 다음, 이 샘플에 나와 있는 것처럼 해당 메서드를 사용하여 액세스를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-184">If your ASP.NET Core app requires file system access, you can request an instance of `IFileProvider` through dependency injection, and then use its methods to perform the access, as shown in this sample.</span></span> <span data-ttu-id="44a13-185">이를 통해 앱이 시작하고 앱이 인스턴스화하는 구현 형식의 수를 줄일 때 공급자를 한 번 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44a13-185">This allows you to configure the provider once, when the app starts up, and reduces the number of implementation types your app instantiates.</span></span>
