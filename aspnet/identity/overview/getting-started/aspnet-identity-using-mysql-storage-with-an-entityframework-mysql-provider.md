---
uid: identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
title: 'ASP.NET Id: EntityFramework MySQL 공급자 (C#)와 MySQL 저장소를 사용 하 여 | Microsoft Docs'
author: maumar
description: 이 자습서에서는 MySQL 견실한 EntityFramework (SQL 클라이언트 공급자)를 사용 하 여 기본 데이터 저장소 메커니즘에 ASP.NET Id에 대 한 대체 하는 방법...
ms.author: riande
ms.date: 12/10/2013
ms.assetid: 15253312-a92c-43ba-908e-b5dacd3d08b8
msc.legacyurl: /identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
msc.type: authoredcontent
ms.openlocfilehash: f510c9bcaf83c6a68e835a7d82555653459df856
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48912373"
---
<a name="aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider-c"></a>ASP.NET Id: EntityFramework MySQL 공급자 (C#)를 사용 하 여 MySQL 저장소 사용
====================
하 여 [Maurycy Markowski](https://github.com/maumar)하십시오 [Raquel Soares De Almeida](https://github.com/raquelsa), [Robert McMurray](https://github.com/rmcmurray)

> 이 자습서에서는 기본 데이터 저장소 메커니즘을 교체 하는 방법을 보여 줍니다 [ **ASP.NET Id** ](introduction-to-aspnet-identity.md) (SQL 클라이언트 공급자) EntityFramework MySQL 공급자를 사용 하 여 합니다.


다음 항목에서는이 자습서에서 설명 합니다.

- Azure에서 MySQL 데이터베이스 만들기
- Visual Studio 2013 MVC 템플릿을 사용 하 여 MVC 응용 프로그램 만들기
- EntityFramework MySQL 데이터베이스 공급자와 함께 작동 하도록 구성
- 결과 확인 하려면 응용 프로그램 실행

이 자습서의 끝 해야 저장 ASP.NET Id를 사용 하 여 MVC 응용 프로그램 Azure에서 호스트 되는 MySQL 데이터베이스를 사용 하는 합니다.

## <a name="creating-a-mysql-database-instance-on-azure"></a>Azure에서 MySQL 데이터베이스 인스턴스 만들기

1. [Azure Portal](https://go.microsoft.com/fwlink/?linkid=529715&amp;clcid=0x409)에 로그인합니다.
2. 클릭 **새로 만들기** 한 다음 선택한 페이지의 맨 아래에서 **스토어**:

    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.png)
3. 에 **선택 및 추가 기능** 마법사 **ClearDB MySQL Database**를 클릭 하 고는 **다음** 프레임의 아래쪽 화살표:

   [확장 하려면 다음 이미지를 클릭 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.png)
4. 기본값을 유지 **무료** 계획으로 변경 합니다 **이름** 에 **IdentityMySQLDatabase**, 가장 가까운, 지역을 선택 하 고 클릭는 **다음** 프레임의 아래쪽 화살표:

   [확장 하려면 다음 이미지를 클릭 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.png)
5. 클릭 합니다 **구매** 데이터베이스 만들기를 완료 하려면 확인 표시 합니다.

   [확장 하려면 다음 이미지를 클릭 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.png)
6. 데이터베이스를 만든 후에서 관리할 수 있습니다 합니다 **추가 기능** 관리 포털에서 탭 합니다. 데이터베이스에 대 한 연결 정보를 검색 하려면 클릭 **연결 정보** 페이지의 맨 아래에서:

   [확장 하려면 다음 이미지를 클릭 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image10.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image9.png)
7. 복사 단추를 클릭 하 여 연결 문자열을 복사 합니다 **CONNECTIONSTRING** 필드 저장 하 고 MVC 응용 프로그램에 대 한이 자습서의 뒷부분에서이 정보를 사용 합니다.

   [확장 하려면 다음 이미지를 클릭 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image12.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image11.png)

## <a name="creating-an-mvc-application-project"></a>MVC 응용 프로그램 프로젝트 만들기

자습서의이 섹션의 단계를 완료 하려면를 먼저 설치 해야 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 하거나 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)합니다. Visual Studio가 설치 된 후 새 MVC 응용 프로그램 프로젝트를 만들려면 다음 단계를 사용 합니다.

1. Visual Studio 2103를 엽니다.
2. 클릭 **새 프로젝트** 에서 합니다 **시작** 하거나 페이지를 클릭 합니다 **파일** 메뉴 차례로 **새 프로젝트**:

   [확장 하려면 다음 이미지를 클릭 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.jpg)
3. 경우는 **새 프로젝트** 대화 상자가 표시 됩니다, 확장 **Visual C#** 템플릿의 목록에서 클릭 **웹**를 선택 하 고 **ASP.NET 웹 응용 프로그램**. 프로젝트 이름을 **IdentityMySQLDemo** 을 클릭 한 다음 **확인**:

   [확장 하려면 다음 이미지를 클릭 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image14.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image13.png)
4. 에 **새 ASP.NET 프로젝트** 대화 상자에서 선택 합니다 **MVC** templatewith; 기본 옵션을 구성 하이는 **개별 사용자 계정** 인증 방법으로 합니다. **확인**을 클릭합니다.

   [확장 하려면 다음 이미지를 클릭 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image16.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image15.png)

## <a name="configure-entityframework-to-work-with-a-mysql-database"></a>MySQL 데이터베이스를 사용 하려면 EntityFramework를 구성 합니다.

### <a name="update-the-entity-framework-assembly-for-your-project"></a>프로젝트에 대 한 Entity Framework 어셈블리를 업데이트 합니다.

Visual Studio 2013 템플릿에서 만든 MVC 응용 프로그램에 대 한 참조를 포함 합니다 [EntityFramework 6.0.0](http://www.nuget.org/packages/EntityFramework) 패키지 있으 나 가지를 포함 하는 해당 릴리스 이후 해당 어셈블리에 대 한 업데이트를 중요 한 되었습니다 성능이 향상 되었습니다. 응용 프로그램에서 이러한 최신 업데이트를 사용 하려면 다음 단계를 사용 합니다.

1. Visual Studio에서 MVC 프로젝트를 엽니다.
2. 클릭 **도구가**, 클릭 **NuGet 패키지 관리자**를 클릭 하 고 **패키지 관리자 콘솔**:

   [확장 하려면 다음 이미지를 클릭 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image18.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image17.png)
3. 합니다 **패키지 관리자 콘솔** Visual Studio의 아래쪽 섹션에 표시 됩니다. 형식 &quot; **Update-package EntityFramework** &quot; Enter 키를 누릅니다.

   [확장 하려면 다음 이미지를 클릭 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image20.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image19.png)

### <a name="install-the-mysql-provider-for-entityframework"></a>EntityFramework MySQL 공급자를 설치 합니다.

MySQL 데이터베이스에 연결 하려면 EntityFramework MySQL 공급자를 설치 해야 합니다. 이 위해 엽니다는 **패키지 관리자 콘솔** 형식과 &quot; **Install-package MySql.Data.Entity-Pre**&quot;, 한 다음 Enter를 누릅니다.

> [!NOTE]
> 어셈블리의 시험판 버전 이며 따라서 버그를 포함할 수 있습니다. 프로덕션 환경에서 시험판 버전의 공급자를 사용 하지 해야 합니다.


[확장 하려면 다음 이미지를 클릭 합니다.]

[![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image22.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image21.png)

### <a name="making-project-configuration-changes-to-the-webconfig-file-for-your-application"></a>응용 프로그램에 대 한 Web.config 파일을 한 프로젝트 구성 변경

방금 설치한 MySQL 공급자를 사용 하는 Entity Framework를 구성 하는이 섹션에서는 MySQL 공급자 팩터리를 등록 하 고 Azure에서 연결 문자열을 추가 합니다.

> [!NOTE]
> 다음 예제에서는 MySql.Data.dll에 대 한 특정 어셈블리 버전을 포함 합니다. 어셈블리 버전을 변경 하는 경우 올바른 버전을 사용 하 여 적절 한 구성 설정을 수정 해야 합니다.


1. Visual Studio 2013에서 프로젝트의 Web.config 파일을 엽니다.
2. Entity Framework에 대 한 기본 데이터베이스 공급자 및 팩터리를 정의 하는 다음 구성 설정을 찾습니다.

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample1.xml)]
3. 해당 구성 설정을 MySQL 공급자를 사용 하는 Entity Framework를 구성 하는 다음을 바꿉니다.

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample2.xml)]
4. 찾을 합니다 &lt;connectionStrings&gt; 섹션 및 Azure에서 호스트 되는 MySQL 데이터베이스에 대 한 연결 문자열을 정의 하는 다음 코드로 바꿉니다 (에서 providerName 값도 변경 되어 있음을 합니다 원본):

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample3.xml?highlight=3-4)]

