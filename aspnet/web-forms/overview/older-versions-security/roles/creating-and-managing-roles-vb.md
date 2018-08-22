---
uid: web-forms/overview/older-versions-security/roles/creating-and-managing-roles-vb
title: 역할 (VB) 만들기 및 관리 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 역할 프레임 워크를 구성 하는 데 필요한 단계를 검토 합니다. 그런 다음, 웹 페이지를 만들고 역할을 삭제 하려면 빌드합니다.
ms.author: riande
ms.date: 03/24/2008
ms.assetid: 83af9f5f-9a00-4f83-8afc-e98bdd49014e
msc.legacyurl: /web-forms/overview/older-versions-security/roles/creating-and-managing-roles-vb
msc.type: authoredcontent
ms.openlocfilehash: e51fa6de3d2fe7b5c9cd84900d154070eb1960b9
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41836606"
---
<a name="creating-and-managing-roles-vb"></a>만들기 및 관리 역할 (VB)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/VB.09.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial09_CreatingRoles_vb.pdf)

> 이 자습서에서는 역할 프레임 워크를 구성 하는 데 필요한 단계를 검토 합니다. 그런 다음, 웹 페이지를 만들고 역할을 삭제 하려면 빌드합니다.


## <a name="introduction"></a>소개

에 <a id="_msoanchor_1"> </a> [ *사용자 기반 권한 부여* ](../membership/user-based-authorization-vb.md) 자습서에서 URL 권한 부여를 사용 하 여 페이지 집합에서 특정 사용자를 제한 하 고 선언적 탐색 하 고 방문한 사용자를 기반으로 하는 ASP.NET 페이지의 기능을 조정 하는 것에 대 한 프로그래밍 기술입니다. 하지만 페이지 액세스 나 사용자 간 별로 기능에 대 한 권한을 부여 될 수 있습니다 시나리오에서 유지 관리 문제일 있는 많은 사용자 계정 또는 사용자의 권한을 자주 변경 하는 경우. 언제 든 지 사용자를 얻거나 잃을 특정 태스크를 수행 하려면 권한 부여 관리자는 적절 한 URL 권한 부여 규칙, 선언적 태그 및 코드를 업데이트 해야 합니다.

일반적으로 사용자를 그룹으로 분류할 수 있습니다 또는 *역할* 차례로-역할 기준 권한 적용 합니다. 예를 들어, 대부분의 웹 응용 프로그램 페이지 또는 관리 사용자에 대해서만 예약 된 작업의 특정 집합을 경우 학습 한 기술을 사용 하는 *사용자 기반 권한 부여* 적절 한 URL 권한 부여 규칙, 선언적 태그 및 코드 지정한 사용자 계정 관리 작업을 수행할 수 있도록 추가 자습서입니다. 하지만 돌아간 다음 구성 파일과 웹 페이지 업데이트를 포함 됩니다 새 관리자를 추가한 경우, 기존 관리자가 관리 권한이 해지 하는 데 필요한 경우. 그러나 역할을 사용 하 여 수 관리자 라는 역할을 만드는 하 고 관리자 역할에 이러한 신뢰할 수 있는 사용자를 할당 합니다. 그런 다음 적절 한 URL 권한 부여 규칙, 선언적 태그 및 관리자 역할을 다양 한 관리 작업을 수행할 수 있도록 코드를 추가 했습니다. 이 인프라를 구축을 사용 하 여 사이트에 새 관리자를 추가 하거나 기존의 유형을 제거 간단 하 게 포함 하 여 또는 관리자 역할에서 사용자를 제거 합니다. 구성, 선언적 태그 또는 코드 변경 없이 필요 합니다.

ASP.NET 역할 정의 및 사용자 계정에 연결 하는 역할 프레임 워크를 제공 합니다. 역할 프레임 워크를 만들고 역할을 삭제할 수 있습니다를 사용 하 여 역할에서 사용자를 제거 하거나, 특정 역할에 속해야 하 고 사용자는 특정 역할에 속하는지 여부를 사용자의 집합을 결정 하는 사용자를 추가 합니다. 역할 프레임 워크를 구성한 후에서는 URL 권한 부여 규칙을 통해 역할-역할별 별로 페이지에 대 한 액세스를 제한 하 고 숨길 수도 추가 정보나 현재 로그온된 한 사용자의 역할을 기반으로 페이지에는 기능입니다.

이 자습서에서는 역할 프레임 워크를 구성 하는 데 필요한 단계를 검토 합니다. 그런 다음, 웹 페이지를 만들고 역할을 삭제 하려면 빌드합니다. 에 <a id="_msoanchor_2"> </a> [ *사용자에 게 역할 할당* ](assigning-roles-to-users-vb.md) 자습서에 추가 하 고 역할에서 사용자를 제거 하는 방법을 살펴보겠습니다. 및에 <a id="_msoanchor_3"> </a> [ *역할 기반 권한 부여* ](role-based-authorization-vb.md) 자습서 페이지 기능에 따라 조정 하는 방법 함께 역할-역할별 기준 페이지에 대 한 액세스를 제한 하는 방법을 살펴보겠습니다 방문한 사용자의 역할입니다. 이제 시작 하겠습니다.

