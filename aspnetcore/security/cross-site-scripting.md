---
title: 사이트 간 스크립팅 (XSS) ASP.NET Core에서 방지
author: rick-anderson
description: 사이트 간 스크립팅 (XSS) 및 ASP.NET Core 앱에서이 취약성을 해결 하는 방법에 알아봅니다.
ms.author: riande
ms.date: 10/14/2016
uid: security/cross-site-scripting
ms.openlocfilehash: 4784b1775d955f0ef00526e50b960fc873ea218d
ms.sourcegitcommit: 927e510d68f269d8335b5a7c8592621219a90965
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2018
ms.locfileid: "39342213"
---
# <a name="prevent-cross-site-scripting-xss-in-aspnet-core"></a><span data-ttu-id="763bb-103">사이트 간 스크립팅 (XSS) ASP.NET Core에서 방지</span><span class="sxs-lookup"><span data-stu-id="763bb-103">Prevent Cross-Site Scripting (XSS) in ASP.NET Core</span></span>

<span data-ttu-id="763bb-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="763bb-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="763bb-105">사이트 간 스크립팅 (XSS)는 보안 취약점으로 인 한 공격자가 클라이언트 측 스크립트 (일반적으로 JavaScript) 웹 페이지에 배치할 수 있도록 하는 경우</span><span class="sxs-lookup"><span data-stu-id="763bb-105">Cross-Site Scripting (XSS) is a security vulnerability which enables an attacker to place client side scripts (usually JavaScript) into web pages.</span></span> <span data-ttu-id="763bb-106">공격자가 스크립트를 실행 하는 영향을 받는 페이지를 로드 하는 다른 사용자를 공격자가 쿠키를 도용 하는 세션 토큰에 사용 하도록 설정 DOM 조작을 통해 웹 페이지의 콘텐츠를 변경 또는 다른 페이지로 브라우저를 리디렉션하십시오.</span><span class="sxs-lookup"><span data-stu-id="763bb-106">When other users load affected pages the attackers scripts will run, enabling the attacker to steal cookies and session tokens, change the contents of the web page through DOM manipulation or redirect the browser to another page.</span></span> <span data-ttu-id="763bb-107">XSS 취약성으로 인 한 응용 프로그램은 사용자 입력 하 고 유효성 검사, 인코딩 또는 해 서 이스케이프 없이 페이지에서 출력 하는 경우에 일반적으로 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-107">XSS vulnerabilities generally occur when an application takes user input and outputs it in a page without validating, encoding or escaping it.</span></span>

## <a name="protecting-your-application-against-xss"></a><span data-ttu-id="763bb-108">XSS에 대 한 응용 프로그램 보호</span><span class="sxs-lookup"><span data-stu-id="763bb-108">Protecting your application against XSS</span></span>

<span data-ttu-id="763bb-109">삽입에 응용 프로그램을 속여에 기본 수준 XSS 작동는 `<script>` 렌더링 된 페이지 또는 삽입 하 여 태그를 `On*` 요소로 이벤트.</span><span class="sxs-lookup"><span data-stu-id="763bb-109">At a basic level XSS works by tricking your application into inserting a `<script>` tag into your rendered page, or by inserting an `On*` event into an element.</span></span> <span data-ttu-id="763bb-110">개발자가 응용 프로그램에 XSS를 소개 하지 않으려면 다음 방지 단계를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-110">Developers should use the following prevention steps to avoid introducing XSS into their application.</span></span>

1. <span data-ttu-id="763bb-111">나머지 아래 단계를 수행 하지 않으면 사용자의 HTML 입력에 신뢰할 수 없는 데이터를 배치 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="763bb-111">Never put untrusted data into your HTML input, unless you follow the rest of the steps below.</span></span> <span data-ttu-id="763bb-112">신뢰할 수 없는 데이터는 공격자, HTML 폼 입력, 쿼리 문자열, HTTP 헤더를 공격자는 응용 프로그램을 위반 수 없습니다. 해당 하는 경우에 데이터베이스를 위반 하는 일을 할 수 있습니다 하는 대로 데이터베이스에서 제공 하는 데이터도 사용할 수 있는 모든 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-112">Untrusted data is any data that may be controlled by an attacker, HTML form inputs, query strings, HTTP headers, even data sourced from a database as an attacker may be able to breach your database even if they cannot breach your application.</span></span>

