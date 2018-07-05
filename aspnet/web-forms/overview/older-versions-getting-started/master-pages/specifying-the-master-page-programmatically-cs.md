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
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/specifying-the-master-page-programmatically-cs
msc.type: authoredcontent
ms.openlocfilehash: 2b3fbd95a8088e20382c426fcdcc6a4b6e67d44b
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37370392"
---
<a name="specifying-the-master-page-programmatically-c"></a>마스터 페이지를 프로그래밍 방식으로 지정 (C#)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_09_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_09_CS.pdf)

> PreInit 이벤트 처리기를 통해 프로그래밍 방식으로 콘텐츠 페이지의 마스터 페이지를 설정 하는 방법을 살펴봅니다.


## <a name="introduction"></a>소개

첫 예제에서는 이후 [ *사이트 전체 레이아웃을 사용 하 여 마스터 페이지 만들기*](creating-a-site-wide-layout-using-master-pages-cs.md)페이지를 통해 선언적으로 해당 마스터 페이지를 참조 한 모든 콘텐츠를 `MasterPageFile` 특성을 `@Page`지시문입니다. 다음 예를 들어 `@Page` 지시문의 마스터 페이지 콘텐츠 페이지 링크 `Site.master`:


[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample1.aspx)]

합니다 [ `Page` 클래스](https://msdn.microsoft.com/library/system.web.ui.page.aspx) 에 `System.Web.UI` 네임 스페이스는 포함는 [ `MasterPageFile` 속성](https://msdn.microsoft.com/library/system.web.ui.page.masterpagefile.aspx) 콘텐츠 페이지의 마스터 페이지 경로 반환 하는이 속성은 로설정된`@Page` 지시문입니다. 이 속성은 프로그래밍 방식으로 콘텐츠 페이지의 마스터 페이지를 지정 하려면 데도 사용할 수 있습니다. 이 방법은 페이지를 방문 하는 사용자와 같은 외부 요인에 따라 마스터 페이지를 동적으로 할당 하려는 경우에 유용 합니다.

이 자습서에서는 웹 사이트에 두 번째 마스터 페이지를 추가 하 고 동적으로 런타임 시 사용 하는 마스터 페이지를 결정 합니다.

## <a name="step-1-a-look-at-the-page-lifecycle"></a>페이지 수명 주기 살펴보기 1 단계:

ASP.NET 엔진 페이지의 fuse 해야 요청 콘텐츠 페이지는 ASP.NET 페이지에 대 한 웹 서버에 도착 될 때마다 콘텐츠를 마스터 페이지에 컨트롤의 contentplaceholder 해당 합니다. 이 fusion 다음 일반적인 페이지 수명 주기를 통해 진행할 수 있는 단일 컨트롤 계층 구조를 만듭니다.

그림 1에서는이 fusion를 보여 줍니다. 그림 1에 1 단계에는 초기 콘텐츠와 마스터 페이지 컨트롤 계층 구조를 보여 줍니다. PreInit 스테이지 콘텐츠 비상 끝날 때 페이지의 컨트롤에 마스터 페이지 (2 단계)의 해당 ContentPlaceHolders에 추가 됩니다. 이 fusion 후 마스터 페이지는 퓨즈 컨트롤 계층의 루트로 사용 됩니다. 제어를 결합 하는이 계층 구조 완성된 컨트롤 계층 구조 (3 단계)를 생성 하기 위해 페이지에 추가 됩니다. 결과는 페이지의 컨트롤 계층 구조 퓨즈 컨트롤 계층 구조에 포함 됩니다.


[![마스터 페이지 콘텐츠 페이지의 컨트롤 계층 구조와 함께 결합 PreInit 단계](specifying-the-master-page-programmatically-cs/_static/image2.png)](specifying-the-master-page-programmatically-cs/_static/image1.png)

**그림 01**:의 마스터 페이지 및 콘텐츠 페이지의 컨트롤 계층 구조 PreInit 단계 동안 함께 결합 하는 ([큰 이미지를 보려면 클릭](specifying-the-master-page-programmatically-cs/_static/image3.png))


## <a name="step-2-setting-themasterpagefileproperty-from-code"></a>2 단계: 설정의`MasterPageFile`코드에서 속성

값에 따라이 fusion에서 마스터 페이지 partakes 합니다 `Page` 개체의 `MasterPageFile` 속성입니다. 설정를 `MasterPageFile` 특성을 `@Page` 할당 하는 순 효과가 지시문을 `Page`의 `MasterPageFile` 속성 페이지의 수명 주기의 첫 번째 단계는 초기화 단계 중입니다. 이 속성을 프로그래밍 방식으로 설정 또는 했습니다. 그러나 반드시 fusion 그림 1에서 수행 되기 전에이 속성을 설정 한다고 합니다.

PreInit 스테이지의 시작 부분에 `Page` 발생 시키는 개체 해당 [ `PreInit` 이벤트](https://msdn.microsoft.com/library/system.web.ui.page.preinit.aspx) 호출 하 고 해당 [ `OnPreInit` 메서드](https://msdn.microsoft.com/library/system.web.ui.page.onpreinit.aspx)합니다. 마스터 페이지를 프로그래밍 방식으로 설정 하려면 다음을 만들 수 있습니다 하거나에 대 한 이벤트 처리기를 `PreInit` 이벤트 또는 재정의 `OnPreInit` 메서드. 두 방법 모두를 살펴보겠습니다.

열어서 시작 `Default.aspx.cs`, 사이트의 홈 페이지에 대 한 코드 숨김 클래스 파일입니다. 페이지에 대 한 이벤트 처리기를 추가 `PreInit` 다음 코드에서를 입력 하 여 이벤트:


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample2.cs)]

