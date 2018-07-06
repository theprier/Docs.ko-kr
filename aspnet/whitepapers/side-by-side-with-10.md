---
uid: whitepapers/side-by-side-with-10
title: .NET Framework 1.0 및 1.1의 ASP.NET-Side-by-side 실행 | Microsoft Docs
author: rick-anderson
description: 이 백서는 타이밍의 버전 중 하나에서 실행 되도록 ASP.NET 웹 응용 프로그램 수 있도록 컴퓨터에.NET 1.0와.NET 1.1을 설치 하는 방법에 설명 하는 중...
ms.author: aspnetcontent
ms.date: 02/10/2010
ms.assetid: bdea2003-e964-4db5-9092-d56cc7560616
msc.legacyurl: /whitepapers/side-by-side-with-10
msc.type: content
ms.openlocfilehash: 1018845e3d2c6603732bfbbde78f4a9183e49d5d
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37808397"
---
<a name="aspnet-side-by-side-execution-of-net-framework-10-and-11"></a><span data-ttu-id="43cfd-103">.NET Framework 1.0 및 1.1의 ASP.NET-Side-by-side 실행</span><span class="sxs-lookup"><span data-stu-id="43cfd-103">ASP.NET Side-by-Side Execution of .NET Framework 1.0 and 1.1</span></span>
====================
> <span data-ttu-id="43cfd-104">이 백서에는 ASP.NET 웹 응용 프로그램 프레임 워크의 버전 중 하나에서 실행할 수 있도록 컴퓨터에.NET 1.0와.NET 1.1을 설치 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-104">This whitepaper describes how to install both .NET 1.0 and .NET 1.1 on your machine, allowing an ASP.NET Web application to run on either version of the framework.</span></span>
> 
> <span data-ttu-id="43cfd-105">ASP.NET 1.0 및 ASP.NET 1.1에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-105">Applies to ASP.NET 1.0 and ASP.NET 1.1.</span></span>


<span data-ttu-id="43cfd-106">ASP.NET에서 실행 되 고 함께 동일한 컴퓨터에 설치 되어 있지만 다른 버전의.NET Framework를 사용 하는 경우 응용 프로그램 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-106">In ASP.NET, applications are said to be running side by side when they are installed on the same computer, but use different versions of the .NET Framework.</span></span> <span data-ttu-id="43cfd-107">다음 항목에서는-병렬 실행에 대 한 ASP.NET 응용 프로그램을 구성 하는 방법에 설명 하 고 하는 자세한 단계를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-107">The following topic describes how to configure ASP.NET applications for side-by-side execution and provides detailed steps to:</span></span>

