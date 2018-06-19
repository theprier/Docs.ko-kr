---
uid: signalr/overview/deployment/using-signalr-with-azure-web-sites
title: SignalR을 사용 하 여 Azure 앱 서비스에서 웹 앱과 | Microsoft Docs
author: pfletcher
description: 이 문서에서는 Microsoft Azure에서 실행 되는 SignalR 응용 프로그램을 구성 하는 방법에 설명 합니다. Visual Studio 2013 또는 Vis.는 자습서에 사용 된 소프트웨어 버전입니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/01/2015
ms.topic: article
ms.assetid: 2a7517a0-b88c-4162-ade3-9bf6ca7062fd
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/deployment/using-signalr-with-azure-web-sites
msc.type: authoredcontent
ms.openlocfilehash: 8386441690a3fb479ffb941ebd7c0b2f83870781
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
ms.locfileid: "28043209"
---
<a name="using-signalr-with-web-apps-in-azure-app-service"></a>Azure 앱 서비스에서 웹 앱과 SignalR을 사용 하 여
====================
으로 [Patrick Fletcher](https://github.com/pfletcher)

> 이 문서에서는 Microsoft Azure에서 실행 되는 SignalR 응용 프로그램을 구성 하는 방법에 설명 합니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads) 또는 Visual Studio 2012
> - .NET 4.5
> - SignalR 버전 2
> - Visual Studio 2013 또는 2012에 대 한 azure SDK 2.3
>   
> 
> 
> ## <a name="questions-and-comments"></a>질문이 나 의견이
> 
> 이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요. 자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR), [StackOverflow.com](http://stackoverflow.com/), 또는 [Microsoft Azure 포럼](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform).


## <a name="table-of-contents"></a>목차

- [소개](#introduction)
- [Azure 앱 서비스에는 SignalR 웹 응용 프로그램 배포](#deploying)
- [Azure 앱 서비스에서 Websocket을 사용 하도록 설정](#websocket)
- [Azure Redis 캐시 백플레인으로 사용 하 여](#backplane)
- [다음 단계](#nextsteps)

<a id="introduction"></a>
## <a name="introduction"></a>소개

ASP.NET SignalR 새로운 수준의 서버와 웹 또는.NET 클라이언트 간의 상호 작용 기능을 사용할 수 있습니다. Azure에서 호스트 되는 경우 SignalR 응용 프로그램 수 및 혜택을 받을 항상 사용 가능한 확장 가능 제공 클라우드에서 실행 하는 고성능 환경입니다.

<a id="deploying"></a>
## <a name="deploying-a-signalr-web-app-to-azure-app-service"></a>Azure 앱 서비스에는 SignalR 웹 응용 프로그램 배포

SignalR로 온-프레미스 서버에 배포와 응용 프로그램을 Azure에 배포에 특정 복잡 한 문제를 추가 되지 않습니다. SignalR을 사용 하는 응용 프로그램 구성 또는 기타 설정에는 별다른 변경 없이 Azure에서 호스팅할 수 있습니다 (그러나 Websocket 지원, 참조 [Azure 앱 서비스에서 Websocket을 사용 하도록 설정](#websocket) 아래.) 이 자습서에서 만든 응용 프로그램을 배포 합니다는 [초보자를 위한 자습서](../getting-started/tutorial-getting-started-with-signalr.md) Azure에 있습니다.

**필수 구성 요소**

- Visual Studio 2013. Visual Studio가 없는 Visual Studio 2013 Express for Web의 Azure SDK 설치에 포함 됩니다.
- [Visual Studio 2013 용 azure SDK 2.3](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) 또는 [Visual Studio 2012 용 Azure SDK 2.3](https://go.microsoft.com/fwlink/p/?linkid=323511)합니다.
- 이 자습서를 완료 하려면 Azure 구독이 필요 합니다. 있습니다 수 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), 또는 [평가판 구독에 등록](https://azure.microsoft.com/pricing/free-trial/)합니다.

### <a name="deploying-a-signalr-web-app-to-azure"></a>SignalR 웹 응용 프로그램을 Azure에 배포

1. 완료 된 [초보자를 위한 자습서](../getting-started/tutorial-getting-started-with-signalr.md)에서 완료 된 프로젝트를 다운로드 하거나 [코드 갤러리](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)합니다.
2. Visual Studio에서 선택 **빌드**, **SignalR 채팅 게시**합니다.
3. "웹 게시" 대화 상자에서 "Windows Azure 웹 사이트"를 선택 합니다.

    ![Azure 웹 사이트를 선택 합니다.](using-signalr-with-azure-web-sites/_static/image1.png)
4. Microsoft 계정에 서명 하지 않은 경우 클릭 **로그인...**  "기존 웹 사이트 선택" 대화 상자에 로그인 합니다.

    ![기존 웹 사이트를 선택 합니다.](using-signalr-with-azure-web-sites/_static/image2.png)    ![Azure에 로그인](using-signalr-with-azure-web-sites/_static/image3.png)
5. "기존 웹 사이트 선택" 대화 상자에서 **새로**합니다.

    ![새 웹 사이트](using-signalr-with-azure-web-sites/_static/image4.png)
6. "Windows Azure에서 사이트 만들기" 대화 상자에서 고유한 응용 프로그램 이름을 입력 합니다. 지역 드롭다운에 가장 가까운 지역을 선택 합니다. **만들기**를 클릭합니다.

    ![Azure에서 사이트를 만듭니다.](using-signalr-with-azure-web-sites/_static/image5.png)
7. "웹 게시" 대화 상자에서 **게시**합니다.

    ![사이트 게시](using-signalr-with-azure-web-sites/_static/image6.png)
8. 응용 프로그램 게시 완료 되 면 Azure 앱 서비스 웹 응용 프로그램에서 호스팅되는 SignalR 채팅 응용 프로그램이 브라우저에서 열립니다.

    ![브라우저에서 사이트](using-signalr-with-azure-web-sites/_static/image7.png)

<a id="websocket"></a>
### <a name="enabling-websockets-on-azure-app-service-web-apps"></a>Azure 앱 서비스 웹 앱에서 Websocket을 사용 하도록 설정

Websocket를; SignalR 응용 프로그램에서 사용할 웹 응용 프로그램에서 명시적으로 사용 해야 합니다. 그렇지 않으면 다른 프로토콜 사용 됩니다 (참조 [전송 및 대체](../getting-started/introduction-to-signalr.md#transports) 세부 정보에 대 한).

Azure 앱 서비스 웹 앱에서 Websocket을 사용 하려면 웹 응용 프로그램의 구성 섹션에 사용 하도록 설정 합니다. 이 수행 하려면에 웹 앱을 열고는 [Azure 관리 포털](https://manage.windowsazure.com/), 구성을 선택 합니다.

![구성 탭](using-signalr-with-azure-web-sites/_static/image8.png)

구성 페이지 맨 위에 있는.NET 4.5를 웹 앱에 대 한 사용을 확인 합니다.

![.NET framework 버전 4.5 설정](using-signalr-with-azure-web-sites/_static/image9.png)

구성 페이지에 **Websocket** 선택 설정을 **에**합니다.

![Websocket 설정을:에서](using-signalr-with-azure-web-sites/_static/image10.png)

구성 페이지의 맨 아래에 선택 **저장** 변경 내용을 저장 합니다.

![설정 저장](using-signalr-with-azure-web-sites/_static/image11.png)

<a id="backplane"></a>
## <a name="using-the-azure-redis-cache-backplane"></a>Azure Redis 캐시 백플레인으로 사용 하 여

웹 앱에 대 한 여러 인스턴스를 사용 하 고 이러한 인스턴스는 사용자 (즉, 예를 들어, 채팅 메시지를 생성 한 인스턴스에서 다른 인스턴스에 연결 된 사용자를 연결할 수) 서로 상호 작용 하는 데 필요한, [Azure Redis 캐시 백플레인](../performance/scaleout-with-redis.md) 응용 프로그램에 구현 되어야 합니다.

<a id="nextsteps"></a>
## <a name="next-steps"></a>다음 단계

Azure 앱 서비스에서 웹 앱에 대 한 자세한 내용은 참조 하십시오. [웹 응용 프로그램 개요](https://azure.microsoft.com/documentation/articles/app-service-web-overview/)합니다.
