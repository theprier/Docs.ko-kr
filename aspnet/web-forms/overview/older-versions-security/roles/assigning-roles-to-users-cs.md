---
uid: web-forms/overview/older-versions-security/roles/assigning-roles-to-users-cs
title: 사용자 (C#)에 역할 할당 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 두 ASP.NET 페이지 어떤 역할에 속하는 사용자 관리를 도우려면 빌드합니다. 첫 번째 페이지에는 어떻게 표시 하는 기능이 포함 됩니다...
ms.author: aspnetcontent
ms.date: 03/24/2008
ms.assetid: d522639a-5aca-421e-9a76-d73f95607f57
msc.legacyurl: /web-forms/overview/older-versions-security/roles/assigning-roles-to-users-cs
msc.type: authoredcontent
ms.openlocfilehash: f8573afc2fd5f12611f88f8bdad7e14389017808
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37820132"
---
<a name="assigning-roles-to-users-c"></a>사용자 (C#)에 역할 할당
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/CS.10.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial10_AssigningRoles_cs.pdf)

> 이 자습서에서는 두 ASP.NET 페이지 어떤 역할에 속하는 사용자 관리를 도우려면 빌드합니다. 첫 번째 페이지는 사용자가 지정된 된 역할에 속한 참조 하는 기능이 포함 됩니다 특정 사용자가 속한 역할 및 기능을 할당 하거나 특정 역할에서 특정 사용자를 제거 합니다. 두 번째 페이지에는 살펴보면서 CreateUserWizard 컨트롤 새로 만든된 사용자가 속한 역할을 지정 하는 단계를 포함 하도록 합니다. 관리자는 새 사용자 계정을 만들 수 있는 시나리오에서 유용 합니다.


## <a name="introduction"></a>소개

<a id="_msoanchor_1"> </a> [이전 자습서](creating-and-managing-roles-cs.md) 역할 프레임 워크를 검사 하며 `SqlRoleProvider`; 사용 하는 방법에 살펴보았습니다는 `Roles` 만들기, 검색 및 역할을 삭제 하는 클래스. 를 만들고 역할을 삭제 하는 것 외에도 할당 또는 역할에서 사용자를 제거 하는 일을 할 수 해야 합니다. 아쉽게도 ASP.NET은 어떤 역할에 속한 사용자를 관리 하기 위한 웹 컨트롤을 사용 하 여 제공 되지 않습니다. 대신 이러한 연결을 관리 하는 고유한 ASP.NET 페이지 만들어야 합니다. 다행 스럽게도 추가 하 고 역할에 사용자를 제거 하는 것은 매우 쉽습니다. `Roles` 클래스에는 하나 이상의 역할에 하나 이상의 사용자를 추가 하기 위한 메서드 수를 포함 합니다.

이 자습서에서는 두 ASP.NET 페이지 어떤 역할에 속하는 사용자 관리를 도우려면 빌드합니다. 첫 번째 페이지는 사용자가 지정된 된 역할에 속한 참조 하는 기능이 포함 됩니다 특정 사용자가 속한 역할 및 기능을 할당 하거나 특정 역할에서 특정 사용자를 제거 합니다. 두 번째 페이지에는 살펴보면서 CreateUserWizard 컨트롤 새로 만든된 사용자가 속한 역할을 지정 하는 단계를 포함 하도록 합니다. 관리자는 새 사용자 계정을 만들 수 있는 시나리오에서 유용 합니다.

이제 시작 하겠습니다.

## <a name="listing-what-users-belong-to-what-roles"></a>어떤 역할에 속한 사용자를 나열 합니다.

첫 번째 업무 우선 순위가 자습서는 사용자 역할에 할당할 있습니다 웹 페이지를 만드는 것입니다. 직접 역할에 사용자를 할당 하는 방법을 고려할 것 전에 보겠습니다 먼저 집중할 어떤 역할에 속한 사용자를 확인 하는 방법. 이 정보를 표시 하는 방법은 두 가지: "역할" 또는 "사용자가." 에서는 방문자 역할을 선택 하 고의 모든 역할 ("역할"으로 표시)에 속하는 사용자 표시를 시작 하거나에서는 사용자를 선택한 다음 표시할 ("user"으로 표시) 해당 사용자에 게 할당 된 역할에 대 한 방문자를 요구할 수 있습니다.

방문자가 사용자를 특정 역할에 속하는 집합 파악 하고자 하는 위치 "에서"역할"보기는 상황에서 유용 "사용자별" 보기 방문자가 특정 사용자의 역할을 알아야 하는 경우에 적합 합니다. "역할별" 및 "사용자"가 모두 포함 하는 페이지 죠 인터페이스입니다.

"사용자별" 인터페이스를 만드는 것부터 시작 하겠습니다. 이 인터페이스는 드롭다운 목록 및 확인란의 목록으로 구성 됩니다. 드롭 다운 목록이 채워집니다 사용자 집합을 사용 하 여 시스템에서 확인란은 역할을 열거 합니다. 드롭다운 목록에서 사용자를 선택 하면 사용자가 속한 역할 확인 합니다. 페이지를 방문 하는 사용자 수를 확인 하거나 추가 하거나 해당 역할에서 선택한 사용자를 제거 하려면 확인란의 선택을 취소 합니다.

> [!NOTE]
> 드롭다운 목록에 목록을 사용 하 여 사용자 계정을 않습니다 웹 사이트에 대 한 이상적인 있는 수백 개의 사용자 계정이 있을 수 있습니다. 드롭다운 목록 옵션 중 비교적 짧은 목록에서 하나의 항목을 선택 하는 사용자를 허용 하도록 설계 되었습니다. 신속 하 게 되기 다루기 목록 항목 수가 증가 합니다. 잠재적으로 많은 수의 사용자 계정 갖게 되는 웹 사이트를 구축 하는 경우 대체 사용자 인터페이스를 사용 하 여 고려해 야 할 페이징할 수 있는 GridView 또는 필터링 가능 인터페이스를 나열 하는 프롬프트 문자를 선택 하는 방문자와 같은 고만 사용자가 선택한 문자로 시작 하는 해당 사용자를 보여 줍니다.


## <a name="step-1-building-the-by-user-user-interface"></a>1 단계: "User" 하 여 사용자 인터페이스 구축

열기는 `UsersAndRoles.aspx` 페이지입니다. 페이지의 맨 위에 있는 라는 레이블을 웹 컨트롤을 추가 `ActionStatus` 지울 및 해당 `Text` 속성입니다. 사용 하 여이 레이블을 대 한 의견을 수행 하는 작업 같은 메시지를 표시, "사용자 Tito에 추가 된 관리자 역할" 또는 "사용자 Jisun는 감독자 역할에서 제거 되었습니다 했습니다." 이러한 확인 하기 위해 레이블 설정 메시지 눈에 띄는 `CssClass` "중요" 속성입니다.

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample1.aspx)]

