---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
title: ASP.NET 웹 페이지-Getting Started 소개 | Microsoft Docs
author: tfitzmac
description: WebMatrix는 더 이상 권장 통합된 개발 환경으로 ASP.NET 웹 페이지에 대 한 합니다. Visual Studio 또는 Visual Studio Code를 사용 합니다. 이 설명서는 중...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: a36d3bdf-ef1b-47a4-b932-3a0cf4cad716
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
msc.type: authoredcontent
ms.openlocfilehash: 12878082306cf51f8ea08ae614d9420251ecb587
ms.sourcegitcommit: 8bf4dff3069e62972c1b0839a93fb444e502afe7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/20/2018
ms.locfileid: "46482959"
---
<a name="introducing-aspnet-web-pages---getting-started"></a><span data-ttu-id="f5227-105">시작-ASP.NET 웹 페이지 소개</span><span class="sxs-lookup"><span data-stu-id="f5227-105">Introducing ASP.NET Web Pages - Getting Started</span></span>
====================
<span data-ttu-id="f5227-106">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="f5227-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE[](~/includes/rp.md)]

> > [!NOTE] 
> > 
> > <span data-ttu-id="f5227-107">WebMatrix는 더 이상 권장 통합된 개발 환경으로 ASP.NET 웹 페이지에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-107">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="f5227-108">사용 하 여 [Visual Studio](../program-asp-net-web-pages-in-visual-studio.md) 하거나 [Visual Studio Code](https://code.visualstudio.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-108">Use [Visual Studio](../program-asp-net-web-pages-in-visual-studio.md) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>
> 
> 
> <span data-ttu-id="f5227-109">이 지침과 응용 프로그램 사용 하면 ASP.NET 웹 페이지 (버전 2 이상)의 개요 및 Razor 구문, 동적 웹 사이트를 만들기 위한 간단한 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-109">This guidance and application gives you an overview of ASP.NET Web Pages (version 2 or later) and Razor syntax, a lightweight framework for creating dynamic websites.</span></span> <span data-ttu-id="f5227-110">또한 WebMatrix, 페이지 및 사이트를 만들기 위한 도구를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-110">It also introduces WebMatrix, a tool for creating pages and sites.</span></span>
> 
> <span data-ttu-id="f5227-111">**수준**: 새 ASP.NET 웹 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-111">**Level**: New to ASP.NET Web Pages.</span></span>  
> <span data-ttu-id="f5227-112">**가정 하는 기술을**: HTML, 기본 css 스타일 시트 ().</span><span class="sxs-lookup"><span data-stu-id="f5227-112">**Skills assumed**: HTML, basic cascading style sheets (CSS).</span></span>
> 
> <span data-ttu-id="f5227-113">학습할 내용 집합의 첫 번째 자습서에서:</span><span class="sxs-lookup"><span data-stu-id="f5227-113">What you'll learn in the first tutorial of the set:</span></span>
> 
> - <span data-ttu-id="f5227-114">ASP.NET Web Pages 기술 이며에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-114">What ASP.NET Web Pages technology is and what it's for.</span></span>
> - <span data-ttu-id="f5227-115">WebMatrix의는입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-115">What WebMatrix is.</span></span>
> - <span data-ttu-id="f5227-116">모든 항목을 설치 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-116">How to install everything.</span></span>
> - <span data-ttu-id="f5227-117">WebMatrix를 사용 하 여 웹 사이트를 만드는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-117">How to create a website by using WebMatrix.</span></span>
>   
> 
> <span data-ttu-id="f5227-118">기능/기술을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-118">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="f5227-119">Microsoft 웹 플랫폼 설치 관리자</span><span class="sxs-lookup"><span data-stu-id="f5227-119">Microsoft Web Platform Installer.</span></span>
> - <span data-ttu-id="f5227-120">WebMatrix 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-120">WebMatrix.</span></span>
> - <span data-ttu-id="f5227-121">*.cshtml* 페이지</span><span class="sxs-lookup"><span data-stu-id="f5227-121">*.cshtml* pages</span></span>
>   
> 
> <span data-ttu-id="f5227-122">Mike 되는 원래이 자습서를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-122">Mike Pope originally wrote this tutorial.</span></span> <span data-ttu-id="f5227-123">Tom FitzMacken Microsoft WebMatrix 3에 대 한 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-123">Tom FitzMacken updated it for Microsoft WebMatrix 3.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f5227-124">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="f5227-124">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="f5227-125">ASP.NET Web Pages (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="f5227-125">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="f5227-126">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="f5227-126">WebMatrix 3</span></span>


## <a name="what-should-you-know"></a><span data-ttu-id="f5227-127">무엇을 알아야 합니다 있습니다?</span><span class="sxs-lookup"><span data-stu-id="f5227-127">What Should You Know?</span></span>

<span data-ttu-id="f5227-128">사용 하 여 친숙 하다는 것으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-128">We're assuming that you're familiar with:</span></span>

- <span data-ttu-id="f5227-129">**HTML**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-129">**HTML**.</span></span> <span data-ttu-id="f5227-130">없는 심층적인 전문 지식이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-130">No in-depth expertise is required.</span></span> <span data-ttu-id="f5227-131">HTML 설명 하지 않겠습니다 것도 사용 하지 마십시오 복잡 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-131">We won't explain HTML, but we also don't use anything complex.</span></span> <span data-ttu-id="f5227-132">여기서 생각 유용 HTML 자습서의 링크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-132">We'll provide links to HTML tutorials where we think they're useful.</span></span>
- <span data-ttu-id="f5227-133">**Css 스타일 시트 ()** 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-133">**Cascading style sheets (CSS)**.</span></span> <span data-ttu-id="f5227-134">과 HTML입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-134">Same as with HTML.</span></span>
- <span data-ttu-id="f5227-135">**기본 데이터베이스 아이디어**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-135">**Basic database ideas**.</span></span> <span data-ttu-id="f5227-136">데이터에 대 한 스프레드시트를 사용 하 고 정렬 하 고 수준의 전문성을를 데이터를 필터링 하는 경우이 자습서 집합 일반적으로 하는 것 이라고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-136">If you've used a spreadsheet for data and sorted and filtered the data, that's the level of expertise we're generally assuming for this tutorial set.</span></span>