여기에서 설정할 수 있습니다는 `MasterPageFile` 속성입니다. 값 할당 되도록 코드 업데이트 "~ / Site.master"에 `MasterPageFile` 속성입니다.


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample3.cs)]

중단점을 설정 하 고 표시 하면 디버깅 하는 작업을 시작 하는 경우 때마다를 `Default.aspx` 때마다는이 페이지를 포스트백 또는 페이지를 방문 합니다 `Page_PreInit` 이벤트 처리기가 실행 및 `MasterPageFile` 속성에 할당 된 "~ / Site.master"입니다.

재정의할 수 있습니다 합니다 `Page` 클래스의 `OnPreInit` 집합과 메서드는 `MasterPageFile` 속성이 있습니다. 예를 들어 보겠습니다 설정 되지 특정 페이지에서 마스터 페이지에서 아니라 `BasePage`합니다. 기본 페이지를 사용자 지정 클래스를 만든 것을 기억 (`BasePage`)에 [ *마스터 페이지에서 제목, 메타 태그 및 기타 HTML 헤더 지정* ](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) 자습서입니다. 현재 `BasePage` 재정의 된 `Page` 클래스의 `OnLoadComplete` 메서드를 페이지의 설정 `Title` 사이트 맵 데이터를 기반으로 속성입니다. 업데이트 해 보겠습니다 `BasePage` 도 재정의 하 여 `OnPreInit` 프로그래밍 방식으로 마스터 페이지를 지정 하는 방법.


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample4.cs)]

모든 콘텐츠 페이지에서 파생 되므로 `BasePage`, 모두 이제 프로그래밍 방식으로 할당 하는 마스터 페이지입니다. 이 시점에서 `PreInit` 이벤트 처리기 `Default.aspx.cs` 불필요 한은 제거를 자유롭게 합니다.

### <a name="what-about-thepagedirective"></a>어떤 점이 합니다`@Page`지시문?

약간 복잡할 수 콘텐츠 페이지는 `MasterPageFile` 속성은 이제 두 위치에 지정 된: 프로그래밍 방식으로 `BasePage` 클래스의 `OnPreInit` 메서드 통해서도 `MasterPageFile` 각 콘텐츠 페이지의 특성 `@Page` 지시문입니다.

페이지 수명 주기의 첫 번째 단계는 초기화 단계입니다. 이 단계는 `Page` 개체의 `MasterPageFile` 속성의 값이 할당 됩니다는 `MasterPageFile` 특성을 `@Page` 지시문 (이 제공 된 경우). PreInit 스테이지 초기화 단계를 따르고은 프로그래밍 방식으로 설정한 다음 합니다 `Page` 개체의 `MasterPageFile` 속성에서 할당 된 값을 덮어쓰게 됩니다는 `@Page` 지시문입니다. 설정 된 것 이기 때문에 `Page` 개체의 `MasterPageFile` 속성을 프로그래밍 방식으로에서는 제거할 수는 `MasterPageFile` 에서 특성을 `@Page` 최종 사용자의 환경 영향을 주지 않고 지시문입니다. 이 직접 유도, 계속 해 서 제거 합니다 `MasterPageFile` 에서 특성을 `@Page` 지시문 `Default.aspx` 다음 브라우저를 통해 페이지를 방문 하 고 합니다. 예상한 대로 출력은 동일 특성 제거 되기 전에 합니다.

