---
uid: web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs
title: SQL Server (C#)에서 멤버 자격 스키마 만들기 | Microsoft Docs
author: rick-anderson
description: 이 자습서는 SqlMembershipProvider 사용 하려면 데이터베이스에 필요한 스키마를 추가 하기 위한 기술을 검사 하 여 시작 합니다. 그런 다음, 우리 wi...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/18/2008
ms.topic: article
ms.assetid: b4ac129d-1b8e-41ca-a38f-9b19d7c7bb0e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs
msc.type: authoredcontent
ms.openlocfilehash: 4fa0476ca8336b56340dd177f9816acbe015ef7d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="creating-the-membership-schema-in-sql-server-c"></a>SQL Server (C#)에서 멤버 자격 스키마 만들기
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_04_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial04_MembershipSetup_cs.pdf)

> 이 자습서는 SqlMembershipProvider 사용 하려면 데이터베이스에 필요한 스키마를 추가 하기 위한 기술을 검사 하 여 시작 합니다. 그런 다음, 스키마에는 키 테이블을 확인 하 고 목적 및 중요도 설명 합니다. 이 자습서를 살펴보면 ASP.NET 응용 프로그램 구성원 프레임 워크를 사용 해야 하는 공급자를 구별 하는 방법으로 끝납니다.


## <a name="introduction"></a>소개

폼 인증을 사용 하 여 웹 사이트 방문자를 식별 하려면 검사 이전 두 자습서입니다. 폼 인증 프레임 워크를 통해 개발자가 인증 티켓을 사용 하 여 페이지 방문할 때마다 기억 하 고 사용자 웹 사이트에 로그인 할 수 있습니다. `FormsAuthentication` 클래스 방문자의 쿠키를 추가 하 고 티켓 생성 메서드가 포함 됩니다. `FormsAuthenticationModule` 들어오는 모든 요청을 검사 하 고, 사용자에 게 유효한 인증 티켓을 만들고와 연결 된 `GenericPrincipal` 및 `FormsIdentity` 개체를 현재 요청 합니다. 폼 인증은 단순히에 및 사용자의 id를 확인 하려면 해당 티켓을 구문 분석 하는 후속 요청에서 로그인 할 때 방문자에 인증 티켓을 부여 하기 위한 메커니즘입니다. 여전히 사용자 계정을 지원 하도록 웹 응용 프로그램에 대 한 하는 사용자 저장소를 구현 하 고 자격 증명 유효성 검사, 새 사용자 및 다른 사용자 계정 관련 작업의 방대한 등록 기능을 추가 해야 합니다.

ASP.NET 2.0 이전 개발자가 이러한 사용자 계정 관련 작업을 모두 구현 하는 데 필요한 후크에 있었습니다. 다행히 ASP.NET 팀이 이러한 단점을 인식 하 고 ASP.NET 2.0과 함께 구성원 프레임 워크가 추가 되었습니다. 멤버 자격 프레임 워크는.NET Framework의 핵심 사용자 계정 관련 작업을 수행 하기 위한 프로그래밍 인터페이스를 제공 하는 클래스의 집합입니다. 이 프레임 워크 위에 빌드된는 [공급자 모델](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx), 개발자가 사용자 지정된 된 구현 하는 표준화 된 API에 연결할 수 있습니다.

에 설명 된 대로 <a id="Tutorial1"> </a> [ *보안 기본 사항 및 ASP.NET 지원* ](../introduction/security-basics-and-asp-net-support-cs.md) 자습서에서는 두 명의 기본 제공 멤버 자격 공급자와 함께 제공 되는.NET Framework: [ `ActiveDirectoryMembershipProvider` ](https://msdn.microsoft.com/library/system.web.security.activedirectorymembershipprovider.aspx) 및 [ `SqlMembershipProvider` ](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx)합니다. 이름에서 알 수 있듯이 `SqlMembershipProvider` 사용자 저장소로 Microsoft SQL Server 데이터베이스를 사용 합니다. 응용 프로그램에서이 공급자를 사용 하려면 공급자를 저장소로 사용 하도록 데이터베이스를 해야 합니다. 짐작할 수는 `SqlMembershipProvider` 사용자 저장소 데이터베이스의 특정 데이터베이스 테이블, 뷰 및 저장된 프로시저를 예상 합니다. 선택한 데이터베이스에이 필요한 스키마를 추가 해야 합니다.

이 자습서를 사용 하려면 데이터베이스에 필요한 스키마를 추가 하기 위한 기술을 검사 하 여 시작 된 `SqlMembershipProvider`합니다. 그런 다음, 스키마에는 키 테이블을 확인 하 고 목적 및 중요도 설명 합니다. 이 자습서를 살펴보면 ASP.NET 응용 프로그램 구성원 프레임 워크를 사용 해야 하는 공급자를 구별 하는 방법으로 끝납니다.

이제 시작 하겠습니다.

## <a name="step-1-deciding-where-to-place-the-user-store"></a>1 단계: 사용자 저장소의 배치 위치 결정

ASP.NET 응용 프로그램의 데이터는 일반적으로 다양 한 데이터베이스의 테이블에에서 저장 됩니다. 구현 하는 경우는 `SqlMembershipProvider` 데이터베이스 스키마에는 응용 프로그램 데이터와 동일한 데이터베이스 또는 대체 데이터베이스에서 멤버 자격 스키마를 배치할지 여부를 결정 해야 합니다.

다음과 같은 이유로 응용 프로그램 데이터와 동일한 데이터베이스에서 멤버 자격 스키마를 찾는 것이 좋습니다.

- **유지 관리 용이성** 하나의 데이터베이스에 데이터가 있는 캡슐화 된 응용 프로그램을 보다 쉽게 이해 하 고 유지 관리 보다는 두 개의 별도 데이터베이스 응용 프로그램을 배포할 수 있습니다.
- **관계 무결성** 응용 프로그램 테이블 것으로 동일한 데이터베이스에 멤버 자격 관련 테이블을 배치 하 여 설정할 수는 [foreign key 제약 조건을](http://en.wikipedia.org/wiki/Foreign_key) 의 기본 키 간에 멤버 자격 관련 테이블 및 관련된 응용 프로그램 테이블입니다.

개별 데이터베이스에 사용자 저장소 및 응용 프로그램 데이터를 분리 하면 여기 여러 응용 프로그램을 별도 데이터베이스를 사용 하 여 각 하지만 일반 사용자 저장소를 공유 해야 합니다.

### <a name="creating-a-database"></a>데이터베이스 만들기

두 번째 자습서 이후 구축한에서는 응용 프로그램에 데이터베이스를 아직 필요 하지 않습니다. 하지만 필요 하나 이제 사용자 저장소에 대 한 합니다. 보겠습니다 만들고 하 여 추가 된 후에 필요한 스키마는 `SqlMembershipProvider` 공급자 (2 단계 참조).

> [!NOTE]
> 이 자습서 시리즈를 사용 합니다는 [Microsoft SQL Server 2005 Express Edition](https://msdn.microsoft.com/sql/Aa336346.aspx) 를 응용 프로그램 테이블을 저장할 데이터베이스 및 `SqlMembershipProvider` 스키마입니다. 두 가지 이유로이 결정 했지만: 먼저-비용으로 인해 무료 Express Edition은 가장 때 액세스할 수 있는 버전의 SQL Server 2005; 둘째, SQL Server 2005 Express Edition 데이터베이스 안에 있을 수 직접 웹 응용 프로그램의 `App_Data` 패키지는 데이터베이스와 웹 응용 프로그램 시작 함께 하나의 ZIP 파일에 하 고 별도 설치 지침 없이 다시 배포 하려면을 쉽게 만드는 폴더 또는 구성 옵션을 지정 합니다. 비-Express Edition 버전의 SQL Server를 사용 하 여 수행 하려는 경우 자유롭게 합니다. 단계는 거의 동일 합니다. `SqlMembershipProvider` 스키마는 모든 버전의 Microsoft SQL Server 2000 사용 및 최대 합니다.


솔루션 탐색기에서 마우스 오른쪽 단추로 클릭는 `App_Data` 폴더를 새 항목 추가를 선택 합니다. (표시 되지 않으면는 `App_Data` 폴더를 프로젝트 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 ASP.NET 폴더 추가 선택 하 고 선택 `App_Data`.) 새 항목 추가 대화 상자에서 명명 된 새 SQL 데이터베이스를 추가 하도록 선택 `SecurityTutorials.mdf`합니다. 추가 될이 자습서는 `SqlMembershipProvider` 추가 만듭니다 후속 자습서;이 데이터베이스에 스키마를 응용 프로그램 데이터를 캡처하는 테이블입니다.


[![App_Data 폴더에 SecurityTutorials.mdf 데이터베이스 라는 새 SQL 데이터베이스를 추가 합니다.](creating-the-membership-schema-in-sql-server-cs/_static/image2.png)](creating-the-membership-schema-in-sql-server-cs/_static/image1.png)

**그림 1**: 새 SQL 데이터베이스 라는 추가 `SecurityTutorials.mdf` 데이터베이스는 `App_Data` 폴더 ([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-cs/_static/image3.png))


에 데이터베이스에 추가 `App_Data` 폴더 데이터베이스 탐색기 보기에서 포함 자동으로 됩니다. (비-Express Edition 버전의 Visual Studio에서 데이터베이스 탐색기 라고 서버 탐색기.) 데이터베이스 탐색기로 이동 하 고는 방금 추가 된 확장 `SecurityTutorials` 데이터베이스입니다. 화면에 데이터베이스 탐색기를 표시 되지 않으면 보기 메뉴로 이동 하 고 데이터베이스 탐색기를 선택 하거나 Ctrl + Alt + S를 적중 합니다. 그림 2에서 볼 수 있듯이 `SecurityTutorials` 데이터베이스가 비어-는 테이블이, 보기가 없습니다 및 저장된 프로시저가 없습니다.


[![현재 SecurityTutorials 데이터베이스가 비어 있습니다.](creating-the-membership-schema-in-sql-server-cs/_static/image5.png)](creating-the-membership-schema-in-sql-server-cs/_static/image4.png)

**그림 2**:는 `SecurityTutorials` 데이터베이스 현재 비어 있습니다 ([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-cs/_static/image6.png))


## <a name="step-2-adding-thesqlmembershipproviderschema-to-the-database"></a>2 단계: 추가 된`SqlMembershipProvider`데이터베이스에 대 한 스키마

`SqlMembershipProvider` 테이블, 뷰 및 저장된 프로시저는 사용자 저장소 데이터베이스에 설치 되어야 하는 특정 집합이 필요 합니다. 사용 하 여 이러한 필요한 데이터베이스 개체를 추가할 수는 [ `aspnet_regsql.exe` 도구](https://msdn.microsoft.com/library/ms229862.aspx)합니다. 이 파일은 `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\` 폴더입니다.

> [!NOTE]
> `aspnet_regsql.exe` 명령줄 기능과 그래픽 사용자 인터페이스 도구를 제공 합니다. 그래픽 인터페이스 더 많은 사용자에 게 친숙 며이 자습서에 맞게 살펴보겠습니다. 명령줄 인터페이스는 유용 추가 `SqlMembershipProvider` 자동화 해야 하는 스키마, 스크립트 또는 테스트 시나리오를 자동화 된 빌드와 같이 합니다.


`aspnet_regsql.exe` 도구 추가 또는 제거 하는 데 사용 됩니다 *ASP.NET 응용 프로그램 서비스* 지정 된 SQL Server 데이터베이스에 있습니다. 에 대 한 스키마를 포함 하는 ASP.NET 응용 프로그램 서비스는 `SqlMembershipProvider` 및 `SqlRoleProvider`, 다른 ASP.NET 2.0 프레임 워크에 대 한 SQL 기반 공급자에 대 한 스키마와 함께 합니다. 두 비트에 정보를 제공 해야는 `aspnet_regsql.exe` 도구:

- 응용 프로그램 서비스를 추가 또는 제거할 원하는 여부 및
- 데이터베이스를 추가 하거나 응용 프로그램 서비스 스키마를 제거 하려면

을 사용 하려면 데이터베이스에 대 한 메시지를 표시에 `aspnet_regsql.exe` 도구는 데이터베이스에 연결 하기 위한 보안 자격 증명에는 데이터베이스가 있는 서버 이름과 데이터베이스 이름을 제공 하 라는 메시지가 나타납니다. 비-Express Edition의 SQL Server를 사용 하는 동일한 정보를 ASP.NET 웹 페이지를 통해 데이터베이스 작업을 수행 하는 경우 연결 문자열을 통해 제공 해야 하는 대로 이미이 정보를을 알고 있어야 합니다. 하지만 SQL Server 2005 Express Edition 데이터베이스를 사용 하는 경우 서버 및 데이터베이스 이름을 확인 하 고 `App_Data` 폴더 약간 더 개입 됩니다.

다음 섹션에서는 SQL Server 2005 Express Edition 데이터베이스에 대 한 서버 및 데이터베이스 이름을 지정 하는 간단한 방법의 검사는 `App_Data` 폴더입니다. SQL Server 2005 Express Edition 자유롭게 설치를 사용 하지 않는 경우 응용 프로그램 서비스 섹션.

### <a name="determining-the-server-and-database-name-for-a-sql-server-2005-express-edition-database-in-theappdatafolder"></a>서버 및 SQL Server 2005 Express Edition 데이터베이스에 대 한 데이터베이스 이름을 확인 하 고`App_Data`폴더

사용 하려면는 `aspnet_regsql.exe` 서버 및 데이터베이스 이름을 알아야 하는 도구입니다. 서버 이름은 `localhost\InstanceName`합니다. 가장 가능성이 높은 *InstanceName* 은 `SQLExpress`합니다. 그러나 수동으로 SQL Server 2005 Express Edition을 설치 하는 경우 (즉, 설치 하지 않은 것 자동으로 Visual Studio를 설치 하는 동안), 다른 인스턴스 이름을 선택 하는 것일 수 있습니다.

데이터베이스 이름이 결정 하는 조금 더 복잡 합니다. 데이터베이스에 `App_Data` 폴더에는 일반적으로 포함 하는 데이터베이스 이름을 가질는 [전역 고유 식별자](http://en.wikipedia.org/wiki/Globally_Unique_Identifier) 데이터베이스 파일의 경로 함께 합니다. 통해 응용 프로그램 서비스 스키마를 추가 하려면이 데이터베이스 이름을 확인 해야 `aspnet_regsql.exe`합니다.

데이터베이스 이름을 확인 하는 가장 쉬운 방법은 SQL Server Management Studio를 통해 검사할 수는 있습니다. SQL Server Management Studio는 SQL Server 2005 데이터베이스를 관리 하기 위한 그래픽 인터페이스를 제공 하지만 Express 버전의 SQL Server 2005 함께 제공 되지 않습니다. 다행 스럽게도 [다운로드할 수 있습니다](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en) 무료 Express 버전의 SQL Server Management Studio 합니다.

> [!NOTE]
> 비-Express Edition 버전 바탕 화면에 설치 된 SQL Server 2005의 경우 Management Studio의 전체 버전 가능성이 설치 됩니다. Express Edition에 대 한 아래 설명 된 대로 동일한 단계에 따라 데이터베이스 이름으로 확인 하려면 정식 버전을 사용할 수 있습니다.


데이터베이스 파일에 Visual Studio에 의해 적용 된 모든 잠금을 닫혔는지 확인 하는 Visual Studio를 닫고 시작 합니다. 다음으로, SQL Server Management Studio를 시작 하 고 연결할는 `localhost\InstanceName` SQL Server 2005 Express Edition에 대 한 데이터베이스입니다. 앞에서 설명한 대로 될 확률이 인스턴스 이름이 `SQLExpress`합니다. 인증 옵션에 대 한 Windows 인증을 선택 합니다.


[![SQL Server 2005 Express Edition 인스턴스는에 연결](creating-the-membership-schema-in-sql-server-cs/_static/image8.png)](creating-the-membership-schema-in-sql-server-cs/_static/image7.png)

**그림 3**: SQL Server 2005 Express Edition 인스턴스는에 연결 ([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-cs/_static/image9.png))


에 SQL Server 2005 Express Edition 인스턴스를 연결한 후 Management Studio는 데이터베이스, 보안 설정, 서버 개체 등에 대 한 폴더를 표시 합니다. 데이터베이스 탭을 확장 하는 경우 확인 하 게는 `SecurityTutorials.mdf` 데이터베이스가 *하지* 먼저 데이터베이스를 연결 해야 데이터베이스 인스턴스-에 등록 합니다.

데이터베이스 폴더 단추로 클릭 하 고 상황에 맞는 메뉴에서 연결을 선택 합니다. 이 데이터베이스 연결 대화 상자를 표시 됩니다. 여기에서 추가 단추를 찾은 `SecurityTutorials.mdf` 데이터베이스, 확인을 클릭 합니다. 그림 4 후 데이터베이스 연결 대화 상자를 보여 줍니다.는 `SecurityTutorials.mdf` 데이터베이스를 선택 합니다. 그림 5 데이터베이스가 성공적으로 연결 된 후 Management Studio 개체 탐색기를 보여줍니다.


[![SecurityTutorials.mdf 데이터베이스에 연결](creating-the-membership-schema-in-sql-server-cs/_static/image11.png)](creating-the-membership-schema-in-sql-server-cs/_static/image10.png)

**그림 4**: 연결에서 `SecurityTutorials.mdf` 데이터베이스 ([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-cs/_static/image12.png))


[![데이터베이스 폴더에 SecurityTutorials.mdf 데이터베이스가 표시](creating-the-membership-schema-in-sql-server-cs/_static/image14.png)](creating-the-membership-schema-in-sql-server-cs/_static/image13.png)

**그림 5**:는 `SecurityTutorials.mdf` 데이터베이스가 데이터베이스 폴더에 나타납니다 ([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-cs/_static/image15.png))


그림 5에서 볼 수 있듯이 `SecurityTutorials.mdf` 데이터베이스 이름이 아니라 abstruse 합니다. (및 입력 하기 쉽게)를 보다 기억 하기 쉬운 바꿔보겠습니다 이름입니다. 데이터베이스를 마우스 오른쪽 단추로 클릭 이름 바꾸기 상황에 맞는 메뉴에서 선택한 이름을 바꾸거나 `SecurityTutorialsDatabase`합니다. 이 파일 이름은 변경 되지 않습니다, 그리고 데이터베이스 이름만 사용 하 여 SQL Server에 자체를 식별 합니다.


[![SecurityTutorialsDatabase에 데이터베이스 이름을 바꾸려면](creating-the-membership-schema-in-sql-server-cs/_static/image17.png)](creating-the-membership-schema-in-sql-server-cs/_static/image16.png)

**그림 6**: 데이터베이스 이름 바꾸기 `SecurityTutorialsDatabase`([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-cs/_static/image18.png))


이 시점에 대 한 서버 및 데이터베이스 이름을 알고는 `SecurityTutorials.mdf` 데이터베이스 파일: `localhost\InstanceName` 및 `SecurityTutorialsDatabase`각각. 통해 응용 프로그램 서비스를 설치할 준비가 됩니다.는 `aspnet_regsql.exe` 도구입니다.

### <a name="installing-the-application-services"></a>응용 프로그램 서비스를 설치합니다.

시작 하는 `aspnet_regsql.exe` 도구 시작 메뉴에 이동 하 고 실행을 선택 합니다. 입력 `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\aspnet_regsql.exe` textbox에 확인을 클릭 합니다. 또는 드릴 다운 적절 한 폴더를 두 번 클릭을 Windows 탐색기를 사용할 수는 `aspnet_regsql.exe` 파일입니다. 어느 방법이 든 동일한 결과 되지 것입니다.

실행 된 `aspnet_regsql.exe` 명령줄 인수 없이 도구 ASP.NET SQL Server 설치 마법사 그래픽 사용자 인터페이스를 시작 합니다. 마법사를 사용을 쉽게 추가 하거나 지정된 된 데이터베이스에는 ASP.NET 응용 프로그램 서비스를 제거 합니다. 그림 7에 표시 된 마법사의 첫 번째 화면 도구의 용도 설명 합니다.


[![ASP.NET SQL Server 설치 마법사는 사용 하 여 멤버 스키마를 추가 하려면](creating-the-membership-schema-in-sql-server-cs/_static/image20.png)](creating-the-membership-schema-in-sql-server-cs/_static/image19.png)

**그림 7**:에서 ASP.NET SQL Server 설치 마법사를 사용 하면 멤버 자격 스키마 추가를 사용 하 여 ([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-cs/_static/image21.png))


마법사의 두 번째 단계는 응용 프로그램 서비스를 추가 하거나 제거 하려는 여부 us를 요청 합니다. 테이블, 뷰 및 저장된 프로시저에 필요한 추가 하는 데는 `SqlMembershipProvider`, 응용 프로그램 서비스 옵션에 대 한 SQL Server 구성를 선택 합니다. 나중이 스키마를 데이터베이스에서 제거 하려는 경우이 마법사를 다시 실행 하지만 대신 기존 데이터베이스 옵션에서 응용 프로그램 서비스 정보 제거를 선택 합니다.


[![선택 된 응용 프로그램 서비스 옵션에 대 한 SQL Server 구성](creating-the-membership-schema-in-sql-server-cs/_static/image23.png)](creating-the-membership-schema-in-sql-server-cs/_static/image22.png)

**그림 8**: 응용 프로그램 서비스 옵션에 대 한 SQL Server 구성 선택 ([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-cs/_static/image24.png))


데이터베이스 정보를 묻는 세 번째 단계: 서버 이름, 인증 정보 및 데이터베이스 이름입니다. 이 자습서를 함께 수행 하 고 추가한 경우는 `SecurityTutorials.mdf` 데이터베이스를 `App_Data`에 연결 된 `localhost\InstanceName`, 되 게 하므로 이름을 바꿀 `SecurityTutorialsDatabase`, 다음 값을 사용 합니다.

- 서버: `localhost\InstanceName`
- Windows 인증
- 데이터베이스: `SecurityTutorialsDatabase`


[![데이터베이스 정보를 입력 합니다.](creating-the-membership-schema-in-sql-server-cs/_static/image26.png)](creating-the-membership-schema-in-sql-server-cs/_static/image25.png)

**그림 9**: 데이터베이스 정보를 입력 ([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-cs/_static/image27.png))


데이터베이스 정보를 입력 한 후 다음을 클릭 합니다. 마지막 단계는 수행 될 하는 단계를 요약 합니다. 응용 프로그램 서비스를 설치 하 고 마법사를 완료 하려면 다음 완료 하려면 다음을 클릭 합니다.

> [!NOTE]
> Management Studio를 사용 하는 데이터베이스 연결 및 데이터베이스 파일의 이름을 바꿀 경우 해야 데이터베이스를 분리 하 고 Visual Studio를 닫은 후 하기 전에 Management Studio를 닫습니다. 분리 하는 `SecurityTutorialsDatabase` 데이터베이스, 데이터베이스 이름을 마우스 오른쪽 단추로 클릭 하 고, 작업 메뉴에서 분리를 선택 합니다.


마법사를 완료 하면 Visual Studio로 되돌아가려면를 데이터베이스 탐색기로 이동 합니다. 테이블 폴더를 확장 합니다. 일련의 테이블 이름이 접두사로 시작 표시 되어야 `aspnet_`합니다. 마찬가지로, 뷰 및 저장 프로시저 폴더 아래에서 다양 한 뷰 및 저장된 프로시저를 찾을 수 있습니다. 이러한 데이터베이스 개체 응용 프로그램 서비스 스키마를 구성 합니다. 3 단계에서에서 멤버 자격 및 역할 관련 데이터베이스 개체를 검사 합니다.


[![데이터베이스에 추가 된 다양 한 테이블, 뷰 및 저장된 프로시저](creating-the-membership-schema-in-sql-server-cs/_static/image29.png)](creating-the-membership-schema-in-sql-server-cs/_static/image28.png)

**그림 10**: A 다양 한의 테이블, 뷰 및 저장 프로시저에 추가 된 데이터베이스 ([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-cs/_static/image30.png))


> [!NOTE]
> `aspnet_regsql.exe` 도구의 그래픽 사용자 인터페이스는 전체 응용 프로그램 서비스 스키마를 설치 합니다. 실행할 때 하지만 `aspnet_regsql.exe` 명령줄에서 지정할 수 있습니다 할 특정 응용 프로그램 서비스 구성 요소를 설치 (또는 제거). 따라서 방금 테이블을 추가 하려는 경우 뷰, 저장 프로시저에 필요한는 `SqlMembershipProvider` 및 `SqlRoleProvider` 공급자, 실행 `aspnet_regsql.exe` 명령줄에서. 또는 수동으로 실행할 수 있습니다는 적절 한 T-SQL의 하위 집합에서 사용 하는 스크립트를 만들 `aspnet_regsql.exe`합니다. 이러한 스크립트에는 `WINDIR%\Microsoft.Net\Framework\v2.0.50727\` 폴더와 같은 이름의 `InstallCommon.sql`,`InstallMembership.sql`,`InstallRoles.sql`, `InstallProfile.sql`,`InstallSqlState.sql`등입니다.


이 시점에서 필요한 데이터베이스 개체를 만들었습니다는 `SqlMembershipProvider`합니다. 그러나 여전히 필요를 사용 하도록 멤버 자격 프레임 워크에 지시 하는 `SqlMembershipProvider` (versus, 예를 들어, `ActiveDirectoryMembershipProvider`) 하 고는 `SqlMembershipProvider` 사용할지는 `SecurityTutorials` 데이터베이스. 어떤 사용할 공급자를 지정 하는 방법 및 4 단계에서에서 선택한 공급자의 설정을 사용자 지정 하는 방법을 살펴보겠습니다. 그러나 먼저 방금 생성 된 데이터베이스 개체에서 자세히 살펴보겠습니다.

## <a name="step-3-a-look-at-the-schemas-core-tables"></a>스키마의 핵심 테이블 살펴보고 3 단계:

ASP.NET 응용 프로그램에서 멤버 자격 및 역할 프레임 워크를 사용할 때 구현 세부 정보는 공급자에 의해 캡슐화 됩니다. .NET Framework를 통해 이러한 프레임 워크와 상호 자습서 이후 `Membership` 및 `Roles` 클래스입니다. 높은 수준의 이러한 Api를 사용 하는 경우 하지 필요가 하는 쿼리를 실행 또는 테이블의 정의와에 의해 수정와 같은 하위 수준 세부 정보는 `SqlMembershipProvider` 및 `SqlRoleProvider`합니다.

이 점을 고려는 2 단계에서에서 만든 데이터베이스 스키마를 탐색 필요 없이 멤버 자격 및 역할 프레임 워크를 자신 있게 사용할 수 없습니다 했습니다. 그러나 응용 프로그램 데이터를 저장할 테이블을 만들 때 사용자 또는 역할에 관련 된 엔터티를 만드는 할 수 있습니다. 에 대 한 지식이 있어야 하는 데 도움이 됩니다는 `SqlMembershipProvider` 및 `SqlRoleProvider` 스키마 외래 설정할 때 응용 프로그램 데이터 테이블 및 2 단계에서에서 만든 테이블 간에 제약 조건을 입력 합니다. 또한 드물게 특정 사용자와 상호 작용할 할 수도 있습니다 하 고 데이터베이스 수준에서 직접 역할 저장 (통해 대신는 `Membership` 또는 `Roles` 클래스).

### <a name="partitioning-the-user-store-into-applications"></a>응용 프로그램에 사용자 저장소 분

멤버 자격 및 역할 프레임 워크는 단일 사용자 및 역할 저장소 다양 한 응용 프로그램 간에 공유할 수 있도록 설계 되었습니다. 멤버 자격 또는 역할 프레임 워크를 사용 하는 ASP.NET 응용 프로그램에 사용 하기 위해 어떤 응용 프로그램 파티션을 지정 해야 합니다. 즉, 여러 웹 응용 프로그램 같은 사용자 및 역할 저장소를 사용할 수 있습니다. 그림 11 보여주고 세 개의 응용 프로그램으로 분할 하는 사용자 및 역할 저장소: HRSite, CustomerSite, 및 SalesSite 합니다. 이러한 세 가지 웹 응용 프로그램 각가 자신의 고유 사용자와 역할을 아직 모두 물리적으로 해당 사용자 계정과 역할 정보를 같은 데이터베이스 테이블에 저장 합니다.


[![여러 응용 프로그램 사용자 계정에 분할 될 수 있습니다.](creating-the-membership-schema-in-sql-server-cs/_static/image32.png)](creating-the-membership-schema-in-sql-server-cs/_static/image31.png)

**그림 11**: 사용자 계정 수 수 분할에서 여러 응용 프로그램 ([전체 크기 이미지를 보려면 클릭](creating-the-membership-schema-in-sql-server-cs/_static/image33.png))


`aspnet_Applications` 테이블이 이러한 파티션을 정의 합니다. 데이터베이스를 사용 하 여 사용자 계정 정보를 저장 하는 각 응용 프로그램은이 테이블의 행으로 표시 됩니다. `aspnet_Applications` 테이블에 4 개의 열이: `ApplicationId`, `ApplicationName`, `LoweredApplicationName`, 및 `Description`합니다. `ApplicationId` 형식의 [ `uniqueidentifier` ](https://msdn.microsoft.com/library/ms187942.aspx) 테이블의 기본 키 이며 `ApplicationName` 각 응용 프로그램에 대 한 고유 사용자에 게 친숙 한 이름을 제공 합니다.

다른 멤버 자격 및 역할 관련 테이블에 다시 연결 된 `ApplicationId` 필드에 `aspnet_Applications`합니다. 예를 들어는 `aspnet_Users` , 각 사용자 계정에 대 한 레코드를 포함 하는 테이블에는 `ApplicationId` 외래 키 필드;에 대 한 ditto는 `aspnet_Roles` 테이블입니다. `ApplicationId` 속한 역할 또는 이러한 테이블의 필드에에서 사용자 계정을 응용 프로그램 파티션을 지정 합니다.

### <a name="storing-user-account-information"></a>사용자 계정 정보를 저장합니다.

사용자 계정 정보는 두 테이블에 들어: `aspnet_Users` 및 `aspnet_Membership`합니다. `aspnet_Users` 필수 사용자 계정 정보를 포함 하는 필드가 테이블에 있습니다. 세 가지 가장 관련성이 큰 열이 됩니다.

- `UserId`
- `UserName`
- `ApplicationId`

`UserId` 기본 키 (유형의 `uniqueidentifier`). `UserName` 형식이 `nvarchar(256)` 및 암호와 함께 사용자의 자격 증명을 만듭니다. (사용자의 암호에 저장 됩니다는 `aspnet_Membership` 테이블입니다.) `ApplicationId` 에서 특정 응용 프로그램에 사용자 계정을 연결 `aspnet_Applications`합니다. 복합 [ `UNIQUE` 제약 조건](https://msdn.microsoft.com/library/ms191166.aspx) 에 `UserName` 및 `ApplicationId` 열입니다. 이렇게 하면 각 사용자 지정된 된 응용 프로그램에 고유 이름이 아직 동일한 고려한 `UserName` 서로 다른 응용 프로그램에서 사용할 수 있습니다.

`aspnet_Membership` 사용자의 암호, 전자 메일 주소는 마지막 로그인 날짜 및 시간 및 등과 같은 추가 사용자 계정 정보가 포함 됩니다. 레코드 간에 일대일 대응이 `aspnet_Users` 및 `aspnet_Membership` 테이블입니다. 이 관계에 의해 보장 되는 `UserId` 필드에 `aspnet_Membership`, 테이블의 기본 키로 제공 되 합니다. 마찬가지로 `aspnet_Users` 테이블 `aspnet_Membership` 포함는 `ApplicationId` 이 정보는 특정 응용 프로그램 파티션에 연결 하는 필드입니다.

### <a name="securing-passwords"></a>암호를 보호

암호 정보에 저장 되는 `aspnet_Membership` 테이블입니다. `SqlMembershipProvider` 암호는 다음 세 가지 기술 중 하나를 사용 하 여 데이터베이스에 저장 될 수 있습니다.

- **지우기** -암호가 일반 텍스트로 데이터베이스에 저장 됩니다. I 하지 않는 것이 옵션을 사용 합니다. 데이터베이스가 손상-해커 백도어 또는 데이터베이스 권한이 직원이 불만된을 발견 하 게 될 경우 모든 단일 사용자의 자격 증명 하는 데는 기록 합니다.
- **해시** -암호는 단방향 해시 알고리즘 및 임의로 생성 된 솔트 값을 사용 하 여 해시 됩니다. 이 해시 된 값 (함께 솔트) 데이터베이스에 저장 됩니다.
- **암호화** -암호의 암호화 된 버전의 데이터베이스에 저장 됩니다.

사용 되는 암호 저장소 기술에 따라 달라 집니다는 `SqlMembershipProvider` 에 지정 된 설정을 `Web.config`합니다. 사용자 지정 방법에 대해서는 `SqlMembershipProvider` 4 단계에서에서 설정 합니다. 기본 동작은 암호의 해시를 저장 하는 것입니다.

암호를 저장 하는 일을 담당 하는 열 `Password`, `PasswordFormat`, 및 `PasswordSalt`합니다. `PasswordFormat` 형식의 필드는 `int` 암호를 저장 하는 데 사용 되는 기술은 나타내는 값: 0 지우기에 대 한; Hashed에 대 한 1; 암호화에 대 한 2입니다. `PasswordSalt` 사용 하는 암호 저장 방법에 관계 없이 임의로 생성 된 문자열을 할당 값 `PasswordSalt` 암호의 해시를 계산할 때만 사용 됩니다. 마지막으로 `Password` 일반 텍스트 암호의 암호화 된 암호 또는 암호를 해시 수를 실제 암호 데이터를 포함 하는 열입니다.

표 1이 3 열의 수 모양을 보여줍니다 다양 한 저장소 기술에 대 한 MySecret 암호를 저장할 때! 이어야 합니다.

| **저장소 기술&lt;\_o3a\_p /&gt;** | **암호&lt;\_o3a\_p /&gt;** | **PasswordFormat&lt;\_o3a\_p /&gt;** | **PasswordSalt&lt;\_o3a\_p /&gt;** |
| --- | --- | --- | --- |
| 지우기 | MySecret! | 0 | tTnkPlesqissc2y2SMEygA== |
| 해시 | 2oXm6sZHWbTHFgjgkGQsc2Ec9ZM= | 1 | wFgjUfhdUFOCKQiI61vtiQ== |
| 암호화 | 62RZgDvhxykkqsMchZ0Yly7HS6onhpaoCYaRxV8g0F4CW56OXUU3e7Inza9j9BKp | 2 | LSRzhGS/aa/oqAXGLHJNBw== |

**표 1**: 암호 MySecret 저장할 때 암호 관련 필드에 대 한 예제 값!

> [!NOTE]
> 특정 암호화 또는에서 사용 하는 해시 알고리즘의 `SqlMembershipProvider` 설정에 따라 결정 되는 `<machineKey>` 요소. 3 단계에서에서이 구성 요소에서 설명한는 <a id="Tutorial3"> </a> [ *폼 인증 구성 및 고급 항목* ](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md) 자습서입니다.


### <a name="storing-roles-and-role-associations"></a>역할 및 역할 연결 저장

역할 프레임 워크에는 개발자를 역할 집합을 정의 하 고 어떤 사용자가 역할에 속한를 지정할 수 있습니다. 두 테이블을 통해 데이터베이스에서이 정보는 캡처됩니다: `aspnet_Roles` 및 `aspnet_UsersInRoles`합니다. 각 레코드는 `aspnet_Roles` 테이블은 특정 응용 프로그램에 대 한 역할을 나타냅니다. 과 거의 동일한는 `aspnet_Users` 테이블은 `aspnet_Roles` 테이블에 세 개의 열이 설명에 관련:

- `RoleId`
- `RoleName`
- `ApplicationId`

`RoleId` 기본 키 (유형의 `uniqueidentifier`). `RoleName`는 `nvarchar(256)` 형식입니다. 및 `ApplicationId` 에서 특정 응용 프로그램에 사용자 계정을 연결 `aspnet_Applications`합니다. 복합 `UNIQUE` 제약 조건에는 `RoleName` 및 `ApplicationId` 열을 지정된 된 응용 프로그램에서 각 역할 이름이 고유한 지 확인 합니다.

`aspnet_UsersInRoles` 테이블 사용자 및 역할 간의 매핑을로 사용 합니다. 두 개의 열이- `UserId` 및 `RoleId` -함께 복합 기본 키를 구성 하 고 있습니다.

## <a name="step-4-specifying-the-provider-and-customizing-its-settings"></a>공급자를 지정 하 고 해당 설정을 사용자 지정 하는 4 단계:

멤버 자격 및 역할 프레임 워크--같은 공급자 모델을 지 원하는 프레임 워크의 모든 자체 구현 세부 사항을 없고 대신 공급자 클래스에 해당 역할을 위임 합니다. 멤버 자격 프레임 워크의 경우는 `Membership` 클래스는 사용자 계정을 관리 하기 위한 API를 정의 하지만 모든 사용자 저장소와 직접 상호 작용 하지 않습니다. 대신,는 `Membership` 클래스의 메서드에 전달 요청에 구성 된 공급자-를 사용 합니다는 `SqlMembershipProvider`합니다. 메서드 중 하나를 호출 우리는 경우는 `Membership` 클래스는 구성원 프레임 워크 확인 방법에 대 한 호출을 위임 하는 `SqlMembershipProvider`?

`Membership` 클래스에는 [ `Providers` 속성](https://msdn.microsoft.com/library/system.web.security.membership.providers.aspx) 구성원 프레임 워크에서 사용 하기 위해 사용할 수 있는 등록 된 공급자 클래스는 모두에 대 한 참조를 포함 하 합니다. 등록 된 각 공급자에 연결 된 이름 및 유형. 이름에 특정 공급자를 참조 하는 사용자에 게 친숙 한 방법을 제공는 `Providers` 형식 공급자 클래스를 식별 하는 동안 컬렉션입니다. 또한 등록 된 각 공급자는 구성 설정을 포함 될 수 있습니다. 멤버 자격 프레임 워크에 대 한 구성 설정을 포함 `passwordFormat` 및 `requiresUniqueEmail`, 다양 한 기타. 표 2에서 사용 하는 구성 설정의 전체 목록에 대 한 참조는 `SqlMembershipProvider`합니다.

`Providers` 속성의 내용을 웹 응용 프로그램의 구성 설정을 통해 지정 됩니다. 기본적으로 모든 웹 응용 프로그램 적용 라는 공급자 `AspNetSqlMembershipProvider` 형식의 `SqlMembershipProvider`합니다. 이 기본 멤버 자격 공급자에 등록 되어 `machine.config` (에 있는 `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG)`:

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample1.xml)]

위의 태그로 [ `<membership>` 요소](https://msdn.microsoft.com/library/1b9hw62f.aspx) 하는 동안 멤버 자격 프레임 워크에 대 한 구성 설정을 정의 [ `<providers>` 자식 요소가](https://msdn.microsoft.com/library/6d4936ht.aspx) 지정는 등록 된 공급자입니다. 공급자 추가 될 수 있습니다 또는 사용 하 여 제거는 [ `<add>` ](https://msdn.microsoft.com/library/whae3t94.aspx) 또는 [ `<remove>` ](https://msdn.microsoft.com/library/aykw9a6d.aspx) 사용; 요소는 [ `<clear>` ](https://msdn.microsoft.com/library/t062y6yc.aspx) 현재 모두 제거 하는 요소 등록 된 공급자입니다. 위의 태그로 `machine.config` 라는 공급자 추가 `AspNetSqlMembershipProvider` 형식의 `SqlMembershipProvider`합니다.

외에 `name` 및 `type` 특성의 `<add>` 요소 다양 한 설정 구성에 대 한 값을 정의 하는 특성을 포함 합니다. 표 2는 사용할 수 있는 목록 `SqlMembershipProvider`-특정 구성 설정과 각각에 대해 설명 합니다.

> [!NOTE]
> 표 2에 명시 된 기본값에 정의 된 기본값 참조는 `SqlMembershipProvider` 클래스입니다. 것은 아닙니다의 구성 설정의 모든 `AspNetSqlMembershipProvider` 의 기본 값에 해당 하는 `SqlMembershipProvider` 클래스입니다. 예를 들어, 멤버 자격 공급자에 지정 되지 않은 경우는 `requiresUniqueEmail` 기본값을 true로 설정 합니다. 그러나는 `AspNetSqlMembershipProvider` 명시적으로 값을 지정 하 여이 기본값을 재정의 `false`합니다.


| **설정&lt;\_o3a\_p /&gt;** | **설명&lt;\_o3a\_p /&gt;** |
| --- | --- |
| `ApplicationName` | 여러 응용 프로그램에 분할할 수를 단일 사용자 저장소에 대 한 멤버 자격 프레임 워크에서는 없다는 것을 기억 합니다. 이 설정은 응용 프로그램 파티션 멤버 자격 공급자에서 사용 하는 이름을 나타냅니다. 경우이 값은 명시적으로 지정 하지, 런타임에 응용 프로그램의 가상 루트 경로 값으로 설정 합니다. |
| `commandTimeout` | SQL 명령 시간 제한 값 (초)을 지정합니다. 기본값은 30입니다. |
| `connectionStringName` | 연결 문자열의 이름에서 `<connectionStrings>` 사용자 저장소 데이터베이스에 연결 하는 데 사용 하는 요소입니다. 이 값이 필요 합니다. |
| `description` | 등록 된 공급자의 사용자에 게 친숙 한 설명을 제공합니다. |
| `enablePasswordRetrieval` | 사용자가 잊어버린된 암호를 검색할 수 있는지 여부를 지정 합니다. 기본값은 `false`입니다. |
| `enablePasswordReset` | 사용자가 자신의 암호를 재설정할 수 있는지 여부를 나타냅니다. 기본값은 `true`입니다. |
| `maxInvalidPasswordAttempts` | 지정된 된 사용자에 대 한 지정 된 하는 동안 발생할 수 있는 실패 한 로그인 시도의 최대 수 `passwordAttemptWindow` 사용자를 잠그기 전에 합니다. 기본값은 5입니다. |
| `minRequiredNonalphanumericCharacters` | 최소 사용자의 암호에 표시 되어야 하는 영숫자가 아닌 문자 수입니다. 이 값은 0에서 128; 사이 여야 합니다. 기본값은 1입니다. |
| `minRequiredPasswordLength` | 최소 암호에 필요한 문자 수입니다. 이 값은 0에서 128; 사이 여야 합니다. 기본값은 7입니다. |
| `name` | 등록 된 공급자의 이름입니다. 이 값이 필요 합니다. |
| `passwordAttemptWindow` | 시간을 분 단위로가 못했습니다 로그인 시도가 추적 됩니다. 사용자는 잘못 된 로그인 자격 증명을 제공 하는 경우 `maxInvalidPasswordAttempts` 시간이 내의 지정 창는 잠깁니다. 기본값은 10입니다. |
| `PasswordFormat` | 암호 저장 형식: `Clear`, `Hashed`, 또는 `Encrypted`합니다. 기본값은 `Hashed`입니다. |
| `passwordStrengthRegularExpression` | 제공 된 정규식이 암호를 변경할 때 또는 새 계정을 만들 때 사용자의 선택 된 암호의 강도 평가 하 ´ ù. 기본값은 빈 문자열입니다. |
| `requiresQuestionAndAnswer` | 사용자가 암호 다시 설정 하거나 검색할 때 그의 보안 질문에 대답 해야 하는지 여부를 지정 합니다. 기본값은 `true`입니다. |
| `requiresUniqueEmail` | 지정 된 응용 프로그램 파티션에 있는 모든 사용자 계정에 고유한 전자 메일 주소가 있어야 하는지 여부를 나타냅니다. 기본값은 `true`입니다. |
| `type` | 공급자의 유형을 지정합니다. 이 값이 필요 합니다. |

**표 2**: 멤버 자격 및 `SqlMembershipProvider` 구성 설정

외에 `AspNetSqlMembershipProvider`, 유사한 태그를 추가 하 여 응용 프로그램에서 응용 프로그램 별로 다른 멤버 자격 공급자를 등록할 수 있습니다는 `Web.config` 파일입니다.

> [!NOTE]
> 역할 프레임 워크 동일한 방식으로 거의:에 기본 등록 된 역할 공급자가 `machine.config` 에서 응용 프로그램에서 응용 프로그램으로 등록 된 공급자를 사용자 지정할 수 있습니다 및 `Web.config`합니다. 역할 프레임 워크 및 세부 정보에서 해당 구성 태그는 이후 자습서 검토할 것입니다.


### <a name="customizing-thesqlmembershipprovidersettings"></a>사용자 지정의`SqlMembershipProvider`설정

기본 `SqlMembershipProvider` (`AspNetSqlMembershipProvider`)가 해당 `connectionStringName` 특성이로 설정 `LocalSqlServer`합니다. 마찬가지로 `AspNetSqlMembershipProvider` 공급자, 연결 문자열 이름 `LocalSqlServer` 에 정의 된 `machine.config`합니다.

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample2.xml)]

이 연결 문자열 정의에 있는 데이터베이스는 SQL 2005 Express Edition 볼 수 있듯이 | DataDirectory|aspnetdb.mdf 합니다. 문자열 | DataDirectory |를 가리키도록 런타임에 변환에서 `~/App_Data/` 디렉터리 하므로 데이터베이스 경로 | DataDirectory|aspnetdb.mdf"로 변환 `~/App_Data` / `aspnet.mdf`합니다.

이 응용 프로그램에서 한 멤버 자격 공급자 정보를 지정 하지 않았기 경우 `Web.config` 파일, 응용 프로그램에 등록 된 기본 멤버 자격 공급자를 사용 하 여 `AspNetSqlMembershipProvider`합니다. 경우는 `~/App_Data/aspnet.mdf` 데이터베이스가 존재 하지 않습니다, ASP.NET 런타임이 자동으로 만들고 응용 프로그램 서비스 스키마를 추가 합니다. 그러나에서는 사용 하지 않음은 `aspnet.mdf` 데이터베이스; 대신 사용 하려는 `SecurityTutorials.mdf` 2 단계에서에서 만든 데이터베이스입니다. 두 가지 방법 중 하나에서이 수정 작업을 수행할 수 있습니다.

- <strong>에 대 한 값을 지정 된</strong><strong>`LocalSqlServer`</strong><strong>의 연결 문자열 이름</strong><strong>`Web.config`</strong><strong>합니다.</strong> 덮어쓰는 방법으로 `LocalSqlServer` 연결 문자열 이름 값의 `Web.config`, 등록 된 기본 멤버 자격 공급자를 사용할 수 있습니다 (`AspNetSqlMembershipProvider`)와 올바르게 사용할는 `SecurityTutorials.mdf` 데이터베이스입니다. 이 방법은 지정 된 구성 설정으로 콘텐츠는 괜 찮으 `AspNetSqlMembershipProvider`합니다. 이 방법에 대 한 자세한 내용은 참조 하십시오. [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 블로그 게시물 [구성 ASP.NET 2.0 응용 프로그램 서비스를 사용 하 여 SQL Server 2000 또는 SQL Server 2005](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)합니다.
- <strong>형식의 새 등록 된 공급자를 추가</strong><strong>`SqlMembershipProvider`</strong><strong>구성 및 해당</strong><strong>`connectionStringName`</strong><strong>는를가리키도록설정</strong> <strong>`SecurityTutorials.mdf`</strong> <strong>데이터베이스입니다.</strong> 이 방법은 데이터베이스 연결 문자열 뿐 아니라 구성 속성을 다른 사용자 지정 하려는 시나리오에서 유용 합니다. 나만의 프로젝트에서 항상 사용이 방법을 사용의 유연성과 가독성 때문에 합니다.

참조 하는 새 등록 된 공급자를 추가 하기 전에 `SecurityTutorials.mdf` 데이터베이스에 먼저 추가 해야 한다고를 적절 한 연결 문자열 값에는 `<connectionStrings>` 섹션 `Web.config`합니다. 라는 새 연결 문자열을 추가 하는 다음 태그 `SecurityTutorialsConnectionString` SQL Server 2005 Express Edition을 참조 하는 `SecurityTutorials.mdf` 여기에 데이터베이스는 `App_Data` 폴더입니다.

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample3.xml)]

> [!NOTE]
> 대체 데이터베이스 파일을 사용 하는 경우 필요에 따라 연결 문자열을 업데이트 합니다. 올바른 연결 문자열을 형성에 자세한 내용은를 참조 [ConnectionStrings.com](http://www.connectionstrings.com/)합니다.

다음에 다음 구성원 구성 태그를를 추가 `Web.config` 파일입니다. 라는 새 공급자를 등록 하는이 태그 `SecurityTutorialsSqlMembershipProvider`합니다.

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample4.xml)]

등록할 뿐만 아니라는 `SecurityTutorialsSqlMembershipProvider` 공급자, 위의 태그는 정의 `SecurityTutorialsSqlMembershipProvider` 기본 공급자로 (통해는 `defaultProvider` 특성에 `<membership>` 요소). 멤버 자격 프레임 워크 여러 개 등록 된 공급자를 가질 수 있다는 점에 유의 하세요. 이후 `AspNetSqlMembershipProvider` 에서 첫 번째 공급자로 등록 `machine.config`, 여기서 명시 하지 않는 한 기본 공급자로 사용 합니다.

현재 응용 프로그램에 두 명의 등록 된 공급자: `AspNetSqlMembershipProvider` 및 `SecurityTutorialsSqlMembershipProvider`합니다. 그러나 등록 하기 전에는 `SecurityTutorialsSqlMembershipProvider` 우리 수 선택을 취소 한 모든 이전에 공급자를 추가 하 여 공급자를 등록 한 [ `<clear />` 요소](https://msdn.microsoft.com/library/t062y6yc.aspx) 바로 앞 우리의 `<add>` 요소입니다. 지울 것이 고 `AspNetSqlMembershipProvider` 의미 하는 등록 된 공급자 목록에서는 `SecurityTutorialsSqlMembershipProvider` 유일한 등록 된 멤버 자격 공급자는 것입니다. 이 방법을 사용한 경우 표시 해야 하지는 `SecurityTutorialsSqlMembershipProvider` 기본 공급자로 이후에 것이 유일한 등록 된 멤버 자격 공급자입니다. 사용 하 여 대 한 자세한 내용은 `<clear />`, 참조 [Using `<clear />` 때 추가 공급자](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx)합니다.

`SecurityTutorialsSqlMembershipProvider`의 `connectionStringName` 는 방금 추가 된 참조를 설정 `SecurityTutorialsConnectionString` 있고 연결 문자열 이름, 해당 `applicationName` SecurityTutorials의 값으로 설정 되었습니다. 또한는 `requiresUniqueEmail` 설정으로 설정 된 `true`합니다. 다른 모든 구성 옵션의 값에 동일 `AspNetSqlMembershipProvider`합니다. 자유롭게 여기에서 구성 수정 하려는 경우. 예를 들어 대신 하나, 두 개의 영숫자 이외의 문자를 요구 하거나를 8 자로 7 대신 암호 길이 늘려 암호 강도 강화할 수 있습니다.

> [!NOTE]
> 여러 응용 프로그램에 분할할 수를 단일 사용자 저장소에 대 한 멤버 자격 프레임 워크에서는 없다는 것을 기억 합니다. 멤버 자격 공급자 `applicationName` 설정 공급자가 사용자 저장소와 함께 작업할 때 사용 하는 응용 프로그램을 나타냅니다. 것이 중요에 대 한 값을 명시적으로 설정 하는 `applicationName` 때문에 구성 설정의 경우는 `applicationName` 명시적으로 설정 하지 않으면 런타임 시 웹 응용 프로그램의 가상 루트 경로에 할당 됩니다. 이 기능이 제대로 작동 하지만 응용 프로그램을 다른 경로로 이동 하는 경우 응용 프로그램의 가상 루트 경로 변경 하지 않는 상태로 `applicationName` 설정도 변경 됩니다. 이런 경우 멤버 자격 공급자는 이전에 사용한 것 다른 응용 프로그램 파티션이 포함 된 작업을 시작 합니다. 이동 하기 전에 만들어진 사용자 계정은 다른 응용 프로그램 파티션에 있으며 해당 사용자가 더 이상 사이트에 로그인 할 수 없게 됩니다. 이 문제에 대 한 심도 있는 논의 알려면 [항상 설정 된 `applicationName` 속성 때 구성 ASP.NET 2.0 멤버 자격 및 기타 공급자](https://weblogs.asp.net/scottgu/443634)합니다.


## <a name="summary"></a>요약

구성 된 응용 프로그램 서비스를 사용 하 여 데이터베이스 했으므로 시점에서 (`SecurityTutorials.mdf`) 및에 멤버 자격 프레임 워크를 사용 하도록 웹 응용 프로그램의 구성에서 `SecurityTutorialsSqlMembershipProvider` 공급자 방금 등록 합니다. 이 등록 된 공급자는 형식의 `SqlMembershipProvider` 되었으며 해당 `connectionStringName` 적절 한 연결 문자열을 설정 (`SecurityTutorialsConnectionString`) 및 해당 `applicationName` 값 명시적으로 설정 합니다.

이제 응용 프로그램에서 멤버 자격 프레임 워크를 사용할 준비가 되었습니다. 다음 자습서를 새 사용자 계정을 만드는 방법을 살펴보겠습니다. 다음 사용자 인증, 사용자 기반 권한 부여를 수행 하 고 데이터베이스에 추가 사용자 관련 정보를 저장 합니다. 살펴볼 것입니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [항상 설정 된 `applicationName` ASP.NET 2.0을 구성 하는 경우에 속성 멤버 자격 및 기타 공급자](https://weblogs.asp.net/scottgu/443634)
- [사용 하 여 SQL Server 2000 또는 SQL Server 2005 응용 프로그램 서비스 ASP.NET 2.0 구성](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)
- [SQL Server Management Studio Express Edition 다운로드](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)
- [ASP.NET 2.0 검사 s 멤버 자격, 역할 및 프로필](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [`<add>` 멤버 자격에 대 한 공급자에 대 한 요소](https://msdn.microsoft.com/library/whae3t94.aspx)
- [`<membership>` 요소](https://msdn.microsoft.com/library/1b9hw62f.aspx)
- [`<providers>` 멤버 자격에 대 한 요소](https://msdn.microsoft.com/library/6d4936ht.aspx)
- [사용 하 여 `<clear />` 공급자를 추가 하는 경우](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx)
- [와 직접 작업 하는 `SqlMembershipProvider`](http://aspnet.4guysfromrolla.com/articles/091207-1.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>이 자습서에 포함 된 항목에 대 한 비디오 교육

- [ASP.NET 멤버 자격 이해](../../../videos/authentication/understanding-aspnet-memberships.md)
- [멤버 자격 스키마와 함께 작동하도록 SQL 구성](../../../videos/authentication/configuring-sql-to-work-with-membership-schemas.md)
- [기본 멤버 자격 스키마에서 멤버 자격 설정 변경](../../../videos/authentication/changing-membership-settings-in-the-default-membership-schema.md)

### <a name="about-the-author"></a>작성자 정보

여러 ASP/ASP.NET 책의 작성자 및 4GuysFromRolla.com의 창립자 Scott Mitchell의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은  *[Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*합니다. Scott에 도달할 수 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 또는에서 그의 블로그 통해 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Alicja Maziarz 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4guysfromrolla.com)합니다.

> [!div class="step-by-step"]
> [다음](creating-user-accounts-cs.md)
