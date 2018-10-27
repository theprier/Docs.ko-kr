---
title: ASP.NET Core에서 교차 사이트 스크립팅(XSS) 방지하기
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
# <a name="prevent-cross-site-scripting-xss-in-aspnet-core"></a><span data-ttu-id="1ab16-103">ASP.NET Core에서 교차 사이트 스크립팅(XSS) 방지하기</span><span class="sxs-lookup"><span data-stu-id="1ab16-103">Prevent Cross-Site Scripting (XSS) in ASP.NET Core</span></span>

<span data-ttu-id="1ab16-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="1ab16-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="1ab16-105">사이트 간 스크립팅 (XSS)는 보안 취약점으로 인 한 공격자가 클라이언트 측 스크립트 (일반적으로 JavaScript) 웹 페이지에 배치할 수 있도록 하는 경우</span><span class="sxs-lookup"><span data-stu-id="1ab16-105">Cross-Site Scripting (XSS) is a security vulnerability which enables an attacker to place client side scripts (usually JavaScript) into web pages.</span></span> <span data-ttu-id="1ab16-106">다른 사용자에 게 공격자의 스크립트를 실행 하는 영향을 받는 페이지를 로드 하는 경우 DOM 조작을 통해 웹 페이지의 콘텐츠를 변경 또는 다른 페이지로 브라우저를 리디렉션할 공격자가 쿠키를 도용 하는 세션 토큰에 사용 하도록 설정.</span><span class="sxs-lookup"><span data-stu-id="1ab16-106">When other users load affected pages the attacker's scripts will run, enabling the attacker to steal cookies and session tokens, change the contents of the web page through DOM manipulation or redirect the browser to another page.</span></span> <span data-ttu-id="1ab16-107">XSS 취약성으로 인 한 응용 프로그램은 사용자 입력 하 고 유효성 검사, 인코딩 또는 해 서 이스케이프 하지 않고 페이지를 출력 하는 경우에 일반적으로 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-107">XSS vulnerabilities generally occur when an application takes user input and outputs it to a page without validating, encoding or escaping it.</span></span>

## <a name="protecting-your-application-against-xss"></a><span data-ttu-id="1ab16-108">응용 프로그램을 XSS로부터 보호하기</span><span class="sxs-lookup"><span data-stu-id="1ab16-108">Protecting your application against XSS</span></span>

<span data-ttu-id="1ab16-109">삽입에 응용 프로그램을 속여에 기본 수준 XSS 작동는 `<script>` 렌더링 된 페이지 또는 삽입 하 여 태그를 `On*` 요소로 이벤트.</span><span class="sxs-lookup"><span data-stu-id="1ab16-109">At a basic level XSS works by tricking your application into inserting a `<script>` tag into your rendered page, or by inserting an `On*` event into an element.</span></span> <span data-ttu-id="1ab16-110">개발자가 응용 프로그램에 XSS를 소개 하지 않으려면 다음 방지 단계를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-110">Developers should use the following prevention steps to avoid introducing XSS into their application.</span></span>

1. <span data-ttu-id="1ab16-111">나머지 아래 단계를 수행 하지 않으면 사용자의 HTML 입력에 신뢰할 수 없는 데이터를 배치 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="1ab16-111">Never put untrusted data into your HTML input, unless you follow the rest of the steps below.</span></span> <span data-ttu-id="1ab16-112">신뢰할 수 없는 데이터는 공격자, HTML 폼 입력, 쿼리 문자열, HTTP 헤더를 공격자는 응용 프로그램을 위반 수 없습니다. 해당 하는 경우에 데이터베이스를 위반 하는 일을 할 수 있습니다 하는 대로 데이터베이스에서 제공 하는 데이터도 사용할 수 있는 모든 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-112">Untrusted data is any data that may be controlled by an attacker, HTML form inputs, query strings, HTTP headers, even data sourced from a database as an attacker may be able to breach your database even if they cannot breach your application.</span></span>

