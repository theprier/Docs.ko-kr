---
uid: web-forms/overview/data-access/introduction/master-pages-and-site-navigation-cs
title: "마스터 페이지 및 사이트 탐색 (C#) | Microsoft Docs"
author: rick-anderson
description: "웹 사이트 사용자에 게 친숙 한 일반적인 특징 일관 되 고 사이트 전체 페이지 레이아웃 및 탐색 체계 수 있는입니다. 이 자습서에서는 방법 y..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 5aee8202-a4e3-4aa9-8a95-cd5d156cea4c
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/introduction/master-pages-and-site-navigation-cs
msc.type: authoredcontent
ms.openlocfilehash: 32ddda8d883a99805d2448c9673e585bfe9ef2f4
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="master-pages-and-site-navigation-c"></a>마스터 페이지 및 사이트 탐색 (C#)
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_3_CS.exe) 또는 [PDF 다운로드](master-pages-and-site-navigation-cs/_static/datatutorial03cs1.pdf)

> 웹 사이트 사용자에 게 친숙 한 일반적인 특징 일관 되 고 사이트 전체 페이지 레이아웃 및 탐색 체계 수 있는입니다. 이 자습서를 쉽게 업데이트할 수 있는 모든 페이지에 걸쳐 일관 된 모양과 느낌을 만드는 방법을 살펴봅니다.


## <a name="introduction"></a>소개

웹 사이트 사용자에 게 친숙 한 일반적인 특징 일관 되 고 사이트 전체 페이지 레이아웃 및 탐색 체계 수 있는입니다. ASP.NET 2.0에는 사이트 전체 페이지 레이아웃 및 탐색 체계 둘 다 구현 간소화 해 주는 두 가지 새로운 기능이 도입 되었습니다: 마스터 페이지 및 사이트 탐색 합니다. 지정 된 편집 가능한 영역을 사용 하 여 사이트 전체 서식 파일을 만들려면 개발자를 위한 마스터 페이지를 사용 합니다. 그런 다음 사이트의 ASP.NET 페이지에이 서식 파일을 적용할 수 있습니다. 이러한 ASP.NET 페이지 제공 하면 콘텐츠 편집 가능한 영역 지정 된 마스터 페이지에 대 한 마스터 페이지를 사용 하는 모든 ASP.NET 페이지에 걸쳐 마스터 페이지의 다른 모든 태그는 동일 합니다. 이 모델에는 개발자를가 정의 하 고 중앙 집중화 하 고 쉽게 업데이트할 수 있는 모든 페이지에 걸쳐 일관 된 모양과 느낌 만들기를 보다 쉽게 사이트 전체 페이지 레이아웃을 수 있습니다.

[사이트 탐색 시스템](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx) 를 모두 제공 페이지 개발자 사이트 맵을 정의 하는 메커니즘 해당 사이트 맵에 대 한 API를 프로그래밍 방식으로 쿼리할 수 있습니다. 메뉴, TreeView 및 SiteMapPath 하기 쉽도록 새 탐색 웹 컨트롤 사이트 맵 공통 탐색 사용자 인터페이스 요소에서의 전체 또는 일부를 렌더링 합니다. 즉 우리의 사이트 맵 XML 형식 파일에 정의할 수는 기본 사이트 탐색 공급자를 사용할 예정입니다.

이러한 개념을 설명 하 고 자습서 웹 사이트를 더 사용할 수 있도록 하려면이 단원에서는 사이트 전체 페이지 레이아웃을 정의 사이트 맵 구현 하 고, 탐색 UI를 추가 해 보겠습니다 소비 해야 합니다. 이 자습서의 끝으로는 자습서 웹 페이지를 구축 하기 위한 세련 된 웹 사이트 디자인을 했습니다.


[![이 자습서의 최종 결과](master-pages-and-site-navigation-cs/_static/image2.png)](master-pages-and-site-navigation-cs/_static/image1.png)

**그림 1**: The 최종 결과의 자습서 ([전체 크기 이미지를 보려면 클릭](master-pages-and-site-navigation-cs/_static/image3.png))


## <a name="step-1-creating-the-master-page"></a>1 단계: 마스터 페이지 만들기

첫 번째 단계는 사이트에 대 한 마스터 페이지를 만드는 것입니다. 웹 사이트 형식의 DataSet만 이루어져 이제를 마우스 오른쪽 단추로 (`Northwind.xsd`에 `App_Code` 폴더), BLL 클래스 (`ProductsBLL.cs`, `CategoriesBLL.cs`, 등의 모두는 `App_Code` 폴더), 데이터베이스 (`NORTHWND.MDF`에 `App_Data` 폴더), 구성 파일 (`Web.config`), 및 CSS 스타일 시트 파일 (`Styles.css`). 페이지 및 이후 사용 하 여 DAL 및 BLL 첫 두 자습서에서 우리는 될 다시 검토 이러한 예제를 자세히 이후 자습서에서 보여 주는 파일만 I 정리 합니다.