여부를 합니다 `MasterPageFile` 속성을 통해 설정 됩니다는 `@Page` 지시문 또는 프로그래밍 방식으로 최종 사용자의 환경에 중요 하지 않습니다. 그러나를 `MasterPageFile` 특성을 `@Page` 지시문은 Visual Studio에서 디자인 타임 동안 만드는 데 사용 된 WYSIWYG 디자이너에서 보기. 반환 하는 경우 `Default.aspx` Visual Studio에서 이동한 디자이너에는 메시지가 표시 됩니다 "마스터 페이지 오류: 페이지에 대 한 마스터 페이지 참조를 필요로 하는 컨트롤 하지만 지정 되지 않은" (그림 2 참조).

유지 해야 하는 간단히 말해 합니다 `MasterPageFile` 특성을 `@Page` 지시문을 Visual Studio에서 다양 한 디자인 타임 경험해 보세요.


[![Visual Studio 사용을 @Page 디자인 뷰를 렌더링 하는 지시문의 MasterPageFile 특성](specifying-the-master-page-programmatically-cs/_static/image5.png)](specifying-the-master-page-programmatically-cs/_static/image4.png)

**그림 02**: Visual Studio에서 사용 하는 `@Page` 지시문의 `MasterPageFile` 디자인 뷰를 렌더링할 특성 ([클릭 하 여 큰 이미지 보기](specifying-the-master-page-programmatically-cs/_static/image6.png))


## <a name="step-3-creating-an-alternative-master-page"></a>3 단계: 프로그램 대신 마스터 페이지 만들기

콘텐츠 페이지의 마스터 페이지는 일부 외부 조건에 따라 특정 마스터 페이지를 동적으로 로드 하는 것이 불가능 런타임에 프로그래밍 방식으로 설정할 수 있습니다 때문에. 이 기능을 사이트의 레이아웃 해야 하는 다를 사용자를 기반으로 하는 경우에 유용할 수 있습니다. 예를 들어, 여기서 각 레이아웃은 다른 마스터 페이지를 사용 하 여 연결 된 해당 사용자가 해당 블로그에 대 한 레이아웃을 선택할 블로그 엔진 웹 응용 프로그램을 수 있습니다. 런타임 시 방문자를 보는 사용자의 블로그, 웹 응용 프로그램 블로그의 레이아웃을 확인 하 고 콘텐츠 페이지를 사용 하 여 해당 마스터 페이지를 동적으로 연결을 해야 합니다.

일부 외부 조건에 따라 런타임에 마스터 페이지를 동적으로 로드 하는 방법을 살펴보겠습니다. 웹 사이트는 하나만 마스터 페이지에 현재 포함 되어 있습니다 (`Site.master`). 다른 마스터 페이지 선택 런타임에 마스터 페이지를 설명 하기 위해 필요 합니다. 이 단계를 만들고 새 마스터 페이지를 구성에 중점을 둡니다. 4 단계는 런타임 시 사용 하는 마스터 페이지를 확인 살펴봅니다.

명명 된 루트 폴더에서 마스터 페이지를 새로 만들 `Alternate.master`합니다. 명명 된 웹 사이트에 새 스타일 시트를 추가할 수도 `AlternateStyles.css`합니다.


[![다른 추가 웹 사이트에 마스터 페이지 및 CSS 파일](specifying-the-master-page-programmatically-cs/_static/image8.png)](specifying-the-master-page-programmatically-cs/_static/image7.png)

**그림 03**: 다른 마스터 페이지 추가 및 CSS 파일을 웹 사이트 ([큰 이미지를 보려면 클릭](specifying-the-master-page-programmatically-cs/_static/image9.png))


