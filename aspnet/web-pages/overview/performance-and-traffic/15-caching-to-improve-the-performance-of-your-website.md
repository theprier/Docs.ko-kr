---
uid: web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
title: (Razor) 사이트 성능 향상을 위해 페이지는 ASP.NET 웹에서 데이터 캐싱 | Microsoft Docs
author: tfitzmac
description: 속도가 빨라질 수 있습니다 웹 사이트-즉, 저장 하 여 캐시에서 검색 하거나 처리 하려면 상당한 시간이 걸리는 일반적으로 데이터의 결과 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/14/2014
ms.topic: article
ms.assetid: 961e525b-7700-469e-8a68-d7010b6fb68c
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
msc.type: authoredcontent
ms.openlocfilehash: 4134c80d7eed4752c90a06aab796a0fd8c2a9782
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37383411"
---
<a name="caching-data-in-an-aspnet-web-pages-razor-site-for-better-performance"></a><span data-ttu-id="81275-103">성능 향상을 위해 ASP.NET 웹 페이지 (Razor) 사이트에서 데이터 캐싱</span><span class="sxs-lookup"><span data-stu-id="81275-103">Caching Data in an ASP.NET Web Pages (Razor) Site for Better Performance</span></span>
====================
<span data-ttu-id="81275-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="81275-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="81275-105">이 문서에서는 ASP.NET Web Pages (Razor) 웹 사이트에서 성능 향상에 대 한 정보를 캐시 하는 도우미를 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-105">This article explains how to use a helper to cache information for faster performance in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="81275-106">저장 하 여 웹 사이트 속도 높일 수 있습니다 &#8212; 즉, 캐시 &#8212; 는 일반적으로 상당한 시간이 걸립니다 받거나 처리 하 고 자주 변경 되지 않는 데이터의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="81275-106">You can speed up your website by having it store &#8212; that is, cache &#8212; the results of data that ordinarily would take considerable time to retrieve or process and that does not change often.</span></span>
> 
> <span data-ttu-id="81275-107">**학습할 내용:**</span><span class="sxs-lookup"><span data-stu-id="81275-107">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="81275-108">웹 사이트의 응답성을 개선 하기 위해 캐싱을 사용 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="81275-108">How to use caching to improve the responsiveness of your website.</span></span>
> 
> <span data-ttu-id="81275-109">다음은 문서에 도입 된 ASP.NET 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="81275-109">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="81275-110">`WebCache` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="81275-110">The `WebCache` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="81275-111">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="81275-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="81275-112">ASP.NET Web Pages (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="81275-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="81275-113">이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>


<span data-ttu-id="81275-114">사이트에서 페이지를 요청이 있을 때마다 웹 서버 요청을 처리 하기 위해 일부 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-114">Every time someone requests a page from your site, the web server has to do some work in order to fulfill the request.</span></span> <span data-ttu-id="81275-115">페이지의 일부 서버 (비교적) 시간이 오래 걸릴, 데이터베이스에서 데이터를 검색 하는 작업을 수행 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81275-115">For some of your pages, the server might have to perform tasks that take a (comparatively) long time, such as retrieving data from a database.</span></span> <span data-ttu-id="81275-116">이러한 작업은 사이트 많은 트래픽이 발생 하는 경우 절대 용어로 장기 사용 하지, 경우에 복잡 하거나 느린 작업을 수행 하려면 웹 서버는 개별 요청에 대 한 전체 계열을 많은 작업을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81275-116">Even if these tasks don't take long in absolute terms, if your site experiences a lot of traffic, a whole series of individual requests that cause the web server to perform the complicated or slow task can add up to a lot of work.</span></span> <span data-ttu-id="81275-117">이 사이트의 성능을 궁극적으로 영향을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81275-117">This can ultimately affect the performance of the site.</span></span>

<span data-ttu-id="81275-118">다음과 같은 상황에서 웹 사이트의 성능을 향상 시키는 한 가지 방법은 데이터를 캐시 하는 경우</span><span class="sxs-lookup"><span data-stu-id="81275-118">One way to improve the performance of your website in circumstances like this is to cache data.</span></span> <span data-ttu-id="81275-119">사이트 가져옵니다 반복된은 같은 정보를 요청 하 고 정보를 각 사용자에 대 한 수정할 필요가 없습니다 시간이 없는 다시 인출 하거나, 다시 계산 하는 대신 중요 한 데이터를 한 번 인출할를 다음 결과 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-119">If your site gets repeated requests for the same information, and the information does not need to be modified for each person, and it's not time sensitive, instead of re-fetching or recalculating it, you can fetch the data once and then store the results.</span></span> <span data-ttu-id="81275-120">다음에는 요청이 들어오면 내용은 수만 가져올 캐시에서.</span><span class="sxs-lookup"><span data-stu-id="81275-120">The next time a request comes in for that information, you just get it out of the cache.</span></span>

