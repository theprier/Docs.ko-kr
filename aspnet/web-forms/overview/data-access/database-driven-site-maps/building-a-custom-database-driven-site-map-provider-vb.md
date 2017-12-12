---
uid: web-forms/overview/data-access/database-driven-site-maps/building-a-custom-database-driven-site-map-provider-vb
title: "빌드 사용자 지정 데이터베이스 기반의 사이트 맵 공급자 (VB) | Microsoft Docs"
author: rick-anderson
description: "ASP.NET 2.0에서 기본 사이트 맵 공급자는 정적 XML 파일에서 해당 데이터를 검색합니다. XML 기반 공급자가 여러 소규모 및 중간 크기에 적합 한 반면..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/26/2007
ms.topic: article
ms.assetid: f904cd2c-a408-4484-9324-8b8d7fe33893
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/database-driven-site-maps/building-a-custom-database-driven-site-map-provider-vb
msc.type: authoredcontent
ms.openlocfilehash: f886936c0033c9fac9c81fe8d2f7905228a9867d
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="building-a-custom-database-driven-site-map-provider-vb"></a>사용자 지정 데이터베이스 기반의 사이트 맵 공급자 (VB) 빌드
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_62_VB.zip) 또는 [PDF 다운로드](building-a-custom-database-driven-site-map-provider-vb/_static/datatutorial62vb1.pdf)

> ASP.NET 2.0에서 기본 사이트 맵 공급자는 정적 XML 파일에서 해당 데이터를 검색합니다. 대부분의 소규모 및 중간 규모의 웹 사이트에 적합 한 XML 기반 공급자 이지만, 큰 웹 응용 프로그램 보다 동적 사이트 맵이 필요 합니다. 비즈니스 논리 계층에서 해당 데이터를 검색 하는 사용자 지정 사이트 맵 공급자 빌드합니다이 자습서에서는 차례로 데이터 데이터베이스에서 검색 합니다.


## <a name="introduction"></a>소개

ASP.NET 2.0의 사이트 맵 기능을 사용 하면 페이지 개발자는 XML 파일에서와 같은 일부 영구 미디어에 웹 응용 프로그램의 사이트 맵을 정의 합니다. 사이트 맵 데이터를 통해 프로그래밍 방식으로 액세스할 수를 정의 고 [ `SiteMap` 클래스](https://msdn.microsoft.com/en-us/library/system.web.sitemap.aspx) 에 [ `System.Web` 네임 스페이스](https://msdn.microsoft.com/en-us/library/system.web.aspx) 또는 탐색의 다양 한을 통해 컨트롤을와 같은 웹는 SiteMapPath, 메뉴 및 TreeView를 제어 합니다. 사이트 맵 시스템에서 사용 하 여 [공급자 모델](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx) 다른 사이트 맵 serialization 구현 만들고 웹 응용 프로그램에 연결할 수 있도록 합니다. ASP.NET 2.0과 함께 제공 되는 기본 사이트 맵 공급자는 XML 파일에 사이트 맵 구조를 유지 합니다. 에 [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-vb.md) 자습서 라는 파일을 만들었습니다 `Web.sitemap` 이 구조를 포함 하 고 각 새 자습서 섹션으로 해당 XML 업데이트 되었습니다.

기본 XML 기반 사이트 맵 공급자 사이트 맵의 구조는이 자습서에 대 한 비교적 정적와 같은 경우에 적합 합니다. 그러나 대부분의 시나리오에서 보다 동적 사이트 맵 필요 합니다. 사이트 맵 그림 1에서 각 범주 및 제품 웹 사이트의 구조에 대 한 섹션으로 표시 하는 위치에 표시 된 것을 고려 합니다. 이 사이트 맵을 사용 하 여 루트 노드에 해당 하는 웹 페이지 방문 나열 될 수 있습니다 모든 범주, 특정 제품의 웹 페이지 보기는 해당 제품 s 세부 정보 표시 하 고 특정 범주의의 웹 페이지를 방문 하면 해당 범주의 제품 나열 됩니다.


[![범주 및 제품 구성을 사이트 맵의 구조](building-a-custom-database-driven-site-map-provider-vb/_static/image1.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image1.png)

**그림 1**: The 범주 및 제품 구성을 사이트 맵의 구조 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image2.png))


이 범주 및 제품 기반 구조에 하드 코딩 될 수는 `Web.sitemap` 파일 파일은 업데이트 해야 할 때마다 범주 또는 제품 추가, 제거 되었거나 이름이 변경 합니다. 따라서 사이트 맵 유지 관리의 구조는 데이터베이스에서 또는 응용 프로그램의 아키텍처의 비즈니스 논리 계층에서 검색 된 경우 크게 간소화 될 것 합니다. 이런 방식으로 제품 및 범주 추가 된, 이름 변경 또는 삭제, 사이트 맵 이러한 변경 내용을 반영 하도록 자동으로 업데이트 합니다.

ASP.NET 2.0의 사이트 맵 serialization 공급자 모델 기반 빌드되기 때문 데이터베이스, 아키텍처 등의 대체 데이터 저장소에서 데이터를 가져와 하는 고유한 사용자 지정 사이트 맵 공급자를 만들 수 있습니다. 이 자습서에서는 BLL에서 해당 데이터를 검색 하는 사용자 지정 공급자를 빌드합니다. Let s가 시작 되었습니다.

