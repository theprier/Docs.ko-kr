---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12
title: "SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: (12는 12 자) 문제 해결 | Microsoft Docs"
author: tdykstra
description: "이 일련의 자습서 배포 하는 방법을 보여 줍니다. (게시) ASP.NET Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: 3fc23eed-921d-4d46-a610-a2d156e4bd03
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12
msc.type: authoredcontent
ms.openlocfilehash: 50de8473d1fd77de4b221f0c96fc7f184621d4b6
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-troubleshooting-12-of-12"></a><span data-ttu-id="b3423-103">SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: (12는 12 자) 문제 해결</span><span class="sxs-lookup"><span data-stu-id="b3423-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Troubleshooting (12 of 12)</span></span>
====================
<span data-ttu-id="b3423-104">으로 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="b3423-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="b3423-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="b3423-105">Download Starter Project</span></span>](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="b3423-106">이 일련의 자습서 배포 하는 방법을 보여 줍니다. (게시)는 ASP.NET 웹에 대 한 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="b3423-107">웹 게시 업데이트를 설치 하는 경우에 Visual Studio 2010을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="b3423-108">계열에 대 한 소개를 참조 하십시오. [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="b3423-109">Visual Studio 2012 RC 릴리스 이후 도입 된 배포 기능 보여주며 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다. Windows Azure 웹 사이트를 배포 하는 방법을 보여 줍니다 하는 자습서를 참조 하십시오. [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Windows Azure Web Sites, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>


<span data-ttu-id="b3423-110">이 페이지는 Visual Studio를 사용 하 여 ASP.NET 웹 응용 프로그램을 배포할 때 발생할 수 있는 몇 가지 일반적인 문제를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-110">This page describes some common problems that may arise when you deploy an ASP.NET web application by using Visual Studio.</span></span> <span data-ttu-id="b3423-111">각 하나에 대 한 가능한 원인과 해당 솔루션을 하나 이상 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-111">For each one, one or more possible causes and corresponding solutions are provided.</span></span>

## <a name="server-error-in--application---current-custom-error-settings-prevent-details-of-the-error-from-being-viewed-remotely"></a><span data-ttu-id="b3423-112">서버 오류 원격으로 볼 수 없도록 오류 정보는 현재 사용자 지정 오류 설정으로 인해 '/' 응용 프로그램-에서</span><span class="sxs-lookup"><span data-stu-id="b3423-112">Server Error in '/' Application - Current Custom Error Settings Prevent Details of the Error from Being Viewed Remotely</span></span>

### <a name="scenario"></a><span data-ttu-id="b3423-113">시나리오</span><span class="sxs-lookup"><span data-stu-id="b3423-113">Scenario</span></span>

<span data-ttu-id="b3423-114">사이트를 원격 호스트에 배포한 후 Web.config 파일에서 customErrors 설정에 언급으로 오류의 실제 원인을 त ल ् 표시 하지 않지만 오류 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-114">After deploying a site to a remote host, you get an error message that mentions the customErrors setting in the Web.config file but doesn't indicate what the actual cause of the error was:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample1.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b3423-115">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="b3423-115">Possible Cause and Solution</span></span>

<span data-ttu-id="b3423-116">기본적으로 ASP.NET 웹 응용 프로그램은 로컬 컴퓨터에서 실행 중인 경우에 자세한 오류 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-116">By default, ASP.NET shows detailed error information only when your web application is running on the local computer.</span></span> <span data-ttu-id="b3423-117">일반적으로 때 해커 취약점을 찾는 응용 프로그램에서이 정보를 사용할 수 있을 수 때문에 웹 응용 프로그램은 인터넷을 통해 공개적으로 사용할 수 있는 자세한 오류 정보를 표시 하지 않으려면입니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-117">Generally you don't want to display detailed error information when your web application is publicly available over the Internet, because hackers may be able to use this information to find vulnerabilities in the application.</span></span> <span data-ttu-id="b3423-118">그러나 사이트에는 사이트 또는 업데이트를 배포 하려는, 경우 경우가 뭔가 잘못 되 고 실제 오류 메시지를 가져오는 데 필요.</span><span class="sxs-lookup"><span data-stu-id="b3423-118">However, when you are deploying a site or updates to a site, sometimes something will go wrong and you need to get the actual error message.</span></span>

<span data-ttu-id="b3423-119">원격 호스트에서 실행 될 경우 자세한 오류 메시지를 표시 하도록 응용 프로그램을 사용 하려면 설정 하려면 Web.config 파일을 편집 `customErrors` 모드 해제, 응용 프로그램을 다시 배포 및 응용 프로그램을 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-119">To enable the application to display detailed error messages when it runs on the remote host, edit the Web.config file to set `customErrors` mode off, redeploy the application, and run the application again:</span></span>

1. <span data-ttu-id="b3423-120">응용 프로그램 Web.config 파일에는 `customErrors` 요소에는 `system.web` 요소를 변경은 `mode` "off"로 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-120">If the application Web.config file has a `customErrors` element in the `system.web` element, change the `mode` attribute to "off".</span></span> <span data-ttu-id="b3423-121">그렇지 않은 경우 추가 `customErrors` 요소에는 `system.web` 인 요소는 `mode` 다음 예제와 같이 특성이 "off"로 설정:</span><span class="sxs-lookup"><span data-stu-id="b3423-121">Otherwise add a `customErrors` element in the `system.web` element with the `mode` attribute set to "off", as shown in the following example:</span></span>

    [!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample2.xml?highlight=3)]
2. <span data-ttu-id="b3423-122">응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-122">Deploy the application.</span></span>
3. <span data-ttu-id="b3423-123">응용 프로그램을 실행 하 고 무엇이 든 했던 이전 오류를 발생 시킨 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-123">Run the application and repeat whatever you did earlier that caused the error to occur.</span></span> <span data-ttu-id="b3423-124">이제가 실제 오류 메시지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-124">Now you can see what the actual error message is.</span></span>
4. <span data-ttu-id="b3423-125">오류를 해결 하는 경우 원래 복원 `customErrors` 설정 하 고 응용 프로그램을 재배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-125">When you have resolved the error, restore the original `customErrors` setting and redeploy the application.</span></span>

## <a name="access-is-denied-in-a-web-page-that-uses-sql-server-compact"></a><span data-ttu-id="b3423-126">액세스가 거부 되었습니다 웹 페이지에서 사용 하 여 SQL Server Compact는</span><span class="sxs-lookup"><span data-stu-id="b3423-126">Access is Denied in a Web Page that Uses SQL Server Compact</span></span>

### <a name="scenario"></a><span data-ttu-id="b3423-127">시나리오</span><span class="sxs-lookup"><span data-stu-id="b3423-127">Scenario</span></span>

<span data-ttu-id="b3423-128">SQL Server Compact를 사용 하는 사이트를 배포 하는 경우 데이터베이스에 액세스 하는 배포 된 사이트에서 페이지를 실행 하면 다음과 같은 오류 메시지가 표시:</span><span class="sxs-lookup"><span data-stu-id="b3423-128">When you deploy a site that uses SQL Server Compact and you run a page in the deployed site that accesses the database, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample3.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b3423-129">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="b3423-129">Possible Cause and Solution</span></span>

<span data-ttu-id="b3423-130">서버에서 네트워크 서비스 계정에 SQL 서비스 Compact 네이티브 이진 파일을 읽을 수 해야는 *bin\amd64* 또는 *bin\x86* 하지만 폴더에 대 한 읽기 권한이 해당 폴더에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-130">The NETWORK SERVICE account on the server needs to be able to read SQL Service Compact native binaries that are in the *bin\amd64* or *bin\x86* folder, but it does not have read permissions for those folders.</span></span> <span data-ttu-id="b3423-131">네트워크 서비스에 대 한 권한이 읽기 설정의 *bin* 폴더, 하위 폴더에 권한을 확장할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-131">Set read permission for NETWORK SERVICE on the *bin* folder, making sure to extend the permissions to subfolders.</span></span>

## <a name="cannot-read-configuration-file-due-to-insufficient-permissions"></a><span data-ttu-id="b3423-132">권한이 충분 하지 않아 구성 파일을 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-132">Cannot Read Configuration File Due to Insufficient Permissions</span></span>

### <a name="scenario"></a><span data-ttu-id="b3423-133">시나리오</span><span class="sxs-lookup"><span data-stu-id="b3423-133">Scenario</span></span>

<span data-ttu-id="b3423-134">클릭 하면 Visual Studio 게시 단추 로컬 컴퓨터의 IIS에 응용 프로그램 배포 실패를 게시 및 **출력** 창 다음과 비슷한 오류 메시지가 표시:</span><span class="sxs-lookup"><span data-stu-id="b3423-134">When you click the Visual Studio publish button to deploy an application to IIS on your local machine, publishing fails and the **Output** window shows an error message similar to this:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample4.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b3423-135">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="b3423-135">Possible Cause and Solution</span></span>

<span data-ttu-id="b3423-136">한 번의 클릭을 사용 하려면 관리자 권한으로 Visual Studio 실행 될 경우, 로컬 컴퓨터의 IIS에 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-136">To use one-click publish to IIS on your local machine, you must be running Visual Studio with administrator permissions.</span></span> <span data-ttu-id="b3423-137">Visual Studio를 닫고 관리자 권한으로 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-137">Close Visual Studio and restart it with administrator permissions.</span></span>

## <a name="could-not-connect-to-the-destination-computer--using-the-specified-process"></a><span data-ttu-id="b3423-138">대상 컴퓨터에 연결할 수 없습니다... 지정된 된 프로세스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b3423-138">Could Not Connect to the Destination Computer ... Using the Specified Process</span></span>

### <a name="scenario"></a><span data-ttu-id="b3423-139">시나리오</span><span class="sxs-lookup"><span data-stu-id="b3423-139">Scenario</span></span>

<span data-ttu-id="b3423-140">클릭 하면 Visual Studio 게시 단추 응용 프로그램 배포 실패를 게시 및 **출력** 창 다음과 비슷한 오류 메시지가 표시:</span><span class="sxs-lookup"><span data-stu-id="b3423-140">When you click the Visual Studio publish button to deploy an application, publishing fails and the **Output** window shows an error message similar to this:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample5.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b3423-141">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="b3423-141">Possible Cause and Solution</span></span>

<span data-ttu-id="b3423-142">프록시 서버는 대상 서버와의 통신을 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-142">A proxy server is interrupting communication with the destination server.</span></span> <span data-ttu-id="b3423-143">Windows 제어판에서 또는 Internet Explorer에서 선택 **인터넷 옵션** 선택 하 고는 **연결** 탭 합니다. 에 **인터넷 속성** 대화 상자를 클릭 **LAN 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-143">From the Windows Control Panel or in Internet Explorer, select **Internet Options** and select the **Connections** tab. In the **Internet Properties** dialog box, click **LAN Settings**.</span></span> <span data-ttu-id="b3423-144">에 **Local Area Network (LAN) 설정** 대화 상자에서 지우기는 **자동으로 설정 검색** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-144">In the **Local Area Network (LAN) Settings** dialog box, clear the **Automatically detect settings** checkbox.</span></span> <span data-ttu-id="b3423-145">다시 게시 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-145">Then click the publish button again.</span></span>

<span data-ttu-id="b3423-146">문제가 지속 되 면 프록시 또는 방화벽 설정을 사용 하 여 수행할 수 있는 작업을 확인 하려면 시스템 관리자에 게 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-146">If the problem persists, contact your system administrator to determine what can be done with proxy or firewall settings.</span></span> <span data-ttu-id="b3423-147">비표준 포트를 사용 하 여 웹 관리 서비스 배포 (8172;)에 대 한 웹 배포 때문에 문제가 발생 하면 다른 연결에 대 한 웹 배포 포트 80을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-147">The problem happens because Web Deploy uses a non-standard port for Web Management Service deployment (8172); for other connections, Web Deploy uses port 80.</span></span> <span data-ttu-id="b3423-148">제 3 자 호스팅 공급자에 게 배포 하는 경우 일반적으로 웹 관리 서비스를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-148">When you are deploying to a third-party hosting provider, you are typically using the Web Management Service.</span></span>

## <a name="default-net-40-application-pool-does-not-exist"></a><span data-ttu-id="b3423-149">기본.NET 4.0 응용 프로그램 풀이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-149">Default .NET 4.0 Application Pool Does Not Exist</span></span>

### <a name="scenario"></a><span data-ttu-id="b3423-150">시나리오</span><span class="sxs-lookup"><span data-stu-id="b3423-150">Scenario</span></span>

<span data-ttu-id="b3423-151">.NET Framework 4를 필요로 하는 응용 프로그램을 배포 하면 다음과 같은 오류 메시지가 표시:</span><span class="sxs-lookup"><span data-stu-id="b3423-151">When you deploy an application that requires the .NET Framework 4, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample6.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b3423-152">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="b3423-152">Possible Cause and Solution</span></span>

<span data-ttu-id="b3423-153">IIS에서 ASP.NET 4 설치 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-153">ASP.NET 4 is not installed in IIS.</span></span> <span data-ttu-id="b3423-154">에 배포 하는 서버는 개발 컴퓨터에 Visual Studio 2010를 설치 하는 경우 ASP.NET 4는 컴퓨터에 설치 되어 있지만 IIS에 설치 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-154">If the server you are deploying to is your development computer and has Visual Studio 2010 installed on it, ASP.NET 4 is installed on the computer but might not be installed in IIS.</span></span> <span data-ttu-id="b3423-155">에 배포 하는 서버에서 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 하 여 IIS에서 ASP.NET 4를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-155">On the server that you are deploying to, open an elevated command prompt and install ASP.NET 4 in IIS by running the following commands:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample7.cmd)]

<span data-ttu-id="b3423-156">기본 응용 프로그램 풀의.NET Framework 버전을 수동으로 설정 하려면 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-156">You might also need to manually set the .NET Framework version of the default application pool.</span></span> <span data-ttu-id="b3423-157">자세한 내용은 참조는 [iis 테스트 환경으로 배포](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-157">For more information, see the [Deploying to IIS as a Test Environment](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) tutorial.</span></span>

## <a name="format-of-the-initialization-string-does-not-conform-to-specification-starting-at-index-0"></a><span data-ttu-id="b3423-158">초기화 문자열의 형식이 인덱스 0부터 시작 하는 사양에 맞지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-158">Format of the initialization string does not conform to specification starting at index 0.</span></span>

### <a name="scenario"></a><span data-ttu-id="b3423-159">시나리오</span><span class="sxs-lookup"><span data-stu-id="b3423-159">Scenario</span></span>

<span data-ttu-id="b3423-160">한 번의 클릭을 사용 하 여 응용 프로그램을 배포한 후 게시를 얻으면 데이터베이스에 액세스 하는 페이지를 실행 하면 다음 오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="b3423-160">After you deploy an application using one-click publish, when you run a page that accesses the database you get the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample8.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b3423-161">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="b3423-161">Possible Cause and Solution</span></span>

<span data-ttu-id="b3423-162">열기는 *Web.config* 배포 된 사이트와 연결 문자열 값으로 시작 하는지 여부를 확인의 파일 `$(ReplacableToken_`다음 예제와 같이,:</span><span class="sxs-lookup"><span data-stu-id="b3423-162">Open the *Web.config* file in the deployed site and check to see whether the connection string values begin with `$(ReplacableToken_`, as in the following example:</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample9.xml)]