<span data-ttu-id="81275-121">일반적으로 자주 변경 되지 않는 정보를 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-121">In general, you cache information that doesn't change frequently.</span></span> <span data-ttu-id="81275-122">캐시에 정보를 배치 하면 웹 서버의 메모리에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81275-122">When you put information in the cache, it's stored in memory on the web server.</span></span> <span data-ttu-id="81275-123">기간 캐시 않아야, 일 시간 (초)에서 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81275-123">You can specify how long it should be cached, from seconds to days.</span></span> <span data-ttu-id="81275-124">캐싱 기간 만료 되 면 캐시에서 정보를 자동으로 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81275-124">When the caching period expires, the information is automatically removed from the cache.</span></span>

> [!NOTE]
> <span data-ttu-id="81275-125">캐시의 항목이 제거 될 수 있습니다 이유로 이외의 만료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="81275-125">Entries in the cache might be removed for reasons other than that they've expired.</span></span> <span data-ttu-id="81275-126">예를 들어, 웹 서버를 일시적으로 발생할 낮은 메모리가 이며 메모리를 회수할 수는 한 가지 방법은 캐시에서 항목을 throw 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-126">For example, the web server might temporarily run low on memory, and one way it can reclaim memory is by throwing entries out of the cache.</span></span> <span data-ttu-id="81275-127">알 수 있듯이, 캐시에 정보를 배치한 경우에, 이것은 필요할 때 되도록 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-127">As you'll see, even if you've put information into the cache, you have to check to be sure it's still there when you need it.</span></span>


<span data-ttu-id="81275-128">웹 사이트에 현재 온도 및 일기 예보를 표시 하는 페이지가 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-128">Imagine your website has a page that displays the current temperature and weather forecast.</span></span> <span data-ttu-id="81275-129">이러한 종류의 정보를 가져오려면 외부 서비스에 요청을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81275-129">To get this type of information, you might send a request to an external service.</span></span> <span data-ttu-id="81275-130">있으므로이 정보 (예를 들어 두 시간 기간) 내 대부분 변경 되지 않습니다 및 외부 호출 시간 및 대역폭이 필요 하므로 캐싱에 적합 한지 합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-130">Since this information doesn't change much (within a two-hour time period, for example) and since external calls require time and bandwidth, it's a good candidate for caching.</span></span>

## <a name="adding-caching-to-a-page"></a><span data-ttu-id="81275-131">페이지에 캐싱 추가</span><span class="sxs-lookup"><span data-stu-id="81275-131">Adding Caching to a Page</span></span>

<span data-ttu-id="81275-132">ASP.NET에 포함 되어는 `WebCache` 쉽게 사이트에 캐싱을 추가 하 고 캐시에 데이터를 추가 하는 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="81275-132">ASP.NET includes a `WebCache` helper that makes it easy to add caching to your site and add data to the cache.</span></span> <span data-ttu-id="81275-133">이 절차에서는 현재 시간을 캐시 하는 페이지를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-133">In this procedure, you'll create a page that caches the current time.</span></span> <span data-ttu-id="81275-134">현재는 종종 변하지와 또한 이것이 계산 하기 복잡 하므로 실제 예에서 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="81275-134">This isn't a real-world example, since the current time is something that does change often, and that moreover isn't complex to calculate.</span></span> <span data-ttu-id="81275-135">그러나 실행 중인 캐싱을 설명 하기 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="81275-135">However, it's a good way to illustrate caching in action.</span></span>

