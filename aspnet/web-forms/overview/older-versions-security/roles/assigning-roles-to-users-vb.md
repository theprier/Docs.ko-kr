---
uid: web-forms/overview/older-versions-security/roles/assigning-roles-to-users-vb
title: 사용자 (VB)에 역할 할당 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 두 ASP.NET 페이지 관리 역할에 속한 사용자가 지원 하기 위해 작성 합니다. 첫 번째 페이지에는 확인할 수 있는 기능 포함 됩니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/24/2008
ms.topic: article
ms.assetid: fd208ee9-69cc-4467-9783-b4e039bdd1d3
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-security/roles/assigning-roles-to-users-vb
msc.type: authoredcontent
ms.openlocfilehash: 959a73f53d4fdb114f222fe8bc830876b76c9d9e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="assigning-roles-to-users-vb"></a>사용자 (VB)에 역할 할당
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/VB.10.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial10_AssigningRoles_vb.pdf)

> 이 자습서에서는 두 ASP.NET 페이지 관리 역할에 속한 사용자가 지원 하기 위해 작성 합니다. 첫 번째 페이지에 지정된 된 역할에 속한 사용자가 볼 수 기능 포함 됩니다는 특정 사용자가 속한 역할 및 할당 하거나 특정 사용자는 특정 역할에서 제거할 수 있습니다. 두 번째 페이지에서 새로 만든된 사용자가 속한 역할을 지정 하는 단계가 포함 되도록 CreateUserWizard 컨트롤을 추가할 됩니다 했습니다. 관리자가 새 사용자 계정을 만들 수 있는 시나리오에서 유용 합니다.


## <a name="introduction"></a>소개

<a id="_msoanchor_1"> </a> [이전 자습서](creating-and-managing-roles-vb.md) 역할 프레임 워크를 검사 및 `SqlRoleProvider`; 사용 하는 방법에 살펴보았습니다는 `Roles` 클래스를 만들기, 검색 및 역할을 삭제 합니다. 만들고 역할을 삭제할 것 외에 할당 하거나 역할에서 사용자를 제거할 수 있게 되기가 필요 합니다. 안타깝게도, ASP.NET 역할에 속한 사용자가 관리 하기 위한 웹 컨트롤이 함께 제공 되지 않습니다. 대신, 이러한 연결을 관리 하는 고유한 ASP.NET 페이지 만들어야 합니다. 다행 스럽게도 추가 및 상당히 쉽습니다 역할에 사용자를 제거 합니다. `Roles` 클래스는 다양 한 하나 이상의 역할에 하나 이상의 사용자를 추가 하기 위한 메서드를 포함 합니다.

이 자습서에서는 두 ASP.NET 페이지 관리 역할에 속한 사용자가 지원 하기 위해 작성 합니다. 첫 번째 페이지에 지정된 된 역할에 속한 사용자가 볼 수 기능 포함 됩니다는 특정 사용자가 속한 역할 및 할당 하거나 특정 사용자는 특정 역할에서 제거할 수 있습니다. 두 번째 페이지에서 새로 만든된 사용자가 속한 역할을 지정 하는 단계가 포함 되도록 CreateUserWizard 컨트롤을 추가할 됩니다 했습니다. 관리자가 새 사용자 계정을 만들 수 있는 시나리오에서 유용 합니다.

이제 시작 하겠습니다.

## <a name="listing-what-users-belong-to-what-roles"></a>역할에 속한 사용자를 나열 합니다.

이 자습서에 대 한 첫 번째 order of 비즈니스 사용자 역할에 할당할 수 있는 웹 페이지를 만드는 것입니다. 직접 역할에 사용자를 할당 하는 방법을 고려할 म 전에 보겠습니다 먼저 집중 역할에 속하는 사용자가 확인 하는 방법입니다. 이 정보를 표시 하는 방법은 두 가지가: "역할" 또는 "사용자입니다." 에서는 방문자 역할을 선택한 다음 모든 역할 ("" 역할"으로 표시)에 속하는 사용자 표시를 시작 하거나 방문자 사용자를 선택한 다음 해당 사용자 ("사용자별"디스플레이)에 할당 된 역할 표시를 요구할 수 있습니다.

"에서"역할"보기 경우에 유용 방문자를; 특정 역할에 속한 사용자에 게 집합을 알고 싶어 하는 위치 방문자가 특정 사용자의 역할에 알아야 할 때 "사용자별" 보기는 이상적입니다. "에서"역할"및"사용자별"가격 페이지 죠 인터페이스입니다.

"사용자별" 인터페이스를 만드는 것부터 시작 하겠습니다. 이 인터페이스는 드롭 다운 목록 및 확인란 목록으로 구성 됩니다. 드롭 다운 목록이 채워집니다 사용자 집합이 시스템; 확인란은 역할을 열거 합니다. 드롭다운 목록에서 사용자를 선택 하면 사용자가 속한 역할을 확인 합니다. 페이지를 방문 하는 사용자 한 다음 확인 하거나 추가 하거나 해당 하는 역할에서 선택한 사용자를 제거 하려면 확인란의 선택을 취소 합니다.

> [!NOTE]
> 드롭다운 목록에 목록을 사용 하 여 사용자 계정을 하지 응용 프로그램을 웹 사이트에 대해 수백 개의 사용자 계정이 될 수 있는 합니다. 드롭다운 목록 옵션 중 비교적 짧은 목록에서 한 항목을 선택 하도록 사용자를 허용 하도록 설계 되었습니다. 가 다루기 목록 항목 수가 증가 합니다. 잠재적으로 많은 수의 사용자 계정에 있는 웹 사이트를 작성 하는 경우 하 한 대체 사용자 인터페이스를 사용 하는 것이 좋습니다 페이징 가능한 GridView 또는 나열 하는 필터링 가능한 인터페이스 프롬프트 문자를 선택 하는 방문자와 같은 차례로 선택한 문자로 시작 했는데 사용자는 해당 사용자가 보여 줍니다.


## <a name="step-1-building-the-by-user-user-interface"></a>1 단계: "User" 하 여 사용자 인터페이스 작성

열기는 `UsersAndRoles.aspx` 페이지. 페이지의 맨 위에 추가 라는 Label 웹 컨트롤 `ActionStatus` 지울 및 해당 `Text` 속성입니다. 이 레이블을 같은 메시지를 표시, 수행 되는 동작에 피드백을 제공 하는 데 사용할 "사용자 Tito에 추가 된 관리자 역할" 또는 "사용자 Jisun 감독자 역할에서 제거 되었습니다 했습니다." 이러한 수 있도록 레이블의 설정 메시지 눈에 띄는 `CssClass` 속성을 "중요"입니다.

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample1.aspx)]

