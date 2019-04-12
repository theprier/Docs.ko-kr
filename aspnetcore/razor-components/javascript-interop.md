---
title: Razor 구성 요소가 JavaScript interop
author: guardrex
description: .NET 및.NET에서 JavaScript 함수를 호출 하는 방법을 알아봅니다 Blazor 및 Razor 구성 요소 앱에서 JavaScript에서 메서드.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 04/08/2019
uid: razor-components/javascript-interop
ms.openlocfilehash: f2588f4ed1ec2f01218283625fae4632d0a8ae58
ms.sourcegitcommit: 948e533e02c2a7cb6175ada20b2c9cabb7786d0b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2019
ms.locfileid: "59515679"
---
# <a name="razor-components-javascript-interop"></a>Razor 구성 요소가 JavaScript interop

하 여 [Javier Calvarro 박](https://github.com/javiercn)하십시오 [Daniel Roth](https://github.com/danroth27), 및 [Luke Latham](https://github.com/guardrex)

구성 요소 Razor 앱을.NET 및.NET에서 JavaScript 함수를 호출할 수 JavaScript 코드에서 메서드.

## <a name="invoke-javascript-functions-from-net-methods"></a>.NET 메서드에서 JavaScript 함수를 호출 합니다.

.NET 코드를 JavaScript 함수를 호출 해야 하는 경우 경우가 있습니다. 예를 들어 JavaScript 호출을 브라우저 기능 또는 앱에 JavaScript 라이브러리에서 기능을 노출할 수 있습니다.

.NET에서 JavaScript로 호출을 사용 하 여는 `IJSRuntime` 추상화 합니다. `InvokeAsync<T>` 메서드는 모든 JSON 직렬화 가능 인수 개수와 함께 호출 하려는 JavaScript 함수에 대 한 식별자를 사용 합니다. 전역 범위와 관련 된 함수 식별자가 (`window`). 호출 하려는 경우 `window.someScope.someFunction`, 식별자가 `someScope.someFunction`합니다. 가 호출 되기 전에 함수를 등록 하려면 않아도가 됩니다. 반환 형식은 `T` 도 JSON 직렬화 해야 합니다.

서버 쪽 ASP.NET Core Razor 구성 요소 앱:

* 서버 쪽 앱에서 여러 사용자 요청을 처리 합니다. 호출 하지 마십시오 `JSRuntime.Current` JavaScript 함수를 호출 하는 구성 요소에 있습니다.
* 삽입 된 `IJSRuntime` 추상화 및 JavaScript interop 호출에 삽입 된 개체를 사용 하 여 합니다.

다음 예제는 기반 [TextDecoder](https://developer.mozilla.org/docs/Web/API/TextDecoder), 실험적 JavaScript 기반 디코더는 합니다. JavaScript 함수를 호출 하는 방법을 보여 줍니다는 C# 메서드. JavaScript 함수에서 바이트 배열을 취하는 C# 메서드를 배열의 디코딩하고 표시에 대 한 구성 요소에 텍스트를 반환 합니다.

내 합니다 `<head>` 요소의 *wwwroot/index.html*를 사용 하는 함수를 제공 `TextDecoder` 전달 된 배열을 디코드 하려면:

```html
<script>
  window.ConvertArray = (win1251Array) => {
    var win1251decoder = new TextDecoder('windows-1251');
    var bytes = new Uint8Array(win1251Array);
    var decodedArray = win1251decoder.decode(bytes);
    console.log(decodedArray);
    return decodedArray;
  };
</script>
```

앞의 예제에 표시 된 코드와 같은 JavaScript 코드를 JavaScript 파일에서 로드할 수도 있습니다 (*.js*)에서 스크립트 파일에 대 한 참조를 사용 하 여 합니다 *wwwroot/index.html* 파일:

```html
<script src="exampleJsInterop.js"></script>
```

다음 구성 요소:

* 호출 하는 `ConvertArray` JavaScript 함수를 사용 하 여 `JsRuntime` 구성 단추 (**변환 배열**) 선택 합니다.
* JavaScript 함수를 호출한 다음 전달된 된 배열은 문자열로 변환 됩니다. 표시에 대 한 구성 요소에는 문자열이 반환 됩니다.

```cshtml
@page "/"
@inject IJSRuntime JsRuntime;

<h1>Call JavaScript Function Example</h1>

<button type="button" class="btn btn-primary" onclick="@ConvertArray">
    Convert Array
</button>

<p class="mt-2" style="font-size:1.6em">
    <span class="badge badge-success">
        @ConvertedText
    </span>
</p>

@functions {
    // Quote (c)2005 Universal Pictures: Serenity
    // https://www.uphe.com/movies/serenity
    // David Krumholtz on IMDB: https://www.imdb.com/name/nm0472710/

    private MarkupString ConvertedText =
        new MarkupString("Select the <b>Convert Array</b> button.");

    private uint[] QuoteArray = new uint[]
        {
            60, 101, 109, 62, 67, 97, 110, 39, 116, 32, 115, 116, 111, 112, 32,
            116, 104, 101, 32, 115, 105, 103, 110, 97, 108, 44, 32, 77, 97,
            108, 46, 60, 47, 101, 109, 62, 32, 45, 32, 77, 114, 46, 32, 85, 110,
            105, 118, 101, 114, 115, 101, 10, 10,
        };

    private async void ConvertArray()
    {
        var text =
            await JsRuntime.InvokeAsync<string>("ConvertArray", QuoteArray);

        ConvertedText = new MarkupString(text);

        StateHasChanged();
    }
}
```

사용 하는 `IJSRuntime` 추상화를 채택 하는 다음 방법 중 하나:

* 삽입 된 `IJSRuntime` 추상화를 Razor 파일 (*.razor*, *.cshtml*):

  ```cshtml
  @inject IJSRuntime JSRuntime

  @functions {
      public override void OnInit()
      {
          StocksService.OnStockTickerUpdated += stockUpdate =>
          {
              JSRuntime.InvokeAsync<object>(
                  "handleTickerChanged",
                  stockUpdate.symbol,
                  stockUpdate.price);
          };
      }
  }
  ```

* 삽입 된 `IJSRuntime` 클래스로 추상화 (*.cs*):

  ```csharp
  public class JsInteropClasses
  {
      private readonly IJSRuntime _jsRuntime;

      public JsInteropClasses(IJSRuntime jsRuntime)
      {
          _jsRuntime = jsRuntime;
      }

      public Task<string> TickerChanged(string data)
      {
          // The handleTickerChanged JavaScript method is implemented
          // in a JavaScript file, such as 'wwwroot/tickerJsInterop.js'.
          return _jsRuntime.InvokeAsync<object>(
              "handleTickerChanged",
              stockUpdate.symbol,
              stockUpdate.price);
      }
  }
  ```

* 사용 하 여 동적 콘텐츠 생성에 대 한 `BuildRenderTree`를 사용 하 여는 `[Inject]` 특성:

  ```csharp
  [Inject] IJSRuntime JSRuntime { get; set; }
  ```

이 항목과 관련 된 클라이언트 쪽 샘플 앱에서 두 JavaScript 함수는 사용자 입력을 받는 환영 메시지를 표시 하는 DOM과 상호 작용 하는 클라이언트 쪽 앱에 사용할 수 있습니다.

* `showPrompt` &ndash; 사용자 입력 (사용자 이름)를 수락할 프롬프트를 생성 하 고 호출자에 게 이름을 반환 합니다.
* `displayWelcome` &ndash; 환영 메시지를 호출자에서 사용 하 여 DOM 개체를 할당 한 `id` 의 `welcome`합니다.

*wwwroot/exampleJsInterop.js*:

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=2-7)]

