---
uid: web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-vb
title: 많은 (VB)에서 사용자 계정 하나를 선택 하는 인터페이스 빌드 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 페이징, 필터링 가능 표를 사용 하 여 사용자 인터페이스를 빌드합니다. 특히 사용자 인터페이스에 대 한 Linkbutton의 일련의 구성 됩니다...
ms.author: aspnetcontent
ms.date: 04/01/2008
ms.assetid: da53380c-a16b-41c7-a20d-24343c735c52
msc.legacyurl: /web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-vb
msc.type: authoredcontent
ms.openlocfilehash: af2a9692e03f147dfc1389f8c13b7d4fd758d62e
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37803259"
---
<a name="building-an-interface-to-select-one-user-account-from-many-vb"></a>많은 (VB)에서 사용자 계정 하나를 선택 하는 인터페이스 빌드
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/VB.12.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial12_SelectUser_vb.pdf)

> 이 자습서에서는 페이징, 필터링 가능 표를 사용 하 여 사용자 인터페이스를 빌드합니다. 특히 사용자 인터페이스는 Linkbutton의 일련의 이름과 일치 하는 사용자를 표시 하는 GridView 컨트롤의 시작 문자를 기준으로 결과 필터링 하는 것에 대 한 구성 됩니다. GridView의 사용자 계정을 모두 나열 하 여 시작 하겠습니다. 그런 다음 3 단계에서에서 Linkbutton을 필터를 추가 합니다. 4 단계에서 필터링된 된 결과 페이징 살펴봅니다. -4 단계에서 생성 된 인터페이스를 특정 사용자 계정에 대 한 관리 작업을 수행 하는 이후 자습서에서 사용 됩니다.


## <a name="introduction"></a>소개

에 <a id="_msoanchor_1"> </a> [ *사용자에 게 역할 할당* ](../roles/assigning-roles-to-users-vb.md) 사용자를 선택 하 고 자신의 역할을 관리 하려면 관리자에 대 한 기본적인 인터페이스를 만든 자습서입니다. 특히 인터페이스의 모든 사용자가 드롭다운 목록을 사용 하 여 관리자를 제공 합니다. 이러한 인터페이스 있지만 개 정도의 사용자 계정, 하지만 수백 또는 수천 개의 계정 사용 하 여 사이트에 대 한 하기 어렵고 적합 합니다. 페이징, 필터링 가능 표는 대형 사용자 자료를 사용 하 여 웹 사이트에 대 한 더 적합 한 사용자 인터페이스입니다.

이 자습서에서는 이러한 사용자 인터페이스를 구축 됩니다. 특히 사용자 인터페이스는 Linkbutton의 일련의 이름과 일치 하는 사용자를 표시 하는 GridView 컨트롤의 시작 문자를 기준으로 결과 필터링 하는 것에 대 한 구성 됩니다. GridView의 사용자 계정을 모두 나열 하 여 시작 하겠습니다. 그런 다음 3 단계에서에서 Linkbutton을 필터를 추가 합니다. 4 단계에서 필터링된 된 결과 페이징 살펴봅니다. -4 단계에서 생성 된 인터페이스를 특정 사용자 계정에 대 한 관리 작업을 수행 하는 이후 자습서에서 사용 됩니다.

이제 시작 하겠습니다.

## <a name="step-1-adding-new-aspnet-pages"></a>1 단계: 새 ASP.NET 페이지 추가

이 자습서에는 다음 두 우리는 검색할 수 다양 한 관리 관련 기능 및 기능입니다. 일련의 항목에서는이 자습서 전체에서 검사를 구현 하려면 ASP.NET 페이지를 해야 합니다. 이러한 페이지를 만들고 사이트 맵을 업데이트 해 보겠습니다.

이라는 프로젝트에 새 폴더를 만들어 시작 `Administration`합니다. 다음으로 각 페이지를 사용 하 여 연결 폴더에 두 개의 새 ASP.NET 페이지를 추가 합니다 `Site.master` 마스터 페이지입니다. 페이지 이름을 지정 합니다.

- `ManageUsers.aspx`
- `UserInformation.aspx`

또한 웹 사이트의 루트 디렉터리에 두 페이지를 추가 합니다. `ChangePassword.aspx` 및 `RecoverPassword.aspx`합니다.

