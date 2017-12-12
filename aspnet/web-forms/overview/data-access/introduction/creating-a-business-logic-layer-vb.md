---
uid: web-forms/overview/data-access/introduction/creating-a-business-logic-layer-vb
title: "비즈니스 논리 계층 (VB) 만들기 | Microsoft Docs"
author: rick-anderson
description: "이 자습서에는 비즈니스 논리 BLL (계층) 교량 t 간에 데이터를 교환에 대 한 역할을 하는 비즈니스 규칙에 중앙 집중화 하는 방법을 살펴보겠습니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 142e5181-29ce-4bb9-907b-2a0becf7928b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/introduction/creating-a-business-logic-layer-vb
msc.type: authoredcontent
ms.openlocfilehash: 7722ed54e333515f641f1c1adf647c4ec08dfb6b
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="creating-a-business-logic-layer-vb"></a>비즈니스 논리 계층 (VB) 만들기
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_2_VB.exe) 또는 [PDF 다운로드](creating-a-business-logic-layer-vb/_static/datatutorial02vb1.pdf)

> 이 자습서에는 비즈니스 논리 BLL (계층) 프레젠테이션 계층 및 DAL 간의 데이터 교환 위한 중간자로 사용할 비즈니스 규칙에 중앙 집중화 하는 방법을 살펴보겠습니다.


## <a name="introduction"></a>소개