다음으로 추가 하기 위해 다음과 같은 CSS 클래스 정의 `Styles.css` 스타일 시트:

[!code-css[Main](assigning-roles-to-users-vb/samples/sample2.css)]

이 CSS 정의는 큰, 빨강 글꼴을 사용 하 여 레이블을 표시 하려면 브라우저에 지시 합니다. 그림 1에서는 Visual Studio 디자이너를 통해이 효과 보여 줍니다.


[![대규모의 빨간색 글꼴로 레이블의 CssClass 속성 결과](assigning-roles-to-users-vb/_static/image2.png)](assigning-roles-to-users-vb/_static/image1.png)

**그림 1**: The 레이블의 `CssClass` 대규모, 빨강 글꼴의에서 속성 결과 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image3.png))


다음으로 설정 하는 페이지에 DropDownList를 추가할 해당 `ID` 속성을 `UserList`를 설정 하 고 해당 `AutoPostBack` 속성을 True로 합니다. 시스템의 모든 사용자를 나열 하려면이 DropDownList를 사용 합니다. 이 DropDownList MembershipUser 개체의 컬렉션에 바인딩됩니다. DropDownList MembershipUser 개체의 UserName 속성 표시 (및 목록 항목의 값으로 사용)를 원하는 있기 때문에 설정 된 DropDownList `DataTextField` 및 `DataValueField` 속성을 "UserName"입니다.

DropDownList를 아래에 명명 된 반복기를 추가 `UsersRoleList`합니다. 이 반복기 모든 나열 됩니다 역할의 시스템에 일련의 확인란을 선택 합니다. 반복기의 정의 `ItemTemplate` 선언적에 다음 태그를 사용 하 여:

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample3.aspx)]

`ItemTemplate` 라는 단일 CheckBox 웹 컨트롤을 포함 하는 태그 `RoleCheckBox`합니다. 확인란의 `AutoPostBack` 속성이 True로 설정 되 고 `Text` 속성이 바인딩되 `Container.DataItem`합니다. 이유 구문이 단순히 `Container.DataItem` 때문에 프레임 워크 역할을 문자열 배열로 역할 이름 목록을 반환 하 고 반복기에 바인딩할 수는 것이 문자열 배열입니다. 철저 한 설명은 이유이 구문을 사용 하 여 데이터 웹 컨트롤에 바인딩된 배열의 내용을 표시 하려면이 자습서의 범위를 벗어납니다. 이 문제에 대 한 자세한 내용은 참조 [스칼라 배열 데이터 웹 컨트롤에 바인딩하거나](http://aspnet.4guysfromrolla.com/articles/082504-1.aspx)합니다.

이 시점에서 "사용자별" 인터페이스의 선언적 태그는 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample4.aspx)]

드롭다운 목록에 사용자 계정 집합과 반복기 역할 집합이 바인딩하기 위한 코드를 쓸 준비가 됩니다. 페이지의 코드 숨김 클래스 라는 메서드를 추가 `BindUsersToUserList` 와 `BindRolesList`, 다음 코드를 사용 하 여:

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample5.vb)]

`BindUsersToUserList` 메서드를 통해 시스템에서 모든 사용자 계정을 검색는 [ `Membership.GetAllUsers` 메서드](https://msdn.microsoft.com/library/dy8swhya.aspx)합니다. 반환 합니다.는 [ `MembershipUserCollection` 개체](https://msdn.microsoft.com/library/system.web.security.membershipusercollection.aspx)의 컬렉션인 [ `MembershipUser` 인스턴스](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)합니다. 이 컬렉션에 바인딩된 다음는 `UserList` DropDownList 합니다. `MembershipUser` 컬렉션와 같은 다양 한 속성을 포함 하는 구성을 인스턴스 `UserName`, `Email`, `CreationDate`, 및 `IsOnline`합니다. 값을 표시할 DropDownList 지시 하기 위해는 `UserName` 속성을 확인는 `UserList` DropDownList의 `DataTextField` 및 `DataValueField` 속성이 "UserName"으로 설정 되어 있는지 합니다.

> [!NOTE]
> `Membership.GetAllUsers` 메서드에 두 개의 오버 로드가: 입력된 된 매개 변수를 허용 하 고 모든 사용자가 반환 하 고 다른 하나는 인덱스 페이지 및 페이지 크기에 대 한 정수 값에서 사용 하 고는 사용자의 하위 집합에 지정 된 반환 합니다. 있는 경우 많은 양의 페이징할 수 있는 사용자 인터페이스 요소에 표시 되는 사용자 계정, 두 번째 오버 로드 데 사용할 수에서 사용자가 페이지 보다 효율적으로 모두가 아닌 사용자 계정의 정확한 하위 집합만 반환 하기 때문입니다.


`BindRolesToList` 메서드를 호출 하 여 시작 된 `Roles` 클래스의 [ `GetAllRoles` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.getallroles.aspx), 시스템에서 역할을 포함 하는 문자열 배열을 반환 하는입니다. 이 문자열 배열 반복기에 바인딩됩니다.

마지막으로, 페이지 처음 로드 될 때이 두 메서드를 호출 해야 합니다. 다음 코드를 `Page_Load` 이벤트 처리기에 추가합니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample6.vb)]