이러한 네 가지 페이지, 이때 있어야 마스터 페이지의 ContentPlaceHolders 마다 하나씩 두 개의 콘텐츠 컨트롤을: `MainContent` 고 `LoginContent`입니다.

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample1.aspx)]

에 대 한 마스터 페이지의 기본 태그를 표시 하려고를 `LoginContent` ContentPlaceHolder 이러한 페이지에 대 한 합니다. 따라서 선언적 태그를 제거 합니다 `Content2` 콘텐츠 컨트롤입니다. 이렇게 하면 페이지 태그 콘텐츠 컨트롤을 한 개만 있어야 합니다.

ASP.NET 페이지에 `Administration` 폴더는 사용자를 대상으로 전적으로 관리 합니다. 시스템에 관리자 역할을 추가한 합니다 <a id="_msoanchor_2"> </a> [ *만들기 및 관리 역할* ](../roles/creating-and-managing-roles-vb.md) 자습서;이 역할에 이러한 두 페이지에 대 한 액세스를 제한 합니다. 이를 위해 추가 `Web.config` 파일을 합니다 `Administration` 폴더 구성 및 해당 `<authorization>` 즐거운 관리자 역할의 사용자 및 다른 모든 사용자를 거부 하는 요소입니다.

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample2.xml)]

이 시점에서 프로젝트의 솔루션 탐색기 스크린 샷을 그림 1에 표시 된 것을 유사 합니다.


[![웹 사이트에 추가 된 4 개의 새 페이지와 Web.config 파일](building-an-interface-to-select-one-user-account-from-many-vb/_static/image2.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image1.png)

**그림 1**: 4 개의 새 페이지와 `Web.config` 웹 사이트에 추가 된 파일 ([클릭 하 여 큰 이미지 보기](building-an-interface-to-select-one-user-account-from-many-vb/_static/image3.png))


마지막으로, 사이트 맵 업데이트 (`Web.sitemap`)에 항목을 포함 하는 `ManageUsers.aspx` 페이지입니다. 추가 후 다음 XML을 `<siteMapNode>` 역할 자습서에 대 한 추가 했습니다.

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample3.xml)]

사이트 맵을 업데이트를 사용 하 여 브라우저를 통해 사이트를 방문 합니다. 그림 2에서 볼 수 있듯이 이제 왼쪽 탐색 관리 자습서에 대 한 항목이 포함 됩니다.


[![사용자 관리 이라는 노드를 포함 하는 사이트 맵](building-an-interface-to-select-one-user-account-from-many-vb/_static/image5.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image4.png)

**그림 2**: 사이트 맵 노드 라는 사용자 관리를 포함 ([큰 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image6.png))


## <a name="step-2-listing-all-user-accounts-in-a-gridview"></a>GridView의 모든 사용자 계정을 나열 하는 2 단계:

이 자습서에 대 한 최종 목표는 관리자로 관리 사용자 계정을 선택할 수는 페이징, 필터링 가능 표를 만드는 것입니다. 나열 하 여 시작 해 보겠습니다 *모든* GridView에는 사용자입니다. 완료 되 면 필터링 및 페이징 인터페이스 및 기능 추가 합니다.

열기를 `ManageUsers.aspx` 페이지에서 `Administration` 폴더 설정 GridView를 추가 하 고 해당 `ID` 에 `UserAccounts` 잠시 후에 사용자 계정 집합을 사용 하 여 GridView에 바인딩하는 코드를 작성 합니다 `Membership` 클래스의 `GetAllUsers` 메서드. 이전 자습서에서 설명 했 듯이 `GetAllUsers` 메서드가 반환 되는 `MembershipUserCollection` 개체 컬렉션인의 `MembershipUser` 개체입니다. 각 `MembershipUser` 컬렉션에 같은 속성을 포함 `UserName`를 `Email`, `IsApproved`등입니다.

GridView에 원하는 사용자 계정 정보를 표시 하기 위해 GridView의 설정 `AutoGenerateColumns` 속성을 false로 BoundFields에 대 한 추가 합니다 `UserName`를 `Email`, 및 `Comment` 속성과 CheckBoxFields에 대 한는 `IsApproved`, `IsLockedOut`, 및 `IsOnline` 속성입니다. 이 구성은 통해 컨트롤의 선언적 태그 또는 필드 대화 상자를 통해 적용할 수 있습니다. 그림 3 후 자동 생성 필드 확인란을 선택 했습니다 CheckBoxFields 고 BoundFields 추가 및 구성 된 대화 상자를 스크린샷 필드를 나타냅니다.


[![GridView에 세 개의 BoundFields 및 세 가지 CheckBoxFields 추가](building-an-interface-to-select-one-user-account-from-many-vb/_static/image8.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image7.png)

**그림 3**: 세 가지 BoundFields 추가 및 GridView에 세 개의 CheckBoxFields ([큰 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image9.png))


에 GridView를 구성한 후 선언적 태그는 다음과 유사한 지 확인 합니다.

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample4.aspx)]

