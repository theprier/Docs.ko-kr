---
title: ASP.NET Core의 부분 보기
author: ardalis
description: 부분 보기가 어떻게 다른 보기 내에서 렌더링된 보기인지, 언제 ASP.NET Core 앱에서 사용해야 하는지 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 07/06/2018
uid: mvc/views/partial
ms.openlocfilehash: 9f90ce39929d0dbc216b47d76d652c1fca866ec2
ms.sourcegitcommit: a09820f91e71a7d98b7347bf93210abb9e995e22
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2018
ms.locfileid: "37889118"
---
# <a name="partial-views-in-aspnet-core"></a>ASP.NET Core의 부분 보기

작성자: [Steve Smith](https://ardalis.com/), [Maher JENDOUBI](https://twitter.com/maherjend), [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Scott Sauber](https://twitter.com/scottsauber)

ASP.NET Core MVC는 부분 보기를 지원합니다. 이 기능은 웹 페이지의 재사용 가능한 부분을 다른 보기에서 공유하려는 경우에 유용합니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/partial/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="what-are-partial-views"></a>부분 보기란?

부분 보기는 다른 보기 내에서 렌더링되는 보기입니다. 부분 보기를 실행하여 생성된 HTML 출력을 호출 (또는 부모) 보기에 렌더링합니다. 보기와 같이 부분 보기는 *.cshtml* 파일 확장명을 사용합니다.

예를 들어, ASP.NET Core 2.1 **웹 응용 프로그램** 프로젝트 템플릿은 *_CookieConsentPartial.cshtml* 부분 보기를 포함합니다. 부분 보기가 *_Layout.cshtml*내에서 로드됩니다.

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Shared/_Layout.cshtml?name=snippet_CookieConsentPartial)]

## <a name="when-to-use-partial-views"></a>부분 보기를 사용하는 경우

부분 보기를 통해 큰 보기를 더 작은 구성 요소로 효과적으로 분리할 수 있습니다. 콘텐츠 보기의 중복을 줄이고 보기 요소를 다시 사용할 수 있습니다. 일반 레이아웃 요소는 [_Layout.cshtml](xref:mvc/views/layout)에서 지정해야 합니다. 레이아웃이 아닌 다시 사용 가능한 콘텐츠는 부분 보기로 캡슐화될 수 있습니다.

논리 조각으로 구성된 복잡한 페이지를 사용하는 경우 고유한 부분 보기로 각 부분을 작업하는 것이 유용합니다. 페이지의 나머지 부분과 분리해서 페이지의 각 부분을 볼 수 있습니다. 전체 페이지 구조와 부분 보기를 렌더링하기 위한 호출만 포함하기 때문에 페이지 자체에 대한 보기가 더 간단해집니다.

> [!TIP]
> 보기에서 [반복 금지 원칙](https://deviq.com/don-t-repeat-yourself/)을 따릅니다.

## <a name="declare-partial-views"></a>부분 보기 선언

부분 보기는 일반 뷰&mdash;와 마찬가지로 *보기* 폴더 내에서 *.cshtml* 파일을 만들어 생성합니다. 부분 보기 및 일반 보기 간에 의미 체계 차이점이 없으나 다르게 렌더링되었습니다. 컨트롤러의 [ViewResult](/dotnet/api/microsoft.aspnetcore.mvc.viewresult)에서 직접 반환되는 보기를 사용할 수 있습니다. 같은 보기를 부분 보기로 사용할 수 있습니다. 보기와 부분 보기가 렌더링되는 방법 간의 주요 차이점은 부분 보기가 *_ViewStart.cshtml*을 실행하지 않는다는 점입니다. 일반 뷰는 *_ViewStart.cshtml*을 실행합니다. [레이아웃](xref:mvc/views/layout)에서 *_ViewStart.cshtml*에 대해 자세히 알아보세요).

보통 부분 보기 파일 이름은 `_`로 시작합니다. 이 명명 규칙은 요구사항은 아니지만 일반 뷰에서 부분 보기를 시각적으로 구분하는 데 도움이 됩니다.

## <a name="reference-a-partial-view"></a>부분 보기 참조

페이지 보기 내에서 부분 보기를 렌더링할 수 있는 여러 가지 방법이 있습니다. 비동기 렌더링을 사용하는 것이 가장 좋습니다.

::: moniker range=">= aspnetcore-2.1"

