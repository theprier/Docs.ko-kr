---
uid: web-forms/overview/older-versions-security/roles/creating-and-managing-roles-cs
title: 만들기 및 관리 역할 (C#) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 역할 프레임 워크를 구성 하는 데 필요한 단계를 검사 합니다. 그런 다음, 웹 페이지를 만들고 삭제할 역할을 작성 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/24/2008
ms.topic: article
ms.assetid: 113f10b3-a19a-471b-8ff6-db3c79ce8a91
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-security/roles/creating-and-managing-roles-cs
msc.type: authoredcontent
ms.openlocfilehash: a4ea7e76e023cd436d1d8ac52307a3ac17267fef
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
---
<a name="creating-and-managing-roles-c"></a>만들기 및 관리 역할 (C#)
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/CS.09.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial09_CreatingRoles_cs.pdf)

> 이 자습서에서는 역할 프레임 워크를 구성 하는 데 필요한 단계를 검사 합니다. 그런 다음, 웹 페이지를 만들고 삭제할 역할을 작성 합니다.


## <a name="introduction"></a>소개

에 <a id="_msoanchor_1"> </a> [ *사용자 기반 권한 부여* ](../membership/user-based-authorization-cs.md) 자습서에 페이지 집합에서 특정 사용자가 제한 하려면 URL 권한 부여를 사용 하 여 검토 하 고 선언적 탐색 하 고 방문한 사용자를 기반으로 하는 ASP.NET 페이지의 기능을 조정 하기 위한 프로그래밍 기술입니다. 그러나 페이지 액세스 또는 사용자가 사용자 단위로 기능에 대 한 권한을 부여, 될 수 있습니다 시나리오에서 유지 관리 밋 없는 여러 사용자 계정 또는 사용자의 권한을 자주 변경 될 때. 언제 든 지 사용자를 얻거나 잃을 특정 태스크를 수행할 수 있는 관리자가 적절 한 URL 권한 부여 규칙, 선언 태그 및 코드를 업데이트 해야 합니다.

일반적으로 사용자가 그룹으로 분류할 수 있습니다 또는 *역할* 다음 역할-역할별 별로 사용 권한을 적용 하 합니다. 예를 들어 대부분의 웹 응용 프로그램에는 특정 페이지 또는 관리 사용자에 대해서만 예약 된 작업입니다. 배운 기술을 사용 하 여 *사용자 기반 권한 부여* 적절 한 URL 권한 부여 규칙, 선언적 태그 및 지정 된 사용자 계정 관리 작업을 수행할 수 있도록 코드를 추가할 것 자습서입니다. 하지만 새 관리자 추가 된 경우 또는 기존 관리자의 관리 권한이 해지 하는 데 필요한 경우 해야 반환 하 고 구성 파일 및 웹 페이지를 업데이트 합니다. 하지만 역할을 사용 우리 관리자 라는 역할 만들고 이러한 신뢰할 수 있는 사용자의 관리자 역할에 할당 합니다. 그런 다음 적절 한 URL 권한 부여 규칙, 선언적 태그 및 관리자 역할 다양 한 관리 작업을 수행할 수 있도록 코드를 추가할 것입니다. 이 인프라와 사이트 새 관리자를 추가 하거나 기존의 유형을 제거 하기만 하면를 포함 하거나 사용자의 관리자 역할에서 제거 됩니다. 구성, 선언 태그 또는 코드 변경 내용 없음는 필요 합니다.

ASP.NET 역할 정의 및 사용자 계정으로 연결 하는 역할 프레임 워크를 제공 합니다. 역할 framework 만들고 역할을 삭제할 수 있습니다를 사용 하면 역할에서 사용자를 제거 하거나, 특정 역할에 속할 수 있으며 사용자는 특정 역할에 속하는지 여부를 판단할 수 있는 사용자 집합을 결정 하는 사용자를 추가 합니다. 역할 프레임 워크 구성 되 면 म 수 URL 권한 부여 규칙을 통해 역할-역할별 별로 페이지에 대 한 액세스를 제한 하 고 또는 표시 하거나 숨길 추가 정보 현재 로그온된 한 사용자의 역할을 기반으로 하는 페이지에서 기능입니다.

이 자습서에서는 역할 프레임 워크를 구성 하는 데 필요한 단계를 검사 합니다. 그런 다음, 웹 페이지를 만들고 삭제할 역할을 작성 합니다. 에 <a id="_msoanchor_2"> </a> [ *사용자에 게 역할 할당* ](assigning-roles-to-users-cs.md) 자습서 추가 하 고 역할에서 사용자를 제거 하는 방법을 살펴보겠습니다. 및에 <a id="_msoanchor_3"> </a> [ *역할 기반 권한 부여* ](role-based-authorization-cs.md) 자습서 페이지 기능에 따라 조정 하는 방법 함께 역할-역할별 별로 페이지에 대 한 액세스를 제한 하는 방법과 방문한 사용자의 역할입니다. 이제 시작 하겠습니다.

## <a name="step-1-adding-new-aspnet-pages"></a>1 단계: 새 ASP.NET 페이지를 추가합니다.

이 자습서에는 다음 두 우리는 수 검사 다양 한 역할 기반 기능 및 기능입니다. 일련의 전체이 자습서에서 설명 하는 항목을 구현 하는 ASP.NET 페이지가 필요 합니다. 이러한 페이지를 만들고 사이트 맵 업데이트 하겠습니다.

시작 이라는 프로젝트에 새 폴더를 만들어서 `Roles`합니다. 다음으로 4 개의 새로운 ASP.NET 페이지에 추가 `Roles` 폴더를 연결 된 각 페이지는 `Site.master` 마스터 페이지입니다. 페이지 이름을 지정 합니다.

- `ManageRoles.aspx`
- `UsersAndRoles.aspx`
- `CreateUserWizardWithRoles.aspx`
- `RoleBasedAuthorization.aspx`

이 시점에서 프로젝트의 솔루션 탐색기에 스크린 샷을 그림 1에 표시 된 비슷해야 합니다.


[![역할 폴더에 추가 된 4 개의 새 페이지](creating-and-managing-roles-cs/_static/image2.png)](creating-and-managing-roles-cs/_static/image1.png)

**그림 1**: 4 개의 새 페이지에 추가 된는 `Roles` 폴더 ([전체 크기 이미지를 보려면 클릭](creating-and-managing-roles-cs/_static/image3.png))


각 페이지,이 시점에서 있어야 마스터 페이지의 contentplaceholders의 마다 하나씩 두 개의 콘텐츠 컨트롤: `MainContent` 및 `LoginContent`합니다.

[!code-aspx[Main](creating-and-managing-roles-cs/samples/sample1.aspx)]

이전에 설명한 대로 `LoginContent` ContentPlaceHolder의 기본 태그 로그온 하거나 로그 오프 사용자가 인증 되는지 여부에 따라 사이트에 대 한 링크를 표시 합니다. 그러나 존재는 `Content2` 콘텐츠 컨트롤은 ASP.NET 페이지에 마스터 페이지의 기본 태그를 재정의 합니다. 설명한 것 처럼 <a id="_msoanchor_4"> </a> [ *폼 인증의 개요는* ](../introduction/an-overview-of-forms-authentication-cs.md) 자습서에서는 기본 태그를 재정의 합니다. 여기서 म 하지 않으려는 표시 로그인 관련 페이지에 유용 왼쪽된 열에 대 한 옵션입니다.

그러나 이러한 4 개 페이지에 대 한 표시 하려고에 대 한 마스터 페이지의 기본 태그는 `LoginContent` ContentPlaceHolder 합니다. 따라서 태그에 대 한 선언적 태그를 제거는 `Content2` 콘텐츠 컨트롤을 합니다. 이렇게 한 다음 4 개의 페이지의 태그의 각 콘텐츠 컨트롤을 한 개만 있어야 합니다.

마지막으로, 사이트 맵 업데이트 (`Web.sitemap`) 이러한 새 웹 페이지를 포함 하도록 합니다. 추가 후 다음 XML는 `<siteMapNode>` 구성원 자습서에 대 한 추가 했습니다.

[!code-xml[Main](creating-and-managing-roles-cs/samples/sample2.xml)]

업데이트 사이트 맵을 사용 하 여 브라우저를 통해 사이트를 방문 합니다. 그림 2에서 볼 수 있듯이 이제 왼쪽 탐색 역할 자습서에 대 한 항목이 포함 됩니다.


[![역할 폴더에 추가 된 4 개의 새 페이지](creating-and-managing-roles-cs/_static/image5.png)](creating-and-managing-roles-cs/_static/image4.png)

**그림 2**: 4 개의 새 페이지에 추가 된는 `Roles` 폴더 ([전체 크기 이미지를 보려면 클릭](creating-and-managing-roles-cs/_static/image6.png))


## <a name="step-2-specifying-and-configuring-the-roles-framework-provider"></a>지정 하 고 역할 Framework 공급자를 구성 하는 2 단계:

멤버 자격 프레임 워크와 같은 역할 framework 공급자 모델 기반 만들어집니다. 에 설명 된 대로 <a id="_msoanchor_5"> </a> [ *보안 기본 사항 및 ASP.NET 지원* ](../introduction/security-basics-and-asp-net-support-cs.md) 자습서에서는 세 가지 기본 제공 역할 공급자와 함께 제공 되는.NET Framework: [ `AuthorizationStoreRoleProvider` ](https://msdn.microsoft.com/library/system.web.security.authorizationstoreroleprovider.aspx) [ `WindowsTokenRoleProvider` ](https://msdn.microsoft.com/library/system.web.security.windowstokenroleprovider.aspx), 및 [ `SqlRoleProvider` ](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx)합니다. 이 자습서 시리즈에 중점을 둡니다는 `SqlRoleProvider`, Microsoft SQL Server 데이터베이스 역할 저장소 기호로 사용 합니다.

내부적 역할 프레임 워크 및 `SqlRoleProvider` 구성원 프레임 워크와 동일 하 게 작동 하 고 `SqlMembershipProvider`합니다. .NET Framework를 포함 한 `Roles` 역할 프레임 워크 API로 사용 되는 클래스입니다. `Roles` 클래스에는 같은 정적 메서드가 `CreateRole`, `DeleteRole`, `GetAllRoles`, `AddUserToRole`, `IsUserInRole`, 등입니다. 이러한 방법 중 하나를 호출 하면는 `Roles` 클래스 구성 된 공급자에 대 한 호출을 위임 합니다. `SqlRoleProvider` 역할 관련 테이블을 사용 (`aspnet_Roles` 및 `aspnet_UsersInRoles`)에 대 한 응답입니다.

사용 하려면는 `SqlRoleProvider` 부터 내용을 저장소로 사용할 데이터베이스를 지정 해야이 응용 프로그램에서 공급자입니다. `SqlRoleProvider` 특정 데이터베이스 테이블, 뷰 및 저장된 프로시저는 지정 된 역할 저장소를 예상 합니다. 사용 하 여 이러한 필요한 데이터베이스 개체를 추가할 수는 [ `aspnet_regsql.exe` 도구](https://msdn.microsoft.com/library/ms229862.aspx)합니다. 이 시점에 필요한 스키마를 사용 하 여 데이터베이스 이미 보유는 `SqlRoleProvider`합니다. 에 <a id="_msoanchor_6"> </a> [ *SQL Server에서 멤버 자격 스키마 만들기* ](../membership/creating-the-membership-schema-in-sql-server-cs.md) 자습서 라는 데이터베이스를 만들었습니다 `SecurityTutorials.mdf` 사용 `aspnet_regsql.exe` 응용 프로그램을 추가 하려면 에 필요한 데이터베이스 개체를 포함 하는 서비스는 `SqlRoleProvider`합니다. 따라서 त ु म 역할 지원을 사용 하도록 설정 하 고 사용 하도록 역할 프레임 워크에 알립니다는 `SqlRoleProvider` 와 `SecurityTutorials.mdf` 역할 저장소와 데이터베이스입니다.

역할 프레임 워크를 통해 구성 됩니다는 &lt; `roleManager` &gt; 응용 프로그램의 요소 `Web.config` 파일입니다. 기본적으로 역할 지원은 사용할 수 없습니다. 을 사용 하려면 설정 해야 합니다는 [ &lt; `roleManager` &gt; ](https://msdn.microsoft.com/library/ms164660.aspx) 요소의 `enabled` 특성을 `true` 같이:

[!code-xml[Main](creating-and-managing-roles-cs/samples/sample3.xml)]

모든 웹 응용 프로그램을 기본적으로 명명 된 역할 공급자는 `AspNetSqlRoleProvider` 형식의 `SqlRoleProvider`합니다. 이 기본 공급자에 등록 되어 `machine.config` (에 있는 `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG`):

[!code-xml[Main](creating-and-managing-roles-cs/samples/sample4.xml)]

공급자의 `connectionStringName` 사용 되는 역할 저장소 특성을 지정 합니다. `AspNetSqlRoleProvider` 이 특성을 설정 하는 공급자 `LocalSqlServer`에 정의 되어 있는 `machine.config` 및 SQL Server 2005 Express Edition 데이터베이스에 기본적으로 포인트는 `App_Data` 라는 폴더 `aspnet.mdf`합니다.

따라서 단순히 역할 framework 응용 프로그램의 모든 공급자 정보를 지정 하지 않고 사용 하도록 설정 하는 경우 `Web.config` 파일, 응용 프로그램에 등록 된 기본 역할 공급자를 사용 하 여 `AspNetSqlRoleProvider`합니다. 경우는 `~/App_Data/aspnet.mdf` 데이터베이스가 존재 하지 않습니다, ASP.NET 런타임이 자동으로 만들고 응용 프로그램 서비스 스키마를 추가 합니다. 그러나 사용 하려는 하지는 `aspnet.mdf` 데이터베이스; 대신 사용 하려는 `SecurityTutorials.mdf` 데이터베이스를 이미 만든 했으며에 응용 프로그램 서비스 스키마를 추가 합니다. 두 가지 방법 중 하나에서이 수정 작업을 수행할 수 있습니다.

- <strong>에 대 한 값을 지정 된</strong><strong>`LocalSqlServer`</strong><strong>의 연결 문자열 이름</strong><strong>`Web.config`</strong><strong>합니다.</strong> 덮어쓰는 방법으로 `LocalSqlServer` 연결 문자열 이름 값의 `Web.config`, 등록 된 기본 역할 공급자를 사용할 수 있습니다 (`AspNetSqlRoleProvider`)와 올바르게 사용할는 `SecurityTutorials.mdf` 데이터베이스입니다. 이 방법에 대 한 자세한 내용은 참조 하십시오. [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 블로그 게시물 [구성 ASP.NET 2.0 응용 프로그램 서비스를 사용 하 여 SQL Server 2000 또는 SQL Server 2005](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)합니다.
- <strong>형식의 새 등록 된 공급자를 추가</strong><strong>`SqlRoleProvider`</strong><strong>구성 및 해당</strong><strong>`connectionStringName`</strong><strong>는를가리키도록설정</strong> <strong>`SecurityTutorials.mdf`</strong> <strong>데이터베이스입니다.</strong> 이것은 좋으며에 사용 되는 방식에서 <a id="_msoanchor_7"> </a> [ *SQL Server에서 멤버 자격 스키마 만들기* ](../membership/creating-the-membership-schema-in-sql-server-cs.md) 자습서와이 방식은이 자습서에서를 사용 합니다.

다음 역할 구성 태그를 추가 `Web.config` 파일입니다. 라는 새 공급자를 등록 하는이 태그 `SecurityTutorialsSqlRoleProvider`합니다.

[!code-xml[Main](creating-and-managing-roles-cs/samples/sample5.xml)]

위의 태그 정의 `SecurityTutorialsSqlRoleProvider` 기본 공급자로 (통해는 `defaultProvider` 특성에 `<roleManager>` 요소). 또한 설정는 `SecurityTutorialsSqlRoleProvider`의 `applicationName` 설정을 `SecurityTutorials`, 동일한 `applicationName` 멤버 자격 공급자가 사용 되는 설정을 (`SecurityTutorialsSqlMembershipProvider`). 여기에서 표시 하지는 [ `<add>` 요소](https://msdn.microsoft.com/library/ms164662.aspx) 에 대 한는 `SqlRoleProvider` 포함 될 수도 있습니다는 `commandTimeout` 특성을 데이터베이스 시간 제한 기간을 초 단위로 지정 합니다. 기본값은 30입니다.

위치에이 구성 태그에서는 응용 프로그램 내에서 역할 기능을 사용 하 여 시작할 준비가 된 것입니다.

> [!NOTE]
> 위의 구성 태그에서는 사용 하 여는 &lt; `roleManager` &gt; 요소의 `enabled` 및 `defaultProvider` 특성입니다. 역할 프레임 워크에서 사용자가 사용자 단위로 역할 정보를 연결 하는 방식에 영향을 주는 다른 특성의 여러 가지가 있습니다. 이러한 설정을 검토 합니다는 <a id="_msoanchor_8"> </a> [ *역할 기반 권한 부여* ](role-based-authorization-cs.md) 자습서입니다.


## <a name="step-3-examining-the-roles-api"></a>3 단계: API 역할 검사

역할 프레임 워크의 기능을 통해 노출 되는 [ `Roles` 클래스](https://msdn.microsoft.com/library/system.web.security.roles.aspx), 역할 기반 작업을 수행 하기 위한 정적 메서드를 13 개 포함 된 합니다. 의견에 귀를 작성 하 고 4 단계에서에서 역할을 삭제할 시점과 6을 사용 합니다는 [ `CreateRole` ](https://msdn.microsoft.com/library/system.web.security.roles.createrole.aspx) 및 [ `DeleteRole` ](https://msdn.microsoft.com/library/system.web.security.roles.deleterole.aspx) 메서드를 추가 하거나 시스템에서 역할을 제거 합니다.

시스템을 가져오려면 모든 역할 목록을 사용 하 여는 [ `GetAllRoles` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.getallroles.aspx) (5 단계 참조). [ `RoleExists` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.roleexists.aspx) 지정된 된 역할에 있는지 여부를 나타내는 부울 값을 반환 합니다.

다음 자습서에서는 사용자가 역할과 연결 하는 방법을 살펴보겠습니다. `Roles` 클래스의 [ `AddUserToRole` ](https://msdn.microsoft.com/library/system.web.security.roles.addusertorole.aspx), [ `AddUserToRoles` ](https://msdn.microsoft.com/library/system.web.security.roles.addusertoroles.aspx), [ `AddUsersToRole` ](https://msdn.microsoft.com/library/system.web.security.roles.adduserstorole.aspx), 및 [ `AddUsersToRoles` ](https://msdn.microsoft.com/library/system.web.security.roles.adduserstoroles.aspx) 메서드는 하나 이상의 역할에 하나 이상의 사용자를 추가합니다. 에서 제거 하려면 사용자 역할을 사용 하 여는 [ `RemoveUserFromRole` ](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromrole.aspx), [ `RemoveUserFromRoles` ](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromroles.aspx), [ `RemoveUsersFromRole` ](https://msdn.microsoft.com/library/system.web.security.roles.removeusersfromrole.aspx), 또는 [ `RemoveUsersFromRoles` ](https://msdn.microsoft.com/library/system.web.security.roles.removeusersfromroles.aspx) 메서드를 합니다.

에 <a id="_msoanchor_9"> </a> [ *역할 기반 권한 부여* ](role-based-authorization-cs.md) 자습서 프로그래밍 방식으로 표시 하거나 숨기기 기능 현재 로그인된 한 사용자의 역할 기반으로 하는 방법을 살펴보겠습니다. 이를 위해 사용할 수는 `Role` 클래스의 [ `FindUsersInRole` ](https://msdn.microsoft.com/library/system.web.security.roles.findusersinrole.aspx), [ `GetRolesForUser` ](https://msdn.microsoft.com/library/system.web.security.roles.getrolesforuser.aspx), [ `GetUsersInRole` ](https://msdn.microsoft.com/library/system.web.security.roles.getusersinrole.aspx), 또는 [ `IsUserInRole` ](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx) 메서드.

> [!NOTE]
> 언제 든 지 이러한 메서드 중 하나를 호출 하 여 `Roles` 클래스 구성 된 공급자에 대 한 호출을 위임 합니다. 이 경우 즉, 호출에 보내지는 `SqlRoleProvider`합니다. `SqlRoleProvider` 다음 호출 된 메서드가에 따라 적절 한 데이터베이스 작업을 수행 합니다. 코드 예를 들어 `Roles.CreateRole("Administrators")` 결과 `SqlRoleProvider` 실행는 `aspnet_Roles_CreateRole` 저장 프로시저에 새 레코드를 삽입 하는 `aspnet_Roles` 관리자 라는 테이블입니다.


이 자습서의 나머지 부분에서는 `Roles` 클래스의 `CreateRole`, `GetAllRoles`, 및 `DeleteRole` 시스템에서 역할을 관리 하는 메서드.

## <a name="step-4-creating-new-roles"></a>4 단계: 새 역할 만들기

역할 그룹 사용자가 임의로 하는 방법을 제공 하 고 권한 부여 규칙을 적용 하는 보다 편리한 방법을이 그룹화 가장 일반적으로 사용 됩니다. 하지만 역할 권한 부여 메커니즘으로 사용 하려면 먼저 정의 해야 역할의 응용 프로그램에 존재 합니다. 그러나 ASP.NET CreateRoleWizard 컨트롤을 포함 하지 않습니다. 새 역할 추가 하려면를 적절 한 사용자 인터페이스를 만들고 역할 API를 직접 호출 해야 합니다. 다행히가 하기가 매우 쉽습니다 된다는 점입니다.

> [!NOTE]
> CreateRoleWizard 웹 컨트롤이 이면 있지만는 [ASP.NET 웹 사이트 관리 도구](https://msdn.microsoft.com/library/ms228053.aspx), 보기 및 관리 웹 응용 프로그램의 구성을 지원 하기 위해 설계 된 로컬 ASP.NET 응용 프로그램은입니다. 그러나 두 가지 이유로 ASP.NET 웹 사이트 관리 도구의 선호 없는 경우 첫째, 약간 버그가 있는 것이 고 사용자 환경 개선의 여지가 권장 될. 둘째, ASP.NET 웹 사이트 관리 도구는 라이브 사이트에 대 한 역할을 원격으로 관리 하는 경우 고유한 역할 관리 웹 페이지를 작성 해야 한다는 의미를 로컬로만 작동 하도록 설계 되었습니다. 이러한 두 가지 이유로이 자습서와 다음 중점적으로 ASP.NET 웹 사이트 관리 도구에 의존 하는 대신 관리 도구는 웹 페이지에 필요한 역할을 작성 합니다.


열기는 `ManageRoles.aspx` 페이지에 `Roles` 폴더 페이지에 텍스트 상자 및 단추 웹 컨트롤을 추가 합니다. TextBox 컨트롤의 설정 `ID` 속성을 `RoleName` 및 단추의 `ID` 및 `Text` 속성을 `CreateRoleButton` 역할 만들기 및 각각. 이 시점에서 페이지의 선언적 태그는 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](creating-and-managing-roles-cs/samples/sample6.aspx)]

다음으로 두 번 클릭는 `CreateRoleButton` 단추를 만들려면 디자이너에서 컨트롤은 `Click` 이벤트 처리기 다음 코드를 추가 합니다.

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample7.cs)]

에 입력 한 트리밍된 역할 이름을 지정 하 여 시작 하는 위의 코드는 `RoleName` 를 텍스트 상자는 `newRoleName` 변수입니다. 그런 다음는 `Roles` 클래스의 `RoleExists` 메서드를 호출 하는 경우를 결정 하는 역할 `newRoleName` 시스템에 이미 있습니다. 에 대 한 호출을 통해 만들어집니다 역할이 없는 경우는 `CreateRole` 메서드. 경우는 `CreateRole` 메서드는 시스템에 이미 있는 역할 이름을 전달 되는 `ProviderException` 예외가 throw 됩니다. 이 때문에 역할 호출 하기 전에 시스템에 이미 존재 하지 않는지 확인 하는 코드는 먼저 확인 `CreateRole`합니다. `Click` 선택을 취소 하 여 이벤트 처리기가 종료 된 `RoleName` 텍스트 상자의 `Text` 속성입니다.

> [!NOTE]
> 어떻게 할까요 사용자는 모든 값을 입력 하지 않습니다는 `RoleName` 텍스트 상자에 붙여넣습니다. 에 전달 된 값은 `CreateRole` 방법은 `null` 또는 빈 문자열인 경우 예외가 발생 합니다. 마찬가지로, 역할 이름에 쉼표가 포함 되어 있으면 예외가 발생 합니다. 따라서 페이지는 사용자가 역할을 입력 하 고 쉼표가 포함 하지 않는 되도록 유효성 검사 컨트롤을 포함 해야 합니다. I 판독기에 대 한 연습으로 그대로 둡니다.


관리자 라고 하는 역할을 만들어 보겠습니다. 방문는 `ManageRoles.aspx` 브라우저를 통해 페이지 상자에 붙여넣습니다 관리자에 입력 합니다 (그림 3 참조) 한 다음 역할 만들기 단추를 클릭 합니다.


[![관리자 역할 만들기](creating-and-managing-roles-cs/_static/image8.png)](creating-and-managing-roles-cs/_static/image7.png)

**그림 3**: 관리자 역할을 만듭니다 ([전체 크기 이미지를 보려면 클릭](creating-and-managing-roles-cs/_static/image9.png))


어떻게 됩니까? 포스트백이 발생할 이지만 역할 실제로 된 시각적 표시가 없습니다 시스템에 추가 합니다. 이 페이지를 시각적 피드백을 포함 하려면 5 단계에서에서 업데이트 됩니다. 하지만 지금은 확인할 수 있습니다으로 이동 하 여 역할을 만든는 `SecurityTutorials.mdf` 데이터베이스에서 데이터를 표시 하는 `aspnet_Roles` 테이블입니다. 그림 4에서 볼 수 있듯이 `aspnet_Roles` 테이블 방금 추가 된 관리자 역할에 대 한 레코드를 포함 합니다.


[![테이블 aspnet_Roles 관리자에 대 한 행을 갖습니다.](creating-and-managing-roles-cs/_static/image11.png)](creating-and-managing-roles-cs/_static/image10.png)

**그림 4**:는 `aspnet_Roles` 테이블에는 관리자에 대 한 행이 있습니다 ([전체 크기 이미지를 보려면 클릭](creating-and-managing-roles-cs/_static/image12.png))


## <a name="step-5-displaying-the-roles-in-the-system"></a>5 단계: 시스템에서 역할을 표시

하겠습니다를 확장 하 고 `ManageRoles.aspx` 시스템의 현재 역할의 목록을 포함 하는 페이지입니다. 이를 위해 페이지에 GridView 컨트롤을 추가 하 고 설정의 `ID` 속성을 `RoleList`합니다. 다음으로 명명 된 페이지의 코드 숨김 클래스에 메서드를 추가 `DisplayRolesInGrid` 다음 코드를 사용 하 여:

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample8.cs)]

`Roles` 클래스의 `GetAllRoles` 메서드 모든 역할의 시스템으로 반환 문자열 배열입니다. 이 문자열 배열 GridView에 바인딩됩니다. 호출 해야 역할의 목록을 GridView에 페이지가 처음 로드 될 때에 바인딩하려면는 `DisplayRolesInGrid` 페이지의 메서드에서 `Page_Load` 이벤트 처리기입니다. 다음 코드 페이지를 처음 방문 하는 경우에 없지만 후속 포스트백이이 메서드를 호출 합니다.

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample9.cs)]

이 코드가 브라우저를 통해 페이지를 방문 합니다. 그림 5에서 볼 수 있듯이 항목 레이블이 지정 된 단일 열과 표를 표시 됩니다. 표 4 단계에서에서 추가 관리자 역할에 대 한 행을 포함 합니다.


[![단일 열에는 역할을 표시 하는 GridView](creating-and-managing-roles-cs/_static/image14.png)](creating-and-managing-roles-cs/_static/image13.png)

**그림 5**: 단일 열에는 역할을 표시 하는 GridView ([전체 크기 이미지를 보려면 클릭](creating-and-managing-roles-cs/_static/image15.png))


GridView 때문에 항목을 레이블이 지정 된 유일한 열이 표시 됩니다는 GridView `AutoGenerateColumns` GridView의 각 속성에 대 한 열을 자동으로 만들려고 하면 True (기본값) 이면 속성이 해당 `DataSource`합니다. 배열에 GridView의 단일 열 이므로 배열에 있는 요소를 나타내는 단일 속성이 있습니다.

GridView 사용 하 여 데이터를 표시할 때 명시적으로 내 열을 정의 하지 않고 GridView에서 암시적으로 생성 되도록 할 않겠습니다. 훨씬 쉽게 데이터의 형식을 지정 하는 열에 명시적으로 정의 하 여 열을 다시 정렬 하 고, 다른 일반적인 작업을 수행 합니다. 따라서 보겠습니다 GridView의 선언적 태그 있도록 업데이트 열이 명시적으로 정의 됩니다.

GridView의 설정 하 여 시작 `AutoGenerateColumns` 속성을 false로 합니다. 다음으로 설정에서 표를 TemplateField 추가 해당 `HeaderText` 속성 역할을 하 고 구성 해당 `ItemTemplate` 배열의 내용을 표시 되도록 합니다. 이를 위해 라는 Label 웹 컨트롤을 추가 `RoleNameLabel` 에 `ItemTemplate` 바인딩하고 해당 `Text` 속성을 `Container.DataItem`합니다.

이러한 속성 및 `ItemTemplate`의 내용을 통해 선언적으로 또는 GridView의 필드 대화 상자 및 템플릿 편집 인터페이스 설정할 수 있습니다. 필드 대화 상자에 도달 하는 GridView의 스마트 태그에 열 편집 링크를 클릭 합니다. 다음으로 설정 하려면 자동 생성 필드 확인란의 선택을 취소는 `AutoGenerateColumns` 속성을 false로, 설정를 TemplateField GridView에 추가 하 고 해당 `HeaderText` 속성 역할을 합니다. 정의 하는 `ItemTemplate`의 내용, GridView의 스마트 태그에서 템플릿 편집 옵션을 선택 합니다. Label 웹 컨트롤을 끌어는 `ItemTemplate`설정, 해당 `ID` 속성을 `RoleNameLabel`, 해당 데이터 바인딩 설정을 구성 하 고 되도록 해당 `Text` 속성이 바인딩된 `Container.DataItem`합니다.

사용 하는 방법에 관계 없이 GridView의 결과 선언적 태그 완료 되 면 다음과 비슷한 표시 됩니다.

[!code-aspx[Main](creating-and-managing-roles-cs/samples/sample10.aspx)]

> [!NOTE]
> 데이터 바인딩 구문을 사용 하 여 배열의 내용을 표시 `<%# Container.DataItem %>`합니다. 철저 한 설명은 이유이 구문을 사용 하 여 GridView에 바인딩되어 있는 배열의 내용을 표시 하는 경우이 자습서의 범위를 벗어납니다. 이 문제에 대 한 자세한 내용은 참조 [스칼라 배열 데이터 웹 컨트롤에 바인딩하거나](http://aspnet.4guysfromrolla.com/articles/082504-1.aspx)합니다.


현재는 `RoleList` GridView 해당 페이지를 처음 방문 하는 경우에 역할의 목록에 연결 되어 있습니다. 새 역할을 추가할 때마다 눈금을 갱신 해야 합니다. 이를 위해 업데이트는 `CreateRoleButton` 단추의 `Click` 되므로 호출 하는 이벤트 처리기는 `DisplayRolesInGrid` 메서드 새 역할이 생성 될 경우.

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample11.cs)]

사용자는 새 역할을 추가 하는 경우 이제는 `RoleList` 역할을 성공적으로 만든 시각적 피드백을 제공 하 GridView 다시 게시 될 방금 추가 된 역할을 표시 합니다. 방문이 설명 하기는 `ManageRoles.aspx` 브라우저를 통해 페이지 고 감독자 라는 역할을 추가 합니다. 역할 만들기 단추를 클릭 하면 계속 다시 게시 될 것 이라고 하 고 표에 새 역할 감독자 뿐만 아니라 관리자가 포함 하도록 업데이트 됩니다.


[![감독자 역할에 추가 된](creating-and-managing-roles-cs/_static/image17.png)](creating-and-managing-roles-cs/_static/image16.png)

**그림 6**: The 감독자 역할에 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](creating-and-managing-roles-cs/_static/image18.png))


