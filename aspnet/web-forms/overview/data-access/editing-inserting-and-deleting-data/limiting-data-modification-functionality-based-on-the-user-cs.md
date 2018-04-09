---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-cs
title: 사용자 (C#)에 따라 데이터 수정 기능을 제한 | Microsoft Docs
author: rick-anderson
description: 사용자가 데이터를 편집할 수 있는 웹 응용 프로그램을 다른 사용자 계정에 다른 데이터 편집 권한을 가질 수 있습니다. 이 자습서에서는 살펴봅니다 어떻게 t...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/17/2006
ms.topic: article
ms.assetid: 2b251c82-77cf-4e36-baa9-b648eddaa394
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-cs
msc.type: authoredcontent
ms.openlocfilehash: b056536eeaa86ef2c73debe23dd38861f41b2a69
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="limiting-data-modification-functionality-based-on-the-user-c"></a>사용자 (C#)에 따라 데이터 수정 기능 제한
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_23_CS.exe) 또는 [PDF 다운로드](limiting-data-modification-functionality-based-on-the-user-cs/_static/datatutorial23cs1.pdf)

> 사용자가 데이터를 편집할 수 있는 웹 응용 프로그램을 다른 사용자 계정에 다른 데이터 편집 권한을 가질 수 있습니다. 이 자습서에서는 방문한 사용자 기반 데이터 수정 기능을 동적으로 조정 하는 방법을 검토 합니다.


## <a name="introduction"></a>소개

사용자 계정을 지원 하 고 다양 한 옵션, 보고서 및 로그인된 한 사용자를 기반으로 기능을 제공 하는 웹 응용 프로그램의 수입니다. 예를 들어이 자습서에서 하고자 할 수 있습니다 아마도-자신의 회사 이름, 공급 업체 정보 함께 제품-이름 및 포장 단위에 대 한 사이트 및 업데이트 일반 정보에 로그온 하려면 공급자 회사에서 사용자가 허용 합니다. 주소, 담당자의 정보 및 등입니다. 또한 다음에 로그온 하 고 주식형, 단위 수준에서 순서를 변경 하 고 등와 같은 제품 정보를 업데이트할 수 있도록 회사에서 사용자를 위한 일부 사용자 계정을 포함 하도록는 것이 좋습니다. 웹 응용 프로그램 (하지 로그온 사람)를 방문 하 여 익명 사용자를 통해서도 수 있지만 데이터를 보기만 하도록 제한 합니다. 이 사용자 계정 시스템 원위치에서에서 웹 컨트롤 데이터 삽입, 편집 및 삭제는 현재 로그온된 한 사용자에 대 한 적절 한 기능을 제공 하는 ASP.NET 페이지에서 원하는 것 म 합니다.

이 자습서에서는 방문한 사용자 기반 데이터 수정 기능을 동적으로 조정 하는 방법을 검토 합니다. 특히, 공급자가 제공 하는 제품을 나열 하는 GridView 함께 편집 가능한 DetailsView에 공급 업체 정보를 표시 하는 페이지를 만들겠습니다. 저희 회사는 페이지를 방문 하는 사용자 인 경우 다음을 수행할 수 있습니다: 모든 공급 업체의 정보 보기 해당 주소; 편집 공급자가 제공 하는 모든 제품에 대 한 정보를 편집 합니다. 그러나 특정 회사에서 사용자가을 하는 경우 수행할 수 있습니다만 보고 하 고 자신의 주소 정보를 편집 하 고, 중단으로 표시 되지 않은 해당 제품에만 편집할 수 있습니다.


[![저희 회사에서 사용자는 모든 공급 업체의 정보를 편집할 수 있습니다.](limiting-data-modification-functionality-based-on-the-user-cs/_static/image2.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image1.png)

**그림 1**: s Our 회사 수 편집 Any 공급 업체 정보에서에서 사용자 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image3.png))


[![사용자가 특정 공급 업체 수 있는 유일한 보기 및 편집의 정보는](limiting-data-modification-functionality-based-on-the-user-cs/_static/image5.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image4.png)

**그림 2**: 특정 공급 업체 수만 보기 및 편집의 정보는 사용자 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image6.png))


