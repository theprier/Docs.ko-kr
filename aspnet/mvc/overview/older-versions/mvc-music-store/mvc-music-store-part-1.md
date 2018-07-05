---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
title: '1 부: 개요 및 파일-> 새 프로젝트 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 1 부에서는 개요 및 파일-> 새 프로젝트입니다.
ms.author: aspnetcontent
ms.date: 04/21/2011
ms.assetid: bd356ca3-5bdb-4067-9dac-c9e9923a86e8
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
msc.type: authoredcontent
ms.openlocfilehash: 57856a4a78a650e4abe872004e5be5f8f3b2dbcd
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37816345"
---
<a name="part-1-overview-and-file-new-project"></a><span data-ttu-id="f2e29-104">1 부: 개요 및 파일-> 새 프로젝트</span><span class="sxs-lookup"><span data-stu-id="f2e29-104">Part 1: Overview and File->New Project</span></span>
====================
<span data-ttu-id="f2e29-105">[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="f2e29-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="f2e29-106">MVC Music Store 자습서 응용 프로그램을 소개 하 고 웹 개발을 위한 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 설명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="f2e29-107">MVC Music Store는 온라인 음악 앨범을 판매 하 고 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="f2e29-108">이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="f2e29-109">1 부에서는 개요 및 파일 기반&gt;새 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-109">Part 1 covers Overview and File-&gt;New Project.</span></span>


## <a name="overview"></a><span data-ttu-id="f2e29-110">개요</span><span class="sxs-lookup"><span data-stu-id="f2e29-110">Overview</span></span>

<span data-ttu-id="f2e29-111">MVC Music Store 자습서 응용 프로그램을 소개 하 고 웹 개발을 위한 ASP.NET MVC 및 Visual Web Developer를 사용 하는 방법을 단계별로 설명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-111">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Web Developer for web development.</span></span> <span data-ttu-id="f2e29-112">에서는 느린 시작 됩니다, 그리고 수준 웹 초보 개발자 환경이 되므로 괜찮습니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-112">We'll be starting slowly, so beginner level web development experience is okay.</span></span>

<span data-ttu-id="f2e29-113">응용 프로그램에서는 작성 하는 간단한 음악 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-113">The application we'll be building is a simple music store.</span></span> <span data-ttu-id="f2e29-114">응용 프로그램에 세 가지 주요 부분이 있습니다: 쇼핑, 체크 아웃 및 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-114">There are three main parts to the application: shopping, checkout, and administration.</span></span>

![](mvc-music-store-part-1/_static/image1.jpg)

<span data-ttu-id="f2e29-115">방문자 장르별로 앨범을 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-115">Visitors can browse Albums by Genre:</span></span>

![](mvc-music-store-part-1/_static/image2.jpg)

<span data-ttu-id="f2e29-116">단일 앨범을 확인 하 고 자신의 카트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-116">They can view a single album and add it to their cart:</span></span>

![](mvc-music-store-part-1/_static/image3.jpg)

<span data-ttu-id="f2e29-117">더 이상 원하는 모든 항목을 제거 하면 해당 카트를 검토할 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="f2e29-117">They can review their cart, removing any items they no longer want:</span></span>

![](mvc-music-store-part-1/_static/image4.jpg)

<span data-ttu-id="f2e29-118">체크 아웃에 계속 로그인 또는 사용자 계정에 등록 하 라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-118">Proceeding to Checkout will prompt them to login or register for a user account.</span></span>

![](mvc-music-store-part-1/_static/image1.png)

![](mvc-music-store-part-1/_static/image2.png)

<span data-ttu-id="f2e29-119">계정을 만들면 전달 및 결제 정보를 기입 하 여 순서를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-119">After creating an account, they can complete the order by filling out shipping and payment information.</span></span> <span data-ttu-id="f2e29-120">간단히 설명 하기에 멋진 프로 모션 실행: 모든 프로 모션 코드 "무료"를 입력 하는 경우 무료 인!</span><span class="sxs-lookup"><span data-stu-id="f2e29-120">To keep things simple, we're running an amazing promotion: everything's free if they enter promotion code "FREE"!</span></span>

![](mvc-music-store-part-1/_static/image5.jpg)

<span data-ttu-id="f2e29-121">정렬 후 간단한 확인 화면이 표시는:</span><span class="sxs-lookup"><span data-stu-id="f2e29-121">After ordering, they see a simple confirmation screen:</span></span>

![](mvc-music-store-part-1/_static/image6.jpg)

<span data-ttu-id="f2e29-122">고객 faceing 페이지 외에도 앨범, 관리자 만들 수 있는 편집의 목록을 보여 주는 관리자 섹션을 빌드 및 앨범을 삭제도 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-122">In addition to customer-faceing pages, we'll also build an administrator section that shows a list of albums from which Administrators can Create, Edit, and Delete albums:</span></span>

![](mvc-music-store-part-1/_static/image7.jpg)

## <a name="1-file--gt-new-project"></a><span data-ttu-id="f2e29-123">1. 파일-&gt; 새 프로젝트</span><span class="sxs-lookup"><span data-stu-id="f2e29-123">1. File -&gt; New Project</span></span>

### <a name="installing-the-software"></a><span data-ttu-id="f2e29-124">소프트웨어 설치</span><span class="sxs-lookup"><span data-stu-id="f2e29-124">Installing the software</span></span>

<span data-ttu-id="f2e29-125">이 자습서는 무료 Visual Web Developer 2010 Express (무료 인)를 사용 하 여 새 ASP.NET MVC 3 프로젝트를 만들어 시작 하 고 전체 작동 중인 응용 프로그램을 만드는 기능이 증분 방식으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-125">This tutorial will begin by creating a new ASP.NET MVC 3 project using the free Visual Web Developer 2010 Express (which is free), and then we'll incrementally add features to create a complete functioning application.</span></span> <span data-ttu-id="f2e29-126">이 과정에서 다루게 데이터베이스 액세스, 폼 게시 시나리오, 데이터 유효성 검사 페이지 업데이트 및 유효성 검사, 사용자 로그인을 위한 AJAX를 사용 하 여 일관 된 페이지 레이아웃의 경우 마스터 페이지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-126">Along the way, we'll cover database access, form posting scenarios, data validation, using master pages for consistent page layout, using AJAX for page updates and validation, user login, and more.</span></span>

<span data-ttu-id="f2e29-127">단계별 지침을 따라 할 수 있습니다 또는에서 완성된 된 응용 프로그램을 다운로드할 수 있습니다 [MVC 음악 스토어](https://github.com/evilDave/MVC-Music-Store)합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-127">You can follow along step by step, or you can download the completed application from [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<span data-ttu-id="f2e29-128">응용 프로그램을 빌드하려면 Visual Studio 2010 SP1 또는 Visual Web Developer 2010 Express SP1 (Visual Studio 2010의 무료 버전)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-128">You can use either Visual Studio 2010 SP1 or Visual Web Developer 2010 Express SP1 (a free version of Visual Studio 2010) to build the application.</span></span> <span data-ttu-id="f2e29-129">사용는 SQL Server Compact (또한 무료) 데이터베이스를 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-129">We'll be using the SQL Server Compact (also free) to host the database.</span></span> <span data-ttu-id="f2e29-130">시작 하기 전에 아래에 나열 된 필수 구성 요소를 설치한 다음 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-130">Before you start, make sure you've installed the prerequisites listed below.</span></span>


- <span data-ttu-id="f2e29-131">[Visual Studio Web Developer Express SP1 필수 구성 요소]</span><span class="sxs-lookup"><span data-stu-id="f2e29-131">[Visual Studio Web Developer Express SP1 prerequisites]</span></span>
- <span data-ttu-id="f2e29-132">[ASP.NET MVC 3 도구 업데이트]</span><span class="sxs-lookup"><span data-stu-id="f2e29-132">[ASP.NET MVC 3 Tools Update]</span></span>
- <span data-ttu-id="f2e29-133">[SQL Server Compact 4.0]-런타임 및 도구 지원을 비롯 하 여</span><span class="sxs-lookup"><span data-stu-id="f2e29-133">[SQL Server Compact 4.0] - including both runtime and tools support</span></span>


### <a name="creating-a-new-aspnet-mvc-3-project"></a><span data-ttu-id="f2e29-134">새 ASP.NET MVC 3 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="f2e29-134">Creating a new ASP.NET MVC 3 project</span></span>

<span data-ttu-id="f2e29-135">Visual Web Developer에서 파일 메뉴에서 "새 프로젝트"를 선택 하 여 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-135">We'll start by selecting "New Project" from the File menu in Visual Web Developer.</span></span> <span data-ttu-id="f2e29-136">그러면 새 프로젝트 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="f2e29-136">This brings up the New Project dialog.</span></span>

![](mvc-music-store-part-1/_static/image5.png)

<span data-ttu-id="f2e29-137">Visual C#-선택&gt; 웹 템플릿 왼쪽에 그룹화 한 다음 가운데 열에서 "ASP.NET MVC 3 웹 응용 프로그램" 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-137">We'll select the Visual C# -&gt; Web Templates group on the left, then choose the "ASP.NET MVC 3 Web Application" template in the center column.</span></span> <span data-ttu-id="f2e29-138">프로젝트가 MvcMusicStore 이름과 확인 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-138">Name your project MvcMusicStore and press the OK button.</span></span>

![](mvc-music-store-part-1/_static/image8.jpg)

<span data-ttu-id="f2e29-139">이 프로젝트에 대 한 몇 가지 MVC 특정 설정을 확인 수 있게 하는 보조 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-139">This will display a secondary dialog which allows us to make some MVC specific settings for our project.</span></span> <span data-ttu-id="f2e29-140">다음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-140">Select the following:</span></span>

<span data-ttu-id="f2e29-141">프로젝트 템플릿을-빈 선택</span><span class="sxs-lookup"><span data-stu-id="f2e29-141">Project Template - select Empty</span></span>

<span data-ttu-id="f2e29-142">보기 엔진-Razor를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-142">View Engine - select Razor</span></span>

<span data-ttu-id="f2e29-143">사용 하 여 HTML5 의미 체계 태그-확인</span><span class="sxs-lookup"><span data-stu-id="f2e29-143">Use HTML5 semantic markup - checked</span></span>

<span data-ttu-id="f2e29-144">있는지 확인 설정을 아래와 같이 한 다음 확인 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-144">Verify that your settings are as shown below, then press the OK button.</span></span>

![](mvc-music-store-part-1/_static/image9.jpg)

<span data-ttu-id="f2e29-145">이 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-145">This will create our project.</span></span> <span data-ttu-id="f2e29-146">오른쪽에 있는 솔루션 탐색기에서 응용 프로그램에 추가 된 폴더에 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-146">Let's take a look at the folders that have been added to our application in the Solution Explorer on the right side.</span></span>

![](mvc-music-store-part-1/_static/image10.jpg)

<span data-ttu-id="f2e29-147">빈 MVC 3 템플릿은 완전히 비어 있지 – 기본 폴더 구조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-147">The Empty MVC 3 template isn't completely empty – it adds a basic folder structure:</span></span>

![](mvc-music-store-part-1/_static/image6.png)

<span data-ttu-id="f2e29-148">ASP.NET MVC는 폴더 이름에 대 한 일부 기본 명명 규칙을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-148">ASP.NET MVC makes use of some basic naming conventions for folder names:</span></span>

| <span data-ttu-id="f2e29-149">**폴더**</span><span class="sxs-lookup"><span data-stu-id="f2e29-149">**Folder**</span></span> | <span data-ttu-id="f2e29-150">**용도**</span><span class="sxs-lookup"><span data-stu-id="f2e29-150">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="f2e29-151">**/Controllers**</span><span class="sxs-lookup"><span data-stu-id="f2e29-151">**/Controllers**</span></span> | <span data-ttu-id="f2e29-152">컨트롤러 응답을 브라우저에서 입력을 수행 하 고 사용자에 게 응답 반환을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-152">Controllers respond to input from the browser, decide what to do with it, and return response to the user.</span></span> |
| <span data-ttu-id="f2e29-153">**/ 뷰**</span><span class="sxs-lookup"><span data-stu-id="f2e29-153">**/Views**</span></span> | <span data-ttu-id="f2e29-154">뷰는 UI 템플릿 저장</span><span class="sxs-lookup"><span data-stu-id="f2e29-154">Views hold our UI templates</span></span> |
| <span data-ttu-id="f2e29-155">**/Models**</span><span class="sxs-lookup"><span data-stu-id="f2e29-155">**/Models**</span></span> | <span data-ttu-id="f2e29-156">모델 보유 하 고 데이터를 조작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-156">Models hold and manipulate data</span></span> |
| <span data-ttu-id="f2e29-157">**/Content**</span><span class="sxs-lookup"><span data-stu-id="f2e29-157">**/Content**</span></span> | <span data-ttu-id="f2e29-158">이 폴더는 이미지, CSS 및 다른 정적 콘텐츠를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-158">This folder holds our images, CSS, and any other static content</span></span> |
| <span data-ttu-id="f2e29-159">**/Scripts**</span><span class="sxs-lookup"><span data-stu-id="f2e29-159">**/Scripts**</span></span> | <span data-ttu-id="f2e29-160">이 폴더는 JavaScript 파일 저장</span><span class="sxs-lookup"><span data-stu-id="f2e29-160">This folder holds our JavaScript files</span></span> |

<span data-ttu-id="f2e29-161">이러한 폴더는 기본적으로 ASP.NET MVC 프레임 워크 "구성 보다 규칙" 방식을 사용 하 고 기본 가정을 폴더 명명 규칙을 기반으로 하기 때문에 빈 ASP.NET MVC 응용 프로그램에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-161">These folders are included even in an Empty ASP.NET MVC application because the ASP.NET MVC framework by default uses a "convention over configuration" approach and makes some default assumptions based on folder naming conventions.</span></span> <span data-ttu-id="f2e29-162">예를 들어 컨트롤러 뷰를 찾습니다 Views 폴더에 기본적으로이 코드에 명시적으로 지정 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-162">For instance, controllers look for views in the Views folder by default without you having to explicitly specify this in your code.</span></span> <span data-ttu-id="f2e29-163">를 작성 하는 데 필요한 코드의 양이 줄어듭니다 기본 규칙 사용 수도 쉽게 다른 개발자가 프로젝트를 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-163">Sticking with the default conventions reduces the amount of code you need to write, and can also make it easier for other developers to understand your project.</span></span> <span data-ttu-id="f2e29-164">이러한 규칙을 응용 프로그램 구축 하는 대로 자세한 설명할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f2e29-164">We'll explain these conventions more as we build our application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f2e29-165">다음</span><span class="sxs-lookup"><span data-stu-id="f2e29-165">Next</span></span>](mvc-music-store-part-2.md)
