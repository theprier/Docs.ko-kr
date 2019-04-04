---
title: Razor 구성 요소 소개
author: guardrex
description: ASP.NET Core 앱에서 .NET을 사용하여 대화형 클라이언트 쪽 웹 UI를 빌드하는 방법인 ASP.NET Core Razor 구성 요소를 살펴봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 03/27/2019
uid: razor-components/index
ms.openlocfilehash: 8b2e87fe856598a5ac231e3bc1d413957829b448
ms.sourcegitcommit: 3e9e1f6d572947e15347e818f769e27dea56b648
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2019
ms.locfileid: "58751011"
---
# <a name="introduction-to-razor-components"></a>Razor 구성 요소 소개

작성자: [Daniel Roth](https://github.com/danroth27) 및 [Luke Latham](https://github.com/guardrex)

‘Razor 구성 요소’는 .NET을 사용하여 대화형 클라이언트 쪽 웹 UI를 빌드하는 방법입니다.

* JavaScript 대신 C#을 사용하여 풍부한 대화형 UI를 빌드합니다.
* 모두 .NET으로 작성된 서버 쪽 및 클라이언트 쪽 앱을 공유합니다.
* 모바일 브라우저를 포함한 광범위한 브라우저 지원을 위해 UI를 HTML 및 CSS로 렌더링합니다.

Razor 구성 요소는 다음을 포함한 대부분의 앱에 필요한 핵심 기능을 지원합니다.

* 매개 변수
* 이벤트 처리
* 데이터 바인딩
* 라우팅
* 종속성 주입
* 레이아웃
* 템플릿
* 연계 값

Razor 구성 요소는 UI 업데이트 적용 방법에서 구성 요소 렌더링 논리를 분리합니다. .NET Core 3.0의 ASP.NET Core Razor 구성 요소는 ASP.NET Core 앱의 서버에서 Razor 구성 요소를 호스트하는 기능을 추가합니다. UI 업데이트는 SignalR 연결을 통해 처리됩니다.

런타임이 다음을 수행합니다.

* 브라우저에서 서버로 UI 이벤트 보내기를 처리합니다.
* 구성 요소를 실행한 후 서버가 보낸 UI 업데이트를 다시 브라우저에 적용합니다.

Razor 구성 요소가 브라우저와 통신하는 데 사용하는 연결은 JavaScript interop 호출을 처리하는 데도 사용됩니다.

![Razor 구성 요소는 서버에서 .NET 코드를 실행하고 SignalR 연결을 통해 클라이언트의 문서 개체 모델과 상호 작용합니다.](index/_static/aspnet-core-razor-components.png)

자세한 내용은 <xref:razor-components/hosting-models#server-side-hosting-model>을 참조하세요.

*Blazor*는 Razor 구성 요소의 실험적 클라이언트 쪽 호스팅 모델입니다. Blazor는 플러그 인이나 코드 소스 간 컴파일 없이 개방형 웹 표준을 사용하여 브라우저의 .NET에서 실행됩니다. 자세한 내용은 <xref:spa/blazor/index> 및 <xref:razor-components/hosting-models#client-side-hosting-model>를 참조하세요.

## <a name="components"></a>구성 요소

‘Razor 구성 요소’는 페이지, 대화 상자 또는 데이터 입력 양식과 같은 UI의 부분입니다. 구성 요소는 사용자 이벤트를 처리하고 유연한 UI 렌더링 논리를 정의합니다. 구성 요소는 중첩 및 재사용될 수 있습니다.

구성 요소는 NuGet 패키지로 공유 및 배포될 수 있는 .NET 어셈블리에 기본 제공된 .NET 클래스입니다. 클래스는 일반적으로 *.razor* 파일 확장자를 가진 Razor 태그 페이지 형식으로 작성됩니다.

[Razor](xref:mvc/views/razor)는 HTML 태그와 C# 코드를 결합하는 구문입니다. Razor는 개발자 생산성을 위해 설계되었으며, 개발자는 [IntelliSense](/visualstudio/ide/using-intellisense) 지원으로 동일한 파일에서 태그와 C# 사이를 전환할 수 있습니다. Razor Pages 및 MVC 뷰에도 Razor를 사용합니다. 요청/응답 모델을 중심으로 빌드된 Razor Pages 및 MVC 뷰와는 달리, 구성 요소는 특별히 UI 컴퍼지션을 처리하는 데 사용됩니다. Razor 구성 요소는 특별히 클라이언트 쪽 UI 논리 및 컴퍼지션에 사용될 수 있습니다.

다음 태그는 Razor 파일(*DialogComponent.razor*)의 사용자 지정 대화 상자 구성 요소의 예입니다.

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

이 구성 요소를 앱의 다른 곳에서 사용할 경우 IntelliSense는 구문 및 매개 변수 완성을 통해 개발 속도를 높입니다.

구성 요소는 유연하고 효율적인 방법으로 UI를 업데이트하는 데 사용할 수 있는 ‘렌더링 트리’라는 브라우저 DOM의 메모리 내 표시로 렌더링됩니다.

## <a name="javascript-interop"></a>JavaScript interop

타사 JavaScript 라이브러리 및 브라우저 API를 필요로 하는 앱의 경우 구성 요소는 JavaScript와 상호 운용됩니다. 구성 요소는 JavaScript가 사용할 수 있는 모든 라이브러리 또는 API를 사용할 수 있습니다. C# 코드는 JavaScript 코드로 호출할 수 있으며, JavaScript 코드는 C# 코드로 호출할 수 있습니다. 자세한 내용은 [JavaScript interop](xref:razor-components/javascript-interop)을 참조하세요.

## <a name="additional-resources"></a>추가 자료

* <xref:spa/blazor/index>
* [WebAssembly](http://webassembly.org/)
* [C# 가이드](/dotnet/csharp/)
* <xref:mvc/views/razor>
* [HTML](https://www.w3.org/html/)