다음으로, 다음 CSS 클래스 정의 추가 합니다 `Styles.css` stylesheet:

[!code-css[Main](assigning-roles-to-users-cs/samples/sample2.css)]

이 CSS 정의 큰, 빨강 글꼴을 사용 하 여 레이블을 표시 하려면 브라우저에 지시 합니다. 그림 1에서는 Visual Studio 디자이너를 통해이 효과 보여 줍니다.


[![대규모의 빨간색 글꼴로 레이블의 CssClass 속성 결과](assigning-roles-to-users-cs/_static/image2.png)](assigning-roles-to-users-cs/_static/image1.png)

**그림 1**: The 레이블의 `CssClass` Large, 빨강 글꼴의에서 속성 결과 ([클릭 하 여 큰 이미지 보기](assigning-roles-to-users-cs/_static/image3.png))


다음으로 설정 페이지로 DropDownList 추가 해당 `ID` 속성을 `UserList`, 설정 및 해당 `AutoPostBack` 속성을 true로 합니다. 시스템의 모든 사용자를 나열 하려면이 DropDownList 사용 됩니다. 이 DropDownList MembershipUser 개체의 컬렉션에 바인딩됩니다. DropDownList MembershipUser 개체의 사용자 이름 속성을 표시 합니다 (및 목록 항목의 값으로 사용)를 원하므로 DropDownList의 설정 `DataTextField` 고 `DataValueField` 속성 "UserName"으로 합니다.

드롭다운 목록에서 아래 추가 라는 Repeater `UsersRoleList`합니다. 이 반복기로 나열 됩니다 역할의 모든 시스템에는 일련의 확인란 합니다. 반복기의 정의 `ItemTemplate` 다음 선언적 태그를 사용 하 여:

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample3.aspx)]

합니다 `ItemTemplate` 라는 단일 CheckBox 웹 컨트롤을 포함 하는 태그 `RoleCheckBox`합니다. 확인란의 `AutoPostBack` 속성이 True로 설정 되 고 `Text` 속성이 바인딩된 `Container.DataItem`. 데이터 바인딩 구문을 원인은 단순히 `Container.DataItem` 역할 프레임 워크를 문자열 배열로 역할 이름 목록을 반환 하 고 반복기에 바인딩할 수는 우리는이 문자열 배열 때문입니다. 철저 한 설명은이 구문은 데이터 웹 컨트롤에 바인딩된 배열의 내용을 표시 하는 이유는이 자습서의 범위를 벗어납니다. 이 문제에 대 한 자세한 내용은 참조 [스칼라 배열 데이터 웹 컨트롤에 바인딩](http://aspnet.4guysfromrolla.com/articles/082504-1.aspx)합니다.

이 시점에서 "사용자별" 인터페이스의 선언적 태그는 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample4.aspx)]

이제 DropDownList에 사용자 계정을 집합과 Repeater에 역할 집합이 바인딩하기 위한 코드를 작성할 준비가 되었습니다. 페이지의 코드 숨김 클래스 라는 메서드를 추가 `BindUsersToUserList` 라는 다른 `BindRolesList`, 다음 코드를 사용 하 여:

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample5.cs)]

합니다 `BindUsersToUserList` 메서드를 통해 시스템에서 모든 사용자 계정을 검색 하는 [ `Membership.GetAllUsers` 메서드](https://msdn.microsoft.com/library/dy8swhya.aspx)합니다. 반환이 [ `MembershipUserCollection` 개체](https://msdn.microsoft.com/library/system.web.security.membershipusercollection.aspx)의 컬렉션인 [ `MembershipUser` 인스턴스](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)합니다. 이 컬렉션을 바인딩할는 `UserList` DropDownList 합니다. 합니다 `MembershipUser` 인스턴스 컬렉션 처럼 다양 한 속성을 포함 하는 구성을 `UserName`를 `Email`, `CreationDate`, 및 `IsOnline`합니다. DropDownList의 값을 표시 하도록 지시 하기 위해를 `UserName` 속성을 있는지 확인 합니다 `UserList` DropDownList의 `DataTextField` 및 `DataValueField` 속성이 "UserName"으로 설정 되었습니다.

> [!NOTE]
> `Membership.GetAllUsers` 메서드에 두 개의 오버 로드가 있습니다: 하나의 입력된 매개 변수가 없으면를 수락 하 고 모든 사용자를 반환 하 고 페이지 크기와 인덱스 페이지에 대 한 정수 값에서 지정 된 사용자의 하위 집합만 반환 하는 하나입니다. 대용량 페이징할 수 있는 사용자 인터페이스 요소에 표시 되는 사용자 계정의 경우 사용자 계정 보다는 모두의 정확한 하위 집합만 반환 되므로 두 번째 오버 로드를 보다 효율적으로 페이지에서 사용자가 사용할 수 있습니다.


합니다 `BindRolesToList` 메서드를 호출 하 여 시작 합니다 `Roles` 클래스의 [ `GetAllRoles` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.getallroles.aspx), 시스템에서 역할을 포함 하는 문자열 배열을 반환 하는 합니다. 이 문자열 배열 반복기에 바인딩됩니다.

마지막으로, 페이지가 처음 로드 될 때이 두 메서드를 호출 해야 합니다. 다음 코드를 `Page_Load` 이벤트 처리기에 추가합니다.

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample6.cs)]

