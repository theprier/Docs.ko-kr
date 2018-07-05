---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs
title: 기존 저장 프로시저 사용에 대 한 형식화 된 데이터 집합의 Tableadapter (C#) | Microsoft Docs
author: rick-anderson
description: 이전 자습서에서 TableAdapter 마법사를 사용 하 여 새 저장된 프로시저를 생성 하는 방법을 알게 되었습니다. 이 자습서에서는 설명 하는 방법 같은 TableAdapter...
ms.author: aspnetcontent
ms.date: 07/18/2007
ms.assetid: 440bef2a-1641-4238-99e3-8e2d44e7d94c
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs
msc.type: authoredcontent
ms.openlocfilehash: 3057b7c296c82b3db740d9fd345aaa222ca31328
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37828872"
---
<a name="using-existing-stored-procedures-for-the-typed-datasets-tableadapters-c"></a>기존 저장 프로시저 사용에 대 한 형식화 된 데이터 집합의 Tableadapter (C#)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_68_CS.zip) 또는 [PDF 다운로드](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/datatutorial68cs1.pdf)

> 이전 자습서에서 TableAdapter 마법사를 사용 하 여 새 저장된 프로시저를 생성 하는 방법을 알게 되었습니다. 이 자습서에서는 기존 저장된 프로시저 함께 동일한 TableAdapter 마법사를 사용 하는 방법을 알아봅니다. 데이터베이스에 새 저장된 프로시저를 수동으로 추가 하는 방법을 알아볼 것입니다.


## <a name="introduction"></a>소개

에 [이전 자습서](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) 형식화 된 데이터 집합의 Tableadapter를 구성 하 수 액세스 임시 보다는 SQL 문으로 저장된 프로시저를 사용 하는 방법에 대해 살펴보았습니다. 특히 TableAdapter 마법사에서 자동으로 이러한 저장된 프로시저를 만드는 방법을 살펴보았습니다. ASP.NET 2.0으로 레거시 응용 프로그램을 이식 하는 경우 또는 기존 데이터 모델을 해결 하는 ASP.NET 2.0 웹 사이트를 빌드할 때 데이터베이스에 이미 필요한 저장된 프로시저를 포함 하는 것이 경우가 있습니다. 또는 수동으로 또는 저장된 프로시저를 자동으로 생성 하는 TableAdapter 마법사 이외의 일부 도구를 통해 저장된 프로시저를 만들 수도 있습니다.

이 자습서에서는 기존 저장된 프로시저를 사용 하도록 TableAdapter를 구성 하는 방법을 살펴보겠습니다. Northwind 데이터베이스에 기본 제공 저장된 프로시저는 작은 집합이 있는 경우 이후도 살펴보겠습니다 Visual Studio 환경을 통해 데이터베이스에 새 저장된 프로시저를 수동으로 추가 하는 데 필요한 단계입니다. Let s 시작!

> [!NOTE]
> 에 [트랜잭션 내에서 데이터베이스 수정 내용을 래핑](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs.md) 자습서 트랜잭션을 지원 하도록 TableAdapter에 메서드를 추가 했습니다 (`BeginTransaction`, `CommitTransaction`등). 또는 트랜잭션 데이터 액세스 계층 코드를 수정 해야 하는 저장된 프로시저 내에서 완전히 관리할 수 있습니다. 이 자습서에서는 트랜잭션의 범위 내에서 저장된 프로시저의 문을 실행 하는 데 사용 하는 T-SQL 명령을 살펴봅니다.


## <a name="step-1-adding-stored-procedures-to-the-northwind-database"></a>1 단계: Northwind 데이터베이스에 저장된 프로시저에 추가

Visual Studio에서는 쉽게 데이터베이스에 새 저장된 프로시저를 추가 합니다. Let s의 모든 열을 반환 하는 Northwind 데이터베이스에 새 저장된 프로시저를 추가 합니다 `Products` 테이블에 있는 특정 `CategoryID` 값입니다. 서버 탐색기 창에서 해당 폴더-데이터베이스 다이어그램, 테이블, 뷰 등-표시 되도록 Northwind 데이터베이스를 확장 합니다. 이전 자습서에서 보았듯이 Stored Procedures 폴더에 데이터베이스 s 기존 저장된 프로시저를 포함 합니다. 새 저장된 프로시저를 추가 하려면 저장 프로시저 폴더를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 새 저장 프로시저 추가 옵션을 선택 합니다.


[![저장된 프로시저 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 저장된 프로시저를 추가 합니다.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image2.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image1.png)

**그림 1**: 저장 프로시저 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 저장 프로시저를 추가 ([큰 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image3.png))


그림 1에서 볼 수 있듯이 새 저장 프로시저 추가 옵션을 선택 하면 스크립트 창이 열립니다 Visual Studio에서 저장된 프로시저를 만드는 데 필요한 SQL 스크립트의 개요를 사용 하 여. 이 스크립트를 구체화 하지만 시점에서 저장된 프로시저에 추가할 데이터베이스를 실행 하는 합니다.

다음 스크립트를 입력 합니다.


[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample1.sql)]

이 스크립트를 실행 하는 경우 명명 된 Northwind 데이터베이스에 새 저장된 프로시저를 추가 `Products_SelectByCategoryID`합니다. 단일 입력된 매개 변수를 허용 하는이 저장된 프로시저 (`@CategoryID`, 형식 `int`) 하 고 일치 하는 이러한 제품에 대 한 필드를 모두 반환 `CategoryID` 값입니다.

이를 실행할 `CREATE PROCEDURE` 스크립트 및 데이터베이스에 저장된 프로시저를 추가, 도구 모음에서 저장 아이콘을 클릭 하거나 Ctrl + S를 누릅니다. 이렇게 한 후, Stored Procedures 폴더 새로 고침을 보여 주는 새로 만든 저장 프로시저입니다. 또한 창에서 스크립트의 미묘한 바뀝니다 `CREATE PROCEDURE dbo.Products_SelectProductByCategoryID` 하 `ALTER PROCEDURE` `dbo.Products_SelectProductByCategoryID`합니다. `CREATE PROCEDURE` 데이터베이스에 새 저장된 프로시저를 추가 하는 동안 `ALTER PROCEDURE` 기존 항목을 업데이트 합니다. 스크립트의 시작 부분에 변경 되었으므로 `ALTER PROCEDURE`, 입력 매개 변수 또는 SQL 문이 저장된 프로시저를 변경 및 저장 아이콘을 클릭 하면 이러한 변경 내용으로 저장된 프로시저를 업데이트 됩니다.

그림 2 표시 한 후 Visual Studio는 `Products_SelectByCategoryID` 저장된 프로시저가 저장 되었습니다.


[![저장된 프로시저 Products_SelectByCategoryID 데이터베이스에 추가 되었습니다.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image5.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image4.png)

**그림 2**:의 저장 프로시저 `Products_SelectByCategoryID` 데이터베이스에 추가 되었습니다 ([클릭 하 여 큰 이미지 보기](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image6.png))


## <a name="step-2-configuring-the-tableadapter-to-use-an-existing-stored-procedure"></a>2 단계: 기존 저장된 프로시저를 사용 하도록 TableAdapter를 구성 합니다.

이제는 `Products_SelectByCategoryID` 저장된 프로시저에 추가한 데이터베이스 concigure 메서드 중 하나를 호출 하면이 저장된 프로시저를 사용 하 여 데이터 액세스 계층 수입니다. 추가 특히를 `GetProducstByCategoryID(categoryID)` 메서드를를 `ProductsTableAdapter` 에 `NorthwindWithSprocs` 호출 하는 입력 데이터 집합은 `Products_SelectByCategoryID` 방금 만든 저장 프로시저.

열어서 시작 합니다 `NorthwindWithSprocs` 데이터 집합입니다. 마우스 오른쪽 단추로 클릭는 `ProductsTableAdapter` TableAdapter 쿼리 구성 마법사를 시작 하려면 쿼리 추가 선택 합니다. 에 [이전 자습서](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) 우리 회사에 새 저장된 프로시저를 만드는 TableAdapter가 하기로 했습니다. 그러나이 자습서에서는 하려는 새 TableAdapter 메서드는 기존 연결 `Products_SelectByCategoryID` 저장 프로시저입니다. 따라서 마법사가 첫 번째 단계에서 사용 하 여 기존 저장된 프로시저 옵션을 선택 하 고 클릭 합니다.


[![기존 저장된 프로시저 옵션 사용 선택](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image8.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image7.png)

**그림 3**: 사용 하 여 기존 프로시저 옵션을 선택 ([큰 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image9.png))


다음 화면 드롭 다운 목록을 채울 s 데이터베이스를 사용 하 여 저장된 프로시저를 제공 합니다. 저장된 프로시저를 선택 하는 입력된 매개 변수를 왼쪽 및 오른쪽 (있는 경우)를 반환 하는 데이터 필드를 나열 합니다. 선택 된 `Products_SelectByCategoryID` 저장 프로시저 목록에서 다음을 클릭 합니다.


[![선택 된 Products_SelectByCategoryID 저장 프로시저](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image11.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image10.png)

**그림 4**: 선택 된 `Products_SelectByCategoryID` 저장 프로시저 ([클릭 하 여 큰 이미지 보기](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image12.png))


다음 화면에서는 어떤 종류의 데이터는 저장된 프로시저에서 반환 하 고 대답을 여기 TableAdapter가 메서드에서 반환 되는 형식을 결정 합니다. 예를 들어 경우 테이블 형식 데이터가 반환 됩니다 나타내고 귀하는 메서드는 반환 된 `ProductsDataTable` 인스턴스는 저장된 프로시저에서 반환 된 레코드를 사용 하 여 채워집니다. 이와 달리이 저장된 프로시저는 단일 값을 반환 하는지를 나타내고 귀하 TableAdapter 반환 됩니다는 `object` 는 저장된 프로시저에서 반환 된 첫 번째 레코드의 첫 번째 열에 값이 할당 됩니다.

이후를 `Products_SelectByCategoryID` 저장된 프로시저는 특정 범주에 속하는 첫 번째 응답-표 형식 데이터를 선택 하 고 다음을 클릭 하는 모든 제품을 반환 합니다.


[![저장된 프로시저가 반환 테이블 형식 데이터를 나타냅니다.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image14.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image13.png)

**그림 5**:는 저장 프로시저가 반환 하는 테이블 형식 데이터를 나타냅니다 ([큰 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image15.png))


에 이러한 메서드의 이름을 뒤 메서드 패턴 사용을 나타냅니다. 두고 모두 채우기는 DataTable 반환 DataTable 옵션을 선택 하지만 메서드를 이름 바꾸기 `FillByCategoryID` 고 `GetProductsByCategoryID`입니다. 마법사가 수행할 작업의 요약을 검토 하려면 다음을 클릭 합니다. 모든 항목이 올바르면 마침을 클릭 합니다.


[![메서드 FillByCategoryID 이름과 GetProductsByCategoryID](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image17.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image16.png)

**그림 6**: 메서드 이름을 `FillByCategoryID` 하 고 `GetProductsByCategoryID` ([클릭 하 여 큰 이미지 보기](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image18.png))


> [!NOTE]
> 방금 만든 TableAdapter 메서드 `FillByCategoryID` 하 고 `GetProductsByCategoryID`, 형식 입력된 매개 변수를 예상 `int`합니다. 이 입력된 매개 변수 값을 통해 저장 프로시저로 전달 됩니다 해당 `@CategoryID` 매개 변수입니다. 수정 하는 경우는 `Products_SelectByCategory` 저장 프로시저 s 매개 변수 또한 이러한 TableAdapter 메서드 매개 변수를 업데이트 해야 합니다. 에 설명 된 대로 합니다 [이전 자습서](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md), 두 가지 방법 중 하나로이 작업을 수행할 수 있습니다: 수동으로 추가 하거나 제거 하 여 매개 변수 또는 매개 변수 컬렉션에서 TableAdapter 마법사를 다시 실행 하 여 합니다.


## <a name="step-3-adding-agetproductsbycategoryidcategoryidmethod-to-the-bll"></a>3 단계: 추가 된`GetProductsByCategoryID(categoryID)`BLL 방법

사용 하 여는 `GetProductsByCategoryID` DAL 메서드 완료를 다음 단계는 비즈니스 논리 계층에서이 메서드에 대 한 액세스를 제공 합니다. 열기는 `ProductsBLLWithSprocs` 클래스 파일 및 다음 메서드를 추가 합니다.


[!code-csharp[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample2.cs)]

이 BLL 메서드는 단순히 반환 합니다 `ProductsDataTable` 에서 반환 된 합니다 `ProductsTableAdapter` s `GetProductsByCategoryID` 메서드. `DataObjectMethodAttribute` 특성 ObjectDataSource가의 데이터 소스 구성 마법사에서 사용 하는 메타 데이터를 제공 합니다. 특히,이 메서드는 선택 탭의 드롭 다운 목록에 표시 됩니다.

## <a name="step-4-displaying-products-by-category"></a>4 단계: 범주별으로 제품 표시

새로 추가 된 테스트할 `Products_SelectByCategoryID` 저장된 프로시저 및 해당 BLL 및 DAL 메서드 s DropDownList 및 GridView를 포함 하는 ASP.NET 페이지를 만듭니다. DropDownList는 GridView는 선택한 범주에 속하는 제품을 표시 하는 동안 모든 데이터베이스에 범주가 나열 됩니다.

> [!NOTE]
> 우리가 만든 ve 마스터/세부 인터페이스 Dropdownlist를 사용 하 여 이전 자습서에서입니다. 마스터/세부 정보 보고서를 이러한 구현에 대 한 자세한 설명에 대 한 참조를 [마스터/세부 정보 필터링으로 DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) 자습서입니다.


엽니다는 `ExistingSprocs.aspx` 페이지에서 `AdvancedDAL` 폴더 및 디자이너 도구 상자에서 끌어서 DropDownList 합니다. 집합 DropDownList s `ID` 속성을 `Categories` 및 해당 `AutoPostBack` 속성을 `true`입니다. 다음으로, 스마트 태그를 바인딩할 DropDownList 라는 새로운 ObjectDataSource는 `CategoriesDataSource`합니다. 해당 데이터를 검색할 수 있도록 ObjectDataSource를 구성 합니다 `CategoriesBLL` s 클래스 `GetCategories` 메서드. UPDATE, INSERT에서에서 드롭 다운 목록을 설정 하 고 탭 (없음)를 삭제 합니다.


[![S CategoriesBLL 클래스 GetCategories 메서드에서 데이터를 검색 합니다.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image20.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image19.png)

**그림 7**: Retrieve Data from 합니다 `CategoriesBLL` s 클래스 `GetCategories` 메서드 ([클릭 하 여 큰 이미지 보기](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image21.png))


[![UPDATE, INSERT 드롭 다운 목록을 설정 하 고 탭 삭제 (없음)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image23.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image22.png)

**그림 8**: 드롭다운 목록에서 업데이트, 삽입 및 삭제 탭 하도록 설정 (없음) ([큰 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image24.png))


ObjectDataSource 마법사를 완료 한 후 표시할 DropDownList를 구성 합니다 `CategoryName` 데이터 필드 사용 하는 `CategoryID` 필드를 `Value` 각각에 대 한 `ListItem`.

이 시점에서 DropDownList 및 ObjectDataSource가 선언적 태그 해야 다음과 비슷합니다.


[!code-aspx[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample3.aspx)]

그런 다음 GridView를 디자이너로 끌어, DropDownList 아래에 배치 합니다. 집합 GridView s `ID` 하 `ProductsByCategory` 및 스마트 태그를 바인딩할 라는 새로운 ObjectDataSource는 `ProductsByCategoryDataSource`합니다. 구성 합니다 `ProductsByCategoryDataSource` ObjectDataSource 사용 하는 `ProductsBLLWithSprocs` 하는 클래스를 사용 하 여 해당 데이터를 검색 합니다 `GetProductsByCategoryID(categoryID)` 메서드. 데이터를 표시 하려면이 GridView 사용만 되므로 UPDATE, INSERT에서에서 드롭 다운 목록을 설정 및 탭 (없음)을 삭제 하 고 클릭 합니다.


[![ProductsBLLWithSprocs 클래스를 사용 하는 ObjectDataSource 구성](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image26.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image25.png)

**그림 9**: ObjectDataSource 사용 하도록 구성 된 `ProductsBLLWithSprocs` 클래스 ([클릭 하 여 큰 이미지 보기](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image27.png))


[![GetProductsByCategoryID(categoryID) 메서드에서 데이터를 검색 합니다.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image29.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image28.png)

**그림 10**: Retrieve Data from 합니다 `GetProductsByCategoryID(categoryID)` 메서드 ([클릭 하 여 큰 이미지 보기](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image30.png))


[선택] 탭에서 선택한 메서드에서 마법사의 마지막 단계에서는 매개 변수의 원본에 대 한 요청 하므로 매개 변수를 예상 합니다. 매개 변수 원본 드롭다운 목록 컨트롤에 설정 하 고 선택 된 `Categories` ControlID 드롭 다운 목록에서 제어 합니다. 마법사를 완료 하려면 마침을 클릭 합니다.


[![범주 DropDownList를 사용 하 여 categoryID 매개 변수 원본으로](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image32.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image31.png)

**그림 11**: 사용 합니다 `Categories` DropDownList의 원본으로는 `categoryID` 매개 변수 ([클릭 하 여 큰 이미지 보기](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image33.png))


ObjectDataSource 마법사를 완료 하면 Visual Studio가 BoundFields 및는 CheckBoxField 제품 데이터 필드에 대해 추가 합니다. 자유롭게 하다 면 이러한 필드를 사용자 지정할 수 있습니다.

브라우저를 통해 페이지를 방문 합니다. 경우 표에 나열 된 해당 제품과 음료 범주를 선택 하는 페이지를 방문 합니다. 그림 12로, 다른 범주에 드롭다운 목록을 변경, 포스트백을 발생 시키는 나타나며 새로 선택한 범주의 제품 표를 다시 로드 합니다.


[![제품 생성 범주에 표시 됩니다.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image35.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image34.png)

**그림 12**: 생성 범주에 있는 제품 표시 됩니다 ([큰 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image36.png))


## <a name="step-5-wrapping-a-stored-procedure-s-statements-within-the-scope-of-a-transaction"></a>5 단계: 트랜잭션 범위 내에서 저장된 프로시저의 문 배치

에 [트랜잭션 내에서 데이터베이스 수정 내용을 래핑](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs.md) 일련의 트랜잭션 범위 내에서 데이터베이스 수정 문 수행 하는 기술을 논의 하는 자습서입니다. 모두 성공 하거나 트랜잭션 산하 수행 수정 하는 재현 율 또는 원자성을 보장 하는 모든 실패 합니다. 트랜잭션 사용에 대 한 기술에는 다음이 포함 됩니다.

- 클래스를 사용 하 여 `System.Transactions` 네임 스페이스
- 과 같은 ADO.NET 클래스를 사용 하 여 데이터 액세스 계층을 가진 `SqlTransaction`, 및
- 저장된 프로시저 내에서 직접 T-SQL 트랜잭션 명령 추가

합니다 *트랜잭션 내에서 데이터베이스 수정 내용을 래핑* DAL에서 ADO.NET 클래스를 사용 하는 자습서입니다. 이 자습서의 나머지 부분에서는 저장된 프로시저 내에서 T-SQL 명령을 사용 하 여 트랜잭션을 관리 하는 방법을 검사 합니다.

수동으로 시작, 커밋 및 트랜잭션 롤백에 대 한 세 가지 주요 SQL 명령은 `BEGIN TRANSACTION`, `COMMIT TRANSACTION`, 및 `ROLLBACK TRANSACTION`, 각각. 다음 패턴을 적용 해야 하는 저장된 프로시저 내에서 트랜잭션을 사용 하 여 ADO.NET 방식의 경우 같은:

1. 트랜잭션 시작을 표시 합니다.
2. 트랜잭션을 구성 하는 SQL 문을 실행 합니다.
3. 2 단계에서 트랜잭션 롤백하고에서에서 문 중 하나에서 오류가 발생 하는 경우
4. 오류 없이 완료 단계 2에서 문의 모든 경우에 트랜잭션을 커밋하십시오.

다음 템플릿을 사용 하 여 T-SQL 구문에서이 패턴을 구현할 수 있습니다.


[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample4.sql)]

템플릿을 정의 하 여 시작을 `TRY...CATCH` 차단, SQL Server 2005로 새 구문입니다. 와 마찬가지로 `try...catch` C#에서 SQL 차단 `TRY...CATCH` 블록에서 문을 실행 합니다 `TRY` 블록입니다. 문일에서 오류가 발생 하면 즉시 제어가 이동 하 여 `CATCH` 블록.

해당 구성의 트랜잭션을 SQL 문을 실행 하는 오류가 없는 경우는 `COMMIT TRANSACTION` 문을 변경 내용을 커밋하고 트랜잭션을 완료 합니다. 하지만 오류가 발생 결과 문 중 하나는 경우는 `ROLLBACK TRANSACTION` 에서 `CATCH` 블록 트랜잭션의 시작 하기 전에 해당 상태로 데이터베이스를 반환 합니다. 저장된 프로시저를 사용 하 여 오류를 발생 합니다 [RAISERROR 명령을](https://msdn.microsoft.com/library/ms178592.aspx), 유발 하는 `SqlException` 응용 프로그램에서 발생 합니다.

> [!NOTE]
> 이후를 `TRY...CATCH` 블록은 새 SQL Server 2005로, 이전 버전의 Microsoft SQL Server를 사용 하는 경우에 위의 템플릿이 작동 하지 것입니다. SQL Server 2005를 사용 하지 않는 경우를 참조 하세요 [SQL Server 저장 프로시저에서 트랜잭션을 관리](http://www.4guysfromrolla.com/webtech/080305-1.shtml) 다른 버전의 SQL Server를 사용 하 여 작동 하는 템플릿에 대 한 합니다.


S를 구체적인 예제를 살펴볼 수 있습니다. 외래 키 제약 조건 사이 존재 합니다 `Categories` 및 `Products` 테이블, 즉 각 `CategoryID` 필드에 `Products` 테이블에 매핑해야 합니다.는 `CategoryID` 값는 `Categories` 테이블. 같은 제품에 연결 된 범주를 삭제 하는 동안이 제약 조건을 위반 하는 모든 작업은 foreign key 제약 조건 위반 하 게 발생 합니다. 이 확인 하려면 이진 데이터 섹션을 사용 하 여 작업에서 업데이트 및 삭제 기존 이진 데이터 예제를 다시 방문 (`~/BinaryData/UpdatingAndDeleting.aspx`). 이 페이지 (그림 13 참조) 편집 및 삭제 단추와 함께 시스템의 각 범주에 나열 하지만 삭제는 foreign key 제약 조건 위반으로 인해 실패 음료-등의 제품-연결 된 범주를 삭제 하려고 하면 (그림 14 참조).


[![각 범주는 편집 및 삭제 단추를 사용 하 여 GridView에 표시 됩니다.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image38.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image37.png)

**그림 13**: 각 범주는 편집 및 삭제 단추를 사용 하 여 GridView에 표시 됩니다 ([큰 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image39.png))


[![기존 제품에는 범주를 삭제할 수 없습니다.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image41.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image40.png)

**그림 14**: 기존 제품에는 범주를 삭제할 수 없습니다 ([큰 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image42.png))


그러나 범주 제품 연결 여부에 관계 없이 삭제할 수 있도록 한다고 가정해 보겠습니다. 제품 범주 삭제도 기존 제품을 삭제 한다고 가정해 보겠습니다 (다른 옵션은 단순히 해당 제품을 설정 하는 것 이지만 `CategoryID` 값을 `NULL`). 외래 키 제약 조건의 cascade 규칙을 통해이 기능을 구현할 수 있습니다. 또는 허용 하는 저장된 프로시저를 만들 수는 `@CategoryID` 입력된 매개 변수를 호출 하면 명시적으로 삭제 합니다. 모든 연결 된 제품 및 다음 지정된 된 범주를 합니다.

이러한 저장된 프로시저는 첫 번째 시도 다음과 같습니다.


[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample5.sql)]

관련된 제품 및 범주를 확실 하 게 삭제 됩니다을 하는 동안이 그렇게 할 수 없습니다 트랜잭션의 산하 합니다. 일부 다른 외래 키 제약 조건 인지 imagine `Categories` 특정의 삭제를 못하도록 하는 `@CategoryID` 값입니다. 이 경우 모든 제품 삭제 될 것 이라는 범주를 삭제 하기 전에 문제가입니다. 결과 이러한 범주에 대 한이 저장된 프로시저는 제거는 모든 제품 범주가 여전히에 관련 된 일부 다른 테이블의 레코드를 유지 하는 동안.

그러나 저장된 프로시저 된 래핑되지 경우 트랜잭션의 범위 내에서를 삭제 합니다 `Products` 테이블 롤백되지 실패 한 삭제 제시간 `Categories`입니다. 다음 저장된 프로시저 스크립트를 두 간의 원자성을 보장 하려면 트랜잭션을 사용 `DELETE` 문:


[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample6.sql)]

추가할 잠시는 `Categories_Delete` 저장 프로시저를 Northwind 데이터베이스입니다. 데이터베이스에 저장된 프로시저를 추가 하는 방법은 1 단계를 다시 참조 합니다.

## <a name="step-6-updating-thecategoriestableadapter"></a>6 단계: 업데이트를`CategoriesTableAdapter`

Ve 동안 추가 `Categories_Delete` DAL 데이터베이스에 저장된 프로시저는 임시 SQL 문을 사용 하 여 삭제를 수행 하도록 현재 구성 되어 있습니다. 업데이트 해야 합니다 `CategoriesTableAdapter` 하 고 사용 하도록 지시 하는 `Categories_Delete` 저장 프로시저를 대신 합니다.

> [!NOTE]
> 이 자습서의 앞부분에서 사용 하 여 작업을 `NorthwindWithSprocs` 데이터 집합입니다. 단일 엔터티를만 집합이 없는 `ProductsDataTable`, 범주를 사용 해야 합니다. 따라서 참조 데이터 액세스 계층 I m을 이야기할 때이 자습서의 나머지 부분에 대 한 합니다 `Northwind` 데이터 집합에서 처음 만든 것을 [데이터 액세스 레이어 만들기](../introduction/creating-a-data-access-layer-cs.md) 자습서.


열기 Northwind 데이터 집합을 선택 합니다 `CategoriesTableAdapter`, 속성 창으로 이동 합니다. 속성 창 목록을 합니다 `InsertCommand`, `UpdateCommand`를 `DeleteCommand`, 및 `SelectCommand` 해당 이름 및 연결 정보 뿐만 아니라 TableAdapter를 사용 합니다. 확장을 `DeleteCommand` 속성을 해당 세부 정보를 참조 하세요. 그림 15와 같이 `DeleteCommand` s `ComamndType` 텍스트를 보내도록 지시 하는 텍스트 속성을 `CommandText` 임시 SQL 쿼리로 속성.


![속성 창에서 해당 속성을 보려면 디자이너에서의 CategoriesTableAdapter 선택](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image43.png)

**그림 15**: 선택 된 `CategoriesTableAdapter` 속성 창에서 해당 속성을 보려면 디자이너에서


이러한 설정을 변경 하려면 속성 창에서 (DeleteCommand) 텍스트를 선택 하 고 드롭다운 목록에서 (새로 만들기)를 선택 합니다. 에 대 한 설정을 지웁니다 합니다 `CommandText`, `CommandType`, 및 `Parameters` 속성입니다. 다음으로 설정 합니다 `CommandType` 속성을 `StoredProcedure` 저장된 프로시저에 대 한 이름을 입력 하 고는 `CommandText` (`dbo.Categories_Delete`). 먼저 순에서 속성을 입력 해야 하는 경우는 `CommandType` 차례로 `CommandText` -Visual Studio에서 매개 변수 컬렉션을 자동으로 채워집니다. 이러한 속성에이 순서를 입력 하지 않으면를 사용 하는 경우에 수동으로 매개 변수 컬렉션 편집기를 통해 매개 변수를 추가 합니다. 두 경우 모두 해당 s (그림 16 참조)는 올바른 매개 변수 설정을 변경 내용이 있는지 확인 하는 매개 변수 컬렉션 편집기를 표시 하려면 매개 변수 속성의 줄임표를 클릭 하는 것이 좋습니다. 대화 상자에서 매개 변수를 표시 되지 않으면 추가 합니다 `@CategoryID` 매개 변수 수동으로 (추가할 필요가 없습니다를 `@RETURN_VALUE` 매개 변수).


![매개 변수 설정이 올바른지 확인 합니다.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image44.png)

**그림 16**: 매개 변수 설정이 올바른지 확인 합니다.


DAL를 업데이트 하면 범주를 삭제 하면 자동으로 모든 연결 된 제품 삭제를 트랜잭션의 산하 이렇게 합니다. 이 확인 하려면 업데이트 및 삭제 하면 기존 이진 데이터 페이지로 반환 하 고 범주 중 하나에 대 한 삭제 단추를 클릭 합니다. 한 번의 클릭으로 마우스의 범주와 모든 연결 된 제품 삭제 됩니다.

> [!NOTE]
> 테스트 하기 전에 `Categories_Delete` 저장된 프로시저는 선택한 범주와 제품을 삭제 하는 것이 좋습니다 데이터베이스의 백업 복사본. 사용 중인 경우는 `NORTHWND.MDF` 데이터베이스에 `App_Data`, 단순히 Visual Studio를 닫고의 MDF 및 LDF 파일을 복사 `App_Data` 다른 폴더로 합니다. 기능을 테스트 한 후 Visual Studio를 닫으면 데이터베이스를 복원할 수 및 현재 MDF 및 LDF 대체 파일 `App_Data` 백업 복사본을 사용 합니다.


## <a name="summary"></a>요약

TableAdapter가의 마법사는 자동으로 우리 회사에 저장된 프로시저를 생성 하지만, 경우에서는 이미 만든 이러한 저장된 프로시저가 있는 수도 만들고 수동으로 또는 다른 도구를 사용 하 여 대신 경우가 있습니다. 이러한 시나리오를 수용할 수 있도록 TableAdapter 기존 저장된 프로시저를 가리키도록 구성할 수도 있습니다. 이 자습서에서는 Visual Studio 환경을 통해 데이터베이스에 저장된 프로시저를 수동으로 추가 하는 방법 및 이러한 저장된 프로시저를 TableAdapter가의 메서드를 연결 하는 방법을 살펴보았습니다. 에서는 T-SQL 명령 및 스크립트 패턴 시작, 커밋 및 저장된 프로시저 내에서 트랜잭션을 롤백하는 데에 검사 합니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Hilton Geisenow, S ren Jacob Lauritsen 및 Teresa Murphy 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)
> [다음](updating-the-tableadapter-to-use-joins-cs.md)