Let s가 시작 되었습니다.

> [!NOTE]
> ASP.NET 2.0 s 멤버 자격 시스템 만들고 관리 하 고 사용자 계정 확인 하기 위한 표준화 되 고 확장 가능한 플랫폼을 제공 합니다. 이 자습서의 범위를 벗어나는 멤버 자격 시스템 검사 결과 이므로,이 자습서에서는 대신 "fakes" 멤버 자격 저희 회사 또는 특정 공급 업체에서 지 여부를 선택 하는 익명 방문자를 허용 하 여 합니다. 멤버 자격에 대 한 자세한에 대 한 참조 내 [ASP.NET 2.0 검사 s 멤버 자격, 역할 및 프로필](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx) 계열 문서입니다.


## <a name="step-1-allowing-the-user-to-specify-their-access-rights"></a>1 단계: 사용자가 자신의 액세스 권한을 지정할 수 있도록

실제 웹 응용 프로그램에서는 회사에 대해 또는 특정 공급 업체에 대 한 작업 하 고 사용자가 사이트에 로그온 한 후이 정보는 ASP.NET 페이지에서 프로그래밍 방식으로 액세스할 수는 여부를 사용자의 계정 정보를 포함 합니다. 사용자 계정 정보 프로 파일 시스템을 통해 또는 일부 사용자 지정 방법으로 ASP.NET 2.0의 역할 시스템을 통해이 정보를 캡처할 수 없습니다.

이 자습서의 목표 조정 로그온된 한 사용자에 따라 데이터 수정 기능을 보여 주기 위해이 고 쇼케이스 ASP.NET 2.0 s 멤버 자격, 역할 및 프로 파일 시스템으로 다루지는지 않습니다, 되므로에서는 매우 간단 하 게 메커니즘을 결정 하는 기능 페이지-있는 사용자 수를 보고 하는 공급 업체 정보 하거나, 무엇을 편집할 수 해야 하는 경우 나타낼 수 DropDownList를 방문 하는 사용자에 대 한 특정 공급 업체의 정보를 볼 수 있으며 편집 합니다. 사용자는이 확인 및 모든 공급 업체 정보 (기본값)를 편집할 수 그녀 나타내면 그녀 수 모든 공급 업체를 통해 페이지, 모든 공급 업체의 주소 정보를 편집한 이름과 포장 선택한 공급자가 제공 하는 모든 제품에 대 한 단위를 편집 합니다. 그러나 사용자만 볼 수 있습니다 및 이름 및 해당 제품에 대 한 단위 정보 당 개수 별 영역의 특정 공급 업체, 다음 그녀 수만 해당 공급자에 대 한 세부 정보 및 제품을 볼 수만 업데이트 되었음을 나타내는 경우 *하지* 중단 되었습니다.

이 자습서의 첫 번째 단계, 하는 것이 DropDownList를 만들고 시스템에 공급 업체를 채웁니다. 열기는 `UserLevelAccess.aspx` 페이지에 `EditInsertDelete` 폴더를 DropDownList를 추가 인 `ID` 속성이로 설정 되어 `Suppliers`, 라는 새 ObjectDataSource이이 DropDownList 바인딩할 `AllSuppliersDataSource`합니다.


[![AllSuppliersDataSource 라는 새 ObjectDataSource 만들기](limiting-data-modification-functionality-based-on-the-user-cs/_static/image8.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image7.png)

**그림 3**: 명명 된 새 ObjectDataSource 만드는 `AllSuppliersDataSource` ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image9.png))


모든 공급자를 포함 하도록이 DropDownList 할 것 이므로 구성 ObjectDataSource를 호출 하 여 `SuppliersBLL` s 클래스 `GetSuppliers()` 메서드. 또한 되도록 ObjectDataSource s `Update()` 메서드가 매핑되는 `SuppliersBLL` s 클래스 `UpdateSupplierAddress` 메서드를이 ObjectDataSource로도 사용해 2 단계에서에서 추가할 예정이 니 DetailsView 합니다.