<span data-ttu-id="b3423-163">이 예제와 같이 연결 문자열을 하는 경우 프로젝트 파일을 편집 하 고 다음 속성을 추가 하는 `PropertyGroup` 에 모든 빌드 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="b3423-163">If the connection strings look like this example, edit the project file and add the following property to the `PropertyGroup` element that is for all build configurations:</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample10.xml)]

<span data-ttu-id="b3423-164">그런 다음 응용 프로그램을 재배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-164">Then redeploy the application.</span></span>

## <a name="http-500-internal-server-error"></a><span data-ttu-id="b3423-165">HTTP 500 내부 서버 오류</span><span class="sxs-lookup"><span data-stu-id="b3423-165">HTTP 500 Internal Server Error</span></span>

### <a name="scenario"></a><span data-ttu-id="b3423-166">시나리오</span><span class="sxs-lookup"><span data-stu-id="b3423-166">Scenario</span></span>

<span data-ttu-id="b3423-167">배포 된 사이트를 실행 하면 오류의 원인을 나타내는 구체적인 정보 없는 다음과 같은 오류 메시지가 참조:</span><span class="sxs-lookup"><span data-stu-id="b3423-167">When you run the deployed site, you see the following error message without specific information indicating the cause of the error:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample11.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b3423-168">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="b3423-168">Possible Cause and Solution</span></span>

