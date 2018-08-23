---
uid: identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
title: 사용자 지정 MySQL ASP.NET Id 저장소 공급자 구현 | Microsoft Docs
author: raquelsa
description: ASP.NET Id는 사용자 고유의 저장소 공급자를 만들고 응용은 작업이 다시 실행 하지 않고 응용 프로그램에 연결할 수 있는 확장 가능한 시스템...
ms.author: riande
ms.date: 05/22/2015
ms.assetid: 248f5fe7-39ba-40ea-ab1e-71a69b0bd649
msc.legacyurl: /identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
msc.type: authoredcontent
ms.openlocfilehash: 358b1a3b7277f21c63a1d395f2a5fce79bbe0d56
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838201"
---
<a name="implementing-a-custom-mysql-aspnet-identity-storage-provider"></a>사용자 지정 MySQL ASP.NET Id 저장소 공급자 구현
====================
하 여 [Raquel Soares De Almeida](https://github.com/raquelsa)하십시오 [Suhas Joshi](https://github.com/suhasj), [Tom FitzMacken](https://github.com/tfitzmac)

> ASP.NET Id는 확장 가능한 시스템 사용자 고유의 저장소 공급자를 만들고 응용 프로그램을 다시 사용 하지 않고 응용 프로그램에 연결할 수 있습니다. 이 항목에서는 ASP.NET Id에 대 한 MySQL 저장소 공급자를 만드는 방법을 설명 합니다. 사용자 지정 저장소 공급자를 만드는 개요를 참조 하세요 [개요의 사용자 지정 저장소 공급자 ASP.NET Id에 대 한](overview-of-custom-storage-providers-for-aspnet-identity.md)합니다.
> 
> 이 자습서를 완료 하려면 Visual Studio 2013 업데이트 2를 사용 하 여 있어야 합니다.
> 
> 이 자습서는:
> 
> - Azure에서 MySQL 데이터베이스 인스턴스를 만드는 방법을 보여 줍니다.
> - MySQL 클라이언트 도구 (MySQL Workbench)를 사용 하 여 테이블을 만들고 Azure에서 원격 데이터베이스를 관리 하는 방법을 보여 줍니다.
> - ASP.NET Id 저장소 구현을 기본 MVC 응용 프로그램 프로젝트에서 사용자 지정 구현으로 대체 하는 방법을 보여 줍니다.
> 
> 이 자습서가 원래 Raquel Soares De Almeida 및 Rick Anderson으로 작성 됩니다 ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) ). 샘플 프로젝트는 Suhas Joshi에서 Identity 2.0에 대 한 업데이트 했습니다. 항목은 Tom FitzMacken에서 Identity 2.0에 대 한 업데이트 했습니다.


## <a name="download-completed-project"></a>다운로드가 완료 된 프로젝트

이 자습서의 끝 MVC 응용 프로그램 프로젝트를 Azure에서 호스트 되는 MySQL 데이터베이스를 사용 하는 ASP.NET id로 지정 해야 합니다.

완료 된 MySQL 저장소 공급자를 다운로드할 수 있습니다 [AspNet.Identity.MySQL (CodePlex)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/)합니다.

## <a name="the-steps-you-will-perform"></a>수행 하는 단계

이 자습서에서는 다음을 수행 해야합니다.

1. Azure에서 MySQL 데이터베이스 만들기
2. MySQL에 ASP.NET Id 테이블 만들기
3. MVC 응용 프로그램을 만들고 MySQL 공급자를 사용 하도록 구성
4. 앱 실행

이 항목에서는 ASP.NET Id 및 고객 저장소 공급자를 구현 하는 경우 해야 결정의 아키텍처를 다루지 않습니다. 해당 정보를 참조 하세요 [개요의 사용자 지정 저장소 공급자 ASP.NET Id에 대 한](overview-of-custom-storage-providers-for-aspnet-identity.md)합니다.

## <a name="review-mysql-storage-provider-classes"></a>MySQL 저장소 공급자 클래스를 검토 합니다.

MySQL 저장소 공급자를 만드는 단계에 들어가기 전에 살펴보겠습니다 저장소 공급자를 구성 하는 클래스입니다. 데이터베이스 작업을 관리 하는 클래스 및 사용자 및 역할 관리 응용 프로그램에서 호출 되는 클래스 해야 합니다.

### <a name="storage-classes"></a>저장소 클래스