이 코드가 잠시; 브라우저를 통해 페이지를 방문 화면 그림 2 비슷해야 합니다. 모든 사용자 계정이 채워집니다 드롭 다운 목록에서 하 고, 아래에, 각 역할 된 확인란으로 표시 합니다. 설정 하는 이유 때문에 `AutoPostBack` 속성 DropDownList 및 확인란의을 True로 선택 된 사용자를 변경 또는 선택 하거나 선택을 취소 하는 역할에서 포스트백이 발생 합니다. 그러나 이러한 작업을 처리 하는 코드를 작성 하려면 아직 때문에 아무 작업도 수행 됩니다. 다음 두 섹션에서 이러한 작업 해결할 합니다.


[![페이지의 사용자 및 역할 표시 됩니다.](assigning-roles-to-users-vb/_static/image5.png)](assigning-roles-to-users-vb/_static/image4.png)

**그림 2**: 사용자 및 역할 페이지 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image6.png))


### <a name="checking-the-roles-the-selected-user-belongs-to"></a>에 선택한 사용자가 속한 역할 확인

페이지가 처음으로 로드 하거나 방문자가 드롭 다운 목록에서 새 사용자를 선택할 때마다 업데이트 해야는 `UsersRoleList`의 확인란을 선택한 사용자가 해당 역할에 속한 경우에 지정된 역할 확인란이 선택 되어 있도록 합니다. 이를 위해 라는 메서드를 만듭니다 `CheckRolesForSelectedUser` 를 다음 코드로:

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample7.vb)]

위의 코드는 선택한 사용자를 확인 하 여 시작 합니다. 역할 클래스의 사용 하 여 다음 [ `GetRolesForUser(userName)` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.getrolesforuser.aspx) 역할을 문자열 배열로 지정된 된 사용자의 집합을 반환 합니다. 반복기의 항목 열거 되는 다음으로, 및 각 항목의 `RoleCheckBox` 확인란을 선택은 프로그래밍 방식으로 참조 합니다. 에 해당 역할에 포함 된 경우에에서 확인란을 선택는 `selectedUsersRoles` 문자열 배열을 반환 합니다.

> [!NOTE]
> `Linq.Enumerable.Contains(Of String)(...)` ASP.NET 버전 2.0 사용 하는 경우 구문 컴파일되지 것입니다. `Contains(Of String)` 메서드는의 일부는 [LINQ 라이브러리](http://en.wikipedia.org/wiki/Language_Integrated_Query), 새로운 ASP.NET 3.5입니다. ASP.NET 버전 2.0 여전히 사용 중인 경우 사용 하 여는 [ `Array.IndexOf(Of String)` 메서드](https://msdn.microsoft.com/library/eha9t187.aspx) 대신 합니다.


`CheckRolesForSelectedUser` 메서드를 두 가지 경우에 호출 해야 합니다.: 페이지가 처음 로드 될 때와 때마다는 `UserList` DropDownList의 선택한 인덱스 변경 됩니다. 따라서에서이 메서드를 호출할는 `Page_Load` 이벤트 처리기 (을 호출한 후 `BindUsersToUserList` 및 `BindRolesToList`). 또한 DropDownList의에 대 한 이벤트 처리기를 만들고 `SelectedIndexChanged` 이벤트 여기에서이 메서드를 호출 합니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample8.vb)]

이 코드 위치에서 브라우저를 통해 페이지를 테스트할 수 있습니다. 그러나 이후에 `UsersAndRoles.aspx` 페이지에는 현재 역할에 사용자를 할당 하는 능력이 없는, 사용자가 역할을 설치 합니다. 이 코드는 작동 하는 내 단어를 사용 하 고 한다는 것 이라면 확인 잠시 후에 사용자 역할에 할당 하기 위한 인터페이스를 만들겠습니다 또는 레코드를 삽입 하 여 역할에 사용자를 수동으로 추가할 수 있습니다는 `aspnet_UsersInRoles` 이 functi 테스트 하기 위해 테이블 이제 onality 합니다.

### <a name="assigning-and-removing-users-from-roles"></a>할당 하 고 역할에서 사용자 제거

방문자를 확인 하거나에서 확인란을 선택 하거나 선택 취소 하면는 `UsersRoleList` 반복기를 추가 하 여 해당 역할에서 선택한 사용자를 제거 해야 합니다. 이 확인란의 `AutoPostBack` 속성이 현재 반복기에서 CheckBox checked 또는 unchecked로 인해 포스트백을 true로 설정 되어 있습니다. 즉, 해당 확인란의 이벤트 처리기를 만들고 해야 `CheckChanged` 이벤트입니다. 반복기 컨트롤에서 확인란은, 원하므로 이벤트 처리기 내부 작업을 수동으로 추가 해야 합니다. 이벤트 처리기로 코드 숨김 클래스를 추가 하 여 시작는 `Protected` 메서드를 다음과 같이:

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample9.vb)]

