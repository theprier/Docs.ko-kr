---
uid: web-forms/overview/older-versions-getting-started/master-pages/specifying-the-master-page-programmatically-cs
title: 마스터 페이지를 프로그래밍 방식으로 지정 (C#) | Microsoft Docs
author: rick-anderson
description: PreInit 이벤트 처리기를 통해 프로그래밍 방식으로 콘텐츠 페이지의 마스터 페이지를 설정 하는 방법을 살펴봅니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/28/2008
ms.topic: article
ms.assetid: 7c4a3445-2440-4aee-b9fd-779c05e6abb2
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/specifying-the-master-page-programmatically-cs
msc.type: authoredcontent
ms.openlocfilehash: 2294ee2e58e55901d77958e7cf45dd74fc2a1187
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="specifying-the-master-page-programmatically-c"></a>마스터 페이지를 프로그래밍 방식으로 지정 (C#)
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_09_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_09_CS.pdf)

> PreInit 이벤트 처리기를 통해 프로그래밍 방식으로 콘텐츠 페이지의 마스터 페이지를 설정 하는 방법을 살펴봅니다.


## <a name="introduction"></a>소개

밝힘으로써 예제 이후 [ *사이트 전체 레이아웃을 사용 하 여 마스터 페이지를 만들어*](creating-a-site-wide-layout-using-master-pages-cs.md), 페이지의 마스터 페이지를 통해 선언적으로 참조 한 모든 콘텐츠는 `MasterPageFile` 특성에는 `@Page`지시문입니다. 예를 들어, 다음 `@Page` 지시문 마스터 페이지 콘텐츠 페이지 링크 `Site.master`:


[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample1.aspx)]

[ `Page` 클래스](https://msdn.microsoft.com/library/system.web.ui.page.aspx) 에 `System.Web.UI` 네임 스페이스는 포함 된 [ `MasterPageFile` 속성](https://msdn.microsoft.com/library/system.web.ui.page.masterpagefile.aspx) 콘텐츠 페이지의 마스터 페이지 경로 반환 하는 즉,이 속성은 로설정된`@Page` 지시문입니다. 프로그래밍 방식으로 콘텐츠 페이지의 마스터 페이지를 지정이 속성을 사용할 수도 있습니다. 이 방법은 페이지를 방문 하는 사용자와 같은 외부 요인에 따라 마스터 페이지를 동적으로 할당 하려는 경우에 유용 합니다.

이 자습서에서는 웹 사이트에 두 번째 마스터 페이지를 추가 하 고 런타임 시 사용 하는 마스터 페이지를 동적으로 결정 합니다.

## <a name="step-1-a-look-at-the-page-lifecycle"></a>페이지 수명 주기의 살펴보겠습니다 1 단계:

ASP.NET 엔진 페이지의 퓨즈 해야 콘텐츠 페이지는 ASP.NET 페이지에 대 한 웹 서버에서 요청이 수신 될 때마다 콘텐츠 마스터 페이지에 컨트롤의 해당 ContentPlaceHolder 컨트롤입니다. 이 Fusion이 일반적인 페이지 수명 주기 동안 진행 하는 단일 제어 계층 구조를 만듭니다.

그림 1에서는이 fusion을 보여 줍니다. 그림 1의 1 단계에서 초기 콘텐츠 및 마스터 페이지 컨트롤 계층을 보여 줍니다. 콘텐츠 PreInit 스테이지의 비상 로그에 페이지의 컨트롤은 마스터 페이지 (2 단계)의 해당 contentplaceholders의에 추가 됩니다. 이 fusion 후 마스터 페이지 퓨즈 컨트롤 계층의 루트로 사용 됩니다. 이 fused 컨트롤 계층 구조를 마무리 컨트롤 계층 구조 (3 단계)를 생성 하기 위해 페이지에 추가 합니다. 결과는 페이지의 컨트롤 계층 구조 퓨즈 컨트롤 계층 구조로는입니다.


[![마스터 페이지 및 콘텐츠 페이지의 컨트롤 계층은 Fused 함께 PreInit 단계](specifying-the-master-page-programmatically-cs/_static/image2.png)](specifying-the-master-page-programmatically-cs/_static/image1.png)

**그림 01**: 마스터 페이지 및 콘텐츠 페이지의 컨트롤 계층은 PreInit 단계 중에 함께 Fused ([전체 크기 이미지를 보려면 클릭](specifying-the-master-page-programmatically-cs/_static/image3.png))


## <a name="step-2-setting-themasterpagefileproperty-from-code"></a>2 단계: 설정의`MasterPageFile`코드에서 속성

값에 따라이 fusion에서 어떤 마스터 페이지 partakes는 `Page` 개체의 `MasterPageFile` 속성입니다. 설정의 `MasterPageFile` 특성에 `@Page` 지시문은 할당 작업의 결과 `Page`의 `MasterPageFile` 초기화 단계는 페이지의 수명 주기의 첫 번째 단계는 속성입니다. 또는이 속성을 프로그래밍 방식으로 설정할 수 있습니다. 그러나 반드시 그림 1에 fusion를 수행 하기 전에이 속성을 설정 한다고 합니다.

PreInit 스테이지의 시작 부분에 `Page` 발생 시키는 개체의 [ `PreInit` 이벤트](https://msdn.microsoft.com/library/system.web.ui.page.preinit.aspx) 를 호출 하 고 해당 [ `OnPreInit` 메서드](https://msdn.microsoft.com/library/system.web.ui.page.onpreinit.aspx)합니다. 마스터 페이지를 프로그래밍 방식으로 설정 하려면 다음을 만들 수 있습니다 하거나에 대 한 이벤트 처리기는 `PreInit` 이벤트 또는 재정의 `OnPreInit` 메서드. 두 방법 모두를 살펴보겠습니다.

열어 시작 `Default.aspx.cs`,이 사이트의 홈 페이지에 대 한 코드 숨김 클래스 파일입니다. 페이지의에 대 한 이벤트 처리기를 추가 `PreInit` 다음 코드에서를 입력 하 여 이벤트:


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample2.cs)]

