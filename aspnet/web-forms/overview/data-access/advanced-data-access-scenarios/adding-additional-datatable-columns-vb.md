---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/adding-additional-datatable-columns-vb
title: 추가 DataTable 열 (VB) 추가 | Microsoft Docs
author: rick-anderson
description: TableAdapter 마법사를 사용 하 여 형식화 된 데이터 집합을 만들를 해당 DataTable 기본 데이터베이스 쿼리에서 반환 되는 열을 포함 합니다. 하지만 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/18/2007
ms.topic: article
ms.assetid: 1e8e65f9-fe3e-4250-810b-c90227786bed
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/adding-additional-datatable-columns-vb
msc.type: authoredcontent
ms.openlocfilehash: b51089057ad1e14901cb09589534d6e575261c3e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="adding-additional-datatable-columns-vb"></a>추가 DataTable 열 (VB)를 추가합니다.
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_70_VB.zip) 또는 [PDF 다운로드](adding-additional-datatable-columns-vb/_static/datatutorial70vb1.pdf)

> TableAdapter 마법사를 사용 하 여 형식화 된 데이터 집합을 만들를 해당 DataTable 기본 데이터베이스 쿼리에서 반환 되는 열을 포함 합니다. 하지만 추가 열을 포함 하는 DataTable을 필요로 하는 경우 경우가 있습니다. 이 자습서에서는 추가 DataTable 열 필요한 경우 저장된 프로시저에서 권장 하는 이유 설명 합니다.


## <a name="introduction"></a>소개

형식화 된 데이터 집합에 TableAdapter에 추가할 때는 해당 DataTable의 스키마 TableAdapter s 주 쿼리에 의해 결정 됩니다. 예를 들어 주 쿼리에서 데이터 필드를 반환 하는 경우 *A*, *B*, 및 *C*, DataTable 라는 3 개의 해당 열이 포함 됩니다 *A*, *B*, 및 *C*합니다. 주 쿼리에서 외에도 TableAdapter, 일부 매개 변수를 기반으로 데이터의 하위 집합을 반환 하는 추가 쿼리를 포함할 수 있습니다. 예를 들어, 이외에 `ProductsTableAdapter` , 모든 제품에 대 한 정보를 반환 하는 s 주 쿼리도 포함 등의 방법을 `GetProductsByCategoryID(categoryID)` 및 `GetProductByProductID(productID)`, 제공 된 매개 변수를 기반으로 하는 특정 제품 정보를 반환 합니다.

TableAdapter s 주 쿼리를 반영 하는 DataTable의 스키마의 모델에는 모든 TableAdapter s 메서드의 같거나 주 쿼리에서 지정 된 것 보다 적은 수의 데이터 필드를 반환 하는 경우에 작동 합니다. TableAdapter 메서드를 추가 데이터 필드를 반환 하는 경우 다음 우리 확장 해야 DataTable의 스키마 적절 하 게 합니다. 에 [마스터/세부 레코드를 사용 하는 글머리 기호 목록의 마스터 세부 정보 사용](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md) 메서드를 추가 하는 자습서는 `CategoriesTableAdapter` 반환 되는 `CategoryID`, `CategoryName`, 및 `Description` 에 정의 된 데이터 필드 더하기 주 쿼리에서 `NumberOfProducts`, 각 범주와 관련 된 제품 수를 보고 하는 추가 데이터 필드입니다. 새 열을 수동으로 추가 했습니다는 `CategoriesDataTable` 캡처하려면는 `NumberOfProducts` 데이터 필드에서이 새 메서드는 값입니다.

에 설명 된 대로 [파일 업로드](../working-with-binary-files/uploading-files-vb.md) 자습서, 매우 주의 해야와 Tableadapter 임시 SQL 문을 사용 하는 메서드가 해당 데이터 필드 주 쿼리를 정확 하 게 일치 하지 않습니다. TableAdapter 구성 마법사를 다시 실행 하는 경우 해당 데이터 필드 목록 주 쿼리에서 일치 하도록 모든 TableAdapter s 메서드의 업데이트 합니다. 따라서 사용자 지정된 열 목록 사용 하 여 모든 메서드 주 쿼리의 열 목록으로를 예상 되는 데이터를 반환 하지 됩니다. 저장된 프로시저를 사용 하는 경우에이 문제가 발생 하지 않습니다.

