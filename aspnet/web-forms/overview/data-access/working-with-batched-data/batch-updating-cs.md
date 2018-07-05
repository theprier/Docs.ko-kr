---
uid: web-forms/overview/data-access/working-with-batched-data/batch-updating-cs
title: 일괄 업데이트 (C#) | Microsoft Docs
author: rick-anderson
description: 단일 작업에서 여러 데이터베이스 레코드를 업데이트 하는 방법에 알아봅니다. 사용자 인터페이스 계층의 각 행이 편집 가능한 GridView를 빌드합니다. 데이터에서...
ms.author: aspnetcontent
ms.date: 06/26/2007
ms.assetid: 4e849bcc-c557-4bc3-937e-f7453ee87265
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-updating-cs
msc.type: authoredcontent
ms.openlocfilehash: 0cb55689ac3a6dc36ed18459ecece82ff0b073b7
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37842194"
---
<a name="batch-updating-c"></a>일괄 업데이트 (C#)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_64_CS.zip) 또는 [PDF 다운로드](batch-updating-cs/_static/datatutorial64cs1.pdf)

> 단일 작업에서 여러 데이터베이스 레코드를 업데이트 하는 방법에 알아봅니다. 사용자 인터페이스 계층의 각 행이 편집 가능한 GridView를 빌드합니다. 데이터 액세스 계층에서는 모든 업데이트가 성공 하거나 모든 업데이트 내용이 롤백됩니다 않도록 트랜잭션 내에서 여러 업데이트 작업 래핑합니다.


## <a name="introduction"></a>소개

에 [이전 자습서](wrapping-database-modifications-within-a-transaction-cs.md) 데이터베이스 트랜잭션에 대 한 지원을 추가 하려면 데이터 액세스 계층을 확장 하는 방법에 살펴보았습니다. 데이터베이스 트랜잭션은 보장 일련의 데이터 수정 문 모든 수정 실패 하거나 성공할 모두 하나의 원자성 작업으로 간주 됩니다. 이 하위 수준 DAL 기능으로 사용 하 여 일괄 처리 데이터 수정 인터페이스 만들기에 대해 준비가 다시 했습니다.

이 자습서의 각 행이 편집 가능한 (그림 1 참조) GridView를 빌드 해 보겠습니다. 각 행의 편집 인터페이스에 여기의 편집 열 필요가 없습니다를 렌더링 하므로 업데이트 및 취소 단추가 있습니다. 대신는 두 개의 제품 업데이트 페이지를 클릭 하면 GridView 행을 열거 하 고 데이터베이스를 업데이트 합니다.


[![GridView의 각 행은 편집 가능](batch-updating-cs/_static/image1.gif)](batch-updating-cs/_static/image1.png)

**그림 1**: GridView의 각 행이 편집 가능 ([큰 이미지를 보려면 클릭](batch-updating-cs/_static/image2.png))


Let s 시작!

> [!NOTE]
> 에 [일괄 처리 업데이트 수행](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-cs.md) DataList 컨트롤을 사용 하 여 자습서를 편집 하는 일괄 처리에서 만든 인터페이스입니다. 이 자습서에서 사용 하는 하나는 이전 GridView 다르며 일괄 업데이트는 트랜잭션 범위 내에서 수행 됩니다. 이 자습서를 완료 한 후 바랍니다 이전 자습서로 돌아와서 이전 자습서에서 추가한 데이터베이스 트랜잭션 관련 기능을 사용 하도록 업데이트 합니다.


## <a name="examining-the-steps-for-making-all-gridview-rows-editable"></a>모든 GridView 행을 편집할 수 있도록 하는 단계를 검사 합니다.

에 설명 된 대로 합니다 [An 개요의 삽입, 업데이트 및 삭제 데이터](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) 자습서에서는 GridView 행 단위로에서 해당 기본 데이터를 편집 하는 것에 대 한 기본 제공 지원을 제공 합니다. GridView의 어떤 행이를 통해 편집할 수 있는 정보 내부적으로 해당 [ `EditIndex` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.editindex(VS.80).aspx)합니다. 각 행을 행의 인덱스 값과 동일한 경우 참조 확인 GridView 되 고 해당 데이터 원본에 바인딩되어 대로 `EditIndex`입니다. 그렇다면 해당 행 필드가 렌더링 되는 편집을 사용 하는 s 인터페이스입니다. BoundFields, 편집 인터페이스는 텍스트 상자 인 `Text` 속성 BoundField s로 지정 된 데이터 필드의 값이 할당 됩니다 `DataField` 속성입니다. TemplateFields에 대 한 합니다 `EditItemTemplate` 대신 사용 되는 `ItemTemplate`합니다.

사용자가의 행 편집 단추를 클릭할 때 편집 워크플로가 시작 되는 것을 기억 하십시오. 포스트백을 발생 시키는이 설정 하는 GridView의 `EditIndex` 속성을 클릭 한 행의 인덱스 및 데이터 표를 다시 바인딩 횟수입니다. 포스트백 될 때 행의 취소 단추를 클릭할 때 합니다 `EditIndex` 의 값으로 설정 되어 `-1` 표에 데이터를 다시 바인딩하기 전에 합니다. GridView의 행은 0에서 인덱싱을 시작, 설정 `EditIndex` 에 `-1` 읽기 전용 모드에서 GridView를 표시 하는 효과가 있습니다.

`EditIndex` 속성은 행별 편집에 적합 하지만 일괄 편집 적합 하지 않습니다. 전체 GridView를 편집할 수 있도록 하려면 각 행의 편집 인터페이스를 사용 하 여 렌더링 해야 합니다. 이 작업을 수행 하는 가장 쉬운 방법은 각 편집 가능한 필드를 TemplateField의 편집 인터페이스에 정의 된 대로 구현 되는 위치를 만들 때의 `ItemTemplate`합니다.

다음을 통해 몇 가지 단계 만들겠습니다 GridView를 완전히 편집할 수 있습니다. 1 단계에서에서에서는 GridView 및 해당 ObjectDataSource를 만들어 시작 하 고 해당 BoundFields 및 CheckBoxField TemplateFields 변환 합니다. 2 단계와 3의 설명으로 넘어가겠습니다 편집 인터페이스는 TemplateFields에서 `EditItemTemplate` s를 해당 `ItemTemplate` s입니다.

## <a name="step-1-displaying-product-information"></a>1 단계: 제품 정보를 표시합니다.

GridView를 만드는 지 걱정 되기 전에 편집할 수 있는 다음 행, s 단순히 제품 정보를 표시 하 여 시작 합니다. 열기는 `BatchUpdate.aspx` 페이지에 `BatchData` 폴더 및 디자이너 도구 상자에서 끌어서 GridView입니다. GridView가 설정 `ID` 하 `ProductsGrid` 하 고 스마트 태그, 라는 새로운 ObjectDataSource는 바인딩할 선택 `ProductsDataSource`합니다. 해당 데이터를 검색할 ObjectDataSource를 구성 합니다 `ProductsBLL` s 클래스 `GetProducts` 메서드.


[![ProductsBLL 클래스를 사용 하는 ObjectDataSource 구성](batch-updating-cs/_static/image2.gif)](batch-updating-cs/_static/image3.png)

**그림 2**: ObjectDataSource 사용 하도록 구성 된 `ProductsBLL` 클래스 ([클릭 하 여 큰 이미지 보기](batch-updating-cs/_static/image4.png))


[![GetProducts 메서드를 사용 하 여 제품 데이터 검색](batch-updating-cs/_static/image3.gif)](batch-updating-cs/_static/image5.png)

**그림 3**: 사용 하 여 제품 데이터를 검색 합니다 `GetProducts` 메서드 ([클릭 하 여 큰 이미지 보기](batch-updating-cs/_static/image6.png))


GridView와 같은 ObjectDataSource가의 수정 기능을 행 단위로에서 작동 하도록 설계 됩니다. 레코드 집합을 업데이트 하기 위해 데이터를 일괄 처리 및 BLL에 전달 하는 ASP.NET 페이지의 코드 숨김 클래스에 약간의 코드를 작성 해야 합니다. 따라서 탭을 설정할 드롭 다운 목록을 ObjectDataSource에서 업데이트, 삽입 및 삭제를 (없음). 마법사를 완료 하려면 마침을 클릭 합니다.


[![UPDATE, INSERT 드롭 다운 목록을 설정 하 고 탭 삭제 (없음)](batch-updating-cs/_static/image4.gif)](batch-updating-cs/_static/image7.png)

**그림 4**: 드롭다운 목록에서 업데이트, 삽입 및 삭제 탭 하도록 설정 (없음) ([큰 이미지를 보려면 클릭](batch-updating-cs/_static/image8.png))


데이터 소스 구성 마법사를 완료 한 후 ObjectDataSource가 선언적 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](batch-updating-cs/samples/sample1.aspx)]

