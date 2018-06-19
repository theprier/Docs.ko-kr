---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs
title: 저장 프로시저의 이름을 형식화 된 데이터 집합의 Tableadapter (C#)에 대 한 기존 사용 | Microsoft Docs
author: rick-anderson
description: 이전 자습서에서는 TableAdapter 마법사를 사용 하 여 새 저장된 프로시저를 생성 하는 방법을 배웠습니다. 이 자습서에서는 배울 방법 같은 TableAdapter...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/18/2007
ms.topic: article
ms.assetid: 440bef2a-1641-4238-99e3-8e2d44e7d94c
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs
msc.type: authoredcontent
ms.openlocfilehash: df8a714325ce99db615eddc3d457da5c926919ba
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30877075"
---
<a name="using-existing-stored-procedures-for-the-typed-datasets-tableadapters-c"></a>형식화 된 데이터 집합의 Tableadapter (C#)에 대 한 기존 사용 하 여 저장 프로시저
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_68_CS.zip) 또는 [PDF 다운로드](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/datatutorial68cs1.pdf)

> 이전 자습서에서는 TableAdapter 마법사를 사용 하 여 새 저장된 프로시저를 생성 하는 방법을 배웠습니다. 이 자습서에서는 같은 TableAdapter 마법사는 기존 저장된 프로시저 함께 사용 하는 방법을 알아봅니다. 우리는 또한 데이터베이스에 새 저장된 프로시저를 수동으로 추가 하는 방법을 알아봅니다.


## <a name="introduction"></a>소개

에 [이전 자습서](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) 액세스 임시 보다는 SQL 문으로 저장된 프로시저를 사용 하는 형식화 된 데이터 집합의 Tableadapter 구성 방법에 대해 살펴보았습니다. 특히, 이러한 저장된 프로시저를 자동으로 만들 TableAdapter 마법사 하는 방법을 검사 했습니다. ASP.NET 2.0으로 레거시 응용 프로그램을 이식 하는 경우 또는 기존 데이터 모델 주위에서 ASP.NET 2.0 웹 사이트를 만들 때 가능성이 필요한 저장된 프로시저에 데이터베이스에 이미 포함 간주 됩니다. 수동으로 또는 자동 생성 저장된 프로시저를 TableAdapter 마법사 이외의 일부 도구를 통해 저장된 프로시저를 만들려고 할 수도 있습니다.

이 자습서에서는 기존 저장된 프로시저를 사용 하 여 TableAdapter를 구성 하는 방법을 살펴보겠습니다. Northwind 데이터베이스에 기본 제공 저장된 프로시저 중 작은 부분만 있는 경우 이후도 살펴보도록 하겠습니다 Visual Studio 환경을 통해 데이터베이스에 새 저장된 프로시저를 수동으로 추가 하는 데 필요한 단계. Let s가 시작 되었습니다.

> [!NOTE]
> 에 [트랜잭션 내에서 데이터베이스 수정 내용을 래핑](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs.md) 트랜잭션을 지원 하기 위해 TableAdapter에 메서드 추가 자습서 (`BeginTransaction`, `CommitTransaction`등). 또는 트랜잭션 내에 데이터 액세스 계층 코드를 수정 하지 않고도 저장된 프로시저를 완전히 관리할 수 있습니다. 이 자습서는 트랜잭션의 범위 내에서 저장된 프로시저의 문을 실행 하는 데 T-SQL 명령을 살펴보겠습니다.


## <a name="step-1-adding-stored-procedures-to-the-northwind-database"></a>1 단계: Northwind 데이터베이스에 저장된 프로시저에 추가

Visual Studio에서는 쉽게 데이터베이스에 새 저장된 프로시저를 추가할 수 있습니다. Let s 모든 열을 반환 하는 Northwind 데이터베이스에 새 저장된 프로시저를 추가할는 `Products` 테이블에 특정 한 `CategoryID` 값입니다. 서버 탐색기 창에서 표시 되는 해당 폴더-데이터베이스 다이어그램, 테이블, 뷰 및 기타-되도록 Northwind 데이터베이스를 확장 합니다. 이전 자습서에서 살펴본 것 처럼 Stored Procedures 폴더에 데이터베이스 s 기존의 저장된 프로시저를 포함 합니다. 새 저장된 프로시저를 추가 하려면 저장 프로시저 폴더를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 새 저장 프로시저 추가 옵션을 선택 합니다.


[![저장된 프로시저 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 저장된 프로시저를 추가 합니다.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image2.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image1.png)

**그림 1**: 저장 프로시저 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 저장 프로시저 추가 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image3.png))


