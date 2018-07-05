---
uid: web-pages/overview/ui-layouts-and-themes/twitter-helper
title: ASP.NET 웹 페이지와 twitter 도우미 | Microsoft Docs
author: tfitzmac
description: 이 항목에서 및 응용 프로그램에는 Twitter 도우미를 WebMatrix 3 프로젝트에 추가 하는 방법을 보여 줍니다. Twitter 도우미 코드를 포함 하 고 도우미를 호출 하는 방법을 보여 줍니다....
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/07/2014
ms.topic: article
ms.assetid: c1a1244e-b9c8-42e6-a00b-8456a4ec027c
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/twitter-helper
msc.type: authoredcontent
ms.openlocfilehash: 2c84a986a39f6802a78df53510847cb70efbb0f2
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37373025"
---
<a name="twitter-helper-with-aspnet-web-pages"></a><span data-ttu-id="22072-104">ASP.NET 웹 페이지와 twitter 도우미</span><span class="sxs-lookup"><span data-stu-id="22072-104">Twitter Helper with ASP.NET Web Pages</span></span>
====================
<span data-ttu-id="22072-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="22072-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="22072-106">이 항목에서 및 응용 프로그램에는 Twitter 도우미를 WebMatrix 3 프로젝트에 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="22072-106">This topic and application show how to add a Twitter Helper to your WebMatrix 3 project.</span></span> <span data-ttu-id="22072-107">Twitter 도우미 코드를 포함 하 고 도우미 메서드를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="22072-107">It contains the Twitter Helper code and shows how to call the helper methods.</span></span>
> 
> <span data-ttu-id="22072-108">Twitter.cshtml 파일에 대 한이 코드에서 개발한 **Tian 팬** Microsoft입니다.</span><span class="sxs-lookup"><span data-stu-id="22072-108">This code for the Twitter.cshtml file was developed by **Tian Pan** of Microsoft.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="22072-109">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="22072-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="22072-110">ASP.NET Web Pages (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="22072-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="22072-111">이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="22072-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>


## <a name="introduction"></a><span data-ttu-id="22072-112">소개</span><span class="sxs-lookup"><span data-stu-id="22072-112">Introduction</span></span>

<span data-ttu-id="22072-113">이 항목에서는 Twitter 도우미 응용 프로그램에 추가 하 고 Razor 구문을 사용 하 여 도우미 메서드를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="22072-113">This topic demonstrates how to add a Twitter Helper to your application and use Razor syntax to call the helper methods.</span></span> <span data-ttu-id="22072-114">Twitter 도우미 쉽게 Twitter 단추 및 응용 프로그램에 대 한 위젯을 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22072-114">The Twitter Helper makes it easy to incorporate Twitter buttons and widgets in your application.</span></span> <span data-ttu-id="22072-115">사용자의 타임 라인 또는 검색 결과는 해시 태그와 같은 Twitter 위젯을 사용 하려면 먼저 만들어야 합니다 [twitter 위젯을](https://twitter.com/settings/widgets)합니다.</span><span class="sxs-lookup"><span data-stu-id="22072-115">To use a Twitter widget, such as a user's timeline or the search results for a hashtag, you must first create the [widget on Twitter](https://twitter.com/settings/widgets).</span></span> <span data-ttu-id="22072-116">위젯을 만들면 위젯 id를 받게 됩니다. 위젯에서 표시 하는 도우미 메서드를 호출할 때이 위젯 id를 매개 변수로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="22072-116">After creating your widget, you will receive a widget id. You pass this widget id as a parameter when calling the helper methods that show widget.</span></span>

<span data-ttu-id="22072-117">이 항목에서는 Twitter API의 버전 1.1에 대 한 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="22072-117">This topic was written for version 1.1 of the Twitter API.</span></span> <span data-ttu-id="22072-118">Twitter API 변경 되 면 Twitter 도우미 코드를 프로젝트에 직접 추가 도우미 코드를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22072-118">By directly adding the Twitter Helper code to your project, you can update the helper code if the Twitter API changes.</span></span>