Visual Studio BoundFields 만들고 GridView에서 제품 데이터 필드에 대 한 CheckBoxField 해도 데이터 소스 구성 마법사를 완료 합니다. 이 자습서에서는 s만 보고 제품의 이름, 범주, 가격 및 지원 되지 않는 상태를 편집 하는 사용자를 허용 하도록 합니다. 제거를 제외한 모든 `ProductName`, `CategoryName`를 `UnitPrice`, 및 `Discontinued` 필드 및 이름 바꾸기는 `HeaderText` 의 처음 3 개 속성 각각 Product, Category 및 Price를 필드입니다. 마지막으로, GridView가 스마트 태그를 사용 하도록 설정 페이징 및 정렬 사용 확인란을 확인 합니다.

이 시점에서 GridView에 세 개의 BoundFields (`ProductName`, `CategoryName`, 및 `UnitPrice`) 및는 CheckBoxField (`Discontinued`). TemplateFields 이러한 네 가지 필드로 변환 하 고 다음 TemplateField s에서 편집 인터페이스를 이동 해야 `EditItemTemplate` 에 해당 `ItemTemplate`합니다.

> [!NOTE]
> 만들기 및 TemplateFields에서 사용자 지정 살펴보았습니다 합니다 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) 자습서입니다. TemplateFields CheckBoxField 고 BoundFields 변환 단계를 안내 및 인터페이스 정의 편집 해당 해당 `ItemTemplate` s, 있지만 막히면 또는 필요한 안 리프레셔가 언제 든 지이 이전 자습서를 다시 참조 하는 경우.


