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
uid: testing/troubleshoot
ms.openlocfilehash: a75dc666621600e1e2fe36c29acbe7484bae9229
ms.sourcegitcommit: c79fd3592f444d58e17518914f8873d0a11219c0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="troubleshoot-aspnet-core-projects"></a><span data-ttu-id="93799-103">ASP.NET Core 프로젝트 문제 해결</span><span class="sxs-lookup"><span data-stu-id="93799-103">Troubleshoot ASP.NET Core projects</span></span>

<span data-ttu-id="93799-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="93799-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="93799-105">다음 링크는 문제 해결 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="93799-105">The following links provide troubleshooting guidance:</span></span>

* [<span data-ttu-id="93799-106">Azure App Service에서 ASP.NET Core 문제 해결</span><span class="sxs-lookup"><span data-stu-id="93799-106">Troubleshoot ASP.NET Core on Azure App Service</span></span>](xref:host-and-deploy/azure-apps/troubleshoot)
* [<span data-ttu-id="93799-107">IIS에서 ASP.NET Core 문제 해결</span><span class="sxs-lookup"><span data-stu-id="93799-107">Troubleshoot ASP.NET Core on IIS</span></span>](xref:host-and-deploy/iis/troubleshoot)
* [<span data-ttu-id="93799-108">ASP.NET Core를 사용하는 Azure App Service 및 IIS에 대한 일반적인 오류 참조</span><span class="sxs-lookup"><span data-stu-id="93799-108">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)
* [<span data-ttu-id="93799-109">YouTube: ASP.NET Core 응용 프로그램의 문제를 진단합니다.</span><span class="sxs-lookup"><span data-stu-id="93799-109">YouTube: Diagnosing issues in ASP.NET Core Applications</span></span>](https://www.youtube.com/watch?v=RYI0DHoIVaA)

<a name="sdk"></a>
## <a name="net-core-sdk-warnings"></a><span data-ttu-id="93799-110">.NET core SDK 경고</span><span class="sxs-lookup"><span data-stu-id="93799-110">.NET Core SDK warnings</span></span>

### <a name="both-the-32-and-64-bit-versions-of-the-net-core-sdk-are-installed"></a><span data-ttu-id="93799-111">모두 32와 64 비트 버전의.NET Core SDK가 설치 된</span><span class="sxs-lookup"><span data-stu-id="93799-111">Both the 32 and 64 bit versions of the .NET Core SDK are installed</span></span>
<span data-ttu-id="93799-112">에 **새 프로젝트** 대화 ASP.NET Core 상단에 표시 하는 경우 다음과 같은 경고가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93799-112">In the **New Project** dialog for ASP.NET Core, you may see the following warning appear at the top:</span></span> 

    Both 32 and 64 bit versions of the .NET Core SDK are installed. Only templates from the 64 bit version(s) installed at C:\Program Files\dotnet\sdk\" will be displayed.

![경고 메시지를 보여 주는 OneASP.NET 대화 상자의 스크린 샷](troubleshoot/_static/both32and64bit.png)

<span data-ttu-id="93799-114">이 경고를 표시 하는 경우 (x86) 32 비트 및 64 비트 (x64) 버전의 모두는 [.NET Core SDK](https://www.microsoft.com/net/download/all) 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93799-114">This warning appears when both 32-bit (x86) and 64-bit (x64) versions of the [.NET Core SDK](https://www.microsoft.com/net/download/all) are installed.</span></span> <span data-ttu-id="93799-115">두 버전을 설치 하려면 일반적인 원인은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93799-115">Common reasons both versions can be installed include:</span></span>

* <span data-ttu-id="93799-116">원래 32 비트 컴퓨터를 사용 하는.NET Core SDK 설치 관리자 다운로드 하지만 다음 복사 프로세스를 수행한 후 하는 64 비트 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="93799-116">You originally downloaded the .NET Core SDK installer using a 32-bit machine, but then copied it across and installed it on a 64-bit machine.</span></span> 
* <span data-ttu-id="93799-117">32 비트.NET Core SDK가 다른 응용 프로그램으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93799-117">The 32-bit .NET Core SDK was installed by another application.</span></span>
* <span data-ttu-id="93799-118">잘못 된 버전은 다운로드 되어 설치 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="93799-118">The wrong version was downloaded and installed.</span></span>

<span data-ttu-id="93799-119">이 경고를 방지 하기 위해 32 비트.NET Core SDK를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="93799-119">Uninstall the 32-bit .NET Core SDK to prevent this warning.</span></span> <span data-ttu-id="93799-120">제거 **제어판** > **프로그램 및 기능** > **제거 또는 변경 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="93799-120">Uninstall from **Control Panel** > **Programs and Features** > **Uninstall or change a program**.</span></span> <span data-ttu-id="93799-121">경고의 발생 이유 및 그 의미를 이해 하는 경우 경고를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93799-121">If you understand why the warning occurs and its implications, you can ignore the warning.</span></span>

### <a name="the-net-core-sdk-is-installed-in-multiple-locations"></a><span data-ttu-id="93799-122">.NET Core SDK가 여러 위치에 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93799-122">The .NET Core SDK is installed in multiple locations</span></span>
<span data-ttu-id="93799-123">에 **새 프로젝트** 대화에 대 한 ASP.NET Core 상단에 표시 하는 경우 다음과 같은 경고가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93799-123">In the **New Project** dialog for ASP.NET Core you may see the following warning appear at the top:</span></span> 

 <span data-ttu-id="93799-124">.NET Core SDK는 여러 위치에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93799-124">The .NET Core SDK is installed in multiple locations.</span></span> <span data-ttu-id="93799-125">에 설치 된과에서 템플릿만 ' C:\Program Files\dotnet\sdk\' 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93799-125">Only templates from the SDK(s) installed at 'C:\Program Files\dotnet\sdk\' will be displayed.</span></span>

![경고 메시지를 보여 주는 OneASP.NET 대화 상자의 스크린 샷](troubleshoot/_static/multiplelocations.png)

<span data-ttu-id="93799-127">.NET Core SDK의 하나 이상 설치 디렉터리의 외부에 있으므로이 메시지는 표시 * C:\Program Files\dotnet\sdk\*합니다.</span><span class="sxs-lookup"><span data-stu-id="93799-127">You are seeing this message because you have at least one installation of the .NET Core SDK in a directory outside of *C:\Program Files\dotnet\sdk\*.</span></span> <span data-ttu-id="93799-128">일반적으로.NET Core SDK MSI 설치 프로그램을 대신 복사/붙여넣기를 사용 하는 컴퓨터에 배포 된 경우 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="93799-128">Usually that happens when the .NET Core SDK has been deployed on a machine using copy/paste instead of the MSI installer.</span></span>

<span data-ttu-id="93799-129">이 경고를 방지 하기 위해 32 비트.NET Core SDK를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="93799-129">Uninstall the 32-bit .NET Core SDK to prevent this warning.</span></span> <span data-ttu-id="93799-130">제거 **제어판** > **프로그램 및 기능** > **제거 또는 변경 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="93799-130">Uninstall from **Control Panel** > **Programs and Features** > **Uninstall or change a program**.</span></span> <span data-ttu-id="93799-131">경고의 발생 이유 및 그 의미를 이해 하는 경우 경고를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93799-131">If you understand why the warning occurs and its implications, you can ignore the warning.</span></span>