## <a name="step-1-adding-new-aspnet-pages"></a>1 단계: 새 ASP.NET 페이지 추가

이 자습서에는 다음 두 우리는 검색할 수 다양 한 역할 기반 기능 및 기능입니다. 일련의 항목에서는이 자습서 전체에서 검사를 구현 하려면 ASP.NET 페이지를 해야 합니다. 이러한 페이지를 만들고 사이트 맵을 업데이트 해 보겠습니다.

이라는 프로젝트에 새 폴더를 만들어 시작 `Roles`합니다. 다음으로, 네 가지 새로운 ASP.NET 페이지를 추가 합니다 `Roles` 폴더에 있는 각 페이지에 연결는 `Site.master` 마스터 페이지입니다. 페이지 이름을 지정 합니다.

- `ManageRoles.aspx`
- `UsersAndRoles.aspx`
- `CreateUserWizardWithRoles.aspx`
- `RoleBasedAuthorization.aspx`

이 시점에서 프로젝트의 솔루션 탐색기 스크린 샷을 그림 1에 표시 된 것을 유사 합니다.


[![역할 폴더에 추가 된 4 개의 새 페이지](creating-and-managing-roles-vb/_static/image2.png)](creating-and-managing-roles-vb/_static/image1.png)

**그림 1**: 4 개의 새 페이지에 추가한 합니다 `Roles` 폴더 ([클릭 하 여 큰 이미지 보기](creating-and-managing-roles-vb/_static/image3.png))


각 페이지에서이 시점에서 있어야 마스터 페이지의 ContentPlaceHolders 마다 하나씩 두 콘텐츠 컨트롤: `MainContent` 고 `LoginContent`입니다.

[!code-aspx[Main](creating-and-managing-roles-vb/samples/sample1.aspx)]

이전에 설명한 대로 `LoginContent` ContentPlaceHolder의 기본 태그는 로그온 하거나 로그 오프 사용자가 인증 되는지 여부에 따라 사이트에 대 한 링크를 표시 합니다. 그러나 현재 상태는 `Content2` 콘텐츠 ASP.NET 페이지에서 컨트롤에 마스터 페이지의 기본 태그 보다 우선 합니다. 설명한 대로 <a id="_msoanchor_4"> </a> [ *는 폼 인증 개요* ](../introduction/an-overview-of-forms-authentication-vb.md) 자습서에서는 기본 태그를 재정의 합니다. 여기서 하지 표시할 로그인 관련 페이지에 유용 왼쪽된 열에 대 한 옵션입니다.

그러나 이러한 네 가지 페이지에 대 한 표시 하려고에 대 한 마스터 페이지의 기본 태그는 `LoginContent` ContentPlaceHolder 합니다. 따라서 선언적 태그를 제거 합니다 `Content2` 콘텐츠 컨트롤입니다. 이렇게 한 다음, 4 페이지의 태그의 각 콘텐츠 컨트롤을 한 개만 있어야 합니다.

마지막으로, 사이트 맵 업데이트 해 보겠습니다 (`Web.sitemap`) 이러한 새 웹 페이지를 포함 합니다. 후 다음 XML을 추가 합니다 `<siteMapNode>` 멤버 자격 자습서에 대 한 추가 했습니다.

[!code-xml[Main](creating-and-managing-roles-vb/samples/sample2.xml)]

사이트 맵을 업데이트를 사용 하 여 브라우저를 통해 사이트를 방문 합니다. 그림 2에서 볼 수 있듯이 이제 왼쪽 탐색 역할 자습서에 대 한 항목이 포함 됩니다.


[![역할 폴더에 추가 된 4 개의 새 페이지](creating-and-managing-roles-vb/_static/image5.png)](creating-and-managing-roles-vb/_static/image4.png)

**그림 2**: 4 개의 새 페이지에 추가한 합니다 `Roles` 폴더 ([클릭 하 여 큰 이미지 보기](creating-and-managing-roles-vb/_static/image6.png))


## <a name="step-2-specifying-and-configuring-the-roles-framework-provider"></a>지정 하 고 역할 Framework 공급자를 구성 하는 2 단계:

