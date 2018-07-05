---
uid: web-forms/overview/older-versions-security/membership/storing-additional-user-information-vb
title: 추가 사용자 정보 (VB)를 저장 합니다. | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 매우 기본적인 방명록 응용 프로그램을 작성 하 여이 질문에 대답은 했습니다. 이 과정에서 살펴보겠습니다 modeli에 대 한 다른 옵션...
ms.author: aspnetcontent
ms.date: 01/18/2008
ms.assetid: ee4b924e-8002-4dc3-819f-695fca1ff867
msc.legacyurl: /web-forms/overview/older-versions-security/membership/storing-additional-user-information-vb
msc.type: authoredcontent
ms.openlocfilehash: 2ea731012f8c053d1e1eac293fdbeaec66db23bf
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37816040"
---
<a name="storing-additional-user-information-vb"></a>추가 사용자 정보 저장 (VB)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_08_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial08_ExtraUserInfo_vb.pdf)

> 이 자습서에서는 매우 기본적인 방명록 응용 프로그램을 작성 하 여이 질문에 대답은 했습니다. 이 과정에서 데이터베이스에서 사용자 정보를 모델링 하기 위한 다양 한 옵션을 살펴보고 하 고 멤버 자격 프레임 워크에 의해 생성 된 사용자 계정을 사용 하 여이 데이터를 연결 하는 방법을 참조 하세요.


## <a name="introduction"></a>소개

ASP 합니다. NET의 멤버 자격 프레임 워크는 사용자를 관리 하기 위한 유연한 인터페이스를 제공 합니다. 멤버 자격 API는 자격 증명 유효성 검사, 현재 로그온된 한 사용자에 대 한 정보를 검색, 새 사용자 계정을 만들고 삭제 하기 위한 다른 사용자 계정에는 메서드를 포함 합니다. 멤버 자격 프레임 워크에서 각 사용자 계정 자격 증명 유효성 검사 및 필수 사용자 계정 관련 작업 수행에 필요한 속성만 포함 합니다. 메서드 및 속성의 된 수치로 증명은이 [ `MembershipUser` 클래스](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)를 모델링 하는 멤버 자격 프레임 워크의 사용자 계정입니다. 이 클래스와 같은 속성이 [ `UserName` ](https://msdn.microsoft.com/library/system.web.security.membershipuser.username.aspx), [ `Email` ](https://msdn.microsoft.com/library/system.web.security.membershipuser.email.aspx), 및 [ `IsLockedOut` ](https://msdn.microsoft.com/library/system.web.security.membershipuser.islockedout.aspx), 및와 같은 메서드 [ `GetPassword` ](https://msdn.microsoft.com/library/system.web.security.membershipuser.getpassword.aspx) 하 고 [ `UnlockUser` ](https://msdn.microsoft.com/library/system.web.security.membershipuser.unlockuser.aspx)합니다.

종종 응용 프로그램 멤버 자격 프레임 워크에 없는 추가 사용자 정보를 저장 해야 합니다. 예를 들어, 온라인 소매점 각 사용자 게 배송 및 대금 청구 주소, 결제 정보 배달 기본 설정에 저장 하 고 연락처 전화 번호를 사용 해야 합니다. 또한 각 주문 시스템에 특정 사용자 계정과 관련이 있습니다.

합니다 `MembershipUser` 클래스와 같은 속성을 포함 하지 않습니다 `PhoneNumber` 하거나 `DeliveryPreferences` 또는 `PastOrders`합니다. 그렇다면 어떻게 수행 응용 프로그램에 필요한 사용자 정보를 추적 하 고 멤버 자격 프레임 워크와 통합 되 게? 이 자습서에서는 매우 기본적인 방명록 응용 프로그램을 작성 하 여이 질문에 대답은 했습니다. 이 과정에서 데이터베이스에서 사용자 정보를 모델링 하기 위한 다양 한 옵션을 살펴보고 하 고 멤버 자격 프레임 워크에 의해 생성 된 사용자 계정을 사용 하 여이 데이터를 연결 하는 방법을 참조 하세요. 이제 시작 하겠습니다.

## <a name="step-1-creating-the-guestbook-applications-data-model"></a>1 단계: 방명록 응용 프로그램의 데이터 모델 만들기

데이터베이스에서 사용자 정보를 캡처 및 멤버 자격 프레임 워크에 의해 생성 된 사용자 계정을 사용 하 여 연결 하는 데 사용할 수 있는 기술의 여러 가지가 있습니다. 이러한 기법을 보여 주기 위해 일종의 사용자 관련 데이터를 캡처할 수 있도록 자습서 웹 응용 프로그램을 확장 해야 합니다. (응용 프로그램의 데이터 모델에서 응용 프로그램에 필요한 테이블 서비스에을 포함 하는 현재는 `SqlMembershipProvider`.)

인증된 된 사용자 의견을 남겨 수 있는 매우 간단한 방명록 응용 프로그램을 만들어 보겠습니다. 방명록 주석을 저장 하는 것 외에도 자신의 홈 타운, 홈 페이지 및 서명을 저장 하는 각 사용자를 허용 해 보겠습니다. 사용자의 홈 도시별으로 제공 하는 경우 홈 페이지 및 서명 그는 방명록의 왼쪽에 각 메시지에 표시 됩니다.

### <a name="adding-theguestbookcommentstable"></a>추가 된`GuestbookComments`테이블

방명록 의견을 캡처하려면 라는 데이터베이스 테이블을 생성 해야 `GuestbookComments` 와 같은 열에 있는 `CommentId`를 `Subject`를 `Body`, 및 `CommentDate`합니다. 각 레코드에도 해야는 `GuestbookComments` 주석을 남긴 사용자 참조 테이블입니다.

이 테이블에 데이터베이스를 추가 하려면 Visual Studio에서 데이터베이스 탐색기로 이동 하 고 드릴 다운을 `SecurityTutorials` 데이터베이스입니다. 테이블 폴더 단추로 클릭 하 고 새 테이블 추가 선택 합니다. 그러면 새 테이블의 열을 정의할 수 있는 인터페이스입니다.


[![SecurityTutorials 데이터베이스에 새 테이블을 추가 합니다.](storing-additional-user-information-vb/_static/image2.png)](storing-additional-user-information-vb/_static/image1.png)

**그림 1**: 새 테이블을 추가 합니다 `SecurityTutorials` 데이터베이스 ([클릭 하 여 큰 이미지 보기](storing-additional-user-information-vb/_static/image3.png))


다음으로 정의 된 `GuestbookComments`의 열입니다. 명명 된 열을 추가 하 여 시작 `CommentId` 형식의 `uniqueidentifier`합니다. 이 열은 방명록에서 각 메모를 고유 하 게 식별을 허용 하므로 `NULL`의 테이블의 기본 키로 표시 합니다. 에 대 한 값을 제공 하는 대신 합니다 `CommentId` 각 필드 `INSERT`를 나타낼 수 있습니다 새 `uniqueidentifier` 에서이 필드에 대 한 값을 자동으로 생성할 수 해야 `INSERT` 열의 기본값을 설정 하 여 `NEWID()`. 이 첫 번째 필드를 기본값으로, primary key 및 설정으로 표시를 추가한 후 화면은 해야 스크린 샷을 그림 2에 표시 된 것과 유사 합니다.


[![CommentId 라는 기본 열 추가](storing-additional-user-information-vb/_static/image5.png)](storing-additional-user-information-vb/_static/image4.png)

**그림 2**: 명명 된 기본 열 추가 `CommentId` ([클릭 하 여 큰 이미지 보기](storing-additional-user-information-vb/_static/image6.png))


다음으로, 라는 열을 추가 `Subject` 형식의 `nvarchar(50)` 및 명명 된 열 `Body` 형식의 `nvarchar(MAX)`를 허용 하지 `NULL` 두 열 모두의 합니다. 그런 다음, 라는 열을 추가 `CommentDate` 형식의 `datetime`합니다. 허용 안 함 `NULL` 집합과 s 합니다 `CommentDate` 열의 기본 값을 `getdate()`합니다.

에 각 방명록 메모를 사용 하 여 사용자 계정에 연결 하는 열을 추가 합니다. 명명 된 열을 추가할 수 있습니다 `UserName` 형식의 `nvarchar(256)`합니다. 이외의 다른 멤버 자격 공급자를 사용 하는 경우이 적합 한 선택은 `SqlMembershipProvider`합니다. 하지만 사용 하는 경우는 `SqlMembershipProvider`처럼이 자습서 시리즈를를 `UserName` 열에는 `aspnet_Users` 테이블 고유성이 보장 되지 않습니다. 합니다 `aspnet_Users` 테이블의 기본 키는 `UserId` 형식인 `uniqueidentifier`합니다. 따라서 합니다 `GuestbookComments` 테이블에 열 이름이 필요 `UserId` 형식의 `uniqueidentifier` (허용 `NULL` 값). 계속 해 서이 열을 추가 합니다.

> [!NOTE]
> 설명한 대로 합니다 [ *SQL Server에서 멤버 자격 스키마 만들기* ](creating-the-membership-schema-in-sql-server-vb.md) 자습서, 멤버 자격 프레임 워크는 여러 웹 응용 프로그램을 다른 사용자 계정으로 동일한 공유 하도록 설계 되었습니다 사용자 저장소입니다. 다른 응용 프로그램에 사용자를 분할 하 여 수행 합니다. 및 각 사용자 이름을 응용 프로그램 내에서 고유 하 게 보장 하는 동안 동일한 사용자 이름을 같은 사용자 저장소를 사용 하 여 다른 응용 프로그램에서 사용할 수 있습니다. 복합 `UNIQUE` 의 제약 조건 합니다 `aspnet_Users` 테이블에 `UserName` 및 `ApplicationId` 필드 이지만의 하나가 아닙니다만 `UserName` 필드. 따라서 있기 aspnet\_Users 테이블 두 개 이상의 레코드가 동일한 `UserName` 값입니다. 그러나을 `UNIQUE` 제약 조건에는 `aspnet_Users` 테이블의 `UserId` (이므로 기본 키) 필드입니다. A `UNIQUE` 제약 조건은 없으면 간의 외래 키 제약 조건을 설정할 수 없습니다 것 때문에 중요 합니다 `GuestbookComments` 및 `aspnet_Users` 테이블.


추가한 후의 `UserId` 저장 도구 모음에서 저장 아이콘을 클릭 하 여 테이블 열입니다. 새 테이블의 이름을 `GuestbookComments`입니다.

마지막 한 가지 문제를 사용 하 여 참가 했습니다 합니다 `GuestbookComments` 테이블: 만들어야를 [foreign key 제약 조건을](https://msdn.microsoft.com/library/ms175464.aspx) 간에 `GuestbookComments.UserId` 열 및 `aspnet_Users.UserId` 열. 이렇게 하려면 외래 키 관계 대화 상자를 시작 하려면 도구 모음에서 관계 아이콘을 클릭 합니다. (또는 시작할 수 있습니다이 대화 상자는 테이블 디자이너 메뉴로 이동 하 고 관계를 선택 하 여.)

외래 키 관계 대화 상자의 왼쪽된 아래 모서리에 있는 추가 단추를 클릭 합니다. 이렇게 하면 여전히 관계에 참여 하는 테이블을 정의 해야 하지만 새 외래 키 제약 조건을 추가 됩니다.


[![테이블의 외래 키 제약 조건을 관리 하는 외래 키 관계 대화 상자를 사용 합니다.](storing-additional-user-information-vb/_static/image8.png)](storing-additional-user-information-vb/_static/image7.png)

**그림 3**: 테이블의 외래 키 제약 조건을 관리 하는 외래 키 관계 대화 상자를 사용 하 여 ([큰 이미지를 보려면 클릭](storing-additional-user-information-vb/_static/image9.png))


다음으로 오른쪽에 있는 "테이블 및 열 사양" 행에 있는 줄임표 아이콘을 클릭 합니다. 이 테이블 및 열 대화 상자를 시작를 지정할 수 있습니다 기본 키 테이블 및 열에서 외래 키 열을 `GuestbookComments` 테이블입니다. 특히 선택 `aspnet_Users` 하 고 `UserId` 기본 키 테이블 및 열 및 `UserId` 에서 `GuestbookComments` 외래 키 열으로 테이블 (그림 4 참조). 기본 및 외래 키 테이블 및 열을 정의한 후 확인을 클릭 하 여 외래 키 관계 대화 상자로 돌아갑니다.


[![외래 키 제약 조건 간에 aspnet_Users 및 GuesbookComments 테이블 설정](storing-additional-user-information-vb/_static/image11.png)](storing-additional-user-information-vb/_static/image10.png)

**그림 4**:는 외래 키 제약 조건 간에 설정 된 `aspnet_Users` 하 고 `GuesbookComments` 테이블 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-vb/_static/image12.png))


