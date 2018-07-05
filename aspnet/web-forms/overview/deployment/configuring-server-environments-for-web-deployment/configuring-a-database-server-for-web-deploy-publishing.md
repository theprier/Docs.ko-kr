---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
title: 배포 게시용 웹에 대 한 데이터베이스 서버 구성 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 웹 배포 및 게시를 지원 하도록 SQL Server 2008 R2 데이터베이스 서버를 구성 하는 방법을 설명 합니다. 이 항목에 설명 된 작업은 공동...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: e7c447f9-eddf-4bbe-9f18-3326d965d093
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
msc.type: authoredcontent
ms.openlocfilehash: 5563b737e3fd200070951f8d281ed8015137ae35
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37384461"
---
<a name="configuring-a-database-server-for-web-deploy-publishing"></a>웹 배포 게시용 데이터베이스 서버 구성
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 웹 배포 및 게시를 지원 하도록 SQL Server 2008 R2 데이터베이스 서버를 구성 하는 방법을 설명 합니다.
> 
> 이 항목에 설명 된 작업은 모든 배포 시나리오에 공통적으로 적용&#x2014;웹 서버는 IIS 웹 배포 도구 (웹 배포) 원격 에이전트 서비스, 웹 배포 처리기 또는 오프 라인 배포를 사용 하도록 구성 된 여부와 상관 또는 응용 프로그램은 단일 웹 서버 또는 서버 팜의에서 실행 됩니다. 데이터베이스를 배포 하는 방법은 보안 요구 사항 및 기타 고려 사항에 따라 변경 될 수 있습니다. 예를 들어, 샘플 데이터 없이 데이터베이스를 배포할 수 있습니다 및 사용자 역할 매핑을 배포 또는 배포 후 수동으로 구성 될 수 있습니다. 그러나 데이터베이스 서버를 구성 하는 방법은 동일 하 게 유지 합니다.


웹 배포를 지원 하도록 데이터베이스 서버를 구성 하는 데 추가 제품 또는 도구를 설치할 필요가 없습니다. 데이터베이스 서버 및 웹 서버를 서로 다른 컴퓨터에서 실행을 만든다고 가정 하면:

- SQL Server TCP/IP를 사용 하 여 통신을 허용 합니다.
- 방화벽을 통해 SQL Server 트래픽을 허용 합니다.
- 웹 서버 컴퓨터 계정을 SQL Server 로그인을 제공 합니다.
- 필요한 데이터베이스 역할에 컴퓨터 계정 로그인을 매핑하십시오.
- 배포는 SQL Server 로그인 및 데이터베이스 작성자 권한이 실행 계정에 부여 합니다.
- 반복 배포를 지원 하려면 배포 계정 로그인을 매핑하는 **db\_소유자** 데이터베이스 역할.

이 항목에서는 이러한 각 절차를 수행 하는 방법을 보여줍니다. 작업은이 항목의 연습에서는 Windows Server 2008 R2를 실행 하는 SQL Server 2008 R2의 기본 인스턴스를 사용 하 여 시작 하 고 있음을 가정 합니다. 계속 하기 전에 확인 합니다.

- Windows Server 2008 R2 서비스 팩 1 및 모든 사용 가능한 업데이트가 설치 됩니다.
- 서버가는 도메인에 가입 된입니다.
- 서버에 고정 IP가 있습니다.
- SQL Server 2008 R2 서비스 팩 1 및 모든 사용 가능한 업데이트가 설치 됩니다.

SQL Server 인스턴스는만 포함 해야 합니다 **데이터베이스 엔진 서비스** 역할을 모든 SQL Server 설치에 자동으로 포함 됩니다. 단, 구성 및 유지 관리 편의성을 위해 권장 하는 합니다 **관리 도구-기본** 하 고 **관리 도구-전체** 서버 역할입니다.

