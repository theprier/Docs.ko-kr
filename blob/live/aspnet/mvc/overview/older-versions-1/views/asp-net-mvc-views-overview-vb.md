---
uid: mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
title: "ASP.NET MVC 뷰 개요 (VB) | Microsoft Docs"
author: StephenWalther
description: "ASP.NET MVC 뷰 란 무엇이 고 어떻게 다른 것 일까요 HTML 페이지에서? 이 자습서에서는 Stephen Walther에서는 보기에 소개 하 고 t 하는 방법을 보여 줍니다. 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/16/2008
ms.topic: article
ms.assetid: c28ba88d-3a93-47f5-a306-049bd766714d
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: c85b969aa4457d0326b4a16da218db9e11d01e10
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-mvc-views-overview-vb"></a><span data-ttu-id="497db-104">ASP.NET MVC 뷰 (VB) 개요</span><span class="sxs-lookup"><span data-stu-id="497db-104">ASP.NET MVC Views Overview (VB)</span></span>
====================
<span data-ttu-id="497db-105">으로 [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="497db-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="497db-106">ASP.NET MVC 뷰 란 무엇이 고 어떻게 다른 것 일까요 HTML 페이지에서?</span><span class="sxs-lookup"><span data-stu-id="497db-106">What is an ASP.NET MVC View and how does it differ from a HTML page?</span></span> <span data-ttu-id="497db-107">이 자습서에서는 Stephen Walther 보기에 소개 하 고 있습니다 사용할 수 있는 방법을 데이터 보기와 보기 내에서 HTML 도우미 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="497db-107">In this tutorial, Stephen Walther introduces you to Views and demonstrates how you can take advantage of View Data and HTML Helpers within a View.</span></span>


<span data-ttu-id="497db-108">이 자습서의 목적은 ASP.NET MVC 뷰, 데이터 보기 및 HTML 도우미에 대 한 간략 한 소개를 제공 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="497db-108">The purpose of this tutorial is to provide you with a brief introduction to ASP.NET MVC views, view data, and HTML Helpers.</span></span> <span data-ttu-id="497db-109">이 자습서를 마치면 하 여 새 보기를 만들 컨트롤러에서 뷰로 데이터를 전달 하 고 콘텐츠를 생성 하는 뷰에서 HTML 도우미를 사용 하는 방법을 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-109">By the end of this tutorial, you should understand how to create new views, pass data from a controller to a view, and use HTML Helpers to generate content in a view.</span></span>

## <a name="understanding-views"></a><span data-ttu-id="497db-110">뷰 이해</span><span class="sxs-lookup"><span data-stu-id="497db-110">Understanding Views</span></span>

<span data-ttu-id="497db-111">ASP.NET 또는 Active Server Pages 달리 ASP.NET MVC는 제외 페이지에 직접 해당 하는 아무 것도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="497db-111">Unlike ASP.NET or Active Server Pages, ASP.NET MVC does not include anything that directly corresponds to a page.</span></span> <span data-ttu-id="497db-112">ASP.NET MVC 응용 프로그램 즉 하지 페이지를 브라우저의 주소 표시줄에 입력 하는 URL의 경로에 해당 하는 디스크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-112">In an ASP.NET MVC application, there is not a page on disk that corresponds to the path in the URL that you type into the address bar of your browser.</span></span> <span data-ttu-id="497db-113">ASP.NET MVC 응용 프로그램의 페이지에 가깝습니다 리 라는 *보기*합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-113">The closest thing to a page in an ASP.NET MVC application is something called a *view*.</span></span>

<span data-ttu-id="497db-114">ASP.NET MVC 응용 프로그램에서 들어오는 브라우저 요청 컨트롤러 작업에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="497db-114">In an ASP.NET MVC application, incoming browser requests are mapped to controller actions.</span></span> <span data-ttu-id="497db-115">컨트롤러 작업 보기를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-115">A controller action might return a view.</span></span> <span data-ttu-id="497db-116">그러나 컨트롤러 작업이 일부 다른 형식의 다른 컨트롤러 작업 리디렉션됩니다 등의 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-116">However, a controller action might perform some other type of action such as redirecting you to another controller action.</span></span>

<span data-ttu-id="497db-117">목록 1 HomeController 라는 간단한 컨트롤러를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-117">Listing 1 contains a simple controller named the HomeController.</span></span> <span data-ttu-id="497db-118">HomeController는 index () 및 Details() 라는 두 개의 컨트롤러 작업을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-118">The HomeController exposes two controller actions named Index() and Details().</span></span>

<span data-ttu-id="497db-119">**1-HomeController.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="497db-119">**Listing 1 - HomeController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample1.vb)]

