---
title: ASP.NET Core를 사용하는 Azure App Service 및 IIS에 대한 일반적인 오류 참조
author: guardrex
description: Azure App Service 및 IIS에서 ASP.NET Core 앱을 호스트할 때 일반적인 오류를 구분합니다.
ms.author: riande
ms.custom: mvc
ms.date: 03/13/2017
uid: host-and-deploy/azure-iis-errors-reference
ms.openlocfilehash: 30b7f1d8e1cfdfd3d1db865ff428eb2094a84d32
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36277321"
---
# <a name="common-errors-reference-for-azure-app-service-and-iis-with-aspnet-core"></a><span data-ttu-id="3f6d7-103">ASP.NET Core를 사용하는 Azure App Service 및 IIS에 대한 일반적인 오류 참조</span><span class="sxs-lookup"><span data-stu-id="3f6d7-103">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>

<span data-ttu-id="3f6d7-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="3f6d7-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="3f6d7-105">다음은 모든 오류를 나열한 목록이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-105">The following isn't a complete list of errors.</span></span> <span data-ttu-id="3f6d7-106">여기에 나열되지 않은 오류가 발생하면 오류를 재현하기 위한 자세한 지침이 포함된 [새 문제를 엽니다](https://github.com/aspnet/Docs/issues/new).</span><span class="sxs-lookup"><span data-stu-id="3f6d7-106">If you encounter an error not listed here, [open a new issue](https://github.com/aspnet/Docs/issues/new) with detailed instructions to reproduce the error.</span></span>

<span data-ttu-id="3f6d7-107">다음과 같은 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-107">Collect the following information:</span></span>

* <span data-ttu-id="3f6d7-108">브라우저 동작</span><span class="sxs-lookup"><span data-stu-id="3f6d7-108">Browser behavior</span></span>
* <span data-ttu-id="3f6d7-109">응용 프로그램 이벤트 로그 항목</span><span class="sxs-lookup"><span data-stu-id="3f6d7-109">Application Event Log entries</span></span>
* <span data-ttu-id="3f6d7-110">ASP.NET Core 모듈 stdout 로그 항목</span><span class="sxs-lookup"><span data-stu-id="3f6d7-110">ASP.NET Core Module stdout log entries</span></span>

<span data-ttu-id="3f6d7-111">정보를 다음 일반 오류와 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-111">Compare the information to the following common errors.</span></span> <span data-ttu-id="3f6d7-112">일치하는 항목이 발견되면 문제 해결 권장 사항을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-112">If a match is found, follow the troubleshooting advice.</span></span>

[!INCLUDE [Azure App Service Preview Notice](../includes/azure-apps-preview-notice.md)]

## <a name="installer-unable-to-obtain-vc-redistributable"></a><span data-ttu-id="3f6d7-113">설치 관리자에서 VC++ 재배포 가능 패키지를 가져올 수 없음</span><span class="sxs-lookup"><span data-stu-id="3f6d7-113">Installer unable to obtain VC++ Redistributable</span></span>

* <span data-ttu-id="3f6d7-114">**설치 관리자 예외:** 0x80072efd 또는 0x80072f76 - 지정되지 않은 오류</span><span class="sxs-lookup"><span data-stu-id="3f6d7-114">**Installer Exception:** 0x80072efd or 0x80072f76 - Unspecified error</span></span>

* <span data-ttu-id="3f6d7-115">**설치 관리자 로그 예외&#8224;:** 오류 0x80072efd 또는 0x80072f76: EXE 패키지를 실행하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-115">**Installer Log Exception&#8224;:** Error 0x80072efd or 0x80072f76: Failed to execute EXE package</span></span>

  <span data-ttu-id="3f6d7-116">&#8224;로그는 C:\Users\\{USER}\AppData\Local\Temp\dd_DotNetCoreWinSvrHosting__{timestamp}.log에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-116">&#8224;The log is located at C:\Users\\{USER}\AppData\Local\Temp\dd_DotNetCoreWinSvrHosting__{timestamp}.log.</span></span>

<span data-ttu-id="3f6d7-117">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="3f6d7-117">Troubleshooting:</span></span>

