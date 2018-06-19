---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-cs
title: 마스터/세부 두 페이지 (C#)에 걸쳐 필터링 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 데이터베이스 공급자를 나열 하는 GridView를 사용 하 여이 패턴을 구현 합니다. GridView에서 각 공급 업체 행은 Vie 포함 됩니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 552d2d50-fe73-4153-9a7f-2b379bec4625
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 0858bf9c8dc380898647293825145654ac1dbc34
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30887791"
---
<a name="masterdetail-filtering-across-two-pages-c"></a>마스터/세부 두 페이지 (C#)에 대해 필터링
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_9_CS.exe) 또는 [PDF 다운로드](master-detail-filtering-across-two-pages-cs/_static/datatutorial09cs1.pdf)

> 이 자습서에서는 데이터베이스 공급자를 나열 하는 GridView를 사용 하 여이 패턴을 구현 합니다. GridView에서 각 공급 업체 행, 클릭 하면 별도 페이지로 사용자 걸립니다 하는 해당 제품을 나열 선택한 공급자에 대 한 제품 보기 링크가 포함 됩니다.


## <a name="introduction"></a>소개

이전 두 자습서에 살펴보았습니다 하는 방법을 [마스터/세부 보고서 dropdownlist 활용을 사용 하 여 단일 웹 페이지에 표시](master-detail-filtering-with-a-dropdownlist-cs.md) 를 ["마스터" 레코드와 GridView 또는 DetailsView 컨트롤 표시](master-detail-filtering-with-two-dropdownlists-cs.md) 표시 하는 " 세부 정보입니다. " 마스터/세부 정보 보고서에 사용 되는 다른 일반적인 패턴은 웹 페이지와 다른 표시 된 세부 정보 마스터 레코드입니다. 포럼 웹 사이트 처럼 [ASP.NET 포럼](https://forums.asp.net/)은 실제로이 패턴의 좋은 예입니다. ASP.NET 포럼 포럼 시작, Web Forms, 데이터 Presentation 컨트롤의 다양 한 구성 됩니다 등에입니다. 각 포럼 스레드 수로 이루어져 및 각 스레드는 다양 한 게시물 이루어져 있습니다. ASP.NET 포럼 홈페이지 포럼 나열 되어 있습니다. 수 whisks 포럼에서을 클릭 하는 `ShowForum.aspx` 페이지 해당 포럼에 대 한 스레드를 나열 합니다. 마찬가지로, 클릭 하면 스레드에서 이동에 `ShowPost.aspx`, 클릭 된 스레드에 대 한 게시물을 표시 하는 합니다.

이 자습서에서는 데이터베이스 공급자를 나열 하는 GridView를 사용 하 여이 패턴을 구현 합니다. GridView에서 각 공급 업체 행, 클릭 하면 별도 페이지로 사용자 걸립니다 하는 해당 제품을 나열 선택한 공급자에 대 한 제품 보기 링크가 포함 됩니다.

## <a name="step-1-addingsupplierlistmasteraspxandproductsforsupplierdetailsaspxpages-to-thefilteringfolder"></a>1 단계: 추가`SupplierListMaster.aspx`및`ProductsForSupplierDetails.aspx`페이지는`Filtering`폴더

"시작" 페이지 수가 세 번째 자습서에서 페이지 레이아웃을 정의할 때 추가 `BasicReporting`, `Filtering`, 및 `CustomFormatting` 폴더입니다. 그러나 우리 추가 하지 않았습니다 기초 페이지가이 자습서에 대 한 해당 시간에 되 고 있으므로 두 개의 새 페이지를 추가 하는 `Filtering` 폴더: `SupplierListMaster.aspx` 및 `ProductsForSupplierDetails.aspx`합니다. `SupplierListMaster.aspx` 하는 동안 "마스터" 레코드 (공급 업체)를 나열 합니다 `ProductsForSupplierDetails.aspx` 선택한 공급자에 대 한 제품을 표시 합니다.

이러한 두 개의 새 페이지를 만들 수 있는 시기를 사용 하 여 연결 하려면 특정는 `Site.master` 마스터 페이지입니다.


![SupplierListMaster.aspx 및 ProductsForSupplierDetails.aspx 페이지를 필터링 폴더에 추가 합니다.](master-detail-filtering-across-two-pages-cs/_static/image1.png)

**그림 1**: 추가 된 `SupplierListMaster.aspx` 및 `ProductsForSupplierDetails.aspx` 페이지는 `Filtering` 폴더


새 페이지에는 프로젝트를 추가할 때는 반드시 사이트 맵 파일을 업데이트할 `Web.sitemap`를 적절 하 게 합니다. 이 자습서에 대 한 추가 `SupplierListMaster.aspx` 다음 XML 콘텐츠를 사용 하 여 필터링 보고서의 자식으로 사이트 맵 페이지 `<siteMapNode>` 요소:


[!code-xml[Main](master-detail-filtering-across-two-pages-cs/samples/sample1.xml)]

> [!NOTE]
> 사용 하 여 페이지 새 ASP.NET을 추가 하는 경우 사이트 맵 파일을 업데이트 하는 프로세스를 자동화할 수 있습니다 [K. Scott Allen](http://odetocode.com/Blogs/scott/)Visual Studio 무료의 [사이트 맵 매크로](http://odetocode.com/Blogs/scott/archive/2005/11/29/2537.aspx)합니다.


## <a name="step-2-displaying-the-supplier-list-insupplierlistmasteraspx"></a>2 단계: 공급자 목록에 표시`SupplierListMaster.aspx`

와 `SupplierListMaster.aspx` 및 `ProductsForSupplierDetails.aspx` 만든 페이지, 다음 단계는 공급자에 GridView 만들려는 `SupplierListMaster.aspx`합니다. 페이지에는 GridView를 추가 하 고 새 ObjectDataSource에 바인딩하십시오. 이 ObjectDataSource 사용할지는 `SuppliersBLL` 클래스의 `GetSuppliers()` 모든 공급 업체를 반환 하는 메서드.


[![SuppliersBLL 클래스 선택](master-detail-filtering-across-two-pages-cs/_static/image3.png)](master-detail-filtering-across-two-pages-cs/_static/image2.png)

**그림 2**: 선택 된 `SuppliersBLL` 클래스 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image4.png))


[![ObjectDataSource GetSuppliers() 메서드를 사용 하도록 구성](master-detail-filtering-across-two-pages-cs/_static/image6.png)](master-detail-filtering-across-two-pages-cs/_static/image5.png)

**그림 3**: 구성에 사용 하 여 ObjectDataSource는 `GetSuppliers()` 메서드 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image7.png))