<span data-ttu-id="f5227-137">기본 프로그래밍을 알아보는 데 관심이 있다고도 하는 것으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-137">We're also assuming that you're interested in learning basic programming.</span></span> <span data-ttu-id="f5227-138">ASP.NET Web Pages 라는 C# 프로그래밍 언어를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-138">ASP.NET Web Pages use a programming language called C#.</span></span> <span data-ttu-id="f5227-139">프로그래밍에서는 방금 것에 관심이 있는 배경 지식이 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-139">You don't have to have any background in programming, just an interest in it.</span></span> <span data-ttu-id="f5227-140">그 어느 때 하기 전에 웹 페이지에서 JavaScript를 작성 한, 배경의 충분 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-140">If you've ever written any JavaScript in a web page before, you've got plenty of background.</span></span>

<span data-ttu-id="f5227-141">신규 프로그래머 속도 제공 하는 동안는 프로그래밍에 익숙한 경우 볼 수 있습니다이 자습서를 처음 설정 하는 참고 느리게 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-141">Note that if you are familiar with programming, you might find that this tutorial set initially moves slowly while we bring new programmers up to speed.</span></span> <span data-ttu-id="f5227-142">첫 번째 몇 가지 자습서 이전 해지면 하지만 작은 기본 프로그래밍에 대해 설명 하 고 작업 빠른 클립에 따라 이동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-142">As we get past the first few tutorials, though, there will be less basic programming to explain and things will move along at a faster clip.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="f5227-143">무엇이 필요?</span><span class="sxs-lookup"><span data-stu-id="f5227-143">What Do You Need?</span></span>

<span data-ttu-id="f5227-144">필요한 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-144">Here's what you'll need:</span></span>

- <span data-ttu-id="f5227-145">Windows 8, Windows 7, Windows Server 2008 또는 Windows Server 2012를 실행 하는 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-145">A computer that is running Windows 8, Windows 7, Windows Server 2008, or Windows Server 2012.</span></span>
- <span data-ttu-id="f5227-146">인터넷으로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-146">A live internet connection.</span></span>
- <span data-ttu-id="f5227-147">관리자 권한 (설치 과정에 필요).</span><span class="sxs-lookup"><span data-stu-id="f5227-147">Administrator privileges (required for the installation process).</span></span>

## <a name="what-is-aspnet-web-pages"></a><span data-ttu-id="f5227-148">ASP.NET 웹 페이지는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f5227-148">What Is ASP.NET Web Pages?</span></span>

<span data-ttu-id="f5227-149">ASP.NET 웹 페이지에는 동적 웹 페이지를 만드는 데 사용할 수 있는 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-149">ASP.NET Web Pages is a framework that you can use to create dynamic web pages.</span></span> <span data-ttu-id="f5227-150">간단한 HTML 웹 페이지를 정적입니다. 콘텐츠는 페이지에는 HTML 태그를 고정된 하 여 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-150">A simple HTML web page is static; its content is determined by the fixed HTML markup that's in the page.</span></span> <span data-ttu-id="f5227-151">ASP.NET 웹 페이지를 사용 하 여 만든 것과 같은 동적 페이지 코드를 사용 하 여 즉석에서 페이지 콘텐츠를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-151">Dynamic pages like those you create with ASP.NET Web Pages let you create the page content on the fly, by using code.</span></span>

<span data-ttu-id="f5227-152">동적 페이지를 통해 모든 종류의 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-152">Dynamic pages let you do all sorts of things.</span></span> <span data-ttu-id="f5227-153">폼을 사용 하 여 입력 메시지를 표시 하 고 페이지를 표시 하는 내용 또는 모양을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-153">You can ask a user for input by using a form and then change what the page displays or how it looks.</span></span> <span data-ttu-id="f5227-154">사용자 로부터 정보를 사용 하 고, 데이터베이스에 저장 하 고, 다음 나중에 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-154">You can take information from a user, save it in a database, and then list it later.</span></span> <span data-ttu-id="f5227-155">사이트에서 전자 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-155">You can send email from your site.</span></span> <span data-ttu-id="f5227-156">(예: 매핑 서비스) 웹에서 다른 서비스와 상호 작용할 수 있으며 해당 소스에서 정보를 통합 하는 페이지를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-156">You can interact with other services on the web (for example, a mapping service) and produce pages that integrate information from those sources.</span></span>

## <a name="what-is-webmatrix"></a><span data-ttu-id="f5227-157">WebMatrix는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="f5227-157">What is WebMatrix?</span></span>

<span data-ttu-id="f5227-158">WebMatrix는 웹 페이지 편집기, 데이터베이스 유틸리티, 페이지 및 웹 사이트를 인터넷에 게시 하기 위한 기능 테스트에 대 한 웹 서버를 통합 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-158">WebMatrix is a tool that integrates a web page editor, a database utility, a web server for testing pages, and features for publishing your website to the Internet.</span></span> <span data-ttu-id="f5227-159">WebMatrix는 무료로 사용할 수 있는 및 설치 하 고 사용 하기 쉬운 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-159">WebMatrix is free, and it's easy to install and easy to use.</span></span> <span data-ttu-id="f5227-160">(또한 작동 일반 HTML 페이지 및 PHP와 같은 다른 기술에 대 한 합니다.)</span><span class="sxs-lookup"><span data-stu-id="f5227-160">(It also works for just plain HTML pages, as well as for other technologies like PHP.)</span></span>

