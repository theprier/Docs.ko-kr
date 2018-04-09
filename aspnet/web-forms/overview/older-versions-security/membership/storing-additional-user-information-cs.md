---
uid: web-forms/overview/older-versions-security/membership/storing-additional-user-information-cs
title: 추가 사용자 정보 (C#)를 저장 합니다. | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 매우 기초적인 수준 방명록 응용 프로그램을 구축 하 여이 질문에 대답 합니다 했습니다. 이 과정에서 살펴보겠습니다 modeli에 대 한 다른 옵션 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/18/2008
ms.topic: article
ms.assetid: 1642132a-1ca5-4872-983f-ab59fc8865d3
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-security/membership/storing-additional-user-information-cs
msc.type: authoredcontent
ms.openlocfilehash: e484f63a82ad9ecf1f376143bdc1924e231e0801
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="storing-additional-user-information-c"></a>추가 사용자 정보를 저장 하는 (C#)
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_08_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial08_ExtraUserInfo_cs.pdf)

> 이 자습서에서는 매우 기초적인 수준 방명록 응용 프로그램을 구축 하 여이 질문에 대답 합니다 했습니다. 이 과정에서 데이터베이스에서 사용자 정보를 모델링 하기 위한 다양 한 옵션을 살펴보고 하 고 구성원 프레임 워크에서 만드는 사용자 계정으로이 데이터를 연결 하는 방법을 참조 합니다.


## <a name="introduction"></a>소개

ASP입니다. NET의 멤버 자격 프레임 워크는 사용자가 관리 하기 위한 유연한 인터페이스를 제공 합니다. 멤버 API에는 자격 증명 유효성 검사, 현재 로그온된 한 사용자에 대 한 정보를 검색, 새 사용자 계정을 만들고 삭제 하기 위한 사용자 계정에 다른 규칙 으로부터 메서드도 포함 됩니다. 멤버 자격 프레임 워크에서 각 사용자 계정 자격 증명 유효성 검사 및 필수 사용자 계정 관련 작업 수행에 필요한 속성에만 포함 되어 있습니다. 메서드 및 속성을이 확인 되는 [ `MembershipUser` 클래스](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx), 사용자 계정에 멤버 자격 프레임 워크를 모델링 하 합니다. 이 클래스와 같은 속성에 [ `UserName` ](https://msdn.microsoft.com/library/system.web.security.membershipuser.username.aspx), [ `Email` ](https://msdn.microsoft.com/library/system.web.security.membershipuser.email.aspx), 및 [ `IsLockedOut` ](https://msdn.microsoft.com/library/system.web.security.membershipuser.islockedout.aspx)와 같은 메서드 및 [ `GetPassword` ](https://msdn.microsoft.com/library/system.web.security.membershipuser.getpassword.aspx) 및 [ `UnlockUser` ](https://msdn.microsoft.com/library/system.web.security.membershipuser.unlockuser.aspx)합니다.

종종 응용 프로그램 구성원 프레임 워크에 없는 추가 사용자 정보를 저장 해야 합니다. 예를 들어 온라인 상점 각 사용자가 배송 및 대금 청구 주소, 결제 정보, 배달 기본 설정을 저장 하 고 연락처 전화 번호를 사용 해야 합니다. 또한 각 주문 시스템에는 특정 사용자 계정와 관련이 있습니다.

`MembershipUser` 클래스와 같은 속성을 포함 하지 않는 `PhoneNumber` 또는 `DeliveryPreferences` 또는 `PastOrders`합니다. 따라서 어떻게 म 응용 프로그램에 필요한 사용자 정보를 추적 하 고 구성원 프레임 워크와 통합 하 게? 이 자습서에서는 매우 기초적인 수준 방명록 응용 프로그램을 구축 하 여이 질문에 대답 합니다 했습니다. 이 과정에서 데이터베이스에서 사용자 정보를 모델링 하기 위한 다양 한 옵션을 살펴보고 하 고 구성원 프레임 워크에서 만드는 사용자 계정으로이 데이터를 연결 하는 방법을 참조 합니다. 이제 시작 하겠습니다.

## <a name="step-1-creating-the-guestbook-applications-data-model"></a>1 단계: 방명록 응용 프로그램의 데이터 모델 만들기

데이터베이스에서 사용자 정보를 캡처하고 구성원 프레임 워크에서 만드는 사용자 계정으로 연결을 사용할 수 있는 기술의 여러 가지가 있습니다. 이러한 기법을 보여 주기 위해 자습서 웹 응용 프로그램을 확장 하 여 일종의 사용자 관련 데이터를 캡처할 수 있도록 해야 합니다. (응용 프로그램에서 필요로 하는 테이블 서비스에 응용 프로그램의 데이터 모델을 포함 하는 현재는 `SqlMembershipProvider`.)

인증된 된 사용자 의견을 남겨 수 있는 매우 간단한 방명록 응용 프로그램을 만들어 보겠습니다. 방명록 설명을, 저장할 뿐만 아니라 각 사용자가을 자신의 홈 동, 홈 페이지 및 서명을 저장할 허용 해 보겠습니다. 제공 된 사용자의 홈 동 경우 홈 페이지 및 서명 그 남아 서는 방명록에 각 메시지에 표시 됩니다.

### <a name="adding-theguestbookcommentstable"></a>추가`GuestbookComments`테이블

명명 된 데이터베이스 테이블을 만들 필요 방명록 의견을 캡처하려면 `GuestbookComments` 처럼 열에 있는 `CommentId`, `Subject`, `Body`, 및 `CommentDate`합니다. 각 레코드를 보유 해야는 `GuestbookComments` 테이블 참조 주석으로 처리 한 사용자입니다.

이 테이블에 데이터베이스를 추가 하려면 Visual Studio에서 데이터베이스 탐색기로 이동 하 고 드릴 다운은 `SecurityTutorials` 데이터베이스입니다. Tables 폴더에 단추로 클릭 하 고 새 테이블 추가 선택 합니다. 이것은 새 테이블에 대 한 열을 정의할 수 있는 인터페이스를 표시 합니다.


[![SecurityTutorials 데이터베이스에 새 테이블을 추가 합니다.](storing-additional-user-information-cs/_static/image2.png)](storing-additional-user-information-cs/_static/image1.png)

**그림 1**: 새 테이블을 추가 하는 `SecurityTutorials` 데이터베이스 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image3.png))


다음으로 정의 된 `GuestbookComments`의 열입니다. 명명 된 열을 추가 하 여 시작 `CommentId` 형식의 `uniqueidentifier`합니다. 이 열은는 방명록에서 각 메모를 고유 하 게 식별, 허용 하므로 `NULL` s 하 고 해당 테이블의 기본 키로 표시 합니다. 에 대 한 값을 제공 하는 대신는 `CommentId` 필드에 각 `INSERT`를 나타낼 수 새 `uniqueidentifier` 값 자동으로 생성할지이 필드에 `INSERT` 열의 기본값을 설정 하 여 `NEWID()`합니다. 기본값, 기본 키 및 설정으로 표시,이 첫 번째 필드를 추가한 후에 스크린 샷을 그림 2에 표시 된 화면 비슷해야 합니다.


[![CommentId 라는 기본 열 추가](storing-additional-user-information-cs/_static/image5.png)](storing-additional-user-information-cs/_static/image4.png)

**그림 2**: 기본 열 라는 추가 `CommentId` ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image6.png))


다음으로 명명 된 열을 추가 `Subject` 형식의 `nvarchar(50)` 및 이라는 열 `Body` 형식의 `nvarchar(MAX)`허용 하지 않는, `NULL` s 두 열 모두에 있습니다. 그런 다음, 이라는 열을 추가 `CommentDate` 형식의 `datetime`합니다. Disallow `NULL` 집합과, s는 `CommentDate` 열의 기본값을 `getdate()`합니다.

이제 남은 것 각 방명록 메모와 함께 사용자 계정을 연결 하는 열을 추가 합니다. 한 가지 옵션 라는 열을 추가 하는 것 `UserName` 형식의 `nvarchar(256)`합니다. 이외의 다른 멤버 자격 공급자를 사용 하는 경우이 적절 한 선택은 `SqlMembershipProvider`합니다. 사용할 경우에 `SqlMembershipProvider`이 자습서 시리즈에 있으므로는 `UserName` 열에는 `aspnet_Users` 테이블은 고유 하 게 아닙니다. `aspnet_Users` 테이블의 기본 키가 `UserId` 형식인 `uniqueidentifier`합니다. 따라서는 `GuestbookComments` 테이블 라는 열에 필요 `UserId` 형식의 `uniqueidentifier` (허용 하지 않고 `NULL` 값). 계속 진행 하 고이 열을 추가 합니다.

> [!NOTE]
> 설명한 것 처럼는 [ *SQL Server에서 멤버 자격 스키마 만들기* ](creating-the-membership-schema-in-sql-server-cs.md) 자습서, 멤버 자격 프레임 워크 여러 웹 응용 프로그램을 다른 사용자 계정으로 동일한 공유 하도록 합니다. 사용자 저장소입니다. 다른 응용 프로그램 사용자 계정을 분할 하 여 수행 합니다. 하며 각 사용자 이름을 응용 프로그램 내에서 고유 하 게 보장 하는 동안 동일한 사용자 저장소를 사용 하 여 다른 응용 프로그램에서 동일한 사용자 이름을 사용할 수 있습니다. 복합 `UNIQUE` 제약 조건에는 `aspnet_Users` 테이블에 `UserName` 및 `ApplicationId` 필드 이지만 아닌에 테이블만 `UserName` 필드입니다. 따라서 전원이 aspnet\_사용자 테이블에는 두 개 이상의 레코드가 동일한 `UserName` 값입니다. 그러나, 한 `UNIQUE` 제약 조건에는 `aspnet_Users` 테이블의 `UserId` 필드 (기본 키 이므로). A `UNIQUE` 제약 조건은 없이 간의 외래 키 제약 조건을 설정할 수 없습니다 것 때문에 중요는 `GuestbookComments` 및 `aspnet_Users` 테이블입니다.


추가한 후의 `UserId` 저장 도구 모음에 저장 아이콘을 클릭 하 여 테이블 열입니다. 새 테이블의 이름을 `GuestbookComments`합니다.

