---
uid: web-forms/overview/data-access/introduction/master-pages-and-site-navigation-cs
title: 마스터 페이지 및 사이트 탐색 (C#) | Microsoft Docs
author: rick-anderson
description: 친숙 한 웹 사이트의 일반적인 특징 중 하나는 일관 되 고 사이트 전체 페이지 레이아웃 및 탐색 체계를가지고 있다고 합니다. 이 자습서는 방법을 찾고 y...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 5aee8202-a4e3-4aa9-8a95-cd5d156cea4c
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/introduction/master-pages-and-site-navigation-cs
msc.type: authoredcontent
ms.openlocfilehash: 7f152dcd32b1a7e3022d939c27860a81396a34b0
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37370363"
---
<a name="master-pages-and-site-navigation-c"></a>마스터 페이지 및 사이트 탐색 (C#)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_3_CS.exe) 또는 [PDF 다운로드](master-pages-and-site-navigation-cs/_static/datatutorial03cs1.pdf)

> 친숙 한 웹 사이트의 일반적인 특징 중 하나는 일관 되 고 사이트 전체 페이지 레이아웃 및 탐색 체계를가지고 있다고 합니다. 이 자습서를 쉽게 업데이트할 수 있는 모든 페이지에 걸쳐 일관 된 모양과 느낌을 만드는 방법을 살펴봅니다.


## <a name="introduction"></a>소개

친숙 한 웹 사이트의 일반적인 특징 중 하나는 일관 되 고 사이트 전체 페이지 레이아웃 및 탐색 체계를가지고 있다고 합니다. ASP.NET 2.0 간소화한 다음 두 사이트 전체 페이지 레이아웃 및 탐색 체계를 구현 하는 두 가지 새로운 기능이 도입 되었습니다: 마스터 페이지 및 사이트 탐색 합니다. 지정 된 편집 가능한 영역을 사용 하 여 사이트 전체 서식 파일을 만드는 개발자를 위한 마스터 페이지를 사용 합니다. 그런 다음 사이트의 ASP.NET 페이지에이 서식 파일을 적용할 수 있습니다. 마스터 페이지 지정 된 편집 가능한 영역에 대 한 이러한 ASP.NET 페이지 콘텐츠를 제공만 필요한 마스터 페이지를 사용 하는 모든 ASP.NET 페이지에 걸쳐 마스터 페이지의 다른 모든 태그는 동일 합니다. 이 모델에는 개발자를 정의 하 고 쉽게 업데이트할 수 있는 모든 페이지에 걸쳐 일관 된 모양과 느낌을 만들려면 보다 쉽게 사이트 전체 페이지 레이아웃을 중앙 집중화할 수 있습니다.

합니다 [사이트 탐색 시스템](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx) 모두 페이지 개발자 사이트 맵을 정의 하는 메커니즘 및 해당 사이트 맵에 대 한 API를 프로그래밍 방식으로 쿼리할 수를 제공 합니다. 메뉴, TreeView 및 SiteMapPath 쉽게 새 탐색 웹 컨트롤이 일반적인 탐색 사용자 인터페이스 요소에 사이트 맵의 일부나 전부를 렌더링 합니다. 즉 XML 서식 파일에는 사이트 맵을 정의할 수는 기본 사이트 탐색 공급자를 사용할 것입니다.

이러한 개념을 설명 하 고 자습서 웹 사이트를 더 사용할 수 있도록 하려면이 단원에서는 사이트 전체 페이지 레이아웃을 정의 하 고, 사이트 맵을 구현, 탐색 UI를 추가 해 보겠습니다 줄입니다. 이 자습서의 끝에서 자습서 웹 페이지를 빌드하기 위한 세련 된 웹 사이트 디자인을 해야 합니다.


[![이 자습서의 최종 결과](master-pages-and-site-navigation-cs/_static/image2.png)](master-pages-and-site-navigation-cs/_static/image1.png)

**그림 1**:의 최종 결과의 자습서 ([큰 이미지를 보려면 클릭](master-pages-and-site-navigation-cs/_static/image3.png))


## <a name="step-1-creating-the-master-page"></a>1 단계: 마스터 페이지 만들기

첫 번째 단계는 사이트의 마스터 페이지를 만드는 것입니다. 이제 웹 사이트 구성만 입력 데이터 집합을 마우스 오른쪽 단추로 (`Northwind.xsd`를 `App_Code` 폴더), 클래스 BLL (`ProductsBLL.cs`, `CategoriesBLL.cs`등, 모두는 `App_Code` 폴더), 데이터베이스 (`NORTHWND.MDF`의 `App_Data` 폴더)에 구성 파일 (`Web.config`), 및 CSS 스타일 시트 파일 (`Styles.css`). 해당 페이지와 이후 사용 하 여 BLL 및 DAL을 처음 두 자습서를 통해 우리는 수 다시 검토 이러한 예제를 자세히 이후 자습서에서 설명 하는 파일 I 정리 합니다.


![프로젝트의 파일](master-pages-and-site-navigation-cs/_static/image4.png)

**그림 2**: 프로젝트의 파일


마스터 페이지를 만들려면 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가 선택 합니다. 다음 템플릿 목록에서 마스터 페이지의 유형을 선택 하 고 이름을 `Site.master`입니다.


[![웹 사이트에 새 마스터 페이지를 추가 합니다.](master-pages-and-site-navigation-cs/_static/image6.png)](master-pages-and-site-navigation-cs/_static/image5.png)

**그림 3**: 웹 사이트에 새 마스터 페이지 추가 ([큰 이미지를 보려면 클릭](master-pages-and-site-navigation-cs/_static/image7.png))


마스터 페이지에서 사이트 전체 페이지 레이아웃 여기를 정의 합니다. 디자인 뷰를 사용할 수 있으며 필요한 모든 레이아웃 또는 웹 컨트롤을 추가 하거나 수동으로 소스 뷰에서 태그를 수동으로 추가할 수 있습니다. 마스터 페이지 내에서 사용 하 여 [cascading style sheet](http://www.w3schools.com/css/default.asp) 배치 및 외부 파일에 정의 된 CSS 설정 사용 하 여 스타일 `Style.css`합니다. 아래에 표시 된 태그에서 알 수 없습니다, 하는 동안 CSS 규칙을 정의 하는 탐색 `<div>`의 콘텐츠는 왼쪽에 표시 되 고 고정 너비가 200 픽셀이 있도록 절대적으로 배치 됩니다.

Site.master


[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample1.aspx)]

마스터 페이지에는 정적 페이지 레이아웃 및 마스터 페이지를 사용 하는 ASP.NET 페이지에서 편집할 수 있는 지역을 정의 합니다. 이러한 콘텐츠 편집 가능한 영역 콘텐츠 내에서 볼 수 있는 ContentPlaceHolder 컨트롤로 표시 됩니다 `<div>`합니다. 마스터 페이지에 단일 ContentPlaceHolder (`MainContent`), 마스터 페이지의 여러 ContentPlaceHolders 있을 수 있습니다.

위에 입력 한 태그를 사용 하 여 마스터 페이지의 레이아웃을 표시 디자인 뷰로 전환 합니다. 이 마스터 페이지를 사용 하는 모든 ASP.NET 페이지에 대 한 태그를 지정 하는 기능을 사용 하 여이 균일 한 레이아웃을 해야 합니다.는 `MainContent` 지역입니다.


[![마스터 페이지, 디자인 뷰를 통해 볼 때](master-pages-and-site-navigation-cs/_static/image9.png)](master-pages-and-site-navigation-cs/_static/image8.png)

**그림 4**:의 마스터 페이지 때 볼 통해 디자인 뷰 ([큰 이미지를 보려면 클릭](master-pages-and-site-navigation-cs/_static/image10.png))


## <a name="step-2-adding-a-homepage-to-the-website"></a>2 단계: 웹 사이트에는 홈 페이지 추가

정의 된 마스터 페이지에서는 웹 사이트에 대 한 ASP.NET 페이지를 추가할 준비가 된 것입니다. 추가 하 여 시작 해 보겠습니다 `Default.aspx`, 웹 사이트의 홈 페이지입니다. 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 새 항목 추가 선택 합니다. 파일 이름과 템플릿 목록에서 Web Form 옵션을 선택 `Default.aspx`합니다. 또한 "마스터 페이지 선택" 확인란을 확인 합니다.


[![확인란을 선택 마스터 페이지를 확인 하는 중 새 Web Form을 추가 합니다.](master-pages-and-site-navigation-cs/_static/image12.png)](master-pages-and-site-navigation-cs/_static/image11.png)

**그림 5**: 확인란 선택 마스터 페이지를 확인 하는 중 새 Web Form 추가 ([큰 이미지를 보려면 클릭](master-pages-and-site-navigation-cs/_static/image13.png))


확인 단추를 클릭 한 후이 새 ASP.NET 페이지를 사용 해야 하는 마스터 페이지를 선택 하 라는 메시지가 표시 하는 것입니다. 프로젝트에 여러 마스터 페이지를 지정할 수 있습니다, 하나만 있는 것입니다.


[![이 ASP.NET 페이지를 사용 해야 하는 마스터 페이지를 선택 합니다.](master-pages-and-site-navigation-cs/_static/image15.png)](master-pages-and-site-navigation-cs/_static/image14.png)

**그림 6**: ASP.NET 페이지는 사용이 마스터 페이지 선택 ([큰 이미지를 보려면 클릭](master-pages-and-site-navigation-cs/_static/image16.png))


마스터 페이지를 선택한 후 새 ASP.NET 페이지에는 다음과 같은 태그가 포함 됩니다.

Default.aspx


[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample2.aspx)]

에 `@Page` 지시문을 가지는 사용 되는 마스터 페이지 파일에 대 한 참조 (`MasterPageFile="~/Site.master"`), 각 컨트롤에 있는 마스터 페이지에 정의 된 ContentPlaceHolder 컨트롤에 대 한 콘텐츠 컨트롤을 포함 하는 ASP.NET 페이지의 태그 및 `ContentPlaceHolderID` 특정 ContentPlaceHolder 컨트롤 콘텐츠를 매핑. 콘텐츠 컨트롤의 태그를 배치 하는 위치는 해당 ContentPlaceHolder에 표시 하려고 합니다. 설정 합니다 `@Page` 지시문의 `Title` 홈으로 특성 및 했으며 일부 콘텐츠를 콘텐츠 컨트롤을 추가 합니다.

Default.aspx


[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample3.aspx)]

