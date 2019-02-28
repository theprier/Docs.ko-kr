---
title: ASP.NET Core를 사용하는 Azure App Service 및 IIS에 대한 일반적인 오류 참조
author: guardrex
description: Azure App Service 및 IIS에서 ASP.NET Core 앱을 호스팅할 때 일반적인 오류에 대한 문제 해결 조언을 얻습니다.
ms.author: riande
ms.custom: mvc
ms.date: 02/21/2019
uid: host-and-deploy/azure-iis-errors-reference
ms.openlocfilehash: d1cdac4d27ee1bc3ebb4329c1bbd3bdacb34a58c
ms.sourcegitcommit: b3894b65e313570e97a2ab78b8addd22f427cac8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743949"
---
# <a name="common-errors-reference-for-azure-app-service-and-iis-with-aspnet-core"></a><span data-ttu-id="d53c6-103">ASP.NET Core를 사용하는 Azure App Service 및 IIS에 대한 일반적인 오류 참조</span><span class="sxs-lookup"><span data-stu-id="d53c6-103">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>

<span data-ttu-id="d53c6-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="d53c6-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="d53c6-105">Azure App Service 및 IIS에서 ASP.NET Core 앱을 호스팅할 때 일반적인 오류에 대한 문제 해결 조언을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-105">This topic offers troubleshooting advice for common errors when hosting ASP.NET Core apps on Azure Apps Service and IIS.</span></span>

<span data-ttu-id="d53c6-106">다음과 같은 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-106">Collect the following information:</span></span>

* <span data-ttu-id="d53c6-107">브라우저 동작(상태 코드 및 오류 메시지)</span><span class="sxs-lookup"><span data-stu-id="d53c6-107">Browser behavior (status code and error message)</span></span>
* <span data-ttu-id="d53c6-108">애플리케이션 이벤트 로그 항목</span><span class="sxs-lookup"><span data-stu-id="d53c6-108">Application Event Log entries</span></span>
  * <span data-ttu-id="d53c6-109">Azure App Service &ndash;는 <xref:host-and-deploy/azure-apps/troubleshoot>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d53c6-109">Azure App Service &ndash; See <xref:host-and-deploy/azure-apps/troubleshoot>.</span></span>
  * <span data-ttu-id="d53c6-110">IIS</span><span class="sxs-lookup"><span data-stu-id="d53c6-110">IIS</span></span>
    1. <span data-ttu-id="d53c6-111">**Windows** 메뉴에서 **시작**을 선택하고, *이벤트 뷰어*를 입력하고, **Enter**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-111">Select **Start** on the **Windows** menu, type *Event Viewer*, and press **Enter**.</span></span>
    1. <span data-ttu-id="d53c6-112">**이벤트 뷰어**가 열리면 사이드바에서 **Windows 로그** > **애플리케이션**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-112">After the **Event Viewer** opens, expand **Windows Logs** > **Application** in the sidebar.</span></span>
