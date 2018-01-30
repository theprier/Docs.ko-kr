---
title: "Azure 앱 서비스 및 ASP.NET 코어는 IIS에 대 한 일반적인 오류 참조"
author: guardrex
description: "Azure 앱 서비스 및 IIS에서 ASP.NET Core 응용 프로그램을 호스트 하는 경우에 일반적인 오류를 구분 합니다."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 03/13/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/azure-iis-errors-reference
ms.openlocfilehash: 214f8c616aa65077690757e7805983a77ec4249e
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="common-errors-reference-for-azure-app-service-and-iis-with-aspnet-core"></a><span data-ttu-id="0d687-103">Azure 앱 서비스 및 ASP.NET 코어는 IIS에 대 한 일반적인 오류 참조</span><span class="sxs-lookup"><span data-stu-id="0d687-103">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>

<span data-ttu-id="0d687-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="0d687-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="0d687-105">다음은 모든 오류를 나열한 목록이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-105">The following isn't a complete list of errors.</span></span> <span data-ttu-id="0d687-106">여기에 나열 되지 오류가 발생 하는 경우 [새 문제점](https://github.com/aspnet/Docs/issues/new) 오류를 재현 하는 방법을 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-106">If you encounter an error not listed here, [open a new issue](https://github.com/aspnet/Docs/issues/new) with detailed instructions to reproduce the error.</span></span>

## <a name="installer-unable-to-obtain-vc-redistributable"></a><span data-ttu-id="0d687-107">설치 관리자에서 VC++ 재배포 가능 패키지를 가져올 수 없음</span><span class="sxs-lookup"><span data-stu-id="0d687-107">Installer unable to obtain VC++ Redistributable</span></span>

* <span data-ttu-id="0d687-108">**설치 관리자 예외:** 0x80072efd 또는 0x80072f76 - 지정되지 않은 오류</span><span class="sxs-lookup"><span data-stu-id="0d687-108">**Installer Exception:** 0x80072efd or 0x80072f76 - Unspecified error</span></span>

* <span data-ttu-id="0d687-109">**설치 관리자 로그 예외&#8224;:** 오류 0x80072efd 또는 0x80072f76: EXE 패키지를 실행하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-109">**Installer Log Exception&#8224;:** Error 0x80072efd or 0x80072f76: Failed to execute EXE package</span></span>

  <span data-ttu-id="0d687-110">&#8224;로그는 C:\Users\\{USER}\AppData\Local\Temp\dd_DotNetCoreWinSvrHosting__{timestamp}.log에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-110">&#8224;The log is located at C:\Users\\{USER}\AppData\Local\Temp\dd_DotNetCoreWinSvrHosting__{timestamp}.log.</span></span>

<span data-ttu-id="0d687-111">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="0d687-111">Troubleshooting:</span></span>

* <span data-ttu-id="0d687-112">시스템에서 서버 호스팅 번들을 설치하지만 인터넷에 액세스할 수 없는 경우 이 예외는 설치 관리자에서 *Microsoft Visual C++ 2015 재배포 가능 패키지*를 얻을 수 없을 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-112">If the system doesn't have Internet access while installing the server hosting bundle, this exception occurs when the installer is prevented from obtaining the *Microsoft Visual C++ 2015 Redistributable*.</span></span> <span data-ttu-id="0d687-113">프로그램 설치 관리자를 가져옵니다는 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=53840)합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-113">Obtain an installer from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53840).</span></span> <span data-ttu-id="0d687-114">설치 관리자에 오류가 발생 하면 서버에서 프레임 워크 종속 배포 (FDD)를 호스트 하는 데 필요한.NET 핵심 런타임을 받지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-114">If the installer fails, the server may not receive the .NET Core runtime required to host a framework-dependent deployment (FDD).</span></span> <span data-ttu-id="0d687-115">FDD 호스팅, 하는 경우 프로그램에서 런타임이 설치 되어 있는지 확인 &amp; 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-115">If hosting an FDD, confirm that the runtime is installed in Programs &amp; Features.</span></span> <span data-ttu-id="0d687-116">필요한 경우에서 런타임 설치 관리자를 가져올 [.NET 다운로드](https://www.microsoft.com/net/download/core)합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-116">If needed, obtain a runtime installer from [.NET Downloads](https://www.microsoft.com/net/download/core).</span></span> <span data-ttu-id="0d687-117">런타임을 설치한 후 시스템을 다시 시작하거나 명령 프롬프트에서 **net stop was /y**에 이어 **net start w3svc**를 실행하여 IIS를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-117">After installing the runtime, restart the system or restart IIS by executing **net stop was /y** followed by **net start w3svc** from a command prompt.</span></span>

## <a name="os-upgrade-removed-the-32-bit-aspnet-core-module"></a><span data-ttu-id="0d687-118">OS 업그레이드에서 32비트 ASP.NET Core 모듈이 제거됨</span><span class="sxs-lookup"><span data-stu-id="0d687-118">OS upgrade removed the 32-bit ASP.NET Core Module</span></span>

* <span data-ttu-id="0d687-119">**응용 프로그램 로그:** 모듈 DLL **C:\WINDOWS\system32\inetsrv\aspnetcore.dll**을(를) 로드하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-119">**Application Log:** The Module DLL **C:\WINDOWS\system32\inetsrv\aspnetcore.dll** failed to load.</span></span> <span data-ttu-id="0d687-120">데이터 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-120">The data is the error.</span></span>

<span data-ttu-id="0d687-121">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="0d687-121">Troubleshooting:</span></span>

* <span data-ttu-id="0d687-122">OS를 업그레이드하는 동안 **C:\Windows\SysWOW64\inetsrv** 디렉터리에 있는 비OS 파일은 보존되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-122">Non-OS files in the **C:\Windows\SysWOW64\inetsrv** directory aren't preserved during an OS upgrade.</span></span> <span data-ttu-id="0d687-123">ASP.NET Core 모듈은 이전에 설치 됩니다. 운영 체제 업그레이드와 모든 AppPool 다음은 운영 체제 업그레이드 한 후 32 비트 모드에서 실행 되 면이 문제가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-123">If the ASP.NET Core Module is installed prior to an OS upgrade and then any AppPool is run in 32-bit mode after an OS upgrade, this issue is encountered.</span></span> <span data-ttu-id="0d687-124">OS를 업그레이드한 후에 ASP.NET Core 모듈을 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-124">After an OS upgrade, repair the ASP.NET Core Module.</span></span> <span data-ttu-id="0d687-125">[.NET Core Windows Server 호스팅 번들 설치](xref:host-and-deploy/iis/index#install-the-net-core-windows-server-hosting-bundle)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0d687-125">See [Install the .NET Core Windows Server Hosting bundle](xref:host-and-deploy/iis/index#install-the-net-core-windows-server-hosting-bundle).</span></span> <span data-ttu-id="0d687-126">선택 **복구** 설치 관리자를 실행 한 경우.</span><span class="sxs-lookup"><span data-stu-id="0d687-126">Select **Repair** when the installer is run.</span></span>

## <a name="platform-conflicts-with-rid"></a><span data-ttu-id="0d687-127">플랫폼이 RID와 충돌함</span><span class="sxs-lookup"><span data-stu-id="0d687-127">Platform conflicts with RID</span></span>

* <span data-ttu-id="0d687-128">**브라우저:** HTTP 오류 502.5 - 프로세스 오류</span><span class="sxs-lookup"><span data-stu-id="0d687-128">**Browser:** HTTP Error 502.5 - Process Failure</span></span>

* <span data-ttu-id="0d687-129">**응용 프로그램 로그:** 응용 프로그램 ' MACHINE/WEBROOT/APPHOST / {어셈블리 (를) ' 실제 루트와 ' c:\{경로}\' commandline와 프로세스를 시작 하지 못했습니다 ' "c:\\{PATH} {어셈블리}. { exe | dll} "', 오류 코드 = ' 0x80004005: ff입니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-129">**Application Log:** Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\{PATH}\' failed to start process with commandline '"C:\\{PATH}{assembly}.{exe|dll}" ', ErrorCode = '0x80004005 : ff.</span></span>

* <span data-ttu-id="0d687-130">**ASP.NET Core 모듈 로그:** 처리 되지 않은 예외: System.BadImageFormatException: 로드할 수 없습니다 파일이 나 어셈블리 '{어셈블리}.dll'.</span><span class="sxs-lookup"><span data-stu-id="0d687-130">**ASP.NET Core Module Log:** Unhandled Exception: System.BadImageFormatException: Could not load file or assembly '{assembly}.dll'.</span></span> <span data-ttu-id="0d687-131">프로그램을 잘못된 형식으로 로드하려고 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-131">An attempt was made to load a program with an incorrect format.</span></span>

<span data-ttu-id="0d687-132">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="0d687-132">Troubleshooting:</span></span>

* <span data-ttu-id="0d687-133">앱이 Kestrel에서 로컬로 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-133">Confirm that the app runs locally on Kestrel.</span></span> <span data-ttu-id="0d687-134">프로세스 오류는 앱 내의 문제 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-134">A process failure might be the result of a problem within the app.</span></span> <span data-ttu-id="0d687-135">자세한 내용은 참조 [문제 해결](xref:host-and-deploy/iis/troubleshoot)합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-135">For more information, see [Troubleshooting](xref:host-and-deploy/iis/troubleshoot).</span></span>

* <span data-ttu-id="0d687-136">확인 하는 `<PlatformTarget>` 에 *.csproj* 의 RID 충돌 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-136">Confirm that the `<PlatformTarget>` in the *.csproj* doesn't conflict with the RID.</span></span> <span data-ttu-id="0d687-137">예를 들어, 지정 하지 않으면는 `<PlatformTarget>` 의 `x86` 의 RID를 사용 하 여 게시 및 `win10-x64`, 사용 하 여 *dotnet 게시-c 릴리스-r win10 x64* 하거나 설정 하는 `<RuntimeIdentifiers>` 에 *.csproj*  를 `win10-x64`합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-137">For example, don't specify a `<PlatformTarget>` of `x86` and publish with an RID of `win10-x64`, either by using *dotnet publish -c Release -r win10-x64* or by setting the `<RuntimeIdentifiers>` in the *.csproj* to `win10-x64`.</span></span> <span data-ttu-id="0d687-138">프로젝트는 경고 또는 오류 없이 게시되지만 시스템에서 위와 같이 로깅된 예외와 함께 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-138">The project publishes without warning or error but fails with the above logged exceptions on the system.</span></span>

* <span data-ttu-id="0d687-139">이 예외는 응용 프로그램을 업그레이드 하는 경우 Azure 응용 프로그램 배포에 대 한 발생 하 고 이전 배포에서 모든 파일을 수동으로 삭제 최신 어셈블리를 배포 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="0d687-139">If this exception occurs for an Azure Apps deployment when upgrading an app and deploying newer assemblies, manually delete all files from the prior deployment.</span></span> <span data-ttu-id="0d687-140">호환되지 않는 어셈블리가 오랫동안 남아 있으면 업그레이드된 응용 프로그램을 배포할 때 `System.BadImageFormatException` 예외가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-140">Lingering incompatible assemblies can result in a `System.BadImageFormatException` exception when deploying an upgraded app.</span></span>

## <a name="uri-endpoint-wrong-or-stopped-website"></a><span data-ttu-id="0d687-141">URI 끝점이 잘못되었거나 중지된 웹 사이트</span><span class="sxs-lookup"><span data-stu-id="0d687-141">URI endpoint wrong or stopped website</span></span>

* <span data-ttu-id="0d687-142">**브라우저:** ERR_CONNECTION_REFUSED</span><span class="sxs-lookup"><span data-stu-id="0d687-142">**Browser:** ERR_CONNECTION_REFUSED</span></span>

* <span data-ttu-id="0d687-143">**응용 프로그램 로그:** 항목 없음</span><span class="sxs-lookup"><span data-stu-id="0d687-143">**Application Log:** No entry</span></span>

* <span data-ttu-id="0d687-144">**ASP.NET Core 모듈 로그:** 로그 파일이 만들어지지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-144">**ASP.NET Core Module Log:** Log file not created</span></span>

<span data-ttu-id="0d687-145">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="0d687-145">Troubleshooting:</span></span>

* <span data-ttu-id="0d687-146">사용 되는 앱에 대 한 올바른 URI 끝점을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-146">Confirm the correct URI endpoint for the app is being used.</span></span> <span data-ttu-id="0d687-147">바인딩을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0d687-147">Check the bindings.</span></span>

* <span data-ttu-id="0d687-148">IIS 웹 사이트에 없음을 확인는 *Stopped* 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-148">Confirm that the IIS website isn't in the *Stopped* state.</span></span>

## <a name="corewebengine-or-w3svc-server-features-disabled"></a><span data-ttu-id="0d687-149">CoreWebEngine 또는 W3SVC 서버 기능이 사용되지 않음</span><span class="sxs-lookup"><span data-stu-id="0d687-149">CoreWebEngine or W3SVC server features disabled</span></span>

* <span data-ttu-id="0d687-150">**OS 예외:** ASP.NET Core 모듈을 사용하려면 IIS 7.0 CoreWebEngine 및 W3SVC 기능이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-150">**OS Exception:** The IIS 7.0 CoreWebEngine and W3SVC features must be installed to use the ASP.NET Core Module.</span></span>

<span data-ttu-id="0d687-151">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="0d687-151">Troubleshooting:</span></span>

* <span data-ttu-id="0d687-152">적절 한 역할 및 기능이 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-152">Confirm that the proper role and features are enabled.</span></span> <span data-ttu-id="0d687-153">[IIS 구성](xref:host-and-deploy/iis/index#iis-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0d687-153">See [IIS Configuration](xref:host-and-deploy/iis/index#iis-configuration).</span></span>

## <a name="incorrect-website-physical-path-or-app-missing"></a><span data-ttu-id="0d687-154">앱이 누락 또는 잘못 된 웹 사이트 실제 경로</span><span class="sxs-lookup"><span data-stu-id="0d687-154">Incorrect website physical path or app missing</span></span>

* <span data-ttu-id="0d687-155">**브라우저:** 403 사용할 수 없음 - 액세스가 거부되었습니다.  **- 또는 -**  403.14 사용할 수 없음 - 웹 서버가 이 디렉터리의 내용을 표시하지 못하도록 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-155">**Browser:** 403 Forbidden - Access is denied **--OR--** 403.14 Forbidden - The Web server is configured to not list the contents of this directory.</span></span>

* <span data-ttu-id="0d687-156">**응용 프로그램 로그:** 항목 없음</span><span class="sxs-lookup"><span data-stu-id="0d687-156">**Application Log:** No entry</span></span>

* <span data-ttu-id="0d687-157">**ASP.NET Core 모듈 로그:** 로그 파일이 만들어지지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-157">**ASP.NET Core Module Log:** Log file not created</span></span>

<span data-ttu-id="0d687-158">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="0d687-158">Troubleshooting:</span></span>

* <span data-ttu-id="0d687-159">IIS 웹 사이트 확인 **기본 설정** 및 실제 응용 프로그램 폴더가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-159">Check the IIS website **Basic Settings** and the physical app folder.</span></span> <span data-ttu-id="0d687-160">IIS 웹 사이트에 있는 폴더에 응용 프로그램 인지 확인 **실제 경로**합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-160">Confirm that the app is in the folder at the IIS website **Physical path**.</span></span>

## <a name="incorrect-role-module-not-installed-or-incorrect-permissions"></a><span data-ttu-id="0d687-161">잘못된 역할, 설치되지 않은 모듈 또는 잘못된 권한</span><span class="sxs-lookup"><span data-stu-id="0d687-161">Incorrect role, module not installed, or incorrect permissions</span></span>

* <span data-ttu-id="0d687-162">**브라우저:** 500.19 내부 서버 오류 - 요청된 페이지와 관련된 구성 데이터가 잘못되어 해당 페이지에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-162">**Browser:** 500.19 Internal Server Error - The requested page cannot be accessed because the related configuration data for the page is invalid.</span></span>

* <span data-ttu-id="0d687-163">**응용 프로그램 로그:** 항목 없음</span><span class="sxs-lookup"><span data-stu-id="0d687-163">**Application Log:** No entry</span></span>

* <span data-ttu-id="0d687-164">**ASP.NET Core 모듈 로그:** 로그 파일이 만들어지지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-164">**ASP.NET Core Module Log:** Log file not created</span></span>

<span data-ttu-id="0d687-165">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="0d687-165">Troubleshooting:</span></span>

* <span data-ttu-id="0d687-166">적절 한 역할을 활성화 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-166">Confirm that the proper role is enabled.</span></span> <span data-ttu-id="0d687-167">[IIS 구성](xref:host-and-deploy/iis/index#iis-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0d687-167">See [IIS Configuration](xref:host-and-deploy/iis/index#iis-configuration).</span></span>

* <span data-ttu-id="0d687-168">**프로그램 &amp; 기능**을 확인하고 **Microsoft ASP.NET Core 모듈**이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-168">Check **Programs &amp; Features** and confirm that the **Microsoft ASP.NET Core Module** has been installed.</span></span> <span data-ttu-id="0d687-169">**Microsoft ASP.NET Core 모듈**이 설치된 프로그램 목록에 없으면 해당 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-169">If the **Microsoft ASP.NET Core Module** isn't present in the list of installed programs, install the module.</span></span> <span data-ttu-id="0d687-170">[.NET Core Windows Server 호스팅 번들 설치](xref:host-and-deploy/iis/index#install-the-net-core-windows-server-hosting-bundle)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0d687-170">See [Install the .NET Core Windows Server Hosting bundle](xref:host-and-deploy/iis/index#install-the-net-core-windows-server-hosting-bundle).</span></span>

* <span data-ttu-id="0d687-171">다음 사항을 확인는 **응용 프로그램 풀** > **프로세스 모델** > **Identity** 로 설정 된 **ApplicationPoolIdentity** 또는 사용자 지정 id는 올바른 권한이 응용 프로그램의 배포 폴더에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-171">Make sure that the **Application Pool** > **Process Model** > **Identity** is set to **ApplicationPoolIdentity** or the custom identity has the correct permissions to access the app's deployment folder.</span></span>

## <a name="incorrect-processpath-missing-path-variable-hosting-bundle-not-installed-systemiis-not-restarted-vc-redistributable-not-installed-or-dotnetexe-access-violation"></a><span data-ttu-id="0d687-172">잘못된 processPath, 누락된 PATH 변수, 설치되지 않은 호스팅 번들, 다시 시작되지 않은 시스템/IIS, 설치되지 않은 VC++ 재배포 가능 패키지 또는 dotnet.exe 액세스 위반</span><span class="sxs-lookup"><span data-stu-id="0d687-172">Incorrect processPath, missing PATH variable, hosting bundle not installed, system/IIS not restarted, VC++ Redistributable not installed, or dotnet.exe access violation</span></span>

* <span data-ttu-id="0d687-173">**브라우저:** HTTP 오류 502.5 - 프로세스 오류</span><span class="sxs-lookup"><span data-stu-id="0d687-173">**Browser:** HTTP Error 502.5 - Process Failure</span></span>

* <span data-ttu-id="0d687-174">**응용 프로그램 로그:** 응용 프로그램 ' MACHINE/WEBROOT/APPHOST / {어셈블리 (를) ' 실제 루트와 ' c:\\{PATH}\' commandline와 프로세스를 시작 하지 못했습니다 ' ".\{ 어셈블리 (를).exe"', 오류 코드 = ' 0x80070002: 0.</span><span class="sxs-lookup"><span data-stu-id="0d687-174">**Application Log:** Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\\{PATH}\' failed to start process with commandline '".\{assembly}.exe" ', ErrorCode = '0x80070002 : 0.</span></span>

* <span data-ttu-id="0d687-175">**ASP.NET Core 모듈 로그:** 로그 파일이 만들어졌지만 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-175">**ASP.NET Core Module Log:** Log file created but empty</span></span>

<span data-ttu-id="0d687-176">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="0d687-176">Troubleshooting:</span></span>

* <span data-ttu-id="0d687-177">앱이 Kestrel에서 로컬로 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-177">Confirm that the app runs locally on Kestrel.</span></span> <span data-ttu-id="0d687-178">프로세스 오류는 앱 내의 문제 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-178">A process failure might be the result of a problem within the app.</span></span> <span data-ttu-id="0d687-179">자세한 내용은 참조 [문제 해결](xref:host-and-deploy/iis/troubleshoot)합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-179">For more information, see [Troubleshooting](xref:host-and-deploy/iis/troubleshoot).</span></span>

* <span data-ttu-id="0d687-180">확인의 *processPath* 특성에 `<aspNetCore>` 요소에 *web.config* 이 있는지 확인 하려면 *dotnet* 프레임 워크 종속 배포 (FDD) 또는 *. \{어셈블리}.exe* 자체 포함된 배포 (SCD)에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-180">Check the *processPath* attribute on the `<aspNetCore>` element in *web.config* to confirm that it's *dotnet* for a framework-dependent deployment (FDD) or *.\{assembly}.exe* for a self-contained deployment (SCD).</span></span>

* <span data-ttu-id="0d687-181">FDD의 경우 *dotnet.exe*에서 PATH 설정을 통해 액세스하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-181">For an FDD, *dotnet.exe* might not be accessible via the PATH settings.</span></span> <span data-ttu-id="0d687-182">시스템 PATH 설정에 *C:\Program Files\dotnet\*이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-182">Confirm that *C:\Program Files\dotnet\* exists in the System PATH settings.</span></span>

* <span data-ttu-id="0d687-183">FDD의 경우 *dotnet.exe*에서 응용 프로그램 풀의 사용자 ID에 액세스하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-183">For an FDD, *dotnet.exe* might not be accessible for the user identity of the Application Pool.</span></span> <span data-ttu-id="0d687-184">AppPool 사용자 ID에 *C:\Program Files\dotnet* 디렉터리에 대한 액세스 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-184">Confirm that the AppPool user identity has access to the *C:\Program Files\dotnet* directory.</span></span> <span data-ttu-id="0d687-185">AppPool 사용자 id에 대해 구성 된 거부 규칙 확인는 *C:\Program Files\dotnet* 및 응용 프로그램 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-185">Confirm that there are no deny rules configured for the AppPool user identity on the *C:\Program Files\dotnet* and app directories.</span></span>

* <span data-ttu-id="0d687-186">FDD 배포 하 고 IIS를 다시 시작 하지 않고.NET Core를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-186">An FDD may have been deployed and .NET Core installed without restarting IIS.</span></span> <span data-ttu-id="0d687-187">서버를 다시 시작하거나 명령 프롬프트에서 **net stop was /y**에 이어 **net start w3svc**를 실행하여 IIS를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-187">Either restart the server or restart IIS by executing **net stop was /y** followed by **net start w3svc** from a command prompt.</span></span>

* <span data-ttu-id="0d687-188">.NET 핵심 런타임을 호스팅하는 시스템에 설치 하지 않고는 FDD는 배포 했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-188">An FDD may have been deployed without installing the .NET Core runtime on the hosting system.</span></span> <span data-ttu-id="0d687-189">.NET 핵심 런타임을 설치 실패 하는 경우 실행는 **번들 설치 관리자.NET 핵심 Windows Server 호스팅** 시스템에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-189">If the .NET Core runtime hasn't been installed, run the **.NET Core Windows Server Hosting bundle installer** on the system.</span></span> <span data-ttu-id="0d687-190">[.NET Core Windows Server 호스팅 번들 설치](xref:host-and-deploy/iis/index#install-the-net-core-windows-server-hosting-bundle)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0d687-190">See [Install the .NET Core Windows Server Hosting bundle](xref:host-and-deploy/iis/index#install-the-net-core-windows-server-hosting-bundle).</span></span> <span data-ttu-id="0d687-191">인터넷 연결 없이 시스템에.NET 핵심 런타임을 설치 하는 동안에서 런타임 가져올 [.NET 다운로드](https://www.microsoft.com/net/download/core) ASP.NET Core 모듈을 설치 하려면 호스팅 번들 설치 관리자를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-191">If attempting to install the .NET Core runtime on a system without an Internet connection, obtain the runtime from [.NET Downloads](https://www.microsoft.com/net/download/core) and run the hosting bundle installer to install the ASP.NET Core Module.</span></span> <span data-ttu-id="0d687-192">설치를 완료하려면 시스템을 다시 시작하거나 명령 프롬프트에서 **net stop was /y**에 이어 **net start w3svc**를 실행하여 IIS를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-192">Complete the installation by restarting the system or restarting IIS by executing **net stop was /y** followed by **net start w3svc** from a command prompt.</span></span>

* <span data-ttu-id="0d687-193">FDD 배포 및 *Microsoft Visual c + + 2015 재배포 가능 (x64)* 시스템에 설치 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-193">An FDD may have been deployed and the *Microsoft Visual C++ 2015 Redistributable (x64)* isn't installed on the system.</span></span> <span data-ttu-id="0d687-194">프로그램 설치 관리자를 가져옵니다는 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=53840)합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-194">Obtain an installer from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53840).</span></span>

## <a name="incorrect-arguments-of-aspnetcore-element"></a><span data-ttu-id="0d687-195">\<aspNetCore\> 요소의 잘못된 인수</span><span class="sxs-lookup"><span data-stu-id="0d687-195">Incorrect arguments of \<aspNetCore\> element</span></span>

* <span data-ttu-id="0d687-196">**브라우저:** HTTP 오류 502.5 - 프로세스 오류</span><span class="sxs-lookup"><span data-stu-id="0d687-196">**Browser:** HTTP Error 502.5 - Process Failure</span></span>

* <span data-ttu-id="0d687-197">**응용 프로그램 로그:** 응용 프로그램 ' MACHINE/WEBROOT/APPHOST / {어셈블리 (를) ' 실제 루트와 ' c:\\{PATH}\' commandline와 프로세스를 시작 하지 못했습니다 ' "dotnet".\{ (를) 어셈블리.dll ', 오류 코드 = ' 0x80004005: 80008081 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-197">**Application Log:** Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\\{PATH}\' failed to start process with commandline '"dotnet" .\{assembly}.dll', ErrorCode = '0x80004005 : 80008081.</span></span>

* <span data-ttu-id="0d687-198">**ASP.NET Core 모듈 로그:** 실행 하려면 응용 프로그램이 없습니다: ' 경로\{어셈블리}.dll '</span><span class="sxs-lookup"><span data-stu-id="0d687-198">**ASP.NET Core Module Log:** The application to execute does not exist: 'PATH\{assembly}.dll'</span></span>

<span data-ttu-id="0d687-199">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="0d687-199">Troubleshooting:</span></span>

* <span data-ttu-id="0d687-200">앱이 Kestrel에서 로컬로 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-200">Confirm that the app runs locally on Kestrel.</span></span> <span data-ttu-id="0d687-201">프로세스 오류는 앱 내의 문제 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-201">A process failure might be the result of a problem within the app.</span></span> <span data-ttu-id="0d687-202">자세한 내용은 참조 [문제 해결](xref:host-and-deploy/iis/troubleshoot)합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-202">For more information, see [Troubleshooting](xref:host-and-deploy/iis/troubleshoot).</span></span>

* <span data-ttu-id="0d687-203">검사는 *인수* 특성에 `<aspNetCore>` 요소에 *web.config* 중 하나 인지 확인 하려면 (a) *.\{ (를) 어셈블리.dll* 프레임 워크 종속 배포 (FDD;)에 대 한 또는 (b)를 표시 하지, 빈 문자열 (*인수 = ""*), 또는 응용 프로그램의 인수 목록 (*인수 "arg1, arg2,..." =*) 자체 포함 배포 (SCD).</span><span class="sxs-lookup"><span data-stu-id="0d687-203">Examine the *arguments* attribute on the `<aspNetCore>` element in *web.config* to confirm that it's either (a) *.\{assembly}.dll* for a framework-dependent deployment (FDD); or (b) not present, an empty string (*arguments=""*), or a list of the app's arguments (*arguments="arg1, arg2, ..."*) for a self-contained deployment (SCD).</span></span>

## <a name="missing-net-framework-version"></a><span data-ttu-id="0d687-204">누락된 .NET Framework 버전</span><span class="sxs-lookup"><span data-stu-id="0d687-204">Missing .NET Framework version</span></span>

* <span data-ttu-id="0d687-205">**브라우저:** 502.3 잘못된 게이트웨이 - 요청을 라우팅하는 동안 연결 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-205">**Browser:** 502.3 Bad Gateway - There was a connection error while trying to route the request.</span></span>

* <span data-ttu-id="0d687-206">**응용 프로그램 로그:** ErrorCode 응용 프로그램 = ' MACHINE/WEBROOT/APPHOST / {어셈블리 (를) ' 실제 루트와 ' c:\\{PATH}\' commandline와 프로세스를 시작 하지 못했습니다 ' "dotnet".\{ (를) 어셈블리.dll ', 오류 코드 = ' 0x80004005: 80008081 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-206">**Application Log:** ErrorCode = Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\\{PATH}\' failed to start process with commandline '"dotnet" .\{assembly}.dll', ErrorCode = '0x80004005 : 80008081.</span></span>

* <span data-ttu-id="0d687-207">**ASP.NET Core 모듈 로그:** 메서드, 파일 또는 어셈블리 예외가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-207">**ASP.NET Core Module Log:** Missing method, file, or assembly exception.</span></span> <span data-ttu-id="0d687-208">예외에 지정된 메서드, 파일 또는 어셈블리는 .NET Framework 메서드, 파일 또는 어셈블리입니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-208">The method, file, or assembly specified in the exception is a .NET Framework method, file, or assembly.</span></span>

<span data-ttu-id="0d687-209">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="0d687-209">Troubleshooting:</span></span>

* <span data-ttu-id="0d687-210">시스템에서 누락된 .NET Framework 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-210">Install the .NET Framework version missing from the system.</span></span>

* <span data-ttu-id="0d687-211">프레임 워크 종속 배포 (FDD)에 대 한 올바른 런타임 시스템에 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-211">For a framework-dependent deployment (FDD), confirm that the correct runtime installed on the system.</span></span> <span data-ttu-id="0d687-212">1.1에서 2.0, 호스팅 시스템에 배포 하는 프로젝트를 업그레이드 하는 경우이 예외로 인해 2.0 프레임 워크를 호스팅 시스템에서 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-212">If the project is upgraded from 1.1 to 2.0, deployed to the hosting system, and this exception results, ensure that the 2.0 framework is on the hosting system.</span></span>

## <a name="stopped-application-pool"></a><span data-ttu-id="0d687-213">중지된 응용 프로그램 풀</span><span class="sxs-lookup"><span data-stu-id="0d687-213">Stopped Application Pool</span></span>

* <span data-ttu-id="0d687-214">**브라우저:** 503 서비스를 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="0d687-214">**Browser:** 503 Service Unavailable</span></span>

* <span data-ttu-id="0d687-215">**응용 프로그램 로그:** 항목 없음</span><span class="sxs-lookup"><span data-stu-id="0d687-215">**Application Log:** No entry</span></span>

* <span data-ttu-id="0d687-216">**ASP.NET Core 모듈 로그:** 로그 파일이 만들어지지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-216">**ASP.NET Core Module Log:** Log file not created</span></span>

<span data-ttu-id="0d687-217">문제 해결</span><span class="sxs-lookup"><span data-stu-id="0d687-217">Troubleshooting</span></span>

* <span data-ttu-id="0d687-218">응용 프로그램 풀에 없음을 확인는 *Stopped* 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-218">Confirm that the Application Pool isn't in the *Stopped* state.</span></span>

## <a name="iis-integration-middleware-not-implemented"></a><span data-ttu-id="0d687-219">IIS 통합 미들웨어가 구현되지 않음</span><span class="sxs-lookup"><span data-stu-id="0d687-219">IIS Integration middleware not implemented</span></span>

* <span data-ttu-id="0d687-220">**브라우저:** HTTP 오류 502.5 - 프로세스 오류</span><span class="sxs-lookup"><span data-stu-id="0d687-220">**Browser:** HTTP Error 502.5 - Process Failure</span></span>

* <span data-ttu-id="0d687-221">**응용 프로그램 로그:** 응용 프로그램 ' MACHINE/WEBROOT/APPHOST / {어셈블리 (를) ' 실제 루트와 ' c:\\{PATH}\' 명령줄을 사용 하 여 프로세스를 만든 ' "c:\\{PATH}\{어셈블리}. { exe | dll} "' 하지만 충돌 또는 응답 하지 않았습니다 또는 ErrorCode 지정한 포트 '{PORT}'에서 수신 하지 않은 '0x800705b4' =</span><span class="sxs-lookup"><span data-stu-id="0d687-221">**Application Log:** Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\\{PATH}\' created process with commandline '"C:\\{PATH}\{assembly}.{exe|dll}" ' but either crashed or did not reponse or did not listen on the given port '{PORT}', ErrorCode = '0x800705b4'</span></span>

* <span data-ttu-id="0d687-222">**ASP.NET Core 모듈 로그:**  로그 파일이 만들어졌고 정상 작동을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-222">**ASP.NET Core Module Log:** Log file created and shows normal operation.</span></span>

<span data-ttu-id="0d687-223">문제 해결</span><span class="sxs-lookup"><span data-stu-id="0d687-223">Troubleshooting</span></span>

* <span data-ttu-id="0d687-224">앱이 Kestrel에서 로컬로 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-224">Confirm that the app runs locally on Kestrel.</span></span> <span data-ttu-id="0d687-225">프로세스 오류는 앱 내의 문제 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-225">A process failure might be the result of a problem within the app.</span></span> <span data-ttu-id="0d687-226">자세한 내용은 참조 [문제 해결](xref:host-and-deploy/iis/troubleshoot)합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-226">For more information, see [Troubleshooting](xref:host-and-deploy/iis/troubleshoot).</span></span>

* <span data-ttu-id="0d687-227">하거나 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-227">Confirm that either:</span></span>
  * <span data-ttu-id="0d687-228">IIS 통합 미들웨어가 referencedby 호출는 `UseIISIntegration` 메서드를 응용 프로그램의 `WebHostBuilder` (ASP.NET Core 1.x)</span><span class="sxs-lookup"><span data-stu-id="0d687-228">The IIS Integration middleware is referencedby calling the `UseIISIntegration` method on the app's `WebHostBuilder` (ASP.NET Core 1.x)</span></span>
  * <span data-ttu-id="0d687-229">앱 사용 하 여는 `CreateDefaultBuilder` 메서드 (ASP.NET Core 2.x).</span><span class="sxs-lookup"><span data-stu-id="0d687-229">The apps uses the `CreateDefaultBuilder` method (ASP.NET Core 2.x).</span></span>
  
  <span data-ttu-id="0d687-230">[ASP.NET Core에서의 호스팅](xref:fundamentals/hosting)에서 자세한 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0d687-230">See [Hosting in ASP.NET Core](xref:fundamentals/hosting) for details.</span></span>

## <a name="sub-application-includes-a-handlers-section"></a><span data-ttu-id="0d687-231">하위 응용 프로그램에 \<handlers\> 섹션이 포함되어 있음</span><span class="sxs-lookup"><span data-stu-id="0d687-231">Sub-application includes a \<handlers\> section</span></span>

* <span data-ttu-id="0d687-232">**브라우저:** HTTP 오류 500.19 - 내부 서버 오류</span><span class="sxs-lookup"><span data-stu-id="0d687-232">**Browser:** HTTP Error 500.19 - Internal Server Error</span></span>

* <span data-ttu-id="0d687-233">**응용 프로그램 로그:** 항목 없음</span><span class="sxs-lookup"><span data-stu-id="0d687-233">**Application Log:** No entry</span></span>

* <span data-ttu-id="0d687-234">**ASP.NET Core 모듈 로그:** 로그 파일이 만들어지고 루트 응용 프로그램에 대 한 정상 작동을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-234">**ASP.NET Core Module Log:** Log file created and shows normal operation for the root app.</span></span> <span data-ttu-id="0d687-235">로그 파일이 하위 앱에 대 한 생성 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-235">Log file not created for the sub-app.</span></span>

<span data-ttu-id="0d687-236">문제 해결</span><span class="sxs-lookup"><span data-stu-id="0d687-236">Troubleshooting</span></span>

* <span data-ttu-id="0d687-237">하위 앱의 *web.config* 파일에 `<handlers>` 섹션이 포함되어 있지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-237">Confirm that the sub-app's *web.config* file doesn't include a `<handlers>` section.</span></span>

## <a name="application-configuration-general-issue"></a><span data-ttu-id="0d687-238">일반적인 응용 프로그램 구성 문제</span><span class="sxs-lookup"><span data-stu-id="0d687-238">Application configuration general issue</span></span>

* <span data-ttu-id="0d687-239">**브라우저:** HTTP 오류 502.5 - 프로세스 오류</span><span class="sxs-lookup"><span data-stu-id="0d687-239">**Browser:** HTTP Error 502.5 - Process Failure</span></span>

* <span data-ttu-id="0d687-240">**응용 프로그램 로그:** 응용 프로그램 ' MACHINE/WEBROOT/APPHOST / {어셈블리 (를) ' 실제 루트와 ' c:\\{PATH}\' 명령줄을 사용 하 여 프로세스를 만든 ' "c:\\{PATH}\{어셈블리}. { exe | dll} "' 하지만 충돌 또는 응답 하지 않았습니다 또는 ErrorCode 지정한 포트 '{PORT}'에서 수신 하지 않은 '0x800705b4' =</span><span class="sxs-lookup"><span data-stu-id="0d687-240">**Application Log:** Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\\{PATH}\' created process with commandline '"C:\\{PATH}\{assembly}.{exe|dll}" ' but either crashed or did not reponse or did not listen on the given port '{PORT}', ErrorCode = '0x800705b4'</span></span>

* <span data-ttu-id="0d687-241">**ASP.NET Core 모듈 로그:** 로그 파일이 만들어졌지만 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-241">**ASP.NET Core Module Log:** Log file created but empty</span></span>

<span data-ttu-id="0d687-242">문제 해결</span><span class="sxs-lookup"><span data-stu-id="0d687-242">Troubleshooting</span></span>

* <span data-ttu-id="0d687-243">이 일반 예외 프로세스 대부분 응용 프로그램 구성 문제로 인해 시작 되지 않았음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-243">This general exception indicates that the process failed to start, most likely due to an app configuration issue.</span></span> <span data-ttu-id="0d687-244">참조 [디렉터리 구조](xref:host-and-deploy/directory-structure)응용 프로그램의 파일을 배포 하는 적절 한 폴더 및 응용 프로그램의 구성 파일이 있는지 확인 하 고 앱 및 환경에 대 한 올바른 설정을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-244">Referring to [Directory Structure](xref:host-and-deploy/directory-structure), confirm that the app's deployed files and folders are appropriate and that the app's configuration files are present and contain the correct settings for the app and environment.</span></span> <span data-ttu-id="0d687-245">자세한 내용은 참조 [문제 해결](xref:host-and-deploy/iis/troubleshoot)합니다.</span><span class="sxs-lookup"><span data-stu-id="0d687-245">For more information, see [Troubleshooting](xref:host-and-deploy/iis/troubleshoot).</span></span>
