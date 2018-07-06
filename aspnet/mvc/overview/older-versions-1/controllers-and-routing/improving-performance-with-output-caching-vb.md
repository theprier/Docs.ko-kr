---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
title: 캐싱 (VB)를 출력으로 성능 향상 | Microsoft Docs
author: microsoft
description: 이 자습서에서는 출력 캐싱을 활용 하 여 ASP.NET MVC 웹 응용 프로그램의 성능을 크게 개선할 수 있습니다 하는 방법에 대해 알아봅니다. 하는 중...
ms.author: aspnetcontent
ms.date: 01/27/2009
ms.assetid: 0e7b4d85-2c46-4eaf-b6a8-6cd566a67334
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
msc.type: authoredcontent
ms.openlocfilehash: 72d73067f6f7dabe4644a35c8d9462bfbc7a93ed
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37807332"
---
<a name="improving-performance-with-output-caching-vb"></a><span data-ttu-id="a8473-104">출력 캐싱 (VB)를 사용 하 여 성능 향상</span><span class="sxs-lookup"><span data-stu-id="a8473-104">Improving Performance with Output Caching (VB)</span></span>
====================
<span data-ttu-id="a8473-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="a8473-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="a8473-106">이 자습서에서는 출력 캐싱을 활용 하 여 ASP.NET MVC 웹 응용 프로그램의 성능을 크게 개선할 수 있습니다 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-106">In this tutorial, you learn how you can dramatically improve the performance of your ASP.NET MVC web applications by taking advantage of output caching.</span></span> <span data-ttu-id="a8473-107">동일한 콘텐츠를 각 시간 작업을 호출 하는 새 사용자를 만들 필요가 없습니다 있도록 컨트롤러 작업에서 반환 된 결과 캐시 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-107">You learn how to cache the result returned from a controller action so that the same content does not need to be created each and every time a new user invokes the action.</span></span>


<span data-ttu-id="a8473-108">이 자습서의 목표는 출력 캐시를 활용 하 여 ASP.NET MVC 응용 프로그램의 성능을 크게 개선할 수 있습니다 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-108">The goal of this tutorial is to explain how you can dramatically improve the performance of an ASP.NET MVC application by taking advantage of the output cache.</span></span> <span data-ttu-id="a8473-109">출력 캐시를 사용 하면 컨트롤러 작업에 의해 반환 된 콘텐츠를 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-109">The output cache enables you to cache the content returned by a controller action.</span></span> <span data-ttu-id="a8473-110">이런 방식으로 동일한 콘텐츠를 매번 동일한 컨트롤러 작업이 호출 됩니다 생성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-110">That way, the same content does not need to be generated each and every time the same controller action is invoked.</span></span>

<span data-ttu-id="a8473-111">예를 들어, ASP.NET MVC 응용 프로그램 데이터베이스 레코드의 목록을 Index 라는 보기에 표시 되는지 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-111">Imagine, for example, that your ASP.NET MVC application displays a list of database records in a view named Index.</span></span> <span data-ttu-id="a8473-112">일반적으로 각 시간 인덱스 뷰를 반환 하는 컨트롤러 작업을 호출 하는 사용자는 데이터베이스 레코드 집합을 검색 해야 데이터베이스에서 데이터베이스 쿼리를 실행 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-112">Normally, each and every time that a user invokes the controller action that returns the Index view, the set of database records must be retrieved from the database by executing a database query.</span></span>

<span data-ttu-id="a8473-113">출력 캐시를 활용을 사용 하는 반면, 하는 경우 다음 방지할 수 있습니다 누구나 동일한 컨트롤러 작업을 호출 될 때마다 데이터베이스 쿼리를 실행.</span><span class="sxs-lookup"><span data-stu-id="a8473-113">If, on the other hand, you take advantage of the output cache then you can avoid executing a database query every time any user invokes the same controller action.</span></span> <span data-ttu-id="a8473-114">뷰는 컨트롤러 작업에서 다시 생성 하는 대신 캐시에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-114">The view can be retrieved from the cache instead of being regenerated from the controller action.</span></span> <span data-ttu-id="a8473-115">서버에서 작동 하면 캐싱 수행 중복을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-115">Caching enables you to avoid performing redundant work on the server.</span></span>

