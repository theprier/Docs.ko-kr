---
title: 사이트 간 스크립팅 (XSS) ASP.NET Core에서 방지
author: rick-anderson
description: 사이트 간 스크립팅 (XSS) 및 ASP.NET Core 앱에서이 취약성을 해결 하는 방법에 알아봅니다.
ms.author: riande
ms.date: 10/02/2018
uid: security/cross-site-scripting
ms.openlocfilehash: e937ce47b7151155197cd607832eeb6bf62e3a19
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48577446"
---
# <a name="prevent-cross-site-scripting-xss-in-aspnet-core"></a>사이트 간 스크립팅 (XSS) ASP.NET Core에서 방지

작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)

사이트 간 스크립팅 (XSS)는 보안 취약점으로 인 한 공격자가 클라이언트 측 스크립트 (일반적으로 JavaScript) 웹 페이지에 배치할 수 있도록 하는 경우 공격자가 스크립트를 실행 하는 영향을 받는 페이지를 로드 하는 다른 사용자를 공격자가 쿠키를 도용 하는 세션 토큰에 사용 하도록 설정 DOM 조작을 통해 웹 페이지의 콘텐츠를 변경 또는 다른 페이지로 브라우저를 리디렉션하십시오. XSS 취약성으로 인 한 응용 프로그램은 사용자 입력 하 고 유효성 검사, 인코딩 또는 해 서 이스케이프 없이 페이지에서 출력 하는 경우에 일반적으로 발생 합니다.

## <a name="protecting-your-application-against-xss"></a>XSS에 대 한 응용 프로그램 보호

삽입에 응용 프로그램을 속여에 기본 수준 XSS 작동는 `<script>` 렌더링 된 페이지 또는 삽입 하 여 태그를 `On*` 요소로 이벤트. 개발자가 응용 프로그램에 XSS를 소개 하지 않으려면 다음 방지 단계를 사용 해야 합니다.

1. 나머지 아래 단계를 수행 하지 않으면 사용자의 HTML 입력에 신뢰할 수 없는 데이터를 배치 하지 마세요. 신뢰할 수 없는 데이터는 공격자, HTML 폼 입력, 쿼리 문자열, HTTP 헤더를 공격자는 응용 프로그램을 위반 수 없습니다. 해당 하는 경우에 데이터베이스를 위반 하는 일을 할 수 있습니다 하는 대로 데이터베이스에서 제공 하는 데이터도 사용할 수 있는 모든 데이터입니다.

2. HTML 요소 내에서 신뢰할 수 없는 데이터를 배치 하기 전에 HTML로 인코딩된 것을 확인 합니다. 와 같은 문자는 HTML 인코딩을 &lt; 와 같은 안전한 형식으로 변경 하 고 &amp;l t;

3. HTML 특성을 신뢰할 수 없는 데이터를 전환 하기 전에 인코딩된 HTML 특성을 확인 합니다. HTML 인코딩을의 상위 집합 및와 같은 추가 문자를 인코딩합니다 HTML 특성 인코딩입니다 "및 '.

4. JavaScript를 신뢰할 수 없는 데이터를 전환 하기 전에 데이터를 런타임에 검색 내용이 HTML 요소에 배치 합니다. 이 불가능 한 다음 데이터를 확인 하는 경우 JavaScript이 인코딩됩니다. JavaScript에 대 한 위험한 문자는 JavaScript 인코딩 및 예를 들어 해당 16 진수 바뀝니다 &lt; 로 인코딩할 수는 `\u003C`합니다.

5. URL 쿼리 문자열이를 신뢰할 수 없는 데이터를 전환 하기 전에 URL로 인코딩된 것을 확인 합니다.

## <a name="html-encoding-using-razor"></a>Razor를 사용 하 여 HTML 인코딩

모두 자동으로 MVC에서 사용 되는 Razor 엔진 인코딩합니다 이렇게 것을 방지 하기 위해 열심히 작업 하지 않는 출력 변수에서 제공 합니다. HTML 특성을 사용할 때마다 인코딩 규칙을 사용 합니다 *@* 지시문입니다. HTML로 인코딩 특성은 HTML 인코딩 즉, HTML 인코딩 또는 HTML 특성 인코딩입니다을 사용할 것인지 걱정 없는 합니다. 만 사용 하는 HTML 컨텍스트에서 JavaScript로 직접 신뢰할 수 없는 입력을 삽입 하려고 할 때 하지 확인 해야 합니다. 태그 도우미는 또한 tag 매개 변수에서 사용 하는 입력을 인코딩합니다.

