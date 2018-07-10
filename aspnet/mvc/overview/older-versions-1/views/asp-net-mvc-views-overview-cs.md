---
uid: mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-cs
title: ASP.NET MVC 보기 개요 (C#) | Microsoft Docs
author: StephenWalther
description: ASP.NET MVC 뷰를 무엇이 고 HTML 페이지에서와 어떻게 합니까? 이 자습서에서는 Stephen walther가 보기 소개 하 고 t 하는 방법을 보여 줍니다....
ms.author: aspnetcontent
ms.date: 02/16/2008
ms.assetid: 152ab1e5-aec2-4ea7-b8cc-27a24dd9acb8
msc.legacyurl: /mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-cs
msc.type: authoredcontent
ms.openlocfilehash: d2fc96f7e991dd7c4e0b3e9ff5c589c1075010ac
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37833661"
---
<a name="aspnet-mvc-views-overview-c"></a><span data-ttu-id="89857-104">ASP.NET MVC 보기 개요 (C#)</span><span class="sxs-lookup"><span data-stu-id="89857-104">ASP.NET MVC Views Overview (C#)</span></span>
====================
<span data-ttu-id="89857-105">[Stephen walther가](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="89857-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="89857-106">ASP.NET MVC 뷰를 무엇이 고 HTML 페이지에서와 어떻게 합니까?</span><span class="sxs-lookup"><span data-stu-id="89857-106">What is an ASP.NET MVC View and how does it differ from a HTML page?</span></span> <span data-ttu-id="89857-107">이 자습서에서는 Stephen walther가 보기 소개 하 고 데이터 보기 및 보기 내에서 HTML 도우미 활용을 걸릴 수 있습니다 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="89857-107">In this tutorial, Stephen Walther introduces you to Views and demonstrates how you can take advantage of View Data and HTML Helpers within a View.</span></span>


<span data-ttu-id="89857-108">이 자습서의 목적은 ASP.NET MVC 뷰, 데이터 보기 및 HTML 도우미에 대 한 간략 한 소개를 제공 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="89857-108">The purpose of this tutorial is to provide you with a brief introduction to ASP.NET MVC views, view data, and HTML Helpers.</span></span> <span data-ttu-id="89857-109">이 자습서를 마치면 새 보기 만들기, 보기를 컨트롤러에서 데이터를 전달 및 HTML 도우미를 사용 하 여 보기에 콘텐츠를 생성 하는 방법을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-109">By the end of this tutorial, you should understand how to create new views, pass data from a controller to a view, and use HTML Helpers to generate content in a view.</span></span>

## <a name="understanding-views"></a><span data-ttu-id="89857-110">뷰 이해</span><span class="sxs-lookup"><span data-stu-id="89857-110">Understanding Views</span></span>

<span data-ttu-id="89857-111">Active Server Pages, ASP.NET에 대 한 ASP.NET MVC 포함 되어 있지는 페이지에 직접 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-111">For ASP.NET or Active Server Pages, ASP.NET MVC does not include anything that directly corresponds to a page.</span></span> <span data-ttu-id="89857-112">ASP.NET MVC 응용 프로그램에서 않습니다 페이지 브라우저의 주소 표시줄에 입력 된 URL의 경로에 해당 하는 디스크.</span><span class="sxs-lookup"><span data-stu-id="89857-112">In an ASP.NET MVC application, there is not a page on disk that corresponds to the path in the URL that you type into the address bar of your browser.</span></span> <span data-ttu-id="89857-113">ASP.NET MVC 응용 프로그램의 페이지에 가깝습니다는 호출을 *보기*합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-113">The closest thing to a page in an ASP.NET MVC application is something called a *view*.</span></span>

<span data-ttu-id="89857-114">ASP.NET MVC 응용 프로그램, 들어오는 브라우저 요청 컨트롤러 작업에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="89857-114">ASP.NET MVC application, incoming browser requests are mapped to controller actions.</span></span> <span data-ttu-id="89857-115">컨트롤러 작업 보기를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-115">A controller action might return a view.</span></span> <span data-ttu-id="89857-116">그러나 컨트롤러 작업을 다른 유형의 다른 컨트롤러 작업으로 리디렉션하는 중 등의 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-116">However, a controller action might perform some other type of action such as redirecting you to another controller action.</span></span>

<span data-ttu-id="89857-117">목록 1 HomeController 라는 간단한 컨트롤러가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-117">Listing 1 contains a simple controller named the HomeController.</span></span> <span data-ttu-id="89857-118">HomeController는 index () 및 Details() 라는 두 개의 컨트롤러 작업을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-118">The HomeController exposes two controller actions named Index() and Details().</span></span>

<span data-ttu-id="89857-119">**1-HomeController.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="89857-119">**Listing 1 - HomeController.cs**</span></span>

[!code-csharp[Main](asp-net-mvc-views-overview-cs/samples/sample1.cs)]

<span data-ttu-id="89857-120">브라우저 주소 표시줄에 다음 URL을 입력 하 여 첫 번째 작업, index () 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-120">You can invoke the first action, the Index() action, by typing the following URL into your browser address bar:</span></span>

<span data-ttu-id="89857-121">/ Home/Index</span><span class="sxs-lookup"><span data-stu-id="89857-121">/Home/Index</span></span>

<span data-ttu-id="89857-122">브라우저에이 주소를 입력 하 여 두 번째 작업에서 Details() 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-122">You can invoke the second action, the Details() action, by typing this address into your browser:</span></span>

<span data-ttu-id="89857-123">/ Home/세부 정보</span><span class="sxs-lookup"><span data-stu-id="89857-123">/Home/Details</span></span>

<span data-ttu-id="89857-124">Index () 작업에는 뷰를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-124">The Index() action returns a view.</span></span> <span data-ttu-id="89857-125">사용자가 만든 대부분의 작업 보기를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-125">Most actions that you create will return views.</span></span> <span data-ttu-id="89857-126">그러나 작업은 다른 유형의 작업 결과 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-126">However, an action can return other types of action results.</span></span> <span data-ttu-id="89857-127">예를 들어 Details() 작업 index () 작업으로 들어오는 요청을 리디렉션하는 RedirectToActionResult를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-127">For example, the Details() action returns a RedirectToActionResult that redirects incoming request to the Index() action.</span></span>

<span data-ttu-id="89857-128">다음 코드 줄이 줄을 포함 하는 index () 작업:</span><span class="sxs-lookup"><span data-stu-id="89857-128">The Index() action contains the following single line of code:</span></span>

<span data-ttu-id="89857-129">View();</span><span class="sxs-lookup"><span data-stu-id="89857-129">View();</span></span>

<span data-ttu-id="89857-130">이 코드 줄을 웹 서버에서 다음 경로 있어야 하는 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-130">This line of code returns a view that must be located at the following path on your web server:</span></span>

<span data-ttu-id="89857-131">\Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="89857-131">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="89857-132">뷰에 대 한 경로 컨트롤러의 이름 및 컨트롤러 작업의 이름에서 유추 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89857-132">The path to the view is inferred from the name of the controller and the name of the controller action.</span></span>

<span data-ttu-id="89857-133">원하는 경우 뷰에 대 한 명시적 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-133">If you prefer, you can be explicit about the view.</span></span> <span data-ttu-id="89857-134">다음 코드 줄에 Fred 라는 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-134">The following line of code returns a view named Fred :</span></span>

<span data-ttu-id="89857-135">보기 (Fred);</span><span class="sxs-lookup"><span data-stu-id="89857-135">View( Fred );</span></span>

<span data-ttu-id="89857-136">이 코드 줄이 실행 되 면 뷰는 다음 경로에서 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89857-136">When this line of code is executed, a view is returned from the following path:</span></span>

<span data-ttu-id="89857-137">\Views\Home\Fred.aspx</span><span class="sxs-lookup"><span data-stu-id="89857-137">\Views\Home\Fred.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="89857-138">ASP.NET MVC 응용 프로그램에 대 한 단위 테스트를 만들 계획인 경우 다음 것 뷰 이름에 대 한 명시적 이어야 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-138">If you plan to create unit tests for your ASP.NET MVC application then it is a good idea to be explicit about view names.</span></span> <span data-ttu-id="89857-139">이런 방식으로 필요한 뷰 컨트롤러 작업에 의해 반환 된 확인 하기 위한 단위 테스트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-139">That way, you can create a unit test to verify that the expected view was returned by a controller action.</span></span>


## <a name="adding-content-to-a-view"></a><span data-ttu-id="89857-140">보기에 콘텐츠 추가</span><span class="sxs-lookup"><span data-stu-id="89857-140">Adding Content to a View</span></span>

<span data-ttu-id="89857-141">뷰는 (X) 스크립트를 포함할 수 있는 HTML 문서 표준.</span><span class="sxs-lookup"><span data-stu-id="89857-141">A view is a standard (X)HTML document that can contain scripts.</span></span> <span data-ttu-id="89857-142">스크립트를 사용 하 여 동적 콘텐츠 뷰를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-142">You use scripts to add dynamic content to a view.</span></span>

<span data-ttu-id="89857-143">예를 들어 목록 2에서 뷰는 현재 날짜 및 시간을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-143">For example, the view in Listing 2 displays the current date and time.</span></span>

<span data-ttu-id="89857-144">**2-나열 \Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="89857-144">**Listing 2 - \Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample2.aspx)]

<span data-ttu-id="89857-145">목록 2에서 HTML 페이지의 본문에 다음 스크립트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-145">Notice that the body of the HTML page in Listing 2 contains the following script:</span></span>

<span data-ttu-id="89857-146">&lt;% Response.Write(DateTime.Now);%&gt;</span><span class="sxs-lookup"><span data-stu-id="89857-146">&lt;% Response.Write(DateTime.Now);%&gt;</span></span>

<span data-ttu-id="89857-147">스크립트 구분 기호를 사용할 &lt;% 및 %&gt; 스크립트의 시작과 끝을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-147">You use the script delimiters &lt;% and %&gt; to mark the beginning and end of a script.</span></span> <span data-ttu-id="89857-148">이 스크립트는 C#으로 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89857-148">This script is written in C#.</span></span> <span data-ttu-id="89857-149">브라우저에 콘텐츠를 렌더링 response.write () 메서드를 호출 하 여 현재 날짜 및 시간이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89857-149">It displays the current date and time by calling the Response.Write() method to render content to the browser.</span></span> <span data-ttu-id="89857-150">스크립트 구분 기호 &lt;% 및 %&gt; 하나 이상의 문을 실행 하기 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-150">The script delimiters &lt;% and %&gt; can be used to execute one or more statements.</span></span>

<span data-ttu-id="89857-151">Response.write ()를 자주 호출 되므로 Microsoft 제공 바로 가기를 사용 하 여 response.write () 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-151">Since you call Response.Write() so often, Microsoft provides you with a shortcut for calling the Response.Write() method.</span></span> <span data-ttu-id="89857-152">구분 기호를 사용 하는 목록 3 뷰 &lt;% = %&gt; response.write () 호출에 대 한 바로 가기로 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-152">The view in Listing 3 uses the delimiters &lt;%= and %&gt; as a shortcut for calling Response.Write().</span></span>

<span data-ttu-id="89857-153">**Listing 3 - Views\Home\Index2.aspx**</span><span class="sxs-lookup"><span data-stu-id="89857-153">**Listing 3 - Views\Home\Index2.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample3.aspx)]