GridView가 스마트 태그에서 필드 대화 상자를 열려면 열 편집 링크를 클릭 합니다. 그런 다음 각 필드를 선택 하 고 TemplateField 링크로 변환이이 필드를 클릭 합니다.


![기존 BoundFields 및 CheckBoxField TemplateField로 변환](batch-updating-cs/_static/image5.gif)

**그림 5**: 기존 BoundFields 및 CheckBoxField TemplateField로 변환


인터페이스 편집 이동할 준비가에서는 이제는 각 필드를 TemplateField, 합니다 `EditItemTemplate` s를 `ItemTemplate` s.

## <a name="step-2-creating-theproductnameunitprice-anddiscontinuedediting-interfaces"></a>2 단계: 만들기 합니다`ProductName`,`UnitPrice`, 및`Discontinued`인터페이스 편집

만들기는 `ProductName`, `UnitPrice`, 및 `Discontinued` 인터페이스는이 단계의 주제 편집과 TemplateField에서 이미 정의 된 각 인터페이스가 간단 하지는 `EditItemTemplate`합니다. 만들기는 `CategoryName` 편집 인터페이스는 해당 범주의 DropDownList를 만드는 필요 하므로 조금 더 복잡 합니다. 이 `CategoryName` 3 단계에서에서 처리는 인터페이스를 편집 합니다.

시작 s는 `ProductName` TemplateField 합니다. GridView가 스마트 태그에서 템플릿 편집 링크를 클릭 하 고 드릴 다운 하 여 `ProductName` TemplateField의 `EditItemTemplate`입니다. 텍스트 선택, 클립보드에 복사 및 붙여 넣습니다 합니다 `ProductName` TemplateField의 `ItemTemplate`입니다. 텍스트 상자 s 변경할 `ID` 속성을 `ProductName`입니다.

RequiredFieldValidator를 다음으로, 추가 `ItemTemplate` 사용자는 각 제품의 이름에 대 한 값을 확인 합니다. 설정 합니다 `ControlToValidate` productname, 속성을 `ErrorMessage` 속성에는 제품의 이름을 제공 해야 합니다. 하며 `Text` 속성을 \*입니다. 이러한 추가 마치면는 `ItemTemplate`, 화면 그림 6 비슷하게 표시 됩니다.


[![텍스트 상자와는 RequiredFieldValidator ProductName TemplateField 이제 포함](batch-updating-cs/_static/image6.gif)](batch-updating-cs/_static/image9.png)

**그림 6**: 합니다 `ProductName` TemplateField 이제 텍스트 상자 및 RequiredFieldValidator ([클릭 하 여 큰 이미지 보기](batch-updating-cs/_static/image10.png))


에 대 한는 `UnitPrice` 인터페이스를 편집에서 텍스트를 복사 하 여 시작 합니다 `EditItemTemplate` 에 `ItemTemplate`. 다음으로, 텍스트 상자 및 집합 앞에 $를 배치할 해당 `ID` UnitPrice 속성 및 해당 `Columns` 8 속성입니다.