ObjectDataSource 마법사를 완료 한 후 구성 하 여 다음 단계를 완료 된 `Suppliers` DropDownList 표시 되도록는 `CompanyName` 사용 하 여 데이터 필드는 `SupplierID` 데이터 필드를 각각에 대 한 값으로 `ListItem`합니다.


[![Suppliers DropDownList CompanyName 및 SupplierID 데이터 필드를 사용 하도록 구성](limiting-data-modification-functionality-based-on-the-user-cs/_static/image11.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image10.png)

**그림 4**: 구성에서 `Suppliers` DropDownList를 사용 하 여는 `CompanyName` 및 `SupplierID` 데이터 필드 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image12.png))


이 시점에서 드롭다운 목록에는 데이터베이스에 공급 업체의 회사 이름을 나열합니다. 그러나 또한 해야 드롭다운 목록에 "Show/편집 모든 공급 업체" 옵션을 포함 합니다. 이를 위해 설정 된 `Suppliers` DropDownList s `AppendDataBoundItems` 속성을 `true` 다음 추가 `ListItem` 인 `Text` "모든 공급 업체 보기/편집"이 고 값이 속성은 `-1`합니다. 추가할 수 있습니다는 디자이너를 사용 하거나 선언 태그를 통해 직접 DropDownList s에 있는 줄임표를 클릭 하 고 속성 창으로 이동 하 여 `Items` 속성입니다.

> [!NOTE]
> 다시 참조는 [ *마스터/세부 정보 필터링 된 정도 DropDownList* ](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) 자습서에 대 한 자세한 내용은 데이터 바인딩된 DropDownList 모두 선택 항목을 추가 합니다.


이후에 `AppendDataBoundItems` 속성이 설정 되어 및 `ListItem` 추가 DropDownList s 선언 태그 같아야 합니다:


[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample1.aspx)]

그림 5에서는 브라우저를 통해 볼 때 현재 진행률의 스크린 샷을 보여 줍니다.


[![각 공급 업체에 대 한 개와 모든 ListItem Suppliers DropDownList는 표시를 포함](limiting-data-modification-functionality-based-on-the-user-cs/_static/image14.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image13.png)

**그림 5**:는 `Suppliers` DropDownList를 모두 표시 포함 `ListItem`, 플러스 한 각 공급 업체에 대 한 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image15.png))


사용자의 선택 영역을 변경한 후에 즉시 대시보드 사용자 인터페이스를 업데이트 하고자 하므로 설정는 `Suppliers` DropDownList s `AutoPostBack` 속성을 `true`합니다. 2 단계에서에서 DropDownList 선택을 기반으로 신뢰에 대 한 정보를 나타내는 DetailsView 컨트롤을 만들겠습니다. 그런 다음 3 단계에서는 만들어이 DropDownList s에 대 한 이벤트 처리기 `SelectedIndexChanged` DetailsView를 적절 한 공급 업체 정보에 바인딩하는 코드는 선택한 공급자에 따라 추가 이벤트입니다.

## <a name="step-2-adding-a-detailsview-control"></a>2 단계: DetailsView 컨트롤 추가

S DetailsView를 사용 하 여 공급 업체 정보를 표시할 수 있도록 합니다. 모든 공급자를 편집 하 고 볼 수 있는 사용자에 대 한 DetailsView는 지원 페이징, 사용자가 한 번에 공급 업체 정보 하나의 레코드를 단계별로 실행할 수 있도록 합니다. 그러나 사용자를 특정 공급 업체에 대 한 작동 DetailsView 해당 특정 공급 업체만 s 정보가 표시 됩니다 않으며 페이징 인터페이스에 포함 되지 않습니다. 두 경우 모두 DetailsView 사용자 공급 업체의 주소, city 및 country 필드를 편집할 수 있도록 해야 합니다.

DetailsView 아래에 있는 페이지에 추가 `Suppliers` DropDownList를 설정의 `ID` 속성을 `SupplierDetails`에 바인딩할는 `AllSuppliersDataSource` ObjectDataSource 이전 단계에서 만든 합니다. 다음으로 DetailsView s 스마트 태그에서 페이징 사용 및 편집 사용 확인란을 선택 합니다.