<span data-ttu-id="89857-154">보기에서 동적 콘텐츠를 생성 하려면 모든.NET 언어를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-154">You can use any .NET language to generate dynamic content in a view.</span></span> <span data-ttu-id="89857-155">일반적으로 안내 컨트롤러와 보기를 쓸 Visual Basic.NET 또는 C#을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-155">Normally, you�ll use either Visual Basic .NET or C# to write your controllers and views.</span></span>

## <a name="using-html-helpers-to-generate-view-content"></a><span data-ttu-id="89857-156">HTML 도우미를 사용 하 여 콘텐츠 보기를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-156">Using HTML Helpers to Generate View Content</span></span>

<span data-ttu-id="89857-157">쉽게 콘텐츠 뷰를 추가 하면 활용 이라는 것을 *HTML 도우미*합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-157">To make it easier to add content to a view, you can take advantage of something called an *HTML Helper*.</span></span> <span data-ttu-id="89857-158">일반적으로 HTML 도우미는 문자열을 생성 하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="89857-158">An HTML Helper, typically, is a method that generates a string.</span></span> <span data-ttu-id="89857-159">텍스트 상자, 링크, 드롭다운 목록, 목록 상자 등 표준 HTML 요소를 생성 하려면 HTML 도우미를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-159">You can use HTML Helpers to generate standard HTML elements such as textboxes, links, dropdown lists, and list boxes.</span></span>