<span data-ttu-id="22072-119">WebMatrix를 설치 하는 방법에 대 한 내용은 [Introducing ASP.NET 웹 페이지 2-Getting Started](../getting-started/introducing-aspnet-web-pages-2/getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="22072-119">For information about installing WebMatrix, see [Introducing ASP.NET Web Pages 2 - Getting Started](../getting-started/introducing-aspnet-web-pages-2/getting-started.md).</span></span>

## <a name="add-twitter-helper-to-your-project"></a><span data-ttu-id="22072-120">Twitter 도우미 프로젝트에 추가</span><span class="sxs-lookup"><span data-stu-id="22072-120">Add Twitter Helper to your project</span></span>

<span data-ttu-id="22072-121">Twitter 도우미를 추가 하려면 먼저 폴더 추가 **앱\_코드** 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="22072-121">To add the Twitter Helper, first, add a folder named **App\_Code** to your project.</span></span> <span data-ttu-id="22072-122">그런 다음 파일을 만듭니다 **Twitter.cshtml**합니다.</span><span class="sxs-lookup"><span data-stu-id="22072-122">Then, create a file named **Twitter.cshtml**.</span></span>

![App_Code 폴더](twitter-helper/_static/image1.png)

<span data-ttu-id="22072-124">Twitter.cshtml의 기본 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="22072-124">Replace the default code in Twitter.cshtml with the following code.</span></span>

[!code-cshtml[Main](twitter-helper/samples/sample1.cshtml)]

## <a name="call-twitter-methods-from-your-web-pages"></a><span data-ttu-id="22072-125">웹 페이지에서 Twitter 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="22072-125">Call Twitter methods from your web pages</span></span>

<span data-ttu-id="22072-126">다음 예제에서는 프로젝트의 페이지에서 Twitter 도우미 메서드를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="22072-126">The following example shows how to use the Twitter Helper methods from a page in your project.</span></span> <span data-ttu-id="22072-127">프로젝트에서 요구 사항과 관련 된 값으로 매개 변수 값을 대체 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22072-127">In your project, you will want to replace the parameter values with values that are relevant to your needs.</span></span> <span data-ttu-id="22072-128">메서드 작동 방식을 탐색할 때 제공 된 위젯 id를 사용할 수 있습니다 하지만 프로젝트에 대 한 고유한 widget을 생성 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="22072-128">You can use the provided widget ids to explore how the methods work, but you will want to generate your own widgets for your project.</span></span>

<span data-ttu-id="22072-129">아래에 표시 된 매개 변수 중 일부는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="22072-129">Not all of the parameters shown below are required.</span></span> <span data-ttu-id="22072-130">선택적 매개 변수는 단추 또는 위젯에 표시 되는 방식을 사용자 지정 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22072-130">The optional parameters are used to customize how the button or widget is displayed.</span></span> <span data-ttu-id="22072-131">예를 들어 필요에 따라 사용자 이름에 따라 단추를 있지만 단추와 언어의 크기를 지정 하는 방법 및 팔로 워 수를 포함 하는 방법을 보여 합니다.</span><span class="sxs-lookup"><span data-stu-id="22072-131">For example, the Follow Button only requires the user name to follow, but the example shows how to include the number of followers, and how specify the size of the button and the language.</span></span>

[!code-html[Main](twitter-helper/samples/sample2.html)]

## <a name="see-the-results"></a><span data-ttu-id="22072-132">결과 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="22072-132">See the results</span></span>

<span data-ttu-id="22072-133">위의 코드에 다음 단추 및 위젯을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="22072-133">The above code produces the following buttons and widgets.</span></span> <span data-ttu-id="22072-134">이러한 단추 및 위젯은 완벽 하 게 작동, 스크린 샷이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="22072-134">These buttons and widgets are fully-functional, not screenshots.</span></span> <span data-ttu-id="22072-135">Language 매개 변수 설정 되었기 때문에 스페인어에 따라 단추가 표시 되는지 **es**합니다.</span><span class="sxs-lookup"><span data-stu-id="22072-135">The Follow Button is displayed in Spanish because the language parameter was set to **es**.</span></span>

### <a name="follow-button"></a><span data-ttu-id="22072-136">단추 수행</span><span class="sxs-lookup"><span data-stu-id="22072-136">Follow Button</span></span>

<span data-ttu-id="22072-137">[에 따라 @aspnet)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span><span class="sxs-lookup"><span data-stu-id="22072-137">[Follow @aspnet)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span></span>

### <a name="tweet-button"></a><span data-ttu-id="22072-138">트 윗 단추</span><span class="sxs-lookup"><span data-stu-id="22072-138">Tweet Button</span></span>

<span data-ttu-id="22072-139">[트 윗](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span><span class="sxs-lookup"><span data-stu-id="22072-139">[Tweet](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span></span>

### <a name="user-timeline-profile"></a><span data-ttu-id="22072-140">사용자 타임 라인 (프로필)</span><span class="sxs-lookup"><span data-stu-id="22072-140">User Timeline (Profile)</span></span>

<span data-ttu-id="22072-141">[트 윗 @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="22072-141">[Tweets by @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="favorites"></a><span data-ttu-id="22072-142">즐겨찾기</span><span class="sxs-lookup"><span data-stu-id="22072-142">Favorites</span></span>

<span data-ttu-id="22072-143">[즐겨 찾는 트 윗 @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="22072-143">[Favorite Tweets by @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="list"></a><span data-ttu-id="22072-144">목록</span><span class="sxs-lookup"><span data-stu-id="22072-144">List</span></span>

<span data-ttu-id="22072-145">[트 윗 @Microsoft/MS \_소비자\_밴드](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="22072-145">[Tweets from @Microsoft/MS\_Consumer\_Bands](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="search"></a><span data-ttu-id="22072-146">검색</span><span class="sxs-lookup"><span data-stu-id="22072-146">Search</span></span>

<span data-ttu-id="22072-147">[에 대 한 트 윗 &quot;#asp.net&quot;](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="22072-147">[Tweets about &quot;#asp.net&quot;](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>
