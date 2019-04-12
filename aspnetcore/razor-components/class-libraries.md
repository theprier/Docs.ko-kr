---
title: Razor 구성 요소 클래스 라이브러리
author: guardrex
description: 외부 구성 요소 라이브러리에서 구성 요소 Razor 앱에 구성 요소를 포함할 수 있습니다 하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 03/14/2019
uid: razor-components/class-libraries
ms.openlocfilehash: 1064ad60d90af15af483ba9bca5ed85fb63c2924
ms.sourcegitcommit: 10e14b85490f064395e9b2f423d21e3c2d39ed8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2019
ms.locfileid: "59515589"
---
# <a name="razor-components-class-libraries"></a><span data-ttu-id="08f78-103">Razor 구성 요소 클래스 라이브러리</span><span class="sxs-lookup"><span data-stu-id="08f78-103">Razor Components Class Libraries</span></span>

<span data-ttu-id="08f78-104">[Simon Timms](https://github.com/stimms)</span><span class="sxs-lookup"><span data-stu-id="08f78-104">By [Simon Timms](https://github.com/stimms)</span></span>

<span data-ttu-id="08f78-105">구성 요소는 Razor 클래스 라이브러리의 프로젝트 간에 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08f78-105">Components can be shared in Razor class libraries across projects.</span></span> <span data-ttu-id="08f78-106">구성 요소를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08f78-106">Components can be included from:</span></span>

* <span data-ttu-id="08f78-107">솔루션의 다른 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="08f78-107">Another project in the solution.</span></span>
* <span data-ttu-id="08f78-108">NuGet 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="08f78-108">A NuGet package.</span></span>
* <span data-ttu-id="08f78-109">참조 된.NET 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="08f78-109">A referenced .NET library.</span></span>

<span data-ttu-id="08f78-110">구성 요소는 일반.NET 형식 처럼 Razor 클래스 라이브러리에서 제공 하는 구성 요소는 일반.NET 어셈블리입니다.</span><span class="sxs-lookup"><span data-stu-id="08f78-110">Just as components are regular .NET types, components provided by Razor class libraries are normal .NET assemblies.</span></span>

<span data-ttu-id="08f78-111">사용 된 `razorclasslib` (Razor 클래스 라이브러리) 템플릿을 사용 하 여 합니다 [새 dotnet](/dotnet/core/tools/dotnet-new) 명령:</span><span class="sxs-lookup"><span data-stu-id="08f78-111">Use the `razorclasslib` (Razor class library) template with the [dotnet new](/dotnet/core/tools/dotnet-new) command:</span></span>

```console
dotnet new razorclasslib -o MyComponentLib1
```

<span data-ttu-id="08f78-112">추가 구성 요소 Razor 파일 (*.razor*)는 Razor 클래스 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="08f78-112">Add Razor Component files (*.razor*) to the Razor class library.</span></span>

<span data-ttu-id="08f78-113">기존 프로젝트에 라이브러리를 추가 하려면 사용 합니다 [dotnet sln](/dotnet/core/tools/dotnet-sln) 명령:</span><span class="sxs-lookup"><span data-stu-id="08f78-113">To add the library to an existing project, use the [dotnet sln](/dotnet/core/tools/dotnet-sln) command:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="08f78-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="08f78-114">Visual Studio</span></span>](#tab/visual-studio)

```console
dotnet sln add .\MyComponentLib1
```

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="08f78-115">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="08f78-115">.NET Core CLI</span></span>](#tab/netcore-cli)

```console
dotnet add WebApplication1 reference MyComponentLib1
```

---

> [!NOTE]
> <span data-ttu-id="08f78-116">Razor 클래스 라이브러리는 ASP.NET Core 미리 보기 3에서 Blazor 앱과 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="08f78-116">Razor class libraries aren't compatible with Blazor apps in ASP.NET Core Preview 3.</span></span>
>
> <span data-ttu-id="08f78-117">만들어진 Blazor 클래스 라이브러리를 사용 하 여 Blazor 및 Razor 구성 요소 앱과 공유할 수 있는 라이브러리의 구성 요소를 만들려면는 `blazorlib` 템플릿.</span><span class="sxs-lookup"><span data-stu-id="08f78-117">To create components in a library that can be shared with Blazor and Razor Components apps, use a Blazor class library created by the `blazorlib` template.</span></span>
>
> <span data-ttu-id="08f78-118">Razor 클래스 라이브러리는 ASP.NET Core 미리 보기 3의 정적 자산을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="08f78-118">Razor class libraries don't support static assets in ASP.NET Core Preview 3.</span></span> <span data-ttu-id="08f78-119">구성 요소 라이브러리를 사용 하 여 `blazorlib` 템플릿 이미지, JavaScript 및 스타일 시트 같은 정적 파일을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08f78-119">Component libraries using the `blazorlib` template can include static files, such as images, JavaScript, and stylesheets.</span></span> <span data-ttu-id="08f78-120">빌드 시 정적 파일은 빌드된 어셈블리 파일에 포함 됩니다 (*.dll*), 해당 리소스를 포함 하는 방법에 걱정할 필요 없이 구성 요소 사용을 허용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f78-120">At build time, static files are embedded into the built assembly file (*.dll*), which allows consumption of the components without having to worry about how to include their resources.</span></span> <span data-ttu-id="08f78-121">에 포함 된 모든 파일을 `content` 디렉터리 포함 리소스로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08f78-121">Any files included in the `content` directory are marked as an embedded resource.</span></span>

## <a name="consume-a-library-component"></a><span data-ttu-id="08f78-122">라이브러리 구성 요소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f78-122">Consume a library component</span></span>

<span data-ttu-id="08f78-123">다른 프로젝트에 라이브러리에 정의 된 구성 요소를 사용 하기 위해 합니다 [ @addTagHelper ](xref:mvc/views/tag-helpers/intro#add-helper-label) 지시문을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f78-123">In order to consume components defined in a library in another project, the [@addTagHelper](xref:mvc/views/tag-helpers/intro#add-helper-label) directive must be used.</span></span> <span data-ttu-id="08f78-124">개별 구성 요소 이름으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08f78-124">Individual components may be added by name.</span></span>

<span data-ttu-id="08f78-125">지시문의 일반 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="08f78-125">The general format of the directive is:</span></span>

```cshtml
@addTagHelper MyComponentLib1.Component1, MyComponentLib1

<h1>Hello, world!</h1>

Welcome to your new app.

<Component1 />
```

<span data-ttu-id="08f78-126">예를 들어 다음 지시문 추가 `Component1` 의 `MyComponentLib1`:</span><span class="sxs-lookup"><span data-stu-id="08f78-126">For example, the following directive adds `Component1` of `MyComponentLib1`:</span></span>

```cshtml
@addTagHelper MyComponentLib1.Component1, MyComponentLib1
```

<span data-ttu-id="08f78-127">그러나는 것이 일반적 모든 와일드 카드를 사용 하 여 어셈블리에서 구성 요소를 포함 하도록 (`*`):</span><span class="sxs-lookup"><span data-stu-id="08f78-127">However, it's common to include all of the components from an assembly using a wildcard (`*`):</span></span>

```cshtml
@addTagHelper *, MyComponentLib1
```

<span data-ttu-id="08f78-128">합니다 `@addTagHelper` 지시문에 포함할 수 있습니다 *_ViewImport.cshtml* 단일 페이지 또는 폴더 내의 페이지 집합에 적용 된 또는 전체 프로젝트에 사용할 수 있는 구성 요소를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f78-128">The `@addTagHelper` directive can be included in *_ViewImport.cshtml* to make the components available for an entire project or applied to a single page or set of pages within a folder.</span></span> <span data-ttu-id="08f78-129">사용 하 여는 `@addTagHelper` 지시문 내부에 구성 요소 라이브러리의 구성 요소 사용 될 수 있습니다 앱과 동일한 어셈블리에 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f78-129">With the `@addTagHelper` directive in place, the components of the component library can be consumed as if they were in the same assembly as the app.</span></span>

## <a name="build-pack-and-ship-to-nuget"></a><span data-ttu-id="08f78-130">빌드, 팩 및 NuGet에 배송</span><span class="sxs-lookup"><span data-stu-id="08f78-130">Build, pack, and ship to NuGet</span></span>

<span data-ttu-id="08f78-131">구성 요소 라이브러리는 표준.NET 라이브러리 이기 때문에 패키징 및 NuGet에 패키징 및 nuget 라이브러리 전달 다르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="08f78-131">Because component libraries are standard .NET libraries, packaging and shipping them to NuGet is no different from packaging and shipping any library to NuGet.</span></span> <span data-ttu-id="08f78-132">패키징을 사용 하 여 수행 되는 [dotnet 팩](/dotnet/core/tools/dotnet-pack) 명령:</span><span class="sxs-lookup"><span data-stu-id="08f78-132">Packaging is performed using the [dotnet pack](/dotnet/core/tools/dotnet-pack) command:</span></span>

```console
dotnet pack
```

<span data-ttu-id="08f78-133">사용 하는 NuGet 패키지를 업로드 합니다 [dotnet nuget](/dotnet/core/tools/dotnet-nuget-push) 명령:</span><span class="sxs-lookup"><span data-stu-id="08f78-133">Upload the package to NuGet using the [dotnet nuget publish](/dotnet/core/tools/dotnet-nuget-push) command:</span></span>

```console
dotnet nuget publish
```

<span data-ttu-id="08f78-134">사용 하는 경우는 `blazorlib` 템플릿, 정적 리소스는 NuGet 패키지에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08f78-134">When using the `blazorlib` template, static resources are included in the NuGet package.</span></span> <span data-ttu-id="08f78-135">라이브러리 소비자에 게 자동으로 수신 스크립트 및 스타일 시트 되므로 소비자가 리소스를 수동으로 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="08f78-135">Library consumers automatically receive scripts and stylesheets, so consumers aren't required to manually install the resources.</span></span>
