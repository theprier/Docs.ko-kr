---
uid: identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity
title: "SQL 멤버 자격에서 ASP.NET Id로 기존 웹 사이트를 마이그레이션 | Microsoft Docs"
author: Rick-Anderson
description: "이 자습서에서는를 사용자와 역할 데이터를 새 ASP.NET Identity의 SQL 멤버 자격을 사용 하 여 만든 기존 웹 응용 프로그램을 마이그레이션하는 단계 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/19/2014
ms.topic: article
ms.assetid: 220d3d75-16b2-4240-beae-a5b534f06419
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 3638c6779a0fcedaaa49623126b28ecf09a4954f
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="migrating-an-existing-website-from-sql-membership-to-aspnet-identity"></a>ASP.NET Id로 기존 웹 사이트 SQL 멤버 자격에서 마이그레이션
====================
여 [Rick Anderson](https://github.com/Rick-Anderson), [Suhas Joshi](https://github.com/suhasj)

> 이 자습서를 사용자와 역할 데이터를 새로운 ASP.NET Identity 시스템 SQL 멤버 자격을 사용 하 여 만든 기존 웹 응용 프로그램을 마이그레이션하는 단계를 보여 줍니다. ASP.NET Id 및 이전/새 클래스를 해당에서 후크 필요한 하나에 기존 데이터베이스 스키마를 변경 하는 것이 방법은 수 있습니다. 데이터베이스 마이그레이션 후이 방식을 채택, 향후 업데이트 하는 Id에 손쉽게 처리 됩니다.


이 자습서에 대 한 사용자 및 역할 데이터를 만들려면 Visual Studio 2010을 사용 하 여 만든 웹 응용 프로그램 템플릿 (Web Forms) 해당 메뉴로 이동 합니다. Id 시스템에 필요한 테이블에 기존 데이터베이스를 마이그레이션하려면 다음 SQL 스크립트 사용 합니다. 그런 다음 필요한 NuGet 패키지 설치 알아보고 멤버 자격 관리에는 Id 시스템을 사용 하는 새 계정 관리 페이지를 추가 하겠습니다. 마이그레이션 테스트로 SQL 멤버 자격을 사용 하 여 만든 사용자가 로그인 할 수 있어야 합니다. 및 새 사용자가 등록할 수 있어야 합니다. 전체 샘플을 찾을 수 있습니다 [여기](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/SQLMembership-Identity-OWIN/)합니다. 참고 항목 [ASP.NET Identity에서 ASP.NET 멤버 자격 마이그레이션](http://travis.io/blog/2015/03/24/migrate-from-aspnet-membership-to-aspnet-identity.html)합니다.

## <a name="getting-started"></a>시작

### <a name="creating-an-application-with-sql-membership"></a>SQL 멤버 자격을 사용 하 여 응용 프로그램 만들기

1. SQL 멤버 자격을 사용 하 여 이며 사용자 및 역할 데이터를 포함 하는 기존 응용 프로그램으로 시작 해야 합니다. 이 문서 Visual Studio 2010에서 웹 응용 프로그램을 만들어 보겠습니다.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image1.jpg)
2. ASP.NET 구성 도구를 사용 하 여 사용자 2 명이 만들: **oldAdminUser** 및 **oldUser 합니다.**

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image1.png)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image2.jpg)
3. 관리자 라고 하는 역할을 만들고 해당 역할에 사용자로 'oldAdminUser'를 추가 합니다.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image2.png)
4. Default.aspx를 사용 하면 사이트의 관리 섹션을 만듭니다. 관리자 역할의 사용자 에게만 액세스를 사용 하도록 설정 하려면 web.config 파일에 권한 부여 태그를 설정 합니다. 자세한 내용은 여기에서 찾을 수 있습니다 [https://www.asp.net/web-forms/tutorials/security/roles/role-based-authorization-cs](../../../web-forms/overview/older-versions-security/roles/role-based-authorization-cs.md)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image3.png)
5. SQL 멤버 자격 시스템에서 만든 테이블을 이해 하려면 서버 탐색기에서 데이터베이스를 봅니다. 에 aspnet 사용자 로그인 데이터가 저장 되\_사용자 및 aspnet\_역할 데이터는 aspnet에 저장 하는 동안 멤버 자격 테이블\_역할 테이블입니다. 에 대 한 사용자가 어떤 역할 aspnet에 저장 된 정보\_UsersInRoles 테이블입니다. 기본 회원 관리에 대 한 것으로 ASP.NET Identity 시스템에 위의 테이블의 정보를 이식 하 충분 합니다.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image4.png)