![이 프로젝트의 파일](master-pages-and-site-navigation-cs/_static/image4.png)

**그림 2**: 프로젝트에 파일


마스터 페이지를 만들려면 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가 선택 합니다. 다음 템플릿 목록에서 마스터 페이지 유형을 선택 하 고 이름을 `Site.master`합니다.


[![웹 사이트에 새 마스터 페이지를 추가 합니다.](master-pages-and-site-navigation-cs/_static/image6.png)](master-pages-and-site-navigation-cs/_static/image5.png)

**그림 3**: 웹 사이트에 새 마스터 페이지를 추가 ([전체 크기 이미지를 보려면 클릭](master-pages-and-site-navigation-cs/_static/image7.png))


마스터 페이지의 여기 사이트 전체 페이지 레이아웃을 정의 합니다. 디자인 뷰를 사용 하 고 필요한 모든 레이아웃 또는 웹 컨트롤을 추가 하거나 직접 소스 뷰에서 태그를 수동으로 추가할 수 있습니다. 마스터 페이지 내에서 사용 [스타일 시트](http://www.w3schools.com/css/default.asp) 배치 및 외부 파일에 정의 된 CSS 설정 가진 스타일 `Style.css`합니다. CSS 규칙을 정의 하는 동안 아래에 표시 된 태그에서 알 수 없습니다, 되도록 탐색 `<div>`의 왼쪽에 나타나고이 200 픽셀의 고정된 폭 있도록 절대 콘텐츠 위치로 지정 합니다.

Site.master


[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample1.aspx)]

마스터 페이지에는 정적 페이지 레이아웃 및 마스터 페이지를 사용 하는 ASP.NET 페이지에서 편집할 수 있는 영역을 모두 정의 합니다. 이러한 콘텐츠 편집 가능한 영역 콘텐츠 내에서 볼 수 있는 해당 ContentPlaceHolder 컨트롤에 의해 표시 됩니다 `<div>`합니다. 이 마스터 페이지에 단일 ContentPlaceHolder (`MainContent`), 마스터 페이지의 여러 contentplaceholders의 있을 수 있습니다.

위에 입력 한 태그를 디자인 뷰로 전환 마스터 페이지의 레이아웃을 표시 됩니다. 이 마스터 페이지를 사용 하는 모든 ASP.NET 페이지에 대 한 태그를 지정 하는 기능과 함께이 균일 한 레이아웃 갖습니다는 `MainContent` 영역입니다.


[![디자인 뷰를 통해 볼 때 마스터 페이지](master-pages-and-site-navigation-cs/_static/image9.png)](master-pages-and-site-navigation-cs/_static/image8.png)

**그림 4**: 마스터 페이지 때 볼 통해의 디자인 뷰 ([전체 크기 이미지를 보려면 클릭](master-pages-and-site-navigation-cs/_static/image10.png))


## <a name="step-2-adding-a-homepage-to-the-website"></a>2 단계: 웹 사이트에는 홈 페이지를 추가합니다.

정의 된 마스터 페이지, 웹 사이트에 대 한 ASP.NET 페이지를 추가 하려면 완료 합니다. 추가 하 여 시작 하겠습니다 `Default.aspx`, 웹 사이트의 홈 페이지입니다. 솔루션 탐색기에서 프로젝트 이름을 단추로 클릭 하 고 새 항목 추가 선택 합니다. 파일 이름을 확인 하 고 템플릿 목록에서 Web Form 옵션을 선택 `Default.aspx`합니다. "마스터 페이지 선택" 확인란을 확인 하십시오.


[![확인란을 선택 마스터 페이지를 확인 하는 중 새 Web Form을 추가](master-pages-and-site-navigation-cs/_static/image12.png)](master-pages-and-site-navigation-cs/_static/image11.png)

**그림 5**: Checkbox 선택 마스터 페이지를 확인 하는 중 새 Web Form을 추가 ([전체 크기 이미지를 보려면 클릭](master-pages-and-site-navigation-cs/_static/image13.png))


확인 단추를 클릭 한 후이 새 ASP.NET 페이지를 사용 해야 하는 마스터 페이지를 선택 하 라는 했습니다. 프로젝트에서 여러 마스터 페이지를 있을 수 있지만, 하나만 있는 것입니다.


[![이 ASP.NET 페이지를 사용 해야 하는 마스터 페이지를 선택 합니다.](master-pages-and-site-navigation-cs/_static/image15.png)](master-pages-and-site-navigation-cs/_static/image14.png)

**그림 6**:이 ASP.NET 페이지를 사용 하 여 마스터 페이지 선택 ([전체 크기 이미지를 보려면 클릭](master-pages-and-site-navigation-cs/_static/image16.png))


