---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
title: 캐싱 (VB)를 출력으로 성능 향상 | Microsoft Docs
author: microsoft
description: 이 자습서에서는 출력 캐싱을 사용 하 여 ASP.NET MVC 웹 응용 프로그램의 성능을 크게 개선할 수 있습니다 방법을 배웁니다. 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: 0e7b4d85-2c46-4eaf-b6a8-6cd566a67334
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
msc.type: authoredcontent
ms.openlocfilehash: 8ee933b477307f5c3f2377e112a1a98d3d6bc337
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874423"
---
<a name="improving-performance-with-output-caching-vb"></a><span data-ttu-id="231bd-104">출력 캐싱 (VB)으로 성능 향상</span><span class="sxs-lookup"><span data-stu-id="231bd-104">Improving Performance with Output Caching (VB)</span></span>
====================
<span data-ttu-id="231bd-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="231bd-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="231bd-106">이 자습서에서는 출력 캐싱을 사용 하 여 ASP.NET MVC 웹 응용 프로그램의 성능을 크게 개선할 수 있습니다 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-106">In this tutorial, you learn how you can dramatically improve the performance of your ASP.NET MVC web applications by taking advantage of output caching.</span></span> <span data-ttu-id="231bd-107">하 여 동일한 콘텐츠 매번 작업을 호출 하는 새 사용자를 만들 수 없습니다 필요가 컨트롤러 작업에서 반환 된 결과 캐시 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-107">You learn how to cache the result returned from a controller action so that the same content does not need to be created each and every time a new user invokes the action.</span></span>


<span data-ttu-id="231bd-108">이 자습서의 목표 출력 캐시의 사용 하 여 ASP.NET MVC 응용 프로그램의 성능을 크게 개선할 수 있습니다 어떻게 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-108">The goal of this tutorial is to explain how you can dramatically improve the performance of an ASP.NET MVC application by taking advantage of the output cache.</span></span> <span data-ttu-id="231bd-109">출력 캐시를 사용 하면 컨트롤러 작업에서 반환 된 콘텐츠를 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-109">The output cache enables you to cache the content returned by a controller action.</span></span> <span data-ttu-id="231bd-110">이런 방식으로 동일한 콘텐츠 매번 동일한 컨트롤러 동작이 호출을 생성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-110">That way, the same content does not need to be generated each and every time the same controller action is invoked.</span></span>

<span data-ttu-id="231bd-111">예를 들어, ASP.NET MVC 응용 프로그램 인덱스 라는 이름의 뷰가 데이터베이스 레코드의 목록에 표시 되는지 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-111">Imagine, for example, that your ASP.NET MVC application displays a list of database records in a view named Index.</span></span> <span data-ttu-id="231bd-112">일반적으로 사용자가 인덱스 뷰를 반환 하는 컨트롤러 작업을 호출 하는 각 시간 데이터베이스 레코드 집합을 검색 해야 데이터베이스에서 데이터베이스 쿼리를 실행 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-112">Normally, each and every time that a user invokes the controller action that returns the Index view, the set of database records must be retrieved from the database by executing a database query.</span></span>

<span data-ttu-id="231bd-113">출력 캐시의 있는 이용할 반면에 있으면 다음 방지할 수 있습니다 될 때마다 동일한 컨트롤러 작업을 호출 하는 모든 사용자는 데이터베이스 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-113">If, on the other hand, you take advantage of the output cache then you can avoid executing a database query every time any user invokes the same controller action.</span></span> <span data-ttu-id="231bd-114">뷰는 컨트롤러 작업에서 다시 생성 되지 않고 캐시에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-114">The view can be retrieved from the cache instead of being regenerated from the controller action.</span></span> <span data-ttu-id="231bd-115">서버에서 작동 하면 캐싱 수행 중복을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-115">Caching enables you to avoid performing redundant work on the server.</span></span>

#### <a name="enabling-output-caching"></a><span data-ttu-id="231bd-116">출력 캐싱을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="231bd-116">Enabling Output Caching</span></span>

