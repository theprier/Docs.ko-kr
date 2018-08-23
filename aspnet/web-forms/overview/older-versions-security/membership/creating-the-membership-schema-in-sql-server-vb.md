---
uid: web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-vb
title: SQL Server (VB)에서 멤버 자격 스키마 만들기 | Microsoft Docs
author: rick-anderson
description: 이 자습서는 SqlMembershipProvider를 사용 하려면 데이터베이스에 필요한 스키마를 추가 하는 기술을 검사 하 여 시작 합니다. 다음에서는 마법사...
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 112a674d-716f-41a6-99b8-4074d65a54c0
msc.legacyurl: /web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-vb
msc.type: authoredcontent
ms.openlocfilehash: 62a6113c9ddad1722160c7092308939cf7883588
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838587"
---
<a name="creating-the-membership-schema-in-sql-server-vb"></a>SQL Server (VB)에서 멤버 자격 스키마 만들기
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_04_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial04_MembershipSetup_vb.pdf)

> 이 자습서는 SqlMembershipProvider를 사용 하려면 데이터베이스에 필요한 스키마를 추가 하는 기술을 검사 하 여 시작 합니다. 다음 스키마에 있는 키 테이블을 검사 하 고 목적 및 중요도 설명 합니다. 이 자습서는 ASP.NET 응용 프로그램 멤버 자격 프레임 워크를 사용 해야 하는 공급자를 구별 하는 방법 살펴보기 끝납니다.


## <a name="introduction"></a>소개

폼 인증을 사용 하 여 웹 사이트 방문자를 식별 하려면 검사할 두 이전 자습서입니다. Forms 인증 프레임 워크를 사용 하면 개발자가 웹 사이트에 사용자를 로그인 하 고 인증 티켓 사용 하 여 페이지 방문에서 기억 하기 쉬워집니다. `FormsAuthentication` 클래스는 티켓을 생성 하 고 방문자의 쿠키를 추가 하기 위한 메서드를 포함 합니다. 합니다 `FormsAuthenticationModule` 들어오는 모든 요청을 검사 하 고 사용자에 게 유효한 인증 티켓을 만들고 연결을 `GenericPrincipal` 및 `FormsIdentity` 현재 요청을 사용 하 여 개체입니다. 폼 인증에는 단순히에, 사용자의 id를 확인 하는 티켓을 구문 분석 하는 후속 요청을 기록할 때 방문자 인증 티켓을 부여 하기 위한 메커니즘입니다. 사용자 계정을 지원 하기 위해 웹 응용 프로그램을 계속 하는 사용자 저장소를 구현 하 고 자격 증명 유효성 검사, 새 사용자 및 다른 사용자 계정 관련 작업 수많은 등록 기능을 추가 해야 합니다.

ASP.NET 2.0 이전에 개발자가 이러한 모든 사용자 계정 관련 작업을 구현 하기 위한에 부딪힌 사람들 않았습니다. 다행 스럽게도 ASP.NET 팀이 이러한 단점을 인식 하 고 ASP.NET 2.0을 사용 하 여 멤버 자격 프레임 워크를 도입 했습니다. 멤버 자격 프레임 워크는.NET Framework의 핵심 사용자 계정 관련 작업을 수행 하는 것에 대 한 프로그래밍 인터페이스를 제공 하는 클래스의 집합입니다. 이 프레임 워크 위에 빌드되는 [공급자 모델](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx), 개발자는 사용자 지정된 구현 하는 표준화 된 API에 연결할 수 있습니다.