다음으로, 사용자 계정을 GridView에 바인딩하는 코드를 작성 해야 합니다. 라는 메서드를 만듭니다 `BindUserAccounts` 이 작업을 수행 하 여 다음에서 호출 하 여 `Page_Load` 첫 번째 페이지 방문의 이벤트 처리기입니다.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample5.vb)]

시간을 내어 브라우저를 통해 페이지를 테스트 합니다. 그림 4에서 알 수 있듯이는 `UserAccounts` GridView 시스템의 사용자 이름, 전자 메일 주소 및 모든 사용자에 대 한 다른 관련 계정 정보를 나열 합니다.


[![GridView에 사용자 계정이 나열 됩니다.](building-an-interface-to-select-one-user-account-from-many-vb/_static/image11.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image10.png)

**그림 4**: GridView에는 사용자 계정이 표시 되는지 ([큰 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image12.png))


## <a name="step-3-filtering-the-results-by-the-first-letter-of-the-username"></a>3 단계: 사용자 이름의 첫 번째 문자로 결과 필터링

현재는 `UserAccounts` GridView를 보여 줍니다 *모든* 사용자 계정입니다. 수백 또는 수천 개의 사용자 계정 사용 하 여 웹 사이트의 경우 반드시 해당 사용자를 신속 하 게 표시 된 계정 줄이려면 수 있습니다. 이 페이지에 Linkbutton 필터링을 추가 하 여 수행할 수 있습니다. 페이지로 27 Linkbutton을 추가 해 보겠습니다: 알파벳의 각 문자에 대 한 하나의 LinkButton 함께 모든 이라는 하나입니다. 방문자가 모든 LinkButton을 클릭 하면 GridView 모든 사용자가 표시 됩니다. 특정 문자를 클릭 하면 사용자가 선택한 문자로 시작 하는 사용자에만 표시 됩니다.

우리의 첫 번째 작업 27 LinkButton 컨트롤을 추가 하는 것입니다. 옵션 중 하나를 27 Linkbutton을 선언적으로 만드는 것 한 번에 하나씩 있습니다. 더 유연한 방법은 사용 하 여 Repeater 컨트롤을 사용 하는 `ItemTemplate` LinkButton을 렌더링 하 고 필터링 옵션으로 반복기에 바인딩됩니다는 `String` 배열입니다.

위의 페이지로 Repeater 컨트롤을 추가 하 여 시작 된 `UserAccounts` GridView입니다. 반복기의 설정 `ID` 속성을 `FilteringUI` 반복기의 템플릿 구성 되도록 해당 `ItemTemplate` LinkButton 렌더링입니다 `Text` 및 `CommandName` 속성이 현재 배열 요소에 바인딩됩니다. 설명한 것 처럼 합니다 <a id="_msoanchor_3"> </a> [ *사용자에 게 역할 할당* ](../roles/assigning-roles-to-users-vb.md) 자습서를 사용 하 여 수행할 수 있습니다는 `Container.DataItem` 데이터 바인딩 구문을 합니다. 반복기를 사용 하 여 `SeparatorTemplate` 각 링크 간에 수직선을 표시 합니다.

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample6.aspx)]

원하는 필터링 옵션을 사용 하 여이 Repeater를 채우기 위해 라는 메서드를 만듭니다 `BindFilteringUI`합니다. 이 메서드를 호출 하는 `Page_Load` 이벤트 처리기의 첫 페이지를 로드 합니다.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample7.vb)]

요소로 필터링 옵션을 지정 하는이 메서드는 `String` 배열 `filterOptions` 반복기가 인 LinkButton을 렌더링 하는 데 배열의 각 요소에 대해 해당 `Text` 및 `CommandName` 배열의 값으로 할당 된 속성 요소입니다.