<span data-ttu-id="f5227-161">실제로 하지 *있는* WebMatrix를 사용 하 여 ASP.NET 웹 페이지를 사용 하 여 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-161">You don't actually *have* to use WebMatrix to work with ASP.NET Web Pages.</span></span> <span data-ttu-id="f5227-162">편집기에서 텍스트를 사용 하 여 페이지를 만드는 예를 들어 하 수에 대 한 액세스를 해야 하는 웹 서버를 사용 하 여 페이지를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-162">You can create pages by using a text editor, for example, and test pages by using a web server that you have access to.</span></span> <span data-ttu-id="f5227-163">그러나 WebMatrix 모두 매우 쉽게,이 자습서 전체에서 WebMatrix를 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-163">However, WebMatrix makes it all very easy, so these tutorials will use WebMatrix throughout.</span></span>

## <a name="about-these-tutorials"></a><span data-ttu-id="f5227-164">이 자습서에 대 한</span><span class="sxs-lookup"><span data-stu-id="f5227-164">About These Tutorials</span></span>

<span data-ttu-id="f5227-165">이 자습서 집합은 ASP.NET 웹 페이지를 사용 하는 방법 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-165">This tutorial set is an introduction to how to use ASP.NET Web Pages.</span></span> <span data-ttu-id="f5227-166">이 소개 자습서 집합에서 총 9 자습서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-166">There are 9 tutorials total in this introductory tutorial set.</span></span> <span data-ttu-id="f5227-167">실제, 전문적인 웹 사이트를 만드는 ASP.NET Web Pages 초보자에서 안내 하는 일련의 자습서 집합 느껴집니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-167">It's part of a series of tutorial sets that takes you from ASP.NET Web Pages novice to creating real, professional-looking websites.</span></span>

<span data-ttu-id="f5227-168">이 첫 번째 자습서에서 ASP.NET 웹 페이지를 사용 하 여 작업 하는 방법의 기본 사항을 보여 주는 중점적으로 다룹니다를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-168">This first tutorial set concentrates on showing you the basics of how to work with ASP.NET Web Pages.</span></span> <span data-ttu-id="f5227-169">완료 되 면이 종료 하 고 좀 더 깊이 웹 페이지를 탐색 하는 위치를 선택 하는 추가 자습서 집합으로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-169">When you're done, you can work with additional tutorial sets that pick up where this one ends and that explore Web Pages in more depth.</span></span>

<span data-ttu-id="f5227-170">에서는 의도적으로 이동 쉽게 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-170">We deliberately go easy on the in-depth explanations.</span></span> <span data-ttu-id="f5227-171">선택한 항목 살펴보겠습니다 때마다이 자습서 집합에 대 한에서는 항상 생각 하는 방식은 가장 이해 하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-171">And whenever we show something, for this tutorial set we always choose the way that we think is easiest to understand.</span></span> <span data-ttu-id="f5227-172">이후 자습서 더 심층적으로 살펴보는 집합과 보다 효율적인 또는 보다 유연한 방법 (더 재미도)를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-172">Later tutorial sets go into more depth and show you more efficient or more flexible approaches (also more fun).</span></span> <span data-ttu-id="f5227-173">하지만 이러한 자습서를 먼저 기본 사항을 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-173">But those tutorials require you to understand the basics first.</span></span>

<span data-ttu-id="f5227-174">방금 시작한 자습서 집합 ASP.NET 웹 페이지의 이러한 기능에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-174">The tutorial set you've just started covers these features of ASP.NET Web Pages:</span></span>

- <span data-ttu-id="f5227-175">소개 및 시작 하는 모든 항목이 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-175">Introduction and getting everything installed.</span></span> <span data-ttu-id="f5227-176">(이것이 여러분 글을 읽고 자습서입니다.)</span><span class="sxs-lookup"><span data-stu-id="f5227-176">(That's in the tutorial you're reading.)</span></span>
- <span data-ttu-id="f5227-177">ASP.NET 웹 페이지 프로그래밍의 기초입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-177">The basics of ASP.NET Web Pages programming.</span></span>
- <span data-ttu-id="f5227-178">데이터베이스를 만드는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-178">Creating a database.</span></span>
- <span data-ttu-id="f5227-179">만들기 및 사용자 입력된 양식을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-179">Creating and processing a user input form.</span></span>
- <span data-ttu-id="f5227-180">추가, 업데이트 및 데이터베이스의 데이터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-180">Adding, updating, and deleting data in the database.</span></span>

## <a name="what-will-you-create"></a><span data-ttu-id="f5227-181">만드나요?</span><span class="sxs-lookup"><span data-stu-id="f5227-181">What Will You Create?</span></span>

<span data-ttu-id="f5227-182">이 자습서 집합 및 이후의 조건은 원하는 영화를 나열할 수 있는 웹 사이트를 중심으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-182">This tutorial set and subsequent ones revolve around a website where you can list movies that you like.</span></span> <span data-ttu-id="f5227-183">영화를 입력 하면 편집 하 고 나열을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-183">You'll be able to enter movies, edit them, and list them.</span></span> <span data-ttu-id="f5227-184">이 자습서 집합에서 만들어야 하는 페이지를 가지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-184">Here are a couple of the pages you'll create in this tutorial set.</span></span> <span data-ttu-id="f5227-185">첫 번째 목록 페이지를 만들어야 하는 영화를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-185">The first one shows the movie listing page that you'll create:</span></span>

![동영상 목록을 보여 주는 완료 했습니다 동영상 앱](getting-started/_static/image1.png)

<span data-ttu-id="f5227-187">그리고은 사이트에 새 영화 정보를 추가할 수 있는 페이지.</span><span class="sxs-lookup"><span data-stu-id="f5227-187">And here's the page that lets you add new movie information to your site:</span></span>

![추가 동영상 페이지를 보여 주는 완료 된 동영상 앱](getting-started/_static/image2.png)

<span data-ttu-id="f5227-189">후속 자습서 집합 빌드에 설정 하 고, 전자 메일 보내기 및 소셜 미디어 통합에 로그인 하는 사람, 사진 업로드 같은 더 많은 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-189">Subsequent tutorial sets build on this set and add more functionality, like uploading pictures, letting people log in, sending email, and integrating with social media.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="f5227-190">Azure에서 실행 되는이 앱 참조</span><span class="sxs-lookup"><span data-stu-id="f5227-190">See this App Running on Azure</span></span>

