---
uid: web-forms/overview/older-versions-security/membership/creating-user-accounts-cs
title: 사용자 계정 (C#) 만들기 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 살펴볼 것입니다 (SqlMembershipProvider)를 통해 멤버 자격이 프레임 워크를 사용 하 여 새 사용자 계정을 만들 수 있습니다. 주세요. 새로 만드는 방법에 확인해 보겠습니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/18/2008
ms.topic: article
ms.assetid: f175278c-6079-4d91-b9b4-2493ed43d9ec
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-security/membership/creating-user-accounts-cs
msc.type: authoredcontent
ms.openlocfilehash: e00417639fba71083cbf392db5d5078561ab26e3
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30892181"
---
<a name="creating-user-accounts-c"></a>사용자 계정 (C#) 만들기
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_05_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial05_CreatingUsers_cs.pdf)

> 이 자습서에서는 살펴볼 것입니다 (SqlMembershipProvider)를 통해 멤버 자격이 프레임 워크를 사용 하 여 새 사용자 계정을 만들 수 있습니다. 프로그래밍 방식으로 및 ASP을 통해 새 사용자를 만드는 방법을 살펴봅니다. NET의 기본 제공 CreateUserWizard 컨트롤입니다.


## <a name="introduction"></a>소개

에 <a id="_msoanchor_1"> </a> [이전 자습서](creating-the-membership-schema-in-sql-server-cs.md) 테이블, 뷰, 추가 하 고 저장 프로시저에서 필요로 하는 데이터베이스에 응용 프로그램 서비스 스키마를 설치 했습니다는 `SqlMembershipProvider` 및 `SqlRoleProvider`합니다. 이이 시리즈의 자습서의 나머지 부분에 대 한 필요한 인프라를 생성 합니다. 이 자습서에서는 살펴볼 것 구성원 프레임 워크를 사용 하 여 (통해는 `SqlMembershipProvider`) 새 사용자 계정을 만들 수 있습니다. 프로그래밍 방식으로 및 ASP을 통해 새 사용자를 만드는 방법을 살펴봅니다. NET의 기본 제공 CreateUserWizard 컨트롤입니다.

새 사용자 계정을 만드는 방법을 학습 하는 것 외에도 처음에 만든 데모 웹 사이트를 업데이트 해야 또한 됩니다는 *<a id="_msoanchor_2"> </a> [폼 인증의 개요는](../introduction/an-overview-of-forms-authentication-cs.md)* 자습서 및 다음에 향상 된는  *<a id="https://www.asp.net/learn/security/tutorial-03-cs.aspx"> </a> 폼 인증 구성 및 고급 항목* 자습서입니다. 데모 웹 응용 프로그램에 하드 코드 된 사용자 이름/암호 쌍에 대 한 사용자의 자격 증명의 유효성을 검사 하는 로그인 페이지를 있습니다. 또한 `Global.asax` 만드는 사용자 지정 코드를 포함 `IPrincipal` 및 `IIdentity` 인증 된 사용자에 대 한 개체입니다. 멤버 자격 framework에 대 한 사용자의 자격 증명의 유효성을 검사 하 고 사용자 지정 보안 주체 및 id 논리를 제거 하는 로그인 페이지를 업데이트 됩니다.

이제 시작 하겠습니다.

## <a name="the-forms-authentication-and-membership-checklist"></a>폼 인증 및 구성원 검사 목록

멤버 자격 프레임 워크와 작업을 시작 하기 전에이 시점까지 이동 하는 중요 한 단계를 검토 하려면 잠시 하겠습니다. 멤버 자격 framework를 사용 하는 경우는 `SqlMembershipProvider` 폼 기반 인증 시나리오에서는 다음 단계에서 웹 응용 프로그램 멤버 자격 기능을 구현 하기 전에 수행 해야 합니다.

1. **폼 기반 인증을 사용 하도록 설정 합니다.** 설명한 것 처럼  *<a id="_msoanchor_4"> </a> [폼 인증의 개요는](../introduction/an-overview-of-forms-authentication-cs.md)*, 편집 하 여 폼 인증을 사용 하는 `Web.config` 설정는 `<authentication>` 요소의 `mode` 특성을 `Forms`합니다. 폼 인증 사용을 들어오는 각 요청을 검사 하는 *폼 인증 티켓*, 있는 경우 식별 하는 요청 자가 있습니다.
2. **해당 데이터베이스에 응용 프로그램 서비스 스키마를 추가 합니다.** 사용 하는 경우는 `SqlMembershipProvider` 데이터베이스에 응용 프로그램 서비스 스키마를 설치 해야 합니다. 일반적으로이 스키마는 응용 프로그램의 데이터 모델을 보유 하는 동일한 데이터베이스에 추가 됩니다. *<a id="_msoanchor_5"> </a> [SQL Server에서 멤버 자격 스키마 만들기](creating-the-membership-schema-in-sql-server-cs.md)* 자습서를 사용 하 여에 검토는 `aspnet_regsql.exe` 이를 위해 도구입니다.
3. **2 단계에서 데이터베이스를 참조 하는 웹 응용 프로그램의 설정을 사용자 지정 합니다.** *SQL Server에서 멤버 자격 스키마 만들기* 자습서 웹 응용 프로그램을 구성 하는 두 가지 방법을 보여 주었습니다 있도록는 `SqlMembershipProvider` 2 단계에서 선택한 데이터베이스를 사용 합니다: 수정 하 여는 `LocalSqlServer` 연결 문자열 이름입니다. 또는 프레임 워크 멤버 자격 공급자의 목록에 새 등록 된 공급자를 추가 하는 새 공급자에서 데이터베이스를 사용 하도록 사용자 지정 하 여 2 단계.

사용 하는 웹 응용 프로그램을 빌드할 경우는 `SqlMembershipProvider` 폼 기반 인증을 해야 합니다를 사용 하기 전에 이러한 세 단계를 수행 하 고는 `Membership` 클래스 또는 ASP.NET 로그인 웹 컨트롤입니다. 이전 자습서의 다음이 단계를 이미 수행한 म 이후 준비가 구성원 프레임 워크를 사용 하 여 시작!

## <a name="step-1-adding-new-aspnet-pages"></a>1 단계: 새 ASP.NET 페이지를 추가합니다.

이 자습서에는 다음 세 우리는 수 검사 다양 한 멤버 자격 관련 기능 및 기능 합니다. 일련의 전체이 자습서에서 설명 하는 항목을 구현 하는 ASP.NET 페이지가 필요 합니다. 이러한 페이지 및 사이트 맵 파일을 만들어 보겠습니다 `(Web.sitemap)`합니다.

시작 이라는 프로젝트에 새 폴더를 만들어서 `Membership`합니다. 다음에 5 개의 새 ASP.NET 페이지에는 추가 `Membership` 폴더를 연결 된 각 페이지는 `Site.master` 마스터 페이지입니다. 페이지 이름을 지정 합니다.

- `CreatingUserAccounts.aspx`
- `UserBasedAuthorization.aspx`
- `EnhancedCreateUserWizard.aspx`
- `AdditionalUserInfo.aspx`
- `Guestbook.aspx`

이 시점에서 프로젝트의 솔루션 탐색기에 스크린 샷을 그림 1에 표시 된 비슷해야 합니다.


[![멤버 자격 폴더에 추가 된 새 페이지 5 개](creating-user-accounts-cs/_static/image2.png)](creating-user-accounts-cs/_static/image1.png)

**그림 1**: 5 개의 새 페이지에 추가 된는 `Membership` 폴더 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-cs/_static/image3.png))


각 페이지,이 시점에서 있어야 마스터 페이지의 contentplaceholders의 마다 하나씩 두 개의 콘텐츠 컨트롤: `MainContent` 및 `LoginContent`합니다.

