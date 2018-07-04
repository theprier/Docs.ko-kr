---
uid: web-forms/overview/data-access/database-driven-site-maps/building-a-custom-database-driven-site-map-provider-vb
title: 사용자 지정 데이터베이스 중심 사이트 맵 공급자 (VB) 빌드 | Microsoft Docs
author: rick-anderson
description: ASP.NET 2.0의 기본 사이트 맵 공급자는 정적 XML 파일에서 해당 데이터를 검색합니다. XML 기반 공급자가 여러 소규모 및 중간 크기에 적합 한 동안...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/26/2007
ms.topic: article
ms.assetid: f904cd2c-a408-4484-9324-8b8d7fe33893
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/database-driven-site-maps/building-a-custom-database-driven-site-map-provider-vb
msc.type: authoredcontent
ms.openlocfilehash: 8e041a5a9163c7f9fe55c6aa06f35301cbdb48a8
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37393972"
---
<a name="building-a-custom-database-driven-site-map-provider-vb"></a>사용자 지정 데이터베이스 중심 사이트 맵 공급자 (VB) 빌드
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_62_VB.zip) 또는 [PDF 다운로드](building-a-custom-database-driven-site-map-provider-vb/_static/datatutorial62vb1.pdf)

> ASP.NET 2.0의 기본 사이트 맵 공급자는 정적 XML 파일에서 해당 데이터를 검색합니다. XML 기반 공급자를 여러 소규모 및 중간 규모의 웹 사이트에 적합 하지만 보다 동적인 사이트 맵을 대규모 웹 응용 프로그램에 필요 합니다. 비즈니스 논리 계층에서 해당 데이터를 검색 하는 사용자 지정 사이트 맵 공급자 빌드 해 보겠습니다이 자습서에서는 다시에서 검색 하는 데이터는 데이터베이스입니다.


## <a name="introduction"></a>소개

