---
uid: identity/overview/extensibility/overview-of-custom-storage-providers-for-aspnet-identity
title: "ASP.NET Id에 대 한 사용자 지정 저장소 공급자 개요 | Microsoft Docs"
author: tfitzmac
description: "ASP.NET Id는 확장 가능한 시스템으로의 응용 프로그램 작업이 다시 실행 하지 않고 응용 프로그램에 연결 하 고 저장소 공급자를 만들 수 있습니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/13/2014
ms.topic: article
ms.assetid: 681a9204-462e-4260-9a0b-19f0644d6ad7
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /identity/overview/extensibility/overview-of-custom-storage-providers-for-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: f43f0a2dd80e26ecff15e5742e18264ddb5b26aa
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="overview-of-custom-storage-providers-for-aspnet-identity"></a>ASP.NET Id에 대 한 사용자 지정 저장소 공급자 개요
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> ASP.NET Id는 확장 가능한 시스템 응용 프로그램 작업이 다시 실행 하지 않고 응용 프로그램에 연결 하 고 저장소 공급자를 만들 수 있습니다. 이 항목에서는 ASP.NET Identity에 대 한 사용자 지정 된 저장소 공급자를 만드는 방법을 설명 합니다. 저장소 공급자를 만들기 위한 중요 한 개념을 다루고 있지만 사용자 지정 저장소 공급자를 구현 하는의 단계별 연습은 아닙니다.
> 
> 사용자 지정 저장소 공급자를 구현 하는의 예제를 보려면 [사용자 지정 MySQL ASP.NET Identity 저장소 공급자 구현](implementing-a-custom-mysql-aspnet-identity-storage-provider.md)합니다.
> 
> 이 항목은 ASP.NET Identity 2.0에 대 한 업데이트 되었습니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - Visual Studio 2013 업데이트 2
> - ASP.NET Id 2


## <a name="introduction"></a>소개

기본적으로 ASP.NET Identity 시스템 SQL Server 데이터베이스에 사용자 정보를 저장 하 고 데이터베이스를 만들 Entity Framework Code First를 사용 합니다. 대부분의 응용 프로그램에 대 한이 방법은 잘 작동합니다. 그러나 다른 종류의 Azure 테이블 저장소와 같은 지 속성 메커니즘을 사용 하는 것이 좋습니다 또는 기본 구현은 매우 다른 구조로 포함 된 데이터베이스 테이블에 이미 있을 수도 있습니다. 두 경우 모두 저장 메커니즘에 대 한 사용자 지정된 공급자를 작성할 수 있으며 응용 프로그램에 해당 공급자를 연결 합니다. 키를 누릅니다.