[!code-aspx[Main](creating-user-accounts-cs/samples/sample1.aspx)]

이전에 설명한 대로 `LoginContent` ContentPlaceHolder의 기본 태그 로그온 하거나 로그 오프 사용자가 인증 되는지 여부에 따라 사이트에 대 한 링크를 표시 합니다. 그러나 존재는 `Content2` 콘텐츠 컨트롤에 마스터 페이지의 기본 태그 보다 우선 합니다. 설명한 것 처럼 *<a id="_msoanchor_6"> </a> [폼 인증의 개요는](../introduction/an-overview-of-forms-authentication-cs.md)* 자습서에서는이 여기서 म 하지 않으려는 왼쪽된 열에 표시 되는 로그인 관련 옵션 페이지에 유용 합니다.

그러나 이러한 5 개 페이지에 대 한 표시 하려고에 대 한 마스터 페이지의 기본 태그는 `LoginContent` ContentPlaceHolder 합니다. 따라서 태그에 대 한 선언적 태그를 제거는 `Content2` 콘텐츠 컨트롤을 합니다. 이렇게 한 다음 5 개 페이지의 태그의 각 콘텐츠 컨트롤을 한 개만 있어야 합니다.

## <a name="step-2-creating-the-site-map"></a>2 단계: 사이트 맵 만들기

가장 간단한 웹 사이트를 제외한 모든 탐색 사용자 인터페이스의 기능을 구현 해야 합니다. 탐색 사용자 인터페이스에는 사이트의 다양 한 섹션에 대 한 링크 간단한 목록 수 있습니다. 또는 메뉴 또는 트리 보기에 이러한 링크를 정렬할 수 있습니다. 페이지 개발자 탐색 사용자 인터페이스 만들기는 스토리의 절반에 있습니다. 또한 관리 하 고 업데이트할 수 있는 방식으로 사이트의 논리 구조를 정의 하기 위한 방법이 필요 합니다. 새 페이지 추가 되거나 기존 페이지는 제거, – 사이트 맵 – 단일 소스를 업데이트할 수 있게 되기를 원하는 되며 이러한 수정 사항을 사이트의 탐색 사용자 인터페이스를 통해 반영 됩니다.

이 두 가지 작업 – 사이트 맵을 정의 하 고 사이트 맵을 기반으로 하는 탐색 사용자 인터페이스를 구현-사이트 맵 프레임 워크 덕분에 수행 하기 위해 쉽게 있으며 ASP.NET 버전 2.0에에서 탐색 웹 컨트롤을 추가할 합니다. 사이트 맵을 정의 하는 개발자에 대 한 사이트 맵 프레임 워크에서는 프로그래밍 방식으로 API를 통해 액세스 한 다음 (의 [ `SiteMap` 클래스](https://msdn.microsoft.com/library/system.web.sitemap.aspx)). 웹 탐색을 제어 하는 기본 제공 포함 한 [Menu 컨트롤](https://msdn.microsoft.com/library/bz09dy46.aspx), [TreeView 컨트롤](https://msdn.microsoft.com/library/3eafky27.aspx), 및 [SiteMapPath 컨트롤](https://msdn.microsoft.com/library/3eafky27.aspx)합니다.

멤버 자격 및 역할 프레임 워크와 같은 사이트 맵 프레임 워크 위에 빌드된는 [공급자 모델](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)합니다. 사이트 맵 공급자 클래스의 작업에서 사용 하는 메모리 내 구조를 생성 하는 것은 `SiteMap` XML 파일 또는 데이터베이스 테이블 등의 영구 데이터 저장소에서 클래스입니다. XML 파일에서 사이트 맵 데이터를 읽을 수 있는 기본 사이트 맵 공급자와 함께 제공 되는.NET Framework ([`XmlSiteMapProvider`](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx)), 이것은 공급자가 자습서에서를 사용 합니다. 일부 대체 사이트 맵 공급자 구현에 대 한이 자습서의 끝에 추가 정보 섹션을 참조 합니다.

기본 사이트 맵 공급자 라는 올바르게 서식이 지정 된 XML 파일에서는 `Web.sitemap` 루트 디렉터리에 존재 합니다. 이 기본 공급자를 사용 하는 원하므로 하 이러한 파일을 추가 하 고 적절 한 XML 형식의 사이트 맵 구조를 정의 해야 합니다. 파일을 추가 하려면 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가 선택 합니다. 대화 상자에서 사이트 맵 이라는 형식의 파일을 추가 하도록 선택할 `Web.sitemap`합니다.


[![프로젝트의 루트 디렉터리로 Web.sitemap 라는 파일](creating-user-accounts-cs/_static/image5.png)](creating-user-accounts-cs/_static/image4.png)

**그림 2**: 라는 파일 추가 `Web.sitemap` 프로젝트의 루트 디렉터리로 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-cs/_static/image6.png))


XML 사이트 맵 파일을 계층으로 웹 사이트의 구조를 정의합니다. 이 계층 관계의 상위 구조를 통해 XML 파일에서 모델링 됩니다는 `<siteMapNode>` 요소입니다. `Web.sitemap` 로 시작 해야 합니다는 `<siteMap>` 정확 하 게 하나를 갖는 부모 노드 `<siteMapNode>` 자식입니다. 이 최상위 `<siteMapNode>` 요소는 계층의 루트를 나타내며 임의 개수의 하위 노드가 있을 수 있습니다. 각 `<siteMapNode>` 요소 포함 되어야 합니다는 `title` 특성을 선택적으로 포함 될 수 있습니다 `url` 및 `description` 특성의 경우; 다른 규칙 으로부터 각 비어 있지 않은 `url` 특성은 고유 해야 합니다.

다음 XML 입력의 `Web.sitemap` 파일:

[!code-xml[Main](creating-user-accounts-cs/samples/sample2.xml)]

위의 사이트 맵 태그는 그림 3과 같이 계층 구조를 정의 합니다.


[![사이트 맵 탐색 계층 구조를 나타냅니다.](creating-user-accounts-cs/_static/image8.png)](creating-user-accounts-cs/_static/image7.png)

**그림 3**: 사이트 맵 탐색 계층 구조를 나타냅니다 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-cs/_static/image9.png))


## <a name="step-3-updating-the-master-page-to-include-a-navigational-user-interface"></a>3 단계: 탐색 사용자 인터페이스를 포함 하도록 마스터 페이지를 업데이트 합니다.

ASP.NET에는 여러 사용자 인터페이스 디자인에 대 한 탐색 관련 웹 컨트롤이 포함 되어 있습니다. 여기에 메뉴, TreeView SiteMapPath 컨트롤 포함 됩니다. 메뉴 및 TreeView 컨트롤이 SiteMapPath 상위 뿐만 아니라 방문 되 고 현재 노드가 표시 된 이동 경로 표시 합니다. 사이트 맵 구조는 트리 또는 메뉴에 각각 렌더링 합니다. 사이트 맵 데이터 웹 컨트롤은 SiteMapDataSource를 사용 하 여 다른 데이터에 바인딩될 수 있으며를 통해 프로그래밍 방식으로 액세스할 수는 `SiteMap` 클래스입니다.

이 자습서 시리즈의 범위를 벗어나는 대 한 자세한 설명은 사이트 맵 프레임 워크 및 탐색 컨트롤 이므로 대신 보겠습니다 고유한 탐색 사용자 인터페이스를 만들어 시간 보다 대신 빌릴 사용 되는 내 *[ ASP.NET 2.0에서 데이터 작업](../../data-access/index.md)* 그림 4에 나와 있는 것 처럼 두 심층 글머리 기호 목록이 탐색 링크를 표시 하려면 반복기 컨트롤을 사용 하는 자습서 시리즈 합니다.