멤버 자격 프레임 워크와 같은 역할 프레임 워크는 공급자 모델 작성 됩니다. 에 설명 된 대로 합니다 <a id="_msoanchor_5"> </a> [ *보안 기본 사항 및 ASP.NET 지원* ](../introduction/security-basics-and-asp-net-support-vb.md) 자습서에서는 세 가지 기본 제공 역할 공급자와 함께 제공 되는.NET Framework: [ `AuthorizationStoreRoleProvider` ](https://msdn.microsoft.com/library/system.web.security.authorizationstoreroleprovider.aspx) 하십시오 [ `WindowsTokenRoleProvider` ](https://msdn.microsoft.com/library/system.web.security.windowstokenroleprovider.aspx), 및 [ `SqlRoleProvider` ](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx)합니다. 이 자습서 시리즈에 중점을 두고는 `SqlRoleProvider`, Microsoft SQL Server 데이터베이스 역할 저장소로 사용 하는.

내부적 역할 프레임 워크 및 `SqlRoleProvider` 멤버 자격 프레임 워크와 마찬가지로 작동 및 `SqlMembershipProvider`합니다. .NET Framework에 포함 된 `Roles` 역할 프레임 워크 API로 사용 되는 클래스입니다. 합니다 `Roles` 클래스와 같은 메서드를 공유 했습니다 `CreateRole`를 `DeleteRole`, `GetAllRoles`를 `AddUserToRole`, `IsUserInRole`등. 다음이 방법 중 하나를 호출 하면는 `Roles` 클래스 구성된 된 공급자에 대 한 호출을 위임 합니다. `SqlRoleProvider` 역할별 테이블을 사용 하 여 작동 (`aspnet_Roles` 고 `aspnet_UsersInRoles`)에 대 한 응답입니다.

사용 하기 위해는 `SqlRoleProvider` 응용 프로그램에서 공급자를 지정 해야 저장소로 사용 하려면 데이터베이스 항목입니다. `SqlRoleProvider` 특정 데이터베이스 테이블, 뷰 및 저장된 프로시저에 지정 된 역할 저장소 필요 합니다. 사용 하 여 이러한 필수 데이터베이스 개체를 추가할 수는 [ `aspnet_regsql.exe` 도구](https://msdn.microsoft.com/library/ms229862.aspx)합니다. 이 시점에서 이미에 필요한 스키마를 사용 하 여 데이터베이스를 `SqlRoleProvider`입니다. 다시 합니다 <a id="_msoanchor_6"> </a> [ *SQL Server에서 멤버 자격 스키마 만들기* ](../membership/creating-the-membership-schema-in-sql-server-vb.md) 자습서 라는 데이터베이스를 만들었습니다 `SecurityTutorials.mdf` 사용 하 고 `aspnet_regsql.exe` 응용 프로그램 추가 필요한 데이터베이스 개체를 포함 하는 서비스는 `SqlRoleProvider`합니다. 따라서 하기만 역할 지원을 사용 하도록 설정 하는 데 사용 하 여 역할 프레임 워크에 알립니다 합니다 `SqlRoleProvider` 사용 하 여는 `SecurityTutorials.mdf` 데이터베이스 역할 저장소로.

역할 프레임 워크를 통해 구성 되는 `<roleManager>` 응용 프로그램의 요소 `Web.config` 파일. 기본적으로 역할 disabled 지원입니다. 를 사용 하도록 설정 해야 합니다 [ `<roleManager>` ](https://msdn.microsoft.com/library/ms164660.aspx) 요소의 `enabled` 특성을 `true` 같이:

[!code-xml[Main](creating-and-managing-roles-vb/samples/sample3.xml)]

기본적으로 모든 웹 응용 프로그램에 명명 된 역할 공급자 `AspNetSqlRoleProvider` 형식의 `SqlRoleProvider`합니다. 이 기본 공급자에 등록 되어 `machine.config` (위치한 `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG`):

[!code-xml[Main](creating-and-managing-roles-vb/samples/sample4.xml)]

공급자의 `connectionStringName` 특성에 사용 되는 역할 저장소를 지정 합니다. `AspNetSqlRoleProvider` 이 특성을 설정 하는 공급자 `LocalSqlServer`에 정의 되어 있는 `machine.config` 지점과, 기본적으로 SQL Server 2005 Express Edition 데이터베이스에 `App_Data` 라는 폴더 `aspnet.mdf`합니다.

따라서 응용 프로그램의 모든 공급자 정보를 지정 하지 않고 단순히 역할 프레임 워크를 사용 하는 경우 `Web.config` 파일을 응용 프로그램에 등록 하는 기본 역할 공급자를 사용 하 여 `AspNetSqlRoleProvider`입니다. 경우는 `~/App_Data/aspnet.mdf` 데이터베이스가 존재 하지 않습니다, ASP.NET 런타임에서 자동으로 만들고 응용 프로그램 서비스 스키마를 추가 합니다. 그러나 사용 하려고 하지 않습니다 합니다 `aspnet.mdf` 사용 하고자 하는 대신 하므로 데이터베이스를 `SecurityTutorials.mdf` 이미 생성 하 고 응용 프로그램 서비스 스키마를 추가 하는 데이터베이스입니다. 이 수정이 두 가지 방법 중 하나로 수행할 수 있습니다.

- <strong>값을 지정 합니다</strong><strong>`LocalSqlServer`</strong><strong>연결 문자열 이름이</strong><strong>`Web.config`</strong><strong>합니다.</strong> 덮어쓰는 방법으로 `LocalSqlServer` 의 연결 문자열 이름 값 `Web.config`를 등록 하는 기본 역할 공급자를 사용할 수 있습니다 (`AspNetSqlRoleProvider`) 있고 올바르게 작동 합니다 `SecurityTutorials.mdf` 데이터베이스. 이 기술에 대 한 자세한 내용은 참조 하세요. [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 블로그 게시물 [사용 하 여 SQL Server 2000 또는 SQL Server 2005로 ASP.NET 2.0 응용 프로그램 서비스 구성](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)합니다.
- <strong>형식의 새 등록 된 공급자를 추가</strong><strong>`SqlRoleProvider`</strong><strong>구성 하 고 해당</strong><strong>`connectionStringName`</strong><strong>를가리키도록설정</strong> <strong>`SecurityTutorials.mdf`</strong> <strong>데이터베이스입니다.</strong> 이 방식은 좋으며에 사용 되는 합니다 <a id="_msoanchor_7"> </a> [ *SQL Server에서 멤버 자격 스키마 만들기* ](../membership/creating-the-membership-schema-in-sql-server-vb.md) 자습서와이 방식은이 자습서에서 사용 됩니다.

다음 역할 구성 태그를 추가 합니다 `Web.config` 파일입니다. 이 태그 라는 새 공급자를 등록 합니다. `SecurityTutorialsSqlRoleProvider.`

[!code-xml[Main](creating-and-managing-roles-vb/samples/sample5.xml)]

위의 태그 정의 `SecurityTutorialsSqlRoleProvider` 기본 공급자로 (통해 합니다 `defaultProvider` 특성을 `<roleManager>` 요소). 또한 설정 합니다 `SecurityTutorialsSqlRoleProvider`의 `applicationName` 설정을 `SecurityTutorials`, 같습니다 `applicationName` 멤버 자격 공급자에서 사용 되는 설정 (`SecurityTutorialsSqlMembershipProvider`). 여기에 표시 되지 않습니다는 [ `<add>` 요소](https://msdn.microsoft.com/library/ms164662.aspx) 에 대 한 합니다 `SqlRoleProvider` 포함 될 수도 있습니다는 `commandTimeout` 데이터베이스 시간 제한 기간 (초)에서 지정 하는 특성입니다. 기본값은 30입니다.

현재 위치에서이 구성 태그에서는 응용 프로그램 내에서 역할 기능을 사용 하 여 시작할 준비가 된 것입니다.

> [!NOTE]
> 위의 구성 태그를 사용 하 여 설명 합니다 `<roleManager>` 요소의 `enabled` 및 `defaultProvider` 특성. 역할 프레임 워크에서 사용자가 사용자 단위로 역할 정보를 연결 하는 방식에 영향을 주는 다른 특성의 여러 가지가 있습니다. 이러한 설정을 검토 합니다는 <a id="_msoanchor_8"> </a> [ *역할 기반 권한 부여* ](role-based-authorization-vb.md) 자습서입니다.


## <a name="step-3-examining-the-roles-api"></a>3 단계: 역할 API 검사

역할 프레임 워크의 기능을 통해 노출 되는 [ `Roles` 클래스](https://msdn.microsoft.com/library/system.web.security.roles.aspx), 역할 기반 작업을 수행 하는 것에 대 한 13 공유 메서드를 포함 하는 합니다. 만들기 및 삭제 4 단계에서에서 역할에 살펴봅니다 시점과 6을 사용 합니다 [ `CreateRole` ](https://msdn.microsoft.com/library/system.web.security.roles.createrole.aspx) 및 [ `DeleteRole` ](https://msdn.microsoft.com/library/system.web.security.roles.deleterole.aspx) 메서드를 추가 하거나 시스템에서 역할을 제거 합니다.

시스템에서 모든 역할의 목록을 가져오려면 합니다 [ `GetAllRoles` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.getallroles.aspx) (5 단계 참조). 합니다 [ `RoleExists` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.roleexists.aspx) 지정된 된 역할에 있는지 여부를 나타내는 부울 값을 반환 합니다.

다음 자습서에서 역할을 사용 하 여 사용자를 연결 하는 방법을 살펴보겠습니다. `Roles` 클래스의 [ `AddUserToRole` ](https://msdn.microsoft.com/library/system.web.security.roles.addusertorole.aspx), [ `AddUserToRoles` ](https://msdn.microsoft.com/library/system.web.security.roles.addusertoroles.aspx)하십시오 [ `AddUsersToRole` ](https://msdn.microsoft.com/library/system.web.security.roles.adduserstorole.aspx), 및 [ `AddUsersToRoles` ](https://msdn.microsoft.com/library/system.web.security.roles.adduserstoroles.aspx) 메서드는 하나 이상의 역할에 하나 이상의 사용자를 추가합니다. 역할에서 사용자를 제거 하려면 사용 합니다 [ `RemoveUserFromRole` ](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromrole.aspx)를 [ `RemoveUserFromRoles` ](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromroles.aspx)를 [ `RemoveUsersFromRole` ](https://msdn.microsoft.com/library/system.web.security.roles.removeusersfromrole.aspx), 또는 [ `RemoveUsersFromRoles` ](https://msdn.microsoft.com/library/system.web.security.roles.removeusersfromroles.aspx) 메서드입니다.

에 <a id="_msoanchor_9"> </a> [ *역할 기반 권한 부여* ](role-based-authorization-vb.md) 자습서 프로그래밍 방식으로 표시 또는 숨기기 기능에서 현재 로그인된 한 사용자의 역할을 기반으로 하는 방법을 살펴보겠습니다. 이렇게 하려면 역할 클래스의 사용할 수 있습니다 [ `FindUsersInRole` ](https://msdn.microsoft.com/library/system.web.security.roles.findusersinrole.aspx)합니다 [ `GetRolesForUser` ](https://msdn.microsoft.com/library/system.web.security.roles.getrolesforuser.aspx)를 [ `GetUsersInRole` ](https://msdn.microsoft.com/library/system.web.security.roles.getusersinrole.aspx), 또는 [ `IsUserInRole` ](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx) 메서드.

> [!NOTE]
> 염두에 언제 든 지 이러한 메서드 중 하나를 호출 하 여 `Roles` 구성된 된 공급자에 대 한 호출을 위임 하는 클래스입니다. 호출에 보내지는 즉 여기서에서는 `SqlRoleProvider`합니다. `SqlRoleProvider` 다음 호출된 방법에 따라 적절 한 데이터베이스 작업을 수행 합니다. 예를 들어, 코드 `Roles.CreateRole("Administrators")` 결과 `SqlRoleProvider` 실행 합니다 `aspnet_Roles_CreateRole` 저장 프로시저에 새 레코드를 삽입 하는 `aspnet_Roles` 관리자 라는 테이블.


이 자습서의 나머지 부분을 사용 하 여 살펴봅니다 합니다 `Roles` 클래스의 `CreateRole`를 `GetAllRoles`, 및 `DeleteRole` 시스템에서 역할을 관리 하는 방법입니다.

## <a name="step-4-creating-new-roles"></a>4 단계: 새 역할 만들기

역할에 임의의 사용자를 그룹화 하는 방법을 제공 하 고 권한 부여 규칙을 적용 하는 보다 편리한 방법에 대 한이 그룹화는 가장 일반적으로 키를 누릅니다. 하지만 권한 부여 메커니즘으로 역할을 사용 하려면 먼저 정의 해야 역할 응용 프로그램에 존재 합니다. 아쉽게도 ASP.NET CreateRoleWizard 컨트롤을 포함 하지 않습니다. 새 역할을 추가 하기 위해 적합 한 사용자 인터페이스를 만들고 역할 API를 직접 호출 해야 합니다. 좋은 소식은이 쉽게 수행 하는 것입니다.

> [!NOTE]
> CreateRoleWizard 웹 컨트롤이 상태인 방법이 합니다 [ASP.NET 웹 사이트 관리 도구](https://msdn.microsoft.com/library/ms228053.aspx), 로컬 ASP.NET 응용 프로그램 보기 및 웹 응용 프로그램의 구성 관리를 사용 하 여 지원 하기 위해 설계는 합니다. 그러나 두 가지 이유로 ASP.NET 웹 사이트 관리 도구를의 열렬 한 팬 아닙니다. 먼저 약간 버그가 있는 것을 사용자 환경 개선의 여지가 많았습니다. 둘째, ASP.NET 웹 사이트 관리 도구는 라이브 사이트에 있는 역할을 원격으로 관리 하는 경우 사용자 고유의 역할 관리 웹 페이지를 구축 해야 하므로 로컬에서 작동 하도록 설계 되었습니다. 이러한 두 가지 이유로이 자습서와 다음 중점적으로 ASP.NET 웹 사이트 관리 도구에 의존 하는 것이 아니라 관리 도구는 웹 페이지에 필요한 역할을 작성 합니다.


엽니다는 `ManageRoles.aspx` 페이지에서 `Roles` 폴더 페이지로 TextBox와 Button 웹 컨트롤을 추가 하 고 합니다. TextBox 컨트롤의 설정 `ID` 속성을 `RoleName` 및 단추의 `ID` 하 고 `Text` 속성을 `CreateRoleButton` 및 Create Role, 각각. 이 시점에서 페이지의 선언적 태그는 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](creating-and-managing-roles-vb/samples/sample6.aspx)]

를 두 번 클릭 합니다 `CreateRoleButton` 만드는 디자이너의 컨트롤 단추는 `Click` 이벤트 처리기 다음 코드를 추가 하 고:

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample7.vb)]

입력 잘린된 역할 이름을 지정 하 여 시작 하는 위의 코드는 `RoleName` 텍스트 상자에는 `newRoleName` 변수입니다. 다음으로 `Roles` 클래스의 `RoleExists` 메서드를 호출 하는 경우를 결정 하 역할 `newRoleName` 시스템에 이미 있습니다. 역할이 없는 경우에 대 한 호출을 통해 생성 됩니다는 `CreateRole` 메서드. 경우는 `CreateRole` 메서드는 시스템에 이미 존재 하는 역할 이름을 전달 되는 `ProviderException` 예외가 throw 됩니다. 이 코드는 먼저 역할 호출 하기 전에 시스템에 아직 존재 하지 않는 되도록 확인 하는 이유는 `CreateRole`합니다. `Click` out 선택을 취소 하 여 이벤트 처리기가 종료 합니다 `RoleName` 텍스트 상자의 `Text` 속성입니다.

> [!NOTE]
> 어떻게 되는지 궁금할 수 있습니다 사용자에 값을 입력 하지 않으면는 `RoleName` 텍스트 상자에 붙여넣습니다. 값으로 전달 되 면 합니다 `CreateRole` 메서드는 `Nothing` 또는 빈 문자열인 경우 예외가 발생 합니다. 마찬가지로, 역할 이름에는 쉼표가 포함 되어 있으면 예외가 발생 합니다. 결과적으로 페이지는 사용자가 역할을 입력 하 고 모든 쉼표를 포함 하지 않는 확인 유효성 검사 컨트롤을 포함 해야 합니다. I 판독기에 대 한 연습을 그대로 둡니다.


관리자 라고 하는 역할을 만들어 보겠습니다. 방문을 `ManageRoles.aspx` 브라우저를 통해 페이지에서 텍스트 상자에 입력 관리자에서 (그림 3 참조) 역할 만들기 단추를 클릭 하 고 있습니다.


[![관리자 역할 만들기](creating-and-managing-roles-vb/_static/image8.png)](creating-and-managing-roles-vb/_static/image7.png)

**그림 3**: 관리자 역할을 만드는 ([큰 이미지를 보려면 클릭](creating-and-managing-roles-vb/_static/image9.png))


어떻게 되나요? 포스트백이 발생 하지만 방법이 다음 있었던 역할 실제로 시각적 표시가 없습니다 시스템에 추가 합니다. 시각적 피드백을 포함 하려면 5 단계에서에서이 페이지는 업데이트 됩니다. 그러나 지금은 확인할 수 있습니다 역할으로 이동 하 여 만들어졌는지 합니다 `SecurityTutorials.mdf` 데이터베이스에서 데이터를 표시 하는 `aspnet_Roles` 테이블입니다. 그림 4에서 알 수 있듯이는 `aspnet_Roles` 방금 추가 된 관리자 역할에 대 한 레코드를 포함 하는 테이블입니다.


[![테이블 aspnet_Roles 관리자에 대 한 행을 갖습니다.](creating-and-managing-roles-vb/_static/image11.png)](creating-and-managing-roles-vb/_static/image10.png)

**그림 4**: 합니다 `aspnet_Roles` 테이블에는 관리자에 대 한 행이 있습니다 ([클릭 하 여 큰 이미지 보기](creating-and-managing-roles-vb/_static/image12.png))


## <a name="step-5-displaying-the-roles-in-the-system"></a>5 단계: 시스템에서 역할을 표시

보겠습니다 보강을 `ManageRoles.aspx` 시스템의 현재 역할의 목록을 포함 하는 페이지입니다. 이렇게 하려면 페이지에 GridView 컨트롤을 추가 하 고 설정 해당 `ID` 속성을 `RoleList`입니다. 다음으로, 라는 페이지의 코드 숨김 클래스에 메서드를 추가 `DisplayRolesInGrid` 다음 코드를 사용 합니다.

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample8.vb)]

합니다 `Roles` 클래스의 `GetAllRoles` 메서드 모든 역할의 시스템으로 반환 문자열 배열입니다. 이 문자열 배열 GridView에 바인딩됩니다. 역할 목록에 바인딩하려면 GridView 페이지가 처음 로드 될 때를 호출 해야 합니다 `DisplayRolesInGrid` 페이지의 메서드에서 `Page_Load` 이벤트 처리기입니다. 다음 코드 페이지를 처음 방문 하는 경우에 없지만 후속 포스트백이이 메서드를 호출 합니다.

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample9.vb)]

이 코드를 사용 하 여 브라우저를 통해 페이지를 방문 합니다. 그림 5에서 알 수 있듯이, 항목 레이블이 지정 된 단일 열이 있는 표가 표시 됩니다. 표 4 단계에서에서 추가한 관리자 역할에 대 한 행이 포함 됩니다.


[![단일 열에는 역할을 표시 하는 GridView](creating-and-managing-roles-vb/_static/image14.png)](creating-and-managing-roles-vb/_static/image13.png)

**그림 5**: 단일 열에는 역할을 표시 하는 GridView ([큰 이미지를 보려면 클릭](creating-and-managing-roles-vb/_static/image15.png))


GridView 때문에 항목을 레이블이 지정 된 유일한 열이 표시 됩니다는 GridView `AutoGenerateColumns` 속성의 각 속성에 대 한 열을 자동으로 만들려면 GridView는 True (기본값)로 설정 되어 해당 `DataSource`합니다. 배열에는 GridView의 단일 열 따라서 배열의 요소를 나타내는 단일 속성이 있습니다.

GridView 사용 하 여 데이터를 표시할 때 명시적으로 내 열을 정의 하지 않고 GridView에서 암시적으로 생성 하도록 않겠습니다. 데이터 서식 지정 쉽게 열에 명시적으로 정의 하 여 열을 다시 정렬 하 고 다른 일반적인 작업을 수행 합니다. 따라서 업데이트 해 보겠습니다 GridView의 선언적 태그는 해당 열은 명시적으로 정의 됩니다.

GridView의을 설정 하 여 시작 `AutoGenerateColumns` 속성을 false로 합니다. 다음으로 집합을 그리드로 templatefield로 추가 해당 `HeaderText` 속성 역할을 구성 하 고 해당 `ItemTemplate` 배열의 내용을 표시 합니다. 이를 위해 라는 레이블을 웹 컨트롤을 추가 `RoleNameLabel` 에 `ItemTemplate` 바인딩하고 해당 `Text` 속성 `Container.DataItem.`

이러한 속성 및 `ItemTemplate`의 내용을 통해 선언적으로 또는 GridView의 필드 대화 상자 및 템플릿 편집 인터페이스 설정할 수 있습니다. 필드 대화 상자에 도달 하려면 GridView의 스마트 태그에 있는 열 편집 링크를 클릭 합니다. 다음으로 설정 하는 자동 생성 필드 확인란의 선택을 취소 합니다 `AutoGenerateColumns` 속성을 False로 설정 GridView를 templatefield로 추가 하 고 해당 `HeaderText` 속성 역할을 합니다. 정의 하는 `ItemTemplate`의 콘텐츠를 GridView의 스마트 태그에서 템플릿 편집 옵션을 선택 합니다. Label 웹 컨트롤을 끌어 합니다 `ItemTemplate`설정, 해당 `ID` 속성을 `RoleNameLabel`, 데이터 바인딩 설정을 구성 하 고 있도록 해당 `Text` 속성이 바인딩되 `Container.DataItem`합니다.

완료 되 면 어떤 접근 방식을 사용에 관계 없이 다음 GridView의 결과 선언적 태그는 유사 합니다.

[!code-aspx[Main](creating-and-managing-roles-vb/samples/sample10.aspx)]

> [!NOTE]
> 데이터 바인딩 구문을 사용 하 여 배열의 내용을 표시 `<%# Container.DataItem %>`합니다. 세부적 설명은 이유이 구문을 사용 하 여 GridView에 바인딩됩니다 배열의 내용을 표시 하는 경우이 자습서의 범위를 벗어납니다. 이 문제에 대 한 자세한 내용은 참조 [스칼라 배열 데이터 웹 컨트롤에 바인딩](http://aspnet.4guysfromrolla.com/articles/082504-1.aspx)합니다.


현재는 `RoleList` GridView 역할 목록에 바인딩된만 해당 페이지를 처음으로 방문 하는 경우. 새 역할 추가 될 때마다 그리드를 새로 고침 해야 합니다. 이를 위해 업데이트를 `CreateRoleButton` 단추의 `Click` 호출 하도록 이벤트 처리기는 `DisplayRolesInGrid` 새 역할이 생성 될 경우 메서드.

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample11.vb)]