<span data-ttu-id="497db-120">브라우저 주소 표시줄에 다음 URL을 입력 하 여 첫 번째 동작인 index () 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-120">You can invoke the first action, the Index() action, by typing the following URL into your browser address bar:</span></span>

<span data-ttu-id="497db-121">/ Home/Index</span><span class="sxs-lookup"><span data-stu-id="497db-121">/Home/Index</span></span>

<span data-ttu-id="497db-122">브라우저에이 주소를 입력 하 여 두 번째 작업에서 Details() 동작을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-122">You can invoke the second action, the Details() action, by typing this address into your browser:</span></span>

<span data-ttu-id="497db-123">/ Home/세부 정보</span><span class="sxs-lookup"><span data-stu-id="497db-123">/Home/Details</span></span>

<span data-ttu-id="497db-124">Index () 작업 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-124">The Index() action returns a view.</span></span> <span data-ttu-id="497db-125">만드는 대부분의 동작 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-125">Most actions that you create will return views.</span></span> <span data-ttu-id="497db-126">그러나 작업은 다른 유형의 작업 결과 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-126">However, an action can return other types of action results.</span></span> <span data-ttu-id="497db-127">예를 들어 Details() 작업 index () 작업으로 들어오는 요청을 리디렉션하는 RedirectToActionResult를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-127">For example, the Details() action returns a RedirectToActionResult that redirects incoming request to the Index() action.</span></span>

<span data-ttu-id="497db-128">Index () 작업에 다음 줄을의 코드 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-128">The Index() action contains the following single line of code:</span></span>

<span data-ttu-id="497db-129">View()</span><span class="sxs-lookup"><span data-stu-id="497db-129">View()</span></span>

<span data-ttu-id="497db-130">이 코드 줄을 웹 서버에서 다음 경로에 있어야 하는 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-130">This line of code returns a view that must be located at the following path on your web server:</span></span>

<span data-ttu-id="497db-131">\Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="497db-131">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="497db-132">뷰에 대 한 경로 컨트롤러의 이름 및 컨트롤러 동작의 이름에서 유추 됩니다.</span><span class="sxs-lookup"><span data-stu-id="497db-132">The path to the view is inferred from the name of the controller and the name of the controller action.</span></span>

<span data-ttu-id="497db-133">원하는 경우 뷰에 대 한 명시적을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-133">If you prefer, you can be explicit about the view.</span></span> <span data-ttu-id="497db-134">다음 코드 줄 Fred 이라는 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-134">The following line of code returns a view named Fred :</span></span>

<span data-ttu-id="497db-135">보기 (Fred)</span><span class="sxs-lookup"><span data-stu-id="497db-135">View( Fred )</span></span>

<span data-ttu-id="497db-136">이 줄의 코드를 실행 하면 다음 경로에서 뷰 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="497db-136">When this line of code is executed, a view is returned from the following path:</span></span>

<span data-ttu-id="497db-137">\Views\Home\Fred.aspx</span><span class="sxs-lookup"><span data-stu-id="497db-137">\Views\Home\Fred.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="497db-138">ASP.NET MVC 응용 프로그램에 대 한 단위 테스트를 만들려고 계획 하는 경우 다음 이기 뷰 이름에 대 한 명시적으로 지정 해야 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-138">If you plan to create unit tests for your ASP.NET MVC application then it is a good idea to be explicit about view names.</span></span> <span data-ttu-id="497db-139">이런 방식으로 예상된 보기 컨트롤러 동작에 의해 반환 된 것을 확인 하는 단위 테스트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-139">That way, you can create a unit test to verify that the expected view was returned by a controller action.</span></span>


