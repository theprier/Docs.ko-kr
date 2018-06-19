---
uid: web-pages/overview/performance-and-traffic/14-analyzing-traffic
title: ASP.NET 웹 페이지 (Razor) 사이트에 대 한 추적 방문자 정보 (분석) | Microsoft Docs
author: tfitzmac
description: 라인 웹 사이트를 참조 한 후에 웹 사이트 트래픽을 분석 하는 것이 좋습니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/17/2014
ms.topic: article
ms.assetid: 360bc6e1-84c5-4b8e-a84c-ea48ab807aa4
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/performance-and-traffic/14-analyzing-traffic
msc.type: authoredcontent
ms.openlocfilehash: 9a381ebaed30325fdfa5f0f558910d3002c61559
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
ms.locfileid: "26528762"
---
<a name="tracking-visitor-information-analytics-for-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="020c6-103">ASP.NET 웹 페이지 (Razor) 사이트에 대 한 방문자 정보 (분석)를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-103">Tracking Visitor Information (Analytics) for an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="020c6-104">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="020c6-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="020c6-105">이 문서는 ASP.NET 웹 페이지 (Razor) 웹 사이트의 페이지에 웹 사이트 분석을 추가 하는 도우미를 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-105">This article describes how to use a helper to add website analytics to pages in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="020c6-106">학습 내용:</span><span class="sxs-lookup"><span data-stu-id="020c6-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="020c6-107">웹 사이트 트래픽 정보 분석 공급자를 전송 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="020c6-107">How to send information about your website traffic to an analytics provider.</span></span>
> 
> <span data-ttu-id="020c6-108">다음은 문서에 도입 된 기능을 프로그래밍 하는 ASP.NET입니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-108">These are the ASP.NET programming features introduced in the article:</span></span>
> 
> - <span data-ttu-id="020c6-109">`Analytics` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-109">The `Analytics` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="020c6-110">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="020c6-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="020c6-111">ASP.NET 웹 페이지 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="020c6-111">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="020c6-112">ASP.NET Web Helpers Library (NuGet 패키지)</span><span class="sxs-lookup"><span data-stu-id="020c6-112">ASP.NET Web Helpers Library (NuGet package)</span></span>


<span data-ttu-id="020c6-113">분석은 사용자가 해당 사이트를 사용 하는 방식을 이해할 수 있도록 웹 사이트의 트래픽을 측정 하는 기술에 대 한 일반적인 용어입니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-113">Analytics is a general term for technology that measures traffic on your website so you can understand how people use the site.</span></span> <span data-ttu-id="020c6-114">많은 분석 서비스는 Google, Yahoo, StatCounter, 등에서 서비스를 포함 하 여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-114">Many analytics services are available, including services from Google, Yahoo, StatCounter, and others.</span></span>

<span data-ttu-id="020c6-115">작동 하에 등록할 계정 등록 한다고 가정해 봅시다 사이트 분석 공급자와 함께 하는 방식으로 분석 추적 하려고 합니다. 공급자 ID 또는 계정에 대 한 코드를 추적을 포함 하는 JavaScript 코드의 코드 조각은 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-115">The way analytics works is that you sign up for an account with the analytics provider, where you register the site that you want to track. The provider sends you a snippet of JavaScript code that includes an ID or tracking code for your account.</span></span> <span data-ttu-id="020c6-116">추적 하려는 사이트의 웹 페이지에는 JavaScript 코드 조각을 추가 합니다. (일반적으로 분석 코드 조각을 추가한 바닥글 또는 레이아웃 페이지 또는 사이트의 모든 페이지에 표시 되는 다른 HTML 태그입니다.) 사용자가 이러한 JavaScript 조각 중 하나를 포함 하는 페이지를 요청, 코드 조각을 현재 페이지에 대 한 정보를 페이지에 대 한 다양 한 세부 정보를 기록 하 게 분석 공급자를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-116">You add the JavaScript snippet to the web pages on the site that you want to track. (You typically add the analytics snippet to a footer or layout page or other HTML markup that appears on every page in your site.) When users request a page that contains one of these JavaScript snippets, the snippet sends information about the current page to the analytics provider, who records various details about the page.</span></span>

<span data-ttu-id="020c6-117">사이트 통계를 확인 하려는 경우에 분석 공급자의 웹 사이트에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-117">When you want to have a look at your site statistics, you log into the analytics provider's website.</span></span> <span data-ttu-id="020c6-118">같은 사이트에 대 한 모든 종류의 보고서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-118">You can then view all sorts of reports about your site, like:</span></span>