이 시점에서 외래 키 제약 조건이 설정 되었습니다. 이 제약 조건의 제공 되므로 [관계 무결성](http://en.wikipedia.org/wiki/Referential_integrity) 는 될 수 없으므로 존재 하지 않는 사용자 계정에 참조 방명록 항목을 보장 하 여 두 테이블 사이입니다. 기본적으로 외래 키 제약 조건을 자식 레코드 해당 하는 경우 삭제할 부모 레코드를 허용 하지 것입니다 됩니다. 즉, 사용자가 하나 이상의 방명록 설명 하는 경우 해당 사용자 계정을 삭제 하려고 하면 다음에 자신의 방명록 의견을 먼저 삭제 됩니다 않으면 삭제가 실패 합니다.

부모 레코드가 삭제 될 때 자동으로 연결 된 자식 레코드를 삭제 하려면 foreign key 제약 조건은 구성할 수 있습니다. 즉, 자신의 사용자 계정을 삭제 하는 경우 사용자의 방명록 항목 자동으로 삭제 되도록이 외래 키 제약 조건을 설정할 수 있습니다. 이렇게 하려면 "INSERT 및 UPDATE 사양" 섹션을 확장 cascade를 지정 하는 "규칙 삭제" 속성을 설정 합니다.


[![하위 삭제를 외래 키 제약 조건 구성](storing-additional-user-information-vb/_static/image14.png)](storing-additional-user-information-vb/_static/image13.png)

**그림 5**: 계단식 삭제를 외래 키 제약 조건 구성 ([큰 이미지를 보려면 클릭](storing-additional-user-information-vb/_static/image15.png))


외래 키 제약을 저장 하려면 외래 키 관계를 종료 하려면 닫기 단추를 클릭 합니다. 테이블 및이 저장 하려면 도구 모음에서 저장 아이콘을 클릭 한 다음 관계입니다.

### <a name="storing-the-users-home-town-homepage-and-signature"></a>사용자의 홈 타운, 홈 페이지 및 서명을 저장

`GuestbookComments` 테이블에는 사용자 계정과 일 대 다 관계를 공유 하는 정보를 저장 하는 방법을 보여 줍니다. 각 사용자 계정 임의 개수의 관련된 댓글 수 없으므로이 관계를 특정 사용자에 게 각 메모를 다시 연결 하는 열을 포함 하는 주석의 집합을 저장할 테이블을 만들어 모델링 됩니다. 사용 하는 경우는 `SqlMembershipProvider`,이 링크를 가장 잘 라는 열을 만들어 설정 `UserId` 형식의 `uniqueidentifier` 및이 열 간의 외래 키 제약 조건 및 `aspnet_Users.UserId`합니다.

이제 사용자의 홈 town, 홈 페이지 및 자신의 방명록 주석에서 표시 되는 시그니처를 저장 하도록 각 사용자 계정을 사용 하 여 세 개의 열을 연결 해야 합니다. 이 작업을 수행 하는 다양 한 방법의 수:

- <strong>새 열을 추가 합니다</strong><strong>`aspnet_Users`</strong><strong>하거나</strong><strong>`aspnet_Membership`</strong><strong>테이블입니다.</strong> 사용 되는 스키마를 수정 하기 때문에이 방법은 권장 하지 않을 필자는 `SqlMembershipProvider`합니다. 이 의사 결정은 조만간 다닐 수 다시 가져올 수 있습니다. 예를 들어 경우 ASP.NET의 이후 버전에서는 다른 `SqlMembershipProvider` 스키마입니다. Microsoft ASP.NET 2.0을 마이그레이션하는 도구에 포함 될 수 있습니다 `SqlMembershipProvider` ASP.NET 2.0을 수정한 경우 이지만 새 스키마를 데이터 `SqlMembershipProvider` 스키마, 이러한 변환은 불가능할 수 있습니다.

- **ASP를 사용 합니다. .NET의 프로필 framework, 홈 타운, 홈 페이지 및 서명 프로필 속성을 정의 합니다.** ASP.NET 추가 사용자 고유의 데이터를 저장 하도록 설계 된 프로필 프레임 워크를 포함 합니다. 멤버 자격 프레임 워크와 같은 프로필 프레임 워크는 공급자 모델 작성 됩니다. .NET Framework와 함께 제공 되는 `SqlProfileProvider` 저장소 SQL Server 데이터베이스의 데이터 프로 파일링 하 합니다. 데이터베이스에 이미 사용 하는 테이블이 실제로 `SqlProfileProvider` (`aspnet_Profile`) 처럼 응용 프로그램 서비스를 다시 추가 했을 때 추가한 합니다 [ *SQL Server에서 멤버 자격 스키마 만들기* ](creating-the-membership-schema-in-sql-server-vb.md)자습서.   
  프로필 프레임 워크의 주된 이점은 개발자가 프로필 속성을 정의 하는 데 수 있다는 점입니다 `Web.config` – 내부 데이터 저장소에서 프로 파일 데이터를 직렬화 하 작성 해야 하는 코드가 없습니다. 즉, 쉽습니다 매우 프로필 속성 집합을 정의 하 고 코드에서 작업할 수 있습니다. 그러나 프로필 시스템 개선의 여지가 버전 관리에 있어 많았습니다 응용 프로그램 위치를 제거 하거나 수정 하 고, 기존 또는 나중에 추가할 새 사용자 고유의 속성을 원하는 다음 프로필 프레임 워크 아닐 경우는  최상의 옵션입니다. 또한는 `SqlProfileProvider` 거의 불가능 했습니다 (예: 얼마나 많은 사용자가를 홈 town의 New York) 프로필 데이터에 대해 직접 쿼리를 실행할 수 있도록 고도로 비 정규화 된 방식으로 프로필 속성을 저장 합니다.   
  프로필 프레임 워크에 대 한 자세한 내용은이 자습서의 끝에 "추가 정보" 섹션을 참조 하세요.

- <strong>데이터베이스에 새 테이블에 이러한 세 개의 열을 추가 하 고이 테이블 간에 한 일 관계를 설정 하 고</strong><strong>`aspnet_Users`</strong><strong>합니다.</strong> 이 방법은 프로필 프레임 워크를 사용 하 여 보다 약간 더 많은 작업이 포함 됩니다. 하지만 데이터베이스에서 추가 사용자 속성은 모델링 하는 방법에 대 한 최대 유연성을 제공 합니다. 이 자습서에서 사용 하는 옵션입니다.

라는 새 테이블을 만들겠습니다 `UserProfiles` 홈 타운, 홈 페이지 및 각 사용자에 대 한 서명을 저장 합니다. 데이터베이스 탐색기 창에서 테이블 폴더 단추로 클릭 하 고 새 테이블을 만들려면 선택 합니다. 첫 번째 열 이름을 `UserId` 해당 유형을 설정 하 고 `uniqueidentifier`입니다. Disallow `NULL` 값 및 기본 키로 열을 표시 합니다. 다음으로 명명 된 열을 추가 합니다. `HomeTown` 형식의 `nvarchar(50)`; `HomepageUrl` 형식의 `nvarchar(100)`; 및 형식 서명을 `nvarchar(500)`합니다. 이러한 세 가지 열 각각에 응하기는 `NULL` 값입니다.


[![UserProfiles 테이블 만들기](storing-additional-user-information-vb/_static/image17.png)](storing-additional-user-information-vb/_static/image16.png)

**그림 6**: 만들기 합니다 `UserProfiles` 표 ([클릭 하 여 큰 이미지 보기](storing-additional-user-information-vb/_static/image18.png))


테이블을 저장 하 고 이름을 `UserProfiles`입니다. 마지막으로, 간의 외래 키 제약 조건을 설정 합니다 `UserProfiles` 테이블의 `UserId` 필드 및 `aspnet_Users.UserId` 필드. 간의 외래 키 제약 조건을 사용 하 여 했던 것 처럼 합니다 `GuestbookComments` 및 `aspnet_Users` 테이블 삭제가 계단식으로 배열 하이 제약 조건이 있습니다. 있으므로 `UserId` 필드에 `UserProfiles` 는 주 서버이 키, 이렇게 하면 둘 이상의 레코드 되도록는 `UserProfiles` 각 사용자 계정에 대 한 테이블입니다. 이 형식의 관계는 일대일로 라고 합니다.

이제 만든 데이터 모델을 만들었으므로 준비가 사용 합니다. 2 단계와 3에 현재 로그온된 한 사용자 수 보기 및 홈 타운, 홈 페이지 및 서명 정보를 편집 하는 방법을 살펴보겠습니다. 4 단계에서에서 인증 된 사용자는 guestbook으로 새 의견을 제출 하 고 기존 서버를 볼 수에 대 한 인터페이스를 만들겠습니다.

## <a name="step-2-displaying-the-users-home-town-homepage-and-signature"></a>2 단계: 사용자의 홈 타운, 홈 페이지 및 서명을 표시

보고 자신의 홈 타운, 홈 페이지 및 서명 정보를 편집 하려면 현재 로그온된 한 사용자를 허용 하는 방법의 여러 가지가 있습니다. 텍스트 상자를 사용 하 여 사용자 인터페이스를 수동으로 만들 수 및 DetailsView 컨트롤과 같은 웹 컨트롤에 데이터 중 하나는 Label 컨트롤 또는에서는 사용할 수 있습니다. 데이터베이스를 수행 하려면 `SELECT` 및 `UPDATE` ADO.NET 작성할 수 있습니다이 페이지의 코드 숨김 클래스에서 코드 문이나, 또는 SqlDataSource와 함께 선언적 방식을 사용 합니다. 이상적으로 응용 프로그램 페이지의 코드 숨김 클래스 또는 선언적으로 ObjectDataSource 컨트롤을 통해 프로그래밍 방식으로 호출 하거나 수 계층화 된 아키텍처를 포함 됩니다.

이 자습서 시리즈는 폼 인증, 권한 부여, 사용자 계정 및 역할에 중점을 두고 있으므로 더 이상 없습니다 철저 한 설명은 다른 데이터 액세스 옵션 또는 SQL 문을 직접 실행을 통해 계층화 된 아키텍처는 것이 좋습니다는 이유 ASP.NET 페이지입니다. – 가장 쉽고 빠른 옵션-SqlDataSource와 DetailsView를 사용 하 여 안내 하고자 하지만 설명 된 개념 대체 웹 컨트롤 및 데이터 액세스 논리에 확실히 적용할 수 있습니다. ASP.NET에서 데이터를 사용 하 여 작업에 대 한 자세한 내용은 참조 내 *[ASP.NET 2.0에서 데이터로 작업할](../../data-access/index.md)* 자습서 시리즈입니다.

열기는 `AdditionalUserInfo.aspx` 페이지에 `Membership` 폴더 ID 속성을 설정 페이지로 DetailsView 컨트롤을 추가한 `UserProfile` 정리 및 해당 `Width` 및 `Height` 속성. DetailsView의 스마트 태그를 확장 하 고 새 데이터 소스 컨트롤에 연결 하려면 선택 합니다. 이 데이터 소스 구성 마법사가 시작 됩니다 (그림 7 참조). 첫 번째 단계를 사용 하면 데이터 원본 유형에를 묻습니다. 에 직접 연결할 것 이므로 `SecurityTutorials` 데이터베이스, 데이터베이스 아이콘을 지정 하는 `ID` 으로 `UserProfileDataSource`입니다.


[![UserProfileDataSource 라는 새 SqlDataSource 컨트롤을 추가 합니다.](storing-additional-user-information-vb/_static/image20.png)](storing-additional-user-information-vb/_static/image19.png)

**그림 7**: 명명 된 새 SqlDataSource 컨트롤을 추가 `UserProfileDataSource` ([클릭 하 여 큰 이미지 보기](storing-additional-user-information-vb/_static/image21.png))


다음 화면을 사용 하는 데이터베이스 요구 합니다. 연결 문자열을 이미 정의한 `Web.config` 에 대 한는 `SecurityTutorials` 데이터베이스입니다. 이 연결 문자열 이름 – `SecurityTutorialsConnectionString` – 드롭다운 목록에 있어야 합니다. 이 옵션을 선택 하 고 클릭 합니다.


[![SecurityTutorialsConnectionString 드롭 다운 목록에서 선택](storing-additional-user-information-vb/_static/image23.png)](storing-additional-user-information-vb/_static/image22.png)

**그림 8**: 선택 `SecurityTutorialsConnectionString` 드롭 다운 목록에서 ([클릭 하 여 큰 이미지 보기](storing-additional-user-information-vb/_static/image24.png))


다음 화면에서는 테이블 및 쿼리 하는 열을 지정 합니다. 선택 된 `UserProfiles` 드롭 다운 목록에서 테이블 및 열 모두 선택 합니다.


[![가져올 UserProfiles 테이블에서 모든 열을 다시](storing-additional-user-information-vb/_static/image26.png)](storing-additional-user-information-vb/_static/image25.png)

**그림 9**: Bring 다시 모든의 열을 `UserProfiles` 테이블 ([클릭 하 여 큰 이미지 보기](storing-additional-user-information-vb/_static/image27.png))


그림 9 반환의 현재 쿼리가 *모든* 의 레코드 `UserProfiles`, 현재 로그온된 한 사용자의 레코드에만 관심이 있지만. 추가할를 `WHERE` 절을 클릭 합니다 `WHERE` 단추를 추가 `WHERE` 절 대화 상자 (그림 10 참조). 여기에서 필터링 할 열, 연산자 및 필터 매개 변수의 소스를 선택할 수 있습니다. 선택 `UserId` 열과 연산자 "="입니다.

아쉽게도 현재 로그온된 한 사용자의 반환할 기본 제공 매개 변수 소스를이 없다는 `UserId` 값입니다. 이 값을 프로그래밍 방식으로 선택 해야 합니다. 따라서 원본 드롭 다운 목록 "None", 추가 매개 변수를 추가 하려면 단추를 클릭 한 다음 클릭을 설정 합니다.


[![UserId 열에서 필터 매개 변수를 추가 합니다.](storing-additional-user-information-vb/_static/image29.png)](storing-additional-user-information-vb/_static/image28.png)

**그림 10**:에서 필터 매개 변수를 추가 합니다 `UserId` 열 ([클릭 하 여 큰 이미지 보기](storing-additional-user-information-vb/_static/image30.png))


확인을 클릭 하면 그림 9에 표시 된 화면에 반환 됩니다. 하지만이 이때 화면 맨 아래에 있는 SQL 쿼리를 포함할지를 `WHERE` 절. "테스트 쿼리" 화면으로 이동 하려면 다음을 클릭 합니다. 쿼리를 실행 하면 다음 결과 확인 합니다. 마법사를 완료 하려면 마침을 클릭 합니다.

데이터 소스 구성 마법사를 완료 하면 Visual Studio에는 마법사에서 지정한 설정에 따라 SqlDataSource 컨트롤을 만듭니다. 또한 수동으로 추가 BoundFields SqlDataSource의에서 반환 된 각 열에 대 한 DetailsView `SelectCommand`합니다. 표시할 필요가 없습니다를 `UserId` 필드에 DetailsView 하므로 사용자는이 값을 알 필요가 없습니다. DetailsView 컨트롤의 선언적 태그에서 직접이 필드를 제거 하거나 "편집 필드"를 클릭 하 여 스마트 태그에서 연결 수 있습니다.

이 시점에서 페이지의 선언적 태그는 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample1.aspx)]

