---
uid: web-pages/overview/ui-layouts-and-themes/installing-helpers
title: (Razor) 사이트 페이지는 ASP.NET 웹 도우미 설치 | Microsoft Docs
author: Rick-Anderson
description: 이 문서에서는 ASP.NET Web Pages (Razor) 웹 사이트에서 도우미를 설치 하는 방법을 설명 합니다. 도우미는 코드 및 당 태그를 포함 하는 재사용 가능한 구성 하는 중...
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 5e968ead-906a-45ea-ac2a-c70e57e1a9b1
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/installing-helpers
msc.type: authoredcontent
ms.openlocfilehash: 5ad717cd7c64e830ce66d5e1361d0eb6ef3cbbec
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021367"
---
<a name="installing-a-helper-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="03250-104">ASP.NET 웹 페이지 (Razor) 사이트에서 도우미 설치</span><span class="sxs-lookup"><span data-stu-id="03250-104">Installing a Helper in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="03250-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="03250-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="03250-106">이 문서에서는 ASP.NET Web Pages (Razor) 웹 사이트에서 도우미를 설치 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="03250-106">This article describes how to install a helper in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="03250-107">A *도우미* 코드와 길거나 복잡 한 않을 수 있는 작업을 수행 하는 태그를 포함 하는 재사용 가능한 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="03250-107">A *helper* is a reusable component that includes code and markup to perform a task that might be tedious or complex.</span></span>
> 
> <span data-ttu-id="03250-108">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="03250-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="03250-109">WebMatrix 3를 사용 하 여 만든 웹 사이트에서 도우미를 설치 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="03250-109">How to install a helper in a website created using WebMatrix 3.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="03250-110">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="03250-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="03250-111">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="03250-111">WebMatrix 3</span></span>


## <a name="overview-of-helpers"></a><span data-ttu-id="03250-112">도우미의 개요</span><span class="sxs-lookup"><span data-stu-id="03250-112">Overview of Helpers</span></span>

<span data-ttu-id="03250-113">일부 작업을 사용자 웹 페이지에서 작업을 수행 하려는 경우가 많습니다 많은 코드가 필요 하거나 추가 정보가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="03250-113">Some tasks that people often want to do on web pages require a lot of code or require extra knowledge.</span></span> <span data-ttu-id="03250-114">예를 들어 데이터에 대 한 차트를 표시 합니다. 페이지에 Twitter "팔 로우" 단추를 넣는 웹 사이트에서 보내는 전자 메일 자르기 또는 이미지 크기 조정 PayPal을 사용 하 여 사이트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="03250-114">Examples include displaying a chart for data; putting a Twitter "Follow" button on a page; sending email from your website; cropping or resizing images; using PayPal for your site.</span></span> <span data-ttu-id="03250-115">이러한 유형의 작업을 위해 쉽게 ASP.NET 웹 페이지를 사용 하면 *도우미*합니다.</span><span class="sxs-lookup"><span data-stu-id="03250-115">To make it easy to do these kinds of things, ASP.NET Web Pages lets you use *helpers*.</span></span> <span data-ttu-id="03250-116">도우미, 줄 또는 Razor 코드의 두 개를 사용 하 여 일반적인 작업을 수행 하는 구성 요소 설치 하는 데 사용할 수 있는 사이트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03250-116">Helpers are components that you install for a site and that let you perform typical tasks by using just a line or two of Razor code.</span></span>

<span data-ttu-id="03250-117">ASP.NET 웹 페이지에 기본 제공 하는 몇 가지 도우미</span><span class="sxs-lookup"><span data-stu-id="03250-117">ASP.NET Web Pages has a few helpers built in.</span></span> <span data-ttu-id="03250-118">그러나 많은 도우미 NuGet 패키지 관리자를 사용 하 여 제공 되는 패키지 (추가 기능)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03250-118">However, many helpers are available in packages (add-ins) that are provided using the NuGet package manager.</span></span> <span data-ttu-id="03250-119">NuGet 패키지 설치를 선택 하면 및 설치의 모든 세부 정보 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="03250-119">NuGet lets you select a package to install and then it takes care of all the details of the installation.</span></span>

## <a name="installing-a-helper-in-webmatrix-3"></a><span data-ttu-id="03250-120">WebMatrix 3에서에서 도우미 설치</span><span class="sxs-lookup"><span data-stu-id="03250-120">Installing a Helper in WebMatrix 3</span></span>

1. <span data-ttu-id="03250-121">WebMatrix 3에서을 클릭 합니다 **NuGet** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="03250-121">In WebMatrix 3, click the **NuGet** button.</span></span>

    ![WebMatrix에서 NuGet 갤러리 대화 상자](installing-helpers/_static/image1.png)
2. <span data-ttu-id="03250-123">이 NuGet 패키지 관리자를 시작 하 고 사용 가능한 패키지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="03250-123">This launches the NuGet package manager and displays available packages.</span></span> <span data-ttu-id="03250-124">검색 상자에서 설치 하려는 도우미에 대 한 키워드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="03250-124">In the search box, enter a keyword for the helper you want to install.</span></span>

    ![WebMatrix에서 NuGet 갤러리 대화 상자](installing-helpers/_static/image2.png)
3. <span data-ttu-id="03250-126">패키지를 선택 하 고 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="03250-126">Select the package and then click **Install**.</span></span> <span data-ttu-id="03250-127">클릭 **예** 패키지를 설치 하 고 약관을 수락 함을 나타내려면 하려는 경우 메시지가 표시 되 면 합니다.</span><span class="sxs-lookup"><span data-stu-id="03250-127">Click **Yes** when asked if you want to install the package and indicate that you accept the terms.</span></span>

     <span data-ttu-id="03250-128">처음으로 도우미를 설치한 경우 NuGet 도우미를 구성 하는 코드에 대 한 웹 사이트의 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03250-128">If this is the first time you've installed a helper, NuGet creates folders in your website for the code that makes up the helper.</span></span>
4. <span data-ttu-id="03250-129">도우미를 제거 하려면 클릭 합니다 **갤러리** 단추를 클릭 하는 **설치 된** 탭을 제거 하려는 패키지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="03250-129">To uninstall a helper, click the **Gallery** button, click the **Installed** tab, and pick the package you want to uninstall.</span></span>

## <a name="installing-the-twitter-helper"></a><span data-ttu-id="03250-130">Twitter 도우미를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="03250-130">Installing the Twitter helper</span></span>

<span data-ttu-id="03250-131">Twitter API의 최신 NuGet을 통해 설치 된 Twitter 도우미를 사용 하 여 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03250-131">The latest version of the Twitter API is not compatible with the Twitter helper you install through NuGet.</span></span> <span data-ttu-id="03250-132">대신 참조를 [WebMatrix 사용 하 여 Twitter 도우미](twitter-helper.md) Twitter 도우미 프로젝트를 설정 하는 방법에 대 한 정보에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="03250-132">Instead, see the [Twitter Helper with WebMatrix](twitter-helper.md) topic for information about how to set up the Twitter helper in your project.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="03250-133">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="03250-133">Additional Resources</span></span>


[<span data-ttu-id="03250-134">소개 ASP.NET 웹 페이지 2-프로그래밍 기본 사항</span><span class="sxs-lookup"><span data-stu-id="03250-134">Introducing ASP.NET Web Pages 2 - Programming Basics</span></span>](../getting-started/introducing-razor-syntax-c.md)

[<span data-ttu-id="03250-135">WebMatrix 사용 하 여 twitter 도우미</span><span class="sxs-lookup"><span data-stu-id="03250-135">Twitter Helper with WebMatrix</span></span>](twitter-helper.md)