잠시 후에이 이벤트 처리기에 대 한 코드를 작성할 돌아갑니다. 그러나 우선 보겠습니다 이벤트 배관을 처리를 완료 합니다. 반복기의 내에서 확인란의 선택을 `ItemTemplate`, 추가 `OnCheckedChanged="RoleCheckBox_CheckChanged"`합니다. 이 구문은 연결는 `RoleCheckBox_CheckChanged` 에 이벤트 처리기는 `RoleCheckBox`의 `CheckedChanged` 이벤트입니다.

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample10.aspx)]

우리의 마지막 작업을 완료 하는 `RoleCheckBox_CheckChanged` 이벤트 처리기입니다. 이 확인란을 인스턴스를 알려줍니다. 역할이 checked 또는 unchecked 통해 때문에 이벤트를 발생 시킨 CheckBox 컨트롤을 참조 하 여을 시작 해야 해당 `Text` 및 `Checked` 속성입니다. 선택한 사용자의 사용자 이름와 함께이 정보를 사용 하 여 우리에서 추가 하거나 제거할 사용자를 통해 역할은 `Roles` 클래스의 [ `AddUserToRole` ](https://msdn.microsoft.com/library/system.web.security.roles.addusertorole.aspx) 또는 [ `RemoveUserFromRole` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromrole.aspx)합니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample11.vb)]

위의 코드를 통해 사용할 수 있는 이벤트를 발생 하는 확인란을 프로그래밍 방식으로 참조 하 여 시작 하는 `sender` 입력된 매개 변수입니다. 확인란을 선택 하는 경우 선택한 사용자 지정된 된 역할, 그렇지 않으면 역할에서 제거한에 추가 됩니다. 두 경우 모두는 `ActionStatus` 레이블 방금 수행한 작업을 요약 하는 메시지를 표시 합니다.

이 페이지는 브라우저를 통해 테스트 보십시오. Tito 사용자를 선택한 다음 Tito 관리자와 감독자 역할에 추가 합니다.


[![Tito는 관리자 및 감독자 역할에 추가 되었습니다.](assigning-roles-to-users-vb/_static/image8.png)](assigning-roles-to-users-vb/_static/image7.png)

**그림 3**: Tito 관리자 및 감독자 역할에 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image9.png))


다음으로, 드롭 다운 목록에서 1 세 사용자를 선택 합니다. 포스트백 있고 반복기의 확인란을 통해 업데이트 되는 `CheckRolesForSelectedUser`합니다. 1 세 아직에 속하지 않은 모든 역할을 하므로 두 확인란을 선택 하 여 검사 되지 않습니다. 다음으로 1 세 감독자 역할에 추가 합니다.


[![1 세 감독자 역할에 추가 된](assigning-roles-to-users-vb/_static/image11.png)](assigning-roles-to-users-vb/_static/image10.png)

**그림 4**: 1 세 감독자 역할에 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image12.png))


추가 기능을 확인 하는 `CheckRolesForSelectedUser` 메서드를 Tito 또는 1 세 이외의 사용자를 선택 합니다. 확인란은 자동으로 선택 되지 않은 어떻게 참고를 나타내는 모든 역할에 속해 있지 않습니다. Tito 돌아갑니다. 관리자와 감독자 확인란 선택 되어야 합니다.

## <a name="step-2-building-the-by-roles-user-interface"></a>2 단계: "역할" 하 여 사용자 인터페이스 작성

이 시점에서 "users" 하 여 인터페이스를 완료 하 고 "역할" 하 여 인터페이스를 수행 하는 작업량과 시작할 준비가 합니다. "역할"에 의해 인터페이스 드롭 다운 목록에서 역할을 선택 하 라는 메시지를 표시 하 고는 GridView에 해당 역할에 속한 사용자에 게 집합을 표시 합니다.

다른 DropDownList 컨트롤을 추가 `UsersAndRoles.aspx page`합니다. 반복기 컨트롤 아래에이 하나씩 배치, 이름을 `RoleList`를 설정 하 고 해당 `AutoPostBack` 속성을 True로 합니다. 아래에는 GridView를 추가 하 고 이름을 `RolesUserList`합니다. 이 GridView 선택된 된 역할에 속하는 사용자를 나열 합니다. GridView의 설정 `AutoGenerateColumns` 속성을 false로, 그리드를 TemplateField 추가할 `Columns` 컬렉션 집합과 해당 `HeaderText` 속성을 "Users"입니다. TemplateField의 정의 `ItemTemplate` 데이터 바인딩 식의 값이 표시 되도록 `Container.DataItem` 에 `Text` 이라는 레이블의 속성 `UserNameLabel`합니다.

추가 하 여 GridView를 구성한 후 "역할" 하 여 인터페이스의 선언적 태그 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample12.aspx)]

채울 필요는 `RoleList` DropDownList 시스템에는 역할 집합을 사용 합니다. 이를 위해 업데이트는 `BindRolesToList` 바인딩 즉 메서드 문자열 배열에서 반환 된는 `Roles.GetAllRoles` 메서드를는 `RolesList` DropDownList (으로 `UsersRoleList` 반복기).

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample13.vb)]

마지막 두 줄을는 `BindRolesToList` 역할 집합이 바인딩할 추가 된 메서드는 `RoleList` DropDownList 제어 합니다. 그림 5에서는 시스템의 역할과 채워진 드롭 다운 목록 브라우저를 통해 볼 때 최종 결과를 보여 줍니다.


[![RoleList 드롭다운 목록에는 역할이 표시 됩니다.](assigning-roles-to-users-vb/_static/image14.png)](assigning-roles-to-users-vb/_static/image13.png)

**그림 5**: The 역할에 표시 되는 `RoleList` DropDownList ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image15.png))