이 코드를 사용 하 여 잠시는 브라우저를 통해 페이지를 방문 화면은 그림 2와 비슷하게 표시 됩니다. 모든 사용자 계정을 채워집니다 드롭 다운 목록에서을 그 아래에, 각 역할 확인란으로 표시 됩니다. 설정 했기 때문은 `AutoPostBack` 포스트백을 발생 시키는 속성 DropDownList 및 확인란의 True로 확인 또는 역할을 선택 취소 하면 선택한 사용자를 변경 합니다. 그러나 아직 있으므로 이러한 작업을 처리 하는 코드를 쓸 조치가 수행 됩니다. 에서는에서는 다음 두 섹션에서 이러한 작업을 수행할 수 있습니다.


[![사용자 및 역할 페이지에 표시 됩니다.](assigning-roles-to-users-cs/_static/image5.png)](assigning-roles-to-users-cs/_static/image4.png)

**그림 2**: 사용자 및 역할 페이지에 표시 됩니다 ([큰 이미지를 보려면 클릭](assigning-roles-to-users-cs/_static/image6.png))


### <a name="checking-the-roles-the-selected-user-belongs-to"></a>에 선택한 사용자가 속한 역할 확인

업데이트 해야 페이지를 먼저 로드 되 면, 방문자가 드롭다운 목록에서 새 사용자를 선택할 때마다는 `UsersRoleList`의 확인란을 지정 된 역할 확인란이 선택 된 사용자가 해당 역할에 속한 경우에 있도록 합니다. 이렇게 하려면 라는 메서드를 만듭니다 `CheckRolesForSelectedUser` 다음 코드를 사용 하 여:

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample7.cs)]

위의 코드는 선택한 사용자가 누구 인지를 확인 하 여 시작 합니다. 그런 다음 역할 클래스의 [ `GetRolesForUser(userName)` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.getrolesforuser.aspx) 역할 문자열 배열로 지정된 된 사용자의 집합을 반환 합니다. 반복기의 항목 열거 어 및 각 항목의 `RoleCheckBox` 확인란을 프로그래밍 방식으로 참조 됩니다. 확인란이 선택 되어 해당 역할에 포함 된 경우에는 `selectedUsersRoles` 문자열 배열입니다.

> [!NOTE]
> `selectedUserRoles.Contains<string>(...)` ASP.NET 버전 2.0 사용 하는 경우 구문 컴파일되지 것입니다. 합니다 `Contains<string>` 메서드는의 일부를 [LINQ 라이브러리](http://en.wikipedia.org/wiki/Language_Integrated_Query), ASP.NET 3.5와 새로운 합니다. 여전히 ASP.NET 버전 2.0 사용 하는 경우 사용 합니다 [ `Array.IndexOf<string>` 메서드](https://msdn.microsoft.com/library/eha9t187.aspx) 대신 합니다.


합니다 `CheckRolesForSelectedUser` 메서드를 두 가지 경우에 호출 해야 합니다.: 페이지가 처음 로드 될 때와 때마다는 `UserList` DropDownList의 선택한 인덱스 변경 됩니다. 따라서에서이 메서드를 호출 합니다 `Page_Load` 이벤트 처리기 (을 호출한 후 `BindUsersToUserList` 고 `BindRolesToList`). DropDownList의에 대 한 이벤트 처리기를 만들 수도, `SelectedIndexChanged` 이벤트에서에서이 메서드를 호출 합니다.

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample8.cs)]

이 코드를 사용 하 여 브라우저를 통해 페이지를 테스트할 수 있습니다. 그러나는 `UsersAndRoles.aspx` 페이지에는 현재 역할에 사용자를 할당 하는 능력이 없는, 역할이 있는 사용자가 없습니다. 이 코드는 필자의 단어를 수행 하 고는 않습니다. 나중에 확인 잠시 후에 사용자 역할에 할당 하기 위한 인터페이스를 만들겠습니다 또는 레코드를 삽입 하 여 역할에 사용자를 수동으로 추가할 수 있습니다는 `aspnet_UsersInRoles` 이 functi 테스트 하기 위해 테이블 이제 onality 합니다.

### <a name="assigning-and-removing-users-from-roles"></a>할당 하 고 역할에서 사용자 제거

방문자를 확인 또는 있는 확인란을 선택 하거나 선택 취소 하면는 `UsersRoleList` Repeater를 추가 하 여 해당 역할에서 선택한 사용자를 제거 해야 합니다. 확인란의 `AutoPostBack` 속성은 현재 checked 또는 unchecked 반복기에서 확인란은 언제 든 지 포스트백을 true로 설정 됩니다. 즉, 해당 확인란의 이벤트 처리기를 생성 해야 `CheckChanged` 이벤트입니다. Repeater 컨트롤의 확인란을 이므로 이벤트 처리기 연결을 수동으로 추가 해야 합니다. 코드 숨김 클래스에 이벤트 처리기를 추가 하 여 시작을 `protected` 메서드를 다음과 같이 합니다.

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample9.cs)]

