---
uid: overview
title: "ASP.NET 개요 | Microsoft Docs"
author: rick-anderson
description: "ASP.NET, 웹 사이트, 웹 응용 프로그램 및 web Api 만들기 위한 무료 프레임 워크에 소개 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/12/2010
ms.topic: article
ms.assetid: 3a309468-f1ca-4e51-b9c3-536af79d7a8b
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: 
msc.type: content
ms.openlocfilehash: ed11c882c801248ffaca95b82f16d23c87fb9be7
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="aspnet-overview"></a><span data-ttu-id="d3c1a-103">ASP.NET 개요</span><span class="sxs-lookup"><span data-stu-id="d3c1a-103">ASP.NET overview</span></span>

<span data-ttu-id="d3c1a-104">ASP.NET은 뛰어난 웹 사이트 및 HTML, CSS 및 JavaScript를 사용 하 여 웹 응용 프로그램을 구축 하기 위한 무료 웹 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-104">ASP.NET is a free web framework for building great websites and web applications using HTML, CSS, and JavaScript.</span></span> <span data-ttu-id="d3c1a-105">웹 Api을 만들고 웹 소켓 같은 실시간 기술을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-105">You can also create Web APIs and use real-time technologies like Web Sockets.</span></span>

<span data-ttu-id="d3c1a-106">[ASP.NET Core](https://docs.microsoft.com/aspnet/core/) ASP.NET 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-106">[ASP.NET Core](https://docs.microsoft.com/aspnet/core/) is an alternative to ASP.NET.</span></span>  <span data-ttu-id="d3c1a-107">참조는 [ASP.NET 및 ASP.NET Core 선택 하는 방법에 대 한 지침](https://docs.microsoft.com/aspnet/core/choose-aspnet-framework)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-107">See the [guidance on how to choose between ASP.NET and ASP.NET Core](https://docs.microsoft.com/aspnet/core/choose-aspnet-framework).</span></span>

## <a name="get-started"></a><span data-ttu-id="d3c1a-108">시작</span><span class="sxs-lookup"><span data-stu-id="d3c1a-108">Get started</span></span>

<span data-ttu-id="d3c1a-109">[Visual Studio 2015를 다운로드](https://go.microsoft.com/fwlink/?LinkId=826064), Windows에서 ASP.NET에 대 한 IDE를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-109">[Download Visual Studio 2015](https://go.microsoft.com/fwlink/?LinkId=826064), a free IDE for ASP.NET on Windows.</span></span>

## <a name="websites-and-web-applications"></a><span data-ttu-id="d3c1a-110">웹 사이트 및 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d3c1a-110">Websites and web applications</span></span>

 <span data-ttu-id="d3c1a-111">ASP.NET은 웹 응용 프로그램을 만들기 위한 세 가지 프레임 워크를 제공: Web Forms, ASP.NET MVC 및 ASP.NET 웹 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-111">ASP.NET offers three frameworks for creating web applications: Web Forms, ASP.NET MVC, and ASP.NET Web Pages.</span></span> <span data-ttu-id="d3c1a-112">모든 세 가지 프레임 워크 안정적이 고 발달 되며 그 중 하나에 있는 뛰어난 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-112">All three frameworks are stable and mature, and you can create great web applications with any of them.</span></span> <span data-ttu-id="d3c1a-113">선택 하면 어떤 프레임 워크에 관계 없이 모든 장점과 ASP.NET everywhere 기능 받아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-113">No matter what framework you choose, you will get all the benefits and features of ASP.NET everywhere.</span></span>

<span data-ttu-id="d3c1a-114">각 프레임 워크에 다양 한 개발 스타일을 대상 으로합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-114">Each framework targets a different development style.</span></span> <span data-ttu-id="d3c1a-115">선택한 하나 익숙해지면 개발 접근 방식 및 응용 프로그램을 만드는의 유형, 프로그래밍 자산 (기술 자료, 기술 및 개발 환경)의 조합에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-115">The one you choose depends on a combination of your programming assets (knowledge, skills, and development experience), the type of application you’re creating, and the development approach you’re comfortable with.</span></span>

<span data-ttu-id="d3c1a-116">다음은 각 프레임 워크가 및 선택 하는 방법에 대 한 몇 가지 아이디어의 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-116">Below is an overview of each of the frameworks and some ideas for how to choose between them.</span></span> <span data-ttu-id="d3c1a-117">한 비디오 소개를 선호 하는 경우 참조 [asp.net 웹 사이트 만들기](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/Making-Websites-with-ASPNET) 및 [웹 도구 란?](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/what-is-web-tools)</span><span class="sxs-lookup"><span data-stu-id="d3c1a-117">If you prefer a video introduction, see [Making Websites with ASP.NET](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/Making-Websites-with-ASPNET) and [What is Web Tools?](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/what-is-web-tools)</span></span>

|   | <span data-ttu-id="d3c1a-118">환경에 있는 경우</span><span class="sxs-lookup"><span data-stu-id="d3c1a-118">If you have experience in</span></span> | <span data-ttu-id="d3c1a-119">개발 스타일</span><span class="sxs-lookup"><span data-stu-id="d3c1a-119">Development style</span></span> | <span data-ttu-id="d3c1a-120">전문 지식</span><span class="sxs-lookup"><span data-stu-id="d3c1a-120">Expertise</span></span> | 
|-----------|----------------------|-----------------------------------------------------|----------------|
| <span data-ttu-id="d3c1a-121">Web Forms</span><span class="sxs-lookup"><span data-stu-id="d3c1a-121">Web Forms</span></span> | <span data-ttu-id="d3c1a-122">Win Forms, WPF, .NET</span><span class="sxs-lookup"><span data-stu-id="d3c1a-122">Win Forms, WPF, .NET</span></span> | <span data-ttu-id="d3c1a-123">HTML 태그를 캡슐화 하는 컨트롤의 풍부한 라이브러리를 사용 하 여 신속 하 게 개발</span><span class="sxs-lookup"><span data-stu-id="d3c1a-123">Rapid development using a rich library of controls that encapsulate HTML markup</span></span> | <span data-ttu-id="d3c1a-124">표준은 중간 수준의 고급 RAD</span><span class="sxs-lookup"><span data-stu-id="d3c1a-124">Mid-Level, Advanced RAD</span></span> |
| <span data-ttu-id="d3c1a-125">MVC</span><span class="sxs-lookup"><span data-stu-id="d3c1a-125">MVC</span></span>       | <span data-ttu-id="d3c1a-126">레일에.NET에 ruby</span><span class="sxs-lookup"><span data-stu-id="d3c1a-126">Ruby on Rails, .NET</span></span>  | <span data-ttu-id="d3c1a-127">HTML 태그, 코드 및 태그, 분리 되 고 테스트를 작성 하기가 대 한 모든 권한을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-127">Full control over HTML markup, code and markup separated, and easy to write tests.</span></span> <span data-ttu-id="d3c1a-128">모바일 및 단일 페이지 응용 프로그램 (SPA)에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-128">The best choice for mobile and single-page applications (SPA).</span></span> | <span data-ttu-id="d3c1a-129">Mid-Level, Advanced</span><span class="sxs-lookup"><span data-stu-id="d3c1a-129">Mid-Level, Advanced</span></span> |
| <span data-ttu-id="d3c1a-130">웹 페이지</span><span class="sxs-lookup"><span data-stu-id="d3c1a-130">Web Pages</span></span>  | <span data-ttu-id="d3c1a-131">클래식 ASP, PHP</span><span class="sxs-lookup"><span data-stu-id="d3c1a-131">Classic ASP, PHP</span></span>     | <span data-ttu-id="d3c1a-132">HTML 태그와 같은 파일에 함께 코드</span><span class="sxs-lookup"><span data-stu-id="d3c1a-132">HTML markup and your code together in the same file</span></span> | <span data-ttu-id="d3c1a-133">새, 중간 수준</span><span class="sxs-lookup"><span data-stu-id="d3c1a-133">New, Mid-Level</span></span> |

### <a name="web-forms"></a><span data-ttu-id="d3c1a-134">Web Forms</span><span class="sxs-lookup"><span data-stu-id="d3c1a-134">Web Forms</span></span>

<span data-ttu-id="d3c1a-135">ASP.NET Web Forms 친숙 한 끌어서 놓기, 이벤트 기반 모델을 사용 하 여 동적 웹 사이트를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-135">With ASP.NET Web Forms, you can build dynamic websites using a familiar drag-and-drop, event-driven model.</span></span> <span data-ttu-id="d3c1a-136">디자인 화면과 수백 개의 컨트롤 및 구성 요소를 통해 빠르게 정교 하 고 강력한 UI 기반의 사이트 데이터 액세스를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-136">A design surface and hundreds of controls and components let you rapidly build sophisticated, powerful UI-driven sites with data access.</span></span> 

[<span data-ttu-id="d3c1a-137">Web Forms에 대 한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="d3c1a-137">Learn more about Web Forms</span></span>](web-forms/index.md)

### <a name="mvc"></a><span data-ttu-id="d3c1a-138">MVC</span><span class="sxs-lookup"><span data-stu-id="d3c1a-138">MVC</span></span>

<span data-ttu-id="d3c1a-139">ASP.NET MVC 문제의 확실히 구분할 수 있도록 제공 하 고,는 태그를 완전히 제어할 기반의 방법을 제공에 대 한 동적 웹 사이트를 구축 하는 강력한 패턴 기반의 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-139">ASP.NET MVC gives you a powerful, patterns-based way to build dynamic websites that enables a clean separation of concerns and that gives you full control over markup for enjoyable, agile development.</span></span> <span data-ttu-id="d3c1a-140">ASP.NET MVC에는 최신 웹 표준을 사용 하는 복잡 한 응용 프로그램을 만들기 위한 개발을 신속 하 고 사용이 가능 하 게 수 있는 여러 기능이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-140">ASP.NET MVC includes many features that enable fast, TDD-friendly development for creating sophisticated applications that use the latest web standards.</span></span> 

[<span data-ttu-id="d3c1a-141">MVC에 대 한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="d3c1a-141">Learn more about MVC</span></span>](mvc/index.md)

### <a name="aspnet-web-pages"></a><span data-ttu-id="d3c1a-142">ASP.NET 웹 페이지</span><span class="sxs-lookup"><span data-stu-id="d3c1a-142">ASP.NET Web Pages</span></span>

<span data-ttu-id="d3c1a-143">ASP.NET 웹 페이지 및 Razor 구문 html 동적 웹 콘텐츠를 만들려는 서버 코드를 결합 하는 빠르고 쉬우며 간편한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-143">ASP.NET Web Pages and the Razor syntax provide a fast, approachable, and lightweight way to combine server code with HTML to create dynamic web content.</span></span> <span data-ttu-id="d3c1a-144">데이터베이스에 연결, 비디오를 추가 하 고, 소셜 네트워킹 사이트에 연결 하 고 많은 포함 최신 웹 표준을 준수 하는 보기 좋은 사이트를 만들 수 있는 더 많은 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-144">Connect to databases, add video, link to social networking sites, and include many more features that help you create beautiful sites that conform to the latest web standards.</span></span>

[<span data-ttu-id="d3c1a-145">웹 페이지에 대 한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="d3c1a-145">Learn more about Web Pages</span></span>](web-pages/index.md)

### <a name="notes-about-web-forms-mvc-and-web-pages"></a><span data-ttu-id="d3c1a-146">Web Forms, MVC 및 웹 페이지에 대 한 참고 사항</span><span class="sxs-lookup"><span data-stu-id="d3c1a-146">Notes about Web Forms, MVC, and Web Pages</span></span>

<span data-ttu-id="d3c1a-147">모든 세 가지 ASP.NET 프레임 워크는.NET Framework를 기반으로 하 고 ASP.NET 및.NET의 핵심 기능을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-147">All three ASP.NET frameworks are based on the .NET Framework and share core functionality of .NET and of ASP.NET.</span></span> <span data-ttu-id="d3c1a-148">예를 들어 모든 세 가지 프레임 워크를 기반으로 멤버 자격, 로그인 보안 모델을 제공 하 고 세 가지 모두 핵심 기능 ASP.NET의 일부인 요청, 처리 세션을 관리 하기 위한 동일한 기능을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-148">For example, all three frameworks offer a login security model based around membership, and all three share the same facilities for managing requests, handling sessions, and so on that are part of the core ASP.NET functionality.</span></span>

<span data-ttu-id="d3c1a-149">그리고 세 개의 프레임 워크가 완전히 독립적 하나를 선택 해도 다른를 사용 하 여 방해 하지 않는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-149">In addition, the three frameworks are not entirely independent, and choosing one does not preclude using another.</span></span> <span data-ttu-id="d3c1a-150">프레임 워크는 동일한 웹 응용 프로그램에서 공존할 수 있으므로 서로 다른 프레임 워크를 사용 하 여 작성 된 응용 프로그램의 개별 구성 요소를 볼 수는 일반적이 지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-150">Since the frameworks can coexist in the same web application, it's not uncommon to see individual components of applications written using different frameworks.</span></span> <span data-ttu-id="d3c1a-151">예를 들어 Web Forms 컨트롤 데이터 및 단순 데이터 액세스를 활용 하도록 데이터 액세스 및 관리 부분은 모두 개발 하는 동안에 태그를 최적화 하기 위해 mvc에서 응용 프로그램의 고객 관련 부분을 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-151">For example, customer-facing portions of an app might be developed in MVC to optimize the markup, while the data access and administrative portions are developed in Web Forms to take advantage of data controls and simple data access.</span></span>

## <a name="web-apis"></a><span data-ttu-id="d3c1a-152">Web API</span><span class="sxs-lookup"><span data-stu-id="d3c1a-152">Web APIs</span></span>

<span data-ttu-id="d3c1a-153">ASP.NET Web API는 다양 한 브라우저 및 모바일 장치를 포함 한 클라이언트를 연결할 HTTP 서비스를 작성을 용이 하 게 하는 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-153">ASP.NET Web API is a framework that makes it easy to build HTTP services that reach a broad range of clients, including browsers and mobile devices.</span></span> <span data-ttu-id="d3c1a-154">ASP.NET Web API는 .NET Framework에서 RESTful 응용 프로그램을 빌드하는 데 이상적인 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-154">ASP.NET Web API is an ideal platform for building RESTful applications on the .NET Framework.</span></span>

[<span data-ttu-id="d3c1a-155">웹 API에 대 한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="d3c1a-155">Learn more about Web API</span></span>](web-api/index.md)

<!-- Put first under Web API TOC:  Watch video (9 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/services-and-aspnet -->

## <a name="real-time-technologies"></a><span data-ttu-id="d3c1a-156">실시간 기술</span><span class="sxs-lookup"><span data-stu-id="d3c1a-156">Real-time technologies</span></span>

<span data-ttu-id="d3c1a-157">ASP.NET SignalR은 ASP.NET 개발자를 위한 개발 실시간 웹 기능을 더 쉽게 하는 새 라이브러리.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-157">ASP.NET SignalR is a new library for ASP.NET developers that makes developing real-time web functionality easier.</span></span> <span data-ttu-id="d3c1a-158">SignalR 서버와 클라이언트 간의 양방향 통신을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-158">SignalR allows bi-directional communication between server and client.</span></span> <span data-ttu-id="d3c1a-159">서버를 사용할 수 있게 되 면 즉시 연결 된 클라이언트에 콘텐츠 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-159">Servers can push content to connected clients instantly as it becomes available.</span></span> <span data-ttu-id="d3c1a-160">SignalR은 Websocket을 지원 및 이전 버전의 브라우저에 대 한 호환 다른 방법으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-160">SignalR supports Web Sockets, and falls back to other compatible techniques for older browsers.</span></span> <span data-ttu-id="d3c1a-161">SignalR 연결 관리에 대 한 Api가 포함 됩니다 (예를 들어, 연결 및 연결 끊기 이벤트), 연결 그룹화 및 권한 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-161">SignalR includes APIs for connection management (for instance, connect and disconnect events), grouping connections, and authorization.</span></span>

[<span data-ttu-id="d3c1a-162">SignalR에 대 한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="d3c1a-162">Learn more about SignalR</span></span>](signalr/index.md)

<!-- Put first under SignalR TOC:  Watch video (6 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/signalr-and-the-real-time-web -->

## <a name="mobile-apps-and-sites"></a><span data-ttu-id="d3c1a-163">모바일 응용 프로그램 및 사이트</span><span class="sxs-lookup"><span data-stu-id="d3c1a-163">Mobile apps and sites</span></span> 

<span data-ttu-id="d3c1a-164">ASP.NET 웹 API 백 엔드 뿐만 아니라 부트스트랩 Twitter와 같은 한 반응 형 디자인 프레임 워크를 사용 하 여 모바일 웹 사이트는 네이티브 모바일 앱을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-164">ASP.NET can power native mobile apps with a Web API back end, as well as mobile web sites using responsive design frameworks like Twitter Bootstrap.</span></span> <span data-ttu-id="d3c1a-165">기본 모바일 앱을 작성 하는 경우 핸들 데이터 액세스, 인증 및 응용 프로그램에서 푸시 알림을 JSON 기반 웹 API를 만드는 것이 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-165">If you are building a native mobile app, it's easy to create a JSON-based Web API to handle data access, authentication, and push notifications for your app.</span></span> <span data-ttu-id="d3c1a-166">반응 형 모바일 사이트를 작성 하는 경우 모든 CSS 프레임 워크 또는 jQuery Mobile 또는 Sencha 및 PhoneGap으로 뛰어난 모바일 응용 프로그램 같은 강력한 모바일 시스템을 선택 하거나 원하는 하면 열기 그리드 시스템을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-166">If you are building a responsive mobile site, you can use any CSS framework or open grid system you prefer, or select a powerful mobile system like jQuery Mobile or Sencha and great mobile applications with PhoneGap.</span></span>

[<span data-ttu-id="d3c1a-167">모바일 응용 프로그램 및 사이트 개발에 대 한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="d3c1a-167">Learn more about mobile app and site development</span></span>](mobile/index.md)

<!-- Put first under mobile TOC:  Watch video (11 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/aspnet-and-mobile -->

## <a name="single-page-applications"></a><span data-ttu-id="d3c1a-168">단일 페이지 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d3c1a-168">Single-page applications</span></span> 

<span data-ttu-id="d3c1a-169">ASP.NET 단일 페이지 응용 프로그램 (SPA)를 사용 하면 HTML 5, CSS 3 및 JavaScript를 사용 하 여 중요 한 클라이언트 쪽 상호 작용을 포함 하는 응용 프로그램을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-169">ASP.NET Single Page Application (SPA) helps you build applications that include significant client-side interactions using HTML 5, CSS 3 and JavaScript.</span></span> <span data-ttu-id="d3c1a-170">Visual Studio knockout.js 및 ASP.NET Web API를 사용 하 여 단일 페이지 응용 프로그램을 구축 하기 위한 서식 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-170">Visual Studio includes a template for building single page applications using knockout.js and ASP.NET Web API.</span></span> <span data-ttu-id="d3c1a-171">기본 제공 SPA 템플릿 외에도 커뮤니티에서 만든 SPA 템플릿은 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-171">In addition to the built-in SPA template, community-created SPA templates are also available for download.</span></span>

[<span data-ttu-id="d3c1a-172">단일 페이지 응용 프로그램 개발에 대 한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="d3c1a-172">Learn more about single-page app development</span></span>](single-page-application/index.md)

## <a name="webhooks"></a><span data-ttu-id="d3c1a-173">웹후크</span><span class="sxs-lookup"><span data-stu-id="d3c1a-173">WebHooks</span></span>

<span data-ttu-id="d3c1a-174">또한 Webhook 배선 함께 웹 Api 및 SaaS 서비스에 대 한 간단한 pub/sub 모델을 제공 하는 간단한 HTTP 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-174">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="d3c1a-175">서비스에는 이벤트가 발생 하면 등록 된 구독자에 HTTP POST 요청의 형태로 알림이 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-175">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="d3c1a-176">POST 요청의 수신자 문제에 대 한 가능 하 게 하는 이벤트에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-176">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="d3c1a-177">또한 Webhook는 많은 수의 Dropbox, GitHub, Instagram, MailChimp, PayPal, 여유 시간, Trello, 및 등을 포함 하 여 서비스에 의해 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-177">WebHooks are exposed by a large number of services including Dropbox, GitHub, Instagram, MailChimp, PayPal, Slack, Trello, and many more.</span></span> <span data-ttu-id="d3c1a-178">예를 들어 여 webhook을 사용할지 의미할 수 있습니다 Dropbox 등의 파일이 변경 또는 GitHub에서 코드 변경이 커밋 또는 지불 PayPal에서 시작 되었습니다 Trello에서 카드를 만들지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c1a-178">For example, a WebHook can indicate that a file has changed in Dropbox, or a code change has been committed in GitHub, or a payment has been initiated in PayPal, or a card has been created in Trello.</span></span>

[<span data-ttu-id="d3c1a-179">또한 Webhook에 대 한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="d3c1a-179">Learn more about WebHooks</span></span>](webhooks/index.md)





<!--
Create Deployment TOC based on https://www.asp.net/aspnet/overview/deployment
Copy deployment content map to MVC, WebForms, Web Pages, Web API sections.
Copy Web Deployment in Enterprise from WebForms to MVC
Move under ASP.NET Best practices
    What not to do in ASP.NET, and what to do instead https://review.docs.microsoft.cus/aspnet/aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
    Async and await https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/async-and-await
    Building Real World Cloud Apps with Azure https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
    Hands on Lab: Maintainable Azure Websites: Managing Change and Scale https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale

-->
