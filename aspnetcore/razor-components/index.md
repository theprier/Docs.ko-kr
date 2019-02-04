---
title: Razor 구성 요소 소개
author: guardrex
description: WebAssembly와 함께 브라우저에서 실행되는 C#/Razor 및 HTML을 사용하여 .NET 웹 프레임워크인 Blazor를 탐색합니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/index
ms.openlocfilehash: 0f7a4b2ec404b6ceec2e643fea9e0635de6ad716
ms.sourcegitcommit: ed76cc752966c604a795fbc56d5a71d16ded0b58
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55667939"
---
# <a name="introduction-to-razor-components"></a><span data-ttu-id="b8e0c-103">Razor 구성 요소 소개</span><span class="sxs-lookup"><span data-stu-id="b8e0c-103">Introduction to Razor Components</span></span>

<span data-ttu-id="b8e0c-104">작성자: [Steve Sanderson](http://blog.stevensanderson.com), [Daniel Roth](https://github.com/danroth27) 및 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="b8e0c-104">By [Steve Sanderson](http://blog.stevensanderson.com), [Daniel Roth](https://github.com/danroth27), and [Luke Latham](https://github.com/guardrex)</span></span>

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

<span data-ttu-id="b8e0c-105">*Blazor*(클라이언트 쪽에서 실행되는 Razor 구성 요소)는 WebAssembly와 함께 브라우저에서 실행되는 C#/Razor 및 HTML을 사용하는 실험적인 .NET 웹 프레임워크인 반면, *ASP.NET Core Razor 구성 요소*는 ASP.NET Core에서 서버 쪽을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-105">*ASP.NET Core Razor Components* executes server-side in ASP.NET Core, while *Blazor* (Razor Components executed client-side) is an experimental .NET web framework using C#/Razor and HTML that runs in the browser with WebAssembly.</span></span> <span data-ttu-id="b8e0c-106">Blazor는 클라이언트에서 .NET을 사용하는 클라이언트 쪽 웹 UI 프레임워크의 모든 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-106">Blazor provides all of the benefits of a client-side web UI framework using .NET on the client.</span></span>

<span data-ttu-id="b8e0c-107">웹 개발은 수년에 걸쳐 여러 면에서 개선되었지만, 최신 웹앱을 빌드하는 데는 여전히 어려움이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-107">Web development has improved in many ways over the years, but building modern web apps still poses challenges.</span></span> <span data-ttu-id="b8e0c-108">브라우저에서 .NET을 사용하면 웹 개발을 보다 쉽고 더 생산적으로 만들 수 있는 많은 이점을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-108">Using .NET in the browser offers many advantages that can help make web development easier and more productive:</span></span>

* <span data-ttu-id="b8e0c-109">**안정성과 일관성**: .NET은 안정적이고 기능이 풍부하며 사용하기 쉬운 플랫폼 전반에 걸쳐 표준화된 프로그래밍 프레임워크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-109">**Stability and consistency**: .NET provides standardized programming frameworks across platforms that are stable, feature-rich, and easy to use.</span></span>
* <span data-ttu-id="b8e0c-110">**최신 혁신 언어**: .NET 언어는 혁신적인 새로운 언어 기능으로 끊임없이 개선되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-110">**Modern innovative languages**: .NET languages are constantly improving with innovative new language features.</span></span>
* <span data-ttu-id="b8e0c-111">**업계 최고의 도구**: Visual Studio 제품군은 Windows, Linux 및 macOS 플랫폼 전반에 걸쳐 환상적인 .NET 개발 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-111">**Industry-leading tools**: The Visual Studio product family provides a fantastic .NET development experience across platforms on Windows, Linux, and macOS.</span></span>
* <span data-ttu-id="b8e0c-112">**속도 및 확장성**: .NET은 앱 개발을 위한 성능, 안정성 및 보안에 대한 강력한 기록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-112">**Speed and scalability**: .NET has a strong history of performance, reliability, and security for app development.</span></span> <span data-ttu-id="b8e0c-113">.NET을 전체 스택 솔루션으로 사용하면 빠르고 안정적이며 안전한 앱을 쉽게 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-113">Using .NET as a full-stack solution makes it easier to build fast, reliable, and secure apps.</span></span>
* <span data-ttu-id="b8e0c-114">**기존 기술을 활용하는 전체 스택 개발**: C#/ Razor 개발자는 기존 C#/Razor 기술을 사용하여 클라이언트 쪽 코드를 작성하고 앱 간에 서버 및 클라이언트 쪽 논리를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-114">**Full-stack development that leverages existing skills**: C#/Razor developers use their existing C#/Razor skills to write client-side code and share server and client-side logic among apps.</span></span>
* <span data-ttu-id="b8e0c-115">**광범위한 브라우저 지원**: Razor 구성 요소는 UI를 일반 태그 및 JavaScript로 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-115">**Wide browser support**: Razor Components render the UI as ordinary markup and JavaScript.</span></span> <span data-ttu-id="b8e0c-116">Blazor는 플러그 인이나 코드 트랜스파일 없이 공개 웹 표준을 사용하여 브라우저의 .NET에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-116">Blazor runs on .NET in the browser using open web standards with no plugins and no code transpilation.</span></span> <span data-ttu-id="b8e0c-117">Blazor는 모바일 브라우저를 비롯한 모든 최신 웹 브라우저에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-117">Blazor works in all modern web browsers, including mobile browsers.</span></span>

## <a name="hosting-models"></a><span data-ttu-id="b8e0c-118">호스팅 모델</span><span class="sxs-lookup"><span data-stu-id="b8e0c-118">Hosting models</span></span>

### <a name="server-side-hosting-model"></a><span data-ttu-id="b8e0c-119">서버 쪽 호스팅 모델</span><span class="sxs-lookup"><span data-stu-id="b8e0c-119">Server-side hosting model</span></span>

<span data-ttu-id="b8e0c-120">Razor 구성 요소는 UI 업데이트가 적용되는 방식과 구성 요소의 렌더링 논리를 분리를 분리하기 때문에 Razor 구성 요소를 호스팅하는 방법에 유연성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-120">Because Razor Components decouple a component's rendering logic from how the UI updates are applied, there is flexibility in how Razor Components can be hosted.</span></span> <span data-ttu-id="b8e0c-121">.NET Core 3.0의 ASP.NET Core Razor 구성 요소는 SignalR 연결을 통해 모든 UI 업데이트가 처리되는 ASP.NET Core 앱의 서버에서 Razor 구성 요소를 호스팅하는 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-121">ASP.NET Core Razor Components in .NET Core 3.0 adds support for hosting Razor Components on the server in an ASP.NET Core app where all UI updates are handled over a SignalR connection.</span></span> <span data-ttu-id="b8e0c-122">런타임은 브라우저에서 서버로 UI 이벤트 전송을 처리한 다음, 구성 요소를 실행한 후 서버에서 보낸 UI 업데이트를 브라우저에 다시 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-122">The runtime handles sending UI events from the browser to the server and then applies UI updates sent by the server back to the browser after running the components.</span></span> <span data-ttu-id="b8e0c-123">JavaScript interop 호출을 처리하는 데에도 동일한 연결이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-123">The same connection is also used to handle JavaScript interop calls.</span></span>

![Razor 구성 요소는 서버에서 .NET 코드를 실행하고 SignalR 연결을 통해 클라이언트의 문서 개체 모델과 상호 작용합니다.](index/_static/aspnet-core-razor-components.png)

<span data-ttu-id="b8e0c-125">자세한 내용은 <xref:razor-components/hosting-models#server-side-hosting-model>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-125">For more information, see <xref:razor-components/hosting-models#server-side-hosting-model>.</span></span>

### <a name="client-side-hosting-model"></a><span data-ttu-id="b8e0c-126">클라이언트 쪽 호스팅 모델</span><span class="sxs-lookup"><span data-stu-id="b8e0c-126">Client-side hosting model</span></span>

<span data-ttu-id="b8e0c-127">웹 브라우저 내에서 .NET 코드를 실행하는 것은 비교적 새로운 기술인 [WebAssembly](http://webassembly.org)(약식 *wasm*)를 통해 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-127">Running .NET code inside web browsers is made possible by a relatively new technology, [WebAssembly](http://webassembly.org) (abbreviated *wasm*).</span></span> <span data-ttu-id="b8e0c-128">WebAssembly는 공개 웹 표준이며 플러그 인 없이 웹 브라우저에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-128">WebAssembly is an open web standard and is supported in web browsers without plugins.</span></span> <span data-ttu-id="b8e0c-129">WebAssembly는 빠른 다운로드와 최대 실행 속도를 위해 최적화된 압축 바이트 코드 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-129">WebAssembly is a compact bytecode format optimized for fast download and maximum execution speed.</span></span>

<span data-ttu-id="b8e0c-130">WebAssembly 코드는 JavaScript interop을 통해 브라우저의 전체 기능에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-130">WebAssembly code can access the full functionality of the browser via JavaScript interop.</span></span> <span data-ttu-id="b8e0c-131">동시에, WebAssembly 코드는 JavaScript와 동일한 신뢰할 수 있는 샌드박스에서 실행되어 클라이언트 머신에서 악의적인 동작을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-131">At the same time, WebAssembly code runs in the same trusted sandbox as JavaScript to prevent malicious actions on the client machine.</span></span>

![Blazor는 WebAssembly와 함께 브라우저에서 .NET 코드를 실행합니다.](index/_static/blazor.png)

<span data-ttu-id="b8e0c-133">Blazor 앱이 빌드되고 브라우저에서 실행되는 경우:</span><span class="sxs-lookup"><span data-stu-id="b8e0c-133">When a Blazor app is built and run in a browser:</span></span>

1. <span data-ttu-id="b8e0c-134">C# 코드 파일과 Razor 파일은 .NET 어셈블리로 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-134">C# code files and Razor files are compiled into .NET assemblies.</span></span>
1. <span data-ttu-id="b8e0c-135">어셈블리와 .NET 런타임이 브라우저에 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-135">The assemblies and the .NET runtime are downloaded to the browser.</span></span>
1. <span data-ttu-id="b8e0c-136">Blazor는 JavaScript를 사용하여 .NET 런타임을 부트스트랩하고 필요한 어셈블리 참조를 로드하도록 런타임을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-136">Blazor uses JavaScript to bootstrap the .NET runtime and configures the runtime to load required assembly references.</span></span> <span data-ttu-id="b8e0c-137">DOM(문서 개체 모델) 조작 및 브라우저 API 호출은 JavaScript 상호 운용성을 통해 Blazor 런타임에 의해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-137">Document object model (DOM) manipulation and browser API calls are handled by the Blazor runtime via JavaScript interoperability.</span></span>

<span data-ttu-id="b8e0c-138">WebAssembly를 지원하지 않는 이전 브라우저를 지원하기 위해 ASP.NET Core Razor 구성 요소 [서버 쪽 호스팅 모델](#server-side-hosting-model)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-138">To support older browsers that don't support WebAssembly, you can use the ASP.NET Core Razor Components [server-side hosting model](#server-side-hosting-model).</span></span>

<span data-ttu-id="b8e0c-139">자세한 내용은 <xref:razor-components/hosting-models#client-side-hosting-model>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-139">For more information, see <xref:razor-components/hosting-models#client-side-hosting-model>.</span></span>

## <a name="components"></a><span data-ttu-id="b8e0c-140">구성 요소</span><span class="sxs-lookup"><span data-stu-id="b8e0c-140">Components</span></span>

<span data-ttu-id="b8e0c-141">앱은 *구성 요소*로 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-141">Apps are built with *components*.</span></span> <span data-ttu-id="b8e0c-142">구성 요소는 페이지, 대화 상자 또는 데이터 입력 양식과 같은 UI의 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-142">A component is a piece of UI, such as a page, dialog, or data entry form.</span></span> <span data-ttu-id="b8e0c-143">구성 요소는 프로젝트 간에 중첩, 재사용 및 공유될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-143">Components can be nested, reused, and shared between projects.</span></span>

<span data-ttu-id="b8e0c-144">*구성 요소*는 .NET 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-144">A *component* is a .NET class.</span></span> <span data-ttu-id="b8e0c-145">클래스는 직접 C# 클래스(*\*.cs*)로 작성되거나 Razor 태그 페이지(*\*.cshtml*)의 형태로 작성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-145">The class can either be written directly, as a C# class (*\*.cs*), or more commonly in the form of a Razor markup page (*\*.cshtml*).</span></span>

<span data-ttu-id="b8e0c-146">[Razor](/aspnet/core/mvc/views/razor)는 HTML 태그와 C# 코드를 결합하는 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-146">[Razor](/aspnet/core/mvc/views/razor) is a syntax for combining HTML markup with C# code.</span></span> <span data-ttu-id="b8e0c-147">Razor는 개발자 생산성을 위해 설계되었으며, 개발자는 [IntelliSense](/visualstudio/ide/using-intellisense) 지원으로 동일한 파일에서 태그와 C# 사이를 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-147">Razor is designed for developer productivity, allowing the developer to switch between markup and C# in the same file with [IntelliSense](/visualstudio/ide/using-intellisense) support.</span></span> <span data-ttu-id="b8e0c-148">다음 태그는 Razor 파일(*DialogComponent.cshtml*)의 기본 사용자 지정 대화 상자 구성 요소의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-148">The following markup is an example of a basic custom dialog component in a Razor file (*DialogComponent.cshtml*):</span></span>

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

<span data-ttu-id="b8e0c-149">이 구성 요소를 앱의 다른 곳에서 사용할 경우 IntelliSense는 구문 및 매개 변수 완성을 통해 개발 속도를 높입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-149">When this component is used elsewhere in the app, IntelliSense speeds development with syntax and parameter completion.</span></span>

<span data-ttu-id="b8e0c-150">구성 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-150">Components can be:</span></span>

* <span data-ttu-id="b8e0c-151">중첩.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-151">Nested.</span></span>
* <span data-ttu-id="b8e0c-152">Razor(*\*.cshtml*) 또는 C#(*\*.cs*) 코드로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-152">Created with Razor (*\*.cshtml*) or C# (*\*.cs*) code.</span></span>
* <span data-ttu-id="b8e0c-153">클래스 라이브러리를 통해 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-153">Shared via class libraries.</span></span>
* <span data-ttu-id="b8e0c-154">브라우저 DOM을 요구하지 않는 단위 테스트.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-154">Unit tested without requiring a browser DOM.</span></span>

## <a name="infrastructure"></a><span data-ttu-id="b8e0c-155">인프라</span><span class="sxs-lookup"><span data-stu-id="b8e0c-155">Infrastructure</span></span>

<span data-ttu-id="b8e0c-156">Razor 구성 요소는 다음을 포함하여 대부분의 앱이 필요로 하는 핵심 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-156">Razor Components offers the core facilities that most apps require, including:</span></span>

* <span data-ttu-id="b8e0c-157">레이아웃</span><span class="sxs-lookup"><span data-stu-id="b8e0c-157">Layouts</span></span>
* <span data-ttu-id="b8e0c-158">라우팅</span><span class="sxs-lookup"><span data-stu-id="b8e0c-158">Routing</span></span>
* <span data-ttu-id="b8e0c-159">종속성 주입</span><span class="sxs-lookup"><span data-stu-id="b8e0c-159">Dependency injection</span></span>

<span data-ttu-id="b8e0c-160">이러한 기능은 모두 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-160">All of these features are optional.</span></span> <span data-ttu-id="b8e0c-161">이러한 기능 중 하나가 앱에서 사용되지 않는 경우 [IL(Intermediate Language) 링커](xref:host-and-deploy/razor-components/configure-linker)에서 게시하면 구현이 앱에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-161">When one of these features isn't used in an app, the implementation is stripped out of the app when published by the [Intermediate Language (IL) Linker](xref:host-and-deploy/razor-components/configure-linker).</span></span>

## <a name="code-sharing-and-net-standard"></a><span data-ttu-id="b8e0c-162">코드 공유 및 .NET Standard</span><span class="sxs-lookup"><span data-stu-id="b8e0c-162">Code sharing and .NET Standard</span></span>

<span data-ttu-id="b8e0c-163">앱은 기존 [.NET Standard](/dotnet/standard/net-standard) 라이브러리를 참조하고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-163">Apps can reference and use existing [.NET Standard](/dotnet/standard/net-standard) libraries.</span></span> <span data-ttu-id="b8e0c-164">.NET Standard는 .NET 구현에서 공통적인 .NET API의 공식 사양입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-164">.NET Standard is a formal specification of .NET APIs that are common across .NET implementations.</span></span> <span data-ttu-id="b8e0c-165">.NET Standard 2.0 이상이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-165">.NET Standard 2.0 or higher is supported.</span></span> <span data-ttu-id="b8e0c-166">웹 브라우저 내에서 적용되지 않는 API(예: 파일 시스템 액세스, 소켓 열기, 스레딩 및 기타 기능)에서 [PlatformNotSupportedException](/dotnet/api/system.platformnotsupportedexception)을 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-166">APIs that aren't applicable inside a web browser (for example, accessing the file system, opening a socket, threading, and other features) throw [PlatformNotSupportedException](/dotnet/api/system.platformnotsupportedexception).</span></span> <span data-ttu-id="b8e0c-167">.NET Standard 클래스 라이브러리는 서버 코드와 브라우저 기반 앱에서 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-167">.NET Standard class libraries can be shared across server code and in browser-based apps.</span></span>

## <a name="javascript-interop"></a><span data-ttu-id="b8e0c-168">JavaScript interop</span><span class="sxs-lookup"><span data-stu-id="b8e0c-168">JavaScript interop</span></span>

<span data-ttu-id="b8e0c-169">타사 JavaScript 라이브러리 및 브라우저 API를 필요로 하는 앱의 경우, WebAssembly는 JavaScript와 상호 운용하도록 디자인되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-169">For apps that require third-party JavaScript libraries and browser APIs, WebAssembly is designed to interoperate with JavaScript.</span></span> <span data-ttu-id="b8e0c-170">Razor 구성 요소는 JavaScript가 사용할 수 있는 모든 라이브러리 또는 API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-170">Razor Components are capable of using any library or API that JavaScript is able to use.</span></span> <span data-ttu-id="b8e0c-171">C# 코드는 JavaScript 코드로 호출할 수 있으며, JavaScript 코드는 C# 코드로 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-171">C# code can call into JavaScript code, and JavaScript code can call into C# code.</span></span> <span data-ttu-id="b8e0c-172">자세한 내용은 [JavaScript interop](xref:razor-components/javascript-interop)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-172">For more information, see [JavaScript interop](xref:razor-components/javascript-interop).</span></span>

## <a name="optimization"></a><span data-ttu-id="b8e0c-173">최적화</span><span class="sxs-lookup"><span data-stu-id="b8e0c-173">Optimization</span></span>

<span data-ttu-id="b8e0c-174">클라이언트 쪽 앱의 경우 페이로드 크기가 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-174">For client-side apps, payload size is critical.</span></span> <span data-ttu-id="b8e0c-175">Blazor는 페이로드 크기를 최적화하여 다운로드 시간을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-175">Blazor optimizes payload size to reduce download times.</span></span> <span data-ttu-id="b8e0c-176">예를 들어 .NET 어셈블리의 사용하지 않는 부분은 빌드 프로세스 중에 제거되고, HTTP 응답은 압축되며 .NET 런타임 및 어셈블리는 브라우저에 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-176">For example, unused parts of .NET assemblies are removed during the build process, HTTP responses are compressed, and the .NET runtime and assemblies are cached in the browser.</span></span>

<span data-ttu-id="b8e0c-177">Razor 구성 요소는 .NET 어셈블리, 앱의 어셈블리 및 런타임 서버 쪽을 유지 관리하여 Blazor보다 작은 페이로드 크기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-177">Razor Components provides an even smaller payload size than Blazor by maintaining .NET assemblies, the app's assembly, and the runtime server-side.</span></span> <span data-ttu-id="b8e0c-178">Razor 구성 요소 앱은 태그, 스크립트 및 스타일시트만 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-178">Razor Components apps only serve markup, script, and stylesheets to clients.</span></span>

## <a name="deployment"></a><span data-ttu-id="b8e0c-179">배포</span><span class="sxs-lookup"><span data-stu-id="b8e0c-179">Deployment</span></span>

<span data-ttu-id="b8e0c-180">Blazor를 사용하여 순수 독립 실행형 클라이언트 쪽 앱 또는 서버 및 클라이언트 앱이 모두 포함된 전체 스택 ASP.NET Core 앱을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-180">Use Blazor to build a pure standalone client-side app or a full-stack ASP.NET Core app that contains both server and client apps:</span></span>

* <span data-ttu-id="b8e0c-181">**독립 실행형 클라이언트 쪽 앱**에서 Blazor 앱은 정적 파일만 포함하는 *dist* 폴더로 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-181">In a **standalone client-side app**, the Blazor app is compiled into a *dist* folder that only contains static files.</span></span> <span data-ttu-id="b8e0c-182">Azure App Service, GitHub 페이지, IIS(정적 파일 서버로 구성), Node.js 서버 및 기타 여러 서버와 서비스에서 파일을 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-182">The files can be hosted on Azure App Service, GitHub Pages, IIS (configured as a static file server), Node.js servers, and many other servers and services.</span></span> <span data-ttu-id="b8e0c-183">프로덕션 환경에서는 서버에 .NET이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-183">.NET isn't required on the server in production.</span></span>
* <span data-ttu-id="b8e0c-184">**전체 스택 ASP.NET Core 앱**에서 서버와 클라이언트 앱 간에 코드를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-184">In a **full-stack ASP.NET Core app**, code can be shared between server and client apps.</span></span> <span data-ttu-id="b8e0c-185">클라이언트 쪽 UI 및 다른 서버 쪽 API 엔드포인트를 제공하는 결과 ASP.NET Core Razor 구성 요소 앱은 ASP.NET Core가 지원하는 모든 클라우드 또는 온-프레미스 호스트에 빌드 및 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-185">The resulting ASP.NET Core Razor Components app, which serves the client-side UI and other server-side API endpoints, can be built and deployed to any cloud or on-premise host supported by ASP.NET Core.</span></span>

## <a name="suggest-a-feature-or-file-a-bug-report"></a><span data-ttu-id="b8e0c-186">기능 또는 파일 버그 보고서 제안</span><span class="sxs-lookup"><span data-stu-id="b8e0c-186">Suggest a feature or file a bug report</span></span>

<span data-ttu-id="b8e0c-187">제안 및 파일 버그 보고서를 만들려면 [문제를 제기](https://github.com/aspnet/AspNetCore/issues/new)하세요.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-187">To make suggestions and file bug reports, please [open an issue](https://github.com/aspnet/AspNetCore/issues/new).</span></span> <span data-ttu-id="b8e0c-188">일반적인 도움말 및 커뮤니티에서 답변을 얻으려면 [Gitter](https://gitter.im/aspnet/Blazor)에 대한 대화에 참여합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e0c-188">For general help and to get answers from the community, join the conversation on [Gitter](https://gitter.im/aspnet/Blazor).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b8e0c-189">추가 자료</span><span class="sxs-lookup"><span data-stu-id="b8e0c-189">Additional resources</span></span>

* [<span data-ttu-id="b8e0c-190">WebAssembly</span><span class="sxs-lookup"><span data-stu-id="b8e0c-190">WebAssembly</span></span>](http://webassembly.org/)
* [<span data-ttu-id="b8e0c-191">C# 가이드</span><span class="sxs-lookup"><span data-stu-id="b8e0c-191">C# Guide</span></span>](/dotnet/csharp/)
* [<span data-ttu-id="b8e0c-192">Razor</span><span class="sxs-lookup"><span data-stu-id="b8e0c-192">Razor</span></span>](/aspnet/core/mvc/views/razor)
* [<span data-ttu-id="b8e0c-193">HTML</span><span class="sxs-lookup"><span data-stu-id="b8e0c-193">HTML</span></span>](https://www.w3.org/html/)