## <a name="adding-content-to-a-view"></a><span data-ttu-id="497db-140">콘텐츠 뷰를 추가</span><span class="sxs-lookup"><span data-stu-id="497db-140">Adding Content to a View</span></span>

<span data-ttu-id="497db-141">뷰는 (스크립트를 포함할 수 있는 HTML 문서 X) 표준입니다.</span><span class="sxs-lookup"><span data-stu-id="497db-141">A view is a standard (X)HTML document that can contain scripts.</span></span> <span data-ttu-id="497db-142">스크립트를 사용 하 여 동적 콘텐츠 보기에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-142">You use scripts to add dynamic content to a view.</span></span>

<span data-ttu-id="497db-143">예를 들어 목록 2는 보기는 현재 날짜 및 시간을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-143">For example, the view in Listing 2 displays the current date and time.</span></span>

<span data-ttu-id="497db-144">**2-나열 \Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="497db-144">**Listing 2 - \Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample2.aspx)]

<span data-ttu-id="497db-145">다음 스크립트는 목록 2에 있는 HTML 페이지의 본문에 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-145">Notice that the body of the HTML page in Listing 2 contains the following script:</span></span>

<span data-ttu-id="497db-146">&lt;% Response.Write(DateTime.Now) %&gt;</span><span class="sxs-lookup"><span data-stu-id="497db-146">&lt;% Response.Write(DateTime.Now)%&gt;</span></span>

<span data-ttu-id="497db-147">스크립트 구분 기호를 사용 하 여 &lt;% 및 %&gt; 스크립트의 시작과 끝을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-147">You use the script delimiters &lt;% and %&gt; to mark the beginning and end of a script.</span></span> <span data-ttu-id="497db-148">이 스크립트는 Visual basic로 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="497db-148">This script is written in Visual basic.</span></span> <span data-ttu-id="497db-149">내용을 브라우저에 렌더링 하 Response.Write() 메서드를 호출 하 여 현재 날짜 및 시간을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-149">It displays the current date and time by calling the Response.Write() method to render content to the browser.</span></span> <span data-ttu-id="497db-150">스크립트 구분 기호 &lt;% 및 %&gt; 는 하나 이상의 문을 실행 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-150">The script delimiters &lt;% and %&gt; can be used to execute one or more statements.</span></span>

<span data-ttu-id="497db-151">Response.Write()를 자주 호출할 수 있으므로 Microsoft 제공 바로 가기를 Response.Write() 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-151">Since you call Response.Write() so often, Microsoft provides you with a shortcut for calling the Response.Write() method.</span></span> <span data-ttu-id="497db-152">목록 3에서 보기의 구분 기호를 사용 하 여 &lt;% = %&gt; Response.Write() 호출에 대 한 바로 가기로 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-152">The view in Listing 3 uses the delimiters &lt;%= and %&gt; as a shortcut for calling Response.Write().</span></span>

<span data-ttu-id="497db-153">**3-Views\Home\Index2.aspx 나열**</span><span class="sxs-lookup"><span data-stu-id="497db-153">**Listing 3 - Views\Home\Index2.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample3.aspx)]

<span data-ttu-id="497db-154">동적 콘텐츠 보기에서 생성 하는 모든.NET 언어를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-154">You can use any .NET language to generate dynamic content in a view.</span></span> <span data-ttu-id="497db-155">일반적으로 ll 있습니다 컨트롤러와 뷰를 작성 하 Visual Basic.NET 또는 C#을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-155">Normally, you�ll use either Visual Basic .NET or C# to write your controllers and views.</span></span>