여기에서 설정할 수 있습니다는 `MasterPageFile` 속성입니다. 값을 할당 하는 코드를 업데이트 "~ / Site.master"에 `MasterPageFile` 속성입니다.


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample3.cs)]

하는 경우 중단점을 설정 하면 디버깅 하 고 시작 합니다 때마다는 `Default.aspx` 페이지를 방문 하거나 때마다는이 페이지를 다시 게시는 `Page_PreInit` 이벤트 처리기를 실행 및 `MasterPageFile` 속성에 할당 된 "~ / Site.master"입니다.

재정의할 수 있습니다는 `Page` 클래스의 `OnPreInit` 집합과, 메서드는 `MasterPageFile` 속성이 있습니다. 예를 들어 보겠습니다 설정 하지 특정 페이지에 있는 마스터 페이지에서 그 보다 `BasePage`합니다. 기본 페이지를 사용자 지정 클래스 만들었다고 회수 (`BasePage`)에 [ *마스터 페이지의 제목, 메타 태그 및 기타 HTML 헤더를 지정 하* ](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) 자습서입니다. 현재 `BasePage` 재정의 `Page` 클래스의 `OnLoadComplete` 메서드를 페이지의 설정에 `Title` 속성 사이트 맵 데이터에 기반 합니다. 정보를 업데이트 `BasePage` 도 재정의 하는 `OnPreInit` 메서드 프로그래밍 방식으로 마스터 페이지를 지정 합니다.


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample4.cs)]

콘텐츠는 모든 페이지에서 파생 되므로 `BasePage`, 이제 했의 마스터 페이지를 프로그래밍 방식으로 할당 합니다. 이 시점에서 `PreInit` 의 이벤트 처리기 `Default.aspx.cs` 는 불필요; 제거 작업을 합니다.

### <a name="what-about-thepagedirective"></a>어떤 점이`@Page`지시문?

약간 복잡할 수 콘텐츠 페이지는 `MasterPageFile` 속성은 이제 두 위치에서 지정 되 고: 프로그래밍 방식으로 `BasePage` 클래스의 `OnPreInit` 메서드를 통해도 `MasterPageFile` 각 콘텐츠 페이지에서 특성 `@Page` 지시문입니다.