### <a name="migrating-to-visual-studio-2013"></a>Visual Studio 2013로 마이그레이션

1. 웹 또는와 함께 Visual Studio 2013 용 Visual Studio Express 2013을 설치는 [최신 업데이트](https://www.microsoft.com/download/details.aspx?id=44921)합니다.
2. 설치 된 버전의 Visual Studio에서 위의 프로젝트를 엽니다. SQL Server Express 설치 되어 있지 않으면 컴퓨터에, 연결 문자열에서 SQL Express를 사용 하기 때문에 프로젝트를 열 때 메시지가 표시 됩니다. SQL Express를 설치 하거나로 해결 변경 LocalDb에 연결 문자열 하도록 선택할 수 있습니다. 이 문서에 대 한 LocalDb로 변경할 수 있습니다.
3. Web.config를 열고 연결 문자열을 변경 합니다. (LocalDb) v 11.0에 SQLExpess 합니다. 제거 ' 사용자 인스턴스 = true' 연결 문자열에서 합니다.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image3.jpg)
4. 서버 탐색기를 열고 테이블 스키마와 데이터를 확인할 수 있는지 확인 합니다.
5. ASP.NET Id 시스템이 버전 4.5 이상이 프레임 워크와 작동합니다. 4.5 이상 응용 프로그램 대상 다시 지정 합니다.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image5.png)

    오류가 없는 있는지 확인 하기 위해 프로젝트를 빌드하십시오.

### <a name="installing-the-nuget-packages"></a>Nuget 패키지 설치

1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 &gt; **NuGet 패키지 관리**합니다. 검색 상자에 "Asp.net Id"를 입력 합니다. 결과 목록에서 패키지를 선택 하 고 설치를 클릭 합니다. "동의 안 함" 단추를 클릭 하 여 사용권 계약에 동의 합니다. 이 패키지에서는 종속성 패키지를 설치 하는 참고: EntityFramework 및 Microsoft ASP.NET Identity Core 합니다. 마찬가지로 (OAuth 로그인을 사용 하도록 설정 하지 않을 경우 마지막 4 OWIN 패키지 건너뛸) 다음 패키지를 설치 합니다.

    - Microsoft.AspNet.Identity.Owin
    - Microsoft.Owin.Host.SystemWeb
    - Microsoft.Owin.Security.Facebook
    - Microsoft.Owin.Security.Google
    - Microsoft.Owin.Security.MicrosoftAccount
    - Microsoft.Owin.Security.Twitter

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image6.png)

### <a name="migrate-database-to-the-new-identity-system"></a>새 Id 시스템으로 데이터베이스 마이그레이션

ASP.NET Id 시스템에 필요한 스키마에 기존 데이터베이스를 마이그레이션하려면 다음 단계가입니다. 달성 하기 위해 새 테이블을 만들고 새 테이블에 기존 사용자 정보를 마이그레이션하려면 명령 집합이 있는 스크립트는 SQL 실행이 합니다. 스크립트 파일을 찾을 수 [여기](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/SQLMembership-Identity-OWIN/Migrations.sql)합니다.

이 스크립트 파일은이 샘플 관련이 있습니다. 테이블에 대 한 스키마를 만든 경우 사용자 지정 된 SQL 멤버 자격을 사용 하 여 하거나 적절 하 게 변경 필요가 스크립트를 수정 합니다.

### <a name="how-to-generate-the-sql-script-for-schema-migration"></a>스키마 마이그레이션에 대 한 SQL 스크립트를 생성 하는 방법

기존 사용자의 데이터에서 작동 하도록 ASP.NET Identity 클래스에 대 한 ASP.NET Identity에 필요한 책갈피로 데이터베이스 스키마를 마이그레이션해야 할. 새 테이블을 추가 하 고 이러한 테이블에 기존 정보를 복사 하 여이 수행할 수 있습니다. 기본적으로 ASP.NET Identity EntityFramework를 사용 하 여 Id 모델 클래스는 데이터베이스 정보를 저장/검색에 다시 매핑할 수 있습니다. 이러한 모델 클래스 사용자 및 역할 개체를 정의 하는 핵심 Identity 인터페이스를 구현 합니다. 테이블 및 데이터베이스의 열에는 이러한 모델 클래스에 기반 합니다. Identity v2.1.0 및 해당 속성에서 EntityFramework 모델 클래스는 아래에 정의 된 대로