링크를 포함 해야 라는 제품 보기 각 GridView 행에는 클릭 하면 해당 사용자 `ProductsForSupplierDetails.aspx` 선택된 된 행에 전달 `SupplierID` querystring 통해 값입니다. 예를 들어, 도쿄 Traders 공급 업체에 대 한 제품 보기 링크를 클릭 (있으며 그는 `SupplierID` 값 4)에 전송 되 `ProductsForSupplierDetails.aspx?SupplierID=4`합니다.

이를 위해 추가 [HyperLinkField](https://msdn.microsoft.com/library/system.web.ui.webcontrols.hyperlinkfield.aspx) 하이퍼링크 각 GridView 행에 추가 하는 GridView에 있습니다. GridView의 스마트 태그에서 열 편집 링크를 클릭 하 여 시작 합니다. 다음으로 HyperLinkField을 왼쪽 위에 있는 목록에서 선택한는 HyperLinkField GridView의 필드 목록에 포함할 추가 클릭 합니다.


[![HyperLinkField GridView에 추가](master-detail-filtering-across-two-pages-cs/_static/image9.png)](master-detail-filtering-across-two-pages-cs/_static/image8.png)

**그림 4**: GridView에는 HyperLinkField 추가 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image10.png))


HyperLinkField 동일한 텍스트를 사용 하도록 구성할 수 있습니다 또는 URL 각 GridView 행에 있는 링크를 값 이나 각 특정 행에 바인딩된 데이터 값에 이러한 값을 만들 수 있습니다. 정적 지정 하려면 모든 행에서 값 사용 HyperLinkField의 `Text` 또는 `NavigateUrl` 속성입니다. 링크 텍스트 모든 행에 대해 동일 하 게 할 것 이므로 설정 HyperLinkField의 `Text` 속성을 제품을 봅니다.


