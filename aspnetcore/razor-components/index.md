---
title: Razor 구성 요소 소개
author: guardrex
description: WebAssembly와 함께 브라우저에서 실행되는 C#/Razor 및 HTML을 사용하여 .NET 웹 프레임워크인 Blazor를 탐색합니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/index
ms.openlocfilehash: 0f7a4b2ec404b6ceec2e643fea9e0635de6ad716
ms.sourcegitcommit: ed76cc752966c604a795fbc56d5a71d16ded0b58
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55667939"
---
# <a name="introduction-to-razor-components"></a>Razor 구성 요소 소개

작성자: [Steve Sanderson](http://blog.stevensanderson.com), [Daniel Roth](https://github.com/danroth27) 및 [Luke Latham](https://github.com/guardrex)

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

*Blazor*(클라이언트 쪽에서 실행되는 Razor 구성 요소)는 WebAssembly와 함께 브라우저에서 실행되는 C#/Razor 및 HTML을 사용하는 실험적인 .NET 웹 프레임워크인 반면, *ASP.NET Core Razor 구성 요소*는 ASP.NET Core에서 서버 쪽을 실행합니다. Blazor는 클라이언트에서 .NET을 사용하는 클라이언트 쪽 웹 UI 프레임워크의 모든 이점을 제공합니다.

웹 개발은 수년에 걸쳐 여러 면에서 개선되었지만, 최신 웹앱을 빌드하는 데는 여전히 어려움이 있습니다. 브라우저에서 .NET을 사용하면 웹 개발을 보다 쉽고 더 생산적으로 만들 수 있는 많은 이점을 얻을 수 있습니다.

* **안정성과 일관성**: .NET은 안정적이고 기능이 풍부하며 사용하기 쉬운 플랫폼 전반에 걸쳐 표준화된 프로그래밍 프레임워크를 제공합니다.
* **최신 혁신 언어**: .NET 언어는 혁신적인 새로운 언어 기능으로 끊임없이 개선되고 있습니다.
* **업계 최고의 도구**: Visual Studio 제품군은 Windows, Linux 및 macOS 플랫폼 전반에 걸쳐 환상적인 .NET 개발 환경을 제공합니다.
* **속도 및 확장성**: .NET은 앱 개발을 위한 성능, 안정성 및 보안에 대한 강력한 기록이 있습니다. .NET을 전체 스택 솔루션으로 사용하면 빠르고 안정적이며 안전한 앱을 쉽게 빌드할 수 있습니다.
* **기존 기술을 활용하는 전체 스택 개발**: C#/ Razor 개발자는 기존 C#/Razor 기술을 사용하여 클라이언트 쪽 코드를 작성하고 앱 간에 서버 및 클라이언트 쪽 논리를 공유합니다.
* **광범위한 브라우저 지원**: Razor 구성 요소는 UI를 일반 태그 및 JavaScript로 렌더링합니다. Blazor는 플러그 인이나 코드 트랜스파일 없이 공개 웹 표준을 사용하여 브라우저의 .NET에서 실행됩니다. Blazor는 모바일 브라우저를 비롯한 모든 최신 웹 브라우저에서 작동합니다.

## <a name="hosting-models"></a>호스팅 모델

### <a name="server-side-hosting-model"></a>서버 쪽 호스팅 모델

Razor 구성 요소는 UI 업데이트가 적용되는 방식과 구성 요소의 렌더링 논리를 분리를 분리하기 때문에 Razor 구성 요소를 호스팅하는 방법에 유연성이 있습니다. .NET Core 3.0의 ASP.NET Core Razor 구성 요소는 SignalR 연결을 통해 모든 UI 업데이트가 처리되는 ASP.NET Core 앱의 서버에서 Razor 구성 요소를 호스팅하는 기능을 추가합니다. 런타임은 브라우저에서 서버로 UI 이벤트 전송을 처리한 다음, 구성 요소를 실행한 후 서버에서 보낸 UI 업데이트를 브라우저에 다시 적용합니다. JavaScript interop 호출을 처리하는 데에도 동일한 연결이 사용됩니다.

![Razor 구성 요소는 서버에서 .NET 코드를 실행하고 SignalR 연결을 통해 클라이언트의 문서 개체 모델과 상호 작용합니다.](index/_static/aspnet-core-razor-components.png)

자세한 내용은 <xref:razor-components/hosting-models#server-side-hosting-model>을 참조하세요.

### <a name="client-side-hosting-model"></a>클라이언트 쪽 호스팅 모델

웹 브라우저 내에서 .NET 코드를 실행하는 것은 비교적 새로운 기술인 [WebAssembly](http://webassembly.org)(약식 *wasm*)를 통해 가능합니다. WebAssembly는 공개 웹 표준이며 플러그 인 없이 웹 브라우저에서 지원됩니다. WebAssembly는 빠른 다운로드와 최대 실행 속도를 위해 최적화된 압축 바이트 코드 형식입니다.

WebAssembly 코드는 JavaScript interop을 통해 브라우저의 전체 기능에 액세스할 수 있습니다. 동시에, WebAssembly 코드는 JavaScript와 동일한 신뢰할 수 있는 샌드박스에서 실행되어 클라이언트 머신에서 악의적인 동작을 방지합니다.

![Blazor는 WebAssembly와 함께 브라우저에서 .NET 코드를 실행합니다.](index/_static/blazor.png)

Blazor 앱이 빌드되고 브라우저에서 실행되는 경우:

1. C# 코드 파일과 Razor 파일은 .NET 어셈블리로 컴파일됩니다.
1. 어셈블리와 .NET 런타임이 브라우저에 다운로드됩니다.
1. Blazor는 JavaScript를 사용하여 .NET 런타임을 부트스트랩하고 필요한 어셈블리 참조를 로드하도록 런타임을 구성합니다. DOM(문서 개체 모델) 조작 및 브라우저 API 호출은 JavaScript 상호 운용성을 통해 Blazor 런타임에 의해 처리됩니다.

WebAssembly를 지원하지 않는 이전 브라우저를 지원하기 위해 ASP.NET Core Razor 구성 요소 [서버 쪽 호스팅 모델](#server-side-hosting-model)을 사용할 수 있습니다.

자세한 내용은 <xref:razor-components/hosting-models#client-side-hosting-model>을 참조하세요.

## <a name="components"></a>구성 요소

앱은 *구성 요소*로 빌드됩니다. 구성 요소는 페이지, 대화 상자 또는 데이터 입력 양식과 같은 UI의 부분입니다. 구성 요소는 프로젝트 간에 중첩, 재사용 및 공유될 수 있습니다.

*구성 요소*는 .NET 클래스입니다. 클래스는 직접 C# 클래스(*\*.cs*)로 작성되거나 Razor 태그 페이지(*\*.cshtml*)의 형태로 작성될 수 있습니다.

[Razor](/aspnet/core/mvc/views/razor)는 HTML 태그와 C# 코드를 결합하는 구문입니다. Razor는 개발자 생산성을 위해 설계되었으며, 개발자는 [IntelliSense](/visualstudio/ide/using-intellisense) 지원으로 동일한 파일에서 태그와 C# 사이를 전환할 수 있습니다. 다음 태그는 Razor 파일(*DialogComponent.cshtml*)의 기본 사용자 지정 대화 상자 구성 요소의 예입니다.

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

구성 요소는 다음과 같습니다.

* 중첩.
* Razor(*\*.cshtml*) 또는 C#(*\*.cs*) 코드로 생성됩니다.
* 클래스 라이브러리를 통해 공유합니다.
* 브라우저 DOM을 요구하지 않는 단위 테스트.

## <a name="infrastructure"></a>인프라

Razor 구성 요소는 다음을 포함하여 대부분의 앱이 필요로 하는 핵심 기능을 제공합니다.

* 레이아웃
* 라우팅
* 종속성 주입

이러한 기능은 모두 선택 사항입니다. 이러한 기능 중 하나가 앱에서 사용되지 않는 경우 [IL(Intermediate Language) 링커](xref:host-and-deploy/razor-components/configure-linker)에서 게시하면 구현이 앱에서 제거됩니다.

## <a name="code-sharing-and-net-standard"></a>코드 공유 및 .NET Standard

앱은 기존 [.NET Standard](/dotnet/standard/net-standard) 라이브러리를 참조하고 사용할 수 있습니다. .NET Standard는 .NET 구현에서 공통적인 .NET API의 공식 사양입니다. .NET Standard 2.0 이상이 지원됩니다. 웹 브라우저 내에서 적용되지 않는 API(예: 파일 시스템 액세스, 소켓 열기, 스레딩 및 기타 기능)에서 [PlatformNotSupportedException](/dotnet/api/system.platformnotsupportedexception)을 throw합니다. .NET Standard 클래스 라이브러리는 서버 코드와 브라우저 기반 앱에서 공유할 수 있습니다.

## <a name="javascript-interop"></a>JavaScript interop

타사 JavaScript 라이브러리 및 브라우저 API를 필요로 하는 앱의 경우, WebAssembly는 JavaScript와 상호 운용하도록 디자인되었습니다. Razor 구성 요소는 JavaScript가 사용할 수 있는 모든 라이브러리 또는 API를 사용할 수 있습니다. C# 코드는 JavaScript 코드로 호출할 수 있으며, JavaScript 코드는 C# 코드로 호출할 수 있습니다. 자세한 내용은 [JavaScript interop](xref:razor-components/javascript-interop)을 참조하세요.

## <a name="optimization"></a>최적화

클라이언트 쪽 앱의 경우 페이로드 크기가 중요합니다. Blazor는 페이로드 크기를 최적화하여 다운로드 시간을 줄입니다. 예를 들어 .NET 어셈블리의 사용하지 않는 부분은 빌드 프로세스 중에 제거되고, HTTP 응답은 압축되며 .NET 런타임 및 어셈블리는 브라우저에 캐시됩니다.

Razor 구성 요소는 .NET 어셈블리, 앱의 어셈블리 및 런타임 서버 쪽을 유지 관리하여 Blazor보다 작은 페이로드 크기를 제공합니다. Razor 구성 요소 앱은 태그, 스크립트 및 스타일시트만 제공합니다.

## <a name="deployment"></a>배포

Blazor를 사용하여 순수 독립 실행형 클라이언트 쪽 앱 또는 서버 및 클라이언트 앱이 모두 포함된 전체 스택 ASP.NET Core 앱을 빌드합니다.

* **독립 실행형 클라이언트 쪽 앱**에서 Blazor 앱은 정적 파일만 포함하는 *dist* 폴더로 컴파일됩니다. Azure App Service, GitHub 페이지, IIS(정적 파일 서버로 구성), Node.js 서버 및 기타 여러 서버와 서비스에서 파일을 호스팅할 수 있습니다. 프로덕션 환경에서는 서버에 .NET이 필요하지 않습니다.
* **전체 스택 ASP.NET Core 앱**에서 서버와 클라이언트 앱 간에 코드를 공유할 수 있습니다. 클라이언트 쪽 UI 및 다른 서버 쪽 API 엔드포인트를 제공하는 결과 ASP.NET Core Razor 구성 요소 앱은 ASP.NET Core가 지원하는 모든 클라우드 또는 온-프레미스 호스트에 빌드 및 배포할 수 있습니다.

## <a name="suggest-a-feature-or-file-a-bug-report"></a>기능 또는 파일 버그 보고서 제안

제안 및 파일 버그 보고서를 만들려면 [문제를 제기](https://github.com/aspnet/AspNetCore/issues/new)하세요. 일반적인 도움말 및 커뮤니티에서 답변을 얻으려면 [Gitter](https://gitter.im/aspnet/Blazor)에 대한 대화에 참여합니다.

## <a name="additional-resources"></a>추가 자료

* [WebAssembly](http://webassembly.org/)
* [C# 가이드](/dotnet/csharp/)
* [Razor](/aspnet/core/mvc/views/razor)
* [HTML](https://www.w3.org/html/)