SqlDataSource 컨트롤의 프로그래밍 방식으로 설정 해야 `UserId` 매개 변수를 현재 로그인된 한 사용자의 `UserId` 데이터 선택 되기 전에 합니다. SqlDataSource의에 대 한 이벤트 처리기를 만들어 이렇게 `Selecting` 이벤트 및 다음 추가 코드 있습니다.

[!code-vb[Main](storing-additional-user-information-vb/samples/sample2.vb)]

위의 코드를 호출 하 여 현재 로그온된 한 사용자에 대 한 참조를 가져와서 시작 합니다 `Membership` 클래스의 `GetUser` 메서드. 반환 합니다.는 `MembershipUser` 개체입니다 `ProviderUserKey` 속성을 포함 합니다 `UserId`합니다. 합니다 `UserId` SqlDataSource의 값이 할당 한 다음 `@UserId` 매개 변수입니다.

> [!NOTE]
> `Membership.GetUser()` 메서드는 현재 로그온된 한 사용자에 대 한 정보를 반환 합니다. 익명 사용자가 페이지를 방문 하 고, 값이 반환 됩니다 `Nothing`합니다. 이러한 경우이로 인해를 `NullReferenceException` 읽으려고 할 때 코드의 다음 줄에는 `ProviderUserKey` 속성입니다. 물론, 걱정할 필요가 없습니다 `Membership.GetUser()` 의 경우 Nothing을 반환 합니다 `AdditionalUserInfo.aspx` 인증 된 사용자만이 폴더에 ASP.NET 리소스에 액세스할 수 있도록 이전 자습서에서 URL 권한 부여를 구성 했기 때문에 페이지입니다. 익명 액세스를 허용 하는 위치 페이지에서 현재 로그온된 한 사용자에 대 한 정보에 액세스 해야 할 경우 해야 하는지 확인 합니다 `MembershipUser` 에서 반환 된 개체는 `GetUser()` 메서드 Nothing이 아닌 해당 속성을 참조 하기 전에 합니다.


방문 하는 경우는 `AdditionalUserInfo.aspx` 페이지 브라우저를 통해 표시 됩니다 모든 행을 추가 하려면 아직 때문에 빈 페이지는 `UserProfiles` 테이블입니다. 새 행을 자동으로 추가할 CreateUserWizard 컨트롤 사용자 지정 하는 방법을 살펴보겠습니다 6 단계에서에서의 `UserProfiles` 새 사용자 계정을 만들면 테이블입니다. 그러나 지금은 해야 수동으로 테이블에 레코드를 만듭니다.

Visual Studio에서 Database Explorer로 이동 하 고 테이블 폴더를 확장 합니다. 마우스 오른쪽 단추로 클릭 합니다 `aspnet_Users` 테이블 및 테이블의 레코드를 보려면 "테이블 데이터 표시" 선택;에 대해 동일한 작업을 수행 합니다 `UserProfiles` 테이블입니다. 그림 11에서는 세로 바둑판식으로 배열 하는 경우 이러한 결과 보여 줍니다. 데이터베이스에 현재 가지 `aspnet_Users` Bruce, Fred 및 Tito에 대 한 레코드 있지만 레코드 없음는 `UserProfiles` 테이블입니다.


[![표시 되는 aspnet_Users 내용과 UserProfiles 테이블](storing-additional-user-information-vb/_static/image32.png)](storing-additional-user-information-vb/_static/image31.png)