와 참석 한 가지 마지막 문제 했으므로 `GuestbookComments` 테이블: 만들어야 하는 [foreign key 제약 조건을](https://msdn.microsoft.com/library/ms175464.aspx) 간에 `GuestbookComments.UserId` 열 및 `aspnet_Users.UserId` 열입니다. 이 위해 외래 키 관계 대화 상자를 시작 하려면 도구 모음에 있는 관계 아이콘을 클릭 합니다. (또는 시작할 수 있습니다이 대화 상자 테이블 디자이너 메뉴로 이동 하 고 관계를 선택 하 여.)

외래 키 관계 대화 상자 왼쪽된 아래에서 추가 단추를 클릭 합니다. 이 관계에 참여 하는 테이블을 정의 해야 하지만 새 외래 키 제약을 추가 됩니다.


[![외래 키 관계 대화 상자를 사용 하 여 테이블의 외래 키 제약 조건을 관리 합니다.](storing-additional-user-information-cs/_static/image8.png)](storing-additional-user-information-cs/_static/image7.png)

**그림 3**: 외래 키 관계 대화 상자를 사용 하 여 테이블의 외래 키 제약 조건 관리 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image9.png))


그런 다음 오른쪽에 있는 "테이블 및 열 사양" 행에 있는 줄임표 아이콘을 클릭 합니다. 이 있는 기본 키 테이블 및 열과 외래 키 열에서 지정할 수 있습니다 테이블 및 열 대화 상자에 시작 됩니다는 `GuestbookComments` 테이블입니다. 특히, 선택 `aspnet_Users` 및 `UserId` 기본 키 테이블 및 열으로 및 `UserId` 에서 `GuestbookComments` 외래 키 열으로 테이블 (그림 4 참조). 기본 및 외래 키 테이블 및 열을 정의한 후 외래 키 관계 대화 상자로 돌아가려면 확인을 클릭 합니다.


[![외래 키 제약 조건 간의 aspnet_Users 및 GuesbookComments 테이블 설정](storing-additional-user-information-cs/_static/image11.png)](storing-additional-user-information-cs/_static/image10.png)

**그림 4**:는 외래 키 제약 조건 간에 설정 된 `aspnet_Users` 및 `GuesbookComments` 테이블 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image12.png))


이 시점에서 외래 키 제약 조건이 설정 되었습니다. 이 제약 조건의 현재 상태를 사용 하면 [관계 무결성](http://en.wikipedia.org/wiki/Referential_integrity) 는 될 수 없으므로 한 방명록 항목이 존재 하지 않는 사용자 계정에 참조를 보장 하 여 두 테이블 간에 합니다. 기본적으로 외래 키 제약 조건을 부모 레코드를 자식 레코드 해당 하는 경우 삭제할 수 하지 못하게 됩니다. 즉, 사용자는 하나 이상의 방명록 메모를 설정 하 고 해당 사용자 계정을 삭제 하려고 하면 다음 자신의 방명록 의견을 먼저 삭제 하지 않는 한 삭제가 실패 합니다.

부모 레코드가 삭제 될 때 자동으로 연결 된 자식 레코드를 삭제 하려면 foreign key 제약 조건은 구성할 수 있습니다. 즉, 자신의 사용자 계정을 삭제 될 때 사용자의 방명록 항목이 자동으로 삭제 되도록이 외래 키 제약 조건을 설정할 수 했습니다. 이를 위해 "INSERT 및 UPDATE 사양" 섹션을 확장 cascade를 지정 하려면 "삭제 규칙" 속성을 설정 합니다.


[![외래 키 제약 조건을 모두 삭제를 구성 합니다.](storing-additional-user-information-cs/_static/image14.png)](storing-additional-user-information-cs/_static/image13.png)

**그림 5**: 모두 삭제 하도록 외래 키 제약 조건을 구성 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image15.png))


외래 키 제약 조건을 저장 하려면 외래 키 관계를 종료 하려면 닫기 단추를 클릭 합니다. 다음 테이블 및이 저장 하려면 도구 모음에 저장 아이콘을 클릭 관계입니다.

### <a name="storing-the-users-home-town-homepage-and-signature"></a>사용자의 홈 동, 홈 페이지 및 서명을 저장

`GuestbookComments` 테이블에는 사용자 계정으로는 일 대 다 관계를 공유 하는 정보를 저장 하는 방법을 보여 줍니다. 각 사용자 계정 관련된 댓글 임의 개수의 수 없으므로이 관계를 특정 사용자에 게 각 추가 다시 연결 하는 열이 포함 된 주석 집합을 저장할 테이블을 만들어 모델링 됩니다. 사용 하는 경우는 `SqlMembershipProvider`,이 링크를 가장 잘 라는 열을 만들어 설정 `UserId` 형식의 `uniqueidentifier` 및이 열 간의 외래 키 제약 조건 및 `aspnet_Users.UserId`합니다.

이제 사용자의 홈 동, 홈 페이지 및 자신의 방명록 의견에 표시 됩니다는 서명을 저장 하려면 각 사용자 계정으로 세 개의 열을 연결 해야 합니다. 다양 한 방법으로이를 위해 숫자:

- <strong>새 열을 추가할는</strong><strong>`aspnet_Users`</strong><strong>또는</strong><strong>`aspnet_Membership`</strong><strong>테이블입니다.</strong> 사용 하는 스키마를 수정 하기 때문에이 방법은 권장 하지 않을 필자는 `SqlMembershipProvider`합니다. 이와 같이이 결정 하면 향후 다닐 위험할 수 있습니다. 예를 들어 경우 이후 버전의 ASP.NET 사용 하 여 다른 `SqlMembershipProvider` 스키마입니다. Microsoft ASP.NET 2.0을 마이그레이션하는 도구를 포함 될 수 있습니다 `SqlMembershipProvider` ASP.NET 2.0을 수정한 경우 이지만 새 스키마로 데이터 `SqlMembershipProvider` 스키마에서 이러한 변환을 불가능할 수도 있습니다.

- **ASP를 사용 합니다. NET의 프로필 framework, 홈 동, 홈 페이지 및 서명을에 프로필 속성을 정의 합니다.** ASP.NET 추가 사용자 관련 데이터를 저장 하도록 디자인 된 프레임 워크 프로필에 포함 되어 있습니다. 멤버 자격 프레임 워크와 같은 프로필 framework 공급자 모델 기반 만들어집니다. .NET Framework와 함께 제공 되는 `SqlProfileProvider` 된 경우 SQL Server 데이터베이스에 프로필 데이터를 저장 합니다. 데이터베이스에 이미 사용 하는 테이블이 실제로 `SqlProfileProvider` (`aspnet_Profile`)는 응용 프로그램 서비스를 다시 추가 하는 경우 추가 된는 <a id="_msoanchor_2"> </a> [ *SQL에서 멤버 자격 스키마 만들기 서버* ](creating-the-membership-schema-in-sql-server-cs.md) 자습서입니다.   
  프로필 프레임 워크의 주요 장점은에서 프로필 속성을 정의 하는 개발자를 위한 수 있다는 점입니다 `Web.config` – 기본 데이터 저장소와 프로필 데이터를 직렬화 하는 데 작성 해야 할 코드가 없습니다. 간단히 프로필 속성 집합을 정의 하 고 코드에서 작업할 수를 쉽게 것입니다. 그러나 프로필 시스템 개선의 여지가 버전 관리에 관한 권장 될 응용 프로그램에서 새 사용자 고유의 속성을 나중 또는 제거 하거나 수정 하 고, 기존 세션에 추가할 수를 예상 다음 프로필 프레임 워크 되지 않을 수 있습니다 위치 하는 경우는  최상의 옵션입니다. 또한는 `SqlProfileProvider` 프로필 속성 (예:는 홈 동 뉴욕은 사용자 수) 프로필 데이터에 대해 직접 쿼리를 실행할 수 없도록 상태로 다음 하는 매우 비 정규화 된 방식으로 저장 합니다.   
  프로필 프레임 워크에 대 한 자세한 내용은이 자습서의 끝에 "추가 정보" 섹션을 참조 하십시오.

- <strong>데이터베이스에 새 테이블에 이러한 3 개의 열을 추가 하 고이 테이블 간에 일대일 관계를 설정 하 고</strong><strong>`aspnet_Users`</strong><strong>합니다.</strong> 이 방법은 프로필 프레임 워크와 보다 약간 더 많은 작업이 하지만 데이터베이스에서 추가 사용자 속성은 모델링 하는 방법의 최대 유연성을 제공 합니다. 이 자습서에 사용 될 옵션입니다.

라는 새 테이블을 만들겠습니다 `UserProfiles` 홈 동, 홈 페이지 및 각 사용자에 대 한 서명을 저장 합니다. 데이터베이스 탐색기 창에서 테이블 폴더 단추로 클릭 하 고 새 테이블을 만들려면 선택 합니다. 첫 번째 열의 이름을 `UserId` 하 고 유형을 설정 하 고 `uniqueidentifier`합니다. Disallow `NULL` 값 및 기본 키로 열을 표시 합니다. 다음으로 명명 된 열을 추가: `HomeTown` 형식의 `nvarchar(50)`; `HomepageUrl` 형식의 `nvarchar(100)`; 및 형식 서명을 `nvarchar(500)`합니다. 수락할 수 있는 이러한 세 개의 열이 각각 한 `NULL` 값입니다.


[![UserProfiles 테이블 만들기](storing-additional-user-information-cs/_static/image17.png)](storing-additional-user-information-cs/_static/image16.png)

**그림 6**: 만들기는 `UserProfiles` 테이블 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image18.png))


테이블을 저장 하 고 이름을 `UserProfiles`합니다. 마지막으로, 간의 외래 키 제약 조건을 설정는 `UserProfiles` 테이블의 `UserId` 필드와 `aspnet_Users.UserId` 필드입니다. 간의 외래 키 제약 조건을 동일한 방식으로 `GuestbookComments` 및 `aspnet_Users` 테이블, 연계 삭제가 제한이 있습니다. 이후는 `UserId` 필드에 `UserProfiles` 이 주 키, 이렇게 하면 것에 둘 이상의 레코드는 `UserProfiles` 각 사용자 계정에 대 한 테이블입니다. 이러한 유형의 관계 일대일로 참조 됩니다.

