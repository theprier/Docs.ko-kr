---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-vb
title: 마스터/세부 정보 필터링 (VB)의 두 페이지에 걸쳐 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 데이터베이스에 공급자를 나열 하는 GridView를 사용 하 여이 패턴에서는 구현 합니다. GridView의 각 공급 업체 행을 Vie 포함 됩니다...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 361d6a44-3f1f-4daf-85df-d4c2b8bf065d
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 290c4eba6f77a6006d424c3f05b77c1c128026b3
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828496"
---
<a name="masterdetail-filtering-across-two-pages-vb"></a>마스터/세부 정보 필터링 (VB)의 두 페이지에 걸쳐
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_9_VB.exe) 또는 [PDF 다운로드](master-detail-filtering-across-two-pages-vb/_static/datatutorial09vb1.pdf)

> 이 자습서에서는 데이터베이스에 공급자를 나열 하는 GridView를 사용 하 여이 패턴에서는 구현 합니다. 각 공급 업체 행 GridView에는 별도 페이지로 사용자를 소요 됩니다을 클릭 하면 때 나열 하는 이러한 제품 선택한 공급자에 대 한 제품 보기 링크가 포함 됩니다.


## <a name="introduction"></a>소개

Dropdownlist를 사용 하 여 "마스터" 레코드를 표시 하려면 단일 웹 페이지에서 마스터/세부 정보 보고서를 표시 하는 방법을 살펴보았습니다 이전 두 자습서에서와 [GridView](master-detail-filtering-with-a-dropdownlist-vb.md) 또는 [DetailsView](master-detail-filtering-with-two-dropdownlists-vb.md) 컨트롤이 표시 하는 " 세부 정보입니다. " 마스터/세부 정보 보고서에 사용 되는 또 다른 일반적인 패턴은 다른 표시 하는 세부 정보를 하나의 웹 페이지에 마스터 레코드입니다. 포럼 웹 사이트 처럼 [ASP.NET 포럼](https://forums.asp.net/), 실제로이 패턴의 좋은 예입니다. ASP.NET 포럼 포럼 시작, Web Forms, 데이터 프레젠테이션 컨트롤의 다양 한 구성 되며 등. 각 포럼 스레드 수 구성 됩니다 하 고 각 스레드의 게시물의 숫자로 구성 됩니다. ASP.NET 포럼 홈 페이지에서 포럼 나열 됩니다. 포럼을 클릭할 수 바로 `ShowForum.aspx` 페이지 해당 포럼에 대 한 스레드를 나열 합니다. 마찬가지로,를 클릭 하면 스레드 이동에 `ShowPost.aspx`는 클릭 된 스레드에 대 한 게시물을 표시 합니다.

이 자습서에서는 데이터베이스에 공급자를 나열 하는 GridView를 사용 하 여이 패턴에서는 구현 합니다. 각 공급 업체 행 GridView에는 별도 페이지로 사용자를 소요 됩니다을 클릭 하면 때 나열 하는 이러한 제품 선택한 공급자에 대 한 제품 보기 링크가 포함 됩니다.

## <a name="step-1-addingsupplierlistmasteraspxandproductsforsupplierdetailsaspxpages-to-thefilteringfolder"></a>1 단계: 추가`SupplierListMaster.aspx`하 고`ProductsForSupplierDetails.aspx`페이지를`Filtering`폴더

다양 한 "시작" 페이지에서 추가한 세 번째 자습서에서 페이지 레이아웃을 정의할 때 합니다 `BasicReporting`, `Filtering`, 및 `CustomFormatting` 폴더입니다. 그러나에서는 추가 하지 않은 시작 페이지를이 자습서에 대 한 해당 시점에, 따라서 잠시 두 새 페이지를 추가 합니다 `Filtering` 폴더: `SupplierListMaster.aspx` 및 `ProductsForSupplierDetails.aspx`합니다. `SupplierListMaster.aspx` 하는 동안 "마스터" 레코드 (공급 업체)를 나열 합니다 `ProductsForSupplierDetails.aspx` 선택한 공급자에 대 한 제품 표시 됩니다.

언제 이러한 두 개의 새 페이지를 만들 수를 사용 하 여 연결 하려면 특정을 `Site.master` 마스터 페이지입니다.


![필터링 폴더로 SupplierListMaster.aspx 및 ProductsForSupplierDetails.aspx 페이지 추가](master-detail-filtering-across-two-pages-vb/_static/image1.png)

**그림 1**: 추가 합니다 `SupplierListMaster.aspx` 하 고 `ProductsForSupplierDetails.aspx` 페이지를 `Filtering` 폴더


또한 프로젝트에 새 페이지를 추가 하는 경우 업데이트 해야 사이트 맵 파일 `Web.sitemap`, 적절 하 게 합니다. 이 자습서에 대 한 추가 합니다 `SupplierListMaster.aspx` 필터링 보고서의 자식으로 다음 XML 콘텐츠를 사용 하 여 사이트 맵 페이지 `<siteMapNode>` 요소:


[!code-xml[Main](master-detail-filtering-across-two-pages-vb/samples/sample1.xml)]

> [!NOTE]
> 사용 하 여 페이지 새로 만들기 ASP.NET를 추가 하는 경우 사이트 맵 파일을 업데이트 하는 프로세스를 자동화 하는 것이 도움이 [K. Scott Allen](http://odetocode.com/Blogs/scott/)의 무료 Visual Studio [사이트 맵 매크로](http://odetocode.com/Blogs/scott/archive/2005/11/29/2537.aspx)합니다.


## <a name="step-2-displaying-the-supplier-list-insupplierlistmasteraspx"></a>2 단계: 공급자 목록 표시`SupplierListMaster.aspx`

사용 하 여 합니다 `SupplierListMaster.aspx` 하 고 `ProductsForSupplierDetails.aspx` 공급 업체의 GridView를 만들려면 만든 페이지, 다음 단계는 `SupplierListMaster.aspx`합니다. 페이지에 GridView를 추가 하 고 새 ObjectDataSource에 바인딩하십시오. 이 ObjectDataSource를 사용 해야 합니다 `SuppliersBLL` 클래스의 `GetSuppliers()` 모든 공급자를 반환 하는 방법입니다.


[![SuppliersBLL 클래스를 선택 합니다.](master-detail-filtering-across-two-pages-vb/_static/image3.png)](master-detail-filtering-across-two-pages-vb/_static/image2.png)

**그림 2**: 선택 된 `SuppliersBLL` 클래스 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-across-two-pages-vb/_static/image4.png))