그림 1 에서처럼 새 저장 프로시저 추가 옵션을 선택 하면 스크립트 창을 엽니다. Visual Studio에서 저장된 프로시저를 만드는 데 필요한 SQL 스크립트의 윤곽을 합니다. 것은 우리의 임무가이 스크립트를 구체화 하 고 나중에 실행 이때 저장된 프로시저가 데이터베이스에 추가 됩니다.

다음 스크립트를 입력 합니다.


[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample1.sql)]

이 스크립트를 실행 하면 명명 된 Northwind 데이터베이스에 새 저장된 프로시저를 추가 합니다 `Products_SelectByCategoryID`합니다. 이 저장된 프로시저는 단일 입력된 매개 변수 (`@CategoryID`, 형식의 `int`) 하 고 일치 하는 해당 제품에 대 한 필드를 모두 반환 `CategoryID` 값입니다.

이를 실행할 `CREATE PROCEDURE` 스크립트 및 데이터베이스에 저장된 프로시저에 추가 하 고 도구 모음에서 저장 아이콘을 클릭 하거나 Ctrl + S를 적중 합니다. 그런 다음, Stored Procedures 폴더 새로 고쳐지고 새로 만든 보여 주는 저장 프로시저입니다. 또한 창에서 스크립트에서 미묘한 바뀝니다 `CREATE PROCEDURE dbo.Products_SelectProductByCategoryID` 를 `ALTER PROCEDURE` `dbo.Products_SelectProductByCategoryID`합니다. `CREATE PROCEDURE` 새 저장된 프로시저를 데이터베이스에 추가 하는 동안 `ALTER PROCEDURE` 기존을 업데이트 합니다. 스크립트의 시작에 변경 되었으므로 `ALTER PROCEDURE`, 입력 매개 변수 또는 SQL 문이 저장된 프로시저를 변경 하 고 저장 아이콘을 클릭 하면 이러한 변경 내용으로 저장된 프로시저를 업데이트 합니다.

그림 2에 표시 한 후 Visual Studio는 `Products_SelectByCategoryID` 저장된 프로시저를 저장 합니다.


[![데이터베이스에 추가 된 저장된 프로시저 Products_SelectByCategoryID](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image5.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image4.png)

**그림 2**: 저장 프로시저의 `Products_SelectByCategoryID` 데이터베이스에 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image6.png))


## <a name="step-2-configuring-the-tableadapter-to-use-an-existing-stored-procedure"></a>2 단계: 기존 저장된 프로시저를 사용 하려면 TableAdapter를 구성 합니다.

이제는 `Products_SelectByCategoryID` 저장된 프로시저에 추가한 데이터베이스를 활용해 서 concigure 메서드 중 하나를 호출 하면이 저장된 프로시저를 사용 하도록 데이터 액세스 계층입니다. 특히, 추가 합니다는 `GetProducstByCategoryID(categoryID)` 메서드를는 `ProductsTableAdapter` 에 `NorthwindWithSprocs` 를 호출 하는 형식화 된 데이터 집합의 `Products_SelectByCategoryID` 방금 만든 저장 프로시저입니다.

