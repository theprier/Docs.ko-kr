---
title: 사이트 간 스크립팅 (XSS) ASP.NET Core에서 방지
author: rick-anderson
description: 사이트 간 스크립팅 (XSS) 및 ASP.NET Core 앱에서이 취약성을 해결 하는 방법에 알아봅니다.
ms.author: riande
ms.date: 10/02/2018
uid: security/cross-site-scripting
ms.openlocfilehash: 50f0211a2c64708d9b788dd10ce9064e66014d55
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48910527"
---
# <a name="prevent-cross-site-scripting-xss-in-aspnet-core"></a>ASP.NET Core에서 크로스 사이트 스크립트 공격(XSS) 방지

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

크로스 사이트 스크립팅(XSS)은 공격자가 웹페이지에 Javascript와 같은 클라이언트 사이드 스크립트를 웹페이지에 배치하도록 하는 보안 취약점을 일컫습니다. 다른 사용자가 공격당한 페이지를 로드할 경우 공격자의 스크립트가 실행되며, 쿠키 및 세션 토큰을 탈취하거나 DOM을 조작하여 페이지 내용을 변경하고, 혹은 다른 페이지로 이동시킬 수 있습니다. XSS 취약점은 보통 검증을 거치지 않은 사용자 입력이나 출력을 검증하거나, 암호화, 혹은 이스케이핑 하지 않을때 발생합니다.  

## <a name="protecting-your-application-against-xss"></a>애플리케이션을 XSS로부터 보호하기

기본적인 단계의 XSS는 렌더링 된 페이지에 `<script>` 태그를 삽입하거나, On 계열의 이벤트를 DOM 요소에 삽입할 때 발생합니다. 개발자들은 이러한 XSS 공격으로부터 방어하기 위해 다음과 같은 조치를 취하여야 합니다.

1. 신뢰할 수 없는 데이터를 나머지 단계를 거치지 않은 이상 HTML 입력에 삽입하지 마십시오. 신뢰할 수 없는 데이터란 공격자의 제어 하에 있을 수 있거나, 폼 입력, 쿼리 문자열, HTTP 헤더, 혹은 공격받았을 수도 있는 데이터베이스로부터 가져온 값 모두를 의미합니다.

2. 신뢰할 수 없는 데이터를 HTML 요소에 삽입하기 전 HTML 인코딩 되었는지 확인하십시오. 예를 들어, `<` 와 같은 문자열을 `&lt;` 등과 같이 안전한 형태로 바꾸는 것과 같습니다.

3. 신뢰할 수 없는 데이터를 HTML 어트리뷰트에 삽입하기 전 HTML 인코딩 되었는지 확인하십시오. HTML 어트리뷰트 인코딩은 HTML 인코딩의 상위집합으로, `"` 나 `'`와 같은 문자들을 추가적으로 인코딩하는 과정입니다.

4. 신뢰할 수 없는 데이터를 Javascript에 삽입하기 전, 런타임에 가져오는 HTML 요소에 데이터를 배치하십시오. 만일 불가능한 경우, 데이터가 JavaScript 인코딩되었는지 확인하십시오. JavaScript 인코딩은  스크립트 동작을 변조할 수 있는 위험한 문자들을 hex 값으로 변환하는 과정으로, `<`를 `\u003C` 로 변환하는 것을 의미합니다.

5. 신뢰할 수 없는 데이터를 URL 쿼리 문자열에 삽입하기 전, URL 인코딩 되었는지 확인하십시오.

## <a name="html-encoding-using-razor"></a>Razor를 이용한 HTML 인코딩

ASP.NET MVC에서 사용되는 Razor 엔진은 XSS를 방지처리를 거치지 않은 변수로부터 유래하는 모든 출력을 자동으로 인코딩합니다. @ 지시자를 사용할때마다 HTML 어트리뷰트 인코딩을 수행합니다. HTML 어트리뷰트 인코딩이 HTML 인코딩의 상위 집합이므로, 개발자는 어떤 것을 사용해야 할 지에 대해 고민할 필요가 없습니다. 신뢰할 수 없는 데이터를 JavaScript에 직접 삽입하지 말고, HTML 컨텍스트 내에서만 @ 지시자를 사용하십시오. 태그 헬퍼 또한 파라메터로 넘겨준 입력값을 인코드 해 줍니다.

다음 Razor View를 살펴봅시다.

```cshtml
   @{
       var untrustedInput = "<\"123\">";
   }

   @untrustedInput
   ```

이 View는 `untrustedInput` 변수의 내용을 출력합니다. 이 변수는 `<`, `"`, `>` 와 같이 XSS 공격에 사용되는 문자들을 담고 있습니다. 이 소스의 렌더링 결과는 다음과 같습니다.

```html
&lt;&quot;123&quot;&gt;
```

