---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
title: '1 부: 파일-> 새 프로젝트 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 1 부에서는 개요 및 파일/새 프로젝트를 다룹니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/21/2010
ms.topic: article
ms.assetid: 15d4652b-d5aa-4172-b186-2c7f96ba316d
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
msc.type: authoredcontent
ms.openlocfilehash: 8c346e88277b6cf43676f7c6b58f9679a591d634
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37388213"
---
<a name="part-1-file--new-project"></a><span data-ttu-id="3e1cd-104">1 부: 파일-> 새 프로젝트</span><span class="sxs-lookup"><span data-stu-id="3e1cd-104">Part 1: File-> New Project</span></span>
====================
<span data-ttu-id="3e1cd-105">[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="3e1cd-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="3e1cd-106">Tailspin Spyworks.NET 플랫폼에 대 한 강력 하 고 확장 가능한 응용 프로그램을 생성 하는 방법을 매우 단순 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="3e1cd-107">해제 쇼핑, 체크 아웃 및 관리를 포함 하는 온라인 상점을 만들려고 ASP.NET 4에서 강력한 새 기능을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="3e1cd-108">이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="3e1cd-109">1 부에서는 개요 및 파일/새 프로젝트를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-109">Part 1 covers Overview and File/New Project.</span></span>


## <a id="_Toc260221666"></a>  <span data-ttu-id="3e1cd-110">개요</span><span class="sxs-lookup"><span data-stu-id="3e1cd-110">Overview</span></span>

<span data-ttu-id="3e1cd-111">이 자습서는 ASP.NET WebForms를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-111">This tutorial is an introduction to ASP.NET WebForms.</span></span> <span data-ttu-id="3e1cd-112">에서는 느린 시작 됩니다, 그리고 수준 웹 초보 개발자 환경이 되므로 괜찮습니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-112">We'll be starting slowly, so beginner level web development experience is okay.</span></span>

<span data-ttu-id="3e1cd-113">응용 프로그램에서는 작성 하는 간단한 온라인 스토어 경우</span><span class="sxs-lookup"><span data-stu-id="3e1cd-113">The application we'll be building is a simple on-line store.</span></span>

![](tailspin-spyworks-part-1/_static/image1.jpg)


<span data-ttu-id="3e1cd-114">방문자는 범주별으로 제품을 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-114">Visitors can browse Products by Category:</span></span>

![](tailspin-spyworks-part-1/_static/image2.jpg)

<span data-ttu-id="3e1cd-115">단일 제품을 확인 하 고 자신의 카트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-115">They can view a single product and add it to their cart:</span></span>

![](tailspin-spyworks-part-1/_static/image3.jpg)

<span data-ttu-id="3e1cd-116">더 이상 원하는 모든 항목을 제거 하면 해당 카트를 검토할 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="3e1cd-116">They can review their cart, removing any items they no longer want:</span></span>

![](tailspin-spyworks-part-1/_static/image4.jpg)

<span data-ttu-id="3e1cd-117">체크 아웃을 계속 묻는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-117">Proceeding to Checkout will prompt them to</span></span>

![](tailspin-spyworks-part-1/_static/image5.jpg)

![](tailspin-spyworks-part-1/_static/image6.jpg)

<span data-ttu-id="3e1cd-118">정렬 후 간단한 확인 화면이 표시는:</span><span class="sxs-lookup"><span data-stu-id="3e1cd-118">After ordering, they see a simple confirmation screen:</span></span>

![](tailspin-spyworks-part-1/_static/image7.jpg)


<span data-ttu-id="3e1cd-119">Visual Studio 2010에서는 새 ASP.NET WebForms 프로젝트를 만들어 먼저 및 전체 작동 중인 응용 프로그램을 만드는 기능이 증분 방식으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-119">We'll begin by creating a new ASP.NET WebForms project in Visual Studio 2010, and we'll incrementally add features to create a complete functioning application.</span></span> <span data-ttu-id="3e1cd-120">이 과정에서 다루게 데이터베이스 액세스, 목록 및 그리드 보기, 페이지를 업데이트 하는 데이터, 데이터 유효성 검사, 마스터 페이지를 사용 하 여 일관 된 페이지 레이아웃, AJAX, 유효성 검사, 사용자 멤버 자격 등입니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-120">Along the way, we'll cover database access, list and grid views, data update pages, data validation, using master pages for consistent page layout, AJAX, validation, user membership, and more.</span></span>

<span data-ttu-id="3e1cd-121">단계별 지침을 따라 할 수 있습니다. 또는에서 완성된 된 응용 프로그램을 다운로드할 수 있습니다. [http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="3e1cd-121">You can follow along step by step, or you can download the completed application from [http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/)</span></span>

<span data-ttu-id="3e1cd-122">Visual Studio 2010 또는 무료 Visual Web Developer 2010에서 사용할 수 있습니다 [ https://www.microsoft.com/express/Web/ ](https://www.microsoft.com/express/Web/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-122">You can use either Visual Studio 2010 or the free Visual Web Developer 2010 from [https://www.microsoft.com/express/Web/](https://www.microsoft.com/express/Web/).</span></span> <span data-ttu-id="3e1cd-123">응용 프로그램을 빌드하려면 SQL Server 또는 무료 SQL Server Express 데이터베이스를 호스팅하는를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-123">To build the application, you can use either SQL Server or the free SQL Server Express to host the database.</span></span>

## <a id="_Toc260221667"></a>  <span data-ttu-id="3e1cd-124">파일 / 새로 만들기 프로젝트</span><span class="sxs-lookup"><span data-stu-id="3e1cd-124">File / New Project</span></span>

<span data-ttu-id="3e1cd-125">Visual Studio에서 파일 메뉴에서 새 프로젝트를 선택 하 여 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-125">We'll start by selecting the New Project from the File menu in Visual Studio.</span></span> <span data-ttu-id="3e1cd-126">그러면 새 프로젝트 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-126">This brings up the New Project dialog.</span></span>

![](tailspin-spyworks-part-1/_static/image8.jpg)

<span data-ttu-id="3e1cd-127">Visual C# 선택 웹 템플릿 왼쪽에 그룹화 하 고 가운데 열에서 "ASP.NET 웹 응용 프로그램" 템플릿을 선택한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-127">We'll select the Visual C# / Web Templates group on the left, and then choose the "ASP.NET Web Application" template in the center column.</span></span> <span data-ttu-id="3e1cd-128">프로젝트가 TailspinSpyworks 이름과 확인 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-128">Name your project TailspinSpyworks and press the OK button.</span></span>

![](tailspin-spyworks-part-1/_static/image9.jpg)

<span data-ttu-id="3e1cd-129">이 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-129">This will create our project.</span></span> <span data-ttu-id="3e1cd-130">오른쪽에 있는 솔루션 탐색기에서 응용 프로그램에 포함 된 폴더에 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-130">Let's take a look at the folders that are included in our application in the Solution Explorer on the right side.</span></span>

![](tailspin-spyworks-part-1/_static/image10.jpg)

<span data-ttu-id="3e1cd-131">빈 솔루션을 완전히 비어 있지 않은 – 기본 폴더 구조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-131">The Empty Solution isn't completely empty – it adds a basic folder structure:</span></span>

![](tailspin-spyworks-part-1/_static/image1.png)

<span data-ttu-id="3e1cd-132">ASP.NET 4 기본 프로젝트 템플릿에 의해 구현 된 규칙을 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-132">Note the conventions implemented by the ASP.NET 4 default project template.</span></span>

- <span data-ttu-id="3e1cd-133">"Account" 폴더는 ASP에 대 한 기본 사용자 인터페이스를 구현합니다. NET의 멤버 자격 하위 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-133">The "Account" folder implements a basic user interface for ASP.NET's membership subsystem.</span></span>
- <span data-ttu-id="3e1cd-134">클라이언트 쪽 JavaScript 파일에 대 한 리포지토리로 사용 되는 "Scripts" 폴더 및 핵심 jQuery.js 파일이 기본적으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-134">The "Scripts" folder serves as the repository for client side JavaScript files and the core jQuery .js files are made available by default.</span></span>
- <span data-ttu-id="3e1cd-135">"스타일" 폴더는 웹 사이트 시각적 개체 (CSS 스타일 시트)를 구성 하는 데</span><span class="sxs-lookup"><span data-stu-id="3e1cd-135">The "Styles" folder is used to organize our web site visuals (CSS Style Sheets)</span></span>

<span data-ttu-id="3e1cd-136">에서는 F5 키를 눌러 응용 프로그램을 실행 하 고 default.aspx 페이지를 렌더링 하는 경우 다음을 참조 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-136">When we press F5 to run our application and render the default.aspx page we see the following.</span></span>

![](tailspin-spyworks-part-1/_static/image11.jpg)

<span data-ttu-id="3e1cd-137">Tailspin Spyworks 응용 프로그램에 대 한 할까요 visual asthetics 렌더링할 연결 된 이미지 파일과 CSS 클래스를 사용 하 여 기본 WebForms 템플릿에서 Style.css 파일을 바꾸려면이 첫 번째 응용 프로그램 향상이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-137">Our first application enhancement will be to replace the Style.css file from the default WebForms template with the CSS classes and associated image files that will render the visual asthetics that we want for our Tailspin Spyworks application.</span></span>

<span data-ttu-id="3e1cd-138">이렇게 한 후 default.aspx 페이지는 다음과 같이 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-138">After doing so our default.aspx page renders like this.</span></span>

![](tailspin-spyworks-part-1/_static/image12.jpg)

<span data-ttu-id="3e1cd-139">맨 위에 있는 이미지 링크 확인 페이지 및 마스터 페이지에 추가 된 메뉴 항목의 오른쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-139">Notice the image links at the top right of the page and the menu items that have been added to the master page.</span></span> <span data-ttu-id="3e1cd-140">"로그인" 및 "Account" 링크 (기본 템플릿에 의해 생성 됨)으로 존재 하는 페이지 및 응용 프로그램 구축으로 구현 하는 페이지의 나머지 부분을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-140">Only the "Sign In" and "Account" links point to pages that exist (generated by the default template) and the rest of the pages we will implement as we build our application.</span></span>

<span data-ttu-id="3e1cd-141">마스터 페이지 스타일 디렉터리에 재배치 하려고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-141">We're also going to relocate the Master Page to the Styles directory.</span></span> <span data-ttu-id="3e1cd-142">이 옵션은 기본 설정에만 사항이 작업을 좀 더 쉽게 응용 프로그램을 나중에 "skinable" 하도록 결정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-142">Though this is only a preference it may make things a little easier if we decide to make our application "skinable" in the future.</span></span>

<span data-ttu-id="3e1cd-143">마스터 페이지를 변경 해야이 작업을 수행한 후 모든.aspx 파일에 대 한 참조에서 생성 된 기본 ASP.NET WebForms 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="3e1cd-143">After doing this we'll need to change the master page references in all the .aspx files generated by the default ASP.NET WebForms pages.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="3e1cd-144">다음</span><span class="sxs-lookup"><span data-stu-id="3e1cd-144">Next</span></span>](tailspin-spyworks-part-2.md)
