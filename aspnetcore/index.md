---
title: "ASP.NET Core 소개"
author: rick-anderson
description: "ASP.NET Core를 소개합니다."
manager: wpickett
ms.author: riande
ms.date: 12/12/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: index
ms.openlocfilehash: d7957bdc6fa982790141bac9b73ad7d3b1dd3d8a
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="introduction-to-aspnet-core"></a><span data-ttu-id="4edf1-103">ASP.NET Core 소개</span><span class="sxs-lookup"><span data-stu-id="4edf1-103">Introduction to ASP.NET Core</span></span>

<span data-ttu-id="4edf1-104">작성자: [Daniel Roth](https://github.com/danroth27), [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Shaun Luttin](https://twitter.com/dicshaunary)</span><span class="sxs-lookup"><span data-stu-id="4edf1-104">By [Daniel Roth](https://github.com/danroth27), [Rick Anderson](https://twitter.com/RickAndMSFT), and [Shaun Luttin](https://twitter.com/dicshaunary)</span></span>

<span data-ttu-id="4edf1-105">ASP.NET Core는 클라우드 기반 인터넷에 연결된 최신 응용 프로그램을 빌드하기 위한 플랫폼 간 고성능 [오픈 소스](https://github.com/aspnet/home) 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-105">ASP.NET Core is a cross-platform, high-performance, [open-source](https://github.com/aspnet/home) framework for building modern, cloud-based, Internet-connected applications.</span></span> <span data-ttu-id="4edf1-106">ASP.NET Core를 사용하면 다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-106">With ASP.NET Core, you can:</span></span>

* <span data-ttu-id="4edf1-107">웹앱 및 서비스, [IoT](https://www.microsoft.com/internet-of-things/) 앱 및 모바일 백 엔드를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-107">Build web apps and services, [IoT](https://www.microsoft.com/internet-of-things/) apps, and mobile backends.</span></span>
* <span data-ttu-id="4edf1-108">Windows, macOS 및 Linux에서 즐겨 찾는 개발 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-108">Use your favorite development tools on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="4edf1-109">클라우드 또는 온-프레미스에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-109">Deploy to the cloud or on-premises.</span></span>
* <span data-ttu-id="4edf1-110">[.NET Core 또는.NET Framework](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-110">Run on [.NET Core or .NET Framework](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server).</span></span>

## <a name="why-use-aspnet-core"></a><span data-ttu-id="4edf1-111">ASP.NET Core를 사용하는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="4edf1-111">Why use ASP.NET Core?</span></span>

<span data-ttu-id="4edf1-112">수백만 명의 개발자가 [ASP.NET 4.x](https://docs.microsoft.com/aspnet/overview)를 사용하여 웹앱을 만들었습니다(계속 사용 중).</span><span class="sxs-lookup"><span data-stu-id="4edf1-112">Millions of developers have used (and continue to use) [ASP.NET 4.x](https://docs.microsoft.com/aspnet/overview) to create web apps.</span></span> <span data-ttu-id="4edf1-113">ASP.NET Core는 간결한 모듈식 프레임워크를 만드는 아키텍처 변경 내용을 포함한 ASP.NET 4.x의 새로운 디자인입니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-113">ASP.NET Core is a redesign of ASP.NET 4.x, with architectural changes that result in a leaner, more modular framework.</span></span>

<span data-ttu-id="4edf1-114">ASP.NET Core는 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-114">ASP.NET Core provides the following benefits:</span></span>

* <span data-ttu-id="4edf1-115">웹 UI 및 웹 API를 동일한 과정으로 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-115">A unified story for building web UI and web APIs.</span></span>
* <span data-ttu-id="4edf1-116">[최신 클라이언트 쪽 프레임워크](xref:client-side/index) 및 워크플로 개발을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-116">Integration of [modern, client-side frameworks](xref:client-side/index) and development workflows.</span></span>
* <span data-ttu-id="4edf1-117">클라우드를 갖춘 환경 기반 [구성 시스템](xref:fundamentals/configuration/index)입니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-117">A cloud-ready, environment-based [configuration system](xref:fundamentals/configuration/index).</span></span>
* <span data-ttu-id="4edf1-118">[종속성 주입](xref:fundamentals/dependency-injection)이 기본 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-118">Built-in [dependency injection](xref:fundamentals/dependency-injection).</span></span>
* <span data-ttu-id="4edf1-119">간단한 [고성능](https://github.com/aspnet/benchmarks) 모듈식 HTTP 요청 파이프라인을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-119">A lightweight, [high-performance](https://github.com/aspnet/benchmarks), and modular HTTP request pipeline.</span></span>
* <span data-ttu-id="4edf1-120">[IIS](xref:host-and-deploy/iis/index), [Nginx](xref:host-and-deploy/linux-nginx), [Apache](xref:host-and-deploy/linux-apache), [Docker](xref:host-and-deploy/docker/index)에서 호스트하거나 고유한 프로세스에서 자체 호스트하는 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-120">Ability to host on [IIS](xref:host-and-deploy/iis/index), [Nginx](xref:host-and-deploy/linux-nginx), [Apache](xref:host-and-deploy/linux-apache), [Docker](xref:host-and-deploy/docker/index), or self-host in your own process.</span></span>
* <span data-ttu-id="4edf1-121">[.NET Core](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server)를 대상으로 하는 경우 앱 버전을 함께 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-121">Side-by-side app versioning when targeting [.NET Core](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server).</span></span>
* <span data-ttu-id="4edf1-122">최신 웹 개발을 간소화하는 도구를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-122">Tooling that simplifies modern web development.</span></span>
* <span data-ttu-id="4edf1-123">Windows, macOS 및 Linux에서 빌드하고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-123">Ability to build and run on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="4edf1-124">오픈 소스이며 [커뮤니티에 중점](https://live.asp.net/)을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-124">Open-source and [community-focused](https://live.asp.net/).</span></span>

<span data-ttu-id="4edf1-125">ASP.NET Core는 완전히 [NuGet](https://www.nuget.org/) 패키지로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-125">ASP.NET Core ships entirely as [NuGet](https://www.nuget.org/) packages.</span></span> <span data-ttu-id="4edf1-126">그러면 필요한 NuGet 패키지만 포함하도록 앱을 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-126">This allows you to optimize your app to include only the necessary NuGet packages.</span></span> <span data-ttu-id="4edf1-127">실제로 .NET Core를 대상으로 하는 ASP.NET Core 2.x 앱에는 [단일 NuGet 패키지](xref:fundamentals/metapackage)만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-127">In fact, ASP.NET Core 2.x apps targeting .NET Core only require a [single NuGet package](xref:fundamentals/metapackage).</span></span> <span data-ttu-id="4edf1-128">작은 앱 노출 영역의 혜택에는 보안 강화, 서비스 절감, 성능 향상이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-128">The benefits of a smaller app surface area include tighter security, reduced servicing, and improved performance.</span></span>

## <a name="build-web-apis-and-web-ui-using-aspnet-core-mvc"></a><span data-ttu-id="4edf1-129">ASP.NET Core MVC를 사용하여 웹 API 및 웹 UI 빌드</span><span class="sxs-lookup"><span data-stu-id="4edf1-129">Build web APIs and web UI using ASP.NET Core MVC</span></span>

<span data-ttu-id="4edf1-130">ASP.NET Core MVC에서는 [Web API](xref:tutorials/index#build-web-apis) 및 [웹앱](xref:tutorials/index#build-web-apps)을 빌드하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-130">ASP.NET Core MVC provides features to build [web APIs](xref:tutorials/index#build-web-apis) and [web apps](xref:tutorials/index#build-web-apps):</span></span>

* <span data-ttu-id="4edf1-131">[MVC(모델-뷰-컨트롤러) 패턴](xref:mvc/overview)을 통해 웹 API 및 웹앱을 [테스트 가능](testing/index.md)하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-131">The [Model-View-Controller (MVC) pattern](xref:mvc/overview) helps make your web APIs and web apps [testable](testing/index.md).</span></span>
* <span data-ttu-id="4edf1-132">[Razor 페이지](xref:mvc/razor-pages/index)(ASP.NET Core 2.0의 새로운 기능)는 웹 UI를 쉽게 빌드하고 생산성을 높일 수 있는 페이지 기반 프로그래밍 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-132">[Razor Pages](xref:mvc/razor-pages/index) (new in ASP.NET Core 2.0) is a page-based programming model that makes building web UI easier and more productive.</span></span>
* <span data-ttu-id="4edf1-133">[Razor 태그](xref:mvc/views/razor)는 [Razor 페이지](xref:mvc/razor-pages/index) 및 [MVC 뷰](xref:mvc/views/overview)에 생산적인 구문을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-133">[Razor markup](xref:mvc/views/razor) provides a productive syntax for [Razor Pages](xref:mvc/razor-pages/index) and [MVC views](xref:mvc/views/overview).</span></span>
* <span data-ttu-id="4edf1-134">[태그 도우미](xref:mvc/views/tag-helpers/intro)를 사용하면 서버 쪽 코드를 Razor 파일에서 HTML 요소를 만들고 렌더링하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-134">[Tag Helpers](xref:mvc/views/tag-helpers/intro) enable server-side code to participate in creating and rendering HTML elements in Razor files.</span></span>
* <span data-ttu-id="4edf1-135">[여러 데이터 형식 및 콘텐츠 협상](mvc/models/formatting.md)에 대한 기본 제공 지원을 통해 웹 API를 브라우저 및 모바일 장치를 포함한 다양한 클라이언트에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-135">Built-in support for [multiple data formats and content negotiation](mvc/models/formatting.md) lets your web APIs reach a broad range of clients, including browsers and mobile devices.</span></span>
* <span data-ttu-id="4edf1-136">[모델 바인딩](xref:mvc/models/model-binding)은 작업 메서드 매개 변수에 HTTP 요청의 데이터를 자동으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-136">[Model binding](xref:mvc/models/model-binding) automatically maps data from HTTP requests to action method parameters.</span></span>
* <span data-ttu-id="4edf1-137">[유효성 검사 모델](xref:mvc/models/validation)은 자동으로 클라이언트와 서버 쪽 유효성 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-137">[Model validation](xref:mvc/models/validation) automatically performs client- and server-side validation.</span></span>

## <a name="client-side-development"></a><span data-ttu-id="4edf1-138">클라이언트 쪽 개발</span><span class="sxs-lookup"><span data-stu-id="4edf1-138">Client-side development</span></span>

<span data-ttu-id="4edf1-139">ASP.NET Core는 [Angular](xref:spa/angular), [React](xref:spa/react), [부트스트랩](xref:client-side/bootstrap) 등 유명한 클라이언트 쪽 프레임워크 및 라이브러리와 원활하게 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-139">ASP.NET Core integrates seamlessly with popular client-side frameworks and libraries, including [Angular](xref:spa/angular), [React](xref:spa/react), and [Bootstrap](xref:client-side/bootstrap).</span></span> <span data-ttu-id="4edf1-140">자세한 내용은 [클라이언트 쪽 개발](xref:client-side/index)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4edf1-140">See [Client-side development](xref:client-side/index) for more details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4edf1-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4edf1-141">Next steps</span></span>

<span data-ttu-id="4edf1-142">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4edf1-142">For more information, see the following resources:</span></span>

* [<span data-ttu-id="4edf1-143">ASP.NET Core 자습서</span><span class="sxs-lookup"><span data-stu-id="4edf1-143">ASP.NET Core tutorials</span></span>](xref:tutorials/index)
* [<span data-ttu-id="4edf1-144">ASP.NET Core 기본 사항</span><span class="sxs-lookup"><span data-stu-id="4edf1-144">ASP.NET Core fundamentals</span></span>](xref:fundamentals/index)
* <span data-ttu-id="4edf1-145">[매주 ASP.NET 커뮤니티 스탠드업](https://live.asp.net/)은 팀의 진행률 및 계획을 다루고</span><span class="sxs-lookup"><span data-stu-id="4edf1-145">[The weekly ASP.NET community standup](https://live.asp.net/) covers the team's progress and plans.</span></span> <span data-ttu-id="4edf1-146">새 블로그 및 타사 소프트웨어를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4edf1-146">It features new blogs and third-party software.</span></span>