2. <span data-ttu-id="763bb-113">HTML 요소 내에서 신뢰할 수 없는 데이터를 배치 하기 전에 HTML로 인코딩된 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-113">Before putting untrusted data inside an HTML element ensure it's HTML encoded.</span></span> <span data-ttu-id="763bb-114">와 같은 문자는 HTML 인코딩을 &lt; 와 같은 안전한 형식으로 변경 하 고 &amp;l t;</span><span class="sxs-lookup"><span data-stu-id="763bb-114">HTML encoding takes characters such as &lt; and changes them into a safe form like &amp;lt;</span></span>

3. <span data-ttu-id="763bb-115">HTML 특성을 신뢰할 수 없는 데이터를 전환 하기 전에 인코딩된 HTML 특성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-115">Before putting untrusted data into an HTML attribute ensure it's HTML attribute encoded.</span></span> <span data-ttu-id="763bb-116">HTML 인코딩을의 상위 집합 및와 같은 추가 문자를 인코딩합니다 HTML 특성 인코딩입니다 "및 '.</span><span class="sxs-lookup"><span data-stu-id="763bb-116">HTML attribute encoding is a superset of HTML encoding and encodes additional characters such as " and '.</span></span>

4. <span data-ttu-id="763bb-117">JavaScript를 신뢰할 수 없는 데이터를 전환 하기 전에 데이터를 런타임에 검색 내용이 HTML 요소에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-117">Before putting untrusted data into JavaScript place the data in an HTML element whose contents you retrieve at runtime.</span></span> <span data-ttu-id="763bb-118">이 불가능 한 다음 데이터를 확인 하는 경우 JavaScript이 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-118">If this isn't possible then ensure the data is JavaScript encoded.</span></span> <span data-ttu-id="763bb-119">JavaScript에 대 한 위험한 문자는 JavaScript 인코딩 및 예를 들어 해당 16 진수 바뀝니다 &lt; 로 인코딩할 수는 `\u003C`합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-119">JavaScript encoding takes dangerous characters for JavaScript and replaces them with their hex, for example &lt; would be encoded as `\u003C`.</span></span>

5. <span data-ttu-id="763bb-120">URL 쿼리 문자열이를 신뢰할 수 없는 데이터를 전환 하기 전에 URL로 인코딩된 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-120">Before putting untrusted data into a URL query string ensure it's URL encoded.</span></span>

## <a name="html-encoding-using-razor"></a><span data-ttu-id="763bb-121">Razor를 사용 하 여 HTML 인코딩</span><span class="sxs-lookup"><span data-stu-id="763bb-121">HTML Encoding using Razor</span></span>

<span data-ttu-id="763bb-122">모두 자동으로 MVC에서 사용 되는 Razor 엔진 인코딩합니다 이렇게 것을 방지 하기 위해 열심히 작업 하지 않는 출력 변수에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-122">The Razor engine used in MVC automatically encodes all output sourced from variables, unless you work really hard to prevent it doing so.</span></span> <span data-ttu-id="763bb-123">HTML 특성을 사용할 때마다 인코딩 규칙을 사용 합니다 *@* 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-123">It uses HTML Attribute encoding rules whenever you use the *@* directive.</span></span> <span data-ttu-id="763bb-124">HTML로 인코딩 특성은 HTML 인코딩 즉, HTML 인코딩 또는 HTML 특성 인코딩입니다을 사용할 것인지 걱정 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-124">As HTML attribute encoding is a superset of HTML encoding this means you don't have to concern yourself with whether you should use HTML encoding or HTML attribute encoding.</span></span> <span data-ttu-id="763bb-125">만 사용 하는 HTML 컨텍스트에서 JavaScript로 직접 신뢰할 수 없는 입력을 삽입 하려고 할 때 하지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-125">You must ensure that you only use @ in an HTML context, not when attempting to insert untrusted input directly into JavaScript.</span></span> <span data-ttu-id="763bb-126">태그 도우미는 또한 tag 매개 변수에서 사용 하는 입력을 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-126">Tag helpers will also encode input you use in tag parameters.</span></span>