> [!NOTE]
> T don 스마트 DetailsView s에서 편집 사용 옵션을 참조 하는 경우 여기에 태그 s ObjectDataSource s 매핑되지 않은 `Update()` 메서드는 `SuppliersBLL` s 클래스 `UpdateSupplierAddress` 메서드. 잠시 뒤로 돌아가이 구성을 변경, 지나면 편집 사용 옵션 DetailsView s 스마트 태그에 표시 됩니다.


이후는 `SuppliersBLL` s 클래스 `UpdateSupplierAddress` 메서드만는 4 개의 매개 변수- `supplierID`, `address`, `city`, 및 `country` -DetailsView의 BoundFields 수정 하는 `CompanyName` 및 `Phone` BoundFields은 읽기 전용입니다. 또한 제거는 `SupplierID` BoundField 모두 합니다. 마지막으로 `AllSuppliersDataSource` ObjectDataSource에 현재 있는 해당 `OldValuesParameterFormatString` 속성이로 설정 `original_{0}`합니다. 선언적 구문 모두에서이 속성 설정을 제거 하거나 기본 값으로 설정 하 `{0}`합니다.

구성한 후의 `SupplierDetails` DetailsView 및 `AllSuppliersDataSource` ObjectDataSource를 다음과 같은 선언적 태그가 있는 됩니다.


[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample2.aspx)]

DetailsView 통해 페이징할 수는 시점에서 및 선택한 공급 업체의 주소 정보를 업데이트할 수에서 선택한 항목에 관계 없이 `Suppliers` DropDownList (그림 6 참조).


[![모든 공급 업체 정보를 볼 수 있으며 해당 주소를 업데이트](limiting-data-modification-functionality-based-on-the-user-cs/_static/image17.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image16.png)

**그림 6**: Any 공급 업체 정보를 볼 수, 하 고 해당 주소를 업데이트 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image18.png))


## <a name="step-3-displaying-only-the-selected-supplier-s-information"></a>3 단계: 선택된 협력 업체의 정보만 표시

현재 가격 페이지에서 선택한 특정 공급 업체 여부에 관계 없이 모든 공급자에 대 한 정보를 표시 된 `Suppliers` DropDownList 합니다. 선택한 공급자에 대 한 공급 업체 정보만 표시 하기 위해 다른 ObjectDataSource 특정 공급 업체에 대 한 정보를 검색 하는 가격 페이지에 추가 해야 합니다.

이름을 지정 하 고 페이지와 새 ObjectDataSource 추가 `SingleSupplierDataSource`합니다. 스마트 태그를 데이터 소스 구성 링크를 클릭 하 고 사용 하 여는 `SuppliersBLL` s 클래스 `GetSupplierBySupplierID(supplierID)` 메서드. 과 마찬가지로 `AllSuppliersDataSource` ObjectDataSource를가 `SingleSupplierDataSource` ObjectDataSource s `Update()` 메서드 매핑할는 `SuppliersBLL` s 클래스 `UpdateSupplierAddress` 메서드.


[![SingleSupplierDataSource ObjectDataSource GetSupplierBySupplierID(supplierID) 메서드를 사용 하도록 구성](limiting-data-modification-functionality-based-on-the-user-cs/_static/image20.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image19.png)

**그림 7**: 구성에서 `SingleSupplierDataSource` 사용할 ObjectDataSource는 `GetSupplierBySupplierID(supplierID)` 메서드 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image21.png))


에 대 한 매개 변수 소스를 지정 하 라는 메시지가 다시 우리는 다음으로 `GetSupplierBySupplierID(supplierID)` s 메서드에 `supplierID` 입력된 매개 변수입니다. 사용 하 여 드롭다운 목록에서 선택한 공급자에 대 한 정보를 표시 하는 데는 `Suppliers` DropDownList의 `SelectedValue` 매개 변수 소스로 속성입니다.


