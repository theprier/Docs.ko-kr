---
uid: web-forms/overview/older-versions-getting-started/master-pages/specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb
title: 마스터 페이지 (VB)에서 제목, 메타 태그 및 다른 HTML 헤더를 지정 하 | Microsoft Docs
author: rick-anderson
description: 다양 한 정의 하기 위한 다양 한 기술을 살펴봅니다 &lt;h e a d&gt; 콘텐츠 페이지의 마스터 페이지에 있는 요소입니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/21/2008
ms.topic: article
ms.assetid: ea8196f5-039d-43ec-8447-8997ad4d3900
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb
msc.type: authoredcontent
ms.openlocfilehash: b8bf9d32eee3e35ffc84521f7f82f7beecc99a0c
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb"></a>마스터 페이지 (VB)에서 제목, 메타 태그 및 다른 HTML 헤더 지정
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_03_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_03_VB.pdf)

> 다양 한 정의 하기 위한 다양 한 기술을 살펴봅니다 &lt;h e a d&gt; 콘텐츠 페이지의 마스터 페이지에 있는 요소입니다.


## <a name="introduction"></a>소개

Visual Studio 2008에서 만든 새 마스터 페이지가 기본적으로 두 개의 ContentPlaceHolder 컨트롤: 이름이 각각 `head`에서 `<head>` 요소로 및 명명 된 이름을 `ContentPlaceHolder1`, 웹 폼 내에 배치 합니다. 목적은 `ContentPlaceHolder1` 에서 페이지 단위로 지정할 수 있는 웹 폼의 영역을 정의 하는 것입니다. `head` ContentPlaceHolder 사용자 지정 콘텐츠를 추가할 페이지를 사용 하면는 `<head>` 섹션. (물론, 이러한 두 contentplaceholders의 수정 하거나 제거 하 고, 수 및 추가 ContentPlaceHolder 마스터 페이지에 추가할 수 있습니다. 가격 마스터 페이지 `Site.master`, 현재 4 개의 ContentPlaceHolder 제어 기능을 포함 합니다.)

HTML `<head>` 요소는 문서 자체의 포함 되지 않은 웹 페이지 문서에 대 한 정보에 대 한 리포지토리로 사용 됩니다. 웹 페이지의 직함 등의 정보가 포함 됩니다, 그리고 파일 검색 엔진 또는 내부 크롤러 및 RSS 피드, JavaScript 및 CSS와 같은 외부 리소스에 대 한 링크에서 메타 정보 사용 합니다. 이 정보 중 일부는 웹 사이트의 모든 페이지에 적절 한 수 있습니다. 예를 들어 다음 모든 ASP.NET 페이지에 대 한 JavaScript 파일 및 동일한 CSS 규칙을 전역적으로 가져올는 것이 좋습니다. 그러나 부분이 있습니다.는 `<head>` 요소는 페이지 마다입니다. 페이지 제목은 가장 대표적인 예입니다.

이 자습서에서는 전역 및 관련 페이지를 정의 하는 방법을 살펴 `<head>` 마스터 페이지와 해당 콘텐츠 페이지에서 섹션 태그입니다.

## <a name="examining-the-master-pagesheadsection"></a>마스터 페이지의 검사`<head>`섹션

Visual Studio 2008에서 만든 기본 마스터 페이지 파일에 다음 태그를 포함 합니다. 해당 `<head>` 섹션:


[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample1.aspx)]

다음에 유의 `<head>` 요소를 포함 한 `runat="server"` 특성에 서버 컨트롤 (HTML이 아닌 정적) 임을 나타냅니다. 파생 되는 모든 ASP.NET 페이지의 [ `Page` 클래스](https://msdn.microsoft.com/library/system.web.ui.page.aspx)에 있는 `System.Web.UI` 네임 스페이스입니다. 이 클래스를 포함 한 [ `Header` 속성](https://msdn.microsoft.com/library/system.web.ui.page.header.aspx) 페이지의에 대 한 액세스를 제공 하는 `<head>` 영역입니다. 사용 하 여 `Header` 속성에는 렌더링 된 추가 태그를 추가 하거나 ASP.NET 페이지의 제목을 설정할 수 `<head>` 섹션. 가능한 경우, 콘텐츠 페이지의 사용자 지정 하려면 `<head>` 페이지의 약간의 코드를 작성 하 여 요소 `Page_Load` 이벤트 처리기입니다. 1 단계에서에서 페이지의 제목을 프로그래밍 방식으로 설정 하는 방법을 알아봅니다.

에 표시 된 태그는 `<head>` 위 요소에는 또한 라는 ContentPlaceHolder 컨트롤 포함 `head`합니다. 콘텐츠 페이지 사용자 지정 콘텐츠를 추가할 수 있습니다이 ContentPlaceHolder 컨트롤은 필요 하지는 `<head>` 요소 프로그래밍 방식으로 합니다. 그러나 콘텐츠 페이지 프로그램이 정적 태그를 추가 해야 하는 경우에에서 도움이 될 수는 `<head>` 요소 태그를 정적으로 해당 하는 콘텐츠 컨트롤을 하지 않고 프로그래밍 방식으로 선언적으로 추가할 수 있습니다.

이외에 `<title>` 요소 및 `head` ContentPlaceHolder, 마스터 페이지의 `<head>` 요소 하나 포함 되어야 `<head>`-모든 페이지에 공통적으로 적용 되는 수준 태그입니다. 이 웹 사이트에서 모든 페이지에 정의 된 CSS 규칙을 사용는 `Styles.css` 파일입니다. 업데이트 했습니다. 따라서는 `<head>` 요소에는 [ *마스터 페이지를 사용 하 여 사이트 전체 레이아웃 만들기* ](creating-a-site-wide-layout-using-master-pages-vb.md) 해당 포함 하도록 자습서 `<link>` 요소입니다. 우리의 `Site.master` 마스터 페이지의 현재 `<head>` 태그는 다음과 같습니다.


[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample2.aspx)]

