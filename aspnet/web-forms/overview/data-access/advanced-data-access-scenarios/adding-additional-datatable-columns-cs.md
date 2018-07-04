---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/adding-additional-datatable-columns-cs
title: 추가 DataTable 열 (C#)를 추가 합니다. | Microsoft Docs
author: rick-anderson
description: 입력 데이터 집합을 만들려면 TableAdapter 마법사를 사용 하는 경우 해당 DataTable 기본 데이터베이스 쿼리에서 반환 되는 열을 포함 합니다. 하지만 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/18/2007
ms.topic: article
ms.assetid: 615f3361-f21f-4338-8bc1-fce8ae071de9
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/adding-additional-datatable-columns-cs
msc.type: authoredcontent
ms.openlocfilehash: 373ba6d3ec86ea2ab26bfecf39647776694960de
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37393985"
---
<a name="adding-additional-datatable-columns-c"></a>추가 DataTable 열 추가 (C#)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_70_CS.zip) 또는 [PDF 다운로드](adding-additional-datatable-columns-cs/_static/datatutorial70cs1.pdf)

> 입력 데이터 집합을 만들려면 TableAdapter 마법사를 사용 하는 경우 해당 DataTable 기본 데이터베이스 쿼리에서 반환 되는 열을 포함 합니다. 하지만 DataTable 경우 추가 열을 포함 해야 하는 경우가 있습니다. 이 자습서에서는 추가 DataTable 열 해야 하는 경우 저장된 프로시저는 권장 하는 이유는 무엇을 알아봅니다.


## <a name="introduction"></a>소개

입력 데이터 집합에 TableAdapter에 추가할 때 해당 DataTable의 스키마 TableAdapter가 기본 쿼리에 의해 결정 됩니다. 예를 들어 데이터 필드를 반환 하는 기본 쿼리에 *A*, *B*, 및 *C*, DataTable 이라는 세 가지 해당 열이 포함 됩니다 *는*, *B*, 및 *C*합니다. 해당 주 쿼리 외에도 TableAdapter 것 일부 매개 변수를 기준으로 데이터의 하위 집합을 반환 하는 추가 쿼리를 포함할 수 있습니다. 예를 들어 외에 `ProductsTableAdapter` 모든 제품에 대 한 정보를 반환 하는 s 기본 쿼리에 포함와 같은 메서드 `GetProductsByCategoryID(categoryID)` 및 `GetProductByProductID(productID)`, 제공 된 매개 변수를 기반으로 하는 특정 제품 정보를 반환 하는 합니다.

TableAdapter가 기본 쿼리를 반영 하는 DataTable의 스키마의 모델에는 동일 하거나 기본 쿼리에 지정 된 것 보다 적은 수의 데이터 필드가 모든 TableAdapter가 메서드의 반환 하는 경우에 잘 작동 합니다. TableAdapter 메서드를 추가 데이터 필드를 반환 해야 하는 경우 다음 해야 확장 DataTable의 스키마 적절 하 게 합니다. [마스터/세부 정보 DataList와 함께 a 글머리 기호 목록의 마스터 레코드를 사용 하 여 세부 정보](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md) 메서드를 추가 했습니다 하는 자습서는 `CategoriesTableAdapter` 반환 되는 `CategoryID`, `CategoryName`, 및 `Description` 에 정의 된 데이터 필드 더하기 주 쿼리 `NumberOfProducts`, 각 범주와 관련 된 제품의 수를 보고 하는 추가 데이터 필드입니다. 새 열을 수동으로 추가한 합니다 `CategoriesDataTable` 캡처하려면를 `NumberOfProducts` 데이터 필드 값이 새 메서드의.

에 설명 된 대로 합니다 [파일 업로드](../working-with-binary-files/uploading-files-cs.md) 방법이 있는 데이터 필드가 주 쿼리를 정확 하 게 일치 하지 않습니다 및 임시 SQL 문을 사용 하는 Tableadapter를 사용 하 여 자습서, 유용한 주의 기울여 해야 합니다. TableAdapter 구성 마법사를 다시 실행 하는 경우 해당 데이터 필드 목록 기본 쿼리에 일치 하도록 모든 TableAdapter가 메서드의 업데이트 됩니다. 따라서 사용자 지정 된 열 목록 사용 하 여 메서드를 기본 쿼리의 열 목록으로 되돌리려면 예상 되는 데이터를 반환 하지 합니다. 저장된 프로시저를 사용 하는 경우에이 문제가 발생 하지 않습니다.

이 자습서에서는 추가 열을 포함 하는 DataTable의 스키마를 확장 하는 방법을 살펴보겠습니다. 임시 SQL 문을 사용 하는 경우 TableAdapter의 때,으로 인해이 자습서에서는 사용 하 여 저장된 프로시저입니다. 참조를 [새 저장 프로시저 만들기 형식화 된 데이터 집합의 Tableadapter에 대 한](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) 하 고 [사용 하 여 기존 저장 프로시저는 입력 데이터 집합의 Tableadapter에 대 한](https://data-access/tutorials/using-existing-stored-procedures-for-the-typed-dataset-amp-rsquo-s-tableadapters-cs) 대 한 자세한 내용은 자습서 저장된 프로시저를 사용 하도록 TableAdapter를 구성 합니다.

## <a name="step-1-adding-apricequartilecolumn-to-theproductsdatatable"></a>1 단계: 추가 된`PriceQuartile`열에는`ProductsDataTable`

에 *새 저장 프로시저 만들기 형식화 된 데이터 집합의 Tableadapter에 대 한* 라는 형식화 된 데이터 집합을 만들었습니다 자습서 `NorthwindWithSprocs`합니다. 이 데이터 집합은 현재 두 개의 Datatable을 포함 합니다. `ProductsDataTable` 고 `EmployeesDataTable`입니다. `ProductsTableAdapter` 는 다음 세 가지 메서드를 포함 합니다.

- `GetProducts` -모든 레코드를 반환 하는 기본 쿼리에 `Products` 테이블
- `GetProductsByCategoryID(categoryID)` -지정 된 모든 제품을 반환 합니다 *categoryID*합니다.
- `GetProductByProductID(productID)` -지정 된 특정 제품을 반환 합니다 *productID*합니다.

기본 쿼리를 두 가지 추가 메서드인 namely의 모든 열에서 데이터 필드의 동일한 집합을 반환 합니다 `Products` 테이블입니다. 상관 관계가 지정 된 하위 쿼리가 없습니다 또는 `JOIN` 관련된 데이터를 가져오는 s 합니다 `Categories` 또는 `Suppliers` 테이블입니다. 따라서 합니다 `ProductsDataTable` 의 각 필드에 대 한 해당 열에는 `Products` 테이블입니다.

이 자습서에서는 s를 사용 하는 메서드를 추가 합니다 `ProductsTableAdapter` 라는 `GetProductsWithPriceQuartile` 반환 하는 모든 제품입니다. 표준 제품 데이터 필드 외에도 `GetProductsWithPriceQuartile` 도 포함 됩니다는 `PriceQuartile`의 제품 가격 대체는 사분 위 수에서 나타내는 데이터 필드입니다. 예를 들어, 가격이 가장 비용이 많이 드는 25%에 해당 제품을 갖습니다는 `PriceQuartile` 4의 값이 포함 됩니다 가격이 아래 25%에 해당 하는 동안 1의 값입니다. 그러나 전에이 정보를 반환 하려면 저장된 프로시저를 만드는 지 걱정 합니다 먼저 업데이트 해야 합니다 `ProductsDataTable` 저장할 열을 포함 하도록는 `PriceQuartile` 결과 때는 `GetProductsWithPriceQuartile` 메서드를 사용 합니다.

엽니다는 `NorthwindWithSprocs` 데이터 집합 마우스 오른쪽 단추로 클릭 하 고는 `ProductsDataTable`합니다. 상황에 맞는 메뉴에서 추가 선택 하 고 열을 선택 합니다.


[![ProductsDataTable에 새 열 추가](adding-additional-datatable-columns-cs/_static/image2.png)](adding-additional-datatable-columns-cs/_static/image1.png)

**그림 1**: 새 열을 추가 하는 `ProductsDataTable` ([클릭 하 여 큰 이미지 보기](adding-additional-datatable-columns-cs/_static/image3.png))


이 형식의 Column1 이라는 DataTable에 새 열이 추가 됩니다 `System.String`합니다. PriceQuartile 및 해당 형식의이 s 열 이름을 업데이트 해야 `System.Int32` 1에서 4 사이의 숫자를 포함 하는 데 사용할 때문입니다. 에 새로 추가 된 열을 선택 합니다 `ProductsDataTable` 속성 창에서 설정 및 합니다 `Name` PriceQuartile 속성 및 `DataType` 속성을 `System.Int32`입니다.


[![새 열의 이름 및 DataType 속성 설정](adding-additional-datatable-columns-cs/_static/image5.png)](adding-additional-datatable-columns-cs/_static/image4.png)

**그림 2**: 새 열 s 설정 `Name` 하 고 `DataType` 속성 ([클릭 하 여 큰 이미지 보기](adding-additional-datatable-columns-cs/_static/image6.png))


열에서 값 열이 자동 증분 열 고유 해야 하는지 여부와 같은 설정할 수 있는 추가 속성 그림 2에서 볼 수 있듯이, 데이터베이스 여부 `NULL` 값이 허용 및 등입니다. 이러한 값을 기본값으로 설정 그대로 둡니다.

## <a name="step-2-creating-thegetproductswithpricequartilemethod"></a>2 단계: 만들기는`GetProductsWithPriceQuartile`메서드

이제는 `ProductsDataTable` 포함 하도록 업데이트 되었습니다를 `PriceQuartile` 열에서는 만들 준비가 된 `GetProductsWithPriceQuartile` 메서드. TableAdapter를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 추가 쿼리를 선택 하 여 시작 합니다. 먼저 임시 SQL 문 또는 신규 또는 기존 저장된 프로시저를 사용 하려는 지 여부에 대 한 요청 하는 TableAdapter 쿼리 구성 마법사를 표시 합니다. 인할에서는 아직 가격 사분 위 수 데이터를 반환 하는 저장 프로시저 때문에이 저장된 프로시저를 만들려면 TableAdapter를 허용 하는 s 수 있습니다. 새 저장된 프로시저 만들기 옵션을 선택 하 고 클릭 합니다.


[![우리 회사에 저장된 프로시저를 만들기 위해 TableAdapter 마법사를 지시 합니다.](adding-additional-datatable-columns-cs/_static/image8.png)](adding-additional-datatable-columns-cs/_static/image7.png)

**그림 3**: TableAdapter 마법사는 저장 프로시저에 대 한 미국 만들려면 지시 ([큰 이미지를 보려면 클릭](adding-additional-datatable-columns-cs/_static/image9.png))


그림 4의 후속 화면에서 마법사에서는 어떤 유형의 쿼리를 추가 합니다. 있으므로 `GetProductsWithPriceQuartile` 메서드는 모든 열 및 레코드를 반환 합니다 `Products` 테이블에서 행 옵션 및 다음 클릭을 반환 하는 선택.


[![쿼리에서 여러 행을 반환 하는 SELECT 문의 됩니다.](adding-additional-datatable-columns-cs/_static/image11.png)](adding-additional-datatable-columns-cs/_static/image10.png)

**그림 4**: 이러한 쿼리 수는 `SELECT` 문에 여러 행을 반환 하 ([전체 크기 이미지를 보려면 클릭](adding-additional-datatable-columns-cs/_static/image12.png))


다음에서는 묻는 `SELECT` 쿼리 합니다. 마법사에 다음 쿼리를 입력 합니다.


[!code-sql[Main](adding-additional-datatable-columns-cs/samples/sample1.sql)]

위의 쿼리는 SQL Server 2005가 새 [ `NTILE` 함수](https://msdn.microsoft.com/library/ms175126.aspx) 그룹에 의해 결정 됩니다 여기서 4 개 그룹으로 결과 분할 하는 `UnitPrice` 내림차순으로 정렬 하는 값입니다.

그러나 쿼리 작성기를 알지 구문 분석 하는 방법의 `OVER` 키워드 위의 쿼리를 구문 분석할 때 오류가 표시 됩니다. 따라서 쿼리 작성기를 사용 하지 않고 마법사에서 텍스트 상자에 직접 위의 쿼리를 입력 합니다.

> [!NOTE]
> NTILE 및 SQL Server 2005 s에 대 한 자세한 내용은 다른 순위 함수를 참조 하세요 [Microsoft SQL Server 2005를 사용 하 여 순위 결과 반환](http://www.4guysfromrolla.com/webtech/010406-1.shtml) 하며 [순위 함수 섹션](https://msdn.microsoft.com/library/ms189798.aspx) 에서 [SQL Server 2005 온라인](https://msdn.microsoft.com/library/ms189798.aspx)합니다.


입력 한 후의 `SELECT` 마법사 요청을 만드는 저장된 프로시저에 대 한 이름을 제공할 쿼리 및 다음을 클릭 합니다. 새 저장된 프로시저의 이름을 `Products_SelectWithPriceQuartile` 다음을 클릭 합니다.


[![저장된 프로시저 Products_SelectWithPriceQuartile 이름](adding-additional-datatable-columns-cs/_static/image14.png)](adding-additional-datatable-columns-cs/_static/image13.png)

**그림 5**: 저장 프로시저의 이름을 `Products_SelectWithPriceQuartile` ([클릭 하 여 큰 이미지 보기](adding-additional-datatable-columns-cs/_static/image15.png))


마지막으로, TableAdapter 메서드 이름을에서는 메시지가 표시 됩니다. 모두 채우기 DataTable 나갔다가 이름과 DataTable 확인란 선택 메서드 `FillWithPriceQuartile` 고 `GetProductsWithPriceQuartile`입니다.


[![완료 하 고 이름 TableAdapter의 메서드](adding-additional-datatable-columns-cs/_static/image17.png)](adding-additional-datatable-columns-cs/_static/image16.png)

**그림 6**: TableAdapter의 메서드 및 마침 이름 ([큰 이미지를 보려면 클릭](adding-additional-datatable-columns-cs/_static/image18.png))


사용 하 여는 `SELECT` 쿼리를 지정 하 고 저장된 프로시저 및 TableAdapter 메서드 라는는 마법사를 완료 하려면 마침을 클릭 합니다. 이 시점에서 경고 또는 격언이 마법사에서 두 개를 발생할 수 있습니다는 `OVER` SQL 구문 또는 문은 지원 되지 않습니다. 이러한 경고를 무시할 수 있습니다.

TableAdapter 마법사를 완료 한 후 포함 해야 합니다 `FillWithPriceQuartile` 하 고 `GetProductsWithPriceQuartile` 메서드 및 데이터베이스 저장된 프로시저를 포함 해야 `Products_SelectWithPriceQuartile`. 시간을 내어 TableAdapter 포함이 새로운 메서드가 실제로 및 저장된 프로시저 데이터베이스에 올바르게 추가 되었는지 확인 합니다. 경우는 저장된 프로시저 시도 마우스 오른쪽 단추로 클릭 Stored Procedures 폴더에 새로 고침을 선택 하면 표시 되지 않으면 데이터베이스를 검사 합니다.


![새 메서드가 TableAdapter에 추가 된 것 확인](adding-additional-datatable-columns-cs/_static/image19.png)

**그림 7**: 새 메서드가 TableAdapter에 추가 된 것 확인


[![데이터베이스는 Products_SelectWithPriceQuartile 포함 되어 있는지 확인 저장 프로시저](adding-additional-datatable-columns-cs/_static/image21.png)](adding-additional-datatable-columns-cs/_static/image20.png)

**그림 8**: 데이터베이스에 포함 되어 있는지 확인 합니다 `Products_SelectWithPriceQuartile` 저장 프로시저 ([클릭 하 여 큰 이미지 보기](adding-additional-datatable-columns-cs/_static/image22.png))


> [!NOTE]
> 임시 SQL 문 대신 저장된 프로시저를 사용 하는 이점 중 하나는 TableAdapter 구성 마법사를 다시 실행 저장된 프로시저 열 목록을 수정 하지 것입니다. TableAdapter를 마우스 오른쪽 단추로 클릭 하 고 마법사를 시작 하려면 상황에 맞는 메뉴에서 구성 옵션을 선택 합니다. 완료 하려면 마침을 클릭 하 여이 확인 합니다. 다음으로, 데이터베이스 및 보기로 이동 합니다 `Products_SelectWithPriceQuartile` 저장 프로시저입니다. 참고 열 목록에 수정 되지 않았습니다. 에서는 사용한 임시 SQL 문이, TableAdapter 구성 마법사를 다시 실행은 되돌리면이 s 쿼리 열 목록에서 사용 하는 쿼리는 NTILE 문을 역폴란드 주 쿼리 열 목록에 맞게는 `GetProductsWithPriceQuartile` 메서드.


때 데이터 액세스 계층 s `GetProductsWithPriceQuartile` 메서드가 호출 되 면 TableAdapter를 실행 합니다 `Products_SelectWithPriceQuartile` 저장 프로시저 및 행을 추가 `ProductsDataTable` 반환 된 각 레코드에 대 한 합니다. 저장된 프로시저에서 반환 된 데이터 필드에 매핑되는 `ProductsDataTable`의 열입니다. 되므로 `PriceQuartile` 저장된 프로시저에서 반환 된 데이터 필드의 값에 할당 합니다 `ProductsDataTable` s `PriceQuartile` 열.

해당 쿼리를 반환 하지 않는 이러한 TableAdapter 메서드는 `PriceQuartile` 데이터 필드를 `PriceQuartile` s 열 값에 지정 된 값이 해당 `DefaultValue` 속성. 이 값은로 그림 2에서 볼 수 있듯이 `DBNull`, 기본값입니다. 다른 기본값을 사용 하려는 경우 설정 하기만 합니다 `DefaultValue` 속성 적절 하 게 합니다. 만 있는지 확인 합니다 `DefaultValue` s 열을 지정 된 값이 유효한 `DataType` (즉, `System.Int32` 에 대 한는 `PriceQuartile` 열).

이 시점에서 DataTable에 추가 열을 추가 하는 것에 대 한 필요한 단계를 수행 했습니다. 추가 열이 예상 대로 작동 하는지 확인 하려면 s를 각 제품의 이름, 가격 및 가격 사분 위 수를 표시 하는 ASP.NET 페이지를 만들 수 있습니다. 작업을 수행 하기 전에 하지만 먼저 업데이트 해야 DAL s 호출 하는 메서드를 포함 하도록 비즈니스 논리 계층 `GetProductsWithPriceQuartile` 메서드. 3 단계에서에서 BLL을 다음으로 업데이트 하 고 4 단계에서에서 ASP.NET 페이지를 만듭니다.

## <a name="step-3-augmenting-the-business-logic-layer"></a>3 단계: 비즈니스 논리 계층 확대

새 사용 전에 `GetProductsWithPriceQuartile` 메서드 프레젠테이션 계층에서 먼저 추가 해야 해당 메서드는 BLL 하 합니다. 열기는 `ProductsBLLWithSprocs` 클래스 파일 및 다음 코드를 추가 합니다.


[!code-csharp[Main](adding-additional-datatable-columns-cs/samples/sample2.cs)]

등의 다른 데이터 검색 메서드보다 `ProductsBLLWithSprocs`의 `GetProductsWithPriceQuartile` 메서드는 간단히 DAL 호출 s 해당 `GetProductsWithPriceQuartile` 메서드 결과 반환 합니다.

## <a name="step-4-displaying-the-price-quartile-information-in-an-aspnet-web-page"></a>ASP.NET 웹 페이지에서 가격 사분 위 수 정보를 표시 하는 4 단계:

BLL 추가 하 여 준비 된 각 제품에 대 한 가격 사분 위 수를 보여주는 ASP.NET 페이지를 만들려면 우리를 완료 합니다. 열기는 `AddingColumns.aspx` 페이지에 `AdvancedDAL` 폴더 및 설정 디자이너 도구 상자에서 GridView 끌어서 해당 `ID` 속성을 `Products`합니다. GridView가 스마트 태그에서 바인딩할 라는 새로운 ObjectDataSource는 `ProductsDataSource`합니다. ObjectDataSource를 사용 하 여 구성 합니다 `ProductsBLLWithSprocs` s 클래스 `GetProductsWithPriceQuartile` 메서드. 되므로이 읽기 전용 표로, UPDATE, INSERT에서에서 드롭 다운 목록을 설정 하 고 탭 (없음)를 삭제 합니다.


[![ProductsBLLWithSprocs 클래스를 사용 하는 ObjectDataSource 구성](adding-additional-datatable-columns-cs/_static/image24.png)](adding-additional-datatable-columns-cs/_static/image23.png)

**그림 9**: ObjectDataSource 사용 하도록 구성 된 `ProductsBLLWithSprocs` 클래스 ([클릭 하 여 큰 이미지 보기](adding-additional-datatable-columns-cs/_static/image25.png))


[![GetProductsWithPriceQuartile 메서드에서 제품 정보 검색](adding-additional-datatable-columns-cs/_static/image27.png)](adding-additional-datatable-columns-cs/_static/image26.png)

**그림 10**:에서 제품 정보를 검색 합니다 `GetProductsWithPriceQuartile` 메서드 ([클릭 하 여 큰 이미지 보기](adding-additional-datatable-columns-cs/_static/image28.png))


데이터 소스 구성 마법사를 완료 한 후 Visual Studio는 자동으로 추가 BoundField 또는 CheckBoxField GridView의 각 메서드에서 반환 된 데이터 필드에 대 한. 이러한 데이터 필드 중 하나가 `PriceQuartile`에 추가한 열을 `ProductsDataTable` 1 단계에서에서 합니다.

제거 GridView의 필드를 편집할 외에 모든 `ProductName`, `UnitPrice`, 및 `PriceQuartile` BoundFields 합니다. 구성 합니다 `UnitPrice` 하 고 해당 값을 통화로 BoundField 합니다 `UnitPrice` 및 `PriceQuartile` BoundFields 오른쪽-및 가운데 맞춤, 각각. 마지막으로 나머지 BoundFields 업데이트 `HeaderText` 속성을 제품, 가격 및 가격 사분 위 수, 각각. 또한 GridView가 스마트 태그에서 정렬 사용 확인란을 확인 합니다.

이러한 수정 후 GridView 및 ObjectDataSource가 선언적 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](adding-additional-datatable-columns-cs/samples/sample3.aspx)]

그림 11에서는 브라우저를 통해 방문 하는 경우이 페이지를 보여 줍니다. 처음에 제품을 기준으로 정렬 됩니다 적절 한 할당 된 각 제품을 사용 하 여 내림차순 가격 확인 `PriceQuartile` 값입니다. 물론이 데이터를 정렬 다른 기준으로 여전히 가격 관련 하 여 제품의 순위를 반영 하는 가격 사분 위 수 열 값을 사용 하 여 (그림 12 참조).


[![제품 가격으로 정렬 됩니다.](adding-additional-datatable-columns-cs/_static/image30.png)](adding-additional-datatable-columns-cs/_static/image29.png)

**그림 11**:의 제품 가격으로 정렬 됩니다 ([큰 이미지를 보려면 클릭](adding-additional-datatable-columns-cs/_static/image31.png))


[![제품 이름으로 정렬 됩니다.](adding-additional-datatable-columns-cs/_static/image33.png)](adding-additional-datatable-columns-cs/_static/image32.png)

**그림 12**: The 제품 이름별으로 정렬 됩니다 ([큰 이미지를 보려면 클릭](adding-additional-datatable-columns-cs/_static/image34.png))


> [!NOTE]
> 몇 줄의 코드로 수 살펴보면서 GridView에 따라 제품 행 색이 지정 된이 되도록 해당 `PriceQuartile` 값입니다. 첫 번째 사분 위 수의 두 번째 사분 위 수는 밝은 노랑을 연한 녹색에서 해당 제품을 색 하 고 등 수 있습니다. 잠시이 기능을 추가 하 게 하시기 바랍니다. GridView를 서식 지정에 리프레셔가 필요한 경우 참조를 [데이터를 기반으로 사용자 지정 서식 지정](../custom-formatting/custom-formatting-based-upon-data-cs.md) 자습서입니다.


## <a name="an-alternative-approach---creating-another-tableadapter"></a>대안은-다른 TableAdapter 만들기

기본 쿼리에서 명시 된 것과 다른 데이터 필드를 반환 하는 TableAdapter에 메서드를 추가 하는 경우이 자습서에서 설명한 것 처럼 해당 열을 DataTable에 추가할 수 있습니다. 그러나 이러한 접근 방식을, 이러한 대체 데이터 필드 기본 쿼리에서 너무 많이 달라 지지 않는 경우 및 다른 데이터 필드를 반환 하는 TableAdapter의 메서드 중 소수의 필요한 경우에 작동 합니다.

DataTable에 열을 추가 하는 대신 다른 데이터 필드를 반환 하는 첫 번째 TableAdapter의 메서드를 포함 하는 데이터 집합에 TableAdapter를 다른 대신 추가할 수 있습니다. 이 자습서에서는 추가 하지 않고는 `PriceQuartile` 열을 합니다 `ProductsDataTable` (만 사용 된 위치에서 `GetProductsWithPriceQuartile` 메서드), 수는 추가 TableAdapter에 추가 라는 데이터 집합 `ProductsWithPriceQuartileTableAdapter` 는 `Products_SelectWithPriceQuartile` 저장 해당 기본 쿼리로 프로시저입니다. 가격 사분 위 수를 사용 하 여 제품 정보를 가져오는 데 필요한 ASP.NET 페이지 사용 합니다 `ProductsWithPriceQuartileTableAdapter`반면 계속 사용할 수 있습니다 하지 못한 것는 `ProductsTableAdapter`합니다.

새 TableAdapter에 추가 하 여 untarnished 유지 된 Datatable 및 해당 열에 해당 TableAdapter가 메서드에서 반환 된 데이터 필드를 정확 하 게 반영 합니다. 그러나 추가 Tableadapter의 반복적인 태스크 및 기능을 제공할 수 있습니다. 예를 들어 이러한 표시는 ASP.NET 페이지는 `PriceQuartile` 열도 필요한 제공 삽입, 업데이트 및 삭제 지원 합니다 `ProductsWithPriceQuartileTableAdapter` 포함 해야 해당 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 속성 제대로 구성 합니다. 이러한 속성은 미러링 하는 동안는 `ProductsTableAdapter` s,이 구성은 별도 단계를 소개 합니다. 또한는 이제 업데이트 하는 두 가지를 삭제 하거나 데이터베이스에 제품을 통해 추가 된 `ProductsTableAdapter` 및 `ProductsWithPriceQuartileTableAdapter` 클래스입니다.

이 자습서에 대 한 다운로드에 포함 되어는 `ProductsWithPriceQuartileTableAdapter` 클래스는 `NorthwindWithSprocs` 이 대안을 보여 주는 데이터 집합입니다.

## <a name="summary"></a>요약

대부분의 시나리오에서 TableAdapter의 메서드 중 모든 데이터 필드의 동일한 집합을 반환 하지만 특정 메서드 또는 두 개의 추가 필드를 반환할 때 해야 하는 경우가 있습니다. 예를 들어,를 [마스터/세부 정보 DataList와 함께 a 글머리 기호 목록의 마스터 레코드를 사용 하 여 세부 정보](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md) 메서드를 추가 했습니다 하는 자습서는 `CategoriesTableAdapter` 반환 되는 기본 쿼리에의 데이터 필드 외에를 `NumberOfProducts` 필드는 각 범주와 관련 된 제품의 수를 보고 합니다. 이 자습서에 메서드 추가 살펴보았습니다를 `ProductsTableAdapter` 반환을 `PriceQuartile` 주 쿼리의 데이터 필드 외에도 필드. 추가 데이터를 캡처할 필드 DataTable에 해당 하는 열을 추가 해야 TableAdapter가 메서드에서 반환 합니다.

DataTable에 열을 수동으로 추가 하려는 경우 TableAdapter 저장된 프로시저를 사용 하는 것이 좋습니다. TableAdapter는 임시 SQL 문을 사용 하 여, 언제 든 지 TableAdapter 구성 마법사 실행 됩니다 모든 데이터 필드 목록이 주 쿼리에서 반환 된 데이터 필드를 되돌리려면 메서드. 이 문제 확장 되지 않습니다 저장 프로시저는 것이 좋습니다 하며이 자습서에 사용 된 이유는.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Randy Schmidt, Jacky Goor, 박 광 준 Leigh 및 Hilton giesenow가 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](updating-the-tableadapter-to-use-joins-cs.md)
> [다음](working-with-computed-columns-cs.md)
