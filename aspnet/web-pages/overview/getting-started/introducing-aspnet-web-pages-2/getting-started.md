---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
title: "ASP.NET 웹 페이지-시작 소개 | Microsoft Docs"
author: tfitzmac
description: "WebMatrix 더 이상 권장 통합된 개발 환경에 대 한 ASP.NET 웹 페이지입니다. Visual Studio 또는 Visual Studio 코드를 사용 합니다. 이 설명서는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: a36d3bdf-ef1b-47a4-b932-3a0cf4cad716
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
msc.type: authoredcontent
ms.openlocfilehash: a6789ee75b4ca6e9443681cc7ec0bd3ab94cedcd
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="introducing-aspnet-web-pages---getting-started"></a><span data-ttu-id="b8715-105">ASP.NET 웹 페이지-시작 소개</span><span class="sxs-lookup"><span data-stu-id="b8715-105">Introducing ASP.NET Web Pages - Getting Started</span></span>
====================
<span data-ttu-id="b8715-106">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="b8715-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> > [!NOTE] 
> > 
> > <span data-ttu-id="b8715-107">WebMatrix 더 이상 권장 통합된 개발 환경에 대 한 ASP.NET 웹 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-107">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="b8715-108">사용 하 여 [Visual Studio](../program-asp-net-web-pages-in-visual-studio.md) 또는 [Visual Studio Code](https://code.visualstudio.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-108">Use [Visual Studio](../program-asp-net-web-pages-in-visual-studio.md) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>
> 
> 
> <span data-ttu-id="b8715-109">이 지침 하 고 응용 프로그램 제공 ASP.NET 웹 페이지 (2 이상 버전)의 개요 및 Razor 구문, 동적 웹 사이트를 만들기 위한 경량 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-109">This guidance and application gives you an overview of ASP.NET Web Pages (version 2 or later) and Razor syntax, a lightweight framework for creating dynamic websites.</span></span> <span data-ttu-id="b8715-110">또한 WebMatrix, 페이지 및 사이트를 만들기 위한 도구를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-110">It also introduces WebMatrix, a tool for creating pages and sites.</span></span>
> 
> <span data-ttu-id="b8715-111">**수준**: ASP.NET 웹 페이지를 처음 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-111">**Level**: New to ASP.NET Web Pages.</span></span>  
> <span data-ttu-id="b8715-112">**가정 기술**: HTML, 기본 css 스타일 시트 ().</span><span class="sxs-lookup"><span data-stu-id="b8715-112">**Skills assumed**: HTML, basic cascading style sheets (CSS).</span></span>
> 
> <span data-ttu-id="b8715-113">학습 내용 집합의 첫 번째 자습서:</span><span class="sxs-lookup"><span data-stu-id="b8715-113">What you'll learn in the first tutorial of the set:</span></span>
> 
> - <span data-ttu-id="b8715-114">ASP.NET 웹 페이지 기술은 이며이 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-114">What ASP.NET Web Pages technology is and what it's for.</span></span>
> - <span data-ttu-id="b8715-115">WebMatrix의는입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-115">What WebMatrix is.</span></span>
> - <span data-ttu-id="b8715-116">모든 항목을 설치 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-116">How to install everything.</span></span>
> - <span data-ttu-id="b8715-117">WebMatrix를 사용 하 여 웹 사이트를 만드는 방법.</span><span class="sxs-lookup"><span data-stu-id="b8715-117">How to create a website by using WebMatrix.</span></span>
>   
> 
> <span data-ttu-id="b8715-118">기능/기술을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-118">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="b8715-119">Microsoft 웹 플랫폼 설치 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-119">Microsoft Web Platform Installer.</span></span>
> - <span data-ttu-id="b8715-120">WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="b8715-120">WebMatrix.</span></span>
> - <span data-ttu-id="b8715-121">*.cshtml* 페이지</span><span class="sxs-lookup"><span data-stu-id="b8715-121">*.cshtml* pages</span></span>
>   
> 
> <span data-ttu-id="b8715-122">원래 Mike 서가이 자습서를 썼습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-122">Mike Pope originally wrote this tutorial.</span></span> <span data-ttu-id="b8715-123">Tom FitzMacken Microsoft WebMatrix 3에 대 한 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-123">Tom FitzMacken updated it for Microsoft WebMatrix 3.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b8715-124">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="b8715-124">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="b8715-125">ASP.NET 웹 페이지 (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="b8715-125">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="b8715-126">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="b8715-126">WebMatrix 3</span></span>


## <a name="what-should-you-know"></a><span data-ttu-id="b8715-127">해야 알고 있습니까?</span><span class="sxs-lookup"><span data-stu-id="b8715-127">What Should You Know?</span></span>

<span data-ttu-id="b8715-128">에 익숙할 것으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-128">We're assuming that you're familiar with:</span></span>

- <span data-ttu-id="b8715-129">**HTML**.</span><span class="sxs-lookup"><span data-stu-id="b8715-129">**HTML**.</span></span> <span data-ttu-id="b8715-130">없음 심층 전문 지식이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-130">No in-depth expertise is required.</span></span> <span data-ttu-id="b8715-131">HTML, 설명 하지 않겠습니다에서는 또한 사용 하지 마십시오 복잡 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-131">We won't explain HTML, but we also don't use anything complex.</span></span> <span data-ttu-id="b8715-132">여기서 한다고 생각 유용 HTML 자습서의 링크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-132">We'll provide links to HTML tutorials where we think they're useful.</span></span>
- <span data-ttu-id="b8715-133">**Css 스타일 시트 ()**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-133">**Cascading style sheets (CSS)**.</span></span> <span data-ttu-id="b8715-134">와 동일 html 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-134">Same as with HTML.</span></span>
- <span data-ttu-id="b8715-135">**Basic 데이터베이스 아이디어**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-135">**Basic database ideas**.</span></span> <span data-ttu-id="b8715-136">스프레드시트 데이터에 사용 되 고 정렬 되었으며 전문 지식 수준을 아닌 데이터를 필터링 하는 경우 일반적으로 있으리라이 자습서 집합에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-136">If you've used a spreadsheet for data and sorted and filtered the data, that's the level of expertise we're generally assuming for this tutorial set.</span></span>

