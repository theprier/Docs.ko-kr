---
title: ASP.NET Core용 Visual Studio의 개발 시간 IIS 지원
author: shirhatti
description: Windows Server에서 IIS 뒤에서 실행 하는 경우 ASP.NET Core 응용 프로그램 디버깅에 대 한 지원이 검색 합니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 09/13/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/iis/development-time-iis-support
ms.openlocfilehash: 218bb2653b92cd7b1cf2c6726b2d4bedbf307a62
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="development-time-iis-support-in-visual-studio-for-aspnet-core"></a><span data-ttu-id="4c11b-103">ASP.NET Core용 Visual Studio의 개발 시간 IIS 지원</span><span class="sxs-lookup"><span data-stu-id="4c11b-103">Development-time IIS support in Visual Studio for ASP.NET Core</span></span>

<span data-ttu-id="4c11b-104">작성자: [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span><span class="sxs-lookup"><span data-stu-id="4c11b-104">By [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span></span>

<span data-ttu-id="4c11b-105">이 문서에서는 설명 [Visual Studio](https://www.visualstudio.com/vs/) Windows 서버에서 IIS 뒤에서 실행 되는 ASP.NET Core 응용 프로그램 디버깅에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="4c11b-105">This article describes [Visual Studio](https://www.visualstudio.com/vs/) support for debugging ASP.NET Core apps running behind IIS on Windows Server.</span></span> <span data-ttu-id="4c11b-106">이 항목에서는이 기능을 사용 하도록 설정 하 고 프로젝트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c11b-106">This topic walks through enabling this feature and setting up a project.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c11b-107">전제 조건</span><span class="sxs-lookup"><span data-stu-id="4c11b-107">Prerequisites</span></span>

[!INCLUDE [](~/includes/net-core-prereqs-windows.md)]

## <a name="enable-iis"></a><span data-ttu-id="4c11b-108">IIS 활성화</span><span class="sxs-lookup"><span data-stu-id="4c11b-108">Enable IIS</span></span>

<span data-ttu-id="4c11b-109">IIS를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c11b-109">Enable IIS.</span></span> <span data-ttu-id="4c11b-110">**제어판** > **프로그램** > **프로그램 및 기능** > **Windows 기능 Windows 기능 사용/사용 안 함**(화면 왼쪽)으로 차례로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4c11b-110">Navigate to **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off** (left side of the screen).</span></span> <span data-ttu-id="4c11b-111">**인터넷 정보 서비스** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c11b-111">Select the **Internet Information Services** checkbox.</span></span>

![인터넷 정보 서비스가 검은 사각형(확인 표시 아님)으로 표시되어 있고 IIS 기능 중 일부가 활성화되었음을 보여 주는 Windows 기능](development-time-iis-support/_static/enable_iis.png)

<span data-ttu-id="4c11b-113">IIS 설치 시 다시 시작해야 하는 경우 시스템을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4c11b-113">If the IIS installation requires a restart, restart the system.</span></span>

## <a name="enable-development-time-iis-support"></a><span data-ttu-id="4c11b-114">개발 시간 IIS 지원 활성화</span><span class="sxs-lookup"><span data-stu-id="4c11b-114">Enable development-time IIS support</span></span>

<span data-ttu-id="4c11b-115">Visual Studio 설치 관리자를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c11b-115">Launch the Visual Studio installer.</span></span> <span data-ttu-id="4c11b-116">선택 된 **IIS 지원 개발 시간** 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="4c11b-116">Select the **Development time IIS support** component.</span></span> <span data-ttu-id="4c11b-117">구성 요소에 옵션으로 나열 됩니다는 **요약** 패널에 대 한는 **ASP.NET 및 웹 개발** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c11b-117">The component is listed as optional in the **Summary** panel for the **ASP.NET and web development** workload.</span></span> <span data-ttu-id="4c11b-118">이 설치는 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)는 ASP.NET Core 응용 프로그램을 실행 하는 데 필요한 네이티브 IIS 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="4c11b-118">This installs the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module), which is a native IIS module required to run ASP.NET Core apps.</span></span>

![Visual Studio 기능 수정: 워크로드 탭이 선택되어 있습니다.](development-time-iis-support/_static/development_time_support.png)

## <a name="configure-the-project"></a><span data-ttu-id="4c11b-122">프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="4c11b-122">Configure the project</span></span>

<span data-ttu-id="4c11b-123">새 실행 프로필을 만들어 개발 시간 IIS 지원을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4c11b-123">Create a new launch profile to add development-time IIS support.</span></span> <span data-ttu-id="4c11b-124">Visual Studio의 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c11b-124">In Visual Studio's **Solution Explorer**, right-click the project and select **Properties**.</span></span> <span data-ttu-id="4c11b-125">**디버그** 탭을 선택합니다. **실행** 드롭다운에서 **IIS**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4c11b-125">Select the **Debug** tab. Select **IIS** from the **Launch** dropdown.</span></span> <span data-ttu-id="4c11b-126">**브라우저 실행** 기능이 올바른 URL을 사용하여 활성화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4c11b-126">Confirm that the **Launch browser** feature is enabled with the correct URL.</span></span>

![디버그 탭이 선택된 프로젝트 속성 창입니다.](development-time-iis-support/_static/project_properties.png)

<span data-ttu-id="4c11b-131">또는 실행 프로필을 수동으로 추가할는 [launchSettings.json](http://json.schemastore.org/launchsettings) 앱에서 파일:</span><span class="sxs-lookup"><span data-stu-id="4c11b-131">Alternatively, manually add a launch profile to the [launchSettings.json](http://json.schemastore.org/launchsettings) file in the app:</span></span>

```json
{
    "iisSettings": {
        "windowsAuthentication": false,
        "anonymousAuthentication": true,
        "iis": {
            "applicationUrl": "http://localhost/WebApplication2",
            "sslPort": 0
        }
    },
    "profiles": {
        "IIS": {
            "commandName": "IIS",
            "launchBrowser": "true",
            "launchUrl": "http://localhost/WebApplication2",
            "environmentVariables": {
                "ASPNETCORE_ENVIRONMENT": "Development"
            }
        }
    }
}
```

<span data-ttu-id="4c11b-132">관리자 권한으로 실행 되 고 있지 visual Studio를 다시 시작을 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c11b-132">Visual Studio may prompt a restart if not running as an administrator.</span></span> <span data-ttu-id="4c11b-133">메시지가 표시되면 Visual Studio를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4c11b-133">If prompted, restart Visual Studio.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4c11b-134">추가 자료</span><span class="sxs-lookup"><span data-stu-id="4c11b-134">Additional resources</span></span>

* [<span data-ttu-id="4c11b-135">IIS가 있는 Windows에서 ASP.NET Core 호스팅</span><span class="sxs-lookup"><span data-stu-id="4c11b-135">Host ASP.NET Core on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="4c11b-136">ASP.NET Core 모듈 소개</span><span class="sxs-lookup"><span data-stu-id="4c11b-136">Introduction to ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)
* [<span data-ttu-id="4c11b-137">ASP.NET Core 모듈 구성 참조</span><span class="sxs-lookup"><span data-stu-id="4c11b-137">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