> [!NOTE]
> 이 자습서에서 만든 사용자 지정 사이트 맵 공급자는 응용 프로그램의 아키텍처 및 데이터 모델에 엄격 하 게 관련 됩니다. 부분 s [SQL Server에서 사이트 맵 저장](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/) 및 [적 기다리고 SQL 사이트 맵 공급자](https://msdn.microsoft.com/msdnmag/issues/06/02/wickedcode/default.aspx) 문서를 SQL Server의 사이트 맵 데이터를 저장 하는 일반화 된 방식을 검사 합니다.


## <a name="step-1-creating-the-custom-site-map-provider-web-pages"></a>1 단계: 사용자 지정 사이트 맵 공급자의 웹 페이지 만들기

사용자 지정 사이트 맵 공급자 만들기를 시작 하기 전에 먼저이 자습서에 사용 해야 하는 ASP.NET 페이지를 추가 하는 s를 사용 합니다. 라는 새 폴더를 추가 하 여 시작 `SiteMapProvider`합니다. 다음에 해당 폴더에 있는 각 페이지에 연결할 수 있도록 다음 ASP.NET 페이지 추가 `Site.master` 마스터 페이지:

- `Default.aspx`
- `ProductsByCategory.aspx`
- `ProductDetails.aspx`

추가적으로 `CustomProviders` 하위 폴더는 `App_Code` 폴더입니다.


![사이트 맵 공급자와 관련 된 자습서에 대 한 ASP.NET 페이지 추가](building-a-custom-database-driven-site-map-provider-vb/_static/image2.gif)

**그림 2**: ASP.NET 페이지는 사이트에 대 한 공급자 관련 자습서 매핑 추가


T 필요 하지 않는 것이 섹션에 대 한 하나의 자습서 이므로 `Default.aspx` 섹션의 자습서를 나열 합니다. 대신, `Default.aspx` 범주 GridView 컨트롤에 표시 됩니다. 해결할이 2 단계에서에서 합니다.

다음으로 업데이트 `Web.sitemap` 에 대 한 참조를 포함 하는 `Default.aspx` 페이지. 특히, 캐싱 후 다음 태그를 추가 `<siteMapNode>`:


[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample1.xml)]

업데이트 한 후 `Web.sitemap`, 브라우저를 통해 자습서 웹 사이트를 보려면 보십시오. 이제는 왼쪽 메뉴에서 유일한 사이트 맵 공급자 자습서에 대 한 항목이 포함 됩니다.


![사이트 맵 사이트 맵 공급자 자습서에는 항목이 포함](building-a-custom-database-driven-site-map-provider-vb/_static/image3.gif)

**그림 3**: 사이트 맵 사이트 맵 공급자 자습서에는 항목이 포함


사용자 지정 사이트 맵 공급자를 만들고 해당 공급자를 사용 하는 웹 응용 프로그램을 구성을 설명 하기 위해이 자습서 s 주로 집중 하는 합니다. 특히, 그림 1에 표시 된 대로 각 범주와 제품에 대 한 노드 함께 루트 노드를 포함 하는 사이트 맵을 반환 하는 공급자를 빌드합니다. 일반적으로 사이트 맵 노드마다 URL을 지정할 수 있습니다. 이 사이트 맵에 대 한 루트 노드의 URL 됩니다 `~/SiteMapProvider/Default.aspx`는 모든 데이터베이스에 대 한 범주를 나열 합니다. 사이트 맵에서 각 범주 노드를 가리키는 URL을 갖게 됩니다 `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID=categoryID`, 모든 지정 된 제품 나열 됩니다는 *categoryID*합니다. 마지막으로, 각 제품 사이트 맵 노드는 가리킵니다 `~/SiteMapProvider/ProductDetails.aspx?ProductID=productID`, 특정 제품 s 세부 정보가 표시 됩니다.

시작 하려면 만들어야 하는 `Default.aspx`, `ProductsByCategory.aspx`, 및 `ProductDetails.aspx` 페이지입니다. 이러한 페이지는 각각 2, 3 및 4 단계에서 완료 됩니다. 이 자습서 많이 사이트 맵 공급자에 있으므로 되 고 만들기 지난 자습서가 다루므로 म-4 단계 2를 통해 서둘러는 이러한 종류의 다중 페이지 마스터/세부 보고 합니다. 여러 페이지에 걸쳐 있는 마스터/세부 보고서를 만드는 방법에 대 한 세부 정보, 필요한 경우 다시 참조는 [마스터/세부 정보 필터링에서 두 페이지가](../masterdetail/master-detail-filtering-across-two-pages-vb.md) 자습서입니다.

## <a name="step-2-displaying-a-list-of-categories"></a>2 단계: 범주 목록을 표시

열기는 `Default.aspx` 페이지에 `SiteMapProvider` 폴더를 끌어서는 GridView 설정 디자이너 도구 상자에서 해당 `ID` 를 `Categories`합니다. GridView s 스마트 태그에서 바인딩할 라는 새 ObjectDataSource `CategoriesDataSource` 사용 하 여 해당 데이터를 검색할 수 있도록 구성 하 고는 `CategoriesBLL` s 클래스 `GetCategories` 메서드. 방금이 GridView 범주를 표시 하 고 데이터 수정 기능을 제공 하지 않습니다, 삽입, 업데이트에 드롭 다운 목록을 설정 하 고 탭 (없음)을 삭제 합니다.


[![ObjectDataSource 반환할 GetCategories 메서드를 사용 하 여 범주를 구성 합니다.](building-a-custom-database-driven-site-map-provider-vb/_static/image4.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image3.png)

**그림 4**: 구성 ObjectDataSource 범주 사용을 반환 하는 `GetCategories` 메서드 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image4.png))


[![삽입, 업데이트에서 드롭 다운 목록을 설정 하 고 탭 (없음)를 삭제](building-a-custom-database-driven-site-map-provider-vb/_static/image5.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image5.png)

**그림 5**: 드롭 다운 목록에서 업데이트, 삽입 및 삭제 탭 하도록 설정 (None) ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image6.png))


데이터 소스 구성 마법사를 완료 한 후 Visual Studio에 대 한 BoundField를 추가 합니다 `CategoryID`, `CategoryName`, `Description`, `NumberOfProducts`, 및 `BrochurePath`합니다. 만 포함 되도록 GridView 편집는 `CategoryName` 및 `Description` BoundFields 하 고 업데이트는 `CategoryName` BoundField의 `HeaderText` 범주에는 속성입니다.

다음으로 HyperLinkField를 추가 하 고 되도록 놓습니다 한다는의 맨 왼쪽 필드입니다. 설정의 `DataNavigateUrlFields` 속성을 `CategoryID` 및 `DataNavigateUrlFormatString` 속성을 `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID={0}`합니다. 설정의 `Text` 속성을 제품을 봅니다.


