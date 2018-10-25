---
title: ASP.NET Core 모듈
author: rick-anderson
description: ASP.NET Core 모듈이 Kestrel 웹 서버에서 역방향 프록시 서버로 IIS 또는 IIS Express를 어떻게 사용하도록 허용하는지 알아봅니다.
ms.author: tdykstra
ms.custom: mvc
ms.date: 09/21/2018
uid: fundamentals/servers/aspnet-core-module
ms.openlocfilehash: 2f73a34b7d311c9e98ad2ecba11894d27bb2aa4d
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48910891"
---
# <a name="aspnet-core-module"></a>ASP.NET Core 모듈

작성자: [Tom Dykstra](https://github.com/tdykstra), [Rick Strahl](https://github.com/RickStrahl) 및 [Chris Ross](https://github.com/Tratcher)

::: moniker range=">= aspnetcore-2.2"

ASP.NET Core 모듈을 사용하면 ASP.NET Core 앱을 IIS 작업자 프로세스에서(*In-Process*) 또는 역방향 프록시 구성의 IIS 뒤에서(*Out-of-Process*) 실행할 수 있습니다. IIS는 고급 웹앱 보안 및 관리 효율성 기능을 제공합니다.

::: moniker-end

::: moniker range="< aspnetcore-2.2"

ASP.NET Core 모듈은 역방향 프록시 구성에서 ASP.NET Core 앱을 IIS 뒤에서 실행할 수 있습니다. IIS는 고급 웹앱 보안 및 관리 효율성 기능을 제공합니다.

::: moniker-end

지원되는 Windows 버전:

* Windows 7 이상
* Windows Server 2008 R2 이상

::: moniker range=">= aspnetcore-2.2"

In-Process로 호스트하는 경우 모듈에는 자체 서버 구현인 `IISHttpServer`가 있습니다.

Out-of-Process로 호스트하는 경우 모듈은 Kestrel에서만 작동합니다. 이 모듈은 [HTTP.sys](xref:fundamentals/servers/httpsys)(이전 명칭 [WebListener](xref:fundamentals/servers/weblistener))와 호환되지 않습니다.

::: moniker-end

::: moniker range="< aspnetcore-2.2"

모듈은 Kestrel에서만 작동합니다. 이 모듈은 [HTTP.sys](xref:fundamentals/servers/httpsys)(이전 명칭 [WebListener](xref:fundamentals/servers/weblistener))와 호환되지 않습니다.

::: moniker-end

## <a name="aspnet-core-module-description"></a>ASP.NET Core 모듈 설명

::: moniker range=">= aspnetcore-2.2"

ASP.NET Core 모듈은 다음을 위해 IIS 파이프라인에 연결되는 네이티브 IIS 모듈입니다.

* IIS 작업자 프로세스(`w3wp.exe`) 내부에 ASP.NET Core 앱을 호스트하며 [In-Process 호스팅 모델](#in-process-hosting-model)이라고 합니다.

* [Kestrel 서버](xref:fundamentals/servers/kestrel)를 실행하는 백 엔드 ASP.NET Core 앱으로 웹 요청을 전달하며 [Out-of-Process 호스팅 모델](#out-of-process-hosting-model)이라고 합니다.

### <a name="in-process-hosting-model"></a>In-Process 호스팅 모델

In-Process 호스팅을 사용하면 ASP.NET Core 앱은 IIS 작업자 프로세스와 동일한 프로세스에서 실행됩니다. 이 경우 Out-of-Process 호스팅 모델을 사용할 때 나타나는 루프백 어댑터로 인한 프록시 요청 성능 저하 문제가 해결됩니다. IIS는 [Windows Process Activation Service(WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was)를 사용하여 프로세스 관리를 처리합니다.

ASP.NET Core 모듈:

* 앱 초기화를 수행합니다.
  * [CoreCLR](/dotnet/standard/glossary#coreclr)을 로드합니다.
  * `Program.Main`.
* IIS 네이티브 요청의 수명을 처리합니다.

다음 다이어그램은 IIS, ASP.NET Core 모듈 및 In-Process에 호스트된 앱 간의 관계를 보여 줍니다.

![ASP.NET Core 모듈](aspnet-core-module/_static/ancm-inprocess.png)

요청은 웹에서 커널 모드 HTTP.sys 드라이버로 도착합니다. 드라이버는 웹 사이트의 구성된 포트[일반적으로 80(HTTP) 또는 443(HTTPS)]에서 IIS로 네이티브 요청을 라우팅합니다. 이 모듈은 네이티브 요청을 수신하고 제어를 `IISHttpServer`로 전달합니다. 그러면 이 서버는 요청을 네이티브에서 관리 상태로 변환합니다.

`IISHttpServer`가 요청을 선택하면 해당 요청이 ASP.NET Core 미들웨어 파이프라인에 푸시됩니다. 미들웨어 파이프라인은 요청을 처리하고 앱의 논리에 `HttpContext` 인스턴스로 전달합니다. 앱의 응답은 IIS로 다시 전달되고, 요청을 시작한 HTTP 클라이언트에 다시 푸시됩니다.

### <a name="out-of-process-hosting-model"></a>Out-of-Process 호스팅 모델

ASP.NET Core 앱은 IIS 작업자 프로세스와 별도의 프로세스에서 실행되므로 이 모듈은 프로세스 관리를 수행합니다. 이 모듈은 첫 번째 요청이 들어올 때 ASP.NET Core 앱용 프로세스를 시작하고 종료되거나 충돌이 발생하면 앱을 다시 시작합니다. 이는 [Windows Process Activation Service(WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was)로 관리되는 In-Process로 실행되는 앱에서 볼 수 있는 동작과 기본적으로 동일합니다.

다음 다이어그램은 IIS, ASP.NET Core 모듈 및 Out-of-Process에 호스트된 앱 간의 관계를 보여 줍니다.

![ASP.NET Core 모듈](aspnet-core-module/_static/ancm-outofprocess.png)

요청은 웹에서 커널 모드 HTTP.sys 드라이버로 도착합니다. 드라이버는 웹 사이트의 구성된 포트(일반적으로 80(HTTP) 또는 443(HTTPS))에서 IIS로 요청을 라우팅합니다. 모듈은 포트 80/443이 아닌 앱의 임의의 포트에서 Kestrel로 요청을 전달합니다.

모듈은 시작 시 환경 변수를 통해 포트를 지정하고 IIS 통합 미들웨어는 `http://localhost:{port}`에서 수신 대기하도록 서버를 구성합니다. 추가 검사가 수행되고 모듈에서 시작되지 않은 요청은 거부됩니다. 모듈은 HTTPS 전달을 지원하지 않으므로 HTTPS를 통해 IIS에서 수신된 경우에도 HTTP를 통해 요청이 전달됩니다.

Kestrel이 모듈에서 요청을 선택한 후, 요청은 ASP.NET Core 미들웨어 파이프라인으로 푸시됩니다. 미들웨어 파이프라인은 요청을 처리하고 앱의 논리에 `HttpContext` 인스턴스로 전달합니다. IIS 통합에 의해 추가된 미들웨어는 체계, 원격 IP 및 경로 기준을 Kestrel에 요청을 전달하기 위한 계정으로 업데이트합니다. 앱의 응답은 IIS로 다시 전달되고, 요청을 시작한 HTTP 클라이언트에 다시 푸시됩니다.

::: moniker-end

::: moniker range="< aspnetcore-2.2"

ASP.NET Core 모듈은 백 엔드 ASP.NET Core 앱으로 웹 요청을 전달하는 IIS 파이프라인에 연결되는 네이티브 IIS 모듈입니다.

ASP.NET Core 앱은 IIS 작업자 프로세스와 별도의 프로세스에서 실행되므로 이 모듈은 프로세스 관리도 수행합니다. 이 모듈은 첫 번째 요청이 들어올 때 ASP.NET Core 앱용 프로세스를 시작하고 충돌이 발생하면 앱을 다시 시작합니다. 이는 [Windows Process Activation Service(WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was)로 관리되는 IIS에서 In-Process로 실행되는 ASP.NET 4.x 앱에서 볼 수 있는 동작과 기본적으로 동일합니다.

다음 다이어그램은 IIS, ASP.NET Core 모듈 및 앱 간의 관계를 보여 줍니다.

![ASP.NET Core 모듈](aspnet-core-module/_static/ancm-outofprocess.png)

요청은 웹에서 커널 모드 HTTP.sys 드라이버로 도착합니다. 드라이버는 웹 사이트의 구성된 포트(일반적으로 80(HTTP) 또는 443(HTTPS))에서 IIS로 요청을 라우팅합니다. 모듈은 포트 80/443이 아닌 앱의 임의의 포트에서 Kestrel로 요청을 전달합니다.

모듈은 시작 시 환경 변수를 통해 포트를 지정하고 IIS 통합 미들웨어는 `http://localhost:{port}`에서 수신 대기하도록 서버를 구성합니다. 추가 검사가 수행되고 모듈에서 시작되지 않은 요청은 거부됩니다. 모듈은 HTTPS 전달을 지원하지 않으므로 HTTPS를 통해 IIS에서 수신된 경우에도 HTTP를 통해 요청이 전달됩니다.

Kestrel이 모듈에서 요청을 선택한 후, 요청은 ASP.NET Core 미들웨어 파이프라인으로 푸시됩니다. 미들웨어 파이프라인은 요청을 처리하고 앱의 논리에 `HttpContext` 인스턴스로 전달합니다. IIS 통합에 의해 추가된 미들웨어는 체계, 원격 IP 및 경로 기준을 Kestrel에 요청을 전달하기 위한 계정으로 업데이트합니다. 앱의 응답은 IIS로 다시 전달되고, 요청을 시작한 HTTP 클라이언트에 다시 푸시됩니다.

::: moniker-end

Windows 인증 등의 많은 네이티브 모듈이 활성 상태로 유지됩니다. 모듈을 사용하여 활성화된 IIS 모듈에 대해 자세히 알아보려면 <xref:host-and-deploy/iis/modules>을 참조하세요.

ASP.NET Core 모듈에는 몇 가지 기타 함수가 있습니다. 모듈은 다음을 수행할 수 있습니다.

* 작업자 프로세스의 환경 변수를 설정합니다.
* 시작 문제를 해결하기 위해 stdout 출력을 파일 저장소에 기록합니다.
* Windows 인증 토큰을 전달합니다.

## <a name="how-to-install-and-use-the-aspnet-core-module"></a>ASP.NET Core 모듈을 설치하고 사용하는 방법

ASP.NET Core 모듈을 설치하고 사용하는 방법에 대한 자세한 지침은 <xref:host-and-deploy/iis/index>를 참조하세요. 모듈 구성에 대한 내용은 <xref:host-and-deploy/aspnet-core-module>을 참조하세요.

## <a name="additional-resources"></a>추가 자료

* <xref:host-and-deploy/iis/index>
* <xref:host-and-deploy/aspnet-core-module>
* [ASP.NET Core 모듈 GitHub 리포지토리(소스 코드)](https://github.com/aspnet/AspNetCoreModule)
* <xref:host-and-deploy/iis/modules>