사용자는 새 역할을 추가 하는 경우 이제는 `RoleList` 역할이 성공적으로 만들어졌는지 시각적 피드백을 제공 GridView 포스트백에서 방금 추가 된 역할을 보여 줍니다. 예를 들어 참조는 `ManageRoles.aspx` 브라우저를 통해 페이지 및 감독자 라는 역할을 추가 합니다. 역할 만들기 단추를 클릭 하면 포스트백 계속 될 것 이라고 및 그리드 관리자 뿐만 아니라 감독자 새 역할을 포함 하도록 업데이트 됩니다.


[![감독자 역할에 추가 되었습니다.](creating-and-managing-roles-vb/_static/image17.png)](creating-and-managing-roles-vb/_static/image16.png)

**그림 6**: 감독자 역할에 추가 되었습니다 ([큰 이미지를 보려면 클릭](creating-and-managing-roles-vb/_static/image18.png))


## <a name="step-6-deleting-roles"></a>6 단계: 역할 삭제

이 시점에서 사용자 새 역할을 만들고 볼 수 있음에서 모든 기존 역할을 `ManageRoles.aspx` 페이지입니다. 또한 역할을 삭제 하는 사용자를 허용 해 보겠습니다. `Roles.DeleteRole` 메서드에 두 개의 오버 로드가 있습니다.

