---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
title: 캐시 된 페이지 (C#)에 동적 콘텐츠 추가 | Microsoft Docs
author: microsoft
description: 같은 페이지의 동적이 고 캐시 된 콘텐츠를 조합 하는 방법에 알아봅니다. 캐시 후 대체를 사용 하면 배너 광고 o 같은 동적 콘텐츠를 표시할 수 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: 2ddd4407-d143-4a94-877c-21771bfb97a6
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
msc.type: authoredcontent
ms.openlocfilehash: 08f680e8d057f47a3f2802b1136edfb00634637d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37364147"
---
<a name="adding-dynamic-content-to-a-cached-page-c"></a><span data-ttu-id="233b7-104">캐시 된 페이지 (C#)에 동적 콘텐츠 추가</span><span class="sxs-lookup"><span data-stu-id="233b7-104">Adding Dynamic Content to a Cached Page (C#)</span></span>
====================
<span data-ttu-id="233b7-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="233b7-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="233b7-106">같은 페이지의 동적이 고 캐시 된 콘텐츠를 조합 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-106">Learn how to mix dynamic and cached content in the same page.</span></span> <span data-ttu-id="233b7-107">캐시 후 대체를 사용 하는 배너 광고 또는 뉴스 항목을 캐시에 출력 하는 페이지 내에서 같은 동적 콘텐츠를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-107">Post-cache substitution enables you to display dynamic content, such as banner advertisements or news items, within a page that has been output cached.</span></span>


<span data-ttu-id="233b7-108">출력 캐싱을 활용 하 고, ASP.NET MVC 응용 프로그램의 성능을 크게 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-108">By taking advantage of output caching, you can dramatically improve the performance of an ASP.NET MVC application.</span></span> <span data-ttu-id="233b7-109">매번 페이지가 요청 될 페이지를 다시 생성 하는 대신에 페이지를 한 번 생성 하 고 여러 사용자에 대 한 메모리에 캐시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-109">Instead of regenerating a page each and every time the page is requested, the page can be generated once and cached in memory for multiple users.</span></span>

<span data-ttu-id="233b7-110">하지만 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-110">But there is a problem.</span></span> <span data-ttu-id="233b7-111">페이지에 동적 콘텐츠를 표시 해야 하는 경우에 어떻게?</span><span class="sxs-lookup"><span data-stu-id="233b7-111">What if you need to display dynamic content in the page?</span></span> <span data-ttu-id="233b7-112">예를 들어 페이지에서 배너 광고를 표시할 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-112">For example, imagine that you want to display a banner advertisement in the page.</span></span> <span data-ttu-id="233b7-113">모든 사용자가 동일한 광고를 볼 수 있도록 캐시할 배너 광고 하지 않으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-113">You don't want the banner advertisement to be cached so that every user sees the very same advertisement.</span></span> <span data-ttu-id="233b7-114">이런 방식으로 모든 비용을 확인 하지 않습니다!</span><span class="sxs-lookup"><span data-stu-id="233b7-114">You wouldn't make any money that way!</span></span>

<span data-ttu-id="233b7-115">다행 스럽게도 쉽게 솔루션을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-115">Fortunately, there is an easy solution.</span></span> <span data-ttu-id="233b7-116">라는 ASP.NET 프레임 워크의 기능 활용을 걸릴 수 있습니다 *캐시 후 대체*합니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-116">You can take advantage of a feature of the ASP.NET framework called *post-cache substitution*.</span></span> <span data-ttu-id="233b7-117">캐시 후 대체를 사용 하면 메모리에 캐시 된 페이지에 동적 콘텐츠를 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-117">Post-cache substitution enables you to substitute dynamic content in a page that has been cached in memory.</span></span>


<span data-ttu-id="233b7-118">일반적으로 [OutputCache] 특성을 사용 하 여 캐시 된 페이지를 출력할 때 페이지는 서버와 클라이언트 (웹 브라우저)에 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-118">Normally, when you output cache a page by using the [OutputCache] attribute, the page is cached on both the server and the client (the web browser).</span></span> <span data-ttu-id="233b7-119">캐시 후 대체를 사용 하면 페이지는 서버에만 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-119">When you use post-cache substitution, a page is cached only on the server.</span></span>


#### <a name="using-post-cache-substitution"></a><span data-ttu-id="233b7-120">캐시 후 대체를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="233b7-120">Using Post-Cache Substitution</span></span>

<span data-ttu-id="233b7-121">캐시 후 대체를 사용 하 여 두 단계가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-121">Using post-cache substitution requires two steps.</span></span> <span data-ttu-id="233b7-122">첫째, 캐시 된 페이지에 표시 하려는 동적 콘텐츠를 나타내는 문자열을 반환 하는 메서드를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-122">First, you need to define a method that returns a string that represents the dynamic content that you want to display in the cached page.</span></span> <span data-ttu-id="233b7-123">다음으로, 동적 콘텐츠 페이지에 삽입할 HttpResponse.WriteSubstitution() 메서드를 호출.</span><span class="sxs-lookup"><span data-stu-id="233b7-123">Next, you call the HttpResponse.WriteSubstitution() method to inject the dynamic content into the page.</span></span>

<span data-ttu-id="233b7-124">예를 들어, 임의로 캐시 된 페이지에서 다른 뉴스 항목을 표시 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-124">Imagine, for example, that you want to randomly display different news items in a cached page.</span></span> <span data-ttu-id="233b7-125">목록 1에서 클래스 라는 RenderNews() 임의로 세 뉴스 항목의 목록에서 하나의 뉴스 항목을 반환 하는 단일 메서드를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-125">The class in Listing 1 exposes a single method, named RenderNews(), that randomly returns one news item from a list of three news items.</span></span>

<span data-ttu-id="233b7-126">**1 – Models\News.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="233b7-126">**Listing 1 – Models\News.cs**</span></span>

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample1.cs)]