`Title` 특성을 `@Page` 지시문을 사용 하면 ASP.NET 페이지에서 페이지의 제목도 설정 하는 `<title>` 요소가 마스터 페이지에 정의 되어 합니다. 설정할 수도 있습니다 제목 프로그래밍 방식으로 사용 하 여 `Page.Title`입니다. 또한 마스터 페이지의 스타일 시트에 대 한 참조 (같은 `Style.css`) 하는 방법과 ASP.NET 페이지의 마스터 페이지를 기준으로 어떤 디렉터리에 관계 없이 모든 ASP.NET 페이지에 자동으로 업데이트 됩니다.

브라우저에서 페이지 모양을 보면 디자인 뷰로 전환 합니다. 디자인에서 마스터 페이지에 정의 되지 않은 ContentPlaceHolder 태그의 콘텐츠 편집 가능한 영역에만 적용 하는 편집할 수는 ASP.NET 페이지에 대 한 보기에 회색으로 표시 합니다.


[![ASP.NET 페이지의 디자인 뷰를 편집할 수 및 편집할 수 없는 영역을 보여 줍니다.](master-pages-and-site-navigation-cs/_static/image18.png)](master-pages-and-site-navigation-cs/_static/image17.png)

**그림 7**:의 디자인 뷰에서 ASP.NET 페이지를 보여 줍니다 모두의 편집 가능 및 비-편집 가능 영역 ([큰 이미지를 보려면 클릭](master-pages-and-site-navigation-cs/_static/image19.png))


