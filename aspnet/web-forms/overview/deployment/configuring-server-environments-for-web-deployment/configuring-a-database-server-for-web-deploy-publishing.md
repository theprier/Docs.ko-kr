---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
title: "배포 게시를 웹에 대 한 데이터베이스 서버 구성 | Microsoft Docs"
author: jrjlee
description: "이 항목에서는 웹 배포 및 게시를 지원 하도록 SQL Server 2008 R2 데이터베이스 서버를 구성 하는 방법에 설명 합니다. 이 항목에 설명 된 작업은 co 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: e7c447f9-eddf-4bbe-9f18-3326d965d093
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
msc.type: authoredcontent
ms.openlocfilehash: 98fd728f48f6fb64a61686bc58824b9fb3a28b13
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="configuring-a-database-server-for-web-deploy-publishing"></a>웹 배포 게시에 대 한 데이터베이스 서버 구성
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 웹 배포 및 게시를 지원 하도록 SQL Server 2008 R2 데이터베이스 서버를 구성 하는 방법에 설명 합니다.
> 
> 이 항목에 설명 된 작업은 일반적으로 모든 배포 시나리오 & #x 2014; 웹 서버에서 IIS 웹 배포 도구 (웹 배포) 원격 에이전트 서비스, 웹 배포 처리기 또는 오프 라인 배포를 사용 하도록 구성 된 여부와 상관 또는 단일 웹 서버 또는 서버 팜에서 응용 프로그램 실행 중입니다. 데이터베이스를 배포 하는 방법은 보안 요구 사항 및 기타 고려 사항에 따라 변경 될 수 있습니다. 예를 들어 상관 없이 샘플 데이터를 데이터베이스를 배포할 수 있습니다 및 사용자 역할 매핑을 배포 또는 배포 후 수동으로 구성할 수 있습니다. 그러나 데이터베이스 서버를 구성 하는 방법은 동일 하 게 유지 합니다.


웹 배포를 지원 하도록 데이터베이스 서버를 구성 하는 데 추가 제품 또는 도구를 설치할 필요가 없습니다. 데이터베이스 서버와 웹 서버를 서로 다른 컴퓨터에서 실행 있다고 가정 하면:

- SQL Server TCP/IP를 사용 하 여 통신을 허용 합니다.
- 방화벽을 통해 SQL Server 트래픽이 허용 됩니다.
- 웹 서버 컴퓨터 계정을 SQL Server 로그인을 제공 합니다.
- 모든 필수 데이터베이스 역할에 컴퓨터 계정 로그인을 매핑하십시오.
- 배포는 SQL Server 로그인 및 데이터베이스 작성자 권한이 실행 될 계정을 지정 합니다.
- 반복 배포를 지원 하기 위해 배포 계정 로그인을 매핑하는 **db\_소유자** 데이터베이스 역할입니다.

이 항목에서는 이러한 각 절차를 수행 하는 방법을 보여줍니다. 작업 및 연습이이 항목에서는 SQL Server 2008 r 2를 Windows Server 2008 r 2에서 실행 되는 기본 인스턴스의으로 시작 하는 가정 합니다. 계속 하기 전에 다음 사항을 확인.

- Windows Server 2008 R2 서비스 팩 1 및 가능한 모든 업데이트가 설치 됩니다.
- 서버가 도메인에 가입 합니다.
- 서버에 고정 IP 주소입니다.
- SQL Server 2008 R2 서비스 팩 1 및 가능한 모든 업데이트가 설치 됩니다.

SQL Server 인스턴스는만 포함 해야는 **데이터베이스 엔진 서비스** SQL Server 설치에 자동으로 포함 된 역할을 합니다. 그러나 구성 및 유지 관리의 용이성을 위해 권장 포함 하는 **관리 도구-기본** 및 **관리 도구-전체** 서버 역할입니다.