페이지 수명 주기의 첫 번째 단계는 초기화 단계. 이 단계는 `Page` 개체의 `MasterPageFile` 속성의 값이 할당 되는 `MasterPageFile` 특성에 `@Page` 지시문 (제공) 하는 경우. PreInit 단계에서 초기화 단계를 따르며은 프로그래밍 방식으로 설정할 여기는 `Page` 개체의 `MasterPageFile` 속성을 함으로써에서 할당 된 값을 덮어쓰지는 `@Page` 지시문입니다. 에서는 설정 때문에 `Page` 개체의 `MasterPageFile` 속성을 프로그래밍 방식으로에서는 제거할 수는 `MasterPageFile` 에서 특성의 `@Page` 최종 사용자 환경에 영향을 주지 않고 지시문입니다. 이 사용자가 직접를 유도 하 계속 진행 하 고 제거는 `MasterPageFile` 에서 특성의 `@Page` 지시문 `Default.aspx` 한 후 브라우저를 통해 페이지를 방문 합니다. 예상 대로 출력은 동일 특성이 제거 하기 전에.

여부는 `MasterPageFile` 속성을 통해 설정는 `@Page` 지시문 또는 프로그래밍 방식으로 최종 사용자의 환경에 중요 하지 않습니다. 그러나는 `MasterPageFile` 특성에 `@Page` 지시문은 Visual Studio에서 디자인 타임 동안 만드는 데 사용 된 WYSIWYG 디자이너의 뷰. 반환 하는 경우 `Default.aspx` Visual Studio에서 탐색 및 디자이너에는 메시지가 표시 됩니다 "마스터 페이지 오류: 페이지에 대 한 마스터 페이지 참조를 필요로 하는 컨트롤 하지만 지정 되지 않은" (그림 2 참조).

상태로 유지 해야 하는 간단히 말해는 `MasterPageFile` 특성에 `@Page` 지시문 Visual Studio에서 풍부한 디자인 타임 환경을 즐길 수 있습니다.


[![Visual Studio는 사용 된 @Page 디자인 뷰를 렌더링 하는 지시문의 MasterPageFile 특성](specifying-the-master-page-programmatically-cs/_static/image5.png)](specifying-the-master-page-programmatically-cs/_static/image4.png)

**그림 02**: 사용 하 여 Visual Studio는 `@Page` 지시문의 `MasterPageFile` 디자인 뷰를 렌더링할 특성 ([전체 크기 이미지를 보려면 클릭](specifying-the-master-page-programmatically-cs/_static/image6.png))


## <a name="step-3-creating-an-alternative-master-page"></a>3 단계: 프로그램 대신 마스터 페이지 만들기

없기 때문에 런타임에 콘텐츠 페이지의 마스터 페이지를 프로그래밍 방식으로 설정할 수를 동적으로 일부 외부 조건에 따라 특정 마스터 페이지를 로드 합니다. 이 기능은 사이트의 레이아웃 해야 하는 다를 사용자에 따라 하는 경우에 유용할 수 있습니다. 예를 들어, 각 레이아웃은 다른 마스터 페이지에 연결 된 해당 사용자가 자신의 블로그에 대 한 레이아웃을 선택할 수 블로그 엔진 웹 응용 프로그램을 허용할 수 있습니다. 런타임에 방문자가 사용자의 블로그를 보고 하는 웹 응용 프로그램 블로그의 레이아웃을 결정 하 콘텐츠 페이지와 해당 마스터 페이지를 동적으로 연결 해야 합니다.

동적으로 일부 외부 조건에 따라 런타임에 마스터 페이지를 로드 하는 방법을 살펴보겠습니다. 웹 사이트는 현재 마스터 페이지를 하나만 포함 (`Site.master`). 다른 마스터 페이지 런타임에 마스터 페이지를 설명 하기 위해 필요 합니다. 이 단계를 만들고 새 마스터 페이지를 구성에 중점을 둡니다. 4 단계는 런타임에 사용할 마스터 페이지를 확인 합니다.

이라는 루트 폴더에는 새 마스터 페이지를 만들고 `Alternate.master`합니다. 이라는 웹 사이트에 새 스타일 시트를 추가할 수도 `AlternateStyles.css`합니다.


[![다른 항목 추가 웹 사이트에 마스터 페이지 및 CSS 파일](specifying-the-master-page-programmatically-cs/_static/image8.png)](specifying-the-master-page-programmatically-cs/_static/image7.png)

**그림 03**: 다른 마스터 페이지 추가 및 CSS 파일을 웹 사이트 ([전체 크기 이미지를 보려면 클릭](specifying-the-master-page-programmatically-cs/_static/image9.png))