이 자습서에서는 추가 열을 포함 하는 DataTable의 스키마를 확장 하는 방법을 살펴보겠습니다. 임시 SQL 문을 사용 하는 경우 TableAdapter의 오류, 때문에이 자습서에서 사용 합니다 저장된 프로시저. 참조는 [새 저장 프로시저 만들기 형식의 DataSet s Tableadapter에 대 한](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) 및 [를 사용 하 여 기존 저장 프로시저 형식화 된 데이터 집합의 Tableadapter에 대 한](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) 대 한 자세한 내용은 자습서 저장된 프로시저를 사용 하 여 TableAdapter를 구성 합니다.

## <a name="step-1-adding-apricequartilecolumn-to-theproductsdatatable"></a>1 단계: 추가 된`PriceQuartile`열에는`ProductsDataTable`

에 *새 저장 프로시저 만들기 형식의 DataSet s Tableadapter에 대 한* 라는 형식화 된 데이터 집합을 만들었습니다 자습서 `NorthwindWithSprocs`합니다. 이 데이터 집합에는 현재 두 개의 DataTables 포함: `ProductsDataTable` 및 `EmployeesDataTable`합니다. `ProductsTableAdapter` 에 다음과 같은 세 가지 메서드가 있습니다.

- `GetProducts` -주 쿼리에서의 모든 레코드를 반환 하는 `Products` 테이블
- `GetProductsByCategoryID(categoryID)` -지정 된 모든 제품을 반환 *categoryID*합니다.
- `GetProductByProductID(productID)` -지정 된 특정 제품을 반환 *productID*합니다.

주 쿼리 및 두 개의 추가 메서드를 모두 반환 즉의 모든 열에서 데이터 필드의 동일한 집합의 `Products` 테이블입니다. 상호 관련 된 하위 쿼리가 없습니다 또는 `JOIN` 관련된 데이터를 가져오는 s는 `Categories` 또는 `Suppliers` 테이블입니다. 따라서는 `ProductsDataTable` 의 각 필드에 대 한 해당 열이 고 `Products` 테이블입니다.

이 자습서에 대 한 s 수 있도록 하는 메서드를 추가 `ProductsTableAdapter` 라는 `GetProductsWithPriceQuartile` 모든 제품을 반환 하는 합니다. 표준 제품 데이터 필드와 함께 `GetProductsWithPriceQuartile` 도 포함 됩니다는 `PriceQuartile`의 제품 가격이는 변 위치에서 나타내는 데이터 필드입니다. 예를 들어 해당 가격 가장 비용이 많이 드는 25%의 단위는 해당 제품을 갖습니다는 `PriceQuartile` 1 인 동안 인 가격 아래쪽 25%에 해당 하는 것은 4의 값을 갖습니다. 그러나이 정보를 반환 하려면 저장된 프로시저를 만드는 방법에 대해 걱정할 것 전에 먼저 업데이트 해야는 `ProductsDataTable` 저장할 열을 포함 하도록는 `PriceQuartile` 결과 때는 `GetProductsWithPriceQuartile` 메서드를 사용 합니다.

열기는 `NorthwindWithSprocs` 데이터 집합에서 마우스 오른쪽 단추로 클릭 하 고는 `ProductsDataTable`합니다. 상황에 맞는 메뉴에서 추가 선택한 다음 열을 선택 합니다.


[![ProductsDataTable에 새 열 추가](adding-additional-datatable-columns-vb/_static/image2.png)](adding-additional-datatable-columns-vb/_static/image1.png)

**그림 1**: 새 열을 추가 하는 `ProductsDataTable` ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-vb/_static/image3.png))