만든 데이터 모델을 만들었으므로 이제 해당 사용할 준비가 됩니다. 단계 2와 3에 현재 로그온된 한 사용자 확인 하 고 홈 동, 홈 페이지 및 시그니처 정보를 편집할 수 방법을 살펴보겠습니다. 4 단계에서에서 인증 된 사용자가 방명록에 새 메모를 제출 하 고 기존 서버를 볼 수에 대 한 인터페이스를 만듭니다.

## <a name="step-2-displaying-the-users-home-town-homepage-and-signature"></a>2 단계: 사용자의 홈 동, 홈 페이지 및 서명을 표시

다양 한 방법으로 현재 로그온된 한 사용자를 보고 그의 홈 동, 홈 페이지 및 시그니처 정보를 편집할 수 있도록 가지가 있습니다. 텍스트 상자와 사용자 인터페이스를 수동으로 만들 수 있습니다 및 데이터 DetailsView 컨트롤 등의 웹 컨트롤 중 하나는 레이블 컨트롤 또는에서는 사용할 수 있습니다. 데이터베이스를 수행 하려면 `SELECT` 및 `UPDATE` ADO.NET를 작성할 수 있습니다 페이지의 코드 숨김 클래스의 코드 문이나, 또는 SqlDataSource 하는 선언적 방법을 사용 합니다. 이상적으로 응용 프로그램에서는 하거나 호출할 수 프로그래밍 방식으로 페이지의 코드 숨김 클래스에서 또는 ObjectDataSource 컨트롤을 통해 선언적으로 하는 계층화 된 아키텍처를 포함 됩니다.

이 자습서 시리즈는 폼 인증, 권한 부여, 사용자 계정 및 역할에 중점을 두고 있으므로 사용할 수 없으므로 이러한 다른 데이터 액세스 옵션 또는 SQL 문을 직접 실행 보다 선호 하는 계층화 된 아키텍처 됩니다 이유에 대 한 자세한 설명은 ASP.NET 페이지. DetailsView 및 – 빠르고 쉬운 옵션-SqlDataSource를 사용 하는 과정을 안내를 하겠습니다 하지만 설명 된 개념은 대체 웹 컨트롤 및 데이터 액세스 논리 확실히 적용할 수 있습니다. 자세한 내용은 ASP.NET의 데이터로 작업 하는 방법에 대 한 참조 내 *[ASP.NET 2.0에서 데이터 작업](../../data-access/index.md)* 자습서 시리즈 합니다.

열기는 `AdditionalUserInfo.aspx` 페이지에 `Membership` 폴더 설정 페이지에 DetailsView 컨트롤을 추가 하 고 해당 `ID` 속성을 `UserProfile` 정리 및 해당 `Width` 및 `Height` 속성입니다. DetailsView의 스마트 태그를 확장 하 고 새 데이터 소스 제어에 연결 하려면 선택 합니다. 데이터 소스 구성 마법사 시작 됩니다 (그림 7 참조). 첫 번째 단계 데이터 원본 유형을 지정할 수 있습니다. 에 직접 연결 해야 것 이므로 `SecurityTutorials` 데이터베이스, 데이터베이스 아이콘을 지정 하는 `ID` 으로 `UserProfileDataSource`합니다.


[![UserProfileDataSource 라는 새 SqlDataSource 컨트롤 추가](storing-additional-user-information-cs/_static/image20.png)](storing-additional-user-information-cs/_static/image19.png)

**그림 7**: 새 SqlDataSource 컨트롤 라는 추가 `UserProfileDataSource` ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image21.png))


다음 화면에서 사용할 데이터베이스를 묻는 메시지가 나타납니다. 연결 문자열을 이미 정의한 `Web.config` 에 대 한는 `SecurityTutorials` 데이터베이스입니다. 이 연결 문자열 이름 – `SecurityTutorialsConnectionString` – 드롭다운 목록에 있어야 합니다. 이 옵션을 선택 하 고 클릭 합니다.


[![SecurityTutorialsConnectionString 드롭 다운 목록에서 선택](storing-additional-user-information-cs/_static/image23.png)](storing-additional-user-information-cs/_static/image22.png)

**그림 8**: 선택 `SecurityTutorialsConnectionString` 드롭 다운 목록에서 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image24.png))


후속 화면 요청 지정 하면 테이블 및 열을 쿼리 합니다. 선택 된 `UserProfiles` 드롭 다운 목록에서 테이블 및 모든 열을 확인 합니다.


[![Bring UserProfiles 테이블에서 모든 열의 백업](storing-additional-user-information-cs/_static/image26.png)](storing-additional-user-information-cs/_static/image25.png)

**그림 9**: 상태로 다시 모든 열을 `UserProfiles` 테이블 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image27.png))


그림 9 반환의 현재 쿼리가 *모든* 에 있는 레코드의 `UserProfiles`, 현재 로그온된 한 사용자의 레코드에만 관심이 있지만 합니다. 추가 하는 `WHERE` 절을 클릭는 `WHERE` 단추 추가를 `WHERE` 절 대화 상자 (그림 10 참조). 여기에서 필터링 할 열, 연산자 및 필터 매개 변수의 소스를 선택할 수 있습니다. 선택 `UserId` 열 및 해당 연산자 "=".

그러나 반환 하려면 현재 로그온된 사용자의 기본 제공 매개 변수 소스가 없다는 `UserId` 값입니다. 이 값을 프로그래밍 방식으로 가져올 필요 합니다. 따라서, "None" 단추를 클릭 추가 매개 변수를 추가 하려면 한 확인을 클릭 한 다음 소스 드롭 다운 목록을 설정 합니다.


[![사용자 Id 열에서 필터 매개 변수를 추가 합니다.](storing-additional-user-information-cs/_static/image29.png)](storing-additional-user-information-cs/_static/image28.png)

**그림 10**:에서 Filter 매개 변수 추가 `UserId` 열 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image30.png))


확인을 클릭 하면 그림 9에 표시 된 화면에 반환 됩니다. 그러나이 이번에 SQL 쿼리에 화면 맨 아래에 포함 됩니다는 `WHERE` 절. "테스트 쿼리" 화면으로 이동 하려면 다음을 클릭 합니다. 쿼리를 실행할 수는 여기에서 결과 확인 합니다. 마법사를 완료 하려면 마침을 클릭 합니다.

데이터 소스 구성 마법사를 완료 되 면 Visual Studio 마법사에 지정 된 설정에 따라 SqlDataSource 컨트롤을 만듭니다. 또한 수동으로 BoundFields에 추가 SqlDataSource에서 반환 된 각 열에 대 한 DetailsView `SelectCommand`합니다. 표시할 필요가 없습니다는 `UserId` 필드에 DetailsView, 사용자가이 값을 알고 필요가 없기 때문입니다. DetailsView 컨트롤의 선언적 태그에서 직접이 필드를 제거 하거나 "편집 필드"를 클릭 하 여 스마트 태그에서 연결할 수 있습니다.

이 시점에서 페이지의 선언적 태그는 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample1.aspx)]

SqlDataSource 컨트롤의 프로그래밍 방식으로 공간을 `UserId` 매개 변수를 현재 로그인된 한 사용자의 `UserId` 전에 데이터를 선택 합니다. SqlDataSource의에 대 한 이벤트 처리기를 만들어이 작업을 수행할 수 수 `Selecting` 이벤트에 다음을 추가 하 고 있는 코드:

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample2.cs)]

호출 하 여 현재 로그온된 한 사용자에 대 한 참조를 가져오는 방법으로 시작 하는 위의 코드는 `Membership` 클래스의 `GetUser` 메서드. 반환 합니다.는 `MembershipUser` 개체의 `ProviderUserKey` 속성에 포함 된 `UserId`합니다. `UserId` SqlDataSource의 값이 할당 한 다음 `@UserId` 매개 변수입니다.

> [!NOTE]
> `Membership.GetUser()` 메서드는 현재 로그온된 한 사용자에 대 한 정보를 반환 합니다. 익명 사용자 페이지를 방문 하는 경우의 값을 반환 합니다 `null`합니다. 이러한 경우를 나타낼는 `NullReferenceException` 을 읽는 동안 코드의 다음 줄에는 `ProviderUserKey` 속성입니다. 물론, 걱정할 필요가 없습니다 `Membership.GetUser()` 반환는 `null` 값에 `AdditionalUserInfo.aspx` 인증 된 사용자만이 폴더에 ASP.NET 리소스에 액세스할 수 있도록 URL 권한 부여 이전 자습서에서 구성한 때문에 페이지입니다. 익명 액세스가 허용 됩니다 페이지에 현재 로그온된 한 사용자에 대 한 정보에 액세스 해야 할 경우 있는지를 확인할 수 있는지 확인 이외`null MembershipUser` 개체에서 반환 되는 `GetUser()` 해당 속성을 참조 하기 전에 메서드.


방문 하는 경우는 `AdditionalUserInfo.aspx` 페이지는 브라우저를 통해 나타납니다 빈 페이지 지정 했으므로 아직 행을 추가 하는 `UserProfiles` 테이블입니다. 6 단계에서에서 살펴보겠습니다 CreateUserWizard 컨트롤에 새 행을 자동으로 추가 하려면 사용자 지정 하는 `UserProfiles` 새 사용자 계정이 만들어질 때 테이블입니다. 그러나 지금은 해야 합니다 수동으로 테이블의 레코드를 만듭니다.

Visual Studio에서 데이터베이스 탐색기로 이동 하 고 테이블 폴더를 확장 합니다. 마우스 오른쪽 단추로 클릭는 `aspnet_Users` 테이블 및 테이블의 레코드를 보려면 "테이블 데이터 표시"를 선택;에 대 한 동일한 작업을 수행 합니다.는 `UserProfiles` 테이블입니다. 그림 11 세로 바둑판식으로 배열 하는 경우 이러한 결과 보여 줍니다. 내 데이터베이스는 현재 `aspnet_Users` 1 세, Fred 및 Tito에 대 한 레코드가 있지만 레코드 없음는 `UserProfiles` 테이블입니다.


[![표시 되는 aspnet_Users 내용과 UserProfiles 테이블](storing-additional-user-information-cs/_static/image32.png)](storing-additional-user-information-cs/_static/image31.png)

**그림 11**: The 내용의 `aspnet_Users` 및 `UserProfiles` 테이블이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image33.png))