<span data-ttu-id="233b7-127">캐시 후 대체를 이용 하려면 HttpResponse.WriteSubstitution() 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-127">To take advantage of post-cache substitution, you call the HttpResponse.WriteSubstitution() method.</span></span> <span data-ttu-id="233b7-128">동적 콘텐츠를 사용 하 여 캐시 된 페이지의 영역을 바꾸려면 WriteSubstitution() 메서드 코드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-128">The WriteSubstitution() method sets up the code to replace a region of the cached page with dynamic content.</span></span> <span data-ttu-id="233b7-129">목록 2 뷰에서 임의의 뉴스 항목을 표시 하려면 WriteSubstitution() 메서드가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-129">The WriteSubstitution() method is used to display the random news item in the view in Listing 2.</span></span>

<span data-ttu-id="233b7-130">**Listing 2 – Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="233b7-130">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample2.aspx)]

<span data-ttu-id="233b7-131">RenderNews 메서드 WriteSubstitution() 메서드에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-131">The RenderNews method is passed to the WriteSubstitution() method.</span></span> <span data-ttu-id="233b7-132">RenderNews 메서드를 호출 하지는 알 수 있습니다 (없습니다 괄호는 있음).</span><span class="sxs-lookup"><span data-stu-id="233b7-132">Notice that the RenderNews method is not called (there are no parentheses).</span></span> <span data-ttu-id="233b7-133">대신 WriteSubstitution()는 메서드에 대 한 참조가 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-133">Instead a reference to the method is passed to WriteSubstitution().</span></span>

<span data-ttu-id="233b7-134">인덱스 보기 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-134">The Index view is cached.</span></span> <span data-ttu-id="233b7-135">보기 3의 컨트롤러 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-135">The view is returned by the controller in Listing 3.</span></span> <span data-ttu-id="233b7-136">Index () 작업을 하면 인덱스 보기에 60 초 동안 캐시에 있는 [OutputCache] 특성으로 데코 레이트 된 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-136">Notice that the Index() action is decorated with an [OutputCache] attribute that causes the Index view to be cached for 60 seconds.</span></span>

<span data-ttu-id="233b7-137">**3 – controllers\ homecontroller.cs를 나열합니다.**</span><span class="sxs-lookup"><span data-stu-id="233b7-137">**Listing 3 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample3.cs)]

