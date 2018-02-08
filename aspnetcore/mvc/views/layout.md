---
title: "레이아웃"
author: ardalis
description: 
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/layout
ms.openlocfilehash: 3e9e5949d8940a33508e24f0da015b49b7ba468c
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="layout"></a>레이아웃

작성자: [Steve Smith](https://ardalis.com/)

뷰는 시각적 개체 및 프로그래밍 요소를 자주 공유합니다. 이 문서에서는 ASP.NET 앱에서 뷰를 렌더링하기 전에 일반적인 레이아웃을 사용하고, 지시문을 공유하며, 공용 코드를 실행하는 방법에 대해 알아봅니다.

## <a name="what-is-a-layout"></a>레이아웃이란

대부분의 웹앱에는 사용자가 페이지를 탐색하는 동안 일관된 환경을 제공하는 일반적인 레이아웃이 있습니다. 일반적으로 레이아웃에는 앱 헤더, 탐색 또는 메뉴 요소, 바닥글과 같은 공통 사용자 인터페이스 요소가 포함됩니다.

![페이지 레이아웃 예제](layout/_static/page-layout.png)

스크립트 및 스타일시트와 같은 공통 HTML 구조는 앱 내에서 여러 페이지에서도 자주 사용됩니다. 이러한 모든 공유 요소를 *레이아웃* 파일에 정의한 후 앱 내에 사용된 모든 뷰에서 참조할 수 있습니다. 레이아웃은 뷰에서 중복 코드를 줄여 [DRY(반복 금지) 원칙](http://deviq.com/don-t-repeat-yourself/)을 따르도록 도와줍니다.

규칙에 따라, ASP.NET 앱의 기본 레이아웃 이름을 `_Layout.cshtml`로 지정합니다. Visual Studio ASP.NET Core MVC 프로젝트 템플릿은 `Views/Shared` 폴더에 이 레이아웃 파일을 포함합니다.

![솔루션 탐색기의 뷰 폴더](layout/_static/web-project-views.png)

이 레이아웃은 앱의 뷰에 대한 최상위 수준 템플릿을 정의합니다. 앱에는 레이아웃이 필요하지 않으며, 앱은 다른 레이아웃을 지정하는 서로 다른 뷰를 포함하는 둘 이상의 레이아웃을 정의할 수 있습니다.

`_Layout.cshtml` 예:

[!code-html[Main](../../common/samples/WebApplication1/Views/Shared/_Layout.cshtml?highlight=42,66)]

## <a name="specifying-a-layout"></a>레이아웃 지정

Razor 뷰는 `Layout` 속성을 포함합니다. 이 속성을 설정하여 레이아웃을 지정하는 개별 뷰:

[!code-html[Main](../../common/samples/WebApplication1/Views/_ViewStart.cshtml?highlight=2)]

지정한 레이아웃은 전체 경로(예: `/Views/Shared/_Layout.cshtml`) 또는 부분 이름(예: `_Layout`)을 사용할 수 있습니다. 부분 이름이 제공되면 Razor 뷰 엔진이 표준 검색 프로세스를 사용하여 레이아웃 파일을 검색합니다. 컨트롤러 관련 폴더를 먼저 검색한 후 `Shared` 폴더를 검색합니다. 이 검색 프로세스는 [부분 뷰](partial.md)를 검색하는 데 사용된 것과 동일합니다.

기본적으로 모든 레이아웃에서 `RenderBody`를 호출해야 합니다. `RenderBody` 호출이 배치될 때마다 뷰의 내용이 렌더링됩니다.

<a name="layout-sections-label"></a>

### <a name="sections"></a>섹션

레이아웃은 `RenderSection`을 호출하여 필요에 따라 하나 이상의 *섹션*을 참조합니다. 섹션에서는 특정 페이지 요소를 배치할 위치를 구성하는 방법을 제공합니다. `RenderSection` 호출 때마다 섹션이 필수 또는 옵션인지 여부를 지정할 수 있습니다. 필수 섹션이 없는 경우 예외가 throw됩니다. 개별 뷰는 `@section` Razor 구문을 사용하여 섹션 내에 렌더링될 콘텐츠를 지정합니다. 뷰에서 섹션을 정의하는 경우 렌더링되어야 합니다(그렇지 않은 경우 오류 발생).

뷰에서 `@section` 정의 예:

```html
@section Scripts {
     <script type="text/javascript" src="/scripts/main.js"></script>
   }
   ```

위의 코드에서는 유효성 검사 스크립트가 양식을 포함하는 뷰의 `scripts` 섹션에 추가됩니다. 동일한 응용 프로그램의 다른 뷰에는 추가 스크립트가 필요하지 않을 수 있으므로 스크립트 섹션을 정의할 필요가 없습니다.

뷰에 정의된 섹션은 즉시 레이아웃 페이지에서만 사용할 수 있습니다. 이들은 부분 뷰, 뷰 구성 요소 또는 뷰 시스템의 다른 부분에서 참조할 수 없습니다.

### <a name="ignoring-sections"></a>섹션 무시

기본적으로 콘텐츠 페이지 본문 및 모든 섹션은 레이아웃 페이지에서 모두 렌더링되어야 합니다. Razor 뷰 엔진은 본문과 각 섹션이 렌더링되었는지 여부를 추적하여 이를 적용합니다.

뷰 엔진이 본문 또는 섹션을 무시하도록 지시하려면 `IgnoreBody` 및 `IgnoreSection` 메서드를 호출합니다.

Razor 페이지의 본문 및 모든 섹션은 렌더링되거나 무시되어야 합니다.

<a name="viewimports"></a>

## <a name="importing-shared-directives"></a>공유 지시문 가져오기

뷰는 Razor 지시문을 사용하여 네임스페이스 가져오기 또는 [종속성 주입](dependency-injection.md) 수행과 같은 많은 작업을 수행할 수 있습니다. 많은 뷰에서 공유된 지시문은 공용 `_ViewImports.cshtml` 파일에 지정할 수 있습니다. `_ViewImports` 파일은 다음 지시문을 지원합니다.

* `@addTagHelper`

* `@removeTagHelper`

* `@tagHelperPrefix`

* `@using`

* `@model`

* `@inherits`

* `@inject`

이 파일은 다른 Razor 기능(예: 함수 및 섹션 정의)을 지원하지 않습니다.

샘플 `_ViewImports.cshtml` 파일:

[!code-html[Main](../../common/samples/WebApplication1/Views/_ViewImports.cshtml)]

ASP.NET Core MVC 앱에 대한 `_ViewImports.cshtml` 파일은 일반적으로 `Views` 폴더에 배치됩니다. `_ViewImports.cshtml` 파일은 모든 폴더 내에 배치할 수 있으며, 이 경우 해당 폴더 및 해당 하위 폴더 내의 뷰에만 적용됩니다. `_ViewImports` 파일은 루트 수준에서부터 처리된 다음, 각 폴더에 대해 뷰 자체의 위치까지 처리되므로 루트 수준에서 지정된 설정이 폴더 수준에서 재정의될 수 있습니다.

예를 들어 루트 수준 `_ViewImports.cshtml` 파일이 `@model` 및 `@addTagHelper`를 지정하고, 뷰의 컨트롤러 관련 폴더에서 다른 `_ViewImports.cshtml` 파일이 다른 `@model`을 지정하며 다른 `@addTagHelper`를 추가하면, 뷰는 두 태그 도우미에 액세스할 수 있고 후자 `@model`을 사용합니다.

뷰에 대해 여러 `_ViewImports.cshtml` 파일이 실행되는 경우 `ViewImports.cshtml` 파일에 포함된 지시문의 결합된 동작은 다음과 같습니다.

* `@addTagHelper`, `@removeTagHelper`: 순서대로 모두 실행

* `@tagHelperPrefix`: 뷰에 가장 가까운 것이 다른 것보다 우선함

* `@model`: 뷰에 가장 가까운 것이 다른 것보다 우선함

* `@inherits`: 뷰에 가장 가까운 것이 다른 것보다 우선함

* `@using`: 모두 포함됨. 중복 항목은 무시됨

* `@inject`: 각 속성에 대해 뷰에 가장 가까운 것이 같은 속성 이름의 다른 것보다 우선함

<a name="viewstart"></a>

## <a name="running-code-before-each-view"></a>각 뷰 이전에 코드 실행

모든 뷰 이전에 실행해야 하는 코드가 있는 경우 `_ViewStart.cshtml` 파일에 배치해야 합니다. 규칙에 따라 `_ViewStart.cshtml` 파일은 `Views` 폴더에 있습니다. `_ViewStart.cshtml`에 나열된 문은 모든 전체 뷰(레이아웃 및 부분 뷰가 아님) 이전에 실행됩니다. [ViewImports.cshtml](xref:mvc/views/layout#viewimports)처럼 `_ViewStart.cshtml`은 계층적입니다. `_ViewStart.cshtml` 파일이 컨트롤러 관련 뷰 폴더에 정의된 경우 `Views` 폴더의 루트에 정의된 항목 뒤에 실행됩니다(있는 경우).

샘플 `_ViewStart.cshtml` 파일:

[!code-html[Main](../../common/samples/WebApplication1/Views/_ViewStart.cshtml)]

위의 파일은 모든 뷰가 `_Layout.cshtml` 레이아웃을 사용하도록 지정합니다.

> [!NOTE]
> 일반적으로 `_ViewStart.cshtml` 또는 `_ViewImports.cshtml`은 `/Views/Shared` 폴더에 배치되지 않습니다. 이러한 파일의 앱 수준 버전은 `/Views` 폴더에 직접 배치해야 합니다.