<span data-ttu-id="89857-160">예를 들어 3 명의 HTML 도우미-활용 4 뷰 BeginForm(), TextBox() 및 Password() 도우미-로그인을 생성 하려면 (그림 1 참조)를 형성 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-160">For example, the view in Listing 4 takes advantage of three HTML Helpers -- the BeginForm(), the TextBox() and Password() helpers -- to generate a Login form (see Figure 1).</span></span>

<span data-ttu-id="89857-161">**Listing 4 -- \Views\Home\Login.aspx**</span><span class="sxs-lookup"><span data-stu-id="89857-161">**Listing 4 -- \Views\Home\Login.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample4.aspx)]


<span data-ttu-id="89857-162">[![새 프로젝트 대화 상자](asp-net-mvc-views-overview-cs/_static/image1.jpg)](asp-net-mvc-views-overview-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="89857-162">[![The New Project dialog box](asp-net-mvc-views-overview-cs/_static/image1.jpg)](asp-net-mvc-views-overview-cs/_static/image1.png)</span></span>

<span data-ttu-id="89857-163">**그림 01**: 표준 로그인 폼 ([큰 이미지를 보려면 클릭](asp-net-mvc-views-overview-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="89857-163">**Figure 01**: A standard Login form ([Click to view full-size image](asp-net-mvc-views-overview-cs/_static/image2.png))</span></span>


<span data-ttu-id="89857-164">HTML 도우미 메서드의 모든 뷰의 Html 속성 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-164">All of the HTML Helpers methods are called on the Html property of the view.</span></span> <span data-ttu-id="89857-165">예를 들어 Html.TextBox() 메서드를 호출 하 여 텍스트를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-165">For example, you render a TextBox by calling the Html.TextBox() method.</span></span>

<span data-ttu-id="89857-166">스크립트 구분 기호를 사용 하는 공지 &lt;% = %&gt; Html.TextBox()와 Html.Password() 도우미를 호출 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="89857-166">Notice that you use the script delimiters &lt;%= and %&gt; when calling both the Html.TextBox() and Html.Password() helpers.</span></span> <span data-ttu-id="89857-167">이러한 도우미는 단순히 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-167">These helpers simply return a string.</span></span> <span data-ttu-id="89857-168">브라우저에 문자열을 렌더링 하기 위해 response.write () 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-168">You need to call Response.Write() in order to render the string to the browser.</span></span>

<span data-ttu-id="89857-169">HTML 도우미 메서드를 사용 하는 것은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="89857-169">Using HTML Helper methods is optional.</span></span> <span data-ttu-id="89857-170">이러한 쉽게 HTML과 스크립트를 작성 해야 하는 양을 줄여 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-170">They make your life easier by reducing the amount of HTML and script that you need to write.</span></span> <span data-ttu-id="89857-171">목록 5에서 뷰는 HTML 도우미를 사용 하지 않고 4의 보기와 정확히 동일한 폼을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-171">The view in Listing 5 renders the exact same form as the view in Listing 4 without using HTML Helpers.</span></span>

<span data-ttu-id="89857-172">**Listing 5 -- \Views\Home\Login.aspx**</span><span class="sxs-lookup"><span data-stu-id="89857-172">**Listing 5 -- \Views\Home\Login.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample5.aspx)]

<span data-ttu-id="89857-173">사용자 고유의 HTML 도우미를 만들 수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-173">You also have the option of creating your own HTML Helpers.</span></span> <span data-ttu-id="89857-174">예를 들어, HTML 테이블에서 데이터베이스 레코드 집합을 자동으로 표시 하는 GridView() 도우미 메서드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-174">For example, you can create a GridView() helper method that displays a set of database records in an HTML table automatically.</span></span> <span data-ttu-id="89857-175">이 항목에서는 자습서에서 살펴봅니다 **사용자 지정 HTML 도우미 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-175">We explore this topic in the tutorial **Creating Custom HTML Helpers**.</span></span>

## <a name="using-view-data-to-pass-data-to-a-view"></a><span data-ttu-id="89857-176">뷰 데이터를 사용 하 여 보기로 데이터 전달</span><span class="sxs-lookup"><span data-stu-id="89857-176">Using View Data to Pass Data to a View</span></span>

<span data-ttu-id="89857-177">데이터 보기를 사용 하 여 컨트롤러에서 보기로 데이터를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-177">You use view data to pass data from a controller to a view.</span></span> <span data-ttu-id="89857-178">메일을 통해 전송 되는 패키지와 같은 데이터 보기 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-178">Think of view data like a package that you send through the mail.</span></span> <span data-ttu-id="89857-179">이 패키지를 사용 하 여 컨트롤러에서 보기로 전달 된 모든 데이터를 전송 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-179">All data passed from a controller to a view must be sent using this package.</span></span> <span data-ttu-id="89857-180">예를 들어 목록 6의 컨트롤러 데이터를 보려면 메시지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-180">For example, the controller in Listing 6 adds a message to view data.</span></span>

<span data-ttu-id="89857-181">**6-ProductController.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="89857-181">**Listing 6 - ProductController.cs**</span></span>

[!code-csharp[Main](asp-net-mvc-views-overview-cs/samples/sample6.cs)]

<span data-ttu-id="89857-182">ViewData 속성이 컨트롤러 이름 및 값 쌍의 컬렉션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="89857-182">The controller ViewData property represents a collection of name and value pairs.</span></span> <span data-ttu-id="89857-183">목록 6 index () 메서드는 값이 Hello World 메시지를 명명 된 뷰 데이터 컬렉션에 항목을 추가!.</span><span class="sxs-lookup"><span data-stu-id="89857-183">In Listing 6, the Index() method adds an item to the view data collection named message with the value Hello World!.</span></span> <span data-ttu-id="89857-184">뷰는 index () 메서드에 의해 반환 되 면 뷰 데이터를 자동으로 뷰로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89857-184">When the view is returned by the Index() method, the view data is passed to the view automatically.</span></span>

<span data-ttu-id="89857-185">7 목록 뷰 데이터 보기에서에서 메시지를 검색 하 고 브라우저에 메시지를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-185">The view in Listing 7 retrieves the message from the view data and renders the message to the browser.</span></span>

<span data-ttu-id="89857-186">**7-나열 \Views\Product\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="89857-186">**Listing 7 -- \Views\Product\Index.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-cs/samples/sample7.aspx)]