| **IdentityUser** | **Type** | **IdentityRole** | **IdentityUserRole** | **IdentityUserLogin** | **IdentityUserClaim** |
| --- | --- | --- | --- | --- | --- |
| ID | string | ID | RoleId | ProviderKey | ID |
| 사용자 이름 | string | name | UserId | UserId | ClaimType |
| PasswordHash | string |  |  | LoginProvider | ClaimValue |
| SecurityStamp | string |  |  |  | 사용자\_Id |
| 메일 | string |  |  |  |  |
| EmailConfirmed | bool |  |  |  |  |
| PhoneNumber | string |  |  |  |  |
| PhoneNumberConfirmed | bool |  |  |  |  |
| LockoutEnabled | bool |  |  |  |  |
| LockoutEndDate | DateTime |  |  |  |  |
| AccessFailedCount | int |  |  |  |  |

각이 모델에 대 한 속성에 해당 하는 열이 있는 테이블을 가져야 필요 합니다. 에 정의 된 클래스 및 테이블 간의 매핑을 `OnModelCreating` 의 메서드는 `IdentityDBContext`합니다. 이 구성의 fluent API 메서드 라고 하며 자세한 정보를 찾을 수 [여기](https://msdn.microsoft.com/data/jj591617.aspx)합니다. 클래스에 대 한 구성은 아래에서 설명한 대로

| **클래스** | **Table** | **기본 키** | **외래 키** |
| --- | --- | --- | --- |
| IdentityUser | AspnetUsers | ID |  |
| IdentityRole | AspnetRoles | ID |  |
| IdentityUserRole | AspnetUserRole | UserId + RoleId | User\_Id-&gt;AspnetUsers RoleId-&gt;AspnetRoles |
| IdentityUserLogin | AspnetUserLogins | ProviderKey + UserId + LoginProvider | UserId-&gt;AspnetUsers |
| IdentityUserClaim | AspnetUserClaims | ID | User\_Id-&gt;AspnetUsers |

이 정보에서는 새 테이블을 만드는 SQL 문을 만들 수 있습니다. 개별적으로 각 문을 작성 하거나 그런 다음 편집할 수는 EntityFramework PowerShell 명령을 사용 하 여 필요에 따라 전체 스크립트를 생성 했습니다. VS 열기에서이 작업을 수행 하는 **패키지 관리자 콘솔** 에서 **보기** 또는 **도구** 메뉴

- EntityFramework 마이그레이션을 설정 하려면 "Enable-migrations" 명령을 실행 합니다.
- C#에서 데이터베이스를 만들려고 초기 설치 코드를 만듭니다 "add-migration 초기" 명령을 실행 / VB.
- 마지막 단계를 실행 하는 "Update-database-스크립트" 모델 클래스를 기반으로 SQL 스크립트를 생성 하는 명령입니다.

여기서 म 합니다 잘 추가 변경 새 열을 추가 하 고 데이터 복사를 시작으로이 데이터베이스 생성 스크립트를 사용할 수 있습니다. 이의 이점은 생성 하는 것입니다는 `_MigrationHistory` EntityFramework 모델 클래스 Identity 릴리스 이후 버전에 대 한 변경 하는 경우 데이터베이스 스키마를 수정 하는 데 사용 되는 테이블입니다. 

SQL 멤버 자격 사용자 정보에 다른 Id 사용자 모델 클래스 즉 전자 메일에서에서 뿐만 아니라 속성, 암호 시도 횟수, 마지막 로그인 날짜, 마지막 잠금 날짜 등이 있습니다. 유용한 정보 이며 같은 Id 시스템에 전달 되 게 합니다. 사용자 모델에 추가 속성을 추가 하 고 데이터베이스의 테이블 열으로 다시 매핑하면 여이 작업을 수행할 수 있습니다. 이렇게 하려면 클래스를 추가 하 여 해당 서브 클래스는 `IdentityUser` 모델입니다. 이 사용자 지정 클래스에 속성을 추가 하 고 테이블을 만들 때 해당 열을 추가한 SQL 스크립트를 편집 했습니다. 이 클래스에 대 한 코드는 문서에서 더 자세히 설명 합니다. 만들기 위한 SQL 스크립트는 `AspnetUsers` 테이블 것 새 속성 추가

[!code-sql[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample1.sql)]

다음 Id에 대 한 SQL 멤버 자격 데이터베이스에서 새로 추가 된 테이블에 기존 정보를 복사 해야 합니다. 이를 다른 한 테이블에서 직접 데이터를 복사 하 여 SQL을 통해 수행할 수 있습니다. 사용 데이터 테이블의 행을 추가 하려면는 `INSERT INTO [Table]` 생성 합니다. 사용 하는 다른 테이블에서 복사 하는 `INSERT INTO` 와 함께 문을 `SELECT` 문. 쿼리 하는 데 필요한 모든 사용자 정보를 가져오려는 *aspnet\_사용자* 및 *aspnet\_구성원* 테이블 데이터를 복사 하는 *AspNetUsers*테이블입니다. 사용 하 여는 `INSERT INTO` 및 `SELECT` 와 함께 `JOIN` 및 `LEFT OUTER JOIN` 문. 쿼리 및 테이블 간에 데이터를 복사 하는 방법에 대 한 자세한 내용은를 참조 [이](https://technet.microsoft.com/library/ms190750%28v=sql.105%29.aspx) 링크 합니다. 또한 AspnetUserLogins 및 AspnetUserClaims 테이블 않으므로 빈로 시작 기본적으로이 매핑되는 SQL 멤버 자격 정보가 없습니다. 복사 하는 유일한 정보는 사용자와 역할입니다. 이전 단계에서 만든 프로젝트에 대 한 정보를 사용자 테이블에 복사 하기 위한 SQL 문을 것

[!code-sql[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample2.sql)]

위의 SQL 문의 각 사용자에 대 한 정보는 *aspnet\_사용자* 및 *aspnet\_구성원* 테이블의 열에 복사 되는  *AspnetUsers* 테이블입니다. 여기에서 완료 하는 유일한 수정할 때 암호 복사 합니다. SQL 멤버 자격에는 암호에 대 한 암호화 알고리즘 사용 'PasswordSalt' 및 'PasswordFormat' 이므로 복사 하는 너무 해시 된 암호와 함께 Id로 암호를 해독 하 사용 될 수 있도록 합니다. 이 사용자 지정 암호 hasher를 후크 하는 경우 문서에 내용을 설명 합니다. 

이 스크립트 파일은이 샘플 관련이 있습니다. 추가 테이블을 포함 하는 응용 프로그램의 경우 개발자가 사용자 모델 클래스에 추가 속성을 추가 하 고 AspnetUsers 테이블의 열에 매핑한 이와 비슷한 방식을 따르면 됩니다. 스크립트를 실행 하려면

1. 서버 탐색기를 엽니다. 'ApplicationServices' 연결 테이블을 표시 하려면 확장 합니다. 테이블 노드를 마우스 오른쪽 단추로 클릭 하 고 새 쿼리 옵션을 선택

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image7.png)
2. 쿼리 창에서 복사한 Migrations.sql 파일에서 전체 SQL 스크립트를 붙여 넣습니다. '실행' 화살표 단추를 클릭 하 여 스크립트 파일을 실행 합니다.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image4.jpg)

    서버 탐색기 창을 새로 고칩니다. 데이터베이스에 5 개의 새 테이블이 만들어집니다.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image8.png)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image9.png)

    다음 SQL 멤버 자격 테이블의 정보는 새 Id 시스템에 매핑되는 방식을입니다.

    aspnet\_Roles --&gt; AspNetRoles

    asp\_netUsers 및 asp\_netMembership-&gt; AspNetUsers

    aspnet\_UserInRoles --&gt; AspNetUserRoles

    위의 섹션에서 설명 했 듯이 AspNetUserClaims 및 AspNetUserLogins 테이블은 비어 있습니다. AspNetUser 테이블의 '판별자' 필드에는 다음 단계로 정의 된 모델 클래스 이름과 일치 해야 합니다. PasswordHash 열이 형식에도 ' 암호화 암호 | 암호 솔트 | 암호 형식 '. 그러면 기존 암호를 다시 사용할 수 있도록 특수 SQL 멤버 자격 암호화 논리를 사용할 수 있습니다. 문서의 뒷부분에 설명 되어 있습니다.

