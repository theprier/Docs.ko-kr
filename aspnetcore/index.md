---
title: ASP.NET Core 소개
author: rick-anderson
description: 클라우드 기반 인터넷에 연결된 최신 응용 프로그램을 빌드하기 위한 플랫폼 간 고성능 오픈 소스 프레임워크인 ASP.NET Core에 대한 소개를 가져옵니다.
ms.author: riande
ms.date: 9/28/2018
uid: index
ms.openlocfilehash: 3bb86fa255548ff66592ac14c1020e0c6b47959c
ms.sourcegitcommit: f43f430a166a7ec137fcad12ded0372747227498
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2018
ms.locfileid: "49391159"
---
# <a name="introduction-to-aspnet-core"></a><span data-ttu-id="6015c-103">ASP.NET Core 소개</span><span class="sxs-lookup"><span data-stu-id="6015c-103">Introduction to ASP.NET Core</span></span>

<span data-ttu-id="6015c-104">작성자: [Daniel Roth](https://github.com/danroth27), [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Shaun Luttin](https://twitter.com/dicshaunary)</span><span class="sxs-lookup"><span data-stu-id="6015c-104">By [Daniel Roth](https://github.com/danroth27), [Rick Anderson](https://twitter.com/RickAndMSFT), and [Shaun Luttin](https://twitter.com/dicshaunary)</span></span>

<span data-ttu-id="6015c-105">ASP.NET Core는 클라우드 기반 인터넷에 연결된 최신 응용 프로그램을 빌드하기 위한 플랫폼 간 고성능 [오픈 소스](https://github.com/aspnet/home) 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-105">ASP.NET Core is a cross-platform, high-performance, [open-source](https://github.com/aspnet/home) framework for building modern, cloud-based, Internet-connected applications.</span></span> <span data-ttu-id="6015c-106">ASP.NET Core를 사용하면 다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-106">With ASP.NET Core, you can:</span></span>

* <span data-ttu-id="6015c-107">웹앱 및 서비스, [IoT](https://www.microsoft.com/internet-of-things/) 앱 및 모바일 백 엔드를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-107">Build web apps and services, [IoT](https://www.microsoft.com/internet-of-things/) apps, and mobile backends.</span></span>
* <span data-ttu-id="6015c-108">Windows, macOS 및 Linux에서 즐겨 찾는 개발 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-108">Use your favorite development tools on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="6015c-109">클라우드 또는 온-프레미스에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-109">Deploy to the cloud or on-premises.</span></span>
* <span data-ttu-id="6015c-110">[.NET Core 또는.NET Framework](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-110">Run on [.NET Core or .NET Framework](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server).</span></span>

## <a name="why-use-aspnet-core"></a><span data-ttu-id="6015c-111">ASP.NET Core를 사용하는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="6015c-111">Why use ASP.NET Core?</span></span>

<span data-ttu-id="6015c-112">수백만 명의 개발자가 [ASP.NET 4.x](https://docs.microsoft.com/aspnet/overview)를 사용하여 웹앱을 만들었습니다(계속 사용 중).</span><span class="sxs-lookup"><span data-stu-id="6015c-112">Millions of developers have used (and continue to use) [ASP.NET 4.x](https://docs.microsoft.com/aspnet/overview) to create web apps.</span></span> <span data-ttu-id="6015c-113">ASP.NET Core는 간결한 모듈식 프레임워크를 만드는 아키텍처 변경 내용을 포함한 ASP.NET 4.x의 새로운 디자인입니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-113">ASP.NET Core is a redesign of ASP.NET 4.x, with architectural changes that result in a leaner, more modular framework.</span></span>

[!INCLUDE[](~/includes/benefits.md)]

## <a name="build-web-apis-and-web-ui-using-aspnet-core-mvc"></a><span data-ttu-id="6015c-114">ASP.NET Core MVC를 사용하여 웹 API 및 웹 UI 빌드</span><span class="sxs-lookup"><span data-stu-id="6015c-114">Build web APIs and web UI using ASP.NET Core MVC</span></span>

<span data-ttu-id="6015c-115">ASP.NET Core MVC에서는 [Web API](xref:tutorials/index#build-web-apis) 및 [웹앱](xref:tutorials/index#build-web-apps)을 빌드하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-115">ASP.NET Core MVC provides features to build [web APIs](xref:tutorials/index#build-web-apis) and [web apps](xref:tutorials/index#build-web-apps):</span></span>

* <span data-ttu-id="6015c-116">[MVC(모델-뷰-컨트롤러) 패턴](xref:mvc/overview)을 통해 웹 API 및 웹앱을 [테스트 가능](xref:test/index)하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-116">The [Model-View-Controller (MVC) pattern](xref:mvc/overview) helps make your web APIs and web apps [testable](xref:test/index).</span></span>
* <span data-ttu-id="6015c-117">[Razor 페이지](xref:razor-pages/index) (2.0의 새로운 기능)는 웹 UI를 쉽게 빌드하고 생산성을 높일 수 있는 페이지 기반 프로그래밍 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-117">[Razor Pages](xref:razor-pages/index) (new in ASP.NET Core 2.0) is a page-based programming model that makes building web UI easier and more productive.</span></span>
* <span data-ttu-id="6015c-118">[Razor 태그](xref:mvc/views/razor)는 [Razor 페이지](xref:razor-pages/index) 및 [MVC 뷰](xref:mvc/views/overview)에 생산적인 구문을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-118">[Razor markup](xref:mvc/views/razor) provides a productive syntax for [Razor Pages](xref:razor-pages/index) and [MVC views](xref:mvc/views/overview).</span></span>
* <span data-ttu-id="6015c-119">[태그 도우미](xref:mvc/views/tag-helpers/intro)를 사용하면 서버 쪽 코드를 Razor 파일에서 HTML 요소를 만들고 렌더링하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-119">[Tag Helpers](xref:mvc/views/tag-helpers/intro) enable server-side code to participate in creating and rendering HTML elements in Razor files.</span></span>
* <span data-ttu-id="6015c-120">[여러 데이터 형식 및 콘텐츠 협상](xref:web-api/advanced/formatting)에 대한 기본 제공 지원을 통해 웹 API를 브라우저 및 모바일 장치를 포함한 다양한 클라이언트에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-120">Built-in support for [multiple data formats and content negotiation](xref:web-api/advanced/formatting) lets your web APIs reach a broad range of clients, including browsers and mobile devices.</span></span>
* <span data-ttu-id="6015c-121">[모델 바인딩](xref:mvc/models/model-binding)은 작업 메서드 매개 변수에 HTTP 요청의 데이터를 자동으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-121">[Model binding](xref:mvc/models/model-binding) automatically maps data from HTTP requests to action method parameters.</span></span>
* <span data-ttu-id="6015c-122">[모델 유효성 검사](xref:mvc/models/validation)는 자동으로 클라이언트 쪽 및 서버 쪽 유효성 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-122">[Model validation](xref:mvc/models/validation) automatically performs client-side and server-side validation.</span></span>

## <a name="client-side-development"></a><span data-ttu-id="6015c-123">클라이언트 쪽 개발</span><span class="sxs-lookup"><span data-stu-id="6015c-123">Client-side development</span></span>

<span data-ttu-id="6015c-124">ASP.NET Core는 [Angular](xref:spa/angular), [React](xref:spa/react), [부트스트랩](https://getbootstrap.com/) 등 유명한 클라이언트 쪽 프레임워크 및 라이브러리와 원활하게 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-124">ASP.NET Core integrates seamlessly with popular client-side frameworks and libraries, including [Angular](xref:spa/angular), [React](xref:spa/react), and [Bootstrap](https://getbootstrap.com/).</span></span> <span data-ttu-id="6015c-125">자세한 내용은 [클라이언트 쪽 개발](xref:client-side/index)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6015c-125">For more information, see [Client-side development](xref:client-side/index).</span></span>

<a name="target-framework"></a>

## <a name="aspnet-core-targeting-net-framework"></a><span data-ttu-id="6015c-126">ASP.NET Core 대상 .NET Framework</span><span class="sxs-lookup"><span data-stu-id="6015c-126">ASP.NET Core targeting .NET Framework</span></span>

<span data-ttu-id="6015c-127">ASP.NET Core는 .NET Core 또는 .NET Framework를 대상으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-127">ASP.NET Core can target .NET Core or .NET Framework.</span></span> <span data-ttu-id="6015c-128">.NET Framework를 대상으로 지정한 ASP.NET Core 앱은 플랫폼 간 교차 사용이 불가능하며 &mdash;Windows에서만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-128">ASP.NET Core apps targeting .NET Framework aren't cross-platform&mdash;they run on Windows only.</span></span> <span data-ttu-id="6015c-129">ASP.NET Core에서 .NET Framework를 대상으로 지정에 대한 지원은 제거되지 않을 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-129">There are no plans to remove support for targeting .NET Framework in ASP.NET Core.</span></span> <span data-ttu-id="6015c-130">일반적으로 ASP.NET Core는 [.NET Standard](/dotnet/standard/net-standard) 라이브러리로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-130">Generally, ASP.NET Core is made up of [.NET Standard](/dotnet/standard/net-standard) libraries.</span></span> <span data-ttu-id="6015c-131">.NET Standard 2.0으로 작성된 앱은 .NET Standard 2.0이 지원되는 모든 위치에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-131">Apps written with .NET Standard 2.0 run anywhere that .NET Standard 2.0 is supported.</span></span>

<span data-ttu-id="6015c-132">ASP.NET Core 2.x는 .NET Standard 2.0과 호환되는 .NET Framework 버전에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-132">ASP.NET Core 2.x is supported on .NET Framework versions compatible with .NET Standard 2.0:</span></span>

* <span data-ttu-id="6015c-133">.NET Framework 4.7.1 이상이 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-133">.NET Framework 4.7.1 and later is strongly recommended.</span></span>
* <span data-ttu-id="6015c-134">.NET Framework 4.6.1 이상</span><span class="sxs-lookup"><span data-stu-id="6015c-134">.NET Framework 4.6.1 and later.</span></span>

<span data-ttu-id="6015c-135">.NET Core를 대상으로 지정하면 여러 이점이 있으며 이러한 장점은 릴리스마다 늘어나고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-135">There are several advantages to targeting .NET Core, and these advantages increase with each release.</span></span> <span data-ttu-id="6015c-136">.NET Framework에서 .NET Core의 몇 가지 장점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-136">Some advantages of .NET Core over .NET Framework include:</span></span>

* <span data-ttu-id="6015c-137">플랫폼 간 사용 가능.</span><span class="sxs-lookup"><span data-stu-id="6015c-137">Cross-platform.</span></span> <span data-ttu-id="6015c-138">macOS, Linux 및 Windows에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-138">Runs on macOS, Linux, and Windows.</span></span>
* <span data-ttu-id="6015c-139">향상된 성능</span><span class="sxs-lookup"><span data-stu-id="6015c-139">Improved performance</span></span>
* <span data-ttu-id="6015c-140">Side-by-side 버전 관리.</span><span class="sxs-lookup"><span data-stu-id="6015c-140">Side-by-side versioning</span></span>
* <span data-ttu-id="6015c-141">새로운 API</span><span class="sxs-lookup"><span data-stu-id="6015c-141">New APIs</span></span>
* <span data-ttu-id="6015c-142">소스 열기</span><span class="sxs-lookup"><span data-stu-id="6015c-142">Open source</span></span>

<span data-ttu-id="6015c-143">.NET Framework에서 .NET Core 사이의 API 차이를 줄이기 위해 최선을 다하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-143">We're working hard to close the API gap from .NET Framework to .NET Core.</span></span> <span data-ttu-id="6015c-144">[Windows 호환 팩](/dotnet/core/porting/windows-compat-pack)을 통해 수천 개의 Windows 전용 API를 .NET Core에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-144">The [Windows Compatibility Pack](/dotnet/core/porting/windows-compat-pack) made thousands of Windows-only APIs available in .NET Core.</span></span> <span data-ttu-id="6015c-145">이러한 API는 .NET Core 1.x에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-145">These APIs weren't available in .NET Core 1.x.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6015c-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6015c-146">Next steps</span></span>

<span data-ttu-id="6015c-147">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6015c-147">For more information, see the following resources:</span></span>

* [<span data-ttu-id="6015c-148">Razor 페이지 시작</span><span class="sxs-lookup"><span data-stu-id="6015c-148">Get started with Razor Pages</span></span>](xref:tutorials/razor-pages/razor-pages-start)
* [<span data-ttu-id="6015c-149">ASP.NET Core 자습서</span><span class="sxs-lookup"><span data-stu-id="6015c-149">ASP.NET Core tutorials</span></span>](xref:tutorials/index)
* <xref:tutorials/publish-to-azure-webapp-using-vs>
* [<span data-ttu-id="6015c-150">ASP.NET Core 기본 사항</span><span class="sxs-lookup"><span data-stu-id="6015c-150">ASP.NET Core fundamentals</span></span>](xref:fundamentals/index)
* <span data-ttu-id="6015c-151">[매주 ASP.NET 커뮤니티 스탠드업](https://live.asp.net/)은 팀의 진행률 및 계획을 다루고</span><span class="sxs-lookup"><span data-stu-id="6015c-151">[The weekly ASP.NET community standup](https://live.asp.net/) covers the team's progress and plans.</span></span> <span data-ttu-id="6015c-152">새 블로그 및 타사 소프트웨어를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6015c-152">It features new blogs and third-party software.</span></span>
