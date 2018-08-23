---
uid: mvc/overview/security/preventing-open-redirection-attacks
title: 오픈 리디렉션 공격 방지 (C#) | Microsoft Docs
author: jongalloway
description: 이 자습서에서는 ASP.NET MVC 응용 프로그램에서 오픈 리디렉션 공격을 방지 하는 방법에 대해 설명 합니다. 이 자습서에는 적용 된 변경 내용을 설명 하는 중...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 69fb02e0-f5b7-4c35-878c-fa87164fc785
msc.legacyurl: /mvc/overview/security/preventing-open-redirection-attacks
msc.type: authoredcontent
ms.openlocfilehash: 767f9c85527fbcdf34e700eb32fe0c6cad30bf0c
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41835470"
---
<a name="preventing-open-redirection-attacks-c"></a><span data-ttu-id="43b7e-104">오픈 리디렉션 공격 방지 (C#)</span><span class="sxs-lookup"><span data-stu-id="43b7e-104">Preventing Open Redirection Attacks (C#)</span></span>
====================
<span data-ttu-id="43b7e-105">[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="43b7e-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="43b7e-106">이 자습서에서는 ASP.NET MVC 응용 프로그램에서 오픈 리디렉션 공격을 방지 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-106">This tutorial explains how you can prevent open redirection attacks in your ASP.NET MVC applications.</span></span> <span data-ttu-id="43b7e-107">이 자습서는 ASP.NET MVC 3에서 AccountController에 적용 된 변경 내용을 설명 하 고에 기존 ASP.NET MVC 1.0 및 2 응용 프로그램에서 이러한 변경 내용을 적용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-107">This tutorial discusses the changes that have been made in the AccountController in ASP.NET MVC 3 and demonstrates how you can apply these changes in your existing ASP.NET MVC 1.0 and 2 applications.</span></span>


## <a name="what-is-an-open-redirection-attack"></a><span data-ttu-id="43b7e-108">오픈 리디렉션 공격 란?</span><span class="sxs-lookup"><span data-stu-id="43b7e-108">What is an Open Redirection Attack?</span></span>

<span data-ttu-id="43b7e-109">잠재적으로 쿼리 문자열 또는 폼 데이터와 같은 요청을 통해 지정 된 URL로 리디렉션하는 모든 웹 응용 프로그램 외부, 악성 URL에 사용자를 리디렉션할 사용 하 여 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-109">Any web application that redirects to a URL that is specified via the request such as the querystring or form data can potentially be tampered with to redirect users to an external, malicious URL.</span></span> <span data-ttu-id="43b7e-110">이 변조 오픈 리디렉션 공격을 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-110">This tampering is called an open redirection attack.</span></span>

<span data-ttu-id="43b7e-111">때마다 응용 프로그램 논리를 지정 된 URL로 리디렉션되면 리디렉션 URL을 사용 하 여 손상 되지 않았는지를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-111">Whenever your application logic redirects to a specified URL, you must verify that the redirection URL hasn't been tampered with.</span></span> <span data-ttu-id="43b7e-112">ASP.NET MVC 1.0 및 ASP.NET MVC 2 모두에 대 한 기본 AccountController에에서 사용 된 로그인은 엽니다 리디렉션 공격에 취약 합니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-112">The login used in the default AccountController for both ASP.NET MVC 1.0 and ASP.NET MVC 2 is vulnerable to open redirection attacks.</span></span> <span data-ttu-id="43b7e-113">다행 스럽게도 ASP.NET MVC 3 미리 보기에서 수정 사항을 사용 하려면 기존 응용 프로그램을 업데이트 하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-113">Fortunately, it is easy to update your existing applications to use the corrections from the ASP.NET MVC 3 Preview.</span></span>

<span data-ttu-id="43b7e-114">취약성을 이해 하려면 살펴보겠습니다 로그인 리디렉션 기본 ASP.NET MVC 2 웹 응용 프로그램 프로젝트에서 작동 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="43b7e-114">To understand the vulnerability, let's look at how the login redirection works in a default ASP.NET MVC 2 Web Application project.</span></span> <span data-ttu-id="43b7e-115">이 응용 프로그램에서 [Authorize] 특성을 갖는 컨트롤러 작업을 방문 하는 동안 권한이 없는 사용자로 리디렉션됩니다 /Account/LogOn 보기.</span><span class="sxs-lookup"><span data-stu-id="43b7e-115">In this application, attempting to visit a controller action that has the [Authorize] attribute will redirect unauthorized users to the /Account/LogOn view.</span></span> <span data-ttu-id="43b7e-116">/Account/LogOn이 이동이 성공적으로 로그인 한 후 원래 요청 된 URL에 사용자를 반환 될 수 있도록 returnUrl 쿼리 문자열 매개 변수가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-116">This redirect to /Account/LogOn will include a returnUrl querystring parameter so that the user can be returned to the originally requested URL after they have successfully logged in.</span></span>

<span data-ttu-id="43b7e-117">아래 스크린샷에서 /Account/LogOn을 로그인 하지 않은 경우 /Account/ChangePassword 뷰에 액세스 하려고 하면 리디렉션에 발생는 알 수 있습니다? ReturnUrl = %2fAccount %2fChangePassword %2f입니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-117">In the screenshot below, we can see that an attempt to access the /Account/ChangePassword view when not logged in results in a redirect to /Account/LogOn?ReturnUrl=%2fAccount%2fChangePassword%2f.</span></span>

[![](preventing-open-redirection-attacks/_static/image2.png)](preventing-open-redirection-attacks/_static/image1.png)

<span data-ttu-id="43b7e-118">**그림 01**:는 열린 리디렉션 사용 하 여 로그인 페이지</span><span class="sxs-lookup"><span data-stu-id="43b7e-118">**Figure 01**: Login page with an open redirection</span></span>

<span data-ttu-id="43b7e-119">ReturnUrl 쿼리 문자열 매개 변수는 유효성이 검사 되지 때문 공격자 오픈 리디렉션 공격을 수행 하는 매개 변수에 모든 URL 주소를 삽입할 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-119">Since the ReturnUrl querystring parameter is not validated, an attacker can modify it to inject any URL address into the parameter to conduct an open redirection attack.</span></span> <span data-ttu-id="43b7e-120">이 보여 주기 위해 ReturnUrl 매개 변수를 수정할 수 있습니다 [ http://bing.com ](http://bing.com)이므로 결과 로그인 URL은 / 계정/로그온? ReturnUrl =<http://www.bing.com/>합니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-120">To demonstrate this, we can modify the ReturnUrl parameter to [http://bing.com](http://bing.com), so the resulting login URL will be /Account/LogOn?ReturnUrl=<http://www.bing.com/>.</span></span> <span data-ttu-id="43b7e-121">성공적으로 사이트에 로그인 시에서는 리디렉션됩니다 [ http://bing.com ](http://bing.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-121">Upon successfully logging in to the site, we are redirected to [http://bing.com](http://bing.com).</span></span> <span data-ttu-id="43b7e-122">이 리디렉션은 유효성이 검사 되지 않습니다 하므로 사용자를 시도 하는 악성 사이트를 대신 가리킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-122">Since this redirection is not validated, it could instead point to a malicious site that attempts to trick the user.</span></span>

### <a name="a-more-complex-open-redirection-attack"></a><span data-ttu-id="43b7e-123">더 복잡 한 오픈 리디렉션 공격</span><span class="sxs-lookup"><span data-stu-id="43b7e-123">A more complex Open Redirection Attack</span></span>

<span data-ttu-id="43b7e-124">오픈 리디렉션 공격은 취약 하 게 특정 웹 사이트에 로그인 하려고 하는 공격자가 알고 있기 때문에 특히 위험을 [피싱 공격](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-124">Open redirection attacks are especially dangerous because an attacker knows that we're trying to log into a specific website, which makes us vulnerable to a [phishing attack](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx).</span></span> <span data-ttu-id="43b7e-125">예를 들어 공격자가 암호를 캡처할 하려고 웹 사이트 사용자에 게 악성 전자 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-125">For example, an attacker could send malicious emails to website users in an attempt to capture their passwords.</span></span> <span data-ttu-id="43b7e-126">NerdDinner 사이트의 작동 원리에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-126">Let's look at how this would work on the NerdDinner site.</span></span> <span data-ttu-id="43b7e-127">(Note: 오픈 리디렉션 공격 으로부터 보호 하기 위해 라이브 NerdDinner 사이트 변경 되었습니다.)</span><span class="sxs-lookup"><span data-stu-id="43b7e-127">(Note that the live NerdDinner site has been updated to protect against open redirection attacks.)</span></span>

<span data-ttu-id="43b7e-128">첫째, 공격자 우리 링크를 보내는 NerdDinner가 위조 된 페이지로 리디렉션을 포함 하는 로그인 페이지:</span><span class="sxs-lookup"><span data-stu-id="43b7e-128">First, an attacker sends us a link to the login page on NerdDinner that includes a redirect to their forged page:</span></span>

[http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn](http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn)

<span data-ttu-id="43b7e-129">반환 URL을 가리키는 nerddiner.com "n" 없는 단어 dinner에서 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-129">Note that the return URL points to nerddiner.com, which is missing an "n" from the word dinner.</span></span> <span data-ttu-id="43b7e-130">이 예에서이 공격자가 제어 하는 도메인.</span><span class="sxs-lookup"><span data-stu-id="43b7e-130">In this example, this is a domain that the attacker controls.</span></span> <span data-ttu-id="43b7e-131">위의 링크에 액세스 하는 경우 합법적인 NerdDinner.com 로그인 페이지로 이동 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-131">When we access the above link, we're taken to the legitimate NerdDinner.com login page.</span></span>

[![](preventing-open-redirection-attacks/_static/image4.png)](preventing-open-redirection-attacks/_static/image3.png)

<span data-ttu-id="43b7e-132">**그림 02**:는 오픈 리디렉션으로 NerdDinner 로그인 페이지</span><span class="sxs-lookup"><span data-stu-id="43b7e-132">**Figure 02**: NerdDinner login page with an open redirection</span></span>

<span data-ttu-id="43b7e-133">제대로 로그인에서는 ASP.NET MVC AccountController 로그온 작업 returnUrl 쿼리 문자열 매개 변수에서 지정한 URL에 우리를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-133">When we correctly log in, the ASP.NET MVC AccountController's LogOn action redirects us to the URL specified in the returnUrl querystring parameter.</span></span> <span data-ttu-id="43b7e-134">즉 공격자가 입력 하는 URL이이 예에서 [ http://nerddiner.com/Account/LogOn ](http://nerddiner.com/Account/LogOn)합니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-134">In this case, it's the URL that the attacker has entered, which is [http://nerddiner.com/Account/LogOn](http://nerddiner.com/Account/LogOn).</span></span> <span data-ttu-id="43b7e-135">우리는 매우 워치 가능성이 매우 높하지 않습니다 알 수 있습니다 따라서 공격자가 있는지 신중 하 게 되지 않았기 때문에 특히 하지 않는 한 해당 위조 된 페이지 합법적인 로그인 페이지와 동일 하 게 보입니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-135">Unless we're extremely watchful, it's very likely we won't notice this, especially because the attacker has been careful to make sure that their forged page looks exactly like the legitimate login page.</span></span> <span data-ttu-id="43b7e-136">이 로그인 페이지에서는 다시 로그인 요청 오류 메시지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-136">This login page includes an error message requesting that we login again.</span></span> <span data-ttu-id="43b7e-137">괴로운 us,에서는 암호를 잘못 입력 했 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-137">Clumsy us, we must have mistyped our password.</span></span>

[![](preventing-open-redirection-attacks/_static/image6.png)](preventing-open-redirection-attacks/_static/image5.png)

<span data-ttu-id="43b7e-138">**그림 03**: 위조 된 NerdDinner 로그인 화면</span><span class="sxs-lookup"><span data-stu-id="43b7e-138">**Figure 03**: Forged NerdDinner Login screen</span></span>

<span data-ttu-id="43b7e-139">에서는 사용자 이름 및 암호를 다시 입력, 하는 경우 위조 된 로그인 페이지 정보를 저장 하 고 합법적인 NerdDinner.com 사이트로 다시 우리를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-139">When we retype our user name and password, the forged login page saves the information and sends us back to the legitimate NerdDinner.com site.</span></span> <span data-ttu-id="43b7e-140">이 시점에서 NerdDinner.com 사이트에 이미 인증 us, 위조 된 로그인 페이지는 해당 페이지에 직접 리디렉션할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-140">At this point, the NerdDinner.com site has already authenticated us, so the forged login page can redirect directly to that page.</span></span> <span data-ttu-id="43b7e-141">최종 결과 사용자 이름 및 암호를 공격자가 하는 한 것에 인식 되지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-141">The end result is that the attacker has our user name and password, and we are unaware that we've provided it to them.</span></span>

## <a name="looking-at-the-vulnerable-code-in-the-accountcontroller-logon-action"></a><span data-ttu-id="43b7e-142">AccountController 로그온 동작에서 취약 한 코드를 살펴보면</span><span class="sxs-lookup"><span data-stu-id="43b7e-142">Looking at the vulnerable code in the AccountController LogOn Action</span></span>

<span data-ttu-id="43b7e-143">ASP.NET MVC 2 응용 프로그램에서 로그온 작업에 대 한 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-143">The code for the LogOn action in an ASP.NET MVC 2 application is shown below.</span></span> <span data-ttu-id="43b7e-144">로그인에 성공 하면 컨트롤러 돌아갑니다 리디렉션을 반환 된 Url을 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-144">Note that upon a successful login, the controller returns a redirect to the returnUrl.</span></span> <span data-ttu-id="43b7e-145">ReturnUrl 매개 변수에 대해 유효성을 검사 하지 수행될지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-145">You can see that no validation is being performed against the returnUrl parameter.</span></span>

<span data-ttu-id="43b7e-146">**목록 1 –에서 ASP.NET MVC 2 로그온 작업 `AccountController.cs`**</span><span class="sxs-lookup"><span data-stu-id="43b7e-146">**Listing 1 – ASP.NET MVC 2 LogOn action in `AccountController.cs`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample1.cs)]

<span data-ttu-id="43b7e-147">이제 ASP.NET MVC 3 로그온 동작 변경에 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-147">Now let's look at the changes to the ASP.NET MVC 3 LogOn action.</span></span> <span data-ttu-id="43b7e-148">이 코드 라는 System.Web.Mvc.Url 도우미 클래스의 새 메서드를 호출 하 여 returnUrl 매개 변수 유효성 검사로 변경 되었습니다 `IsLocalUrl()`합니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-148">This code has been changed to validate the returnUrl parameter by calling a new method in the System.Web.Mvc.Url helper class named `IsLocalUrl()`.</span></span>

<span data-ttu-id="43b7e-149">**2 –에서 ASP.NET MVC 3 로그온 작업 나열 `AccountController.cs`**</span><span class="sxs-lookup"><span data-stu-id="43b7e-149">**Listing 2 – ASP.NET MVC 3 LogOn action in `AccountController.cs`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample2.cs)]

<span data-ttu-id="43b7e-150">이 System.Web.Mvc.Url 도우미 클래스의 새 메서드를 호출 하 여 반환 URL 매개 변수 유효성 검사로 바뀌었습니다 `IsLocalUrl()`합니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-150">This has been changed to validate the return URL parameter by calling a new method in the System.Web.Mvc.Url helper class, `IsLocalUrl()`.</span></span>

## <a name="protecting-your-aspnet-mvc-10-and-mvc-2-applications"></a><span data-ttu-id="43b7e-151">및 보호 하 여 ASP.NET MVC 1.0 MVC 2 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="43b7e-151">Protecting Your ASP.NET MVC 1.0 and MVC 2 Applications</span></span>

<span data-ttu-id="43b7e-152">IsLocalUrl() 도우미 메서드를 추가 하 고 returnUrl 매개 변수 유효성을 검사 하려면 로그온 작업을 업데이트 하 여이 기존 ASP.NET MVC 1.0 및 2 응용 프로그램에서 ASP.NET MVC 3 변경 내용 활용을 걸릴 수 있습니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-152">We can take advantage of the ASP.NET MVC 3 changes in our existing ASP.NET MVC 1.0 and 2 applications by adding the IsLocalUrl() helper method and updating the LogOn action to validate the returnUrl parameter.</span></span>

<span data-ttu-id="43b7e-153">이 유효성 검사로 System.Web.WebPages 메서드가 실제로 호출 UrlHelper IsLocalUrl() 메서드도 ASP.NET Web Pages 응용 프로그램에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-153">The UrlHelper IsLocalUrl() method actually just calling into a method in System.Web.WebPages, as this validation is also used by ASP.NET Web Pages applications.</span></span>

<span data-ttu-id="43b7e-154">**3 – ASP.NET MVC 3 UrlHelper에서 IsLocalUrl() 메서드를 나열합니다. `class`**</span><span class="sxs-lookup"><span data-stu-id="43b7e-154">**Listing 3 – The IsLocalUrl() method from the ASP.NET MVC 3 UrlHelper `class`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample3.cs)]