새 레코드를 추가 `UserProfiles` 에 대 한 값을 수동으로 입력 하 여 테이블의 `HomeTown`, `HomepageUrl`, 및 `Signature` 필드입니다. 유효한 얻으려고 하는 가장 쉬운 방법은 `UserId` 새 값 `UserProfiles` 레코드는 선택 하는 `UserId` 의 특정 사용자 계정에서 필드는 `aspnet_Users` 테이블 및 붙여 넣기에 `UserId` 필드에 `UserProfiles`합니다. 그림 12는 `UserProfiles` 1 세에 대 한 새 레코드를 추가한 후 테이블입니다.


[![레코드에 대 한 1 세 UserProfiles에 추가 된](storing-additional-user-information-cs/_static/image35.png)](storing-additional-user-information-cs/_static/image34.png)

**그림 12**: A 레코드에 추가 된 `UserProfiles` 1 세에 대 한 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image36.png))


으로 돌아와서는 `AdditionalUserInfo.aspx` 페이지에서 1 세로 로그인 합니다. 그림 13에서 볼 수 있듯이 1 세의 설정이 표시 됩니다.


[![현재 방문 사용자가 His 설정 표시](storing-additional-user-information-cs/_static/image38.png)](storing-additional-user-information-cs/_static/image37.png)

**그림 13**: The 현재 방문 사용자가 His 설정 표시 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image39.png))


> [!NOTE]
> 이동을 수동으로 추가의 레코드는 `UserProfiles` 각 멤버 자격 사용자에 대 한 테이블입니다. 6 단계에서에서 살펴보겠습니다 CreateUserWizard 컨트롤에 새 행을 자동으로 추가 하려면 사용자 지정 하는 `UserProfiles` 새 사용자 계정이 만들어질 때 테이블입니다.


## <a name="step-3-allowing-the-user-to-edit-his-home-town-homepage-and-signature"></a>3 단계: 사용자가 자신의 홈 동, 홈 페이지 및 서명을 편집할 수 있도록

현재 로그인된 한 사용자를 자신의 홈 동, 홈 페이지 및 서명 설정을 볼 수는 시점에서 있지만 아직 수정할 수 없습니다. 데이터를 편집할 수 있도록에 보겠습니다 DetailsView 컨트롤을 업데이트 합니다.

가장 먼저 해야 할 추가 되는 `UpdateCommand` SqlDataSource에 대 한 지정 하는 `UPDATE` 에 실행할 문 및 해당 매개 변수에 있습니다. SqlDataSource를 선택 하 고 속성 창에서 명령 및 매개 변수 편집기 대화 상자를 표시할 UpdateQuery 속성 옆의 줄임표를 클릭 합니다. 다음과 같이 입력 `UPDATE` 문을 상자에 붙여넣습니다.

[!code-sql[Main](storing-additional-user-information-cs/samples/sample3.sql)]

SqlDataSource 컨트롤의 매개 변수를 만드는 "매개 변수 새로 고침" 단추를 클릭 `UpdateParameters` 컬렉션에서 매개 변수 마다는 `UPDATE` 문. 모든 매개 변수 집합에 대 한 소스를 None으로 두고 대화 상자를 완료 하려면 확인 단추를 클릭 합니다.


[![SqlDataSource의 UpdateCommand 및 UpdateParameters 지정](storing-additional-user-information-cs/_static/image41.png)](storing-additional-user-information-cs/_static/image40.png)

**그림 14**: SqlDataSource의 지정 `UpdateCommand` 및 `UpdateParameters` ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image42.png))


추가 된 항목으로 인해 이제를 지원할 수 있는 편집 DetailsView SqlDataSource 컨트롤에 만들었습니다. DetailsView의 스마트 태그에서 확인 "편집 사용" 확인란을 선택 합니다. 컨트롤의 한 CommandField 추가 `Fields` 사용 하 여 컬렉션의 `ShowEditButton` 속성이 True로 설정 합니다. 이 읽기 전용 모드 및 업데이트에 DetailsView 표시 되 고 취소 단추에 표시 될 때 편집 모드로 편집 단추를 렌더링 합니다. 편집을 클릭 하 여 사용자를 요구 하는 대신 하지만 수 DetailsView 렌더링에에서 있는 "편집 가능한 항상" 상태 DetailsView 컨트롤을 설정 하 여 [ `DefaultMode` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.defaultmode.aspx) 를 `Edit`합니다.

이러한 변경 내용으로 DetailsView 컨트롤의 선언적 태그는 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample4.aspx)]

CommandField 추가 및 `DefaultMode` 속성입니다.

계속 진행 하 고 브라우저를 통해이 페이지를 테스트 합니다. 해당 레코드를 가진 사용자가을 방문할 때 `UserProfiles`, 사용자의 설정을 편집 가능한 인터페이스에 표시 됩니다.


[![DetailsView 편집 가능한 인터페이스를 렌더링합니다.](storing-additional-user-information-cs/_static/image44.png)](storing-additional-user-information-cs/_static/image43.png)

**그림 15**: DetailsView 편집 가능한 인터페이스를 렌더링 합니다. ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image45.png))


시도 값을 변경 하 고 업데이트 단추를 클릭 합니다. 아무 작업도 수행 처럼 표시 됩니다. 다시 게시 하 고 값이 데이터베이스에 저장 됩니다 있지만 저장 발생 한 시각적 알 수 없습니다.

이 해결 하려면 Visual Studio 돌아가서 DetailsView 위에 Label 컨트롤을 추가 합니다. 설정의 `ID` 를 `SettingsUpdatedMessage`, 해당 `Text` 속성을 "설정에 업데이트 되지 않은 경우" 및 해당 `Visible` 및 `EnableViewState` 속성을 `false`합니다.

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample5.aspx)]

표시 해야는 `SettingsUpdatedMessage` DetailsView 업데이트 될 때마다 레이블을 지정 합니다. DetailsView의에 대 한 이벤트 처리기를 만들고이를 위해 `ItemUpdated` 이벤트를 다음 코드를 추가 합니다.

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample6.cs)]

으로 돌아와서는 `AdditionalUserInfo.aspx` 브라우저를 통해 페이지와 데이터를 업데이트 합니다. 이 이번에는 유용한 상태 메시지가 표시 됩니다.


[![간단한 메시지가 표시 되는 경우의 설정이 업데이트 되는](storing-additional-user-information-cs/_static/image47.png)](storing-additional-user-information-cs/_static/image46.png)

**그림 16**: 설정이 업데이트 되는 짧은 메시지가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image48.png))


> [!NOTE]
> DetailsView 컨트롤의 편집 인터페이스 leaves 권장 될 많습니다. 표준 크기의 입력란을 사용 하지만 서명 필드는 여러 줄 텍스트 상자 될 것입니다. RegularExpressionValidator 된 홈 페이지 URL을 입력 하는 경우 시작 되도록 "http://" 또는 "https://"는 것 같습니다. DetailsView 컨트롤에는 또한 이후에 해당 `DefaultMode` 속성이로 설정 `Edit`, "취소" 단추가 아무 작업도 수행 하지 않습니다. 그 중 하나를 제거 해야 하거나를 클릭 하면 사용자를 리디렉션합니다 다른 페이지 (예: `~/Default.aspx`). I 이러한 향상 된 판독기에 대 한 연습으로 둡니다.


### <a name="adding-a-link-to-theadditionaluserinfoaspxpage-in-the-master-page"></a>추가에 대 한 링크는`AdditionalUserInfo.aspx`마스터 페이지의 페이지

현재 웹 사이트에 대 한 연결 제공 하지 않습니다는 `AdditionalUserInfo.aspx` 페이지. 도달 하는 유일한 방법은 브라우저의 주소 표시줄에 직접 페이지의 URL을 입력 하는 것입니다. 이 페이지에 대 한 링크를 추가 해 보겠습니다는 `Site.master` 마스터 페이지입니다.

마스터 페이지에는 LoginView 웹 컨트롤에 회수 해당 `LoginContent` ContentPlaceHolder 인증 되 고 익명 방문자에 대 한 다른 태그를 표시 하는 합니다. LoginView 컨트롤의 업데이트 `LoggedInTemplate` 에 링크를 포함 하는 `AdditionalUserInfo.aspx` 페이지. LoginView 이러한 변경을 수행한 후 컨트롤의 선언적 태그는 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample7.aspx)]

추가 `lnkUpdateSettings` 하이퍼링크 컨트롤에는 `LoggedInTemplate`합니다. 위치에이 링크와 함께 인증 된 사용자 자신의 홈 동, 홈 페이지 및 서명을 설정 확인 및 수정 하려면 페이지를 빠르게 이동할 수 있습니다.

## <a name="step-4-adding-new-guestbook-comments"></a>4 단계: 새 방명록 주석 추가

`Guestbook.aspx` 인증 된 사용자는 방명록 볼 하 고 명령을 남길 수 있는 페이지입니다. 새 방명록 주석을 추가 하는 인터페이스를 만드는 것부터 시작 하겠습니다.

열기는 `Guestbook.aspx` Visual Studio에서 페이지 하 고 새 메모의 제목 및 본문에 대 한 두 개의 TextBox 컨트롤 구성 된 사용자 인터페이스를 구성 합니다. 첫 번째 TextBox 컨트롤의 설정 `ID` 속성을 `Subject` 및 해당 `Columns` 속성 40; 설정된 초 `ID` 를 `Body`, 해당 `TextMode` 를 `MultiLine`, 및 해당 `Width` 및 `Rows` 속성을 "95%" 및 8, 각각. 사용자 인터페이스를 완료 하려면 라는 단추 웹 컨트롤을 추가 `PostCommentButton` 설정 하 고 해당 `Text` 속성을 "주석 Post"입니다.

각 방명록 메모 제목 및 본문을 필요한 하므로 각 텍스트 상자에 대 한 한 RequiredFieldValidator를 추가 합니다. 설정의 `ValidationGroup` "EnterComment"; 이러한 컨트롤의 속성 설정 마찬가지로,는 `PostCommentButton` 컨트롤의 `ValidationGroup` 속성을 "EnterComment"입니다. 대 한 자세한 내용은 ASP 합니다. NET의 유효성 검사 컨트롤을 체크 아웃 [asp.net에서 폼 유효성](http://www.4guysfromrolla.com/webtech/090200-1.shtml), [ASP.NET 2.0에서 유효성 검사 컨트롤 나누어서](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx), 및 [유효성 검사 서버 컨트롤 자습서](http://www.w3schools.com/aspnet/aspnet_refvalidationcontrols.asp) [W3Schools](http://www.w3schools.com/)합니다.

사용자 인터페이스를 만들어 후 다음과 같은 페이지의 선언적 태그가 표시 됩니다.

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample8.aspx)]

