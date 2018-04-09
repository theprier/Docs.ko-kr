---
uid: web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
title: (Razor) 사이트 페이지는 ASP.NET 웹에 지도 표시 합니다. | Microsoft Docs
author: tfitzmac
description: 이 문서에서는 대화형 지도 매핑 Bing, Google, Ma 제공한 서비스를 기반으로 하는 ASP.NET 웹 페이지 (Razor) 웹 사이트의 페이지에 표시 하는 방법에 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2014
ms.topic: article
ms.assetid: b5c268dd-ca6a-4562-b94c-a220fcf01f58
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 608dab8760bad7b877ab6fd4f89b21e980f5b1db
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="displaying-maps-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="3159e-103">ASP.NET 웹 페이지 (Razor) 사이트에 지도 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-103">Displaying Maps in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="3159e-104">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3159e-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="3159e-105">이 문서에서는 대화형 지도 매핑 Bing, Google, 지도 보기, Yahoo에서 제공 되는 서비스를 기반으로 하는 ASP.NET 웹 페이지 (Razor) 웹 사이트의 페이지에 표시 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-105">This article explains how to display interactive maps on pages in an ASP.NET Web Pages (Razor) website based on mapping services provided by Bing, Google, MapQuest, and Yahoo.</span></span>
> 
> <span data-ttu-id="3159e-106">학습 내용:</span><span class="sxs-lookup"><span data-stu-id="3159e-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="3159e-107">주소에 기반 하는 맵을 생성 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="3159e-107">How to generate a map based on an address.</span></span>
> - <span data-ttu-id="3159e-108">위도 및 경도 좌표에 따라 맵을 생성 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="3159e-108">How to generate a map based on latitude and longitude coordinates.</span></span>
> - <span data-ttu-id="3159e-109">Bing 지도와 사용할 키를 가져오고, Bing Maps 개발자 계정을 등록 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="3159e-109">How to register a Bing Maps Developer Account and get a key to use with Bing Maps.</span></span>
> 
> <span data-ttu-id="3159e-110">다음은 문서에 도입 된 ASP.NET 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-110">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="3159e-111">`Maps` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-111">The `Maps` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3159e-112">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="3159e-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="3159e-113">ASP.NET 웹 페이지 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="3159e-113">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="3159e-114">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="3159e-114">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="3159e-115">이 자습서는 WebMatrix 3 에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-115">This tutorial also works with WebMatrix 3.</span></span>


<span data-ttu-id="3159e-116">웹 페이지를 표시할 수 있습니다 맵 페이지에서 사용 하 여 `Maps` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-116">In Web Pages, you can display maps on a page by using `Maps` helper.</span></span> <span data-ttu-id="3159e-117">주소 또는 경도 및 위도 좌표 집합을 기반으로 하는 지도 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-117">You can generate maps based either on an address or on a set of longitude and latitude coordinates.</span></span> <span data-ttu-id="3159e-118">`Maps` 클래스 Bing, Google, 지도 보기, Yahoo 등 널리 사용 되 지도 엔진을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-118">The `Maps` class lets you call into popular map engines including Bing, Google, MapQuest, and Yahoo.</span></span>

<span data-ttu-id="3159e-119">페이지에 매핑을 추가 하는 단계는 호출 지도 엔진에 관계 없이 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-119">The steps for adding mapping to a page are the same regardless of which of the map engines you call.</span></span> <span data-ttu-id="3159e-120">지도 표시 하는 사용할 수 있는 메서드를 사용 하면 JavaScript 파일 참조를 추가 하 고의 메서드를 호출 하는 다음의 `Maps` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-120">You just add a JavaScript file reference that makes available methods to display the map, and then you call methods of the `Maps` helper.</span></span>

<span data-ttu-id="3159e-121">에 따라 지도 서비스를 선택 `Maps` 도우미 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-121">You choose a map service based on which `Maps` helper method you use.</span></span> <span data-ttu-id="3159e-122">이러한 항목 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-122">You can use any of these:</span></span>