### <a name="adding-a-two-level-list-of-links-in-the-left-column"></a>왼쪽된 열에 대 한 링크 목록이 두 수준의 추가

이 인터페이스를 만들려면 다음과 같은 선언적 태그를 추가 `Site.master` 마스터 페이지의 왼쪽 열에 텍스트 "TODO: 메뉴는 여기로 이동..." 현재 상주 합니다.

[!code-aspx[Main](creating-user-accounts-cs/samples/sample3.aspx)]

위의 태그 바인딩하 라는 반복기 컨트롤 `menu` SiteMapDataSource를 반환 하는 사이트 맵 계층에 정의 된 `Web.sitemap`합니다. SiteMapDataSource 컨트롤의 이후 [ `ShowStartingNode` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemapdatasource.showstartingnode.aspx) "홈" 노드의 하위 항목이 시작 되는 사이트 맵 계층 반환을 시작 하는 False로 설정 됩니다. 반복기에서 이러한 각 노드 (현재 방금 "구성원")를 표시 한 `<li>` 요소입니다. 다른, 내부 반복기는 중첩된 된 순서가 지정 되지 않은 목록에 현재 노드의 자식을 표시합니다.

그림 4는 2 단계에서에서 만든 사이트 맵 구조를 사용 하 여 위의 태그의 렌더링 된 출력을 보여줍니다. 반복기 바닐라 순서가 지정 되지 않은 목록 태그;를 렌더링합니다. 에 정의 된 연계 스타일 시트 규칙 `Styles.css` -시선을 레이아웃을 담당 합니다. 위의 태그의 작동 방식을 보다 자세한 내용은 참조는 [마스터 페이지 및 사이트 탐색](https://asp.net/learn/data-access/tutorial-03-cs.aspx) 자습서입니다.


[![탐색 사용자 인터페이스는 렌더링 목록을 사용 하 여 중첩 된 순서가 지정 되지 않은](creating-user-accounts-cs/_static/image11.png)](creating-user-accounts-cs/_static/image10.png)

**그림 4**: 탐색의 사용자 인터페이스는 렌더링 목록을 사용 하 여 중첩 된 순서가 지정 되지 않은 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-cs/_static/image12.png))


### <a name="adding-breadcrumb-navigation"></a>이동 경로 탐색 추가

왼쪽된 열에 대 한 링크 목록 외에 죠 각 페이지 표시는 [이동 경로 탐색](http://en.wikipedia.org/wiki/Breadcrumb_%28navigation%29)합니다. 이동 경로 신속 하 게 사용자에 게 사이트 계층 구조 내에 있는 현재 위치를 표시 하는 탐색 사용자 인터페이스 요소입니다. SiteMapPath 컨트롤 사이트 맵 프레임 워크를 사용 하 여 사이트 맵에서 현재 페이지의 위치를 결정 하 고이 정보에 따라 이동 경로 표시 합니다.

특히, 추가할는 `<span>` 마스터 페이지의 헤더에 요소 `<div>` 요소를 새 설정 `<span>` 요소의 `class` 특성을 "이동" 합니다. (의 `Styles.css` 클래스 "이동" 클래스에 대 한 규칙을 포함 합니다.) 다음에 추가 된 SiteMapPath 새 `<span>` 요소입니다.

[!code-aspx[Main](creating-user-accounts-cs/samples/sample4.aspx)]

그림 5를 방문할 때는 SiteMapPath 출력이 나와 `~/Membership/CreatingUserAccounts.aspx`합니다.


[![현재 페이지를 표시 된 이동 경로 및 해당 상위 사이트에 있는 지도](creating-user-accounts-cs/_static/image14.png)](creating-user-accounts-cs/_static/image13.png)

**그림 5**: 된 이동 경로 사이트 맵 현재 페이지와 해당 상위 항목 표시 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-cs/_static/image15.png))


## <a name="step-4-removing-the-custom-principal-and-identity-logic"></a>4 단계: 사용자 지정 보안 주체 및 Id 논리를 제거합니다.

에 *<a id="_msoanchor_7"> </a> [폼 인증 구성 및 고급 항목](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md)* 자습서 인증된 된 사용자에 사용자 지정 보안 주체 및 identity 개체를 연결 하는 방법에 살펴보았습니다. 이벤트 처리기를 만들어이 작업을 수행 했습니다 `Global.asax` 응용 프로그램에 대 한 `PostAuthenticateRequest` 후 발생 하는 이벤트는 `FormsAuthenticationModule` 사용자를 인증 합니다. 이 이벤트 처리기에서 교체는 `GenericPrincipal` 및 `FormsIdentity` 하 여 추가 된 개체는 `FormsAuthenticationModule` 와 `CustomPrincipal` 및 `CustomIdentity` 해당 자습서에서 만든 개체입니다.

사용자 지정 보안 주체 및 identity 개체는 대부분의 경우에서 특정 시나리오에서 유용는 `GenericPrincipal` 및 `FormsIdentity` 개체는 충분 합니다. 따라서 기본 동작으로 되돌립니다 많은 도움이 될 것 생각 됩니다. 이 변경 내용을 제거 하거나 주석으로 처리 여는 `PostAuthenticateRequest` 이벤트 처리기 또는 삭제 하 여는 `Global.asax` 완전히 합니다.

## <a name="step-5-programmatically-creating-a-new-user"></a>5 단계: 새 사용자를 프로그래밍 방식으로 만들기

