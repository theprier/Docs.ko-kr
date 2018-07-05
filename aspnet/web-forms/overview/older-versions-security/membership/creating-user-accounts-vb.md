---
uid: web-forms/overview/older-versions-security/membership/creating-user-accounts-vb
title: 사용자 계정 (VB) 만들기 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 새 사용자 계정을 만드는 (SqlMembershipProvider)를 통해 멤버 자격 프레임 워크를 사용 하 여 살펴봅니다. 미국 새로 만드는 방법을 살펴보겠습니다...
ms.author: aspnetcontent
ms.date: 01/18/2008
ms.assetid: 9ef3e893-bebe-4b13-9fe5-8b71720dd85e
msc.legacyurl: /web-forms/overview/older-versions-security/membership/creating-user-accounts-vb
msc.type: authoredcontent
ms.openlocfilehash: fe5e55df3fa9f65a94199c2064a785255f231537
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37815345"
---
<a name="creating-user-accounts-vb"></a>사용자 계정 만들기 (VB)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_05_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial05_CreatingUsers_vb.pdf)

> 이 자습서에서는 새 사용자 계정을 만드는 (SqlMembershipProvider)를 통해 멤버 자격 프레임 워크를 사용 하 여 살펴봅니다. 프로그래밍 방식으로 및 ASP를 통해 새 사용자를 만드는 방법을 살펴보겠습니다. NET의 기본 제공 CreateUserWizard 컨트롤입니다.


## <a name="introduction"></a>소개

에 <a id="_msoanchor_1"> </a> [이전 자습서](creating-the-membership-schema-in-sql-server-vb.md) 응용 프로그램 서비스 스키마는 테이블, 뷰, 추가 및 저장 프로시저에 필요한 데이터베이스에서 설치한 합니다 `SqlMembershipProvider` 및 `SqlRoleProvider`합니다. 이렇게 해야이 시리즈의 자습서의 나머지 부분에 대 한 인프라를 생성 됩니다. 이 자습서에서 살펴봅니다 멤버 자격 프레임 워크를 사용 하 여 (통해를 `SqlMembershipProvider`) 새 사용자 계정을 만들 수 있습니다. 프로그래밍 방식으로 및 ASP를 통해 새 사용자를 만드는 방법을 살펴보겠습니다. NET의 기본 제공 CreateUserWizard 컨트롤입니다.

새 사용자 계정을 만드는 방법을 학습 하는 것 외에도 또한 해야에서 먼저 만들었습니다 데모 웹 사이트를 업데이트 합니다 *<a id="_msoanchor_2"> </a> [는 폼 인증 개요](../introduction/an-overview-of-forms-authentication-vb.md)* 자습서 및의 향상 된 다음 합니다 *<a id="_msoanchor_3"> </a> [폼 인증 구성 및 고급 항목](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md)* 자습서입니다. 데모 웹 응용 프로그램에 하드 코딩 된 사용자 이름/암호 쌍에 대 한 사용자의 자격 증명의 유효성을 검사 하는 로그인 페이지를 있습니다. 게다가 `Global.asax` 만드는 사용자 지정 코드를 포함 `IPrincipal` 고 `IIdentity` 인증 된 사용자에 대 한 개체입니다. 멤버 자격 프레임 워크에 대 한 사용자의 자격 증명의 유효성을 검사 하 고 사용자 지정 보안 주체와 id 논리를 제거 하는 로그인 페이지를 업데이트 됩니다.

이제 시작 하겠습니다.

## <a name="the-forms-authentication-and-membership-checklist"></a>폼 인증 및 멤버 자격 검사 목록

멤버 자격 프레임 워크를 사용 하 여 작업을 시작 하기 전에이 시점까지 이동 하는 중요 한 단계를 검토 하려면 잠시를 살펴보겠습니다. 사용 하 여 멤버 자격 프레임 워크를 사용 하는 경우는 `SqlMembershipProvider` 폼 기반 인증 시나리오에서 다음 단계를 웹 응용 프로그램의 멤버 자격 기능을 구현 하기 전에 수행 해야 합니다.

1. **폼 기반 인증을 사용 하도록 설정 합니다.** 설명한 대로  *<a id="_msoanchor_4"> </a> [는 폼 인증 개요](../introduction/an-overview-of-forms-authentication-vb.md)* 를 편집 하 여 폼 인증을 사용할 `Web.config` 설정 하는 `<authentication>` 요소의 `mode` 특성을 `Forms`입니다. 사용 하도록 설정 하는 폼 인증을 사용 하 여 들어오는 각 요청에 대해 검사 됩니다는 *폼 인증 티켓*에 있는 경우를 식별 하는 요청자에 게 합니다.
2. **해당 데이터베이스에 응용 프로그램 서비스 스키마를 추가 합니다.** 사용 하는 경우는 `SqlMembershipProvider` 데이터베이스에 응용 프로그램 서비스 스키마를 설치 해야 합니다. 일반적으로이 스키마는 응용 프로그램의 데이터 모델 보유 하는 동일한 데이터베이스에 추가 됩니다. 합니다 *<a id="_msoanchor_5"> </a> [SQL Server에서 멤버 자격 스키마 만들기](creating-the-membership-schema-in-sql-server-vb.md)* 자습서를 사용 하 여 살펴보았습니다는 `aspnet_regsql.exe` 이 작업을 수행 하는 도구입니다.
3. **2 단계에서 데이터베이스를 참조 하도록 웹 응용 프로그램의 설정을 사용자 지정 합니다.** 합니다 *SQL Server에서 멤버 자격 스키마 만들기* 자습서 응용 프로그램을 구성 하는 두 가지 방법에 설명 했습니다 있도록를 `SqlMembershipProvider` 2 단계에서 선택한 데이터베이스를 사용 합니다: 수정 하 여는 `LocalSqlServer` 연결 문자열 이름입니다. 또는 멤버 자격 프레임 워크 공급자 목록에 새 등록 된 공급자를 추가 하는 새 공급자에서 데이터베이스를 사용 하도록 사용자 지정 하 여 2 단계.

때 사용 하는 웹 응용 프로그램을 빌드하기 합니다 `SqlMembershipProvider` 사용 하기 전에 다음 세 단계를 수행 해야 폼 기반 인증 및는 `Membership` 클래스 또는 Asp.net 로그인 컨트롤입니다. 이전 자습서에서 다음이 단계를 이미 수행한 것 이므로 준비가 멤버 자격 프레임 워크를 사용 하 여 시작!

## <a name="step-1-adding-new-aspnet-pages"></a>1 단계: 새 ASP.NET 페이지 추가

이 자습서에는 다음 세 우리는 검색할 수 다양 한 멤버 자격 관련 기능 및 기능입니다. 일련의 항목에서는이 자습서 전체에서 검사를 구현 하려면 ASP.NET 페이지를 해야 합니다. 해당 페이지 및 사이트 맵 파일을 만들어 보겠습니다 `(Web.sitemap)`합니다.

이라는 프로젝트에 새 폴더를 만들어 시작 `Membership`합니다. 다음으로, 새 ASP.NET 페이지를 5 개를 추가 합니다 `Membership` 폴더에 있는 각 페이지에 연결는 `Site.master` 마스터 페이지. 페이지 이름을 지정 합니다.

- `CreatingUserAccounts.aspx`
- `UserBasedAuthorization.aspx`
- `EnhancedCreateUserWizard.aspx`
- `AdditionalUserInfo.aspx`
- `Guestbook.aspx`

이 시점에서 프로젝트의 솔루션 탐색기 스크린 샷을 그림 1에 표시 된 것을 유사 합니다.


[![멤버 자격 폴더에 5 개의 새 페이지를 추가 했습니다.](creating-user-accounts-vb/_static/image2.png)](creating-user-accounts-vb/_static/image1.png)

