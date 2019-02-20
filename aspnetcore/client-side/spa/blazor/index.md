---
title: Blazor 소개
author: guardrex
description: WebAssembly를 통해 브라우저에서 실행되는 대화형 클라이언트 쪽 앱을 .NET을 사용하여 빌드하는 새로운 프레임워크인 ASP.NET Core Blazor를 살펴봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/11/2019
uid: spa/blazor/index
---
# <a name="introduction-to-blazor"></a><span data-ttu-id="bc455-103">Blazor 소개</span><span class="sxs-lookup"><span data-stu-id="bc455-103">Introduction to Blazor</span></span>

<span data-ttu-id="bc455-104">작성자: [Daniel Roth](https://github.com/danroth27) 및 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="bc455-104">By [Daniel Roth](https://github.com/danroth27) and [Luke Latham](https://github.com/guardrex)</span></span>

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

<span data-ttu-id="bc455-105">Blazor는 .NET을 사용하여 대화형 클라이언트 쪽 웹앱을 빌드하기 위한 단일 페이지 앱 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-105">Blazor is a single-page app framework for building interactive client-side Web apps with .NET.</span></span> <span data-ttu-id="bc455-106">Blazor는 플러그 인이나 코드 소스 간 컴파일 없이 개방형 웹 표준을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-106">Blazor uses open web standards without plugins or code transpilation.</span></span> <span data-ttu-id="bc455-107">Blazor는 모바일 브라우저를 비롯한 모든 최신 웹 브라우저에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-107">Blazor works in all modern web browsers, including mobile browsers.</span></span>

<span data-ttu-id="bc455-108">브라우저에서 클라이언트 쪽 웹 개발에 .NET을 사용하면 다음과 같은 많은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-108">Using .NET in the browser for client-side web development offers many advantages:</span></span>

* <span data-ttu-id="bc455-109">**C# 언어**: JavaScript 대신 C#으로 코드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-109">**C# language**: Write code in C# instead of JavaScript.</span></span>
* <span data-ttu-id="bc455-110">**.NET 에코시스템**: .NET 라이브러리의 기존 에코시스템을 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-110">**.NET Ecosystem**: Leverage the existing ecosystem of .NET libraries.</span></span>
* <span data-ttu-id="bc455-111">**전체 스택 개발**: 서버 및 클라이언트 쪽 논리를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-111">**Full-stack development**: Share server and client-side logic.</span></span>
* <span data-ttu-id="bc455-112">**속도 및 확장성**: .NET은 성능, 안정성 및 보안을 위해 빌드되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-112">**Speed and scalability**: .NET was built for performance, reliability, and security.</span></span>
* <span data-ttu-id="bc455-113">**업계 최고의 도구**: Windows, Linux 및 macOS에서 Visual Studio를 사용하여 생산성을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-113">**Industry-leading tools**: Stay productive with Visual Studio on Windows, Linux, and macOS.</span></span>
* <span data-ttu-id="bc455-114">**안정성 및 일관성**:  안정적이고, 기능이 풍부하고, 간편한 일반적인 언어, 프레임워크 및 도구를 기반으로 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-114">**Stability and consistency**:  Build on a commonset of languages, frameworks, and tools that are stable, feature-rich, and easy to use.</span></span>

<span data-ttu-id="bc455-115">웹 브라우저 내에서 .NET 코드를 실행하는 것은 [WebAssembly](http://webassembly.org)(약식 *wasm*)를 통해 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-115">Running .NET code inside web browsers is made possible by [WebAssembly](http://webassembly.org) (abbreviated *wasm*).</span></span> <span data-ttu-id="bc455-116">WebAssembly는 개방형 웹 표준이고 플러그 인 없이 웹 브라우저에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-116">WebAssembly is an open web standard and supported in web browsers without plugins.</span></span> <span data-ttu-id="bc455-117">WebAssembly는 빠른 다운로드와 최대 실행 속도를 위해 최적화된 압축 바이트 코드 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-117">WebAssembly is a compact bytecode format optimized for fast download and maximum execution speed.</span></span>

<span data-ttu-id="bc455-118">WebAssembly 코드는 JavaScript interop을 통해 브라우저의 전체 기능에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-118">WebAssembly code can access the full functionality of the browser via JavaScript interop.</span></span> <span data-ttu-id="bc455-119">동시에, WebAssembly를 통해 실행되는 .NET 코드는 JavaScript와 동일한 신뢰할 수 있는 샌드박스에서 실행되어 클라이언트 머신에서 악의적인 동작을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-119">At the same time, .NET code executed via WebAssembly runs in the same trusted sandbox as JavaScript to prevent malicious actions on the client machine.</span></span>

![Blazor는 WebAssembly와 함께 브라우저에서 .NET 코드를 실행합니다.](index/_static/blazor.png)

<span data-ttu-id="bc455-121">Blazor 앱이 빌드되고 브라우저에서 실행되는 경우:</span><span class="sxs-lookup"><span data-stu-id="bc455-121">When a Blazor app is built and run in a browser:</span></span>

* <span data-ttu-id="bc455-122">C# 코드 파일과 Razor 파일은 .NET 어셈블리로 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-122">C# code files and Razor files are compiled into .NET assemblies.</span></span>
* <span data-ttu-id="bc455-123">어셈블리와 .NET 런타임이 브라우저에 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-123">The assemblies and the .NET runtime are downloaded to the browser.</span></span>
* <span data-ttu-id="bc455-124">Blazor는 .NET 런타임을 부트스트랩하고 앱의 어셈블리를 로드하도록 런타임을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-124">Blazor bootstraps the .NET runtime and configures the runtime to load the assemblies for the app.</span></span> <span data-ttu-id="bc455-125">DOM(문서 개체 모델) 조작 및 브라우저 API 호출은 JavaScript interop을 통해 Blazor 런타임에 의해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-125">Document Object Model (DOM) manipulation and browser API calls are handled by the Blazor runtime via JavaScript interop.</span></span>

<span data-ttu-id="bc455-126">Blazor는 다음을 포함한 대부분의 앱에 필요한 핵심 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-126">Blazor supports core facilities required by most apps, including:</span></span>

* <span data-ttu-id="bc455-127">매개 변수</span><span class="sxs-lookup"><span data-stu-id="bc455-127">Parameters</span></span>
* <span data-ttu-id="bc455-128">이벤트 처리</span><span class="sxs-lookup"><span data-stu-id="bc455-128">Event handling</span></span>
* <span data-ttu-id="bc455-129">데이터 바인딩</span><span class="sxs-lookup"><span data-stu-id="bc455-129">Data binding</span></span>
* <span data-ttu-id="bc455-130">라우팅</span><span class="sxs-lookup"><span data-stu-id="bc455-130">Routing</span></span>
* <span data-ttu-id="bc455-131">종속성 주입</span><span class="sxs-lookup"><span data-stu-id="bc455-131">Dependency injection</span></span>
* <span data-ttu-id="bc455-132">레이아웃</span><span class="sxs-lookup"><span data-stu-id="bc455-132">Layouts</span></span>
* <span data-ttu-id="bc455-133">템플릿</span><span class="sxs-lookup"><span data-stu-id="bc455-133">Templating</span></span>
* <span data-ttu-id="bc455-134">연계 값</span><span class="sxs-lookup"><span data-stu-id="bc455-134">Cascading values</span></span>

<span data-ttu-id="bc455-135">다운로드된 앱의 크기를 줄이기 위해 [IL(중간 언어) 링커](xref:host-and-deploy/razor-components/configure-linker)에서 게시하면 사용되지 않는 코드가 앱에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-135">To reduce the size of the downloaded app unused code stripped out of the app when it's published by the [Intermediate Language (IL) Linker](xref:host-and-deploy/razor-components/configure-linker).</span></span>

<span data-ttu-id="bc455-136">Blazor는 Razor 구성 요소의 클라이언트 쪽 호스팅 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-136">Blazor is the client-side hosting model for Razor Components.</span></span> <span data-ttu-id="bc455-137">Razor 구성 요소는 UI 업데이트 적용 방식에서 구성 요소의 렌더링 논리를 분리하기 때문에 Razor 구성 요소를 호스트하는 방법에 유연성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-137">Because Razor Components decouple a component's rendering logic from how UI updates are applied, there's flexibility in how Razor Components can be hosted.</span></span> <span data-ttu-id="bc455-138">ASP.NET Core Razor 구성 요소를 사용하여 SignalR 연결을 통해 모든 UI 업데이트가 처리되는 ASP.NET Core 앱의 서버에서 Razor 구성 요소를 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-138">Use ASP.NET Core Razor Components to host Razor Components on the server in an ASP.NET Core app where UI updates are handled over a SignalR connection.</span></span> <span data-ttu-id="bc455-139">자세한 내용은 <xref:razor-components/hosting-models#server-side-hosting-model>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc455-139">For more information, see <xref:razor-components/hosting-models#server-side-hosting-model>.</span></span> 

## <a name="components"></a><span data-ttu-id="bc455-140">구성 요소</span><span class="sxs-lookup"><span data-stu-id="bc455-140">Components</span></span>

<span data-ttu-id="bc455-141">‘Razor 구성 요소’는 페이지, 대화 상자 또는 데이터 입력 양식과 같은 UI의 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-141">A *Razor Component* is a piece of UI, such as a page, dialog, or data entry form.</span></span> <span data-ttu-id="bc455-142">구성 요소는 사용자 이벤트를 처리하고 유연한 UI 렌더링 논리를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-142">Components handle user events and define flexible UI rendering logic.</span></span> <span data-ttu-id="bc455-143">구성 요소는 중첩 및 재사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-143">Components can be nested and reused.</span></span>

<span data-ttu-id="bc455-144">구성 요소는 NuGet 패키지로 공유 및 배포될 수 있는 .NET 어셈블리에 기본 제공된 .NET 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-144">Components are .NET classes built into .NET assemblies that can be shared and distributed as NuGet packages.</span></span> <span data-ttu-id="bc455-145">클래스는 Razor 태그 페이지(*.cshtml*) 또는 C# 클래스(*.cs*) 형식으로 작성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-145">The class can either be written in the form of a Razor markup page (*.cshtml*) or as a C# class (*.cs*).</span></span>

<span data-ttu-id="bc455-146">[Razor](xref:mvc/views/razor)는 HTML 태그와 C# 코드를 결합하는 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-146">[Razor](xref:mvc/views/razor) is a syntax for combining HTML markup with C# code.</span></span> <span data-ttu-id="bc455-147">Razor는 개발자 생산성을 위해 설계되었으며, 개발자는 [IntelliSense](/visualstudio/ide/using-intellisense) 지원으로 동일한 파일에서 태그와 C# 사이를 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-147">Razor is designed for developer productivity, allowing the developer to switch between markup and C# in the same file with [IntelliSense](/visualstudio/ide/using-intellisense) support.</span></span> <span data-ttu-id="bc455-148">Razor Pages 및 MVC 뷰에도 Razor를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-148">Razor Pages and MVC views also use Razor.</span></span> <span data-ttu-id="bc455-149">요청/응답 모델을 중심으로 빌드된 Razor Pages 및 MVC 뷰와는 달리, 구성 요소는 특별히 UI 컴퍼지션을 처리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-149">Unlike Razor Pages and MVC views, which are built around a request/response model, components are used specifically for handling UI composition.</span></span> <span data-ttu-id="bc455-150">Razor 구성 요소는 특별히 클라이언트 쪽 UI 논리 및 컴퍼지션에 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-150">Razor Components can be used specifically for client-side UI logic and composition.</span></span>

<span data-ttu-id="bc455-151">다음 태그는 Razor 파일(*DialogComponent.cshtml*)의 사용자 지정 대화 상자 구성 요소의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-151">The following markup is an example of a custom dialog component in a Razor file (*DialogComponent.cshtml*):</span></span>

```cshtml
<div>
    <h2>@Title</h2>
    @BodyContent
    <button onclick=@OnOK>OK</button>
</div>

@functions {
    public string Title { get; set; }
    public RenderFragment BodyContent { get; set; }
    public Action OnOK { get; set; }
}
```

<span data-ttu-id="bc455-152">이 구성 요소를 앱의 다른 곳에서 사용할 경우 IntelliSense는 구문 및 매개 변수 완성을 통해 개발 속도를 높입니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-152">When this component is used elsewhere in the app, IntelliSense speeds development with syntax and parameter completion.</span></span>

<span data-ttu-id="bc455-153">구성 요소는 유연하고 효율적인 방법으로 UI를 업데이트하는 데 사용할 수 있는 ‘렌더링 트리’라는 브라우저 DOM의 메모리 내 표시로 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-153">Components render into an in-memory representation of the browser DOM called a *render tree* that can then be used to update the UI in a flexible and efficient way.</span></span>

## <a name="javascript-interop"></a><span data-ttu-id="bc455-154">JavaScript interop</span><span class="sxs-lookup"><span data-stu-id="bc455-154">JavaScript interop</span></span>

<span data-ttu-id="bc455-155">타사 JavaScript 라이브러리 및 브라우저 API를 필요로 하는 앱의 경우 Blazor는 JavaScript와 상호 운용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-155">For apps that require third-party JavaScript libraries and browser APIs, Blazor interoperates with JavaScript.</span></span> <span data-ttu-id="bc455-156">구성 요소는 JavaScript가 사용할 수 있는 모든 라이브러리 또는 API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-156">Components are capable of using any library or API that JavaScript is able to use.</span></span> <span data-ttu-id="bc455-157">C# 코드는 JavaScript 코드로 호출할 수 있으며, JavaScript 코드는 C# 코드로 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-157">C# code can call into JavaScript code, and JavaScript code can call into C# code.</span></span> <span data-ttu-id="bc455-158">자세한 내용은 [JavaScript interop](xref:razor-components/javascript-interop)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc455-158">For more information, see [JavaScript interop](xref:razor-components/javascript-interop).</span></span>

## <a name="code-sharing-and-net-standard"></a><span data-ttu-id="bc455-159">코드 공유 및 .NET Standard</span><span class="sxs-lookup"><span data-stu-id="bc455-159">Code sharing and .NET Standard</span></span>

<span data-ttu-id="bc455-160">앱은 기존 [.NET Standard](/dotnet/standard/net-standard) 라이브러리를 참조하고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-160">Apps can reference and use existing [.NET Standard](/dotnet/standard/net-standard) libraries.</span></span> <span data-ttu-id="bc455-161">.NET Standard는 .NET 구현에서 공통적인 .NET API의 공식 사양입니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-161">.NET Standard is a formal specification of .NET APIs that are common across .NET implementations.</span></span> <span data-ttu-id="bc455-162">.NET Standard 2.0 이상이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-162">.NET Standard 2.0 or higher is supported.</span></span> <span data-ttu-id="bc455-163">웹 브라우저 내에서 적용되지 않는 API(예: 파일 시스템 액세스, 소켓 열기, 스레딩 및 기타 기능)에서 <xref:System.PlatformNotSupportedException>을 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-163">APIs that aren't applicable inside a web browser (for example, accessing the file system, opening a socket, threading, and other features) throw <xref:System.PlatformNotSupportedException>.</span></span> <span data-ttu-id="bc455-164">.NET Standard 클래스 라이브러리는 서버 코드와 브라우저 기반 앱에서 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-164">.NET Standard class libraries can be shared across server code and in browser-based apps.</span></span>

## <a name="optimization"></a><span data-ttu-id="bc455-165">최적화</span><span class="sxs-lookup"><span data-stu-id="bc455-165">Optimization</span></span>

<span data-ttu-id="bc455-166">페이로드 크기는 앱의 유용성에 중요한 성능 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-166">Payload size is a critical performance factor for an app's useability.</span></span> <span data-ttu-id="bc455-167">Blazor는 페이로드 크기를 최적화하여 다운로드 시간을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-167">Blazor optimizes payload size to reduce download times:</span></span>

* <span data-ttu-id="bc455-168">.NET 어셈블리의 사용되지 않는 부분은 빌드 프로세스 중에 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-168">Unused parts of .NET assemblies are removed during the build process.</span></span>
* <span data-ttu-id="bc455-169">HTTP 응답이 압축됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-169">HTTP responses are compressed.</span></span>
* <span data-ttu-id="bc455-170">.NET 런타임 및 어셈블리가 브라우저에 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-170">The .NET runtime and assemblies are cached in the browser.</span></span>

<span data-ttu-id="bc455-171">[서버 쪽 Razor 구성 요소](xref:razor-components/index)는 .NET 어셈블리, 앱의 어셈블리 및 런타임 서버 쪽을 유지 관리하여 Blazor보다 작은 페이로드 크기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-171">[Server-side Razor Components](xref:razor-components/index) provides an even smaller payload size than Blazor by maintaining .NET assemblies, the app's assembly, and the runtime server-side.</span></span> <span data-ttu-id="bc455-172">Razor 구성 요소 앱은 클라이언트에 태그 파일 및 정적 자산만 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bc455-172">Razor Components apps only serve markup files and static assets to clients.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bc455-173">추가 자료</span><span class="sxs-lookup"><span data-stu-id="bc455-173">Additional resources</span></span>

* <xref:razor-components/index>
* [<span data-ttu-id="bc455-174">WebAssembly</span><span class="sxs-lookup"><span data-stu-id="bc455-174">WebAssembly</span></span>](http://webassembly.org/)
* [<span data-ttu-id="bc455-175">C# 가이드</span><span class="sxs-lookup"><span data-stu-id="bc455-175">C# Guide</span></span>](/dotnet/csharp/)
* <xref:mvc/views/razor>
* [<span data-ttu-id="bc455-176">HTML</span><span class="sxs-lookup"><span data-stu-id="bc455-176">HTML</span></span>](https://www.w3.org/html/)