그림 5는 `ManageUsers.aspx` 브라우저를 통해 볼 때 페이지입니다.


[![Repeater 27 필터링 Linkbutton 나열](building-an-interface-to-select-one-user-account-from-many-vb/_static/image14.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image13.png)

**그림 5**: The Repeater 나열 27 필터링 Linkbutton ([큰 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image15.png))


> [!NOTE]
> 사용자는 모든 문자, 숫자 및 문장 부호를 포함 하 여 시작할 수 있습니다. 이러한 계정은 보려면 관리자가 모든 LinkButton 옵션을 사용 해야 합니다. 또는 숫자로 시작 하는 모든 사용자 계정을 반환 하는 LinkButton을 추가할 수 있습니다. 필자는 판독기에 대 한 연습으로 둡니다.


포스트백을 발생 시키는 필터링 Linkbutton을 클릭 하 고 반복기의 발생 `ItemCommand` 이벤트를 아직 했습니다 때문에 표에 변하지 않습니다 하지만 결과 필터링 하는 코드를 작성 합니다. `Membership` 클래스에 포함 된 [ `FindUsersByName` 메서드](https://technet.microsoft.com/library/system.web.security.membership.findusersbyname.aspx) 사용자 지정 된 검색 패턴과 일치 하는 해당 사용자 계정을 반환 하는. 이 메서드 해당 사용자 이름 문자로 시작 하 여 지정 된 해당 사용자 계정을 검색 하려면 사용할 수 있습니다는 `CommandName` 클릭 된 필터링 된 LinkButton의 합니다.

업데이트 하 여 시작 합니다 `ManageUser.aspx` 라는 속성이 포함 되도록 페이지의 코드 숨김 클래스 `UsernameToMatch` 이 속성이 다시 게시할 때마다 사용자 이름 필터 문자열을 유지 합니다.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample8.vb)]

합니다 `UsernameToMatch` 속성에 할당 된 값을 저장 합니다 `ViewState` UsernameToMatch 키를 사용 하 여 컬렉션입니다. 값의 존재 여부를 확인 하는이 속성의이 값을 읽을 때의 `ViewState` 컬렉션 그렇지 않은 경우 해당 기본값인 빈 문자열을 반환 합니다. `UsernameToMatch` 속성은 namely를 뷰 상태 변경 내용을 속성에는 포스트백 간에 지속 되도록 값을 유지 하는 일반적인 패턴을 나타냅니다. 이 패턴에 대 한 자세한 내용은 읽을 [이해 ASP.NET 뷰 상태](https://msdn.microsoftn-us/library/ms972976.aspx)합니다.

다음으로 업데이트 하는 `BindUserAccounts` 메서드 호출의 `Membership.GetAllUsers`, 호출 `Membership.FindUsersByName`값에 전달 합니다 `UsernameToMatch` SQL 와일드 카드 문자를 사용 하 여 추가 속성 %입니다.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample9.vb)]

사용자 A로 시작 하는 해당 사용자를 표시 하려면 설정 합니다 `UsernameToMatch` 속성을 다음 호출 `BindUserAccounts` 이에 대 한 호출 결과로 `Membership.FindUsersByName("A%")`, 를반환하려면1.마찬가지로,를사용하여시작반환하는모든사용자에게사용자*모든* 사용자를 할당 하는 빈 문자열을 `UsernameToMatch` 속성 있도록를 `BindUserAccounts` 메서드는 호출 `Membership.FindUsersByName("%")`시켜 모든 사용자 계정을 반환 합니다.

반복기의에 대 한 이벤트 처리기를 만들고 `ItemCommand` 이벤트입니다. 이 이벤트는 Linkbutton 필터 중 하나를 클릭 합니다. 클릭할된 LinkButton의 전달 된 `CommandName` 를 통해 값을 `RepeaterCommandEventArgs` 개체입니다. 적절 한 값을 할당 해야 합니다 `UsernameToMatch` 속성과 호출 합니다 `BindUserAccounts` 메서드. 경우는 `CommandName` 은 All 이며, 빈 문자열을 할당 `UsernameToMatch` 모든 사용자 계정이 표시 되도록 합니다. 그렇지 않은 경우, 할당 된 `CommandName` 값 `UsernameToMatch`

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample10.vb)]