디자인 했습니다는 `Alternate.master` 마스터 페이지 남색 배경에 및 가운데 페이지의 맨 위쪽에 표시 되는 제목입니다. 왼쪽 열 분배 하 고 아래에 해당 콘텐츠를 이동 했으므로 필자는 `MainContent` 이제 페이지의 전체 너비를 확장 하 합니다. 정렬 되지 않은 단원 목록을 nixed I와 위의 가로 목록으로 대체 하는 또한 `MainContent`합니다. 글꼴 및 색에 사용 되는 마스터 페이지 (을 확장 하면 해당 콘텐츠 페이지)도 업데이트 합니다. 그림 4 `Default.aspx` 사용 하는 경우는 `Alternate.master` 마스터 페이지입니다.

> [!NOTE]
> ASP.NET 정의 하는 기능에 포함 되어 *테마*합니다. 테마는 이미지, CSS 파일 및 스타일 관련 웹 컨트롤 속성 설정 페이지 런타임 시에 적용할 수 있는 컬렉션. 테마는 사이트의 레이아웃 및 CSS 규칙에 표시 되는 이미지에만 다른 경우로 이동 하는 방법. 레이아웃 등 다른 웹 컨트롤을 사용 하거나 매우 다른 레이아웃을 실질적으로 더 달라 별도 마스터 페이지를 사용 해야 합니다. 테마에 대 한 자세한 내용은이 자습서의 끝에 추가 정보 섹션을 참조 하십시오.


[![콘텐츠 분량 이제 새로운 모양과 느낌을 사용할 수 있습니다.](specifying-the-master-page-programmatically-cs/_static/image11.png)](specifying-the-master-page-programmatically-cs/_static/image10.png)

**그림 04**: 콘텐츠 분량 이제 새로운 모양과 느낌을 사용할 수 ([전체 크기 이미지를 보려면 클릭](specifying-the-master-page-programmatically-cs/_static/image12.png))


마스터 및 콘텐츠 페이지의 태그를 결합 하는 경우는 `MasterPage` 클래스 검사 하는 모든 콘텐츠를 콘텐츠 페이지에서 컨트롤에 마스터 페이지에서 ContentPlaceHolder 참조 합니다. 존재 하지 않는 ContentPlaceHolder 참조 하는 콘텐츠 컨트롤을 찾을 수 있는 경우 예외가 throw 됩니다. 콘텐츠 페이지에 할당 되는 마스터 페이지에 각각에 대해 한 ContentPlaceHolder 추가 해야 하는 즉, 콘텐츠 페이지에서 컨트롤의 콘텐츠입니다.

`Site.master` 마스터 페이지에 4 개의 ContentPlaceHolder 컨트롤이 포함 됩니다.

- `head`
- `MainContent`
- `QuickLoginUI`
- `LeftColumnContent`

하나 또는 두 개만 콘텐츠 컨트롤; 웹 사이트에서 콘텐츠 페이지 중 일부가 포함 다른 각 사용 가능한 contentplaceholders의 대 한 콘텐츠 컨트롤을 포함 됩니다. 경우 새 마스터 페이지 (`Alternate.master`)에서 contentplaceholders의 모든 콘텐츠 컨트롤을 포함 하는 콘텐츠 페이지에 할당 되지 않을 수 있습니다 `Site.master` 것이 중요 하 `Alternate.master` 와동일한ContentPlaceHolder컨트롤포함`Site.master`.

가져오려는 프로그램 `Alternate.master` 마스터 페이지 (그림 4 참조)를 검색, 마스터 페이지의 스타일을 정의 하 여 시작을 다음과 같이 표시 하는 `AlternateStyles.css` 스타일 시트입니다. 에 다음 규칙에 추가할 `AlternateStyles.css`:


[!code-css[Main](specifying-the-master-page-programmatically-cs/samples/sample5.css)]

다음으로, 다음 선언적 태그를 추가 `Alternate.master`합니다. 볼 수 있듯이 `Alternate.master` 같은 네 가지 ContentPlaceHolder 컨트롤 포함 `ID` 값에서 ContentPlaceHolder 컨트롤로 `Site.master`합니다. 또한 ASP.NET AJAX 프레임 워크를 사용 하는 웹 사이트에서 해당 페이지에 필요한는 ScriptManager 컨트롤이 포함 됩니다.