2. <span data-ttu-id="1ab16-113">신뢰할 수 없는 데이터를 HTML 요소에 삽입하기 전에 HTML로 인코딩되었는지 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="1ab16-113">Before putting untrusted data inside an HTML element ensure it's HTML encoded.</span></span> <span data-ttu-id="1ab16-114">예를 들어, &lt;와 같은 문자열을 &amp; 등과 같이 안전한 형태로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-114">HTML encoding takes characters such as &lt; and changes them into a safe form like &amp;lt;</span></span>

3. <span data-ttu-id="1ab16-115">HTML 특성을 신뢰할 수 없는 데이터를 전환 하기 전에 HTML로 인코딩된 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-115">Before putting untrusted data into an HTML attribute ensure it's HTML encoded.</span></span> <span data-ttu-id="1ab16-116">HTML 인코딩을의 상위 집합 및와 같은 추가 문자를 인코딩합니다 HTML 특성 인코딩입니다 "및 '.</span><span class="sxs-lookup"><span data-stu-id="1ab16-116">HTML attribute encoding is a superset of HTML encoding and encodes additional characters such as " and '.</span></span>

4. <span data-ttu-id="1ab16-117">신뢰할 수 없는 데이터를 Javascript에 삽입하기 전에, 런타임에 콘텐츠를 가져오는 HTML 요소에 데이터를 배치하십시오.</span><span class="sxs-lookup"><span data-stu-id="1ab16-117">Before putting untrusted data into JavaScript place the data in an HTML element whose contents you retrieve at runtime.</span></span> <span data-ttu-id="1ab16-118">배치할 수 없는 경우, 데이터가 JavaScript로 인코딩되었는지 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="1ab16-118">If this isn't possible, then ensure the data is JavaScript encoded.</span></span> <span data-ttu-id="1ab16-119">JavaScript 인코딩은 스크립트 동작을 변조할 수 있는 위험한 문자들을 hex 값으로 변환하는 과정으로, 예를 들면 &lt;를 `\u003C`로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-119">JavaScript encoding takes dangerous characters for JavaScript and replaces them with their hex, for example &lt; would be encoded as `\u003C`.</span></span>

5. <span data-ttu-id="1ab16-120">신뢰할 수 없는 데이터를 URL 쿼리 문자열에 삽입하기 전에 URL로 인코딩되었는지 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="1ab16-120">Before putting untrusted data into a URL query string ensure it's URL encoded.</span></span>

## <a name="html-encoding-using-razor"></a><span data-ttu-id="1ab16-121">Razor를 사용하여 HTML로 인코딩하기</span><span class="sxs-lookup"><span data-stu-id="1ab16-121">HTML Encoding using Razor</span></span>

<span data-ttu-id="1ab16-122">모두 자동으로 MVC에서 사용 되는 Razor 엔진 인코딩합니다 이렇게 것을 방지 하기 위해 열심히 작업 하지 않는 출력 변수에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-122">The Razor engine used in MVC automatically encodes all output sourced from variables, unless you work really hard to prevent it doing so.</span></span> <span data-ttu-id="1ab16-123">사용할 때마다 HTML 특성에 대 한 인코딩 규칙을 사용 합니다 *@* 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-123">It uses HTML attribute encoding rules whenever you use the *@* directive.</span></span> <span data-ttu-id="1ab16-124">HTML로 인코딩 특성은 HTML 인코딩 즉, HTML 인코딩 또는 HTML 특성 인코딩입니다을 사용할 것인지 걱정 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-124">As HTML attribute encoding is a superset of HTML encoding this means you don't have to concern yourself with whether you should use HTML encoding or HTML attribute encoding.</span></span> <span data-ttu-id="1ab16-125">만 사용 하는 HTML 컨텍스트에서 JavaScript로 직접 신뢰할 수 없는 입력을 삽입 하려고 할 때 하지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-125">You must ensure that you only use @ in an HTML context, not when attempting to insert untrusted input directly into JavaScript.</span></span> <span data-ttu-id="1ab16-126">태그 도우미는 또한 tag 매개 변수에서 사용 하는 입력을 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-126">Tag helpers will also encode input you use in tag parameters.</span></span>