CompareValidator 추가 합니다 `UnitPrice` s `ItemTemplate` 되도록 사용자가 입력 한 값 보다 크거나 같은 $0.00 유효한 통화 값입니다. 유효성 검사기가 설정 `ControlToValidate` 속성을 UnitPrice, 해당 `ErrorMessage` 속성에 유효한 통화 값을 입력 해야 합니다. 모든 통화 기호.를 생략 하세요 해당 `Text` 속성을 \*, 해당 `Type` 속성을 `Currency`, 해당 `Operator` 속성을 `GreaterThanEqual`, 및 해당 `ValueToCompare` 속성을 0입니다.


[![가격 입력 되도록 CompareValidator는 음수가 아닌 통화 값 추가](batch-updating-cs/_static/image7.gif)](batch-updating-cs/_static/image11.png)

**그림 7**: 가격 입력 되도록 CompareValidator는 음수가 아닌 통화 값을 추가 ([큰 이미지를 보려면 클릭](batch-updating-cs/_static/image12.png))


에 대 한 합니다 `Discontinued` TemplateField에 이미 정의 된 확인란을 사용할 수 있습니다는 `ItemTemplate`합니다. 설정 하기만 하면 됩니다 해당 `ID` Discontinued 하 고 `Enabled` 속성을 `true`입니다.

## <a name="step-3-creating-thecategorynameediting-interface"></a>3 단계: 만들기는`CategoryName`인터페이스 편집

편집 인터페이스는 `CategoryName` TemplateField s `EditItemTemplate` 의 값을 표시 하는 텍스트 상자가 포함는 `CategoryName` 데이터 필드입니다. 가능한 범주를 나열 하는 DropDownList 한 개로 대체 해야 합니다.

> [!NOTE]
> 합니다 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) 자습서 더 철저 하 고 전체 토론 TextBox와 달리 DropDownList를 포함 하도록 템플릿을 사용자 지정에 포함 되어 있습니다. 여기에 나오는 단계를 완료 하는 동안 상품 표시 됩니다. 에 대 한 더 상세한 만들기 및 구성 범주 DropDownList를 다시 참조를 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) 자습서입니다.


DropDownList를 도구 상자에서 끌어 합니다 `CategoryName` TemplateField s `ItemTemplate`설정, 해당 `ID` 에 `Categories`입니다. 이 시점에서 우리는 일반적으로 Dropdownlist의 데이터 원본을 정의할 해당 스마트 태그를 통해 새 ObjectDataSource 만들기. 그러나 내 ObjectDataSource 추가이 `ItemTemplate`, 각 GridView 행에 대해 만든 ObjectDataSource 인스턴스 결과 합니다. 대신 만든을 GridView의 TemplateFields 외부 ObjectDataSource 사용 수 있습니다. 아래에 디자이너 도구 상자에서 ObjectDataSource를 끌어서 템플릿 편집을 종료 합니다 `ProductsDataSource` ObjectDataSource 합니다. 이름을 새 ObjectDataSource `CategoriesDataSource` 사용 하도록 구성 하는 `CategoriesBLL` s 클래스 `GetCategories` 메서드.


[![ObjectDataSource CategoriesBLL Clas를 사용 하도록 구성](batch-updating-cs/_static/image8.gif)](batch-updating-cs/_static/image13.png)

**그림 8**: ObjectDataSource 사용 하도록 구성 된 `CategoriesBLL` Clas ([클릭 하 여 큰 이미지 보기](batch-updating-cs/_static/image14.png))


[![GetCategories 메서드를 사용 하 여 범주 데이터를 검색 합니다.](batch-updating-cs/_static/image9.gif)](batch-updating-cs/_static/image15.png)

**그림 9**: 사용 하 여 범주 데이터를 검색 합니다 `GetCategories` 메서드 ([클릭 하 여 큰 이미지 보기](batch-updating-cs/_static/image16.png))


이 ObjectDataSource를 사용 하 여 데이터를 검색 하는 단순히, 드롭 다운 목록에서 UPDATE 및 DELETE 탭 (없음)을 설정 합니다. 마법사를 완료 하려면 마침을 클릭 합니다.


[![집합에 UPDATE 및 DELETE 탭 (없음)을 드롭다운 목록](batch-updating-cs/_static/image10.gif)](batch-updating-cs/_static/image17.png)

**그림 10**: (없음)로 업데이트 및 삭제 하는 탭의 드롭다운 목록을 설정 ([큰 이미지를 보려면 클릭](batch-updating-cs/_static/image18.png))