> [!NOTE]
> 참조 컴퓨터를 도메인에 가입 하는 방법은 [도메인 및 로그온에 컴퓨터 가입](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)합니다. 고정 IP 주소를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [정적 IP 주소를 구성](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)합니다. SQL Server 설치에 대 한 자세한 내용은 참조 하세요. [SQL Server 2008 R2 설치](https://technet.microsoft.com/library/bb500395.aspx)합니다.


## <a name="enable-remote-access-to-sql-server"></a>SQL Server에 대 한 원격 액세스를 사용 하도록 설정

SQL Server TCP/IP를 사용 하 여 원격 컴퓨터와 통신할 수 있습니다. 데이터베이스 서버 및 웹 서버는 서로 다른 컴퓨터에 있는 경우에 필요 합니다.

- SQL Server TCP/IP를 통한 통신을 허용 하도록 네트워킹 설정을 구성 합니다.
- TCP 트래픽을 허용 (및 사용자 데이터 그램 프로토콜 (UDP)의 경우 일부 트래픽)에 SQL Server 인스턴스를 사용 하는 포트에서 모든 하드웨어 또는 소프트웨어 방화벽을 구성 합니다.

TCP/IP를 통해 통신 하는 SQL Server를 사용 하도록 설정 하려면 SQL Server 인스턴스에 대 한 네트워크 구성을 변경 하려면 SQL Server 구성 관리자를 사용 합니다.

**TCP/IP를 사용 하 여 통신 하도록 SQL Server를 사용 하도록 설정 하려면**

1. 에 **시작** 메뉴에서 **프로그램도**, 클릭 **Microsoft SQL Server 2008 R2**, 클릭 **구성 도구**, 클릭 하 고 **SQL Server 구성 관리자**합니다.
2. 트리 뷰 창에서 확장 **SQL Server 네트워크 구성**를 클릭 하 고 **MSSQLSERVER 용 프로토콜**합니다.

   > [!NOTE]
   > SQL Server의 여러 인스턴스를 설치한 경우 표시 됩니다는 <strong>에 대 한 프로토콜</strong><em>[인스턴스 이름]</em> 각 인스턴스에 대 한 항목입니다. 인스턴스에 의해 단위로 네트워크 설정을 구성 해야 합니다.
3. 세부 정보 창에서 마우스 오른쪽 단추로 클릭 합니다 **TCP/IP** 행을 클릭 하 고 **사용**합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image1.png)
4. 에 **경고** 대화 상자, 클릭 **확인**합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image2.png)
5. 새로운 네트워크 구성을 적용 하려면 MSSQLSERVER 서비스를 다시 시작 해야 합니다. 서비스 콘솔에서 또는 SQL Server Management Studio에서 명령 프롬프트에서 수행할 수 있습니다. 이 절차에서는 SQL Server Management Studio를 사용 합니다.
6. SQL Server 구성 관리자를 닫습니다.
7. 에 **시작** 메뉴에서 **모든 프로그램**, 클릭 **Microsoft SQL Server 2008 R2**를 클릭 하 고 **SQL Server Management Studio**합니다.
8. 에 **서버에 연결** 대화 상자의 합니다 **서버 이름** 상자, 데이터베이스 서버의 이름을 입력 한 다음 클릭 **연결**합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image3.png)
9. 에 **개체 탐색기** 창 상위 서버 노드를 마우스 오른쪽 단추로 클릭 (예를 들어 **TESTDB1**)를 클릭 하 고 **다시 시작**합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image4.png)
10. 에 **Microsoft SQL Server Management Studio** 대화 상자, 클릭 **예**합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image5.png)
11. 서비스 다시 시작 하는 경우 SQL Server Management Studio를 닫습니다.

방화벽을 통해 SQL Server 트래픽을 허용 하려면 먼저 SQL Server 인스턴스를 사용 하 여 포트를 알고 해야 합니다. 이 SQL Server 인스턴스를 생성 하 고 구성 하는 방법에 따라 달라 집니다.