![HyperLinkField 범주 GridView에 추가](building-a-custom-database-driven-site-map-provider-vb/_static/image6.gif)

**그림 6**:에 HyperLinkField 추가 `Categories` GridView


ObjectDataSource를 만들고 GridView의 필드 사용자 지정 후 두 개의 선언 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample2.aspx)]

그림 7은 `Default.aspx` 브라우저를 통해 볼 때. 범주의 제품 보기를 클릭 하면 링크 이동 수 `ProductsByCategory.aspx?CategoryID=categoryID`는 3 단계에서에서 작성 합니다.


[![제품 보기 링크와 함께 나열 된 각 범주는](building-a-custom-database-driven-site-map-provider-vb/_static/image7.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image7.png)

**그림 7**: 제품 보기 링크와 함께 나열 된 각 범주는 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image8.png))


## <a name="step-3-listing-the-selected-category-s-products"></a>선택한 범주의의 제품을 나열 하는 3 단계:

열기는 `ProductsByCategory.aspx` 페이지 및 이름을 지정 하는 GridView 추가 `ProductsByCategory`합니다. 스마트 태그를 바인딩할 GridView 라는 새 ObjectDataSource `ProductsByCategoryDataSource`합니다. ObjectDataSource 사용 하도록 구성 된 `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)` UPDATE, INSERT 및 DELETE 탭에 있는 드롭 다운 목록 (없음)을 메서드 및 설정 합니다.


[![ProductsBLL 클래스의 GetProductsByCategoryID(categoryID) 메서드를 사용 하 여](building-a-custom-database-driven-site-map-provider-vb/_static/image8.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image9.png)

**그림 8**: 사용 된 `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)` 메서드 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image10.png))


데이터 소스 구성 마법사의 마지막 단계에 대 한 매개 변수 원본에 대 한 프롬프트 *categoryID*합니다. 이 정보는 쿼리 문자열 필드를 통해 전달 되므로 `CategoryID`, 드롭 다운 목록에서 쿼리 문자열을 선택 하 고 그림 9에 표시 된 것 처럼 CategoryID QueryStringField 텍스트 상자에 입력 합니다. 마법사를 완료 하려면 마침을 클릭 합니다.


[![CategoryID Querystring 필드를 사용 하 여 categoryid 매개 변수](building-a-custom-database-driven-site-map-provider-vb/_static/image9.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image11.png)

**그림 9**: 사용 된 `CategoryID` 에 대 한 Querystring 필드는 *categoryID* 매개 변수 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image12.png))


마법사를 완료 한 후 Visual Studio가 해당 BoundFields 및는 CheckBoxField 제품 데이터 필드에 대 한 GridView에 추가 합니다. 제거 제외한 모두 `ProductName`, `UnitPrice`, 및 `SupplierName` BoundFields 합니다. 이러한 세 가지 BoundFields 사용자 지정 `HeaderText` 속성을 각각 제품, 가격 및 공급 업체를 읽습니다. 형식에서 `UnitPrice` 통화로 BoundField 합니다.

다음으로 HyperLinkField를 추가 하 고 맨 왼쪽 위치로 이동 합니다. 설정의 `Text` 속성을 자세히 보기의 `DataNavigateUrlFields` 속성을 `ProductID`, 및 해당 `DataNavigateUrlFormatString` 속성을 `~/SiteMapProvider/ProductDetails.aspx?ProductID={0}`합니다.


![ProductDetails.aspx 가리키는 보기 세부 정보 HyperLinkField 추가](building-a-custom-database-driven-site-map-provider-vb/_static/image10.gif)

**그림 10**: 뷰를 가리키는 HyperLinkField 세부 정보 추가`ProductDetails.aspx`


이러한 사용자 지정에 확인 한 후 GridView 및 ObjectDataSource s 선언적 태그는 다음과 같아야 합니다.


[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample3.aspx)]

보기를 반환할 `Default.aspx` 음료에 대 한 링크를 통해 브라우저와 제품 보기를 클릭 합니다. 이 데 `ProductsByCategory.aspx?CategoryID=1`, 음료 범주에 속하는 Northwind 데이터베이스의 이름과 가격, 제품 공급 업체 표시 (11 그림 참조). 범주 목록 페이지를 사용자가 반환 하는 링크를 포함 하는이 페이지를 더욱 향상 시킬 자유롭게 (`Default.aspx`) 및 s 선택한 범주 이름 및 설명을 표시 하는 DetailsView 또는 FormView 컨트롤입니다.


[![음료 이름, 가격, 및 공급 업체 표시 됩니다.](building-a-custom-database-driven-site-map-provider-vb/_static/image11.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image13.png)

**그림 11**: The 음료 이름, 가격, 및 공급 업체 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image14.png))


## <a name="step-4-showing-a-product-s-details"></a>4 단계: 제품 s 세부 정보를 표시합니다.

마지막 페이지 `ProductDetails.aspx`, 선택 된 제품 세부 정보를 표시 합니다. 열기 `ProductDetails.aspx` 디자이너 도구 상자에서 DetailsView를 끕니다. DetailsView s 설정 `ID` 속성을 `ProductInfo` 지울 및 해당 `Height` 및 `Width` 속성 값입니다. 스마트 태그를 바인딩할 DetailsView 라는 새 ObjectDataSource `ProductDataSource`, ObjectDataSource에서 해당 데이터를 가져오도록 구성 된 `ProductsBLL` s 클래스 `GetProductByProductID(productID)` 메서드. 2, 3 단계에서 만든 이전 웹 페이지와 마찬가지로 UPDATE, INSERT에서에서 드롭 다운 목록을 설정 하 고 탭 (없음)를 삭제 합니다.


[![ObjectDataSource GetProductByProductID(productID) 메서드를 사용 하도록 구성](building-a-custom-database-driven-site-map-provider-vb/_static/image12.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image15.png)

**그림 12**: 구성에 사용 하 여 ObjectDataSource는 `GetProductByProductID(productID)` 메서드 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image16.png))