<span data-ttu-id="b8715-137">또한 기본 프로그래밍 학습에 관심이으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-137">We're also assuming that you're interested in learning basic programming.</span></span> <span data-ttu-id="b8715-138">ASP.NET 웹 페이지 라는 C# 프로그래밍 언어를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-138">ASP.NET Web Pages use a programming language called C#.</span></span> <span data-ttu-id="b8715-139">프로그래밍에서는 방금 것에 관심 있는 배경 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-139">You don't have to have any background in programming, just an interest in it.</span></span> <span data-ttu-id="b8715-140">계속 하기 전에 웹 페이지에서 모든 JavaScript 작성 한, 충분 한 배경 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-140">If you've ever written any JavaScript in a web page before, you've got plenty of background.</span></span>

<span data-ttu-id="b8715-141">프로그래밍에 익숙한 경우 수 되어이 자습서에서는 처음 설정 하는 참고 새 프로그래머 속도 제공 하는 동안 느린 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-141">Note that if you are familiar with programming, you might find that this tutorial set initially moves slowly while we bring new programmers up to speed.</span></span> <span data-ttu-id="b8715-142">첫 번째 몇 가지 자습서 지나서 대로, 하지만 설명 하기 위해 작은 기본 프로그래밍 있고이 작업에 더 빠르게 클립을 따라 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-142">As we get past the first few tutorials, though, there will be less basic programming to explain and things will move along at a faster clip.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="b8715-143">어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="b8715-143">What Do You Need?</span></span>

<span data-ttu-id="b8715-144">필요한 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-144">Here's what you'll need:</span></span>

- <span data-ttu-id="b8715-145">Windows 8, Windows 7, Windows Server 2008 또는 Windows Server 2012를 실행 하는 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="b8715-145">A computer that is running Windows 8, Windows 7, Windows Server 2008, or Windows Server 2012.</span></span>
- <span data-ttu-id="b8715-146">라이브 인터넷 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-146">A live internet connection.</span></span>
- <span data-ttu-id="b8715-147">관리자 권한 (설치 과정에 필요).</span><span class="sxs-lookup"><span data-stu-id="b8715-147">Administrator privileges (required for the installation process).</span></span>

## <a name="what-is-aspnet-web-pages"></a><span data-ttu-id="b8715-148">ASP.NET 웹 페이지는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b8715-148">What Is ASP.NET Web Pages?</span></span>

<span data-ttu-id="b8715-149">ASP.NET 웹 페이지에는 동적 웹 페이지를 만드는 데 사용할 수 있는 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-149">ASP.NET Web Pages is a framework that you can use to create dynamic web pages.</span></span> <span data-ttu-id="b8715-150">간단한 HTML 웹 페이지 정적입니다. 페이지에는 HTML 태그를 고정된 의해 그 내용이 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-150">A simple HTML web page is static; its content is determined by the fixed HTML markup that's in the page.</span></span> <span data-ttu-id="b8715-151">ASP.NET 웹 페이지를 만드는 것과 같은 동적 페이지에는 코드를 사용 하 여 즉시 페이지 콘텐츠를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-151">Dynamic pages like those you create with ASP.NET Web Pages let you create the page content on the fly, by using code.</span></span>

<span data-ttu-id="b8715-152">동적 페이지를 사용 하 여 모든 종류의 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-152">Dynamic pages let you do all sorts of things.</span></span> <span data-ttu-id="b8715-153">폼을 사용 하 여 입력 메시지를 표시 하 고 페이지에 표시 하거나 어떻게 나타나는지를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-153">You can ask a user for input by using a form and then change what the page displays or how it looks.</span></span> <span data-ttu-id="b8715-154">사용자 정보를 가져올 하 고, 데이터베이스에 저장 하 고, 그런 다음 나중에 나열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-154">You can take information from a user, save it in a database, and then list it later.</span></span> <span data-ttu-id="b8715-155">사이트에서 전자 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-155">You can send email from your site.</span></span> <span data-ttu-id="b8715-156">웹 (예: 매핑 서비스)에서 다른 서비스와 상호 작용할 수 있으며 해당 소스에서 정보를 통합 하는 페이지를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-156">You can interact with other services on the web (for example, a mapping service) and produce pages that integrate information from those sources.</span></span>

## <a name="what-is-webmatrix"></a><span data-ttu-id="b8715-157">WebMatrix는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="b8715-157">What is WebMatrix?</span></span>

<span data-ttu-id="b8715-158">WebMatrix는 웹 페이지 편집기, 데이터베이스 유틸리티, 페이지 및 웹 사이트를 인터넷에 게시 하기 위한 기능 테스트용 웹 서버를 통합 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-158">WebMatrix is a tool that integrates a web page editor, a database utility, a web server for testing pages, and features for publishing your website to the Internet.</span></span> <span data-ttu-id="b8715-159">WebMatrix는 무료 이며 쉽게 설치 하 고 사용 하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-159">WebMatrix is free, and it's easy to install and easy to use.</span></span> <span data-ttu-id="b8715-160">(또한 작동 셨 겠지만 HTML 페이지에 대 한 것은 물론 PHP와 같은 다른 기술 합니다.)</span><span class="sxs-lookup"><span data-stu-id="b8715-160">(It also works for just plain HTML pages, as well as for other technologies like PHP.)</span></span>

