---
uid: signalr/overview/performance/scaleout-with-sql-server
title: SQL Server와 함께 SignalR 확장 | Microsoft Docs
author: MikeWasson
description: 이전 버전의에 대 한 내용은이 항목의 버전 2 이전 버전을 Visual Studio 2013.NET 4.5 SignalR이이 항목에서 사용 하는 소프트웨어 버전 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: 98358b6e-9139-4239-ba3a-2d7dd74dd664
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/performance/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: b3189c36fc076333c0c6007bd039b12e03d63bc8
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874371"
---
<a name="signalr-scaleout-with-sql-server"></a>SQL Server와 함께 SignalR 확장
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


이 자습서에서는 SQL Server를 사용 하 여 두 개의 별도 IIS 인스턴스에서 배포 되는 SignalR 응용 프로그램 간에 메시지를 분산 합니다. 단일 테스트 컴퓨터에서이 자습서를 실행할 수도 있지만 모든 결과 얻기 위해 둘 이상의 서버 SignalR 응용 프로그램 배포 해야 합니다. 서버 중 하나 또는 별도 전용된 서버에도 SQL Server를 설치 해야 합니다. 두 번째 방법은 Azure에서 Vm을 사용 하는 자습서를 실행 하는 것입니다.

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a>전제 조건

Microsoft SQL Server 2005 이상입니다. 백플레인에서는 데스크톱 및 서버 모두 SQL Server 버전을 지원합니다. SQL Server Compact Edition 또는 Azure SQL 데이터베이스를 지원 하지 않습니다. (응용 프로그램을 Azure에서 호스트 될 고려 서비스 버스 백플레인에서 대신 합니다.)

## <a name="overview"></a>개요

자세한 자습서에 들어가기 전에 수행할 작업의 간략 한 개요는 다음과 같습니다.

1. 비어 있는 새 데이터베이스를 만듭니다. 백플레인에서이 데이터베이스에 필요한 테이블 만들어집니다.
2. 응용 프로그램에 이러한 NuGet 패키지를 추가 합니다. 

    - [Microsoft.AspNet.SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [Microsoft.AspNet.SignalR.SqlServer](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. SignalR 응용 프로그램을 만듭니다.
4. 백플레인에서 구성 하려면 Startup.cs에 다음 코드를 추가 합니다. 

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

   이 코드에 대 한 기본 값으로 백플레인에서 구성 [TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) 및 [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)합니다. 변경 된 이러한 값에 대 한 정보를 참조 하십시오. [SignalR 성능: 확장 메트릭](signalr-performance.md#scaleout_metrics)합니다. 

## <a name="configure-the-database"></a>데이터베이스 구성

응용 프로그램 Windows 인증 또는 SQL Server 인증을 사용 하는 데이터베이스에 액세스할 수 있는지 여부를 결정 합니다. 그럼에도 불구 하 고 데이터베이스 사용자는 로그인 하 고 스키마를 만들 테이블을 만들 수 있는 권한이 있는지 확인 하십시오.

사용할 백플레인에서 대 한 새 데이터베이스를 만듭니다. 데이터베이스에 임의의 이름을 지정할 수 있습니다. 데이터베이스;에서 모든 테이블을 만들 필요가 없습니다. 백플레인에서 필요한 테이블 만들어집니다.

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a>Service Broker를 사용 하도록 설정

백플레인 데이터베이스에 대 한 Service Broker를 활성화 하는 것이 좋습니다. Service Broker는 메시징 및 백플레인에서 업데이트를 보다 효율적으로 받을 수 있는 SQL Server의 큐에 대 한 기본 지원을 제공 합니다. 그러나 (백플레인에서 에서도 사용할 수 없는 Service Broker.)

Service Broker가 설정 여부를 확인 하려면 쿼리는 **은\_브로커\_활성화** 열에는 **sys.databases** 카탈로그 뷰.

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

Service Broker를 활성화 하려면 다음 SQL 쿼리를 사용 합니다.

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> DB에 연결 하는 응용 프로그램이 없습니다 없으면이 쿼리 표시 하려면 교착 상태에 있는지 확인 하세요.


추적을 사용 하는 경우 추적 Service Broker 사용 되는지 여부를 표시도 됩니다.

## <a name="create-a-signalr-application"></a>SignalR 응용 프로그램 만들기

이러한 자습서 중 하나를 수행 하 여 SignalR 응용 프로그램을 만듭니다.

- [SignalR 2.0 시작](../getting-started/tutorial-getting-started-with-signalr.md)
- [SignalR 2.0 및 MVC 5 시작](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

다음으로, SQL Server와 함께 확장을 지원 하도록 채팅 응용 프로그램을 수정 합니다. 먼저 프로젝트에 SignalR.SqlServer NuGet 패키지를 추가 합니다. Visual Studio에서에서 **도구** 메뉴 선택 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

다음으로 Startup.cs 파일을 엽니다. 다음 코드를 추가 하는 **구성** 메서드:

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a>배포 및 응용 프로그램 실행

SignalR 응용 프로그램을 배포 하 여 Windows Server 인스턴스를 준비 합니다.

IIS 역할을 추가 합니다. WebSocket 프로토콜을 포함 하 여 "응용 프로그램 개발" 기능을 포함 합니다.

![](scaleout-with-sql-server/_static/image4.png)

관리 서비스 ("관리 도구" 아래에 나열)도 포함 됩니다.

![](scaleout-with-sql-server/_static/image5.png)

**설치 웹 배포 3.0.** IIS 관리자를 실행 하면, Microsoft 웹 플랫폼 설치를 묻습니다 또는 할 수 있습니다 때 [는 intstaller 다운로드](https://go.microsoft.com/fwlink/?LinkId=255386)합니다. 플랫폼 설치 관리자에서 웹 배포를 검색 하 고 웹 배포 3.0 설치

![](scaleout-with-sql-server/_static/image6.png)

웹 관리 서비스에서 실행 되 고 있는지 확인 합니다. 그렇지 않은 경우 서비스를 시작 합니다. (웹 관리 서비스 보이지 않으면의 Windows 서비스 목록에 있는지 확인 IIS 역할을 추가 했을 때 관리 서비스를 설치 합니다.)

마지막으로, tcp 8172 포트를 엽니다. 웹 배포 도구를 사용 하는 포트입니다.

이제 서버에 개발 컴퓨터에서 Visual Studio 프로젝트를 배포할 준비가 되었습니다. 솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.

웹 배포에 대 한 설명서 보다 자세한 참조 [Visual Studio 및 ASP.NET에 대 한 웹 배포 콘텐츠 맵](../../../whitepapers/aspnet-web-deployment-content-map.md)합니다.

두 명의 서버에 응용 프로그램을 배포 하는 경우 각 인스턴스는 별도 브라우저 창에서 열고 하 고 다른에서 SignalR 메시지를 받을 구성 파일은 각각을 확인할 수 있습니다. (물론, 프로덕션 환경에서 두 서버는 sit 부하 분산 장치 뒤.)

![](scaleout-with-sql-server/_static/image7.png)

응용 프로그램을 실행 한 후에 SignalR에 데이터베이스에 테이블을 만들었다고 자동으로 확인할 수 있습니다.

![](scaleout-with-sql-server/_static/image8.png)

SignalR 테이블을 관리합니다. 응용 프로그램을 배포한으로 하지 않는 행을 삭제을 테이블을 수정 하 고 등 합니다.
