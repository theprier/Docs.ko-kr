---
uid: identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
title: MySQL 사용자 지정 ASP.NET Identity 저장소 공급자 구현 | Microsoft Docs
author: raquelsa
description: ASP.NET Id는 확장 가능한 시스템으로의 응용 프로그램 작업이 다시 실행 하지 않고 응용 프로그램에 연결 하 고 저장소 공급자를 만들 수 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/22/2015
ms.topic: article
ms.assetid: 248f5fe7-39ba-40ea-ab1e-71a69b0bd649
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
msc.type: authoredcontent
ms.openlocfilehash: d843b31e011fe520aad6cfdab0beca2d12477f12
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30872740"
---
<a name="implementing-a-custom-mysql-aspnet-identity-storage-provider"></a>MySQL 사용자 지정 ASP.NET Identity 저장소 공급자 구현
====================
여 [Raquel Soares De Almeida](https://github.com/raquelsa), [Suhas Joshi](https://github.com/suhasj), [Tom FitzMacken](https://github.com/tfitzmac)

> ASP.NET Id는 확장 가능한 시스템 응용 프로그램 작업이 다시 실행 하지 않고 응용 프로그램에 연결 하 고 저장소 공급자를 만들 수 있습니다. 이 항목에서는 ASP.NET Identity에 대 한 MySQL 저장소 공급자를 만드는 방법을 설명 합니다. 사용자 지정 저장소 공급자를 만드는 방법의 개요를 참조 하십시오. [개요의 사용자 지정 저장소에 대 한 공급자 ASP.NET Identity](overview-of-custom-storage-providers-for-aspnet-identity.md)합니다.
> 
> 이 자습서를 완료 하려면 Visual Studio 2013 업데이트 2에 있어야 합니다.
> 
> 이 자습서 수행합니다.
> 
> - Azure에서 MySQL 데이터베이스 인스턴스를 만드는 방법을 보여 줍니다.
> - MySQL 클라이언트 도구 (MySQL 워크 벤치)를 사용 하 여 테이블을 만들고 Azure에서 원격 데이터베이스를 관리 하는 방법을 보여 줍니다.
> - ASP.NET Id 저장소 구현을 기본 MVC 응용 프로그램 프로젝트에 사용자 지정 구현을으로 바꾸는 방법을 보여 줍니다.
> 
> 이 자습서 Raquel Soares De Almeida Rick Anderson로 기록 되었으나 ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) ). 샘플 프로젝트 Suhas Joshi Identity 2.0에 대 한 업데이트 했습니다. 항목은 Tom FitzMacken Identity 2.0에 대 한 업데이트 했습니다.


## <a name="download-completed-project"></a>다운로드가 완료 프로젝트

이 자습서의 끝으로 Azure에서 호스트 되는 MySQL 데이터베이스를 사용 하는 ASP.NET Identity MVC 응용 프로그램 프로젝트를 해야 합니다.

완료 된 MySQL 저장소 공급자를 다운로드할 수 있습니다 [AspNet.Identity.MySQL (CodePlex)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/)합니다.

## <a name="the-steps-you-will-perform"></a>수행 하는 단계

이 자습서에서는 다음을 수행합니다.

1. Azure에서 MySQL 데이터베이스 만들기
2. MySQL에 ASP.NET Identity 테이블을 만들기
3. MVC 응용 프로그램 만들기 및 MySQL 공급자를 사용 하도록 구성
4. 앱 실행

이 항목의 아키텍처는 결정 해야 하는 고객 저장소 공급자를 구현 하는 경우와 ASP.NET Identity를 다루지 않습니다. 해당 정보를 참조 하십시오. [개요의 사용자 지정 저장소에 대 한 공급자 ASP.NET Identity](overview-of-custom-storage-providers-for-aspnet-identity.md)합니다.

## <a name="review-mysql-storage-provider-classes"></a>MySQL 저장소 공급자 클래스를 검토 합니다.

MySQL 저장소 공급자를 만드는 단계를 시작 하기 전에 살펴 보겠습니다 저장소 공급자를 구성 하는 클래스입니다. 데이터베이스 작업을 관리 하는 클래스 및 사용자 및 역할 관리 응용 프로그램에서 호출 하는 클래스가 필요 합니다.

### <a name="storage-classes"></a>저장소 클래스

- [IdentityUser](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/IdentityUser.cs) -사용자에 대 한 속성을 포함 합니다.
- [UserStore](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserStore.cs) -추가, 업데이트 또는 사용자 검색에 대 한 작업을 포함 합니다.
- [IdentityRole](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/IdentityRole.cs) -역할에 대 한 속성을 포함 합니다.
- [RoleStore](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/RoleStore.cs) -추가, 삭제, 업데이트 및 역할을 검색 하기 위한 작업이 포함 되어 있습니다.