멤버 자격 프레임 워크 사용을 통해 새 사용자 계정을 만들려면는 `Membership` 클래스의 [ `CreateUser` 메서드](https://msdn.microsoft.com/library/system.web.security.membership.createuser.aspx)합니다. 이 메서드는 사용자 이름, 암호 및 기타 사용자 관련 필드에 대 한 매개 변수 입력 있습니다. 호출에서 새 사용자 계정 만드는 구성 된 멤버 자격 공급자에 위임 하 고 다음 반환는 [ `MembershipUser` 개체](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx) 방금 만든 사용자 계정을 표시 합니다.

`CreateUser` 메서드에 4 개의 오버 로드가 각각 다른 개수의 입력된 매개 변수를 수락 합니다.

- [`CreateUser(username, password)`](https://msdn.microsoft.com/library/d8t4h2es.aspx)
- [`CreateUser(username, password, email)`](https://msdn.microsoft.com/library/t8yy6w3h.aspx)
- [`CreateUser(username, password, email, passwordQuestion, passwordAnswer, isApproved, MembershipCreateStatus)`](https://msdn.microsoft.com/library/82xx2e62.aspx)
- [`CreateUser(username, password, email, passwordQuestion, passwordAnswer, isApproved, providerUserKey, MembershipCreateStatus)`](https://msdn.microsoft.com/library/ms152012.aspx)

이러한 4 개의 오버 로드에 수집 되는 정보의 양을 마다 다릅니다. 첫 번째 오버 로드 예를 들어이 필요 사용자 이름 및 암호는 새 사용자 계정에 대 한 하지만 두 번째 식에도 사용자의 전자 메일 주소가 필요 합니다.

이러한 오버 로드에는 새 사용자 계정을 만드는 데 필요한 정보 멤버 자격 공급자의 구성 설정에 따라 다르기 때문에 존재 합니다. 에 *<a id="_msoanchor_8"> </a> [SQL Server에서 멤버 자격 스키마 만들기](creating-the-membership-schema-in-sql-server-cs.md)* 자습서의 멤버 자격 공급자 구성 설정 지정을 검사 했습니다 `Web.config`합니다. 표 2는 구성 설정의 전체 목록을 포함 합니다.

설정 하는 이러한 한 멤버 자격 공급자 구성에 어떤 영향을 줍니다 `CreateUser` 오버 로드를 사용할 수 있습니다.이 `requiresQuestionAndAnswer` 설정 합니다. 경우 `requiresQuestionAndAnswer` 로 설정 된 `true` (기본값), 새 사용자 계정을 만들 때 보안 질문 및 대답 지정 해야 합니다. 이 정보는 해당 암호를 다시 설정 하거나 변경 해야 하는 경우 나중에 사용 됩니다. 특히, 당시에는 표시 된 보안 질문을 재설정 하거나 암호를 변경 하기 위해 올바른 답을 입력 해야 합니다. 따라서 경우는 `requiresQuestionAndAnswer` 로 설정 된 `true` 처음 두 가지 중 하나를 호출 하는 다음 `CreateUser` 보안 질문 및 대답 누락 되어 예외가 발생 하는 오버 로드 합니다. 응용 프로그램은 현재 보안 질문과 대답을 요구 하도록 구성 된 사용자의 프로그래밍 방식으로 만들 때 두 번째 오버 로드 중 하나를 사용 해야 합니다.

사용 하 여 설명 하기 위해는 `CreateUser` 메서드를 사용자에 게 이름, 암호, 전자 메일 및 미리 정의 된 보안 질문에 대 한 답변을 확인 했습니다 사용자 인터페이스를 만들어 보겠습니다. 열기는 `CreatingUserAccounts.aspx` 페이지에 `Membership` 폴더 콘텐츠 컨트롤을 다음 웹 컨트롤을 추가:

- 명명 된 TextBox `Username`
- 명명 된 TextBox `Password`, 해당 `TextMode` 속성 `Password`
- 명명 된 TextBox `Email`
- 이라는 레이블이 `SecurityQuestion` 와 해당 `Text` 속성 삭제
- 명명 된 TextBox `SecurityAnswer`
- 이라는 단추 `CreateAccountButton` 텍스트 속성이 "사용자 계정 만들기"에 설정 된
- 명명 된 Label 컨트롤 `CreateAccountResults` 와 해당 `Text` 속성 삭제

이 시점에서 사용자의 화면 스크린샷과 그림 6에 표시 된 비슷해야 합니다.


[![다양 한 웹 컨트롤 CreatingUserAccounts.aspx 페이지에 추가](creating-user-accounts-cs/_static/image17.png)](creating-user-accounts-cs/_static/image16.png)

**그림 6**: 다양 한 웹 컨트롤을 추가 `CreatingUserAccounts.aspx` 페이지 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-cs/_static/image18.png))


`SecurityQuestion` 레이블 및 `SecurityAnswer` TextBox 미리 정의 된 보안 질문을 표시 하 고 사용자의 답변을 수집 하도록 되어 있습니다. 참고가 보안 질문과 대답이 저장 되도록 사용자가 사용자 단위로 되므로 각 사용자가 자신의 보안 질문을 정의할 수 있습니다. 그러나 즉 유니버설 보안 질문을 사용 하기로이 예제에 대 한: "원하는 색 란?"

이 미리 정의 된 보안 질문을 구현 하려면 상수 이라는 페이지의 코드 숨김 클래스에 추가 `passwordQuestion`, 보안 질문을 할당 합니다. 그런 다음는 `Page_Load` 이벤트 처리기, 할당에이 상수는 `SecurityQuestion` 레이블의 `Text` 속성:

[!code-csharp[Main](creating-user-accounts-cs/samples/sample5.cs)]

에 대 한 이벤트 처리기를 다음으로 만듭니다는 `CreateAccountButton`의 `Click` 이벤트를 다음 코드를 추가 합니다.

[!code-csharp[Main](creating-user-accounts-cs/samples/sample6.cs)]

`Click` 이벤트 처리기 라는 변수를 정의 하 여 시작 `createStatus` 형식의 [ `MembershipCreateStatus` ](https://msdn.microsoft.com/library/system.web.security.membershipcreatestatus.aspx)합니다. `MembershipCreateStatus` 상태를 표시 하는 열거형은 `CreateUser` 작업 합니다. 예를 들어, 결과로 생성 된 사용자 계정이 성공적으로 생성 하는 경우 `MembershipCreateStatus` 인스턴스 값으로 설정 됩니다 `Success`다른; 반면, 동일한 사용자 이름 가진 사용자 이미 있으므로 작업이 실패 하는 경우의 값으로 설정할 수는 `DuplicateUserName`. 에 `CreateUser` 를 전달 해야 오버 로드를 사용 하 여는 `MembershipCreateStatus` 로 메서드에 인스턴스는 `out` 매개 변수입니다. 이 매개 변수 내에서 적절 한 값으로 설정 되는 `CreateUser` 메서드와에서는 메서드 호출에 사용자 계정을 성공적으로 만들어졌는지 여부를 확인 한 후 해당 값을 검사할 수 있습니다.

호출한 후 `CreateUser`을 전달 `createStatus`, `switch` 문을 사용 하는 적절 한 메시지에 할당 된 값에 따라 출력를 `createStatus`합니다. 그림 7에서는 새 사용자를 성공적으로 생성 되 면 출력을 보여 줍니다. 그림 8과 9에는 사용자 계정이 만들어지지 않은 경우 출력을 보여 줍니다. 그림 8 방문자 멤버 자격 공급자 구성 설정에 암호 강도 요구 사항을 충족 하지 않는 5 못 암호를 입력 합니다. 그림 9, 방문자를 기존 사용자 이름 (그림 7에서 만들어진 것) 있는 사용자 계정을 생성할 하려고 합니다.


[![새 사용자 계정을 성공적으로 생성 됩니다.](creating-user-accounts-cs/_static/image20.png)](creating-user-accounts-cs/_static/image19.png)

**그림 7**: A 새 사용자 계정을 성공적으로 생성 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-cs/_static/image21.png))


[![제공 된 암호가 너무 약 합니다. 사용자 계정 생성 되지 않습니다.](creating-user-accounts-cs/_static/image23.png)](creating-user-accounts-cs/_static/image22.png)

**그림 8**: 제공 된 암호가 너무 약 The 사용자 계정이 생성 되지 않습니다 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-cs/_static/image24.png))


[![만든 때문이 아니라 사용자 이름은 이미 사용 중인 사용자 계정](creating-user-accounts-cs/_static/image26.png)](creating-user-accounts-cs/_static/image25.png)

**그림 9**: The 사용자 계정은 만든 때문이 아니라 사용자 이름을 이미 사용 중인 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-cs/_static/image27.png))


> [!NOTE]
> 처음 두 가지 중 하나를 사용 하는 경우 성공 또는 실패를 확인 하는 방법을 할까요 `CreateUser` 메서드 오버 로드를 둘 다의 형식 매개 변수가 있는 `MembershipCreateStatus`합니다. 이러한 처음 두 개의 오버 로드를 throw 한 [ `MembershipCreateUserException` 예외](https://msdn.microsoft.com/library/system.web.security.membershipcreateuserexception.aspx) 포함 하는 오류는 [ `StatusCode` 속성](https://msdn.microsoft.com/library/system.web.security.membershipcreateuserexception.statuscode.aspx) 형식의 `MembershipCreateStatus`합니다.


사용자 계정 몇 개를 만든 후의 내용을 나열 하 여 계정을 만들어졌는지 확인는 `aspnet_Users` 및 `aspnet_Membership` 테이블에 `SecurityTutorials.mdf` 데이터베이스입니다. 그림 10과 같이 두 명의 사용자가 통해 추가 했 고 `CreatingUserAccounts.aspx` 페이지: Tito 및 1 세 합니다.


[![멤버 자격 사용자 저장소에 두 사용자가 있는: Tito 및 1 세](creating-user-accounts-cs/_static/image29.png)](creating-user-accounts-cs/_static/image28.png)

**그림 10**: 멤버 자격 사용자 저장소에 두 사용자가 있는: Tito 및 1 세 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-cs/_static/image30.png))