> [!NOTE]
> 참조 컴퓨터는 도메인에 가입에 대 한 자세한 내용은 [도메인 및 로그온에 컴퓨터 가입](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)합니다. 고정 IP 주소를 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [고정 IP 주소 구성](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)합니다. SQL Server 설치에 대 한 자세한 내용은 참조 하십시오. [SQL Server 2008 R2 설치](https://technet.microsoft.com/library/bb500395.aspx)합니다.


## <a name="enable-remote-access-to-sql-server"></a>SQL Server에 대 한 원격 액세스를 사용 하도록 설정

SQL Server TCP/IP를 사용 하 여 원격 컴퓨터와 통신 합니다. 데이터베이스 서버와 웹 서버는 서로 다른 컴퓨터에 있는 경우 해야 합니다.

- SQL Server TCP/IP를 통한 통신을 허용 하도록 네트워킹 설정을 구성 합니다.
- TCP 트래픽을 허용 (및 경우에 따라 데이터 그램 프로토콜 UDP (User) 트래픽)에 SQL Server 인스턴스가 사용 하는 포트에서 하드웨어 또는 소프트웨어 방화벽을 구성 합니다.

TCP/IP를 통해 통신 하는 SQL Server를 사용 하려면 SQL Server 구성 관리자를 사용 하 여 SQL Server 인스턴스에 대 한 네트워크 구성을 변경 합니다.

**TCP/IP를 사용 하 여 통신 하도록 SQL Server를 사용 하도록 설정 하려면**

1. 에 **시작** 메뉴에서 **모든 프로그램**, 클릭 **Microsoft SQL Server 2008 R2**, 클릭 **구성 도구**, 클릭 하 고 **SQL Server 구성 관리자**합니다.
2. 트리 뷰 창에서 확장 **SQL Server 네트워크 구성**, 클릭 하 고 **MSSQLSERVER에 대 한 프로토콜**합니다.

    > [!NOTE]
    > SQL Server의 여러 인스턴스를 설치한 경우 표시 됩니다는 **에 대 한 프로토콜 * * * [인스턴스 이름]* 각 인스턴스에 대 한 항목입니다. 인스턴스에 의해 인스턴스 기반에서 네트워크 설정을 구성 해야 합니다.
3. 세부 정보 창에서 마우스 오른쪽 단추로 클릭는 **TCP/IP** 행을 클릭 하 고 **사용**합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image1.png)
4. 에 **경고** 대화 상자를 클릭 **확인**합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image2.png)
5. 새로운 네트워크 구성의 적용 하려면 MSSQLSERVER 서비스를 다시 시작 해야 합니다. SQL Server Management Studio 또는 서비스 콘솔에서 명령 프롬프트를 수행할 수 있습니다. 이 절차에서는 SQL Server Management Studio를 사용 합니다.
6. SQL Server 구성 관리자를 닫습니다.
7. 에 **시작** 메뉴에서 **모든 프로그램**, 클릭 **Microsoft SQL Server 2008 R2**, 클릭 하 고 **SQL Server Management Studio**합니다.
8. 에 **서버에 연결** 대화 상자는 **서버 이름** 상자 데이터베이스 서버의 이름을 입력 한 다음 클릭 **연결**합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image3.png)
9. 에 **개체 탐색기** 창 부모 서버 노드를 마우스 오른쪽 단추로 클릭 (예를 들어 **TESTDB1**)를 클릭 하 고 **다시 시작**합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image4.png)
10. 에 **Microsoft SQL Server Management Studio** 대화 상자를 클릭 **예**합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image5.png)
11. 서비스를 다시 시작한 경우에 SQL Server Management Studio를 닫습니다.

방화벽을 통해 SQL Server 트래픽을 허용 하려면 먼저 SQL Server 인스턴스에서 사용 하는 포트를 확인 해야 합니다. 이 SQL Server 인스턴스를 생성 하 고 구성 하는 방법에 따라 달라 집니다.