우리의 다음 작업은 완료 사용자 인터페이스에 새 레코드를 삽입 하는 `GuestbookComments` 하면 테이블의 `PostCommentButton` 를 클릭 합니다. 여러 가지 방법으로이 작업을 수행할 수 있습니다: 단추의 ADO.NET 코드를 작성할 수 있습니다 `Click` ; 이벤트 처리기 구성에 페이지를 SqlDataSource 컨트롤을 추가할 수는 `InsertCommand`, 한 다음 호출 해당 `Insert` 에서 메서드는 `Click` 이벤트 처리기; 또는에서이 기능을 호출을 새 방명록 주석 삽입에 관련 된 중간 계층을 작성할 수 있습니다는 `Click` 이벤트 처리기입니다. 여기서는 SqlDataSource를 사용 하 여 3 단계에서에서 살펴본 후 보겠습니다 ADO.NET 코드 여기 사용 됩니다.

> [!NOTE]
> Microsoft SQL Server 데이터베이스에서 데이터를 프로그래밍 방식으로 액세스 하는 데 사용 하는 ADO.NET 클래스에는 `System.Data.SqlClient` 네임 스페이스입니다. 페이지의 코드 숨김 클래스로이 네임 스페이스를 가져올 해야 할 수 있습니다 (즉, `using System.Data.SqlClient;`).


에 대 한 이벤트 처리기를 만들고는 `PostCommentButton`의 `Click` 이벤트를 다음 코드를 추가 합니다.

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample9.cs)]

`Click` 사용자가 제공한 데이터가 유효한 지 확인 하 여 이벤트 처리기를 시작 합니다. 그렇지 않은 경우 이벤트 처리기는 레코드를 삽입 하기 전에 종료 됩니다. 제공 된 데이터가 유효 가정 하 고 현재 로그온된 한 사용자의 `UserId` 값 검색 하 고에 저장 되는 `currentUserId` 지역 변수입니다. 제공 해야 하기 때문에이 값이 필요한 한 `UserId` 에 레코드 삽입 시 값 `GuestbookComments`합니다.

그런 다음, 연결에 대 한 문자열의 `SecurityTutorials` 데이터베이스에서 검색 됩니다 `Web.config` 및 `INSERT` SQL 문을 지정 합니다. A `SqlConnection` 개체가 다음 생성 되 고 열립니다. 그런 다음는 `SqlCommand` 개체가 생성 되 고 매개 변수 값에 사용는 `INSERT` 쿼리 할당 됩니다. `INSERT` 문을 다음 실행 하 고 연결이 종료 됩니다. 이벤트 처리기의 끝에는 `Subject` 및 `Body` 입력란 `Text` 사용자의 값이 다시 게시 간에 유지 되지 있도록 속성이 지워집니다.

계속를 브라우저에서이 페이지를 테스트 합니다. 이 페이지에 존재 하므로 `Membership` 폴더 액세스할 수 없는 익명 방문자에 게 있습니다. 따라서 먼저 (있는 경우 아직)에 로그온 해야 합니다. 값을 입력에서 `Subject` 및 `Body` 텍스트 상자를 클릭 하 고는 `PostCommentButton` 단추입니다. 이렇게 하면 새 레코드에 추가할 `GuestbookComments`합니다. 다시 게시 될 제목 및 본문을 제공 하는 텍스트 상자에서 초기화 됩니다.

클릭 한 후의 `PostCommentButton` 확인 표시가 나타납니다 시각적 피드백은 없습니다는 방명록에 주석 추가 합니다. 계속 5 단계에서에서 작업이 수행 됩니다 기존 방명록 메모를 표시 하려면이 페이지를 업데이트 해야 합니다. 위해, 되 면 방금 추가 된 주석은 적절 한 시각적 피드백을 제공 하는 주석 목록에 표시 됩니다. 지금은 방명록 메모의 내용을 검사 하 여 저장 된 것을 확인는 `GuestbookComments` 테이블입니다.

그림 17의 내용이 표시는 `GuestbookComments` 테이블 두 주석이 있습니다.


[![GuestbookComments 표에 방명록 의견](storing-additional-user-information-cs/_static/image50.png)](storing-additional-user-information-cs/_static/image49.png)

**그림 17**:의 방명록 주석을 볼 수는 `GuestbookComments` 테이블 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image51.png))


> [!NOTE]
> 사용자가 잠재적으로 포함 된 방명록 주석을 삽입 하는 HTML – ASP.NET과 같은 위험한 태그 –에서 throw 한 `HttpRequestValidationException`합니다. 이 예외를 throw 이유 및 사용자가 잠재적으로 위험한 값을 제출 하도록 허용 하는 방법에 대 한 자세한 내용은 참조는 [요청 유효성 검사 백서](../../../../whitepapers/request-validation.md)합니다.


## <a name="step-5-listing-the-existing-guestbook-comments"></a>5 단계: 기존 방명록 주석 나열

메모를 방문한 사용자를 종료 하는 것 외에도 `Guestbook.aspx` 페이지도 방명록의 기존 주석을 보려면 수 있어야 합니다. 이를 위해 라는 ListView 컨트롤을 추가 `CommentList` 페이지 맨 아래에 있습니다.

> [!NOTE]
> ListView 컨트롤을 ASP.NET 3.5 버전 새로운 기능입니다. 사용자 지정 가능 하 고 유연한 레이아웃으로 항목의 목록을 표시 아직 여전히 기본 제공 편집, 삽입, 삭제, 페이징 및 정렬을 GridView 등과 같은 기능을 제공 하도록 설계 않았습니다. ASP.NET 2.0을 사용 하는 경우에 DataList 또는 반복기 컨트롤을 대신 사용 해야 합니다. ListView 사용에 대 한 자세한 내용은 참조 하십시오. [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 블로그 항목- [asp: ListView 컨트롤](https://weblogs.asp.net/scottgu/archive/2007/08/10/the-asp-listview-control-part-1-building-a-product-listing-page-with-clean-css-ui.aspx), 내 문서 및 [ListView 컨트롤을 사용 하 여 데이터 표시](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)합니다.


ListView의 스마트 태그를 열고 데이터 소스 선택 드롭다운 목록에서 새 데이터 소스에 컨트롤 바인딩 합니다. 2 단계에서에서 설명한 것 처럼 데이터 소스 구성 마법사 시작 됩니다. 데이터베이스 아이콘을 선택, 결과 SqlDataSource 이름을 `CommentsDataSource`, 확인을 클릭 합니다. 다음으로, 선택는 `SecurityTutorialsConnectionString` 연결 드롭 다운 목록에서 문자열을 다음을 클릭 합니다.

이 시점에서 2 단계에서에서 지정한 기 데이터 쿼리를 선택 하 여는 `UserProfiles` 드롭 다운 목록에서 테이블을 반환할 열을 선택 (그림 9를 다시 참조). 그러나이 이번에 하려고 뿐만 아니라 레코드를 다시 가져오는 SQL 문을 만들 `GuestbookComments`, 하지만 또한 메모를 만든의 홈 동, 홈 페이지, 서명 및 사용자 이름입니다. 따라서 "사용자 지정 SQL 문 또는 저장된 프로시저 지정" 라디오 단추를 선택 하 고 클릭 합니다.

그러면 "정의 사용자 지정 문 또는 저장 프로시저" 화면이 표시 됩니다. 그래픽으로 쿼리를 작성 하려면 쿼리 작성기 단추를 클릭 합니다. 쿼리 작성기에서 쿼리 하려는 테이블을 지정 하 라는 메시지가 표시 하기 시작 합니다. 선택 된 `GuestbookComments`, `UserProfiles`, 및 `aspnet_Users` 테이블 하 고 OK를 클릭 합니다. 이렇게 하면 세 테이블 디자인 화면에 추가 됩니다. 적절 한 외래 키 제약 조건이 있으므로 `GuestbookComments`, `UserProfiles`, 및 `aspnet_Users` 테이블, 쿼리 작성기 자동으로 `JOIN` s 이러한 테이블입니다.

이제 남은 것 반환할 열을 지정 합니다. `GuestbookComments` 선택 테이블의 `Subject`, `Body`, 및 `CommentDate` 열; 반환은 `HomeTown`, `HomepageUrl`, 및 `Signature` 열을는 `UserProfiles` ; 테이블을 반환 `UserName` 에서`aspnet_Users`. 또한 추가 "`ORDER BY CommentDate DESC`"의 끝에는 `SELECT` 최근 게시물을 먼저 반환 되도록 쿼리 합니다. 이러한 선택 항목에 확인 한 후 쿼리 작성기 인터페이스 그림 18에서 스크린샷과 비슷해야 합니다.


[![GuestbookComments, UserProfiles, 및 aspnet_Users 테이블을 조인 하는 생성 된 쿼리](storing-additional-user-information-cs/_static/image53.png)](storing-additional-user-information-cs/_static/image52.png)

**그림 18**: 생성 된 쿼리 `JOIN` s는 `GuestbookComments`, `UserProfiles`, 및 `aspnet_Users` 테이블 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image54.png))


쿼리 작성기 창을 닫고 정의 사용자 지정 문 또는 저장 프로시저 "" 화면으로 돌아가려면 확인을 클릭 합니다. 클릭 쿼리 테스트 단추를 클릭 하 여 쿼리 결과 볼 수 있는 "테스트 쿼리" 화면으로 이동 합니다. 준비 되 면 데이터 소스 구성 마법사를 완료 하려면 마침을 클릭 합니다.

2 단계에서 연결된 된 DetailsView 컨트롤의 데이터 소스 구성 마법사를 완료 했습니다 `Fields` 컬렉션에서 반환 된 각 열에 대 한 BoundField를 포함 하도록 업데이트 되었습니다는 `SelectCommand`합니다. 하지만 ListView 변경 되지 않습니다. 계속 해당 레이아웃을 정의 해야 합니다. ListView의 레이아웃은 선언적 태그를 통해 또는 "ListView 구성" 옵션의 스마트 태그에서 수동으로 생성할 수 있습니다. I 일반적으로 태그를 직접 정의 것을 선호 하지만 가장 자연 방법을 사용 합니다.