데이터 소스 구성 마법사의 마지막 단계 메시지의 원본에 대 한 표시는 *productID* 매개 변수입니다. 쿼리 문자열 필드를 통해이 데이터를 제공 하므로 `ProductID`, 드롭 다운 목록을 QueryString 및 ProductID QueryStringField textbox로 설정 합니다. 마지막으로, 마법사를 완료 하려면 "마침" 단추를 클릭 합니다.


[![ProductID ProductID Querystring 필드의 값을 밀어넣을 수 매개 변수를 구성 합니다.](building-a-custom-database-driven-site-map-provider-vb/_static/image13.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image17.png)

**그림 13**: 구성에서 *productID* 에서 해당 값을 매개 변수는 `ProductID` Querystring 필드 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image18.png))


데이터 소스 구성 마법사를 완료 한 후 Visual Studio는 만듭니다 해당 BoundFields 및는 CheckBoxField 제품 데이터 필드에 대 한 DetailsView에서 합니다. 제거는 `ProductID`, `SupplierID`, 및 `CategoryID` BoundFields 하 고 원하는 대로 나머지 필드를 구성 합니다. 소수의 미적인 구성 후 내 DetailsView 및 ObjectDataSource s 선언적 태그는 다음과 같은 조회:


[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample4.aspx)]

이 페이지를 테스트 하려면 반환 `Default.aspx` 음료 범주에 대 한 제품 보기를 클릭 합니다. 에서는 음료 제품 목록에서 Chai 찻잔에 대 한 세부 정보 보기 링크를 클릭 합니다. 이 데 `ProductDetails.aspx?ProductID=1`, Chai 찻잔 s를 보여 주는 세부 정보 (그림 14 참조).


[![Chai 찻잔 s 공급 업체, 범주, 가격 및 기타 정보 표시](building-a-custom-database-driven-site-map-provider-vb/_static/image14.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image19.png)

**그림 14**: Chai 찻잔 s 공급 업체, 범주, 가격 및 기타 정보가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image20.png))


## <a name="step-5-understanding-the-inner-workings-of-a-site-map-provider"></a>5 단계: 사이트 맵 공급자의 내부 작동 방식을 이해

사이트 맵은 컬렉션으로 웹 서버의 메모리에 표현 `SiteMapNode` 인스턴스를 계층 구조를 형성 합니다. 정확히 하나의 루트 여야 합니다, 모든 루트가 아닌 노드 정확히 하나의 부모 노드가 있고 모든 노드는 임의 개수의 자식 있을 수 있습니다. 각 `SiteMapNode` 개체 s 웹 사이트 구조의 섹션을 나타냅니다; 이러한 섹션에는 일반적으로 해당 웹 페이지는 합니다. 따라서는 [ `SiteMapNode` 클래스](https://msdn.microsoft.com/en-us/library/system.web.sitemapnode.aspx) 같은 속성이 `Title`, `Url`, 및 `Description`, 섹션에 대 한 정보를 제공는 `SiteMapNode` 나타냅니다. 또한는 `Key` 각각 고유 하 게 식별 하는 속성 `SiteMapNode` 이 계층 구조를 설정 하는 데 사용 된 속성 뿐만 아니라 계층 구조에서 `ChildNodes`, `ParentNode`, `NextSibling`, `PreviousSibling`, 등입니다.

그림 15 나타나지만 일반 사이트 맵 구조 그림 1에서 보다 자세히 살펴본 구현 세부 정보를 사용 합니다.


[![각 SiteMapNode가 속성 같은 제목, Url, 키 및 등](building-a-custom-database-driven-site-map-provider-vb/_static/image16.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image15.gif)

**그림 15**: 각 `SiteMapNode` 에 속성 예 `Title`, `Url`, `Key`등 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image17.gif))