[![GetSuppliers() 메서드를 사용 하는 ObjectDataSource 구성](master-detail-filtering-across-two-pages-vb/_static/image6.png)](master-detail-filtering-across-two-pages-vb/_static/image5.png)

**그림 3**: ObjectDataSource 사용 하도록 구성 된 `GetSuppliers()` 메서드 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-across-two-pages-vb/_static/image7.png))


링크를 포함 해야 이라는 제품 보기 각 GridView 행에서를 클릭 하면 해당 사용자 `ProductsForSupplierDetails.aspx` 선택한 행의 전달 `SupplierID` querystring 통해 값입니다. 예를 들어, 사용자가 도쿄 Traders 공급자에 대 한 제품 보기 링크를 클릭 하면 (있는 `SupplierID` 값이 4)에 전송 되 `ProductsForSupplierDetails.aspx?SupplierID=4`합니다.

이를 위해 추가 된 [HyperLinkField](https://msdn.microsoft.com/library/system.web.ui.webcontrols.hyperlinkfield.aspx) GridView에 각 GridView 행에 하이퍼링크 추가 합니다. GridView의 스마트 태그에서 열 편집 링크를 클릭 하 여 시작 합니다. 다음으로 HyperLinkField을 왼쪽 위에 있는 목록에서 선택한는 HyperLinkField GridView의 필드 목록에 포함할 추가 클릭 합니다.


[![GridView에는 HyperLinkField 추가](master-detail-filtering-across-two-pages-vb/_static/image9.png)](master-detail-filtering-across-two-pages-vb/_static/image8.png)

**그림 4**: GridView를 HyperLinkField 추가할 ([큰 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-vb/_static/image10.png))


동일한 텍스트를 사용 하 여 HyperLinkField를 구성할 수 있습니다 또는 URL 각 GridView 행에 있는 링크를 값 이나 각 특정 행에 바인딩된 데이터 값에 이러한 값을 기본 수 있습니다. 모든 행에 값을 정적 지정 하려면 HyperLinkField의을 사용 합니다 `Text` 또는 `NavigateUrl` 속성입니다. 모든 행에 대해 동일한 링크 텍스트, 것 이므로 설정 HyperLinkField의 `Text` 보기 제품에는 속성입니다.


[![제품 보기로 HyperLinkField의 Text 속성 설정](master-detail-filtering-across-two-pages-vb/_static/image12.png)](master-detail-filtering-across-two-pages-vb/_static/image11.png)

**그림 5**: HyperLinkField의 설정 `Text` 제품 보기 속성 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-across-two-pages-vb/_static/image13.png))


