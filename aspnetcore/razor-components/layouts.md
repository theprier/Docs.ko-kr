---
title: Razor 구성 요소 레이아웃
author: guardrex
description: Razor 구성 요소 앱에 대 한 재사용 가능한 레이아웃 구성 요소를 만드는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 04/07/2019
uid: razor-components/layouts
ms.openlocfilehash: 31ed940ce40e3ae6e3744418cf241d396308f4fe
ms.sourcegitcommit: 6bde1fdf686326c080a7518a6725e56e56d8886e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59515646"
---
# <a name="razor-components-layouts"></a><span data-ttu-id="1af37-103">Razor 구성 요소 레이아웃</span><span class="sxs-lookup"><span data-stu-id="1af37-103">Razor Components layouts</span></span>

<span data-ttu-id="1af37-104">[Rainer Stropek](https://www.timecockpit.com)</span><span class="sxs-lookup"><span data-stu-id="1af37-104">By [Rainer Stropek](https://www.timecockpit.com)</span></span>

<span data-ttu-id="1af37-105">앱은 일반적으로 둘 이상의 구성 요소를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-105">Apps typically contain more than one component.</span></span> <span data-ttu-id="1af37-106">메뉴, 저작권 메시지 및 로고와 같은 레이아웃 요소는 모든 구성 요소에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-106">Layout elements, such as menus, copyright messages, and logos, must be present on all components.</span></span> <span data-ttu-id="1af37-107">이러한 레이아웃 요소의 코드를 앱의 구성 요소를 모두 복사 효율적이 지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-107">Copying the code of these layout elements into all of the components of an app isn't an efficient approach.</span></span> <span data-ttu-id="1af37-108">이러한 중복을 유지 관리 하 고 아마도 시간에 따른 일관 되지 않은 콘텐츠에 이어집니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-108">Such duplication is hard to maintain and probably leads to inconsistent content over time.</span></span> <span data-ttu-id="1af37-109">*레이아웃* 이 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-109">*Layouts* solve this problem.</span></span>

<span data-ttu-id="1af37-110">기술적으로 레이아웃에는 다른 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-110">Technically, a layout is just another component.</span></span> <span data-ttu-id="1af37-111">Razor 템플릿 또는 레이아웃을 정의 된 C# 코드 및 포함 될 수 있습니다 [데이터 바인딩](xref:razor-components/components#data-binding)를 [종속성 주입](xref:razor-components/dependency-injection), 및 기타 일반 기능 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-111">A layout is defined in a Razor template or in C# code and can contain [data binding](xref:razor-components/components#data-binding), [dependency injection](xref:razor-components/dependency-injection), and other ordinary features of components.</span></span>

<span data-ttu-id="1af37-112">설정 하는 두 가지 추가적인 측면을 *구성 요소* 에 *레이아웃*</span><span class="sxs-lookup"><span data-stu-id="1af37-112">Two additional aspects turn a *component* into a *layout*</span></span>

* <span data-ttu-id="1af37-113">레이아웃 구성 요소에서 상속 해야 `LayoutComponentBase`합니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-113">The layout component must inherit from `LayoutComponentBase`.</span></span> `LayoutComponentBase` <span data-ttu-id="1af37-114">정의 `Body` 레이아웃 내에서 렌더링할 콘텐츠를 포함 하는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-114">defines a `Body` property that contains the content to be rendered inside the layout.</span></span>
* <span data-ttu-id="1af37-115">레이아웃 구성 요소를 사용 합니다 `Body` 본문 콘텐츠에 표시 될 위치를 지정 하는 속성 Razor 구문을 사용 하 여 렌더링 `@Body`합니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-115">The layout component uses the `Body` property to specify where the body content should be rendered using the Razor syntax `@Body`.</span></span> <span data-ttu-id="1af37-116">렌더링 하는 동안 `@Body` 레이아웃의 내용으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-116">During rendering, `@Body` is replaced by the content of the layout.</span></span>

<span data-ttu-id="1af37-117">다음 코드 샘플에는 레이아웃 요소의 Razor 템플릿을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-117">The following code sample shows the Razor template of a layout component.</span></span> <span data-ttu-id="1af37-118">사용 하 여 `LayoutComponentBase` 고 `@Body`:</span><span class="sxs-lookup"><span data-stu-id="1af37-118">Note the use of `LayoutComponentBase` and `@Body`:</span></span>

[!code-cshtml[](layouts/sample_snapshot/3.x/MasterLayout.cshtml)]

## <a name="use-a-layout-in-a-component"></a><span data-ttu-id="1af37-119">구성 요소에서 레이아웃을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="1af37-119">Use a layout in a component</span></span>

<span data-ttu-id="1af37-120">Razor 지시문을 사용 하 여 `@layout` 구성 요소에 레이아웃을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-120">Use the Razor directive `@layout` to apply a layout to a component.</span></span> <span data-ttu-id="1af37-121">컴파일러는 변환에이 지시문을 `LayoutAttribute`, 구성 요소 클래스에 적용 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-121">The compiler converts this directive into a `LayoutAttribute`, which is applied to the component class.</span></span>

<span data-ttu-id="1af37-122">다음 코드 예제에서는 개념을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-122">The following code sample demonstrates the concept.</span></span> <span data-ttu-id="1af37-123">이 구성 요소의 내용이 삽입 됩니다 합니다 *MasterLayout* 의 위치에 `@Body`:</span><span class="sxs-lookup"><span data-stu-id="1af37-123">The content of this component is inserted into the *MasterLayout* at the position of `@Body`:</span></span>

```cshtml
@layout MasterLayout
@page "/master-list"

<h2>Master Episode List</h2>
```

## <a name="centralized-layout-selection"></a><span data-ttu-id="1af37-124">중앙 집중식된 레이아웃 선택</span><span class="sxs-lookup"><span data-stu-id="1af37-124">Centralized layout selection</span></span>

<span data-ttu-id="1af37-125">모든 폴더는 앱은 명명 된 템플릿 파일을 포함할 수도 있습니다 *_ViewImports.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-125">Every folder of a an app can optionally contain a template file named *_ViewImports.cshtml*.</span></span> <span data-ttu-id="1af37-126">컴파일러는 동일한 폴더에서 Razor 템플릿 및 모든 하위 폴더에 재귀적으로 모든 뷰 가져오기 파일에 지정 된 지시문을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-126">The compiler includes the directives specified in the view imports file in all of the Razor templates in the same folder and recursively in all of its subfolders.</span></span> <span data-ttu-id="1af37-127">따라서를 *_ViewImports.cshtml* 포함 된 파일 `@layout MainLayout` 폴더를 사용 하는 구성 요소의 모든는 *MainLayout* 레이아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-127">Therefore, a *_ViewImports.cshtml* file containing `@layout MainLayout` ensures that all of the components in a folder use the *MainLayout* layout.</span></span> <span data-ttu-id="1af37-128">반복적으로 추가할 필요가 없습니다 `@layout` 의 모든 항목에 *.razor* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-128">There's no need to repeatedly add `@layout` to all of the *.razor* files.</span></span>

<span data-ttu-id="1af37-129">기본 템플릿을 사용 하는 참고 합니다 *_ViewImports.cshtml* 레이아웃을 선택 하기 위한 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-129">Note that the default template uses the *_ViewImports.cshtml* mechanism for layout selection.</span></span> <span data-ttu-id="1af37-130">새로 만든된 앱을 포함 합니다 *_ViewImports.cshtml* 파일을 *구성 요소/페이지* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-130">A newly created app contains the *_ViewImports.cshtml* file in the *Components/Pages* folder.</span></span>

## <a name="nested-layouts"></a><span data-ttu-id="1af37-131">중첩 된 레이아웃</span><span class="sxs-lookup"><span data-stu-id="1af37-131">Nested layouts</span></span>

<span data-ttu-id="1af37-132">중첩 된 레이아웃의 앱 구성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-132">Apps can consist of nested layouts.</span></span> <span data-ttu-id="1af37-133">구성 요소에서 다른 레이아웃을 참조 하는 레이아웃을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-133">A component can reference a layout which in turn references another layout.</span></span> <span data-ttu-id="1af37-134">예를 들어 중첩 레이아웃 다중 수준 메뉴 구조를 반영 하기 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-134">For example, nesting layouts can be used to reflect a multi-level menu structure.</span></span>

<span data-ttu-id="1af37-135">다음 코드 샘플에는 중첩 된 레이아웃을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-135">The following code samples show how to use nested layouts.</span></span> <span data-ttu-id="1af37-136">합니다 *EpisodesComponent.cshtml* 파일은 표시할 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-136">The *EpisodesComponent.cshtml* file is the component to display.</span></span> <span data-ttu-id="1af37-137">구성 요소는 레이아웃을 참조 하는 참고 `MasterListLayout`합니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-137">Note that the component references the layout `MasterListLayout`.</span></span>

<span data-ttu-id="1af37-138">*EpisodesComponent.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="1af37-138">*EpisodesComponent.cshtml*:</span></span>

```cshtml
@layout MasterListLayout
@page "/master-list/episodes"

<h1>Episodes</h1>
```

<span data-ttu-id="1af37-139">*MasterListLayout.cshtml* 파일은 제공 된 `MasterListLayout`합니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-139">The *MasterListLayout.cshtml* file provides the `MasterListLayout`.</span></span> <span data-ttu-id="1af37-140">다른 레이아웃을 참조 하는 레이아웃 `MasterLayout`, 포함할 수 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-140">The layout references another layout, `MasterLayout`, where it's going to be embedded.</span></span>

<span data-ttu-id="1af37-141">*MasterListLayout.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="1af37-141">*MasterListLayout.cshtml*:</span></span>

```cshtml
@layout MasterLayout
@inherits LayoutComponentBase

<nav>
    <!-- Menu structure of master list -->
    ...
</nav>

@Body
```

<span data-ttu-id="1af37-142">마지막으로, `MasterLayout` 머리글, 바닥글 및 주 메뉴와 같은 최상위 레이아웃 요소를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1af37-142">Finally, `MasterLayout` contains the top-level layout elements, such as the header, footer, and main menu.</span></span>

<span data-ttu-id="1af37-143">*MasterLayout.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="1af37-143">*MasterLayout.cshtml*:</span></span>

```cshtml
@inherits LayoutComponentBase

<header>...</header>
<nav>...</nav>

@Body
```