사이트 맵은 통해 액세스할 수는 [ `SiteMap` 클래스](https://msdn.microsoft.com/en-us/library/system.web.sitemap.aspx) 에 [ `System.Web` 네임 스페이스](https://msdn.microsoft.com/en-us/library/system.web.aspx)합니다. 이 클래스 s `RootNode` 사이트 맵의 루트를 반환 하는 속성 `SiteMapNode` 인스턴스이거나 `CurrentNode` 반환 된 `SiteMapNode` 인 `Url` 속성에는 현재 요청 된 페이지의 URL과 일치 합니다. 이 클래스는 ASP.NET 2.0의 탐색 웹 컨트롤에서 내부적으로 사용 됩니다.

경우는 `SiteMap`의 클래스 속성에 액세스, 메모리에 일부 영구적인 매체에서 사이트 맵 구조를 serialize 해야 합니다. 그러나 사이트 맵 직렬화 논리 않습니다 하드에 코딩 된 `SiteMap` 클래스입니다. 대신, 런타임에 `SiteMap` 클래스 결정 어떤 사이트 맵 *공급자* serialization에 사용할 합니다. 기본적으로는 [ `XmlSiteMapProvider` 클래스](https://msdn.microsoft.com/en-us/library/system.web.xmlsitemapprovider.aspx) 을 사용 하는 사이트 맵의 구조 형식이 잘못 된 XML 파일에서 읽습니다. 그러나 약간의 작업에서는 고유한 사용자 지정 사이트 맵 공급자를 만들 수 있습니다.

파생 해야 하는 모든 사이트 맵 공급자는 [ `SiteMapProvider` 클래스](https://msdn.microsoft.com/en-us/library/system.web.sitemapprovider.aspx), 필수 메서드를 포함 하 고 사이트에 필요한 속성 공급자, 매핑하지만 많은 구현 세부 사항을 생략 합니다. 두 번째 클래스인 [ `StaticSiteMapProvider` ](https://msdn.microsoft.com/en-us/library/system.web.staticsitemapprovider.aspx), 확장 된 `SiteMapProvider` 클래스 하 고 필요한 기능을 구현 하는 보다 강력한 포함 합니다. 내부적으로 `StaticSiteMapProvider` 저장는 `SiteMapNode` 에 매핑하는 사이트의 인스턴스는 `Hashtable` 와 같은 메서드를 제공 하 고 `AddNode(child, parent)`, `RemoveNode(siteMapNode),` 및 `Clear()` 추가 및 제거 하는 `SiteMapNode` 내부 s `Hashtable`합니다. `XmlSiteMapProvider`는 `StaticSiteMapProvider`에서 파생됩니다.

확장 하는 사용자 지정 사이트 맵 공급자를 만들 때 `StaticSiteMapProvider`를 재정의 해야 하는 두 가지 추상 메서드는: [ `BuildSiteMap` ](https://msdn.microsoft.com/en-us/library/system.web.staticsitemapprovider.buildsitemap.aspx) 및 [ `GetRootNodeCore` ](https://msdn.microsoft.com/en-us/library/system.web.sitemapprovider.getrootnodecore.aspx)합니다. `BuildSiteMap`이름에서 알 수 있듯이 영구 저장소에서 사이트 맵 구조를 로드 하 고 메모리에 생성 하는 일을 담당 합니다. `GetRootNodeCore`사이트 맵의 루트 노드를 반환합니다.

웹 되기 전 까지의 응용 응용 프로그램의 구성에 등록 해야 하는 사이트 맵 공급자를 사용할 수 있습니다. 기본적으로는 `XmlSiteMapProvider` 클래스 이름을 사용 하 여 등록 `AspNetXmlSiteMapProvider`합니다. 추가 사이트 맵 공급자를 등록 하려면 다음 태그를 추가 `Web.config`:


[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample5.xml)]

*이름* 값 동안 공급자 이해 하기 쉬운 이름이 지정 *형식* 사이트 맵 공급자의 정규화 된 형식 이름을 지정 합니다. 에 대 한 구체적인 값을 살펴볼 것는 *이름* 및 *형식* 7 단계에서에서 값 했습니다 우리의 사용자 지정 사이트 맵 공급자를 만들었으면 했습니다.

사이트 맵 공급자 클래스에서 액세스할 때 처음으로 인스턴스화된는 `SiteMap` 클래스와 웹 응용 프로그램의 수명에 대 한 메모리에 유지 됩니다. 여러 명의 동시 웹 사이트 방문자에서 호출할 수 있는 사이트 맵 공급자의 인스턴스가 하나만 이므로 반드시 s 공급자 메서드는 수는 *스레드로부터 안전한*합니다.

성능 및 확장성 때문에 대 한 것 s 메모리 내 사이트를 캐시 하는 것이 중요 한 구조를 매핑한 될 때마다 다시 만드는 것이 아니라 구조 캐시이 반환할는 `BuildSiteMap` 메서드가 호출 됩니다. `BuildSiteMap`페이지와 사이트 맵 구조의 깊이에서 사용 중인 탐색 컨트롤에 따라 사용자 단위 페이지 요청에 따라 여러 번 호출할 수 있습니다. 사이트 맵 구조에 캐시 되지 않는 하면 사례에서 `BuildSiteMap` 를 호출할 때마다 해야 다시 아키텍처 (즉 쿼리에서 데이터베이스)에서 제품 테이블과 범주 정보를 검색 합니다. 이전 캐싱 자습서에서 설명한 대로 캐시 된 데이터 부실 해질 수 있습니다. 이 해결 하려면 시간-또는 SQL 캐시 종속성 기반 expiries 중 하나를 사용할 수 있습니다.

> [!NOTE]
> 사이트 맵 공급자를 선택적으로 재정의할 수 있습니다는 [ `Initialize` 메서드](https://msdn.microsoft.com/en-us/library/system.web.sitemapprovider.initialize.aspx)합니다. `Initialize`사이트 맵 공급자가 처음 인스턴스화 및에서 공급자에 할당 된 모든 사용자 지정 특성에 전달 될 때 호출 되 `Web.config` 에 `<add>` 와 같은 요소가: `<add name="name" type="type" customAttribute="value" />`합니다. 공급자의 코드를 수정 하지 않고도 다양 한 사이트 맵 공급자 관련 설정을 지정 하려면 페이지 개발자 허용 하려는 경우에 유용 합니다. 예를 들어 가능성이 반대인 d 우리 아키텍처를 통해 데이터베이스에서 직접 범주 및 제품 데이터를 읽는 것 म 경우 활용할 수 있도록 하려면 통해 데이터베이스 연결 문자열을 지정 하면 페이지 개발자 `Web.config` 하드 코드를 사용 하는 대신 공급자의 코드 값입니다. 6 단계에서에서 구축 하 게 하는 사용자 지정 사이트 맵 공급자가 재정의 하지 않는 `Initialize` 메서드. 사용 하는 예제에 대 한는 `Initialize` 메서드를 가리키는 [부분](http://www.wintellect.com/Weblogs/CategoryView,category,Jeff%20Prosise.aspx) s [SQL Server에서 사이트 맵 저장](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/) 문서.


## <a name="step-6-creating-the-custom-site-map-provider"></a>6 단계: 사용자 지정 사이트 맵 공급자 만들기

확장 하는 클래스를 만드는 필요 범주 및 Northwind 데이터베이스의 제품에서 사이트 맵을 작성 하는 사용자 지정 사이트 맵 공급자를 만들려면 `StaticSiteMapProvider`합니다. 1 단계에서에서 요청한 경우 추가할 수는 `CustomProviders` 폴더에는 `App_Code` 폴더-라는이 폴더에 새 클래스를 추가 `NorthwindSiteMapProvider`합니다. `NorthwindSiteMapProvider` 클래스에 다음 코드를 추가합니다.


[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample6.vb)]

이 클래스 s 탐색부터 시작 하는 s `BuildSiteMap` 메서드 시작 되는 [ `lock` 문을](https://msdn.microsoft.com/en-us/library/c5kehkcz.aspx)합니다. `lock` 문은 함으로써 해당 코드에 대 한 액세스를 직렬화 하 고 두 개의 동시 스레드 서로 s 거의 없었으나에서 단계별 실행 하지 못하도록를 입력 하려면 한 번에 스레드를 하나씩만 허용 합니다.

클래스 수준 `SiteMapNode` 변수 `root` 사이트 맵 구조를 캐시 하는 데 사용 됩니다. 처음으로 또는 기본 데이터를 수정한 후 처음으로 사이트 맵 생성 될 때 `root` 됩니다 `Nothing` 이며 사이트 맵 구조를 생성 합니다. 에 할당 된 사이트 맵의 루트 노드 `root` 생성 하는 동안 프로세스를 다음에이 메서드를 호출할 `root` 됩니다 `Nothing`합니다. 결과적으로 `root` 않습니다 `Nothing` 다시 만들 필요 없이 사이트 맵 구조를 호출자에 게 반환 됩니다.

루트 이면 `Nothing`, 범주 및 제품 정보에서 사이트 맵 구조 만들어집니다. 사이트 맵을 만들어 빌드될는 `SiteMapNode` 인스턴스 및 다음 호출을 통해 계층을 형성는 `StaticSiteMapProvider` s 클래스 `AddNode` 메서드. `AddNode`저장 된 다양 한 내부 정리 작업을 수행 `SiteMapNode` 인스턴스에 `Hashtable`합니다. 호출 하 여 시작 계층 구조 생성을 시작 하기 전에 `Clear` 메서드 내부에서 요소를 지우는 `Hashtable`합니다. 다음으로 `ProductsBLL` s 클래스 `GetProducts` 메서드와 그 결과 `ProductsDataTable` 지역 변수에 저장 합니다.

루트 노드를 만들고 할당 하 여 사이트 맵의 구성 시작 `root`합니다. 오버 로드는 [ `SiteMapNode` s 생성자](https://msdn.microsoft.com/en-us/library/system.web.sitemapnode.sitemapnode.aspx) 여기 또는이 사용 `BuildSiteMap` 다음 정보를 전달 됩니다.

- 사이트 맵 공급자에 대 한 참조 (`Me`).
- `SiteMapNode` s `Key`합니다. 이 값은 각각에 대해 고유 해야 합니다. 필수 `SiteMapNode`합니다.
- `SiteMapNode` s `Url`합니다. `Url`선택 사항이 각 제공 하지만 `SiteMapNode` s `Url` 값은 고유 해야 합니다.
- `SiteMapNode` s `Title`, 필요 합니다.

`AddNode(root)` 메서드 호출 추가 `SiteMapNode` `root` 루트로 사이트 맵을 합니다. 그런 다음, 각 `ProductRow` 에 `ProductsDataTable` 열거 됩니다. 경우 이미는 `SiteMapNode` 현재 s 제품 범주에 대 한 참조입니다. 그렇지 않으면 새 `SiteMapNode` 범주 만들어지고의 자식으로 추가 `SiteMapNode``root` 통해는 `AddNode(categoryNode, root)` 메서드를 호출 합니다. 적절 한 범주 후 `SiteMapNode` 노드 발견 했거나, 만든는 `SiteMapNode` 현재 제품에 대해 생성 되어 범주에 속하는 자식으로 추가 `SiteMapNode` 통해 `AddNode(productNode, categoryNode)`합니다. 범주 `SiteMapNode` s `Url` 속성 값은 `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID=categoryID` 제품 동안 `SiteMapNode` s `Url` 속성에 할당 되 `~/SiteMapNode/ProductDetails.aspx?ProductID=productID`합니다.

> [!NOTE]
> 데이터베이스 없는 제품을 `NULL` 에 대 한 값 자신의 `CategoryID` 범주 아래에 그룹화 됩니다 `SiteMapNode` 인 `Title` 속성이 None이 고 `Url` 속성이 빈 문자열로 설정 되어 있습니다. 설정 하기로 `Url` 이후 빈 문자열로 `ProductBLL` s 클래스 `GetProductsByCategory(categoryID)` 메서드는 현재 해당 제품을 반환 하는 기능에는 `NULL` `CategoryID` 값입니다. 또한, 탐색 컨트롤 렌더링 되는 방식을 보여 줍니다. 하고자 합니다.는 `SiteMapNode` 에 있는 값이 없는 해당 `Url` 속성입니다. 이 자습서에서는 확장을 확인해 보십시오 있도록 없음 `SiteMapNode` s `Url` 속성이 가리키는 `ProductsByCategory.aspx`, 제품을 아직만 표시 `NULL` `CategoryID` 값.


사이트 맵을 생성 한 후 임의 개체에서 SQL 캐시 종속성을 사용 하 여 데이터 캐시에 추가 됩니다는 `Categories` 및 `Products` 를 통해 테이블는 `AggregateCacheDependency` 개체입니다. SQL 캐시 종속성을 사용 하 여 이전 자습서에서에서 살펴본 *를 사용 하 여 SQL 캐시 종속성*합니다. 하지만 사용자 지정 사이트 맵 공급자의 데이터 캐시 s 오버 로드를 사용 `Insert` 메서드 것 아직를 탐색 했습니다. 이 오버 로드는 캐시에서 개체가 제거 될 때 호출 되는 대리자의 마지막 입력된 매개 변수로 허용 합니다. 새 전달 특히 [ `CacheItemRemovedCallback` 위임](https://msdn.microsoft.com/en-us/library/system.web.caching.cacheitemremovedcallback.aspx) 가리키는 `OnSiteMapChanged` 메서드가 아래에 정의 `NorthwindSiteMapProvider` 클래스입니다.

> [!NOTE]
> 사이트 맵의 메모리 내 표현을 클래스 수준 변수를 통해 캐시 된 `root`합니다. 웹 응용 프로그램에서 해당 인스턴스는 모든 스레드에서 공유 하는 이후 및 사용자 지정 사이트 맵 공급자 클래스의 인스턴스를 하나만 이므로이 클래스 변수에 캐시로 사용 됩니다. `BuildSiteMap` 만 하는 것은 기본 데이터베이스 데이터에 때 알림을 받으려면 메서드도 사용 하 여 데이터 캐시는 `Categories` 또는 `Products` 변경 내용 테이블입니다. 참고가 현재 날짜 및 시간 데이터 캐시에 추가할 값입니다. 실제 사이트 맵 데이터는 *하지* 데이터 캐시에 위치 합니다.


`BuildSiteMap` 메서드 사이트 맵의 루트 노드를 반환 하 여 완료 합니다.

나머지 메서드는 매우 간단 합니다. `GetRootNodeCore`루트 노드를 반환 하는 일을 담당 합니다. 이후 `BuildSiteMap` 루트를 반환 `GetRootNodeCore` 단순히 반환 `BuildSiteMap`의 값을 반환 합니다. `OnSiteMapChanged` 메서드 집합 `root` 다시 `Nothing` 캐시 항목이 제거 되는 경우. 으로 다시 설정 하는 루트와 `Nothing`, 다음에 `BuildSiteMap` 은 호출 사이트 맵 구조 다시 작성 됩니다. 마지막으로,는 `CachedDate` 속성이 이러한 값이 있는 경우 데이터 캐시에 저장 된 날짜 및 시간 값을 반환 합니다. 사이트 맵 데이터에 마지막으로 캐시를 확인 하려면이 속성 페이지 개발자가 사용할 수 있습니다.

## <a name="step-7-registering-thenorthwindsitemapprovider"></a>7 단계: 등록 된`NorthwindSiteMapProvider`

사용 하도록 웹 응용 프로그램에 대 한 순서 대로 `NorthwindSiteMapProvider` 를 등록 해야 6 단계에서에서 만든 사이트 맵 공급자는 `<siteMap>` 섹션 `Web.config`합니다. 특히, 내에 다음 태그를 추가할는 `<system.web>` 요소 `Web.config`:


[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample7.xml)]

이 태그는 두 가지 기능이: 의미를 먼저 기본 제공 `AspNetXmlSiteMapProvider` 는 기본 사이트 맵 공급자; 둘째, Northwind 사용자에 게 친숙 한 이름의 6 단계에서에서 만든 사용자 지정 사이트 맵 공급자를 등록 합니다.

> [!NOTE]
> 응용 프로그램 s에 있는 사이트 맵 공급자에 대 한 `App_Code` 폴더의 가치는 `type` 특성은 단순히 클래스 이름입니다. 또는 사용자 지정 사이트 맵 공급자 수 만든 별도 클래스 라이브러리 프로젝트에 웹 응용 프로그램 s에 배치 하는 컴파일된 어셈블리와 `/Bin` 디렉터리입니다. 이 경우에 `type` 번호 특성 값은 *Namespace*. *ClassName*, *AssemblyName* 합니다.


업데이트 한 후 `Web.config`, 브라우저에서이 자습서에서 페이지를 볼 보십시오. 왼쪽의 탐색 인터페이스는 섹션을 계속 표시 되며 자습서에 정의 된 `Web.sitemap`합니다. 부터 때문에 이것이 `AspNetXmlSiteMapProvider` 기본 공급자로 합니다. 사용 하는 탐색 사용자 인터페이스 요소를 만들기 위해는 `NorthwindSiteMapProvider`, Northwind 사이트 맵 공급자를 사용 해야 함을 명시적으로 지정 해야 합니다. 8 단계에서에서이 수행 하는 방법을 살펴보겠습니다.

## <a name="step-8-displaying-site-map-information-using-the-custom-site-map-provider"></a>8 단계: 사용자 지정 사이트 맵 공급자를 사용 하 여 사이트 맵 정보를 표시 합니다.

사용자 지정 사이트 맵 공급자 생성 하 고 등록 `Web.config`, 탐색 컨트롤을 추가 하려면 준비 된 우리는 `Default.aspx`, `ProductsByCategory.aspx`, 및 `ProductDetails.aspx` 페이지에 `SiteMapProvider` 폴더입니다. 열어 시작는 `Default.aspx` 끌어서 페이지는 `SiteMapPath` 디자이너 도구 상자에서입니다. SiteMapPath 컨트롤은 도구 상자의 탐색 섹션에 있습니다.


[![Default.aspx로는 SiteMapPath 추가](building-a-custom-database-driven-site-map-provider-vb/_static/image19.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image18.gif)

**그림 16**:를 SiteMapPath 추가 `Default.aspx` ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image20.gif))


SiteMapPath 컨트롤 사이트 맵 내에서 현재 페이지의 위치를 나타내는 이동 경로 표시 합니다. 마스터 페이지의 맨 위에 SiteMapPath 추가 다시는 *마스터 페이지 및 사이트 탐색* 자습서입니다.

브라우저를 통해이 페이지를 보려면 잠시 시간. 그림 16에서 추가 SiteMapPath에서 해당 데이터를 가져올 기본 사이트 맵 공급자를 사용 하 여 `Web.sitemap`합니다. 따라서, 홈 경로 기록 표시 &gt; 사이트 맵 오른쪽 위 모서리에서 이동 경로와 마찬가지로 사용자 지정 합니다.


[![기본 사이트 맵 공급자를 사용 하는 경로 기록](building-a-custom-database-driven-site-map-provider-vb/_static/image22.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image21.gif)

**그림 17**: 된 이동 경로 기본 사이트 맵 공급자를 사용 하 여 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image23.gif))


6 단계에서에서 만든 사용자 지정 사이트 맵 공급자를 사용 하 여 그림 16에서 추가 SiteMapPath, 설정 해당 [ `SiteMapProvider` 속성](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.sitemappath.sitemapprovider.aspx) northwind에에서는 할당 된 이름에는 `NorthwindSiteMapProvider` 에서 `Web.config`합니다. 안타깝게도, 디자이너 기본 사이트 맵 공급자를 사용 하 여 계속 하지만 속성 변경 후 브라우저를 통해 페이지를 방문 하는 경우 표시 된 이동 경로 이제는 사용자 지정 사이트 맵 공급자를 사용 합니다.


[![지금 사용 하 여 사용자 지정 사이트 맵 공급자 NorthwindSiteMapProvider 경로 기록](building-a-custom-database-driven-site-map-provider-vb/_static/image25.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image24.gif)

**그림 18**: 된 이동 경로 지금 사용 하 여 사용자 지정 사이트 맵 공급자 `NorthwindSiteMapProvider` ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image26.gif))


SiteMapPath이 컨트롤은 표시의 기능적 사용자 인터페이스는 `ProductsByCategory.aspx` 및 `ProductDetails.aspx` 페이지입니다. 이 페이지를 설정 하는 SiteMapPath 추가 `SiteMapProvider` Northwind로 두는 속성입니다. `Default.aspx` 음료에 대 한 제품 보기 링크를 선택한 다음 Chai 찻잔에 대 한 세부 정보 보기 링크를 클릭 합니다. 현재 사이트 맵 섹션 (Chai 찻잔) 및 해당 상위 항목 이동 포함 그림 19에서 볼 수 있듯이: Beverages 및 모든 범주입니다.


[![지금 사용 하 여 사용자 지정 사이트 맵 공급자 NorthwindSiteMapProvider 경로 기록](building-a-custom-database-driven-site-map-provider-vb/_static/image27.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image21.png)

**그림 19**: 된 이동 경로 지금 사용 하 여 사용자 지정 사이트 맵 공급자 `NorthwindSiteMapProvider` ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image22.png))


사용자 인터페이스 요소 다른 탐색 메뉴와 TreeView 컨트롤과 같은 SiteMapPath 외에도 사용할 수 있습니다. `Default.aspx`, `ProductsByCategory.aspx`, 및 `ProductDetails.aspx` 의 예를 들어이 자습서에 대 한 다운로드 페이지 메뉴 컨트롤 (그림 20 참조) 모두 포함 합니다. 참조 [ASP.NET 2.0 검사 s 사이트 탐색 기능](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx) 및 [사이트 탐색 컨트롤을 사용 하](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/navigation/sitenavcontrols.aspx) 의 섹션은 [ASP.NET 2.0 퀵 스타트](https://quickstarts.asp.net/QuickStartv20/aspnet/) 를 더 자세히 살펴보려면는 탐색 컨트롤 및 사이트 시스템을의 ASP.NET 2.0을 매핑합니다.


[![각 범주 및 제품을 나열 하는 Menu 컨트롤](building-a-custom-database-driven-site-map-provider-vb/_static/image29.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image28.gif)

**그림 20**: The 메뉴 컨트롤 나열 각 범주 및 제품 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-vb/_static/image30.gif))


사이트 맵 구조를 통해 프로그래밍 방식으로 액세스할 수이 자습서의 앞부분에서 설명 했 듯이 `SiteMap` 클래스입니다. 다음 코드에서는 루트 반환 `SiteMapNode` 기본 공급자의:


[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample8.vb)]

