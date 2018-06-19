---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
title: 캐시 된 페이지 (C#)에 동적 콘텐츠 추가 | Microsoft Docs
author: microsoft
description: 같은 페이지의 동적 및 캐시 된 콘텐츠를 혼합 하는 방법을 알아봅니다. 캐시 후 대체 배너 광고 o 같은 동적 콘텐츠를 표시할 수 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: 2ddd4407-d143-4a94-877c-21771bfb97a6
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
msc.type: authoredcontent
ms.openlocfilehash: 9f91cc07bc531cfb3edf577ab79e91fd94a57a3c
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30868583"
---
<a name="adding-dynamic-content-to-a-cached-page-c"></a><span data-ttu-id="86f19-104">캐시 된 페이지 (C#)에 동적 콘텐츠 추가</span><span class="sxs-lookup"><span data-stu-id="86f19-104">Adding Dynamic Content to a Cached Page (C#)</span></span>
====================
<span data-ttu-id="86f19-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="86f19-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="86f19-106">같은 페이지의 동적 및 캐시 된 콘텐츠를 혼합 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-106">Learn how to mix dynamic and cached content in the same page.</span></span> <span data-ttu-id="86f19-107">캐시 후 대체 배너 보급 알림 또는 뉴스 항목 캐시 페이지 출력 된 변수가 있는 내에서 같은 동적 콘텐츠를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-107">Post-cache substitution enables you to display dynamic content, such as banner advertisements or news items, within a page that has been output cached.</span></span>


<span data-ttu-id="86f19-108">출력 캐싱을 활용 하기 위해, ASP.NET MVC 응용 프로그램의 성능을 크게 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-108">By taking advantage of output caching, you can dramatically improve the performance of an ASP.NET MVC application.</span></span> <span data-ttu-id="86f19-109">매번 페이지가 요청 될 페이지를 다시 생성 하는 대신 페이지 한 번만 생성 되어 여러 사용자에 대 한 메모리에 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-109">Instead of regenerating a page each and every time the page is requested, the page can be generated once and cached in memory for multiple users.</span></span>

<span data-ttu-id="86f19-110">하지만 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-110">But there is a problem.</span></span> <span data-ttu-id="86f19-111">페이지에 동적 콘텐츠를 표시 해야 하는 경우에 어떻게?</span><span class="sxs-lookup"><span data-stu-id="86f19-111">What if you need to display dynamic content in the page?</span></span> <span data-ttu-id="86f19-112">예를 들어 페이지에 배너 광고를 표시할 것인지 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-112">For example, imagine that you want to display a banner advertisement in the page.</span></span> <span data-ttu-id="86f19-113">모든 사용자가 동일한 광고를 볼 수 있도록 캐시 되도록 배너 광고가 되기를 원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-113">You don't want the banner advertisement to be cached so that every user sees the very same advertisement.</span></span> <span data-ttu-id="86f19-114">이런 방식으로 돈을 더를 확인 하지 않습니다!</span><span class="sxs-lookup"><span data-stu-id="86f19-114">You wouldn't make any money that way!</span></span>

<span data-ttu-id="86f19-115">다행히 쉬운 방법이입니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-115">Fortunately, there is an easy solution.</span></span> <span data-ttu-id="86f19-116">라는 ASP.NET 프레임 워크의 기능을 이용할 수 있습니다 *캐시 후 대체*합니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-116">You can take advantage of a feature of the ASP.NET framework called *post-cache substitution*.</span></span> <span data-ttu-id="86f19-117">캐시 후 대체를 사용 하면 메모리에 캐시 되어 있는 페이지의 동적 콘텐츠를 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-117">Post-cache substitution enables you to substitute dynamic content in a page that has been cached in memory.</span></span>


<span data-ttu-id="86f19-118">일반적으로 [OutputCache] 특성을 사용 하 여 캐시 된 페이지를 출력할 때 페이지는 서버와 클라이언트 (웹 브라우저)에 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-118">Normally, when you output cache a page by using the [OutputCache] attribute, the page is cached on both the server and the client (the web browser).</span></span> <span data-ttu-id="86f19-119">캐시 후 대체를 사용 하는 경우 페이지는 서버에만 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-119">When you use post-cache substitution, a page is cached only on the server.</span></span>


#### <a name="using-post-cache-substitution"></a><span data-ttu-id="86f19-120">캐시 후 대체를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="86f19-120">Using Post-Cache Substitution</span></span>

<span data-ttu-id="86f19-121">캐시 후 대체를 사용 하 여 하려면 두 단계가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-121">Using post-cache substitution requires two steps.</span></span> <span data-ttu-id="86f19-122">첫째, 캐시 된 페이지에 표시 하려고 하는 동적 콘텐츠를 나타내는 문자열을 반환 하는 메서드를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-122">First, you need to define a method that returns a string that represents the dynamic content that you want to display in the cached page.</span></span> <span data-ttu-id="86f19-123">다음으로 페이지에 동적 콘텐츠를 삽입할 HttpResponse.WriteSubstitution() 메서드를 호출.</span><span class="sxs-lookup"><span data-stu-id="86f19-123">Next, you call the HttpResponse.WriteSubstitution() method to inject the dynamic content into the page.</span></span>

<span data-ttu-id="86f19-124">예를 들어 임의로 캐시 된 페이지에 다른 뉴스 항목을 표시 한다고 가정해 보세요.</span><span class="sxs-lookup"><span data-stu-id="86f19-124">Imagine, for example, that you want to randomly display different news items in a cached page.</span></span> <span data-ttu-id="86f19-125">목록 1의 클래스에는 라는 RenderNews() 임의로 세 뉴스 항목의 목록에서 하나의 뉴스 항목을 반환 하는 단일 메서드를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-125">The class in Listing 1 exposes a single method, named RenderNews(), that randomly returns one news item from a list of three news items.</span></span>

<span data-ttu-id="86f19-126">**1 – Models\News.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="86f19-126">**Listing 1 – Models\News.cs**</span></span>

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample1.cs)]