위치는 `<script>` JavaScript 파일에서 참조 하는 태그를 *wwwroot/index.html* 파일:

[!code-html[](./common/samples/3.x/BlazorSample/wwwroot/index.html?highlight=15)]

놓지 마십시오를 `<script>` 때문에 구성 요소 파일에 태그를 `<script>` 태그를 동적으로 업데이트할 수 없습니다.

JavaScript 사용 하 여.NET 메서드 interop의 함수는 *exampleJsInterop.js* 를 호출 하 여 파일 `IJSRuntime.InvokeAsync<T>`합니다.

`IJSRuntime` 추상화는 비동기 서버 쪽 시나리오에 대 한 허용 하도록 합니다. 클라이언트 쪽 앱이 실행 되는 JavaScript 함수를 동기적으로 호출 하려는 경우에 다운 `IJSInProcessRuntime` 호출 `Invoke<T>` 대신 합니다. 대부분의 JavaScript interop 라이브러리 비동기 Api를 사용 하 여 라이브러리를 모든 시나리오에서 클라이언트 쪽 또는 서버 쪽에서 사용할 수 있는지 확인 하는 것이 좋습니다.

샘플 앱은 JavaScript 상호 운용성을 보여 주기 위해 구성 요소를 포함 합니다. 구성 요소:

* JavaScript 프롬프트를 통해 사용자 입력을 받습니다.
* 처리에 대 한 구성 요소에 텍스트를 반환합니다.
* 시작 메시지를 표시 하려면 DOM과 상호 작용 하는 두 번째 JavaScript 함수를 호출 합니다.

*Pages/JSInterop.cshtml*:

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?name=snippet_JSInterop1&highlight=3,19-21,23-25)]