이후는 `AspNetXmlSiteMapProvider` 기본 공급자가이 응용 프로그램에 대 한 위의 코드에 정의 된 루트 노드를 반환 합니다 `Web.sitemap`합니다. 사용 하 여 기본이 아닌 다른 사이트 맵 공급자를 참조 하려면는 `SiteMap` s 클래스 [ `Providers` 속성](https://msdn.microsoft.com/en-us/library/system.web.sitemap.providers.aspx) 같이:


[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample9.vb)]

여기서 *이름* (웹 응용 프로그램에 대 한: Northwind)의 사용자 지정 사이트 맵 공급자의 이름입니다.

사이트 맵 공급자에 특정 멤버에 액세스 하려면 사용 하 여 `SiteMap.Providers["name"]` 공급자 인스턴스를 검색 한 다음 적절 한 형식으로 캐스팅 하 합니다. 예를 들어, 표시 하는 `NorthwindSiteMapProvider` s `CachedDate` 다음 코드를 사용 하는 ASP.NET 페이지의 속성:


[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample10.vb)]

> [!NOTE]
> SQL 캐시 종속성 기능을 테스트 해야 합니다. 방문 후의 `Default.aspx`, `ProductsByCategory.aspx`, 및 `ProductDetails.aspx` 페이지의 편집, 삽입 및 삭제 섹션의에서 자습서 중 하나로 이동 및 범주 또는 제품의 이름을 편집 합니다. 다음에서 페이지 중 하나로 반환는 `SiteMapProvider` 폴더입니다. 내부 데이터베이스에 변경 사항을 확인 하는 폴링 메커니즘에 대 한 충분 한 시간이 지나면 라고 가정할 경우 사이트 맵 새로운 제품 또는 범주 이름을 표시 하도록 업데이트 되어야 합니다.