멤버 자격 사용자 저장소에서 이제 1 세 및 Tito의 계정 정보를 포함 하는 동안 아직 1 세 또는 Tito 사이트에 로그온 할 수 있는 기능을 구현 합니다. 현재 `Login.aspx` 사용자의 자격 증명의 유효성을 검사는 사용자 이름/암호 쌍 – 하드 코드 된 집합에 대해 *하지* 구성원 프레임 워크에 대해 제공된 된 자격 증명의 유효성을 검사 합니다. 이제 새 사용자 계정에 확인 하는 데는 `aspnet_Users` 및 `aspnet_Membership` 테이블 충분 해야 합니다. 다음 자습서에서는  *<a id="_msoanchor_9"> </a> [유효성 검사 사용자 자격 증명에 대해의 멤버 자격 사용자 저장할](validating-user-credentials-against-the-membership-user-store-cs.md)*, 구성원 저장소에 대 한 유효성을 검사 하는 로그인 페이지 업데이트 됩니다.

> [!NOTE]
> 모든 사용자가 표시 되지 않으면 프로그램 `SecurityTutorials.mdf` 웹 응용 프로그램은 기본 멤버 자격 공급자를 사용 하 여 때문일 수 있습니다 데이터베이스 `AspNetSqlMembershipProvider`, 사용 하는 `ASPNETDB.mdf` 사용자 저장소로 데이터베이스입니다. 이것이 문제 인지를 확인 하려면 솔루션 탐색기에서 새로 고침 단추를 클릭 합니다. 라는 데이터베이스가 `ASPNETDB.mdf` 에 추가 되었습니다는 `App_Data` 폴더를 이것이 문제가 있습니다. 4 단계로 돌아가서는 *<a id="_msoanchor_10"> </a> [SQL Server에서 멤버 자격 스키마 만들기](creating-the-membership-schema-in-sql-server-cs.md)* 올바르게 멤버 자격 공급자를 구성 하는 방법에 대 한 자습서입니다.


대부분의 시나리오를 만들 사용자 계정, 방문자에 게 자신의 사용자 이름, 암호, 전자 메일, 이때 새 계정을 만든, 기타 중요 한 정보 입력에 대 한 몇 가지 인터페이스 제공 됩니다. 이 단계에서는 이러한 인터페이스를 직접 작성에 검토 하 고 다음 사용 하는 방법을 보여 준다는 사실을 알았습니다는 `Membership.CreateUser` 사용자의 입력을 기반으로 하는 메서드를 프로그래밍 방식으로 새 사용자 계정을 추가 합니다. 그러나 코드, 방금 만든 새 사용자 계정입니다. 모든 후속 방금 만든 사용자 계정에서 사이트에 사용자를 로그인 또는 사용자에 게 확인 전자 메일을 보내는 등의 작업은 수행 하지 못했습니다. 이러한 단계를 더 단추의 추가 코드가 필요 `Click` 이벤트 처리기입니다.

ASP.NET은 CreateUserWizard 컨트롤을 렌더링 하는 계정을 멤버 자격 프레임 워크를 만들고 수행 후 계정에 새 사용자 계정을 만들기 위한 사용자 인터페이스에서 사용자 계정 생성 프로세스를 처리 하도록 설계 된 제공 만들기 등의 작업을 확인 전자 메일을 보내고 방금 만든 사용자 사이트에 로그인 합니다. CreateUserWizard 컨트롤을 사용 하는 것은 CreateUserWizard 컨트롤 페이지 도구 상자에서 끌어서 다음 몇 가지 속성을 설정 하기만입니다. 대부분의 경우에 한 줄의 코드를 작성할 필요가 없습니다. 이 유용한 컨트롤 6 단계에서에서 자세히 설명 합니다.

일반적인 계정을 만드는 웹 페이지를 통해 새 사용자 계정을 만드는, 되지 않았으면 해야 할 수는 현재까지 사용 하는 코드를 작성 하는 `CreateUser` 메서드를 CreateUserWizard 컨트롤은 가능성이 요구를 충족 합니다. 그러나는 `CreateUser` 방법은 시나리오에서 유용 하 게 고도로 사용자 지정 된 계정 정보 만들기 사용자 경험을 해야 하거나 프로그래밍 방식으로 다른 인터페이스를 통해 새 사용자 계정 만들기를 중지 해야 합니다. 예를 들어 사용자가 다른 응용 프로그램에서 사용자 정보를 포함 하는 XML 파일을 업로드 하도록 허용 하는 페이지를 할 수 있습니다. 페이지 구문 분석 하 여 업로드 된 XML의 콘텐츠 파일을 호출 하 여 XML에 표시 되는 각 사용자에 대 한 새 계정을 만들 수는 `CreateUser` 메서드.

## <a name="step-6-creating-a-new-user-with-the-createuserwizard-control"></a>6 단계: CreateUserWizard 컨트롤에서 새 사용자 만들기

ASP.NET는 여러 로그인 웹 컨트롤이 함께 제공 됩니다. 이러한 컨트롤 여러 일반적인 사용자 계정 및 로그인 관련 시나리오 용이해 집니다. [CreateUserWizard 컨트롤](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/createuserwizard.aspx) 새 사용자 계정을 멤버 자격 프레임 워크를 추가 하기 위한 사용자 인터페이스를 제공 하도록 설계 된 해당 한 컨트롤이 있습니다.

마찬가지로 여러 다른 로그인 관련 웹 컨트롤은 CreateUserWizard 코드 한 줄도 작성 하지 않고 사용할 수 있습니다. 멤버 자격 공급자의 구성 설정과 내부적으로 호출에 따라 사용자 인터페이스를 제공 직관적으로 `Membership` 클래스의 `CreateUser` 메서드 후 사용자가 필요한 정보를 입력 하 고 "사용자 만들기" 단추를 클릭 합니다. CreateUserWizard 컨트롤은 매우 사용자 지정할 수 있습니다. 계정 생성 프로세스의 다양 한 단계를 실행 하는 이벤트의 호스트 있습니다. 계정 만들기 워크플로 사용자 지정 논리를 삽입 하려면 필요에 따라 이벤트 처리기를 만들 수 있습니다. 또한 CreateUserWizard의 모양을 매우 유연 합니다. 기본 인터페이스의 모양을 정의 하는 속성의 여러 가지 필요한 경우 컨트롤 템플릿으로 변환 될 수 또는 추가 사용자 등록 "단계"에 추가 될 수 있습니다.

CreateUserWizard 컨트롤의 기본 인터페이스 및 동작을 사용 하 여 보는 것으로 시작 하겠습니다. 컨트롤의 속성 및 이벤트를 통해 모양을 사용자 지정 하는 방법을 다음 살펴보겠습니다.

### <a name="examining-the-createuserwizards-default-interface-and-behavior"></a>CreateUserWizard의 기본 인터페이스 및 동작 검사

으로 돌아와서는 `CreatingUserAccounts.aspx` 페이지에 `Membership` 폴더를 디자인 또는 분할 모드를 전환 하 고 다음 페이지의 맨 위에 CreateUserWizard 컨트롤을 추가 합니다. CreateUserWizard 컨트롤 도구 상자의 로그인 제어 섹션 아래에 정렬 됩니다. 설정 된 컨트롤을 추가한 후 해당 `ID` 속성을 `RegisterUser`합니다. 스크린샷에에서 그림 11 보여 대로 CreateUserWizard 새 사용자의 사용자 이름, 암호, 전자 메일 주소 및 보안 질문 및 답변에 대 한 텍스트 상자를 사용 하 여 인터페이스를 렌더링 합니다.