<span data-ttu-id="b3423-169">500 오류의 원인이 많습니다 있지만 XML 변환 파일 중 하나에 잘못 된 위치에는 XML 요소를 배치 하는 오류가 발생 하는 경우 이러한 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-169">There are many causes of 500 errors, but one possible cause if you are following these tutorials is that you put an XML element in the wrong place in one of the XML transformation files.</span></span> <span data-ttu-id="b3423-170">예를 들어 삽입 하는 변환 입력 된 경우이 오류가 발생할 것 있습니다는 `<location>` 요소 아래의 `<system.web>` 대신 바로 아래 `<configuration>`합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-170">For example, you would get this error if you put the transformation that inserts a `<location>` element under `<system.web>` instead of directly under `<configuration>`.</span></span> <span data-ttu-id="b3423-171">이 경우 방법은 XML 변환 파일을 수정 하 여 다시 배포할입니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-171">The solution in that case is to correct the XML transformation file and redeploy.</span></span>

## <a name="http-50021-internal-server-error"></a><span data-ttu-id="b3423-172">HTTP 500.21 내부 서버 오류</span><span class="sxs-lookup"><span data-stu-id="b3423-172">HTTP 500.21 Internal Server Error</span></span>

### <a name="scenario"></a><span data-ttu-id="b3423-173">시나리오</span><span class="sxs-lookup"><span data-stu-id="b3423-173">Scenario</span></span>

<span data-ttu-id="b3423-174">배포 된 사이트를 실행 하면 다음과 같은 오류 메시지가 표시:</span><span class="sxs-lookup"><span data-stu-id="b3423-174">When you run the deployed site, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample12.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b3423-175">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="b3423-175">Possible Cause and Solution</span></span>

<span data-ttu-id="b3423-176">사이트 대상이 ASP.NET 4 있지만 ASP.NET 4에에서 등록 되지 않은 IIS 서버에 배포 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-176">The site you have deployed targets ASP.NET 4, but ASP.NET 4 is not registered in IIS on the server.</span></span> <span data-ttu-id="b3423-177">서버에서 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 하 여 ASP.NET 4를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-177">On the server open an elevated command prompt and register ASP.NET 4 by running the following commands:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample13.cmd)]

<span data-ttu-id="b3423-178">기본 응용 프로그램 풀의.NET Framework 버전을 수동으로 설정 하려면 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-178">You might also need to manually set the .NET Framework version of the default application pool.</span></span> <span data-ttu-id="b3423-179">자세한 내용은 참조는 [iis 테스트 환경으로 배포](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-179">For more information, see the [Deploying to IIS as a Test Environment](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) tutorial.</span></span>

## <a name="login-failed-opening-sql-server-express-database-in-appdata"></a><span data-ttu-id="b3423-180">SQL Server Express 데이터베이스를 여는 앱에서 로그인이 실패 했습니다\_데이터</span><span class="sxs-lookup"><span data-stu-id="b3423-180">Login Failed Opening SQL Server Express Database in App\_Data</span></span>

### <a name="scenario"></a><span data-ttu-id="b3423-181">시나리오</span><span class="sxs-lookup"><span data-stu-id="b3423-181">Scenario</span></span>

<span data-ttu-id="b3423-182">업데이트는 *Web.config* 으로 SQL Server Express 데이터베이스를 가리키도록 연결 문자열을 파일는 *.mdf* 파일을 여 *앱\_데이터* 폴더를 찾아 첫 번째 다음과 같은 오류 메시지가 나타나면 응용 프로그램을 실행 하는 시간:</span><span class="sxs-lookup"><span data-stu-id="b3423-182">You updated the *Web.config* file connection string to point to a SQL Server Express database as an *.mdf* file in your *App\_Data* folder, and the first time you run the application you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample14.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b3423-183">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="b3423-183">Possible Cause and Solution</span></span>