## <a name="summary"></a>요약

ASP.NET 2.0의 사이트 맵 기능에 포함 되어는 `SiteMap` 클래스, 다양 한 기본 제공 웹 탐색 컨트롤 및 기본 사이트 맵 공급자 사이트 맵 정보를 필요로 하는 XML 파일에 저장 합니다. 데이터베이스에서와 같은 다른 소스에서 사이트 맵 정보를 사용 하려면 응용 프로그램의 아키텍처 또는 사용자 지정 사이트를 만들어야 하는 원격 웹 서비스 공급자를 매핑합니다. 여기에 직접 또는 간접적으로 파생 되는 클래스를 만들어에서 `SiteMapProvider` 클래스입니다.

이 자습서에서는 응용 프로그램 아키텍처에서 추려 낸 제품 테이블과 범주 정보를 사이트 맵 기반 사용자 지정 사이트 맵 공급자를 만드는 방법에 살펴보았습니다. 공급자 확장 우리의 `StaticSiteMapProvider` 클래스 및 수반 만들기는 `BuildSiteMap` 메서드는 데이터를 검색 하는 사이트 맵 계층 구현 되 고 클래스 수준 변수 구조는 해당 결과 캐시 합니다. 캐시 된 무효화를 콜백 함수로 SQL 캐시 종속성을 사용 때 구조 내부 `Categories` 또는 `Products` 데이터를 수정 합니다.

만족도 매우 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [SQL Server에 사이트 맵 저장](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/) 및 [적 기다리고 SQL 사이트 맵 공급자](https://msdn.microsoft.com/msdnmag/issues/06/02/wickedcode/default.aspx)
- [살펴보면 ASP.NET 2.0의 공급자 모델](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)
- [공급자 도구 키트](https://msdn.microsoft.com/en-us/asp.net/aa336558.aspx)
- [ASP.NET 2.0 검사 s 사이트 탐색 기능](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Dave Gardner, Zack jones 이면 특정, Teresa 머피 및 박 광 준 Leigh 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](building-a-custom-database-driven-site-map-provider-cs.md)
