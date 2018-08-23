---
uid: web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 문제 해결 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시)에서 실행 중인 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자...
ms.author: riande
ms.date: 06/01/2015
ms.assetid: c0090595-ab3b-4b9b-9e16-7a1891e8cb2f
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: 65cd5cd9f7d1f9c5fdaea9b0d16bdfd84259efdd
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838869"
---
<a name="aspnet-web-deployment-using-visual-studio-troubleshooting"></a><span data-ttu-id="f1d56-103">Visual Studio를 사용 하 여 ASP.NET 웹 배포: 문제 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-103">ASP.NET Web Deployment using Visual Studio: Troubleshooting</span></span>
====================
<span data-ttu-id="f1d56-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="f1d56-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="f1d56-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="f1d56-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="f1d56-106">이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="f1d56-107">시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


<span data-ttu-id="f1d56-108">이 페이지에서는 Visual Studio를 사용 하 여 ASP.NET 웹 응용 프로그램을 배포할 때 발생할 수 있는 몇 가지 일반적인 문제를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-108">This page describes some common problems that may arise when you deploy an ASP.NET web application by using Visual Studio.</span></span> <span data-ttu-id="f1d56-109">각각에 대 한 가능한 원인과 해당 솔루션은 하나 이상의 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-109">For each one, one or more possible causes and corresponding solutions are provided.</span></span>

<span data-ttu-id="f1d56-110">표시 된 시나리오는 Azure와 타사 호스팅 공급자에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-110">The scenarios shown apply to both Azure and third-party hosting providers.</span></span> <span data-ttu-id="f1d56-111">Azure App Service에서 웹 앱 문제를 해결 하는 방법에 대 한 자세한 내용은 다음 리소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f1d56-111">For more information about troubleshooting web apps in Azure App Service, see the following resources:</span></span>