### <a name="data-access-layer-classes"></a>데이터 액세스 계층 클래스

이 예제에 대 한 데이터 액세스 계층 클래스는 테이블; 작업에 대 한 SQL 문을 포함 하지만, 코드에서 Entity Framework 또는 NHibernate 등 개체-관계형 매핑 ORM ()를 사용 하도록 필요할 수 있습니다. 특히, 응용 프로그램 지연 로드 및 캐시 개체를 포함 하는 ORM 없이 성능 저하를 발생할 수 있습니다. 자세한 내용은 참조 [Entity Framework 없이 ASP.NET Identity 2.0?](https://aspnetidentity.codeplex.com/discussions/561828)

- [MySQLDatabase](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) -MySQL 데이터베이스 연결 및 데이터베이스 작업을 수행 하기 위한 메서드를 포함 합니다. UserStore 및 RoleStore이이 클래스의 인스턴스로 인스턴스화됩니다.
- [RoleTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/RoleTable.cs) -역할을 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.
- [UserClaimsTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) -사용자 클레임을 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.
- [UserLoginsTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) -사용자 로그인 정보를 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.
- [UserRoleTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) -있는 역할에 할당 되는 사용자를 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.
- [UserTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserTable.cs) -사용자가 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.

## <a name="create-a-mysql-database-instance-on-azure"></a>Azure에서 MySQL 데이터베이스 인스턴스 만들기

1. 에 로그인 하 고 [Azure 포털](https://manage.windowsazure.com/)합니다.
2. 클릭 **+ 새로 만들기** 페이지 및 다음 선택의 맨 아래에 **저장소**합니다.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.png)
3. 에 **선택 및 추가 기능** 선택 마법사 **ClearDB MySQL 데이터베이스** 대화 상자의 오른쪽 맨 아래에 있는 다음 화살표를 클릭 하 고 있습니다.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.png)
4. 기본값을 유지 **무료** 계획 하 고 변경 된 **이름** 를 **IdentityMySQLDatabase**합니다. 가장 가까운 지역을 선택 하 고 화살표를 클릭 합니다.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.png)
5. 데이터베이스 만들기를 완료 하 고 확인 표시를 클릭 합니다.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image4.png)
6. 데이터베이스를 만든 후에서 관리할 수 있습니다는 **추가 기능** 관리 포털에서 탭 합니다.   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image5.png)
7. 클릭 하 여 데이터베이스 연결 정보를 얻을 수 **연결 정보입니다.** 페이지의 맨 아래에 있습니다.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image6.png)
8. 복사 단추를 클릭 하 여 연결 문자열을 복사 하 고 나중에 MVC 응용 프로그램에서 사용할 수 있도록 저장 합니다.   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image7.png)

## <a name="create-the-aspnet-identity-tables-in-a-mysql-database"></a>MySQL 데이터베이스에 ASP.NET Identity 테이블을 만들기

### <a name="install-mysql-workbench-tool-to-connect-and-manage-mysql-database"></a>연결 하 고 MySQL 데이터베이스를 관리할 MySQL 워크 벤치 도구 설치

1. 설치는 **MySQL 워크 벤치** 에서 도구는 [MySQL 다운로드 페이지](http://dev.mysql.com/downloads/windows/installer/)
2. 응용 프로그램을 실행 하 고, 클릭에 추가 **MySQLConnections +** 단추를 새 연결을 추가 합니다. 이 자습서의 앞부분에서 만든 Azure의 MySQL 데이터베이스에서 복사 하는 연결 문자열 데이터를 사용 합니다.
3. 연결을 만든 후 새 엽니다 **쿼리** 탭, 붙여넣기에서 명령을 [MySQLIdentity.sql](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql) 쿼리로 하 고 데이터베이스 테이블을 만들기 위해 실행 합니다.
4. ASP.NET Identity 필요한 모든 테이블 아래와 같이 Azure에서 호스트 되는 MySQL 데이터베이스에 생성 해야 합니다.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.jpg)

## <a name="create-an-mvc-application-project-from-template-and-configure-it-to-use-mysql-provider"></a>템플릿에서 MVC 응용 프로그램 프로젝트를 만들고 MySQL 공급자를 사용 하도록 구성

필요한 경우 하나를 설치 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 또는 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) 업데이트 2입니다.