다음 Razor 보기를 수행 합니다.

```cshtml
@{
       var untrustedInput = "<\"123\">";
   }

   @untrustedInput
   ```

이 보기의 내용을 출력 합니다 *untrustedInput* 변수입니다. Namely XSS 공격에 사용 되는 일부 문자를 포함 하는이 변수 &lt;, "및 &gt;합니다. 원본 검사로 인코드된 렌더링 된 출력을 보여 줍니다.

```html
&lt;&quot;123&quot;&gt;
   ```

>[!WARNING]
> 제공 하는 ASP.NET Core MVC는 `HtmlString` 클래스는 출력 시 자동으로 인코딩된 되지 않습니다. 이 되지 사용할 함께 신뢰할 수 없는 입력으로이 XSS 취약점에 노출 됩니다.

## <a name="javascript-encoding-using-razor"></a>Razor를 사용 하 여 Javascript 인코딩

보기 처리 하는 JavaScript 값을 삽입 하려는 경우가 있을 수 있습니다. 구체적인 방법은 두 가지입니다. 값을 삽입 하는 가장 안전한 방법은 태그의 데이터 특성의 값을 배치 하 여 JavaScript에서 검색 됩니다. 예를 들어:

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

다음 HTML이 생성

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

실행 될 때 렌더링 됩니다; 다음

```none
<"123">
   <"123">
   ```

또한 JavaScript 인코더를 직접 호출할 수 있습니다.

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

이 브라우저에서 다음과 같이 렌더링;

```html
<script>
       document.write("\u003C\u0022123\u0022\u003E");
   </script>
   ```

>[!WARNING]
> DOM 요소를 만드는 JavaScript에서 신뢰할 수 없는 입력을 연결 하지 마십시오. 사용 해야 `createElement()` 속성 값을 적절 하 게 같은 할당 `node.TextContent=`를 사용할지 `element.SetAttribute()` / `element[attribute]=` 그렇지 않은 경우에 노출 됩니다 XSS DOM 기반 합니다.

## <a name="accessing-encoders-in-code"></a>코드에서 인코더에 액세스

HTML, JavaScript 및 URL 인코더는 두 가지 방법으로 코드를 통해 삽입할 수 있습니다 [종속성 주입](xref:fundamentals/dependency-injection) 에 포함 된 기본 인코더를 사용할 수 있습니다는 `System.Text.Encodings.Web` 네임 스페이스입니다. 에 적용 되는 모든 기본 인코더를 사용 하는 경우에 문자 범위와 안전 하 게 처리 되도록 적용 되지 않습니다-기본 인코더 가능한 가장 안전한 인코딩 규칙을 사용 합니다.

생성자에서 수행 해야 하는 DI 통해 구성할 수 있는 인코더를 사용 하는 *HtmlEncoder*를 *JavaScriptEncoder* 하 고 *UrlEncoder* 적절 하 게 매개 변수입니다. 예를 들어,

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

## <a name="encoding-url-parameters"></a>URL 매개 변수 인코딩

신뢰할 수 없는 입력을 있는 그대로 사용 하는 값을 사용 하 여 URL 쿼리 문자열을 작성 하려는 경우는 `UrlEncoder` 값을 인코딩할 합니다. 예를 들어 개체에 적용된

```csharp
var example = "\"Quoted Value with spaces and &\"";
   var encodedValue = _urlEncoder.Encode(example);
   ```

변수에 포함 됩니다는 encodedValue 인코딩 후 `%22Quoted%20Value%20with%20spaces%20and%20%26%22`합니다. 공백, 따옴표, 문장 부호 및 기타 안전 하지 않은 문자는 인코딩해야 백분율을 16 진수 값으로, 예를 들어 공백을 %20 됩니다.

>[!WARNING]
> URL 경로의 일부로 신뢰할 수 없는 입력을 사용 하지 마세요. 항상 신뢰할 수 없는 입력 쿼리 문자열 값으로 전달 합니다.

<a name="security-cross-site-scripting-customization"></a>

## <a name="customizing-the-encoders"></a>인코더를 사용자 지정