#### <a name="enabling-output-caching"></a><span data-ttu-id="a8473-116">출력 캐싱을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="a8473-116">Enabling Output Caching</span></span>

<span data-ttu-id="a8473-117">추가 하 여 출력 캐싱을 사용 하도록 설정 하는 &lt;OutputCache&gt; 개별 컨트롤러 작업 또는 전체 컨트롤러 클래스는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-117">You enable output caching by adding an &lt;OutputCache&gt; attribute to either an individual controller action or an entire controller class.</span></span> <span data-ttu-id="a8473-118">예를 들어 목록 1에서 컨트롤러 index () 라는 작업을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-118">For example, the controller in Listing 1 exposes an action named Index().</span></span> <span data-ttu-id="a8473-119">Index () 작업의 출력은 10 초 동안 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-119">The output of the Index() action is cached for 10 seconds.</span></span>

<span data-ttu-id="a8473-120">**1 – Controllers\HomeController.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="a8473-120">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample1.vb)]


<span data-ttu-id="a8473-121">ASP.NET MVC의 베타 버전에서는 출력 캐싱에 적합 하지 않습니다과 같은 URL [ http://www.MySite.com/ ](http://www.mysite.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-121">In the Beta versions of ASP.NET MVC, output caching does not work for a URL like [http://www.MySite.com/](http://www.mysite.com/).</span></span> <span data-ttu-id="a8473-122">과 같은 URL을 입력 해야 하는 대신 [ http://www.MySite.com/Home/Index ](http://www.mysite.com/Home/Index)합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-122">Instead, you must enter a URL like [http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index).</span></span>


<span data-ttu-id="a8473-123">목록 1의 index () 작업의 출력은 10 초 동안 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-123">In Listing 1, the output of the Index() action is cached for 10 seconds.</span></span> <span data-ttu-id="a8473-124">원하는 경우 훨씬 더 캐시 기간을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-124">If you prefer, you can specify a much longer cache duration.</span></span> <span data-ttu-id="a8473-125">예를 들어, 하루에 대 한 컨트롤러 작업의 출력을 캐시 하려는 경우 다음 지정할 수 있습니다 캐시 기간 86400 초 (60 초 \* 60 분 \* 24).</span><span class="sxs-lookup"><span data-stu-id="a8473-125">For example, if you want to cache the output of a controller action for one day then you can specify a cache duration of 86400 seconds (60 seconds \* 60 minutes \* 24 hours).</span></span>

<span data-ttu-id="a8473-126">콘텐츠가 보장할 수 없습니다 지정 된 시간 동안 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-126">There is no guarantee that content will be cached for the amount of time that you specify.</span></span> <span data-ttu-id="a8473-127">메모리 리소스가 부족 해질, 캐시 제거 콘텐츠가 자동으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-127">When memory resources become low, the cache starts evicting content automatically.</span></span>

<span data-ttu-id="a8473-128">목록 1에서 Home 컨트롤러 목록 2에서 인덱스 뷰를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-128">The Home controller in Listing 1 returns the Index view in Listing 2.</span></span> <span data-ttu-id="a8473-129">이 보기에 대 한 특별 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-129">There is nothing special about this view.</span></span> <span data-ttu-id="a8473-130">인덱스 보기는 현재 시간을 표시 하기만 하면 됩니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="a8473-130">The Index view simply displays the current time (see Figure 1).</span></span>

<span data-ttu-id="a8473-131">**Listing 2 – Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="a8473-131">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](improving-performance-with-output-caching-vb/samples/sample2.aspx)]

<span data-ttu-id="a8473-132">**그림 1-캐시 된 인덱스 뷰**</span><span class="sxs-lookup"><span data-stu-id="a8473-132">**Figure 1 – Cached Index view**</span></span>

![clip_image002](improving-performance-with-output-caching-vb/_static/image1.jpg)

<span data-ttu-id="a8473-134">브라우저의 주소 표시줄에 URL /Home/인덱스를 입력 하 고 반복적으로 다음 인덱스 뷰에서 표시 되는 시간과 브라우저에서 새로 고침/다시 로드 단추에 도달 하 여 index () 작업을 여러 번 호출 하는 경우 10 초 동안 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-134">If you invoke the Index() action multiple times by entering the URL /Home/Index in the address bar of your browser and hitting the Refresh/Reload button in your browser repeatedly, then the time displayed by the Index view won't change for 10 seconds.</span></span> <span data-ttu-id="a8473-135">보기 캐시 되므로 한 번 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-135">The same time is displayed because the view is cached.</span></span>