[![제품 보기로 HyperLinkField의 Text 속성 설정](master-detail-filtering-across-two-pages-cs/_static/image12.png)](master-detail-filtering-across-two-pages-cs/_static/image11.png)

**그림 5**: HyperLinkField의 설정 `Text` 속성을 제품 보기 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image13.png))


텍스트 또는 GridView 행에 바인딩된 원본 데이터를 기반으로 할에 URL 값을 설정 하려면 데이터 텍스트 필드 또는 URL 값에서 끌어와야 합니다 지정는 `DataTextField` 또는 `DataNavigateUrlFields` 속성입니다. `DataTextField` 단일 데이터 필드;로 설정할 수 있습니다. 하지만`DataNavigateUrlFields`,, 데이터 필드의 쉼표로 구분 된 목록으로 설정할 수 있습니다. 자주 텍스트 또는 현재 행의 데이터 필드 값과 일부 static 태그의 조합에 대 한 URL을 기반으로 해야 합니다. 이 자습서에서는 예를 들어 원하는 HyperLinkField의 링크의 URL을 `ProductsForSupplierDetails.aspx?SupplierID=supplierID`여기서 *`supplierID`* 각 GridView 행이 `SupplierID` 값입니다. 정적 필요 하 고 여기 값 데이터 기반 알림:는 `ProductsForSupplierDetails.aspx?SupplierID=` 링크의 URL의 일부는 정적 반면는 *`supplierID`* 부분은 데이터 기반으로 해당 값은 각 행의 자체 `SupplierID` 값입니다.

정적 및 데이터 기반 값의 조합을 나타내기 위해 사용 하 여는 `DataTextFormatString` 및 `DataNavigateUrlFormatString` 속성입니다. 필요에 따라 이러한 속성의 static 태그를 입력 한 다음 마커를 사용 하 여 `{0}` 에 지정 된 필드의 값을 원하는 `DataTextField` 또는 `DataNavigateUrlFields` 속성을 표시 합니다. 경우는 `DataNavigateUrlFields` 속성에는 여러 필드가 지정 된 사용 `{0}` 삽입, 첫 번째 필드 값을 원하는 경우 `{1}` 등에 대 한는 두 번째 필드 값입니다.

이이 자습서를 적용 하도록 설정 해야는 `DataNavigateUrlFields` 속성을 `SupplierID`데이터 값 필드를 행 단위로에 사용자 지정 해야 할 것 이므로, 및 `DataNavigateUrlFormatString` 속성을 `ProductsForSupplierDetails.aspx?SupplierID={0}`합니다.


[![HyperLinkField SupplierID에 따라 적절 한 링크 URL을 포함 하도록 구성](master-detail-filtering-across-two-pages-cs/_static/image15.png)](master-detail-filtering-across-two-pages-cs/_static/image14.png)

**그림 6**: HyperLinkField는 적절 한 링크 URL 기반에 포함 하도록 구성 된 `SupplierID` ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image16.png))


HyperLinkField를 추가한 후 자유롭게 사용자 지정 하 고 GridView의 필드 순서를 변경 합니다. 다음 태그 약간 필드 수준 사용자 지정 내용이 사이 GridView를 보여 줍니다.


[!code-aspx[Main](master-detail-filtering-across-two-pages-cs/samples/sample2.aspx)]

보려면 잠시는 `SupplierListMaster.aspx` 브라우저를 통해 페이지입니다. 그림 7에서 볼 수 있듯이 페이지 현재 모든 나열 제품 보기 링크를 포함 하 여 공급 업체 중 합니다. 제품 보기를 클릭 하면 링크는 데 `ProductsForSupplierDetails.aspx`공급 업체의 따라 전달 `SupplierID` 쿼리 문자열에서 합니다.