<span data-ttu-id="86f19-127">캐시 후 대체를 이용 하려면 HttpResponse.WriteSubstitution() 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-127">To take advantage of post-cache substitution, you call the HttpResponse.WriteSubstitution() method.</span></span> <span data-ttu-id="86f19-128">동적 콘텐츠는 캐시 된 페이지의 영역 바꿉니다 WriteSubstitution() 메서드 코드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-128">The WriteSubstitution() method sets up the code to replace a region of the cached page with dynamic content.</span></span> <span data-ttu-id="86f19-129">WriteSubstitution() 메서드를 사용 하 여 목록 2의 뷰에서 임의의 뉴스 항목을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-129">The WriteSubstitution() method is used to display the random news item in the view in Listing 2.</span></span>

<span data-ttu-id="86f19-130">**Listing 2 – Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="86f19-130">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample2.aspx)]

<span data-ttu-id="86f19-131">RenderNews 메서드에 WriteSubstitution() 메서드에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-131">The RenderNews method is passed to the WriteSubstitution() method.</span></span> <span data-ttu-id="86f19-132">확인 된 RenderNews 메서드가 호출 되지 않습니다 (없습니다 괄호는 있음).</span><span class="sxs-lookup"><span data-stu-id="86f19-132">Notice that the RenderNews method is not called (there are no parentheses).</span></span> <span data-ttu-id="86f19-133">대신 WriteSubstitution()는 메서드에 대 한 참조가 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-133">Instead a reference to the method is passed to WriteSubstitution().</span></span>

<span data-ttu-id="86f19-134">인덱스 뷰 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-134">The Index view is cached.</span></span> <span data-ttu-id="86f19-135">보기는 보기 3의 컨트롤러에 의해 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-135">The view is returned by the controller in Listing 3.</span></span> <span data-ttu-id="86f19-136">Index () 동작 60 초 동안 캐시 될 인덱스 뷰를 발생 시키는 [OutputCache] 특성으로 데코레이팅되 어 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-136">Notice that the Index() action is decorated with an [OutputCache] attribute that causes the Index view to be cached for 60 seconds.</span></span>

