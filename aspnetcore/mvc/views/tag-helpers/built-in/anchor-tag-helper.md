---
title: "ASP.NET Core의 앵커 태그 도우미"
author: pkellner
description: "앵커 태그 도우미 사용 방법 소개"
manager: wpickett
ms.author: riande
ms.date: 12/20/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/tag-helpers/builtin-th/anchor-tag-helper
ms.openlocfilehash: 404fc7bc3b35114066f035e1ac28d10a8279ccbc
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="anchor-tag-helper"></a>앵커 태그 도우미

작성자: [Peter Kellner](http://peterkellner.net) 

앵커 태그 도우미는 새 특성을 추가하여 HTML 앵커(`<a ... ></a>`) 태그를 강화합니다. 생성되는(`href` 태그에서) 링크는 새 특성을 사용하여 만들어집니다. 해당 URL은 https 같은 선택적 프로토콜을 포함할 수 있습니다.

아래의 스피커 컨트롤러는 이 문서의 샘플에 사용됩니다.

**SpeakerController.cs** 

[!code-csharp[SpeakerController](sample/TagHelpersBuiltInAspNetCore/src/TagHelpersBuiltInAspNetCore/Controllers/SpeakerController.cs)]


## <a name="anchor-tag-helper-attributes"></a>앵커 태그 도우미 특성

### <a name="asp-controller"></a>asp-controller

`asp-controller`는 URL을 생성하는 데 사용할 컨트롤러를 연결하는 데 사용됩니다. 지정된 컨트롤러가 현재 프로젝트에 있어야 합니다. 다음 코드는 모든 스피커를 나열합니다. 

```cshtml
<a asp-controller="Speaker" asp-action="Index">All Speakers</a>
```

생성된 태그는 다음과 같습니다.

```html
<a href="/Speaker">All Speakers</a>
```

`asp-controller`를 지정하고 `asp-action`을 지정하지 않으면 기본 `asp-action`이 현재 실행 중인 보기의 기본 컨트롤러 메서드가 됩니다. 즉, 위의 예에서 `asp-action`을 생략하면 이 앵커 태그 도우미는 *HomeController*의 `Index` 보기(**/Home**)에서 생성되고, 생성된 태그는 다음과 같습니다.

```html
<a href="/Home">All Speakers</a>
```

### <a name="asp-action"></a>asp-action

`asp-action`은 생성되는 `href`에 포함할 컨트롤러의 작업 메서드 이름입니다. 예를 들어 다음 코드는 생성된 `href`가 스피커 세부 정보 페이지를 가리키도록 설정합니다.

```html
<a asp-controller="Speaker" asp-action="Detail">Speaker Detail</a>
```

생성된 태그는 다음과 같습니다.

```html
<a href="/Speaker/Detail">Speaker Detail</a>
```

`asp-controller` 특성을 지정하지 않으면 현재 보기를 실행 중인 보기를 호출하는 기본 컨트롤러가 사용됩니다.  
 
`asp-action` 특성이 `Index`이면 URL에 아무 작업도 추가되지 않고, 기본 `Index` 메서드가 호출됩니다. 지정된(또는 기본값으로 설정된) 작업은 `asp-controller`에서 참조되는 컨트롤러에 있어야 합니다.

### <a name="asp-page"></a>asp-page

앵커 태그에 `asp-page` 특성을 사용하여 특정 페이지를 가리키도록 URL을 설정합니다. 페이지 이름에 슬래시("/")를 접두사로 사용하여 URL을 만듭니다. 아래 샘플의 URL은 현재 디렉터리의 "스피커" 페이지를 가리킵니다.

```cshtml
<a asp-page="/Speakers">All Speakers</a>
```

이전 코드 샘플의 `asp-page` 특성은 보기에서 다음 코드 조각과 비슷한 HTML 출력을 렌더링합니다.

```html
<a href="/items?page=%2FSpeakers">Speakers</a>
```

`asp-page` 특성은 `asp-route`, `asp-controller` 및 `asp-action` 특성과 함께 사용할 수 없습니다. 그러나 다음 코드 샘플에서 보여주듯이, `asp-page`는 `asp-route-id`와 함께 사용하여 라우팅을 제어할 수 있습니다.

```cshtml
<a asp-page="/Speaker" asp-route-id="@speaker.Id">View Speaker</a>
```

`asp-route-id`는 다음 출력을 생성합니다.

```html
https://localhost:44399/Speakers/Index/2?page=%2FSpeaker
```

> [!NOTE]
> `asp-page` 특성을 Razor 페이지에 사용하려면 URL이 상대 경로(예: `"./Speaker"`)여야 합니다. `asp-page` 특성의 상대 경로는 MVC 보기에서 사용할 수 없습니다. MVC 보기에는 "/" 구문을 사용합니다.

### <a name="asp-route-value"></a>asp-route-{value}

`asp-route-`는 와일드 카드 경로 접두사입니다. 후행 대시 뒤에 배치되는 모든 값은 잠재적 경로 매개 변수로 해석됩니다. 기본 경로를 찾을 수 없는 경우 이 경로 접두사는 생성되는 href에 요청 매개 변수 및 값으로 추가됩니다. 그렇지 않은 경우 이 경로 접두사는 경로 템플릿에서 대체됩니다.

다음과 같이 정의된 컨트롤러 메서드가 있다고 가정하겠습니다.

```csharp
public IActionResult AnchorTagHelper(string id)
{
    var speaker = new SpeakerData()
    {
        SpeakerId = 12
    };
    return View(viewName, speaker);
}
```

그리고 *Startup.cs*에 다음과 같은 기본 경로 템플릿이 정의되어 있습니다.

```csharp
app.UseMvc(routes =>
{
   routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{id?}");
});

```

컨트롤러에서 보기로 전달된 **스피커** 모델 매개 변수를 사용하는 데 필요한 앵커 태그 도우미를 포함하고 있는 **cshtml** 파일은 다음과 같습니다.

```cshtml
@model SpeakerData
<!DOCTYPE html>
<html><body>
<a asp-controller='Speaker' asp-action='Detail' asp-route-id=@Model.SpeakerId>SpeakerId: @Model.SpeakerId</a>
<body></html>
```

**id**가 기본 경로에서 발견되었기 때문에 다음과 같은 HTML이 생성됩니다.

```html
<a href='/Speaker/Detail/12'>SpeakerId: 12</a>
```

경로 접두사가 발견된 라우팅 템플릿의 일부가 아닌 경우 **cshtml** 파일은 다음과 같습니다.

```cshtml
@model SpeakerData
<!DOCTYPE html>
<html><body>
<a asp-controller='Speaker' asp-action='Detail' asp-route-speakerid=@Model.SpeakerId>SpeakerId: @Model.SpeakerId</a>
<body></html>
```

매칭된 경로에서 **speakerid**를 찾지 못했기 때문에 다음과 같은 HTML이 생성됩니다.

```html
<a href='/Speaker/Detail?speakerid=12'>SpeakerId: 12</a>
```

`asp-controller` 또는 `asp-action`을 지정하지 않으면 동일한 기본 처리가 `asp-route` 특성에 있는 그대로 이어집니다.

### <a name="asp-route"></a>asp-route

`asp-route`는 명명된 경로에 직접 연결되는 URL을 만드는 방법을 제공합니다. 라우팅 특성을 사용하면 `SpeakerController`에서 보여주는 것처럼 이름을 지정하고 해당 `Evaluations` 메서드에서 사용할 수 있습니다.

`Name = "speakerevals"`는 `/Speaker/Evaluations` URL을 사용하여 해당 컨트롤러 메서드에 직접 연결되는 경로를 생성하라고 앵커 태그 도우미에 알립니다. `asp-route` 외에 `asp-controller` 또는 `asp-action`을 지정하면 예상과 다른 경로가 생성될 수 있습니다. 경로 충돌을 방지하기 위해 `asp-route`를 `asp-controller` 또는 `asp-action` 특성과 함께 사용하면 안 됩니다.

### <a name="asp-all-route-data"></a>asp-all-route-data

`asp-all-route-data`를 사용하면 키가 매개 변수이고 값은 그 키와 연결된 값인 키 값 쌍 사전을 만들 수 있습니다.

아래 예제처럼 인라인 사전이 만들어지고 razor 보기에 데이터가 전달됩니다. 모델을 사용하여 데이터를 전달하는 방법도 있습니다.

```cshtml
@{
    var dict =
        new Dictionary<string, string>
        {
            {"speakerId", "11"},
            {"currentYear", "true"}
        };
}
<a asp-route="speakerevalscurrent"
asp-all-route-data="dict">SpeakerEvals</a>
```

위의 코드는 http://localhost/Speaker/EvaluationsCurrent?speakerId=11&currentYear=true URL을 생성합니다.

링크를 클릭하면 컨트롤러 메서드 `EvaluationsCurrent`가 호출됩니다. 해당 컨트롤러에는 `asp-all-route-data` 사전에서 만들어진 항목과 일치하는 두 개의 문자열 매개 변수가 있기 때문에 이 메서드가 호출됩니다.

사전에 있는 아무 키가 경로 매개 변수와 일치하는 경우 경로에서 해당 값이 적절하게 대체되고 일치하지 않는 다른 값은 요청 매개 변수로 생성됩니다.

### <a name="asp-fragment"></a>asp-fragment

`asp-fragment`는 URL에 추가할 URL 조각을 정의합니다. 앵커 태그 도우미는 해시 문자(#)를 추가합니다. 태그를 만들면:

```cshtml
<a asp-action="Evaluations" asp-controller="Speaker"  
   asp-fragment="SpeakerEvaluations">About Speaker Evals</a>
```

http://localhost/Speaker/Evaluations#SpeakerEvaluations URL이 생성됩니다.

해시 태그는 클라이언트 쪽 응용 프로그램을 빌드할 때 유용합니다. 다음과 같이 JavaScript에서 손쉽게 만들고 검색하는 데 사용할 수 있습니다.

### <a name="asp-area"></a>asp-area

`asp-area`는 ASP.NET Core에서 적절한 경로를 설정하기 위해 사용하는 영역 이름을 설정합니다. 아래는 영역 특성으로 인해 경로가 다시 매핑되는 원리를 보여주는 예입니다. `asp-area`를 Blogs로 설정하면 이 앵커 태그에 대해 연결된 컨트롤러 및 보기의 경로에 `Areas/Blogs` 디렉터리가 접두사로 붙습니다.

* 프로젝트 이름
  * wwwroot
  * 영역
    * 블로그
      * 컨트롤러
        * HomeController.cs
      * 보기
        * 홈
          * Index.cshtml
          * AboutBlog.cshtml
  * 컨트롤러

```AboutBlog.cshtml``` 파일을 참조할 때 ```area="Blogs"``` 같은 유효한 영역 태그를 지정하면 앵커 태그 도우미를 사용하여 다음 예처럼 표시됩니다.

```cshtml
<a asp-action="AboutBlog" asp-controller="Home" asp-area="Blogs">Blogs About</a>
```

생성된 HTML에는 영역 세그먼트가 포함되며 다음과 같습니다.

```html
<a href="/Blogs/Home/AboutBlog">Blogs About</a>
```

> [!TIP]
> MVC 영역이 웹 응용 프로그램에서 작동하려면 경로 템플릿에 영역의 참조가 포함되어야 합니다(있는 경우). `routes.MapRoute` 메서드 호출의 두 번째 매개 변수인 이 템플릿은 `template: '"{area:exists}/{controller=Home}/{action=Index}"'`와 비슷하게 표시됩니다.

### <a name="asp-protocol"></a>asp-protocol

`asp-protocol`은 URL에서 프로토콜(예: `https`)을 지정하는 데 사용됩니다. 프로토콜을 포함하는 앵커 태그 도우미 예제는 다음과 같습니다.

```<a asp-protocol="https" asp-action="About" asp-controller="Home">About</a>```

그리고 다음과 같은 HTML을 생성합니다.

```<a href="https://localhost/Home/About">About</a>```

이 예제의 도메인인 localhost이지만, 앵커 태그 도우미는 URL을 생성할 때 웹 사이트의 공용 도메인을 사용합니다.

## <a name="additional-resources"></a>추가 리소스

* [영역](xref:mvc/controllers/areas)