[![각 공급 업체 행 보기 제품 링크를 포함합니다.](master-detail-filtering-across-two-pages-cs/_static/image18.png)](master-detail-filtering-across-two-pages-cs/_static/image17.png)

**그림 7**: 보기 제품 링크를 포함 하는 각 공급 업체 행 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image19.png))


## <a name="step-3-listing-the-suppliers-products-inproductsforsupplierdetailsaspx"></a>에 공급 업체의 제품을 나열 하는 3 단계:`ProductsForSupplierDetails.aspx`

이 시점에서 `SupplierListMaster.aspx` 페이지에서 사용자가을 보내는 `ProductsForSupplierDetails.aspx`, 선택한 공급자의 전달 `SupplierID` 쿼리 문자열에서 합니다. 이 자습서의 마지막 단계에서 GridView에 제품을 표시 하는 `ProductsForSupplierDetails.aspx` 인 `SupplierID` equals는 `SupplierID` querystring를 통해 전달 합니다. 이 시작 하는 GridView를 추가 하 여 수행 하는 `ProductsForSupplierDetails.aspx` 페이지 라는 새 ObjectDataSource 컨트롤을 사용 하 여 `ProductsBySupplierDataSource` 를 호출 하는 `GetProductsBySupplierID(supplierID)` 에서 메서드는 `ProductsBLL` 클래스입니다.


[![ProductsBySupplierDataSource 라는 새 ObjectDataSource를 추가 합니다.](master-detail-filtering-across-two-pages-cs/_static/image21.png)](master-detail-filtering-across-two-pages-cs/_static/image20.png)

**그림 8**: 새 ObjectDataSource 라는 추가 `ProductsBySupplierDataSource` ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image22.png))


[![ProductsBLL 클래스 선택](master-detail-filtering-across-two-pages-cs/_static/image24.png)](master-detail-filtering-across-two-pages-cs/_static/image23.png)

**그림 9**: 선택 된 `ProductsBLL` 클래스 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image25.png))


[![GetProductsBySupplierID(supplierID) 메서드를 호출 ObjectDataSource 있어야 합니다.](master-detail-filtering-across-two-pages-cs/_static/image27.png)](master-detail-filtering-across-two-pages-cs/_static/image26.png)

**그림 10**: ObjectDataSource 호출가 `GetProductsBySupplierID(supplierID)` 메서드 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image28.png))


데이터 소스 구성 마법사의 마지막 단계에서는의 소스를 제공 하는 `GetProductsBySupplierID(supplierID)` 메서드의 *`supplierID`* 매개 변수입니다. 쿼리 문자열 값을 사용 하려면 쿼리 문자열 매개 변수 원본을 설정 하 고 QueryStringField 텍스트 상자에 사용할 쿼리 문자열 값의 이름을 입력 (`SupplierID`).


[![SupplierID를 SupplierID Querystring 값에서 매개 변수 값을 채웁니다](master-detail-filtering-across-two-pages-cs/_static/image30.png)](master-detail-filtering-across-two-pages-cs/_static/image29.png)

**그림 11**: 채우기는 *`supplierID`* 에서 매개 변수 값은 `SupplierID` Querystring 값 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image31.png))


그을 마쳤습니다. 그림 12는 `ProductsForSupplierDetails.aspx` 도쿄 Traders 링크를 클릭 하 여 방문 페이지 `SupplierListMaster.aspx`합니다.


[![표시 된 도쿄 Traders에서 제품 제공](master-detail-filtering-across-two-pages-cs/_static/image33.png)](master-detail-filtering-across-two-pages-cs/_static/image32.png)

**그림 12**: 표시 되는 제품 제공한 도쿄 Traders ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image34.png))


## <a name="displaying-supplier-information-inproductsforsupplierdetailsaspx"></a>에 공급 업체 정보를 표시합니다.`ProductsForSupplierDetails.aspx`

