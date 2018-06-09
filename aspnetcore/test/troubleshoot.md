---
title: ASP.NET Core에 대 한 문제 해결
author: Rick-Anderson
description: 이해 하 고 경고 및 ASP.NET Core 프로젝트를 사용 하 여 오류를 해결 합니다.
manager: wpickett
ms.author: riande
ms.date: 04/05/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: content
uid: test/troubleshoot
ms.openlocfilehash: 64a353a9bdf0753c63f676f9d07f42ba45acdcab
ms.sourcegitcommit: 43bd79667bbdc8a07bd39fb4cd6f7ad3e70212fb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "35217649"
---
# <a name="troubleshoot-aspnet-core-projects"></a><span data-ttu-id="170d0-103">ASP.NET Core 프로젝트 문제 해결</span><span class="sxs-lookup"><span data-stu-id="170d0-103">Troubleshoot ASP.NET Core projects</span></span>

<span data-ttu-id="170d0-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="170d0-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="170d0-105">다음 링크는 문제 해결 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-105">The following links provide troubleshooting guidance:</span></span>

* [<span data-ttu-id="170d0-106">Azure App Service에서 ASP.NET Core 문제 해결</span><span class="sxs-lookup"><span data-stu-id="170d0-106">Troubleshoot ASP.NET Core on Azure App Service</span></span>](xref:host-and-deploy/azure-apps/troubleshoot)
* [<span data-ttu-id="170d0-107">IIS에서 ASP.NET Core 문제 해결</span><span class="sxs-lookup"><span data-stu-id="170d0-107">Troubleshoot ASP.NET Core on IIS</span></span>](xref:host-and-deploy/iis/troubleshoot)
* [<span data-ttu-id="170d0-108">ASP.NET Core를 사용하는 Azure App Service 및 IIS에 대한 일반적인 오류 참조</span><span class="sxs-lookup"><span data-stu-id="170d0-108">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)
* [<span data-ttu-id="170d0-109">YouTube: ASP.NET Core 응용 프로그램의 문제 진단</span><span class="sxs-lookup"><span data-stu-id="170d0-109">YouTube: Diagnosing issues in ASP.NET Core Applications</span></span>](https://www.youtube.com/watch?v=RYI0DHoIVaA)

<a name="sdk"></a>
## <a name="net-core-sdk-warnings"></a><span data-ttu-id="170d0-110">.NET core SDK 경고</span><span class="sxs-lookup"><span data-stu-id="170d0-110">.NET Core SDK warnings</span></span>

### <a name="both-the-32-bit-and-64-bit-versions-of-the-net-core-sdk-are-installed"></a><span data-ttu-id="170d0-111">설치 되는 32 비트 및 64 비트 버전의.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="170d0-111">Both the 32 bit and 64 bit versions of the .NET Core SDK are installed</span></span>
<span data-ttu-id="170d0-112">에 **새 프로젝트** 대화 ASP.NET Core에 대 한 다음과 같은 경고가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-112">In the **New Project** dialog for ASP.NET Core, you may see the following warning:</span></span> 

    Both 32 and 64 bit versions of the .NET Core SDK are installed. Only templates from the 64 bit version(s) installed at C:\Program Files\dotnet\sdk\" will be displayed.

![경고 메시지를 보여 주는 OneASP.NET 대화 상자의 스크린 샷](troubleshoot/_static/both32and64bit.png)

<span data-ttu-id="170d0-114">이 경고를 표시 하는 경우 (x86) 32 비트 및 64 비트 (x64) 버전의 모두는 [.NET Core SDK](https://www.microsoft.com/net/download/all) 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-114">This warning appears when both 32-bit (x86) and 64-bit (x64) versions of the [.NET Core SDK](https://www.microsoft.com/net/download/all) are installed.</span></span> <span data-ttu-id="170d0-115">두 버전을 설치 하려면 일반적인 원인은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-115">Common reasons both versions can be installed include:</span></span>

* <span data-ttu-id="170d0-116">원래 32 비트 컴퓨터를 사용 하는.NET Core SDK 설치 관리자 다운로드 하지만 다음 복사 프로세스를 수행한 후 하는 64 비트 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-116">You originally downloaded the .NET Core SDK installer using a 32-bit machine, but then copied it across and installed it on a 64-bit machine.</span></span> 
* <span data-ttu-id="170d0-117">32 비트.NET Core SDK가 다른 응용 프로그램으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-117">The 32-bit .NET Core SDK was installed by another application.</span></span>
* <span data-ttu-id="170d0-118">잘못 된 버전은 다운로드 되어 설치 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-118">The wrong version was downloaded and installed.</span></span>

<span data-ttu-id="170d0-119">이 경고를 방지 하기 위해 32 비트.NET Core SDK를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-119">Uninstall the 32-bit .NET Core SDK to prevent this warning.</span></span> <span data-ttu-id="170d0-120">제거 **제어판** > **프로그램 및 기능** > **제거 또는 변경 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-120">Uninstall from **Control Panel** > **Programs and Features** > **Uninstall or change a program**.</span></span> <span data-ttu-id="170d0-121">경고의 발생 이유 및 그 의미를 이해 하는 경우 경고를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-121">If you understand why the warning occurs and its implications, you can ignore the warning.</span></span>

### <a name="the-net-core-sdk-is-installed-in-multiple-locations"></a><span data-ttu-id="170d0-122">.NET Core SDK가 여러 위치에 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-122">The .NET Core SDK is installed in multiple locations</span></span>
<span data-ttu-id="170d0-123">에 **새 프로젝트** 대화 ASP.NET Core에 대 한 다음과 같은 경고가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-123">In the **New Project** dialog for ASP.NET Core you may see the following warning:</span></span> 

 <span data-ttu-id="170d0-124">.NET Core SDK는 여러 위치에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-124">The .NET Core SDK is installed in multiple locations.</span></span> <span data-ttu-id="170d0-125">에 설치 된과에서 템플릿만 ' C:\Program Files\dotnet\sdk\' 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-125">Only templates from the SDK(s) installed at 'C:\Program Files\dotnet\sdk\' will be displayed.</span></span>

![경고 메시지를 보여 주는 OneASP.NET 대화 상자의 스크린 샷](troubleshoot/_static/multiplelocations.png)

<span data-ttu-id="170d0-127">.NET Core SDK의 하나 이상 설치 디렉터리의 외부에 있는 경우이 메시지가 나타나는 * C:\Program Files\dotnet\sdk\*합니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-127">You see this message when you have at least one installation of the .NET Core SDK in a directory outside of *C:\Program Files\dotnet\sdk\*.</span></span> <span data-ttu-id="170d0-128">일반적으로.NET Core SDK MSI 설치 프로그램을 대신 복사/붙여넣기를 사용 하는 컴퓨터에 배포 된 경우 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-128">Usually that happens when the .NET Core SDK has been deployed on a machine using copy/paste instead of the MSI installer.</span></span>

<span data-ttu-id="170d0-129">이 경고를 방지 하기 위해 32 비트.NET Core SDK를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-129">Uninstall the 32-bit .NET Core SDK to prevent this warning.</span></span> <span data-ttu-id="170d0-130">제거 **제어판** > **프로그램 및 기능** > **제거 또는 변경 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-130">Uninstall from **Control Panel** > **Programs and Features** > **Uninstall or change a program**.</span></span> <span data-ttu-id="170d0-131">경고의 발생 이유 및 그 의미를 이해 하는 경우 경고를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-131">If you understand why the warning occurs and its implications, you can ignore the warning.</span></span>

### <a name="no-net-core-sdks-were-detected"></a><span data-ttu-id="170d0-132">.NET Core Sdk은 찾았습니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-132">No .NET Core SDKs were detected</span></span>
<span data-ttu-id="170d0-133">에 **새 프로젝트** 대화 ASP.NET Core에 대 한 다음과 같은 경고가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-133">In the **New Project** dialog for ASP.NET Core you may see the following warning:</span></span> 

<span data-ttu-id="170d0-134">**.NET Core Sdk를 찾았습니다., 'PATH' 환경 변수에 포함**</span><span class="sxs-lookup"><span data-stu-id="170d0-134">**No .NET Core SDKs were detected, ensure they are included in the environment variable 'PATH'**</span></span>

![경고 메시지를 보여 주는 OneASP.NET 대화 상자의 스크린 샷](troubleshoot/_static/NoNetCore.png)

<span data-ttu-id="170d0-136">이 경고를 표시 하는 경우 환경 변수 `PATH` 컴퓨터에 모든.NET Core Sdk를 가리키지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-136">This warning appears when the environment variable `PATH` doesn’t point to any .NET Core SDKs on the machine.</span></span> <span data-ttu-id="170d0-137">이 문제를 해결 방법:</span><span class="sxs-lookup"><span data-stu-id="170d0-137">To resolve this problem:</span></span>

* <span data-ttu-id="170d0-138">설치 또는.NET Core SDK 설치 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-138">Install or verify the .NET Core SDK is installed.</span></span>
* <span data-ttu-id="170d0-139">확인 된 `PATH` 환경 변수는 SDK가 설치 하는 위치를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-139">Verify the `PATH` environment variable points to the location the SDK is installed.</span></span> <span data-ttu-id="170d0-140">설치 관리자는 일반적으로 설정 된 `PATH`합니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-140">The installer normally sets the `PATH`.</span></span>

::: moniker range=">= aspnetcore-2.1"

### <a name="use-of-ihtmlhelperpartial-may-result-in-application-deadlocks"></a><span data-ttu-id="170d0-141">응용 프로그램 교착 상태에서 IHtmlHelper.Partial 사용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-141">Use of IHtmlHelper.Partial may result in application deadlocks</span></span>

<span data-ttu-id="170d0-142">ASP.NET Core 2.1 이상 버전에서는 호출 `Html.Partial` 교착 상태가 발생할 수 있으므로 분석기 경고를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-142">In ASP.NET Core 2.1 and later, calling `Html.Partial` results in an analyzer warning due to the potential for deadlocks.</span></span> <span data-ttu-id="170d0-143">가 경고 메시지:</span><span class="sxs-lookup"><span data-stu-id="170d0-143">The warning message is:</span></span>

<span data-ttu-id="170d0-144">*응용 프로그램 교착 상태에서 IHtmlHelper.Partial 사용 될 수 있습니다. 사용 하는 것이 좋습니다 `<partial>` 태그 도우미 또는 `IHtmlHelper.PartialAsync`합니다.*</span><span class="sxs-lookup"><span data-stu-id="170d0-144">*Use of IHtmlHelper.Partial may result in application deadlocks. Consider using `<partial>` Tag Helper or `IHtmlHelper.PartialAsync`.*</span></span>

<span data-ttu-id="170d0-145">에 대 한 호출이 `@Html.Partial` 으로 대체 해야 `@await Html.PartialAsync` 또는 부분 태그 도우미 `<partial name="_Partial" />`합니다.</span><span class="sxs-lookup"><span data-stu-id="170d0-145">Calls to `@Html.Partial` should be replaced by `@await Html.PartialAsync` or the partial tag helper `<partial name="_Partial" />`.</span></span>

::: moniker-end