최종적 다음을 사용 하 여 `LayoutTemplate`, `ItemTemplate`, 및 `ItemSeparatorTemplate` 내 ListView 컨트롤에 대 한:

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample10.aspx)]

`LayoutTemplate` 태그를 정의 하는 동안 컨트롤에 의해 생성 되는 `ItemTemplate` SqlDataSource에서 반환 된 각 항목을 렌더링 합니다. `ItemTemplate`의 결과 태그에 배치 되는 `LayoutTemplate`의 `itemPlaceholder` 제어 합니다. 이외에 `itemPlaceholder`, `LayoutTemplate` ListView 페이지 (기본값) 당 10 개만 방명록 주석 표시를 제한 하는 한 DataPager 컨트롤을 포함 하 고 페이징 인터페이스를 렌더링 합니다.

내 `ItemTemplate` 각 방명록 메모 주제에 표시 됩니다는 `<h4>` 요소를 본문 제목 아래에 위치 합니다. 구문 본문을 표시 하는 데 사용 하 여 반환 되는 데이터는 `Eval("Body")` databinding 문에서 문자열, 변환 및와 대체 줄 바꿈는 `<br />` 요소입니다. 이 변환은 HTML에서 공백 무시 하므로 주석으로 처리를 전송할 때 입력 한 줄 바꿈 표시 하기 위해 필요 합니다. 사용자의 서명은 그의 홈 페이지, 메모를 만든 날짜 및 시간과 주석을 유지 하는 사용자의 사용자 이름에 대 한 링크는 사용자의 홈 동 이어서 기울임꼴로 본문 아래에 표시 됩니다.

브라우저를 통해 페이지를 보려면 잠시 시간. 여기에 표시 된 5 단계에서에서 방명록에 추가 하는 주석을 표시 되어야 합니다.


[![Guestbook.aspx 지금은 방명록의 메모를 표시합니다.](storing-additional-user-information-cs/_static/image56.png)](storing-additional-user-information-cs/_static/image55.png)

**그림 19**: `Guestbook.aspx` 방명록의 주석 표시 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image57.png))


방명록에 새 메모를 추가 해 보십시오. 클릭 하면는 `PostCommentButton` 단추 페이지 다시 게시 및 주석으로 처리는 데이터베이스에 추가 되지만 ListView 컨트롤 새 메모를 표시 하도록 업데이트 되지 않습니다. 이 해결할 수 있습니다.

- 업데이트는 `PostCommentButton` 단추의 `Click` 한다는 ListView 컨트롤을 호출 하도록 이벤트 처리기 `DataBind()` 메서드는 데이터베이스에 새 메모를 삽입 한 후 또는
- ListView 컨트롤 설정 `EnableViewState` 속성을 `false`합니다. 이 방법은 컨트롤의 뷰 상태를 해제 하 여이 다시 바인딩해야 포스트백이 발생할 때마다 기본 데이터에 때문에 작동 합니다.

이 자습서에서 다운로드할 수 있는 자습서 웹 사이트에는 두 가지 방법을 모두 보여 줍니다. ListView 컨트롤의 `EnableViewState` 속성을 `false` 프로그래밍 방식으로 데이터 ListView 다시 바인딩해야 하는 데 필요한 코드에 있는지는 `Click` 이벤트 처리기 있지만 주석으로 처리 됩니다.

> [!NOTE]
> 현재는 `AdditionalUserInfo.aspx` 페이지 보기 및 홈 동, 홈 페이지 및 서명을 설정을 편집할 수 있습니다. 업데이트 좋을 것 `AdditionalUserInfo.aspx` 로그온 된 사용자의 방명록 주석에 표시를 합니다. 즉, 검사 하 고 그녀의 정보를 수정 하는 것 외에도 사용자를 방문할 수는 `AdditionalUserInfo.aspx` 를 이전에 이루어집니다 그녀 어떤 방명록 설명을 표시 합니다. I이 그대로 실행으로 관심된 판독기에 대 한 합니다.


## <a name="step-6-customizing-the-createuserwizard-control-to-include-an-interface-for-the-home-town-homepage-and-signature"></a>6 단계: 홈 동, 홈 페이지 및 서명을 대 한 인터페이스를 포함 하도록 CreateUserWizard 컨트롤 사용자 지정

`SELECT` 사용 하는 쿼리는 `Guestbook.aspx` 사용 하 여 페이지는 `INNER JOIN` 적절 한 관련된 레코드를 결합 하는 `GuestbookComments`, `UserProfiles`, 및 `aspnet_Users` 테이블입니다. 사용자가의 레코드가 없는 `UserProfiles` 방명록 하는지 주석 처리 주석으로 처리 하기 때문에 ListView에 표시 되지 않습니다는 `INNER JOIN` 만 반환 `GuestbookComments` 레코드에 일치 하는 레코드가 없는 경우 `UserProfiles` 및 `aspnet_Users`합니다. 사용자 레코드가 없는 경우 3 단계에서에서 설명한 것 처럼 및 `UserProfiles` 보거나의 그녀의 설정을 편집할 수 없는 그녀는 `AdditionalUserInfo.aspx` 페이지.

물론, 디자인으로 인해 사용 해야 하는 멤버 자격 시스템의 모든 사용자 계정을 일치 하는 의사 결정에 기록 된 `UserProfiles` 테이블입니다. 에 추가할 수 있는 해당 레코드에는 원하는 `UserProfiles` 은 CreateUserWizard를 통해 새 멤버 자격 사용자 계정이 생성 될 때마다 합니다.

에 설명 된 대로 [ *사용자 계정 만들기* ](creating-user-accounts-cs.md) 자습서에서는 새 멤버 자격 사용자 계정을 CreateUserWizard 컨트롤을 만든 후 발생 해당 [ `CreatedUser` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx). 이 이벤트에 대 한 이벤트 처리기를 만든, 방금 만든 사용자에 대 한 사용자 Id를 가져오기 하에 레코드를 삽입 한 다음 수는 `UserProfiles` 테이블에 대 한 기본 값으로는 `HomeTown`, `HomepageUrl`, 및 `Signature` 열입니다. 게다가 것 말하도록 하기 위해 이러한 값에 대 한 추가 텍스트 상자를 포함 하도록 CreateUserWizard 컨트롤의 인터페이스를 사용자 지정 하 여 가능 합니다.

새 행을 추가 하는 방법부터 알아보겠습니다는 `UserProfiles` 테이블에 `CreatedUser` 기본 값으로 이벤트 처리기입니다. 그런 다음, 새 사용자의 홈 동, 홈 페이지 및 서명을 수집 하도록 추가 양식 필드를 포함 하려면 CreateUserWizard 컨트롤의 사용자 인터페이스 사용자 지정 하는 방법을 살펴봅니다.

### <a name="adding-a-default-row-touserprofiles"></a>기본 행을 추가합니다.`UserProfiles`

에 [ *사용자 계정 만들기* ](creating-user-accounts-cs.md) CreateUserWizard 컨트롤을 추가 하는 자습서는 `CreatingUserAccounts.aspx` 페이지에 `Membership` 폴더입니다. 컨트롤은 CreateUserWizard을 가지려면에 레코드를 추가 `UserProfiles` 테이블 사용자 계정 생성 시 CreateUserWizard 컨트롤의 기능을 업데이트 해야 합니다. 에 변경 내용을이 적용 하는 것 보다는 `CreatingUserAccounts.aspx` 페이지에서 새 CreateUserWizard 컨트롤에 대신 추가 `EnhancedCreateUserWizard.aspx` 페이지 하 고이 자습서에서는 하 게 수정 합니다.

열기는 `EnhancedCreateUserWizard.aspx` Visual Studio에서 페이지 및 페이지 도구 상자에서 CreateUserWizard 컨트롤을 끕니다. CreateUserWizard 컨트롤 설정 `ID` 속성을 `NewUserWizard`합니다. 설명한 것 처럼는 <a id="_msoanchor_5"> </a> [ *사용자 계정 만들기* ](creating-user-accounts-cs.md) 자습서, CreateUserWizard의 기본 사용자 인터페이스에서 묻는 메시지를 표시 하는 데 필요한 정보에 대 한 방문자입니다. 이 정보를 제공한 후 컨트롤 내부적으로 만들며 새 사용자 계정을 멤버 자격 프레임 워크에서 모든 필요 없이 한 줄의 코드를 작성 합니다.

CreateUserWizard 컨트롤의 워크플로 중 다양을 한 이벤트를 발생 시킵니다. CreateUserWizard 컨트롤 처음 발생 한 후 방문자 요청 정보를 제공가 양식을 전송를 해당 [ `CreatingUser` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.creatinguser.aspx)합니다. 하지만 만들기 프로세스 중에 문제가 있으면는 [ `CreateUserError` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createusererror.aspx) ; 발생 사용자가 정상적으로 작성 하는 경우, 하면 [ `CreatedUser` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx) 발생 합니다. 에 <a id="_msoanchor_6"> </a> [ *사용자 계정 만들기* ](creating-user-accounts-cs.md) 자습서에 대 한 이벤트 처리기에서 만든는 `CreatingUser` 제공된 된 사용자는 선행 포함 되지 않은 이벤트 또는 후행 공백이 있는 경우와 사용자 이름 암호에 아무 곳 이나 표시 않았습니다 되지 않습니다.

행을 추가 하기 위해는 `UserProfiles` 테이블에 대 한 이벤트 처리기를 만들고 해야 방금 만든 사용자에 대 한는 `CreatedUser` 이벤트입니다. 시간순으로는 `CreatedUser` 수 있어 계정의 사용자 Id 값을 검색 하는 멤버 자격 프레임 워크에 사용자 계정이 이미 만들어져, 이벤트가 발생 합니다.

에 대 한 이벤트 처리기를 만들고는 `NewUserWizard`의 `CreatedUser` 이벤트를 다음 코드를 추가 합니다.

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample11.cs)]

방금 추가 된 사용자 계정의 사용자 Id를 검색 하 여 위의 코드 존재 합니다. 사용 하 여 이렇게는 `Membership.GetUser(username)` , 특정 사용자 및 사용 하 여 다음에 대 한 정보를 반환 하는 메서드는 `ProviderUserKey` 속성의 사용자 Id를 검색 합니다. CreateUserWizard 컨트롤에 사용자가 입력 한 사용자 이름을 통해 사용할 수는 [ `UserName` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.username.aspx)합니다.

