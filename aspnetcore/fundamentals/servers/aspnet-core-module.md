---
title: ASP.NET Core 모듈
author: rick-anderson
description: ASP.NET Core 모듈이 Kestrel 웹 서버에서 역방향 프록시 서버로 IIS 또는 IIS Express를 어떻게 사용하도록 허용하는지 알아봅니다.
ms.author: tdykstra
ms.custom: mvc
ms.date: 02/23/2018
uid: fundamentals/servers/aspnet-core-module
ms.openlocfilehash: 319ab80f20f3917dae921f43566e368b51c29f0b
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36272337"
---
# <a name="aspnet-core-module"></a>ASP.NET Core 모듈

작성자: [Tom Dykstra](https://github.com/tdykstra), [Rick Strahl](https://github.com/RickStrahl) 및 [Chris Ross](https://github.com/Tratcher) 

ASP.NET Core 모듈은 역방향 프록시 구성에서 ASP.NET Core 앱을 IIS 뒤에서 실행할 수 있습니다. IIS는 고급 웹앱 보안 및 관리 효율성 기능을 제공합니다.

지원되는 Windows 버전:

* Windows 7 이상
* Windows Server 2008 R2 이상

ASP.NET Core 모듈은 Kestrel에서만 작동합니다. 이 모듈은 [HTTP.sys](xref:fundamentals/servers/httpsys)(이전 명칭 [WebListener](xref:fundamentals/servers/weblistener))와 호환되지 않습니다.

## <a name="aspnet-core-module-description"></a>ASP.NET Core 모듈 설명

ASP.NET Core 모듈은 백 엔드 ASP.NET Core 앱으로 웹 요청을 리디렉션하는 IIS 파이프라인에 연결되는 네이티브 IIS 모듈입니다. Windows 인증 등의 많은 네이티브 모듈이 활성 상태로 유지됩니다. 모듈을 사용하여 활성화된 IIS 모듈에 대해 자세히 알아보려면 [IIS 모듈](xref:host-and-deploy/iis/modules)을 참조하세요.

ASP.NET Core 앱은 IIS 작업자 프로세스와 별도의 프로세스에서 실행되므로 이 모듈은 프로세스 관리도 수행합니다. 이 모듈은 첫 번째 요청이 들어올 때 ASP.NET Core 앱용 프로세스를 시작하고 충돌이 발생하면 앱을 다시 시작합니다. 이는 [Windows Process Activation Service(WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was)로 관리되는 IIS에서 In Process로 실행되는 ASP.NET 4.x 앱에서 볼 수 있는 동작과 기본적으로 동일합니다.

다음 다이어그램은 IIS, ASP.NET Core 모듈 및 ASP.NET Core 앱 간의 관계를 보여 줍니다.

![ASP.NET Core 모듈](aspnet-core-module/_static/ancm.png)

요청은 웹에서 커널 모드 HTTP.sys 드라이버로 도착합니다. 드라이버는 웹 사이트의 구성된 포트(일반적으로 80(HTTP) 또는 443(HTTPS))에서 IIS로 요청을 라우팅합니다. 모듈은 포트 80/443이 아닌 앱의 임의의 포트에서 Kestrel로 요청을 전달합니다.

모듈은 시작 시 환경 변수를 통해 포트를 지정하고 IIS 통합 미들웨어는 `http://localhost:{port}`에서 수신 대기하도록 서버를 구성합니다. 추가 검사가 수행되고 모듈에서 시작되지 않은 요청은 거부됩니다. 모듈은 HTTPS 전달을 지원하지 않으므로 HTTPS를 통해 IIS에서 수신된 경우에도 HTTP를 통해 요청이 전달됩니다.

Kestrel이 모듈에서 요청을 선택한 후, 요청은 ASP.NET Core 미들웨어 파이프라인으로 푸시됩니다. 미들웨어 파이프라인은 요청을 처리하고 앱의 논리에 `HttpContext` 인스턴스로 전달합니다. 앱의 응답은 IIS로 다시 전달되고, 요청을 시작한 HTTP 클라이언트에 다시 푸시됩니다.

ASP.NET Core 모듈에는 몇 가지 기타 함수가 있습니다. 모듈은 다음을 수행할 수 있습니다.

* 작업자 프로세스의 환경 변수를 설정합니다.
* 시작 문제를 해결하기 위해 stdout 출력을 파일 저장소에 기록합니다.
* Windows 인증 토큰을 전달합니다.

## <a name="how-to-install-and-use-the-aspnet-core-module"></a>ASP.NET Core 모듈을 설치하고 사용하는 방법

ASP.NET Core 모듈을 설치하고 사용하는 방법에 대한 자세한 지침은 [IIS가 있는 Windows에서 호스트](xref:host-and-deploy/iis/index)를 참조하세요. 모듈 구성에 대한 자세한 내용은 [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)를 참조하세요.

## <a name="additional-resources"></a>추가 자료

* [IIS를 사용하여 Windows에서 호스트](xref:host-and-deploy/iis/index)
* [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)
* [ASP.NET Core 모듈 GitHub 리포지토리(소스 코드)](https://github.com/aspnet/AspNetCoreModule)