그림 12에서 볼 수 있듯이 `ProductsForSupplierDetails.aspx` 페이지에서 제공 하는 제품을 간단 하 게 나열는 `SupplierID` 쿼리 문자열에 지정 합니다. 그러나이 페이지에 직접 전송 누군가가을 인식 하지 못하기 그림 12 도쿄 Traders 제품을 표시 됩니다. 이 해결 하려면 공급 업체 정보 뿐 아니라이 페이지에 표시할 수 있습니다.

먼저 제품 GridView 위에 FormView를 추가 합니다. 이라는 새 ObjectDataSource 컨트롤을 만들어 `SuppliersDataSource` 를 호출 하 여 `SuppliersBLL` 클래스의 `GetSupplierBySupplierID(supplierID)` 메서드.


[![SuppliersBLL 클래스 선택](master-detail-filtering-across-two-pages-cs/_static/image36.png)](master-detail-filtering-across-two-pages-cs/_static/image35.png)

**그림 13**: 선택 된 `SuppliersBLL` 클래스 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image37.png))


[![GetSupplierBySupplierID(supplierID) 메서드를 호출 ObjectDataSource 있어야 합니다.](master-detail-filtering-across-two-pages-cs/_static/image39.png)](master-detail-filtering-across-two-pages-cs/_static/image38.png)

**그림 14**: ObjectDataSource 호출가 `GetSupplierBySupplierID(supplierID)` 메서드 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image40.png))


와 마찬가지로 `ProductsBySupplierDataSource`, 있어야는 *`supplierID`* 매개 변수 값이 할당은 `SupplierID` querystring 값입니다.


[![SupplierID를 SupplierID Querystring 값에서 매개 변수 값을 채웁니다](master-detail-filtering-across-two-pages-cs/_static/image42.png)](master-detail-filtering-across-two-pages-cs/_static/image41.png)

**그림 15**: 채우기는 *`supplierID`* 에서 매개 변수 값은 `SupplierID` Querystring 값 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image43.png))


Visual Studio FormView의을 자동으로 만들어집니다 FormView 디자인 뷰에서 ObjectDataSource에 바인딩할 때 `ItemTemplate`, `InsertItemTemplate`, 및 `EditItemTemplate` 각에서 반환 된 데이터 필드에 대 한 레이블 및 TextBox 웹 컨트롤이 ObjectDataSource 합니다. 공급 업체 정보를 자유롭게 제거 표시 하고자 하므로 `InsertItemTemplate` 및 `EditItemTemplate`합니다. 다음으로 ItemTemplate 편집에 공급 업체의 회사 이름이 표시 됩니다는 `<h3>` 요소 및 주소, city, country 및 회사 이름 아래에 전화 번호입니다. 또는 FormView의 수동으로 설정할 수 `DataSourceID` 만듭니다는 `ItemTemplate` 태그 다시에서 같이 "[the ObjectDataSource와 데이터를 표시](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)" 자습서입니다.

이 편집 내용을 후 FormView의 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](master-detail-filtering-across-two-pages-cs/samples/sample3.aspx)]

그림 16의 스크린 샷을 표시는 `ProductsForSupplierDetails.aspx` 페이지 후 위에서 자세히 설명 하는 공급 업체 정보 포함 되었습니다.


[![공급자에 대 한 요약을 포함 하는 제품 목록이](master-detail-filtering-across-two-pages-cs/_static/image45.png)](master-detail-filtering-across-two-pages-cs/_static/image44.png)

**그림 16**: 공급자의에 대 한 요약을 포함 하는 제품 목록이 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image46.png))


## <a name="applying-the-final-touches-for-theproductsforsupplierdetailsaspxui"></a>에 대 한 연결의 마지막으로 적용 된`ProductsForSupplierDetails.aspx`UI

사용자를 개선 하기 위해 있는이 보고서에 대 한 환경은 몇 가지 추가 있도록 있어는 `ProductsForSupplierDetails.aspx` 페이지. 사용자에서 이동할 수 있는 유일한 방법은 현재는 `ProductsForSupplierDetails.aspx` 다시 공급 업체 목록에는 페이지는 브라우저의 뒤로 단추를 클릭 하 여 합니다. 하이퍼링크 컨트롤을 추가 해 보겠습니다는 `ProductsForSupplierDetails.aspx` 에 다시 연결 하는 페이지 `SupplierListMaster.aspx`, 마스터 목록으로 돌아가려면 사용자에 대 한 또 다른 방법을 제공 합니다.