연결 문자열에서 검색 되는 다음으로, `Web.config` 및 `INSERT` 문을 지정 합니다. 필요한 ADO.NET 개체 인스턴스화되고 명령을 실행 합니다. 코드에서 할당 한 [ `DBNull` ](https://msdn.microsoft.com/library/system.dbnull.aspx) 인스턴스를 `@HomeTown`, `@HomepageUrl`, 및 `@Signature` 매개 변수를 데이터베이스에 삽입 하는 효과가 `NULL` 에 대 한 값의 `HomeTown`, `HomepageUrl`, 및 `Signature` 필드입니다.

방문는 `EnhancedCreateUserWizard.aspx` 브라우저를 통해 페이지 하 고 새 사용자 계정을 만듭니다. 이렇게 하면 Visual Studio로 반환 하 고의 내용 검사는 `aspnet_Users` 및 `UserProfiles` 테이블 (같이 다시 그림 12). 새 사용자 계정에 표시 되어야 `aspnet_Users` 및 해당 `UserProfiles` 행 (으로 `NULL` 에 대 한 값 `HomeTown`, `HomepageUrl`, 및 `Signature`).


[![추가 된 새 사용자 계정 및 UserProfiles 레코드](storing-additional-user-information-cs/_static/image59.png)](storing-additional-user-information-cs/_static/image58.png)

**그림 20**: 새 사용자 계정 및 `UserProfiles` 레코드가 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image60.png))


방문자가 자신의 새 계정 정보를 제공 하 고 "사용자 만들기" 단추를 클릭 한, 사용자 계정 생성 후에 행이 추가 `UserProfiles` 테이블입니다. CreateUserWizard 표시 한 다음 해당 `CompleteWizardStep`, 성공 메시지 및 계속 단추를 표시 하는 합니다. 포스트백 단추를 클릭 하면 되지만 아무 작업도 수행에 고정 사용자는 `EnhancedCreateUserWizard.aspx` 페이지.

URL을 사용자에 게 보낼 CreateUserWizard 컨트롤을 통해 단추를 클릭할 때를 지정할 수 있습니다 [ `ContinueDestinationPageUrl` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)합니다. 설정의 `ContinueDestinationPageUrl` 속성을 "~ / Membership/AdditionalUserInfo.aspx"입니다. 이 작업을 수행 하려면 새 사용자 `AdditionalUserInfo.aspx`, 여기서을 확인 하 고 해당 설정을 업데이트 합니다.

### <a name="customizing-the-createuserwizards-interface-to-prompt-for-the-new-users-home-town-homepage-and-signature"></a>새 사용자의 홈 동, 홈 페이지 및 서명 확인으로 CreateUserWizard의 인터페이스를 사용자 지정

간단한 계정 만들기 시나리오만 핵심 사용자 계정 정보 같은 사용자 이름, 암호 및 전자 메일을 수집 될 필요 오류 CreateUserWizard 컨트롤의 기본 인터페이스가입니다. 하지만 경우에 어떻게 해야 할까요 방문자 자신의 계정을 만드는 동안 그녀의 홈 동, 홈 페이지 및 서명을 입력 하 라는 메시지? 등록에 대 한 추가 정보를 수집할 CreateUserWizard 컨트롤의 인터페이스를 사용자 지정할 수는 및에이 정보를 사용할 수 있습니다는 `CreatedUser` 이벤트 처리기를 기본 데이터베이스에 추가 레코드를 삽입 합니다.

CreateUserWizard 컨트롤 확장 페이지 개발자 일련의 순서가 지정 된 정의 허용 하는 컨트롤은 ASP.NET Wizard 컨트롤 `WizardSteps`합니다. 마법사 컨트롤 활성 단계를 렌더링 하 고이 단계를 통해 이동 하는 방문자를 허용 하는 탐색 인터페이스를 제공 합니다. 마법사 컨트롤 긴 작업을 몇 가지 간단한 단계로 이상적입니다. 마법사 컨트롤에 대 한 자세한 내용은 참조 하십시오. [ASP.NET 2.0 Wizard 컨트롤을 사용 하 여 단계별 사용자 인터페이스 만들기](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)합니다.

두 개의 CreateUserWizard 컨트롤의 기본 태그 정의 `WizardSteps`: `CreateUserWizardStep` 및 `CompleteWizardStep`합니다.

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample12.aspx)]

첫 번째 `WizardStep`, `CreateUserWizardStep`, 사용자 이름, 암호, 전자 메일, 등에 대 한 요청 하는 인터페이스를 렌더링 합니다. 표시 된 방문자가이 정보를 제공 하 고 "사용자 만들기"를 클릭 한 후 그녀는 `CompleteWizardStep`, 성공 메시지 및 계속 단추를 보여 주는 합니다.

추가 양식 필드를 포함 하려면 CreateUserWizard 컨트롤의 인터페이스를 사용자 지정 하려면에서는 다음과 같은 작업을 수행할 수 있습니다.

- <strong>하나 이상의 새로 만들기</strong><strong>`WizardStep`</strong><strong>추가 사용자 인터페이스 요소를 포함 하는 s</strong>합니다. 새 `WizardStep` 은 CreateUserWizard 클릭에서 "추가/제거 `WizardSteps`" 링크를 시작 하려면 스마트 태그에서는 `WizardStep` 컬렉션 편집기. 여기에서 추가, 제거 또는 마법사의 단계를 다시 정렬할 수 있습니다. 이 방법이이 자습서를 사용 합니다.

- <strong>변환 된</strong><strong>`CreateUserWizardStep`</strong><strong>에 편집 가능한</strong><strong>`WizardStep`</strong><strong>합니다.</strong> 이 대체는 `CreateUserWizardStep` 는 동일한 `WizardStep` 일치 하는 사용자 인터페이스를 정의 하는 피드백은 `CreateUserWizardStep`' s입니다. 변환 하 여는 `CreateUserWizardStep` 에 `WizardStep` 컨트롤의 위치를 변경 하거나이 단계를 추가 사용자 인터페이스 요소를 추가할 수 있습니다. 변환 하는 `CreateUserWizardStep` 또는 `CompleteWizardStep` 에 편집 가능한 `WizardStep`컨트롤의 스마트 태그에서 "사용자 지정 단계를 완료"의 링크 또는 "사용자 지정 사용자 만들기 단계"를 클릭 합니다.

- **위의 두 옵션 중 일부 조합을 사용 합니다.**

기억해 야 할 중요 한 사항은 CreateUserWizard 컨트롤 내에서 "사용자 만들기" 단추를 클릭 하면 해당 사용자 계정 생성 프로세스를 실행 하는 `CreateUserWizardStep`합니다. 추가적인 문제가 되지 않습니다 `WizardStep` 후 s는 `CreateUserWizardStep` 여부입니다.

사용자 지정을 추가할 때 `WizardStep` 사용자 지정의 추가 사용자 입력을 수집 하도록 CreateUserWizard 컨트롤에 `WizardStep` 앞 이나 뒤에 배치할 수 있습니다는 `CreateUserWizardStep`합니다. 앞에 배치 되는 경우는 `CreateUserWizardStep` 사용자 지정에서 추가 사용자 입력을 수집 하는 다음 `WizardStep` 에 사용할 수는 `CreatedUser` 이벤트 처리기입니다. 그러나 경우 사용자 지정 `WizardStep` 뒤에 오는 `CreateUserWizardStep` 시간순으로 다음 사용자 지정 `WizardStep` 표시 됩니다 새 사용자 계정을 이미 만들어져 및 `CreatedUser` 이벤트가 이미 발생 합니다.

그림 21 워크플로가 나와 때 추가 된 `WizardStep` 앞에 `CreateUserWizardStep`합니다. 추가 사용자 정보는 시간에 의해 수집 된 이후는 `CreatedUser` 하기만 하면 모든 이벤트 발생에는 업데이트는 `CreatedUser` 이러한 입력을 검색에 대 한 역할을 사용 하는 이벤트 처리기는 `INSERT` 문의 매개 변수 값 (보다는 `DBNull.Value`).


[![추가 WizardStep 앞는 CreateUserWizardStep 때 CreateUserWizard 워크플로](storing-additional-user-information-cs/_static/image62.png)](storing-additional-user-information-cs/_static/image61.png)

**그림 21**: The CreateUserWizard 워크플로 때는 추가 `WizardStep` Precedes는 `CreateUserWizardStep` ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image63.png))


하지만 하는 경우 사용자 지정 `WizardStep` 놓입니다 *후* 는 `CreateUserWizardStep`, 사용자 계정 만들기 프로세스가 수행 되는 사용자에 그녀의 홈 동, 홈 페이지 또는 서명 입력 전에 합니다. 이 경우이 추가 정보에 삽입 되는 데이터베이스 사용자 계정이 만들어진 후 그림 22와 같이 필요 합니다.


[![CreateUserWizard 워크플로 추가 WizardStep는 CreateUserWizardStep 뒤에 오는 경우](storing-additional-user-information-cs/_static/image65.png)](storing-additional-user-information-cs/_static/image64.png)

**그림 22**: The CreateUserWizard 워크플로 때는 추가 `WizardStep` 후 제공 되는 `CreateUserWizardStep` ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image66.png))


에 레코드를 삽입 하기 위해 대기 하는 그림 22에 표시 된 워크플로 `UserProfiles` 단계 2가 완료 될 때까지 테이블입니다. 그러나 방문자가 1 단계 후의 브라우저를 닫은 경우 우리에 도달 합니다 여기서 사용자 계정이 생성 되었지만에 레코드가 추가 된 상태 `UserProfiles`합니다. 와 레코드를 포함 하는 한 가지 해결 방법은 것 `NULL` 또는 삽입 된 값을 default `UserProfiles` 에 `CreatedUser` (1 단계 후 실행)이 표시 되는 이벤트 처리기 및 2 단계를 완료 한 후 기록이 업데이트 합니다. 이렇게 하면 한 `UserProfiles` 사용자를 통해 등록 프로세스 도중 종료 하는 경우에 사용자 계정에 대 한 레코드가 추가 됩니다.