경우는 `Default.aspx` 브라우저에서 페이지를 방문, ASP.NET 엔진은 자동으로 페이지의 마스터 페이지 콘텐츠 및 ASP 병합 합니다. 장치와 콘텐츠를 요청한 브라우저에 전송 되는 최종 HTML에 병합 된 콘텐츠를 렌더링 합니다. 마스터 페이지의 콘텐츠 업데이트 되 면이 마스터 페이지를 사용 하는 모든 ASP.NET 페이지는 해당 콘텐츠를 요청 하는 다음에 새 마스터 페이지 콘텐츠를 사용 하 여 remerged 해야 합니다. 단일 페이지에 대 한 마스터 페이지 모델을 사용 하면 간단히 말해 되도록 레이아웃 템플릿 정의 (마스터 페이지) 해당 변경 내용이 전체 사이트에 바로 반영 됩니다.

## <a name="adding-additional-aspnet-pages-to-the-website"></a>웹 사이트에 추가 하는 ASP.NET 페이지 추가

결국 다양 한 보고 데모를 보유 하는 사이트에 ASP.NET 페이지 스텁을 추가 추가 하려면 잠시를 살펴보겠습니다. 자세한 35 데모 전체적으로 하므로 모든 스텁 페이지 보겠습니다 만들지 않고 바로 보다 첫 번째 몇 가지를 만듭니다. 사용 해야 하는 여러 범주의 데모에 있으므로 더 효율적으로 관리할 데모 범주에 대 한 폴더를 추가 합니다. 지금은 다음 세 개의 폴더를 추가 합니다.

- `BasicReporting`
- `Filtering`
- `CustomFormatting`

마지막으로, 그림 8의 솔루션 탐색기에서 표시 된 것과 같이 새 파일을 추가 합니다. 각 파일에 추가 하는 경우 "마스터 페이지 선택" 확인란을 선택 해야 합니다.


![다음 파일 추가](master-pages-and-site-navigation-cs/_static/image20.png)

**그림 8**: 다음 파일 추가


## <a name="step-2-creating-a-site-map"></a>2 단계: 사이트 맵 만들기