마스터 페이지를 선택한 후 새 ASP.NET 페이지에 다음 태그를 포함 됩니다.

Default.aspx


[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample2.aspx)]

에 `@Page` 있습니다 지시문은 사용 되는 마스터 페이지 파일에 대 한 참조 (`MasterPageFile="~/Site.master"`), 각 컨트롤에 있는 마스터 페이지에 정의 된 ContentPlaceHolder 컨트롤에 대 한 콘텐츠 컨트롤을 포함 하는 ASP.NET 페이지의 태그 `ContentPlaceHolderID` 특정 ContentPlaceHolder 컨트롤 매핑 콘텐츠입니다. 콘텐츠 컨트롤의 태그를 배치 하는 위치에 있는 해당 ContentPlaceHolder 표시를 합니다. 설정의 `@Page` 지시문의 `Title` 홈으로 특성을 환영 일부 콘텐츠는 콘텐츠 컨트롤을 추가 합니다.

Default.aspx


[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample3.aspx)]

`Title` 특성에 `@Page` 지시문을 사용 하면 ASP.NET 페이지에서 페이지의 제목도 설정할 수는 `<title>` 요소가 마스터 페이지에 정의 되어 있습니다. 설정할 수 있습니다도 제목 프로그래밍 방식으로 사용 하 여 `Page.Title`합니다. 또한 스타일 시트에 대 한 마스터 페이지의 한 참조 (같은 `Style.css`) 하는 방법과 마스터 페이지에 따라 ASP.NET 페이지는 어떤 디렉터리에 상관 없이 모든 ASP.NET 페이지에 자동으로 업데이트 됩니다.

가격 페이지는 브라우저에서 어떻게 나타나는지 확인할 수 있습니다 디자인 뷰로 전환 합니다. ContentPlaceHolder 아닌 태그를 마스터 페이지에 정의 된 콘텐츠 편집 가능한 영역을 편집할 수는 ASP.NET 페이지에 대 한 보기 디자인은 회색으로 표시 합니다.


[![ASP.NET 페이지에 대 한 디자인 보기 편집 가능한과 편집 불가능 영역을 보여 줍니다.](master-pages-and-site-navigation-cs/_static/image18.png)](master-pages-and-site-navigation-cs/_static/image17.png)

**그림 7**: The 디자인 뷰는 ASP.NET 페이지 표시 모두의 편집 가능 및 비 편집 영역 ([전체 크기 이미지를 보려면 클릭](master-pages-and-site-navigation-cs/_static/image19.png))


경우는 `Default.aspx` ASP.NET 엔진은 자동으로 페이지의 마스터 페이지 콘텐츠 및 ASP 병합, 브라우저에서 페이지를 방문 합니다. NET의 콘텐츠를 하 고 요청 하는 브라우저에 전송 되는 최종 HTML에 병합 된 콘텐츠를 렌더링 합니다. 마스터 페이지의 콘텐츠가 업데이트 될 때이 마스터 페이지를 사용 하는 모든 ASP.NET 페이지 다음에 요청 콘텐츠 새 마스터 페이지와 remerged 자신의 콘텐츠를 갖습니다. 즉, 마스터 페이지 확장성 모델은 단일 페이지 (마스터 페이지)를 정의 하는 레이아웃 템플릿이 되도록 변경 내용을 전체 사이트에 바로 반영 됩니다.

## <a name="adding-additional-aspnet-pages-to-the-website"></a>웹 사이트에 추가 하는 ASP.NET 페이지 추가

추가 ASP.NET 페이지가 스텁의 결국 다양 한 보고 데모를 보유 하는 사이트에 추가 하려면 간단히 살펴보겠습니다. 자세한 35 데모 전체적으로 하므로 모든 스텁 페이지 보겠습니다 작성 하지 않고 바로 보다 처음 몇을 만듭니다. 사용 해야 하는 여러 범주의 데모, 하므로 보다 효율적으로 관리할 데모 범주에 대 한 폴더를 추가 합니다. 지금은 다음 세 개의 폴더를 추가 합니다.

- `BasicReporting`
- `Filtering`
- `CustomFormatting`

그림 8의 솔루션 탐색기에 표시 된 대로 새 파일을 마지막으로 추가 합니다. 각 파일을 추가 하는 경우 "마스터 페이지 선택" 확인란을 선택 해야 합니다.


![다음 파일에 추가](master-pages-and-site-navigation-cs/_static/image20.png)

**그림 8**: 다음 파일에 추가


## <a name="step-2-creating-a-site-map"></a>2 단계: 사이트 맵 만들기