<span data-ttu-id="231bd-117">추가 하 여 출력 캐싱을 사용 하도록 설정 하면 프로그램 &lt;OutputCache&gt; 특성을 개별 컨트롤러 동작 또는 전체 컨트롤러 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-117">You enable output caching by adding an &lt;OutputCache&gt; attribute to either an individual controller action or an entire controller class.</span></span> <span data-ttu-id="231bd-118">예를 들어 컨트롤러 목록 1의 index () 라는 동작을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-118">For example, the controller in Listing 1 exposes an action named Index().</span></span> <span data-ttu-id="231bd-119">Index () 작업의 출력은 10 초 동안 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-119">The output of the Index() action is cached for 10 seconds.</span></span>

<span data-ttu-id="231bd-120">**Listing 1 – Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="231bd-120">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample1.vb)]


<span data-ttu-id="231bd-121">베타 버전의 ASP.NET MVC 출력 캐싱을 사용할 수 없습니다와 같은 URL에 대 한 [ http://www.MySite.com/ ](http://www.mysite.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-121">In the Beta versions of ASP.NET MVC, output caching does not work for a URL like [http://www.MySite.com/](http://www.mysite.com/).</span></span> <span data-ttu-id="231bd-122">같은 URL을 입력 해야 하는 대신, [ http://www.MySite.com/Home/Index ](http://www.mysite.com/Home/Index)합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-122">Instead, you must enter a URL like [http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index).</span></span>


<span data-ttu-id="231bd-123">목록 1의 index () 작업의 출력은 10 초 동안 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-123">In Listing 1, the output of the Index() action is cached for 10 seconds.</span></span> <span data-ttu-id="231bd-124">원하는 경우에 훨씬 더 긴 캐시 기간을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-124">If you prefer, you can specify a much longer cache duration.</span></span> <span data-ttu-id="231bd-125">예를 들어 1 일에 대 한 컨트롤러 작업의 출력을 캐시 하려는 경우 지정할 수 있습니다 캐시 지속 시간이 86, 400 초 (60 초 \* 60 분 \* 24 시간).</span><span class="sxs-lookup"><span data-stu-id="231bd-125">For example, if you want to cache the output of a controller action for one day then you can specify a cache duration of 86400 seconds (60 seconds \* 60 minutes \* 24 hours).</span></span>

<span data-ttu-id="231bd-126">콘텐츠가 다 사용자가 지정한 시간 동안 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-126">There is no guarantee that content will be cached for the amount of time that you specify.</span></span> <span data-ttu-id="231bd-127">메모리 리소스가 부족 해지면, 캐시 제거 콘텐츠를 자동으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-127">When memory resources become low, the cache starts evicting content automatically.</span></span>

<span data-ttu-id="231bd-128">목록 1의 Home 컨트롤러 목록 2의 인덱스 뷰를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-128">The Home controller in Listing 1 returns the Index view in Listing 2.</span></span> <span data-ttu-id="231bd-129">이 보기에 대 한 특별 합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-129">There is nothing special about this view.</span></span> <span data-ttu-id="231bd-130">인덱스 보기에는 단순히 현재 시간이 표시 됩니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="231bd-130">The Index view simply displays the current time (see Figure 1).</span></span>

<span data-ttu-id="231bd-131">**Listing 2 – Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="231bd-131">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](improving-performance-with-output-caching-vb/samples/sample2.aspx)]

<span data-ttu-id="231bd-132">**그림 1-캐시 된 인덱스 뷰**</span><span class="sxs-lookup"><span data-stu-id="231bd-132">**Figure 1 – Cached Index view**</span></span>

![clip_image002](improving-performance-with-output-caching-vb/_static/image1.jpg)

<span data-ttu-id="231bd-134">브라우저의 주소 표시줄에 URL /Home/인덱스를 입력 하 고 반복 해 서 다음 인덱스 뷰에서 표시 된 시간이 브라우저의 새로 고침/다시 로드 단추에 도달 하 여 index () 작업이 여러 번 호출 하는 경우 10 초 동안 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-134">If you invoke the Index() action multiple times by entering the URL /Home/Index in the address bar of your browser and hitting the Refresh/Reload button in your browser repeatedly, then the time displayed by the Index view won't change for 10 seconds.</span></span> <span data-ttu-id="231bd-135">보기 캐시 되므로 한 번 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-135">The same time is displayed because the view is cached.</span></span>