## <a name="step-1-setting-a-content-pages-title"></a>1 단계: 콘텐츠 페이지의 제목 설정

웹 페이지의 제목을 통해 지정 됩니다는 `<title>` 요소입니다. 각 페이지의 제목은 적절 한 값으로 설정 하는 것이 유용 합니다. 페이지를 방문 하는 경우 브라우저의 제목 표시줄에 제목 표시 됩니다. 또한 페이지 책갈피를 설정 하는 경우 브라우저 페이지의 제목을 책갈피에 대 한 제안된 된 이름으로 사용 합니다. 또한 대부분의 검색 엔진 검색 결과 표시 하는 경우 페이지의 제목을 표시 합니다.

> [!NOTE]
> 기본적으로 Visual Studio 설정에서 `<title>` "제목 없음 페이지"로 마스터 페이지의 요소입니다. 마찬가지로, 새 ASP.NET 페이지 있어야 해당 `<title>` 너무 "제목 없음 페이지"로 설정 합니다. 페이지의 제목은 적절 한 값으로 설정를 잊기 쉬울 수 있기 때문에 여러 페이지 제목 "제목 없음 페이지"를 사용 하 여 인터넷에는 있습니다. Google이 제목의 웹 페이지 검색 대략 2,460,000 결과가 반환 됩니다. 에 Microsoft는 "제목 없음 페이지" 라는 이름의 게시 웹 페이지에 취약 합니다. 이 문서 작성 당시의 Google 검색 Microsoft.com 도메인에서 이러한이 236 웹 페이지를 보고 합니다.


ASP.NET 페이지에는 다음 방법 중 하나에 해당 제목을 지정할 수 있습니다.:

- 내에서 직접 값을 배치 하 여는 `<title>` 요소
- 사용 하 여 `Title` 특성에 `<%@ Page %>` 지시문
- 프로그래밍 방식으로 페이지의 설정 `Title` 같은 코드를 사용 하 여 속성 `Page.Title="title"` 또는 `Page.Header.Title="title"`합니다.

페이지 없는 콘텐츠는 `<title>` 요소가 마스터 페이지에 정의 되어 있습니다. 따라서 콘텐츠 페이지의 제목을 설정 하려면 사용할 수 있습니다는 `<%@ Page %>` 지시문의 `Title` 특성 또는 프로그래밍 방식으로 설정 합니다.

### <a name="setting-the-pages-title-declaratively"></a>선언적으로 페이지의 제목 설정

콘텐츠 페이지의 제목을 통해 선언적으로 설정할 수는 `Title` 특성에는 [ `<%@ Page %>` 지시문](https://msdn.microsoft.com/library/ydy4x04a.aspx)합니다. 이 속성을 직접 수정 하 여 설정할 수 있습니다는 `<%@ Page %>` 지시문 또는 속성 창을 통해 합니다. 두 방법 모두를 살펴보겠습니다.

소스 뷰에서 찾습니다는 `<%@ Page %>` 는 페이지의 선언적 태그의 위쪽에 있는 지시문입니다. `<%@ Page %>` 에 대 한 지시문 `Default.aspx` 따릅니다.


[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample3.aspx)]

`<%@ Page %>` 지시문 구문 분석 하 고 페이지를 컴파일할 때 ASP.NET 엔진에 의해 사용 되는 페이지별 특성을 지정 합니다. 마스터 페이지 파일, 해당 코드 파일 및 기타 정보 중에서 제목을의 위치에이 포함 됩니다.

Visual Studio 설정 새 콘텐츠 페이지를 만들 때 기본적으로는 `Title` 특성을 "제목 없음 페이지"입니다. 변경 `Default.aspx`의 `Title` "제목 없음 페이지"에서 특성 "마스터 페이지 자습서"을 선택한 다음 브라우저를 통해 페이지를 봅니다. 그림 1에서는 새 페이지 제목이 반영 하는 브라우저의 제목 표시줄을 보여 줍니다.