- A *기본 인스턴스* 수신의 SQL Server (및에 응답) TCP 포트 1433에 대 한 요청입니다.
- A *명명 된 인스턴스* 수신의 SQL Server (및 응답 하는) 동적으로 할당 된 TCP 포트에서 요청 합니다.
- SQL Server Browser 서비스를 사용 하는 경우 클라이언트는 UDP 포트 1434 특정 SQL Server 인스턴스에 사용 하는 TCP 포트를 찾으려면 서비스를 쿼리할 수 있습니다. 그러나이 서비스 종종 보안상의 이유로 불가능 합니다.

SQL Server의 기본 인스턴스를 사용 하는 있다고 가정할 경우 트래픽을 허용 하도록 방화벽을 구성 해야 합니다.

| 방향 | 포트에서 | 이식 하려면 | 포트 유형 |
| --- | --- | --- | --- |
| 인바운드 | 임의의 값 | 1433 | TCP |
| 아웃 바운드 | 1433 | 임의의 값 | TCP |
  

> [!NOTE]
> 기술적으로 클라이언트 컴퓨터 SQL Server와 통신 하 1024과 5000 사이의 임의로 할당 된 TCP 포트를 사용 되 고 그에 따라 방화벽 규칙을 제한할 수 있습니다. SQL Server 포트 및 방화벽에 대 한 자세한 내용은 참조 하십시오. [TCP/IP 포트 번호 to SQL 방화벽을 통해 통신 하는 데 필요한](https://go.microsoft.com/?linkid=9805125) 및 [하는 방법: 특정 TCP 포트로 (SQL Server 구성에서 수신 하도록 서버 구성 관리자)](https://msdn.microsoft.com/library/ms177440.aspx)합니다.


대부분의 Windows Server 환경에서 데이터베이스 서버에서 Windows 방화벽을 구성 해야 가능성이 높습니다. 기본적으로 Windows 방화벽 규칙을 구체적으로 금지 하지 않는 한 모든 아웃 바운드 트래픽을 허용 합니다. 데이터베이스에 액세스 하도록 웹 서버를 사용 하려면 SQL Server 인스턴스가 사용 하는 포트 번호에 TCP 트래픽을 허용 하는 인바운드 규칙을 구성 해야 합니다. SQL Server의 기본 인스턴스를 사용 하는 경우에이 규칙을 구성 하려면 다음 절차를 사용할 수 있습니다.

**기본 SQL Server 인스턴스를 사용한 통신을 허용 하도록 Windows 방화벽을 구성 하려면**

1. 데이터베이스 서버에서에 **시작** 메뉴에서 **관리 도구**, 클릭 하 고 **고급 보안이 포함 된 Windows 방화벽**합니다.
2. 트리 뷰 창에서 클릭 **인바운드 규칙**합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image6.png)
3. 에 **동작** 창 아래에서 **인바운드 규칙**, 클릭 **새 규칙**합니다.
4. 새 인바운드 규칙 마법사에서에 **규칙 유형** 페이지에서 **포트**, 클릭 하 고 **다음**합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image7.png)
5. 에 **프로토콜 및 포트** 페이지 **TCP** 을 선택 및는 **특정 로컬 포트** 상자에 입력 합니다 **1433**, 클릭 하 고 **다음**합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image8.png)
6. 에 **동작** 페이지에서 **연결 허용** 선택한 클릭 **다음**합니다.
7. 에 **프로필** 페이지에서 **도메인** 선택의 선택을 취소는 **개인** 및 **공용** 확인란을 선택한 다음 클릭  **다음**합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image9.png)
8. 에 **이름** 페이지에서 규칙에 적절 한 설명이 포함 된 이름을 지정 (예를 들어 **SQL Server 기본 인스턴스에 대 한 네트워크 액세스**)를 클릭 하 고 **마침**합니다.