<span data-ttu-id="1ab16-127">다음의 Razor 뷰를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-127">Take the following Razor view:</span></span>

```cshtml
@{
       var untrustedInput = "<\"123\">";
   }

   @untrustedInput
   ```

<span data-ttu-id="1ab16-128">이 보기의 내용을 출력 합니다 *untrustedInput* 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-128">This view outputs the contents of the *untrustedInput* variable.</span></span> <span data-ttu-id="1ab16-129">Namely XSS 공격에 사용 되는 일부 문자를 포함 하는이 변수 &lt;, "및 &gt;합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-129">This variable includes some characters which are used in XSS attacks, namely &lt;, " and &gt;.</span></span> <span data-ttu-id="1ab16-130">원본 검사로 인코드된 렌더링 된 출력을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-130">Examining the source shows the rendered output encoded as:</span></span>

```html
&lt;&quot;123&quot;&gt;
   ```

>[!WARNING]
> <span data-ttu-id="1ab16-131">ASP.NET Core MVC는 출력 시 자동으로 인코딩되지 않는 `HtmlString` 클래스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-131">ASP.NET Core MVC provides an `HtmlString` class which isn't automatically encoded upon output.</span></span> <span data-ttu-id="1ab16-132">XSS 취약점이 노출될 수 있으므로 절대로 신뢰할 수 없는 입력값과 함께 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="1ab16-132">This should never be used in combination with untrusted input as this will expose an XSS vulnerability.</span></span>

## <a name="javascript-encoding-using-razor"></a><span data-ttu-id="1ab16-133">Razor를 사용하여 JavaScript로 인코딩하기</span><span class="sxs-lookup"><span data-stu-id="1ab16-133">JavaScript Encoding using Razor</span></span>

<span data-ttu-id="1ab16-134">보기 처리 하는 JavaScript 값을 삽입 하려는 경우가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-134">There may be times you want to insert a value into JavaScript to process in your view.</span></span> <span data-ttu-id="1ab16-135">구체적인 방법은 두 가지입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-135">There are two ways to do this.</span></span> <span data-ttu-id="1ab16-136">값을 삽입 하는 가장 안전한 방법은 태그의 데이터 특성의 값을 배치 하 여 JavaScript에서 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-136">The safest way to insert values is to place the value in a data attribute of a tag and retrieve it in your JavaScript.</span></span> <span data-ttu-id="1ab16-137">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="1ab16-137">For example:</span></span>

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

<span data-ttu-id="1ab16-138">인코딩 결과로 다음과 같은 HTML이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-138">This will produce the following HTML</span></span>

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

<span data-ttu-id="1ab16-139">실행 될 때 다음 렌더링 됩니다. 다음</span><span class="sxs-lookup"><span data-stu-id="1ab16-139">Which, when it runs, will render the following:</span></span>

```none
<"123">
   <"123">
   ```

<span data-ttu-id="1ab16-140">또한 JavaScript 인코더를 직접 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-140">You can also call the JavaScript encoder directly:</span></span>

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

<span data-ttu-id="1ab16-141">그러면 브라우저에서 다음과 같이 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-141">This will render in the browser as follows:</span></span>

```html
<script>
       document.write("\u003C\u0022123\u0022\u003E");
   </script>
   ```

>[!WARNING]
> <span data-ttu-id="1ab16-142">DOM 요소를 만드는 JavaScript에서 신뢰할 수 없는 입력을 연결 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="1ab16-142">Don't concatenate untrusted input in JavaScript to create DOM elements.</span></span> <span data-ttu-id="1ab16-143">사용 해야 `createElement()` 속성 값을 적절 하 게 같은 할당 `node.TextContent=`를 사용할지 `element.SetAttribute()` / `element[attribute]=` 그렇지 않은 경우에 노출 됩니다 XSS DOM 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-143">You should use `createElement()` and assign property values appropriately such as `node.TextContent=`, or use `element.SetAttribute()`/`element[attribute]=` otherwise you expose yourself to DOM-based XSS.</span></span>