설계 했지만 `Alternate.master` 남색 배경 및 가운데 페이지의 위쪽에 표시 되는 제목 할 마스터 페이지입니다. 왼쪽 열의 분배 하 고 아래 콘텐츠를 이동 했습니다는 `MainContent` 이제 페이지의 전체 너비로 확장 되는 각각의 ContentPlaceHolder 컨트롤로 합니다. 또한, 순서가 지정 되지 않은 단원 목록 nixed 했으며 위의 가로 목록으로 대체 `MainContent`합니다. 필자는 또한 글꼴 및 색에 사용 되는 마스터 페이지 (을 확장 하면 해당 콘텐츠 페이지) 업데이트. 그림 4에 나와 `Default.aspx` 사용 하는 경우는 `Alternate.master` 마스터 페이지입니다.

> [!NOTE]
> 정의 하는 기능을 포함 하는 ASP.NET *테마*합니다. 테마는 이미지, CSS 파일 및 스타일 관련 웹 컨트롤 속성 설정을 런타임 시 페이지에 적용할 수 있는 컬렉션. 테마는 사이트의 레이아웃 및 CSS 규칙을 표시 되는 이미지에만 다른 경우 이동 하는 방법입니다. 레이아웃 등 다양 한 웹 컨트롤을 사용 하거나 전혀 다른 레이아웃을 더 크게 달라 집니다 별도 마스터 페이지를 사용 해야 합니다. 테마에 대 한 자세한 내용은이 자습서의 끝에 추가 정보 섹션을 참조 하세요.


[![콘텐츠 페이지는 새로운 모양과 느낌을 이제 사용할 수 있습니다.](specifying-the-master-page-programmatically-cs/_static/image11.png)](specifying-the-master-page-programmatically-cs/_static/image10.png)

**그림 04**: 콘텐츠 페이지는 새로운 모양과 느낌을 이제 사용할 수 있습니다 ([큰 이미지를 보려면 클릭](specifying-the-master-page-programmatically-cs/_static/image12.png))


마스터 및 콘텐츠 페이지의 태그를 결합 하는 경우는 `MasterPage` 모든 콘텐츠를 확인 하는 클래스 콘텐츠 페이지의 컨트롤에 마스터 페이지의 ContentPlaceHolder를 참조 합니다. 존재 하지 않는 ContentPlaceHolder를 참조 하는 콘텐츠 컨트롤을이 없으면 예외가 throw 됩니다. 즉, 반드시 콘텐츠 페이지에 할당 되는 마스터 페이지에는 ContentPlaceHolder 각 콘텐츠 컨트롤의 콘텐츠 페이지입니다.

`Site.master` 마스터 페이지에는 네 가지 ContentPlaceHolder 컨트롤이 포함 되어 있습니다.:

- `head`
- `MainContent`
- `QuickLoginUI`
- `LeftColumnContent`

하나 또는 두 개만 콘텐츠 컨트롤; 웹 사이트에서 콘텐츠 페이지의 일부 포함 다른 사용 가능한 ContentPlaceHolders의 각 콘텐츠 컨트롤을 포함합니다. 하는 경우 새 마스터 페이지 (`Alternate.master`)에서 ContentPlaceHolders의 모든 콘텐츠 컨트롤에는 이러한 콘텐츠 페이지 적이 할당 될 수 있습니다 `Site.master` 것이 중요는 `Alternate.master` 와같은ContentPlaceHolder컨트롤포함`Site.master`.

가져오려고 하 `Alternate.master` 마스터 페이지 (그림 4 참조) 마이닝의 마스터 페이지의 스타일을 정의 하 여 시작을 비슷하게 보일 수는 `AlternateStyles.css` 스타일 시트입니다. 에 다음 규칙에 추가할 `AlternateStyles.css`:


[!code-css[Main](specifying-the-master-page-programmatically-cs/samples/sample5.css)]

다음으로, 다음 선언적 태그를 추가 `Alternate.master`합니다. 알 수 있듯이 `Alternate.master` 같은 네 가지 ContentPlaceHolder 컨트롤 포함 `ID` 값의 ContentPlaceHolder 컨트롤로 `Site.master`합니다. 또한 ASP.NET AJAX 프레임 워크를 사용 하는 웹 사이트에서 해당 페이지에 필요한 ScriptManager 컨트롤을 포함 합니다.


[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample6.aspx)]

### <a name="testing-the-new-master-page"></a>새 마스터 페이지를 테스트합니다.

