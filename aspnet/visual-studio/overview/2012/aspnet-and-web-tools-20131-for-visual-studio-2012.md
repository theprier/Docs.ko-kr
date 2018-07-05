---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: ASP.NET 및 Visual Studio 2012 용 웹 도구 2013.1 릴리스 정보 | Microsoft Docs
author: microsoft
description: 이 문서에서는 Visual Studio 2012 용 ASP.NET 및 웹 도구 2013.1 릴리스를 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/13/2013
ms.topic: article
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
ms.technology: ''
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 85cd45c25e0f2ad3c8d6d6de73a1a493533e7f7b
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374262"
---
<a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="7f10d-103">ASP.NET 및 Visual Studio 2012 용 웹 도구 2013.1 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="7f10d-103">Release Notes for ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>
====================
<span data-ttu-id="7f10d-104">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="7f10d-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="7f10d-105">이 문서에서는 Visual Studio 2012 용 ASP.NET 및 웹 도구 2013.1 릴리스를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-105">This document describes the release of ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>


## <a name="contents"></a><span data-ttu-id="7f10d-106">목차</span><span class="sxs-lookup"><span data-stu-id="7f10d-106">Contents</span></span>

- [<span data-ttu-id="7f10d-107">설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="7f10d-107">Installation Notes</span></span>](#install)
- [<span data-ttu-id="7f10d-108">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="7f10d-108">Software Requirements</span></span>](#requirements)
- <span data-ttu-id="7f10d-109">ASP.NET 및 Visual Studio 2012 용 웹 도구 2013.1의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="7f10d-109">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

    - [<span data-ttu-id="7f10d-110">부트스트랩</span><span class="sxs-lookup"><span data-stu-id="7f10d-110">Bootstrap</span></span>](#bootstrap)
    - [<span data-ttu-id="7f10d-111">템플릿</span><span class="sxs-lookup"><span data-stu-id="7f10d-111">Templates</span></span>](#templates)

        - [<span data-ttu-id="7f10d-112">ASP.NET MVC 5 템플릿에서</span><span class="sxs-lookup"><span data-stu-id="7f10d-112">ASP.NET MVC 5 template</span></span>](#mvc5template)
        - [<span data-ttu-id="7f10d-113">ASP.NET Web API 2 템플릿</span><span class="sxs-lookup"><span data-stu-id="7f10d-113">ASP.NET Web API 2 template</span></span>](#apitemplate)
        - [<span data-ttu-id="7f10d-114">항목 템플릿</span><span class="sxs-lookup"><span data-stu-id="7f10d-114">Item Templates</span></span>](#itemtemplate)
    - [<span data-ttu-id="7f10d-115">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="7f10d-115">Entity Framework 6</span></span>](#ef6)
    - [<span data-ttu-id="7f10d-116">ASP.NET 스 캐 폴딩</span><span class="sxs-lookup"><span data-stu-id="7f10d-116">ASP.NET Scaffolding</span></span>](#scaffold)
    - [<span data-ttu-id="7f10d-117">Razor 편집기</span><span class="sxs-lookup"><span data-stu-id="7f10d-117">Razor Editor</span></span>](#razor)
    - [<span data-ttu-id="7f10d-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="7f10d-118">NuGet 2.7</span></span>](#nuget)
- <span data-ttu-id="7f10d-119">알려진된 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="7f10d-119">Known Issues and Breaking Changes</span></span>

    - [<span data-ttu-id="7f10d-120">ASP.NET 스 캐 폴딩</span><span class="sxs-lookup"><span data-stu-id="7f10d-120">ASP.NET Scaffolding</span></span>](#issuescaffolding)

        - [<span data-ttu-id="7f10d-121">MVC 및 Web API 스 캐 폴딩-HTTP 404 찾을 수 없음 오류</span><span class="sxs-lookup"><span data-stu-id="7f10d-121">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>](#404issue)
        - [<span data-ttu-id="7f10d-122">Visual Studio Express 2012 for Web 스 캐 폴드 된 항목을 추가한 후 작동이 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-122">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>](#expressissue)
    - [<span data-ttu-id="7f10d-123">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="7f10d-123">ASP.NET Razor 3</span></span>](#issuerazor)

        - [<span data-ttu-id="7f10d-124">서버 오류가 발생 하는 브라우저 또는 f5 키를 사용 하 여 cshtml 파일 보기</span><span class="sxs-lookup"><span data-stu-id="7f10d-124">Viewing cshtml file with Browse With or F5 causes a server error</span></span>](#browseissue)
        - [<span data-ttu-id="7f10d-125">Url 재작성 및 Tilde(~)</span><span class="sxs-lookup"><span data-stu-id="7f10d-125">Url Rewrite and Tilde(~)</span></span>](#rewriteissue)
    - [<span data-ttu-id="7f10d-126">템플릿</span><span class="sxs-lookup"><span data-stu-id="7f10d-126">Templates</span></span>](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a><span data-ttu-id="7f10d-127">설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="7f10d-127">Installation Notes</span></span>

<span data-ttu-id="7f10d-128">[설치](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET 및 웹 도구 2013.1 Visual Studio 2012 용입니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-128">[Install](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="7f10d-129">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="7f10d-129">Software Requirements</span></span>

<span data-ttu-id="7f10d-130">Visual Studio 2012 또는 Visual Studio Express 2012 for Web 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-130">You must have either Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="7f10d-131">ASP.NET 및 Visual Studio 2012 용 웹 도구 2013.1의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="7f10d-131">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<a id="bootstrap"></a>
### <a name="bootstrap"></a><span data-ttu-id="7f10d-132">부트스트랩</span><span class="sxs-lookup"><span data-stu-id="7f10d-132">Bootstrap</span></span>

<span data-ttu-id="7f10d-133">보기에 대 한 태그를 사용 하 여 MVC 5 컨트롤러와 뷰 스 캐 폴드 하는 경우 [부트스트랩](http://getbootstrap.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-133">When you scaffold MVC 5 controllers and views, the markup for the views uses [Bootstrap](http://getbootstrap.com/).</span></span>

<a id="templates"></a>
### <a name="templates"></a><span data-ttu-id="7f10d-134">템플릿</span><span class="sxs-lookup"><span data-stu-id="7f10d-134">Templates</span></span>

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a><span data-ttu-id="7f10d-135">ASP.NET MVC 5 템플릿에서</span><span class="sxs-lookup"><span data-stu-id="7f10d-135">ASP.NET MVC 5 template</span></span>

<span data-ttu-id="7f10d-136">새 MVC 5 템플릿을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-136">We added a new MVC 5 template.</span></span> <span data-ttu-id="7f10d-137">최신 MVC 5 NuGet 패키지 참조 및 스 캐 폴딩 컨트롤러 및 뷰를 추가 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-137">It references the latest MVC 5 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a><span data-ttu-id="7f10d-138">ASP.NET Web API 2 템플릿</span><span class="sxs-lookup"><span data-stu-id="7f10d-138">ASP.NET Web API 2 template</span></span>

<span data-ttu-id="7f10d-139">새 Web API 2 템플릿을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-139">We added a new Web API 2 template.</span></span> <span data-ttu-id="7f10d-140">최신 웹 API 2 NuGet 패키지 참조 및 스 캐 폴딩 컨트롤러 및 뷰를 추가 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-140">It references the latest Web API 2 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="itemtemplate"></a>
#### <a name="item-templates"></a><span data-ttu-id="7f10d-141">항목 템플릿</span><span class="sxs-lookup"><span data-stu-id="7f10d-141">Item Templates</span></span>

<span data-ttu-id="7f10d-142">MVC 5 뷰, 웹 페이지 (Razor 3) 및 Web API 2 컨트롤러에 대 한 새 항목 템플릿을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-142">We added new item templates for MVC 5 views, Web Pages (Razor 3), and Web API 2 controllers.</span></span> <span data-ttu-id="7f10d-143">새 항목을 추가 하는 동안 프로젝트에 관련 된 NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-143">They install the related NuGet packages to the project while adding new items.</span></span>

<a id="ef6"></a>
### <a name="entity-framework-6"></a><span data-ttu-id="7f10d-144">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="7f10d-144">Entity Framework 6</span></span>

<span data-ttu-id="7f10d-145">Entity Framework를 사용 하 여 MVC 또는 Web API 컨트롤러를 스 캐 폴딩 하면 Framework 6을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-145">When you scaffold an MVC or Web API controller using Entity Framework, we use Framework 6.</span></span> <span data-ttu-id="7f10d-146">Entity Framework에 대 한 자세한 내용은 참조는 [Entity Framework 버전 기록이](https://msdn.com/data/jj574253)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-146">For more information about Entity Framework, see the [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<span data-ttu-id="7f10d-147">또한 다운로드 하 고 Visual Studio 2012에 대 한 Entity Framework 6 도구를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-147">You can also download and install the Entity Framework 6 Tools for Visual Studio 2012.</span></span> <span data-ttu-id="7f10d-148">참조 된 [Entity Framework 가져오기](https://msdn.com/data/ee712906#tooling)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-148">See the [Get Entity Framework](https://msdn.com/data/ee712906#tooling).</span></span>

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="7f10d-149">ASP.NET 스 캐 폴딩</span><span class="sxs-lookup"><span data-stu-id="7f10d-149">ASP.NET Scaffolding</span></span>

<span data-ttu-id="7f10d-150">ASP.NET 스 캐 폴딩은 ASP.NET 웹 응용 프로그램에 대 한 코드 생성 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="7f10d-150">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="7f10d-151">쉽게 데이터 모델과 상호 작용 하는 프로젝트에 상용구 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-151">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="7f10d-152">이전 버전의 Visual Studio에서 스 캐 폴딩 ASP.NET MVC 프로젝트에 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-152">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="7f10d-153">이 업데이트를 Web Forms를 비롯 한 모든 ASP.NET 프로젝트에 대 한 스 캐 폴딩을 이제 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-153">With this update, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="7f10d-154">이 업데이트를 Web Forms 프로젝트에 대 한 생성 페이지를 지원 하지 않습니다 하지만 프로젝트에 MVC 종속성을 추가 하 여 Web forms 스 캐 폴딩을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-154">This update does not support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="7f10d-155">Web Forms에 대 한 페이지를 생성 하는 것에 대 한 지원이 향후 업데이트에서 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-155">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="7f10d-156">스 캐 폴딩을 사용 하는 경우 프로젝트의 종속성이 설치 되어 필요한 모든 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-156">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="7f10d-157">예를 들어, ASP.NET Web Forms 프로젝트를 시작 하 고 다음 스 캐 폴딩을 사용 하 여 Web API 컨트롤러를 추가할 경우 필요한 NuGet 패키지와 참조를 프로젝트에 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-157">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="7f10d-158">MVC 스 캐 폴딩에 Web Forms 프로젝트를 추가 하려면 추가 된 **새 스 캐 폴드 된 항목** 선택한 **MVC 5 종속성** 대화 상자에서.</span><span class="sxs-lookup"><span data-stu-id="7f10d-158">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="7f10d-159">두 가지 옵션이 있습니다; MVC 스 캐 폴딩에 대 한 최소 및 전체.</span><span class="sxs-lookup"><span data-stu-id="7f10d-159">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="7f10d-160">최소를 선택 하면 프로젝트에 NuGet 패키지 및 ASP.NET MVC에 대 한 참조만 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-160">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="7f10d-161">전체 옵션을 선택 하는 경우 MVC 프로젝트에 필요한 콘텐츠 파일 뿐만 아니라 최소한의 종속성에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-161">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="7f10d-162">Entity Framework 6에서 새 비동기 기능을 사용 하는 비동기 컨트롤러 스 캐 폴딩에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="7f10d-162">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="7f10d-163">자세한 내용 및 자습서를 참조 하세요 [ASP.NET 스 캐 폴딩 개요](../2013/aspnet-scaffolding-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-163">For more information and tutorials, see [ASP.NET Scaffolding Overview](../2013/aspnet-scaffolding-overview.md).</span></span> <span data-ttu-id="7f10d-164">이러한 자습서에는 Visual Studio 2013을 사용 하 여 스 캐 폴딩을 보여 줍니다. 하지만 ASP.NET 및 Visual Studio 2012 용 웹 도구 2013.1에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-164">These tutorials show scaffolding with Visual Studio 2013, but they are also applicable to ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="razor"></a>
### <a name="razor-editor"></a><span data-ttu-id="7f10d-165">Razor 편집기</span><span class="sxs-lookup"><span data-stu-id="7f10d-165">Razor Editor</span></span>

<span data-ttu-id="7f10d-166">이 업데이트를 사용 하 여 Visual Studio 2012는 이제 Razor 3 도구/편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-166">With this update, Visual Studio 2012 now supports Razor 3 tooling/editing.</span></span>

<a id="nuget"></a>
### <a name="nuget-27"></a><span data-ttu-id="7f10d-167">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="7f10d-167">NuGet 2.7</span></span>

<span data-ttu-id="7f10d-168">NuGet 2.7에 자세히 설명 하는 새로운 기능의 다양 한 집합을 포함 [NuGet 2.7 릴리스 정보](http://docs.nuget.org/docs/release-notes/nuget-2.7)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-168">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="7f10d-169">이 버전의 NuGet이 누락 된 패키지를 복원 하려면 NuGet을 명시적으로 허용 하는 사용자에 대 한 필요성을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-169">This version of NuGet removes the need for users to explicitly allow NuGet to restore missing packages.</span></span> <span data-ttu-id="7f10d-170">NuGet 2.7의 경우 사용자를 암시적으로 설치 하는 경우 자동으로 누락 된 패키지를 복원에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-170">When installing NuGet 2.7, users implicitly consent to automatically restoring missing packages.</span></span> <span data-ttu-id="7f10d-171">사용자는 Visual Studio에서 NuGet 설정을 통해 패키지 복원에서 명시적으로 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-171">Users can explicitly opt out of package restoration through the NuGet settings in Visual Studio.</span></span> <span data-ttu-id="7f10d-172">이 변경은 패키지 복원의 작동 원리를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-172">This change simplifies how package restoration works.</span></span>

## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="7f10d-173">알려진된 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="7f10d-173">Known Issues and Breaking Changes</span></span>

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="7f10d-174">ASP.NET 스 캐 폴딩</span><span class="sxs-lookup"><span data-stu-id="7f10d-174">ASP.NET Scaffolding</span></span>

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="7f10d-175">MVC 및 Web API 스 캐 폴딩-HTTP 404 찾을 수 없음 오류</span><span class="sxs-lookup"><span data-stu-id="7f10d-175">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="7f10d-176">프로젝트에 스 캐 폴드 된 항목을 추가할 때 오류가 발생 하면 경우 프로젝트가 일관성 없는 상태로 남게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-176">If you encounter an error when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="7f10d-177">변경 내용 스 캐 폴딩 수 중 일부를 롤백할 수 있지만 설치 된 NuGet 패키지와 같은 다른 변경 내용을 다시 롤백할 수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-177">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="7f10d-178">라우팅 구성 변경 내용이 롤백되어도 경우 스 캐 폴드 항목으로 이동 하는 경우 사용자는 HTTP 404 오류를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-178">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="7f10d-179">MVC에 대 한이 오류를 해결 하려면 새 스 캐 폴드 된 항목을 추가 하 고 MVC 5 종속성 선택 (최소 또는 전체).</span><span class="sxs-lookup"><span data-stu-id="7f10d-179">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="7f10d-180">이 프로세스에서 필요한 변경의 모든 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-180">This process will add all of the required changes to your project.</span></span>

<span data-ttu-id="7f10d-181">웹 API에 대 한이 오류를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-181">To fix this error for Web API:</span></span>

1. <span data-ttu-id="7f10d-182">프로젝트에 다음 WebApiConfig 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-182">Add the following WebApiConfig class to your project.</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. <span data-ttu-id="7f10d-183">응용 프로그램에서 WebApiConfig.Register 구성\_Global.asax에서 다음과 같은 메서드를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-183">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a><span data-ttu-id="7f10d-184">Visual Studio Express 2012 for Web 스 캐 폴드 된 항목을 추가한 후 작동이 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-184">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>

<span data-ttu-id="7f10d-185">Visual Studio Express 2012 for Web (예: Web API 2 컨트롤러 작업을 사용 하 여 Entity Framework를 사용 하 여) Entity Framework와 함께 스 캐 폴드 된 항목을 추가한 후 작동을 멈출 경우는 어셈블리의 네이티브 이미지를 로드 하지 못했습니다 Visual Studio Express System.Web.Extensions에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-185">If Visual Studio Express 2012 for Web stops working after adding scaffolded item with Entity Framework (such as Web API 2 Controller with actions, using Entity Framework), it is possible that Visual Studio Express failed to load the native image of an assembly dependent on System.Web.Extensions.</span></span>

<span data-ttu-id="7f10d-186">이 문제를 해결 하려면 Visual Studio Express System.Web.Extensions MSIL 이미지와 함께 작동 하도록을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-186">To correct this problem, configure Visual Studio Express to work with the MSIL image of System.Web.Extensions:</span></span>

1. <span data-ttu-id="7f10d-187">관리자 모드에서 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-187">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="7f10d-188">%ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE 또는 (64 비트 Windows)에 대 한 %Programfiles(x86)% %\Microsoft Visual Studio 11.0\Common7\IDE로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-188">Go to %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE or %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (for 64 bit Windows).</span></span>
3. <span data-ttu-id="7f10d-189">VWDExpress.exe.config 텍스트 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-189">Open VWDExpress.exe.config in a text editor.</span></span>
4. <span data-ttu-id="7f10d-190">아래에 다음 줄을 추가 합니다 &lt;configuration&gt;/&lt;런타임&gt; 요소:</span><span class="sxs-lookup"><span data-stu-id="7f10d-190">Add the following line under the &lt;configuration&gt;/&lt;runtime&gt; element:</span></span>  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. <span data-ttu-id="7f10d-191">다시 Visual Studio Express 2012 for Web.</span><span class="sxs-lookup"><span data-stu-id="7f10d-191">Restart Visual Studio Express 2012 for Web.</span></span>

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a><span data-ttu-id="7f10d-192">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="7f10d-192">ASP.NET Razor 3</span></span>

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-withbrowse-withorf5causes-a-server-error"></a><span data-ttu-id="7f10d-193">Cshtml 파일 withBrowse WithorF5causes 서버 오류 보기</span><span class="sxs-lookup"><span data-stu-id="7f10d-193">Viewing cshtml file withBrowse WithorF5causes a server error</span></span>

<span data-ttu-id="7f10d-194">-없다는 오류가 표시는 Visual Studio 2012 (또는 Visual Studio 2013에서 만든 Visual Studio 2012는 MVC 5 프로젝트에서 열기)에서 MVC 5 프로젝트 만들기를 cshtml 파일을 사용 하 여 찾아보기 또는 f5 키를 사용 하 여 보려고 **에서 서버 오류 '/' 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-194">When you create an MVC 5 project in Visual Studio 2012 (or open in Visual Studio 2012 an MVC 5 project that was created in Visual Studio 2013) and attempt to view a cshtml file by using Browse With or F5, you will receive an error that states - **Server Error in '/' Application**.</span></span> <span data-ttu-id="7f10d-195">서버를 탐색 하려고 합니다. `http://localhost:XXXX/Views/../XXXX.cshtml`</span><span class="sxs-lookup"><span data-stu-id="7f10d-195">The server attempts to navigate to `http://localhost:XXXX/Views/../XXXX.cshtml`</span></span>

<span data-ttu-id="7f10d-196">이 문제를 해결 하려면 변경 된 **시작 작업** 하기 위해 프로젝트에서 설정 **특정 페이지**합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-196">To resolve this issue, change the **Start Action** setting in your project to **Specific Page**.</span></span> <span data-ttu-id="7f10d-197">페이지에 대 한 값을 제공할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-197">You do not need to provide a value for the page.</span></span>

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

<span data-ttu-id="7f10d-198">이렇게 변경한 후 f5 키를 선택 하면 이동할 응용 프로그램의 루트 (`http://localhost:XXXX`).</span><span class="sxs-lookup"><span data-stu-id="7f10d-198">After making this change, selecting F5 navigates to the root of your application (`http://localhost:XXXX`).</span></span> <span data-ttu-id="7f10d-199">이 동작은 다릅니다 Visual Studio 2013에서 MVC 5 프로젝트에 대 한 동작으로 위치를 **현재 페이지** 설정 페이지 열기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-199">This behavior is not the same as the behavior for MVC 5 projects in Visual Studio 2013, where the **Current Page** setting launches the open page.</span></span>

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a><span data-ttu-id="7f10d-200">Url 재작성 및 Tilde(~)</span><span class="sxs-lookup"><span data-stu-id="7f10d-200">Url Rewrite and Tilde(~)</span></span>

<span data-ttu-id="7f10d-201">ASP.NET Razor 3 또는 ASP.NET MVC 5로 업그레이드 한 후 tilde(~) 표기법을 사용할 수 없습니다 올바르게 URL 재작성을 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="7f10d-201">After upgrading to ASP.NET Razor 3 or ASP.NET MVC 5, the tilde(~) notation may no longer work correctly if you are using URL rewrites.</span></span> <span data-ttu-id="7f10d-202">URL 다시 쓰기에 영향을 줍니다 tilde(~) 표기법에서 HTML 요소와 같은 &lt;A /&gt;, &lt;스크립트 /&gt;, &lt;링크 /&gt;, 물결표 루트 디렉터리에 더 이상 매핑됩니다 결과적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-202">The URL rewrite affects the tilde(~) notation in HTML elements such as &lt;A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;, and as a result the tilde no longer maps to the root directory.</span></span>

<span data-ttu-id="7f10d-203">예를 들어에 대 한 요청을 다시 작성할 때 **asp.net/content** 하 **asp.net**, href 특성에 &lt;a "~/content/" = /&gt; 확인 **/content/ 콘텐츠 /** of **/** 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-203">For example, if you rewrite requests for **asp.net/content** to **asp.net**, the href attribute in &lt;A href="~/content/"/&gt; resolves to **/content/content/** instead of **/**.</span></span> <span data-ttu-id="7f10d-204">이 변경 하지 않으려면 설정할 수 있습니다 합니다 **IIS\_WasUrlRewritten** 각 웹 페이지 또는 false로 상황에 맞는 **응용 프로그램\_BeginRequest** Global.asax의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-204">To suppress this change, you can set the **IIS\_WasUrlRewritten** context to false in each Web Page or in **Application\_BeginRequest** in Global.asax.</span></span>

<a id="templateissue"></a>
### <a name="templates"></a><span data-ttu-id="7f10d-205">템플릿</span><span class="sxs-lookup"><span data-stu-id="7f10d-205">Templates</span></span>

<span data-ttu-id="7f10d-206">만들 때 ASP.NET MVC 프로젝트 Windows 8.1 또는 Windows Server 2012 R2, Visual Studio에서 Visual Studio 2012를 사용 하 여 구성 봚 [url] asp.net 4.5가 실패 했습니다. "를 나타내는 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-206">When you create ASP.NET MVC projects with Visual Studio 2012 on Windows 8.1 or Windows Server 2012 R2, Visual Studio displays an error message that states "Configuring Web [url] for ASP.NET 4.5 failed."</span></span>

![구성 오류](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

<span data-ttu-id="7f10d-208">해당 릴리스의 Windows에서 설치 될 때 Visual Studio 2012에 ASP.NET 4.5 기능을 활성화 하지 때문에이 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-208">You see this error because Visual Studio 2012 does not enable the ASP.NET 4.5 feature when it is installed on those releases of Windows.</span></span> <span data-ttu-id="7f10d-209">ASP.NET 4.5를 사용 하도록 설정 하려면에 설명 된 단계를 수행 [설정할 Windows 기능 사용 /](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-209">To enable ASP.NET 4.5, perform the steps described in [Turn Windows features on or off](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).</span></span>

![Windows 기능 설정](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

<span data-ttu-id="7f10d-211">또는 명령줄을 통해 ASP.NET 4.5를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-211">Alternatively, you can enable ASP.NET 4.5 through the command line.</span></span>

1. <span data-ttu-id="7f10d-212">관리자 모드에서 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-212">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="7f10d-213">ASP.NET 4.5를 사용 하도록 설정 하려면 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f10d-213">Run the following command to enable ASP.NET 4.5.</span></span>  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