- A *기본 인스턴스* SQL server에 대 한 수신 (및 응답할) TCP 포트 1433에 대 한 요청입니다.
- A *명명 된 인스턴스* SQL server에 대 한 수신 (및 응답할) 동적으로 할당 된 TCP 포트에서 요청 합니다.
- SQL Server Browser 서비스를 사용 하는 경우 클라이언트는 UDP 포트 1434 특정 SQL Server 인스턴스에 대해 사용 하는 TCP 포트를 확인 하려면 서비스를 쿼리할 수 있습니다. 그러나이 서비스는 종종 보안상의 이유로 비활성화 됩니다.

SQL Server의 기본 인스턴스를 사용 하는 가정 트래픽을 허용 하도록 방화벽을 구성 해야 합니다.

| 방향 | 포트에서 | 포트 | 포트 유형 |
| --- | --- | --- | --- |
| 인바운드 | 임의의 값 | 1433 | TCP |
| 아웃 바운드 | 1433 | 임의의 값 | TCP |
  

> [!NOTE]
> 기술적으로 클라이언트 컴퓨터를 임의로 할당 된 TCP 포트 1024-5000을 사용 하 여 SQL Server와 통신 하 고 방화벽 규칙을 적절 하 게 제한할 수 있습니다. SQL Server 포트 및 방화벽에 대 한 자세한 내용은 참조 하세요. [to SQL 방화벽을 통해 통신 해야 하는 TCP/IP 포트 번호](https://go.microsoft.com/?linkid=9805125) 및 [방법: 특정 TCP 포트 (SQL Server 구성에서 수신 하도록 서버 구성 관리자)](https://msdn.microsoft.com/library/ms177440.aspx)합니다.


대부분의 Windows Server 환경에서 데이터베이스 서버에서 Windows 방화벽을 구성 해야 가능성이 높습니다. 기본적으로 Windows 방화벽 규칙을 구체적으로 금지 하지 않는 한 모든 아웃 바운드 트래픽을 허용 합니다. 데이터베이스에 연결할 웹 서버를 사용 하려면 SQL Server 인스턴스를 사용 하는 포트 번호에 TCP 트래픽을 허용 하는 인바운드 규칙을 구성 해야 합니다. SQL Server의 기본 인스턴스를 사용 하는 경우에이 규칙을 구성 하려면 다음 절차를 사용할 수 있습니다.

**기본 SQL Server 인스턴스를 사용 하 여 통신을 허용 하도록 Windows 방화벽을 구성 하려면**

1. 데이터베이스 서버의는 **시작** 메뉴에서 **관리 도구**를 클릭 하 고 **고급 보안이 포함 된 Windows 방화벽**합니다.
2. 트리 뷰 창에서 클릭 **인바운드 규칙**합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image6.png)
3. 에 **동작** 창 아래에 있는 **인바운드 규칙**, 클릭 **새 규칙**합니다.
4. 새 인바운드 규칙 마법사에서에 **규칙 유형** 페이지에서 **포트**를 클릭 하 고 **다음**합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image7.png)
5. 에 **프로토콜 및 포트** 페이지에서 **TCP** 을 선택 하면 및를 **특정 로컬 포트** 상자에 입력 **1433**를 클릭 하 고 **다음**합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image8.png)
6. 에 **동작** 페이지에서 **연결을 허용** 선택 하 고 클릭 **다음**합니다.
7. 에 **프로필** 페이지에서 **도메인** 지우기 옵션을 선택 합니다 **개인** 및 **공용** 확인란을 선택한 다음 클릭  **다음**합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image9.png)
8. 에 **이름** 페이지에서 규칙 이름을 적절 하 게 설명 (예를 들어 **SQL Server 기본 인스턴스에 대 한 네트워크 액세스**)를 클릭 하 고 **마침**.

