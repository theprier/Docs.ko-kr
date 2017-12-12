---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: "업그레이드 되었으며 수정 자습서 소개 | Microsoft Docs"
author: shanselman
description: "새로운 프레임 워크를 파악 하는 가장 좋은 방법은 다른 구성 요소로 작성 하는 것입니다. 이 자습서는 ASP.NE를 사용 하 여 완료 하지만 크기가 작은 응용 프로그램을 빌드하는 방법을 안내 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: 57eedb224e26867c78cc399b89f91b95f722074d
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="introducing-the-nerddinner-tutorial"></a><span data-ttu-id="f928f-104">업그레이드 되었으며 수정 자습서 소개</span><span class="sxs-lookup"><span data-stu-id="f928f-104">Introducing the NerdDinner Tutorial</span></span>
====================
<span data-ttu-id="f928f-105">으로 [Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="f928f-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

[<span data-ttu-id="f928f-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="f928f-106">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="f928f-107">새로운 프레임 워크를 파악 하는 가장 좋은 방법은 다른 구성 요소로 작성 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f928f-107">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="f928f-108">이 자습서는 작고 빌드만 ASP.NET MVC 1을 사용 하 여 응용 프로그램을 완료 하는 방법을 안내 하 고 필요한 핵심 개념 중 일부를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="f928f-108">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC 1, and introduces some of the core concepts behind it.</span></span>
> 
> <span data-ttu-id="f928f-109">ASP.NET MVC 3을 사용 하는 경우 수행한 것이 좋습니다는 [가져오기 시작 MVC 3과](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="f928f-109">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-tutorial"></a><span data-ttu-id="f928f-110">업그레이드 되었으며 수정 자습서</span><span class="sxs-lookup"><span data-stu-id="f928f-110">NerdDinner Tutorial</span></span>

<span data-ttu-id="f928f-111">새로운 프레임 워크를 파악 하는 가장 좋은 방법은 다른 구성 요소로 작성 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f928f-111">The best way to learn a new framework is to build something with it.</span></span> <span data-ttu-id="f928f-112">이 자습서는 작고 빌드만 ASP.NET MVC를 사용 하 여 응용 프로그램을 완료 하는 방법을 안내 하 고 필요한 핵심 개념 중 일부를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="f928f-112">This tutorial walks through how to build a small, but complete, application using ASP.NET MVC, and introduces some of the core concepts behind it.</span></span>

<span data-ttu-id="f928f-113">빌드 하려는 응용 프로그램 "업그레이드 되었으며 수정" 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f928f-113">The application we are going to build is called "NerdDinner".</span></span> <span data-ttu-id="f928f-114">업그레이드 되었으며 수정 찾고 dinners 온라인을 구성 하는 사용자는 쉬운 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f928f-114">NerdDinner provides an easy way for people to find and organize dinners online:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image1.png)

<span data-ttu-id="f928f-115">업그레이드 되었으며 수정에는 등록 된 사용자를 만들고 편집 하 고 dinners 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f928f-115">NerdDinner enables registered users to create, edit and delete dinners.</span></span> <span data-ttu-id="f928f-116">응용 프로그램 간에 일관 된 유효성 검사 및 비즈니스 규칙 집합이 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="f928f-116">It enforces a consistent set of validation and business rules across the application:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image2.png)

<span data-ttu-id="f928f-117">방문자는 AJAX 기반 지도 사용 하 여 향후 dinners 근처 보유 하 고 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f928f-117">Visitors can use an AJAX-based map to search for upcoming dinners being held near them:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image3.png)

<span data-ttu-id="f928f-118">클릭 하면는 dinner 됩니다으로 이동 세부 정보 페이지에 알아볼 수 있는 더 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="f928f-118">Clicking a dinner will take them to a details page where they can learn more about it:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image4.png)

<span data-ttu-id="f928f-119">사이트에 등록 하거나 로그인 하려면 dinner 참석 하려고 경우:</span><span class="sxs-lookup"><span data-stu-id="f928f-119">If they are interested in attending the dinner they can login or register on the site:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image5.png)

