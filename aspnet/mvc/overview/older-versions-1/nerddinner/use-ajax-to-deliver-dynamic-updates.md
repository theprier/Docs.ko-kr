---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: AJAX를 사용 하 여 동적 업데이트를 제공 하도록 | Microsoft Docs
author: microsoft
description: 10 단계 구현 dinner 세부 정보에 통합 하는 Ajax 기반 접근 방식을 사용 하는 dinner 참석 사람들이 관심 RSVP에 로그인 한 사용자에 대 한 지원...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: e902881d3dab6a902cb747a197a32f317d199723
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41827139"
---
<a name="use-ajax-to-deliver-dynamic-updates"></a><span data-ttu-id="07eb4-103">AJAX를 사용 하 여 동적 업데이트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-103">Use AJAX to Deliver Dynamic Updates</span></span>
====================
<span data-ttu-id="07eb4-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="07eb4-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="07eb4-105">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="07eb4-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="07eb4-106">이 무료의 10 단계인 ["NerdDinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 는 안내를 통한 작은 빌드 하지만 ASP.NET MVC 1을 사용 하 여 웹 응용 프로그램을 완료 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-106">This is step 10 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="07eb4-107">10 단계 구현 dinner 세부 정보 페이지에 통합 하는 Ajax 기반 접근 방식을 사용 하는 dinner 참석 사람들이 관심 RSVP에 로그인 한 사용자에 대 한 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-107">Step 10 implements support for logged-in users to RSVP their interest in attending a dinner, using an Ajax-based approach integrated within the dinner details page.</span></span>
> 
> <span data-ttu-id="07eb4-108">ASP.NET MVC 3을 사용 하는 경우 수행 하는 것이 좋습니다 합니다 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 하거나 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a><span data-ttu-id="07eb4-109">NerdDinner 10 단계: 않으십니까를 사용 하도록 설정 하는 AJAX 허용</span><span class="sxs-lookup"><span data-stu-id="07eb4-109">NerdDinner Step 10: AJAX Enabling RSVPs Accepts</span></span>

<span data-ttu-id="07eb4-110">이제 로그인 한 사용자의를 저녁 식사에 참석 사람들이 관심을 회신에 대 한 지원을 구현 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-110">Let's now implement support for logged-in users to RSVP their interest in attending a dinner.</span></span> <span data-ttu-id="07eb4-111">지원할 예정이 dinner 세부 정보 페이지 내에서 통합 된 AJAX 기반 접근 방식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-111">We'll enable this using an AJAX-based approach integrated within the dinner details page.</span></span>

### <a name="indicating-whether-the-user-is-rsvpd"></a><span data-ttu-id="07eb4-112">사용자가 주최 하는 여부를 나타내는</span><span class="sxs-lookup"><span data-stu-id="07eb4-112">Indicating whether the user is RSVP'd</span></span>

<span data-ttu-id="07eb4-113">사용자가 방문할 수는 */Dinners 세부 정보 / [id*] 특정 저녁에 대 한 세부 정보를 보려면 URL:</span><span class="sxs-lookup"><span data-stu-id="07eb4-113">Users can visit the */Dinners/Details/[id*] URL to see details about a particular dinner:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

<span data-ttu-id="07eb4-114">작업 메서드는 구현 Details() 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-114">The Details() action method is implemented like so:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