ASP.NET 2.0의 사이트 맵 기능을 사용 하면 페이지 개발자가 XML 파일에서와 같은 일부 영구 매체에서 웹 응용 프로그램의 사이트 맵을 정의 합니다. 사이트 맵 데이터 정의 통해 프로그래밍 방식으로 액세스할 수 있습니다 합니다 [ `SiteMap` 클래스](https://msdn.microsoft.com/library/system.web.sitemap.aspx) 에 [ `System.Web` 네임 스페이스](https://msdn.microsoft.com/library/system.web.aspx) 다양 한 탐색을 통해 웹 컨트롤, 같은 또는 SiteMapPath, 메뉴 및 TreeView 컨트롤입니다. 사이트 맵 시스템에서 사용 하 여 [공급자 모델](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx) 다른 사이트 맵 serialization 구현을 생성 하 고 웹 응용 프로그램에 연결할 수 있도록 합니다. ASP.NET 2.0과 함께 제공 되는 기본 사이트 맵 공급자는 XML 파일에 사이트 맵 구조를 유지 합니다. 다시 합니다 [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-vb.md) 라는 파일을 만들었습니다 자습서 `Web.sitemap` 이 구조를 포함 하 고 각 새 자습서 섹션을 사용 하 여 해당 XML 업데이트 되었습니다.

기본 XML 기반 사이트 맵 공급자에는 이러한 자습서에 대 한 사이트 맵의 구조는 상당히 정적인와 같은 경우에 작동 합니다. 그러나 대부분의 시나리오에서 보다 동적인 사이트 맵이 필요 합니다. 그림 1에서 각 범주 및 제품 웹 사이트 s 구조의 섹션으로 표시 하는 위치에 표시 된 사이트 맵을 것이 좋습니다. 이 사이트 맵을 사용 하 여 루트 노드에 해당 하는 웹 페이지를 방문 하 나열 될 수 있습니다 모든 범주를 특정 범주의 웹 페이지를 방문 하는 해당 범주 제품은 나열 하 고 특정 제품의 웹 페이지 보기는 해당 제품 s 세부 정보를 표시 합니다.


[![범주 및 제품 구성 사이트 맵의 구조](building-a-custom-database-driven-site-map-provider-vb/_static/image1.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image1.png)

**그림 1**:의 범주 및 제품 구성 사이트 맵의 구조 ([큰 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image2.png))


이 범주 및 제품 기반 구조에 하드 코딩 될 수는 `Web.sitemap` 파일, 파일 범주 때마다 업데이트 해야 합니다. 또는 제품 추가, 제거 또는 변경 합니다. 따라서 사이트 맵 유지 관리가 크게 간소화 됩니다 해당 구조는 데이터베이스에서 또는 응용 프로그램의 아키텍처의 비즈니스 논리 계층에서 검색 된 경우. 이런 방식으로 제품 및 범주에 추가 된, 바꾸거나, 삭제, 사이트 맵이 변경 사항을 반영 하도록 자동으로 업데이트 합니다.

ASP.NET 2.0의 사이트 맵 serialization으로 공급자 모델 빌드 되었기 때문 데이터베이스 또는 아키텍처와 같은 대체 데이터 저장소에서 데이터를 가져오는 고유한 사용자 지정 사이트 맵 공급자를 만들 수 있습니다. 이 자습서에서는에서는 BLL에서 해당 데이터를 검색 하는 사용자 지정 공급자를 빌드합니다. Let s 시작!

> [!NOTE]
> 이 자습서에서 만든 사용자 지정 사이트 맵 공급자가 응용 프로그램의 아키텍처 및 데이터 모델에 밀접 하 게 합니다. Jeff Prosise s [SQL Server의 사이트 맵 저장](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/) 하 고 [적 기다리고 SQL 사이트 맵 공급자](https://msdn.microsoft.com/msdnmag/issues/06/02/wickedcode/default.aspx) 문서를 SQL Server의 사이트 맵 데이터를 저장 하는 일반화 된 방식을 검사 합니다.


## <a name="step-1-creating-the-custom-site-map-provider-web-pages"></a>1 단계: 사용자 지정 사이트 맵 공급자의 웹 페이지 만들기

사용자 지정 사이트 맵 공급자를 만들기 시작 하기 전에 먼저이 자습서에 대 한 필요 하 여 ASP.NET 페이지를 추가 하는 s 수 있습니다. 라는 새 폴더를 추가 하 여 시작 `SiteMapProvider`합니다. 다음에 있는 각 페이지에 연결할 수 있도록 해당 폴더에 다음 ASP.NET 페이지를 추가 합니다 `Site.master` 마스터 페이지:

- `Default.aspx`
- `ProductsByCategory.aspx`
- `ProductDetails.aspx`

추가 `CustomProviders` 하위 폴더는 `App_Code` 폴더입니다.


![사이트 맵 공급자 관련 자습서에 대 한 ASP.NET 페이지 추가](building-a-custom-database-driven-site-map-provider-vb/_static/image2.gif)

**그림 2**: ASP.NET 페이지는 사이트에 대 한 공급자 관련 자습서 매핑 추가


T 필요 하지에서는이 섹션에 대 한 하나의 자습서 이므로 `Default.aspx` s 자습서를 나열 합니다. 대신 `Default.aspx` GridView 컨트롤의 범주가 표시 됩니다. 해결할이 2 단계.

다음으로 업데이트 `Web.sitemap` 에 대 한 참조를 포함 하는 `Default.aspx` 페이지입니다. 특히 캐싱 후 다음 태그를 추가 `<siteMapNode>`:


[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample1.xml)]

업데이트 한 후 `Web.sitemap`, 잠시 브라우저를 통해 자습서 웹 사이트를 확인 합니다. 이제 메뉴 왼쪽에서 유일한 사이트 맵 공급자 자습서에 대 한 항목을 포함합니다.


![사이트 맵 사이트 맵 공급자 자습서에 대 한 항목이 포함](building-a-custom-database-driven-site-map-provider-vb/_static/image3.gif)

**그림 3**: 사이트 맵 사이트 맵 공급자 자습서에 대 한 항목이 포함


이 자습서가 주로 집중 설명 하는 데 사용자 지정 사이트 맵 공급자를 만들고 해당 공급자를 사용 하 여 웹 응용 프로그램을 구성 합니다. 특히, 그림 1에 표시 된 대로 각 범주 및 제품에 대 한 노드가 함께 루트 노드를 포함 하는 사이트 맵을 반환 하는 공급자를 빌드 해 보겠습니다. 일반적으로 사이트 맵에 있는 각 노드의 URL을 지정할 수 있습니다. 사이트 맵의 루트 노드의 URL은 `~/SiteMapProvider/Default.aspx`, 모든 데이터베이스의 범주를 표시 합니다. 사이트 맵에 있는 각 범주 노드를 가리키는 URL을 갖게 됩니다 `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID=categoryID`에 모든 나열 하는 지정 된 제품 *categoryID*합니다. 마지막으로, 각 제품 사이트 맵 노드를 가리킵니다 `~/SiteMapProvider/ProductDetails.aspx?ProductID=productID`, 특정 제품 s 세부 정보 표시 됩니다.

시작 하려면 만들어야 합니다 `Default.aspx`, `ProductsByCategory.aspx`, 및 `ProductDetails.aspx` 페이지입니다. 이러한 페이지는 각각 2, 3 및 4 단계에서 완료 됩니다. 사이트 맵 공급자에이 자습서를 위한 것 이므로 지난 자습서 만들기 포함 되므로 이러한 종류의 다중 페이지 마스터/세부 정보 보고서 및,-4 단계 2를 통해 서 두는 것입니다. 여러 페이지에 걸쳐 마스터/세부 정보 보고서 작성에 리프레셔가 필요한 경우 다시 참조를 [마스터/세부 정보 필터링에서 두 페이지가](../masterdetail/master-detail-filtering-across-two-pages-vb.md) 자습서입니다.

## <a name="step-2-displaying-a-list-of-categories"></a>2 단계: 범주 목록이 표시

열기는 `Default.aspx` 페이지를 `SiteMapProvider` 폴더 및 설정 디자이너 도구 상자에서 GridView 끌어서 해당 `ID` 에 `Categories`합니다. GridView가 스마트 태그에서 바인딩할 라는 한 새 ObjectDataSource `CategoriesDataSource` 사용 하 여 해당 데이터를 검색할 수 있도록 구성 하 고는 `CategoriesBLL` s 클래스 `GetCategories` 메서드. 만이 GridView 범주를 표시 하 고 데이터 수정 기능을 제공 하지 않습니다, UPDATE, INSERT에서에서 드롭 다운 목록을 설정 하 고 탭 (없음)를 삭제 합니다.


[![GetCategories 메서드를 사용 하 여 범주를 반환 하는 ObjectDataSource 구성](building-a-custom-database-driven-site-map-provider-vb/_static/image4.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image3.png)

**그림 4**: 범주 사용을 반환 하는 ObjectDataSource를 구성 합니다 `GetCategories` 메서드 ([클릭 하 여 큰 이미지 보기](building-a-custom-database-driven-site-map-provider-vb/_static/image4.png))


[![UPDATE, INSERT 드롭 다운 목록을 설정 하 고 탭 삭제 (없음)](building-a-custom-database-driven-site-map-provider-vb/_static/image5.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image5.png)

**그림 5**: 드롭다운 목록에서 업데이트, 삽입 및 삭제 탭 하도록 설정 (없음) ([큰 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image6.png))


데이터 소스 구성 마법사를 완료 한 후 Visual Studio에 대 한 BoundField 추가 `CategoryID`, `CategoryName`, `Description`합니다 `NumberOfProducts`, 및 `BrochurePath`합니다. 만 포함 되도록 GridView 편집 합니다 `CategoryName` 및 `Description` BoundFields 및 업데이트를 `CategoryName` BoundField의 `HeaderText` 범주에는 속성.

다음으로 HyperLinkField를 추가 하 고 따라서 배치 한다는의 가장 왼쪽 필드입니다. 설정 된 `DataNavigateUrlFields` 속성을 `CategoryID` 하며 `DataNavigateUrlFormatString` 속성을 `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID={0}`입니다. 설정 된 `Text` 보기 제품에는 속성입니다.


![범주 GridView에는 HyperLinkField 추가](building-a-custom-database-driven-site-map-provider-vb/_static/image6.gif)

**그림 6**:를 HyperLinkField 추가 `Categories` GridView


ObjectDataSource를 만들고 GridView의 필드를 사용자 지정 후 두 개의 선언적 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample2.aspx)]

그림 7은 `Default.aspx` 브라우저를 통해 볼 때. S 제품 보기 범주를 클릭 하면 링크 하면 `ProductsByCategory.aspx?CategoryID=categoryID`, 3 단계에서에서 빌드할 것입니다.


[![보기 제품 링크를 사용 하 여 함께 나열 된 각 범주는](building-a-custom-database-driven-site-map-provider-vb/_static/image7.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image7.png)

**그림 7**: 보기 제품 링크를 사용 하 여 함께 나열 된 각 범주는 ([큰 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image8.png))


## <a name="step-3-listing-the-selected-category-s-products"></a>선택한 범주의 제품을 나열 하는 3 단계:

엽니다는 `ProductsByCategory.aspx` 페이지 및 추가 이름을 지정 하는 GridView `ProductsByCategory`합니다. 스마트 태그를 바인딩할 GridView 라는 새로운 ObjectDataSource는 `ProductsByCategoryDataSource`합니다. ObjectDataSource 사용 하도록 구성 합니다 `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)` 메서드 집합과 드롭다운 목록 (None) UPDATE, INSERT 및 DELETE 탭에 있습니다.


[![ProductsBLL 클래스의 GetProductsByCategoryID(categoryID) 메서드를 사용 하 여](building-a-custom-database-driven-site-map-provider-vb/_static/image8.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image9.png)

**그림 8**: 사용 된 `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)` 메서드 ([클릭 하 여 큰 이미지 보기](building-a-custom-database-driven-site-map-provider-vb/_static/image10.png))


데이터 소스 구성 마법사의 마지막 단계에 대 한 매개 변수 소스 묻는 *categoryID*합니다. 이 정보는 쿼리 문자열 필드를 통해 전달 되므로 `CategoryID`QueryString 드롭 다운 목록에서 선택 하 고 그림 9 에서처럼 CategoryID QueryStringField 텍스트 상자에 입력 합니다. 마법사를 완료 하려면 마침을 클릭 합니다.


[![CategoryID Querystring 필드를 사용 하 여 categoryid 매개 변수](building-a-custom-database-driven-site-map-provider-vb/_static/image9.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image11.png)

**그림 9**: 사용 합니다 `CategoryID` 에 대 한 Querystring 필드를 *categoryID* 매개 변수 ([클릭 하 여 큰 이미지 보기](building-a-custom-database-driven-site-map-provider-vb/_static/image12.png))


마법사를 완료 한 후 Visual Studio가 해당 BoundFields 및는 CheckBoxField 제품 데이터 필드에 대 한 GridView에 추가 합니다. 제거를 제외한 모든 `ProductName`, `UnitPrice`, 및 `SupplierName` BoundFields 합니다. 이러한 세 가지 BoundFields 사용자 지정 `HeaderText` 제품, 가격 및 공급 업체을 각각 읽을 속성입니다. 형식으로 `UnitPrice` 통화로 BoundField 합니다.

다음으로 HyperLinkField를 추가 하 고 맨 왼쪽 위치로 이동 합니다. 설정 해당 `Text` 속성 세부 정보를 보려면, 해당 `DataNavigateUrlFields` 속성을 `ProductID`, 및 해당 `DataNavigateUrlFormatString` 속성을 `~/SiteMapProvider/ProductDetails.aspx?ProductID={0}`입니다.


![ProductDetails.aspx 가리키는 보기 세부 정보 HyperLinkField를 추가 합니다.](building-a-custom-database-driven-site-map-provider-vb/_static/image10.gif)

**그림 10**: 뷰를 가리키는 HyperLinkField 세부 정보 추가 `ProductDetails.aspx`


이러한 사용자 지정을 마치면 GridView 및 ObjectDataSource가 선언적 태그는 다음과 같아야 합니다.


[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample3.aspx)]

보기 돌아갑니다 `Default.aspx` 음료에 대 한 링크를 통해 브라우저를 제품 보기를 클릭 합니다. 이렇게 하면 `ProductsByCategory.aspx?CategoryID=1`, 음료 범주에 속하는 Northwind 데이터베이스의 이름, 가격 및 제품의 공급 업체 표시 (그림 11 참조). 범주 목록 페이지에 사용자를 반환 하는 링크를 포함 하려면이 페이지를 좀 더 강화 하려면 자유롭게 (`Default.aspx`) 및 DetailsView 또는 FormView 컨트롤을 선택한 범주의 이름 및 설명을 표시 합니다.


[![음료 이름, 가격 및 공급 업체 표시 됩니다.](building-a-custom-database-driven-site-map-provider-vb/_static/image11.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image13.png)

**그림 11**: The 음료 이름, 가격 및 공급 업체 표시 됩니다 ([큰 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image14.png))


## <a name="step-4-showing-a-product-s-details"></a>4 단계: 제품 s 세부 정보를 표시합니다.

마지막 페이지 `ProductDetails.aspx`, 선택한 제품 세부 정보를 표시 합니다. 열기 `ProductDetails.aspx` 디자이너 도구 상자에서을 DetailsView를 끕니다. 집합 DetailsView s `ID` 속성을 `ProductInfo` 지울 및 해당 `Height` 고 `Width` 속성 값입니다. 스마트 태그를 바인딩할 DetailsView 라는 한 새 ObjectDataSource `ProductDataSource`, ObjectDataSource에서 해당 데이터를 가져오도록 구성 합니다 `ProductsBLL` s 클래스 `GetProductByProductID(productID)` 메서드. 2, 3 단계에서 만든 이전 웹 페이지와 마찬가지로 UPDATE, INSERT에서에서 드롭 다운 목록을 설정 하 고 탭 (없음)를 삭제 합니다.


[![GetProductByProductID(productID) 메서드를 사용 하는 ObjectDataSource 구성](building-a-custom-database-driven-site-map-provider-vb/_static/image12.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image15.png)

**그림 12**: ObjectDataSource 사용 하도록 구성 된 `GetProductByProductID(productID)` 메서드 ([클릭 하 여 큰 이미지 보기](building-a-custom-database-driven-site-map-provider-vb/_static/image16.png))


원본에 대 한 프롬프트 데이터 소스 구성 마법사의 마지막 단계는 *productID* 매개 변수입니다. 쿼리 문자열 필드를 통해이 데이터가 있으므로 `ProductID`, QueryString을 ProductID QueryStringField 텍스트 상자의 드롭 다운 목록을 설정 합니다. 마지막으로 마법사를 완료 하려면 "마침" 단추를 클릭 합니다.


[![ProductID ProductID Querystring 필드에서 해당 값을 가져오려고 매개 변수를 구성 합니다.](building-a-custom-database-driven-site-map-provider-vb/_static/image13.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image17.png)

**그림 13**: 구성 된 *productID* 매개 변수에서 값을 가져오려고 합니다 `ProductID` Querystring 필드 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image18.png))


데이터 소스 구성 마법사를 완료 한 후 Visual Studio가 해당 BoundFields 및는 CheckBoxField에서 제품 데이터 필드에 대 한 DetailsView 만듭니다 됩니다. 제거 합니다 `ProductID`, `SupplierID`, 및 `CategoryID` BoundFields 하다 면 나머지 필드를 구성 합니다. 소수의 시각적인 구성 후 내 DetailsView 및 ObjectDataSource가 선언적 태그는 다음과 같았습니다.


[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample4.aspx)]

이 페이지를 테스트 하려면 돌아갑니다 `Default.aspx` 음료 범주에 대 한 제품 보기에서 클릭 합니다. 음료 제품의 목록에 Chai 차에 대 한 세부 정보 보기 링크를 클릭 합니다. 이렇게 하면 `ProductDetails.aspx?ProductID=1`, Chai Tea s를 보여 주는 세부 정보 (그림 14 참조).


[![Chai Tea s 공급 업체, 범주, 가격 및 기타 정보 표시](building-a-custom-database-driven-site-map-provider-vb/_static/image14.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image19.png)

**그림 14**: Chai Tea s 공급 업체, 범주, 가격 및 기타 정보 표시 됩니다 ([큰 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image20.png))


## <a name="step-5-understanding-the-inner-workings-of-a-site-map-provider"></a>5 단계: 사이트 맵 공급자의 내부 작업 이해

사이트 맵 컬렉션으로 웹 서버의 메모리에 표시 됩니다 `SiteMapNode` 인스턴스는 계층 구조를 형성 합니다. 정확히 하나의 루트 여야 하 고 모든 루트가 아닌 노드에 부모 노드가 하나만 있어야 합니다. 모든 노드는 임의 개수의 자식 있을 수 있습니다. 각 `SiteMapNode` 일반적으로 이러한 섹션에는 해당 웹 페이지가; 개체에는 웹 사이트 s 구조의 섹션을 나타냅니다. 결과적으로 [ `SiteMapNode` 클래스](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx) 와 같은 속성이 `Title`를 `Url`, 및 `Description`, 섹션에 대 한 정보를 제공 하는 `SiteMapNode` 나타냅니다. 도 `Key` 각각 고유 하 게 식별 하는 속성 `SiteMapNode` 이 계층 구조를 설정 하는 데 사용 되는 속성 뿐만 아니라 계층 `ChildNodes`, `ParentNode`를 `NextSibling`, `PreviousSibling`등.

그림 15에서는 그림 1에서 하지만 보다 자세히 살펴본 구현 세부 정보를 사용 하 여 일반 사이트 맵 구조를 보여 줍니다.


[![각 있으면이 속성 같은 Title, Url, 키 및 등](building-a-custom-database-driven-site-map-provider-vb/_static/image16.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image15.gif)

**그림 15**: 각 `SiteMapNode` 와 같은 속성에 `Title`, `Url`를 `Key`등과 ([클릭 하 여 큰 이미지 보기](building-a-custom-database-driven-site-map-provider-vb/_static/image17.gif))


사이트 맵을 통해 액세스할 수 합니다 [ `SiteMap` 클래스](https://msdn.microsoft.com/library/system.web.sitemap.aspx) 에 [ `System.Web` 네임 스페이스](https://msdn.microsoft.com/library/system.web.aspx)합니다. 이 클래스는 s `RootNode` 사이트 맵을의 루트를 반환 하는 속성 `SiteMapNode` 인스턴스; `CurrentNode` 반환 합니다 `SiteMapNode` 인 `Url` 속성에는 현재 요청 된 페이지의 URL과 일치 합니다. 이 클래스는 ASP.NET 2.0의 탐색 웹 컨트롤에 의해 내부적으로 사용 됩니다.

경우는 `SiteMap`의 클래스 속성에 액세스, 메모리로 일부 영구 매체에서 사이트 맵 구조를 serialize 해야 하 합니다. 그러나 사이트 맵 직렬화 논리는 어렵지 않습니다에 코딩 된 `SiteMap` 클래스입니다. 대신 런타임에 합니다 `SiteMap` 클래스에는 사이트 맵 결정 *공급자* serialization에 사용할 합니다. 기본적으로 [ `XmlSiteMapProvider` 클래스](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx) 사용 되는 올바른 형식의 XML 파일에서 사이트 맵의 구조를 소리내어 합니다. 그러나 약간의 작업을 사용 하 여 고유한 사용자 지정 사이트 맵 공급자를 만들 수 있습니다.

모든 사이트 맵 공급자에서 파생 되어야 합니다는 [ `SiteMapProvider` 클래스](https://msdn.microsoft.com/library/system.web.sitemapprovider.aspx)필수 메서드를 포함 하는 고 사이트에 필요한 속성 공급자 매핑하지만 다양 한 구현 세부 정보를 생략 합니다. 두 번째 클래스인 [ `StaticSiteMapProvider` ](https://msdn.microsoft.com/library/system.web.staticsitemapprovider.aspx)를 확장 합니다 `SiteMapProvider` 클래스 및 더욱 강력한 구현은 필요한 기능을 포함 합니다. 내부적으로 `StaticSiteMapProvider` 저장 합니다 `SiteMapNode` 에 매핑할 사이트의 인스턴스를 `Hashtable` 와 같은 메서드를 제공 하 고 `AddNode(child, parent)`, `RemoveNode(siteMapNode),` 및 `Clear()` 를 추가 및 제거 `SiteMapNode` 내부를 `Hashtable`. `XmlSiteMapProvider`는 `StaticSiteMapProvider`에서 파생됩니다.

확장 하는 사용자 지정 사이트 맵 공급자를 만들 때 `StaticSiteMapProvider`, 두 가지가 있습니다 추상 재정의 해야 합니다: [ `BuildSiteMap` ](https://msdn.microsoft.com/library/system.web.staticsitemapprovider.buildsitemap.aspx) 하 고 [ `GetRootNodeCore` ](https://msdn.microsoft.com/library/system.web.sitemapprovider.getrootnodecore.aspx)합니다. `BuildSiteMap`해당 이름에서 알 수 있듯이 영구 저장소에서 사이트 맵 구조를 로드 하 고 메모리에서 생성 하는 일을 담당 합니다. `GetRootNodeCore` 사이트 맵의 루트 노드를 반환합니다.

웹 되기 전 응용 프로그램 응용 프로그램의 구성에 등록 해야 하는 사이트 맵 공급자를 사용할 수 있습니다. 기본적으로 `XmlSiteMapProvider` 클래스의 이름을 사용 하 여 등록 `AspNetXmlSiteMapProvider`합니다. 추가 사이트 맵 공급자를 등록 하려면 다음 태그를 추가 `Web.config`:


[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample5.xml)]

합니다 *이름을* 하는 동안 공급자에 알기 쉬운 이름을 할당 하는 값 *형식* 사이트 맵 공급자의 정규화 된 형식 이름을 지정 합니다. 에 대 한 구체적인 값을 살펴보겠습니다 합니다 *이름* 및 *형식* 7 단계에서에서 값 ve 우리의 사용자 지정 사이트 맵 공급자를 만들었으면 했습니다.

사이트 맵 공급자 클래스에서 액세스할 때 처음으로 인스턴스화될는 `SiteMap` 클래스 및 웹 응용 프로그램의 수명 동안 메모리에 유지 됩니다. 여러 개의 동시 웹 사이트 방문자에서 호출할 수 있는 사이트 맵 공급자의 인스턴스가 하나만 있으면 이므로 공급자가의 메서드 되도록 명령적 *스레드로부터 안전한*합니다.

성능 및 확장성을 높이기 위해 해당 s 메모리 내 사이트를 캐시 하는 것이 중요 한 구조를 매핑하고 반환 될 때마다 다시 하는 것이 아니라 구조 캐시 하는이 `BuildSiteMap` 메서드가 호출 됩니다. `BuildSiteMap` 페이지 및 사이트 맵 구조의 깊이에서 사용 하 여 있는 탐색 컨트롤에 따라 사용자 당 페이지 요청에 따라 여러 번 호출할 수 있습니다. 모든 경우에서 사이트 맵 구조 캐시 안 함에서는 `BuildSiteMap` 아키텍처 (결과적으로 쿼리에서 데이터베이스로)에서 제품 테이블과 범주 정보를 다시 검색할 해야 됩니다 될 때마다 호출 됩니다. 캐싱 이전 자습서에서 설명한 대로 캐시 된 데이터 부실 해질 수 있습니다. 이 대처 하기 위해 시간 또는 SQL 캐시 종속성 기반 expiries 사용할 수 있습니다.

> [!NOTE]
> 사이트 맵 공급자를 선택적으로 재정의할 수 있습니다 합니다 [ `Initialize` 메서드](https://msdn.microsoft.com/library/system.web.sitemapprovider.initialize.aspx)합니다. `Initialize` 사이트 맵 공급자가 처음 인스턴스화 및 공급자에 할당 된 사용자 지정 특성이 전달 될 때 호출 되 `Web.config` 에 `<add>` 와 같은 요소: `<add name="name" type="type" customAttribute="value" />`합니다. 공급자가의 코드를 수정 하지 않고도 다양 한 사이트 맵 공급자 관련 설정을 지정 하는 페이지 개발자를 허용 하려는 경우 유용 합니다. 예를 들어, 범주 및 제품 데이터와는 반대로 d에서는 아키텍처를 통해 데이터베이스에서 직접 가능성이 읽고 된에서는 하 게 하려면를 통해 데이터베이스 연결 문자열을 지정 하는 페이지 개발자 `Web.config` 하드 코드를 사용 하는 대신 공급자가의 코드에 대 한 값입니다. 6 단계에서에서 빌드 해 보겠습니다 사용자 지정 사이트 맵 공급자가를 재정의 하지 않는 `Initialize` 메서드. 사용 하는 예는 `Initialize` 메서드를 가리킵니다 [Jeff Prosise](http://www.wintellect.com/Weblogs/CategoryView,category,Jeff%20Prosise.aspx) s [SQL Server의 사이트 맵 저장](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/) 문서.


## <a name="step-6-creating-the-custom-site-map-provider"></a>6 단계: 사용자 지정 사이트 맵 공급자 만들기

Northwind 데이터베이스의 제품 범주와 사이트 맵을 작성 하는 사용자 지정 사이트 맵 공급자를 만들려면 확장 하는 클래스를 생성 해야 `StaticSiteMapProvider`합니다. 1 단계에서에서 라고 했 추가 `CustomProviders` 폴더에는 `App_Code` 폴더-이 폴더에 새 클래스를 추가 `NorthwindSiteMapProvider`합니다. `NorthwindSiteMapProvider` 클래스에 다음 코드를 추가합니다.


[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample6.vb)]

이 클래스 s 탐색 시작 s `BuildSiteMap` 메서드를 사용 하 여 시작을 [ `lock` 문을](https://msdn.microsoft.com/library/c5kehkcz.aspx)합니다. `lock` 문은 있으므로 해당 코드에 대 한 액세스를 직렬화 하 고 서로 s 발가락에 한 단계씩 실행할 두 개의 동시 스레드를 차단 입력을 한 번에 하나의 스레드만 허용 합니다.

클래스 수준 `SiteMapNode` 변수 `root` 사이트 맵 구조를 캐시 하는 데 사용 됩니다. 처음으로 또는 기본 데이터를 수정한 후 처음으로 사이트 맵에서 생성 될 때 `root` 됩니다 `Nothing` 사이트 맵 구조 만들어집니다. 에 할당 된 사이트 맵의 루트 노드 `root` 생성 하는 동안 프로세스는 다음에이 메서드는 호출 `root` 됩니다 `Nothing`합니다. 따라서 하기만 `root` 아닙니다 `Nothing` 다시 만들 필요 없이 사이트 맵 구조를 호출자에 게 반환 됩니다.

루트가 `Nothing`, 범주 및 제품 정보에서 사이트 맵 구조 만들어집니다. 사이트 맵을 만들어 빌드되는 `SiteMapNode` 인스턴스 및 다음 호출을 통해 계층 구조를 형성 합니다 `StaticSiteMapProvider` s 클래스 `AddNode` 메서드. `AddNode` 저장 된 다양 한 내부 정리 작업 수행 `SiteMapNode` 인스턴스는 `Hashtable`합니다. 계층 생성을 시작 하기 전에 호출 하 여 시작 합니다 `Clear` 메서드 내부에서 요소를 지웁니다 `Hashtable`합니다. 다음으로 `ProductsBLL` s 클래스 `GetProducts` 메서드와 결과 `ProductsDataTable` 로컬 변수에 저장 됩니다.

루트 노드를 만들고 할당 하 여 사이트 맵의 생성 시작 `root`합니다. 오버 로드는 [ `SiteMapNode` s 생성자](https://msdn.microsoft.com/library/system.web.sitemapnode.sitemapnode.aspx) 여기 고이 전체에서 사용 되는 `BuildSiteMap` 다음 정보를 전달:

- 사이트 맵 공급자에 대 한 참조 (`Me`).
- 합니다 `SiteMapNode` s `Key`입니다. 이 값은 각각에 대해 고유 해야 합니다. 필수 `SiteMapNode`합니다.
- 합니다 `SiteMapNode` s `Url`입니다. `Url` 선택적 이며 각 제공 하는 경우 `SiteMapNode` s `Url` 값은 고유 해야 합니다.
- `SiteMapNode` s `Title`에 필요 합니다.

`AddNode(root)` 메서드 호출을 추가 합니다 `SiteMapNode` `root` 루트로 사이트 맵. 그런 다음 각 `ProductRow` 에 `ProductsDataTable` 열거 됩니다. 경우 이미 존재는 `SiteMapNode` 현재 s 제품 범주에 대 한 참조입니다. 이 고, 그렇지 새 `SiteMapNode` 범주 만들어지고의 자식으로 추가 합니다 `SiteMapNode``root` 를 통해를 `AddNode(categoryNode, root)` 메서드 호출 합니다. 적절 한 범주 뒤 `SiteMapNode` 노드 발견 되었거나 생성을 `SiteMapNode` 이 현재 제품에 대해 만들어지고 범주의 자식으로 추가 `SiteMapNode` 를 통해 `AddNode(productNode, categoryNode)`합니다. 범주 `SiteMapNode` s `Url` 속성 값이 `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID=categoryID` 제품 while `SiteMapNode` s `Url` 속성은 할당 `~/SiteMapNode/ProductDetails.aspx?ProductID=productID`합니다.

> [!NOTE]
> 데이터베이스에 있는 해당 제품 `NULL` 값에 대 한 해당 `CategoryID` 범주 아래에 그룹화 됩니다 `SiteMapNode` 인 `Title` None 및 해당 속성은 `Url` 속성을 빈 문자열로 설정 됩니다. 설정 하기로 `Url` 이후 빈 문자열로 합니다 `ProductBLL` s 클래스 `GetProductsByCategory(categoryID)` 메서드는 현재 사용 하 여 해당 제품을 반환 하는 기능에는 `NULL` `CategoryID` 값입니다. 또한 탐색 컨트롤을 렌더링 하는 방법을 보여 주고자.는 `SiteMapNode` 에 값이 없는 해당 `Url` 속성입니다. 이 자습서를 확장 하 게 하시기 바랍니다 있도록 None `SiteMapNode` s `Url` 속성이 가리키는 `ProductsByCategory.aspx`, 아직 제품과 표시 됩니다 `NULL` `CategoryID` 값입니다.


사이트 맵, 생성 한 후 임의 개체에서 SQL 캐시 종속성을 사용 하 여 데이터 캐시에 추가 됩니다는 `Categories` 및 `Products` 를 통해 테이블을 `AggregateCacheDependency` 개체입니다. 이전 자습서에서는 SQL 캐시 종속성을 사용 하 여 살펴보았습니다 *를 사용 하 여 SQL 캐시 종속성*합니다. 하지만 사용자 지정 사이트 맵 공급자가의 데이터 캐시의 오버 로드를 사용 `Insert` 메서드는 ve 아직를 탐색 합니다. 이 오버 로드는 대리자 개체는 캐시에서 제거 될 때 호출 되는 마지막 입력된 매개 변수로 허용 합니다. 새 전달 특히 [ `CacheItemRemovedCallback` 대리자](https://msdn.microsoft.com/library/system.web.caching.cacheitemremovedcallback.aspx) 가리키는 `OnSiteMapChanged` 메서드가 정의 아래에는 `NorthwindSiteMapProvider` 클래스.

> [!NOTE]
> 사이트 맵의 메모리 내 표현을 클래스 수준 변수를 통해 캐시 된 `root`합니다. 사용자 지정 사이트 맵 공급자 클래스 및 해당 인스턴스는 웹 응용 프로그램에서 모든 스레드 간에 공유 되므로 하나의 인스턴스만 이므로이 클래스 변수에 캐시 역할도 합니다. 합니다 `BuildSiteMap` 메서드 또한 사용 하 여 데이터 캐시에만 기본 데이터베이스 데이터의 경우 알림을 받을 수 있는 방법을 합니다 `Categories` 또는 `Products` 변경 내용 테이블입니다. 참고 현재 날짜 및 시간 데이터 캐시에 추가할 값입니다. 실제 사이트 지도 데이터가 *되지* 데이터 캐시에 저장 합니다.


`BuildSiteMap` 메서드 사이트 맵의 루트 노드를 반환 하 여 완료 합니다.

나머지 메서드는 매우 간단 합니다. `GetRootNodeCore` 루트 노드를 반환 하는 일을 담당 합니다. 이후 `BuildSiteMap` 루트를 반환 합니다 `GetRootNodeCore` 반환 하기만 `BuildSiteMap`의 값을 반환 합니다. 합니다 `OnSiteMapChanged` 메서드 집합 `root` 돌아가기 `Nothing` 캐시 항목이 제거 되는 경우. 다시 설정 하는 루트를 사용 하 여 `Nothing`, 다음에 `BuildSiteMap` 은 호출 사이트 맵 구조 다시 작성 됩니다. 마지막으로 `CachedDate` 이러한 값이 있는 경우 데이터 캐시에 저장 된 날짜 및 시간 값을 반환 합니다. 사이트 맵 데이터를 마지막으로 캐싱된 결정할 페이지 개발자가이 속성을 사용할 수 있습니다.

## <a name="step-7-registering-thenorthwindsitemapprovider"></a>7 단계: 등록 된`NorthwindSiteMapProvider`

사용 하도록 웹 응용 프로그램에 대 한 순서 대로 `NorthwindSiteMapProvider` 6 단계에서에서 만든 사이트 맵 공급자에 등록 해야 합니다 `<siteMap>` 부분 `Web.config`합니다. 특히, 내에서 다음 태그를 추가 합니다 `<system.web>` 요소에서 `Web.config`:


[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample7.xml)]

이 태그는 두 가지: 함을 나타냅니다 먼저 기본 제공 `AspNetXmlSiteMapProvider` 는 기본 사이트 맵 공급자; 둘째, 친숙 한 이름을 Northwind 사용 하 여 6 단계에서에서 만든 사용자 지정 사이트 맵 공급자를 등록 합니다.

> [!NOTE]
> 응용 프로그램 s에 있는 사이트 맵 공급자에 대 한 `App_Code` 폴더의 값을 `type` 특성은 단순히 클래스 이름입니다. 또는 사용자 지정 사이트 맵 공급자 수에 만들어져 별도 클래스 라이브러리 프로젝트를 웹 응용 프로그램에서에서 배치 된 컴파일된 어셈블리를 사용 하 여 `/Bin` 디렉터리입니다. 이런 경우는 `type` 특성 값 *Namespace*. *ClassName*하십시오 *AssemblyName* 합니다.


업데이트 한 후 `Web.config`, 잠시 시간을 브라우저에서 자습서를 통해 페이지를 볼 수 있습니다. 왼쪽의 탐색 인터페이스 섹션을 계속 표시 하 고 자습서에 정의 된 `Web.sitemap`합니다. 남아 있는 것 이므로 `AspNetXmlSiteMapProvider` 기본 공급자로 합니다. 사용 하는 탐색 사용자 인터페이스 요소를 만들기 위해는 `NorthwindSiteMapProvider`, Northwind 사이트 맵 공급자를 사용 해야 함을 명시적으로 지정 해야 합니다. 8 단계에서에서이 작업을 수행 하는 방법을 살펴보겠습니다.

## <a name="step-8-displaying-site-map-information-using-the-custom-site-map-provider"></a>8 단계: 사용자 지정 사이트 맵 공급자를 사용 하 여 사이트 맵 정보를 표시 합니다.

사용자 지정 사이트 맵 공급자를 만들고 등록의 `Web.config`, 탐색 컨트롤을 추가 하려면 준비 된 것을 `Default.aspx`, `ProductsByCategory.aspx`, 및 `ProductDetails.aspx` 페이지에 `SiteMapProvider` 폴더. 열어서 시작 합니다 `Default.aspx` 끌어서 페이지는 `SiteMapPath` 디자이너 도구 상자에서. SiteMapPath 컨트롤을 도구 상자의 탐색 섹션에 있습니다.


[![Default.aspx로는 SiteMapPath를 추가 합니다.](building-a-custom-database-driven-site-map-provider-vb/_static/image19.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image18.gif)

**그림 16**: 추가 하는 SiteMapPath `Default.aspx` ([클릭 하 여 큰 이미지 보기](building-a-custom-database-driven-site-map-provider-vb/_static/image20.gif))


SiteMapPath 컨트롤 사이트 맵 내에서 현재 페이지의 위치를 나타내는 breadcrumb을 표시 합니다. 마스터 페이지의 맨 위에 SiteMapPath를 추가한 년대 합니다 *마스터 페이지 및 사이트 탐색* 자습서입니다.

브라우저를 통해이 페이지를 보려면 잠시 시간이 소요 됩니다. 그림 16에 추가 하는 SiteMapPath 해당 데이터를 가져오는 기본 사이트 맵 공급자를 사용 하 여 `Web.sitemap`입니다. 따라서, 이동 경로 탐색 표시 홈 &gt; 사이트 맵에서 오른쪽 위 모서리에 있는 이동 경로 탐색에서와 마찬가지로 사용자 지정 합니다.


[![기본 사이트 맵 공급자를 사용 하 여 이동 경로 탐색](building-a-custom-database-driven-site-map-provider-vb/_static/image22.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image21.gif)

**그림 17**: 기본 사이트 맵 공급자를 사용 하 여 이동 경로 탐색 ([큰 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image23.gif))


그림 16에 추가 하는 SiteMapPath 6 단계에서에서 만든 사용자 지정 사이트 맵 공급자를 사용 하도록 설정 해당 [ `SiteMapProvider` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemappath.sitemapprovider.aspx) northwind에에서는 할당 된 이름에는 `NorthwindSiteMapProvider` 에서 `Web.config`합니다. 아쉽게도 디자이너 계속 기본 사이트 맵 공급자를 사용 하 여 있지만이 속성을 변경한 후 브라우저를 통해 페이지를 방문 하는 경우 이동 경로 탐색 이제는 사용자 지정 사이트 맵 공급자 확인할 수 있습니다.


[![이제 사용 하 여 사용자 지정 사이트 맵 공급자 NorthwindSiteMapProvider 이동 경로 탐색](building-a-custom-database-driven-site-map-provider-vb/_static/image25.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image24.gif)

**그림 18**: 이제 사용 하 여 사용자 지정 사이트 맵 공급자의 이동 경로 탐색 `NorthwindSiteMapProvider` ([클릭 하 여 큰 이미지 보기](building-a-custom-database-driven-site-map-provider-vb/_static/image26.gif))


SiteMapPath 컨트롤에 더 많은 기능 사용자 인터페이스를 표시 합니다 `ProductsByCategory.aspx` 고 `ProductDetails.aspx` 페이지입니다. SiteMapPath를 설정 하는 이러한 페이지에 추가 된 `SiteMapProvider` Northwind로 모두 속성. `Default.aspx` 음료, 제품 보기 링크에 Chai 차에 대 한 세부 정보 보기 링크를 클릭 합니다. 현재 사이트 맵 섹션 (Chai Tea) 및 해당 상위 항목 이동 포함 그림 19와 같이: Beverages 및 모든 범주입니다.


[![이제 사용 하 여 사용자 지정 사이트 맵 공급자 NorthwindSiteMapProvider 이동 경로 탐색](building-a-custom-database-driven-site-map-provider-vb/_static/image27.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image21.png)

**그림 19**: 이제 사용 하 여 사용자 지정 사이트 맵 공급자의 이동 경로 탐색 `NorthwindSiteMapProvider` ([클릭 하 여 큰 이미지 보기](building-a-custom-database-driven-site-map-provider-vb/_static/image22.png))


Menu 및 TreeView 컨트롤과 같은 SiteMapPath 외에도 다른 탐색 사용자 인터페이스 요소를 사용할 수 있습니다. 합니다 `Default.aspx`, `ProductsByCategory.aspx`, 및 `ProductDetails.aspx` 예를 들어이 자습서에서는 다운로드에서 페이지 메뉴 컨트롤 (그림 20 참조) 모두 포함 합니다. 참조 [ASP.NET 2.0 검사 s 사이트 탐색 기능](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx) 및 [사이트 탐색 컨트롤을 사용 하](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/navigation/sitenavcontrols.aspx) 섹션을 [ASP.NET 2.0 퀵 스타트](https://quickstarts.asp.net/QuickStartv20/aspnet/) 더 자세히 살펴보려면를 탐색 컨트롤 및 ASP.NET 2.0의 사이트 맵 시스템입니다.


[![메뉴 컨트롤에는 각 범주 및 제품 나열](building-a-custom-database-driven-site-map-provider-vb/_static/image29.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image28.gif)

**그림 20**: The 메뉴 컨트롤 나열 각 범주 및 제품의 ([큰 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image30.gif))


사이트 맵 구조를 통해 프로그래밍 방식으로 액세스할 수 있습니다이 자습서의 앞부분에서 설명 했 듯이 `SiteMap` 클래스입니다. 다음 코드는 루트를 반환 합니다. `SiteMapNode` 기본 공급자입니다.


[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample8.vb)]

하므로 합니다 `AspNetXmlSiteMapProvider` 는 기본 공급자 샘플 응용 프로그램에서는 위의 코드에 정의 된 루트 노드를 반환 합니다 `Web.sitemap`. 기본값이 아닌 사이트 맵 공급자를 참조 하려면 사용 합니다 `SiteMap` s 클래스 [ `Providers` 속성](https://msdn.microsoft.com/library/system.web.sitemap.providers.aspx) 같이:


[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample9.vb)]

여기서 *이름을* (웹 응용 프로그램에 대 한: Northwind)의 사용자 지정 사이트 맵 공급자의 이름입니다.

사이트 맵 공급자에 게 특정 멤버에 액세스 하려면 사용 하 여 `SiteMap.Providers["name"]` 공급자 인스턴스를 검색 하 여 다음 적절 한 형식으로 캐스팅 합니다. 예를 들어 표시할를 `NorthwindSiteMapProvider` s `CachedDate` 속성 ASP.NET 페이지에서 다음 코드를 사용 합니다.


[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample10.vb)]

> [!NOTE]
> SQL 캐시 종속성 기능을 테스트 해야 합니다. 방문 후 합니다 `Default.aspx`, `ProductsByCategory.aspx`, 및 `ProductDetails.aspx` 페이지 편집, 삽입 및 삭제 섹션의에서 자습서 중 하나로 이동 및 범주 또는 제품의 이름을 편집 합니다. 다음 페이지 중 하나를 반환 합니다 `SiteMapProvider` 폴더입니다. 기본 데이터베이스에 변경 사항을 기록 하는 폴링 메커니즘에 대 한 충분 한 시간이 경과 가정 하 고, 사이트 맵 새 제품이 나 범주 이름을 표시 하도록 업데이트 되어야 합니다.


## <a name="summary"></a>요약

ASP.NET 2.0 사이트 맵 기능 포함을 `SiteMap` 클래스, 다양 한 기본 제공 탐색 웹 컨트롤 및 사이트 맵 정보를 필요로 하는 기본 사이트 맵 공급자는 XML 파일에 저장 합니다. 하려면 데이터베이스, 응용 프로그램의 아키텍처, 또는 사용자 지정 사이트 맵 공급자를 만들어야 하는 원격 웹 서비스와 같은 다른 원본에서 사이트 맵 정보를 사용 합니다. 직접 또는 간접적으로 파생 된 클래스 생성이 포함 됩니다에서 `SiteMapProvider` 클래스입니다.

이 자습서에서는 응용 프로그램 아키텍처에서 추려 낸 제품 테이블과 범주 정보를 사이트 맵 기반 하는 사용자 지정 사이트 맵 공급자를 만드는 방법에 살펴보았습니다. 확장 공급자는 `StaticSiteMapProvider` 클래스 및 수반 만들기는 `BuildSiteMap` 메서드 데이터를 검색 하는 사이트 맵 계층 구조를 생성 하 고 클래스 수준 변수 구조는 해당 결과 캐시 합니다. SQL 캐시 종속성을 콜백 함수를 사용 하 여 캐시 무효화를 사용 했습니다 경우 구조체 내부 `Categories` 또는 `Products` 데이터가 수정 됩니다.

즐거운 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [SQL Server에서 사이트 맵 저장](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/) 고 [적 기다리고 SQL 사이트 맵 공급자](https://msdn.microsoft.com/msdnmag/issues/06/02/wickedcode/default.aspx)
- [ASP.NET 2.0 살펴보기 공급자 모델](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)
- [공급자 도구 키트](https://msdn.microsoft.com/asp.net/aa336558.aspx)
- [ASP.NET 2.0 검사 사이트 탐색 기능](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Dave Gardner, Zack Jones, Teresa Murphy 및 박 광 준 Leigh 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](building-a-custom-database-driven-site-map-provider-cs.md)
