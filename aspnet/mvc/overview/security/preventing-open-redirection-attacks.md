---
uid: mvc/overview/security/preventing-open-redirection-attacks
title: 열린 리디렉션 공격 방지 (C#) | Microsoft Docs
author: jongalloway
description: 이 자습서에서는 ASP.NET MVC 응용 프로그램에서 열려 리디렉션 공격을 방지 하는 방법에 대해 설명 합니다. 이 자습서에는 적용 된 변경 사항에 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/27/2014
ms.topic: article
ms.assetid: 69fb02e0-f5b7-4c35-878c-fa87164fc785
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/security/preventing-open-redirection-attacks
msc.type: authoredcontent
ms.openlocfilehash: ec1cd1791eb6d32e7c1ea50bc6626929cad2960e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="preventing-open-redirection-attacks-c"></a><span data-ttu-id="3b600-104">열린 리디렉션 공격 방지 (C#)</span><span class="sxs-lookup"><span data-stu-id="3b600-104">Preventing Open Redirection Attacks (C#)</span></span>
====================
<span data-ttu-id="3b600-105">으로 [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="3b600-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="3b600-106">이 자습서에서는 ASP.NET MVC 응용 프로그램에서 열려 리디렉션 공격을 방지 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-106">This tutorial explains how you can prevent open redirection attacks in your ASP.NET MVC applications.</span></span> <span data-ttu-id="3b600-107">이 자습서 AccountController ASP.NET MVC 3에서에서 적용 된 변경에 설명 하 고 기존 ASP.NET MVC 1.0 프로그램 및 2 응용 프로그램에서 이러한 변경 내용을 적용 하는 방법을 시연 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-107">This tutorial discusses the changes that have been made in the AccountController in ASP.NET MVC 3 and demonstrates how you can apply these changes in your existing ASP.NET MVC 1.0 and 2 applications.</span></span>


## <a name="what-is-an-open-redirection-attack"></a><span data-ttu-id="3b600-108">열린 리디렉션 공격 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="3b600-108">What is an Open Redirection Attack?</span></span>

<span data-ttu-id="3b600-109">잠재적으로 쿼리 문자열 또는 폼 데이터와 같은 요청을 통해 지정 된 URL로 리디렉션하는 웹 응용 프로그램 외부, 악성 URL로 사용자를 리디렉션하기와 훼손 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-109">Any web application that redirects to a URL that is specified via the request such as the querystring or form data can potentially be tampered with to redirect users to an external, malicious URL.</span></span> <span data-ttu-id="3b600-110">이 변조 열려 리디렉션 공격을 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-110">This tampering is called an open redirection attack.</span></span>

<span data-ttu-id="3b600-111">응용 프로그램 논리를 지정 된 URL로 리디렉션합니다, 때마다와 리디렉션 URL이 손상 되지 않았음을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-111">Whenever your application logic redirects to a specified URL, you must verify that the redirection URL hasn't been tampered with.</span></span> <span data-ttu-id="3b600-112">ASP.NET MVC 1.0와 ASP.NET MVC 2에 대 한 기본 AccountController에에서 사용 되는 로그인은 열 리디렉션 공격에 취약 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-112">The login used in the default AccountController for both ASP.NET MVC 1.0 and ASP.NET MVC 2 is vulnerable to open redirection attacks.</span></span> <span data-ttu-id="3b600-113">다행히 ASP.NET MVC 3 Preview의 수정 사항이 사용 하 여 기존 응용 프로그램을 업데이트 하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-113">Fortunately, it is easy to update your existing applications to use the corrections from the ASP.NET MVC 3 Preview.</span></span>

<span data-ttu-id="3b600-114">이 취약점을 이해 하려면 살펴보겠습니다 로그인 리디렉션 기본 ASP.NET MVC 2 웹 응용 프로그램 프로젝트에서 작동 하는 방식.</span><span class="sxs-lookup"><span data-stu-id="3b600-114">To understand the vulnerability, let's look at how the login redirection works in a default ASP.NET MVC 2 Web Application project.</span></span> <span data-ttu-id="3b600-115">이 응용 프로그램에서 [Authorize] 특성이 있는 컨트롤러 작업을 방문 하는 권한이 없는 사용자를를 리디렉션합니다 /Account/LogOn 보기.</span><span class="sxs-lookup"><span data-stu-id="3b600-115">In this application, attempting to visit a controller action that has the [Authorize] attribute will redirect unauthorized users to the /Account/LogOn view.</span></span> <span data-ttu-id="3b600-116">/Account/LogOn이 이동이 성공적으로 로그인 한 후 원래 요청 된 URL로 사용자를 반환 수 있도록 returnUrl querystring 매개 변수를 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-116">This redirect to /Account/LogOn will include a returnUrl querystring parameter so that the user can be returned to the originally requested URL after they have successfully logged in.</span></span>

<span data-ttu-id="3b600-117">아래 스크린샷에서 /Account/LogOn을 리디렉션에 로그인 하지 않은 경우 /Account/ChangePassword 보기에 액세스 하려고 발생 알 수 있습니다. ReturnUrl = %2fAccount 2fChangePassword% 2f%입니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-117">In the screenshot below, we can see that an attempt to access the /Account/ChangePassword view when not logged in results in a redirect to /Account/LogOn?ReturnUrl=%2fAccount%2fChangePassword%2f.</span></span>

[![](preventing-open-redirection-attacks/_static/image2.png)](preventing-open-redirection-attacks/_static/image1.png)

<span data-ttu-id="3b600-118">**그림 01**: 열려 리디렉션을 로그인 페이지</span><span class="sxs-lookup"><span data-stu-id="3b600-118">**Figure 01**: Login page with an open redirection</span></span>

<span data-ttu-id="3b600-119">이후 ReturnUrl querystring 매개 변수 유효성이 검사 되지 않습니다 하면 공격자가 열려 리디렉션 공격을 수행 하 고 매개 변수를 모든 URL 주소를 삽입 하도록 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-119">Since the ReturnUrl querystring parameter is not validated, an attacker can modify it to inject any URL address into the parameter to conduct an open redirection attack.</span></span> <span data-ttu-id="3b600-120">이 증명 하려면 ReturnUrl 매개 변수를 수정할 수 있을 [ http://bing.com ](http://bing.com)결과 로그인 URL을 갖게 됩니다/계정/로그온? ReturnUrl =<http://www.bing.com/>합니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-120">To demonstrate this, we can modify the ReturnUrl parameter to [http://bing.com](http://bing.com), so the resulting login URL will be /Account/LogOn?ReturnUrl=<http://www.bing.com/>.</span></span> <span data-ttu-id="3b600-121">성공적으로 사이트에 로그인 하 되 면 우리는 리디렉션됩니다 [ http://bing.com ](http://bing.com)합니다. 이후이 리디렉션이 유효성이 검사 되지 않습니다 대신 사용자 속일 하려는 악성 사이트를 가리킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-121">Upon successfully logging in to the site, we are redirected to [http://bing.com](http://bing.com). Since this redirection is not validated, it could instead point to a malicious site that attempts to trick the user.</span></span>

### <a name="a-more-complex-open-redirection-attack"></a><span data-ttu-id="3b600-122">더 복잡 한 열기 리디렉션 공격</span><span class="sxs-lookup"><span data-stu-id="3b600-122">A more complex Open Redirection Attack</span></span>

<span data-ttu-id="3b600-123">열기 리디렉션 공격은 특히 위험에 취약해 우리 특정 웹 사이트에 로그인 하려고 하는 공격자가 알기 때문에 [피싱 공격](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-123">Open redirection attacks are especially dangerous because an attacker knows that we're trying to log into a specific website, which makes us vulnerable to a [phishing attack](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx).</span></span> <span data-ttu-id="3b600-124">예를 들어 공격자가 암호를 캡처할 하기 위해 웹 사이트 사용자에 게 악성 전자 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-124">For example, an attacker could send malicious emails to website users in an attempt to capture their passwords.</span></span> <span data-ttu-id="3b600-125">업그레이드 되었으며 수정 사이트에서 어떻게 작동할 것에서 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-125">Let's look at how this would work on the NerdDinner site.</span></span> <span data-ttu-id="3b600-126">(Note: 라이브 업그레이드 되었으며 수정 사이트가 열려 리디렉션 공격 으로부터 보호 하도록 업데이트 되었습니다.)</span><span class="sxs-lookup"><span data-stu-id="3b600-126">(Note that the live NerdDinner site has been updated to protect against open redirection attacks.)</span></span>

<span data-ttu-id="3b600-127">첫째, 공격자가 보내는 링크 로그인 페이지 리디렉션을 위조 된 페이지를 포함 하는 업그레이드 되었으며 수정에:</span><span class="sxs-lookup"><span data-stu-id="3b600-127">First, an attacker sends us a link to the login page on NerdDinner that includes a redirect to their forged page:</span></span>

[http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn](http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn)

<span data-ttu-id="3b600-128">Note 반환 URL 단어 dinner에서 "n" 없는 nerddiner.com 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-128">Note that the return URL points to nerddiner.com, which is missing an "n" from the word dinner.</span></span> <span data-ttu-id="3b600-129">이 예제에서는 공격자가 제어 하는 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-129">In this example, this is a domain that the attacker controls.</span></span> <span data-ttu-id="3b600-130">위의 링크에 액세스 했습니다 합법적인 NerdDinner.com 로그인 페이지로 이동 하 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-130">When we access the above link, we're taken to the legitimate NerdDinner.com login page.</span></span>

[![](preventing-open-redirection-attacks/_static/image4.png)](preventing-open-redirection-attacks/_static/image3.png)

<span data-ttu-id="3b600-131">**그림 02**: 열려 리디렉션을 업그레이드 되었으며 수정 로그인 페이지</span><span class="sxs-lookup"><span data-stu-id="3b600-131">**Figure 02**: NerdDinner login page with an open redirection</span></span>

<span data-ttu-id="3b600-132">ASP.NET MVC AccountController 로그온 작업을 올바르게에 로그인 하겠습니다 returnUrl querystring 매개 변수에서 지정 된 URL로 우리 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-132">When we correctly log in, the ASP.NET MVC AccountController's LogOn action redirects us to the URL specified in the returnUrl querystring parameter.</span></span> <span data-ttu-id="3b600-133">이 경우에 공격자가 입력 한 URL을는 [ http://nerddiner.com/Account/LogOn ](http://nerddiner.com/Account/LogOn)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-133">In this case, it's the URL that the attacker has entered, which is [http://nerddiner.com/Account/LogOn](http://nerddiner.com/Account/LogOn).</span></span> <span data-ttu-id="3b600-134">We're 매우 워치 매우 높습니다이 알 수 없습니다 공격자가 있는지 확인 하려면 신중 하 게 되지 않았기 때문에 특히 하지 않는 한 해당 위조 된 페이지 합법적인 로그인 페이지와 동일 하 게 보입니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-134">Unless we're extremely watchful, it's very likely we won't notice this, especially because the attacker has been careful to make sure that their forged page looks exactly like the legitimate login page.</span></span> <span data-ttu-id="3b600-135">이 로그인 페이지에 다시 로그인 하는 오류 메시지 요청에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-135">This login page includes an error message requesting that we login again.</span></span> <span data-ttu-id="3b600-136">어 색 하 게 us, 암호를 입력 했 해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-136">Clumsy us, we must have mistyped our password.</span></span>

[![](preventing-open-redirection-attacks/_static/image6.png)](preventing-open-redirection-attacks/_static/image5.png)

<span data-ttu-id="3b600-137">**그림 03**: 위조 업그레이드 되었으며 수정 로그인 화면</span><span class="sxs-lookup"><span data-stu-id="3b600-137">**Figure 03**: Forged NerdDinner Login screen</span></span>

<span data-ttu-id="3b600-138">에서는 사용자 이름과 암호를 다시 입력, 위조 된 로그인 페이지 정보를 저장 하 고 합법적인 NerdDinner.com 사이트에 다시 보내는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-138">When we retype our user name and password, the forged login page saves the information and sends us back to the legitimate NerdDinner.com site.</span></span> <span data-ttu-id="3b600-139">이 시점에서 NerdDinner.com 사이트가 이미 인증 us, 위조 된 로그인 페이지는 해당 페이지에 직접 리디렉션할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-139">At this point, the NerdDinner.com site has already authenticated us, so the forged login page can redirect directly to that page.</span></span> <span data-ttu-id="3b600-140">최종 결과는 공격자가 사용자 이름과 암호를 및 하 나와 것을 알지는입니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-140">The end result is that the attacker has our user name and password, and we are unaware that we've provided it to them.</span></span>

## <a name="looking-at-the-vulnerable-code-in-the-accountcontroller-logon-action"></a><span data-ttu-id="3b600-141">AccountController 로그온 액션에 취약 한 코드를 살펴보면</span><span class="sxs-lookup"><span data-stu-id="3b600-141">Looking at the vulnerable code in the AccountController LogOn Action</span></span>

<span data-ttu-id="3b600-142">ASP.NET MVC 2 응용 프로그램에서 로그온 작업에 대 한 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-142">The code for the LogOn action in an ASP.NET MVC 2 application is shown below.</span></span> <span data-ttu-id="3b600-143">성공적으로 로그인 할 때 컨트롤러 돌아갑니다 리디렉션을 returnUrl 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-143">Note that upon a successful login, the controller returns a redirect to the returnUrl.</span></span> <span data-ttu-id="3b600-144">유효성 검사가 수행 되지 returnUrl 매개 변수에 대해 수행 되 고 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-144">You can see that no validation is being performed against the returnUrl parameter.</span></span>

<span data-ttu-id="3b600-145">**1 –에서 ASP.NET MVC 2 로그온 작업 나열 `AccountController.cs`**</span><span class="sxs-lookup"><span data-stu-id="3b600-145">**Listing 1 – ASP.NET MVC 2 LogOn action in `AccountController.cs`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample1.cs)]

<span data-ttu-id="3b600-146">이제 ASP.NET MVC 3 로그온 동작의 변경 내용을 살펴 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-146">Now let's look at the changes to the ASP.NET MVC 3 LogOn action.</span></span> <span data-ttu-id="3b600-147">이 코드는 returnUrl 매개 변수 이름의 System.Web.Mvc.Url 도우미 클래스의 새 메서드를 호출 하 여 유효성을 검사 하도록 변경 되었습니다 `IsLocalUrl()`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-147">This code has been changed to validate the returnUrl parameter by calling a new method in the System.Web.Mvc.Url helper class named `IsLocalUrl()`.</span></span>

<span data-ttu-id="3b600-148">**2 –에서 ASP.NET MVC 3 로그온 작업 나열 `AccountController.cs`**</span><span class="sxs-lookup"><span data-stu-id="3b600-148">**Listing 2 – ASP.NET MVC 3 LogOn action in `AccountController.cs`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample2.cs)]

<span data-ttu-id="3b600-149">반환 URL 매개 변수 System.Web.Mvc.Url 도우미 클래스의 새 메서드를 호출 하 여 유효성을 검사 하도록 변경 되었습니다이 `IsLocalUrl()`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-149">This has been changed to validate the return URL parameter by calling a new method in the System.Web.Mvc.Url helper class, `IsLocalUrl()`.</span></span>

## <a name="protecting-your-aspnet-mvc-10-and-mvc-2-applications"></a><span data-ttu-id="3b600-150">ASP.NET MVC 1.0 및 MVC 2 보호 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="3b600-150">Protecting Your ASP.NET MVC 1.0 and MVC 2 Applications</span></span>

<span data-ttu-id="3b600-151">IsLocalUrl() 도우미 메서드를 추가 하 고 returnUrl 매개 변수 유효성을 검사 하는 로그온 동작을 업데이트 하 여 기존 ASP.NET MVC 1.0 우리의 및 2 응용 프로그램에서 ASP.NET MVC 3 변경 내용 활용을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-151">We can take advantage of the ASP.NET MVC 3 changes in our existing ASP.NET MVC 1.0 and 2 applications by adding the IsLocalUrl() helper method and updating the LogOn action to validate the returnUrl parameter.</span></span>

<span data-ttu-id="3b600-152">ASP.NET 웹 페이지 응용 프로그램에서 실제로 호출에서이 유효성 검사와 System.Web.WebPages 메서드로 UrlHelper IsLocalUrl() 메서드도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-152">The UrlHelper IsLocalUrl() method actually just calling into a method in System.Web.WebPages, as this validation is also used by ASP.NET Web Pages applications.</span></span>

<span data-ttu-id="3b600-153">**3 – ASP.NET MVC 3 UrlHelper에서 IsLocalUrl() 메서드를 나열합니다. `class`**</span><span class="sxs-lookup"><span data-stu-id="3b600-153">**Listing 3 – The IsLocalUrl() method from the ASP.NET MVC 3 UrlHelper `class`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample3.cs)]

