---
uid: web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
title: 페이지 (Razor) 사이트를 ASP.NET 웹에 소셜 네트워킹 추가 | Microsoft Docs
author: tfitzmac
description: 이 소셜 네트워킹 서비스를 사용 하 여 사이트를 통합 하는 방법을 설명 합니다. 이 장에서 웹 사이트에 대 한 책갈피/링크 수 있게 하는 방법을 배웁니다...
ms.author: aspnetcontent
ms.date: 02/21/2014
ms.assetid: 03c342f9-b35c-4d7c-b9ed-cd9aaaffedb6
msc.legacyurl: /web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: e50a35d9770da247d18bbe1b3660b7bd5d46d8e9
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37822446"
---
<a name="adding-social-networking-to-aspnet-web-pages-razor-sites"></a><span data-ttu-id="d2918-104">소셜 네트워킹 ASP.NET 웹 페이지 (Razor) 사이트 추가</span><span class="sxs-lookup"><span data-stu-id="d2918-104">Adding Social Networking to ASP.NET Web Pages (Razor) Sites</span></span>
====================
<span data-ttu-id="d2918-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="d2918-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="d2918-106">이 문서는 ASP.NET Web Pages (Razor) 웹 사이트의 페이지에 Facebook, Twitter, Reddit, 및 Digg에 대 한 소셜 네트워킹 링크를 추가 하는 방법 및 Twitter 피드, Xbox 게이머 카드 및 Gravatar 이미지를 포함 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-106">This article explains how to add social networking links for Facebook, Twitter, Reddit, and Digg to pages in an ASP.NET Web Pages (Razor) website, and how to include Twitter feeds, Xbox gamer cards, and Gravatar images.</span></span>
> 
> <span data-ttu-id="d2918-107">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="d2918-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="d2918-108">책갈피/링크 사이트 사용자에 게는 한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-108">How to let people bookmark/link your site.</span></span>
> - <span data-ttu-id="d2918-109">Twitter 피드를 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-109">How to add a Twitter feed.</span></span>
> - <span data-ttu-id="d2918-110">Facebook을 추가 하는 방법 **같은** 페이지에는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-110">How to add a Facebook **Like** button to pages.</span></span>
> - <span data-ttu-id="d2918-111">Gravatar.com 이미지를 렌더링 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-111">How to render Gravatar.com images.</span></span>
> - <span data-ttu-id="d2918-112">사이트에는 Xbox 게이머 카드를 표시 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="d2918-112">How to display an Xbox gamer card on your site.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="d2918-113">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="d2918-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="d2918-114">ASP.NET Web Pages (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="d2918-114">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="d2918-115">ASP.NET 웹 도우미 라이브러리 (NuGet 패키지)</span><span class="sxs-lookup"><span data-stu-id="d2918-115">ASP.NET Web Helper Library (NuGet package)</span></span>
>   
> 
> <span data-ttu-id="d2918-116">이 자습서는 또한 ASP.NET 웹 도우미 라이브러리를 사용 하는 일부 제외 하 고 ASP.NET 웹 페이지 3을 사용 하 여 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-116">This tutorial also works with ASP.NET Web Pages 3, except for parts that use the ASP.NET Web Helper Library.</span></span>


<a id="Linking_Your_Website"></a>
## <a name="linking-your-website-on-social-networking-sites"></a><span data-ttu-id="d2918-117">소셜 네트워킹 사이트에서 웹 사이트를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-117">Linking Your Website on Social Networking Sites</span></span>

<span data-ttu-id="d2918-118">사용자와 같은 사이트에서 어떤 일을 하는 경우 종종 친구 들과 공유 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-118">If people like something on your site, they often want to share it with friends.</span></span> <span data-ttu-id="d2918-119">가능이 쉬운 사용자가 클릭 하 여 Digg, Reddit, Facebook, Twitter 또는 유사한 사이트에서 페이지를 공유할 수 있는 문자 (아이콘)를 표시 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-119">You can make this easy by displaying glyphs (icons) that people can click to share a page on Digg, Reddit, Facebook, Twitter, or similar sites.</span></span>