이 코드를 사용 하 여 필터링 기능을 테스트 합니다. 페이지를 방문 하는 먼저 모든 사용자 계정이 표시 됩니다 (그림 5를 다시 참조). LinkButton을 클릭 하면 포스트백을 발생 시키는 및 A로 시작 하는 사용자 계정 으로만 표시 된 결과 필터링 합니다.


[![필터링 Linkbutton을 사용 하 여 사용자가 특정 문자로 시작 하는 해당 사용자를 표시 합니다.](building-an-interface-to-select-one-user-account-from-many-vb/_static/image17.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image16.png)

**그림 6**: 필터링 Linkbutton을 사용 하 여 해당 사용자가 있는 사용자 이름이 특정 문자로 시작 표시 ([큰 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image18.png))


## <a name="step-4-updating-the-gridview-to-use-paging"></a>4 단계: 업데이트 페이징을 사용 하 여 GridView

그림 5와 6에 표시 된 GridView에서 반환 된 레코드의 모든를 나열 합니다 `FindUsersByName` 메서드. 수백 또는 수천 개의 사용자 계정이 있는 경우 (마찬가지로 모든 LinkButton을 클릭 합니다. 또는 처음에 페이지를 방문 하는 경우) 모든 계정을 볼 때 정보 과부하 문제를 발생할 수 있습니다이 있습니다. 사용자 계정을 관리 하기 쉽게 표시를 위해 10 개의 사용자 계정을 한 번에 표시할 GridView 구성 하겠습니다.

GridView 컨트롤에서는 두 가지 유형의 페이징 제공합니다.

- **기본 페이징은** -구현 하기 쉽고 하지만 비효율적입니다. 간단히 말해 GridView를 페이징 하는 기본값을 사용 하 여 예상 *모든* 해당 데이터 원본에서 레코드입니다. 그런 다음만 페이지를 표시할 적절 한 레코드입니다.
- **사용자 지정 페이징을** -를 구현 하는 데 필요한 작업이 더 기본 페이징 원본 데이터를 페이징 하는 사용자 지정을 사용 하 여 정확 하 게 표시할 레코드 집합만 반환 하기 때문에 보다 더 효율적 이지만 합니다.

수천 개의 레코드를 통해 페이징 하는 경우 기본 및 사용자 지정 페이징의 성능 차이 매우 길 수 있습니다. 빌드하는 것 때문에 있다고 가정 하 고이 인터페이스 수 있으므로 수백 또는 수천 개의 사용자 계정에 사용자 지정 페이징을 사용 하겠습니다.

> [!NOTE]
> 사용자 지정 페이징을 구현에 관련 된 문제 뿐만 아니라 기본 및 사용자 지정 페이징을 간의 차이점에 자세한 내용은 참조 [효율적으로 페이징을 통해 많은 양의 데이터](https://asp.net/learn/data-access/tutorial-25-vb.aspx)입니다. 기본 및 사용자 지정 페이징의 성능 차이의 몇 가지 분석을 참조 하세요 [SQL Server 2005를 사용 하 여 ASP.NET에서 사용자 지정 페이징을](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)합니다.


사용자 지정 페이징을 구현 하려면 먼저 몇 가지 메커니즘을 GridView에 표시 되는 레코드의 정확한 하위 집합을 검색할 해야 합니다. 다행 스럽게도 하는 `Membership` 클래스의 `FindUsersByName` 메서드는 페이지 인덱스 및 페이지 크기를 지정할 수 있도록 하는 오버 로드가 있습니다 하 고 레코드 범위에 속하는 사용자 계정만 반환 합니다.

특히이 오버 로드에는 다음 서명을: [ `FindUsersByName(usernameToMatch, pageIndex, pageSize, totalRecords)` ](https://msdn.microsoft.com/library/fa5st8b2.aspx)합니다.

합니다 *pageIndex* 반환할; 사용자 계정 페이지를 지정 하는 매개 변수 *pageSize* 페이지당 표시할 레코드 수를 나타냅니다. 합니다 *totalRecords* 매개 변수는 한 `ByRef` 사용자 저장소의 총 사용자 계정 수를 반환 하는 매개 변수입니다.

> [!NOTE]
> 반환한 데이터 `FindUsersByName` username;는 정렬할 정렬 조건을 사용자 지정할 수 없습니다.


사용자 지정 페이징을 사용 하지만 경우에 바인딩할 ObjectDataSource 컨트롤을 GridView는 구성할 수 있습니다. 사용자 지정 페이징을 구현 하기가 ObjectDataSource 컨트롤, 필요한 두 가지 방법: 시작 하는 행 인덱스 및 레코드를 표시 하려면 최대 전달 되는 정확한; 해당 범위 내에 속하는 레코드 하위 집합을 반환 합니다 와 레코드의 총 수를 반환 하는 메서드를 통해 페이징 되 고 있습니다. 합니다 `FindUsersByName` 오버 로드 페이지 인덱스 및 페이지 크기를 받고을 통해 레코드의 총 수를 반환을 `ByRef` 매개 변수입니다. 따라서 인터페이스 불일치를 있습니다.

옵션 중 하나를 예상 하 고 내부적으로 호출 하는 ObjectDataSource 인터페이스를 노출 하는 프록시 클래스를 만드는 것은 `FindUsersByName` 메서드. 또 다른 옵션 및이 문서에 대 한 사용 하 여 하나-고유한 페이징 인터페이스를 만들어 GridView의 기본 제공 페이징 인터페이스 대신 사용 하는 것입니다.

### <a name="creating-a-first-previous-next-last-paging-interface"></a>먼저 만들기 이전 페이징 인터페이스를 다음으로, 마지막

첫 번째 "," 이전 "," 다음 "및" 마지막 Linkbutton을 사용 하 여 페이징 인터페이스를 빌드 해 보겠습니다. 첫 번째 LinkButton을 클릭 하면 이전은 그 이전 페이지로 반환 하는 반면 사용자 데이터의 첫 번째 페이지 걸립니다. 마찬가지로, 다음 및 마지막은 사용자의 다음 및 마지막 페이지에서 각각 이동 합니다. 아래에 네 가지 LinkButton 컨트롤을 추가 합니다 `UserAccounts` GridView입니다.

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample11.aspx)]

다음으로, 각 LinkButton의에 대 한 이벤트 처리기를 만들고 `Click` 이벤트입니다.

그림 7에서는 Visual Web Developer 디자인 뷰를 통해 볼 때 4 개의 Linkbutton을 보여 줍니다.


[![다음으로, 첫 번째, 이전, 추가 및 GridView 아래 Linkbutton 마지막](building-an-interface-to-select-one-user-account-from-many-vb/_static/image20.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image19.png)

**그림 7**: 첫 번째 추가, 이전, Next 및 GridView 아래에 있는 마지막 Linkbutton ([큰 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image21.png))


### <a name="keeping-track-of-the-current-page-index"></a>현재 페이지 인덱스의 추적

사용자를 처음으로 방문 합니다 `ManageUsers.aspx` 단추는 필터링에 대 한 페이지 또는 클릭을 GridView에서 데이터의 첫 번째 페이지를 표시 하려고 합니다. 그러나 사용자가 탐색 Linkbutton 중 하나를 클릭 하면 해야 페이지의 인덱스를 업데이트 합니다. 페이지 인덱스 및 한 페이지에 표시할 레코드 수를 유지 하려면 다음 두 속성을 페이지의 코드 숨김 클래스에 추가 합니다.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample12.vb)]

