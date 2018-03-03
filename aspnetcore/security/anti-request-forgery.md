---
title: "ASP.NET Core 공격 방지 교차 사이트 요청 위조 XSRF/CSRF)"
author: steve-smith
description: "악성 웹 사이트 클라이언트 브라우저와 응용 프로그램 간의 상호 작용에 적용할 수 있는 웹 응용 프로그램에 대 한 공격을 방지 하는 방법을 검색 합니다."
manager: wpickett
ms.author: riande
ms.date: 7/14/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/anti-request-forgery
ms.openlocfilehash: 80651a3c3e4c722e0cb96d7cc07de366819f8d1d
ms.sourcegitcommit: 7ac15eaae20b6d70e65f3650af050a7880115cbf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2018
---
# <a name="prevent-cross-site-request-forgery-xsrfcsrf-attacks-in-aspnet-core"></a><span data-ttu-id="05d55-103">ASP.NET Core 공격 방지 교차 사이트 요청 위조 XSRF/CSRF)</span><span class="sxs-lookup"><span data-stu-id="05d55-103">Prevent Cross-Site Request Forgery (XSRF/CSRF) attacks in ASP.NET Core</span></span>

<span data-ttu-id="05d55-104">[Steve Smith](https://ardalis.com/), [Fiyaz Hasan](https://twitter.com/FiyazBinHasan), 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="05d55-104">[Steve Smith](https://ardalis.com/), [Fiyaz Hasan](https://twitter.com/FiyazBinHasan), and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

## <a name="what-attack-does-anti-forgery-prevent"></a><span data-ttu-id="05d55-105">위조 방지 어떤 공격을 방지가?</span><span class="sxs-lookup"><span data-stu-id="05d55-105">What attack does anti-forgery prevent?</span></span>

<span data-ttu-id="05d55-106">교차 사이트 요청 위조 (XSRF 또는 CSRF, 발음 함 *참조 surf*)가 악의적인 웹 사이트 클라이언트 브라우저와 신뢰 하는 웹 사이트 간의 상호 작용 영향을 줄 수는 그에 따라 웹 호스팅 응용 프로그램에 대 한 공격 해당 브라우저입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-106">Cross-site request forgery (also known as XSRF or CSRF, pronounced *see-surf*) is an attack against web-hosted applications whereby a malicious web site can influence the interaction between a client browser and a web site that trusts that browser.</span></span> <span data-ttu-id="05d55-107">이러한 공격은 웹 브라우저가 웹 사이트에 일부 유형의 인증 토큰 모든 요청에 자동으로 전송 하기 때문에 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-107">These attacks are made possible because web browsers send some types of authentication tokens automatically with every request to a web site.</span></span> <span data-ttu-id="05d55-108">이러한 형태의 악용 라고도는 *원클릭 공격* 또는 as *세션 도용을*공격 활용 하는 사용자의 세션을 이전에 인증의 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-108">This form of exploit's also known as a *one-click attack* or as *session riding*, because the attack takes advantage of the user's previously authenticated session.</span></span>

<span data-ttu-id="05d55-109">CSRF 공격의 예:</span><span class="sxs-lookup"><span data-stu-id="05d55-109">An example of a CSRF attack:</span></span>

1. <span data-ttu-id="05d55-110">사용자가에 로그인 `www.example.com`, 폼 인증을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-110">A user logs into `www.example.com`, using forms authentication.</span></span>
2. <span data-ttu-id="05d55-111">서버에서 사용자를 인증 하지 않으며 인증 쿠키를 포함 하는 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-111">The server authenticates the user and issues a response that includes an authentication cookie.</span></span>
3. <span data-ttu-id="05d55-112">사용자가 악성 사이트를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-112">The user visits a malicious site.</span></span>

   <span data-ttu-id="05d55-113">악성 사이트 다음과 유사한 HTML 폼을 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-113">The malicious site contains an HTML form similar to the following:</span></span>

   ```html
   <h1>You Are a Winner!</h1>
   <form action="http://example.com/api/account" method="post">
       <input type="hidden" name="Transaction" value="withdraw">
       <input type="hidden" name="Amount" value="1000000">
       <input type="submit" value="Click Me">
   </form>
   ```

<span data-ttu-id="05d55-114">Form action에는 취약 한 사이트 악성 사이트에 게시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-114">Notice that the form action posts to the vulnerable site, not to the malicious site.</span></span> <span data-ttu-id="05d55-115">CSRF의 "사이트 간" 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-115">This is the “cross-site” part of CSRF.</span></span>

4. <span data-ttu-id="05d55-116">사용자가 제출 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-116">The user clicks the submit button.</span></span> <span data-ttu-id="05d55-117">브라우저 요청을 사용 하 여 요청 된 도메인 (이 경우에 취약 한 사이트)에 대 한 인증 쿠키를 자동으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-117">The browser automatically includes the authentication cookie for the requested domain (the vulnerable site in this case) with the request.</span></span>
5. <span data-ttu-id="05d55-118">요청은 사용자의 인증 컨텍스트를 사용 하 여 서버에서 실행 되며 인증된 된 사용자가 수행할 수 있는 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-118">The request runs on the server with the user's authentication context and can perform any action that an authenticated user is allowed to do.</span></span>

<span data-ttu-id="05d55-119">이 예제에서는 사용자 양식 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-119">This example requires the user to click the form button.</span></span> <span data-ttu-id="05d55-120">악의적인 페이지는 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-120">The malicious page could:</span></span>

* <span data-ttu-id="05d55-121">폼을 자동으로 전송 하는 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-121">Run a script that automatically submits the form.</span></span>
* <span data-ttu-id="05d55-122">양식을 제출을 하 여 AJAX 요청으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-122">Sends a form submission as an AJAX request.</span></span> 
* <span data-ttu-id="05d55-123">Css 숨겨진된 폼을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-123">Use a hidden form with CSS.</span></span> 

<span data-ttu-id="05d55-124">SSL을 사용 하 여 CSRF 공격을 방지 하지 않습니다, 악성 사이트로 보낼 수는 `https://` 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-124">Using SSL doesn't prevent a CSRF attack, the malicious site can send an `https://` request.</span></span> 

<span data-ttu-id="05d55-125">일부 공격 대상에 응답 하는 사이트 끝점 `GET` (공격의이 폼은 일반적인 포럼 사이트에 이미지를 허용 하지만 JavaScript를 차단 하는) 작업을 수행할 경우의 이미지 태그를 사용할 수 있는 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-125">Some attacks target site endpoints that respond to `GET` requests, in which case an image tag can be used to perform the action (this form of attack is common on forum sites that permit images but block JavaScript).</span></span> <span data-ttu-id="05d55-126">상태 변경 하는 응용 프로그램 `GET` 요청은 악의적인 공격에 취약 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-126">Applications that change state with `GET` requests are vulnerable from malicious attacks.</span></span>

<span data-ttu-id="05d55-127">CSRF 공격 브라우저가 대상 웹 사이트에 모든 관련 쿠키를 전송 하기 때문에 인증을 위한 쿠키를 사용 하는 웹 사이트에 대해 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-127">CSRF attacks are possible against web sites that use cookies for authentication, because browsers send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="05d55-128">그러나 CSRF 공격 쿠키 악용에 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-128">However, CSRF attacks are not limited to exploiting cookies.</span></span> <span data-ttu-id="05d55-129">예를 들어, 기본 및 다이제스트 인증 취약 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-129">For example, Basic and Digest authentication are also vulnerable.</span></span> <span data-ttu-id="05d55-130">기본 또는 다이제스트 인증을 사용 하 여 사용자가 로그 되어 세션이 종료 될 때까지 브라우저가 자동으로 자격 증명을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-130">After a user logs in with Basic or Digest authentication, the browser automatically sends the credentials until the session ends.</span></span>

<span data-ttu-id="05d55-131">참고:이 컨텍스트에서 *세션* 참조 하는 사용자가 인증 하는 클라이언트 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-131">Note: In this context, *session* refers to the client-side session during which the user is authenticated.</span></span> <span data-ttu-id="05d55-132">서버 쪽 세션에 관련 되지 않은 또는 [세션 미들웨어](xref:fundamentals/app-state)합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-132">It's unrelated to server-side sessions or [session middleware](xref:fundamentals/app-state).</span></span>

<span data-ttu-id="05d55-133">사용자가 여 CSRF 취약점을 방지할 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="05d55-133">Users can guard against CSRF vulnerabilities by:</span></span>
* <span data-ttu-id="05d55-134">웹 사이트에서 사용 하 여 종료 되었음을 로깅입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-134">Logging off of web sites when they have finished using them.</span></span>
* <span data-ttu-id="05d55-135">주기적으로 브라우저의 쿠키를 지우고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-135">Clearing their browser's cookies periodically.</span></span>

<span data-ttu-id="05d55-136">그러나 CSRF 취약점은 기본적으로 웹 앱을 최종 사용자가 아닌 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-136">However, CSRF vulnerabilities are fundamentally a problem with the web app, not the end user.</span></span>

## <a name="how-does-aspnet-core-mvc-address-csrf"></a><span data-ttu-id="05d55-137">ASP.NET Core MVC CSRF를 처리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="05d55-137">How does ASP.NET Core MVC address CSRF?</span></span>

> [!WARNING]
> <span data-ttu-id="05d55-138">ASP.NET Core request 위조 방지를 사용 하 여 구현 하는 [ASP.NET Core 데이터 보호 스택의](xref:security/data-protection/introduction)합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-138">ASP.NET Core implements anti-request-forgery using the [ASP.NET Core data protection stack](xref:security/data-protection/introduction).</span></span> <span data-ttu-id="05d55-139">ASP.NET Core 데이터 보호 서버 팜에서 작동 하도록 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-139">ASP.NET Core data protection must be configured to work in a server farm.</span></span> <span data-ttu-id="05d55-140">참조 [데이터 보호를 구성](xref:security/data-protection/configuration/overview) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-140">See [Configuring data protection](xref:security/data-protection/configuration/overview) for more information.</span></span>

<span data-ttu-id="05d55-141">ASP.NET Core anti request 위조 기본 데이터 보호 구성</span><span class="sxs-lookup"><span data-stu-id="05d55-141">ASP.NET Core anti-request-forgery default data protection configuration</span></span> 

<span data-ttu-id="05d55-142">ASP.NET Core MVC 2.0에서는 [FormTagHelper](xref:mvc/views/working-with-forms#the-form-tag-helper) HTML 폼 요소에 대 한 위조 방지 토큰을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-142">In ASP.NET Core MVC 2.0 the [FormTagHelper](xref:mvc/views/working-with-forms#the-form-tag-helper) injects anti-forgery tokens for HTML form elements.</span></span> <span data-ttu-id="05d55-143">예를 들어 Razor 파일에 다음 태그 위조 방지 토큰을 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-143">For example, the following markup in a Razor file will automatically generate anti-forgery tokens:</span></span>

```html
<form method="post">
  <!-- form markup -->
</form>
```

<span data-ttu-id="05d55-144">발생 하는 HTML 폼 요소에 대 한 자동 생성 위조 방지 토큰의 경우:</span><span class="sxs-lookup"><span data-stu-id="05d55-144">The automatic generation of anti-forgery tokens for HTML form elements happens when:</span></span>

* <span data-ttu-id="05d55-145">`form` 태그에는 `method="post"` 특성 AND</span><span class="sxs-lookup"><span data-stu-id="05d55-145">The `form` tag contains the `method="post"` attribute AND</span></span>

  * <span data-ttu-id="05d55-146">Action 특성은 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-146">The action attribute is empty.</span></span> <span data-ttu-id="05d55-147">( `action=""`) OR</span><span class="sxs-lookup"><span data-stu-id="05d55-147">( `action=""`) OR</span></span>
  * <span data-ttu-id="05d55-148">작업 특성을 제공 하지 않으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-148">The action attribute isn't supplied.</span></span> <span data-ttu-id="05d55-149">(`<form method="post">`)</span><span class="sxs-lookup"><span data-stu-id="05d55-149">(`<form method="post">`)</span></span>

<span data-ttu-id="05d55-150">위조 방지 토큰에서 HTML 폼 요소에 대 한 자동 생성을 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-150">You can disable automatic generation of anti-forgery tokens for HTML form elements by:</span></span>

* <span data-ttu-id="05d55-151">명시적으로 사용 하지 않도록 설정 `asp-antiforgery`합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-151">Explicitly disabling `asp-antiforgery`.</span></span> <span data-ttu-id="05d55-152">예</span><span class="sxs-lookup"><span data-stu-id="05d55-152">For example</span></span>

  ```html
  <form method="post" asp-antiforgery="false">
  </form>
  ```

* <span data-ttu-id="05d55-153">태그 도우미를 사용 하 여 태그 도우미 부족 form 요소를 선택할 [! 옵트아웃 기호](xref:mvc/views/tag-helpers/intro#opt-out)합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-153">Opt the form element out of Tag Helpers by using the Tag Helper [! opt-out symbol](xref:mvc/views/tag-helpers/intro#opt-out).</span></span>

  ```html
  <!form method="post">
  </!form>
  ```

* <span data-ttu-id="05d55-154">제거는 `FormTagHelper` 보기에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-154">Remove the `FormTagHelper` from the view.</span></span> <span data-ttu-id="05d55-155">제거할 수는 `FormTagHelper` Razor 보기에는 다음 지시문을 추가 하 여 보기에서:</span><span class="sxs-lookup"><span data-stu-id="05d55-155">You can remove the `FormTagHelper` from a view by adding the following directive to the Razor view:</span></span>

  ```html
  @removeTagHelper Microsoft.AspNetCore.Mvc.TagHelpers.FormTagHelper, Microsoft.AspNetCore.Mvc.TagHelpers
  ```

> [!NOTE]
> <span data-ttu-id="05d55-156">[Razor 페이지](xref:mvc/razor-pages/index) XSRF/CSRF에서 자동으로 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-156">[Razor Pages](xref:mvc/razor-pages/index) are automatically protected from XSRF/CSRF.</span></span> <span data-ttu-id="05d55-157">추가 코드를 작성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-157">You don't have to write any additional code.</span></span> <span data-ttu-id="05d55-158">참조 [XSRF/CSRF 및 Razor 페이지](xref:mvc/razor-pages/index#xsrf) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-158">See [XSRF/CSRF and Razor Pages](xref:mvc/razor-pages/index#xsrf) for more information.</span></span>

<span data-ttu-id="05d55-159">CSRF 공격 으로부터 보호 하는 데 가장 일반적인 방법은 동기화 장치 토큰 패턴이 (STP)입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-159">The most common approach to defending against CSRF attacks is the synchronizer token pattern (STP).</span></span> <span data-ttu-id="05d55-160">STP에는 사용자 페이지를 양식 데이터로 요청할 때 사용 되는 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-160">STP is a technique used when the user requests a page with form data.</span></span> <span data-ttu-id="05d55-161">서버는 클라이언트에 현재 사용자의 id와 연결 된 토큰을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-161">The server sends a token associated with the current user's identity to the client.</span></span> <span data-ttu-id="05d55-162">클라이언트가 보냅니다 확인을 위해 서버를 다시 토큰.</span><span class="sxs-lookup"><span data-stu-id="05d55-162">The client sends back the token to the server for verification.</span></span> <span data-ttu-id="05d55-163">인증 된 사용자의 id와 일치 하지 않는 토큰을 수신 하는 서버, 요청이 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-163">If the server receives a token that doesn't match the authenticated user's identity, the request is rejected.</span></span> <span data-ttu-id="05d55-164">토큰이 고유 하 고 예측할 수 없는 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-164">The token is unique and unpredictable.</span></span> <span data-ttu-id="05d55-165">토큰은 적절 한 시퀀스에는 일련의 요청 (3 페이지 앞에 오는 페이지 2 앞에 오는 등과 페이지 1) 되도록 데도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-165">The token can also be used to ensure proper sequencing of a series of requests (ensuring page 1 precedes page 2 which precedes page 3).</span></span> <span data-ttu-id="05d55-166">ASP.NET Core MVC 템플릿의 모든 양식을 antiforgery 토큰을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-166">All the forms in ASP.NET Core MVC templates generate antiforgery tokens.</span></span> <span data-ttu-id="05d55-167">뷰 논리의 다음 두 예제는 antiforgery 토큰을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-167">The following two examples of view logic generate antiforgery tokens:</span></span>

```html
<form asp-controller="Manage" asp-action="ChangePassword" method="post">

</form>

@using (Html.BeginForm("ChangePassword", "Manage"))
{
    
}
```

<span data-ttu-id="05d55-168">Antiforgery 토큰을 명시적으로 추가할 수는 `<form>` HTML 도우미와 태그 도우미를 사용 하지 않고 요소 `@Html.AntiForgeryToken`:</span><span class="sxs-lookup"><span data-stu-id="05d55-168">You can explicitly add an antiforgery token to a `<form>` element without using tag helpers with the HTML helper `@Html.AntiForgeryToken`:</span></span>


```html
<form action="/" method="post">
    @Html.AntiForgeryToken()
</form>
```

<span data-ttu-id="05d55-169">위의 경우 중 각 ASP.NET Core 다음과 유사한 숨겨진된 양식 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-169">In each of the preceding cases, ASP.NET Core will add a hidden form field similar to the following:</span></span>
```html
<input name="__RequestVerificationToken" type="hidden" value="CfDJ8NrAkSldwD9CpLRyOtm6FiJB1Jr_F3FQJQDvhlHoLNJJrLA6zaMUmhjMsisu2D2tFkAiYgyWQawJk9vNm36sYP1esHOtamBEPvSk1_x--Sg8Ey2a-d9CV2zHVWIN9MVhvKHOSyKqdZFlYDVd69XYx-rOWPw3ilHGLN6K0Km-1p83jZzF0E4WU5OGg5ns2-m9Yw">
```

<span data-ttu-id="05d55-170">ASP.NET Core 3 개 포함 [필터](xref:mvc/controllers/filters) antiforgery 토큰을 사용 하기 위한: `ValidateAntiForgeryToken`, `AutoValidateAntiforgeryToken`, 및 `IgnoreAntiforgeryToken`합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-170">ASP.NET Core includes three [filters](xref:mvc/controllers/filters) for working with antiforgery tokens: `ValidateAntiForgeryToken`, `AutoValidateAntiforgeryToken`, and `IgnoreAntiforgeryToken`.</span></span>

### <a name="validateantiforgerytoken"></a><span data-ttu-id="05d55-171">ValidateAntiForgeryToken</span><span class="sxs-lookup"><span data-stu-id="05d55-171">ValidateAntiForgeryToken</span></span>

<span data-ttu-id="05d55-172">`ValidateAntiForgeryToken` 는 개별 작업은 컨트롤러에 적용할 수 있는 작업 필터는 전역적으로 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-172">The `ValidateAntiForgeryToken` is an action filter that can be applied to an individual action, a controller, or globally.</span></span> <span data-ttu-id="05d55-173">요청에 유효한 antiforgery 토큰에 포함 되지 않으면이 필터 적용이 영향을 주는 작업에 대 한 요청을 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-173">Requests made to actions that have this filter applied will be blocked unless the request includes a valid antiforgery token.</span></span>

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<IActionResult> RemoveLogin(RemoveLoginViewModel account)
{
    ManageMessageId? message = ManageMessageId.Error;
    var user = await GetCurrentUserAsync();
    if (user != null)
    {
        var result = await _userManager.RemoveLoginAsync(user, account.LoginProvider, account.ProviderKey);
        if (result.Succeeded)
        {
            await _signInManager.SignInAsync(user, isPersistent: false);
            message = ManageMessageId.RemoveLoginSuccess;
        }
    }
    return RedirectToAction(nameof(ManageLogins), new { Message = message });
}
```

<span data-ttu-id="05d55-174">`ValidateAntiForgeryToken` 특성 포함 하 여 데코레이팅되 작업 메서드에 요청에 대 한 토큰 요구 `HTTP GET` 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-174">The `ValidateAntiForgeryToken` attribute requires a token for requests to action methods it decorates, including `HTTP GET` requests.</span></span> <span data-ttu-id="05d55-175">광범위 하 게 적용 하는 경우 사용 하 여 재정의할 수 있습니다는 `IgnoreAntiforgeryToken` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-175">If you apply it broadly, you can override it with the `IgnoreAntiforgeryToken` attribute.</span></span>

### <a name="autovalidateantiforgerytoken"></a><span data-ttu-id="05d55-176">AutoValidateAntiforgeryToken</span><span class="sxs-lookup"><span data-stu-id="05d55-176">AutoValidateAntiforgeryToken</span></span>

<span data-ttu-id="05d55-177">ASP.NET Core 응용 프로그램은 일반적으로 HTTP는 안전 메서드 (GET, HEAD, 옵션 및 추적)에 대 한 antiforgery 토큰 생성 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-177">ASP.NET Core apps generally don't generate antiforgery tokens for HTTP safe methods (GET, HEAD, OPTIONS, and TRACE).</span></span> <span data-ttu-id="05d55-178">광범위 하 게 적용 하는 대신는 `ValidateAntiForgeryToken` 특성과 다음 사용 하 여 재정의 `IgnoreAntiforgeryToken` 사용할 수 있습니다 특성은 ``AutoValidateAntiforgeryToken`` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-178">Instead of broadly applying the `ValidateAntiForgeryToken` attribute and then overriding it with `IgnoreAntiforgeryToken` attributes, you can use the ``AutoValidateAntiforgeryToken`` attribute.</span></span> <span data-ttu-id="05d55-179">이 특성은 동일 하 게 작동는 `ValidateAntiForgeryToken` 특성을 제외 하 고 토큰에 대 한 다음과 같은 HTTP 메서드를 사용 하 여 요청 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-179">This attribute works identically to the `ValidateAntiForgeryToken` attribute, except that it doesn't require tokens for requests made using the following HTTP methods:</span></span>

* <span data-ttu-id="05d55-180">가져오기</span><span class="sxs-lookup"><span data-stu-id="05d55-180">GET</span></span>
* <span data-ttu-id="05d55-181">HEAD</span><span class="sxs-lookup"><span data-stu-id="05d55-181">HEAD</span></span>
* <span data-ttu-id="05d55-182">옵션</span><span class="sxs-lookup"><span data-stu-id="05d55-182">OPTIONS</span></span>
* <span data-ttu-id="05d55-183">TRACE</span><span class="sxs-lookup"><span data-stu-id="05d55-183">TRACE</span></span>

<span data-ttu-id="05d55-184">사용 하는 것이 좋습니다 `AutoValidateAntiforgeryToken` 비 API 시나리오에 대 한 광범위 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-184">We recommend you use `AutoValidateAntiforgeryToken` broadly for non-API scenarios.</span></span> <span data-ttu-id="05d55-185">이렇게 하면 기본적으로 POST 작업 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-185">This ensures your POST actions are protected by default.</span></span> <span data-ttu-id="05d55-186">대신 사용 하는 표시 되지 않으면 기본적으로 antiforgery 토큰을 무시 하도록 `ValidateAntiForgeryToken` 개별 작업 메서드에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-186">The alternative is to ignore antiforgery tokens by default, unless `ValidateAntiForgeryToken` is applied to the individual action method.</span></span> <span data-ttu-id="05d55-187">되도록 POST 작업 메서드에 대 한이 시나리오에서 더 많이 왼쪽 보호 되지 CSRF 공격에 취약 한 응용 프로그램을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-187">It's more likely in this scenario for a POST action method to be left unprotected, leaving your app vulnerable to CSRF attacks.</span></span> <span data-ttu-id="05d55-188">도 익명 게시물 antiforgery 토큰을 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-188">Even anonymous POSTS should send the antiforgery token.</span></span>

<span data-ttu-id="05d55-189">참고: Api 토큰;의 쿠키 일부로 보내기 위한 자동 메커니즘 없는 구현은 클라이언트 코드 구현에 따라 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-189">Note: APIs don't have an automatic mechanism for sending the non-cookie part of the token; your implementation will likely depend on your client code implementation.</span></span> <span data-ttu-id="05d55-190">몇 가지 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-190">Some examples are shown below.</span></span>

<span data-ttu-id="05d55-191">예 (클래스 수준):</span><span class="sxs-lookup"><span data-stu-id="05d55-191">Example (class level):</span></span>

```csharp
[Authorize]
[AutoValidateAntiforgeryToken]
public class ManageController : Controller
{
```

<span data-ttu-id="05d55-192">예 (전역):</span><span class="sxs-lookup"><span data-stu-id="05d55-192">Example (global):</span></span>

```csharp
services.AddMvc(options => 
    options.Filters.Add(new AutoValidateAntiforgeryTokenAttribute()));
```

<a name="iaft"></a>

### <a name="ignoreantiforgerytoken"></a><span data-ttu-id="05d55-193">IgnoreAntiforgeryToken</span><span class="sxs-lookup"><span data-stu-id="05d55-193">IgnoreAntiforgeryToken</span></span>

<span data-ttu-id="05d55-194">`IgnoreAntiforgeryToken` 필터는 지정 된 작업 (또는 컨트롤러)를 사용할 수는 antiforgery 토큰에 대 한 필요성을 제거 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-194">The `IgnoreAntiforgeryToken` filter is used to eliminate the need for an antiforgery token to be present for a given action (or controller).</span></span> <span data-ttu-id="05d55-195">이 필터는 재정의 적용 하면 `ValidateAntiForgeryToken` 및/또는 `AutoValidateAntiforgeryToken` (전역적으로 또는 컨트롤러)는 더 높은 수준에서 지정 된 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-195">When applied, this filter will override `ValidateAntiForgeryToken` and/or `AutoValidateAntiforgeryToken` filters specified at a higher level (globally or on a controller).</span></span>

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

## <a name="javascript-ajax-and-spas"></a><span data-ttu-id="05d55-196">JavaScript, AJAX 및 SPAs</span><span class="sxs-lookup"><span data-stu-id="05d55-196">JavaScript, AJAX, and SPAs</span></span>

<span data-ttu-id="05d55-197">기존의 HTML 기반 응용 프로그램, antiforgery 토큰 숨겨진된 양식 필드를 사용 하 여 서버에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-197">In traditional HTML-based applications, antiforgery tokens are passed to the server using hidden form fields.</span></span> <span data-ttu-id="05d55-198">최신 JavaScript 기반 응용 프로그램 및 단일 페이지 응용 프로그램 (SPAs)에서 많은 요청이 프로그래밍 방식으로 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-198">In modern JavaScript-based apps and single page applications (SPAs), many requests are made programmatically.</span></span> <span data-ttu-id="05d55-199">이러한 AJAX 요청 토큰 다른 기술 (예: 요청 헤더 또는 쿠키)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-199">These AJAX requests may use other techniques (such as request headers or cookies) to send the token.</span></span> <span data-ttu-id="05d55-200">인증 토큰을 저장 하 고 서버에 대 한 API 요청을 인증 쿠키를 사용 하는 경우에 CSRF 잠재적인 문제 수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-200">If cookies are used to store authentication tokens and to authenticate API requests on the server, then CSRF will be a potential problem.</span></span> <span data-ttu-id="05d55-201">그러나 로컬 저장소를 사용 하 여 토큰을 저장, CSRF 취약점 완화할 수 있습니다, 이후 모든 새 요청을 사용 하 여 서버에 로컬 저장소의 값을 자동으로 보내지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-201">However, if local storage is used to store the token, CSRF vulnerability may be mitigated, since values from local storage are not sent automatically to the server with every new request.</span></span> <span data-ttu-id="05d55-202">따라서 요청 헤더는 권장된 방법으로 토큰을 보내는 클라이언트에 antiforgery 토큰을 저장할 로컬 저장소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-202">Thus, using local storage to store the antiforgery token on the client and sending the token as a request header is a recommended approach.</span></span>

### <a name="angularjs"></a><span data-ttu-id="05d55-203">AngularJS</span><span class="sxs-lookup"><span data-stu-id="05d55-203">AngularJS</span></span>

<span data-ttu-id="05d55-204">AngularJS는 CSRF 주소로 규칙을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-204">AngularJS uses a convention to address CSRF.</span></span> <span data-ttu-id="05d55-205">서버 이름으로 쿠키를 전송 하는 경우 `XSRF-TOKEN`는 각 `$http` 서비스에서 값에서이 쿠키를 추가 헤더는이 서버에 요청을 보낼 때.</span><span class="sxs-lookup"><span data-stu-id="05d55-205">If the server sends a cookie with the name `XSRF-TOKEN`, the Angular `$http` service will add the value from this cookie to a header when it sends a request to this server.</span></span> <span data-ttu-id="05d55-206">이 프로세스는 자동; 헤더를 명시적으로 설정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-206">This process is automatic; you don't need to set the header explicitly.</span></span> <span data-ttu-id="05d55-207">헤더 이름이 `X-XSRF-TOKEN`합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-207">The header name is `X-XSRF-TOKEN`.</span></span> <span data-ttu-id="05d55-208">서버는이 헤더를 검색 하 고 해당 내용의 유효성을 검사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-208">The server should detect this header and validate its contents.</span></span>

<span data-ttu-id="05d55-209">ASP.NET Core API에 대 한이 규칙을 통해 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-209">For ASP.NET Core API work with this convention:</span></span>

* <span data-ttu-id="05d55-210">호출 하는 쿠키에 토큰을 제공할 앱 구성 `XSRF-TOKEN`</span><span class="sxs-lookup"><span data-stu-id="05d55-210">Configure your app to provide a token in a cookie called `XSRF-TOKEN`</span></span>
* <span data-ttu-id="05d55-211">라는 헤더 찾으려는 antiforgery 서비스 구성 `X-XSRF-TOKEN`</span><span class="sxs-lookup"><span data-stu-id="05d55-211">Configure the antiforgery service to look for a header named `X-XSRF-TOKEN`</span></span>

```csharp
services.AddAntiforgery(options => options.HeaderName = "X-XSRF-TOKEN");
```

<span data-ttu-id="05d55-212">[보기 샘플](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/anti-request-forgery/sample/AngularSample)합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-212">[View sample](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/anti-request-forgery/sample/AngularSample).</span></span>

### <a name="javascript"></a><span data-ttu-id="05d55-213">JavaScript</span><span class="sxs-lookup"><span data-stu-id="05d55-213">JavaScript</span></span>

<span data-ttu-id="05d55-214">JavaScript에서 뷰를 사용 하 여 보기 내에서 서비스를 사용 하 여 토큰을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-214">Using JavaScript with views, you can create the token using a service from within your view.</span></span> <span data-ttu-id="05d55-215">이 위해 삽입는 `Microsoft.AspNetCore.Antiforgery.IAntiforgery` 보기 및 호출 계층에 서비스 `GetAndStoreTokens`표시 된 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="05d55-215">To do so, you inject the `Microsoft.AspNetCore.Antiforgery.IAntiforgery` service into the view and call `GetAndStoreTokens`, as shown:</span></span>

[!code-csharp[](anti-request-forgery/sample/MvcSample/Views/Home/Ajax.cshtml?highlight=4-10,12-13,28)]

<span data-ttu-id="05d55-216">이 방법은 서버에서 쿠키를 설정 하거나 클라이언트에서 읽기를 직접 사용 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-216">This approach eliminates the need to deal directly with setting cookies from the server or reading them from the client.</span></span>

<span data-ttu-id="05d55-217">앞의 예제 jQuery를 사용 하 여 AJAX POST 헤더에 대 한 숨겨진된 필드 값을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-217">The preceding example uses jQuery to read the hidden field value for the AJAX POST header.</span></span> <span data-ttu-id="05d55-218">토큰의 값을 얻기 위해 JavaScript를 사용 하려면 사용 하 여 `document.getElementById('RequestVerificationToken').value`합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-218">To use JavaScript to obtain the token's value, use `document.getElementById('RequestVerificationToken').value`.</span></span>

<span data-ttu-id="05d55-219">JavaScript 쿠키, 제공 된 토큰에 액세스할 수도 아래와 같이 쿠키의 내용이 토큰의 값을 가진 헤더를 만드는 데 사용할 수 있으며</span><span class="sxs-lookup"><span data-stu-id="05d55-219">JavaScript can also access tokens provided in cookies, and then use the cookie's contents to create a header with the token's value, as shown below.</span></span>

```csharp
context.Response.Cookies.Append("CSRF-TOKEN", tokens.RequestToken, 
  new Microsoft.AspNetCore.Http.CookieOptions { HttpOnly = false });
```

<span data-ttu-id="05d55-220">그런 다음 스크립트를 작성 하는 것으로 가정 요청 헤더에 토큰을 보냅니다 `X-CSRF-TOKEN`, antiforgery 서비스를 찾도록 구성 된 `X-CSRF-TOKEN` 헤더:</span><span class="sxs-lookup"><span data-stu-id="05d55-220">Then, assuming you construct your script requests to send the token in a header called `X-CSRF-TOKEN`, configure the antiforgery service to look for the `X-CSRF-TOKEN` header:</span></span>

```csharp
services.AddAntiforgery(options => options.HeaderName = "X-CSRF-TOKEN");
```

<span data-ttu-id="05d55-221">다음 예제에서는 jQuery를 사용 하 여 적절 한 헤더를 사용 하는 AJAX 요청 확인.</span><span class="sxs-lookup"><span data-stu-id="05d55-221">The following example uses jQuery to make an AJAX request with the appropriate header:</span></span>

```javascript
var csrfToken = $.cookie("CSRF-TOKEN");

$.ajax({
    url: "/api/password/changepassword",
    contentType: "application/json",
    data: JSON.stringify({ "newPassword": "ReallySecurePassword999$$$" }),
    type: "POST",
    headers: {
        "X-CSRF-TOKEN": csrfToken
    }
});
```

## <a name="configuring-antiforgery"></a><span data-ttu-id="05d55-222">Antiforgery 구성</span><span class="sxs-lookup"><span data-stu-id="05d55-222">Configuring Antiforgery</span></span>

<span data-ttu-id="05d55-223">`IAntiforgery` antiforgery 시스템을 구성 하는 API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-223">`IAntiforgery` provides the API to configure the antiforgery system.</span></span> <span data-ttu-id="05d55-224">서비스를 요청할 수 있습니다는 `Configure` 의 메서드는 `Startup` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-224">It can be requested in the `Configure` method of the `Startup` class.</span></span> <span data-ttu-id="05d55-225">다음 예제에서는 응용 프로그램의 홈 페이지에서 미들웨어를 사용 하 여 antiforgery 토큰을 생성 하 고 쿠키 (기본 각도 명명 규칙 위에서 설명한 사용)으로 응답에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-225">The following example uses middleware from the app's home page to generate an antiforgery token and send it in the response as a cookie (using the default Angular naming convention described above):</span></span>


```csharp
public void Configure(IApplicationBuilder app, 
    IAntiforgery antiforgery)
{
    app.Use(next => context =>
    {
        string path = context.Request.Path.Value;
        if (
            string.Equals(path, "/", StringComparison.OrdinalIgnoreCase) ||
            string.Equals(path, "/index.html", StringComparison.OrdinalIgnoreCase))
        {
            // We can send the request token as a JavaScript-readable cookie, 
            // and Angular will use it by default.
            var tokens = antiforgery.GetAndStoreTokens(context);
            context.Response.Cookies.Append("XSRF-TOKEN", tokens.RequestToken, 
                new CookieOptions() { HttpOnly = false });
        }

        return next(context);
    });
    //
}
```

### <a name="options"></a><span data-ttu-id="05d55-226">옵션</span><span class="sxs-lookup"><span data-stu-id="05d55-226">Options</span></span>

<span data-ttu-id="05d55-227">사용자 지정할 수 있습니다 [antiforgery 옵션](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions#fields_summary) 에 `ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="05d55-227">You can customize [antiforgery options](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions#fields_summary) in `ConfigureServices`:</span></span>

```csharp
services.AddAntiforgery(options => 
{
    options.CookieDomain = "mydomain.com";
    options.CookieName = "X-CSRF-TOKEN-COOKIENAME";
    options.CookiePath = "Path";
    options.FormFieldName = "AntiforgeryFieldname";
    options.HeaderName = "X-CSRF-TOKEN-HEADERNAME";
    options.RequireSsl = false;
    options.SuppressXFrameOptionsHeader = false;
});
```

<!-- QAfix fix table -->

|<span data-ttu-id="05d55-228">옵션</span><span class="sxs-lookup"><span data-stu-id="05d55-228">Option</span></span>        | <span data-ttu-id="05d55-229">설명</span><span class="sxs-lookup"><span data-stu-id="05d55-229">Description</span></span> |
|------------- | ----------- |
|<span data-ttu-id="05d55-230">CookieDomain</span><span class="sxs-lookup"><span data-stu-id="05d55-230">CookieDomain</span></span>  | <span data-ttu-id="05d55-231">쿠키의 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-231">The domain of the cookie.</span></span> <span data-ttu-id="05d55-232">기본값은 `null`입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-232">Defaults to `null`.</span></span> |
|<span data-ttu-id="05d55-233">CookieName</span><span class="sxs-lookup"><span data-stu-id="05d55-233">CookieName</span></span>    | <span data-ttu-id="05d55-234">쿠키의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-234">The name of the cookie.</span></span> <span data-ttu-id="05d55-235">을 설정 하지는 시스템 생성 됩니다로 시작 하는 고유한 이름을 `DefaultCookiePrefix` (". AspNetCore.Antiforgery입니다. ")입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-235">If not set, the system will generate a unique name beginning with the `DefaultCookiePrefix` (".AspNetCore.Antiforgery.").</span></span> |
|<span data-ttu-id="05d55-236">CookiePath</span><span class="sxs-lookup"><span data-stu-id="05d55-236">CookiePath</span></span>    | <span data-ttu-id="05d55-237">쿠키에 설정 된 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-237">The path set on the cookie.</span></span> |
|<span data-ttu-id="05d55-238">FormFieldName</span><span class="sxs-lookup"><span data-stu-id="05d55-238">FormFieldName</span></span> | <span data-ttu-id="05d55-239">뷰에서 antiforgery 토큰을 렌더링 하는 antiforgery 시스템에서 사용 하는 숨겨진된 폼 필드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-239">The name of the hidden form field used by the antiforgery system to render antiforgery tokens in views.</span></span> |
|<span data-ttu-id="05d55-240">HeaderName</span><span class="sxs-lookup"><span data-stu-id="05d55-240">HeaderName</span></span>    | <span data-ttu-id="05d55-241">Antiforgery 시스템에서 사용 하는 헤더의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-241">The name of the header used by the antiforgery system.</span></span> <span data-ttu-id="05d55-242">경우 `null`, 시스템은만 양식 데이터를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-242">If `null`, the system will consider only form data.</span></span> |
|<span data-ttu-id="05d55-243">RequireSsl</span><span class="sxs-lookup"><span data-stu-id="05d55-243">RequireSsl</span></span>    | <span data-ttu-id="05d55-244">Antiforgery 시스템에서 SSL이 필요한 지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-244">Specifies whether SSL is required by the antiforgery system.</span></span> <span data-ttu-id="05d55-245">기본값은 `false`입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-245">Defaults to `false`.</span></span> <span data-ttu-id="05d55-246">경우 `true`, 비 SSL 요청이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-246">If `true`, non-SSL requests will fail.</span></span> |
|<span data-ttu-id="05d55-247">SuppressXFrameOptionsHeader</span><span class="sxs-lookup"><span data-stu-id="05d55-247">SuppressXFrameOptionsHeader</span></span> | <span data-ttu-id="05d55-248">생성을 표시 하지 않을 것인지를 지정 된 `X-Frame-Options` 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-248">Specifies whether to suppress generation of the `X-Frame-Options` header.</span></span> <span data-ttu-id="05d55-249">기본적으로 머리글은 "SAMEORIGIN"의 값으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-249">By default, the header is generated with a value of "SAMEORIGIN".</span></span> <span data-ttu-id="05d55-250">기본값은 `false`입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-250">Defaults to `false`.</span></span> |

<span data-ttu-id="05d55-251">Https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.cookieauthenticationoptions 대 한 자세한 정보를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="05d55-251">See https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.builder.cookieauthenticationoptions for more info.</span></span>

### <a name="extending-antiforgery"></a><span data-ttu-id="05d55-252">Antiforgery 확장</span><span class="sxs-lookup"><span data-stu-id="05d55-252">Extending Antiforgery</span></span>

<span data-ttu-id="05d55-253">[IAntiForgeryAdditionalDataProvider](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider) 형식에서는 개발자가 각 토큰의 추가 데이터를 왕복 하 여 ANTI-XSRF 시스템의 동작을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-253">The [IAntiForgeryAdditionalDataProvider](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider) type allows developers to extend the behavior of the anti-XSRF system by round-tripping additional data in each token.</span></span> <span data-ttu-id="05d55-254">[GetAdditionalData](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider#Microsoft_AspNetCore_Antiforgery_IAntiforgeryAdditionalDataProvider_GetAdditionalData_Microsoft_AspNetCore_Http_HttpContext_) 될 때마다 메서드는 필드 토큰이 생성 되 고 반환 값은 생성 되는 토큰 내에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-254">The [GetAdditionalData](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider#Microsoft_AspNetCore_Antiforgery_IAntiforgeryAdditionalDataProvider_GetAdditionalData_Microsoft_AspNetCore_Http_HttpContext_) method is called each time a field token is generated, and the return value is embedded within the generated token.</span></span> <span data-ttu-id="05d55-255">구현 자가 수 타임 스탬프, nonce, 또는 다른 모든 값을 반환 하 고 호출 [ValidateAdditionalData](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider#Microsoft_AspNetCore_Antiforgery_IAntiforgeryAdditionalDataProvider_ValidateAdditionalData_Microsoft_AspNetCore_Http_HttpContext_System_String_) 토큰의 유효성을 검사할 때이 데이터를 유효성 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-255">An implementer could return a timestamp, a nonce, or any other value and then call [ValidateAdditionalData](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider#Microsoft_AspNetCore_Antiforgery_IAntiforgeryAdditionalDataProvider_ValidateAdditionalData_Microsoft_AspNetCore_Http_HttpContext_System_String_) to validate this data when the token is validated.</span></span> <span data-ttu-id="05d55-256">클라이언트의 사용자 이름은 이미 생성 된 토큰에 포함 되어 있으므로이 정보를 포함할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-256">The client's username is already embedded in the generated tokens, so there's no need to include this information.</span></span> <span data-ttu-id="05d55-257">아니지만 추가 데이터 토큰을 포함 하는 경우 `IAntiForgeryAdditionalDataProvider` 된 구성, 보조 데이터 확인 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-257">If a token includes supplemental data but no `IAntiForgeryAdditionalDataProvider` has been configured, the supplemental data isn't validated.</span></span>

## <a name="fundamentals"></a><span data-ttu-id="05d55-258">기본 사항</span><span class="sxs-lookup"><span data-stu-id="05d55-258">Fundamentals</span></span>

<span data-ttu-id="05d55-259">CSRF 공격 도메인과 해당 도메인에 대 한 모든 요청 연관 된 쿠키를 보낼 기본 브라우저 동작에 의존 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-259">CSRF attacks rely on the default browser behavior of sending cookies associated with a domain with every request made to that domain.</span></span> <span data-ttu-id="05d55-260">이러한 쿠키는 브라우저 내에서 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-260">These cookies are stored within the browser.</span></span> <span data-ttu-id="05d55-261">인증 된 사용자에 대 한 세션 쿠키가 포함 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-261">They frequently include session cookies for authenticated users.</span></span> <span data-ttu-id="05d55-262">쿠키 기반 인증에는 인기 있는 형태의 인증입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-262">Cookie-based authentication is a popular form of authentication.</span></span> <span data-ttu-id="05d55-263">SPAs 및 기타 "스마트 클라이언트" 시나리오에 특히 토큰 기반 인증 시스템에서 인기, 증가 하 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-263">Token-based authentication systems have been growing in popularity, especially for SPAs and other "smart client" scenarios.</span></span>

### <a name="cookie-based-authentication"></a><span data-ttu-id="05d55-264">쿠키 기반 인증</span><span class="sxs-lookup"><span data-stu-id="05d55-264">Cookie-based authentication</span></span>

<span data-ttu-id="05d55-265">사용자가 자신의 사용자 이름과 암호를 사용 하 여 인증가 식별 하 고 인증 되었는지 유효성을 검사 하는 데 사용할 수 있는 토큰을 발급 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-265">Once a user has authenticated using their username and password, they're issued a token that can be used to identify them and validate that they have been authenticated.</span></span> <span data-ttu-id="05d55-266">토큰이는 클라이언트는 모든 요청을 함께 제공 되는 쿠키 함에 따라 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-266">The token is stored as a cookie that accompanies every request the client makes.</span></span> <span data-ttu-id="05d55-267">생성 하 고이 쿠키를 유효성 검사 쿠키 인증 미들웨어에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-267">Generating and validating this cookie is done by the cookie authentication middleware.</span></span> <span data-ttu-id="05d55-268">ASP.NET Core 쿠키를 제공 합니다. [미들웨어](xref:fundamentals/middleware/index) 주 서버를 다시 만들어 암호화 된 쿠키에 사용자 계정 또는 그 반대로 serialize 하 고 그런 다음 이후 요청에서 쿠키를 유효성을 검사에 할당 합니다는 `User` 속성 `HttpContext`.</span><span class="sxs-lookup"><span data-stu-id="05d55-268">ASP.NET Core provides cookie [middleware](xref:fundamentals/middleware/index) which serializes a user principal into an encrypted cookie and then, on subsequent requests, validates the cookie, recreates the principal and assigns it to the `User` property on `HttpContext`.</span></span>

<span data-ttu-id="05d55-269">쿠키를 사용 하면 인증 쿠키가 단순한 폼 인증 티켓에 대 한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-269">When a cookie is used, The authentication cookie is just a container for the forms authentication ticket.</span></span> <span data-ttu-id="05d55-270">티켓 각 요청과 함께 폼 인증 쿠키의 값으로 전달 되 고 인증된 된 사용자를 식별 하는 서버에서 폼 인증에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-270">The ticket is passed as the value of the forms authentication cookie with each request and is used by forms authentication, on the server, to identify an authenticated user.</span></span>

<span data-ttu-id="05d55-271">사용자가 시스템에 로그인 할 때 사용자 세션 서버 측에서 만들어지고 데이터베이스나 다른 영구 저장소에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-271">When a user is logged in to a system, a user session is created on the server-side and is stored in a database or some other persistent store.</span></span> <span data-ttu-id="05d55-272">시스템 데이터 저장소에 실제 세션에 연결 되는 세션 키를 생성 하 고 클라이언트 쪽 쿠키로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-272">The system generates a session key that points to the actual session in the data store and it's sent as a client side cookie.</span></span> <span data-ttu-id="05d55-273">웹 서버 사용자 권한 부여를 요구 하는 리소스를 요청 하는 언제 든 지가 세션 키를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-273">The web server will check this session key any time a user requests a resource that requires authorization.</span></span> <span data-ttu-id="05d55-274">시스템 연결 된 사용자 세션에 요청된 된 리소스에 액세스할 수 있는 권한이 있는지 여부를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-274">The system checks whether the associated user session has the privilege to access the requested resource.</span></span> <span data-ttu-id="05d55-275">이 경우 요청은 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-275">If so, the request continues.</span></span> <span data-ttu-id="05d55-276">그렇지 않으면, 요청이 인증 되지 않았습니다.으로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-276">Otherwise, the request returns as not authorized.</span></span> <span data-ttu-id="05d55-277">이 방법에서는 상태 저장 것 처럼 응용 프로그램을 쿠키를 사용, 사용자가 서버와 이전에 인증 하 고 "기억" 하는 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-277">In this approach, cookies are used to make the application appear to be stateful, since it's able to "remember" that the user has previously authenticated with the server.</span></span>

### <a name="user-tokens"></a><span data-ttu-id="05d55-278">사용자 토큰</span><span class="sxs-lookup"><span data-stu-id="05d55-278">User tokens</span></span>

<span data-ttu-id="05d55-279">토큰 기반 인증 서버에 세션을 저장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-279">Token-based authentication doesn't store session on the server.</span></span> <span data-ttu-id="05d55-280">사용자가 로그인 할 때 (하지 antiforgery 토큰) 토큰을 발급 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-280">When a user is logged in, they're issued a token (not an antiforgery token).</span></span> <span data-ttu-id="05d55-281">이 토큰은 토큰의 유효성을 검사 하는 데 필요한 데이터를 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-281">This token holds the data that's required to validate the token.</span></span> <span data-ttu-id="05d55-282">또한 정보가 사용자의 형태로 [클레임](https://docs.microsoft.com/dotnet/framework/security/claims-based-identity-model)합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-282">It also contains user information in the form of [claims](https://docs.microsoft.com/dotnet/framework/security/claims-based-identity-model).</span></span> <span data-ttu-id="05d55-283">사용자가 인증을 요구 하는 서버 리소스에 액세스 하려고 하는 경우 토큰이 전달자 {토큰}의 양식에서 추가 인증 헤더를 사용 하 여 서버에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-283">When a user wants to access a server resource requiring authentication, the token is sent to the server with an additional authorization header in form of Bearer {token}.</span></span> <span data-ttu-id="05d55-284">이렇게 하면 응용 프로그램 상태 비저장 각 후속 요청에 토큰은 전달 요청에 서버 쪽 유효성 검사에 대 한 이후 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-284">This makes the application stateless since in each subsequent request the token is passed in the request for server-side validation.</span></span> <span data-ttu-id="05d55-285">이 토큰이 없는 *암호화 된*; 보다는 *인코딩된*합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-285">This token isn't *encrypted*; rather it's *encoded*.</span></span> <span data-ttu-id="05d55-286">서버 쪽에서 토큰 내에서 원시 정보에 액세스 하려면 토큰을 디코딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-286">On the server-side, the token can be decoded to access the raw information within the token.</span></span> <span data-ttu-id="05d55-287">토큰의 후속 요청을 보내려면 하나 저장 브라우저의 로컬 저장소에 또는 쿠키에 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-287">To send the token in subsequent requests, either store it in the browser's local storage or in a cookie.</span></span> <span data-ttu-id="05d55-288">토큰의 로컬 저장소에 저장 되어 있지만 토큰 쿠키에 저장 되는 경우 문제가 발생 하는 경우에 XSRF 취약점에 대 한 걱정 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="05d55-288">Don't worry about XSRF vulnerability if the token is stored in the local storage, but it's an issue if the token is stored in a cookie.</span></span>

### <a name="multiple-applications-are-hosted-in-one-domain"></a><span data-ttu-id="05d55-289">여러 응용 프로그램 도메인에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-289">Multiple applications are hosted in one domain</span></span>

<span data-ttu-id="05d55-290">하지만 `example1.cloudapp.net` 및 `example2.cloudapp.net` 는 서로 다른 호스트에서 호스트 간의 암시적 트러스트 관계가 있는 `*.cloudapp.net` 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-290">Although `example1.cloudapp.net` and `example2.cloudapp.net` are different hosts, there's an implicit trust relationship between hosts under the `*.cloudapp.net` domain.</span></span> <span data-ttu-id="05d55-291">이 암시적 트러스트 관계에는 신뢰할 수 없는 호스트를 (AJAX 요청을 제어 하는 동일 원본 정책 반드시 HTTP 쿠키를 적용 하지 않는) 다른 사용자의 쿠키에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-291">This implicit trust relationship allows potentially untrusted hosts to affect each other's cookies (the same-origin policies that govern AJAX requests don't necessarily apply to HTTP cookies).</span></span> <span data-ttu-id="05d55-292">ASP.NET Core 런타임 사용자 이름 필드 토큰에 포함 되는 몇 가지 완화를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-292">The ASP.NET Core runtime provides some mitigation in that the username is embedded into the field token.</span></span> <span data-ttu-id="05d55-293">세션 토큰을 덮어쓸 수는 악의적인 하위 도메인 경우 사용자에 대 한 유효한 필드 토큰을 생성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-293">Even if a malicious subdomain is able to overwrite a session token, it can't generate a valid field token for the user.</span></span> <span data-ttu-id="05d55-294">이러한 환경에서 호스트 되는 경우 기본 제공 ANTI-XSRF 루틴 여전히 없습니다 공격을 방어할 세션 하이재킹 또는 CSRF 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-294">When hosted in such an environment, the built-in anti-XSRF routines still can't defend against session hijacking or login CSRF attacks.</span></span> <span data-ttu-id="05d55-295">공유 호스팅 환경 세션 하이재킹, CSRF, 로그인 및 기타 공격 vunerable 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05d55-295">Shared hosting environments are vunerable to session hijacking, login CSRF, and other attacks.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="05d55-296">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="05d55-296">Additional resources</span></span>

* <span data-ttu-id="05d55-297">[XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)) 에 [웹 응용 프로그램 보안 프로젝트를 열고](https://www.owasp.org/index.php/Main_Page) (OWASP).</span><span class="sxs-lookup"><span data-stu-id="05d55-297">[XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)) on [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP).</span></span>
