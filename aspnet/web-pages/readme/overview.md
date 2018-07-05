---
uid: web-pages/readme/overview
title: WebMatrix 추가 정보 | Microsoft Docs
author: rick-anderson
description: WebMatrix 및 ASP.NET 웹 페이지 (Razor) 1.0 릴리스 정보
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/06/2011
ms.topic: article
ms.assetid: 36c5beeb-45a7-48a0-9c30-f82cdf5c5f5f
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/readme
msc.type: content
ms.openlocfilehash: 924bf04772a1d73c7fdfb1168090daef388438ab
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37398802"
---
<a name="webmatrix-readme"></a><span data-ttu-id="9d502-103">WebMatrix 추가 정보</span><span class="sxs-lookup"><span data-stu-id="9d502-103">WebMatrix Readme</span></span>
====================
<span data-ttu-id="9d502-104">2011 년 1 월 13</span><span class="sxs-lookup"><span data-stu-id="9d502-104">13 January 2011</span></span>

## <a name="contents"></a><span data-ttu-id="9d502-105">목차</span><span class="sxs-lookup"><span data-stu-id="9d502-105">Contents</span></span>

> [!NOTE]
> <span data-ttu-id="9d502-106">이 추가 정보는 WebMatrix의 1.0 릴리스에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-106">This readme applies to the 1.0 release of WebMatrix.</span></span>