## <a name="using-html-helpers-to-generate-view-content"></a><span data-ttu-id="497db-156">HTML 도우미를 사용 하 여 콘텐츠 보기를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-156">Using HTML Helpers to Generate View Content</span></span>

<span data-ttu-id="497db-157">콘텐츠 뷰를 추가할 좀 더 쉽게 있습니다 활용할 수 라는 것는 *HTML 도우미*합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-157">To make it easier to add content to a view, you can take advantage of something called an *HTML Helper*.</span></span> <span data-ttu-id="497db-158">HTML 도우미, 문자열을 생성 하는 메서드를 일반적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-158">An HTML Helper, typically, is a method that generates a string.</span></span> <span data-ttu-id="497db-159">텍스트 상자, 링크, 드롭다운 목록, 목록 상자와 같은 표준 HTML 요소를 생성 하려면 HTML 도우미를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-159">You can use HTML Helpers to generate standard HTML elements such as textboxes, links, dropdown lists, and list boxes.</span></span>

<span data-ttu-id="497db-160">예를 들어 3 명의 HTML 도우미-활용 목록 4에서에서 보기 BeginForm(), TextBox() 및 Password() 도우미-로그인을 생성 하려면 (그림 1 참조)을 형성 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-160">For example, the view in Listing 4 takes advantage of three HTML Helpers -- the BeginForm(), the TextBox() and Password() helpers -- to generate a Login form (see Figure 1).</span></span>

<span data-ttu-id="497db-161">**4--나열 \Views\Home\Login.aspx**</span><span class="sxs-lookup"><span data-stu-id="497db-161">**Listing 4 -- \Views\Home\Login.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample4.aspx)]