<span data-ttu-id="231bd-136">동일한 응용 프로그램을 방문 하는 모든 작업에 대 한 캐시는 이해 하는 것이 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-136">It is important to understand that the same view is cached for everyone who visits your application.</span></span> <span data-ttu-id="231bd-137">Index () 작업을 호출 하는 모든 사람이 동일한 캐시 된 버전을 인덱스 뷰를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-137">Anyone who invokes the Index() action will get the same cached version of the Index view.</span></span> <span data-ttu-id="231bd-138">즉, 웹 서버에서 인덱스 뷰를 제공 하기 위해 수행 해야 하는 작업의 양을 크게 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-138">This means that the amount of work that the web server must perform to serve the Index view is dramatically reduced.</span></span>

<span data-ttu-id="231bd-139">보기 목록 2에는 매우 간단한 작업을 수행할 수 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-139">The view in Listing 2 happens to be doing something really simple.</span></span> <span data-ttu-id="231bd-140">방금 보기는 현재 시간을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-140">The view just displays the current time.</span></span> <span data-ttu-id="231bd-141">그러나 캐시 데이터베이스 레코드 집합을 표시 하는 보기 쉽게와 마찬가지로 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-141">However, you could just as easily cache a view that displays a set of database records.</span></span> <span data-ttu-id="231bd-142">이 경우 데이터베이스 레코드 집합은 각 시간 보기를 반환 하는 컨트롤러 작업 호출 되는 데이터베이스에서 검색 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-142">In that case, the set of database records would not need to be retrieved from the database each and every time the controller action that returns the view is invoked.</span></span> <span data-ttu-id="231bd-143">캐싱 웹 서버와 데이터베이스 서버 모두에서 수행 해야 하는 작업의 양을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-143">Caching can reduce the amount of work that both your web server and database server must perform.</span></span>

<span data-ttu-id="231bd-144">페이지를 사용 하지 않는 &lt;% @ OutputCache %&gt; MVC 뷰에 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-144">Don't use the page &lt;%@ OutputCache %&gt; directive in an MVC view.</span></span> <span data-ttu-id="231bd-145">이 지시문은 위에 Web Forms 세계에서 고 대 ASP.NET MVC 응용 프로그램에서는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-145">This directive is bleeding over from the Web Forms world and should not be used in an ASP.NET MVC application.</span></span> 

#### <a name="where-content-is-cached"></a><span data-ttu-id="231bd-146">콘텐츠가 캐시 되며</span><span class="sxs-lookup"><span data-stu-id="231bd-146">Where Content is Cached</span></span>

<span data-ttu-id="231bd-147">기본적으로 사용 하는 경우는 &lt;OutputCache&gt; 콘텐츠 특성 세 위치에 캐시 된: 웹 서버, 모든 프록시 서버 및 웹 브라우저입니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-147">By default, when you use the &lt;OutputCache&gt; attribute, content is cached in three locations: the web server, any proxy servers, and the web browser.</span></span> <span data-ttu-id="231bd-148">콘텐츠의 Location 속성을 수정 하 여 캐시 된 위치에 정확 하 게 제어할 수 있습니다는 &lt;OutputCache&gt; 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-148">You can control exactly where content is cached by modifying the Location property of the &lt;OutputCache&gt; attribute.</span></span>

<span data-ttu-id="231bd-149">다음 값 중 하나에 Location 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-149">You can set the Location property to any one of the following values:</span></span>

> <span data-ttu-id="231bd-150">· 모든</span><span class="sxs-lookup"><span data-stu-id="231bd-150">· Any</span></span>
> 
> <span data-ttu-id="231bd-151">· 클라이언트</span><span class="sxs-lookup"><span data-stu-id="231bd-151">· Client</span></span>
> 
> <span data-ttu-id="231bd-152">· 다운스트림</span><span class="sxs-lookup"><span data-stu-id="231bd-152">· Downstream</span></span>
> 
> <span data-ttu-id="231bd-153">· 서버</span><span class="sxs-lookup"><span data-stu-id="231bd-153">· Server</span></span>
> 
> <span data-ttu-id="231bd-154">· 없음</span><span class="sxs-lookup"><span data-stu-id="231bd-154">· None</span></span>
> 
> <span data-ttu-id="231bd-155">· ServerAndClient</span><span class="sxs-lookup"><span data-stu-id="231bd-155">· ServerAndClient</span></span>