### <a name="creating-models-and-membership-pages"></a>모델 및 멤버 자격 페이지 만들기

앞서 언급 했 듯이 Id 기능은 기본적으로 계정 정보를 저장 하기 위해 데이터베이스에 설명 하는 Entity Framework를 사용 합니다. 테이블의 기존 데이터를 사용 하려면 테이블에 다시 매핑할 및 Id 시스템에 연결 하는 모델 클래스를 만들어야 할 합니다. Identity 계약의 일부로 모델 클래스 Identity.Core dll에 정의 된 인터페이스를 구현 해야 하거나 또는 Microsoft.AspNet.Identity.EntityFramework에서 사용할 수 있는 이러한 인터페이스의 기존 구현을 확장할 수 있습니다.

이 예제에서는 AspNetRoles, AspNetUserClaims, AspNetLogins 및 AspNetUserRole 테이블 Id 시스템의 기존 구현을 유사한 열이 포함 됩니다. 따라서 이러한 테이블에 매핑할 기존 클래스 다시 사용할 수 있습니다. AspNetUser 테이블에는 SQL 멤버 자격 테이블에서 추가 정보를 저장 하는 데 사용 되는 몇 개의 추가 열에 있습니다. 'IdentityUser'의 기존 구현을 확장 하 고 추가 속성을 추가 하는 모델 클래스를 만들어이 매핑할 수 있습니다.