[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample6.aspx)]

### <a name="testing-the-new-master-page"></a>새 마스터 페이지를 테스트합니다.

이 새 마스터 페이지 업데이트를 테스트 하는 `BasePage` 클래스의 `OnPreInit` 메서드 있도록는 `MasterPageFile` 속성 값이 할당은 "~ / Alternate.master" 한 후 웹 사이트를 방문 합니다. 모든 페이지는 두 가지를 제외한 오류 없이 작동 해야: `~/Admin/AddProduct.aspx` 및 `~/Admin/Products.aspx`합니다. 제품에 DetailsView을 추가할 `~/Admin/AddProduct.aspx` 결과 `NullReferenceException` 마스터 페이지의 설정 하려고 시도 하는 코드 줄에서 `GridMessageText` 속성입니다. 방문할 때 `~/Admin/Products.aspx` 는 `InvalidCastException` 메시지와 함께 페이지 로드에 throw 됩니다: "종류의 개체를 캐스팅할 수 없습니다. ' ASP.alternate\_마스터 ' 형식으로 ' ASP.site\_마스터 '."

이러한 오류가 발생 하기 때문에 `Site.master` 코드 숨김 클래스를 공용 이벤트, 속성 및 메서드에 정의 되어 있지 않은 포함 `Alternate.master`합니다. 이러한 두 페이지의 태그 일부는 `@MasterType` 참조 하는 지시문은 `Site.master` 마스터 페이지입니다.


[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample7.aspx)]

또한 DetailsView의 `ItemInserted` 의 이벤트 처리기 `~/Admin/AddProduct.aspx` 자유로운 형식의 캐스팅 하는 코드가 포함 되어 `Page.Master` 속성 형식의 개체로 `Site`합니다. `@MasterType` 지시문 (이러한 방식으로 사용 됨)과의 캐스트는 `ItemInserted` 이벤트 처리기 밀접 하 게 결합 된 `~/Admin/AddProduct.aspx` 및 `~/Admin/Products.aspx` 페이지를 `Site.master` 마스터 페이지입니다.

시켜 서이 밀접 한 결합을 중단 하려면 `Site.master` 및 `Alternate.master` 공용 멤버에 대 한 정의 포함 하는 공통 기본 클래스에서 파생 됩니다. 그런 다음, 업데이트할 수는 `@MasterType` 지시문이 공통 기본 형식을 참조할 수 있습니다.

### <a name="creating-a-custom-base-master-page-class"></a>사용자 지정 기본 마스터 페이지 클래스 만들기

새 클래스 파일에 추가 된 `App_Code` 라는 폴더 `BaseMasterPage.cs` 에서 파생 되 게 `System.Web.UI.MasterPage`합니다. 정의 해야는 `RefreshRecentProductsGrid` 메서드 및 `GridMessageText` 속성 `BaseMasterPage`를 이동할 수 없습니다. 단순히에서 해당 있습니다 하지만 `Site.master` 이러한 멤버는 관련 된 웹 컨트롤을 사용 하기 때문에 `Site.master` 마스터 페이지 (의 `RecentProducts` GridView 및 `GridMessage` 레이블).

구성 작업을 수행 하 필요한 것은 `BaseMasterPage` 이러한 멤버를 정의 하지만에서 실제로 구현 하는 하는 방식으로 `BaseMasterPage`의 파생 된 클래스 (`Site.master` 및 `Alternate.master`). 클래스 및 해당 멤버를 표시 하 여 이러한 유형의 상속은 가능한 `abstract`합니다. 즉, 추가 `abstract` 키워드 이러한 두 멤버를가 하는 데몬에 `BaseMasterPage` 구현 있지 않은 `RefreshRecentProductsGrid` 및 `GridMessageText`했지만 해당 클래스의 파생된 클래스는 합니다.

또한를 정의 해야는 `PricesDoubled` 이벤트에 `BaseMasterPage` 이벤트를 발생 시키는 파생된 클래스에서 제공 합니다. 이 동작을 용이 하 게 하려면.NET Framework에서 사용 되는 패턴은 기본 클래스에 공용 이벤트를 만들고 보호 된 추가 `virtual` 라는 메서드 `OnEventName`합니다. 파생된 클래스를 발생 시키고이 메서드를 호출한 다음 수 또는 코드를 실행 하는 이벤트가 발생 한 후 또는 바로 앞에 재정의할 수 있습니다.