**그림 11**: The 내용의 합니다 `aspnet_Users` 하 고 `UserProfiles` 테이블이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-vb/_static/image33.png))


새 레코드를 추가 합니다 `UserProfiles` 수동으로 대 한 값을 입력 하 여 테이블을 `HomeTown`, `HomepageUrl`, 및 `Signature` 필드. 유효한 얻을 수 있는 가장 쉬운 방법은 `UserId` 새 값 `UserProfiles` 레코드는 선택 하는 `UserId` 의 특정 사용자 계정에서 필드를 `aspnet_Users` 테이블 복사 및 붙여 넣습니다 합니다 `UserId` 필드에 `UserProfiles`. 그림 12는 `UserProfiles` Bruce에 대 한 새 레코드를 추가한 후 테이블입니다.


[![Bruce UserProfiles에 추가한 레코드](storing-additional-user-information-vb/_static/image35.png)](storing-additional-user-information-vb/_static/image34.png)

**그림 12**: A 레코드에 추가 되었습니다 `UserProfiles` Bruce에 대 한 ([클릭 하 여 큰 이미지 보기](storing-additional-user-information-vb/_static/image36.png))


반환 합니다 `AdditionalUserInfo.aspx page`, Bruce로 로그인 합니다. 그림 13에서 알 수 있듯이, Bruce의 설정이 표시 됩니다.


[![현재 방문 사용자가 His 설정 표시](storing-additional-user-information-vb/_static/image38.png)](storing-additional-user-information-vb/_static/image37.png)

**그림 13**: 현재 방문 사용자는 His 설정 표시 ([큰 이미지를 보려면 클릭](storing-additional-user-information-vb/_static/image39.png))


> [!NOTE]
> 수동으로 추가 레코드를 `UserProfiles` 각 멤버 자격 사용자에 대 한 테이블입니다. 새 행을 자동으로 추가할 CreateUserWizard 컨트롤 사용자 지정 하는 방법을 살펴보겠습니다 6 단계에서에서의 `UserProfiles` 새 사용자 계정을 만들면 테이블입니다.


## <a name="step-3-allowing-the-user-to-edit-his-home-town-homepage-and-signature"></a>3 단계: 사용자가 자신의 홈 타운, 홈 페이지 및 서명을 편집할 수 있도록

현재 로그인된 한 사용자를 해당 홈 town, 홈 페이지 및 서명 설정을 볼 수는 시점에서 있지만 이러한 아직 수정할 수 없습니다. 데이터를 편집할 수 있도록 DetailsView 컨트롤을 업데이트 해 보겠습니다.

가장 먼저 해야 할 추가 됩니다는 `UpdateCommand` SqlDataSource에 대 한 지정 하는 `UPDATE` 문을 실행 하 고 해당 매개 변수. SqlDataSource를 선택 하 고 속성 창에서 명령 및 매개 변수 편집기 대화 상자를 표시 하려면 UpdateQuery 속성 옆의 줄임표를 클릭 합니다. 다음과 같이 입력 `UPDATE` 문 텍스트 상자에 붙여넣습니다.

[!code-sql[Main](storing-additional-user-information-vb/samples/sample3.sql)]

다음으로, SqlDataSource 컨트롤의 매개 변수를 생성 하는 "매개 변수 새로 고침" 단추를 클릭 `UpdateParameters` 매개 변수 각각에 대 한 컬렉션을 `UPDATE` 문입니다. None 매개 변수 집합의 모든 소스를 두고 대화 상자를 완료 하려면 확인 단추를 클릭 합니다.


[![SqlDataSource의 UpdateCommand 및 UpdateParameters 지정](storing-additional-user-information-vb/_static/image41.png)](storing-additional-user-information-vb/_static/image40.png)

**그림 14**: SqlDataSource의 지정할 `UpdateCommand` 하 고 `UpdateParameters` ([클릭 하 여 큰 이미지 보기](storing-additional-user-information-vb/_static/image42.png))


추가 된 항목으로 인해 이제를 지원할 수 있는 편집 DetailsView SqlDataSource 컨트롤에 만들었습니다. DetailsView의 스마트 태그에서 "편집 사용" 확인란을 확인 합니다. 컨트롤에는 CommandField 추가 `Fields` 컬렉션과 해당 `ShowEditButton` 속성이 True로 설정 합니다. 이 DetailsView 읽기 전용 모드 및 업데이트에 표시 되 고 취소 단추에 표시 되는 모드를 편집 하는 경우 편집 단추를 렌더링 합니다. 사용자가 편집 클릭에 요구 하는 대신 그러나 있다는 DetailsView 렌더링 "항상 편집 가능" 상태로 DetailsView 컨트롤을 설정 하 여 [ `DefaultMode` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.defaultmode.aspx) 하려면 `Edit`합니다.

이러한 변경으로 DetailsView 컨트롤의 선언적 태그는 다음과 같아야 합니다.

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample4.aspx)]

CommandField 추가 및 `DefaultMode` 속성입니다.

계속 해 서 브라우저를 통해이 페이지를 테스트 합니다. 해당 레코드에 있는 사용자를 방문할 때 `UserProfiles`, 사용자의 설정을 편집할 수 있는 인터페이스에 표시 됩니다.


[![DetailsView를 편집할 수 있는 인터페이스를 렌더링합니다.](storing-additional-user-information-vb/_static/image44.png)](storing-additional-user-information-vb/_static/image43.png)

**그림 15**: DetailsView를 편집할 수 있는 인터페이스를 렌더링 합니다. ([큰 이미지를 보려면 클릭](storing-additional-user-information-vb/_static/image45.png))


시도 값을 변경 하 고 업데이트 단추를 클릭 합니다. 아무 작업도 처럼 표시 됩니다. 다시 게시 하 고 값이 데이터베이스에 저장 됩니다 있지만 저장 수행한 visual 알 수 없습니다.

이 해결 하려면 Visual Studio로 돌아가서 및 DetailsView 위에 레이블 컨트롤을 추가 합니다. 설정 해당 `ID` 에 `SettingsUpdatedMessage`, 해당 `Text` 속성을 "사용자 설정이 업데이트 되었습니다," 및 해당 `Visible` 하 고 `EnableViewState` 속성을 `False`입니다.

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample5.aspx)]

표시할 필요는 `SettingsUpdatedMessage` DetailsView 업데이트 될 때마다 레이블. DetailsView의에 대 한 이벤트 처리기를 만들고이를 위해 `ItemUpdated` 이벤트 다음 코드를 추가 합니다.

[!code-vb[Main](storing-additional-user-information-vb/samples/sample6.vb)]

반환 합니다 `AdditionalUserInfo.aspx` 브라우저를 통해 페이지와 데이터를 업데이트 합니다. 이 이번에는 유용한 상태 메시지가 표시 됩니다.


[![짧은 메시지를 표시 되는 경우 설정 업데이트](storing-additional-user-information-vb/_static/image47.png)](storing-additional-user-information-vb/_static/image46.png)

**그림 16**: 설정이 업데이트 되는 짧은 메시지가 표시 됩니다 ([큰 이미지를 보려면 클릭](storing-additional-user-information-vb/_static/image48.png))


> [!NOTE]
> DetailsView 컨트롤의 편집 인터페이스 리프는 부분이 됩니다. 표준 크기의 텍스트 상자를 사용 하지만 서명 필드는 여러 줄 텍스트 상자 되어야 할 수 있습니다. RegularExpressionValidator는 홈 페이지 URL을 입력 하는 경우 시작 "http://" 또는 "https://"로 확인 하는 것 같습니다. DetailsView 컨트롤에는 또한 이후에 해당 `DefaultMode` 속성이 설정 `Edit`, 취소 단추 아무 작업도 하지 않습니다. 이 하거나 제거 하거나를 클릭 하면 사용자를 리디렉션할 다른 일부 페이지 (같은 `~/Default.aspx`). I 이러한 향상 된이 기능은 판독기에 대 한 연습을 그대로 둡니다.


### <a name="adding-a-link-to-theadditionaluserinfoaspxpage-in-the-master-page"></a>에 대 한 링크를 추가 합니다`AdditionalUserInfo.aspx`마스터 페이지에서 페이지

현재 웹 사이트에 대 한 링크 제공 하지 않습니다는 `AdditionalUserInfo.aspx` 페이지입니다. 서버에 도달 하는 유일한 방법은 브라우저의 주소 표시줄에 직접 페이지의 URL을 입력 하는 것입니다. 이 페이지에 대 한 링크를 추가 해 보겠습니다는 `Site.master` 마스터 페이지입니다.

마스터 페이지에는 LoginView 웹 컨트롤에 회수 해당 `LoginContent` ContentPlaceHolder 인증 및 익명 방문자에 대 한 다른 태그를 표시 하는 합니다. LoginView 컨트롤의 업데이트 `LoggedInTemplate` 링크를 포함 하는 `AdditionalUserInfo.aspx` 페이지입니다. LoginView 이러한 변경을 수행한 후 컨트롤의 선언적 태그는 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample7.aspx)]

추가 된 `lnkUpdateSettings` 하이퍼링크 컨트롤을는 `LoggedInTemplate`합니다. 진행에서이 링크를 사용 하 여 인증 된 사용자가 홈 타운, 홈 페이지 및 서명을 설정 보기 및 수정 페이지 빠르게 이동할 수 있습니다.

## <a name="step-4-adding-new-guestbook-comments"></a>4 단계: 새 방명록 주석 추가

`Guestbook.aspx` 페이지 위치 이며 인증 된 사용자 수는 방명록 보고 의견을 남겨 주세요. 새 방명록 주석을 추가 하는 인터페이스를 만드는 것부터 시작 하겠습니다.

열기는 `Guestbook.aspx` Visual Studio에서 페이지 및 새 메모의 제목 및 본문에 대 한 두 개의 텍스트 상자 컨트롤 구성 된 사용자 인터페이스를 생성 합니다. 첫 번째 텍스트 상자 컨트롤을 설정 `ID` 속성을 `Subject` 및 해당 `Columns` 40 속성; 설정된 두 번째 `ID` 하 `Body`, 해당 `TextMode` 에 `MultiLine`, 및 해당 `Width` 및 `Rows` 속성을 "95%" 및 8, 각각. 사용자 인터페이스를 완료 하려면 라는 단추 웹 컨트롤을 추가 `PostCommentButton` 설정 및 해당 `Text` "댓글 게시" 하는 속성입니다.