형식의 열 1 라는 DataTable에 새 열이 추가 됩니다 `System.String`합니다. 이 열의 이름을 업데이트할 수도 PriceQuartile 및 매개 변수 형식 해야 `System.Int32` 1에서 4 사이의 숫자를 저장 하는 이후 합니다. 새로 추가 된 열 선택의 `ProductsDataTable` 속성 창에서 설정 및는 `Name` 속성 PriceQuartile 및 `DataType` 속성을 `System.Int32`합니다.


[![새 열의 이름 및 데이터 형식 속성을 설정 합니다.](adding-additional-datatable-columns-vb/_static/image5.png)](adding-additional-datatable-columns-vb/_static/image4.png)

**그림 2**: 새 열 s 설정 `Name` 및 `DataType` 속성 ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-vb/_static/image6.png))


열에서 값 열이 자동 증분 열에는 고유 해야 하는지 여부와 같은 설정할 수 있는 추가 속성 그림 2에서 볼 수 있듯이, 여부 데이터베이스 `NULL` 값 허용 여부와 등입니다. 이러한 값을 기본값으로 설정 그대로 둡니다.

## <a name="step-2-creating-thegetproductswithpricequartilemethod"></a>2 단계: 만들기는`GetProductsWithPriceQuartile`메서드

이제는 `ProductsDataTable` 포함 하도록 업데이트 되었습니다는 `PriceQuartile` 만들 준비가 된 열에서 우리는 `GetProductsWithPriceQuartile` 메서드. TableAdapter를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 추가 쿼리를 선택 하 여 시작 합니다. 그러면는 TableAdapter 쿼리 구성 마법사를 먼저 임시 SQL 문 또는 기존 또는 새 저장된 프로시저를 사용 하 려 하는지 여부에 대 한 라는 메시지가 나타납니다. 이후 인할 म 집중식 가격 사분 위 수 데이터를 반환 하는 저장된 프로시저를 위해이 저장된 프로시저를 만드는 TableAdapter를 허용 하는 s가 있습니다. 새 저장된 프로시저 만들기 옵션을 선택 하 고 클릭 합니다.


[![Us에 대 한 저장된 프로시저를 만드는 TableAdapter 마법사를 지시 합니다.](adding-additional-datatable-columns-vb/_static/image8.png)](adding-additional-datatable-columns-vb/_static/image7.png)

**그림 3**: TableAdapter 마법사는 저장 프로시저에 대 한 우리 만들려는 지시 ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-vb/_static/image9.png))


그림 4에 표시 된 후속 화면에서 묻는 메시지가 우리 어떤 유형의 쿼리를 추가 합니다. 이후는 `GetProductsWithPriceQuartile` 메서드는 모든 열과의 레코드를 반환 된 `Products` 테이블에서 행 반환 옵션 고 다음을 클릭 하 고 SELECT를 선택 합니다.


[![이 예제 쿼리에서 SELECT 문을 해당 반환 여러 행 됩니다.](adding-additional-datatable-columns-vb/_static/image11.png)](adding-additional-datatable-columns-vb/_static/image10.png)

**그림 4**: Our 쿼리가 됩니다는 `SELECT` 문을 해당 반환 여러 행 ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-vb/_static/image12.png))


다음에 대 한 메시지가 나타나면 우리는 `SELECT` 쿼리 합니다. 마법사에 다음 쿼리를 입력 합니다.


[!code-sql[Main](adding-additional-datatable-columns-vb/samples/sample1.sql)]