업데이트 프로그램 `BaseMasterPage` 클래스 다음 코드를 포함 합니다.


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample8.cs)]

다음으로 이동 하는 `Site.master` 코드 숨김 클래스에서 파생 되는 및 `BaseMasterPage`합니다. 때문에 `BaseMasterPage` 은 `abstract` 옵션 보다 우선 적용 해야 `abstract` 에서 멤버 `Site.master`합니다. 추가 `override` 키워드는 메서드 및 속성 정의를 합니다. 또한를 발생 시키는 코드를 업데이트는 `PricesDoubled` 이벤트에는 `DoublePrice` 단추의 `Click` 기본 클래스를 호출 하 여 이벤트 처리기 `OnPricesDoubled` 메서드.

이러한 수정 후의 `Site.master` 코드 숨김 클래스는 다음 코드를 포함 해야 합니다.


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample9.cs)]

도 업데이트 해야 `Alternate.master`의 코드 숨김 클래스를 파생할 `BaseMasterPage` 두 재정의 `abstract` 멤버입니다. 하지만 없기 때문에 `Alternate.master` 는 가장 최근의 제품 또는 새 제품 후 메시지를 표시 하는 레이블을 데이터베이스에 추가 되는 목록, 이러한 방법 필요가 없습니다 아무런 작업도 GridView 포함 되어 있지 않습니다.


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample10.cs)]

### <a name="referencing-the-base-master-page-class"></a>기본 마스터 페이지 클래스 참조

완료 했으므로 `BaseMasterPage` 있고 클래스를 확장 하는 두 개의 마스터 페이지 있는 업데이트 하는 마지막 단계는 `~/Admin/AddProduct.aspx` 및 `~/Admin/Products.aspx` 이 공통 형식에 참조 하는 페이지입니다. 변경 하 여 시작 된 `@MasterType` 에서 페이지를 둘 다에 지시문:


[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample11.aspx)]

대상:


[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample12.aspx)]

파일 경로 참조 하는 대신는 `@MasterType` 속성 참조의 기본 형식 (`BaseMasterPage`). 따라서 강력한 형식의 `Master` 두 페이지의 코드 숨김 클래스에 사용 되는 속성은 이제 형식의 `BaseMasterPage` (형식 대신 `Site`). 위치에 이러한 변경으로 인해 다시 방문 `~/Admin/Products.aspx`합니다. 이전에 그 결과 되었습니다 캐스팅 오류는 페이지를 사용 하도록 구성 되어 있으므로 `Alternate.master` 마스터 페이지 이지만 `@MasterType` 참조 지시문은 `Site.master` 파일입니다. 하지만 이제 페이지를 오류 없이 렌더링 합니다. 때문에 이것이 `Alternate.master` 마스터 페이지를 형식의 개체로 캐스팅 될 수 `BaseMasterPage` (이후 것 확장).

수행 해야 하는 한 작은 변경 내용이 없는지 `~/Admin/AddProduct.aspx`합니다. DetailsView 컨트롤 `ItemInserted` 이벤트 처리기에서 모두 강력한 형식의 사용 `Master` 속성 및 자유로운 형식의 `Page.Master` 속성입니다. 업데이트에서는 강력한 형식의 참조 해결는 `@MasterType` 지시문을 사용 하지만를 자유로운 형식의 참조를 업데이트 해야 합니다. 다음 코드 줄을 바꿉니다.


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample13.cs)]

캐스팅 하는 다음과 같은 `Page.Master` 기본 형식:


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample14.cs)]

## <a name="step-4-determining-what-master-page-to-bind-to-the-content-pages"></a>4 단계: 마스터 페이지 콘텐츠 페이지를 바인딩할 결정

우리의 `BasePage` 클래스에는 모든 콘텐츠 페이지의 현재 설정 `MasterPageFile` 페이지 수명 주기의 특정 PreInit 단계에서 하드 코드 된 값에는 속성입니다. 일부 외부 요인에 마스터 페이지를 기반으로이 코드를 업데이트할 수 있습니다. 아마도 마스터 페이지를 로드 현재 로그온된 한 사용자의 기본 설정에 따라 달라 집니다. 코드를 작성 해야 경우에 `OnPreInit` 메서드에서 `BasePage` 현재 방문한 사용자의 마스터 페이지를 기본을 조회 하는 합니다.