### <a name="adding-custom-migrationhistory-context"></a>사용자 지정 MigrationHistory 컨텍스트 추가

Entity Framework Code First 사용 하는 **MigrationHistory** 테이블 모델 변경 내용을 추적 하 고 데이터베이스 스키마와 개념적 스키마 간의 일관성을 유지 하도록 합니다. 그러나이 테이블 작동 하지 않습니다 MySQL에 대 한 기본적으로 기본 키 너무 크기 때문에. 이 문제를 해결 하려면 해당 테이블에 대 한 키 크기를 축소 해야 합니다. 이렇게 하려면 다음 단계를 사용 합니다.

1. 이 테이블에 대 한 스키마 정보가 캡처됩니다를 **HistoryContext**, 모든 다른 수정 될 수 있습니다 **DbContext**합니다. 이렇게 하려면 라는 새 클래스 파일을 추가 **MySqlHistoryContext.cs** 프로젝트에 해당 내용을 다음 코드로 바꿉니다.

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample4.cs)]
2. 수정 된 데 Entity Framework를 구성 해야 하는 다음 **HistoryContext**, 기본 대신 합니다. 이 코드 기반 구성 기능을 활용 하 여 수행할 수 있습니다. 이렇게 하려면 라는 새 클래스 파일을 추가 **MySqlConfiguration.cs** 프로젝트에 사용 하 여 해당 내용을 바꿉니다.

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample5.cs)]