텍스트 또는 GridView 행에 바인딩된 내부 데이터를 기반으로 하는 URL 값을 설정 하려면 데이터 텍스트 필드 또는 URL 값에서 끌어와야를 지정 합니다 `DataTextField` 또는 `DataNavigateUrlFields` 속성입니다. `DataTextField` 단일 데이터 필드를로 설정할 수 있습니다. 그러나`DataNavigateUrlFields`, 데이터 필드의 쉼표로 구분 된 목록에 설정할 수 있습니다. 자주 텍스트 또는 현재 행의 데이터 필드 값 및 몇 가지 정적 태그의 조합에 대 한 URL을 기반으로 해야 합니다. 이 자습서에서는 예를 들어, 원하는 수의 HyperLinkField 링크의 URL `ProductsForSupplierDetails.aspx?SupplierID=supplierID`, 여기서 *`supplierID`* 각 GridView의 행이 `SupplierID` 값입니다. 정적 해야 있고 여기 값 데이터를 기반: 합니다 `ProductsForSupplierDetails.aspx?SupplierID=` 링크의 URL 부분은 정적 반면를 *`supplierID`* 부분은 데이터를 기반으로 해당 값은 각 행의 고유한 `SupplierID` 값.

정적 및 데이터 기반 값을 조합한을 나타내기 위해 사용 합니다 `DataTextFormatString` 및 `DataNavigateUrlFormatString` 속성입니다. 필요에 따라 이러한 속성의 static 태그를 입력 하 고 다음 마커를 사용 하 여 `{0}` 에 지정 된 필드의 값을 원하는 위치를 `DataTextField` 또는 `DataNavigateUrlFields` 속성을 표시 합니다. 경우는 `DataNavigateUrlFields` 속성이 여러 필드 지정 된 사용 `{0}` 첫 번째 필드 값을 삽입 하는 경우 `{1}` 등에 대 한는 두 번째 필드 값입니다.

이 자습서를 적용 하면를 설정 해야 합니다 `DataNavigateUrlFields` 속성을 `SupplierID`데이터 값 필드를 행 기준에 따라 사용자 지정 해야 하는 것 이므로, 및 `DataNavigateUrlFormatString` 속성을 `ProductsForSupplierDetails.aspx?SupplierID={0}`합니다.


[![SupplierID에 따라 적절 한 링크 URL을 포함 하도록 HyperLinkField 구성](master-detail-filtering-across-two-pages-vb/_static/image15.png)](master-detail-filtering-across-two-pages-vb/_static/image14.png)

**그림 6**: 구성의 적절 한 링크 URL을 기반으로 포함 하도록 HyperLinkField 합니다 `SupplierID` ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-vb/_static/image16.png))


HyperLinkField를 추가한 후 자유롭게 사용자 지정 하 고 GridView의 필드 다시 정렬 합니다. 다음 태그에서는 약간 필드 수준 사용자 지정 작성 한 후 GridView를 보여 줍니다.


[!code-aspx[Main](master-detail-filtering-across-two-pages-vb/samples/sample2.aspx)]

보려는 잠시는 `SupplierListMaster.aspx` 브라우저를 통해 페이지입니다. 그림 7에서 알 수 있듯이, 페이지를 현재 모두 나열 제품 보기 링크를 포함 한 공급 업체의 합니다. 제품 보기 클릭 하면 링크가 이동 됩니다 `ProductsForSupplierDetails.aspx`공급자를 따라 전달 `SupplierID` 쿼리 문자열에서.