<span data-ttu-id="43b7e-155">IsUrlLocalToHost 메서드 목록 4에 나와 있는 것 처럼 실제 유효성 검사 논리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-155">The IsUrlLocalToHost method contains the actual validation logic, as shown in Listing 4.</span></span>

<span data-ttu-id="43b7e-156">**4-IsUrlLocalToHost() 메서드에서 System.Web.WebPages RequestExtensions 클래스 나열**</span><span class="sxs-lookup"><span data-stu-id="43b7e-156">**Listing 4 – IsUrlLocalToHost() method from the System.Web.WebPages RequestExtensions class**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample4.cs)]

<span data-ttu-id="43b7e-157">ASP.NET MVC 1.0 또는 2 응용 프로그램에서 IsLocalUrl() 메서드는 AccountController를 추가한 않지만 가능 하면 별도 도우미 클래스를 추가 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-157">In our ASP.NET MVC 1.0 or 2 application, we'll add a IsLocalUrl() method to the AccountController, but you're encouraged to add it to a separate helper class if possible.</span></span> <span data-ttu-id="43b7e-158">AccountController 내에서 작동할 수 있도록 IsLocalUrl()의 ASP.NET MVC 3 버전 두 작은 변경을 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-158">We will make two small changes to the ASP.NET MVC 3 version of IsLocalUrl() so that it will work inside the AccountController.</span></span> <span data-ttu-id="43b7e-159">먼저에서는 변경 고 public 메서드에서 개인 메서드에 컨트롤러 작업으로 컨트롤러의 공용 메서드에 액세스할 수 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-159">First, we'll change it from a public method to a private method, since public methods in controllers can be accessed as controller actions.</span></span> <span data-ttu-id="43b7e-160">둘째, 응용 프로그램 호스트에 대 한 URL 호스트를 확인 하는 호출이 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-160">Second, we'll modify the call that checks the URL host against the application host.</span></span> <span data-ttu-id="43b7e-161">호출 로컬 RequestContext를 활용할 수 있도록 UrlHelper 클래스의 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-161">That call makes use of a local RequestContext field in the UrlHelper class.</span></span> <span data-ttu-id="43b7e-162">대신이 사용 합니다. RequestContext.HttpContext.Request.Url.Host,이 항목이 사용 됩니다. Request.Url.Host 합니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-162">Instead of using this.RequestContext.HttpContext.Request.Url.Host, we will use this.Request.Url.Host.</span></span> <span data-ttu-id="43b7e-163">다음 코드는 ASP.NET MVC 1.0 및 2 응용 프로그램 컨트롤러 클래스 사용에 대 한 수정 된 IsLocalUrl() 메서드를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-163">The following code shows the modified IsLocalUrl() method for use with a controller class in ASP.NET MVC 1.0 and 2 applications.</span></span>