<span data-ttu-id="a8473-136">동일한 뷰 응용 프로그램을 방문 하는 모든 사람에 대 한 캐시 되는 이해 하는 것이 반드시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-136">It is important to understand that the same view is cached for everyone who visits your application.</span></span> <span data-ttu-id="a8473-137">Index () 작업을 호출 하는 모든 사람이 동일한 캐시 된 버전을 인덱스 뷰의 받습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-137">Anyone who invokes the Index() action will get the same cached version of the Index view.</span></span> <span data-ttu-id="a8473-138">즉, 웹 서버, 인덱스 뷰를 제공 하기 위해 수행 해야 하는 작업의 크기는 크게 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-138">This means that the amount of work that the web server must perform to serve the Index view is dramatically reduced.</span></span>

<span data-ttu-id="a8473-139">매우 간단한 할 일 목록 2 뷰 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-139">The view in Listing 2 happens to be doing something really simple.</span></span> <span data-ttu-id="a8473-140">현재 뷰를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-140">The view just displays the current time.</span></span> <span data-ttu-id="a8473-141">그러나 캐시 된 데이터베이스 레코드 집합을 표시 하는 보기 쉽게 처럼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-141">However, you could just as easily cache a view that displays a set of database records.</span></span> <span data-ttu-id="a8473-142">이 경우 데이터베이스 레코드 집합은 각 시간 보기를 반환 하는 컨트롤러 동작을 호출 하는 데이터베이스에서 검색할 수 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-142">In that case, the set of database records would not need to be retrieved from the database each and every time the controller action that returns the view is invoked.</span></span> <span data-ttu-id="a8473-143">캐싱은 웹 서버와 데이터베이스 서버에서 수행 해야 하는 작업의 양을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-143">Caching can reduce the amount of work that both your web server and database server must perform.</span></span>

<span data-ttu-id="a8473-144">페이지를 사용 하지 마세요 &lt;% @ OutputCache %&gt; MVC 뷰의 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-144">Don't use the page &lt;%@ OutputCache %&gt; directive in an MVC view.</span></span> <span data-ttu-id="a8473-145">이 지시문은 Web Forms를 통해 bleeding는 ASP.NET MVC 응용 프로그램에서는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-145">This directive is bleeding over from the Web Forms world and should not be used in an ASP.NET MVC application.</span></span> 

#### <a name="where-content-is-cached"></a><span data-ttu-id="a8473-146">콘텐츠가 캐시 된</span><span class="sxs-lookup"><span data-stu-id="a8473-146">Where Content is Cached</span></span>

<span data-ttu-id="a8473-147">기본적으로 사용 하는 경우는 &lt;OutputCache&gt; 특성, 콘텐츠 세 위치에 캐시 된: 웹 서버, 모든 프록시 서버 및 웹 브라우저입니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-147">By default, when you use the &lt;OutputCache&gt; attribute, content is cached in three locations: the web server, any proxy servers, and the web browser.</span></span> <span data-ttu-id="a8473-148">콘텐츠의 Location 속성을 수정 하 여 캐시 된 위치에 정확 하 게 제어할 수 있습니다.는 &lt;OutputCache&gt; 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-148">You can control exactly where content is cached by modifying the Location property of the &lt;OutputCache&gt; attribute.</span></span>

<span data-ttu-id="a8473-149">다음 값 중 하나로 Location 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-149">You can set the Location property to any one of the following values:</span></span>

> <span data-ttu-id="a8473-150">· 모든</span><span class="sxs-lookup"><span data-stu-id="a8473-150">· Any</span></span>
> 
> <span data-ttu-id="a8473-151">· 클라이언트</span><span class="sxs-lookup"><span data-stu-id="a8473-151">· Client</span></span>
> 
> <span data-ttu-id="a8473-152">· 다운스트림</span><span class="sxs-lookup"><span data-stu-id="a8473-152">· Downstream</span></span>
> 
> <span data-ttu-id="a8473-153">· 서버</span><span class="sxs-lookup"><span data-stu-id="a8473-153">· Server</span></span>
> 
> <span data-ttu-id="a8473-154">· 없음</span><span class="sxs-lookup"><span data-stu-id="a8473-154">· None</span></span>
> 
> <span data-ttu-id="a8473-155">· ServerAndClient</span><span class="sxs-lookup"><span data-stu-id="a8473-155">· ServerAndClient</span></span>