<span data-ttu-id="86f19-137">**3 – Controllers\HomeController.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="86f19-137">**Listing 3 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample3.cs)]

<span data-ttu-id="86f19-138">인덱스 뷰 캐시 되는 경우에 인덱스 페이지를 요청 하는 경우 다른 임의의 뉴스 항목이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-138">Even though the Index view is cached, different random news items are displayed when you request the Index page.</span></span> <span data-ttu-id="86f19-139">인덱스 페이지를 요청 하는 경우 60 초 (그림 1 참조)에 대 한 페이지에 의해 표시 된 시간이 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-139">When you request the Index page, the time displayed by the page does not change for 60 seconds (see Figure 1).</span></span> <span data-ttu-id="86f19-140">시간 변경 되지 않는 팩트 페이지가 캐시를 증명 합니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-140">The fact that the time does not change proves that the page is cached.</span></span> <span data-ttu-id="86f19-141">각 요청과 함께 WriteSubstitution() 메서드-임의 뉴스 항목 – 변경에 의해 콘텐츠 삽입 되는 반면 합니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-141">However, the content injected by the WriteSubstitution() method – the random news item – changes with each request .</span></span>

<span data-ttu-id="86f19-142">**그림 1-캐시 된 페이지에 동적 뉴스 항목 삽입**</span><span class="sxs-lookup"><span data-stu-id="86f19-142">**Figure 1 – Injecting dynamic news items in a cached page**</span></span>

![clip_image002](adding-dynamic-content-to-a-cached-page-cs/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a><span data-ttu-id="86f19-144">도우미 메서드에서 캐시 후 대체를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="86f19-144">Using Post-Cache Substitution in Helper Methods</span></span>

<span data-ttu-id="86f19-145">캐시 후 대체 기능을 활용할 수 있는 더욱 손쉬운 방법을 사용자 지정 도우미 메서드 내에서 WriteSubstitution() 메서드에 대 한 호출을 캡슐화 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-145">An easier way to take advantage of post-cache substitution is to encapsulate the call to the WriteSubstitution() method within a custom helper method.</span></span> <span data-ttu-id="86f19-146">목록 4의 도우미 메서드에 의해이 방법은 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-146">This approach is illustrated by the helper method in Listing 4.</span></span>

<span data-ttu-id="86f19-147">**4 – AdHelper.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="86f19-147">**Listing 4 – AdHelper.cs**</span></span>

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample4.cs)]

<span data-ttu-id="86f19-148">두 개의 메서드를 노출 하는 정적 클래스를 포함 목록 4: RenderBanner() 및 RenderBannerInternal() 합니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-148">Listing 4 contains a static class that exposes two methods: RenderBanner() and RenderBannerInternal().</span></span> <span data-ttu-id="86f19-149">RenderBanner() 메서드를 실제 도우미 메서드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-149">The RenderBanner() method represents the actual helper method.</span></span> <span data-ttu-id="86f19-150">이 메서드는 다른 도우미 메서드와 마찬가지로 뷰에서 Html.RenderBanner()를 호출할 수 있도록 표준 ASP.NET MVC HtmlHelper 클래스를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-150">This method extends the standard ASP.NET MVC HtmlHelper class so that you can call Html.RenderBanner() in a view just like any other helper method.</span></span>

<span data-ttu-id="86f19-151">RenderBanner() 메서드 RenderBannerInternal() 메서드 WriteSubsitution() 메서드에 전달 HttpResponse.WriteSubstitution() 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-151">The RenderBanner() method calls the HttpResponse.WriteSubstitution() method passing the RenderBannerInternal() method to the WriteSubsitution() method.</span></span>

<span data-ttu-id="86f19-152">RenderBannerInternal() 메서드는 private 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-152">The RenderBannerInternal() method is a private method.</span></span> <span data-ttu-id="86f19-153">이 메서드는 도우미 메서드로 노출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-153">This method won't be exposed as a helper method.</span></span> <span data-ttu-id="86f19-154">임의로 RenderBannerInternal() 메서드는 세 가지 배너 광고 이미지의 목록에서 광고 배너 이미지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-154">The RenderBannerInternal() method randomly returns one banner advertisement image from a list of three banner advertisement images.</span></span>

