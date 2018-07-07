---
title: ASP.NET Core 프로젝트 문제 해결
author: Rick-Anderson
description: ASP.NET Core 프로젝트를 사용하여 경고 및 오류를 이해하고 문제를 해결합니다.
ms.author: riande
ms.date: 04/05/2018
uid: test/troubleshoot
ms.openlocfilehash: b4d90f541a4cda2d41b49101b7ea39af87a4dcb4
ms.sourcegitcommit: a09820f91e71a7d98b7347bf93210abb9e995e22
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2018
ms.locfileid: "37889014"
---
# <a name="troubleshoot-aspnet-core-projects"></a><span data-ttu-id="d651c-103">ASP.NET Core 프로젝트 문제 해결</span><span class="sxs-lookup"><span data-stu-id="d651c-103">Troubleshoot ASP.NET Core projects</span></span>

<span data-ttu-id="d651c-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="d651c-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="d651c-105">다음 링크를 문제 해결 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-105">The following links provide troubleshooting guidance:</span></span>

* [<span data-ttu-id="d651c-106">Azure App Service에서 ASP.NET Core 문제 해결</span><span class="sxs-lookup"><span data-stu-id="d651c-106">Troubleshoot ASP.NET Core on Azure App Service</span></span>](xref:host-and-deploy/azure-apps/troubleshoot)
* [<span data-ttu-id="d651c-107">IIS에서 ASP.NET Core 문제 해결</span><span class="sxs-lookup"><span data-stu-id="d651c-107">Troubleshoot ASP.NET Core on IIS</span></span>](xref:host-and-deploy/iis/troubleshoot)
* [<span data-ttu-id="d651c-108">ASP.NET Core를 사용하는 Azure App Service 및 IIS에 대한 일반적인 오류 참조</span><span class="sxs-lookup"><span data-stu-id="d651c-108">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)
* [<span data-ttu-id="d651c-109">ASP.NET Core 응용 프로그램에서 문제를 진단 하는 NDC 회의 (런던, 2018):</span><span class="sxs-lookup"><span data-stu-id="d651c-109">NDC Conference (London, 2018): Diagnosing issues in ASP.NET Core Applications</span></span>](https://www.youtube.com/watch?v=RYI0DHoIVaA)
* [<span data-ttu-id="d651c-110">ASP.NET Core 성능 문제를 해결 하는 ASP.NET 블로그:</span><span class="sxs-lookup"><span data-stu-id="d651c-110">ASP.NET Blog: Troubleshooting ASP.NET Core Performance Problems</span></span>](https://blogs.msdn.microsoft.com/webdev/2018/05/23/asp-net-core-performance-improvements/)

## <a name="net-core-sdk-warnings"></a><span data-ttu-id="d651c-111">.NET core SDK 경고</span><span class="sxs-lookup"><span data-stu-id="d651c-111">.NET Core SDK warnings</span></span>

### <a name="both-the-32-bit-and-64-bit-versions-of-the-net-core-sdk-are-installed"></a><span data-ttu-id="d651c-112">32 비트와 64 비트 버전의.NET Core SDK가 설치 된</span><span class="sxs-lookup"><span data-stu-id="d651c-112">Both the 32 bit and 64 bit versions of the .NET Core SDK are installed</span></span>

<span data-ttu-id="d651c-113">에 **새 프로젝트** 대화 ASP.NET Core에 대 한 다음과 같은 경고가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-113">In the **New Project** dialog for ASP.NET Core, you may see the following warning:</span></span>

> <span data-ttu-id="d651c-114">모두 32 비트 및 64 비트 버전의.NET Core SDK 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-114">Both 32 and 64 bit versions of the .NET Core SDK are installed.</span></span> <span data-ttu-id="d651c-115">에 설치 된 64 비트 버전의 템플릿만 ' c:\\Program Files\\dotnet\\sdk\\' 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-115">Only templates from the 64 bit version(s) installed at 'C:\\Program Files\\dotnet\\sdk\\' will be displayed.</span></span>

![경고 메시지를 보여 주는 OneASP.NET 대화 상자의 스크린샷](troubleshoot/_static/both32and64bit.png)

<span data-ttu-id="d651c-117">이 경고를 표시 하는 경우 32 비트 (x86)와 버전의 64 비트 (x64) 합니다 [.NET Core SDK](https://www.microsoft.com/net/download/all) 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-117">This warning appears when both 32-bit (x86) and 64-bit (x64) versions of the [.NET Core SDK](https://www.microsoft.com/net/download/all) are installed.</span></span> <span data-ttu-id="d651c-118">두 버전을 설치할 수 있습니다 하는 일반적인 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-118">Common reasons both versions may be installed include:</span></span>

* <span data-ttu-id="d651c-119">원래 32 비트 컴퓨터를 사용 하 여.NET Core SDK 설치 관리자를 다운로드 하지만 다음 복사 하는 것을 64 비트 컴퓨터에 설치.</span><span class="sxs-lookup"><span data-stu-id="d651c-119">You originally downloaded the .NET Core SDK installer using a 32-bit machine but then copied it across and installed it on a 64-bit machine.</span></span>
* <span data-ttu-id="d651c-120">32 비트.NET Core SDK가 다른 응용 프로그램으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-120">The 32-bit .NET Core SDK was installed by another application.</span></span>
* <span data-ttu-id="d651c-121">잘못 된 버전 다운로드 되어 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-121">The wrong version was downloaded and installed.</span></span>

<span data-ttu-id="d651c-122">이 경고를 방지 하기 위해 32 비트.NET Core SDK를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-122">Uninstall the 32-bit .NET Core SDK to prevent this warning.</span></span> <span data-ttu-id="d651c-123">제거할 **Control Panel** > **프로그램 및 기능** > **제거 또는 변경 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-123">Uninstall from **Control Panel** > **Programs and Features** > **Uninstall or change a program**.</span></span> <span data-ttu-id="d651c-124">경고가 발생 하는 이유 및 그 의미를 이해 하면 경고를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-124">If you understand why the warning occurs and its implications, you can ignore the warning.</span></span>

### <a name="the-net-core-sdk-is-installed-in-multiple-locations"></a><span data-ttu-id="d651c-125">여러 위치에서.NET Core SDK가 설치</span><span class="sxs-lookup"><span data-stu-id="d651c-125">The .NET Core SDK is installed in multiple locations</span></span>

<span data-ttu-id="d651c-126">에 **새 프로젝트** 대화 ASP.NET Core에 대 한 다음과 같은 경고가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-126">In the **New Project** dialog for ASP.NET Core, you may see the following warning:</span></span>

> <span data-ttu-id="d651c-127">.NET Core SDK는 여러 위치에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-127">The .NET Core SDK is installed in multiple locations.</span></span> <span data-ttu-id="d651c-128">Sdk의 템플릿만에 설치 된 템플릿 ' c:\\Program Files\\dotnet\\sdk\\' 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-128">Only templates from the SDK(s) installed at 'C:\\Program Files\\dotnet\\sdk\\' will be displayed.</span></span>

![경고 메시지를 보여 주는 OneASP.NET 대화 상자의 스크린샷](troubleshoot/_static/multiplelocations.png)

<span data-ttu-id="d651c-130">하나 이상의.NET Core SDK 설치 디렉터리 외부에 있는 경우에이 메시지를 참조 하세요 *c:\\Program Files\\dotnet\\sdk\\*합니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-130">You see this message when you have at least one installation of the .NET Core SDK in a directory outside of *C:\\Program Files\\dotnet\\sdk\\*.</span></span> <span data-ttu-id="d651c-131">일반적으로.NET Core SDK MSI 설치 관리자 대신 복사/붙여넣기를 사용 하는 컴퓨터에 배포 된 경우 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-131">Usually this happens when the .NET Core SDK has been deployed on a machine using copy/paste instead of the MSI installer.</span></span>

<span data-ttu-id="d651c-132">이 경고를 방지 하기 위해 32 비트.NET Core SDK를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-132">Uninstall the 32-bit .NET Core SDK to prevent this warning.</span></span> <span data-ttu-id="d651c-133">제거할 **Control Panel** > **프로그램 및 기능** > **제거 또는 변경 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-133">Uninstall from **Control Panel** > **Programs and Features** > **Uninstall or change a program**.</span></span> <span data-ttu-id="d651c-134">경고가 발생 하는 이유 및 그 의미를 이해 하면 경고를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-134">If you understand why the warning occurs and its implications, you can ignore the warning.</span></span>

### <a name="no-net-core-sdks-were-detected"></a><span data-ttu-id="d651c-135">.NET Core Sdk 발견</span><span class="sxs-lookup"><span data-stu-id="d651c-135">No .NET Core SDKs were detected</span></span>

<span data-ttu-id="d651c-136">에 **새 프로젝트** 대화 ASP.NET Core에 대 한 다음과 같은 경고가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-136">In the **New Project** dialog for ASP.NET Core, you may see the following warning:</span></span>

> <span data-ttu-id="d651c-137">.NET Core Sdk 발견, 'PATH' 환경 변수에 포함 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-137">No .NET Core SDKs were detected, ensure they are included in the environment variable 'PATH'.</span></span>

![경고 메시지를 보여 주는 OneASP.NET 대화 상자의 스크린샷](troubleshoot/_static/NoNetCore.png)

<span data-ttu-id="d651c-139">이 경고를 표시 하는 경우 환경 변수 `PATH` 컴퓨터에서 모든.NET Core Sdk를 가리키지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-139">This warning appears when the environment variable `PATH` doesn't point to any .NET Core SDKs on the machine.</span></span> <span data-ttu-id="d651c-140">이 문제를 해결 하려면</span><span class="sxs-lookup"><span data-stu-id="d651c-140">To resolve this problem:</span></span>

* <span data-ttu-id="d651c-141">설치 또는.NET Core SDK 설치 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-141">Install or verify the .NET Core SDK is installed.</span></span>
* <span data-ttu-id="d651c-142">확인 된 `PATH` 환경 변수는 SDK가 설치 하는 위치를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-142">Verify that the `PATH` environment variable points to the location in which the SDK is installed.</span></span> <span data-ttu-id="d651c-143">설치 관리자가 일반적으로 설정 된 `PATH`합니다.</span><span class="sxs-lookup"><span data-stu-id="d651c-143">The installer normally sets the `PATH`.</span></span>