<span data-ttu-id="b8715-161">실제로 하지 않으면 *가* WebMatrix ASP.NET 웹 페이지를 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-161">You don't actually *have* to use WebMatrix to work with ASP.NET Web Pages.</span></span> <span data-ttu-id="b8715-162">편집기에서 텍스트를 사용 하 여 페이지를 만들 예를 들어 있고 액세스할 수 있는 웹 서버를 사용 하 여 페이지를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-162">You can create pages by using a text editor, for example, and test pages by using a web server that you have access to.</span></span> <span data-ttu-id="b8715-163">그러나 WebMatrix를 사용 하면 모든,이 자습서 전체에서 WebMatrix를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-163">However, WebMatrix makes it all very easy, so these tutorials will use WebMatrix throughout.</span></span>

## <a name="about-these-tutorials"></a><span data-ttu-id="b8715-164">이 자습서에 대 한</span><span class="sxs-lookup"><span data-stu-id="b8715-164">About These Tutorials</span></span>

<span data-ttu-id="b8715-165">이 자습서 집합은 ASP.NET 웹 페이지를 사용 하는 방법에 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-165">This tutorial set is an introduction to how to use ASP.NET Web Pages.</span></span> <span data-ttu-id="b8715-166">이 소개 용 자습서 집합의 총 9 자습서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-166">There are 9 tutorials total in this introductory tutorial set.</span></span> <span data-ttu-id="b8715-167">그의 real, 전문가 수준의 웹 사이트를 만드는 데 ASP.NET 웹 페이지 초보자에서 이동 하는 자습서 집합 시리즈의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-167">It's part of a series of tutorial sets that takes you from ASP.NET Web Pages novice to creating real, professional-looking websites.</span></span>

<span data-ttu-id="b8715-168">이 첫 번째 자습서에서 ASP.NET 웹 페이지를 사용 하는 방법의 기본 사항을 보여 주는 중점적을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-168">This first tutorial set concentrates on showing you the basics of how to work with ASP.NET Web Pages.</span></span> <span data-ttu-id="b8715-169">완료 되 면 여기서이 이와 종료 하는 웹 페이지 및 탐색 좀 더 깊이 선택 하는 추가 자습서 집합으로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-169">When you're done, you can work with additional tutorial sets that pick up where this one ends and that explore Web Pages in more depth.</span></span>

<span data-ttu-id="b8715-170">의도 한 대로, 이제 쉽게에서 자세한 설명을 비롯 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-170">We deliberately go easy on the in-depth explanations.</span></span> <span data-ttu-id="b8715-171">선택 하 고 문제가 알아보겠습니다 때마다이 자습서 집합에 대 한에서는 항상 한다고 생각 하는 방법을 이해 하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-171">And whenever we show something, for this tutorial set we always choose the way that we think is easiest to understand.</span></span> <span data-ttu-id="b8715-172">이후 자습서 더 자세하게 검토할 집합과 보다 효율적인 또는 보다 유연한 방법을 (도 더 재미 있게)를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-172">Later tutorial sets go into more depth and show you more efficient or more flexible approaches (also more fun).</span></span> <span data-ttu-id="b8715-173">하지만 해당 자습서 먼저 기본 사항을 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-173">But those tutorials require you to understand the basics first.</span></span>

<span data-ttu-id="b8715-174">처음 자습서 집합 ASP.NET 웹 페이지의 이러한 기능에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-174">The tutorial set you've just started covers these features of ASP.NET Web Pages:</span></span>

- <span data-ttu-id="b8715-175">소개 및 가져오는 모든 항목이 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-175">Introduction and getting everything installed.</span></span> <span data-ttu-id="b8715-176">(하는 현재 읽고 있는 자습서입니다.)</span><span class="sxs-lookup"><span data-stu-id="b8715-176">(That's in the tutorial you're reading.)</span></span>
- <span data-ttu-id="b8715-177">ASP.NET 웹 페이지 프로그래밍의 기본입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-177">The basics of ASP.NET Web Pages programming.</span></span>
- <span data-ttu-id="b8715-178">데이터베이스를 만드는 중</span><span class="sxs-lookup"><span data-stu-id="b8715-178">Creating a database.</span></span>
- <span data-ttu-id="b8715-179">만들기 및 사용자 입력된 폼을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-179">Creating and processing a user input form.</span></span>
- <span data-ttu-id="b8715-180">추가, 업데이트 및 데이터베이스의에서 데이터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-180">Adding, updating, and deleting data in the database.</span></span>

## <a name="what-will-you-create"></a><span data-ttu-id="b8715-181">만들 있습니까?</span><span class="sxs-lookup"><span data-stu-id="b8715-181">What Will You Create?</span></span>

<span data-ttu-id="b8715-182">이 자습서를 설정 하 고 원하는 영화를 나열할 수 있는 웹 사이트를 중심으로 이후의 조건 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-182">This tutorial set and subsequent ones revolve around a website where you can list movies that you like.</span></span> <span data-ttu-id="b8715-183">영화를 입력 하 고 편집을 나열 하는 작업을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-183">You'll be able to enter movies, edit them, and list them.</span></span> <span data-ttu-id="b8715-184">다음은 자습서이 집합에서 페이지가입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-184">Here are a couple of the pages you'll create in this tutorial set.</span></span> <span data-ttu-id="b8715-185">첫 번째 만들게 페이지 나열 영화를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-185">The first one shows the movie listing page that you'll create:</span></span>

![동영상 목록을 보여 주는 완료 했습니다 만든 동영상 앱](getting-started/_static/image1.png)

<span data-ttu-id="b8715-187">및 새 동영상 정보를 사이트에 추가할 수 있는 페이지가 표시 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-187">And here's the page that lets you add new movie information to your site:</span></span>

![동영상 추가 페이지를 보여 주는 완성된 동영상 앱](getting-started/_static/image2.png)

<span data-ttu-id="b8715-189">이 후속 자습서 집합 빌드 설정 및 사진 업로드, 로그인 사용자 수 있도록, 전자 메일을 보내고 소셜 미디어와 통합 같은 다른 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-189">Subsequent tutorial sets build on this set and add more functionality, like uploading pictures, letting people log in, sending email, and integrating with social media.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="b8715-190">Azure에서 실행 되는이 응용 프로그램 참조</span><span class="sxs-lookup"><span data-stu-id="b8715-190">See this App Running on Azure</span></span>