1. 때 `TriggerJsPrompt` 구성 요소를 선택 하 여 실행 됩니다 **트리거 JavaScript 프롬프트** 단추를 JavaScript `showPrompt` 함수에 제공 합니다 *wwwroot/exampleJsInterop.js* 파일은 호출 됩니다.
1. `showPrompt` HTML 인코딩 및 구성 요소에 반환 된 사용자 입력 (사용자 이름)을 허용 하는 함수입니다. 구성 요소를 로컬 변수에 사용자 이름을 저장 `name`합니다.
1. 문자열에 저장 `name` 는 JavaScript 함수에 전달 되는 환영 메시지를 통합 `displayWelcome`를 환영 메시지 머리글 태그로 렌더링 합니다.

## <a name="capture-references-to-elements"></a>요소에 대 한 참조를 캡처

일부 [JavaScript interop](xref:razor-components/javascript-interop) 시나리오에는 HTML 요소에 대 한 참조가 필요 합니다. 예를 들어, UI 라이브러리 요소 참조를 초기화 해야 할 수 있습니다 또는 같은 요소에 대해 비슷한 Api를 호출 해야 할 수 있습니다 `focus` 또는 `play`합니다.

구성 요소에서 HTML 요소에 대 한 참조를 추가 하 여 캡처할 수 있습니다는 `ref` HTML 요소에 특성 및 다음 형식의 필드를 정의할 `ElementRef` 이름이 값과 일치는 `ref` 특성입니다.

다음 예제에서는 사용자 입력된 요소에 대 한 참조를 캡처를 보여 줍니다.

```cshtml
<input ref="username" ...>

@functions {
    ElementRef username;
}
```

> [!NOTE]
> 수행할 **되지** DOM을 채우는 방법으로 캡처된 요소 참조를 사용 합니다. 이렇게 선언적 렌더링 모델을 방해할 수 있습니다.

.NET 코드와 관련 된 관련해 서는 `ElementRef` 불투명 핸들입니다. 합니다 *만* 작업을 수행할 수 있습니다 `ElementRef` JavaScript interop을 통해 JavaScript 코드를 통해 전달 됩니다. 이렇게 하면 JavaScript 쪽 코드를 받는 `HTMLElement` 인스턴스 일반 DOM Api를 사용 하 여 사용할 수 있습니다.

예를 들어, 다음 코드 요소에 포커스를 설정 하는 수 있게 해 주는.NET 확장 메서드를 정의 합니다.

*exampleJsInterop.js*:

```javascript
window.exampleJsFunctions = {
  focusElement : function (element) {
    element.focus();
  }
}
```

사용 하 여 `IJSRuntime.InvokeAsync<T>` 호출 `exampleJsFunctions.focusElement` 사용 하 여는 `ElementRef` 요소를 집중할 수:

[!code-cshtml[](javascript-interop/samples_snapshot/component1.cshtml?highlight=1,3,7,11-12)]

요소에 집중 하는 확장 메서드를 사용 하려면 수신 하는 정적 확장 메서드를 만들기는 `IJSRuntime` 인스턴스:

```csharp
public static Task Focus(this ElementRef elementRef, IJSRuntime jsRuntime)
{
    return jsRuntime.InvokeAsync<object>(
        "exampleJsFunctions.focusElement", elementRef);
}
```

개체에 직접 메서드 호출 됩니다. 다음 예에서는 가정 정적 `Focus` 메서드는에서 사용할 수는 `JsInteropClasses` 네임 스페이스:

[!code-cshtml[](javascript-interop/samples_snapshot/component2.cshtml?highlight=1,4,8,12)]

> [!IMPORTANT]
> 합니다 `username` 변수는 구성 요소를 렌더링 하 고 해당 출력을 포함 한 후에 채워집니다는 `>` 요소입니다. 채워지지를 전달 하려고 하면 `ElementRef` JavaScript 코드에 JavaScript 코드를 받는 `null`합니다. 구성 요소 사용 (초기 포커스 요소에 설정)로 렌더링을 마친 후 요소 참조를 조작 하는 `OnAfterRenderAsync` 나 `OnAfterRender` [구성 요소 수명 주기 메서드](xref:razor-components/components#lifecycle-methods)합니다.

## <a name="invoke-net-methods-from-javascript-functions"></a>JavaScript 함수에서.NET 메서드를 호출 합니다.

### <a name="static-net-method-call"></a>정적.NET 메서드 호출

JavaScript에서 정적.NET 메서드를 호출 하려면 사용 합니다 `DotNet.invokeMethod` 또는 `DotNet.invokeMethodAsync` 함수입니다. 정적 메서드를 호출 하 고 함수 및 인수를 포함 하는 어셈블리의 이름을 하려는의 식별자를 전달 합니다. 비동기 버전은 서버 쪽 시나리오를 지원 하도록 기본 설정입니다. JavaScript에서 호출 되도록.NET 메서드는 이어야 합니다 public, 정적 및 사용 하 여 데코 레이트 된 `[JSInvokable]`합니다. 기본적으로 메서드 식별자 메서드 이름 이지만 사용 하 여 다른 식별자를 지정할 수 있습니다는 `JSInvokableAttribute` 생성자입니다. 개방형 제네릭 메서드를 호출 합니다. 현재 지원 되지 않습니다.

샘플 앱에 포함 되어는 C# 배열을 반환 하는 방법 `int`s입니다. 로 데코레이팅된 메서드는 `JSInvokable` 특성입니다.

*Pages/JsInterop.cshtml*:

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?name=snippet_JSInterop2&highlight=7-11)]

