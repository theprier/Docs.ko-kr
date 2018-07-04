---
uid: web-forms/overview/data-access/introduction/creating-a-business-logic-layer-vb
title: 비즈니스 논리 레이어 만들기 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에는 계층 BLL (비즈니스 논리) t 간의 데이터 교환 위한 중간자로 사용 되는 비즈니스 규칙에 중앙 집중화 하는 방법을 살펴보겠습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 142e5181-29ce-4bb9-907b-2a0becf7928b
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/introduction/creating-a-business-logic-layer-vb
msc.type: authoredcontent
ms.openlocfilehash: 06799205ca180ca504083a6e2e99faceb79b22fc
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37375317"
---
<a name="creating-a-business-logic-layer-vb"></a>비즈니스 논리 레이어 만들기 (VB)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_2_VB.exe) 또는 [PDF 다운로드](creating-a-business-logic-layer-vb/_static/datatutorial02vb1.pdf)

> 이 자습서에는 계층 BLL (비즈니스 논리) 프레젠테이션 계층과 DAL 간의 데이터 교환 위한 중간자로 사용 되는 비즈니스 규칙에 중앙 집중화 하는 방법을 살펴보겠습니다.


## <a name="introduction"></a>소개

(DAL (데이터 액세스 계층)에서 만든 합니다 [첫 번째 자습서](creating-a-data-access-layer-vb.md) 프레젠테이션 논리에서 논리를 액세스 하는 데이터를 명확 하 게 구분 합니다. 그러나 DAL 프레젠테이션 계층에서 데이터 액세스 세부 정보를 명확 하 게 구분을 하는 동안 적용 될 수 있는 모든 비즈니스 규칙 적용 하지 않습니다. 예를 들어, 응용 프로그램에서는 허용 하지 않을 수는 `CategoryID` 또는 `SupplierID` 필드를 `Products` 수정할 때 테이블은 `Discontinued` 필드를 1로 설정 하거나 하고자 할 수 있습니다 이라는 규칙을 적용 하는 경우를 금지는 직원 하 고용 된 사람에 의해 관리 됩니다. 또 다른 일반적인 시나리오는 특정 역할에 사용자를 가장만 권한 부여 제품 삭제 하거나 변경할 수는 `UnitPrice` 값입니다.

이 자습서에는 계층 BLL (비즈니스 논리) 프레젠테이션 계층과 DAL 간의 데이터 교환 위한 중간자로 사용 되는 이러한 비즈니스 규칙에 중앙 집중화 하는 방법을 살펴보겠습니다. 실제 응용 프로그램에서는 별도 클래스 라이브러리 프로젝트로; BLL은 구현 그러나이 자습서에 대 한 구현 하겠습니다 BLL 일련의 클래스는 `App_Code` 프로젝트 구조를 단순화 하기 위해 폴더입니다. 그림 1에서는 프레젠테이션 계층, BLL 및 DAL 간의 아키텍처 관계를 보여 줍니다.


![BLL은 데이터 액세스 계층에서 프레젠테이션 계층을 분리 하 고 비즈니스 규칙 적용](creating-a-business-logic-layer-vb/_static/image1.png)

**그림 1**: BLL은 데이터 액세스 계층에서 프레젠테이션 계층을 분리 하 고 비즈니스 규칙 적용


구현 하는 별도 클래스를 만드는 대신 우리의 [비즈니스 논리](http://en.wikipedia.org/wiki/Business_logic), partial 클래스를 사용 하 여 입력 데이터 집합에서 직접 또는이 논리를 배치할 수 있습니다. 을 만들고 입력 데이터 집합 확장의 예제에 대 한 첫 번째 자습서를 다시 가리킵니다.

## <a name="step-1-creating-the-bll-classes"></a>1 단계: BLL 클래스 만들기

이 BLL은 DAL;에서 각 TableAdapter에 대해 하나씩 네 개의 클래스 구성 각 클래스 BLL는 메서드를 검색, 삽입, 업데이트 및 적절 한 비즈니스 규칙을 적용 하는 DAL에서 해당 TableAdapter에서 삭제 해야 합니다.

두 개의 하위 폴더를 만들어 보겠습니다을 보다 명확 하 게 DAL 및 BLL에 관련 된 클래스를 구분 합니다 `App_Code` 폴더를 `DAL` 및 `BLL`합니다. 오른쪽 단추로 클릭 하면는 `App_Code` 솔루션 탐색기에서 폴더 및 새 폴더를 선택 합니다. 이러한 두 개의 폴더를 만든 후에 첫 번째 자습서에서 만든 형식화 된 데이터 집합을 이동 합니다 `DAL` 하위 폴더입니다.

다음으로, 네 개의 BLL 클래스 파일을 만듭니다는 `BLL` 하위 폴더입니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭는 `BLL` 하위 폴더에 새 항목 추가 선택 하 고 클래스 템플릿을 선택 합니다. 4 개 클래스의 이름을 `ProductsBLL`, `CategoriesBLL`를 `SuppliersBLL`, 및 `EmployeesBLL`합니다.


![App_Code 폴더에 4 개의 새 클래스 추가](creating-a-business-logic-layer-vb/_static/image2.png)

**그림 2**: 4 개의 새 클래스를 추가 합니다 `App_Code` 폴더


다음으로, 첫 번째 자습서에서 Tableadapter에 대 한 정의 된 메서드를 래핑하는 클래스의 각 메서드를 추가 해 보겠습니다. 이제 이러한 메서드를 호출 하면 직접 DAL; 나중에 필요한 비즈니스 논리 추가 반환 합니다.

> [!NOTE]
> Visual Studio Standard Edition을 사용 하는 경우 또는 위의 (즉, 여러분이 *하지* Visual Web Developer를 사용 하 여), 필요에 따라 시각적으로 사용 하 여 클래스를 디자인할 수 있습니다를 [클래스 디자이너](https://msdn.microsoft.com/library/default.asp?url=/library/dv_vstechart/html/clssdsgnr.asp)합니다. 참조 된 [클래스 디자이너 블로그](https://blogs.msdn.com/classdesigner/default.aspx) Visual Studio에서이 새로운 기능에 대 한 자세한 내용은 합니다.


에 대 한는 `ProductsBLL` 클래스는 총 7 개의 메서드를 추가 해야 합니다.

- `GetProducts()` 모든 제품을 반환합니다.
- `GetProductByProductID(productID)` 지정 된 제품 ID 사용 하 여 곱을 반환합니다.
- `GetProductsByCategoryID(categoryID)` 지정 된 범주의 모든 제품을 반환합니다.
- `GetProductsBySupplier(supplierID)` 지정 된 공급자 로부터 모든 제품을 반환합니다.
- `AddProduct(productName, supplierID, categoryID, quantityPerUnit, unitPrice, unitsInStock, unitsOnOrder, reorderLevel, discontinued)` 값을 사용 하 여 데이터베이스에 새 제품을 삽입 전달 인; 반환 된 `ProductID` 새로 삽입된 된 레코드의 값
- `UpdateProduct(productName, supplierID, categoryID, quantityPerUnit, unitPrice, unitsInStock, unitsOnOrder, reorderLevel, discontinued, productID)` 전달 된 값을 사용 하 여 데이터베이스에서 기존 제품 업데이트 반환 `True` 행씩 정확 하 게 업데이트 된 경우 `False` 그렇지 않은 경우
- `DeleteProduct(productID)` 데이터베이스에서 지정된 된 제품 삭제

ProductsBLL.vb


[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample1.vb)]

단순히 데이터를 반환 하는 메서드가 `GetProducts`, `GetProductByProductID`를 `GetProductsByCategoryID`, 및 `GetProductBySuppliersID` 단순히를 호출 하므로 DAL에는 매우 간단 합니다. 일부 시나리오에서는 있을 구현 해야 하는 비즈니스 규칙 (예: 현재 로그온된 한 사용자 또는 사용자가 속해 있는 역할 기반 권한 부여 규칙)이 수준에서 단순히 보면 이러한 메서드-됩니다. 이러한 메서드의 그런 다음 BLL 단순히 프록시의 역할을 하는 프레젠테이션 계층 데이터 액세스 계층에서 기본 데이터에 액세스 합니다.

합니다 `AddProduct` 고 `UpdateProduct` 메서드 모두 매개 변수로 제품의 다양 한 필드의 값 및 새 제품을 추가 하거나 기존 각각 업데이트 합니다. 다양 한 이후 합니다 `Product` 테이블의 열을 사용할 수 있습니다 `NULL` 값 (`CategoryID`를 `SupplierID`, 및 `UnitPrice`, 등), 해당 입력에 대 한 매개 변수 `AddProduct` 및 `UpdateProduct` 사용할열에매핑되는[nullable 형식](https://msdn.microsoft.com/library/1t3y8s4s(v=vs.80).aspx)합니다. Nullable 형식에.NET 2.0 및 여부를 나타내는 여부를 값 형식, 대신에 기술을 제공 `Nothing`합니다. 참조를 [Paul Vick](http://www.panopticoncentral.net/)의 블로그 항목 [Nullable 형식에 대 한 The 사실 및 VB](http://www.panopticoncentral.net/archive/2004/06/04/1180.aspx) 기술 설명서와 합니다 [Nullable](https://msdn.microsoft.com/library/b3h38hb0%28VS.80%29.aspx) 구조에 대 한 자세한 내용은 합니다.

세 가지 방법을 모두 행 된 삽입, 업데이트 또는 삭제 작업이 영향을 받는 행을 얻을 수 없습니다 때문에 있는지 여부를 나타내는 부울 값을 반환 합니다. 예를 들어, 페이지 개발자 호출 하는 경우 `DeleteProduct` 전달를 `ProductID` 존재 하지 않는 제품에 대 한 합니다 `DELETE` 데이터베이스에 실행 된 문이 아무 영향도 주지 것입니다 있어를 `DeleteProduct` 메서드는 반환 `False`합니다.

새 제품을 추가할 때 또는 기존 업데이트에서는 변수로 새롭거나 수정 된 제품의 필드 값의 목록을 수락 하는 대신 스칼라를 `ProductsRow` 인스턴스. 때문에이 접근 방식을 선택 했습니다 합니다 `ProductsRow` ADO.NET에서 파생 되는 클래스 `DataRow` 클래스를 기본 매개 변수가 없는 생성자가 없습니다. 새 만들려면 `ProductsRow` 인스턴스를 먼저 만들어야 합니다를 `ProductsDataTable` 인스턴스 및 기능을 호출 해당 `NewProductRow()` 메서드 (에서 수행 하는 `AddProduct`). 이러한 단점 삽입 및 ObjectDataSource를 사용 하 여 제품 업데이트를 설정 하는 경우 견과류를 rears 합니다. 즉, ObjectDataSource 입력된 매개 변수의 인스턴스를 만들 하려고 합니다. BLL 메서드를 필요로 하는 경우는 `ProductsRow` 들어 ObjectDataSource 하려고 만든 하지만 기본 매개 변수가 없는 생성자의 부족으로 인해 실패 합니다. 이 문제에 대 한 자세한 내용은 다음 두 ASP.NET 포럼 게시물을 참조: [Strongly-Typed 데이터 집합을 사용 하 여 업데이트 ObjectDataSources](https://forums.asp.net/1098630/ShowPost.aspx), 및 [ObjectDataSource 사용 하 여 문제 및 Strongly-Typed 데이터 집합](https://forums.asp.net/1048212/ShowPost.aspx).

둘 다에서 다음 `AddProduct` 하 고 `UpdateProduct`, 코드를 만듭니다를 `ProductsRow` 인스턴스 하 고 바로 전달 되는 값으로 채웁니다. Datacolumns DataRow의 값을 할당할 때 다양 한 필드 수준 유효성 검사가 발생할 수 있습니다. 따라서 수동으로 DataRow에 전달 된 값을 다시 설치 하면 BLL 메서드에 전달 되는 데이터의 유효성을 검사 합니다. 그러나 Visual Studio에서 생성 된 강력한 형식의 DataRow 클래스는 nullable 형식 사용 하지 마세요. 대신 나타내는 DataRow의 특정 DataColumn 일치 해야 하는 `NULL` 데이터베이스 값을 사용 해야 합니다는 `SetColumnNameNull()` 메서드.

`UpdateProduct` 제품에 사용 하 여 업데이트를 먼저 로드 `GetProductByProductID(productID)`합니다. 이 데이터베이스에는 불필요 한 여정 처럼 보일 수 있지만,이 추가로 이동은 낙관적 동시성을 탐색 하는 이후 자습서에서 유용한 것입니다. 낙관적 동시성은 작업 하는 동시에 동일한 데이터에서 두 명의 사용자가 서로의 변경을 실수로 덮어쓰지는 확인 하는 기술입니다. 전체 레코드를 클릭 한 다음도 쉽게만 DataRow의 열 하위 집합을 수정 하는 BLL에 업데이트 메서드를 만듭니다. 탐색 하는 것은 `SuppliersBLL` 클래스는 예를 살펴보겠습니다.

마지막으로, 이때를 `ProductsBLL` 클래스에는 [DataObject 특성](https://msdn.microsoft.com/library/system.componentmodel.dataobjectattribute.aspx) 적용 (는 `[System.ComponentModel.DataObject]` 구문 파일의 위쪽 class 문 바로 앞) 메서드가 있고 [ DataObjectMethodAttribute 특성](https://msdn.microsoft.com/library/system.componentmodel.dataobjectmethodattribute.aspx)합니다. 합니다 `DataObject` 특성 클래스는 개체에 대 한 바인딩에 적합 한 것으로 표시를 [ObjectDataSource 컨트롤](https://msdn.microsoft.com/library/9a4kyhcx.aspx)반면는 `DataObjectMethodAttribute` 메서드의 용도 나타냅니다. 앞으로 살펴보겠지만 나중에 자습서에서 ASP.NET 2.0 ObjectDataSource 쉽게 클래스에서 데이터를 선언적으로 액세스할 수 있습니다. ObjectDataSource의 마법사에서 바인딩할 가능한 클래스 목록 필터링을 위해 기본적으로 표시 하는 클래스에만 `DataObjects` 마법사의 드롭다운 목록에 표시 됩니다. `ProductsBLL` 클래스는 이러한 특성이 없는 경우와 마찬가지로 작동 하지만 ObjectDataSource의 마법사에서 작업을 쉽게 추가 합니다.

## <a name="adding-the-other-classes"></a>다른 클래스를 추가합니다.

사용 하 여는 `ProductsBLL` 클래스 완료 해야 작업 범주, 공급 업체 및 직원을 위한 클래스를 추가 합니다. 시간을 내어 다음 클래스와 위의 예제에서 개념을 사용 하 여 메서드를 만듭니다.

- **CategoriesBLL.cs**

    - `GetCategories()`
    - `GetCategoryByCategoryID(categoryID)`
- **SuppliersBLL.cs**

    - `GetSuppliers()`
    - `GetSupplierBySupplierID(supplierID)`
    - `GetSuppliersByCountry(country)`
    - `UpdateSupplierAddress(supplierID, address, city, country)`
- **EmployeesBLL.cs**

    - `GetEmployees()`
    - `GetEmployeeByEmployeeID(employeeID)`
    - `GetEmployeesByManager(managerID)`

주목할 만한 한 가지 방법은 합니다 `SuppliersBLL` 클래스의 `UpdateSupplierAddress` 메서드. 이 메서드는 방금 공급자의 주소 정보를 업데이트 하는 것에 대 한 인터페이스를 제공 합니다. 이 메서드는 내부적으로 읽습니다 합니다 `SupplierDataRow` 지정 된 개체 `supplierID` (사용 하 여 `GetSupplierBySupplierID`), 주소 관련 속성을 설정 하 고 다음에 호출 합니다 `SupplierDataTable`의 `Update` 메서드. `UpdateSupplierAddress` 메서드 다음과 같습니다.


[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample2.vb)]

전체 구현은 클래스 BLL에 대 한이 기사의 다운로드를 참조 하십시오.

## <a name="step-2-accessing-the-typed-datasets-through-the-bll-classes"></a>2 단계: BLL 클래스를 통해 형식화 된 데이터 집합 액세스

첫 번째 자습서에 대 한 예제를 직접 입력 데이터 집합을 사용 하 여 프로그래밍 방식으로 살펴보았습니다 있지만 클래스 BLL 추가 하 여 프레젠테이션 계층을 사용할 BLL에 대해 대신 합니다. 에 `AllProducts.aspx` 첫 번째 자습서의 예제는 `ProductsTableAdapter` 다음 코드에 표시 된 대로 제품 목록의 GridView에 바인딩하는 데 사용 되었습니다:


[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample3.vb)]

새 BLL을 사용 하도록 변경 해야 하는 모든 클래스는 코드의 첫 번째 줄 바꾸기만 합니다 `ProductsTableAdapter` 개체를 `ProductBLL` 개체:


[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample4.vb)]

ObjectDataSource를 사용 하 여 클래스 BLL를 선언적 (입력 데이터 집합 수)으로 액세스할 수도 있습니다. 살펴보겠습니다. 자세히 ObjectDataSource를 다음 자습서에서입니다.


[![제품 목록 GridView에 표시 됩니다.](creating-a-business-logic-layer-vb/_static/image4.png)](creating-a-business-logic-layer-vb/_static/image3.png)

**그림 3**: GridView에는 제품 목록 표시 됩니다 ([큰 이미지를 보려면 클릭](creating-a-business-logic-layer-vb/_static/image5.png))


## <a name="step-3-adding-field-level-validation-to-the-datarow-classes"></a>DataRow 클래스에 필드 수준 유효성 검사를 추가 하는 3 단계:

필드 수준 유효성 검사를 삽입 하거나 업데이트할 때 비즈니스 개체의 속성 값에 관련 된 검사 제품에 대 한 몇 가지 필드 수준 유효성 검사 규칙은 다음과 같습니다.

- `ProductName` 필드는 40 자 이하의 해야 합니다.
- `QuantityPerUnit` 20 자 또는 길이가 필드 여야 합니다
- 합니다 `ProductID`하십시오 `ProductName`, 및 `Discontinued` 필드는 필요 하지만 다른 모든 필드는 선택 사항
- 합니다 `UnitPrice`, `UnitsInStock`를 `UnitsOnOrder`, 및 `ReorderLevel` 필드는 0 보다 크거나 해야 합니다.

이러한 규칙을 데이터베이스 수준에서 표현 되어야 합니다. 문자 제한에는 `ProductName` 하 고 `QuantityPerUnit` 필드에 있는 해당 열의 데이터 형식에 의해 캡처되는 `Products` 테이블 (`nvarchar(40)` 및 `nvarchar(20)`각각). 데이터베이스 테이블 열에서 허용 하는 경우 여 표현 됩니다 필수 및 선택적 필드 되는지 `NULL` s입니다. 네 [check 제약 조건](https://msdn.microsoft.com/library/ms188258.aspx) 존재만 값 0 보다 크거나 같은 경우에 수행할 수 있는지를 확인 하는 합니다 `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`, 또는 `ReorderLevel` 열입니다.

데이터베이스에서 이러한 규칙을 적용 하는 것 외에도 이러한도 적용할 데이터 집합 수준에 있습니다. 사실, 필드 길이 및 값이 필수 또는 선택적인 이미 각 데이터 테이블의 DataColumns 집합에 대 한 캡처됩니다. 자동으로 제공 하는 기존 필드 수준 유효성 검사를 확인 하려면 디자이너로 이동 하 여 데이터 집합, 하나는 Datatable에서 필드를 선택 하 고 속성 창에 이동 합니다. 그림 4에서 알 수 있듯이, 합니다 `QuantityPerUnit` DataColumn의 합니다 `ProductsDataTable` 최대 길이가 20 자가 고 허용 않는 `NULL` 값. 설정 하려고 하는 경우는 `ProductsDataRow`의 `QuantityPerUnit` 20 자 보다 긴 문자열 값으로 속성을 `ArgumentException` throw 됩니다.


[![DataColumn 기본 필드 수준 유효성 검사를 제공합니다.](creating-a-business-logic-layer-vb/_static/image7.png)](creating-a-business-logic-layer-vb/_static/image6.png)

**그림 4**: The DataColumn 제공 기본 필드 수준 유효성 검사 ([큰 이미지를 보려면 클릭](creating-a-business-logic-layer-vb/_static/image8.png))


안타깝게도 없습니다 지정 범위 검사와 같은 `UnitPrice` 속성 창을 통해 0 보다 크거나 값 이어야 합니다. 이 형식의 필드 수준 유효성 검사를 제공 하기 위해 DataTable의에 대 한 이벤트 처리기를 생성 해야 [ColumnChanging](https://msdn.microsoft.com/library/system.data.datatable.columnchanging%28VS.80%29.aspx) 이벤트입니다. 에 설명 된 대로 합니다 [이전 자습서](creating-a-data-access-layer-vb.md), partial 클래스를 사용 하 여 입력 데이터 집합에서 만든 데이터 집합, Datatable 및 DataRow 개체를 확장할 수 있습니다. 만들 수 있습니다이 기술을 사용 하는 `ColumnChanging` 에 대 한 이벤트 처리기는 `ProductsDataTable` 클래스입니다. 클래스를 만들어 시작 합니다 `App_Code` 라는 폴더 `ProductsDataTable.ColumnChanging.vb`합니다.


[![App_Code 폴더에 새 클래스를 추가 합니다.](creating-a-business-logic-layer-vb/_static/image10.png)](creating-a-business-logic-layer-vb/_static/image9.png)

**그림 5**: 새 클래스를 추가 합니다 `App_Code` 폴더 ([클릭 하 여 큰 이미지 보기](creating-a-business-logic-layer-vb/_static/image11.png))


다음에 대 한 이벤트 처리기를 만듭니다는 `ColumnChanging` 되도록 하는 이벤트를 `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`, 및 `ReorderLevel` 열 값 (그렇지 않은 경우 `NULL`)는 0 보다 크거나 같은 경우. 이러한 열이 범위를 벗어나는 경우 throw는 `ArgumentException`합니다.

ProductsDataTable.ColumnChanging.vb


[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample5.vb)]

## <a name="step-4-adding-custom-business-rules-to-the-blls-classes"></a>4 단계: 클래스 BLL의 사용자 지정 비즈니스 규칙 추가

필드 수준 유효성 검사 외에도 같은 다른 엔터티 또는 단일 열 수준에서 개념을 표현할 수 없습니다를 포함 하는 높은 수준의 사용자 지정 비즈니스 규칙이 있을 수 있습니다.

- 제품이 단종 된 경우 해당 `UnitPrice` 업데이트할 수 없습니다.
- 직원의 거주 국가를 해당 관리자의 거주 국가와 동일 해야
- 제품은 제품만 공급자가 제공 하는 경우 중단 될 수 없습니다.

클래스 BLL 하 여 응용 프로그램의 비즈니스 규칙을 준수 검사를 포함 해야 합니다. 이러한 검사를 적용 하는 메서드를 추가할 수 있습니다.

비즈니스 규칙에는 제품을 표시할 수 없습니다 지원 되지 않는 지정 된 공급자 로부터 제품만 되었으면 받아쓰기는 한다고 가정 합니다. 그러나 즉, 경우 제품 *X* 공급 업체에서 구매한 것만 제품 이었습니다 *Y*, 표시할 수 없습니다 것 *X* 지원 되지 않는; 경우 처럼 공급자 *Y*세 가지 제품과 함께 제공 하는 미국 *A*, *B*, 및 *C*, 그런 다음 모든 표시 수 및 중단으로 이러한 모든 합니다. 항상 홀수 비즈니스 규칙을 있지만 비즈니스 규칙 및 상식적인 정렬 되지 않습니다!

이 비즈니스 규칙을 적용 하는 `UpdateProducts` 메서드를 확인 하 여 시작 했습니다 `Discontinued` 로 설정 된 `True` 따라서 호출 하는 경우 `GetProductsBySupplierID` 에서는이 제품의 공급이 업체에서 구매한 제품 수를 결정 하 합니다. 경우에이 공급 업체에서 구매한 제품 하나를 두어는 `ApplicationException`합니다.


[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample6.vb)]

## <a name="responding-to-validation-errors-in-the-presentation-tier"></a>프레젠테이션 계층에서 유효성 검사 오류에 응답

프레젠테이션 계층에서 BLL을 호출할 때 발생할 수 있습니다 또는 ASP.NET 버블링 수 있도록 하는 모든 예외를 처리할 것인지를 결정할 수 있습니다 (발생 시키고 합니다 `HttpApplication`의 `Error` 이벤트). BLL을 사용 하 여 프로그래밍 방식으로 작업 하는 경우 예외를 처리를 사용할 수 있습니다는 [시도 하는 중... Catch](https://msdn.microsoft.com/library/fk6t46tz%28VS.80%29.aspx) 다음 예와 같이 블록:


[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample7.vb)]

나중에 자습서 살펴보겠습니다, 데이터를 사용 하는 경우 BLL에서 버블 업 예외 처리 웹 컨트롤 삽입, 업데이트 또는 코드에서 줄 바꿈 하는 대신 이벤트 처리기에서 직접 데이터 삭제를 처리할 수 있습니다 `Try...Catch` 블록.

## <a name="summary"></a>요약

잘 설계 된 응용 프로그램을 특정 역할을 캡슐화 하는 각 고유 레이어로 생성 됩니다. 이 문서 시리즈의 첫 번째 자습서에서 형식화 된 데이터 집합;를 사용 하 여 데이터 액세스 계층을 만들었습니다. 이 자습서에서는 기본 제공 비즈니스 논리 레이어 일련의 클래스 응용 프로그램의 `App_Code` 는 DAL을 호출 하는 폴더입니다. BLL에 응용 프로그램에 대 한 필드 수준과 비즈니스 수준의 논리를 구현 합니다. 별도 BLL을 만드는 것 외에이 자습서에서 수행한 것 처럼 다른 옵션으로 partial 클래스를 사용 하 여 Tableadapter의 메서드를 확장 합니다. 그러나이 방법을 사용할 수 없도록 기존 메서드를 재정의 하 되 지도 않습니다 하는 DAL 및 분리는 BLL이 문서의 살펴보았으며 접근 방식으로 완전히.

DAL 및 완료 하는 BLL을 사용 하 여 준비가 프레젠테이션 계층에서 시작 합니다. 에 [다음 자습서](master-pages-and-site-navigation-vb.md) 에서는 데이터 액세스 항목에서 간단한 우회를 수행 하 고이 자습서 전체에서 사용에 대 한 일관 된 페이지 레이아웃을 정의 합니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Liz Shulok, Dennis Patterson, Carlos Santos 및 Hilton giesenow가 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](creating-a-data-access-layer-vb.md)
> [다음](master-pages-and-site-navigation-vb.md)
