---
title: "부분 보기"
author: ardalis
description: "ASP.NET Core MVC에서 부분 보기 사용"
manager: wpickett
ms.author: riande
ms.date: 03/14/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/partial
ms.openlocfilehash: 169948e5d7dc8068463ed61114666148b785b217
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="partial-views"></a>부분 보기

작성자: [Steve Smith](https://ardalis.com/), [Maher JENDOUBI](https://twitter.com/maherjend) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)

ASP.NET Core MVC는 부분 보기를 지원합니다. 이 기능은 웹 페이지의 재사용 가능한 부분을 다른 보기에서 공유하려는 경우에 유용합니다.

[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/partial/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="what-are-partial-views"></a>부분 보기란?

부분 보기는 다른 보기 내에서 렌더링되는 보기입니다. 부분 보기를 실행하여 생성된 HTML 출력을 호출 (또는 부모) 보기에 렌더링합니다. 보기와 같이 부분 보기는 *.cshtml* 파일 확장명을 사용합니다.

## <a name="when-should-i-use-partial-views"></a>어떤 경우에 부분 보기를 사용해야 하나요?

부분 보기를 통해 큰 보기를 더 작은 구성 요소로 효과적으로 분리할 수 있습니다. 콘텐츠 보기의 중복을 줄이고 보기 요소를 다시 사용할 수 있습니다. 일반 레이아웃 요소는 [_Layout.cshtml](layout.md)에서 지정해야 합니다. 레이아웃이 아닌 다시 사용 가능한 콘텐츠는 부분 보기로 캡슐화될 수 있습니다.

논리 조각으로 구성된 복잡 한 페이지를 사용하는 경우 고유한 부분 보기로 각 부분을 작업하는 것이 유용할 수 있습니다. 페이지의 나머지 부분과 분리에서 페이지의 각 부분을 볼 수 있습니다. 페이지 자체에 대한 보기가 전체 페이지 구조 호출을 포함하여 부분 보기를 렌더링하므로 훨씬 더 간단합니다.

팁: 보기에서 [반복 금지 원칙](http://deviq.com/don-t-repeat-yourself/)을 따릅니다.

## <a name="declaring-partial-views"></a>부분 보기 선언

부분 보기를 다른 뷰와 마찬가지로 만듭니다. *보기* 폴더 내에서 *.cshtml* 파일을 만듭니다. 부분 보기 및 일반 보기 간에 의미 체계 차이점이 없습니다. 그저 다르게 렌더링되었을 뿐입니다. 컨트롤러의 `ViewResult`에서 직접 반환되는 보기를 사용할 수 있습니다. 같은 보기를 부분 보기로 사용할 수 있습니다. 보기와 부분 보기가 렌더링되는 방법 간의 주요 차이점은 부분 보기가 *_ViewStart.cshtml*을 실행하지 않는다는 점입니다. (보기에서 수행하는 동안 [레이아웃](layout.md)에서 *_viewstart.vbhtml*에 대해 자세히 알아봅니다.)

## <a name="referencing-a-partial-view"></a>부분 보기 참조

페이지 보기 내에서 부분 보기를 렌더링할 수 있는 여러 가지 방법이 있습니다. `Html.Partial`을 사용하는 것이 가장 간단합니다. 그러면 `IHtmlString`을 반환하고 `@`을 포함하는 호출을 접두사로 사용하여 참조될 수 있습니다.

[!code-html[Main](partial/sample/src/PartialViewsSample/Views/Home/About.cshtml?range=9)]

`PartialAsync` 메서드는 비동기 코드가 포함된 부분 보기를 사용할 수 있습니다(하지만 보기의 코드는 일반적으로 권장되지 않음).

[!code-html[Main](partial/sample/src/PartialViewsSample/Views/Home/About.cshtml?range=8)]

`RenderPartial`을 사용하여 부분 보기를 렌더링할 수도 있습니다. 이 메서드는 결과를 반환하지 않습니다. 렌더링된 출력을 응답에 직접 스트리밍합니다. 결과를 반환하지 않기 때문에 Razor 코드 블록 내에서 호출되어야 합니다(필요한 경우 `RenderPartialAsync`를 호출할 수도 있음).

[!code-html[Main](partial/sample/src/PartialViewsSample/Views/Home/About.cshtml?range=10-12)]

결과를 직접 스트리밍하기 때문에 `RenderPartial` 및 `RenderPartialAsync`는 일부 시나리오에서 더 잘 수행될 수 있습니다. 그러나 대부분의 경우 `Partial` 및 `PartialAsync`를 사용하는 것이 좋습니다.

> [!NOTE]
> 보기가 코드를 실행해야 하는 경우 권장되는 패턴은 부분 보기 대신 [보기 구성 요소](view-components.md)를 사용하는 것입니다.

### <a name="partial-view-discovery"></a>부분 보기 검색

부분 보기를 참조하는 경우 여러 가지 방법으로 해당 위치를 참조할 수 있습니다.

```text
// Uses a view in current folder with this name
// If none is found, searches the Shared folder
@Html.Partial("ViewName")

// A view with this name must be in the same folder
@Html.Partial("ViewName.cshtml")

// Locate the view based on the application root
// Paths that start with "/" or "~/" refer to the application root
@Html.Partial("~/Views/Folder/ViewName.cshtml")
@Html.Partial("/Views/Folder/ViewName.cshtml")

// Locate the view using relative paths
@Html.Partial("../Account/LoginPartial.cshtml")
```

다른 보기 폴더에서 이름이 같은 다른 부분 보기를 사용할 수 있습니다. 파일 확장명을 제외한 이름으로 보기를 참조할 때 각 폴더의 보기는 해당 보기와 같은 폴더에서 부분 보기를 사용합니다. 또한 사용할 기본 부분 보기를 지정하고 *공유* 폴더에 배치할 수 있습니다. 공유 부분 보기는 부분 보기의 고유한 버전이 설치되지 않은 모든 보기에서 사용합니다. *공유*에서 기본 부분 보기를 사용할 수 있고 부모 보기와 같은 폴더에 이름이 같은 부분 보기에 의해 재정의됩니다.

부분 보기는 *연결될* 수 있습니다. 즉, (루프를 만들지 않으면) 부분 보기는 다른 부분 보기를 호출할 수 있습니다. 각 보기 또는 부분 보기 내에서 상대 경로는 루트 또는 부모 보기가 아닌 항상 해당 보기를 기준으로 합니다.

> [!NOTE]
> 부분 보기에서 [Razor](razor.md) `section`를 선언하는 경우 해당 부모 보기에 표시되지 않습니다. 부분 보기로 제한됩니다.

## <a name="accessing-data-from-partial-views"></a>부분 보기의 데이터에 액세스

부모 보기가 인스턴스화되면 부모 보기의 `ViewData` 사전의 복사본을 가져옵니다. 부분 보기 내에서 데이터에 대한 업데이트는 부모 보기에 유지되지 않습니다. 부분 보기에서 변경된 `ViewData`는 부분 보기가 반환될 때 손실됩니다.

`ViewDataDictionary`의 인스턴스를 부분 보기로 전달할 수 있습니다.

```csharp
@Html.Partial("PartialName", customViewData)
   ```

모델을 부분 보기에 전달할 수도 있습니다. 페이지의 보기 모델 또는 그 중 일부나 사용자 지정 개체일 수 있습니다. 모델을 `Partial`,`PartialAsync`, `RenderPartial` 또는 `RenderPartialAsync`에 전달할 수 있습니다.

```csharp
@Html.Partial("PartialName", viewModel)
   ```

`ViewDataDictionary`의 인스턴스 및 보기 모델을 부분 보기에 전달할 수 있습니다.

[!code-html[Main](partial/sample/src/PartialViewsSample/Views/Articles/Read.cshtml?range=15-16)]

다음 태그는 두 개의 부분 보기를 포함하는 *Views/Articles/Read.cshtml* 보기를 보여줍니다. 두 번째 부분 보기는 모델 및 `ViewData`를 부분 보기에 전달합니다. 아래의 강조 표시된 `ViewDataDictionary`의 생성자 오버로드를 사용하는 경우 기존 `ViewData`를 유지하면서 새로운 `ViewData` 사전을 전달할 수 있습니다.

[!code-html[Main](partial/sample/src/PartialViewsSample/Views/Articles/Read.cshtml)]

*Views/Shared/AuthorPartial*:

[!code-html[Main](partial/sample/src/PartialViewsSample/Views/Shared/AuthorPartial.cshtml)]

*ArticleSection* 부분:

[!code-html[Main](partial/sample/src/PartialViewsSample/Views/Articles/ArticleSection.cshtml)]

런타임 시 부분은 부모 보기에 렌더링됩니다. 여기서 자체는 공유 *_Layout.cshtml* 내에서 렌더링됩니다.

![부분 보기 출력](partial/_static/output.png)