이 새 마스터 페이지 업데이트를 테스트 하는 `BasePage` 클래스의 `OnPreInit` 메서드 있도록를 `MasterPageFile` 속성 값이 할당 됩니다 "~ / Alternate.master" 한 후 웹 사이트를 방문 합니다. 모든 페이지는 두 가지를 제외 하 고 오류 없이 작동 해야 합니다. `~/Admin/AddProduct.aspx` 고 `~/Admin/Products.aspx`입니다. 제품의 DetailsView을 추가할 `~/Admin/AddProduct.aspx` 결과 `NullReferenceException` 마스터 페이지의 설정 하려고 시도 하는 코드 줄에서 `GridMessageText` 속성입니다. 방문할 때 `~/Admin/Products.aspx` 는 `InvalidCastException` 메시지를 사용 하 여 페이지 로드 시 throw 됩니다: "종류의 개체를 캐스팅할 수 없습니다. ' ASP.alternate\_마스터 ' 입력 ' ASP.site\_마스터 '."

이러한 오류가 발생할 합니다 `Site.master` 공용 이벤트, 속성 및 메서드에 정의 되어 있지 않은 코드 숨김 클래스에 포함 되어 있습니다 `Alternate.master`합니다. 이러한 두 페이지의 태그 일부를 `@MasterType` 를 참조 하는 지시문의 `Site.master` 마스터 페이지입니다.


[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample7.aspx)]

또한: DetailsView `ItemInserted` 이벤트 처리기 `~/Admin/AddProduct.aspx` 느슨한 형식 캐스팅 하는 코드가 포함 되어 `Page.Master` 형식의 개체에 속성 `Site`합니다. `@MasterType` 지시문 (이러한 방식으로 사용)과의 캐스트는 `ItemInserted` 이벤트 처리기에서 밀접 하 게 결합 합니다 `~/Admin/AddProduct.aspx` 및 `~/Admin/Products.aspx` 페이지를 `Site.master` 마스터 페이지입니다.

있다는 밀접 한 결합이 중단 `Site.master` 고 `Alternate.master` public 멤버에 대 한 정의 포함 하는 공통 기본 클래스에서 파생 합니다. 그런 다음, 업데이트를 `@MasterType` 이 일반적인 기본 형식 참조 지시문입니다.

### <a name="creating-a-custom-base-master-page-class"></a>사용자 지정 기본 마스터 페이지 클래스 만들기

새 클래스 파일을 추가 합니다 `App_Code` 라는 폴더 `BaseMasterPage.cs` 에서 파생 되 게 `System.Web.UI.MasterPage`합니다. 정의 해야 합니다 `RefreshRecentProductsGrid` 메서드 및 `GridMessageText` 속성에서 `BaseMasterPage`를 이동할 수 없습니다. 단순히까지 있습니다 하지만 `Site.master` 이러한 멤버에 관련 된 웹 컨트롤을 사용 하 여 작업 하기 때문에 `Site.master` 마스터 페이지 (합니다 `RecentProducts` GridView 및 `GridMessage` 레이블).

위해 필요한 것은 구성 `BaseMasterPage` 는 이러한 멤버를 정의 되어 있지만를에서 실제로 구현 하는 하는 방식으로 `BaseMasterPage`의 파생 클래스 (`Site.master` 고 `Alternate.master`). 클래스 및 해당 멤버를 표시 하 여이 형식의 상속 가능 `abstract`합니다. 즉, 추가 합니다 `abstract` 키워드 이러한 두 멤버를 발표 하는 `BaseMasterPage` 구현 되지 않은 `RefreshRecentProductsGrid` 및 `GridMessageText`있지만, 해당 파생된 클래스는 합니다.

정의 해야 합니다 `PricesDoubled` 이벤트에 `BaseMasterPage` 이벤트를 발생 시킬 파생된 클래스에서 제공 하는 수단입니다. 이 동작을 용이 하 게.NET Framework에서 사용 되는 패턴은 기본 클래스의 공용 이벤트를 만들고 추가 보호 된 `virtual` 라는 메서드 `OnEventName`합니다. 파생된 클래스에는 다음 이벤트를 발생 시키려면이 메서드를 호출 수 또는 바로 앞 또는 이벤트가 발생 한 후 코드를 실행 하도록 재정의할 수 있습니다.