<span data-ttu-id="497db-162">[![새 프로젝트 대화 상자](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="497db-162">[![The New Project dialog box](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)</span></span>

<span data-ttu-id="497db-163">**그림 01**: 표준 로그인 폼 ([전체 크기 이미지를 보려면 클릭](asp-net-mvc-views-overview-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="497db-163">**Figure 01**: A standard Login form ([Click to view full-size image](asp-net-mvc-views-overview-vb/_static/image2.png))</span></span>


<span data-ttu-id="497db-164">뷰의 Html 속성에서 모든 HTML 도우미 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-164">All of the HTML Helpers methods are called on the Html property of the view.</span></span> <span data-ttu-id="497db-165">예를 들어 Html.TextBox() 메서드를 호출 하 여 텍스트 상자를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-165">For example, you render a TextBox by calling the Html.TextBox() method.</span></span>

<span data-ttu-id="497db-166">스크립트 구분 기호를 사용 하는 알림 &lt;% = %&gt; Html.TextBox()와 Html.Password() 도우미를 호출할 때입니다.</span><span class="sxs-lookup"><span data-stu-id="497db-166">Notice that you use the script delimiters &lt;%= and %&gt; when calling both the Html.TextBox() and Html.Password() helpers.</span></span> <span data-ttu-id="497db-167">이러한 도우미 클래스는 단순히 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-167">These helpers simply return a string.</span></span> <span data-ttu-id="497db-168">브라우저에 문자열을 렌더링 하는 데 Response.Write()를 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-168">You need to call Response.Write() in order to render the string to the browser.</span></span>

<span data-ttu-id="497db-169">HTML 도우미 메서드를 사용 하는 것은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="497db-169">Using HTML Helper methods is optional.</span></span> <span data-ttu-id="497db-170">쉽게 단순화 하 여 HTML 및 스크립트를 작성 해야 하는 양이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="497db-170">They make your life easier by reducing the amount of HTML and script that you need to write.</span></span> <span data-ttu-id="497db-171">목록 5에서 보기는 HTML 도우미를 사용 하지 않고 목록 4의 보기와 정확히 같은 폼을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-171">The view in Listing 5 renders the exact same form as the view in Listing 4 without using HTML Helpers.</span></span>

<span data-ttu-id="497db-172">**5--나열 \Views\Home\Login.aspx**</span><span class="sxs-lookup"><span data-stu-id="497db-172">**Listing 5 -- \Views\Home\Login.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample5.aspx)]

<span data-ttu-id="497db-173">사용자 고유의 HTML 도우미를 만들을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-173">You also have the option of creating your own HTML Helpers.</span></span> <span data-ttu-id="497db-174">예를 들어 HTML 테이블에 데이터베이스 레코드 집합을 자동으로 표시 하는 GridView() 도우미 메서드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-174">For example, you can create a GridView() helper method that displays a set of database records in an HTML table automatically.</span></span> <span data-ttu-id="497db-175">자습서의이 항목을 탐색 **사용자 지정 HTML 도우미 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-175">We explore this topic in the tutorial **Creating Custom HTML Helpers**.</span></span>

## <a name="using-view-data-to-pass-data-to-a-view"></a><span data-ttu-id="497db-176">데이터 보기를 사용 하 여 데이터를 전달 하는 보기</span><span class="sxs-lookup"><span data-stu-id="497db-176">Using View Data to Pass Data to a View</span></span>

<span data-ttu-id="497db-177">데이터 보기를 사용 하 여 보기에는 컨트롤러에서 데이터를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-177">You use view data to pass data from a controller to a view.</span></span> <span data-ttu-id="497db-178">메일을 통해 전송 하는 패키지와 같이 데이터 보기 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-178">Think of view data like a package that you send through the mail.</span></span> <span data-ttu-id="497db-179">이 패키지를 사용 하 여 보기에는 컨트롤러에서 전달 된 모든 데이터를 전송 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-179">All data passed from a controller to a view must be sent using this package.</span></span> <span data-ttu-id="497db-180">예를 들어 컨트롤러 목록 6에 데이터를 보려면 메시지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-180">For example, the controller in Listing 6 adds a message to view data.</span></span>

<span data-ttu-id="497db-181">**6-ProductController.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="497db-181">**Listing 6 - ProductController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample6.vb)]

<span data-ttu-id="497db-182">컨트롤러 ViewData 속성 이름 / 값 쌍의 컬렉션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="497db-182">The controller ViewData property represents a collection of name and value pairs.</span></span> <span data-ttu-id="497db-183">목록 6 index () 메서드는 Hello World 값으로 메시지를 명명 된 뷰 데이터 컬렉션에 항목을 추가!입니다.</span><span class="sxs-lookup"><span data-stu-id="497db-183">In Listing 6, the Index() method adds an item to the view data collection named message with the value Hello World!.</span></span> <span data-ttu-id="497db-184">보기는 index () 메서드에 의해 반환 되 면 뷰 데이터 보기를 자동으로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="497db-184">When the view is returned by the Index() method, the view data is passed to the view automatically.</span></span>

<span data-ttu-id="497db-185">보기 목록 7의 데이터 보기에서에서 메시지를 검색 하 고 브라우저에 메시지를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-185">The view in Listing 7 retrieves the message from the view data and renders the message to the browser.</span></span>

<span data-ttu-id="497db-186">**7-나열 \Views\Product\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="497db-186">**Listing 7 -- \Views\Product\Index.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample7.aspx)]

<span data-ttu-id="497db-187">확인 메시지를 렌더링 하는 경우 보기에서는 Html.Encode() HTML 도우미 메서드를 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-187">Notice that the view takes advantage of the Html.Encode() HTML Helper method when rendering the message.</span></span> <span data-ttu-id="497db-188">Html.Encode() HTML 도우미와 같은 특수 문자를 인코딩합니다 &lt; 및 &gt; 웹 페이지에 표시 하기에 안전한 문자로 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-188">The Html.Encode() HTML Helper encodes special characters such as &lt; and &gt; into characters that are safe to display in a web page.</span></span> <span data-ttu-id="497db-189">사용자가 웹 사이트에 전송 하는 콘텐츠를 렌더링할 때마다 JavaScript 주입 공격을 방지 하기 위해 콘텐츠를 인코딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-189">Whenever you render content that a user submits to a website, you should encode the content to prevent JavaScript injection attacks.</span></span>