### <a name="creating-a-custom-entityframework-initializer-for-applicationdbcontext"></a>ApplicationDbContext EntityFramework 이니셜라이저를 사용자 지정 만들기

데이터베이스에 연결 하기 위해 모델 이니셜라이저를 사용 해야 하므로이 자습서에서 제공 되는 MySQL 공급자 Entity Framework 마이그레이션을 현재 지원 하지 않습니다. 이 자습서가 Azure에서 MySQL 인스턴스를 사용 하 고, 있으므로 사용자 지정 하는 Entity Framework 이니셜라이저를 만들려고 해야 합니다.

> [!NOTE]
> Azure 또는 온-프레미스에서 호스트 되는 데이터베이스를 사용 하는 경우에 SQL Server 인스턴스에 연결 하는 경우에이 단계가 필요 하지 않습니다.


MySQL에 대 한 Entity Framework 이니셜라이저를 사용자 지정을 만들려면 다음 단계를 사용 합니다.

1. 라는 새 클래스 파일을 추가 **MySqlInitializer.cs** 내용을 다음 코드로 바꾸고 프로젝트에는:

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample6.cs?highlight=23)]
2. 열기는 **IdentityModels.cs** 에 있는 프로젝트에 대 한 파일을 **모델** 디렉터리 해당 콘텐츠를 다음으로 바꾸고:

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample7.cs)]

## <a name="running-the-application-and-verifying-the-database"></a>응용 프로그램을 실행 하 고 데이터베이스를 확인 합니다.

이전 섹션의 단계를 완료 한 후 데이터베이스를 테스트 해야 합니다. 이렇게 하려면 다음 단계를 사용 합니다.

1. 키를 눌러 **ctrl+f5** 을 빌드 및 웹 응용 프로그램을 실행 합니다.
2. 클릭 합니다 **등록** 페이지 맨 위에 있는 탭:

   [확장 하려면 다음 이미지를 클릭 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.jpg)
3. 새 사용자 이름 및 암호를 입력 한 다음 클릭 **등록**:

   [확장 하려면 다음 이미지를 클릭 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image24.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image23.png)
4. 이 시점에서 ASP.NET Id 테이블은 MySQL 데이터베이스에서 만들어지고 사용자가 등록 하 고 응용 프로그램에 로그인:

   [확장 하려면 다음 이미지를 클릭 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.jpg)

### <a name="installing-mysql-workbench-tool-to-verify-the-data"></a>데이터를 확인 하려면 MySQL 워크 벤치 도구 설치

1. 설치 합니다 **MySQL Workbench** 에서 도구는 [MySQL 다운로드 페이지](http://dev.mysql.com/downloads/windows/installer/)
2. 설치 마법사에서: **기능 선택** 탭을 선택 **MySQL Workbench** 아래의 **응용 프로그램** 섹션입니다.
3. 앱을 시작 하 고이 자습서의 받아야에서 만든 Azure MySQL 데이터베이스에서 연결 문자열 데이터를 사용 하 여 새 연결을 추가 합니다.
4. 연결을 만든 후 검사를 **ASP.NET Id** 에서 만든 테이블을 **IdentityMySQLDatabase 합니다.**
5. 아래 이미지에 표시 된 대로 테이블이 만들어집니다 필요한 모든 ASP.NET Id를 볼 수 있습니다.

   [확장 하려면 다음 이미지를 클릭 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.jpg)
6. 검사를 **aspnetusers** 예를 들어 테이블에 새 사용자를 등록 하는 대로 항목에 대해 확인 합니다.

   [확장 하려면 다음 이미지를 클릭 합니다. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image26.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image25.png)