위의 쿼리에서 새 SQL Server 2005 s 사용 [ `NTILE` 함수](https://msdn.microsoft.com/library/ms175126.aspx) 그룹에 의해 결정 됩니다 여기서 4 개 그룹으로 결과 분할 하는 `UnitPrice` 내림차순으로 정렬 하는 값입니다.

안타깝게도, 쿼리 작성기 방법을 모르는 구문 분석 하는 `OVER` 키워드 위의 쿼리를 구문 분석할 때 오류가 표시 됩니다. 따라서 쿼리 작성기를 사용 하지 않고 마법사에서 텍스트 상자에 직접 위의 쿼리를 입력 합니다.

> [!NOTE]
> NTILE 및 SQL Server 2005 s에 대 한 자세한 내용은 다른 순위 함수 참조 [Microsoft SQL Server 2005를 사용 하 여 순위 결과 반환](http://www.4guysfromrolla.com/webtech/010406-1.shtml) 및 [순위 함수 섹션](https://msdn.microsoft.com/library/ms189798.aspx) 에서 [SQL Server 2005 온라인 설명서](https://msdn.microsoft.com/library/ms189798.aspx)합니다.


입력 한 후의 `SELECT` 마법사 요청을 만드는 저장된 프로시저에 대 한 이름을 제공 하 쿼리 및 다음을 클릭 합니다. 새 저장된 프로시저의 이름을 `Products_SelectWithPriceQuartile` 고 다음을 클릭 합니다.


[![저장된 프로시저 Products_SelectWithPriceQuartile 이름](adding-additional-datatable-columns-vb/_static/image14.png)](adding-additional-datatable-columns-vb/_static/image13.png)

**그림 5**: 저장 프로시저 이름을 `Products_SelectWithPriceQuartile` ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-vb/_static/image15.png))


마지막으로, TableAdapter 메서드 이름을 지정 하 라는 메시지가 나타나면 했습니다. 두 채우기 DataTable 두고 메서드를 확인 하는 DataTable 확인란 및 이름을 반환 `FillWithPriceQuartile` 및 `GetProductsWithPriceQuartile`합니다.


[![이름 TableAdapter s 메서드와 클릭 마침](adding-additional-datatable-columns-vb/_static/image17.png)](adding-additional-datatable-columns-vb/_static/image16.png)

**그림 6**: TableAdapter의 메서드 및 마침 이름을 ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-vb/_static/image18.png))


와 `SELECT` 쿼리 지정 및 저장된 프로시저 및 TableAdapter 메서드 명명 된 인스턴스인지에 마법사를 완료 하려면 마침을 클릭 합니다. 이 시점에서 경고 또는 되었다는 마법사에서 두 개를 발생할 수 있습니다는 `OVER` SQL 구문 또는 문은 지원 되지 않습니다. 이러한 경고는 무시 됩니다.

TableAdapter 마법사를 완료 한 후 포함할지는 `FillWithPriceQuartile` 및 `GetProductsWithPriceQuartile` 메서드 및 데이터베이스 라는 저장된 프로시저를 포함 해야 `Products_SelectWithPriceQuartile`합니다. 잠시 TableAdapter는이 새로운 방법을 실제로 되 고 저장된 프로시저는 데이터베이스에 올바르게 추가 되었습니다. 때는 저장된 프로시저가 try 마우스 오른쪽 단추로 클릭 Stored Procedures 폴더에 새로 고침 선택 표시 되지 않으면 데이터베이스를 검사 합니다.


![TableAdapter에 새 메서드를 추가 되었는지 확인](adding-additional-datatable-columns-vb/_static/image19.png)

**그림 7**: TableAdapter에 새 메서드를 추가 되었는지 확인


[![데이터베이스는 Products_SelectWithPriceQuartile 포함 되어 있는지 확인 하십시오. 저장 프로시저](adding-additional-datatable-columns-vb/_static/image21.png)](adding-additional-datatable-columns-vb/_static/image20.png)

**그림 8**: 데이터베이스에 포함 되어 있는지 확인은 `Products_SelectWithPriceQuartile` 저장 프로시저 ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-vb/_static/image22.png))


> [!NOTE]
> 임시 SQL 문 대신 저장된 프로시저를 사용 하는 이점 중 하나는 TableAdapter 구성 마법사를 다시 실행 저장된 프로시저 열 목록을 수정 하지 것입니다. TableAdapter를 마우스 오른쪽 단추로 클릭 하 고 마법사를 시작 하려면 상황에 맞는 메뉴에서 구성 옵션을 선택 합니다. 다음 일까요 마침을 클릭 하 여이 확인 합니다. 다음으로 이동 하 여 데이터베이스를 보기는 `Products_SelectWithPriceQuartile` 저장 프로시저입니다. 참고 열 목록에 수정 되지 않았습니다. 여기서 사용 했던 임시 SQL 문, TableAdapter 구성 마법사를 다시 실행은 되돌리면이 s 쿼리 열 목록에서 사용 하는 쿼리에서 NTILE 문을 역폴란드 주 쿼리에서 열 목록과 일치 하는 `GetProductsWithPriceQuartile` 메서드.