[![CreateUserWizard 컨트롤 렌더링 되는 일반 사용자 인터페이스 만들기](creating-user-accounts-cs/_static/image32.png)](creating-user-accounts-cs/_static/image31.png)

**그림 11**: CreateUserWizard 컨트롤 렌더링을 일반 사용자 인터페이스 만들기 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-cs/_static/image33.png))


5 단계에서에서 만든 인터페이스와 CreateUserWizard 컨트롤에 의해 생성 된 기본 사용자 인터페이스를 비교 하려면 간단히 살펴보겠습니다. 먼저 수동으로 만든 인터페이스를 사용 하는 미리 정의 된 보안 질문을 사용 하는 반면 CreateUserWizard 컨트롤 방문자가 보안 질문 및 대답을 모두 지정할 수 있습니다. CreateUserWizard 컨트롤의 인터페이스 했습니다. 아직이 인터페이스의 폼 필드에 유효성 검사를 구현 하는 반면 유효성 검사 컨트롤도 포함 됩니다. 와 CreateUserWizard 컨트롤 인터페이스 (텍스트 입력 "Password" 및 "암호 비교" 입력란 같은지 되도록 CompareValidator) 함께 "암호 확인" textbox를 포함 합니다.

흥미로운은 CreateUserWizard 컨트롤의 사용자 인터페이스를 렌더링 하는 경우 멤버 자격 공급자 구성 설정 참조는입니다. 예를 들어 보안 질문 및 대답 텍스트 상자는 경우에 표시 `requiresQuestionAndAnswer` 가 True로 설정 합니다. 마찬가지로, CreateUserWizard 암호 강도 요구 사항을 충족 되 고 설정 되도록 RegularExpressionValidator 컨트롤을 자동으로 추가 해당 `ErrorMessage` 및 `ValidationExpression` 속성에 따라는 `minRequiredPasswordLength`, `minRequiredNonalphanumericCharacters`, 및 `passwordStrengthRegularExpression` 구성 설정입니다.

파생 이름에서 알 수 있듯이 CreateUserWizard 컨트롤은 [Wizard 컨트롤](https://msdn.microsoft.com/library/s2etd1ek.aspx)합니다. 마법사 컨트롤 다중 단계 작업을 완료 하기 위한 인터페이스를 제공 하도록 설계 되었습니다. Wizard 컨트롤 임의 개수의 있을 수 `WizardSteps`, 각각는 HTML을 정의 하는 서식 파일 및 웹 컨트롤에 대 한 해당 단계입니다. 마법사 컨트롤은 처음에 첫 번째 표시 `WizardStep`, 사용자 한 단계에서 다음 단계로 계속 진행 하거나 이전 단계로 돌아가려면 것을 허용 하는 탐색 컨트롤과 함께 합니다.

그림 11에 선언적 태그에서 볼 수 있듯이 CreateUserWizard 컨트롤의 기본 인터페이스 두 개 포함 `WizardSteps:`

- [`CreateUserWizardStep`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizardstep.aspx) -새 사용자 계정 만들기에 대 한 정보를 수집 하는 인터페이스를 렌더링 합니다. 그림 11 단계입니다.
- [`CompleteWizardStep`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.completewizardstep.aspx) – 계정을 성공적으로 만들어졌음을 나타내는 메시지를 렌더링 합니다.

CreateUserWizard의 모양 및 동작을 수정할 수 템플릿,으로 다음이 단계 중 하나를 변환 하 여 직접 추가 하 여 `WizardSteps`합니다. 추가 대해서는 `WizardStep` 에서 등록 인터페이스는 *추가 사용자 정보를 저장* 자습서입니다.

CreateUserWizard 컨트롤을 작동을 살펴보겠습니다. 방문 된 `CreatingUserAccounts.aspx` 브라우저를 통해 페이지입니다. CreateUserWizard의 인터페이스에 일부 잘못 된 값을 입력 하 여 시작 합니다. 암호 강도 요구 사항을 또는 빈 종료는 "사용자 이름" textbox에 맞지 않는 암호를 입력 하십시오. CreateUserWizard 적절 한 오류 메시지가 표시 됩니다. 그림 12 충분 강력한 암호로 사용자를 만들려고 할 때의 출력을 표시 합니다.


[![CreateUserWizard 컨트롤을 유효성 검사를 자동으로 삽입합니다.](creating-user-accounts-cs/_static/image35.png)](creating-user-accounts-cs/_static/image34.png)

**그림 12**:은 CreateUserWizard 자동으로 삽입 합니다. 유효성 검사 컨트롤 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-cs/_static/image36.png))


다음은 CreateUserWizard에 적절 한 값을 입력 하 고 "사용자 만들기" 단추를 클릭 합니다. 필수 필드를 입력 하 고 암호의 강도가 충분 한 경우는 CreateUserWizard 구성원 프레임 워크를 통해 새 사용자 계정을 만들고 다음 표시는 `CompleteWizardStep`의 인터페이스 (그림 13 참조). CreateUserWizard 내부적으로 호출 된 `Membership.CreateUser` 메서드, 5 단계에서에서 했던 것 처럼 합니다.


[![새 사용자 계정에 성공적으로 만들어진](creating-user-accounts-cs/_static/image38.png)](creating-user-accounts-cs/_static/image37.png)

**그림 13**: 새 사용자 계정에 성공적으로 만들어진 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-cs/_static/image39.png))


> [!NOTE]
> 그림 13에서 볼 수 있듯이 `CompleteWizardStep`의 인터페이스는 계속 단추를 포함 합니다. 그러나이 시점에서 바로 클릭 방문자 동일한 페이지에 유지, 포스트백을 수행 합니다. "CreateUserWizard의 모양 및 해당 속성을 통해 동작을 사용자 지정" 섹션에서 방식 방문자에 보낼이 단추를 사용할 수 있습니다 살펴보겠습니다 `Default.aspx` (또는 다른 페이지).


새 사용자 계정을 만든 후 Visual Studio로 되돌아가려면 및 검사는 `aspnet_Users` 및 `aspnet_Membership` 계정을 성공적으로 만들어졌는지 확인 하려면 그림 10에서 수행한 것 처럼 테이블입니다.

### <a name="customizing-the-createuserwizards-behavior-and-appearance-through-its-properties"></a>CreateUserWizard의 동작과 모양은 해당 속성을 통해 사용자 지정

CreateUserWizard 다양 한 방식으로 속성을 통해 사용자 지정할 수 있습니다 `WizardSteps`, 및 이벤트 처리기입니다. 이 섹션에서는 살펴보겠습니다 속성; 컨트롤의 모양을 사용자 지정 하는 방법 다음 섹션에서 이벤트 처리기를 통해 컨트롤의 동작을 확장 살펴봅니다.