잠시 후에이 이벤트 처리기에 대 한 코드를 쓸 반환 됩니다. 먼저 이벤트 처리 작업을 완료 하겠습니다. 반복기의 내에서 확인란의 선택을 `ItemTemplate`, 추가 `OnCheckedChanged="RoleCheckBox_CheckChanged"`합니다. 이 구문은 연결 합니다 `RoleCheckBox_CheckChanged` 이벤트 처리기는 `RoleCheckBox`의 `CheckedChanged` 이벤트입니다.

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample10.aspx)]

마지막 작업을 완료 하는 것은 `RoleCheckBox_CheckChanged` 이벤트 처리기입니다. 이 확인란을 인스턴스를 알려줍니다. 역할 된 checked 또는 unchecked 통해 때문에 이벤트를 발생 시킨 CheckBox 컨트롤을 참조 하 여 시작 하려면 먼저 해당 `Text` 고 `Checked` 속성입니다. 선택한 사용자의 사용자 이름과 함께이 정보를 사용 하에서는 추가 하거나 제거할 사용자 역할을 통해 합니다 `Roles` 클래스의 [ `AddUserToRole` ](https://msdn.microsoft.com/library/system.web.security.roles.addusertorole.aspx) 하거나 [ `RemoveUserFromRole` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromrole.aspx)합니다.

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample11.cs)]

위의 코드를 통해 사용할 수 있는 이벤트를 발생 하는 확인란을 프로그래밍 방식으로 참조 하 여 시작 된 `sender` 입력된 매개 변수입니다. 확인란을 선택한 경우 선택한 사용자 지정된 역할을이 고 그렇지 역할에서 제거 됩니다에 추가 됩니다. 두 경우 모두는 `ActionStatus` 레이블 방금 수행한 작업을 요약 메시지를 표시 합니다.

시간을 내어 브라우저를 통해이 페이지를 테스트 합니다. Tito 사용자를 선택 하 고 Tito 관리자 및 감독자 역할에 추가 합니다.


[![관리자 및 감독자 역할에 추가한 Tito](assigning-roles-to-users-cs/_static/image8.png)](assigning-roles-to-users-cs/_static/image7.png)

**그림 3**: Tito 관리자 및 감독자 역할에 추가 되었습니다 ([큰 이미지를 보려면 클릭](assigning-roles-to-users-cs/_static/image9.png))


그런 다음 드롭다운 목록에서 Bruce 사용자를 선택 합니다. 다시 게시 되며 반복기의 확인란을 통해 업데이트 되는 `CheckRolesForSelectedUser`합니다. Bruce 속해 있지 않으므로 아직 모든 역할을 하므로 두 확인란 검사 되지 않습니다. 다음으로 Bruce 감독자 역할에 추가 합니다.


[![Bruce는 감독자 역할에 추가 되었습니다.](assigning-roles-to-users-cs/_static/image11.png)](assigning-roles-to-users-cs/_static/image10.png)

**그림 4**: Bruce 감독자 역할에 추가 되었습니다 ([큰 이미지를 보려면 클릭](assigning-roles-to-users-cs/_static/image12.png))


추가 기능을 확인 하는 `CheckRolesForSelectedUser` 메서드를 Tito 또는 Bruce 이외의 사용자를 선택 합니다. 확인란은 자동으로 선택 하는 방법, 나타내는 모든 역할에 속해 있지 않습니다. Tito를 반환 합니다. 관리자 및 감독자 확인란 확인 해야 합니다.

## <a name="step-2-building-the-by-roles-user-interface"></a>2 단계: "역할"에 의해 사용자 인터페이스 구축

이 시점에서 "사용자가 인터페이스를 완료 하 고"역할"에 의해 인터페이스 처리를 시작할 준비가 합니다. "역할"에 의해 인터페이스 드롭 다운 목록에서 역할을 선택 하 라는 메시지 하 고 GridView에서 해당 역할에 속해 있는 사용자 집합을 표시 합니다.

다른 DropDownList 컨트롤을 추가 합니다 `UsersAndRoles.aspx` 페이지입니다. Repeater 컨트롤 아래에 있는이 항목을 배치 하 고 이름을 `RoleList`, 설정 및 해당 `AutoPostBack` 속성을 true로 합니다. 아래는 GridView를 추가 하 고 이름을 `RolesUserList`입니다. 이 GridView에는 선택한 역할에 속한 사용자를 표시 합니다. GridView의 설정 `AutoGenerateColumns` 속성을 false로, 표를 TemplateField 추가할 `Columns` 컬렉션 집합과 해당 `HeaderText` 속성을 "사용자"입니다. TemplateField의 정의 `ItemTemplate` 데이터 바인딩 식의 값이 표시 되도록 `Container.DataItem` 에 `Text` 라는 레이블의 속성 `UserNameLabel`합니다.

를 추가 하 고는 GridView 구성과 "역할"에 따라 인터페이스의 선언적 태그 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample12.aspx)]

채울 필요는 `RoleList` DropDownList 시스템에 역할 집합이 포함 된 합니다. 이를 위해 업데이트를 `BindRolesToList` 바인딩합니다 이것이 메서드에서 반환한 문자열 배열이 합니다 `Roles.GetAllRoles` 메서드를를 `RolesList` DropDownList (뿐만 `UsersRoleList` 반복기).

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample13.cs)]

마지막 두 줄을 `BindRolesToList` 역할 집합이 바인딩할 메서드를 추가한는 `RoleList` DropDownList 컨트롤입니다. 그림 5-시스템의 역할을 사용 하 여 채워진 드롭다운 목록 브라우저를 통해 볼 때 최종 결과를 보여 줍니다.


[![역할은 RoleList DropDownList에 표시 됩니다.](assigning-roles-to-users-cs/_static/image14.png)](assigning-roles-to-users-cs/_static/image13.png)

**그림 5**:의 역할에 표시 되는 `RoleList` DropDownList ([클릭 하 여 큰 이미지 보기](assigning-roles-to-users-cs/_static/image15.png))