[![매개 변수 소스 supplierID로 Suppliers DropDownList를 사용 하 여](limiting-data-modification-functionality-based-on-the-user-cs/_static/image23.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image22.png)

**그림 8**: 사용 된 `Suppliers` 으로 DropDownList는 `supplierID` 매개 변수 소스 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image24.png))


추가 된이 두 번째 ObjectDataSource를 사용 하더라도 DetailsView 컨트롤은 항상 사용 하도록 구성 현재는 `AllSuppliersDataSource` ObjectDataSource 합니다. 필요에 따라 DetailsView에 사용 되는 데이터 소스를 조정 하는 논리를 추가 하는 `Suppliers` DropDownList 항목을 선택 합니다. 이를 위해 만들기는 `SelectedIndexChanged` Suppliers 드롭다운 목록에 대 한 이벤트 처리기입니다. 이 디자이너에 필요한 DropDownList를 두 번 클릭 하 여 가장 쉽게 만들 수 있습니다. 이 이벤트 처리기 사용 하 여 데이터 원본을 확인 하 고 데이터 DetailsView 다시 바인딩해야 합니다. 이 작업은 다음 코드와 함께 수행 됩니다.


[!code-csharp[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample3.cs)]

이벤트 처리기는 "모든 공급 업체 보기/편집" 옵션이 선택 되어 있는지 여부를 확인 하 여 시작 합니다. 설정에 있는 경우는 `SupplierDetails` DetailsView s `DataSourceID` 를 `AllSuppliersDataSource` 공급자 집합의 첫 번째 레코드를 설정 하 여 사용자를 반환 하 고는 `PageIndex` 속성을 0입니다. 그러나 사용자가 특정 공급 업체에서에서 선택한 DetailsView의 DropDownList 경우 `DataSourceID` 에 할당 된 `SingleSuppliersDataSource`합니다. 데이터에 관계 없이 사용 소스는 `SuppliersDetails` 모드는 읽기 전용 모드로 되돌아갑니다 및 데이터를 호출 하 여 다시 DetailsView에 바인딩할는 `SuppliersDetails` 컨트롤의 `DataBind()` 메서드.

이 이벤트 처리기 위치에 DetailsView 컨트롤 이제 표시 선택한 공급 업체는 쿼리에서 모든 공급 업체 중 확인할 수 있습니다 페이징 인터페이스를 통해 "모든 공급 업체 보기/편집" 옵션을 선택한 경우가 아니면 됩니다. 그림 9 "표시/편집 모든 공급 업체" 옵션을 선택 합니다; 페이지를 보여 줍니다. 사용자가 방문 하 고 모든 공급 업체를 업데이트할 수 있도록 페이징 인터페이스 있는지 note 합니다. 그림 10 선택한 Ma 트레이 공급 업체와 페이지를 보여줍니다. 만 Ma 트레이의 정보는 볼 수 있는 편집 가능한이 경우.


[![모든 공급 업체 정보 보기 및 편집](limiting-data-modification-functionality-based-on-the-user-cs/_static/image26.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image25.png)

**그림 9**: 모든 공급 업체 정보를 볼 수 있습니다 및 편집한 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image27.png))


[![선택한 공급자의 정보만 확인 및 편집할 수](limiting-data-modification-functionality-based-on-the-user-cs/_static/image29.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image28.png)

**그림 10**: 선택한 공급자의 정보로 보기 및 편집 된 될 수 있습니다 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image30.png))


> [!NOTE]
> 이 자습서에서는 DropDownList와 DetailsView 제어 s `EnableViewState` 으로 설정 되어 있어야 `true` (기본값) 때문에 DropDownList s `SelectedIndex` 및 DetailsView의 `DataSourceID` 게시할 s 속성 변경 내용을 저장 해야 합니다.


## <a name="step-4-listing-the-suppliers-products-in-an-editable-gridview"></a>편집 가능한 GridView에 공급 업체 제품을 나열 하는 4 단계:

전체 DetailsView와 다음 단계는 선택한 공급자가 제공 하는 해당 제품을 나열 하는 편집 가능한 GridView를 포함 하는 것입니다. 이 GridView에만 편집할 수 있도록 해야는 `ProductName` 및 `QuantityPerUnit` 필드입니다. 또한 페이지를 방문 하는 사용자를 특정 공급 업체에서 경우만 허용 해야 해당 제품에 대 한 업데이트 *하지* 중단 되었습니다. 먼저의 오버 로드를 추가 해야이를 위해는 `ProductsBLL` s 클래스 `UpdateProducts` 메서드는 수행 하는 테이블만 `ProductID`, `ProductName`, 및 `QuantityPerUnit` 입력으로 필드입니다. 에서는 다양 한 자습서에서는 미리이 프로세스를 진행 하면서 했습니다 사용에 추가 해야 하는 코드을 여기에서 확인 하는 s `ProductsBLL`:


[!code-csharp[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample4.cs)]

이 오버 로드를 가진 만들어지면 GridView 컨트롤 및 해당 관련된 ObjectDataSource를 추가 하려면 준비 된 것입니다. 페이지에는 새 GridView 추가 설정, 해당 `ID` 속성을 `ProductsBySupplier`, 라는 새 ObjectDataSource를 사용 하도록 구성 하 고 `ProductsBySupplierDataSource`합니다. 선택한 공급자가 해당 제품을 나열 하려면이 GridView 할 것 이므로 사용 된 `ProductsBLL` s 클래스 `GetProductsBySupplierID(supplierID)` 메서드. 또한 매핑할는 `Update()` 메서드를 새 `UpdateProduct` 방금 만든 오버 로드 합니다.


[![ObjectDataSource 방금 만든 UpdateProduct 오버 로드를 사용 하도록 구성](limiting-data-modification-functionality-based-on-the-user-cs/_static/image32.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image31.png)

**그림 11**: 구성에 사용 하 여 ObjectDataSource는 `UpdateProduct` 방금 만든 오버 로드 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image33.png))


에 대 한 매개 변수 소스를 선택 하 라는 메시지가 다시 우리는 `GetProductsBySupplierID(supplierID)` s 메서드에 `supplierID` 입력된 매개 변수입니다. 사용 하 여 DetailsView에서 선택한 공급자에 대 한 제품을 표시 하는 데는 `SuppliersDetails` DetailsView 컨트롤의 `SelectedValue` 매개 변수 소스로 속성입니다.


[![매개 변수 소스로 SuppliersDetails DetailsView의 SelectedValue 속성을 사용 하 여](limiting-data-modification-functionality-based-on-the-user-cs/_static/image35.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image34.png)

**그림 12**: 사용 된 `SuppliersDetails` DetailsView s `SelectedValue` 매개 변수 소스로 속성 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image36.png))


GridView 필드를 제외 하 고 모두 제거 GridView 돌아가 `ProductName`, `QuantityPerUnit`, 및 `Discontinued`표시는 `Discontinued` CheckBoxField 읽기 전용으로 합니다. 또한 GridView s 스마트 태그에서 편집 사용 옵션을 선택 합니다. 이러한 변경 내용을 적용 된 GridView 및 ObjectDataSource에 대 한 선언적 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample5.aspx)]

이 이전 ObjectDataSources이 하나의 s와 마찬가지로 `OldValuesParameterFormatString` 속성이 `original_{0}`, s 제품 이름 또는 단위당 수량을 업데이트 하려고 할 때 문제가 발생 합니다. 선언적 구문에서이 속성을 완전히 제거 하거나 해당 기본값으로 설정 `{0}`합니다.

이 구성이 완료 가격 페이지 이제 제품이 나열 GridView에서 선택한 공급자가 제공 (그림 13 참조). 현재 *모든*의 제품 이름 또는 포장 단위를 업데이트할 수 있습니다. 그러나 이러한 기능은 특정 공급 업체와 연결 된 사용자에 대해 지원 되지 않는 제품을 금지 수 있도록이 페이지 논리를 업데이트 해야 합니다. 5 단계에서에서 마지막 요소가 해결할 합니다.