- [`DeleteRole(roleName)`](https://msdn.microsoft.com/library/ek4sywc0.aspx) -역할을 삭제 *roleName*합니다. 역할 하나 이상의 멤버를 포함 하는 경우 예외가 throw 됩니다.
- [`DeleteRole(roleName, throwOnPopulatedRole)`](https://msdn.microsoft.com/library/38h6wf59.aspx) -역할을 삭제 *roleName*합니다. 하는 경우 *throwOnPopulateRole* 는 `True`, 다음 역할 하나 이상의 멤버를 포함 하는 경우 예외가 throw 됩니다. 하는 경우 *throwOnPopulateRole* 는 `False`, 역할 또는 멤버를 포함 하는지 여부를 삭제 됩니다. 내부적으로 `DeleteRole(roleName)` 메서드 호출 `DeleteRole(roleName, True)`합니다.

`DeleteRole` 메서드는 경우에 예외를 throw *roleName* 됩니다 `Nothing` 이거나 빈 문자열 이거나 *roleName* 쉼표를 포함 합니다. 하는 경우 *roleName* 시스템에 존재 하지 않는 `DeleteRole` 예외가 발생 하지 않고 자동으로 실패 합니다.

GridView에 보강 해 보겠습니다 `ManageRoles.aspx` 포함 하려면 삭제 단추를 클릭 하면 선택한 역할을 삭제 합니다. 필드 대화 상자로 이동 하 고 CommandField 옵션 아래에 있는 삭제 단추를 추가 하 여 GridView에 삭제 단추를 추가 하 여 시작 합니다. 맨 왼쪽된 열 단추 설정 및 삭제를 확인 합니다. 해당 `DeleteText` 속성 삭제 역할을 합니다.


[![RoleList GridView에 삭제 단추를 추가 합니다.](creating-and-managing-roles-vb/_static/image20.png)](creating-and-managing-roles-vb/_static/image19.png)

**그림 7**: 삭제 단추를 추가 합니다 `RoleList` GridView ([클릭 하 여 큰 이미지 보기](creating-and-managing-roles-vb/_static/image21.png))


삭제 단추를 추가한 후 GridView의 선언적 태그는 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](creating-and-managing-roles-vb/samples/sample12.aspx)]