구성 페이지의 몇 개 웹 사이트를 관리 하는 문제 중 하나는 방문자가 사이트를 탐색할 수 있는 간단한 방법을 제공 합니다. 시작 하려면 사이트의 탐색 구조를 정의 합니다. 다음으로,이 구조 메뉴 등 이동 경로 탐색 사용자 인터페이스 요소를 변환 해야 합니다. 마지막으로,이 전체 프로세스 유지 관리 하 고 제거 하는 기존 사이트를 새 페이지 추가 됨에 따라 업데이트 해야 합니다. ASP.NET 2.0 이전 개발자, 유지 관리 및 탐색 사용자 인터페이스 요소에 변환에 대 한 자신의 사이트의 탐색 구조를 만드는 방법에 있었습니다. 그러나 ASP.NET 2.0을 사용 하 여 개발자가 활용할 수 있습니다 매우 유연한 사이트 탐색 시스템 기본 제공 합니다.

ASP.NET 2.0 사이트 탐색 시스템 사이트 맵을 정의 하 고 다음 프로그래밍 방식으로 API를 통해이 정보에 액세스 하는 개발자를 위한 방법을 제공 합니다. ASP.NET은 사이트 맵 데이터를 특정 방식으로 형식이 지정 된 XML 파일에 저장할 수를 예상 하는 사이트 맵 공급자를 사용 하 여 제공 됩니다. 그러나 사이트 탐색 시스템은 기반으로 하므로 합니다 [공급자 모델](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx) 사이트 맵 정보를 직렬화 하는 작업에 대 한 대체 방법을 지원 하도록 확장할 수 있습니다. Jeff Prosise의 문서 [The SQL 사이트 맵 공급자를 이전 된 완벽 하 게](https://msdn.microsoft.com/msdnmag/issues/06/02/WickedCode/default.aspx) 사이트 맵 SQL Server 데이터베이스에 저장 하는 사이트 맵 공급자를 만들려면; 만들려면 또 다른 옵션은 하는 방법을 보여 줍니다 [사이트 맵 공급자에 따라 파일 시스템 구조](http://aspnet.4guysfromrolla.com/articles/020106-1.aspx)합니다.

그러나이 자습서에서는 보겠습니다 사용 하 여 제공 되는 기본 사이트 맵 공급자 ASP.NET 2.0을 사용 하 여 합니다. 사이트 맵을 단순히 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭, 새 항목 추가 만든 사이트 맵 옵션을 선택 합니다. 이름으로 그대로 `Web.sitemap` 추가 단추를 클릭 합니다.


[![사이트 맵을 프로젝트에 추가](master-pages-and-site-navigation-cs/_static/image22.png)](master-pages-and-site-navigation-cs/_static/image21.png)

**그림 9**: 사이트 맵을 프로젝트에 추가 ([큰 이미지를 보려면 클릭](master-pages-and-site-navigation-cs/_static/image23.png))


사이트 맵 파일은 XML 파일입니다. Visual Studio는 사이트 맵 구조에 대 한 IntelliSense를 제공 하는 참고 합니다. 사이트 맵 파일이 있어야 합니다 `<siteMap>` 정확 하 게 하나 포함 해야 하는 해당 루트 노드를 노드 `<siteMapNode>` 자식 요소입니다. 먼저 `<siteMapNode>` 포함할 수 있는 다음 요소 하위는 임의의 수 `<siteMapNode>` 요소입니다.

파일 시스템 구조를 모방 하기 위해 사이트 맵을 정의 합니다. 추가 된 `<siteMapNode>` 각 세 개의 폴더 및 자식 요소 `<siteMapNode>` 같이 해당 폴더에 있는 ASP.NET 페이지의 각 요소:

Web.sitemap


[!code-xml[Main](master-pages-and-site-navigation-cs/samples/sample4.xml)]

사이트 맵은 사이트의 다양 한 섹션을 설명 하는 계층 구조는 웹 사이트의 탐색 구조를 정의 합니다. 각 `<siteMapNode>` 요소에서 `Web.sitemap` 사이트의 탐색 구조에서 섹션을 나타냅니다.


[![사이트 맵 탐색 계층 구조를 나타냅니다.](master-pages-and-site-navigation-cs/_static/image25.png)](master-pages-and-site-navigation-cs/_static/image24.png)

**그림 10**: 사이트 맵 탐색 계층 구조를 나타냅니다 ([큰 이미지를 보려면 클릭](master-pages-and-site-navigation-cs/_static/image26.png))


ASP.NET 사이트 맵 구조.NET Framework를 통해 노출 [SiteMap 클래스](https://msdn.microsoft.com/library/system.web.sitemap.aspx)합니다. 이 클래스에는 `CurrentNode` 사용자가 현재 방문; 섹션에 대 한 정보를 반환 하는 속성을 `RootNode` 속성 사이트 맵의 루트를 반환 합니다. (집이 사이트 맵에서). 모두를 `CurrentNode` 및 `RootNode` 속성 반환 [있으면](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx) 속성을 포함 하는 경우와 같은 `ParentNode`를 `ChildNodes`, `NextSibling`, `PreviousSibling`, 등 사이트 맵에 대 한 허용 하는 진행할 계층입니다.

## <a name="step-3-displaying-a-menu-based-on-the-site-map"></a>사이트 맵 기반 메뉴를 표시 하는 3 단계:

ASP.NET 2.0의 데이터에 액세스할 수 ASP.NET에서와 같이 프로그래밍 방식으로 수행 1.x 또는 선언적으로 새 [데이터 소스 컨트롤](https://msdn.microsoft.com/library/ms227679.aspx)합니다. SqlDataSource 컨트롤 클래스 등의 데이터에 액세스 하기 위한 ObjectDataSource 컨트롤, 관계형 데이터베이스 데이터에 액세스 하기 위한 같은 여러 기본 제공 데이터 소스 컨트롤이 있습니다. 만들 수도 있습니다 고유한 [사용자 지정 데이터 소스 컨트롤](https://msdn.microsoft.com/asp.net/reference/data/default.aspx?pull=/library/dnvs05/html/DataSourceCon1.asp)합니다.

데이터 소스 컨트롤 ASP.NET 페이지와 원본 데이터 간의 프록시 역할을 합니다. 데이터 소스 컨트롤의 검색된 데이터를 표시 하려면에서는 일반적으로 페이지에 다른 웹 컨트롤을 추가 하 고 데이터 소스 컨트롤에 바인딩합니다. 웹 컨트롤을 데이터 소스 컨트롤에 바인딩할 단순히 웹 컨트롤의 설정 `DataSourceID` 속성을 데이터 소스 컨트롤의 값 `ID` 속성입니다.

사이트 맵 데이터를 사용 하 여 작업을 지원 하기 위해 ASP.NET 웹 사이트의 사이트 맵에 대 한 웹 컨트롤에 바인딩할 수 있는 SiteMapDataSource 컨트롤을 포함 합니다. 두 웹 컨트롤의 TreeView 및 메뉴 탐색 사용자 인터페이스를 제공 하 여 자주 사용 됩니다. 이러한 두 컨트롤 중 하나에 사이트 맵 데이터를 바인딩할 SiteMapDataSource TreeView와 함께 페이지에 추가 또는 메뉴 컨트롤 `DataSourceID` 속성을 적절 하 게 설정 합니다. 예를 들어, 다음 태그를 사용 하 여 마스터 페이지 메뉴 컨트롤을 추가 수 없습니다.


[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample5.aspx)]

내보낸된 HTML에 대 한 제어를 더 세부적인 수준에 대 한 Repeater 컨트롤, SiteMapDataSource 컨트롤을 바인딩할 수 있습니다 다음과 같이 합니다.


[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample6.aspx)]

SiteMapDataSource 컨트롤 수준을 반환 합니다 사이트 맵 계층 1 번 루트 사이트 맵 노드를 사용 하 여 시작 (집이 사이트 맵에서), (기본 보고, 보고서 필터링 및 사용자 지정 서식 지정) 한 후 다음 수준 및 등입니다. 첫 번째 수준 열거 SiteMapDataSource Repeater에 바인딩할 때 반환 하 고 인스턴스화합니다 합니다 `ItemTemplate` 각각에 대 한 `SiteMapNode` 해당 첫 번째 수준의 인스턴스. 특정 속성에 액세스 하는 `SiteMapNode`를 사용할 수 있습니다 `Eval(propertyName)`를 가져오는 방법에 대해 각각은 `SiteMapNode`의 `Url` 및 `Title` 하이퍼링크 컨트롤에 대 한 속성입니다.

위의 반복기 예제는 다음과 같은 태그가 렌더링 됩니다.


[!code-html[Main](master-pages-and-site-navigation-cs/samples/sample7.html)]

이러한 사이트 맵 노드 (기본 보고, 보고서 필터링 및 사용자 지정 서식 지정)를 구성 하는 *두 번째* 렌더링 되 고 첫 번째 사이트 맵의 수준입니다. 왜냐하면 SiteMapDataSource의 `ShowStartingNode` 속성이 False로 루트 사이트 맵 노드를 무시 하는 사이트 맵 계층에서 두 번째 수준을 반환 하 여 시작 대신 SiteMapDataSource 발생 합니다.

기본 보고, 보고서 필터링 및 사용자 지정 서식 지정에 대 한 자식을 표시할 `SiteMapNode` 개이면 다른 반복기 초기 Repeater를 추가할 수 `ItemTemplate`입니다. 이 두 번째 반복기에 바인딩될 합니다 `SiteMapNode` 인스턴스의 `ChildNodes` 속성을 다음과 같이:


[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample8.aspx)]