<span data-ttu-id="3b600-154">IsUrlLocalToHost 메서드 목록 4와 같이 실제 유효성 검사 논리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-154">The IsUrlLocalToHost method contains the actual validation logic, as shown in Listing 4.</span></span>

<span data-ttu-id="3b600-155">**4 – System.Web.WebPages RequestExtensions 클래스에서 IsUrlLocalToHost() 메서드를 나열합니다.**</span><span class="sxs-lookup"><span data-stu-id="3b600-155">**Listing 4 – IsUrlLocalToHost() method from the System.Web.WebPages RequestExtensions class**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample4.cs)]

<span data-ttu-id="3b600-156">ASP.NET MVC 1.0 우리의 또는 2 응용 프로그램에서 IsLocalUrl() 메서드는 AccountController를 추가 합니다 바꿔야 하는데이 가능 하다 면 별도 도우미 클래스에 추가 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-156">In our ASP.NET MVC 1.0 or 2 application, we'll add a IsLocalUrl() method to the AccountController, but you're encouraged to add it to a separate helper class if possible.</span></span> <span data-ttu-id="3b600-157">해 드립니다 두 약간 변경 IsLocalUrl()의 ASP.NET MVC 3 버전에는 AccountController 내 작동할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-157">We will make two small changes to the ASP.NET MVC 3 version of IsLocalUrl() so that it will work inside the AccountController.</span></span> <span data-ttu-id="3b600-158">먼저 변경 합니다 것 public 메서드에서 전용 메서드를 컨트롤러의 public 메서드를 컨트롤러 작업으로 액세스할 수 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-158">First, we'll change it from a public method to a private method, since public methods in controllers can be accessed as controller actions.</span></span> <span data-ttu-id="3b600-159">둘째, 응용 프로그램 호스트에 대해 URL 호스트를 확인 하는 호출이 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-159">Second, we'll modify the call that checks the URL host against the application host.</span></span> <span data-ttu-id="3b600-160">호출에서 로컬 RequestContext를 활용 필드 UrlHelper 클래스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-160">That call makes use of a local RequestContext field in the UrlHelper class.</span></span> <span data-ttu-id="3b600-161">대신이 사용 합니다. RequestContext.HttpContext.Request.Url.Host,이 사용 합니다 했습니다. Request.Url.Host 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-161">Instead of using this.RequestContext.HttpContext.Request.Url.Host, we will use this.Request.Url.Host.</span></span> <span data-ttu-id="3b600-162">다음 코드는 ASP.NET MVC 1.0 및 2 응용 프로그램 컨트롤러 클래스와 함께 사용 하기 위해 수정 된 IsLocalUrl() 메서드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-162">The following code shows the modified IsLocalUrl() method for use with a controller class in ASP.NET MVC 1.0 and 2 applications.</span></span>

