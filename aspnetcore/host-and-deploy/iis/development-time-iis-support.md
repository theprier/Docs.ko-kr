---
title: "ASP.NET Core용 Visual Studio의 개발 시간 IIS 지원"
author: shirhatti
description: "Windows Server에서 IIS 배후에서 실행 중인 경우 ASP.NET Core 응용 프로그램 디버깅에 대한 지원을 확인해 보세요."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 09/13/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/iis/development-time-iis-support
ms.openlocfilehash: a5f727dd21ac0c6702691df2215c42f4adc0ec27
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="development-time-iis-support-in-visual-studio-for-aspnet-core"></a>ASP.NET Core용 Visual Studio의 개발 시간 IIS 지원

작성자: [Sourabh Shirhatti](https://twitter.com/sshirhatti)

이 문서에서는 Windows Server에서 IIS 배후에서 실행 중인 ASP.NET Core 응용 프로그램 디버깅에 대한 [Visual Studio](https://www.visualstudio.com/vs/) 지원을 설명합니다. 이 항목에서는이 기능을 사용 하도록 설정 하 고 프로젝트를 설정 합니다.

## <a name="prerequisites"></a>필수 구성 요소

* Visual Studio(2017/버전 15.3 이상)
* ASP.NET 및 웹 개발 워크로드 *또는* .NET Core 플랫폼 간 개발 워크로드

## <a name="enable-iis"></a>IIS 활성화

IIS를 사용 하도록 설정 합니다. **제어판** > **프로그램** > **프로그램 및 기능** > **Windows 기능 Windows 기능 사용/사용 안 함**(화면 왼쪽)으로 차례로 이동합니다. **인터넷 정보 서비스** 확인란을 선택합니다.

![인터넷 정보 서비스가 검은 사각형(확인 표시 아님)으로 표시되어 있고 IIS 기능 중 일부가 활성화되었음을 보여 주는 Windows 기능](development-time-iis-support/_static/enable_iis.png)

IIS 설치를 다시 부팅 해야, 시스템을 재부팅 합니다.

## <a name="enable-development-time-iis-support"></a>개발 시간 IIS 지원 활성화

IIS가 설치 되 면 기존 Visual Studio 설치를 수정 하려면 Visual Studio 설치 관리자를 시작 합니다. 설치 관리자에서 **개발 시간 IIS 지원** 구성 요소를 선택합니다. 이 구성 요소는 **ASP.NET 및 웹 개발** 워크로드에 대한 **요약** 패널에 선택적 구성 요소로 나열됩니다. 그러면 ASP.NET Core 애플리케이션을 실행하는 데 필요한 네이티브 IIS 모듈인 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)이 설치됩니다.

![Visual Studio 기능 수정: 워크로드 탭이 선택되어 있습니다. 웹 및 클라우드 섹션에는 ASP.NET 및 웹 개발 패널이 선택되어 있습니다. 요약 패널의 선택적 영역의 오른쪽에 IIS를 지 원하는 개발 시간 확인란은 있습니다.](development-time-iis-support/_static/development_time_support.png)

## <a name="configure-the-project"></a>프로젝트 구성

새 실행 프로필을 만들어 개발 시간 IIS 지원을 추가합니다. Visual Studio의 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다. **디버그** 탭을 선택합니다. **실행** 드롭다운에서 **IIS**를 선택합니다. **브라우저 실행** 기능이 올바른 URL을 사용하여 활성화되었는지 확인합니다.

![디버그 탭이 선택된 프로젝트 속성 창입니다. 프로필 및 실행 설정은 IIS로 설정되어 있습니다. 브라우저 실행 기능은 http://localhost/WebApplication2의 주소를 사용하여 활성화되었습니다. 익명 인증 사용이 활성화된 웹 서버 설정 영역의 앱 URL 필드에도 동일한 주소가 제공됩니다.](development-time-iis-support/_static/project_properties.png)

또는 실행 프로필을 수동으로 추가할는 [launchSettings.json](http://json.schemastore.org/launchsettings) 앱에서 파일:

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

관리자 권한으로 실행 되 고 있지 visual Studio를 다시 시작을 경우도 있습니다. 메시지가 표시되면 Visual Studio를 다시 시작합니다.

지금까지 이 시점에서 개발 시 IIS 지원에 대 한 프로젝트 구성 됩니다. 

## <a name="additional-resources"></a>추가 리소스

* [IIS가 있는 Windows에서 ASP.NET Core 호스팅](xref:host-and-deploy/iis/index)
* [ASP.NET Core 모듈 소개](xref:fundamentals/servers/aspnet-core-module)
* [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)
