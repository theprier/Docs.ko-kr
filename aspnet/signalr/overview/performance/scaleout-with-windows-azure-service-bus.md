---
uid: signalr/overview/performance/scaleout-with-windows-azure-service-bus
title: Azure Service Bus로 SignalR 규모 확장 | Microsoft Docs
author: MikeWasson
description: 소프트웨어 버전 2 이전 버전을이 항목에서는이 항목의 SignalR 1.x 버전의이 항목에서는 Visual Studio 2013.NET 4.5 SignalR 버전에서 사용 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: ce1305f9-30fd-49e3-bf38-d0a78dfb06c3
ms.technology: dotnet-signalr
msc.legacyurl: /signalr/overview/performance/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: a9e5d59c1b9120a32fabe55b4864d861040bcd67
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37369152"
---
<a name="signalr-scaleout-with-azure-service-bus"></a>Azure Service Bus로 SignalR 규모 확장
====================
하 여 [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)

이 자습서에서는 Service Bus 백플레인에서 사용 하 여 각 역할 인스턴스에 메시지를 분산 하는 Windows Azure 웹 역할에는 SignalR 응용 프로그램 배포. (사용 하 여 Service Bus 백플레인에서 이용할 수 있습니다 [Azure App Service의 웹 앱](https://docs.microsoft.com/azure/app-service-web/).)

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

필수 구성 요소:

- Windows Azure 계정입니다.
- 합니다 [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409)합니다.
- Visual Studio 2012 또는 2013입니다.

Service bus 백플레인에서 호환 이기도 [Windows Server 용 Service Bus](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), 버전 1.1입니다. 그러나 Service Bus for Windows Server의 버전 1.0과 호환 되지 않습니다.

## <a name="pricing"></a>가격

Service Bus 백플레인에서 메시지를 보낼 항목을 사용 합니다. 최신 가격 정보 참조 [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/)합니다. 이 문서 작성 당시 1 달러 미만 매월 1,000,000 개의 메시지를 보낼 수 있습니다. 백플레인에서는 SignalR 허브 메서드에 대 한 각 호출에 대 한 service bus 메시지를 보냅니다. 일부 제어 메시지 등에 대 한 연결, 연결 끊김, 조인 또는 그대로 유지 되어 그룹도 있습니다. 대부분의 응용 프로그램에서 대부분의 메시지 트래픽 허브 메서드 호출 됩니다.

## <a name="overview"></a>개요

자세한 자습서를 시작 하기 전에 수행할 작업의 간략 한 개요는 다음과 같습니다.

1. 새 Service Bus 네임 스페이스를 만들려면 Windows Azure 포털을 사용 합니다.
2. 응용 프로그램에 이러한 NuGet 패키지를 추가 합니다. 

    - [Microsoft.AspNet.SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [Microsoft.AspNet.SignalR.ServiceBus3](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3) 또는 [Microsoft.AspNet.SignalR.ServiceBus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus)
3. SignalR 응용 프로그램을 만듭니다.
4. Startup.cs 백플레인에서 구성 하려면 다음 코드를 추가 합니다. 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

이 코드에 대 한 기본값을 사용 하 여 백플레인에서 구성 [TopicCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx) 하 고 [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)합니다. 이러한 값을 변경에 대 한 내용은 참조 하세요 [SignalR 성능: 확장 메트릭](signalr-performance.md#scaleout_metrics)합니다.

각 응용 프로그램에 대 한 "응용 프로그램 이름"에 대 한 다른 값을 선택 합니다. 여러 응용 프로그램에서 동일한 값을 사용 하지 마세요.

## <a name="create-the-azure-services"></a>Azure 서비스 만들기

에 설명 된 대로 클라우드 서비스를 만듭니다 [클라우드 서비스 만들기 및 배포 하는 방법을](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)합니다. 섹션의 단계에 따라 "방법: 빠른 생성을 사용 하 여 클라우드 서비스 만들기"입니다. 이 자습서에서는 인증서를 업로드할 필요가 없습니다.

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

에 설명 된 대로 새 Service Bus 네임 스페이스를 만듭니다 [방법을 사용 하 여 Service Bus 토픽/구독에](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)입니다. "서비스 Namespace 만들기" 섹션의 단계를 수행 합니다.

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> 클라우드 서비스 및 Service Bus 네임 스페이스에 대 한 동일한 지역을 선택 해야 합니다.


## <a name="create-the-visual-studio-project"></a>Visual Studio 프로젝트 만들기

Visual Studio를 시작합니다. **파일** 메뉴에서 클릭 **새 프로젝트**합니다.

에 **새 프로젝트** 대화 상자에서 **Visual C#** 합니다. 아래 **설치 된 템플릿**를 선택 **클라우드** 선택한 후 **Windows Azure 클라우드 서비스**합니다. 기본.NET Framework 4.5를 유지 합니다. ChatService 응용 프로그램 이름을 지정 하 고 클릭 **확인**합니다.

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

에 **새 Windows Azure 클라우드 서비스** 대화 상자에서 ASP.NET 웹 역할을 선택 합니다. 오른쪽 화살표 단추를 클릭 (**&gt;**) 솔루션에 역할을 추가 합니다.

따라서 새 역할 위로 마우스를 이동 연필 아이콘을 표시 합니다. 역할 이름을 바꾸려면이 아이콘을 클릭 합니다. "SignalRChat" 역할 이름을 지정 하 고 클릭 **확인**합니다.

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

에 **새 ASP.NET 프로젝트** 대화 상자에서 **MVC**, 확인을 클릭 합니다.

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

프로젝트 마법사에서 두 개의 프로젝트를 만듭니다.

- ChatService:이 프로젝트는 Windows Azure 응용 프로그램. Azure 역할 및 기타 구성 옵션을 정의합니다.
- SignalRChat:이 프로젝트는 ASP.NET MVC 5 프로젝트.

## <a name="create-the-signalr-chat-application"></a>SignalR 채팅 응용 프로그램 만들기

채팅 응용 프로그램을 만들려면이 자습서의 단계를 따라 [SignalR 및 MVC 5 시작](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)합니다.

필요한 라이브러리를 설치 하려면 NuGet을 사용 합니다. **도구** 메뉴에서 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다. 에 **패키지 관리자 콘솔** 창에서 다음 명령을 입력 합니다.

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

사용 된 `-ProjectName` Windows Azure 프로젝트 보다는 ASP.NET MVC 프로젝트에 패키지를 설치 하는 옵션입니다.

## <a name="configure-the-backplane"></a>백플레인에서 구성

응용 프로그램의 Startup.cs 파일에 다음 코드를 추가 합니다.

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

이제 service bus 연결 문자열 가져오기 해야 합니다. Azure portal에서 만든 service bus 네임 스페이스를 선택 하 고 액세스 키 아이콘을 클릭 합니다.

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

연결 문자열을 클립보드에 복사한 다음 붙여 넣습니다 합니다 *connectionString* 변수입니다.

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a>Azure에 배포

솔루션 탐색기에서 확장을 **역할** ChatService 프로젝트 내부 폴더.

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

SignalRChat 역할을 마우스 오른쪽 단추로 클릭 **속성**합니다. 선택 된 **구성** 탭 합니다. 아래 **인스턴스** 2를 선택 합니다. VM 크기 설정할 수도 있습니다 **작음**합니다.

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

변경 내용을 저장합니다.

솔루션 탐색기에서 ChatService 프로젝트를 마우스 오른쪽 단추로 클릭 합니다. **게시**를 선택합니다.

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

Windows Azure에 첫 번째 시간 게시 인 경우 자격 증명을 다운로드 해야 합니다. 에 **게시** 마법사 "자격 증명을 다운로드 하려면 로그인"을 클릭 합니다. Windows Azure 포털에 로그인 하 고 게시 설정 파일을 다운로드 하 라는 메시지가 나타납니다이 있습니다.

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

클릭 **가져오기** 다운로드 한 게시 설정 파일을 선택 합니다.

**다음**을 클릭합니다. 에 **게시 설정** 대화 상자 아래에 있는 **클라우드 서비스**, 앞에서 만든 클라우드 서비스를 선택 합니다.

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

**게시**를 클릭합니다. 응용 프로그램을 배포 하 고 Vm을 시작 하려면 몇 분 정도 걸릴 수 있습니다.

지금 채팅 응용 프로그램을 실행 하는 경우 역할 인스턴스가 Service Bus 토픽을 사용 하 여 Azure Service Bus를 통해 통신 합니다. 항목은 여러 구독자를 허용 하는 메시지 큐입니다.

백플레인에서 항목 및 구독에 자동으로 만듭니다. 구독 및 메시지 작업을 보려면 Azure portal을 열고 Service Bus 네임 스페이스를 선택한 "항목"을 클릭 합니다.

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

메시지 작업 대시보드에 표시 되는 데 몇 분 정도 걸릴 것을 확인 합니다.

![](scaleout-with-windows-azure-service-bus/_static/image15.png)

SignalR 항목 수명을 관리 합니다. 응용 프로그램 배포는 수동으로 항목을 삭제 하거나 해당 항목에 대 한 설정을 변경 하지 마세요.

## <a name="troubleshooting"></a>문제 해결

**System.InvalidOperationException "만 지원 되는 IsolationLevel is 'IsolationLevel.Serializable'."**

이 오류는 작업에 대 한 트랜잭션 수준을 이외의 값으로 설정 된 경우 `Serializable`합니다. 작업이 없는 다른 트랜잭션 수준을 사용 하 여 수행 되는 것을 확인 합니다.