에 설명 된 대로 합니다 <a id="Tutorial1"> </a> [ *보안 기본 사항 및 ASP.NET 지원* ](../introduction/security-basics-and-asp-net-support-vb.md) 자습서에서는 두 명의 기본 제공 멤버 자격 공급자와 함께 제공 되는.NET Framework: [ `ActiveDirectoryMembershipProvider` ](https://msdn.microsoft.com/library/system.web.security.activedirectorymembershipprovider.aspx) 및 [ `SqlMembershipProvider` ](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx)합니다. 이름에서 알 수 있듯이 `SqlMembershipProvider` 사용자 저장소로 Microsoft SQL Server 데이터베이스를 사용 합니다. 응용 프로그램에서이 공급자를 사용 하려면 저장소로 사용할 데이터베이스 공급자를 지시 해야 합니다. 짐작할 수는 `SqlMembershipProvider` 사용자 저장소 데이터베이스 특정 데이터베이스 테이블, 뷰 및 저장된 프로시저에 필요 합니다. 선택한 데이터베이스에이 필요한 스키마를 추가 해야 합니다.

이 자습서를 사용 하려면 데이터베이스에 필요한 스키마를 추가 하는 기술을 검사 하 여 시작 된 `SqlMembershipProvider`합니다. 다음 스키마에 있는 키 테이블을 검사 하 고 목적 및 중요도 설명 합니다. 이 자습서는 ASP.NET 응용 프로그램 멤버 자격 프레임 워크를 사용 해야 하는 공급자를 구별 하는 방법 살펴보기 끝납니다.

이제 시작 하겠습니다.

## <a name="step-1-deciding-where-to-place-the-user-store"></a>1 단계: 사용자 저장소를 배치 하는 위치를 결정 합니다.

ASP.NET 응용 프로그램의 데이터는 일반적으로 다양 한 데이터베이스의 테이블에 저장 됩니다. 구현 하는 경우는 `SqlMembershipProvider` 데이터베이스 스키마에 응용 프로그램 데이터와 동일한 데이터베이스 또는 대체 데이터베이스에서 멤버 자격 스키마를 배치할지 여부를 결정 해야 합니다.

다음과 같은 이유로 응용 프로그램 데이터와 같은 데이터베이스에서 멤버 자격 스키마를 찾는 것이 좋습니다.

- **유지 관리** 를 이해 하 고, 유지 관리 하 고, 보다 2 개의 개별 데이터베이스에 있는 응용 프로그램을 배포 하는 응용 프로그램 데이터는 하나의 데이터베이스에 캡슐화 되어 쉽습니다.
- **관계 무결성** 응용 프로그램 테이블로 동일한 데이터베이스에 멤버 자격 관련 테이블을 배치 하 여 설정할 수는 [foreign key 제약 조건을](http://en.wikipedia.org/wiki/Foreign_key) 의 기본 키 간에 멤버 자격 관련 된 테이블과 관련 된 응용 프로그램입니다.

사용자 저장소 및 응용 프로그램 데이터를 개별 데이터베이스로 분리만 적합 한 여러 응용 프로그램을 각각 별도 데이터베이스를 사용 하지만 일반 사용자 저장소를 공유 해야 합니다.

### <a name="creating-a-database"></a>데이터베이스 만들기

에서는 구축 하는 두 번째 자습서에는 데이터베이스를 아직 필요 하지 않으므로 응용 프로그램입니다. 필요 하나 이제 단, 사용자 저장소에 대 한 합니다. 보겠습니다 만들어에 추가 된 후에 필요한 스키마를 `SqlMembershipProvider` 공급자 (2 단계 참조).

> [!NOTE]
> 이 자습서 시리즈 전체에서 사용할 것임을 [Microsoft SQL Server 2005 Express Edition](https://msdn.microsoft.com/sql/Aa336346.aspx) 응용 프로그램 테이블을 저장 하는 데이터베이스 및 `SqlMembershipProvider` 스키마입니다. 두 가지 이유로이 결정 되었습니다: 먼저 비용-인해 무료-Express Edition은 액세스할 때 가장의 버전 SQL Server 2005; 둘째, 웹 응용 프로그램에 직접 SQL Server 2005 Express Edition 데이터베이스를 배치할 수 있습니다 `App_Data` 데이터베이스 패키지 ZIP 파일 하나에 응용 프로그램을 함께 웹 하 고 별도 설치 지침 없이 다시 배포 하는 작업도 매우 간단 하므로 폴더 또는 구성 옵션을 지정 합니다. 비-Express Edition 버전의 SQL Server를 사용 하 여 수행 하려는 경우 자유롭게 있습니다. 단계를 거의 동일합니다. `SqlMembershipProvider` 스키마는 Microsoft SQL Server 2000의 모든 버전을 사용 하 여 작업 및 설정 합니다.

솔루션 탐색기에서 마우스 오른쪽 단추로 클릭는 `App_Data` 폴더 새 항목 추가 선택 합니다. (표시 되지 않는 경우는 `App_Data` 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭, ASP.NET 폴더 추가 선택 및 선택 된 프로젝트에서 폴더 `App_Data`.) 새 항목 추가 대화 상자에서 명명 된 새 SQL 데이터베이스를 추가 하도록 선택할 `SecurityTutorials.mdf`합니다. 이 자습서에서는 추가 된 `SqlMembershipProvider` 스키마 추가 만들겠습니다 후속 자습서에서는이 데이터베이스에 응용 프로그램 데이터를 캡처 테이블입니다.


[![App_Data 폴더에 SecurityTutorials.mdf 데이터베이스 라는 새 SQL 데이터베이스를 추가 합니다.](creating-the-membership-schema-in-sql-server-vb/_static/image2.png)](creating-the-membership-schema-in-sql-server-vb/_static/image1.png)

**그림 1**: 새 SQL 데이터베이스 이름 추가 `SecurityTutorials.mdf` 데이터베이스를 `App_Data` 폴더 ([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-vb/_static/image3.png))


데이터베이스를 추가 합니다 `App_Data` 폴더 자동으로 포함 데이터베이스 탐색기 보기에서. (비-Express Edition 버전의 Visual Studio 데이터베이스 탐색기 라고 서버 탐색기.) 데이터베이스 탐색기로 이동 하 고는 방금 추가 된 확장 `SecurityTutorials` 데이터베이스입니다. 데이터베이스 탐색기 화면에 표시 되지 않는다면 보기 메뉴 이동 및 데이터베이스 탐색기를 선택 하거나 Ctrl + Alt + S를 누릅니다. 그림 2에서 볼 수 있듯이 `SecurityTutorials` 데이터베이스가 비어-가 있는 테이블이 없는지, 없습니다 뷰 및 저장된 프로시저가 없습니다 포함 합니다.


[![현재 SecurityTutorials 데이터베이스가 비어 있습니다.](creating-the-membership-schema-in-sql-server-vb/_static/image5.png)](creating-the-membership-schema-in-sql-server-vb/_static/image4.png)

**그림 2**: 합니다 `SecurityTutorials` 데이터베이스가 현재 비어 ([클릭 하 여 큰 이미지 보기](creating-the-membership-schema-in-sql-server-vb/_static/image6.png))


## <a name="step-2-adding-thesqlmembershipproviderschema-to-the-database"></a>2 단계: 추가 된`SqlMembershipProvider`데이터베이스 스키마

`SqlMembershipProvider` 테이블, 뷰 및 저장된 프로시저를 사용자 저장소 데이터베이스를 설치할 특정 집합이 필요 합니다. 사용 하 여 이러한 필수 데이터베이스 개체를 추가할 수는 [ `aspnet_regsql.exe` 도구](https://msdn.microsoft.com/library/ms229862.aspx)합니다. 이 파일에는 `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\` 폴더입니다.

> [!NOTE]
> `aspnet_regsql.exe` 도구는 그래픽 사용자 인터페이스 및 명령줄 기능을 제공 합니다. 그래픽 인터페이스를 더 사용자 친화적 이며이 자습서에 맞게 살펴보겠습니다. 명령줄 인터페이스는 유용한 추가 `SqlMembershipProvider` 자동화 해야 하는 스키마, 스크립트 또는 테스트 시나리오를 자동화 된 빌드 같이 합니다.

합니다 `aspnet_regsql.exe` 도구는 추가 또는 제거 하는 데 사용 됩니다 *ASP.NET 응용 프로그램 서비스* 지정 된 SQL Server 데이터베이스에 있습니다. ASP.NET 응용 프로그램 서비스에 대 한 스키마를 포함 합니다 `SqlMembershipProvider` 및 `SqlRoleProvider`, 다른 ASP.NET 2.0 프레임 워크에 대 한 SQL 기반 공급자에 대 한 스키마와 함께 합니다. 두 개의 비트 정보를 제공 해야 합니다 `aspnet_regsql.exe` 도구:

- 추가 하거나 응용 프로그램 서비스를 제거 하려는 지 여부 및
- 데이터베이스를 추가 하거나 응용 프로그램 서비스 스키마를 제거 하려면

를 사용 하려면 데이터베이스에 대 한 라는 메시지가 표시 된 `aspnet_regsql.exe` 도구에서는 데이터베이스에 연결 하기 위한 보안 자격 증명에는 데이터베이스가 있는 서버 이름과 데이터베이스 이름을 제공 합니다. 비-Express Edition의 SQL Server를 사용 하는 경우 이미 알아야 할이 내용은 ASP.NET 웹 페이지를 통해 데이터베이스를 사용 하 여 작업 하는 경우 연결 문자열을 통해 제공 해야 동일한 정보를 그대로입니다. SQL Server 2005 Express Edition 데이터베이스를 사용 하는 경우 서버 및 데이터베이스 이름을 확인 하는 `App_Data` 폴더 것 인데, 좀 더 복잡 합니다.

다음 섹션에서는 SQL Server 2005 Express Edition 데이터베이스에 대 한 서버 및 데이터베이스 이름을 지정 하는 간단한 방법을 검사는 `App_Data` 폴더입니다. SQL Server 2005 Express Edition 자유롭게를 설치 하기 위해 바로 건너뛸를 사용 하지 않는 경우 응용 프로그램 서비스 섹션입니다.

### <a name="determining-the-server-and-database-name-for-a-sql-server-2005-express-edition-database-in-theappdatafolder"></a>SQL Server 2005 Express Edition 데이터베이스에 대 한 데이터베이스 이름과 서버를 결정 하는`App_Data`폴더

사용 하기 위해는 `aspnet_regsql.exe` 서버 및 데이터베이스 이름을 알아야 하는 도구입니다. 서버 이름은 `localhost\InstanceName`합니다. 대부분의 *InstanceName* 는 `SQLExpress`합니다. 그러나 SQL Server 2005 Express Edition를 수동으로 설치한 경우 (즉, 설치 하지 않은 자동으로 Visual Studio를 설치 하는 동안), 다른 인스턴스 이름을 선택 하는 것일 수 있습니다.

데이터베이스 이름은 결정할 좀 더 까다롭습니다. 데이터베이스를 `App_Data` 폴더에는 일반적으로 포함 하는 데이터베이스 이름이 있는 [전역적으로 고유 식별자](http://en.wikipedia.org/wiki/Globally_Unique_Identifier) 데이터베이스 파일의 경로 함께 합니다. 통해 응용 프로그램 서비스 스키마를 추가 하려면이 데이터베이스 이름을 확인 해야 `aspnet_regsql.exe`합니다.

데이터베이스 이름을 확인 하는 가장 쉬운 방법은 SQL Server Management Studio를 통해 검사할 됩니다. SQL Server Management Studio SQL Server 2005 데이터베이스를 관리 하기 위한 그래픽 인터페이스를 제공 하지만 Express Edition의 SQL Server 2005를 사용 하 여 제공 되지 않습니다. 좋은 소식은 [다운로드할 수 있습니다](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en) 무료 Express 버전의 SQL Server Management Studio를 합니다.

> [!NOTE]
> 바탕 화면에 설치 된 SQL Server 2005의 비-Express Edition 버전도 있는 경우 Management Studio의 전체 버전 가능성이 설치 됩니다. Express Edition에 대 한 아래 설명 된 대로 동일한 단계를 따라 데이터베이스 이름으로 확인 하려면 전체 버전을 사용할 수 있습니다.

Visual Studio 데이터베이스 파일에 따른 잠금을 닫았는지 확인 해야 하는 Visual Studio를 닫아 시작 합니다. 다음으로, SQL Server Management Studio를 시작 하 고 연결 하는 `localhost\InstanceName` SQL Server 2005 Express edition 데이터베이스입니다. 앞에서 설명한 대로 가능성이 인스턴스 이름이 `SQLExpress`합니다. 인증 옵션에 대 한 Windows 인증을 선택 합니다.


[![SQL Server 2005 Express Edition 인스턴스를 연결 합니다.](creating-the-membership-schema-in-sql-server-vb/_static/image8.png)](creating-the-membership-schema-in-sql-server-vb/_static/image7.png)

**그림 3**: SQL Server 2005 Express Edition 인스턴스를 연결할 ([큰 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-vb/_static/image9.png))


SQL Server 2005 Express Edition 인스턴스를 연결한 후 Management Studio는 데이터베이스, 보안 설정, 서버 개체 등에 대 한 폴더를 표시 합니다. 데이터베이스 탭을 확장 하는 경우 표시 됩니다는 합니다 `SecurityTutorials.mdf` 데이터베이스가 *하지* 데이터베이스 인스턴스에 등록 해야 데이터베이스를 먼저 연결 합니다.

데이터베이스 폴더 단추로 클릭 하 고 상황에 맞는 메뉴에서 연결을 선택 합니다. 이 데이터베이스 연결 대화 상자가 표시 됩니다. 여기에서 추가 단추 클릭로 이동는 `SecurityTutorials.mdf` 데이터베이스 및 확인을 클릭 합니다. 그림 4 후 데이터베이스 연결 대화 상자를 보여 줍니다.는 `SecurityTutorials.mdf` 데이터베이스를 선택 합니다. 그림 5에서는 데이터베이스에 연결 되 면 Management Studio 개체 탐색기를 보여 줍니다.


[![SecurityTutorials.mdf 데이터베이스 연결](creating-the-membership-schema-in-sql-server-vb/_static/image11.png)](creating-the-membership-schema-in-sql-server-vb/_static/image10.png)

**그림 4**: 연결 된 `SecurityTutorials.mdf` 데이터베이스 ([클릭 하 여 큰 이미지 보기](creating-the-membership-schema-in-sql-server-vb/_static/image12.png))


[![SecurityTutorials.mdf 데이터베이스 데이터베이스 폴더에 표시 됩니다.](creating-the-membership-schema-in-sql-server-vb/_static/image14.png)](creating-the-membership-schema-in-sql-server-vb/_static/image13.png)

**그림 5**: 합니다 `SecurityTutorials.mdf` 데이터베이스가 데이터베이스 폴더에 나타납니다 ([클릭 하 여 큰 이미지 보기](creating-the-membership-schema-in-sql-server-vb/_static/image15.png))


그림 5에서 알 수 있듯이는 `SecurityTutorials.mdf` 데이터베이스 대신 abstruse 이름이 있습니다. 변경해 보겠습니다 (및 쉽게 입력할)를 보다 기억 하기 쉬운 이름. 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고, 이름 바꾸기 상황에 맞는 메뉴에서 선택 하 고, 이름을 바꾸거나 `SecurityTutorialsDatabase`합니다. 파일 이름을 변경 하지 않습니다, 그리고 데이터베이스 이름만 사용 하 여 SQL server 자체를 식별 합니다.


[![SecurityTutorialsDatabase에 데이터베이스 이름을 바꾸려면](creating-the-membership-schema-in-sql-server-vb/_static/image17.png)](creating-the-membership-schema-in-sql-server-vb/_static/image16.png)

**그림 6**: 데이터베이스 이름 바꾸기 `SecurityTutorialsDatabase`([클릭 하 여 큰 이미지 보기](creating-the-membership-schema-in-sql-server-vb/_static/image18.png))


이 시점에 대 한 서버 및 데이터베이스 이름을 알고 합니다 `SecurityTutorials.mdf` 데이터베이스 파일: `localhost\InstanceName` 고 `SecurityTutorialsDatabase`각각. 통해 응용 프로그램 서비스를 설치할 준비가 됩니다.는 `aspnet_regsql.exe` 도구입니다.

### <a name="installing-the-application-services"></a>응용 프로그램 서비스를 설치합니다.

시작 하 여 `aspnet_regsql.exe` 도구, 시작 메뉴로 이동 하 고 실행을 선택 합니다. 입력 `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\aspnet_regsql.exe` 텍스트 상자에 확인을 클릭 합니다. Windows 탐색기를 사용 하 여 드릴 다운 적절 한 폴더를 두 번 클릭 수 또는 `aspnet_regsql.exe` 파일입니다. 어느 방법이 든 동일한 결과 net 됩니다.

실행 된 `aspnet_regsql.exe` 도구 명령줄 인수 없이 ASP.NET SQL Server 설치 마법사 그래픽 사용자 인터페이스를 시작 합니다. 마법사를 쉽게 추가 하거나 지정된 된 데이터베이스에 ASP.NET 응용 프로그램 서비스를 제거 합니다. 그림 7 에서처럼 마법사의 첫 번째 화면 도구의 용도 설명 합니다.


[![ASP.NET SQL Server 설치 마법사는 사용 하 여 멤버 자격 스키마를 추가 합니다.](creating-the-membership-schema-in-sql-server-vb/_static/image20.png)](creating-the-membership-schema-in-sql-server-vb/_static/image19.png)

**그림 7**: 멤버 자격 스키마를 추가 하는 ASP.NET SQL Server 설치 마법사를 사용 하면 사용 하 여 ([큰 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-vb/_static/image21.png))


응용 프로그램 서비스를 추가 하거나 제거 하려는 지 여부는 마법사의 두 번째 단계에서는 합니다. 테이블, 뷰 및 저장된 프로시저에 필요한 추가 하고자 하므로 `SqlMembershipProvider`, 응용 프로그램 서비스 옵션에 대 한 SQL Server 구성를 선택 합니다. 나중에 데이터베이스에서이 스키마를 제거 하려는 경우이 마법사를 다시 실행 하지만 대신 기존 데이터베이스 옵션에서 응용 프로그램 서비스 정보 제거를 선택 합니다.


[![선택 된 응용 프로그램 서비스 옵션에 대 한 SQL Server 구성](creating-the-membership-schema-in-sql-server-vb/_static/image23.png)](creating-the-membership-schema-in-sql-server-vb/_static/image22.png)

**그림 8**: 응용 프로그램 서비스 옵션에 대 한 SQL Server 구성 선택 ([큰 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-vb/_static/image24.png))


데이터베이스 정보를 묻는 메시지가 세 번째 단계: 서버 이름, 인증 정보 및 데이터베이스 이름입니다. 이 자습서와 함께 수행 하 고 추가한 경우 합니다 `SecurityTutorials.mdf` 데이터베이스를 `App_Data`에 연결 `localhost\InstanceName`, 및로 바꾸었습니다 `SecurityTutorialsDatabase`, 다음 값을 사용 합니다:

- 서버: `localhost\InstanceName`
- Windows 인증
- 데이터베이스: `SecurityTutorialsDatabase`


[![데이터베이스 정보를 입력 합니다.](creating-the-membership-schema-in-sql-server-vb/_static/image26.png)](creating-the-membership-schema-in-sql-server-vb/_static/image25.png)

**그림 9**: 데이터베이스 정보를 입력 ([큰 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-vb/_static/image27.png))


데이터베이스 정보를 입력 한 후 다음을 클릭 합니다. 마지막 단계는 단계를 요약 합니다. 응용 프로그램 서비스를 설치 하 고 다음 마법사를 완료 하려면 완료 하려면 다음을 클릭 합니다.

> [!NOTE]
> Management Studio를 사용 하는 데이터베이스 연결 및 데이터베이스 파일의 이름을 바꿀 경우에 Visual Studio를 다시 열어 하기 전에 Management Studio를 닫고 데이터베이스를 분리 하려면 해야 합니다. 분리 된 `SecurityTutorialsDatabase` 데이터베이스, 데이터베이스 이름을 마우스 오른쪽 단추로 클릭 하 고, 작업 메뉴에서 분리를 선택 합니다.

마법사를 완료 하면 Visual Studio 돌아가서 데이터베이스 탐색기로 이동 합니다. 테이블 폴더를 확장 합니다. 일련의 이름이 접두사로 시작 하는 테이블로 표시 `aspnet_`합니다. 마찬가지로, 뷰 및 저장된 프로시저의 다양 한 뷰 및 저장 프로시저 폴더에서 찾을 수 있습니다. 이러한 데이터베이스 개체 응용 프로그램 서비스 스키마를 구성 합니다. 3 단계에에서 있는 멤버 자격 및 역할 관련 데이터베이스 개체를 살펴보겠습니다.


[![데이터베이스에 추가 된 다양 한 테이블, 뷰 및 저장된 프로시저](creating-the-membership-schema-in-sql-server-vb/_static/image29.png)](creating-the-membership-schema-in-sql-server-vb/_static/image28.png)

**그림 10**:는 다양 한의 테이블, 뷰 및 저장 프로시저에 추가 된 데이터베이스 ([큰 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-vb/_static/image30.png))


> [!NOTE]
> `aspnet_regsql.exe` 도구의 그래픽 사용자 인터페이스는 전체 응용 프로그램 서비스 스키마를 설치 합니다. 하지만 실행 하는 경우 `aspnet_regsql.exe` 명령줄에서 지정할 수 있습니다 특정 응용 프로그램 서비스 구성 요소 설치 (또는 제거) 합니다. 따라서 테이블만 추가 하려는 경우 뷰, 저장 프로시저에 대 한 필요한 합니다 `SqlMembershipProvider` 및 `SqlRoleProvider` 공급자를 실행 `aspnet_regsql.exe` 명령줄에서. 또는 수동으로 실행할 수 있습니다 적절 한 T-SQL의 하위 집합에 사용 하 여 스크립트 만들기 `aspnet_regsql.exe`합니다. 이러한 스크립트에 있는 합니다 `WINDIR%\Microsoft.Net\Framework\v2.0.50727\` 와 같은 이름의 폴더 `InstallCommon.sql`, `InstallMembership.sql`, `InstallRoles.sql`를 `InstallProfile.sql`, `InstallSqlState.sql`등.

이 시점에서 필요한 데이터베이스 개체를 만들었습니다는 `SqlMembershipProvider`합니다. 그러나 해야 지시 멤버 자격 프레임 워크를 사용 하도록 합니다 `SqlMembershipProvider` (versus, 예를 들어, `ActiveDirectoryMembershipProvider`) 하 고는 `SqlMembershipProvider` 사용 해야는 `SecurityTutorials` 데이터베이스. 사용 하 여 어떤 공급자를 지정 하는 방법 및 4 단계에서에서 선택한 공급자의 설정을 사용자 지정 하는 방법을 살펴보겠습니다. 먼저, 방금 만든 데이터베이스 개체에서 자세히 살펴보겠습니다.

## <a name="step-3-a-look-at-the-schemas-core-tables"></a>3 단계: 스키마의 핵심 테이블 참조

ASP.NET 응용 프로그램에서 멤버 자격 및 역할 프레임 워크를 사용할 때 공급자가 구현 세부 사항은 캡슐화 됩니다. .NET Framework를 통해 이러한 프레임 워크를 사용 하 여 인터페이스는 우리가 자습서 향후 `Membership` 및 `Roles` 클래스입니다. 에서는 어떤 쿼리를 실행 하거나 어떤 테이블에서 수정와 같은 하위 수준 세부 정보를 사용 하 여 직접 관련이 않아도 이러한 높은 수준의 Api를 사용 하는 경우는 `SqlMembershipProvider` 고 `SqlRoleProvider`입니다.

이 점을 고려는 2 단계에서에서 만든 데이터베이스 스키마를 탐색 하지 않고 멤버 자격 및 역할 프레임 워크를 자신 있게 사용할 수 했습니다. 그러나 응용 프로그램 데이터를 저장할 테이블을 만들 때 사용자 또는 역할에 관련 된 엔터티를 만들 해야 있습니다. 사용 경험을 할 수 있도록 합니다 `SqlMembershipProvider` 및 `SqlRoleProvider` 스키마 외래 설정할 때 응용 프로그램 데이터 테이블 사이의 2 단계에서에서 만든 테이블 제약 조건 키입니다. 또한 특정 드문 경우에서 사용자와 상호 연결 해야 할 수 및 데이터베이스 수준에서 직접 저장소 역할 (통하지 않고 합니다 `Membership` 또는 `Roles` 클래스).

### <a name="partitioning-the-user-store-into-applications"></a>응용 프로그램에 사용자 저장소 분

멤버 자격 및 역할 프레임 워크는 단일 사용자 및 역할 저장소 다양 한 응용 프로그램 간에 공유할 수 있도록 설계 되었습니다. 멤버 자격 또는 역할 프레임 워크를 사용 하는 ASP.NET 응용 프로그램에 사용 하기 위해 어떤 응용 프로그램 파티션을 지정 해야 합니다. 즉, 여러 웹 응용 프로그램 같은 사용자 및 역할 저장소를 사용할 수 있습니다. 그림 11은 세 개의 응용 프로그램에 분할 하는 사용자 및 역할 저장소를 보여 줍니다: HRSite, CustomerSite, 및 SalesSite 합니다. 이러한 세 가지 웹 응용 프로그램 각각가 자신의 고유한 사용자 및 역할을 아직 모두 실제로 해당 사용자 계정 및 역할 정보 같은 데이터베이스 테이블에 저장 합니다.


[![여러 응용 프로그램 사용자 계정에 분할 될 수 있습니다.](creating-the-membership-schema-in-sql-server-vb/_static/image32.png)](creating-the-membership-schema-in-sql-server-vb/_static/image31.png)

**그림 11**: 사용자 계정 수 수 분할에서 여러 응용 프로그램 ([큰 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-vb/_static/image33.png))


`aspnet_Applications` 테이블은 이러한 파티션을 정의 합니다. 데이터베이스를 사용 하 여 사용자 계정 정보를 저장 하는 각 응용 프로그램은이 테이블의 행으로 표시 됩니다. `aspnet_Applications` 테이블에 열이 4: `ApplicationId`, `ApplicationName`, `LoweredApplicationName`, 및 `Description`합니다.`ApplicationId` 유형의 [ `uniqueidentifier` ](https://msdn.microsoft.com/library/ms187942.aspx) 테이블의 기본 키 이며 `ApplicationName` 각 응용 프로그램에 대 한 고유 사용자에 게 친숙 한 이름을 제공 합니다.

멤버 자격 및 역할에 관련 된 다른 테이블에 다시 연결 합니다 `ApplicationId` 필드에 `aspnet_Applications`입니다. 예를 들어 합니다 `aspnet_Users` 각 사용자 계정에 대 한 레코드를 포함 하는 테이블에는 `ApplicationId` 외래 키 필드;에 대 한 ditto는 `aspnet_Roles` 테이블입니다. `ApplicationId` 이러한 테이블의 필드에에서 사용자 계정을 응용 프로그램 파티션을 지정 또는 역할에 속합니다.

### <a name="storing-user-account-information"></a>사용자 계정 정보를 저장합니다.

두 테이블의 사용자 계정 정보를 저장 합니다. `aspnet_Users` 및 `aspnet_Membership`합니다. `aspnet_Users` 필수 사용자 계정 정보를 포함 하는 필드를 포함 하는 테이블입니다. 세 개의 열이 가장 관련 됩니다.

- `UserId`
- `UserName`
- `ApplicationId`

`UserId` 기본 키 (및 형식의 `uniqueidentifier`). `UserName` 형식의 `nvarchar(256)` 및 사용자의 자격 증명을 구성 하는 암호를 함께 합니다. (사용자의 암호에 저장 되는 `aspnet_Membership` 테이블입니다.) `ApplicationId` 사용자 계정에서 특정 응용 프로그램 연결 `aspnet_Applications`합니다. 복합 [ `UNIQUE` 제약 조건](https://msdn.microsoft.com/library/ms191166.aspx) 에 `UserName` 및 `ApplicationId` 열입니다. 이렇게 하면 각 사용자 지정된 응용 프로그램에서 고유 이름이 아직 동일한 있도록는 `UserName` 다른 응용 프로그램에서 사용할 수 있습니다.

`aspnet_Membership` 테이블 및와 같은 사용자의 암호, 전자 메일 주소, 마지막 로그인 날짜 및 시간 등의 추가 사용자 계정 정보를 포함 합니다. 레코드 간에 한 일 대응 됩니다 합니다 `aspnet_Users` 고 `aspnet_Membership` 테이블입니다. 이 관계에 의해 보장 되는 `UserId` 필드에 `aspnet_Membership`, 테이블의 기본 키로 사용 되는 합니다. 같은 합니다 `aspnet_Users` 테이블 `aspnet_Membership` 포함는 `ApplicationId` 이 정보는 특정 응용 프로그램 파티션에 연결 하는 필드입니다.

### <a name="securing-passwords"></a>암호를 보호 하기

암호 정보에 저장 되는 `aspnet_Membership` 테이블입니다. `SqlMembershipProvider` 암호는 다음 세 가지 기술 중 하나를 사용 하 여 데이터베이스에 저장 될 수 있습니다.

- **지우기** -암호를 일반 텍스트로 데이터베이스에 저장 됩니다. I 하지 않는 것이이 옵션을 사용 합니다. 데이터베이스 액세스 권한이 있는 사용자는 불만 품은 직원 또는 백도어가 해커가 수-데이터베이스가 손상 된 경우 모든 단일 사용자의 자격 증명을 수행 하기 위한 사항이 합니다.
- **해시** -암호는 단방향 해시 알고리즘 및 임의로 생성 된 솔트 값을 사용 하 여 해시 됩니다. 이 해시 된 값 (salt)와 함께 데이터베이스에 저장 됩니다.
- **암호화** -암호의 암호화 된 버전의 데이터베이스에 저장 됩니다.

사용 되는 암호 저장소 기술에 따라 달라 집니다 합니다 `SqlMembershipProvider` 에 지정 된 설정을 `Web.config`합니다. 사용자 지정에서 살펴볼 것은 `SqlMembershipProvider` 4 단계에서에서 설정 합니다. 기본 동작은 암호의 해시를 저장 하는 것입니다.

암호를 저장 하는 열은 `Password`하십시오 `PasswordFormat`, 및 `PasswordSalt`합니다. `PasswordFormat` 형식의 필드임 `int` 암호를 저장 하는 데 사용 되는 방법을 나타내는 값을 가지: 지우기에 대 한 0 Hashed 1; 2 암호화에 대 한 합니다. `PasswordSalt` 암호 저장소 기술 사용에 관계 없이 임의로 생성 된 문자열을 할당 변수의 `PasswordSalt` 암호의 해시를 계산할 때만 사용 됩니다. 마지막으로 `Password` 실제 암호 데이터를 포함 하는 열, 일반 텍스트 암호를 해시는 암호나 암호화 된 암호입니다.

표 1에서는 이러한 세 개의 열 모양을 다양 한 저장소 기법에 대 한 MySecret 암호를 저장 하는 경우를 보여 줍니다! .

| **저장소 기술&lt;\_o3a\_p /&gt;** | **암호&lt;\_o3a\_p /&gt;** | **PasswordFormat&lt;\_o3a\_p /&gt;** | **PasswordSalt&lt;\_o3a\_p /&gt;** |
| --- | --- | --- | --- |
| 지우기 | MySecret! | 0 | tTnkPlesqissc2y2SMEygA== |
| 해시 | 2oXm6sZHWbTHFgjgkGQsc2Ec9ZM= | 1 | wFgjUfhdUFOCKQiI61vtiQ== |
| 암호화 | 62RZgDvhxykkqsMchZ0Yly7HS6onhpaoCYaRxV8g0F4CW56OXUU3e7Inza9j9BKp | 2 | LSRzhGS/aa/oqAXGLHJNBw== |

**표 1**: 암호 MySecret 저장할 때 암호 관련 필드에 대 한 예제 값!

> [!NOTE]
> 사용 되는 해시 알고리즘을 특정 암호화 합니다 `SqlMembershipProvider` 설정에 따라 결정 됩니다는 `<machineKey>` 요소입니다. 이 구성 요소 3 단계에서에서 설명한 합니다 <a id="Tutorial3"> </a> [ *폼 인증 구성 및 고급 항목* ](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md) 자습서입니다.

### <a name="storing-roles-and-role-associations"></a>역할 및 역할 연결 저장

역할 프레임 워크에는 개발자를 역할 집합을 정의 하 고 어떤 역할에 속한 사용자를 지정할 수 있습니다. 두 테이블을 통해 데이터베이스에이 정보가 캡처됩니다: `aspnet_Roles` 고 `aspnet_UsersInRoles`입니다. 각 레코드는 `aspnet_Roles` 테이블에는 특정 응용 프로그램에 대 한 역할을 나타냅니다. 마찬가지로 합니다 `aspnet_Users` 테이블을 `aspnet_Roles` 테이블에 세 개의 열이 설명에 관련:

- `RoleId`
- `RoleName`
- `ApplicationId`

`RoleId` 기본 키 (및 형식의 `uniqueidentifier`). `RoleName`는 `nvarchar(256)` 형식입니다. 및 `ApplicationId` 사용자 계정에서 특정 응용 프로그램 연결 `aspnet_Applications`합니다. 복합 `UNIQUE` 제약 조건에는 `RoleName` 및 `ApplicationId` 열을 지정된 된 응용 프로그램에서 각 역할 이름이 고유한 지 확인 합니다.

`aspnet_UsersInRoles` 테이블 사용자 및 역할 간의 매핑을 역할도 합니다. 두 개의 열을 가지 `UserId` 및 `RoleId` -함께 복합 기본 키에 등록 하 고 있습니다.

## <a name="step-4-specifying-the-provider-and-customizing-its-settings"></a>4 단계: 공급자를 지정 하 고 해당 설정을 사용자 지정

모든 역할과 멤버 자격 프레임 워크-와 같은 공급자 모델을 지 원하는 프레임 워크 자체 구현 세부 정보 부족 및 대신 공급자 클래스는 책임을 위임 합니다. 멤버 자격 프레임 워크의 경우는 `Membership` 클래스는 사용자 계정을 관리 하기 위한 API를 정의 하지만 모든 사용자 저장소와 직접 상호 작용 하지 않습니다. 대신 합니다 `Membership` 클래스의 메서드 전달 요청 구성된 된 공급자-을 사용 합니다는 `SqlMembershipProvider`합니다. 경우 호출의 메서드 중 하나는 `Membership` 클래스, 멤버 자격 프레임 워크를 어떻게 확인 합니까에 대 한 호출을 위임 하는 `SqlMembershipProvider`?

합니다 `Membership` 클래스에는 [ `Providers` 속성](https://msdn.microsoft.com/library/system.web.security.membership.providers.aspx) 멤버 자격 프레임 워크에서 모든 사용 가능한 등록 된 공급자 클래스에 대 한 참조를 포함 하는 합니다. 등록 된 각 공급자는 연결 된 이름 및 형식에 있습니다. 이름에 특정 공급자를 참조 하는 친숙 한 방법을 제공 합니다 `Providers` 형식 공급자 클래스를 식별 하는 동안 컬렉션입니다. 또한 등록 된 각 공급자에는 구성 설정을 포함할 수 있습니다. 멤버 자격 프레임 워크에 대 한 구성 설정을 포함 `PasswordFormat` 고 `requiresUniqueEmail`, 다양 한 기타. 표 2에서 사용 하는 구성 설정의 전체 목록을 보려면를 `SqlMembershipProvider`입니다.

`Providers` 속성의 콘텐츠는 웹 응용 프로그램의 구성 설정을 통해 지정 됩니다. 기본적으로 모든 웹 응용 프로그램에 명명 된 공급자 `AspNetSqlMembershipProvider` 형식의 `SqlMembershipProvider`합니다. 이 기본 멤버 자격 공급자에 등록 되어 `machine.config` (위치한 `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG`):

[!code-xml[Main](creating-the-membership-schema-in-sql-server-vb/samples/sample1.xml)]

위의 태그로 합니다 [ `<membership>` 요소](https://msdn.microsoft.com/library/1b9hw62f.aspx) 하는 동안 멤버 자격 프레임 워크에 대 한 구성 설정을 정의 합니다 [ `<providers>` 자식 요소](https://msdn.microsoft.com/library/6d4936ht.aspx) 등록 된 지정 공급자입니다. 공급자를 추가할 수 있습니다 또는 사용 하 여 제거 합니다 [ `<add>` ](https://msdn.microsoft.com/library/whae3t94.aspx) 또는 [ `<remove>` ](https://msdn.microsoft.com/library/aykw9a6d.aspx) 요소를 사용 합니다 [ `<clear>` ](https://msdn.microsoft.com/library/t062y6yc.aspx) 현재 모두 제거 하는 요소 등록 된 공급자입니다. 위의 태그로 `machine.config` 명명 된 공급자를 추가 `AspNetSqlMembershipProvider` 형식의 `SqlMembershipProvider`합니다.

외에 합니다 `name` 및 `type` 특성을 `<add>` 다양 한 구성 설정에 대 한 값을 정의 하는 특성을 포함 하는 요소입니다. 표 2를 사용할 수 있는 목록 `SqlMembershipProvider`-특정 구성 설정을 함께 각각에 대해 설명 합니다.

> [!NOTE]
> 표 2에 명시 된 기본값에 정의 된 기본값 참조는 `SqlMembershipProvider` 클래스입니다. 것은 아닙니다 모든 구성 설정이 `AspNetSqlMembershipProvider` 의 기본 값에 해당 하는 `SqlMembershipProvider` 클래스입니다. 예를 들어, 멤버 자격 공급자를 지정 하지는 `requiresUniqueEmail` 기본값을 true로 설정 합니다. 그러나 합니다 `AspNetSqlMembershipProvider` 의 값을 명시적으로 지정 하 여이 기본값을 재정의 `false`합니다.

| **설정&lt;\_o3a\_p /&gt;** | **설명을&lt;\_o3a\_p /&gt;** |
| --- | --- |
| `ApplicationName` | 멤버 자격 프레임 워크는 단일 사용자 저장소에 여러 응용 프로그램에서 분할 될 수 있도록 회수 합니다. 이 설정은 멤버 자격 공급자에서 사용 하는 응용 프로그램 파티션의 이름을 나타냅니다. 경우이 값은 명시적으로 지정 되지, 설정 되어, 런타임, 응용 프로그램의 가상 루트 경로 값입니다. |
| `commandTimeout` | SQL 명령 시간 제한 값 (초)을 지정합니다. 기본값은 30입니다. |
| `connectionStringName` | 연결 문자열의 이름을 합니다 `<connectionStrings>` 사용자 저장소 데이터베이스에 연결 하는 데는 요소입니다. 이 값이 필요 합니다. |
| `description` | 등록 된 공급자에 대 한 친숙 한 설명을 제공합니다. |
| `enablePasswordRetrieval` | 사용자가 잊어버린된 암호를 검색할 수 있는지 여부를 지정 합니다. 기본값은 `false`입니다. |
| `enablePasswordReset` | 사용자가 암호를 재설정할 수 있는지 여부를 나타냅니다. 기본값은 `true`입니다. |
| `maxInvalidPasswordAttempts` | 지정 된 사용자 지정 하는 동안 발생할 수 있는 실패 한 로그인 시도의 최대 `passwordAttemptWindow` 사용자를 잠그기 전에 합니다. 기본값은 5입니다. |
| `minRequiredNonalphanumericCharacters` | 사용자의 암호에 표시 되어야 하는 영숫자가 아닌 문자의 최소 수입니다. 이 값은 0에서 128; 사이 여야 합니다. 기본값은 1입니다. |
| `minRequiredPasswordLength` | 암호에 필요한 문자의 최소 수입니다. 이 값은 0에서 128; 사이 여야 합니다. 기본값은 7입니다. |
| `name` | 등록 된 공급자의 이름입니다. 이 값이 필요 합니다. |
| `passwordAttemptWindow` | 분 수의 입력 시도가 추적 되는 로그인 하지 못했습니다. 사용자는 잘못 된 로그인 자격 증명을 제공 하는 경우 `maxInvalidPasswordAttempts` 잠긴을이 번 창을 지정 합니다. 기본값은 10입니다. |
| `PasswordFormat` | 암호 저장 형식: `Clear`, `Hashed`, 또는 `Encrypted`합니다. 기본값은 `Hashed`입니다. |
| `passwordStrengthRegularExpression` | 제공 하는 경우 자신의 암호를 변경 하는 경우 또는 새 계정을 만들 때 사용자가 선택한 암호의 강도 평가 하려면 정규식이 사용 됩니다. 기본값은 빈 문자열입니다. |
| `requiresQuestionAndAnswer` | 사용자 검색 또는 암호를 재설정할 때 자신의 보안 질문에 대답 해야 하는지 여부를 지정 합니다. 기본값은 `true`입니다. |
| `requiresUniqueEmail` | 지정 된 응용 프로그램 파티션의 모든 사용자 계정에 고유한 전자 메일 주소를이 있어야 하는지 여부를 나타냅니다. 기본값은 `true`입니다. |
| `type` | 공급자의 형식을 지정합니다. 이 값이 필요 합니다. |

**표 2**: 멤버 자격 및 `SqlMembershipProvider` 구성 설정

외에 `AspNetSqlMembershipProvider`, 다른 멤버 자격 공급자와 유사한 태그를 추가 하 여 응용 프로그램으로 등록 될 수도 있습니다는 `Web.config` 파일입니다.

> [!NOTE]
> 역할 framework 거의 동일한 방식:에 기본 등록 된 역할 공급자가 `machine.config` 등록된 된 공급자에는 응용 프로그램 별로 사용자 지정할 수 있습니다 및 `Web.config`합니다. 이후 자습서 역할 프레임 워크 및 해당 구성 태그 자세히 검토할 것입니다.

### <a name="customizing-thesqlmembershipprovidersettings"></a>사용자 지정을`SqlMembershipProvider`설정

기본값 `SqlMembershipProvider` (`AspNetSqlMembershipProvider`)에 해당 `connectionStringName` 특성이 설정 `LocalSqlServer`합니다. 같은 합니다 `AspNetSqlMembershipProvider` 공급자, 연결 문자열 이름만 `LocalSqlServer` 에 정의 된 `machine.config`합니다.

[!code-xml[Main](creating-the-membership-schema-in-sql-server-vb/samples/sample2.xml)]

이 연결 문자열 정의 SQL 2005 Express Edition 데이터베이스에 있는 알 수 있듯이 | DataDirectory|aspnetdb.mdf 합니다. 문자열 | DataDirectory | 가리키도록 런타임 시 변환 되는 `~/App_Data/` 디렉터리 이므로 데이터베이스 경로 | 변환 DataDirectory|aspnetdb.mdf `~/App_Data` / `aspnet.mdf`합니다.

우리가 하는 경우 응용 프로그램의 멤버 자격 공급자 정보를 지정 하지는 않았습니다 `Web.config` 파일을 응용 프로그램에 등록 하는 기본 멤버 자격 공급자를 사용 하 여 `AspNetSqlMembershipProvider`입니다. 경우는 `~/App_Data/aspnet.mdf` 데이터베이스가 존재 하지 않습니다, ASP.NET 런타임에서 자동으로 만들고 응용 프로그램 서비스 스키마를 추가 합니다. 그러나 사용 하려고 하지 않습니다 합니다 `aspnet.mdf` 사용 하고자 하는 대신 하므로 데이터베이스를 `SecurityTutorials.mdf` 2 단계에서에서 만든 데이터베이스입니다. 이 수정이 두 가지 방법 중 하나로 수행할 수 있습니다.

- <strong>값을 지정 합니다</strong><strong>`LocalSqlServer`</strong><strong>연결 문자열 이름이</strong><strong>`Web.config`</strong><strong>합니다.</strong> 덮어쓰는 방법으로 `LocalSqlServer` 연결 문자열 이름 값 `Web.config`를 등록 하는 기본 멤버 자격 공급자를 사용할 수 있습니다 (`AspNetSqlMembershipProvider`) 올바르게 작동 하도록는 `SecurityTutorials.mdf` 데이터베이스. 지정 된 구성 설정을 사용 하 여는 경우이 방법이 괜찮습니다 `AspNetSqlMembershipProvider`합니다. 이 기술에 대 한 자세한 내용은 참조 하세요. [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 블로그 게시물 [사용 하 여 SQL Server 2000 또는 SQL Server 2005로 ASP.NET 2.0 응용 프로그램 서비스 구성](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)합니다.
- <strong>형식의 새 등록 된 공급자를 추가</strong><strong>`SqlMembershipProvider`</strong><strong>구성 하 고 해당</strong><strong>`connectionStringName`</strong><strong>를가리키도록설정</strong> <strong>`SecurityTutorials.mdf`</strong> <strong>데이터베이스입니다.</strong> 이 방법은 데이터베이스 연결 문자열 외에도 다른 구성 속성을 사용자 지정 하려는 시나리오에서 유용 합니다. 내 프로젝트 있습니까 항상이 접근 방식을 사용의 유연성과 가독성 때문입니다.

참조 하는 새 등록 된 공급자를 추가 하기 전에 `SecurityTutorials.mdf` 데이터베이스에 먼저 추가 해야에 적절 한 연결 문자열 값을 `<connectionStrings>` 섹션 `Web.config`합니다. 라는 새 연결 문자열을 추가 하는 다음과 같은 태그가 `SecurityTutorialsConnectionString` SQL Server 2005 Express Edition을 참조 하는 `SecurityTutorials.mdf` 데이터베이스에 `App_Data` 폴더입니다.

[!code-xml[Main](creating-the-membership-schema-in-sql-server-vb/samples/sample3.xml)]

> [!NOTE]
> 대체 데이터베이스 파일을 사용 하는 경우 필요에 따라 연결 문자열을 업데이트 합니다. 올바른 연결 문자열을 형성 하는 방법은 참조 [ConnectionStrings.com](http://www.connectionstrings.com/)합니다.

다음으로, 다음 멤버 자격 구성 태그를 추가 합니다 `Web.config` 파일입니다. 이 태그 라는 새 공급자를 등록 `SecurityTutorialsSqlMembershipProvider`합니다.

[!code-xml[Main](creating-the-membership-schema-in-sql-server-vb/samples/sample4.xml)]

등록 하는 것 외에도 `SecurityTutorialsSqlMembershipProvider` 공급자, 위의 태그는 정의 `SecurityTutorialsSqlMembershipProvider` 기본 공급자로 (통해를 `defaultProvider` 특성을 `<membership>` 요소). 멤버 자격 프레임 워크에서 여러 등록 된 공급자를 가질 수 있다는 사실을 기억 하십시오. 이후 `AspNetSqlMembershipProvider` 에서 첫 번째 공급자로 등록 된 `machine.config`,에서는 명시 하지 않는 한 기본 공급자로 사용 됩니다.

현재 응용 프로그램에 두 명의 등록 된 공급자: `AspNetSqlMembershipProvider` 고 `SecurityTutorialsSqlMembershipProvider`입니다. 등록 있으 나 먼저를 `SecurityTutorialsSqlMembershipProvider` 공급자에서는 수 선택을 취소 한 모든 이전에 추가 하 여 공급자를 등록을 [ `<clear />` 요소](https://msdn.microsoft.com/library/t062y6yc.aspx) 직전 우리의 `<add>` 요소입니다. 지울는이 `AspNetSqlMembershipProvider` 이므로 등록 된 공급자의 목록에서를 `SecurityTutorialsSqlMembershipProvider` 만 등록 된 멤버 자격 공급자는 것입니다. 이 방법을 사용 했습니다 경우 표시 해야 하지는 `SecurityTutorialsSqlMembershipProvider` 기본 공급자 이후에 것이 유일한 등록 된 멤버 자격 공급자입니다. 사용 하 여 대 한 자세한 내용은 `<clear />`를 참조 하세요 [사용 하 여 `<clear />` 공급자 추가](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx)합니다.

유의 합니다 `SecurityTutorialsSqlMembershipProvider`의 `connectionStringName` 는 방금 추가 된 참조를 설정 `SecurityTutorialsConnectionString` 하 고 연결 문자열 이름에 해당 `applicationName` SecurityTutorials 값으로 설정 되었습니다. 또한 합니다 `requiresUniqueEmail` 설정 되었습니다 `true`합니다. 다른 모든 구성 옵션의 값에 동일 `AspNetSqlMembershipProvider`합니다. 언제 든 지 원하는 경우 여기에서 모든 구성을 수정할 수 있도록 합니다. 예를 들어 하나 대신 두 개의 영숫자가 아닌 문자를 요구 하거나 7 대신 8 자 암호 길이 늘려 암호 강도 강화할 수 있습니다.

> [!NOTE]
> 멤버 자격 프레임 워크는 단일 사용자 저장소에 여러 응용 프로그램에서 분할 될 수 있도록 회수 합니다. 멤버 자격 공급자의 `applicationName` 설정은 사용자 저장소를 사용 하 여 작업 하는 경우 공급자를 사용 하 여 응용 프로그램을 나타냅니다. 값 명시적으로 설정 하는 것이 중요 합니다 `applicationName` 구성 설정 때문에 경우는 `applicationName` 명시적으로 설정 하지 않으면 런타임 시 웹 응용 프로그램의 가상 루트 경로에 할당 됩니다. 이 정상적으로 응용 프로그램의 가상 루트 경로 변경 하지 않습니다 하지만 응용 프로그램을 다른 경로로 이동 하는 경우는 `applicationName` 설정이 너무 변경 됩니다. 이 경우 멤버 자격 공급자는 이전에 사용한 것 보다 다양 한 응용 프로그램 파티션 작업 시작 됩니다. 이동 하기 전에 만든 사용자 계정을 다른 응용 프로그램 파티션에 있고 해당 사용자는 더 이상 사이트에 로그인 할 수 없습니다. 이 문제에 대 한 자세한 논의 참조 하세요 [항상 설정 합니다 `applicationName` 속성 때 구성 ASP.NET 2.0 멤버 자격 및 기타 공급자](https://weblogs.asp.net/scottgu/443634)합니다.

## <a name="summary"></a>요약

이 시점에서 구성 된 응용 프로그램 서비스를 사용 하 여 데이터베이스 했습니다 (`SecurityTutorials.mdf`)에 멤버 자격 프레임 워크를 사용 하도록 웹 응용 프로그램 구성 및를 `SecurityTutorialsSqlMembershipProvider` 방금 등록 공급자. 이 등록 된 공급자 형식입니다 `SqlMembershipProvider` 있고 해당 `connectionStringName` 적절 한 연결 문자열에 설정 됩니다 (`SecurityTutorialsConnectionString`) 및 해당 `applicationName` 값이 명시적으로 설정 합니다.

이제 응용 프로그램에서 멤버 자격 프레임 워크를 사용할 준비가 되었습니다. 다음 자습서에서 새 사용자 계정을 만드는 방법을 살펴보겠습니다. 사용자 인증, 사용자 기반 권한 부여를 수행 하 고 데이터베이스에 추가 사용자 관련 정보를 저장 살펴봅니다는 다음과 같습니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [항상 설정 된 `applicationName` 속성 때 구성 ASP.NET 2.0 멤버 자격 및 기타 공급자](https://weblogs.asp.net/scottgu/443634)
- [ASP.NET 2.0 구성 응용 프로그램 서비스를 사용 하 여 SQL Server 2000 또는 SQL Server 2005](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)
- [SQL Server Management Studio Express Edition 다운로드](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)
- [ASP.NET 2.0 검사 s 멤버 자격, 역할 및 프로필](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [`<add>` 멤버 자격 공급자에 대 한 요소](https://msdn.microsoft.com/library/whae3t94.aspx)
- [`<membership>` 요소](https://msdn.microsoft.com/library/1b9hw62f.aspx)
- [`<providers>` 멤버 자격에 대 한 요소](https://msdn.microsoft.com/library/6d4936ht.aspx)
- [사용 하 여 `<clear />` 공급자 추가](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx)
- [직접 작업을 `SqlMembershipProvider`](http://aspnet.4guysfromrolla.com/articles/091207-1.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>이 자습서에 포함 된 항목의 비디오 교육

- [ASP.NET 멤버 자격 이해](../../../videos/authentication/understanding-aspnet-memberships.md)
- [멤버 자격 스키마와 함께 작동하도록 SQL 구성](../../../videos/authentication/configuring-sql-to-work-with-membership-schemas.md)
- [기본 멤버 자격 스키마에서 멤버 자격 설정 변경](../../../videos/authentication/changing-membership-settings-in-the-default-membership-schema.md)

### <a name="about-the-author"></a>저자 소개

Scott Mitchell, 여러 ASP/ASP.NET 책의 저자 이자 4GuysFromRolla.com의 설립자 이며 1998 Microsoft 웹 기술을 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는  *[Sams 설명 직접 ASP.NET 2.0 24 시간 동안의](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 합니다. Scott에 도달할 수 있습니다 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 통하거나 저자의 블로그 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Alicja Maziarz 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)합니다.

> [!div class="step-by-step"]
> [이전](storing-additional-user-information-cs.md)
> [다음](creating-user-accounts-vb.md)