<span data-ttu-id="f5227-191">라이브 웹 앱으로 실행 하는 완성 된 사이트를 참조 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="f5227-191">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="f5227-192">다음 단추를 클릭 하 여 Azure 계정에 앱의 전체 버전을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-192">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebPagesMovies)

<span data-ttu-id="f5227-193">이 솔루션을 Azure에 배포 하려면 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-193">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="f5227-194">계정이 아직 없는 경우 다음 옵션:</span><span class="sxs-lookup"><span data-stu-id="f5227-194">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="f5227-195">[Azure 계정을 무료로 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -크레딧을 받게 사용 하면 유료 Azure 서비스를 사용해볼 수 있습니다 하 고 사용한 후에 계정을 유지 하면 최대 사용 하 여 무료 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-195">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="f5227-196">[MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -MSDN 구독은 크레딧을 매달 제공 유료 Azure 서비스에 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-196">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="installing-everything"></a><span data-ttu-id="f5227-197">모든 설치</span><span class="sxs-lookup"><span data-stu-id="f5227-197">Installing Everything</span></span>

<span data-ttu-id="f5227-198">Microsoft에서 웹 플랫폼 설치 관리자를 사용 하 여 모든 항목을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-198">You can install everything by using the Web Platform Installer from Microsoft.</span></span> <span data-ttu-id="f5227-199">실제로 설치 관리자를 설치 하 고를 사용 하 여 다른 모든 요소를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-199">In effect, you install the installer, and then use it to install everything else.</span></span>

<span data-ttu-id="f5227-200">웹 페이지를 사용 하려면 적어도 대해서도 해야 Windows Server 2008 이상 또는 Windows XP SP3 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-200">To use Web Pages, you have to be have at least Windows XP with SP3 installed, or Windows Server 2008 or later.</span></span>

<span data-ttu-id="f5227-201">에 [웹 페이지의 페이지](../../../index.md) ASP.NET 웹 사이트 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-201">On the [Web Pages page](../../../index.md) of the ASP.NET website, click **Install**.</span></span>

![ASP.NET 웹 사이트 표시 &quot;WebMatrix 설치&quot; 단추](getting-started/_static/image3.png)

<span data-ttu-id="f5227-203">개인정보취급방침 WebMatrix를 설치 하기 전에 사용 약관에 동의 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-203">You are asked to accept the license terms and privacy statement before installing WebMatrix.</span></span>

![설치를 시작 하는 용어를 허용 합니다.](getting-started/_static/image4.png)

<span data-ttu-id="f5227-205">클릭 **실행** 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-205">Click **Run** to start the installation.</span></span> <span data-ttu-id="f5227-206">(설치 관리자를 저장 하려면 클릭 **저장할** 다음 저장 폴더에서 설치 관리자를 실행 합니다.)</span><span class="sxs-lookup"><span data-stu-id="f5227-206">(If you want to save the installer, click **Save** and then run the installer from the folder where you saved it.)</span></span>

![](getting-started/_static/image5.png)

<span data-ttu-id="f5227-207">웹 플랫폼 설치 관리자를 표시 하는 작업은 WebMatrix를 설치할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-207">The Web Platform Installer appears, ready to install WebMatrix.</span></span> <span data-ttu-id="f5227-208">**설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-208">Click **Install**.</span></span>

![](getting-started/_static/image6.png)

<span data-ttu-id="f5227-209">설치 프로세스는 컴퓨터에 설치 하는 것에 파악 하 고 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-209">The installation process figures out what it has to install on your computer and starts the process.</span></span> <span data-ttu-id="f5227-210">어떤 정확 하 게 설치할 수에 따라 프로세스 걸릴 수 있습니다 몇 분에서 몇 분 정도입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-210">Depending on what exactly has to be installed, the process can take anywhere from a few moments to several minutes.</span></span> <span data-ttu-id="f5227-211">선택 **동의** 라이선스 사용 조건에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-211">Select **I Accept** to accept the license terms.</span></span>

## <a name="hello-webmatrix"></a><span data-ttu-id="f5227-212">Hello, WebMatrix</span><span class="sxs-lookup"><span data-stu-id="f5227-212">Hello, WebMatrix</span></span>

<span data-ttu-id="f5227-213">완료 되 면 설치 프로세스는 WebMatrix를 자동으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-213">When it's done, the installation process can launch WebMatrix automatically.</span></span> <span data-ttu-id="f5227-214">그렇지 않은 경우 Windows에서의를 **시작** 메뉴에서 **Microsoft WebMatrix**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-214">If it doesn't, in Windows, from the **Start** menu, launch **Microsoft WebMatrix**.</span></span>

<span data-ttu-id="f5227-215">WebMatrix를 처음 시작할 때 Microsoft 계정으로 Microsoft Azure에 로그인 할 수 있는 기회를 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-215">When you launch WebMatrix for the first time, you are given a chance to sign in to Microsoft Azure with your Microsoft account.</span></span> <span data-ttu-id="f5227-216">로그인 하면 Azure 통해 10 개의 무료 웹 앱 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-216">By signing in, you will receive 10 free web apps through Azure.</span></span> <span data-ttu-id="f5227-217">이러한 무료 웹 앱에 앱을 테스트 하는 편리한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-217">These free web apps provide a convenient way to test your apps.</span></span> <span data-ttu-id="f5227-218">Azure 계정이 아직 없는 경우 MSDN subscription 필요가 있습니다 [MSDN 구독 혜택을 활성화](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-218">If you don't already have an Azure account, but you do have an MSDN subscription, you can [activate your MSDN subscription benefits](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="f5227-219">이 고, 그렇지 몇 분만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-219">Otherwise, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f5227-220">자세한 내용은 참조 하세요 [Azure 무료 평가판](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-220">For details, see [Azure Free Trial](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span>

<span data-ttu-id="f5227-221">이 자습서를 계속 하려면 지금 로그인 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-221">You do not have to sign in right now to continue with this tutorial.</span></span> <span data-ttu-id="f5227-222">서명 하지 않은 이제, 하는 경우 여전히 나중에 로그인 하는 옵션을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-222">If you do not sign in now, you will still have the option to sign in later.</span></span> <span data-ttu-id="f5227-223">마지막 [항목](publishing.md) 시계열이이 자습서에서는 Azure에 웹 사이트를 배포 하는 방법에 설명, 따라서 해당 항목을 완료 하려면 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-223">The last [topic](publishing.md) in this tutorial series covers how to deploy your website to Azure; therefore, you would need to sign in to complete that topic.</span></span>

<span data-ttu-id="f5227-224">Microsoft 계정 또는 선택 로그인 하거나 이때 **나중에** 오른쪽 아래 모퉁이에서.</span><span class="sxs-lookup"><span data-stu-id="f5227-224">At this point, either sign in with your Microsoft account or select **Not Now** in the lower right corner.</span></span>

![링크를](getting-started/_static/image7.png)

<span data-ttu-id="f5227-226">시작 하려면 있습니다 빈 웹 사이트를 만들고 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-226">To begin, you'll create a blank website and add a page.</span></span> <span data-ttu-id="f5227-227">이 자습서의 뒷부분에서 기본 제공 웹 사이트 템플릿 중 하나를 사용 하 여 재생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-227">In a later tutorial in this set you'll play with one of the built-in website templates.</span></span>

<span data-ttu-id="f5227-228">시작 창에서 클릭 **새로 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-228">In the start window, click **New**.</span></span>

![WebMatrix 시작 화면](getting-started/_static/image8.png)

<span data-ttu-id="f5227-230">템플릿은 미리 작성 된 파일 및 다양 한 유형의 웹 사이트에 대 한 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-230">Templates are prebuilt files and pages for different types of websites.</span></span> <span data-ttu-id="f5227-231">기본적으로 사용할 수 있는 템플릿을 모두를 보려면 템플릿 갤러리 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-231">To see all of the templates that are available by default, select the Template Gallery option.</span></span>

![템플릿 갤러리 선택](getting-started/_static/image9.png)

<span data-ttu-id="f5227-233">에 **빠른 시작** 창에서 **빈 사이트** 에서 **ASP.NET** 그룹화 하 고 새 사이트 "WebPagesMovies" 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-233">In the **Quick Start** window, select **Empty Site** from the **ASP.NET** group and name the new site "WebPagesMovies".</span></span>

![선택한 빈 사이트 템플릿 사용 하 여 WebMatrix 빠른 시작 창](getting-started/_static/image10.png)

<span data-ttu-id="f5227-235">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-235">Click **Next**.</span></span>

<span data-ttu-id="f5227-236">Microsoft 계정에 로그인 한 경우 Azure에서 사이트를 만들 수를 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-236">If you have signed in to your Microsoft account, you will be given the opportunity to create the site on Azure.</span></span> <span data-ttu-id="f5227-237">기본 이름은 사이트의 이름을 기반으로 **WebPagesMovies.azurewebsites.net** 제안 됩니다; 그러나 느낌표가이 이름은 Windows Azure에서 제공 되지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-237">Based on the name of your site, the default name of **WebPagesMovies.azurewebsites.net** is suggested; however, the exclamation point indicates that this name is not available on Windows Azure.</span></span> <span data-ttu-id="f5227-238">간단히 하기 위해 선택 **Skip** 지금 Azure에서 웹 사이트를 작성 하지 않으려면입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-238">For simplicity, select **Skip** to bypass creating the web site on Azure right now.</span></span> <span data-ttu-id="f5227-239">이 시리즈의 뒷부분에서 Azure로 사이트를 게시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-239">Later in this series, we will publish the site to Azure.</span></span>

![azure 사이트 만들기](getting-started/_static/image11.png)

<span data-ttu-id="f5227-241">WebMatrix가 만들고 사이트가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-241">WebMatrix creates and opens the site:</span></span>

![WebMatrix에 새 WebPagesMovies 사이트 열기](getting-started/_static/image12.png)

<span data-ttu-id="f5227-243">맨 위에 있는 빠른 실행 도구 모음 및 리본 메뉴가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-243">At the top, there's a Quick Access Toolbar and a ribbon.</span></span> <span data-ttu-id="f5227-244">왼쪽 아래에 표시 작업 영역 선택기 작업 간에 전환 하는 위치 (**사이트**를 **파일**를 **데이터베이스**를 **보고서**).</span><span class="sxs-lookup"><span data-stu-id="f5227-244">At the bottom left, you see the workspace selector where you switch between tasks (**Site**, **Files**, **Databases**, **Reports**).</span></span> <span data-ttu-id="f5227-245">오른쪽의 편집기 및 보고서에 대 한 콘텐츠 창이입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-245">On the right is the content pane for the editor and for reports.</span></span> <span data-ttu-id="f5227-246">및 맨 아래에서 종종 보게 메시지에 대 한 알림 표시줄을 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-246">And across the bottom you'll occasionally see a notification bar for messages.</span></span>

<span data-ttu-id="f5227-247">이 자습서를 진행 하면서 WebMatrix 및 해당 기능에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-247">You'll learn more about WebMatrix and its features as you go through these tutorials.</span></span>

## <a name="creating-a-web-page"></a><span data-ttu-id="f5227-248">웹 페이지 만들기</span><span class="sxs-lookup"><span data-stu-id="f5227-248">Creating a Web Page</span></span>

<span data-ttu-id="f5227-249">WebMatrix 및 ASP.NET Web Pages에 익숙해지고 간단한 페이지를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-249">To become familiar with WebMatrix and ASP.NET Web Pages, you'll create a simple page.</span></span>

<span data-ttu-id="f5227-250">작업 영역 선택기를 선택 합니다 **파일** 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-250">In the workspace selector, select the **Files** workspace.</span></span> <span data-ttu-id="f5227-251">이 작업 영역에는 파일 및 폴더를 사용 하 여 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-251">This workspace lets you work with files and folders.</span></span> <span data-ttu-id="f5227-252">왼쪽된 창에 사이트의 파일 구조를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-252">The left pane shows the file structure of your site.</span></span> <span data-ttu-id="f5227-253">파일 관련 작업을 표시 하는 리본 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-253">The ribbon changes to show file-related tasks.</span></span>

![WebMatrix 작업 영역 파일](getting-started/_static/image13.png)

<span data-ttu-id="f5227-255">리본 메뉴에 아래의 화살표를 클릭 **새로 만들기** 을 클릭 한 다음 **새 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-255">In the ribbon, click the arrow under **New** and then click **New File**.</span></span>

![사용 하는 &quot;새로 만들기&quot; 새 파일을 만들려면 리본 메뉴에 명령](getting-started/_static/image14.png)

<span data-ttu-id="f5227-257">WebMatrix에는 파일 형식 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-257">WebMatrix displays a list of file types.</span></span> <span data-ttu-id="f5227-258">선택 **CSHTML**, 및는 **이름** 상자에 "HelloWorld"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-258">Select **CSHTML**, and in the **Name** box, type "HelloWorld".</span></span> <span data-ttu-id="f5227-259">CSHTML 페이지는 ASP.NET Web Pages 페이지가입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-259">A CSHTML page is an ASP.NET Web Pages page.</span></span>

![HelloWorld.cshtml 라는 새 CSHTML 페이지 만들기](getting-started/_static/image15.png)

<span data-ttu-id="f5227-261">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-261">Click **OK**.</span></span>

<span data-ttu-id="f5227-262">WebMatrix 페이지를 만들고 편집기에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-262">WebMatrix creates the page and opens it in the editor.</span></span>

![WebMatrix 편집기에서 새 HelloWorld 페이지](getting-started/_static/image16.png)

<span data-ttu-id="f5227-264">알 수 있듯이 대부분 일반 HTML 태그를 다음과 같이 맨 위에 있는 블록을 제외 하 고 페이지에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-264">As you can see, the page contains mostly ordinary HTML markup, except for a block at the top that looks like this:</span></span>

[!code-cshtml[Main](getting-started/samples/sample1.cshtml)]

<span data-ttu-id="f5227-265">잠시 후에 볼 수 있듯이 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-265">That's for adding code, as you'll see shortly.</span></span>

<span data-ttu-id="f5227-266">페이지의 다른 부분 &mdash; 요소 이름, 특성 및 텍스트와 맨 위에 있는 블록-서로 다른 색으로 모든 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-266">Notice that the different parts of the page &mdash; the element names, attributes, and text, plus the block at the top — are all in different colors.</span></span> <span data-ttu-id="f5227-267">이 이라고 *구문 강조 표시*, 쉽게 모든 항목의 선택을 취소 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-267">This is called *syntax highlighting*, and it makes it easier to keep everything clear.</span></span> <span data-ttu-id="f5227-268">쉽게 WebMatrix에서 웹 페이지를 사용 하 여 작업할 수 있도록 하는 기능 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-268">It's one of the features that makes it easy to work with web pages in WebMatrix.</span></span>

<span data-ttu-id="f5227-269">콘텐츠를 추가 합니다 `<head>` 및 `<body>` 다음 예와에서 같은 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-269">Add content for the `<head>` and `<body>` elements like in the following example.</span></span> <span data-ttu-id="f5227-270">(원한다 면 방금 다음 블록을 복사 하 수 전체 기존 페이지를 다음이 코드로 바꿉니다.)</span><span class="sxs-lookup"><span data-stu-id="f5227-270">(If you want, you can just copy the following block and replace the entire existing page with this code.)</span></span>

[!code-cshtml[Main](getting-started/samples/sample2.cshtml)]

<span data-ttu-id="f5227-271">빠른 실행 도구 모음 또는 합니다 **파일** 메뉴에서 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-271">In the Quick Access Toolbar or in the **File** menu, click **Save**.</span></span>

![WebMatrix 빠른 실행 도구 모음에서 저장 단추](getting-started/_static/image17.png)

## <a name="testing-the-page"></a><span data-ttu-id="f5227-273">페이지 테스트</span><span class="sxs-lookup"><span data-stu-id="f5227-273">Testing the Page</span></span>

<span data-ttu-id="f5227-274">에 **파일** 작업 영역에서 마우스 오른쪽 단추로 클릭 합니다 *HelloWorld.cshtml* 페이지를 클릭 한 다음 **브라우저에서 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-274">In the **Files** workspace, right-click the *HelloWorld.cshtml* page and then click **Launch in browser**.</span></span>

![WebMatrix 리본에서 [실행] 단추를 사용 하는 페이지를 실행 합니다.](getting-started/_static/image18.png)

<span data-ttu-id="f5227-276">WebMatrix는 컴퓨터에 페이지를 테스트 하는 데 사용할 수 있는 기본 제공 웹 서버 (IIS Express)를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-276">WebMatrix starts a built-in web server (IIS Express) that you can use to test pages on your computer.</span></span> <span data-ttu-id="f5227-277">(WebMatrix에서 IIS Express 없이 해야 페이지를 웹 서버에 게시 어딘가에 전에 테스트할 수 있습니다.) 페이지는 기본 브라우저에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-277">(Without IIS Express in WebMatrix, you'd have to publish your page to a web server somewhere before you could test it.) The page is displayed in your default browser.</span></span>

![&quot;Hello World&quot; 브라우저에서 실행 되 고 페이지](getting-started/_static/image19.png)

<span data-ttu-id="f5227-279">WebMatrix에서 페이지를 테스트 하는 경우 브라우저에서 URL는 비슷하게 `http://localhost:33651/HelloWorld.cshtml.` 이름을 *localhost* 페이지가 자신의 컴퓨터에 있는 웹 서버에서 반환 되는 즉, 로컬 서버를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-279">Notice that when you test a page in WebMatrix, the URL in the browser is something like `http://localhost:33651/HelloWorld.cshtml.` The name *localhost* refers to a local server, meaning that the page is served by a web server that's on your own computer.</span></span> <span data-ttu-id="f5227-280">언급 했 듯이 WebMatrix 라는 페이지를 시작 하는 경우 실행 되는 IIS Express 웹 서버 프로그램을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-280">As noted, WebMatrix includes a web server program named IIS Express that runs when you launch a page.</span></span>

<span data-ttu-id="f5227-281">다음의 숫자 *localhost* (예를 들어 *localhost:33651*) 참조를 *포트 번호* 컴퓨터에.</span><span class="sxs-lookup"><span data-stu-id="f5227-281">The number after *localhost* (for example, *localhost:33651*) refers to a *port number* on your computer.</span></span> <span data-ttu-id="f5227-282">이 특정 웹 사이트의 IIS Express를 사용 하는 "채널"입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-282">This is the number of the "channel" that IIS Express uses for this particular website.</span></span> <span data-ttu-id="f5227-283">포트 번호는 사이트를 만들고이 사용자가 만든 모든 사이트에 대 한 다른 1024 ~ 65536 범위에서 임의로 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-283">The port number is selected at random from the range 1024 through 65536 when you create your site, and it's different for every site that you create.</span></span> <span data-ttu-id="f5227-284">(고유한 사이트를 테스트 하는 경우 포트 번호를 반드시 있습니다 33561 보다 여러.) 각 웹 사이트에 다른 포트를 사용 하 여 IIS Express 유지할 수 직선와 통신 하는지 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-284">(When you test your own site, the port number will almost certainly be a different number than 33561.) By using a different port for each website, IIS Express can keep straight which of your sites it's talking to.</span></span>

<span data-ttu-id="f5227-285">사이트를 게시할 공용 웹 서버에 더 이상 표시 하는 경우 이후 *localhost* url에서입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-285">Later when you publish your site to a public web server, you no longer see *localhost* in the URL.</span></span> <span data-ttu-id="f5227-286">이 시점에서 볼 수와 같은 보다 일반적인 URL `http://myhostingsite/mywebsite/HelloWorld.cshtml` 무엇이 든 페이지 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-286">At that point, you'll see a more typical URL like `http://myhostingsite/mywebsite/HelloWorld.cshtml` or whatever the page is.</span></span> <span data-ttu-id="f5227-287">이 자습서 시리즈의 뒷부분에서 사이트를 게시 하는 방법에 대 한 더 알아봅니다 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-287">You'll learn more about publishing a site later in this tutorial series.</span></span>

## <a name="adding-some-server-side-code"></a><span data-ttu-id="f5227-288">일부 서버 쪽 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-288">Adding Some Server-Side Code</span></span>

<span data-ttu-id="f5227-289">브라우저를 닫고 WebMatrix에서 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-289">Close the browser and go back to the page in WebMatrix.</span></span>

<span data-ttu-id="f5227-290">다음 코드와 같이 표시 되도록 줄 코드 블록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-290">Add a line to the code block so that it looks like the following code:</span></span>

[!code-cshtml[Main](getting-started/samples/sample3.cshtml)]

<span data-ttu-id="f5227-291">약간 Razor 코드의 경우</span><span class="sxs-lookup"><span data-stu-id="f5227-291">This is a little bit of Razor code.</span></span> <span data-ttu-id="f5227-292">아마도 명확 현재 날짜 및 시간을 가져옵니다 해당 값을 배치 하는 *변수* 라는 `currentDateTime`합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-292">It's probably clear that it gets the current date and time and puts that value into a *variable* named `currentDateTime`.</span></span> <span data-ttu-id="f5227-293">자세한 내용을 확인할 수 있습니다 다음 자습서의 Razor 구문에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-293">You'll read more about Razor syntax in the next tutorial.</span></span>

<span data-ttu-id="f5227-294">페이지의 본문에 후는 `<p>Hello World!</p>` 요소에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-294">In the body of the page, after the `<p>Hello World!</p>` element, add the following:</span></span>

[!code-html[Main](getting-started/samples/sample4.html)]

<span data-ttu-id="f5227-295">이 코드에 배치 하는 값을 가져옵니다는 `currentDateTime` 맨 위에 있는 변수는 페이지의 태그에 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-295">This code gets the value that you put into the `currentDateTime` variable at the top and inserts it into the markup of the page.</span></span> <span data-ttu-id="f5227-296">`@` 문자 페이지에서 ASP.NET 웹 페이지 코드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-296">The `@` character marks the ASP.NET Web Pages code in the page.</span></span>

<span data-ttu-id="f5227-297">(WebMatrix 변경 내용을 저장 하면에 대 한 페이지를 실행 하기 전에)의 페이지를 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-297">Run the page again (WebMatrix saves the changes for you before it runs the page).</span></span> <span data-ttu-id="f5227-298">이 현재 날짜 및 시간 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-298">This time you see the date and time in the page.</span></span>

![&quot;Hello World&quot; 동적으로 생성 된 시간 표시를 사용 하 여 브라우저에서 실행 되는 페이지](getting-started/_static/image20.png)

<span data-ttu-id="f5227-300">몇 분 정도 기다린 다음 브라우저에서 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-300">Wait a few moments and then refresh the page in the browser.</span></span> <span data-ttu-id="f5227-301">날짜 및 시간 표시를 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-301">The date and time display is updated.</span></span>

<span data-ttu-id="f5227-302">브라우저에서 페이지 소스를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-302">In the browser, look at the page source.</span></span> <span data-ttu-id="f5227-303">다음 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-303">It looks like the following markup:</span></span>

[!code-html[Main](getting-started/samples/sample5.html)]

<span data-ttu-id="f5227-304">에 `@{ }` 맨 위에 있는 블록 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-304">Notice that the `@{ }` block at the top isn't there.</span></span> <span data-ttu-id="f5227-305">날짜 및 시간 표시는 실제 문자열을 확인할 수도 (`1/18/2012 2:49:50 PM` 또는)가 아니라 `@currentDateTime` 에서 제공 되었던 같은 합니다 *.cshtml* 페이지.</span><span class="sxs-lookup"><span data-stu-id="f5227-305">Also notice that the date and time display shows an actual string of characters (`1/18/2012 2:49:50 PM` or whatever), not `@currentDateTime` like you had in the *.cshtml* page.</span></span> <span data-ttu-id="f5227-306">같습니다. 페이지를 실행 하면 ASP.NET 처리 모든 코드 (거의이 경우)로 표시 된 내용 `@`합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-306">What happened here is that when you ran the page, ASP.NET processed all the code (very little in this case) that was marked with `@`.</span></span> <span data-ttu-id="f5227-307">코드 출력을 생성 하 고 출력을 페이지에 삽입 된 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-307">The code produces output, and that output was inserted into the page.</span></span>

## <a name="this-is-what-aspnet-web-pages-are-about"></a><span data-ttu-id="f5227-308">이 새로운 ASP.NET 웹 페이지에 대 한</span><span class="sxs-lookup"><span data-stu-id="f5227-308">This Is What ASP.NET Web Pages Are About</span></span>

<span data-ttu-id="f5227-309">ASP.NET 웹 페이지 동적 웹 콘텐츠를 생성 한다는 읽을 때 개념은 여기서 살펴본 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-309">When you read that ASP.NET Web Pages produces dynamic web content, what you've seen here is the idea.</span></span> <span data-ttu-id="f5227-310">방금 만든 페이지 전에 볼 수 있는 동일한 HTML 태그를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-310">The page you just created contains the same HTML markup that you've seen before.</span></span> <span data-ttu-id="f5227-311">모든 종류의 작업을 수행할 수 있는 코드를 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-311">It can also contain code that can perform all sorts of tasks.</span></span> <span data-ttu-id="f5227-312">이 예제에서는 현재 날짜 및 시간을 가져오는 간단한 작업을 수행한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-312">In this example, it did the trivial task of getting the current date and time.</span></span> <span data-ttu-id="f5227-313">살펴본 것 처럼 HTML 페이지에서 출력을 사용 하 여 코드 중간에 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-313">As you saw, you can intersperse code with the HTML to produce output in the page.</span></span> <span data-ttu-id="f5227-314">사용자가 요청 하는 경우는 *.cshtml* ASP.NET 브라우저에서 페이지의 웹 서버에에서 있는 동안 해당 페이지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-314">When someone requests a *.cshtml* page in the browser, ASP.NET processes the page while it's still in the hands of the web server.</span></span> <span data-ttu-id="f5227-315">ASP.NET 코드의 출력 (있는 경우) 페이지에 삽입 된 HTML로.</span><span class="sxs-lookup"><span data-stu-id="f5227-315">ASP.NET inserts the output of the code (if any) into the page as HTML.</span></span> <span data-ttu-id="f5227-316">코드를 처리 하는 완료 되 면 ASP.NET 결과 페이지를 브라우저에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-316">When the code processing is done, ASP.NET sends the resulting page to the browser.</span></span> <span data-ttu-id="f5227-317">브라우저가 적이 받는 HTML입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-317">All the browser ever gets is HTML.</span></span> <span data-ttu-id="f5227-318">다음 다이어그램은입니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-318">Here's a diagram:</span></span>

![생성 하는 방법을 ASP.NET HTML 동적으로의 개념적 흐름](getting-started/_static/image21.png)

<span data-ttu-id="f5227-320">개념은 간단 하지만 코드를 수행할 수 있는 여러 가지 흥미로운 작업 않으며 여러 가지 흥미로운 수 동적으로 추가할 수 있는 HTML 콘텐츠 페이지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-320">The idea is simple, but there are many interesting tasks that the code can perform, and there are many interesting ways in which you can dynamically add HTML content to the page.</span></span> <span data-ttu-id="f5227-321">및 ASP.NET *.cshtml* 모든 HTML 페이지와 같은 페이지를 브라우저 자체 (JavaScript 및 jQuery 코드)에서 실행 되는 코드를 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-321">And ASP.NET *.cshtml* pages, like any HTML page, can also include code that runs in the browser itself (JavaScript and jQuery code).</span></span> <span data-ttu-id="f5227-322">이 자습서 집합 및 이후의 조건은 이러한 작업을 모두 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-322">You'll explore all of these things in this tutorial set and in subsequent ones.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="f5227-323">다음에 나오는</span><span class="sxs-lookup"><span data-stu-id="f5227-323">Coming Up Next</span></span>

<span data-ttu-id="f5227-324">이 시리즈의 다음 자습서에서는 ASP.NET 웹 페이지 프로그래밍 좀 더 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-324">In the next tutorial in this series, you explore ASP.NET Web Pages programming a little more.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f5227-325">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f5227-325">Additional Resources</span></span>

<span data-ttu-id="f5227-326">[ASP.NET 웹 사이트를 처음부터 만들기](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-326">[Create an ASP.NET website from scratch](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch).</span></span> <span data-ttu-id="f5227-327">이것은 특히는 자습서 WebMatrix (없습니다: ASP.NET 웹 페이지)를 사용 하는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5227-327">This is a tutorial that's specifically about using WebMatrix (not ASP.NET Web Pages).</span></span> <span data-ttu-id="f5227-328">으로 이동 하기 잠시이 자습서 집합에서 다루지는 WebMatrix의 추가 기능 중 일부에 대 한 자세한 정보.</span><span class="sxs-lookup"><span data-stu-id="f5227-328">It goes into a little more detail about some of the additional features of WebMatrix that we won't cover in this tutorial set.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f5227-329">다음</span><span class="sxs-lookup"><span data-stu-id="f5227-329">Next</span></span>](intro-to-web-pages-programming.md)