<span data-ttu-id="763bb-127">다음 Razor 보기를; 사용</span><span class="sxs-lookup"><span data-stu-id="763bb-127">Take the following Razor view;</span></span>

```none
@{
       var untrustedInput = "<\"123\">";
   }

   @untrustedInput
   ```

<span data-ttu-id="763bb-128">이 보기의 내용을 출력 합니다 *untrustedInput* 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-128">This view outputs the contents of the *untrustedInput* variable.</span></span> <span data-ttu-id="763bb-129">Namely XSS 공격에 사용 되는 일부 문자를 포함 하는이 변수 &lt;, "및 &gt;합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-129">This variable includes some characters which are used in XSS attacks, namely &lt;, " and &gt;.</span></span> <span data-ttu-id="763bb-130">원본 검사로 인코드된 렌더링 된 출력을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-130">Examining the source shows the rendered output encoded as:</span></span>

```html
&lt;&quot;123&quot;&gt;
   ```

>[!WARNING]
> <span data-ttu-id="763bb-131">제공 하는 ASP.NET Core MVC는 `HtmlString` 클래스는 출력 시 자동으로 인코딩된 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-131">ASP.NET Core MVC provides an `HtmlString` class which isn't automatically encoded upon output.</span></span> <span data-ttu-id="763bb-132">이 되지 사용할 함께 신뢰할 수 없는 입력으로이 XSS 취약점에 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-132">This should never be used in combination with untrusted input as this will expose an XSS vulnerability.</span></span>

## <a name="javascript-encoding-using-razor"></a><span data-ttu-id="763bb-133">Razor를 사용 하 여 Javascript 인코딩</span><span class="sxs-lookup"><span data-stu-id="763bb-133">Javascript Encoding using Razor</span></span>

<span data-ttu-id="763bb-134">보기 처리 하는 JavaScript 값을 삽입 하려는 경우가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-134">There may be times you want to insert a value into JavaScript to process in your view.</span></span> <span data-ttu-id="763bb-135">구체적인 방법은 두 가지입니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-135">There are two ways to do this.</span></span> <span data-ttu-id="763bb-136">값을 삽입 하는 가장 안전한 방법은 태그의 데이터 특성의 값을 배치 하 여 JavaScript에서 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-136">The safest way to insert  values is to place the value in a data attribute of a tag and retrieve it in your JavaScript.</span></span> <span data-ttu-id="763bb-137">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="763bb-137">For example:</span></span>