소수의 페이지 이상으로 구성 하는 웹 사이트 관리의 과제 중 하나는 방문자가 있는 사이트를 통해 탐색 하는 간단한 방법을 제공 합니다. 처음에 사이트의 탐색 구조 정의 되어야 합니다. 다음으로,이 구조 메뉴 등 이동 경로 탐색 가능한 사용자 인터페이스 요소 변환 해야 합니다. 마지막으로,이 전체 프로세스 유지 관리 하 고 새 페이지는 사이트 및 제거 하는 기존 세션에 추가 될 때 업데이트 해야 합니다. ASP.NET 2.0 이전 버전을 유지 관리 및 탐색 가능한 사용자 인터페이스 요소를 변환에 대 한 자신의 사이트의 탐색 구조를 만드는 방법에 개발자가 했습니다. 그러나 ASP.NET 2.0을 개발자가 사용할 수 있습니다 매우 유연한 사이트 탐색 시스템에 기본 제공.

ASP.NET 2.0 사이트 탐색 시스템 사이트 맵을 정의 하 고 다음 프로그래밍 방식으로 API를 통해이 정보에 액세스 하는 개발자를 위한 방법을 제공 합니다. ASP.NET은 사이트 맵 데이터를 특정 방식으로 서식이 지정 된 XML 파일에 저장할 수를 예상 하는 사이트 맵 공급자 함께 제공 됩니다. 하지만 사이트 탐색 시스템은 기반으로 하므로 [공급자 모델](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx) 사이트 맵 정보를 직렬화 하는 작업에 대 한 대체 방법을 지원 하도록 확장할 수 있습니다. 부분의 문서 [The SQL 사이트 맵 공급자 하면 이전 된 완벽 하 게](https://msdn.microsoft.com/msdnmag/issues/06/02/WickedCode/default.aspx) 사이트 맵 SQL Server 데이터베이스에 저장 하는 사이트 맵 공급자를 만들려면;를 만드는 또 다른 옵션은 방법을 보여 줍니다. [사이트 맵 공급자에 따라 파일 시스템 구조](http://aspnet.4guysfromrolla.com/articles/020106-1.aspx)합니다.

하지만이 자습서에서는 보겠습니다 함께 제공 되는 기본 사이트 맵 공급자와 사용 ASP.NET 2.0. 사이트 맵을 만들려면 단순히에서 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭, 새 항목 추가 및 사이트 맵 옵션을 선택 합니다. 이름으로 `Web.sitemap` 추가 단추를 클릭 합니다.


[![사이트 맵을 프로젝트에 추가](master-pages-and-site-navigation-cs/_static/image22.png)](master-pages-and-site-navigation-cs/_static/image21.png)

**그림 9**: 사이트 맵을 프로젝트에 추가 ([전체 크기 이미지를 보려면 클릭](master-pages-and-site-navigation-cs/_static/image23.png))


사이트 맵 파일은 XML 파일입니다. Visual Studio에서는 사이트 맵 구조에 대 한 IntelliSense를 제공 하는 참고 합니다. 사이트 맵 파일이 있어야는 `<siteMap>` 정확 하 게 하나 포함 되어야 하는 루트 노드로 노드 `<siteMapNode>` 자식 요소입니다. 첫 번째 `<siteMapNode>` 요소 수는 임의 개수의 하위 포함한 다음 `<siteMapNode>` 요소입니다.

파일 시스템 구조를 모방 하기 위해 사이트 맵을 정의 합니다. 즉, 추가 `<siteMapNode>` 세 폴더 및 자식 각각에 대해 요소 `<siteMapNode>` 같이 ASP.NET 페이지의 해당 폴더의 각 요소:

Web.sitemap


[!code-xml[Main](master-pages-and-site-navigation-cs/samples/sample4.xml)]

사이트 맵 사이트의 다양 한 섹션에 설명 하는 계층 구조는 웹 사이트의 탐색 구조를 정의 합니다. 각 `<siteMapNode>` 요소 `Web.sitemap` 사이트의 탐색 구조의 섹션을 나타냅니다.


[![사이트 맵 탐색 계층 구조를 나타냅니다.](master-pages-and-site-navigation-cs/_static/image25.png)](master-pages-and-site-navigation-cs/_static/image24.png)

**그림 10**: 사이트 맵 탐색 계층 구조를 나타냅니다 ([전체 크기 이미지를 보려면 클릭](master-pages-and-site-navigation-cs/_static/image26.png))


.NET Framework를 통해 사이트 맵 구조를 표시 하는 ASP.NET [SiteMap 클래스](https://msdn.microsoft.com/en-us/library/system.web.sitemap.aspx)합니다. 이 클래스에는 `CurrentNode` 속성을 사용자가 현재 방문; 섹션에 대 한 정보를 반환 하는 `RootNode` 사이트 맵의 제곱근을 반환 하는 속성 (집 우리의 사이트 맵에서). 둘 다는 `CurrentNode` 및 `RootNode` 속성 반환 [SiteMapNode](https://msdn.microsoft.com/en-us/library/system.web.sitemapnode.aspx) 인스턴스 속성이 같은 `ParentNode`, `ChildNodes`, `NextSibling`, `PreviousSibling`, 등의 사이트 맵 수 있는 진행할를 계층 구조입니다.

## <a name="step-3-displaying-a-menu-based-on-the-site-map"></a>사이트 맵에 따라 메뉴를 표시 하는 3 단계:

ASP.NET 2.0에서 데이터에 액세스할 수 ASP.NET에서와 같이 프로그래밍 방식으로 수행 1.x 또는 새 통해 선언적으로 [데이터 소스 컨트롤과](https://msdn.microsoft.com/en-us/library/ms227679.aspx)합니다. 관계형 데이터베이스 데이터, ObjectDataSource 컨트롤에서 클래스 및 다른 사용자 데이터에 액세스 하는 것에 대 한 액세스를 위한 SqlDataSource 컨트롤 같은 기본 제공 데이터 소스 컨트롤이 여러 개 있습니다. 만들 수도 있습니다 직접 [사용자 지정 데이터 소스 컨트롤과](https://msdn.microsoft.com/asp.net/reference/data/default.aspx?pull=/library/en-us/dnvs05/html/DataSourceCon1.asp)합니다.

데이터 소스 컨트롤은 ASP.NET 페이지 및 원본 데이터 간의 프록시도 사용 됩니다. 데이터 소스 컨트롤의 검색된 데이터를 표시 하기 위해 일반적으로 페이지에 다른 웹 컨트롤을 추가할 알아보고 하겠습니다 데이터 소스 컨트롤에 바인딩합니다. 웹 컨트롤을 데이터 소스 제어에 바인딩할 웹 컨트롤을 설정 하기만 하면 `DataSourceID` 속성을 데이터 소스 컨트롤의 값으로 `ID` 속성입니다.

사이트 맵 데이터 작업을 지 원하는, ASP.NET 웹 사이트의 사이트 맵에 대해 웹 컨트롤에 바인딩할 수 있는 SiteMapDataSource 컨트롤 포함 되어 있습니다. 두 개의 웹 컨트롤의 트리 보기 및 메뉴 탐색 사용자 인터페이스를 제공 하 여 자주 사용 됩니다. 이 두 컨트롤 중 하나에 사이트 맵 데이터를 바인딩할 SiteMapDataSource TreeView 함께 페이지에 추가 또는 메뉴 컨트롤 `DataSourceID` 속성을 적절 하 게 설정 합니다. 예를 들어 다음 태그를 사용 하 여 마스터 페이지에는 메뉴 컨트롤을 추가할 수 있습니다.


[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample5.aspx)]

내보낸된 HTML에 대 한 제어는 보다 세부적인 수준에 대 한 반복기 컨트롤에 SiteMapDataSource 컨트롤 바인딩할 수 같이:


[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample6.aspx)]

SiteMapDataSource 제어가 반환 사이트 맵 한 계층 수준을 한 번에 루트 사이트 맵 노드 시작 (집 우리의 사이트 맵에서), (기본 보고, 필터링 보고서 및 사용자 지정 형식 지정), 다음 다음 수준 등에입니다. 첫 번째 수준 열거는 반복기에는 SiteMapDataSource 바인딩할 경우 반환 되 고 인스턴스화하는 `ItemTemplate` 각각에 대해 `SiteMapNode` 해당 첫 번째 수준에는 인스턴스. 특정 속성에 액세스 하려면는 `SiteMapNode`, 사용할 수 `Eval(propertyName)`를 가져오는 방법에 대해 각각 변수인 `SiteMapNode`의 `Url` 및 `Title` 하이퍼링크 컨트롤에 대 한 속성입니다.

위의 반복기 예제에 다음 태그를 렌더링 됩니다.


[!code-html[Main](master-pages-and-site-navigation-cs/samples/sample7.html)]

이러한 사이트 맵 노드 (기본 보고, 필터링 보고서 및 사용자 지정 서식)를 구성 하는 *두 번째* 렌더링 되 고 첫 번째 사이트 맵의 수준입니다. 때문에 이것이 SiteMapDataSource의 `ShowStartingNode` 루트 사이트 맵 노드를 무시 하는 사이트 맵 계층에서 두 번째 수준을 반환 하 여 시작 대신 SiteMapDataSource 일으키는 속성이 False로 설정 되어 있습니다.

기본 보고, 필터링 보고서 및 사용자 지정 서식 지정에 대 한 자식 항목을 표시 하려면 `SiteMapNode` s, 다른 반복기 초기 반복기를 추가할 수 있는 `ItemTemplate`합니다. 이 두 번째 반복기에 연결 되는 `SiteMapNode` 인스턴스의 `ChildNodes` 속성을 다음과 같이:


[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample8.aspx)]

