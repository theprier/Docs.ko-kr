---
uid: web-pages/readme/beta3
title: Webmatrix 및 ASP.NET 웹 페이지 (Razor) 베타 3 릴리스 정보 | Microsoft Docs
author: rick-anderson
description: Webmatrix 및 ASP.NET 웹 페이지 (Razor) 베타 3 릴리스 추가 정보
ms.author: riande
ms.date: 01/10/2011
ms.assetid: ffa3d5c9-91e5-4da3-b409-560b0c7fbbf0
msc.legacyurl: /web-pages/readme/beta3
msc.type: content
ms.openlocfilehash: 3d729d1b0615533dddceff484acb3d42247f6cab
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41835776"
---
<a name="web-matrix-and-aspnet-web-pages-razor-beta-3-release-readme"></a><span data-ttu-id="0b290-103">Webmatrix 및 ASP.NET 웹 페이지 (Razor) 베타 3 릴리스 추가 정보</span><span class="sxs-lookup"><span data-stu-id="0b290-103">Web Matrix and ASP.NET Web Pages (Razor) Beta 3 Release Readme</span></span>
====================
> <span data-ttu-id="0b290-104">Webmatrix 및 ASP.NET 웹 페이지 (Razor) 베타 3 릴리스 추가 정보</span><span class="sxs-lookup"><span data-stu-id="0b290-104">Web Matrix and ASP.NET Web Pages (Razor) Beta 3 Release Readme</span></span>

<span data-ttu-id="0b290-105">2010 년 11 월 9</span><span class="sxs-lookup"><span data-stu-id="0b290-105">9 November 2010</span></span>

## <a name="contents"></a><span data-ttu-id="0b290-106">목차</span><span class="sxs-lookup"><span data-stu-id="0b290-106">Contents</span></span>