<span data-ttu-id="231bd-156">기본적으로 Location 속성이 어떤 값을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-156">By default, the Location property has the value Any.</span></span> <span data-ttu-id="231bd-157">그러나 경우가 브라우저에 대해서만 또는 서버에만 캐시에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-157">However, there are situations in which you might want to cache only on the browser or only on the server.</span></span> <span data-ttu-id="231bd-158">예를 들어, 각 사용자에 대 한 개인 정보를 캐시 하는 경우 다음 하면 안됩니다 서버에 대 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-158">For example, if you are caching information that is personalized for each user then you should not cache the information on the server.</span></span> <span data-ttu-id="231bd-159">다른 사용자에 게 서로 다른 정보를 표시 하는 경우 클라이언트에 대해서만 정보를 캐시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-159">If you are displaying different information to different users then you should cache the information only on the client.</span></span>

<span data-ttu-id="231bd-160">예를 들어 목록 3의 컨트롤러 GetName() 현재 사용자 이름을 반환 하는 작업을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-160">For example, the controller in Listing 3 exposes an action named GetName() that returns the current user name.</span></span> <span data-ttu-id="231bd-161">잭 웹 사이트에 로그인 하 고 GetName() 작업을 호출 하는 경우 다음 동작 문자열을 반환 "Hi 잭"입니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-161">If Jack logs into the website and invokes the GetName() action then the action returns the string "Hi Jack".</span></span> <span data-ttu-id="231bd-162">Jill이 웹 사이트에 로그인 하 고 GetName() 작업을 호출 하는 그 후 다음 그녀 가져옵니다 문자열을 "Hi 잭"입니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-162">If, subsequently, Jill logs into the website and invokes the GetName() action then she also will get the string "Hi Jack".</span></span> <span data-ttu-id="231bd-163">문자열 잭 컨트롤러 작업을 처음 호출 후 모든 사용자에 대해 웹 서버에 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-163">The string is cached on the web server for all users after Jack initially invokes the controller action.</span></span>

<span data-ttu-id="231bd-164">**Listing 3 – Controllers\BadUserController.vb**</span><span class="sxs-lookup"><span data-stu-id="231bd-164">**Listing 3 – Controllers\BadUserController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample3.vb)]

<span data-ttu-id="231bd-165">대부분의 경우 목록 3의 컨트롤러를 원하는 대로 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-165">Most likely, the controller in Listing 3 does not work the way that you want.</span></span> <span data-ttu-id="231bd-166">Jill "Hi 잭" 메시지를 표시 하는 것이 않으려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-166">You don't want to display the message "Hi Jack" to Jill.</span></span>

<span data-ttu-id="231bd-167">서버 캐시에 콘텐츠를 캐시 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-167">You should never cache personalized content in the server cache.</span></span> <span data-ttu-id="231bd-168">그러나 다음 성능 향상을 위해 브라우저 캐시에 개인 설정 된 콘텐츠를 캐시 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-168">However, you might want to cache the personalized content in the browser cache to improve performance.</span></span> <span data-ttu-id="231bd-169">브라우저에서 콘텐츠를 캐시 하는 경우 사용자는 같은 컨트롤러 동작을 여러 번 호출 서버 대신 브라우저 캐시에서 콘텐츠를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-169">If you cache content in the browser, and a user invokes the same controller action multiple times, then the content can be retrieved from the browser cache instead of the server.</span></span>

<span data-ttu-id="231bd-170">목록 4에 수정 된 컨트롤러 GetName() 작업의 출력을 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-170">The modified controller in Listing 4 caches the output of the GetName() action.</span></span> <span data-ttu-id="231bd-171">그러나 콘텐츠 서버에 없는 및 브라우저에만 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-171">However, the content is cached only on the browser and not on the server.</span></span> <span data-ttu-id="231bd-172">이런 방식으로 여러 사용자가 GetName() 메서드를 호출 하는 경우, 각 사용자가 자신의 사용자 이름 및 또 다른 사람의 사용자 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-172">That way, when multiple users invoke the GetName() method, each person gets their own user name and not another person's user name.</span></span>

