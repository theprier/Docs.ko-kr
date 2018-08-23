---
uid: web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
title: 모바일 장치에 대 한 페이지 (Razor) 사이트 ASP.NET 웹 렌더링 | Microsoft Docs
author: tfitzmac
description: '이 문서에는 모바일 장치에 적절 하 게 렌더링 하는 ASP.NET Web Pages (Razor) 사이트에서 페이지를 만드는 방법을 설명 합니다. 학습할 내용: 있습니다 방법...'
ms.author: riande
ms.date: 02/17/2014
ms.assetid: f15ab392-c05e-4269-83bf-7c6d2b8c8ec8
msc.legacyurl: /web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
msc.type: authoredcontent
ms.openlocfilehash: 7159283efcd4a82d5dff68f2d9e315f804e7cdcb
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41836744"
---
<a name="rendering-aspnet-web-pages-razor-sites-for-mobile-devices"></a><span data-ttu-id="258cb-104">모바일 장치에 대 한 ASP.NET 웹 페이지 (Razor) 사이트 렌더링</span><span class="sxs-lookup"><span data-stu-id="258cb-104">Rendering ASP.NET Web Pages (Razor) Sites for Mobile Devices</span></span>
====================
<span data-ttu-id="258cb-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="258cb-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="258cb-106">이 문서에는 모바일 장치에 적절 하 게 렌더링 하는 ASP.NET Web Pages (Razor) 사이트에서 페이지를 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="258cb-106">This article describes how to create pages in an ASP.NET Web Pages (Razor) site that will render appropriately on mobile devices.</span></span>
> 
> <span data-ttu-id="258cb-107">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="258cb-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="258cb-108">페이지를 지정 하는 명명 규칙을 사용 하는 방법은 모바일 장치용으로 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="258cb-108">How to use a naming convention to specify that a page is designed specifically for mobile devices.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="258cb-109">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="258cb-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="258cb-110">ASP.NET Web Pages (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="258cb-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="258cb-111">이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="258cb-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>


<span data-ttu-id="258cb-112">ASP.NET 웹 페이지를 통해 모바일 또는 다른 장치에서 콘텐츠 렌더링에 대 한 사용자 지정 표시를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="258cb-112">ASP.NET Web Pages lets you create custom displays for rendering content on mobile or other devices.</span></span>

<span data-ttu-id="258cb-113">ASP.NET 웹 페이지 사이트에서 장치별 페이지를 만드는 가장 간단한 방법은 다음과 같이 파일 명명 패턴을 사용 하 여가: <em>파일 이름.</em> <em>Mobile</em><em>.cshtml</em>합니다.</span><span class="sxs-lookup"><span data-stu-id="258cb-113">The simplest way to create device-specific page in an ASP.NET Web Pages site is by using a file-naming pattern like this: <em>FileName.</em><em>Mobile</em><em>.cshtml</em>.</span></span> <span data-ttu-id="258cb-114">페이지의 두 버전을 만들 수 있습니다 (예를 들어 라는 하나 <em>MyFile.cshtml</em> 및 이름이 <em>MyFile.Mobile.cshtml</em>).</span><span class="sxs-lookup"><span data-stu-id="258cb-114">You can create two versions of a page (for example, one named <em>MyFile.cshtml</em> and one named <em>MyFile.Mobile.cshtml</em>).</span></span> <span data-ttu-id="258cb-115">런타임 시 모바일 장치를 요청 하는 경우 <em>MyFile.cshtml</em>에서 콘텐츠를 렌더링 하는 ASP.NET <em>MyFile.Mobile.cshtml</em>합니다.</span><span class="sxs-lookup"><span data-stu-id="258cb-115">At run time, when a mobile device requests <em>MyFile.cshtml</em>, ASP.NET renders the content from <em>MyFile.Mobile.cshtml</em>.</span></span> <span data-ttu-id="258cb-116">그렇지 않으면 <em>MyFile.cshtml</em> 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="258cb-116">Otherwise, <em>MyFile.cshtml</em> is rendered.</span></span>

<span data-ttu-id="258cb-117">다음 예제에서는 모바일 장치에 대 한 콘텐츠 페이지를 추가 하 여 모바일 렌더링을 사용 하도록 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="258cb-117">The following example shows how to enable mobile rendering by adding a content page for mobile devices.</span></span> <span data-ttu-id="258cb-118">*Page1.cshtml* 콘텐츠 탐색 세로 막대를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="258cb-118">*Page1.cshtml* contains content plus a navigation sidebar.</span></span> <span data-ttu-id="258cb-119">*Page1.Mobile.cshtml* 콘텐츠는 동일 하지만 보충 기사를 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="258cb-119">*Page1.Mobile.cshtml* contains the same content, but omits the sidebar.</span></span>

1. <span data-ttu-id="258cb-120">ASP.NET 웹 페이지 사이트에서 파일을 만듭니다 *Page1.cshtml* 및 현재 콘텐츠를 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="258cb-120">In an ASP.NET Web Pages site, create a file named *Page1.cshtml* and replace the current content with following markup.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample1.html)]
2. <span data-ttu-id="258cb-121">이라는 파일을 만듭니다 *Page1.Mobile.cshtml* 기존 콘텐츠를 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="258cb-121">Create a file named *Page1.Mobile.cshtml* and replace the existing content with the following markup.</span></span> <span data-ttu-id="258cb-122">페이지의 모바일 버전을 더 작은 화면에서 더 나은 렌더링에 대 한 탐색 섹션 생략는 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="258cb-122">Notice that the mobile version of the page omits the navigation section for better rendering on a smaller screen.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample2.html)]
3. <span data-ttu-id="258cb-123">데스크톱 브라우저를 실행 하 고 이동할 *Page1.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="258cb-123">Run a desktop browser and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="258cb-124">![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="258cb-124">![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span></span>
4. <span data-ttu-id="258cb-125">모바일 브라우저 (또는 모바일 장치 에뮬레이터)를 실행 하 고 이동할 *Page1.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="258cb-125">Run a mobile browser (or a mobile device emulator) and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="258cb-126">(공지 포함 되지 않은 *.mobile 합니다.*</span><span class="sxs-lookup"><span data-stu-id="258cb-126">(Notice that you do not include *.mobile.*</span></span> <span data-ttu-id="258cb-127">URL의 일부로 합니다.) 요청 하는 것에 *Page1.cshtml*, ASP.NET 렌더링 *Page1.Mobile.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="258cb-127">as part of the URL.) Even though the request is to *Page1.cshtml*, ASP.NET renders *Page1.Mobile.cshtml*.</span></span>

    ![mobilesites-2](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="258cb-129">모바일 페이지를 테스트 하려면 데스크톱 컴퓨터에서 실행 되는 모바일 장치 시뮬레이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="258cb-129">To test mobile pages, you can use a mobile device simulator that runs on a desktop computer.</span></span> <span data-ttu-id="258cb-130">이 도구를 사용 하면 웹 페이지 테스트 모바일 장치에 표시 됩니다 (즉, 일반적으로 훨씬 더 작은 사용 하 여 표시 영역).</span><span class="sxs-lookup"><span data-stu-id="258cb-130">This tool lets you test web pages as they would look on mobile devices (that is, typically with a much smaller display area).</span></span> <span data-ttu-id="258cb-131">시뮬레이터의 한 가지 예는 합니다 [사용자 에이전트 전환기 추가 기능](http://addons.mozilla.org/firefox/addon/user-agent-switcher/) Mozilla Firefox는 하면 데스크톱 버전의 Firefox에서 다양 한 모바일 브라우저를 에뮬레이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="258cb-131">One example of a simulator is the [User Agent Switcher add-on](http://addons.mozilla.org/firefox/addon/user-agent-switcher/) for Mozilla Firefox, which lets you emulate various mobile browsers from a desktop version of Firefox.</span></span>


<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="258cb-132">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="258cb-132">Additional Resources</span></span>


<span data-ttu-id="258cb-133">[Windows Phone 에뮬레이터](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)</span><span class="sxs-lookup"><span data-stu-id="258cb-133">[Windows Phone Emulator](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)</span></span>
