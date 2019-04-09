---
title: ASP.NET Core의 Razor 구성 요소 소개
author: guardrex
description: ASP.NET Core 앱에서 .NET을 사용하여 대화형 클라이언트 쪽 웹 UI를 빌드하는 방법인 ASP.NET Core Razor 구성 요소를 살펴봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: seoapril2019
ms.date: 03/27/2019
uid: razor-components/index
ms.openlocfilehash: 43d5cf1d752b66a531c8d974deeb5a5fc8e94b43
ms.sourcegitcommit: 1a7000630e55da90da19b284e1b2f2f13a393d74
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2019
ms.locfileid: "59012658"
---
# <a name="introduction-to-razor-components"></a><span data-ttu-id="5ffd5-103">Razor 구성 요소 소개</span><span class="sxs-lookup"><span data-stu-id="5ffd5-103">Introduction to Razor Components</span></span>

<span data-ttu-id="5ffd5-104">작성자: [Daniel Roth](https://github.com/danroth27) 및 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="5ffd5-104">By [Daniel Roth](https://github.com/danroth27) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="5ffd5-105">.NET을 사용하여 대화형 클라이언트 쪽 웹 UI를 빌드하기 위해 ASP.NET Core 3.0(미리 보기)에서 제공된 *Razor 구성 요소*를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-105">*Razor Components*, introduced in ASP.NET Core 3.0 (Preview), is a way to build interactive client-side web UI with .NET:</span></span>

* <span data-ttu-id="5ffd5-106">JavaScript 대신 C#을 사용하여 풍부한 대화형 UI를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-106">Build rich interactive UIs using C# instead of JavaScript.</span></span>
* <span data-ttu-id="5ffd5-107">모두 .NET으로 작성된 서버 쪽 및 클라이언트 쪽 앱을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-107">Share server-side and client-side app logic all written with .NET.</span></span>
* <span data-ttu-id="5ffd5-108">모바일 브라우저를 포함한 광범위한 브라우저 지원을 위해 UI를 HTML 및 CSS로 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-108">Render the UI as HTML and CSS for wide browser support, including mobile browsers.</span></span>

<span data-ttu-id="5ffd5-109">Razor 구성 요소는 다음을 포함한 대부분의 앱에 필요한 핵심 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-109">Razor Components supports core facilities required by most apps, including:</span></span>

* <span data-ttu-id="5ffd5-110">매개 변수</span><span class="sxs-lookup"><span data-stu-id="5ffd5-110">Parameters</span></span>
* <span data-ttu-id="5ffd5-111">이벤트 처리</span><span class="sxs-lookup"><span data-stu-id="5ffd5-111">Event handling</span></span>
* <span data-ttu-id="5ffd5-112">데이터 바인딩</span><span class="sxs-lookup"><span data-stu-id="5ffd5-112">Data binding</span></span>
* <span data-ttu-id="5ffd5-113">라우팅</span><span class="sxs-lookup"><span data-stu-id="5ffd5-113">Routing</span></span>
* <span data-ttu-id="5ffd5-114">종속성 주입</span><span class="sxs-lookup"><span data-stu-id="5ffd5-114">Dependency injection</span></span>
* <span data-ttu-id="5ffd5-115">레이아웃</span><span class="sxs-lookup"><span data-stu-id="5ffd5-115">Layouts</span></span>
* <span data-ttu-id="5ffd5-116">템플릿</span><span class="sxs-lookup"><span data-stu-id="5ffd5-116">Templating</span></span>
* <span data-ttu-id="5ffd5-117">연계 값</span><span class="sxs-lookup"><span data-stu-id="5ffd5-117">Cascading values</span></span>

<span data-ttu-id="5ffd5-118">Razor 구성 요소는 UI 업데이트 적용 방법에서 구성 요소 렌더링 논리를 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-118">Razor Components decouples component rendering logic from how UI updates are applied.</span></span> <span data-ttu-id="5ffd5-119">.NET Core 3.0의 ASP.NET Core Razor 구성 요소는 ASP.NET Core 앱의 서버에서 Razor 구성 요소를 호스트하는 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-119">ASP.NET Core Razor Components in .NET Core 3.0 adds support for hosting Razor Components on the server in an ASP.NET Core app.</span></span> <span data-ttu-id="5ffd5-120">UI 업데이트는 SignalR 연결을 통해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-120">UI updates are handled over a SignalR connection.</span></span>

<span data-ttu-id="5ffd5-121">런타임이 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-121">The runtime:</span></span>

* <span data-ttu-id="5ffd5-122">브라우저에서 서버로 UI 이벤트 보내기를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-122">Handles sending UI events from the browser to the server.</span></span>
* <span data-ttu-id="5ffd5-123">구성 요소를 실행한 후 서버가 보낸 UI 업데이트를 다시 브라우저에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-123">Applies UI updates sent by the server back to the browser after running the components.</span></span>

<span data-ttu-id="5ffd5-124">Razor 구성 요소가 브라우저와 통신하는 데 사용하는 연결은 JavaScript interop 호출을 처리하는 데도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-124">The connection used by Razor Components to communicate with the browser is also used to handle JavaScript interop calls.</span></span>

![Razor 구성 요소는 서버에서 .NET 코드를 실행하고 SignalR 연결을 통해 클라이언트의 문서 개체 모델과 상호 작용합니다.](index/_static/aspnet-core-razor-components.png)

<span data-ttu-id="5ffd5-126">자세한 내용은 <xref:razor-components/hosting-models#server-side-hosting-model>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-126">For more information, see <xref:razor-components/hosting-models#server-side-hosting-model>.</span></span>

<span data-ttu-id="5ffd5-127">*Blazor*는 Razor 구성 요소의 실험적 클라이언트 쪽 호스팅 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-127">*Blazor* is the experimental client-side hosting model of Razor Components.</span></span> <span data-ttu-id="5ffd5-128">Blazor는 플러그 인이나 코드 소스 간 컴파일 없이 개방형 웹 표준을 사용하여 브라우저의 .NET에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-128">Blazor runs on .NET in the browser using open web standards without plugins or code transpilation.</span></span> <span data-ttu-id="5ffd5-129">자세한 내용은 <xref:spa/blazor/index> 및 <xref:razor-components/hosting-models#client-side-hosting-model>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-129">For more information, see <xref:spa/blazor/index> and <xref:razor-components/hosting-models#client-side-hosting-model>.</span></span>

## <a name="components"></a><span data-ttu-id="5ffd5-130">구성 요소</span><span class="sxs-lookup"><span data-stu-id="5ffd5-130">Components</span></span>

<span data-ttu-id="5ffd5-131">‘Razor 구성 요소’는 페이지, 대화 상자 또는 데이터 입력 양식과 같은 UI의 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-131">A *Razor Component* is a piece of UI, such as a page, dialog, or data entry form.</span></span> <span data-ttu-id="5ffd5-132">구성 요소는 사용자 이벤트를 처리하고 유연한 UI 렌더링 논리를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-132">Components handle user events and define flexible UI rendering logic.</span></span> <span data-ttu-id="5ffd5-133">구성 요소는 중첩 및 재사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-133">Components can be nested and reused.</span></span>

<span data-ttu-id="5ffd5-134">구성 요소는 NuGet 패키지로 공유 및 배포될 수 있는 .NET 어셈블리에 기본 제공된 .NET 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-134">Components are .NET classes built into .NET assemblies that can be shared and distributed as NuGet packages.</span></span> <span data-ttu-id="5ffd5-135">클래스는 일반적으로 *.razor* 파일 확장자를 가진 Razor 태그 페이지 형식으로 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-135">The class is normally written in the form of a Razor markup page with a *.razor* file extension.</span></span>

<span data-ttu-id="5ffd5-136">[Razor](xref:mvc/views/razor)는 HTML 태그와 C# 코드를 결합하는 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-136">[Razor](xref:mvc/views/razor) is a syntax for combining HTML markup with C# code.</span></span> <span data-ttu-id="5ffd5-137">Razor는 개발자 생산성을 위해 설계되었으며, 개발자는 [IntelliSense](/visualstudio/ide/using-intellisense) 지원으로 동일한 파일에서 태그와 C# 사이를 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-137">Razor is designed for developer productivity, allowing the developer to switch between markup and C# in the same file with [IntelliSense](/visualstudio/ide/using-intellisense) support.</span></span> <span data-ttu-id="5ffd5-138">Razor Pages 및 MVC 뷰에도 Razor를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-138">Razor Pages and MVC views also use Razor.</span></span> <span data-ttu-id="5ffd5-139">요청/응답 모델을 중심으로 빌드된 Razor Pages 및 MVC 뷰와는 달리, 구성 요소는 특별히 UI 컴퍼지션을 처리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-139">Unlike Razor Pages and MVC views, which are built around a request/response model, components are used specifically for handling UI composition.</span></span> <span data-ttu-id="5ffd5-140">Razor 구성 요소는 특별히 클라이언트 쪽 UI 논리 및 컴퍼지션에 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-140">Razor Components can be used specifically for client-side UI logic and composition.</span></span>

<span data-ttu-id="5ffd5-141">다음 태그는 Razor 파일(*DialogComponent.razor*)의 사용자 지정 대화 상자 구성 요소의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-141">The following markup is an example of a custom dialog component in a Razor file (*DialogComponent.razor*):</span></span>

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

<span data-ttu-id="5ffd5-142">이 구성 요소를 앱의 다른 곳에서 사용할 경우 IntelliSense는 구문 및 매개 변수 완성을 통해 개발 속도를 높입니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-142">When this component is used elsewhere in the app, IntelliSense speeds development with syntax and parameter completion.</span></span>

<span data-ttu-id="5ffd5-143">구성 요소는 유연하고 효율적인 방법으로 UI를 업데이트하는 데 사용할 수 있는 ‘렌더링 트리’라는 브라우저 DOM의 메모리 내 표시로 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-143">Components render into an in-memory representation of the browser DOM called a *render tree* that can then be used to update the UI in a flexible and efficient way.</span></span>

## <a name="javascript-interop"></a><span data-ttu-id="5ffd5-144">JavaScript interop</span><span class="sxs-lookup"><span data-stu-id="5ffd5-144">JavaScript interop</span></span>

<span data-ttu-id="5ffd5-145">타사 JavaScript 라이브러리 및 브라우저 API를 필요로 하는 앱의 경우 구성 요소는 JavaScript와 상호 운용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-145">For apps that require third-party JavaScript libraries and browser APIs, components interoperate with JavaScript.</span></span> <span data-ttu-id="5ffd5-146">구성 요소는 JavaScript가 사용할 수 있는 모든 라이브러리 또는 API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-146">Components are capable of using any library or API that JavaScript is able to use.</span></span> <span data-ttu-id="5ffd5-147">C# 코드는 JavaScript 코드로 호출할 수 있으며, JavaScript 코드는 C# 코드로 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-147">C# code can call into JavaScript code, and JavaScript code can call into C# code.</span></span> <span data-ttu-id="5ffd5-148">자세한 내용은 [JavaScript interop](xref:razor-components/javascript-interop)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ffd5-148">For more information, see [JavaScript interop](xref:razor-components/javascript-interop).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5ffd5-149">추가 자료</span><span class="sxs-lookup"><span data-stu-id="5ffd5-149">Additional resources</span></span>

* <xref:spa/blazor/index>
* [<span data-ttu-id="5ffd5-150">WebAssembly</span><span class="sxs-lookup"><span data-stu-id="5ffd5-150">WebAssembly</span></span>](http://webassembly.org/)
* [<span data-ttu-id="5ffd5-151">C# 가이드</span><span class="sxs-lookup"><span data-stu-id="5ffd5-151">C# Guide</span></span>](/dotnet/csharp/)
* <xref:mvc/views/razor>
* [<span data-ttu-id="5ffd5-152">HTML</span><span class="sxs-lookup"><span data-stu-id="5ffd5-152">HTML</span></span>](https://www.w3.org/html/)