비표준 또는 동적 포트를 통해 SQL Server와 통신, 참조 하는 경우에 특히 SQL Server, Windows 방화벽 구성에 대 한 자세한 내용은 [하는 방법: 데이터베이스 엔진 액세스에 대 한 Windows 방화벽 구성](https://technet.microsoft.com/library/ms175043.aspx)합니다.

## <a name="configure-logins-and-database-permissions"></a>로그인을 구성 및 데이터베이스 권한

인터넷 정보 서비스 (IIS)에 웹 응용 프로그램을 배포 하면 응용 프로그램이 응용 프로그램 풀의 id를 사용 하 여 실행 합니다. 도메인 환경에서 응용 프로그램 풀 id에는 네트워크 리소스에 액세스할 실행 되는 서버의 컴퓨터 계정을 사용 합니다. 컴퓨터 계정에는 다음 양식을 사용 * [도메인 이름]***\** * [컴퓨터 이름]***$ * * & #x 2014; 예를 들어 **FABRIKAM\TESTWEB1$**합니다. 네트워크를 통해 데이터베이스에 액세스 하려면 웹 응용 프로그램을 허용 하려면:

- SQL Server 인스턴스를 웹 서버 컴퓨터 계정에 대 한 로그인을 추가 합니다.
- 모든 필수 데이터베이스 역할에 컴퓨터 계정 로그인 매핑 (일반적으로 **db\_datareader** 및 **db\_datawriter**).

단일 서버 보다는 서버 팜의으로 웹 응용 프로그램 실행은 서버 팜의 모든 웹 서버에 대해이 절차를 반복 해야 합니다.

> [!NOTE]
> 응용 프로그램 풀 id 및 네트워크 리소스에 액세스에 대 한 자세한 내용은 참조 하십시오. [응용 프로그램 풀 Id](https://go.microsoft.com/?linkid=9805123)합니다.


다양 한 방법으로 이러한 작업을 높일 수 있습니다. 로그인을 제출할 수 있습니다.

- TRANSACT-SQL 또는 SQL Server Management Studio를 사용 하 여 데이터베이스 서버에 수동으로 로그인을 만듭니다.
- Visual Studio에서 SQL Server 2008 서버 프로젝트를 사용 하 여 만들고 로그인에 배포 합니다.

SQL Server 로그인 이므로 데이터베이스 수준 개체 보다는 서버 수준 개체를 배포 하려는 데이터베이스에 종속 되지 않습니다. 따라서 언제 든 지 로그인을 만들 수 있습니다 및 가장 쉬운 방법은 종종 하는 데이터베이스 배포를 시작 하기 전에 데이터베이스 서버에서 로그인을 수동으로 만들어야 합니다. 로그인을 만들려면 SQL Server Management Studio에서 다음 절차를 사용할 수 있습니다.

**웹 서버 컴퓨터 계정에 대 한 SQL Server 로그인을 만들려면**

1. 데이터베이스 서버에서에 **시작** 메뉴에서 **모든 프로그램**, 클릭 **Microsoft SQL Server 2008 R2**, 클릭 하 고 **SQL Server Management Studio** .
2. 에 **서버에 연결** 대화 상자는 **서버 이름** 상자 데이터베이스 서버의 이름을 입력 한 다음 클릭 **연결**합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image10.png)
3. 에 **개체 탐색기** 창에서 마우스 오른쪽 단추로 클릭 **보안**, 가리킨 **새로**, 클릭 하 고 **로그인**합니다.
4. 에 **로그인-신규** 대화 상자는 **로그인 이름** 웹 서버 컴퓨터 계정 이름을 입력 합니다 (예를 들어 **FABRIKAM\TESTWEB1$**).

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image11.png)
5. **확인**을 클릭합니다.

