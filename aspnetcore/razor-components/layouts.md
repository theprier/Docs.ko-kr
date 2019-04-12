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
# <a name="razor-components-layouts"></a>Razor 구성 요소 레이아웃

[Rainer Stropek](https://www.timecockpit.com)

앱은 일반적으로 둘 이상의 구성 요소를 포함 합니다. 메뉴, 저작권 메시지 및 로고와 같은 레이아웃 요소는 모든 구성 요소에 있어야 합니다. 이러한 레이아웃 요소의 코드를 앱의 구성 요소를 모두 복사 효율적이 지 않습니다. 이러한 중복을 유지 관리 하 고 아마도 시간에 따른 일관 되지 않은 콘텐츠에 이어집니다. *레이아웃* 이 문제를 해결 합니다.

기술적으로 레이아웃에는 다른 구성 요소입니다. Razor 템플릿 또는 레이아웃을 정의 된 C# 코드 및 포함 될 수 있습니다 [데이터 바인딩](xref:razor-components/components#data-binding)를 [종속성 주입](xref:razor-components/dependency-injection), 및 기타 일반 기능 구성 요소입니다.

설정 하는 두 가지 추가적인 측면을 *구성 요소* 에 *레이아웃*

* 레이아웃 구성 요소에서 상속 해야 `LayoutComponentBase`합니다. `LayoutComponentBase` 정의 `Body` 레이아웃 내에서 렌더링할 콘텐츠를 포함 하는 속성입니다.
* 레이아웃 구성 요소를 사용 합니다 `Body` 본문 콘텐츠에 표시 될 위치를 지정 하는 속성 Razor 구문을 사용 하 여 렌더링 `@Body`합니다. 렌더링 하는 동안 `@Body` 레이아웃의 내용으로 바뀝니다.

다음 코드 샘플에는 레이아웃 요소의 Razor 템플릿을 보여 줍니다. 사용 하 여 `LayoutComponentBase` 고 `@Body`:

[!code-cshtml[](layouts/sample_snapshot/3.x/MasterLayout.cshtml)]

## <a name="use-a-layout-in-a-component"></a>구성 요소에서 레이아웃을 사용 하 여

Razor 지시문을 사용 하 여 `@layout` 구성 요소에 레이아웃을 적용 합니다. 컴파일러는 변환에이 지시문을 `LayoutAttribute`, 구성 요소 클래스에 적용 되는 합니다.

다음 코드 예제에서는 개념을 보여 줍니다. 이 구성 요소의 내용이 삽입 됩니다 합니다 *MasterLayout* 의 위치에 `@Body`:

```cshtml
@layout MasterLayout
@page "/master-list"

<h2>Master Episode List</h2>
```

## <a name="centralized-layout-selection"></a>중앙 집중식된 레이아웃 선택

모든 폴더는 앱은 명명 된 템플릿 파일을 포함할 수도 있습니다 *_ViewImports.cshtml*합니다. 컴파일러는 동일한 폴더에서 Razor 템플릿 및 모든 하위 폴더에 재귀적으로 모든 뷰 가져오기 파일에 지정 된 지시문을 포함 합니다. 따라서를 *_ViewImports.cshtml* 포함 된 파일 `@layout MainLayout` 폴더를 사용 하는 구성 요소의 모든는 *MainLayout* 레이아웃 합니다. 반복적으로 추가할 필요가 없습니다 `@layout` 의 모든 항목에 *.razor* 파일입니다.

기본 템플릿을 사용 하는 참고 합니다 *_ViewImports.cshtml* 레이아웃을 선택 하기 위한 메커니즘입니다. 새로 만든된 앱을 포함 합니다 *_ViewImports.cshtml* 파일을 *구성 요소/페이지* 폴더입니다.

## <a name="nested-layouts"></a>중첩 된 레이아웃

중첩 된 레이아웃의 앱 구성 될 수 있습니다. 구성 요소에서 다른 레이아웃을 참조 하는 레이아웃을 참조할 수 있습니다. 예를 들어 중첩 레이아웃 다중 수준 메뉴 구조를 반영 하기 위해 사용할 수 있습니다.

다음 코드 샘플에는 중첩 된 레이아웃을 사용 하는 방법을 보여 줍니다. 합니다 *EpisodesComponent.cshtml* 파일은 표시할 구성 요소입니다. 구성 요소는 레이아웃을 참조 하는 참고 `MasterListLayout`합니다.

*EpisodesComponent.cshtml*:

```cshtml
@layout MasterListLayout
@page "/master-list/episodes"

<h1>Episodes</h1>
```

*MasterListLayout.cshtml* 파일은 제공 된 `MasterListLayout`합니다. 다른 레이아웃을 참조 하는 레이아웃 `MasterLayout`, 포함할 수 있는 것입니다.

*MasterListLayout.cshtml*:

```cshtml
@layout MasterLayout
@inherits LayoutComponentBase

<nav>
    <!-- Menu structure of master list -->
    ...
</nav>

@Body
```

마지막으로, `MasterLayout` 머리글, 바닥글 및 주 메뉴와 같은 최상위 레이아웃 요소를 포함 합니다.

*MasterLayout.cshtml*:

```cshtml
@inherits LayoutComponentBase

<header>...</header>
<nav>...</nav>

@Body
```