### <a name="displaying-the-users-that-belong-to-the-selected-role"></a>선택된 된 역할에 속하는 사용자를 표시 합니다.

페이지가 처음 로드할 때 또는에서 새 역할을 선택 하는 경우는 `RoleList` DropDownList를 GridView에서 해당 역할에 속하는 사용자의 목록을 표시 해야 합니다. 라는 메서드를 만듭니다 `DisplayUsersBelongingToRole` 다음 코드를 사용 하 여:

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample14.vb)]

이 메서드를 통해 선택된 된 역할에서 시작 된 `RoleList` DropDownList 합니다. 다음 사용 하 여는 [ `Roles.GetUsersInRole(roleName)` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.getusersinrole.aspx) 해당 역할에 속하는 사용자의 사용자 이름의 문자열 배열을 검색 합니다. 이 배열에 바인딩된 다음는 `RolesUserList` GridView입니다.

이 메서드를 두 가지 상황에서 호출 해야 합니다.: 페이지가 처음 로드 될 때 선택된 된 역할에는 `RoleList` DropDownList 변경 합니다. 따라서 업데이트는 `Page_Load` 이벤트 처리기를 호출한 후이 메서드는 호출 되도록 `CheckRolesForSelectedUser`합니다. 에 대 한 이벤트 처리기를 다음으로 만듭니다는 `RoleList`의 `SelectedIndexChanged` 이벤트를 너무 여기에서이 메서드를 호출 합니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample15.vb)]

현재 위치에서이 코드는 `RolesUserList` GridView 선택된 된 역할에 속하는 사용자를 표시 해야 합니다. 그림 6에서 볼 수 있듯이 감독자 역할 두 멤버로 구성: 1 세 및 Tito 합니다.


[![선택한 역할에 속하는 사용자를 나열 하는 GridView](assigning-roles-to-users-vb/_static/image17.png)](assigning-roles-to-users-vb/_static/image16.png)

**그림 6**: The GridView 나열 된 사용자에 속함을 선택 된 역할 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image18.png))


### <a name="removing-users-from-the-selected-role"></a>선택된 된 역할에서 사용자 제거

하겠습니다를 확장 하 고 `RolesUserList` GridView의 열이 포함 되도록 "제거" 단추입니다. 특정 사용자에 대 한 "제거" 단추를 클릭 하면 해당 역할에서 제거 됩니다.

GridView에 삭제 단추 필드를 추가 하 여 시작 합니다. 이 필드를 필드 가장 왼쪽으로 나타나고 변경 해당 `DeleteText` 속성이 "Delete" (기본값)에서 "제거"으로 합니다.


[![추가](assigning-roles-to-users-vb/_static/image20.png)](assigning-roles-to-users-vb/_static/image19.png)

**그림 7**: GridView에 "제거" 단추를 추가 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image21.png))


포스트백 계속 "제거" 단추를 클릭할 때 및 GridView의 `RowDeleting` 이벤트가 발생 합니다. 이 이벤트에 대 한 이벤트 처리기를 만들고 선택된 된 역할에서 사용자를 제거 하는 코드를 작성 해야 합니다. 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample16.vb)]

선택한 역할 이름을 확인 하 여 시작 하는 코드입니다. 그런 다음 프로그래밍 방식으로 참조는 `UserNameLabel` 제거할 사용자의 사용자를 확인 하기 위해 해당 "제거" 단추를 클릭 한 행에서 제어 합니다. 사용자가 다음에 대 한 호출을 통해 역할에서 제거 되 고 `Roles.RemoveUserFromRole` 메서드. `RolesUserList` GridView 다음 새로 고쳐지고이 통해 메시지가 표시 됩니다는 `ActionStatus` 레이블 컨트롤입니다.

> [!NOTE]
> "제거" 단추는 모든 종류의 사용자 로부터 역할에서 사용자를 제거 하기 전에 확인 필요 하지 않습니다. 있습니까 초대 일정 수준의 사용자에 게 확인을 추가할 수 있습니다. 작업을 확인 하는 가장 쉬운 방법 중 하나는 클라이언트 쪽 확인 대화 상자입니다. 이 방법에 대 한 자세한 내용은 참조 하십시오. [추가 클라이언트 쪽 확인 때 삭제](https://asp.net/learn/data-access/tutorial-42-vb.aspx)합니다.


그림 8 Tito 사용자 권한이 그룹에서 제거 된 후 페이지를 보여줍니다.


[![안타깝게도 Tito는 더 이상 감독자](assigning-roles-to-users-vb/_static/image23.png)](assigning-roles-to-users-vb/_static/image22.png)

**그림 8**: 안타깝게도 Tito는 더 이상 감독자 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image24.png))


### <a name="adding-new-users-to-the-selected-role"></a>선택된 된 역할에 새 사용자 추가

선택된 된 역할에서 사용자를 제거, 함께이 페이지는 방문자도 할 수 있어야 선택된 된 역할에 사용자를 추가 합니다. 선택된 된 역할에 사용자를 추가 하기 위한 최상의 인터페이스 것으로 예상 되는 사용자 계정 수에 따라 달라 집니다. 웹 사이트를 몇 십 개의 사용자 계정을 저장할이 하 이면 DropDownList를 여기서 사용할 수 있습니다. 수천 개의 사용자 계정이 있을 수 있습니다는 하려는 경우 특정 계정에 대 한 검색 계정을 통해 페이지 또는 사용자 계정에 몇 가지 다른 방식으로 필터링 하도록 방문자를 허용 하는 사용자 인터페이스를 포함 합니다.