다음으로 GridView의에 대 한 이벤트 처리기를 만들고 `RowDeleting` 이벤트입니다. 역할 삭제 단추를 클릭 하면 포스트백에서 발생 하는 이벤트입니다. 다음 코드를 이벤트 처리기에 추가합니다.

[!code-vb[Main](creating-and-managing-roles-vb/samples/sample13.vb)]

프로그래밍 방식으로 참조 하 여 시작 하는 코드는 `RoleNameLabel` 웹 컨트롤에서 해당 역할 삭제 단추를 클릭 한 행입니다. `Roles.DeleteRole` 메서드는 호출에 전달 합니다 `Text` 의 `RoleNameLabel` 및 `False`시켜 여부에 관계 없이 역할을 삭제 역할과 연결 된 사용자가 있는. 마지막으로 `RoleList` GridView만 삭제 된 역할은 더 이상 눈금에 표시 되도록 새로 고쳐집니다.

> [!NOTE]
> 역할 삭제 단추는 모든 종류의 사용자 로부터 역할을 삭제 하기 전에 확인 필요 하지 않습니다. 작업을 확인 하는 가장 쉬운 방법 중 하나는 클라이언트 쪽 확인 대화 상자를 통해입니다. 이 기술에 대 한 자세한 내용은 참조 하세요. [삭제 하는 경우 클라이언트 쪽 확인 추가](https://asp.net/learn/data-access/tutorial-42-vb.aspx)합니다.


## <a name="summary"></a>요약

많은 웹 응용 프로그램에는 특정 권한 부여 규칙 또는 사용자의 특정 클래스에 제공 되는 페이지 수준 기능이 있습니다. 예를 들어, 관리자만 액세스할 수 있는 웹 페이지 집합이 있을 수 있습니다. 사용자가 사용자 단위로 이러한 권한 부여 규칙을 정의 대신 경우가 많습니다 것이 더 유용 역할에 따라 규칙을 정의할 수 있습니다. 즉, Scott 및 Jisun 관리 웹 페이지에 액세스 하려면 사용자를 명시적으로 허용 하는 대신를 더 쉽게 유지 관리할 방법은 이러한 페이지에 액세스 하려면 관리자 역할의 멤버를 허용 및 Scott 및 Jisun에 속하는 사용자로 표시 하는 관리자 역할입니다.

역할 프레임 워크를 손쉽게 역할 만들기 및 관리 합니다. 이 자습서에서 사용 하기 위해 역할 프레임 워크를 구성 하는 방법을 살펴보았습니다는 `SqlRoleProvider`, Microsoft SQL Server 데이터베이스 역할 저장소로 사용 하는 합니다. 에서는 시스템에서 기존 역할을 나열 하 고 만들 새 역할에 대 한 허용 하는 웹 페이지 및 삭제할 기존도 만들었습니다. 후속 자습서에서는 사용자 역할에 할당 하는 방법 및 역할 기반 권한 부여를 적용 하는 방법을 살펴보겠습니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 2.0의 검사 멤버 자격, 역할 및 프로필](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [방법: ASP.NET 2.0에서에서 역할 관리자를 사용 합니다.](https://msdn.microsoft.com/library/ms998314.aspx)
- [역할 공급자](https://msdn.microsoft.com/library/aa478950.aspx)
- [고유한 웹 사이트 관리 도구를 롤링합니다.](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [에 대 한 기술 설명서는 `<roleManager>` 요소](https://msdn.microsoft.com/library/ms164660.aspx)
- [멤버 자격 및 역할 관리자 Api를 사용 하 여](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/membership.aspx)

### <a name="about-the-author"></a>저자 소개

Scott Mitchell, 여러 ASP/ASP.NET 책의 저자 이자 4GuysFromRolla.com의 설립자 이며 1998 Microsoft 웹 기술을 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는  *[Sams 설명 직접 ASP.NET 2.0 24 시간 동안의](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 합니다. Scott에 도달할 수 있습니다 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 통하거나 저자의 블로그 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Alicja Maziarz, Suchi Banerjee 및 Teresa Murphy 포함 됩니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](role-based-authorization-cs.md)
> [다음](assigning-roles-to-users-vb.md)