거의 모든 CreateUserWizard 컨트롤의 기본 사용자 인터페이스에 표시 되는 텍스트는 다양 한 속성을 통해 사용자 지정할 수 있습니다. 예를 들어 입력란의 왼쪽에 표시 되는 "User Name", "Password", "암호 확인", "전자 메일", "보안 질문" 및 "보안 대답" 레이블을 사용자 지정할 수 있습니다는 [ `UserNameLabelText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.usernamelabeltext.aspx), [ `PasswordLabelText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.passwordlabeltext.aspx), [ `ConfirmPasswordLabelText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.confirmpasswordlabeltext.aspx), [ `EmailLabelText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.emaillabeltext.aspx), [ `QuestionLabelText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.questionlabeltext.aspx), 및 [ `AnswerLabelText` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.answerlabeltext.aspx)속성을 각각. 마찬가지로, 텍스트에서 "Create User" 및 "Continue" 단추를 지정 하는 것에 대 한 속성은는 `CreateUserWizardStep` 및 `CompleteWizardStep`도 처럼는 경우 이러한 단추는 단추, 링크, 단추가 또는 ImageButtons로 렌더링 됩니다.

색, 테두리, 글꼴 및 기타 시각적 요소는 스타일 속성의 호스트를 통해 구성할 수 있습니다. 자체 CreateUserWizard 컨트롤에 공용 웹 컨트롤 스타일 속성 – `BackColor`, `BorderStyle`, `CssClass`, `Font`등과 – 아니며의 특정 섹션에 대 한 모양을 정의 하기 위한 스타일 속성 수는 CreateUserWizard의 인터페이스입니다. [ `TextBoxStyle` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.textboxstyle.aspx), 예를 들어,에 텍스트 상자에 대 한 스타일을 정의 `CreateUserWizardStep`, 동안는 [ `TitleTextStyle` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.titletextstyle.aspx) ("로그인을 새 사용자에 대 한 title에 대 한 스타일을 정의 합니다. 계정 ")입니다.

모양 관련 속성 외에도 다양 한 CreateUserWizard 컨트롤의 동작에 영향을 주는 속성이 있습니다. [ `DisplayCancelButton` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.wizard.displaycancelbutton.aspx)경우 (기본값은 False) "사용자 만들기" 단추 옆에 있는 취소 단추를 표시 합니다. True로 설정 합니다. 취소 단추를 표시 하는 경우도 설정 해야는 [ `CancelDestinationPageUrl` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx), 취소 클릭 한 후 사용자가 보낸 페이지를 지정 하는 합니다. 계속 단추, 위의 섹션에서 설명한 것 처럼는 `CompleteWizardStep`의 인터페이스는 포스트백이 발생 하지만 방문자 동일한 페이지에 남겨 둡니다. 다른 페이지로 방문자 단추를 클릭 한 후을 보내려면에 URL을 지정 하기만 하면는 [ `ContinueDestinationPageUrl` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)합니다.

정보를 업데이트는 `RegisterUser` CreateUserWizard 컨트롤 취소 단추를 표시 하 고 방문자에 보낼 `Default.aspx` 계속 또는 취소 단추를 클릭 하는 경우. 이를 위해 설정 된 `DisplayCancelButton` 속성을 true로 지정 하 고 둘 다는 `CancelDestinationPageUrl` 및 `ContinueDestinationPageUrl` 속성을 "~ / Default.aspx"입니다. 그림 14 브라우저를 통해 볼 때 업데이트 된 CreateUserWizard 보여 줍니다.


[![CreateUserWizardStep에 "취소" 단추가 포함 됩니다.](creating-user-accounts-cs/_static/image41.png)](creating-user-accounts-cs/_static/image40.png)

**그림 14**:는 `CreateUserWizardStep` 취소 단추가 포함 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-cs/_static/image42.png))


방문자가 사용자 이름, 암호, 전자 메일 주소 및 보안 질문 및 답변을 입력 하 고 "사용자 만들기"를 클릭 하는 경우 새 사용자 계정을 만들고 방문자가 새로 생성된 된 해당 사용자로 로그인 합니다. 페이지를 방문 하는 사용자가 자신에 대 한 새 계정을 만들고, 있다고 가정할 경우이 올바른된 동작이 가능성이 높습니다. 그러나 다음 관리자가 새 사용자 계정을 추가 하도록 허용 하는 것이 좋습니다. 이 과정에서 사용자 계정 생성 되기, 관리자는 상태를 유지 하면서 로그인 관리자 권한으로 (새로 만든된 계정이 아니라). 부울 통해이 문제를 수정할 수 있으므로 [ `LoginCreatedUser` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.logincreateduser.aspx)합니다.

구성원 프레임 워크에서 사용자 계정에는 승인 된 플래그; 포함 승인 되지 않은 사용자가 사이트에 로그인 할 수 없습니다. 기본적으로 새로 만든된 계정에는 사용자가 즉시 사이트에 로그인 할 수 있도록 승인 된 것으로 표시 됩니다. 그러나 승인 되지 않은 것으로 표시 하는 새 사용자 계정을 사용 하는 것이 가능 합니다. 에 로그온 하려면 전에 새 사용자를 수동으로 승인 하려면 관리자로 수도 있습니다. 또는 사용자가 로그온을 허용 하기 전에 등록 시 입력 한 전자 메일 주소가 올바른지 확인 하려고 할 수도 있습니다. 관계 없이 대/소문자 수 있습니다, CreateUserWizard 컨트롤을 설정 하 여 승인 되지 않은 것으로 표시 된 새로 만든된 사용자 계정만 가질 수 [ `DisableCreatedUser` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.disablecreateduser.aspx) 를 True (기본값은 False)입니다.

다른 동작 관련 속성 중 하나가 포함 `AutoGeneratePassword` 및 `MailDefinition`합니다. 경우는 [ `AutoGeneratePassword` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.autogeneratepassword.aspx) True로 설정 된 `CreateUserWizardStep` "Password" 및 "암호 확인" 입력란; 표시 하지 않습니다 대신, 새로 만든 사용자의 암호는 자동으로 사용 하 여 생성는 `Membership` 클래스의 [ `GeneratePassword` 메서드](https://msdn.microsoft.com/library/system.web.security.membership.generatepassword.aspx)합니다. `GeneratePassword` 메서드와 영숫자가 아닌 문자 구성 된 암호 강도 요구 사항을 충족 하기 위해 충분 한 수를 지정 된 길이의 암호를 생성 합니다.

[ `MailDefinition` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.maildefinition.aspx) 계정 생성 프로세스 중에 지정 된 전자 메일 주소로 전자 메일을 보내려는 경우에 유용 합니다. `MailDefinition` 속성 일련의 생성 된 전자 메일 메시지에 대 한 정보를 정의 하기 위한 하위 속성을 포함 합니다. 이러한 하위 속성와 같은 옵션이 포함 `Subject`, `Priority`, `IsBodyHtml`, `From`, `CC`, 및 `BodyFileName`합니다. [ `BodyFileName` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.bodyfilename.aspx) 텍스트 또는 전자 메일 메시지의 본문을 포함 하는 HTML 파일을 가리킵니다. 본문에는 두 명의 미리 정의 된 자리 표시자 지원: `<%UserName%>` 및 `<%Password%>`합니다. 이러한 자리 표시자에 있는 경우에 `BodyFileName` 파일, 방금 만든 사용자의 이름 및 암호로 대체 됩니다.

> [!NOTE]
> `CreateUserWizard` 컨트롤의 `MailDefinition` 속성 방금 새 계정이 만들어질 때 전송 되는 전자 메일 메시지에 대 한 세부 정보를 지정 합니다. 전자 메일 메시지를 보낸 실제로 방법에 대 한 세부 정보는 포함 되지 않습니다 (즉, SMTP 서버 또는 메일 드롭 디렉터리 사용 여부, 모든 인증 정보 및 등). 이러한 하위 수준 세부 정보에서 정의 해야 합니다.는 `<system.net>` 섹션 `Web.config`합니다. 이러한 구성 설정 및 일반적 ASP.NET 2.0에서 전자 메일을 보내는 방법에 자세한 내용은 참조는 [SystemNetMail.com에서 Faq](http://www.systemnetmail.com/) 와 내 문서 [ASP.NET 2.0에서 전자 메일 보내기](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)합니다.


### <a name="extending-the-createuserwizards-behavior-using-event-handlers"></a>이벤트 처리기를 사용 하 여 CreateUserWizard의 동작을 확장 합니다.

CreateUserWizard 컨트롤의 워크플로 중 다양을 한 이벤트를 발생 시킵니다. 예를 들어 방문자가 자신의 사용자 이름, 암호 및 기타 관련 정보를 입력 하 고 "사용자 만들기" 단추를 클릭 한 후 CreateUserWizard 컨트롤 발생 해당 [ `CreatingUser` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.creatinguser.aspx)합니다. 하지만 만들기 프로세스 중에 문제가 있으면는 [ `CreateUserError` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createusererror.aspx) ; 발생 사용자가 정상적으로 작성 하는 경우, 하면 [ `CreatedUser` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx) 발생 합니다. 추가 CreateUserWizard 컨트롤 이벤트를 발생 있지만 세 가지 가장 콘텐츠와.

특정 시나리오에서 우리는 해당 이벤트에 대 한 이벤트 처리기를 만들어 실행할 수 있는 CreateUserWizard 워크플로 활용할 수 있습니다 바랍니다. 이 설명 하기 향상 되어 이제는 `RegisterUser` CreateUserWizard 컨트롤 사용자 이름과 암호의 일부 사용자 지정 유효성 검사를 포함 합니다. 특히, 보겠습니다 우리의 CreateUserWizard 하도록 개선 사용자 이름에 선행 또는 후행 공백을 포함할 수 없습니다 및 사용자 이름 암호의 아무 곳 이나 나타날 수 없습니다. 즉, 다른 사용자가 만드는 "Scott" 같은 사용자 이름을 "Scott" 및 "Scott.1234"와 같은 사용자 이름/암호 조합 또는 방지 하려고 합니다.

에 대 한 이벤트 처리기를 만들겠습니다이를 위해는 `CreatingUser` 우리의 추가 유효성 검사를 수행 하는 이벤트입니다. 제공 된 데이터가 유효 하지 않을 경우 생성 프로세스를 취소 해야 합니다. 또한 사용자 이름 또는 암호가 올바르지 않음을 설명 하는 메시지를 표시 하려면 페이지에 레이블 웹 컨트롤을 추가 해야 합니다. 시작 설정 CreateUserWizard 컨트롤 아래에 레이블 컨트롤을 추가 하 여 해당 `ID` 속성을 `InvalidUserNameOrPasswordMessage` 및 해당 `ForeColor` 속성을 `Red`합니다. 삭제는 `Text` 속성 집합과 해당 `EnableViewState` 및 `Visible` 속성을 false로 합니다.

[!code-aspx[Main](creating-user-accounts-cs/samples/sample7.aspx)]

다음으로 CreateUserWizard 컨트롤에 대 한 이벤트 처리기를 만들고 `CreatingUser` 이벤트입니다. 이벤트 처리기를 만들려면 디자이너에서 컨트롤을 선택 하 고 속성 창으로 이동 하십시오. 여기에서 번개 모양 아이콘 클릭 한 다음 이벤트 처리기를 만들 적합 한 이벤트를 두 번 클릭 합니다.

다음 코드를 `CreatingUser` 이벤트 처리기에 추가합니다.

[!code-csharp[Main](creating-user-accounts-cs/samples/sample8.cs)]

사용자 이름 및 CreateUserWizard 컨트롤에 입력 한 암호를 통해 사용할 수는 해당 [ `UserName` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.username.aspx) 및 [ `Password` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.password.aspx)각각. 제공된 된 사용자의 선행 또는 후행 공백을 포함 되는지 여부 및 암호에 사용자 이름이 있는 여부를 확인 하려면 위의 이벤트 처리기에서 이러한 속성을 사용 했습니다. 에 오류 메시지가 표시 됩니다 이러한 조건 중 하나라도 충족 되 면는 `InvalidUserNameOrPasswordMessage` 레이블 및 이벤트 처리기의 `e.Cancel` 속성이 `true`합니다. 경우 `e.Cancel` 로 설정 된 `true`은 CreateUserWizard short-circuits 해당 워크플로 효과적으로 사용자 계정 생성 프로세스를 취소 합니다.

그림 15 표시의 스크린 샷을 `CreatingUserAccounts.aspx` 사용자가 선행 공백이 사용자 이름입니다.


[![사용자 이름은 선행 또는 후행 공백이 허용 되지 않습니다.](creating-user-accounts-cs/_static/image44.png)](creating-user-accounts-cs/_static/image43.png)

**그림 15**: 사용자 이름은 선행 또는 후행 공백이 허용 되지 않습니다 ([전체 크기 이미지를 보려면 클릭](creating-user-accounts-cs/_static/image45.png))


> [!NOTE]
> CreateUserWizard 컨트롤을 사용 하는 예제를 살펴봅니다 `CreatedUser` 이벤트에는 *<a id="_msoanchor_11"> </a> [추가 사용자 정보를 저장](storing-additional-user-information-cs.md)* 자습서입니다.


## <a name="summary"></a>요약

`Membership` 클래스의 `CreateUser` 메서드 멤버 자격 프레임 워크에 새 사용자 계정을 만듭니다. 이 작업을 수행 하 여 구성 된 멤버 자격 공급자에 대 한 호출을 위임 합니다. 경우에 `SqlMembershipProvider`, `CreateUser` 레코드를 추가 하는 메서드는 `aspnet_Users` 및 `aspnet_Membership` 데이터베이스 테이블입니다.

새 사용자 계정을 생성할 수 프로그래밍 방식으로 (에서 설명한 것 처럼 5 단계) 동안 CreateUserWizard 컨트롤을 사용 하는 빠르고 쉬운 방법이입니다. 이 컨트롤에 사용자 정보를 수집 하 고 구성원 프레임 워크에서 새 사용자를 만들기 위한 multi-step 사용자 인터페이스를 렌더링 합니다. 이 컨트롤 사용 동일한 내부적 `Membership.CreateUser` 5 단계 있지만 컨트롤에서 검사 하는 대로 메서드가 유효성 검사 컨트롤 사용자 인터페이스를 생성 되 고 코드가 전혀 작성 하지 않고도 사용자 계정 만들기 오류에 응답 합니다.

이 시점에서 새 사용자 계정을 만들 수 있는 원위치에서 기능이 있는 합니다. 그러나 로그인 페이지 여전히의 유효성을 검사할 두 번째 자습서에는 다시 지정한 기 하드 코드 된 자격 증명에 대 한 합니다. 에 <a id="_msoanchor_12"> </a> [다음 자습서](validating-user-credentials-against-the-membership-user-store-cs.md) 업데이트할 것 `Login.aspx` 의 유효성을 검사할 사용자 구성원 프레임 워크에 대해 자격 증명 제공 합니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [`CreateUser` 기술 문서](https://msdn.microsoft.com/library/system.web.security.membershipprovider.createuser.aspx)
- [CreateUserWizard 컨트롤 개요](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/createuserwizard.aspx)
- [파일 시스템 기반 사이트 맵 공급자 만들기](http://aspnet.4guysfromrolla.com/articles/020106-1.aspx)
- [ASP.NET 2.0 Wizard 컨트롤을 사용 하 여 단계별 사용자 인터페이스 만들기](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)
- [사이트 탐색의 ASP.NET 2.0 검사](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [마스터 페이지 및 사이트 탐색](https://asp.net/learn/data-access/tutorial-03-vb.aspx)
- [에 대 한 왔습니다 SQL 사이트 맵 공급자](https://msdn.microsoft.com/msdnmag/issues/06/02/WickedCode/default.aspx)

### <a name="about-the-author"></a>작성자 정보

여러 ASP/ASP.NET 책의 작성자 및 4GuysFromRolla.com의 창립자 Scott Mitchell의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은  *[Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 합니다. Scott에 도달할 수 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 또는에서 그의 블로그 통해 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특히 감사 드립니다.

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Teresa 머피의 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)합니다.

> [!div class="step-by-step"]
> [이전](creating-the-membership-schema-in-sql-server-cs.md)
> [다음](validating-user-credentials-against-the-membership-user-store-cs.md)
