---
uid: whitepapers/mvc4-beta-release-notes
title: ASP.NET MVC 4 | Microsoft Docs
author: rick-anderson
description: 이 문서에서는 Visual Studio 2010 용 ASP.NET MVC 4 베타 출시를 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/09/2011
ms.topic: article
ms.assetid: 666407bb-81de-4319-89ba-0302c382a208
ms.technology: ''
msc.legacyurl: /whitepapers/mvc4-beta-release-notes
msc.type: content
ms.openlocfilehash: 62bd641b1c5c926ec33ed3948854365aea99e979
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37390610"
---
<a name="aspnet-mvc-4"></a><span data-ttu-id="a9ddf-103">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="a9ddf-103">ASP.NET MVC 4</span></span>
====================
> <span data-ttu-id="a9ddf-104">이 문서에서는 Visual Studio 2010 용 ASP.NET MVC 4 베타 출시를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-104">This document describes the release of ASP.NET MVC 4 Beta for Visual Studio 2010.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="a9ddf-105">가장 최근 릴리스가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-105">This is not the most current release.</span></span> <span data-ttu-id="a9ddf-106">ASP.NET MVC 4 RC 릴리스 정보 [여기](mvc4-release-notes.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-106">The ASP.NET MVC 4 RC release notes are available [here](mvc4-release-notes.md).</span></span>


- [<span data-ttu-id="a9ddf-107">설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="a9ddf-107">Installation Notes</span></span>](#_Toc303253802)
- [<span data-ttu-id="a9ddf-108">문서</span><span class="sxs-lookup"><span data-stu-id="a9ddf-108">Documentation</span></span>](#_Toc303253803)
- [<span data-ttu-id="a9ddf-109">지원</span><span class="sxs-lookup"><span data-stu-id="a9ddf-109">Support</span></span>](#_Toc303253804)
- [<span data-ttu-id="a9ddf-110">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="a9ddf-110">Software Requirements</span></span>](#_Toc303253805)
- [<span data-ttu-id="a9ddf-111">ASP.NET MVC 3 프로젝트를 ASP.NET MVC 4로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="a9ddf-111">Upgrading an ASP.NET MVC 3 Project to ASP.NET MVC 4</span></span>](#_Toc303253806)
- [<span data-ttu-id="a9ddf-112">ASP.NET MVC 4 베타의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="a9ddf-112">New Features in ASP.NET MVC 4 Beta</span></span>](#_Toc303253807)

    - [<span data-ttu-id="a9ddf-113">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="a9ddf-113">ASP.NET Web API</span></span>](#_Toc317096197)
    - [<span data-ttu-id="a9ddf-114">ASP.NET 단일 페이지 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="a9ddf-114">ASP.NET Single Page Application</span></span>](#_Toc317096198)
    - [<span data-ttu-id="a9ddf-115">향상 된 기본 프로젝트 템플릿</span><span class="sxs-lookup"><span data-stu-id="a9ddf-115">Enhancements to Default Project Templates</span></span>](#_Toc303253808)
    - [<span data-ttu-id="a9ddf-116">모바일 프로젝트 템플릿</span><span class="sxs-lookup"><span data-stu-id="a9ddf-116">Mobile Project Template</span></span>](#_Toc303253809)
    - [<span data-ttu-id="a9ddf-117">디스플레이 모드</span><span class="sxs-lookup"><span data-stu-id="a9ddf-117">Display Modes</span></span>](#_Toc303253810)
    - [<span data-ttu-id="a9ddf-118">jQuery 모바일 뷰 전환기와 브라우저 재정의</span><span class="sxs-lookup"><span data-stu-id="a9ddf-118">jQuery Mobile, the View Switcher, and Browser Overriding</span></span>](#_Toc303253811)
    - [<span data-ttu-id="a9ddf-119">Visual Studio에서 코드 생성에 대 한 레시피</span><span class="sxs-lookup"><span data-stu-id="a9ddf-119">Recipes for Code Generation in Visual Studio</span></span>](#_Toc303253812)
    - [<span data-ttu-id="a9ddf-120">비동기 컨트롤러에 대 한 작업 지원</span><span class="sxs-lookup"><span data-stu-id="a9ddf-120">Task Support for Asynchronous Controllers</span></span>](#_Toc303253813)
    - [<span data-ttu-id="a9ddf-121">Azure SDK</span><span class="sxs-lookup"><span data-stu-id="a9ddf-121">Azure SDK</span></span>](#_Toc303253814)
    - [<span data-ttu-id="a9ddf-122">알려진된 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="a9ddf-122">Known Issues and Breaking Changes</span></span>](#_Toc303253815)

<a id="_Toc303253802"></a>
## <a name="installation-notes"></a><span data-ttu-id="a9ddf-123">설치 참고 사항</span><span class="sxs-lookup"><span data-stu-id="a9ddf-123">Installation Notes</span></span>

<span data-ttu-id="a9ddf-124">Visual Studio 2010 용 ASP.NET MVC 4 베타에서 설치할 수 있습니다 합니다 [ASP.NET MVC 4 홈페이지](../mvc/mvc4.md) 웹 플랫폼 설치 관리자를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-124">ASP.NET MVC 4 Beta for Visual Studio 2010 can be installed from the [ASP.NET MVC 4 home page](../mvc/mvc4.md) using the Web Platform Installer.</span></span>

<span data-ttu-id="a9ddf-125">ASP.NET MVC 4 베타를 설치 하기 전에 ASP.NET MVC 4의 모든 이전에 설치 된 미리 보기를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-125">You must uninstall any previously installed previews of ASP.NET MVC 4 prior to installing ASP.NET MVC 4 Beta.</span></span>

<span data-ttu-id="a9ddf-126">이 릴리스에.NET Framework 4.5 Developer Preview와 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-126">This release is not compatible with the .NET Framework 4.5 Developer Preview.</span></span> <span data-ttu-id="a9ddf-127">ASP.NET MVC 4 베타를 설치 하기 전에.NET 4.5 Developer Preview를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-127">You must uninstall the .NET 4.5 Developer Preview before installing the ASP.NET MVC 4 Beta.</span></span>

<span data-ttu-id="a9ddf-128">ASP.NET MVC 4 설치할 수 있으며-나란히 실행할 수 있습니다 ASP.NET MVC 3을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-128">ASP.NET MVC 4 can be installed and can run side-by-side with ASP.NET MVC 3.</span></span>

<a id="_Toc303253803"></a>
## <a name="documentation"></a><span data-ttu-id="a9ddf-129">설명서</span><span class="sxs-lookup"><span data-stu-id="a9ddf-129">Documentation</span></span>

<span data-ttu-id="a9ddf-130">ASP.NET MVC에 대 한 설명서는 다음 URL의 MSDN 웹 사이트에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-130">Documentation for ASP.NET MVC is available on the MSDN website at the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=243043](https://go.microsoft.com/fwlink/?LinkID=243043)

<span data-ttu-id="a9ddf-131">자습서 및 기타 정보 ASP.NET MVC는 ASP.NET 웹 사이트의 MVC 4 페이지에서 사용할 수 있습니다 ([https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)).</span><span class="sxs-lookup"><span data-stu-id="a9ddf-131">Tutorials and other information about ASP.NET MVC are available on the MVC 4 page of the ASP.NET website ([https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)).</span></span>

<a id="_Toc303253804"></a>
## <a name="support"></a><span data-ttu-id="a9ddf-132">Support(지원)</span><span class="sxs-lookup"><span data-stu-id="a9ddf-132">Support</span></span>

<span data-ttu-id="a9ddf-133">이 미리 보기 버전 이며 공식적으로 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-133">This is a preview release and is not officially supported.</span></span> <span data-ttu-id="a9ddf-134">이 릴리스를 사용 하는 방법에 대 한 질문이 있으면 ASP.NET MVC 포럼에 게시 ([https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)) ASP.NET 커뮤니티 회원이 비공식적인 지원을 제공 하기 위해 자주 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-134">If you have questions about working with this release, post them to the ASP.NET MVC forum ([https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)), where members of the ASP.NET community are frequently able to provide informal support.</span></span>

<a id="_Toc303253805"></a>
## <a name="software-requirements"></a><span data-ttu-id="a9ddf-135">소프트웨어 요구 사항</span><span class="sxs-lookup"><span data-stu-id="a9ddf-135">Software Requirements</span></span>

<span data-ttu-id="a9ddf-136">Visual Studio의 ASP.NET MVC 4 구성 요소 PowerShell 2.0 및 Visual Studio 2010 서비스 팩 1 또는 Visual Web Developer Express 2010 서비스 팩 1에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-136">The ASP.NET MVC 4 components for Visual Studio require PowerShell 2.0 and either Visual Studio 2010 with Service Pack 1 or Visual Web Developer Express 2010 with Service Pack 1.</span></span>

<a id="_Toc303253806"></a>
## <a name="upgrading-an-aspnet-mvc-3-project-to-aspnet-mvc-4"></a><span data-ttu-id="a9ddf-137">ASP.NET MVC 3 프로젝트를 ASP.NET MVC 4로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="a9ddf-137">Upgrading an ASP.NET MVC 3 Project to ASP.NET MVC 4</span></span>

<span data-ttu-id="a9ddf-138">ASP.NET MVC 4를 ASP.NET MVC 4 ASP.NET MVC 3 응용 프로그램을 업그레이드 하는 시기 선택에 유연성을 제공 하는 동일한 컴퓨터에서 ASP.NET MVC 3에 나란히 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-138">ASP.NET MVC 4 can be installed side by side with ASP.NET MVC 3 on the same computer, which gives you flexibility in choosing when to upgrade an ASP.NET MVC 3 application to ASP.NET MVC 4.</span></span>

<span data-ttu-id="a9ddf-139">업그레이드 하는 가장 간단한 방법은 새 ASP.NET MVC 4 프로젝트를 만들고 복사 모든 뷰, 컨트롤러, 코드 및 콘텐츠 파일을 기존 MVC 3 프로젝트에서 새 프로젝트에 되어 다음 어셈블리를 업데이트 하려면 이전 프로젝트와 일치 하도록 새 프로젝트에서 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-139">The simplest way to upgrade is to create a new ASP.NET MVC 4 project and copy all the views, controllers, code, and content files from the existing MVC 3 project to the new project and then to update the assembly references in the new project to match the old project.</span></span> <span data-ttu-id="a9ddf-140">MVC 3 프로젝트의 Web.config 파일을 변경한 경우 MVC 4 프로젝트의 Web.config 파일에 이러한 변경 내용을 병합 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-140">If you have made changes to the Web.config file in the MVC 3 project, you must also merge those changes into the Web.config file in the MVC 4 project.</span></span>

<span data-ttu-id="a9ddf-141">기존 ASP.NET MVC 3 응용 프로그램 버전 4 수동으로 업그레이드 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-141">To manually upgrade an existing ASP.NET MVC 3 application to version 4, do the following:</span></span>

1. <span data-ttu-id="a9ddf-142">(에 프로젝트에서 Views 폴더를 하나, 하나는 프로젝트에서 각 영역의 Views 폴더의 루트에 하나) 프로젝트의 모든 Web.config 파일에서 다음 텍스트의 모든 인스턴스를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-142">In all Web.config files in the project (there is one in the root of the project, one in the Views folder, and one in the Views folder for each area in your project), replace every instance of the following text:</span></span>

    [!code-console[Main](mvc4-beta-release-notes/samples/sample1.cmd)]

    <span data-ttu-id="a9ddf-143">해당 텍스트:</span><span class="sxs-lookup"><span data-stu-id="a9ddf-143">with the following corresponding text:</span></span>

    [!code-console[Main](mvc4-beta-release-notes/samples/sample2.cmd)]
2. <span data-ttu-id="a9ddf-144">루트 Web.config 파일을 업데이트 합니다 *webPages:Version* "2.0.0.0" 요소를 새로 추가 *PreserveLoginUrl* "true" 값이 있는 키:</span><span class="sxs-lookup"><span data-stu-id="a9ddf-144">In the root Web.config file, update the *webPages:Version* element to "2.0.0.0" and add a new *PreserveLoginUrl* key that has the value "true":</span></span>

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample3.xml)]
3. <span data-ttu-id="a9ddf-145">솔루션 탐색기에서 삭제에 대 한 참조가 *System.Web.Mvc* (가리키는 버전 3 DLL).</span><span class="sxs-lookup"><span data-stu-id="a9ddf-145">In Solution Explorer, delete the reference to *System.Web.Mvc* (which points to the version 3 DLL).</span></span> <span data-ttu-id="a9ddf-146">다음에 대 한 참조를 추가 *System.Web.Mvc* (v4.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="a9ddf-146">Then add a reference to *System.Web.Mvc* (v4.0.0.0).</span></span> <span data-ttu-id="a9ddf-147">특히, 어셈블리 참조를 업데이트 하려면 다음 변경 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-147">In particular, make the following changes to update the assembly references.</span></span> <span data-ttu-id="a9ddf-148">자세한 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-148">Here are the details:</span></span>

    1. <span data-ttu-id="a9ddf-149">솔루션 탐색기에서 다음 어셈블리에 대 한 참조를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-149">In Solution Explorer, delete the references to the following assemblies:</span></span> 

        - <span data-ttu-id="a9ddf-150">*System.Web.Mvc*(v3.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="a9ddf-150">*System.Web.Mvc*(v3.0.0.0)</span></span>
        - <span data-ttu-id="a9ddf-151">*System.Web.WebPages*(v1.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="a9ddf-151">*System.Web.WebPages*(v1.0.0.0)</span></span>
        - <span data-ttu-id="a9ddf-152">*System.Web.Razor*(v1.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="a9ddf-152">*System.Web.Razor*(v1.0.0.0)</span></span>
        - <span data-ttu-id="a9ddf-153">*System.Web.WebPages.Deployment*(v1.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="a9ddf-153">*System.Web.WebPages.Deployment*(v1.0.0.0)</span></span>
        - <span data-ttu-id="a9ddf-154">*System.Web.WebPages.Razor*(v1.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="a9ddf-154">*System.Web.WebPages.Razor*(v1.0.0.0)</span></span>
    2. <span data-ttu-id="a9ddf-155">다음 어셈블리에 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-155">Add a references to the following assemblies:</span></span> 

        - <span data-ttu-id="a9ddf-156">*System.Web.Mvc*(v4.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="a9ddf-156">*System.Web.Mvc*(v4.0.0.0)</span></span>
        - <span data-ttu-id="a9ddf-157">*System.Web.WebPages*(v2.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="a9ddf-157">*System.Web.WebPages*(v2.0.0.0)</span></span>
        - <span data-ttu-id="a9ddf-158">*System.Web.Razor*(v2.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="a9ddf-158">*System.Web.Razor*(v2.0.0.0)</span></span>
        - <span data-ttu-id="a9ddf-159">*System.Web.WebPages.Deployment*(v2.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="a9ddf-159">*System.Web.WebPages.Deployment*(v2.0.0.0)</span></span>
        - <span data-ttu-id="a9ddf-160">*System.Web.WebPages.Razor*(v2.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="a9ddf-160">*System.Web.WebPages.Razor*(v2.0.0.0)</span></span>
4. <span data-ttu-id="a9ddf-161">솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 프로젝트 언로드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-161">In Solution Explorer, right-click the project name and then select Unload Project.</span></span> <span data-ttu-id="a9ddf-162">그런 다음 이름을 다시 마우스 오른쪽 단추로 클릭 하 고 편집 선택 *ProjectName*.csproj 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-162">Then right-click the name again and select Edit *ProjectName*.csproj.</span></span>
5. <span data-ttu-id="a9ddf-163">찾을 합니다 *ProjectTypeGuids* 요소와 {E3E379DF-F4C6-4180-9B81-6769533ABE47} {E53F8FEA-EAE0-44A6-8774-FFD645390401} 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-163">Locate the *ProjectTypeGuids* element and replace {E53F8FEA-EAE0-44A6-8774-FFD645390401} with {E3E379DF-F4C6-4180-9B81-6769533ABE47}.</span></span>
6. <span data-ttu-id="a9ddf-164">변경 내용을 저장, 편집 하 고 프로젝트 (.csproj) 파일을 닫습니다, 그리고 프로젝트를 마우스 오른쪽 단추로 클릭 선택한 후 프로젝트 다시 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-164">Save the changes, close the project (.csproj) file you were editing, right-click the project, and then select Reload Project.</span></span>
7. <span data-ttu-id="a9ddf-165">이전 버전의 ASP.NET MVC를 사용 하 여 컴파일되는 모든 타사 라이브러리를 프로젝트에서 참조 하는 경우 루트 Web.config 파일을 열고 다음 세 가지 추가 *bindingRedirect* 아래에 요소를  *구성* 섹션:</span><span class="sxs-lookup"><span data-stu-id="a9ddf-165">If the project references any third-party libraries that are compiled using previous versions of ASP.NET MVC, open the root Web.config file and add the following three *bindingRedirect* elements under the *configuration* section:</span></span> 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample4.xml)]

<a id="_Toc303253807"></a>
## <a name="new-features-in-aspnet-mvc-4-beta"></a><span data-ttu-id="a9ddf-166">ASP.NET MVC 4 베타의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="a9ddf-166">New Features in ASP.NET MVC 4 Beta</span></span>

<span data-ttu-id="a9ddf-167">도입 된 기능을 설명 하는이 섹션에서는 ASP.NET MVC 4 베타 릴리스에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-167">This section describes features that have been introduced in the ASP.NET MVC 4 Beta release.</span></span>

<a id="_Toc317096197"></a>
### <a name="aspnet-web-api"></a><span data-ttu-id="a9ddf-168">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="a9ddf-168">ASP.NET Web API</span></span>

<span data-ttu-id="a9ddf-169">HTTP 서비스를 만들기 위한 새로운 프레임 워크는 광범위 한 브라우저 및 모바일 장치를 비롯 하 여 클라이언트를 연결할 수, ASP.NET MVC 4는 이제 ASP.NET 웹 API 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-169">ASP.NET MVC 4 now includes ASP.NET Web API, a new framework for creating HTTP services that can reach a broad range of clients including browsers and mobile devices.</span></span> <span data-ttu-id="a9ddf-170">ASP.NET Web API RESTful 서비스를 빌드하기 위한 이상적인 플랫폼 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-170">ASP.NET Web API is also an ideal platform for building RESTful services.</span></span>

<span data-ttu-id="a9ddf-171">ASP.NET Web API를 사용 하면 다음과 같은 기능에 대 한 지원도:</span><span class="sxs-lookup"><span data-stu-id="a9ddf-171">ASP.NET Web API includes support for the following features:</span></span>

- <span data-ttu-id="a9ddf-172">**최신 HTTP 프로그래밍 모델:** 직접 액세스 하 고 새 강력한 형식의 HTTP 개체 모델을 사용 하 여 웹 Api의 HTTP 요청 및 응답을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-172">**Modern HTTP programming model:** Directly access and manipulate HTTP requests and responses in your Web APIs using a new, strongly typed HTTP object model.</span></span> <span data-ttu-id="a9ddf-173">동일한 프로그래밍 모델 및 HTTP 파이프라인은 대칭적으로 새로운 HttpClient 형식을 통해 클라이언트에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-173">The same programming model and HTTP pipeline is symmetrically available on the client through the new HttpClient type.</span></span>
- <span data-ttu-id="a9ddf-174">**전체 경로 대 한 지원**: Web Api는 이제 경로 매개 변수 및 제약 조건을 포함 하 여 웹 스택의 일부 항상 되었던 경로 기능 전체 집합을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-174">**Full support for routes**: Web APIs now support the full set of route capabilities that have always been a part of the Web stack, including route parameters and constraints.</span></span> <span data-ttu-id="a9ddf-175">또한 작업에 대 한 매핑 있으므로 규칙에 대 한 전체 지원 같은 [HttpPost] 특성을 적용 해야 하는 더 이상 클래스 및 메서드.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-175">Additionally, mapping to actions has full support for conventions, so you no longer need to apply attributes such as [HttpPost] to your classes and methods.</span></span>
- <span data-ttu-id="a9ddf-176">**콘텐츠 협상**: 클라이언트와 서버가 함께 작동 하 여 API에서 반환 되는 데이터에 대 한 올바른 형식을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-176">**Content negotiation**: The client and server can work together to determine the right format for data being returned from an API.</span></span> <span data-ttu-id="a9ddf-177">XML, JSON 및 양식 URL로 인코딩된 형식에 대 한 기본 지원을 제공 하 고 고유한 포맷터를 추가 하 여이 지원을 확장 하거나 기본 콘텐츠 협상 전략을 교체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-177">We provide default support for XML, JSON, and Form URL-encoded formats, and you can extend this support by adding your own formatters, or even replace the default content negotiation strategy.</span></span>
- <span data-ttu-id="a9ddf-178">**모델 바인딩 및 유효성 검사:** 모델 바인더에는 HTTP 요청의 여러 부분에서 데이터를 추출 하 고 해당 메시지 파트 Web API 작업으로 사용할 수 있는.NET 개체로 변환 하는 쉬운 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-178">**Model binding and validation:** Model binders provide an easy way to extract data from various parts of an HTTP request and convert those message parts into .NET objects which can be used by the Web API actions.</span></span>
- <span data-ttu-id="a9ddf-179">**필터:** 웹 Api는 이제 [Authorize] 특성와 같은 잘 알려진 필터를 포함 하 여 필터를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-179">**Filters:** Web APIs now supports filters, including well-known filters such as the [Authorize] attribute.</span></span> <span data-ttu-id="a9ddf-180">작성 하 고, 작업, 권한 부여 및 예외 처리에 대 한 필터를 직접 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-180">You can author and plug in your own filters for actions, authorization and exception handling.</span></span>
- <span data-ttu-id="a9ddf-181">**쿼리 컴퍼지션:** 단순히 IQueryable을 반환 하 여&lt;T&gt;, Web API OData URL 규칙을 통해 쿼리를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-181">**Query composition:** By simply returning IQueryable&lt;T&gt;, your Web API will support querying via the OData URL conventions.</span></span>
- <span data-ttu-id="a9ddf-182">**HTTP 세부의 테스트 용이성 향상:** 정적 컨텍스트 개체에서 HTTP 세부 정보를 설정 하는 대신 Web API 작업 HttpRequestMessage 및 HttpResponseMessage의 인스턴스를 사용 하 여 작동 이제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-182">**Improved testability of HTTP details:** Rather than setting HTTP details in static context objects, Web API actions can now work with instances of HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="a9ddf-183">이러한 개체의 제네릭 버전은 또한 HTTP 형식 외에도 사용자 지정 형식을 사용 하 여 작업할 수 있도록 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-183">Generic versions of these objects also exist to let you work with your custom types in addition to the HTTP types.</span></span>
- <span data-ttu-id="a9ddf-184">**Inversion of Control (IoC) DependencyResolver 통해 향상:** Web API 여러 다른 기능에 대 한 인스턴스를 얻는 이제 MVC의 종속성 확인자를 구현한 서비스 로케이터 패턴을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-184">**Improved Inversion of Control (IoC) via DependencyResolver:** Web API now uses the service locator pattern implemented by MVC's dependency resolver to obtain instances for many different facilities.</span></span>
- <span data-ttu-id="a9ddf-185">**코드 기반 구성:** Web API 구성 코드를 통해서만 수행 됩니다, 파일 정리 config를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-185">**Code-based configuration:** Web API configuration is accomplished solely through code, leaving your config files clean.</span></span>
- <span data-ttu-id="a9ddf-186">**자체 호스트:** 경로의 모든 기능 및 웹 API의 기타 기능을 계속 사용 하면서 IIS 외에도 고유한 프로세스에서 웹 Api를 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-186">**Self-host:** Web APIs can be hosted in your own process in addition to IIS while still using the full power of routes and other features of Web API.</span></span>

<span data-ttu-id="a9ddf-187">ASP.NET Web API에 대 한 자세한 내용은 참조 하세요 [ https://www.asp.net/web-api ](../web-api/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-187">For more details on ASP.NET Web API please visit [https://www.asp.net/web-api](../web-api/index.md).</span></span>

<a id="_Toc317096198"></a>
### <a name="aspnet-single-page-application"></a><span data-ttu-id="a9ddf-188">ASP.NET 단일 페이지 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="a9ddf-188">ASP.NET Single Page Application</span></span>

<span data-ttu-id="a9ddf-189">ASP.NET MVC 4는 이제 JavaScript 및 Web Api를 사용 하 여 중요 한 클라이언트 쪽 상호 작용을 사용 하 여 단일 페이지 응용 프로그램을 빌드하기 위한 환경의 초기 미리 보기가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-189">ASP.NET MVC 4 now includes an early preview of the experience for building single page applications with significant client-side interactions using JavaScript and Web APIs.</span></span> <span data-ttu-id="a9ddf-190">이 지원에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-190">This support includes:</span></span>

- <span data-ttu-id="a9ddf-191">캐시 된 데이터를 사용 하 여 다양 한 로컬 상호 작용에 대 한 JavaScript 라이브러리 집합</span><span class="sxs-lookup"><span data-stu-id="a9ddf-191">A set of JavaScript libraries for richer local interactions with cached data</span></span>
- <span data-ttu-id="a9ddf-192">작업 단위와 DAL 지원에 대 한 추가 Web API 구성 요소</span><span class="sxs-lookup"><span data-stu-id="a9ddf-192">Additional Web API components for unit of work and DAL support</span></span>
- <span data-ttu-id="a9ddf-193">MVC 프로젝트 템플릿을 사용 하 여 빠르게 시작 하려면 스 캐 폴딩</span><span class="sxs-lookup"><span data-stu-id="a9ddf-193">An MVC project template with scaffolding to get started quickly</span></span>

<span data-ttu-id="a9ddf-194">단일 페이지 응용 프로그램에 대 한 자세한 내용은 ASP.NET MVC 4에서 지원에 대 한 방문 하십시오 [ https://www.asp.net/single-page-application ](../single-page-application/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-194">For more details on the Single Page Application support in ASP.NET MVC 4 please visit [https://www.asp.net/single-page-application](../single-page-application/index.md).</span></span>

<a id="_Toc303253808"></a>
### <a name="enhancements-to-default-project-templates"></a><span data-ttu-id="a9ddf-195">향상 된 기본 프로젝트 템플릿</span><span class="sxs-lookup"><span data-stu-id="a9ddf-195">Enhancements to Default Project Templates</span></span>

<span data-ttu-id="a9ddf-196">더 최신 웹 사이트를 만들고 새 ASP.NET MVC 4 프로젝트를 만드는 데 사용 되는 템플릿을 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-196">The template that is used to create new ASP.NET MVC 4 projects has been updated to create a more modern-looking website:</span></span>

![](mvc4-beta-release-notes/_static/image1.png)

<span data-ttu-id="a9ddf-197">표면적인 향상 된 새 템플릿에 기능을 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-197">In addition to cosmetic improvements, there's improved functionality in the new template.</span></span> <span data-ttu-id="a9ddf-198">템플릿을 적응형 렌더링 데스크톱 브라우저와 사용자 지정 하지 않고 모바일 브라우저에서 보기 좋게 하 라는 기술을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-198">The template employs a technique called adaptive rendering to look good in both desktop browsers and mobile browsers without any customization.</span></span>

![](mvc4-beta-release-notes/_static/image2.png)

<span data-ttu-id="a9ddf-199">작업에서 적응형 렌더링을 보려면 모바일 에뮬레이터를 사용할 수도 있고 더 작게 할 데스크톱 브라우저 창의 크기를 조정 하십시오. 단 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-199">To see adaptive rendering in action, you can use a mobile emulator or just try resizing the desktop browser window to be smaller.</span></span> <span data-ttu-id="a9ddf-200">브라우저 창을 충분히 작게 가져오면 페이지의 레이아웃 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-200">When the browser window gets small enough, the layout of the page will change.</span></span>

<span data-ttu-id="a9ddf-201">기본 프로젝트 템플릿에 다른 향상 된 다양 한 UI를 제공 하는 JavaScript의 사용입니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-201">Another enhancement to the default project template is the use of JavaScript to provide a richer UI.</span></span> <span data-ttu-id="a9ddf-202">템플릿에서 사용 되는 로그인 및 등록 링크를은 다양 한 로그인 화면을 표시 하기 위해 jQuery UI 대화 상자를 사용 하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-202">The Login and Register links that are used in the template are examples of how to use the jQuery UI Dialog to present a rich login screen:</span></span>

![](mvc4-beta-release-notes/_static/image3.png)

<a id="_Toc303253809"></a>
### <a name="mobile-project-template"></a><span data-ttu-id="a9ddf-203">모바일 프로젝트 템플릿</span><span class="sxs-lookup"><span data-stu-id="a9ddf-203">Mobile Project Template</span></span>

<span data-ttu-id="a9ddf-204">새 프로젝트를 시작 하 고 모바일에 맞게 사이트 및 태블릿 브라우저를 만들려고 할 경우에 새 모바일 응용 프로그램 프로젝트 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-204">If you're starting a new project and want to create a site specifically for mobile and tablet browsers, you can use the new Mobile Application project template.</span></span> <span data-ttu-id="a9ddf-205">이 jQuery Mobile, 터치에 최적화 된 UI를 빌드하기 위한 오픈 소스 라이브러리를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-205">This is based on jQuery Mobile, an open-source library for building touch-optimized UI:</span></span>

![](mvc4-beta-release-notes/_static/image4.png)

<span data-ttu-id="a9ddf-206">이 템플릿에 인터넷 응용 프로그램 템플릿 동일한 응용 프로그램 구조 (및 컨트롤러 코드는 거의 동일) 이지만 스타일 jQuery Mobile을 사용 하 여 보기 좋게 하 고 터치 기반 모바일 장치에서 잘 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-206">This template contains the same application structure as the Internet Application template (and the controller code is virtually identical), but it's styled using jQuery Mobile to look good and behave well on touch-based mobile devices.</span></span> <span data-ttu-id="a9ddf-207">구조체 및 모바일 UI 스타일을 지정 하는 방법에 대 한 자세한 내용은 참조는 [jQuery 모바일 프로젝트 웹 사이트](http://jquerymobile.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-207">To learn more about how to structure and style mobile UI, see the [jQuery Mobile project website](http://jquerymobile.com/).</span></span>

<span data-ttu-id="a9ddf-208">모바일에 최적화 된 뷰를 추가 하거나 다른 방식으로 스타일이 지정 된 뷰 데스크톱 및 모바일 브라우저를 제공 하는 단일 사이트를 만들려는 경우 데스크톱 지향 사이트에 이미 있는 경우에 새로운 디스플레이 모드 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-208">If you already have a desktop-oriented site that you want to add mobile-optimized views to, or if you want to create a single site that serves differently styled views to desktop and mobile browsers, you can use the new Display Modes feature.</span></span> <span data-ttu-id="a9ddf-209">(다음 섹션을 참조 하세요.)</span><span class="sxs-lookup"><span data-stu-id="a9ddf-209">(See the next section.)</span></span>

<a id="_Toc303253810"></a>
### <a name="display-modes"></a><span data-ttu-id="a9ddf-210">디스플레이 모드</span><span class="sxs-lookup"><span data-stu-id="a9ddf-210">Display Modes</span></span>

<span data-ttu-id="a9ddf-211">새로운 디스플레이 모드 기능에는 응용 프로그램을 요청을 수행 하는 브라우저에 따라 뷰를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-211">The new Display Modes feature lets an application select views depending on the browser that's making the request.</span></span> <span data-ttu-id="a9ddf-212">예를 들어, 데스크톱 브라우저 홈 페이지를 요청 하는 경우 응용 프로그램 Views\Home\Index.cshtml 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-212">For example, if a desktop browser requests the Home page, the application might use the Views\Home\Index.cshtml template.</span></span> <span data-ttu-id="a9ddf-213">모바일 브라우저 홈 페이지를 요청 하는 경우 Views\Home\Index.mobile.cshtml 템플릿 응용 프로그램에 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-213">If a mobile browser requests the Home page, the application might return the Views\Home\Index.mobile.cshtml template.</span></span>

<span data-ttu-id="a9ddf-214">특정 브라우저 종류에 대 한 레이아웃 및 부분을 재정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-214">Layouts and partials can also be overridden for particular browser types.</span></span> <span data-ttu-id="a9ddf-215">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="a9ddf-215">For example:</span></span>

- <span data-ttu-id="a9ddf-216">Views\Shared 폴더에 모두 포함 하는 경우는 \_Layout.cshtml 및 \_Layout.mobile.cshtml 템플릿, 응용 프로그램 사용은 기본적으로 \_ 모바일브라우저에서요청하는동안Layout.mobile.cshtml\_Layout.cshtml 다른 요청 중입니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-216">If your Views\Shared folder contains both the \_Layout.cshtml and \_Layout.mobile.cshtml templates, by default the application will use \_Layout.mobile.cshtml during requests from mobile browsers and \_Layout.cshtml during other requests.</span></span>
- <span data-ttu-id="a9ddf-217">둘 다 포함 된 폴더 \_MyPartial.cshtml 및 \_MyPartial.mobile.cshtml, 지침 @Html.Partial("\_MyPartial")가 렌더링 \_MyPartial.mobile.cshtml mobile에서 요청 하는 동안 브라우저 및 \_MyPartial.cshtml 다른 요청 중입니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-217">If a folder contains both \_MyPartial.cshtml and \_MyPartial.mobile.cshtml, the instruction @Html.Partial("\_MyPartial") will render \_MyPartial.mobile.cshtml during requests from mobile browsers, and \_MyPartial.cshtml during other requests.</span></span>

<span data-ttu-id="a9ddf-218">보다 구체적인 뷰, 레이아웃 또는 다른 장치에 대 한 부분 뷰를 만들려면, 새 등록할 수 있습니다 *DefaultDisplayMode* 인스턴스는 요청을 특정 조건을 충족 하는 경우를 검색할 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-218">If you want to create more specific views, layouts, or partial views for other devices, you can register a new *DefaultDisplayMode* instance to specify which name to search for when a request satisfies particular conditions.</span></span> <span data-ttu-id="a9ddf-219">예를 들어, 다음 코드를 추가할 수 있습니다 합니다 *응용 프로그램\_시작* Apple iPhone 브라우저 요청을 수행 하는 경우 적용 되는 디스플레이 모드를 "iPhone" 문자열을 등록 하려면 Global.asax 파일에는 메서드:</span><span class="sxs-lookup"><span data-stu-id="a9ddf-219">For example, you could add the following code to the *Application\_Start* method in the Global.asax file to register the string "iPhone" as a display mode that applies when the Apple iPhone browser makes a request:</span></span>

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample5.cs)]

<span data-ttu-id="a9ddf-220">응용 프로그램을 Views\Shared 사용할 Apple iPhone 브라우저를 요청 하면이 코드가 실행 된 후\\_Layout.iPhone.cshtml 레이아웃 (있는 경우).</span><span class="sxs-lookup"><span data-stu-id="a9ddf-220">After this code runs, when an Apple iPhone browser makes a request, your application will use the Views\Shared\\_Layout.iPhone.cshtml layout (if it exists).</span></span>

<a id="_Toc303253811"></a>
### <a name="jquery-mobile-the-view-switcher-and-browser-overriding"></a><span data-ttu-id="a9ddf-221">jQuery 모바일 뷰 전환기와 브라우저 재정의</span><span class="sxs-lookup"><span data-stu-id="a9ddf-221">jQuery Mobile, the View Switcher, and Browser Overriding</span></span>

<span data-ttu-id="a9ddf-222">jQuery Mobile은 터치에 최적화 된 웹 UI를 빌드하기 위한 오픈 소스 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-222">jQuery Mobile is an open source library for building touch-optimized web UI.</span></span> <span data-ttu-id="a9ddf-223">ASP.NET MVC 4 응용 프로그램을 사용 하 여 jQuery Mobile을 사용 하려는 경우 다운로드 하 고 시작 하는 데 도움이 되는 NuGet 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-223">If you want to use jQuery Mobile with an ASP.NET MVC 4 application, you can download and install a NuGet package that helps you get started.</span></span> <span data-ttu-id="a9ddf-224">Visual Studio 패키지 관리자 콘솔에서 설치 하려면 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-224">To install it from the Visual Studio Package Manager Console, type the following command:</span></span>

[!code-powershell[Main](mvc4-beta-release-notes/samples/sample6.ps1)]

<span data-ttu-id="a9ddf-225">JQuery Mobile 및 다음과 같은 몇 가지 도우미 파일에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-225">This installs jQuery Mobile and some helper files, including the following:</span></span>

- <span data-ttu-id="a9ddf-226">Views/Shared/\_Layout.Mobile.cshtml jQuery Mobile 기반 레이아웃입니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-226">Views/Shared/\_Layout.Mobile.cshtml, which is a jQuery Mobile-based layout.</span></span>
- <span data-ttu-id="a9ddf-227">Views/Shared 구성 하는 뷰 전환기 구성요소/\_ViewSwitcher.cshtml 부분 뷰와 ViewSwitcherController.cs 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-227">A view-switcher component, which consists of the Views/Shared/\_ViewSwitcher.cshtml partial view and the ViewSwitcherController.cs controller.</span></span>

<span data-ttu-id="a9ddf-228">패키지를 설치한 후 모바일 브라우저를 사용 하 여 응용 프로그램을 실행 (또는 Firefox와 같은 이와 동등한 [사용자 에이전트 전환기](http://chrispederick.com/work/user-agent-switcher/) 추가 기능).</span><span class="sxs-lookup"><span data-stu-id="a9ddf-228">After you install the package, run your application using a mobile browser (or equivalent, like the Firefox [User Agent Switcher](http://chrispederick.com/work/user-agent-switcher/) add-on).</span></span> <span data-ttu-id="a9ddf-229">페이지 레이아웃을 처리 하는 jQuery Mobile 때문에 상당히 다르게 표시 표시 및 스타일 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-229">You'll see that your pages look quite different, because jQuery Mobile handles layout and styling.</span></span> <span data-ttu-id="a9ddf-230">이 이용 하려면 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-230">To take advantage of this, you can do the following:</span></span>

- <span data-ttu-id="a9ddf-231">아래 설명 된 대로 모바일 전용 뷰 재정의 만듭니다 [디스플레이 모드](#_Toc303253810) 이전 (예를 들어 Views\Home\Index.mobile.cshtml Views\Home\Index.cshtml 모바일 브라우저에 대 한 재정의 만들기).</span><span class="sxs-lookup"><span data-stu-id="a9ddf-231">Create mobile-specific view overrides as described under [Display Modes](#_Toc303253810) earlier (for example, create Views\Home\Index.mobile.cshtml to override Views\Home\Index.cshtml for mobile browsers).</span></span>
- <span data-ttu-id="a9ddf-232">읽기를 [jQuery 모바일 설명서](http://jquerymobile.com/) 모바일 보기에서 터치에 최적화 된 UI 요소를 추가 하는 방법에 자세히 알아보려면 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-232">Read the [jQuery Mobile documentation](http://jquerymobile.com/) to learn more about how to add touch-optimized UI elements in mobile views.</span></span>

<span data-ttu-id="a9ddf-233">모바일에 최적화 된 웹 페이지에 대 한 규칙을 해당 텍스트는 바탕 화면 보기 또는 사용자가 페이지의 데스크톱 버전을 전환할 수 있는 전체 사이트 모드와 같은 링크를 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-233">A convention for mobile-optimized web pages is to add a link whose text is something like Desktop view or Full site mode that lets users switch to a desktop version of the page.</span></span> <span data-ttu-id="a9ddf-234">JQuery.Mobile.MVC 패키지는이 목적을 위해 샘플 뷰 전환기 구성 요소를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-234">The jQuery.Mobile.MVC package includes a sample view-switcher component for this purpose.</span></span> <span data-ttu-id="a9ddf-235">기본 Views\Shared 되\\_Layout.Mobile.cshtml 뷰를 다음과 같이 페이지를 렌더링 하는 경우 및:</span><span class="sxs-lookup"><span data-stu-id="a9ddf-235">It's used in the default Views\Shared\\_Layout.Mobile.cshtml view, and it looks like this when the page is rendered:</span></span>

![](mvc4-beta-release-notes/_static/image5.png)

<span data-ttu-id="a9ddf-236">방문자가 링크를 클릭 동일한 페이지의 데스크톱 버전으로 전환 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-236">If visitors click the link, they're switched to the desktop version of the same page.</span></span>

<span data-ttu-id="a9ddf-237">데스크톱 레이아웃 기본적으로 뷰 전환기를 포함 하지 않습니다, 방문자 모바일 모드를 가져올 수가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-237">Because your desktop layout will not include a view switcher by default, visitors won't have a way to get to mobile mode.</span></span> <span data-ttu-id="a9ddf-238">이렇게 하려면 다음 참조를 추가  *\_ViewSwitcher* 내에서 바로 사용자 데스크톱 레이아웃에는 *&lt;본문&gt;* 요소:</span><span class="sxs-lookup"><span data-stu-id="a9ddf-238">To enable this, add the following reference to *\_ViewSwitcher* to your desktop layout, just inside the *&lt;body&gt;* element:</span></span>

[!code-cshtml[Main](mvc4-beta-release-notes/samples/sample7.cshtml)]

<span data-ttu-id="a9ddf-239">뷰 전환기 브라우저 재정의 라는 새로운 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-239">The view switcher uses a new feature called Browser Overriding.</span></span> <span data-ttu-id="a9ddf-240">이 기능 될 예정 된 경우에 따라 요청을 처리 하는 응용 프로그램을 통해 보다 다양 한 브라우저 (사용자 에이전트)에서 이러한 사실에서.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-240">This feature lets your application treat requests as if they were coming from a different browser (user agent) than the one they're actually from.</span></span> <span data-ttu-id="a9ddf-241">다음 표에서 브라우저 재정의 제공 하는 메서드를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-241">The following table lists the methods that Browser Overriding provides.</span></span>

| `HttpContext.SetOverriddenBrowser(userAgentString)` | <span data-ttu-id="a9ddf-242">지정 된 사용자 에이전트를 사용 하 여 요청의 실제 사용자 에이전트 값을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-242">Overrides the request's actual user agent value using the specified user agent.</span></span> |
| --- | --- |
| `HttpContext.GetOverriddenUserAgent()` | <span data-ttu-id="a9ddf-243">재정의 없습니다가 지정 된 경우 요청의 사용자 에이전트 재정의 값에서 또는 실제 사용자 에이전트 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-243">Returns the request's user agent override value, or the actual user agent string if no override has been specified.</span></span> |
| `HttpContext.GetOverriddenBrowser()` | <span data-ttu-id="a9ddf-244">반환 된 *HttpBrowserCapabilitiesBase* 사용자 에이전트 요청에 대 한 현재 설정에 해당 하는 인스턴스 (실제 또는 재정의).</span><span class="sxs-lookup"><span data-stu-id="a9ddf-244">Returns an *HttpBrowserCapabilitiesBase* instance that corresponds to the user agent currently set for the request (actual or overridden).</span></span> <span data-ttu-id="a9ddf-245">같은 속성을 가져오는 데이 값을 사용할 수 있습니다 *IsMobileDevice*합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-245">You can use this value to get properties such as *IsMobileDevice*.</span></span> |
| `HttpContext.ClearOverriddenBrowser()` | <span data-ttu-id="a9ddf-246">현재 요청에 대 한 재정의 된 사용자 에이전트를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-246">Removes any overridden user agent for the current request.</span></span> |

<span data-ttu-id="a9ddf-247">브라우저 재정의 ASP.NET MVC 4의 핵심 기능 및는 jQuery.Mobile.MVC 패키지를 설치 하지 않는 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-247">Browser Overriding is a core feature of ASP.NET MVC 4 and is available even if you don't install the jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="a9ddf-248">그러나 뷰, 레이아웃 및 부분 뷰 선택을 적용-종속 된 다른 모든 ASP.NET 기능에 영향을 주지 않습니다 합니다 *Request.Browser* 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-248">However, it affects only view, layout, and partial-view selection — it does not affect any other ASP.NET feature that depends on the *Request.Browser* object.</span></span>

<span data-ttu-id="a9ddf-249">기본적으로 사용자 에이전트 재정의 쿠키를 사용 하 여 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-249">By default, the user-agent override is stored using a cookie.</span></span> <span data-ttu-id="a9ddf-250">다른 곳 (예: 데이터베이스)의 재정의 저장 하려는 경우 기본 공급자를 바꿀 수 있습니다 (*BrowserOverrideStores.Current*).</span><span class="sxs-lookup"><span data-stu-id="a9ddf-250">If you want to store the override elsewhere (for example, in a database), you can replace the default provider (*BrowserOverrideStores.Current*).</span></span> <span data-ttu-id="a9ddf-251">이 공급자에 대 한 설명서는 이후 버전의 ASP.NET MVC를 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-251">Documentation for this provider will be available to accompany a later release of ASP.NET MVC.</span></span>

<a id="_Toc303253812"></a>
### <a name="recipes-for-code-generation-in-visual-studio"></a><span data-ttu-id="a9ddf-252">Visual Studio에서 코드 생성에 대 한 레시피</span><span class="sxs-lookup"><span data-stu-id="a9ddf-252">Recipes for Code Generation in Visual Studio</span></span>

<span data-ttu-id="a9ddf-253">새 작성법 기능은 Visual Studio에서 NuGet을 사용 하 여 설치할 수 있는 패키지를 기반으로 하는 솔루션 별 코드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-253">The new Recipes feature enables Visual Studio to generate solution-specific code based on packages that you can install using NuGet.</span></span> <span data-ttu-id="a9ddf-254">레시피 프레임 워크를 사용 하면 영역 추가, 컨트롤러 추가 및 보기 추가 대 한 기본 제공 코드 생성기를 바꾸려면도 사용할 수 있는 코드 생성 플러그 인을 작성 하는 개발자 쉬워집니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-254">The Recipes framework makes it easy for developers to write code-generation plugins, which you can also use to replace the built-in code generators for Add Area, Add Controller, and Add View.</span></span> <span data-ttu-id="a9ddf-255">레시피는 NuGet 패키지로 배포 때문에 쉽게 소스 제어에 체크 인 고 수 자동으로 프로젝트에 모든 개발자와 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-255">Because recipes are deployed as NuGet packages, they can easily be checked into source control and shared with all developers on the project automatically.</span></span> <span data-ttu-id="a9ddf-256">솔루션 당 단위로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-256">They are also available on a per-solution basis.</span></span>

<a id="_Toc303253813"></a>
### <a name="task-support-for-asynchronous-controllers"></a><span data-ttu-id="a9ddf-257">비동기 컨트롤러에 대 한 작업 지원</span><span class="sxs-lookup"><span data-stu-id="a9ddf-257">Task Support for Asynchronous Controllers</span></span>

<span data-ttu-id="a9ddf-258">작성할 수 있습니다 비동기 작업 메서드 형식의 개체를 반환 하는 단일 메서드 *태스크* 하거나 *태스크&lt;ActionResult&gt;* 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-258">You can now write asynchronous action methods as single methods that return an object of type *Task* or *Task&lt;ActionResult&gt;*.</span></span>

<span data-ttu-id="a9ddf-259">예를 들어, Visual C# 5를 사용 하는 경우 (또는 사용 하 여는 [비동기 CTP](https://msdn.microsoft.com/vstudio/async.aspx))를 다음 처럼 보이는 비동기 동작 메서드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-259">For example, if you're using Visual C# 5 (or using the [Async CTP](https://msdn.microsoft.com/vstudio/async.aspx)), you can create an asynchronous action method that looks like the following:</span></span>

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample8.cs)]

<span data-ttu-id="a9ddf-260">이전 작업 메서드에서 호출 *newsService.GetHeadlinesAsync* 하 고 *sportsService.GetScoresAsync* 비동기적으로 호출 되 고 스레드 풀에서 스레드를 차단 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-260">In the previous action method, the calls to *newsService.GetHeadlinesAsync* and *sportsService.GetScoresAsync* are called asynchronously and do not block a thread from the thread pool.</span></span>

<span data-ttu-id="a9ddf-261">반환 하는 비동기 작업 메서드 *태스크* 인스턴스 시간 제한도 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-261">Asynchronous action methods that return *Task* instances can also support timeouts.</span></span> <span data-ttu-id="a9ddf-262">취소 가능한 작업 메서드를 확인, 형식의 매개 변수를 추가 *CancellationToken* 작업 메서드 서명에 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-262">To make your action method cancellable, add a parameter of type *CancellationToken* to the action method signature.</span></span> <span data-ttu-id="a9ddf-263">다음 예제에서는 2500 시간 (밀리초)의 제한 시간을 포함 하 고 표시 하는 비동기 동작 메서드를 *TimedOut* 시간 초과가 발생 하는 경우 클라이언트에 보기.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-263">The following example shows an asynchronous action method that has a timeout of 2500 milliseconds and that displays a *TimedOut* view to the client if a timeout occurs.</span></span>

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample9.cs)]

<a id="_Toc303253814"></a>
### <a name="azure-sdk"></a><span data-ttu-id="a9ddf-264">Azure SDK</span><span class="sxs-lookup"><span data-stu-id="a9ddf-264">Azure SDK</span></span>

<span data-ttu-id="a9ddf-265">ASP.NET MVC 4 베타는 Windows Azure SDK 1.5 2011 년 9 월 릴리스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-265">ASP.NET MVC 4 Beta supports the September 2011 1.5 release of the Windows Azure SDK.</span></span>

<a id="_Toc303253815"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="a9ddf-266">알려진된 문제 및 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="a9ddf-266">Known Issues and Breaking Changes</span></span>

- <span data-ttu-id="a9ddf-267">**ASP.NET MVC 4 베타를 설치한 후 Visual Studio 2010 서비스 팩 1 CSHTML/VBHTML 편집기의 CSHTML/VBHTML 편집기 있습니다 cshtml 또는 vbhtml 파일 내에서 코드 조각 또는 JavaScript 코드를 입력 한 후 오랫동안 일시 중지 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a9ddf-267">**After installing ASP.NET MVC 4 Beta, the CSHTML/VBHTML editor in Visual Studio 2010 Service Pack 1 CSHTML/VBHTML editor may pause for a long time after typing snippet or JavaScript inside cshtml or vbhtml files.**</span></span> <span data-ttu-id="a9ddf-268">이 아직 컴파일되지 않습니다 하 고 방금 만든 ASP.NET MVC 4 응용 프로그램 에서만 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-268">This occurs only in ASP.NET MVC 4 applications which have just been created and have not yet been compiled.</span></span>

    <span data-ttu-id="a9ddf-269">Bin 폴더에 어셈블리를 가져올 프로젝트를 컴파일하는 데이 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-269">The workaround is to compile the project to get the assemblies in the bin folder.</span></span> <span data-ttu-id="a9ddf-270">Note bin 폴더에서 어셈블리를 제거 하는 프로젝트를 정리 하는 경우 편집기 문제 다시 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-270">Note, if you clean the project which removes the assemblies from the bin folder, the editor problem will come back.</span></span>

    <span data-ttu-id="a9ddf-271">이 다음 릴리스에서 수정 될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-271">This will be corrected in the next release.</span></span>
- <span data-ttu-id="a9ddf-272">**Visual Studio 11 Beta 용 C# 프로젝트 템플릿 Global.asax.cs에서 잘못 된 연결 문자열을 포함 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a9ddf-272">**C# Project templates for Visual Studio 11 Beta contain an incorrect connection string in Global.asax.cs.**</span></span> <span data-ttu-id="a9ddf-273">응용 프로그램에서 지정 된 기본 연결이\_언 이스케이프 된 백슬래시를 포함 하는 LocalDB 연결 문자열을 포함 하는 Visual Studio 11 Beta에서 만든 프로젝트에 대 한 Start 메서드 (\) 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-273">The default connection specified in the Application\_Start method for projects created in Visual Studio 11 Beta contain a LocalDB connection string which contains an unescaped backslash (\) character.</span></span> <span data-ttu-id="a9ddf-274">이 인해 SqlException를 생성 하는 Entity Framework DbContext에 액세스 하려고 하면 연결 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-274">This results in a connection error upon attempts to access a Entity Framework DbContext, which generates a SqlException.</span></span>

    <span data-ttu-id="a9ddf-275">이 문제를 해결 하려면 앱에서 백슬래시를 이스케이프\_다음과 같이 읽을 수 있도록 Global.asax.cs의 메서드를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-275">To correct this issue, escape the backslash character in the App\_Start method of Global.asax.cs so that it reads as follows:</span></span>

    [!code-csharp[Main](mvc4-beta-release-notes/samples/sample10.cs)]
- <span data-ttu-id="a9ddf-276">**.NET 4.5를 대상으로 하는 ASP.NET MVC 4 응용 프로그램에.NET 4.0에서 실행 될 경우 System.Net.Http.dll 어셈블리에 액세스 하려고 하면 FileLoadException throw 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="a9ddf-276">**ASP.NET MVC 4 applications which target .NET 4.5 will throw a FileLoadException upon attempt to access the System.Net.Http.dll assembly when run under .NET 4.0.**</span></span> <span data-ttu-id="a9ddf-277">.NET 4.5에서 만든 ASP.NET MVC 4 응용 프로그램 바인딩을 포함 되어 있는 상태는 FileLoadException 될 리디렉션 로드할 수 없음"파일이 나 어셈블리 'System.Net.Http' 또는 해당 종속성 중 하나입니다."</span><span class="sxs-lookup"><span data-stu-id="a9ddf-277">ASP.NET MVC 4 applications created under .NET 4.5 contain a binding redirect that will result in a FileLoadException which that states "Could not load file or assembly 'System.Net.Http' or one of its dependencies."</span></span> <span data-ttu-id="a9ddf-278">때 응용 프로그램이.NET 4.0이 설치 된 시스템에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-278">when the application is executed on a system with .NET 4.0 installed.</span></span> <span data-ttu-id="a9ddf-279">이 문제를 해결 하려면 다음 바인딩 리디렉션을 web.config에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-279">To correct this issue, remove the following binding redirect from web.config:</span></span>

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample11.xml)]

    <span data-ttu-id="a9ddf-280">수정 된 web.config에 어셈블리 바인딩 요소는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-280">The assembly binding element in the modified web.config should appear as follows:</span></span>

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample12.xml)]
- <span data-ttu-id="a9ddf-281"><strong>Visual Basic 프로젝트에서 "컨트롤러 추가" 항목 템플릿을 호출할 때 잘못 된 네임 스페이스를 생성</strong><strong>에서 영역 내에서.</strong></span><span class="sxs-lookup"><span data-stu-id="a9ddf-281"><strong>The "Add Controller" item template in Visual Basic projects generates an incorrect namespace when invoked</strong><strong>from inside an area.</strong></span></span> <span data-ttu-id="a9ddf-282">Visual Basic을 사용 하는 ASP.NET MVC 프로젝트에서 영역에 컨트롤러를 추가 하는 경우 항목 템플릿을 컨트롤러에 잘못 된 네임 스페이스를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-282">When you add a controller to an area in an ASP.NET MVC project that uses Visual Basic, the item template inserts the wrong namespace into the controller.</span></span> <span data-ttu-id="a9ddf-283">결과 컨트롤러의 모든 작업을 이동할 때 "파일이 없습니다." 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-283">The result is a "file not found" error when you navigate to any action in the controller.</span></span>  
  
  <span data-ttu-id="a9ddf-284">생성된 된 네임 스페이스 루트 네임 스페이스 후 모든 것을 생략합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-284">The generated namespace omits everything after the root namespace.</span></span> <span data-ttu-id="a9ddf-285">생성 된 네임 스페이스는 예를 들어 *RootNamespace* 있지만 있어야 *RootNamespace.Areas.AreaName.Controllers* 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-285">For example, the namespace generated is *RootNamespace* but should be *RootNamespace.Areas.AreaName.Controllers* .</span></span>
- <span data-ttu-id="a9ddf-286">**Razor 보기 엔진의 주요 변경 내용입니다.**</span><span class="sxs-lookup"><span data-stu-id="a9ddf-286">**Breaking changes in the Razor View Engine.**</span></span> <span data-ttu-id="a9ddf-287">Razor 파서를 다시 작성의 일부로, 다음 형식에서 제거 되었습니다 *System.Web.Mvc.Razor*:</span><span class="sxs-lookup"><span data-stu-id="a9ddf-287">As part of a rewrite of the Razor parser, the following types were removed from *System.Web.Mvc.Razor*:</span></span> 

    - <span data-ttu-id="a9ddf-288">*ModelSpan*</span><span class="sxs-lookup"><span data-stu-id="a9ddf-288">*ModelSpan*</span></span>
    - <span data-ttu-id="a9ddf-289">*MvcVBRazorCodeGenerator*</span><span class="sxs-lookup"><span data-stu-id="a9ddf-289">*MvcVBRazorCodeGenerator*</span></span>
    - <span data-ttu-id="a9ddf-290">*MvcCSharpRazorCodeGenerator*</span><span class="sxs-lookup"><span data-stu-id="a9ddf-290">*MvcCSharpRazorCodeGenerator*</span></span>
    - <span data-ttu-id="a9ddf-291">*MvcVBRazorCodeParser*</span><span class="sxs-lookup"><span data-stu-id="a9ddf-291">*MvcVBRazorCodeParser*</span></span>

  <span data-ttu-id="a9ddf-292">다음 방법 또한 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-292">The following methods were also removed:</span></span> 

    - <span data-ttu-id="a9ddf-293">*MvcCSharpRazorCodeParser.ParseInheritsStatement(System.Web.Razor.Parser.CodeBlockInfo)*</span><span class="sxs-lookup"><span data-stu-id="a9ddf-293">*MvcCSharpRazorCodeParser.ParseInheritsStatement(System.Web.Razor.Parser.CodeBlockInfo)*</span></span>
    - <span data-ttu-id="a9ddf-294">*MvcWebPageRazorHost.DecorateCodeGenerator(System.Web.Razor.Generator.RazorCodeGenerator)*</span><span class="sxs-lookup"><span data-stu-id="a9ddf-294">*MvcWebPageRazorHost.DecorateCodeGenerator(System.Web.Razor.Generator.RazorCodeGenerator)*</span></span>
    - <span data-ttu-id="a9ddf-295">*MvcVBRazorCodeParser.ParseInheritsStatement(System.Web.Razor.Parser.CodeBlockInfo)*</span><span class="sxs-lookup"><span data-stu-id="a9ddf-295">*MvcVBRazorCodeParser.ParseInheritsStatement(System.Web.Razor.Parser.CodeBlockInfo)*</span></span>
- <span data-ttu-id="a9ddf-296">**WebMatrix.WebData.dll는 ASP.NET MVC 4 응용 프로그램의 /bin 디렉터리에 포함 되어 있으면, 폼 인증에 대 한 URL을 통해 걸립니다.**</span><span class="sxs-lookup"><span data-stu-id="a9ddf-296">**When WebMatrix.WebData.dll is included in the /bin directory of an ASP.NET MVC 4 apps, it takes over the URL for forms authentication.**</span></span> <span data-ttu-id="a9ddf-297">/ 계정 로그온에 대 한 인증 로그인 리디렉션을 재정의 WebMatrix.WebData.dll 어셈블리를 응용 프로그램 (예를 들어, 선택 하 여 추가 "Razor 구문을 사용 하 여 ASP.NET 웹 페이지" 배포 가능 종속성 추가 대화 상자를 사용 하는 경우) 대신 / 기본 ASP.NET MVC 계정 컨트롤러 예상 대로 계정 로그인입니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-297">Adding the WebMatrix.WebData.dll assembly to your application (for example, by selecting "ASP.NET Web Pages with Razor Syntax" when using the Add Deployable Dependencies dialog) will override the authentication login redirect to /account/logon rather than /account/login as expected by the default ASP.NET MVC Account Controller.</span></span> <span data-ttu-id="a9ddf-298">이 문제를 방지 하 고 web.config의 인증 섹션에서 이미 지정 된 URL을 사용 하려면 PreserveLoginUrl 이라는 appSetting을 추가 하 고 true로 설정:</span><span class="sxs-lookup"><span data-stu-id="a9ddf-298">To prevent this behavior and use the URL specified already in the authentication section of web.config, you can add an appSetting called PreserveLoginUrl and set it to true:</span></span> 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample13.xml)]
- <span data-ttu-id="a9ddf-299">**NuGet 패키지 관리자 Visual Studio 2010 및 Visual Web Developer 2010의 병렬 설치에 대 한 ASP.NET MVC 4를 설치 하려고 하면 설치에 실패 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a9ddf-299">**The NuGet package manager fails to install when attempting to install ASP.NET MVC 4 for side by side installations of Visual Studio 2010 and Visual Web Developer 2010.**</span></span> <span data-ttu-id="a9ddf-300">Visual Studio 2010 및 Visual Web Developer 2010 ASP.NET MVC 4와 함께 실행 하려면 두 버전의 Visual Studio가 이미 설치 된 후 ASP.NET MVC 4를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-300">To run Visual Studio 2010 and Visual Web Developer 2010 side by side with ASP.NET MVC 4 you must install ASP.NET MVC 4 after both versions of Visual Studio have already been installed.</span></span>
- <span data-ttu-id="a9ddf-301">**ASP.NET MVC 4를 제거 하면 필수 구성 요소가 이미 제거 된 경우 실패 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a9ddf-301">**Uninstalling ASP.NET MVC 4 fails if prerequisites have already been uninstalled.**</span></span> <span data-ttu-id="a9ddf-302">ASP.NET MVC를 완전히 제거할 4you Visual Studio를 제거 하기 전에 ASP.NET MVC 4를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-302">To cleanly uninstall ASP.NET MVC 4you must uninstall ASP.NET MVC 4 prior to uninstalling Visual Studio.</span></span>
- <span data-ttu-id="a9ddf-303">**기본 Web API 프로젝트를 실행 합니다. 존재 하지 않는 RegisterApis 메서드를 사용 하 여 경로 추가할 사용자를 올바르게 지시 하는 지침을 보여 줍니다.**</span><span class="sxs-lookup"><span data-stu-id="a9ddf-303">**Running a default Web API project shows instructions that incorrectly direct the user to add routes using the RegisterApis method, which doesn't exist.**</span></span> <span data-ttu-id="a9ddf-304">경로 ASP.NET 경로 테이블을 사용 하 여 RegisterRoutes 메서드에 추가 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-304">Routes should be added in the RegisterRoutes method using the ASP.NET route table.</span></span>
- <span data-ttu-id="a9ddf-305">**ASP.NET MVC 3 RTM 응용 프로그램을 중단 ASP.NET MVC 4 베타를 설치 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a9ddf-305">**Installing ASP.NET MVC 4 Beta breaks ASP.NET MVC 3 RTM applications.**</span></span> <span data-ttu-id="a9ddf-306">생성 된 ASP.NET MVC 3 응용 프로그램 (없습니다 사용 하 여 ASP.NET MVC 3 도구 업데이트 릴리스에서) 릴리스 나란히 ASP.NET MVC 4 베타를 사용 하 여를 작동 하려면 다음과 같이 변경 해야 RTM을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-306">ASP.NET MVC 3 applications that were created with the RTM release (not with the ASP.NET MVC 3 Tools Update release) require the following changes in order to work side-by-side with ASP.NET MVC 4 Beta.</span></span> <span data-ttu-id="a9ddf-307">이러한 업데이트 결과 컴파일 오류가 발생에서 하지 않고 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-307">Building the project without making these updates results in compilation errors.</span></span> 

    <span data-ttu-id="a9ddf-308">**필수 업데이트**</span><span class="sxs-lookup"><span data-stu-id="a9ddf-308">**Required updates**</span></span>

  1. <span data-ttu-id="a9ddf-309">루트 Web.config 파일에서 추가 된 새 *&lt;appSettings&gt;* 키를 사용 하 여 항목 *webPages:Version* 값 *1.0.0.0*합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-309">In the root Web.config file, add a new *&lt;appSettings&gt;* entry with the key *webPages:Version* and the value *1.0.0.0*.</span></span>

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample14.xml)]
  2. <span data-ttu-id="a9ddf-310">솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 프로젝트 언로드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-310">In Solution Explorer, right-click the project name and then select Unload Project.</span></span> <span data-ttu-id="a9ddf-311">그런 다음 이름을 다시 마우스 오른쪽 단추로 클릭 하 고 편집 선택 *ProjectName*.csproj 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-311">Then right-click the name again and select Edit *ProjectName*.csproj.</span></span>
  3. <span data-ttu-id="a9ddf-312">다음 어셈블리 참조를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-312">Locate the following assembly references:</span></span> 

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample15.xml)]

      <span data-ttu-id="a9ddf-313">다음을 사용 하 여 하를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-313">Replace them with the following:</span></span>

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample16.xml)]
  4. <span data-ttu-id="a9ddf-314">변경 내용을 저장, 하면 편집 된 프로젝트를 마우스 오른쪽 단추로 클릭을 선택한 다음 다시 로드 하 고 프로젝트 (.csproj) 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a9ddf-314">Save the changes, close the project (.csproj) file you were editing, and then right-click the project and select Reload.</span></span>