각 방명록 주석 제목 및 본문에 필요한 있으므로 각 텍스트 상자에 대 한는 RequiredFieldValidator를 추가 합니다. 설정 합니다 `ValidationGroup` "EnterComment"; 이러한 컨트롤의 속성 마찬가지로 설정 합니다 `PostCommentButton` 컨트롤의 `ValidationGroup` "EnterComment" 속성입니다. ASP에 대 한 자세한 내용은 합니다. NET의 유효성 검사 컨트롤, 체크 아웃 [asp.net에서 양식 유효성 검사](http://www.4guysfromrolla.com/webtech/090200-1.shtml)를 [ASP.NET 2.0의 유효성 검사 컨트롤 분석](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx), 및 [유효성 검사 서버 컨트롤 자습서](http://www.w3schools.com/aspnet/aspnet_refvalidationcontrols.asp) 온 [W3Schools](http://www.w3schools.com/)합니다.

사용자 인터페이스를 작성 한 후 페이지의 선언적 태그 다음과 유사한 출력이 표시 됩니다.

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample8.aspx)]

에 새 레코드를 삽입 하는 다음 작업은 전체 사용자 인터페이스를 사용 하 여를 `GuestbookComments` 때 테이블을 `PostCommentButton` 를 클릭 합니다. 여러 가지 방법으로에서 수행할 수 있습니다: 단추의 ADO.NET 코드를 작성할 수 있습니다 `Click` 이벤트 처리기에 구성에 페이지를 SqlDataSource 컨트롤을 추가할 수 해당 `InsertCommand`, 호출 및 해당 `Insert` 메서드에서 `Click` 이벤트 처리기 새 방명록 주석을 삽입 하는 일을 담당 했습니다 되는 중간 계층을 구축 하 고에서이 기능을 호출할 수 있었습니다 또는 `Click` 이벤트 처리기입니다. SqlDataSource를 사용 하 여 3 단계에서에서 보이는 것 이므로 보겠습니다 ADO.NET 코드 여기 사용 합니다.

> [!NOTE]
> Microsoft SQL Server 데이터베이스에서 데이터를 프로그래밍 방식으로 액세스 하는 데 ADO.NET 클래스에는 `System.Data.SqlClient` 네임 스페이스입니다. 페이지의 코드 숨김 클래스에이 네임 스페이스를 가져와야 할 수 있습니다 (즉, `Imports System.Data.SqlClient`).


이벤트 처리기를 만듭니다는 `PostCommentButton`의 `Click` 이벤트 다음 코드를 추가 합니다.

[!code-vb[Main](storing-additional-user-information-vb/samples/sample9.vb)]

`Click` 이벤트 처리기는 사용자 제공 데이터가 유효한 지 확인 하 여 시작 합니다. 없는 경우 레코드를 삽입 하기 전에 이벤트 처리기를 종료 합니다. 제공 된 데이터가 잘못 가정 하 고 현재 로그온된 한 사용자의 `UserId` 값을 검색 하 고 저장 합니다 `currentUserId` 지역 변수입니다. 에서는 제공 해야 하기 때문에이 값이 필요를 `UserId` 에 레코드 삽입 시 값 `GuestbookComments`합니다.

다음에 대 한 연결 문자열을 `SecurityTutorials` 데이터베이스에서 검색 됩니다 `Web.config` 및 `INSERT` SQL 문을 지정 합니다. `SqlConnection` 개체가 다음 생성 되 고 열립니다. 다음으로 `SqlCommand` 개체가 생성 되 고 매개 변수의 값에 사용를 `INSERT` 쿼리 할당 됩니다. `INSERT` 문을 다음으로 실행 되 고 연결이 종료 됩니다. 이벤트 처리기의 끝에는 `Subject` 및 `Body` 텍스트 상자 `Text` 포스트백에서 사용자의 값이 유지 되지 않습니다 있도록 속성이 지워집니다.

계속 해 서 브라우저에서이 페이지를 테스트 합니다. 이 페이지의 이므로 `Membership` 익명 방문자에 게 액세스할 수 없기 폴더입니다. 따라서 먼저 (있는 경우 아직)에 로그온 해야 합니다. 에 값을 입력 합니다 `Subject` 및 `Body` 텍스트 상자 클릭 및는 `PostCommentButton` 단추. 이렇게 하면 새 레코드에 추가할 `GuestbookComments`합니다. 포스트백에서 제목 및 본문 입력 된 텍스트 상자에서 초기화 됩니다.

클릭 한 후의 `PostCommentButton` 단추에 있는 시각적 피드백은 없습니다를 guestbook으로 주석이 추가 된 합니다. 5 단계에서에서 수행 하는 기존 방명록 메모를 표시 하려면이 페이지를 업데이트 해야 합니다. 이렇게 우리가 방금 추가 된 주석 주석, 적절 한 시각적 피드백을 제공 목록에 표시 됩니다. 지금은 방명록 의견의 내용을 검사 하 여 저장 된 것을 확인 합니다 `GuestbookComments` 테이블입니다.

그림 17의 내용을 보여 줍니다는 `GuestbookComments` 테이블 두 주석이 있습니다.


[![GuestbookComments 표에 방명록 주석을 볼 수 있습니다.](storing-additional-user-information-vb/_static/image50.png)](storing-additional-user-information-vb/_static/image49.png)

**그림 17**: 방명록 주석을 표시 합니다 `GuestbookComments` 테이블 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-vb/_static/image51.png))


> [!NOTE]
> HTML – ASP.NET 같은 위험한 태그 – 사용자가 잠재적으로 포함 하는 방명록 주석 삽입 하려고 하는 경우 throw 됩니다는 `HttpRequestValidationException`합니다. 이 예외를 throw 이유 및 사용자가 잠재적으로 위험한 값을 제출 하도록 허용 하는 방법에 대 한 자세한 내용은 참조는 [요청 유효성 검사 백서](../../../../whitepapers/request-validation.md)합니다.


## <a name="step-5-listing-the-existing-guestbook-comments"></a>5 단계: 기존 방명록 주석을 나열

의견을 방문한 사용자 외에 `Guestbook.aspx` 페이지도 방명록의 기존 주석을 볼 수 있어야 합니다. 이렇게 하려면 명명 된 ListView 컨트롤을 추가 `CommentList` 페이지 맨 아래에 있습니다.

> [!NOTE]
> ListView 컨트롤은 ASP.NET 3.5 버전을 새입니다. 사용자 지정 가능 하 고 유연한 레이아웃에서 항목의 목록을 표시 하지만 계속 기본 제공 편집, 삽입, 삭제, 페이징 및 정렬 GridView와 같은 기능을 제공 하도록 설계 되었습니다. ASP.NET 2.0을 사용 하는 경우에 DataList 또는 Repeater 컨트롤을 대신 사용 해야 합니다. ListView를 사용 하 여 자세한 내용은 [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 블로그 항목 [asp: ListView 컨트롤](https://weblogs.asp.net/scottgu/archive/2007/08/10/the-asp-listview-control-part-1-building-a-product-listing-page-with-clean-css-ui.aspx), 및 필자의 기사 [ListView 컨트롤을 사용 하 여 데이터 표시](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)합니다.


ListView의 스마트 태그를 열고 데이터 소스 선택 드롭다운 목록에서 새 데이터 소스에 컨트롤을 바인딩하십시오. 2 단계에서에서 보았듯이 데이터 소스 구성 마법사 시작 됩니다. 데이터베이스 아이콘을 선택, 결과 SqlDataSource 이름을 `CommentsDataSource`, 확인을 클릭 합니다. 다음으로, 선택 된 `SecurityTutorialsConnectionString` 연결 문자열 드롭다운 목록에서 다음을 클릭 합니다.

이 시점에서 2 단계에서에서 지정한 데이터 쿼리를 선택 하 여는 `UserProfiles` 드롭 다운 목록에서 테이블 및 반환할 열을 선택 하면 (그림 9 다시 참조). 그러나이 이때 하고자 뿐만 아니라에서 레코드를 다시 가져오는 SQL 문을 만들 `GuestbookComments`, 하지만 메모의 홈 마을 또한, 홈페이지, 서명 및 사용자 이름입니다. 따라서 "사용자 지정 SQL 문 또는 저장된 프로시저 지정" 라디오 단추를 선택 하 고 클릭 합니다.

"정의 사용자 지정 문 또는 저장 프로시저" 화면이 표시 됩니다. 쿼리를 작성 하는 그래픽 쿼리 작성기 단추를 클릭 합니다. 쿼리 작성기에서 쿼리 하려는 테이블을 지정 하 라는 메시지가 표시 하 여 시작 합니다. 선택 합니다 `GuestbookComments`, `UserProfiles`, 및 `aspnet_Users` 테이블 및 확인을 클릭 합니다. 이렇게 하면 모든 세 테이블 디자인 화면에 추가 됩니다. 간에 외래 키 제약 조건이 있으므로 합니다 `GuestbookComments`, `UserProfiles`, 및 `aspnet_Users` 테이블을 쿼리 작성기를 자동으로 `JOIN` s 이러한 테이블.

에 반환할 열을 지정 합니다. `GuestbookComments` 테이블을 `Subject`, `Body`, 및 `CommentDate` 열은 반환을 `HomeTown`, `HomepageUrl`, 및 `Signature` 열에서를 `UserProfiles` ; 테이블을 반환 `UserName` 에서`aspnet_Users`. 또한 추가 "`ORDER BY CommentDate DESC`"의 끝에는 `SELECT` 최근 게시물 먼저 반환 되도록 쿼리 합니다. 이러한 선택 항목에 확인 한 후 쿼리 작성기 인터페이스 그림 18에서 스크린샷과 유사 합니다.


[![생성 된 쿼리 GuestbookComments, UserProfiles, 및 aspnet_Users 테이블 조인](storing-additional-user-information-vb/_static/image53.png)](storing-additional-user-information-vb/_static/image52.png)

**그림 18**: 생성 된 쿼리 `JOIN` s 합니다 `GuestbookComments`, `UserProfiles`, 및 `aspnet_Users` 테이블 ([클릭 하 여 큰 이미지 보기](storing-additional-user-information-vb/_static/image54.png))


쿼리 작성기 창을 닫고 정의 사용자 지정 문 또는 저장 프로시저 "" 화면으로 돌아가서 확인을 클릭 합니다. 쿼리 테스트 단추를 클릭 하 여 쿼리 결과 볼 수 있는 "테스트 쿼리" 화면에 고급을 클릭 합니다. 준비 되 면, 데이터 소스 구성 마법사를 완료 하려면 마침을 클릭 합니다.

2 단계에서 연결된 된 DetailsView 컨트롤의 데이터 소스 구성 마법사를 완료 하는 것 `Fields` 컬렉션에서 반환 된 각 열에 대 한 BoundField를 포함 하도록 업데이트 되었으며는 `SelectCommand`합니다. 그러나 ListView, 그대로 유지 됩니다. 해당 레이아웃을 정의 해야 합니다. 해당 선언적 태그를 통해 또는 스마트 태그가 "ListView 구성" 옵션에서 ListView의 레이아웃을 수동으로 생성할 수 있습니다. 일반적으로 태그를 직접 정의 하는 것이 좋습니다. 했지만 할 가장 자연 스러운 방법을 사용 합니다.

최종적 다음을 사용 하 여 `LayoutTemplate`, `ItemTemplate`, 및 `ItemSeparatorTemplate` ListView 컨트롤에 대 한 합니다.

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample10.aspx)]

