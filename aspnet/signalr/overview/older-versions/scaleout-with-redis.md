---
uid: signalr/overview/older-versions/scaleout-with-redis
title: Redis로 SignalR 규모 확장 (SignalR 1.x) | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 05/01/2013
ms.assetid: 6abecf80-8ffa-41ba-b0d9-1d9edbe7687b
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 1aa391aadfada85f90fe37a70a983b2efa3fbb62
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37833114"
---
<a name="signalr-scaleout-with-redis-signalr-1x"></a>Redis로 SignalR 규모 확장 (SignalR 1.x)
====================
하 여 [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)

이 자습서에서는 사용할지 [Redis](http://redis.io/) 에 메시지를 두 개의 별도 IIS 인스턴스에 배포 된 SignalR 응용 프로그램을 분산 합니다.

Redis는 메모리 내 키-값 저장소입니다. 또한 게시/구독 모델을 사용 하 여 메시징 시스템을 지원합니다. SignalR에서 Redis 백플레인에서 pub/sub 기능을 사용 하 여 다른 서버에 메시지를 전달 합니다.

![](scaleout-with-redis/_static/image1.png)

이 자습서에서는 세 명의 서버를 사용 합니다.

- SignalR 응용 프로그램을 배포 하는 데 사용할 Windows를 실행 하는 두 서버.
- 서버를 하나 사용 하 여 Redis를 실행 하는 Linux를 실행 합니다. 이 자습서의 스크린샷에서, Ubuntu 12.04 TLS 사용 했습니다.

사용 하는 세 명의 물리적 서버를 설정 하지 않은 경우에 Hyper-v에서 Vm을 만들 수 있습니다. Azure에서 Vm을 만들어야 하는 방법도 있습니다.

이 자습서에서는 공식 Redis 구현 하지만 이기도 한 [Redis의 Windows 포트](https://github.com/MSOpenTech/redis) MSOpenTech에서. 설치 및 구성 서로 다르지만 고, 그렇지는 단계는 동일 합니다.

> [!NOTE] 
> 
> Redis로 SignalR 규모 확장에서 Redis 클러스터를 지원 하지 않습니다.


## <a name="overview"></a>개요

자세한 자습서를 시작 하기 전에 수행할 작업의 간략 한 개요는 다음과 같습니다.

1. Redis를 설치 하 고 Redis 서버를 시작 합니다.
2. 응용 프로그램에 이러한 NuGet 패키지를 추가 합니다. 

    - [Microsoft.AspNet.SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [Microsoft.AspNet.SignalR.Redis](http://nuget.org/packages/Microsoft.AspNet.SignalR.Redis)
3. SignalR 응용 프로그램을 만듭니다.
4. Global.asax 백플레인에서 구성 하려면 다음 코드를 추가 합니다. 

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a>Hyper-v에서 Ubuntu

Windows Hyper-v를 사용 하 여 Windows Server에서 Ubuntu VM을 쉽게 만들 수 있습니다.

Ubuntu에서 ISO를 다운로드 [ http://www.ubuntu.com ](http://www.ubuntu.com/)합니다.

Hyper-v에서 새 VM을 추가 합니다. 에 **가상 하드 디스크 연결** 선택 단계 **가상 하드 디스크 만들기**합니다.

![](scaleout-with-redis/_static/image2.png)

에 **설치 옵션** 선택 단계 **이미지 파일 (.iso)**, 클릭 **찾아보기**, Ubuntu 설치 ISO 찾습니다.

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a>Redis를 설치 합니다.

단계에 따라 [ http://redis.io/download ](http://redis.io/download) 다운로드 및 Redis를 빌드해야 합니다.

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

Redis 이진이 빌드는 `src` 디렉터리입니다.

기본적으로 Redis는 암호를 필요 하지 않습니다. 암호를 설정 하려면 편집을 `redis.conf` 소스 코드의 루트 디렉터리에 있는 파일입니다. (편집 하기 전에 파일의 백업 복사본을 만듭니다.) 다음 지시문을 추가 `redis.conf`:

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

이제 Redis 서버를 시작 합니다.

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

열린 포트 6379를 Redis는 기본 포트에서 수신 합니다. (구성 파일에서 포트 번호를 변경할 수 있습니다.)

## <a name="create-the-signalr-application"></a>SignalR 응용 프로그램 만들기

이러한 자습서 중 하나를 수행 하 여 SignalR 응용 프로그램을 만듭니다.

- [SignalR 시작](../getting-started/tutorial-getting-started-with-signalr.md)
- [SignalR 및 MVC 4 시작](tutorial-getting-started-with-signalr-and-mvc-4.md)

다음으로 Redis로 규모 확장을 지원 하기 위해 채팅 응용 프로그램을 수정 합니다. 먼저 프로젝트에 SignalR.Redis NuGet 패키지를 추가 합니다. Visual Studio에서에서 합니다 **도구** 메뉴에서 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

다음으로 Global.asax 파일을 엽니다. 다음 코드를 추가 합니다 **응용 프로그램\_시작** 메서드:

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- "server"는 Redis를 실행 하는 서버의 이름입니다.
- *포트* 는 포트 번호
- "password"는 redis.conf 파일에 정의 된 암호가입니다.
- "AppName"는 문자열입니다. SignalR이이 이름을 가진 Redis pub/sub 채널을 만듭니다.

예를 들어:

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a>배포 하 고 응용 프로그램 실행

SignalR 응용 프로그램을 배포 하려면 Windows Server 인스턴스를 준비 합니다.

IIS 역할을 추가 합니다. WebSocket 프로토콜을 포함 하 여 "응용 프로그램 개발" 기능을 포함 합니다.

![](scaleout-with-redis/_static/image5.png)

관리 서비스 ("관리 도구" 아래)를 포함 합니다.

![](scaleout-with-redis/_static/image6.png)

**설치 웹 배포 3.0.** IIS 관리자를 실행 하면, Microsoft 웹 플랫폼을 설치 하 라는 메시지가 나타납니다 것 또는 할 수 있습니다 [다운로드를 intstaller](https://go.microsoft.com/fwlink/?LinkId=255386)합니다. 플랫폼 설치 관리자에서 웹 배포에 대 한 검색 하 고 웹 배포 3.0 설치

![](scaleout-with-redis/_static/image7.png)

Web Management Service가 실행 중인지 확인 합니다. 그렇지 않은 경우 서비스를 시작 합니다. (웹 관리 서비스 Windows 서비스 목록에 보이지 않으면 확인 IIS 역할을 추가 했을 때 Management 서비스를 설치 합니다.)

기본적으로 웹 관리 서비스 8172 TCP 포트에서 수신합니다. Windows 방화벽에서 8172 포트의 TCP 트래픽을 허용 하는 새 인바운드 규칙을 만듭니다. 자세한 내용은 [방화벽 규칙 구성](https://technet.microsoft.com/library/dd448559(WS.10).aspx)합니다. (Azure에서 Vm을 호스트 하는 경우 이렇게 하려면 Azure portal에서 직접. 참조 [Virtual Machine에 끝점을 설정 하는 방법](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)

이제 서버에 개발 컴퓨터에서 Visual Studio 프로젝트를 배포할 준비가 되었습니다. 솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.

자세한 내용을 보려면 웹 배포에 대 한 설명서를 참조 하세요 [Visual Studio 및 ASP.NET 웹 배포 콘텐츠 맵](../../../whitepapers/aspnet-web-deployment-content-map.md)합니다.

두 명의 서버 응용 프로그램을 배포 하는 경우에 별도 브라우저 창에서 각 인스턴스를 엽니다 하 고 다른에서 SignalR 메시지를 받을 각각 볼 수 있습니다. (물론 프로덕션 환경에서 두 서버는 sit 부하 분산 합니다.)

![](scaleout-with-redis/_static/image8.png)

원하는 경우 사용할 수 있습니다, Redis로 전송 되는 메시지를 볼 수는 **redis cli** 클라이언트를 Redis를 사용 하 여 설치 합니다.

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