![브라우저의 제목 표시줄에 이제 표시 &quot;마스터 페이지 자습서&quot; 대신 &quot;제목 없음된 페이지&quot;](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image1.png)

**그림 01**: 브라우저의 제목 표시줄에 이제 "제목 없음된 페이지" 대신 "마스터 페이지 자습서" 표시


페이지의 제목 속성 창에서 설정할 수도 있습니다. 속성 창에서 문서 드롭 다운 목록에서 부하 페이지 수준 속성을 포함 하는 선택 된 `Title` 속성입니다. 그림 2 후 속성 창 표시 되어 `Title` "마스터 페이지 자습서"으로 설정 되었습니다.


![속성 창에서 제목이 너무 구성할 수 있습니다.](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image2.png)

**그림 02**: 너무 제목 속성 창에서 구성할 수 있습니다


### <a name="setting-the-pages-title-programmatically"></a>프로그래밍 방식으로 페이지의 제목 설정

마스터 페이지의 `<head runat="server">` 태그로 변환 되는 [ `HtmlHead` 클래스](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlhead.aspx) 페이지가 ASP.NET 엔진에서 렌더링 될 때 인스턴스. `HtmlHead` 클래스에는 [ `Title` 속성](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlhead.title.aspx) 해당 값은 반영에 렌더링 된 `<title>` 요소입니다. 이 속성은 ASP.NET 페이지의 코드 숨김 클래스를 통해에서 액세스할 수 있는 `Page.Header.Title`;이 같은 속성을 통해 액세스할 수도 `Page.Title`합니다.

페이지의 제목을 프로그래밍 방식으로 설정 하는 것이 좋습니다.로 이동 하는 `About.aspx` 페이지의 코드 숨김 페이지의에 대 한 이벤트 처리기를 만들고 클래스 `Load` 이벤트입니다. 그런 다음, 페이지의 제목을 설정 "마스터 페이지 자습서::에 대 한:: *날짜*" 여기서 *날짜* 은 현재 날짜입니다. 이 코드를 추가한 후에 `Page_Load` 이벤트 처리기는 다음과 비슷해야 합니다.


[!code-vb[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample4.vb)]

그림 3을 방문할 때 브라우저의 제목 표시줄에 표시 된 `About.aspx` 페이지.


![페이지의 제목 프로그래밍 방식으로 설정 되 고 현재 날짜를 포함](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image3.png)

**그림 03**: The 페이지의 제목 프로그래밍 방식으로 설정 되 고 현재 날짜를 포함


## <a name="step-2-automatically-assigning-a-page-title"></a>2 단계: 페이지 제목을 자동으로 할당

1 단계에서에서 설명한 것 처럼 페이지의 제목 선언적으로 또는 프로그래밍 방식으로 설정할 수 있습니다. 그러나 명시적으로 변경 하기 쉬운 제목을 기억나지 않는 경우 페이지는가 기본 제목 "제목 없음 페이지"입니다. 이상적으로 페이지의 제목은 자동으로 설정을 수행해 줍니다 명시 하지 않고 명시적으로 해당 값을 합니다. 예를 들어 런타임 시 페이지의 제목은 "제목 없음 페이지", 경우에 제목이 ASP.NET 페이지의 파일 이름으로 동일 하 게 자동으로 업데이트 하는 것이 좋습니다. 다행 스럽게도 사용 하면 약간의 선행 작업이 있어야 자동으로 할당 된 제목 수입니다.

파생 되는 모든 ASP.NET 웹 페이지는 `Page` System.Web.UI 네임 스페이스의 클래스입니다. `Page` 클래스는 ASP.NET 페이지에서 필요한 최소한의 기능을 정의 하며, 같은 필수 속성을 노출 `IsPostBack`, `IsValid`, `Request`, 및 `Response`, 다양 한 기타. 종종 웹 응용 프로그램의 모든 페이지는 추가 기능 또는 기능에 필요합니다. 일반적으로이 제공 하는 기본 페이지를 사용자 지정 클래스를 만드는 것입니다. 기본 페이지를 사용자 지정 클래스에서 파생 되는 클래스를 만들면는 `Page` 클래스 및 추가 기능을 포함 합니다. 이 기본 클래스를 만든 후에 여기에서 파생 되는 ASP.NET 페이지에 있을 수 있습니다 (보다는 `Page` 클래스)에서 ASP.NET 페이지에는 확장 된 기능을 제공 합니다.

이 단계에서는 제목을 그렇지 않으면 명시적으로 설정 하지 않은 경우 ASP.NET 페이지의 파일 이름에는 페이지의 제목을 자동으로 설정 하는 기본 페이지를 만듭니다. 3 단계 확인 사이트 맵을 기반으로 하는 페이지의 제목을 설정 합니다.