합니다 `LayoutTemplate` 태그를 정의 하는 동안 컨트롤에 의해 생성 되는 `ItemTemplate` SqlDataSource에서 반환 된 각 항목을 렌더링 합니다. `ItemTemplate`의 결과 태그에 배치 되는 `LayoutTemplate`의 `itemPlaceholder` 제어 합니다. 외에 `itemPlaceholder`, `LayoutTemplate` (기본값) 페이지당 10 개만 방명록 주석을 표시 하는 ListView를 제한 하는 DataPager 컨트롤을 포함 하 고 페이징 인터페이스를 렌더링 합니다.

내 `ItemTemplate` 에서 각 방명록 주석의 주체 표시는 `<h4>` 요소를 본문 제목 아래에 위치 합니다. 구문 본문을 표시 하는 데 사용 하 여 반환 되는 데이터를 `Eval("Body")` 데이터 바인딩 문을 문자열로 변환 하 고 사용 하 여 대체 줄 바꿈 합니다 `<br />` 요소입니다. 이 변환은 입력 HTML 공백 무시 되므로 메모를 제출할 때 줄 바꿈을 표시 하기 위해 필요 합니다. 사용자의 서명 뒤에 사용자의 홈 도시별으로 자신의 홈 페이지, 메모를 만든 날짜 및 시간과 주석을 남긴 사용자의 사용자 이름에 대 한 링크를 기울임꼴로 본문 아래에 표시 됩니다.

브라우저를 통해 페이지를 보려면 잠시 시간이 소요 됩니다. 여기에 표시 된 5 단계에서에서 방명록에 추가 하는 주석을 표시 되어야 합니다.


[![Guestbook.aspx 이제 방명록의 주석 표시](storing-additional-user-information-vb/_static/image56.png)](storing-additional-user-information-vb/_static/image55.png)

**그림 19**: `Guestbook.aspx` 방명록의 주석 표시 ([클릭 하 여 큰 이미지 보기](storing-additional-user-information-vb/_static/image57.png))


guestbook으로 새 메모를 추가 해 보세요. 클릭 하면는 `PostCommentButton` 단추 페이지 다시 게시 및 주석 데이터베이스에 추가 되지만 ListView 컨트롤 새 메모를 표시 하도록 업데이트 되지 않습니다. 이 통해 해결할 수 있습니다.

- 업데이트를 `PostCommentButton` 단추의 `Click` 이벤트 처리기는 ListView 컨트롤의 호출 되므로 `DataBind()` 메서드를 데이터베이스에 새 메모를 삽입 한 후 또는
- ListView 컨트롤의 설정 `EnableViewState` 속성을 `False`입니다. 컨트롤의 뷰 상태를 해제 하 여이 다시 바인딩해야 포스트백이 발생할 때마다 기본 데이터에 없으므로이 접근 방식은 유용 합니다.

이 자습서에서 다운로드할 수 있는 자습서 웹 사이트에 두 가지 방법을 모두 보여 줍니다. ListView 컨트롤의 `EnableViewState` 속성을 `False` 프로그래밍 방식으로 데이터를 ListView 다시 바인딩해야 하는 데 필요한 코드에 있는지를 `Click` 이벤트 처리기를 주석 처리 되어 있지만.

> [!NOTE]
> 현재는 `AdditionalUserInfo.aspx` 페이지 수 있도록 하려면 해당 홈 타운, 홈 페이지 및 서명을 설정 보기 및 편집 합니다. 업데이트 좋을 것 `AdditionalUserInfo.aspx` 표시할 로그온 된 사용자의 방명록 설명 합니다. 즉, 검사 하 고 자신의 정보를 수정 하는 것 외에도 사용자 방문할 수는 `AdditionalUserInfo.aspx` 페이지를 이전에 이루어집니다 그녀는 방명록 주석을 참조 하세요. I 관심이 있는 독자를 연습으로 둡니다.


## <a name="step-6-customizing-the-createuserwizard-control-to-include-an-interface-for-the-home-town-homepage-and-signature"></a>6 단계: 홈 타운, 홈 페이지 및 서명을 위한 인터페이스를 포함 하도록 CreateUserWizard 컨트롤 사용자 지정

`SELECT` 사용 하는 쿼리를 `Guestbook.aspx` 사용 하 여 페이지를 `INNER JOIN` 간에 관련된 레코드를 결합 하는 `GuestbookComments`를 `UserProfiles`, 및 `aspnet_Users` 테이블입니다. 사용자가 없는 레코드에 있는 `UserProfiles` 방명록 하면 주석, 주석 때문에 ListView에 표시 되지 않습니다는 `INNER JOIN` 만 반환 `GuestbookComments` 일치 하는 레코드의 경우 레코드 `UserProfiles` 및 `aspnet_Users`. 및 사용자 레코드가 없는 경우 3 단계에서에서 설명한 것 처럼 `UserProfiles` 보거나에 게 설정을 편집할 수 없는 그녀는 `AdditionalUserInfo.aspx` 페이지입니다.

물론 디자인으로 인해 일치 하는 모든 사용자 계정이 멤버 자격 시스템에 있는 것으로 결정에 기록 된 `UserProfiles` 테이블입니다. 해당 레코드를 추가할 수는 원하는 `UserProfiles` 새 멤버 자격 사용자 계정이 CreateUserWizard 통해 때마다 만들어집니다.

에 설명 된 대로 합니다 [ *사용자 계정 만들기* ](creating-user-accounts-vb.md) 자습서에서는 새 멤버 자격 사용자 계정이 CreateUserWizard 컨트롤 만들어지면 발생 해당 [ `CreatedUser` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx). 수이 이벤트에 대 한 이벤트 처리기를 만듭니다, 방금 만든 사용자에 대 한 사용자 Id를 가져오기 하 고 다음에 레코드를 삽입 합니다 `UserProfiles` 테이블에 대 한 기본값을 사용 하 여는 `HomeTown`, `HomepageUrl`, 및 `Signature` 열입니다. 게다가를 CreateUserWizard 컨트롤의 추가 텍스트를 포함 하는 인터페이스를 사용자 지정 하 여 이러한 값에 대 한 사용자에 게는 것이 가능 합니다.

새 행을 추가 하는 방법부터 알아보겠습니다 합니다 `UserProfiles` 테이블에 `CreatedUser` 기본값을 사용 하 여 이벤트 처리기입니다. 그런 다음, 새 사용자의 홈 타운, 홈 페이지 및 서명 수집 하도록 추가 양식 필드를 포함 하도록 CreateUserWizard 컨트롤의 사용자 인터페이스 사용자 지정 하는 방법을 살펴보겠습니다.

### <a name="adding-a-default-row-touserprofiles"></a>기본 행을 추가합니다.`UserProfiles`

에 [ *사용자 계정 만들기* ](creating-user-accounts-vb.md) CreateUserWizard 컨트롤을 추가 했습니다 하는 자습서는 `CreatingUserAccounts.aspx` 페이지에서 `Membership` 폴더. 컨트롤의 레코드를 추가 하려면 CreateUserWizard `UserProfiles` 테이블 사용자 계정 생성 시 CreateUserWizard 컨트롤의 기능을 업데이트 해야 합니다. 변경 내용을이 적용 하는 것 보다는 `CreatingUserAccounts.aspx` 페이지에서 새 CreateUserWizard 컨트롤을 대신 추가 `EnhancedCreateUserWizard.aspx` 페이지 및이 자습서에서는 수정 작업을 수행할 합니다.

열기는 `EnhancedCreateUserWizard.aspx` Visual Studio에서 페이지 및 페이지 도구 상자에서 CreateUserWizard 컨트롤을 끌어 옵니다. CreateUserWizard 컨트롤의 `ID` 속성을 `NewUserWizard`입니다. 설명한 대로 합니다 [ *사용자 계정 만들기* ](creating-user-accounts-vb.md) 자습서, CreateUserWizard의 기본 사용자 인터페이스에서 라는 메시지를 표시 하는 데 필요한 정보에 대 한 방문자입니다. 이 정보를 제공한 후 컨트롤 내부적으로 새 사용자 계정을 만듭니다 멤버 자격 프레임 워크에 코드 한 줄도 작성할 필요 없이 합니다.

CreateUserWizard 컨트롤 해당 워크플로 중에 다양을 한 이벤트를 발생 시킵니다. CreateUserWizard 컨트롤 처음 발생 방문자가 양식을 전송 요청 정보를 제공 하 고 해당 [ `CreatingUser` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.creatinguser.aspx)합니다. 하지만 만들기 프로세스 중에 문제가 있으면를 [ `CreateUserError` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createusererror.aspx) 이벤트가 발생 이면 사용자가 성공적으로 만들어지면 해당 [ `CreatedUser` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx) 발생 합니다. 에 [ *사용자 계정 만들기* ](creating-user-accounts-vb.md) 자습서에 대 한 이벤트 처리기를 만들었습니다는 `CreatingUser` 선행 또는 후행 공백 및는 제공 된 사용자 이름이 포함 되지 않은 이벤트는 사용자 이름 암호에 표시 되지 않았습니다.

행을 추가 하려면 합니다 `UserProfiles` 테이블 방금 만든 사용자에 대 한 이벤트 처리기를 생성 해야 합니다 `CreatedUser` 이벤트입니다. 시간을 `CreatedUser` 이벤트가 발생 한, 계정의 사용자 Id 값을 검색 하기를 사용 하도록 설정 하는 멤버 자격 프레임 워크에 사용자 계정이 이미 만들어져 있습니다.

이벤트 처리기를 만듭니다는 `NewUserWizard`의 `CreatedUser` 이벤트 다음 코드를 추가 합니다.

[!code-vb[Main](storing-additional-user-information-vb/samples/sample11.vb)]