<span data-ttu-id="231bd-173">**Listing 4 – Controllers\UserController.vb**</span><span class="sxs-lookup"><span data-stu-id="231bd-173">**Listing 4 – Controllers\UserController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample4.vb)]

<span data-ttu-id="231bd-174">에 &lt;OutputCache&gt; 목록 4에는 특성 OutputCacheLocation.Client 값으로 설정 하는 Location 속성이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-174">Notice that the &lt;OutputCache&gt; attribute in Listing 4 includes a Location property set to the value OutputCacheLocation.Client.</span></span> <span data-ttu-id="231bd-175">&lt;OutputCache&gt; NoStore 속성 특성에도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-175">The &lt;OutputCache&gt; attribute also includes a NoStore property.</span></span> <span data-ttu-id="231bd-176">NoStore 속성은 캐시 된 콘텐츠의 영구 복사본 저장 하지 마십시오 프록시 서버와 브라우저 알리는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-176">The NoStore property is used to inform proxy servers and browsers that they should not store a permanent copy of the cached content.</span></span>

#### <a name="varying-the-output-cache"></a><span data-ttu-id="231bd-177">출력 캐시를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-177">Varying the Output Cache</span></span>

<span data-ttu-id="231bd-178">경우에 따라 서로 다른 캐시 된 버전의 동일한 콘텐츠를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-178">In some situations, you might want different cached versions of the very same content.</span></span> <span data-ttu-id="231bd-179">예를 들어 마스터/세부 정보 페이지를 만들고 있는 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-179">Imagine, for example, that you are creating a master/detail page.</span></span> <span data-ttu-id="231bd-180">마스터 페이지 영화 제목 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-180">The master page displays a list of movie titles.</span></span> <span data-ttu-id="231bd-181">제목을 클릭 하면 선택한 동영상에 대 한 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-181">When you click a title, you get details for the selected movie.</span></span>

<span data-ttu-id="231bd-182">세부 정보 페이지, 캐시 같은 동영상에 대 한 세부 정보 클릭 하면 어떤 동영상에 관계 없이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-182">If you cache the details page, then the details for the same movie will be displayed no matter which movie you click.</span></span> <span data-ttu-id="231bd-183">첫 번째 사용자가 선택한 첫 번째 동영상 이후의 모든 사용자에 게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-183">The first movie selected by the first user will be displayed to all future users.</span></span>

<span data-ttu-id="231bd-184">VaryByParam 속성을 활용 하 여이 문제를 해결할 수는 &lt;OutputCache&gt; 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-184">You can fix this problem by taking advantage of the VaryByParam property of the &lt;OutputCache&gt; attribute.</span></span> <span data-ttu-id="231bd-185">이 속성을 사용 하면 서로 다른 캐시 된 버전의 동일한 콘텐츠 때 폼 매개 변수를 만들 수 있습니다 또는 쿼리 문자열 매개 변수 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-185">This property enables you to create different cached versions of the very same content when a form parameter or query string parameter varies.</span></span>

<span data-ttu-id="231bd-186">예를 들어 목록 5에 있는 컨트롤러 Master() 및 Details() 라는 두 가지 동작을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-186">For example, the controller in Listing 5 exposes two actions named Master() and Details().</span></span> <span data-ttu-id="231bd-187">Master() 작업 영화 제목의 목록을 반환 하 고 Details() 작업 선택한 동영상에 대 한 세부 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-187">The Master() action returns a list of movie titles and the Details() action returns the details for the selected movie.</span></span>

<span data-ttu-id="231bd-188">**Listing 5 – Controllers\MoviesController.vb**</span><span class="sxs-lookup"><span data-stu-id="231bd-188">**Listing 5 – Controllers\MoviesController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample5.vb)]

<span data-ttu-id="231bd-189">Master() 동작 포함 VaryByParam 속성 값으로 "none"입니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-189">The Master() action includes a VaryByParam property with the value "none".</span></span> <span data-ttu-id="231bd-190">작업을 호출할 Master() 동일한 캐시 된 버전의 마스터를 볼 때 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-190">When the Master() action is invoked, the same cached version of the Master view is returned.</span></span> <span data-ttu-id="231bd-191">모든 폼 매개 변수 또는 쿼리 문자열 매개 변수는 무시 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="231bd-191">Any form parameters or query string parameters are ignored (see Figure 2).</span></span>