열어 시작는 `NorthwindWithSprocs` 데이터 집합입니다. 마우스 오른쪽 단추로 클릭는 `ProductsTableAdapter` TableAdapter 쿼리 구성 마법사를 시작 하려면 추가 쿼리를 선택 합니다. 에 [이전 자습서](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) us에 대 한 새 저장된 프로시저를 만드는 TableAdapter가 하기로 선택 했습니다. 그러나이 자습서에서는 우리를 연결 하 려 새 TableAdapter 메서드를 기존 `Products_SelectByCategoryID` 저장 프로시저입니다. 따라서 마법사 s 첫 번째 단계에서 사용 하 여 기존 저장된 프로시저 옵션을 선택 하 고 클릭 합니다.


[![기존 저장된 프로시저 옵션 사용](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image8.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image7.png)

**그림 3**: 저장 된 프로시저 옵션을 사용 하 여 기존 선택 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image9.png))


다음 화면이 드롭 다운 목록 채워진 s 데이터베이스 저장된 프로시저를 제공 합니다. 저장된 프로시저를 선택 하 고 왼쪽 및 오른쪽 (있는 경우)를 반환 하는 데이터 필드에 입력된 매개 변수를 나열 합니다. 선택 된 `Products_SelectByCategoryID` 저장 프로시저 목록에서 다음을 클릭 합니다.


[![선택 된 Products_SelectByCategoryID 저장 프로시저](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image11.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image10.png)

**그림 4**: 선택 된 `Products_SelectByCategoryID` 저장 프로시저 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image12.png))


다음 화면에서는 어떤 종류의 데이터가 저장된 프로시저에서 반환 하 고 여기에 대답 TableAdapter의 메서드에 의해 반환 되는 형식을 결정 합니다. 예를 들어 테이블 형식 데이터가 반환 됩니다을 나타낼 경우 메서드는 반환 된 `ProductsDataTable` 저장된 프로시저에서 반환 되는 레코드도 채워진 인스턴스. 이와 달리이 저장된 프로시저는 단일 값을 반환 하는지을 나타내는 경우 TableAdapter 반환 됩니다는 `object` 하는 저장된 프로시저에서 반환 된 첫 번째 레코드의 첫 번째 열에 값을 할당 합니다.

이후는 `Products_SelectByCategoryID` 저장된 프로시저는 특정 범주에 속하는-테이블 형식 데이터-첫 번째 응답을 선택 하 고 다음을 클릭 하는 모든 제품을 반환 합니다.


[![저장된 프로시저 테이블 형식 데이터를 반환 하는지 나타냅니다.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image14.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image13.png)

**그림 5**: 저장 프로시저 테이블 형식 데이터를 반환 하는지 나타냅니다 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image15.png))


이제 남은 것 이러한 방법에 대 한 이름 이어서 메서드를 사용 하는 패턴을 나타냅니다. 와 그대로 둘 모두 채우기는 DataTable 반환 DataTable 옵션 확인 되지만 하는 메서드 이름 바꾸기 `FillByCategoryID` 및 `GetProductsByCategoryID`합니다. 마법사가 수행할 태스크의 요약을 검토 하려면 다음을 클릭 합니다. 잘못 된 항목이, 마침을 클릭 합니다.


[![메서드 FillByCategoryID 이름과 GetProductsByCategoryID](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image17.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image16.png)

**그림 6**: 메서드 이름을 `FillByCategoryID` 및 `GetProductsByCategoryID` ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image18.png))


> [!NOTE]
> TableAdapter 메서드, 방금 만든 `FillByCategoryID` 및 `GetProductsByCategoryID`, 형식의 입력된 매개 변수를 기대 `int`합니다. 이 입력된 매개 변수 값을 통해 저장된 프로시저에 전달 되는 `@CategoryID` 매개 변수입니다. 수정 하는 경우는 `Products_SelectByCategory`의 프로시저 매개 변수를 저장 합니다. 또한 이러한 TableAdapter 메서드는 매개 변수를 업데이트 해야 합니다. 에 설명 된 대로 [이전 자습서](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md), 두 가지 방법 중 하나에서이 작업을 수행할 수 있습니다: 수동으로 추가 하거나 제거 하 여 매개 변수 또는 매개 변수 컬렉션에서 TableAdapter 마법사를 다시 실행 하 여 합니다.