- [IdentityUser](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/IdentityUser.cs) -사용자에 대 한 속성을 포함 합니다.
- [UserStore](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserStore.cs) -추가, 업데이트 또는 사용자 검색에 대 한 작업을 포함 합니다.
- [IdentityRole](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/IdentityRole.cs) -역할에 대 한 속성을 포함 합니다.
- [RoleStore](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/RoleStore.cs) -추가, 삭제, 업데이트 및 역할을 검색 하는 작업이 포함 됩니다.

### <a name="data-access-layer-classes"></a>데이터 액세스 계층 클래스

예를 들어 데이터 액세스 계층 클래스는 테이블; 작업에 대 한 SQL 문을 포함 그러나 코드에서 Entity Framework 또는 NHibernate 같은 개체-관계형 매핑 (ORM)를 사용 수 있습니다. 특히, 응용 프로그램 지연 로드 및 개체 캐싱을 포함 하는 ORM 없이 성능 저하를 발생할 수 있습니다. 자세한 내용은 참조 하세요. [Entity Framework 없이 ASP.NET Identity 2.0?](https://aspnetidentity.codeplex.com/discussions/561828)

- [MySQLDatabase](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) -MySQL 데이터베이스 연결 및 데이터베이스 작업을 수행 하기 위한 메서드를 포함 합니다. UserStore 및 RoleStore이이 클래스의 인스턴스를 사용 하 여 인스턴스화됩니다.
- [RoleTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/RoleTable.cs) -역할을 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.
- [UserClaimsTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) -사용자 클레임을 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.
- [UserLoginsTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) -사용자 로그인 정보를 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.
- [UserRoleTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) -역할에 할당 된 사용자를 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.
- [UserTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserTable.cs) -사용자를 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.

## <a name="create-a-mysql-database-instance-on-azure"></a>Azure에서 MySQL 데이터베이스 인스턴스 만들기

1. [Azure Portal](https://manage.windowsazure.com/)에 로그인합니다.
2. 클릭 **+ 새로 만들기** 한 다음 선택한 페이지의 맨 아래에서 **스토어**합니다.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.png)
3. 에 **선택 및 추가 기능** 마법사 **ClearDB MySQL 데이터베이스** 대화의 오른쪽 맨 아래에 있는 다음 화살표를 클릭 합니다.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.png)
4. 기본값을 유지 **무료** 계획 하 고 변경 합니다 **이름** 하 **IdentityMySQLDatabase**합니다. 가장 가까운 지역을 선택 하 고 화살표를 클릭 합니다.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.png)
5. 데이터베이스 만들기를 완료 하려면 확인 표시를 클릭 합니다.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image4.png)
6. 데이터베이스를 만든 후에서 관리할 수 있습니다 합니다 **추가 기능** 관리 포털에서 탭 합니다.   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image5.png)
7. 클릭 하 여 데이터베이스 연결 정보를 가져올 수 있습니다 **연결 정보** 페이지의 맨 아래에 있습니다.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image6.png)
8. 복사 단추를 클릭 하 여 연결 문자열을 복사 하 고 나중에 MVC 응용 프로그램에서 사용할 수 있도록 저장 합니다.   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image7.png)

## <a name="create-the-aspnet-identity-tables-in-a-mysql-database"></a>MySQL 데이터베이스에 ASP.NET Id 테이블 만들기

### <a name="install-mysql-workbench-tool-to-connect-and-manage-mysql-database"></a>MySQL Workbench 연결 하 여 MySQL 데이터베이스를 관리 하는 도구를 설치 합니다.

1. 설치 합니다 **MySQL Workbench** 에서 도구는 [MySQL 다운로드 페이지](http://dev.mysql.com/downloads/windows/installer/)
2. 앱을 시작 하 고 클릭에 추가 합니다 **MySQLConnections +** 단추를 새 연결을 추가 합니다. 이 자습서의 앞부분에서 만든 Azure MySQL 데이터베이스에서 복사한 연결 문자열 데이터를 사용 합니다.
3. 연결을 만든 후 새 엽니다 **쿼리** 탭,에서 명령을 붙여 [MySQLIdentity.sql](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql) 쿼리로 데이터베이스 테이블을 만들기 위해 실행 합니다.
4. 이제 ASP.NET Id 필요한 모든 테이블 아래와 같이 Azure에서 호스트 되는 MySQL 데이터베이스에 생성 해야 합니다.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.jpg)

## <a name="create-an-mvc-application-project-from-template-and-configure-it-to-use-mysql-provider"></a>템플릿에서 MVC 응용 프로그램 프로젝트를 만들고 MySQL 공급자를 사용 하도록 구성

필요한 경우 설치할 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 하거나 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) 업데이트 2를 사용 하 여 합니다.