1. 프로젝트에 만듭니다 모델 폴더 고 사용자 클래스를 추가 합니다. 클래스의 이름 'AspnetUsers' 테이블의 '판별자' 열에 추가 된 데이터를 일치 해야 합니다.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image10.png)

    사용자 클래스에 IdentityUser 클래스를 확장 해야는 *Microsoft.AspNet.Identity.EntityFramework* dll입니다. AspNetUser 열에 다시 매핑되는 클래스의 속성을 선언 합니다. 속성 ID, 사용자 이름, PasswordHash 및 SecurityStamp는 IdentityUser에 정의 되어 있고 따라서 생략 됩니다. 다음은 모든 속성이 있는 사용자 클래스에 대 한 코드

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample3.cs)]
2. Entity Framework DbContext 클래스 모델 테이블에에서 데이터를 유지 하 고 모델을 채우는 테이블에서 데이터를 검색 하기 위해 필요 합니다. *Microsoft.AspNet.Identity.EntityFramework* dll 검색 한 정보를 저장 하는 Identity 테이블와 상호 작용 하는 IdentityDbContext 클래스를 정의 합니다. 구체적인 IdentityDbContext&lt;s e r&gt; IdentityUser 클래스를 확장 하는 모든 클래스 될 수 있는 's e r' 클래스를 사용 합니다.

    ApplicationDBContext IdentityDbContext 1 단계에서 만든 'User' 클래스에서 전달 '모델' 폴더를 확장 하는 새 클래스 만들기

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample4.cs)]
3. 사용자 관리 하는 새 Id 시스템에 의해 이루어진다는 usermanager가 사용 하 여&lt;s e r&gt; 에 정의 된 클래스는 *Microsoft.AspNet.Identity.EntityFramework* dll입니다. 1 단계에서 만든 'User' 클래스에 전달 합니다. UserManager를 확장 하는 사용자 지정 클래스를 만드는 해야 합니다.

    모델 폴더 UserManager UserManager를 확장 하는 새 클래스를 만듭니다&lt;사용자&gt;

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample5.cs)]
4. 응용 프로그램의 사용자의 암호는 암호화 및 데이터베이스에 저장 됩니다. SQL 멤버 자격에 사용 되는 암호화 알고리즘은 새 Id 시스템에 있는 것과에서 다릅니다. 이전 암호 다시 사용 하려면 선택적으로 오래 된 사용자가 SQL 멤버 자격 알고리즘을 사용 하 여 새 사용자에 대 한 id에서는 암호화 알고리즘을 사용 하는 동안 로그인 암호를 해독 해야 합니다.

    Usermanager가 클래스에 'PasswordHasher' 'IPasswordHasher' 인터페이스를 구현 하는 클래스의 인스턴스를 저장 하는 속성이 있습니다. 이 사용자 인증 트랜잭션 중 암호 암호화/해독에 사용 됩니다. 3 단계에서 정의 된 UserManager 클래스에서 만들 새 클래스 SQLPasswordHasher 및 복사는 아래 코드입니다.

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample6.cs)]

    System.Text 및 System.Security.Cryptography 네임 스페이스를 가져와서 컴파일 오류를 해결 합니다.

    EncodePassword 메서드는 기본 SQL 멤버 자격 암호화 구현에 따라 암호를 암호화합니다. System.Web dll에서 정보를 가져옵니다. 경우 이전 앱 여기에 사용자 지정 구현을 다음 반영 되어야 합니다. 다른 두 메서드를 정의 해야 *HashPassword* 및 *VerifyHashedPassword* 사용 하는 *EncodePassword* 메서드를 지정 된 암호를 해시 또는 일반 텍스트를 확인 합니다. 데이터베이스에 하나의 기존 암호입니다.

    PasswordHash, PasswordSalt와 PasswordFormat을 등록 하거나 자신의 암호를 변경할 때 사용자가 입력 한 암호를 해시를 사용 하는 SQL 멤버 자격 시스템입니다. 마이그레이션 중 3 개의 필드 구분 하 여 AspNetUser 표에 PasswordHash 열에 저장 된는 ' |' 문자입니다. 사용자가 로그인 하는 경우 암호에 이러한 필드에서는을 사용 하 여 SQL 멤버 자격 암호화의 암호입니다. 그렇지 않으면 Id 시스템 기본 암호화 암호를 확인 하려면 사용 합니다. 이러한 방식으로 오래 된 사용자가 필요는 없습니다 앱 마이그레이션된 후 암호를 변경 합니다.