마법사를 완료 한 후의 `CategoriesDataSource` s 선언적 태그는 다음과 같습니다.


[!code-aspx[Main](batch-updating-cs/samples/sample2.aspx)]

사용 하 여 합니다 `CategoriesDataSource` 를 만들고 구성한 돌아갑니다 합니다 `CategoryName` TemplateField의 `ItemTemplate` DropDownList s 스마트 태그에서 데이터 원본 선택 링크를 클릭 합니다. 데이터 소스 구성 마법사에서 선택 합니다 `CategoriesDataSource` 첫 번째 드롭다운 목록에서 옵션을 선택할 `CategoryName` 표시에 사용 하 고 `CategoryID` 값으로.


[![DropDownList를 CategoriesDataSource에 바인딩](batch-updating-cs/_static/image11.gif)](batch-updating-cs/_static/image19.png)

**그림 11**: DropDownList를 바인딩하는 `CategoriesDataSource` ([클릭 하 여 큰 이미지 보기](batch-updating-cs/_static/image20.png))


이 시점에서 `Categories` DropDownList 모든 범주가 나열 되지만 선택 되지 않습니다 아직 자동으로 GridView 행에 바인딩된 제품에 대 한 적절 한 범주입니다. 로 설정 해야이 작업을 수행 하는 `Categories` DropDownList s `SelectedValue` s 제품 `CategoryID` 값입니다. DropDownList s 스마트 태그에서 데이터 바인딩 편집 링크를 클릭 하 고 연결 합니다 `SelectedValue` 속성과 `CategoryID` 그림 12에 나와 있는 것 처럼 데이터 필드입니다.


![제품의 CategoryID DropDownList의 SelectedValue 속성에 바인딩](batch-updating-cs/_static/image12.gif)

**그림 12**: 제품 s 바인딩할 `CategoryID` DropDownList의 값 `SelectedValue` 속성


한 마지막 문제 유지: 제품 만들어지고 t를 사용 하는 경우는 `CategoryID` 값에 지정 된 다음 데이터 바인딩 문을 `SelectedValue` 예외가 발생 합니다. DropDownList 범주에 대 한 항목만 포함 하 고 해당 제품에 대 한 옵션을 제공 하지 않습니다 있기 때문에 `NULL` 데이터베이스에 대 한 값 `CategoryID`합니다. 이 문제를 해결 하려면 DropDownList s를 설정 `AppendDataBoundItems` 속성을 `true` 드롭다운 목록에서 새 항목을 추가 하 고 생략는 `Value` 선언적 구문에서 속성입니다. 즉, 있는지는 `Categories` DropDownList s 선언적 구문은 다음과 같습니다:


[!code-aspx[Main](batch-updating-cs/samples/sample3.aspx)]

참고 하는 방법을 `<asp:ListItem Value="">` -하나 선택-가 해당 `Value` 특성이 명시적으로 빈 문자열로 설정 합니다. 다시 참조를 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) 이 추가 DropDownList 항목 처리에 필요한 이유는 대 한 더 상세히 논의 자습서 합니다 `NULL` 사례 이유와 할당은 `Value` 속성을 빈 문자열로 반드시 필요 합니다.