<span data-ttu-id="d2918-120">이러한 문자 모양을 표시 하려면 추가 `LinkSharecode` 페이지로 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-120">To display these glyphs, add the `LinkSharecode` helper to a page.</span></span> <span data-ttu-id="d2918-121">페이지를 방문 하는 사용자는 개별 문자 모양을 클릭 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-121">People who visit your page can click an individual glyph.</span></span> <span data-ttu-id="d2918-122">해당 소셜 네트워킹 사이트에 계정이 있으면 다음 해당 사이트의 페이지에 대 한 링크를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-122">If they have an account with that social networking site, they can then post a link to your page on that site.</span></span>

![그림 1](13-adding-social-networking-to-your-web-site/_static/image1.jpg)

1. <span data-ttu-id="d2918-124">에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)하십시오.-추가 하지 않은 경우 라는 페이지를 만듭니다 *ListLinkShare.cshtml* 추가 다음 태그:</span><span class="sxs-lookup"><span data-stu-id="d2918-124">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.- Create a page named *ListLinkShare.cshtml* and add the following markup:</span></span>

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample1.cshtml)]

    <span data-ttu-id="d2918-125">이 예제의 경우는 `LinkShare` 도우미 실행 페이지 제목을 소셜 네트워킹 사이트 페이지 제목을 전달 매개 변수로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-125">In this example, when the `LinkShare` helper runs, the page title is passed as a parameter, which in turn passes the page title to the social networking site.</span></span> <span data-ttu-id="d2918-126">그러나 원하는 모든 문자열에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-126">However, you could pass in any string you want.</span></span> <span data-ttu-id="d2918-127">이 예제는 또한 목록에 포함 하는 소셜 네트워킹 사이트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-127">This example also specifies which social networking sites to include in the list.</span></span> <span data-ttu-id="d2918-128">사이트에 관련 된 소셜 네트워킹 사이트를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-128">You can specify the social networking sites that are relevant to your site.</span></span>
2. <span data-ttu-id="d2918-129">실행 합니다 *ListLinkShare.cshtml* 브라우저에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-129">Run the *ListLinkShare.cshtml* page in a browser.</span></span> <span data-ttu-id="d2918-130">(페이지에서 선택한 있는지 확인 합니다 **파일** 실행 하기 전에 작업 영역입니다.)</span><span class="sxs-lookup"><span data-stu-id="d2918-130">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
3. <span data-ttu-id="d2918-131">에 등록 되셨습니다는 사이트 중 하나에 대 한 문자 모양을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-131">Click a glyph for one of the sites that you're signed up for.</span></span> <span data-ttu-id="d2918-132">링크는 페이지를 공유할 수 있는 선택한 소셜 네트워크 사이트에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-132">The link takes you to the page on the selected social network site where you can share a link.</span></span> <span data-ttu-id="d2918-133">예를 들어, Reddit 링크를 클릭 하면 이동 하면는 `submit to reddit` Reddit 웹 사이트의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-133">For example, if you click the Reddit link, you're taken to the `submit to reddit` page on the Reddit website.</span></span>

     ![그림 2](13-adding-social-networking-to-your-web-site/_static/image2.jpg)

<a id="Adding_a_Twitter_Feed"></a>
## <a name="adding-a-twitter-feed"></a><span data-ttu-id="d2918-135">피드는 Twitter 추가</span><span class="sxs-lookup"><span data-stu-id="d2918-135">Adding a Twitter Feed</span></span>