[![각 공급 업체 행 보기 제품 링크를 포함합니다.](master-detail-filtering-across-two-pages-vb/_static/image18.png)](master-detail-filtering-across-two-pages-vb/_static/image17.png)

**그림 7**: 보기 제품 링크를 포함 하는 각 공급 업체 행 ([큰 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-vb/_static/image19.png))


## <a name="step-3-listing-the-suppliers-products-inproductsforsupplierdetailsaspx"></a>에 공급 업체의 제품을 나열 하는 3 단계:`ProductsForSupplierDetails.aspx`

이 시점에서 `SupplierListMaster.aspx` 페이지에서 사용자가 보내는 `ProductsForSupplierDetails.aspx`, 선택한 공급자의 전달 `SupplierID` 쿼리 문자열에서. 자습서의 마지막 단계에서 GridView에서 제품을 표시 하는 `ProductsForSupplierDetails.aspx` 해당 `SupplierID` equals는 `SupplierID` 쿼리 문자열에 전달 합니다. 이 시작 하기 위한 GridView를 추가 하 여 수행 하는 `ProductsForSupplierDetails.aspx` 라는 새 ObjectDataSource 컨트롤을 사용 하 여 페이지 `ProductsBySupplierDataSource` 를 호출 하는 합니다 `GetProductsBySupplierID(supplierID)` 메서드에서 `ProductsBLL` 클래스.


[![ProductsBySupplierDataSource 라는 새 ObjectDataSource를 추가 합니다.](master-detail-filtering-across-two-pages-vb/_static/image21.png)](master-detail-filtering-across-two-pages-vb/_static/image20.png)

**그림 8**: 새 ObjectDataSource 라는 추가 `ProductsBySupplierDataSource` ([클릭 하 여 큰 이미지 보기](master-detail-filtering-across-two-pages-vb/_static/image22.png))


[![ProductsBLL 클래스를 선택 합니다.](master-detail-filtering-across-two-pages-vb/_static/image24.png)](master-detail-filtering-across-two-pages-vb/_static/image23.png)

**그림 9**: 선택 된 `ProductsBLL` 클래스 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-across-two-pages-vb/_static/image25.png))


[![GetProductsBySupplierID(supplierID) 메서드를 호출 하는 ObjectDataSource가](master-detail-filtering-across-two-pages-vb/_static/image27.png)](master-detail-filtering-across-two-pages-vb/_static/image26.png)

**그림 10**: ObjectDataSource 호출 있어야 합니다 `GetProductsBySupplierID(supplierID)` 메서드 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-across-two-pages-vb/_static/image28.png))


데이터 소스 구성 마법사의 마지막 단계에서는의 원본을 제공 합니다 `GetProductsBySupplierID(supplierID)` 메서드의 *`supplierID`* 매개 변수입니다. Querystring 값을 사용 하려면 쿼리 문자열 매개 변수 원본을 설정 하 고 QueryStringField 텍스트 상자에 사용할 쿼리 문자열 값의 이름을 입력 (`SupplierID`).


[![SupplierID를 SupplierID Querystring 값에서 매개 변수 값을 채웁니다](master-detail-filtering-across-two-pages-vb/_static/image30.png)](master-detail-filtering-across-two-pages-vb/_static/image29.png)

**그림 11**: 채우기 합니다 *`supplierID`* 에서 매개 변수 값을 `SupplierID` Querystring 값 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-vb/_static/image31.png))


이것이 전부입니다! 그림 12는 `ProductsForSupplierDetails.aspx` 페이지에서 도쿄 Traders 링크를 클릭 하면 방문 하면 `SupplierListMaster.aspx`합니다.


[![나와 도쿄 Traders에서 제품 제공](master-detail-filtering-across-two-pages-vb/_static/image33.png)](master-detail-filtering-across-two-pages-vb/_static/image32.png)

**그림 12**: 표시 되는 제품 제공한 도쿄 Traders ([큰 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-vb/_static/image34.png))


## <a name="displaying-supplier-information-inproductsforsupplierdetailsaspx"></a>에 공급 업체 정보를 표시합니다.`ProductsForSupplierDetails.aspx`