사용자-를 사용 하는 마스터 페이지를 선택할 수 있도록 하는 웹 페이지를 만들어 보겠습니다 `Site.master` 또는 `Alternate.master` -여기에서이 선택한 세션 변수에 저장 합니다. 명명 된 루트 디렉터리에서 새로운 웹 페이지를 만들어 시작 `ChooseMasterPage.aspx`합니다. 이 페이지 (또는 다른 콘텐츠 페이지 예측이)를 만들 때 마스터 페이지 프로그래밍 방식으로 설정 되어 있으므로 마스터 페이지에 바인딩할 필요가 없습니다 `BasePage`합니다. 그러나 마스터 페이지에 새 페이지에 연결 하지 않으면 다음 새 페이지의 기본 선언적 태그가 포함 Web Form 및 마스터 페이지에서 제공 하는 다른 콘텐츠입니다. 적절 한 콘텐츠 컨트롤과이 태그를 수동으로 교체 해야 합니다. 이런 이유로 필자 쉬울 마스터 페이지에 새 ASP.NET 페이지를 바인딩할.

> [!NOTE]
> 때문에 `Site.master` 및 `Alternate.master` 동일 집합을 가져서는 ContentPlaceHolder 컨트롤 마스터 페이지에 새 콘텐츠 페이지를 만들 때 선택한 관계는 문제가 되지 않습니다. 일관성을 위해는 것이 좋습니다를 사용 하 여 `Site.master`합니다.


[![웹 사이트에 새 콘텐츠 페이지를 추가 합니다.](specifying-the-master-page-programmatically-cs/_static/image14.png)](specifying-the-master-page-programmatically-cs/_static/image13.png)

**그림 05**: 웹 사이트에 새 콘텐츠 페이지 추가 ([전체 크기 이미지를 보려면 클릭](specifying-the-master-page-programmatically-cs/_static/image15.png))


업데이트는 `Web.sitemap` 파일을이 단원에 대 한 항목을 포함 합니다. 아래에 다음 태그를 추가 `<siteMapNode>` 마스터 페이지 및 ASP.NET AJAX 단원:


[!code-xml[Main](specifying-the-master-page-programmatically-cs/samples/sample15.xml)]

모든 콘텐츠를 추가 하기 전에 `ChooseMasterPage.aspx` 페이지에서 파생 되도록 페이지의 코드 숨김 클래스를 업데이트 하려면 잠시 `BasePage` (대신 `System.Web.UI.Page`). 다음으로 페이지에 필요한 DropDownList 컨트롤을 추가, 설정 해당 `ID` 속성을 `MasterPageChoice`와 두 개의 ListItems 추가 `Text` 의 값 "~ / Site.master" 및 "~ / Alternate.master"입니다.

페이지에 단추 웹 컨트롤을 추가 하 고 설정 해당 `ID` 및 `Text` 속성을 `SaveLayout` 및 "저장 레이아웃 선택"를 각각. 이 시점에서 페이지의 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample16.aspx)]

해당 페이지를 처음 방문 하는 경우 사용자의 현재 선택 된 마스터 페이지 선택 표시 해야 합니다. 만들기는 `Page_Load` 이벤트 처리기를 다음 코드를 추가 합니다.


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample17.cs)]

위의 코드는 첫 번째 페이지 방문에만 (및 후속 포스트백에 없는)를 실행 합니다. 먼저 확인 하는 경우 세션 변수 `MyMasterPage` 존재 합니다. 일치 하는 ListItem를 찾으려고 시도 하는 경우는 `MasterPageChoice` DropDownList 합니다. 일치 하는 ListItem이 없으면 해당 `Selected` 속성이 `true`합니다.

또한 사용자의 선택에 저장 하는 코드가 필요는 `MyMasterPage` 세션 변수입니다. 에 대 한 이벤트 처리기를 만들고는 `SaveLayout` 단추의 `Click` 이벤트를 다음 코드를 추가 합니다.


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample18.cs)]

> [!NOTE]
> 시간순으로는 `Click` 포스트백에 대해 이벤트 처리기 실행, 마스터 페이지 이미 선택 되었습니다. 따라서 다음 페이지를 방문 될 때까지 사용자가 드롭다운 목록에서 선택한 적용 되지 않습니다. `Response.Redirect` 브라우저를 다시 요청을 강제로 `ChooseMasterPage.aspx`합니다.