**그림 1**: 5 개의 새 페이지에 추가한 합니다 `Membership` 폴더 ([클릭 하 여 큰 이미지 보기](creating-user-accounts-vb/_static/image3.png))


각 페이지에서이 시점에서 있어야 마스터 페이지의 ContentPlaceHolders 마다 하나씩 두 콘텐츠 컨트롤: `MainContent` 고 `LoginContent`입니다.

[!code-aspx[Main](creating-user-accounts-vb/samples/sample1.aspx)]

이전에 설명한 대로 `LoginContent` ContentPlaceHolder의 기본 태그는 로그온 하거나 로그 오프 사용자가 인증 되는지 여부에 따라 사이트에 대 한 링크를 표시 합니다. 그러나 현재 상태는 `Content2` 콘텐츠 컨트롤에 마스터 페이지의 기본 태그 보다 우선 합니다. 설명한 대로 *<a id="_msoanchor_6"> </a> [는 폼 인증 개요](../introduction/an-overview-of-forms-authentication-vb.md)* 자습서에서는이 여기서 하지 왼쪽된 열에서 로그인 관련 옵션을 표시 하려면 페이지에서 유용 합니다.

그러나 이러한 5 개 페이지에 대 한 표시 하려고에 대 한 마스터 페이지의 기본 태그는 `LoginContent` ContentPlaceHolder 합니다. 따라서 선언적 태그를 제거 합니다 `Content2` 콘텐츠 컨트롤입니다. 이렇게 하면 5 페이지의 태그의 각 콘텐츠 컨트롤을 한 개만 있어야 합니다.

## <a name="step-2-creating-the-site-map"></a>2 단계: 사이트 맵 만들기

가장 간단한 웹 사이트를 제외한 모든 형태의 탐색 사용자 인터페이스를 구현 해야 합니다. 탐색 사용자 인터페이스에는 사이트의 다양 한 섹션에 대 한 링크의 단순 목록을 수 있습니다. 또는 메뉴 또는 트리 보기에 이러한 링크를 정렬할 수 있습니다. 페이지 개발자 탐색 사용자 인터페이스 만들기는 스토리의 절반에 불과합니다. 또한 유지 하 고 업데이트할 수 있는 방식으로 사이트의 논리 구조를 정의 하기 위한 방법이 필요 합니다. 새 페이지 추가 하거나 기존 페이지를 제거 하면-사이트 맵-단일 소스를 업데이트 하고자 하 고 이러한 수정 사항은 사이트의 탐색 사용자 인터페이스를 통해 반영 합니다.