## <a name="step-3-adding-agetproductsbycategoryidcategoryidmethod-to-the-bll"></a>3 단계: 추가 된`GetProductsByCategoryID(categoryID)`BLL 메서드

와 `GetProductsByCategoryID` DAL 완료를 다음 단계 하는 메서드가 비즈니스 논리 계층에서이 메서드에 대 한 액세스를 제공 합니다. 열기는 `ProductsBLLWithSprocs` 클래스 파일을 다음 메서드를 추가 합니다.


[!code-csharp[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample2.cs)]

이 BLL 메서드는 단순히 반환는 `ProductsDataTable` 에서 반환 되는 `ProductsTableAdapter` s `GetProductsByCategoryID` 메서드. `DataObjectMethodAttribute` 특성은 ObjectDataSource의 데이터 소스 구성 마법사에서 사용 하는 메타 데이터를 제공 합니다. 특히,이 메서드는 선택 탭의 드롭 다운 목록에 표시 됩니다.

## <a name="step-4-displaying-products-by-category"></a>4 단계: 범주별으로 제품 표시

새로 추가 된 테스트 하려면 `Products_SelectByCategoryID` 저장된 프로시저와 해당 DAL 및 BLL 메서드는 경우 s DropDownList 및는 GridView 포함 된 ASP.NET 페이지를 만듭니다. GridView에 선택한 범주에 속하는 제품이 표시 됩니다 하는 동안 DropDownList 모든 데이터베이스에 대 한 범주 나열 됩니다.

> [!NOTE]
> 여기서 만든 했습니다 마스터/세부 인터페이스 dropdownlist 활용 이전 자습서에서 사용 하 여 합니다. 구현 하는 이러한 마스터/세부 정보 보고서에 대 한 자세한 설명에 대 한 참조는 [마스터/세부 정보 필터링 된 정도 DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) 자습서입니다.


열기는 `ExistingSprocs.aspx` 페이지에 `AdvancedDAL` 폴더와 디자이너 도구 상자에서 끌어서 DropDownList 합니다. DropDownList s 설정 `ID` 속성을 `Categories` 및 해당 `AutoPostBack` 속성을 `true`합니다. 다음으로, 스마트 태그를 바인딩할 DropDownList 라는 새 ObjectDataSource `CategoriesDataSource`합니다. 구성에서 해당 데이터를 검색 하는 ObjectDataSource는 `CategoriesBLL` s 클래스 `GetCategories` 메서드. 삽입, 업데이트에서 드롭 다운 목록을 설정 하 고 각 탭 (없음)을 삭제 합니다.


[![CategoriesBLL 클래스의 GetCategories 메서드에서 데이터를 검색 합니다.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image20.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image19.png)

**그림 7**: Retrieve Data from는 `CategoriesBLL` s 클래스 `GetCategories` 메서드 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image21.png))


[![삽입, 업데이트에서 드롭 다운 목록을 설정 하 고 탭 (없음)를 삭제](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image23.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image22.png)

**그림 8**: 드롭 다운 목록에서 업데이트, 삽입 및 삭제 탭 하도록 설정 (None) ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image24.png))


ObjectDataSource 마법사를 완료 한 후 표시할 DropDownList를 구성는 `CategoryName` 데이터 필드 및 사용 하는 `CategoryID` 필드는 `Value` 각각에 대해 `ListItem`합니다.

이 시점에서 DropDownList 및 ObjectDataSource s 선언적 태그는 다음과 유사 해야합니다.


[!code-aspx[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample3.aspx)]