## <a name="step-6-deleting-roles"></a>6 단계: 역할 삭제

이 시점에서 사용자는 새 역할을 만들고 볼 수에서 기존의 모든 역할의 `ManageRoles.aspx` 페이지. 역할을 삭제할 수도 있습니다 보겠습니다. `Roles.DeleteRole` 메서드에 두 개의 오버 로드가 있습니다.

- [`DeleteRole(roleName)`](https://msdn.microsoft.com/library/ek4sywc0.aspx) -역할이 삭제 *roleName*합니다. 역할 하나 이상의 멤버를 포함 하는 경우 예외가 throw 됩니다.
- [`DeleteRole(roleName, throwOnPopulatedRole)`](https://msdn.microsoft.com/library/38h6wf59.aspx) -역할이 삭제 *roleName*합니다. 경우 *throwOnPopulateRole* 은 `true`, 역할 하나 이상의 멤버를 포함 하는 경우 예외가 throw 됩니다. 경우 *throwOnPopulateRole* 은 `false`, 역할 또는 멤버를 포함 하는지 여부를 삭제 됩니다. 내부적으로 `DeleteRole(roleName)` 메서드 호출 `DeleteRole(roleName, true)`합니다.

`DeleteRole` 메서드는 경우에 예외를 throw *roleName* 은 `null` 또는 빈 문자열인 경우 *roleName* 에 쉼표가 포함 되어 있습니다. 경우 *roleName* 시스템에 존재 하지 않는 `DeleteRole` 예외가 발생 하지 않고 자동으로 실패 합니다.

GridView에서를 확장 하는 보겠습니다 `ManageRoles.aspx` 포함 하려면 삭제 단추를 클릭 하면 선택한 역할을 삭제 합니다. 필드 대화 상자로 이동 하는 CommandField 옵션 아래에 있는 삭제 단추를 추가 하 여 GridView를 삭제 단추를 추가 하 여 시작 합니다. 맨 왼쪽된 열 단추 설정 및 삭제를 확인 합니다. 해당 `DeleteText` 속성 삭제할 역할을 합니다.


[![RoleList GridView에 삭제 단추를 추가 합니다.](creating-and-managing-roles-cs/_static/image20.png)](creating-and-managing-roles-cs/_static/image19.png)

**그림 7**: 삭제 단추를 추가할는 `RoleList` GridView ([전체 크기 이미지를 보려면 클릭](creating-and-managing-roles-cs/_static/image21.png))


삭제 단추를 추가한 후 GridView의 선언적 태그는 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](creating-and-managing-roles-cs/samples/sample12.aspx)]

