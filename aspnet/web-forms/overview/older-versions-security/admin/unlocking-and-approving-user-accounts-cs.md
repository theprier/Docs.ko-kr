---
uid: web-forms/overview/older-versions-security/admin/unlocking-and-approving-user-accounts-cs
title: 잠금 해제 및 승인 사용자 계정 (C#) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 관리자가 관리 하는 웹 페이지를 빌드하는 방법을 보여 줍니다. 사용자의 잠긴 및 상태를 승인 합니다. 새 사용자 o를 승인 하는 방법 또한 살펴보겠습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/01/2008
ms.topic: article
ms.assetid: 5346aab1-9974-489f-a065-ae3883b8a350
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-security/admin/unlocking-and-approving-user-accounts-cs
msc.type: authoredcontent
ms.openlocfilehash: f6bf76579898a8ff36b18380100ce4ab2e74fc8d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37392715"
---
<a name="unlocking-and-approving-user-accounts-c"></a>사용자 계정 잠금 해제 및 승인 (C#)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/CS.14.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial14_UnlockAndApprove_cs.pdf)

> 이 자습서에서는 관리자가 관리 하는 웹 페이지를 빌드하는 방법을 보여 줍니다. 사용자의 잠긴 및 상태를 승인 합니다. 전자 메일 주소를 확인 한 후에 새 사용자를 승인 하는 방법 또한 살펴보겠습니다.


## <a name="introduction"></a>소개

사용자 이름, 암호 및 전자 메일을와 함께 각 사용자 계정에 사용자 사이트에 로그인 할 수 있는지 여부를 지정 하는 두 개의 상태 필드: 잠긴 및 승인 합니다. 사용자는 지정 된 수 만큼 지정된 된 수 (기본 설정을 잠글 사용자 10 분 내에 5 개의 잘못 된 로그인 시도 후) 하는 시간 (분) 내에서 잘못 된 자격 증명을 제공 하는 경우 자동으로 잠겨 있습니다. 승인된 상태는 일부 작업을 새 사용자가 사이트에 로그온 할 수 있기 전에 경과 해야 있는 시나리오에서 유용 합니다. 예를 들어, 사용자는 먼저 전자 메일 주소를 확인 하거나 로그인 하기 전에 관리자가 승인 해야 합니다.

때문에 잠긴 out 또는 승인 되지 않은 것이 이러한 상태를 다시 설정할 수 있습니다 하는 방법을 궁금해 할 유일한 자연, 사용자가 로그인 할 수 없습니다. ASP.NET 모든 기본 제공 기능이 포함 되어 있지 않습니다 또는 사용자를 관리 하기 위한 웹 컨트롤 잠겨 및 사이트 간 단위로 처리할이 판단이 필요 하기 때문에 일부 상태를 승인 합니다. 일부 사이트는 모든 새 사용자 계정 (기본 동작)를 자동으로 승인 될 수 있습니다. 다른 관리자에 게 새 계정을 승인 하거나 등록할 때 제공 된 전자 메일 주소로 전송 링크를 방문할 때까지 사용자가 승인 하지 마십시오. 마찬가지로, 관리자가 해당 상태를 다시 설정 될 때까지 일부 사이트 사용자 잠글 수 있습니다, 그리고 되지만 다른 사이트 URL 사용 하 여 잠긴된 사용자에 게 전자 메일을 보내는 방문할 수 있는 해당 계정의 잠금을 해제 합니다.

이 자습서에서는 관리자가 관리 하는 웹 페이지를 빌드하는 방법을 보여 줍니다. 사용자의 잠긴 및 상태를 승인 합니다. 전자 메일 주소를 확인 한 후에 새 사용자를 승인 하는 방법 또한 살펴보겠습니다.

## <a name="step-1-managing-users-locked-out-and-approved-statuses"></a>1 단계: 잠긴 사용자를 관리 및 승인 상태

에 <a id="Tutorial12"> </a> [ *대부분의 사용자 계정 하나를 선택 하는 인터페이스 빌드* ](building-an-interface-to-select-one-user-account-from-many-cs.md) 자습서에서 페이징, 각 사용자 계정 나열 하는 페이지를 생성 했습니다 GridView를 필터링 합니다. 표에서 각 사용자의 이름 및 전자 메일, 해당 승인 및 잠긴 상태, 현재 온라인 있는지 여부 및 사용자에 대 한 설명을 나열 합니다. 승인 된 사용자를 관리 하려면 및 잠긴 상태에서는 없습니다이 표를 편집할 수 있도록 합니다. 사용자의 승인 된 상태를 변경 하려면 관리자는 먼저 사용자 계정을 찾아 하거나 승인 된 확인란 선택을 취소 한 다음 해당 GridView 행 편집 합니다. 또는 별도 ASP.NET 페이지를 통해 승인 및 잠긴 상태 관리 수 없습니다.

이 자습서에서는 두 ASP.NET 페이지를 사용 하겠습니다: `ManageUsers.aspx` 고 `UserInformation.aspx`입니다. 여기서는 `ManageUsers.aspx` 시스템에서 사용자 계정을 나열 하는 동안 `UserInformation.aspx` 특정 사용자에 대 한 승인 및 잠긴 상태를 관리 하는 관리자를 사용 하도록 설정 합니다. 이 첫 번째 업무 우선 순위에서 GridView를 확대 하는 것 `ManageUsers.aspx` 링크 열으로 렌더링 하는 HyperLinkField를 포함 합니다. 각 링크를 가리키도록 하겠습니다 `UserInformation.aspx?user=UserName`, 여기서 *UserName* 편집 하려면 사용자의 이름입니다.

> [!NOTE]
> 에 대 한 코드를 다운로드 하는 경우는 <a id="Tutorial13"> </a> [ *복구 및 암호 변경* ](recovering-and-changing-passwords-cs.md) 했을 수 있는 자습서를 `ManageUsers.aspx` 페이지 집합이 이미 " 관리"링크 및 `UserInformation.aspx` 페이지에서는 선택한 사용자의 암호를 변경 하는 것에 대 한 인터페이스를 제공 합니다. 멤버 자격 API를 우회 하 고 사용자의 암호를 변경 하는 SQL Server 데이터베이스와 직접 작동 하 여 작동 하므로이 자습서를 사용 하 여 관련 코드의 해당 기능을 복제할 필요가 하기로 결정 합니다. 이 자습서를 사용 하 여 처음부터 새로 시작 된 `UserInformation.aspx` 페이지입니다.


### <a name="adding-manage-links-to-theuseraccountsgridview"></a>추가 "관리"에 대 한 링크는`UserAccounts`GridView

엽니다는 `ManageUsers.aspx` 페이지 및 추가에 HyperLinkField는 `UserAccounts` GridView. HyperLinkField의 설정 `Text` 속성을 "Manage" 및 해당 `DataNavigateUrlFields` 하 고 `DataNavigateUrlFormatString` 속성을 `UserName` 및 "UserInformation.aspx?user={0}", 각각. "관리" 텍스트를 표시 하는 모든 하이퍼링크 되지만 각 링크에 적절 한 전달 되도록 이러한 설정을 구성 합니다 HyperLinkField *UserName* 값을 쿼리 합니다.

GridView에는 HyperLinkField를 추가한 후 잠시 보기는 `ManageUsers.aspx` 브라우저를 통해 페이지입니다. 그림 1에서 볼 수 있듯이 각 GridView 행은 이제 "Manage" 링크를 포함 합니다. Bruce에 대 한 "Manage" 링크가 가리키는 `UserInformation.aspx?user=Bruce`Dave에 대 한 "Manage" 링크가 가리키는 반면, `UserInformation.aspx?user=Dave`합니다.


[![HyperLinkField 추가](unlocking-and-approving-user-accounts-cs/_static/image2.png)](unlocking-and-approving-user-accounts-cs/_static/image1.png)

**그림 1**: 각 사용자 계정에 대 한 "Manage" 링크를 추가 하는 HyperLinkField ([큰 이미지를 보려면 클릭](unlocking-and-approving-user-accounts-cs/_static/image3.png))


사용자 인터페이스를 대 한 코드는 `UserInformation.aspx` 보겠습니다 talk 현재 있지만 첫 번째 페이지에 대 한 프로그래밍 방식으로 사용자를 변경 하는 방법의 잠긴 및 상태를 승인 합니다. [ `MembershipUser` 클래스](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx) 했습니다 [ `IsLockedOut` ](https://msdn.microsoft.com/library/system.web.security.membershipuser.islockedout.aspx) 고 [ `IsApproved` 속성](https://msdn.microsoft.com/library/system.web.security.membershipuser.isapproved.aspx)합니다. `IsLockedOut` 속성은 읽기 전용입니다. 프로그래밍 방식으로 사용자를 잠그지 메커니즘이 없습니다. 사용자 잠금 해제 하려면 사용 합니다 `MembershipUser` 클래스의 [ `UnlockUser` 메서드](https://msdn.microsoft.com/library/system.web.security.membershipuser.unlockuser.aspx)합니다. `IsApproved` 속성을 읽고 쓰기 가능 합니다. 이 속성에 모든 변경 내용을 저장 하려면 호출 해야 합니다 `Membership` 클래스의 [ `UpdateUser` 메서드](https://msdn.microsoft.com/library/system.web.security.membership.updateuser.aspx)수정 된 전달 `MembershipUser` 개체입니다.

때문에 `IsApproved` 속성을 읽고, CheckBox 컨트롤을이 속성을 구성 하는 것에 대 한 최상의 사용자 인터페이스 요소 것입니다. 하지만에 대 한 확인란이 작동 하지 것입니다는 `IsLockedOut` 속성 관리자 사용자를 잠글 수 없습니다, 때문에 그녀는 수만 사용자의 잠금을 해제 합니다. 에 대 한 적절 한 사용자 인터페이스는 `IsLockedOut` 속성은 단추를 클릭 하는 경우에 사용자 계정 잠금 해제 합니다. 이 단추는 사용자가 잠겨 있는 경우에 설정 되어야 합니다.

### <a name="creating-theuserinformationaspxpage"></a>만들기는`UserInformation.aspx`페이지

사용자 인터페이스를 구현할 준비가 됩니다. `UserInformation.aspx`합니다. 이 페이지를 열고 다음 웹 컨트롤을 추가 합니다.

- 하이퍼링크 컨트롤을 클릭 하면 관리자에 게 반환 된 `ManageUsers.aspx` 페이지입니다.
- 선택한 사용자의 이름을 표시 하기 위한 레이블 웹 컨트롤입니다. 이 레이블을 설정할 `ID` 하 `UserNameLabel` 지울 및 해당 `Text` 속성입니다.
- CheckBox 컨트롤 이라는 `IsApproved`합니다. 설정 해당 `AutoPostBack` 속성을 `true`입니다.
- 사용자 표시에 대 한 레이블 컨트롤의 날짜와 마지막으로 잠깁니다. 이 레이블 이름을 `LastLockedOutDateLabel` 지울 및 해당 `Text` 속성입니다.
- 사용자 잠금 해제 하는 단추입니다. 이 단추 이름을 `UnlockUserButton` 설정 및 해당 `Text` 속성을 "사용자 잠금 해제" 합니다.
- 예를 들어 "사용자의 승인된 상태가 업데이트 되었습니다." 상태 메시지를 표시 하는 것에 대 한 레이블 컨트롤 이 컨트롤의 이름을 `StatusMessage`out 지우기, 해당 `Text` 속성을 설정 하 고 해당 `CssClass` 속성을 `Important`입니다. (합니다 `Important` CSS 클래스에 정의 된는 `Styles.css` 스타일 시트 파일 큰 빨간색 글꼴로 해당 텍스트를 표시 합니다.)

이러한 컨트롤을 추가한 후 Visual Studio의 디자인 뷰에서 그림 2의 스크린샷과 유사 합니다.


[![UserInformation.aspx에 대 한 사용자 인터페이스 만들기](unlocking-and-approving-user-accounts-cs/_static/image5.png)](unlocking-and-approving-user-accounts-cs/_static/image4.png)

**그림 2**:에 대 한 사용자 인터페이스를 만듭니다 `UserInformation.aspx` ([클릭 하 여 큰 이미지 보기](unlocking-and-approving-user-accounts-cs/_static/image6.png))


다음 작업은 전체 사용자 인터페이스를 사용 하 여 설정 하는 `IsApproved` 선택한 사용자의 정보를 기반으로 다른 컨트롤과 확인란을 선택 합니다. 페이지에 대 한 이벤트 처리기를 만들고 `Load` 이벤트 다음 코드를 추가 합니다.

[!code-csharp[Main](unlocking-and-approving-user-accounts-cs/samples/sample1.cs)]

위의 코드 페이지 및 후속 다시 게시 하지를 처음 방문할 이것이 함으로써 시작 합니다. 통과 사용자 이름의 읽을 합니다 `user` querystring 필드를 통해 해당 사용자 계정에 대 한 정보를 검색 하 고는 `Membership.GetUser(username)` 메서드. 쿼리 문자열을 통해 제공 된 사용자 이름은 없음 또는 지정된 된 사용자를 찾을 수 없습니다, 경우 관리자는 다시 전송 하는 경우는 `ManageUsers.aspx` 페이지입니다.

`MembershipUser` 개체의 `UserName` 의 값이 표시 됩니다는 `UserNameLabel` 및 `IsApproved` 확인란에 따라는 `IsApproved` 속성 값입니다.

`MembershipUser` 개체의 [ `LastLockoutDate` 속성](https://msdn.microsoft.com/library/system.web.security.membershipuser.lastlockoutdate.aspx) 반환을 `DateTime` 잠겨으로 하는 사용자가 마지막으로 나타내는 값입니다. 사용자가 되지 잠겨, 반환 되는 값 멤버 자격 공급자에 따라 다릅니다. 새 계정을 만들면 합니다 `SqlMembershipProvider` 설정 합니다 `aspnet_Membership` 테이블의 `LastLockoutDate` 필드를 `1754-01-01 12:00:00 AM`입니다. 위의 코드에서 빈 문자열을 표시 합니다 `LastLockoutDateLabel` 경우는 `LastLockoutDate` 속성 년 전에 발생 2000;이 고, 그렇지의 날짜 부분은 `LastLockoutDate` 속성에 레이블이 표시 됩니다. 합니다 `UnlockUserButton'` s `Enabled` 속성이 사용자의 차단 상태, 즉 사용자 잠겨 있으면이 단추가 활성화만 됩니다.

잠시 테스트는 `UserInformation.aspx` 브라우저를 통해 페이지입니다. 물론, 해야 시작 `ManageUsers.aspx` 관리할 사용자 계정을 선택 합니다. 도착 시 `UserInformation.aspx`는 `IsApproved` 확인란은 사용자가 승인 되 면만 확인 됩니다. 사용자가 어느 잠겨, 마지막 날짜를 잠긴 표시 됩니다. 사용자 잠금 해제 단추는 사용자가 현재 잠겨 하는 경우에 활성화 됩니다. 선택 하거나 선택을 취소 합니다 `IsApproved` 확인란을 선택 하거나 사용자 잠금 해제 단추를 클릭 하면 포스트백을 하지만 없는 수정 내용이 사용자 계정에 아직 했습니다 때문에 이러한 이벤트에 대 한 이벤트 처리기를 만듭니다.

에 대 한 이벤트 처리기를 만들고 Visual Studio로 돌아가서 합니다 `IsApproved` 확인란의 `CheckedChanged` 이벤트와 `UnlockUser` 단추의 `Click` 이벤트입니다. 에 `CheckedChanged` 이벤트 처리기를 설정 합니다. `IsApproved` 속성을 합니다 `Checked` 확인란을 선택한 다음 호출을 통해 변경 내용을 저장 하는 속성 `Membership.UpdateUser`합니다. 에 `Click` 이벤트 처리기를 호출 하기만 하면 합니다 `MembershipUser` 개체의 `UnlockUser` 메서드. 두 이벤트 처리기에서에 적합 한 메시지를 표시 합니다 `StatusMessage` 레이블.

[!code-csharp[Main](unlocking-and-approving-user-accounts-cs/samples/sample2.cs)]

### <a name="testing-theuserinformationaspxpage"></a>테스트는`UserInformation.aspx`페이지

현재 위치에서 이러한 이벤트 처리기를 사용 하 여 페이지를 다시 방문 및 승인 되지 않은 사용자입니다. 그림 3과 같이 표시 되어야 사용자를 나타내는 페이지의 메시지 간단한 `IsApproved` 속성 성공적으로 수정 합니다.


[![Chris 승인 되었으면 합니다.](unlocking-and-approving-user-accounts-cs/_static/image8.png)](unlocking-and-approving-user-accounts-cs/_static/image7.png)

**그림 3**: Chris 승인 되었습니다 ([큰 이미지를 보려면 클릭](unlocking-and-approving-user-accounts-cs/_static/image9.png))


다음으로, 로그 아웃 하 고 계정을 가진 사용자로 로그인 시도 방금 승인 없습니다. 사용자 승인 되지 않은, 때문에 로그인 할 수 없습니다. 기본적으로 로그인 컨트롤 어떤 이유로 든 사용자 로그인 할 수 없는 경우 동일한 메시지를 표시 합니다. 하지만 합니다 <a id="Tutorial6"> </a> [ *유효성 검사 사용자 자격 증명에 대 한 멤버 자격 사용자 스토어* ](../membership/validating-user-credentials-against-the-membership-user-store-cs.md) 자습서 더 적절 한 메시지를 표시 하려면 Login 컨트롤 향상에 대해 살펴보았습니다. 그림 4에서 알 수 있듯이, Chris 계정을 아직 승인 되지 않은 때문에 로그인 할 수 없는 그 설명 하는 메시지가 표시 됩니다.


[![Chris 없습니다 때문에 His 로그인은 승인 되지 않음](unlocking-and-approving-user-accounts-cs/_static/image11.png)](unlocking-and-approving-user-accounts-cs/_static/image10.png)

**그림 4**: Chris 없습니다 때문에 His 로그인은 승인 되지 않음 ([큰 이미지를 보려면 클릭](unlocking-and-approving-user-accounts-cs/_static/image12.png))


잠금된 기능을 테스트 하려면 승인 된 권한으로 로그인 하지만 잘못 된 암호를 사용 하려고 합니다. 필요한 횟수 사용자 계정이 잠겨 때까지이 프로세스를 반복 합니다. Login 컨트롤 사용자 지정을 표시 하도록 업데이트 되었습니다 잠긴된 계정에서 로그인 하려고 하는 경우. 계정 로그인 페이지에 다음 메시지가 표시 되 면 잠 궜 습니다 알고: "계정의 잠겨 잘못 된 로그인 시도 너무 많이 때문입니다. 관리자 계정이 잠금 해제에 문의 하십시오. "

반환 합니다 `ManageUsers.aspx` 페이지 및 잠긴된 사용자 관리 링크를 클릭 합니다. 그림 5에서 알 수 있듯이의 값이 표시 됩니다 하는 `LastLockedOutDateLabel` 사용자 잠금 해제 단추를 사용 해야 합니다. 사용자 계정의 잠금을 해제 하려면 사용자 잠금 해제 단추를 클릭 합니다. 사용자 잠금 해제 한 후 다시 로그인 할 수 있습니다.


[![Dave는 시스템에서 잠 궜 습니다.](unlocking-and-approving-user-accounts-cs/_static/image14.png)](unlocking-and-approving-user-accounts-cs/_static/image13.png)

**그림 5**: Dave가 된 잠긴 개 시스템 ([큰 이미지를 보려면 클릭](unlocking-and-approving-user-accounts-cs/_static/image15.png))


## <a name="step-2-specifying-new-users-approved-status"></a>2 단계: 새 사용자 지정 상태를 승인

승인된 상태는 일부 작업을 새 사용자가 로그인 하 고 사이트의 사용자 관련 기능에 액세스할 수 있기 전에 수행 하려는 시나리오에서 유용 합니다. 예를 들어, 개인 웹 사이트를 모든 페이지의 로그인 및 등록 페이지를 제외 하 고 인증 된 사용자만 액세스할 수 있는 실행 수 있습니다. 하지만 등록 페이지를 찾아 계정을 만들고 낯선 웹 사이트에 도달 하면 어떻게 되나요? 이를 방지 하려면 등록 페이지를 이동할 수 있습니다는 `Administration` 폴더에 각 계정에 관리자는 수동으로 만들 필요 합니다. 또는 등록을 허용 하지만 사용자 계정 관리자가 승인할 때까지 사이트 액세스를 금지할 수 있습니다.

CreateUserWizard 컨트롤 기본적으로 새 계정을 승인합니다. 컨트롤을 사용 하 여이 동작을 구성할 수 있습니다 [ `DisableCreatedUser` 속성](https://msdn.microsoft.com/en-gb/library/system.web.ui.webcontrols.createuserwizard.disablecreateduser.aspx)합니다. 이 속성을 설정 `true` 새 사용자 계정을 승인 하지 않도록 합니다.

> [!NOTE]
> 기본적으로 CreateUserWizard 컨트롤을 자동으로 새 사용자 계정에 기록합니다. 이 동작은 컨트롤에 의해 결정 됩니다 [ `LoginCreatedUser` 속성](https://msdn.microsoft.com/en-gb/library/system.web.ui.webcontrols.createuserwizard.logincreateduser.aspx)합니다. 승인 되지 않은 사용자가 사이트에 로그인 할 수 없습니다 때문에 때 `DisableCreatedUser` 됩니다 `true` 의 값에 관계 없이 사이트에 새 사용자 계정 기록 되지 않습니다는 `LoginCreatedUser` 속성입니다.


새 사용자 계정을 통해 프로그래밍 방식으로 만들려는 경우 합니다 `Membership.CreateUser` 승인 되지 않은 사용자 계정을 만들려면 메서드를 새 사용자를 받아들이는 오버 로드 중 하나를 사용 합니다. `IsApproved` 입력된 매개 변수로 속성 값입니다.

## <a name="step-3-approving-users-by-verifying-their-email-address"></a>3 단계: 전자 메일 주소를 확인 하 여 사용자가 승인

많은 웹 사이트를 지 원하는 사용자 계정을 등록할 때 제공 된 전자 메일 주소 확인 될 때까지 새 사용자를 승인 하지 마십시오. 이 확인 프로세스에는 고유한 확인된 전자 메일 주소가 필요 하 고 등록 프로세스에는 추가 단계가 추가 봇, 스팸 및 기타 ne'er-do-wells를 저지 하 일반적으로 사용 됩니다. 이 모델을 사용 하 여 새 사용자가 등록할 때 전송 됩니다 확인 페이지에 대 한 링크를 포함 하는 전자 메일 메시지. 링크를 방문 하 여 사용자는 전자 메일을 받은 것 이며, 따라서 제공 된 전자 메일 주소는 유효한 것으로 입증 되었습니다. 확인 페이지는 사용자를 승인 하는 일을 담당 합니다. 이러한 경우 자동으로 있으므로이 페이지에 도달 하면 모든 사용자를 승인 또는 사용자와 같은 몇 가지 추가 정보를 제공 하는 후에을 [CAPTCHA](http://en.wikipedia.org/wiki/Captcha)합니다.

이 워크플로 수용할 수 있도록 새 사용자가 승인 되지 않도록 계정 만들기 페이지를 먼저 업데이트 해야 합니다. 열기는 `EnhancedCreateUserWizard.aspx` 페이지에 `Membership` 폴더 집합과 CreateUserWizard 컨트롤의 `DisableCreatedUser` 속성을 `true`입니다.

그런 다음 해당 계정을 확인 하는 방법에 대 한 지침을 사용 하 여 새 사용자에 게 전자 메일을 보내려면 CreateUserWizard 컨트롤을 구성 해야 합니다. 전자 메일의 링크를 포함 특히 합니다 `Verification.aspx` 페이지 (에 아직 했습니다는 만들기) 새 사용자의 전달 `UserId` querystring을 통해. `Verification.aspx` 페이지 지정된 된 사용자를 조회 및 승인 된 것으로 표시 됩니다.

### <a name="sending-a-verification-email-to-new-users"></a>새 사용자에 게 확인 전자 메일을 보낼

CreateUserWizard 컨트롤에서 전자 메일을 보내도록 구성 해당 `MailDefinition` 속성 적절 하 게 합니다. 에 설명 된 대로 합니다 <a id="Tutorial13"> </a> [이전 자습서](recovering-and-changing-passwords-cs.md), ChangePassword 및 PasswordRecovery 컨트롤 포함는 [ `MailDefinition` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.maildefinition.aspx) 동일한 방식으로 작동 하는 CreateUserWizard 컨트롤입니다.

> [!NOTE]
> 사용 하는 `MailDefinition` 메일 배달을 지정 해야 하는 속성의 옵션 `Web.config`합니다. 자세한 내용은 참조 [ASP.NET에서 전자 메일 보내기](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)합니다.


라는 새 email 템플릿을 만들어 시작 `CreateUserWizard.txt` 에 `EmailTemplates` 폴더입니다. 템플릿에 대 한 다음 텍스트를 사용 합니다.

[!code-aspx[Main](unlocking-and-approving-user-accounts-cs/samples/sample3.aspx)]

설정 된 `MailDefinition'` s `BodyFileName` 속성을 "~ / EmailTemplates/CreateUserWizard.txt" 고 `Subject` 속성을 "내 웹 사이트 시작! 계정을 활성화 하세요. "

`CreateUserWizard.txt` 전자 메일 템플릿을 포함 한 `<%VerificationUrl%>` 자리 표시자입니다. 이 경우에 대 한 URL을 `Verification.aspx` 페이지에 표시 됩니다. CreateUserWizard 자동으로 대체 합니다 `<%UserName%>` 하 고 `<%Password%>` 새 계정의 이름과 암호를 사용 하 여 자리 표시자 이지만 기본 제공 되지 않습니다 `<%VerificationUrl%>` 자리 표시자. 수동으로 적절 한 확인 URL로 교체 해야 합니다.

이렇게 하려면 CreateUserWizard의에 대 한 이벤트 처리기를 만듭니다 [ `SendingMail` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.sendingmail.aspx) 다음 코드를 추가 합니다.

[!code-csharp[Main](unlocking-and-approving-user-accounts-cs/samples/sample4.cs)]

합니다 `SendingMail` 이벤트가 발생 한 후는 `CreatedUser` 이벤트에는 위의 이벤트 처리기가 새 사용자 실행 시간을 기준으로 계정을 이미 만들었습니다. 새 사용자의 액세스할 수 있습니다 `UserId` 호출 하 여 값을 `Membership.GetUser` 전달 하는 메서드는 `UserName` CreateUserWizard 컨트롤에 입력 합니다. 다음으로, 확인 URL은 형성 됩니다. 문이 `Request.Url.GetLeftPart(UriPartial.Authority)` 반환을 `http://yourserver.com` 부분 URL입니다. `Request.ApplicationPath` 응용 프로그램 루트의 위치 경로 반환 합니다. URL이 다음으로 정의 되어 확인 `Verification.aspx?ID=userId`합니다. 이러한 두 문자열의 전체 URL을 구성 하기 위해 다음 연결 됩니다. 마지막으로 전자 메일 메시지 본문 (`e.Message.Body`)의 모든 항목에 `<%VerificationUrl%>` 전체 URL로 대체 합니다.

최종적은 새 사용자 아니라는 승인 사이트에 로그인 할 수 없습니다.을 의미 합니다. 또한 자동으로 전송 됩니다 링크를 사용 하 여 전자 메일 확인 URL (그림 6 참조).


[![새 사용자에 게 확인 URL에 대 한 링크를 사용 하 여 전자 메일](unlocking-and-approving-user-accounts-cs/_static/image17.png)](unlocking-and-approving-user-accounts-cs/_static/image16.png)

**그림 6**: 새 사용자는 확인 URL에 대 한 링크를 사용 하 여 전자 메일을 받습니다 ([큰 이미지를 보려면 클릭](unlocking-and-approving-user-accounts-cs/_static/image18.png))


> [!NOTE]
> CreateUserWizard 컨트롤의 기본 CreateUserWizard 단계에는 사용자가 만든 계정과 계속 단추를 표시 하는 메시지가 표시 됩니다. 컨트롤의 지정 된 URL로 이동이 클릭 하면 `ContinueDestinationPageUrl` 속성입니다. CreateUserWizard `EnhancedCreateUserWizard.aspx` 새 사용자를 보내도록 구성 된는 `~/Membership/AdditionalUserInfo.aspx`, 사용자에 게 해당 출생지, 홈 페이지 URL 및 서명 확인 메시지를 표시 합니다. 사이트의 홈 페이지를 다시 사용자에 게 전송 하려면이 속성을 업데이트 하는 데이 정보만 추가할 수 있으므로 하 여 로그온 한 사용자, 적합 (`~/Default.aspx`). 또한는 `EnhancedCreateUserWizard.aspx` 페이지나 CreateUserWizard 단계 확인 전자 메일이 전송 된 하 고 해당 계정을이 전자 메일의 지침에 따라 해당 될 때까지 활성화 되지 않습니다 사용자에 게 확장할 수 해야 합니다. I 이러한 수정 사항을 판독기에 대 한 연습을 그대로 둡니다.


### <a name="creating-the-verification-page"></a>확인 페이지 만들기

마지막 작업을 만드는 것은 `Verification.aspx` 페이지입니다. 이 페이지와 연결할 루트 폴더에 추가 된 `Site.master` 마스터 페이지입니다. 대부분의 사이트에 추가 하 여 이전 콘텐츠 페이지를 사용 하 여 수행한 대로 참조 하는 콘텐츠 컨트롤을 제거 합니다 `LoginContent` ContentPlaceHolder 콘텐츠 페이지에는 마스터 페이지의 사용 되도록 기본 콘텐츠입니다.

Label 웹 컨트롤을 추가 합니다 `Verification.aspx` 페이지에서 해당 `ID` 를 `StatusMessage` 해당 텍스트 속성을 지울 및. 다음으로 만듭니다는 `Page_Load` 이벤트 처리기 다음 코드를 추가 합니다.

[!code-csharp[Main](unlocking-and-approving-user-accounts-cs/samples/sample5.cs)]

위 코드의 대부분을 확인 하는 합니다 `UserId` querystring 있는지, 유효한 것을 통해 제공 된 `Guid` 값 및 기존 사용자 계정을 참조 하는 것입니다. 이러한 모든 검사를 통과 하는 경우 사용자 계정이 승인 된; 그렇지 않으면 적합 한 상태 메시지가 표시 됩니다.

그림 7은는 `Verification.aspx` 브라우저를 통해 방문 페이지입니다.


[![새 사용자의 계정이 이제 승인](unlocking-and-approving-user-accounts-cs/_static/image20.png)](unlocking-and-approving-user-accounts-cs/_static/image19.png)

**그림 7**:의 새 사용자 계정이 이제 승인 ([큰 이미지를 보려면 클릭](unlocking-and-approving-user-accounts-cs/_static/image21.png))


## <a name="summary"></a>요약

모든 멤버 자격 사용자 계정에 사용자 사이트에 로그인 할 수 있는지 여부를 결정 하는 두 가지 상태: `IsLockedOut` 고 `IsApproved`입니다. 이러한 속성을 모두 해야 `true` 로그인 사용자에 대 한 합니다.

사용자의 잠긴 상태 (brute force) 메서드를 통해 사이트에 주요 해커의 가능성을 줄이기 위해 보안 조치로 사용 됩니다. 특히 사용자 특정 특정 기간 내에 잘못 된 로그인 시도 수 없으면 잠겨 있습니다. 이러한 경계는의 멤버 자격 공급자 설정을 통해 구성 가능한 `Web.config`합니다.

승인된 상태는 일반적으로 새 사용자가 일부 작업 지났는지 될 때까지 로그인 하지 못하게 하려면 수단으로 사용 됩니다. 아마도 사이트에 필요한 새로운 계정 관리자가 승인 먼저 또는 전자 메일 주소를 확인 하 여 3 단계에서에서 보았듯이 합니다.

즐거운 프로그래밍!

### <a name="about-the-author"></a>저자 소개

Scott Mitchell, 여러 ASP/ASP.NET 책의 저자 이자 4GuysFromRolla.com의 설립자 이며 1998 Microsoft 웹 기술을 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는  *[Sams 설명 직접 ASP.NET 2.0 24 시간 동안의](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 합니다. Scott에 도달할 수 있습니다 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 통하거나 저자의 블로그 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사 하는 중...

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](recovering-and-changing-passwords-cs.md)
> [다음](building-an-interface-to-select-one-user-account-from-many-vb.md)