<span data-ttu-id="a8473-156">기본적으로 위치 속성을 모든 값을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-156">By default, the Location property has the value Any.</span></span> <span data-ttu-id="a8473-157">그러나는 하려는 브라우저 또는 서버에만 캐시 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-157">However, there are situations in which you might want to cache only on the browser or only on the server.</span></span> <span data-ttu-id="a8473-158">예를 들어, 각 사용자에 대 한 개인 설정 되는 정보를 캐시 하는 경우 다음 하면 안됩니다 서버의 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-158">For example, if you are caching information that is personalized for each user then you should not cache the information on the server.</span></span> <span data-ttu-id="a8473-159">다른 사용자에 게 다양 한 정보를 표시 하는 경우 클라이언트에만 정보를 캐시 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-159">If you are displaying different information to different users then you should cache the information only on the client.</span></span>

<span data-ttu-id="a8473-160">예를 들어 목록 3에서 컨트롤러를 현재 사용자 이름을 반환 하는 GetName() 라는 작업을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-160">For example, the controller in Listing 3 exposes an action named GetName() that returns the current user name.</span></span> <span data-ttu-id="a8473-161">Jack 웹 사이트에 로그인 하 고 GetName() 작업을 호출 하는 경우 다음 동작 문자열을 반환 합니다 "Hi Jack"입니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-161">If Jack logs into the website and invokes the GetName() action then the action returns the string "Hi Jack".</span></span> <span data-ttu-id="a8473-162">Jill (질) 웹 사이트에 로그인 하 고 GetName() 작업 호출 이후에 다음 그녀는 또한 받습니다 문자열을 "Hi Jack".</span><span class="sxs-lookup"><span data-stu-id="a8473-162">If, subsequently, Jill logs into the website and invokes the GetName() action then she also will get the string "Hi Jack".</span></span> <span data-ttu-id="a8473-163">문자열은 Jack 컨트롤러 작업을 처음 호출 후 모든 사용자에 대 한 웹 서버에 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-163">The string is cached on the web server for all users after Jack initially invokes the controller action.</span></span>

<span data-ttu-id="a8473-164">**3 – Controllers\BadUserController.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="a8473-164">**Listing 3 – Controllers\BadUserController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample3.vb)]

<span data-ttu-id="a8473-165">대부분의 경우 목록 3의 컨트롤러는 원하는 방식으로 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-165">Most likely, the controller in Listing 3 does not work the way that you want.</span></span> <span data-ttu-id="a8473-166">Jill에 게 "Hi Jack" 메시지를 표시 하지 않으려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-166">You don't want to display the message "Hi Jack" to Jill.</span></span>

<span data-ttu-id="a8473-167">서버 캐시에 콘텐츠를 캐시 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-167">You should never cache personalized content in the server cache.</span></span> <span data-ttu-id="a8473-168">그러나 다음 성능 향상을 위해 브라우저 캐시에 개인 설정 된 콘텐츠를 캐시 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-168">However, you might want to cache the personalized content in the browser cache to improve performance.</span></span> <span data-ttu-id="a8473-169">브라우저에서 콘텐츠를 캐시 하 고 사용자가 여러 번 동일한 컨트롤러 작업을 호출 하는 경우 서버 대신 브라우저 캐시에서 콘텐츠를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-169">If you cache content in the browser, and a user invokes the same controller action multiple times, then the content can be retrieved from the browser cache instead of the server.</span></span>

<span data-ttu-id="a8473-170">목록 4의 수정 된 컨트롤러 GetName() 작업의 출력을 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-170">The modified controller in Listing 4 caches the output of the GetName() action.</span></span> <span data-ttu-id="a8473-171">그러나 콘텐츠는 브라우저 및 서버에 없는 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-171">However, the content is cached only on the browser and not on the server.</span></span> <span data-ttu-id="a8473-172">이런 방식으로 여러 사용자가 GetName() 메서드를 호출 하는 경우, 각 사용자는 자신의 사용자 이름 및 다른 사람의 사용자 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-172">That way, when multiple users invoke the GetName() method, each person gets their own user name and not another person's user name.</span></span>