```none
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

<span data-ttu-id="763bb-138">다음 HTML이 생성</span><span class="sxs-lookup"><span data-stu-id="763bb-138">This will produce the following HTML</span></span>

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

<span data-ttu-id="763bb-139">실행 될 때 렌더링 됩니다; 다음</span><span class="sxs-lookup"><span data-stu-id="763bb-139">Which, when it runs, will render the following;</span></span>

```none
<"123">
   <"123">
   ```

<span data-ttu-id="763bb-140">JavaScript 인코더를 직접 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-140">You can also call the JavaScript encoder directly,</span></span>

```none
@using System.Text.Encodings.Web;
   @inject JavaScriptEncoder encoder;

   @{
       var untrustedInput = "<\"123\">";
   }

   <script>
       document.write("@encoder.Encode(untrustedInput)");
   </script>
   ```

<span data-ttu-id="763bb-141">이 브라우저에서 다음과 같이 렌더링;</span><span class="sxs-lookup"><span data-stu-id="763bb-141">This will render in the browser as follows;</span></span>

```html
<script>
       document.write("\u003C\u0022123\u0022\u003E");
   </script>
   ```

>[!WARNING]
> <span data-ttu-id="763bb-142">DOM 요소를 만드는 JavaScript에서 신뢰할 수 없는 입력을 연결 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="763bb-142">Don't concatenate untrusted input in JavaScript to create DOM elements.</span></span> <span data-ttu-id="763bb-143">사용 해야 `createElement()` 속성 값을 적절 하 게 같은 할당 `node.TextContent=`를 사용할지 `element.SetAttribute()` / `element[attribute]=` 그렇지 않은 경우에 노출 됩니다 XSS DOM 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-143">You should use `createElement()` and assign property values appropriately such as `node.TextContent=`, or use `element.SetAttribute()`/`element[attribute]=` otherwise you expose yourself to DOM-based XSS.</span></span>

## <a name="accessing-encoders-in-code"></a><span data-ttu-id="763bb-144">코드에서 인코더에 액세스</span><span class="sxs-lookup"><span data-stu-id="763bb-144">Accessing encoders in code</span></span>

<span data-ttu-id="763bb-145">HTML, JavaScript 및 URL 인코더는 두 가지 방법으로 코드를 통해 삽입할 수 있습니다 [종속성 주입](xref:fundamentals/dependency-injection) 에 포함 된 기본 인코더를 사용할 수 있습니다는 `System.Text.Encodings.Web` 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-145">The HTML, JavaScript and URL encoders are available to your code in two ways, you can inject them via [dependency injection](xref:fundamentals/dependency-injection) or you can use the default encoders contained in the `System.Text.Encodings.Web` namespace.</span></span> <span data-ttu-id="763bb-146">에 적용 되는 모든 기본 인코더를 사용 하는 경우에 문자 범위와 안전 하 게 처리 되도록 적용 되지 않습니다-기본 인코더 가능한 가장 안전한 인코딩 규칙을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-146">If you use the default encoders then any  you applied to character ranges to be treated as safe won't take effect - the default encoders use the safest encoding rules possible.</span></span>

<span data-ttu-id="763bb-147">생성자에서 수행 해야 하는 DI 통해 구성할 수 있는 인코더를 사용 하는 *HtmlEncoder*를 *JavaScriptEncoder* 하 고 *UrlEncoder* 적절 하 게 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-147">To use the configurable encoders via DI your constructors should take an *HtmlEncoder*, *JavaScriptEncoder* and *UrlEncoder* parameter as appropriate.</span></span> <span data-ttu-id="763bb-148">예를 들어,</span><span class="sxs-lookup"><span data-stu-id="763bb-148">For example;</span></span>

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

## <a name="encoding-url-parameters"></a><span data-ttu-id="763bb-149">URL 매개 변수 인코딩</span><span class="sxs-lookup"><span data-stu-id="763bb-149">Encoding URL Parameters</span></span>

<span data-ttu-id="763bb-150">신뢰할 수 없는 입력을 있는 그대로 사용 하는 값을 사용 하 여 URL 쿼리 문자열을 작성 하려는 경우는 `UrlEncoder` 값을 인코딩할 합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-150">If you want to build a URL query string with untrusted input as a value use the `UrlEncoder` to encode the value.</span></span> <span data-ttu-id="763bb-151">예를 들어 개체에 적용된</span><span class="sxs-lookup"><span data-stu-id="763bb-151">For example,</span></span>

```csharp
var example = "\"Quoted Value with spaces and &\"";
   var encodedValue = _urlEncoder.Encode(example);
   ```

<span data-ttu-id="763bb-152">변수에 포함 됩니다는 encodedValue 인코딩 후 `%22Quoted%20Value%20with%20spaces%20and%20%26%22`합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-152">After encoding the encodedValue variable will contain `%22Quoted%20Value%20with%20spaces%20and%20%26%22`.</span></span> <span data-ttu-id="763bb-153">공백, 따옴표, 문장 부호 및 기타 안전 하지 않은 문자는 인코딩해야 백분율을 16 진수 값으로, 예를 들어 공백을 %20 됩니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-153">Spaces, quotes, punctuation and other unsafe characters will be percent encoded to their hexadecimal value, for example a space character will become %20.</span></span>

>[!WARNING]
> <span data-ttu-id="763bb-154">URL 경로의 일부로 신뢰할 수 없는 입력을 사용 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="763bb-154">Don't use untrusted input as part of a URL path.</span></span> <span data-ttu-id="763bb-155">항상 신뢰할 수 없는 입력 쿼리 문자열 값으로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-155">Always pass untrusted input as a query string value.</span></span>

<a name="security-cross-site-scripting-customization"></a>

## <a name="customizing-the-encoders"></a><span data-ttu-id="763bb-156">인코더를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="763bb-156">Customizing the Encoders</span></span>

<span data-ttu-id="763bb-157">기본적으로 인코더 기본 라틴어 유니코드 범위를 제한 하는 안전 하 게 목록을 사용 하 여 하 고 해당 문자 코드와 해당 범위 외부에서 모든 문자를 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-157">By default encoders use a safe list limited to the Basic Latin Unicode range and encode all characters outside of that range as their character code equivalents.</span></span> <span data-ttu-id="763bb-158">이 동작은 또한를 사용 하 여 인코더 출력 문자열에 따라 Razor TagHelper HtmlHelper 렌더링을 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-158">This behavior also affects Razor TagHelper and HtmlHelper rendering as it will use the encoders to output your strings.</span></span>

<span data-ttu-id="763bb-159">이 알 수 없거나 향후 브라우저 버그 (이전 브라우저 버그는 영어가 아닌 문자를 처리 하는 기반 구문 분석을 중단점이 있는) 로부터 보호 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-159">The reasoning behind this is to protect against unknown or future browser bugs (previous browser bugs have tripped up parsing based on the processing of non-English characters).</span></span> <span data-ttu-id="763bb-160">웹 사이트가 중국어 등의 비 라틴 문자를 많이 사용 하는 경우 키릴 자모 또는 다른 사용자가이 동작은 않이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-160">If your web site makes heavy use of non-Latin characters, such as Chinese, Cyrillic or others this is probably not the behavior you want.</span></span>

<span data-ttu-id="763bb-161">범위에서 시작 하는 동안 응용 프로그램에 적합 한 유니코드를 포함 하도록 인코더 안전 목록을 사용자 지정할 수 있습니다 `ConfigureServices()`합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-161">You can customize the encoder safe lists to include Unicode ranges appropriate to your application during startup, in `ConfigureServices()`.</span></span>

<span data-ttu-id="763bb-162">예를 들어, Razor HtmlHelper를 사용할 수 있습니다 기본 구성을 사용 하 여 다음과 같이;</span><span class="sxs-lookup"><span data-stu-id="763bb-162">For example, using the default configuration you might use a Razor HtmlHelper like so;</span></span>

```html
<p>This link text is in Chinese: @Html.ActionLink("汉语/漢語", "Index")</p>
   ```

<span data-ttu-id="763bb-163">웹 페이지의 소스를 볼 때 표시 됩니다 인코딩된; 중국어 텍스트를 사용 하 여 다음과 같이 렌더링 된</span><span class="sxs-lookup"><span data-stu-id="763bb-163">When you view the source of the web page you will see it has been rendered as follows, with the Chinese text encoded;</span></span>

```html
<p>This link text is in Chinese: <a href="/">&#x6C49;&#x8BED;/&#x6F22;&#x8A9E;</a></p>
   ```

<span data-ttu-id="763bb-164">취급 문자 범위를 넓히려면 인코더에 의해 안전 하 게 삽입 하 여 다음 줄에는 `ConfigureServices()` 의 메서드 `startup.cs`;</span><span class="sxs-lookup"><span data-stu-id="763bb-164">To widen the characters treated as safe by the encoder you would insert the following line into the `ConfigureServices()` method in `startup.cs`;</span></span>

```csharp
services.AddSingleton<HtmlEncoder>(
     HtmlEncoder.Create(allowedRanges: new[] { UnicodeRanges.BasicLatin,
                                               UnicodeRanges.CjkUnifiedIdeographs }));
   ```

<span data-ttu-id="763bb-165">이 예제에서는 유니코드 범위 CjkUnifiedIdeographs 포함 하도록 안전 목록을 확대 합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-165">This example widens the safe list to include the Unicode Range CjkUnifiedIdeographs.</span></span> <span data-ttu-id="763bb-166">렌더링된 된 출력은 이제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-166">The rendered output would now become</span></span>

```html
<p>This link text is in Chinese: <a href="/">汉语/漢語</a></p>
   ```

<span data-ttu-id="763bb-167">안전한 범위는 유니코드 코드 차트에서 하지 언어로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-167">Safe list ranges are specified as Unicode code charts, not languages.</span></span> <span data-ttu-id="763bb-168">합니다 [유니코드 표준](http://unicode.org/) 목록을 가진 [차트 코드](http://www.unicode.org/charts/index.html) 문자가 포함 된 차트를 찾는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-168">The [Unicode standard](http://unicode.org/) has a list of [code charts](http://www.unicode.org/charts/index.html) you can use to find the chart containing your characters.</span></span> <span data-ttu-id="763bb-169">Html, JavaScript 및 Url을 각 인코더는 개별적으로 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-169">Each encoder, Html, JavaScript and Url, must be configured separately.</span></span>

> [!NOTE]
> <span data-ttu-id="763bb-170">수신 허용 목록 사용자 지정 DI를 통해 제공 되는 인코더를만 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-170">Customization of the safe list only affects encoders sourced via DI.</span></span> <span data-ttu-id="763bb-171">인코더를 통해 직접 액세스 하는 경우 `System.Text.Encodings.Web.*Encoder.Default` 다음 기본값인 기본 라틴 수신만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-171">If you directly access an encoder via `System.Text.Encodings.Web.*Encoder.Default` then the default, Basic Latin only safelist will be used.</span></span>

## <a name="where-should-encoding-take-place"></a><span data-ttu-id="763bb-172">인코딩 수행을 배치 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="763bb-172">Where should encoding take place?</span></span>

<span data-ttu-id="763bb-173">일반적인 방법은 지점 출력 인코딩을 수행 하 고 인코딩된 값은 데이터베이스에 저장 해서는 안 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-173">The general accepted practice is that encoding takes place at the point of output and encoded values should never be stored in a database.</span></span> <span data-ttu-id="763bb-174">출력 시 인코딩 쿼리 문자열 값으로 HTML에서에서 예를 들어, 데이터의 사용을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-174">Encoding at the point of output allows you to change the use of data, for example, from HTML to a query string value.</span></span> <span data-ttu-id="763bb-175">또한 검색 하기 전에 값을 인코딩할 필요 없이 데이터를 쉽게 검색할 수 있습니다 하 고 변경 사항이 나 인코더에 대 한 버그 수정 프로그램을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-175">It also enables you to easily search your data without having to encode values before searching and allows you to take advantage of any changes or bug fixes made to encoders.</span></span>

## <a name="validation-as-an-xss-prevention-technique"></a><span data-ttu-id="763bb-176">XSS 방지 기술로 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="763bb-176">Validation as an XSS prevention technique</span></span>

<span data-ttu-id="763bb-177">유효성 검사 제한 XSS 공격에 유용한 도구가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-177">Validation can be a useful tool in limiting XSS attacks.</span></span> <span data-ttu-id="763bb-178">예를 들어 0-9 문자만 포함 된 숫자 문자열 XSS 공격을 트리거하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-178">For example, a numeric string containing only the characters 0-9 won't trigger an XSS attack.</span></span> <span data-ttu-id="763bb-179">유효성 검사 불가능 하지 않다면 어려울는 HTML 입력을 구문 분석할-사용자 입력의 HTML을 허용 하려는 경우 문제가 더 복잡해 집니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-179">Validation becomes more complicated should you wish to accept HTML in user input - parsing HTML input is difficult, if not impossible.</span></span> <span data-ttu-id="763bb-180">MarkDown 및 다른 텍스트 형식이 안전한 옵션이 다양 한 입력에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-180">MarkDown and other text formats would be a safer option for rich input.</span></span> <span data-ttu-id="763bb-181">유효성 검사에 의존 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="763bb-181">You should never rely on validation alone.</span></span> <span data-ttu-id="763bb-182">항상 수행한 유효성 검사에 관계 없이 출력 하기 전에 신뢰할 수 없는 입력을 인코딩하십시오.</span><span class="sxs-lookup"><span data-stu-id="763bb-182">Always encode untrusted input before output, no matter what validation you have performed.</span></span>