때 데이터 액세스 계층 s `GetProductsWithPriceQuartile` 메서드가 호출 되 면 TableAdapter 실행는 `Products_SelectWithPriceQuartile` 에 행을 추가 하 고 저장 프로시저는 `ProductsDataTable` 반환 된 각 레코드에 대 한 합니다. 저장된 프로시저에서 반환 된 데이터 필드에 매핑되는 `ProductsDataTable`의 열입니다. 있기 때문는 `PriceQuartile` 저장된 프로시저에서 반환 된 데이터 필드에 해당 값이 할당 되는 `ProductsDataTable` s `PriceQuartile` 열입니다.

해당 쿼리에서 반환 되지 않도록 하는 TableAdapter 메서드에서 `PriceQuartile` 데이터 필드는 `PriceQuartile` s 열 값에 지정 된 값은 해당 `DefaultValue` 속성입니다. 이 값은로 설정 그림 2에서 볼 수 있듯이 `DBNull`, 기본값입니다. 다른 기본값을 사용 하려는 경우 설정 하기만 `DefaultValue` 속성 적절 하 게 합니다. 해야 하는 `DefaultValue` s 열 값이 유효한 `DataType` (즉, `System.Int32` 에 대 한는 `PriceQuartile` 열)입니다.

이 시점에서 DataTable에는 추가 열을 추가 하는 데 필요한 단계를 수행 했는지 했습니다. 추가 열이 예상 대로 작동 하는지 확인 하려면 만든 각 제품의 이름, 가격 및 가격 사분 위 수를 표시 하는 ASP.NET 페이지의 사용 수 있습니다. 그 전에 하지만 먼저 업데이트 해야 DAL s에 호출 하는 메서드를 포함 하도록 비즈니스 논리 계층 `GetProductsWithPriceQuartile` 메서드. 3 단계에서에서 BLL를 다음으로 업데이트 하 고 4 단계에서에서 ASP.NET 페이지를 만듭니다 합니다.

## <a name="step-3-augmenting-the-business-logic-layer"></a>3 단계: 비즈니스 논리 계층 확장

새 사용 전에 `GetProductsWithPriceQuartile` 메서드 프레젠테이션 계층에서에서는 먼저 추가 해야 해당 메서드가 BLL에 있습니다. 열기는 `ProductsBLLWithSprocs` 클래스 파일을 다음 코드를 추가 합니다.


[!code-vb[Main](adding-additional-datatable-columns-vb/samples/sample2.vb)]

등의 다른 데이터 검색 방법을 `ProductsBLLWithSprocs`, `GetProductsWithPriceQuartile` 메서드는 단순히 DAL 호출 s 해당 `GetProductsWithPriceQuartile` 메서드 해당 결과 반환 합니다.

## <a name="step-4-displaying-the-price-quartile-information-in-an-aspnet-web-page"></a>4 단계: ASP.NET 웹 페이지에 가격 사분 위 수 정보를 표시합니다.

BLL 추가 하 여 준비 된 각 제품에 대 한 가격 사분 위 수를 보여 주는 ASP.NET 페이지를 만드는 것를 완료 합니다. 열기는 `AddingColumns.aspx` 페이지에 `AdvancedDAL` 폴더를 끌어서는 GridView 설정 디자이너 도구 상자에서 해당 `ID` 속성을 `Products`합니다. GridView s 스마트 태그에서 바인딩할 라는 새 ObjectDataSource `ProductsDataSource`합니다. ObjectDataSource 사용 하도록 구성 된 `ProductsBLLWithSprocs` s 클래스 `GetProductsWithPriceQuartile` 메서드. 있으므로이 읽기 전용 표로, 삽입, 업데이트에서 드롭 다운 목록을 설정 하 고 각 탭 (없음)을 삭제 합니다.