(DAL (데이터 액세스 계층)에서 만든는 [첫 번째 자습서](creating-a-data-access-layer-vb.md) 프레젠테이션 논리에서 논리를 액세스 하는 데이터 명확 하 게 구분 합니다. 그러나 DAL 프레젠테이션 계층과에서 데이터 액세스 정보를 명확 하 게 구분을 하는 동안 고려해 야 하는 모든 비즈니스 규칙 적용 하지 않습니다. 예를 들어 응용 프로그램에 대 한 것이 좋겠습니다 disallow는 `CategoryID` 또는 `SupplierID` 의 필드는 `Products` 수정할 때 테이블의 `Discontinued` 필드를 1로 설정 하거나 म 수 이라는 규칙을 적용 하는 상황을 방지는 직원은 다음 고용 된 사람에 의해 관리 됩니다. 다른 일반적인 시나리오는 특정 역할에 사용자를 아마도 권한 부여 제품 삭제 하거나 변경할 수는 `UnitPrice` 값입니다.

이 자습서에서는 이러한 비즈니스 규칙에는 비즈니스 논리 BLL (계층) 프레젠테이션 계층 및 DAL 간의 데이터 교환 위한 중간자로 사용할 중앙 집중화 하는 방법을 살펴보겠습니다. 실제 응용 프로그램에서 별도 클래스 라이브러리 프로젝트로; BLL은 구현 그러나이 자습서에 대 한 구현 BLL 일련의 클래스의 우리의 `App_Code` 프로젝트 구조를 단순화 하기 위해 폴더입니다. 그림 1 프레젠테이션 계층, BLL, 및 DAL 아키텍처 관계를 보여 줍니다.


![BLL은 데이터 액세스 계층에서 프레젠테이션 계층을 분리 하 고 비즈니스 규칙 적용](creating-a-business-logic-layer-vb/_static/image1.png)

**그림 1**: BLL 데이터 액세스 계층에서 프레젠테이션 계층을 분리 하 고 비즈니스 규칙 적용


구현 하는 별도 클래스를 만드는 대신 우리의 [비즈니스 논리](http://en.wikipedia.org/wiki/Business_logic), partial 클래스와 형식화 된 데이터 집합에서 직접이 논리 또는 배치할 수 있습니다. 만들기 및 형식화 된 데이터 집합을 확장의 예로에 대 한 첫 번째 자습서로 다시 참조 합니다.

## <a name="step-1-creating-the-bll-classes"></a>1 단계: BLL 클래스 만들기

DAL;에서 각 TableAdapter에 대해 하나씩 네 개의 클래스 우리의 BLL 구성 됩니다. 각 BLL 클래스는 검색, 삽입, 업데이트 및 적절 한 비즈니스 규칙을 적용 하는 DAL에서 해당 TableAdapter에서 삭제 하기 위한 메서드를 갖습니다.

두 개의 하위 폴더를 만들어 보겠습니다을 보다 명확 하 게 하려면 DAL 및 BLL 관련 클래스를 구분는 `App_Code` 폴더 `DAL` 및 `BLL`합니다. 오른쪽 단추로 클릭 하면는 `App_Code` 솔루션 탐색기에서 폴더를 새 폴더를 선택 합니다. 다음과 같은 두 폴더를 만든 후에 첫 번째 자습서에서 만든 형식화 된 데이터 집합을 이동는 `DAL` 하위 폴더입니다.

다음으로 4 개의 BLL 클래스 파일을 만듭니다는 `BLL` 하위 폴더입니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭는 `BLL` 하위 폴더를 새 항목 추가 선택 하 고 클래스 템플릿을 선택 합니다. 4 개 클래스의 이름을 `ProductsBLL`, `CategoriesBLL`, `SuppliersBLL`, 및 `EmployeesBLL`합니다.


![App_Code 폴더에 4 개의 새 클래스 추가](creating-a-business-logic-layer-vb/_static/image2.png)

**그림 2**: 4 개의 새 클래스를 추가 `App_Code` 폴더


다음으로, 단순히 첫 번째 자습서에서 Tableadapter에 대해 정의 된 메서드를 래핑하는 클래스의 각 메서드를 추가 해 보겠습니다. 이제 이러한 메서드는 호출 하 게 직접 DAL; 필요한 비즈니스 논리를 추가 하려면 이상 반환 합니다.

> [!NOTE]
> Visual Studio Standard Edition을 사용 하는 이상 (본인이 즉, *하지* Visual Web Developer를 사용 하 여)을 시각적으로 사용 하 여 클래스를 선택적으로 디자인할 수 있습니다는 [클래스 디자이너](https://msdn.microsoft.com/library/default.asp?url=/library/en-us/dv_vstechart/html/clssdsgnr.asp)합니다. 참조는 [클래스 디자이너 블로그](https://blogs.msdn.com/classdesigner/default.aspx) Visual Studio에서이 새로운 기능에 대 한 자세한 내용은 합니다.


에 대 한는 `ProductsBLL` 클래스는 총 7 개의 메서드를 추가 해야 합니다.

- `GetProducts()`모든 제품을 반환합니다.
- `GetProductByProductID(productID)`지정 된 제품 ID로 곱을 반환합니다.
- `GetProductsByCategoryID(categoryID)`지정 된 범주에 속한 모든 제품을 반환합니다.
- `GetProductsBySupplier(supplierID)`지정 된 공급자 로부터 모든 제품을 반환합니다.
- `AddProduct(productName, supplierID, categoryID, quantityPerUnit, unitPrice, unitsInStock, unitsOnOrder, reorderLevel, discontinued)`값을 사용 하 여 데이터베이스에 새 제품을 삽입 전달 인; 반환 된 `ProductID` 새로 삽입된 된 레코드의 값
- `UpdateProduct(productName, supplierID, categoryID, quantityPerUnit, unitPrice, unitsInStock, unitsOnOrder, reorderLevel, discontinued, productID)`전달 된 값을 사용 하 여 데이터베이스에서 기존 제품 업데이트 반환 `True` 정확 하 게 하나의 행을 업데이트 하는 경우 `False` 그렇지 않은 경우
- `DeleteProduct(productID)`데이터베이스에서 지정된 된 제품을 삭제합니다.

ProductsBLL.vb


[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample1.vb)]

단순히 데이터를 반환 하는 메서드가 `GetProducts`, `GetProductByProductID`, `GetProductsByCategoryID`, 및 `GetProductBySuppliersID` 은 단순히 호출 DAL에는 매우 간단 합니다. 일부 시나리오에서 있습니다 수 있지만 구현 되어야 하는 비즈니스 규칙 (예: 현재 로그온된 한 사용자 또는 사용자가 속한 역할 기반 권한 부여 규칙)이이 수준에서 단순히 두겠습니다 이러한 방법으로-됩니다. 이러한 방법에 대 한 다음, BLL 프록시로 사용 되어 단순히는는 프레젠테이션 계층 데이터 액세스 계층에서 기본 데이터에 액세스 합니다.

`AddProduct` 및 `UpdateProduct` 메서드 둘 다 매개 변수로 다양 한 제품 필드에 대 한 값 및 새 제품을 추가 하거나 기존을 각각 업데이트 합니다. 다양 한 이후는 `Product` 테이블의 열을 사용할 수 `NULL` 값 (`CategoryID`, `SupplierID`, 및 `UnitPrice`, 등), 이러한 입력 매개 변수를 `AddProduct` 및 `UpdateProduct` 이러한 열 사용 매핑되[nullable 형식](https://msdn.microsoft.com/en-us/library/1t3y8s4s(v=vs.80).aspx)합니다. Nullable 형식은.NET 2.0에 새로 고 여야 하는지 여부를 값 형식 해야 대신 나타내는 기술을 제공 `Nothing`합니다. 참조는 [Paul Vick](http://www.panopticoncentral.net/)의 블로그 항목 [Nullable 형식에 대 한 The 진위 여부 및 VB](http://www.panopticoncentral.net/archive/2004/06/04/1180.aspx) 및에 대 한 기술 문서는 [Nullable](https://msdn.microsoft.com/en-US/library/b3h38hb0%28VS.80%29.aspx) 구조에 대 한 자세한 내용은 합니다.

세 가지 방법이 모두 행 된 삽입, 업데이트 또는 영향을 받는 행의 작업을 발생 하지 않을 수 있으므로 삭제 여부를 나타내는 부울 값을 반환 합니다. 예를 들어, 페이지 개발자 호출 하는 경우 `DeleteProduct` 전달는 `ProductID` 존재 하지 않는 제품에 대 한는 `DELETE` 데이터베이스에 실행 된 문이 아무 영향도 주지 것입니다 따라서 및는 `DeleteProduct` 메서드는 반환 `False`합니다.

새 제품을 추가 하는 경우 or는 기존 업데이트를 수행 새롭거나 수정 된 제품의 필드 값의 스칼라 수락 하는 대신 목록으로는 `ProductsRow` 인스턴스. 이 방법은 때문에 선택 되었습니다는 `ProductsRow` ADO.NET에서 클래스 파생 `DataRow` 클래스를 기본 매개 변수가 없는 생성자가 없습니다. 새을 만들기 위해 `ProductsRow` 먼저 만들어야 인스턴스를 한 `ProductsDataTable` 인스턴스 한 다음 해당 `NewProductRow()` 메서드 (에서 일 하 `AddProduct`). 이러한 단점 삽입 하 고는 ObjectDataSource를 사용 하 여 제품 업데이트를 설정 하는 경우 해당 h e a d rears 합니다. 즉, ObjectDataSource는 입력된 매개 변수의 인스턴스를 만들려고 시도 합니다. BLL 메서드에서 예상 하는 경우는 `ProductsRow` 인스턴스가는 ObjectDataSource을 만들 되, 기본 매개 변수가 없는 생성자가 없기 때문에 실패 시도 합니다. 이 문제에 대 한 자세한 내용은 다음 두 개의 ASP.NET 포럼 게시물을 참조 하십시오: [Strongly-Typed 데이터 집합과 업데이트 ObjectDataSources](https://forums.asp.net/1098630/ShowPost.aspx), 및 [문제가 있는 ObjectDataSource 및 Strongly-Typed DataSet](https://forums.asp.net/1048212/ShowPost.aspx).

둘 다에서 다음 `AddProduct` 및 `UpdateProduct`, 코드 만듭니다는 `ProductsRow` 인스턴스를 방금 전달 된 값으로 채웁니다. DataRow의 DataColumns에 값을 지정 하는 경우 필드 수준 유효성 검사를 다양 한 발생할 수 있습니다. 따라서 수동으로 DataRow에 전달 된 값을 다시 설치 하면 BLL 메서드에 전달 되는 데이터의 유효성을 검사 합니다. 그러나 Visual Studio에서 생성 된 강력한 형식의 DataRow 클래스 nullable 형식을 사용 하지 마십시오. 대신, DataRow의 특정 DataColumn에 대응 되어야 나타내기 위해는 `NULL` 데이터베이스 사용 해야 하는 값은 `SetColumnNameNull()` 메서드.

`UpdateProduct` 를 사용 하 여 업데이트 제품에 먼저 로드 `GetProductByProductID(productID)`합니다. 이 데이터베이스에는 불필요 한 이동 처럼 보일 수 있지만,이 추가로 이동은 낙관적 동시성을 탐색 하는 이후 자습서에 것입니다. 낙관적 동시성은 작업 하는 동시에 동일한 데이터에서 두 사용자가 다른의 변경 내용을 덮어쓸 실수로 하지 확인 하는 기법입니다. 전체 레코드를 클릭 한 다음도 쉽게 수만 데이터 행의 열 하위 집합을 수정 하는 BLL에 update 메서드를 만듭니다. 탐색 우리는 `SuppliersBLL` 클래스 예제를 살펴보겠습니다.

마지막으로, 유의 `ProductsBLL` 클래스에는 [DataObject 특성](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataobjectattribute.aspx) 적용 (의 `[System.ComponentModel.DataObject]` 파일의 맨 위 근처에 class 문 바로 앞에 구문) 메서드가 있고 [ DataObjectMethodAttribute 특성](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataobjectmethodattribute.aspx)합니다. `DataObject` 특성 클래스는 개체에 대 한 바인딩에 적합 한 것으로 표시 된 [ObjectDataSource 컨트롤](https://msdn.microsoft.com/en-us/library/9a4kyhcx.aspx)반면는 `DataObjectMethodAttribute` 메서드의 용도 나타냅니다. 자습서 나중에 볼 수 있겠지만, ASP.NET 2.0 ObjectDataSource 쉽게 선언적으로 클래스에서 데이터에 액세스할 수 있습니다. ObjectDataSource의 마법사에서 바인딩할 가능한 클래스 목록 필터링을 위해 기본적으로 표시 된 클래스만 `DataObjects` 마법사의 드롭다운 목록에 표시 됩니다. `ProductsBLL` 클래스와 마찬가지로 이러한 특성이 없는 작동 하지만 ObjectDataSource의 마법사에서 사용 하기 쉽게에 추가 합니다.

## <a name="adding-the-other-classes"></a>다른 클래스를 추가합니다.

와 `ProductsBLL` 클래스 완료 해야 작업 범주, 공급 업체 및 직원을 위한 클래스를 추가 합니다. 다음 클래스 및 메서드를 위 예제의 개념을 사용 하 여 만들 보십시오.

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

주목할 한 가지 방법은 `SuppliersBLL` 클래스의 `UpdateSupplierAddress` 메서드. 이 메서드는 방금 공급 업체의 주소 정보를 업데이트 하기 위한 인터페이스를 제공 합니다. 이 메서드를 내부적으로 읽습니다는 `SupplierDataRow` 지정 된 개체 `supplierID` (사용 하 여 `GetSupplierBySupplierID`), 주소 관련 속성을 설정 하 고 다음 호출는 `SupplierDataTable`의 `Update` 메서드. `UpdateSupplierAddress` 메서드 다음과:


[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample2.vb)]

내 전체 BLL 클래스 구현에 대 한이 다운로드가이 문서를 참조 하십시오.

## <a name="step-2-accessing-the-typed-datasets-through-the-bll-classes"></a>2 단계: BLL 클래스를 통해 형식화 된 데이터 집합 액세스

프로그래밍 방식, 형식화 된 데이터 집합으로 직접 작업의 예는 첫 번째 자습서에서 살펴본 하지만 BLL 클래스를 추가 프레젠테이션 계층 해야 작동 BLL에 대해 대신 합니다. `AllProducts.aspx` 첫 번째 자습서에서 예제는 `ProductsTableAdapter` 다음 코드에 나와 있는 것 처럼 제품 목록이 GridView에 바인딩하는 데 사용 되었습니다.


[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample3.vb)]

새 BLL를 사용 하려면 변경 해야 하는 모든 클래스는 코드의 첫 번째 줄을 바꾸면는 `ProductsTableAdapter` 개체는 `ProductBLL` 개체:


[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample4.vb)]

BLL 클래스는 ObjectDataSource를 사용 하 여 선언적 (형식화 된 데이터 집합 수)으로 액세스할 수도 있습니다. 다룰 것 자세히 ObjectDataSource에서 다음과 같은 자습서입니다.


[![제품 목록은 GridView에 표시 됩니다.](creating-a-business-logic-layer-vb/_static/image4.png)](creating-a-business-logic-layer-vb/_static/image3.png)

**그림 3**:는 GridView에 제품의 목록이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-a-business-logic-layer-vb/_static/image5.png))