* <span data-ttu-id="d53c6-113">ASP.NET Core 모듈 stdout 및 디버그 로그 항목</span><span class="sxs-lookup"><span data-stu-id="d53c6-113">ASP.NET Core Module stdout and debug log entries</span></span>
  * <span data-ttu-id="d53c6-114">Azure App Service &ndash;는 <xref:host-and-deploy/azure-apps/troubleshoot>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d53c6-114">Azure App Service &ndash; See <xref:host-and-deploy/azure-apps/troubleshoot>.</span></span>
  * <span data-ttu-id="d53c6-115">IIS &ndash;는 ASP.NET Core 모듈 항목의 [로그 생성 및 리디렉션](xref:host-and-deploy/aspnet-core-module#log-creation-and-redirection) 및 [향상된 진단 로그](xref:host-and-deploy/aspnet-core-module#enhanced-diagnostic-logs) 섹션의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-115">IIS &ndash; Follow the instructions in the [Log creation and redirection](xref:host-and-deploy/aspnet-core-module#log-creation-and-redirection) and [Enhanced diagnostic logs](xref:host-and-deploy/aspnet-core-module#enhanced-diagnostic-logs) sections of the ASP.NET Core Module topic.</span></span>

<span data-ttu-id="d53c6-116">오류 정보를 다음 일반 오류와 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-116">Compare error information to the following common errors.</span></span> <span data-ttu-id="d53c6-117">일치하는 항목이 발견되면 문제 해결 권장 사항을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-117">If a match is found, follow the troubleshooting advice.</span></span>

<span data-ttu-id="d53c6-118">이 항목의 오류 목록은 완전하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-118">The list of errors in this topic isn't exhaustive.</span></span> <span data-ttu-id="d53c6-119">여기에 나열되지 않은 오류가 발생하는 경우 오류를 재현하는 방법에 대한 자세한 지침과 함께 이 항목 하단에 있는 **콘텐츠 피드백** 단추를 사용하여 새 문제를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-119">If you encounter an error not listed here, open a new issue using the **Content feedback** button at the bottom of this topic with detailed instructions on how to reproduce the error.</span></span>

[!INCLUDE[Azure App Service Preview Notice](../includes/azure-apps-preview-notice.md)]

## <a name="installer-unable-to-obtain-vc-redistributable"></a><span data-ttu-id="d53c6-120">설치 관리자에서 VC++ 재배포 가능 패키지를 가져올 수 없음</span><span class="sxs-lookup"><span data-stu-id="d53c6-120">Installer unable to obtain VC++ Redistributable</span></span>

* <span data-ttu-id="d53c6-121">**설치 관리자 예외:** 0x80072efd **--또는--**  0x80072f76 - 지정되지 않은 오류</span><span class="sxs-lookup"><span data-stu-id="d53c6-121">**Installer Exception:** 0x80072efd **--OR--** 0x80072f76 - Unspecified error</span></span>

* <span data-ttu-id="d53c6-122">**설치 관리자 로그 예외&#8224;:** 오류 0x80072efd **--또는--** 0x80072f76: EXE 패키지 실행 실패</span><span class="sxs-lookup"><span data-stu-id="d53c6-122">**Installer Log Exception&#8224;:** Error 0x80072efd **--OR--** 0x80072f76: Failed to execute EXE package</span></span>

  <span data-ttu-id="d53c6-123">&#8224;로그는 C:\Users*C:\Users\{USER}\AppData\Local\Temp\dd_DotNetCoreWinSvrHosting__{TIMESTAMP}.log*에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-123">&#8224;The log is located at *C:\Users\{USER}\AppData\Local\Temp\dd_DotNetCoreWinSvrHosting__{TIMESTAMP}.log*.</span></span>

<span data-ttu-id="d53c6-124">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="d53c6-124">Troubleshooting:</span></span>

<span data-ttu-id="d53c6-125">시스템에서 [.NET Core 호스팅 번들을 설치](xref:host-and-deploy/iis/index#install-the-net-core-hosting-bundle)하는 동안 인터넷에 액세스할 수 없는 경우 이 예외는 설치 관리자에서 *Microsoft Visual C++ 2015 재배포 가능 패키지*를 얻을 수 없을 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-125">If the system doesn't have Internet access while [installing the .NET Core Hosting Bundle](xref:host-and-deploy/iis/index#install-the-net-core-hosting-bundle), this exception occurs when the installer is prevented from obtaining the *Microsoft Visual C++ 2015 Redistributable*.</span></span> <span data-ttu-id="d53c6-126">[Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=53840)에서 설치 관리자를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-126">Obtain an installer from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53840).</span></span> <span data-ttu-id="d53c6-127">설치 관리자에 오류가 발생하면 서버가 [FDD(프레임워크 종속 배포)](/dotnet/core/deploying/#framework-dependent-deployments-fdd)를 호스트하는 데 필요한 .NET Core 런타임을 받지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-127">If the installer fails, the server may not receive the .NET Core runtime required to host a [framework-dependent deployment (FDD)](/dotnet/core/deploying/#framework-dependent-deployments-fdd).</span></span> <span data-ttu-id="d53c6-128">FDD를 호스팅하는 경우 런타임이 **프로그램 및 기능** 또는 **앱 및 기능**에 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-128">If hosting an FDD, confirm that the runtime is installed in **Programs & Features** or **Apps & features**.</span></span> <span data-ttu-id="d53c6-129">특정 런타임이 필요한 경우 [.NET Download Archives](https://dotnet.microsoft.com/download/archives)에서 런타임을 다운로드하여 시스템에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-129">If a specific runtime is required, download the runtime from the [.NET Download Archives](https://dotnet.microsoft.com/download/archives) and install it on the system.</span></span> <span data-ttu-id="d53c6-130">런타임을 설치한 후 시스템을 다시 시작하거나 명령 프롬프트에서 **net stop was /y**에 이어 **net start w3svc**를 실행하여 IIS를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-130">After installing the runtime, restart the system or restart IIS by executing **net stop was /y** followed by **net start w3svc** from a command prompt.</span></span>

## <a name="os-upgrade-removed-the-32-bit-aspnet-core-module"></a><span data-ttu-id="d53c6-131">OS 업그레이드에서 32비트 ASP.NET Core 모듈이 제거됨</span><span class="sxs-lookup"><span data-stu-id="d53c6-131">OS upgrade removed the 32-bit ASP.NET Core Module</span></span>

<span data-ttu-id="d53c6-132">**애플리케이션 로그:** 모듈 DLL **C:\WINDOWS\system32\inetsrv\aspnetcore.dll**을 로드하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-132">**Application Log:** The Module DLL **C:\WINDOWS\system32\inetsrv\aspnetcore.dll** failed to load.</span></span> <span data-ttu-id="d53c6-133">데이터 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-133">The data is the error.</span></span>

<span data-ttu-id="d53c6-134">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="d53c6-134">Troubleshooting:</span></span>

<span data-ttu-id="d53c6-135">OS를 업그레이드하는 동안 **C:\Windows\SysWOW64\inetsrv** 디렉터리에 있는 비OS 파일은 보존되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-135">Non-OS files in the **C:\Windows\SysWOW64\inetsrv** directory aren't preserved during an OS upgrade.</span></span> <span data-ttu-id="d53c6-136">OS를 업그레이드하기 전에 ASP.NET Core 모듈을 설치한 다음, OS를 업그레이드한 후에 32비트 모드에서 앱 풀을 실행하면 이 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-136">If the ASP.NET Core Module is installed prior to an OS upgrade and then any app pool is run in 32-bit mode after an OS upgrade, this issue is encountered.</span></span> <span data-ttu-id="d53c6-137">OS를 업그레이드한 후에 ASP.NET Core 모듈을 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-137">After an OS upgrade, repair the ASP.NET Core Module.</span></span> <span data-ttu-id="d53c6-138">[.NET Core 호스팅 번들 설치](xref:host-and-deploy/iis/index#install-the-net-core-hosting-bundle)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d53c6-138">See [Install the .NET Core Hosting bundle](xref:host-and-deploy/iis/index#install-the-net-core-hosting-bundle).</span></span> <span data-ttu-id="d53c6-139">설치 관리자가 실행될 때 **복구**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-139">Select **Repair** when the installer is run.</span></span>

## <a name="an-x86-app-is-deployed-but-the-app-pool-isnt-enabled-for-32-bit-apps"></a><span data-ttu-id="d53c6-140">x86 앱이 배포되었지만 32비트 앱에 대해 앱 풀이 활성화되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-140">An x86 app is deployed but the app pool isn't enabled for 32-bit apps</span></span>

* <span data-ttu-id="d53c6-141">**브라우저:** HTTP 오류 500.30 - ANCM In-Process 시작 실패</span><span class="sxs-lookup"><span data-stu-id="d53c6-141">**Browser:** HTTP Error 500.30 - ANCM In-Process Start Failure</span></span>

* <span data-ttu-id="d53c6-142">**애플리케이션 로그:** 실제 루트 '{PATH}'가 있는 애플리케이션 '/LM/W3SVC/5/ROOT'에서 예기치 않은 관리 예외, 예외 코드 = '0xe0434352'가 적중했습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-142">**Application Log:** Application '/LM/W3SVC/5/ROOT' with physical root '{PATH}' hit unexpected managed exception, exception code = '0xe0434352'.</span></span> <span data-ttu-id="d53c6-143">자세한 내용은 stderr 로그를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="d53c6-143">Please check the stderr logs for more information.</span></span> <span data-ttu-id="d53c6-144">실제 루트'{PATH}'가 있는 애플리케이션 '/LM/W3SVC/5/ROOT'에서 clr 및 관리되는 애플리케이션을 로드하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-144">Application '/LM/W3SVC/5/ROOT' with physical root '{PATH}' failed to load clr and managed application.</span></span> <span data-ttu-id="d53c6-145">CLR 작업자 스레드가 조기에 종료됨</span><span class="sxs-lookup"><span data-stu-id="d53c6-145">CLR worker thread exited prematurely</span></span>

* <span data-ttu-id="d53c6-146">**ASP.NET Core 모듈 stdout 로그:** 로그 파일이 생성되었지만 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-146">**ASP.NET Core Module stdout Log:** The log file is created but empty.</span></span>

::: moniker range=">= aspnetcore-2.2"

* <span data-ttu-id="d53c6-147">**ASP.NET Core 모듈 디버그 로그:** 실패한 HRESULT가 반환되었습니다. 0x8007023e</span><span class="sxs-lookup"><span data-stu-id="d53c6-147">**ASP.NET Core Module Debug Log:** Failed HRESULT returned: 0x8007023e</span></span>

::: moniker-end

<span data-ttu-id="d53c6-148">이 시나리오는 자체 포함된 앱을 게시할 때 SDK에 의해 트래핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-148">This scenario is trapped by the SDK when publishing a self-contained app.</span></span> <span data-ttu-id="d53c6-149">RID가 플랫폼 대상과 일치하지 않으면 SDK에서 오류가 발생합니다(예: 프로젝트 파일에 `<PlatformTarget>x86</PlatformTarget>`이 있는 `win10-x64` RID).</span><span class="sxs-lookup"><span data-stu-id="d53c6-149">The SDK produces an error if the RID doesn't match the platform target (for example, `win10-x64` RID with `<PlatformTarget>x86</PlatformTarget>` in the project file).</span></span>

<span data-ttu-id="d53c6-150">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="d53c6-150">Troubleshooting:</span></span>

<span data-ttu-id="d53c6-151">x86 프레임워크 종속 배포(`<PlatformTarget>x86</PlatformTarget>`)의 경우 32비트 앱용 IIS 앱 풀을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-151">For an x86 framework-dependent deployment (`<PlatformTarget>x86</PlatformTarget>`), enable the IIS app pool for 32-bit apps.</span></span> <span data-ttu-id="d53c6-152">IIS 관리자에서 앱 풀의 **고급 설정**을 열고 **32비트 앱 사용**을 **True**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-152">In IIS Manager, open the app pool's **Advanced Settings** and set **Enable 32-Bit Applications** to **True**.</span></span>

## <a name="platform-conflicts-with-rid"></a><span data-ttu-id="d53c6-153">플랫폼이 RID와 충돌함</span><span class="sxs-lookup"><span data-stu-id="d53c6-153">Platform conflicts with RID</span></span>

* <span data-ttu-id="d53c6-154">**브라우저:** HTTP 오류 502.5 - 프로세스 오류</span><span class="sxs-lookup"><span data-stu-id="d53c6-154">**Browser:** HTTP Error 502.5 - Process Failure</span></span>

* <span data-ttu-id="d53c6-155">**애플리케이션 로그:** 실제 루트 'C:\{PATH}\'가 있는 애플리케이션 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}'에서 '"C:\{PATH}{ASSEMBLY}.{exe|dll}" ' 명령줄로 프로세스를 시작하지 못했습니다. 오류 코드 = '0x80004005 : ff.</span><span class="sxs-lookup"><span data-stu-id="d53c6-155">**Application Log:** Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\{PATH}\' failed to start process with commandline '"C:\{PATH}{ASSEMBLY}.{exe|dll}" ', ErrorCode = '0x80004005 : ff.</span></span>

* <span data-ttu-id="d53c6-156">**ASP.NET Core 모듈 stdout 로그:** 처리되지 않은 예외: System.BadImageFormatException: 파일 또는 어셈블리 '{ASSEMBLY}.dll'을 로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-156">**ASP.NET Core Module stdout Log:** Unhandled Exception: System.BadImageFormatException: Could not load file or assembly '{ASSEMBLY}.dll'.</span></span> <span data-ttu-id="d53c6-157">프로그램을 잘못된 형식으로 로드하려고 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-157">An attempt was made to load a program with an incorrect format.</span></span>

<span data-ttu-id="d53c6-158">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="d53c6-158">Troubleshooting:</span></span>

* <span data-ttu-id="d53c6-159">앱이 Kestrel에서 로컬로 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-159">Confirm that the app runs locally on Kestrel.</span></span> <span data-ttu-id="d53c6-160">프로세스 오류는 앱 내의 문제 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-160">A process failure might be the result of a problem within the app.</span></span> <span data-ttu-id="d53c6-161">자세한 내용은 [문제 해결(IIS)](xref:host-and-deploy/iis/troubleshoot) 또는 [문제 해결(Azure App Service)](xref:host-and-deploy/azure-apps/troubleshoot)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d53c6-161">For more information, see [Troubleshoot (IIS)](xref:host-and-deploy/iis/troubleshoot) or [Troubleshoot (Azure App Service)](xref:host-and-deploy/azure-apps/troubleshoot).</span></span>

* <span data-ttu-id="d53c6-162">Azure 앱 배포에서 앱을 업그레이드하고 새 어셈블리를 배포할 때 이 예외가 발생하면 이전 배포에서 모든 파일을 수동으로 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-162">If this exception occurs for an Azure Apps deployment when upgrading an app and deploying newer assemblies, manually delete all files from the prior deployment.</span></span> <span data-ttu-id="d53c6-163">호환되지 않는 어셈블리가 오랫동안 남아 있으면 업그레이드된 응용 프로그램을 배포할 때 `System.BadImageFormatException` 예외가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-163">Lingering incompatible assemblies can result in a `System.BadImageFormatException` exception when deploying an upgraded app.</span></span>

## <a name="uri-endpoint-wrong-or-stopped-website"></a><span data-ttu-id="d53c6-164">URI 엔드포인트가 잘못되었거나 중지된 웹 사이트</span><span class="sxs-lookup"><span data-stu-id="d53c6-164">URI endpoint wrong or stopped website</span></span>

* <span data-ttu-id="d53c6-165">**브라우저:** ERR_CONNECTION_REFUSED **--또는--** 연결할 수 없음</span><span class="sxs-lookup"><span data-stu-id="d53c6-165">**Browser:** ERR_CONNECTION_REFUSED **--OR--** Unable to connect</span></span>

* <span data-ttu-id="d53c6-166">**애플리케이션 로그:** 진입 금지</span><span class="sxs-lookup"><span data-stu-id="d53c6-166">**Application Log:** No entry</span></span>

* <span data-ttu-id="d53c6-167">**ASP.NET Core 모듈 stdout 로그:** 로그 파일이 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-167">**ASP.NET Core Module stdout Log:** The log file isn't created.</span></span>

::: moniker range=">= aspnetcore-2.2"

* <span data-ttu-id="d53c6-168">**ASP.NET Core 모듈 디버그 로그:** 로그 파일이 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-168">**ASP.NET Core Module Debug Log:** The log file isn't created.</span></span>

::: moniker-end

<span data-ttu-id="d53c6-169">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="d53c6-169">Troubleshooting:</span></span>

* <span data-ttu-id="d53c6-170">사용 중인 앱에 대해 올바른 URI 엔드포인트를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-170">Confirm the correct URI endpoint for the app is in use.</span></span> <span data-ttu-id="d53c6-171">바인딩을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-171">Check the bindings.</span></span>

* <span data-ttu-id="d53c6-172">IIS 웹 사이트가 ‘중지됨’ 상태가 아닌지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-172">Confirm that the IIS website isn't in the *Stopped* state.</span></span>

## <a name="corewebengine-or-w3svc-server-features-disabled"></a><span data-ttu-id="d53c6-173">CoreWebEngine 또는 W3SVC 서버 기능이 사용되지 않음</span><span class="sxs-lookup"><span data-stu-id="d53c6-173">CoreWebEngine or W3SVC server features disabled</span></span>

<span data-ttu-id="d53c6-174">**OS 예외:** ASP.NET Core 모듈을 사용하려면 IIS 7.0 CoreWebEngine 및 W3SVC 기능이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-174">**OS Exception:** The IIS 7.0 CoreWebEngine and W3SVC features must be installed to use the ASP.NET Core Module.</span></span>

<span data-ttu-id="d53c6-175">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="d53c6-175">Troubleshooting:</span></span>

<span data-ttu-id="d53c6-176">적절한 역할 및 기능이 사용 가능한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-176">Confirm that the proper role and features are enabled.</span></span> <span data-ttu-id="d53c6-177">[IIS 구성](xref:host-and-deploy/iis/index#iis-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d53c6-177">See [IIS Configuration](xref:host-and-deploy/iis/index#iis-configuration).</span></span>

## <a name="incorrect-website-physical-path-or-app-missing"></a><span data-ttu-id="d53c6-178">잘못된 웹 사이트 실제 경로 또는 누락된 앱</span><span class="sxs-lookup"><span data-stu-id="d53c6-178">Incorrect website physical path or app missing</span></span>

* <span data-ttu-id="d53c6-179">**브라우저:** 403 사용할 수 없음 - 액세스가 거부되었습니다. **--또는--** 403.14 사용할 수 없음 - 웹 서버가 이 디렉터리의 내용을 표시하지 못하도록 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-179">**Browser:** 403 Forbidden - Access is denied **--OR--** 403.14 Forbidden - The Web server is configured to not list the contents of this directory.</span></span>

* <span data-ttu-id="d53c6-180">**애플리케이션 로그:** 진입 금지</span><span class="sxs-lookup"><span data-stu-id="d53c6-180">**Application Log:** No entry</span></span>

* <span data-ttu-id="d53c6-181">**ASP.NET Core 모듈 stdout 로그:** 로그 파일이 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-181">**ASP.NET Core Module stdout Log:** The log file isn't created.</span></span>

::: moniker range=">= aspnetcore-2.2"

* <span data-ttu-id="d53c6-182">**ASP.NET Core 모듈 디버그 로그:** 로그 파일이 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-182">**ASP.NET Core Module Debug Log:** The log file isn't created.</span></span>

::: moniker-end

<span data-ttu-id="d53c6-183">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="d53c6-183">Troubleshooting:</span></span>

<span data-ttu-id="d53c6-184">IIS 웹 사이트 **기본 설정**과 실제 앱 폴더를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-184">Check the IIS website **Basic Settings** and the physical app folder.</span></span> <span data-ttu-id="d53c6-185">앱이 IIS 웹 사이트 **실제 경로**의 폴더에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-185">Confirm that the app is in the folder at the IIS website **Physical path**.</span></span>

## <a name="incorrect-role-aspnet-core-module-not-installed-or-incorrect-permissions"></a><span data-ttu-id="d53c6-186">잘못된 역할, 설치되지 않은 ASP.NET Core 모듈 또는 잘못된 권한</span><span class="sxs-lookup"><span data-stu-id="d53c6-186">Incorrect role, ASP.NET Core Module not installed, or incorrect permissions</span></span>

* <span data-ttu-id="d53c6-187">**브라우저:** 500.19 내부 서버 오류 - 요청된 페이지와 관련된 구성 데이터가 잘못되어 해당 페이지에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-187">**Browser:** 500.19 Internal Server Error - The requested page cannot be accessed because the related configuration data for the page is invalid.</span></span> <span data-ttu-id="d53c6-188">**--또는--** 이 페이지를 표시할 수 없습니다</span><span class="sxs-lookup"><span data-stu-id="d53c6-188">**--OR--** This page can't be displayed</span></span>

* <span data-ttu-id="d53c6-189">**애플리케이션 로그:** 진입 금지</span><span class="sxs-lookup"><span data-stu-id="d53c6-189">**Application Log:** No entry</span></span>

* <span data-ttu-id="d53c6-190">**ASP.NET Core 모듈 stdout 로그:** 로그 파일이 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-190">**ASP.NET Core Module stdout Log:** The log file isn't created.</span></span>

::: moniker range=">= aspnetcore-2.2"

* <span data-ttu-id="d53c6-191">**ASP.NET Core 모듈 디버그 로그:** 로그 파일이 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-191">**ASP.NET Core Module Debug Log:** The log file isn't created.</span></span>

::: moniker-end

<span data-ttu-id="d53c6-192">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="d53c6-192">Troubleshooting:</span></span>

* <span data-ttu-id="d53c6-193">적절한 역할을 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-193">Confirm that the proper role is enabled.</span></span> <span data-ttu-id="d53c6-194">[IIS 구성](xref:host-and-deploy/iis/index#iis-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d53c6-194">See [IIS Configuration](xref:host-and-deploy/iis/index#iis-configuration).</span></span>

* <span data-ttu-id="d53c6-195">**프로그램 및 기능** 또는 **앱 및 기능**을 열고 **Windows Server 호스팅**이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-195">Open **Programs & Features** or **Apps & features** and confirm that **Windows Server Hosting** is installed.</span></span> <span data-ttu-id="d53c6-196">**Windows Server 호스팅**이 설치된 프로그램 목록에 없는 경우 .NET Core 호스팅 번들을 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-196">If **Windows Server Hosting** isn't present in the list of installed programs, download and install the .NET Core Hosting Bundle.</span></span>

  [<span data-ttu-id="d53c6-197">현재 .NET Core 호스팅 번들 설치 관리자(직접 다운로드)</span><span class="sxs-lookup"><span data-stu-id="d53c6-197">Current .NET Core Hosting Bundle installer (direct download)</span></span>](https://www.microsoft.com/net/permalink/dotnetcore-current-windows-runtime-bundle-installer)

  <span data-ttu-id="d53c6-198">자세한 내용은 [.NET Core 호스팅 번들 설치](xref:host-and-deploy/iis/index#install-the-net-core-hosting-bundle)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d53c6-198">For more information, see [Install the .NET Core Hosting Bundle](xref:host-and-deploy/iis/index#install-the-net-core-hosting-bundle).</span></span>

* <span data-ttu-id="d53c6-199">**애플리케이션 풀** > **프로세스 모델** > **ID**가 **ApplicationPoolIdentity**로 설정되어 있는지 또는 사용자 지정 ID에 앱의 배포 폴더에 액세스할 수 있는 올바른 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-199">Make sure that the **Application Pool** > **Process Model** > **Identity** is set to **ApplicationPoolIdentity** or the custom identity has the correct permissions to access the app's deployment folder.</span></span>

* <span data-ttu-id="d53c6-200">ASP.NET Core 호스팅 번들을 제거하고 이전 버전의 호스팅 번들을 설치하는 경우 *applicationHost.config* 파일에는 ASP.NET Core 모듈에 대한 섹션이 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-200">If you uninstalled the ASP.NET Core Hosting Bundle and installed an earlier version of the hosting bundle, the *applicationHost.config* file doesn't include a section for the ASP.NET Core Module.</span></span> <span data-ttu-id="d53c6-201">*%windir%/System32/inetsrv/config*에서 *applicationHost.config*를 열고 `<configuration><configSections><sectionGroup name="system.webServer">` 섹션 그룹을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-201">Open *applicationHost.config* at *%windir%/System32/inetsrv/config* and find the `<configuration><configSections><sectionGroup name="system.webServer">` section group.</span></span> <span data-ttu-id="d53c6-202">ASP.NET Core 모듈에 대한 섹션이 섹션 그룹에서 누락된 경우 섹션 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-202">If the section for the ASP.NET Core Module is missing from the section group, add the section element:</span></span>

  ```xml
  <section name="aspNetCore" overrideModeDefault="Allow" />
  ```
  
  <span data-ttu-id="d53c6-203">또는 최신 버전의 ASP.NET Core 호스팅 번들을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-203">Alternatively, install the lastest version of the ASP.NET Core Hosting Bundle.</span></span> <span data-ttu-id="d53c6-204">최신 버전은 지원되는 이전 버전의 ASP.NET Core 앱과 호환 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-204">The latest version is backwards-compatible with supported ASP.NET Core apps.</span></span>

## <a name="incorrect-processpath-missing-path-variable-hosting-bundle-not-installed-systemiis-not-restarted-vc-redistributable-not-installed-or-dotnetexe-access-violation"></a><span data-ttu-id="d53c6-205">잘못된 processPath, 누락된 PATH 변수, 설치되지 않은 호스팅 번들, 다시 시작되지 않은 시스템/IIS, 설치되지 않은 VC++ 재배포 가능 패키지 또는 dotnet.exe 액세스 위반</span><span class="sxs-lookup"><span data-stu-id="d53c6-205">Incorrect processPath, missing PATH variable, Hosting Bundle not installed, system/IIS not restarted, VC++ Redistributable not installed, or dotnet.exe access violation</span></span>

::: moniker range=">= aspnetcore-2.2"

* <span data-ttu-id="d53c6-206">**브라우저:** HTTP 오류 500.0 - ANCM In-Process 처리기 로드 실패</span><span class="sxs-lookup"><span data-stu-id="d53c6-206">**Browser:** HTTP Error 500.0 - ANCM In-Process Handler Load Failure</span></span>

* <span data-ttu-id="d53c6-207">**애플리케이션 로그:** 실제 루트 'C:\{PATH}\'가 있는 애플리케이션 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}'에서 '"{...}" 명령줄로 프로세스를 시작하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-207">**Application Log:** Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\{PATH}\' failed to start process with commandline '"{...}"</span></span> <span data-ttu-id="d53c6-208">', ErrorCode = '0x80070002 : 0.</span><span class="sxs-lookup"><span data-stu-id="d53c6-208">', ErrorCode = '0x80070002 : 0.</span></span> <span data-ttu-id="d53c6-209">애플리케이션 '{PATH}'를 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-209">Application '{PATH}' wasn't able to start.</span></span> <span data-ttu-id="d53c6-210">'{PATH}'에서 실행 파일을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-210">Executable was not found at '{PATH}'.</span></span> <span data-ttu-id="d53c6-211">애플리케이션 '/LM/W3SVC/2/ROOT'를 시작하지 못했습니다. 오류 코드 '0x8007023e'.</span><span class="sxs-lookup"><span data-stu-id="d53c6-211">Failed to start application '/LM/W3SVC/2/ROOT', ErrorCode '0x8007023e'.</span></span>

* <span data-ttu-id="d53c6-212">**ASP.NET Core 모듈 stdout 로그:** 로그 파일이 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-212">**ASP.NET Core Module stdout Log:** The log file isn't created.</span></span>

* <span data-ttu-id="d53c6-213">**ASP.NET Core 모듈 디버그 로그:** 이벤트 로그: '애플리케이션 '{PATH}'를 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-213">**ASP.NET Core Module Debug Log:** Event Log: 'Application '{PATH}' wasn't able to start.</span></span> <span data-ttu-id="d53c6-214">'{PATH}'에서 실행 파일을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-214">Executable was not found at '{PATH}'.</span></span> <span data-ttu-id="d53c6-215">실패한 HRESULT가 반환되었습니다. 0x8007023e</span><span class="sxs-lookup"><span data-stu-id="d53c6-215">Failed HRESULT returned: 0x8007023e</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

* <span data-ttu-id="d53c6-216">**브라우저:** HTTP 오류 502.5 - 프로세스 오류</span><span class="sxs-lookup"><span data-stu-id="d53c6-216">**Browser:** HTTP Error 502.5 - Process Failure</span></span>

* <span data-ttu-id="d53c6-217">**애플리케이션 로그:** 실제 루트 'C:\{PATH}\'가 있는 애플리케이션 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}'에서 '"{...}" 명령줄로 프로세스를 시작하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-217">**Application Log:** Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\{PATH}\' failed to start process with commandline '"{...}"</span></span> <span data-ttu-id="d53c6-218">', ErrorCode = '0x80070002 : 0.</span><span class="sxs-lookup"><span data-stu-id="d53c6-218">', ErrorCode = '0x80070002 : 0.</span></span>

* <span data-ttu-id="d53c6-219">**ASP.NET Core 모듈 stdout 로그:** 로그 파일이 생성되었지만 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-219">**ASP.NET Core Module stdout Log:** The log file is created but empty.</span></span>

::: moniker-end

<span data-ttu-id="d53c6-220">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="d53c6-220">Troubleshooting:</span></span>

* <span data-ttu-id="d53c6-221">앱이 Kestrel에서 로컬로 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-221">Confirm that the app runs locally on Kestrel.</span></span> <span data-ttu-id="d53c6-222">프로세스 오류는 앱 내의 문제 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-222">A process failure might be the result of a problem within the app.</span></span> <span data-ttu-id="d53c6-223">자세한 내용은 [문제 해결(IIS)](xref:host-and-deploy/iis/troubleshoot) 또는 [문제 해결(Azure App Service)](xref:host-and-deploy/azure-apps/troubleshoot)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d53c6-223">For more information, see [Troubleshoot (IIS)](xref:host-and-deploy/iis/troubleshoot) or [Troubleshoot (Azure App Service)](xref:host-and-deploy/azure-apps/troubleshoot).</span></span>

* <span data-ttu-id="d53c6-224">*web.config*의 `<aspNetCore>` 요소에서 *processPath* 특성을 확인하여 FDD(프레임워크 종속 배포)에 대한 `dotnet`인지 또는 [SCD(자체 포함 배포)](/dotnet/core/deploying/#self-contained-deployments-scd)에 대한 `.\{ASSEMBLY}.exe`인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-224">Check the *processPath* attribute on the `<aspNetCore>` element in *web.config* to confirm that it's `dotnet` for a framework-dependent deployment (FDD) or `.\{ASSEMBLY}.exe` for a [self-contained deployment (SCD)](/dotnet/core/deploying/#self-contained-deployments-scd).</span></span>

* <span data-ttu-id="d53c6-225">FDD의 경우 *dotnet.exe*에서 PATH 설정을 통해 액세스하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-225">For an FDD, *dotnet.exe* might not be accessible via the PATH settings.</span></span> <span data-ttu-id="d53c6-226">시스템 PATH 설정에 *C:\Program Files\dotnet\\* 이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-226">Confirm that *C:\Program Files\dotnet\\* exists in the System PATH settings.</span></span>

* <span data-ttu-id="d53c6-227">FDD의 경우 *dotnet.exe*에서 앱 풀의 사용자 ID에 액세스하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-227">For an FDD, *dotnet.exe* might not be accessible for the user identity of the app pool.</span></span> <span data-ttu-id="d53c6-228">앱 풀 사용자 ID에 *C:\Program Files\dotnet* 디렉터리에 대한 액세스 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-228">Confirm that the app pool user identity has access to the *C:\Program Files\dotnet* directory.</span></span> <span data-ttu-id="d53c6-229">*C:\Program Files\dotnet* 및 앱 디렉터리에 앱 풀 사용자 ID에 대해 구성된 거부 규칙이 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-229">Confirm that there are no deny rules configured for the app pool user identity on the *C:\Program Files\dotnet* and app directories.</span></span>

* <span data-ttu-id="d53c6-230">IIS를 다시 시작하지 않은 상태로 FDD를 배포하고 .NET Core를 설치했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-230">An FDD may have been deployed and .NET Core installed without restarting IIS.</span></span> <span data-ttu-id="d53c6-231">서버를 다시 시작하거나 명령 프롬프트에서 **net stop was /y**에 이어 **net start w3svc**를 실행하여 IIS를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-231">Either restart the server or restart IIS by executing **net stop was /y** followed by **net start w3svc** from a command prompt.</span></span>

* <span data-ttu-id="d53c6-232">호스팅 시스템에 .NET Core 런타임을 설치하지 않고 FDD를 배포했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-232">An FDD may have been deployed without installing the .NET Core runtime on the hosting system.</span></span> <span data-ttu-id="d53c6-233">.NET Core 런타임이 설치되어 있지 않으면 시스템에서 **.NET Core 호스팅 번들 설치 관리자**를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-233">If the .NET Core runtime hasn't been installed, run the **.NET Core Hosting Bundle installer** on the system.</span></span>

  [<span data-ttu-id="d53c6-234">현재 .NET Core 호스팅 번들 설치 관리자(직접 다운로드)</span><span class="sxs-lookup"><span data-stu-id="d53c6-234">Current .NET Core Hosting Bundle installer (direct download)</span></span>](https://www.microsoft.com/net/permalink/dotnetcore-current-windows-runtime-bundle-installer)

  <span data-ttu-id="d53c6-235">자세한 내용은 [.NET Core 호스팅 번들 설치](xref:host-and-deploy/iis/index#install-the-net-core-hosting-bundle)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d53c6-235">For more information, see [Install the .NET Core Hosting Bundle](xref:host-and-deploy/iis/index#install-the-net-core-hosting-bundle).</span></span>

  <span data-ttu-id="d53c6-236">특정 런타임이 필요한 경우 [.NET Download Archives](https://dotnet.microsoft.com/download/archives)에서 런타임을 다운로드하여 시스템에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-236">If a specific runtime is required, download the runtime from the [.NET Download Archives](https://dotnet.microsoft.com/download/archives) and install it on the system.</span></span> <span data-ttu-id="d53c6-237">설치를 완료하려면 시스템을 다시 시작하거나 명령 프롬프트에서 **net stop was /y**에 이어 **net start w3svc**를 실행하여 IIS를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-237">Complete the installation by restarting the system or restarting IIS by executing **net stop was /y** followed by **net start w3svc** from a command prompt.</span></span>

* <span data-ttu-id="d53c6-238">FDD를 배포했을 수 있지만 ‘Microsoft Visual C++ 2015 재배포 가능 패키지(x64)’가 시스템에 설치되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-238">An FDD may have been deployed and the *Microsoft Visual C++ 2015 Redistributable (x64)* isn't installed on the system.</span></span> <span data-ttu-id="d53c6-239">[Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=53840)에서 설치 관리자를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-239">Obtain an installer from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53840).</span></span>

## <a name="incorrect-arguments-of-aspnetcore-element"></a><span data-ttu-id="d53c6-240">\<aspNetCore> 요소의 잘못된 인수</span><span class="sxs-lookup"><span data-stu-id="d53c6-240">Incorrect arguments of \<aspNetCore> element</span></span>

::: moniker range=">= aspnetcore-2.2"

* <span data-ttu-id="d53c6-241">**브라우저:** HTTP 오류 500.0 - ANCM In-Process 처리기 로드 실패</span><span class="sxs-lookup"><span data-stu-id="d53c6-241">**Browser:** HTTP Error 500.0 - ANCM In-Process Handler Load Failure</span></span>

* <span data-ttu-id="d53c6-242">**애플리케이션 로그:** hostfxr를 호출하여 inprocess 요청 처리기를 찾는 데 실패했으며 네이티브 종속성을 찾지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-242">**Application Log:** Invoking hostfxr to find the inprocess request handler failed without finding any native dependencies.</span></span> <span data-ttu-id="d53c6-243">이는 앱이 잘못 구성되었음을 의미할 가능성이 높으며, 앱이 대상으로 하고 머신에 설치되어 있는 Microsoft.NetCore.App 및 Microsoft.AspNetCore.App 버전을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="d53c6-243">This most likely means the app is misconfigured, please check the versions of Microsoft.NetCore.App and Microsoft.AspNetCore.App that are targeted by the application and are installed on the machine.</span></span> <span data-ttu-id="d53c6-244">inprocess 요청 처리기를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-244">Could not find inprocess request handler.</span></span> <span data-ttu-id="d53c6-245">hostfxr 호출에서 캡처된 출력: dotnet SDK 명령을 실행하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="d53c6-245">Captured output from invoking hostfxr: Did you mean to run dotnet SDK commands?</span></span> <span data-ttu-id="d53c6-246">다음 위치에서 dotnet SDK를 설치하세요. https://go.microsoft.com/fwlink/?LinkID=798306&clcid=0x409 애플리케이션 '/LM/W3SVC/3/ROOT'를 시작하지 못했습니다. 오류 코드 '0x8000ffff'.</span><span class="sxs-lookup"><span data-stu-id="d53c6-246">Please install dotnet SDK from: https://go.microsoft.com/fwlink/?LinkID=798306&clcid=0x409 Failed to start application '/LM/W3SVC/3/ROOT', ErrorCode '0x8000ffff'.</span></span>

* <span data-ttu-id="d53c6-247">**ASP.NET Core 모듈 stdout 로그:** dotnet SDK 명령을 실행하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="d53c6-247">**ASP.NET Core Module stdout Log:** Did you mean to run dotnet SDK commands?</span></span> <span data-ttu-id="d53c6-248">[https://go.microsoft.com/fwlink/?LinkID=798306&amp;clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=798306&clcid=0x409) 에서 dotnet SDK를 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="d53c6-248">Please install dotnet SDK from: https://go.microsoft.com/fwlink/?LinkID=798306&clcid=0x409</span></span>

* <span data-ttu-id="d53c6-249">**ASP.NET Core 모듈 디버그 로그:** hostfxr를 호출하여 inprocess 요청 처리기를 찾는 데 실패했으며 네이티브 종속성을 찾지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-249">**ASP.NET Core Module Debug Log:** Invoking hostfxr to find the inprocess request handler failed without finding any native dependencies.</span></span> <span data-ttu-id="d53c6-250">이는 앱이 잘못 구성되었음을 의미할 가능성이 높으며, 앱이 대상으로 하고 머신에 설치되어 있는 Microsoft.NetCore.App 및 Microsoft.AspNetCore.App 버전을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="d53c6-250">This most likely means the app is misconfigured, please check the versions of Microsoft.NetCore.App and Microsoft.AspNetCore.App that are targeted by the application and are installed on the machine.</span></span> <span data-ttu-id="d53c6-251">실패한 HRESULT가 반환되었습니다. 0x8000ffff inprocess 요청 처리기를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-251">Failed HRESULT returned: 0x8000ffff Could not find inprocess request handler.</span></span> <span data-ttu-id="d53c6-252">hostfxr 호출에서 캡처된 출력: dotnet SDK 명령을 실행하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="d53c6-252">Captured output from invoking hostfxr: Did you mean to run dotnet SDK commands?</span></span> <span data-ttu-id="d53c6-253">다음 위치에서 dotnet SDK를 설치하세요. https://go.microsoft.com/fwlink/?LinkID=798306&clcid=0x409 실패한 HRESULT가 반환되었습니다. 0x8000ffff</span><span class="sxs-lookup"><span data-stu-id="d53c6-253">Please install dotnet SDK from: https://go.microsoft.com/fwlink/?LinkID=798306&clcid=0x409 Failed HRESULT returned: 0x8000ffff</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

* <span data-ttu-id="d53c6-254">**브라우저:** HTTP 오류 502.5 - 프로세스 오류</span><span class="sxs-lookup"><span data-stu-id="d53c6-254">**Browser:** HTTP Error 502.5 - Process Failure</span></span>

* <span data-ttu-id="d53c6-255">**애플리케이션 로그:** 실제 루트 'C:\{PATH}\'가 있는 애플리케이션 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}'에서 '"dotnet" .\{ASSEMBLY}.dll' 명령줄로 프로세스를 시작하지 못했습니다. 오류 코드 = '0x80004005 : 80008081.</span><span class="sxs-lookup"><span data-stu-id="d53c6-255">**Application Log:** Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\{PATH}\' failed to start process with commandline '"dotnet" .\{ASSEMBLY}.dll', ErrorCode = '0x80004005 : 80008081.</span></span>

* <span data-ttu-id="d53c6-256">**ASP.NET Core 모듈 stdout 로그:** 실행할 애플리케이션이 없습니다. 'PATH\{ASSEMBLY}.dll'</span><span class="sxs-lookup"><span data-stu-id="d53c6-256">**ASP.NET Core Module stdout Log:** The application to execute does not exist: 'PATH\{ASSEMBLY}.dll'</span></span>

::: moniker-end

<span data-ttu-id="d53c6-257">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="d53c6-257">Troubleshooting:</span></span>

* <span data-ttu-id="d53c6-258">앱이 Kestrel에서 로컬로 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-258">Confirm that the app runs locally on Kestrel.</span></span> <span data-ttu-id="d53c6-259">프로세스 오류는 앱 내의 문제 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-259">A process failure might be the result of a problem within the app.</span></span> <span data-ttu-id="d53c6-260">자세한 내용은 [문제 해결(IIS)](xref:host-and-deploy/iis/troubleshoot) 또는 [문제 해결(Azure App Service)](xref:host-and-deploy/azure-apps/troubleshoot)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d53c6-260">For more information, see [Troubleshoot (IIS)](xref:host-and-deploy/iis/troubleshoot) or [Troubleshoot (Azure App Service)](xref:host-and-deploy/azure-apps/troubleshoot).</span></span>

* <span data-ttu-id="d53c6-261">*web.config*의 `<aspNetCore>` 요소에서 *인수* 특성을 검사하여 (a) FDD(프레임워크 종속 배포)에 대한 `.\{ASSEMBLY}.dll`인지, 또는 (b) 없는 경우 빈 문자열(`arguments=""`)이거나 SCD(자체 포함 배포)에 대한 앱의 인수(`arguments="{ARGUMENT_1}, {ARGUMENT_2}, ... {ARGUMENT_X}"`) 목록인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-261">Examine the *arguments* attribute on the `<aspNetCore>` element in *web.config* to confirm that it's either (a) `.\{ASSEMBLY}.dll` for a framework-dependent deployment (FDD); or (b) not present, an empty string (`arguments=""`), or a list of the app's arguments (`arguments="{ARGUMENT_1}, {ARGUMENT_2}, ... {ARGUMENT_X}"`) for a self-contained deployment (SCD).</span></span>

::: moniker range=">= aspnetcore-2.2"

## <a name="missing-net-core-shared-framework"></a><span data-ttu-id="d53c6-262">.NET Core 공유 프레임워크 누락</span><span class="sxs-lookup"><span data-stu-id="d53c6-262">Missing .NET Core shared framework</span></span>

* <span data-ttu-id="d53c6-263">**브라우저:** HTTP 오류 500.0 - ANCM In-Process 처리기 로드 실패</span><span class="sxs-lookup"><span data-stu-id="d53c6-263">**Browser:** HTTP Error 500.0 - ANCM In-Process Handler Load Failure</span></span>

* <span data-ttu-id="d53c6-264">**애플리케이션 로그:** hostfxr를 호출하여 inprocess 요청 처리기를 찾는 데 실패했으며 네이티브 종속성을 찾지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-264">**Application Log:** Invoking hostfxr to find the inprocess request handler failed without finding any native dependencies.</span></span> <span data-ttu-id="d53c6-265">이는 앱이 잘못 구성되었음을 의미할 가능성이 높으며, 앱이 대상으로 하고 머신에 설치되어 있는 Microsoft.NetCore.App 및 Microsoft.AspNetCore.App 버전을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="d53c6-265">This most likely means the app is misconfigured, please check the versions of Microsoft.NetCore.App and Microsoft.AspNetCore.App that are targeted by the application and are installed on the machine.</span></span> <span data-ttu-id="d53c6-266">inprocess 요청 처리기를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-266">Could not find inprocess request handler.</span></span> <span data-ttu-id="d53c6-267">hostfxr 호출에서 캡처된 출력: 호환 가능한 프레임워크 버전을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-267">Captured output from invoking hostfxr: It was not possible to find any compatible framework version.</span></span> <span data-ttu-id="d53c6-268">지정된 프레임워크 'Microsoft.AspNetCore.App', 버전 '{VERSION}'을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-268">The specified framework 'Microsoft.AspNetCore.App', version '{VERSION}' was not found.</span></span>

<span data-ttu-id="d53c6-269">애플리케이션 '/LM/W3SVC/5/ROOT'를 시작하지 못했습니다. 오류 코드 '0x8000ffff'.</span><span class="sxs-lookup"><span data-stu-id="d53c6-269">Failed to start application '/LM/W3SVC/5/ROOT', ErrorCode '0x8000ffff'.</span></span>

* <span data-ttu-id="d53c6-270">**ASP.NET Core 모듈 stdout 로그:** 호환 가능한 프레임워크 버전을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-270">**ASP.NET Core Module stdout Log:** It was not possible to find any compatible framework version.</span></span> <span data-ttu-id="d53c6-271">지정된 프레임워크 'Microsoft.AspNetCore.App', 버전 '{VERSION}'을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-271">The specified framework 'Microsoft.AspNetCore.App', version '{VERSION}' was not found.</span></span>

* <span data-ttu-id="d53c6-272">**ASP.NET Core 모듈 디버그 로그:** 실패한 HRESULT가 반환되었습니다. 0x8000ffff</span><span class="sxs-lookup"><span data-stu-id="d53c6-272">**ASP.NET Core Module Debug Log:** Failed HRESULT returned: 0x8000ffff</span></span>

::: moniker-end

<span data-ttu-id="d53c6-273">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="d53c6-273">Troubleshooting:</span></span>

<span data-ttu-id="d53c6-274">FDD(프레임워크 종속 배포)의 경우 시스템에 올바른 런타임이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-274">For a framework-dependent deployment (FDD), confirm that the correct runtime installed on the system.</span></span>

## <a name="stopped-application-pool"></a><span data-ttu-id="d53c6-275">중지된 애플리케이션 풀</span><span class="sxs-lookup"><span data-stu-id="d53c6-275">Stopped Application Pool</span></span>

* <span data-ttu-id="d53c6-276">**브라우저:** 503 서비스를 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="d53c6-276">**Browser:** 503 Service Unavailable</span></span>

* <span data-ttu-id="d53c6-277">**애플리케이션 로그:** 진입 금지</span><span class="sxs-lookup"><span data-stu-id="d53c6-277">**Application Log:** No entry</span></span>

* <span data-ttu-id="d53c6-278">**ASP.NET Core 모듈 stdout 로그:** 로그 파일이 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-278">**ASP.NET Core Module stdout Log:** The log file isn't created.</span></span>

::: moniker range=">= aspnetcore-2.2"

* <span data-ttu-id="d53c6-279">**ASP.NET Core 모듈 디버그 로그:** 로그 파일이 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-279">**ASP.NET Core Module Debug Log:** The log file isn't created.</span></span>

::: moniker-end

<span data-ttu-id="d53c6-280">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="d53c6-280">Troubleshooting:</span></span>

<span data-ttu-id="d53c6-281">애플리케이션 풀이 ‘중지됨’ 상태가 아닌지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-281">Confirm that the Application Pool isn't in the *Stopped* state.</span></span>

## <a name="sub-application-includes-a-handlers-section"></a><span data-ttu-id="d53c6-282">하위 애플리케이션에 \<handlers> 섹션이 포함되어 있음</span><span class="sxs-lookup"><span data-stu-id="d53c6-282">Sub-application includes a \<handlers> section</span></span>

* <span data-ttu-id="d53c6-283">**브라우저:** HTTP 오류 500.19 - 내부 서버 오류</span><span class="sxs-lookup"><span data-stu-id="d53c6-283">**Browser:** HTTP Error 500.19 - Internal Server Error</span></span>

* <span data-ttu-id="d53c6-284">**애플리케이션 로그:** 진입 금지</span><span class="sxs-lookup"><span data-stu-id="d53c6-284">**Application Log:** No entry</span></span>

* <span data-ttu-id="d53c6-285">**ASP.NET Core 모듈 stdout 로그:** 루트 앱의 로그 파일이 생성되고 정상 작동을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-285">**ASP.NET Core Module stdout Log:** The root app's log file is created and shows normal operation.</span></span> <span data-ttu-id="d53c6-286">하위 앱의 로그 파일이 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-286">The sub-app's log file isn't created.</span></span>

::: moniker range=">= aspnetcore-2.2"

* <span data-ttu-id="d53c6-287">**ASP.NET Core 모듈 디버그 로그:** 루트 앱의 로그 파일이 생성되고 정상 작동을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-287">**ASP.NET Core Module Debug Log:** The root app's log file is created and shows normal operation.</span></span> <span data-ttu-id="d53c6-288">하위 앱의 로그 파일이 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-288">The sub-app's log file isn't created.</span></span>

::: moniker-end

<span data-ttu-id="d53c6-289">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="d53c6-289">Troubleshooting:</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="d53c6-290">하위 앱의 *web.config* 파일에 `<handlers>` 섹션이 포함되어 있지 않거나 하위 앱이 부모 앱의 처리기를 상속하지 않았는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-290">Confirm that the sub-app's *web.config* file doesn't include a `<handlers>` section or that the sub-app doesn't inherit the parent app's handlers.</span></span>

<span data-ttu-id="d53c6-291">*web.config*의 부모 앱 `<system.webServer>` 섹션은 `<location>` 요소 내부에 배치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-291">The parent app's `<system.webServer>` section of *web.config* is placed inside of a `<location>` element.</span></span> <span data-ttu-id="d53c6-292"><xref:System.Configuration.SectionInformation.InheritInChildApplications*> 속성이 `false`로 설정되어 [\<location>](/iis/manage/managing-your-configuration-settings/understanding-iis-configuration-delegation#the-concept-of-location) 요소 내에서 지정된 설정이 부모 앱의 하위 디렉터리에 있는 앱에 상속되지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-292">The <xref:System.Configuration.SectionInformation.InheritInChildApplications*> property is set to `false` to indicate that the settings specified within the [\<location>](/iis/manage/managing-your-configuration-settings/understanding-iis-configuration-delegation#the-concept-of-location) element aren't inherited by apps that reside in a subdirectory of the parent app.</span></span> <span data-ttu-id="d53c6-293">자세한 내용은 <xref:host-and-deploy/aspnet-core-module>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d53c6-293">For more information, see <xref:host-and-deploy/aspnet-core-module>.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="d53c6-294">하위 앱의 *web.config* 파일에 `<handlers>` 섹션이 포함되어 있지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-294">Confirm that the sub-app's *web.config* file doesn't include a `<handlers>` section.</span></span>

::: moniker-end

## <a name="stdout-log-path-incorrect"></a><span data-ttu-id="d53c6-295">stdout 로그 경로가 올바르지 않음</span><span class="sxs-lookup"><span data-stu-id="d53c6-295">stdout log path incorrect</span></span>

* <span data-ttu-id="d53c6-296">**브라우저:** 앱이 정상적으로 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-296">**Browser:** The app responds normally.</span></span>

::: moniker range=">= aspnetcore-2.2"

* <span data-ttu-id="d53c6-297">**애플리케이션 로그:** C:\Program Files\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll에서 stdout 리디렉션을 시작하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-297">**Application Log:** Could not start stdout redirection in C:\Program Files\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll.</span></span> <span data-ttu-id="d53c6-298">예외 메시지: HRESULT 0x80070005가 {PATH}\aspnetcoremodulev2\commonlib\fileoutputmanager.cpp:84에서 반환되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-298">Exception message: HRESULT 0x80070005 returned at {PATH}\aspnetcoremodulev2\commonlib\fileoutputmanager.cpp:84.</span></span> <span data-ttu-id="d53c6-299">C:\Program Files\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll에서 stdout 리디렉션을 중지하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-299">Could not stop stdout redirection in C:\Program Files\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll.</span></span> <span data-ttu-id="d53c6-300">예외 메시지: HRESULT 0x80070002가 {PATH}에서 반환되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-300">Exception message: HRESULT 0x80070002 returned at {PATH}.</span></span> <span data-ttu-id="d53c6-301">{PATH}\aspnetcorev2_inprocess.dll에서 stdout 리디렉션을 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-301">Could not start stdout redirection in {PATH}\aspnetcorev2_inprocess.dll.</span></span>

* <span data-ttu-id="d53c6-302">**ASP.NET Core 모듈 stdout 로그:** 로그 파일이 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-302">**ASP.NET Core Module stdout Log:** The log file isn't created.</span></span>

* <span data-ttu-id="d53c6-303">**ASP.NET Core 모듈 디버그 로그:** C:\Program Files\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll에서 stdout 리디렉션을 시작하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-303">**ASP.NET Core Module debug Log:** Could not start stdout redirection in C:\Program Files\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll.</span></span> <span data-ttu-id="d53c6-304">예외 메시지: HRESULT 0x80070005가 {PATH}\aspnetcoremodulev2\commonlib\fileoutputmanager.cpp:84에서 반환되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-304">Exception message: HRESULT 0x80070005 returned at {PATH}\aspnetcoremodulev2\commonlib\fileoutputmanager.cpp:84.</span></span> <span data-ttu-id="d53c6-305">C:\Program Files\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll에서 stdout 리디렉션을 중지하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-305">Could not stop stdout redirection in C:\Program Files\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll.</span></span> <span data-ttu-id="d53c6-306">예외 메시지: HRESULT 0x80070002가 {PATH}에서 반환되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-306">Exception message: HRESULT 0x80070002 returned at {PATH}.</span></span> <span data-ttu-id="d53c6-307">{PATH}\aspnetcorev2_inprocess.dll에서 stdout 리디렉션을 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-307">Could not start stdout redirection in {PATH}\aspnetcorev2_inprocess.dll.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

* <span data-ttu-id="d53c6-308">**애플리케이션 로그:** 경고: stdoutLogFile \\?\{PATH}\path_doesnt_exist\stdout_{PROCESS ID}_{TIMESTAMP}.log를 만들지 못했습니다. 오류 코드 = -2147024893.</span><span class="sxs-lookup"><span data-stu-id="d53c6-308">**Application Log:** Warning: Could not create stdoutLogFile \\?\{PATH}\path_doesnt_exist\stdout_{PROCESS ID}_{TIMESTAMP}.log, ErrorCode = -2147024893.</span></span>

* <span data-ttu-id="d53c6-309">**ASP.NET Core 모듈 stdout 로그:** 로그 파일이 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-309">**ASP.NET Core Module stdout Log:** The log file isn't created.</span></span>

::: moniker-end

<span data-ttu-id="d53c6-310">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="d53c6-310">Troubleshooting:</span></span>

* <span data-ttu-id="d53c6-311">*web.config*의 `<aspNetCore>` 요소에 지정된 `stdoutLogFile` 경로가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-311">The `stdoutLogFile` path specified in the `<aspNetCore>` element of *web.config* doesn't exist.</span></span> <span data-ttu-id="d53c6-312">자세한 내용은 [ASP.NET Core 모듈: 로그 만들기 및 리디렉션](xref:host-and-deploy/aspnet-core-module#log-creation-and-redirection)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d53c6-312">For more information, see [ASP.NET Core Module: Log creation and redirection](xref:host-and-deploy/aspnet-core-module#log-creation-and-redirection).</span></span>

* <span data-ttu-id="d53c6-313">앱 풀 사용자는 stdout 로그 경로에 대한 쓰기 액세스 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-313">The app pool user doesn't have write access to the stdout log path.</span></span>

## <a name="application-configuration-general-issue"></a><span data-ttu-id="d53c6-314">일반적인 애플리케이션 구성 문제</span><span class="sxs-lookup"><span data-stu-id="d53c6-314">Application configuration general issue</span></span>

::: moniker range=">= aspnetcore-2.2"

* <span data-ttu-id="d53c6-315">**브라우저:** HTTP 오류 500.0 - ANCM In-Process 처리기 로드 실패 **--또는--** HTTP 오류 500.30 - ANCM In-Process 시작 실패</span><span class="sxs-lookup"><span data-stu-id="d53c6-315">**Browser:** HTTP Error 500.0 - ANCM In-Process Handler Load Failure **--OR--** HTTP Error 500.30 - ANCM In-Process Start Failure</span></span>

* <span data-ttu-id="d53c6-316">**애플리케이션 로그:** 변수</span><span class="sxs-lookup"><span data-stu-id="d53c6-316">**Application Log:** Variable</span></span>

* <span data-ttu-id="d53c6-317">**ASP.NET Core 모듈 stdout 로그:** 로그 파일은 생성되지만 비어 있거나 앱이 실패할 때까지 일반 항목으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-317">**ASP.NET Core Module stdout Log:** The log file is created but empty or created with normal entries until the point of the app failing.</span></span>

* <span data-ttu-id="d53c6-318">**ASP.NET Core 모듈 디버그 로그:** 변수</span><span class="sxs-lookup"><span data-stu-id="d53c6-318">**ASP.NET Core Module Debug Log:** Variable</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

* <span data-ttu-id="d53c6-319">**브라우저:** HTTP 오류 502.5 - 프로세스 오류</span><span class="sxs-lookup"><span data-stu-id="d53c6-319">**Browser:** HTTP Error 502.5 - Process Failure</span></span>

* <span data-ttu-id="d53c6-320">**애플리케이션 로그:** 실제 루트 'C:\{PATH}\'가 있는 애플리케이션 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}'에서 '"C:\{PATH}\{ASSEMBLY}.{exe|dll}" ' 명령줄로 프로세스를 만들었지만 지정된 포트 '{PORT}'에서 크래시하거나 응답하지 않거나 수신 대기하지 않습니다. 오류 코드 = '{ERROR CODE}'</span><span class="sxs-lookup"><span data-stu-id="d53c6-320">**Application Log:** Application 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}' with physical root 'C:\{PATH}\' created process with commandline '"C:\{PATH}\{ASSEMBLY}.{exe|dll}" ' but either crashed or did not respond or did not listen on the given port '{PORT}', ErrorCode = '{ERROR CODE}'</span></span>

* <span data-ttu-id="d53c6-321">**ASP.NET Core 모듈 stdout 로그:** 로그 파일이 생성되었지만 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-321">**ASP.NET Core Module stdout Log:** The log file is created but empty.</span></span>

::: moniker-end

<span data-ttu-id="d53c6-322">문제 해결:</span><span class="sxs-lookup"><span data-stu-id="d53c6-322">Troubleshooting:</span></span>

<span data-ttu-id="d53c6-323">앱 구성 또는 프로그래밍 문제로 인해 프로세스를 시작하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="d53c6-323">The process failed to start, most likely due to an app configuration or programming issue.</span></span>

<span data-ttu-id="d53c6-324">자세한 내용은 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d53c6-324">For more information, see the following topics:</span></span>

* <xref:host-and-deploy/iis/troubleshoot>
* <xref:host-and-deploy/azure-apps/troubleshoot>
* <xref:test/troubleshoot>