ASP.NET Id는 Visual Studio 2013 템플릿 중 대부분에 기본적으로 포함 됩니다. 통해 ASP.NET Identity에 업데이트를 가져올 수 [Microsoft AspNet Identity EntityFramework NuGet 패키지](http://www.nuget.org/packages/Microsoft.AspNet.Identity.EntityFramework/)합니다.

이 항목은 다음 섹션으로 구성되어 있습니다.

- [아키텍처를 이해](#architecture)
- [저장 된 데이터 이해](#data)
- [데이터 액세스 계층 만들기](#dal)
- [사용자 클래스를 사용자 지정](#user)
- [사용자 저장소에 사용자 지정](#userstore)
- [Role 클래스를 사용자 지정](#role)
- [역할 저장소의 사용자 지정](#rolestore)
- [새 저장소 공급자를 사용 하도록 응용 프로그램을 다시 구성](#reconfigure)
- [다른 사용자 지정 저장소 공급자 구현](#other)

<a id="architecture"></a>
## <a name="understand-the-architecture"></a>아키텍처를 이해

ASP.NET Identity 관리자와 저장소를 호출 하는 클래스로 구성 됩니다. 관리자는 상위 클래스 응용 프로그램 개발자를 사용 하 여 ASP.NET Identity 시스템에는 사용자 만들기 같은 작업을 수행 합니다. 저장소는 사용자 및 역할을 하는 등의 엔터티는 유지 하는 방법을 지정 하는 하위 클래스입니다. 저장소는 지 속성 메커니즘이와 밀접 하 게 연결 되어 하지만 관리자에서에서 분리 됩니다 저장소 즉, 전체 응용 프로그램을 방해 하지 않고 지 속성 메커니즘을 바꿀 수 있습니다.

저장소 데이터 액세스 계층 상호 작용 및 다음 다이어그램은 웹 응용 프로그램 관리자, 상호 작용 하는 방법을 보여 줍니다.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image1.png)

ASP.NET Id에 대 한 사용자 지정 된 저장소 공급자를 만들려면이 데이터 액세스 계층으로 데이터 원본, 데이터 액세스 계층 상호 작용 하는 저장소 클래스를 만들 수 있어야 합니다. 사용자에 했지만 이제는 해당 데이터를 다른 저장소 시스템에 저장할 데이터 작업을 수행 하려면 동일한 관리자 Api를 사용 하 여 계속할 수 있습니다.

사용자 클래스의 형식을 제공 UserManager 또는 RoleManager의 새 인스턴스를 만들 때 관리자 클래스를 사용자 지정 하 고 저장소 클래스의 인스턴스를 인수로 전달할 필요가 없습니다. 이 방법을 사용 하면 사용자 지정 된 클래스를 기존 구조에 연결할 수 있습니다. UserManager 및 RoleManager 섹션에서 사용자 지정 된 저장소 클래스를 인스턴스화하는 방법을 나타납니다 [새 저장소 공급자를 사용 하도록 응용 프로그램을 다시 구성](#reconfigure)합니다.

<a id="data"></a>
## <a name="understand-the-data-that-is-stored"></a>저장 된 데이터 이해

사용자 지정 저장소 공급자를 구현 하려면 ASP.NET Identity에서 사용 된 데이터 유형의 이해 하 고 있는 응용 프로그램과 관련 된 기능을 결정 합니다.

| 데이터 | 설명 |
| --- | --- |
| 사용자 | 웹 사이트의 등록 된 사용자입니다. 사용자 Id 및 사용자 이름을 포함합니다. 사용자가 사이트에만 적용 되는 자격 증명으로 로그인 하는 경우에 해시 된 암호를 포함 될 수 있습니다 (아님 Facebook 등의 외부 사이트에서 자격 증명을 사용 하 여), 및 보안 스탬프 아무 것도 사용자 자격 증명에 변경 되었는지 여부를 나타냅니다. 전자 메일 주소를 포함할 수도, 전화 번호를 실패 한 로그인을 현재 수가 2 단계 인증이 사용 되는지 여부를 수도 있습니다 이며 계정이 잠겨 있는지 여부. |
| 사용자 클레임 | 사용자의 id를 나타내는 사용자에 대 한 문 (또는 클레임)의 집합입니다. 더 나은 식의 역할을 통해 액세스가 가능 보다는 사용자의 id 사용 하도록 설정할 수 있습니다. |
| 사용자 로그인 | 외부 인증 공급자 (예: Facebook)에 대 한 정보는 사용자를 로그인 할 때 사용 하도록 합니다. |
| 역할 | 사이트에 대 한 권한 부여 그룹입니다. 역할 Id 및 역할 이름 (예: "Admin" 또는 "Employee")를 포함합니다. |

<a id="dal"></a>
## <a name="create-the-data-access-layer"></a>데이터 액세스 계층 만들기

이 항목에서는 사용 하고자 하는 지 속성 메커니즘 및 해당 메커니즘에 대 한 엔터티를 만드는 방법에 익숙한 가정 합니다. 이 항목을 저장소 또는 데이터 액세스 클래스; 만드는 방법에 대 한 세부 정보를 제공 하지 않습니다. 대신, ASP.NET Identity를 작업할 때 확인 해야 할 몇 가지 제안 디자인 결정 사항에 대 한 제공 합니다.

저장소 공급자는 사용자 지정에 대 한 저장소를 디자인할 때 원하는 대로 많은 해야 합니다. 응용 프로그램에서 사용 하려는 기능에 대 한 리포지토리를 만들 하기만 하면 됩니다. 예를 들어 응용 프로그램에서 역할을 사용 하지 않는 경우 역할 또는 사용자 역할에 대 한 저장소를 만들 필요가 없습니다 합니다. 기술 및 기존 인프라에는 ASP.NET Identity의 기본 구현에서 매우 다른 구조가 필요할 수 있습니다. 데이터 액세스 계층에서 사용자 저장소의 구조를 사용 하는 논리를 제공할 수 있습니다.

ASP.NET Identity 2.0에 대 한 데이터 저장소는 MySQL 구현을 참조 [MySQLIdentity.sql](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql)합니다.

데이터 액세스 계층에서 데이터 원본에 ASP.NET Identity에서 데이터를 저장 하는 논리를 제공할 수 있습니다. 사용자 지정 된 저장소 공급자에 대 한 데이터 액세스 계층에는 사용자 및 역할 정보를 저장 하는 다음 클래스가 포함 될 수 있습니다.

| 클래스 | 설명 | 예 |
| --- | --- | --- |
| 컨텍스트 | 지 속성 메커니즘에 연결 하 고 쿼리를 실행 하는 정보를 캡슐화 합니다. 이 클래스는 핵심 데이터 액세스 계층입니다. 다른 데이터 클래스는 해당 작업을 수행 하려면이 클래스의 인스턴스를 해야 합니다. 또한이 클래스의 인스턴스와 저장소 클래스를 초기화 합니다. | [MySQLDatabase](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) |
| 사용자 저장소 | 저장 하 고 사용자 정보 (예: 사용자 이름 및 암호 해시)를 검색 합니다. | [UserTable (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserTable.cs) |
| 역할 저장소 | 저장 하 고 (예: 역할 이름) 역할 정보를 검색 합니다. | [RoleTable (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/RoleTable.cs) |
| UserClaims 저장소 | 저장 하 고 사용자 클레임 정보 (예: 클레임 유형 및 값)를 검색 합니다. | [UserClaimsTable (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) |
| UserLogins 저장소 | 저장 하 고 (예: 외부 인증 공급자 사용 하 는) 사용자 로그인 정보를 검색 합니다. | [UserLoginsTable (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) |
| UserRole 저장소 | 저장 하 고 있는 역할에 할당 된 사용자를 검색 합니다. | [UserRoleTable (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) |

다시, 응용 프로그램에서 사용 하려는 클래스를 구현 하기만 하면 됩니다.

데이터 액세스 클래스 특정 지 속성 메커니즘에 대 한 데이터 작업을 수행 하는 코드를 제공할 수 있습니다. 예를 들어 UserTable 클래스 MySQL 구현 내에서 사용자가 데이터베이스 테이블에 새 레코드를 삽입 하는 메서드를 포함 합니다. 라는 변수 `_database` MySQLDatabase 클래스의 인스턴스입니다.

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample1.cs)]

데이터 액세스 클래스를 만든 후 데이터 액세스 계층의 특정 메서드를 호출 하는 저장소 클래스를 만들어야 합니다.

<a id="user"></a>
## <a name="customize-the-user-class"></a>사용자 클래스를 사용자 지정

에 해당 하는 사용자 클래스를 만들어야 사용자 고유의 저장소 공급자를 구현할 때는 [IdentityUser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityuser(v=vs.108).aspx) 클래스에 [Microsoft.ASP.NET.Identity.EntityFramework](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx) 네임 스페이스:

다음 다이어그램에서는 만들어야 하는 IdentityUser 클래스 및이 클래스에서 구현 하는 인터페이스를 보여 줍니다.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image2.png)

[IUser&lt;TKey&gt; ](https://msdn.microsoft.com/library/dn613291(v=vs.108).aspx) 인터페이스 usermanager가 요청 된 작업을 수행 하는 때를 호출 하려고 하는 속성을 정의 합니다. 인터페이스에는 두 개의 속성-Id와 사용자 이름이 포함 되어 있습니다. [IUser&lt;TKey&gt; ](https://msdn.microsoft.com/library/dn613291(v=vs.108).aspx) 인터페이스를 사용 하면 제네릭을 통해 사용자에 대 한 키의 형식을 지정할 수 **TKey** 매개 변수입니다. Id 속성의 유형을 TKey 매개 변수의 값을 찾습니다.

Id 프레임 워크 또한 제공 된 [IUser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.iuser(v=vs.108).aspx) (제네릭 매개 변수) 없이 인터페이스 키에는 문자열 값을 사용 하려는 경우.

IdentityUser 클래스 IUser 구현 및 추가 속성 또는 웹 사이트에서 사용자에 대 한 생성자를 포함 합니다. 다음 예제에서는 정수를 사용 하 여 키에 대 한 IdentityUser 클래스를 보여 줍니다. Id 필드로 설정 되어 **int** 제네릭 매개 변수의 값과 일치 하도록 합니다. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample2.cs)]

 완전 한 구현에 대 한 참조 [IdentityUser (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/IdentityUser.cs)합니다. 

<a id="userstore"></a>
## <a name="customize-the-user-store"></a>사용자 저장소에 사용자 지정

또한 사용자에 대 한 모든 데이터 작업에 대 한 메서드를 제공 하는 UserStore 클래스를 만듭니다. 이 클래스는 해당 하는 [UserStore&lt;s e r&gt; ](https://msdn.microsoft.com/library/dn315446(v=vs.108).aspx) 클래스에 [Microsoft.ASP.NET.Identity.EntityFramework](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx) 네임 스페이스입니다. UserStore 클래스에서 구현 하는 [IUserStore&lt;TKey, s e r&gt; ](https://msdn.microsoft.com/library/dn613276(v=vs.108).aspx) 및 선택적 인터페이스입니다. 응용 프로그램에서 제공 하려는 기능에 따라 구현 해야 하는 선택적 인터페이스를 선택 합니다.

다음 이미지는 만들어야 UserStore 클래스 및 관련 인터페이스를 표시 합니다.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image3.png)

기본 프로젝트 템플릿을 Visual Studio에서 사용자 저장소에 구현 된 여러 가지 선택적 인터페이스 가정 하는 코드를 포함 합니다. 기본 템플릿을 사용자 지정 된 사용자 저장소를 사용 하는 경우 사용자 저장소에 선택적 인터페이스를 구현 하거나 더 이상 구현 하지 인터페이스의 메서드를 호출 하는 템플릿 코드를 변경 합니다.

 다음 예제에서는 간단한 사용자 저장소 클래스를 보여 줍니다. **s e r** 제네릭 매개 변수는 일반적으로 사용자가 정의한 IdentityUser 클래스는 사용자 클래스의 형식을 사용 합니다. **TKey** 제네릭 매개 변수는 사용자 키 유형을 사용 합니다. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample3.cs)]

 이 예제에서는 매개 변수를 사용 하는 생성자를 이름이 *데이터베이스* 형식이 ExampleDatabase가만의 사용자 데이터 액세스 클래스에 전달 하는 방법 보여 줍니다. 예를 들어 MySQL 구현에서는이 생성자는 MySQLDatabase 형식의 매개 변수를 사용 합니다. 

UserStore 클래스 내에서 작업을 수행 하기 위해 만든 데이터 액세스 클래스를 사용 합니다. 예를 들어 MySQL 구현 UserStore 클래스에 UserTable의 인스턴스를 사용 하 여 새 레코드를 삽입 하는 CreateAsync 메서드를 사용 합니다. **삽입** 에서 메서드는 **userTable** 개체는 이전 섹션에 표시 된 것과 동일한 메서드. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample4.cs)]

### <a name="interfaces-to-implement-when-customizing-user-store"></a>사용자 저장소에 사용자 지정 하는 경우 구현 하는 인터페이스

다음 이미지는 각 인터페이스에 정의 된 기능에 대 한 자세한 정보를 나타냅니다. 모든 선택적 인터페이스 IUserStore에서 상속합니다.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image4.png)

- **IUserStore**  
 [IUserStore&lt;s e r, TKey&gt; ](https://msdn.microsoft.com/library/dn613278(v=vs.108).aspx) 인터페이스는 인터페이스에서 사용자 저장소를 구현 해야 합니다. 만들기, 업데이트, 삭제 및 사용자를 검색 하기 위한 메서드를 정의 합니다.
- **IUserClaimStore**  
 [IUserClaimStore&lt;s e r, TKey&gt; ](https://msdn.microsoft.com/library/dn613265(v=vs.108).aspx) 인터페이스 메서드를 정의 합니다. 사용자 클레임을 사용 하도록 설정 하려면 사용자 저장소에서 구현 해야 합니다. 메서드 또는 추가, 제거 및 사용자 클레임을 검색을 포함 합니다.
- **IUserLoginStore**  
 [IUserLoginStore&lt;s e r, TKey&gt; ](https://msdn.microsoft.com/library/dn613272(v=vs.108).aspx) 메서드 정의 외부 인증 공급자를 사용 하도록 설정 하려면 사용자 저장소에서 구현 해야 합니다. 추가, 제거 및 사용자 로그인 및 로그인 정보에 따라 사용자를 검색 하기 위한 메서드를 검색 하기 위한 메서드를 포함 합니다.
- **IUserRoleStore**  
 [IUserRoleStore&lt;TKey, s e r&gt; ](https://msdn.microsoft.com/library/dn613276(v=vs.108).aspx) 메서드를 정의 하는 인터페이스 역할에 사용자를 매핑할 사용자 저장소에서 구현 해야 합니다. 추가, 제거 및 사용자의 역할 및 사용자를 역할에 할당 된 경우를 확인 하는 메서드를 검색 하는 메서드를 포함 합니다.
- **IUserPasswordStore**  
 [s w&lt;s e r, TKey&gt; ](https://msdn.microsoft.com/library/dn613273(v=vs.108).aspx) 인터페이스를 유지 하 여 사용자 저장소에서 구현 해야 하는 메서드를 정의 합니다. 해시 된 암호입니다. 가져오기 및 해시 된 암호와 사용자가 암호를 설정 하는지 여부를 나타내는 방법을 설정 하는 메서드를 포함 합니다.
- **IUserSecurityStampStore**  
 [IUserSecurityStampStore&lt;s e r, TKey&gt; ](https://msdn.microsoft.com/library/dn613277(v=vs.108).aspx) 사용자의 계정 정보가 변경 되었는지 여부를 나타내는에 보안 스탬프를 사용 하 여 사용자 저장소에서 구현 해야 하는 메서드를 정의 하는 인터페이스 . 사용자의 암호 변경 또는 추가 하거나 로그인을 제거 하는 경우이 스탬프 업데이트 됩니다. 가져오기 및 설정의 보안 스탬프에 대 한 메서드를 포함 합니다.
- **IUserTwoFactorStore**  
 [t w&lt;s e r, TKey&gt; ](https://msdn.microsoft.com/library/dn613279(v=vs.108).aspx) 인터페이스 구현에 구현 2 단계 인증을 해야 하는 메서드를 정의 합니다. 가져오기 및 사용자에 대해 2 단계 인증이 사용 되는지 여부를 설정 하는 메서드를 포함 합니다.
- **IUserPhoneNumberStore**  
 [p h&lt;s e r, TKey&gt; ](https://msdn.microsoft.com/library/dn613275(v=vs.108).aspx) 인터페이스 사용자 전화 번호를 저장 하기 위해 구현 해야 하는 메서드를 정의 합니다. 가져오기 및 전화 번호와 전화 번호가 확인 되었는지 여부를 설정 하는 메서드를 포함 합니다.
- **IUserEmailStore**  
 [o r e&lt;s e r, TKey&gt; ](https://msdn.microsoft.com/library/dn613143(v=vs.108).aspx) 인터페이스 사용자 전자 메일 주소를 저장 하기 위해 구현 해야 하는 메서드를 정의 합니다. 가져오기 및 전자 메일 주소 및 전자 메일이 확인 여부를 설정 하는 메서드를 포함 합니다.
- **IUserLockoutStore**  
 [o r e&lt;s e r, TKey&gt; ](https://msdn.microsoft.com/library/dn613271(v=vs.108).aspx) 인터페이스 계정 잠금에 대 한 정보를 저장 하기 위해 구현 해야 하는 메서드를 정의 합니다. 현재 실패 한 액세스 시도 수를 가져오는, 가져오기 설정 여부는 계정을 잠글 수 있는, 가져오기 및 시도 실패 수가 증가 하는 잠금 종료 날짜를 설정 하 고 실패 한 시도 횟수를 다시 설정에 대 한 메서드를 포함 합니다.
- **IQueryableUserStore**  
 [i q&lt;s e r, TKey&gt; ](https://msdn.microsoft.com/library/dn613267(v=vs.108).aspx) 인터페이스 쿼리 가능한 사용자 저장소를 제공 하도록 구현 해야 하는 멤버를 정의 합니다. 쿼리 가능한 사용자가 포함 하는 속성을 포함 합니다.

 사용자 응용 프로그램에서 필요한 인터페이스를 구현 와 같은, IUserClaimStore, IUserLoginStore, IUserRoleStore, s w, 및 IUserSecurityStampStore 아래와 같이 인터페이스입니다. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample5.cs)]

(모든 인터페이스 포함)는 전체 구현을 참조 [UserStore (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserStore.cs)합니다.

### <a name="identityuserclaim-identityuserlogin-and-identityuserrole"></a>IdentityUserClaim, IdentityUserLogin, 및 IdentityUserRole

Microsoft.AspNet.Identity.EntityFramework 네임 스페이스에 구현 된 [IdentityUserClaim](https://msdn.microsoft.com/library/dn613250(v=vs.108).aspx), [IdentityUserLogin](https://msdn.microsoft.com/library/dn613251(v=vs.108).aspx), 및 [IdentityUserRole](https://msdn.microsoft.com/library/dn613252(v=vs.108).aspx) 클래스입니다. 이러한 기능을 사용 하는 경우에 이러한 클래스의 사용자가 자체 버전을 만들고 응용 프로그램에 대 한 속성을 정의 하는 것이 좋습니다. 그러나 때로는 것이 효율적 기본 작업 (예: 추가 또는 제거 하는 사용자의 클레임)를 수행할 때 이러한 엔터티를 메모리에 로드 하지 않도록 합니다. 대신, 백 엔드 저장소 클래스는 데이터 원본에 직접 이러한 작업을 실행할 수 있습니다. 예를 들어 UserStore.GetClaimsAsync() 메서드는 userClaimTable.FindByUserId(user.를 호출할 수 있습니다. 직접 테이블 및 클레임의 목록을 반환 하는에서 쿼리를 실행 하려면 id) 메서드.

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample6.cs)]

<a id="role"></a>
## <a name="customize-the-role-class"></a>Role 클래스를 사용자 지정

에 해당 하는 역할 클래스 만들어야 사용자 고유의 저장소 공급자를 구현할 때는 [IdentityRole](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityrole(v=vs.108).aspx) 클래스에 [Microsoft.ASP.NET.Identity.EntityFramework](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx) 네임 스페이스:

다음 다이어그램에서는 만들어야 하는 IdentityRole 클래스 및이 클래스에서 구현 하는 인터페이스를 보여 줍니다.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image5.png)

[IRole&lt;TKey&gt; ](https://msdn.microsoft.com/library/dn613268(v=vs.108).aspx) 인터페이스는 RoleManager 요청 된 작업을 수행 하는 때를 호출 하려고 하는 속성을 정의 합니다. 인터페이스에는 두 개의 속성-Id와 이름을 포함합니다. [IRole&lt;TKey&gt; ](https://msdn.microsoft.com/library/dn613268(v=vs.108).aspx) 인터페이스를 사용 하면 제네릭을 통해 역할에 대 한 키의 형식을 지정할 수 **TKey** 매개 변수입니다. Id 속성의 유형을 TKey 매개 변수의 값을 찾습니다.

Id 프레임 워크 또한 제공 된 [IRole](https://msdn.microsoft.com/library/microsoft.aspnet.identity.irole(v=vs.108).aspx) (제네릭 매개 변수) 없이 인터페이스 키에는 문자열 값을 사용 하려는 경우.

다음 예제에서는 정수를 사용 하 여 키에 대 한 IdentityRole 클래스를 보여 줍니다. Id 필드는 제네릭 매개 변수의 값과 일치 하도록 int로 설정 됩니다. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample7.cs)]

 완전 한 구현에 대 한 참조 [IdentityRole (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/IdentityRole.cs)합니다. 

<a id="rolestore"></a>
## <a name="customize-the-role-store"></a>역할 저장소의 사용자 지정

역할에 대 한 모든 데이터 작업에 대 한 메서드를 제공 하는 RoleStore 클래스를 만들 수도 있습니다. 이 클래스는 해당 하는 [RoleStore&lt;TRole&gt; ](https://msdn.microsoft.com/library/dn468181(v=vs.108).aspx) Microsoft.ASP.NET.Identity.EntityFramework 네임 스페이스의 클래스입니다. RoleStore 클래스에서 구현 하는 [IRoleStore&lt;TRole, TKey&gt; ](https://msdn.microsoft.com/library/dn613266(v=vs.108).aspx) 및 필요에 따라는 [r e&lt;TRole, TKey&gt; ](https://msdn.microsoft.com/library/dn613262(v=vs.108).aspx) 인터페이스입니다.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image6.png)

다음 예제에서는 역할 저장소 클래스를 보여 줍니다. TRole 제네릭 매개 변수는 일반적으로 사용자가 정의한 IdentityRole 클래스는 역할 클래스의 형식을 사용 합니다. TKey 제네릭 매개 변수 역할 키 유형을 사용 합니다. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample8.cs)]

- **IRoleStore&lt;TRole&gt;**  
 [IRoleStore](https://msdn.microsoft.com/library/dn468195.aspx) 인터페이스 역할 저장소 클래스에서 구현 하는 메서드를 정의 합니다. 만들기, 업데이트, 삭제 및 역할을 검색 하는 메서드를 포함 합니다.
- **RoleStore&lt;TRole&gt;**  
 RoleStore를 사용자 지정 하려면 IRoleStore 인터페이스를 구현 하는 클래스를 만듭니다. 경우에이 클래스를 구현 하기만 하면 시스템에서 역할을 사용 하려면. 명명 된 매개 변수를 사용 하는 생성자를 *데이터베이스* 형식이 ExampleDatabase가만의 사용자 데이터 액세스 클래스에 전달 하는 방법 보여 줍니다. 예를 들어 MySQL 구현에서는이 생성자는 MySQLDatabase 형식의 매개 변수를 사용 합니다.  
  
 완전 한 구현에 대 한 참조 [RoleStore (MySQL)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/RoleStore.cs) 합니다.

<a id="reconfigure"></a>
## <a name="reconfigure-application-to-use-new-storage-provider"></a>새 저장소 공급자를 사용 하도록 응용 프로그램을 다시 구성

새 저장소 공급자에 구현 했습니다. 이제이 저장소 공급자를 사용 하도록 응용 프로그램을 구성 해야 합니다. 기본 저장소 공급자가 프로젝트에 포함 하는 경우 기본 공급자를 제거 하 고 공급 업체 대체할 해야 합니다.

### <a name="replace-default-storage-provider-in-mvc-project"></a>MVC 프로젝트의 기본 저장소 공급자를 대체 합니다.

1. 에 **NuGet 패키지 관리** 창 제거는 **Microsoft ASP.NET Identity EntityFramework** 패키지 합니다. Identity.EntityFramework에 대 한 설치 된 패키지를 검색 하 여이 패키지를 찾을 수 있습니다.  
    ![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image7.png)Entity Framework를 제거 하려는 경우 묻는 메시지가 표시 됩니다. 응용 프로그램의 다른 부분에 필요 하지 않은 경우에이 제거할 수 있습니다.
2. 모델 폴더에서 IdentityModels.cs 파일에서 삭제 하거나 주석으로 처리는 **ApplicationUser** 및 **ApplicationDbContext** 클래스입니다. MVC 응용 프로그램에서 전체 IdentityModels.cs 파일을 삭제할 수 있습니다. Web Forms 응용 프로그램에서는 두 개의 클래스를 삭제 하지만 IdentityModels.cs 파일에는 도우미 클래스를 유지 해야 합니다.
3. 저장소 공급자와는 별도 프로젝트에 있는 경우 웹 응용 프로그램에 대 한 참조를 추가 합니다.
4. 에 대 한 모든 참조 바꿉니다 `using Microsoft.AspNet.Identity.EntityFramework;` 을 사용 하 여 저장소 공급자의 네임 스페이스에 대 한 문입니다.
5. 에 **Startup.Auth.cs** 클래스, 변경의 **ConfigureAuth** 메서드를 적절 한 컨텍스트가의 단일 인스턴스를 사용 합니다. 

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample9.cs?highlight=3)]
6. 앱에서\_시작 폴더를 엽니다 **IdentityConfig.cs**합니다. ApplicationUserManager 클래스에서 변경 된 **만들기** 메서드를 사용자 지정 된 사용자 저장소를 사용 하는 사용자 관리자를 반환 합니다. 

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample10.cs?highlight=3)]
7. 에 대 한 모든 참조 바꿉니다 **ApplicationUser** 와 **IdentityUser**합니다.
8. 기본 프로젝트 면 IUser 인터페이스에서 정의 되지 않은 사용자 클래스에서는 일부 멤버를 포함 합니다. 메일, PasswordHash, 등 GenerateUserIdentityAsync 합니다. 사용자 클래스에 이러한 멤버에 없는 경우 구현 하거나 이러한 멤버를 사용 하는 코드를 변경 합니다.
9. RoleManager의 모든 인스턴스를 만들면 새 RoleStore 클래스를 사용 하도록 코드를 변경 합니다.  

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample11.cs)]
10. 기본 프로젝트에는 키에 대 한 문자열 값을 갖는 사용자 클래스에 대 한 설계 되었습니다. 사용자 클래스에는 키 (예: 정수)에 대 한 다른 형식이 있으면 사용자 형식을 사용 하려면 프로젝트를 변경 해야 합니다. 참조 [ASP.NET Identity에서 사용자에 대 한 기본 키를 변경](change-primary-key-for-users-in-aspnet-identity.md)합니다.
11. 필요한 경우 연결 문자열을 Web.config 파일을 추가 합니다.

<a id="other"></a>
## <a name="other-resources"></a>기타 리소스

- 블로그: [ASP.NET Identity 구현](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx)
- 자습서 및 GIT 코드: [Simple.Data Asp.Net Id 공급자](http://designcoderelease.blogspot.co.uk/2015/03/simpledata-aspnet-identity-provider.html)
- 자습서:[기본 Id 계정은를 설정 하 고 외부 데이터베이스를 가리키는 이러한](http://typecastexception.com/post/2013/10/27/Configuring-Db-Connection-and-Code-First-Migration-for-Identity-Accounts-in-ASPNET-MVC-5-and-Visual-Studio-2013.aspx)합니다. 여 [ @xivSolutions ](https://twitter.com/xivSolutions)합니다.
- 자습서[: 사용자 지정 MySQL ASP.NET Identity 저장소 공급자 구현](implementing-a-custom-mysql-aspnet-identity-storage-provider.md)
- [CodeFluent 엔터티](http://blog.codefluententities.com/2014/04/30/asp-net-identity-v2-and-codefluent-entities/) 여 [SoftFluent](http://www.softfluent.com/)
- [Azure 테이블 저장소](https://www.nuget.org/packages/accidentalfish.aspnet.identity.azure/) James 있고 여 합니다.
- Azure 테이블 저장소: [AspNet.Identity.TableStorage](https://github.com/stuartleeks/leeksnet.AspNet.Identity.TableStorage) 여 [ @stuartleeks ](https://twitter.com/stuartleeks)합니다.
- [CouchDB / 김 Wertheim 여 Cloudant 합니다.](https://github.com/danielwertheim/mycouch.aspnet.identity)
- 탄력적 검색[h: 탄력적 Identity](https://github.com/bmbsqd/elastic-identity) Bombsquad AB. 하 여
- [MongoDB](http://www.nuget.org/packages/MongoDB.AspNet.Identity/) Jonathan Sheely Jonathan Sheely 여 합니다.
- [NHibernate.AspNet.Identity](https://github.com/milesibastos/NHibernate.AspNet.Identity) Antônio Milesi Bastos 여 합니다.
- [RavenDB](http://www.nuget.org/packages/AspNet.Identity.RavenDB/1.0.0) 여 [ @tourismgeek ](https://twitter.com/tourismgeek)합니다.
- [RavenDB.AspNet.Identity](https://github.com/ILMServices/RavenDB.AspNet.Identity) 여 [ILMServices](http://www.ilmservice.com/)합니다.
- Redis: [Redis.AspNet.Identity](https://github.com/aminjam/Redis.AspNet.Identity)
- "데이터베이스 먼저" 사용자 저장소에 대 한 코드 EF를 생성 하도록 T4 템플릿을: [AspNet.Identity.EntityFramework](https://github.com/cbfrank/AspNet.Identity.EntityFramework)
