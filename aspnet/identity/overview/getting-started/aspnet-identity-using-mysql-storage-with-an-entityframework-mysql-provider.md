---
uid: identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
title: ": ASP.NET Identity EntityFramework MySQL 공급자 (C#)와 함께 MySQL 저장소를 사용 하 여 | Microsoft Docs"
author: maumar
description: "이 자습서에서는 MySQL 견실한와 EntityFramework (SQL 클라이언트 공급자)으로 ASP.NET Identity에 대 한 기본 데이터 저장소 메커니즘을 바꾸는 방법을 보여 줍니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/10/2013
ms.topic: article
ms.assetid: 15253312-a92c-43ba-908e-b5dacd3d08b8
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
msc.type: authoredcontent
ms.openlocfilehash: ac254abcb756d048d159a9b67967a581f35ac871
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider-c"></a>: ASP.NET Identity EntityFramework MySQL 공급자 (C#) MySQL 저장소 사용
====================
여 [Maurycy Markowski](https://github.com/maumar), [Raquel Soares De Almeida](https://github.com/raquelsa), [Robert McMurray](https://github.com/rmcmurray)

> 이 자습서에 대 한 기본 데이터 저장소 메커니즘을 대체 하는 방법을 보여 줍니다. [ **ASP.NET Identity** ](introduction-to-aspnet-identity.md) EntityFramework (SQL 클라이언트 공급자)는 MySQL 공급자와 함께 사용 합니다.


이 자습서는 다음 항목 설명 합니다.

- Azure에서 MySQL 데이터베이스 만들기
- Visual Studio 2013 MVC 템플릿을 사용 하 여 MVC 응용 프로그램 만들기
- EntityFramework MySQL 데이터베이스 공급자와 작동 하도록 구성
- 결과 확인 하려면 응용 프로그램 실행

이 자습서를 마치면 나면 MVC 응용 프로그램을 ASP.NET Identity 저장 Azure에서 호스팅하는 MySQL 데이터베이스를 사용 하는 합니다.

## <a name="creating-a-mysql-database-instance-on-azure"></a>Azure에서 MySQL 데이터베이스 인스턴스 만들기

1. 에 로그인 하 고 [Azure 포털](https://go.microsoft.com/fwlink/?linkid=529715&amp;clcid=0x409)합니다.
2. 클릭 **새로** 페이지 및 다음 선택의 맨 아래에 **저장소**:  
  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.png)
3. 에 **선택 및 추가 기능** 선택 마법사 **ClearDB MySQL 데이터베이스**, 클릭 하 고는 **다음** 프레임의 아래쪽 화살표:  
  
 [확장 하려면 다음 이미지를 클릭 합니다. ]  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.png)
4. 기본값을 유지 **무료** 변경, 계획 된 **이름** 를 **IdentityMySQLDatabase**영역을 가장 가까운 항목을 선택한 다음 클릭는 **다음** 프레임의 아래쪽 화살표:  
  
 [확장 하려면 다음 이미지를 클릭 합니다. ]  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.png)
5. 클릭는 **구매** 데이터베이스 만들기를 완료 하려면 확인 표시 합니다.  
  
 [확장 하려면 다음 이미지를 클릭 합니다. ]  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.png)
6. 데이터베이스를 만든 후에서 관리할 수 있습니다는 **추가 기능** 관리 포털에서 탭 합니다. 데이터베이스에 대 한 연결 정보를 검색 하려면 클릭 **연결 정보입니다.** 페이지의 맨 아래에 있습니다.  
  
 [확장 하려면 다음 이미지를 클릭 합니다. ]  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image10.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image9.png)
7. [복사] 단추를 클릭 하 여 연결 문자열을 복사는 **CONNECTIONSTRING** 필드 및 저장; MVC 응용 프로그램에 대 한이 자습서의 뒷부분에서이 정보를 사용 합니다.  
  
 [확장 하려면 다음 이미지를 클릭 합니다. ]  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image12.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image11.png)

## <a name="creating-an-mvc-application-project"></a>MVC 응용 프로그램 프로젝트 만들기

자습서의이 섹션의 단계를 완료 하려면 먼저 할 설치 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 또는 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)합니다. Visual Studio를 설치한 후 새 MVC 응용 프로그램 프로젝트를 만들려면 다음 단계를 사용 합니다.

1. Visual Studio 2013을 엽니다.
2. 클릭 **새 프로젝트** 에서 **시작** 페이지 또는 있습니다 클릭할 수는 **파일** 메뉴 차례로 **새 프로젝트**:  
  
 [확장 하려면 다음 이미지를 클릭 합니다. ]  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.jpg)