### <a name="download-the-aspnetidentitymysql-project-from-codeplex"></a>CodePlex의 ASP.NET.Identity.MySQL 프로젝트를 다운로드 합니다.

1. 리포지토리 URL로 이동 [AspNet.Identity.MySQL (CodePlex)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/)합니다.
2. 소스 코드를 다운로드 합니다.
3. 로컬 폴더에.zip 파일을 추출 합니다.
4. AspNet.Identity.MySQL 솔루션을 열고 빌드하십시오.

### <a name="create-a-new-mvc-application-project-from-template"></a>템플릿에서 새 MVC 응용 프로그램 프로젝트 만들기

1. 마우스 오른쪽 단추로 클릭 합니다 **AspNet.Identity.MySQL** 솔루션 및 **추가**, **새 프로젝트**
2. 에 **새 프로젝트 추가** 대화 상자 선택 **Visual C#** 왼쪽에서 다음 **웹** 선택한 후 **ASP.NET 웹 응용 프로그램**합니다. 프로젝트 이름을 **IdentityMySQLDemo**; 확인을 클릭 하 고 있습니다.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.jpg)
3. 에 **새 ASP.NET 프로젝트** 대화 상자에서 기본 옵션을 사용 하 여 MVC 템플릿을 선택 (포함 하는 **개별 사용자 계정** 인증 방법으로)를 클릭 하 고 **확인** .![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.jpg)
4. 솔루션 탐색기에서 IdentityMySQLDemo 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리**합니다. 검색 텍스트 상자 대화 상자에서 입력 **Identity.EntityFramework**합니다. 결과 목록에서이 패키지를 선택 하 고 클릭 **제거**합니다. EntityFramework 종속성 패키지를 제거 하 라는 메시지가 표시 됩니다. 예를 클릭이 응용 프로그램에서이 패키지는 더 이상.
5. IdentityMySQLDemo 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음를 선택 합니다 **추가**하십시오 **참조, 솔루션, 프로젝트** AspNet.Identity.MySQL 프로젝트를 선택 하 고 클릭 **확인**합니다.
6. IdentityMySQLDemo 프로젝트에 대 한 모든 참조를 대체  
    `using Microsoft.AspNet.Identity.EntityFramework;`  
   다음 문자열로 바꾸세요.  
     `using AspNet.Identity.MySQL;`
7. IdentityModels.cs를 설정 **ApplicationDbContext** 에서 파생 시키는 **MySqlDatabase** 연결 이름이 단일 매개 변수를 사용 하는 생성자를 포함 합니다.  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample1.cs)]
8. IdentityConfig.cs 파일을 엽니다. 에 **ApplicationUserManager.Create** 메서드를 다음 코드를 사용 하 여 UserManager 인스턴스화 바꾸기:  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample2.cs)]
9. Web.config 파일을 열고이 항목의 이전 단계에서 만든 MySQL 데이터베이스 연결 문자열을 사용 하 여 강조 표시 된 값 대체를 사용 하 여 DefaultConnection 문자열을 바꿉니다.  

    [!code-xml[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample3.xml?highlight=2)]

## <a name="run-the-app-and-connect-to-the-mysql-db"></a>앱을 실행 하 고 MySQL DB에 연결

1. 마우스 오른쪽 단추로 클릭 합니다 **IdentityMySQLDemo** 프로젝트를 마우스 **시작 프로젝트로 설정**
2. 키를 눌러 **ctrl+f5** 를 빌드하고 앱을 실행 합니다.
3. 클릭할 **등록** 페이지 위쪽의 탭 합니다.
4. 새 사용자 이름 및 암호를 입력 하 고 클릭 **등록**합니다.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image8.png)
5. 이제 새 사용자 등록 되 고 로그인 합니다.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image9.png)
6. MySQL Workbench 도구로 다시 이동 하 고 검사 합니다 **IdentityMySQLDatabase** 테이블의 내용입니다. 새 사용자를 등록 하는 대로 항목에 대 한 사용자 테이블을 검사 합니다.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image10.png)

## <a name="next-steps"></a>다음 단계

이 앱에 다른 인증 방법을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 참조 [Facebook 및 Google OAuth2 및 OpenID Sign on을 사용 하 여 ASP.NET MVC 5 앱 만들기](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)합니다.

OAuth를 사용 하 여 DB를 통합 하 고 앱에 대 한 사용자 액세스를 제한 하려면 역할을 설정 하는 방법에 알아보려면 참조 [멤버 자격, OAuth 및 SQL Database를 사용 하 여 보안 ASP.NET MVC 5 앱을 Azure에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다.