이 페이지에 대 한 시스템에서 사용자 계정 수에 관계 없이 작동 하는 매우 간단한 인터페이스를 사용해 보겠습니다. 즉, 선택된 된 역할에 추가 하려고 하는 사용자의 사용자 이름을 입력 하 여 방문자에 게 확인 텍스트 상자를 사용 합니다. 해당 이름의 사용자 없거나에 메시지를 표시 합니다 사용자 역할의 구성원이 이미 있으면 `ActionStatus` 레이블. 하지만 존재는 사용자를 역할의 멤버인 경우에서는 합니다는 역할에 추가 하 고 눈금을 새로 고칩니다.

텍스트 상자 및 단추 GridView 아래에 추가 합니다. 텍스트 상자의 설정 `ID` 를 `UserNameToAddToRole` 단추의 설정 `ID` 및 `Text` 속성을 `AddUserToRoleButton` 및 "사용자 역할에 추가"를 각각.

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample17.aspx)]

다음으로 만듭니다는 `Click` 에 대 한 이벤트 처리기는 `AddUserToRoleButton` 다음 코드를 추가 하 고 있습니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample18.vb)]

대부분의 코드에는 `Click` 이벤트 처리기는 다양 한 유효성 검사를 수행 합니다. 방문자에서 사용자 이름을 제공 됨을 보장 하므로 `UserNameToAddToRole` 이미 선택된 된 역할에 속하지 않은 사용자는 시스템에 존재 하 고 텍스트 상자입니다. 적절 한 메시지에 표시 됩니다는 이러한 점검 작업이 실패 하면, `ActionStatus` 및 이벤트 처리기를 종료 합니다. 사용자가을 통해 역할에 추가 모든 검사를 통과 `Roles.AddUserToRole` 메서드. 그런 다음, 입력란의 `Text` 속성이 선택 취소 되어, GridView을 새로 고칠 및 `ActionStatus` 레이블이 지정된 된 사용자 선택된 된 역할에 성공적으로 추가 된 메시지가 표시 됩니다.

> [!NOTE]
> 사용을 보장 하기 위해 지정 된 사용자가 이미 선택된 된 역할에 속해 있지는 [ `Roles.IsUserInRole(userName, roleName)` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx)를 나타내는 부울 값을 반환 하는 여부를 *userName* 의멤버인*roleName*합니다. 다시이 메서드를 사용 합니다는 <a id="_msoanchor_2"> </a> [다음 자습서](role-based-authorization-vb.md) 역할 기반 권한 부여 때 살펴보겠습니다.


브라우저를 통해 페이지를 방문 하 고 있는 감독자 역할을 선택는 `RoleList` DropDownList 합니다. 잘못 된 사용자 이름을 입력 해 봅니다-사용자가 시스템에 존재 하지 않는지를 설명 하는 메시지가 표시 되어야 합니다.


[![존재 하지 않는 사용자 역할에 추가할 수 없습니다.](assigning-roles-to-users-vb/_static/image26.png)](assigning-roles-to-users-vb/_static/image25.png)

**그림 9**: 존재 하지 않는 사용자 역할에 추가할 수 없습니다 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image27.png))


이제 유효한 사용자를 추가 해 보십시오. 계속 진행 하 고 다시 Tito 감독자 역할에 추가 합니다.


[![Tito는 감독자 다시 한 번!](assigning-roles-to-users-vb/_static/image29.png)](assigning-roles-to-users-vb/_static/image28.png)

**그림 10**: Tito는 감독자 다시!  ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image30.png))


## <a name="step-3-cross-updating-the-by-user-and-by-role-interfaces"></a>3 단계: 간 업데이트는 "사용자별" 및 "역할" 하 여 인터페이스

`UsersAndRoles.aspx` 페이지는 사용자 및 역할을 관리 하기 위한 두 개의 서로 다른 인터페이스를 제공 합니다. 현재 두 인터페이스는 하나의 인터페이스의 변경 내용을 반영 되지 것입니다 즉시 다른 수 있으므로 서로 독립적으로 작동 합니다. 예를 들어 방문자 페이지에 있는 감독자 역할을 선택 한다고 가정해 보세요는 `RoleList` DropDownList 1 세 및 Tito의 구성원으로 나열 합니다. 방문자 Tito에서를 선택 하는 다음으로 `UserList` DropDownList 관리자 및 감독자 확인란에서 검사 하는 `UsersRoleList` 반복기입니다. 방문자 다음 반복기에서 Supervisor 역할을 선택 하거나 선택 취소 하십시오 Tito가 감독자 역할에서 제거 되지만이 수정 "역할별" 인터페이스에 반영 되지 않습니다. GridView는 감독자 역할의 멤버인 것으로 Tito 표시 합니다.

Checked 또는 unchecked에서 역할은 때마다 GridView를 갱신 해야이 문제를 해결 하는 `UsersRoleList` 반복기입니다. 마찬가지로, 사용자를 제거 하거나 "역할" 하 여 인터페이스에서 역할에 추가할 때마다 반복기 새로 고침 해야 합니다.

"사용자별" 인터페이스에 반복기를 호출 하 여 새로 고칠는 `CheckRolesForSelectedUser` 메서드. "역할" 하 여 인터페이스를 수정할 수는 `RolesUserList` GridView의 `RowDeleting` 이벤트 처리기 및 `AddUserToRoleButton` 단추의 `Click` 이벤트 처리기입니다. 따라서 호출 해야는 `CheckRolesForSelectedUser` 이러한 각 방법에서 메서드.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample19.vb)]

