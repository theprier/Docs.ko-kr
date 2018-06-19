---
uid: signalr/overview/performance/scaleout-with-redis
title: Redis와 함께 SignalR 확장 | Microsoft Docs
author: MikeWasson
description: 이전 버전의에 대 한 내용은이 항목의 버전 2 이전 버전을 Visual Studio 2013.NET 4.5 SignalR이이 항목에서 사용 하는 소프트웨어 버전 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: 6ecd08c1-e364-4cd7-ad4c-806521911585
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/performance/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 2ef161f35e69ef4a754d2740199166ee48c3fbab
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
ms.locfileid: "28042692"
---
<a name="signalr-scaleout-with-redis"></a>Redis와 함께 SignalR 확장
====================
여 [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)

> ## <a name="software-versions-used-in-this-topic"></a>이 항목에서 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - SignalR 버전 2
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a>이 항목의 이전 버전
> 
> 이전 버전의 SignalR에 대 한 정보를 참조 하십시오. [SignalR 이전 버전](../older-versions/index.md)합니다.
> 
> ## <a name="questions-and-comments"></a>질문이 나 의견이
> 
> 이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요. 자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.


이 자습서를 사용 하 여 [Redis](http://redis.io/) 두 개의 별도 IIS 인스턴스에 배포 하는 SignalR 응용 프로그램 간에 메시지를 분산 합니다.

Redis는 메모리에 키-값 저장소입니다. 또한 게시/구독 모델을 사용 하는 메시징 시스템을 지원합니다. SignalR Redis 백플레인에서 다른 서버로 메시지를 전달 하는 pub/sub 기능을 사용 합니다.

![](scaleout-with-redis/_static/image1.png)

이 자습서에서는 세 명의 서버를 사용 합니다.

- SignalR 응용 프로그램을 배포 하는 데 사용할 수 있는 Windows를 실행 하는 두 개의 서버
- 서버를 하나 사용 하는 Redis를 실행 하는 Linux를 실행 합니다. 이 자습서에서 스크린 샷에 대 한 Ubuntu 12.04 TLS를 사용 했습니다.

사용 하는 세 명의 물리적 서버를 설정 하지 않은 경우에 Hyper-v에서 Vm을 만들 수 있습니다. 두 번째 방법은 Azure에서 Vm을 만들려고 하는 것입니다.

이 자습서에서는 공식 Redis 구현 하지만 이기도 한 [Windows Redis 포트](https://github.com/MSOpenTech/redis) MSOpenTech에서 합니다. 설치 및 구성 하는 다르지만 그렇지 않은 경우 단계는 동일 합니다.

> [!NOTE] 
> 
> SignalR 확장 Redis와 함께 Redis 클러스터를 지원 하지 않습니다.


## <a name="overview"></a>개요

자세한 자습서에 들어가기 전에 수행할 작업의 간략 한 개요는 다음과 같습니다.

1. Redis를 설치 하 고 Redis 서버를 시작 합니다.
2. 응용 프로그램에 이러한 NuGet 패키지를 추가 합니다. 

    - [Microsoft.AspNet.SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [Microsoft.AspNet.SignalR.Redis](http://nuget.org/packages/Microsoft.AspNet.SignalR.Redis)
3. SignalR 응용 프로그램을 만듭니다.
4. 백플레인에서 구성 하려면 Startup.cs에 다음 코드를 추가 합니다. 

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a>Hyper-v의 Ubuntu

Windows Hyper-v를 사용 하 여 Windows Server에서 Ubuntu VM을 쉽게 만들 수 있습니다.

Ubuntu ISO를 다운로드 [http://www.ubuntu.com](http://www.ubuntu.com/)합니다.

Hyper-v, 새 VM을 추가 합니다. 에 **가상 하드 디스크 연결** 단계에서는 **가상 하드 디스크 만들기**합니다.

![](scaleout-with-redis/_static/image2.png)

에 **설치 옵션** 단계에서는 **이미지 파일 (.iso)**, 클릭 **찾아보기**, Ubuntu 설치 ISO 찾습니다.

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a>Redis를 설치 합니다.

단계에 따라 [http://redis.io/download](http://redis.io/download) 다운로드 하 고 Redis를 작성 합니다.

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

Redis 이진 파일에서 빌드이 고 `src` 디렉터리입니다.

기본적으로 Redis에 암호가 필요 하지 않습니다. 암호를 설정 하려면 편집는 `redis.conf` 소스 코드의 루트 디렉터리에 있는 파일입니다. (편집 하기 전에 파일의 백업 복사본을 만듭니다.) 다음 지시문을 추가 `redis.conf`:

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

Redis 서버를 지금 시작 합니다.

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

열린 포트 6379, Redis는 기본 포트에서 수신 합니다. (구성 파일에서 포트 번호를 변경할 수 있습니다.)

## <a name="create-the-signalr-application"></a>SignalR 응용 프로그램 만들기

이러한 자습서 중 하나를 수행 하 여 SignalR 응용 프로그램을 만듭니다.

- [SignalR 2.0 시작](../getting-started/tutorial-getting-started-with-signalr.md)
- [SignalR 2.0 및 MVC 5 시작](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

다음으로, Redis와 함께 확장을 지원 하도록 채팅 응용 프로그램을 수정 합니다. 먼저 프로젝트에 SignalR.Redis NuGet 패키지를 추가 합니다. Visual Studio에서에서 **도구** 메뉴 선택 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

다음으로 Startup.cs 파일을 엽니다. 다음 코드를 추가 하는 **구성** 메서드:

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- "서버"는 Redis를 실행 하는 서버의 이름입니다.
- *포트* 는 포트 번호
- "p"는 redis.conf 파일에 정의 된 암호입니다.
- "응용 프로그램 이름"은 모든 문자열입니다. SignalR이이 이름을 가진 Redis pub/sub 채널을 만듭니다.

예:

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a>배포 및 응용 프로그램 실행

SignalR 응용 프로그램을 배포 하 여 Windows Server 인스턴스를 준비 합니다.

IIS 역할을 추가 합니다. WebSocket 프로토콜을 포함 하 여 "응용 프로그램 개발" 기능을 포함 합니다.

![](scaleout-with-redis/_static/image5.png)

관리 서비스 ("관리 도구" 아래에 나열)도 포함 됩니다.

![](scaleout-with-redis/_static/image6.png)

**설치 웹 배포 3.0.** IIS 관리자를 실행 하면, Microsoft 웹 플랫폼 설치를 묻습니다 또는 할 수 있습니다 때 [는 intstaller 다운로드](https://go.microsoft.com/fwlink/?LinkId=255386)합니다. 플랫폼 설치 관리자에서 웹 배포를 검색 하 고 웹 배포 3.0 설치

![](scaleout-with-redis/_static/image7.png)

웹 관리 서비스에서 실행 되 고 있는지 확인 합니다. 그렇지 않은 경우 서비스를 시작 합니다. (웹 관리 서비스 보이지 않으면의 Windows 서비스 목록에 있는지 확인 IIS 역할을 추가 했을 때 관리 서비스를 설치 합니다.)

웹 관리 서비스는 기본적으로 TCP 8172 포트에서 수신합니다. Windows 방화벽에서 TCP 8172 포트 트래픽을 허용 하는 새 인바운드 규칙을 만듭니다. 자세한 내용은 참조 [방화벽 규칙 구성](https://technet.microsoft.com/library/dd448559(WS.10).aspx)합니다. (Azure에서 Vm을 호스팅하는 경우 이렇게 하려면 Azure 포털에서 직접 합니다. 참조 [가상 컴퓨터에 끝점을 설정 하는 방법을](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)

이제 서버에 개발 컴퓨터에서 Visual Studio 프로젝트를 배포할 준비가 되었습니다. 솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.

웹 배포에 대 한 설명서 보다 자세한 참조 [Visual Studio 및 ASP.NET에 대 한 웹 배포 콘텐츠 맵](../../../whitepapers/aspnet-web-deployment-content-map.md)합니다.

두 명의 서버에 응용 프로그램을 배포 하는 경우 각 인스턴스는 별도 브라우저 창에서 열고 하 고 다른에서 SignalR 메시지를 받을 구성 파일은 각각을 확인할 수 있습니다. (물론, 프로덕션 환경에서 두 서버는 sit 부하 분산 장치 뒤.)

![](scaleout-with-redis/_static/image8.png)

내용은로 보내지는 Redis를 사용할 수 있습니다 메시지를 볼 수는 **redis cli** Redis와 함께 설치 된 클라이언트입니다.

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