<span data-ttu-id="a8473-173">**4-Controllers\UserController.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="a8473-173">**Listing 4 – Controllers\UserController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample4.vb)]

<span data-ttu-id="a8473-174">에 &lt;OutputCache&gt; 4 특성 OutputCacheLocation.Client 값으로 설정 된 위치 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-174">Notice that the &lt;OutputCache&gt; attribute in Listing 4 includes a Location property set to the value OutputCacheLocation.Client.</span></span> <span data-ttu-id="a8473-175">합니다 &lt;OutputCache&gt; 특성 NoStore 속성에도 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-175">The &lt;OutputCache&gt; attribute also includes a NoStore property.</span></span> <span data-ttu-id="a8473-176">NoStore 속성은 캐시 된 콘텐츠를의 영구 복사본을 저장 하지 마십시오 프록시 서버와 브라우저 알리는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-176">The NoStore property is used to inform proxy servers and browsers that they should not store a permanent copy of the cached content.</span></span>

#### <a name="varying-the-output-cache"></a><span data-ttu-id="a8473-177">출력 캐시를 변경</span><span class="sxs-lookup"><span data-stu-id="a8473-177">Varying the Output Cache</span></span>

<span data-ttu-id="a8473-178">경우에 따라 다른 캐시 된 버전의 동일한 콘텐츠 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-178">In some situations, you might want different cached versions of the very same content.</span></span> <span data-ttu-id="a8473-179">예를 들어 마스터/세부 정보 페이지를 만든다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-179">Imagine, for example, that you are creating a master/detail page.</span></span> <span data-ttu-id="a8473-180">마스터 페이지에는 영화 제목 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-180">The master page displays a list of movie titles.</span></span> <span data-ttu-id="a8473-181">제목을 클릭 하면 선택한 동영상에 대 한 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-181">When you click a title, you get details for the selected movie.</span></span>

<span data-ttu-id="a8473-182">세부 정보 페이지 캐시 하면, 동일한 동영상에 대 한 세부 정보 클릭 하면 어떤 영화에 관계 없이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-182">If you cache the details page, then the details for the same movie will be displayed no matter which movie you click.</span></span> <span data-ttu-id="a8473-183">첫 번째 사용자가 선택한 첫 번째 영화의 모든 이후 사용자에 게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-183">The first movie selected by the first user will be displayed to all future users.</span></span>

<span data-ttu-id="a8473-184">VaryByParam 속성 활용 하 여이 문제를 해결할 수는 &lt;OutputCache&gt; 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-184">You can fix this problem by taking advantage of the VaryByParam property of the &lt;OutputCache&gt; attribute.</span></span> <span data-ttu-id="a8473-185">이 속성을 사용 하면 서로 다른 캐시 된 버전 때 폼 매개 변수와 동일한 콘텐츠를 만들 수 있습니다 또는 쿼리 문자열 매개 변수 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-185">This property enables you to create different cached versions of the very same content when a form parameter or query string parameter varies.</span></span>

<span data-ttu-id="a8473-186">예를 들어 목록 5의 컨트롤러 Master() 및 Details() 라는 두 가지 작업을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-186">For example, the controller in Listing 5 exposes two actions named Master() and Details().</span></span> <span data-ttu-id="a8473-187">Master() 작업 영화 타이틀의 목록을 반환 하 고 Details() 작업 선택한 동영상에 대 한 세부 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-187">The Master() action returns a list of movie titles and the Details() action returns the details for the selected movie.</span></span>

<span data-ttu-id="a8473-188">**5-Controllers\MoviesController.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="a8473-188">**Listing 5 – Controllers\MoviesController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample5.vb)]

<span data-ttu-id="a8473-189">Master() 동작 값을 사용 하 여 VaryByParam 속성을 포함 "none"입니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-189">The Master() action includes a VaryByParam property with the value "none".</span></span> <span data-ttu-id="a8473-190">작업을 호출할 Master() 동일한 캐시 된 버전의 마스터를 볼 때 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-190">When the Master() action is invoked, the same cached version of the Master view is returned.</span></span> <span data-ttu-id="a8473-191">매개 변수는 모든 형식 매개 변수 또는 쿼리 문자열 무시 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="a8473-191">Any form parameters or query string parameters are ignored (see Figure 2).</span></span>