### <a name="displaying-the-users-that-belong-to-the-selected-role"></a>선택한 역할에 속한 사용자를 표시 합니다.

페이지 로드 될 때 먼저 또는에서 새 역할을 선택 하는 경우는 `RoleList` 드롭다운 목록에서 GridView에서 해당 역할에 속한 사용자의 목록을 표시 해야 합니다. 라는 메서드를 만듭니다 `DisplayUsersBelongingToRole` 다음 코드를 사용 합니다.

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample14.cs)]

선택한 역할을 가져오면 서 시작 됩니다이 메서드는 `RoleList` DropDownList 합니다. 사용 하 여는 [ `Roles.GetUsersInRole(roleName)` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.getusersinrole.aspx) 문자열 배열을 해당 역할에 속하는 사용자의 사용자 이름 검색 하려면. 이 배열에 바인딩됩니다.는 `RolesUserList` GridView입니다.

이 메서드를 두 가지 상황에서 호출 해야 합니다.: 때와 페이지가 처음 로드 될 때 선택된 된 역할에는 `RoleList` DropDownList 변경 합니다. 따라서 업데이트를 `Page_Load` 이벤트 처리기를 호출한 후이 메서드는 호출 되도록 `CheckRolesForSelectedUser`합니다. 다음에 대 한 이벤트 처리기를 만듭니다는 `RoleList`의 `SelectedIndexChanged` 이벤트 너무 여기에서이 메서드를 호출 합니다.

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample15.cs)]

현재 위치에서이 코드는 `RolesUserList` GridView에는 선택한 역할에 속하는 해당 사용자가 표시 됩니다. 그림 6에서 알 수 있듯이, 감독자 역할 두 멤버로 구성: Bruce 및 Tito 합니다.


[![선택한 역할에 속하는 해당 사용자를 나열 하는 GridView](assigning-roles-to-users-cs/_static/image17.png)](assigning-roles-to-users-cs/_static/image16.png)

**그림 6**: The GridView 나열 된 사용자는 역할의 구성원 선택 ([큰 이미지를 보려면 클릭](assigning-roles-to-users-cs/_static/image18.png))


### <a name="removing-users-from-the-selected-role"></a>선택된 된 역할에서 사용자 제거

보겠습니다 보강을 `RolesUserList` GridView 열을 포함 하도록 "제거" 단추입니다. 특정 사용자에 대 한 "제거" 단추를 클릭 하면 해당 역할에서 제거 됩니다.

GridView에 삭제 단추 필드를 추가 하 여 시작 합니다. 이 필드에 필드 가장 왼쪽으로 표시 되 고 변경 해야 해당 `DeleteText` "삭제" (기본값)에서 "제거" 속성입니다.


[![추가 된](assigning-roles-to-users-cs/_static/image20.png)](assigning-roles-to-users-cs/_static/image19.png)

**그림 7**: GridView를 "제거" 단추를 추가 ([큰 이미지를 보려면 클릭](assigning-roles-to-users-cs/_static/image21.png))


포스트백 근거가 "제거" 단추를 클릭할 때 GridView의 및 `RowDeleting` 이벤트가 발생 합니다. 이 이벤트에 대 한 이벤트 처리기를 만들고 선택된 된 역할에서 사용자를 제거 하는 코드를 작성 해야 합니다. 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample16.cs)]

선택한 역할 이름을 확인 하 여 코드를 시작 합니다. 그런 다음 프로그래밍 방식으로 참조를 `UserNameLabel` 제거할 사용자의 사용자를 확인 하기 위해 해당 "제거" 단추를 클릭 한 행에서 제어 합니다. 사용자가 다음에 대 한 호출을 통해 역할에서 제거 된 `Roles.RemoveUserFromRole` 메서드. 합니다 `RolesUserList` GridView 다음 새로 고쳐지고이 통해 메시지가 표시 됩니다는 `ActionStatus` 레이블 컨트롤입니다.

> [!NOTE]
> "제거" 단추는 모든 종류의 사용자에서 역할에서 사용자를 제거 하기 전에 확인 필요 하지 않습니다. 초대한 사용자에 게 확인의 일정 수준에 추가할 수 있습니다. 작업을 확인 하는 가장 쉬운 방법 중 하나는 클라이언트 쪽 확인 대화 상자를 통해입니다. 이 기술에 대 한 자세한 내용은 참조 하세요. [삭제 하는 경우 클라이언트 쪽 확인 추가](https://asp.net/learn/data-access/tutorial-42-cs.aspx)합니다.


그림 8 사용자 Tito 감독자 그룹에서 제거 된 후 페이지를 보여 줍니다.


[![안타깝게도 Tito 더 이상 감독자](assigning-roles-to-users-cs/_static/image23.png)](assigning-roles-to-users-cs/_static/image22.png)

**그림 8**: 슬프게 Tito 더 이상 감독자 ([큰 이미지를 보려면 클릭](assigning-roles-to-users-cs/_static/image24.png))


### <a name="adding-new-users-to-the-selected-role"></a>선택한 역할에 새 사용자 추가

사용자를 선택된 된 역할에서 제거와 함께이 페이지로 방문자 선택한 역할에 사용자를 추가할 수 수도 해야 합니다. 선택한 역할에 사용자를 추가 하는 것에 대 한 최상의 인터페이스 것으로 예상 되는 사용자 계정의 수에 따라 달라 집니다. 웹 사이트를 소수의 수십 개의 사용자 계정을 저장할 이하인 경우, DropDownList를 여기서 사용할 수 있습니다. 수천 개의 사용자 계정 수 있는 경우 된 계정에 특정 계정에 대 한 검색을 통해 페이지 또는 다른 방식으로 사용자 계정을 필터링 방문자를 허용 하는 사용자 인터페이스를 포함 하려고 합니다.

이 페이지에 대 한 시스템에서 사용자 계정 수에 관계 없이 작동 하는 매우 간단한 인터페이스를 사용해 보겠습니다. 즉, 방문자 선택한 역할에 추가 하려고 합니다. 사용자의 사용자 이름을 입력 하 라는 메시지가 표시 텍스트를 사용 합니다. 이름이 없는 사용자가 있는 경우 사용자 역할의 멤버인 이미 인 경우 메시지가 표시 됩니다 `ActionStatus` 레이블. 하지만 사용자는 존재 하 고 역할의 멤버인 경우 하는 경우에 역할에 추가 하 고 표를 새로 고침에서는 했습니다.

텍스트 상자 및 GridView 아래 단추를 추가 합니다. TextBox의 설정 `ID` 하 `UserNameToAddToRole` 단추를 설정 하 고 `ID` 및 `Text` 속성을 `AddUserToRoleButton` 및 "사용자 역할에 추가"를 각각.

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample17.aspx)]