- [<span data-ttu-id="0b290-107">개요</span><span class="sxs-lookup"><span data-stu-id="0b290-107">Overview</span></span>](#Overview)
- [<span data-ttu-id="0b290-108">설치</span><span class="sxs-lookup"><span data-stu-id="0b290-108">Installation</span></span>](#Installation_Notes)
- [<span data-ttu-id="0b290-109">새 기능, 변경 및 Beta 3 릴리스에의 알려진 문제</span><span class="sxs-lookup"><span data-stu-id="0b290-109">New Features, Changes, and Known Issues in the Beta 3 release</span></span>](#Known_Issues)

    - [<span data-ttu-id="0b290-110">WebMatrix 설치 문제</span><span class="sxs-lookup"><span data-stu-id="0b290-110">WebMatrix Installation Issues</span></span>](#Known_Issues_Installation)
    - [<span data-ttu-id="0b290-111">ASP.NET 웹 페이지 2</span><span class="sxs-lookup"><span data-stu-id="0b290-111">ASP.NET Web Pages</span></span>](#Known_Issues_ASPNET)
    - [<span data-ttu-id="0b290-112">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="0b290-112">SQL Server Compact</span></span>](#Known_Issues_SQL_Server_Compact)
    - [<span data-ttu-id="0b290-113">응용 프로그램 설치</span><span class="sxs-lookup"><span data-stu-id="0b290-113">Installing Applications</span></span>](#Known_Issues_Installing_Applications)
    - [<span data-ttu-id="0b290-114">응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="0b290-114">Publishing Applications</span></span>](#Known_Issues_Publishing_Applications)
    - [<span data-ttu-id="0b290-115">기타 문제</span><span class="sxs-lookup"><span data-stu-id="0b290-115">Other Issues</span></span>](#Known_Issues_Other_Issues)
- [<span data-ttu-id="0b290-116">자세한 내용은</span><span class="sxs-lookup"><span data-stu-id="0b290-116">For More Information</span></span>](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a><span data-ttu-id="0b290-117">개요</span><span class="sxs-lookup"><span data-stu-id="0b290-117">Overview</span></span>

> <span data-ttu-id="0b290-118">Microsoft WebMatrix 베타는 몇 분 안에 설치 하는 무료 웹 개발 스택입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-118">Microsoft WebMatrix Beta is a free web development stack that installs in minutes.</span></span> <span data-ttu-id="0b290-119">데이터베이스 및 프로그래밍 프레임 워크를 단일 통합된 환경 만들기를 사용 하 여 웹 서버를 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-119">It integrates a web server with database and programming frameworks to create a single, integrated experience.</span></span> <span data-ttu-id="0b290-120">WebMatrix 베타를 사용 하 여 코드, 테스트 및 고유한 ASP.NET 또는 PHP 웹 사이트를 게시 하는 방법을 간소화할 수 있습니다 또는 DotNetNuke, Umbraco, WordPress 또는 Joomla와 같은 인기 있는 오픈 소스 앱을 사용 하 여 새 웹 사이트를 시작 하려면 WebMatrix 베타를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-120">You can use WebMatrix Beta to streamline the way you code, test, and publish your own ASP.NET or PHP website, or you can use WebMatrix Beta to start a new website using popular open-source apps like DotNetNuke, Umbraco, WordPress, or Joomla.</span></span> <span data-ttu-id="0b290-121">WebMatrix 베타 같은 강력한 웹 서버, 데이터베이스 엔진 및 원활 하 게 개발에서 프로덕션으로 전환 하면 인터넷에서 웹 사이트를 실행 되는 프레임 워크 환경을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-121">WebMatrix Beta uses the same powerful web server, database engine, and frameworks environment that will run your website on the internet, which makes the transition from development to production smooth and seamless.</span></span>


<a id="Installation_Notes"></a>

## <a name="installation"></a><span data-ttu-id="0b290-122">설치</span><span class="sxs-lookup"><span data-stu-id="0b290-122">Installation</span></span>

> <span data-ttu-id="0b290-123">사용할 WebMatrix 베타 3을 설치 하려면 [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-123">To install WebMatrix Beta 3, you use [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span> <span data-ttu-id="0b290-124">웹 플랫폼 설치 관리자를 설치한 후에 WebMatrix 베타 3을 설치 하려면 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-124">After you've installed the Web Platform Installer, you can use it to install WebMatrix Beta 3.</span></span>
> 
> <span data-ttu-id="0b290-125">설치 중에 문제가 있는 경우 가리킵니다 [Microsoft 웹 플랫폼 설치 관리자를 사용 하 여 문제 해결](https://go.microsoft.com/fwlink/?LinkId=196212)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-125">If you have problems during installation, refer to [Troubleshooting Problems with Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).</span></span>


<a id="Installation_Notes0"></a>

## <a name="instructions-for-publishing-applications"></a><span data-ttu-id="0b290-126">응용 프로그램을 게시 하기 위한 지침</span><span class="sxs-lookup"><span data-stu-id="0b290-126">Instructions for Publishing Applications</span></span>

> <span data-ttu-id="0b290-127">참조 [응용 프로그램을 게시 하기 위한 단계별 지침](https://go.microsoft.com/fwlink/?LinkID=196149)</span><span class="sxs-lookup"><span data-stu-id="0b290-127">See [Step-by-Step Instructions for Publishing Applications](https://go.microsoft.com/fwlink/?LinkID=196149)</span></span>


<a id="Known_Issues"></a>

## <a name="new-features-changes-andknown-issues"></a><span data-ttu-id="0b290-128">새 기능을 변경 andKnown 문제</span><span class="sxs-lookup"><span data-stu-id="0b290-128">New Features, Changes, andKnown Issues</span></span>

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-beta-3-installation"></a><span data-ttu-id="0b290-129">WebMatrix 베타 3 설치</span><span class="sxs-lookup"><span data-stu-id="0b290-129">WebMatrix Beta 3 Installation</span></span>

#### <a name="issue-webmatrix-beta-3-is-only-available-on-platforms-that-support-microsoft-net-framework-4"></a><span data-ttu-id="0b290-130">문제: WebMatrix Beta 3은 Microsoft.NET Framework 4를 지 원하는 플랫폼에서 사용할 수 있습니다만</span><span class="sxs-lookup"><span data-stu-id="0b290-130">Issue: WebMatrix Beta 3 is only available on platforms that support Microsoft .NET Framework 4</span></span>

> <span data-ttu-id="0b290-131">.NET Framework 버전 4가 WebMatrix 베타 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-131">The .NET Framework version 4 is required for WebMatrix Beta.</span></span> <span data-ttu-id="0b290-132">특정 경우에 지원 되는 구성 집합의 일부가 아닌 플랫폼에 설치 하려고 하면 WebMatrix 베타 설치 관리자 그러면 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-132">In certain cases, the WebMatrix Beta installer will let you try to install on a platform that is not part of the supported configuration set.</span></span> <span data-ttu-id="0b290-133">특히 Windows Vista SP1 업데이트를 사용 하면 WebMatrix 베타 설치를 시작할 수 있지만.NET Framework 4 구성 요소 실패를 업데이트 하 고 설치를 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-133">In particular, Windows Vista without the SP1 update will let you begin the installation of WebMatrix Beta, but the .NET Framework 4 component will fail and block your installation.</span></span>
> 
> <span data-ttu-id="0b290-134">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-134">**Workaround**</span></span>  
> <span data-ttu-id="0b290-135">포함 하는 지원 되는 플랫폼에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-135">Install on a supported platform, which includes:</span></span>
> 
> - <span data-ttu-id="0b290-136">Windows 7</span><span class="sxs-lookup"><span data-stu-id="0b290-136">Windows 7</span></span>
> - <span data-ttu-id="0b290-137">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="0b290-137">Windows Server 2008</span></span>
> - <span data-ttu-id="0b290-138">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="0b290-138">Windows Server 2008 R2</span></span>
> - <span data-ttu-id="0b290-139">Windows Vista SP1 이상</span><span class="sxs-lookup"><span data-stu-id="0b290-139">Windows Vista SP1 or later</span></span>
> - <span data-ttu-id="0b290-140">Windows XP SP3</span><span class="sxs-lookup"><span data-stu-id="0b290-140">Windows XP SP3</span></span>
> - <span data-ttu-id="0b290-141">Windows Server 2003 SP2</span><span class="sxs-lookup"><span data-stu-id="0b290-141">Windows Server 2003 SP2</span></span>


#### <a name="issue-cannot-install-webmatrix-beta-3-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a><span data-ttu-id="0b290-142">문제: Microsoft Visual Studio 2008은 Microsoft Visual Studio 2008 SP1 없이 설치 된 경우 WebMatrix 베타 3을 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-142">Issue: Cannot install WebMatrix Beta 3 if Microsoft Visual Studio 2008 is installed without Microsoft Visual Studio 2008 SP1</span></span>

> <span data-ttu-id="0b290-143">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-143">**Workaround**</span></span>  
> <span data-ttu-id="0b290-144">설치할 [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) Microsoft 다운로드 센터에서.</span><span class="sxs-lookup"><span data-stu-id="0b290-144">Install [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) from the Microsoft Download Center.</span></span>


#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a><span data-ttu-id="0b290-145">문제: SQL Server Compact 4.0에 대 한 일부 어셈블리는 GAC에 설치 되지</span><span class="sxs-lookup"><span data-stu-id="0b290-145">Issue: Some assemblies for SQL Server Compact 4.0 are not installed in the GAC</span></span>

> <span data-ttu-id="0b290-146">64 비트 컴퓨터에서 SQL Server Compact 4.0을 설치 하 고 컴퓨터 프로필에만.NET Framework 3.5 SP1 클라이언트 설치에 SQL Server Compact 4.0 용 관리 되는 어셈블리를 전역 어셈블리 캐시 (GAC)에 배치 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-146">The managed assemblies for SQL Server Compact 4.0 are not placed in the global assembly cache (GAC) when you install SQL Server Compact 4.0 on a 64-bit computer and the computer has only the .NET Framework 3.5 SP1 Client Profile installed.</span></span> <span data-ttu-id="0b290-147">GAC에 설치 되지 않은 관리 되는 어셈블리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-147">The managed assemblies that are not installed in the GAC are:</span></span>
> 
> - <span data-ttu-id="0b290-148">*System.Data.SqlServerCe.dll* (ADO.NET 공급자)</span><span class="sxs-lookup"><span data-stu-id="0b290-148">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span></span>
> - <span data-ttu-id="0b290-149">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework)</span><span class="sxs-lookup"><span data-stu-id="0b290-149">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span></span>
> 
> <span data-ttu-id="0b290-150">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-150">**Workaround**</span></span>  
> <span data-ttu-id="0b290-151">제거할 SQL Server Compact 4.0입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-151">Uninstall SQL Server Compact 4.0.</span></span> <span data-ttu-id="0b290-152">다운로드 하 고 다음 위치에서.NET Framework 3.5 SP1의 정식 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-152">Download and install the full version of .NET Framework 3.5 SP1 from the following location:</span></span>  
>   
> [<span data-ttu-id="0b290-153">Microsoft.NET Framework 3.5 서비스 팩 1 (전체 패키지)</span><span class="sxs-lookup"><span data-stu-id="0b290-153">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> <span data-ttu-id="0b290-154">SQL Server Compact 4.0를 다시 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-154">Then reinstall SQL Server Compact 4.0.</span></span>


#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a><span data-ttu-id="0b290-155">문제: SQL Server Compact는 명령줄을 사용 하 여 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-155">Issue: Cannot uninstall SQL Server Compact using the command line</span></span>

> <span data-ttu-id="0b290-156">SQL Server Compact 명령줄 옵션을 사용 하 여 제거는이 릴리스에서 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-156">Uninstallation of SQL Server Compact using command-line options does not work in this release.</span></span>
> 
> <span data-ttu-id="0b290-157">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-157">**Workaround**</span></span>  
> <span data-ttu-id="0b290-158">사용 하 여 *프로그램 및 기능* Microsoft SQL Server Compact 4.0을 제거 하려면 Windows 제어판에서.</span><span class="sxs-lookup"><span data-stu-id="0b290-158">Use *Programs and Features* in the Windows Control Panel to uninstall Microsoft SQL Server Compact 4.0.</span></span>


<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a><span data-ttu-id="0b290-159">ASP.NET 웹 페이지</span><span class="sxs-lookup"><span data-stu-id="0b290-159">ASP.NET Web Pages</span></span>

<span data-ttu-id="0b290-160">문서의이 섹션에서는 새로운 기능, 변경 및 Razor 구문이 있는 ASP.NET 웹 페이지의 베타 3 릴리스를 사용 하 여 알려진된 문제에 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-160">This section of the document describes new features, changes, and known issues with the Beta 3 release of ASP.NET Web Pages with Razor syntax.</span></span>

- [<span data-ttu-id="0b290-161">새로운 기능</span><span class="sxs-lookup"><span data-stu-id="0b290-161">New features</span></span>](#NewFeatures)
- [<span data-ttu-id="0b290-162">변경 내용</span><span class="sxs-lookup"><span data-stu-id="0b290-162">Changes</span></span>](#Changes)
- [<span data-ttu-id="0b290-163">문제</span><span class="sxs-lookup"><span data-stu-id="0b290-163">Issues</span></span>](#Issues)

<a id="NewFeatures"></a>

#### <a name="new-features-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="0b290-164">Razor 구문이 있는 ASP.NET 웹 페이지에 대 한 베타 3의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="0b290-164">New Features in Beta 3 for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="new-htmlraw-method-renders-unencoded-markup"></a><span data-ttu-id="0b290-165">"Html.Raw" 메서드 인코딩되지 않은 태그를 렌더링 하는 새로운 기능:</span><span class="sxs-lookup"><span data-stu-id="0b290-165">New: "Html.Raw" method renders unencoded markup</span></span>

> <span data-ttu-id="0b290-166">새 `Html.Raw` 메서드를 사용 하면 인코딩된 출력을 렌더링 하는 대신 태그로 HTML 태그를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-166">The new `Html.Raw` method lets you render HTML markup as markup instead of rendering encoded output.</span></span> <span data-ttu-id="0b290-167">(기본적으로 ASP.NET Razor 인코딩합니다 문자열을 렌더링 하기 전에.) 사용되는 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-167">(By default, ASP.NET Razor encodes strings before rendering them.) The syntax is:</span></span>
> 
> `Html.Raw(value)`
> 
> <span data-ttu-id="0b290-168">다음 예제에서는 `Html.Raw`을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-168">The following example shows how to use `Html.Raw`:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample1.cshtml)]


<a id="Changes"></a>

#### <a name="changes-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="0b290-169">Razor 구문이 있는 ASP.NET 웹 페이지의 Beta 3의에서 변경 내용</span><span class="sxs-lookup"><span data-stu-id="0b290-169">Changes in Beta 3 for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="change-hrefattribute-method-removed"></a><span data-ttu-id="0b290-170">변경 내용: "HrefAttribute" 메서드가 제거</span><span class="sxs-lookup"><span data-stu-id="0b290-170">Change: "HrefAttribute" method removed</span></span>

> <span data-ttu-id="0b290-171">합니다 `HrefAttribute` 메서드는 `WebPage` 클래스가 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-171">The `HrefAttribute` method of the `WebPage` class has been removed.</span></span> <span data-ttu-id="0b290-172">이 도우미는 Url에 안전 하지 않은 문자를 인코딩하는 데 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-172">This helper was used to encode unsafe characters in URLs.</span></span> <span data-ttu-id="0b290-173">ASP.NET Razor 자동으로 인코딩되고, 문자열 때문에 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-173">It is no longer required because ASP.NET Razor automatically encodes strings.</span></span> <span data-ttu-id="0b290-174">(새 `Html.Raw` 인코딩되지 않은 문자열을 렌더링 하는 방법입니다.)</span><span class="sxs-lookup"><span data-stu-id="0b290-174">(Use the new `Html.Raw` method to render unencoded strings.)</span></span>


#### <a name="change-syntax-for-declarative-helper-helpers-changed"></a><span data-ttu-id="0b290-175">변경: 구문에 대 한 선언적 "@helper" 변경 하는 도우미</span><span class="sxs-lookup"><span data-stu-id="0b290-175">Change: Syntax for declarative "@helper" helpers changed</span></span>

> <span data-ttu-id="0b290-176">Beta 3 릴리스에 ASP.NET 변경 하는 방법을 사용 하 여 만든 도우미를 구문 분석 된 `@helper` 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-176">In the Beta 3 release, ASP.NET changes how it parses helpers that are created using the `@helper` syntax.</span></span> <span data-ttu-id="0b290-177">기본적으로 `@helper` 구문은 이제 코드를 포함할 수 있는 태그 블록으로 대신 코드 블록으로 구문 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-177">In essence, the `@helper` syntax is now parsed as a code block instead of as a block of markup that can include code.</span></span> <span data-ttu-id="0b290-178">따라서 도우미 내부에서 코드 않아도 묶어야 `@{ }` 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-178">Therefore, code inside the helper does not need to be enclosed in `@{ }` blocks.</span></span> <span data-ttu-id="0b290-179">태그 도우미 내부에서 ASP.NET Razor 또는 HTML 요소에 명시적으로 포함 되도록에 반대로, `<text></text>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-179">Conversely, markup inside the helper has to be explicitly included in HTML elements or in ASP.NET Razor `<text></text>` tags.</span></span>
> 
> <span data-ttu-id="0b290-180">예를 들어, 다음 `@helper` 구문 Beta 3 릴리스에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-180">For example, the following `@helper` syntax works in the Beta 3 release:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample2.cshtml)]
> 
> <span data-ttu-id="0b290-181">Beta 3 릴리스에이 도우미를 다음과 같이 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-181">In the Beta 3 release, this helper must be changed to look like the following example:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample3.cshtml)]
> 
> <span data-ttu-id="0b290-182">에 `@{ }` 도우미에서 초기 코드 주위 문자는 더 이상 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-182">Notice that the `@{ }` characters around the initial code in the helper is no longer used.</span></span> <span data-ttu-id="0b290-183">즉, 기본적으로 도우미의 내용을 코드 블록으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-183">This is because the contents of the helpers are treated as a code block by default.</span></span> <span data-ttu-id="0b290-184">시작 하 여는 태그를 렌더링 하는 도우미 `<a>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-184">The helper renders markup, which starts with the opening `<a>` tag.</span></span> <span data-ttu-id="0b290-185">일반 텍스트 또는 닫는 태그를 포함 하지 않는 태그 도우미를 렌더링 해야 하는 경우 (예를 들어 `<meta>` 태그), 콘텐츠를 렌더링할에 있어야 합니다. `<text></text>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-185">If the helper must render plain text or tags that do not include a closing tag (for example, `<meta>` tags), the content to be rendered must be in `<text></text>` tags.</span></span>


#### <a name="change-webpagecontexthttpcontext-removed"></a><span data-ttu-id="0b290-186">변경 내용: "WebPageContext.HttpContext" 제거</span><span class="sxs-lookup"><span data-stu-id="0b290-186">Change: "WebPageContext.HttpContext" removed</span></span>

> <span data-ttu-id="0b290-187">`WebPageContext.HttpContext` 속성이 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-187">The `WebPageContext.HttpContext` property has been removed.</span></span> <span data-ttu-id="0b290-188">대신 `HttpContext.Current`를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="0b290-188">Use `HttpContext.Current` instead.</span></span> <span data-ttu-id="0b290-189">(의 `WebPageContext.HttpContext` 속성 래핑되어이.)</span><span class="sxs-lookup"><span data-stu-id="0b290-189">(The `WebPageContext.HttpContext` property simply wrapped this.)</span></span>


#### <a name="change-facebook-helper-moved-to-new-package"></a><span data-ttu-id="0b290-190">새 패키지를 이동 하는 변경 내용: "Facebook" 도우미</span><span class="sxs-lookup"><span data-stu-id="0b290-190">Change: "Facebook" helper moved to new package</span></span>

> <span data-ttu-id="0b290-191">`Facebook` 도우미로 이동 되었습니다 합니다 *Facebook.Helper* 포함 하는 라이브러리는 `Facebook` 도우미와 추가 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-191">The `Facebook` helper has been moved to the *Facebook.Helper* library, which includes the `Facebook` helper and additional functionality.</span></span> <span data-ttu-id="0b290-192">에 설치 해야이 라이브러리는 별도 패키지로 "패키지 관리자 사용 하 여 설치 도우미"에 설명 된 대로 자습서 [Getting Started with ASP.NET 페이지](https://go.microsoft.com/fwlink/?LinkId=202889)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-192">You must install this library as a separate package, as described in "Installing Helpers with Package Manager" in the tutorial [Getting Started with ASP.NET Pages](https://go.microsoft.com/fwlink/?LinkId=202889).</span></span>


#### <a name="change-membership-role-and-security-types-moves-to-new-assembly"></a><span data-ttu-id="0b290-193">새 어셈블리를 변경 합니다: 멤버 자격, 역할 및 보안 형식 이동</span><span class="sxs-lookup"><span data-stu-id="0b290-193">Change: Membership, Role, and Security types moves to new assembly</span></span>

> <span data-ttu-id="0b290-194">다음 형식에 이동 된는 `WebMatrix.WebData` 어셈블리:</span><span class="sxs-lookup"><span data-stu-id="0b290-194">The following types were moved to the `WebMatrix.WebData` assembly:</span></span>
> 
> - `ExtendedMembershipProvider`
> - `SimpleMembershipProvider`
> - `SimpleRoleProvider`
> - `WebSecurity`


#### <a name="change-tagbuilder-class-moved-to-systemwebwebpagesdll-assembly"></a><span data-ttu-id="0b290-195">변경 내용: ""는 TagBuilder 클래스 System.Web.WebPages.dll 어셈블리로 이동</span><span class="sxs-lookup"><span data-stu-id="0b290-195">Change: "TagBuilder" class moved to System.Web.WebPages.dll assembly</span></span>

> <span data-ttu-id="0b290-196">`TagBuilde` r 클래스 System.Web.WebPages.dll 어셈블리로 이동 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-196">The `TagBuilde` r class has been moved to the System.Web.WebPages.dll assembly.</span></span> <span data-ttu-id="0b290-197">이전에이 ASP.NET MVC의 일부 였던 어셈블리에 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-197">Previously, this was in an assembly that was part of ASP.NET MVC.</span></span> <span data-ttu-id="0b290-198">따라서 사용 하기 위해 ASP.NET MVC를 설치할 필요가 없습니다를 `TagBuilder` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-198">This change means that you do not have to install ASP.NET MVC in order to use the `TagBuilder` class.</span></span>
> 
> <span data-ttu-id="0b290-199">그러나 클래스는 여전히는 `System.Web.Mvc` 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-199">However, the class is still in the `System.Web.Mvc` namespace.</span></span> <span data-ttu-id="0b290-200">사용 하기 위해 합니다 `TagBuilder` 클래스 (예를 들어, 사용자 지정 ASP.NET Razor 도우미)를 네임 스페이스를 참조 해야 합니다 (예를 들어, 추가 하 여 `@using System.Web.Mvc` 코드에).</span><span class="sxs-lookup"><span data-stu-id="0b290-200">In order to use the `TagBuilder` class (for example, in a custom ASP.NET Razor helper), you must reference the namespace (for example, by adding `@using System.Web.Mvc` to your code).</span></span>


#### <a name="change-request-validation-syntax-changed-validation-class-removed"></a><span data-ttu-id="0b290-201">변경: 요청 유효성 검사 구문이 변경 되었습니다. "유효성 검사" 클래스 제거</span><span class="sxs-lookup"><span data-stu-id="0b290-201">Change: Request validation syntax changed; "Validation" class removed</span></span>

> <span data-ttu-id="0b290-202">Beta 3 릴리스에 개별 필드 또는 필드의 집합에 대 한 유효성 검사를 사용 하지 않도록 설정 하려면 호출 하 여는 `Validation.Exclude` 메서드를 유효성 검사에서 제외할 필드의 이름을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-202">In the Beta 3 release, to disable validation for an individual field or set of fields, you can call the `Validation.Exclude` method, passing in the name or names of the fields to exclude from validation.</span></span> <span data-ttu-id="0b290-203">새로운 구문 유효성 검사를 생략 하는 것에 대 한 Beta 3 릴리스에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-203">A new syntax is available in the Beta 3 release for bypassing validation.</span></span> <span data-ttu-id="0b290-204">`Validation` Beta 3에서 사용 하는 메서드가 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-204">The `Validation` method used in Beta 3 has been removed.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="0b290-205">웹 사이트와 같은 오류를 보고 사용자 (예를 들어, 서식 있는 텍스트 편집기를 사용 하 여 페이지)에서 HTML 태그를 업로드 하려고 하는 경우 요청 유효성 검사를 해제 하지 않는 경우 *클라이언트에서잠재적으로위험한Request.Form값이검색되었습니다*사용자 입력이 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-205">If you do not disable request validation, if users try to upload HTML markup (for example, by using a rich text editor on a page), the website will report an error like *A potentially dangerous Request.Form value was detected from the client* and the user input is not accepted.</span></span> <span data-ttu-id="0b290-206">잠재적으로 위험한 태그를 포함 하거나 하지 같이 사용 하 여 스크립트 되도록 사용자 입력 요청 유효성 검사를 비활성화 하면 수동으로 확인 해야 합니다는 [Microsoft Anti-cross Site Scripting Library V4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-206">If you disable request validation, you must manually check user input to make sure that it does not contain potentially dangerous markup or script using something like the [Microsoft Anti-Cross Site Scripting Library V4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651).</span></span>
> 
> 
> <span data-ttu-id="0b290-207">자동 요청 유효성 검사를 해제 하려면 호출을 `Request.Unvalidated` 메서드, 필드 또는 다른 게시물 개체에 대 한 요청 유효성 검사를 무시 하려는 이름을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-207">To disable automatic request validation, call the `Request.Unvalidated` method, passing it the name of the field or other post object that you want to bypass request validation for.</span></span> <span data-ttu-id="0b290-208">이 메서드를 사용 하 여 모든 항목에 대 한 유효성 검사를 무시 하는 `Form`, `QueryString`를 `Cookies`, 및 `ServerVariables` 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-208">You can use this method to bypass validation for any items in the `Form`, `QueryString`, `Cookies`, and `ServerVariables` collections.</span></span> <span data-ttu-id="0b290-209">다음 예제에 사용 하는 방법을 보여 줍니다는 `Unvalidated` 메서드:</span><span class="sxs-lookup"><span data-stu-id="0b290-209">The following examples show how to use the `Unvalidated` method:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample4.cs)]


<a id="Issues"></a>

#### <a name="known-issues-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="0b290-210">Razor 구문이 있는 ASP.NET 웹 페이지에 대 한 알려진된 문제</span><span class="sxs-lookup"><span data-stu-id="0b290-210">Known Issues for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a><span data-ttu-id="0b290-211">문제: 예기치 않은 동작이 멤버 자격에 대 한 사용자 테이블을 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="0b290-211">Issue: Unexpected behavior when using a custom user table for membership</span></span>

> <span data-ttu-id="0b290-212">호출 하는 ASP.NET Razor 웹 사이트에 대 한 멤버 자격 공급자를 초기화 하는 `WebSecurity.InitializeDatabaseConnection` 메서드.</span><span class="sxs-lookup"><span data-stu-id="0b290-212">To initialize the membership provider for an ASP.NET Razor website, you call the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="0b290-213">(시작 사이트 템플릿의 WebMatrix에서이 메서드에 대 한 호출을 포함 합니다  *\_AppStart.cshtml* 파일입니다.) 경우는 `autoCreateTables` 이 메서드의 매개 변수 설정을 true로 (기본적으로 설정은 시작 사이트 템플릿의 true), 하며 메서드는 인식할 수 없는 테이블 이름 (두 번째 매개 변수) 메서드에 전달 되 면 오류가 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-213">(In WebMatrix, the Starter Site template includes a call to this method in the *\_AppStart.cshtml* file.) If the `autoCreateTables` parameter of this method is set to true (by default, it is set to true in the Starter Site template), and if an unrecognized table name is passed to the method (the second parameter), the method does not throw an error.</span></span> <span data-ttu-id="0b290-214">대신 테이블을 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-214">Instead, it automatically creates the table.</span></span>
> 
> <span data-ttu-id="0b290-215">이 멤버 자격에 대 한 사용자 테이블을 사용 하지만 잘못 된 테이블 이름을 전달 하려는 경우 문제가 될 수는 `WebSecurity.InitializeDatabaseConnection` 메서드.</span><span class="sxs-lookup"><span data-stu-id="0b290-215">This can be a problem if you intend to use a custom user table for membership but pass the wrong table name to the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="0b290-216">메서드는 기본적으로 오류가 발생 하지 지정한 테이블 없으면 및 대신 새 테이블을 만들기 때문에 응용 프로그램 작동에 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-216">Because the method does not by default raise an error if the table you specify does not exist, and because it instead creates a new table, the application can appear to be working.</span></span> <span data-ttu-id="0b290-217">그러나 사용자 테이블 (및 해당 필드에)를 사용 하는 응용 프로그램 코드 예기치 않은 오류를 사용 하 여 최종적으로 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-217">However, application code that relies on your custom user table (and on fields in it) can eventually fail with unexpected errors.</span></span>
> 
> <span data-ttu-id="0b290-218">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-218">**Workaround**</span></span>  
> <span data-ttu-id="0b290-219">이름에 성공 했는지 확인 합니다 `InitializeDatabaseConnection` 사용자 프로필 멤버 자격 데이터베이스에서 테이블 또는 했는지 메서드 일치를 `autoCreateTables` 매개 변수를 false로.</span><span class="sxs-lookup"><span data-stu-id="0b290-219">Make sure that the name passed in the `InitializeDatabaseConnection` method matches the user profile table in the membership database, or make sure that the `autoCreateTables` parameter is set to false.</span></span>


#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a><span data-ttu-id="0b290-220">문제: "못했습니다" SQL Server의 사용자 인스턴스 생성 오류</span><span class="sxs-lookup"><span data-stu-id="0b290-220">Issue: "Failed to generate a user instance of SQL Server" error</span></span>

> <span data-ttu-id="0b290-221">WebMatrix 웹 응용 프로그램을 SQL Server Express를 사용 하 여 Windows 7 또는 Windows Server 2008 R2에서 IIS 7.5를 실행 중인 경우 SQL Server가 런타임 시 사용자의 로컬 응용 프로그램 경로 검색할 수 없습니다 나타내는 오류가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-221">If a WebMatrix Web application uses SQL Server Express and is running IIS 7.5 on Windows 7 or Windows Server 2008 R2, you might see an error that indicates that SQL Server cannot retrieve the user's local application path at run time.</span></span>
> 
> <span data-ttu-id="0b290-222">**해결 방법** 응용 프로그램 (일반적으로 NETWORK SERVICE)에서 실행 되는 Windows 계정에 하위 폴더 및 응용 프로그램의 루트 폴더에 대 한 읽기/쓰기 권한을 같은 *앱\_데이터*.</span><span class="sxs-lookup"><span data-stu-id="0b290-222">**Workaround** Make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as *App\_Data*.</span></span> <span data-ttu-id="0b290-223">자세한 내용은 기술 자료 문서에서 사용할 수 [SQL Server Express 사용자 인스턴스 및 ASP.net 웹 응용 프로그램 프로젝트를 사용 하 여 문제](https://support.microsoft.com/kb/2002980)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-223">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>


#### <a name="issue-in-visual-studio-namespaces-for-custom-assemblies-dlls-are-not-imported-automatically"></a><span data-ttu-id="0b290-224">문제: Visual Studio에서 사용자 지정 어셈블리 (Dll)에 대 한 네임 스페이스는 자동 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-224">Issue: In Visual Studio, namespaces for custom assemblies (DLLs) are not imported automatically</span></span>

> <span data-ttu-id="0b290-225">Visual Studio에서 프로젝트의 사용자 지정 어셈블리를 사용 하는 경우에 디자인 타임에 해당 어셈블리에 선언 된 네임 스페이스는 자동으로 가져오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-225">If you use custom assemblies in a project in Visual Studio, the namespaces declared in those assemblies are not automatically imported at design time.</span></span> <span data-ttu-id="0b290-226">결과적으로, 사용자 지정 형식에 대 한 참조 디자인 타임에 인식 하지 않으며 ("물결선" 사용)에서 인식할 수 없는 Visual Studio로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-226">As a result, references to custom types might not be recognized at design time and are marked as not recognized in Visual Studio (using a "squiggle").</span></span> <span data-ttu-id="0b290-227">Visual Studio에서 디자인 타임에만이 문제가 발생 응용 프로그램 자체가 제대로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-227">This problem occurs only at design time in Visual Studio; the application itself runs properly.</span></span>
> 
> <span data-ttu-id="0b290-228">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-228">**Workaround**</span></span>  
> <span data-ttu-id="0b290-229">포함 된 `using` 문 (`imports` Visual Basic의) 디자인 타임에 인식 되지 않는 엔터티를 참조 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-229">Include a `using` statement (`imports` in Visual Basic) that references the entities that are not recognized at design time.</span></span>


#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a><span data-ttu-id="0b290-230">문제: Visual Studio IntelliSense 및 프로젝트 템플릿이 ASP.NET MVC 3 버전 에서만 사용할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="0b290-230">Issue: Visual Studio IntelliSense and project templates available only in ASP.NET MVC version 3</span></span>

> <span data-ttu-id="0b290-231">ASP.NET 웹 페이지를 설치 설치 하지 않습니다도 도구 Visual Studio에 대 한 예: ASP.NET Web Pages 응용 프로그램에 대 한 IntelliSense 및 프로젝트 템플릿.</span><span class="sxs-lookup"><span data-stu-id="0b290-231">Installing ASP.NET Web Pages does not also install tools for Visual Studio such as IntelliSense and project templates for ASP.NET Web Pages applications.</span></span>
> 
> <span data-ttu-id="0b290-232">**해결 방법** 웹 플랫폼 설치 관리자를 통해 ASP.NET MVC 3 RC 설치 Visual Studio에서 ASP.NET 웹 페이지 응용 프로그램에 대 한 IntelliSense 및 프로젝트 템플릿을 사용 하려면 또는 [독립 실행형 설치 관리자](https://go.microsoft.com/fwlink/?LinkID=191797)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-232">**Workaround** To use IntelliSense and project templates for ASP.NET Web Pages applications in Visual Studio, install ASP.NET MVC 3 RC either through the Web Platform Installer or the [stand-alone installer](https://go.microsoft.com/fwlink/?LinkID=191797).</span></span>


#### <a name="issue-lthelpergt-class-cannot-be-found-error"></a><span data-ttu-id="0b290-233">문제: "&lt;도우미&gt; 클래스를 찾을 수 없습니다" 오류</span><span class="sxs-lookup"><span data-stu-id="0b290-233">Issue: "&lt;helper&gt; class cannot be found" error</span></span>

> <span data-ttu-id="0b290-234">Beta 3으로 업그레이드 한 후 오류가 표시 될 수 있습니다 하는 도우미 클래스 (예를 들어를 `Facebook` 클래스)를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-234">After you upgrade to Beta 3, you might see an error that a helper class (for example, the `Facebook` class) cannot not be found.</span></span> <span data-ttu-id="0b290-235">Beta 2에서 시작 하 고 베타 3에서 계속에 명시적으로 설치 해야 하는 패키지 도우미 이동 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-235">Starting in Beta 2 and continuing in Beta 3, helpers have been moved to packages that you must explicitly install.</span></span> <span data-ttu-id="0b290-236">이러한 패키지를 포함 하도록 기존 사이트는 업그레이드 되지 않습니다. 여기에 사이트를 *\My Documents\IISExpress* 또는 *\My Documents\My 웹 사이트* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-236">Existing sites are not upgraded to include these packages; this includes sites in the *\My Documents\IISExpress* or *\My Documents\My Web Sites* folders.</span></span> <span data-ttu-id="0b290-237">기본 사이트를 사용 하는 경우이 오류가 표시 됩니다는 특히 *내 사이트* 에 대 한 참조를 포함 하는 (WebSite1)는 `Twitter` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-237">In particular, you will see this error if you use the default site in *My Sites* (WebSite1), which includes a reference to the `Twitter` helper.</span></span>
> 
> <span data-ttu-id="0b290-238">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-238">**Workaround**</span></span>  
> <span data-ttu-id="0b290-239">모든 도우미 사이트에서 실행에 대 한 호출을 주석 합니다  *\_관리자* 페이지 및 사용 하려는 도우미를 포함 하는 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-239">Comment out calls to any helpers in the site, run the *\_Admin* page, and install the package or packages that include the helpers that you want to use.</span></span> <span data-ttu-id="0b290-240">패키지를 설치한 후 도우미 참조 하는 줄을 주석 처리 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-240">After you've installed the package, you can uncomment the lines that reference helpers.</span></span>


#### <a name="issue-deploying-beta-3-aspnet-razor-assemblies-to-the-bin-folder-might-not-work-on-hosting-sites"></a><span data-ttu-id="0b290-241">문제: 베타 3 ASP.NET Razor 어셈블리를 Bin 폴더로 배포에서 작동할 수 없습니다 사이트 호스팅</span><span class="sxs-lookup"><span data-stu-id="0b290-241">Issue: Deploying Beta 3 ASP.NET Razor assemblies to the Bin folder might not work on hosting sites</span></span>

> <span data-ttu-id="0b290-242">호스팅 사이트에는 ASP.NET Web Pages 웹 사이트를 배포 하는 경우 및 사이트의 ASP.NET Razor 베타 3 어셈블리를 배포 하는 경우 *Bin* 폴더에 다음을 비롯 한 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-242">If you deploy an ASP.NET Web Pages website to a hosting site, and if you deploy the ASP.NET Razor Beta 3 assemblies to the site's *Bin* folder, you might experience errors, including the following:</span></span>
> 
> `Could not load type 'Microsoft.Web.Infrastructure.DynamicModuleHelper.DynamicModuleUtility' from assembly 'Microsoft.Web.Infrastructure, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
> 
> <span data-ttu-id="0b290-243">이 호스팅 공급자가 서버의 전역 어셈블리 캐시 (GAC)에 ASP.NET 웹 페이지 베타 1 어셈블리를 설치 하는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-243">This can happen if the hosting provider has installed the ASP.NET Web Pages Beta 1 assemblies into the server's global application cache (GAC).</span></span> <span data-ttu-id="0b290-244">GAC의 어셈블리 우선적으로 로컬에 설치 된 어셈블리를 *Bin* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-244">Assemblies in the GAC get precedence over assemblies installed locally in the *Bin* folder.</span></span>
> 
> <span data-ttu-id="0b290-245">**해결 방법** 오류가 표시 되는 공급자의 버전 간의 충돌로 인해 있는지 확인 하려면 호스팅 공급자에 게 문의 어셈블리 및 사용자.</span><span class="sxs-lookup"><span data-stu-id="0b290-245">**Workaround** Contact your hosting provider to confirm that the errors you are seeing are due to a conflict between the provider's versions of the assemblies and yours.</span></span> <span data-ttu-id="0b290-246">그렇다면, 호스팅 공급자는 서버의 GAC에 어셈블리를 업데이트 하는 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-246">If so, request that the hosting provider update the assemblies in the server's GAC.</span></span>


#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a><span data-ttu-id="0b290-247">문제: 프록시 서버를 통해 다른 외부 데이터 나 피드 읽기</span><span class="sxs-lookup"><span data-stu-id="0b290-247">Issue: Reading feeds or other external data via a proxy server</span></span>

> <span data-ttu-id="0b290-248">에 대 한 프록시 정보를 구성 해야 사이트를 실행 하는 서버를 프록시 서버로 보호 하는 경우는 *Web.config* 외부 사이트에서 제공 되는 정보를 읽을 수 있도록 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-248">If the server running the site is behind a proxy server, you might need to configure proxy information in the *Web.config* file in order to be able to read information that comes from outside your site.</span></span> <span data-ttu-id="0b290-249">예를 들어, 사용 하는 경우는 `ReCaptcha` 도우미 도우미 reCAPTCHA 서비스와 통신 하지만 프록시 서버에서 차단 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-249">For example, if you use the `ReCaptcha` helper, the helper communicates with the reCAPTCHA service, but might be blocked by your proxy server.</span></span> <span data-ttu-id="0b290-250">마찬가지로, 패키지 관리자를 사용한 피드 등 ASP.NET 웹 페이지에서 사용 되는 피드 프록시 구성이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-250">Similarly, feeds that are used in ASP.NET Web Pages, such as the feed used by the package manager, might require proxy configuration.</span></span>
> 
> <span data-ttu-id="0b290-251">패키지 피드를 사용 하거나 외부 서비스를 사용 하 여 작업에 문제가 있는 경우 다음 요소를 응용 프로그램의 루트에 배치 *Web.config* 파일:</span><span class="sxs-lookup"><span data-stu-id="0b290-251">If you experience problems in working with an external service or working with the package feed, put the following elements into your application's root *Web.config* file:</span></span>
> 
> [!code-xml[Main](beta3/samples/sample5.xml)]
> 
> <span data-ttu-id="0b290-252">프록시 서버를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [ &lt;프록시&gt; 요소 (네트워크 설정)](https://msdn.microsoft.com/library/sa91de1e.aspx) MSDN 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-252">For more information about configuring a proxy server, see [&lt;proxy&gt; Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on the MSDN Web site.</span></span>


#### <a name="issue-microsoftwebinfrastructuredll-cannot-be-loaded-error"></a><span data-ttu-id="0b290-253">문제: "Microsoft.Web.Infrastructure.dll를 로드할 수 없습니다." 오류</span><span class="sxs-lookup"><span data-stu-id="0b290-253">Issue: "Microsoft.Web.Infrastructure.dll cannot be loaded" error</span></span>

> <span data-ttu-id="0b290-254">이전에 Razor 구문이 있는 ASP.NET 웹 페이지의 베타 1 버전을 설치 하 고 다음 베타 3 버전을 설치 하는 경우 모든 적절 한 어셈블리 제외 하 고 GAC에 설치 됩니다 *Microsoft.Web.Infrastructure.dll*합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-254">If you previously installed the Beta 1 version of ASP.NET Web Pages with Razor syntax and then install the Beta 3 version, all appropriate assemblies are installed in the GAC except *Microsoft.Web.Infrastructure.dll*.</span></span> <span data-ttu-id="0b290-255">따라서 ASP.NET Razor 페이지를 실행 하면 오류가 발생 함을 *Microsoft.Web.Infrastructure.dll* 로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-255">As a consequence, when you run ASP.NET Razor pages, you see an error that indicates that *Microsoft.Web.Infrastructure.dll* could not be loaded.</span></span>
> 
> <span data-ttu-id="0b290-256">클린 컴퓨터에서 베타 3 릴리스를 로드 하는 경우에이 문제가 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-256">This issue does not occur if you loaded the Beta 3 release on a clean computer.</span></span>
> 
> <span data-ttu-id="0b290-257">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-257">**Workaround**</span></span>  
> <span data-ttu-id="0b290-258">제어판에서 ASP.NET 웹 페이지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-258">In Control Panel, uninstall ASP.NET Web Pages.</span></span> <span data-ttu-id="0b290-259">베타 3 릴리스를 다시 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-259">Then reinstall the Beta 3 release.</span></span>


#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="0b290-260">문제: Razor 구문이 있는 ASP.NET 웹 페이지를 사용 하지 않도록 설정.NET Framework 버전 4 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-260">Issue: Uninstalling the .NET Framework version 4 disables ASP.NET Web Pages with Razor Syntax</span></span>

> <span data-ttu-id="0b290-261">.NET Framework 버전 4 제거 하 고 다시 설치 하는 경우에 Razor 구문이 있는 ASP.NET 웹 페이지 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-261">If you uninstall the .NET Framework version 4 and then reinstall it, ASP.NET Web Pages with Razor syntax is disabled.</span></span> <span data-ttu-id="0b290-262">사용 하 여 페이지의 *.cshtml* 확장 제대로 실행 되지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="0b290-262">Pages with the *.cshtml* extension do not run correctly.</span></span> <span data-ttu-id="0b290-263">컴퓨터 루트에 있는 어셈블리를 등록 하는 ASP.NET 웹 페이지 *Web.config* 파일 및.NET Framework를 제거 합니다. 해당 파일을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-263">ASP.NET Web Pages registers an assembly in the machine root *Web.config* file, and removing the .NET Framework removes that file.</span></span> <span data-ttu-id="0b290-264">.NET Framework를 다시 설치 하면 구성 파일의 새 버전을 설치 하지만 ASP.NET 웹 페이지 어셈블리에 대 한 참조를 추가 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-264">Reinstalling the .NET Framework installs a new version of the configuration file, but does not add the reference for the ASP.NET Web Pages assembly.</span></span>
> 
> <span data-ttu-id="0b290-265">**해결 방법** .NET Framework를 다시 설치한 후 Razor 구문이 있는 ASP.NET 웹 페이지를 다시 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-265">**Workaround** After reinstalling the .NET Framework, reinstall ASP.NET Web Pages with Razor syntax.</span></span> <span data-ttu-id="0b290-266">다음 요소를 추가 합니다 *Web.config* 일반적으로 다음 위치에 있는 컴퓨터 루트에 있는 파일:</span><span class="sxs-lookup"><span data-stu-id="0b290-266">This adds the following element to the *Web.config* file in the machine root, which is typically in the following location:</span></span>  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> 
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](beta3/samples/sample6.xml)]


#### <a name="issue-applications-previously-deployed-with-aspnet-assemblies-in-the-bin-folder-experience-errors"></a><span data-ttu-id="0b290-267">문제: Bin 폴더에 ASP.NET 어셈블리를 사용 하 여 이전에 배포 된 응용 프로그램 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-267">Issue: Applications previously deployed with ASP.NET assemblies in the Bin folder experience errors</span></span>

> <span data-ttu-id="0b290-268">ASP.NET 웹 페이지 어셈블리의 복사본을 배포 하는 동안 (예를 들어 *Microsoft.WebPages.dll*)에 *Bin* 서버의 웹 사이트의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-268">During deployment, copies of the ASP.NET Web Pages assemblies (for example, *Microsoft.WebPages.dll*) to the *Bin* folder of the website on the server.</span></span> <span data-ttu-id="0b290-269">(이 때문일 수 있습니다 자동으로 배포 하는 동안 개발자는 어셈블리를 명시적으로 복사 되므로 또는.) 그러나 베타 3 릴리스를 설치할 때 오류 발생, 특정 형식을 찾을 수 있는 오류와 같은 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-269">(This might have happened automatically during deployment or because the developer explicitly copied the assemblies.) However, when the Beta 3 release is installed, errors occurs, such as errors that certain types cannot be found.</span></span> <span data-ttu-id="0b290-270">ASP.NET Web Pages 형식의 숫자로 Beta 3 릴리스에 대 한 다른 네임 스페이스로 이동 된이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-270">This occurs because a number of ASP.NET Web Pages types were moved into different namespaces for the Beta 3 release.</span></span>
> 
> <span data-ttu-id="0b290-271">**해결 방법** </span><span class="sxs-lookup"><span data-stu-id="0b290-271">**Workaround** </span></span>  
> <span data-ttu-id="0b290-272">선택을 취소는 *Bin* 배포 된 응용 프로그램의 새 어셈블리 폴더에 복사 (또는 응용 프로그램을 재배포) 한 다음 응용 프로그램 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-272">Clear the *Bin* folder of the deployed application, copy the new assemblies to the folder (or redeploy the application), and then restart the application.</span></span>


#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a><span data-ttu-id="0b290-273">문제: 확장명 없는 Url을 IIS 7 또는 IIS 7.5.cshtml/.vbhtml 파일 찾지 못한</span><span class="sxs-lookup"><span data-stu-id="0b290-273">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span></span>

> <span data-ttu-id="0b290-274">IIS 7 또는 IIS 7.5에서 다음과 같은 URL 사용 하 여 요청은 포함 된 페이지를 찾을 수 합니다 *.cshtml* 하거나 *.vbhtml* 확장:</span><span class="sxs-lookup"><span data-stu-id="0b290-274">On IIS 7 or IIS 7.5, requests with a URL like the following are not able to find pages that have the *.cshtml* or *.vbhtml* extension:</span></span>  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> <span data-ttu-id="0b290-275">URL 재작성 활성화 되어 있지 않으므로 기본적으로 IIS 7 또는 IIS 7.5 용 르면 문제가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-275">The issue arises because URL rewriting is not enabled by default for IIS 7 or IIS 7.5.</span></span> <span data-ttu-id="0b290-276">문제일 수 있습니다 시나리오에는 IIS Express를 사용 하 여 로컬로 테스트할 때 문제가 표시 되지 않으면 있지만 호스팅 웹 사이트에 웹 사이트를 배포할 때 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-276">The likeliest scenario is that you do not see the problem when testing locally using IIS Express, but you experience it when you deploy your website to a hosting website.</span></span>
> 
> <span data-ttu-id="0b290-277">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-277">**Workaround**</span></span>
> 
> - <span data-ttu-id="0b290-278">서버 컴퓨터에 대 한 제어를 사용 하는 경우 서버 컴퓨터의 설치에 설명 된 업데이트가 [는 업데이트를 사용할 수 있도록 특정 Url을 요청 하는 IIS 7.0 또는 IIS 7.5 처리기를 처리 하는 마침표로 끝나지 않는](https://support.microsoft.com/kb/980368)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-278">If you have control over the server computer, on the server computer install the update that is described in [A update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).</span></span>
> - <span data-ttu-id="0b290-279">서버 컴퓨터에 대 한 제어 없는 경우 (예를 들어, 배포 하는 호스팅 웹 사이트), 웹 사이트의 다음 추가할 *Web.config* 파일:</span><span class="sxs-lookup"><span data-stu-id="0b290-279">If you do not have control over the server computer (for example, you are deploying to a hosting website), add the following to the website's *Web.config* file:</span></span>
> 
> 
> [!code-xml[Main](beta3/samples/sample7.xml)]


#### <a name="issue-using-web-application-project-or-aspnet-mvc-and-aspnet-web-pages-in-the-same-application"></a><span data-ttu-id="0b290-280">문제: ASP.NET MVC 및 ASP.NET 웹 페이지 또는 웹 응용 프로그램 프로젝트를 사용 하 여 동일한 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="0b290-280">Issue: Using Web Application Project or ASP.NET MVC and ASP.NET Web pages in the same application</span></span>

> <span data-ttu-id="0b290-281">ASP.NET 웹 페이지에서 웹 응용 프로그램 프로젝트 또는 ASP.NET MVC 응용 프로그램을 사용할 때 오류가 표시 될 수 있습니다 하 *WebPageHttpApplication* 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-281">If you were using ASP.NET Web Pages in a Web Application project or ASP.NET MVC application, you might see an error that *WebPageHttpApplication* cannot be found.</span></span>
> 
> <span data-ttu-id="0b290-282">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-282">**Workaround**</span></span>  
> <span data-ttu-id="0b290-283">이 오류가 발생할 경우 응용 프로그램 파생 되는 기본 클래스를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-283">If you get this error, change the base class from which the application derives.</span></span> <span data-ttu-id="0b290-284">에 *Global.asax* 파일에서 다음 줄을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-284">In the *Global.asax* file, change the following line:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample8.cs)]
> 
> <span data-ttu-id="0b290-285">다음과 같이 변경</span><span class="sxs-lookup"><span data-stu-id="0b290-285">To this:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample9.cs)]
> 
> <span data-ttu-id="0b290-286">도입 된 변경 적용 반대로이 Razor 구문이 있는 ASP.NET 웹 페이지의 베타 1 릴리스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-286">This in effect reverses a change that was introduced for the Beta 1 release of ASP.NET Web Pages with Razor syntax.</span></span>


#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a><span data-ttu-id="0b290-287">문제: SQL Server Compact 설치 되지 않은 컴퓨터에 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="0b290-287">Issue: Deploying an application to a computer that does not have SQL Server Compact installed</span></span>

> <span data-ttu-id="0b290-288">SQL Server Compact 데이터베이스를 포함 하는 응용 프로그램 SQL Server Compact는 설치 되지 않은 컴퓨터에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-288">Applications that include SQL Server Compact databases can run on a computer where SQL Server Compact is not installed.</span></span> <span data-ttu-id="0b290-289">Microsoft WebMatrix Beta 3에서 자동으로 이러한 이진 파일을 복사 하 고 적절 한 수행 *Web.config* 파일 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-289">Microsoft WebMatrix Beta 3 automatically copies these binaries for you and performs the appropriate *Web.config* file transforms.</span></span>
> 
> <span data-ttu-id="0b290-290">**해결 방법** 이러한 파일을 복사 하 고 확인 해야 할 경우 합니다 *Web.config* 파일 변경 내용을 수동으로 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-290">**Workaround** If you need to copy these files and make the *Web.config* file changes manually, do the following :</span></span>
> 
> 1. <span data-ttu-id="0b290-291">데이터베이스 엔진 어셈블리를 복사 합니다 *Bin* 대상 컴퓨터에서 응용 프로그램의 폴더 (및 하위 폴더).</span><span class="sxs-lookup"><span data-stu-id="0b290-291">Copy the database engine assemblies to the *Bin* folder (and subfolders) of the application on the target computer:</span></span> 
> 
>     - <span data-ttu-id="0b290-292">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **to** *\Bin*</span><span class="sxs-lookup"><span data-stu-id="0b290-292">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **to** *\Bin*</span></span>
>     - <span data-ttu-id="0b290-293">복사본 *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\*\* **하** *\Bin\x86*</span><span class="sxs-lookup"><span data-stu-id="0b290-293">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\*\* **to** *\Bin\x86*</span></span>
>     - <span data-ttu-id="0b290-294">복사본 *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **하** *\Bin\amd64*</span><span class="sxs-lookup"><span data-stu-id="0b290-294">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **to** *\Bin\amd64*</span></span>
> 2. <span data-ttu-id="0b290-295">웹 사이트의 루트 폴더를 만들거나 엽니다는 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-295">In the root folder of the website, create or open a *Web.config* file.</span></span> <span data-ttu-id="0b290-296">(WebMatrix 베타 3을이 파일 형식은 클릭할 경우 사용할 수 있습니다 **모든** 에 **파일 형식을 선택** 대화 상자.)</span><span class="sxs-lookup"><span data-stu-id="0b290-296">(In WebMatrix Beta 3, this file type is available if you click **All** in the **Choose a File Type** dialog box.)</span></span>
> 3. <span data-ttu-id="0b290-297">다음 요소 자식으로 추가 합니다 **&lt;구성&gt;** 요소 (에 포함 되지 않은 합니다 **&lt;system.web&gt;** 요소):</span><span class="sxs-lookup"><span data-stu-id="0b290-297">Add the following element as a child of the **&lt;configuration&gt;** element (not inside the **&lt;system.web&gt;** element):</span></span>
> 
> 
> [!code-xml[Main](beta3/samples/sample10.xml)]


#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a><span data-ttu-id="0b290-298">문제: 데이터베이스 및 WebGrid 도우미 Visual Basic에서 보통 신뢰에서 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-298">Issue: Database and WebGrid helpers do not work in Medium Trust in Visual Basic</span></span>

> <span data-ttu-id="0b290-299">Visual Basic을 사용 하는 경우 (만드는 *.vbhtml* 파일), `Database` 고 `WebGrid` 도우미 응용 프로그램은 보통 신뢰를 사용 하도록 설정 된 경우 작동 하지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-299">If you are using Visual Basic (creating *.vbhtml* files), the `Database` and `WebGrid` helpers will not work if the application is set to use Medium Trust.</span></span>
> 
> <span data-ttu-id="0b290-300">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-300">**Workaround**</span></span>  
> <span data-ttu-id="0b290-301">완전 신뢰를 사용 하 여 응용 프로그램을 일시적으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-301">Temporarily set the application to use Full Trust.</span></span>

<a id="Known_Issues_SQL_Server_Compact"></a>
### <a name="sql-server-compact"></a><span data-ttu-id="0b290-302">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="0b290-302">SQL Server Compact</span></span>

#### <a name="issue-encrypt-property-is-not-recognized"></a><span data-ttu-id="0b290-303">문제: "Encrypt" 속성이 인식 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-303">Issue: "Encrypt" property is not recognized</span></span>

> <span data-ttu-id="0b290-304">SQL Server Compact 4.0 인식 하지 못합니다 합니다 `Encrypt` 의 속성을 `SqlCeConnection` 클래스.</span><span class="sxs-lookup"><span data-stu-id="0b290-304">SQL Server Compact 4.0 does not recognize the `Encrypt` property of the `SqlCeConnection` class.</span></span> <span data-ttu-id="0b290-305">데이터베이스 파일을 암호화 하려면이 속성을 사용 하지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-305">You should not use this property to encrypt database files.</span></span> <span data-ttu-id="0b290-306">`Encrypt` 속성 된 SQL Server Compact 3.5 릴리스에서 사용 되지 않으며 이전 버전과 호환성을 위해서만 유지 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-306">The `Encrypt` property was deprecated in SQL Server Compact 3.5 release and was retained only for backward compatibility.</span></span> 
> 
> <span data-ttu-id="0b290-307">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-307">**Workaround**</span></span>  
> <span data-ttu-id="0b290-308">사용 하 여 합니다 `Encryption Mode` 의 속성을 `SqlCeConnection` SQL Server Compact 4.0 데이터베이스 파일을 암호화 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-308">Use the `Encryption Mode` property of the `SqlCeConnection` class to encrypt SQL Server Compact 4.0 database files.</span></span> <span data-ttu-id="0b290-309">다음 예제에 사용 하 여 암호화 된 SQL Server Compact 4.0 데이터베이스를 만드는 방법을 보여 줍니다는 `Encryption Mode` 속성:</span><span class="sxs-lookup"><span data-stu-id="0b290-309">The following example shows how to create an encrypted SQL Server Compact 4.0 database using the `Encryption Mode` property:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample11.cs)]
> 
> [!code-vb[Main](beta3/samples/sample12.vb)]
> 
> <span data-ttu-id="0b290-310">기존 SQL Server Compact 4.0 데이터베이스의 암호화 모드를 변경 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-310">To change the encryption mode of an existing SQL Server Compact 4.0 database, do the following:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample13.cs)]
> 
> [!code-vb[Main](beta3/samples/sample14.vb)]
> 
> <span data-ttu-id="0b290-311">암호화 되지 않은 SQL Server Compact 4.0 데이터베이스를 암호화 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-311">To encrypt an unencrypted SQL Server Compact 4.0 database, do the following:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample15.cs)]
> 
> [!code-vb[Main](beta3/samples/sample16.vb)]


#### <a name="issue-microsoft-visual-c-2008-runtime-libraries-are-required"></a><span data-ttu-id="0b290-312">문제: Microsoft Visual c + + 2008 런타임 라이브러리는 필요</span><span class="sxs-lookup"><span data-stu-id="0b290-312">Issue: Microsoft Visual C++ 2008 runtime libraries are required</span></span>

> <span data-ttu-id="0b290-313">네이티브 Dll의 SQL Server Compact 4.0에는 Microsoft Visual c + + 2008 런타임 라이브러리 ((x86, IA64 및 x64), 서비스 팩 1에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-313">The native DLLs of SQL Server Compact 4.0 need the Microsoft Visual C++ 2008 Runtime Libraries (x86, IA64, and x64), Service Pack 1.</span></span>
> 
> <span data-ttu-id="0b290-314">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-314">**Workaround**</span></span>  
> <span data-ttu-id="0b290-315">.NET Framework 3.5 SP1을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-315">Install the .NET Framework 3.5 SP1.</span></span> <span data-ttu-id="0b290-316">Visual c + + 2008 런타임 라이브러리 SP1도 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-316">This also installs the Visual C++ 2008 Runtime Libraries SP1.</span></span> <span data-ttu-id="0b290-317">다음 위치에서 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-317">You can download the libraries from the following location:</span></span>   
>   
> [<span data-ttu-id="0b290-318">Microsoft Visual c + + 2008 서비스 팩 1 재배포 가능 패키지 ATL 보안 업데이트</span><span class="sxs-lookup"><span data-stu-id="0b290-318">Microsoft Visual C++ 2008 Service Pack 1 Redistributable Package ATL Security Update</span></span>](https://go.microsoft.com/fwlink/?LinkId=194827)
> 
> [!NOTE]
> <span data-ttu-id="0b290-319">.NET Framework 2.0, 3.0, 설치 또는 4 *되지* Visual c + + 2008 런타임 라이브러리에 SP1을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-319">Note that installing the .NET Framework 2.0, 3.0, or 4 does *not* install the Visual C++ 2008 Runtime Libraries SP1.</span></span>


#### <a name="issue-if-sql-server-compact-is-installed-prior-to-installing-net-framework-on-the-computer-its-provider-invariant-name-is-not-registered-in-the-net-framework-machineconfig-file"></a><span data-ttu-id="0b290-320">문제: 컴퓨터의.NET Framework를 설치 하기 전에 SQL Server Compact를 설치 하는 경우 해당 공급자 고정 이름에에서 등록 되지 않은.NET Framework machine.config 파일</span><span class="sxs-lookup"><span data-stu-id="0b290-320">Issue: If SQL Server Compact is installed prior to installing .NET Framework on the computer, its provider invariant name is not registered in the .NET Framework machine.config file</span></span>

> <span data-ttu-id="0b290-321">SQL Server Compact.NET Framework가 SQL Server Compact는.NET framework가 필요 하기 때문에 설치 되지 않은 컴퓨터에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-321">SQL Server Compact can be installed on a machine that does not have .NET Framework installed because SQL Server Compact does require the .NET framework.</span></span> <span data-ttu-id="0b290-322">SQL Server Compact를 설치 하기 전에.NET Framework 버전 3.5 또는 4를 모두 설치 되어 있으면 SQL Server Compact 설치에서 공급자 고정 이름을 등록 하지 않습니다 합니다 *machine.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-322">If neither .NET Framework version 3.5 nor 4 is installed before you install SQL Server Compact, the SQL Server Compact Setup does not register its provider invariant name in the *machine.config* file.</span></span> <span data-ttu-id="0b290-323">SQL Server Compact 항목을 사용 하는 모든 응용 프로그램을 *machine.config* 파일 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-323">Any application that relies on the SQL Server Compact entry in the *machine.config* file will fail.</span></span> <span data-ttu-id="0b290-324">고정 이름이 등록 항목 *machine.config* 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-324">The invariant name registration entry in *machine.config* looks like the following example:</span></span>
> 
> [!code-xml[Main](beta3/samples/sample17.xml)]
> 
> <span data-ttu-id="0b290-325">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-325">**Workaround**</span></span>  
> <span data-ttu-id="0b290-326">SQL Server Compact 4.0 CTP1을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-326">Uninstall SQL Server Compact 4.0 CTP1.</span></span> <span data-ttu-id="0b290-327">다운로드 하 고 다음 위치에서.NET Framework의 전체 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-327">Download and install the full versions of the .NET Framework from the following location:</span></span>
> 
> [<span data-ttu-id="0b290-328">Microsoft.NET Framework 3.5 서비스 팩 1 (전체 패키지)</span><span class="sxs-lookup"><span data-stu-id="0b290-328">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
> [<span data-ttu-id="0b290-329">Microsoft.NET Framework 4.0 릴리스 (전체 패키지)</span><span class="sxs-lookup"><span data-stu-id="0b290-329">Microsoft .NET Framework 4.0 Release (Full Package)</span></span>](https://www.microsoft.com/downloads/details.aspx?FamilyID=9cfb2d51-5ff4-4491-b0e5-b386f32c0992&amp;displaylang=en)
> 
> <span data-ttu-id="0b290-330">제거한 [SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-330">Then reinstall [SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en).</span></span>


<a id="Known_Issues_Installing_Applications"></a>

### <a name="installing-applications"></a><span data-ttu-id="0b290-331">응용 프로그램 설치</span><span class="sxs-lookup"><span data-stu-id="0b290-331">Installing Applications</span></span>

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a><span data-ttu-id="0b290-332">문제: 응용 프로그램을 설치할 수 시간이 오래 걸릴 경우 사용자의 내 문서 폴더는 네트워크 공유로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-332">Issue: Installing an application can take a long time if the user's My Documents folder is redirected to a network share</span></span>

> <span data-ttu-id="0b290-333">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-333">**Workaround**</span></span>  
> <span data-ttu-id="0b290-334">없음</span><span class="sxs-lookup"><span data-stu-id="0b290-334">None.</span></span> <span data-ttu-id="0b290-335">응용 프로그램을 설치 하는 데 소요 되지만 제대로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-335">The application might take a while to install, but will install correctly.</span></span>


<a id="Known_Issues_Publishing_Applications"></a>

### <a name="publishing-applications"></a><span data-ttu-id="0b290-336">응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="0b290-336">Publishing Applications</span></span>

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a><span data-ttu-id="0b290-337">문제: 사이트 "대상 URL" 필드는 http:// 또는 https:// 로 시작 하지 않는 경우 게시 한 후 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-337">Issue: Site might not work after publishing if the "Destination URL" field is not prefixed with http:// or https://</span></span>

> <span data-ttu-id="0b290-338">에 **게시 설정** 대화 상자에서 대상 URL로 시작 하지 않는 경우 `http://` 또는 `https://`, 사이트 배포 후 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-338">In the **Publishing Settings** dialog box, if the destination URL does not begin with `http://` or `https://`, the site might not work after deployment.</span></span>
> 
> <span data-ttu-id="0b290-339">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-339">**Workaround**</span></span>  
> <span data-ttu-id="0b290-340">있는지 확인 하는 사이트에서 대상 URL을 게시 하기 전에 합니다 **게시 설정** 대화 상자 시작 `http://` 또는 `https://`합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-340">Make sure that before you publish a site, the destination URL in the **Publish Settings** dialog box starts with `http://` or `https://`.</span></span>


#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a><span data-ttu-id="0b290-341">문제: MySQL 데이터베이스를 게시할 오류로 인해 실패 "데이터베이스를 게시 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-341">Issue: Publishing a MySQL database fails with the error "Failed to publish the database.</span></span> <span data-ttu-id="0b290-342">이 경우 발생할 수 있습니다 원격 데이터베이스에서 스크립트를 실행할 수 없습니다. "</span><span class="sxs-lookup"><span data-stu-id="0b290-342">This can happen if the remote database cannot run the script."</span></span>

> <span data-ttu-id="0b290-343">이 오류는 다양 한 이유로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-343">The error can occur for a number of reasons.</span></span> <span data-ttu-id="0b290-344">이 오류를 확인할 수 있습니다 하는 이유 중 하나 이며 경우 데이터베이스 스크립트 문자가 작은따옴표 (') u t F-8로 대상 MySQL 데이터베이스의 기본 문자 집합이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-344">One reason you can see this error is if the database script contains a single quotation character (') and the destination MySQL database's default character set is not to UTF-8.</span></span>
> 
> <span data-ttu-id="0b290-345">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-345">**Workaround**</span></span>  
> <span data-ttu-id="0b290-346">U t F-8로 원격 MySQL 데이터베이스에 대 한 기본 문자를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-346">Set the default character set for the remote MySQL database to UTF-8.</span></span>


<a id="Known_Issues_Other_Issues"></a>

### <a name="other-issues"></a><span data-ttu-id="0b290-347">기타 문제</span><span class="sxs-lookup"><span data-stu-id="0b290-347">Other Issues</span></span>

#### <a name="issue-searchfilter-does-not-work-in-reports-for-group-by-issue-type"></a><span data-ttu-id="0b290-348">문제: 검색/필터에 작동 하지 않습니다 보고서의 Group By: 문제 유형</span><span class="sxs-lookup"><span data-stu-id="0b290-348">Issue: Search/Filter does not work in Reports for Group By: Issue Type</span></span>

> <span data-ttu-id="0b290-349">텍스트를 입력 하는 경우 사이트에 대 한 보고서를 실행할 때 합니다 *URL 필터링* 상자 하 고 클릭 *검색*, 아무 일도 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-349">When you run a report for a site, if you enter text in the *Filter by URL* box and click *Search*, nothing happens.</span></span> <span data-ttu-id="0b290-350">이 제어 하는 동안 작동 하지 않습니다. 왜냐하면 합니다 *Group By* 보고서의 상태가로 설정 된 *문제 유형*, 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-350">This is because this control is not functional while the *Group By* state of the report is set to *Issue Type*, which is the default.</span></span>
> 
> <span data-ttu-id="0b290-351">**해결 방법** 에 *Group By* 탭 리본 메뉴를 클릭 *URL* 해당 소스 URL에서 항목을 그룹화 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-351">**Workaround** In the *Group By* tab of ribbon, click *URL* to group the entries by their source URL.</span></span> <span data-ttu-id="0b290-352">단추 항목을 필터링 하 고 텍스트 상자는이 상태에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-352">The text box and button to filter the entries are functional while in this state.</span></span>


#### <a name="issue-wcf-applications-fail-to-run-with-iis-express"></a><span data-ttu-id="0b290-353">문제: WCF 응용 프로그램이 실행 되지 IIS express</span><span class="sxs-lookup"><span data-stu-id="0b290-353">Issue: WCF applications fail to run with IIS Express</span></span>

> <span data-ttu-id="0b290-354">WCF 응용 프로그램으로 이동 다음과 같은 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-354">Browsing to a WCF application results in an error like the following one:</span></span>
> 
> <span data-ttu-id="0b290-355">*파일 또는 어셈블리를 로드할 수 없습니다 ' Microsoft.Web.Administration, 버전 7.0.0.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35 =' 또는 해당 종속성 중 하나입니다. 지정한 파일을 찾을 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="0b290-355">*Could not load file or assembly 'Microsoft.Web.Administration, Version=7.0.0.0, Culture=neutral,PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.*</span></span>
> 
> <span data-ttu-id="0b290-356">IIS Express 베타 릴리스 기본적으로 WCF를 지원 하지 않으므로이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-356">This occurs because IIS Express Beta release doesn't support WCF by default.</span></span>
> 
> <span data-ttu-id="0b290-357">**해결 방법** 다음 해결 방법 중 하나를 사용 하 여 (해결 방법 2 필요한 Microsoft Windows Vista 이상):</span><span class="sxs-lookup"><span data-stu-id="0b290-357">**Workaround** Use any one of the following workarounds (workaround #2 requires Microsoft Windows Vista or higher):</span></span>
> 
> 
> 1. <span data-ttu-id="0b290-358">복사 합니다 *Microsoft.Web.dll* 하 고 *Microsoft.Web.Administration.dll* WebMatrix 설치 위치에서 어셈블리를 *bin* wcf 디렉터리 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-358">Copy the *Microsoft.Web.dll* and *Microsoft.Web.Administration.dll* assemblies from the WebMatrix installation location to the *bin* directory of the WCF application.</span></span> <span data-ttu-id="0b290-359">기본적으로 WebMatrix에서 설치 합니다 *Microsoft WebMatrix* 시스템의 하위 폴더 *Program Files* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-359">By default, WebMatrix is installed in the *Microsoft WebMatrix* subfolder under the system's *Program Files* folder.</span></span>
> 2. <span data-ttu-id="0b290-360">Microsoft Windows Vista 이상에서의 어셈블리에 symlink를 만듭니다는 *bin* 디렉터리에서 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-360">On Microsoft Windows Vista or higher, create a symlink to the assemblies in the *bin* directory using the following commands.</span></span> <span data-ttu-id="0b290-361">(이 방법은 이점이 어셈블리의 복사본이 만들어지지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="0b290-361">(This approach has the advantage that it does not create a copy of the assemblies.)</span></span>
> 
>     [!code-console[Main](beta3/samples/sample18.cmd)]
> 3. <span data-ttu-id="0b290-362">두 어셈블리를 GAC에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-362">Install the two assemblies in the GAC.</span></span> <span data-ttu-id="0b290-363">상승된 된 프롬프트에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-363">From an elevated prompt, run the following commands:</span></span>
> 
>     [!code-console[Main](beta3/samples/sample19.cmd)]


#### <a name="issue-webmatrix-beta-3-is-unable-to-perform-certain-tasks-that-require-elevation"></a><span data-ttu-id="0b290-364">문제: WebMatrix 베타 3 상승이 필요한 특정 작업을 수행할 수 없는</span><span class="sxs-lookup"><span data-stu-id="0b290-364">Issue: WebMatrix Beta 3 is unable to perform certain tasks that require elevation</span></span>

> <span data-ttu-id="0b290-365">WebMatrix 베타 3가 다음과 같은 상황에서 추가 구성 요소를 설치 하는 등의 권한 상승 해야 하는 특정 작업을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-365">WebMatrix Beta 3 is unable to perform certain tasks that require elevation, such as installing additional components in the following situations:</span></span>
> 
> - <span data-ttu-id="0b290-366">Windows Vista 또는 Windows 7에서 관리자 권한이 없는 계정으로 로그온 한 사용자 계정 컨트롤 (UAC)을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-366">On Windows Vista or Windows 7, you are logged in with an account that does not have administrative privileges and User Account Control (UAC) is disabled.</span></span>
> - <span data-ttu-id="0b290-367">Microsoft Windows XP 또는 Microsoft Windows Server 2003을 사용 하는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-367">You are using Microsoft Windows XP or Microsoft Windows Server 2003.</span></span>
> 
> <span data-ttu-id="0b290-368">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-368">**Workaround**</span></span>  
> <span data-ttu-id="0b290-369">WebMatrix Beta 3에서 대부분의 작업에는 관리 권한이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-369">Most tasks in WebMatrix Beta 3 do not require administrative permission.</span></span> <span data-ttu-id="0b290-370">이러한 조작자에 대 한 다음이 단계를 수행 또는 관리자로 서 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-370">For those that do, you can perform the operation as an administrator, or follow these steps:</span></span>
> 
> - <span data-ttu-id="0b290-371">Windows Vista 또는 Windows 7에서 UAC를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-371">On Windows Vista or Windows 7, enable UAC.</span></span>
> - <span data-ttu-id="0b290-372">Windows XP에서 Administrators 보안 그룹에 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-372">On Windows XP, add the user to the Administrators security group.</span></span>


#### <a name="issue-site-from-web-gallery-is-disabled"></a><span data-ttu-id="0b290-373">문제: "웹 갤러리에서 사이트"을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-373">Issue: "Site from Web Gallery" is disabled</span></span>

> <span data-ttu-id="0b290-374">합니다 **웹 갤러리에서 사이트** 웹 플랫폼 설치 관리자 3.0이 설치 되지 않은 경우 옵션은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-374">The **Site from Web Gallery** option is disabled if the Web Platform Installer 3.0 is not installed.</span></span>
> 
> <span data-ttu-id="0b290-375">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-375">**Workaround**</span></span>  
> <span data-ttu-id="0b290-376">설치 합니다 [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-376">Install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span>


#### <a name="issue-on-windows-server-2003-iis-express-does-not-start-for-a-non-administrative-user"></a><span data-ttu-id="0b290-377">문제: Windows Server 2003에서 IIS Express 시작 되지 않으면 관리자가 아닌 사용자에 대 한</span><span class="sxs-lookup"><span data-stu-id="0b290-377">Issue: On Windows Server 2003, IIS Express does not start for a non-administrative user</span></span>

> <span data-ttu-id="0b290-378">Windows Server 2003에서 페이지를 시작 하거나 IIS Express를 시작 하는 경우 IIS Express 시작 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-378">On Windows Server 2003, when you launch a page or start IIS Express, IIS Express does not start.</span></span> <span data-ttu-id="0b290-379">웹 페이지 응용 프로그램 관리자가 아닌 사용자가 시작한 있는지 여부를 나타내는 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-379">For Web pages, an error is displayed that indicates that the application has been started by a non-administrative user.</span></span>
> 
> <span data-ttu-id="0b290-380">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-380">**Workaround**</span></span>  
> <span data-ttu-id="0b290-381">관리자 권한으로 WebMatrix 베타 3을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-381">Start WebMatrix Beta 3 as an administrative user.</span></span> <span data-ttu-id="0b290-382">자세한 내용은 다음 기술 자료 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0b290-382">For more details, see the following KnowledgeBase article:</span></span>  
>   
> [<span data-ttu-id="0b290-383">관리자가 아닌 사용자가 시작 되는 응용 프로그램은 응용 프로그램이 Windows Vista, Windows Server 2003 또는 Windows XP에서 실행 되는 컴퓨터의 HTTP 트래픽을 수신할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-383">An application that is started by a non-administrative user cannot listen to the HTTP traffic of the computer on which the application is running in Windows Vista, Windows Server 2003, or Windows XP.</span></span>](https://support.microsoft.com/kb/939786)


#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a><span data-ttu-id="0b290-384">문제: Google Chrome 실행 옵션으로 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-384">Issue: Google Chrome is not available as a Run option</span></span>

> <span data-ttu-id="0b290-385">Google Chrome 브라우저에서 목록에 표시 되지 않습니다 **실행할** 에 **홈** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-385">Google Chrome is not displayed in the list of browsers under **Run** on the **Home** tab.</span></span>
> 
> <span data-ttu-id="0b290-386">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-386">**Workaround**</span></span>  
> <span data-ttu-id="0b290-387">Google Chrome의 일부 버전에서는 등록 하지 자체 올바르게 Windows의 기본 프로그램 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-387">Some versions of Google Chrome do not register themselves correctly with the Default Programs feature in Windows.</span></span> <span data-ttu-id="0b290-388">대 안으로, Google Chrome을 시작 합니다 *사용자 지정 및 Google Chrome 컨트롤* 메뉴에서 클릭 *옵션*를 클릭 하 고 *확인 Google Chrome 기본 브라우저*.</span><span class="sxs-lookup"><span data-stu-id="0b290-388">As a workaround, start Google Chrome, click the *Customize and control Google Chrome* menu, click *Options*, and then click *Make Google Chrome my default browser*.</span></span>


#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a><span data-ttu-id="0b290-389">문제: "외래 키" 대화 상자를 허용 하지 않습니다는 기본 키를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-389">Issue: The "Foreign Key" dialog box doesn't allow entering a primary key</span></span>

> <span data-ttu-id="0b290-390">합니다 **외래 키** 대화 상자 기본 키 테이블에서 기본 키 이름을 입력할 수를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-390">The **Foreign Key** dialog box does not allow you to enter the primary key name from the primary key table.</span></span>
> 
> <span data-ttu-id="0b290-391">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-391">**Workaround**</span></span>  
> <span data-ttu-id="0b290-392">이 의도적입니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-392">This is intentional.</span></span> <span data-ttu-id="0b290-393">기본 키 테이블에서 기본 키의 이름을 입력할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-393">You do not need to enter the name of the primary key from the primary key table.</span></span>


#### <a name="issue-the-relationships-button-is-disabled"></a><span data-ttu-id="0b290-394">문제: "관계" 단추는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-394">Issue: The "Relationships" button is disabled</span></span>

> <span data-ttu-id="0b290-395">**관계** 단추를 **테이블** 탭에 **데이터베이스** SQL Server Compact 데이터베이스에 대 한 작업 영역을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-395">The **Relationships** button under the **Table** tab in the **Databases** workspace is disabled for SQL Server Compact databases.</span></span>
> 
> <span data-ttu-id="0b290-396">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-396">**Workaround**</span></span>  
> <span data-ttu-id="0b290-397">없음</span><span class="sxs-lookup"><span data-stu-id="0b290-397">None.</span></span> <span data-ttu-id="0b290-398">SQL Server Compact 테이블 간의 관계를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-398">SQL Server Compact does not support relationships between tables.</span></span>


#### <a name="issue-parameterized-sql-queries-throw-exceptions"></a><span data-ttu-id="0b290-399">문제: 매개 변수가 있는 SQL 쿼리 예외 throw</span><span class="sxs-lookup"><span data-stu-id="0b290-399">Issue: Parameterized SQL queries throw exceptions</span></span>

> <span data-ttu-id="0b290-400">SQL Server Compact 4.0에서는 데이터 형식 같은 지정 하지 않으면 `SqlDbType` 또는 `DbType` 매개 변수가 있는 쿼리에서 매개 변수의 경우 쿼리를 실행할 때 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-400">In SQL Server Compact 4.0, if you do not specify a data type such as `SqlDbType` or `DbType` for parameters in parameterized queries, an exception is thrown when the query runs.</span></span>
> 
> <span data-ttu-id="0b290-401">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="0b290-401">**Workaround**</span></span>  
> <span data-ttu-id="0b290-402">와 같은 매개 변수의 데이터 형식을 명시적으로 설정할 `SqlDbType` 또는 `DbType`합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-402">Explicitly set the data type for parameters such as `SqlDbType` or `DbType`.</span></span> <span data-ttu-id="0b290-403">이 BLOB 데이터 형식의 경우 중요 (`image` 고 `ntext`).</span><span class="sxs-lookup"><span data-stu-id="0b290-403">This is critical in the case of BLOB data types (`image` and `ntext`).</span></span> <span data-ttu-id="0b290-404">다음과 같은 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-404">Use code like the following:</span></span>
> 
> [!code-sql[Main](beta3/samples/sample20.sql)]
> 
> [!code-vb[Main](beta3/samples/sample21.vb)]


<a id="More_Info"></a>

## <a name="for-more-information"></a><span data-ttu-id="0b290-405">자세한 내용</span><span class="sxs-lookup"><span data-stu-id="0b290-405">For More Information</span></span>

<span data-ttu-id="0b290-406">WebMatrix 베타 3에 대 한 자세한 내용은 다음 웹 사이트를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0b290-406">For more information about WebMatrix Beta 3, see the following websites:</span></span>

- [<span data-ttu-id="0b290-407">IIS.net</span><span class="sxs-lookup"><span data-stu-id="0b290-407">IIS.net</span></span>](http://iis.net/)
- [<span data-ttu-id="0b290-408">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0b290-408">ASP.NET</span></span>](https://asp.net/webmatrix)
- [<span data-ttu-id="0b290-409">Microsoft.com/web</span><span class="sxs-lookup"><span data-stu-id="0b290-409">Microsoft.com/web</span></span>](https://www.microsoft.com/web)

* * *

<span data-ttu-id="0b290-410">© 2010 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="0b290-410">© 2010 Microsoft Corporation.</span></span> <span data-ttu-id="0b290-411">All Rights Reserved.</span><span class="sxs-lookup"><span data-stu-id="0b290-411">All Rights Reserved.</span></span> <span data-ttu-id="0b290-412">[사용 약관](https://msdn.microsoft.cos/cc300389.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b290-412">[Terms of Use](https://msdn.microsoft.cos/cc300389.aspx).</span></span>
