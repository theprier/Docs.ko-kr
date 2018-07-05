---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-cs
title: 데이터 수정 기능 제한 사용자를 기반으로 합니다 (C#) | Microsoft Docs
author: rick-anderson
description: 사용자가 데이터를 편집할 수 있도록 웹 응용 프로그램에서 다른 사용자 계정에는 다른 데이터 편집 권한이 있을 수 있습니다. 이 자습서에서는 검토 방법 t...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/17/2006
ms.topic: article
ms.assetid: 2b251c82-77cf-4e36-baa9-b648eddaa394
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-cs
msc.type: authoredcontent
ms.openlocfilehash: d8141a47bc7036641a93a0946b43e1f8086b9a93
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37372244"
---
<a name="limiting-data-modification-functionality-based-on-the-user-c"></a>사용자 (C#)를 기반으로 하는 데이터 수정 기능 제한
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_23_CS.exe) 또는 [PDF 다운로드](limiting-data-modification-functionality-based-on-the-user-cs/_static/datatutorial23cs1.pdf)

> 사용자가 데이터를 편집할 수 있도록 웹 응용 프로그램에서 다른 사용자 계정에는 다른 데이터 편집 권한이 있을 수 있습니다. 이 자습서를 방문한 사용자를 기반으로 하는 데이터 수정 기능을 동적으로 조정 하는 방법을 살펴보겠습니다.


## <a name="introduction"></a>소개

다양 한 웹 응용 프로그램 사용자 계정을 지원 및 다양 한 옵션, 보고서 및 로그인된 사용자를 기반으로 하는 기능을 제공 합니다. 예를 들어이 자습서를 통해 수 하고자 아마도-해당 회사 이름과 같은 공급자 정보와 함께 해당 이름 및 단위 수량이 해당 제품-에 대 한 사이트 및 업데이트 일반 정보에 로그온 할 공급자 회사에서 사용자를 허용 합니다. 주소, 담당자가의 정보 및 등입니다. 또한 로그온 하 고 재고에서 단위 수준에서 다시 정렬 등와 같은 제품 정보를 업데이트할 수 있도록 회사에서 사용자의 일부 사용자 계정은 포함 하고자 할 수 있습니다. 웹 응용 프로그램 (사용자가 로그온 하지)를 방문 하 여 익명 사용자를 허용할 수 있지만 데이터를 보기만 하도록 제한 됩니다. 이러한 사용자 계정 시스템에서 위치를 사용 하 여 삽입, 편집 및 삭제는 현재 로그온된 한 사용자에 대 한 적절 한 기능을 제공 하 여 ASP.NET 페이지에서 데이터 웹 제어 하려고 합니다.

이 자습서를 방문한 사용자를 기반으로 하는 데이터 수정 기능을 동적으로 조정 하는 방법을 살펴보겠습니다. 특히는 편집 가능한 DetailsView 공급자가 제공 제품이 나열 되는 GridView와 함께 공급 업체 정보를 표시 하는 페이지를 만들겠습니다. 회사에서 페이지를 방문 하는 사용자 인 경우 가능 합니다: 모든 공급자가의 정보를 보려면 해당 주소; 편집 한 공급자가 제공 하는 모든 제품에 대 한 정보를 편집 합니다. 수만 있습니다, 있지만 사용자 인 경우 특정 회사에서 보고 하 고 자신의 주소 정보를 편집 하 고, 중단으로 표시 되지 않은 제품에만 편집할 수 있습니다.


[![회사에서 사용자는 모든 공급 업체의 정보를 편집할 수 있습니다.](limiting-data-modification-functionality-based-on-the-user-cs/_static/image2.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image1.png)

**그림 1**: 이러한 회사 수 편집 Any 공급자의 정보에서에서 사용자 ([큰 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image3.png))


[![사용자를 특정 공급 업체 수만 보기 및 편집 정보](limiting-data-modification-functionality-based-on-the-user-cs/_static/image5.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image4.png)

**그림 2**: 사용자를 특정 공급 업체 수만 보기 및 편집의 정보에서 ([큰 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image6.png))


Let s 시작!

> [!NOTE]
> ASP.NET 2.0 멤버 자격 시스템 만들기, 관리 및 사용자 계정 유효성 검사에 대 한 표준화 되 고 확장 가능한 플랫폼을 제공 합니다. 멤버 자격 시스템에 대 한 검사 이러한 자습서에서 다루지 이므로이 자습서 대신 "fakes" 멤버 자격 또는 회사에서 특정 공급 업체에서 지 여부를 선택할 수 익명 방문자를 허용 하 여 합니다. 참조 한 멤버 자격에 자세한 내용은 필자의 [ASP.NET 2.0 검사 s 멤버 자격, 역할 및 프로필](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx) 연재 기사입니다.


## <a name="step-1-allowing-the-user-to-specify-their-access-rights"></a>1 단계: 해당 액세스 권한을 지정할 수 있도록

실제 웹 응용 프로그램에서는 여부 또는 특정 공급 업체, 회사에 대 한 작업 및 사용자가 사이트에 로그온 한 후이 정보는 ASP.NET 페이지에서 프로그래밍 방식으로 액세스할 수는 사용자가의 계정 정보가 포함 됩니다. 프로필 시스템을 통해 또는 일부 사용자 지정 하는 수단을 통해 사용자 수준 계정 정보로 ASP.NET 2.0 역할 시스템을 통해이 정보를 캡처할 수 없습니다.

이 자습서의 목적은 조정 로그온된 사용자를 기반으로 하는 데이터 수정 기능을 보여 주기 위해 ASP.NET 2.0 소개 s 멤버 자격, 역할 및 프로필 시스템 하기 위한 것을 하므로 사용 하 여 매우 간단 하 게 메커니즘을 결정 합니다 기능 페이지-올 사용자 보기 및 편집 하는 공급 업체 정보 또는, 또는 무엇을 할 수 있어야 하는 경우 나타낼 수 있습니다 DropDownList를 방문 하는 사용자에 대 한 특정 공급 업체의 정보 확인 및 편집할 수 있습니다. 사용자는 자신이 확인 하 고 편집할 수 모든 공급 업체 정보 (기본값)를 나타내는 경우 모든 공급 업체를 통해 페이지 하 고, 모든 공급자가의 주소 정보를 편집 하 고, 이름 및 선택한 공급자가 제공 하는 모든 제품에 대 한 단위당 수량을 편집할 수 있습니다 그녀. 하지만 사용자만 볼 수 있습니다 및 특정 공급 업체, 다음 그녀는 수만 해당 공급자에 대 한 세부 정보 및 제품 보기 및 편집 수만 이름 및 수량이 해당 제품에 대 한 단위 정보를 업데이트 하는 경우 *없습니다* 중단 합니다.

이 자습서에서는 첫 번째 단계, 하는 것이 DropDownList를 만들고 시스템에서 공급자를 사용 하 여 채웁니다. 열기는 `UserLevelAccess.aspx` 페이지를 `EditInsertDelete` 폴더를 DropDownList를 추가입니다 `ID` 속성이로 설정 되어 `Suppliers`, 라는 새로운 ObjectDataSource는 하이 DropDownList를 바인딩하고 `AllSuppliersDataSource`합니다.


[![AllSuppliersDataSource 라는 새로운 ObjectDataSource는 만들기](limiting-data-modification-functionality-based-on-the-user-cs/_static/image8.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image7.png)

**그림 3**: 명명 된 새 ObjectDataSource 만들려면 `AllSuppliersDataSource` ([클릭 하 여 큰 이미지 보기](limiting-data-modification-functionality-based-on-the-user-cs/_static/image9.png))


모든 공급자를 포함 하도록이 DropDownList, 것 이므로 구성 ObjectDataSource를 호출 하 여 `SuppliersBLL` s 클래스 `GetSuppliers()` 메서드. ObjectDataSource가 확인 해야 `Update()` 메서드 매핑되는 `SuppliersBLL` s 클래스 `UpdateSupplierAddress` 메서드이 ObjectDataSource와도에서 사용할 2 단계에서에서 추가할 예정 DetailsView 합니다.

ObjectDataSource 마법사를 완료 한 후 구성 단계를 완료 합니다 `Suppliers` DropDownList 표시 되도록 합니다 `CompanyName` 사용 하 여 데이터 필드를 `SupplierID` 각각에 대 한 값으로 데이터 필드 `ListItem`합니다.


[![CompanyName 및 SupplierID 데이터 필드를 사용 하는 공급 업체 DropDownList를 구성 합니다.](limiting-data-modification-functionality-based-on-the-user-cs/_static/image11.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image10.png)

**그림 4**: 구성 합니다 `Suppliers` DropDownList를 사용 하 여 합니다 `CompanyName` 하 고 `SupplierID` 데이터 필드 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image12.png))


이 시점에서 DropDownList 데이터베이스의 공급 업체의 회사 이름을 나열합니다. 그러나 DropDownList에 "모든 공급 업체 표시/편집" 옵션을 포함 해야 했습니다. 이를 위해 설정 합니다 `Suppliers` DropDownList s `AppendDataBoundItems` 속성을 `true` 추가한 다음을 `ListItem` 인 `Text` 속성은 "모든 공급 업체 표시/편집"이 고 값이 `-1`합니다. 추가할 수 있습니다 선언적 태그를 통해 직접 또는 디자이너를 통해 속성 창으로 이동 하 고 DropDownList에서 줄임표를 클릭 하 여 `Items` 속성입니다.

> [!NOTE]
> 다시 참조를 [ *마스터/세부 정보 필터링으로 DropDownList* ](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) 보다 자세한 논의 데이터 바인딩된 DropDownList 모두 선택 항목을 추가 하는 방법에 대 한 자습서입니다.


후 합니다 `AppendDataBoundItems` 속성이 설정 되어 및 `ListItem` 추가 DropDownList s 선언적 태그와 같습니다.


[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample1.aspx)]

그림 5는 브라우저를 통해 볼 때 스크린샷을 현재 진행률을 보여줍니다.


[![모든 ListItem와 각 공급자에 대 한 쇼를 포함 하는 공급 업체 DropDownList](limiting-data-modification-functionality-based-on-the-user-cs/_static/image14.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image13.png)

**그림 5**: 합니다 `Suppliers` DropDownList 포함 모두 표시 `ListItem`, Plus의 경우 첫 번째 각 공급 업체 ([클릭 하 여 큰 이미지 보기](limiting-data-modification-functionality-based-on-the-user-cs/_static/image15.png))


사용자가 선택 영역을 변경한 후에 즉시 사용자 인터페이스를 업데이트 하려고 하므로 설정 합니다 `Suppliers` DropDownList s `AutoPostBack` 속성을 `true`입니다. 2 단계에서에서 DropDownList 선택을 기반으로 신뢰에 대 한 정보를 보여주는 DetailsView 컨트롤을 만듭니다. 그런 다음 3 단계에서에서 만들겠습니다이 DropDownList s에 대 한 이벤트 처리기 `SelectedIndexChanged` 선택한 공급자를 기반으로 적절 한 공급 업체 정보 DetailsView를 바인딩하는 코드를 추가 하는 이벤트입니다.

## <a name="step-2-adding-a-detailsview-control"></a>2 단계: DetailsView 컨트롤 추가

S를 DetailsView를 사용 하 여 공급 업체 정보를 표시할 수 있습니다. 확인 및 모든 공급 업체를 편집할 수 있는 사용자에 대해 DetailsView는 지원 페이징, 한 번에 공급 업체 정보 하나의 레코드를 단계별로 실행할 수 있도록 허용 합니다. 그러나 사용자 특정 공급 업체에 대해 작동 하는 경우 DetailsView 해당 특정 공급자만 s 정보가 표시 됩니다 있으며 페이징 인터페이스를 포함 하지 않습니다. 두 경우 모두 DetailsView 사용자가 공급자의의 주소, 도시 및 국가 필드를 편집 하도록 허용 해야 합니다.

아래에 있는 페이지에는 DetailsView를 추가 합니다 `Suppliers` 드롭다운 목록에서 설정 해당 `ID` 속성을 `SupplierDetails`에 바인딩할는 `AllSuppliersDataSource` 이전 단계에서 만든 ObjectDataSource. 다음으로, DetailsView가 스마트 태그에서 페이징을 사용 하도록 설정 하 고 편집 사용 확인란을 확인 합니다.

> [!NOTE]
> Don t 스마트 DetailsView s에서 편집 사용 옵션을 참조 하는 경우 태그 s ObjectDataSource가 매핑되지 않은 `Update()` 메서드를 `SuppliersBLL` s 클래스 `UpdateSupplierAddress` 메서드. 시간을 내어 돌아가서이 구성을 변경에는 편집 사용 옵션 DetailsView가 스마트 태그에 표시 됩니다.


이후를 `SuppliersBLL` s 클래스 `UpdateSupplierAddress` 메서드 4 개의 매개 변수-허용 `supplierID`, `address`, `city`, 및 `country` -DetailsView의 BoundFields 수정 되도록를 `CompanyName` 및 `Phone` BoundFields은 읽기 전용입니다. 또한 제거는 `SupplierID` BoundField 모두 합니다. 마지막으로, 합니다 `AllSuppliersDataSource` ObjectDataSource 갖고 해당 `OldValuesParameterFormatString` 속성으로 설정 `original_{0}`합니다. 잠시 선언적 구문 모두에서이 속성 설정을 제거 하거나 값을 기본값으로 설정 `{0}`합니다.

구성한 후 합니다 `SupplierDetails` DetailsView 및 `AllSuppliersDataSource` ObjectDataSource, 다음과 같은 선언적 태그가 포함 됩니다.


[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample2.aspx)]

DetailsView 통해 페이징할 수 이때 및 선택한 공급자가의 주소 정보를 업데이트할 수에서 선택한 옵션에 관계 없이 `Suppliers` DropDownList (그림 6 참조).


[![공급 업체 정보를 볼 수 있으며 해당 주소를 업데이트](limiting-data-modification-functionality-based-on-the-user-cs/_static/image17.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image16.png)

**그림 6**: 모든 공급 업체 정보를 볼 수, 하 고 해당 주소를 업데이트 ([큰 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image18.png))


## <a name="step-3-displaying-only-the-selected-supplier-s-information"></a>선택한 공급자가의 정보만 표시 하는 3 단계:

이 페이지에는 현재 특정 공급 업체의 선택 여부에 관계 없이 모든 공급 업체에 대 한 정보가 표시 됩니다는 `Suppliers` DropDownList 합니다. 선택한 공급자에 대 한 공급자 정보만 표시 하기 위해 다른 ObjectDataSource 특정 공급 업체에 대 한 정보를 검색 하는 페이지에 추가 해야 합니다.

추가할 새 ObjectDataSource 페이지 이름을 `SingleSupplierDataSource`입니다. 스마트 태그를 데이터 소스 구성 링크를 클릭 하 고 사용 하 게 합니다 `SuppliersBLL` s 클래스 `GetSupplierBySupplierID(supplierID)` 메서드. 와 마찬가지로 `AllSuppliersDataSource` ObjectDataSource를가 합니다 `SingleSupplierDataSource` ObjectDataSource s `Update()` 메서드에 매핑할를 `SuppliersBLL` s 클래스 `UpdateSupplierAddress` 메서드.


[![GetSupplierBySupplierID(supplierID) 메서드를 사용 하 여 SingleSupplierDataSource ObjectDataSource 구성](limiting-data-modification-functionality-based-on-the-user-cs/_static/image20.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image19.png)

**그림 7**: 구성 합니다 `SingleSupplierDataSource` ObjectDataSource 사용 합니다 `GetSupplierBySupplierID(supplierID)` 메서드 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image21.png))


매개 변수 원본에 대 한을 지정 하 라는 메시지가 다시 우리는 다음으로 `GetSupplierBySupplierID(supplierID)` s 메서드에 `supplierID` 입력된 매개 변수입니다. 사용 하 여 드롭다운 목록에서 선택한 공급자에 대 한 정보를 표시 하려고 하므로 합니다 `Suppliers` DropDownList의 `SelectedValue` 속성 매개 변수 원본으로 합니다.


[![공급 업체 DropDownList supplierID 매개 변수 원본으로 사용](limiting-data-modification-functionality-based-on-the-user-cs/_static/image23.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image22.png)

**그림 8**: 사용 합니다 `Suppliers` 으로 DropDownList를 `supplierID` 매개 변수 원본 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image24.png))


추가이 두 번째 ObjectDataSource를 사용 하더라도 DetailsView 컨트롤은 항상 사용 하도록 구성할 현재는 `AllSuppliersDataSource` ObjectDataSource 합니다. 에 따라 DetailsView에 사용 되는 데이터 소스를 조정 하는 논리를 추가 해야 합니다 `Suppliers` DropDownList 항목을 선택 합니다. 이렇게 하려면 만들기를 `SelectedIndexChanged` Suppliers DropDownList에 대 한 이벤트 처리기입니다. 이 디자이너에서 DropDownList를 두 번 클릭 하 여 가장 쉽게 만들 수 있습니다. 이 이벤트 처리기 사용 하 여 데이터 원본을 확인 해야 하며 데이터 DetailsView 다시 바인딩해야 합니다. 이 작업은 다음 코드를 사용 하 여 수행 됩니다.


[!code-csharp[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample3.cs)]

이벤트 처리기는 "모든 공급 업체 표시/편집" 옵션이 선택 되어 있는지 여부를 확인 하 여 시작 합니다. 성공한 경우에 설정 합니다 `SupplierDetails` DetailsView s `DataSourceID` 에 `AllSuppliersDataSource` 설정 하 여 공급자 집합에서 첫 번째 레코드를 반환 하 고는 `PageIndex` 속성을 0. 그러나 사용자가 특정 공급 업체에서에서 선택한 DropDownList, DetailsView s 라면 `DataSourceID` 에 할당 된 `SingleSuppliersDataSource`합니다. 사용은 원본 데이터에 상관 없이 `SuppliersDetails` 모드는 읽기 전용 모드로 취소 되 고 데이터를 호출 하 여 다시 DetailsView에 바인딩되는 `SuppliersDetails` s control `DataBind()` 메서드.

이 이벤트 처리기를 사용 하 여 DetailsView 컨트롤 이제 표시 선택한 공급자에 게 "모든 공급 업체 표시/편집" 옵션을 선택한 경우 모든 공급 업체의 확인할 수 있습니다 페이징 인터페이스를 통해 하지 않으면 됩니다. 그림 9 "표시/편집 모든 공급 업체" 옵션이 선택 되어; 페이지를 보여 줍니다. 사용자가 방문 하 여 모든 업데이트 페이징 인터페이스 있는지 note 합니다. 그림 10 선택한 Ma 트레이 공급자를 사용 하 여 페이지를 보여 줍니다. Ma 트레이의 정보만 볼 수 있고 편집할 수 있는 경우에 합니다.


[![모든 공급 업체 정보 보기 및 편집](limiting-data-modification-functionality-based-on-the-user-cs/_static/image26.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image25.png)

**그림 9**: 모든 편집 하 고 공급 업체 정보를 볼 수 있습니다 ([큰 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image27.png))


[![선택한 공급자가의 정보만 확인 및 편집할 수](limiting-data-modification-functionality-based-on-the-user-cs/_static/image29.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image28.png)

**그림 10**: 선택한 공급자가의 정보 보기 및 편집 될 수 있습니다 ([큰 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image30.png))


> [!NOTE]
> 이 자습서에서는 DropDownList 및 DetailsView 컨트롤 s `EnableViewState` 으로 설정 되어 있어야 `true` (기본값) 때문에 DropDownList s `SelectedIndex` 및 DetailsView의 `DataSourceID` 게시할 s 속성 변경 내용을 저장 해야 합니다.


## <a name="step-4-listing-the-suppliers-products-in-an-editable-gridview"></a>편집할 수는 GridView에 공급 업체 제품을 나열 하는 4 단계:

전체 DetailsView를 사용 하 여 다음 단계는 선택한 공급자가 제공 하는 이러한 제품을 나열 하는 편집 가능한 GridView를 포함 하는 것입니다. 이 GridView에만 편집할 수 있도록 해야 합니다 `ProductName` 고 `QuantityPerUnit` 필드입니다. 또한 특정 공급 업체에서 페이지를 방문 하는 사용자 인 경우만 허용 해야 해당 제품을 업데이트 *되지* 중단 합니다. 먼저 오버 로드를 추가 해야이 작업을 수행 하는 `ProductsBLL` s 클래스 `UpdateProducts` 에서 사용 하는 메서드만 `ProductID`, `ProductName`, 및 `QuantityPerUnit` 입력 필드입니다. 에서는 다양 한 자습서에서는 먼저이 프로세스를 통해 단계별 ve s에 추가 해야 하는 코드을 여기에서 확인 수 있습니다 `ProductsBLL`:


[!code-csharp[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample4.cs)]

이 오버 로드로 만든 GridView 컨트롤 및 해당 관련 된 ObjectDataSource에 추가할 준비가 했습니다. GridView를 새 페이지로 추가 해당 `ID` 속성을 `ProductsBySupplier`, 명명 된 새 ObjectDataSource를 사용 하도록 구성 하 고 `ProductsBySupplierDataSource`입니다. 선택한 공급자가 해당 제품을 나열 하려면이 GridView, 것 이므로 사용 합니다 `ProductsBLL` s 클래스 `GetProductsBySupplierID(supplierID)` 메서드. 매핑할 수도 합니다 `Update()` 메서드를 새 `UpdateProduct` 방금 만든 오버 로드 합니다.


[![방금 만든 UpdateProduct 오버 로드를 사용 하는 ObjectDataSource 구성](limiting-data-modification-functionality-based-on-the-user-cs/_static/image32.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image31.png)

**그림 11**: ObjectDataSource 사용 하도록 구성 된 `UpdateProduct` 방금 만든 오버 로드 ([클릭 하 여 큰 이미지 보기](limiting-data-modification-functionality-based-on-the-user-cs/_static/image33.png))


에 대 한 매개 변수 소스를 선택 하 라는 메시지가 다시 우리는 `GetProductsBySupplierID(supplierID)` s 메서드에 `supplierID` 입력된 매개 변수입니다. DetailsView를 사용 하 여에서 선택한 공급자에 대 한 제품을 표시 하려고 하므로 합니다 `SuppliersDetails` DetailsView 컨트롤의 `SelectedValue` 속성 매개 변수 원본으로 합니다.


[![매개 변수 원본으로 SuppliersDetails DetailsView의 SelectedValue 속성 사용](limiting-data-modification-functionality-based-on-the-user-cs/_static/image35.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image34.png)

**그림 12**: 사용 합니다 `SuppliersDetails` DetailsView s `SelectedValue` 매개 변수 원본 속성 ([클릭 하 여 큰 이미지 보기](limiting-data-modification-functionality-based-on-the-user-cs/_static/image36.png))


GridView 필드를 제외 하 고 모두 제거 GridView 돌아가기 `ProductName`, `QuantityPerUnit`, 및 `Discontinued`표시는 `Discontinued` CheckBoxField 읽기 전용으로 합니다. 또한 GridView가 스마트 태그에서 편집 사용 옵션을 선택 합니다. 이러한 변경 내용이 GridView 및 ObjectDataSource의 선언 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample5.aspx)]

이 이전 ObjectDataSources, 1이 s와 마찬가지로 `OldValuesParameterFormatString` 속성이 `original_{0}`, s 제품 이름 또는 단위당 수량을 업데이트 하려고 할 때 문제가 발생 합니다. 선언적 구문에서이 속성을 완전히 제거 하거나 해당 기본값으로 설정 `{0}`합니다.

이 구성이 완료 페이지 이제 나열 GridView에서 선택한 공급자가 제공 하는 제품 (그림 13 참조). 현재 *모든*의 제품 이름 또는 포장 단위를 업데이트할 수 있습니다. 그러나 이러한 기능은 특정 공급 업체와 연결 된 사용자에 대 한 지원 되지 않는 제품에 대 한 금지 됩니다 있도록이 페이지 논리를 업데이트 해야 합니다. 5 단계에서에서이 마지막 부분이 해결할 합니다.


[![선택한 공급자가 제공 하는 제품 표시](limiting-data-modification-functionality-based-on-the-user-cs/_static/image38.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image37.png)

**그림 13**: 표시 되는 선택한 공급자가 제공 되는 제품 ([큰 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image39.png))


> [!NOTE]
> 이 편집 가능한 GridView 추가 합니다 `Suppliers` DropDownList의 `SelectedIndexChanged` GridView 읽기 전용 상태를 반환 하도록 이벤트 처리기를 업데이트 해야 합니다. 이 고, 그렇지 제품 정보를 편집 중 다른 공급자를 선택 하면 해당 새 공급 업체에 대 한 GridView 인덱스 편집할 수도 있습니다. 이 방지 하려면 GridView s를 설정 하기만 `EditIndex` 속성을 `-1` 에 `SelectedIndexChanged` 이벤트 처리기입니다.


또한 GridView가의 보기 상태 사용 (기본 동작)는 중요 한 것을 기억 하십시오. GridView가 설정 하는 경우 `EnableViewState` 속성을 `false`, 동시 사용자가 실수로 삭제 하거나 편집할 레코드의 위험이 있습니다. 참조 [경고: 동시성 문제 사용 하 여 ASP.NET 2.0 Gridview/DetailsView/FormViews 해당 지원 편집 및/또는 삭제 하 고 있는 뷰 상태를 사용 하지 않도록 설정](http://scottonwriting.net/sowblog/posts/10054.aspx) 자세한 내용은 합니다.

## <a name="step-5-disallow-editing-for-discontinued-products-when-showedit-all-suppliers-is-not-selected"></a>5 단계: 지원 되지 않는 제품 때 표시/편집 모든 공급 업체는 선택 하지 편집 허용 안 함

하지만 `ProductsBySupplier` GridView를 완벽 하 게 작동 하기 현재 너무 많은 액세스 권한을 부여 특정 공급 업체에서 해당 사용자입니다. 이 비즈니스 규칙에 따라 이러한 사용자 없습니다 수 있어야 지원 되지 않는 제품을 업데이트 합니다. 이 위해서는에서는 수 숨기기 (또는 사용 하지 않도록 설정) 공급자에서 사용자가 페이지를 방문 하는 경우 지원 되지 않는 제품을 사용 하 여 GridView 행에서 편집 단추입니다.

GridView s에 대 한 이벤트 처리기를 만들고 `RowDataBound` 이벤트입니다. 이 이벤트 처리기에서 사용자 Suppliers DropDownList s를 확인 하 여이 자습서에서는 확인할 수 있습니다 특정 공급 업체와 관련이 있는지 여부를 결정 해야 `SelectedValue` 속성-하는 경우 해당 s-1로, 사용자 보다 다른 것은 특정 공급자를 사용 하 여 연결 합니다. 이러한 사용자에 대 한 다음 제품이 단종 된 여부를 결정 해야 합니다. 이전 나옵니다 실제에 대 한 참조 `ProductRow` 인스턴스를 통해 GridView 행에 바인딩된를 `e.Row.DataItem` 에 설명 된 대로 속성을 [ *바닥글 GridView에서에서 요약 정보 표시* ](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs.md) 자습서입니다. 에서는 이전 자습서에서 설명한 기술을 사용 하 여 CommandField GridView에서에서 편집 단추에 대 한 프로그래밍 참조 나옵니다 제품이 단종 된 경우 [ *추가 클라이언트 쪽 확인 삭제* ](adding-client-side-confirmation-when-deleting-cs.md). 숨기 거 나 단추를 비활성화 한 다음 우리가 참조가 있는 것입니다.


[!code-csharp[Main](limiting-data-modification-functionality-based-on-the-user-cs/samples/sample6.cs)]

이 이벤트와 처리기를 편집할 수 없으면이 페이지를 방문 사용자로 특정 공급 업체에서 지원 제품 편집 단추와 숨겨져 이러한 제품에 대 한 있습니다. 예를 들어, Chef 한 100의 수프 New Orleans 케이준 Delights 공급자에 대 한 지원 되지 않는 제품입니다. 이 제품에 대 한 편집 단추에서에서 숨겨집니다이 특정 공급 업체에 대 한 페이지를 방문 하면 (그림 14 참조). 그러나 "표시/편집 모든 공급 업체"를 사용 하 여 방문 하는 경우 편집 단추는 사용할 수 있습니다 (그림 15 참조).


[![공급자 특정 사용자에 대 한 Chef 한 100의 수프에 대 한 편집 단추 숨겨져](limiting-data-modification-functionality-based-on-the-user-cs/_static/image41.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image40.png)

**그림 14**: Chef 한 100 s 수프 편집 단추가 숨겨집니다 공급자 특정 사용자에 대 한 ([큰 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image42.png))


[![표시/편집 모든 공급 업체 사용자에 대해 Chef 한 100 s 수프 편집 단추가 표시 됩니다.](limiting-data-modification-functionality-based-on-the-user-cs/_static/image44.png)](limiting-data-modification-functionality-based-on-the-user-cs/_static/image43.png)

**그림 15**: 사용자에 대 한 표시/편집 모든 공급 업체, 수프 표시 되는 Chef 한 100 s에 대 한 편집 단추 ([큰 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-cs/_static/image45.png))


## <a name="checking-for-access-rights-in-the-business-logic-layer"></a>비즈니스 논리 계층에 대 한 액세스 권한 확인

이 자습서는 ASP.NET 페이지는 사용자가 볼 수 있는 정보를 관련 하 여 모든 논리를 처리 하 고 업데이트할 수 그 어떤 제품입니다. 이상적으로이 논리는 비즈니스 논리 계층에 존재할 수도 있습니다. 예를 들어,를 `SuppliersBLL` s 클래스 `GetSuppliers()` (반환 하는 모든 공급 업체) 메서드는 현재 로그온된 한 사용자가 확인 하는 검사가 포함 될 수 있습니다 *하지* 특정 공급자를 사용 하 여 연결 합니다. 마찬가지로,는 `UpdateSupplierAddress` 메서드는 하거나 회사에 대 한 작업 (및 따라서 모든 공급 업체 주소 정보를 업데이트할 수)는 현재 로그온된 한 사용자를 확인 하는 검사가 포함 될 수 있습니다 또는 해당 데이터를 업데이트 하는 공급자를 사용 하 여 연결 됩니다.

이 자습서에서 사용자가의 권한을 DropDownList 클래스 BLL에 액세스할 수 없는 페이지에 의해 결정 되기 때문에 이러한 계층 BLL 검사 포함 되지 I. 멤버 자격 시스템 또는 아웃-기본 인증 체계 (예: Windows 인증 사용), ASP.NET에서 제공 중 하나를 사용 하는 경우 현재 로그온 한 사용자가 정보와 역할에서에서 액세스할 수 있습니다 이러한 액세스를 받으므로 BLL은 권한 확인 프레젠테이션 및 BLL 계층 모두에서 가능 합니다.

## <a name="summary"></a>요약

사용자 계정을 제공 하는 대부분의 사이트에 로그인된 한 사용자에 따라 데이터 수정 인터페이스 사용자 지정 해야 합니다. 비관리자 사용자만 업데이트 또는 직접 만든 레코드를 삭제 하려면 제한 될 수 있습니다 하는 반면 관리자에 게 삭제 하 고 모든 레코드를 편집 하는 일을 할 수 있습니다. 반갑지 않은 경우 수, 데이터 웹 컨트롤, ObjectDataSource에 있으며 추가 하 여 로그온된 한 사용자를 기반으로 특정 기능을 거부 하는 비즈니스 논리 계층 클래스를 확장할 수 있습니다. 이 자습서에서는 사용자가 특정 공급 업체를 사용 하 여 연결 인지 또는 회사에 대 한 협력 하는 경우에 따라 보고 편집할 수 있는 데이터를 제한 하는 방법에 살펴보았습니다.

이 자습서의 삽입, 업데이트 및 GridView, DetailsView 및 FormView 컨트롤을 사용 하 여 데이터를 삭제 하는 검사를 완료 했습니다. 다음 자습서를 시작 페이징 및 정렬 기능 추가 설정 됩니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [이전](adding-client-side-confirmation-when-deleting-cs.md)
> [다음](an-overview-of-inserting-updating-and-deleting-data-vb.md)