호출 하 여 "역할" 하 여 인터페이스에서 GridView 새로 고쳐집니다 마찬가지로,는 `DisplayUsersBelongingToRole` 메서드와 "사용자별" 인터페이스를 통해 수정 되는 `RoleCheckBox_CheckChanged` 이벤트 처리기입니다. 따라서 호출 해야는 `DisplayUsersBelongingToRole` 이벤트 처리기에서 메서드.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample20.vb)]

이러한 코드 변경 내용으로는 이제에 인터페이스 "사용자별" 및 "역할" 하 여 정확 하 게 업데이트 합니다. 이 확인 하려면 브라우저를 통해 페이지를 방문 하 고 Tito 및 감독자에서 선택 된 `UserList` 및 `RoleList` dropdownlist 활용, 각각. "사용자별" 인터페이스에 반복 Tito에 대 한 감독자 역할을 선택 취소 하는 대로 Tito 자동으로 제거 되도록 "역할" 하 여 인터페이스에서 GridView에서 note 합니다. "사용자별" 인터페이스에 감독자 확인란을 확인 다시 Tito 감독자 역할에 다시 "역할" 하 여 인터페이스에서 자동으로 추가 합니다.

## <a name="step-4-customizing-the-createuserwizard-to-include-a-specify-roles-step"></a>4 단계: CreateUserWizard "역할을 지정 합니다." 단계를 포함 하도록 사용자 지정

에 <a id="_msoanchor_3"> </a> [ *사용자 계정 만들기* ](../membership/creating-user-accounts-vb.md) 자습서 CreateUserWizard 웹 컨트롤을 사용 하 여 새 사용자 계정을 만들기 위한 인터페이스를 제공 해야 하는 방법에 살펴보았습니다. 두 가지 방법 중 하나에 CreateUserWizard 컨트롤을 사용할 수 있습니다.

- 사이트에서 자신의 사용자 계정을 만들려면 방문자 위한 수단으로 하 고
- 관리자가 새 계정을 만들 수는 방법으로

첫 번째 사용 사례는 방문자가 사이트에 제공 하 고 사이트에 등록 하기 위해 해당 정보를 입력 하 고 CreateUserWizard 사항을 입력 합니다. 두 번째 경우에는 관리자가 다른 사용자에 대 한 새 계정을 만듭니다.

다른 사람에 대 한 관리자 계정을 만들어질 때에 관리자가 새 사용자 계정이 속한 역할을 지정할 수 있도록 유용할 수 있습니다. 에 <a id="_msoanchor_4"> </a> [ *저장* *추가 사용자 정보* ](../membership/storing-additional-user-information-vb.md) 은 CreateUserWizard 추가 추가 하 여 사용자 지정 하는 방법에 대해 살펴보았습니다 자습서 `WizardSteps`. 새 사용자의 역할을 지정 하기 위해은 CreateUserWizard에 추가 단계를 추가 하는 방법에 살펴보겠습니다.

열기는 `CreateUserWizardWithRoles.aspx` 페이지 라는 CreateUserWizard 컨트롤을 추가 하 고 `RegisterUserWithRoles`합니다. 컨트롤의 `ContinueDestinationPageUrl` 속성을 "~ / Default.aspx"입니다. 여기서는 관리자가이 CreateUserWizard 컨트롤은 데 사용할 새 사용자 계정을 만들 이기 때문에 컨트롤의 설정 `LoginCreatedUser` 속성을 false로 합니다. 이 `LoginCreatedUser` 속성 여부를 지정 하는 방문자가 방금 만든 사용자로 로그온 자동으로 기본값은 True입니다. 에서는 False로 설정에 사용 하기 위해 관리자가 새 계정을 만들 때을 자신으로 로그인 하 게 합니다.

다음으로, 선택는 "추가/제거 `WizardSteps`..." CreateUserWizard의 스마트 태그에서 옵션을 추가할 새 `WizardStep`설정 해당 `ID` 를 `SpecifyRolesStep`합니다. 이동 된 `SpecifyRolesStep WizardStep` "로그인에 새 계정" 단계가 끝나고 "완료" 단계 전에 제공 되도록 합니다. 설정의 `WizardStep`의 `Title` 속성 "역할 지정"을 해당 `StepType` 속성을 `Step`, 및 해당 `AllowReturn` 속성을 false로 합니다.


[![추가](assigning-roles-to-users-vb/_static/image32.png)](assigning-roles-to-users-vb/_static/image31.png)

**그림 11**: 추가 "를 지정 된 역할" `WizardStep` 은 CreateUserWizard를 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image33.png))


이 변경 후 CreateUserWizard의 선언적 태그는 다음과 같이 표시 됩니다.

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample21.aspx)]

"지정 된 역할"의 `WizardStep`, 라는 CheckBoxList 추가 `RoleList.` 이 CheckBoxList은 사용 가능한 역할을 나열에 새로 만든된 사용자가 속한 어떤 역할을 확인 하는 페이지를 방문 하는 사용자를 사용 하도록 설정 합니다.

두 개의 코딩 작업 하: 채워야 먼저는 `RoleList` 시스템;에 있는 역할 CheckBoxList 둘째, "완료" 단계를 "역할 지정" 단계에서 사용자가 선택한 역할에 만든된 사용자를 추가 해야 합니다. 첫 번째 작업을 수행할 수 있습니다는 `Page_Load` 이벤트 처리기입니다. 다음 코드 프로그래밍 방식으로 참조는 `RoleList` 첫 번째 확인란이 선택 페이지를 열 및 역할을 시스템에서 해당 인스턴스에 바인딩됩니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample22.vb)]

