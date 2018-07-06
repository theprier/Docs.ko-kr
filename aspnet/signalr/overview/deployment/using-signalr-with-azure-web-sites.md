---
uid: signalr/overview/deployment/using-signalr-with-azure-web-sites
title: SignalR을 사용 하 여 Azure App Service에서 Web Apps를 사용 하 여 | Microsoft Docs
author: pfletcher
description: 이 문서에서는 Microsoft Azure에서 실행 되는 SignalR 응용 프로그램을 구성 하는 방법을 설명 합니다. 소프트웨어 버전은 Visual Studio 2013 또는 Vis. 자습서에서 사용...
ms.author: aspnetcontent
ms.date: 07/01/2015
ms.assetid: 2a7517a0-b88c-4162-ade3-9bf6ca7062fd
msc.legacyurl: /signalr/overview/deployment/using-signalr-with-azure-web-sites
msc.type: authoredcontent
ms.openlocfilehash: 03db2debe6bf5935ced926ae8278df8b9d47c86a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37822168"
---
<a name="using-signalr-with-web-apps-in-azure-app-service"></a>Azure App Service에서 Web Apps에 SignalR 사용
====================
[Patrick Fletcher](https://github.com/pfletcher)

> 이 문서에서는 Microsoft Azure에서 실행 되는 SignalR 응용 프로그램을 구성 하는 방법을 설명 합니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads) 또는 Visual Studio 2012
> - .NET 4.5
> - SignalR 버전 2
> - Visual Studio 2013 또는 2012 용 azure SDK 2.3
>   
> 
> 
> ## <a name="questions-and-comments"></a>질문이 나 의견이 있으면
> 
> 이 자습서를 연결 하는 방법 및 새로운 개선할 수 있습니다 페이지의 맨 아래에 의견에서에 의견을 남겨 주세요. 에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR), [StackOverflow.com](http://stackoverflow.com/), 또는 [Microsoft Azure 포럼](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform).


## <a name="table-of-contents"></a>목차

- [소개](#introduction)
- [SignalR 웹 앱을 Azure App Service에 배포](#deploying)
- [Azure App Service에서 Websocket을 사용 하도록 설정](#websocket)
- [Azure Redis 캐시 백플레인으로 사용 하 여](#backplane)
- [다음 단계](#nextsteps)

<a id="introduction"></a>
## <a name="introduction"></a>소개

ASP.NET SignalR 새로운 수준의 서버와 웹 또는.NET 클라이언트 간의 상호 작용을 사용할 수 있습니다. Azure에서 호스트 하는 경우 SignalR 응용 프로그램 수 활용 항상 사용 가능한 확장성을 제공 클라우드에서 실행 하는 고성능 환경입니다.

<a id="deploying"></a>
## <a name="deploying-a-signalr-web-app-to-azure-app-service"></a>SignalR 웹 앱을 Azure App Service에 배포

SignalR은 온-프레미스 서버에 배포와 Azure에 응용 프로그램을 배포 하는 데 특정 복잡 한 문제를 추가 하지 않습니다. SignalR을 사용 하는 응용 프로그램 구성 또는 기타 설정을 변경 하지 않고 Azure에서 호스팅할 수 있습니다 (그러나 Websocket 지원에 대 한 참조 [Azure App Service에서 사용 하도록 설정 하면 Websocket](#websocket) 아래.) 이 자습서에서 만든 응용 프로그램 배포 하는 [초보자를 위한 자습서](../getting-started/tutorial-getting-started-with-signalr.md) azure.

**필수 구성 요소**

- Visual Studio 2013. Visual Studio가 없는 Visual Studio 2013 Express for Web의 Azure SDK 설치에 포함 됩니다.
- [Visual Studio 2013 용 azure SDK 2.3](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) 나 [Visual Studio 2012 용 Azure SDK 2.3](https://go.microsoft.com/fwlink/p/?linkid=323511)합니다.
- 이 자습서를 완료 하려면 Azure 구독을 사용 해야 합니다. 할 수 있습니다 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), 또는 [평가판 구독을 신청](https://azure.microsoft.com/pricing/free-trial/)합니다.

### <a name="deploying-a-signalr-web-app-to-azure"></a>Azure SignalR 웹 앱 배포

1. 완료 합니다 [초보자를 위한 자습서](../getting-started/tutorial-getting-started-with-signalr.md), 또는에서 완료 된 프로젝트를 다운로드 [코드 갤러리](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)합니다.
2. Visual Studio에서 선택 **빌드**하십시오 **SignalR 채팅 게시**합니다.
3. "웹 게시" 대화 상자에서 "Windows Azure 웹 사이트"를 선택 합니다.

    ![Azure 웹 사이트를 선택 합니다.](using-signalr-with-azure-web-sites/_static/image1.png)
4. Microsoft 계정에 로그인 하지 않은 경우 클릭 **로그인 하는 중...**  "기존 웹 사이트 선택" 대화 상자에 로그인 합니다.

    ![기존 웹 사이트를 선택 합니다.](using-signalr-with-azure-web-sites/_static/image2.png)    ![Azure에 로그인](using-signalr-with-azure-web-sites/_static/image3.png)
5. "기존 웹 사이트 선택" 대화 상자에서 클릭 **새로 만들기**합니다.

    ![새 웹 사이트](using-signalr-with-azure-web-sites/_static/image4.png)
6. "Windows Azure에서 사이트 만들기" 대화 상자에서 고유한 앱 이름을 입력 합니다. 지역 드롭다운 목록에서 가장 가까운 지역을 선택 합니다. **만들기**를 클릭합니다.

    ![Azure에서 사이트 만들기](using-signalr-with-azure-web-sites/_static/image5.png)
7. "웹 게시" 대화 상자에서 클릭 **게시**합니다.

    ![사이트 게시](using-signalr-with-azure-web-sites/_static/image6.png)
8. 앱 게시 완료 되 면 Azure App Service Web Apps에서 호스팅되는 SignalR 채팅 응용 프로그램을 브라우저에서 열립니다.

    ![브라우저에서 열고 사이트](using-signalr-with-azure-web-sites/_static/image7.png)

<a id="websocket"></a>
### <a name="enabling-websockets-on-azure-app-service-web-apps"></a>Azure App Service Web Apps에서 Websocket을 사용 하도록 설정

Websocket를 SignalR 응용 프로그램에 사용할 웹 앱에서 명시적으로 설정 해야 합니다. 그렇지 않으면 다른 프로토콜 사용 됩니다 (참조 [전송과 대체](../getting-started/introduction-to-signalr.md#transports) 세부 정보에 대 한).

Azure App Service Web Apps에서 Websocket을 사용 하려면 웹 앱의 구성 섹션에서 사용 하도록 설정 합니다. 이렇게 하려면 웹 앱을 엽니다는 [Azure 관리 포털](https://manage.windowsazure.com/), 선택한 구성 합니다.

![구성 탭](using-signalr-with-azure-web-sites/_static/image8.png)

구성 페이지의 맨 위에 있는 웹 앱에.NET 4.5 사용 됨을 확인 합니다.

![.NET framework 4.5 버전 설정](using-signalr-with-azure-web-sites/_static/image9.png)

구성 페이지에 **Websocket** 설정 선택 **에서**합니다.

![Websocket 설정을:에](using-signalr-with-azure-web-sites/_static/image10.png)

구성 페이지의 맨 아래에서 선택 **저장할** 변경 내용을 저장 합니다.

![설정 저장](using-signalr-with-azure-web-sites/_static/image11.png)

<a id="backplane"></a>
## <a name="using-the-azure-redis-cache-backplane"></a>Azure Redis 캐시 백플레인으로 사용 하 여

여러 인스턴스를 사용 하 여 웹 앱에 대 한 및 해당 인스턴스의 사용자 (, 예를 들어 하나의 인스턴스만 생성 하는 채팅 메시지 연결할 수 있도록 다른 인스턴스에 연결 된 사용자) 간에 상호 작용 해야 하는 경우, [Azure Redis Cache 백플레인에서](../performance/scaleout-with-redis.md) 응용 프로그램에서 구현 해야 합니다.

<a id="nextsteps"></a>
## <a name="next-steps"></a>다음 단계

Azure App Service에서 웹 앱에 대 한 자세한 내용은 참조 하세요. [Web Apps 개요](https://azure.microsoft.com/documentation/articles/app-service-web-overview/)합니다.
