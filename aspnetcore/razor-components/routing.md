---
title: 라우팅 razor 구성 요소
author: guardrex
description: 앱에 NavLink 구성 요소에 대 한 요청을 라우팅하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 04/07/2019
uid: razor-components/routing
ms.openlocfilehash: ef82fa7e0d571979a43fd8ce712bf4f22c06f9a7
ms.sourcegitcommit: 948e533e02c2a7cb6175ada20b2c9cabb7786d0b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2019
ms.locfileid: "59515678"
---
# <a name="razor-components-routing"></a>라우팅 razor 구성 요소

[Luke Latham](https://github.com/guardrex)으로

앱에 NavLink 구성 요소에 대 한 요청을 라우팅하는 방법에 알아봅니다.

## <a name="aspnet-core-endpoint-routing-integration"></a>ASP.NET Core 끝점 라우팅 통합

Razor 구성 요소에 통합 되어 [ASP.NET Core 라우팅](xref:fundamentals/routing)합니다. ASP.NET Core 앱을 사용 하 여 대화형 Razor 구성 요소에 대 한 들어오는 연결을 허용 하도록 구성 된 `MapComponentHub<TComponent>` 에서 `Startup.Configure`합니다. `MapComponentHub` 지정 된 루트 구성 요소 `App` 선택기와 일치 하는 DOM 요소 안에 렌더링 해야 `app`:

```csharp
app.UseRouting(routes =>
{
    routes.MapRazorPages();
    routes.MapComponentHub<App>("app");
});
```

## <a name="route-templates"></a>경로 템플릿

`<Router>` 구성 요소를 사용 하면 라우팅 및 경로 템플릿에 액세스할 수 있는 각 구성 요소에 제공 됩니다. 합니다 `<Router>` 구성 요소에 표시 되는 *Components/App.razor* 파일:

```cshtml
<Router AppAssembly="typeof(Program).Assembly" />
```

때를 *.razor* 또는 *.cshtml* 파일을 `@page` 지시문 컴파일됩니다, 생성된 된 클래스는 지정 된을 <xref:Microsoft.AspNetCore.Mvc.RouteAttribute> 경로 템플릿을 지정 합니다. 런타임 시 사용 하 여 구성 요소 클래스에 대 한 라우터 찾습니다는 `RouteAttribute` 하 고 어떤 구성 요소는 요청 된 URL과 일치 하는 경로 템플릿을 렌더링 합니다.

여러 경로 템플릿 구성 요소에 적용할 수 있습니다. 다음 구성 요소에 대 한 요청에 응답할 `/BlazorRoute` 고 `/DifferentBlazorRoute`:

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/BlazorRoute.cshtml?name=snippet_BlazorRoute)]

`<Router>` 확인할 때 요청 된 경로 렌더링에 대 한 대체 (fallback) 구성 요소를 설정 하는 지원 되지 않습니다. 설정 하 여이 옵트인 시나리오를 사용 하도록 설정 된 `FallbackComponent` 대체 (fallback) 구성 요소 클래스의 형식 매개 변수입니다.

다음 예제에서는 설정에 정의 된 구성 요소 *Pages/MyFallbackRazorComponent.cshtml* 에 대 한 대체 (fallback) 구성 요소로 `<Router>`:

```cshtml
<Router ... FallbackComponent="typeof(Pages.MyFallbackRazorComponent)" />
```

> [!IMPORTANT]
> 경로 올바르게 생성 하려면 앱을 포함 해야 합니다는 `<base>` 태그 해당 *wwwroot/index.html* 에 지정 된 앱 기본 경로 사용 하 여 파일을 `href` 특성 (`<base href="/">`). 자세한 내용은 <xref:host-and-deploy/razor-components-blazor/blazor#app-base-path>을 참조하세요.

## <a name="route-parameters"></a>경로 매개 변수

라우터 경로 매개 변수를 사용 하 여 동일한 이름 (대/소문자 구분)를 사용 하 여 해당 구성 요소 매개 변수를 채웁니다.

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/RouteParameter.cshtml?name=snippet_RouteParameter&highlight=2,7-8)]

