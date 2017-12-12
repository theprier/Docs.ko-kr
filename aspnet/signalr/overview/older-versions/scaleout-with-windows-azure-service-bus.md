---
uid: signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
title: "Azure 서비스 버스에 SignalR 확장 (SignalR 1.x) | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/01/2013
ms.topic: article
ms.assetid: 501db899-e68c-49ff-81b2-1dc561bfe908
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: 0dd245b597ebd4b58b60a53276d7808b6e2377e7
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="signalr-scaleout-with-azure-service-bus-signalr-1x"></a>Azure 서비스 버스에 SignalR 확장 (SignalR 1.x)
====================
여 [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)

이 자습서에서는 서비스 버스 백플레인에서 사용 하 여 메시지를 각 역할 인스턴스에 배포 하는 Windows Azure 웹 역할에는 SignalR 응용 프로그램을 배포 합니다.

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

필수 구성 요소:

- Windows Azure 계정입니다.
- [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409)합니다.
- Visual Studio 2012입니다.

서비스 버스 백플레인에서 호환 이기도 [Service Bus for Windows Server](https://msdn.microsoft.com/en-us/library/windowsazure/dn282144.aspx), 버전 1.1. 그러나 Service Bus for Windows Server의 버전 1.0과 호환 되지 않습니다.

## <a name="pricing"></a>가격

서비스 버스 백플레인에서 항목을 사용 하 여 메시지를 보냅니다. 최신 가격 정보에 대 한 참조 [서비스 버스](https://azure.microsoft.com/pricing/details/service-bus/)합니다. 이 문서 작성 당시의 1 달러 매달 1000000 메시지를 보낼 수 있습니다. 백플레인에서 각 SignalR 허브 메서드 호출에 대해 서비스 버스 메시지를 보냅니다. 연결, 연결 끊김, 그룹 및 기타 조인 또는 종료에 대 한 일부 제어 메시지도 있습니다. 대부분의 응용 프로그램에서 대부분의 메시지 트래픽 허브 메서드 호출 됩니다.

## <a name="overview"></a>개요

자세한 자습서에 들어가기 전에 수행할 작업의 간략 한 개요는 다음과 같습니다.

1. Windows Azure 포털을 사용 하 여 새 서비스 버스 네임 스페이스를 만듭니다.
2. 응용 프로그램에 이러한 NuGet 패키지를 추가 합니다. 

    - [Microsoft.AspNet.SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [Microsoft.AspNet.SignalR.ServiceBus](http://www.nuget.org/packages/SignalR.WindowsAzureServiceBus)
3. SignalR 응용 프로그램을 만듭니다.
4. 백플레인에서 구성 하는 Global.asax에 다음 코드를 추가 합니다. 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

각 응용 프로그램에 대 한 "앱 이름"에 대 한 다른 값을 선택 합니다. 여러 응용 프로그램에서 동일한 값을 사용 하지 마십시오.

## <a name="create-the-azure-services"></a>Azure 서비스 만들기

에 설명 된 대로 클라우드 서비스를 만드는 [만들어 클라우드 서비스를 배포 하는 방법을](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)합니다. 섹션의 단계에 따라 "방법: 빠른 생성을 사용 하 여 클라우드 서비스 만들기"입니다. 이 자습서에 대 한 인증서를 업로드할 필요가 없습니다.

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

에 설명 된 대로 새 서비스 버스 네임 스페이스 만들기 [사용 하 여 서비스 버스 항목/구독 하는 방법을](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)합니다. "서비스 Namespace 만들기" 섹션의 단계를 수행 합니다.

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> 클라우드 서비스 및 서비스 버스 네임 스페이스에 대 한 동일한 지역을 선택 해야 합니다.


## <a name="create-the-visual-studio-project"></a>Visual Studio 프로젝트 만들기

Visual Studio를 시작합니다. **파일** 메뉴를 클릭 하 여 **새 프로젝트**합니다.

에 **새 프로젝트** 대화 상자에서 **Visual C#**합니다. 아래 **설치 된 템플릿**선택, **클라우드** 선택한 후 **Windows Azure 클라우드 서비스**합니다. 기본.NET Framework 4.5를 유지 합니다. ChatService 응용 프로그램 이름을 지정 하 고 클릭 **확인**합니다.

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

에 **새 Windows Azure 클라우드 서비스** 대화 상자에서 ASP.NET MVC 4 웹 역할 선택 합니다. 오른쪽 화살표 단추를 클릭 (**&gt;**) 솔루션에 역할을 추가 하려면.

따라서 새 역할 위로 마우스를 가져가고 연필 아이콘을 표시 합니다. 역할의 이름을 바꾸려면이 아이콘을 클릭 합니다. "SignalRChat" 역할 이름을 지정 하 고 클릭 **확인**합니다.

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

에 **새 ASP.NET MVC 4 프로젝트** 선택 마법사 **인터넷 응용 프로그램**합니다. **확인**을 클릭합니다. 프로젝트 마법사에서 두 개의 프로젝트를 만듭니다.

- ChatService:이 프로젝트는 Windows Azure 응용 프로그램. Azure 역할 및 기타 구성 옵션을 정의합니다.
- SignalRChat:이 프로젝트는 ASP.NET MVC 4 프로젝트.

## <a name="create-the-signalr-chat-application"></a>SignalR 채팅 응용 프로그램 만들기

채팅 응용 프로그램을 만들려면이 자습서의 단계를 따라 [SignalR 및 MVC 4 시작](tutorial-getting-started-with-signalr-and-mvc-4.md)합니다.

NuGet을 사용 하 여 필요한 라이브러리를 설치 합니다. **도구** 메뉴 선택 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다. 에 **패키지 관리자 콘솔** 창에서 다음 명령을 입력 합니다.

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

사용 하 여 `-ProjectName` Windows Azure 프로젝트를 사용 하지 않고 ASP.NET MVC 프로젝트에 패키지를 설치 하는 옵션입니다.

## <a name="configure-the-backplane"></a>백플레인에서 구성

응용 프로그램의 Global.asax 파일에 다음 코드를 추가 합니다.

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

이제 서비스 버스 연결 문자열을 가져올 해야 합니다. Azure 포털에서 만든 서비스 버스 네임 스페이스를 선택 하 고 선택 키 아이콘을 클릭 합니다.

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

클립보드에 연결 문자열을 복사한 다음에 붙여 넣습니다는 *connectionString* 변수입니다.

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a>Azure에 배포

솔루션 탐색기에서 확장 된 **역할** ChatService 프로젝트 내의 폴더입니다.

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

SignalRChat 역할을 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다. 선택 된 **구성** 탭 합니다. 아래 **인스턴스** 2를 선택 합니다. VM 크기 설정할 수도 있습니다 **매우 작음으로**합니다.

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

변경 내용을 저장 합니다.

솔루션 탐색기에서 ChatService 프로젝트를 마우스 오른쪽 단추로 클릭 합니다. **게시**를 선택합니다.

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

프로그램 첫 번째 시간 Windows Azure에 게시 인 경우 자격 증명을 다운로드 해야 합니다. 에 **게시** 마법사 "자격 증명을 다운로드 하려면 로그인"을 클릭 합니다. 이 라는 Windows Azure 포털에 로그인 하 여 게시 설정 파일 다운로드 표시 됩니다.

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

클릭 **가져오기** 하 고 다운로드 한 게시 설정 파일을 선택 합니다.

**다음**을 클릭합니다. 에 **게시 설정** 대화에서 **클라우드 서비스**를 앞에서 만든 클라우드 서비스를 선택 합니다.

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

**게시**를 클릭합니다. 응용 프로그램을 배포 하 고 Vm을 시작 하는 데 몇 분 정도 걸릴 수 있습니다.

이제 채팅 응용 프로그램을 실행 하면 역할 인스턴스에 서비스 버스 항목을 사용 하 여 Azure 서비스 버스를 통해 통신 합니다. 한 항목은 여러 구독자를 허용 하는 메시지 큐입니다.

백플레인에서 항목 및 구독에 자동으로 만듭니다. 구독 및 메시지 활동을 보려면 Azure 포털을 열고 서비스 버스 네임 스페이스 선택한 "항목"을 클릭 합니다.

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

대시보드에 표시 메시지 활동에 대 일 분 정도 걸릴 것으로 확인 합니다.

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

SignalR 항목 수명을 관리합니다. 응용 프로그램을 배포한으로 수동으로 항목을 삭제 하거나 항목의 설정을 변경 하지 마세요.