## <a name="step-3-adding-field-level-validation-to-the-datarow-classes"></a>3 단계: DataRow 클래스에 필드 수준 유효성 검사 추가

필드 수준 유효성 검사는 삽입 하거나 업데이트할 때 비즈니스 개체의 속성 값에 관련 된 검사 합니다. 제품에 대 한 일부 필드 수준 유효성 검사 규칙은 다음과 같습니다.

- `ProductName` 40 자 이하의 필드 여야 합니다
- `QuantityPerUnit` 20 자 이하의 필드 여야 합니다
- `ProductID`, `ProductName`, 및 `Discontinued` 필드는 필요 하지만 다른 모든 필드는 선택 사항
- `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`, 및 `ReorderLevel` 필드는 0 보다 크거나 이어야 합니다

이러한 규칙 수 및 데이터베이스 수준에서 표시 해야 합니다. 문자 제한에는 `ProductName` 및 `QuantityPerUnit` 필드에 있는 해당 열의 데이터 형식에서 캡처되는 `Products` 테이블 (`nvarchar(40)` 및 `nvarchar(20)`각각). 데이터베이스 테이블 열에서 허용 하는 경우 하 여 표현 됩니다 필수 및 선택적 필드 인지 `NULL` s입니다. 4 개의 [check 제약 조건](https://msdn.microsoft.com/en-us/library/ms188258.aspx) 존재만 값이 0 보다 크거나 같은 경우에 사용할 수 있는지 확인 하는 `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`, 또는 `ReorderLevel` 열입니다.

데이터베이스에서 이러한 규칙을 적용 하는 것 외에도 이러한 해야 적용 될 데이터 집합 수준. 사실, 필드 길이 및 값이 필수 또는 선택적인 이미 DataColumns의 각 데이터 테이블 집합에 대 한 캡처. 자동으로 제공 하는 기존 필드 수준 유효성 검사를 보려면 데이터 집합 디자이너로 이동 하는 Datatable 중 하나에서 필드를 선택 하 고 속성 창으로 이동 하 여 합니다. 그림 4에서 볼 수 있듯이 `QuantityPerUnit` DataColumn에는 `ProductsDataTable` 최대 길이는 20 자가 고 허용 않는 `NULL` 값입니다. 설정 하려고 하면는 `ProductsDataRow`의 `QuantityPerUnit` 속성을 문자열 값을 20 자 보다 긴는 `ArgumentException` throw 됩니다.


[![DataColumn 기본 필드 수준 유효성 검사를 제공합니다.](creating-a-business-logic-layer-vb/_static/image7.png)](creating-a-business-logic-layer-vb/_static/image6.png)

**그림 4**: The DataColumn 제공 기본 필드 수준 유효성 검사 ([전체 크기 이미지를 보려면 클릭](creating-a-business-logic-layer-vb/_static/image8.png))


그러나 우리 지정할 수 없습니다 범위 검사와 같은 `UnitPrice` 속성 창을 통해 0 보다 크거나 값 이어야 합니다. 이 형식의 필드 수준 유효성 검사를 제공 하기 위해 DataTable의에 대 한 이벤트 처리기를 만들고 해야 [ColumnChanging](https://msdn.microsoft.com/en-us/library/system.data.datatable.columnchanging%28VS.80%29.aspx) 이벤트입니다. 설명한 것 처럼는 [이전 자습서](creating-a-data-access-layer-vb.md), partial 클래스를 사용 하 여 입력 데이터 집합에서 생성 된 DataSet, Datatable 및 DataRow 개체를 확장할 수 있습니다. 만들 수 있습니다이 기술을 사용 하는 `ColumnChanging` 에 대 한 이벤트 처리기는 `ProductsDataTable` 클래스입니다. 클래스를 만들어 시작는 `App_Code` 라는 폴더 `ProductsDataTable.ColumnChanging.vb`합니다.


[![App_Code 폴더에 새 클래스를 추가 합니다.](creating-a-business-logic-layer-vb/_static/image10.png)](creating-a-business-logic-layer-vb/_static/image9.png)

**그림 5**:에 새 클래스 추가 `App_Code` 폴더 ([전체 크기 이미지를 보려면 클릭](creating-a-business-logic-layer-vb/_static/image11.png))


에 대 한 이벤트 처리기를 다음으로 만듭니다는 `ColumnChanging` 되도록 이벤트는 `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`, 및 `ReorderLevel` 열 값 (그렇지 않은 경우 `NULL`) 보다 크거나 0입니다. 이러한 열이 범위를 벗어나는 경우 throw는 `ArgumentException`합니다.

ProductsDataTable.ColumnChanging.vb


[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample5.vb)]

## <a name="step-4-adding-custom-business-rules-to-the-blls-classes"></a>4 단계: BLL의 클래스에 사용자 지정 비즈니스 규칙 추가

필드 수준 유효성 검사 외에도 같은 서로 다른 엔터티 또는 단일 열 수준에서 개념을 표현할 수 없습니다와 관련 된 높은 수준의 사용자 지정 비즈니스 규칙 있을 수 있습니다.

- 제품의 사용이 중지 되는 경우 해당 `UnitPrice` 업데이트할 수 없습니다.
- 직원의 거주 아니어야 거주 관리자의 국가와 동일
- 유일한 제품 공급 업체에서 제공 하는 경우 제품을 중단 될 수 없습니다.

BLL 클래스 하 여 응용 프로그램의 비즈니스 규칙을 준수 검사를 포함 해야 합니다. 이러한 검사가 적용 되는 메서드를 직접 추가할 수 있습니다.

우리의 비즈니스 규칙에는 제품을 표시할 수 없습니다 지원 되지 않는 특정된 공급 업체에서 유일한 제품 되었으면 지정는 한다고 가정 합니다. 그러나 즉, 하는 경우 제품 *X* 유일한 제품 공급 업체에서 구입한 म *Y*, 우리 표시할 수 없습니다. *X* 중단할; 경우, 대로 공급 업체 *Y*우리 세 개의 제품과 함께 제공 *A*, *B*, 및 *C*, 다음 모든 표시할 수 있습니다 및이 방법으로 모든 사용이 중지 합니다. 비즈니스 규칙과 어떻게 작동 하지만 홀수 비즈니스 규칙을 항상 정렬 되지 않습니다!

이 비즈니스 규칙을 적용 하는 `UpdateProducts` 확인 하 여 먼저 메서드 `Discontinued` 로 설정 된 `True` 및 것 이라고, `GetProductsBySupplierID` म이 제품의 공급이 업체에서 구매한 제품 수를 확인 하려면. 경우에이 공급 업체에서 구매한 한 제품을 두어는 `ApplicationException`합니다.


[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample6.vb)]