다음으로 만듭니다는 `Click` 에 대 한 이벤트 처리기는 `AddUserToRoleButton` 다음 코드를 추가 하 고:

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample18.cs)]

대부분의 코드는 `Click` 이벤트 처리기는 다양 한 유효성 검사를 수행 합니다. 방문자에서 사용자 이름을 제공 하는 것이 되도록는 `UserNameToAddToRole` 텍스트는 사용자가 시스템을 이미 선택한 역할에 속하지 않는 상자에 붙여넣습니다. 이러한 검사가 실패 하면이에 적절 한 메시지가 표시 됩니다 `ActionStatus` 이벤트 처리기가 종료 되었습니다. 사용자를 통해 역할에 추가 됩니다 모든 검사를 통과 합니다 `Roles.AddUserToRole` 메서드. 그런 다음, 텍스트의 `Text` 속성을 해제, GridView 새로 고쳐지면 및 `ActionStatus` 레이블을 선택한 역할에 지정된 된 사용자가 성공적으로 추가 되었는지 나타내는 메시지를 표시 합니다.

> [!NOTE]
> 사용을 보장 하기 위해 지정된 된 사용자는 선택한 역할에 이미 속해 있지 않습니다 합니다 [ `Roles.IsUserInRole(userName, roleName)` 메서드](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx)를 나타내는 부울 값을 반환 하는 여부를 *userName* 의멤버인*roleName*합니다. 다시이 메서드를 사용할지는 <a id="_msoanchor_2"> </a> [다음 자습서](role-based-authorization-cs.md) 역할 기반 권한 부여에서 살펴보겠습니다.


브라우저를 통해 페이지를 방문 하 고 있는 감독자 역할을 선택 합니다 `RoleList` DropDownList 합니다. 잘못 된 사용자 이름을 입력 하세요 – 사용자 시스템에 없는 경우를 설명 하는 메시지를 표시 합니다.


[![존재 하지 않는 사용자 역할에 추가할 수 없습니다.](assigning-roles-to-users-cs/_static/image26.png)](assigning-roles-to-users-cs/_static/image25.png)

**그림 9**: 존재 하지 않는 사용자 역할에 추가할 수 없습니다 ([큰 이미지를 보려면 클릭](assigning-roles-to-users-cs/_static/image27.png))


이제 유효한 사용자를 추가 해 보세요. 계속 해 서 다시 Tito 감독자 역할에 추가 합니다.


[![Tito 감독자는 다시 한 번!](assigning-roles-to-users-cs/_static/image29.png)](assigning-roles-to-users-cs/_static/image28.png)

**그림 10**: Tito 감독자는 다시 한 번!  ([클릭 하 여 큰 이미지 보기](assigning-roles-to-users-cs/_static/image30.png))


## <a name="step-3-cross-updating-the-by-user-and-by-role-interfaces"></a>3 단계: 간 업데이트는 "User" 및 "역할" 인터페이스

`UsersAndRoles.aspx` 페이지에서는 사용자 및 역할 관리에 대 한 두 개의 서로 다른 인터페이스를 제공 합니다. 현재 이러한 두 가지 인터페이스는 하나의 인터페이스의 변경 사항을 반영 되지 것입니다 즉시 다른 가능한 되므로 서로 독립적으로 작동 합니다. 예를 들어, 페이지 방문자는 감독자 역할을 선택 한다고 가정해 보겠습니다는 `RoleList` DropDownList Bruce 및 Tito 구성원으로 나열 합니다. 방문자 Tito에서를 선택 하는 다음으로 `UserList` DropDownList에 관리자 및 감독자 확인란을 확인 하는 `UsersRoleList` 반복기입니다. 방문자 다음 반복기에서 Supervisor 역할을 선택 하거나 선택 취소 합니다 Tito가 감독자 역할에서 제거 되지만이 수정 "역할별" 인터페이스에 반영 되지 않습니다. GridView는 감독자 역할의 구성원으로 Tito 계속 표시 됩니다.

역할은 checked 또는 unchecked에서 때마다 GridView를 갱신 해야이 문제를 해결 하는 `UsersRoleList` 반복기입니다. 마찬가지로, 사용자를 제거 하거나 "역할" 하 여 인터페이스에서 역할에 추가할 때마다 Repeater를 새로 고침 해야 합니다.

"사용자"가 인터페이스에서 반복기를 호출 하 여 새로 고쳐질는 `CheckRolesForSelectedUser` 메서드. "역할" 하 여 인터페이스를 수정할 수는 `RolesUserList` GridView의 `RowDeleting` 이벤트 처리기 및 `AddUserToRoleButton` 단추의 `Click` 이벤트 처리기입니다. 따라서 호출 해야 합니다 `CheckRolesForSelectedUser` 에서 이러한 각 메서드는 메서드.

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample19.cs)]

