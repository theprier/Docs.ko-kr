---
uid: web-pages/overview/ui-layouts-and-themes/4-working-with-forms
title: "ASP.NET 웹 페이지 (Razor) 사이트의 HTML 양식 작업 | Microsoft Docs"
author: tfitzmac
description: "양식은은 텍스트 상자, 확인란, 라디오 단추, 풀 다운 목록 등의 사용자 입력 컨트롤을 배치 하는 위치는 HTML 문서의 섹션입니다. 양식을 사용 하면 wh..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2014
ms.topic: article
ms.assetid: f3f4b8c8-e8f6-4474-ad94-69228a6c01ee
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/4-working-with-forms
msc.type: authoredcontent
ms.openlocfilehash: fcdded3a7e80ee797eae445f347735f0f7b3d7ad
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="working-with-html-forms-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="c2ca5-104">ASP.NET 웹 페이지 (Razor) 사이트에서 HTML 폼 사용</span><span class="sxs-lookup"><span data-stu-id="c2ca5-104">Working with HTML Forms in ASP.NET Web Pages (Razor) Sites</span></span>
====================
<span data-ttu-id="c2ca5-105">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c2ca5-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="c2ca5-106">이 문서에서는 텍스트 상자 및 단추) (사용 하 여 HTML 폼을 처리 하는 방법을 설명에서 ASP.NET 웹 페이지 (Razor) 웹 사이트에서 작업 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-106">This article describes how to process an HTML form (with text boxes and buttons) when you are working in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="c2ca5-107">**학습 내용:**</span><span class="sxs-lookup"><span data-stu-id="c2ca5-107">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="c2ca5-108">HTML 폼을 만드는 방법.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-108">How to create an HTML form.</span></span>
> - <span data-ttu-id="c2ca5-109">폼에서 사용자 입력을 읽고 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-109">How to read user input from the form.</span></span>
> - <span data-ttu-id="c2ca5-110">사용자 입력의 유효성을 검사 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-110">How to validate user input.</span></span>
> - <span data-ttu-id="c2ca5-111">페이지가 제출 되 양식 값을 복원 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-111">How to restore form values after the page is submitted.</span></span>
> 
> <span data-ttu-id="c2ca5-112">프로그래밍 개념 문서에 도입 된 ASP.NET은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-112">These are the ASP.NET programming concepts introduced in the article:</span></span>
> 
> - <span data-ttu-id="c2ca5-113">`Request` 개체</span><span class="sxs-lookup"><span data-stu-id="c2ca5-113">The `Request` object.</span></span>
> - <span data-ttu-id="c2ca5-114">입력된 유효성 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-114">Input validation.</span></span>
> - <span data-ttu-id="c2ca5-115">HTML 인코딩입니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-115">HTML encoding.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c2ca5-116">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="c2ca5-116">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="c2ca5-117">ASP.NET 웹 페이지 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="c2ca5-117">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="c2ca5-118">이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-118">This tutorial also works with ASP.NET Web Pages 2.</span></span>


## <a name="creating-a-simple-html-form"></a><span data-ttu-id="c2ca5-119">간단한 HTML 양식 만들기</span><span class="sxs-lookup"><span data-stu-id="c2ca5-119">Creating a Simple HTML Form</span></span>

1. <span data-ttu-id="c2ca5-120">새 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-120">Create a new website.</span></span>
2. <span data-ttu-id="c2ca5-121">루트 폴더에 명명 된 웹 페이지 생성 *Form.cshtml* 다음 태그를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-121">In the root folder, create a web page named *Form.cshtml* and enter the following markup:</span></span>

    [!code-html[Main](4-working-with-forms/samples/sample1.html)]
3. <span data-ttu-id="c2ca5-122">브라우저에서 페이지를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-122">Launch the page in your browser.</span></span> <span data-ttu-id="c2ca5-123">(WebMatrix에서에서 **파일** 작업 영역에서 파일을 마우스 오른쪽 단추로 클릭 한 다음 선택 **브라우저에서 시작**.) 세 개의 입력된 필드가 있는 간단한 양식 및 **전송** 단추가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-123">(In WebMatrix, in the **Files** workspace, right-click the file and then select **Launch in browser**.) A simple form with three input fields and a **Submit** button is displayed.</span></span>

    ![세 가지 텍스트 상자를 사용 하 여 폼의 스크린 샷](4-working-with-forms/_static/image1.jpg)

    <span data-ttu-id="c2ca5-125">클릭 하면이 시점에서 **전송** 단추를 아무 일도 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-125">At this point, if you click the **Submit** button, nothing happens.</span></span> <span data-ttu-id="c2ca5-126">폼을 유용 하 게 하는 서버에서 실행 되는 일부 코드를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-126">To make the form useful, you have to add some code that will run on the server.</span></span>

## <a name="reading-user-input-from-the-form"></a><span data-ttu-id="c2ca5-127">폼에서 사용자 입력을 읽기</span><span class="sxs-lookup"><span data-stu-id="c2ca5-127">Reading User Input from the Form</span></span>

<span data-ttu-id="c2ca5-128">폼을 처리 하려면 제출 된 필드 값을 읽고를 이러한 특정 작업을 수행 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-128">To process the form, you add code that reads the submitted field values and does something with them.</span></span> <span data-ttu-id="c2ca5-129">이 절차는 필드를 읽고 페이지에서 사용자 입력을 표시 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-129">This procedure shows you how to read the fields and display the user input on the page.</span></span> <span data-ttu-id="c2ca5-130">(프로덕션 응용 프로그램에서는 일반적으로 수행한 사용자 입력으로 더욱 흥미로운 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-130">(In a production application, you generally do more interesting things with user input.</span></span> <span data-ttu-id="c2ca5-131">작업입니다 데이터베이스 작업에 대 한 문서에서.)</span><span class="sxs-lookup"><span data-stu-id="c2ca5-131">You'll do that in the article about working with databases.)</span></span>

1. <span data-ttu-id="c2ca5-132">맨 위에 있는 *Form.cshtml* 파일에서 다음 코드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-132">At the top of the *Form.cshtml* file, enter the following code:</span></span>

    [!code-cshtml[Main](4-working-with-forms/samples/sample2.cshtml)]

    <span data-ttu-id="c2ca5-133">먼저 사용자가 페이지를 요청 하는 경우 빈 폼에만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-133">When the user first requests the page, only the empty form is displayed.</span></span> <span data-ttu-id="c2ca5-134">(있습니다 수) 있는 사용자는 양식을 누르면 **전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-134">The user (which will be you) fills in the form and then clicks **Submit**.</span></span> <span data-ttu-id="c2ca5-135">(게시)를 전송 하는이 서버에 사용자 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-135">This submits (posts) the user input to the server.</span></span> <span data-ttu-id="c2ca5-136">기본적으로 동일한 페이지로 이동 (즉, *Form.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="c2ca5-136">By default, the request goes to the same page (namely, *Form.cshtml*).</span></span>

    <span data-ttu-id="c2ca5-137">이 현재 페이지를 전송 하는 경우 폼 바로 위에 입력 한 값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-137">When you submit the page this time, the values you entered are displayed just above the form:</span></span>

    ![페이지에 표시 하는 입력 한 값을 보여 주는 스크린 샷](4-working-with-forms/_static/image2.jpg)

    <span data-ttu-id="c2ca5-139">코드 페이지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-139">Look at the code for the page.</span></span> <span data-ttu-id="c2ca5-140">먼저 사용 하는 `IsPost` 페이지가 게시 되 고 있는지 여부 및 #8212; 즉, 사용자가 클릭 했는지 여부를 확인 하는 **전송** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-140">You first use the `IsPost` method to determine whether the page is being posted &#8212; that is, whether a user clicked the **Submit** button.</span></span> <span data-ttu-id="c2ca5-141">Post, 이것이 `IsPost` true를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-141">If this is a post, `IsPost` returns true.</span></span> <span data-ttu-id="c2ca5-142">이것이 있는지 여부를 사용 하는 초기 요청 (GET 요청) 또는 다시 게시 (POST 요청)을 확인 하려면 ASP.NET 웹 페이지에서 표준 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-142">This is the standard way in ASP.NET Web Pages to determine whether you're working with an initial request (a GET request) or a postback (a POST request).</span></span> <span data-ttu-id="c2ca5-143">(GET 및 POST에 대 한 자세한 내용은 "HTTP GET 및 POST 및 IsPost Property" 세로 막대의 참조 [ASP.NET 웹 페이지 프로그래밍 구문을 사용 하 여 Razor 소개](https://go.microsoft.com/fwlink/?LinkId=202890#SB_HttpGetPost).)</span><span class="sxs-lookup"><span data-stu-id="c2ca5-143">(For more information about GET and POST, see the sidebar "HTTP GET and POST and the IsPost Property" in [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890#SB_HttpGetPost).)</span></span>

    <span data-ttu-id="c2ca5-144">사용자가 입력 하는 값을 가져오려면 다음으로 `Request.Form` 개체에 추가한 변수 나중에 적용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-144">Next, you get the values that the user filled in from the `Request.Form` object, and you put them in variables for later.</span></span> <span data-ttu-id="c2ca5-145">`Request.Form` 키로 식별 하는 각 페이지와 전송 된 모든 값을 포함 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-145">The `Request.Form` object contains all the values that were submitted with the page, each identified by a key.</span></span> <span data-ttu-id="c2ca5-146">키는 해당 하는 고 `name` 읽으려는 양식 필드의 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-146">The key is the equivalent to the `name` attribute of the form field that you want to read.</span></span> <span data-ttu-id="c2ca5-147">예를 들어, 읽을 수는 `companyname` 필드 (텍스트 상자)를 사용 하면 `Request.Form["companyname"]`합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-147">For example, to read the `companyname` field (text box), you use `Request.Form["companyname"]`.</span></span>

    <span data-ttu-id="c2ca5-148">폼 값에 저장 되는 `Request.Form` 문자열로 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-148">Form values are stored in the `Request.Form` object as strings.</span></span> <span data-ttu-id="c2ca5-149">따라서는 숫자, 날짜 또는 일부 다른 형식으로 값을 사용 해야 할 때 해당 형식으로 문자열에서 변환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-149">Therefore, when you have to work with a value as a number or a date or some other type, you have to convert it from a string to that type.</span></span> <span data-ttu-id="c2ca5-150">예제에서는 `AsInt` 의 메서드는 `Request.Form` (포함 하는 직원 수) 직원 필드의 값을 정수로 변환 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-150">In the example, the `AsInt` method of the `Request.Form` is used to convert the value of the employees field (which contains an employee count) to an integer.</span></span>
2. <span data-ttu-id="c2ca5-151">브라우저에서 페이지를 시작, 양식 필드를 입력 하 고 클릭 **전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-151">Launch the page in your browser, fill in the form fields, and click **Submit**.</span></span> <span data-ttu-id="c2ca5-152">페이지 입력 한 값을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-152">The page displays the values you entered.</span></span>

> [!TIP] 
> 
> <a id="SB_HTMLEncoding"></a>
> ### <a name="html-encoding-for-appearance-and-security"></a><span data-ttu-id="c2ca5-153">모양 및 보안에 대 한 인코딩을 HTML</span><span class="sxs-lookup"><span data-stu-id="c2ca5-153">HTML Encoding for Appearance and Security</span></span>
> 
> <span data-ttu-id="c2ca5-154">등의 문자에 대 한 특별 한 용도로 사용할 HTML `<`, `>`, 및 `&`합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-154">HTML has special uses for characters like `<`, `>`, and `&`.</span></span> <span data-ttu-id="c2ca5-155">이러한 특수 문자가 표시 되지 필요한 위치, 모양 및 기능 웹 페이지의 손상 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-155">If these special characters appear where they're not expected, they can ruin the appearance and functionality of your web page.</span></span> <span data-ttu-id="c2ca5-156">브라우저에서 해석 하는 예를 들어는 `<` (에 오지 않으면 공백)는 HTML 요소의 시작으로 같은 문자 `<b>` 또는 `<input ...>`합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-156">For example, the browser interprets the `<` character (unless it's followed by a space) as the beginning of an HTML element, like `<b>` or `<input ...>`.</span></span> <span data-ttu-id="c2ca5-157">브라우저에서 요소를 인식 하지 못하는 경우는 삭제 됩니다로 시작 하는 문자열 `<` 다시 인식 도달할 때까지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-157">If the browser doesn't recognize the element, it simply discards the string that begins with `<` until it reaches something that it again recognizes.</span></span> <span data-ttu-id="c2ca5-158">물론,이 페이지에서 일부 이상한 렌더링에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-158">Obviously, this can result in some weird rendering in the page.</span></span>
> 
> <span data-ttu-id="c2ca5-159">HTML 인코딩을 브라우저 올바른 기호로 해석 된 코드와 같은 예약 된 문자를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-159">HTML encoding replaces these reserved characters with a code that browsers interpret as the correct symbol.</span></span> <span data-ttu-id="c2ca5-160">예를 들어는 `<` 문자 아래 템플릿으로 바뀝니다 `&lt;` 및 `>` 문자 아래 템플릿으로 바뀝니다 `&gt;`합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-160">For example, the `<` character is replaced with `&lt;` and the `>` character is replaced with `&gt;`.</span></span> <span data-ttu-id="c2ca5-161">브라우저 보려는 문자로 이러한 대체 문자열을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-161">The browser renders these replacement strings as the characters that you want to see.</span></span>
> 
> <span data-ttu-id="c2ca5-162">되었기 HTML 문자열을 표시 하는 언제 든 지 인코딩을 사용 하도록 (입력) 사용자 로부터 받은 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-162">It's a good idea to use HTML encoding any time you display strings (input) that you got from a user.</span></span> <span data-ttu-id="c2ca5-163">이렇게 하지 않으면 사용자는 사용자 웹 페이지를 악성 스크립트를 실행 하거나 다른 작업을 사이트 보안을 저해 하 또는 의도 하지 않은 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-163">If you don't, a user can try to get your web page to run a malicious script or do something else that compromises your site security or that's just not what you intend.</span></span> <span data-ttu-id="c2ca5-164">(이것은 예를 들어 블로그 주석으로 사용자 검토를; 사용자 입력을 했지만 위치를 저장 한 다음 나중에 &#8212;표시할 사용 하는 경우에 특히 중요 또는 같은 내용을)</span><span class="sxs-lookup"><span data-stu-id="c2ca5-164">(This is particularly important if you take user input, store it someplace, and then display it later &#8212; for example, as a blog comment, user review, or something like that.)</span></span>
> 
> <span data-ttu-id="c2ca5-165">이러한 문제를 ASP.NET 웹 페이지를 자동으로 방지 하려면 HTML로 인코딩하고 텍스트 콘텐츠를 사용자 코드에서 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-165">To help prevent these problems, ASP.NET Web Pages automatically HTML-encodes any text content that you output from your code.</span></span> <span data-ttu-id="c2ca5-166">예를 들어, 변수 또는 같은 코드를 사용 하는 식의 내용을 표시할 때는 `@MyVar`, ASP.NET 웹 페이지는 출력을 자동으로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-166">For example, when you display the content of a variable or an expression using code such as `@MyVar`, ASP.NET Web Pages automatically encodes the output.</span></span>


## <a name="validating-user-input"></a><span data-ttu-id="c2ca5-167">사용자 입력 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="c2ca5-167">Validating User Input</span></span>

<span data-ttu-id="c2ca5-168">사용자 실수.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-168">Users make mistakes.</span></span> <span data-ttu-id="c2ca5-169">필드에 입력 하도록 요청 하면 및, 인하고 잊지 않도록 또는 직원 수를 입력 하도록 요청 하면 및 대신 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-169">You ask them to fill in a field, and they forget to, or you ask them to enter the number of employees and they type a name instead.</span></span> <span data-ttu-id="c2ca5-170">을 하는 폼 채워져 올바르게 처리 하기 전에 확인 하기 위해 사용자의 입력을 검증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-170">To make sure that a form has been filled in correctly before you process it, you validate the user's input.</span></span>

<span data-ttu-id="c2ca5-171">이 절차에서는 사용자 하지 않았습니다 고 비워 두어도 되도록 모든 세 양식 필드의 유효성을 검사 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-171">This procedure shows how to validate all three form fields to make sure the user didn't leave them blank.</span></span> <span data-ttu-id="c2ca5-172">또한 직원 수 값이 숫자 인지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-172">You also check that the employee count value is a number.</span></span> <span data-ttu-id="c2ca5-173">오류를 표시 합니다 오류가 있는 경우 값은 사용자에 게 알리는 메시지 유효성 검사를 통과 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-173">If there are errors, you'll display an error message that tells the user what values didn't pass validation.</span></span>

1. <span data-ttu-id="c2ca5-174">에 *Form.cshtml* 파일, 코드의 첫 번째 블록을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-174">In the *Form.cshtml* file, replace the first block of code with the following code:</span></span> 

    [!code-cshtml[Main](4-working-with-forms/samples/sample3.cshtml)]

    <span data-ttu-id="c2ca5-175">사용자 입력 유효성 검사를 사용 하면는 `Validation` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-175">To validate user input, you use the `Validation` helper.</span></span> <span data-ttu-id="c2ca5-176">필수 필드를 호출 하 여 등록 `Validation.RequireField`합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-176">You register required fields by calling `Validation.RequireField`.</span></span> <span data-ttu-id="c2ca5-177">다른 종류의 유효성 검사를 호출 하 여 등록 `Validation.Add` 유효성을 검사할 필드와 수행할 유효성 검사의 유형을 지정 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-177">You register other types of validation by calling `Validation.Add` and specifying the field to validate and the type of validation to perform.</span></span>

    <span data-ttu-id="c2ca5-178">페이지를 실행 하는 경우 ASP.NET 사용자에 대 한 모든 유효성 검사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-178">When the page runs, ASP.NET does all the validation for you.</span></span> <span data-ttu-id="c2ca5-179">호출 하 여 결과 확인할 수 `Validation.IsValid`, 모든 항목에 전달 되 면 true를 반환 하 고 필드 유효성 검사에 실패 하면 false입니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-179">You can check the results by calling `Validation.IsValid`, which returns true if everything passed and false if any field failed validation.</span></span> <span data-ttu-id="c2ca5-180">일반적으로 호출 `Validation.IsValid` 전에 사용자 입력에 처리를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-180">Typically, you call `Validation.IsValid` before you perform any processing on the user input.</span></span>
2. <span data-ttu-id="c2ca5-181">업데이트는 `<body>` 를 세 번 호출을 추가 하 여 요소는 `Html.ValidationMessage` 다음과 같이 메서드:</span><span class="sxs-lookup"><span data-stu-id="c2ca5-181">Update the `<body>` element by adding three calls to the `Html.ValidationMessage` method, like this:</span></span>

    [!code-cshtml[Main](4-working-with-forms/samples/sample4.cshtml?highlight=8,13,18)]

    <span data-ttu-id="c2ca5-182">유효성 검사 오류 메시지를 표시 하려면 Html을 호출할 수 있습니다.`ValidationMessage`</span><span class="sxs-lookup"><span data-stu-id="c2ca5-182">To display validation error messages, you can call Html.`ValidationMessage`</span></span> <span data-ttu-id="c2ca5-183">에 대 한 메시지를 원하는 필드의 이름을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-183">and pass it the name of the field that you want the message for.</span></span>
3. <span data-ttu-id="c2ca5-184">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-184">Run the page.</span></span> <span data-ttu-id="c2ca5-185">필드를 비워 두고 클릭 **전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-185">Leave the fields blank and click **Submit**.</span></span> <span data-ttu-id="c2ca5-186">오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-186">You see error messages.</span></span>

    ![사용자 입력 유효성 검사를 통과 하지 못하면 오류 메시지가 표시를 보여 주는 스크린 샷](4-working-with-forms/_static/image3.jpg)
4. <span data-ttu-id="c2ca5-188">문자열 (예를 들어 "ABC")을 추가 **직원 수** 필드를 클릭 **전송** 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-188">Add a string (for example, "ABC") to the **Employee Count** field and click **Submit** again.</span></span> <span data-ttu-id="c2ca5-189">이 시간을 나타내는 오류가 표시 문자열 올바른 형식으로 정수 즉, 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-189">This time you see an error that indicates that the string isn't in the right format, namely, an integer.</span></span>

    ![사용자가 직원 필드에 대 한 문자열을 입력 하는 경우 표시 되는 오류 메시지를 보여 주는 스크린 샷](4-working-with-forms/_static/image4.jpg)

<span data-ttu-id="c2ca5-191">ASP.NET 웹 페이지에는 사용자 입력을 자동으로 사용자가 브라우저에 대 한 즉각적인 피드백 얻을 수 있도록 클라이언트 스크립트를 사용 하 여 유효성 검사를 수행 하는 기능을 포함 하 여 유효성을 검사 하는 옵션이 더 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-191">ASP.NET Web Pages provides more options for validating user input, including the ability to automatically perform validation using client script, so that users get immediate feedback in the browser.</span></span> <span data-ttu-id="c2ca5-192">참조는 [추가 리소스](#Additional_Resources) 자세한 내용은 나중에 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-192">See the [Additional Resources](#Additional_Resources) section later for more information.</span></span>

## <a name="restoring-form-values-after-postbacks"></a><span data-ttu-id="c2ca5-193">포스트백 후 양식 값을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-193">Restoring Form Values After Postbacks</span></span>

<span data-ttu-id="c2ca5-194">이전 섹션에서 페이지를 테스트할 때 발견할 수 있습니다 하는 경우 다음 유효성 검사 오류, (잘못 된 데이터 뿐 아니라)를 입력 한 모든 항목이 제거 되었고가 모든 필드에 대 한 값을 다시 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-194">When you tested the page in the previous section, you might have noticed that if you had a validation error, everything you entered (not just the invalid data) was gone, and you had to re-enter values for all the fields.</span></span> <span data-ttu-id="c2ca5-195">중요 한 점은 들: 페이지는 처음부터 다시 만들어질 때 페이지를 제출 하 고 처리 한 다음 페이지를 다시 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-195">This illustrates an important point: when you submit a page, process it, and then render the page again, the page is re-created from scratch.</span></span> <span data-ttu-id="c2ca5-196">살펴본 것 처럼 즉, 전송 될 때 페이지에 있는 모든 값은 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-196">As you saw, this means that any values that were in the page when it was submitted are lost.</span></span>

<span data-ttu-id="c2ca5-197">그러나 해결할 수 있습니다이 쉽게.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-197">You can fix this easily, however.</span></span> <span data-ttu-id="c2ca5-198">전송 된 값에 액세스할 수 있습니다 (에 `Request.Form` 개체, 페이지 렌더링 될 때 다시 양식 필드에 해당 값을 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-198">You have access to the values that were submitted (in the `Request.Form` object, so you can fill those values back into the form fields when the page is rendered.</span></span>

1. <span data-ttu-id="c2ca5-199">에 *Form.cshtml* 파일, 대체는 `value` 의 특성은 `<input>` 사용 하 여 요소는 `value` 특성.:</span><span class="sxs-lookup"><span data-stu-id="c2ca5-199">In the *Form.cshtml* file, replace the `value` attributes of the `<input>` elements using the `value` attribute.:</span></span> 

    [!code-cshtml[Main](4-working-with-forms/samples/sample5.cshtml?highlight=13,19,25)]

    <span data-ttu-id="c2ca5-200">`value` 특성에는 `<input>` 동적으로의 필드 값을 읽을로 설정 된 요소는 `Request.Form` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-200">The `value` attribute of the `<input>` elements has been set to dynamically read the field value out of the `Request.Form` object.</span></span> <span data-ttu-id="c2ca5-201">처음으로 페이지를 요청 하는 값은 `Request.Form` 개체 모두 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-201">The first time that the page is requested, the values in the `Request.Form` object are all empty.</span></span> <span data-ttu-id="c2ca5-202">이런 방식으로 폼 비어 있습니다. 때문에 이것이 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-202">This is fine, because that way the form is blank.</span></span>
2. <span data-ttu-id="c2ca5-203">브라우저에서 페이지를 시작, 폼 필드에 또는 해당 비워 놓고 클릭 **전송**합니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-203">Launch the page in your browser, fill in the form fields or leave them blank, and click **Submit**.</span></span> <span data-ttu-id="c2ca5-204">제출 된 값을 보여 주는 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2ca5-204">A page that shows the submitted values is displayed.</span></span>

    ![폼 5](4-working-with-forms/_static/image5.jpg)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="c2ca5-206">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="c2ca5-206">Additional Resources</span></span>

- [<span data-ttu-id="c2ca5-207">웹 사용자의 입력에 1,001 방법</span><span class="sxs-lookup"><span data-stu-id="c2ca5-207">1,001 Ways to Get Input from Web Users</span></span>](https://msdn.microsoft.com/en-us/library/ms971057.aspx)
- <span data-ttu-id="c2ca5-208">[폼을 사용 하 고 사용자 입력 처리](https://msdn.microsoft.com/en-us/library/ms525182(VS.90).aspx)</span><span class="sxs-lookup"><span data-stu-id="c2ca5-208">[Using Forms and Processing User Input](https://msdn.microsoft.com/en-us/library/ms525182(VS.90).aspx)</span></span>
- [<span data-ttu-id="c2ca5-209">ASP.NET 웹 페이지 사이트에서 사용자 입력 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="c2ca5-209">Validating User Input in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=253002)
- <span data-ttu-id="c2ca5-210">[HTML 폼에서 자동 완성 사용](https://msdn.microsoft.com/en-us/library/ms533032(VS.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="c2ca5-210">[Using AutoComplete in HTML Forms](https://msdn.microsoft.com/en-us/library/ms533032(VS.85).aspx)</span></span>