이러한 두 반복기 (일부 태그 제거 되었습니다 간략하게 표현 하기 위해) 다음 태그에서 발생 합니다.


[!code-html[Main](master-pages-and-site-navigation-cs/samples/sample9.html)]

선택한 스타일 CSS를 사용 하 여에서 [Rachel Andrew](http://www.rachelandrew.co.uk/)책의 [The CSS Anthology: 101 필수 팁, 요령 &amp; 해킹](https://www.amazon.com/gp/product/0957921888/qid=1137565739/sr=8-1/ref=pd_bbs_1/103-0562306-3386214?n=507846&amp;s=books&amp;v=glance)의 `<ul>` 및 `<li>` 요소의 스타일이 지정 되도록 태그에는 다음 visual 출력이 생성 됩니다.


![두 반복기 및 일부 CSS에서 구성 메뉴](master-pages-and-site-navigation-cs/_static/image27.png)

**그림 11**: 두 개의 반복기 및 일부 CSS에서 구성 메뉴


이 메뉴 마스터 페이지 및에 정의 된 사이트 맵에 바인딩된 `Web.sitemap`즉, 사용 하는 페이지는 사이트 맵 변경 내용이 즉시 반영 됩니다 모든는 `Site.master` 마스터 페이지입니다.

## <a name="disabling-viewstate"></a>ViewState를 사용 하지 않도록 설정

모든 ASP.NET 컨트롤에 해당 상태를 유지할 필요에 따라 수를 [상태를 볼](https://msdn.microsoft.com/msdnmag/issues/03/02/CuttingEdge/), 렌더링된 된 HTML에서 숨겨진된 양식 필드도 serialize 되는 합니다. 뷰 상태 데이터 웹 컨트롤에 바인딩된 데이터가 같은 컨트롤에서 포스트백에서 자신의 프로그래밍 방식으로 변경 상태를 기억 사용 됩니다. 뷰 상태 정보를 다시 게시할 때마다 저장을 허용 하는 동안 클라이언트에 보내야 합니다 및 심각한 페이지 블 로트가 발생 시킬 수 없으면 면밀히 모니터링 하는 태그의 크기를 증가 합니다. 데이터 웹 컨트롤 특히 GridView는 특히 페이지에 수십 개의 추가 킬로바이트의 태그를 추가 합니다. 이러한 증대 광대역 또는 인트라넷 사용자가 무시할 수 있지만, 뷰 상태를 사용 하 여 몇 초 정도 전화 접속 사용자에 대 한 왕복에 추가할 수 있습니다.

상태 보기, 브라우저에서 페이지를 방문 하 고 다음 소스 웹 페이지에서 전송의 영향을 보려면 (Internet Explorer에서 보기 메뉴 및 원본 옵션을 선택). 또한 설정할 수 있습니다 [페이지 추적](https://msdn.microsoft.com/library/sfbfw58f.aspx) 할당 각 페이지의 컨트롤에서 사용 하는 보기 상태를 확인 합니다. 뷰 상태 정보가 라는 숨겨진된 폼 필드에 serialize 되 `__VIEWSTATE`에 있는 `<div>` 바로 뒤 요소 `<form>` 태그입니다. 웹 양식에 사용 되는 경우에 뷰 상태가 유지 됩니다. ASP.NET 페이지에 포함 되지 않은 경우는 `<form runat="server">` 없습니다 해당 선언적 구문에서는 `__VIEWSTATE` 렌더링된 된 태그에서 숨겨진된 폼 필드입니다.

`__VIEWSTATE` 마스터 페이지에 의해 생성 된 양식 필드 생성 되는 페이지의 태그에 약 1,800 바이트를 추가 합니다. Repeater 컨트롤을 주된 이유는이 추가 블 로트가 발생 SiteMapDataSource 컨트롤의 콘텐츠를 뷰 상태 유지 됩니다. 추가 1,800 바이트 얼마나 많은 필드와 레코드를 사용 하 여 GridView를 사용 하는 경우에 대 한 흥미를 보일 수, 하는 동안 뷰 상태를 10 개 이상의 비율로 쉽게 부풀어 오름 수 있습니다.

뷰 상태를 설정 하 여 컨트롤 또는 페이지 수준에서 사용할 수는 `EnableViewState` 속성을 `false`에 렌더링된 된 태그의 크기를 줄입니다. 데이터 웹 컨트롤 유지 하 고 다시 게시할 때마다 데이터 웹 컨트롤에 바인딩된 데이터의 뷰 상태를, 이후 웹 컨트롤의 뷰 상태 데이터를 사용 하지 않도록 설정 하는 경우 데이터 바인딩되어야 모든 포스트백에 합니다. ASP.NET 버전에서 1.x이이 책임은 페이지 개발자; 결코 빠졌습니다 그러나 ASP.NET 2.0을 사용 하 여 데이터 웹 컨트롤은 다시 바인딩 다시 게시할 때마다 해당 데이터 소스 컨트롤에 필요한 경우.

페이지의 뷰 상태를 보겠습니다 줄이려면 설정 Repeater 컨트롤 `EnableViewState` 속성을 `false`입니다. 또는 선언적으로 원본 뷰 디자이너에서 속성 창을 통해이 수행할 수 있습니다. 이렇게 변경한 후 반복기의 선언적 태그 같이 표시 됩니다.


[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample10.aspx)]

이렇게이 변경 하면 페이지의 보기 상태 크기 뿐 축소에 렌더링 후 52 바이트, 97% 절감 보기 상태 크기! 이 시리즈 전체 자습서에서에서는 비활성화 데이터 웹 컨트롤의 뷰 상태를 기본적으로 렌더링된 된 태그의 크기를 줄이기 위해. 대부분의 예제는 `EnableViewState` 속성에 설정할 `false` 언급 없이 수행 하 고 합니다. 에 보기 상태에 설명 합니다는 여기서 데이터에 대 한 순서 대로 설정 해야 하는 시나리오의 웹 예상 되는 기능을 제공 하도록 제어 합니다.

## <a name="step-4-adding-breadcrumb-navigation"></a>4 단계: 추가 이동 경로 탐색

마스터 페이지를 완료 하려면 각 페이지에는 이동 경로 탐색 UI 요소를 추가 해 보겠습니다. 이동 경로 탐색의 현재 위치는 사이트 계층 구조 내에서 사용자를 신속 하 게 보여 줍니다. ASP.NET 2.0의 breadcrumb 쉽습니다 방금 추가 SiteMapPath 컨트롤을 페이지로; 코드가 없는 필요 합니다.

이 사이트에 대 한 헤더에이 컨트롤을 추가 `<div>`:


[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample11.aspx)]

루트까지 사용자는 해당 사이트의 "상위" 맵 노드를 비롯 하 여 사이트 맵 계층 구조에 방문 하 여 이동 경로 탐색이 현재 페이지를 보여 줍니다. (집이 사이트 맵에서).


![현재 페이지를 표시 하는 이동 경로 및 해당 상위 사이트의 계층 구조를 매핑합니다.](master-pages-and-site-navigation-cs/_static/image28.png)

**그림 12**: 현재 페이지를 표시 하는 이동 경로 및 해당 상위 사이트의 계층 구조를 매핑하려면


## <a name="step-5-adding-the-default-page-for-each-section"></a>5 단계: 각 섹션에 대 한 기본 페이지 추가

사이트의 자습서에서는 서로 다른 범주로 기본 보고, 필터링, 사용자 지정 형식 지정 등 각 범주 및 해당 폴더 내의 ASP.NET 페이지와 해당 자습서에 대 한 폴더를 사용 하 여 세분화 됩니다. 또한 각 폴더에는 `Default.aspx` 페이지입니다. 이 기본 페이지에 대 한 모든 현재 섹션에 대 한 자습서를 표시 해 보겠습니다. 즉,에 대 한 합니다 `Default.aspx` 에 `BasicReporting` 폴더 링크를 클릭 해야 하는 `SimpleDisplay.aspx`, `DeclarativeParams.aspx`, 및 `ProgrammaticParams.aspx`합니다. 여기에서 다시 사용할 수 있습니다 합니다 `SiteMap` 에 정의 된 클래스와 데이터 웹 컨트롤 사이트 맵을 기반으로이 정보를 표시할 `Web.sitemap`합니다.

마찬가지로 이번 제목 및 자습서의 설명을 표시 됩니다는 반복기를 사용 하 여 순서 없는 목록에 표시 해 보겠습니다. 태그 및이 수행 하는 코드를 각각에 대해 반복 해야 하므로 `Default.aspx` 페이지에서이 UI 논리를 캡슐화 수 것을 [사용자 정의 컨트롤](https://msdn.microsoft.com/library/y6wb1a0e.aspx)합니다. 이라는 웹 사이트에 폴더를 만듭니다 `UserControls` 라는 웹 사용자 컨트롤 유형의 새 항목을 추가 하 고 `SectionLevelTutorialListing.ascx`, 다음 태그를 추가 하 고:


[![UserControls 폴더에 새 웹 사용자 컨트롤 추가](master-pages-and-site-navigation-cs/_static/image30.png)](master-pages-and-site-navigation-cs/_static/image29.png)

**그림 13**: 새 웹 사용자 컨트롤을 추가 합니다 `UserControls` 폴더 ([클릭 하 여 큰 이미지 보기](master-pages-and-site-navigation-cs/_static/image31.png))


SectionLevelTutorialListing.ascx


[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample12.aspx)]

SectionLevelTutorialListing.ascx.cs


[!code-csharp[Main](master-pages-and-site-navigation-cs/samples/sample13.cs)]

그러나 바인딩된에서는 이전 반복기 예제에서는 `SiteMap` 데이터 Repeater 선언적으로, `SectionLevelTutorialListing` 사용자 컨트롤, 인스턴스까지 프로그래밍 방식으로 합니다. 에 `Page_Load` 이벤트 처리기를이 페이지 URL에서 사이트 맵 노드 매핑되는 s 되도록 하면 검사가 수행 됩니다. 이 사용자 정의 컨트롤을 해당 없는 페이지에 사용 되는 경우 `<siteMapNode>` 항목을 `SiteMap.CurrentNode` 돌아갑니다 `null` 데이터가 없는 Repeater에 바인딩될 및 합니다. 가정 하 고는 `CurrentNode`에 바인딩하기만 해당 `ChildNodes` Repeater 컬렉션. 사이트 맵 설정 되어 있으므로 되도록는 `Default.aspx` 페이지의 각 섹션의 해당 섹션 내에서 자습서의 모든 부모 노드를 아래 스크린샷에서 표시 된 것 처럼이 코드는에 대 한 링크 및 모든 섹션의 자습서의 설명에 표시 됩니다.

이 반복기를 만든 후 엽니다는 `Default.aspx` 폴더의 각 페이지 디자인 보기로 이동 하 여 간단히 사용자 정의 컨트롤에서에서 끌어서 솔루션 탐색기에서 디자인 화면으로 하려는 표시할 자습서 목록입니다.


[![Default.aspx에 추가 된 사용자 컨트롤에](master-pages-and-site-navigation-cs/_static/image33.png)](master-pages-and-site-navigation-cs/_static/image32.png)

**그림 14**: 사용자 정의 컨트롤에 추가할 `Default.aspx` ([클릭 하 여 큰 이미지 보기](master-pages-and-site-navigation-cs/_static/image34.png))


[![기본 보고 자습서 나와 있습니다.](master-pages-and-site-navigation-cs/_static/image36.png)](master-pages-and-site-navigation-cs/_static/image35.png)

**그림 15**:의 기본 보고 자습서 나열 됩니다 ([큰 이미지를 보려면 클릭](master-pages-and-site-navigation-cs/_static/image37.png))


## <a name="summary"></a>요약

정의 된 사이트 맵 및 마스터 페이지 전체를 사용 하 여 이제 일관 된 페이지 레이아웃 및 탐색 체계를 있으므로 데이터 관련 자습서에 대 한 합니다. 당사 사이트로 추가 페이지 수에 관계 없이 사이트 전체 페이지 레이아웃이 나 사이트 탐색 정보를 업데이트 하는 중앙 집중화 되 고이 정보로 인해 빠르고 간단한 프로세스. 페이지 레이아웃 정보를 마스터 페이지에 정의 되어 특히 `Site.master` 에서 매핑할 사이트 `Web.sitemap`합니다. 작성할 필요가 없었습니다 *모든* 이 사이트 전체 페이지 레이아웃 및 탐색 메커니즘을 달성 하기 위해 코드 및 Visual Studio에서 전체 WYSIWYG 디자이너 지원을 유지 합니다.

데이터 액세스 계층 및 비즈니스 논리 레이어 완료 하 고 정의 하는 일관 된 페이지 레이아웃 및 사이트 탐색에 있는 일반적인 보고 패턴 탐색을 시작 하려면 준비 합니다. 에 [다음](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md) 세 개의 자습서 살펴보겠습니다 DetailsView gridview에서 BLL에서 검색 된 데이터를 표시 하는 기본 보고 작업 및 FormView 컨트롤입니다.

즐거운 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 마스터 페이지 개요](https://msdn.microsoft.com/library/wtxbf3hh.aspx)
- [ASP.NET 2.0의에서 마스터 페이지](http://odetocode.com/Articles/419.aspx)
- [ASP.NET 2.0 디자인 템플릿](https://msdn.microsoft.com/asp.net/reference/design/templates/default.aspx)
- [ASP.NET 사이트 탐색 개요](https://msdn.microsoft.com/library/e468hxky.aspx)
- [사이트 탐색의 ASP.NET 2.0 검사](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [ASP.NET 2.0 사이트 탐색 기능](https://weblogs.asp.net/scottgu/archive/2005/11/20/431019.aspx)
- [ASP.NET 뷰 상태 이해](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/viewstate.asp)
- [방법: ASP.NET 페이지에 대 한 추적을 사용 하도록 설정](https://msdn.microsoft.com/library/94c55d08%28VS.80%29.aspx)
- [ASP.NET 사용자 컨트롤](https://msdn.microsoft.com/library/y6wb1a0e.aspx)

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Liz Shulok, Dennis Patterson 및 Hilton giesenow가 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](creating-a-business-logic-layer-cs.md)
> [다음](creating-a-data-access-layer-vb.md)