<span data-ttu-id="86f19-155">목록 5의 수정 된 인덱스 뷰 RenderBanner() 도우미 메서드를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-155">The modified Index view in Listing 5 illustrates how you can use the RenderBanner() helper method.</span></span> <span data-ttu-id="86f19-156">다음에 유의 추가 &lt;% @ 가져오기 %&gt; 지시문 MvcApplication1.Helpers 네임 스페이스를 가져오는 뷰의 맨 아래에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-156">Notice that an additional &lt;%@ Import %&gt; directive is included at the top of the view to import the MvcApplication1.Helpers namespace.</span></span> <span data-ttu-id="86f19-157">이 네임 스페이스를 가져오지 않은, RenderBanner() 메서드 Html 속성의 메서드로 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-157">If you neglect to import this namespace, then the RenderBanner() method won't appear as a method on the Html property.</span></span>

<span data-ttu-id="86f19-158">**5-Views\Home\Index.aspx (RenderBanner() 메서드로)를 나열합니다.**</span><span class="sxs-lookup"><span data-stu-id="86f19-158">**Listing 5 – Views\Home\Index.aspx (with RenderBanner() method)**</span></span>

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample5.aspx)]

<span data-ttu-id="86f19-159">목록 5의 보기에서 렌더링 된 페이지를 요청 다른 배너 보급을 각 요청과 함께 표시 됩니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="86f19-159">When you request the page rendered by the view in Listing 5, a different banner advertisement is displayed with each request (see Figure 2).</span></span> <span data-ttu-id="86f19-160">페이지 캐시 되지만 RenderBanner() 도우미 메서드에 의해 배너 광고를 동적으로 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-160">The page is cached, but the banner advertisement is injected dynamically by the RenderBanner() helper method.</span></span>

<span data-ttu-id="86f19-161">**그림 2 – 임의 배너 광고를 표시 된 인덱스 뷰**</span><span class="sxs-lookup"><span data-stu-id="86f19-161">**Figure 2 – The Index view displaying a random banner advertisement**</span></span>

![clip_image004](adding-dynamic-content-to-a-cached-page-cs/_static/image2.jpg)

#### <a name="summary"></a><span data-ttu-id="86f19-163">요약</span><span class="sxs-lookup"><span data-stu-id="86f19-163">Summary</span></span>

<span data-ttu-id="86f19-164">이 자습서에서는 캐시 된 페이지의 내용을 동적으로 업데이트 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-164">This tutorial explained how you can dynamically update content in a cached page.</span></span> <span data-ttu-id="86f19-165">동적 콘텐츠 캐시 된 페이지에 지정 된 수를 사용할 수 있도록 HttpResponse.WriteSubstitution() 메서드를 사용 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-165">You learned how to use the HttpResponse.WriteSubstitution() method to enable dynamic content to be injected in a cached page.</span></span> <span data-ttu-id="86f19-166">또한 HTML 도우미 메서드 내에서 WriteSubstitution() 메서드에 대 한 호출을 캡슐화 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-166">You also learned how to encapsulate the call to the WriteSubstitution() method within an HTML helper method.</span></span>

<span data-ttu-id="86f19-167">웹 응용 프로그램의 성능에 큰 영향을 줄 수 것-가능한 경우 항상 캐싱을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-167">Take advantage of caching whenever possible – it can have a dramatic impact on the performance of your web applications.</span></span> <span data-ttu-id="86f19-168">이 자습서에서 설명 했 듯이를 페이지에 동적 콘텐츠를 표시 해야 하는 경우에 캐싱의 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86f19-168">As explained in this tutorial, you can take advantage of caching even when you need to display dynamic content in your pages.</span></span>

## 

## 

> [!div class="step-by-step"]
> <span data-ttu-id="86f19-169">[이전](improving-performance-with-output-caching-cs.md)
> [다음](creating-a-controller-cs.md)</span><span class="sxs-lookup"><span data-stu-id="86f19-169">[Previous](improving-performance-with-output-caching-cs.md)
[Next](creating-a-controller-cs.md)</span></span>