- [<span data-ttu-id="f1d56-112">Visual Studio를 사용하여 Azure App Service의 웹앱 문제 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-112">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)
- [<span data-ttu-id="f1d56-113">Azure App Service에서 Web Apps 모니터링</span><span class="sxs-lookup"><span data-stu-id="f1d56-113">Monitor Web Apps in Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-monitor//)
- <span data-ttu-id="f1d56-114">[.NET 용 Windows Azure SDK 2.0의 출시를 발표](http://https://weblogs.asp.net/scottgu/announcing-the-release-of-windows-azure-sdk-2-0-for-net) (ScottGu의 블로그는 Visual Studio에서 진단 로그를 가져오는 방법을 표시 하는 데 사용)</span><span class="sxs-lookup"><span data-stu-id="f1d56-114">[Announcing the release of Windows Azure SDK 2.0 for .NET](http://https://weblogs.asp.net/scottgu/announcing-the-release-of-windows-azure-sdk-2-0-for-net) (ScottGu's blog, shows how to get diagnostic logs in Visual Studio)</span></span>

## <a name="server-error-in--application---current-custom-error-settings-prevent-details-of-the-error-from-being-viewed-remotely"></a><span data-ttu-id="f1d56-115">서버 오류 현재 사용자 지정 오류 설정을 원격으로 볼 수 없도록 오류의 세부 정보를 방지 '/' 응용 프로그램-</span><span class="sxs-lookup"><span data-stu-id="f1d56-115">Server Error in '/' Application - Current Custom Error Settings Prevent Details of the Error from Being Viewed Remotely</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-116">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-116">Scenario</span></span>

<span data-ttu-id="f1d56-117">사이트를 원격 호스트에 배포한 후 Web.config 파일에는 customErrors 설정에 언급 하지만 던 오류의 실제 원인을 나타내지 않습니다 오류 메시지가 표시:</span><span class="sxs-lookup"><span data-stu-id="f1d56-117">After deploying a site to a remote host, you get an error message that mentions the customErrors setting in the Web.config file but doesn't indicate what the actual cause of the error was:</span></span>

[!code-xml[Main](troubleshooting/samples/sample1.xml)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-118">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-118">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-119">기본적으로 ASP.NET 웹 응용 프로그램이 로컬 컴퓨터에서 실행 되는 경우에 자세한 오류 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-119">By default, ASP.NET shows detailed error information only when your web application is running on the local computer.</span></span> <span data-ttu-id="f1d56-120">일반적으로 웹 응용 프로그램 이므로 인터넷을 통해 공개적으로 사용할 수 있는 해커는 취약점을 찾기 위해 응용 프로그램에서이 정보를 사용 하는 일을 할 수 있습니다 하는 경우 자세한 오류 정보를 표시 하지 않으려면입니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-120">Generally you don't want to display detailed error information when your web application is publicly available over the Internet, because hackers may be able to use this information to find vulnerabilities in the application.</span></span> <span data-ttu-id="f1d56-121">그러나를 배포 하는 사이트 또는 업데이트 사이트에 따라 잘못 될 수 시간과 실제 오류 메시지를 준비 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-121">However, when you are deploying a site or updates to a site, sometimes something will go wrong and you need to get the actual error message.</span></span>

<span data-ttu-id="f1d56-122">원격 호스트에서 실행 될 때 자세한 오류 메시지를 표시 하도록 응용 프로그램을 사용 하려면, customErrors 모드를 해제 하 고, 응용 프로그램을 다시 배포 하 고, 응용 프로그램을 다시 실행 하려면 Web.config 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-122">To enable the application to display detailed error messages when it runs on the remote host, edit the Web.config file to set customErrors mode off, redeploy the application, and run the application again:</span></span>

1. <span data-ttu-id="f1d56-123">응용 프로그램 Web.config 파일에 acustomErrors 요소 thesystem.web 요소의 경우 themode 특성을 "off"로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-123">If the application Web.config file has acustomErrors element in thesystem.web element, change themode attribute to "off".</span></span> <span data-ttu-id="f1d56-124">그렇지 않으면 요소를 추가 acustomErrors thesystem.web 요소 themode 특성을 "off"로 설정 하 여 다음 예와에서 같이:</span><span class="sxs-lookup"><span data-stu-id="f1d56-124">Otherwise add acustomErrors element in thesystem.web element with themode attribute set to "off", as shown in the following example:</span></span> 

    [!code-xml[Main](troubleshooting/samples/sample2.xml)]
2. <span data-ttu-id="f1d56-125">응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-125">Deploy the application.</span></span>
3. <span data-ttu-id="f1d56-126">응용 프로그램을 실행 하 고 모든 이전 오류를 발생 시킨 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-126">Run the application and repeat whatever you did earlier that caused the error to occur.</span></span> <span data-ttu-id="f1d56-127">이제 실제 오류 메시지의 내용 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-127">Now you can see what the actual error message is.</span></span>
4. <span data-ttu-id="f1d56-128">오류를 해결 하는 경우 원래 customErrors 설정을 복원 하 고 응용 프로그램을 재배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-128">When you have resolved the error, restore the original customErrors setting and redeploy the application.</span></span>

## <a name="cannot-createshadow-copy-contosouniversity-when-that-file-already-exists"></a><span data-ttu-id="f1d56-129">없습니다 만들어 섀도 복사본 'ContosoUniversity' 파일이 이미 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="f1d56-129">Cannot create/shadow copy 'ContosoUniversity' when that file already exists.</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-130">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-130">Scenario</span></span>

<span data-ttu-id="f1d56-131">Visual Studio에서 프로젝트를 실행 하려고 할 때 다음과 비슷한 메시지와 함께 오류 페이지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-131">When you try to run a project in Visual Studio you get an error page with a message like the following example:</span></span>

<span data-ttu-id="f1d56-132">'/' 응용 프로그램에 서버 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-132">Server Error in '/' Application.</span></span> <span data-ttu-id="f1d56-133">없습니다 만들어 섀도 복사본 'ContosoUniversity' 파일이 이미 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="f1d56-133">Cannot create/shadow copy 'ContosoUniversity' when that file already exists.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-134">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-134">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-135">잠깐 브라우저 새로 고침 또는 사이트를 다시 컴파일할 및 다시 실행 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="f1d56-135">Wait a minute and refresh the browser, or recompile the site and try running it again.</span></span>

## <a name="access-is-denied-in-a-web-page-that-uses-sql-server-compact"></a><span data-ttu-id="f1d56-136">액세스가 거부 되었습니다. 웹 페이지에서 사용 하 여 SQL Server Compact는</span><span class="sxs-lookup"><span data-stu-id="f1d56-136">Access is Denied in a Web Page that Uses SQL Server Compact</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-137">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-137">Scenario</span></span>

<span data-ttu-id="f1d56-138">SQL Server Compact를 사용 하는 사이트를 배포 하 고 데이터베이스에 액세스 하는 배포 된 사이트의 페이지를 실행 하는 경우 다음 오류 메시지가 표시:</span><span class="sxs-lookup"><span data-stu-id="f1d56-138">When you deploy a site that uses SQL Server Compact and you run a page in the deployed site that accesses the database, you see the following error message:</span></span>

<span data-ttu-id="f1d56-139">액세스가 거부되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-139">Access is denied.</span></span> <span data-ttu-id="f1d56-140">(HRESULT의 예외: 0x80070005 (E\_ACCESSDENIED))</span><span class="sxs-lookup"><span data-stu-id="f1d56-140">(Exception from HRESULT: 0x80070005 (E\_ACCESSDENIED))</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-141">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-141">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-142">서버에 네트워크 서비스 계정에 있는 SQL 서비스 Compact 네이티브 이진 파일을 읽을 수 있어야 합니다 *bin\amd64* 또는 *bin\x86* 하지만 폴더는 읽기 권한이 해당 폴더에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-142">The NETWORK SERVICE account on the server needs to be able to read SQL Service Compact native binaries that are in the *bin\amd64* or *bin\x86* folder, but it does not have read permissions for those folders.</span></span> <span data-ttu-id="f1d56-143">집합에서 네트워크 서비스에 대 한 권한이 읽기를 *bin* 폴더, 하위 폴더에 사용 권한을 확장할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-143">Set read permission for NETWORK SERVICE on the *bin* folder, making sure to extend the permissions to subfolders.</span></span>

## <a name="cannot-read-configuration-file-due-to-insufficient-permissions"></a><span data-ttu-id="f1d56-144">권한이 부족 하 여 구성 파일을 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-144">Cannot Read Configuration File Due to Insufficient Permissions</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-145">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-145">Scenario</span></span>

<span data-ttu-id="f1d56-146">클릭 하면 Visual Studio 게시 단추 로컬 컴퓨터에 IIS에 응용 프로그램 배포 실패를 게시 및 **출력** 창 다음과 유사한 오류 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-146">When you click the Visual Studio publish button to deploy an application to IIS on your local machine, publishing fails and the **Output** window shows an error message similar to this:</span></span>

<span data-ttu-id="f1d56-147">' MACHINE/리디렉션 ' IIS 구성 파일을 읽는 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-147">An error occurred when reading the IIS Configuration File 'MACHINE/REDIRECTION'.</span></span> <span data-ttu-id="f1d56-148">이 작업을 수행 하는 id가 하는 중... 오류: 권한이 부족 하 여 구성 파일을 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-148">The identity performing this operation was ... Error: Cannot read configuration file due to insufficient permissions.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-149">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-149">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-150">한 번의 클릭을 사용 하려면 로컬 컴퓨터에 IIS에 게시, 관리자 권한으로 Visual Studio 실행 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-150">To use one-click publish to IIS on your local machine, you must be running Visual Studio with administrator permissions.</span></span> <span data-ttu-id="f1d56-151">Visual Studio를 닫고 관리자 권한으로 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-151">Close Visual Studio and restart it with administrator permissions.</span></span>

## <a name="could-not-connect-to-the-destination-computer--using-the-specified-process"></a><span data-ttu-id="f1d56-152">대상 컴퓨터에 연결 하지 못했습니다... 지정된 된 프로세스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f1d56-152">Could Not Connect to the Destination Computer ... Using the Specified Process</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-153">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-153">Scenario</span></span>

<span data-ttu-id="f1d56-154">클릭 하면 Visual Studio 게시 응용 프로그램을 배포 하는 단추 실패를 게시 및 **출력** 창 다음과 유사한 오류 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-154">When you click the Visual Studio publish button to deploy an application, publishing fails and the **Output** window shows an error message similar to this:</span></span>

[!code-console[Main](troubleshooting/samples/sample3.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-155">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-155">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-156">프록시 서버는 대상 서버와의 통신을 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-156">A proxy server is interrupting communication with the destination server.</span></span> <span data-ttu-id="f1d56-157">Windows 제어판에서 또는 Internet Explorer에서 선택 **인터넷 옵션** 선택 합니다 **연결** 탭 합니다. 에 **인터넷 속성** 대화 상자, 클릭 **LAN 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-157">From the Windows Control Panel or in Internet Explorer, select **Internet Options** and select the **Connections** tab. In the **Internet Properties** dialog box, click **LAN Settings**.</span></span> <span data-ttu-id="f1d56-158">에 **Local Area Network (LAN) 설정** 대화 상자, 일반를 **자동으로 설정 검색** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-158">In the **Local Area Network (LAN) Settings** dialog box, clear the **Automatically detect settings** checkbox.</span></span> <span data-ttu-id="f1d56-159">다시 게시 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-159">Then click the publish button again.</span></span>

<span data-ttu-id="f1d56-160">문제가 지속 되 면 프록시 또는 방화벽 설정을 사용 하 여 수행할 수 있는 작업을 확인 하려면 시스템 관리자에 게 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-160">If the problem persists, contact your system administrator to determine what can be done with proxy or firewall settings.</span></span> <span data-ttu-id="f1d56-161">웹 관리 서비스 배포 (8172;)에 대 한 비표준 포트를 사용 하 여 웹 배포 문제 발생 다른 연결에 대 한 웹 배포 포트 80을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-161">The problem happens because Web Deploy uses a non-standard port for Web Management Service deployment (8172); for other connections, Web Deploy uses port 80.</span></span> <span data-ttu-id="f1d56-162">타사 호스팅 공급자에 배포 하는 경우 일반적으로 웹 관리 서비스를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-162">When you are deploying to a third-party hosting provider, you are typically using the Web Management Service.</span></span>

## <a name="default-net-40-application-pool-does-not-exist"></a><span data-ttu-id="f1d56-163">기본.NET 4.0 응용 프로그램 풀이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-163">Default .NET 4.0 Application Pool Does Not Exist</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-164">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-164">Scenario</span></span>

<span data-ttu-id="f1d56-165">.NET Framework 4가 필요 하는 응용 프로그램을 배포할 때 다음 오류 메시지가 표시:</span><span class="sxs-lookup"><span data-stu-id="f1d56-165">When you deploy an application that requires the .NET Framework 4, you see the following error message:</span></span>

<span data-ttu-id="f1d56-166">기본.NET 4.0 응용 프로그램 풀이 존재 하지 않거나 응용 프로그램을 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-166">The default .NET 4.0 application pool does not exist or the application could not be added.</span></span> <span data-ttu-id="f1d56-167">ASP.NET 4.0이이 컴퓨터에 설치 되어 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f1d56-167">Please verify that ASP.NET 4.0 is installed on this machine.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-168">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-168">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-169">IIS에서 ASP.NET 4 설치 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-169">ASP.NET 4 is not installed in IIS.</span></span> <span data-ttu-id="f1d56-170">에 배포 하는 서버는 개발 컴퓨터에 Visual Studio 2010를 설치 하는 경우 ASP.NET 4 컴퓨터에 설치 되어 있지만 iis에서를 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-170">If the server you are deploying to is your development computer and has Visual Studio 2010 installed on it, ASP.NET 4 is installed on the computer but might not be installed in IIS.</span></span> <span data-ttu-id="f1d56-171">배포 하는 서버에서 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 하 여 IIS에서 ASP.NET 4를 설치:</span><span class="sxs-lookup"><span data-stu-id="f1d56-171">On the server that you are deploying to, open an elevated command prompt and install ASP.NET 4 in IIS by running the following commands:</span></span>

[!code-console[Main](troubleshooting/samples/sample4.cmd)]

<span data-ttu-id="f1d56-172">기본 응용 프로그램 풀의.NET Framework 버전을 수동으로 설정 하려면 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-172">You might also need to manually set the .NET Framework version of the default application pool.</span></span> <span data-ttu-id="f1d56-173">자세한 내용은이 시리즈의 자습서 테스트 환경으로 IIS에 배포를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f1d56-173">For more information, see the Deploying to IIS as a Test Environment tutorial in this series.</span></span>

## <a name="format-of-the-initialization-string-does-not-conform-to-specification-starting-at-index-0"></a><span data-ttu-id="f1d56-174">초기화 문자열 형식의 인덱스 0부터 시작 하는 사양에 맞지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-174">Format of the initialization string does not conform to specification starting at index 0.</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-175">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-175">Scenario</span></span>

<span data-ttu-id="f1d56-176">한 번의 클릭을 사용 하 여 응용 프로그램을 배포한 후 게시를 받으면 데이터베이스에 액세스 하는 페이지를 실행 하면 다음 오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="f1d56-176">After you deploy an application using one-click publish, when you run a page that accesses the database you get the following error message:</span></span>

<span data-ttu-id="f1d56-177">초기화 문자열 형식의 인덱스 0부터 시작 하는 사양에 맞지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-177">Format of the initialization string does not conform to specification starting at index 0.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-178">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-178">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-179">엽니다는 *Web.config* 배포 된 사이트에 연결 문자열 값을 $로 시작 하는지 여부를 확인 하는 파일 (ReplacableToken\_, 다음 예제 에서처럼에서:</span><span class="sxs-lookup"><span data-stu-id="f1d56-179">Open the *Web.config* file in the deployed site and check to see whether the connection string values begin with $(ReplacableToken\_, as in the following example:</span></span>

[!code-xml[Main](troubleshooting/samples/sample5.xml)]

<span data-ttu-id="f1d56-180">연결 문자열이 예제와 같이, 프로젝트 파일을 편집 하 고 모든 빌드 구성 되는 PropertyGroup 요소에 다음 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-180">If the connection strings look like this example, edit the project file and add the following property to the PropertyGroup element that is for all build configurations:</span></span>

[!code-xml[Main](troubleshooting/samples/sample6.xml)]

<span data-ttu-id="f1d56-181">그런 다음 응용 프로그램을 재배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-181">Then redeploy the application.</span></span>

## <a name="http-500-internal-server-error"></a><span data-ttu-id="f1d56-182">HTTP 500 내부 서버 오류</span><span class="sxs-lookup"><span data-stu-id="f1d56-182">HTTP 500 Internal Server Error</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-183">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-183">Scenario</span></span>

<span data-ttu-id="f1d56-184">배포 된 사이트를 실행 하면 다음 오류 메시지가 표시 오류의 원인을 나타내는 구체적인 정보 없이:</span><span class="sxs-lookup"><span data-stu-id="f1d56-184">When you run the deployed site, you see the following error message without specific information indicating the cause of the error:</span></span>

<span data-ttu-id="f1d56-185">HTTP 오류 500-내부 서버 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-185">HTTP Error 500 - Internal Server Error.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-186">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-186">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-187">500 오류는 여러 가지 원인이 있지만 Web.config 변환 파일 중 하나에 잘못 된 위치에 XML 요소를 추가 하는 오류가 발생 하는 경우 이러한 자습서.</span><span class="sxs-lookup"><span data-stu-id="f1d56-187">There are many causes of 500 errors, but one possible cause if you are following these tutorials is that you put an XML element in the wrong place in one of the Web.config transformation files.</span></span> <span data-ttu-id="f1d56-188">예를 들어, 변환을 삽입 하는 경우이 오류가 발생할 것 있습니다를 &lt;위치&gt; 요소 아래에 있는 &lt;system.web&gt; 대신 바로 아래 &lt;구성&gt;합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-188">For example, you would get this error if you put the transformation that inserts a &lt;location&gt; element under &lt;system.web&gt; instead of directly under &lt;configuration&gt;.</span></span> <span data-ttu-id="f1d56-189">변환이 의도 한 대로 작동 하는지 확인 하려면 Web.config 변환 미리 보기 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-189">You can use the Web.config transform preview feature to verify that transformations are working as intended.</span></span> <span data-ttu-id="f1d56-190">올바르게 코딩 하는 변환의 찾을 경우 솔루션 변환 파일을 수정 하 고 다시 배포 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-190">The solution if you find a transform that was coded incorrectly is to correct the transformation file and redeploy.</span></span> <span data-ttu-id="f1d56-191">확실 한 오류가 없으면 변환 주석으로 처리 해 500 오류를 일으키는지 어느를 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-191">If an error isn't obvious, try commenting out transforms and redeploying to see which one is causing the 500 error.</span></span>

## <a name="http-50021-internal-server-error"></a><span data-ttu-id="f1d56-192">HTTP 500.21 내부 서버 오류</span><span class="sxs-lookup"><span data-stu-id="f1d56-192">HTTP 500.21 Internal Server Error</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-193">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-193">Scenario</span></span>

<span data-ttu-id="f1d56-194">배포 된 사이트를 실행 하면 다음 오류 메시지가 표시:</span><span class="sxs-lookup"><span data-stu-id="f1d56-194">When you run the deployed site, you see the following error message:</span></span>

<span data-ttu-id="f1d56-195">HTTP 오류 500.21-내부 서버 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-195">HTTP Error 500.21 - Internal Server Error.</span></span> <span data-ttu-id="f1d56-196">"PageHandlerFactory 통합" 처리기에 해당 모듈 목록에 잘못 된 모듈 "ManagedPipelineHandler"입니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-196">Handler "PageHandlerFactory-Integrated" has a bad module "ManagedPipelineHandler" in its module list.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-197">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-197">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-198">사이트 대상 ASP.NET 4, 하지만 ASP.NET 4에에서 등록 하지 않은 IIS 서버에 배포 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-198">The site you have deployed targets ASP.NET 4, but ASP.NET 4 is not registered in IIS on the server.</span></span> <span data-ttu-id="f1d56-199">서버에서 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 하 여 ASP.NET 4를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-199">On the server open an elevated command prompt and register ASP.NET 4 by running the following commands:</span></span>

[!code-console[Main](troubleshooting/samples/sample7.cmd)]

<span data-ttu-id="f1d56-200">기본 응용 프로그램 풀의.NET Framework 버전을 수동으로 설정 하려면 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-200">You might also need to manually set the .NET Framework version of the default application pool.</span></span> <span data-ttu-id="f1d56-201">자세한 내용은이 시리즈의 자습서 테스트 환경으로 IIS에 배포를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f1d56-201">For more information, see the Deploying to IIS as a Test Environment tutorial in this series.</span></span>

## <a name="login-failed-opening-sql-server-express-database-in-appdata"></a><span data-ttu-id="f1d56-202">SQL Server Express 데이터베이스를 여는 앱에서 로그인이 실패 했습니다\_데이터</span><span class="sxs-lookup"><span data-stu-id="f1d56-202">Login Failed Opening SQL Server Express Database in App\_Data</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-203">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-203">Scenario</span></span>

<span data-ttu-id="f1d56-204">업데이트를 *Web.config* SQL Server Express 데이터베이스를 가리키도록 연결 문자열을 파일을 *.mdf* 파일에 *앱\_데이터* 폴더 및 첫 번째 다음 오류 메시지가 표시 응용 프로그램을 실행 하는 시간:</span><span class="sxs-lookup"><span data-stu-id="f1d56-204">You updated the *Web.config* file connection string to point to a SQL Server Express database as an *.mdf* file in your *App\_Data* folder, and the first time you run the application you see the following error message:</span></span>

<span data-ttu-id="f1d56-205">System.Data.SqlClient.SqlException: "DatabaseName" 로그인에서 요청한 데이터베이스를 열 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-205">System.Data.SqlClient.SqlException: Cannot open database "DatabaseName" requested by the login.</span></span> <span data-ttu-id="f1d56-206">로그인에 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-206">The login failed.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-207">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-207">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-208">이름을 합니다 *.mdf* 파일 삭제 한 경우에 컴퓨터에 이전에 있던 모든 SQL Server Express 데이터베이스의 이름을 일치할 수 없습니다. 합니다 *.mdf* 기존 데이터베이스의 파일.</span><span class="sxs-lookup"><span data-stu-id="f1d56-208">The name of the *.mdf* file cannot match the name of any SQL Server Express database that has ever existed on your computer, even if you deleted the *.mdf* file of the previously existing database.</span></span> <span data-ttu-id="f1d56-209">이름을 변경 합니다 *.mdf* 변경 데이터베이스 이름으로 사용 되지 않은 이름으로 파일을 *Web.config* 새 이름을 사용 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-209">Change the name of the *.mdf* file to a name that has never been used as a database name and change the *Web.config* file to use the new name.</span></span> <span data-ttu-id="f1d56-210">사용할 수 있습니다 [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) 기존 SQL Server Express를 삭제 하려면 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-210">As an alternative, you can use [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) to delete previously existing SQL Server Express databases.</span></span>

## <a name="model-compatibility-cannot-be-checked"></a><span data-ttu-id="f1d56-211">검사할 수 없습니다. 모델 호환성</span><span class="sxs-lookup"><span data-stu-id="f1d56-211">Model Compatibility Cannot be Checked</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-212">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-212">Scenario</span></span>

<span data-ttu-id="f1d56-213">업데이트를 *Web.config* 파일을 새 SQL Server Express 데이터베이스를 가리키도록 연결 문자열 및 다음과 같은 오류 메시지가 표시 처음으로 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-213">You updated the *Web.config* file connection string to point to a new SQL Server Express database, and the first time you run the application you see the following error message:</span></span>

<span data-ttu-id="f1d56-214">데이터베이스는 모델 메타 데이터를 포함 하지 않으므로 모델 호환성을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-214">Model compatibility cannot be checked because the database does not contain model metadata.</span></span> <span data-ttu-id="f1d56-215">IncludeMetadataConvention DbModelBuilder 규칙에 추가 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-215">Ensure that IncludeMetadataConvention has been added to the DbModelBuilder conventions.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-216">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-216">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-217">전에 컴퓨터에 데이터베이스를 이미 있을 수 있습니다 것에서 일부 테이블을 사용 하 여 Web.config 파일에 배치 하면 데이터베이스 이름을 사용한 적이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-217">If the database name you put in the Web.config file was ever used before on your computer, a database might already exist with some tables in it.</span></span> <span data-ttu-id="f1d56-218">변경 하기 전에 컴퓨터의 사용 되지 않은 새 이름을 선택 합니다 *Web.config* 이 새 데이터베이스 이름을 사용 하 여 가리키도록 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-218">Select a new name that has not been used on your computer before and change the *Web.config* file to point to use this new database name.</span></span> <span data-ttu-id="f1d56-219">사용할 수 있습니다 [SQL Server Express 유틸리티](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990) 하거나 [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) 기존 데이터베이스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-219">As an alternative, you can use [SQL Server Express Utility](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990) or [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) to delete the existing database.</span></span>

## <a name="sql-error-when-a-script-attempts-to-create-users-or-roles"></a><span data-ttu-id="f1d56-220">스크립트를 사용자 또는 역할을 만들려고 시도 하는 동안 SQL 오류가 발생 했습니다</span><span class="sxs-lookup"><span data-stu-id="f1d56-220">SQL Error When a Script Attempts to Create Users or Roles</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-221">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-221">Scenario</span></span>

<span data-ttu-id="f1d56-222">에 구성 된 데이터베이스 배포를 사용 하는 합니다 **패키지 및 게시 SQL** 탭을 배포 하는 동안 실행 되는 SQL 스크립트 포함 Create User 또는 Create Role 명령 및 스크립트 실행 실패 하면 해당 명령이 실행 될 때.</span><span class="sxs-lookup"><span data-stu-id="f1d56-222">You are using database deployment configured on the **Package/Publish SQL** tab, SQL scripts that run during deployment include Create User or Create Role commands, and script execution fails when those commands are executed.</span></span> <span data-ttu-id="f1d56-223">자세한 내용을 보려면 다음과 같은 메시지가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-223">You might see more detailed messages, such as the following:</span></span>

[!code-console[Main](troubleshooting/samples/sample8.cmd)]

<span data-ttu-id="f1d56-224">에 데이터베이스 배포를 구성한 경우이 오류가 발생 합니다 **웹 게시** 마법사 대신 **SQL 패키지 및 게시** 탭에 스레드는 [구성 및 배포](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) 포럼 및 솔루션 문제 해결이 페이지에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-224">If this error occurs when you have configured database deployment in the **Publish Web** wizard rather than the **Package/Publish SQL** tab, create a thread in the [Configuration and Deployment](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) forum, and the solution will be added to this troubleshooting page.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-225">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-225">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-226">배포를 수행 하는 데 사용할 사용자 계정에 사용자 또는 역할을 만들 수 있는 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-226">The user account you are using to perform deployment does not have permission to create users or roles.</span></span> <span data-ttu-id="f1d56-227">호스팅 업체에서 db를 할당할 수는 예를 들어\_datareader를 db\_datawriter 여부, 및 db\_를 설정 하는 사용자 계정에 ddladmin 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-227">For example, the hosting company might assign the db\_datareader, db\_datawriter, and db\_ddladmin roles to the user account that it sets up for you.</span></span> <span data-ttu-id="f1d56-228">이들은 충분 한 대부분의 데이터베이스 개체를 만들기 위한 하지만 사용자 또는 역할을 만들기 위한 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-228">These are sufficient for creating most database objects, but not for creating users or roles.</span></span> <span data-ttu-id="f1d56-229">오류를 방지 하는 하나의 방법은 데이터베이스 배포에서 사용자 및 역할을 제외 하 여 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-229">One way to avoid the error is by excluding users and roles from database deployment.</span></span> <span data-ttu-id="f1d56-230">다음 특성을 포함 하도록 데이터베이스의 자동으로 생성 된 스크립트에 대 한 PreSource 요소를 편집 하 여이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-230">You can do this by editing the PreSource element for the database's automatically generated script so that it includes the following attributes:</span></span>

[!code-console[Main](troubleshooting/samples/sample9.cmd)]

<span data-ttu-id="f1d56-231">프로젝트 파일에서 PreSource 요소를 편집 하는 방법에 대 한 정보를 참조 하세요 [방법: 프로젝트 파일에서 배포 설정 편집](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-231">For information about how to edit the PreSource element in the project file, see [How to: Edit Deployment Settings in the Project File](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx).</span></span> <span data-ttu-id="f1d56-232">사용자 또는 역할을 개발 데이터베이스에서 대상 데이터베이스에 필요한 경우 지원에 대 한 호스팅 공급자에 게 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-232">If the users or roles in your development database need to be in the destination database, contact your hosting provider for assistance.</span></span>

## <a name="sql-server-timeout-error-when-running-custom-scripts-during-deployment"></a><span data-ttu-id="f1d56-233">배포 하는 동안 사용자 지정 스크립트를 실행 하는 경우 SQL Server 시간 초과 오류</span><span class="sxs-lookup"><span data-stu-id="f1d56-233">SQL Server Timeout Error When Running Custom Scripts During Deployment</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-234">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-234">Scenario</span></span>

<span data-ttu-id="f1d56-235">사용자 지정 SQL 스크립트를 배포 하는 동안 실행할 지정 하 고 실행 될 때 웹 배포 하는 시간을 초과 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-235">You have specified custom SQL scripts to run during deployment, and when Web Deploy runs them, they time out.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-236">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-236">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-237">다른 트랜잭션 모드에 있는 여러 스크립트를 실행 시간 초과 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-237">Running multiple scripts that have different transaction modes can cause time-out errors.</span></span> <span data-ttu-id="f1d56-238">기본적으로 트랜잭션에서 자동으로 생성 된 스크립트를 실행 하지만 사용자 지정 스크립트에는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-238">By default, automatically generated scripts run in a transaction, but custom scripts do not.</span></span> <span data-ttu-id="f1d56-239">선택 하는 경우는 **데이터 및/또는 기존 데이터베이스에서 스키마 가져오기** 옵션을 합니다 **SQL 패키지 및 게시** 탭 사용자 지정 SQL 스크립트를 추가 하는 경우 일부 스크립트의 트랜잭션 설정을 변경 해야 합니다 있도록 모든 스크립트에는 동일한 트랜잭션 설정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-239">If you select the **Pull data and/or schema from an existing database** option on the **Package/Publish SQL** tab, and if you add a custom SQL script, you must change transaction settings on some scripts so that all scripts use the same transaction settings.</span></span> <span data-ttu-id="f1d56-240">자세한 내용은 [방법:를 사용 하 여 웹 프로젝트를 데이터베이스 응용 프로그램을 배포](https://msdn.microsoft.com/library/dd465343.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-240">For more information, see [How to: Deploy a Database With a Web Application Project](https://msdn.microsoft.com/library/dd465343.aspx).</span></span>

<span data-ttu-id="f1d56-241">모두 동일한 있도록 트랜잭션 설정을 구성 해도이 오류가 여전히 발생 하는 경우 가능한 해결 방법은 개별적으로 스크립트를 실행 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-241">If you have configured transaction settings so that all are the same but still get this error, a possible workaround is to run the scripts separately.</span></span> <span data-ttu-id="f1d56-242">에 **데이터베이스 스크립트** 표에 **패키지/게시** SQL 탭을 선택 취소를 **포함** 확인란 스크립트 시간 제한 오류를 발생 시킨 다음 프로젝트를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-242">In the **Database Scripts** grid in the **Package/Publish** SQL tab, clear the **Include** check box for the script that causes the timeout error, then publish the project.</span></span> <span data-ttu-id="f1d56-243">로 다시 이동 합니다 **데이터베이스 스크립트** 표에서 해당 스크립트의 선택 **포함** 확인란을 선택한의 선택을 취소는 **포함** 다른 스크립트에 대 한 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-243">Then go back into the **Database Scripts** grid, select that script's **Include** check box, and clear the **Include** check boxes for the other scripts.</span></span> <span data-ttu-id="f1d56-244">그런 다음 프로젝트를 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-244">Then publish the project again.</span></span> <span data-ttu-id="f1d56-245">이 이번에 게시 하는 경우, 선택한 사용자 지정 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-245">This time when you publish, only the selected custom script runs.</span></span>

## <a name="stream-data-of-site-manifest-is-not-yet-available"></a><span data-ttu-id="f1d56-246">사이트 매니페스트의 Stream 데이터를 아직 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-246">Stream Data of Site Manifest Is Not Yet Available</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-247">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-247">Scenario</span></span>

<span data-ttu-id="f1d56-248">설치 하는 경우 사용 하 여 패키지를 *deploy.cmd* 파일 t (테스트) 옵션을 사용 하 여 다음과 같은 오류 메시지가 표시:</span><span class="sxs-lookup"><span data-stu-id="f1d56-248">When you are installing a package using the *deploy.cmd* file with the t (test) option, you see the following error message:</span></span>

<span data-ttu-id="f1d56-249">오류:의 스트림 데이터를 ' sitemanifest/dbFullSql [@path= 'C:\TEMP\AdventureWorksGrant.sql']/sqlScript'를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-249">Error: The stream data of 'sitemanifest/dbFullSql[@path='C:\TEMP\AdventureWorksGrant.sql']/sqlScript' is not yet available.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-250">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-250">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-251">오류 메시지 명령을 테스트 보고서를 생성할 수 없는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-251">The error message means that the command cannot produce a test report.</span></span> <span data-ttu-id="f1d56-252">그러나 y (실제 설치) 옵션을 사용 하는 경우 명령이 실행 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-252">However, the command might run if you use the y (actual installation) option.</span></span> <span data-ttu-id="f1d56-253">메시지는 테스트 모드에서 명령을 실행 하는 문제가 있는 것만 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-253">The message indicates only that there is a problem with running the command in test mode.</span></span>

## <a name="this-application-requires-managedruntimeversion-v40"></a><span data-ttu-id="f1d56-254">이 응용 프로그램 필요 ManagedRuntimeVersion v4.0</span><span class="sxs-lookup"><span data-stu-id="f1d56-254">This Application Requires ManagedRuntimeVersion v4.0</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-255">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-255">Scenario</span></span>

<span data-ttu-id="f1d56-256">배포 하려는 경우 다음 오류 메시지가 표시:</span><span class="sxs-lookup"><span data-stu-id="f1d56-256">When you attempt to deploy, you see the following error message:</span></span>

<span data-ttu-id="f1d56-257">사용 하려는 응용 프로그램 풀 'managedRuntimeVersion' 속성이 ('v2.0'로 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-257">The application pool that you are trying to use has the 'managedRuntimeVersion' property set to 'v2.0'.</span></span> <span data-ttu-id="f1d56-258">이 응용 프로그램 'v4.0' 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-258">This application requires 'v4.0'.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-259">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-259">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-260">IIS에서 ASP.NET 4 설치 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-260">ASP.NET 4 is not installed in IIS.</span></span> <span data-ttu-id="f1d56-261">에 배포 하는 서버는 개발 컴퓨터에 Visual Studio 2010를 설치 하는 경우 ASP.NET 4 컴퓨터에 설치 되어 있지만 iis에서를 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-261">If the server you are deploying to is your development computer and has Visual Studio 2010 installed on it, ASP.NET 4 is installed on the computer but might not be installed in IIS.</span></span> <span data-ttu-id="f1d56-262">배포 하는 서버에서 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 하 여 IIS에서 ASP.NET 4를 설치:</span><span class="sxs-lookup"><span data-stu-id="f1d56-262">On the server that you are deploying to, open an elevated command prompt and install ASP.NET 4 in IIS by running the following commands:</span></span>

[!code-console[Main](troubleshooting/samples/sample10.cmd)]

## <a name="unable-to-cast-microsoftwebdeploymentdeploymentprovideroptions"></a><span data-ttu-id="f1d56-263">Microsoft.Web.Deployment.DeploymentProviderOptions 캐스팅할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-263">Unable to cast Microsoft.Web.Deployment.DeploymentProviderOptions</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-264">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-264">Scenario</span></span>

<span data-ttu-id="f1d56-265">패키지를 배포 하는 경우 다음 오류 메시지가 표시:</span><span class="sxs-lookup"><span data-stu-id="f1d56-265">When you are deploying a package, you see the following error message:</span></span>

<span data-ttu-id="f1d56-266">'Microsoft.Web.Deployment.DeploymentProviderOptions'를 ' Microsoft.Web.Deployment.DeploymentProviderOptions' 형식의 개체를 캐스팅할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-266">Unable to cast object of type 'Microsoft.Web.Deployment.DeploymentProviderOptions' to 'Microsoft.Web.Deployment.DeploymentProviderOptions'.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-267">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-267">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-268">웹 배포 2.0이 설치 되어 있는 서버에 웹 배포 1.1 UI를 사용 하 여 IIS 관리자에서 배포 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-268">You are trying to deploy from IIS Manager using the Web Deploy 1.1 UI to a server that has Web Deploy 2.0 installed.</span></span> <span data-ttu-id="f1d56-269">가져오기 패키지를 확인 하 여 배포 하는 IIS 원격 관리 도구를 사용 하는 경우는 **기능은 사용할 수 있는 새** 연결을 설정 하는 경우 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="f1d56-269">If you are using the IIS Remote Administration Tool to deploy by importing a package, check the **New Features Available** dialog box when you establish the connection.</span></span> <span data-ttu-id="f1d56-270">(이 대화 상자만 표시 될 수 있습니다 한 번 연결이 먼저 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-270">(This dialog box might only be shown once when the connection is first established.</span></span> <span data-ttu-id="f1d56-271">연결의 선택을 취소 하 고 다시 시작, IIS 관리자를 닫습니다 및 inetmgr을 입력 하 여 다시 시작 간 명령 프롬프트에서 다시 설정 합니다.) 나열 된 기능 중 하나 인지 **웹 배포 UI**을 8 보다 낮은 버전 번호가 있기를 배포 하는 서버 1.1 및 2.0 버전의 웹 배포 설치 되어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-271">To clear the connection and start over, close IIS Manager and start it up again by entering inetmgr /reset at the command prompt.) If one of the features listed is **Web Deploy UI**, and it has a version number lower than 8, the server you are deploying to might have both 1.1 and 2.0 versions of Web Deploy installed.</span></span> <span data-ttu-id="f1d56-272">2.0이 설치 되어 있는 클라이언트를 배포 하려면 서버에만 웹 배포 2.0이 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-272">To deploy from a client that has 2.0 installed, the server must have only Web Deploy 2.0 installed.</span></span> <span data-ttu-id="f1d56-273">이 문제를 해결 하려면 호스팅 공급자에 게 문의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-273">You will have to contact your hosting provider to resolve this problem.</span></span>

## <a name="unable-to-load-the-native-components-of-sql-server-compact"></a><span data-ttu-id="f1d56-274">SQL Server Compact의 네이티브 구성 요소를 로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-274">Unable to load the native components of SQL Server Compact</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-275">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-275">Scenario</span></span>

<span data-ttu-id="f1d56-276">배포 된 사이트를 실행 하면 다음 오류 메시지가 표시:</span><span class="sxs-lookup"><span data-stu-id="f1d56-276">When you run the deployed site, you see the following error message:</span></span>

<span data-ttu-id="f1d56-277">SQL Server compact 버전 8482 ADO.NET 공급자에 게 해당 네이티브 구성 요소를 로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-277">Unable to load the native components of SQL Server Compact corresponding to the ADO.NET provider of version 8482.</span></span> <span data-ttu-id="f1d56-278">올바른 버전의 SQL Server Compact를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-278">Install the correct version of SQL Server Compact.</span></span> <span data-ttu-id="f1d56-279">자세한 내용은 기술 자료 문서 974247 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f1d56-279">Refer to KB article 974247 for more details.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-280">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-280">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-281">배포 된 사이트에 없는 *amd64* 하 고 *x86* 하위 폴더는 응용 프로그램에 네이티브 어셈블리를 사용 하 여 *bin* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-281">The deployed site does not have *amd64* and *x86* subfolders with the native assemblies in them under the application's *bin* folder.</span></span> <span data-ttu-id="f1d56-282">SQL Server Compact 설치 된 컴퓨터에서 네이티브 어셈블리에 위치한 *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-282">On a computer that has SQL Server Compact installed, the native assemblies are located in *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*.</span></span> <span data-ttu-id="f1d56-283">Visual Studio 프로젝트에 올바른 폴더에 올바른 파일을 얻을 수 있는 최상의 방법은 NuGet SqlServerCompact 패키지를 설치 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-283">The best way to get the correct files into the correct folders in a Visual Studio project is to install the NuGet SqlServerCompact package.</span></span> <span data-ttu-id="f1d56-284">네이티브 어셈블리를 복사 하는 빌드 후 스크립트를 추가 하는 패키지 설치 *amd64* 하 고 *x86*합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-284">Package installation adds a post-build script to copy the native assemblies into *amd64* and *x86*.</span></span> <span data-ttu-id="f1d56-285">그러나 배포에 대 한 순서로 프로젝트에 수동으로 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-285">In order for these to be deployed, however, you have to manually include them in the project.</span></span> <span data-ttu-id="f1d56-286">자세한 내용은 참조는 [SQL Server Compact 배포](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-286">For more information, see the [Deploying SQL Server Compact](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) tutorial.</span></span>

## <a name="path-is-not-valid-error-after-deploying-an-entity-framework-code-first-application"></a><span data-ttu-id="f1d56-287">Entity Framework Code First 응용 프로그램을 배포한 후 "경로가 잘못 되었습니다." 오류</span><span class="sxs-lookup"><span data-stu-id="f1d56-287">"Path is not valid" error after deploying an Entity Framework Code First application</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-288">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-288">Scenario</span></span>

<span data-ttu-id="f1d56-289">SQL Server Compact 데이터베이스를 앱의 파일에 저장 하는 같은 Entity Framework Code First 마이그레이션 및 DBMS를 사용 하는 응용 프로그램을 배포한\_데이터 폴더.</span><span class="sxs-lookup"><span data-stu-id="f1d56-289">You deploy an application that uses Entity Framework Code First Migrations and a DBMS such as SQL Server Compact which stores its database in a file in the App\_Data folder.</span></span> <span data-ttu-id="f1d56-290">Code First 마이그레이션 후 첫 번째 배포 데이터베이스를 만들도록 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-290">You have Code First Migrations configured to create the database after your first deployment.</span></span> <span data-ttu-id="f1d56-291">응용 프로그램을 실행 하는 경우 다음 예제와 같이 오류 메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-291">When you run the application you get an error message like the following example:</span></span>

<span data-ttu-id="f1d56-292">경로가 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-292">The path is not valid.</span></span> <span data-ttu-id="f1d56-293">데이터베이스에 대 한 디렉터리를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-293">Check the directory for the database.</span></span> <span data-ttu-id="f1d56-294">[Path = c:\inetpub\wwwroot\App\_Data\DatabaseName.sdf ]</span><span class="sxs-lookup"><span data-stu-id="f1d56-294">[Path = c:\inetpub\wwwroot\App\_Data\DatabaseName.sdf ]</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-295">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-295">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-296">먼저 코드 데이터베이스 하지만 앱을 만들려고 시도\_데이터 폴더가 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-296">Code First is attempting to create the database but the App\_Data folder does not exist.</span></span> <span data-ttu-id="f1d56-297">에 모든 파일을 저장 하지 않은 하거나 합니다 *앱\_데이터* 를 배포 하면 또는 선택한 폴더 **제외 앱\_데이터** 에 **웹패키지및게시** 프로젝트 속성 창의 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-297">Either you didn't have any files in the *App\_Data* folder when you deployed, or you selected **Exclude App\_Data** on the **Package/Publish Web** tab of the Project Properties window.</span></span> <span data-ttu-id="f1d56-298">서버에 복사할 폴더에 파일이 없을 경우 배포 프로세스 서버에서 폴더를 만듭니다 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-298">The deployment process won't create a folder on the server if there are no files in the folder to be copied to the server.</span></span> <span data-ttu-id="f1d56-299">사이트에서 설정한 데이터베이스를 이미 설치한 경우 배포 프로세스는 파일을 삭제 하며 *앱\_데이터* 폴더를 선택한 경우 자체 **대상에서 추가 파일 제거** 에서 게시 프로필입니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-299">If you already had the database set up in the site, the deployment process will delete the files and the *App\_Data* folder itself if you selected **Remove additional files at destination** in the publish profile.</span></span> <span data-ttu-id="f1d56-300">.txt 파일과 같은 문제를 해결 하기 위해 자리 표시자 파일을 저장 합니다 *앱\_데이터* 폴더 필요가 있는지 **제외 앱\_데이터** 선택 하 고 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-300">To solve the problem, put a placeholder file such as a .txt file in the *App\_Data* folder, make sure you do not have **Exclude App\_Data** selected, and redeploy.</span></span>

## <a name="com-object-that-has-been-separated-from-its-underlying-rcw-cannot-be-used"></a><span data-ttu-id="f1d56-301">"기본 RCW에서 분리 된 COM 개체를 사용할 수 없습니다."</span><span class="sxs-lookup"><span data-stu-id="f1d56-301">"COM object that has been separated from its underlying RCW cannot be used."</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-302">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-302">Scenario</span></span>

<span data-ttu-id="f1d56-303">성공적으로 되었습니다 한 번의 클릭을 사용 하 여 응용 프로그램 배포를 게시 하 고이 오류를 가져오기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-303">You have been successfully using one-click publish to deploy your application and then you start getting this error:</span></span>

<span data-ttu-id="f1d56-304">Web deployment 작업에 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-304">Web deployment task failed.</span></span> <span data-ttu-id="f1d56-305">(원격 에이전트 URL로 요청을 완료할 수 없습니다 '<https://serverurl.com/msdeploy.axd?site=sitename>'.)</span><span class="sxs-lookup"><span data-stu-id="f1d56-305">(Could not complete the request to remote agent URL '<https://serverurl.com/msdeploy.axd?site=sitename>'.)</span></span>  
 <span data-ttu-id="f1d56-306">원격 에이전트 URL로 요청을 완료할 수 없습니다 '<https://url/msdeploy.axd?site=sitename>'.</span><span class="sxs-lookup"><span data-stu-id="f1d56-306">Could not complete the request to remote agent URL '<https://url/msdeploy.axd?site=sitename>'.</span></span>  
<span data-ttu-id="f1d56-307">요청이 중단 되었습니다: 요청이 취소 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-307">The request was aborted: The request was canceled.</span></span>  
<span data-ttu-id="f1d56-308">기본 RCW에서 분리 된 COM 개체를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-308">COM object that has been separated from its underlying RCW cannot be used.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-309">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-309">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-310">닫고 Visual Studio를 다시 시작은 일반적으로이 오류를 해결 하는 데 필요한 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-310">Closing and restarting Visual Studio is usually all that is required to resolve this error.</span></span>

## <a name="deployment-fails-because-user-credentials-used-for-publishing-dont-have-setacl-authority"></a><span data-ttu-id="f1d56-311">배포 실패 하기 때문에 사용자 자격 증명에 사용할 게시 없는 setACL 기관</span><span class="sxs-lookup"><span data-stu-id="f1d56-311">Deployment Fails Because User Credentials Used for Publishing Don't Have setACL Authority</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-312">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-312">Scenario</span></span>

<span data-ttu-id="f1d56-313">게시 실패 수를 나타내는 오류가 있는 기관 (사용 중인 사용자 계정 없는 setACL 기관) 폴더 사용 권한을 설정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-313">Publishing fails with an error that indicates you don't have authority to set folder permissions (the user account you are using doesn't have setACL authority).</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-314">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-314">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-315">기본적으로 Visual Studio 설정 사이트의 루트 폴더에 읽기 권한 및 앱에 대 한 쓰기 권한이\_데이터 폴더.</span><span class="sxs-lookup"><span data-stu-id="f1d56-315">By default, Visual Studio sets read permissions on the root folder of the site and write permissions on the App\_Data folder.</span></span> <span data-ttu-id="f1d56-316">추가 하 여이 동작을 해제 하는 사이트 폴더에 대 한 기본 권한을 올바른지, 그리고 설정할 필요가 없습니다를 알면 **&lt;IncludeSetACLProviderOn 대상&gt;False&lt;/ IncludeSetACLProviderOnDestination&gt;** (모든 프로필 적용할).wpp.targets 파일 또는 게시 프로필 파일 (단일 프로필을 적용할).</span><span class="sxs-lookup"><span data-stu-id="f1d56-316">If you know that the default permissions on site folders are correct and do not need to be set, you disable this behavior by adding **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** to the publish profile file (to affect a single profile) or to the wpp.targets file (to affect all profiles).</span></span> <span data-ttu-id="f1d56-317">이러한 파일을 편집 하는 방법에 대 한 정보를 참조 하세요 [방법: 프로필 (.pubxml) 파일에서 배포 설정을 편집](https://msdn.microsoft.com/library/ff398069.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-317">For information about how to edit these files, see [How to: Edit Deployment Settings in Profile (.pubxml) Files](https://msdn.microsoft.com/library/ff398069.aspx).</span></span>

## <a name="access-denied-errors-when-the-application-tries-to-write-to-an-application-folder"></a><span data-ttu-id="f1d56-318">응용 프로그램을 응용 프로그램 폴더에 기록 하려고 할 때 액세스 거부 오류</span><span class="sxs-lookup"><span data-stu-id="f1d56-318">Access Denied Errors when the Application Tries to Write to an Application Folder</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-319">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-319">Scenario</span></span>

<span data-ttu-id="f1d56-320">해당 폴더에 대 한 쓰기 기관에 없기 때문에 응용 프로그램 폴더 중 하나에 파일 만들기 또는 편집 하려고 할 때 응용 프로그램 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-320">Your application errors when it tries to create or edit a file in one of the application folders, because it does not have write authority for that folder.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-321">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-321">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-322">기본적으로 Visual Studio 설정 사이트의 루트 폴더에 읽기 권한 및 앱에 대 한 쓰기 권한이\_데이터 폴더.</span><span class="sxs-lookup"><span data-stu-id="f1d56-322">By default, Visual Studio sets read permissions on the root folder of the site and write permissions on the App\_Data folder.</span></span> <span data-ttu-id="f1d56-323">응용 프로그램 하위 폴더에 대 한 쓰기 액세스에 필요한 경우이 시리즈의 자습서에서는 프로덕션 환경에 배포 폴더 사용 권한 설정에 표시 된 것 처럼 해당 폴더에 대 한 권한을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-323">If your application needs write access to a sub-folder, you can set permissions for that folder as shown in the Setting Folder Permissions and Deploying to the Production Environment tutorials in this series.</span></span> <span data-ttu-id="f1d56-324">응용 프로그램 사이트의 루트 폴더에 대 한 쓰기 액세스에 필요한 경우 추가 하 여 루트 폴더에 읽기 전용 액세스를 설정 하지 못하도록 **&lt;IncludeSetACLProviderOn 대상&gt;False&lt;/ IncludeSetACLProviderOnDestination&gt;** (모든 프로필 적용할).wpp.targets 파일 또는 게시 프로필 파일 (단일 프로필을 적용할).</span><span class="sxs-lookup"><span data-stu-id="f1d56-324">If your application needs write access to the root folder of the site, you have to prevent it from setting read-only access on the root folder by adding **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** to the publish profile file (to affect a single profile) or to the wpp.targets file (to affect all profiles).</span></span> <span data-ttu-id="f1d56-325">이러한 파일을 편집 하는 방법에 대 한 정보를 참조 하세요 [방법: 프로필 (.pubxml) 파일에서 배포 설정을 편집](https://msdn.microsoft.com/library/ff398069.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-325">For information about how to edit these files, see [How to: Edit Deployment Settings in Profile (.pubxml) Files](https://msdn.microsoft.com/library/ff398069.aspx).</span></span>

<a id="aspnet45error"></a>

## <a name="configuration-error---targetframework-attribute-references-a-version-that-is-later-than-the-installed-version-of-the-net-framework"></a><span data-ttu-id="f1d56-326">구성 오류-targetFramework 특성 참조의.NET Framework 설치 된 버전 보다 최신 버전</span><span class="sxs-lookup"><span data-stu-id="f1d56-326">Configuration Error - targetFramework attribute references a version that is later than the installed version of the .NET Framework</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-327">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-327">Scenario</span></span>

<span data-ttu-id="f1d56-328">ASP.NET 4.5를 대상으로 하는 웹 프로젝트를 성공적으로 게시 되지만 다음 오류가 발생 하면 ("꺼짐" 파일에 있는 web.config로 customErrors 모드)와 응용 프로그램을 실행 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="f1d56-328">You successfully published a web project that targets ASP.NET 4.5, but when you run the application (with the customErrors mode set to "off" in the Web.config file) you get the following error:</span></span>

<span data-ttu-id="f1d56-329">'TargetFramework' 특성을 &lt;컴파일&gt; Web.config 파일의 요소 나중의.NET Framework 4.0 대상 버전에만 사용 됩니다 (예를 들어, '&lt;컴파일 targetFramework = "4.0"&gt;').</span><span class="sxs-lookup"><span data-stu-id="f1d56-329">The 'targetFramework' attribute in the &lt;compilation&gt; element of the Web.config file is used only to target version 4.0 and later of the .NET Framework (for example, '&lt;compilation targetFramework="4.0"&gt;').</span></span> <span data-ttu-id="f1d56-330">'TargetFramework' 특성에는 현재 설치 된 버전의.NET Framework 보다 최신 버전을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-330">The 'targetFramework' attribute currently references a version that is later than the installed version of the .NET Framework.</span></span> <span data-ttu-id="f1d56-331">.NET Framework의 올바른 대상 버전을 지정 하거나.NET Framework의 필수 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-331">Specify a valid target version of the .NET Framework, or install the required version of the .NET Framework.</span></span>

<span data-ttu-id="f1d56-332">오류 페이지의 소스 오류 상자 오류의 원인으로 Web.config에서 다음 줄을 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-332">The Source Error box of the error page highlights the following line from Web.config as the cause of the error:</span></span>

<span data-ttu-id="f1d56-333">&lt;컴파일 targetFramework = "4.5" /&gt;</span><span class="sxs-lookup"><span data-stu-id="f1d56-333">&lt;compilation targetFramework="4.5" /&gt;</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-334">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-334">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-335">서버에서 ASP.NET 4.5를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-335">The server does not support ASP.NET 4.5.</span></span> <span data-ttu-id="f1d56-336">시기 및 ASP.NET 4.5에 대 한 지원을 추가할 수 있는지를 확인 하려면 호스팅 공급자에 게 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-336">Contact the hosting provider to determine when and if support for ASP.NET 4.5 can be added.</span></span> <span data-ttu-id="f1d56-337">ASP.NET 4 또는 이전 버전을 대상으로 하는 웹 프로젝트를 배포 해야 하는 서버를 업그레이드 하는 옵션이 아닌 경우 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-337">If upgrading the server is not an option, you have to deploy a web project that targets ASP.NET 4 or earlier instead.</span></span>

<span data-ttu-id="f1d56-338">동일한 대상에는 ASP.NET 4 또는 이전 웹 프로젝트를 배포 하는 경우 선택 합니다 **대상에서 추가 파일 제거** 확인란 합니다 **설정** 탭은 **웹 게시**마법사.</span><span class="sxs-lookup"><span data-stu-id="f1d56-338">If you deploy an ASP.NET 4 or earlier web project to the same destination, select the **Remove additional files at destination** check box on the **Settings** tab of the **Publish Web** wizard.</span></span> <span data-ttu-id="f1d56-339">선택 하지 않으면 **대상에서 추가 파일 제거**에 구성 오류 페이지를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-339">If you don't select **Remove additional files at destination**, you will continue to get the Configuration Error page.</span></span>

<span data-ttu-id="f1d56-340">프로젝트 **속성** windows에는 대상 프레임 워크 드롭다운 목록에 포함 되어 있지만 변경 하 여이 문제를 해결할 수 없는 **.NET Framework 4.5** 에 **.NETFramework4**.</span><span class="sxs-lookup"><span data-stu-id="f1d56-340">The project **Properties** windows includes a Target framework drop-down list, but you can't resolve this problem by just changing that from **.NET Framework 4.5** to **.NET Framework 4**.</span></span> <span data-ttu-id="f1d56-341">이전 프레임 워크 버전으로 대상 프레임 워크를 변경 하면 프로젝트는 최신 프레임 워크 버전의 어셈블리에 대 한 참조 및 여전히 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-341">If you change the target framework to an earlier framework version, the project will still have references to the later framework version's assemblies and will not run.</span></span> <span data-ttu-id="f1d56-342">해야 수동으로 해당 참조를 변경 하거나.NET Framework 4 또는 이전 버전을 대상으로 하는 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-342">You have to manually change those references or create a new project that targets .NET Framework 4 or earlier.</span></span> <span data-ttu-id="f1d56-343">자세한 내용은 [웹 사이트에 대 한.NET Framework 타기](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-343">For more information, see [.NET Framework Targeting for Web Sites](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx).</span></span>

## <a name="medium-trust-errors"></a><span data-ttu-id="f1d56-344">보통 신뢰 오류</span><span class="sxs-lookup"><span data-stu-id="f1d56-344">Medium Trust Errors</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-345">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-345">Scenario</span></span>

<span data-ttu-id="f1d56-346">프로덕션 환경에서 응용 프로그램을 실행 하는 경우에 보통 신뢰와 관련 된 오류가 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-346">When you run your application in production, it gets an error related to medium trust.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-347">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-347">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-348">많은 타사 호스팅 공급자는 몇 가지 작업을 수행할 수 없습니다는 보통 신뢰에서 웹 사이트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-348">Many third-party hosting providers run your web site in medium trust, which means that there are some things it isn't allowed to do.</span></span> <span data-ttu-id="f1d56-349">예를 들어, 응용 프로그램 코드 없습니다 Windows 레지스트리에 액세스 및 없습니다 읽기 또는 쓰기 응용 프로그램의 폴더 계층 구조 외부에 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-349">For example, application code can't access the Windows registry and can't read or write files that are outside of your application's folder hierarchy.</span></span> <span data-ttu-id="f1d56-350">기본적으로 응용 프로그램에서 실행 *완전 신뢰* 로컬 컴퓨터에서 의미 하는 응용 프로그램이 프로덕션에 배포할 때 오류가 발생 하는 작업을 수행 하는 일을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-350">By default your application runs in *full trust* on your local computer, which means that the application might be able to do things that would fail when you deploy it to production.</span></span>

<span data-ttu-id="f1d56-351">문제를 해결 하기 위해 로컬 IIS 환경에서 보통 신뢰에서 실행 되도록 응용 프로그램을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-351">You can configure the application to run in medium trust in the local IIS environment in order to troubleshoot.</span></span> <span data-ttu-id="f1d56-352">이렇게 하려면 응용 프로그램을 엽니다 *Web.config* 파일을 추가한를 **트러스트** 요소에는 **system.web** 요소를이 예와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-352">To do that, open the application *Web.config* file, and add a **trust** element in the **system.web** element, as shown in this example.</span></span>

[!code-xml[Main](troubleshooting/samples/sample11.xml)]

<span data-ttu-id="f1d56-353">응용 프로그램이 이제 로컬 컴퓨터에도 IIS에서 보통 신뢰에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-353">The application will now run in medium trust in IIS even on your local computer.</span></span>

<span data-ttu-id="f1d56-354">이 경우 작업을 수행 하지 Azure 보통 신뢰 필요 하지 않기 때문에 Azure App Service에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-354">Don't do this if you are deploying to Azure App Service, because Azure does not require medium trust.</span></span> <span data-ttu-id="f1d56-355">2012 년 2 월에에서이 자습서를 쓰고 시이 메서드를 사용 하 여 응용 프로그램을 쉽게 보통 신뢰 수준에서 실행 하면 오류가 발생 Azure에서.</span><span class="sxs-lookup"><span data-stu-id="f1d56-355">At the time this tutorial is being written in February, 2012, using this method to make your application run in medium trust will cause an error in Azure.</span></span>

<span data-ttu-id="f1d56-356">Entity Framework Code First 마이그레이션을 사용 하는 보통 신뢰 수준에서 응용 프로그램을 실행 하는 호스팅 공급자에 배포 하는 경우 버전 5.0 했는지 또는 나중에 설치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-356">If you are using Entity Framework Code First Migrations and you are deploying to a hosting provider that runs your application in medium trust, make sure that you have version 5.0 or later installed.</span></span> <span data-ttu-id="f1d56-357">Entity framework 버전 4.3, 마이그레이션 데이터베이스 스키마를 업데이트 하려면 완전 신뢰가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-357">In Entity Framework version 4.3, Migrations requires full trust in order to update the database schema.</span></span>

## <a name="http-40417-not-found-error"></a><span data-ttu-id="f1d56-358">HTTP 404.17 찾을 수 없음 오류</span><span class="sxs-lookup"><span data-stu-id="f1d56-358">HTTP 404.17 Not Found Error</span></span>

### <a name="scenario"></a><span data-ttu-id="f1d56-359">시나리오</span><span class="sxs-lookup"><span data-stu-id="f1d56-359">Scenario</span></span>

<span data-ttu-id="f1d56-360">IIS에서 개발 컴퓨터에 배포 된 사이트를 실행 하면 서버 Default.aspx를 처리할 수 없습니다를 보고 다음 오류 메시지가 표시:</span><span class="sxs-lookup"><span data-stu-id="f1d56-360">When you run the deployed site on your development computer in IIS, you see the following error message reporting that the server can't process Default.aspx:</span></span>

<span data-ttu-id="f1d56-361">HTTP 오류 404.17-찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="f1d56-361">HTTP Error 404.17 - Not Found</span></span>

<span data-ttu-id="f1d56-362">요청 된 콘텐츠를 스크립트로 및 정적 파일 처리기에서 처리 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-362">The requested content appears to be script and will not be served by the static file handler.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="f1d56-363">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="f1d56-363">Possible Cause and Solution</span></span>

<span data-ttu-id="f1d56-364">컴퓨터에 ASP.NET 4.5를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d56-364">ASP.NET 4.5 might not be installed on your computer.</span></span> <span data-ttu-id="f1d56-365">ASP.NET 4.5를 설치 하는 방법을 설명 하는이 시리즈의 자습서 테스트 환경으로 IIS에 배포의 단계를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f1d56-365">See the steps in the Deploying to IIS as a Test Environment tutorial in this series that explain how to install ASP.NET 4.5.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f1d56-366">이전</span><span class="sxs-lookup"><span data-stu-id="f1d56-366">Previous</span></span>](deploying-extra-files.md)