3. 경우는 **새 프로젝트** 대화 상자가 표시 됩니다, 확장 **Visual C#** 템플릿 목록에서 클릭 **웹**를 선택 하 고 **ASP.NET 웹 응용 프로그램**. 프로젝트 이름을 **IdentityMySQLDemo** 클릭 하 고 **확인**:  
  
 [확장 하려면 다음 이미지를 클릭 합니다. ]  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image14.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image13.png)
4. 에 **새 ASP.NET 프로젝트** 대화 상자에서는 **MVC** templatewith 기본 옵션; 이렇게 설정이 하면 구성 **개별 사용자 계정** 인증 방법으로 합니다. 클릭 **확인**:  
  
 [확장 하려면 다음 이미지를 클릭 합니다. ]  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image16.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image15.png)

## <a name="configure-entityframework-to-work-with-a-mysql-database"></a>MySQL 데이터베이스를 작성 하려면 EntityFramework 구성

### <a name="update-the-entity-framework-assembly-for-your-project"></a>프로젝트에 대 한 Entity Framework 어셈블리를 업데이트 합니다.

Visual Studio 2013 서식 파일에서 만든 MVC 응용 프로그램에 대 한 참조를 포함 된 [EntityFramework 6.0.0](http://www.nuget.org/packages/EntityFramework) 있어야 하지만 패키지 하 고, 업데이트를 해당 릴리스 이후 해당 어셈블리에 포함 된 중요 한 되었습니다 성능 향상입니다. 응용 프로그램에서 이러한 최신 업데이트를 사용 하려면 다음 단계를 사용 합니다.

1. Visual Studio 2013에서 MVC 프로젝트를 엽니다.
2. 클릭 **도구**, 클릭 **라이브러리 패키지 관리자**, 클릭 하 고 **패키지 관리자 콘솔**:  
  
 [확장 하려면 다음 이미지를 클릭 합니다. ]  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image18.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image17.png)
3. **패키지 관리자 콘솔** Visual Studio의 아래쪽 섹션에 표시 됩니다. 형식 &quot; **업데이트 패키지 EntityFramework** &quot; Enter 키를 누릅니다.  
  
 [확장 하려면 다음 이미지를 클릭 합니다. ]  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image20.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image19.png)

### <a name="install-the-mysql-provider-for-entityframework"></a>EntityFramework에 대 한 MySQL 공급자를 설치 합니다.

MySQL 데이터베이스에 연결 하는 EntityFramework MySQL 공급자를 설치 해야 합니다. 이 위해 열고는 **패키지 관리자 콘솔** 유형과 &quot; **Install-package MySql.Data.Entity 사전**&quot;, 한 다음 Enter 키를 누릅니다.

> [!NOTE]
> 어셈블리의 시험판 버전 이며 따라서 버그를 포함할 수 있습니다. 하지 프로덕션 환경에서 시험판 버전의 공급자를 사용 해야 합니다.


[다음 그림을 확장 하려면 클릭 합니다.]  
  
[![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image22.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image21.png)

### <a name="making-project-configuration-changes-to-the-webconfig-file-for-your-application"></a>프로젝트 구성을 변경 응용 프로그램에 대 한 Web.config 파일

방금 설치한 MySQL 공급자를 사용 하려면 Entity Framework를 구성 하는이 섹션에서는 MySQL 공급자 팩터리를 등록 하 고 Azure에서 연결 문자열을 추가 합니다.

> [!NOTE]
> 다음 예에서는 MySql.Data.dll에 대 한 특정 어셈블리 버전을 포함 합니다. 어셈블리 버전 변경 되는 경우에 올바른 버전으로 적절 한 구성 설정을 수정 해야 합니다.


1. Visual Studio 2013에서 프로젝트에 대 한 Web.config 파일을 엽니다.
2. Entity Framework에 대 한 기본 데이터베이스 공급자 및 팩터리를 정의 하는 다음 구성 설정을 찾습니다.

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample1.xml)]
3. 이러한 구성 설정을 MySQL 공급자를 사용 하려면 Entity Framework 구성에서 다음을 바꿉니다. 

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample2.xml)]
4. 찾을 &lt;connectionStrings&gt; 섹션 및 Azure에서 호스팅하는 MySQL 데이터베이스에 대 한 연결 문자열을 정의 합니다를 다음 코드로 바꿉니다 (providerName 값에서 변경도 원본):

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample3.xml?highlight=3-4)]

### <a name="adding-custom-migrationhistory-context"></a>사용자 지정 MigrationHistory 컨텍스트 추가

사용 하 여 entity Framework Code First는 **MigrationHistory** 테이블 모델 변경 내용을 추적 하 고 데이터베이스 스키마 및 개념 스키마 간의 일관성을 보장 합니다. 그러나이 테이블 작동 하지 않습니다 MySQL 용 기본적으로 기본 키가 너무 커서. 이 문제를 해결 하려면 해당 테이블에 대 한 키 크기를 축소 해야 합니다. 이렇게 하려면 다음 단계를 사용 합니다.

