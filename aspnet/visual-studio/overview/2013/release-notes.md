---
uid: visual-studio/overview/2013/release-notes
title: "ASP.NET 및 Web Tools for Visual Studio 2013 릴리스 정보 | Microsoft Docs"
author: microsoft
description: "이 문서에서는 Visual Studio 2013 용 ASP.NET 및 웹 도구 릴리스를 설명 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: 10835c39d3bca752ed3068a23fecaaab56449e41
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a><span data-ttu-id="0eaf7-103">ASP.NET 및 Web Tools for Visual Studio 2013 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="0eaf7-103">ASP.NET and Web Tools for Visual Studio 2013 Release Notes</span></span>
====================
<span data-ttu-id="0eaf7-104">여 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="0eaf7-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="0eaf7-105">이 문서에서는 Visual Studio 2013 용 ASP.NET 및 웹 도구 릴리스를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-105">This document describes the release of ASP.NET and Web Tools for Visual Studio 2013.</span></span>


## <a name="contents"></a><span data-ttu-id="0eaf7-106">목차</span><span class="sxs-lookup"><span data-stu-id="0eaf7-106">Contents</span></span>

- [<span data-ttu-id="0eaf7-107">설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="0eaf7-107">Installation Notes</span></span>](#TOC1)
- [<span data-ttu-id="0eaf7-108">문서</span><span class="sxs-lookup"><span data-stu-id="0eaf7-108">Documentation</span></span>](#TOC2)
- [<span data-ttu-id="0eaf7-109">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="0eaf7-109">Software Requirements</span></span>](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="0eaf7-110">ASP.NET 및 Web Tools for Visual Studio 2013의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="0eaf7-110">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

- [<span data-ttu-id="0eaf7-111">One ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0eaf7-111">One ASP.NET</span></span>](#TOC6)
- [<span data-ttu-id="0eaf7-112">새 웹 프로젝트 경험</span><span class="sxs-lookup"><span data-stu-id="0eaf7-112">New Web Project Experience</span></span>](#newproj)
- [<span data-ttu-id="0eaf7-113">ASP.NET 스 캐 폴딩</span><span class="sxs-lookup"><span data-stu-id="0eaf7-113">ASP.NET Scaffolding</span></span>](#scaffold)
- [<span data-ttu-id="0eaf7-114">브라우저 링크</span><span class="sxs-lookup"><span data-stu-id="0eaf7-114">Browser Link</span></span>](#browser-link)
- [<span data-ttu-id="0eaf7-115">Visual Studio 웹 편집기의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="0eaf7-115">Visual Studio Web Editor Enhancements</span></span>](#web-editor)
- [<span data-ttu-id="0eaf7-116">Visual Studio에서 azure 앱 서비스 웹 앱 지원</span><span class="sxs-lookup"><span data-stu-id="0eaf7-116">Azure App Service Web Apps Support in Visual Studio</span></span>](#waws)
- [<span data-ttu-id="0eaf7-117">향상 된 기능으로 웹 게시</span><span class="sxs-lookup"><span data-stu-id="0eaf7-117">Web Publish Enhancements</span></span>](#publish)
- [<span data-ttu-id="0eaf7-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="0eaf7-118">NuGet 2.7</span></span>](#nuget)
- [<span data-ttu-id="0eaf7-119">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="0eaf7-119">ASP.NET Web Forms</span></span>](#TOC9)
- [<span data-ttu-id="0eaf7-120">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="0eaf7-120">ASP.NET MVC 5</span></span>](#TOC10)
- [<span data-ttu-id="0eaf7-121">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="0eaf7-121">ASP.NET Web API 2</span></span>](#TOC11)
- [<span data-ttu-id="0eaf7-122">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="0eaf7-122">ASP.NET SignalR</span></span>](#TOC13)
- [<span data-ttu-id="0eaf7-123">ASP.NET Id</span><span class="sxs-lookup"><span data-stu-id="0eaf7-123">ASP.NET Identity</span></span>](#TOC8)
- [<span data-ttu-id="0eaf7-124">Microsoft OWIN 구성 요소</span><span class="sxs-lookup"><span data-stu-id="0eaf7-124">Microsoft OWIN Components</span></span>](#TOC7)
- [<span data-ttu-id="0eaf7-125">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="0eaf7-125">Entity Framework 6</span></span>](#ef6)
- [<span data-ttu-id="0eaf7-126">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="0eaf7-126">ASP.NET Razor 3</span></span>](#TOC14)
- [<span data-ttu-id="0eaf7-127">ASP.NET 앱 일시 중단</span><span class="sxs-lookup"><span data-stu-id="0eaf7-127">ASP.NET App Suspend</span></span>](#TOC15)
- [<span data-ttu-id="0eaf7-128">알려진된 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="0eaf7-128">Known Issues and Breaking Changes</span></span>](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a><span data-ttu-id="0eaf7-129">설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="0eaf7-129">Installation Notes</span></span>

<span data-ttu-id="0eaf7-130">ASP.NET 및 Web Tools for Visual Studio 2013 주요 설치 관리자에 제공 되어 있으며 다운로드할 수 있습니다 [여기](https://www.asp.net/downloads)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-130">ASP.NET and Web Tools for Visual Studio 2013 are bundled in the main installer and can be downloaded [here](https://www.asp.net/downloads).</span></span>

<a id="TOC2"></a>
## <a name="documentation"></a><span data-ttu-id="0eaf7-131">설명서</span><span class="sxs-lookup"><span data-stu-id="0eaf7-131">Documentation</span></span>

<span data-ttu-id="0eaf7-132">사용할 수 있는 자습서 및 Visual Studio 2013 용 ASP.NET 및 Web Tools에 대 한 기타 정보는 [ASP.NET 웹 사이트](https://www.asp.net/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-132">Tutorials and other information about ASP.NET and Web Tools for Visual Studio 2013 are available from the [ASP.NET web site](https://www.asp.net/).</span></span>

<a id="TOC4"></a>
## <a name="software-requirements"></a><span data-ttu-id="0eaf7-133">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="0eaf7-133">Software Requirements</span></span>

<span data-ttu-id="0eaf7-134">ASP.NET 및 Web Tools는 Visual Studio 2013 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-134">ASP.NET and Web Tools requires Visual Studio 2013.</span></span>

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="0eaf7-135">ASP.NET 및 Web Tools for Visual Studio 2013의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="0eaf7-135">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

<span data-ttu-id="0eaf7-136">다음 섹션에서는 릴리스에서 도입 된 기능을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-136">The following sections describe the features that have been introduced in the release.</span></span>

<a id="TOC6"></a>
## <a name="one-aspnet"></a><span data-ttu-id="0eaf7-137">One ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0eaf7-137">One ASP.NET</span></span>

<span data-ttu-id="0eaf7-138">Visual Studio 2013의 릴리스로 쉽게을 혼합 하 고 사용자가 원하는 일치 수 있도록 ASP.NET 기술을 사용 경험을 통합 하기 위한 단계를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-138">With the release of Visual Studio 2013, we have taken a step towards unifying the experience of using ASP.NET technologies, so that you can easily mix and match the ones you want.</span></span> <span data-ttu-id="0eaf7-139">예를 들어 수 MVC를 사용 하 여 프로젝트를 시작할와 쉽게 나중에 프로젝트를 Web Forms 페이지를 추가 또는 Web Api Web Forms 프로젝트에 스 캐 폴드 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-139">For example, you can start a project using MVC and easily add Web Forms pages to the project later, or scaffold Web APIs in a Web Forms project.</span></span> <span data-ttu-id="0eaf7-140">One ASP.NET 모두 쉽게을 ASP.NET에서 선호 하는 작업을 수행 하려면 개발자는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-140">One ASP.NET is all about making it easier for you as a developer to do the things you love in ASP.NET.</span></span> <span data-ttu-id="0eaf7-141">선택한 기술은에 관계 없이 하나의 ASP.NET의 신뢰할 수 있는 기본 프레임 워크에서 작성할 수 있도록 한다는 확신을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-141">No matter what technology you choose, you can have confidence that you are building on the trusted underlying framework of One ASP.NET.</span></span>

<a id="newproj"></a>
## <a name="new-web-project-experience"></a><span data-ttu-id="0eaf7-142">새 웹 프로젝트 경험</span><span class="sxs-lookup"><span data-stu-id="0eaf7-142">New Web Project Experience</span></span>

<span data-ttu-id="0eaf7-143">Visual Studio 2013에서 새 웹 프로젝트를 만드는 환경과 향상 된 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-143">We have enhanced the experience of creating new web projects in Visual Studio 2013.</span></span> <span data-ttu-id="0eaf7-144">에 **새 ASP.NET 웹 프로젝트** 대화 원하는, 어떠한 조합의 기술 (Web Forms, MVC, Web API)를 구성 하 고, 인증 옵션을 구성 단위 테스트 프로젝트를 추가 프로젝트 유형을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-144">In the **New ASP.NET Web Project** dialog you can select the project type you want, configure any combination of technologies (Web Forms, MVC, Web API), configure authentication options, and add a unit test project.</span></span>

![새 ASP.NET 프로젝트](release-notes/_static/image1.png)

<span data-ttu-id="0eaf7-146">새 대화 상자를 사용 하는 템플릿 중 대부분에 대 한 기본 인증 옵션을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-146">The new dialog enables you to change the default authentication options for many of the templates.</span></span> <span data-ttu-id="0eaf7-147">예를 들어, ASP.NET Web Forms 프로젝트를 만들 때 다음 옵션 중 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-147">For example, when you create an ASP.NET Web Forms project you can select any of the following options:</span></span>

- <span data-ttu-id="0eaf7-148">인증 안 함</span><span class="sxs-lookup"><span data-stu-id="0eaf7-148">No Authentication</span></span>
- <span data-ttu-id="0eaf7-149">개별 사용자 계정 (ASP.NET 멤버 자격 또는 소셜 공급자 로그에서)</span><span class="sxs-lookup"><span data-stu-id="0eaf7-149">Individual User Accounts (ASP.NET membership or social provider log in)</span></span>
- <span data-ttu-id="0eaf7-150">조직 계정 (인터넷 응용 프로그램에 Active Directory)</span><span class="sxs-lookup"><span data-stu-id="0eaf7-150">Organizational Accounts (Active Directory in an internet application)</span></span>
- <span data-ttu-id="0eaf7-151">Windows 인증 (인트라넷 응용 프로그램에서 Active Directory)</span><span class="sxs-lookup"><span data-stu-id="0eaf7-151">Windows Authentication (Active Directory in an intranet application)</span></span>

![인증 옵션](release-notes/_static/image2.png)

<span data-ttu-id="0eaf7-153">웹 프로젝트를 만들기 위한 새 프로세스에 대 한 자세한 내용은 참조 [Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기](creating-web-projects-in-visual-studio.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-153">For more information about the new process for creating web projects, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span> <span data-ttu-id="0eaf7-154">새 인증 옵션에 대 한 자세한 내용은 참조 [ASP.NET Identity](#TOC8) 이 문서의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-154">For more information about the new authentication options, see [ASP.NET Identity](#TOC8) later in this document.</span></span>

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a><span data-ttu-id="0eaf7-155">ASP.NET 스 캐 폴딩</span><span class="sxs-lookup"><span data-stu-id="0eaf7-155">ASP.NET Scaffolding</span></span>

<span data-ttu-id="0eaf7-156">ASP.NET 스 캐 폴딩 ASP.NET 웹 응용 프로그램에 대 한 코드 생성 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-156">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="0eaf7-157">쉽게 데이터 모델과 상호 작용 하는 프로젝트에 상용구 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-157">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="0eaf7-158">이전 버전의 Visual Studio를 스 캐 폴딩 ASP.NET MVC 프로젝트에 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-158">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="0eaf7-159">Visual Studio 2013, Web Forms를 포함 하 여 모든 ASP.NET 프로젝트에 대 한 스 캐 폴딩을 지금 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-159">With Visual Studio 2013, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="0eaf7-160">Visual Studio 2013 생성 페이지 Web Forms 프로젝트에 대 한 현재 지원 하지 않는 있지만 프로젝트에 MVC 종속성을 추가 하 여 스 캐 폴딩 Web Forms를 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-160">Visual Studio 2013 does not currently support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="0eaf7-161">Web forms 페이지를 생성 하는 것에 대 한 지원이 향후 업데이트에서 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-161">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="0eaf7-162">스 캐 폴딩을 사용할 때 필요한 모든 프로젝트에 종속성이 설치 되어을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-162">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="0eaf7-163">예를 들어, ASP.NET Web Forms 프로젝트와 함께 시작 하 고 다음 스 캐 폴딩을 사용 하 여 웹 API 컨트롤러를 추가 하려면 필요한 NuGet 패키지와 참조를 프로젝트에 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-163">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="0eaf7-164">MVC 스 캐 폴딩 Web Forms 프로젝트를 추가 하려면 추가 **스 캐 폴드 된 새 항목** 선택 **MVC 5 종속성** 대화 상자 창에서.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-164">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="0eaf7-165">MVC; 스 캐 폴딩에 대 한 다음과 같은 최소이 고 전체.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-165">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="0eaf7-166">최소을 선택 하면 NuGet 패키지와 ASP.NET MVC에 대 한 참조가 프로젝트에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-166">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="0eaf7-167">전체 옵션을 선택 하는 경우 MVC 프로젝트에 필요한 콘텐츠 파일 뿐만 아니라 최소한의 종속성 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-167">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="0eaf7-168">비동기 컨트롤러를 스 캐 폴딩에 대 한 지원 Entity Framework 6의 새로운 비동기 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-168">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="0eaf7-169">자세한 내용과 자습서에 대 한 참조 [ASP.NET 스 캐 폴딩 개요](aspnet-scaffolding-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-169">For more information and tutorials, see [ASP.NET Scaffolding Overview](aspnet-scaffolding-overview.md).</span></span>

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a><span data-ttu-id="0eaf7-170">브라우저 링크-브라우저와 Visual Studio 간의 SignalR 채널</span><span class="sxs-lookup"><span data-stu-id="0eaf7-170">Browser Link – SignalR channel between browser and Visual Studio</span></span>

<span data-ttu-id="0eaf7-171">새 [브라우저 링크](using-browser-link.md) 를 통해 Visual Studio에 여러 브라우저를 연결 하 고 도구 모음에서 단추를 클릭 하 여 모든 고쳐지므로 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-171">The new [Browser Link](using-browser-link.md) feature lets you connect multiple browsers to Visual Studio and refresh them all by clicking a button in the toolbar.</span></span> <span data-ttu-id="0eaf7-172">모바일 에뮬레이터를 비롯 하 여 개발 사이트에 여러 브라우저를 연결할 수 있고 동시에 모두 있는 모든 브라우저 새로 고침에 새로 고침을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-172">You can connect multiple browsers to your development site, including mobile emulators, and click refresh to refresh all the browsers all at the same time.</span></span> <span data-ttu-id="0eaf7-173">브라우저 링크는 또한 개발자 브라우저 링크 확장을 작성할 수 있도록 API를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-173">Browser Link also exposes an API to enable developers to write Browser Link extensions.</span></span>

![](release-notes/_static/image3.png)

<span data-ttu-id="0eaf7-174">브라우저 링크 API를 활용 하는 개발자를 활성화 하 여 Visual Studio와 연결 된 모든 브라우저 간의 경계를 교차 하는 고급 시나리오를 만들 수 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-174">By enabling developers to take advantage of the Browser Link API, it becomes possible to create very advanced scenarios that crosses boundaries between Visual Studio and any browser that's connected.</span></span> <span data-ttu-id="0eaf7-175">웹 Essentials에서는 Visual Studio 및 브라우저의 개발자 도구, 모바일 에뮬레이터 및 더 많은 제어 원격 간에 통합된 된 환경을 만들려면 API 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-175">Web Essentials takes advantage of the API to create an integrated experience between Visual Studio and the browser's developer tools, remote controlling mobile emulators and a lot more.</span></span>

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a><span data-ttu-id="0eaf7-176">Visual Studio 웹 편집기의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="0eaf7-176">Visual Studio Web Editor Enhancements</span></span>

<span data-ttu-id="0eaf7-177">Visual Studio 2013 웹 응용 프로그램에서는 Razor 파일 및 HTML 파일에 대 한 새 HTML 편집기를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-177">Visual Studio 2013 includes a new HTML editor for Razor files and HTML files in web applications.</span></span> <span data-ttu-id="0eaf7-178">새 HTML 편집기 HTML5에 따라 단일 통합된 스키마를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-178">The new HTML editor provides a single unified schema based on HTML5.</span></span> <span data-ttu-id="0eaf7-179">자동 중괄호 완성, jQuery UI 및 AngularJS 특성 IntelliSense, IntelliSense 그룹화, ID, Intellisense, 클래스 이름 및 기타 개선 기능 보다 나은 성능, 서식 지정을 포함 하 여 특성 및 스마트 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-179">It has automatic brace completion, jQuery UI and AngularJS attribute IntelliSense, attribute IntelliSense Grouping, ID and class name Intellisense, and other improvements including better performance, formatting and SmartTags.</span></span>

<span data-ttu-id="0eaf7-180">다음 스크린 샷에서 HTML 편집기에서 IntelliSense 부트스트랩 특성을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-180">The following screenshot demonstrates using Bootstrap attribute IntelliSense in the HTML editor.</span></span>

![HTML 편집기의 Intellisense](release-notes/_static/image4.png)

<span data-ttu-id="0eaf7-182">Visual Studio 2013 모두 CoffeeScript 서 기본 제공 편집기에도 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-182">Visual Studio 2013 also comes with both CoffeeScript and LESS editors built in.</span></span> <span data-ttu-id="0eaf7-183">LESS 편집기에서는 CSS 편집기에서 훌륭한 기능이 함께 제공 되었으며 변수와 mixin에 대 한 특정 Intellisense의 덜 모든 문서 전체에서 @import 체인입니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-183">The LESS editor comes with all the cool features from the CSS editor and has specific Intellisense for variables and mixins across all the LESS documents in the @import chain.</span></span>

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a><span data-ttu-id="0eaf7-184">Visual Studio에서 azure 앱 서비스 웹 앱 지원</span><span class="sxs-lookup"><span data-stu-id="0eaf7-184">Azure App Service Web Apps Support in Visual Studio</span></span>

<span data-ttu-id="0eaf7-185">Azure SDK for.NET 2.2와 Visual Studio 2013에서 사용할 수 있습니다 **서버 탐색기** 원격 웹 앱과 직접 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-185">In Visual Studio 2013 with the Azure SDK for .NET 2.2, you can use **Server Explorer** to interact directly with your remote web apps.</span></span> <span data-ttu-id="0eaf7-186">Azure 계정에 로그인 새 웹 응용 프로그램을 만들, 앱 구성 등 실시간 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-186">You can sign in to your Azure account, create new web apps, configure apps, view real-time logs, and more.</span></span> <span data-ttu-id="0eaf7-187">기능은 이후 SDK 2.2 릴리스, Azure에서 원격으로 디버그 모드로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-187">Coming soon after SDK 2.2 is released, you'll be able to run in debug mode remotely in Azure.</span></span> <span data-ttu-id="0eaf7-188">Azure 앱 서비스 웹 앱에 대 한 새로운 기능 대부분.NET 용 Azure SDK의 현재 버전을 설치 하면 Visual Studio 2012에서 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-188">Most of the new features for Azure App Service Web Apps also work in Visual Studio 2012 when you install the current release of the Azure SDK for .NET.</span></span>

<span data-ttu-id="0eaf7-189">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-189">For more information, see the following resources:</span></span>

- [<span data-ttu-id="0eaf7-190">Azure 앱 서비스에서 ASP.NET 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="0eaf7-190">Create an ASP.NET web app in Azure App Service</span></span>](https://azure.microsoft.com/en-us/documentation/articles/web-sites-dotnet-get-started/)
- [<span data-ttu-id="0eaf7-191">Visual Studio를 사용 하 여 Azure 앱 서비스의 웹 응용 프로그램 문제 해결</span><span class="sxs-lookup"><span data-stu-id="0eaf7-191">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](https://azure.microsoft.com/en-us/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a><span data-ttu-id="0eaf7-192">향상 된 기능으로 웹 게시</span><span class="sxs-lookup"><span data-stu-id="0eaf7-192">Web Publish Enhancements</span></span>

<span data-ttu-id="0eaf7-193">Visual Studio 2013에는 새로운 기능과 향상 된 웹 게시 기능이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-193">Visual Studio 2013 includes new and enhanced Web Publish features.</span></span> <span data-ttu-id="0eaf7-194">그 중 일부는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-194">Here are a few of them:</span></span>

- <span data-ttu-id="0eaf7-195">쉽게 [Web.config 파일 암호화 자동화](https://go.microsoft.com/fwlink/?LinkId=325529)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-195">Easily [automate Web.config file encryption](https://go.microsoft.com/fwlink/?LinkId=325529).</span></span> <span data-ttu-id="0eaf7-196">(이 링크 및 다음 두 지점 저녁에 10/17에까지 제공 되지 않을 수 있는 msdn 설명서를 합니다.)</span><span class="sxs-lookup"><span data-stu-id="0eaf7-196">(This link and the following two point to documentation on MSDN that might not be available until late in the day on 10/17.)</span></span>
- <span data-ttu-id="0eaf7-197">쉽게 [응용 프로그램 오프 라인으로 배포 하는 동안 수행 자동화](https://go.microsoft.com/fwlink/?LinkId=325530)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-197">Easily [automate taking an application offline during deployment](https://go.microsoft.com/fwlink/?LinkId=325530).</span></span>
- <span data-ttu-id="0eaf7-198">웹 배포를 구성 [파일 체크섬을 사용 하 여 마지막 변경 날짜 대신](https://go.microsoft.com/fwlink/?LinkId=325531) 서버에 있는 파일을 복사할 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-198">Configure Web Deploy to [use file checksum instead of last-changed date](https://go.microsoft.com/fwlink/?LinkId=325531) for determining which files should be copied to the server.</span></span>
- <span data-ttu-id="0eaf7-199">메서드를 게시 하는 파일 시스템 또는 FTP를 사용 하는 경우 뿐만 아니라 웹 배포와 개별 선택한 파일 (Web.config 포함)를 신속 하 게 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-199">Quickly publish individual selected files (including Web.config) when you're using the FTP or file system publish methods as well as with Web Deploy.</span></span>

<span data-ttu-id="0eaf7-200">ASP.NET 웹 배포에 대 한 자세한 내용은 참조 [ASP.NET 사이트](https://go.microsoft.com/fwlink/?LinkId=322027)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-200">For more information about ASP.NET web deployment, see [the ASP.NET site](https://go.microsoft.com/fwlink/?LinkId=322027).</span></span>

<a id="nuget"></a>
## <a name="nuget-27"></a><span data-ttu-id="0eaf7-201">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="0eaf7-201">NuGet 2.7</span></span>

<span data-ttu-id="0eaf7-202">NuGet 2.7에 자세히 설명 하는 새로운 기능의 풍부한 포함 [NuGet 2.7 릴리스 정보](http://docs.nuget.org/docs/release-notes/nuget-2.7)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-202">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="0eaf7-203">또한이 버전의 NuGet 패키지를 다운로드 하려면 NuGet의 패키지 복원 기능에 대 한 명시적 동의 제공 하는 것을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-203">This version of NuGet also removes the need to provide explicit consent for NuGet's package restore feature to download packages.</span></span> <span data-ttu-id="0eaf7-204">동의 (및 연결 된 확인란 NuGet의 기본 설정 대화 상자) NuGet을 설치 하 여 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-204">Consent (and the associated checkbox in NuGet's preferences dialog) is now granted by installing NuGet.</span></span> <span data-ttu-id="0eaf7-205">이제 패키지를 복원 하기만 하면 기본적으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-205">Now package restore simply works by default.</span></span>

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="0eaf7-206">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="0eaf7-206">ASP.NET Web Forms</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="0eaf7-207">One ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0eaf7-207">One ASP.NET</span></span>

<span data-ttu-id="0eaf7-208">Web Forms 프로젝트 템플릿 새 One ASP.NET 환경과 완벽 하 게 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-208">The Web Forms project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="0eaf7-209">MVC 및 Web API Web Forms 프로젝트를 지원 하 고 하나의 ASP.NET 프로젝트 만들기 마법사를 사용 하 여 인증을 구성할 수 있습니다를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-209">You can add MVC and Web API support to your Web Forms project, and you can configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="0eaf7-210">자세한 내용은 참조 [Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기](creating-web-projects-in-visual-studio.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-210">For more information, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="0eaf7-211">ASP.NET ID</span><span class="sxs-lookup"><span data-stu-id="0eaf7-211">ASP.NET Identity</span></span>

<span data-ttu-id="0eaf7-212">Web Forms 프로젝트 템플릿은 새로운 ASP.NET Identity 프레임 워크를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-212">The Web Forms project templates support the new ASP.NET Identity framework.</span></span> <span data-ttu-id="0eaf7-213">또한 서식 파일에는 이제 Web Forms 인트라넷 프로젝트를 만드는 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-213">In addition, the templates now support creation of a Web Forms intranet project.</span></span> <span data-ttu-id="0eaf7-214">자세한 내용은 참조 [인증 방법을](creating-web-projects-in-visual-studio.md#auth) 에 **Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-214">For more information, see [Authentication Methods](creating-web-projects-in-visual-studio.md#auth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="bootstrap"></a><span data-ttu-id="0eaf7-215">부트스트랩</span><span class="sxs-lookup"><span data-stu-id="0eaf7-215">Bootstrap</span></span>

<span data-ttu-id="0eaf7-216">Web Forms 템플릿을 사용 하 여 [부트스트랩](http://twitter.github.io/bootstrap/) 는 매끄러운 및 응답성이 뛰어난 디자인을 쉽게 사용자 지정할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-216">The Web Forms templates use [Bootstrap](http://twitter.github.io/bootstrap/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="0eaf7-217">자세한 내용은 참조 [Visual Studio 2013 웹 프로젝트 템플릿에서 부트스트랩](creating-web-projects-in-visual-studio.md#bootstrap)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-217">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a><span data-ttu-id="0eaf7-218">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="0eaf7-218">ASP.NET MVC 5</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="0eaf7-219">One ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0eaf7-219">One ASP.NET</span></span>

<span data-ttu-id="0eaf7-220">웹 MVC 프로젝트 템플릿을 새 One ASP.NET 환경과 완벽 하 게 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-220">The Web MVC project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="0eaf7-221">MVC 프로젝트를 사용자 지정 하 고 하나의 ASP.NET 프로젝트 만들기 마법사를 사용 하 여 인증을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-221">You can customize your MVC project and configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="0eaf7-222">ASP.NET MVC 5에 있는 소개 자습서에서 찾을 수 있습니다 [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-222">An introductory tutorial to ASP.NET MVC 5 can be found at [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="0eaf7-223">MVC 5로 MVC 4 프로젝트 업그레이드에 대 한 자세한 내용은 참조 하십시오. [ASP.NET MVC 4 및 Web API 프로젝트를 ASP.NET MVC 5 및 Web API 2로 업그레이드 하는 방법을](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-223">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="0eaf7-224">ASP.NET ID</span><span class="sxs-lookup"><span data-stu-id="0eaf7-224">ASP.NET Identity</span></span>

<span data-ttu-id="0eaf7-225">MVC 프로젝트 템플릿 인증 및 id 관리에 대 한 ASP.NET Id를 사용 하도록 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-225">The MVC project templates have been updated to use ASP.NET Identity for authentication and identity management.</span></span> <span data-ttu-id="0eaf7-226">Facebook 및 Google 인증 및 새로운 구성원 API 자습서에서 찾을 수 있습니다 [Facebook, Google OAuth2 및 OpenID 로그온 ASP.NET MVC 5 응용 프로그램을 만들](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 및 [auth ASP.NET MVC 응용 프로그램 만들기 및 SQL DB Azure 앱 서비스를 배포 하 고](https://azure.microsoft.com/en-us/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-226">A tutorial featuring Facebook and Google authentication and the new membership API can be found at [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) and [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).</span></span>

### <a name="bootstrap"></a><span data-ttu-id="0eaf7-227">부트스트랩</span><span class="sxs-lookup"><span data-stu-id="0eaf7-227">Bootstrap</span></span>

<span data-ttu-id="0eaf7-228">MVC 프로젝트 템플릿을 사용 하도록 업데이트 되었습니다 [부트스트랩](http://getbootstrap.com/) 는 매끄러운 및 응답성이 뛰어난 디자인을 쉽게 사용자 지정할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-228">The MVC project template has been updated to use [Bootstrap](http://getbootstrap.com/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="0eaf7-229">자세한 내용은 참조 [Visual Studio 2013 웹 프로젝트 템플릿에서 부트스트랩](creating-web-projects-in-visual-studio.md#bootstrap)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-229">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="0eaf7-230">인증 필터</span><span class="sxs-lookup"><span data-stu-id="0eaf7-230">Authentication filters</span></span>

<span data-ttu-id="0eaf7-231">인증 필터는 새로운 종류의 필터를 실행 하는 ASP.NET MVC 파이프라인에서 권한 부여 필터 전에 인증 논리 당-작업을 지정할 수 있도록 ASP.NET MVC에서 컨트롤러 당 또는 모든 컨트롤러에 대 한 전역적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-231">Authentication filters are a new kind of filter in ASP.NET MVC that run prior to authorization filters in the ASP.NET MVC pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="0eaf7-232">인증 필터 요청에 자격 증명을 처리 하 고 해당 보안 주체를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-232">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="0eaf7-233">인증 필터 권한이 없는 요청에 부응 인증 챌린지에 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-233">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="0eaf7-234">필터 재정</span><span class="sxs-lookup"><span data-stu-id="0eaf7-234">Filter overrides</span></span>

<span data-ttu-id="0eaf7-235">이제 재정의 필터를 지정 하 여 지정 된 동작 메서드 또는 컨트롤러에 적용 하는 필터를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-235">You can now override which filters apply to a given action method or controller by specifying an override filter.</span></span> <span data-ttu-id="0eaf7-236">재정의 필터에 지정된 된 범위 (작업이 나 컨트롤러)에 대 한 실행 하지 않아야 하는 필터 형식 집합을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-236">Override filters specify a set of filter types that should not be run for a given scope (action or controller).</span></span> <span data-ttu-id="0eaf7-237">이 통해 전체적으로 적용 되지만 다음의 특정 작업이 나 컨트롤러에 적용 하 여 특정 전역 필터를 제외 하는 필터를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-237">This allows you to configure filters that apply globally but then exclude certain global filters from applying to specific actions or controllers.</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="0eaf7-238">특성 라우팅</span><span class="sxs-lookup"><span data-stu-id="0eaf7-238">Attribute routing</span></span>

<span data-ttu-id="0eaf7-239">ASP.NET MVC의 작성자, Tim McCall 여 기여 덕분에 특성 라우팅을 지원 [http://attributerouting.net](http://attributerouting.net)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-239">ASP.NET MVC now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="0eaf7-240">특성 라우팅을 사용 하 여 작업 및 컨트롤러를 주석을 달아 프로그램 경로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-240">With attribute routing you can specify your routes by annotating your actions and controllers.</span></span>

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a><span data-ttu-id="0eaf7-241">ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="0eaf7-241">ASP.NET Web API 2</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="0eaf7-242">특성 라우팅</span><span class="sxs-lookup"><span data-stu-id="0eaf7-242">Attribute routing</span></span>

<span data-ttu-id="0eaf7-243">ASP.NET Web API는 이제 Tim McCall, 작성자에 의해 기여 덕분에 특성 라우팅을 지원 [http://attributerouting.net](http://attributerouting.net)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-243">ASP.NET Web API now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="0eaf7-244">특성 라우팅을 사용 하 여 다음과 같은 컨트롤러를 주석을 달아 웹 API 경로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-244">With attribute routing you can specify your Web API routes by annotating your actions and controllers like this:</span></span>

[!code-csharp[Main](release-notes/samples/sample1.cs)]

<span data-ttu-id="0eaf7-245">특성 라우팅을 제어할 수 더 많은 Uri 통해 웹 API에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-245">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="0eaf7-246">예를 들어 단일 API 컨트롤러를 사용 하 여 리소스 계층 구조를 쉽게 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-246">For example, you can easily define a resource hierarchy using a single API controller:</span></span>

[!code-csharp[Main](release-notes/samples/sample2.cs)]

<span data-ttu-id="0eaf7-247">특성 라우팅을 선택적 매개 변수, 기본값 및 경로 제약 조건을 지정 하기 위한 편리한 구문을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-247">Attribute routing also provides a convenient syntax for specifying optional parameters, default values, and route constraints:</span></span>

[!code-csharp[Main](release-notes/samples/sample3.cs)]

<span data-ttu-id="0eaf7-248">특성 라우팅에 대 한 자세한 내용은 참조 [특성 Web API 2에서의 라우팅](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-248">For more information about attribute routing, see [Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).</span></span>

### <a name="oauth-20"></a><span data-ttu-id="0eaf7-249">OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="0eaf7-249">OAuth 2.0</span></span>

<span data-ttu-id="0eaf7-250">이제 Web API 및 단일 페이지 응용 프로그램 프로젝트 템플릿이 OAuth 2.0을 사용 하는 인증을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-250">The Web API and Single Page Application project templates now support authorization using OAuth 2.0.</span></span> <span data-ttu-id="0eaf7-251">OAuth 2.0은 보호 된 리소스에 대 한 클라이언트 액세스 권한 부여를 위한 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-251">OAuth 2.0 is a framework for authorizing client access to protected resources.</span></span> <span data-ttu-id="0eaf7-252">브라우저 및 모바일 장치를 포함 하 여 클라이언트의 다양 한 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-252">It works for a variety of clients including browsers and mobile devices.</span></span>

<span data-ttu-id="0eaf7-253">OAuth 2.0에 대 한 지원 구현 하는 권한 부여 서버 역할 및 Microsoft OWIN 구성 요소에서 제공 하는 전달자 인증에 대 한 새 보안 미들웨어를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-253">Support for OAuth 2.0 is based on new security middleware provided by the Microsoft OWIN Components for bearer authentication and implementing the authorization server role.</span></span> <span data-ttu-id="0eaf7-254">또는 Azure Active Directory 또는 Windows Server 2012 r 2에서 ad FS와 같은 조직 권한 부여 서버를 사용 하 여 클라이언트에 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-254">Alternatively, clients can be authorized using an organizational authorization server, such as Azure Active Directory or ADFS in Windows Server 2012 R2.</span></span>

### <a name="odata-improvements"></a><span data-ttu-id="0eaf7-255">OData 개선 사항</span><span class="sxs-lookup"><span data-stu-id="0eaf7-255">OData Improvements</span></span>

<span data-ttu-id="0eaf7-256">**$Batch, 및 $value $select, $에 대 한 지원 확장**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-256">**Support for $select, $expand, $batch, and $value**</span></span>

<span data-ttu-id="0eaf7-257">이제 완전히 지원 ASP.NET Web API OData $select에 대 한, $expand, 및 $value 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-257">ASP.NET Web API OData now has full support for $select, $expand, and $value.</span></span> <span data-ttu-id="0eaf7-258">또한 일괄 처리 및 변경 집합이 처리 요청에 대 한 $batch를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-258">You can also use $batch for request batching and processing of change sets.</span></span>

<span data-ttu-id="0eaf7-259">$Select 및 $expand 옵션 OData 끝점에서 반환 되는 데이터의 모양을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-259">The $select and $expand options let you change the shape of the data that is returned from an OData endpoint.</span></span> <span data-ttu-id="0eaf7-260">자세한 내용은 참조 [$select 소개 및 $expand에 Web API OData 지원](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-260">For more information, see [Introducing $select and $expand support in Web API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).</span></span>

<span data-ttu-id="0eaf7-261">**향상 된 확장성**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-261">**Improved extensibility**</span></span>

<span data-ttu-id="0eaf7-262">이제 OData 포맷터를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-262">The OData formatters are now extensible.</span></span> <span data-ttu-id="0eaf7-263">Atom 항목 메타 데이터를 추가할 명명 된 스트림 및 미디어 링크 항목을 지원 및 인스턴스 주석을 추가 링크가 생성 되는 방법을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-263">You can add Atom entry metadata, support named stream and media link entries, add instance annotations, and customize how links are generated.</span></span>

<span data-ttu-id="0eaf7-264">**형식 없는 지원**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-264">**Type-less support**</span></span>

<span data-ttu-id="0eaf7-265">이제 엔터티 형식에 대 한 CLR 형식을 정의할 필요 없이 OData 서비스를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-265">You can now build OData services without needing to define CLR types for your entity types.</span></span> <span data-ttu-id="0eaf7-266">OData 컨트롤러 수 걸리거나의 인스턴스를 반환 하는 대신, **IEdmObject**되는 OData 포맷터 직렬화/역직렬화 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-266">Instead, your OData controllers can take or return instances of **IEdmObject**, which are the OData formatters serialize/deserialize.</span></span>

<span data-ttu-id="0eaf7-267">**기존 모델을 다시 사용**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-267">**Reuse an existing model**</span></span>

<span data-ttu-id="0eaf7-268">기존 엔터티 데이터 모델 (EDM)를 이미 있는 경우 이제 다시 사용할 수 있습니다 것을 직접 새로 작성 하는 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-268">If you already have an existing entity data model (EDM), you can now reuse it directly, instead of having to build a new one.</span></span> <span data-ttu-id="0eaf7-269">예를 들어, Entity Framework를 사용 하는 경우에 EF 빌드 수에 대 한 EDM를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-269">For example, if you are using Entity Framework, you can use the EDM that EF builds for you.</span></span>

### <a name="request-batching"></a><span data-ttu-id="0eaf7-270">일괄 처리 요청</span><span class="sxs-lookup"><span data-stu-id="0eaf7-270">Request Batching</span></span>

<span data-ttu-id="0eaf7-271">일괄 처리 요청 네트워크 트래픽을 줄일 수 다 스러운 사용자 인터페이스 보다 매끄럽게, 제공 하는 단일 HTTP POST 요청을 여러 작업을 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-271">Request batching combines multiple operations into a single HTTP POST request, to reduce network traffic and provide a smoother, less chatty user interface.</span></span> <span data-ttu-id="0eaf7-272">ASP.NET Web API는 이제 일괄 처리 요청에 대 한 몇 가지 전략을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-272">ASP.NET Web API now supports several strategies for request batching:</span></span>

- <span data-ttu-id="0eaf7-273">OData 서비스의 $batch 끝점을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-273">Use the $batch endpoint of an OData service.</span></span>
- <span data-ttu-id="0eaf7-274">여러 개의 요청을 단일 MIME 다중 파트 요청으로 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-274">Package multiple requests into a single MIME multipart request.</span></span>
- <span data-ttu-id="0eaf7-275">일괄 처리 사용자 지정 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-275">Use a custom batching format.</span></span>

<span data-ttu-id="0eaf7-276">일괄 처리 요청을 사용 하려면 Web API 구성을 일괄 처리 처리기가 포함 된 경로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-276">To enable request batching, simply add a route with a batching handler to your Web API configuration:</span></span>

[!code-csharp[Main](release-notes/samples/sample4.cs)]

<span data-ttu-id="0eaf7-277">제어할 수도 있는지 여부를 요청 또는 순차적으로 또는 순서에 관계 없이 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-277">You can also control whether requests or executed sequentially or in any order.</span></span>

### <a name="portable-aspnet-web-api-client"></a><span data-ttu-id="0eaf7-278">휴대용 ASP.NET 웹 API 클라이언트</span><span class="sxs-lookup"><span data-stu-id="0eaf7-278">Portable ASP.NET Web API Client</span></span>

<span data-ttu-id="0eaf7-279">이제 Windows 스토어 및 Windows Phone 8 응용 프로그램에 걸쳐 작동 하는 이식 가능한 클래스 라이브러리를 만드는 ASP.NET 웹 API 클라이언트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-279">You can now use the ASP.NET Web API Client to create portable class libraries that work across your Windows Store and Windows Phone 8 applications.</span></span> <span data-ttu-id="0eaf7-280">클라이언트와 서버 간에 공유할 수 있는 휴대용 포맷터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-280">You can also create portable formatters that can be shared across client and server.</span></span>

### <a name="improved-testability"></a><span data-ttu-id="0eaf7-281">테스트 용이성 향상된</span><span class="sxs-lookup"><span data-stu-id="0eaf7-281">Improved Testability</span></span>

<span data-ttu-id="0eaf7-282">API 2에서는 웹 API 컨트롤러를 테스트 하는 것이 훨씬 쉽게 단위 수입니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-282">Web API 2 makes it much easier to unit test your API controllers.</span></span> <span data-ttu-id="0eaf7-283">방금 요청 메시지와 구성을 API 컨트롤러 인스턴스화하고 테스트 하려는 작업 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-283">Just instantiate your API controller with your request message and configuration, and then call the action method you wish to test.</span></span> <span data-ttu-id="0eaf7-284">모의로 쉽게는 **UrlHelper** 링크 생성을 수행 하는 작업 방법에 대 한 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-284">It is also easy to mock the **UrlHelper** class, for action methods that perform link generation.</span></span>

### <a name="ihttpactionresult"></a><span data-ttu-id="0eaf7-285">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="0eaf7-285">IHttpActionResult</span></span>

<span data-ttu-id="0eaf7-286">이제 Web API 동작 메서드의 결과 캡슐화 하는 IHttpActionResult 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-286">You can now implement IHttpActionResult to encapsulate the result of your Web API action methods.</span></span> <span data-ttu-id="0eaf7-287">웹 API 동작 메서드에서 반환 되는 IHttpActionResult 결과 응답 메시지를 만들기 위해 ASP.NET Web API 런타임에 의해 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-287">An IHttpActionResult returned from a Web API action method is executed by the ASP.NET Web API runtime to produce the resultant response message.</span></span> <span data-ttu-id="0eaf7-288">IHttpActionResult 단위를 간소화 하기 위해 웹 API 작업에서 반환 될 수의 웹 API 구현을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-288">An IHttpActionResult can be returned from any Web API action to simplify unit testing of your Web API implementation.</span></span> <span data-ttu-id="0eaf7-289">많은 IHttpActionResult 구현 관련 상태 코드를 반환 하는 것에 대 한 결과 포함 하 여 기본적으로 제공 되는 편의 위해 콘텐츠 또는 콘텐츠 협상 응답을 포맷 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-289">For convenience a number of IHttpActionResult implementations are provided out of the box including results for returning specific status codes, formatted content or content-negotiated responses.</span></span>

### <a name="httprequestcontext"></a><span data-ttu-id="0eaf7-290">HttpRequestContext</span><span class="sxs-lookup"><span data-stu-id="0eaf7-290">HttpRequestContext</span></span>

<span data-ttu-id="0eaf7-291">새 **HttpRequestContext** 요청에 연결 하지 않으면이 요청에서 바로 사용할 수 있는 모든 상태를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-291">The new **HttpRequestContext** tracks any state that is tied to the request but is not immediately available from the request.</span></span> <span data-ttu-id="0eaf7-292">예를 들어, 사용할 수는 **HttpRequestContext** 경로 데이터를 클라이언트 인증서를 요청에 연결 된 보안 주체 가져오는 **UrlHelper** 및 가상 경로 루트입니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-292">For example, you can use the **HttpRequestContext** to get route data, the principal associated with the request, the client certificate, the **UrlHelper** and the virtual path root.</span></span> <span data-ttu-id="0eaf7-293">쉽게 만들 수 있습니다는 **HttpRequestContext** 단위에 대 한 테스트 목적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-293">You can easily create an **HttpRequestContext** for unit testing purposes.</span></span>

<span data-ttu-id="0eaf7-294">요청에 대 한 보안 주체에 의존 하지 않고 요청으로 흐를 때문에 **Thread.CurrentPrincipal**, Web API 파이프라인 되는 동안 주 서버 요청의 수명 주기 동안 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-294">Because the principal for the request is flowed with the request instead of relying on **Thread.CurrentPrincipal**, the principal is now available throughout the lifetime of the request while it is in the Web API pipeline.</span></span>

### <a name="cors"></a><span data-ttu-id="0eaf7-295">CORS</span><span class="sxs-lookup"><span data-stu-id="0eaf7-295">CORS</span></span>

<span data-ttu-id="0eaf7-296">Brock Allen에서 또 다른 훌륭한 기여를 통해 ASP.NET 완벽 하 게 지원 요청 공유 CORS (Cross Origin).</span><span class="sxs-lookup"><span data-stu-id="0eaf7-296">Thanks to another great contribution from Brock Allen, ASP.NET now fully supports Cross Origin Request Sharing (CORS).</span></span>

<span data-ttu-id="0eaf7-297">브라우저 보안 다른 도메인에 대 한 AJAX 요청에서 웹 페이지를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-297">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="0eaf7-298">[CORS](http://www.w3.org/TR/cors/) 은 W3C 표준 동일 원본 정책을 완화 하도록 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-298">[CORS](http://www.w3.org/TR/cors/) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="0eaf7-299">CORS를 사용 하는 서버는 다른 사용자를 거부 하는 동안 일부 크로스-원본 요청을 명시적으로 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-299">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span>

<span data-ttu-id="0eaf7-300">Web API 2에는 이제 자동으로 실행 전 요청 처리를 포함 하 여 CORS를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-300">Web API 2 now supports CORS, including automatic handling of preflight requests.</span></span> <span data-ttu-id="0eaf7-301">자세한 내용은 참조 [ASP.NET Web API에서 크로스-원본 요청을 사용 하도록 설정](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-301">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="0eaf7-302">인증 필터</span><span class="sxs-lookup"><span data-stu-id="0eaf7-302">Authentication Filters</span></span>

<span data-ttu-id="0eaf7-303">인증 필터는 새로운 종류의 필터에 ASP.NET Web API 파이프라인의 권한 부여 필터 전에 실행 하 고 인증 논리 당-작업을 지정할 수 있도록 하는 ASP.NET Web API 컨트롤러 당 또는 모든 컨트롤러에 대 한 전역적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-303">Authentication filters are a new kind of filter in ASP.NET Web API that run prior to authorization filters in the ASP.NET Web API pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="0eaf7-304">인증 필터 요청에 자격 증명을 처리 하 고 해당 보안 주체를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-304">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="0eaf7-305">인증 필터 권한이 없는 요청에 부응 인증 챌린지에 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-305">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="0eaf7-306">필터 재정</span><span class="sxs-lookup"><span data-stu-id="0eaf7-306">Filter Overrides</span></span>

<span data-ttu-id="0eaf7-307">이제 재정의 필터를 지정 하 여 지정 된 동작 메서드 또는 컨트롤러에 적용 하는 필터를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-307">You can now override which filters apply to a given action method or controller, by specifying an override filter.</span></span> <span data-ttu-id="0eaf7-308">재정의 필터에 지정된 된 범위 (작업이 나 컨트롤러)에 대 한 실행 하지 않아야 하는 필터 형식 집합을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-308">Override filters specify a set of filter types that should not run for a given scope (action or controller).</span></span> <span data-ttu-id="0eaf7-309">이 옵션을 사용 하면 전역 필터를 추가 하지만 특정 작업이 나 컨트롤러에서 일부를 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-309">This allows you to add global filters, but then exclude some from specific actions or controllers.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="0eaf7-310">OWIN 통합</span><span class="sxs-lookup"><span data-stu-id="0eaf7-310">OWIN Integration</span></span>

<span data-ttu-id="0eaf7-311">ASP.NET Web API 이제 완벽 하 게 지원 OWIN 하며 모든 OWIN 가능 호스트에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-311">ASP.NET Web API now fully supports OWIN and can be run on any OWIN capable host.</span></span> <span data-ttu-id="0eaf7-312">또한 포함 됩니다는 **HostAuthenticationFilter** OWIN 인증 시스템과 통합을 제공 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-312">Also included is a **HostAuthenticationFilter** that provides integration with the OWIN authentication system.</span></span>

<span data-ttu-id="0eaf7-313">OWIN 통합 SignalR 등 다른 OWIN 미들웨어와 함께 사용자가 소유한 프로세스에 Web API를 자체 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-313">With OWIN integration, you can self-host Web API in your own process alongside other OWIN middleware, such as SignalR.</span></span> <span data-ttu-id="0eaf7-314">자세한 내용은 참조 [Self-Host ASP.NET Web API를 사용 하 여 OWIN](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-314">For more information, see [Use OWIN to Self-Host ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a><span data-ttu-id="0eaf7-315">ASP.NET SignalR 2.0</span><span class="sxs-lookup"><span data-stu-id="0eaf7-315">ASP.NET SignalR 2.0</span></span>

<span data-ttu-id="0eaf7-316">다음 섹션에서는 SignalR 2.0의 기능을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-316">The following sections describe features of SignalR 2.0.</span></span>

- [<span data-ttu-id="0eaf7-317">OWIN 기반</span><span class="sxs-lookup"><span data-stu-id="0eaf7-317">Built on OWIN</span></span>](#builtonowin)
- [<span data-ttu-id="0eaf7-318">MapHubs 및 MapConnection MapSignalR 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-318">MapHubs and MapConnection are now MapSignalR</span></span>](#MapSignalR)
- [<span data-ttu-id="0eaf7-319">도메인 간 지원</span><span class="sxs-lookup"><span data-stu-id="0eaf7-319">Cross-Domain Support</span></span>](#crossdomain)
- [<span data-ttu-id="0eaf7-320">iOS 및 Android MonoTouch 및 MonoDroid를 통해 지원</span><span class="sxs-lookup"><span data-stu-id="0eaf7-320">iOS and Android support via MonoTouch and MonoDroid</span></span>](#mobile)
- [<span data-ttu-id="0eaf7-321">이식 가능한.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="0eaf7-321">Portable .NET Client</span></span>](#portable)
- [<span data-ttu-id="0eaf7-322">자체 호스트 하는 새 패키지</span><span class="sxs-lookup"><span data-stu-id="0eaf7-322">New Self-Host Package</span></span>](#selfhost)
- [<span data-ttu-id="0eaf7-323">이전 버전과 호환성 서버 지원</span><span class="sxs-lookup"><span data-stu-id="0eaf7-323">Backward-compatible server support</span></span>](#backwardcompat)
- [<span data-ttu-id="0eaf7-324">.NET 4.0에 대 한 서버 지원을 제거</span><span class="sxs-lookup"><span data-stu-id="0eaf7-324">Removed server support for .NET 4.0</span></span>](#remove40)
- [<span data-ttu-id="0eaf7-325">클라이언트 및 그룹의 목록으로 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="0eaf7-325">Sending a message to a list of clients and groups</span></span>](#messagelist)
- [<span data-ttu-id="0eaf7-326">특정 사용자에 게 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="0eaf7-326">Sending a message to a specific user</span></span>](#sendtouser)
- [<span data-ttu-id="0eaf7-327">더 나은 오류 처리 지원</span><span class="sxs-lookup"><span data-stu-id="0eaf7-327">Better error handling support</span></span>](#errorhandling)
- [<span data-ttu-id="0eaf7-328">보다 쉽게 단위 테스트 허브의</span><span class="sxs-lookup"><span data-stu-id="0eaf7-328">Easier unit testing of hubs</span></span>](#unittesting)
- [<span data-ttu-id="0eaf7-329">JavaScript 오류 처리</span><span class="sxs-lookup"><span data-stu-id="0eaf7-329">JavaScript error handling</span></span>](#javascripterror)

<span data-ttu-id="0eaf7-330">SignalR 2.0으로 기존 1.x 프로젝트를 업그레이드 하는 방법의 예제를 보려면 [업그레이드 하는 SignalR 프로젝트 1.x](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-330">For an example of how to upgrade an existing 1.x project to SignalR 2.0, see [Upgrading a SignalR 1.x Project](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<a id="builtonowin"></a>
### <a name="built-on-owin"></a><span data-ttu-id="0eaf7-331">OWIN 기반</span><span class="sxs-lookup"><span data-stu-id="0eaf7-331">Built on OWIN</span></span>

<span data-ttu-id="0eaf7-332">SignalR 2.0에 완전히 빌드될 [OWIN (.NET에 대 한 Open Web Interface)](http://owin.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-332">SignalR 2.0 is built completely on [OWIN (the Open Web Interface for .NET)](http://owin.org/).</span></span> <span data-ttu-id="0eaf7-333">이러한 변경 하면 설치 프로세스를 SignalR에 대 한 훨씬 더 웹 호스팅 및 자체 호스트 된 SignalR 응용 프로그램 간에 일관 하지만 다양 한 API 변경 때도 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-333">This change makes the setup process for SignalR much more consistent between web-hosted and self-hosted SignalR applications, but has also required a number of API changes.</span></span>

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a><span data-ttu-id="0eaf7-334">MapHubs 및 MapConnection MapSignalR 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-334">MapHubs and MapConnection are now MapSignalR</span></span>

<span data-ttu-id="0eaf7-335">OWIN 표준 호환성을 위해 이러한 메서드로 변경 되었습니다 `MapSignalR`합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-335">For compatibility with OWIN standards, these methods have been renamed to `MapSignalR`.</span></span> <span data-ttu-id="0eaf7-336">`MapSignalR`매개 변수는 모든 허브 매핑됩니다 없이 호출 (으로 `MapHubs` 버전에서 1.x); 개별 매핑할 **PersistentConnection** 개체, 형식 매개 변수 및으로 연결에 대 한 URL 확장명 연결 유형을 지정는 첫 번째 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-336">`MapSignalR` called without parameters will map all hubs (as `MapHubs` does in version 1.x); to map individual **PersistentConnection** objects, specify the connection type as the type parameter, and the URL extension for the connection as the first argument.</span></span>

<span data-ttu-id="0eaf7-337">`MapSignalR` 메서드 Owin 시작 클래스에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-337">The `MapSignalR` method is called in an Owin startup class.</span></span> <span data-ttu-id="0eaf7-338">Owin 시작 클래스;에 대 한 새 서식 파일을 포함 하는 visual Studio 2013 이 서식 파일을 사용 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-338">Visual Studio 2013 contains a new template for an Owin startup class; to use this template, do the following:</span></span>

1. <span data-ttu-id="0eaf7-339">프로젝트를 마우스 오른쪽 단추로 클릭</span><span class="sxs-lookup"><span data-stu-id="0eaf7-339">Right-click on the project</span></span>
2. <span data-ttu-id="0eaf7-340">선택 **추가**, **새 항목...**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-340">Select **Add**, **New Item...**</span></span>
3. <span data-ttu-id="0eaf7-341">선택 **Owin 시작 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-341">Select **Owin Startup class**.</span></span> <span data-ttu-id="0eaf7-342">클래스의 새 이름을 **Startup.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-342">Name the new class **Startup.cs**.</span></span>

<span data-ttu-id="0eaf7-343">에 **웹 응용 프로그램을** 는 Owin 시작 클래스를 포함 하는 `MapSignalR` 메서드가 아래와 같이 다음 항목을 사용 하 여 Web.Config 파일의 응용 프로그램 설정 노드에 Owin의 시작 프로세스에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-343">In a **Web application,** the Owin startup class containing the `MapSignalR` method is then added to Owin's startup process using an entry in the application settings node of the Web.Config file, as shown below.</span></span>

<span data-ttu-id="0eaf7-344">에 **자체 응용 프로그램을 호스트**, 시작 클래스의 형식 매개 변수로 전달 되는 `WebApp.Start` 메서드.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-344">In a **Self-hosted application**, the Startup class is passed as the type parameter of the `WebApp.Start` method.</span></span>

<span data-ttu-id="0eaf7-345">**SignalR 연결 및 허브 매핑 1.x (웹 응용 프로그램의 전역 응용 프로그램 파일)에서:**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-345">**Mapping hubs and connections in SignalR 1.x (from the global application file in a web application):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

<span data-ttu-id="0eaf7-346">**Owin 시작 클래스 파일) (에서 SignalR 2.0의 연결 및 허브 매핑:**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-346">**Mapping hubs and connections in SignalR 2.0 (from an Owin Startup class file):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

<span data-ttu-id="0eaf7-347">에 **자체 응용 프로그램을 호스트**, 시작 클래스에 대 한 형식 매개 변수로 전달 되는 `WebApp.Start` 메서드를 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-347">In a **Self-hosted application**, the Startup class is passed as the type parameter for the `WebApp.Start` method, as shown below.</span></span>

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a><span data-ttu-id="0eaf7-348">도메인 간 지원</span><span class="sxs-lookup"><span data-stu-id="0eaf7-348">Cross-Domain Support</span></span>

<span data-ttu-id="0eaf7-349">SignalR에서 도메인 간 요청 1.x 된 단일 EnableCrossDomain 플래그에 의해 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-349">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="0eaf7-350">이 플래그는 모두 JSONP 및 CORS 요청을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-350">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="0eaf7-351">모든 CORS 지원 유연성을 높이기 위해 SignalR의 서버 구성 요소에서 제거 되었습니다 (JavaScript lients 여전히 CORS 일반적으로 브라우저 지원 하는지 검색 하는 경우)을 사용할 새 OWIN 미들웨어가 제공 되기 이러한 시나리오를 지원 하도록 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-351">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript lients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="0eaf7-352">SignalR 2.0의 경우 JSONP에 필요 클라이언트 (이전 브라우저에서 도메인 간 요청을 지 원하는)을 설정 하 여 명시적으로 설정 해야 합니다 `EnableJSONP` 에 `HubConfiguration` 개체를 `true`다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-352">In SignalR 2.0, If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="0eaf7-353">JSONP는 CORS 보다 덜 안전 이므로 기본적으로 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-353">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="0eaf7-354">SignalR 2.0을 새 CORS 미들웨어를 추가 하려면 추가 `Microsoft.Owin.Cors` 라이브러리를 프로젝트 및 호출 `UseCors` SignalR 미들웨어, 아래 섹션에 나와 있는 것 처럼 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-354">To add the new CORS middleware in SignalR 2.0, add the `Microsoft.Owin.Cors` library to your project, and call `UseCors` before your SignalR middleware, as shown in the section below.</span></span>

<span data-ttu-id="0eaf7-355">**Microsoft.Owin.Cors 프로젝트에 추가**:이 라이브러리를 설치 하려면 패키지 관리자 콘솔에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-355">**Adding Microsoft.Owin.Cors to your project**: To install this library, run the following command in the Package Manager Console:</span></span>

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

<span data-ttu-id="0eaf7-356">이 명령은 2.0.0을 추가 합니다 프로젝트에 패키지의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-356">This command will add the 2.0.0 version of the package to your project.</span></span>

<span data-ttu-id="0eaf7-357">**UseCors 호출**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-357">**Calling UseCors**</span></span>

<span data-ttu-id="0eaf7-358">다음 코드 조각에는 SignalR에서 도메인 간 연결을 구현 하는 방법을 보여 1.x 및 2.0.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-358">The following code snippets demonstrate how to implement cross-domain connections in SignalR 1.x and 2.0.</span></span>

<span data-ttu-id="0eaf7-359">**SignalR에서 도메인 간 요청을 구현 1.x (에서 전역 응용 프로그램 파일)**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-359">**Implementing cross-domain requests in SignalR 1.x (from the global application file)**</span></span>

[!code-csharp[Main](release-notes/samples/sample9.cs)]

<span data-ttu-id="0eaf7-360">**(C# 코드 파일)에서 SignalR 2.0에서 도메인 간 요청을 구현합니다.**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-360">**Implementing cross-domain requests in SignalR 2.0 (from a C# code file)**</span></span>

<span data-ttu-id="0eaf7-361">다음 코드는 SignalR 2.0 프로젝트에서 JSONP 또는 CORS를 사용 하도록 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-361">The following code demonstrates how to enable CORS or JSONP in a SignalR 2.0 project.</span></span> <span data-ttu-id="0eaf7-362">이 코드 샘플에서는 `Map` 및 `RunSignalR` 대신 `MapSignalR`CORS 미들웨어 CORS 지원 해야 하는 SignalR 요청에 대해서만 실행 되도록 하는, (아니라에 지정 된 경로에 모든 트래픽에 대해 `MapSignalR`.) `Map` 특정 URL 접두사에 대 한 아니라 전체 응용 프로그램을 실행 하는 다른 모든 미들웨어에 대 한 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-362">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) `Map` can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a><span data-ttu-id="0eaf7-363">iOS 및 Android MonoTouch 및 MonoDroid를 통해 지원</span><span class="sxs-lookup"><span data-stu-id="0eaf7-363">iOS and Android support via MonoTouch and MonoDroid</span></span>

<span data-ttu-id="0eaf7-364">IOS 및 Android 클라이언트에서 MonoTouch 및 MonoDroid 구성 요소를 사용 하 여에 대 한 지원이 추가 되었습니다는 [Xamarin 라이브러리](https://xamarin.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-364">Support has been added for iOS and Android clients using MonoTouch and MonoDroid components from the [Xamarin library](https://xamarin.com/).</span></span> <span data-ttu-id="0eaf7-365">사용 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Xamarin 구성 요소를 사용 하 여](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-365">For more information on how to use them, see [Using Xamarin Components](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln).</span></span> <span data-ttu-id="0eaf7-366">이러한 구성 요소에서 사용할 수 있습니다는 [Xamarin 스토어](https://store.xamarin.com/) SignalR RTW 릴리스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-366">These components will be available in the [Xamarin Store](https://store.xamarin.com/) when the SignalR RTW release is available.</span></span>

<a id="portable"></a><span data-ttu-id="0eaf7-367"># # # 이식 가능한.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="0eaf7-367">### Portable .NET client</span></span>

<span data-ttu-id="0eaf7-368">보다 잘 Silverlight, WinRT 플랫폼 간 개발을 용이 하 게 하 고 Windows Phone 클라이언트는 단일 이식 가능한.NET 클라이언트를 지 원하는 플랫폼은 다음과 같은 대체 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-368">To better facilitate cross-platform development, the Silverlight, WinRT and Windows Phone clients have been replaced with a single portable .NET client that supports the following platforms:</span></span>

- <span data-ttu-id="0eaf7-369">NET 4.5</span><span class="sxs-lookup"><span data-stu-id="0eaf7-369">NET 4.5</span></span>
- <span data-ttu-id="0eaf7-370">Silverlight 5</span><span class="sxs-lookup"><span data-stu-id="0eaf7-370">Silverlight 5</span></span>
- <span data-ttu-id="0eaf7-371">WinRT (Windows 스토어 앱 용.NET)</span><span class="sxs-lookup"><span data-stu-id="0eaf7-371">WinRT (.NET for Windows Store Apps)</span></span>
- <span data-ttu-id="0eaf7-372">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="0eaf7-372">Windows Phone 8</span></span>

<a id="selfhost"></a>

### <a name="new-self-host-package"></a><span data-ttu-id="0eaf7-373">자체 호스트 하는 새 패키지</span><span class="sxs-lookup"><span data-stu-id="0eaf7-373">New Self-Host Package</span></span>

<span data-ttu-id="0eaf7-374">SignalR 자가 호스트 (SignalR 응용 프로그램 프로세스에서 호스트 되는 다른 응용 프로그램을 대신 또는 웹 서버에 호스트 중인)를 시작 하기 쉽게 수행할 수 있도록 NuGet 패키지가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-374">There is now a NuGet package to make it easier to get started with SignalR Self-Host (SignalR applications that are hosted in a process or other application, rather than being hosted in a web server).</span></span> <span data-ttu-id="0eaf7-375">SignalR을 사용 하 여 작성 하는 자체 호스트 프로젝트를 업그레이드 하려면 1.x Microsoft.AspNet.SignalR.Owin 패키지를 제거 하 고 Microsoft.AspNet.SignalR.SelfHost 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-375">To upgrade a self-host project built with SignalR 1.x, remove the Microsoft.AspNet.SignalR.Owin package, and add the Microsoft.AspNet.SignalR.SelfHost package.</span></span> <span data-ttu-id="0eaf7-376">시작 자가 호스트 패키지에 대 한 자세한 내용은 참조 하십시오. [자습서: 자체 호스트 하는 SignalR](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-376">For more information on getting started with the self-host package, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a><span data-ttu-id="0eaf7-377">이전 버전과 호환성 서버 지원</span><span class="sxs-lookup"><span data-stu-id="0eaf7-377">Backward-compatible server support</span></span>

<span data-ttu-id="0eaf7-378">이전 버전의 SignalR에 동일 해야 하는 서버 및 클라이언트에서 사용 되는 SignalR 패키지의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-378">In previous versions of SignalR, the versions of the SignalR package used in the client and the server needed to be identical.</span></span> <span data-ttu-id="0eaf7-379">업데이트 하기 어려운는 굵게 클라이언트 응용 프로그램을 지원 하기 위해 SignalR 2.0 이전 클라이언트를 최신 서버 버전을 사용 하 여 이제 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-379">In order to support thick-client applications that would be difficult to update, SignalR 2.0 now supports using a newer server version with an older client.</span></span> <span data-ttu-id="0eaf7-380">**참고: SignalR 2.0 최신 클라이언트를 사용 하 여 이전 버전으로 작성 하는 서버를 지원 하지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-380">**Note: SignalR 2.0 does not support servers built with older versions with newer clients.**</span></span>

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a><span data-ttu-id="0eaf7-381">.NET 4.0에 대 한 서버 지원을 제거</span><span class="sxs-lookup"><span data-stu-id="0eaf7-381">Removed server support for .NET 4.0</span></span>

<span data-ttu-id="0eaf7-382">SignalR 2.0 미만으로 떨어졌습니다.NET 4.0이 있는 서버 상호 운용성에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-382">SignalR 2.0 has dropped support for server interoperability with .NET 4.0.</span></span> <span data-ttu-id="0eaf7-383">.NET 4.5 SignalR 2.0 서버와 함께 사용 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-383">.NET 4.5 must be used with SignalR 2.0 servers.</span></span> <span data-ttu-id="0eaf7-384">SignalR 2.0에 대 한.NET 4.0 클라이언트는 여전히 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-384">There is still a .NET 4.0 client for SignalR 2.0.</span></span>

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a><span data-ttu-id="0eaf7-385">클라이언트 및 그룹의 목록으로 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="0eaf7-385">Sending a message to a list of clients and groups</span></span>

<span data-ttu-id="0eaf7-386">SignalR 2.0에서는 클라이언트와 그룹 Id 목록을 사용 하 여 메시지를 보낼 수는.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-386">In SignalR 2.0, it's possible to send a message using a list of client and group IDs.</span></span> <span data-ttu-id="0eaf7-387">다음 코드 조각에서는이 작업을 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-387">The following code snippets demonstrate how to do this.</span></span>

<span data-ttu-id="0eaf7-388">**클라이언트 및 PersistentConnection를 사용 하 여 그룹의 목록으로 메시지 보내기**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-388">**Sending a message to a list of clients and groups using PersistentConnection**</span></span>

[!code-csharp[Main](release-notes/samples/sample11.cs)]

<span data-ttu-id="0eaf7-389">**클라이언트와 허브를 사용 하 여 그룹의 목록으로 메시지 보내기**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-389">**Sending a message to a list of clients and groups using Hubs**</span></span>

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a><span data-ttu-id="0eaf7-390">특정 사용자에 게 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="0eaf7-390">Sending a message to a specific user</span></span>

<span data-ttu-id="0eaf7-391">사용자 대상을 지정 하는 사용자 Id는이 기능을 통해 IUserIdProvider 새 인터페이스를 통해 IRequest에 따라:</span><span class="sxs-lookup"><span data-stu-id="0eaf7-391">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider:</span></span>

<span data-ttu-id="0eaf7-392">**IUserIdProvider 인터페이스**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-392">**The IUserIdProvider interface**</span></span>

[!code-csharp[Main](release-notes/samples/sample13.cs)]

<span data-ttu-id="0eaf7-393">기본적으로에 사용자의 IPrincipal.Identity.Name 사용자 이름으로 사용 하는 구현이 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-393">By default there will be an implementation that uses the user's IPrincipal.Identity.Name as the user name.</span></span>

<span data-ttu-id="0eaf7-394">허브에서 새 API 통해 이러한 사용자에 게 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-394">In hubs, you'll be able to send messages to these users via a new API:</span></span>

<span data-ttu-id="0eaf7-395">**Clients.User API를 사용 하 여**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-395">**Using the Clients.User API**</span></span>

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a><span data-ttu-id="0eaf7-396">더 나은 오류 처리 지원</span><span class="sxs-lookup"><span data-stu-id="0eaf7-396">Better Error Handling Support</span></span>

<span data-ttu-id="0eaf7-397">사용자가 throw 할 수 이제 **HubException** 모든 허브 호출에서.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-397">Users can now throw **HubException** from any hub invocation.</span></span> <span data-ttu-id="0eaf7-398">생성자는 **HubException** 문자열 메시지와 개체 표시 되려면 추가 오류 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-398">The constructor of the **HubException** can take a string message and an object extra error data.</span></span> <span data-ttu-id="0eaf7-399">SignalR 예외를 자동 serialize 하 고 클라이언트에 보냅니다 거부/실패 허브 메서드 호출에 사용할 수는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-399">SignalR will auto-serialize the exception and send it to the client where it will be used to reject/fail the hub method invocation.</span></span>

<span data-ttu-id="0eaf7-400">**자세한 허브 예외 표시** 설정은 관련이 없습니다 **HubException** 는 없습니다; 다시 클라이언트에 전송 되 고 항상 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-400">The **show detailed hub exceptions** setting has no bearing on **HubException** being sent back to the client or not; it is always sent.</span></span>

<span data-ttu-id="0eaf7-401">**서버 쪽 코드는 HubException 클라이언트에 게 보내는 시연**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-401">**Server-side code demonstrating sending a HubException to the client**</span></span>

[!code-csharp[Main](release-notes/samples/sample15.cs)]

<span data-ttu-id="0eaf7-402">**JavaScript 클라이언트 코드가 서버에서 보낸 HubException에 응답을 시연**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-402">**JavaScript client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-html[Main](release-notes/samples/sample16.html)]

<span data-ttu-id="0eaf7-403">**서버에서 보낸 HubException에 응답을 보여 주는.NET 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-403">**.NET client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a><span data-ttu-id="0eaf7-404">보다 쉽게 단위 테스트 허브의</span><span class="sxs-lookup"><span data-stu-id="0eaf7-404">Easier unit testing of hubs</span></span>

<span data-ttu-id="0eaf7-405">SignalR 2.0 이라는 인터페이스에 `IHubCallerConnectionContext` 모의 클라이언트 쪽 호출을 만드는 쉽게 허브에서.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-405">SignalR 2.0 includes an interface called `IHubCallerConnectionContext` on Hubs that makes it easier to create mock client side invocations.</span></span> <span data-ttu-id="0eaf7-406">다음 코드 조각 인기 있는 테스트 장비와이 인터페이스를 사용 하 여 보여 줍니다. [xUnit.net](https://github.com/xunit/xunit) 및 [moq](https://code.google.com/p/moq/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-406">The following code snippets demonstrate using this interface with popular test harnesses [xUnit.net](https://github.com/xunit/xunit) and [moq](https://code.google.com/p/moq/).</span></span>

<span data-ttu-id="0eaf7-407">**SignalR를 사용한 단위 테스트 xUnit.net**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-407">**Unit testing SignalR with xUnit.net**</span></span>

[!code-csharp[Main](release-notes/samples/sample18.cs)]

<span data-ttu-id="0eaf7-408">**SignalR를 사용한 단위 테스트 moq**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-408">**Unit testing SignalR with moq**</span></span>

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a><span data-ttu-id="0eaf7-409">JavaScript 오류 처리</span><span class="sxs-lookup"><span data-stu-id="0eaf7-409">JavaScript error handling</span></span>

<span data-ttu-id="0eaf7-410">SignalR 2.0 모든 JavaScript 오류 처리 콜백을 원시 문자열 대신 JavaScript 오류 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-410">In SignalR 2.0, all JavaScript error handling callbacks return JavaScript error objects instead of raw strings.</span></span> <span data-ttu-id="0eaf7-411">따라서 오류 처리기에 다양 한 정보를 이동 하는 SignalR 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-411">This allows SignalR to flow richer information to your error handlers.</span></span> <span data-ttu-id="0eaf7-412">내부 예외를 가져올 수 있습니다는 `source` 오류 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-412">You can get the inner exception from the `source` property of the error.</span></span>

<span data-ttu-id="0eaf7-413">**Start.Fail 예외를 처리 하는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-413">**JavaScript client code that handles the Start.Fail exception**</span></span>

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a><span data-ttu-id="0eaf7-414">ASP.NET ID</span><span class="sxs-lookup"><span data-stu-id="0eaf7-414">ASP.NET Identity</span></span>

### <a name="new-aspnet-membership-system"></a><span data-ttu-id="0eaf7-415">새 ASP.NET 멤버 자격 시스템</span><span class="sxs-lookup"><span data-stu-id="0eaf7-415">New ASP.NET Membership System</span></span>

<span data-ttu-id="0eaf7-416">ASP.NET Id는 ASP.NET 응용 프로그램에 대 한 새 멤버 자격 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-416">ASP.NET Identity is the new membership system for ASP.NET applications.</span></span> <span data-ttu-id="0eaf7-417">ASP.NET Id를 사용 하면 쉽게 응용 프로그램 데이터와 사용자 고유의 프로필 데이터를 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-417">ASP.NET Identity makes it easy to integrate user-specific profile data with application data.</span></span> <span data-ttu-id="0eaf7-418">ASP.NET Id를 사용 하면 응용 프로그램의 사용자 프로필에 대 한 지 속성 모델을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-418">ASP.NET Identity also allows you to choose the persistence model for user profiles in your application.</span></span> <span data-ttu-id="0eaf7-419">SQL Server 데이터베이스 또는 Azure 저장소 테이블 같은 NoSQL 데이터 저장소를 포함 하 여 다른 데이터 저장소에 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-419">You can store the data in a SQL Server database or another data store, including NoSQL data stores such as Azure Storage Tables.</span></span> <span data-ttu-id="0eaf7-420">자세한 내용은 참조 [개별 사용자 계정](creating-web-projects-in-visual-studio.md#indauth) 에 **Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-420">For more information, see [Individual User Accounts](creating-web-projects-in-visual-studio.md#indauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="claims-based-authentication"></a><span data-ttu-id="0eaf7-421">클레임 기반 인증</span><span class="sxs-lookup"><span data-stu-id="0eaf7-421">Claims-based authentication</span></span>

<span data-ttu-id="0eaf7-422">이제 ASP.NET 클레임 기반 인증 일 경우 사용자의 id은 신뢰할 수 있는 발급자 클레임 집합으로 표시 되는 위치를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-422">ASP.NET now supports claims-based authentication, where the user's identity is represented as a set of claims from a trusted issuer.</span></span> <span data-ttu-id="0eaf7-423">인증 된 사용자 이름 및 응용 프로그램 데이터베이스에서 유지 관리 하는 암호를 사용 하 여 또는 소셜 id 공급자를 사용 하 여 사용자가 될 수 있습니다 (예: Microsoft 계정, Facebook, Google, Twitter), 또는 Azure Active Directory를 통해 조직 계정을 사용 하 여 또는 Active Directory Federation Services (ad FS)입니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-423">Users can be authenticated using a username and password maintained in an application database, or using social identity providers (for example: Microsoft Accounts, Facebook, Google, Twitter), or using organizational accounts through Azure Active Directory or Active Directory Federation Services (ADFS).</span></span>

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a><span data-ttu-id="0eaf7-424">Azure Active Directory 및 Windows Server Active Directory와의 통합</span><span class="sxs-lookup"><span data-stu-id="0eaf7-424">Integration with Azure Active Directory and Windows Server Active Directory</span></span>

<span data-ttu-id="0eaf7-425">이제 인증을 위해 Azure Active Directory 또는 Windows Server AD (Active Directory)를 사용 하는 ASP.NET 프로젝트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-425">You can now create ASP.NET projects that use Azure Active Directory or Windows Server Active Directory (AD) for authentication.</span></span> <span data-ttu-id="0eaf7-426">자세한 내용은 참조 [조직 계정](creating-web-projects-in-visual-studio.md#orgauth) 에 **Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-426">For more information, see [Organizational Accounts](creating-web-projects-in-visual-studio.md#orgauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="0eaf7-427">OWIN 통합</span><span class="sxs-lookup"><span data-stu-id="0eaf7-427">OWIN Integration</span></span>

<span data-ttu-id="0eaf7-428">ASP.NET 인증은 이제 모든 OWIN 기반 호스트에서 사용할 수 있는 OWIN 미들웨어 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-428">ASP.NET authentication is now based on OWIN middleware that can be used on any OWIN-based host.</span></span> <span data-ttu-id="0eaf7-429">OWIN에 대 한 자세한 내용은 다음을 참조 하십시오. [Microsoft OWIN 구성 요소](#TOC7) 섹션.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-429">For more information about OWIN, see the following [Microsoft OWIN Components](#TOC7) section.</span></span>

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a><span data-ttu-id="0eaf7-430">Microsoft OWIN 구성 요소</span><span class="sxs-lookup"><span data-stu-id="0eaf7-430">Microsoft OWIN Components</span></span>

<span data-ttu-id="0eaf7-431">[.NET 용 웹 인터페이스를 열고](http://owin.org/) (OWIN).NET 웹 서버와 웹 응용 프로그램 간의 추상화를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-431">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="0eaf7-432">OWIN 웹 응용 프로그램 호스트를 알 수 없는 하는 서버에서 웹 응용 프로그램을 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-432">OWIN decouples the web application from the server, making web applications host-agnostic.</span></span> <span data-ttu-id="0eaf7-433">예를 들어 IIS에서 OWIN 기반 웹 응용 프로그램을 호스팅할 수도 있고 사용자 지정 프로세스에서 자체 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-433">For example, you can host an OWIN-based web application in IIS or self-host it in a custom process.</span></span>

<span data-ttu-id="0eaf7-434">Microsoft OWIN 구성 요소 (Katana 프로젝트 라고도 함)에 도입 된 변경 내용을 새 서버와 호스트 구성 요소, 새로운 도우미 라이브러리 및 미들웨어 및 새로운 인증 미들웨어 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-434">Changes introduced in the Microsoft OWIN components (also known as the Katana project) include new server and host components, new helper libraries and middleware, and new authentication middleware.</span></span>

<span data-ttu-id="0eaf7-435">OWIN 및 Katana에 대 한 자세한 내용은 참조 [OWIN 및 Katana 새로운](../../../aspnet/overview/owin-and-katana/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-435">For more information about OWIN and Katana, see [What's new in OWIN and Katana](../../../aspnet/overview/owin-and-katana/index.md).</span></span>

<span data-ttu-id="0eaf7-436">**참고: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) 응용 프로그램 IIS 클래식 모드에서 실행할 수 없습니다; 통합된 모드에서 실행 해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-436">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications cannot run in IIS classic mode; they must be run in integrated mode.**</span></span>

<span data-ttu-id="0eaf7-437">**참고: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) 완전 신뢰에서 응용 프로그램을 실행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-437">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications must be run in full trust.**</span></span>

### <a name="new-servers-and-hosts"></a><span data-ttu-id="0eaf7-438">새 서버와 호스트</span><span class="sxs-lookup"><span data-stu-id="0eaf7-438">New Servers and Hosts</span></span>

<span data-ttu-id="0eaf7-439">이 릴리스에서 새 구성 요소는 자체 호스트 시나리오를 사용 하도록 설정에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-439">With this release, new components were added to enable self-host scenarios.</span></span> <span data-ttu-id="0eaf7-440">이러한 구성 요소는 다음과 같은 NuGet 패키지를 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-440">These components include the following NuGet packages:</span></span>

- <span data-ttu-id="0eaf7-441">**Microsoft.Owin.Host.HttpListener**합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-441">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="0eaf7-442">사용 하는 OWIN 서버 제공 **HttpListener** 하 OWIN 파이프라인에 지시 하 고 HTTP 요청을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-442">Provides an OWIN server that uses **HttpListener** to listen for HTTP requests and direct them into the OWIN pipeline.</span></span>
- <span data-ttu-id="0eaf7-443">**Microsoft.Owin.Hosting** 자체 콘솔 응용 프로그램 또는 Windows 서비스와 같은 사용자 지정 프로세스에서 OWIN 파이프라인을 호스트 하려는 개발자가 있는 라이브러리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-443">**Microsoft.Owin.Hosting** Provides a library for developers who wish to self-host an OWIN pipeline in a custom process, such as a console application or Windows service.</span></span>
- <span data-ttu-id="0eaf7-444">**OwinHost**합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-444">**OwinHost**.</span></span> <span data-ttu-id="0eaf7-445">래핑하는 독립 실행형 실행 파일을 제공 `Microsoft.Owin.Hosting` 자체 사용자 지정 호스트 응용 프로그램을 작성 하지 않고도 OWIN 파이프라인을 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-445">Provides a stand-alone executable that wraps `Microsoft.Owin.Hosting` and lets you self-host an OWIN pipeline without having to write a custom host application.</span></span>

<span data-ttu-id="0eaf7-446">또한는 `Microsoft.Owin.Host.SystemWeb` 패키지 수 있게 되었습니다. 힌트를 제공 하는 미들웨어는 **SystemWeb** 특정 ASP.NET 파이프라인 단계 동안 미들웨어를 호출 해야 함을 나타내는 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-446">In addition, the `Microsoft.Owin.Host.SystemWeb` package now enables middleware to provide hints to the **SystemWeb** server, indicating that the middleware should be called during a specific ASP.NET pipeline stage.</span></span> <span data-ttu-id="0eaf7-447">이 기능은 인증 미들웨어 초기 ASP.NET 파이프라인에에서 실행 되어야 하는 데 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-447">This feature is particularly useful for authentication middleware, which should run early in the ASP.NET pipeline.</span></span>

### <a name="helper-libraries-and-middleware"></a><span data-ttu-id="0eaf7-448">도우미 라이브러리 및 미들웨어</span><span class="sxs-lookup"><span data-stu-id="0eaf7-448">Helper Libraries and Middleware</span></span>

<span data-ttu-id="0eaf7-449">OWIN 사양에서 함수 및 유형 정의 사용 하는 OWIN 구성 요소를 작성할 수 있지만 새 `Microsoft.Owin` 패키지 보다 사용자 친화적인 집합의 추상화를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-449">Although you can write OWIN components using only the function and type definitions from the OWIN specification, the new `Microsoft.Owin` package provides a more user-friendly set of abstractions.</span></span> <span data-ttu-id="0eaf7-450">이 패키지는 여러 이전 패키지 결합 (예: `Owin.Extensions`, `Owin.Types`) 사용할 수 있는 다음 쉽게 다른 OWIN 구성 요소에서 단일, 잘 구성 된 개체 모델을 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-450">This package combines several earlier packages (e.g., `Owin.Extensions`, `Owin.Types`) into a single, well-structured object model that can then be easily used by other OWIN components.</span></span> <span data-ttu-id="0eaf7-451">실제로 대부분의 Microsoft OWIN 구성 요소는 이제이 패키지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-451">In fact, the majority of Microsoft OWIN components now use this package.</span></span>

> [!NOTE]
> <span data-ttu-id="0eaf7-452">[OWIN](http://www.owin.org) 응용 프로그램 IIS 클래식 모드에서 실행할 수 없습니다; 통합된 모드에서 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-452">[OWIN](http://www.owin.org) applications cannot run in IIS classic mode; they must be run in integrated mode.</span></span>

> [!NOTE]
> <span data-ttu-id="0eaf7-453">[OWIN](http://www.owin.org) 완전 신뢰에서 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-453">[OWIN](http://www.owin.org) applications must be run in full trust.</span></span>

<span data-ttu-id="0eaf7-454">이 릴리스에서 실행 중인 OWIN 응용 프로그램 유효성을 검사 하는 미들웨어와 오류를 조사 하는 데 오류 페이지 미들웨어를 포함 하는 Microsoft.Owin.Diagnostics 패키지용을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-454">This release also includes the Microsoft.Owin.Diagnostics package, which includes middleware to validate a running OWIN application, plus error-page middleware to help investigate failures.</span></span>

### <a name="authentication-components"></a><span data-ttu-id="0eaf7-455">인증 구성 요소</span><span class="sxs-lookup"><span data-stu-id="0eaf7-455">Authentication Components</span></span>

<span data-ttu-id="0eaf7-456">다음 인증 구성 요소가 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-456">The following authentication components are available.</span></span>

- <span data-ttu-id="0eaf7-457">**Microsoft.Owin.Security.ActiveDirectory**합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-457">**Microsoft.Owin.Security.ActiveDirectory**.</span></span> <span data-ttu-id="0eaf7-458">온-프레미스 또는 클라우드 기반 디렉터리 서비스를 사용 하 여 인증을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-458">Enables authentication using on-premise or cloud-based directory services.</span></span>
- <span data-ttu-id="0eaf7-459">**Microsoft.Owin.Security.Cookies** 쿠키를 사용 하 여 사용 하면 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-459">**Microsoft.Owin.Security.Cookies** Enables authentication using cookies.</span></span> <span data-ttu-id="0eaf7-460">이 패키지 변수의 이름이 이전에 `Microsoft.Owin.Security.Forms`합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-460">This package was previously named `Microsoft.Owin.Security.Forms`.</span></span>
- <span data-ttu-id="0eaf7-461">**Microsoft.Owin.Security.Facebook** Facebook의 OAuth 기반 서비스를 사용 하 여 사용 하면 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-461">**Microsoft.Owin.Security.Facebook** Enables authentication using Facebook's OAuth-based service.</span></span>
- <span data-ttu-id="0eaf7-462">**Microsoft.Owin.Security.Google** Google의 OpenID 기반 서비스를 사용 하 여 사용 하면 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-462">**Microsoft.Owin.Security.Google** Enables authentication using Google's OpenID-based service.</span></span>
- <span data-ttu-id="0eaf7-463">**Microsoft.Owin.Security.Jwt** JWT 토큰을 사용 하 여 사용 하면 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-463">**Microsoft.Owin.Security.Jwt** Enables authentication using JWT tokens.</span></span>
- <span data-ttu-id="0eaf7-464">**Microsoft.Owin.Security.MicrosoftAccount** Microsoft 계정을 사용 하 여 사용 하면 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-464">**Microsoft.Owin.Security.MicrosoftAccount** Enables authentication using Microsoft accounts.</span></span>
- <span data-ttu-id="0eaf7-465">**Microsoft.Owin.Security.OAuth**합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-465">**Microsoft.Owin.Security.OAuth**.</span></span> <span data-ttu-id="0eaf7-466">전달자 토큰을 인증 하기 위한에서는 OAuth 권한 부여 서버는 물론 미들웨어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-466">Provides an OAuth authorization server as well as middleware for authenticating bearer tokens.</span></span>
- <span data-ttu-id="0eaf7-467">**Microsoft.Owin.Security.Twitter** Twitter의 OAuth 기반 서비스를 사용 하 여 사용 하면 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-467">**Microsoft.Owin.Security.Twitter** Enables authentication using Twitter's OAuth-based service.</span></span>

<span data-ttu-id="0eaf7-468">또한이 릴리스는는 `Microsoft.Owin.Cors` 크로스-원본 HTTP 요청 처리에 대 한 미들웨어를 포함 하는 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-468">This release also includes the `Microsoft.Owin.Cors` package, which contains middleware for processing cross-origin HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="0eaf7-469">Visual Studio 2013의 최종 버전에서 JWT를 서명 하는 것에 대 한 지원이 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-469">Support for JWT signing has been removed in the final version of Visual Studio 2013.</span></span>

<a id="ef6"></a>
## <a name="entity-framework-6"></a><span data-ttu-id="0eaf7-470">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="0eaf7-470">Entity Framework 6</span></span>

<span data-ttu-id="0eaf7-471">새로운 기능 및 Entity Framework 6의 다른 변경의 목록이 참조 [Entity Framework 버전 기록이](https://msdn.com/data/jj574253)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-471">For a list of new features and other changes in Entity Framework 6, see [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a><span data-ttu-id="0eaf7-472">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="0eaf7-472">ASP.NET Razor 3</span></span>

<span data-ttu-id="0eaf7-473">ASP.NET Razor 3에는 다음과 같은 새로운 기능이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-473">ASP.NET Razor 3 includes the following new features:</span></span>

- <span data-ttu-id="0eaf7-474">탭에서 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-474">Support for Tab editing.</span></span> <span data-ttu-id="0eaf7-475">Preivously,는 **문서 서식** 사용 하는 경우 명령, 자동 들여쓰기 및 서식을 Visual Studio에서 자동 올바르게 작동 하지 않았습니다 고 **탭 유지** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-475">Preivously, the **Format Document** command, auto indenting, and auto formatting in Visual Studio did not work correctly when using the **Keep Tabs** option.</span></span> <span data-ttu-id="0eaf7-476">이 변경에는 Visual Studio 서식 탭에 대 한 Razor 코드에 대 한 서식을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-476">This change corrects Visual Studio formatting for Razor code for tab formatting.</span></span>
- <span data-ttu-id="0eaf7-477">링크를 생성 하는 경우 URL 재작성 규칙에 대 한 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-477">Support for URL Rewrite rules when generating links.</span></span>
- <span data-ttu-id="0eaf7-478">보안 투명 특성으로 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-478">Removal of security transparent attribute.</span></span>
 > [!NOTE]
 > <span data-ttu-id="0eaf7-479">이 주요 변경 내용, 고 Razor 3 호환 되지 않는 mvc 4 및 이전 버전에서는 동안 Razor 2 m v c 5 또는 m v c 5에 대해 컴파일된 어셈블리와 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-479">This is a breaking change, and makes Razor 3 incompatible with MVC4 and earlier, while Razor 2 is incompatible with MVC5 or assemblies compiled against MVC5.</span></span>

<span data-ttu-id="0eaf7-480">시험판 버전에서 Visual Studio 2013에서 해결 된 razor 3 문제 있습니다 [여기](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-480">Razor 3 issues fixed in Visual Studio 2013 from pre-release versions can be found [here](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a><span data-ttu-id="0eaf7-481">ASP.NET 앱 일시 중단</span><span class="sxs-lookup"><span data-stu-id="0eaf7-481">ASP.NET App Suspend</span></span>

<span data-ttu-id="0eaf7-482">ASP.NET 앱 일시 중단에는 사용자 환경 및 많은 수의 단일 컴퓨터에 ASP.NET 사이트를 호스팅하기 위한 경제 모델 근본적으로 변경 하는.NET Framework 4.5.1의에서 게임 변경 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-482">ASP.NET App Suspend is a game-changing feature in the .NET Framework 4.5.1 that radically changes the user experience and economic model for hosting large numbers of ASP.NET sites on a single machine.</span></span> <span data-ttu-id="0eaf7-483">자세한 내용은 참조 [ASP.NET 앱 일시 중단 – 응답 공유.NET 웹 호스팅](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-483">For more information, see [ASP.NET App Suspend – responsive shared .NET web hosting](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).</span></span>

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="0eaf7-484">알려진된 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="0eaf7-484">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="0eaf7-485">이 섹션에서는 Visual Studio 2013 용 ASP.NET 및 Web Tools의 주요 변경 내용 및 알려진된 문제를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-485">This section describes known issues and breaking changes in the ASP.NET and Web Tools for Visual Studio 2013.</span></span>

### <a name="nuget"></a><span data-ttu-id="0eaf7-486">NuGet</span><span class="sxs-lookup"><span data-stu-id="0eaf7-486">NuGet</span></span>

- <span data-ttu-id="0eaf7-487">[SLN 파일을 사용 하는 경우 새 패키지를 복원 모노에서 작동 하지 않습니다](https://nuget.codeplex.com/workitem/3596) – 예정 된 nuget.exe 다운로드에 수정 될 예정 및 [NuGet.CommandLine 패키지](http://www.nuget.org/packages/NuGet.CommandLine/) 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-487">[New package restore doesn't work on Mono when using SLN file](https://nuget.codeplex.com/workitem/3596) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="0eaf7-488">[새 패키지를 복원 Wix 프로젝트와 함께 작동 하지 않는](https://nuget.codeplex.com/workitem/3598) – 예정 된 nuget.exe 다운로드에 수정 될 예정 및 [NuGet.CommandLine 패키지](http://www.nuget.org/packages/NuGet.CommandLine/) 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-488">[New package restore doesn't work with Wix projects](https://nuget.codeplex.com/workitem/3598) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="0eaf7-489">[프로젝트는 솔루션 폴더에 대 한 자동 패키지 복원 작동 하지 않는](https://nuget.codeplex.com/workitem/3625) – NuGet 2.8에서 수정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-489">[Automatic Package restore doesn't work for projects under a solution folder](https://nuget.codeplex.com/workitem/3625) – will be fixed in NuGet 2.8.</span></span>

### <a name="aspnet-web-api"></a><span data-ttu-id="0eaf7-490">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="0eaf7-490">ASP.NET Web API</span></span>

1. <span data-ttu-id="0eaf7-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)`반환 하지 `IQueryable<T>` 에 대 한 지원을 추가 하는 대로 항상 `$select` 및 `$expand`합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)` doesn't return `IQueryable<T>` always, as we added support for `$select` and `$expand`.</span></span>

    <span data-ttu-id="0eaf7-492">에 대 한 이전 샘플 `ODataQueryOptions<T>` 항상 캐스팅할의 반환 값에서 `ApplyTo` 를 `IQueryable<T>`합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-492">Our earlier samples for `ODataQueryOptions<T>` always casted the return value from `ApplyTo` to `IQueryable<T>`.</span></span> <span data-ttu-id="0eaf7-493">이전에서는이 되는 쿼리 옵션 때문에 이전 작업을 지원 하는지 (`$filter`, `$orderby`, `$skip`, `$top`) 쿼리의 셰이프를 변경 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-493">This worked earlier because the query options that we supported earlier (`$filter`, `$orderby`, `$skip`, `$top`) do not change the shape of the query.</span></span> <span data-ttu-id="0eaf7-494">지원 했으므로 `$select` 및 `$expand` 반환 값을 `ApplyTo` 됩니다 `IQueryable<T>` 항상 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-494">Now that we support `$select` and `$expand` the return value from `ApplyTo` will not be `IQueryable<T>` always.</span></span>

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    <span data-ttu-id="0eaf7-495">클라이언트를 보내지 않는 경우 작업에서 이전 예제 코드를 사용 하는 경우 계속 `$select` 및 `$expand`합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-495">If you are using the sample code from earlier, it will continue working if the client does not send `$select` and `$expand`.</span></span> <span data-ttu-id="0eaf7-496">그러나 지원 하려는 경우 `$select` 및 `$expand` 이 코드를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-496">However, if you wish to support `$select` and `$expand` you have to change that code to this.</span></span>

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. <span data-ttu-id="0eaf7-497">**일괄 처리를 요청 하는 동안 Request.Url 나 RequestContext.Url null 임**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-497">**Request.Url or RequestContext.Url is null during a batch request**</span></span>

    <span data-ttu-id="0eaf7-498">일괄 처리 시나리오에서 **UrlHelper** 에서 액세스할 때 null **Request.Url** 또는 **RequestContext.Url**합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-498">In a batching scenario, **UrlHelper** is null when accessed from **Request.Url** or **RequestContext.Url**.</span></span>

    <span data-ttu-id="0eaf7-499">현재이 문제는 여기에 추적: [BatchRequestContext.Url은 요청을 일괄 처리에 대해 null](http://aspnetwebstack.codeplex.com/workitem/1301)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-499">This issue is currently tracked here: [BatchRequestContext.Url is null for batching request](http://aspnetwebstack.codeplex.com/workitem/1301).</span></span>

    <span data-ttu-id="0eaf7-500">새 인스턴스를 만드는 것이 문제에 대 한 해결 **UrlHelper**다음 예제와 같이,:</span><span class="sxs-lookup"><span data-stu-id="0eaf7-500">The workaround for this issue is to create a new instance of **UrlHelper**, as in the following example:</span></span>

    <span data-ttu-id="0eaf7-501">**UrlHelper의 새 인스턴스 만들기**</span><span class="sxs-lookup"><span data-stu-id="0eaf7-501">**Creating a new instance of UrlHelper**</span></span>

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a><span data-ttu-id="0eaf7-502">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="0eaf7-502">ASP.NET MVC</span></span>

1. <span data-ttu-id="0eaf7-503">를 사용할 때는 m v c 5 OrgAuth, AntiForgerToken 유효성 검사를 수행 하는 보기가 있는 경우 보기에 데이터를 게시 하면 다음 오류를 발견할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-503">When using MVC5 and OrgAuth, if you have views which do AntiForgerToken validation, you might come across the following error when you post data to the view:</span></span>

    <span data-ttu-id="0eaf7-504">**오류**:</span><span class="sxs-lookup"><span data-stu-id="0eaf7-504">**Error**:</span></span>

    <span data-ttu-id="0eaf7-505">*'/' 응용 프로그램에서 서버 오류입니다.*</span><span class="sxs-lookup"><span data-stu-id="0eaf7-505">*Server Error in '/' Application.*</span></span>

    <span data-ttu-id="0eaf7-506">*클레임 형식 'http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier' 또는 'http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider'의 제공 된 ClaimsIdentity에 표시 되지 않았습니다. 위조 방지 토큰 지원 클레임 기반 인증을 사용 하도록 설정 하려면 구성 된 클레임 공급자 생성 ClaimsIdentity 인스턴스에서 이러한 클레임의 둘 다 제공할가 있는지 확인 하십시오. 구성 된 클레임 공급자 대신 다른 클레임 유형에 사용 하 여 고유 식별자로, AntiForgeryConfig.UniqueClaimTypeIdentifier 정적 속성을 설정 하 여 구성할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="0eaf7-506">*A claim of type 'http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier' or 'http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider' was not present on the provided ClaimsIdentity. To enable anti-forgery token support with claims-based authentication, please verify that the configured claims provider is providing both of these claims on the ClaimsIdentity instances it generates. If the configured claims provider instead uses a different claim type as a unique identifier, it can be configured by setting the static property AntiForgeryConfig.UniqueClaimTypeIdentifier.*</span></span>

    <span data-ttu-id="0eaf7-507">**해결 방법**:</span><span class="sxs-lookup"><span data-stu-id="0eaf7-507">**Workaround**:</span></span>

    <span data-ttu-id="0eaf7-508">해결 하는 Global.asax에 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-508">Add the following line in Global.asax to fix it:</span></span>

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    <span data-ttu-id="0eaf7-509">그러면 다음 릴리스에 대 한 수정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-509">This will be fixed for the next release.</span></span>
2. <span data-ttu-id="0eaf7-510">Mvc 4 응용 m v c 5로 업그레이드 한 후 솔루션을 빌드하고 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-510">After upgrading an MVC4 app to MVC5, build the solution and launch it.</span></span> <span data-ttu-id="0eaf7-511">다음과 같은 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-511">You should see the following error:</span></span>

    <span data-ttu-id="0eaf7-512">[A] System.Web.WebPages.Razor.Configuration.HostSection [B]System.Web.WebPages.Razor.Configuration.HostSection으로 캐스팅할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-512">[A]System.Web.WebPages.Razor.Configuration.HostSection cannot be cast to [B]System.Web.WebPages.Razor.Configuration.HostSection.</span></span> <span data-ttu-id="0eaf7-513">A 형식 발생 ' System.Web.WebPages.Razor, Version = 2.0.0.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35' 컨텍스트에서 'Default' 위치에 ' C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\ v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-513">Type A originates from 'System.Web.WebPages.Razor, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'.</span></span> <span data-ttu-id="0eaf7-514">B 형식 발생 ' System.Web.WebPages.Razor, Version 3.0.0.0, Culture = neutral, PublicKeyToken = = 31bf3856ad364e35' 컨텍스트의 'Default' 위치에 ' C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\ e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-514">Type B originates from 'System.Web.WebPages.Razor, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.</span></span>

    <span data-ttu-id="0eaf7-515">위의 오류를 해결 하려면 열고 *모든* 프로젝트 및 다음을 수행에 Web.config 파일 (Views 폴더에 있는 구성을 포함):</span><span class="sxs-lookup"><span data-stu-id="0eaf7-515">To fix the above error, open *all* the Web.config files (including the ones in the Views folder) in your project and do the following:</span></span>

    1. <span data-ttu-id="0eaf7-516">버전 "4.0.0.0"의 "System.Web.Mvc"를 "5.0.0.0"의 모든 항목을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-516">Update all occurrences of version "4.0.0.0" of "System.Web.Mvc" to "5.0.0.0".</span></span>
    2. <span data-ttu-id="0eaf7-517">"System.Web.Helpers"의 "2.0.0.0" 버전의 항목을 모두 업데이트 &quot;System.Web.WebPages&quot; 및 &quot;System.Web.WebPages.Razor&quot; "3.0.0.0"를</span><span class="sxs-lookup"><span data-stu-id="0eaf7-517">Update all occurrences of version "2.0.0.0" of "System.Web.Helpers", &quot;System.Web.WebPages&quot; and &quot;System.Web.WebPages.Razor&quot; to "3.0.0.0"</span></span>

    <span data-ttu-id="0eaf7-518">예를 들어 위의 변경을 수행한 후 어셈블리 바인딩 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-518">For example, after you make the above changes, the assembly bindings should look like this:</span></span>

    [!code-xml[Main](release-notes/samples/sample24.xml)]

    <span data-ttu-id="0eaf7-519">MVC 5로 MVC 4 프로젝트 업그레이드에 대 한 자세한 내용은 참조 하십시오. [ASP.NET MVC 4 및 Web API 프로젝트를 ASP.NET MVC 5 및 Web API 2로 업그레이드 하는 방법을](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-519">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>
3. <span data-ttu-id="0eaf7-520">유효성 검사 비 가시적인 jQuery 함께 클라이언트 쪽 유효성 검사를 사용 하면 유효성 검사 메시지 올바르지 않을 경우에 따라 형식과 HTML input 요소에 대 한 = 'number'.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-520">When using client-side validation with jQuery Unobtrusive Validation, the validation message is sometimes incorrect for an HTML input element with type='number'.</span></span> <span data-ttu-id="0eaf7-521">유효성 검사 오류에 대해 필요한 값 ("The이 지 필드는 필수")가 표시 유효한 숫자가 필수임 올바른 메시지 대신 잘못 된 숫자 입력 된 경우.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-521">The validation error for a required value ("The Age field is required") is shown when an invalid number is entered instead of the correct message that a valid number is required.</span></span>

    <span data-ttu-id="0eaf7-522">이 문제는 일반적으로 만들기 및 편집 보기에는 정수 속성을 사용 하 여 모델에 대 한 스 캐 폴드 코드로 발견 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-522">This issue is commonly found with scaffolded code for a model with an integer property on the Create and Edit views.</span></span>

    <span data-ttu-id="0eaf7-523">이 문제를 해결 하려면 편집기 도우미를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-523">To work around this issue, change the editor helper from:</span></span>

    `@Html.EditorFor(person => person.Age)`

    <span data-ttu-id="0eaf7-524">대상:</span><span class="sxs-lookup"><span data-stu-id="0eaf7-524">To:</span></span>

    `@Html.TextBoxFor(person => person.Age)`
4. <span data-ttu-id="0eaf7-525">ASP.NET MVC 5 부분 신뢰를 더 이상 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-525">ASP.NET MVC 5 no longer supports partial trust.</span></span> <span data-ttu-id="0eaf7-526">MVC 또는 WebAPI 바이너리에 연결 하는 프로젝트를 제거 해야는 [SecurityTransparent](https://msdn.microsoft.com/en-us/library/system.security.securitytransparentattribute.aspx) 특성 및 [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/en-us/library/system.security.allowpartiallytrustedcallersattribute.aspx) 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-526">Projects linking to the MVC or WebAPI binaries should remove the [SecurityTransparent](https://msdn.microsoft.com/en-us/library/system.security.securitytransparentattribute.aspx) attribute and the [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/en-us/library/system.security.allowpartiallytrustedcallersattribute.aspx) attribute.</span></span> <span data-ttu-id="0eaf7-527">이러한 특성을 제거 하면 다음과 같은 컴파일러 오류 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-527">Removing these attributes will eliminate compiler errors such as the following.</span></span>

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > <span data-ttu-id="0eaf7-528">단,이 사용자의 부작용으로 사용할 수 없습니다 4.0 및 5.0 어셈블리 같은 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-528">Note, as a side effect of this you cannot use 4.0 and 5.0 assemblies in the same application.</span></span> <span data-ttu-id="0eaf7-529">5.0에이 모두 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-529">You need to update all of them to 5.0.</span></span>

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a><span data-ttu-id="0eaf7-530">웹 사이트는 인트라넷 영역에서 호스트 하면서 Facebook 인증 인 SPA 템플릿을 IE에서 불안정 해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-530">SPA Template with Facebook authorization may cause instability in IE while the web site is hosted in intranet zone</span></span>

<span data-ttu-id="0eaf7-531">SPA 템플릿은 Facebook 사용 하 여 외부 로그를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-531">The SPA template provides external log in with Facebook.</span></span> <span data-ttu-id="0eaf7-532">템플릿을 사용 하 여 만든 프로젝트는 로컬로 실행 되는 경우 IE 작동이 중단 됩니다. 로그인에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-532">When the project created with the template is running locally, signing in may cause IE to crash.</span></span>

<span data-ttu-id="0eaf7-533">해결책:</span><span class="sxs-lookup"><span data-stu-id="0eaf7-533">Solution:</span></span>

1. <span data-ttu-id="0eaf7-534">인터넷 영역;에서 웹 사이트를 호스팅하거나 또는</span><span class="sxs-lookup"><span data-stu-id="0eaf7-534">Host the web site in internet zone; or</span></span>

2. <span data-ttu-id="0eaf7-535">IE 이외의 브라우저에서 시나리오를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-535">Test the scenario in a browser other than IE.</span></span>

### <a name="web-forms-scaffolding"></a><span data-ttu-id="0eaf7-536">Web Forms 스 캐 폴딩</span><span class="sxs-lookup"><span data-stu-id="0eaf7-536">Web Forms Scaffolding</span></span>

<span data-ttu-id="0eaf7-537">Web Forms 스 캐 폴딩 VS2013에서 제거 되었습니다 및 Visual Studio에 대 한 향후 업데이트에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-537">Web Forms Scaffolding has been removed from VS2013 and will be available in a future update to Visual Studio.</span></span> <span data-ttu-id="0eaf7-538">그러나 Web Forms 프로젝트 내에서 스 캐 폴딩 MVC 종속성을 추가 하 고 스 캐 폴딩 MVC에 대해 생성 하 여 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-538">However, you can still use scaffolding within a Web Forms project by adding MVC dependencies and generating scaffolding for MVC.</span></span> <span data-ttu-id="0eaf7-539">프로젝트는 Web Forms 및 MVC의 조합을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-539">Your project will contain a combination of Web Forms and MVC.</span></span>

<span data-ttu-id="0eaf7-540">MVC Web Forms 프로젝트를 추가 하려면 새 스 캐 폴드 항목을 추가 하 고 선택 **MVC 5 종속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-540">To add MVC to your Web Forms project, add a new scaffolded item and select **MVC 5 Dependencies**.</span></span> <span data-ttu-id="0eaf7-541">최소 또는 스크립트와 같은 콘텐츠 파일의 모든 해야 하는지 여부에 따라 전체 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-541">Select either Minimal or Full depending on whether you need all of the content files, such as scripts.</span></span> <span data-ttu-id="0eaf7-542">Mvc 프로젝트의 뷰 및 컨트롤러를 생성 하는 스 캐 폴드 된 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-542">Then, add a scaffolded item for MVC, which will create views and a controller in your project.</span></span>

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="0eaf7-543">MVC 및 Web API 스 캐 폴딩-HTTP 404 찾을 수 없음 오류</span><span class="sxs-lookup"><span data-stu-id="0eaf7-543">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="0eaf7-544">프로젝트에 스 캐 폴드 된 항목을 추가할 때 오류가 발생 있기 프로젝트 일관성 없는 상태로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-544">If an error is encountered when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="0eaf7-545">스 캐 폴딩 수 변경 중 일부는 롤백할 수 있지만 설치 된 NuGet 패키지와 같은 다른 변경 내용을 다시 롤백되며 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-545">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="0eaf7-546">라우팅 구성 변경 내용이 롤백되어도 경우 스 캐 폴드 항목으로 이동 하는 경우 사용자가 HTTP 404 오류를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-546">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="0eaf7-547">해결 방법:</span><span class="sxs-lookup"><span data-stu-id="0eaf7-547">Workaround:</span></span>

- <span data-ttu-id="0eaf7-548">MVC에 대 한이 오류를 해결 하려면 새 스 캐 폴드 항목을 추가 하 고 MVC 5 종속성 선택 (최소 또는 전체).</span><span class="sxs-lookup"><span data-stu-id="0eaf7-548">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="0eaf7-549">이 프로세스의 모든 필요한 변경 사항을 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-549">This process will add all of the required changes to your project.</span></span>
- <span data-ttu-id="0eaf7-550">웹 API에 대 한이 오류를 해결 하려면:</span><span class="sxs-lookup"><span data-stu-id="0eaf7-550">To fix this error for Web API:</span></span>

    1. <span data-ttu-id="0eaf7-551">프로젝트에 경우 WebApiConfig 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-551">Add the WebApiConfig class to your project.</span></span>

        [!code-csharp[Main](release-notes/samples/sample25.cs)]

        [!code-vb[Main](release-notes/samples/sample26.vb)]
    2. <span data-ttu-id="0eaf7-552">응용 프로그램에서 WebApiConfig.Register 구성\_Global.asax에 다음과 같이 메서드를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eaf7-552">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

        [!code-csharp[Main](release-notes/samples/sample27.cs)]

        [!code-vb[Main](release-notes/samples/sample28.vb)]