업데이트 프로그램 `BaseMasterPage` 클래스 다음 코드를 포함 합니다.


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample8.cs)]

다음으로 이동 합니다 `Site.master` 코드 숨김 클래스에서 파생 되 게 및 `BaseMasterPage`합니다. 때문에 `BaseMasterPage` 됩니다 `abstract` 재정의 해야 `abstract` 의 멤버 `Site.master`합니다. 추가 된 `override` 메서드 및 속성 정의에 키워드입니다. 도 발생 하는 코드를 업데이트 합니다 `PricesDoubled` 이벤트에는 `DoublePrice` 단추의 `Click` 기본 클래스에 대 한 호출을 사용 하 여 이벤트 처리기 `OnPricesDoubled` 메서드.

이러한 수정 후의 `Site.master` 코드 숨김 클래스에 다음 코드를 포함 해야 합니다.


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample9.cs)]

또한 업데이트 해야 `Alternate.master`의 코드 숨김 클래스를 파생할 `BaseMasterPage` 시키고 두 `abstract` 멤버입니다. 그러나 `Alternate.master` 최신 제품 또는 새 제품을 한 후 메시지를 표시 하는 레이블이 데이터베이스에 추가 되는 목록, 이러한 메서드 필요 하지 않다는 수행할 GridView를 포함 하지 않습니다.


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample10.cs)]

### <a name="referencing-the-base-master-page-class"></a>기본 마스터 페이지 클래스를 참조

했습니다 했으므로 `BaseMasterPage` 클래스를 확장 하 여 두 마스터 페이지에 있는 마지막 단계는 업데이트를 `~/Admin/AddProduct.aspx` 및 `~/Admin/Products.aspx` 이 공통 형식 참조 페이지. 변경 하 여 시작 된 `@MasterType` 지시문 두 페이지에서:


[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample11.aspx)]

대상:


[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample12.aspx)]

파일 경로 참조 하는 대신 합니다 `@MasterType` 속성의 기본 형식 참조 (`BaseMasterPage`). 따라서 강력한 형식의 `Master` 두 페이지의 코드 숨김 클래스에 사용 되는 속성은 이제 형식의 `BaseMasterPage` (형식 대신 `Site`). 현재 위치에서이 변경 내용을 다시 `~/Admin/Products.aspx`입니다. 이전에이 오류가 발생 한 캐스팅 페이지를 사용 하도록 구성 되어 있으므로 합니다 `Alternate.master` 마스터 페이지 하지만 `@MasterType` 참조 지시문을 `Site.master` 파일. 하지만 오류 없이 페이지를 렌더링 합니다. 왜냐하면 합니다 `Alternate.master` 마스터 페이지 형식의 개체로 캐스팅할 수 `BaseMasterPage` (때문에를 확장 하 고).

수행 해야 하는 한 작은 변경 사항은 `~/Admin/AddProduct.aspx`합니다. DetailsView 컨트롤의 `ItemInserted` 이벤트 처리기에서 모두 강력한 형식의 사용 `Master` 속성과 느슨한 형 `Page.Master` 속성입니다. 업데이트 하는 경우 강력한 형식의 참조를 수정 합니다 `@MasterType` 지시문 했지만 느슨한 형 참조를 업데이트 해야 합니다. 다음 코드 줄을 바꿉니다.


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample13.cs)]

다음으로 캐스팅 `Page.Master` 기본 형식:


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample14.cs)]

## <a name="step-4-determining-what-master-page-to-bind-to-the-content-pages"></a>4 단계: 콘텐츠 페이지를 바인딩할 마스터 페이지를 확인합니다.

우리의 `BasePage` 클래스에는 현재 모든 콘텐츠 페이지의 설정 `MasterPageFile` 페이지 수명 주기의 PreInit 단계에서 하드 코드 된 값으로 속성입니다. 일부 외부 요인에 마스터 페이지를 기반으로이 코드를 업데이트할 수 있습니다. 아마도 마스터 페이지를 로드 현재 로그온된 한 사용자의 기본 설정에 따라 달라 집니다. 이 경우에 코드를 작성 해야 합니다 `OnPreInit` 의 메서드 `BasePage` 현재 방문한 사용자의 마스터 페이지를 기본 조회 하는 합니다.