<span data-ttu-id="b8715-191">실시간 웹 앱으로 실행 하는 완료 된 사이트를 참조 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="b8715-191">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="b8715-192">다음 단추 클릭 하 여 Azure 계정에 완전 한 버전의 앱을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-192">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebPagesMovies)

<span data-ttu-id="b8715-193">Azure에이 솔루션을 배포 하려면 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-193">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="b8715-194">계정이 아직 없는 경우 다음 옵션:</span><span class="sxs-lookup"><span data-stu-id="b8715-194">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="b8715-195">[무료 Azure 계정을 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -크레딧을 얻게 유료 Azure 서비스를 실행 해 사용할 수 있으며, 사용 후에 최대 계정 등에 사용 가능한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-195">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="b8715-196">[MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -Your MSDN을 구독 하면 크레딧 매달 유료 Azure 서비스에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-196">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="installing-everything"></a><span data-ttu-id="b8715-197">설치 하는 모든 항목</span><span class="sxs-lookup"><span data-stu-id="b8715-197">Installing Everything</span></span>

<span data-ttu-id="b8715-198">Microsoft에서 웹 플랫폼 설치 관리자를 사용 하 여 모든 항목을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-198">You can install everything by using the Web Platform Installer from Microsoft.</span></span> <span data-ttu-id="b8715-199">실제로 설치 관리자를 설치 하 고를 사용 하 여 다른 모든 요소를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-199">In effect, you install the installer, and then use it to install everything else.</span></span>

<span data-ttu-id="b8715-200">이상 있을 수 있는 웹 페이지를 사용 하려면 Windows Server 2008 이상 또는 Windows XP sp3 이상 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-200">To use Web Pages, you have to be have at least Windows XP with SP3 installed, or Windows Server 2008 or later.</span></span>

<span data-ttu-id="b8715-201">에 [웹 페이지의 페이지](../../../index.md) ASP.NET 웹 사이트의 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-201">On the [Web Pages page](../../../index.md) of the ASP.NET website, click **Install**.</span></span>

![ASP.NET 웹 사이트 보여 주는 &quot;WebMatrix 설치&quot; 단추](getting-started/_static/image3.png)

<span data-ttu-id="b8715-203">WebMatrix를 설치 하기 전에 개인정보취급방침 사용 조건에 동의 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-203">You are asked to accept the license terms and privacy statement before installing WebMatrix.</span></span>

![설치를 시작 하는 용어를 허용 합니다.](getting-started/_static/image4.png)

<span data-ttu-id="b8715-205">클릭 **실행** 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-205">Click **Run** to start the installation.</span></span> <span data-ttu-id="b8715-206">(설치 프로그램을 저장 하려면 클릭 **저장** 다음 사용자가 저장 폴더에서 설치 프로그램을 실행 합니다.)</span><span class="sxs-lookup"><span data-stu-id="b8715-206">(If you want to save the installer, click **Save** and then run the installer from the folder where you saved it.)</span></span>

![](getting-started/_static/image5.png)

<span data-ttu-id="b8715-207">웹 플랫폼 설치 관리자 나타나고 해당 WebMatrix를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-207">The Web Platform Installer appears, ready to install WebMatrix.</span></span> <span data-ttu-id="b8715-208">**설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-208">Click **Install**.</span></span>

![](getting-started/_static/image6.png)

<span data-ttu-id="b8715-209">설치 프로세스에 컴퓨터에 설치으로 파악 하 고 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-209">The installation process figures out what it has to install on your computer and starts the process.</span></span> <span data-ttu-id="b8715-210">정확 하 게 설치에 기능에 따라 프로세스 걸릴 수 있습니다 몇 분에서 몇 분 정도.</span><span class="sxs-lookup"><span data-stu-id="b8715-210">Depending on what exactly has to be installed, the process can take anywhere from a few moments to several minutes.</span></span> <span data-ttu-id="b8715-211">선택 **동의** 하려면 사용 조건에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-211">Select **I Accept** to accept the license terms.</span></span>

## <a name="hello-webmatrix"></a><span data-ttu-id="b8715-212">Hello, WebMatrix</span><span class="sxs-lookup"><span data-stu-id="b8715-212">Hello, WebMatrix</span></span>

<span data-ttu-id="b8715-213">완료 되 면 설치 프로세스는 WebMatrix를 자동으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-213">When it's done, the installation process can launch WebMatrix automatically.</span></span> <span data-ttu-id="b8715-214">그렇지 않은 경우 windows에서에서 **시작** 메뉴에서 **Microsoft WebMatrix**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-214">If it doesn't, in Windows, from the **Start** menu, launch **Microsoft WebMatrix**.</span></span>

<span data-ttu-id="b8715-215">처음으로 WebMatrix를 시작할 때 Microsoft 계정으로 Microsoft Azure에 로그인 하 여 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-215">When you launch WebMatrix for the first time, you are given a chance to sign in to Microsoft Azure with your Microsoft account.</span></span> <span data-ttu-id="b8715-216">에 로그인 하면 Azure 통해 무료 웹 앱을 10 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-216">By signing in, you will receive 10 free web apps through Azure.</span></span> <span data-ttu-id="b8715-217">이러한 무료 웹 앱에 앱을 테스트 하는 편리한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-217">These free web apps provide a convenient way to test your apps.</span></span> <span data-ttu-id="b8715-218">Azure 계정이 아직 없는 MSDN 구독이 있는 경우 다음을 할 수 있습니다 [MSDN 구독 혜택을 활성화](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-218">If you don't already have an Azure account, but you do have an MSDN subscription, you can [activate your MSDN subscription benefits](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="b8715-219">그렇지 않은 경우 몇 분에서에서 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-219">Otherwise, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b8715-220">자세한 내용은 참조 [Azure 무료 평가판](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-220">For details, see [Azure Free Trial](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span>

<span data-ttu-id="b8715-221">이 자습서와 함께 계속 하려면 지금 바로 로그인 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-221">You do not have to sign in right now to continue with this tutorial.</span></span> <span data-ttu-id="b8715-222">사용자 로그인 하지 않는 이제,는 여전히 경우 나중에 로그인 하는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-222">If you do not sign in now, you will still have the option to sign in later.</span></span> <span data-ttu-id="b8715-223">마지막 [항목](publishing.md) 해당 항목을 완료 하려면 로그인 해야 하는 따라서; 시리즈가이 자습서에서는 Azure에 웹 사이트를 배포 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-223">The last [topic](publishing.md) in this tutorial series covers how to deploy your website to Azure; therefore, you would need to sign in to complete that topic.</span></span>

<span data-ttu-id="b8715-224">Microsoft 계정 또는 select를 사용 하 여 로그인 하거나이 시점에서 **나중** 오른쪽 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-224">At this point, either sign in with your Microsoft account or select **Not Now** in the lower right corner.</span></span>

![링크를](getting-started/_static/image7.png)

<span data-ttu-id="b8715-226">를 시작 하려면 빈 웹 사이트를 만들 하 고 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-226">To begin, you'll create a blank website and add a page.</span></span> <span data-ttu-id="b8715-227">이 자습서의 뒷부분에서 기본 제공 웹 사이트 템플릿 중 하나을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-227">In a later tutorial in this set you'll play with one of the built-in website templates.</span></span>

<span data-ttu-id="b8715-228">시작 창에서 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-228">In the start window, click **New**.</span></span>

![WebMatrix 시작 화면](getting-started/_static/image8.png)

<span data-ttu-id="b8715-230">서식 파일은 미리 작성 된 파일 및 다른 유형의 웹 사이트에 대 한 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-230">Templates are prebuilt files and pages for different types of websites.</span></span> <span data-ttu-id="b8715-231">기본적으로 사용할 수 있는 서식 파일의 모든을 보려면 템플릿 갤러리 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-231">To see all of the templates that are available by default, select the Template Gallery option.</span></span>

![선택 템플릿 갤러리](getting-started/_static/image9.png)

<span data-ttu-id="b8715-233">에 **빠른 시작** 창에서 **빈 사이트** 에서 **ASP.NET** 그룹화 하 고 새 사이트 "WebPagesMovies" 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-233">In the **Quick Start** window, select **Empty Site** from the **ASP.NET** group and name the new site "WebPagesMovies".</span></span>

![선택 된 빈 사이트 템플릿 사용 하 여 WebMatrix 빠른 시작 창](getting-started/_static/image10.png)

<span data-ttu-id="b8715-235">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-235">Click **Next**.</span></span>

<span data-ttu-id="b8715-236">Microsoft 계정에 로그인 하면 Azure에서 사이트를 만들 수 있습니다를 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-236">If you have signed in to your Microsoft account, you will be given the opportunity to create the site on Azure.</span></span> <span data-ttu-id="b8715-237">기본 이름은 사이트의 이름에 따라 **WebPagesMovies.azurewebsites.net** 제안 됩니다; 그러나 느낌표가이 이름은 Windows Azure에서 제공 하지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-237">Based on the name of your site, the default name of **WebPagesMovies.azurewebsites.net** is suggested; however, the exclamation point indicates that this name is not available on Windows Azure.</span></span> <span data-ttu-id="b8715-238">간단히 하기 위해 선택 **Skip** 지금은 Azure에서 웹 사이트를 만드는 무시 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-238">For simplicity, select **Skip** to bypass creating the web site on Azure right now.</span></span> <span data-ttu-id="b8715-239">이 시리즈의 뒷부분에 나오는 azure 사이트를 발표 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-239">Later in this series, we will publish the site to Azure.</span></span>

![azure 사이트 만들기](getting-started/_static/image11.png)

<span data-ttu-id="b8715-241">WebMatrix를 만들고 해당 사이트:</span><span class="sxs-lookup"><span data-stu-id="b8715-241">WebMatrix creates and opens the site:</span></span>

![에 열어 새 WebPagesMovies 사이트](getting-started/_static/image12.png)

<span data-ttu-id="b8715-243">맨 위에 있는 빠른 실행 도구 모음 및가 리본 메뉴</span><span class="sxs-lookup"><span data-stu-id="b8715-243">At the top, there's a Quick Access Toolbar and a ribbon.</span></span> <span data-ttu-id="b8715-244">왼쪽 아래에 표시 작업 영역 선택기 작업 간에 전환 하는 위치 (**사이트**, **파일**, **데이터베이스**, **보고서**).</span><span class="sxs-lookup"><span data-stu-id="b8715-244">At the bottom left, you see the workspace selector where you switch between tasks (**Site**, **Files**, **Databases**, **Reports**).</span></span> <span data-ttu-id="b8715-245">오른쪽 편집기 및 보고서에 대 한 콘텐츠 창이입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-245">On the right is the content pane for the editor and for reports.</span></span> <span data-ttu-id="b8715-246">및 아래쪽 종종 보게 메시지에 대 한 알림 표시줄입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-246">And across the bottom you'll occasionally see a notification bar for messages.</span></span>

<span data-ttu-id="b8715-247">이 자습서를 진행할 때 WebMatrix 및 해당 기능에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-247">You'll learn more about WebMatrix and its features as you go through these tutorials.</span></span>

## <a name="creating-a-web-page"></a><span data-ttu-id="b8715-248">웹 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="b8715-248">Creating a Web Page</span></span>

<span data-ttu-id="b8715-249">WebMatrix 및 ASP.NET 웹 페이지를 살펴, 간단한 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-249">To become familiar with WebMatrix and ASP.NET Web Pages, you'll create a simple page.</span></span>

<span data-ttu-id="b8715-250">작업 영역 편집기 도구 모음에서 선택 된 **파일** 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-250">In the workspace selector, select the **Files** workspace.</span></span> <span data-ttu-id="b8715-251">이 작업 영역에는 파일 및 폴더를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-251">This workspace lets you work with files and folders.</span></span> <span data-ttu-id="b8715-252">왼쪽된 창 사이트의 파일 구조를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-252">The left pane shows the file structure of your site.</span></span> <span data-ttu-id="b8715-253">파일 관련 작업을 표시 하는 리본 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-253">The ribbon changes to show file-related tasks.</span></span>

![WebMatrix에서 파일 작업 영역](getting-started/_static/image13.png)

<span data-ttu-id="b8715-255">리본 메뉴에 아래의 화살표를 클릭 합니다. **새로** 클릭 하 고 **새 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-255">In the ribbon, click the arrow under **New** and then click **New File**.</span></span>

![사용 하는 &quot;새로&quot; 새 파일을 만들려면 리본 메뉴의 명령을](getting-started/_static/image14.png)

<span data-ttu-id="b8715-257">WebMatrix에는 파일 형식 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-257">WebMatrix displays a list of file types.</span></span> <span data-ttu-id="b8715-258">선택 **CSHTML**, 및는 **이름** "HelloWorld"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-258">Select **CSHTML**, and in the **Name** box, type "HelloWorld".</span></span> <span data-ttu-id="b8715-259">CSHTML 페이지에는 ASP.NET 웹 페이지 페이지가입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-259">A CSHTML page is an ASP.NET Web Pages page.</span></span>

![HelloWorld.cshtml 라는 새 CSHTML 페이지 만들기](getting-started/_static/image15.png)

<span data-ttu-id="b8715-261">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-261">Click **OK**.</span></span>

<span data-ttu-id="b8715-262">WebMatrix 페이지를 만들고이 편집기에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-262">WebMatrix creates the page and opens it in the editor.</span></span>

![WebMatrix 편집기에서 새 HelloWorld 페이지](getting-started/_static/image16.png)

<span data-ttu-id="b8715-264">볼 수 있듯이 페이지 대부분 일반 HTML 태그를 다음과 같은 맨 위에 있는 블록을 제외한 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-264">As you can see, the page contains mostly ordinary HTML markup, except for a block at the top that looks like this:</span></span>

[!code-cshtml[Main](getting-started/samples/sample1.cshtml)]

<span data-ttu-id="b8715-265">코드를 추가, 잠시 후에 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-265">That's for adding code, as you'll see shortly.</span></span>

<span data-ttu-id="b8715-266">해당 페이지의 다른 부분 &mdash; 요소 이름, 특성 및 텍스트와 맨 위에 블록이-는 서로 다른 색으로 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-266">Notice that the different parts of the page &mdash; the element names, attributes, and text, plus the block at the top — are all in different colors.</span></span> <span data-ttu-id="b8715-267">이 라고 *구문 강조 표시*를 보다 쉽게 지우기 모든 항목을 유지 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-267">This is called *syntax highlighting*, and it makes it easier to keep everything clear.</span></span> <span data-ttu-id="b8715-268">WebMatrix에서 웹 페이지를 사용 하기 쉽게 있는 기능 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-268">It's one of the features that makes it easy to work with web pages in WebMatrix.</span></span>

<span data-ttu-id="b8715-269">에 대 한 내용을 추가 `<head>` 및 `<body>` 다음 예제에서와 같은 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-269">Add content for the `<head>` and `<body>` elements like in the following example.</span></span> <span data-ttu-id="b8715-270">(원할 경우 방금 다음 블록을 복사 하 수 기존 페이지 전체를이 코드로 바꿉니다.)</span><span class="sxs-lookup"><span data-stu-id="b8715-270">(If you want, you can just copy the following block and replace the entire existing page with this code.)</span></span>

[!code-cshtml[Main](getting-started/samples/sample2.cshtml)]

<span data-ttu-id="b8715-271">빠른 실행 도구 모음 또는 **파일** 메뉴를 클릭 하 여 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-271">In the Quick Access Toolbar or in the **File** menu, click **Save**.</span></span>

![WebMatrix 빠른 실행 도구 모음에서 저장 단추](getting-started/_static/image17.png)

## <a name="testing-the-page"></a><span data-ttu-id="b8715-273">테스트 페이지</span><span class="sxs-lookup"><span data-stu-id="b8715-273">Testing the Page</span></span>

<span data-ttu-id="b8715-274">에 **파일** 작업 영역을 마우스 오른쪽 단추로 클릭는 *HelloWorld.cshtml* 페이지 한 다음 클릭 **브라우저에서 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-274">In the **Files** workspace, right-click the *HelloWorld.cshtml* page and then click **Launch in browser**.</span></span>

![WebMatrix 리본에서 [실행] 단추를 사용 하는 페이지를 실행 합니다.](getting-started/_static/image18.png)

<span data-ttu-id="b8715-276">WebMatrix는 컴퓨터에 있는 페이지를 테스트 하는 데 사용할 수 있는 기본 제공 웹 서버 (IIS Express)를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-276">WebMatrix starts a built-in web server (IIS Express) that you can use to test pages on your computer.</span></span> <span data-ttu-id="b8715-277">(사용 하지 않으면 WebMatrix에서 IIS Express는 해야 페이지는 웹 서버에 게시 어딘가에 전에 테스트할 수 있습니다.) 페이지 기본 브라우저에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-277">(Without IIS Express in WebMatrix, you'd have to publish your page to a web server somewhere before you could test it.) The page is displayed in your default browser.</span></span>

![&quot;Hello World&quot; 브라우저에서 실행 되 고 페이지](getting-started/_static/image19.png)

<span data-ttu-id="b8715-279">WebMatrix에서 페이지를 테스트할 때 브라우저의 URL은 다음과 같이 `http://localhost:33651/HelloWorld.cshtml.` 이름 *localhost* 의미 페이지가 컴퓨터에 있는 웹 서버에 의해 반환 되는 로컬 서버를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-279">Notice that when you test a page in WebMatrix, the URL in the browser is something like `http://localhost:33651/HelloWorld.cshtml.` The name *localhost* refers to a local server, meaning that the page is served by a web server that's on your own computer.</span></span> <span data-ttu-id="b8715-280">설명한 것 처럼, IIS Express는 페이지를 시작할 때 실행 되는 명명 된 웹 서버 프로그램 WebMatrix에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-280">As noted, WebMatrix includes a web server program named IIS Express that runs when you launch a page.</span></span>

<span data-ttu-id="b8715-281">다음의 숫자 *localhost* (예를 들어 *localhost:33651*) 참조 하는 *포트 번호* 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-281">The number after *localhost* (for example, *localhost:33651*) refers to a *port number* on your computer.</span></span> <span data-ttu-id="b8715-282">이 특정 웹 사이트에 대 한 사용 하 여 IIS Express는 "채널"의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-282">This is the number of the "channel" that IIS Express uses for this particular website.</span></span> <span data-ttu-id="b8715-283">포트 번호는 사이트를 만들고 만든 모든 사이트에 대 한 다른 1024 65536부터 범위에서 임의로 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-283">The port number is selected at random from the range 1024 through 65536 when you create your site, and it's different for every site that you create.</span></span> <span data-ttu-id="b8715-284">(사이트를 테스트할 때 포트 번호는 거의 항상 됩니다 33561 보다 다른 숫자를.) 각 웹 사이트에 대 한 서로 다른 포트를 사용 하 여 IIS Express 유지할 수 직선 통신 중인 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-284">(When you test your own site, the port number will almost certainly be a different number than 33561.) By using a different port for each website, IIS Express can keep straight which of your sites it's talking to.</span></span>

<span data-ttu-id="b8715-285">나중에 게시할 때 사이트에 공용 웹 서버를 더 이상 참조 *localhost* url에서입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-285">Later when you publish your site to a public web server, you no longer see *localhost* in the URL.</span></span> <span data-ttu-id="b8715-286">이때 표시와 같은 대부분의 일반적인 URL `http://myhostingsite/mywebsite/HelloWorld.cshtml` 어떤 페이지가 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-286">At that point, you'll see a more typical URL like `http://myhostingsite/mywebsite/HelloWorld.cshtml` or whatever the page is.</span></span> <span data-ttu-id="b8715-287">이 자습서 시리즈의 뒷부분에 나오는 사이트를 게시 하는 방법에 대 한 더 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-287">You'll learn more about publishing a site later in this tutorial series.</span></span>

## <a name="adding-some-server-side-code"></a><span data-ttu-id="b8715-288">서버 쪽 코드 추가</span><span class="sxs-lookup"><span data-stu-id="b8715-288">Adding Some Server-Side Code</span></span>

<span data-ttu-id="b8715-289">브라우저를 닫고 WebMatrix에서 페이지로 다시 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-289">Close the browser and go back to the page in WebMatrix.</span></span>

<span data-ttu-id="b8715-290">다음 코드 처럼 표시 되도록 코드 블록을 한 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-290">Add a line to the code block so that it looks like the following code:</span></span>

[!code-cshtml[Main](getting-started/samples/sample3.cshtml)]

<span data-ttu-id="b8715-291">약간의 Razor 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-291">This is a little bit of Razor code.</span></span> <span data-ttu-id="b8715-292">현재 날짜 및 시간을 가져옵니다 하 고 해당 값에 아마도 명확는 *변수* 라는 `currentDateTime`합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-292">It's probably clear that it gets the current date and time and puts that value into a *variable* named `currentDateTime`.</span></span> <span data-ttu-id="b8715-293">읽게 되는 내용은 다음 자습서에서 Razor 구문에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-293">You'll read more about Razor syntax in the next tutorial.</span></span>

<span data-ttu-id="b8715-294">페이지의 본문에서 후는 `<p>Hello World!</p>` 요소를 다음에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-294">In the body of the page, after the `<p>Hello World!</p>` element, add the following:</span></span>

[!code-html[Main](getting-started/samples/sample4.html)]

<span data-ttu-id="b8715-295">이 코드를 설정 하는 값을 가져옵니다는 `currentDateTime` 변수 맨 위에 있는 페이지의 태그에 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-295">This code gets the value that you put into the `currentDateTime` variable at the top and inserts it into the markup of the page.</span></span> <span data-ttu-id="b8715-296">`@` 문자 페이지에서 ASP.NET 웹 페이지 코드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-296">The `@` character marks the ASP.NET Web Pages code in the page.</span></span>

<span data-ttu-id="b8715-297">(WebMatrix 변경 내용을 저장 하면에 대 한 페이지를 실행 하기 전에)의 페이지를 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-297">Run the page again (WebMatrix saves the changes for you before it runs the page).</span></span> <span data-ttu-id="b8715-298">이 시간 날짜 및 시간 페이지에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-298">This time you see the date and time in the page.</span></span>

![&quot;Hello World&quot; 동적으로 생성 된 시간 표시를 사용 하 여 브라우저에서 실행 되 고 페이지](getting-started/_static/image20.png)

<span data-ttu-id="b8715-300">몇 분 정도 후 브라우저에서 페이지를 새로 고 치세요.</span><span class="sxs-lookup"><span data-stu-id="b8715-300">Wait a few moments and then refresh the page in the browser.</span></span> <span data-ttu-id="b8715-301">날짜 및 시간 디스플레이가 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-301">The date and time display is updated.</span></span>

<span data-ttu-id="b8715-302">브라우저에서 페이지 소스를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-302">In the browser, look at the page source.</span></span> <span data-ttu-id="b8715-303">다음 태그 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-303">It looks like the following markup:</span></span>

[!code-html[Main](getting-started/samples/sample5.html)]

<span data-ttu-id="b8715-304">에 `@{ }` 블록이 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-304">Notice that the `@{ }` block at the top isn't there.</span></span> <span data-ttu-id="b8715-305">또한가 표시 된 날짜 및 시간 표시는 실제 문자열 (`1/18/2012 2:49:50 PM` 또는)이 아니라 `@currentDateTime` 에서 제공 되었던 처럼는 *.cshtml* 페이지.</span><span class="sxs-lookup"><span data-stu-id="b8715-305">Also notice that the date and time display shows an actual string of characters (`1/18/2012 2:49:50 PM` or whatever), not `@currentDateTime` like you had in the *.cshtml* page.</span></span> <span data-ttu-id="b8715-306">여기서는 페이지를 실행 한 경우 ASP.NET을 처리 하는 모든 코드 (거의이 경우)로 표시 된 변경 사항 `@`합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-306">What happened here is that when you ran the page, ASP.NET processed all the code (very little in this case) that was marked with `@`.</span></span> <span data-ttu-id="b8715-307">코드 출력을 생성 하 고 해당 출력의 페이지에 삽입 된 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-307">The code produces output, and that output was inserted into the page.</span></span>

## <a name="this-is-what-aspnet-web-pages-are-about"></a><span data-ttu-id="b8715-308">이에 대 한 ASP.NET 웹 페이지는</span><span class="sxs-lookup"><span data-stu-id="b8715-308">This Is What ASP.NET Web Pages Are About</span></span>

<span data-ttu-id="b8715-309">된 ASP.NET 웹 페이지 생성 동적 웹 콘텐츠를 읽을 때 개념은 무엇을 보았을 여기 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-309">When you read that ASP.NET Web Pages produces dynamic web content, what you've seen here is the idea.</span></span> <span data-ttu-id="b8715-310">방금 만든 페이지 하기 전에 살펴 보았으며 하는 동일한 HTML 태그를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-310">The page you just created contains the same HTML markup that you've seen before.</span></span> <span data-ttu-id="b8715-311">모든 종류의 작업을 수행할 수 있는 코드를 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-311">It can also contain code that can perform all sorts of tasks.</span></span> <span data-ttu-id="b8715-312">이 예제에서는 trivial 작업의 현재 날짜와 시간을 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-312">In this example, it did the trivial task of getting the current date and time.</span></span> <span data-ttu-id="b8715-313">살펴본 것 처럼 페이지에서 출력을 생성 하는 html 코드 중간에 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-313">As you saw, you can intersperse code with the HTML to produce output in the page.</span></span> <span data-ttu-id="b8715-314">다른 사람이 요청 하는 경우는 *.cshtml* ASP.NET 브라우저에서 페이지에 웹 서버에에서 있는 동안 해당 페이지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-314">When someone requests a *.cshtml* page in the browser, ASP.NET processes the page while it's still in the hands of the web server.</span></span> <span data-ttu-id="b8715-315">ASP.NET 코드의 출력 (있는 경우)에 삽입 페이지 HTML로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-315">ASP.NET inserts the output of the code (if any) into the page as HTML.</span></span> <span data-ttu-id="b8715-316">코드 처리가 완료 되 면 ASP.NET 결과 페이지를 브라우저에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-316">When the code processing is done, ASP.NET sends the resulting page to the browser.</span></span> <span data-ttu-id="b8715-317">브라우저가 현재까지 받는 HTML입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-317">All the browser ever gets is HTML.</span></span> <span data-ttu-id="b8715-318">다음 다이어그램은입니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-318">Here's a diagram:</span></span>

![ASP.NET 설명 생성 방법을 HTML 동적으로 개념적 흐름](getting-started/_static/image21.png)

<span data-ttu-id="b8715-320">개념은 간단 하지만 여러 흥미로운 작업을 코드로 수행할 수 있으며 여러 가지 흥미로운를 동적으로 추가할 수 HTML 콘텐츠 페이지.</span><span class="sxs-lookup"><span data-stu-id="b8715-320">The idea is simple, but there are many interesting tasks that the code can perform, and there are many interesting ways in which you can dynamically add HTML content to the page.</span></span> <span data-ttu-id="b8715-321">및 ASP.NET *.cshtml* 자체 (JavaScript 및 jQuery 코드) 브라우저에서 실행 되는 코드 페이지, HTML 페이지, 처럼 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-321">And ASP.NET *.cshtml* pages, like any HTML page, can also include code that runs in the browser itself (JavaScript and jQuery code).</span></span> <span data-ttu-id="b8715-322">이 자습서에서는 및 이후의 조건은에서 이러한 작업을 모두 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-322">You'll explore all of these things in this tutorial set and in subsequent ones.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="b8715-323">다음에 나오는</span><span class="sxs-lookup"><span data-stu-id="b8715-323">Coming Up Next</span></span>

<span data-ttu-id="b8715-324">이 시리즈의 다음 자습서에서는 ASP.NET 웹 페이지 프로그래밍 좀 더 살펴볼 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-324">In the next tutorial in this series, you explore ASP.NET Web Pages programming a little more.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b8715-325">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b8715-325">Additional Resources</span></span>

<span data-ttu-id="b8715-326">[ASP.NET 웹 사이트를 처음부터 만들](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-326">[Create an ASP.NET website from scratch](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch).</span></span> <span data-ttu-id="b8715-327">이것은 자습서를 WebMatrix (하지: ASP.NET 웹 페이지)를 사용 하는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8715-327">This is a tutorial that's specifically about using WebMatrix (not ASP.NET Web Pages).</span></span> <span data-ttu-id="b8715-328">이동에 약간이 자습서에서는 다루지 않습니다 WebMatrix의 추가 기능 중 일부에 대 한 자세한 정보.</span><span class="sxs-lookup"><span data-stu-id="b8715-328">It goes into a little more detail about some of the additional features of WebMatrix that we won't cover in this tutorial set.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="b8715-329">다음</span><span class="sxs-lookup"><span data-stu-id="b8715-329">Next</span></span>](intro-to-web-pages-programming.md)