<span data-ttu-id="89857-187">뷰를 활용 한다는 Html.Encode() HTML 도우미 메서드는 메시지를 렌더링할 때 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-187">Notice that the view takes advantage of the Html.Encode() HTML Helper method when rendering the message.</span></span> <span data-ttu-id="89857-188">Html.Encode() HTML 도우미와 같은 특수 문자를 인코딩합니다 &lt; 고 &gt; 안전한 웹 페이지에 표시할 문자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-188">The Html.Encode() HTML Helper encodes special characters such as &lt; and &gt; into characters that are safe to display in a web page.</span></span> <span data-ttu-id="89857-189">사용자가 웹 사이트에 제출 하는 콘텐츠를 렌더링할 때마다 JavaScript 주입 공격을 방지 하기 위해 콘텐츠를 인코딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-189">Whenever you render content that a user submits to a website, you should encode the content to prevent JavaScript injection attacks.</span></span>

<span data-ttu-id="89857-190">(만들었기 때문에 메시지를 직접 여 ProductController에서, 우리가 인할 실제로 메시지를 인코딩하는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-190">(Because we created the message ourselves in the ProductController, we don�t really need to encode the message.</span></span> <span data-ttu-id="89857-191">그러나는 것이 뷰 내에서 데이터 보기에서에서 검색 콘텐츠를 표시 하는 경우 항상 Html.Encode() 메서드를 호출 하는 좋은 습관입니다.)</span><span class="sxs-lookup"><span data-stu-id="89857-191">However, it is a good habit to always call the Html.Encode() method when displaying content retrieved from view data within a view.)</span></span>

<span data-ttu-id="89857-192">7 목록 보기 컨트롤러에서 단순 문자열 메시지를 전달 하는 뷰 데이터를 활용을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-192">In Listing 7, we took advantage of view data to pass a simple string message from a controller to a view.</span></span> <span data-ttu-id="89857-193">다른 유형의 데이터베이스 레코드 보기 컨트롤러에서 컬렉션과 같은 데이터를 전달할 데이터 보기를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-193">You also can use view data to pass other types of data, such as a collection of database records, from a controller to a view.</span></span> <span data-ttu-id="89857-194">예를 들어 데이터베이스의 컬렉션을 전달 하는 제품 데이터베이스 테이블의 내용을 보기에 표시 하려는 경우 보기에 데이터 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-194">For example, if you want to display the contents of the Products database table in a view, then you would pass the collection of database records in view data.</span></span>

<span data-ttu-id="89857-195">컨트롤러에서 보기로 강력한 형식의 뷰 데이터를 전달할 수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-195">You also have the option of passing strongly typed view data from a controller to a view.</span></span> <span data-ttu-id="89857-196">이 항목에서는 자습서에서 살펴봅니다 **이해 강력한 형식의 뷰 데이터 뷰와**합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-196">We explore this topic in the tutorial **Understanding Strongly Typed View Data and Views**.</span></span>

## <a name="summary"></a><span data-ttu-id="89857-197">요약</span><span class="sxs-lookup"><span data-stu-id="89857-197">Summary</span></span>

<span data-ttu-id="89857-198">이 자습서는 ASP.NET MVC 뷰, 데이터 보기 및 HTML 도우미에 대 한 간략 한 소개를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="89857-198">This tutorial provided a brief introduction to ASP.NET MVC views, view data, and HTML Helpers.</span></span> <span data-ttu-id="89857-199">첫 번째 섹션에서는 프로젝트에 새 뷰를 추가 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-199">In the first section, you learned how to add new views to your project.</span></span> <span data-ttu-id="89857-200">추가 해야 뷰 오른쪽 폴더로 특정 컨트롤러에서 호출 하기 위해 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-200">You learned that you must add a view to the right folder in order to call it from a particular controller.</span></span> <span data-ttu-id="89857-201">다음으로, HTML 도우미의 항목에 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-201">Next, we discussed the topic of HTML Helpers.</span></span> <span data-ttu-id="89857-202">HTML 도우미 표준 HTML 콘텐츠를 쉽게 생성할 수 있도록 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-202">You learned how HTML Helpers enable you to easily generate standard HTML content.</span></span> <span data-ttu-id="89857-203">마지막으로, 컨트롤러에서 보기로 데이터를 전달 하는 뷰 데이터를 활용 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="89857-203">Finally, you learned how to take advantage of view data to pass data from a controller to a view.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="89857-204">다음</span><span class="sxs-lookup"><span data-stu-id="89857-204">Next</span></span>](creating-custom-html-helpers-cs.md)
