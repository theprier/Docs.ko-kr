---
uid: signalr/overview/older-versions/scaleout-with-sql-server
title: SQL Server로 SignalR 규모 확장 (SignalR 1.x) | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 05/01/2013
ms.assetid: 1dca7967-8296-444a-9533-837eb284e78c
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: be4adf7a5e8af603d64bb26d97e0149f40fb92a3
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37810371"
---
<a name="signalr-scaleout-with-sql-server-signalr-1x"></a>SQL Server로 SignalR 규모 확장 (SignalR 1.x)
====================
하 여 [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)

이 자습서에서는 SQL Server를 사용 하 여 메시지를 두 개의 별도 IIS 인스턴스에서 배포 되는 SignalR 응용 프로그램을 분산 하는 있습니다. 단일 테스트 컴퓨터에서이 자습서를 실행할 수도 있지만 모든 결과 얻으려면 두 개 이상의 서버에 SignalR 응용 프로그램을 배포 해야 합니다. 서버 중 하나에서 또는 별도 전용 서버에 SQL Server를 설치 해야 합니다. Azure에서 Vm을 사용 하는 자습서를 실행 하는 방법도 있습니다.

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a>전제 조건

Microsoft SQL Server 2005 이상입니다. 백플레인에서는 데스크톱 및 서버 모두 SQL Server 버전을 지원합니다. Azure SQL Database 또는 SQL Server Compact Edition을 지원 하지 않습니다. (응용 프로그램을 Azure에서 호스팅되는 경우 Service Bus 백플레인에서 대신 고려 합니다.)

## <a name="overview"></a>개요

자세한 자습서를 시작 하기 전에 수행할 작업의 간략 한 개요는 다음과 같습니다.

1. 새 빈 데이터베이스를 만듭니다. 백플레인에서이 데이터베이스에 필요한 테이블을 만들겠습니다.
2. 응용 프로그램에 이러한 NuGet 패키지를 추가 합니다. 

    - [Microsoft.AspNet.SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [Microsoft.AspNet.SignalR.SqlServer](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. SignalR 응용 프로그램을 만듭니다.
4. Global.asax 백플레인에서 구성 하려면 다음 코드를 추가 합니다. 

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

## <a name="configure-the-database"></a>데이터베이스 구성

응용 프로그램 Windows 인증 또는 SQL Server 인증을 사용 하는 데이터베이스에 액세스할 수 있는지 여부를 결정 합니다. 그럼에도 불구 하 고 데이터베이스 사용자 로그인, 스키마를 만들고, 테이블을 만들 수 있는 권한이 있는지 확인 합니다.

백플레인으로 사용에 대 한 새 데이터베이스를 만듭니다. 데이터베이스 이름을 지정할 수 있습니다. 데이터베이스에서 모든 테이블을 만들 필요가 없습니다. 백플레인에서 필요한 테이블을 만듭니다.

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a>Service Broker를 사용 하도록 설정

백플레인에서 데이터베이스에 대 한 Service Broker를 활성화 하는 것이 좋습니다. Service Broker는 메시징 및 백플레인에서 업데이트를 보다 효율적으로 받을 수 있는 SQL Server의 큐에 대 한 기본 지원을 제공 합니다. 그러나 (백플레인에서 없이 이루어집니다 Service Broker.)

Service Broker 사용 되는지 여부를 확인, 쿼리를 **은\_broker\_사용 하도록 설정** 열에는 **sys.databases** 카탈로그 뷰.

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

Service Broker를 사용 하도록 설정 하려면 다음 SQL 쿼리를 사용 합니다.

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> 교착 상태가 발생 했는지를이 쿼리가 나타납니다 경우 DB에 연결 하는 응용 프로그램이 없습니다.


추적을 설정한 경우 추적 Service Broker 사용 되는지 여부를 표시도 됩니다.

## <a name="create-a-signalr-application"></a>SignalR 응용 프로그램 만들기

이러한 자습서 중 하나를 수행 하 여 SignalR 응용 프로그램을 만듭니다.

- [SignalR 시작](../getting-started/tutorial-getting-started-with-signalr.md)
- [SignalR 및 MVC 4 시작](tutorial-getting-started-with-signalr-and-mvc-4.md)

다음으로, SQL Server를 사용 하 여 확장을 지원 하기 위해 채팅 응용 프로그램을 수정 합니다. 먼저 프로젝트에 SignalR.SqlServer NuGet 패키지를 추가 합니다. Visual Studio에서에서 합니다 **도구** 메뉴에서 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

다음으로 Global.asax 파일을 엽니다. 다음 코드를 추가 합니다 **응용 프로그램\_시작** 메서드:

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a>배포 하 고 응용 프로그램 실행

SignalR 응용 프로그램을 배포 하려면 Windows Server 인스턴스를 준비 합니다.

IIS 역할을 추가 합니다. WebSocket 프로토콜을 포함 하 여 "응용 프로그램 개발" 기능을 포함 합니다.

![](scaleout-with-sql-server/_static/image4.png)

관리 서비스 ("관리 도구" 아래)를 포함 합니다.

![](scaleout-with-sql-server/_static/image5.png)

**설치 웹 배포 3.0.** IIS 관리자를 실행 하면, Microsoft 웹 플랫폼을 설치 하 라는 메시지가 나타납니다 것 또는 할 수 있습니다 [다운로드를 intstaller](https://go.microsoft.com/fwlink/?LinkId=255386)합니다. 플랫폼 설치 관리자에서 웹 배포에 대 한 검색 하 고 웹 배포 3.0 설치

![](scaleout-with-sql-server/_static/image6.png)

Web Management Service가 실행 중인지 확인 합니다. 그렇지 않은 경우 서비스를 시작 합니다. (웹 관리 서비스 Windows 서비스 목록에 보이지 않으면 확인 IIS 역할을 추가 했을 때 Management 서비스를 설치 합니다.)

마지막으로, tcp 8172 포트를 엽니다. 웹 배포 도구를 사용 하는 포트입니다.

이제 서버에 개발 컴퓨터에서 Visual Studio 프로젝트를 배포할 준비가 되었습니다. 솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.

자세한 내용을 보려면 웹 배포에 대 한 설명서를 참조 하세요 [Visual Studio 및 ASP.NET 웹 배포 콘텐츠 맵](../../../whitepapers/aspnet-web-deployment-content-map.md)합니다.

두 명의 서버 응용 프로그램을 배포 하는 경우에 별도 브라우저 창에서 각 인스턴스를 엽니다 하 고 다른에서 SignalR 메시지를 받을 각각 볼 수 있습니다. (물론 프로덕션 환경에서 두 서버는 sit 부하 분산 합니다.)

![](scaleout-with-sql-server/_static/image7.png)

응용 프로그램을 실행 한 후에 SignalR에 데이터베이스의 테이블을 만들었다고 자동으로 확인할 수 있습니다.

![](scaleout-with-sql-server/_static/image8.png)

SignalR의 테이블을 관리합니다. 응용 프로그램을 배포 하기만 없는 행을 삭제, 테이블을 수정 및 등입니다.
