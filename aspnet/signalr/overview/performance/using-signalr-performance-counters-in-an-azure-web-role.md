---
uid: signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
title: SignalR 성능 카운터를 사용 하 여 Azure 웹 역할에서 | Microsoft Docs
author: guardrex
description: 설치 하 고 Azure 웹 역할에서 SignalR 성능 카운터를 사용 하는 방법.
keywords: ASP.NET,signalr,performance 카운터, azure 웹 역할
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/11/2017
ms.topic: article
ms.assetid: 2a127d3b-21ed-4cc9-bec0-cdab4e742a25
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
msc.type: authoredcontent
ms.openlocfilehash: 2f6c6feb030fc17f95e7862c39029569f3d8c5dc
ms.sourcegitcommit: d8aa1d314891e981460b5e5c912afb730adbb3ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/05/2018
---
# <a name="using-signalr-performance-counters-in-an-azure-web-role"></a>SignalR 성능 카운터를 사용 하 여 Azure 웹 역할에서

[Luke Latham](https://github.com/guardrex)으로

SignalR 성능 카운터는 Azure 웹 역할에서 응용 프로그램의 성능을 모니터링 하는 데 사용 됩니다. 카운터는 Microsoft Azure 진단에서 캡처됩니다. SignalR 성능 카운터와 Azure에서 설치한 *signalr.exe*, 독립 실행형 또는 온-프레미스 응용 프로그램에 사용 되는 동일한 도구입니다. Azure 역할은 일시적인, 앱 설치 및 시작할 때 SignalR 성능 카운터를 등록을 구성 합니다.

## <a name="prerequisites"></a>필수 구성 요소

* [Visual Studio 2015](https://www.visualstudio.com/vs/visual-studio-express/)
* [Visual Studio 2015 (VS2015) 용 Microsoft Azure SDK](https://azure.microsoft.com/downloads/) **참고: SDK를 설치한 후 컴퓨터를 다시 시작 합니다.**
* Microsoft Azure 구독: Azure 무료 평가판 계정에 등록 하려면 참조 [Azure 무료 평가판](https://azure.microsoft.com/free/)합니다.

## <a name="creating-an-azure-web-role-application-that-exposes-signalr-performance-counters"></a>SignalR 성능 카운터를 노출 하는 Azure 웹 역할 응용 프로그램 만들기

1. Visual Studio 2015를 엽니다.

2. Visual Studio 2015에서 선택 **파일** > **새로** > **프로젝트**합니다.

3. 에 **템플릿** 의 창은 **새 프로젝트** 창의 **Visual C#** 노드를 선택는 **클라우드** 노드를 선택은 **Azure 클라우드 서비스** 템플릿. 앱 이름 지정 **SignalRPerfCounters** 선택 **확인**합니다.

   ![새 클라우드 응용 프로그램](using-signalr-performance-counters-in-an-azure-web-role/_static/image1.png)
    
4. 에 **새 Microsoft Azure 클라우드 서비스** 대화 상자에서 **ASP.NET 웹 역할** 선택 하 고는 > 단추를 역할 프로젝트에 추가 합니다. **확인**을 선택합니다.

   ![ASP.NET 웹 역할 추가](using-signalr-performance-counters-in-an-azure-web-role/_static/image2.png)
    
5. 에 **새 ASP.NET 웹 응용 프로그램-WebRole1** 대화 상자에서는 **MVC** 템플릿을 선택한 다음 선택 **확인**합니다.

   ![MVC 및 Web API 추가](using-signalr-performance-counters-in-an-azure-web-role/_static/image3.png)
    
6. **솔루션 탐색기**열고는 *diagnostics.wadcfgx* 아래 파일 **WebRole1**합니다.

   ![솔루션 탐색기 diagnostics.wadcfgx](using-signalr-performance-counters-in-an-azure-web-role/_static/image4.png)
    
7. 다음 구성 파일의 내용을 바꿉니다 하 고 파일을 저장 합니다.

   [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample1.xml)]
    
8. 열기는 **패키지 관리자 콘솔** 에서 **도구** > **NuGet 패키지 관리자**합니다. SignalR 및 SignalR 유틸리티 패키지의 최신 버전을 설치 하려면 다음 명령을 입력 합니다.

   [!code-powershell[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample2.ps1)]
    
9. 시작 하거나 재활용 하는 경우 역할 인스턴스로 SignalR 성능 카운터를 설치 하려면 응용 프로그램을 구성 합니다. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **WebRole1** 프로젝트를 마우스 선택 **추가** > **새 폴더**합니다. 새 폴더 이름을 *시작*합니다.

   ![시작 폴더를 추가 합니다.](using-signalr-performance-counters-in-an-azure-web-role/_static/image5.png)
    
10. 복사는 *signalr.exe* 파일 (사용 하 여 추가 된 **Microsoft.AspNet.SignalR.Utils** 패키지)에서 \<프로젝트 폴더 > / SignalRPerfCounters/packages/Microsoft.AspNet.SignalR.Utils.\< 버전 > / 도구에 *시작* 이전 단계에서 만든 폴더에 있습니다.

11. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *시작* 폴더와 선택 **추가** > **기존 항목**합니다. 나타나는 대화 상자에서 선택 *signalr.exe* 선택 **추가**합니다.

    ![Signalr.exe 프로젝트에 추가](using-signalr-performance-counters-in-an-azure-web-role/_static/image6.png)
    
12. 마우스 오른쪽 단추로 클릭는 *시작* 사용자가 만든 폴더입니다. **추가** > **새 항목**을 선택합니다. 선택 된 **일반** 노드를 선택 **텍스트 파일**, 새 항목 이름을 *SignalRPerfCounterInstall.cmd*합니다. 이 명령 파일은 웹 역할로 SignalR 성능 카운터를 설치 합니다.

    ![SignalR 성능 카운터 설치 배치 파일 만들기](using-signalr-performance-counters-in-an-azure-web-role/_static/image7.png)
     
13. Visual Studio를 만들 때의 *SignalRPerfCounterInstall.cmd* 파일을 자동으로 열립니다 주 창에 있습니다. 다음 스크립트는 파일의 내용을 대체 한 다음 저장 하 고 파일을 닫습니다. 이 스크립트 실행 *signalr.exe*, 역할 인스턴스 SignalR 성능 카운터에 추가 합니다.

    [!code-console[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample3.cmd)]
    
14. 선택 된 *signalr.exe* 파일 **솔루션 탐색기**합니다. 파일의 **속성**설정, **출력 디렉터리로 복사** 를 **항상 복사**합니다.

    ![항상 복사를 출력 디렉터리로 복사 설정](using-signalr-performance-counters-in-an-azure-web-role/_static/image8.png)
    
15. 에 대해 이전 단계를 반복 하는 *SignalRPerfCounterInstall.cmd* 파일입니다.

    
16. 마우스 오른쪽 단추로 클릭는 *SignalRPerfCounterInstall.cmd* 파일을 선택 **프로그램**합니다. 나타나는 대화 상자에서 선택 **바이너리 편집기** 선택 **확인**합니다.

    ![바이너리 편집기를 사용 하 여 열기](using-signalr-performance-counters-in-an-azure-web-role/_static/image9.png)
    
17. 바이너리 편집기에서 파일에 모든 선행 바이트를 선택 하 고 삭제 합니다. 파일을 저장한 후 닫습니다.

    ![선행 바이트를 삭제 합니다.](using-signalr-performance-counters-in-an-azure-web-role/_static/image10.png)
    
18. 열기 *ServiceDefinition.csdef* 실행 되는 시작 작업을 추가 하 고는 *SignalrPerfCounterInstall.cmd* 서비스가 시작할 때 파일:

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample4.xml?highlight=4-7)]
    
19. 열기 `Views/Shared/_Layout.cshtml` jQuery 번들 스크립트 파일의 끝에서 제거 합니다.

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample5.cshtml)]
    