사용자를 사용 하는 마스터 페이지를 선택할 수 있도록 웹 페이지를 만들어 보겠습니다 `Site.master` 또는 `Alternate.master` -세션 변수에이 선택 항목을 저장 합니다. 명명 된 루트 디렉터리에 새 웹 페이지를 만들어 시작 `ChooseMasterPage.aspx`합니다. 이 페이지 (또는 다른 콘텐츠 페이지 예측이)를 만들 때 마스터 페이지 프로그래밍 방식으로 설정 되어 있으므로 마스터 페이지에 바인딩할 필요가 없습니다 `BasePage`합니다. 그러나 마스터 페이지에 새 페이지에 연결 하지 않으면 하는 경우 다음 새 페이지의 기본 선언적 태그에 Web Form 및 마스터 페이지에서 제공 하는 다른 콘텐츠 적절 한 콘텐츠 컨트롤을 사용 하 여이 태그를 수동으로 교체 해야 합니다. 이러한 이유로 필자 쉽게 마스터 페이지에 새 ASP.NET 페이지를 바인딩할 수 있습니다.

> [!NOTE]
> 때문에 `Site.master` 고 `Alternate.master` 동일한 설정한 ContentPlaceHolder 컨트롤의 새 콘텐츠 페이지를 만들 때 선택한 마스터 페이지는 중요 하지 않습니다. 일관성을 위해 것이 좋습니다를 사용 하 여 `Site.master`입니다.


[![웹 사이트에 새 콘텐츠 페이지를 추가 합니다.](specifying-the-master-page-programmatically-cs/_static/image14.png)](specifying-the-master-page-programmatically-cs/_static/image13.png)

**그림 05**: 웹 사이트에 새 콘텐츠 페이지 추가 ([큰 이미지를 보려면 클릭](specifying-the-master-page-programmatically-cs/_static/image15.png))


업데이트 된 `Web.sitemap` 이 단원에 대 한 항목을 포함 하는 파일입니다. 아래에 다음 태그를 추가 합니다 `<siteMapNode>` 마스터 페이지 및 ASP.NET AJAX 단원:


[!code-xml[Main](specifying-the-master-page-programmatically-cs/samples/sample15.xml)]

모든 콘텐츠를 추가 하기 전에 합니다 `ChooseMasterPage.aspx` 페이지에서 파생 되도록 페이지의 코드 숨김 클래스를 업데이트 하려면 잠시 `BasePage` (대신 `System.Web.UI.Page`). 다음으로, DropDownList 컨트롤이 페이지에 추가 하 여 설정 합니다 해당 `ID` 속성을 `MasterPageChoice`를 사용 하 여 두 ListItems 추가 `Text` 값 "~ / Site.master" 및 "~ / Alternate.master"입니다.

페이지에 단추 웹 컨트롤을 추가 하 고 설정 해당 `ID` 하 고 `Text` 속성을 `SaveLayout` "저장 레이아웃 선택", 각각. 이 시점에서 페이지의 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample16.aspx)]

해당 페이지를 처음으로 방문 하는 경우 사용자의 현재 선택 된 마스터 페이지 선택 표시 해야 합니다. 만들기는 `Page_Load` 이벤트 처리기 다음 코드를 추가 합니다.


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample17.cs)]

위의 코드는 첫 번째 페이지 방문에만 (및 후속 포스트백에 없는)를 실행합니다. 먼저 확인 하는 경우 세션 변수 `MyMasterPage` 존재 합니다. 이 경우에 일치 하는 ListItem를 찾으려고 시도 합니다 `MasterPageChoice` DropDownList 합니다. 일치 하는 ListItem가 있으면 해당 `Selected` 속성이 `true`합니다.

해야 사용자가 선택한에 저장 하는 코드는 `MyMasterPage` 세션 변수입니다. 이벤트 처리기를 만듭니다는 `SaveLayout` 단추의 `Click` 이벤트 다음 코드를 추가 합니다.


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample18.cs)]

> [!NOTE]
> 시간을 `Click` 포스트백 될 때 이벤트 처리기가 실행, 마스터 페이지 이미 선택 되었습니다. 따라서 다음 페이지를 방문 될 때까지 사용자가 드롭다운 목록에서 선택한 적용 되지 않습니다. 합니다 `Response.Redirect` 다시 요청 하려면 브라우저를 강제로 `ChooseMasterPage.aspx`입니다.