<span data-ttu-id="f928f-120">이벤트 참석자는 AJAX 기반 RSVP 링크를 클릭 한 다음 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="f928f-120">They can then click an AJAX-based RSVP link to attend the event:</span></span>

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a><span data-ttu-id="f928f-121">업그레이드 되었으며 수정 구현</span><span class="sxs-lookup"><span data-stu-id="f928f-121">Implementing NerdDinner</span></span>

<span data-ttu-id="f928f-122">파일-를 사용 하 여 업그레이드 되었으며 수정 응용 프로그램을 시작 하겠습니다&gt;새로운 ASP.NET MVC 프로젝트를 만들려면 Visual Studio 내에서 새 프로젝트 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="f928f-122">We are going to begin our NerdDinner application by using the File-&gt;New Project command within Visual Studio to create a brand new ASP.NET MVC project.</span></span> <span data-ttu-id="f928f-123">그런 다음 증분 기능 및 추가 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f928f-123">We will then incrementally add functionality and features.</span></span> <span data-ttu-id="f928f-124">방식에 따라 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f928f-124">Along the way we'll cover:</span></span>

1. [<span data-ttu-id="f928f-125">새 ASP.NET MVC 프로젝트를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="f928f-125">How to create a new ASP.NET MVC Project</span></span>](# "새 ASP.NET MVC 프로젝트 만들기")
2. [<span data-ttu-id="f928f-126">데이터베이스를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="f928f-126">How to create a database</span></span>](# "데이터베이스 만들기")
3. [<span data-ttu-id="f928f-127">비즈니스 규칙 유효성 검사를 사용 하 여 모델을 작성 하는 방법</span><span class="sxs-lookup"><span data-stu-id="f928f-127">How to build a model with business rule validations</span></span>](# "비즈니스 규칙 유효성 검사를 사용 하 여 모델 빌드")
4. [<span data-ttu-id="f928f-128">등록/정보 UI를 구현 하려면 컨트롤러와 뷰를 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="f928f-128">How to use controllers and views to implement a listing/details UI</span></span>](# "사용 하 여 컨트롤러와 뷰 목록/세부 정보 UI를 구현 하려면")
5. <span data-ttu-id="f928f-129">[CRUD 제공 하는 방법 (만들기, 읽기, 업데이트, 삭제) 데이터 항목 지원 형성](# "제공 CRUD (만들기, 읽기, 업데이트, 삭제) 데이터 형식 항목 지원")</span><span class="sxs-lookup"><span data-stu-id="f928f-129">[How to provide CRUD (create, read, update, delete) data form entry support](# "Provide CRUD (Create, Read, Update, Delete) Data Form Entry Support")</span></span>
6. [<span data-ttu-id="f928f-130">ViewData를 사용 하 고 ViewModel 클래스를 구현 하는 방법</span><span class="sxs-lookup"><span data-stu-id="f928f-130">How to use ViewData and implement ViewModel classes</span></span>](# "ViewData 사용 및 ViewModel 클래스 구현")
7. [<span data-ttu-id="f928f-131">마스터 페이지 및 부분을 사용 하 여 UI를 다시 사용 하는 방법을</span><span class="sxs-lookup"><span data-stu-id="f928f-131">How to re-use UI using master pages and partials</span></span>](# "마스터 페이지를 사용 하 여 UI 다시 사용 및 부분")
8. [<span data-ttu-id="f928f-132">효율적인 데이터 페이징을 구현 하는 방법을</span><span class="sxs-lookup"><span data-stu-id="f928f-132">How to implement efficient data paging</span></span>](# "구현 효율적인 데이터 페이징")
9. [<span data-ttu-id="f928f-133">인증 및 권한 부여를 사용 하 여 응용 프로그램을 보호 하는 방법</span><span class="sxs-lookup"><span data-stu-id="f928f-133">How to secure applications using authentication and authorization</span></span>](# "보안 응용 프로그램 사용 하 여 인증 및 권한 부여")
10. [<span data-ttu-id="f928f-134">AJAX를 사용 하 여 동적 업데이트를 제공 하는 방법</span><span class="sxs-lookup"><span data-stu-id="f928f-134">How to use AJAX to deliver dynamic updates</span></span>](# "동적 업데이트 제공을 사용 하 여 AJAX")
11. [<span data-ttu-id="f928f-135">AJAX를 사용 하 여 매핑 시나리오를 구현 하는 방법</span><span class="sxs-lookup"><span data-stu-id="f928f-135">How to use AJAX to implement mapping scenarios</span></span>](# "구현 매핑 시나리오를 사용 하 여 AJAX")
12. [<span data-ttu-id="f928f-136">자동화 된 단위 테스트를 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="f928f-136">How to enable automated unit testing</span></span>](# "자동화 된 단위 테스트 설정")

<span data-ttu-id="f928f-137">업그레이드 되었으며 수정의 고유 사본을 만들 수 있습니다 각를 완료 하 여 처음부터 단계에서는이 장에서 연습입니다.</span><span class="sxs-lookup"><span data-stu-id="f928f-137">You can build your own copy of NerdDinner from scratch by completing each step we walkthrough in this chapter.</span></span> <span data-ttu-id="f928f-138">여기에 소스 코드의 전체 버전을 다운로드할 수 또는: [GitHub에서 업그레이드 되었으며 수정](https://github.com/AspNetMVPSamples/NerdDinner)합니다.</span><span class="sxs-lookup"><span data-stu-id="f928f-138">Alternatively, you can download a completed version of the source code here: [NerdDinner on GitHub](https://github.com/AspNetMVPSamples/NerdDinner).</span></span> <span data-ttu-id="f928f-139">또한 필요에 따라 수도 있습니다 [이 자습서의 무료 PDF 버전을 다운로드할](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) 자습서를 오프 라인으로 보려는 경우.</span><span class="sxs-lookup"><span data-stu-id="f928f-139">You can also optionally also [download a free PDF version of this tutorial](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) if you want to read the tutorial offline.</span></span>

<span data-ttu-id="f928f-140">응용 프로그램을 빌드하려면 Visual Studio 2008 또는 무료 Visual Web Developer 2008 Express를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f928f-140">You can use either Visual Studio 2008 or the free Visual Web Developer 2008 Express to build the application.</span></span> <span data-ttu-id="f928f-141">데이터베이스에 대 한 SQL Server 또는 무료 SQL Server Express를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f928f-141">You can use either SQL Server or the free SQL Server Express for the database.</span></span>

<span data-ttu-id="f928f-142">ASP.NET MVC, Visual Web Developer 2008 Express 및 SQL Server Express (모든 사용 가능)의 v 2를 사용 하 여 설치할 수는 [Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)</span><span class="sxs-lookup"><span data-stu-id="f928f-142">You can install ASP.NET MVC, Visual Web Developer 2008 Express, and SQL Server Express (all free) using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)</span></span>

### <a name="now-lets-get-started"></a><span data-ttu-id="f928f-143">이제 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f928f-143">Now let's get started....</span></span>

<span data-ttu-id="f928f-144">이제 업그레이드 되었으며 수정 란 설명한 보겠습니다 우리의 진행할 롤업을 일부 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f928f-144">Now that we've covered what NerdDinner is, let's roll up our sleeves and write some code.</span></span>

<span data-ttu-id="f928f-145">파일-를 사용 하 여 먼저&gt;업그레이드 되었으며 수정 응용 프로그램을 만들려면 Visual Studio 내에서 새 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="f928f-145">We'll begin by using File-&gt;New Project within Visual Studio to create the NerdDinner application.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="f928f-146">다음</span><span class="sxs-lookup"><span data-stu-id="f928f-146">Next</span></span>](create-a-new-aspnet-mvc-project.md)