>[!WARNING]
> ASP.NET Core MVC는 자동으로 인코딩 되지 않는 `HtmlString` 클래스를 제공합니다. XSS 취약점을 방지하기 위하여 절대로 신뢰할 수 없는 데이터와 함께 사용하지 마십시오. 

## <a name="javascript-encoding-using-razor"></a>Razor를 이용한 JavaScript 인코딩

간혹 View 처리 과정에서 JavaScript에 값을 삽입하고 싶을 수 있습니다. 그런 경우 두가지 방법이 있습니다. 제일 안전한 방법으로는 data 어트리뷰트에 값을 삽입하고 JavaScript에서 가져오도록 하면 됩니다.

```cshtml
   @{
       var untrustedInput = "<\"123\">";
   }

   <div
       id="injectedData"
       data-untrustedinput="@untrustedInput" />

   <script>
     var injectedData = document.getElementById("injectedData");

     // All clients
     var clientSideUntrustedInputOldStyle =
         injectedData.getAttribute("data-untrustedinput");

     // HTML 5 clients only
     var clientSideUntrustedInputHtml5 =
         injectedData.dataset.untrustedinput;

     document.write(clientSideUntrustedInputOldStyle);
     document.write("<br />")
     document.write(clientSideUntrustedInputHtml5);
   </script>
   ```
   
이 코드로부터 다음과 같은 HTML이 생성됩니다.

```html
<div
     id="injectedData"
     data-untrustedinput="&lt;&quot;123&quot;&gt;" />

   <script>
     var injectedData = document.getElementById("injectedData");

     var clientSideUntrustedInputOldStyle =
         injectedData.getAttribute("data-untrustedinput");

     var clientSideUntrustedInputHtml5 =
         injectedData.dataset.untrustedinput;

     document.write(clientSideUntrustedInputOldStyle);
     document.write("<br />")
     document.write(clientSideUntrustedInputHtml5);
   </script>
   ```

그리고 다음과 같은 렌더링 결과를 얻을 수 있습니다.

```none
<"123">
   <"123">
   ```

또한 JavaScript 인코더를 직접 호출할 수도 있습니다.

```cshtml
@using System.Text.Encodings.Web;
   @inject JavaScriptEncoder encoder;

   @{
       var untrustedInput = "<\"123\">";
   }

   <script>
       document.write("@encoder.Encode(untrustedInput)");
   </script>
   ```

그럼 다음과 같이 렌더링 됩니다.

```html
<script>
       document.write("\u003C\u0022123\u0022\u003E");
   </script>
   ```

>[!WARNING]
> 절대 DOM 요소를 생성하기 위해 신뢰할 수 없는 데이터를 JavaScript와 연결하지 마십시오. `createElement()`를 이용하여 요소를 생성한 후 `node.TextContent=` 나 `element.setAttribute()`를 이용하여 속성값을 대입해 주어야 합니다. 그렇지 않은 경우 DOM 기반 XSS 취약점이 발생합니다.

## <a name="accessing-encoders-in-code"></a>코드에서 인코더에 접근하기

HTML, JavaScript 및 URL 인코더는 두 가지 방법으로 코드에서 이용할 수 있습니다. [종속성 주입](xref:fundamentals/dependency-injection)을 이용하거나, `System.Text.Encodings.Web` 네임스페이스에 포함된 기본 인코더를 사용할 수 있습니다. 만일 기본 인코더를 사용하는 경우 가장 안전한 인코딩 규칙을 사용하므로 개발자가 직접 정의한 안전 문자 범위는 적용되지 않습니다.

종속성 주입을 이용하여 설정 가능한 인코더를 사용하려는 경우 생성자에 `HtmlEncoder`, `JavaScriptEncoder`, 그리고 `UrlEncoder`를 파라메터로 적절하게 넘겨주어야 합니다. 예를 들어봅시다.

```csharp
public class HomeController : Controller
   {
       HtmlEncoder _htmlEncoder;
       JavaScriptEncoder _javaScriptEncoder;
       UrlEncoder _urlEncoder;

       public HomeController(HtmlEncoder htmlEncoder,
                             JavaScriptEncoder javascriptEncoder,
                             UrlEncoder urlEncoder)
       {
           _htmlEncoder = htmlEncoder;
           _javaScriptEncoder = javascriptEncoder;
           _urlEncoder = urlEncoder;
       }
   }
   ```

## <a name="encoding-url-parameters"></a>URL 매개변수 인코딩

신뢰할 수 없는 입력을 이용하여 URL 쿼리 문자열을 만들고자 하는 경우, `UrlEncoder`를 사용하십시오. 예를 들어,

```csharp
var example = "\"Quoted Value with spaces and &\"";
   var encodedValue = _urlEncoder.Encode(example);
   ```
   