내용은 비표준 또는 동적 포트를 통해 SQL Server와 통신 해야 하는 경우에 특히 SQL Server에 대 한 Windows 방화벽을 구성 하는 방법은 [방법: 데이터베이스 엔진 액세스에 대 한 Windows 방화벽 구성](https://technet.microsoft.com/library/ms175043.aspx)합니다.

## <a name="configure-logins-and-database-permissions"></a>로그인을 구성 및 데이터베이스 권한

인터넷 정보 서비스 (IIS) 웹 응용 프로그램을 배포할 때는 응용 프로그램 풀의 id를 사용 하 여 응용 프로그램을 실행 합니다. 도메인 환경에서 응용 프로그램 풀 id에는 실행 네트워크 리소스에 액세스 하는 서버의 컴퓨터 계정을 사용 합니다. 컴퓨터 계정 형태가 <em>[도메인 이름]</em><strong>\</s o n ><em>[컴퓨터 이름]</em><strong>$</strong>&#x2014;예를 들어, <strong>FABRIKAM\TESTWEB1$</strong>합니다. 네트워크를 통해 데이터베이스에 액세스 하려면 웹 응용 프로그램에 있도록 해야 합니다.

- SQL Server 인스턴스를 웹 서버 컴퓨터 계정에 대 한 로그인을 추가 합니다.
- 필요한 데이터베이스 역할에 컴퓨터 계정 로그인에 매핑합니다 (일반적으로 **db\_datareader** 하 고 **db\_datawriter**).

웹 응용 프로그램은 단일 서버가 아닌 서버 팜에 실행 하는 경우에 서버 팜의 모든 웹 서버에 대해이 절차를 반복 해야 합니다.

> [!NOTE]
> 응용 프로그램 풀 id 및 네트워크 리소스에 액세스에 대 한 자세한 내용은 참조 하세요. [응용 프로그램 풀 Id](https://go.microsoft.com/?linkid=9805123)합니다.


다양 한 방법으로 이러한 작업을 높일 수 있습니다. 로그인을 만들려면 다음 하거나 수행할 수 있습니다.

- TRANSACT-SQL 또는 SQL Server Management Studio를 사용 하 여 데이터베이스 서버의 로그인을 수동으로 만듭니다.
- Visual Studio에서 SQL Server 2008 서버 프로젝트를 사용 하 여 만들고 로그인을 배포 합니다.

SQL Server 로그인 이므로 데이터베이스 수준 개체를 보다는 서버 수준 개체를 배포 하려는 데이터베이스에 종속 되지 않습니다. 이와 같이 언제 든 지 로그인을 만들 수 있습니다 및 가장 쉬운 방법은 데이터베이스를 배포 하기 전에 데이터베이스 서버의 로그인을 수동으로 만들 경우가 많습니다. SQL Server Management Studio에서 로그인을 만들려면 다음 절차를 사용할 수 있습니다.

**웹 서버 컴퓨터 계정에 대 한 SQL Server 로그인을 만들려면**

1. 데이터베이스 서버의는 **시작** 메뉴에서 **모든 프로그램**, 클릭 **Microsoft SQL Server 2008 R2**를 클릭 하 고 **SQL Server Management Studio** .
2. 에 **서버에 연결** 대화 상자의 합니다 **서버 이름** 상자, 데이터베이스 서버의 이름을 입력 한 다음 클릭 **연결**합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image10.png)
3. 에 **개체 탐색기** 창 마우스 오른쪽 단추로 클릭 **보안**를 가리킨 **새로 만들기**, 클릭 하 고 **로그인**합니다.
4. 에 **로그인 – 새로 만들기** 대화 상자의 합니다 **로그인 이름** 상자에 웹 서버 컴퓨터 계정의 이름을 입력 (예를 들어 **FABRIKAM\TESTWEB1$**).

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image11.png)
5. **확인**을 클릭합니다.