<span data-ttu-id="b3423-184">이름에서 *.mdf* 파일 삭제 한 경우에 컴퓨터에서 현재까지 존재 하는 모든 SQL Server Express 데이터베이스의 이름을 일치할 수 없습니다는 *.mdf* 에 기존 데이터베이스의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-184">The name of the *.mdf* file cannot match the name of any SQL Server Express database that has ever existed on your computer, even if you deleted the *.mdf* file of the previously existing database.</span></span> <span data-ttu-id="b3423-185">이름을 변경는 *.mdf* 데이터베이스 이름 및 변경에 따라 사용 되지 않은 이름으로 파일은 *Web.config* 파일을 새 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-185">Change the name of the *.mdf* file to a name that has never been used as a database name and change the *Web.config* file to use the new name.</span></span> <span data-ttu-id="b3423-186">사용할 수 있습니다 [SQL Server Management Studio Express](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&amp;id=7593) 데이터베이스에 기존 SQL Server Express를 삭제 하려면.</span><span class="sxs-lookup"><span data-stu-id="b3423-186">As an alternative, you can use [SQL Server Management Studio Express](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&amp;id=7593) to delete previously existing SQL Server Express databases.</span></span>

## <a name="model-compatibility-cannot-be-checked"></a><span data-ttu-id="b3423-187">검사할 모델 호환성 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-187">Model Compatibility Cannot be Checked</span></span>

### <a name="scenario"></a><span data-ttu-id="b3423-188">시나리오</span><span class="sxs-lookup"><span data-stu-id="b3423-188">Scenario</span></span>

<span data-ttu-id="b3423-189">업데이트는 *Web.config* 새 SQL Server Express 데이터베이스를 가리키도록 연결 문자열을 파일을 처음으로 응용 프로그램을 실행 하면 다음과 같은 오류 메시지가 표시:</span><span class="sxs-lookup"><span data-stu-id="b3423-189">You updated the *Web.config* file connection string to point to a new SQL Server Express database, and the first time you run the application you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample15.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b3423-190">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="b3423-190">Possible Cause and Solution</span></span>

<span data-ttu-id="b3423-191">컴퓨터에 데이터베이스 이미 존재할 수 일부 테이블과 전에 Web.config 파일에 두면 데이터베이스 이름을 사용 적이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-191">If the database name you put in the Web.config file was ever used before on your computer, a database might already exist with some tables in it.</span></span> <span data-ttu-id="b3423-192">변경 및 하기 전에 컴퓨터에 사용 하지 않은 새 이름 선택는 *Web.config* 이 새 데이터베이스 이름을 사용 하 여 가리키도록 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-192">Select a new name that has not been used on your computer before and change the *Web.config* file to point to use this new database name.</span></span> <span data-ttu-id="b3423-193">사용할 수 있습니다 [SQL Server Express 유틸리티](https://www.microsoft.com/en-us/download/details.aspx?DisplayLang=en&amp;id=3990) 또는 [SQL Server Management Studio Express](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&amp;id=7593) 기존 데이터베이스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-193">As an alternative, you can use [SQL Server Express Utility](https://www.microsoft.com/en-us/download/details.aspx?DisplayLang=en&amp;id=3990) or [SQL Server Management Studio Express](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&amp;id=7593) to delete the existing database.</span></span>

## <a name="sql-error-when-a-script-attempts-to-create-users-or-roles"></a><span data-ttu-id="b3423-194">SQL 오류는 스크립트가 사용자 또는 역할을 만들려고 시도 하는 경우</span><span class="sxs-lookup"><span data-stu-id="b3423-194">SQL Error When a Script Attempts to Create Users or Roles</span></span>

### <a name="scenario"></a><span data-ttu-id="b3423-195">시나리오</span><span class="sxs-lookup"><span data-stu-id="b3423-195">Scenario</span></span>

<span data-ttu-id="b3423-196">에 구성 된 데이터베이스 배포를 사용 하는 **SQL 패키지 및 게시** 탭에서 배포 하는 동안 실행 되는 SQL 스크립트 Create User 또는 역할 만들기 명령 및 포함 스크립트 실행할 수 없으며 이러한 명령이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-196">You are using database deployment configured on the **Package/Publish SQL** tab, SQL scripts that run during deployment include Create User or Create Role commands, and script execution fails when those commands are executed.</span></span> <span data-ttu-id="b3423-197">더 자세한 다음과 같은 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-197">You might see more detailed messages, such as the following:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample16.cmd)]

<span data-ttu-id="b3423-198">에 데이터베이스 배포를 구성한 경우이 오류가 발생 하는 경우는 **웹 게시** 마법사 보다는 **SQL 패키지 및 게시** 탭에서 스레드를 만들는 [구성 및 배포](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) 포럼과 솔루션 문제 해결이 페이지에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-198">If this error occurs when you have configured database deployment in the **Publish Web** wizard rather than the **Package/Publish SQL** tab, create a thread in the [Configuration and Deployment](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) forum, and the solution will be added to this troubleshooting page.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b3423-199">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="b3423-199">Possible Cause and Solution</span></span>

<span data-ttu-id="b3423-200">배포를 수행 하는 사용 하는 사용자 계정에 사용자 또는 역할을 만들 수 있는 권한이 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-200">The user account you are using to perform deployment does not have permission to create users or roles.</span></span> <span data-ttu-id="b3423-201">예를 들어, 호스팅 회사 할당할 수는 `db_datareader`, `db_datawriter`, 및 `db_ddladmin` 를 설정 하는 사용자 계정에는 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-201">For example, the hosting company might assign the `db_datareader`, `db_datawriter`, and `db_ddladmin` roles to the user account that it sets up for you.</span></span> <span data-ttu-id="b3423-202">충분 한 이들은 대부분의 데이터베이스 개체를 만들기 위한 하지만 사용자 또는 역할을 만들기 위한 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-202">These are sufficient for creating most database objects, but not for creating users or roles.</span></span> <span data-ttu-id="b3423-203">오류를 방지 하기 위해 한 가지 방법은 데이터베이스 배포에서 사용자 및 역할을 제외 하 여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-203">One way to avoid the error is by excluding users and roles from database deployment.</span></span> <span data-ttu-id="b3423-204">편집 하 여이 작업을 수행할 수는 `PreSource` 요소는 데이터베이스에 대 한의 자동으로 생성 된 스크립트는 다음과 같은 특성이 포함 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-204">You can do this by editing the `PreSource` element for the database's automatically generated script so that it includes the following attributes:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample17.cmd)]