## <a name="accessing-encoders-in-code"></a><span data-ttu-id="1ab16-144">코드에서 인코더에 액세스하기</span><span class="sxs-lookup"><span data-stu-id="1ab16-144">Accessing encoders in code</span></span>

<span data-ttu-id="1ab16-145">HTML, JavaScript 및 URL 인코더는 두 가지 방법으로 코드를 통해 삽입할 수 있습니다 [종속성 주입](xref:fundamentals/dependency-injection) 에 포함 된 기본 인코더를 사용할 수 있습니다는 `System.Text.Encodings.Web` 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-145">The HTML, JavaScript and URL encoders are available to your code in two ways, you can inject them via [dependency injection](xref:fundamentals/dependency-injection) or you can use the default encoders contained in the `System.Text.Encodings.Web` namespace.</span></span> <span data-ttu-id="1ab16-146">에 적용 되는 모든 기본 인코더를 사용 하는 경우에 문자 범위와 안전 하 게 처리 되도록 적용 되지 않습니다-기본 인코더 가능한 가장 안전한 인코딩 규칙을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-146">If you use the default encoders then any  you applied to character ranges to be treated as safe won't take effect - the default encoders use the safest encoding rules possible.</span></span>

<span data-ttu-id="1ab16-147">생성자에서 수행 해야 하는 DI 통해 구성할 수 있는 인코더를 사용 하는 *HtmlEncoder*를 *JavaScriptEncoder* 하 고 *UrlEncoder* 적절 하 게 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-147">To use the configurable encoders via DI your constructors should take an *HtmlEncoder*, *JavaScriptEncoder* and *UrlEncoder* parameter as appropriate.</span></span> <span data-ttu-id="1ab16-148">예를 들어,</span><span class="sxs-lookup"><span data-stu-id="1ab16-148">For example;</span></span>

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

## <a name="encoding-url-parameters"></a><span data-ttu-id="1ab16-149">URL 매개 변수 인코딩하기</span><span class="sxs-lookup"><span data-stu-id="1ab16-149">Encoding URL Parameters</span></span>

<span data-ttu-id="1ab16-150">신뢰할 수 없는 입력값을 사용하여 URL 쿼리 문자열을 작성하려면 `UrlEncoder`를 사용하여 값을 인코딩하십시오.</span><span class="sxs-lookup"><span data-stu-id="1ab16-150">If you want to build a URL query string with untrusted input as a value use the `UrlEncoder` to encode the value.</span></span> <span data-ttu-id="1ab16-151">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-151">For example,</span></span>

```csharp
var example = "\"Quoted Value with spaces and &\"";
   var encodedValue = _urlEncoder.Encode(example);
   ```

<span data-ttu-id="1ab16-152">변수에 포함 됩니다는 encodedValue 인코딩 후 `%22Quoted%20Value%20with%20spaces%20and%20%26%22`합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-152">After encoding the encodedValue variable will contain `%22Quoted%20Value%20with%20spaces%20and%20%26%22`.</span></span> <span data-ttu-id="1ab16-153">공백, 따옴표, 문장 부호 및 기타 안전 하지 않은 문자는 인코딩해야 백분율을 16 진수 값으로, 예를 들어 공백을 %20 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-153">Spaces, quotes, punctuation and other unsafe characters will be percent encoded to their hexadecimal value, for example a space character will become %20.</span></span>

>[!WARNING]
> <span data-ttu-id="1ab16-154">신뢰할 수 없는 입력값을 URL 경로에 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="1ab16-154">Don't use untrusted input as part of a URL path.</span></span> <span data-ttu-id="1ab16-155">신뢰할 수 없는 입력값은 항상 쿼리 문자열의 값으로 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-155">Always pass untrusted input as a query string value.</span></span>

<a name="security-cross-site-scripting-customization"></a>