[![사용자를 다시 SupplierListMaster.aspx를 안내 하는 하이퍼링크 컨트롤 추가](master-detail-filtering-across-two-pages-cs/_static/image48.png)](master-detail-filtering-across-two-pages-cs/_static/image47.png)

**그림 17**: 하이퍼링크 컨트롤을 다시 사용자 추가 `SupplierListMaster.aspx` ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image49.png))


에 모든 제품 없는 공급 업체에 대 한 제품 보기 링크를 클릭 하는 경우는 `ProductsBySupplierDataSource` ObjectDataSource에서 `ProductsForSupplierDetails.aspx` 아무 결과도 반환 되지 않습니다. GridView에서 ObjectDataSource에 바인딩된 사용자의 브라우저에서 페이지의 빈 영역에 태그를 렌더링 하지 않습니다. 사용자에 게 통신 보다 명확 하 게 선택 된 공급자와 관련 된 제품이 있는지 GridView의 설정할 수 있습니다 `EmptyDataText` 속성을 원하는 이러한 상황이 발생 하는 경우 표시 되는 메시지입니다. 이 속성을 "이 공급이 업체에서 제공 되지 않는 제품이 없는"로 설정

기본적으로 Northwinds 데이터베이스에 있는 모든 공급자의 하나 이상의 제품을 제공합니다. 그러나이 자습서에 대 한 수동으로 수정 했지만 `Products` 테이블 Escargots Nouveaux 공급 업체 더 이상 제품에 연결 되어 있도록 합니다. 그림 18이 변경 후 Escargots Nouveaux에 대 한 세부 정보 페이지를 보여 줍니다.


[![사용자가 공급 업체 모든 제품을 제공 하지 않는 내용 알림이 표시 됩니다.](master-detail-filtering-across-two-pages-cs/_static/image51.png)](master-detail-filtering-across-two-pages-cs/_static/image50.png)

**그림 18**: 사용자가 공급 업체 모든 제품을 제공 하지 않는 내용 알림이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image52.png))


## <a name="summary"></a>요약

마스터/세부 정보 보고서는 단일 페이지에 마스터 및 세부 정보 레코드를 표시할 수, 하는 동안 여러 웹 사이트에서 구분 됩니다 두 웹 페이지에 걸쳐 있습니다. 이 자습서에서는 "마스터" 웹 페이지에 GridView에 나열 된 공급자와 연결 된 제품을 "details" 페이지에 나열 하 여 마스터/세부 정보 보고서를 구현 하는 방법을 찾았습니다. 마스터 웹 페이지에 각 공급 업체 행의 행을 따라 전달 하는 세부 정보 페이지에 대 한 링크 포함 `SupplierID` 값입니다. GridView의 HyperLinkField를 사용 하 여 이러한 행에 지정 링크를 쉽게 추가할 수 있습니다.

세부 정보 페이지에서 호출 하 여 수행 된 지정 된 공급자에 대 한 해당 제품을 검색 하는 `ProductsBLL` 클래스의 `GetProductsBySupplierID(supplierID)` 메서드. *`supplierID`* querystring 매개 변수 원본으로 사용 하 여 매개 변수 값이 지정 되었습니다. 또한 살펴보았습니다는 FormView를 사용 하 여 세부 정보 페이지에 공급자 세부 정보를 표시 하는 방법.

우리의 [다음 자습서](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) 마스터/세부 정보 보고서에 최종 라는 것입니다. 각 행에 선택 단추는 GridView에 제품의 목록을 표시 하는 방법을 살펴보겠습니다. Select 버튼을 클릭 하면 DetailsView 컨트롤 같은 페이지에 있는 해당 제품의 세부 정보가 표시 됩니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Hilton Giesenow 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](master-detail-filtering-with-two-dropdownlists-cs.md)
> [다음](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)