<span data-ttu-id="3b600-163">**MVC 컨트롤러 클래스에 수정 될 목록 5 – IsLocalUrl() 메서드**</span><span class="sxs-lookup"><span data-stu-id="3b600-163">**Listing 5 – IsLocalUrl() method, which is modified for use with an MVC Controller class**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample5.cs)]

<span data-ttu-id="3b600-164">IsLocalUrl() 메서드 이면 했으므로 다음 코드에 나와 있는 것 처럼 returnUrl 매개 변수 유효성을 검사 하 여 로그온 작업에서 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-164">Now that the IsLocalUrl() method is in place, we can call it from our LogOn action to validate the returnUrl parameter, as shown in the following code.</span></span>

<span data-ttu-id="3b600-165">**6-업데이트 된 로그온 방법 returnUrl 매개 변수를의 유효성을 검사 목록**</span><span class="sxs-lookup"><span data-stu-id="3b600-165">**Listing 6 – Updated LogOn method which validates the returnUrl parameter**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample6.cs)]

<span data-ttu-id="3b600-166">이제 열려 리디렉션 공격 외부 반환 URL을 사용 하 여 로그인을 시도 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-166">Now we can test an open redirection attack by attempting to log in using an external return URL.</span></span> <span data-ttu-id="3b600-167">/Account/LogOn 사용? ReturnUrl =<http://www.bing.com/> 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-167">Let's use /Account/LogOn?ReturnUrl=<http://www.bing.com/> again.</span></span>

