---
title: "앵커 태그 도우미"
author: pkellner
description: "ASP.NET Core 앵커 태그 도우미 특성 및 HTML 앵커 태그의 동작을 확장할 때 각 특성이 담당하는 역할을 검색합니다."
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 01/31/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/tag-helpers/builtin-th/anchor-tag-helper
ms.openlocfilehash: f3b704174c3287edda12725b7973a2464e485bac
ms.sourcegitcommit: f2a11a89037471a77ad68a67533754b7bb8303e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="anchor-tag-helper"></a>앵커 태그 도우미

작성자: [Peter Kellner](http://peterkellner.net) 및 [Scott Addie](https://github.com/scottaddie)

[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/tag-helpers/built-in/samples/TagHelpersBuiltInAspNetCore)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

[앵커 태그 도우미](/dotnet/api/microsoft.aspnetcore.mvc.taghelpers.anchortaghelper)는 새 특성을 추가하여 표준 HTML 앵커(`<a ... ></a>`) 태그를 향상시킵니다. 규칙에 따라 특성 이름의 접두사는 `asp-`입니다. 렌더링된 앵커 요소의 `href` 특성 값은 `asp-` 특성 값에 따라 결정됩니다.

*SpeakerController*는 이 문서 전반의 샘플에서 사용됩니다.

[!code-csharp[](samples/TagHelpersBuiltInAspNetCore/Controllers/SpeakerController.cs?name=snippet_SpeakerController)]

`asp-` 특성의 인벤토리는 다음과 같습니다.

## <a name="asp-controller"></a>asp-controller

[asp-controller](/dotnet/api/microsoft.aspnetcore.mvc.taghelpers.anchortaghelper.controller) 특성은 URL 생성에 사용되는 컨트롤러를 할당합니다. 다음 태그는 모든 스피커를 나열합니다.

[!code-cshtml[](samples/TagHelpersBuiltInAspNetCore/Views/Home/Index.cshtml?name=snippet_AspController)]

생성된 코드:

```html
<a href="/Speaker">All Speakers</a>
```

`asp-controller` 특성이 지정되고 `asp-action`이 지정되지 않으면, 기본 `asp-action` 값은 현재 실행 중인 보기와 연결된 컨트롤러 작업입니다. 위의 태그에서 `asp-action`이 생략되고 *HomeController*의 *인덱스* 보기(*/Home*)에서 앵커 태그 도우미가 사용되는 경우 생성된 HTML은 다음과 같습니다.

```html
<a href="/Home">All Speakers</a>
```

## <a name="asp-action"></a>asp-action

[asp-action](/dotnet/api/microsoft.aspnetcore.mvc.taghelpers.anchortaghelper.action) 특성 값은 생성된 `href` 특성에 포함된 컨트롤러 작업 이름을 나타냅니다. 다음 태그는 생성된 `href` 특성 값을 스피커 평가 페이지로 설정합니다.

[!code-cshtml[](samples/TagHelpersBuiltInAspNetCore/Views/Home/Index.cshtml?name=snippet_AspAction)]

생성된 코드:

```html
<a href="/Speaker/Evaluations">Speaker Evaluations</a>
```

`asp-controller` 특성을 지정하지 않으면 현재 보기를 실행 중인 보기를 호출하는 기본 컨트롤러가 사용됩니다.

`asp-action` 특성 값이 `Index`이면 URL에 아무 작업도 추가되지 않으므로 기본 `Index` 작업이 호출됩니다. 지정된(또는 기본값으로 설정된) 작업은 `asp-controller`에서 참조되는 컨트롤러에 있어야 합니다.

## <a name="asp-route-value"></a>asp-route-{value}

[asp-route-{value}](/dotnet/api/microsoft.aspnetcore.mvc.taghelpers.anchortaghelper.routevalues) 특성은 와일드카드 경로 접두사를 사용하도록 설정합니다. `{value}` 자리 표시자에 포함되는 모든 값은 잠재적인 경로 매개 변수로 해석됩니다. 기본 경로가 없으면 이 경로 접두사가 생성되는 `href` 특성에 요청 매개 변수 및 값으로 추가됩니다. 그렇지 않으면 경로 템플릿에서 이 경로 접두사가 대체됩니다.

다음 컨트롤러 작업을 살펴보세요.

[!code-csharp[](samples/TagHelpersBuiltInAspNetCore/Controllers/BuiltInTagController.cs?name=snippet_AnchorTagHelperAction)]

*Startup.Configure*에 정의된 기본 경로 템플릿을 사용하는 경우 다음과 같습니다.

[!code-csharp[](samples/TagHelpersBuiltInAspNetCore/Startup.cs?name=snippet_UseMvc&highlight=8-10)]

MVC 보기는 다음과 같이 작업을 통해 제공되는 모델을 사용합니다.

```cshtml
@model Speaker
<!DOCTYPE html>
<html>
<body>
    <a asp-controller="Speaker"
       asp-action="Detail" 
       asp-route-id="@Model.SpeakerId">SpeakerId: @Model.SpeakerId</a>
</body>
</html>
```

기본 경로의 `{id?}` 자리 표시자가 일치했습니다. 생성된 코드:

```html
<a href="/Speaker/Detail/12">SpeakerId: 12</a>
```

다음 MVC 보기와 마찬가지로 경로 접두사가 라우팅 템플릿의 일부와 일치하지 않는다고 가정합니다.

```cshtml
@model Speaker
<!DOCTYPE html>
<html>
<body>
    <a asp-controller="Speaker" 
       asp-action="Detail" 
       asp-route-speakerid="@Model.SpeakerId">SpeakerId: @Model.SpeakerId</a>
<body>
</html>
```

일치하는 경로에서 `speakerid`를 찾을 수 없기 때문에 생성된 HTML은 다음과 같습니다.

```html
<a href="/Speaker/Detail?speakerid=12">SpeakerId: 12</a>
```

`asp-controller` 또는 `asp-action`이 지정되지 않으면 `asp-route` 특성과 동일한 기본 처리가 그대로 수행됩니다.

## <a name="asp-route"></a>asp-route

[asp-route](/dotnet/api/microsoft.aspnetcore.mvc.taghelpers.anchortaghelper.route) 특성은 명명된 경로에 직접 연결되는 URL을 만드는 데 사용됩니다. [라우팅 특성](xref:mvc/controllers/routing#attribute-routing)을 사용하면 경로가 `SpeakerController`에 표시된 이름으로 지정되고 해당 `Evaluations` 메서드에서 사용할 수 있습니다.

[!code-cshtml[](samples/TagHelpersBuiltInAspNetCore/Controllers/SpeakerController.cs?range=22-24)]

다음 태그에서 `asp-route` 특성은 명명된 경로를 참조합니다.

[!code-cshtml[](samples/TagHelpersBuiltInAspNetCore/Views/Home/Index.cshtml?name=snippet_AspRoute)]

앵커 태그 도우미는 */Speaker/Evaluations* URL을 사용하여 해당 컨트롤러 작업을 직접 가리키는 경로를 생성합니다. 생성된 코드:

```html
<a href="/Speaker/Evaluations">Speaker Evaluations</a>
```

`asp-route` 외에 `asp-controller` 또는 `asp-action`을 지정하면 예상과 다른 경로가 생성될 수 있습니다. 경로 충돌을 방지하기 위해 `asp-route`는 `asp-controller` 및 `asp-action` 특성과 함께 사용하지 않아야 합니다.

## <a name="asp-all-route-data"></a>asp-all-route-data

[asp-all-route-data](/dotnet/api/microsoft.aspnetcore.mvc.taghelpers.anchortaghelper.routevalues) 특성은 키-값 쌍 사전을 만들도록 지원합니다. 키는 매개 변수 이름이고, 값은 매개 변수 값입니다.

다음 예제에서는 사전이 초기화되어 Razor 보기로 전달됩니다. 또는 모델을 사용하여 데이터를 전달할 수도 있습니다.

[!code-cshtml[](samples/TagHelpersBuiltInAspNetCore/Views/Home/Index.cshtml?name=snippet_AspAllRouteData)]

앞의 코드에서 생성된 HTML은 다음과 같습니다.

```html
<a href="/Speaker/EvaluationsCurrent?speakerId=11&currentYear=true">Speaker Evaluations</a>
```

`asp-all-route-data` 사전을 평면화하여 오버로드된 `Evaluations` 작업의 요구 사항을 충족하는 쿼리 문자열을 생성합니다.

[!code-csharp[](samples/TagHelpersBuiltInAspNetCore/Controllers/SpeakerController.cs?range=26-30)]

사전에 있는 키가 경로 매개 변수와 일치하면 해당 값이 경로에서 적절하게 대체됩니다. 일치하지 않는 다른 값은 요청 매개 변수로 생성됩니다.

## <a name="asp-fragment"></a>asp-fragment

[asp-fragment](/dotnet/api/microsoft.aspnetcore.mvc.taghelpers.anchortaghelper.fragment) 특성은 URL에 추가할 URL 조각을 정의합니다. 앵커 태그 도우미는 해시 문자(#)를 추가합니다. 다음 태그를 살펴보세요.

[!code-cshtml[](samples/TagHelpersBuiltInAspNetCore/Views/Home/Index.cshtml?name=snippet_AspFragment)]

생성된 코드:

```html
<a href="/Speaker/Evaluations#SpeakerEvaluations">Speaker Evaluations</a>
```

해시 태그는 클라이언트 쪽 앱을 빌드할 때 유용합니다. 다음과 같이 JavaScript에서 손쉽게 만들고 검색하는 데 사용할 수 있습니다.

## <a name="asp-area"></a>asp-area

[asp-area](/dotnet/api/microsoft.aspnetcore.mvc.taghelpers.anchortaghelper.area) 특성은 적절한 경로를 설정하는 데 사용되는 영역 이름을 설정합니다. 다음 예제에서는 area 특성으로 인해 경로가 다시 매핑되는 방식을 보여 줍니다. `asp-area`를 "Blogs"로 설정하면 이 앵커 태그에 대해 연결된 컨트롤러 및 보기의 경로에 *Areas/Blogs* 디렉터리가 접두사로 붙습니다.

* **<프로젝트 이름\>**
  * **wwwroot**
  * **영역**
    * **블로그**
      * **컨트롤러**
        * *HomeController.cs*
      * **뷰**
        * **Home**
          * *AboutBlog.cshtml*
          * *Index.cshtml*
        * *_ViewStart.cshtml*
  * **컨트롤러**

앞의 디렉터리 계층 구조에서 *AboutBlog.cshtml* 파일을 참조하는 태그는 다음과 같습니다.

[!code-cshtml[](samples/TagHelpersBuiltInAspNetCore/Views/Home/Index.cshtml?name=snippet_AspArea)]

생성된 코드:

```html
<a href="/Blogs/Home/AboutBlog">About Blog</a>
```

> [!TIP]
> MVC 앱에서 작업할 영역이 있는 경우 경로 템플릿에 해당 영역에 대한 참조가 포함되어야 합니다. 해당 템플릿은 *Startup.Configure*에서 `routes.MapRoute` 메서드 호출의 두 번째 매개 변수([!code-csharp[](samples/TagHelpersBuiltInAspNetCore/Startup.cs?name=snippet_UseMvc&highlight=5)])로 표시됩니다.

## <a name="asp-protocol"></a>asp-protocol

[asp-protocol](/dotnet/api/microsoft.aspnetcore.mvc.taghelpers.anchortaghelper.protocol) 특성은 URL에서 프로토콜(예: `https`)을 지정하는 데 사용됩니다. 예:

[!code-cshtml[samples/TagHelpersBuiltInAspNetCore/Views/Index.cshtml?name=snippet_AspProtocol]]

생성된 코드:

```html
<a href="https://localhost/Home/About">About</a>
```

이 예제의 호스트 이름은 localhost이지만, 앵커 태그 도우미는 URL을 생성할 때 웹 사이트의 공용 도메인을 사용합니다.

## <a name="asp-host"></a>asp-host

[asp-host](/dotnet/api/microsoft.aspnetcore.mvc.taghelpers.anchortaghelper.host) 특성은 URL에 호스트 이름을 지정하는 데 사용됩니다. 예:

[!code-cshtml[](samples/TagHelpersBuiltInAspNetCore/Views/Home/Index.cshtml?name=snippet_AspHost)]

생성된 코드:

```html
<a href="https://microsoft.com/Home/About">About</a>
```

## <a name="asp-page"></a>asp-page

[asp-page](/dotnet/api/microsoft.aspnetcore.mvc.taghelpers.anchortaghelper.page) 특성은 Razor 페이지와 함께 사용됩니다. 이는 앵커 태그의 `href` 특성 값을 특정 페이지로 설정하는 데 사용됩니다. 페이지 이름 앞에 슬래시("/")를 접두사로 사용하여 URL을 만듭니다.

다음 샘플은 참석자 Razor 페이지를 가리킵니다.

[!code-cshtml[](samples/TagHelpersBuiltInAspNetCore/Views/Home/Index.cshtml?name=snippet_AspPage)]

생성된 코드:

```html
<a href="/Attendee">All Attendees</a>
```

`asp-page` 특성은 `asp-route`, `asp-controller` 및 `asp-action` 특성과 함께 사용할 수 없습니다. 그러나 다음 태그에서 보여 주듯이 `asp-page`는 `asp-route-{value}`와 함께 사용하여 라우팅을 제어할 수 있습니다.

[!code-cshtml[](samples/TagHelpersBuiltInAspNetCore/Views/Home/Index.cshtml?name=snippet_AspPageAspRouteId)]

생성된 코드:

```html
<a href="/Attendee?attendeeid=10">View Attendee</a>
```

## <a name="asp-page-handler"></a>asp-page-handler

[asp-page-handler](/dotnet/api/microsoft.aspnetcore.mvc.taghelpers.anchortaghelper.pagehandler) 특성은 Razor 페이지와 함께 사용됩니다. 특정 페이지 처리기에 연결하기 위한 것입니다.

다음 페이지 처리기를 살펴보세요.

[!code-csharp[](samples/TagHelpersBuiltInAspNetCore/Pages/Attendee.cshtml.cs?name=snippet_OnGetProfileHandler)]

페이지 모델 관련 태그는 `OnGetProfile` 페이지 처리기에 연결됩니다. 페이지 처리기 메서드 이름의 `On<Verb>` 접두사는 `asp-page-handler` 특성 값에서 생략됩니다. 비동기 메서드인 경우 `Async` 접미사도 생략됩니다.

[!code-cshtml[](samples/TagHelpersBuiltInAspNetCore/Views/Home/Index.cshtml?name=snippet_AspPageHandler)]

생성된 코드:

```html
<a href="/Attendee?attendeeid=12&handler=Profile">Attendee Profile</a>
```

## <a name="additional-resources"></a>추가 리소스

* [영역](xref:mvc/controllers/areas)
* [Razor 페이지 소개](xref:mvc/razor-pages/index)