다음으로 GridView에 대 한 이벤트 처리기를 만들고 `RowDeleting` 이벤트입니다. 역할 삭제 단추를 클릭할 때 포스트백에서 발생 하는 이벤트입니다. 다음 코드를 이벤트 처리기에 추가합니다.

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample13.cs)]

프로그래밍 방식으로 참조 하 여 시작 하는 코드는 `RoleNameLabel` 웹 인 역할 삭제 단추를 클릭 한 행에는 컨트롤입니다. `Roles.DeleteRole` 다음 메서드, 전달는 `Text` 의 `RoleNameLabel` 및 `false`없어지고 여부에 관계 없이 역할을 삭제 하면 역할에 연결 된 사용자가 있습니다. 마지막으로 `RoleList` GridView를 새로 고치면 just 삭제 된 역할은 더 이상 눈금에 표시 합니다.

> [!NOTE]
> 역할 삭제 단추는 모든 종류의 사용자 로부터 역할을 삭제 하기 전에 확인 필요 하지 않습니다. 작업을 확인 하는 가장 쉬운 방법 중 하나는 클라이언트 쪽 확인 대화 상자입니다. 이 방법에 대 한 자세한 내용은 참조 하십시오. [추가 클라이언트 쪽 확인 때 삭제](https://asp.net/learn/data-access/tutorial-42-cs.aspx)합니다.


## <a name="summary"></a>요약

많은 웹 응용 프로그램에는 특정 권한 부여 규칙 또는 특정 클래스의 사용자 에게만 제공 되는 페이지 수준 기능 있어야 합니다. 예를 들어 관리자만 액세스할 수 있는 웹 페이지 집합이 있을 수 있습니다. 사용자가 사용자 단위로 이러한 권한 부여 규칙을 정의 하는 대신 종종 것이 더욱 유용 역할에 따라 규칙을 정의 합니다. Scott 및 Jisun 관리 웹 페이지에 액세스 하려면 사용자를 명시적으로 허용 하는 대신 더 쉽게 유지 관리할 방법 즉, 관리자 역할의 구성원이 이러한 페이지에 액세스 하도록 허용 하기 위해 다음 Scott 및 Jisun에 속하는 사용자로 표시 하는 관리자 역할입니다.

역할 프레임 워크를 통해 쉽게 만들고 역할을 관리 합니다. 이 자습서를 사용 하기 위해 역할 프레임 워크를 구성 하는 방법을 검사는 `SqlRoleProvider`, Microsoft SQL Server 데이터베이스 역할 저장소 기호로 사용 합니다. 또한 시스템의 기존 역할을 나열 하 고 새 역할을 만들 수를 허용 하는 웹 페이지 및 삭제할 기존 만든 합니다. 이후 자습서에서 사용자 역할에 할당 하는 방법 및 역할 기반 권한 부여를 적용 하는 방법을 살펴봅니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 2.0의 검사 멤버 자격, 역할 및 프로필](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [방법: ASP.NET 2.0에서에서 역할 관리자를 사용 하 여](https://msdn.microsoft.com/library/ms998314.aspx)
- [역할 공급자](https://msdn.microsoft.com/library/aa478950.aspx)
- [자신의 웹 사이트 관리 도구를 롤링합니다.](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [에 대 한 기술 문서는 `<roleManager>` 요소](https://msdn.microsoft.com/library/ms164660.aspx)
- [멤버 자격 및 역할 관리자 Api를 사용 하 여](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/membership.aspx)

### <a name="about-the-author"></a>작성자 정보

여러 ASP/ASP.NET 책의 작성자 및 4GuysFromRolla.com의 창립자 Scott Mitchell의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은  *[Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*합니다. Scott에 도달할 수 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 또는에서 그의 블로그 통해 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Alicja Maziarz, Suchi Banerjee 및 Teresa 머피의 포함 됩니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [다음](assigning-roles-to-users-cs.md)