5. Usermanager가 클래스에 대 한 생성자를 선언 하 고는 SQLPasswordHasher 처럼 속성은 생성자에 전달 합니다.

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample7.cs)]

### <a name="create-new-account-management-pages"></a>새 계정 관리 페이지 만들기

다음 단계는 마이그레이션 계정 관리 페이지를 등록 및 로그인 사용자를 추가 하는 것입니다. SQL 멤버 자격에서 이전 계정을 페이지는 새 Id 시스템을 사용 하지 않는 컨트롤을 사용 합니다. 새 사용자를 추가 하려면 관리 페이지는 다음이 링크에서 자습서를 따라 [https://www.asp.net/identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project](../getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project.md) 단계의 시작 ' Web Forms 응용 프로그램에 사용자를 등록 하기 위한 추가 ' 이미 프로젝트를 만든 고 NuGet 패키지를 추가 했습니다.

여기에 있는 프로젝트와 함께 작동 하도록이 샘플에 대 한 일부 변경 해야 합니다.

- Register.aspx.cs 및 Login.aspx.cs 코드 숨김 클래스 사용의 `UserManager` 사용자를 만들려면 Identity 패키지에서 합니다. 이 예에서는 앞에서 언급 한 단계에 따라 모델 폴더에 추가 합니다. UserManager를 사용 합니다.
- 클래스 뒤 Register.aspx.cs 및 Login.aspx.cs 코드에서 IdentityUser 대신 만들어진 사용자 클래스를 사용 합니다. 이 Id 시스템에 사용자 지정 클래스에 연결 합니다.
- 데이터베이스를 만드는 일부를 건너뛸 수 있습니다.
- 개발자는 현재 응용 프로그램 ID와 일치 하는 새 사용자에 대 한 응용 프로그램 Id를 설정 해야 합니다. 사용자 개체 Register.aspx.cs 클래스에서 만들어지기 전에이 응용 프로그램에 대 한 응용 프로그램 Id를 쿼리 하 고 사용자를 만들기 전에 설정 하 여이 작업을 수행할 수 있습니다. 

    예제:

    Aspnet 쿼리할 Register.aspx.cs 페이지에서 메서드를 정의\_응용 프로그램 테이블 및 응용 프로그램 이름에 따라 응용 프로그램 Id 가져오기

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample8.cs)]

    이제 get이 개체에 설정 사용자

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample9.cs)]

기존 사용자 이름 및 암호를 사용 하 여 기존 사용자를 로그인 합니다. 등록 페이지를 사용 하 여 새 사용자를 만듭니다. 또한 예상 대로 사용자 역할에 있는지 확인 합니다.

Id 시스템에 이식를 통해 사용자는 Open Authentication (OAuth) 응용 프로그램에 추가 합니다. 이 샘플을 참조 하십시오 [여기](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/SQLMembership-Identity-OWIN/) 가 OAuth를 사용 하도록 설정 합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 SQL 멤버 자격의 사용자가 ASP.NET Identity에 이식 하는 방법 했죠 하지만 프로필 데이터 포트 하지 않은 것입니다. 다음 자습서에서는 새 Id 시스템에 SQL 멤버 자격에서 프로필 데이터를 이식를 살펴보겠습니다.

이 문서의 맨 아래에 피드백을 둘 수 있습니다.

*문서를 검토 하기 위한 Tom Dykstra 및 Rick Anderson 가져주셔서 감사 합니다.*