다음으로 GridView 디자이너로 끌어, 드롭다운 목록 아래에 배치 하는 것입니다. GridView s 설정 `ID` 를 `ProductsByCategory` 및 스마트 태그를 바인딩할 라는 새 ObjectDataSource `ProductsByCategoryDataSource`합니다. 구성에서 `ProductsByCategoryDataSource` ObjectDataSource 사용 하는 `ProductsBLLWithSprocs` 하도록 클래스를 사용 하 여 해당 데이터를 검색에서 `GetProductsByCategoryID(categoryID)` 메서드. 데이터를 표시 하려면이 GridView 사용만 되므로 삽입, 업데이트에서 드롭 다운 목록을 설정 하 고 탭 (없음)을 삭제 하 고 클릭 합니다.


[![ObjectDataSource ProductsBLLWithSprocs 클래스를 사용 하도록 구성](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image26.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image25.png)

**그림 9**: 구성에 사용 하 여 ObjectDataSource는 `ProductsBLLWithSprocs` 클래스 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image27.png))


[![GetProductsByCategoryID(categoryID) 메서드에서 데이터를 검색 합니다.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image29.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image28.png)

**그림 10**: Retrieve Data from는 `GetProductsByCategoryID(categoryID)` 메서드 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image30.png))


마법사의 마지막 단계 라는 메시지가 나타납니다에 대 한 매개 변수의 소스 되므로, 매개 변수를 기대 하는 선택 탭에서 선택한 방법입니다. 매개 변수 소스 드롭 다운 목록 컨트롤에 설정 하 고 선택 된 `Categories` ControlID 드롭 다운 목록에서 제어 합니다. 마법사를 완료 하려면 마침을 클릭 합니다.


[![매개 변수 categoryID의 소스로 범주 DropDownList를 사용 하 여](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image32.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image31.png)

**그림 11**: 사용 된 `Categories` DropDownList의 소스로 `categoryID` 매개 변수 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image33.png))


ObjectDataSource 마법사를 완료 되 면 Visual Studio가 BoundFields 및는 CheckBoxField 각 제품 데이터 필드에 대 한 추가 합니다. 자유롭게 보시기 이러한 필드를 사용자 지정할 수 있습니다.

브라우저를 통해 페이지를 방문 합니다. 음료 범주를 선택 하는 페이지 및 표에 나열 된 해당 제품을 방문할 때 그림 12는 다른 범주에 드롭다운 목록을 변경, 포스트백 보여주며, 새로 선택한 범주의 제품이 포함 된 표를 다시 로드 합니다.


[![생성할 범주의 제품 표시](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image35.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image34.png)

**그림 12**: The 제품 생성 범주에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image36.png))


## <a name="step-5-wrapping-a-stored-procedure-s-statements-within-the-scope-of-a-transaction"></a>5 단계: 트랜잭션 범위 내에서 저장된 프로시저의 문은 래핑

에 [트랜잭션 내에서 데이터베이스 수정 내용을 래핑](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs.md) 자습서 일련의 트랜잭션 범위 내에서 데이터베이스 수정 문 수행 하기 위한 기술에 설명 했습니다. 모두 성공 하거나 트랜잭션의 포괄적인 아래 수행 수정 회수 또는 원자성을 보장 하는 모든 실패 합니다. 트랜잭션을 사용 하기 위한 기술은 다음과 같습니다.

- 클래스를 사용 하 여 `System.Transactions` 네임 스페이스
- 와 같은 ADO.NET 클래스를 사용 하 여 데이터 액세스 계층에 있는 `SqlTransaction`, 및
- 저장된 프로시저 내에서 직접 T-SQL 트랜잭션 명령 추가

*트랜잭션 내에서 데이터베이스 수정 내용을 래핑* 자습서 DAL에서 ADO.NET 클래스를 사용 합니다. 이 자습서의 나머지 부분에서는 저장된 프로시저 내에서 T-SQL 명령을 사용 하 여 트랜잭션을 관리 하는 방법을 검사 합니다.

