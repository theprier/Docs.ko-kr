---
uid: mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-vb
title: JavaScript 주입 공격 방지 (VB) | Microsoft Docs
author: StephenWalther
description: JavaScript 주입 공격 및 사이트 간 스크립팅 공격 발생에서을 방지 합니다. 이 자습서에서는 Stephen walther가 하는 방법을 쉽게 de 설명 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/19/2008
ms.topic: article
ms.assetid: 9274a72e-34dd-4dae-8452-ed733ae71377
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-vb
msc.type: authoredcontent
ms.openlocfilehash: 6c022847462239624d5b84816999918ec77f8337
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37402343"
---
<a name="preventing-javascript-injection-attacks-vb"></a><span data-ttu-id="71cee-104">JavaScript 주입 공격 방지 (VB)</span><span class="sxs-lookup"><span data-stu-id="71cee-104">Preventing JavaScript Injection Attacks (VB)</span></span>
====================
<span data-ttu-id="71cee-105">[Stephen walther가](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="71cee-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="71cee-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="71cee-106">Download PDF</span></span>](http://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_06_VB.pdf)

> <span data-ttu-id="71cee-107">JavaScript 주입 공격 및 사이트 간 스크립팅 공격 발생에서을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-107">Prevent JavaScript Injection Attacks and Cross-Site Scripting Attacks from happening to you.</span></span> <span data-ttu-id="71cee-108">이 자습서에서는 Stephen walther가 이러한 유형의 HTML 콘텐츠 인코딩에 의해 공격을 쉽게 무력화 수 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-108">In this tutorial, Stephen Walther explains how you can easily defeat these types of attacks by HTML encoding your content.</span></span>


<span data-ttu-id="71cee-109">이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 JavaScript 주입 공격을 방지 하는 방법 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-109">The goal of this tutorial is to explain how you can prevent JavaScript injection attacks in your ASP.NET MVC applications.</span></span> <span data-ttu-id="71cee-110">이 자습서에는 JavaScript 주입 공격 으로부터 웹 사이트를 보호 하는 데 두 가지 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-110">This tutorial discusses two approaches to defending your website against a JavaScript injection attack.</span></span> <span data-ttu-id="71cee-111">데이터 표시를 인코딩하여 JavaScript 주입 공격을 방지 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-111">You learn how to prevent JavaScript injection attacks by encoding the data that you display.</span></span> <span data-ttu-id="71cee-112">동의 하는 데이터를 인코딩하여 JavaScript 주입 공격을 방지 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-112">You also learn how to prevent JavaScript injection attacks by encoding the data that you accept.</span></span>

## <a name="what-is-a-javascript-injection-attack"></a><span data-ttu-id="71cee-113">JavaScript 주입 공격을 란?</span><span class="sxs-lookup"><span data-stu-id="71cee-113">What is a JavaScript Injection Attack?</span></span>

<span data-ttu-id="71cee-114">사용자 입력을 허용 하 고 사용자 입력을 다시 표시 될 때마다 JavaScript 주입 공격에 웹 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-114">Whenever you accept user input and redisplay the user input, you open your website to JavaScript injection attacks.</span></span> <span data-ttu-id="71cee-115">JavaScript 주입 공격에 개방 된 구체적인 응용 프로그램을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-115">Let's examine a concrete application that is open to JavaScript injection attacks.</span></span>

<span data-ttu-id="71cee-116">고객 피드백 웹 사이트를 만들었다고 가정해 보겠습니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="71cee-116">Imagine that you have created a customer feedback website (see Figure 1).</span></span> <span data-ttu-id="71cee-117">고객 웹 사이트를 방문 하 고 제품을 사용 하 여 해당 환경을 피드백 입력 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-117">Customers can visit the website and enter feedback on their experience using your products.</span></span> <span data-ttu-id="71cee-118">고객 피드백을 제출 하는 경우 사용자 의견 피드백 페이지의 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-118">When a customer submits their feedback, the feedback is redisplayed on the feedback page.</span></span>


<span data-ttu-id="71cee-119">[![고객 피드백 웹 사이트](preventing-javascript-injection-attacks-vb/_static/image2.png)](preventing-javascript-injection-attacks-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="71cee-119">[![Customer Feedback Website](preventing-javascript-injection-attacks-vb/_static/image2.png)](preventing-javascript-injection-attacks-vb/_static/image1.png)</span></span>

<span data-ttu-id="71cee-120">**그림 01**: 고객 피드백 웹 사이트 ([큰 이미지를 보려면 클릭](preventing-javascript-injection-attacks-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="71cee-120">**Figure 01**: Customer Feedback Website ([Click to view full-size image](preventing-javascript-injection-attacks-vb/_static/image3.png))</span></span>


<span data-ttu-id="71cee-121">고객 피드백 웹 사이트를 사용 하는 `controller` 목록 1에서.</span><span class="sxs-lookup"><span data-stu-id="71cee-121">The customer feedback website uses the `controller` in Listing 1.</span></span> <span data-ttu-id="71cee-122">이 `controller` 라는 두 가지 동작 포함 `Index()` 및 `Create()`합니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-122">This `controller` contains two actions named `Index()` and `Create()`.</span></span>

<span data-ttu-id="71cee-123">**목록 1 – `HomeController.vb`**</span><span class="sxs-lookup"><span data-stu-id="71cee-123">**Listing 1 – `HomeController.vb`**</span></span>

[!code-vb[Main](preventing-javascript-injection-attacks-vb/samples/sample1.vb)]

<span data-ttu-id="71cee-124">합니다 `Index()` 메서드 표시는 `Index` 보기.</span><span class="sxs-lookup"><span data-stu-id="71cee-124">The `Index()` method displays the `Index` view.</span></span> <span data-ttu-id="71cee-125">이 메서드는 모든 이전 고객 피드백에 전달 된 `Index` (LINQ to SQL 쿼리를 사용 하 여) 데이터베이스에서 피드백을 검색 하 여 보기.</span><span class="sxs-lookup"><span data-stu-id="71cee-125">This method passes all of the previous customer feedback to the `Index` view by retrieving the feedback from the database (using a LINQ to SQL query).</span></span>

<span data-ttu-id="71cee-126">`Create()` 메서드는 새 피드백 항목을 만들고 데이터베이스에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-126">The `Create()` method creates a new Feedback item and adds it to the database.</span></span> <span data-ttu-id="71cee-127">폼에서를 입력 하는 메시지에 전달 되는 `Create()` 메시지 매개 변수에 메서드.</span><span class="sxs-lookup"><span data-stu-id="71cee-127">The message that the customer enters in the form is passed to the `Create()` method in the message parameter.</span></span> <span data-ttu-id="71cee-128">피드백 항목을 만들고 메시지 피드백 항목에 할당 되어 `Message` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-128">A Feedback item is created and the message is assigned to the Feedback item's `Message` property.</span></span> <span data-ttu-id="71cee-129">피드백을 사용 하 여 데이터베이스에 제출 되는 `DataContext.SubmitChanges()` 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-129">The Feedback item is submitted to the database with the `DataContext.SubmitChanges()` method call.</span></span> <span data-ttu-id="71cee-130">마지막으로, 방문자는 리디렉션됩니다는 `Index` 보기의 모든 의견 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-130">Finally, the visitor is redirected back to the `Index` view where all of the feedback is displayed.</span></span>

<span data-ttu-id="71cee-131">`Index` 보기가 목록 2에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-131">The `Index` view is contained in Listing 2.</span></span>

<span data-ttu-id="71cee-132">**2 – 나열 `Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="71cee-132">**Listing 2 – `Index.aspx`**</span></span>

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample2.aspx)]

<span data-ttu-id="71cee-133">`Index` 보기에는 두 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-133">The `Index` view has two sections.</span></span> <span data-ttu-id="71cee-134">맨 위 섹션에는 실제 고객 피드백이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-134">The top section contains the actual customer feedback form.</span></span> <span data-ttu-id="71cee-135">아래쪽 섹션에는 For 포함... 모든 이전 고객 피드백 항목을 반복 하 고 각 피드백 항목에 대 한 EntryDate 및 메시지 속성을 표시 하는 각 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-135">The bottom section contains a For..Each loop that loops through all of the previous customer feedback items and displays the EntryDate and Message properties for each feedback item.</span></span>

<span data-ttu-id="71cee-136">고객 피드백 웹 사이트는 간단한 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-136">The customer feedback website is a simple website.</span></span> <span data-ttu-id="71cee-137">그러나 웹 사이트는 JavaScript 주입 공격에 열려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-137">Unfortunately, the website is open to JavaScript injection attacks.</span></span>

<span data-ttu-id="71cee-138">고객 사용자 의견 양식으로 다음 텍스트를 입력 하는 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-138">Imagine that you enter the following text into the customer feedback form:</span></span>

[!code-html[Main](preventing-javascript-injection-attacks-vb/samples/sample3.html)]

<span data-ttu-id="71cee-139">이 텍스트는 경고 메시지 상자를 표시 하는 JavaScript 스크립트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-139">This text represents a JavaScript script that displays an alert message box.</span></span> <span data-ttu-id="71cee-140">이 스크립트를 피드백 제출 누군가가 후 양식의 메시지 <em>Boo!</em> 모든 사용자가 고객 피드백 웹 사이트에 방문 앞으로 (그림 2 참조) 될 때마다 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-140">After someone submits this script into the feedback form, the message <em>Boo!</em>will appear whenever anyone visits the customer feedback website in the future (see Figure 2).</span></span>


<span data-ttu-id="71cee-141">[![JavaScript 주입](preventing-javascript-injection-attacks-vb/_static/image5.png)](preventing-javascript-injection-attacks-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="71cee-141">[![JavaScript Injection](preventing-javascript-injection-attacks-vb/_static/image5.png)](preventing-javascript-injection-attacks-vb/_static/image4.png)</span></span>

<span data-ttu-id="71cee-142">**그림 02**: JavaScript 주입 ([큰 이미지를 보려면 클릭](preventing-javascript-injection-attacks-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="71cee-142">**Figure 02**: JavaScript Injection ([Click to view full-size image](preventing-javascript-injection-attacks-vb/_static/image6.png))</span></span>


<span data-ttu-id="71cee-143">이제 JavaScript 주입 공격에 대 한 초기 응답 무관심 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-143">Now, your initial response to JavaScript injection attacks might be apathy.</span></span> <span data-ttu-id="71cee-144">JavaScript 주입 공격의 형식일 뿐는 생각 *파손* 공격입니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-144">You might think that JavaScript injection attacks are simply a type of *defacement* attack.</span></span> <span data-ttu-id="71cee-145">아무도 작업을 수행 하려면 실제로 악의적인 JavaScript 주입 공격을 커밋하여 않다고 판단할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-145">You might believe that no one can do anything truly evil by committing a JavaScript injection attack.</span></span>

<span data-ttu-id="71cee-146">아쉽게도 해커가 가능 일부 실제로 웹 사이트에 JavaScript를 주입 하 여 실제로 악의적인 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-146">Unfortunately, a hacker can do some really, really evil things by injecting JavaScript into a website.</span></span> <span data-ttu-id="71cee-147">사이트 간 스크립팅 (XSS) 공격을 수행 하는 JavaScript 주입 공격을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-147">You can use a JavaScript injection attack to perform a Cross-Site Scripting (XSS) attack.</span></span> <span data-ttu-id="71cee-148">사이트 간 스크립팅 공격, 기밀 사용자 정보를 도용 하 고 다른 웹 사이트에 정보를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-148">In a Cross-Site Scripting attack, you steal confidential user information and send the information to another website.</span></span>

<span data-ttu-id="71cee-149">예를 들어 해커가 값을 다른 사용자의 브라우저 쿠키를 도용 하 JavaScript 주입 공격을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-149">For example, a hacker can use a JavaScript injection attack to steal the values of browser cookies from other users.</span></span> <span data-ttu-id="71cee-150">암호, 신용 카드 번호나 주민 등록 번호 – 같은 중요 한 정보는 브라우저 쿠키에 저장 됩니다, 해커가이 정보를 도용 하 JavaScript 주입 공격을를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-150">If sensitive information -- such as passwords, credit card numbers, or social security numbers – is stored in the browser cookies, then a hacker can use a JavaScript injection attack to steal this information.</span></span> <span data-ttu-id="71cee-151">또는 사용자가 해커는 주입 된 JavaScript를 사용 하 여 폼 데이터를 다른 사이트로 전송 하 수 JavaScript 공격을 사용 하 여 손상 된 페이지에 포함 된 폼 필드에 중요 한 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-151">Or, if a user enters sensitive information in a form field contained in a page that has been compromised with a JavaScript attack, then the hacker can use the injected JavaScript to grab the form data and send it to another website.</span></span>

<span data-ttu-id="71cee-152">*장단점이 수*입니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-152">*Please be scared*.</span></span> <span data-ttu-id="71cee-153">JavaScript 주입 공격을 심각 하 게 수행 하 고 사용자의 기밀 정보를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-153">Take JavaScript injection attacks seriously and protect your user's confidential information.</span></span> <span data-ttu-id="71cee-154">다음 두 섹션에서는 JavaScript 주입 공격 으로부터 ASP.NET MVC 응용 프로그램을 보호 하는 데 사용할 수 있는 두 가지 기술을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-154">In the next two sections, we discuss two techniques that you can use to defend your ASP.NET MVC applications from JavaScript injection attacks.</span></span>

## <a name="approach-1-html-encode-in-the-view"></a><span data-ttu-id="71cee-155">방법 #1: HTML 보기에서 인코딩</span><span class="sxs-lookup"><span data-stu-id="71cee-155">Approach #1: HTML Encode in the View</span></span>

<span data-ttu-id="71cee-156">HTML로 JavaScript 주입 공격을 방지 하는 쉬운 방법을 한 가지 뷰에서 데이터를 다시 표시 하면 웹 사이트 사용자가 입력 한 모든 데이터를 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-156">One easy method of preventing JavaScript injection attacks is to HTML encode any data entered by website users when you redisplay the data in a view.</span></span> <span data-ttu-id="71cee-157">업데이트 된 `Index` 보기 목록 3에서은이 접근 방식을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-157">The updated `Index` view in Listing 3 follows this approach.</span></span>

<span data-ttu-id="71cee-158">**코드 3 – `Index.aspx` (인코딩된 HTML)**</span><span class="sxs-lookup"><span data-stu-id="71cee-158">**Listing 3 – `Index.aspx` (HTML Encoded)**</span></span>

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample4.aspx)]

<span data-ttu-id="71cee-159">값 `feedback.Message` html 값을 다음 코드로 표시 되기 전에 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-159">Notice that the value of `feedback.Message` is HTML encoded before the value is displayed with the following code:</span></span>

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample5.aspx)]

<span data-ttu-id="71cee-160">것 평균 HTML로 인코딩 문자열로?</span><span class="sxs-lookup"><span data-stu-id="71cee-160">What does it mean to HTML encode a string?</span></span> <span data-ttu-id="71cee-161">HTML 인코딩할 때 문자열, 위험 등의 문자 `<` 하 고 `>` 와 같은 HTML 엔터티 참조로 대체 됩니다 `&lt;` 및 `&gt;`합니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-161">When you HTML encode a string, dangerous characters such as `<` and `>` are replaced by HTML entity references such as `&lt;` and `&gt;`.</span></span> <span data-ttu-id="71cee-162">있으므로 문자열 `<script>alert("Boo!")</script>` html 인코딩 변환 `&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`합니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-162">So when the string `<script>alert("Boo!")</script>` is HTML encoded, it gets converted to `&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`.</span></span> <span data-ttu-id="71cee-163">인코딩된 문자열은 더 이상 브라우저에서 해석 하는 경우 JavaScript 스크립트로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-163">The encoded string no longer executes as a JavaScript script when interpreted by a browser.</span></span> <span data-ttu-id="71cee-164">대신, 그림 3에 무해 한 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-164">Instead, you get the harmless page in Figure 3.</span></span>


<span data-ttu-id="71cee-165">[![패배 JavaScript 공격](preventing-javascript-injection-attacks-vb/_static/image8.png)](preventing-javascript-injection-attacks-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="71cee-165">[![Defeated JavaScript Attack](preventing-javascript-injection-attacks-vb/_static/image8.png)](preventing-javascript-injection-attacks-vb/_static/image7.png)</span></span>

<span data-ttu-id="71cee-166">**그림 03**: 패배 JavaScript 공격 ([큰 이미지를 보려면 클릭](preventing-javascript-injection-attacks-vb/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="71cee-166">**Figure 03**: Defeated JavaScript Attack ([Click to view full-size image](preventing-javascript-injection-attacks-vb/_static/image9.png))</span></span>


<span data-ttu-id="71cee-167">되었는지 확인 합니다 `Index` 의 값만 목록 3에서 볼 `feedback.Message` 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-167">Notice that in the `Index` view in Listing 3 only the value of `feedback.Message` is encoded.</span></span> <span data-ttu-id="71cee-168">변수의 `feedback.EntryDate` 는 인코딩되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-168">The value of `feedback.EntryDate` is not encoded.</span></span> <span data-ttu-id="71cee-169">사용자가 입력 한 데이터를 인코드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-169">You only need to encode data entered by a user.</span></span> <span data-ttu-id="71cee-170">EntryDate 값 컨트롤러에서 생성 된 때문에 없는 필요한 HTML로 인코딩할이 값입니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-170">Because the value of EntryDate was generated in the controller, you don't need to HTML encode this value.</span></span>

## <a name="approach-2-html-encode-in-the-controller"></a><span data-ttu-id="71cee-171">컨트롤러의 접근 방식 2: HTML 인코딩</span><span class="sxs-lookup"><span data-stu-id="71cee-171">Approach #2: HTML Encode in the Controller</span></span>

<span data-ttu-id="71cee-172">HTML HTML 인코딩 데이터 뷰에서 데이터를 표시 하는 경우, 대신 있습니다 데이터베이스로 데이터를 제출 하기 전에만 데이터를 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-172">Instead of HTML encoding data when you display the data in a view, you can HTML encode the data just before you submit the data to the database.</span></span> <span data-ttu-id="71cee-173">이 두 번째 방법은의 경우 사용 되는 `controller` 4에서.</span><span class="sxs-lookup"><span data-stu-id="71cee-173">This second approach is taken in the case of the `controller` in Listing 4.</span></span>

<span data-ttu-id="71cee-174">**코드 4 – `HomeController.cs` (인코딩된 HTML)**</span><span class="sxs-lookup"><span data-stu-id="71cee-174">**Listing 4 – `HomeController.cs` (HTML Encoded)**</span></span>

[!code-vb[Main](preventing-javascript-injection-attacks-vb/samples/sample6.vb)]

<span data-ttu-id="71cee-175">메시지의 값을 HTML 인코딩된 값 내에 데이터베이스에 전송 되기 전에는 `Create()` 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-175">Notice that the value of Message is HTML encoded before the value is submitted to the database within the `Create()` action.</span></span> <span data-ttu-id="71cee-176">보기에서 메시지를 다시 표시 됩니다, 경우 메시지 HTML 인코딩해야 이며 메시지에 지정 된 JavaScript 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-176">When the Message is redisplayed in the view, the Message is HTML encoded and any JavaScript injected in the Message is not executed.</span></span>

<span data-ttu-id="71cee-177">일반적으로이 두 번째 접근 방식을 통해이 자습서에 설명 된 첫 번째 방법은 선호 합니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-177">Typically, you should favor the first approach discussed in this tutorial over this second approach.</span></span> <span data-ttu-id="71cee-178">이 두 번째 방법의 문제는 결국 HTML로 인코딩된 데이터를 사용 하 여 데이터베이스의 경우</span><span class="sxs-lookup"><span data-stu-id="71cee-178">The problem with this second approach is that you end up with HTML encoded data in your database.</span></span> <span data-ttu-id="71cee-179">즉, 데이터베이스 데이터 재미 있는 보이는 문자를 사용 하 여 정리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-179">In other words, your database data is dirtied with funny looking characters.</span></span>

<span data-ttu-id="71cee-180">이 이유는 잘못 된?</span><span class="sxs-lookup"><span data-stu-id="71cee-180">Why is this bad?</span></span> <span data-ttu-id="71cee-181">웹 페이지 외의 다른 데이터베이스 데이터를 표시 해야 하는 경우 다음은 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-181">If you ever need to display the database data in something other than a web page, then you will have problems.</span></span> <span data-ttu-id="71cee-182">예를 들어, Windows Forms 응용 프로그램에서 데이터를 더 이상 쉽게 표시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-182">For example, you can no longer easily display the data in a Windows Forms application.</span></span>

## <a name="summary"></a><span data-ttu-id="71cee-183">요약</span><span class="sxs-lookup"><span data-stu-id="71cee-183">Summary</span></span>

<span data-ttu-id="71cee-184">이 자습서의 목적은 JavaScript 주입 공격을 없어질 수 있다는 가능성에 대 한 두려워 하는 것 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="71cee-184">The purpose of this tutorial was to scare you about the prospect of a JavaScript injection attack.</span></span> <span data-ttu-id="71cee-185">이 자습서에는 JavaScript 주입 공격 으로부터 ASP.NET MVC 응용 프로그램을 방어 하기 위한 두 가지 방법을 설명: 할 수 있습니다 하거나 HTML 제출 하는 사용자를 인코딩할 수 있는 HTML 보기에는 데이터 제출 하는 사용자를 인코딩 컨트롤러의 데이터.</span><span class="sxs-lookup"><span data-stu-id="71cee-185">This tutorial discussed two approaches for defending your ASP.NET MVC applications against JavaScript injection attacks: you can either HTML encode user submitted data in the view or you can HTML encode user submitted data in the controller.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="71cee-186">이전</span><span class="sxs-lookup"><span data-stu-id="71cee-186">Previous</span></span>](authenticating-users-with-windows-authentication-vb.md)