[![](preventing-open-redirection-attacks/_static/image8.png)](preventing-open-redirection-attacks/_static/image7.png)

<span data-ttu-id="3b600-168">**그림 04**: 업데이트 된 로그온 동작을 테스트</span><span class="sxs-lookup"><span data-stu-id="3b600-168">**Figure 04**: Testing the updated LogOn Action</span></span>

<span data-ttu-id="3b600-169">성공적으로 로그인 한 후에 외부 URL이 아닌 Home/Index 컨트롤러 동작 리디렉션됩니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-169">After successfully logging in, we are redirected to the Home/Index Controller action rather than the external URL.</span></span>

[![](preventing-open-redirection-attacks/_static/image10.png)](preventing-open-redirection-attacks/_static/image9.png)

<span data-ttu-id="3b600-170">**그림 05**: 열기 리디렉션 공격을 막을 수</span><span class="sxs-lookup"><span data-stu-id="3b600-170">**Figure 05**: Open Redirection attack defeated</span></span>

## <a name="summary"></a><span data-ttu-id="3b600-171">요약</span><span class="sxs-lookup"><span data-stu-id="3b600-171">Summary</span></span>

<span data-ttu-id="3b600-172">열기 리디렉션 공격 리디렉션 Url은 응용 프로그램에 대 한 URL에 매개 변수로 전달 될 때 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-172">Open redirection attacks can occur when redirection URLs are passed as parameters in the URL for an application.</span></span> <span data-ttu-id="3b600-173">리디렉션 공격 으로부터 보호 하기 위해 코드를 포함 하는 서식 파일은 ASP.NET MVC 3을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-173">The ASP.NET MVC 3 template includes code to protect against open redirection attacks.</span></span> <span data-ttu-id="3b600-174">일부 수정 하지 않고도 ASP.NET MVC 1.0 및 2 응용 프로그램에이 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b600-174">You can add this code with some modification to ASP.NET MVC 1.0 and 2 applications.</span></span> <span data-ttu-id="3b600-175">ASP.NET 1.0 및 2 응용 프로그램에 로그인 할 때 열린 리디렉션 공격을 방지 하기 위해 IsLocalUrl() 메서드를 추가 하 고 로그온 동작에서 returnUrl 매개 변수 유효성 검사.</span><span class="sxs-lookup"><span data-stu-id="3b600-175">To protect against open redirection attacks when logging into ASP.NET 1.0 and 2 applications, add a IsLocalUrl() method and validate the returnUrl parameter in the LogOn action.</span></span>