### <a name="partial-tag-helper"></a>부분 태그 도우미

부분 태그 도우미에는 ASP.NET Core 2.1 이상이 필요합니다. 이는 비동기적으로 렌더링하고 HTML과 유사한 구문을 사용합니다.

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Home/Discovery.cshtml?name=snippet_PartialTagHelper)]

자세한 내용은 <xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper>을 참조하세요.

::: moniker-end

### <a name="asynchronous-html-helper"></a>비동기 HTML 도우미

HTML 도우미를 사용할 때 가장 좋은 방법은 [PartialAsync](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.partialasync#Microsoft_AspNetCore_Mvc_Rendering_HtmlHelperPartialExtensions_PartialAsync_Microsoft_AspNetCore_Mvc_Rendering_IHtmlHelper_System_String_)를 사용하는 것입니다. `Task`에 래핑된 형식으로 [IHtmlContent](/dotnet/api/microsoft.aspnetcore.html.ihtmlcontent)를 반환합니다. `@`을 접두사로 호출을 사용하여 메서드를 참조합니다.

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Home/Discovery.cshtml?name=snippet_PartialAsync)]

또는 [RenderPartialAsync](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.renderpartialasync)를 사용하여 부분 보기를 렌더링할 수 있습니다. 이 메서드는 결과를 반환하지 않습니다. 렌더링된 출력을 응답에 직접 스트리밍합니다. 이 메서드는 결과를 반환하지 않기 때문에 Razor 코드 블록 내에서 호출되어야 합니다.

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Home/Discovery.cshtml?name=snippet_RenderPartialAsync)]

결과를 직접 스트리밍하기 때문에 `RenderPartialAsync`는 일부 시나리오에서 더 잘 작동할 수 있습니다. 그러나 `PartialAsync`를 사용하는 것이 좋습니다.

### <a name="synchronous-html-helper"></a>동기 HTML 도우미

[Partial](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.partial) 및 [RenderPartial](/dotnet/api/microsoft.aspnetcore.mvc.rendering.htmlhelperpartialextensions.renderpartial)의 해당하는 동기 항목은 각각 `PartialAsync` 및 `RenderPartialAsync`입니다. 교착 상태인 시나리오가 있으므로 동기 해당 항목을 사용하지 않는 것이 좋습니다. 향후 릴리스는 동기 메서드를 포함하지 않을 예정입니다.

> [!IMPORTANT]
> 보기가 코드를 실행해야 하는 경우 부분 보기 대신 [보기 구성 요소](xref:mvc/views/view-components)를 사용합니다.

::: moniker range=">= aspnetcore-2.1"

ASP.NET Core 2.1 이상 버전에서는 `Partial` 또는 `RenderPartial` 호출 시 분석기 경고가 발생합니다. 예를 들어 `Partial` 사용 시 다음 경고 메시지가 나타납니다.

> IHtmlHelper.Partial 사용 시 응용 프로그램이 교착 상태가 될 수 있습니다. `<partial>` 태그 도우미 또는 `IHtmlHelper.PartialAsync`를 사용하는 것이 좋습니다.