이 자습서에 대 한 만들기 새 `WizardStep` 후 발생 하는 `CreateUserWizardStep` 하기 전에 `CompleteWizardStep`합니다. 첫 번째 get WizardStep에 배치 하 고 구성 하 고 다음 म 합니다 살펴보겠습니다 코드.

CreateUserWizard 컨트롤의 스마트 태그에서 선택 된 "추가/제거 `WizardStep` s"를 표시는 `WizardStep` 컬렉션 편집기 대화 상자. 새로 추가 `WizardStep`설정 해당 `ID` 를 `UserSettings`, 해당 `Title` "Your 설정"으로 및 해당 `StepType` 를 `Step`합니다. 다음에 오는 다음 위치에서 `CreateUserWizardStep` ("로그인을 새 계정에") 하기 전에 `CompleteWizardStep` ("전체"), 그림 23에 나와 있는 것 처럼 합니다.


[![새 WizardStep CreateUserWizard 컨트롤에 추가](storing-additional-user-information-cs/_static/image68.png)](storing-additional-user-information-cs/_static/image67.png)

**그림 23**: 새로 추가 `WizardStep` CreateUserWizard 컨트롤에 ([전체 크기 이미지를 보려면 클릭](storing-additional-user-information-cs/_static/image69.png))


확인을 눌러 닫습니다는 `WizardStep` 컬렉션 편집기 대화 상자. 새 `WizardStep` 은 CreateUserWizard 컨트롤의 업데이트 된 선언적 마크업으로 확인 되었습니다.:

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample13.aspx)]

새 확인 `<asp:WizardStep>` 요소입니다. 새 사용자의 홈 동, 홈 페이지 및 여기에 서명을 수집 하는 사용자 인터페이스를 추가 해야 합니다. 이 콘텐츠는 디자이너를 사용 하거나 선언적 구문에서 입력할 수 있습니다. 디자이너를 사용 하려면 디자이너의 단계를 참조 하도록 스마트 태그에서 드롭 다운 목록에서 "Your 설정" 단계를 선택 합니다.

> [!NOTE]
> CreateUserWizard 컨트롤의 스마트 태그의 드롭다운 목록을 통해 단계를 선택 하면 업데이트 [ `ActiveStepIndex` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.activestepindex.aspx), 시작 단계 인덱스를 지정 하는 합니다. 따라서이 드롭 다운 목록을 사용 하 여 디자이너에서 "Your 설정" 단계를 편집 하는 경우 반드시 사용자가 처음 방문 하는 경우이 단계는 표시 되도록 다시 "Sign Up for Your 새 Account"로 설정 하는 `EnhancedCreateUserWizard.aspx` 페이지.


라는 3 개의 TextBox 컨트롤을 포함 하는 "Your 설정" 단계 내에서 사용자 인터페이스 만들기 `HomeTown`, `HomepageUrl`, 및 `Signature`합니다. 이 인터페이스를 생성 한 후 CreateUserWizard의 선언적 태그는 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample14.aspx)]

계속 하 고 브라우저를 통해이 페이지를 방문를 홈 동, 홈 페이지 및 서명을 대 한 값을 지정 하는 새 사용자 계정을 만들 합니다. 완료 한 후의 `CreateUserWizardStep` 사용자 계정이 멤버 자격 프레임 워크에서 생성 및 `CreatedUser` 새 행을 추가 하는 이벤트 처리기 실행 `UserProfiles`, 하지만 데이터베이스와 `NULL` 값 `HomeTown`, `HomepageUrl`, 및 `Signature`. 홈 동, 홈 페이지 및 서명을 입력 된 값이 사용 되지 않습니다 됩니다. 그 결과 새 사용자 계정에는 `UserProfiles` 갖는 기록 `HomeTown`, `HomepageUrl`, 및 `Signature` 필드 아직만 지정 해야 합니다.

사용자가 입력 한 홈 동, honepage, 및 서명을 값을 사용 하 고 적절 한 업데이트 하는 "Your 설정" 단계를 수행한 후 코드를 실행 해야 `UserProfiles` 레코드입니다. 마법사의 마법사의 단계 사이 이동할 때마다 컨트롤 [ `ActiveStepChanged` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.wizard.activestepchanged.aspx) 발생 합니다. 이 이벤트와 업데이트에 대 한 이벤트 처리기를 만들 수 있습니다는 `UserProfiles` "Your 설정" 단계 완료 되 면 테이블입니다.

CreateUserWizard의에 대 한 이벤트 처리기를 추가 `ActiveStepChanged` 이벤트를 다음 코드를 추가 합니다.

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample15.cs)]

위의 코드에서는 "완료" 단계 도달 하는 경우를 확인 하 여 시작 합니다. "완료" 단계 "Your 설정" 단계 바로 뒤에 오는, 이후 다음 방문자에 도달할 때 "완료" 단계를 진행 "Your 설정" 단계를 방금 완료 그녀 의미입니다.

내에서 TextBox 컨트롤을 프로그래밍 방식으로 참조 해야 이러한 경우는 `UserSettings WizardStep`합니다. 사용 하 여 이렇게는 `FindControl` 메서드를 프로그래밍 방식으로 참조 하는 `UserSettings WizardStep`, 다음 텍스트 상자 내에서 참조를 다시는 `WizardStep`합니다. 실행 준비 되었는지 텍스트 상자의 참조 된, 일단는 `UPDATE` 문. `UPDATE` 문에으로 매개 변수 수가 같은 `INSERT` 의 문에서 `CreatedUser` 이벤트 처리기 있지만 여기서는 사용자가 제공한 홈 동, 홈 페이지 및 서명을 값을 사용 하는 여기 합니다.

이 이벤트 처리기 위치에 방문는 `EnhancedCreateUserWizard.aspx` 브라우저를 통해 페이지 및 홈 동, 홈 페이지 및 서명을 대 한 값을 지정 하는 새 사용자 계정을 만듭니다. 새 계정을 만든 후 리디렉션되어야 하는 `AdditionalUserInfo.aspx` 페이지에서 방금 입력 홈 동, 홈 페이지 및 시그니처 정보 표시 됩니다.

> [!NOTE]
> 웹 사이트는 현재 두 페이지는 방문자가 있는 새 계정을 만들 수는: `CreatingUserAccounts.aspx` 및 `EnhancedCreateUserWizard.aspx`합니다. 웹 사이트의 사이트 맵 및 로그인 페이지 가리킵니다는 `CreatingUserAccounts.aspx` 페이지 이지만 `CreatingUserAccounts.aspx` 페이지에서 사용자의 홈 동, 홈 페이지 및 시그니처 정보에 표시 되지 않습니다 및 해당 행을 추가 하지 않습니다 `UserProfiles`합니다. 따라서 업데이트 하거나는 `CreatingUserAccounts.aspx` 페이지를이 기능을 제공 하거나 참조 하 고 사이트 맵 및 로그인 페이지를 업데이트 `EnhancedCreateUserWizard.aspx` 대신 `CreatingUserAccounts.aspx`합니다. 후자 옵션을 선택 하는 경우 업데이트 해야는 `Membership` 폴더의 `Web.config` 익명 사용자에 대 한 액세스를 허용 하기 위해 파일은 `EnhancedCreateUserWizard.aspx` 페이지.


## <a name="summary"></a>요약

이 자습서에서는 멤버 자격 프레임 워크 내에서 사용자 계정에 관련 된 데이터를 모델링 하는 것에 대 한 기술에서 찾았습니다. 특히, 일대일 관계를 공유 하는 데이터 뿐 아니라 사용자 계정에는 일 대 다 관계를 공유 하는 엔터티를 모델링 살펴보았습니다. 또한 살펴본 어떻게이 관련 정보 수 수 표시, 삽입, 업데이트, SqlDataSource 컨트롤 및 다른 사용자를 사용 하 여 몇 가지 예는 ADO.NET 코드를 사용 하 여 합니다.

이 자습서에는 사용자 계정이에서 모양을 완료합니다. 다음 자습서와 함께 시작 역할에 설정 됩니다. 역할 프레임 워크는 방법에 여러 자습서는 다음을 통해 새 역할을 생성 하는 방법을 참조 하 고 역할을 결정 하는 사용자가 속한 방법, 사용자에 게 역할을 할당 하는 방법 역할 기반 권한 부여를 적용 합니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 2.0에서에서 데이터 액세스 및 업데이트](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [ASP.NET 2.0 Wizard 컨트롤](https://weblogs.asp.net/scottgu/archive/2006/02/21/438732.aspx)
- [ASP.NET 2.0 Wizard 컨트롤을 사용 하 여 단계별 사용자 인터페이스 만들기](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)
- [사용자 지정 데이터 원본 제어 매개 변수 만들기](http://aspnet.4guysfromrolla.com/articles/110106-1.aspx)
- [CreateUserWizard 컨트롤 사용자 지정](http://aspnet.4guysfromrolla.com/articles/070506-1.aspx)
- [DetailsView 컨트롤 퀵 스타트](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/data/detailsview.aspx)
- [ListView 컨트롤을 사용 하 여 데이터를 표시합니다.](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)
- [ASP.NET 2.0에서에서 유효성 검사 컨트롤 나누어서](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)
- [데이터 삽입을 편집 및 삭제](../../data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)
- [ASP.NET에서 폼 유효성 검사](http://www.4guysfromrolla.com/webtech/090200-1.shtml)
- [사용자 지정 사용자 등록 정보를 수집합니다.](https://weblogs.asp.net/scottgu/archive/2006/07/05/Tip_2F00_Trick_3A00_-Gathering-Custom-User-Registration-Information.aspx)
- [ASP.NET 2.0에서 프로필](http://www.odetocode.com/Articles/440.aspx)
- [Asp: ListView 컨트롤](https://weblogs.asp.net/scottgu/archive/2007/08/10/the-asp-listview-control-part-1-building-a-product-listing-page-with-clean-css-ui.aspx)
- [사용자 프로필 빠른 시작](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/profile/default.aspx)

### <a name="about-the-author"></a>작성자 정보

여러 ASP/ASP.NET 책의 작성자 및 4GuysFromRolla.com의 창립자 Scott Mitchell의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은  *[Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*합니다. Scott에 도달할 수 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 또는에서 그의 블로그 통해 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특히 감사 드립니다.

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)합니다.

> [!div class="step-by-step"]
> [이전](user-based-authorization-cs.md)
> [다음](creating-the-membership-schema-in-sql-server-vb.md)