[![ObjectDataSource ProductsBLLWithSprocs 클래스를 사용 하도록 구성](adding-additional-datatable-columns-vb/_static/image24.png)](adding-additional-datatable-columns-vb/_static/image23.png)

**그림 9**: 구성에 사용 하 여 ObjectDataSource는 `ProductsBLLWithSprocs` 클래스 ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-vb/_static/image25.png))


[![GetProductsWithPriceQuartile 메서드에서 제품 정보 검색](adding-additional-datatable-columns-vb/_static/image27.png)](adding-additional-datatable-columns-vb/_static/image26.png)

**그림 10**: 제품 정보에서 검색 된 `GetProductsWithPriceQuartile` 메서드 ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-vb/_static/image28.png))


데이터 소스 구성 마법사를 완료 한 후 Visual Studio는 자동으로 추가 BoundField 또는 CheckBoxField GridView 각 메서드에 의해 반환 되는 데이터 필드에 대 한. 이러한 데이터 필드 중 하나는 `PriceQuartile`에 추가한 열은 `ProductsDataTable` 1 단계에서에서 합니다.

제거 GridView의 필드를 편집 제외한 모두 `ProductName`, `UnitPrice`, 및 `PriceQuartile` BoundFields 합니다. 구성에서 `UnitPrice` BoundField 통화로 해당 값의 형식을 지정 하는 `UnitPrice` 및 `PriceQuartile` BoundFields 오른쪽-및 가운데 맞춤, 각각. 마지막으로 남은 BoundFields 업데이트 `HeaderText` 속성을 제품, 가격 및 가격 사분 위 수, 각각. GridView s 스마트 태그에서 정렬 사용 확인란을 확인 하십시오.

이러한 수정 후 GridView 및 ObjectDataSource s 선언적 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](adding-additional-datatable-columns-vb/samples/sample3.aspx)]

그림 11 브라우저를 통해가 방문 하면이 페이지를 보여 줍니다. 즉, 처음에 제품으로 정렬 됩니다 내림차순 적절 한 할당 된 각 제품의 가격 참고 `PriceQuartile` 값입니다. 여전히 가격에 대해 제품의 순위를 반영 가격 사분 위 수 열 값이 있는 다른 기준으로이 데이터를 정렬 하 된 물론 (그림 12 참조).


[![제품 가격으로 정렬 됩니다.](adding-additional-datatable-columns-vb/_static/image30.png)](adding-additional-datatable-columns-vb/_static/image29.png)

**그림 11**: The 제품 가격으로 정렬 됩니다 ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-vb/_static/image31.png))


[![제품 이름으로 정렬 합니다.](adding-additional-datatable-columns-vb/_static/image33.png)](adding-additional-datatable-columns-vb/_static/image32.png)

**그림 12**: The 제품 이름으로 정렬 됩니다 ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-vb/_static/image34.png))


> [!NOTE]
> 코드 몇 줄만 म 수 보강 GridView에 기반 하 여 제품 행을 색이 지정 되도록 해당 `PriceQuartile` 값입니다. 첫 번째 사분 위 수의 두 번째 사분 위 수 연한 노랑 연한 녹색에서 해당 제품 색을 등 수 있습니다. 확인해 보십시오 잠시이 기능을 추가 합니다. 세부 정보는 GridView 서식 지정 해야 하는 경우 참조는 [데이터 기반 시 사용자 지정 서식](../custom-formatting/custom-formatting-based-upon-data-vb.md) 자습서입니다.


## <a name="an-alternative-approach---creating-another-tableadapter"></a>다른 방법은-다른 TableAdapter 만들기

주 쿼리에서 명시 된 것과 다른 데이터 필드를 반환 하는 TableAdapter에 메서드를 추가 하는 경우이 자습서에서 설명한 것 처럼에 DataTable을 해당 열을 추가할 수 있습니다. 그러나 이러한 접근 방식은, 된 대체 데이터 필드는 기본 쿼리에서 너무 많이 달라 지지 않도록 하는 경우와 다른 데이터 필드를 반환 하는 메서드는 TableAdapter의 수가 적은 경우에 작동 합니다.