20. 추가 지속적으로 호출 하는 JavaScript 클라이언트는 `increment` 서버에서 메서드. 열기 `Views/Home/Index.cshtml` 하 고 내용을 다음 코드로 바꿉니다.

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample6.cshtml)]
    
21. 새 폴더 만들기는 **WebRole1** 라는 프로젝트 *허브*합니다. 마우스 오른쪽 단추로 클릭는 *허브* 폴더에 **솔루션 탐색기**선택, **웹** > **SignalR**를 선택 하 고  **SignalR 허브 클래스 (v2)** 합니다. 새 허브 이름을 *MyHub.cs* 선택 **추가**합니다.

    ![새 항목 추가 대화 상자에서 허브 폴더에 추가 하는 SignalR 허브 클래스](using-signalr-performance-counters-in-an-azure-web-role/_static/image13.png)

22. *MyHub.cs* 주 창에 자동으로 열립니다. 내용을 다음 코드로 바꿉니다 다음 저장 하 고 파일을 닫습니다.

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample7.cs)]
    
23. *[Crank.exe](signalr-connection-density-testing-with-crank.md)*  SignalR 코드 베이스와 함께 제공 되는 도구 테스트 연결 밀도 됩니다. 크랭크 영구 연결을 요구 하므로 추가할 있습니다 사용할 사이트를 테스트할 때. 새 폴더를 추가할는 **WebRole1** 라는 프로젝트 *PersistentConnections*합니다. 이 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** > **클래스**합니다. 새 클래스 파일의 이름을 *MyPersistentConnections.cs* 선택 **추가**합니다.