방금 추가 된 사용자 계정의 사용자 Id를 검색 하 여 위의 코드 시작 합니다. 사용 하 여 이렇게 합니다 `Membership.GetUser(username)` 특정 사용자를 사용 하 여 다음 정보를 반환 하는 방법은 `ProviderUserKey` 해당 사용자 Id를 검색할 속성. CreateUserWizard 컨트롤에서 사용자가 입력 한 사용자 이름은 통해 사용할 수 있는 해당 [ `UserName` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.username.aspx)합니다.

연결 문자열에서 검색 되는 어 `Web.config` 및 `INSERT` 문을 지정 합니다. 필요한 ADO.NET 개체를 인스턴스화하고 명령을 실행 합니다. 코드에서 할당을 [ `DBNull` ](https://msdn.microsoft.com/library/system.dbnull.aspx) 인스턴스를 `@HomeTown`, `@HomepageUrl`, 및 `@Signature` 효과가 데이터베이스에 삽입 하는 매개 변수 `NULL` 에 대 한 값을 `HomeTown`, `HomepageUrl`, 및 `Signature` 필드입니다.

방문을 `EnhancedCreateUserWizard.aspx` 브라우저를 통해 페이지 및 새 사용자 계정을 만듭니다. 이렇게 한 다음, Visual Studio로 돌아가서 및의 내용을 검사 합니다 `aspnet_Users` 및 `UserProfiles` 테이블 (예: 다시에 수행한 그림 12). 새 사용자 계정에 표시 되어야 `aspnet_Users` 및 해당 `UserProfiles` 행 (사용 하 여 `NULL` 에 대 한 값 `HomeTown`에 `HomepageUrl`, 및 `Signature`).


[![추가 된 새 사용자 계정 및 UserProfiles 레코드](storing-additional-user-information-vb/_static/image59.png)](storing-additional-user-information-vb/_static/image58.png)

**그림 20**: 새 사용자 계정 및 `UserProfiles` 레코드가 추가 되었습니다 ([클릭 하 여 큰 이미지 보기](storing-additional-user-information-vb/_static/image60.png))


사용자 계정 생성 되 고 행이 추가 방문자에 자신의 새 계정 정보를 제공 하 고 "Create User" 단추를 클릭 한 후의 `UserProfiles` 테이블입니다. CreateUserWizard을 표시 합니다. 해당 `CompleteWizardStep`, 계속 단추 성공 메시지를 표시 합니다. 포스트백을 계속 단추를 클릭 하면 아무 작업도 수행 하지만 중단 사용자는 `EnhancedCreateUserWizard.aspx` 페이지입니다.

CreateUserWizard 컨트롤을 통해 계속 단추를 클릭 하는 경우에 사용자를 보낼 URL을 지정할 수 있습니다 [ `ContinueDestinationPageUrl` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)합니다. 설정 된 `ContinueDestinationPageUrl` 속성을 "~ / Membership/AdditionalUserInfo.aspx"입니다. 새 사용자를 이렇게 `AdditionalUserInfo.aspx`, 여기서 확인 하 고 해당 설정을 업데이트 합니다.

### <a name="customizing-the-createuserwizards-interface-to-prompt-for-the-new-users-home-town-homepage-and-signature"></a>새 사용자의 홈 타운, 홈 페이지 및 서명 확인에 대 한 CreateUserWizard의 인터페이스를 사용자 지정

CreateUserWizard 컨트롤의 기본 인터페이스와 같은 사용자 이름, 암호 및 전자 메일만 core 사용자 계정 정보 필요 수집할 단순 계정 만들기 시나리오에 충분 합니다. 그러나 방문자 자신의 계정을 만드는 동안 자신의 홈 타운, 홈 페이지 및 서명을 입력 하 라는 메시지가 표시 하려는 경우에 어떻게? 등록에서 추가 정보를 수집 하려면 CreateUserWizard 컨트롤의 인터페이스를 사용자 지정할 수 있으며이 정보는에서 사용할 수는 `CreatedUser` 이벤트 처리기를 기본 데이터베이스에 추가 레코드를 삽입 합니다.

CreateUserWizard 컨트롤 확장 페이지 개발자는 일련의 정렬 된 정의를 허용 하는 컨트롤은 ASP.NET 마법사 컨트롤 `WizardSteps`합니다. 활성 단계를 렌더링 하 고이 단계를 통해 이동할 방문자를 허용 하는 탐색 인터페이스를 제공 하는 마법사 컨트롤입니다. 마법사 컨트롤 긴 작업을 몇 가지 간단한 단계에 적합 합니다. 마법사 컨트롤에 대 한 자세한 내용은 참조 하세요. [ASP.NET 2.0 Wizard 컨트롤을 사용한 단계별 사용자 인터페이스 만들기](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)합니다.

CreateUserWizard 컨트롤의 기본 태그 정의 두 `WizardSteps`: `CreateUserWizardStep` 고 `CompleteWizardStep`입니다.

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample12.aspx)]

첫 번째 `WizardStep`, `CreateUserWizardStep`, 사용자 이름, 암호, 전자 메일을 요구 하는 인터페이스를 렌더링 합니다. 그녀는 표시 된 방문자가이 정보를 제공 하 고 "Create User"를 클릭 한 후의 `CompleteWizardStep`, 성공 메시지와 계속 단추를 보여 줍니다.

CreateUserWizard 컨트롤의 추가 양식 필드를 포함 하는 인터페이스를 사용자 지정 하려면 다음과 같은 것을 수행할 수 있습니다.

- <strong>하나 이상의 새로 만들기</strong><strong>`WizardStep`</strong><strong>추가 사용자 인터페이스 요소를 포함 하는 s</strong>입니다. 새 추가 하려면 `WizardStep` CreateUserWizard, 클릭는 "추가/제거 `WizardStep` s" 시작 하려면 스마트 태그의 링크를 `WizardStep` 컬렉션 편집기. 여기에서 추가, 제거 또는 마법사의 단계를 다시 정렬할 수 있습니다. 이 방법이이 자습서에 사용 됩니다.

- <strong>변환 된</strong><strong>`CreateUserWizardStep`</strong><strong>에 편집 가능한</strong><strong>`WizardStep`</strong><strong>합니다.</strong> 이 대체 합니다 `CreateUserWizardStep` 가 동일한 `WizardStep` 해당 태그와 일치 하는 사용자 인터페이스를 정의 합니다 `CreateUserWizardStep`' s. 변환 하 여 합니다 `CreateUserWizardStep` 에 `WizardStep` 컨트롤의 위치 또는이 단계에 추가 사용자 인터페이스 요소를 추가할 수 있습니다. 변환할 합니다 `CreateUserWizardStep` 또는 `CompleteWizardStep` 에 편집 가능한 `WizardStep`는 "사용자 지정 만들기 사용자 단계"를 클릭 하거나 컨트롤의 스마트 태그에서 "사용자 지정 완료 단계"의 링크입니다.

- **위의 두 옵션 중 몇 가지 조합을 사용 합니다.**

기억해 야 할 중요 한 사항은 내에서 "Create User" 단추를 클릭할 때 CreateUserWizard 컨트롤의 사용자 계정 만들기 프로세스를 실행 하는 해당 `CreateUserWizardStep`합니다. 여부는 중요 하지 않는 추가적인 `WizardStep` 후 s는 `CreateUserWizardStep` 여부입니다.

사용자 지정을 추가 하는 경우 `WizardStep` CreateUserWizard 컨트롤 사용자 지정의 추가 사용자 입력 수집 `WizardStep` 전이나 후에 배치할 수 있습니다는 `CreateUserWizardStep`합니다. 앞에 배치 되는 경우는 `CreateUserWizardStep` 사용자 지정에서 추가 사용자 입력을 수집 하는 다음 `WizardStep` 수는 `CreatedUser` 이벤트 처리기입니다. 그러나 경우 사용자 지정 `WizardStep` 뒤에 오는 `CreateUserWizardStep` 시간을 기준으로 다음 사용자 지정 `WizardStep` 표시 됩니다 새 사용자 계정을 이미 만든 및 `CreatedUser` 이벤트가 이미 발생 한 합니다.

그림 21 워크플로 보여 줍니다. 때 추가한 `WizardStep` 앞에 `CreateUserWizardStep`. 추가 사용자 정보에 의해 수집 된 이후 합니다 `CreatedUser` 는 업데이트 작업을 수행 해야 하는 모든 이벤트가 발생 합니다 `CreatedUser` 이러한 입력을 가져와 사용에 대 한 이벤트 처리기는 `INSERT` 문의 매개 변수 값 (대신 `DBNull.Value`).


[![CreateUserWizard 워크플로 추가 WizardStep는 CreateUserWizardStep 앞에 오는 경우](storing-additional-user-information-vb/_static/image62.png)](storing-additional-user-information-vb/_static/image61.png)

**그림 21**: The CreateUserWizard 워크플로 때는 추가 `WizardStep` Precedes 합니다 `CreateUserWizardStep` ([클릭 하 여 큰 이미지 보기](storing-additional-user-information-vb/_static/image63.png))


그러나 하는 경우 사용자 지정 `WizardStep` 놓입니다 *후* 는 `CreateUserWizardStep`, 만들기 사용자 계정 프로세스를 사용자에 게 홈 타운, 홈 페이지 또는 서명 입력할 수 전에 발생 합니다. 이러한 경우에이 추가 정보를 삽입할 데이터베이스 사용자 계정을 만든 후에, 그림 22와 같이 해야 합니다.


[![CreateUserWizard 워크플로 추가 WizardStep는 CreateUserWizardStep 뒤에 오는 경우](storing-additional-user-information-vb/_static/image65.png)](storing-additional-user-information-vb/_static/image64.png)

**그림 22**: The CreateUserWizard 워크플로 때는 추가 `WizardStep` 후 제공 되는 `CreateUserWizardStep` ([클릭 하 여 큰 이미지 보기](storing-additional-user-information-vb/_static/image66.png))


그림 22와 같이 워크플로 대기에 레코드를 삽입 하 여 `UserProfiles` 2 단계 완료 될 때까지 테이블입니다. 그러나 방문자는 1 단계 후 브라우저를 닫으면,는 제품이 출시 되었으므로 여기서 사용자 계정이 생성 되었지만 없는 레코드에 추가 된 상태 `UserProfiles`합니다. 한 가지 해결 방법은 사용 하 여 레코드를 포함 하는 것 `NULL` 기본값을 삽입 하거나 `UserProfiles` 에 `CreatedUser` (발생 하는 1 단계 후) 이벤트 처리기 및 2 단계를 완료 한 후 기록이 업데이트 합니다. 이렇게 하면 한 `UserProfiles` 사용자 등록 프로세스가 중간에 종료 하는 경우에 사용자 계정에 대 한 레코드가 추가 됩니다.