<span data-ttu-id="43b7e-164">**5-IsLocalUrl() 메서드를 나열 하는 사용할 수 있도록 수정 하는 MVC 컨트롤러 클래스를 사용 하 여**</span><span class="sxs-lookup"><span data-stu-id="43b7e-164">**Listing 5 – IsLocalUrl() method, which is modified for use with an MVC Controller class**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample5.cs)]

<span data-ttu-id="43b7e-165">IsLocalUrl() 메서드 내부에는 이제 다음 코드 에서처럼 returnUrl 매개 변수 유효성을 검사 하 여 로그온 작업에서 호출할 수 했습니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-165">Now that the IsLocalUrl() method is in place, we can call it from our LogOn action to validate the returnUrl parameter, as shown in the following code.</span></span>

<span data-ttu-id="43b7e-166">**6-returnUrl 매개 변수 유효성을 검사 하는 업데이트 된 로그온 메서드를 나열 합니다.**</span><span class="sxs-lookup"><span data-stu-id="43b7e-166">**Listing 6 – Updated LogOn method which validates the returnUrl parameter**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample6.cs)]

<span data-ttu-id="43b7e-167">이제 오픈 리디렉션 공격 외부 반환 URL을 사용 하 여 로그인을 시도 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-167">Now we can test an open redirection attack by attempting to log in using an external return URL.</span></span> <span data-ttu-id="43b7e-168">/Account/LogOn 사용해 보겠습니다. ReturnUrl =<http://www.bing.com/> 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-168">Let's use /Account/LogOn?ReturnUrl=<http://www.bing.com/> again.</span></span>