그림 12에서 볼 수 있듯이 `ProductsForSupplierDetails.aspx` 페이지에는 간단 하 게 제공 되는 제품 나열를 `SupplierID` 쿼리 문자열에서 지정 합니다. 그러나이 페이지를 직접 보낸 사람이는 알지 못합니다 그림 12에 도쿄 Traders 제품 보여주는. 이 문제를 해결 하려면 것 뿐 아니라이 페이지에서 공급 업체 정보를 표시할 수 있습니다.

GridView 제품 위에 FormView를 추가 하 여 시작 합니다. 라는 새 ObjectDataSource 컨트롤을 만들 `SuppliersDataSource` 를 호출 하는 `SuppliersBLL` 클래스의 `GetSupplierBySupplierID(supplierID)` 메서드.


[![SuppliersBLL 클래스를 선택 합니다.](master-detail-filtering-across-two-pages-vb/_static/image36.png)](master-detail-filtering-across-two-pages-vb/_static/image35.png)

**그림 13**: 선택 된 `SuppliersBLL` 클래스 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-across-two-pages-vb/_static/image37.png))


[![GetSupplierBySupplierID(supplierID) 메서드를 호출 하는 ObjectDataSource가](master-detail-filtering-across-two-pages-vb/_static/image39.png)](master-detail-filtering-across-two-pages-vb/_static/image38.png)

**그림 14**: ObjectDataSource 호출 있어야 합니다 `GetSupplierBySupplierID(supplierID)` 메서드 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-across-two-pages-vb/_static/image40.png))


와 마찬가지로 합니다 `ProductsBySupplierDataSource`가 합니다 *`supplierID`* 매개 변수 값이 할당를 `SupplierID` querystring 값.


[![SupplierID를 SupplierID Querystring 값에서 매개 변수 값을 채웁니다](master-detail-filtering-across-two-pages-vb/_static/image42.png)](master-detail-filtering-across-two-pages-vb/_static/image41.png)

**그림 15**: 채우기 합니다 *`supplierID`* 에서 매개 변수 값을 `SupplierID` Querystring 값 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-vb/_static/image43.png))


디자인 뷰에서 ObjectDataSource에 FormView 바인딩할 경우 Visual Studio에서 자동으로 FormView의을 만듭니다 `ItemTemplate`, `InsertItemTemplate`, 및 `EditItemTemplate` 각 반환한 데이터 필드에 대 한 레이블 및 텍스트 웹 컨트롤을 사용 하 여는 ObjectDataSource 합니다. 공급 업체 정보 자유롭게 제거할 표시 하고자 하므로 합니다 `InsertItemTemplate` 고 `EditItemTemplate`입니다. 공급자의 회사 이름 표시 되도록 ItemTemplate을 다음으로, 편집을 `<h3>` 요소 및 주소, 도시, 국가 및 회사 이름 아래에 전화 번호입니다. 또는 FormView의 수동으로 설정할 수 있습니다 `DataSourceID` 만들고는 `ItemTemplate` 태그 다시에서 수행한 것 처럼는 "[the ObjectDataSource 사용 하 여 데이터 표시](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)" 자습서입니다.

이러한 편집 후 FormView의 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](master-detail-filtering-across-two-pages-vb/samples/sample3.aspx)]

그림 16의 스크린 샷을 보여 줍니다는 `ProductsForSupplierDetails.aspx` 페이지 위에서 자세히 설명 하는 공급 업체 정보에 포함 되었습니다.


[![제품 목록에는 공급자에 대 한 요약이 포함 됩니다.](master-detail-filtering-across-two-pages-vb/_static/image45.png)](master-detail-filtering-across-two-pages-vb/_static/image44.png)

**그림 16**: 공급자의에 대 한 요약을 포함 하는 제품 목록이 ([큰 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-vb/_static/image46.png))


## <a name="applying-the-final-touches-for-theproductsforsupplierdetailsaspxui"></a>마지막 적용에 대 한 터치를`ProductsForSupplierDetails.aspx`UI

사용자를 개선 하기 위해이 보고서에 있는 환경을 가지는 있도록 있어 추가 `ProductsForSupplierDetails.aspx` 페이지입니다. 사용자에서 이동할 수는 유일한 방법은 현재는 `ProductsForSupplierDetails.aspx` 공급 업체의 목록으로 돌아가기는 페이지는 브라우저의 뒤로 단추를 클릭 합니다. 하이퍼링크 컨트롤을 추가 해 보겠습니다 합니다 `ProductsForSupplierDetails.aspx` 에 다시 연결 하는 페이지 `SupplierListMaster.aspx`, 마스터 목록으로 돌아가려면 사용자에 대 한 다른 방법을 제공 합니다.