<span data-ttu-id="231bd-192">**그림 2 – /Movies/Master 보기**</span><span class="sxs-lookup"><span data-stu-id="231bd-192">**Figure 2 – The /Movies/Master view**</span></span>

![clip_image004](improving-performance-with-output-caching-vb/_static/image2.jpg)

<span data-ttu-id="231bd-194">**그림 3 – / 영화/세부 정보 보기**</span><span class="sxs-lookup"><span data-stu-id="231bd-194">**Figure 3 – The /Movies/Details view**</span></span>

![clip_image006](improving-performance-with-output-caching-vb/_static/image3.jpg)

<span data-ttu-id="231bd-196">Details() 동작 "Id" 값을 갖는 VaryByParam 속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-196">The Details() action includes a VaryByParam property with the value "Id".</span></span> <span data-ttu-id="231bd-197">Id 매개 변수에 다른 값은 컨트롤러 작업에 전달 되 면 자세히 보기의 캐시 된 버전을 다른 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-197">When different values of the Id parameter are passed to the controller action, different cached versions of the Details view are generated.</span></span>

<span data-ttu-id="231bd-198">더 많은 캐싱에 VaryByParam 속성 결과 사용 하는 및 적은 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-198">It is important to understand that using the VaryByParam property results in more caching and not less.</span></span> <span data-ttu-id="231bd-199">자세히 보기의 다른 캐시 된 버전 Id 매개 변수의 각 버전에 대해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-199">A different cached version of the Details view is created for each different version of the Id parameter.</span></span>

<span data-ttu-id="231bd-200">VaryByParam 속성은 다음 값으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-200">You can set the VaryByParam property to the following values:</span></span>

> <span data-ttu-id="231bd-201">\* = 폼 또는 쿼리 문자열 매개 변수 변경 될 때마다 서로 다른 캐시 된 버전을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-201">\* = Create a different cached version whenever a form or query string parameter varies.</span></span>
> 
> <span data-ttu-id="231bd-202">none = 사용 안 함 다양 한 캐시 된 버전을 만들려면</span><span class="sxs-lookup"><span data-stu-id="231bd-202">none = Never create different cached versions</span></span>
> 
> <span data-ttu-id="231bd-203">세미콜론 매개 변수 목록이 다릅니다 폼 또는 쿼리 문자열 매개 변수 목록에서 때마다 만들기 서로 다른 캐시 된 버전 =</span><span class="sxs-lookup"><span data-stu-id="231bd-203">Semicolon list of parameters = Create different cached versions whenever any of the form or query string parameters in the list varies</span></span>


#### <a name="creating-a-cache-profile"></a><span data-ttu-id="231bd-204">캐시 프로필 만들기</span><span class="sxs-lookup"><span data-stu-id="231bd-204">Creating a Cache Profile</span></span>

<span data-ttu-id="231bd-205">속성을 수정 하 여 출력 캐시 속성을 구성 하는 대신는 &lt;OutputCache&gt; 특성 웹 구성 파일 (web.config) 파일에서 캐시 프로필을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-205">As an alternative to configuring output cache properties by modifying properties of the &lt;OutputCache&gt; attribute, you can create a cache profile in the web configuration (web.config) file.</span></span> <span data-ttu-id="231bd-206">웹 구성 파일에서 캐시 프로필을 만드는 몇 가지 중요 한 이점이 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-206">Creating a cache profile in the web configuration file offers a couple of important advantages.</span></span>

<span data-ttu-id="231bd-207">첫째, 웹 구성 파일에서 출력 캐시를 구성 하 여 컨트롤러 작업에서 하나의 중앙 위치에 콘텐츠를 캐시 하는 방법을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-207">First, by configuring output caching in the web configuration file, you can control how controller actions cache content in one central location.</span></span> <span data-ttu-id="231bd-208">캐시 프로필이 두 개를 만들고 여러 컨트롤러 또는 컨트롤러 동작 프로필을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-208">You can create one cache profile and apply the profile to several controllers or controller actions.</span></span>