> [!NOTE]
> 만들고 기본 페이지를 사용자 지정 클래스를 사용 하는 철저 한 검사가 자습서 시리즈의 범위를 벗어납니다. 자세한 내용은 [Your ASP.NET 페이지의 코드 숨김 클래스에 대 한 사용자 지정 기본 클래스를 사용 하 여](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)합니다.


### <a name="creating-the-base-page-class"></a>기본 페이지 클래스 만들기

이 첫 번째 작업은 한 기본 페이지 클래스를 확장 하는 클래스를 만드는 것은 `Page` 클래스입니다. 추가 하 여 시작 된 `App_Code` 폴더를 프로젝트, 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고, ASP.NET 폴더 추가 선택 하 고, 다음을 선택 하 여 `App_Code`합니다. 그런 다음 마우스 오른쪽 단추로 클릭는 `App_Code` 폴더 라는 새 클래스를 추가 하 고 `BasePage.vb`합니다. 그림 4 후 솔루션 탐색기에 표시 된 `App_Code` 폴더 및 `BasePage.vb` 클래스가 추가 되었습니다.


![App_Code 폴더와 BasePage 라는 클래스를 추가 합니다.](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image4.png)

**그림 04**: 추가 된 `App_Code` 폴더와 라는 클래스 `BasePage`