이 시점에서 데이터베이스 서버는 웹 배포 게시를 위해 준비 합니다. 그러나 배포 하는 모든 솔루션에 필요한 데이터베이스 역할에 컴퓨터 계정 로그인을 매핑할 때까지 작동 하지 않습니다. 생각 보다 많이 필요한 데이터베이스 역할에 로그인 매핑, 것 없습니다 후 될 때까지 지도 역할 배포한 데이터베이스입니다. 컴퓨터 계정 로그인에 필요한 데이터베이스 역할을 매핑할 수 있습니다.

- 처음으로 데이터베이스를 배포한 후 로그인에 데이터베이스 역할을 수동으로 할당 합니다.
- 배포 후 스크립트를 사용 하 여 로그인에 데이터베이스 역할을 할당 합니다.

로그인 및 데이터베이스 역할 매핑을 만들기를 자동화 하는 방법은 참조 하세요 [배포 데이터베이스 역할 멤버 자격 테스트 환경에](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)입니다. 또는 필요한 데이터베이스 역할에 컴퓨터 계정 로그인을 수동으로 매핑할 다음 절차를 사용할 수 있습니다. 될 때까지이 절차를 수행할 수 없다는 기억 *후* 데이터베이스를 배포 했습니다.

**데이터베이스 역할은 웹 서버 컴퓨터 계정 로그인에 매핑할**

1. 이전 처럼 SQL Server Management Studio를 엽니다.
2. 에 **개체 탐색기** 창 확장를 **보안** 노드를 확장 합니다 **로그인** 노드를 컴퓨터 계정 로그인을 두 번 클릭 하 고 (예를 들어  **FABRIKAM\TESTWEB1$**).

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image12.png)
3. 에 **로그인 속성** 대화 상자, 클릭 **사용자 매핑**합니다.
4. 에 **이 로그인으로 매핑된 사용자** 테이블에서 데이터베이스의 이름을 선택 (예를 들어 **ContactManager**).
5. 에 **데이터베이스 역할 멤버 자격:** *[데이터베이스 이름]* 목록에서 필요한 권한을 선택 합니다. Contact Manager 샘플 솔루션의 경우 선택 해야 합니다 **db\_datareader** 및 **db\_datawriter** 역할입니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image13.png)
6. **확인**을 클릭합니다.

데이터베이스 역할을 수동으로 매핑 테스트 환경에 더욱 적합 한 경우가 것 스테이징 또는 프로덕션 환경에 자동화 된 또는 한 번 클릭 배포를 위해 그다지 바람직하지 않습니다. 이러한 종류의 배포 후 스크립트를 사용 하 여 태스크의 자동화에 대 한 자세한 정보를 찾을 수 있습니다 [배포 데이터베이스 역할 멤버 자격 테스트 환경에](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)입니다.

> [!NOTE]
> 서버 프로젝트와 데이터베이스 프로젝트에 대 한 자세한 내용은 참조 하세요. [Visual Studio 2010 SQL Server 데이터베이스 프로젝트](https://msdn.microsoft.com/library/ff678491.aspx)합니다.


## <a name="configure-permissions-for-the-deployment-account"></a>배포 계정에 대 한 사용 권한 구성

배포를 실행 하려면 사용 하는 계정이 SQL 서버 관리자가 아닌 경우에이 계정에 대 한 로그인을 만드는 해야 합니다. 데이터베이스를 만들기 위해 계정은의 구성원 이어야 합니다는 **dbcreator** 서버 역할 이거나 해당 권한을 가져야 합니다.

> [!NOTE]
> 웹 배포 또는 VSDBCMD를 사용 하 여 데이터베이스를 배포 하는 경우 (SQL Server 인스턴스 혼합된 모드 인증을 지원 하도록 구성 됨) 하는 경우 Windows 자격 증명 또는 SQL Server 자격 증명을 사용할 수 있습니다. 다음 절차는 Windows 자격 증명을 사용 하려고 하지만에서 배포를 구성한 경우 연결 문자열에 SQL Server 사용자 이름 및 암호를 지정 하면 중지 하는 항목이 없는 가정 합니다.


**배포 계정에 대 한 사용 권한을 설정 하려면**

1. 이전 처럼 SQL Server Management Studio를 엽니다.
2. 에 **개체 탐색기** 창 마우스 오른쪽 단추로 클릭 **보안**를 가리킨 **새로 만들기**, 클릭 하 고 **로그인**합니다.
3. 에 **로그인 – 새로 만들기** 대화 상자의 합니다 **로그인 이름** 상자 배포 계정의 이름을 입력 합니다 (예를 들어 **FABRIKAM\matt**).
4. 에 **페이지 선택** 창 클릭 **서버 역할**입니다.
5. 선택 **dbcreator**를 클릭 하 고 **확인**합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image14.png)