`@Html.Partial`에 대한 호출을 `@await Html.PartialAsync`나 부분 태그 도우미로 바꿉니다. 부분 태그 도우미 마이그레이션에 대한 자세한 내용은 [HTML 도우미에서 마이그레이션](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper#migrate-from-an-html-helper)을 참조합니다.

::: moniker-end

## <a name="partial-view-discovery"></a>부분 보기 검색

부분 보기를 참조하는 경우 여러 가지 방법으로 해당 위치를 참조할 수 있습니다. 예:

::: moniker range=">= aspnetcore-2.1"

```cshtml
// Uses a view in current folder with this name.
// If none is found, searches the Shared folder.
<partial name="_ViewName" />

// A view with this name must be in the same folder
<partial name="_ViewName.cshtml" />

// Locate the view based on the app root.
// Paths that start with "/" or "~/" refer to the app root.
<partial name="~/Views/Folder/_ViewName.cshtml" />
<partial name="/Views/Folder/_ViewName.cshtml" />

// Locate the view using a relative path
<partial name="../Account/_LoginPartial.cshtml" />
```

앞의 예제는 ASP.NET Core 2.1 이상을 필요로 하는 부분 태그 도우미를 사용합니다. 다음 예제에서는 비동기 HTML 도우미를 사용하여 동일한 작업을 수행합니다.

::: moniker-end

```cshtml
// Uses a view in current folder with this name.
// If none is found, searches the Shared folder.
@await Html.PartialAsync("_ViewName")

// A view with this name must be in the same folder
@await Html.PartialAsync("_ViewName.cshtml")

// Locate the view based on the app root.
// Paths that start with "/" or "~/" refer to the app root.
@await Html.PartialAsync("~/Views/Folder/_ViewName.cshtml")
@await Html.PartialAsync("/Views/Folder/_ViewName.cshtml")

// Locate the view using a relative path
@await Html.PartialAsync("../Account/_LoginPartial.cshtml")
```

다른 보기 폴더에서 파일 이름이 같은 다른 부분 보기를 사용할 수 있습니다. 파일 확장명을 제외한 이름으로 보기를 참조할 때 각 폴더의 보기는 해당 보기와 같은 폴더에서 부분 보기를 사용합니다. 또한 사용할 기본 부분 보기를 지정하고 *공유* 폴더에 배치할 수 있습니다. 공유 부분 보기는 부분 보기의 고유한 버전이 설치되지 않은 모든 보기에서 사용합니다. *공유*에서 기본 부분 보기를 사용할 수 있고 부모 보기와 같은 폴더에 이름이 같은 부분 보기에 의해 재정의됩니다.

부분 보기는 *연결될* 수 있습니다. &mdash;즉, (루프를 만들지 않으면) 부분 보기는 다른 부분 보기를 호출할 수 있습니다. 각 보기 또는 부분 보기 내에서 상대 경로는 루트 또는 부모 보기가 아닌 항상 해당 보기를 기준으로 합니다.

> [!NOTE]
> 부분 보기에 정의된 [Razor](xref:mvc/views/razor) `section`이 부모 보기에 표시되지 않습니다. `section`만 정의되어 있는 부분 보기에 표시됩니다.

## <a name="access-data-from-partial-views"></a>부분 보기에서 데이터 액세스

부모 보기가 인스턴스화되면 부모 보기의 `ViewData` 사전의 복사본을 가져옵니다. 부분 보기 내에서 데이터에 대한 업데이트는 부모 보기에 유지되지 않습니다. 부분 보기에서 변경된 `ViewData`는 부분 보기가 반환될 때 손실됩니다.

[ViewDataDictionary](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary)의 인스턴스를 부분 보기로 전달할 수 있습니다.

```cshtml
@await Html.PartialAsync("_PartialName", customViewData)
```

모델을 부분 보기에 전달할 수 있습니다. 해당 모델은 페이지의 보기 모델 또는 사용자 지정 개체일 수 있습니다. 모델을 `PartialAsync` 또는 `RenderPartialAsync`에 전달할 수 있습니다.

```cshtml
@await Html.PartialAsync("_PartialName", viewModel)
```

`ViewDataDictionary`의 인스턴스 및 보기 모델을 부분 보기에 전달할 수 있습니다.

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Articles/Read.cshtml?name=snippet_PartialAsync)]

다음 태그는 두 개의 부분 보기를 포함하는 *Views/Articles/Read.cshtml* 보기를 보여줍니다. 두 번째 부분 보기는 모델 및 `ViewData`를 부분 보기에 전달합니다. 강조 표시된 `ViewDataDictionary` 생성자 오버로드를 사용하여 기존 `ViewData` 사전을 유지하면서 새로운 `ViewData` 사전을 전달할 수 있습니다.

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Articles/Read.cshtml?name=snippet_ReadPartialView&highlight=17-20)]

*Views/Shared/_AuthorPartial*:

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Shared/_AuthorPartial.cshtml)]

*_ArticleSection* 부분:

[!code-cshtml[](partial/sample/PartialViewsSample/Views/Articles/_ArticleSection.cshtml)]

런타임 시 부분은 부모 보기에 렌더링됩니다. 여기서 자체는 공유 *_Layout.cshtml* 내에서 렌더링됩니다.

![부분 보기 출력](partial/_static/output.png)

## <a name="additional-resources"></a>추가 자료

::: moniker range=">= aspnetcore-2.1"

* <xref:mvc/views/razor>
* <xref:mvc/views/tag-helpers/intro>
* <xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper>
* <xref:mvc/views/view-components>

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

* <xref:mvc/views/razor>
* <xref:mvc/views/view-components>

::: moniker-end