- <span data-ttu-id="020c6-119">개별 페이지에 대 한 페이지 보기 수입니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-119">The number of page views for individual pages.</span></span> <span data-ttu-id="020c6-120">이 표시는 사이트를 방문 하는 개략적인 얼마나 많은 사람들이 사이트에 해당 페이지가 가장 많이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-120">This tells you (roughly) how many people are visiting the site, and which pages on your site are the most popular.</span></span>
- <span data-ttu-id="020c6-121">시간 사람들은 특정 페이지에 대 한 주입니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-121">How long people spend on specific pages.</span></span> <span data-ttu-id="020c6-122">이 홈 페이지 관심 있는 사람들의 동기화가 있는지 여부 등을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-122">This can tell you things like whether your home page is keeping people's interest.</span></span>
- <span data-ttu-id="020c6-123">사이트를 방문 하기 전에 사이트 사용자에 했습니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-123">What sites people were on before they visited your site.</span></span> <span data-ttu-id="020c6-124">이렇게 하면 트래픽이 검색과 등에서 링크에서 온 것인지 여부를 이해 하는 데 있습니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-124">This helps you understand whether your traffic is coming from links, from searches, and so on.</span></span>
- <span data-ttu-id="020c6-125">사용자 사이트를 방문 하는 경우 및 시간을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-125">When people visit your site and how long they stay.</span></span>
- <span data-ttu-id="020c6-126">어떤 국가에서 방문자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-126">What countries your visitors are from.</span></span>
- <span data-ttu-id="020c6-127">어떤 브라우저와 운영 체제 방문자가 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-127">What browsers and operating systems your visitors are using.</span></span>

    ![Ch14traffic 1](14-analyzing-traffic/_static/image1.jpg)

## <a name="using-a-helper-to-add-analytics-to-a-page"></a><span data-ttu-id="020c6-129">도우미 메서드를 사용 하 여 분석 한 페이지에 추가 하려면</span><span class="sxs-lookup"><span data-stu-id="020c6-129">Using a Helper to Add Analytics to a Page</span></span>

<span data-ttu-id="020c6-130">ASP.NET 웹 페이지에는 여러 가지 분석 도우미가 포함 되어 (`Analytics.GetGoogleHtml`, `Analytics.GetYahooHtml`, 및 `Analytics.GetStatCounterHtml`) 쉽게 분석에 사용 되는 JavaScript 코드 조각을 관리할 수 있도록 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-130">ASP.NET Web Pages includes several analytics helpers (`Analytics.GetGoogleHtml`, `Analytics.GetYahooHtml`, and `Analytics.GetStatCounterHtml`) that make it easy to manage the JavaScript snippets used for analytics.</span></span> <span data-ttu-id="020c6-131">방법 및 위치를 파악 하는 대신 JavaScript 코드에만 하면 됩니다 도우미 페이지에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-131">Instead of figuring out how and where to put the JavaScript code, all you have to do is add the helper to a page.</span></span> <span data-ttu-id="020c6-132">제공 하는 데 필요한 유일한 정보는 계정 이름, ID 또는 추적 코드는 합니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-132">The only information you need to provide is your account name, ID, or tracking code.</span></span> <span data-ttu-id="020c6-133">(StatCounter, 있어 몇 가지 추가 값을 제공 합니다.)</span><span class="sxs-lookup"><span data-stu-id="020c6-133">(For StatCounter, you also have to provide a few additional values.)</span></span>

<span data-ttu-id="020c6-134">이 절차에서 사용 하는 레이아웃 페이지 만듭니다는 `GetGoogleHtml` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-134">In this procedure, you'll create a layout page that uses the `GetGoogleHtml` helper.</span></span> <span data-ttu-id="020c6-135">다른 분석 공급자 중 하나가 지정 된 계정이 이미 있는 경우 해당 계정을 대신 사용할 수 있으며 필요에 따라 약간의 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-135">If you already have an account with one of the other analytics providers, you can use that account instead and make slight adjustments as needed.</span></span>