### <a name="download-the-aspnetidentitymysql-project-from-codeplex"></a>CodePlex에서 ASP.NET.Identity.MySQL 프로젝트를 다운로드 합니다.

1. 저장소 URL로 이동 [AspNet.Identity.MySQL (CodePlex)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/)합니다.
2. 소스 코드를 다운로드 합니다.
3. 로컬 폴더에.zip 파일을 다운로드 합니다.
4. AspNet.Identity.MySQL 솔루션을 열을 포함 합니다.

### <a name="create-a-new-mvc-application-project-from-template"></a>서식 파일에서 새 MVC 응용 프로그램 프로젝트 만들기

1. 마우스 오른쪽 단추로 클릭 하 고 **AspNet.Identity.MySQL** 솔루션 및 **추가**, **새 프로젝트**
2. 에 **새 프로젝트 추가** 대화 선택 **Visual C#** 다음 왼쪽에 **웹** 선택한 후 **ASP.NET 웹 응용 프로그램**합니다. 프로젝트 이름을 **IdentityMySQLDemo**; 한 다음 확인을 클릭 합니다.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.jpg)
3. 에 **새 ASP.NET 프로젝트** 대화 상자에서 기본 옵션으로 MVC 템플릿을 선택 (포함 된 **개별 사용자 계정** 인증 방법으로)를 클릭 하 고 **확인** .![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.jpg)
4. 솔루션 탐색기에서 IdentityMySQLDemo 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리**합니다. 검색 텍스트 상자 대화 상자에 입력 **Identity.EntityFramework**합니다. 결과 목록에서이 패키지를 선택한 다음 클릭 **제거**합니다. EntityFramework 종속성 패키지를 제거 하 라는 메시지가 표시 됩니다. 예를 클릭에서는 더 이상이 응용 프로그램에서이 패키지 됩니다.
5. IdentityMySQLDemo 프로젝트를 마우스 오른쪽 단추로 클릭, 선택 **추가**, **참조, 솔루션, 프로젝트;** AspNet.Identity.MySQL 프로젝트를 선택 하 고 클릭 **확인**합니다.
6. IdentityMySQLDemo 프로젝트에서 대체에 대 한 모든 참조  
    `using Microsoft.AspNet.Identity.EntityFramework;`  
   다음 문자열로 바꾸세요.  
     `using AspNet.Identity.MySQL;`
7. IdentityModels.cs, 설정 **ApplicationDbContext** 를 파생할 **MySqlDatabase** 하 고 있는 연결 이름 단일 매개 변수를 사용 하는 생성자를 포함 합니다.  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample1.cs)]
8. IdentityConfig.cs 파일을 엽니다. 에 **ApplicationUserManager.Create** 메서드, UserManager를 다음 코드로 인스턴스화 바꾸기:  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample2.cs)]
9. Web.config 파일을 열고 DefaultConnection 문자열과 이전 단계에서 만든 MySQL 데이터베이스의 연결 문자열을 바꿀 값이 강조 표시 된이 항목으로 대체 합니다.  

    [!code-xml[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample3.xml?highlight=2)]

## <a name="run-the-app-and-connect-to-the-mysql-db"></a>응용 프로그램을 실행 하 고 MySQL DB에 연결

1. 마우스 오른쪽 단추로 클릭 하 고 **IdentityMySQLDemo** 프로젝트를 마우스 선택 **시작 프로젝트로 설정**
2. 키를 눌러 **Ctrl + f 5를 눌러** 작성 하 고 응용 프로그램을 실행 합니다.
3. 클릭 **등록** 페이지 위쪽의 탭 합니다.
4. 새 사용자 이름 및 암호를 입력 한 후에 클릭 **등록**합니다.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image8.png)
5. 이제 새 사용자 등록 되 고 로그인 합니다.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image9.png)
6. MySQL 워크 벤치 도구도 돌아가서를 검사 하는 **IdentityMySQLDatabase** 테이블의 내용입니다. 새 사용자 등록 항목에 대 한 사용자 테이블을 검사 합니다.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image10.png)

## <a name="next-steps"></a>다음 단계

이 앱에 다른 인증 방법을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 참조 [Facebook, Google OAuth2 및 OpenID 로그온 ASP.NET MVC 5 응용 프로그램을 만들](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)합니다.

DB OAuth와 통합 하 고 응용 프로그램에 대 한 사용자 액세스를 제한 하려면 역할을 설정 하는 방법에 자세한 내용은 [azure SQL 데이터베이스 멤버 자격, OAuth와 Secure ASP.NET MVC 5 앱을 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다.
