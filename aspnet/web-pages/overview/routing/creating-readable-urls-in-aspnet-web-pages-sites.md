---
uid: web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
title: 페이지 (Razor) 사이트를 ASP.NET 웹에서 읽을 수 있는 Url을 만들면 | Microsoft Docs
author: tfitzmac
description: 이 문서는 ASP.NET 웹 페이지 (Razor) 웹 사이트 및 어떻게 이렇게 하면 더 쉽게 읽고 SEO에 더 나은 있는 Url을 사용 하 여의 라우팅 설명 합니다. 합니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/17/2014
ms.topic: article
ms.assetid: a8aac1ac-89de-4415-afe0-97a41c6423d2
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: 7858b7cbd6dccafb2867ed9a1d102561e211e435
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
ms.locfileid: "26529752"
---
<a name="creating-readable-urls-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="091f0-104">ASP.NET 웹 페이지 (Razor) 사이트에서 읽을 수 있는 Url 만들기</span><span class="sxs-lookup"><span data-stu-id="091f0-104">Creating Readable URLs in ASP.NET Web Pages (Razor) Sites</span></span>
====================
<span data-ttu-id="091f0-105">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="091f0-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="091f0-106">이 문서는 ASP.NET 웹 페이지 (Razor) 웹 사이트 및 어떻게 이렇게 하면 더 쉽게 읽고 SEO에 더 나은 있는 Url을 사용 하 여의 라우팅 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-106">This article describes routing in an ASP.NET Web Pages (Razor) website, and how this lets you use URLs that are more readable and better for SEO.</span></span>
> 
> <span data-ttu-id="091f0-107">학습 내용:</span><span class="sxs-lookup"><span data-stu-id="091f0-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="091f0-108">ASP.NET 사용 하는 방법 라우팅 보다 읽기 쉽고 검색 가능한 Url을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-108">How ASP.NET uses routing to let you use more readable and searchable URLs.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="091f0-109">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="091f0-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="091f0-110">ASP.NET 웹 페이지 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="091f0-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="091f0-111">이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>


## <a name="about-routing"></a><span data-ttu-id="091f0-112">라우팅에 대 한</span><span class="sxs-lookup"><span data-stu-id="091f0-112">About Routing</span></span>

<span data-ttu-id="091f0-113">사이트의 페이지에 대 한 Url 얼마나 잘 사이트 작동에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-113">The URLs for the pages in your site can have an impact on how well the site works.</span></span> <span data-ttu-id="091f0-114">URL을 &quot;친숙 한&quot; 사이트를 사용 하기 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-114">A URL that's &quot;friendly&quot; can make it easier for people to use the site.</span></span> <span data-ttu-id="091f0-115">사이트에 대 한 검색 엔진 최적화 (SEO)와 함께 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-115">It can also help with search-engine optimization (SEO) for the site.</span></span> <span data-ttu-id="091f0-116">ASP.NET 웹 사이트는 친화적 Url을 자동으로 사용 하는 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-116">ASP.NET websites include the ability to use friendly URLs automatically.</span></span>

<span data-ttu-id="091f0-117">ASP.NET에는 방금 서버에서 파일을 가리키는 대신 사용자 조치에 설명 하는 의미 있는 Url을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-117">ASP.NET lets you create meaningful URLs that describe user actions instead of just pointing to a file on the server.</span></span> <span data-ttu-id="091f0-118">이러한 Url에 대해 고려할 가상의 블로그:</span><span class="sxs-lookup"><span data-stu-id="091f0-118">Consider these URLs for a fictional blog:</span></span>

- `http://www.contoso.com/Blog/blog.cshtml?categories=hardware`
- `http://www.contoso.com//Blog/blog.cshtml?startdate=2009-11-01&enddate=2009-11-30`

<span data-ttu-id="091f0-119">다음 항목에 해당 Url을 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-119">Compare those URLs to the following ones:</span></span>

- `http://www.contoso.com/Blog/categories/hardware/`
- `http://www.contoso.com/Blog/2009/November`

<span data-ttu-id="091f0-120">첫 번째 쌍에서 사용자 알고 있어야 합니다 블로그를 사용 하 여 표시 되는 *blog.cshtml* 페이지와 오른쪽 범주 또는 날짜 범위를 가져오는 쿼리 문자열을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-120">In the first pair, a user would have to know that the blog is displayed using the *blog.cshtml* page, and would then have to construct a query string that gets the right category or date range.</span></span> <span data-ttu-id="091f0-121">두 번째 예제 집합 이해 하 고 만드는 훨씬 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-121">The second set of examples is much easier to comprehend and create.</span></span>