세 가지 주요 SQL 명령은 수동으로 시작, 커밋 및 트랜잭션을 롤백하면 `BEGIN TRANSACTION`, `COMMIT TRANSACTION`, 및 `ROLLBACK TRANSACTION`각각. 다음 패턴을 적용 해야 하는 저장된 프로시저 내에서 트랜잭션을 사용 하 여 ADO.NET 접근 방식으로 선택 합니다.

1. 트랜잭션의 시작을 표시 합니다.
2. 트랜잭션을 구성 하는 SQL 문을 실행 합니다.
3. 2 단계에서 트랜잭션 롤백하고에서에서 문 중 하나에서 오류가 발생 하는 경우
4. 오류 없이 완료 모든 2 단계에서에서 문을 경우 트랜잭션을 커밋하십시오.

다음 템플릿을 사용 하 여 T-SQL 구문에이 패턴을 구현할 수 있습니다.


[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample4.sql)]

서식 파일을 정의 하 여 시작 되는 `TRY...CATCH` 차단, SQL Server 2005를 처음 사용 하는 구문입니다. 와 함께 `try...catch` C#으로 SQL 블록 `TRY...CATCH` 블록의 문은 실행의 `TRY` 블록입니다. 모든 문은 오류가 발생 하면 즉시 제어가 이동 하는 `CATCH` 블록입니다.

해당 구성의 트랜잭션을 SQL 문을 실행 오류가 없는 경우는 `COMMIT TRANSACTION` 변경 내용을 커밋하면 문과 트랜잭션을 완료 합니다. 그러나 하면 오류가 발생 문 중 하나는 경우는 `ROLLBACK TRANSACTION` 에 `CATCH` 블록에 트랜잭션의 시작 이전의 상태로 데이터베이스를 반환 합니다. 저장된 프로시저도 사용 하 여 오류를 발생는 [RAISERROR 명령](https://msdn.microsoft.com/library/ms178592.aspx), 유발 하는 한 `SqlException` 응용 프로그램에서 발생 합니다.

> [!NOTE]
> 이후는 `TRY...CATCH` 블록은 새로운 SQL Server 2005, 이전 버전의 Microsoft SQL Server를 사용 하는 경우에 위의 템플릿이 작동 하지 것입니다. SQL Server 2005를 사용 하지 않는 경우 참조 [SQL Server 저장 프로시저에서 트랜잭션을 관리](http://www.4guysfromrolla.com/webtech/080305-1.shtml) SQL Server의 다른 버전과 함께 작동 하는 서식 파일에 대 한 합니다.


구체적인 예를 살펴 s를 사용 합니다. 외래 키 제약 조건 사이 존재는 `Categories` 및 `Products` 테이블, 즉 각 `CategoryID` 필드에 `Products` 테이블에 매핑되어야 합니다.는 `CategoryID` 값에 `Categories` 테이블입니다. 제품에 연결 된 범주를 삭제 하는 등이 제약 조건을 위반 하는 모든 작업을 외래 키 제약 조건 위반 하 게 발생 합니다. 이 확인 하려면 이진 데이터 섹션으로 작업의 업데이트 및 삭제 기존 이진 데이터 예제를 다시 확인 (`~/BinaryData/UpdatingAndDeleting.aspx`). 이 페이지 (그림 13 참조) 편집 및 삭제 단추와 함께 시스템에서 각 범주에 나열 되지만 음료-등의 제품-연결 된 범주를 삭제 하려고 하면 삭제가 외래 키 제약 조건 위반으로 인해 실패 (그림 14 참조).


[![각 범주는 편집 및 삭제 단추가 있는 GridView에 표시 됩니다.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image38.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image37.png)

**그림 13**: 각 범주는 편집 및 삭제 단추가 있는 GridView에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image39.png))


[![기존 제품 범주를 삭제할 수 없습니다.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image41.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image40.png)

**그림 14**: 기존 제품 범주를 삭제할 수 없습니다 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image42.png))