DataTable에 열을 추가 하는 대신 다른 데이터 필드를 반환 하는 첫 번째 TableAdapter의 메서드를 포함 된 데이터 집합 대신 다른 TableAdapter를 추가할 수 있습니다. 이 자습서에 대 한 추가 하지 않고는 `PriceQuartile` 열을는 `ProductsDataTable` (위치에서 사용 되는 `GetProductsWithPriceQuartile` 메서드), 수 추가 TableAdapter에 추가한 라는 데이터 집합 `ProductsWithPriceQuartileTableAdapter` 사용는 `Products_SelectWithPriceQuartile` 저장 기본 쿼리로 프로시저입니다. ASP.NET 페이지 가격 변 위치를 사용 하 여 제품 정보를 가져오는 데 필요한 사용는 `ProductsWithPriceQuartileTableAdapter`계속 사용할 수 하지 않은 하는 반면는 `ProductsTableAdapter`합니다.

새 TableAdapter를 추가는 Datatable untarnished 남아 있고 해당 열 자신의 TableAdapter의 메서드에 의해 반환 되는 데이터 필드를 정확 하 게 반영 합니다. 그러나 반복 되는 작업 및 기능 추가 Tableadapter 발생할 수 있습니다. 예를 들어 이러한 경우 ASP.NET 페이지가 표시 되는 `PriceQuartile` 열도 필요한 insert, 수 있도록 업데이트 및 삭제 지원는 `ProductsWithPriceQuartileTableAdapter` 있어야 해당 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 속성 제대로 구성합니다. 이러한 속성은 미러링할 동안는 `ProductsTableAdapter` s,이 구성은 별도 단계를 소개 합니다. 또한는 이제 업데이트 하는 두 가지를 삭제 하거나 데이터베이스에 제품을 통해 추가 된 `ProductsTableAdapter` 및 `ProductsWithPriceQuartileTableAdapter` 클래스입니다.

이 자습서에 대 한 다운로드에 포함 되어는 `ProductsWithPriceQuartileTableAdapter` 클래스에 `NorthwindWithSprocs` 집합이이 대체 방법을 보여 줍니다.

## <a name="summary"></a>요약

대부분의 시나리오에서 TableAdapter의 메서드는의 모든 데이터 필드의 동일한 집합을 반환 하지만 특정 메서드 또는 두 개의 추가 필드를 반환 해야 할 수는 경우 경우가 있습니다. 예를 들어는 [마스터/세부 레코드를 사용 하는 글머리 기호 목록의 마스터 세부 정보 사용](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md) 메서드를 추가 하는 자습서는 `CategoriesTableAdapter` 반환 하는 기본 쿼리에의 데이터 필드 외에도 하는 `NumberOfProducts` 필드 각 범주와 관련 된 제품 수를 보고 합니다. 이 자습서에서 보이는 것 처럼에 메서드 추가 `ProductsTableAdapter` 반환 되는 `PriceQuartile` 주 쿼리의 데이터 필드와 함께 필드입니다. 추가 데이터를 캡처하려면 필드를 DataTable로 해당 열을 추가 해야 TableAdapter의 메서드에 의해 반환 합니다.

수동으로 DataTable에 열을 추가 하려는 경우 TableAdapter 저장된 프로시저를 사용 하는 것이 좋습니다. TableAdapter에서 임시 SQL 문이 사용 하는 경우 언제 든 지 TableAdapter 구성 마법사가 실행 모든 주 쿼리에서 반환 된 데이터 필드에 데이터 필드 목록 되돌릴 메서드. 이 문제는 속하지 저장된 프로시저에 이기 때문에 권장 되 하며이 자습서에 사용 된 합니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Randy Schmidt, Jacky Goor, 박 광 준 Leigh 및 Hilton Giesenow 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](updating-the-tableadapter-to-use-joins-vb.md)
> [다음](working-with-computed-columns-vb.md)