<span data-ttu-id="a8473-192">**그림 2 – /Movies/Master 보기**</span><span class="sxs-lookup"><span data-stu-id="a8473-192">**Figure 2 – The /Movies/Master view**</span></span>

![clip_image004](improving-performance-with-output-caching-vb/_static/image2.jpg)

<span data-ttu-id="a8473-194">**그림 3 – / Movies/세부 정보 보기**</span><span class="sxs-lookup"><span data-stu-id="a8473-194">**Figure 3 – The /Movies/Details view**</span></span>

![clip_image006](improving-performance-with-output-caching-vb/_static/image3.jpg)

<span data-ttu-id="a8473-196">Details() 작업에는 "Id" 값을 사용 하 여 VaryByParam 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-196">The Details() action includes a VaryByParam property with the value "Id".</span></span> <span data-ttu-id="a8473-197">Id 매개 변수에 다른 값 컨트롤러 작업에 전달 하는 경우 다른 캐시 된 버전의 세부 정보 보기 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-197">When different values of the Id parameter are passed to the controller action, different cached versions of the Details view are generated.</span></span>

<span data-ttu-id="a8473-198">것이 줄이고 이상의 캐싱 VaryByParam 속성 결과 사용 하는 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-198">It is important to understand that using the VaryByParam property results in more caching and not less.</span></span> <span data-ttu-id="a8473-199">자세히 보기의 다른 캐시 된 버전의 Id 매개 변수에 각 버전에 대해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-199">A different cached version of the Details view is created for each different version of the Id parameter.</span></span>

<span data-ttu-id="a8473-200">VaryByParam 속성은 다음 값으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-200">You can set the VaryByParam property to the following values:</span></span>

> <span data-ttu-id="a8473-201">\* = 폼 또는 쿼리 문자열 매개 변수 다릅니다 때마다 다른 캐시 된 버전을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-201">\* = Create a different cached version whenever a form or query string parameter varies.</span></span>
> 
> <span data-ttu-id="a8473-202">none = 사용 안 함 다양 한 캐시 된 버전을 만들려면</span><span class="sxs-lookup"><span data-stu-id="a8473-202">none = Never create different cached versions</span></span>
> 
> <span data-ttu-id="a8473-203">매개 변수 목록을 세미콜론으로 폼 또는 쿼리 문자열 매개 변수 목록의 다릅니다 때마다 다른 캐시 된 버전을 만들기 =</span><span class="sxs-lookup"><span data-stu-id="a8473-203">Semicolon list of parameters = Create different cached versions whenever any of the form or query string parameters in the list varies</span></span>


#### <a name="creating-a-cache-profile"></a><span data-ttu-id="a8473-204">캐시 프로필 만들기</span><span class="sxs-lookup"><span data-stu-id="a8473-204">Creating a Cache Profile</span></span>

<span data-ttu-id="a8473-205">속성을 수정 하 여 출력 캐시 속성을 구성 하는 대신 합니다 &lt;OutputCache&gt; 특성인 웹 구성 (web.config) 파일에서 캐시 프로필을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-205">As an alternative to configuring output cache properties by modifying properties of the &lt;OutputCache&gt; attribute, you can create a cache profile in the web configuration (web.config) file.</span></span> <span data-ttu-id="a8473-206">웹 구성 파일에서 캐시 프로필을 만드는 몇 가지 중요 한 이점 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-206">Creating a cache profile in the web configuration file offers a couple of important advantages.</span></span>

<span data-ttu-id="a8473-207">첫째, 웹 구성 파일에서 출력 캐시를 구성 하 여 컨트롤러 작업에서 하나의 중앙 위치에서 콘텐츠를 캐시 하는 방법을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-207">First, by configuring output caching in the web configuration file, you can control how controller actions cache content in one central location.</span></span> <span data-ttu-id="a8473-208">캐시 프로필을 두 개 만들고 여러 컨트롤러 또는 컨트롤러 작업 프로필을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-208">You can create one cache profile and apply the profile to several controllers or controller actions.</span></span>