그러나 제품을 연결 했는지 여부에 관계 없이 삭제할 범주를 허용 한다고 가정해 보세요. 제품 범주를 삭제할 수, 기존 제품 삭제 하려고 (또 다른 옵션의 제품을 설정 하기만 하는 것 이지만 `CategoryID` 값을 `NULL`). 외래 키 제약 조건의 cascade 규칙을 통해이 기능을 구현할 수 있습니다. 또는 허용 하는 저장된 프로시저를 만들 수 있습니다는 `@CategoryID` 입력된 매개 변수 및 호출 되 면 명시적으로 삭제 모든 연결 된 제품 및 지정된 된 범주입니다.

첫 번째 작업에서 이러한 저장된 프로시저는 다음과 같을 수 있습니다.


[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample5.sql)]

확실 하 게 관련된 제품 및 범주 삭제 됩니다, 동안 것 이렇게 하지 않으면 트랜잭션 포괄적인 아래 합니다. 몇 가지 다른 외래 키 제약 조건을 `Categories` 특정의 삭제를 못하도록 하는 `@CategoryID` 값입니다. 이 경우 모든 제품 삭제 될 것 이라는 범주를 삭제 하기 전에 문제가입니다. 결과 이러한 범주에 대 한이 저장된 프로시저는 모두 제거 제품 범주 것 여전히에 관련 된 다른 테이블의 레코드를 유지 하는 동안 되었습니다.

그러나 저장된 프로시저 된 래핑되는 트랜잭션의 범위 내에서를 삭제 하는 경우는 `Products` 테이블은에서 다시 롤백되며 실패 한 삭제 한 경우에도 `Categories`합니다. 다음 저장된 프로시저 스크립트 두 간의 원자성을 보장 하려면 트랜잭션을 사용 `DELETE` 문:


[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/samples/sample6.sql)]

추가 하는 `Categories_Delete` 프로시저 Northwind 데이터베이스에 저장 합니다. 데이터베이스에 추가 하는 저장된 프로시저에 대 한 지침은 단계 1로 다시 참조 합니다.

## <a name="step-6-updating-thecategoriestableadapter"></a>6 단계: 업데이트는`CategoriesTableAdapter`

했습니다 추가 우리는 `Categories_Delete` DAL 데이터베이스에 저장된 프로시저 현재 임시 SQL 문을 사용 하 여 삭제 작업을 수행 하도록 구성 되어 있습니다. 업데이트 해야는 `CategoriesTableAdapter` 하 고 사용 하도록 지시 하는 `Categories_Delete` 저장 프로시저를 대신 합니다.

> [!NOTE]
> 이 자습서의 앞부분에 있는 작업은 `NorthwindWithSprocs` 데이터 집합입니다. 데이터 집합에만 하나의 항목에 해당 `ProductsDataTable`, 이며 범주는 실행 되도록 해야 합니다. 따라서 여기서 가리키는 데이터 액세스 계층 I m이이 자습서의 나머지 부분에 대 한는 `Northwind` 데이터 집합에서 처음 만든 한은 [데이터 액세스 계층을 만들려면](../introduction/creating-a-data-access-layer-cs.md) 자습서입니다.


열기 Northwind 데이터 집합 선택에서 `CategoriesTableAdapter`, 속성 창으로 이동 하 고 있습니다. 속성 창 목록은 `InsertCommand`, `UpdateCommand`, `DeleteCommand`, 및 `SelectCommand` TableAdapter를 뿐만 아니라 해당 이름 및 연결 정보에서 사용 합니다. 확장 된 `DeleteCommand` 속성을 해당 세부 정보를 참조 하십시오. 그림 15에서 볼 수 있듯이 `DeleteCommand` s `ComamndType` 의 텍스트를 보내려면 하도록 지시 하는 텍스트를 속성이 `CommandText` 임시 SQL 쿼리로 속성입니다.


![속성 창에 해당 속성을 보려면 디자이너에서의 CategoriesTableAdapter 선택](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image43.png)

**그림 15**: 선택 된 `CategoriesTableAdapter` 속성 창에서 속성을 보려면 디자이너에서