[![SupplierListMaster.aspx에 사용자를 다시 수행 하는 하이퍼링크 컨트롤 추가](master-detail-filtering-across-two-pages-vb/_static/image48.png)](master-detail-filtering-across-two-pages-vb/_static/image47.png)

**그림 17**:를 다시 사용자 하이퍼링크 컨트롤을 추가 `SupplierListMaster.aspx` ([클릭 하 여 큰 이미지 보기](master-detail-filtering-across-two-pages-vb/_static/image49.png))


모든 제품 없는 공급자에 대 한 제품 보기 링크를 클릭할 경우 합니다 `ProductsBySupplierDataSource` ObjectDataSource `ProductsForSupplierDetails.aspx` 어떤 결과도 반환 되지 않습니다. GridView의 ObjectDataSource에 바인딩된 사용자의 브라우저에서 페이지의 빈 영역에 태그를 렌더링 하지 않습니다. GridView의 사용자에 게 알려 보다 명확 하 게 선택한 공급자와 관련 된 제품이 있는지를 설정할 수 있습니다 `EmptyDataText` 속성을 메시지 이러한 상황이 발생 하는 경우 표시 하려고 합니다. 이 속성을 "제품이 없습니다이 공급 업체에서 제공한" 설정한

기본적으로 Northwinds 데이터베이스에 있는 모든 공급자는 하나 이상의 제품을 제공합니다. 그러나이 자습서를 위해 수동으로 수정 했습니다는 `Products` 테이블 Escargots Nouveaux 공급자 제품을 사용 하 여 연결 되어 있지 않습니다. 그림 18이 변경 후 Escargots Nouveaux에 대 한 세부 정보 페이지를 보여 줍니다.


[![사용자가 공급자가 모든 제품을 제공 하지 않는 내용 알림이 표시 됩니다.](master-detail-filtering-across-two-pages-vb/_static/image51.png)](master-detail-filtering-across-two-pages-vb/_static/image50.png)

**그림 18**: 사용자가 공급자가 모든 제품을 제공 하지 않는 내용 알림이 표시 됩니다 ([큰 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-vb/_static/image52.png))


## <a name="summary"></a>요약

마스터/세부 정보 보고서는 단일 페이지에 마스터 및 세부 정보 레코드를 표시할 수 있습니다, 있지만 여러 웹 사이트에서 구분 됩니다 두 웹 페이지에 걸쳐. 이 자습서에서는 "마스터" 웹 페이지에 GridView에 나열 된 공급자 및 연결 된 제품 "정보" 페이지에 나열 된 함으로써 이러한 마스터/세부 정보 보고서를 구현 하는 방법에 살펴보았습니다. 마스터 웹 페이지의 각 공급 업체 행의 행을 전달 하는 세부 정보 페이지에 대 한 링크 포함 `SupplierID` 값입니다. GridView의 HyperLinkField를 사용 하 여 이러한 행 관련 링크를 쉽게 추가할 수 있습니다.

세부 정보 페이지에서 호출 하 여 수행 된 지정 된 공급자에 대 한 해당 제품을 검색 합니다 `ProductsBLL` 클래스의 `GetProductsBySupplierID(supplierID)` 메서드. 합니다 *`supplierID`* 매개 변수 값이 매개 변수 원본으로 쿼리 문자열을 사용 하 여 선언적으로 지정 되었습니다. 또한 살펴보았습니다 FormView를 사용 하 여 세부 정보 페이지에 공급자 세부 정보를 표시 하는 방법.

우리의 [다음 자습서](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md) 마지막 마스터/세부 정보 보고서입니다. 각 행의 선택 단추가 있는 GridView 제품 목록을 표시 하는 방법을 살펴보겠습니다. 선택 단추를 클릭 하면 동일한 페이지의 DetailsView 컨트롤에서 해당 제품의 세부 정보 표시 됩니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Hilton giesenow와 함께 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](master-detail-filtering-with-two-dropdownlists-vb.md)
> [다음](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md)