## <a name="customizing-the-encoders"></a><span data-ttu-id="1ab16-156">사용자 지정 인코더 만들기</span><span class="sxs-lookup"><span data-stu-id="1ab16-156">Customizing the Encoders</span></span>

<span data-ttu-id="1ab16-157">기본적으로 인코더에서 사용하는 안전 목록은 기본 라틴 유니코드 범위에 한정되어 있으며, 이 외의 모든 문자는 해당 문자 코드로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-157">By default encoders use a safe list limited to the Basic Latin Unicode range and encode all characters outside of that range as their character code equivalents.</span></span> <span data-ttu-id="1ab16-158">이러한 동작은 인코딩을 사용하여 문자열을 출력하는 Razor TagHelper와 HtmlHelper 렌더링에도 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-158">This behavior also affects Razor TagHelper and HtmlHelper rendering as it will use the encoders to output your strings.</span></span>

<span data-ttu-id="1ab16-159">이는 알 수 없는 문제의 발생을 막거나 이전의 브라우저 버그는 영어 이외의 문자 처리를 기반으로 한 구문 분석에 방해가 되었기에 향후 발생할 수 있는 브라우저 버그를 막기 위한 조치입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-159">The reasoning behind this is to protect against unknown or future browser bugs (previous browser bugs have tripped up parsing based on the processing of non-English characters).</span></span> <span data-ttu-id="1ab16-160">한자, 키릴 문자와 같은 비 라틴계 문자를 자주 사용하는 웹사이트의 경우에는 불편할 수 있는 조치일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-160">If your web site makes heavy use of non-Latin characters, such as Chinese, Cyrillic or others this is probably not the behavior you want.</span></span>

<span data-ttu-id="1ab16-161">시작할 때 응용 프로그램에 적절한 유니 코드 범위가 포함되도록 `ConfigureServices()`에 인코더 안전 목록을 직접 사용자 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-161">You can customize the encoder safe lists to include Unicode ranges appropriate to your application during startup, in `ConfigureServices()`.</span></span>

<span data-ttu-id="1ab16-162">예를 들어 다음과 같은 기본 구성에서 Razor HtmlHelper를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-162">For example, using the default configuration you might use a Razor HtmlHelper like so;</span></span>

```html
<p>This link text is in Chinese: @Html.ActionLink("汉语/漢語", "Index")</p>
   ```

<span data-ttu-id="1ab16-163">웹페이지에서 소스를 확인하면 중국어 텍스트가 다음과 같이 렌더링된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-163">When you view the source of the web page you will see it has been rendered as follows, with the Chinese text encoded;</span></span>

```html
<p>This link text is in Chinese: <a href="/">&#x6C49;&#x8BED;/&#x6F22;&#x8A9E;</a></p>
   ```

<span data-ttu-id="1ab16-164">안전하게 사용할 수 있는 문자의 범위를 확장하고 싶은 경우 `startup.cs` 내의 `ConfigureServices()` 메서드에 다음 행을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-164">To widen the characters treated as safe by the encoder you would insert the following line into the `ConfigureServices()` method in `startup.cs`;</span></span>

```csharp
services.AddSingleton<HtmlEncoder>(
     HtmlEncoder.Create(allowedRanges: new[] { UnicodeRanges.BasicLatin,
                                               UnicodeRanges.CjkUnifiedIdeographs }));
   ```

<span data-ttu-id="1ab16-165">이 예제에서는 유니코드 범위 CjkUnifiedIdeographs 포함 하도록 안전 목록을 확대 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-165">This example widens the safe list to include the Unicode Range CjkUnifiedIdeographs.</span></span> <span data-ttu-id="1ab16-166">렌더링된 된 출력은 이제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-166">The rendered output would now become</span></span>

```html
<p>This link text is in Chinese: <a href="/">汉语/漢語</a></p>
   ```