호출 하 여 "역할" 하 여 인터페이스에서 GridView 마찬가지로 새로 고쳐집니다 합니다 `DisplayUsersBelongingToRole` 메서드와 "사용자별" 인터페이스를 통해 수정 되는 `RoleCheckBox_CheckChanged` 이벤트 처리기입니다. 따라서 호출 해야 합니다 `DisplayUsersBelongingToRole` 이벤트 처리기에서 메서드.

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample20.cs)]

이러한 코드 변경 내용으로는 "user" 및 "역할" 이제 인터페이스 정확 하 게 업데이트 합니다. 이 확인 하려면 브라우저를 통해 페이지를 방문 하 고 Tito 및 감독자에서 선택 합니다 `UserList` 고 `RoleList` Dropdownlist, 각각. 감독자 역할 Tito에서 "사용자"가 인터페이스에서 반복기에 대 한을 선택 취소 하는 대로 Tito 자동으로 제거 되도록 "역할" 하 여 인터페이스에서 GridView에서 note 합니다. 감독자 확인란 "사용자별" 인터페이스에 확인 다시 Tito 감독자 역할에 다시 "역할" 하 여 인터페이스에서 자동으로 추가 합니다.

## <a name="step-4-customizing-the-createuserwizard-to-include-a-specify-roles-step"></a>4 단계: CreateUserWizard "역할을 지정 합니다." 단계를 포함 하도록 사용자 지정

에 <a id="_msoanchor_3"> </a> [ *사용자 계정 만들기* ](../membership/creating-user-accounts-cs.md) 자습서 CreateUserWizard 웹 컨트롤을 사용 하 여 새 사용자 계정을 만들기 위한 인터페이스를 제공 하는 방법에 살펴보았습니다. CreateUserWizard 컨트롤은 두 가지 방법 중 하나에서 사용할 수 있습니다.

- 방문자가 사이트에서 자신의 사용자 계정을 만들기 위한 수단으로 및
- 새 계정을 만들 수는 관리자를 위한 수단으로

첫 번째 사용 사례에 방문자를 사이트에 제공 하 고 CreateUserWizard, 사이트에 등록 하기 위해 해당 정보를 입력 사항을 입력 합니다. 두 번째 경우, 관리자가 다른 사용자에 대 한 새 계정을 만듭니다.

일부 다른 사용자에 대 한 관리자가 계정을 만들어질 때에 관리자가 새 사용자 계정이 속한 역할을 지정할 수 있도록 유용할 수 있습니다. 에 <a id="_msoanchor_4"> </a> [ *저장* *추가 사용자 정보* ](../membership/storing-additional-user-information-cs.md) CreateUserWizard 추가 하 여 사용자 지정 하는 방법에 살펴보았습니다 자습서 `WizardSteps`. CreateUserWizard 새 사용자의 역할을 지정 하기 위해 추가 단계를 추가 하는 방법에 살펴보겠습니다.

엽니다는 `CreateUserWizardWithRoles.aspx` 라는 CreateUserWizard 컨트롤을 추가한 페이지 `RegisterUserWithRoles`합니다. 컨트롤의 설정 `ContinueDestinationPageUrl` 속성을 "~ / Default.aspx"입니다. 관리자가이 CreateUserWizard 컨트롤 데 사용할 새 사용자 계정을 만드는 것 이기 때문에 컨트롤의 설정 `LoginCreatedUser` 속성을 false로 합니다. 이 `LoginCreatedUser` 속성 있는지 여부를 방금 만든 사용자로 방문자가 자동으로 로그온 하 고 기본값은 True로 지정 합니다. 에서는 False로 설정 하므로 자신으로 로그인 하 게 하려면 관리자로 새 계정을 만들 때.

다음으로, 선택는 "추가/제거 `WizardSteps`..." CreateUserWizard의 스마트 태그에서 옵션 및 새 `WizardStep`설정, 해당 `ID` 에 `SpecifyRolesStep`입니다. 이동 된 `SpecifyRolesStep WizardStep` "Sign Up for 새 계정" 단계를 수행 하면 되지만 "완료" 단계 전에 제공 되도록 합니다. 설정 된 `WizardStep`의 `Title` 속성 "지정 역할"을 해당 `StepType` 속성을 `Step`, 및 해당 `AllowReturn` 속성을 false로 합니다.


[![추가 된](assigning-roles-to-users-cs/_static/image32.png)](assigning-roles-to-users-cs/_static/image31.png)

**그림 11**: "지정 된 역할"을 추가 `WizardStep` CreateUserWizard를 ([클릭 하 여 큰 이미지 보기](assigning-roles-to-users-cs/_static/image33.png))


이 변경 후 CreateUserWizard의 선언적 태그는 다음과 같이 표시 됩니다.

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample21.aspx)]

"지정 된 역할" `WizardStep`, CheckBoxList 라는 추가 `RoleList`합니다. 새로 만든된 사용자가 속한 역할을 확인 하려면 페이지를 방문 하는 사용자를 사용 하도록 설정 하면 사용 가능한 역할을이 CheckBoxList에 나열 됩니다.

두 가지 코딩 작업을 사용 하 여 왼쪽: 채워야 먼저는 `RoleList` CheckBoxList 시스템의 역할을 사용 하 여 둘째, "지정 역할" 단계의 "완료" 단계를 이동할 때 선택한 역할을 만든된 사용자를 추가 해야 합니다. 에서는 첫 번째 태스크를 수행할 수는 `Page_Load` 이벤트 처리기입니다. 다음 코드는 프로그래밍 방식으로 참조 된 `RoleList` 첫 번째 확인란을 페이지에 방문 하 고를 시스템의 역할을 바인딩합니다.

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample22.cs)]