같은 합니다 `UsernameToMatch` 속성인은 `PageIndex` 속성이 뷰 상태에 해당 값을 유지 합니다. 읽기 전용 `PageSize` 속성 하드 코드 된 값을 10을 반환 합니다. 와 동일한 패턴을 사용 하도록이 속성을 업데이트 하려면 관심 있는 판독기를 초대한 `PageIndex`를 차례로 확장 하는 `ManageUsers.aspx` 페이지를 방문 하는 사용자 당 표시할 얼마나 많은 사용자 계정 페이지를 지정할 수 있도록 페이지입니다.

### <a name="retrieving-just-the-current-pages-records-updating-the-page-index-and-enabling-and-disabling-the-paging-interface-linkbuttons"></a>현재 페이지의 레코드만 검색, 페이지 인덱스를 업데이트, 사용 및 페이징 인터페이스 Linkbutton 사용 하지 않도록 설정

원위치에서 페이징 인터페이스를 사용 하 여 및 `PageIndex` 및 `PageSize` 속성 추가, 업데이트 준비가 합니다 `BindUserAccounts` 메서드를 사용 하 여 적절 한 `FindUsersByName` 오버 로드 합니다. 또한이 메서드를 사용 하도록 설정 또는 표시 되는 페이지에 따라 페이징 인터페이스를 사용 하지 않도록 설정 해야 합니다. 데이터의 첫 페이지를 볼 때 첫 번째 및 이전 링크 수 없게 됩니다. 마지막 페이지를 볼 때 다음 하 고 마지막으로 해제 되어야 합니다.