<span data-ttu-id="233b7-138">인덱스 보기 캐시 된 경우에 인덱스 페이지를 요청 하는 경우 다른 임의의 뉴스 항목이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-138">Even though the Index view is cached, different random news items are displayed when you request the Index page.</span></span> <span data-ttu-id="233b7-139">인덱스 페이지를 요청 하면 페이지에 의해 표시 된 시간이 60 초 (그림 1 참조)에 대 한 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-139">When you request the Index page, the time displayed by the page does not change for 60 seconds (see Figure 1).</span></span> <span data-ttu-id="233b7-140">페이지 캐시 되는 증명 하는 시간을 변경 하지 않는 팩트 합니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-140">The fact that the time does not change proves that the page is cached.</span></span> <span data-ttu-id="233b7-141">그러나 각 요청과 함께 WriteSubstitution() 메서드 – 임의의 뉴스 항목 – 변경에 의해 콘텐츠가 삽입 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-141">However, the content injected by the WriteSubstitution() method – the random news item – changes with each request .</span></span>

<span data-ttu-id="233b7-142">**그림 1-캐시 된 페이지에 동적 뉴스 항목 삽입**</span><span class="sxs-lookup"><span data-stu-id="233b7-142">**Figure 1 – Injecting dynamic news items in a cached page**</span></span>

![clip_image002](adding-dynamic-content-to-a-cached-page-cs/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a><span data-ttu-id="233b7-144">캐시 후 대체를 사용 하 여 도우미 메서드에서</span><span class="sxs-lookup"><span data-stu-id="233b7-144">Using Post-Cache Substitution in Helper Methods</span></span>

<span data-ttu-id="233b7-145">캐시 후 대체를 활용 하는 간단한 방법인 캡슐화 하는 데 사용자 지정 도우미 메서드 내에서 WriteSubstitution() 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-145">An easier way to take advantage of post-cache substitution is to encapsulate the call to the WriteSubstitution() method within a custom helper method.</span></span> <span data-ttu-id="233b7-146">이 방법은 4의 도우미 메서드에 의해 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-146">This approach is illustrated by the helper method in Listing 4.</span></span>

<span data-ttu-id="233b7-147">**4-AdHelper.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="233b7-147">**Listing 4 – AdHelper.cs**</span></span>

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample4.cs)]

<span data-ttu-id="233b7-148">두 메서드를 노출 하는 정적 클래스에 포함 코드 4: RenderBanner() 및 RenderBannerInternal() 합니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-148">Listing 4 contains a static class that exposes two methods: RenderBanner() and RenderBannerInternal().</span></span> <span data-ttu-id="233b7-149">RenderBanner() 메서드를 실제 도우미 메서드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-149">The RenderBanner() method represents the actual helper method.</span></span> <span data-ttu-id="233b7-150">이 메서드는 다른 도우미 메서드와 마찬가지로 뷰에서 Html.RenderBanner()를 호출할 수 있도록 표준 ASP.NET MVC HtmlHelper 클래스를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-150">This method extends the standard ASP.NET MVC HtmlHelper class so that you can call Html.RenderBanner() in a view just like any other helper method.</span></span>

<span data-ttu-id="233b7-151">RenderBanner() 메서드 RenderBannerInternal() WriteSubsitution() 메서드에 전달 HttpResponse.WriteSubstitution() 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-151">The RenderBanner() method calls the HttpResponse.WriteSubstitution() method passing the RenderBannerInternal() method to the WriteSubsitution() method.</span></span>

<span data-ttu-id="233b7-152">RenderBannerInternal() 메서드는 전용 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-152">The RenderBannerInternal() method is a private method.</span></span> <span data-ttu-id="233b7-153">이 메서드는 도우미 메서드도 노출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-153">This method won't be exposed as a helper method.</span></span> <span data-ttu-id="233b7-154">RenderBannerInternal() 메서드는 임의로 세 배너 광고 이미지 목록에서 하나의 배너 광고 이미지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-154">The RenderBannerInternal() method randomly returns one banner advertisement image from a list of three banner advertisement images.</span></span>