> [!NOTE]
> <span data-ttu-id="020c6-136">분석 계정을 만들 때 추적 될 사이트의 URL을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-136">When you create an analytics account, you register the URL of the site that you want to be tracking.</span></span> <span data-ttu-id="020c6-137">경우 로컬 컴퓨터의 모든 항목을 테스트 하는, 있하지 않습니다을 추적 하지 (트래픽만 사용자) 실제 트래픽, 사이트 통계를 기록 하 고 봅니다를 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-137">If you're testing everything on your local computer, you won't be tracking actual traffic (the only traffic is you), so you won't be able to record and view site statistics.</span></span> <span data-ttu-id="020c6-138">하지만이 절차는 분석 도우미 페이지에 추가 되는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-138">But this procedure shows how you add an analytics helper to a page.</span></span> <span data-ttu-id="020c6-139">사이트를 게시할 라이브 사이트 분석 공급자에 정보를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-139">When you publish your site, the live site will send information to your analytics provider.</span></span>


1. <span data-ttu-id="020c6-140">에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)추가 하지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="020c6-140">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="020c6-141">Google 웹 로그 분석 계정을 만들고 및 계정 이름을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-141">Create an account with Google Analytics and record the account name.</span></span>
3. <span data-ttu-id="020c6-142">명명 된 레이아웃 페이지 만들기 *Analytics.cshtml* 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-142">Create a layout page named *Analytics.cshtml* and add the following markup:</span></span>

    [!code-cshtml[Main](14-analyzing-traffic/samples/sample1.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="020c6-143">에 대 한 호출을 배치 해야는 `Analytics` 웹 페이지의 본문에는 도우미 (전에 `</body>` 태그).</span><span class="sxs-lookup"><span data-stu-id="020c6-143">You must place the call to the `Analytics` helper in the body of your web page (before the `</body>` tag).</span></span> <span data-ttu-id="020c6-144">그렇지 않은 경우 브라우저는 스크립트를 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-144">Otherwise, the browser will not run the script.</span></span>

    <span data-ttu-id="020c6-145">다른 분석 공급자를 사용 하는 경우 대신 다음 도우미 중 하나:</span><span class="sxs-lookup"><span data-stu-id="020c6-145">If you're using a different analytics provider, use one of the following helpers instead:</span></span>

    - <span data-ttu-id="020c6-146">(Yahoo)`@Analytics.GetYahooHtml("myaccount")`</span><span class="sxs-lookup"><span data-stu-id="020c6-146">(Yahoo) `@Analytics.GetYahooHtml("myaccount")`</span></span>
    - <span data-ttu-id="020c6-147">(StatCounter)`@Analytics.GetStatCounterHtml("project", "security")`</span><span class="sxs-lookup"><span data-stu-id="020c6-147">(StatCounter) `@Analytics.GetStatCounterHtml("project", "security")`</span></span>
4. <span data-ttu-id="020c6-148">대체 `myaccount` 계정, ID 또는 1 단계에서 만든 추적 코드의 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-148">Replace `myaccount` with the name of the account, ID, or tracking code that you created in step 1.</span></span>
5. <span data-ttu-id="020c6-149">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-149">Run the page in the browser.</span></span> <span data-ttu-id="020c6-150">(있는지 확인 페이지에서 선택한는 **파일** 실행 하기 전에 작업 영역입니다.)</span><span class="sxs-lookup"><span data-stu-id="020c6-150">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
6. <span data-ttu-id="020c6-151">브라우저에서 페이지 소스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-151">In the browser, view the page source.</span></span> <span data-ttu-id="020c6-152">렌더링 된 분석 코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-152">You'll be able to see the rendered analytics code:</span></span>

    [!code-html[Main](14-analyzing-traffic/samples/sample2.html)]
7. <span data-ttu-id="020c6-153">Google Analytics 사이트로 하 고 사이트에 대 한 통계를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-153">Log onto the Google Analytics site and examine the statistics for your site.</span></span> <span data-ttu-id="020c6-154">라이브 사이트에서 페이지를 실행할 방문 페이지를 기록 하는 항목이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="020c6-154">If you're running the page on a live site, you see an entry that logs the visit to your page.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="020c6-155">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="020c6-155">Additional Resources</span></span>

- [<span data-ttu-id="020c6-156">Google Analytics 사이트</span><span class="sxs-lookup"><span data-stu-id="020c6-156">Google Analytics site</span></span>](https://www.google.com/analytics/)
- [<span data-ttu-id="020c6-157">Yahoo! 웹 사이트 분석</span><span class="sxs-lookup"><span data-stu-id="020c6-157">Yahoo! Web Analytics site</span></span>](http://help.yahoo.com/l/us/yahoo/ywa/)
- [<span data-ttu-id="020c6-158">StatCounter 사이트</span><span class="sxs-lookup"><span data-stu-id="020c6-158">StatCounter site</span></span>](http://statcounter.com/)