기본적으로 인코더 기본 라틴어 유니코드 범위를 제한 하는 안전 하 게 목록을 사용 하 여 하 고 해당 문자 코드와 해당 범위 외부에서 모든 문자를 인코딩합니다. 이 동작은 또한를 사용 하 여 인코더 출력 문자열에 따라 Razor TagHelper HtmlHelper 렌더링을 영향을 줍니다.

이 알 수 없거나 향후 브라우저 버그 (이전 브라우저 버그는 영어가 아닌 문자를 처리 하는 기반 구문 분석을 중단점이 있는) 로부터 보호 하는 것입니다. 웹 사이트가 중국어 등의 비 라틴 문자를 많이 사용 하는 경우 키릴 자모 또는 다른 사용자가이 동작은 않이 있습니다.

범위에서 시작 하는 동안 응용 프로그램에 적합 한 유니코드를 포함 하도록 인코더 안전 목록을 사용자 지정할 수 있습니다 `ConfigureServices()`합니다.

예를 들어, Razor HtmlHelper를 사용할 수 있습니다 기본 구성을 사용 하 여 다음과 같이;

```html
<p>This link text is in Chinese: @Html.ActionLink("汉语/漢語", "Index")</p>
   ```

웹 페이지의 소스를 볼 때 표시 됩니다 인코딩된; 중국어 텍스트를 사용 하 여 다음과 같이 렌더링 된

```html
<p>This link text is in Chinese: <a href="/">&#x6C49;&#x8BED;/&#x6F22;&#x8A9E;</a></p>
   ```

취급 문자 범위를 넓히려면 인코더에 의해 안전 하 게 삽입 하 여 다음 줄에는 `ConfigureServices()` 의 메서드 `startup.cs`;

```csharp
services.AddSingleton<HtmlEncoder>(
     HtmlEncoder.Create(allowedRanges: new[] { UnicodeRanges.BasicLatin,
                                               UnicodeRanges.CjkUnifiedIdeographs }));
   ```

이 예제에서는 유니코드 범위 CjkUnifiedIdeographs 포함 하도록 안전 목록을 확대 합니다. 렌더링된 된 출력은 이제 됩니다.

```html
<p>This link text is in Chinese: <a href="/">汉语/漢語</a></p>
   ```

안전한 범위는 유니코드 코드 차트에서 하지 언어로 지정 됩니다. 합니다 [유니코드 표준](http://unicode.org/) 목록을 가진 [차트 코드](http://www.unicode.org/charts/index.html) 문자가 포함 된 차트를 찾는 데 사용할 수 있습니다. Html, JavaScript 및 Url을 각 인코더는 개별적으로 구성 되어야 합니다.

> [!NOTE]
> 수신 허용 목록 사용자 지정 DI를 통해 제공 되는 인코더를만 영향을 줍니다. 인코더를 통해 직접 액세스 하는 경우 `System.Text.Encodings.Web.*Encoder.Default` 다음 기본값인 기본 라틴 수신만 사용 됩니다.

## <a name="where-should-encoding-take-place"></a>인코딩 수행을 배치 해야 합니까?

일반적인 방법은 지점 출력 인코딩을 수행 하 고 인코딩된 값은 데이터베이스에 저장 해서는 안 허용 합니다. 출력 시 인코딩 쿼리 문자열 값으로 HTML에서에서 예를 들어, 데이터의 사용을 변경할 수 있습니다. 또한 검색 하기 전에 값을 인코딩할 필요 없이 데이터를 쉽게 검색할 수 있습니다 하 고 변경 사항이 나 인코더에 대 한 버그 수정 프로그램을 활용할 수 있습니다.

## <a name="validation-as-an-xss-prevention-technique"></a>XSS 방지 기술로 유효성 검사

유효성 검사 제한 XSS 공격에 유용한 도구가 될 수 있습니다. 예를 들어 0-9 문자만 포함 된 숫자 문자열 XSS 공격을 트리거하지 않습니다. 유효성 검사 사용자 입력에서 HTML을 허용할 때 좀 더 복잡해 집니다. HTML 입력을 구문 분석 하는 것은 불가능 하지 않다면 어려울 합니다. 포함 된 HTML을 제거 하는 파서를 사용 하 여 결합 된 markdown에는 다양 한 입력을 수락 하기 위해 더 안전한 옵션입니다. 유효성 검사에만 의존해 서는 안 됩니다. 항상 어떤 유효성 검사 또는 삭제가 수행 된 관계 없이 출력 하기 전에 신뢰할 수 없는 입력을 인코딩하십시오.