이 자습서에 대 한 만들겠습니다 새 `WizardStep` 후에 발생 하는 합니다 `CreateUserWizardStep` 하기 전에 `CompleteWizardStep`합니다. 첫 번째 get에서 WizardStep 배치 하 고 구성 하 고에서는 살펴보겠습니다 코드.

CreateUserWizard 컨트롤의 스마트 태그를 선택 합니다 "추가/제거 `WizardStep` s"를 불러는 `WizardStep` 컬렉션 편집기 대화 상자. 새 `WizardStep`설정, 해당 `ID` 를 `UserSettings`, 해당 `Title` "설정" 하 고 `StepType` 를 `Step`. 다음에 오는 다음 위치를 `CreateUserWizardStep` ("등록 새 계정에 대 한") 하기 전에 `CompleteWizardStep` ("완료"), 그림 23 에서처럼 합니다.


[![CreateUserWizard 컨트롤에 새 WizardStep 추가](storing-additional-user-information-vb/_static/image68.png)](storing-additional-user-information-vb/_static/image67.png)

**그림 23**: 새 추가 `WizardStep` CreateUserWizard 컨트롤 ([클릭 하 여 큰 이미지 보기](storing-additional-user-information-vb/_static/image69.png))


확인을 눌러 닫습니다는 `WizardStep` 컬렉션 편집기 대화 상자. 새 `WizardStep` CreateUserWizard 컨트롤의 업데이트 된 선언적 태그 된 수치로 증명 됩니다.

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample13.aspx)]

새 확인 `<asp:WizardStep>` 요소입니다. 새 사용자의 홈 타운, 홈 페이지 및 여기에 서명을 수집 하는 사용자 인터페이스를 추가 해야 합니다. 선언적 구문 또는 디자이너를 통해이 콘텐츠를 입력할 수 있습니다. 디자이너를 사용 하려면 디자이너의 단계를 참조 하도록 스마트 태그에서 드롭 다운 목록에서 "설정" 단계를 선택 합니다.

> [!NOTE]
> CreateUserWizard 컨트롤의 스마트 태그의 드롭다운 목록을 통해 단계를 선택 하면 업데이트 [ `ActiveStepIndex` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.activestepindex.aspx), 시작 단계 인덱스를 지정 하는 합니다. 따라서 디자이너에서 "설정" 단계를 편집 하려면이 드롭다운 목록에서를 사용 하는 경우 반드시 사용자가 처음 방문 하는 경우이 단계에 표시 되도록 "Sign Up for 새 계정"으로 설정 하 여 `EnhancedCreateUserWizard.aspx` 페이지입니다.


라는 3 개의 TextBox 컨트롤을 포함 하는 "설정" 단계 내의 사용자 인터페이스를 만들 `HomeTown`, `HomepageUrl`, 및 `Signature`합니다. 이 인터페이스를 생성 한 후 CreateUserWizard의 선언적 태그는 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](storing-additional-user-information-vb/samples/sample14.aspx)]

진행 하 고 브라우저를 통해이 페이지를 방문 홈 타운, 홈 페이지 및 서명에 대 한 값을 지정 하는 새 사용자 계정을 만듭니다. 완료 한 후 합니다 `CreateUserWizardStep` 멤버 자격 프레임 워크에서 사용자 계정이 생성 됩니다 및 `CreatedUser` 에 새 행을 추가 하는 이벤트 처리기 실행 `UserProfiles`, 하지만 데이터베이스를 사용 하 여 `NULL` 값 `HomeTown`, `HomepageUrl`, 및 `Signature`. 홈 타운, 홈 페이지 및 서명 입력 한 값은 사용 되지 됩니다. 최종적인 결론은 새 사용자 계정에는 `UserProfiles` 갖는 기록 `HomeTown`, `HomepageUrl`, 및 `Signature` 필드 아직 지정 합니다.

사용자가 입력 한 홈 타운, honepage, 및 서명 값을 사용 하 고 적절 한 업데이트는 "설정" 단계를 수행한 후 코드를 실행 해야 `UserProfiles` 레코드입니다. 마법사의 마법사 단계 사이 이동할 때마다 컨트롤 [ `ActiveStepChanged` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.wizard.activestepchanged.aspx) 발생 합니다. 이 이벤트와 업데이트에 대 한 이벤트 처리기를 만들 수 있습니다는 `UserProfiles` "설정" 단계 완료 되 면 테이블입니다.

CreateUserWizard의에 대 한 이벤트 처리기를 추가 `ActiveStepChanged` 이벤트 다음 코드를 추가 합니다.

[!code-vb[Main](storing-additional-user-information-vb/samples/sample15.vb)]

위의 코드에서는 "완료" 단계 도달 여부를 확인 하 여 시작 합니다. "완료" 단계 "설정" 단계 직후 발생 하므로 다음 방문자에 도달 하면 "완료" 단계 "설정" 단계를 방금 완료 한 그녀 의미 합니다.

이러한 경우에 내에서 텍스트 상자 컨트롤을 프로그래밍 방식으로 참조 해야 합니다 `UserSettings WizardStep`합니다. 첫 번째를 사용 하 여 이렇게 합니다 `FindControl` 프로그래밍 방식으로 참조 하는 방법을 `UserSettings WizardStep`, 다음 텍스트 상자 내에서 참조를 다시는 `WizardStep`합니다. 우리가 실행할 준비가 된 텍스트 상자, 참조 된 후의 `UPDATE` 문입니다. `UPDATE` 문을 동일한 개수의 매개 변수를 `INSERT` 문에서 `CreatedUser` 이벤트 처리기를 여기는 사용자가 제공한 홈 타운, 홈 페이지 및 서명 값을 사용 하지만 합니다.

이 이벤트 처리기를 사용 하 여 방문을 `EnhancedCreateUserWizard.aspx` 브라우저를 통해 페이지 및 홈 타운, 홈 페이지 및 서명에 대 한 값을 지정 하는 새 사용자 계정을 만듭니다. 새 계정을 만든 후 리디렉션되어야 하는 `AdditionalUserInfo.aspx` 페이지에서 방금 입력 홈 타운, 홈 페이지 및 서명 정보를 표시 되는 위치입니다.

> [!NOTE]
> 웹 사이트에 갖고 두 페이지는 방문자를 새 계정을 만들 수 있습니다: `CreatingUserAccounts.aspx` 및 `EnhancedCreateUserWizard.aspx`합니다. 웹 사이트의 사이트 맵 및 로그인 페이지를 가리킵니다 합니다 `CreatingUserAccounts.aspx` 페이지에서 하지만 `CreatingUserAccounts.aspx` 페이지 홈 타운, 홈 페이지 및 시그니처 정보에 대 한 사용자를 묻지 않습니다 하 고 해당 행을 추가 하지 않습니다 `UserProfiles`합니다. 따라서 하거나 업데이트 합니다 `CreatingUserAccounts.aspx` 이 기능을 제공 되도록 페이지 또는 참조 사이트 맵 및 로그인 페이지를 업데이트 `EnhancedCreateUserWizard.aspx` 대신 `CreatingUserAccounts.aspx`합니다. 후자 옵션을 선택 하는 경우 업데이트 해야 합니다 `Membership` 폴더의 `Web.config` 익명 사용자에 대 한 액세스를 허용 하도록 파일을 `EnhancedCreateUserWizard.aspx` 페이지입니다.


## <a name="summary"></a>요약

이 자습서에서는 멤버 자격 프레임 워크 내에서 사용자 계정에 관련 된 데이터를 모델링 하는 것에 대 한 기술에 살펴보았습니다. 특히, 일대일 관계를 공유 하는 데이터 뿐만 아니라 사용자 계정에 일 대 다 관계를 공유 하는 엔터티 모델링 살펴보았습니다. 또한 살펴본이 관계 정보를 표시, 삽입 및 업데이트, SqlDataSource 컨트롤 등을 사용 하는 몇 가지 예제를 사용 하 여 수 ADO.NET 코드를 사용 합니다.

이 자습서는 사용자 계정 확인을 완료합니다. 다음 자습서를 사용 하 여 시작에 대해 역할 기능을 합니다. 역할 framework 살펴보겠습니다 여러 자습서는 다음을 통해 새 역할을 만드는 방법을 참조 하세요 역할을 확인 하려면 사용자가 속한, 방법 및 사용자에 게 역할을 할당 하는 방법 역할 기반 권한 부여를 적용 합니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 2.0의에서 데이터 액세스 및 업데이트](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [ASP.NET 2.0 마법사 컨트롤](https://weblogs.asp.net/scottgu/archive/2006/02/21/438732.aspx)
- [ASP.NET 2.0 Wizard 컨트롤을 사용한 단계별 사용자 인터페이스 만들기](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)
- [사용자 지정 데이터 원본 제어 매개 변수 만들기](http://aspnet.4guysfromrolla.com/articles/110106-1.aspx)
- [CreateUserWizard 컨트롤 사용자 지정](http://aspnet.4guysfromrolla.com/articles/070506-1.aspx)
- [DetailsView 컨트롤 빠른 시작](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/data/detailsview.aspx)
- [ListView 컨트롤을 사용 하 여 데이터를 표시합니다.](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)
- [ASP.NET 2.0의에서 유효성 검사 컨트롤 분석](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)
- [데이터 삽입을 편집 및 삭제](../../data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)
- [ASP.NET에서 폼 유효성 검사](http://www.4guysfromrolla.com/webtech/090200-1.shtml)
- [사용자 지정 사용자 등록 정보를 수집합니다.](https://weblogs.asp.net/scottgu/archive/2006/07/05/Tip_2F00_Trick_3A00_-Gathering-Custom-User-Registration-Information.aspx)
- [ASP.NET 2.0의 프로필](http://www.odetocode.com/Articles/440.aspx)
- [Asp: ListView 컨트롤](https://weblogs.asp.net/scottgu/archive/2007/08/10/the-asp-listview-control-part-1-building-a-product-listing-page-with-clean-css-ui.aspx)
- [사용자 프로필 빠른 시작](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/profile/default.aspx)

### <a name="about-the-author"></a>저자 소개

Scott Mitchell, 여러 ASP/ASP.NET 책의 저자 이자 4GuysFromRolla.com의 설립자 이며 1998 Microsoft 웹 기술을 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는  *[Sams 설명 직접 ASP.NET 2.0 24 시간 동안의](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 합니다. Scott에 도달할 수 있습니다 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 통하거나 저자의 블로그 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사 하는 중...

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)합니다.

> [!div class="step-by-step"]
> [이전](user-based-authorization-vb.md)