후속 배포를 지원 하려면 해야 배포 계정을 추가 하는 **db\_소유자** 처음 배포 된 후 데이터베이스의 역할입니다. 후속 배포에는 기존 데이터베이스의 스키마를 수정 하지 않고 있습니다 새 데이터베이스를 만들기 때문입니다. 이전 섹션에서 설명한 대로, 여러 가지 이유로 데이터베이스를 만든 때까지 사용자는 데이터베이스 역할에 추가할 수 없습니다.

**Db 배포 계정 로그인에 매핑할\_소유자 데이터베이스 역할**

1. 이전 처럼 SQL Server Management Studio를 엽니다.
2. 에 **개체 탐색기** 창 확장를 **보안** 노드를 확장 합니다 **로그인** 노드를 컴퓨터 계정 로그인을 두 번 클릭 하 고 (예를 들어,  **FABRIKAM\matt**).
3. 에 **로그인 속성** 대화 상자, 클릭 **사용자 매핑**합니다.
4. 에 **이 로그인으로 매핑된 사용자** 테이블에서 데이터베이스의 이름을 선택 (예를 들어 **ContactManager**).
5. 에 **데이터베이스 역할 멤버 자격:** *[데이터베이스 이름]* 목록에서를 **db\_소유자** 역할입니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image15.png)
6. **확인**을 클릭합니다.

## <a name="conclusion"></a>결론

이제 데이터베이스 서버에 원격 데이터베이스 배포를 허용 하는 데 원격 IIS 웹 서버가 데이터베이스에 액세스할 수 있도록 준비 됩니다. 배포 하 고 데이터베이스를 사용 하려고 하기 전에 이러한 요점을 확인 하는 것이 좋습니다.

- SQL Server 원격 TCP/IP 연결을 허용 하도록 구성 했습니까?
- SQL Server 트래픽을 허용 하도록 방화벽을 구성 했습니까?
- SQL Server를 액세스 하는 모든 웹 서버에 대 한 컴퓨터 계정 로그인을 작성 했습니까?
- 데이터베이스 배포 스크립트를 만들 사용자 역할 매핑을 포함 또는 처음으로 데이터베이스를 배포한 후 수동으로 이러한 만들어야 하나요?
- 가 배포 계정에 대 한 로그인을 만들고 추가 하는 **dbcreator** 서버 역할?

## <a name="further-reading"></a>추가 정보

데이터베이스 프로젝트를 배포 하는 방법에 대 한 지침을 참조 하세요 [데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md)합니다. 배포 후 스크립트를 실행 하 여 데이터베이스 역할 멤버 자격을 만들기에 대 한 지침을 참조 하세요 [배포 데이터베이스 역할 멤버 자격 테스트 환경에](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)입니다. 멤버 자격 데이터베이스에서 발생할 수 있는 고유한 배포 과제를 충족 하는 방법에 대 한 지침을 참조 하세요 [엔터프라이즈 환경에 멤버 자격 데이터베이스 배포](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)합니다.

> [!div class="step-by-step"]
> [이전](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
> [다음](creating-a-server-farm-with-the-web-farm-framework.md)
