---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
title: ASP.NET 4.7 Web Forms 및 Visual Studio 2017 시작 | Microsoft Docs
author: Erikre
description: 이 단계별 자습서 시리즈는 ASP.NET 4.7 및 Microsoft Visual Studio를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항 설명
ms.author: riande
ms.date: 01/09/2019
ms.assetid: 9b96eaa1-8ef0-4338-a2e8-e0f970bfaf68
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
msc.type: authoredcontent
ms.openlocfilehash: fb41ce72e9454d8d670a0b95234d2bc3f909f0ee
ms.sourcegitcommit: 42a8164b8aba21f322ffefacb92301bdfb4d3c2d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54341555"
---
<a name="getting-started-with-aspnet-45-web-forms-and-visual-studio-2017"></a><span data-ttu-id="e2d9a-103">ASP.NET 4.5 Web Forms 및 Visual Studio 2017을 사용 하 여 시작</span><span class="sxs-lookup"><span data-stu-id="e2d9a-103">Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2017</span></span>
====================

<span data-ttu-id="e2d9a-104">[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF) 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="e2d9a-104">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

<span data-ttu-id="e2d9a-105">이 자습서 시리즈에서는 ASP.NET 4.5와 Microsoft Visual Studio 2017을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-105">This tutorial series shows you how to build an ASP.NET Web Forms application with ASP.NET 4.5 and Microsoft Visual Studio 2017.</span></span> 

## <a name="introduction"></a><span data-ttu-id="e2d9a-106">소개</span><span class="sxs-lookup"><span data-stu-id="e2d9a-106">Introduction</span></span>

<span data-ttu-id="e2d9a-107">이 자습서 시리즈 ASP.NET 4.5와 Visual Studio 2017을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-107">This tutorial series guides you through creating an ASP.NET Web Forms application using Visual Studio 2017 and ASP.NET 4.5.</span></span> <span data-ttu-id="e2d9a-108">명명 된 응용 프로그램을 만든 **Wingtip Toys** -간소화 된 storefront 웹 사이트를 온라인으로 항목을 판매 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-108">You'll create an application named **Wingtip Toys** - a simplified storefront web site selling items online.</span></span> <span data-ttu-id="e2d9a-109">시리즈 중 ASP.NET 4.5의 새로운 기능에 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-109">During the series, new ASP.NET 4.5 features are highlighted.</span></span>

### <a name="target-audience"></a><span data-ttu-id="e2d9a-110">대상 사용자</span><span class="sxs-lookup"><span data-stu-id="e2d9a-110">Target audience</span></span>

<span data-ttu-id="e2d9a-111">새 ASP.NET Web forms 개발자는이 자습서 시리즈에 대 한 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-111">Developers new to ASP.NET Web Forms are the target audience for this tutorial series.</span></span>

<span data-ttu-id="e2d9a-112">다음 영역에서 약간의 지식이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-112">You should have some knowledge in the following areas:</span></span>

- <span data-ttu-id="e2d9a-113">개체 지향 프로그래밍 (OOP) 및 언어</span><span class="sxs-lookup"><span data-stu-id="e2d9a-113">Object-oriented programming (OOP) and languages</span></span>
- <span data-ttu-id="e2d9a-114">웹 개발 (HTML, CSS, JavaScript)</span><span class="sxs-lookup"><span data-stu-id="e2d9a-114">Web development (HTML, CSS, JavaScript)</span></span>
- <span data-ttu-id="e2d9a-115">관계형 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="e2d9a-115">Relational databases</span></span>
- <span data-ttu-id="e2d9a-116">N 계층 아키텍처</span><span class="sxs-lookup"><span data-stu-id="e2d9a-116">N-tier architecture</span></span>

<span data-ttu-id="e2d9a-117">다양 한이 분야를 검토 하려면 다음 콘텐츠를 연구 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-117">To review these areas, consider studying the following content:</span></span>