위의 코드 익숙할 것입니다. 에 <a id="_msoanchor_5"> </a> [ *저장* *추가 사용자 정보* ](../membership/storing-additional-user-information-cs.md) 자습서 2를 사용 했습니다 `FindControl` 웹 컨트롤을 참조 하는 문 사용자 지정 내 `WizardStep`합니다. 및이 자습서의 앞부분에서 역할 CheckBoxList에 바인딩하는 코드에서 가져왔습니다.

두 번째 프로그래밍 작업을 수행 하기 위해 알아야 "지정 역할" 단계가 완료 된 경우. CreateUserWizard 있는 회수는 `ActiveStepChanged` 방문자가 다른 한 단계에서 이동할 때마다 발생 하는 이벤트입니다. 에서는 여기에 사용자를 "완료" 단계에 도달한 경우 확인할 수 있습니다. 만약 그렇다면 선택된 된 역할에 사용자를 추가 해야 합니다.

이벤트 처리기를 만듭니다는 `ActiveStepChanged` 이벤트 다음 코드를 추가 합니다.

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample23.cs)]

이벤트 처리기의 항목 열거 사용자만 "완료" 단계에 도달 하는 경우는 `RoleList` CheckBoxList와 방금 만든 사용자는 선택한 역할에 할당 됩니다.

브라우저를 통해이 페이지를 방문 합니다. CreateUserWizard는 첫 번째 단계는 표준 "Sign Up for 새 계정" 단계를 새 사용자의 사용자 이름, 암호, 메일 및 기타 주요 정보를 묻는 경우 Wanda 라는 새 사용자를 만드는 데 필요한 정보를 입력 합니다.


[![Wanda 라는 새 사용자 만들기](assigning-roles-to-users-cs/_static/image35.png)](assigning-roles-to-users-cs/_static/image34.png)

**그림 12**: 새 사용자 라는 Wanda 만듭니다 ([큰 이미지를 보려면 클릭](assigning-roles-to-users-cs/_static/image36.png))


"Create User" 단추를 클릭 합니다. CreateUserWizard 내부적으로 호출 된 `Membership.CreateUser` 메서드를 새 사용자 계정 및 다음 진행 됨에 따라 다음 단계를 만드는 "역할을 지정 합니다." 여기에 시스템 역할은 나열 됩니다. 감독자 확인란을 선택 하 고 클릭 합니다.


[![Wanda 감독자 역할의 멤버로 설정](assigning-roles-to-users-cs/_static/image38.png)](assigning-roles-to-users-cs/_static/image37.png)

**그림 13**: Wanda 감독자 역할의 멤버로 설정 ([큰 이미지를 보려면 클릭](assigning-roles-to-users-cs/_static/image39.png))


다시 게시 및 업데이트 하면 다음을 클릭 하 여 `ActiveStep` "완료" 단계를 합니다. 에 `ActiveStepChanged` 이벤트 처리기를 최근에 만든 사용자 계정 감독자 역할에 할당 됩니다. 이 확인 하려면 돌아갑니다 합니다 `UsersAndRoles.aspx` 감독자에서 선택한 페이지를 `RoleList` DropDownList 합니다. 그림 14에서 알 수 있듯이, 감독자는 이제 이루어져 3 명의 사용자: Bruce, Tito, 및 Wanda 합니다.


[![Bruce, Tito, Wanda와 모든 감독자](assigning-roles-to-users-cs/_static/image41.png)](assigning-roles-to-users-cs/_static/image40.png)

**그림 14**: Bruce, Tito, Wanda와 모든 감독자 ([큰 이미지를 보려면 클릭](assigning-roles-to-users-cs/_static/image42.png))


## <a name="summary"></a>요약

역할 프레임 워크는 특정 사용자의 역할 및 사용자 지정된 역할에 속해야 확인 방법에 대 한 정보를 검색 하는 메서드를 제공 합니다. 또한 하나 이상의 역할에 하나 이상의 사용자 추가 및 제거 하기 위한 메서드는 여러 가지가 있습니다. 이 자습서에서 이러한 메서드 중 두 개만에 집중 합니다. `AddUserToRole` 고 `RemoveUserFromRole`입니다. 단일 사용자에 게 여러 역할을 할당 하 고 여러 사용자가 단일 역할에 추가할 설계 추가 변형이 있습니다.

이 자습서에도 확장 하기로 CreateUserWizard 컨트롤 살펴보고는 `WizardStep` 새로 만든 사용자의 역할을 지정 합니다. 이러한 단계는 새 사용자에 대 한 사용자 계정을 만드는 과정을 간소화 하는 관리자를 수 있습니다.

이 시점에서 만들고 역할을 삭제 하는 방법 및 추가 하 고 역할에서 사용자를 제거 하는 방법을 확인 했습니다. 하지만 아직 역할 기반 권한 부여를 적용 확인 했습니다. 에 <a id="_msoanchor_6"> </a> [다음 자습서](role-based-authorization-cs.md) 살펴보겠습니다-역할에 따라 URL 권한 부여 규칙을 정의 현재 로그인된 한 사용자의 역할을 기반으로 페이지 수준 기능을 제한 하는 방법입니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 웹 사이트 관리 도구 개요](https://msdn.microsoft.com/library/ms228053.aspx)
- [ASP를 검사 합니다. NET의 멤버 자격, 역할 및 프로필](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [고유한 웹 사이트 관리 도구를 롤링합니다.](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)

### <a name="about-the-author"></a>저자 소개

Scott Mitchell, 여러 ASP/ASP.NET 책의 저자 이자 4GuysFromRolla.com의 설립자 이며 1998 Microsoft 웹 기술을 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는  *[Sams 설명 직접 ASP.NET 2.0 24 시간 동안의](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 합니다. Scott에 도달할 수 있습니다 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 통하거나 저자의 블로그 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사 하는 중...

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Teresa Murphy 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](creating-and-managing-roles-cs.md)
> [다음](role-based-authorization-cs.md)