이 시점에서 데이터베이스 서버는 웹 배포 게시를 위해 준비 합니다. 그러나 모든 솔루션 배포 필수 데이터베이스 역할에 컴퓨터 계정 로그인을 매핑할 때까지 작동 하지 않습니다. 생각 보다 많은 필요 데이터베이스 역할에 로그인 매핑 때 없습니다 후까지 맵 역할 배포한 데이터베이스. 필수 데이터베이스 역할에 컴퓨터 계정 로그인을 매핑하려면 제출할 수 있습니다.

- 처음으로 데이터베이스를 배포한 후 해당 로그인에 데이터베이스 역할을 수동으로 할당 합니다.
- 배포 후 스크립트를 사용 하 여 로그인에 데이터베이스 역할을 할당 합니다.

로그인 및 데이터베이스 역할 매핑을 만들기를 자동화에 대 한 자세한 내용은 참조 하십시오. [배포 데이터베이스 역할 멤버 자격이 테스트 환경에](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)합니다. 또는 필수 데이터베이스 역할에 컴퓨터 계정 로그인을 수동으로 매핑할 다음 절차를 사용할 수 있습니다. 기억 될 때까지이 절차를 수행할 수 없습니다 *후* 데이터베이스를 배포 했습니다.

**데이터베이스 역할을 웹 서버 컴퓨터 계정 로그인에 매핑**

1. 이전 처럼 SQL Server Management Studio를 엽니다.
2. 에 **개체 탐색기** 창에서 확장 하 고는 **보안** 노드를 확장 하 고는 **로그인** 노드를 한 컴퓨터 계정 로그인을 두 번 클릭 한 다음 (예를 들어  **FABRIKAM\TESTWEB1$**).

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image12.png)
3. 에 **로그인 속성** 대화 상자를 클릭 **사용자 매핑**합니다.
4. 에 **이 로그인으로 매핑된 사용자** 테이블, 데이터베이스의 이름을 선택 (예를 들어 **ContactManager**).
5. 에 **데이터베이스 역할 멤버 자격:** *[데이터베이스 이름]* 목록에서 필요한 권한을 선택 합니다. Contact Manager 샘플 솔루션의 경우 선택 해야 합니다는 **db\_datareader** 및 **db\_datawriter** 역할입니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image13.png)
6. **확인**을 클릭합니다.

데이터베이스 역할을 수동으로 매핑은 테스트 환경에 더욱 적합 한 종종를 스테이징 또는 프로덕션 환경에 대 한 자동화 된 또는 한 번의 클릭 배포에 대 한 작은 좋을 것입니다. 이러한 종류의 배포 후 스크립트를 사용 하 여 작업의 자동화에서 자세한 정보를 찾을 수 [배포 데이터베이스 역할 멤버 자격이 테스트 환경에](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)합니다.

> [!NOTE]
> 서버 프로젝트 및 데이터베이스 프로젝트에 대 한 자세한 내용은 참조 하십시오. [Visual Studio 2010 SQL Server 데이터베이스 프로젝트](https://msdn.microsoft.com/library/ff678491.aspx)합니다.


## <a name="configure-permissions-for-the-deployment-account"></a>배포 계정에 대 한 사용 권한 구성

사용 하 여 배포를 실행 하는 계정이 SQL Server 관리자가 아닌 경우도이 계정에 대 한 로그인을 만드는 데 필요 합니다. 데이터베이스를 만들기 위해는 계정은의 구성원 이어야 합니다는 **dbcreator** 서버 역할 또는 동등한 권한이 있어야 합니다.

> [!NOTE]
> 웹 배포 또는 VSDBCMD를 사용 하 여 데이터베이스를 배포 하는 경우 (SQL Server 인스턴스는 혼합된 모드 인증을 지원 하도록 구성 됨) 하는 경우 Windows 자격 증명 또는 SQL Server 자격 증명을 사용할 수 있습니다. 다음 절차에서는 Windows 자격 증명을 사용 하려고 하지만에서 배포를 구성 하는 경우 연결 문자열에 SQL Server 사용자 이름 및 암호를 지정 하면 아무는 가정 합니다.


**배포 계정에 대 한 사용 권한을 설정 하려면**

1. 이전 처럼 SQL Server Management Studio를 엽니다.
2. 에 **개체 탐색기** 창에서 마우스 오른쪽 단추로 클릭 **보안**, 가리킨 **새로**, 클릭 하 고 **로그인**합니다.
3. 에 **로그인-신규** 대화 상자는 **로그인 이름** 배포 계정의 이름을 입력 합니다 (예를 들어 **FABRIKAM\matt**).
4. 에 **페이지 선택** 창에서 클릭 **서버 역할**합니다.
5. 선택 **dbcreator**, 클릭 하 고 **확인**합니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image14.png)