> [!NOTE]
> 잠재적인 성능 및 확장성 문제를 여기서 유의 해야 하는 경우 각 행에는 DropDownList를 `CategoriesDataSource` 해당 데이터 원본으로는 `CategoriesBLL` s 클래스 `GetCategories` 메서드가 호출 될 *n* 페이지 마다 한 번 방문 위치 *n* 입니다 GridView의 행 수입니다. 이러한 *n* 호출 `GetCategories` 될 *n* 데이터베이스에 쿼리 합니다. 이 미치는 데이터베이스 요청 캐시 또는 종속성 또는 매우 짧은 시간 기반 만료 캐싱을 SQL을 사용 하 여 캐싱 계층을 통해 반환 된 범주를 캐시 하 여 떨어질 수 없습니다. 캐싱 옵션에 당 요청에 대 한 자세한 내용은 참조 [ `HttpContext.Items` 당 요청 캐시 저장소](http://aspnet.4guysfromrolla.com/articles/060904-1.aspx)합니다.


## <a name="step-4-completing-the-editing-interface"></a>4 단계: 완료 편집 인터페이스

에서는 ve 진행 상황을 보려면 일시 중지 하지 않고 GridView가 템플릿에 변경 횟수를 수행 합니다. 시간을 내어 브라우저를 통해 진행 상황을 확인 합니다. 사용 하 여 각 행은 렌더링 그림 13에서 볼 수 있듯이 해당 `ItemTemplate`, 인터페이스 편집 셀 s를 포함 하는 합니다.


[![각 GridView 행은 편집 가능](batch-updating-cs/_static/image13.gif)](batch-updating-cs/_static/image21.png)

**그림 13**: 각 GridView 행은 편집 가능 ([큰 이미지를 보려면 클릭](batch-updating-cs/_static/image22.png))


관리 하는 것은 시점에서 몇 가지 사소한 서식 문제가 있습니다. 이때 먼저는 `UnitPrice` 값 네 개의 소수 자릿수가 포함 되어 있습니다. 이 문제를 해결 하려면 돌아갑니다 합니다 `UnitPrice` TemplateField의 `ItemTemplate` TextBox가 스마트 태그에서 데이터 바인딩 편집 링크를 클릭 합니다. 다음으로, 지정 된 `Text` 숫자로 속성의 서식을 지정 합니다.


![숫자로 Text 속성 형식](batch-updating-cs/_static/image14.gif)

**그림 14**: 형식은 `Text` 숫자로 속성


둘째, let s center에서 확인란을 `Discontinued` 열 대신 왼쪽 맞춤 하 합니다. GridView가 스마트 태그에서 열 편집을 클릭 하 고 선택 된 `Discontinued` TemplateField 왼쪽된 아래 모퉁이의 필드 목록에서. 드릴 다운 `ItemStyle` 설정의 `HorizontalAlign` 그림 15 에서처럼 센터로 속성입니다.


![Center는 지원 되지 않는 확인란](batch-updating-cs/_static/image15.gif)

**그림 15**: Center는 `Discontinued` 확인란


그런 다음 페이지로 ValidationSummary 컨트롤을 추가 하 고 설정 해당 `ShowMessageBox` 속성을 `true` 및 해당 `ShowSummary` 속성을 `false`입니다. 또한 단추 웹 컨트롤을 클릭할 때를 추가, 변경 하는 사용자가 업데이트 됩니다. 특히, 두 개의 단추 웹 컨트롤을 GridView 위와 및 한 수준 아래에 두 컨트롤 모두 설정 추가 `Text` 속성 업데이트 제품을 합니다.

GridView가 이후 해당 TemplateFields에 정의 된 인터페이스를 편집 `ItemTemplate` s를 `EditItemTemplate` s 불필요 한 되어 삭제 될 수 있습니다.

위의 만드는 서식 변경 사항을 언급 했 듯이, 후 단추 컨트롤을 추가 하 고 불필요 한 제거 `EditItemTemplate` s, 페이지 s 선언적 구문에는 다음과 같습니다.


[!code-aspx[Main](batch-updating-cs/samples/sample4.aspx)]

그림 16에서는 단추 웹 컨트롤을 추가한 후 브라우저를 통해 볼 때이 페이지 및 서식 지정 변경 내용을 보여 줍니다.


[![이제 페이지에는 두 업데이트 제품 단추가 포함 되어 있습니다.](batch-updating-cs/_static/image16.gif)](batch-updating-cs/_static/image23.png)

**그림 16**: The 페이지 이제 포함 두 업데이트 제품 단추 ([큰 이미지를 보려면 클릭](batch-updating-cs/_static/image24.png))


## <a name="step-5-updating-the-products"></a>5 단계: 업데이트 제품

사용자가이 페이지를 방문 하는 경우 이러한 수정 내용이 두 개의 업데이트 제품 단추 중 하나를 클릭 합니다. 어떤 이유로 든 각 행에 대 한 사용자가 입력 한 값을 저장 하려고 하는 시점을 `ProductsDataTable` 인스턴스 및 다음 전달한 됩니다 하는 BLL 메서드에 전달할 `ProductsDataTable` DAL의 인스턴스 `UpdateWithTransaction` 메서드. 합니다 `UpdateWithTransaction` 에서 만든 메서드를 [이전 자습서](wrapping-database-modifications-within-a-transaction-cs.md), 되도록 변경 내용의 일괄 처리는 원자성 작업으로 업데이트 됩니다.

라는 메서드를 만듭니다 `BatchUpdate` 에서 `BatchUpdate.aspx.cs` 다음 코드를 추가 합니다.


[!code-csharp[Main](batch-updating-cs/samples/sample5.cs)]

이 메서드가 모든 제품으로 시작에 `ProductsDataTable` BLL s에 대 한 호출을 통해 `GetProducts` 메서드. 그런 다음 열거 하는 `ProductGrid` GridView s [ `Rows` 컬렉션](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rows(VS.80).aspx)합니다. `Rows` 컬렉션에는 [ `GridViewRow` 인스턴스](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewrow.aspx) GridView에 표시 되는 각 행에 대 한 합니다. 각 페이지에 GridView가 최대 10 개의 행을 표시 하는 것 이므로 `Rows` 컬렉션 10 개 이하의 항목이 됩니다.

각 행에 대 한는 `ProductID` 에서 놓은는 `DataKeys` 컬렉션 및 적절 한 `ProductsRow` 에서 선택 된를 `ProductsDataTable`합니다. 네 가지 TemplateField 입력된 컨트롤을 참조 하는 프로그래밍 방식으로 및 해당 값에 할당 합니다 `ProductsRow` 속성 인스턴스. 각 GridView 후 s 행에 값 사용 되어 업데이트를 `ProductsDataTable`, 해당 s BLL s에 전달 `UpdateWithTransaction` 메서드를 호출 하는, 이전 자습서에서 살펴본 것 처럼 간단히 DAL s에 `UpdateWithTransaction` 메서드.

이 자습서에 사용 된 일괄 처리 업데이트 알고리즘에서 각 행을 업데이트 합니다 `ProductsDataTable`의 제품 정보가 변경 되었는지 여부에 관계 없이 GridView의 행에 해당 하는 합니다. 이러한 과제를 안겨 유효 하지 t 일반적으로 성능 문제를 업데이트 하는 동안 데이터베이스 테이블에 변경 내용을 다시 감사 하는 경우 불필요 한 레코드를 발생할 수 있습니다 이러한 합니다. 다시 합니다 [일괄 처리 업데이트 수행](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-cs.md) 자습서 DataList를 사용 하 여 인터페이스를 업데이트 하는 일괄 처리를 탐색 하 고만 실제로 사용자가 수정 된 레코드만 업데이트 하는 코드를 추가 합니다. 기술을 사용 하 여 자유롭게 [일괄 처리 업데이트 수행](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-cs.md) 원하는 경우이 자습서에서는 코드를 업데이트 합니다.

> [!NOTE]
> Visual Studio GridView s에 기본 키 값의 원본 데이터를 자동으로 할당 스마트 태그를 통해 GridView에 데이터 원본을 바인딩할 경우 `DataKeyNames` 속성입니다. 바인딩하지 않았습니다 ObjectDataSource GridView가 스마트 태그를 통해 GridView에 1 단계에에서 설명 된 대로 경우 GridView가 수동으로 설정 해야 합니다 `DataKeyNames` 속성에 액세스 하기 위해 ProductID는 `ProductID` 통해 각 행에 대 한 값을 `DataKeys` 컬렉션입니다.


사용 된 코드 `BatchUpdate` BLL에서 사용 되는 것과 비슷합니다 `UpdateProduct` 메서드, 주요 차이점에는 합니다 `UpdateProduct` 메서드 하나만 `ProductRow` 아키텍처에서 인스턴스를 검색 합니다. 속성을 할당 하는 코드를 `ProductRow` 간에 동일 합니다 `UpdateProducts` 메서드 및 코드를 `foreach` 루프 `BatchUpdate`전체 패턴에는 합니다.

이 자습서를 완료 하려면 할 필요는 `BatchUpdate` 메서드를 호출 하는 경우 업데이트 제품 단추 중 하나를 클릭 합니다. 에 대 한 이벤트 처리기 만들기는 `Click` 이러한 두 이벤트 단추 컨트롤 및 이벤트 처리기에 다음 코드를 추가 합니다.


[!code-csharp[Main](batch-updating-cs/samples/sample6.cs)]

호출 하려고 먼저 `BatchUpdate`합니다. 다음으로 `ClientScript property` 제품 업데이트 되었습니다. 읽는 messagebox를 표시 하는 JavaScript를 삽입 하는 데 사용 됩니다.

이 코드를 테스트해 1 분이 걸립니다. 방문 `BatchUpdate.aspx` 브라우저를 통해 많은 행을 편집 하 고 업데이트 제품 단추 중 하나를 클릭 합니다. 입력된 유효성 검사 오류가 없는 경우 제품 업데이트 되었습니다. 읽는 messagebox를 표시 됩니다. 원자성 업데이트를 확인 하려면 추가할 임의 `CHECK` 제약 조건을 허용 하지 않는 것 처럼 `UnitPrice` 1234.56의 값입니다. 다음 `BatchUpdate.aspx`, s 제품 중 하나를 설정할 수 있도록 레코드 수가 편집 `UnitPrice` 금지 된 값 (1234.56) 값입니다. 이 원래 값으로 롤백할 해당 일괄 처리 작업 중 다른 변경 내용으로 업데이트 제품을 클릭 하는 경우 오류가 발생 해야 합니다.

## <a name="an-alternativebatchupdatemethod"></a>대 안으로`BatchUpdate`메서드

`BatchUpdate` 방금 메서드 검사 검색 *모든* BLL s에서 제품 `GetProducts` 메서드 다음 GridView에 표시 되는 해당 레코드를 업데이트 합니다. 이 방법은 GridView 페이징, 사용 하지 않지만 경우 있을 수백, 수천 또는 수만 개의 제품을 GridView에 10 번만 행의 경우에 적합 합니다. 이러한 경우에만 수정할 데이터베이스를 그 중 10 개에서 시작 하는 모든 제품은 그다지 적합 합니다.

이러한 유형의 경우 다음을 사용 하는 것이 좋습니다 `BatchUpdateAlternate` 메서드 대신:


[!code-csharp[Main](batch-updating-cs/samples/sample7.cs)]

`BatchMethodAlternate` 비어 있는 새를 만들어 시작 `ProductsDataTable` 라는 `products`합니다. 그런 다음 GridView의 단계별로 `Rows` 컬렉션 및 BLL s를 사용 하 여 특정 제품 정보를 가져옵니다 하는 각 행에 대 한 `GetProductByProductID(productID)` 메서드. 검색 `ProductsRow` 인스턴스에 해당 속성을 동일한 방식으로 업데이트 `BatchUpdate`, 뒤에 가져온 행을 업데이트 합니다 `products``ProductsDataTable` DataTable s를 통해 [ `ImportRow(DataRow)` 메서드](https://msdn.microsoft.com/library/system.data.datatable.importrow(VS.80).aspx)합니다.

후 합니다 `foreach` 루프가 완료 되 면 `products` 하나가 포함 되어 있습니다 `ProductsRow` GridView의 각 행에 대 한 인스턴스. 이후 각를 `ProductsRow` 에 추가 된 인스턴스를 `products` (대신 업데이트) 맹목적으로 전달 되도록 하는 경우를 `UpdateWithTransaction` 메서드를 `ProductsTableAdatper` 레코드의 각 데이터베이스에 삽입 하려고 합니다. 대신, 각이 행의 수정 되었다는 사실을 (추가 됨)을 지정 해야 합니다.

명명 된 BLL에 새 메서드를 추가 하 여 수행할 수 있습니다이 `UpdateProductsWithTransaction`합니다. `UpdateProductsWithTransaction`아래와 같이 설정 합니다 `RowState` 각를 `ProductsRow` 인스턴스를 `ProductsDataTable` 에 `Modified` 다음 전달를 `ProductsDataTable` DAL s에 `UpdateWithTransaction` 메서드.


[!code-csharp[Main](batch-updating-cs/samples/sample8.cs)]

## <a name="summary"></a>요약

GridView 행 마다 기본 편집 기능을 제공 하지만 완벽 하 게 편집할 수 있는 인터페이스를 만들기 위한 지원 하지 않습니다. 이 자습서에서 살펴본 것 처럼 이러한 인터페이스 가능 하지만, 약간의 작업이 필요 합니다. 모든 행은 편집할 수는 GridView를 만들려면 TemplateFields GridView의 필드를 변환 하 여 내 편집 인터페이스를 정의 해야 합니다 `ItemTemplate` s입니다. 또한 업데이트 All-단추 웹 컨트롤 형식 GridView에서 별도 페이지에 추가 되어야 합니다. 이러한 단추 `Click` GridView가 열거 해야 하는 이벤트 처리기 `Rows` 컬렉션에서 변경 내용을 저장을 `ProductsDataTable`, 업데이트 된 정보는 해당 BLL 메서드에 전달 합니다.

다음 자습서에서 일괄 처리를 삭제 하기 위한 인터페이스를 만드는 방법에 살펴보겠습니다. 각 GridView 행 되는 확인란을 포함 하 고 대신 모든를 업데이트 하는 특히-단추 입력 단추 선택한 행을 삭제 해야 합니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자는 Teresa Murphy 및 David Suru 있었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](wrapping-database-modifications-within-a-transaction-cs.md)
> [다음](batch-deleting-cs.md)
