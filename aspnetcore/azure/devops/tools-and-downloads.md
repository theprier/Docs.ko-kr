---
title: ASP.NET Core 및 Azure를 사용 하 여 DevOps | 도구 및 다운로드
author: CamSoper
description: Azure에서 호스팅되는 ASP.NET Core 앱에 대한 DevOps 파이프라인을 빌드하는 방법에 대한 종단 간 지침을 제공하는 가이드입니다.
ms.author: casoper
ms.date: 08/07/2018
uid: azure/devops/tools-and-downloads
ms.openlocfilehash: 5529068b83db475315784571fbf4151d7ecd0d5d
ms.sourcegitcommit: 57eccdea7d89a62989272f71aad655465f1c600a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44340162"
---
# <a name="tools-and-downloads"></a><span data-ttu-id="095a1-103">도구 및 다운로드</span><span class="sxs-lookup"><span data-stu-id="095a1-103">Tools and downloads</span></span>

<span data-ttu-id="095a1-104">Azure에 프로 비전 및와 같은 리소스를 관리 하기 위한 몇 가지 인터페이스를 [Azure portal](https://portal.azure.com)를 [Azure CLI](https://docs.microsoft.com/cli/azure/)를 [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview), [Azure 클라우드 셸](https://shell.azure.com/bash), 및 Visual Studio입니다.</span><span class="sxs-lookup"><span data-stu-id="095a1-104">Azure has several interfaces for provisioning and managing resources, such as the [Azure portal](https://portal.azure.com), [Azure CLI](https://docs.microsoft.com/cli/azure/), [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview), [Azure Cloud Shell](https://shell.azure.com/bash), and Visual Studio.</span></span> <span data-ttu-id="095a1-105">이 가이드는 최소 방식을 사용 하 고는 데 필요한 단계를 줄이기 위해 가능 하면 Azure Cloud Shell를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="095a1-105">This guide takes a minimalist approach and uses the Azure Cloud Shell whenever possible to reduce the steps required.</span></span> <span data-ttu-id="095a1-106">그러나 일부에 대 한 Azure portal은 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="095a1-106">However, the Azure portal must be used for some portions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="095a1-107">전제 조건</span><span class="sxs-lookup"><span data-stu-id="095a1-107">Prerequisites</span></span>

<span data-ttu-id="095a1-108">다음 구독이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="095a1-108">The following subscriptions are required:</span></span>

* <span data-ttu-id="095a1-109">Azure &mdash; 계정이 없다면 [무료 평가판 받기](https://azure.microsoft.com/free/)합니다.</span><span class="sxs-lookup"><span data-stu-id="095a1-109">Azure &mdash; If you don't have an account, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="095a1-110">Azure DevOps 서비스 &mdash; Azure DevOps 구독 및 조직 4 장의 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="095a1-110">Azure DevOps Services &mdash; your Azure DevOps subscription and organization is created in Chapter 4.</span></span>
* <span data-ttu-id="095a1-111">GitHub &mdash; 계정이 없다면 [무료로 등록](https://github.com/join)합니다.</span><span class="sxs-lookup"><span data-stu-id="095a1-111">GitHub &mdash; If you don't have an account, [sign up for free](https://github.com/join).</span></span>

<span data-ttu-id="095a1-112">다음 도구가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="095a1-112">The following tools are required:</span></span>

* <span data-ttu-id="095a1-113">[Git](https://git-scm.com/downloads) &mdash; Git에 대 한 기본적인 이해는이 가이드에 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="095a1-113">[Git](https://git-scm.com/downloads) &mdash; A fundamental understanding of Git is recommended for this guide.</span></span> <span data-ttu-id="095a1-114">검토 합니다 [Git 설명서](https://git-scm.com/doc), 특히 [git 원격](https://git-scm.com/docs/git-remote) 하 고 [git 푸시](https://git-scm.com/docs/git-push)합니다.</span><span class="sxs-lookup"><span data-stu-id="095a1-114">Review the [Git documentation](https://git-scm.com/doc), specifically [git remote](https://git-scm.com/docs/git-remote) and [git push](https://git-scm.com/docs/git-push).</span></span>
* <span data-ttu-id="095a1-115">[.NET core SDK](https://www.microsoft.com/net/download/) &mdash; 2.1.300 버전을 빌드하고 샘플 앱을 실행 하려면 나중에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="095a1-115">[.NET Core SDK](https://www.microsoft.com/net/download/) &mdash; Version 2.1.300 or later is required to build and run the sample app.</span></span> <span data-ttu-id="095a1-116">Visual Studio가 설치 된 경우는 **.NET Core 플랫폼 간 개발** 워크 로드를.NET Core SDK가 이미 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="095a1-116">If Visual Studio is installed with the **.NET Core cross-platform development** workload, the .NET Core SDK is already installed.</span></span>

    <span data-ttu-id="095a1-117">.NET Core SDK 설치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="095a1-117">Verify your .NET Core SDK installation.</span></span> <span data-ttu-id="095a1-118">명령 셸을 열고 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="095a1-118">Open a command shell, and run the following command:</span></span>

    ```console
    dotnet --version
    ```

## <a name="recommended-tools-windows-only"></a><span data-ttu-id="095a1-119">권장된 도구 (Windows만 해당)</span><span class="sxs-lookup"><span data-stu-id="095a1-119">Recommended tools (Windows only)</span></span>

* <span data-ttu-id="095a1-120">[Visual Studio](https://www.visualstudio.com/)의 강력한 Azure 도구 GUI에 대 한 제공 대부분의 기능에이 가이드에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="095a1-120">[Visual Studio](https://www.visualstudio.com/)'s robust Azure tools provide a GUI for most of the functionality described in this guide.</span></span> <span data-ttu-id="095a1-121">무료 Visual Studio Community Edition을 비롯 한 모든 버전의 Visual Studio 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="095a1-121">Any edition of Visual Studio will work, including the free Visual Studio Community Edition.</span></span> <span data-ttu-id="095a1-122">자습서를 사용 하 여와 Visual Studio 없이 개발, 배포 및 DevOps를 보여 주기 위해 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="095a1-122">The tutorials are written to demonstrate development, deployment, and DevOps both with and without Visual Studio.</span></span>

  <span data-ttu-id="095a1-123">Visual Studio에는 다음이 있는지 확인 [워크 로드](https://docs.microsoft.com/visualstudio/install/modify-visual-studio) 설치:</span><span class="sxs-lookup"><span data-stu-id="095a1-123">Confirm that Visual Studio has the following [workloads](https://docs.microsoft.com/visualstudio/install/modify-visual-studio) installed:</span></span>

  * <span data-ttu-id="095a1-124">ASP.NET 및 웹 개발</span><span class="sxs-lookup"><span data-stu-id="095a1-124">ASP.NET and web development</span></span>
  * <span data-ttu-id="095a1-125">Azure 개발</span><span class="sxs-lookup"><span data-stu-id="095a1-125">Azure development</span></span>
  * <span data-ttu-id="095a1-126">.NET Core 플랫폼 간 개발</span><span class="sxs-lookup"><span data-stu-id="095a1-126">.NET Core cross-platform development</span></span>