- `Maps.GetBingHtml`
- `Maps.GetGoogleHtml`
- `Maps.GetYahooHtml`
- `Maps.GetMapQuestHtml`

## <a name="installing-the-pieces-you-need"></a><span data-ttu-id="3159e-123">필요한 구성 요소를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-123">Installing the Pieces You Need</span></span>

<span data-ttu-id="3159e-124">지도 표시 하려면이 정보가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-124">To display maps, you need these pieces:</span></span>

- <span data-ttu-id="3159e-125">`Maps` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-125">The `Maps` helper.</span></span> <span data-ttu-id="3159e-126">이 도우미 ASP.NET Web Helpers Library의 버전 2입니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-126">This helper is in version 2 of the ASP.NET Web Helpers Library.</span></span> <span data-ttu-id="3159e-127">라이브러리를 추가 하지 않은 경우 NuGet 패키지로 사이트에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-127">If you haven't already added the library, you can install it in your site as a NuGet package.</span></span> <span data-ttu-id="3159e-128">자세한 내용은 참조 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)합니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-128">For details, see [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372).</span></span> <span data-ttu-id="3159e-129">(갤러리에서 검색 된 `microsoft-web-helpers` 패키지 합니다.)</span><span class="sxs-lookup"><span data-stu-id="3159e-129">(In the Gallery, search for the `microsoft-web-helpers` package.)</span></span>
- <span data-ttu-id="3159e-130">JQuery 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-130">The jQuery library.</span></span> <span data-ttu-id="3159e-131">JQuery 라이브러리에 이미 포함 되어 WebMatrix 사이트 템플릿 중 일부의 *스크립트* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-131">Several of the WebMatrix site templates already include jQuery libraries in their *Script* folders.</span></span> <span data-ttu-id="3159e-132">이러한 라이브러리가 최신 jQuery 라이브러리에서 직접 다운로드할 수 있습니다는 [jQuery.org](http://jQuery.org) 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-132">If you do not have these libraries, you can download the latest jQuery library directly from the [jQuery.org](http://jQuery.org) site.</span></span> <span data-ttu-id="3159e-133">서식 파일을 사용 하 여 새 사이트를 만들 수 있습니다 (예를 들어는 **시작 사이트** 템플릿을) 현재 사이트에 해당 사이트에서 jQuery 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-133">Or you can create a new site using a template (for example, the **Starter Site** template) and then copy the jQuery files from that site to your current site.</span></span>

<span data-ttu-id="3159e-134">마지막으로, Bing maps를 사용 하려는 경우 먼저 (무료) 계정 만들고 해야 키를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-134">Finally, if you want to use Bing maps, you must first create a (free) account and get a key.</span></span> <span data-ttu-id="3159e-135">키를 가져오려면 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="3159e-135">To get a key, follow these steps:</span></span>

1. <span data-ttu-id="3159e-136">계정을 만듭니다는 [Bing Maps 개발자 계정](https://www.microsoft.com/maps/developers/web.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-136">Create an account on the [Bing Maps Developer Account](https://www.microsoft.com/maps/developers/web.aspx).</span></span> <span data-ttu-id="3159e-137">Microsoft 계정 (Windows Live ID)도 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-137">You must have a Microsoft account (Windows Live ID) as well.</span></span>

    <span data-ttu-id="3159e-138">에 대 한 키를 사용 하도록 지정할 수 있습니다 **평가/테스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-138">You can specify that you want to use the key for **Evaluation/Test**.</span></span> <span data-ttu-id="3159e-139">이동 컴퓨터에 IIS Express 및 WebMatrix를 사용 하 여 매핑 함수를 테스트 하는 경우는 **사이트** 작업 영역을 참고 하면 사이트의 URL (예를 들어 `http://localhost:50408`, 포트 번호는 다르지만 것).</span><span class="sxs-lookup"><span data-stu-id="3159e-139">If you are testing the mapping function on your own computer using WebMatrix and IIS Express, go the **Site** workspace and note the URL of your site (for example, `http://localhost:50408`, although your port number will probably be different).</span></span> <span data-ttu-id="3159e-140">이 사용 하 여 *localhost* 등록할 때 사이트와 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-140">You can use this *localhost* address as the site when you register.</span></span>
2. <span data-ttu-id="3159e-141">을 계정에 등록 한 후 Bing Maps 계정 센터 이동 하 고 클릭 **만들기 또는 뷰 키**:</span><span class="sxs-lookup"><span data-stu-id="3159e-141">After you have registered for an account, go to the Bing Maps Account Center and click **Create or view keys**:</span></span>

    ![mapping-2](displaying-maps-in-an-aspnet-web-pages-site/_static/image1.png)
3. <span data-ttu-id="3159e-143">Bing 만드는 키를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-143">Record the key that Bing creates.</span></span>

## <a name="creating-a-map-based-on-an-address-using-google"></a><span data-ttu-id="3159e-144">주소 (사용 하 여 Google)에 따라 맵 만들기</span><span class="sxs-lookup"><span data-stu-id="3159e-144">Creating a Map Based on an Address (Using Google)</span></span>

<span data-ttu-id="3159e-145">다음 예제에는 주소에 기반 하는 구조를 렌더링 하는 페이지를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-145">The following example shows how to create a page that renders a map based on an address.</span></span> <span data-ttu-id="3159e-146">이 예제에는 Google 맵을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-146">This example shows how to use Google Maps.</span></span>

1. <span data-ttu-id="3159e-147">라는 파일을 만들어 *MapAddress.cshtml* 사이트의 루트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-147">Create a file named *MapAddress.cshtml* in the root of the site.</span></span> <span data-ttu-id="3159e-148">이 페이지는 지도를 전달 하는 주소에 따라 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-148">This page will generate a map based on an address that you pass to it.</span></span>
2. <span data-ttu-id="3159e-149">다음 코드를 파일에 복사 기존 내용을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-149">Copy the following code into the file, overwriting the existing content.</span></span>

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    <span data-ttu-id="3159e-150">페이지의 다음 기능을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-150">Notice the following features of the page:</span></span>

    - <span data-ttu-id="3159e-151">`<script>` 요소에는 `<head>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-151">The `<script>` element in the `<head>` element.</span></span> <span data-ttu-id="3159e-152">예제에서는 `<script>` 요소 참조는 *jquery 1.6.4.min.js* jQuery 라이브러리, 1.6.4 버전 (압축된) 축소 된 버전에 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-152">In the example, the `<script>` element references the *jquery-1.6.4.min.js* file, which is a minified (compressed) version of the jQuery library, version 1.6.4.</span></span> <span data-ttu-id="3159e-153">참조 가정는 *.js* 중인 파일의 *스크립트* 사이트의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-153">Note that the reference assumes that the *.js* file is in the *Scripts* folder of your site.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="3159e-154">다른 버전의 jQuery 라이브러리를 사용 하는 경우 단지를 가리키고 있는 해당 버전 올바르게 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-154">If you're using a different version of the jQuery library, just make sure that you're pointing to that version correctly.</span></span>
    - <span data-ttu-id="3159e-155">에 대 한 호출에서 `@Maps.GetGoogleHtml` 페이지의 본문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-155">The call to the `@Maps.GetGoogleHtml` in the body of the page.</span></span> <span data-ttu-id="3159e-156">주소를 매핑하려면 주소 문자열을 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-156">To map an address, you must pass an address string.</span></span> <span data-ttu-id="3159e-157">비슷한 방법으로 다른 맵 엔진에 대 한 메서드는 작동 (`@Maps.GetYahooHtml`, `@Maps.GetMapQuestHtml`).</span><span class="sxs-lookup"><span data-stu-id="3159e-157">The methods for the other map engines work in a similar way (`@Maps.GetYahooHtml`, `@Maps.GetMapQuestHtml`).</span></span>
3. <span data-ttu-id="3159e-158">페이지를 실행 하 고 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-158">Run the page and enter an address.</span></span> <span data-ttu-id="3159e-159">사용자가 지정한 위치를 표시 하는 Google 맵에 따라 지도 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-159">The page displays a map, based on Google Maps, that shows the location that you specified.</span></span>

     ![mapping-1](displaying-maps-in-an-aspnet-web-pages-site/_static/image2.png)

## <a name="creating-a-map-based-on-latitude-and-longitude-coordinates-using-bing"></a><span data-ttu-id="3159e-161">위도 및 경도에 따라 맵 만들기 좌표를 (Bing 사용)</span><span class="sxs-lookup"><span data-stu-id="3159e-161">Creating a Map Based on Latitude and Longitude Coordinates (Using Bing)</span></span>

<span data-ttu-id="3159e-162">이 예제에는 좌표에 따라 지도 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-162">This example shows how to create a map based on coordinates.</span></span> <span data-ttu-id="3159e-163">이 예제에서는 Bing maps를 사용 하는 방법과 Bing 키를 포함 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-163">This example shows how to use Bing maps and how to include your Bing key.</span></span> <span data-ttu-id="3159e-164">(또한 Bing 키를 사용 하지 않고 다른 맵 엔진 사용 하 여 좌표에 따라 맵을 만들 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="3159e-164">(You can create a map based on coordinates using the other map engines also, without using a Bing key.)</span></span>

1. <span data-ttu-id="3159e-165">라는 파일을 만들어 *MapCoordinates.cshtml* 사이트와의 다음 코드와 태그를 사용 하 여 기존 콘텐츠 바꾸기의 루트에서:</span><span class="sxs-lookup"><span data-stu-id="3159e-165">Create a file named *MapCoordinates.cshtml* in the root of the site and replace the existing content with the following code and markup:</span></span>

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample2.cshtml)]
2. <span data-ttu-id="3159e-166">대체 `your-key-here` 앞에서 생성 하는 Bing 지도 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-166">Replace `your-key-here` with the Bing Maps key that you generated earlier.</span></span>
3. <span data-ttu-id="3159e-167">실행 된 *MapCoordinates.cshtml* 페이지 위도 및 경도 좌표를 입력 한 다음 클릭는 **Map It!**</span><span class="sxs-lookup"><span data-stu-id="3159e-167">Run the *MapCoordinates.cshtml* page, enter latitude and longitude coordinates, and then click the **Map It!**</span></span> <span data-ttu-id="3159e-168">클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-168">button.</span></span> <span data-ttu-id="3159e-169">(모든 좌표를 모르는 경우 다음을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-169">(If you don't know any coordinates, try the following.</span></span> <span data-ttu-id="3159e-170">이 Microsoft 레드먼드 본사에 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="3159e-170">This is a location on the Microsoft Redmond campus.)</span></span>

   - <span data-ttu-id="3159e-171">위도: 47.6781005859375</span><span class="sxs-lookup"><span data-stu-id="3159e-171">Latitude: 47.6781005859375</span></span>
   - <span data-ttu-id="3159e-172">Longitude: -122.158317565918</span><span class="sxs-lookup"><span data-stu-id="3159e-172">Longitude: -122.158317565918</span></span>

     <span data-ttu-id="3159e-173">지정한 좌표를 사용 하는 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3159e-173">The page is displayed using the coordinates that you specified.</span></span>

     ![mapping-3](displaying-maps-in-an-aspnet-web-pages-site/_static/image3.png)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="3159e-175">추가 자료</span><span class="sxs-lookup"><span data-stu-id="3159e-175">Additional Resources</span></span>


[<span data-ttu-id="3159e-176">Microsoft.Maps API 참조</span><span class="sxs-lookup"><span data-stu-id="3159e-176">Microsoft.Maps API Reference</span></span>](https://msdn.microsoft.com/library/gg427611.aspx)