[![](preventing-open-redirection-attacks/_static/image8.png)](preventing-open-redirection-attacks/_static/image7.png)

<span data-ttu-id="43b7e-169">**그림 04**: 업데이트 된 로그온 작업 테스트</span><span class="sxs-lookup"><span data-stu-id="43b7e-169">**Figure 04**: Testing the updated LogOn Action</span></span>

<span data-ttu-id="43b7e-170">성공적으로 로그인 한 후에 외부 URL이 아닌 Home/Index 컨트롤러 작업 리디렉션됩니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-170">After successfully logging in, we are redirected to the Home/Index Controller action rather than the external URL.</span></span>

[![](preventing-open-redirection-attacks/_static/image10.png)](preventing-open-redirection-attacks/_static/image9.png)

<span data-ttu-id="43b7e-171">**그림 05**: 패 오픈 리디렉션 공격</span><span class="sxs-lookup"><span data-stu-id="43b7e-171">**Figure 05**: Open Redirection attack defeated</span></span>

## <a name="summary"></a><span data-ttu-id="43b7e-172">요약</span><span class="sxs-lookup"><span data-stu-id="43b7e-172">Summary</span></span>

<span data-ttu-id="43b7e-173">오픈 리디렉션 공격 리디렉션 Url은 응용 프로그램에 대 한 URL에 매개 변수로 전달 될 때 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-173">Open redirection attacks can occur when redirection URLs are passed as parameters in the URL for an application.</span></span> <span data-ttu-id="43b7e-174">템플릿은 으로부터 보호 하기 위해 코드를 포함 하는 ASP.NET MVC 3 리디렉션 공격을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-174">The ASP.NET MVC 3 template includes code to protect against open redirection attacks.</span></span> <span data-ttu-id="43b7e-175">ASP.NET MVC 1.0 및 2 응용 프로그램에 일부 수정 하 여이 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-175">You can add this code with some modification to ASP.NET MVC 1.0 and 2 applications.</span></span> <span data-ttu-id="43b7e-176">ASP.NET 1.0 및 2 응용 프로그램에 로그인 할 때 오픈 리디렉션 공격을 방지 하기 IsLocalUrl() 메서드를 추가 하 고 로그온 작업 returnUrl 매개 변수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="43b7e-176">To protect against open redirection attacks when logging into ASP.NET 1.0 and 2 applications, add a IsLocalUrl() method and validate the returnUrl parameter in the LogOn action.</span></span>