1. <span data-ttu-id="81275-136">명명 된 새 페이지 추가 *WebCache.cshtml* 웹 사이트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81275-136">Add a new page named *WebCache.cshtml* to the website.</span></span>
2. <span data-ttu-id="81275-137">페이지에 다음 코드와 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-137">Add the following code and markup to the page:</span></span>

    [!code-cshtml[Main](15-caching-to-improve-the-performance-of-your-website/samples/sample1.cshtml)]

    <span data-ttu-id="81275-138">데이터를 캐시 하는 경우에 넣기는 이름을 사용 하 여 캐시가는 웹 사이트에서 고유 합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-138">When you cache data, you put it into the cache using a name this is unique across the website.</span></span> <span data-ttu-id="81275-139">이 경우 명명 된 캐시 엔트리를 사용할지 `CachedTime`합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-139">In this case, you'll use a cache entry named `CachedTime`.</span></span> <span data-ttu-id="81275-140">이 `cacheItemKey` 코드 예제에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-140">This is the `cacheItemKey` shown in the code example.</span></span>

    <span data-ttu-id="81275-141">코드를 먼저 읽습니다.는 `CachedTime` 항목을 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-141">The code first reads the `CachedTime` cache entry.</span></span> <span data-ttu-id="81275-142">(즉, 캐시 항목에 없는 경우 null) 값을 반환 되 면 코드 캐시 데이터를 시간 변수 값만 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-142">If a value is returned (that is, if the cache entry isn't null), the code just sets the value of the time variable to the cache data.</span></span>

    <span data-ttu-id="81275-143">그러나 캐시 항목이 존재 하지 않는 경우 (즉, 인 null) 코드 시간 값을 설정, 캐시에 추가 하 고 만료 값을 1 분으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-143">However, if the cache entry doesn't exist (that is, it's null), the code sets the time value, adds it to the cache, and sets an expiration value to one minute.</span></span> <span data-ttu-id="81275-144">1 분 후 캐시 항목 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81275-144">After one minute, the cache entry is discarded.</span></span> <span data-ttu-id="81275-145">(캐시에서 항목에 대 한 만료 기본값은 20 분입니다.) 이 명령은 `WebCache.Set(cacheItemKey, time, 1, false)` 캐시에 현재 시간 값을 추가 하 고 만료 되기 1 분으로 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="81275-145">(The default expiration value for an item in the cache is 20 minutes.) The command `WebCache.Set(cacheItemKey, time, 1, false)` shows how to add the current time value to the cache and set its expiration to 1 minute.</span></span> <span data-ttu-id="81275-146">설정 된 *slidingExpiration* 매개 변수를 `false` 만료 시간을 요청할 때마다 갱신 하지 않으면 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-146">Setting the *slidingExpiration* parameter to `false` means the expiration time is not renewed each time it is requested.</span></span> <span data-ttu-id="81275-147">원래 캐시에 추가 된 후 정확 하 게 1 분 후 만료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81275-147">It will expire exactly 1 minute after it was originally added to the cache.</span></span> <span data-ttu-id="81275-148">이 값을 설정 하는 경우 `true` 1 분의 만료 시간에는 캐시에서 값을 요청할 때마다 다시 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81275-148">If you set this value to `true` the 1 minute expiration time is reset each time the value is requested from the cache.</span></span>

    <span data-ttu-id="81275-149">이 코드에서는 데이터를 캐시 하는 경우 항상 사용 해야 하는 패턴을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="81275-149">This code illustrates the pattern you should always use when you cache data.</span></span> <span data-ttu-id="81275-150">캐시에서 항목을 가져오기 전에 항상 먼저 확인 여부는 `WebCache.Get` 메서드가 null을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-150">Before you get something out of the cache, always check first whether the `WebCache.Get` method has returned null.</span></span> <span data-ttu-id="81275-151">캐시 항목 만료 또는 제거 되었거나 다른 이유로, 지정 된 항목은 캐시 된다는 보장이 없으므로 하므로 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-151">Remember that the cache entry might have expired or might have been removed for some other reason, so any given entry is never guaranteed to be in the cache.</span></span>
3. <span data-ttu-id="81275-152">실행할 *WebCache.cshtml* 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-152">Run *WebCache.cshtml* in a browser.</span></span> <span data-ttu-id="81275-153">(페이지에서 선택한 있는지 확인 합니다 **파일** 실행 하기 전에 작업 영역입니다.) 처음 페이지를 요청할 때는 데이터를 캐시에 없는 및 코드는 시간 값을 캐시에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-153">(Make sure the page is selected in the **Files** workspace before you run it.) The first time you request the page, the time data isn't in the cache, and the code has to add the time value to the cache.</span></span>

    ![캐시-1](15-caching-to-improve-the-performance-of-your-website/_static/image1.jpg)
4. <span data-ttu-id="81275-155">새로 고침 *WebCache.cshtml* 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-155">Refresh *WebCache.cshtml* in the browser.</span></span> <span data-ttu-id="81275-156">이 시간은 데이터를 캐시 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81275-156">This time, the time data is in the cache.</span></span> <span data-ttu-id="81275-157">에 마지막 페이지를 볼 이후 변경 되지 않은 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="81275-157">Notice that the time hasn't changed since the last time you viewed the page.</span></span>

    ![캐시-2](15-caching-to-improve-the-performance-of-your-website/_static/image2.jpg)
5. <span data-ttu-id="81275-159">캐시를 비울 수에 대 일 분 정도 기다린 다음 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="81275-159">Wait one minute for the cache to be emptied, and then refresh the page.</span></span> <span data-ttu-id="81275-160">페이지에는 다시 캐시에 데이터를 찾을 수 없습니다 하 고 업데이트 된 시간이 캐시에 추가 됩니다 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="81275-160">The page again indicates that the time data wasn't found in the cache, and the updated time is added to the cache.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="81275-161">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="81275-161">Additional Resources</span></span>


- [<span data-ttu-id="81275-162">차트에 데이터 표시</span><span class="sxs-lookup"><span data-stu-id="81275-162">Displaying Data in a Chart</span></span>](https://go.microsoft.com/fwlink/?LinkId=202895)
- <span data-ttu-id="81275-163">[WebCache API 참조](https://msdn.microsoft.com/library/system.web.helpers.webcache(v=vs.99).aspx) (MSDN)</span><span class="sxs-lookup"><span data-stu-id="81275-163">[WebCache API reference](https://msdn.microsoft.com/library/system.web.helpers.webcache(v=vs.99).aspx) (MSDN)</span></span>
