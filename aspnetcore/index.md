---
title: ASP.NET Core 소개
author: rick-anderson
description: 클라우드 기반 인터넷에 연결된 최신 응용 프로그램을 빌드하기 위한 플랫폼 간 고성능 오픈 소스 프레임워크인 ASP.NET Core에 대한 소개를 가져옵니다.
ms.author: riande
ms.custom: mvc
ms.date: 11/10/2018
uid: index
ms.openlocfilehash: 1699acc0086dfd50c573afc239bc8f37eb9e7af9
ms.sourcegitcommit: 408921a932448f66cb46fd53c307a864f5323fe5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51569990"
---
# <a name="introduction-to-aspnet-core"></a><span data-ttu-id="6a336-103">ASP.NET Core 소개</span><span class="sxs-lookup"><span data-stu-id="6a336-103">Introduction to ASP.NET Core</span></span>

<span data-ttu-id="6a336-104">작성자: [Daniel Roth](https://github.com/danroth27), [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Shaun Luttin](https://twitter.com/dicshaunary)</span><span class="sxs-lookup"><span data-stu-id="6a336-104">By [Daniel Roth](https://github.com/danroth27), [Rick Anderson](https://twitter.com/RickAndMSFT), and [Shaun Luttin](https://twitter.com/dicshaunary)</span></span>

<span data-ttu-id="6a336-105">ASP.NET Core는 클라우드 기반 인터넷에 연결된 최신 응용 프로그램을 빌드하기 위한 플랫폼 간 고성능 [오픈 소스](https://github.com/aspnet/home) 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-105">ASP.NET Core is a cross-platform, high-performance, [open-source](https://github.com/aspnet/home) framework for building modern, cloud-based, Internet-connected applications.</span></span> <span data-ttu-id="6a336-106">ASP.NET Core를 사용하면 다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-106">With ASP.NET Core, you can:</span></span>

* <span data-ttu-id="6a336-107">웹앱 및 서비스, [IoT](https://www.microsoft.com/internet-of-things/) 앱 및 모바일 백 엔드를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-107">Build web apps and services, [IoT](https://www.microsoft.com/internet-of-things/) apps, and mobile backends.</span></span>
* <span data-ttu-id="6a336-108">Windows, macOS 및 Linux에서 즐겨 찾는 개발 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-108">Use your favorite development tools on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="6a336-109">클라우드 또는 온-프레미스에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-109">Deploy to the cloud or on-premises.</span></span>
* <span data-ttu-id="6a336-110">[.NET Core 또는.NET Framework](/dotnet/articles/standard/choosing-core-framework-server)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-110">Run on [.NET Core or .NET Framework](/dotnet/articles/standard/choosing-core-framework-server).</span></span>

## <a name="why-use-aspnet-core"></a><span data-ttu-id="6a336-111">ASP.NET Core를 사용하는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="6a336-111">Why use ASP.NET Core?</span></span>

<span data-ttu-id="6a336-112">수백만 명의 개발자가 [ASP.NET 4.x](/aspnet/overview)를 사용하여 웹앱을 만들었습니다(계속 사용 중).</span><span class="sxs-lookup"><span data-stu-id="6a336-112">Millions of developers have used (and continue to use) [ASP.NET 4.x](/aspnet/overview) to create web apps.</span></span> <span data-ttu-id="6a336-113">ASP.NET Core는 간결한 모듈식 프레임워크를 만드는 아키텍처 변경 내용을 포함한 ASP.NET 4.x의 새로운 디자인입니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-113">ASP.NET Core is a redesign of ASP.NET 4.x, with architectural changes that result in a leaner, more modular framework.</span></span>

[!INCLUDE[](~/includes/benefits.md)]

## <a name="build-web-apis-and-web-ui-using-aspnet-core-mvc"></a><span data-ttu-id="6a336-114">ASP.NET Core MVC를 사용하여 웹 API 및 웹 UI 빌드</span><span class="sxs-lookup"><span data-stu-id="6a336-114">Build web APIs and web UI using ASP.NET Core MVC</span></span>

<span data-ttu-id="6a336-115">ASP.NET Core MVC에서는 [Web API](xref:tutorials/first-web-api) 및 [웹앱](xref:tutorials/razor-pages/index)을 빌드하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-115">ASP.NET Core MVC provides features to build [web APIs](xref:tutorials/first-web-api) and [web apps](xref:tutorials/razor-pages/index):</span></span>

* <span data-ttu-id="6a336-116">[MVC(모델-뷰-컨트롤러) 패턴](xref:mvc/overview)을 통해 웹 API 및 웹앱을 테스트 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-116">The [Model-View-Controller (MVC) pattern](xref:mvc/overview) helps make your web APIs and web apps testable.</span></span>
* <span data-ttu-id="6a336-117">[Razor 페이지](xref:razor-pages/index) (2.0의 새로운 기능)는 웹 UI를 쉽게 빌드하고 생산성을 높일 수 있는 페이지 기반 프로그래밍 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-117">[Razor Pages](xref:razor-pages/index) (new in ASP.NET Core 2.0) is a page-based programming model that makes building web UI easier and more productive.</span></span>
* <span data-ttu-id="6a336-118">[Razor 태그](xref:mvc/views/razor)는 [Razor 페이지](xref:razor-pages/index) 및 [MVC 뷰](xref:mvc/views/overview)에 생산적인 구문을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-118">[Razor markup](xref:mvc/views/razor) provides a productive syntax for [Razor Pages](xref:razor-pages/index) and [MVC views](xref:mvc/views/overview).</span></span>
* <span data-ttu-id="6a336-119">[태그 도우미](xref:mvc/views/tag-helpers/intro)를 사용하면 서버 쪽 코드를 Razor 파일에서 HTML 요소를 만들고 렌더링하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-119">[Tag Helpers](xref:mvc/views/tag-helpers/intro) enable server-side code to participate in creating and rendering HTML elements in Razor files.</span></span>
* <span data-ttu-id="6a336-120">[여러 데이터 형식 및 콘텐츠 협상](xref:web-api/advanced/formatting)에 대한 기본 제공 지원을 통해 웹 API를 브라우저 및 모바일 장치를 포함한 다양한 클라이언트에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-120">Built-in support for [multiple data formats and content negotiation](xref:web-api/advanced/formatting) lets your web APIs reach a broad range of clients, including browsers and mobile devices.</span></span>
* <span data-ttu-id="6a336-121">[모델 바인딩](xref:mvc/models/model-binding)은 작업 메서드 매개 변수에 HTTP 요청의 데이터를 자동으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-121">[Model binding](xref:mvc/models/model-binding) automatically maps data from HTTP requests to action method parameters.</span></span>
* <span data-ttu-id="6a336-122">[모델 유효성 검사](xref:mvc/models/validation)는 자동으로 클라이언트 쪽 및 서버 쪽 유효성 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-122">[Model validation](xref:mvc/models/validation) automatically performs client-side and server-side validation.</span></span>

## <a name="client-side-development"></a><span data-ttu-id="6a336-123">클라이언트 쪽 개발</span><span class="sxs-lookup"><span data-stu-id="6a336-123">Client-side development</span></span>

<span data-ttu-id="6a336-124">ASP.NET Core는 [Angular](xref:spa/angular), [React](xref:spa/react), [부트스트랩](https://getbootstrap.com/) 등 유명한 클라이언트 쪽 프레임워크 및 라이브러리와 원활하게 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-124">ASP.NET Core integrates seamlessly with popular client-side frameworks and libraries, including [Angular](xref:spa/angular), [React](xref:spa/react), and [Bootstrap](https://getbootstrap.com/).</span></span> <span data-ttu-id="6a336-125">자세한 내용은 [클라이언트 쪽 개발](xref:client-side/index)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a336-125">For more information, see [Client-side development](xref:client-side/index).</span></span>

<a name="target-framework"></a>

## <a name="aspnet-core-targeting-net-framework"></a><span data-ttu-id="6a336-126">ASP.NET Core 대상 .NET Framework</span><span class="sxs-lookup"><span data-stu-id="6a336-126">ASP.NET Core targeting .NET Framework</span></span>

<span data-ttu-id="6a336-127">ASP.NET Core 2.x는 .NET Core 또는 .NET Framework를 대상으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-127">ASP.NET Core 2.x can target .NET Core or .NET Framework.</span></span> <span data-ttu-id="6a336-128">.NET Framework를 대상으로 지정한 ASP.NET Core 앱은 플랫폼 간 교차 사용이 불가능하며 &mdash;Windows에서만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-128">ASP.NET Core apps targeting .NET Framework aren't cross-platform&mdash;they run on Windows only.</span></span> <span data-ttu-id="6a336-129">일반적으로 ASP.NET Core 2.x는 [.NET 표준](/dotnet/standard/net-standard) 라이브러리로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-129">Generally, ASP.NET Core 2.x is made up of [.NET Standard](/dotnet/standard/net-standard) libraries.</span></span> <span data-ttu-id="6a336-130">.NET Standard 2.0으로 작성된 앱은 .NET Standard 2.0이 지원되는 모든 위치에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-130">Apps written with .NET Standard 2.0 run anywhere that .NET Standard 2.0 is supported.</span></span>

<span data-ttu-id="6a336-131">ASP.NET Core 2.x는 .NET Standard 2.0과 호환되는 .NET Framework 버전에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-131">ASP.NET Core 2.x is supported on .NET Framework versions compatible with .NET Standard 2.0:</span></span>

* <span data-ttu-id="6a336-132">.NET Framework 4.7.1 이상이 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-132">.NET Framework 4.7.1 and later is strongly recommended.</span></span>
* <span data-ttu-id="6a336-133">.NET Framework 4.6.1 이상</span><span class="sxs-lookup"><span data-stu-id="6a336-133">.NET Framework 4.6.1 and later.</span></span>

<span data-ttu-id="6a336-134">ASP.NET Core 3.0 이상은 .NET Core에서만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-134">ASP.NET Core 3.0 and later will only run on .NET Core.</span></span> <span data-ttu-id="6a336-135">이 변경 사항에 대한 자세한 내용은 [ASP.NET Core 3.0에 도입되는 변경 사항 개요](https://blogs.msdn.microsoft.com/webdev/2018/10/29/a-first-look-at-changes-coming-in-asp-net-core-3-0/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a336-135">For more details regarding this change, see [A first look at changes coming in ASP.NET Core 3.0](https://blogs.msdn.microsoft.com/webdev/2018/10/29/a-first-look-at-changes-coming-in-asp-net-core-3-0/).</span></span>

<span data-ttu-id="6a336-136">.NET Core를 대상으로 지정하면 여러 이점이 있으며 이러한 장점은 릴리스마다 늘어나고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-136">There are several advantages to targeting .NET Core, and these advantages increase with each release.</span></span> <span data-ttu-id="6a336-137">.NET Framework에서 .NET Core의 몇 가지 장점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-137">Some advantages of .NET Core over .NET Framework include:</span></span>

* <span data-ttu-id="6a336-138">플랫폼 간 사용 가능.</span><span class="sxs-lookup"><span data-stu-id="6a336-138">Cross-platform.</span></span> <span data-ttu-id="6a336-139">macOS, Linux 및 Windows에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-139">Runs on macOS, Linux, and Windows.</span></span>
* <span data-ttu-id="6a336-140">향상된 성능</span><span class="sxs-lookup"><span data-stu-id="6a336-140">Improved performance</span></span>
* <span data-ttu-id="6a336-141">Side-by-side 버전 관리.</span><span class="sxs-lookup"><span data-stu-id="6a336-141">Side-by-side versioning</span></span>
* <span data-ttu-id="6a336-142">새로운 API</span><span class="sxs-lookup"><span data-stu-id="6a336-142">New APIs</span></span>
* <span data-ttu-id="6a336-143">소스 열기</span><span class="sxs-lookup"><span data-stu-id="6a336-143">Open source</span></span>

<span data-ttu-id="6a336-144">.NET Framework에서 .NET Core 사이의 API 차이를 줄이기 위해 최선을 다하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-144">We're working hard to close the API gap from .NET Framework to .NET Core.</span></span> <span data-ttu-id="6a336-145">[Windows 호환 팩](/dotnet/core/porting/windows-compat-pack)을 통해 수천 개의 Windows 전용 API를 .NET Core에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-145">The [Windows Compatibility Pack](/dotnet/core/porting/windows-compat-pack) made thousands of Windows-only APIs available in .NET Core.</span></span> <span data-ttu-id="6a336-146">이러한 API는 .NET Core 1.x에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-146">These APIs weren't available in .NET Core 1.x.</span></span>

## <a name="how-to-download-a-sample"></a><span data-ttu-id="6a336-147">샘플 다운로드 방법</span><span class="sxs-lookup"><span data-stu-id="6a336-147">How to download a sample</span></span>

<span data-ttu-id="6a336-148">대부분의 문서 및 자습서에는 샘플 코드에 대한 링크가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-148">Many of the articles and tutorials include links to sample code.</span></span>

1. <span data-ttu-id="6a336-149">[ASP.NET 리포지토리 zip 파일을 다운로드합니다](https://codeload.github.com/aspnet/Docs/zip/master).</span><span class="sxs-lookup"><span data-stu-id="6a336-149">[Download the ASP.NET repository zip file](https://codeload.github.com/aspnet/Docs/zip/master).</span></span>
1. <span data-ttu-id="6a336-150">*Docs-master.zip* 파일의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-150">Unzip the *Docs-master.zip* file.</span></span>
1. <span data-ttu-id="6a336-151">샘플 링크의 URL을 사용하여 샘플 디렉터리로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-151">Use the URL in the sample link to help you navigate to the sample directory.</span></span>

<span data-ttu-id="6a336-152">여러 시나리오를 보여주기 위해 샘플 앱은 `#define` 및 `#if-#else/#elif-#endif` C# 문을 사용하여 샘플 코드의 다양한 섹션을 선택적으로 컴파일하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-152">To demonstrate multiple scenarios, sample apps make use of the `#define` and `#if-#else/#elif-#endif` C# statements to selectively compile and run different sections of sample code.</span></span> <span data-ttu-id="6a336-153">이 방법을 사용하는 해당 샘플의 경우 C# 파일 상단에 있는 `#define` 문을 실행할 시나리오와 연결된 기호로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-153">For those samples that make use of this approach, set the `#define` statement at the top of the C# files to the symbol associated with the scenario that you want to run.</span></span> <span data-ttu-id="6a336-154">시나리오를 실행하려면 샘플에서 여러 파일의 맨 위에 기호를 설정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-154">A sample may require you to set the symbol at the top of multiple files in order to run a scenario.</span></span>

<span data-ttu-id="6a336-155">예를 들어, 다음 `#define` 기호 목록은 네 가지 시나리오를 사용할 수 있음을 나타냅니다(기호당 하나의 시나리오).</span><span class="sxs-lookup"><span data-stu-id="6a336-155">For example, the following `#define` symbol list indicates that four scenarios are available (one scenario per symbol).</span></span> <span data-ttu-id="6a336-156">현재 샘플 구성에서는 `TemplateCode` 시나리오를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-156">The current sample configuration runs the `TemplateCode` scenario:</span></span>

```csharp
#define TemplateCode // or LogFromMain or ExpandDefault or FilterInCode
```

<span data-ttu-id="6a336-157">`ExpandDefault` 시나리오를 실행하도록 샘플을 변경하려면 `ExpandDefault` 기호를 정의하고 나머지 기호는 주석으로 처리하세요.</span><span class="sxs-lookup"><span data-stu-id="6a336-157">To change the sample to run the `ExpandDefault` scenario, define the `ExpandDefault` symbol and leave the remaining symbols commented-out:</span></span>

```csharp
#define ExpandDefault // TemplateCode or LogFromMain or FilterInCode
```

<span data-ttu-id="6a336-158">[C# 전 처리기 지시문](/dotnet/csharp/language-reference/preprocessor-directives/)을 사용하여 코드 섹션을 선택적으로 컴파일하는 방법에 대한 자세한 내용은 [#define(C# 참조)](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-define) 및 [#if(C# 참조)](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-if)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a336-158">For more information on using [C# preprocessor directives](/dotnet/csharp/language-reference/preprocessor-directives/) to selectively compile sections of code, see [#define (C# Reference)](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-define) and [#if (C# Reference)](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-if).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a336-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6a336-159">Next steps</span></span>

<span data-ttu-id="6a336-160">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6a336-160">For more information, see the following resources:</span></span>

* [<span data-ttu-id="6a336-161">Razor 페이지 시작</span><span class="sxs-lookup"><span data-stu-id="6a336-161">Get started with Razor Pages</span></span>](xref:tutorials/razor-pages/razor-pages-start)
* <xref:tutorials/publish-to-azure-webapp-using-vs>
* [<span data-ttu-id="6a336-162">ASP.NET Core 기본 사항</span><span class="sxs-lookup"><span data-stu-id="6a336-162">ASP.NET Core fundamentals</span></span>](xref:fundamentals/index)
* <span data-ttu-id="6a336-163">[매주 ASP.NET 커뮤니티 스탠드업](https://live.asp.net/)은 팀의 진행률 및 계획을 다루고</span><span class="sxs-lookup"><span data-stu-id="6a336-163">[The weekly ASP.NET community standup](https://live.asp.net/) covers the team's progress and plans.</span></span> <span data-ttu-id="6a336-164">새 블로그 및 타사 소프트웨어를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6a336-164">It features new blogs and third-party software.</span></span>