- [<span data-ttu-id="e2d9a-118">Visual C# 시작</span><span class="sxs-lookup"><span data-stu-id="e2d9a-118">Getting Started with Visual C#</span></span>](https://msdn.microsoft.com/library/a72418yk.aspx)
- <span data-ttu-id="e2d9a-119">[Web Development](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, PHP, JQuery](http://w3schools.com/)</span><span class="sxs-lookup"><span data-stu-id="e2d9a-119">[Web Development](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, PHP, JQuery](http://w3schools.com/)</span></span>
- [<span data-ttu-id="e2d9a-120">관계형 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="e2d9a-120">Relational database</span></span>](http://en.wikipedia.org/wiki/Relational_database)
- [<span data-ttu-id="e2d9a-121">다중 계층 아키텍처</span><span class="sxs-lookup"><span data-stu-id="e2d9a-121">Multitier architecture</span></span>](http://en.wikipedia.org/wiki/Multitier_architecture)

### <a name="application-features"></a><span data-ttu-id="e2d9a-122">응용 프로그램 기능</span><span class="sxs-lookup"><span data-stu-id="e2d9a-122">Application features</span></span>

<span data-ttu-id="e2d9a-123">이 시리즈에 제공 된 ASP.NET Web Form 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-123">The ASP.NET Web Form features presented in this series include:</span></span>

- <span data-ttu-id="e2d9a-124">웹 응용 프로그램 프로젝트 (웹 사이트 프로젝트가 아닌)</span><span class="sxs-lookup"><span data-stu-id="e2d9a-124">The Web Application Project (not Web Site Project)</span></span>
- <span data-ttu-id="e2d9a-125">Web Forms</span><span class="sxs-lookup"><span data-stu-id="e2d9a-125">Web Forms</span></span>
- <span data-ttu-id="e2d9a-126">마스터 페이지, 구성</span><span class="sxs-lookup"><span data-stu-id="e2d9a-126">Master Pages, Configuration</span></span>
- <span data-ttu-id="e2d9a-127">부트스트랩</span><span class="sxs-lookup"><span data-stu-id="e2d9a-127">Bootstrap</span></span>
- <span data-ttu-id="e2d9a-128">Entity Framework 코드 먼저 LocalDB</span><span class="sxs-lookup"><span data-stu-id="e2d9a-128">Entity Framework Code First, LocalDB</span></span>
- <span data-ttu-id="e2d9a-129">요청 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="e2d9a-129">Request Validation</span></span>
- <span data-ttu-id="e2d9a-130">강력한 형식의 데이터 컨트롤</span><span class="sxs-lookup"><span data-stu-id="e2d9a-130">Strongly-typed Data Controls</span></span>
- <span data-ttu-id="e2d9a-131">모델 바인딩</span><span class="sxs-lookup"><span data-stu-id="e2d9a-131">Model Binding</span></span>
- <span data-ttu-id="e2d9a-132">데이터 주석</span><span class="sxs-lookup"><span data-stu-id="e2d9a-132">Data Annotations</span></span>
- <span data-ttu-id="e2d9a-133">값 공급자</span><span class="sxs-lookup"><span data-stu-id="e2d9a-133">Value Providers</span></span>
- <span data-ttu-id="e2d9a-134">SSL 및 OAuth</span><span class="sxs-lookup"><span data-stu-id="e2d9a-134">SSL and OAuth</span></span>
- <span data-ttu-id="e2d9a-135">ASP.NET Id, 구성 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="e2d9a-135">ASP.NET Identity, Configuration, and Authorization</span></span>
- <span data-ttu-id="e2d9a-136">비간섭 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="e2d9a-136">Unobtrusive Validation</span></span>
- <span data-ttu-id="e2d9a-137">라우팅</span><span class="sxs-lookup"><span data-stu-id="e2d9a-137">Routing</span></span>
- <span data-ttu-id="e2d9a-138">ASP.NET 오류 처리</span><span class="sxs-lookup"><span data-stu-id="e2d9a-138">ASP.NET Error Handling</span></span>

### <a name="application-scenarios-and-tasks"></a><span data-ttu-id="e2d9a-139">응용 프로그램 시나리오 및 작업</span><span class="sxs-lookup"><span data-stu-id="e2d9a-139">Application scenarios and tasks</span></span>

<span data-ttu-id="e2d9a-140">자습서 시리즈 작업에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-140">Tutorial series tasks include:</span></span>

- <span data-ttu-id="e2d9a-141">만들기, 검토 및 새 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-141">Creating, reviewing, and running a new project</span></span>
- <span data-ttu-id="e2d9a-142">데이터베이스 구조 만들기</span><span class="sxs-lookup"><span data-stu-id="e2d9a-142">Creating a database structure</span></span>
- <span data-ttu-id="e2d9a-143">초기화 및 데이터베이스 시 딩</span><span class="sxs-lookup"><span data-stu-id="e2d9a-143">Initializing and seeding a database</span></span>
- <span data-ttu-id="e2d9a-144">스타일, 그래픽 및 마스터 페이지를 사용 하 여 UI 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="e2d9a-144">Customizing the UI with styles, graphics, and a master page</span></span>
- <span data-ttu-id="e2d9a-145">페이지 및 탐색 기능 추가</span><span class="sxs-lookup"><span data-stu-id="e2d9a-145">Adding pages and navigation</span></span>
- <span data-ttu-id="e2d9a-146">메뉴 세부 정보 및 제품 데이터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-146">Displaying menu details and product data</span></span>
- <span data-ttu-id="e2d9a-147">쇼핑 카트 만들기</span><span class="sxs-lookup"><span data-stu-id="e2d9a-147">Creating a shopping cart</span></span>
- <span data-ttu-id="e2d9a-148">추가 SSL 및 OAuth 지원</span><span class="sxs-lookup"><span data-stu-id="e2d9a-148">Adding SSL and OAuth support</span></span>
- <span data-ttu-id="e2d9a-149">지불 방법 추가</span><span class="sxs-lookup"><span data-stu-id="e2d9a-149">Adding a payment method</span></span>
- <span data-ttu-id="e2d9a-150">관리자 역할 및 응용 프로그램에 사용자를 포함 하 여</span><span class="sxs-lookup"><span data-stu-id="e2d9a-150">Including an administrator role and a user to the application</span></span>
- <span data-ttu-id="e2d9a-151">특정 페이지 및 폴더에 대 한 액세스 제한</span><span class="sxs-lookup"><span data-stu-id="e2d9a-151">Restricting access to specific pages and folder</span></span>
- <span data-ttu-id="e2d9a-152">웹 응용 프로그램 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-152">Uploading a file to the web application</span></span>
- <span data-ttu-id="e2d9a-153">입력된 유효성 검사 구현</span><span class="sxs-lookup"><span data-stu-id="e2d9a-153">Implementing input validation</span></span>
- <span data-ttu-id="e2d9a-154">웹 응용 프로그램에 대 한 경로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-154">Registering routes for the web application</span></span>
- <span data-ttu-id="e2d9a-155">오류 처리 및 오류 로깅 구현</span><span class="sxs-lookup"><span data-stu-id="e2d9a-155">Implementing error handling and error logging</span></span>

## <a name="overview"></a><span data-ttu-id="e2d9a-156">개요</span><span class="sxs-lookup"><span data-stu-id="e2d9a-156">Overview</span></span>

<span data-ttu-id="e2d9a-157">이 자습서 시리즈에 프로그래밍 개념에 익숙한 사용자에 게 적합 하지만 새 ASP.NET Web forms는입니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-157">This tutorial series is intended for someone familiar with programming concepts, but new to ASP.NET Web Forms.</span></span> <span data-ttu-id="e2d9a-158">인 경우 이미 친숙 한 ASP.NET Web Forms를 사용 하 여이 시리즈도 도움이 될 수 있습니다 새 ASP.NET 4.5 기능에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-158">If you're already familiar with ASP.NET Web Forms, this series can still help you learn about new ASP.NET 4.5 features.</span></span> <span data-ttu-id="e2d9a-159">프로그래밍 개념 및 ASP.NET Web Forms를 사용 하 여 알 수 없는 판독기에 제공 된 추가 Web Forms 자습서를 참조 하세요. 합니다 [Getting Started](../../../index.md) ASP.NET 웹 사이트의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-159">For readers unfamiliar with programming concepts and ASP.NET Web Forms, see the additional Web Forms tutorials provided in the [Getting Started](../../../index.md) section on the ASP.NET Web site.</span></span>

<span data-ttu-id="e2d9a-160">이 자습서 시리즈에서 제공 하는 ASP.NET 4.5에는 다음 기능이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-160">The ASP.NET 4.5 provided in this tutorial series includes the following features:</span></span>

- <span data-ttu-id="e2d9a-161">제공 하는 프로젝트를 만들기 위한 간단한 UI [많은 ASP.NET 프레임 워크에 대 한 지원을](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) (Web Forms, MVC 및 Web API).</span><span class="sxs-lookup"><span data-stu-id="e2d9a-161">A simple UI for creating projects that offers [support for many ASP.NET frameworks](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) (Web Forms, MVC, and Web API).</span></span>
- <span data-ttu-id="e2d9a-162">[부트스트랩](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), 레이아웃, 테마 및 반응 형 디자인 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-162">[Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), a layout, theming, and responsive design framework.</span></span>
- <span data-ttu-id="e2d9a-163">[ASP.NET Id](../../../../identity/index.md), 웹 호스팅 IIS 외에 소프트웨어를 사용 하 여 모든 ASP.NET 프레임 워크와에서 동일 하 게 작동 하는 새로운 ASP.NET 멤버 자격 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-163">[ASP.NET Identity](../../../../identity/index.md), a new ASP.NET membership system that works the same in all ASP.NET frameworks and works with web hosting software other than IIS.</span></span>
- [<span data-ttu-id="e2d9a-164">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="e2d9a-164">Entity Framework 6</span></span>](https://msdn.microsoft.com/data/ef.aspx)

  <span data-ttu-id="e2d9a-165">수 있도록 하는 Entity Framework에 대 한 업데이트:</span><span class="sxs-lookup"><span data-stu-id="e2d9a-165">An update to the Entity Framework enabling you to:</span></span>
  - <span data-ttu-id="e2d9a-166">강력한 형식의 개체로 데이터 검색 및 조작</span><span class="sxs-lookup"><span data-stu-id="e2d9a-166">Retrieve and manipulate data as strongly-typed objects</span></span>
  - <span data-ttu-id="e2d9a-167">데이터를 비동기적으로 액세스</span><span class="sxs-lookup"><span data-stu-id="e2d9a-167">Access data asynchronously</span></span>
  - <span data-ttu-id="e2d9a-168">일시적인 연결 오류 처리</span><span class="sxs-lookup"><span data-stu-id="e2d9a-168">Handle transient connection faults</span></span>
  - <span data-ttu-id="e2d9a-169">로그 SQL 문</span><span class="sxs-lookup"><span data-stu-id="e2d9a-169">Log SQL statements</span></span>

<span data-ttu-id="e2d9a-170">ASP.NET 4.5 기능 목록은 참조 하세요 [ASP.NET 및 Web Tools for Visual Studio 2013 릴리스 정보](../../../../visual-studio/overview/2013/release-notes.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-170">For a complete ASP.NET 4.5 feature list, see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](../../../../visual-studio/overview/2013/release-notes.md).</span></span>

### <a name="the-wingtip-toys-sample-application"></a><span data-ttu-id="e2d9a-171">Wingtip Toys 샘플 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="e2d9a-171">The Wingtip Toys sample application</span></span>

<span data-ttu-id="e2d9a-172">다음 스크린샷에서이 자습서 시리즈에서 만든 ASP.NET Web Forms 응용 프로그램에서.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-172">The following screenshots are from the ASP.NET Web Forms application that you create in this tutorial series.</span></span> <span data-ttu-id="e2d9a-173">Visual Studio에서 응용 프로그램을 실행 하는 경우 다음 웹 홈 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-173">When you run the application in Visual Studio, the following web Home page appears.</span></span>

![Wingtip Toys-기본 페이지](introduction-and-overview/_static/image1.png)

<span data-ttu-id="e2d9a-175">새 사용자로 등록 하거나 기존 사용자로 로그인 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-175">You can register as a new user, or sign in as an existing user.</span></span> <span data-ttu-id="e2d9a-176">위쪽 탐색 모음에는 데이터베이스에서 제품 범주 및 해당 제품에 대 한 링크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-176">The top navigation has links to product categories and their products from the database.</span></span>

<span data-ttu-id="e2d9a-177">선택 하는 경우 **제품**, 사용 가능한 제품은 모두 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-177">If you select **Products**, all available products are displayed.</span></span> 

![Wingtip Toys-제품](introduction-and-overview/_static/image2.png)

<span data-ttu-id="e2d9a-179">특정 제품을 선택 하면 제품 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-179">If you select a specific product, product details are displayed.</span></span>


![Wingtip Toys-제품 세부 정보](introduction-and-overview/_static/image3.png)

<span data-ttu-id="e2d9a-181">사용자로 등록 한 Web Forms 템플릿 기본 기능을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-181">As a user, you can register and sign in with Web Forms template default functionality.</span></span> <span data-ttu-id="e2d9a-182">이 자습서에는 또한 기존 Gmail 계정을 사용 하 여 로그인 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-182">This tutorial also explains how to sign in using an existing Gmail account.</span></span> <span data-ttu-id="e2d9a-183">또한 추가 하 고 데이터베이스에서 제품을 제거 하려면 관리자 권한으로 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-183">Additionally, you can sign in as the administrator to add and remove products from the database.</span></span>

![Wingtip Toys-로그인](introduction-and-overview/_static/image4.png)

<span data-ttu-id="e2d9a-185">사용자로 로그인 한 후 PayPal로 체크 아웃을 쇼핑 카트에 제품을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-185">Once you've signed in as a user, you can add products to the shopping cart and checkout with PayPal.</span></span> <span data-ttu-id="e2d9a-186">샘플 응용 프로그램은 PayPal의 개발자 샌드박스에서 작동 하도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-186">The sample application is designed to work in PayPal's developer sandbox.</span></span> <span data-ttu-id="e2d9a-187">실제 비용 트랜잭션이 수행이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-187">No actual money transaction takes place.</span></span>

![Wingtip Toys-쇼핑 카트](introduction-and-overview/_static/image5.png)

<span data-ttu-id="e2d9a-189">PayPal 계정, 순서 및 결제 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-189">PayPal confirms your account, order, and payment information.</span></span>

![Wingtip Toys-PayPal](introduction-and-overview/_static/image6.png)

<span data-ttu-id="e2d9a-191">PayPal에서 반환한 검토 하 고 주문을 완료 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-191">After returning from PayPal, you can review and complete your order.</span></span>

![Wingtip Toys-주문 검토](introduction-and-overview/_static/image7.png)

## <a name="prerequisites"></a><span data-ttu-id="e2d9a-193">전제 조건</span><span class="sxs-lookup"><span data-stu-id="e2d9a-193">Prerequisites</span></span>

<span data-ttu-id="e2d9a-194">시작 하기 전에 다음 소프트웨어가 컴퓨터에 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-194">Before you start, make sure the following software is installed on your computer:</span></span>

- <span data-ttu-id="e2d9a-195">[Microsoft Visual Studio 2017 또는 Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-195">[Microsoft Visual Studio 2017 or Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/).</span></span>

<span data-ttu-id="e2d9a-196">.NET Framework는 자동으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-196">The .NET Framework is installed automatically.</span></span>

<span data-ttu-id="e2d9a-197">이 자습서 시리즈는 Microsoft Visual Studio Community 2017을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-197">This tutorial series uses Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="e2d9a-198">중 하나를 사용할 수 있습니다 또는 Microsoft Visual Studio 2017이 자습서 시리즈를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-198">You can use either that or Microsoft Visual Studio 2017 to complete this tutorial series.</span></span>

<span data-ttu-id="e2d9a-199">Visual Studio에 대 한 다음 note:</span><span class="sxs-lookup"><span data-stu-id="e2d9a-199">Note the following about Visual Studio:</span></span>

* <span data-ttu-id="e2d9a-200">Microsoft Visual Studio 2017 및 Microsoft Visual Studio Community 2017 이라고 *Visual Studio* 이 자습서 시리즈 전체.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-200">Microsoft Visual Studio 2017 and Microsoft Visual Studio Community 2017 are referred to as *Visual Studio* throughout this tutorial series.</span></span>

* <span data-ttu-id="e2d9a-201">Visual Studio 2017이 이미 설치 된 이전 버전 옆에 있는 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-201">Visual Studio 2017 is installed next to any older versions already installed.</span></span> <span data-ttu-id="e2d9a-202">이전 버전에서 만든 사이트는 Visual Studio 2017에서 열 수 있습니다 하 고 이전 버전에서 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-202">Sites created in earlier versions can be opened in Visual Studio 2017 and continue to open in previous versions.</span></span>

* <span data-ttu-id="e2d9a-203">처음으로 Visual Studio를 시작, 선택한 가정 합니다 *웹 개발* 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-203">The first time you started Visual Studio, it is assumed you selected the *Web Development* settings.</span></span> <span data-ttu-id="e2d9a-204">자세한 내용은 [방법: 웹 개발 환경 설정 선택](https://msdn.microsoft.com/library/ff521558.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-204">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>

<span data-ttu-id="e2d9a-205">필수 구성 요소를 설치한 후이 자습서 시리즈에서 제공 하는 웹 프로젝트 만들기를 시작 하려면 준비가입니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-205">After installing the prerequisites, you're ready to begin creating the Web project presented in this tutorial series.</span></span>

## <a name="download-the-sample-application"></a><span data-ttu-id="e2d9a-206">샘플 응용 프로그램 다운로드</span><span class="sxs-lookup"><span data-stu-id="e2d9a-206">Download the sample application</span></span>

 <span data-ttu-id="e2d9a-207">MSDN 샘플 사이트에서 언제 든 지에서 완성 된 샘플 applicatiion를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-207">You can download the completed sample applicatiion at anytime from the MSDN Samples site:</span></span>

<span data-ttu-id="e2d9a-208">[Getting Started with ASP.NET 4.5 Web Forms 및 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span><span class="sxs-lookup"><span data-stu-id="e2d9a-208">[Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span></span> 

 <span data-ttu-id="e2d9a-209">이 다운로드에는 다음 항목에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-209">This download has the following items:</span></span>

- <span data-ttu-id="e2d9a-210">샘플 응용 프로그램을 *WingtipToys* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-210">The sample application in the *WingtipToys* folder.</span></span>
- <span data-ttu-id="e2d9a-211">샘플 응용 프로그램을 만들려면 사용 하는 리소스를 *WingtipToys 자산* 폴더에는 *WingtipToys* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-211">The resources used to create the sample application in the *WingtipToys-Assets* folder in the *WingtipToys* folder.</span></span>

<span data-ttu-id="e2d9a-212">다운로드 되는 *.zip* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-212">The download is a *.zip* file.</span></span> <span data-ttu-id="e2d9a-213">이 자습서 시리즈에서 만든 완료 된 프로젝트, 찾기 및 선택 합니다 *C#* .zip 파일에는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-213">To see the completed project that this tutorial series creates, find and select the *C#* folder in the .zip file.</span></span> <span data-ttu-id="e2d9a-214">저장 된 C# 폴더로 Visual Studio 프로젝트를 사용 하 여 작업에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-214">Save the C# folder to the folder you use to work with Visual Studio projects.</span></span> <span data-ttu-id="e2d9a-215">기본적으로 Visual Studio 2017 프로젝트 폴더는:</span><span class="sxs-lookup"><span data-stu-id="e2d9a-215">By default, the Visual Studio 2017 projects folder is:</span></span>

<span data-ttu-id="e2d9a-216"><strong>C:\Users&#92;</strong><strong><em>&lt;username&gt;</em></strong><strong>\source\repos</strong></span><span class="sxs-lookup"><span data-stu-id="e2d9a-216"><strong>C:\Users&#92;</strong><strong><em>&lt;username&gt;</em></strong><strong>\source\repos</strong></span></span>

<span data-ttu-id="e2d9a-217">이름 바꾸기는 ***C#*** 폴더 ***WingtipToys***합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-217">Rename the ***C#*** folder to ***WingtipToys***.</span></span>

> [!NOTE]
> <span data-ttu-id="e2d9a-218">라는 폴더를 이미 있다면 *WingtipToys* 에 프로젝트 폴더의 이름을 일시적으로 기존 폴더 이름을 바꾸기 전에 *C#* 폴더를 *WingtipToys*합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-218">If you already have a folder named *WingtipToys* in your Projects folder, temporarily rename that existing folder before renaming the *C#* folder to *WingtipToys*.</span></span>

<span data-ttu-id="e2d9a-219">완료 된 프로젝트를 실행 하려면 엽니다는 *WingtipToys* 폴더를 두 번 클릭 합니다 *WingtipToys.sln* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-219">To run the completed project, open the *WingtipToys* folder and double-click the *WingtipToys.sln* file.</span></span> <span data-ttu-id="e2d9a-220">Visual Studio 2017 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-220">Visual Studio 2017 opens the project.</span></span> <span data-ttu-id="e2d9a-221">그런 다음 마우스 오른쪽 단추로 클릭 합니다 *Default.aspx* 파일 **솔루션 탐색기** 선택한 **브라우저에서 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-221">Next, right-click the *Default.aspx* file in **Solution Explorer** and select **View In Browser**.</span></span>

## <a name="take-a-aspnet-web-forms-quiz-to-review-content"></a><span data-ttu-id="e2d9a-222">ASP.NET Web Forms 퀴즈를 통해 콘텐츠를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-222">Take a ASP.NET Web Forms quiz to review content</span></span>

<span data-ttu-id="e2d9a-223">자습서 시리즈를 완료 한 후 퀴즈를 배운 내용을 테스트 하 고 주요 개념을 보강 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-223">After completing the tutorial series, take a quiz to test your knowledge and reinforce key concepts.</span></span> <span data-ttu-id="e2d9a-224">각 질문 설명 및 추가 지침에 대 한 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-224">Each question provides an explanation and links to additional guidance.</span></span>

 * [<span data-ttu-id="e2d9a-225">ASP.NET Web Forms 퀴즈</span><span class="sxs-lookup"><span data-stu-id="e2d9a-225">ASP.NET Web Forms Quiz</span></span>](https://blogs.msdn.microsoft.com/erikreitan/2016/01/08/asp-net-web-forms-quiz/) 

## <a name="tutorial-support-and-comments"></a><span data-ttu-id="e2d9a-226">자습서 지원 및 주석</span><span class="sxs-lookup"><span data-stu-id="e2d9a-226">Tutorial support and comments</span></span>

<span data-ttu-id="e2d9a-227">의견 및 질문에 대 한 질문과 대답 섹션에 포함을 사용 합니다 [Getting Started with ASP.NET 4.5 Web Forms 및 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) 샘플 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-227">For questions and comments, use the Q and A section included on the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample page.</span></span>

<span data-ttu-id="e2d9a-228">이 자습서 시리즈에 대 한 의견을 기다리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-228">Comments on this tutorial series are welcome.</span></span> <span data-ttu-id="e2d9a-229">이 자습서 시리즈를 업데이트 하는 경우에 수정 또는 향상 된 기능에 대 한 제안 사항을 고려해 야 할 노력이 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-229">When this tutorial series is updated, every effort is made to consider corrections or suggestions for improvements.</span></span>

<span data-ttu-id="e2d9a-230">오류가 발생을 해당 하는 오류 메시지는 혼동 될 수 없습니다를 해결 하는 방법에 대 한 설명이 없으므로 좋은 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-230">If an error occurs, the corresponding error messages could be confusing, with no good explanation on how to fix it.</span></span> <span data-ttu-id="e2d9a-231">에 대 한 도움말을 확인할 수 있습니다 합니다 [ASP.NET 포럼](https://forums.asp.net/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-231">For help, you can check the [ASP.NET forums](https://forums.asp.net/).</span></span> <span data-ttu-id="e2d9a-232">또 다른 좋은 소스는 질문과 대답 섹션에는 [Getting Started with ASP.NET 4.5 Web Forms 및 Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) 샘플 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="e2d9a-232">Another good source is the Q and A section in the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample page.</span></span> 

> [!div class="step-by-step"]
> [<span data-ttu-id="e2d9a-233">다음</span><span class="sxs-lookup"><span data-stu-id="e2d9a-233">Next</span></span>](create-the-project.md)