<span data-ttu-id="497db-190">(메시지 직접에서 만든는 ProductController, 때문에 여기서 인할 실제로 메시지를 인코딩하는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-190">(Because we created the message ourselves in the ProductController, we don�t really need to encode the message.</span></span> <span data-ttu-id="497db-191">그러나이 뷰 내의 데이터 보기에서에서 검색 콘텐츠를 표시 하는 경우 항상 Html.Encode() 메서드를 호출 하는 좋은 습관입니다.)</span><span class="sxs-lookup"><span data-stu-id="497db-191">However, it is a good habit to always call the Html.Encode() method when displaying content retrieved from view data within a view.)</span></span>

<span data-ttu-id="497db-192">목록 7에서의 순서로 보기 데이터를 보기에 컨트롤러에서 간단한 문자열 메시지를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-192">In Listing 7, we took advantage of view data to pass a simple string message from a controller to a view.</span></span> <span data-ttu-id="497db-193">다른 보기에는 컨트롤러에서 데이터베이스 레코드의 컬렉션과 같은 데이터 형식을 전달 하려면 데이터 보기를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-193">You also can use view data to pass other types of data, such as a collection of database records, from a controller to a view.</span></span> <span data-ttu-id="497db-194">예를 들어 데이터베이스의 컬렉션을 전달 하는 다음 제품 데이터베이스 테이블의 내용을 보기에 표시 하려는 경우 보기에 데이터 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-194">For example, if you want to display the contents of the Products database table in a view, then you would pass the collection of database records in view data.</span></span>

<span data-ttu-id="497db-195">또한 보기를 컨트롤러에서 강력한 형식의 뷰 데이터를 전달 하는 옵션도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-195">You also have the option of passing strongly typed view data from a controller to a view.</span></span> <span data-ttu-id="497db-196">자습서의이 항목을 탐색 **이해 강력한 형식의 뷰 데이터와 뷰**합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-196">We explore this topic in the tutorial **Understanding Strongly Typed View Data and Views**.</span></span>

## <a name="summary"></a><span data-ttu-id="497db-197">요약</span><span class="sxs-lookup"><span data-stu-id="497db-197">Summary</span></span>

<span data-ttu-id="497db-198">이 자습서에는 ASP.NET MVC 뷰, 데이터 보기 및 HTML 도우미에 대 한 간략 한 소개를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="497db-198">This tutorial provided a brief introduction to ASP.NET MVC views, view data, and HTML Helpers.</span></span> <span data-ttu-id="497db-199">첫 번째 섹션에서는 프로젝트에 새 보기를 추가 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-199">In the first section, you learned how to add new views to your project.</span></span> <span data-ttu-id="497db-200">특정 컨트롤러에서 호출 하기 위해 뷰를 추가에 적합 한 폴더 해야 한다고 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-200">You learned that you must add a view to the right folder in order to call it from a particular controller.</span></span> <span data-ttu-id="497db-201">다음으로, HTML 도우미의 주제에 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-201">Next, we discussed the topic of HTML Helpers.</span></span> <span data-ttu-id="497db-202">HTML 도우미 표준 HTML 콘텐츠를 쉽게 생성할 수 있도록 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-202">You learned how HTML Helpers enable you to easily generate standard HTML content.</span></span> <span data-ttu-id="497db-203">마지막으로, 보기에는 컨트롤러에서 데이터를 전달 하는 뷰 데이터를 활용 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="497db-203">Finally, you learned how to take advantage of view data to pass data from a controller to a view.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="497db-204">[이전](passing-data-to-view-master-pages-cs.md)
[다음](creating-custom-html-helpers-vb.md)</span><span class="sxs-lookup"><span data-stu-id="497db-204">[Previous](passing-data-to-view-master-pages-cs.md)
[Next](creating-custom-html-helpers-vb.md)</span></span>