<span data-ttu-id="d2918-136">Twitter API의 현재 버전과 호환 되는 Twitter 도우미를 사용 하는 방법에 대 한 내용은 [Twitter 도우미](../ui-layouts-and-themes/twitter-helper.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-136">For information about using a Twitter helper that is compatible with the current version of the Twitter API, see [Twitter helper](../ui-layouts-and-themes/twitter-helper.md).</span></span> <span data-ttu-id="d2918-137">이 예제에서는 여러 페이지에서 코드를 쉽게 다시 사용할 수 있도록 고유한 도우미를 작성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-137">This example shows how to write your own helper so you can easily reuse the code from many pages.</span></span>

<a id="Displaying_a_Facebook_Button"></a>
## <a name="displaying-a-facebook-quotlikequot-button"></a><span data-ttu-id="d2918-138">Facebook 표시 &quot;같은&quot; 단추</span><span class="sxs-lookup"><span data-stu-id="d2918-138">Displaying a Facebook &quot;Like&quot; Button</span></span>

<span data-ttu-id="d2918-139">경우에 따라 것이 가장 좋은 도우미에 의존 하는 것이 아니라 소셜 네트워킹 공급자에서 직접 코드를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-139">In some cases, your best option is to get the code directly from the social networking provider rather than relying on a helper.</span></span> <span data-ttu-id="d2918-140">소셜 네트워크 공급자 도우미는 업데이트 보다 더 빨리 해당 옵션을 업데이트 하는 경우 특히 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-140">This is especially true if the social network provider updates its options more quickly than the helper is updated.</span></span>

<span data-ttu-id="d2918-141">Facebook 기능 (예: Like 단추)에 사이트를 추가 하려면 코드 조각에서 검색할 수 있습니다 합니다 [developers.facebook.com](https://developers.facebook.com/) 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-141">To add Facebook features (such as the Like button) to your site, you can retrieve code snippets from the [developers.facebook.com](https://developers.facebook.com/) site.</span></span> <span data-ttu-id="d2918-142">Facebook 사이트에서 사이트와 관련 된 코드를 생성 하는 도구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-142">On the Facebook site, you use their tools to generate a code snippet that is relevant to your site.</span></span>

<span data-ttu-id="d2918-143">다음 강조 표시 된 코드는 developers.facebook.com 사이트 단추와 같은 도구에서 검색 된 코드가입니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-143">The following highlighted code is the code that was retrieved from the Like Button tool on the developers.facebook.com site.</span></span> <span data-ttu-id="d2918-144">사용자 고유의 앱 ID를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-144">You must provide your own app ID.</span></span>

[!code-html[Main](13-adding-social-networking-to-your-web-site/samples/sample2.html?highlight=7-14,16-17)]

<a id="Rendering_a_Gravatar_Image"></a>
## <a name="rendering-a-gravatar-image"></a><span data-ttu-id="d2918-145">Gravatar 이미지 렌더링</span><span class="sxs-lookup"><span data-stu-id="d2918-145">Rendering a Gravatar Image</span></span>

<span data-ttu-id="d2918-146">*Gravatar* (을 &quot;전역적으로 인식된 아바타&quot;)은 여러 웹 사이트에서 아바타로 사용할 수 있는 이미지 &#8212; 수를 표시 하는 이미지, 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-146">A *Gravatar* (a &quot;globally recognized avatar&quot;) is an image that can be used on multiple websites as your avatar &#8212; that is, an image that represents you.</span></span> <span data-ttu-id="d2918-147">예를 들어, 한 Gravatar 블로그 주석에서 포럼 게시물에서는 사용자를 식별 하 고 등 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-147">For example, a Gravatar can identify a person in a forum post, in a blog comment, and so on.</span></span> <span data-ttu-id="d2918-148">(사용자 고유의 Gravatar Gravatar 웹 사이트에서 등록할 수 있습니다 [ http://www.gravatar.com/ ](http://www.gravatar.com/).) 웹 사이트에 사용자의 이름 또는 이메일 주소 옆에 있는 이미지를 표시 하려는 경우 Gravatar 도우미를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-148">(You can register your own Gravatar at the Gravatar website at [http://www.gravatar.com/](http://www.gravatar.com/).) If you want to display images next to people's names or email addresses on your website, you can use the Gravatar helper.</span></span>

<span data-ttu-id="d2918-149">이 예제에서는 직접 나타내는 단일 Gravatar 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-149">In this example, you're using a single Gravatar that represents yourself.</span></span> <span data-ttu-id="d2918-150">Gravatar를 사용 하는 또 다른 방법은 사이트에 등록할 때 해당 Gravatar 주소를 지정 하는 사용자에 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-150">Another way to use a Gravatar is to let people specify their Gravatar address when they register on your site.</span></span> <span data-ttu-id="d2918-151">(에 등록할 수 있게 하는 방법을 알아볼 수 있습니다 [추가 보안 및 ASP.NET 웹 페이지 사이트 멤버 자격](https://go.microsoft.com/fwlink/?LinkId=202904).) 해당 사용자에 대 한 정보를 표시할 때마다 사용자의 이름을 표시 하는 위치는 Gravatar만 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-151">(You can learn how to let people register in [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).) Then whenever you display information for that user, you can just add the Gravatar to where you display the user's name.</span></span>

1. <span data-ttu-id="d2918-152">에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372), 아직 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="d2918-152">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="d2918-153">라는 새 웹 페이지를 만듭니다 *Gravatar.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-153">Create a new web page named *Gravatar.cshtml*.</span></span>
3. <span data-ttu-id="d2918-154">파일에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-154">Add the following markup to the file:</span></span> 

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample3.cshtml)]

    <span data-ttu-id="d2918-155">`Gravatar.GetHtml` 메서드는 페이지의 Gravatar 이미지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-155">The `Gravatar.GetHtml` method displays the Gravatar image on the page.</span></span> <span data-ttu-id="d2918-156">이미지의 크기를 변경 하려면 두 번째 매개 변수로 숫자를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-156">To change the size of the image, you can include a number as a second parameter.</span></span> <span data-ttu-id="d2918-157">기본 크기는 80입니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-157">The default size is 80.</span></span> <span data-ttu-id="d2918-158">숫자 보다 작거나 80 확인 이미지 작은 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-158">Numbers less than 80 make the image smaller.</span></span> <span data-ttu-id="d2918-159">80 보다 큰 숫자 보다 큰 이미지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-159">Numbers greater than 80 make the image larger.</span></span>
4. <span data-ttu-id="d2918-160">에 `Gravatar.GetHtml` 메서드를 대체 `<Your Gravatar account here>` Gravatar 계정에 사용 하는 전자 메일 주소를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-160">In the `Gravatar.GetHtml` methods, replace `<Your Gravatar account here>` with the email address that you use for your Gravatar account.</span></span> <span data-ttu-id="d2918-161">(Gravatar 계정이 없으면 사용할 수는 사용자의 이메일 주소입니다.)</span><span class="sxs-lookup"><span data-stu-id="d2918-161">(If you don't have a Gravatar account, you can use the email address of someone who does.)</span></span>
5. <span data-ttu-id="d2918-162">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-162">Run the page in your browser.</span></span> <span data-ttu-id="d2918-163">페이지는 지정한 전자 메일 주소에 대 한 두 가지 Gravatar 이미지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-163">The page displays two Gravatar images for the email address you specified.</span></span> <span data-ttu-id="d2918-164">두 번째 이미지는 첫 번째 보다 작습니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-164">The second image is smaller than the first.</span></span> 

    ![그림 4](13-adding-social-networking-to-your-web-site/_static/image3.jpg)

<a id="Displaying_an_Xbox_Gamer_Card"></a>
## <a name="displaying-an-xbox-gamer-card"></a><span data-ttu-id="d2918-166">Xbox 게이머 카드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-166">Displaying an Xbox Gamer Card</span></span>

<span data-ttu-id="d2918-167">사용자는 Microsoft Xbox 온라인 게임을 재생 하는 경우 각 사용자 고유 ID가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-167">When people play Microsoft Xbox games online, each user has a unique ID.</span></span> <span data-ttu-id="d2918-168">통계는 평판, 게이머 점수를 보여 줍니다. 최근에 게임을 재생 하며 게이머 카드의 형태로 각 플레이어에 대해 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-168">Statistics are kept for each player in the form of a gamer card, which shows their reputation, gamer score, and recently played games.</span></span> <span data-ttu-id="d2918-169">Xbox 게이머 인 경우에 표시할 수 있습니다 게이머 카드 사이트에서에서 페이지를 사용 하 여는 `GamerCard` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-169">If you're an Xbox gamer, you can show your gamer card on pages in your site by using the `GamerCard` helper.</span></span>

1. <span data-ttu-id="d2918-170">에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372), 아직 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="d2918-170">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="d2918-171">라는 새 페이지를 만듭니다 *XboxGamer.cshtml* 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-171">Create a new page named *XboxGamer.cshtml* and add the following markup.</span></span>

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample4.cshtml)]

    <span data-ttu-id="d2918-172">사용 된 `GamerCard.GetHtml` 표시할 게이머 카드에 대 한 별칭을 지정 하는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-172">You use the `GamerCard.GetHtml` property to specify the alias for the gamer card to be displayed.</span></span>
3. <span data-ttu-id="d2918-173">브라우저에서 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-173">Run the page in your browser.</span></span> <span data-ttu-id="d2918-174">페이지는 지정한 Xbox 게이머 카드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2918-174">The page displays the Xbox gamer card that you specified.</span></span>

    ![그림 5](13-adding-social-networking-to-your-web-site/_static/image4.jpg)