[![선택한 공급자가 제공 하는 제품 표시](limiting-data-modification-functionality-based-on-the-user-cs/_static/image38.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image37.png)

**그림 13**: 선택한 공급 업체에서 제공 되는 제품 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image39.png))


> [!NOTE]
> 이 편집 가능한 GridView가 추가 된 `Suppliers` DropDownList의 `SelectedIndexChanged` GridView 읽기 전용 상태로 되돌리려면 이벤트 처리기를 업데이트 해야 합니다. 그렇지 않으면 다른 공급 업체가 제공한 중간에 제품 정보를 편집을 선택 하면 해당 인덱스가 새 공급 업체에 대 한 GridView에 편집 가능한 수도 있습니다. 이 방지 하려면 GridView s를 설정 하기만 `EditIndex` 속성을 `-1` 에 `SelectedIndexChanged` 이벤트 처리기입니다.


또한는 것이 중요 s 뷰 상태 수 GridView (기본 동작)을 사용할 수 있는지 생각해 보세요. GridView s를 설정 하면 `EnableViewState` 속성을 `false`, 위험을 실수로 삭제 하거나 편집을 기록 하는 동시 사용자가 실행 합니다. 참조 [경고: 동시성 문제가 있는 ASP.NET 2.0 Gridview/DetailsView/FormViews 해당 편집을 원하는 및/또는 삭제 및 뷰 상태를 사용 하지 않으면](http://scottonwriting.net/sowblog/posts/10054.aspx) 자세한 정보에 대 한 합니다.

## <a name="step-5-disallow-editing-for-discontinued-products-when-showedit-all-suppliers-is-not-selected"></a>5 단계: 지원 되지 않는 제품 때 보기/편집 모든 공급 업체는 선택 하지 않은 편집 허용 안 함

동안는 `ProductsBySupplier` GridView가 올바르게 작동 현재 부여 너무 많은 액세스 권한을 사용자에 게 특정 공급 업체에서 됩니다. 이 비즈니스 규칙에 따라 이러한 사용자는 지원 되지 않는 제품을 업데이트할 수 수 없습니다. 이 적용 하려면 म 수 숨길 (또는 해제) 지원 되지 않는 제품 공급 업체에서 사용자가 페이지를 방문 하는 경우 포함 된 GridView 행에서 편집 단추입니다.

GridView s에 대 한 이벤트 처리기를 만들고 `RowDataBound` 이벤트입니다. 이 이벤트 처리기에서 사용자가 Suppliers DropDownList s를 선택 하 여이 자습서에서 확인할 수 있는 특정 공급 업체와 연결 여부를 결정 해야 `SelectedValue` 속성-경우 것 이외의 형식-1로, 다음 사용자 s가 연결 된 특정 공급 업체입니다. 이러한 사용자에 대 한 제품 지원 되지 않는 여부를 결정 해야 합니다. 실제에 대 한 참조를 얻을 수 있습니다 `ProductRow` 통해 GridView 행에 바인딩된 인스턴스는 `e.Row.DataItem` 속성에 설명 된 대로 [ *GridView의 바닥글의에서 요약 정보 표시* ](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs.md) 자습서입니다. GridView s 이전 자습서에 설명 된 기술을 사용 하 여 CommandField에서에서 편집 단추에 대 한 프로그래밍 참조를 얻을 수 제품의 사용이 중지 되 면 [ *추가 클라이언트 쪽 확인 때 삭제* ](adding-client-side-confirmation-when-deleting-cs.md). 일단 숨기 거 나이 단추를 비활성화 한 다음 म 참조 해야 합니다.


[!code-csharp[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample6.cs)]

이 이벤트와 위치에 대 한 처리기를 편집할 수 없는이 페이지를 방문이 사용자로 특정 공급 업체에서 제품을 제공이 중단 된 경우 편집 5d; 단추로 숨겨져 이러한 제품에 대 한 있습니다. 예를 들어 Chef 한 100의 수프는 새로 식품 케이준 사용해 공급 업체에 대 한 지원 되지 않는 제품입니다. 이 제품에 대 한 편집 단추에서에서 숨겨져이 특정 공급 업체에 대 한 페이지를 방문 하는 경우 (그림 14 참조). 그러나 "보기/편집 모든 공급 업체"를 사용 하 여 방문 하는 경우 편집 단추는 (그림 15 참조).


[![Chef 한 100의 수프에 대 한 편집 단추는 숨겨집니다 공급 업체 관련 사용자에 대 한](limiting-data-modification-functionality-based-on-the-user-cs/_static/image41.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image40.png)

**그림 14**: Chef 한 100의 수프에 대 한 편집 단추 숨겨져 공급 업체 관련 사용자에 대 한 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image42.png))