인코딩 이후 `encodedValue` 변수의 값은 `%22Quoted%20Value%20with%20spaces%20and%20%26%22`가 됩니다. 공백, 따옴표, 마침표, 그리고 기타 안전하지 않은 문자들은 URL 인코딩 됩니다. 예를 들어, 공백 문자는 `%20` 으로 인코딩됩니다.

>[!WARNING]
> 신뢰할 수 없는 데이터를 URL 경로에 사용하지 마십시오. 항상 쿼리 문자열의 값으로서 전달되어야 합니다.

<a name="security-cross-site-scripting-customization"></a>

## <a name="customizing-the-encoders"></a>사용자 지정 인코더 제작하기

기본 인코더가 사용하는 화이트리스트는 기본 라틴 유니코드 페이지에 한정되어 있으며, 이 외의 모든 문자들을 해당하는 문자 코드로 인코딩합니다. 이러한 동작은 Razor TagHelper와 HtmlHelper가 사용하는 인코더가 렌더링 하는 문자열에 영향을 줍니다. 

이것은 알 수 없거나 이후의 브라우저 버그들(이전의 브라우저 버그가 비 영문권 문자들을 처리하는데 방해가 되었기에)들을 막기 위한 조치입니다. 만일 사이트가 한자, 키릴 문자와 같은 비 라틴계 문자를 대량으로 사용하는 경우 개발자에게 원치 않는 동작일 것입니다. 

`ConfigureServices()`에 적절한 인코더 화이트리스트를 직접 정의할 수 있습니다.

예를 들어, 기본 구성을 이용하여 Razor HtmlHelper를 이용한다면 다음과 같습니다.

```html
<p>This link text is in Chinese: @Html.ActionLink("汉语/漢語", "Index")</p>
   ```

브라우저에서 소스를 확인하면 다음과 같이 렌더링 된 것을 확인할 수 잇습니다.

```html
<p>This link text is in Chinese: <a href="/">&#x6C49;&#x8BED;/&#x6F22;&#x8A9E;</a></p>
   ```
   
화이트리스트의 범위를 넓히고 싶은 경우 `startup.cs` 내의 `ConfigureServices()` 에서 다음과 같이 코드를 작성하여 주면 됩니다.

```csharp
services.AddSingleton<HtmlEncoder>(
     HtmlEncoder.Create(allowedRanges: new[] { UnicodeRanges.BasicLatin,
                                               UnicodeRanges.CjkUnifiedIdeographs }));
   ```

이 예제에서는 `CjkUnifiedIdeographs`의 유니코드 범위를 포함 하도록 화이트리스트를 확대했습니다. 이후 렌더링 된 결과는 다음과 같습니다.

```html
<p>This link text is in Chinese: <a href="/">汉语/漢語</a></p>
   ```

화이트리스트 범위는 언어가 아닌 유니코드 차트로서 명시되어 있습니다. [유니코드 표준](http://unicode.org/)은 이러한 [코드 차트](http://www.unicode.org/charts/index.html) 목록을 가지고 있으며 필요한 문자가 포함 된 차트를 찾는 데 사용할 수 있습니다. 각각의 인코더(Html, JavaScript, Url) 는 반드시 개별적으로 구성되어야 합니다.

> [!NOTE]
> 화이트리스팅 설정은 종속성 주입에 의해 생성된 인코더에서만 적용됩니다. `System.Text.Encodings.Web.*Encoder.Default` 를 통하여 직접 사용할 경우 기본 라틴계열 문자만 화이트리스팅 됩니다.

## <a name="where-should-encoding-take-place"></a>인코딩이 일어나야할 시점

일반적으로 인코딩은 출력 시점에 이루어져야 하며 절대로 데이터베이스에 입력되어선 안됩니다. 출력 시점의 인코딩은 HTML에서 쿼리 문자열 값으로 변경하듯 데이터의 용도를 변경할 수 있습니다. 이는 검색 전 값을 인코딩 하지 않고도 쉽게 자료를 찾을 수 있도록 하며 인코더의 변경이나 버그 수정으로부터 이점을 가질 수 있도록 합니다.

## <a name="validation-as-an-xss-prevention-technique"></a>XSS 방지 기술로서의 유효성 검사

유효성 검사 역시 XSS 공격 방지에 유용한 도구가 될 수 있습니다. 예를 들어 0에서 9 까지의 문자만 포함 된 숫자 문자열은 XSS 공격을 일으키지 않습니다. 이러한 검사 과정은 HTML을 사용자 입력으로서 받아들일 때 더욱 복잡해집니다. HTML 입력을 파싱하는것은 불가능 하지는 않으나 어렵습니다. Markdown과 같이 파서가 삽입된 HTML을 제거하도록 하는 기능은 다채로운 입력을 받을 때 더욱 안전한 선택일 것입니다. 절대로 유효성 검사에만 의존하지 마십시오. 어떠한 검증이나 처리가 이루어 졌다 하더라도, 항상 출력 전 신뢰할 수 없는 입력을 인코딩하시기 바랍니다.