* <span data-ttu-id="3f6d7-118">시스템에서 호스팅 번들을 설치하는 동안 인터넷에 액세스할 수 없는 경우 이 예외는 설치 관리자에서 ‘Microsoft Visual C++ 2015 재배포 가능 패키지’를 다운로드할 수 없을 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-118">If the system doesn't have Internet access while installing the Hosting Bundle, this exception occurs when the installer is prevented from obtaining the *Microsoft Visual C++ 2015 Redistributable*.</span></span> <span data-ttu-id="3f6d7-119">[Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=53840)에서 설치 관리자를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-119">Obtain an installer from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53840).</span></span> <span data-ttu-id="3f6d7-120">설치 관리자에 오류가 발생하면 서버가 FDD(프레임워크 종속 배포)를 호스트하는 데 필요한 .NET Core 런타임을 받지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-120">If the installer fails, the server may not receive the .NET Core runtime required to host a framework-dependent deployment (FDD).</span></span> <span data-ttu-id="3f6d7-121">FDD를 호스트하려면 프로그램 및 기능에서 런타임이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-121">If hosting an FDD, confirm that the runtime is installed in Programs &amp; Features.</span></span> <span data-ttu-id="3f6d7-122">필요한 경우 [.NET 모든 다운로드](https://www.microsoft.com/net/download/all)에서 런타임 설치 관리자를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-122">If needed, obtain a runtime installer from [.NET All Downloads](https://www.microsoft.com/net/download/all).</span></span> <span data-ttu-id="3f6d7-123">런타임을 설치한 후 시스템을 다시 시작하거나 명령 프롬프트에서 **net stop was /y**에 이어 **net start w3svc**를 실행하여 IIS를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-123">After installing the runtime, restart the system or restart IIS by executing **net stop was /y** followed by **net start w3svc** from a command prompt.</span></span>

## <a name="os-upgrade-removed-the-32-bit-aspnet-core-module"></a><span data-ttu-id="3f6d7-124">OS 업그레이드에서 32비트 ASP.NET Core 모듈이 제거됨</span><span class="sxs-lookup"><span data-stu-id="3f6d7-124">OS upgrade removed the 32-bit ASP.NET Core Module</span></span>

* <span data-ttu-id="3f6d7-125">**응용 프로그램 로그:** 모듈 DLL **C:\WINDOWS\system32\inetsrv\aspnetcore.dll**을(를) 로드하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-125">**Application Log:** The Module DLL **C:\WINDOWS\system32\inetsrv\aspnetcore.dll** failed to load.</span></span> <span data-ttu-id="3f6d7-126">데이터 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-126">The data is the error.</span></span>

<span data-ttu-id="3f6d7-127">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="3f6d7-127">Troubleshooting:</span></span>

* <span data-ttu-id="3f6d7-128">OS를 업그레이드하는 동안 **C:\Windows\SysWOW64\inetsrv** 디렉터리에 있는 비OS 파일은 보존되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-128">Non-OS files in the **C:\Windows\SysWOW64\inetsrv** directory aren't preserved during an OS upgrade.</span></span> <span data-ttu-id="3f6d7-129">OS를 업그레이드하기 전에 ASP.NET Core 모듈을 설치한 다음, OS를 업그레이드한 후에 32비트 모드에서 AppPool을 실행하면 이 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-129">If the ASP.NET Core Module is installed prior to an OS upgrade and then any AppPool is run in 32-bit mode after an OS upgrade, this issue is encountered.</span></span> <span data-ttu-id="3f6d7-130">OS를 업그레이드한 후에 ASP.NET Core 모듈을 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-130">After an OS upgrade, repair the ASP.NET Core Module.</span></span> <span data-ttu-id="3f6d7-131">[.NET Core 호스팅 번들 설치](xref:host-and-deploy/iis/index#install-the-net-core-hosting-bundle)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-131">See [Install the .NET Core Hosting bundle](xref:host-and-deploy/iis/index#install-the-net-core-hosting-bundle).</span></span> <span data-ttu-id="3f6d7-132">설치 관리자가 실행될 때 **복구**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-132">Select **Repair** when the installer is run.</span></span>

## <a name="platform-conflicts-with-rid"></a><span data-ttu-id="3f6d7-133">플랫폼이 RID와 충돌함</span><span class="sxs-lookup"><span data-stu-id="3f6d7-133">Platform conflicts with RID</span></span>

* <span data-ttu-id="3f6d7-134">**브라우저:** HTTP 오류 502.5 - 프로세스 오류</span><span class="sxs-lookup"><span data-stu-id="3f6d7-134">**Browser:** HTTP Error 502.5 - Process Failure</span></span>

* <span data-ttu-id="3f6d7-135">**응용 프로그램 로그:** 실제 루트 'C:\{PATH}\'가 있는 응용 프로그램 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}'에서 '"C:\\{PATH}{assembly}.{exe|dll}" ' 명령줄로 프로세스를 시작하지 못했습니다. 오류 코드 = '0x80004005 : ff.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-135">**Application Log:** Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\{PATH}\' failed to start process with commandline '"C:\\{PATH}{assembly}.{exe|dll}" ', ErrorCode = '0x80004005 : ff.</span></span>

* <span data-ttu-id="3f6d7-136">**ASP.NET Core 모듈 로그:** 처리되지 않은 예외: System.BadImageFormatException: 파일이나 어셈블리 '{assembly}.dll'을 로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-136">**ASP.NET Core Module Log:** Unhandled Exception: System.BadImageFormatException: Could not load file or assembly '{assembly}.dll'.</span></span> <span data-ttu-id="3f6d7-137">프로그램을 잘못된 형식으로 로드하려고 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-137">An attempt was made to load a program with an incorrect format.</span></span>

<span data-ttu-id="3f6d7-138">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="3f6d7-138">Troubleshooting:</span></span>

* <span data-ttu-id="3f6d7-139">앱이 Kestrel에서 로컬로 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-139">Confirm that the app runs locally on Kestrel.</span></span> <span data-ttu-id="3f6d7-140">프로세스 오류는 앱 내의 문제 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-140">A process failure might be the result of a problem within the app.</span></span> <span data-ttu-id="3f6d7-141">자세한 내용은 [문제 해결](xref:host-and-deploy/iis/troubleshoot)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-141">For more information, see [Troubleshooting](xref:host-and-deploy/iis/troubleshoot).</span></span>

* <span data-ttu-id="3f6d7-142">*.csproj*의 `<PlatformTarget>`이 RID와 충돌하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-142">Confirm that the `<PlatformTarget>` in the *.csproj* doesn't conflict with the RID.</span></span> <span data-ttu-id="3f6d7-143">예를 들어 *dotnet publish -c Release -r win10-x64*를 사용하거나 *.csproj*의 `<RuntimeIdentifiers>`를 `win10-x64`로 설정하여 `x86`인 `<PlatformTarget>`을 지정하지 않고 `win10-x64`인 RID를 사용하여 게시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-143">For example, don't specify a `<PlatformTarget>` of `x86` and publish with an RID of `win10-x64`, either by using *dotnet publish -c Release -r win10-x64* or by setting the `<RuntimeIdentifiers>` in the *.csproj* to `win10-x64`.</span></span> <span data-ttu-id="3f6d7-144">프로젝트는 경고 또는 오류 없이 게시되지만 시스템에서 위와 같이 로깅된 예외와 함께 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-144">The project publishes without warning or error but fails with the above logged exceptions on the system.</span></span>

* <span data-ttu-id="3f6d7-145">Azure 앱 배포에서 앱을 업그레이드하고 새 어셈블리를 배포할 때 이 예외가 발생하면 이전 배포에서 모든 파일을 수동으로 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-145">If this exception occurs for an Azure Apps deployment when upgrading an app and deploying newer assemblies, manually delete all files from the prior deployment.</span></span> <span data-ttu-id="3f6d7-146">호환되지 않는 어셈블리가 오랫동안 남아 있으면 업그레이드된 응용 프로그램을 배포할 때 `System.BadImageFormatException` 예외가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-146">Lingering incompatible assemblies can result in a `System.BadImageFormatException` exception when deploying an upgraded app.</span></span>

## <a name="uri-endpoint-wrong-or-stopped-website"></a><span data-ttu-id="3f6d7-147">URI 끝점이 잘못되었거나 중지된 웹 사이트</span><span class="sxs-lookup"><span data-stu-id="3f6d7-147">URI endpoint wrong or stopped website</span></span>

* <span data-ttu-id="3f6d7-148">**브라우저:** ERR_CONNECTION_REFUSED</span><span class="sxs-lookup"><span data-stu-id="3f6d7-148">**Browser:** ERR_CONNECTION_REFUSED</span></span>

* <span data-ttu-id="3f6d7-149">**응용 프로그램 로그:** 항목 없음</span><span class="sxs-lookup"><span data-stu-id="3f6d7-149">**Application Log:** No entry</span></span>

* <span data-ttu-id="3f6d7-150">**ASP.NET Core 모듈 로그:** 로그 파일이 만들어지지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-150">**ASP.NET Core Module Log:** Log file not created</span></span>

<span data-ttu-id="3f6d7-151">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="3f6d7-151">Troubleshooting:</span></span>

* <span data-ttu-id="3f6d7-152">앱에 올바른 URI 끝점을 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-152">Confirm the correct URI endpoint for the app is being used.</span></span> <span data-ttu-id="3f6d7-153">바인딩을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-153">Check the bindings.</span></span>

* <span data-ttu-id="3f6d7-154">IIS 웹 사이트가 ‘중지됨’ 상태가 아닌지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-154">Confirm that the IIS website isn't in the *Stopped* state.</span></span>

## <a name="corewebengine-or-w3svc-server-features-disabled"></a><span data-ttu-id="3f6d7-155">CoreWebEngine 또는 W3SVC 서버 기능이 사용되지 않음</span><span class="sxs-lookup"><span data-stu-id="3f6d7-155">CoreWebEngine or W3SVC server features disabled</span></span>

* <span data-ttu-id="3f6d7-156">**OS 예외:** ASP.NET Core 모듈을 사용하려면 IIS 7.0 CoreWebEngine 및 W3SVC 기능이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-156">**OS Exception:** The IIS 7.0 CoreWebEngine and W3SVC features must be installed to use the ASP.NET Core Module.</span></span>

<span data-ttu-id="3f6d7-157">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="3f6d7-157">Troubleshooting:</span></span>

* <span data-ttu-id="3f6d7-158">적절한 역할 및 기능이 사용 가능한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-158">Confirm that the proper role and features are enabled.</span></span> <span data-ttu-id="3f6d7-159">[IIS 구성](xref:host-and-deploy/iis/index#iis-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-159">See [IIS Configuration](xref:host-and-deploy/iis/index#iis-configuration).</span></span>

## <a name="incorrect-website-physical-path-or-app-missing"></a><span data-ttu-id="3f6d7-160">잘못된 웹 사이트 실제 경로 또는 누락된 앱</span><span class="sxs-lookup"><span data-stu-id="3f6d7-160">Incorrect website physical path or app missing</span></span>

* <span data-ttu-id="3f6d7-161">**브라우저:** 403 사용할 수 없음 - 액세스가 거부되었습니다. **- 또는 -** 403.14 사용할 수 없음 - 웹 서버가 이 디렉터리의 내용을 표시하지 못하도록 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-161">**Browser:** 403 Forbidden - Access is denied **--OR--** 403.14 Forbidden - The Web server is configured to not list the contents of this directory.</span></span>

* <span data-ttu-id="3f6d7-162">**응용 프로그램 로그:** 항목 없음</span><span class="sxs-lookup"><span data-stu-id="3f6d7-162">**Application Log:** No entry</span></span>

* <span data-ttu-id="3f6d7-163">**ASP.NET Core 모듈 로그:** 로그 파일이 만들어지지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-163">**ASP.NET Core Module Log:** Log file not created</span></span>

<span data-ttu-id="3f6d7-164">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="3f6d7-164">Troubleshooting:</span></span>

* <span data-ttu-id="3f6d7-165">IIS 웹 사이트 **기본 설정**과 실제 앱 폴더를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-165">Check the IIS website **Basic Settings** and the physical app folder.</span></span> <span data-ttu-id="3f6d7-166">앱이 IIS 웹 사이트 **실제 경로**의 폴더에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-166">Confirm that the app is in the folder at the IIS website **Physical path**.</span></span>

## <a name="incorrect-role-module-not-installed-or-incorrect-permissions"></a><span data-ttu-id="3f6d7-167">잘못된 역할, 설치되지 않은 모듈 또는 잘못된 권한</span><span class="sxs-lookup"><span data-stu-id="3f6d7-167">Incorrect role, module not installed, or incorrect permissions</span></span>

* <span data-ttu-id="3f6d7-168">**브라우저:** 500.19 내부 서버 오류 - 요청된 페이지와 관련된 구성 데이터가 잘못되어 해당 페이지에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-168">**Browser:** 500.19 Internal Server Error - The requested page cannot be accessed because the related configuration data for the page is invalid.</span></span>

* <span data-ttu-id="3f6d7-169">**응용 프로그램 로그:** 항목 없음</span><span class="sxs-lookup"><span data-stu-id="3f6d7-169">**Application Log:** No entry</span></span>

* <span data-ttu-id="3f6d7-170">**ASP.NET Core 모듈 로그:** 로그 파일이 만들어지지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-170">**ASP.NET Core Module Log:** Log file not created</span></span>

<span data-ttu-id="3f6d7-171">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="3f6d7-171">Troubleshooting:</span></span>

* <span data-ttu-id="3f6d7-172">적절한 역할을 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-172">Confirm that the proper role is enabled.</span></span> <span data-ttu-id="3f6d7-173">[IIS 구성](xref:host-and-deploy/iis/index#iis-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-173">See [IIS Configuration](xref:host-and-deploy/iis/index#iis-configuration).</span></span>

* <span data-ttu-id="3f6d7-174">**프로그램 &amp; 기능**을 확인하고 **Microsoft ASP.NET Core 모듈**이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-174">Check **Programs &amp; Features** and confirm that the **Microsoft ASP.NET Core Module** has been installed.</span></span> <span data-ttu-id="3f6d7-175">**Microsoft ASP.NET Core 모듈**이 설치된 프로그램 목록에 없으면 해당 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-175">If the **Microsoft ASP.NET Core Module** isn't present in the list of installed programs, install the module.</span></span> <span data-ttu-id="3f6d7-176">[.NET Core 호스팅 번들 설치](xref:host-and-deploy/iis/index#install-the-net-core-hosting-bundle)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-176">See [Install the .NET Core Hosting Bundle](xref:host-and-deploy/iis/index#install-the-net-core-hosting-bundle).</span></span>

* <span data-ttu-id="3f6d7-177">**응용 프로그램 풀** > **프로세스 모델** > **ID**가 **ApplicationPoolIdentity**로 설정되어 있는지 또는 사용자 지정 ID에 앱의 배포 폴더에 액세스할 수 있는 올바른 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-177">Make sure that the **Application Pool** > **Process Model** > **Identity** is set to **ApplicationPoolIdentity** or the custom identity has the correct permissions to access the app's deployment folder.</span></span>

## <a name="incorrect-processpath-missing-path-variable-hosting-bundle-not-installed-systemiis-not-restarted-vc-redistributable-not-installed-or-dotnetexe-access-violation"></a><span data-ttu-id="3f6d7-178">잘못된 processPath, 누락된 PATH 변수, 설치되지 않은 호스팅 번들, 다시 시작되지 않은 시스템/IIS, 설치되지 않은 VC++ 재배포 가능 패키지 또는 dotnet.exe 액세스 위반</span><span class="sxs-lookup"><span data-stu-id="3f6d7-178">Incorrect processPath, missing PATH variable, Hosting Bundle not installed, system/IIS not restarted, VC++ Redistributable not installed, or dotnet.exe access violation</span></span>

* <span data-ttu-id="3f6d7-179">**브라우저:** HTTP 오류 502.5 - 프로세스 오류</span><span class="sxs-lookup"><span data-stu-id="3f6d7-179">**Browser:** HTTP Error 502.5 - Process Failure</span></span>

* <span data-ttu-id="3f6d7-180">**응용 프로그램 로그:** 실제 루트 'C:\\{PATH}\'가 있는 응용 프로그램 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}'에서 '".\{assembly}.exe" ' 명령줄로 프로세스를 시작하지 못했습니다. 오류 코드 = '0x80070002 : 0.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-180">**Application Log:** Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\\{PATH}\' failed to start process with commandline '".\{assembly}.exe" ', ErrorCode = '0x80070002 : 0.</span></span>

* <span data-ttu-id="3f6d7-181">**ASP.NET Core 모듈 로그:** 로그 파일이 만들어졌지만 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-181">**ASP.NET Core Module Log:** Log file created but empty</span></span>

<span data-ttu-id="3f6d7-182">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="3f6d7-182">Troubleshooting:</span></span>

* <span data-ttu-id="3f6d7-183">앱이 Kestrel에서 로컬로 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-183">Confirm that the app runs locally on Kestrel.</span></span> <span data-ttu-id="3f6d7-184">프로세스 오류는 앱 내의 문제 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-184">A process failure might be the result of a problem within the app.</span></span> <span data-ttu-id="3f6d7-185">자세한 내용은 [문제 해결](xref:host-and-deploy/iis/troubleshoot)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-185">For more information, see [Troubleshooting](xref:host-and-deploy/iis/troubleshoot).</span></span>

* <span data-ttu-id="3f6d7-186">*web.config*의 `<aspNetCore>` 요소에서 *processPath* 특성을 확인하여 FDD(프레임워크 종속 배포)에 대한 *dotnet*인지 또는 SCD(자체 포함 배포)에 대한 *.\{assembly}.exe*인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-186">Check the *processPath* attribute on the `<aspNetCore>` element in *web.config* to confirm that it's *dotnet* for a framework-dependent deployment (FDD) or *.\{assembly}.exe* for a self-contained deployment (SCD).</span></span>

* <span data-ttu-id="3f6d7-187">FDD의 경우 *dotnet.exe*에서 PATH 설정을 통해 액세스하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-187">For an FDD, *dotnet.exe* might not be accessible via the PATH settings.</span></span> <span data-ttu-id="3f6d7-188">시스템 PATH 설정에 *C:\Program Files\dotnet\*이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-188">Confirm that *C:\Program Files\dotnet\* exists in the System PATH settings.</span></span>

* <span data-ttu-id="3f6d7-189">FDD의 경우 *dotnet.exe*에서 응용 프로그램 풀의 사용자 ID에 액세스하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-189">For an FDD, *dotnet.exe* might not be accessible for the user identity of the Application Pool.</span></span> <span data-ttu-id="3f6d7-190">AppPool 사용자 ID에 *C:\Program Files\dotnet* 디렉터리에 대한 액세스 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-190">Confirm that the AppPool user identity has access to the *C:\Program Files\dotnet* directory.</span></span> <span data-ttu-id="3f6d7-191">*C:\Program Files\dotnet* 및 앱 디렉터리에 AppPool 사용자 ID에 대해 구성된 거부 규칙이 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-191">Confirm that there are no deny rules configured for the AppPool user identity on the *C:\Program Files\dotnet* and app directories.</span></span>

* <span data-ttu-id="3f6d7-192">IIS를 다시 시작하지 않은 상태로 FDD를 배포하고 .NET Core를 설치했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-192">An FDD may have been deployed and .NET Core installed without restarting IIS.</span></span> <span data-ttu-id="3f6d7-193">서버를 다시 시작하거나 명령 프롬프트에서 **net stop was /y**에 이어 **net start w3svc**를 실행하여 IIS를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-193">Either restart the server or restart IIS by executing **net stop was /y** followed by **net start w3svc** from a command prompt.</span></span>

* <span data-ttu-id="3f6d7-194">호스팅 시스템에 .NET Core 런타임을 설치하지 않고 FDD를 배포했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-194">An FDD may have been deployed without installing the .NET Core runtime on the hosting system.</span></span> <span data-ttu-id="3f6d7-195">.NET Core 런타임이 설치되어 있지 않으면 시스템에서 **.NET Core 호스팅 번들 설치 관리자**를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-195">If the .NET Core runtime hasn't been installed, run the **.NET Core Hosting Bundle installer** on the system.</span></span> <span data-ttu-id="3f6d7-196">[.NET Core 호스팅 번들 설치](xref:host-and-deploy/iis/index#install-the-net-core-hosting-bundle)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-196">See [Install the .NET Core Hosting Bundle](xref:host-and-deploy/iis/index#install-the-net-core-hosting-bundle).</span></span> <span data-ttu-id="3f6d7-197">인터넷에 연결되지 않은 시스템에 .NET Core 런타임을 설치하려는 경우 [.NET 모든 다운로드](https://www.microsoft.com/net/download/all)에서 런타임을 다운로드한 다음, 호스팅 번들 설치 관리자를 실행하여 ASP.NET Core 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-197">If attempting to install the .NET Core runtime on a system without an Internet connection, obtain the runtime from [.NET All Downloads](https://www.microsoft.com/net/download/all) and run the Hosting Bundle installer to install the ASP.NET Core Module.</span></span> <span data-ttu-id="3f6d7-198">설치를 완료하려면 시스템을 다시 시작하거나 명령 프롬프트에서 **net stop was /y**에 이어 **net start w3svc**를 실행하여 IIS를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-198">Complete the installation by restarting the system or restarting IIS by executing **net stop was /y** followed by **net start w3svc** from a command prompt.</span></span>

* <span data-ttu-id="3f6d7-199">FDD를 배포했을 수 있지만 ‘Microsoft Visual C++ 2015 재배포 가능 패키지(x64)’가 시스템에 설치되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-199">An FDD may have been deployed and the *Microsoft Visual C++ 2015 Redistributable (x64)* isn't installed on the system.</span></span> <span data-ttu-id="3f6d7-200">[Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=53840)에서 설치 관리자를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-200">Obtain an installer from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53840).</span></span>

## <a name="incorrect-arguments-of-aspnetcore-element"></a><span data-ttu-id="3f6d7-201">\<aspNetCore\> 요소의 잘못된 인수</span><span class="sxs-lookup"><span data-stu-id="3f6d7-201">Incorrect arguments of \<aspNetCore\> element</span></span>

* <span data-ttu-id="3f6d7-202">**브라우저:** HTTP 오류 502.5 - 프로세스 오류</span><span class="sxs-lookup"><span data-stu-id="3f6d7-202">**Browser:** HTTP Error 502.5 - Process Failure</span></span>

* <span data-ttu-id="3f6d7-203">**응용 프로그램 로그:** 실제 루트 'C:\\{PATH}\'가 있는 응용 프로그램 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}'에서 '"dotnet" .\{assembly}.dll' 명령줄로 프로세스를 시작하지 못했습니다. 오류 코드 = '0x80004005 : 80008081.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-203">**Application Log:** Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\\{PATH}\' failed to start process with commandline '"dotnet" .\{assembly}.dll', ErrorCode = '0x80004005 : 80008081.</span></span>

* <span data-ttu-id="3f6d7-204">**ASP.NET Core 모듈 로그:** 실행할 응용 프로그램이 없습니다. 'PATH\{assembly}.dll'</span><span class="sxs-lookup"><span data-stu-id="3f6d7-204">**ASP.NET Core Module Log:** The application to execute does not exist: 'PATH\{assembly}.dll'</span></span>

<span data-ttu-id="3f6d7-205">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="3f6d7-205">Troubleshooting:</span></span>

* <span data-ttu-id="3f6d7-206">앱이 Kestrel에서 로컬로 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-206">Confirm that the app runs locally on Kestrel.</span></span> <span data-ttu-id="3f6d7-207">프로세스 오류는 앱 내의 문제 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-207">A process failure might be the result of a problem within the app.</span></span> <span data-ttu-id="3f6d7-208">자세한 내용은 [문제 해결](xref:host-and-deploy/iis/troubleshoot)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-208">For more information, see [Troubleshooting](xref:host-and-deploy/iis/troubleshoot).</span></span>

* <span data-ttu-id="3f6d7-209">*web.config*의 `<aspNetCore>` 요소에서 *arguments* 특성을 검사하여 (a) FDD(프레임워크 종속 배포)에 대한 *.\{assembly}.dll*인지, 또는 (b) 없는 경우 빈 문자열(*arguments=""*)이거나 SCD(자체 포함 배포)에 대한 앱의 인수(*arguments="arg1, arg2, ..."*) 목록인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-209">Examine the *arguments* attribute on the `<aspNetCore>` element in *web.config* to confirm that it's either (a) *.\{assembly}.dll* for a framework-dependent deployment (FDD); or (b) not present, an empty string (*arguments=""*), or a list of the app's arguments (*arguments="arg1, arg2, ..."*) for a self-contained deployment (SCD).</span></span>

## <a name="missing-net-framework-version"></a><span data-ttu-id="3f6d7-210">누락된 .NET Framework 버전</span><span class="sxs-lookup"><span data-stu-id="3f6d7-210">Missing .NET Framework version</span></span>

* <span data-ttu-id="3f6d7-211">**브라우저:** 502.3 잘못된 게이트웨이 - 요청을 라우팅하는 동안 연결 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-211">**Browser:** 502.3 Bad Gateway - There was a connection error while trying to route the request.</span></span>

* <span data-ttu-id="3f6d7-212">**응용 프로그램 로그:** 오류 코드 = 실제 루트 'C:\\{PATH}\'가 있는 응용 프로그램 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}'에서 '"dotnet" .\{assembly}.dll' 명령줄로 프로세스를 시작하지 못했습니다. 오류 코드 = '0x80004005 : 80008081.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-212">**Application Log:** ErrorCode = Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\\{PATH}\' failed to start process with commandline '"dotnet" .\{assembly}.dll', ErrorCode = '0x80004005 : 80008081.</span></span>

* <span data-ttu-id="3f6d7-213">**ASP.NET Core 모듈 로그:** 메서드, 파일 또는 어셈블리 예외가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-213">**ASP.NET Core Module Log:** Missing method, file, or assembly exception.</span></span> <span data-ttu-id="3f6d7-214">예외에 지정된 메서드, 파일 또는 어셈블리는 .NET Framework 메서드, 파일 또는 어셈블리입니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-214">The method, file, or assembly specified in the exception is a .NET Framework method, file, or assembly.</span></span>

<span data-ttu-id="3f6d7-215">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="3f6d7-215">Troubleshooting:</span></span>

* <span data-ttu-id="3f6d7-216">시스템에서 누락된 .NET Framework 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-216">Install the .NET Framework version missing from the system.</span></span>

* <span data-ttu-id="3f6d7-217">FDD(프레임워크 종속 배포)의 경우 시스템에 올바른 런타임이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-217">For a framework-dependent deployment (FDD), confirm that the correct runtime installed on the system.</span></span> <span data-ttu-id="3f6d7-218">프로젝트가 1.1에서 2.0으로 업그레이드되고 호스팅 시스템에 배포된 다음, 이 예외가 발생하면 2.0 프레임워크가 호스팅 시스템에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-218">If the project is upgraded from 1.1 to 2.0, deployed to the hosting system, and this exception results, ensure that the 2.0 framework is on the hosting system.</span></span>

## <a name="stopped-application-pool"></a><span data-ttu-id="3f6d7-219">중지된 응용 프로그램 풀</span><span class="sxs-lookup"><span data-stu-id="3f6d7-219">Stopped Application Pool</span></span>

* <span data-ttu-id="3f6d7-220">**브라우저:** 503 서비스를 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="3f6d7-220">**Browser:** 503 Service Unavailable</span></span>

* <span data-ttu-id="3f6d7-221">**응용 프로그램 로그:** 항목 없음</span><span class="sxs-lookup"><span data-stu-id="3f6d7-221">**Application Log:** No entry</span></span>

* <span data-ttu-id="3f6d7-222">**ASP.NET Core 모듈 로그:** 로그 파일이 만들어지지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-222">**ASP.NET Core Module Log:** Log file not created</span></span>

<span data-ttu-id="3f6d7-223">문제 해결</span><span class="sxs-lookup"><span data-stu-id="3f6d7-223">Troubleshooting</span></span>

* <span data-ttu-id="3f6d7-224">응용 프로그램 풀이 ‘중지됨’ 상태가 아닌지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-224">Confirm that the Application Pool isn't in the *Stopped* state.</span></span>

## <a name="iis-integration-middleware-not-implemented"></a><span data-ttu-id="3f6d7-225">IIS 통합 미들웨어가 구현되지 않음</span><span class="sxs-lookup"><span data-stu-id="3f6d7-225">IIS Integration middleware not implemented</span></span>

* <span data-ttu-id="3f6d7-226">**브라우저:** HTTP 오류 502.5 - 프로세스 오류</span><span class="sxs-lookup"><span data-stu-id="3f6d7-226">**Browser:** HTTP Error 502.5 - Process Failure</span></span>

* <span data-ttu-id="3f6d7-227">**응용 프로그램 로그:** 실제 루트 'C:\\{PATH}\'이(가) 있는 응용 프로그램 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}'에서 '"C:\\{PATH}\{assembly}.{exe|dll}" ' 명령줄로 프로세스를 만들었지만 지정된 포트 '{PORT}'에서 크래시하거나 응답하지 않거나 수신 대기하지 않습니다. 오류 코드 = '0x800705b4'</span><span class="sxs-lookup"><span data-stu-id="3f6d7-227">**Application Log:** Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\\{PATH}\' created process with commandline '"C:\\{PATH}\{assembly}.{exe|dll}" ' but either crashed or did not reponse or did not listen on the given port '{PORT}', ErrorCode = '0x800705b4'</span></span>

* <span data-ttu-id="3f6d7-228">**ASP.NET Core 모듈 로그:** 로그 파일이 만들어졌고 정상 작동을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-228">**ASP.NET Core Module Log:** Log file created and shows normal operation.</span></span>

<span data-ttu-id="3f6d7-229">문제 해결</span><span class="sxs-lookup"><span data-stu-id="3f6d7-229">Troubleshooting</span></span>

* <span data-ttu-id="3f6d7-230">앱이 Kestrel에서 로컬로 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-230">Confirm that the app runs locally on Kestrel.</span></span> <span data-ttu-id="3f6d7-231">프로세스 오류는 앱 내의 문제 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-231">A process failure might be the result of a problem within the app.</span></span> <span data-ttu-id="3f6d7-232">자세한 내용은 [문제 해결](xref:host-and-deploy/iis/troubleshoot)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-232">For more information, see [Troubleshooting](xref:host-and-deploy/iis/troubleshoot).</span></span>

* <span data-ttu-id="3f6d7-233">다음 중 하나를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-233">Confirm that either:</span></span>
  * <span data-ttu-id="3f6d7-234">IIS 통합 미들웨어를 참조하려면 앱의 `WebHostBuilder`에서 `UseIISIntegration` 메서드를 호출합니다(ASP.NET Core 1.x).</span><span class="sxs-lookup"><span data-stu-id="3f6d7-234">The IIS Integration middleware is referencedby calling the `UseIISIntegration` method on the app's `WebHostBuilder` (ASP.NET Core 1.x)</span></span>
  * <span data-ttu-id="3f6d7-235">앱에서 `CreateDefaultBuilder` 메서드를 사용합니다(ASP.NET Core 2.x).</span><span class="sxs-lookup"><span data-stu-id="3f6d7-235">The apps uses the `CreateDefaultBuilder` method (ASP.NET Core 2.x).</span></span>
  
  <span data-ttu-id="3f6d7-236">자세한 내용은 [ASP.NET Core의 호스트](xref:fundamentals/host/index)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-236">See [Host in ASP.NET Core](xref:fundamentals/host/index) for details.</span></span>

## <a name="sub-application-includes-a-handlers-section"></a><span data-ttu-id="3f6d7-237">하위 응용 프로그램에 \<handlers\> 섹션이 포함되어 있음</span><span class="sxs-lookup"><span data-stu-id="3f6d7-237">Sub-application includes a \<handlers\> section</span></span>

* <span data-ttu-id="3f6d7-238">**브라우저:** HTTP 오류 500.19 - 내부 서버 오류</span><span class="sxs-lookup"><span data-stu-id="3f6d7-238">**Browser:** HTTP Error 500.19 - Internal Server Error</span></span>

* <span data-ttu-id="3f6d7-239">**응용 프로그램 로그:** 항목 없음</span><span class="sxs-lookup"><span data-stu-id="3f6d7-239">**Application Log:** No entry</span></span>

* <span data-ttu-id="3f6d7-240">**ASP.NET Core 모듈 로그:** 로그 파일이 만들어졌고 루트 앱에 대해 정상 작동을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-240">**ASP.NET Core Module Log:** Log file created and shows normal operation for the root app.</span></span> <span data-ttu-id="3f6d7-241">하위 앱에 대한 로그 파일이 만들어지지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-241">Log file not created for the sub-app.</span></span>

<span data-ttu-id="3f6d7-242">문제 해결</span><span class="sxs-lookup"><span data-stu-id="3f6d7-242">Troubleshooting</span></span>

* <span data-ttu-id="3f6d7-243">하위 앱의 *web.config* 파일에 `<handlers>` 섹션이 포함되어 있지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-243">Confirm that the sub-app's *web.config* file doesn't include a `<handlers>` section.</span></span>

## <a name="stdout-log-path-incorrect"></a><span data-ttu-id="3f6d7-244">stdout 로그 경로가 올바르지 않음</span><span class="sxs-lookup"><span data-stu-id="3f6d7-244">stdout log path incorrect</span></span>

* <span data-ttu-id="3f6d7-245">**브라우저:** 앱이 정상적으로 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-245">**Browser:** The app responds normally.</span></span>

* <span data-ttu-id="3f6d7-246">**응용 프로그램 로그:** 경고: stdoutLogFile \\?\C:\_apps\app_folder\bin\Release\netcoreapp2.0\win10-x64\publish\logs\path_doesnt_exist\stdout_8748_201831835937.log를 만들 수 없습니다. 오류 코드 = -2147024893.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-246">**Application Log:** Warning: Could not create stdoutLogFile \\?\C:\_apps\app_folder\bin\Release\netcoreapp2.0\win10-x64\publish\logs\path_doesnt_exist\stdout_8748_201831835937.log, ErrorCode = -2147024893.</span></span>

* <span data-ttu-id="3f6d7-247">**ASP.NET Core 모듈 로그:** 로그 파일이 만들어지지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-247">**ASP.NET Core Module Log:** Log file not created</span></span>

<span data-ttu-id="3f6d7-248">문제 해결</span><span class="sxs-lookup"><span data-stu-id="3f6d7-248">Troubleshooting</span></span>

* <span data-ttu-id="3f6d7-249">*web.config*의 `<aspNetCore>` 요소에 지정된 `stdoutLogFile` 경로가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-249">The `stdoutLogFile` path specified in the `<aspNetCore>` element of *web.config* doesn't exist.</span></span> <span data-ttu-id="3f6d7-250">자세한 내용은 ASP.NET Core 모듈 구성 참조 항목의 [로그 만들기 및 리디렉션](xref:host-and-deploy/aspnet-core-module#log-creation-and-redirection) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-250">For more information, see the [Log creation and redirection](xref:host-and-deploy/aspnet-core-module#log-creation-and-redirection) section of the ASP.NET Core Module configuration reference topic.</span></span>

## <a name="application-configuration-general-issue"></a><span data-ttu-id="3f6d7-251">일반적인 응용 프로그램 구성 문제</span><span class="sxs-lookup"><span data-stu-id="3f6d7-251">Application configuration general issue</span></span>

* <span data-ttu-id="3f6d7-252">**브라우저:** HTTP 오류 502.5 - 프로세스 오류</span><span class="sxs-lookup"><span data-stu-id="3f6d7-252">**Browser:** HTTP Error 502.5 - Process Failure</span></span>

* <span data-ttu-id="3f6d7-253">**응용 프로그램 로그:** 실제 루트 'C:\\{PATH}\'이(가) 있는 응용 프로그램 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}'에서 '"C:\\{PATH}\{assembly}.{exe|dll}" ' 명령줄로 프로세스를 만들었지만 지정된 포트 '{PORT}'에서 크래시하거나 응답하지 않거나 수신 대기하지 않습니다. 오류 코드 = '0x800705b4'</span><span class="sxs-lookup"><span data-stu-id="3f6d7-253">**Application Log:** Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\\{PATH}\' created process with commandline '"C:\\{PATH}\{assembly}.{exe|dll}" ' but either crashed or did not reponse or did not listen on the given port '{PORT}', ErrorCode = '0x800705b4'</span></span>

* <span data-ttu-id="3f6d7-254">**ASP.NET Core 모듈 로그:** 로그 파일이 만들어졌지만 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-254">**ASP.NET Core Module Log:** Log file created but empty</span></span>

<span data-ttu-id="3f6d7-255">문제 해결</span><span class="sxs-lookup"><span data-stu-id="3f6d7-255">Troubleshooting</span></span>

* <span data-ttu-id="3f6d7-256">이 일반 예외는 앱 구성 문제로 인해 프로세스가 시작되지 못했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-256">This general exception indicates that the process failed to start, most likely due to an app configuration issue.</span></span> <span data-ttu-id="3f6d7-257">[디렉터리 구조](xref:host-and-deploy/directory-structure)를 참조하여 앱의 배포된 파일과 폴더가 적절하고, 앱의 구성 파일이 있고, 앱과 환경에 대한 올바른 설정을 포함하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-257">Referring to [Directory Structure](xref:host-and-deploy/directory-structure), confirm that the app's deployed files and folders are appropriate and that the app's configuration files are present and contain the correct settings for the app and environment.</span></span> <span data-ttu-id="3f6d7-258">자세한 내용은 [문제 해결](xref:host-and-deploy/iis/troubleshoot)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f6d7-258">For more information, see [Troubleshooting](xref:host-and-deploy/iis/troubleshoot).</span></span>