24. Visual Studio 열립니다는 *MyPersistentConnections.cs* 주 창에는 파일입니다. 내용을 다음 코드로 바꿉니다 다음 저장 하 고 파일을 닫습니다.

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample8.cs)]
    
25. 사용 하는 `Startup` OWIN 시작 될 때 클래스 SignalR 개체를 시작 합니다. 열기 또는 만들기 *Startup.cs* 하 고 내용을 다음 코드로 바꿉니다.

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample9.cs)]
    
    위의 코드에는 `OwinStartup` 특성 OWIN 시작 하려면이 클래스를 표시 합니다. `Configuration` 메서드 SignalR을 시작 합니다.
    
26. Microsoft Azure 에뮬레이터에서 키를 눌러 응용 프로그램을 테스트 **F5**합니다.

    > [!NOTE]
    > 발생 하는 경우는 **FileLoadException** 에서 **MapSignalR**에 바인딩 리디렉션을 변경 *web.config* 다음과:

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample12.xml?highlight=3,7)]
    
27. 1 분 정도 기다립니다. Visual Studio에서 클라우드 탐색기 도구 창을 엽니다 (**보기** > **클라우드 탐색기**) 경로 확장 하 고 `(Local)/Storage Accounts/(Development)/Tables`합니다. 두 번 클릭 **WADPerformanceCountersTable**합니다. 테이블 데이터의 SignalR 카운터에 표시 됩니다. 테이블 보이지 않으면 Azure 저장소 자격 증명을 입력 해야 합니다. 선택 해야는 **새로 고침** 표를 참조 하는 단추 **클라우드 탐색기** 선택 또는 **새로 고침** 테이블 열기 창의 테이블에 데이터를 보려면 단추입니다.

    ![Visual Studio 클라우드 탐색기에서 WAD 성능 카운터 테이블을 선택 하면](using-signalr-performance-counters-in-an-azure-web-role/_static/image11.png)

    ![WAD 성능 카운터 테이블에서 수집 된 카운터를 표시 합니다.](using-signalr-performance-counters-in-an-azure-web-role/_static/image12.png)
    
28. 클라우드에서 응용 프로그램을 테스트 하려면 업데이트는 **ServiceConfiguration.Cloud.cscfg** 파일 및 설정는 `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` 에 유효한 Azure 저장소 계정 연결 문자열입니다.

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample10.xml)]

29. Azure 구독에 응용 프로그램을 배포 합니다. Azure에 응용 프로그램을 배포 하는 방법에 대 한 세부 정보를 참조 하십시오. [만들어 클라우드 서비스를 배포 하는 방법을](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)합니다.

30. 몇 분 기다립니다. **클라우드 탐색기**, 위에 구성 된 저장소 계정 키를 찾아서 찾을 `WADPerformanceCountersTable` 테이블에 있습니다. 테이블 데이터의 SignalR 카운터에 표시 됩니다. 테이블 보이지 않으면 Azure 저장소 자격 증명을 입력 해야 합니다. 선택 해야는 **새로 고침** 표를 참조 하는 단추 **클라우드 탐색기** 선택 또는 **새로 고침** 테이블 열기 창의 테이블에 데이터를 보려면 단추입니다.

특히 감사 드립니다 [Martin Richard](https://social.msdn.microsoft.com/profile/Martin+Richard) 이 자습서에 사용 된 원래 콘텐츠에 대 한 합니다.