- [<span data-ttu-id="43cfd-108">.NET Framework 버전 1.0 설치 하는 동안 웹 응용 프로그램의 매핑을 유지 관리</span><span class="sxs-lookup"><span data-stu-id="43cfd-108">Maintain your Web application's mapping to .NET Framework version 1.0 during installation</span></span>](#1)
- [<span data-ttu-id="43cfd-109">특정 버전.NET Framework의 웹 응용 프로그램 맵</span><span class="sxs-lookup"><span data-stu-id="43cfd-109">Map a Web application to a specific version of the .NET Framework</span></span>](#2)
- [<span data-ttu-id="43cfd-110">웹 사이트를 사용 하는.NET Framework의 버전을 확인</span><span class="sxs-lookup"><span data-stu-id="43cfd-110">Find the version of the .NET Framework that a Web site is using</span></span>](#3)

<span data-ttu-id="43cfd-111">일반적으로 구성 요소 또는 응용 프로그램을 컴퓨터에 업데이트 되 면 이전 버전은 제거 되 고 최신 버전으로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-111">Traditionally, when a component or application is updated on a computer, the older version is removed and replaced with the newer version.</span></span> <span data-ttu-id="43cfd-112">새 버전이 이전 버전과 호환 되지 않으면 일반적으로 응용 프로그램 구성 요소 또는 응용 프로그램 사용 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-112">If the new version is not compatible with the previous version, this usually breaks other applications that use the component or application.</span></span> <span data-ttu-id="43cfd-113">.NET Framework 어셈블리 또는 동시에 동일한 컴퓨터에 설치할 응용 프로그램의 여러 버전을 허용 하는-병렬 실행에 대 한 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-113">The .NET Framework provides support for side-by-side execution, which allows multiple versions of an assembly or application to be installed on the same computer at the same time.</span></span> <span data-ttu-id="43cfd-114">여러 버전이 동시에 설치할 수 있으므로 관리 되는 응용 프로그램 다른 버전을 사용 하는 응용 프로그램에 영향을 주지 않고 사용할 버전을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-114">Because multiple versions can be installed simultaneously, managed applications can select which version to use without affecting applications that use a different version.</span></span>

<span data-ttu-id="43cfd-115">기본적으로.NET Framework 버전 1.1 설치 하는 동안 기존 ASP.NET 응용 프로그램 모두 자동으로 재구성 됩니다.NET Framework의 최신 버전을 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-115">By default, during the installation of the .NET Framework version 1.1, all existing ASP.NET applications are automatically reconfigured to use the latest version of the .NET Framework.</span></span> <span data-ttu-id="43cfd-116">ASP.NET 응용 프로그램을.NET Framework 1.1을 기본값으로 하지 않으려면 클릭 [여기](#1) 를 설치 하는 동안이 방지 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-116">If you do not want your ASP.NET applications to default to .NET Framework 1.1, click [here](#1) to learn how to prevent this during installation.</span></span>

<span data-ttu-id="43cfd-117">.NET Framework 1.1로 웹 서버를 업데이트 하 고 하나 이상의 웹 응용 프로그램에.NET Framework 1.0을 실행 하는 경우 인터넷 정보 서비스 (IIS) 스크립트 맵을 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-117">If you update your Web server to .NET Framework 1.1 and want one or more Web applications to run .NET Framework 1.0, you need to update the Internet Information Services (IIS) Script Map.</span></span> <span data-ttu-id="43cfd-118">스크립트 매핑은 특정 웹 응용 프로그램을.NET Framework의 버전에 대 한.aspx 파일 확장명을 매핑하려 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-118">The script mapping is the mechanism to map the .aspx file extension for a specific Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="43cfd-119">클릭 [여기](#2) 에 특정 버전.NET Framework의 웹 응용 프로그램을 매핑하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-119">Click [here](#2) to learn how to map a Web application to a specific version of the .NET Framework.</span></span>

<span data-ttu-id="43cfd-120">인터넷 정보 관리자 또는 ASP.NET IIS 등록 도구를 사용할 수 있습니다 (Aspnet\_regiis.exe) 특정 웹 응용 프로그램을 실행 중인.NET Framework 버전을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-120">You can use the Internet Information Manger or the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe) to find which .NET Framework version is running a particular Web application.</span></span> <span data-ttu-id="43cfd-121">클릭 [여기](#3) 에 웹 사이트를 사용 하는.NET Framework의 버전을 확인 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-121">Click [here](#3) to learn how to find the version of the .NET Framework that a Web site is using.</span></span>

<span data-ttu-id="43cfd-122">각 버전의.NET Framework는 자체의 Machine.config 파일은.NET Framework 1.1로 마이그레이션하는 경우 하나의 가져오기 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-122">One import consideration when migrating to .NET Framework 1.1 is that each version of the .NET Framework uses its own Machine.config file.</span></span> <span data-ttu-id="43cfd-123">결과적으로, 웹 관리자가 변경할 경우 Machine.config 파일,.NET Framework 1.1 Machine.config 파일에 이러한 변경 내용은 마이그레이션해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-123">As a result, if a Web administrator has made changes to the Machine.config file, those changes must be migrated to the .NET Framework 1.1 Machine.config file.</span></span>

<a id="1"></a>

## <a name="maintaining-your-web-applications-mapping-to-net-framework-10-during-installation"></a><span data-ttu-id="43cfd-124">.NET Framework 1.0을 설치 하는 동안 웹 응용 프로그램의 매핑을 유지 관리</span><span class="sxs-lookup"><span data-stu-id="43cfd-124">Maintaining your Web application's mapping to .NET Framework 1.0 during installation</span></span>

<span data-ttu-id="43cfd-125">기본적으로 모든 기존 ASP.NET 응용 프로그램 설치 중.NET Framework의 최신 버전을 사용 하기 위해 자동으로 재구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-125">By default, all existing ASP.NET applications are automatically reconfigured during installation to use the newer version of the .NET Framework.</span></span> <span data-ttu-id="43cfd-126">.NET Framework의 최신 버전을 사용 하 여 응용 프로그램 개선 사항과 새 버전에 포함 된 새로운 기능을 완전히 활용을 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-126">Using the newer version of the .NET Framework, applications can take full advantage of improvements and new features included in the new release.</span></span> <span data-ttu-id="43cfd-127">동시에 응용 프로그램을 세부적으로 제어 하려는 웹 관리자는 업데이트, 자동 다시 매핑할 모든 기존 ASP.NET 응용 프로그램의.NET Framework를 설치 하는 동안 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-127">At the same time, the Web administrator, who might want granular control over which applications are updated, can prevent the automatic remapping of all existing ASP.NET applications during installation of the .NET Framework.</span></span>

<span data-ttu-id="43cfd-128">.NET Framework의 최신 버전으로 전체 ASP.NET 응용 프로그램의 자동 다시 매핑을 사용 하지 않으려면 웹 관리자 Dotnetfx.exe 설치 프로그램을 사용 하 여 /noaspupgrade 명령줄 옵션을 사용 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-128">To prevent the automatic remapping of the entire ASP.NET application to the newer version of the .NET Framework, the Web administrator can use the /noaspupgrade command-line option with the Dotnetfx.exe setup program.</span></span>

<span data-ttu-id="43cfd-129">**ASP.NET 응용 프로그램을 최신 버전의 전체 다시 매핑을 방지 하기 위해**</span><span class="sxs-lookup"><span data-stu-id="43cfd-129">**To prevent total remapping of ASP.NET application to newer version**</span></span>

1. <span data-ttu-id="43cfd-130">로 이동 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-130">Go to **Start**.</span></span>
2. <span data-ttu-id="43cfd-131">클릭할 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-131">Click on **run**.</span></span>
3. <span data-ttu-id="43cfd-132">**cmd**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-132">Type **cmd**.</span></span>
4. <span data-ttu-id="43cfd-133">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-133">Click **OK**.</span></span>  
  
    ![](side-by-side-with-10/_static/image1.gif)
5. <span data-ttu-id="43cfd-134">명령 프롬프트에서.NET Framework의 설치를 시작 하려면 다음 줄을 입력 합니다. **Dotnetfx.exe /c: "/noaspupgrade 설치?** 합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-134">From the command prompt, type the following line to start the installation of the .NET Framework: **Dotnetfx.exe /c:"install /noaspupgrade?**.</span></span>  
  
    ![](side-by-side-with-10/_static/image2.gif)
6. <span data-ttu-id="43cfd-135">클릭 **예** Microsoft.NET Framework 1.1 설치에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-135">Click **Yes** in the Microsoft .NET Framework 1.1 Setup.</span></span> <span data-ttu-id="43cfd-136">이.NET Framework 1.1의 설치 프로세스를 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-136">This will start the setup process of the .NET Framework 1.1.</span></span>  
  
    ![](side-by-side-with-10/_static/image3.gif)

<a id="2"></a>

## <a name="map-a-web-application-to-a-specific-version-of-the-net-framework"></a><span data-ttu-id="43cfd-137">특정 버전.NET Framework의 웹 응용 프로그램 맵</span><span class="sxs-lookup"><span data-stu-id="43cfd-137">Map a Web application to a specific version of the .NET Framework</span></span>

<span data-ttu-id="43cfd-138">ASP.NET IIS Registration Tool의 버전을 포함 하는 각 버전의.NET Framework (Aspnet\_regiis.exe).</span><span class="sxs-lookup"><span data-stu-id="43cfd-138">Each version of the .NET Framework includes a version of the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe).</span></span> <span data-ttu-id="43cfd-139">이 도구에는 관리자를 웹 응용 프로그램을.NET Framework의 특정 버전에서 실행 되도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-139">This tool enables administrators to specify that a Web application be run under a particular version of the .NET Framework.</span></span> <span data-ttu-id="43cfd-140">이 웹 응용 프로그램을.NET Framework의 버전 매핑 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-140">This is referred to as mapping a Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="43cfd-141">관리자를 선택 하 여 Aspnet 해야\_regiis.exe 웹 응용 프로그램과 관련 된.NET Framework의 버전에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-141">Administrators must select the Aspnet\_regiis.exe that corresponds to the version of the .NET Framework that will be associated with the Web application.</span></span> <span data-ttu-id="43cfd-142">예를 들어, 웹 사이트를.NET Framework 1.1을 사용 하도록 지정 하려는 관리자 Aspnet를 사용 해야\_regiis.exe.NET Framework 1.1을 사용 하 여 제공 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-142">For example, an administrator who wants to specify that a Web site use .NET Framework 1.1 must use the Aspnet\_regiis.exe that comes with .NET Framework 1.1.</span></span>

<span data-ttu-id="43cfd-143">Aspnet\_regiis.exe 버전 1.0에 대 한 위치는:</span><span class="sxs-lookup"><span data-stu-id="43cfd-143">The Aspnet\_regiis.exe for version 1.0 is located at:</span></span>

- <span data-ttu-id="43cfd-144">C:\WINDOWS\Microsoft.NET\Framework\**v1.0.3705**\aspnet\_regiis</span><span class="sxs-lookup"><span data-stu-id="43cfd-144">C:\WINDOWS\Microsoft.NET\Framework\**v1.0.3705**\aspnet\_regiis</span></span>

<span data-ttu-id="43cfd-145">Aspnet\_regiis.exe 버전 1, 1에 대 한 위치는:</span><span class="sxs-lookup"><span data-stu-id="43cfd-145">The Aspnet\_regiis.exe for version 1,1 is located at:</span></span>

- <span data-ttu-id="43cfd-146">C:\WINDOWS\Microsoft.NET\Framework\**v1.1.4322**\aspnet\_regiis</span><span class="sxs-lookup"><span data-stu-id="43cfd-146">C:\WINDOWS\Microsoft.NET\Framework\**v1.1.4322**\aspnet\_regiis</span></span>

<span data-ttu-id="43cfd-147">Aspnet\_regiis.exe 스크립트 매핑 웹 응용 프로그램에 대 한 두 가지 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-147">The Aspnet\_regiis.exe provides two options for script mapping a Web application:</span></span>

- <span data-ttu-id="43cfd-148">**-s** 설정 스크립트 맵을 경로 및 해당 하위 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-148">**-s** sets the script map in the path and in its child directories.</span></span>
- <span data-ttu-id="43cfd-149">**-sn** 만 경로에 스크립트 맵을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-149">**-sn** sets the script map in the path only.</span></span>

<span data-ttu-id="43cfd-150">W3SVC/루트 형식에 정의 되어 있는 웹 응용 프로그램 IIS 메타 데이터 경로 정의 하는 경로 / {WebSiteNumber} / {응용 프로그램\_이름}.</span><span class="sxs-lookup"><span data-stu-id="43cfd-150">The path defines the Web application IIS metadata path, which is defined in the form of W3SVC/ROOT/{WebSiteNumber}/{Application\_Name}.</span></span> <span data-ttu-id="43cfd-151">예를 들어 기본 웹 사이트 아래에 있는 포털 이라는 웹 응용 프로그램, 메타 베이스 경로 W3SVC/1/루트/포털입니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-151">For example, for a Web application called Portal located under the default Web site, the metabase path is W3SVC/1/ROOT/Portal.</span></span>

![](side-by-side-with-10/_static/image4.gif)

<span data-ttu-id="43cfd-152">메타 베이스 경로를 가져오는 메타 베이스 편집기 라는 도구를 사용할 수도 있습니다 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-152">Note You can also use a tool called the Metabase Editor to get the metabase path.</span></span> <span data-ttu-id="43cfd-153">Microsoft 지원 사이트에서이 도구를 다운로드할 수 있습니다 [ https://support.microsoft.com/default.aspx?scid=kb; en-우리; 232068 합니다.](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)</span><span class="sxs-lookup"><span data-stu-id="43cfd-153">You can download this tool from the Microsoft Support site at [https://support.microsoft.com/default.aspx?scid=kb;en-us;232068.](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)</span></span>

- <span data-ttu-id="43cfd-154">Aspnet 실행\_맵과 해당 subapplication regiis.exe-s W3SVC/1/루트/포털 IIS 포털 업데이트를 스크립팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-154">Run Aspnet\_regiis.exe -s W3SVC/1/ROOT/Portal to update the portal IIS script map and its subapplication.</span></span>  
  
    ![](side-by-side-with-10/_static/image5.gif)

- <span data-ttu-id="43cfd-155">Aspnet 실행\_regiis.exe-sn W3SVC/1/루트/포털 포털 IIS 스크립트를 업데이트 하에 매핑하는 포털에서 응용 프로그램에 영향을 주지 않고? s 하위 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-155">Run Aspnet\_regiis.exe -sn W3SVC/1/ROOT/Portal to update the portal IIS script map, without affecting applications in the portal?s subdirectories.</span></span>  
  
    ![](side-by-side-with-10/_static/image6.gif)

<a id="3"></a>

## <a name="find-the-net-framework-version-that-a-web-application-is-using"></a><span data-ttu-id="43cfd-156">웹 응용 프로그램을 사용 하는.NET Framework 버전 확인</span><span class="sxs-lookup"><span data-stu-id="43cfd-156">Find the .NET Framework version that a Web application is using</span></span>

<span data-ttu-id="43cfd-157">관리자로는 인터넷 서비스 관리자를 사용 하 여 웹 사이트를 실행 하는.NET Framework의 버전을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-157">An administrator can use the Internet Service Manager to find which version of the .NET Framework runs a Web site.</span></span> <span data-ttu-id="43cfd-158">다른 운영 체제 버전 다르게 인터넷 서비스 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-158">Different operating system versions launch the Internet Service Manager differently.</span></span> <span data-ttu-id="43cfd-159">서비스 관리자를 시작 하려면 아래에 나열 된 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-159">To start the service manager, follow the steps listed below.</span></span>

<span data-ttu-id="43cfd-160">**인터넷 서비스 관리자를 시작 하려면**</span><span class="sxs-lookup"><span data-stu-id="43cfd-160">**To start Internet Service Manager**</span></span>

1. <span data-ttu-id="43cfd-161">로 이동 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-161">Go to **Start**.</span></span>
2. <span data-ttu-id="43cfd-162">클릭할 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-162">Click on **run**.</span></span>
3. <span data-ttu-id="43cfd-163">형식 **inetmgr**합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-163">Type **inetmgr**.</span></span>  
  
    ![](side-by-side-with-10/_static/image7.gif)
4. <span data-ttu-id="43cfd-164">인터넷 서비스 관리자에서 웹 응용 프로그램 확인 하려는.NET Framework의 버전을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-164">From the Internet Service Manager, select the Web application whose version of the .NET Framework you want to know.</span></span>  
  
    ![](side-by-side-with-10/_static/image8.gif)
5. <span data-ttu-id="43cfd-165">웹 응용 프로그램을 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성입니다.**</span><span class="sxs-lookup"><span data-stu-id="43cfd-165">Right-click on the Web application, and click on **Properties.**</span></span>  
  
    ![](side-by-side-with-10/_static/image9.gif)
6. <span data-ttu-id="43cfd-166">속성 창에서 선택 **구성 합니다.**</span><span class="sxs-lookup"><span data-stu-id="43cfd-166">From the Property window, select **Configuration.**</span></span>  
  
    ![](side-by-side-with-10/_static/image10.gif)
7. <span data-ttu-id="43cfd-167">응용 프로그램 매핑 테이블에서 선택 **.aspx**, 클릭 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-167">From the application mapping table, select **.aspx**, and click **Edit**.</span></span>  
  
    ![](side-by-side-with-10/_static/image11.gif)
8. <span data-ttu-id="43cfd-168">**실행 파일** 텍스트 상자를 스크롤하여 버전 디렉터리를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-168">From the **Executable** text box, look at the version directory by scrolling.</span></span> <span data-ttu-id="43cfd-169">버전 디렉터리 v.1.1.4322 인 경우 응용 프로그램이.NET Framework 1.1에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-169">If the version directory is v.1.1.4322, the application is mapped to .NET Framework 1.1.</span></span> <span data-ttu-id="43cfd-170">반대로, 버전 디렉터리 v1.0.3705 인 경우 응용 프로그램이.NET Framework 1.0에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="43cfd-170">Conversely, if the version directory is v1.0.3705, the application is mapped to .NET Framework 1.0.</span></span>  
  
    ![](side-by-side-with-10/_static/image12.gif)