<span data-ttu-id="233b7-155">목록 5에서 수정 된 인덱스 뷰 RenderBanner() 도우미 메서드를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-155">The modified Index view in Listing 5 illustrates how you can use the RenderBanner() helper method.</span></span> <span data-ttu-id="233b7-156">추가 &lt;가져오기 % @ %&gt; 지시문 MvcApplication1.Helpers 네임 스페이스를 가져오는 뷰의 맨 위에 있는 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-156">Notice that an additional &lt;%@ Import %&gt; directive is included at the top of the view to import the MvcApplication1.Helpers namespace.</span></span> <span data-ttu-id="233b7-157">이 네임 스페이스를 가져오지 않은, 경우에 Html 속성의 메서드로 RenderBanner() 메서드 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-157">If you neglect to import this namespace, then the RenderBanner() method won't appear as a method on the Html property.</span></span>

<span data-ttu-id="233b7-158">**5-Views\Home\Index.aspx (RenderBanner() 메서드로)를 나열합니다.**</span><span class="sxs-lookup"><span data-stu-id="233b7-158">**Listing 5 – Views\Home\Index.aspx (with RenderBanner() method)**</span></span>

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample5.aspx)]

<span data-ttu-id="233b7-159">목록 5의 보기에서 렌더링 된 페이지를 요청 하면 다른 배너 광고를 각 요청과 함께 표시 됩니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="233b7-159">When you request the page rendered by the view in Listing 5, a different banner advertisement is displayed with each request (see Figure 2).</span></span> <span data-ttu-id="233b7-160">페이지 캐시 되지만 배너 광고 RenderBanner() 도우미 메서드에 의해 동적으로 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-160">The page is cached, but the banner advertisement is injected dynamically by the RenderBanner() helper method.</span></span>

<span data-ttu-id="233b7-161">**그림 2 – 임의의 배너 광고를 표시 된 인덱스 뷰**</span><span class="sxs-lookup"><span data-stu-id="233b7-161">**Figure 2 – The Index view displaying a random banner advertisement**</span></span>

![clip_image004](adding-dynamic-content-to-a-cached-page-cs/_static/image2.jpg)

#### <a name="summary"></a><span data-ttu-id="233b7-163">요약</span><span class="sxs-lookup"><span data-stu-id="233b7-163">Summary</span></span>

<span data-ttu-id="233b7-164">이 자습서는 캐시 된 페이지의 콘텐츠를 동적으로 업데이트 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-164">This tutorial explained how you can dynamically update content in a cached page.</span></span> <span data-ttu-id="233b7-165">캐시 된 페이지에 지정 된 수를 동적 콘텐츠를 사용 하도록 설정 하려면 HttpResponse.WriteSubstitution() 메서드를 사용 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-165">You learned how to use the HttpResponse.WriteSubstitution() method to enable dynamic content to be injected in a cached page.</span></span> <span data-ttu-id="233b7-166">HTML 도우미 메서드 내 WriteSubstitution() 메서드에 대 한 호출을 캡슐화 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-166">You also learned how to encapsulate the call to the WriteSubstitution() method within an HTML helper method.</span></span>

<span data-ttu-id="233b7-167">가능한 – 웹 응용 프로그램의 성능에 상당한 영향을 미칠 수 있습니다이 캐싱을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-167">Take advantage of caching whenever possible – it can have a dramatic impact on the performance of your web applications.</span></span> <span data-ttu-id="233b7-168">이 자습서에서 설명 했 듯이 캐싱 페이지에 동적 콘텐츠를 표시 해야 하는 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="233b7-168">As explained in this tutorial, you can take advantage of caching even when you need to display dynamic content in your pages.</span></span>

## 

## 

> [!div class="step-by-step"]
> <span data-ttu-id="233b7-169">[이전](improving-performance-with-output-caching-cs.md)
> [다음](creating-a-controller-cs.md)</span><span class="sxs-lookup"><span data-stu-id="233b7-169">[Previous](improving-performance-with-output-caching-cs.md)
[Next](creating-a-controller-cs.md)</span></span>