클라이언트에 제공 하는 JavaScript를 호출 하는 C# .NET 메서드.

*wwwroot/exampleJsInterop.js*:

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=8-14)]

경우는 **트리거.NET 정적 메서드에 ReturnArrayAsync** 단추를 선택한 경우 브라우저의 웹 개발자 도구에서 콘솔 출력을 검토 합니다.

콘솔 출력은 다음과 같습니다.

```console
Array(4) [ 1, 2, 3, 4 ]
```

네 번째 배열 값을 배열에 푸시됩니다. (`data.push(4);`)에서 반환 된 `ReturnArrayAsync`합니다.

### <a name="instance-method-call"></a>인스턴스 메서드 호출

또한 JavaScript에서.NET 인스턴스 메서드를 호출할 수 있습니다. JavaScript에서.NET 인스턴스 메서드를 호출 하려면 먼저 전달할.NET 인스턴스 JavaScript에 래핑하여는 `DotNetObjectRef` 인스턴스. .NET 인스턴스 JavaScript로 참조로 전달 되 고 사용 하 여 인스턴스에 대 한.NET 인스턴스 메서드를 호출할 수 있습니다 합니다 `invokeMethod` 또는 `invokeMethodAsync` 함수입니다. JavaScript에서 다른.NET 메서드를 호출 하는 경우.NET 인스턴스를 인수로 전달할 수도 있습니다.

> [!NOTE]
> 샘플 앱은 클라이언트 콘솔에 메시지를 기록합니다. 샘플 앱에서 보여 주는 다음 예제에 대 한 브라우저의 개발자 도구에서 브라우저의 콘솔 출력을 검사 합니다.

경우는 **HelloHelper.SayHello 트리거.NET 인스턴스 메서드** 단추를 선택 하면 `ExampleJsInterop.CallHelloHelperSayHello` 라고 하 고 이름을 전달 `Blazor`, 메서드.

*Pages/JsInterop.cshtml*:

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?name=snippet_JSInterop3&highlight=8-9)]

`CallHelloHelperSayHello` JavaScript 함수를 호출 `sayHello` 의 새 인스턴스를 사용 하 여 `HelloHelper`입니다.

*JsInteropClasses/ExampleJsInterop.cs*:

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/ExampleJsInterop.cs?name=snippet1&highlight=10-16)]

*wwwroot/exampleJsInterop.js*:

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=15-18)]

이름에 전달 됩니다 `HelloHelper`의 설정 하는 생성자를 `HelloHelper.Name` 속성입니다. 때 JavaScript 함수 `sayHello` 실행 됩니다 `HelloHelper.SayHello` 반환을 `Hello, {Name}!` JavaScript 함수에 의해 콘솔에 기록 되는 메시지입니다.

*JsInteropClasses/HelloHelper.cs*:

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/HelloHelper.cs?name=snippet1&highlight=5,10-11)]

브라우저의 웹 개발자 도구에서 출력을 콘솔:

```console
Hello, Blazor!
```

## <a name="share-interop-code-in-a-razor-component-class-library"></a>구성 요소 Razor 클래스 라이브러리에서 interop 코드 공유

구성 요소 Razor 클래스 라이브러리에 JavaScript interop 코드를 포함할 수 있습니다 (`dotnet new razorclasslib`), NuGet 패키지의 코드를 공유할 수 있습니다.

구성 요소 Razor 클래스 라이브러리는 빌드된 어셈블리에 포함 JavaScript 리소스를 처리합니다. JavaScript 파일에 배치 되는 *wwwroot* 폴더입니다. 라이브러리를 빌드할 때 리소스를 포함 하는의 도구를 담당 합니다.

기본 제공된 NuGet 패키지를 기본 NuGet 패키지 참조 하는 것 처럼 앱의 프로젝트 파일에서 참조 됩니다. 앱 복원 되 면 앱 코드 것 처럼 JavaScript에 호출할 수 있습니다 C#입니다.

자세한 내용은 <xref:razor-components/class-libraries>을 참조하세요.