<span data-ttu-id="07eb4-115">RSVP 지원을 구현 하기 위해 첫 번째 단계 (내에서 앞서 작성 Dinner.cs 부분 클래스)은 Dinner 개체 "IsUserRegistered(username)" 도우미 메서드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-115">Our first step to implement RSVP support will be to add an "IsUserRegistered(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="07eb4-116">이 도우미 메서드는 Dinner에 대 한 현재 주최 하는 사용자 여부에 따라 true 또는 false를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-116">This helper method returns true or false depending on whether the user is currently RSVP'd for the Dinner:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

<span data-ttu-id="07eb4-117">다음 이벤트 또는 하지 Details.aspx 보기 템플릿은 사용자가 등록 되어 있는지 여부를 나타내는 적절 한 메시지를 표시 하려면 다음 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-117">We can then add the following code to our Details.aspx view template to display an appropriate message indicating whether the user is registered or not for the event:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

<span data-ttu-id="07eb4-118">고 이제 사용자에 대 한 등록 하는 Dinner 방문이 메시지 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-118">And now when a user visits a Dinner they are registered for they'll see this message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

<span data-ttu-id="07eb4-119">표시에 대 한 등록 하지는 저녁 식사를 방문할 때와 메시지 아래:</span><span class="sxs-lookup"><span data-stu-id="07eb4-119">And when they visit a Dinner they are not registered for they'll see the below message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a><span data-ttu-id="07eb4-120">Register 작업 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-120">Implementing the Register Action Method</span></span>

<span data-ttu-id="07eb4-121">세부 정보 페이지에서 사용자는 저녁에 RSVP를 사용 하는 데 필요한 기능을 이제 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-121">Let's now add the functionality necessary to enable users to RSVP for a dinner from the details page.</span></span>

<span data-ttu-id="07eb4-122">이 구현 하려면 만들겠습니다 새 "RSVPController" 클래스 \Controllers 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 추가-선택 하 여&gt;컨트롤러 메뉴 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-122">To implement this, we'll create a new "RSVPController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span>

<span data-ttu-id="07eb4-123">인수로 저녁에는 id를 가져오고, 확인 하 고 경우에 로그인 한 사용자를 등록 하는 사용자 목록에서 현재 경우 적절 한 Dinner 개체를 검색 하는 새 RSVPController 클래스 내에서 "등록" 작업 메서드를 구현 합니다. 에 RSVP 개체를 추가 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-123">We'll implement a "Register" action method within the new RSVPController class that takes an id for a Dinner as an argument, retrieves the appropriate Dinner object, checks to see if the logged-in user is currently in the list of users who have registered for it, and if not adds an RSVP object for them:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

<span data-ttu-id="07eb4-124">위의 간단한 문자열을 동작 메서드의 출력으로 반환 되는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-124">Notice above how we are returning a simple string as the output of the action method.</span></span> <span data-ttu-id="07eb4-125">이 메시지는 보기 템플릿 내의 포함 수 것 하지만 컨트롤러 기본 클래스에 위의 문자열 메시지와 같은 반환 Content() 도우미 메서드를 사용 작기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-125">We could have embedded this message within a view template – but since it is so small we'll just use the Content() helper method on the controller base class and return a string message like above.</span></span>

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a><span data-ttu-id="07eb4-126">AJAX를 사용 하 여 RSVPForEvent 작업 메서드를 호출</span><span class="sxs-lookup"><span data-stu-id="07eb4-126">Calling the RSVPForEvent Action Method using AJAX</span></span>

<span data-ttu-id="07eb4-127">AJAX 사용 하 여 세부 정보 보기에서 등록 동작 메서드를 호출 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-127">We'll use AJAX to invoke the Register action method from our Details view.</span></span> <span data-ttu-id="07eb4-128">이 구현 하는 것은 매우 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-128">Implementing this is pretty easy.</span></span> <span data-ttu-id="07eb4-129">먼저 두 개의 스크립트 라이브러리 참조 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-129">First we'll add two script library references:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

<span data-ttu-id="07eb4-130">핵심 ASP.NET AJAX 클라이언트 쪽 스크립트 라이브러리를 참조 하는 첫 번째 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-130">The first library references the core ASP.NET AJAX client-side script library.</span></span> <span data-ttu-id="07eb4-131">이 파일 (압축) 크기가 약 24 k 핵심 클라이언트 쪽 AJAX 기능이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-131">This file is approximately 24k in size (compressed) and contains core client-side AJAX functionality.</span></span> <span data-ttu-id="07eb4-132">두 번째 라이브러리에는 ASP.NET MVC의 기본 제공 AJAX 도우미 메서드 (곧 사용 하겠습니다)와 통합 되는 유틸리티 함수가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-132">The second library contains utility functions that integrate with ASP.NET MVC's built-in AJAX helper methods (which we'll use shortly).</span></span>

<span data-ttu-id="07eb4-133">RSVP 컨트롤러에서 우리의 RSVPForEvent 작업 메서드를 호출 하는 AJAX 호출을 수행 하는 발견 된 "등록 되지 않습니다이 이벤트에 대 한" 메시지를 대신에서는 대신 렌더링 되도록 링크는 푸시 될 때 이전에 추가한 보기 템플릿 코드를 업데이트 한 다음 수 있습니다. 및 사용자 RSVPs:</span><span class="sxs-lookup"><span data-stu-id="07eb4-133">We can then update the view template code we added earlier so that instead of outputing a "You are not registered for this event" message, we instead render a link that when pushed performs an AJAX call that invokes our RSVPForEvent action method on our RSVP controller and RSVPs the user:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

<span data-ttu-id="07eb4-134">위에서 사용한 Ajax.ActionLink() 도우미 메서드는 ASP.NET MVC에 기본 제공 이며는 Html.ActionLink() 도우미 메서드를 제외 하는 표준 탐색을 수행 하는 대신 있도록 동작 메서드에 대 한 AJAX 호출 링크를 클릭할 때입니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-134">The Ajax.ActionLink() helper method used above is built-into ASP.NET MVC and is similar to the Html.ActionLink() helper method except that instead of performing a standard navigation it makes an AJAX call to the action method when the link is clicked.</span></span> <span data-ttu-id="07eb4-135">위에서 "RSVP" 컨트롤러에서 "Register" 작업 메서드를 호출 하 고를 DinnerID "id" 매개 변수로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-135">Above we are calling the "Register" action method on the "RSVP" controller and passing the DinnerID as the "id" parameter to it.</span></span> <span data-ttu-id="07eb4-136">마지막 AjaxOptions 매개 변수 전달 한다는 동작 메서드에서 반환 된 콘텐츠를 가져와서 HTML을 업데이트 하 &lt;div&gt; id가 "rsvpmsg" 페이지의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-136">The final AjaxOptions parameter we are passing indicates that we want to take the content returned from the action method and update the HTML &lt;div&gt; element on the page whose id is "rsvpmsg".</span></span>

<span data-ttu-id="07eb4-137">이며 하는 사용자가 탐색할 때에 등록 되지 않은 하 아직 링크에 대 한 RSVP 보게 이제:</span><span class="sxs-lookup"><span data-stu-id="07eb4-137">And now when a user browses to a dinner they aren't registered for yet they'll see a link to RSVP for it:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

<span data-ttu-id="07eb4-138">"이이 이벤트에 대 한 RSVP" 링크를 클릭 하는 경우 해당 등록 동작 메서드에 대 한 AJAX 호출 RSVP 컨트롤러에서 만들고 업데이트 된 메시지를 보게 완료 되 면 아래와 같은:</span><span class="sxs-lookup"><span data-stu-id="07eb4-138">If they click the "RSVP for this event" link they'll make an AJAX call to the Register action method on the RSVP controller, and when it completes they'll see an updated message like below:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

<span data-ttu-id="07eb4-139">네트워크 대역폭 및 트래픽이 AJAX 호출을 수행할 때 관련 된 매우 간단한 경우</span><span class="sxs-lookup"><span data-stu-id="07eb4-139">The network bandwidth and traffic involved when making this AJAX call is really lightweight.</span></span> <span data-ttu-id="07eb4-140">작은 HTTP POST 네트워크 요청을 사용자가 "RSVP이이 이벤트에 대 한" 링크를 클릭 하려고 합니다 */Dinners/Register/1* URL 유선상 아래 처럼 보이지만입니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-140">When the user clicks on the "RSVP for this event" link, a small HTTP POST network request is made to the */Dinners/Register/1* URL that looks like below on the wire:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

<span data-ttu-id="07eb4-141">및 Register 작업 메서드는 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-141">And the response from our Register action method is simply:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

<span data-ttu-id="07eb4-142">이 간단한 호출은 속도가 느린 네트워크를 통해도 작동 하며</span><span class="sxs-lookup"><span data-stu-id="07eb4-142">This lightweight call is fast and will work even over a slow network.</span></span>

### <a name="adding-a-jquery-animation"></a><span data-ttu-id="07eb4-143">JQuery 애니메이션 추가</span><span class="sxs-lookup"><span data-stu-id="07eb4-143">Adding a jQuery Animation</span></span>

<span data-ttu-id="07eb4-144">AJAX 기능을 구현 했습니다 및 빠른 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-144">The AJAX functionality we implemented works well and fast.</span></span> <span data-ttu-id="07eb4-145">경우에 따라 발생할 수 있습니다 따라서 빠르고 하지만 사용자를 새 텍스트로 RSVP 링크를 교체한을 느끼지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-145">Sometimes it can happen so fast, though, that a user might not notice that the RSVP link has been replaced with new text.</span></span> <span data-ttu-id="07eb4-146">업데이트 메시지에 주목 하도록 간단한 애니메이션을 더할 결과 좀 더 명확 하 게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-146">To make the outcome a little more obvious we can add a simple animation to draw attention to the update message.</span></span>

<span data-ttu-id="07eb4-147">기본 ASP.NET MVC 프로젝트 템플릿은 jQuery-microsoft 에서도 지원 되는 뛰어난과 매우 인기 있는 오픈 소스 JavaScript 라이브러리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-147">The default ASP.NET MVC project template includes jQuery – an excellent (and very popular) open source JavaScript library that is also supported by Microsoft.</span></span> <span data-ttu-id="07eb4-148">jQuery 다양 한 유용한 HTML DOM 선택 및 효과 라이브러리를 포함 하 여 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-148">jQuery provides a number of features, including a nice HTML DOM selection and effects library.</span></span>

<span data-ttu-id="07eb4-149">JQuery를 사용 하려면 먼저 스크립트 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-149">To use jQuery we'll first add a script reference to it.</span></span> <span data-ttu-id="07eb4-150">때문에 다양 한 위치 내에서 jQuery를 사용 하 여 사이트 내에서 수를 모든 페이지에서 사용할 수 있도록 스크립트 참조가 Site.master 마스터 페이지 파일 내에서 추가 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-150">Because we are going to be using jQuery within a variety of places within our site, we'll add the script reference within our Site.master master page file so that all pages can use it.</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

<span data-ttu-id="07eb4-151">*팁: VS 2008 sp1 JavaScript 파일 (jQuery 포함)에 대 한 다양 한 intellisense를 지 원하는 JavaScript intellisense 핫픽스를 설치 했는지 확인 합니다. 다운로드할 수 있습니다. http://tinyurl.com/vs2008javascripthotfix*</span><span class="sxs-lookup"><span data-stu-id="07eb4-151">*Tip: make sure you have installed the JavaScript intellisense hotfix for VS 2008 SP1 that enables richer intellisense support for JavaScript files (including jQuery). You can download it from: http://tinyurl.com/vs2008javascripthotfix*</span></span>

<span data-ttu-id="07eb4-152">JQuery를 자주 사용 하 여 작성 된 코드는 전역 "$ ()"를 사용 하 여 CSS 선택기를 사용 하 여 하나 이상의 HTML 요소를 검색 하는 JavaScript 메서드.</span><span class="sxs-lookup"><span data-stu-id="07eb4-152">Code written using JQuery often uses a global "$()" JavaScript method that retrieves one or more HTML elements using a CSS selector.</span></span> <span data-ttu-id="07eb4-153">예를 들어 <em>$("#rsvpmsg")</em> rsvpmsg의 id 사용 하 여 모든 HTML 요소를 선택 하는 동안 <em>$(".something")</em> "휴대 하는 것" CSS를 사용 하 여 모든 요소를 선택 하는 클래스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-153">For example, <em>$("#rsvpmsg")</em> selects any HTML element with the id of rsvpmsg, while <em>$(".something")</em> would select all elements with the "something" CSS class name.</span></span> <span data-ttu-id="07eb4-154">"Return 모든 선택 된 라디오 단추"와 같은 보다 고급 수준의 쿼리를 작성할 수도 있습니다와 같은 선택기 쿼리를 사용 하 여: <em>$("입력 [@type= 라디오] [@checked]")</em>합니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-154">You can also write more advanced queries like "return all of the checked radio buttons" using a selector query like: <em>$("input[@type=radio][@checked]")</em>.</span></span>

<span data-ttu-id="07eb4-155">숨기기와 같은 작업을 수행 하도록에서 메서드를 호출 하 여 요소를 선택한 후: *$("#rsvpmsg").hide();*</span><span class="sxs-lookup"><span data-stu-id="07eb4-155">Once you've selected elements, you can call methods on them to take action, like hiding them: *$("#rsvpmsg").hide();*</span></span>

<span data-ttu-id="07eb4-156">참석 여부 회신 시나리오에서는 "rsvpmsg"를 선택 하는 "AnimateRSVPMessage" 라는 간단한 JavaScript 함수를 정의 하겠습니다 &lt;div&gt; 해당 텍스트 콘텐츠 크기에 애니메이션 효과 줍니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-156">For our RSVP scenario, we'll define a simple JavaScript function named "AnimateRSVPMessage" that selects the "rsvpmsg" &lt;div&gt; and animates the size of its text content.</span></span> <span data-ttu-id="07eb4-157">그 다음으로 작은 텍스트 원인 시작 아래 코드는 400 밀리초 시간 지남에 따라 증가할 것:</span><span class="sxs-lookup"><span data-stu-id="07eb4-157">The below code starts the text small and then causes it to increase over a 400 milliseconds timeframe:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

<span data-ttu-id="07eb4-158">우리가 수 다음 실시간 접속 AJAX 호출 이름과 Ajax.ActionLink() 도우미 메서드를 전달 하 여 성공적으로 완료 된 후 호출할 JavaScript 함수가 (AjaxOptions "OnSuccess"를 통해 이벤트 속성):</span><span class="sxs-lookup"><span data-stu-id="07eb4-158">We can then wire-up this JavaScript function to be called after our AJAX call successfully completes by passing its name to our Ajax.ActionLink() helper method (via the AjaxOptions "OnSuccess" event property):</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

<span data-ttu-id="07eb4-159">이제 "RSVP이이 이벤트에 대 한" 링크를 클릭 하 고 AJAX 호출 완료 되 면 전송 된 메시지 콘텐츠 다시 애니메이션을 적용 되며 커질:</span><span class="sxs-lookup"><span data-stu-id="07eb4-159">And now when the "RSVP for this event" link is clicked and our AJAX call completes successfully, the content message sent back will animate and grow large:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

<span data-ttu-id="07eb4-160">"OnSuccess" 이벤트를 제공 하는 것 외에도 AjaxOptions 개체는 다양 한 다른 속성 및 유용한 옵션) (함께 처리할 수 있는 OnBegin, OnFailure, 및 OnComplete 이벤트를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-160">In addition to providing an "OnSuccess" event, the AjaxOptions object exposes OnBegin, OnFailure, and OnComplete events that you can handle (along with a variety of other properties and useful options).</span></span>

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a><span data-ttu-id="07eb4-161">정리-RSVP 부분 보기는 리팩터링</span><span class="sxs-lookup"><span data-stu-id="07eb4-161">Cleanup - Refactor out a RSVP Partial View</span></span>

<span data-ttu-id="07eb4-162">세부 정보 보기 템플릿은 초과 하 게 조금 이해 하기가 약간 긴 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-162">Our details view template is starting to get a little long, which overtime will make it a little harder to understand.</span></span> <span data-ttu-id="07eb4-163">코드 가독성을 높이기 위해 보겠습니다 가격 세부 정보 페이지에 대 한 RSVP 뷰 코드를 모두 캡슐화 하는 부분 보기 – RSVPStatus.ascx – 만들어 마무리 합니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-163">To help improve the code readability, let's finish up by creating a partial view – RSVPStatus.ascx – that encapsulate all of the RSVP view code for our Details page.</span></span>

<span data-ttu-id="07eb4-164">\Views\Dinners 폴더를 마우스 오른쪽 단추로 클릭 한 다음 선택 추가-이렇게 할&gt;메뉴 명령을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-164">We can do this by right-clicking on the \Views\Dinners folder and then choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="07eb4-165">해당 강력한 ViewModel로 저녁 식사를 적용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-165">We'll have it take a Dinner object as its strongly-typed ViewModel.</span></span> <span data-ttu-id="07eb4-166">에서는 다음 붙여 넣을 수 RSVP 콘텐츠를 Details.aspx 보기에서.</span><span class="sxs-lookup"><span data-stu-id="07eb4-166">We can then copy/paste the RSVP content from our Details.aspx view into it.</span></span>

<span data-ttu-id="07eb4-167">작업을 수행한 후도 보기를 만들어 보겠습니다 다른 부분 – EditAndDeleteLinks.ascx-편집 및 삭제 링크 보기 코드를 캡슐화 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-167">Once we've done that, let's also create another partial view – EditAndDeleteLinks.ascx - that encapsulates our Edit and Delete link view code.</span></span> <span data-ttu-id="07eb4-168">또한 해야 해당 강력한 ViewModel로 Dinner 개체를 사용 하 고 편집 및 삭제 논리를 Details.aspx 보기에서 복사/붙여넣기.</span><span class="sxs-lookup"><span data-stu-id="07eb4-168">We'll also have it take a Dinner object as its strongly-typed ViewModel, and copy/paste the Edit and Delete logic from our Details.aspx view into it.</span></span>

<span data-ttu-id="07eb4-169">정보의는 템플릿 수를 확인 한 후 바로 아래에 두 Html.RenderPartial() 메서드 호출을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-169">Our details view template can then just include two Html.RenderPartial() method calls at the bottom:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

<span data-ttu-id="07eb4-170">이렇게 하면 코드를 더 깔끔하게 읽고 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-170">This makes the code cleaner to read and maintain.</span></span>

### <a name="next-step"></a><span data-ttu-id="07eb4-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="07eb4-171">Next Step</span></span>

<span data-ttu-id="07eb4-172">이제 살펴보겠습니다 것을 수 있는 방법은 더욱 AJAX를 사용 하 여 응용 프로그램에 대화형 매핑 지원을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="07eb4-172">Let's now look at how we can use AJAX even further and add interactive mapping support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="07eb4-173">[이전](secure-applications-using-authentication-and-authorization.md)
> [다음](use-ajax-to-implement-mapping-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="07eb4-173">[Previous](secure-applications-using-authentication-and-authorization.md)
[Next](use-ajax-to-implement-mapping-scenarios.md)</span></span>