`BindUserAccounts` 메서드를 다음 코드로 업데이트합니다.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample13.vb)]

통해 페이징 되 고 레코드의 총 수의 마지막 매개 변수에 의해 결정 됩니다는 `FindUsersByName` 메서드. 사용자 계정의 지정된 된 페이지 반환 된 후 4 Linkbutton 중 하나를 사용, 데이터의 첫 번째 또는 마지막 페이지를 보고 하는지 여부에 따라 합니다.

마지막 단계는 4 개의 Linkbutton에 대 한 코드를 쓸 `Click` 이벤트 처리기입니다. 이러한 이벤트 처리기를 업데이트 해야 합니다.는 `PageIndex` 속성을 다음 호출을 통해 GridView에 데이터를 다시 바인딩해야 `BindUserAccounts` 의 첫 번째, 이전 및 다음 이벤트 처리기는 매우 간단 합니다. 그러나 `Click` 마지막 LinkButton에 대 한 이벤트 처리기 이므로 좀 더 복잡 레코드 개수는 마지막 페이지 인덱스를 확인 하기 위해 표시 되는 확인 해야 합니다.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample14.vb)]

그림 8과 9 작업에 사용자 지정 페이징 인터페이스를 표시합니다. 그림 8에 표시 된 `ManageUsers.aspx` 모든 사용자 계정에 대 한 데이터의 첫 페이지를 볼 때 페이지입니다. Note 13 계정의 10 표시 됩니다. 다음 또는 마지막 링크를 클릭 하면 포스트백에서 업데이트를 `PageIndex` 을 1로 사용자의 두 번째 페이지를 그리드로 계정을 바인딩합니다 (그림 9 참조).


[![첫 번째 10 사용자 계정이 표시 됩니다.](building-an-interface-to-select-one-user-account-from-many-vb/_static/image23.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image22.png)

**그림 8**:의 첫 번째 10 사용자 계정이 표시 됩니다 ([큰 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image24.png))


[![다음 링크를 클릭 하면 사용자 계정의 두 번째 페이지가 표시 됩니다.](building-an-interface-to-select-one-user-account-from-many-vb/_static/image26.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image25.png)

**그림 9**: 다음 링크를 클릭 하는 두 번째 페이지의 사용자 계정이 표시 됩니다 ([큰 이미지를 보려면 클릭](building-an-interface-to-select-one-user-account-from-many-vb/_static/image27.png))


## <a name="summary"></a>요약

관리자는 사용자 계정 목록에서 선택 해야 합니다. 이전 자습서에서 사용자, 채워진 드롭다운 목록을 사용 하 여 살펴보았습니다 있지만이 방법은 잘 확장 되지 않습니다. 이 자습서에서는 더 나은 방법은 살펴보았습니다:는 필터링 가능한 인터페이스 페이징된 GridView에 결과가 표시 됩니다. 이 사용자 인터페이스를 사용 하 여 관리자를 빠르고 효율적으로 찾은 후 수천 간에 사용자 계정 하나를 선택 합니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [SQL Server 2005 사용 하 여 ASP.NET에서 사용자 지정 페이징](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)
- [많은 양의 데이터를 효율적으로 페이징](https://asp.net/learn/data-access/tutorial-25-vb.aspx)
- [고유한 웹 사이트 관리 도구를 롤링합니다.](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)

### <a name="about-the-author"></a>저자 소개

Scott Mitchell, 여러 ASP/ASP.NET 책의 저자 이자 4GuysFromRolla.com의 설립자 이며 1998 Microsoft 웹 기술을 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는  *[Sams 설명 직접 ASP.NET 2.0 24 시간 동안의](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 합니다. Scott에 도달할 수 있습니다 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 통하거나 저자의 블로그 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Alicja Maziarz 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선

> [!div class="step-by-step"]
> [이전](unlocking-and-approving-user-accounts-cs.md)
> [다음](recovering-and-changing-passwords-vb.md)