1. 이 테이블에 대 한 스키마 정보에서 캡처되는 **HistoryContext**, 모든 다른 수정할 수 있는 **DbContext**합니다. 이렇게 하려면 라는 새 클래스 파일 추가 **MySqlHistoryContext.cs** 을 프로젝트에 해당 내용을 다음 코드로 바꿉니다.

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample4.cs)]
2. 그런 다음 수정 된 사용 하려면 Entity Framework를 구성 해야 합니다 **HistoryContext**, 기본 대신 합니다. 코드 기반 구성 기능을 활용 하 여이 작업을 수행할 수 있습니다. 이렇게 하려면 라는 새 클래스 파일 추가 **MySqlConfiguration.cs** 프로젝트 및 그 내용을 바꾸기:

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample5.cs)]

### <a name="creating-a-custom-entityframework-initializer-for-applicationdbcontext"></a>ApplicationDbContext에 대 한 사용자 지정 EntityFramework 이니셜라이저 만들기

데이터베이스에 연결 하기 위해 모델 이니셜라이저를 사용 해야이 자습서에서는 추천 목록에 MySQL 공급자 Entity Framework 마이그레이션의 현재 지원 하지 않습니다. 이 자습서에서는 Azure에서 MySQL 인스턴스를 사용 하는, 때문에 사용자 지정 Entity Framework 이니셜라이저 만들 해야 필요 합니다.

> [!NOTE]
> Azure 또는 온-프레미스에서 호스트 된 데이터베이스를 사용 하는 경우에 SQL Server 인스턴스에 연결 하는 경우에이 단계가 필요 하지 않습니다.


MySQL에 대 한 사용자 지정 Entity Framework 이니셜라이저를 만들려면 다음 단계를 사용 합니다.

1. 라는 새 클래스 파일 추가 **MySqlInitializer.cs** 프로젝트 및 바꾸기를 다음 코드를 사용 하 여 콘텐츠: 

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample6.cs?highlight=23)]
2. 열기는 **IdentityModels.cs** 파일에 있는 프로젝트에 대해는 **모델** 디렉터리의 내용을 다음으로 바꿉니다. 

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample7.cs)]

## <a name="running-the-application-and-verifying-the-database"></a>응용 프로그램을 실행 하 고 데이터베이스를 확인 하는 중

이전 섹션의 단계를 완료 후 데이터베이스를 테스트 해야 합니다. 이렇게 하려면 다음 단계를 사용 합니다.

1. 키를 눌러 **Ctrl + f 5를 눌러** 작성 하 고 웹 응용 프로그램을 실행 합니다.
2. 클릭는 **등록** 페이지 위쪽의 탭:  
  
 [확장 하려면 다음 이미지를 클릭 합니다. ]  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.jpg)
3. 새 사용자 이름 및 암호를 입력 한 다음 클릭 **등록**:  
  
 [확장 하려면 다음 이미지를 클릭 합니다. ]  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image24.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image23.png)
4. 이 시점에서 ASP.NET Identity 테이블은에서 MySQL 데이터베이스 만들어지고 사용자가 등록 하 고 응용 프로그램에 로그인:  
  
 [확장 하려면 다음 이미지를 클릭 합니다. ]  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.jpg)

### <a name="installing-mysql-workbench-tool-to-verify-the-data"></a>데이터를 확인 하려면 MySQL 워크 벤치 도구 설치

1. 설치는 **MySQL 워크 벤치** 에서 도구는 [MySQL 다운로드 페이지](http://dev.mysql.com/downloads/windows/installer/)
2. 설치 마법사에서: **기능 선택** 탭에서 **MySQL 워크 벤치** 아래 **응용 프로그램** 섹션.
3. 응용 프로그램을 실행 하 고이 자습서의 말아달라 때 만든 Azure의 MySQL 데이터베이스의 연결 문자열 데이터를 사용 하 여 새 연결을 추가 합니다.
4. 연결을 만든 후 검사는 **ASP.NET Identity** 에 생성 된 테이블은 **IdentityMySQLDatabase 합니다.**
5. 모든 ASP.NET Identity 필요한 아래 이미지에 표시 된 대로 테이블을 만들 수 있는지 확인할 수 있습니다.  
  
 [확장 하려면 다음 이미지를 클릭 합니다. ]  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.jpg)
6. 검사는 **aspnetusers** 테이블 예를 들어 새 사용자를 등록할 때 항목을 확인 합니다.  
  
 [확장 하려면 다음 이미지를 클릭 합니다. ]  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image26.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image25.png)