<span data-ttu-id="b3423-205">편집 하는 방법에 대 한 내용은 `PreSource` 프로젝트 파일의 요소 참조 [하는 방법: 프로젝트 파일에서 배포 설정을 편집](https://msdn.microsoft.com/en-us/library/ff398069(v=vs.100).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-205">For information about how to edit the `PreSource` element in the project file, see [How to: Edit Deployment Settings in the Project File](https://msdn.microsoft.com/en-us/library/ff398069(v=vs.100).aspx).</span></span> <span data-ttu-id="b3423-206">사용자 또는 역할 개발 데이터베이스의 대상 데이터베이스에 저장할 필요가, 호스팅 제공 업체를에 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b3423-206">If the users or roles in your development database need to be in the destination database, contact your hosting provider for assistance.</span></span>

## <a name="sql-server-timeout-error-when-running-custom-scripts-during-deployment"></a><span data-ttu-id="b3423-207">배포 하는 동안 사용자 지정 스크립트를 실행 하는 경우 SQL Server 시간 초과 오류</span><span class="sxs-lookup"><span data-stu-id="b3423-207">SQL Server Timeout Error When Running Custom Scripts During Deployment</span></span>

### <a name="scenario"></a><span data-ttu-id="b3423-208">시나리오</span><span class="sxs-lookup"><span data-stu-id="b3423-208">Scenario</span></span>

<span data-ttu-id="b3423-209">사용자 지정 SQL 스크립트를 배포 하는 동안 실행할 지정한 및 제한 시간 실행 될 때 웹 배포에 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-209">You have specified custom SQL scripts to run during deployment, and when Web Deploy runs them, they time out.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b3423-210">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="b3423-210">Possible Cause and Solution</span></span>

<span data-ttu-id="b3423-211">다른 트랜잭션 모드에 있는 여러 스크립트를 실행 하면 시간 초과 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-211">Running multiple scripts that have different transaction modes can cause time-out errors.</span></span> <span data-ttu-id="b3423-212">기본적으로 자동으로 생성 된 스크립트는 트랜잭션에서 실행 되지만 사용자 지정 스크립트는 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-212">By default, automatically generated scripts run in a transaction, but custom scripts do not.</span></span> <span data-ttu-id="b3423-213">선택 하는 경우는 **데이터 및/또는 기존 데이터베이스에서 스키마 가져오기** 옵션에 **SQL 패키지 및 게시** 탭 사용자 지정 SQL 스크립트를 추가 하는 경우에 일부 스크립트의 트랜잭션 설정을 변경 해야 하 고 있도록 모든 스크립트에서 동일한 트랜잭션 설정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-213">If you select the **Pull data and/or schema from an existing database** option on the **Package/Publish SQL** tab, and if you add a custom SQL script, you must change transaction settings on some scripts so that all scripts use the same transaction settings.</span></span> <span data-ttu-id="b3423-214">자세한 내용은 참조 [하는 방법: 한 데이터베이스와 웹 응용 프로그램 프로젝트를 배포](https://msdn.microsoft.com/en-us/library/dd465343.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-214">For more information, see [How to: Deploy a Database With a Web Application Project](https://msdn.microsoft.com/en-us/library/dd465343.aspx).</span></span>

<span data-ttu-id="b3423-215">모든 있도록 동일한 트랜잭션 설정을 구성 해도이 오류가 여전히 발생 하는 경우 가능한 해결 방법은 개별적으로 스크립트를 실행 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-215">If you have configured transaction settings so that all are the same but still get this error, a possible workaround is to run the scripts separately.</span></span> <span data-ttu-id="b3423-216">에 **데이터베이스 스크립트** 표에 **패키지/게시** SQL 탭을 선택 취소는 **Include** 제한 시간 오류를 발생 하는 스크립트에 대 한 확인란은 다음 프로젝트를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-216">In the **Database Scripts** grid in the **Package/Publish** SQL tab, clear the **Include** check box for the script that causes the timeout error, then publish the project.</span></span> <span data-ttu-id="b3423-217">다시으로 이동한 다음는 **데이터베이스 스크립트** 표에서 해당 스크립트를 선택 **Include** 확인란을 선택한의 선택을 취소는 **Include** 다른 스크립트에 대 한 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-217">Then go back into the **Database Scripts** grid, select that script's **Include** check box, and clear the **Include** check boxes for the other scripts.</span></span> <span data-ttu-id="b3423-218">그런 다음 프로젝트를 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-218">Then publish the project again.</span></span> <span data-ttu-id="b3423-219">이 이번에 게시할 때, 선택한 사용자 지정 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-219">This time when you publish, only the selected custom script runs.</span></span>

## <a name="stream-data-of-site-manifest-is-not-yet-available"></a><span data-ttu-id="b3423-220">사이트 매니페스트의 스트림 데이터를 아직 사용할 수</span><span class="sxs-lookup"><span data-stu-id="b3423-220">Stream Data of Site Manifest Is Not Yet Available</span></span>

### <a name="scenario"></a><span data-ttu-id="b3423-221">시나리오</span><span class="sxs-lookup"><span data-stu-id="b3423-221">Scenario</span></span>

<span data-ttu-id="b3423-222">설치 하는 경우 사용 하 여 패키지는 *deploy.cmd* 파일는 `t` (테스트) 옵션을 다음 오류 메시지가 표시:</span><span class="sxs-lookup"><span data-stu-id="b3423-222">When you are installing a package using the *deploy.cmd* file with the `t` (test) option, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample18.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b3423-223">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="b3423-223">Possible Cause and Solution</span></span>

<span data-ttu-id="b3423-224">오류 메시지 명령을 테스트 보고서를 생성할 수 없는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-224">The error message means that the command cannot produce a test report.</span></span> <span data-ttu-id="b3423-225">그러나 명령을 사용 하는 경우 실행 될 수 있습니다는 `y` (실제 설치) 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-225">However, the command might run if you use the `y` (actual installation) option.</span></span> <span data-ttu-id="b3423-226">메시지는 테스트 모드에서 명령을 실행에 문제가 있다는 것만 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-226">The message indicates only that there is a problem with running the command in test mode.</span></span>

## <a name="this-application-requires-managedruntimeversion-v40"></a><span data-ttu-id="b3423-227">이 응용 프로그램 필요 ManagedRuntimeVersion v4.0</span><span class="sxs-lookup"><span data-stu-id="b3423-227">This Application Requires ManagedRuntimeVersion v4.0</span></span>

### <a name="scenario"></a><span data-ttu-id="b3423-228">시나리오</span><span class="sxs-lookup"><span data-stu-id="b3423-228">Scenario</span></span>

<span data-ttu-id="b3423-229">배포 하려고 하면 다음과 같은 오류 메시지가 표시:</span><span class="sxs-lookup"><span data-stu-id="b3423-229">When you attempt to deploy, you see the following error message:</span></span>

 <span data-ttu-id="b3423-230">오류:의 스트림 데이터 ' sitemanifest/dbFullSql [@path= 'C:\TEMP\AdventureWorksGrant.sql']/sqlScript'를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-230">Error: The stream data of 'sitemanifest/dbFullSql[@path='C:\TEMP\AdventureWorksGrant.sql']/sqlScript' is not yet available.</span></span> <span data-ttu-id="b3423-231">사용 하도록 시도 하 고 있는 응용 프로그램 풀에 'managedRuntimeVersion' 속성이 'v2.0'로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-231">The application pool that you are trying to use has the 'managedRuntimeVersion' property set to 'v2.0'.</span></span> <span data-ttu-id="b3423-232">이 응용 프로그램 'v4.0' 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-232">This application requires 'v4.0'.</span></span> 

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b3423-233">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="b3423-233">Possible Cause and Solution</span></span>

<span data-ttu-id="b3423-234">IIS에서 ASP.NET 4 설치 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-234">ASP.NET 4 is not installed in IIS.</span></span> <span data-ttu-id="b3423-235">에 배포 하는 서버는 개발 컴퓨터에 Visual Studio 2010를 설치 하는 경우 ASP.NET 4는 컴퓨터에 설치 되어 있지만 IIS에 설치 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-235">If the server you are deploying to is your development computer and has Visual Studio 2010 installed on it, ASP.NET 4 is installed on the computer but might not be installed in IIS.</span></span> <span data-ttu-id="b3423-236">에 배포 하는 서버에서 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 하 여 IIS에서 ASP.NET 4를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-236">On the server that you are deploying to, open an elevated command prompt and install ASP.NET 4 in IIS by running the following commands:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample19.cmd)]

## <a name="unable-to-cast-microsoftwebdeploymentdeploymentprovideroptions"></a><span data-ttu-id="b3423-237">Microsoft.Web.Deployment.DeploymentProviderOptions 캐스팅할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-237">Unable to cast Microsoft.Web.Deployment.DeploymentProviderOptions</span></span>

### <a name="scenario"></a><span data-ttu-id="b3423-238">시나리오</span><span class="sxs-lookup"><span data-stu-id="b3423-238">Scenario</span></span>

<span data-ttu-id="b3423-239">패키지를 배포 하는 경우 다음과 같은 오류 메시지가 표시:</span><span class="sxs-lookup"><span data-stu-id="b3423-239">When you are deploying a package, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample20.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b3423-240">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="b3423-240">Possible Cause and Solution</span></span>

<span data-ttu-id="b3423-241">웹 배포 2.0이 설치 되어 있는 서버에 웹 배포 1.1 UI를 사용 하 여 IIS 관리자에서 배포 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-241">You are trying to deploy from IIS Manager using the Web Deploy 1.1 UI to a server that has Web Deploy 2.0 installed.</span></span> <span data-ttu-id="b3423-242">검사 패키지를 가져와서 배포 하는 IIS 원격 관리 도구를 사용 하는 경우는 **새로운 사용 가능한 기능** 대화 상자에서 연결을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-242">If you are using the IIS Remote Administration Tool to deploy by importing a package, check the **New Features Available** dialog box when you establish the connection.</span></span> <span data-ttu-id="b3423-243">(이 대화 상자 수만 표시 됩니다 한 번 연결을 먼저 설정.</span><span class="sxs-lookup"><span data-stu-id="b3423-243">(This dialog box might only be shown once when the connection is first established.</span></span> <span data-ttu-id="b3423-244">연결의 선택을 취소 하 고 다시 시작, IIS 관리자를 닫습니다를 입력 하 여 다시 시작 `inetmgr /reset` 명령 프롬프트에서.) 나열 된 기능 중 하나 인지 **웹 배포 UI**, 및 8 보다 낮은 버전 번호가 있기, 배포 하는 서버에 웹 배포 설치의 버전 1.1 및 2.0이 모두 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-244">To clear the connection and start over, close IIS Manager and start it up again by entering `inetmgr /reset` at the command prompt.) If one of the features listed is **Web Deploy UI**, and it has a version number lower than 8, the server you are deploying to might have both 1.1 and 2.0 versions of Web Deploy installed.</span></span> <span data-ttu-id="b3423-245">2.0이 설치 된 클라이언트를 배포 하려면 서버에만 웹 배포 2.0이 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-245">To deploy from a client that has 2.0 installed, the server must have only Web Deploy 2.0 installed.</span></span> <span data-ttu-id="b3423-246">이 문제를 해결 하려면 호스팅 공급자에 게 문의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-246">You will have to contact your hosting provider to resolve this problem.</span></span>

## <a name="unable-to-load-the-native-components-of-sql-server-compact"></a><span data-ttu-id="b3423-247">SQL Server Compact의 기본 구성 요소를 로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-247">Unable to load the native components of SQL Server Compact</span></span>

### <a name="scenario"></a><span data-ttu-id="b3423-248">시나리오</span><span class="sxs-lookup"><span data-stu-id="b3423-248">Scenario</span></span>

<span data-ttu-id="b3423-249">배포 된 사이트를 실행 하면 다음과 같은 오류 메시지가 표시:</span><span class="sxs-lookup"><span data-stu-id="b3423-249">When you run the deployed site, you see the following error message:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample21.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b3423-250">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="b3423-250">Possible Cause and Solution</span></span>

<span data-ttu-id="b3423-251">배포 된 사이트에 없는 *amd64* 및 *x86* 하위 폴더에는 응용 프로그램의 네이티브 어셈블리와 함께 *bin* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-251">The deployed site does not have *amd64* and *x86* subfolders with the native assemblies in them under the application's *bin* folder.</span></span> <span data-ttu-id="b3423-252">SQL Server Compact 설치 되어 있는 컴퓨터에서 네이티브 어셈블리에 있는 *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-252">On a computer that has SQL Server Compact installed, the native assemblies are located in *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*.</span></span> <span data-ttu-id="b3423-253">Visual Studio 프로젝트의 올바른 폴더에 올바른 파일을 가져올 수는 가장 좋은 방법은 NuGet SqlServerCompact 패키지를 설치 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-253">The best way to get the correct files into the correct folders in a Visual Studio project is to install the NuGet SqlServerCompact package.</span></span> <span data-ttu-id="b3423-254">네이티브 어셈블리를 복사 하는 빌드 후 스크립트를 추가 하는 패키지 설치 *amd64* 및 *x86*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-254">Package installation adds a post-build script to copy the native assemblies into *amd64* and *x86*.</span></span> <span data-ttu-id="b3423-255">그러나이 배포를 위해 프로젝트에이 수동으로 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-255">In order for these to be deployed, however, you have to manually include them in the project.</span></span> <span data-ttu-id="b3423-256">자세한 내용은 참조는 [SQL Server Compact 배포](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-256">For more information, see the [Deploying SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) tutorial.</span></span>

## <a name="path-is-not-valid-error-after-deploying-an-entity-framework-code-first-application"></a><span data-ttu-id="b3423-257">Entity Framework Code First 응용 프로그램을 배포한 후 "경로가 잘못 되었습니다." 오류</span><span class="sxs-lookup"><span data-stu-id="b3423-257">"Path is not valid" error after deploying an Entity Framework Code First application</span></span>

### <a name="scenario"></a><span data-ttu-id="b3423-258">시나리오</span><span class="sxs-lookup"><span data-stu-id="b3423-258">Scenario</span></span>

<span data-ttu-id="b3423-259">Entity Framework Code First 마이그레이션 및 DBMS를 사용 하 여 SQL Server Compact는 데이터베이스 응용 프로그램의 파일에 저장 하는 등 응용 프로그램을 배포할\_데이터 폴더.</span><span class="sxs-lookup"><span data-stu-id="b3423-259">You deploy an application that uses Entity Framework Code First Migrations and a DBMS such as SQL Server Compact which stores its database in a file in the App\_Data folder.</span></span> <span data-ttu-id="b3423-260">Code First 마이그레이션을 첫 번째 배포 후 데이터베이스를 생성 하도록 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-260">You have Code First Migrations configured to create the database after your first deployment.</span></span> <span data-ttu-id="b3423-261">응용 프로그램을 실행 하는 경우에 다음 예제와 같은 오류 메시지가 나타날:</span><span class="sxs-lookup"><span data-stu-id="b3423-261">When you run the application you get an error message like the following example:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample22.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b3423-262">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="b3423-262">Possible Cause and Solution</span></span>

<span data-ttu-id="b3423-263">코드 되지만 응용 프로그램 데이터베이스를 먼저 만들려고\_데이터 폴더가 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-263">Code First is attempting to create the database but the App\_Data folder does not exist.</span></span> <span data-ttu-id="b3423-264">하거나 필요가 모든 파일는 *앱\_데이터* 폴더에 배포 하거나 선택한 **제외 앱\_데이터** 에 **웹패키지및게시** 탭은 **프로젝트 속성** 창.</span><span class="sxs-lookup"><span data-stu-id="b3423-264">Either you didn't have any files in the *App\_Data* folder when you deployed, or you selected **Exclude App\_Data** on the **Package/Publish Web** tab of the **Project Properties** window.</span></span> <span data-ttu-id="b3423-265">서버에 복사할 폴더에 파일이 없는 경우 배포 프로세스 서버에 폴더를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-265">The deployment process won't create a folder on the server if there are no files in the folder to be copied to the server.</span></span> <span data-ttu-id="b3423-266">사이트에서 설정한 데이터베이스를 이미 설치한 경우 배포 프로세스 파일은 삭제 및 *앱\_데이터* 폴더를 선택한 경우 자체 **대상에서 추가 파일 제거** 에서 게시 프로필입니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-266">If you already had the database set up in the site, the deployment process will delete the files and the *App\_Data* folder itself if you selected **Remove additional files at destination** in the publish profile.</span></span> <span data-ttu-id="b3423-267">.txt 파일 문제를 해결 하기 위해 자리 표시자 파일을 저장는 *앱\_데이터* 폴더를 포함 하지 않는지 확인 **제외 앱\_데이터** 선택 하 고 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-267">To solve the problem, put a placeholder file such as a .txt file in the *App\_Data* folder, make sure you do not have **Exclude App\_Data** selected, and redeploy.</span></span> 

## <a name="com-object-that-has-been-separated-from-its-underlying-rcw-cannot-be-used"></a><span data-ttu-id="b3423-268">"기본 RCW에서 분리 된 COM 개체를 사용할 수 없습니다."</span><span class="sxs-lookup"><span data-stu-id="b3423-268">"COM object that has been separated from its underlying RCW cannot be used."</span></span>

### <a name="scenario"></a><span data-ttu-id="b3423-269">시나리오</span><span class="sxs-lookup"><span data-stu-id="b3423-269">Scenario</span></span>

<span data-ttu-id="b3423-270">성공적으로 된 응용 프로그램 배포를 게시 한 번의 클릭을 사용 하 고이 오류를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-270">You have been successfully using one-click publish to deploy your application and then you start getting this error:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample23.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b3423-271">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="b3423-271">Possible Cause and Solution</span></span>

<span data-ttu-id="b3423-272">닫았다가 Visual Studio를 다시 시작은 일반적으로이 오류를 해결 하는 데 필요한 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-272">Closing and restarting Visual Studio is usually all that is required to resolve this error.</span></span>

## <a name="deployment-fails-because-user-credentials-used-for-publishing-dont-have-setacl-authority"></a><span data-ttu-id="b3423-273">배포 실패 하기 때문에 사용자 자격 증명에 사용 게시 없는 setACL 기관</span><span class="sxs-lookup"><span data-stu-id="b3423-273">Deployment Fails Because User Credentials Used for Publishing Don't Have setACL Authority</span></span>

### <a name="scenario"></a><span data-ttu-id="b3423-274">시나리오</span><span class="sxs-lookup"><span data-stu-id="b3423-274">Scenario</span></span>

<span data-ttu-id="b3423-275">표시 되는 오류와 함께 게시 실패 (사용 하는 사용자 계정이 없는 경우 setACL 기관) 폴더 사용 권한을 설정할 권한이 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-275">Publishing fails with an error that indicates you don't have authority to set folder permissions (the user account you are using doesn't have setACL authority).</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b3423-276">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="b3423-276">Possible Cause and Solution</span></span>

<span data-ttu-id="b3423-277">기본적으로 Visual Studio 집합 사이트의 루트 폴더에 읽기 권한 및 앱에 대 한 쓰기 권한이\_데이터 폴더.</span><span class="sxs-lookup"><span data-stu-id="b3423-277">By default, Visual Studio sets read permissions on the root folder of the site and write permissions on the App\_Data folder.</span></span> <span data-ttu-id="b3423-278">이 동작을 사용 하지 않도록 추가 하 여 사이트 폴더에 대 한 기본 권한을 올바르고 설정할 필요가 없습니다 하는지 알고 있는 경우  **&lt;IncludeSetACLProviderOn 대상&gt;False&lt;/ IncludeSetACLProviderOnDestination&gt;**  게시 프로필 파일 (영향을 줄 단일 프로필) 또는 (모든 프로필에 영향을)를 wpp.targets 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-278">If you know that the default permissions on site folders are correct and do not need to be set, you disable this behavior by adding **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** to the publish profile file (to affect a single profile) or to the wpp.targets file (to affect all profiles).</span></span> <span data-ttu-id="b3423-279">이러한 파일을 편집 하는 방법에 대 한 정보를 참조 하십시오. [하는 방법: 프로 파일 (.pubxml) 파일에서 배포 설정을 편집](https://msdn.microsoft.com/en-us/library/ff398069.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-279">For information about how to edit these files, see [How to: Edit Deployment Settings in Profile (.pubxml) Files](https://msdn.microsoft.com/en-us/library/ff398069.aspx).</span></span> 

## <a name="access-denied-errors-when-the-application-tries-to-write-to-an-application-folder"></a><span data-ttu-id="b3423-280">응용 프로그램에서 응용 프로그램 폴더에 기록 하려고 할 때 액세스 거부 오류</span><span class="sxs-lookup"><span data-stu-id="b3423-280">Access Denied Errors when the Application Tries to Write to an Application Folder</span></span>

### <a name="scenario"></a><span data-ttu-id="b3423-281">시나리오</span><span class="sxs-lookup"><span data-stu-id="b3423-281">Scenario</span></span>

<span data-ttu-id="b3423-282">해당 폴더에 대 한 쓰기 권한이 없기 때문에 응용 프로그램 폴더 중 하나에 파일 만들기 또는 편집 하려고 할 때 응용 프로그램 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-282">Your application errors when it tries to create or edit a file in one of the application folders, because it does not have write authority for that folder.</span></span>

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b3423-283">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="b3423-283">Possible Cause and Solution</span></span>

<span data-ttu-id="b3423-284">기본적으로 Visual Studio 집합 사이트의 루트 폴더에 읽기 권한 및 앱에 대 한 쓰기 권한이\_데이터 폴더.</span><span class="sxs-lookup"><span data-stu-id="b3423-284">By default, Visual Studio sets read permissions on the root folder of the site and write permissions on the App\_Data folder.</span></span> <span data-ttu-id="b3423-285">응용 프로그램은 하위 폴더에 대 한 쓰기에 필요한 경우에 표시 된 대로 해당 폴더에 대 한 권한을 설정할 수 있습니다는 [폴더 사용 권한 설정](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md) 및 [프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-285">If your application needs write access to a sub-folder, you can set permissions for that folder as shown in the [Setting Folder Permissions](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md) and [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorials.</span></span> <span data-ttu-id="b3423-286">루트 폴더에 추가 하 여 읽기 전용 액세스를 설정 하지 못하도록 해야 응용 프로그램에 사이트의 루트 폴더에 대 한 쓰기 권한이 필요한 경우  **&lt;IncludeSetACLProviderOn 대상&gt;False&lt;/ IncludeSetACLProviderOnDestination&gt;**  게시 프로필 파일 (영향을 줄 단일 프로필) 또는 (모든 프로필에 영향을)를 wpp.targets 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-286">If your application needs write access to the root folder of the site, you have to prevent it from setting read-only access on the root folder by adding **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** to the publish profile file (to affect a single profile) or to the wpp.targets file (to affect all profiles).</span></span> <span data-ttu-id="b3423-287">이러한 파일을 편집 하는 방법에 대 한 정보를 참조 하십시오. [하는 방법: 프로 파일 (.pubxml) 파일에서 배포 설정을 편집](https://msdn.microsoft.com/en-us/library/ff398069.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-287">For information about how to edit these files, see [How to: Edit Deployment Settings in Profile (.pubxml) Files](https://msdn.microsoft.com/en-us/library/ff398069.aspx).</span></span> <a id="aspnet45error"></a>

## <a name="configuration-error---targetframework-attribute-references-a-version-that-is-later-than-the-installed-version-of-the-net-framework"></a><span data-ttu-id="b3423-288">구성 오류-targetFramework 특성 참조의.NET Framework 설치 된 버전 보다 최신인 버전</span><span class="sxs-lookup"><span data-stu-id="b3423-288">Configuration Error - targetFramework attribute references a version that is later than the installed version of the .NET Framework</span></span>

### <a name="scenario"></a><span data-ttu-id="b3423-289">시나리오</span><span class="sxs-lookup"><span data-stu-id="b3423-289">Scenario</span></span>

<span data-ttu-id="b3423-290">ASP.NET 4.5를 대상으로 하는 웹 프로젝트를 성공적으로 게시 하지만 응용 프로그램을 실행 하는 경우 (으로 `customErrors` 모드가 Web.config 파일에서 "off"로 설정) 다음과 같은 오류가:</span><span class="sxs-lookup"><span data-stu-id="b3423-290">You successfully published a web project that targets ASP.NET 4.5, but when you run the application (with the `customErrors` mode set to "off" in the Web.config file) you get the following error:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample24.cmd)]

<span data-ttu-id="b3423-291">오류 페이지의 원본 오류 상자 오류의 원인으로 Web.config에서 다음 줄이 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-291">The Source Error box of the error page highlights the following line from Web.config as the cause of the error:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample25.cmd)]

### <a name="possible-cause-and-solution"></a><span data-ttu-id="b3423-292">가능한 원인 및 해결</span><span class="sxs-lookup"><span data-stu-id="b3423-292">Possible Cause and Solution</span></span>

<span data-ttu-id="b3423-293">서버에서 ASP.NET 4.5를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-293">The server does not support ASP.NET 4.5.</span></span> <span data-ttu-id="b3423-294">시기 및 ASP.NET 4.5에 대 한 지원을 추가할 수 있는지 확인 하려면 호스팅 공급자를 게 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b3423-294">Contact the hosting provider to determine when and if support for ASP.NET 4.5 can be added.</span></span> <span data-ttu-id="b3423-295">ASP.NET 4 또는 이전 버전을 대상으로 하는 웹 프로젝트를 배포 해야 하는 서버를 업그레이드 하는 옵션을 없으면 대신 합니다. 동일한 대상에는 ASP.NET 4 또는 이전 웹 프로젝트를 배포 하는 경우 선택 된 **대상에서 추가 파일 제거** 확인란은 **설정** 탭은 **웹에게시**마법사.</span><span class="sxs-lookup"><span data-stu-id="b3423-295">If upgrading the server is not an option, you have to deploy a web project that targets ASP.NET 4 or earlier instead.If you deploy an ASP.NET 4 or earlier web project to the same destination, select the **Remove additional files at destination** check box on the **Settings** tab of the **Publish Web** wizard.</span></span> <span data-ttu-id="b3423-296">선택 하지 않으면 **대상에서 추가 파일 제거**, 구성 오류 페이지를 가져오는 데 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-296">If you don't select **Remove additional files at destination**, you will continue to get the Configuration Error page.</span></span>

<span data-ttu-id="b3423-297">프로젝트 **속성** windows 대상 프레임 워크 드롭다운 목록에 포함 되어 있지만 변경 하 여이 문제를 해결할 수 없는 **.NET Framework 4.5** 를 **.NETFramework4**.</span><span class="sxs-lookup"><span data-stu-id="b3423-297">The project **Properties** windows includes a Target framework drop-down list, but you can't resolve this problem by just changing that from **.NET Framework 4.5** to **.NET Framework 4**.</span></span> <span data-ttu-id="b3423-298">이전 프레임 워크 버전으로 대상 프레임 워크를 변경 하는 경우 프로젝트는 최신 프레임 워크 버전의 어셈블리에 대 한 참조 및 여전히 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-298">If you change the target framework to an earlier framework version, the project will still have references to the later framework version's assemblies and will not run.</span></span> <span data-ttu-id="b3423-299">수동으로 해당 참조를 변경 하거나.NET Framework 4 또는 이전 버전을 대상으로 하는 새 프로젝트 만들기 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-299">You have to manually change those references or create a new project that targets .NET Framework 4 or earlier.</span></span> <span data-ttu-id="b3423-300">자세한 내용은 참조 [웹 사이트에 대 한.NET Framework 대상 지정](https://msdn.microsoft.com/en-us/library/bb398791(v=vs.100).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3423-300">For more information, see [.NET Framework Targeting for Web Sites](https://msdn.microsoft.com/en-us/library/bb398791(v=vs.100).aspx).</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="b3423-301">이전</span><span class="sxs-lookup"><span data-stu-id="b3423-301">Previous</span></span>](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)
