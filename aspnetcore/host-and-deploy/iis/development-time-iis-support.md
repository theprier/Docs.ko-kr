---
title: "ASP.NET Core용 Visual Studio의 개발 시간 IIS 지원"
author: shirhatti
description: "Windows Server에서 IIS 뒤에서 실행 하는 경우 ASP.NET Core 응용 프로그램 디버깅에 대 한 지원이 검색 합니다."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 09/13/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/iis/development-time-iis-support
ms.openlocfilehash: a8bdf4c0c0399c62666e6e61e70c0298a42c2c12
ms.sourcegitcommit: 9f758b1550fcae88ab1eb284798a89e6320548a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2018
---
# <a name="development-time-iis-support-in-visual-studio-for-aspnet-core"></a><span data-ttu-id="82efb-103">ASP.NET Core용 Visual Studio의 개발 시간 IIS 지원</span><span class="sxs-lookup"><span data-stu-id="82efb-103">Development-time IIS support in Visual Studio for ASP.NET Core</span></span>

<span data-ttu-id="82efb-104">작성자: [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span><span class="sxs-lookup"><span data-stu-id="82efb-104">By: [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span></span>

<span data-ttu-id="82efb-105">이 문서에서는 설명 [Visual Studio](https://www.visualstudio.com/vs/) Windows 서버에서 IIS 뒤에서 실행 되는 ASP.NET Core 응용 프로그램 디버깅에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="82efb-105">This article describes [Visual Studio](https://www.visualstudio.com/vs/) support for debugging ASP.NET Core apps running behind IIS on Windows Server.</span></span> <span data-ttu-id="82efb-106">이 항목에서는이 기능을 사용 하도록 설정 하 고 프로젝트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="82efb-106">This topic walks through enabling this feature and setting up a project.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82efb-107">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="82efb-107">Prerequisites</span></span>

* <span data-ttu-id="82efb-108">Visual Studio(2017/버전 15.3 이상)</span><span class="sxs-lookup"><span data-stu-id="82efb-108">Visual Studio (2017/version 15.3 or later)</span></span>
* <span data-ttu-id="82efb-109">ASP.NET 및 웹 개발 워크로드 *또는* .NET Core 플랫폼 간 개발 워크로드</span><span class="sxs-lookup"><span data-stu-id="82efb-109">ASP.NET and web development workload *OR* the .NET Core cross-platform development workload</span></span>

## <a name="enable-iis"></a><span data-ttu-id="82efb-110">IIS 활성화</span><span class="sxs-lookup"><span data-stu-id="82efb-110">Enable IIS</span></span>

<span data-ttu-id="82efb-111">IIS를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="82efb-111">Enable IIS.</span></span> <span data-ttu-id="82efb-112">**제어판** > **프로그램** > **프로그램 및 기능** > **Windows 기능 Windows 기능 사용/사용 안 함**(화면 왼쪽)으로 차례로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="82efb-112">Navigate to **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off** (left side of the screen).</span></span> <span data-ttu-id="82efb-113">**인터넷 정보 서비스** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82efb-113">Select the **Internet Information Services** checkbox.</span></span>

![인터넷 정보 서비스가 검은 사각형(확인 표시 아님)으로 표시되어 있고 IIS 기능 중 일부가 활성화되었음을 보여 주는 Windows 기능](development-time-iis-support/_static/enable_iis.png)

<span data-ttu-id="82efb-115">IIS 설치를 다시 시작이 필요한 경우 시스템 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="82efb-115">If the IIS installation requires a restart, restart the system.</span></span>

## <a name="enable-development-time-iis-support"></a><span data-ttu-id="82efb-116">개발 시간 IIS 지원 활성화</span><span class="sxs-lookup"><span data-stu-id="82efb-116">Enable development-time IIS support</span></span>

<span data-ttu-id="82efb-117">Visual Studio 설치 관리자를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="82efb-117">Launch the Visual Studio installer.</span></span> <span data-ttu-id="82efb-118">선택 된 **IIS 지원 개발 시간** 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="82efb-118">Select the **Development time IIS support** component.</span></span> <span data-ttu-id="82efb-119">구성 요소에 옵션으로 나열 됩니다는 **요약** 패널에 대 한는 **ASP.NET 및 웹 개발** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="82efb-119">The component is listed as optional in the **Summary** panel for the **ASP.NET and web development** workload.</span></span> <span data-ttu-id="82efb-120">이 설치는 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)는 ASP.NET Core 응용 프로그램을 실행 하는 데 필요한 네이티브 IIS 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="82efb-120">This installs the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module), which is a native IIS module required to run ASP.NET Core apps.</span></span>

![Visual Studio 기능 수정: 워크로드 탭이 선택되어 있습니다.](development-time-iis-support/_static/development_time_support.png)

## <a name="configure-the-project"></a><span data-ttu-id="82efb-124">프로젝트 구성</span><span class="sxs-lookup"><span data-stu-id="82efb-124">Configure the project</span></span>

<span data-ttu-id="82efb-125">새 실행 프로필을 만들어 개발 시간 IIS 지원을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="82efb-125">Create a new launch profile to add development-time IIS support.</span></span> <span data-ttu-id="82efb-126">Visual Studio의 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82efb-126">In Visual Studio's **Solution Explorer**, right-click the project and select **Properties**.</span></span> <span data-ttu-id="82efb-127">**디버그** 탭을 선택합니다. **실행** 드롭다운에서 **IIS**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82efb-127">Select the **Debug** tab. Select **IIS** from the **Launch** dropdown.</span></span> <span data-ttu-id="82efb-128">**브라우저 실행** 기능이 올바른 URL을 사용하여 활성화되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="82efb-128">Confirm that the **Launch browser** feature is enabled with the correct URL.</span></span>

![디버그 탭이 선택된 프로젝트 속성 창입니다.](development-time-iis-support/_static/project_properties.png)

<span data-ttu-id="82efb-133">또는 실행 프로필을 수동으로 추가할는 [launchSettings.json](http://json.schemastore.org/launchsettings) 앱에서 파일:</span><span class="sxs-lookup"><span data-stu-id="82efb-133">Alternatively, manually add a launch profile to the [launchSettings.json](http://json.schemastore.org/launchsettings) file in the app:</span></span>

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

<span data-ttu-id="82efb-134">관리자 권한으로 실행 되 고 있지 visual Studio를 다시 시작을 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82efb-134">Visual Studio may prompt a restart if not running as an administrator.</span></span> <span data-ttu-id="82efb-135">메시지가 표시되면 Visual Studio를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="82efb-135">If prompted, restart Visual Studio.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="82efb-136">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="82efb-136">Additional resources</span></span>

* [<span data-ttu-id="82efb-137">IIS가 있는 Windows에서 ASP.NET Core 호스팅</span><span class="sxs-lookup"><span data-stu-id="82efb-137">Host ASP.NET Core on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="82efb-138">ASP.NET Core 모듈 소개</span><span class="sxs-lookup"><span data-stu-id="82efb-138">Introduction to ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)
* [<span data-ttu-id="82efb-139">ASP.NET Core 모듈 구성 참조</span><span class="sxs-lookup"><span data-stu-id="82efb-139">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