선택적 매개 변수는 아직 지원 되지 않습니다 하므로 두 `@page` 지시문 위의 예제에 적용 됩니다. 첫 번째 매개 변수 없이 구성 요소에 대 한 탐색을 허용합니다. 두 번째 `@page` 지시문은 합니다 `{text}` 경로 매개 변수 및 값을 할당 합니다 `Text` 속성입니다.

## <a name="route-constraints"></a>경로 제약 조건

경로 제약 조건 형식 구성 요소에 경로 세그먼트에서 일치를 적용 합니다.

다음 예에서 경로 사용자 구성 요소를 경우에 일치 합니다.

* `Id` 경로 세그먼트는 요청 URL에 존재 합니다.
* 합니다 `Id` 세그먼트는 정수 (`int`).

[!code-cshtml[](routing/samples_snapshot/3.x/Constraint.cshtml?highlight=1)]

다음 표에 표시 된 경로 제약 조건을 사용할 수 있습니다. 고정 문화권을 사용 하 여 일치 하는 경로 제약 조건에 대 한이 경고 테이블에 대 한 자세한 내용은 아래를 참조 하세요.

| 제약 조건 | 예제           | 일치하는 예제                                                                  | 고정<br>culture<br>일치 |
| ---------- | ----------------- | -------------------------------------------------------------------------------- | :------------------------------: |
| `bool`     | `{active:bool}`   | `true`, `FALSE`                                                                  | 아니요                               |
| `datetime` | `{dob:datetime}`  | `2016-12-31`, `2016-12-31 7:32pm`                                                | 예                              |
| `decimal`  | `{price:decimal}` | `49.99`, `-1,000.01`                                                             | 예                              |
| `double`   | `{weight:double}` | `1.234`, `-1,001.01e8`                                                           | 예                              |
| `float`    | `{weight:float}`  | `1.234`, `-1,001.01e8`                                                           | 예                              |
| `guid`     | `{id:guid}`       | `CD2C1638-1638-72D5-1638-DEADBEEF1638`, `{CD2C1638-1638-72D5-1638-DEADBEEF1638}` | 아니요                               |
| `int`      | `{id:int}`        | `123456789`, `-123456789`                                                        | 예                              |
| `long`     | `{ticks:long}`    | `123456789`, `-123456789`                                                        | 예                              |

> [!WARNING]
> CLR 형식(예: `int` 또는 `DateTime`)으로 변환되는 URL을 확인하는 경로 제약 조건은 항상 고정 문화권을 사용합니다. 이러한 제약 조건은 URL은 지역화될 수 없다고 가정합니다.

## <a name="navlink-component"></a>NavLink 구성 요소

HTML 대신 NavLink 구성 요소를 사용 하 여 `<a>` 탐색 링크를 만들 때 요소입니다. NavLink 구성 요소 처럼를 `<a>` 요소를 설정/해제 하는 점을 제외 하 고는 `active` CSS 클래스에 따라 해당 `href` 현재 URL과 일치 합니다. `active` 클래스는 사용자는 페이지는 표시 된 탐색 링크 간에 활성 페이지를 이해 합니다.

다음 NavMenu 구성 요소를 만듭니다는 [부트스트랩](https://getbootstrap.com/docs/) NavLink 구성 요소를 사용 하는 방법에 설명 하는 탐색 모음:

[!code-cshtml[](common/samples/3.x/BlazorSample/Shared/NavMenu.cshtml?name=snippet_NavLinks&highlight=4-6,9-11)]

두 개의 `NavLinkMatch` 옵션:

* `NavLinkMatch.All` &ndash; 전체 현재 URL 일치 하는 경우는 NavLink 해야 활성 수를 지정 합니다.
* `NavLinkMatch.Prefix` &ndash; NavLink 함을 active 현재 URL의 접두사를 벗어난 일치할 경우를 지정 합니다.

위의 예에서 홈 NavLink (`href=""`) 모든 Url과 일치 하 고 항상 수신 된 `active` CSS 클래스입니다. 두 번째 NavLink 데이터만 수신 합니다 `active` Blazor 경로 구성 요소를 방문 하는 사용자 클래스 (`href="BlazorRoute"`).