<span data-ttu-id="1ab16-167">안전 목록 범위는 언어가 아닌 유니코드 차트로서 명시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-167">Safe list ranges are specified as Unicode code charts, not languages.</span></span> <span data-ttu-id="1ab16-168">[유니코드 표준](http://unicode.org/)에는 필요한 문자가 포함된 차트를 찾을 수 있도록 [코드 차트](http://www.unicode.org/charts/index.html) 목록이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-168">The [Unicode standard](http://unicode.org/) has a list of [code charts](http://www.unicode.org/charts/index.html) you can use to find the chart containing your characters.</span></span> <span data-ttu-id="1ab16-169">각 인코더(예: Html, JavaScript, Url)는 개별적으로 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-169">Each encoder, Html, JavaScript and Url, must be configured separately.</span></span>

> [!NOTE]
> <span data-ttu-id="1ab16-170">사용자 지정 안전 목록은 종속성 주입을 통해 생성된 인코더에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-170">Customization of the safe list only affects encoders sourced via DI.</span></span> <span data-ttu-id="1ab16-171">`System.Text.Encodings.Web.*Encoder.Default`를 통해 직접 인코더에 액세스하는 경우 기본 라틴계 문자 안전 목록만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-171">If you directly access an encoder via `System.Text.Encodings.Web.*Encoder.Default` then the default, Basic Latin only safelist will be used.</span></span>

## <a name="where-should-encoding-take-place"></a><span data-ttu-id="1ab16-172">인코딩이 이뤄져야 할 시점</span><span class="sxs-lookup"><span data-stu-id="1ab16-172">Where should encoding take place?</span></span>

<span data-ttu-id="1ab16-173">일반적으로 인코딩은 출력 시점에 이루어져야 하며 인코딩한 값을 데이터베이스에 저장해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-173">The general accepted practice is that encoding takes place at the point of output and encoded values should never be stored in a database.</span></span> <span data-ttu-id="1ab16-174">출력 시점에서 인코딩하면 데이터의 용도를 변경(예: HTML에서 쿼리 문자열 값으로 변경)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-174">Encoding at the point of output allows you to change the use of data, for example, from HTML to a query string value.</span></span> <span data-ttu-id="1ab16-175">또한 검색 전 값을 인코딩 하지 않고도 데이터를 쉽게 검색할 수 있으며 인코더의 변경이나 버그 수정 시 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-175">It also enables you to easily search your data without having to encode values before searching and allows you to take advantage of any changes or bug fixes made to encoders.</span></span>

## <a name="validation-as-an-xss-prevention-technique"></a><span data-ttu-id="1ab16-176">XSS 방지 기술로서의 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="1ab16-176">Validation as an XSS prevention technique</span></span>

<span data-ttu-id="1ab16-177">유효성 검사는 XSS 공격을 제한하는 유용한 도구가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-177">Validation can be a useful tool in limiting XSS attacks.</span></span> <span data-ttu-id="1ab16-178">예를 들어 0~9 사이의 문자만 포함된 숫자 문자열은 XSS 공격을 일으키지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-178">For example, a numeric string containing only the characters 0-9 won't trigger an XSS attack.</span></span> <span data-ttu-id="1ab16-179">이러한 검사 과정은 HTML을 통한 사용자 입력을 허용할 때 더욱 복잡해집니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-179">Validation becomes more complicated when accepting HTML in user input.</span></span> <span data-ttu-id="1ab16-180">HTML 입력값을 구문 분석하는 것은 불가능하지는 않으나 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-180">Parsing HTML input is difficult, if not impossible.</span></span> <span data-ttu-id="1ab16-181">Markdown과 같이 파서가 삽입된 HTML을 제거하는 기능은 다양한 값이 입력될 때 보다 안전한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-181">Markdown, coupled with a parser that strips embedded HTML, is a safer option for accepting rich input.</span></span> <span data-ttu-id="1ab16-182">유효성 검사에만 의존하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="1ab16-182">Never rely on validation alone.</span></span> <span data-ttu-id="1ab16-183">어떠한 검증 과정이나 처리가 이루어졌다 하더라도 항상 출력 전에 신뢰할 수 없는 입력값을 인코딩하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="1ab16-183">Always encode untrusted input before output, no matter what validation or sanitization has been performed.</span></span>