[![보기/편집 모든 공급 업체 사용자에 대해 Chef 한 100의 수프에 대 한 편집 단추가 표시 됩니다.](limiting-data-modification-functionality-based-on-the-user-cs/_static/image44.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image43.png)

**그림 15**: 사용자에 대 한 보기/편집 모든 공급 업체, 수프 표시 되는 Chef 한 100 s에 대 한 편집 단추 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image45.png))


## <a name="checking-for-access-rights-in-the-business-logic-layer"></a>비즈니스 논리 계층에 대 한 액세스 권한을 확인 하는 중

페이지는 ASP.NET이이 자습서에서는 사용자가 볼 수 정보에 대해 모든 논리를 처리 하 고 업데이트할 수 그 어떤 제품입니다. 이상적으로이 논리는 비즈니스 논리 계층에 존재할 수도 합니다. 예를 들어는 `SuppliersBLL` s 클래스 `GetSuppliers()` (반환 하는 모든 공급 업체) 메서드는 현재 로그온된 한 사용자가 되도록 확인 포함 될 수 있습니다 *하지* 특정 공급 업체와 관련 된 합니다. 마찬가지로,는 `UpdateSupplierAddress` 메서드 하나 저희 회사에 대 한 작업 (및 따라서 모든 공급 업체 주소 정보를 업데이트할 수)는 현재 로그온된 한 사용자 확인 검사를 포함 될 수에 해당 데이터를 업데이트 하 고 공급 업체와 연결 되어 있습니다.

이 자습서의 s 사용자 권한은 DropDownList BLL 클래스에 액세스할 수 없는 페이지에 의해 결정 되기 때문에 이러한 BLL 레이어 검사 포함 없습니다 I. 멤버 자격 시스템 또는 (예: Windows 인증의 경우)에서 ASP.NET이 제공 아웃-기본 인증 스키마 중 하나를 사용 하는 경우 현재 로그온 한 사용자 s에 정보와 역할 정보에서에서 액세스할 수 있습니다 이러한 액세스를 받으므로 BLL 권한 확인 프레젠테이션 및 BLL 계층 모두에서 가능 합니다.

## <a name="summary"></a>요약

사용자 계정을 제공 하는 대부분의 사이트에 로그인 한 사용자 기반 데이터 수정 인터페이스를 사용자 지정 해야 합니다. 관리자 외 사용자만 업데이트 또는 직접 만든 레코드 삭제 제한 될 수 있습니다 하지만 관리자에 게 삭제 하 고 모든 레코드를 편집할 수. 있습니다 모든 시나리오 수, 데이터 웹 컨트롤, ObjectDataSource, 있으며 비즈니스 논리 계층 클래스를 추가 하 여 로그온된 한 사용자를 기반으로 특정 기능을 거부 확장 될 수 있습니다. 이 자습서에서는 사용자가 특정 공급 업체와 연결 인지 또는 회사에 대 한 작업 하는 경우에 따라 고 볼 수 있는 편집 가능한 데이터를 제한 하는 방법에 살펴보았습니다.

이 자습서에는 삽입, 업데이트 및 삭제 GridView, DetailsView, FormView 컨트롤을 사용 하 여 데이터를 검사 하는 완료 됩니다. 다음 자습서를 시작 페이징 및 정렬 기능 추가 설정 합니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [이전](adding-client-side-confirmation-when-deleting-cs.md)
> [다음](an-overview-of-inserting-updating-and-deleting-data-vb.md)
