---
uid: web-forms/overview/older-versions-security/admin/unlocking-and-approving-user-accounts-cs
title: 잠금 해제 하 고 사용자 계정 (C#) 승인 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 관리자 관리 하기 위한 웹 페이지를 빌드하는 방법을 보여 줍니다. 사용자의 잠긴 및 상태를 승인 합니다. 새 사용자 o 승인 하는 방법 또한 살펴보겠습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/01/2008
ms.topic: article
ms.assetid: 5346aab1-9974-489f-a065-ae3883b8a350
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-security/admin/unlocking-and-approving-user-accounts-cs
msc.type: authoredcontent
ms.openlocfilehash: 8b3d69e96513192bc73a2a6a7cbb4c6e33eb610b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30891401"
---
<a name="unlocking-and-approving-user-accounts-c"></a>사용자 계정 잠금 해제 또는 승인 (C#)
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/CS.14.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial14_UnlockAndApprove_cs.pdf)

> 이 자습서에서는 관리자 관리 하기 위한 웹 페이지를 빌드하는 방법을 보여 줍니다. 사용자의 잠긴 및 상태를 승인 합니다. 전자 메일 주소를 확인 한 후에 새 사용자가 승인 하는 방법 또한 살펴봅니다.


## <a name="introduction"></a>소개

각 사용자 계정에 사용자는 사이트에 로그인 할 수 있는지 여부를 지정 하는 두 개의 상태 필드는 사용자 이름, 암호 및 전자 메일을 함께: 잠기며 승인 합니다. 사용자 지정 된 분 수입니다 (기본 설정을 잠글 사용자 후 10 분 내에 잘못 된 로그인 시도 5) 내에서 지정 된 횟수 잘못 된 자격 증명을 제공 하는 경우 자동으로 잠겨 있습니다. 승인 된 상태는 새 사용자가 사이트에 로그온 할 수 있기 전에 특별 한 조치에 경과 해야 하는 시나리오에서 유용 합니다. 예를 들어 사용자가 전자 메일 주소를 먼저 확인 하거나 로그인 하기 전에 관리자가 승인 해야 합니다.

때문에 잠긴 out 또는 승인 되지 않은 유일한 자연 이러한 상태를 다시 설정할 수 있는 방법을 염려 하는, 사용자 로그인 할 수 없습니다. ASP.NET에는 기본 제공 기능이 없습니다 또는 사용자의 관리를 위한 웹 컨트롤 잠기며 이러한 결정 사이트 간 단위로 처리 해야 하기 때문에 상태, 부분적으로 승인 합니다. 일부 사이트는 모든 새 사용자 계정 (기본 동작)를 자동으로 승인 될 수 있습니다. 다른 관리자가 새 계정을 승인 하거나 등록 될 때 제공 된 전자 메일 주소로 전송 링크를 방문할 때까지 사용자가 승인 하지 않아야 합니다. 마찬가지로, 관리자가 해당 상태를 다시 설정 될 때까지 사용자가 일부 사이트를 잠글 수 있습니다, 그리고 자신의 계정을 잠금 해제를 방문할 수 있는 다른 사이트 URL로 잠긴된 사용자에 게 전자 메일을 보낼 때.

이 자습서에서는 관리자 관리 하기 위한 웹 페이지를 빌드하는 방법을 보여 줍니다. 사용자의 잠긴 및 상태를 승인 합니다. 전자 메일 주소를 확인 한 후에 새 사용자가 승인 하는 방법 또한 살펴봅니다.

## <a name="step-1-managing-users-locked-out-and-approved-statuses"></a>1 단계: 잠긴 사용자의 관리 및 상태를 승인

에 <a id="Tutorial12"> </a> [ *많은에서 사용자 계정 하나를 선택 하는 인터페이스를 빌드* ](building-an-interface-to-select-one-user-account-from-many-cs.md) 에서는 각 사용자 계정에는 페이지 된를 나열 하는 페이지를 생성 하는 자습서는 GridView를 필터링 합니다. 표에 각 사용자의 이름 및 전자 메일, 해당 승인 되거나 잠긴 상태, 현재 온라인 있는지 여부 및 사용자에 대 한 설명을 나열 합니다. 승인 된 사용자의 관리 상태를 잠겨 म 하 게 되 고이 표 편집할 수 있습니다. 사용자의 승인 된 상태를 변경 하려면 관리자는 먼저 사용자 계정을 찾은 다음 승인 된 확인란을 선택 하거나 해당 GridView 행을 편집 합니다. 또는 별도 ASP.NET 페이지를 통해 승인 된 및 잠금 상태를 관리할 수 있습니다.

이 자습서에 대 한 두 ASP.NET 페이지를 사용해 보겠습니다: `ManageUsers.aspx` 및 `UserInformation.aspx`합니다. 여기서는 `ManageUsers.aspx` 시스템에서 사용자 계정을 나열 하는 동안 `UserInformation.aspx` 사용 하면 관리자가 특정 사용자에 대 한 승인 및 잠금 상태를 관리 하 합니다. 첫 번째 order of 비즈니스에서 GridView 보강 하는 것 `ManageUsers.aspx` 링크의 열으로 렌더링 하는 HyperLinkField 포함 하도록 합니다. 각 링크를 가리키도록 원하는 `UserInformation.aspx?user=UserName`여기서 *UserName* 편집할 사용자의 이름입니다.

> [!NOTE]
> 에 대 한 코드를 다운로드 한 경우는 <a id="Tutorial13"> </a> [ *Recovering 및 암호 변경* ](recovering-and-changing-passwords-cs.md) 알 수 있습니다 하는 자습서는 `ManageUsers.aspx` 페이지에는 이미 집합이 포함 되어 " "링크를 관리 및 `UserInformation.aspx` 페이지에서는 선택한 사용자의 암호를 변경 하기 위한 인터페이스를 제공 합니다. I 하지 않기로 결정 멤버 API를 우회 하 고 사용자의 암호를 변경 하려면 SQL Server 데이터베이스와 직접 작동 하 여 정상적으로 완료 하기 때문에이 자습서와 관련 된 코드에서 해당 기능을 복제 합니다. 이 자습서와 처음부터 다시 시작 되 고 `UserInformation.aspx` 페이지.


### <a name="adding-manage-links-to-theuseraccountsgridview"></a>추가 "관리"에 대 한 링크는`UserAccounts`GridView

열기는 `ManageUsers.aspx` 페이지 및 추가에 HyperLinkField는 `UserAccounts` GridView입니다. HyperLinkField의 설정 `Text` 속성을 "Manage" 및 해당 `DataNavigateUrlFields` 및 `DataNavigateUrlFormatString` 속성을 `UserName` 및 "을 (를) UserInformation.aspx?user={0" 각각. 텍스트 "Manage"를 표시 하는 모든 하이퍼링크 되지만 각 링크에 적절 한 전달 되도록 이러한 설정은 구성 된 HyperLinkField *UserName* 쿼리 문자열에 값입니다.

HyperLinkField GridView를 추가한 후 잠시 볼 수는 `ManageUsers.aspx` 브라우저를 통해 페이지입니다. 그림 1에서 볼 수 있듯이 각 GridView 행에 이제 "Manage" 링크가 포함 됩니다. 1 세에 대 한 "Manage" 링크가 가리키는 `UserInformation.aspx?user=Bruce`Dave에 대 한 "Manage" 링크가 가리키는 반면, `UserInformation.aspx?user=Dave`합니다.


[![HyperLinkField 추가](unlocking-and-approving-user-accounts-cs/_static/image2.png)](unlocking-and-approving-user-accounts-cs/_static/image1.png)

**그림 1**: 각 사용자 계정에 대 한 "Manage" 링크를 추가 하는 HyperLinkField ([전체 크기 이미지를 보려면 클릭](unlocking-and-approving-user-accounts-cs/_static/image3.png))


사용자 인터페이스 만들어져에 대 한 코드는 `UserInformation.aspx` 보겠습니다 talk 잠시 있지만 첫 번째 페이지에 대 한 프로그래밍 방식으로 사용자를 변경 하는 방법의 잠기며 상태를 승인 합니다. [ `MembershipUser` 클래스](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx) 가 [ `IsLockedOut` ](https://msdn.microsoft.com/library/system.web.security.membershipuser.islockedout.aspx) 및 [ `IsApproved` 속성](https://msdn.microsoft.com/library/system.web.security.membershipuser.isapproved.aspx)합니다. `IsLockedOut` 속성은 읽기 전용입니다. 프로그래밍 방식으로 사용자를 잠그려면는; 메커니즘이 없습니다. 사용자의 잠금을 해제 하려면 사용 된 `MembershipUser` 클래스의 [ `UnlockUser` 메서드](https://msdn.microsoft.com/library/system.web.security.membershipuser.unlockuser.aspx)합니다. `IsApproved` 속성은 읽기 및 쓰기 가능 합니다. 이 속성을 변경 내용을 저장 하려면 호출 해야는 `Membership` 클래스의 [ `UpdateUser` 메서드](https://msdn.microsoft.com/library/system.web.security.membership.updateuser.aspx)을 수정 된 전달 `MembershipUser` 개체입니다.

때문에 `IsApproved` 속성을 읽고 쓸, CheckBox 컨트롤은이 속성을 구성 하기 위한 최상의 사용자 인터페이스 요소 때문일 수 있습니다. 그러나 CheckBox 적합 하지 것입니다는 `IsLockedOut` 속성 관리자는 사용자를 잠글 수 없으면 때문에 그녀 수만 사용자의 잠금을 해제 합니다. 에 대 한 적절 한 사용자 인터페이스는 `IsLockedOut` 속성은 단추를 클릭 하면 사용자 계정 잠금 해제 합니다. 이 단추는 사용자가 잠겨 하는 경우에 활성화 해야 합니다.

### <a name="creating-theuserinformationaspxpage"></a>만들기는`UserInformation.aspx`페이지

사용자 인터페이스를 구현 합니다. 이제 준비가 `UserInformation.aspx`합니다. 이 페이지를 열고 다음 웹 컨트롤을 추가 합니다.

- 하이퍼링크 컨트롤을 클릭 하면 관리자에 게 반환 된 `ManageUsers.aspx` 페이지.
- 선택한 사용자의 이름을 표시 하기 위한 레이블 웹 컨트롤입니다. 이 레이블은 설정 `ID` 를 `UserNameLabel` 지울 및 해당 `Text` 속성입니다.
- CheckBox 컨트롤 이라는 `IsApproved`합니다. 설정의 `AutoPostBack` 속성을 `true`합니다.
- 사용자를 표시 하기 위한 레이블 컨트롤의 날짜와 마지막 잠깁니다. 이 레이블은 이름을 `LastLockedOutDateLabel` 지울 및 해당 `Text` 속성입니다.
- 사용자 잠금 해제 하는 단추입니다. 이 단추 이름을 `UnlockUserButton` 설정 하 고 해당 `Text` 속성을 "사용자의 잠금을 해제" 합니다.
- 와 같은 "사용자의 승인된 상태가 업데이트 되었습니다." 상태 메시지를 표시 하기 위한 레이블 컨트롤 이 컨트롤의 이름을 `StatusMessage`아웃 지우기, 해당 `Text` 속성 집합과 해당 `CssClass` 속성을 `Important`합니다. (의 `Important` 에 정의 된 CSS 클래스는 `Styles.css` 스타일 시트 파일 큰 빨간색 글꼴로 해당 텍스트를 표시 합니다.)

이러한 컨트롤을 추가한 다음 스크린샷과 그림 2에서 Visual Studio의 디자인 뷰에서 비슷해야 합니다.


[![UserInformation.aspx에 대 한 사용자 인터페이스 만들기](unlocking-and-approving-user-accounts-cs/_static/image5.png)](unlocking-and-approving-user-accounts-cs/_static/image4.png)

**그림 2**:에 대 한 사용자 인터페이스 만들기 `UserInformation.aspx` ([전체 크기 이미지를 보려면 클릭](unlocking-and-approving-user-accounts-cs/_static/image6.png))


설정 하는 다음 작업이 완료 사용자 인터페이스는 `IsApproved` 확인란 및 다른 컨트롤을 선택한 사용자의 정보에 기반 합니다. 페이지의에 대 한 이벤트 처리기를 만들고 `Load` 이벤트를 다음 코드를 추가 합니다.

[!code-csharp[Main](unlocking-and-approving-user-accounts-cs/samples/sample1.cs)]

위의 코드 페이지와 이후 다시 게시 하지를 처음 방문할 인지 확인 하 여 시작 합니다. 그런 다음을 통해 전달 되는 사용자를 읽어는 `user` querystring 필드를 통해 해당 사용자 계정에 대 한 정보를 검색 하 고는 `Membership.GetUser(username)` 메서드. 사용자는 쿼리 문자열을 통해 제공 된 경우 지정된 된 사용자를 찾을 수 없습니다, 하는 경우 관리자에 게 다시 보냅니다는 `ManageUsers.aspx` 페이지.

`MembershipUser` 개체의 `UserName` 값은 다음에 표시 되는 `UserNameLabel` 및 `IsApproved` 확인란에 따라는 `IsApproved` 속성 값입니다.

`MembershipUser` 개체의 [ `LastLockoutDate` 속성](https://msdn.microsoft.com/library/system.web.security.membershipuser.lastlockoutdate.aspx) 반환는 `DateTime` 잠겼습니다 사용자가 마지막를 나타내는 값입니다. 사용자가 되지 잠긴, 하는 경우 반환 되는 값에는 멤버 자격 공급자에 따라 다릅니다. 새 계정을 만든 경우의 `SqlMembershipProvider` 설정는 `aspnet_Membership` 테이블의 `LastLockoutDate` 필드를 `1754-01-01 12:00:00 AM`합니다. 위의 코드에 빈 문자열을 표시 합니다.는 `LastLockoutDateLabel` 경우는 `LastLockoutDate` 속성이 발생 해 전에 고, 그렇지 않으면 2000의 날짜 부분은 `LastLockoutDate` 레이블의에 속성이 표시 됩니다. `UnlockUserButton'` s `Enabled` 속성이 사용자의 잠긴 상태, 즉 사용자 잠겨 있으면이 단추가 활성화만 됩니다.

테스트 하는 `UserInformation.aspx` 브라우저를 통해 페이지입니다. 시작 해야 물론, 합니다, `ManageUsers.aspx` 하 고 관리 하려면 사용자 계정을 선택 합니다. 에 도착 시 `UserInformation.aspx`는 `IsApproved` 확인란은 사용자 승인 된 경우에 확인 됩니다. 사용자가 계속 잠긴, 날짜 잠겨 마지막으로 표시 됩니다. 사용자 잠금 해제 단추는 사용자가 현재 잠겨 있는 경우에 활성화 됩니다. 선택 하거나 선택을 취소는 `IsApproved` 확인란을 선택 하거나 사용자의 잠금을 해제 단추를 클릭 하는 포스트백이 발생 하지만 아직를 이유임 때문에 사용자 계정에 없는 수정 내용이 이러한 이벤트에 대 한 이벤트 처리기를 만듭니다.

에 대 한 이벤트 처리기를 만들고 Visual Studio로 되돌아가려면는 `IsApproved` 확인란의 `CheckedChanged` 이벤트 및 `UnlockUser` 단추의 `Click` 이벤트입니다. 에 `CheckedChanged` 이벤트 처리기는 사용자의 설정 `IsApproved` 속성을는 `Checked` 속성 확인란을 선택한 다음 호출을 통해 변경 내용을 저장할 `Membership.UpdateUser`합니다. 에 `Click` 이벤트 처리기를 호출 하기만 하면는 `MembershipUser` 개체의 `UnlockUser` 메서드. 두 이벤트 처리기에서에 적합 한 메시지를 표시는 `StatusMessage` 레이블.

[!code-csharp[Main](unlocking-and-approving-user-accounts-cs/samples/sample2.cs)]

### <a name="testing-theuserinformationaspxpage"></a>테스트는`UserInformation.aspx`페이지

이러한 이벤트 처리기 위치에서 페이지를 다시 확인 및 승인 되지 않은 사용자입니다. 그림 3과 같이 표시 되어야 하는지 여부를 나타내는 페이지에서 사용자의 메시지 간단한 `IsApproved` 속성 성공적으로 수정 합니다.


[![Chris 승인 되었습니다.](unlocking-and-approving-user-accounts-cs/_static/image8.png)](unlocking-and-approving-user-accounts-cs/_static/image7.png)

**그림 3**: Chris 승인 되었습니다 ([전체 크기 이미지를 보려면 클릭](unlocking-and-approving-user-accounts-cs/_static/image9.png))


다음으로 로그 아웃 및 계정을 가진 사용자로 로그인 하십시오에서 방금 승인 없습니다. 사용자 승인 되지 않은 때문에 로그인 할 수 없는 합니다. 기본적으로 Login 컨트롤 어떤 이유로 든 사용자 로그인 할 수 없는 경우 동일한 메시지를 표시 합니다. 하지만 <a id="Tutorial6"> </a> [ *유효성 검사 사용자 자격 증명에 대 한 멤버 자격 사용자 스토어* ](../membership/validating-user-credentials-against-the-membership-user-store-cs.md) 자습서 더 적절 한 메시지를 표시 하려면 Login 컨트롤 향상 살펴보았습니다. 그림 4에서 볼 수 있듯이 Chris 자신의 계정을 아직 승인 되지 않은 때문에 로그인 할 수 없는 그 설명 하는 메시지가 표시 됩니다.


[![Chris 없습니다 로그인 하기 때문에 His 계정이 인지 승인 안 됨](unlocking-and-approving-user-accounts-cs/_static/image11.png)](unlocking-and-approving-user-accounts-cs/_static/image10.png)

**그림 4**: Chris 없습니다 로그인 하기 때문에 His 계정이 인지 승인 되지 않은 ([전체 크기 이미지를 보려면 클릭](unlocking-and-approving-user-accounts-cs/_static/image12.png))


잠금된 기능을 테스트 하려면는 승인 된 사용자로 로그인 하지만 잘못 된 암호를 사용 하려고 합니다. 필요한 횟수 사용자 계정이 잠겼습니다 될 때까지이 프로세스를 반복 합니다. Login 컨트롤 사용자 지정 표시 하도록 업데이트 되었습니다 잠긴된 계정에서 로그인 하려고 하는 경우 메시지입니다. 계정이 잠겼습니다 로그인 페이지에 다음 메시지가 표시 되는 시작 되 면 알고: "계정 잠겼습니다 시도 횟수가 너무 많아서 잘못 된 로그인. 관리자 계정 잠금 해제에 연락 하세요. "

으로 돌아와서는 `ManageUsers.aspx` 페이지 하 고 잠긴된 사용자에 대 한 관리 링크를 클릭 합니다. 에 값이를 표시 해야 그림 5에서 볼 수 있듯이 `LastLockedOutDateLabel` 사용자 잠금 해제 단추를 사용 해야 합니다. 사용자 계정의 잠금을 해제 하려면 사용자의 잠금을 해제 단추를 클릭 합니다. 사용자, 잠금을 해제 한 후 다시 로그인 할 수 없게 됩니다.


[![시스템에서 잠긴 Dave](unlocking-and-approving-user-accounts-cs/_static/image14.png)](unlocking-and-approving-user-accounts-cs/_static/image13.png)

**그림 5**: Dave가 되었습니다 잠긴의 시스템 ([전체 크기 이미지를 보려면 클릭](unlocking-and-approving-user-accounts-cs/_static/image15.png))


## <a name="step-2-specifying-new-users-approved-status"></a>2 단계: 새 사용자 지정 상태를 승인

승인 된 상태는 일부 작업을 새 사용자가 로그인 하 고 사이트의 사용자 특정 기능에 액세스할 수 있기 전에 수행 하도록 하려는 시나리오에서 유용 합니다. 예를 들어 개인 웹 사이트를 등록 및 로그인 페이지를 제외한 모든 페이지 인증 된 사용자만 액세스할 수 있는 실행 수 있습니다. 하지만 등록 페이지를 찾아가 계정을 만들고 모르는 웹 사이트에 도달 하면 어떻게 되나요? 이 상황이 발생 하지 않도록 등록 페이지를 이동할 수 있습니다는 `Administration` 폴더를 관리자가 수동으로 각 계정을 만들 필요 합니다. 또는 모든 사람이 등록 하도록 허용 하지만 사용자 계정 관리자가 승인할 때까지 사이트 액세스 금지 수 있습니다.

기본적으로 CreateUserWizard 컨트롤에 새 계정을 승인 합니다. 컨트롤의를 사용 하 여이 동작을 구성할 수 있습니다 [ `DisableCreatedUser` 속성](https://msdn.microsoft.com/en-gb/library/system.web.ui.webcontrols.createuserwizard.disablecreateduser.aspx)합니다. 이 속성을 설정 `true` 새 사용자 계정을 승인 하지 않습니다.

> [!NOTE]
> 기본적으로 CreateUserWizard 컨트롤을 자동으로 새 사용자 계정에 기록합니다. 이 동작은 컨트롤의 명령을 받습니다 [ `LoginCreatedUser` 속성](https://msdn.microsoft.com/en-gb/library/system.web.ui.webcontrols.createuserwizard.logincreateduser.aspx)합니다. 승인 되지 않은 사용자가 사이트에 로그인 하기 때문에 때 `DisableCreatedUser` 은 `true` 의 값에 관계 없이 사이트에 새 사용자 계정을 기록 되지 않습니다는 `LoginCreatedUser` 속성입니다.


통해 새 사용자 계정을 프로그래밍 방식으로 만들려는 경우에 `Membership.CreateUser` 메서드 승인 되지 않은 사용자 계정을 만들려면 새 사용자를 받아들이는 오버 로드 중 하나를 사용 합니다. `IsApproved` 입력된 매개 변수로 속성 값입니다.

## <a name="step-3-approving-users-by-verifying-their-email-address"></a>3 단계: 전자 메일 주소를 확인 하 여 사용자가 승인

사용자 계정을 지 원하는 많은 웹 사이트를 등록할 때 제공 된 전자 메일 주소를 확인할 때까지 새 사용자를 승인 하지 마십시오. 이 확인 프로세스는 대개 봇, 스팸 메일 및 기타 ne'er-do-wells 차단 하는 고유 하 고 확인 된 전자 메일 주소가 필요 하 고 등록 프로세스에는 추가 단계를 추가 합니다. 이 모델을 새 사용자가 등록할 때 전송 됩니다 확인 페이지에 대 한 링크를 포함 하는 전자 메일 메시지. 링크를 방문 하 여 사용자 전자 메일 받은 이며 있는지, 따라서 제공 된 전자 메일 주소는 유효한 입증 합니다. 확인 페이지는 사용자 승인 하는 일을 담당 합니다. 이 발생할 수 있습니다 자동으로 하므로 모든 사용자가이 페이지에 도달 하면 승인 또는 사용자와 같은 몇 가지 추가 정보를 제공 하는 후에는 [CAPTCHA](http://en.wikipedia.org/wiki/Captcha)합니다.

이 워크플로 수용할 수 있도록 새 사용자가 승인 되지 않도록 먼저 계정 만들기 페이지를 업데이트 해야 합니다. 열기는 `EnhancedCreateUserWizard.aspx` 페이지에 `Membership` 폴더 집합과 CreateUserWizard 컨트롤의 `DisableCreatedUser` 속성을 `true`합니다.

다음으로, 해당 계정을 확인 하는 방법에 대 한 지침이 포함 된 새 사용자에 게 전자 메일을 보내는 CreateUserWizard 컨트롤을 구성 해야 합니다. 링크는 메일에 포함 됩니다는 특히는 `Verification.aspx` 페이지 (에 아직 이유임 있는 만들기)을 새 사용자의 전달 `UserId` querystring을 통해. `Verification.aspx` 페이지 지정된 된 사용자를 조회 하 고 승인 된 것으로 표시 됩니다.

### <a name="sending-a-verification-email-to-new-users"></a>새 사용자에 게 확인 전자 메일 보내기

CreateUserWizard 컨트롤에서 전자 메일을 보내려면 구성 해당 `MailDefinition` 속성 적절 하 게 합니다. 에 설명 된 대로 <a id="Tutorial13"> </a> [이전 자습서](recovering-and-changing-passwords-cs.md), ChangePassword 및 PasswordRecovery 컨트롤에는 한 [ `MailDefinition` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.maildefinition.aspx) 같은 방식으로 작동 하는 CreateUserWizard 컨트롤의 합니다.

> [!NOTE]
> 사용 하 여 `MailDefinition` 메일 배달 지정 해야 하는 속성의 옵션 `Web.config`합니다. 자세한 내용은를 참조 [ASP.NET에서 전자 메일 보내기](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)합니다.


라는 이름의 새 전자 메일 템플릿을 만들어 시작 `CreateUserWizard.txt` 에 `EmailTemplates` 폴더입니다. 서식 파일에 다음 텍스트를 사용 합니다.

[!code-aspx[Main](unlocking-and-approving-user-accounts-cs/samples/sample3.aspx)]

설정의 `MailDefinition'` s `BodyFileName` 속성을 "~ / EmailTemplates/CreateUserWizard.txt" 및 해당 `Subject` 속성을 "내 웹 사이트를 시작! 계정 활성화 하십시오. "

`CreateUserWizard.txt` 전자 메일 템플릿을 포함 한 `<%VerificationUrl%>` 자리 표시자입니다. 여기에에 대 한 URL의 `Verification.aspx` 페이지에 표시 됩니다. CreateUserWizard 자동으로 대체는 `<%UserName%>` 및 `<%Password%>` 자리 표시자를로 새 계정의 사용자 이름과 암호를 기본 제공 되지 않습니다 이지만 `<%VerificationUrl%>` 자리 표시자입니다. 수동으로 적절 한 확인 URL로 대체 해야 합니다.

CreateUserWizard의에 대 한 이벤트 처리기를 만들고이를 위해 [ `SendingMail` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.sendingmail.aspx) 다음 코드를 추가 합니다.

[!code-csharp[Main](unlocking-and-approving-user-accounts-cs/samples/sample4.cs)]

`SendingMail` 이벤트가 발생 한 후의 `CreatedUser` 이벤트의 경우에 새 사용자를 실행 하는 위의 이벤트 처리기에서 계정을 이미 만들어졌음을 의미 합니다. 새 사용자에 액세스할 수 있습니다 `UserId` 호출 하 여 값의 `Membership.GetUser` 전달 하는 메서드는 `UserName` CreateUserWizard 컨트롤에 입력 합니다. 다음으로 확인 URL 형성 됩니다. 문이 `Request.Url.GetLeftPart(UriPartial.Authority)` 반환 된 `http://yourserver.com` ; URL의 부분 `Request.ApplicationPath` 반환 경로 응용 프로그램 루트의 위치입니다. URL은 다음으로 정의 된 확인 `Verification.aspx?ID=userId`합니다. 이러한 두 문자열의 전체 URL을 구성 하기 위해 다음 연결 됩니다. 마지막으로 전자 메일 메시지 본문 (`e.Message.Body`)의 모든 발생 수가 `<%VerificationUrl%>` 전체 URL로 대체 합니다.

한 순수 효과 새 사용자 되지 않는다는 승인 된, 즉 사이트에 로그인 할 수 없습니다. 또한 자동으로 전송 됩니다 한 링크가 있는 전자 메일 확인 URL (그림 6 참조).


[![새 사용자에 게 전자 메일을 확인 URL에 대 한 링크](unlocking-and-approving-user-accounts-cs/_static/image17.png)](unlocking-and-approving-user-accounts-cs/_static/image16.png)

**그림 6**: 새 사용자에 게 전자 메일을 확인 URL에 대 한 링크 ([전체 크기 이미지를 보려면 클릭](unlocking-and-approving-user-accounts-cs/_static/image18.png))


> [!NOTE]
> CreateUserWizard 컨트롤의 기본 CreateUserWizard 단계 계정으로 만든 하 고 계속 단추를 표시할 사용자에 게 알리는 메시지가 표시 됩니다. 컨트롤의 지정 된 URL로 이동이 아이콘을 클릭 `ContinueDestinationPageUrl` 속성입니다. CreateUserWizard `EnhancedCreateUserWizard.aspx` 사용자에 게 보내도록 구성는 `~/Membership/AdditionalUserInfo.aspx`, 사용자에 게 자신의 출신지, 홈 페이지 URL 및 서명 확인 메시지를 표시 합니다. 이 정보만 추가할 수 있으므로 하 여 로그온 한 사용자는를 업데이트 하려면이 속성을 사용자에 게 사이트의 홈 페이지에 다시 보낼 것이 좋습니다 (`~/Default.aspx`). 또한는 `EnhancedCreateUserWizard.aspx` 페이지나 CreateUserWizard 단계 사용자 게 확인 전자 메일이 전송 된 계정으로이 전자 메일의 지침에 따라 될 때까지 활성화 되지 않습니다 보강 되어야 합니다. I 이러한 수정 사항은 판독기에 대 한 연습으로 둡니다.


### <a name="creating-the-verification-page"></a>확인 페이지 만들기

우리의 마지막 작업을 만드는 것은 `Verification.aspx` 페이지. 이 페이지를 사용 하 여 연결 루트 폴더에 추가 `Site.master` 마스터 페이지입니다. 대부분의 사이트에 추가 하 여 이전 콘텐츠 페이지 함께 수행한 대로 참조 하는 콘텐츠 컨트롤을 제거는 `LoginContent` ContentPlaceHolder 콘텐츠 페이지에서 마스터 페이지의 사용 되도록 기본 콘텐츠입니다.

Label 웹 컨트롤을 추가 `Verification.aspx` 페이지에서 설정 해당 `ID` 를 `StatusMessage` 아웃 text 속성의 선택을 취소 합니다. 다음으로 만듭니다는 `Page_Load` 이벤트 처리기를 다음 코드를 추가 합니다.

[!code-csharp[Main](unlocking-and-approving-user-accounts-cs/samples/sample5.cs)]

위의 코드의 대부분을 확인 하는 `UserId` querystring 있는지, 유효한 인지를 통해 제공 된 `Guid` 값 및 기존 사용자 계정을 참조 하는 것입니다. 이러한 모든 검사를 통과 하는 경우 사용자 계정 승인 된; 그렇지 않으면 적절 한 상태 메시지가 표시 됩니다.

그림 7은는 `Verification.aspx` 브라우저를 통해 방문 페이지입니다.


[![새 사용자의 계정이 이제 승인입니다.](unlocking-and-approving-user-accounts-cs/_static/image20.png)](unlocking-and-approving-user-accounts-cs/_static/image19.png)

**그림 7**: The 새 사용자 계정이 이제 승인 ([전체 크기 이미지를 보려면 클릭](unlocking-and-approving-user-accounts-cs/_static/image21.png))


## <a name="summary"></a>요약

모든 멤버 자격 사용자 계정이 있는 사용자는 사이트에 로그인 할 수 있는지 여부를 결정 하는 두 개의 상태: `IsLockedOut` 및 `IsApproved`합니다. 이러한 두 속성이 있어야 `true` 로그인에 사용자에 대 한 합니다.

사용자의 잠긴 상태 무작위 메서드를 통해 사이트를 분리 하는 해커의 가능성을 줄이기 위해 보안 조치로 사용 됩니다. 특히 사용자가 특정 기간 내에 잘못 된 로그인 시도의 특정 수 없으면 잠겨 있습니다. 이 경계에 멤버 자격 공급자 설정을 통해 구성할 수는 `Web.config`합니다.

승인 된 상태 일반적으로 새 사용자가 특별 한 조치 적용 될 때까지 로그인 하지 못하도록 하는 방법으로 사용 됩니다. 사이트는 새 계정을 먼저 승인 하도록 관리자가 필요 아마도 또는 전자 메일 주소를 확인 하 여 3 단계에서에서 설명한 것 처럼 합니다.

만족도 매우 프로그래밍!

### <a name="about-the-author"></a>작성자 정보

여러 ASP/ASP.NET 책의 작성자 및 4GuysFromRolla.com의 창립자 Scott Mitchell의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은  *[Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 합니다. Scott에 도달할 수 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 또는에서 그의 블로그 통해 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특히 감사 드립니다.

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](recovering-and-changing-passwords-cs.md)
> [다음](building-an-interface-to-select-one-user-account-from-many-vb.md)