## <a name="responding-to-validation-errors-in-the-presentation-tier"></a>프레젠테이션 계층에서 유효성 검사 오류에 응답

프레젠테이션 계층에서 BLL를 호출 하는 경우에 발생할 수 있습니다 또는 ASP.NET 전달 되도록 허용 하는 모든 예외를 처리 하도록 시도할 것인지를 결정할 수 있습니다 (발생 시키고는 `HttpApplication`의 `Error` 이벤트). 사용할 수 BLL를 프로그래밍 방식으로 작업할 때 예외를 처리 하는 [시도 중... Catch](https://msdn.microsoft.com/en-us/library/fk6t46tz%28VS.80%29.aspx) 다음 예제와 같이 블록:


[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample7.vb)]

: 자습서 나중에 볼 수 있겠지만, 데이터를 사용 하는 경우 BLL에서 버블 업 하는 예외 처리 웹 컨트롤 삽입, 업데이트 또는 이벤트 처리기에 코드를 래핑하는 대신에서 직접 데이터 삭제를 처리할 수 있습니다 `Try...Catch` 블록입니다.

## <a name="summary"></a>요약

특정 역할을 캡슐화 하는 각각 별도 계층에는 잘 설계 된 응용 프로그램 트 됩니다. 이 문서 시리즈의 첫 번째 자습서에서 만든 형식화 된 데이터 집합;를 사용 하 여 데이터 액세스 계층 이 자습서에서는 비즈니스 논리 계층으로 작성 일련의 클래스를이 응용 프로그램에서 `App_Code` 우리의 DAL로 호출 하는 폴더입니다. BLL 응용 프로그램에 대 한 필드 수준과 수준 비즈니스 논리를 구현합니다. 별도 BLL를 만들 뿐만 아니라이 자습서에서와 같이 또 다른 옵션은 partial 클래스를 사용 하 여 Tableadapter의 메서드를 확장 합니다. 그러나이 방법을 사용 하지 못하도록 기존 메서드를 재정의할 수 없으며 않습니다 것 분리 하는 DAL 우리의 BLL म 수행 하는 데이 문서의 접근 방식을 완전히 합니다.

DAL 및 BLL 완료를 준비가 우리의 프레젠테이션 계층에서 시작 합니다. 에 [다음 자습서](master-pages-and-site-navigation-vb.md) 알아보고이 자습서에서 사용할 수 있도록 일관 된 페이지 레이아웃을 정의할 데이터 액세스 항목에서 간단한 우회를 수행 하겠습니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Liz Shulok, Dennis Patterson, Carlos Santos 및 Hilton Giesenow 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](creating-a-data-access-layer-vb.md)
[다음](master-pages-and-site-navigation-vb.md)