이러한 두 작업 (사이트 맵을 정의 및 사이트 맵 기반 탐색 사용자 인터페이스를 구현)가 사이트 맵 프레임 워크를 통해 간편 하 고 탐색 웹의 추가 ASP.NET 버전 2.0 제어 합니다. 사이트 맵을 정의 하는 개발자를 위한 사이트 맵 프레임 워크를 사용 하면 프로그래밍 방식으로 API를 통해 액세스 하는 다음 (합니다 [ `SiteMap` 클래스](https://msdn.microsoft.com/library/system.web.sitemap.aspx)). 포함 하는 기본 제공 탐색 웹 컨트롤을 [Menu 컨트롤](https://msdn.microsoft.com/library/bz09dy46.aspx), [TreeView 컨트롤](https://msdn.microsoft.com/library/3eafky27.aspx), 및 [SiteMapPath 컨트롤](https://msdn.microsoft.com/library/3eafky27.aspx).

멤버 자격 및 역할 프레임 워크와 같은 사이트 맵 프레임 워크 위에 빌드되는 [공급자 모델](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)합니다. 사이트 맵 공급자 클래스의 작업에서 사용 하는 메모리 내 구조를 생성 하는 것은 `SiteMap` XML 파일 또는 데이터베이스 테이블과 같은 영구 데이터 저장소에서 클래스입니다. .NET Framework는 XML 파일에서 사이트 맵 데이터를 읽는 기본 사이트 맵 공급자와 함께 제공 됩니다 ([`XmlSiteMapProvider`](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx)),이이 자습서를 사용 하는 공급자입니다. 일부 대체 사이트 맵 공급자 구현에 대 한이 자습서의 끝에 추가 정보 섹션을 참조 합니다.

기본 사이트 맵 공급자에서는 올바른 형식의 XML 파일을 명명 된 `Web.sitemap` 루트 디렉터리에 있어야 합니다. 이 기본 공급자를 사용 하므로 이러한 파일을 추가 하 고 적절 한 XML 형식으로 사이트 맵 구조를 정의 해야 합니다. 파일을 추가 하려면 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가 선택 합니다. 대화 상자에서 사이트 맵 라는 형식의 파일을 추가 하도록 선택할 `Web.sitemap`합니다.


[![프로젝트의 루트 디렉터리는 Web.sitemap 이라는 파일 추가](creating-user-accounts-vb/_static/image5.png)](creating-user-accounts-vb/_static/image4.png)

**그림 2**: 라는 파일을 추가 `Web.sitemap` 프로젝트의 루트 디렉터리 ([클릭 하 여 큰 이미지 보기](creating-user-accounts-vb/_static/image6.png))


사이트 맵 XML 파일을 계층으로 웹 사이트의 구조를 정의합니다. 이 계층 관계의 상위 구조를 통해 XML 파일에서 모델링 됩니다는 `<siteMapNode>` 요소입니다. 합니다 `Web.sitemap` 로 시작 해야 합니다는 `<siteMap>` 정확 하 게 하나를 포함 하는 부모 노드로 `<siteMapNode>` 자식입니다. 이 최상위 `<siteMapNode>` 요소 계층의 루트를 나타내며 임의 개수의 하위 노드가 있을 수 있습니다. 각 `<siteMapNode>` 요소에 포함 해야 합니다는 `title` 특성 및 선택적으로 포함할 수 있습니다 `url` 및 `description` 특히; 특성을 각 비어 있지 않은 `url` 특성은 고유 해야 합니다.

다음 XML을 입력 합니다 `Web.sitemap` 파일:

[!code-xml[Main](creating-user-accounts-vb/samples/sample2.xml)]

위의 사이트 맵 태그 그림 3과 같이 계층 구조를 정의 합니다.


[![사이트 맵 탐색 계층 구조를 나타냅니다.](creating-user-accounts-vb/_static/image8.png)](creating-user-accounts-vb/_static/image7.png)

**그림 3**: 사이트 맵 탐색 계층 구조를 나타냅니다 ([큰 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image9.png))


## <a name="step-3-updating-the-master-page-to-include-a-navigational-user-interface"></a>3 단계: 마스터 페이지는 탐색 사용자 인터페이스를 포함 하도록 업데이트

ASP.NET에는 다양 한 사용자 인터페이스 디자인에 대 한 탐색 관련 웹 컨트롤이 포함 되어 있습니다. 이러한 메뉴, TreeView 및 SiteMapPath 컨트롤을 포함 합니다. Menu 및 TreeView 컨트롤은 SiteMapPath 상위 항목 뿐만 아니라 방문 중인 현재 노드를 보여 주는 이동 경로 표시 하는 반면 사이트 맵 구조 메뉴 또는 트리를 각각 렌더링 합니다. 사이트 맵 데이터 웹 컨트롤 SiteMapDataSource를 사용 하 여 다른 데이터에 바인딩될 수 고를 통해 프로그래밍 방식으로 액세스할 수는 `SiteMap` 클래스입니다.

사이트 맵 framework와 탐색 컨트롤에 대 한 자세한 내용은이 자습서 시리즈의 범위를 벗어납니다 이므로 대신 보겠습니다 고유의 탐색 사용자 인터페이스를 작성 하는 시간 보다 대신 차용에서 사용한 필자의 *[ ASP.NET 2.0에서 데이터로 작업할](../../data-access/index.md)* 그림 4 에서처럼 탐색 링크의 두 심층 글머리 기호 목록을 표시 하려면 Repeater 컨트롤을 사용 하는 자습서 시리즈입니다.

### <a name="adding-a-two-level-list-of-links-in-the-left-column"></a>왼쪽된 열에서 두 수준의 목록을 링크 추가

이 인터페이스를 만들려면 다음 선언적 태그를 추가 합니다 `Site.master` 마스터 페이지의 왼쪽 열 위치 텍스트 TODO: 메뉴는 여기에... 현재 상주 합니다.

[!code-aspx[Main](creating-user-accounts-vb/samples/sample3.aspx)]

위의 태그 라는 Repeater 컨트롤을 바인딩하 `menu` SiteMapDataSource를를 반환 하는 사이트 지도 계층에 정의 된 `Web.sitemap`합니다. SiteMapDataSource 컨트롤의 이후 [ `ShowStartingNode` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemapdatasource.showstartingnode.aspx) 홈 노드의 하위 항목이 시작 되는 사이트 맵의 계층을 반환 하기 시작 하는 False로 설정 됩니다. 반복기에서 이러한 각 노드 (현재는 그냥 멤버 자격)을 표시는 `<li>` 요소입니다. 다른, 내부 Repeater 중첩 된 순서가 지정 되지 않은 목록에서 현재 노드의 자식을 표시합니다.

그림 4는 2 단계에서에서 만든 사이트 맵 구조를 사용 하 여 위의 태그를 렌더링 된 출력을 보여줍니다. Repeater 바닐라 순서가 지정 되지 않은 목록 태그;를 렌더링합니다. 에 정의 된 연계 스타일 시트 규칙 `Styles.css` 심미안 것 레이아웃에 대 한 책임이 있습니다. 위의 태그의 작동 방식을 더 자세한 내용은 참조는 [마스터 페이지 및 사이트 탐색](https://asp.net/learn/data-access/tutorial-03-vb.aspx) 자습서입니다.


[![렌더링 된 목록을 사용 하 여 중첩 된 순서가 지정 되지 않은 탐색 사용자 인터페이스는](creating-user-accounts-vb/_static/image11.png)](creating-user-accounts-vb/_static/image10.png)

**그림 4**: The 탐색 사용자 인터페이스는 렌더링 된 목록을 사용 하 여 중첩 된 순서가 지정 되지 않은 ([큰 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image12.png))


### <a name="adding-breadcrumb-navigation"></a>추가 이동 경로 탐색

왼쪽된 열에 대 한 링크, 목록 외에 저 각 페이지 표시를 [breadcrumb](http://en.wikipedia.org/wiki/Breadcrumb_%28navigation%29)합니다. 이동 경로 신속 하 게 사용자에 게 사이트 계층 구조 내에 있는 현재 위치를 표시 하는 탐색 사용자 인터페이스 요소입니다. SiteMapPath 컨트롤 사이트 맵에서 현재 페이지의 위치를 확인 하는 사이트 맵 프레임 워크를 사용 하 고이 정보를 기반으로 하는 이동 경로 탐색을 표시 합니다.

특히 추가 `<span>` 마스터 페이지의 헤더 요소 `<div>` 요소를 새 설정 `<span>` 요소의 `class` 이동 경로 탐색 하는 특성입니다. (의 `Styles.css` 이동 경로 탐색 클래스에 대 한 규칙을 포함 하는 클래스입니다.) 그런 다음 추가 하는 SiteMapPath이 새로운 `<span>` 요소입니다.

[!code-aspx[Main](creating-user-accounts-vb/samples/sample4.aspx)]

그림 5를 방문할 때는 SiteMapPath의 출력을 보여 줍니다 `~/Membership/CreatingUserAccounts.aspx`합니다.


[![현재 페이지를 표시 하는 이동 경로 탐색 및 사이트의 상위 항목 매핑](creating-user-accounts-vb/_static/image14.png)](creating-user-accounts-vb/_static/image13.png)

**그림 5**: 사이트 맵에서 현재 페이지와 해당 상위 요소를 표시 하는 이동 경로 탐색 ([큰 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image15.png))


## <a name="step-4-removing-the-custom-principal-and-identity-logic"></a>4 단계: 사용자 지정 보안 주체와 Id 논리를 제거합니다.

에 *<a id="_msoanchor_7"> </a> [폼 인증 구성 및 고급 항목](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md)* 자습서 인증 된 사용자에 게 사용자 지정 principal 및 identity 개체를 연결 하는 방법에 살펴보았습니다. 이벤트 처리기를 만들어이 작업을 수행 했습니다 `Global.asax` 응용 프로그램에 대 한 `PostAuthenticateRequest` 후 발생 하는 이벤트를 `FormsAuthenticationModule` 에서 사용자를 인증 합니다. 이 이벤트 처리기에서 교체를 `GenericPrincipal` 및 `FormsIdentity` 하 여 추가 된 개체를 `FormsAuthenticationModule` 사용 하 여를 `CustomPrincipal` 및 `CustomIdentity` 해당 자습서에서 만든 개체.

사용자 지정 principal 및 identity 개체는 대부분의 경우에서 특정 시나리오에서 유용 합니다 `GenericPrincipal` 및 `FormsIdentity` 개체는 충분 합니다. 결과적으로 기본 동작을 반환 하는 것 이라고 생각 합니다. 제거 하거나 주석으로 처리 하 여 이와 같이 변경 합니다 `PostAuthenticateRequest` 이벤트 처리기 또는 삭제 하 여는 `Global.asax` 완전히 파일.

> [!NOTE]
> 코드를 제거 하거나 주석 처리 했습니다 `Global.asax`에서 코드를 주석 처리 해야 합니다 `Default.aspx's` 캐스팅 하는 코드 숨김 클래스는 `User.Identity` 속성을는 `CustomIdentity` 인스턴스.


## <a name="step-5-programmatically-creating-a-new-user"></a>5 단계: 새 사용자를 프로그래밍 방식으로 만들기

멤버 자격 프레임 워크 사용을 통해 새 사용자 계정을 만들려면 합니다 `Membership` 클래스의 [ `CreateUser` 메서드](https://msdn.microsoft.com/library/system.web.security.membership.createuser.aspx)합니다. 이 메서드는 사용자 이름, 암호 및 다른 사용자와 관련 된 필드에 대 한 매개 변수를 입력 합니다. 호출에서 구성된 된 멤버 자격 공급자에 위임 하는 새 사용자 계정 생성 하 고 반환 합니다는 [ `MembershipUser` 개체](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx) 방금 만든 사용자 계정을 표시 합니다.

`CreateUser` 메서드는 4 개의 오버 로드가 각각 다른 개수의 입력된 매개 변수를 수락 합니다.

- [`CreateUser(username, password)`](https://msdn.microsoft.com/library/d8t4h2es.aspx)
- [`CreateUser(username, password, email)`](https://msdn.microsoft.com/library/t8yy6w3h.aspx)
- [`CreateUser(username, password, email, passwordQuestion, passwordAnswer, isApproved, MembershipCreateStatus)`](https://msdn.microsoft.com/library/82xx2e62.aspx)
- [`CreateUser(username, password, email, passwordQuestion, passwordAnswer, isApproved, providerUserKey, MembershipCreateStatus)`](https://msdn.microsoft.com/library/ms152012.aspx)

이러한 4 개의 오버 로드는 수집 되는 정보의 양에 따라 다릅니다. 첫 번째 오버 로드를 예를 들어 필요 username 및 password 새 사용자 계정에 대 한 반면 두 번째 사용자의 전자 메일 주소가 필요 합니다.

이러한 오버 로드는 새 사용자 계정을 만드는 데 필요한 정보를 멤버 자격 공급자의 구성 설정에 따라 달라 지므로 존재 합니다. 에 *<a id="_msoanchor_8"> </a> [SQL Server에서 멤버 자격 스키마 만들기](creating-the-membership-schema-in-sql-server-vb.md)* 검사할 멤버 자격 공급자 구성 설정에서 지정 하는 자습서 `Web.config`합니다. 표 2에 구성 설정의 전체 목록을 포함 합니다.

이러한 멤버 자격 공급자 구성 설정에 어떤 영향을 줍니다 `CreateUser` 오버 로드를 사용할 수는 `requiresQuestionAndAnswer` 설정 합니다. 하는 경우 `requiresQuestionAndAnswer` 로 설정 된 `true` (기본값), 새 사용자 계정을 만들 때 보안 질문 및 답변을 지정 해야 합니다. 이 정보는 사용자가 자신의 암호를 변경 또는 재설정 해야 하는 경우에 나중에 사용 됩니다. 특히, 이때 보안 질문이 표시 됩니다 및 다시 설정 하거나 암호를 변경 하기 위해 올바른 답을 입력 해야 합니다. 결과적으로 경우 합니다 `requiresQuestionAndAnswer` 로 설정 되어 `true` 를 호출 하는 첫 번째 두 `CreateUser` 보안 질문 및 답변 누락 되었기 때문에 예외가 발생 오버 로드 합니다. 응용 프로그램은 현재 보안 질문 및 대답을 요구 하도록 구성 된 후 사용자의 프로그래밍 방식으로 만들 때 후자의 두 오버 로드 중 하나를 사용 해야 합니다.

사용법을 설명 하기는 `CreateUser` 메서드는 메시지를 표시 이름, 암호, 메일 및 미리 정의 된 보안 질문에 대 한 답변에 대 한 사용자는 사용자 인터페이스를 만들어 보겠습니다. 엽니다는 `CreatingUserAccounts.aspx` 페이지에서 `Membership` 폴더 콘텐츠 컨트롤에 다음과 같은 웹 컨트롤을 추가:

- 명명 된 TextBox `Username`
- 명명 된 TextBox `Password`해당 `TextMode` 속성 `Password`
- 명명 된 TextBox `Email`
- 이라는 레이블이 `SecurityQuestion` 사용 하 여 해당 `Text` 속성 삭제
- 명명 된 TextBox `SecurityAnswer`
- 이라는 단추가 `CreateAccountButton` 해당 `Text` 속성을 만들려면 사용자 계정
- 명명 된 Label 컨트롤 `CreateAccountResults` 사용 하 여 해당 `Text` 속성 삭제

이 시점에서 화면 스크린샷과 그림 6 에서처럼 유사 합니다.


[![CreatingUserAccounts.aspx 페이지에 다양 한 웹 컨트롤 추가](creating-user-accounts-vb/_static/image17.png)](creating-user-accounts-vb/_static/image16.png)

**그림 6**: 다양 한 웹 컨트롤을 추가 합니다 `CreatingUserAccounts.aspx Page` ([클릭 하 여 큰 이미지 보기](creating-user-accounts-vb/_static/image18.png))


`SecurityQuestion` 레이블 및 `SecurityAnswer` 텍스트 상자는 미리 정의 된 보안 질문을 표시 하 고 사용자의 답변을 수집 하려고 합니다. 참고는 보안 질문 및 답변에 모두 저장 되므로 사용자 간 별로 각 사용자가 자신의 보안 질문을 정의 하도록 허용 하는 것이 가능 합니다. 그러나이 예의 namely 유니버설 보안 질문을 사용 하기로: 원하는 색 이란?

이 미리 정의 된 보안 질문을 구현 하려면 이라는 페이지의 코드 숨김 클래스에 상수를 추가 `passwordQuestion`, 보안 질문을 할당 합니다. 그런 다음 합니다 `Page_Load` 이벤트 처리기를 할당 하려면이 상수는 `SecurityQuestion` 레이블의 `Text` 속성:

[!code-vb[Main](creating-user-accounts-vb/samples/sample5.vb)]

다음에 대 한 이벤트 처리기를 만듭니다는 `CreateAccountButton'` s `Click` 이벤트 다음 코드를 추가 합니다.

[!code-vb[Main](creating-user-accounts-vb/samples/sample6.vb)]

합니다 `Click` 이벤트 처리기 라는 변수를 정의 하 여 시작 `createStatus` 형식의 [ `MembershipCreateStatus` ](https://msdn.microsoft.com/library/system.web.security.membershipcreatestatus.aspx)합니다. `MembershipCreateStatus` 상태를 나타내는 열거형을 `CreateUser` 작업 합니다. 예를 들어 결과 사용자 계정을 성공적으로 만들 `MembershipCreateStatus` 인스턴스를 값으로 설정 됩니다 `Success;` 반면에 있는 동일한 사용자 이름 사용 하 여 사용자를 이미 존재 하기 때문에 작업이 실패할 경우 설정 됩니다 의값으로`DuplicateUserName`. 에 `CreateUser` 사용 하 여 오버 로드를 전달할 필요는 `MembershipCreateStatus` 인스턴스 메서드를 합니다. 이 매개 변수 내에서 적절 한 값으로 설정 되는 `CreateUser` 메서드 및에서는 사용자 계정을 성공적으로 만들어졌는지 여부를 결정 하는 메서드를 호출한 후 해당 값을 검사할 수 있습니다.

호출한 후 `CreateUser`전달 `createStatus`, `Select Case` 문을 사용 하에 할당 된 값에 따라 적절 한 메시지를 출력 `createStatus`합니다. 그림 7에서는 새 사용자가 성공적으로 만들어지면 출력을 보여 줍니다. 그림 8과 9에는 사용자 계정이 만들어지지 않은 경우 출력을 보여 줍니다. 그림 8, 방문자 멤버 자격 공급자의 구성 설정에서 명시 하는 암호 강도 요구 사항을 충족 하지 않는 5 자로 암호를 입력 합니다. 그림 9, 방문자를 기존 사용자 이름 (그림 7에서 만든 하나)를 사용 하 여 사용자 계정을 만들 하려고 합니다.


[![새 사용자 계정을 성공적으로 생성 됩니다.](creating-user-accounts-vb/_static/image20.png)](creating-user-accounts-vb/_static/image19.png)

**그림 7**:는 새 사용자 계정을 성공적으로 생성 됩니다 ([큰 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image21.png))


[![제공 된 암호가 너무 약 때문에 사용자 계정이 만들어지지 않습니다.](creating-user-accounts-vb/_static/image23.png)](creating-user-accounts-vb/_static/image22.png)

**그림 8**: 제공 된 암호가 너무 약 때문에 사용자 계정이 만들어지지 않습니다 ([큰 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image24.png))


[![사용자 계정이 생성 때문이 아니라 사용자가 이미 사용](creating-user-accounts-vb/_static/image26.png)](creating-user-accounts-vb/_static/image25.png)

**그림 9**:의 사용자 계정이 생성 때문이 아니라 사용자가 이미 사용에서 ([큰 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image27.png))


> [!NOTE]
> 처음 두 가지 중 하나를 사용 하는 경우 성공 또는 실패를 확인 하는 방법을 궁금할 수 있습니다 `CreateUser` 메서드 오버 로드를 모두의 형식 매개 변수가 있는 `MembershipCreateStatus`합니다. 이러한 처음 두 오버 로드 throw를 [ `MembershipCreateUserException` 예외](https://msdn.microsoft.com/library/system.web.security.membershipcreateuserexception.aspx) 포함 된 오류가 발생 하는 경우를 [ `StatusCode` 속성](https://msdn.microsoft.com/library/system.web.security.membershipcreateuserexception.statuscode.aspx) 형식의 `MembershipCreateStatus`합니다.


소수의 사용자를 만든 후의 내용을 나열 하 여 계정이 만들어졌는지 확인 합니다 `aspnet_Users` 및 `aspnet_Membership` 테이블에 `SecurityTutorials.mdf` 데이터베이스입니다. 통해 두 명의 사용자가 추가한 그림 10과 같이 `CreatingUserAccounts.aspx` 페이지: Tito 및 Bruce 합니다.


[![멤버 자격 사용자 저장소에 두 사용자가 있는: Tito 및 Bruce](creating-user-accounts-vb/_static/image29.png)](creating-user-accounts-vb/_static/image28.png)

**그림 10**: 멤버 자격 사용자 저장소에 두 사용자가 있는: Tito 및 Bruce ([큰 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image30.png))


멤버 자격 사용자 저장소에서 이제 Bruce 및 Tito의 계정 정보를 포함 하는 동안 아직 Bruce 또는 Tito 사이트에 로그온 할 수 있는 기능을 구현 합니다. 현재 `Login.aspx` 사용자의 자격 증명의 유효성을 검사는 사용자 이름/암호 쌍-하드 코드 된 집합에 대해 *하지* 멤버 자격 프레임 워크에 대해 제공된 된 자격 증명의 유효성을 검사 합니다. 이제 새 사용자 계정을 확인 하는 데는 `aspnet_Users` 고 `aspnet_Membership` 테이블 충분 해야 합니다. 다음 자습서에서는  *<a id="_msoanchor_9"> </a> [유효성 검사 사용자 자격 증명에 대해의 멤버 자격 사용자 저장소](validating-user-credentials-against-the-membership-user-store-vb.md)*, 멤버 자격 저장소에 대 한 유효성을 검사 하는 로그인 페이지 업데이트 됩니다.

> [!NOTE]
> 모든 사용자가 표시 되지 않으면 사용자 `SecurityTutorials.mdf` 데이터베이스 되었기 때문일 수 있습니다 웹 응용 프로그램에 기본 멤버 자격 공급자를 사용 하는 `AspNetSqlMembershipProvider`를 사용 하는 `ASPNETDB.mdf` 데이터베이스의 사용자 저장소로. 이것이 문제 인지를 확인 하려면 솔루션 탐색기에서 새로 고침 단추를 클릭 합니다. 라는 데이터베이스가 `ASPNETDB.mdf` 에 추가 되었습니다는 `App_Data` 폴더 문제입니다. 4 단계의 반환 된 *<a id="_msoanchor_10"> </a> [SQL Server에서 멤버 자격 스키마 만들기](creating-the-membership-schema-in-sql-server-vb.md)* 제대로 멤버 자격 공급자를 구성 하는 방법에 대 한 지침은 자습서입니다.


대부분의 시나리오를 만들 사용자 계정, 사용자 이름, 암호, 메일 및이 시점에서 새 계정을 만들어집니다 다른 필수 정보를 입력 하기 위해 일부 인터페이스와 방문자가 표시 됩니다. 이 단계에서는 이러한 인터페이스를 직접 구축에 검토 하 고 사용 하는 방법을 확인 하는 `Membership.CreateUser` 사용자의 입력을 기반으로 하는 메서드를 프로그래밍 방식으로 새 사용자 계정을 추가 합니다. 그러나 코드, 방금 만든 새 사용자 계정입니다. 모든 후속 방금 만든 사용자 계정에서 사이트에 사용자를 로그인 또는 사용자에 게 확인 전자 메일을 보내는 등의 작업을 수행 하지는 않았습니다. 다음 단계 단추에 코드를 추가 해야 합니다. `Click` 이벤트 처리기입니다.

ASP.NET 렌더링 후 계정 및 계정 멤버 자격 프레임 워크에서 만드는 새 사용자 계정을 만들기 위한 사용자 인터페이스에서 사용자 계정 생성 프로세스를 처리 하도록 설계 된 CreateUserWizard 컨트롤을 사용 하 여 제공 됩니다. 만들기 등의 작업을 확인 전자 메일을 보내고 사이트에 방금 만든 사용자를 로그인 합니다. CreateUserWizard 컨트롤을 사용 하 여 간단 하 게 페이지를 도구 상자에서 CreateUserWizard 컨트롤을 끌어서 다음 몇 가지 속성을 설정 합니다. 대부분의 경우에서 코드 한 줄도 작성할 필요가 없습니다. 이 유용한 컨트롤을 6 단계에서에서 자세히 살펴보겠습니다.

사용 하는 코드를 작성 해야 어느 그럴 가능성은 새 사용자 계정을 일반적인 계정 만들기 웹 페이지를 통해 만들어진 경우는 `CreateUser` 메서드, CreateUserWizard 컨트롤은 가능성이 요구 사항을 충족 합니다. 그러나는 `CreateUser` 고도로 사용자 지정 된 계정 만들기 사용자 경험을 해야 하거나 프로그래밍 방식으로 다른 인터페이스를 통해 새 사용자 계정을 생성 해야 하는 경우 메서드는 시나리오에서 유용 하 게 합니다. 예를 들어 사용자가 다른 응용 프로그램에서 사용자 정보를 포함 하는 XML 파일을 업로드 하도록 허용 하는 페이지를 해야 합니다. 페이지 구문 분석 하 여 업로드 된 XML의 콘텐츠 파일을 호출 하 여 XML에서 나타내는 각 사용자에 대 한 새 계정을 만들 수는 `CreateUser` 메서드.

## <a name="step-6-creating-a-new-user-with-the-createuserwizard-control"></a>6 단계: CreateUserWizard 컨트롤을 사용 하 여 새 사용자 만들기

ASP.NET 여러 로그인 웹 컨트롤이 포함 되어 있습니다. 이러한 컨트롤은 여러 가지 일반적인 사용자 계정 및 로그인에 관련 된 시나리오에 도움이 됩니다. 합니다 [CreateUserWizard 컨트롤](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/createuserwizard.aspx) 멤버 자격 프레임 워크에 새 사용자 계정을 추가 하기 위한 사용자 인터페이스를 제공 하도록 설계 된 이러한 컨트롤을 하나입니다.

다른 로그인 관련 웹 컨트롤은 많은 마찬가지로 CreateUserWizard 코드 한 줄도 작성 하지 않고 사용할 수 있습니다. 직관적으로 멤버 자격 공급자의 구성 설정 및 내부적으로 호출 기반 사용자 인터페이스를 제공 합니다 `Membership` 클래스의 `CreateUser` 메서드 후 사용자가 필요한 정보를 입력 하 고 사용자 만들기 단추를 클릭 합니다. CreateUserWizard 컨트롤은 매우 사용자 지정할 수 있습니다. 계정 만들기 프로세스의 다양 한 단계를 실행 하는 이벤트는 있습니다. 계정 만들기 워크플로를 사용자 지정 논리를 삽입 하려면 필요에 따라 이벤트 처리기를 만들 수 있습니다. 또한, CreateUserWizard의 모양을 매우 유연 합니다. 기본 인터페이스의 모양을 정의 하는 속성의 여러 가지 필요한 경우 컨트롤 템플릿으로 변환할 수 있습니다 또는 추가 사용자 등록 단계를 추가할 수 있습니다.

CreateUserWizard 컨트롤의 기본 인터페이스 및 동작을 사용 하 여 참조를 사용 하 여 시작 해 보겠습니다. 컨트롤의 속성 및 이벤트를 통해 모양을 사용자 지정 하는 방법을 다음 살펴보겠습니다.

### <a name="examining-the-createuserwizards-default-interface-and-behavior"></a>CreateUserWizard의 기본 인터페이스 및 동작을 검사합니다.

반환 합니다 `CreatingUserAccounts.aspx` 페이지에서 `Membership` 폴더 디자인 또는 분할 모드를 전환한 후 페이지의 맨 위에 CreateUserWizard 컨트롤을 추가 합니다. CreateUserWizard 컨트롤 도구 상자의 로그인 컨트롤 섹션 아래에 정렬 합니다. 설정 된 컨트롤을 추가한 후 해당 `ID` 속성을 `RegisterUser`입니다. 그림 11에서는에서 스크린샷, 대로 CreateUserWizard 새 사용자의 사용자 이름, 암호, 전자 메일 주소 및 보안 질문 및 답변에 대 한 텍스트 상자를 사용 하 여 인터페이스를 렌더링 합니다.


[![CreateUserWizard 컨트롤 렌더링을 일반 사용자 인터페이스 만들기](creating-user-accounts-vb/_static/image32.png)](creating-user-accounts-vb/_static/image31.png)

**그림 11**: CreateUserWizard 컨트롤 렌더링을 일반 사용자 인터페이스 만들기 ([큰 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image33.png))


5 단계에서에서 만든 인터페이스를 사용 하 여 CreateUserWizard 컨트롤에 의해 생성 된 기본 사용자 인터페이스를 비교할 잠시를 살펴보겠습니다. 먼저 수동으로 만든 인터페이스에는 미리 정의 된 보안 질문을 사용 하는 반면 CreateUserWizard 컨트롤 방문자가 보안 질문 및 대답을 모두 지정할 수 있습니다. CreateUserWizard 컨트롤의 인터페이스 했습니다 아직 인터페이스의 폼 필드에 유효성 검사를 구현 하는 반면 유효성 검사 컨트롤도 포함 됩니다. CreateUserWizard 컨트롤 인터페이스 (함께 텍스트 암호를 입력 하 고 비교 하는 암호 텍스트 상자 같은지를 확인 하는 CompareValidator) 암호 확인 textbox 포함 되어 있습니다.

흥미로운 점은 CreateUserWizard 컨트롤 사용자 인터페이스를 렌더링할 때 멤버 자격 공급자의 구성 파일 참조는입니다. 예를 들어, 보안 질문 및 답변 텍스트 상자는 경우에 표시 `requiresQuestionAndAnswer` 가 True로 설정 합니다. CreateUserWizard는 암호 강도 요구 사항을 충족 되 고이 설정 하는 확인 RegularExpressionValidator 컨트롤을 자동으로 추가 되는 마찬가지로, 해당 `ErrorMessage` 및 `ValidationExpression` 기반으로 하는 속성을 `minRequiredPasswordLength`, `minRequiredNonalphanumericCharacters`, 및 `passwordStrengthRegularExpression` 구성 설정입니다.

파생 이름에서 알 수 있듯이 CreateUserWizard 컨트롤을 [Wizard 컨트롤](https://msdn.microsoft.com/library/s2etd1ek.aspx)합니다. 마법사 컨트롤은 다중 단계 작업을 완료 하기 위한 인터페이스를 제공 하도록 설계 되었습니다. 마법사 컨트롤에는 임의 개수의 있을 `WizardSteps`, HTML을 정의 하는 서식 파일은 각각 및 웹 컨트롤에 대 한 해당 단계입니다. 마법사 컨트롤은 처음에 첫 번째 표시 `WizardStep`, 함께 다음 하나의 단계를 진행 하기 하거나 이전 단계로 돌아갈 사용자를 허용 하는 탐색 컨트롤입니다.

그림 11에 있는 선언적 태그에서 알 수 있듯이, CreateUserWizard 컨트롤의 기본 인터페이스 포함 두 `WizardStep` s:

- [`CreateUserWizardStep`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizardstep.aspx) ? 새 사용자 계정 만들기에 대 한 정보를 수집 하는 인터페이스를 렌더링 합니다. 그림 11에 나와 있는 단계입니다.
- [`CompleteWizardStep`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.completewizardstep.aspx) ? 계정이 성공적으로 생성 되어 있는지를 나타내는 메시지를 렌더링 합니다.

CreateUserWizard의 모양 및 동작을 수정할 수 템플릿에 이러한 단계 중 하나를 변환 하 여 직접 추가 하 여 `WizardStep` s입니다. 추가 살펴보겠습니다를 `WizardStep` 등록 인터페이스를 *추가 사용자 정보 저장* 자습서입니다.

CreateUserWizard 컨트롤의 작동을 확인해 보겠습니다. 방문을 `CreatingUserAccounts.aspx` 브라우저를 통해 페이지입니다. CreateUserWizard의 인터페이스에 일부 잘못 된 값을 입력 하 여 시작 합니다. 시도 암호 강도 요구 사항에 맞지 않는 암호를 입력 하거나 사용자 이름 텍스트 상자를 비워 두면 됩니다. CreateUserWizard는 적절 한 오류 메시지가 표시 됩니다. 그림 12 분산이 강력한 암호를 사용 하 여 사용자를 만들려고 할 때 출력을 보여줍니다.


[![CreateUserWizard 컨트롤 유효성 검사를 자동으로 삽입](creating-user-accounts-vb/_static/image35.png)](creating-user-accounts-vb/_static/image34.png)

**그림 12**: The CreateUserWizard 자동으로 삽입 유효성 검사 컨트롤 ([큰 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image36.png))


다음으로, CreateUserWizard에 적절 한 값을 입력 하 고 사용자 만들기 단추를 클릭 합니다. 필수 필드에 입력 되 었어야 하 고 암호의 강도가 충분 한 가정 하 고, CreateUserWizard 멤버 자격 프레임 워크를 통해 새 사용자 계정을 만들고 다음 표시는 `CompleteWizardStep`의 인터페이스 (그림 13 참조). CreateUserWizard 내부적으로 호출 된 `Membership.CreateUser` 5 단계에서에서 수행한 것 처럼 메서드.


[![새 사용자 계정에 성공적으로 생성 된](creating-user-accounts-vb/_static/image38.png)](creating-user-accounts-vb/_static/image37.png)

**그림 13**: 새 사용자 계정에 성공적으로 생성 된 ([큰 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image39.png))


> [!NOTE]
> 그림 13에서 볼 수 있듯이 `CompleteWizardStep`의 인터페이스에는 계속 단추가 포함 됩니다. 그러나이 시점에서 바로 클릭 같은 페이지를 방문자를 두면 포스트백을 수행 합니다. 사용자 지정 하기 CreateUserWizard의 모양 및 동작을 통해 해당 속성 섹션에서는 방식 방문자를 전송 하는이 단추를 사용할 수 있습니다 살펴봅니다 `Default.aspx` (또는 일부 다른 페이지).


새 사용자 계정을 만들면 Visual Studio로 돌아가서 및 검사 합니다 `aspnet_Users` 및 `aspnet_Membership` 계정을 성공적으로 만들어졌는지 확인 하려면 그림 10에서 수행한 것 처럼 테이블입니다.

### <a name="customizing-the-createuserwizards-behavior-and-appearance-through-its-properties"></a>CreateUserWizard의 동작 및 해당 속성을 통해 모양을 사용자 지정

CreateUserWizard 다양 한 방법으로 속성을 통해 사용자 지정할 수 있습니다 `WizardStep` 및 이벤트 처리기입니다. 이 섹션에서 살펴보겠습니다 해당 속성을 통해 컨트롤의 모양을 사용자 지정 하는 방법 다음 섹션에서는 이벤트 처리기를 통해 컨트롤의 동작을 확장 살펴봅니다.

CreateUserWizard 컨트롤의 기본 사용자 인터페이스에 표시 되는 텍스트의 거의 모든 사용자는 다양 한 속성을 통해 지정할 수 있습니다. 예를 들어 입력란의 왼쪽에 표시 되는 사용자 이름, 암호, 암호 확인, 전자 메일, 보안 질문 및 보안 대답 레이블을 사용자 지정할 수 있습니다 합니다 [ `UserNameLabelText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.usernamelabeltext.aspx)하십시오 [ `PasswordLabelText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.passwordlabeltext.aspx), [ `ConfirmPasswordLabelText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.confirmpasswordlabeltext.aspx), [ `EmailLabelText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.emaillabeltext.aspx)하십시오 [ `QuestionLabelText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.questionlabeltext.aspx), 및 [ `AnswerLabelText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.answerlabeltext.aspx) 속성을 각각. 마찬가지로 만들 사용자와 계속 단추에 텍스트를 지정 하는 속성을 `CreateUserWizardStep` 및 `CompleteWizardStep`이면도 대로 이러한 단추는 Linkbutton을 단추나 ImageButtons로 렌더링 됩니다.

색, 테두리, 글꼴 및 기타 시각적 요소 스타일 속성의 호스트를 통해 구성할 수 있습니다. CreateUserWizard 컨트롤 자체에 일반적인 웹 컨트롤 스타일 속성- `BackColor`, `BorderStyle`, `CssClass`, `Font`등에-아니며의 모양을 정의 하 고 특정 부분에 대 한 스타일 속성 수를 CreateUserWizard의 인터페이스입니다. [ `TextBoxStyle` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.textboxstyle.aspx), 예를 들어에서 텍스트 상자에 대 한 스타일을 정의 합니다 `CreateUserWizardStep`, 하는 동안는 [ `TitleTextStyle` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.titletextstyle.aspx) 스타일을 정의 합니다 (등록 사용자 새 제목에 대 한 계정)입니다.

모양과 관련 된 속성 외에도 많은 CreateUserWizard 컨트롤의 동작에 영향을 주는 속성이 있습니다. 합니다 [ `DisplayCancelButton` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.wizard.displaycancelbutton.aspx)이면 True를 표시 합니다 (기본값은 False) Create User 단추 옆에 있는 취소 단추를 설정 합니다. 취소 단추를 표시 하는 경우도 설정 해야 합니다 [ `CancelDestinationPageUrl` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx), 취소 클릭 한 후 보낼 사용자 페이지를 지정 하는 합니다. 계속 단추에 이전 섹션에서 설명 했 듯이 `CompleteWizardStep`의 인터페이스 포스트백을 두고 동일한 페이지의 방문자입니다. 계속 단추를 클릭 한 후 다른 페이지로 방문자를 보내도록에서 URL을 지정 하기만 합니다 [ `ContinueDestinationPageUrl` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)합니다.

업데이트 해 보겠습니다 합니다 `RegisterUser` CreateUserWizard 컨트롤 취소 단추를 표시 하 고 방문자를 보낼 `Default.aspx` 취소 또는 계속 단추를 클릭할 때입니다. 이를 위해 설정 합니다 `DisplayCancelButton` 속성을 true로, 합니다 `CancelDestinationPageUrl` 및 `ContinueDestinationPageUrl` 속성을 ~ / Default.aspx입니다. 그림 14에서는 브라우저를 통해 볼 때 업데이트 된 CreateUserWizard를 보여 줍니다.


[![CreateUserWizardStep 취소 단추가 포함 됩니다.](creating-user-accounts-vb/_static/image41.png)](creating-user-accounts-vb/_static/image40.png)

**그림 14**: 합니다 `CreateUserWizardStep` 취소 단추가 포함 됩니다 ([클릭 하 여 큰 이미지 보기](creating-user-accounts-vb/_static/image42.png))


방문자를 사용자 이름, 암호, 전자 메일 주소 및 보안 질문 및 답변을 입력 하 고 사용자 만들기를 클릭 하면, 새 사용자 계정을 만들고 방문자가 새로 생성된 된 해당 사용자로 로그인 합니다. 페이지를 방문 하는 사용자가 자신에 대 한 새 계정을 만들 가정 이것이 원하는 동작을 것입니다. 그러나 다음 새 사용자 계정을 추가 하려면 관리자가 허용 하는 것이 좋습니다. 이 과정에서 사용자 계정에 만들어집니다 있지만 관리자로 (및 새로 만든된 계정 아니라) 관리자 로그인 남습니다. 부울을 통해이 동작을 수정할 수 있습니다 [ `LoginCreatedUser` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.logincreateduser.aspx)합니다.

멤버 자격 프레임 워크에서 사용자 계정을 포함은 승인 된 플래그입니다. 승인 되지 않은 사용자가 사이트에 로그인 하지 못합니다. 기본적으로 새로 만든된 계정에는 사용자가 즉시 사이트에 로그인 할 수 있도록 승인 됨으로 표시 됩니다. 그러나, 승인 되지 않은 것으로 표시 하는 새 사용자 계정을 사용 하는 것이 가능입니다. 로그인 할 수 있는; 전에 새 사용자를 수동으로 승인 하려면 관리자 권한 필요 또는 사용자 로그온을 허용 하기 전에 등록 시 입력 한 전자 메일 주소가 올바른지 확인 하려고 할 수도 있습니다. 원하는 경우 수 있습니다 새로 만든된 사용자 계정이 CreateUserWizard 컨트롤을 설정 하 여 승인 되지 않은 것으로 표시 [ `DisableCreatedUser` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.disablecreateduser.aspx) true (기본값은 False)입니다.

참고의 다른 동작 관련 속성 포함 `AutoGeneratePassword` 고 `MailDefinition`입니다. 경우는 [ `AutoGeneratePassword` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.autogeneratepassword.aspx) True로 설정 되는 `CreateUserWizardStep` 암호 및 암호 확인 텍스트 상자;를 표시 하지 않습니다 대신 새로 만든 사용자의 암호는 자동으로 사용 하 여 생성를 `Membership` 클래스의 [ `GeneratePassword` 메서드](https://msdn.microsoft.com/library/system.web.security.membership.generatepassword.aspx)합니다. `GeneratePassword` 메서드는 지정 된 길이 및 영숫자가 아닌 문자 구성 된 암호 강도 요구 사항을 충족 하기 위해 충분 한 수를 사용 하 여 암호를 생성 합니다.

합니다 [ `MailDefinition` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.maildefinition.aspx) 계정 만들기 프로세스 중에 지정 된 전자 메일 주소로 전자 메일을 보내려는 경우에 유용 합니다. `MailDefinition` 속성 일련의 생성 된 전자 메일 메시지에 대 한 정보를 정의 하는 것에 대 한 하위 속성을 포함 합니다. 이러한 하위 속성 같은 옵션을 포함할 `Subject`, `Priority`, `IsBodyHtml`, `From`, `CC`, 및 `BodyFileName`합니다. 합니다 [ `BodyFileName` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.bodyfilename.aspx) 텍스트 또는 전자 메일 메시지의 본문을 포함 하는 HTML 파일을 가리킵니다. 본문 미리 정의 된 두 명의 자리 표시자를 지원 합니다. `<%UserName%>` 및 `<%Password%>`합니다. 이러한 자리 표시이 자가 있는 경우는 `BodyFileName` 파일, 방금 만든 사용자의 이름 및 암호를 사용 하 여 바뀝니다.

> [!NOTE]
> 합니다 `CreateUserWizard` 컨트롤의 `MailDefinition` 속성 새 계정을 만들 때 전송 되는 전자 메일 메시지에 대 한 정보를 지정 합니다. 전자 메일 메시지는 실제로 전송 하는 방법에 대 한 세부 정보는 포함 되지 않습니다 (즉, SMTP 서버 또는 메일 드롭 디렉터리를 사용 되는지 여부, 모든 인증 정보 및 등). 이러한 하위 수준 세부 정보에서 정의 해야 합니다 `<system.net>` 단원의 `Web.config`합니다. 이러한 구성 설정에 대 한 일반적 ASP.NET 2.0에서 전자 메일을 보내는 방법에 자세한 내용은 참조는 [SystemNetMail.com에서 Faq](http://www.systemnetmail.com/) 및 필자의 기사 [ASP.NET 2.0의 전자 메일 보내기](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)합니다.


### <a name="extending-the-createuserwizards-behavior-using-event-handlers"></a>이벤트 처리기를 사용 하 여 CreateUserWizard의 동작을 확장 합니다.

CreateUserWizard 컨트롤 해당 워크플로 중에 다양을 한 이벤트를 발생 시킵니다. 예를 들어, 방문자를 자신의 사용자 이름, 암호 및 기타 관련 정보를 입력 하 고 사용자 만들기 단추를 클릭 한 후 CreateUserWizard 컨트롤 발생 해당 [ `CreatingUser` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.creatinguser.aspx)합니다. 하지만 만들기 프로세스 중에 문제가 있으면를 [ `CreateUserError` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createusererror.aspx) 이벤트가 발생 이면 사용자가 성공적으로 만들어지면 해당 [ `CreatedUser` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx) 발생 합니다. 추가 CreateUserWizard 컨트롤 이벤트를 발생 시킬 있지만 이러한 세 가지 가장 밀접 것입니다.

특정 시나리오에서는 할 탭 CreateUserWizard 워크플로에 적절 한 이벤트에 대 한 이벤트 처리기를 만들어 수행할 수 있습니다. 예를 들어를 개선해 보겠습니다는 `RegisterUser` CreateUserWizard 컨트롤 사용자 이름 및 암호에 일부 사용자 지정 유효성 검사를 포함 합니다. 특히 개선해 보겠습니다 우리의 CreateUserWizard 사용자 이름에 선행 또는 후행 공백을 포함할 수 없습니다 하 고 사용자 이름 암호에 어디서 나 나타날 수 없습니다. 즉, 다른 사용자와 "Scott" 같은 사용자 이름을 만들거나 Scott Scott.1234 등 사용자 이름/암호 조합을 것을 방지 하려고 합니다.

에 대 한 이벤트 처리기를 만들겠습니다이 작업을 수행 하는 `CreatingUser` 우리의 추가 유효성 검사를 수행 하는 이벤트입니다. 제공 된 데이터를 유효 하지 않은 경우 생성 프로세스를 취소 해야 합니다. 또한 사용자 이름 또는 암호가 잘못 되었음을 설명 하는 메시지를 표시 하려면 페이지 레이블 웹 컨트롤을 추가 해야 합니다. 시작 설정, CreateUserWizard 컨트롤 아래에 레이블 컨트롤을 추가 하 여 해당 `ID` 속성을 `InvalidUserNameOrPasswordMessage` 및 해당 `ForeColor` 속성을 `Red`입니다. 지웁니다 해당 `Text` 속성 집합과 해당 `EnableViewState` 고 `Visible` 속성을 false로 합니다.

[!code-aspx[Main](creating-user-accounts-vb/samples/sample7.aspx)]

다음으로, CreateUserWizard 컨트롤에 대 한 이벤트 처리기를 만들고 `CreatingUser` 이벤트입니다. 이벤트 처리기를 만들려면 디자이너에서 컨트롤을 선택 하 고 속성 창으로 이동 합니다. 여기에서 번개 모양 아이콘 클릭 한 다음 이벤트 처리기를 만들려면 적절 한 이벤트를 두 번 클릭 합니다.

다음 코드를 `CreatingUser` 이벤트 처리기에 추가합니다.

[!code-vb[Main](creating-user-accounts-vb/samples/sample8.vb)]

사용자 이름 및 CreateUserWizard 컨트롤에 입력 한 암호를 통해 사용할 수는 해당 [ `UserName` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.username.aspx) 하 고 [ `Password` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.password.aspx), 각각. 제공 된 사용자 이름은 선행 또는 후행 공백이 포함 되는지 여부 및 사용자 이름 암호가 있는지 여부를 확인 하려면 위의 이벤트 처리기에서 이러한 속성을 사용 했습니다. 에 오류 메시지가 표시 됩니다 이러한 조건 중 하나가 충족 될 경우는 `InvalidUserNameOrPasswordMessage` 레이블 및 해당 이벤트 처리기 `e.Cancel` 속성이 `True`합니다. 하는 경우 `e.Cancel` 로 설정 된 `True`, CreateUserWizard 단락 (short-circuit) 워크플로 효과적으로 사용자 계정 만들기 프로세스를 취소 합니다.

그림 15의 스크린 샷을 보여 줍니다 `CreatingUserAccounts.aspx` 사용자가 선행 공백을 사용 하 여 사용자 이름을 입력 하는 경우.


[![사용자 이름은 선행 또는 후행 공백이 허용 되지 않습니다.](creating-user-accounts-vb/_static/image44.png)](creating-user-accounts-vb/_static/image43.png)

**그림 15**: 사용자 이름은 선행 또는 후행 공백이 허용 되지 않습니다 ([큰 이미지를 보려면 클릭](creating-user-accounts-vb/_static/image45.png))


> [!NOTE]
> CreateUserWizard 컨트롤을 사용 하는 예제를 살펴봅니다 `CreatedUser` 이벤트에는 *<a id="_msoanchor_11"> </a> [추가 사용자 정보 저장](storing-additional-user-information-vb.md)* 자습서입니다.


## <a name="summary"></a>요약

합니다 `Membership` 클래스의 `CreateUser` 메서드 멤버 자격 프레임 워크에 새 사용자 계정을 만듭니다. 구성된 된 멤버 자격 공급자에 대 한 호출을 위임 하 여 수행 합니다. 경우에 `SqlMembershipProvider`, `CreateUser` 레코드를 추가 하는 메서드는 `aspnet_Users` 및 `aspnet_Membership` 데이터베이스 테이블입니다.

프로그래밍 방식으로 (살펴본 것 처럼 5 단계에서에서) 새 사용자 계정을 만들 수 있지만 CreateUserWizard 컨트롤을 사용 하는 빠르고 쉬운 방법이입니다. 이 컨트롤에 사용자 정보를 수집 하 고 멤버 자격 프레임 워크에서 새 사용자를 만들기 위한 여러 단계의 사용자 인터페이스를 렌더링 합니다. 이 컨트롤은 동일한 내부적으로 `Membership.CreateUser` 5 단계 있지만 컨트롤에서 검사할 메서드 유효성 검사 컨트롤 사용자 인터페이스를 만들고 코드를 전혀 작성 하지 않고도 사용자 계정 만들기 오류에 응답 합니다.

이 시점에서 기능을 새 사용자 계정을 만들 수 있습니다. 그러나 로그인 페이지 여전히의 유효성을 검사할 두 번째 자습서에 다시 지정한 하드 코드 된 자격 증명에 대 한 합니다. 에 <a id="_msoanchor_12"> </a> [다음 자습서](validating-user-credentials-against-the-membership-user-store-vb.md) 업데이트 `Login.aspx` 의 유효성을 검사할 사용자 멤버 자격 프레임 워크에 대해 자격 증명 제공 합니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [`CreateUser` 기술 문서](https://msdn.microsoft.com/library/system.web.security.membershipprovider.createuser.aspx)
- [CreateUserWizard 컨트롤 개요](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/createuserwizard.aspx)
- [파일 시스템 기반 사이트 맵 공급자 만들기](http://aspnet.4guysfromrolla.com/articles/020106-1.aspx)
- [ASP.NET 2.0 Wizard 컨트롤을 사용한 단계별 사용자 인터페이스 만들기](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)
- [사이트 탐색의 ASP.NET 2.0 검사](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [마스터 페이지 및 사이트 탐색](https://asp.net/learn/data-access/tutorial-03-vb.aspx)
- [에 대 한 왔습니다 SQL 사이트 맵 공급자](https://msdn.microsoft.com/msdnmag/issues/06/02/WickedCode/default.aspx)

### <a name="about-the-author"></a>저자 소개

Scott Mitchell, 여러 ASP/ASP.NET 책의 저자 이자 4GuysFromRolla.com의 설립자 이며 1998 Microsoft 웹 기술을 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는  *[Sams 설명 직접 ASP.NET 2.0 24 시간 동안의](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 합니다. Scott에 도달할 수 있습니다 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 통하거나 저자의 블로그 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Teresa Murphy 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4guysfromrolla.com)합니다.

> [!div class="step-by-step"]
> [이전](creating-the-membership-schema-in-sql-server-vb.md)
> [다음](validating-user-credentials-against-the-membership-user-store-vb.md)