이러한 설정을 변경 하려면 속성 창에서 (DeleteCommand) 텍스트를 선택 하 고 드롭다운 목록에서 (새로 만들기)를 선택 합니다. 에 대 한 설정을 지웁니다는 `CommandText`, `CommandType`, 및 `Parameters` 속성입니다. 다음으로 설정 된 `CommandType` 속성을 `StoredProcedure` 다음에 대 한 저장된 프로시저의 이름을 입력 하 고는 `CommandText` (`dbo.Categories_Delete`) 합니다. 먼저 순에서 속성을 입력할 수 있는지 확인 하는 경우는 `CommandType` 차례로 `CommandText` -Visual Studio에서 Parameters 컬렉션을 자동으로 입력 됩니다. 이 순서 대로 이러한 속성을 입력 하지 않으면를 사용 하는 경우에 수동으로 매개 변수 컬렉션 편집기를 통해 매개 변수를 추가 합니다. 두 경우 모두이 s (참조 그림 16) 올바른 매개 변수 설정을 변경 사항이 있는지 확인 하려면 매개 변수 컬렉션 편집기를 표시 하려면 매개 변수 속성의 줄임표를 클릭 하는 것이 좋습니다. 대화 상자에서 매개 변수를 표시 되지 않으면 추가 `@CategoryID` 매개 변수 수동으로 (추가할 필요가 없습니다는 `@RETURN_VALUE` 매개 변수).


![매개 변수 설정이 수정 되어 있는지 확인 하십시오.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs/_static/image44.png)

**그림 16**: 매개 변수 설정이 수정 되어 있는지 확인 하십시오.


DAL를 업데이트 후는 범주를 삭제 하는 자동으로 삭제 모든 관련된 제품 하 고 트랜잭션의 포괄적인 아래 작업을 수행 합니다. 이 확인 하려면 업데이트 및 삭제 기존 이진 데이터 페이지로 돌아가서 범주 중 하나에 대 한 삭제 단추를 클릭 합니다. 한 번의 클릭으로 마우스, 범주 및 모든 관련된 제품 삭제 됩니다.

> [!NOTE]
> 테스트 하기 전에 `Categories_Delete` 선택한 범주와 제품 수가 삭제 하는, 저장된 프로시저 수 있습니다 프로그램 데이터베이스의 백업 복사본을 만드는 것이 좋습니다. 사용 하는 경우는 `NORTHWND.MDF` 여기에 데이터베이스 `App_Data`, 하기만 하면 Visual Studio를 닫고의 MDF 및 LDF 파일을 복사 `App_Data` 다른 폴더에 있습니다. 기능을 테스트 한 후 Visual Studio를 닫고 데이터베이스를 복원할 수 및 파일에 현재 MDF 및 LDF 교체 `App_Data` 백업 복사본을 사용 합니다.


## <a name="summary"></a>요약

TableAdapter의 마법사 us에 대 한 저장된 프로시저를 자동으로 생성 됩니다, 동안 때 म 수 이미 이러한 저장된 프로시저 생성 하려는 또는 만드는지에 수동으로 또는 다른 도구와 함께 대신 경우가 있습니다. 이러한 시나리오를 수용할 수 있도록 TableAdapter 기존 저장된 프로시저를 가리키도록 구성할 수도 있습니다. 이 자습서에서는 Visual Studio 환경을 통해 데이터베이스에 저장된 프로시저를 수동으로 추가 하는 방법과 이러한 저장된 프로시저를 TableAdapter의 메서드를 연결 하는 방법을 살펴보았습니다. T-SQL 명령 및 스크립트 패턴 시작, 및 저장된 프로시저 내에서 트랜잭션을 롤백하는 중에 사용 되는 검사도 했습니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자가 Hilton Geisenow, S ren 야곱의 Lauritsen 및 Teresa 머피의 합니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)
> [다음](updating-the-tableadapter-to-use-joins-cs.md)