후속 배포를 지원 하기 위해 해야에 배포 하는 계정을 추가 하는 **db\_소유자** 처음 배포 된 후 데이터베이스 역할을 합니다. 후속 배포에는 기존 데이터베이스의 스키마를 수정 하지 않고 하므로 새 데이터베이스를 만드는 중입니다. 이전 섹션에서 설명한 이유로 데이터베이스를 만든 될 때까지 사용자 데이터베이스 역할에 추가할 수 없습니다.

**Db 배포 계정 로그인을 매핑할\_소유자 데이터베이스 역할**

1. 이전 처럼 SQL Server Management Studio를 엽니다.
2. 에 **개체 탐색기** 창 확장는 **보안** 노드를 확장 하 고는 **로그인** 노드를 한 컴퓨터 계정 로그인을 두 번 클릭 한 다음 (예를 들어  **FABRIKAM\matt**).
3. 에 **로그인 속성** 대화 상자를 클릭 **사용자 매핑**합니다.
4. 에 **이 로그인으로 매핑된 사용자** 테이블, 데이터베이스의 이름을 선택 (예를 들어 **ContactManager**).
5. 에 **데이터베이스 역할 멤버 자격:** *[데이터베이스 이름]* 목록, 선택는 **db\_소유자** 역할입니다.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image15.png)
6. **확인**을 클릭합니다.

## <a name="conclusion"></a>결론

이제 데이터베이스 서버에 원격 데이터베이스 배포에 동의 하 고 원격 IIS 웹 서버에 데이터베이스에 액세스할 수 있도록 준비 됩니다. 배포 하 고 데이터베이스를 사용 하려고 하기 전에 이러한 주요 사항을 확인 하는 것이 좋습니다.

- SQL Server 원격 TCP/IP 연결을 허용 하도록 구성 했습니까?
- SQL Server 트래픽을 허용 하도록 방화벽 구성 했습니까?
- SQL Server에 액세스 하는 모든 웹 서버에 대 한 컴퓨터 계정 로그인 작성 했습니까?
- 데이터베이스 배포 스크립트를 만들 사용자 역할 매핑을 포함 또는이를 만들 수동으로 처음으로 데이터베이스를 배포한 후 해야 하나요?
- 사용자 배포 계정에 대 한 로그인을 만들고 추가 하는 **dbcreator** 서버 역할?

## <a name="further-reading"></a>추가 정보

데이터베이스 프로젝트 배포에 대 한 지침을 참조 하십시오. [데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md)합니다. 배포 후 스크립트를 실행 하 여 데이터베이스 역할 멤버 자격을 만들기에 대 한 지침을 참조 하십시오. [배포 데이터베이스 역할 멤버 자격이 테스트 환경에](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)합니다. 멤버 자격 데이터베이스에서 발생할 수 있는 고유한 배포 과제를 충족 하는 방법에 대 한 지침을 참조 하십시오. [엔터프라이즈 환경에 배포 멤버 자격 데이터베이스](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)합니다.

>[!div class="step-by-step"]
[이전](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
[다음](creating-a-server-farm-with-the-web-farm-framework.md)