> [!NOTE]
> Visual Studio 프로젝트 관리의 두 모드를 지원: 웹 사이트 프로젝트와 웹 응용 프로그램 프로젝트입니다. `App_Code` 폴더 웹 사이트 프로젝트 모델에 사용할 수 있도록 디자인 되었습니다. 웹 응용 프로그램 프로젝트 모델을 사용 하는 경우 배치의 `BasePage.vb` 아닌 다른 이름의 폴더의 클래스 `App_Code`와 같은 `Classes`합니다. 이 항목에 대 한 자세한 내용은 참조 [웹 응용 프로그램 프로젝트에 웹 사이트 프로젝트를 마이그레이션하](http://webproject.scottgu.com/VisualBasic/Migration2/Migration2.aspx)합니다.


확장 하는 데 필요한 사용자 지정 기본 페이지가 ASP.NET 페이지의 코드 숨김 클래스에 대 한 기본 클래스로 사용, 때문에 `Page` 클래스입니다.


[!code-vb[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample5.vb)]

ASP.NET 페이지를 요청할 때마다 일련의 단계를 HTML로 렌더링 되 고 요청된 된 페이지의 정점 진행 됩니다. 재정의 하 여 단계를 활용할 수 있습니다는 `Page` 클래스의 `OnEvent` 메서드. 이 자료에 대 한 페이지 보겠습니다 것에 지정 하지 않으면 명시적으로 하 여 제목을 자동으로 설정는 `LoadComplete` 단계 (을 짐작할 수 후에 발생는 `Load` 단계).

이를 위해 재정의 `OnLoadComplete` 메서드 다음 코드를 입력 합니다.


[!code-vb[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample6.vb)]

`OnLoadComplete` 메서드를 확인 하 여 시작 된 `Title` 속성 아직 명시적으로 설정 되지 않았습니다. 경우는 `Title` 속성은 `Nothing`, 빈 문자열을 "제목 없음 페이지" 값이 요청된 된 ASP.NET 페이지의 파일 이름에 할당 됩니다. 실제 경로 요청된 하는 ASP.NET 페이지- `C:\MySites\Tutorial03\Login.aspx`, 예를 들어-는 통해 액세스할 수는 `Request.PhysicalPath` 속성입니다. `Path.GetFileNameWithoutExtension` 메서드를 사용 하는 파일 이름 부분만 추출 하 고이 filename에 할당 됩니다는 `Page.Title` 속성입니다.

> [!NOTE]
> 지금부터 타이틀의 형식 개선 하기 위해이 논리를 강화 합니다. 예를 들어, 페이지의 파일 이름이 `Company-Products.aspx`, 위의 코드에서 제목이 "회사-Products"를 생성 하지만 "회사 제품"와 같이 공백으로 대시는 대체 하는 것이 가장 좋습니다. 또한 대/소문자 변경 될 때마다 공간을 추가 하는 것이 좋습니다. 즉, 파일 이름 변환 하는 코드 추가 고려 `OurBusinessHours.aspx` 의 Our "업무 시간" 제목입니다.


### <a name="having-the-content-pages-inherit-the-base-page-class"></a>콘텐츠 페이지를 기본 Page 클래스를 상속 합니다.

이제 사용자 지정 기본 페이지에서 파생 하는 사이트의 ASP.NET 페이지를 업데이트 해야 (`BasePage`) 대신는 `Page` 클래스입니다. 수행 각 코드 숨김 클래스이 이동에서 클래스 선언을 변경:


[!code-vb[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample7.vb)]

대상:


[!code-vb[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample8.vb)]

이렇게 한 다음 브라우저를 통해 사이트를 방문 합니다. 제목이 명시적으로 설정 되어와 같은 페이지를 방문 하는 경우 `Default.aspx` 또는 `About.aspx`, 명시적으로 지정 된 제목이 사용 됩니다. 그러나 해당 제목 ("제목 없음 페이지") 기본값에서 변경 되지 않은 페이지를 방문 하면 하는 경우 기본 페이지 클래스는 페이지의 파일 이름에 제목을 설정 합니다.

그림 5는 `MultipleContentPlaceHolders.aspx` 브라우저를 통해 볼 때 페이지입니다. 제목 (낮은 확장명) 페이지의 파일 이름을 정확 하 게는 "MultipleContentPlaceHolders"입니다.


[![제목을 이면 명시적으로 지정 되지 페이지의 파일 이름이 자동으로 사용](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image6.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image5.png)

**그림 05**: 제목을 이면 명시적으로 지정 되지 페이지의 파일 이름이 자동으로 사용 ([전체 크기 이미지를 보려면 클릭](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image7.png))


## <a name="step-3-basing-the-page-title-on-the-site-map"></a>3 단계: 사이트 맵 페이지 제목을 기준

ASP.NET은 페이지 개발자가 웹 컨트롤 (예: SiteMapPath, 사이트 맵에 대 한 정보를 표시 하기 위한 함께 외부 리소스 (예: XML 파일이 나 데이터베이스 테이블)에서 계층적 사이트 맵 정의 하는 강력한 사이트 맵 프레임 워크를 제공 메뉴 및 TreeView 컨트롤이)입니다.

사이트 맵 구조는 ASP.NET 페이지의 코드 숨김 클래스에서 프로그래밍 방식으로 액세스할 수도 있습니다. 이런이 방식으로 사이트 맵에서 해당 노드의의 제목에는 페이지의 제목을 설정할 자동으로 수 있습니다. 보겠습니다 향상 된 `BasePage` 2 단계에서에서 만든이 기능을 제공 하는 클래스입니다. 하지만 사이트에 대 한 사이트 맵을 만들려면 먼저 다음 해야 합니다.

> [!NOTE]
> 이 자습서에서는 독자가 가정 이미 ASP에 잘 알고 있습니다. NET의 사이트 맵 기능입니다. 사이트 맵 사용에 대 한 자세한 내용은 내 여러 부분으로 구성 문서 시리즈를 참조 하십시오. [ASP 검사 합니다. NET의 사이트 탐색](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)합니다.


### <a name="creating-the-site-map"></a>사이트 맵 만들기

사이트 맵 시스템 위에 빌드된는 [공급자 모델](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx), 영구 저장소와 메모리 간의 사이트 맵 정보 또는 그 반대로 serialize 하는 논리에서 사이트 맵 API를 분리 하는 합니다. .NET Framework와 함께 제공 되는 [ `XmlSiteMapProvider` 클래스](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx), 기본 사이트 맵 공급자 변수인 합니다. 이름에서 알 수 있듯이 `XmlSiteMapProvider` 사이트 맵 저장소로 XML 파일을 사용 합니다. 이 사이트 맵을 정의 하기 위한이 공급자를 사용 하겠습니다.

웹 사이트의 루트 폴더에 사이트 맵 파일을 만들어 시작 `Web.sitemap`합니다. 이렇게 하려면 솔루션 탐색기에서 웹 사이트 이름을 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가 사이트 맵 템플릿을 선택 합니다. 파일의 이름은 확인 `Web.sitemap` 추가를 클릭 합니다.


[![웹 사이트의 루트 폴더에 Web.sitemap 라는 파일](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image9.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image8.png)

**그림 06**: 라는 파일 추가 `Web.sitemap` 웹 사이트의 루트 폴더 ([전체 크기 이미지를 보려면 클릭](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image10.png))


다음 XML을 추가 하는 `Web.sitemap` 파일:


[!code-xml[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample9.xml)]

이 XML 그림 7에 표시 되는 계층적 사이트 맵 구조를 정의 합니다.


![사이트 맵은 현재 구성의 세 가지 사이트 맵 노드](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image11.png)

**그림 07**: The 사이트 맵은 현재 구성의 세 가지 사이트 맵 노드


새 예제를 추가 하는 대로 사이트 맵 구조 이후 자습서에서 업데이트 됩니다.

### <a name="updating-the-master-page-to-include-navigation-web-controls"></a>마스터 페이지 탐색 웹 컨트롤을 포함 하도록 업데이트

이제 사이트 맵을 정의 했으므로 탐색 웹 컨트롤을 포함 하도록 마스터 페이지를 업데이트 해 보겠습니다. 특히,는 순서가 지정 되지 않은 목록을 사이트 맵에서 정의 된 각 노드에 대 한 목록 항목을 렌더링 하는 단원 섹션의 왼쪽된 열에 추가할 ListView 컨트롤 보겠습니다.

> [!NOTE]
> ListView 컨트롤을 ASP.NET 3.5 버전 새로운 기능입니다. 이전 버전의 ASP.NET 사용 하는 경우 반복기 컨트롤을 대신 사용 합니다. ListView 컨트롤에 대 한 자세한 내용은 참조 하십시오. [를 사용 하 여 ASP.NET 3.5의 ListView 및 DataPager 컨트롤](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)합니다.


단원 섹션에서 기존 순서가 지정 되지 않은 목록 태그를 제거 하 여 시작 합니다. 다음으로 도구 상자에서 ListView 컨트롤을 끌어 놓습니다 단원을 아래에 있는 머리글입니다. 다른 보기 컨트롤 함께 도구 상자의 데이터 섹션에 있는 ListView: GridView, DetailsView, 및 FormView 합니다. ListView의 설정 `ID` 속성을 `LessonsList`합니다.

데이터 소스 구성 마법사에서 ListView 라는 새 SiteMapDataSource 컨트롤에 바인딩할 선택 `LessonsDataSource`합니다. SiteMapDataSource 컨트롤 사이트 맵 시스템에서 계층 구조를 반환합니다.


[![LessonsList ListView 컨트롤에 SiteMapDataSource 컨트롤 바인딩](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image13.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image12.png)

**그림 08**: SiteMapDataSource 컨트롤 LessonsList ListView 컨트롤을 바인딩할 ([전체 크기 이미지를 보려면 클릭](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image14.png))


SiteMapDataSource 컨트롤을 만든 후에 순서가 지정 되지 않은 목록 SiteMapDataSource 컨트롤에 의해 반환 된 각 노드에 대 한 목록 항목으로 렌더링 되도록 ListView의 템플릿 정의 해야 합니다. 서식 파일에 다음 태그를 사용 하 여 수행할 수 있습니다.


[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample10.aspx)]

`LayoutTemplate` 순서가 지정 되지 않은 목록에 대 한 태그를 생성 (`<ul>...</ul>`) 동안는 `ItemTemplate` 목록 항목으로 SiteMapDataSource에서 반환 된 각 항목 렌더링 (`<li>`) 특정 단원에 대 한 링크를 포함 하 합니다.

ListView의 서식 파일을 구성한 후의 웹 사이트를 방문 합니다. 그림 9에서 볼 수 있듯이 단일 글머리 기호 항목 홈 단원 섹션에 포함 합니다. 정보 및 여러 ContentPlaceHolder 컨트롤 단원을 사용 하 여 어디 입니까? 데이터의 계층적 집합을 반환 하는 SiteMapDataSource 만들어졌지만 ListView 컨트롤에는 단일 수준 계층으로 표시할 수 있습니다. 따라서 첫 번째 사이트 맵 노드는 SiteMapDataSource 반환한 수준의 표시 됩니다.


[![단원 섹션에는 포함 된 단일 목록 항목](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image16.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image15.png)

**그림 09**: 단원 섹션에는 포함 된 단일 목록 항목 ([전체 크기 이미지를 보려면 클릭](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image17.png))


여러 수준을 표시 하려면 우리 중첩 시킬 수 내에서 여러 Listview에서 `ItemTemplate`합니다. 이 기술은에서 검사 된는 [ *마스터 페이지 및 사이트 탐색* 자습서](../../data-access/introduction/master-pages-and-site-navigation-vb.md) 의 내 [데이터 자습서 시리즈 작업](../../data-access/index.md)합니다. 그러나이 자습서 시리즈에 대 한 우리의 사이트 맵 포함 됩니다는 두 수준 방금: 홈 (최상위 수준); 및 홈의 자식으로 각 단원입니다. 중첩 된 ListView를 만들어 대신 수 대신 하도록 지시를 설정 하 여 시작 노드를 반환 하지 SiteMapDataSource 해당 [ `ShowStartingNode` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemapdatasource.showstartingnode.aspx) 를 `False`합니다. 한 순수 효과 SiteMapDataSource 사이트 맵 노드의 두 번째 계층을 반환 하 여 시작 하는 합니다.

이러한 변경으로 인해 ListView 정보에 대 한 글머리 기호 항목만 표시 되며 여러 ContentPlaceHolder 컨트롤 사용 하 여 학습 과정을 하지만 홈에 대 한 글머리 기호 항목을 생략 합니다. 이 해결 하려면 추가할 수 있습니다 명시적으로 글머리 기호 항목의 홈에 대 한는 `LayoutTemplate`:


[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample11.aspx)]

구성 시작 노드를 생략 하려면 SiteMapDataSource 명시적으로 홈 글머리 기호 항목을 추가 하는 여 이제 단원 섹션 원하는 출력에 표시 됩니다.


[![홈 및 각 자식 노드에 대 한 글머리 기호 항목을 포함 하는 단원 섹션](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image19.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image18.png)

**그림 10**: Home 및 각 자식 노드 용 글머리 기호 항목을 포함 하는 단원 섹션 ([전체 크기 이미지를 보려면 클릭](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image20.png))


### <a name="setting-the-title-based-on-the-site-map"></a>사이트 맵에 따라 제목 설정

현재 위치에서 사이트 맵을 업데이트 하면 다음과 같이 우리의 `BasePage` 사이트 맵에서 지정 된 제목을 사용 하는 클래스입니다. 2 단계에서에서 했던 것 처럼 페이지의 제목 페이지 개발자가 명시적으로 설정 되지 않은 경우 사이트 맵 노드 제목을 사용 하겠습니다. 요청 된 페이지에는 명시적으로 설정 된 없는 경우에 없는 사이트 맵을 다시 이동는 요청 된 페이지의 파일 이름 확장명) (낮은 사용 하 여 2 단계에서에서와 같이 다음 및 페이지 제목입니다. 그림 11이 의사 결정 프로세스를 보여 줍니다.


![명시적으로 설정 페이지 제목이 없는 경우에는 해당 사이트 맵 노드 제목이 사용 됩니다.](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image21.png)

**그림 11**: 명시적으로 설정 페이지 제목 없는 경우, 해당 사이트 맵 노드의 제목이 사용 됩니다


업데이트는 `BasePage` 클래스의 `OnLoadComplete` 메서드를 다음 코드를 포함 합니다.


[!code-vb[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample12.vb)]

이전 처럼는 `OnLoadComplete` 페이지의 제목 명시적으로 설정 되었는지 여부를 확인 하 여 메서드를 시작 합니다. 경우 `Page.Title` 은 `Nothing`, 빈 문자열을 코드에 값을 자동으로 할당 한 다음 "제목 없음 페이지" 값이 할당 또는 `Page.Title`합니다.

사용할 제목을 확인 하려면를 참조 하 여 시작 하는 코드는 [ `SiteMap` 클래스](https://msdn.microsoft.com/library/system.web.sitemap.aspx)의 [ `CurrentNode` 속성](https://msdn.microsoft.com/library/system.web.sitemap.currentnode.aspx)합니다. `CurrentNode` 반환 된 [ `SiteMapNode` ](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx) 현재 요청 된 페이지에 해당 하는 사이트 맵에서 인스턴스. 현재 요청 된 페이지 가정 사이트 맵 내에서 발견 되는 `SiteMapNode`의 `Title` 속성이 페이지의 제목에 할당 됩니다. 현재 요청 된 페이지 사이트 맵에 없는 경우 `CurrentNode` 반환 `Nothing` 요청 된 페이지의 파일 이름 (2 단계에서에서 수행 했던) 것 처럼 제목으로 사용 됩니다.

그림 12는 `MultipleContentPlaceHolders.aspx` 브라우저를 통해 볼 때 페이지입니다. 이 페이지의이 제목 명시적으로 설정 되어 있지 않으므로 해당 사이트 맵 노드의 제목이 대신 사용 됩니다.


![사이트 맵에서 끌어온 MultipleContentPlaceHolders.aspx 페이지의 제목](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/_static/image22.png)

**그림 12**: 사이트 맵에서 끌어온 The MultipleContentPlaceHolders.aspx 페이지의 제목


## <a name="step-4-adding-other-page-specific-markup-to-theheadsection"></a>4 단계: 다른 페이지 관련 태그를 추가`<head>`섹션

사용자 지정에 1, 2, 3 단계 검토는 `<title>` 페이지 단위로 별로 요소입니다. 외에 `<title>`, `<head>` 섹션은 포함할 수 `<meta>` 요소 및 `<link>` 요소입니다. 이 자습서의 앞부분에서 설명한 것 처럼 `Site.master`의 `<head>` 섹션에는 `<link>` 요소의 `Styles.css`합니다. 때문에이 `<link>` 요소가 마스터 페이지 내에서 정의 된에 포함 되어는 `<head>` 모든 콘텐츠 페이지에 대 한 섹션. 어떻게 까 추가 하지만 `<meta>` 및 `<link>` 요소에서 페이지 단위로?

페이지 관련 콘텐츠를 추가 하는 가장 쉬운 방법은 `<head>` 섹션 마스터 페이지에서 ContentPlaceHolder 컨트롤을 만드는 것입니다. 이미 해당 ContentPlaceHolder (라는 `head`). 따라서 사용자 지정을 추가 하려면 `<head>` 태그를 만들려면 해당 페이지에서 제어 콘텐츠 및 태그 놓일 합니다.

추가 사용자 지정을 설명 하기 위해 `<head>` 태그 페이지에 포함 되어 보겠습니다는 `<meta>` 설명 요소 콘텐츠 페이지의 현재 집합입니다. `<meta>` description 요소 웹 페이지에 대 한 간략 한 설명을 제공 합니다; 대부분의 검색 엔진 검색 결과 표시할 때 어떤 형태로이 정보를 통합 합니다.

A `<meta>` description 요소 형식은 다음과 같습니다.


[!code-html[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample13.html)]

이 태그에는 콘텐츠 페이지를 추가 하려면 위의 텍스트 마스터 페이지에 매핑되는 콘텐츠 컨트롤에 추가 `head` ContentPlaceHolder 합니다. 예를 들어, 정의 하는 `<meta>` description 요소에 대 한 `Default.aspx`, 다음 태그를 추가:


[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample14.aspx)]

때문에 `head` HTML 페이지의 본문 내에 없으면 ContentPlaceHolder, 콘텐츠 컨트롤에 추가 하는 태그 디자인 뷰에 표시 되지 않습니다. 참조 하는 `<meta>` 설명 요소 방문 `Default.aspx` 브라우저를 통해 합니다. 페이지 로드 된 후 소스를 볼 하 고는 `<head>` 콘텐츠 컨트롤에 지정 된 태그 섹션에 포함 되어 있습니다.

추가 하려면 잠시 `<meta>` 설명 요소를 `About.aspx`, `MultipleContentPlaceHolders.aspx`, 및 `Login.aspx`합니다.

### <a name="programmatically-adding-markup-to-theheadregion"></a>프로그래밍 방식으로 태그를 추가`<head>`영역

`head` ContentPlaceHolder 선언적으로 마스터 페이지에 사용자 지정 태그를 추가 하는 데 사용할 수 있으며 `<head>` 영역입니다. 사용자 지정 태그 프로그래밍 방식으로 추가 될 수도 있습니다. 이전에 설명한 대로 `Page` 클래스의 `Header` 속성에서 반환 된 `HtmlHead` 마스터 페이지에 정의 된 인스턴스 (의 `<head runat="server">`).

프로그래밍 방식으로 콘텐츠를 추가할 수는 `<head>` 지역은 추가할 콘텐츠는 동적 하는 경우에 유용 합니다. 페이지를 방문 하는 사용자에 기반 하는 아마도 이전 데이터베이스에서 풀링 하는 합니다. 어떤 이유로 든, 콘텐츠를 추가할 수 있습니다는 `HtmlHead` 컨트롤을 추가 하 여 해당 `Controls` 같이 컬렉션:


[!code-vb[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb/samples/sample15.vb)]

추가 하는 위의 코드는 `<meta>` 키워드 요소를는 `<head>` 영역 페이지를 설명 하는 키워드의 쉼표로 구분 된 목록을 제공 합니다. 추가 하는 한 `<meta>` 태그를 만들면는 [ `HtmlMeta` ](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlmeta.aspx) 인스턴스를 설정의 `Name` 및 `Content` 속성을 다음에 추가 `Header`의 `Controls` 컬렉션입니다. 마찬가지로, 프로그래밍 방식으로 추가 하는 `<link>` 요소를 만들기는 [ `HtmlLink` ](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmllink.aspx) 개체, 해당 속성을 설정한 다음에 추가 하는 `Header`의 `Controls` 컬렉션입니다.

> [!NOTE]
> 임의 태그를 추가 하려면 만듭니다는 [ `LiteralControl` ](https://msdn.microsoft.com/library/system.web.ui.literalcontrol.aspx) 인스턴스를 설정의 `Text` 속성을 다음에 추가 하는 `Header`의 `Controls` 컬렉션입니다.


## <a name="summary"></a>요약

이 자습서에서 보이는 것 처럼 다양 한 방법으로 추가할 `<head>` 페이지 단위로 별로 지역 태그입니다. 마스터 페이지에 포함 해야는 `HtmlHead` 인스턴스 (`<head runat="server">`)는 ContentPlaceHolder 사용 합니다. `HtmlHead` 콘텐츠 페이지 프로그래밍 방식으로 액세스를 허용 된 `<head>` 지역 제목의 선언적 방법과 프로그래밍 방식으로 페이지를 설정 하 고 ContentPlaceHolder 제어에 추가할 사용자 지정 태그를 사용 하면는 `<head>` 콘텐츠 컨트롤을 통해 선언적으로 섹션입니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [동적 asp.net에서 페이지의 제목 설정](http://aspnet.4guysfromrolla.com/articles/051006-1.aspx)
- [ASP를 검사 합니다. NET의 사이트 탐색](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [HTML 메타 태그를 사용 하는 방법](http://searchenginewatch.com/showPage.html?page=2167931)
- [Asp.net에서 마스터 페이지](http://www.odetocode.com/articles/419.aspx)
- [ASP.NET 3.5의를 사용 하 여 ListView 및 DataPager 컨트롤](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)
- [ASP.NET 페이지의 코드 숨김 클래스에 대 한 사용자 지정 기본 클래스를 사용 하 여](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)

### <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 작성자 여러 ASP/ASP.NET 설명서와 4GuysFromRolla.com의 창립자의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 3.5 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. Scott에 도달할 수 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com) 또는에서 그의 블로그 통해 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Zack Jones 및 Suchi Banerjee 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)합니다.

> [!div class="step-by-step"]
> [이전](multiple-contentplaceholders-and-default-content-vb.md)
> [다음](urls-in-master-pages-vb.md)