<span data-ttu-id="a8473-209">둘째, 응용 프로그램을 다시 컴파일하지 않고 웹 구성 파일을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-209">Second, you can modify the web configuration file without recompiling your application.</span></span> <span data-ttu-id="a8473-210">프로덕션 환경에 이미 배포 된 응용 프로그램에 대 한 캐싱을 사용 하지 않도록 설정 해야 할 경우 다음 수정할 수 있습니다 단순히 웹 구성 파일에 정의 된 캐시 프로필.</span><span class="sxs-lookup"><span data-stu-id="a8473-210">If you need to disable caching for an application that has already been deployed to production, then you can simply modify the cache profiles defined in the web configuration file.</span></span> <span data-ttu-id="a8473-211">웹 구성 파일에 변경 내용을 자동으로 검색 되어 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-211">Any changes to the web configuration file will be detected automatically and applied.</span></span>

<span data-ttu-id="a8473-212">예를 들어 합니다 &lt;캐싱&gt; Cache1Hour 명명 된 캐시 프로필을 정의 하는 웹 구성 섹션 6 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-212">For example, the &lt;caching&gt; web configuration section in Listing 6 defines a cache profile named Cache1Hour.</span></span> <span data-ttu-id="a8473-213">합니다 &lt;캐싱&gt; 섹션 내에 나타나야 합니다 합니다 &lt;system.web&gt; 웹 구성 파일의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-213">The &lt;caching&gt; section must appear within the &lt;system.web&gt; section of a web configuration file.</span></span>

<span data-ttu-id="a8473-214">**코드 6 – web.config에 대 한 캐싱 섹션**</span><span class="sxs-lookup"><span data-stu-id="a8473-214">**Listing 6 – Caching section for web.config**</span></span>

[!code-xml[Main](improving-performance-with-output-caching-vb/samples/sample6.xml)]

<span data-ttu-id="a8473-215">7의 컨트롤러 Cache1Hour 프로필을 사용 하 여 컨트롤러 작업에 적용 하는 방법을 보여 줍니다.는 &lt;OutputCache&gt; 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-215">The controller in Listing 7 illustrates how you can apply the Cache1Hour profile to a controller action with the &lt;OutputCache&gt; attribute.</span></span>

<span data-ttu-id="a8473-216">**Listing 7 – Controllers\ProfileController.vb**</span><span class="sxs-lookup"><span data-stu-id="a8473-216">**Listing 7 – Controllers\ProfileController.vb**</span></span>

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample7.vb)]

<span data-ttu-id="a8473-217">7의 컨트롤러에 의해 노출 index () 작업을 호출 하는 경우 동시는 1 시간 동안 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-217">If you invoke the Index() action exposed by the controller in Listing 7 then the same time will be returned for 1 hour.</span></span>

#### <a name="summary"></a><span data-ttu-id="a8473-218">요약</span><span class="sxs-lookup"><span data-stu-id="a8473-218">Summary</span></span>

<span data-ttu-id="a8473-219">출력 캐싱을 크게 ASP.NET MVC 응용 프로그램의 성능을 향상 시키기 위해 쉽게 메서드를 사용 하 여 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-219">Output caching provides you with a very easy method of dramatically improving the performance of your ASP.NET MVC applications.</span></span> <span data-ttu-id="a8473-220">이 자습서에서는 사용 하는 방법을 배웠습니다 합니다 &lt;OutputCache&gt; 특성을 컨트롤러 작업의 출력을 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-220">In this tutorial, you learned how to use the &lt;OutputCache&gt; attribute to cache the output of controller actions.</span></span> <span data-ttu-id="a8473-221">또한 속성을 수정 하는 방법을 배웠습니다 합니다 &lt;OutputCache&gt; 콘텐츠가 캐시 되는 방식을 수정 하려면 기간과 VaryByParam 속성과 같은 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-221">You also learned how to modify properties of the &lt;OutputCache&gt; attribute such as the Duration and VaryByParam properties to modify how content gets cached.</span></span> <span data-ttu-id="a8473-222">마지막으로 웹 구성 파일에서 캐시 프로필을 정의 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="a8473-222">Finally, you learned how to define cache profiles in the web configuration file.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a8473-223">[이전](understanding-action-filters-vb.md)
> [다음](adding-dynamic-content-to-a-cached-page-vb.md)</span><span class="sxs-lookup"><span data-stu-id="a8473-223">[Previous](understanding-action-filters-vb.md)
[Next](adding-dynamic-content-to-a-cached-page-vb.md)</span></span>