<span data-ttu-id="091f0-122">또한 첫 번째 예에 대 한 Url을 특정 파일에 직접 가리키도록 (*blog.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="091f0-122">The URLs for the first example also point directly to a specific file (*blog.cshtml*).</span></span> <span data-ttu-id="091f0-123">어떤 이유로 블로그 이동 된 경우 다른 폴더를 서버에서 나 블로그 다른 페이지를 사용 하도록 다시 작성 된 경우 링크는 잘못 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-123">If for some reason the blog were moved to another folder on the server, or if the blog were rewritten to use a different page, the links would be wrong.</span></span> <span data-ttu-id="091f0-124">Url의 두 번째 집합은 특정 페이지를 가리키지 않습니다. 하더라도 블로그 구현 또는 위치 변경, Url은의 결과가 계속 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-124">The second set of URLs doesn't point to a specific page, so even if the blog implementation or location changes, the URLs would still be valid.</span></span>

<span data-ttu-id="091f0-125">ASP.NET 웹 페이지에서 ASP.NET을 사용 하기 때문에 위의 예제에서와 같이 친숙 한 Url을 만들 수 있습니다 *라우팅*합니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-125">In ASP.NET Web Pages, you can create friendlier URLs like those in the above examples because ASP.NET uses *routing*.</span></span> <span data-ttu-id="091f0-126">라우팅 요청을 수행할 수 있는 페이지 (또는 페이지)에 URL에서 논리적 매핑을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-126">Routing creates logical mapping from a URL to a page (or pages) that can fulfill the request.</span></span> <span data-ttu-id="091f0-127">매핑이 논리 이므로 (하지 물리적, 특정 파일에), 라우팅은 다양 한 사이트에 대 한 Url을 정의 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-127">Because the mapping is logical (not physical, to a specific file), routing provides great flexibility in how you define the URLs for your site.</span></span>

## <a name="how-routing-works"></a><span data-ttu-id="091f0-128">라우팅의 작동 원리</span><span class="sxs-lookup"><span data-stu-id="091f0-128">How Routing Works</span></span>

<span data-ttu-id="091f0-129">ASP.NET 요청을 처리할 때 URL을 전달 하는 방법을 결정 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-129">When ASP.NET processes a request, it reads the URL to determine how to route it.</span></span> <span data-ttu-id="091f0-130">ASP.NET 때 개별 세그먼트에 대 한 URL 디스크의 파일에서 왼쪽에서 오른쪽으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-130">ASP.NET tries to match individual segments of the URL to files on disk, going from left to right.</span></span> <span data-ttu-id="091f0-131">일치 하는 경우 페이지를 전달 되는 URL에 남아 있는 모든 항목 *경로 정보*합니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-131">If there's a match, anything remaining in the URL is passed to the page as *path information*.</span></span>

<span data-ttu-id="091f0-132">다른 사용자가이 URL을 사용 하 여 요청을 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-132">Imagine that someone makes a request using this URL:</span></span>

`http://www.contoso.com/a/b/c`

<span data-ttu-id="091f0-133">검색을 다음과 같이 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-133">The search goes like this:</span></span>

1. <span data-ttu-id="091f0-134">파일의 이름 및 경로 거기 */a/b/c.cshtml*?</span><span class="sxs-lookup"><span data-stu-id="091f0-134">Is there a file with the path and name of */a/b/c.cshtml*?</span></span> <span data-ttu-id="091f0-135">이 경우 해당 페이지를 실행 하 고 없는 정보를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-135">If so, run that page and pass no information to it.</span></span> <span data-ttu-id="091f0-136">그렇지 않은 경우...</span><span class="sxs-lookup"><span data-stu-id="091f0-136">Otherwise ...</span></span>
2. <span data-ttu-id="091f0-137">파일의 이름 및 경로 거기 */a/b.cshtml*?</span><span class="sxs-lookup"><span data-stu-id="091f0-137">Is there a file with the path and name of */a/b.cshtml*?</span></span> <span data-ttu-id="091f0-138">따라서 해당 페이지를 실행 하 고 값을 전달 하는 경우 `c` 를 합니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-138">If so, run that page and pass the value `c` to it.</span></span> <span data-ttu-id="091f0-139">그렇지 않은 경우...</span><span class="sxs-lookup"><span data-stu-id="091f0-139">Otherwise …</span></span>
3. <span data-ttu-id="091f0-140">파일의 이름 및 경로 거기 */a.cshtml*?</span><span class="sxs-lookup"><span data-stu-id="091f0-140">Is there a file with the path and name of */a.cshtml*?</span></span> <span data-ttu-id="091f0-141">따라서 해당 페이지를 실행 하 고 값을 전달 하는 경우 `b/c` 를 합니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-141">If so, run that page and pass the value `b/c` to it.</span></span>

<span data-ttu-id="091f0-142">더 정확 하 게 찾을 수 검색에 대 한 일치 하는 경우 *.cshtml* 가 지정 된 폴더의 파일, ASP.NET 계속 이러한 파일에 대 한 차례로 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-142">If the search found no exact matches for *.cshtml* files in their specified folders, ASP.NET continues looking for these files in turn:</span></span>

1. <span data-ttu-id="091f0-143">*/a/b/c/default.cshtml* (경로 정보 없음).</span><span class="sxs-lookup"><span data-stu-id="091f0-143">*/a/b/c/default.cshtml* (no path information).</span></span>
2. <span data-ttu-id="091f0-144">*/a/b/c/index.cshtml* (경로 정보 없음).</span><span class="sxs-lookup"><span data-stu-id="091f0-144">*/a/b/c/index.cshtml* (no path information).</span></span>

> [!NOTE]
> <span data-ttu-id="091f0-145">분명히, 특정 페이지에 대 한 요청 (즉, 포함 된 요청이 *.cshtml* 파일 이름 확장명) 예상 하는 것 처럼 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-145">To be clear, requests for specific pages (that is, requests that include the *.cshtml* filename extension) work just like you'd expect.</span></span> <span data-ttu-id="091f0-146">요청을 같은 `http://www.contoso.com/a/b.cshtml` 페이지를 실행 *b.cshtml* 제대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-146">A request like `http://www.contoso.com/a/b.cshtml` will run the page *b.cshtml* just fine.</span></span>


<span data-ttu-id="091f0-147">페이지, 내부 페이지의를 통해 경로 정보를 얻을 수 `UrlData` 속성이 사전 설정 되어 만들어져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-147">Inside a page, you can get the path information via the page's `UrlData` property, which is a dictionary.</span></span> <span data-ttu-id="091f0-148">라는 파일이 있다고 가정해 보세요. *ViewCustomers.cshtml* 사이트가이 요청을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-148">Imagine that you have a file named *ViewCustomers.cshtml* and your site gets this request:</span></span>

`http://mysite.com/myWebSite/ViewCustomers/1000`

<span data-ttu-id="091f0-149">위 규칙에 표시 된 것과 같이 페이지 요청이 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-149">As described in the rules above, the request will go to your page.</span></span> <span data-ttu-id="091f0-150">다음 페이지를 가져와 경로 정보를 표시 하는 다음과 같은 코드를 사용할 수 있습니다 (이 경우 값 &quot;1000&quot;):</span><span class="sxs-lookup"><span data-stu-id="091f0-150">Inside the page, you can use code like the following to get and display the path information (in this case, the value &quot;1000&quot;):</span></span>

[!code-html[Main](creating-readable-urls-in-aspnet-web-pages-sites/samples/sample1.html)]

> [!NOTE]
> <span data-ttu-id="091f0-151">라우팅 전체 파일 이름을 포함 하지 않습니다, 때문에 있을 수 있습니다 모호성으로 인해 동일한 페이지가 있는 경우 이름 하지만 서로 다른 파일 이름 확장명 (예를 들어 *MyPage.cshtml* 및 *MyPage.html*) .</span><span class="sxs-lookup"><span data-stu-id="091f0-151">Because routing doesn't involve complete file names, there can be ambiguity if you have pages that have the same name but different file-name extensions (for example, *MyPage.cshtml* and *MyPage.html*).</span></span> <span data-ttu-id="091f0-152">라우팅을 사용 하 여 문제를 방지 하기 위해서는 없는지 페이지 이름이 해당 확장만 다른 사이트에 있는지 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-152">In order to avoid problems with routing, it's best to make sure that you don't have pages in your site whose names differ only in their extension.</span></span>


<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="091f0-153">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="091f0-153">Additional Resources</span></span>

<span data-ttu-id="091f0-154">[WebMatrix-Url, UrlData 및 SEO에 대 한 라우팅](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO)합니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-154">[WebMatrix - URLs, UrlData and Routing for SEO](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO).</span></span> <span data-ttu-id="091f0-155">Mike Brind 하 여이 블로그 항목 라우팅의 작동 원리 ASP.NET 웹 페이지에 대 한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="091f0-155">This blog entry by Mike Brind provides some additional details on how routing works in ASP.NET Web Pages.</span></span>