<span data-ttu-id="231bd-209">둘째, 응용 프로그램을 다시 컴파일하지 않고 웹 구성 파일을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-209">Second, you can modify the web configuration file without recompiling your application.</span></span> <span data-ttu-id="231bd-210">프로덕션 환경에 이미 배포 된 응용 프로그램에 대 한 캐싱을 사용 하지 않도록 설정 해야 할 경우 다음 수정할 수 있습니다 단순히 웹 구성 파일에 정의 된 캐시 프로필.</span><span class="sxs-lookup"><span data-stu-id="231bd-210">If you need to disable caching for an application that has already been deployed to production, then you can simply modify the cache profiles defined in the web configuration file.</span></span> <span data-ttu-id="231bd-211">웹 구성 파일에 변경 내용을 자동으로 검색 하 고 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-211">Any changes to the web configuration file will be detected automatically and applied.</span></span>

<span data-ttu-id="231bd-212">예를 들어는 &lt;캐싱&gt; 목록 6에 웹 구성 섹션 Cache1Hour 명명 된 캐시 프로필을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-212">For example, the &lt;caching&gt; web configuration section in Listing 6 defines a cache profile named Cache1Hour.</span></span> <span data-ttu-id="231bd-213">&lt;캐싱&gt; 섹션 내에 나타나야 합니다는 &lt;system.web&gt; 웹 구성 파일의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-213">The &lt;caching&gt; section must appear within the &lt;system.web&gt; section of a web configuration file.</span></span>

<span data-ttu-id="231bd-214">**6-web.config에 대 한 Caching 섹션 나열**</span><span class="sxs-lookup"><span data-stu-id="231bd-214">**Listing 6 – Caching section for web.config**</span></span>

[!code-xml[Main](improving-performance-with-output-caching-vb/samples/sample6.xml)]

<span data-ttu-id="231bd-215">컨트롤러 목록 7에 있는 컨트롤러 작업에 Cache1Hour 프로필을 적용 하는 방법을 보여 줍니다.는 &lt;OutputCache&gt; 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-215">The controller in Listing 7 illustrates how you can apply the Cache1Hour profile to a controller action with the &lt;OutputCache&gt; attribute.</span></span>

<span data-ttu-id="231bd-216">**Listing 7 – Controllers\ProfileController.vb**</span><span class="sxs-lookup"><span data-stu-id="231bd-216">**Listing 7 – Controllers\ProfileController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample7.vb)]

<span data-ttu-id="231bd-217">컨트롤러 목록 7에 의해 노출 되는 index () 동작을 호출 하는 경우 동시 1 시간에 대해 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-217">If you invoke the Index() action exposed by the controller in Listing 7 then the same time will be returned for 1 hour.</span></span>

#### <a name="summary"></a><span data-ttu-id="231bd-218">요약</span><span class="sxs-lookup"><span data-stu-id="231bd-218">Summary</span></span>

<span data-ttu-id="231bd-219">출력 캐싱을 현저 하 게 ASP.NET MVC 응용 프로그램의 성능을 향상 하는 매우 쉬운 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-219">Output caching provides you with a very easy method of dramatically improving the performance of your ASP.NET MVC applications.</span></span> <span data-ttu-id="231bd-220">이 자습서를 사용 하는 방법을 배웠습니다는 &lt;OutputCache&gt; 특성을 컨트롤러 작업의 출력을 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-220">In this tutorial, you learned how to use the &lt;OutputCache&gt; attribute to cache the output of controller actions.</span></span> <span data-ttu-id="231bd-221">또한 속성을 수정 하는 방법을 배웠습니다는 &lt;OutputCache&gt; 콘텐츠 가져옵니다 캐시 하는 방식을 수정 하려면 기간과 VaryByParam 속성 등의 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-221">You also learned how to modify properties of the &lt;OutputCache&gt; attribute such as the Duration and VaryByParam properties to modify how content gets cached.</span></span> <span data-ttu-id="231bd-222">마지막으로, 웹 구성 파일에서 캐시 프로필을 정의 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="231bd-222">Finally, you learned how to define cache profiles in the web configuration file.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="231bd-223">[이전](understanding-action-filters-vb.md)
> [다음](adding-dynamic-content-to-a-cached-page-vb.md)</span><span class="sxs-lookup"><span data-stu-id="231bd-223">[Previous](understanding-action-filters-vb.md)
[Next](adding-dynamic-content-to-a-cached-page-vb.md)</span></span>