이러한 두 반복기에 다음 태그 (태그 제거 되었습니다 간단히 하기 위해)에서 발생 합니다.


[!code-html[Main](master-pages-and-site-navigation-cs/samples/sample9.html)]

선택한 스타일 CSS를 사용 하 여에서 [Rachel Andrew](http://www.rachelandrew.co.uk/)책의 [The CSS Anthology: 101 필수 팁, 요령 &amp; 해킹](https://www.amazon.com/gp/product/0957921888/qid=1137565739/sr=8-1/ref=pd_bbs_1/103-0562306-3386214?n=507846&amp;s=books&amp;v=glance), `<ul>` 및 `<li>` 요소는 스타일이 지정 되도록 태그는 다음과 같은 시각적 출력을 생성합니다.


![두 개의 반복기 및 일부 CSS에서 구성 된 메뉴](master-pages-and-site-navigation-cs/_static/image27.png)

**그림 11**: 두 개의 반복기 및 일부 CSS에서 구성 된 메뉴로


이 메뉴를 마스터 페이지에 바인딩되고에 정의 된 사이트 맵을 `Web.sitemap`즉, 사용 하는 페이지 사이트 맵의 모든 변경 내용이 모두에 즉시 반영 됩니다는 `Site.master` 마스터 페이지입니다.

## <a name="disabling-viewstate"></a>ViewState를 사용 하지 않도록 설정

모든 ASP.NET 컨트롤의 상태를 유지할 필요에 따라 수는 [뷰 상태](https://msdn.microsoft.com/msdnmag/issues/03/02/CuttingEdge/), 렌더링 된 HTML에서 숨겨진된 양식 필드도 serialize 되는 합니다. 뷰 상태 데이터 웹 컨트롤에 바인딩된 데이터가 같은 컨트롤에서 포스트백을 통해 프로그래밍 방식으로 변경의 상태를 기억 하기 사용 됩니다. 뷰 상태 정보를 게시할를 기억 하 고 허용 하는 동안 클라이언트에 전송 해야 하며 심각한 페이지 크기를 늘리지 발생할 수 있습니다 되지 않은 경우 주의 깊게 모니터링 하는 태그의 크기를 증가 합니다. 웹 컨트롤 GridView 특히 데이터는 특히 태그의 추가 킬로바이트 수십 개 페이지에 추가 합니다. 이러한 증가 하는 광대역 또는 인트라넷 사용자가 무시할 수 있지만, 뷰 상태를 사용 하 여 몇 초 정도 전화 접속 사용자에 대 한 왕복에 추가할 수 있습니다.

뷰 상태를 브라우저에서 페이지를 방문 하는 웹 페이지에서 보낸 소스를 볼의 영향을 확인 하려면 (Internet Explorer에서 보기 메뉴 옵션을 선택 소스). 또한 켤 수 [페이지 추적](https://msdn.microsoft.com/en-us/library/sfbfw58f.aspx) 할당 각 페이지에 컨트롤에서 사용 하는 보기 상태를 볼 수 있습니다. 뷰 상태 정보가 라는 숨겨진된 폼 필드에 serialize 되는 `__VIEWSTATE`에 있는 한 `<div>` 열기 바로 다음 요소 `<form>` 태그입니다. 뷰 상태는 Web Form 사용 되는 경우에 유지 ASP.NET 페이지에 포함 되어 있지 않으면는 `<form runat="server">` 없습니다 선언적 구문에는 `__VIEWSTATE` 렌더링된 된 태그에서 숨겨진된 양식 필드입니다.

`__VIEWSTATE` 마스터 페이지에 의해 생성 된 양식 필드 생성 되는 페이지의 태그에 약 1, 800 바이트를 추가 합니다. 반복기 컨트롤을 주로 추가 볼록이는 상태를 보려면 SiteMapDataSource 컨트롤의 내용이 유지 됩니다. 추가 1, 800 바이트는 GridView 많은 필드와 레코드를 사용 하는 경우, 흥미를 얼마나 하지 보일 수 있지만, 뷰 상태는 10 개 이상의 인수에 따라 쉽게 부풀어 오름 수 있습니다.

뷰 상태를 설정 하 여 컨트롤 또는 페이지 수준에서 사용할 수는 `EnableViewState` 속성을 `false`없어지고 렌더링된 된 태그의 크기를 줄이십시오. 웹 컨트롤 게시할 데이터 웹 컨트롤에 바인딩된 데이터를 유지 하는 데이터에 대 한 상태 보기 이후 웹 컨트롤의 뷰 상태 데이터를 사용 하지 않도록 설정 하는 경우 데이터에 바인딩되어 있어야 각 다시 게시 합니다. ASP.NET 버전에서이 책임은 결코 페이지 개발자; 속하는 1.x 하지만 ASP.NET 2.0을 사용 데이터 웹 컨트롤 다시 바인딩됩니다 다시 게시할 때마다 해당 데이터 소스 제어에 필요한 경우.

반복기 컨트롤의 설정 페이지의 뷰 상태를 줄이기 위해 보겠습니다 `EnableViewState` 속성을 `false`합니다. 디자이너 또는 선언적으로 소스 뷰에서 속성 창을 통해이 작업을 수행할 수 있습니다. 이 같이 변경한 후 반복기의 선언적 태그는 같습니다.


[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample10.aspx)]

이러한 변경 페이지의 상태 크기에 뿐을 축소 하는 뷰를 렌더링 한 다음 52 바이트, 97% 절감 뷰 상태에 크기! 이 시리즈 자습서 중이지만 렌더링된 된 태그의 크기를 줄이기 위해 데이터 웹 컨트롤의 뷰 상태를 기본적으로 비활성화 합니다. 대부분의 예제는 `EnableViewState` 속성으로 설정 됩니다 `false` 언급 없이를 수행 하 고 있습니다. 에 데이터에 대 한 순서에서 사용할 수 있어야 하는 경우에는 보기 상태에 설명 합니다 웹 컨트롤 예상된 기능을 제공 합니다.

## <a name="step-4-adding-breadcrumb-navigation"></a>4 단계: 추가 이동 경로 탐색

마스터 페이지를 완료 하려면 각 페이지에는 이동 경로 탐색 UI 요소를 추가 해 보겠습니다. 경로 기록의 사이트 계층 구조 내에 있는 현재 위치 사용자를 신속 하 게 보여 줍니다. 페이지; SiteMapPath 컨트롤에 추가 ASP.NET 2.0에서 이동 경로 쉽게 추가 코드가 필요 합니다.

이 사이트에 대 한 헤더에이 컨트롤을 추가할 `<div>`:


[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample11.aspx)]

이동 경로 탐색 루트 위쪽으로 사용자를 해당 사이트 "상위" 맵 노드를 비롯 하 여 사이트 맵 계층 구조에 방문 현재 페이지가 표시 (집 우리의 사이트 맵에서).


![현재 페이지를 표시 된 이동 경로 및 상위 사이트에 있는 지도 계층](master-pages-and-site-navigation-cs/_static/image28.png)

**그림 12**: 현재 페이지를 표시 된 이동 경로 및 상위 사이트에서 계층 구조 매핑


## <a name="step-5-adding-the-default-page-for-each-section"></a>5 단계: 각 섹션에 대 한 기본 페이지 추가

사이트의 자습서에서는 범주로 구분 다른 기본 보고 필터링, 사용자 지정 형식 지정, 각 범주 및 해당 폴더 내의 ASP.NET 페이지와 해당 자습서에 대 한 폴더와 등. 또한 각 폴더에는 `Default.aspx` 페이지. 이 기본 페이지에 대 한 모든 현재 섹션에 대 한 자습서를 표시 해 보겠습니다. 즉,에 대 한는 `Default.aspx` 에 `BasicReporting` 폴더 우리는에 대 한 링크가 `SimpleDisplay.aspx`, `DeclarativeParams.aspx`, 및 `ProgrammaticParams.aspx`합니다. 여기에서 다시 사용할 수는 `SiteMap` 에 정의 된 클래스 및 데이터 사이트 맵을 기반으로이 정보를 표시 하려면 웹 컨트롤 `Web.sitemap`합니다.

다시 이번 제목 및 자습서의 설명을 표시 합니다는 반복기를 사용 하는 순서가 지정 되지 않은 목록을 표시 해 보겠습니다. 태그와이는 수행 하는 코드를 각각에 대해 반복 해야 하므로 `Default.aspx` 페이지에서는 캡슐화 할 수 있습니다이 UI 논리에는 [사용자 정의 컨트롤](https://msdn.microsoft.com/en-us/library/y6wb1a0e.aspx)합니다. 호출 하는 웹 사이트에 폴더를 만들고 `UserControls` 하 라는 웹 사용자 정의 컨트롤 유형의 새 항목 추가 `SectionLevelTutorialListing.ascx`, 다음 태그를 추가 하 고:


[![Usercontrol은 폴더에 새 웹 사용자 컨트롤 추가](master-pages-and-site-navigation-cs/_static/image30.png)](master-pages-and-site-navigation-cs/_static/image29.png)

**그림 13**: 새 웹 사용자 정의 컨트롤을 추가 `UserControls` 폴더 ([전체 크기 이미지를 보려면 클릭](master-pages-and-site-navigation-cs/_static/image31.png))


SectionLevelTutorialListing.ascx


[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample12.aspx)]

SectionLevelTutorialListing.ascx.cs


[!code-csharp[Main](master-pages-and-site-navigation-cs/samples/sample13.cs)]

하지만 바인딩된 म 개씩 반복기는 `SiteMap` 데이터 반복기를 선언적으로; `SectionLevelTutorialListing` 사용자 정의 컨트롤을이 작업을 수행 프로그래밍 방식으로 합니다. 에 `Page_Load` 이벤트 처리기 검사가 수행 되는이 페이지 URL에서 사이트 맵 노드 매핑됩니다 s 되도록 합니다. 이 사용자 정의 컨트롤에 해당 하지 않은 페이지에 사용 되는 경우 `<siteMapNode>` 항목, `SiteMap.CurrentNode` 반환 됩니다 `null` 데이터가 없는 반복기에 바인딩될 수 됩니다. 있다고 가정해 봅시다는 `CurrentNode`, 바인딩한 해당 `ChildNodes` 컬렉션을 반복 합니다. 우리의 사이트 맵 설정 되어 있으므로 되도록는 `Default.aspx` 각 섹션에는 페이지는 해당 섹션 내에서 자습서의 모든 부모 노드, 화면 아래에 나와 있는 것 처럼이 코드는에 대 한 링크 및 섹션의 자습서의 모든 설명에 표시 됩니다.

이 반복기를 만든 후 엽니다는 `Default.aspx` , 폴더의 각 페이지 디자인 보기로 이동 하 고 간단히 사용자 정의 컨트롤 디자인 화면으로 솔루션 탐색기에서 원하는 위치로 끕니다 자습서 목록이 표시 합니다.


[![사용자 정의 컨트롤은 Default.aspx에 추가 된](master-pages-and-site-navigation-cs/_static/image33.png)](master-pages-and-site-navigation-cs/_static/image32.png)

**그림 14**: 사용자 정의 컨트롤에 추가 된에 `Default.aspx` ([전체 크기 이미지를 보려면 클릭](master-pages-and-site-navigation-cs/_static/image34.png))


[![기본 보고 자습서와 같습니다.](master-pages-and-site-navigation-cs/_static/image36.png)](master-pages-and-site-navigation-cs/_static/image35.png)

**그림 15**: The 기본 보고 자습서와 같습니다 ([전체 크기 이미지를 보려면 클릭](master-pages-and-site-navigation-cs/_static/image37.png))


## <a name="summary"></a>요약

사이트 맵 정의와 마스터 페이지 전체를 이제 일관성 있는 페이지 레이아웃 및 탐색 체계에 대 한 우리의 데이터와 관련 된 자습서입니다. 사이트에 추가 페이지 수에 관계 없이 중앙 집중식으로 되 고이 정보로 인해 빠르고 간편한 프로세스는 사이트 전체 페이지 레이아웃 또는 사이트 탐색 정보를 업데이트 합니다. 페이지 레이아웃 정보 마스터 페이지에 정의 되어 특히 `Site.master` 및 사이트에서 맵 `Web.sitemap`합니다. 쓸 필요가 없 었 *모든* 이 사이트 전체 페이지 레이아웃 및 탐색 메커니즘을 달성 하기 위해 코드 및 Visual Studio에서 전체 WYSIWYG 디자이너 지원을 유지 했습니다.

데이터 액세스 계층 및 비즈니스 논리 계층 마치면 정의 된 일관성 있는 페이지 레이아웃 및 사이트 탐색 having, 준비가 보고의 일반 패턴을 탐색을 시작 하 고 있습니다. 에 [다음](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md) 세 개의 자습서에서 살펴보게 BLL DetailsView, GridView에서에서 검색 된 데이터를 표시 하는 기본 보고 작업 하 고 FormView 제어 합니다.

만족도 매우 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 마스터 페이지 개요](https://msdn.microsoft.com/en-us/library/wtxbf3hh.aspx)
- [ASP.NET 2.0의에서 마스터 페이지](http://odetocode.com/Articles/419.aspx)
- [ASP.NET 2.0 디자인 템플릿](https://msdn.microsoft.com/asp.net/reference/design/templates/default.aspx)
- [ASP.NET 사이트 탐색 개요](https://msdn.microsoft.com/en-us/library/e468hxky.aspx)
- [사이트 탐색의 ASP.NET 2.0 검사](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [ASP.NET 2.0 사이트 탐색 기능](https://weblogs.asp.net/scottgu/archive/2005/11/20/431019.aspx)
- [ASP.NET 뷰 상태 이해](https://msdn.microsoft.com/library/default.asp?url=/library/en-us/dnaspp/html/viewstate.asp)
- [방법: ASP.NET 페이지에 대 한 추적을 설정 합니다.](https://msdn.microsoft.com/en-us/library/94c55d08%28VS.80%29.aspx)
- [ASP.NET 사용자 정의 컨트롤](https://msdn.microsoft.com/en-us/library/y6wb1a0e.aspx)

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자가 Liz Shulok, Dennis Patterson 및 Hilton Giesenow 합니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](creating-a-business-logic-layer-cs.md)
[다음](creating-a-data-access-layer-vb.md)