위의 코드는 친숙 한 표시 됩니다. 에 <a id="_msoanchor_5"> </a> [ *저장* *추가 사용자 정보* ](../membership/storing-additional-user-information-vb.md) 사용 두 자습서 `FindControl` 웹 컨트롤을 참조 하는 문 사용자 지정 내 `WizardStep`합니다. 및이 자습서의 앞부분에 나오는 역할 CheckBoxList에 바인딩되는 코드에서 가져왔습니다.

두 번째 프로그래밍 작업을 수행 하려면 "역할을 지정" 단계가 완료 된 경우를 파악 해야 합니다. CreateUserWizard에 회수는 `ActiveStepChanged` 방문자가 다른 한 단계에서 이동할 때마다 발생 하는 이벤트입니다. 에서는 여기에 사용자 "완료" 단계;에 도달 하는 경우 확인할 수 있습니다. 이 경우 선택한 역할에 사용자를 추가 해야 합니다.

에 대 한 이벤트 처리기를 만들고는 `ActiveStepChanged` 이벤트를 다음 코드를 추가 합니다.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample23.vb)]

이벤트 처리기의 항목을 열거 하는 경우 사용자가 "완료" 단계에 도달 하면 방금는 `RoleList` CheckBoxList 고 방금 만든 사용자 선택 된 역할에 할당 됩니다.

브라우저를 통해이 페이지를 방문 합니다. 첫 번째 단계는 CreateUserWizard은 새 사용자의 사용자 이름, 암호, 전자 메일 및 기타 주요 정보를 묻는 표준 "로그인에 새 계정" 단계입니다. Wanda 라는 새 사용자를 만드는 데 필요한 정보를 입력 합니다.


[![Wanda 라는 새 사용자 만들기](assigning-roles-to-users-vb/_static/image35.png)](assigning-roles-to-users-vb/_static/image34.png)

**그림 12**: 새 사용자 라는 Wanda 만들기 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image36.png))


"사용자 만들기" 단추를 클릭 합니다. CreateUserWizard 내부적으로 호출 된 `Membership.CreateUser` 새 사용자 계정 및 다음 진행 되 고 다음 단계를 만드는 메서드를 "역할 지정 합니다." 여기에 시스템 역할은 나열 되어 있습니다. 감독자 확인란을 선택 하 고 클릭 합니다.


[![Wanda 감독자 역할의 구성원을으로 만듭니다.](assigning-roles-to-users-vb/_static/image38.png)](assigning-roles-to-users-vb/_static/image37.png)

**그림 13**: Wanda 감독자 역할의 멤버로 설정 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image39.png))


포스트백 및 업데이트 하면 다음을 클릭 하 고 `ActiveStep` "완료" 단계에 있습니다. 에 `ActiveStepChanged` 이벤트 처리기를 최근에 만든 사용자 계정 감독자 역할에 할당 됩니다. 이 확인 하려면 반환는 `UsersAndRoles.aspx` 감독자에서 선택한 페이지는 `RoleList` DropDownList 합니다. 그림 14에서 볼 수 있듯이 감독자는 이제 구성 된 사용자 3 명을: 1 세, Tito, 및 Wanda 합니다.


[![1 세, Tito, 및 Wanda는 모든 권한이](assigning-roles-to-users-vb/_static/image41.png)](assigning-roles-to-users-vb/_static/image40.png)

**그림 14**: 1 세, Tito, 및 Wanda는 모든 권한이 ([전체 크기 이미지를 보려면 클릭](assigning-roles-to-users-vb/_static/image42.png))


## <a name="summary"></a>요약

역할 프레임 워크에서는 특정 사용자의 역할 및 사용자가 지정 된 역할의 구성원을 확인 하기 위한 방법에 대 한 정보를 검색 하는 메서드를 제공 합니다. 또한 하나 이상의 역할에 하나 이상의 사용자 추가 및 제거에 대 한 메서드의 여러 가지가 있습니다. 이 자습서에서는 이러한 메서드 중 두 개만 포함에 집중: `AddUserToRole` 및 `RemoveUserFromRole`합니다. 에 추가 변형이 단일 역할에 여러 사용자를 추가 하 고 단일 사용자에 게 여러 역할을 할당 하도록 설계 되었습니다.

이 자습서에 포함 하도록 CreateUserWizard 컨트롤 확장을 참조도 포함 되어는 `WizardStep` 새로 만든 사용자의 역할을 지정할 수 있습니다. 이러한 단계 관리자가 새 사용자에 대 한 사용자 계정을 만드는 프로세스를 간소화할 수 있습니다.

이 시점에서 살펴본 것를 만들고 역할을 삭제 하는 방법과 추가 하 고 역할에서 사용자를 제거 합니다. 하지만 아직 역할 기반 권한 부여 적용을 살펴봅니다. 에 <a id="_msoanchor_6"> </a> [자습서 다음](role-based-authorization-vb.md) 살펴보도록 하겠습니다 역할-역할별 기준 URL 권한 부여 규칙을 정의 현재 로그인된 한 사용자의 역할에 따라 페이지 수준의 기능을 제한 하는 방법에 있습니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 웹 사이트 관리 도구 개요](https://msdn.microsoft.com/library/ms228053.aspx)
- [ASP를 검사 합니다. NET의 멤버 자격, 역할 및 프로필](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [자신의 웹 사이트 관리 도구를 롤링합니다.](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)

### <a name="about-the-author"></a>작성자 정보

여러 ASP/ASP.NET 책의 작성자 및 4GuysFromRolla.com의 창립자 Scott Mitchell의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은  *[Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*합니다. Scott에 도달할 수 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 또는에서 그의 블로그 통해 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특히 감사 드립니다.

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Teresa 머피의 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](creating-and-managing-roles-vb.md)
> [다음](role-based-authorization-vb.md)