- [<span data-ttu-id="9d502-107">개요</span><span class="sxs-lookup"><span data-stu-id="9d502-107">Overview</span></span>](#Overview)
- [<span data-ttu-id="9d502-108">설치</span><span class="sxs-lookup"><span data-stu-id="9d502-108">Installation</span></span>](#Installation_Notes)
- [<span data-ttu-id="9d502-109">응용 프로그램을 게시 하는 방법</span><span class="sxs-lookup"><span data-stu-id="9d502-109">How to Publish Applications</span></span>](#InstructionsForPublishingApplications)
- [<span data-ttu-id="9d502-110">변경 내용 및 문제</span><span class="sxs-lookup"><span data-stu-id="9d502-110">Changes and Issues</span></span>](#ChangesAndIssues)

    - [<span data-ttu-id="9d502-111">WebMatrix 1.0 설치</span><span class="sxs-lookup"><span data-stu-id="9d502-111">WebMatrix 1.0 Installation</span></span>](#Known_Issues_Installation)
    - [<span data-ttu-id="9d502-112">ASP.NET 웹 페이지 2</span><span class="sxs-lookup"><span data-stu-id="9d502-112">ASP.NET Web Pages</span></span>](#Known_Issues_ASPNET)
    - [<span data-ttu-id="9d502-113">WebMatrix</span><span class="sxs-lookup"><span data-stu-id="9d502-113">WebMatrix</span></span>](#Known_Issues_WebMatrix)
    - [<span data-ttu-id="9d502-114">IIS Express</span><span class="sxs-lookup"><span data-stu-id="9d502-114">IIS Express</span></span>](#Known_Issues_IISExpress)
    - [<span data-ttu-id="9d502-115">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="9d502-115">SQL Server Compact</span></span>](#Known_Issues_SQLServerCompact)
    - [<span data-ttu-id="9d502-116">응용 프로그램 설치</span><span class="sxs-lookup"><span data-stu-id="9d502-116">Installing Applications</span></span>](#Known_Issues_Installing_Applications)
    - [<span data-ttu-id="9d502-117">응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="9d502-117">Publishing Applications</span></span>](#Known_Issues_Publishing_Applications)
- [<span data-ttu-id="9d502-118">자세한 내용은</span><span class="sxs-lookup"><span data-stu-id="9d502-118">For More Information</span></span>](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a><span data-ttu-id="9d502-119">개요</span><span class="sxs-lookup"><span data-stu-id="9d502-119">Overview</span></span>

> <span data-ttu-id="9d502-120">Microsoft WebMatrix 1.0은 몇 분 안에 설치 하는 무료 웹 개발 스택입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-120">Microsoft WebMatrix 1.0 is a free web development stack that installs in minutes.</span></span> <span data-ttu-id="9d502-121">데이터베이스 및 프로그래밍 프레임 워크를 단일 통합된 환경 만들기를 사용 하 여 웹 서버를 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-121">It integrates a web server with database and programming frameworks to create a single, integrated experience.</span></span> <span data-ttu-id="9d502-122">WebMatrix를 사용 하 여 코드, 테스트 및 고유한 ASP.NET 또는 PHP 웹 사이트를 게시 하는 방법을 간소화할 수 있습니다 또는 WebMatrix를 사용 하 여 DotNetNuke, Umbraco, WordPress 또는 Joomla와 같은 인기 있는 오픈 소스 앱을 사용 하 여 새 웹 사이트를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-122">You can use WebMatrix to streamline the way you code, test, and publish your own ASP.NET or PHP website, or you can use WebMatrix to start a new website using popular open-source apps like DotNetNuke, Umbraco, WordPress, or Joomla.</span></span> <span data-ttu-id="9d502-123">WebMatrix에는 동일한 강력한 웹 서버, 데이터베이스 엔진 및 프레임 워크 환경을 원활 하 게 개발에서 프로덕션으로 전환 하면 인터넷에서 웹 사이트를 실행 되는 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-123">WebMatrix uses the same powerful web server, database engine, and frameworks environment that will run your website on the internet, which makes the transition from development to production smooth and seamless.</span></span>


<a id="Installation_Notes"></a>

## <a name="installation"></a><span data-ttu-id="9d502-124">설치</span><span class="sxs-lookup"><span data-stu-id="9d502-124">Installation</span></span>

> <span data-ttu-id="9d502-125">WebMatrix 1.0을 설치 하려면 먼저 설치 해야 합니다 [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-125">To install WebMatrix 1.0, you must first install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span> <span data-ttu-id="9d502-126">웹 플랫폼 설치 관리자를 설치한 후에 WebMatrix 설치에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-126">After you've installed the Web Platform Installer, you can use it to install WebMatrix.</span></span>
> 
> <span data-ttu-id="9d502-127">설치 중에 문제가 있는 경우 가리킵니다 [Microsoft 웹 플랫폼 설치 관리자를 사용 하 여 문제 해결](https://go.microsoft.com/fwlink/?LinkId=196212)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-127">If you have problems during installation, refer to [Troubleshooting Problems with Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).</span></span>


<a id="InstructionsForPublishingApplications"></a>
## <a name="how-to-publish-applications"></a><span data-ttu-id="9d502-128">응용 프로그램을 게시 하는 방법</span><span class="sxs-lookup"><span data-stu-id="9d502-128">How to Publish Applications</span></span>

> <span data-ttu-id="9d502-129">참조 [응용 프로그램을 게시 하기 위한 단계별 지침](https://go.microsoft.com/fwlink/?LinkID=196149)</span><span class="sxs-lookup"><span data-stu-id="9d502-129">See [Step-by-Step Instructions for Publishing Applications](https://go.microsoft.com/fwlink/?LinkID=196149)</span></span>


<a id="ChangesAndIssues"></a>

## <a name="changes-and-issues"></a><span data-ttu-id="9d502-130">변경 내용 및 문제</span><span class="sxs-lookup"><span data-stu-id="9d502-130">Changes and Issues</span></span>

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-10-installation-issues"></a><span data-ttu-id="9d502-131">WebMatrix 1.0 설치 문제</span><span class="sxs-lookup"><span data-stu-id="9d502-131">WebMatrix 1.0 Installation Issues</span></span>

#### <a name="issue-webmatrix-10-is-available-only-on-platforms-that-support-microsoft-net-framework-4"></a><span data-ttu-id="9d502-132">문제: WebMatrix 1.0은 Microsoft.NET Framework 4를 지 원하는 플랫폼 에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-132">Issue: WebMatrix 1.0 is available only on platforms that support Microsoft .NET Framework 4</span></span>

> <span data-ttu-id="9d502-133">.NET Framework 버전 4가 WebMatrix 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-133">The .NET Framework version 4 is required for WebMatrix.</span></span> <span data-ttu-id="9d502-134">특정 경우에 WebMatrix 1.0 설치 관리자는 사용해 볼 수 있도록 지원 되는 구성 집합의 일부가 아닌 플랫폼을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-134">In certain cases, the WebMatrix 1.0 installer will let you try to install on a platform that is not part of the supported configuration set.</span></span> <span data-ttu-id="9d502-135">특히 Windows Vista SP1 업데이트를 사용 하면 WebMatrix의 설치를 시작 하면 되지만.NET Framework 4 구성 요소는 실패 하 고 설치를 차단 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-135">In particular, Windows Vista without the SP1 update will let you begin the installation of WebMatrix, but the .NET Framework 4 component will fail and block your installation.</span></span>
> 
> <span data-ttu-id="9d502-136">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-136">**Workaround**</span></span>  
> <span data-ttu-id="9d502-137">포함 하는 지원 되는 플랫폼에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-137">Install on a supported platform, which includes:</span></span>
> 
> - <span data-ttu-id="9d502-138">Windows 7</span><span class="sxs-lookup"><span data-stu-id="9d502-138">Windows 7</span></span>
> - <span data-ttu-id="9d502-139">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="9d502-139">Windows Server 2008</span></span>
> - <span data-ttu-id="9d502-140">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="9d502-140">Windows Server 2008 R2</span></span>
> - <span data-ttu-id="9d502-141">Windows Vista SP1 이상</span><span class="sxs-lookup"><span data-stu-id="9d502-141">Windows Vista SP1 or later</span></span>
> - <span data-ttu-id="9d502-142">Windows XP SP3</span><span class="sxs-lookup"><span data-stu-id="9d502-142">Windows XP SP3</span></span>
> - <span data-ttu-id="9d502-143">Windows Server 2003 SP2</span><span class="sxs-lookup"><span data-stu-id="9d502-143">Windows Server 2003 SP2</span></span>


#### <a name="issue-cannot-install-webmatrix-10-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a><span data-ttu-id="9d502-144">문제: Microsoft Visual Studio 2008은 Microsoft Visual Studio 2008 SP1 없이 설치 된 경우 WebMatrix 1.0을 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-144">Issue: Cannot install WebMatrix 1.0 if Microsoft Visual Studio 2008 is installed without Microsoft Visual Studio 2008 SP1</span></span>

> <span data-ttu-id="9d502-145">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-145">**Workaround**</span></span>  
> <span data-ttu-id="9d502-146">설치할 [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) Microsoft 다운로드 센터에서.</span><span class="sxs-lookup"><span data-stu-id="9d502-146">Install [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) from the Microsoft Download Center.</span></span>


#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a><span data-ttu-id="9d502-147">문제: SQL Server Compact 4.0에 대 한 일부 어셈블리는 GAC에 설치 되지</span><span class="sxs-lookup"><span data-stu-id="9d502-147">Issue: Some assemblies for SQL Server Compact 4.0 are not installed in the GAC</span></span>

> <span data-ttu-id="9d502-148">64 비트 컴퓨터에서 SQL Server Compact 4.0을 설치 하 고 컴퓨터 프로필에만.NET Framework 3.5 SP1 클라이언트 설치에 SQL Server Compact 4.0 용 관리 되는 어셈블리를 전역 어셈블리 캐시 (GAC)에 배치 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-148">The managed assemblies for SQL Server Compact 4.0 are not placed in the global assembly cache (GAC) when you install SQL Server Compact 4.0 on a 64-bit computer and the computer has only the .NET Framework 3.5 SP1 Client Profile installed.</span></span> <span data-ttu-id="9d502-149">GAC에 설치 되지 않은 관리 되는 어셈블리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-149">The managed assemblies that are not installed in the GAC are:</span></span>
> 
> - <span data-ttu-id="9d502-150">*System.Data.SqlServerCe.dll* (ADO.NET 공급자)</span><span class="sxs-lookup"><span data-stu-id="9d502-150">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span></span>
> - <span data-ttu-id="9d502-151">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework)</span><span class="sxs-lookup"><span data-stu-id="9d502-151">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span></span>
> 
> <span data-ttu-id="9d502-152">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-152">**Workaround**</span></span>  
> <span data-ttu-id="9d502-153">제거할 SQL Server Compact 4.0입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-153">Uninstall SQL Server Compact 4.0.</span></span> <span data-ttu-id="9d502-154">다운로드 하 고 다음 위치에서.NET Framework 3.5 SP1의 정식 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-154">Download and install the full version of .NET Framework 3.5 SP1 from the following location:</span></span>  
>   
> [<span data-ttu-id="9d502-155">Microsoft.NET Framework 3.5 서비스 팩 1 (전체 패키지)</span><span class="sxs-lookup"><span data-stu-id="9d502-155">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> <span data-ttu-id="9d502-156">SQL Server Compact 4.0를 다시 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-156">Then reinstall SQL Server Compact 4.0.</span></span>


#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a><span data-ttu-id="9d502-157">문제: SQL Server Compact는 명령줄을 사용 하 여 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-157">Issue: Cannot uninstall SQL Server Compact using the command line</span></span>

> <span data-ttu-id="9d502-158">SQL Server Compact 명령줄 옵션을 사용 하 여 제거는이 릴리스에서 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-158">Uninstallation of SQL Server Compact using command-line options does not work in this release.</span></span>
> 
> <span data-ttu-id="9d502-159">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-159">**Workaround**</span></span>  
> <span data-ttu-id="9d502-160">사용 하 여 *프로그램 및 기능* Microsoft SQL Server Compact 4.0을 제거 하려면 Windows 제어판에서.</span><span class="sxs-lookup"><span data-stu-id="9d502-160">Use *Programs and Features* in the Windows Control Panel to uninstall Microsoft SQL Server Compact 4.0.</span></span>


<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a><span data-ttu-id="9d502-161">ASP.NET 웹 페이지</span><span class="sxs-lookup"><span data-stu-id="9d502-161">ASP.NET Web Pages</span></span>

<span data-ttu-id="9d502-162">문서의이 섹션에서는 새로운 기능, 변경 및 Razor 구문이 있는 ASP.NET 웹 페이지 1.0 릴리스를 사용 하 여 알려진된 문제에 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-162">This section of the document describes new features, changes, and known issues with the 1.0 release of ASP.NET Web Pages with Razor syntax.</span></span>

- [<span data-ttu-id="9d502-163">새로운 기능</span><span class="sxs-lookup"><span data-stu-id="9d502-163">New features</span></span>](#NewFeatures)
- [<span data-ttu-id="9d502-164">변경 내용</span><span class="sxs-lookup"><span data-stu-id="9d502-164">Changes</span></span>](#Changes)
- [<span data-ttu-id="9d502-165">문제</span><span class="sxs-lookup"><span data-stu-id="9d502-165">Issues</span></span>](#Issues)

#### <a id="NewFeatures"></a>  <span data-ttu-id="9d502-166">새로운 기능</span><span class="sxs-lookup"><span data-stu-id="9d502-166">New Features</span></span>

#### <a name="new-configuration-setting-added-to-disable-the-package-manager"></a><span data-ttu-id="9d502-167">패키지 관리자를 사용 하지 않도록 설정에 구성 설정을 추가 하는 새로운 기능:</span><span class="sxs-lookup"><span data-stu-id="9d502-167">New: Configuration setting added to disable the package manager</span></span>

> <span data-ttu-id="9d502-168">새 `asp:AdminManagerEnabled` 키 수를 `<appSettings>` 요소에는 *web.config* 완전히 패키지 관리자를 사용 하지 않도록 설정할 수 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-168">A new `asp:AdminManagerEnabled` key is available for the `<appSettings>` element in the *web.config* file, which lets you completely disable the package manager.</span></span> <span data-ttu-id="9d502-169">이 요소에 대 한 기본값은 true, 즉에 포함 되지 않으면 합니다 *web.config* 파일, 패키지 관리자를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-169">The default value for this element is true, meaning that if it is not included in the *web.config* file, the package manager is enabled.</span></span> <span data-ttu-id="9d502-170">패키지 관리자를 사용 하지 않으려면 다음 요소를 추가 합니다 *web.config* 웹 사이트의 루트에 있는 파일:</span><span class="sxs-lookup"><span data-stu-id="9d502-170">To disable the package manager, add the following element to the *web.config* file in the root of the website:</span></span>
> 
> [!code-xml[Main](overview/samples/sample1.xml)]


#### <a id="Changes"></a>  <span data-ttu-id="9d502-171">Changes</span><span class="sxs-lookup"><span data-stu-id="9d502-171">Changes</span></span>

#### <a name="change-webpagesadminfoldervirtualpath-key-renamed-to-aspadminfoldervirtualpath"></a><span data-ttu-id="9d502-172">"Asp: AdminFolderVirtualPath" 이름이 "webPages:AdminFolderVirtualPath" 키를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-172">Change: "webPages:AdminFolderVirtualPath" key renamed to "asp:AdminFolderVirtualPath"</span></span>

> <span data-ttu-id="9d502-173">`webPages:AdminFolderVirtualPath` 에 추가할 수 있는 키를 *web.config* 사용 하려면 패키지 관리자의 위치를 지정 하는 파일 이름이 바뀐를 `asp:` 대신 네임 스페이스는 `webPages` 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-173">The `webPages:AdminFolderVirtualPath` key that can be added to the *web.config* file to specify the location of the package manager has been renamed to use the `asp:` namespace instead of the `webPages` namespace.</span></span> <span data-ttu-id="9d502-174">이 요소를 사용한 경우 구성 파일의 이름을 바꿀 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-174">If you have used this element, you must rename it in the configuration file.</span></span>


#### <a id="Issues"></a>  <span data-ttu-id="9d502-175">알려진된 문제</span><span class="sxs-lookup"><span data-stu-id="9d502-175">Known Issues</span></span>

#### <a name="issue-passwords-for-membership-users-no-longer-recognized"></a><span data-ttu-id="9d502-176">더 이상 인식 하는 멤버 자격 사용자에 대 한 암호 문제:</span><span class="sxs-lookup"><span data-stu-id="9d502-176">Issue: Passwords for membership users no longer recognized</span></span>

> <span data-ttu-id="9d502-177">만들기 및 멤버 자격 (로그인) 암호를 저장 하기 위한 알고리즘 보다 안전한 것으로 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-177">The algorithm for creating and storing membership (login) passwords has been changed to be more secure.</span></span> <span data-ttu-id="9d502-178">결과적으로, ASP.NET Razor의 베타 버전에서 만든 멤버 (사용자)에 대 한 저장 된 암호를 인식할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-178">As a result, the passwords stored for members (users) created in Beta versions of ASP.NET Razor will not be recognized.</span></span> 
> 
> <span data-ttu-id="9d502-179">**해결 방법** 사이트에 아직 프로덕션에 배치 된 되지 경우 멤버 자격 데이터베이스에서 사용자 레코드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-179">**Workaround** If the site has not yet been put into production, remove the user records from the membership database.</span></span> <span data-ttu-id="9d502-180">프로그래밍 방식으로 데이터베이스 라이브 인 경우 멤버 자격 데이터베이스에서 기존 암호 다시 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-180">If database is live, programmatically regenerate existing passwords in the membership database.</span></span>


#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a><span data-ttu-id="9d502-181">문제: 예기치 않은 동작이 멤버 자격에 대 한 사용자 테이블을 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="9d502-181">Issue: Unexpected behavior when using a custom user table for membership</span></span>

> <span data-ttu-id="9d502-182">호출 하는 ASP.NET Razor 웹 사이트에 대 한 멤버 자격 공급자를 초기화 하는 `WebSecurity.InitializeDatabaseConnection` 메서드.</span><span class="sxs-lookup"><span data-stu-id="9d502-182">To initialize the membership provider for an ASP.NET Razor website, you call the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="9d502-183">(시작 사이트 템플릿의 WebMatrix에서이 메서드에 대 한 호출을 포함 합니다  *\_AppStart.cshtml* 파일입니다.) 경우는 `autoCreateTables` 이 메서드의 매개 변수 설정을 true로 (기본적으로 설정은 시작 사이트 템플릿의 true), 하며 메서드는 인식할 수 없는 테이블 이름 (두 번째 매개 변수) 메서드에 전달 되 면 오류가 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-183">(In WebMatrix, the Starter Site template includes a call to this method in the *\_AppStart.cshtml* file.) If the `autoCreateTables` parameter of this method is set to true (by default, it is set to true in the Starter Site template), and if an unrecognized table name is passed to the method (the second parameter), the method does not throw an error.</span></span> <span data-ttu-id="9d502-184">대신 테이블을 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-184">Instead, it automatically creates the table.</span></span>
> 
> <span data-ttu-id="9d502-185">이 멤버 자격에 대 한 사용자 테이블을 사용 하지만 잘못 된 테이블 이름을 전달 하려는 경우 문제가 될 수는 `WebSecurity.InitializeDatabaseConnection` 메서드.</span><span class="sxs-lookup"><span data-stu-id="9d502-185">This can be a problem if you intend to use a custom user table for membership but pass the wrong table name to the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="9d502-186">메서드는 기본적으로 오류가 발생 하지 지정한 테이블 없으면 및 대신 새 테이블을 만들기 때문에 응용 프로그램 작동에 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-186">Because the method does not by default raise an error if the table you specify does not exist, and because it instead creates a new table, the application can appear to be working.</span></span> <span data-ttu-id="9d502-187">그러나 사용자 테이블 (및 해당 필드에)를 사용 하는 응용 프로그램 코드 예기치 않은 오류를 사용 하 여 최종적으로 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-187">However, application code that relies on your custom user table (and on fields in it) can eventually fail with unexpected errors.</span></span>
> 
> <span data-ttu-id="9d502-188">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-188">**Workaround**</span></span>  
> <span data-ttu-id="9d502-189">이름에 성공 했는지 확인 합니다 `InitializeDatabaseConnection` 사용자 프로필 멤버 자격 데이터베이스에서 테이블 또는 했는지 메서드 일치를 `autoCreateTables` 매개 변수를 false로.</span><span class="sxs-lookup"><span data-stu-id="9d502-189">Make sure that the name passed in the `InitializeDatabaseConnection` method matches the user profile table in the membership database, or make sure that the `autoCreateTables` parameter is set to false.</span></span>


#### <a name="issue-error-message-the-admin-module-requires-access-to-appdata"></a><span data-ttu-id="9d502-190">문제: 오류 메시지 "~/App에 대 한 액세스 관리 모듈에 필요한\_데이터"</span><span class="sxs-lookup"><span data-stu-id="9d502-190">Issue: Error message "The Admin Module requires access to ~/App\_Data"</span></span>

> <span data-ttu-id="9d502-191">상황에 따라 사용자 만들기 또는 그렇지 않은 경우 ASP.NET 멤버 자격 시스템을 사용 하려고 하면 오류를 표시 하도록 페이지 *The 관리자 모듈 ~/App 액세스할 수 있어야\_데이터*입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-191">Under some circumstances, trying to create users or otherwise work with the ASP.NET membership system can cause the page to display the error *The Admin Module requires access to ~/App\_Data*.</span></span> <span data-ttu-id="9d502-192">IIS 또는 IIS Express에서 실행 되는 계정을 만들고 쓸 수 있는 권한이 없는 경우이 경고가 발생 합니다 *앱\_데이터* 웹 사이트 루트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-192">This occurs if the account that IIS or IIS Express is running under does not have permissions to create and write to the *App\_Data* folder under the website root.</span></span> 
> 
> <span data-ttu-id="9d502-193">**해결 방법** 수동으로 만들기는 *App\_데이터* 웹 사이트에 대 한 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-193">**Workaround** Manually create an *App\_Data* folder for the website.</span></span> <span data-ttu-id="9d502-194">응용 프로그램 (일반적으로 NETWORK SERVICE)에서 실행 되는 Windows 계정에 앱과 같은 하위 폴더 및 응용 프로그램의 루트 폴더에 대 한 읽기/쓰기 권한이 있는지를 확인 한 다음\_데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-194">Then make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as App\_Data.</span></span> <span data-ttu-id="9d502-195">자세한 내용은 기술 자료 문서에서 사용할 수 [SQL Server Express 사용자 인스턴스 및 ASP.net 웹 응용 프로그램 프로젝트를 사용 하 여 문제](https://support.microsoft.com/kb/2002980)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-195">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>


#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a><span data-ttu-id="9d502-196">문제: "못했습니다" SQL Server의 사용자 인스턴스 생성 오류</span><span class="sxs-lookup"><span data-stu-id="9d502-196">Issue: "Failed to generate a user instance of SQL Server" error</span></span>

> <span data-ttu-id="9d502-197">WebMatrix 웹 응용 프로그램을 SQL Server Express를 사용 하 여 Windows 7 또는 Windows Server 2008 R2에서 IIS 7.5를 실행 중인 경우 SQL Server가 런타임 시 사용자의 로컬 응용 프로그램 경로 검색할 수 없습니다 나타내는 오류가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-197">If a WebMatrix Web application uses SQL Server Express and is running IIS 7.5 on Windows 7 or Windows Server 2008 R2, you might see an error that indicates that SQL Server cannot retrieve the user's local application path at run time.</span></span>
> 
> <span data-ttu-id="9d502-198">**해결 방법** 응용 프로그램 (일반적으로 NETWORK SERVICE)에서 실행 되는 Windows 계정에 하위 폴더 및 응용 프로그램의 루트 폴더에 대 한 읽기/쓰기 권한을 같은 *앱\_데이터*.</span><span class="sxs-lookup"><span data-stu-id="9d502-198">**Workaround** Make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as *App\_Data*.</span></span> <span data-ttu-id="9d502-199">자세한 내용은 기술 자료 문서에서 사용할 수 [SQL Server Express 사용자 인스턴스 및 ASP.net 웹 응용 프로그램 프로젝트를 사용 하 여 문제](https://support.microsoft.com/kb/2002980)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-199">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>


#### <a name="issue-files-that-contains-package-manager-resources-or-package-manager-passwords-are-servable-under-iis-60-and-earlier"></a><span data-ttu-id="9d502-200">문제: 패키지 관리자 리소스 또는 패키지 관리자 암호를 포함 하는 파일은 IIS 6.0에서 제공 가능으로 및 이전 버전</span><span class="sxs-lookup"><span data-stu-id="9d502-200">Issue: Files that contains package-manager resources or package-manager passwords are servable under IIS 6.0 and earlier</span></span>

> <span data-ttu-id="9d502-201">RC2 릴리스를 사용 하 여 빌드된 하는 ASP.NET Web Pages (Razor) 응용 프로그램을 배포 하는 경우 및 응용 프로그램을 포함 하는 경우는 *password.txt* 하거나 *packagesources.txt* 파일 */App\_ 데이터/관리자*, IIS 6.0 요청, 잠재적으로 패키지 관리자 인스턴스에 대 한 암호를 노출 하는 경우 파일을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-201">If you deploy an ASP.NET Web Pages (Razor) application that was built using the RC2 release, and if the application contains a *password.txt* or *packagesources.txt* file under */App\_Data/admin*, IIS 6.0 will serve the file if requested, potentially exposing the passwords for your package manager instance.</span></span> 
> 
> <span data-ttu-id="9d502-202">**해결 방법** 이름 바꾸기는 *password.txt* 하거나 *packagesources.txt* 파일을 *password.config* 또는 *packagesources.config*. IIS 6.0은 기본적으로 파일을 처리 하지 않는 경우는 *.config* 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-202">**Workaround** Rename the *password.txt* or *packagesources.txt* file to *password.config* or *packagesources.config*. By default, IIS 6.0 does not serve files that have the *.config* extension.</span></span> <span data-ttu-id="9d502-203">(IIS 7에서는에 파일이 없는 합니다 *앱\_데이터* 폴더가 제공 되는 파일 이름을 바꿀 필요가 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="9d502-203">(In IIS 7, no files in the *App\_Data* folder are served, so you do not need to rename the files.)</span></span>


#### <a name="issue-uninstalling-packages-installed-using-the-beta-3-release-does-not-completely-remove-package-components"></a><span data-ttu-id="9d502-204">문제: 베타 3 릴리스를 사용 하 여 설치 된 패키지를 제거 하면 완전히 제거 하지 않습니다 패키지 구성 요소</span><span class="sxs-lookup"><span data-stu-id="9d502-204">Issue: Uninstalling packages installed using the Beta 3 release does not completely remove package components</span></span>

> <span data-ttu-id="9d502-205">Beta 3 릴리스에에서 패키지 관리자를 사용 하 여 패키지를 설치 하 고 현재 버전을 사용 하 여 제거를 시도 하는 경우 패키지를 완전히 제거 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-205">If you installed a package using the package manager in the Beta 3 release and then try to uninstall it using the current release, the package is not completely uninstalled.</span></span> <span data-ttu-id="9d502-206">패키지 관리자를 사용 하 여 **제거** 단추 몇 가지 구성 요소를 제거 하지만 라이브러리 코드 패키지의 떠나고 업데이트 되지 않는 합니다 *package.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-206">Using the package manager's **Uninstall** button removes some components, but leaves the package's library code and does not update the *package.config* file.</span></span>
> 
> <span data-ttu-id="9d502-207">**해결 방법** </span><span class="sxs-lookup"><span data-stu-id="9d502-207">**Workaround** </span></span>  
> <span data-ttu-id="9d502-208">다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-208">Perform these steps:</span></span>  
> 1. <span data-ttu-id="9d502-209">삭제 된 *앱\_Data\packages* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-209">Delete the *App\_Data\packages* folder.</span></span> <span data-ttu-id="9d502-210">이 모든 패키지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-210">This removes all packages.</span></span>   
> 2. <span data-ttu-id="9d502-211">삭제 된 *packages.config* 웹 사이트의 루트에 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-211">Delete the *packages.config* file in the root of the website.</span></span>


#### <a name="issue-in-visual-studio-invoking-the-web-based-package-manager-takes-the-application-offline"></a><span data-ttu-id="9d502-212">문제: Visual Studio에서 웹 기반 패키지 관리자를 호출 합니다. 오프 라인 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="9d502-212">Issue: In Visual Studio, invoking the web-based package manager takes the application offline</span></span>

> <span data-ttu-id="9d502-213">Visual Studio (없습니다 WebMatrix)에서 작업 하는 하 고 사용 하는 경우는  *\_관리자* Visual Studio 패키지 관리자를 시작 하는 기능이 응용 프로그램을 오프 라인으로 전환 하 고 게시 합니다 *앱\_ offline.htm* 패키지 관리자를 사용 하는 기능을 방해 하는 웹 사이트 루트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-213">If you are working in Visual Studio (not WebMatrix) and use the *\_admin* functionality to start the package manager, Visual Studio takes the application offline and posts the *app\_offline.htm* into the website root, which disrupts your ability to use the package manager.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="9d502-214">추가, 제거 또는에서 파일을 수정 하는 경우 동일한 동작이 수행는 가장 일반적으로 표시 되지만이 문제는 웹 기반 패키지 관리자 인터페이스를 사용 하는 경우에 *앱\_데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-214">Although you would most typically see this behavior when using the web-based package manager interface, the same behavior occurs if you add, remove, or modify any files in the *App\_Data* folder.</span></span>
> 
> <span data-ttu-id="9d502-215">**해결 방법** </span><span class="sxs-lookup"><span data-stu-id="9d502-215">**Workaround** </span></span>  
> <span data-ttu-id="9d502-216">Visual Studio에서 패키지를 사용 하려면 웹 기반 패키지 관리자 대신 NuGet 확장을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-216">To work with packages in Visual Studio, use the NuGet extension instead of the web-based package manager.</span></span> <span data-ttu-id="9d502-217">정보에 대 한 참조를 [NuGet 설명서](https://docs.microsoft.com/nuget/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-217">For information, see the [NuGet documentation](https://docs.microsoft.com/nuget/).</span></span> <span data-ttu-id="9d502-218">다른 파일을 사용 하 여 작업 하는 경우는 *앱\_데이터* 폴더에이 문제를 방지 하려면 다른 위치에서 파일을 유지 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-218">If you are working with other files in the *App\_Data* folder, consider keeping the files elsewhere to avoid this issue.</span></span> <span data-ttu-id="9d502-219">그렇게 해도 효과가 없는 경우 삭제 합니다 *앱\_offline.htm* 파일을 수동으로 또는 자동으로 (기본적으로 30 초 후) 사이트를 다시 온라인 상태가 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-219">If that's not practical, delete the *app\_offline.htm* file manually or wait until the site comes back online automatically (by default, after 30 seconds).</span></span>


#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a><span data-ttu-id="9d502-220">문제: Visual Studio IntelliSense 및 프로젝트 템플릿이 ASP.NET MVC 3 버전 에서만 사용할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="9d502-220">Issue: Visual Studio IntelliSense and project templates available only in ASP.NET MVC version 3</span></span>

> <span data-ttu-id="9d502-221">ASP.NET 웹 페이지를 설치 설치 하지 않습니다도 도구 Visual Studio에 대 한 예: ASP.NET Web Pages 응용 프로그램에 대 한 IntelliSense 및 프로젝트 템플릿.</span><span class="sxs-lookup"><span data-stu-id="9d502-221">Installing ASP.NET Web Pages does not also install tools for Visual Studio such as IntelliSense and project templates for ASP.NET Web Pages applications.</span></span>
> 
> <span data-ttu-id="9d502-222">**해결 방법** 웹 플랫폼 설치 관리자를 통해 ASP.NET MVC 3 RC 설치 Visual Studio에서 ASP.NET 웹 페이지 응용 프로그램에 대 한 IntelliSense 및 프로젝트 템플릿을 사용 하려면 또는 [독립 실행형 설치 관리자](https://go.microsoft.com/fwlink/?LinkID=191797)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-222">**Workaround** To use IntelliSense and project templates for ASP.NET Web Pages applications in Visual Studio, install ASP.NET MVC 3 RC either through the Web Platform Installer or the [stand-alone installer](https://go.microsoft.com/fwlink/?LinkID=191797).</span></span>


#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a><span data-ttu-id="9d502-223">문제: 프록시 서버를 통해 다른 외부 데이터 나 피드 읽기</span><span class="sxs-lookup"><span data-stu-id="9d502-223">Issue: Reading feeds or other external data via a proxy server</span></span>

> <span data-ttu-id="9d502-224">에 대 한 프록시 정보를 구성 해야 사이트를 실행 하는 서버를 프록시 서버로 보호 하는 경우는 *web.config* 외부 사이트에서 제공 되는 정보를 읽을 수 있도록 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-224">If the server running the site is behind a proxy server, you might need to configure proxy information in the *web.config* file in order to be able to read information that comes from outside your site.</span></span> <span data-ttu-id="9d502-225">예를 들어, 사용 하는 경우는 `ReCaptcha` 도우미 도우미 reCAPTCHA 서비스와 통신 하지만 프록시 서버에서 차단 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-225">For example, if you use the `ReCaptcha` helper, the helper communicates with the reCAPTCHA service, but might be blocked by your proxy server.</span></span> <span data-ttu-id="9d502-226">마찬가지로, 패키지 관리자를 사용한 피드 등 ASP.NET 웹 페이지에서 사용 되는 피드 프록시 구성이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-226">Similarly, feeds that are used in ASP.NET Web Pages, such as the feed used by the package manager, might require proxy configuration.</span></span>
> 
> <span data-ttu-id="9d502-227">패키지 피드를 사용 하거나 외부 서비스를 사용 하 여 작업에 문제가 있는 경우 다음 요소를 응용 프로그램의 루트에 배치 *web.config* 파일:</span><span class="sxs-lookup"><span data-stu-id="9d502-227">If you experience problems in working with an external service or working with the package feed, put the following elements into your application's root *web.config* file:</span></span>
> 
> [!code-xml[Main](overview/samples/sample2.xml)]
> 
> <span data-ttu-id="9d502-228">프록시 서버를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [ &lt;프록시&gt; 요소 (네트워크 설정)](https://msdn.microsoft.com/library/sa91de1e.aspx) MSDN 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-228">For more information about configuring a proxy server, see [&lt;proxy&gt; Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on the MSDN Web site.</span></span>


#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="9d502-229">문제: Razor 구문이 있는 ASP.NET 웹 페이지를 사용 하지 않도록 설정.NET Framework 버전 4 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-229">Issue: Uninstalling the .NET Framework version 4 disables ASP.NET Web Pages with Razor Syntax</span></span>

> <span data-ttu-id="9d502-230">.NET Framework 버전 4 제거 하 고 다시 설치 하는 경우에 Razor 구문이 있는 ASP.NET 웹 페이지 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-230">If you uninstall the .NET Framework version 4 and then reinstall it, ASP.NET Web Pages with Razor syntax is disabled.</span></span> <span data-ttu-id="9d502-231">사용 하 여 페이지의 *.cshtml* 확장 제대로 실행 되지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="9d502-231">Pages with the *.cshtml* extension do not run correctly.</span></span> <span data-ttu-id="9d502-232">컴퓨터 루트에 있는 어셈블리를 등록 하는 ASP.NET 웹 페이지 *web.config* 파일 및.NET Framework를 제거 합니다. 해당 파일을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-232">ASP.NET Web Pages registers an assembly in the machine root *web.config* file, and removing the .NET Framework removes that file.</span></span> <span data-ttu-id="9d502-233">.NET Framework를 다시 설치 하면 구성 파일의 새 버전을 설치 하지만 ASP.NET 웹 페이지 어셈블리에 대 한 참조를 추가 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-233">Reinstalling the .NET Framework installs a new version of the configuration file, but does not add the reference for the ASP.NET Web Pages assembly.</span></span>
> 
> <span data-ttu-id="9d502-234">**해결 방법** .NET Framework를 다시 설치한 후 Razor 구문이 있는 ASP.NET 웹 페이지를 다시 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-234">**Workaround** After reinstalling the .NET Framework, reinstall ASP.NET Web Pages with Razor syntax.</span></span> <span data-ttu-id="9d502-235">다음 요소를 추가 합니다 *web.config* 일반적으로 다음 위치에 있는 컴퓨터 루트에 있는 파일:</span><span class="sxs-lookup"><span data-stu-id="9d502-235">This adds the following element to the *web.config* file in the machine root, which is typically in the following location:</span></span>  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](overview/samples/sample3.xml)]


#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a><span data-ttu-id="9d502-236">문제: 확장명 없는 Url을 IIS 7 또는 IIS 7.5.cshtml/.vbhtml 파일 찾지 못한</span><span class="sxs-lookup"><span data-stu-id="9d502-236">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span></span>

> <span data-ttu-id="9d502-237">IIS 7 또는 IIS 7.5에서 다음과 같은 URL 사용 하 여 요청은 포함 된 페이지를 찾을 수 합니다 *.cshtml* 하거나 *.vbhtml* 확장:</span><span class="sxs-lookup"><span data-stu-id="9d502-237">On IIS 7 or IIS 7.5, requests with a URL like the following are not able to find pages that have the *.cshtml* or *.vbhtml* extension:</span></span>  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> <span data-ttu-id="9d502-238">URL 재작성 활성화 되어 있지 않으므로 기본적으로 IIS 7 또는 IIS 7.5 용 르면 문제가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-238">The issue arises because URL rewriting is not enabled by default for IIS 7 or IIS 7.5.</span></span> <span data-ttu-id="9d502-239">문제일 수 있습니다 시나리오에는 IIS Express를 사용 하 여 로컬로 테스트할 때 문제가 표시 되지 않으면 있지만 호스팅 웹 사이트에 웹 사이트를 배포할 때 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-239">The likeliest scenario is that you do not see the problem when testing locally using IIS Express, but you experience it when you deploy your website to a hosting website.</span></span>
> 
> <span data-ttu-id="9d502-240">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-240">**Workaround**</span></span>
> 
> - <span data-ttu-id="9d502-241">서버 컴퓨터에 대 한 제어를 사용 하는 경우 서버 컴퓨터의 설치에 설명 된 업데이트가 [는 업데이트를 사용할 수 있도록 특정 Url을 요청 하는 IIS 7.0 또는 IIS 7.5 처리기를 처리 하는 마침표로 끝나지 않는](https://support.microsoft.com/kb/980368)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-241">If you have control over the server computer, on the server computer install the update that is described in [A update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).</span></span>
> - <span data-ttu-id="9d502-242">서버 컴퓨터에 대 한 제어 없는 경우 (예를 들어, 배포 하는 호스팅 웹 사이트), 웹 사이트의 다음 추가할 *web.config* 파일:</span><span class="sxs-lookup"><span data-stu-id="9d502-242">If you do not have control over the server computer (for example, you are deploying to a hosting website), add the following to the website's *web.config* file:</span></span> 
> 
>     [!code-xml[Main](overview/samples/sample4.xml)]


#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a><span data-ttu-id="9d502-243">문제: SQL Server Compact 설치 되지 않은 컴퓨터에 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="9d502-243">Issue: Deploying an application to a computer that does not have SQL Server Compact installed</span></span>

> <span data-ttu-id="9d502-244">SQL Server Compact 데이터베이스를 포함 하는 응용 프로그램 SQL Server Compact는 설치 되지 않은 컴퓨터에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-244">Applications that include SQL Server Compact databases can run on a computer where SQL Server Compact is not installed.</span></span> <span data-ttu-id="9d502-245">Microsoft WebMatrix 1.0에서 자동으로 이러한 이진 파일을 복사 하 고 적절 한 수행 *web.config* 파일 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-245">Microsoft WebMatrix 1.0 automatically copies these binaries for you and performs the appropriate *web.config* file transforms.</span></span>
> 
> <span data-ttu-id="9d502-246">**해결 방법** 이러한 파일을 복사 하 고 확인 해야 할 경우 합니다 *web.config* 파일 변경 내용을 수동으로 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-246">**Workaround** If you need to copy these files and make the *web.config* file changes manually, do the following:</span></span>
> 
> 1. <span data-ttu-id="9d502-247">데이터베이스 엔진 어셈블리를 복사 합니다 *Bin* 대상 컴퓨터에서 응용 프로그램의 폴더 (및 하위 폴더).</span><span class="sxs-lookup"><span data-stu-id="9d502-247">Copy the database engine assemblies to the *Bin* folder (and subfolders) of the application on the target computer:</span></span>  
> 
>    - <span data-ttu-id="9d502-248">Copy *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* </span><span class="sxs-lookup"><span data-stu-id="9d502-248">Copy *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* </span></span>  
>        <span data-ttu-id="9d502-249">**to** *\Bin*</span><span class="sxs-lookup"><span data-stu-id="9d502-249">**to** *\Bin*</span></span>
>    - <span data-ttu-id="9d502-250">복사본 <em>C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\</em><strong><em>하</em></strong>\Bin\x86\*</span><span class="sxs-lookup"><span data-stu-id="9d502-250">Copy <em>C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\</em><strong><em>to</em></strong>\Bin\x86\*</span></span>
>    - <span data-ttu-id="9d502-251">복사본 <em>C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\</em>\* <strong>하</strong><em>\Bin\amd64</em></span><span class="sxs-lookup"><span data-stu-id="9d502-251">Copy <em>C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\</em>\* <strong>to</strong><em>\Bin\amd64</em></span></span>
> 
> 2. <span data-ttu-id="9d502-252">웹 사이트의 루트 폴더를 만들거나 엽니다는 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-252">In the root folder of the website, create or open a *web.config* file.</span></span> <span data-ttu-id="9d502-253">(WebMatrix 1.0에서이 파일 형식은 클릭할 경우 사용할 수 있습니다 **모든** 에 **파일 형식을 선택** 대화 상자.)</span><span class="sxs-lookup"><span data-stu-id="9d502-253">(In WebMatrix 1.0, this file type is available if you click **All** in the **Choose a File Type** dialog box.)</span></span>
> 3. <span data-ttu-id="9d502-254">다음 요소 자식으로 추가 합니다 `<configuration>` 요소 (에 포함 되지 않은 `<system.web>` 요소).</span><span class="sxs-lookup"><span data-stu-id="9d502-254">Add the following element as a child of the `<configuration>` element (not inside the `<system.web>` element):</span></span>
> 
>     [!code-xml[Main](overview/samples/sample5.xml)]


#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a><span data-ttu-id="9d502-255">문제: Visual Basic에서 보통 신뢰 "Database" 및 "WebGrid" 도우미 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-255">Issue: "Database" and "WebGrid" helpers do not work in Medium Trust in Visual Basic</span></span>

> <span data-ttu-id="9d502-256">Visual Basic을 사용 하는 경우 (만드는 *.vbhtml* 파일), `Database` 고 `WebGrid` 도우미 응용 프로그램은 보통 신뢰를 사용 하도록 설정 된 경우 작동 하지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-256">If you are using Visual Basic (creating *.vbhtml* files), the `Database` and `WebGrid` helpers will not work if the application is set to use Medium Trust.</span></span>
> 
> <span data-ttu-id="9d502-257">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-257">**Workaround**</span></span>  
> <span data-ttu-id="9d502-258">Visual Studio 2010을 사용 하는 경우에 서비스 팩 1 릴리스를 설치 하 여이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-258">If you use Visual Studio 2010, you can resolve this problem by installing the Service Pack 1 release.</span></span> <span data-ttu-id="9d502-259">Sp1의 최종 버전까지 베타 버전에서 SP1 다운로드할 수 있습니다 합니다 [Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) Microsoft 다운로드 센터 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-259">Until the final version of the SP1 release is available, you can download the Beta version of SP1 from the [Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) page on the Microsoft Download Center.</span></span>   
>   
> <span data-ttu-id="9d502-260">이 방법은 실용적이 지 않거나 Visual Studio 2010을 사용 하지 않으면 하면 일시적으로 완전 신뢰를 사용 하 여 응용 프로그램을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-260">If this is not practical, or if you do not use Visual Studio 2010, you can temporarily set the application to use Full Trust.</span></span>


#### <a name="issue-applicationpart-resources-are-externally-accessible"></a><span data-ttu-id="9d502-261">문제: "ApplicationPart" 리소스는 외부에서 액세스할 수</span><span class="sxs-lookup"><span data-stu-id="9d502-261">Issue: "ApplicationPart" resources are externally accessible</span></span>

> <span data-ttu-id="9d502-262">어셈블리에서 파생 되는 개체를 포함 하는 경우는 `ApplicationPart` 어셈블리의 리소스에 의해 노출 되는 클래스는 `ResourceRouteHandler` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-262">If an assembly contains objects that derives from the `ApplicationPart` class, that assembly's resources are exposed by the `ResourceRouteHandler` class.</span></span> <span data-ttu-id="9d502-263">예를 들어 다음 URL을 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-263">For example, consider the following URL:</span></span>  
>   
> `~/r.ashx/System.Web.WebPages.Administration/Resources/AdminResources.resources`  
>   
> <span data-ttu-id="9d502-264">이 요청에 리소스 문자열의 모든 다운로드 합니다 *System.Web.WebPages.Administration.dll* 어셈블리입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-264">This request downloads all of the resource strings in the *System.Web.WebPages.Administration.dll* assembly.</span></span> <span data-ttu-id="9d502-265">(도 정적 콘텐츠를 제공할 수 없습니다) 포함 된 리소스를 모두 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-265">All of the embedded resources (even those that are not intended to be served as static content) are downloaded.</span></span> <span data-ttu-id="9d502-266">포함된 리소스에 중요 한 정보를 포함 하는 경우 보안 위험을 나타낼 수 있습니다이 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-266">If the embedded resources contain sensitive information, this can represent a security risk.</span></span> 
> 
> <span data-ttu-id="9d502-267">**해결 방법** </span><span class="sxs-lookup"><span data-stu-id="9d502-267">**Workaround** </span></span>  
> <span data-ttu-id="9d502-268">만드는 경우는 **ApplicationPart** 개체가 포함된 된 리소스가 연결 된 선택 되어 있는지 확인 합니다 **ApplicationPart** 개체의 어셈블리에 중요 한 정보가 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-268">If you create an **ApplicationPart** object, make sure that the embedded resources associated with that **ApplicationPart** object's assembly do not contain sensitive information.</span></span>


<a id="Known_Issues_WebMatrix"></a>

### <a name="webmatrix"></a><span data-ttu-id="9d502-269">WebMatrix</span><span class="sxs-lookup"><span data-stu-id="9d502-269">WebMatrix</span></span>

> [!NOTE]
> <span data-ttu-id="9d502-270">WebMatrix에 대 한 설치 문제에 대 한 정보를 참조 하세요 [WebMatrix 설치 문제](#Known_Issues_Installation) 이 문서의 앞부분에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-270">For information about installation issues for WebMatrix, see [WebMatrix Installation Issues](#Known_Issues_Installation) earlier in this document.</span></span>


<span data-ttu-id="9d502-271">문서의이 섹션에서는 WebMatrix 개발 환경에 대 한 알려진된 문제를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-271">This section of the document describes known issues for the WebMatrix development environment.</span></span>

#### <a name="issue-changes-in-the-username-or-password-of-a-database-connection-string-in-a-webconfig-file-are-not-reflected-in-the-databases-workspace"></a><span data-ttu-id="9d502-272">문제: 사용자 이름 또는 web.config 파일에서 데이터베이스 연결 문자열의 암호 변경 내용은 데이터베이스 작업 영역에 반영 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-272">Issue: Changes in the username or password of a database connection string in a web.config file are not reflected in the Databases workspace</span></span>

> <span data-ttu-id="9d502-273">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-273">**Workaround**</span></span>  
> 
> 1. <span data-ttu-id="9d502-274">에 *web.config* 파일, 연결 문자열에 데이터베이스 이름을 변경 (예를 들어를 "1" 추가).</span><span class="sxs-lookup"><span data-stu-id="9d502-274">In the *web.config* file, change the database name in the connection string (for example, add "1" to it).</span></span>
> 2. <span data-ttu-id="9d502-275">저장 된 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-275">Save the *web.config* file.</span></span>
> 3. <span data-ttu-id="9d502-276">클릭 **데이터베이스** 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-276">Click **Databases** and refresh.</span></span>
> 4. <span data-ttu-id="9d502-277">연결 문자열에 데이터베이스 이름을 변경 합니다 *web.config* 에 파일을 다시 원래 데이터베이스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-277">Change the database name in the connection string in the *web.config* file back to the original database name.</span></span>
> 5. <span data-ttu-id="9d502-278">저장 된 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-278">Save the *web.config* file.</span></span>
> 6. <span data-ttu-id="9d502-279">클릭 **데이터베이스** 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-279">Click **Databases** and refresh.</span></span>


#### <a name="issue-folders-created-by-webmatrix-cannot-be-deleted"></a><span data-ttu-id="9d502-280">문제: WebMatrix에서 생성 된 폴더를 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-280">Issue: Folders created by WebMatrix cannot be deleted</span></span>

> <span data-ttu-id="9d502-281">WebMatrix 상승 된 권한을 사용 하 여 실행 중인 경우 (즉, WebMatrix를 사용 하 여 시작 하는 **관리자 권한으로 실행** Windows에서 옵션), Windows 탐색기를 사용 하 여 WebMatrix에서 생성 되는 폴더를 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-281">If WebMatrix is running using elevated permissions (that is, you started WebMatrix using the **Run as Administrator** option in Windows), folders that are created by WebMatrix cannot be deleted using Windows Explorer.</span></span>
> 
> <span data-ttu-id="9d502-282">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-282">**Workaround**</span></span>  
> <span data-ttu-id="9d502-283">상승 된 권한을 사용 하 여 Windows 탐색기를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-283">Run Windows Explorer using elevated permissions.</span></span> <span data-ttu-id="9d502-284">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-284">Follow these steps:</span></span>  
> 
> 1. <span data-ttu-id="9d502-285">Windows, 클릭 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-285">In Windows, click **Start**.</span></span>
> 2. <span data-ttu-id="9d502-286">"Windows Explorer"를 입력 하 고 항목을 마우스 오른쪽 단추로 클릭 **Windows 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-286">Enter "Windows Explorer" and right-click the entry for **Windows Explorer**.</span></span>
> 3. <span data-ttu-id="9d502-287">클릭 **관리자 권한으로 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-287">Click **Run as Administrator**.</span></span> <span data-ttu-id="9d502-288">폴더를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-288">You can then delete the folders.</span></span>


#### <a name="issue-webmatrix-10-is-unable-to-perform-certain-tasks-that-require-elevation"></a><span data-ttu-id="9d502-289">문제: WebMatrix 1.0 권한 상승을 요구 하는 특정 작업을 수행할 수 없습니다</span><span class="sxs-lookup"><span data-stu-id="9d502-289">Issue: WebMatrix 1.0 is unable to perform certain tasks that require elevation</span></span>

> <span data-ttu-id="9d502-290">WebMatrix 1.0가 다음과 같은 상황에서 추가 구성 요소를 설치 하는 등의 권한 상승 해야 하는 특정 작업을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-290">WebMatrix 1.0 is unable to perform certain tasks that require elevation, such as installing additional components in the following situations:</span></span>
> 
> - <span data-ttu-id="9d502-291">Windows Vista 또는 Windows 7에서 관리자 권한이 없는 계정으로 로그온 한 사용자 계정 컨트롤 (UAC)을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-291">On Windows Vista or Windows 7, you are logged in with an account that does not have administrative privileges and User Account Control (UAC) is disabled.</span></span>
> - <span data-ttu-id="9d502-292">Microsoft Windows XP 또는 Microsoft Windows Server 2003을 사용 하는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-292">You are using Microsoft Windows XP or Microsoft Windows Server 2003.</span></span>
> 
> <span data-ttu-id="9d502-293">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-293">**Workaround**</span></span>  
> <span data-ttu-id="9d502-294">WebMatrix 1.0에서 대부분의 작업에는 관리 권한이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-294">Most tasks in WebMatrix 1.0 do not require administrative permission.</span></span> <span data-ttu-id="9d502-295">이러한 조작자에 대 한 다음이 단계를 수행 또는 관리자로 서 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-295">For those that do, you can perform the operation as an administrator, or follow these steps:</span></span>
> 
> - <span data-ttu-id="9d502-296">Windows Vista 또는 Windows 7에서 UAC를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-296">On Windows Vista or Windows 7, enable UAC.</span></span>
> - <span data-ttu-id="9d502-297">Windows XP에서 Administrators 보안 그룹에 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-297">On Windows XP, add the user to the Administrators security group.</span></span>


#### <a name="issue-site-from-web-gallery-is-disabled"></a><span data-ttu-id="9d502-298">문제: "웹 갤러리에서 사이트"을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-298">Issue: "Site from Web Gallery" is disabled</span></span>

> <span data-ttu-id="9d502-299">합니다 **웹 갤러리에서 사이트** 웹 플랫폼 설치 관리자 3.0이 설치 되지 않은 경우 옵션은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-299">The **Site from Web Gallery** option is disabled if the Web Platform Installer 3.0 is not installed.</span></span>
> 
> <span data-ttu-id="9d502-300">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-300">**Workaround**</span></span>  
> <span data-ttu-id="9d502-301">설치 합니다 [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-301">Install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span>


#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a><span data-ttu-id="9d502-302">문제: Google Chrome 실행 옵션으로 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-302">Issue: Google Chrome is not available as a Run option</span></span>

> <span data-ttu-id="9d502-303">Google Chrome 브라우저에서 목록에 표시 되지 않습니다 **실행할** 에 **홈** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-303">Google Chrome is not displayed in the list of browsers under **Run** on the **Home** tab.</span></span>
> 
> <span data-ttu-id="9d502-304">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-304">**Workaround**</span></span>  
> <span data-ttu-id="9d502-305">Google Chrome의 일부 버전에서는 등록 하지 자체 올바르게 Windows의 기본 프로그램 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-305">Some versions of Google Chrome do not register themselves correctly with the Default Programs feature in Windows.</span></span> <span data-ttu-id="9d502-306">대 안으로, Google Chrome을 시작 합니다 *사용자 지정 및 Google Chrome 컨트롤* 메뉴에서 클릭 *옵션*를 클릭 하 고 *확인 Google Chrome 기본 브라우저*.</span><span class="sxs-lookup"><span data-stu-id="9d502-306">As a workaround, start Google Chrome, click the *Customize and control Google Chrome* menu, click *Options*, and then click *Make Google Chrome my default browser*.</span></span>


#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a><span data-ttu-id="9d502-307">문제: "외래 키" 대화 상자를 허용 하지 않습니다는 기본 키를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-307">Issue: The "Foreign Key" dialog box doesn't allow entering a primary key</span></span>

> <span data-ttu-id="9d502-308">합니다 **외래 키** 대화 상자 기본 키 테이블에서 기본 키 이름을 입력할 수를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-308">The **Foreign Key** dialog box does not allow you to enter the primary key name from the primary key table.</span></span>
> 
> <span data-ttu-id="9d502-309">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-309">**Workaround**</span></span>  
> <span data-ttu-id="9d502-310">이 의도적입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-310">This is intentional.</span></span> <span data-ttu-id="9d502-311">기본 키 테이블에서 기본 키의 이름을 입력할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-311">You do not need to enter the name of the primary key from the primary key table.</span></span>


#### <a name="issue-intellisense-is-not-available-in-webmatrix-for-razor-syntax-c-or-visual-basic"></a><span data-ttu-id="9d502-312">문제: IntelliSense는 Razor 구문, C# 또는 Visual Basic WebMatrix에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-312">Issue: IntelliSense is not available in WebMatrix for Razor syntax, C#, or Visual Basic</span></span>

> <span data-ttu-id="9d502-313">HTML 및 CSS WebMatrix에서 IntelliSense가 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-313">IntelliSense is supported in WebMatrix for HTML and CSS.</span></span> <span data-ttu-id="9d502-314">그러나 다른 언어에 대해 사용할 수 없는 경우</span><span class="sxs-lookup"><span data-stu-id="9d502-314">However, it is not available for other languages.</span></span> 
> 
> <span data-ttu-id="9d502-315">**해결 방법** </span><span class="sxs-lookup"><span data-stu-id="9d502-315">**Workaround** </span></span>  
> <span data-ttu-id="9d502-316">없음</span><span class="sxs-lookup"><span data-stu-id="9d502-316">None.</span></span>


#### <a name="issue-intellisense-for-html-and-css-suggests-elements-that-are-not-contextually-appropriate"></a><span data-ttu-id="9d502-317">문제: HTML 및 CSS에 대 한 IntelliSense 제안 컨텍스트에 적절 하지 않은 요소</span><span class="sxs-lookup"><span data-stu-id="9d502-317">Issue: IntelliSense for HTML and CSS suggests elements that are not contextually appropriate</span></span>

> <span data-ttu-id="9d502-318">WebMatrix의 태그에 대 한 IntelliSense 지원 사용 하 여 HTML 합니다 [XHTML 1.0 Transitional 스키마](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional) 하 고 CSS를 사용 하는 [CSS 2.1 스키마](http://www.w3.org/TR/CSS2/).</span><span class="sxs-lookup"><span data-stu-id="9d502-318">IntelliSense for markup in WebMatrix supports HTML using the [XHTML 1.0 Transitional schema](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional) and CSS using the [CSS 2.1 schema](http://www.w3.org/TR/CSS2/).</span></span> <span data-ttu-id="9d502-319">IntelliSense를 이러한 특정 스키마를 기반으로 하기 때문에 특정 태그, 특성 또는 속성 수 제안 하는 현재 페이지 또는 스타일 정의에 적합 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-319">Because IntelliSense is based on these specific schemas, certain tags, attributes, or properties might be suggested that are not appropriate for the current page or style definition.</span></span> <span data-ttu-id="9d502-320">HTML에 대 한 잘못 된 XHTML (예: 태그가 닫혀 있지 않은 경우)로 해석 될 수 있는 콘텐츠에 예기치 않은 제안 발생할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-320">For HTML, it can also lead to unexpected suggestions in content that might be interpreted as malformed XHTML (for example, when tags are not closed).</span></span> <span data-ttu-id="9d502-321">이 문제는 불완전 한 태그를 안에 삽입 지점이 있을 경우 더 두드러질 수 있습니다. 이 경우 IntelliSense 태그를 새 열을 제안 하거나 다른 잘못 된 제안 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-321">This issue might be more noticeable if the insertion point is inside an incomplete tag; in that case, IntelliSense might suggest new opening tags or offer other incorrect suggestions.</span></span> 
> 
> <span data-ttu-id="9d502-322">**해결 방법** </span><span class="sxs-lookup"><span data-stu-id="9d502-322">**Workaround** </span></span>  
> <span data-ttu-id="9d502-323">HTML, 잘 구성 된, 완전 한 XHTML 페이지 내에서 작업 하는 것이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-323">For HTML, make sure that you are working within a well-formed, complete XHTML page.</span></span> <span data-ttu-id="9d502-324">CSS에 대 한 해결 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-324">For CSS, there is no workaround.</span></span>


#### <a name="issue-intellisense-is-not-invoked-while-you-type"></a><span data-ttu-id="9d502-325">문제: 입력할 때 IntelliSense가 호출 되지 않는다</span><span class="sxs-lookup"><span data-stu-id="9d502-325">Issue: IntelliSense is not invoked while you type</span></span>

> <span data-ttu-id="9d502-326">때때로 HTML 또는 CSS 편집기에서 입력 되는 IntelliSense 호출 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-326">At times, IntelliSense might not be invoked as HTML or CSS is being entered in the editor.</span></span> <span data-ttu-id="9d502-327">특히,이 파일의 끝 또는 다른 요소 옆에 있는 직접 삽입 지점이 있을 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-327">In particular, this might happen when the insertion point is directly next to another element or at the end of a file.</span></span> 
> 
> <span data-ttu-id="9d502-328">**해결 방법** </span><span class="sxs-lookup"><span data-stu-id="9d502-328">**Workaround** </span></span>  
> <span data-ttu-id="9d502-329">삽입 포인터 주위 공백 인지 삽입 지점이 되 고 있지 않음을 파일의 끝에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-329">Make sure that there is whitespace around the insertion point and that the insertion point is not at the end of a file.</span></span> <span data-ttu-id="9d502-330">또한 Ctrl + 스페이스바를 눌러 IntelliSense를 수동으로 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-330">You can also invoke IntelliSense manually by pressing Ctrl+Space.</span></span>


#### <a name="issue-no-ui-is-available-for-disabling-intellisense"></a><span data-ttu-id="9d502-331">문제: UI 수 IntelliSense를 사용 하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="9d502-331">Issue: No UI is available for disabling IntelliSense</span></span>

> <span data-ttu-id="9d502-332">WebMatrix 1.0 IntelliSense를 사용 하지 않도록 설정 하는 것에 대 한 UI 또는 제스처를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-332">WebMatrix 1.0 provides no UI or gesture for disabling IntelliSense.</span></span> 
> 
> <span data-ttu-id="9d502-333">**해결 방법** </span><span class="sxs-lookup"><span data-stu-id="9d502-333">**Workaround** </span></span>  
> <span data-ttu-id="9d502-334">IntelliSense를 사용 하지 않도록 설정 하는 스위치를 포함 하는 다음 명령을 사용 하 여 WebMatrix를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-334">Start WebMatrix using the following command, which includes a switch that disables IntelliSense:</span></span>  
>   
> `WebMatrix.exe #ExecuteCommand# EditorIntelliSense off`


<a id="Known_Issues_IISExpress"></a>
### <a name="iis-express"></a><span data-ttu-id="9d502-335">IIS Express</span><span class="sxs-lookup"><span data-stu-id="9d502-335">IIS Express</span></span>

<span data-ttu-id="9d502-336">IIS Express는 다음 URL에서 사용할 수 있는 추가 정보 파일을 사용 하는 자체에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-336">IIS Express has its own readme file, which is available at the following URL:</span></span>

[<span data-ttu-id="9d502-337">https://go.microsoft.com/fwlink/?LinkID=207675&ampclcid = 0x409</span><span class="sxs-lookup"><span data-stu-id="9d502-337">https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409</span></span>](https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409)

<a id="Known_Issues_SQLServerCompact"></a>

### <a name="sql-server-compact"></a><span data-ttu-id="9d502-338">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="9d502-338">SQL Server Compact</span></span>

<span data-ttu-id="9d502-339">SQL Server Compact에 다음 URL에서 사용할 수 있는 추가 정보 파일을 사용 하는 자체 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-339">SQL Server Compact has its own readme file, which is available at the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=208545](https://go.microsoft.com/fwlink/?LinkID=208545&amp;clcid=0x409)

<span data-ttu-id="9d502-340">WebMatrix의 일부로 SQL Server Compact 설치와 관련 된 문제에 대 한 내용은 [WebMatrix 설치 문제](#Known_Issues_Installation) 이 문서의 앞부분에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-340">For information about issues that involve installing SQL Server Compact as part of WebMatrix, see [WebMatrix Installation Issues](#Known_Issues_Installation) earlier in this document.</span></span>

### <a id="Known_Issues_Installing_Applications"></a>  <span data-ttu-id="9d502-341">응용 프로그램 설치</span><span class="sxs-lookup"><span data-stu-id="9d502-341">Installing Applications</span></span>

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a><span data-ttu-id="9d502-342">문제: 응용 프로그램을 설치할 수 시간이 오래 걸릴 경우 사용자의 내 문서 폴더는 네트워크 공유로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-342">Issue: Installing an application can take a long time if the user's My Documents folder is redirected to a network share</span></span>

> <span data-ttu-id="9d502-343">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-343">**Workaround**</span></span>  
> <span data-ttu-id="9d502-344">없음</span><span class="sxs-lookup"><span data-stu-id="9d502-344">None.</span></span> <span data-ttu-id="9d502-345">응용 프로그램을 설치 하는 데 소요 되지만 제대로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-345">The application might take a while to install, but will install correctly.</span></span>


### <a id="Known_Issues_Publishing_Applications"></a>  <span data-ttu-id="9d502-346">응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="9d502-346">Publishing Applications</span></span>

#### <a name="issue-required-permissions-cannot-be-acquired-error-when-publishing-a-sql-compact-database"></a><span data-ttu-id="9d502-347">문제: "는 데 필요한 사용 권한을 가져올 수 없습니다" 오류 SQL Compact 데이터베이스를 게시 하는 경우</span><span class="sxs-lookup"><span data-stu-id="9d502-347">Issue: "Required permissions cannot be acquired" error when publishing a SQL Compact Database</span></span>

> <span data-ttu-id="9d502-348">WebMatrix에서는 보통 신뢰 수준 구성을 사용 하 여.NET Framework 버전 3.5 실행 하는 서버에 SQL Server Compact에 대 한 지원 이진 파일을 배포 완전히 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-348">WebMatrix does not fully support deploying supporting binaries for SQL Server Compact to a server that is running .NET Framework version 3.5 with a medium trust configuration.</span></span>
> 
> <span data-ttu-id="9d502-349">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-349">**Workaround**</span></span>  
> <span data-ttu-id="9d502-350">기본 해결 방법은 서버에서.NET Framework 4를 설치 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-350">The preferred workaround is to install the .NET Framework 4 on the server.</span></span> <span data-ttu-id="9d502-351">또는 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-351">Alternatively, do the following:</span></span>
> 
> 1. <span data-ttu-id="9d502-352">다음 요소를 추가 합니다 `SecurityClasses` 단원의 *웹\_MediumTrust.config* 파일:</span><span class="sxs-lookup"><span data-stu-id="9d502-352">Add the following elements to the `SecurityClasses` section in *Web\_MediumTrust.config* file:</span></span>
> 
>     [!code-html[Main](overview/samples/sample6.html)]
> 2. <span data-ttu-id="9d502-353">만들 새 권한 집합는 *웹\_MediumTrust.config* 다음 필요한 권한이 있는 파일:</span><span class="sxs-lookup"><span data-stu-id="9d502-353">Create a new permission set in the *Web\_MediumTrust.config* file with the following required permissions:</span></span>
> 
>     [!code-html[Main](overview/samples/sample7.html)]
> 3. <span data-ttu-id="9d502-354">다음 요소에 배치 하 여 SQL Server Compact로 설정 된 사용 권한을 적용 합니다 *웹\_MediumTrust.config* 파일:</span><span class="sxs-lookup"><span data-stu-id="9d502-354">Apply the permission set to SQL Server Compact by putting the following elements in the *Web\_MediumTrust.config* file:</span></span>
> 
>     [!code-html[Main](overview/samples/sample8.html)]


#### <a name="issue-gallery-and-phpbb-web-applications-display-a-service-is-unavailable-error-after-publishing"></a><span data-ttu-id="9d502-355">문제: 웹 응용 프로그램 갤러리 및 PhpBB "서비스를 사용할 수 없습니다." 오류를 게시 한 후 표시</span><span class="sxs-lookup"><span data-stu-id="9d502-355">Issue: Gallery and PhpBB web applications display a "Service is unavailable" error after publishing</span></span>

> <span data-ttu-id="9d502-356">상황에 따라 응용 프로그램을 게시 하면 "서비스를 사용할 수 없습니다." 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-356">Under some circumstances, publishing an application causes a "service is unavailable" error.</span></span>
> 
> <span data-ttu-id="9d502-357">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-357">**Workaround**</span></span>  
> <span data-ttu-id="9d502-358">WebMatrix에서 백슬래시를 추가 (\) 에서 서버 이름의 끝에는 **게시 설정** 창 및 응용 프로그램을 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-358">In WebMatrix, add a backslash (\) to the end of the server name in the **Publish Settings** window and then publish the application again.</span></span>


#### <a name="issue-moodle-website-layout-and-links-are-broken-after-publishing"></a><span data-ttu-id="9d502-359">문제: Moodle 웹 사이트 레이아웃 및 링크는 끊어진 게시 후</span><span class="sxs-lookup"><span data-stu-id="9d502-359">Issue: Moodle website layout and links are broken after publishing</span></span>

> <span data-ttu-id="9d502-360">Moodle은 응용 프로그램을 게시 한 후 응용 프로그램이 제대로 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-360">After you publish a Moodle application, the application does not work correctly.</span></span>
> 
> <span data-ttu-id="9d502-361">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-361">**Workaround**</span></span>  
> <span data-ttu-id="9d502-362">WebMatrix에서의 끝에 슬래시 (/)를 추가 합니다 **사이트 이름** 필드를 **게시 설정** 창 한 다음 응용 프로그램을 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-362">In WebMatrix, add a slash (/) to the end of the **Site Name** field in the **Publish Settings** window and then publish the application again.</span></span>


#### <a name="issue-publishing-nopcommerce-fails-with-a-database-error"></a><span data-ttu-id="9d502-363">문제: 데이터베이스 오류로 인해 실패할 nopCommerce 게시</span><span class="sxs-lookup"><span data-stu-id="9d502-363">Issue: Publishing nopCommerce fails with a database error</span></span>

> <span data-ttu-id="9d502-364">게시 nopCommerce는 실패 하 고 같은 데이터베이스 오류를 보고 "를 nop 삽입\_로그 table이 실패 했습니다."</span><span class="sxs-lookup"><span data-stu-id="9d502-364">Publishing nopCommerce fails and reports a database error like "Insert into the nop\_log table failed."</span></span>
> 
> <span data-ttu-id="9d502-365">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-365">**Workaround**</span></span>  
> 
> 1. <span data-ttu-id="9d502-366">WebMatrix에서 클릭 **실행** nopCommerce 로컬로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-366">In WebMatrix, click **Run** to launch nopCommerce locally.</span></span>
> 2. <span data-ttu-id="9d502-367">관리 페이지에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-367">Log into the administration page.</span></span>
> 3. <span data-ttu-id="9d502-368">클릭 합니다 **시스템** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="9d502-368">Click the **System** menu.</span></span>
> 4. <span data-ttu-id="9d502-369">클릭 합니다 **로그** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-369">Click the **Log** option.</span></span>
> 5. <span data-ttu-id="9d502-370">클릭 합니다 **로그 지우기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-370">Click the **Clear Log** button.</span></span>
> 6. <span data-ttu-id="9d502-371">NopCommerce를 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-371">Publish nopCommerce again.</span></span>


#### <a name="issue-silverstripe-cms-displays-a-http-500-php-fcgi-error-when-you-download-a-published-site"></a><span data-ttu-id="9d502-372">문제: Silverstripe CMS 오류를 표시 "HTTP 500 PHP FCGI" 게시 된 사이트를 다운로드 하는 경우</span><span class="sxs-lookup"><span data-stu-id="9d502-372">Issue: Silverstripe CMS displays a "HTTP 500 PHP FCGI Error" when you download a published site</span></span>

> <span data-ttu-id="9d502-373">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-373">**Workaround**</span></span>  
> <span data-ttu-id="9d502-374">클릭 한 후 **다운로드 사이트를 게시**, 건너뛰기 `silverstripe-cache/manifest_main` 에서 **게시 미리 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-374">After you click **Download published site**, skip `silverstripe-cache/manifest_main` in **Publish Preview**.</span></span> <span data-ttu-id="9d502-375">이 파일 캐싱 목적으로 사용 되 고 각 컴퓨터에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-375">This file is used for caching purposes and is specific to each computer.</span></span>


#### <a name="issue-subtext-displays-server-error-in--application-when-you-download-a-published-site"></a><span data-ttu-id="9d502-376">문제: Subtext 표시 "서버 오류 '/' 응용 프로그램 의" 게시 된 사이트를 다운로드 하는 경우</span><span class="sxs-lookup"><span data-stu-id="9d502-376">Issue: Subtext displays "Server Error in '/' Application" when you download a published site</span></span>

> <span data-ttu-id="9d502-377">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-377">**Workaround**</span></span>  
> <span data-ttu-id="9d502-378">사이트를 엽니다 *web.config* 파일 및 SQL Server 관리자 자격 증명 ("sa" 자격 증명)를 사용 하 여 사용자 ID 및 데이터베이스 연결 문자열에 암호를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-378">Open the site's *web.config* file and replace the user ID and password in the database connection string with the SQL Server administrator credentials (the "sa" credentials).</span></span>
> 
> <span data-ttu-id="9d502-379">또는 로그인 하는 사용자 계정에 부여 하려면 다음이 단계를 수행 `db_owner` 권한:</span><span class="sxs-lookup"><span data-stu-id="9d502-379">Alternatively, follow these steps in order to give the user account you are logged in with `db_owner` permissions:</span></span>
> 
> 1. <span data-ttu-id="9d502-380">웹 플랫폼 설치 관리자를 사용 하 여 SQL Server Management Studio를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-380">Install SQL Server Management Studio using the Web Platform Installer.</span></span>
> 2. <span data-ttu-id="9d502-381">로컬 SQL Server Express 인스턴스에 연결 (기본적으로 `.\SQLEXPRESS`).</span><span class="sxs-lookup"><span data-stu-id="9d502-381">Connect to the local SQL Server Express instance (by default, `.\SQLEXPRESS`).</span></span>
> 3. <span data-ttu-id="9d502-382">클릭 **데이터베이스** &gt; *[localSubtextDatabase]* &gt; **Security** &gt; **사용자** &gt; *[localSubtextUser*] (기본값은 `subtextuser`]를 마우스 오른쪽 단추로 클릭 하 고 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-382">Click **Databases** &gt; *[localSubtextDatabase]* &gt; **Security** &gt; **Users** &gt; *[localSubtextUser*] (default is `subtextuser`], right-click, and click **Properties**.</span></span>
> 4. <span data-ttu-id="9d502-383">선택 **db\_소유자** 역할 멤버 자격 섹션에서입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-383">Select **db\_owner** in the role membership section.</span></span>


#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a><span data-ttu-id="9d502-384">문제: 사이트 "대상 URL" 필드는 http:// 또는 https://로 시작 하지 않는 경우 게시 한 후 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-384">Issue: Site might not work after publishing if the "Destination URL" field is not prefixed with http:// or https://</span></span>

> <span data-ttu-id="9d502-385">에 **게시 설정** 대화 상자에서 대상 URL로 시작 하지 않는 경우 `http://` 또는 `https://`, 사이트 배포 후 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-385">In the **Publishing Settings** dialog box, if the destination URL does not begin with `http://` or `https://`, the site might not work after deployment.</span></span>
> 
> <span data-ttu-id="9d502-386">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-386">**Workaround**</span></span>  
> <span data-ttu-id="9d502-387">있는지 확인 하는 사이트에서 대상 URL을 게시 하기 전에 합니다 **게시 설정** 대화 상자 시작 `http://` 또는 `https://`합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-387">Make sure that before you publish a site, the destination URL in the **Publish Settings** dialog box starts with `http://` or `https://`.</span></span>


#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a><span data-ttu-id="9d502-388">문제: MySQL 데이터베이스를 게시할 오류로 인해 실패 "데이터베이스를 게시 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-388">Issue: Publishing a MySQL database fails with the error "Failed to publish the database.</span></span> <span data-ttu-id="9d502-389">이 경우 발생할 수 있습니다 원격 데이터베이스에서 스크립트를 실행할 수 없습니다. "</span><span class="sxs-lookup"><span data-stu-id="9d502-389">This can happen if the remote database cannot run the script."</span></span>

> <span data-ttu-id="9d502-390">이 오류는 다양 한 이유로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-390">The error can occur for a number of reasons.</span></span> <span data-ttu-id="9d502-391">이 오류를 확인할 수 있습니다 하는 이유 중 하나 이며 경우 데이터베이스 스크립트 문자가 작은따옴표 (') u t F-8로 대상 MySQL 데이터베이스의 기본 문자 집합이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-391">One reason you can see this error is if the database script contains a single quotation character (') and the destination MySQL database's default character set is not to UTF-8.</span></span>
> 
> <span data-ttu-id="9d502-392">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-392">**Workaround**</span></span>  
> <span data-ttu-id="9d502-393">U t F-8로 원격 MySQL 데이터베이스에 대 한 기본 문자를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-393">Set the default character set for the remote MySQL database to UTF-8.</span></span>


#### <a name="issue-some-links-are-not-visible-in-dotnetnuke-after-publishing-or-downloading-the-site"></a><span data-ttu-id="9d502-394">문제: 일부 링크에에서 표시 되지 않습니다 DotNetNuke 게시 하거나 사이트를 다운로드 한 후</span><span class="sxs-lookup"><span data-stu-id="9d502-394">Issue: Some links are not visible in DotNetNuke after publishing or downloading the site</span></span>

> <span data-ttu-id="9d502-395">게시 하거나 다운로드 DotNetNuke 사이트, 사이트에 표시할 새 링크의 캐시의 선택을 취소 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-395">If you publish or download a DotNetNuke site, you might need to clear the cache to get the new links to appear on the site.</span></span>
> 
> <span data-ttu-id="9d502-396">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-396">**Workaround**</span></span>
> 
> 1. <span data-ttu-id="9d502-397">"Host"로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-397">Log in as "Host".</span></span>
> 2. <span data-ttu-id="9d502-398">호스트 메뉴로 이동 하 고 선택 **호스트 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-398">Go to the host menu and select **Host Settings**.</span></span>
> 3. <span data-ttu-id="9d502-399">아래로 스크롤하여 **고급 설정**를 확장 하 고 **성능 설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-399">Scroll down and under **Advanced Settings**, expand **Performance Settings**.</span></span>
> 4. <span data-ttu-id="9d502-400">클릭 합니다 **캐시 지우기** 페이지에 대 한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-400">Click the **Clear Cache** link for pages.</span></span>
> 5. <span data-ttu-id="9d502-401">페이지 아래쪽으로 이동한 다음 응용 프로그램을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-401">Go to the bottom of the page and restart the application.</span></span>


#### <a name="issue-some-links-in-atomsite-are-broken-after-you-download-a-published-site"></a><span data-ttu-id="9d502-402">문제: 게시 된 사이트를 다운로드 한 후 인 AtomSite의 일부 링크 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-402">Issue: Some links in AtomSite are broken after you download a published site</span></span>

> <span data-ttu-id="9d502-403">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-403">**Workaround**</span></span>  
> <span data-ttu-id="9d502-404">*service.config* 파일인 *users.config* 파일 및 모든 *.xml* 파일을 대체 URL 문자열 (예를 들어, `http://myhost.com/atomsite`)을 로컬 (예를 들어 `http://localhost:1239`).</span><span class="sxs-lookup"><span data-stu-id="9d502-404">In the *service.config* file, *users.config* file, and all *.xml* files, replace the URL string (for example, `http://myhost.com/atomsite`) with the local one (for example, `http://localhost:1239`).</span></span>


#### <a name="issue-mysql-based-applications-like-wordpress-fail-to-publish-and-report-a-database-error"></a><span data-ttu-id="9d502-405">문제: WordPress와 같은 MySQL 기반 응용 프로그램을 게시 하 고 데이터베이스 오류를 보고 실패</span><span class="sxs-lookup"><span data-stu-id="9d502-405">Issue: MySQL-based applications like WordPress fail to publish and report a database error</span></span>

> <span data-ttu-id="9d502-406">기본적으로 WebMatrix에서 utf-8 문자 집합을 사용 하 여 MySQL을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-406">By default, WebMatrix installs MySQL with the UTF-8 character set.</span></span> <span data-ttu-id="9d502-407">직접 MySQL을 설치 하 고 문자 집합을 u t F-8 없는 경우 (예를 들어 인 Latin1) 데이터베이스에 대 한 게시 프로세스가 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-407">If you install MySQL on your own, and the character set is not UTF-8 (for example, it is Latin1), the publish process for databases might fail.</span></span>
> 
> <span data-ttu-id="9d502-408">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-408">**Workaround**</span></span>
> 
> 1. <span data-ttu-id="9d502-409">U t F-8로 MySQL의 문자 집합을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-409">Change the character set for MySQL to UTF-8.</span></span> <span data-ttu-id="9d502-410">(세부 정보를 참조 하세요 [서버 문자 집합 및 데이터 정렬](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html) MySQL 웹 사이트의.)</span><span class="sxs-lookup"><span data-stu-id="9d502-410">(For details, see [Server Character Set and Collation](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html) on the MySQL website.)</span></span>
> 2. <span data-ttu-id="9d502-411">응용 프로그램을 다시 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-411">Reinstall the application.</span></span>
> 3. <span data-ttu-id="9d502-412">응용 프로그램을 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-412">Republish the application.</span></span>


#### <a name="issue-download-published-site-fails-for-applications-that-have-browser-based-setup"></a><span data-ttu-id="9d502-413">문제: "다운로드 사이트를 게시 하는 데 사용" 응용 프로그램을 브라우저 기반 설치에 대 한 실패</span><span class="sxs-lookup"><span data-stu-id="9d502-413">Issue: "Download published site" fails for applications that have browser-based setup</span></span>

> <span data-ttu-id="9d502-414">일부 응용 프로그램 (예: Kentico CMS) 데이터베이스 만들기 같은 설치 후 설치를 수행 하기 위해 브라우저에서 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-414">Some applications (for example, Kentico CMS) require you to launch them in the browser in order to perform post-installation setup such as creating a database.</span></span> <span data-ttu-id="9d502-415">다음과 같은 브라우저 기반 설치를 완료 하지 않고 응용 프로그램을 게시 하는 경우 원격 서버에서 같은 사이트를 다운로드 하려는 시도 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-415">If you publish an application like this without completing the browser-based setup, attempting to download the same site from a remote server will fail.</span></span>
> 
> <span data-ttu-id="9d502-416">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-416">**Workaround**</span></span>  
> <span data-ttu-id="9d502-417">사이트를 게시 하기 전에 브라우저 기반 설치를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-417">Finish browser-based setup before publishing the site.</span></span>


#### <a name="issue-download-published-site-fails-with-a-database-error-for-dotnetnuke-and-kooboo-cms"></a><span data-ttu-id="9d502-418">문제: "다운로드 사이트를 게시 하는 데 사용" DotNetNuke 및 Kooboo CMS에 대 한 데이터베이스 오류와 함께 실패</span><span class="sxs-lookup"><span data-stu-id="9d502-418">Issue: "Download published site" fails with a database error for DotNetNuke and Kooboo CMS</span></span>

> <span data-ttu-id="9d502-419">서버에서 응용 프로그램을 다운로드 하려는 경우 및 관리자 자격 증명에서 데이터베이스 연결 문자열에는 **게시 설정** 대화 상자에서 게시 로그에 다음 오류가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-419">If you try to download an application from a server and you have administrator credentials in the database connection string in the **Publish Settings** dialog, you might see the following error in the publish log:</span></span>
> 
> [!code-console[Main](overview/samples/sample9.cmd)]
> 
> <span data-ttu-id="9d502-420">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="9d502-420">**Workaround**</span></span>  
> <span data-ttu-id="9d502-421">실제 환경인 경우 사이트를 다시 게시 (또는 게시) 데이터베이스에 대 한 비관리자 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-421">If practical, republish the site (or have it published) using non-administrator credentials for the database.</span></span>


<a id="More_Info"></a>

## <a name="for-more-information"></a><span data-ttu-id="9d502-422">자세한 내용</span><span class="sxs-lookup"><span data-stu-id="9d502-422">For More Information</span></span>

<span data-ttu-id="9d502-423">WebMatrix 1.0에 대 한 자세한 내용은 다음 웹 사이트를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="9d502-423">For more information about WebMatrix 1.0, see the following websites:</span></span>

- [<span data-ttu-id="9d502-424">IIS.net</span><span class="sxs-lookup"><span data-stu-id="9d502-424">IIS.net</span></span>](http://iis.net/)
- [<span data-ttu-id="9d502-425">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9d502-425">ASP.NET</span></span>](https://asp.net/webmatrix)
- [<span data-ttu-id="9d502-426">Microsoft.com/web</span><span class="sxs-lookup"><span data-stu-id="9d502-426">Microsoft.com/web</span></span>](https://www.microsoft.com/web)

<span data-ttu-id="9d502-427">© 2011 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="9d502-427">© 2011 Microsoft Corporation.</span></span> <span data-ttu-id="9d502-428">All Rights Reserved.</span><span class="sxs-lookup"><span data-stu-id="9d502-428">All Rights Reserved.</span></span> <span data-ttu-id="9d502-429">[사용 약관](https://msdn.microsoft.cos/cc300389.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d502-429">[Terms of Use](https://msdn.microsoft.cos/cc300389.aspx).</span></span>