사용 하 여는 `ChooseMasterPage.aspx` 하도록 페이지 전체에서 마지막 작업은 `BasePage` 할당 합니다 `MasterPageFile` 속성의 값에 따라는 `MyMasterPage` 세션 변수. 세션 변수 설정 하지 않은 경우 `BasePage` 기본적으로 `Site.master`입니다.


[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample19.cs)]

> [!NOTE]
> 할당 하는 코드를 이동 합니다 `Page` 개체의 `MasterPageFile` 개 속성은 `OnPreInit` 이벤트 처리기 및 두 개의 별도 메서드로 합니다. 이 첫 번째 메서드인 `SetMasterPageFile`를 할당 합니다 `MasterPageFile` 속성 두 번째 메서드에 의해 반환 되는 값을 `GetMasterPageFileFromSession`입니다. 필자는 `SetMasterPageFile` 메서드 `virtual` 를 확장 하는 향후 클래스 `BasePage` 필요한 경우 사용자 지정 논리를 구현 하도록 재정의할 필요에 따라 수 있습니다. 재정의 하는 예제를 살펴보겠습니다 `BasePage`의 `SetMasterPageFile` 다음 자습서에서는 속성입니다.


이 코드를 사용 하 여 방문을 `ChooseMasterPage.aspx` 페이지입니다. 처음에 `Site.master` 마스터 페이지 선택된 (그림 6 참조), 이지만 사용자 드롭다운 목록에서 다른 마스터 페이지를 선택할 수 있습니다.


[![콘텐츠 페이지 Site.master 마스터 페이지를 사용 하 여 표시 됩니다.](specifying-the-master-page-programmatically-cs/_static/image17.png)](specifying-the-master-page-programmatically-cs/_static/image16.png)

**그림 06**: 콘텐츠 페이지를 사용 하 여 표시 합니다 `Site.master` 마스터 페이지 ([클릭 하 여 큰 이미지 보기](specifying-the-master-page-programmatically-cs/_static/image18.png))


[![콘텐츠 페이지 Alternate.master 마스터 페이지를 사용 하 여 표시 됩니다.](specifying-the-master-page-programmatically-cs/_static/image20.png)](specifying-the-master-page-programmatically-cs/_static/image19.png)

**그림 07**: 콘텐츠 페이지는 이제 표시 된 `Alternate.master` 마스터 페이지 ([클릭 하 여 큰 이미지 보기](specifying-the-master-page-programmatically-cs/_static/image21.png))


## <a name="summary"></a>요약

콘텐츠 페이지를 방문할 때 해당 콘텐츠는 해당 마스터 페이지의 ContentPlaceHolder 컨트롤로 결합 합니다. 콘텐츠 페이지의 마스터 페이지가으로 표시 되는 `Page` 클래스의 `MasterPageFile` 속성에 할당 되는 `@Page` 지시문의 `MasterPageFile` 초기화 단계는 특성입니다. 표시 값을 할당할 수 있습니다이 자습서와는 `MasterPageFile` 속성 PreInit 단계 종료 되기 전에 이렇게 하기만 합니다. 프로그래밍 방식으로 마스터 페이지를 지정할 수 있는 외부 요인에 따라 마스터 페이지에 콘텐츠 페이지를 동적으로 바인딩 같은 보다 고급 시나리오에 노출 합니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 페이지 수명 주기 다이어그램](http://emanish.googlepages.com/Asp.Net2.0Lifecycle.PNG)
- [ASP.NET 페이지 수명 주기 개요](https://msdn.microsoft.com/library/ms178472.aspx)
- [ASP.NET 테마 및 스킨 개요](https://msdn.microsoft.com/library/ykzx33wh.aspx)
- [마스터 페이지: 팁, 요령 및 트랩](http://www.odetocode.com/articles/450.aspx)
- [ASP.NET의 테마](http://www.odetocode.com/articles/423.aspx)

### <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 작성자의 여러 ASP/ASP.NET 서적과 4GuysFromRolla.com의 설립자 이며, 왔습니다 Microsoft 웹 기술을 1998 합니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 3.5 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)합니다. Scott에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com) 통하거나 저자의 블로그 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Suchi Banerjee 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](master-pages-and-asp-net-ajax-cs.md)
> [다음](nested-master-pages-cs.md)