와 `ChooseMasterPage.aspx` 완료 페이지에서 우리의 마지막 작업 있어야 하는 `BasePage` 할당는 `MasterPageFile` 속성의 값에 따라는 `MyMasterPage` 세션 변수입니다. 세션 변수 설정 하지 않은 경우 `BasePage` 기본적으로 `Site.master`합니다.


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample19.cs)]

> [!NOTE]
> 할당 하는 코드를 이동 했는데는 `Page` 개체의 `MasterPageFile` 의 속성은 `OnPreInit` 이벤트 처리기 및 두 개의 별도 메서드로 합니다. 이 첫 번째 방법은 `SetMasterPageFile`, 할당 된 `MasterPageFile` 속성을 두 번째 메서드에 의해 반환 된 값으로 `GetMasterPageFileFromSession`합니다. 내용이 `SetMasterPageFile` 메서드 `virtual` 를 확장 하는 이후의 클래스 `BasePage` 필요한 경우 사용자 지정 논리를 구현 하도록 재정의 필요에 따라 수 있습니다. 재정의의 예를 보면 `BasePage`의 `SetMasterPageFile` 다음 자습서의 속성입니다.


이 코드가 방문는 `ChooseMasterPage.aspx` 페이지. 처음에 `Site.master` 마스터 페이지 선택된 (그림 6 참조), 이지만 사용자 드롭 다운 목록에서 다른 마스터 페이지를 선택할 수 있습니다.


[![Site.master 마스터 페이지를 사용 하 여 콘텐츠 페이지는 표시](specifying-the-master-page-programmatically-cs/_static/image17.png)](specifying-the-master-page-programmatically-cs/_static/image16.png)

**그림 06**: 콘텐츠 페이지를 사용 하 여 표시 되는 `Site.master` 마스터 페이지 ([전체 크기 이미지를 보려면 클릭](specifying-the-master-page-programmatically-cs/_static/image18.png))


[![콘텐츠 페이지 Alternate.master 마스터 페이지를 사용 하 여 표시 됩니다.](specifying-the-master-page-programmatically-cs/_static/image20.png)](specifying-the-master-page-programmatically-cs/_static/image19.png)

**그림 07**: 콘텐츠 페이지는 표시를 사용 하 여는 `Alternate.master` 마스터 페이지 ([전체 크기 이미지를 보려면 클릭](specifying-the-master-page-programmatically-cs/_static/image21.png))


## <a name="summary"></a>요약

콘텐츠 페이지를 방문 하는 경우 해당 콘텐츠 컨트롤을 해당 마스터 페이지의 ContentPlaceHolder 컨트롤과 결합 합니다. 콘텐츠 페이지의 마스터 페이지가으로 표시 되는 `Page` 클래스의 `MasterPageFile` 속성에 할당 되는 `@Page` 지시문의 `MasterPageFile` 초기화 단계는 특성입니다. 표시 값을 할당할 수 있습니다이 자습서로는 `MasterPageFile` PreInit 단계를 완료 하기 전에 이렇게 만큼 속성입니다. 프로그래밍 방식으로 마스터 페이지를 지정 하기 위해서는 외부 요인에 따라 마스터 페이지에 콘텐츠 페이지를 동적으로 바인딩 같은 더 고급 시나리오에 노출 합니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 페이지 수명 주기 다이어그램](http://emanish.googlepages.com/Asp.Net2.0Lifecycle.PNG)
- [ASP.NET 페이지 수명 주기 개요](https://msdn.microsoft.com/library/ms178472.aspx)
- [ASP.NET 테마 및 스킨 개요](https://msdn.microsoft.com/library/ykzx33wh.aspx)
- [마스터 페이지: 팁, 요령 및 트랩](http://www.odetocode.com/articles/450.aspx)
- [Asp.net 테마](http://www.odetocode.com/articles/423.aspx)

### <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 작성자 여러 ASP/ASP.NET 설명서와 4GuysFromRolla.com의 창립자의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 3.5 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)합니다. Scott에 도달할 수 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com) 또는에서 그의 블로그 통해 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Suchi Banerjee 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](master-pages-and-asp-net-ajax-cs.md)
> [다음](nested-master-pages-cs.md)
