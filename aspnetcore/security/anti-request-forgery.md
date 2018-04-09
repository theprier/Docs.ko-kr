---
title: ASP.NET Core 공격 방지 교차 사이트 요청 위조 XSRF/CSRF)
author: steve-smith
description: 악성 웹 사이트 클라이언트 브라우저와 응용 프로그램 간의 상호 작용에 적용할 수 있는 웹 응용 프로그램에 대 한 공격을 방지 하는 방법을 검색 합니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 03/19/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/anti-request-forgery
ms.openlocfilehash: ad50f8b261447d40ccc24c0ee006239aa976bf20
ms.sourcegitcommit: 7d02ca5f5ddc2ca3eb0258fdd6996fbf538c129a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/03/2018
---
# <a name="prevent-cross-site-request-forgery-xsrfcsrf-attacks-in-aspnet-core"></a>ASP.NET Core 공격 방지 교차 사이트 요청 위조 XSRF/CSRF)

여 [Steve Smith](https://ardalis.com/), [Fiyaz Hasan](https://twitter.com/FiyazBinHasan), 및 [Rick Anderson](https://twitter.com/RickAndMSFT)

교차 사이트 요청 위조 (XSRF 또는 CSRF, 발음 함 *참조 surf*)가 악의적인 웹 앱 클라이언트 브라우저와를 신뢰 하는 웹 응용 프로그램 간의 상호 작용 영향을 줄 수는 그에 따라 웹 호스팅 응용 프로그램에 대 한 공격 브라우저. 이러한 공격은 웹 브라우저가 웹 사이트에 일부 유형의 인증 토큰 모든 요청에 자동으로 전송 하기 때문에 가능 합니다. 이러한 형태의 악용은 라고도 *원클릭 공격* 또는 *세션 도용을* 사용자 세션의 이전에 인증 활용 하기 때문에 방지할 수 있었던 공격입니다.

CSRF 공격의 예:

1. 사용자가에 로그인 할 `www.good-banking-site.com` 폼 인증을 사용 하 여 합니다. 서버에서 사용자를 인증 하지 않으며 인증 쿠키를 포함 하는 응답 합니다. 사이트는 유효한 인증 쿠키와 함께 수신 하는 모든 요청을 신뢰 하기 때문에 공격에 취약 합니다.
1. 사용자가 악성 사이트를 방문 `www.bad-crook-site.com`합니다.

   악성 사이트 `www.bad-crook-site.com`, 다음과 유사한 HTML 폼을 포함 합니다.

   ```html
   <h1>Congratulations! You're a Winner!</h1>
   <form action="http://good-banking-site.com/api/account" method="post">
       <input type="hidden" name="Transaction" value="withdraw">
       <input type="hidden" name="Amount" value="1000000">
       <input type="submit" value="Click to collect your prize!">
   </form>
   ```

   양식의 `action` 악성 사이트 아닌 취약 한 사이트에 대 한 게시 합니다. CSRF의 "사이트 간" 부분입니다.

1. 제출 단추를 선택합니다. 브라우저 요청을 수행 하 고 요청 된 도메인에 대 한 인증 쿠키를 자동으로 포함 `www.good-banking-site.com`합니다.
1. 요청에서 실행 되는 `www.good-banking-site.com` 사용자의 인증 컨텍스트를 사용 하는 서버 인증된 된 사용자가을 수행할 수 있는 모든 작업을 수행할 수 있습니다.

사용자가 양식을 전송 하는 단추를 선택 하는 경우 악성 사이트 수행할 수 있습니다.

* 폼을 자동으로 전송 하는 스크립트를 실행 합니다.
* 양식을 제출을 하 여 AJAX 요청으로 보냅니다. 
* Css 숨겨진된 폼을 사용 합니다. 

HTTPS를 사용 하 여 CSRF 공격을 방지 하지 않습니다. 악성 사이트로 보낼 수는 `https://www.good-banking-site.com/` 안전 하지 않은 요청을 보낼 수 처럼 손쉽게 요청 합니다.

일부 공격 대상 작업을 수행 하려면 이미지 태그를 사용할 수는 쿼리에서 GET 요청에 응답 하는 끝점입니다. 이 형태의 공격이 이미지를 허용 하지만 JavaScript를 차단 하는 포럼 사이트에서 일반적입니다. 변수 또는 리소스 변경에 GET 요청에서 상태를 변경 하는 앱은 악의적인 공격에 취약 합니다. **상태를 변경 하는 GET 요청은 안전 하지 않습니다. GET 요청에서 상태 변경 하는 것이 좋습니다.**

CSRF 공격 되므로 인증용 쿠키를 사용 하는 웹 응용 프로그램에 대해 발생할 수 있습니다.

* 브라우저 웹 응용 프로그램에서 발급 하는 쿠키를 저장 합니다.
* 저장 된 쿠키는 인증 된 사용자에 대 한 세션 쿠키를 포함합니다.
* 브라우저가 모든 쿠키와 관련 된 도메인을 웹 응용 프로그램 브라우저 내에서 응용 프로그램에 요청 생성 방법에 관계 없이 모든 요청을 전송 합니다.

그러나 CSRF 공격에 제한 되지 않습니다 쿠키를 이용 합니다. 예를 들어, 기본 및 다이제스트 인증 취약 됩니다. 브라우저에서 세션까지 자격 증명을 자동으로 전송 후 사용자가 기본 또는 다이제스트 인증 로그인을&dagger; 종료 합니다.

&dagger;이 컨텍스트에서 *세션* 참조 하는 사용자가 인증 하는 클라이언트 세션입니다. 서버 쪽 세션에 관련 되지 않은 또는 [ASP.NET Core 세션 미들웨어](xref:fundamentals/app-state)합니다.

사용자가 예방 조치를 수행 하 여 CSRF 취약점을 방지할 수 있습니다.

* 사용 하 여 완료 되 면 웹 앱에서 로그인 합니다.
* 주기적으로 지우기 브라우저 쿠키입니다.

그러나 CSRF 취약점은 기본적으로 웹 앱을 최종 사용자가 아닌 문제입니다.

## <a name="authentication-fundamentals"></a>인증 기본 사항

쿠키 기반 인증에는 인기 있는 형태의 인증입니다. 토큰 기반 인증 시스템은 단일 페이지 응용 프로그램 (SPAs)를 위해 특별히에서 인기, 커지고 있습니다.

### <a name="cookie-based-authentication"></a>쿠키 기반 인증

사용자가 자신의 사용자 이름과 암호를 사용 하 여 인증, 인증 및 권한 부여에 사용할 수 있는 인증 티켓을 포함 하는 토큰을 발급 하는 합니다. 토큰이는 클라이언트는 모든 요청을 함께 제공 되는 쿠키 함에 따라 저장 됩니다. 생성 하 고이 쿠키를 유효성 검사 쿠키 인증 미들웨어에서 수행 됩니다. [미들웨어](xref:fundamentals/middleware/index) 사용자 계정 암호화 된 쿠키에 serialize 합니다. 이후 요청에서 미들웨어 쿠키의 유효성을 검사, 주 서버를 다시 만드는 및 보안 주체에 할당 된 [사용자](/dotnet/api/microsoft.aspnetcore.http.httpcontext.user) 속성 [HttpContext](/dotnet/api/microsoft.aspnetcore.http.httpcontext)합니다.

### <a name="token-based-authentication"></a>토큰 기반 인증

사용자가 인증 될 때 (하지 antiforgery 토큰) 토큰을 발급 하는 합니다. 형식으로 사용자 정보를 포함 하는 토큰 [클레임](/dotnet/framework/security/claims-based-identity-model) 또는 응용 프로그램에서 유지 관리 하는 사용자 상태를 응용 프로그램을 가리키는 참조 토큰입니다. 사용자가 인증을 요구 하는 리소스에 액세스 하려고 하는 경우 응용 프로그램을 추가 인증 헤더에서 전달자 토큰의 형태로 토큰이 보내집니다. 이렇게 하면 응용 프로그램 상태 비저장 있습니다. 각 후속 요청에 토큰은 서버 쪽 유효성 검사에 대 한 요청에 전달 됩니다. 이 토큰이 없는 *암호화 된*; 있기 *인코딩된*합니다. 서버에서 해당 정보에 액세스 하는 토큰은 디코딩됩니다. 토큰 이후의 요청을 보내려면 토큰 브라우저의 로컬 저장소에 저장 합니다. 토큰은 브라우저의 로컬 저장소에 저장 되는 경우 CSRF 취약점에 대 한 관심이 해서는 안 됩니다. CSRF 문제가 있으면 토큰 쿠키에 저장 됩니다.

### <a name="multiple-apps-hosted-at-one-domain"></a>한 도메인에서 호스팅되는 여러 앱

공유 호스팅 환경은 세션 하이재킹, CSRF, 로그인 및 기타 공격에 취약 합니다.

하지만 `example1.contoso.net` 및 `example2.contoso.net` 는 서로 다른 호스트에서 호스트 간의 암시적 트러스트 관계가 있는 `*.contoso.net` 도메인입니다. 이 암시적 트러스트 관계에는 신뢰할 수 없는 호스트를 (AJAX 요청을 제어 하는 동일 원본 정책 반드시 HTTP 쿠키를 적용 하지 않는) 다른 사용자의 쿠키에 영향을 줄 수 있습니다.

도메인을 공유 하지 않고 함으로써 같은 도메인에 호스트 되는 앱 간에 신뢰할 수 있는 쿠키를 악용 하는 공격을 방지할 수 있습니다. 각 응용 프로그램은 자체 도메인에서 호스트 되는 경우 암시적 쿠키 트러스트 관계가 없는 악용할 수 있습니다.

## <a name="aspnet-core-antiforgery-configuration"></a>ASP.NET Core antiforgery 구성

> [!WARNING]
> ASP.NET Core antiforgery를 사용 하 여 구현 [ASP.NET Core 데이터 보호](xref:security/data-protection/introduction)합니다. 데이터 보호 스택의 서버 팜에서 작동 하도록 구성 되어야 합니다. 참조 [데이터 보호를 구성](xref:security/data-protection/configuration/overview) 자세한 정보에 대 한 합니다.

ASP.NET Core 2.0 이상에서는 [FormTagHelper](xref:mvc/views/working-with-forms#the-form-tag-helper) antiforgery 토큰 HTML 폼 요소를 삽입 합니다. Razor 파일에 다음 태그는 자동으로 antiforgery 토큰을 생성 합니다.

```cshtml
<form method="post">
    ...
</form>
```

마찬가지로, [IHtmlHelper.BeginForm](/dotnet/api/microsoft.aspnetcore.mvc.rendering.ihtmlhelper.beginform) 폼의 메서드가 GET 실행 되지 않으면 기본적으로 antiforgery 토큰을 생성 합니다.

발생 하는 HTML 폼 요소에 대 한 자동 생성 antiforgery 토큰의 경우는 `<form>` 태그에는 `method="post"` 특성 및 다음 중 하나에 해당할:

  * 동작 특성이 비어 (`action=""`).
  * 작업 특성을 제공 하지 않으면 (`<form method="post">`).

HTML 폼 요소에 대 한 antiforgery 토큰의 자동 생성을 비활성화할 수 있습니다.

* Antiforgery 토큰을 사용 하 여 명시적으로 비활성화할는 `asp-antiforgery` 특성:

  ```cshtml
  <form method="post" asp-antiforgery="false">
      ...
  </form>
  ```

* Form 요소는 선택한 아웃 태그 도우미의 태그 도우미를 사용 하 여 [! 옵트아웃 기호](xref:mvc/views/tag-helpers/intro#opt-out):

  ```cshtml
  <!form method="post">
      ...
  </!form>
  ```

* 제거는 `FormTagHelper` 보기에서 합니다. `FormTagHelper` Razor 보기에는 다음 지시문을 추가 하 여 보기에서 제거할 수 있습니다.

  ```cshtml
  @removeTagHelper Microsoft.AspNetCore.Mvc.TagHelpers.FormTagHelper, Microsoft.AspNetCore.Mvc.TagHelpers
  ```

> [!NOTE]
> [Razor 페이지](xref:mvc/razor-pages/index) XSRF/CSRF에서 자동으로 보호 됩니다. 자세한 내용은 참조 [XSRF/CSRF 및 Razor 페이지](xref:mvc/razor-pages/index#xsrf)합니다.

가장 일반적인 방법은 CSRF 공격 으로부터 보호 하는 데 사용 하는 것은 *동기화 장치 토큰 패턴이* (STP). STP은 사용자 양식 데이터로 페이지를 요청할 때 사용 됩니다.

1. 서버는 클라이언트에 현재 사용자의 id와 연결 된 토큰을 보냅니다.
1. 클라이언트가 보냅니다 확인을 위해 서버를 다시 토큰.
1. 인증 된 사용자의 id와 일치 하지 않는 토큰을 수신 하는 서버, 요청이 거부 됩니다.

토큰이 고유 하 고 예측할 수 없는 되었습니다. 토큰을 사용 하 여 일련의 요청을 적절 한 시퀀싱 할 수도 수 (요청 시퀀스의 예를 들어 보장: 1 페이지가 &ndash; 2 페이지 &ndash; 3 페이지). 모든 Razor 페이지 및 ASP.NET Core MVC 템플릿에서 양식의 antiforgery 토큰을 생성 합니다. 다음 예제 보기 쌍 antiforgery 토큰을 생성 합니다.

```cshtml
<form asp-controller="Manage" asp-action="ChangePassword" method="post">
    ...
</form>

@using (Html.BeginForm("ChangePassword", "Manage"))
{
    ...
}
```

Antiforgery 토큰을 명시적으로 추가 된 `<form>` HTML 도우미와 태그 도우미를 사용 하지 않고 요소 [ @Html.AntiForgeryToken ](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.htmlhelper.antiforgerytoken):

```cshtml
<form action="/" method="post">
    @Html.AntiForgeryToken()
</form>
```

위의 경우 중 각 ASP.NET Core 다음과 유사한 숨겨진된 양식 필드를 추가합니다.

```cshtml
<input name="__RequestVerificationToken" type="hidden" value="CfDJ8NrAkS ... s2-m9Yw">
```

ASP.NET Core 3 개 포함 [필터](xref:mvc/controllers/filters) antiforgery 토큰을 사용 하기 위한:

* [ValidateAntiForgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.validateantiforgerytokenattribute)
* [AutoValidateAntiforgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.autovalidateantiforgerytokenattribute)
* [IgnoreAntiforgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.ignoreantiforgerytokenattribute)

## <a name="antiforgery-options"></a>Antiforgery 옵션

사용자 지정 [antiforgery 옵션](/dotnet/api/Microsoft.AspNetCore.Antiforgery.AntiforgeryOptions) 에 `Startup.ConfigureServices`:

```csharp
services.AddAntiforgery(options => 
{
    options.CookieDomain = "contoso.com";
    options.CookieName = "X-CSRF-TOKEN-COOKIENAME";
    options.CookiePath = "Path";
    options.FormFieldName = "AntiforgeryFieldname";
    options.HeaderName = "X-CSRF-TOKEN-HEADERNAME";
    options.RequireSsl = false;
    options.SuppressXFrameOptionsHeader = false;
});
```

| 옵션 | 설명 |
| ------ | ----------- |
| [쿠키](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.cookie) | Antiforgery 쿠키를 만드는 데 설정을 결정 합니다. |
| [CookieDomain](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.cookiedomain) | 쿠키의 도메인입니다. 기본값은 `null`입니다. 이 속성은 사용 되지 않으며 이후 버전에서 제거 됩니다. 권장 방법은 Cookie.Domain입니다. |
| [CookieName](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.cookiename) | 쿠키의 이름입니다. 을 설정 하지 시스템 생성 고유 이름으로 시작 된 [DefaultCookiePrefix](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.defaultcookieprefix) (". AspNetCore.Antiforgery입니다. ")입니다. 이 속성은 사용 되지 않으며 이후 버전에서 제거 됩니다. 권장 방법은 Cookie.Name입니다. |
| [CookiePath](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.cookiepath) | 쿠키에 설정 된 경로입니다. 이 속성은 사용 되지 않으며 이후 버전에서 제거 됩니다. 권장 방법은 Cookie.Path입니다. |
| [FormFieldName](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.formfieldname) | 뷰에서 antiforgery 토큰을 렌더링 하는 antiforgery 시스템에서 사용 하는 숨겨진된 폼 필드의 이름입니다. |
| [HeaderName](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.headername) | Antiforgery 시스템에서 사용 하는 헤더의 이름입니다. 경우 `null`, 시스템에서는 양식 데이터입니다. |
| [RequireSsl](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.requiressl) | Antiforgery 시스템에서 SSL이 필요한 지 여부를 지정 합니다. 경우 `true`, 비 SSL 요청이 실패 합니다. 기본값은 `false`입니다. 이 속성은 사용 되지 않으며 이후 버전에서 제거 됩니다. 메서드 대신 Cookie.SecurePolicy를 설정 하는 것입니다. |
| [SuppressXFrameOptionsHeader](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.suppressxframeoptionsheader) | 생성을 표시 하지 않을 것인지를 지정 된 `X-Frame-Options` 헤더입니다. 기본적으로 머리글은 "SAMEORIGIN"의 값으로 생성 됩니다. 기본값은 `false`입니다. |

자세한 내용은 참조 [CookieAuthenticationOptions](/dotnet/api/Microsoft.AspNetCore.Builder.CookieAuthenticationOptions)합니다.

## <a name="configure-antiforgery-features-with-iantiforgery"></a>IAntiforgery와 antiforgery 기능을 구성 합니다.

[IAntiforgery](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgery) antiforgery 기능을 구성 하는 API를 제공 합니다. `IAntiforgery` 요청한 크기에 `Configure` 의 메서드는 `Startup` 클래스입니다. 다음 예제에서는 응용 프로그램의 홈 페이지에서 미들웨어를 사용 하 여 antiforgery 토큰을 생성 하 고 쿠키 (사용 하 여 기본 각도 명명 규칙이이 항목의 뒷부분에서 설명)으로 응답에 보냅니다.

```csharp
public void Configure(IApplicationBuilder app, IAntiforgery antiforgery)
{
    app.Use(next => context =>
    {
        string path = context.Request.Path.Value;

        if (
            string.Equals(path, "/", StringComparison.OrdinalIgnoreCase) ||
            string.Equals(path, "/index.html", StringComparison.OrdinalIgnoreCase))
        {
            // The request token can be sent as a JavaScript-readable cookie, 
            // and Angular uses it by default.
            var tokens = antiforgery.GetAndStoreTokens(context);
            context.Response.Cookies.Append("XSRF-TOKEN", tokens.RequestToken, 
                new CookieOptions() { HttpOnly = false });
        }

        return next(context);
    });
}
```

### <a name="require-antiforgery-validation"></a>Antiforgery 유효성 검사 필요

[ValidateAntiForgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.validateantiforgerytokenattribute) 는 개별 작업은 컨트롤러에 적용할 수 있는 작업 필터는 전역적으로 또는 합니다. 요청에 유효한 antiforgery 토큰에 포함 되지 않으면이 필터 적용이 영향을 주는 작업에 대 한 요청 차단 됩니다.

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<IActionResult> RemoveLogin(RemoveLoginViewModel account)
{
    ManageMessageId? message = ManageMessageId.Error;
    var user = await GetCurrentUserAsync();

    if (user != null)
    {
        var result = 
            await _userManager.RemoveLoginAsync(
                user, account.LoginProvider, account.ProviderKey);

        if (result.Succeeded)
        {
            await _signInManager.SignInAsync(user, isPersistent: false);
            message = ManageMessageId.RemoveLoginSuccess;
        }
    }

    return RedirectToAction(nameof(ManageLogins), new { Message = message });
}
```

`ValidateAntiForgeryToken` 특성에 대 한 요청 작업 메서드 HTTP GET 요청을 포함 하 여 데코레이팅되 토큰이 필요 합니다. 경우는 `ValidateAntiForgeryToken` 특성은 응용 프로그램의 컨트롤러에 적용 되며,으로 재정의 될 수는 `IgnoreAntiforgeryToken` 특성입니다.

> [!NOTE]
> ASP.NET Core GET 요청에 antiforgery 토큰을 자동으로 추가 지원 하지 않습니다.

### <a name="automatically-validate-antiforgery-tokens-for-unsafe-http-methods-only"></a>자동으로 안전 하지 않은 HTTP 메서드에 대 한 antiforgery 토큰 유효성을 검사합니다

ASP.NET Core 응용 프로그램 안전 HTTP 메서드 (GET, HEAD, 옵션 및 추적)에 대 한 antiforgery 토큰을 생성 하지 않습니다. 광범위 하 게 적용 하는 대신는 `ValidateAntiForgeryToken` 특성 및 사용 하 여를 재정의 `IgnoreAntiforgeryToken` 특성은 [AutoValidateAntiforgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.autovalidateantiforgerytokenattribute) 특성을 사용할 수 있습니다. 이 특성은 동일 하 게 작동는 `ValidateAntiForgeryToken` 특성을 제외 하 고 토큰에 대 한 다음과 같은 HTTP 메서드를 사용 하 여 요청 필요 하지 않습니다.

* 가져오기
* HEAD
* 옵션
* TRACE

사용 권장 `AutoValidateAntiforgeryToken` 비 API 시나리오에 대 한 광범위 하 게 합니다. 이렇게 하면 기본적으로 POST 작업 보호 됩니다. 대신 사용 하는 표시 되지 않으면 기본적으로 antiforgery 토큰을 무시 하도록 `ValidateAntiForgeryToken` 개별 작업 메서드에 적용 됩니다. 것에 쓰지만 대개 남겨둘 POST 작업 메서드에 대 한이 시나리오에서는 보호 되지 않은 상태로 실수로 CSRF 공격에 취약 한 응용 프로그램을 종료 합니다. 모든 게시물 antiforgery 토큰을 보내야 합니다.

Api는 토큰의 쿠키 일부로 보내기 위한 자동 메커니즘이 필요는 없습니다. 아마도 구현 클라이언트 코드 구현에 따라 달라 집니다. 몇 가지 예는 다음과 같습니다.

클래스 수준 예:

```csharp
[Authorize]
[AutoValidateAntiforgeryToken]
public class ManageController : Controller
{
```

전역 예:

```csharp
services.AddMvc(options => 
    options.Filters.Add(new AutoValidateAntiforgeryTokenAttribute()));
```

### <a name="override-global-or-controller-antiforgery-attributes"></a>전역 재정의 또는 컨트롤러 antiforgery 특성

[IgnoreAntiforgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.ignoreantiforgerytokenattribute) 필터는 지정 된 작업 (또는 컨트롤러)에 대 한 antiforgery 토큰에 대 한 필요성을 제거 하는 데 사용 됩니다. 이 필터 재정의 적용 하면 `ValidateAntiForgeryToken` 및 `AutoValidateAntiforgeryToken` (전역적으로 또는 컨트롤러)는 더 높은 수준에서 지정 된 필터입니다.

```csharp
[Authorize]
[AutoValidateAntiforgeryToken]
public class ManageController : Controller
{
    [HttpPost]
    [IgnoreAntiforgeryToken]
    public async Task<IActionResult> DoSomethingSafe(SomeViewModel model)
    {
        // no antiforgery token required
    }
}
```

## <a name="refresh-tokens-after-authentication"></a>인증 후 새로 고침 토큰

뷰 또는 Razor 페이지의 페이지에 사용자를 리디렉션하여 사용자가 인증 한 후 토큰 새로 고쳐야 합니다.

## <a name="javascript-ajax-and-spas"></a>JavaScript, AJAX 및 SPAs

기존 HTML 기반 앱에서 antiforgery 토큰 숨겨진된 양식 필드를 사용 하 여 서버에 전달 됩니다. 최신 JavaScript 기반 응용 프로그램 및 SPAs 많은 요청이 프로그래밍 방식으로 이루어집니다. 이러한 AJAX 요청 토큰 다른 기술 (예: 요청 헤더 또는 쿠키)를 사용할 수 있습니다.

인증 토큰을 저장 하 고 서버에 대 한 API 요청을 인증 쿠키를 사용 하는 경우 CSRF 잠재적인 문제가 됩니다. 토큰을 저장할 로컬 저장소 사용 하는 경우 로컬 저장소에서 값은 모든 요청을 사용 하 여 서버에 자동으로 전송 되지 않습니다 때문에 CSRF 취약성을 완화할 수 있습니다. 따라서 요청 헤더는 권장된 방법으로 토큰을 보내는 클라이언트에 antiforgery 토큰을 저장할 로컬 저장소를 사용 합니다.

### <a name="javascript"></a>JavaScript

JavaScript에서 뷰를 사용 하는 토큰 만들 수 있습니다 보기 내에서 서비스를 사용 하 여 합니다. 삽입 된 [Microsoft.AspNetCore.Antiforgery.IAntiforgery](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgery) 보기 및 호출 계층에 서비스 [GetAndStoreTokens](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgery.getandstoretokens):

[!code-csharp[](anti-request-forgery/sample/MvcSample/Views/Home/Ajax.cshtml?highlight=4-10,12-13,35-36)]

이 방법은 서버에서 쿠키를 설정 하거나 클라이언트에서 읽기를 직접 사용 않아도 됩니다.

앞의 예제 JavaScript를 사용 하 여 AJAX POST 헤더에 대 한 숨겨진된 필드 값을 읽을 수 있습니다.

JavaScript 쿠키의 토큰에 액세스할 수 있고 쿠키의 콘텐츠를 사용 하 여 토큰의 값을 사용 하는 헤더를 만듭니다.

```csharp
context.Response.Cookies.Append("CSRF-TOKEN", tokens.RequestToken, 
    new Microsoft.AspNetCore.Http.CookieOptions { HttpOnly = false });
```

헤더에 토큰을 보낼 요청 스크립트 가정 `X-CSRF-TOKEN`, 찾으려는 antiforgery 서비스 구성의 `X-CSRF-TOKEN` 헤더:

```csharp
services.AddAntiforgery(options => options.HeaderName = "X-CSRF-TOKEN");
```

다음 예제에서는 JavaScript를 사용 하 여 적절 한 헤더를 사용 하는 AJAX 요청 확인.

```javascript
function getCookie(cname) {
    var name = cname + "=";
    var decodedCookie = decodeURIComponent(document.cookie);
    var ca = decodedCookie.split(';');
    for(var i = 0; i <ca.length; i++) {
        var c = ca[i];
        while (c.charAt(0) == ' ') {
            c = c.substring(1);
        }
        if (c.indexOf(name) == 0) {
            return c.substring(name.length, c.length);
        }
    }
    return "";
}

var csrfToken = getCookie("CSRF-TOKEN");

var xhttp = new XMLHttpRequest();
xhttp.onreadystatechange = function() {
    if (xhttp.readyState == XMLHttpRequest.DONE) {
        if (xhttp.status == 200) {
            alert(xhttp.responseText);
        } else {
            alert('There was an error processing the AJAX request.');
        }
    }
};
xhttp.open('POST', '/api/password/changepassword', true);
xhttp.setRequestHeader("Content-type", "application/json");
xhttp.setRequestHeader("X-CSRF-TOKEN", csrfToken);
xhttp.send(JSON.stringify({ "newPassword": "ReallySecurePassword999$$$" }));
```

### <a name="angularjs"></a>AngularJS

AngularJS는 CSRF 주소로 규칙을 사용합니다. 서버 이름으로 쿠키를 전송 하는 경우 `XSRF-TOKEN`, AngularJS `$http` 서비스 서버에 요청을 보낼 때 헤더에 쿠키 값을 추가 합니다. 이 프로세스는 자동. 헤더를 명시적으로 설정할 필요가 없습니다. 헤더 이름이 `X-XSRF-TOKEN`합니다. 서버는이 헤더를 검색 하 고 해당 내용의 유효성을 검사 해야 합니다.

ASP.NET Core API에 대 한이 규칙을 통해 작동 합니다.

* 호출 하는 쿠키에 토큰을 제공할 앱을 구성 `XSRF-TOKEN`합니다.
* 라는 헤더 찾으려는 antiforgery 서비스 구성 `X-XSRF-TOKEN`합니다.

```csharp
services.AddAntiforgery(options => options.HeaderName = "X-XSRF-TOKEN");
```

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/anti-request-forgery/sample/AngularSample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="extend-antiforgery"></a>Antiforgery 확장

[IAntiForgeryAdditionalDataProvider](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider) 형식에서는 개발자가 각 토큰의 추가 데이터를 왕복 하 여 앤티 CSRF 시스템의 동작을 확장할 수 있습니다. [GetAdditionalData](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider.getadditionaldata) 될 때마다 메서드는 필드 토큰이 생성 되 고 반환 값은 생성 되는 토큰 내에 포함 되어 있습니다. 구현 자가 수 타임 스탬프, nonce, 또는 다른 모든 값을 반환 하 고 호출 [ValidateAdditionalData](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider.validateadditionaldata) 토큰의 유효성을 검사할 때이 데이터를 유효성 검사 합니다. 클라이언트의 사용자 이름은 이미 생성 된 토큰에 포함 되어 있으므로이 정보를 포함할 필요가 없습니다. 아니지만 추가 데이터 토큰을 포함 하는 경우 `IAntiForgeryAdditionalDataProvider` 가 구성, 보조 데이터 확인 되지 않습니다.

## <a name="additional-resources"></a>추가 자료

* [CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)) 에 [웹 응용 프로그램 보안 프로젝트를 열고](https://www.owasp.org/index.php/Main_Page) (OWASP).
