---
uid: web-forms/overview/data-access/working-with-batched-data/batch-updating-vb
title: "일괄 업데이트 (VB) | Microsoft Docs"
author: rick-anderson
description: "한 번에 여러 데이터베이스 레코드를 업데이트 하는 방법에 알아봅니다. 사용자 인터페이스 계층의 각 행은 편집할 수는 GridView 작성할 수 있습니다. 데이터에서..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/26/2007
ms.topic: article
ms.assetid: d191a204-d7ea-458d-b81c-0b9049ecb55f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-updating-vb
msc.type: authoredcontent
ms.openlocfilehash: 02df858a7ad2ccefce4717e9bb7b08fc4c8d6ace
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="batch-updating-vb"></a>일괄 업데이트 (VB)
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_64_VB.zip) 또는 [PDF 다운로드](batch-updating-vb/_static/datatutorial64vb1.pdf)

> 한 번에 여러 데이터베이스 레코드를 업데이트 하는 방법에 알아봅니다. 사용자 인터페이스 계층의 각 행은 편집할 수는 GridView 작성할 수 있습니다. 데이터 액세스 계층으로 모든 업데이트가 성공 하거나 모든 업데이트 롤백되는 트랜잭션에서 여러 업데이트 작업을 래핑할 합니다.


## <a name="introduction"></a>소개

에 [이전 자습서](wrapping-database-modifications-within-a-transaction-vb.md) 데이터베이스 트랜잭션에 대 한 지원을 추가 하도록 데이터 액세스 계층을 확장 하는 방법에 살펴보았습니다. 데이터베이스 트랜잭션을 보장 일련의 데이터 수정 문이 모든 수정 작업은 실패 하며 또는 성공할 모두 보장 하는 하나의 원자성 작업으로 간주 합니다. 이 하위 수준 DAL 기능으로 위치로 다시 우리 배웠으므로 일괄 처리 데이터 수정 인터페이스 만들기 준비 합니다.

이 자습서의 각 행이 편집 가능한 (그림 1 참조)는 GridView 빌드합니다. 각 행의 편집 인터페이스의 거기에서 편집의 열에 대 한 필요 하지를 렌더링 하므로 업데이트 및 취소 단추입니다. 대신,는 두 개의 제품 업데이트 페이지에서를 클릭 하면 GridView 행을 열거 하 고 데이터베이스를 업데이트 합니다.


[![GridView에서 각 행은 편집 가능](batch-updating-vb/_static/image1.gif)](batch-updating-vb/_static/image1.png)

**그림 1**: GridView에서 각 행은 편집 가능 ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image2.png))


Let s가 시작 되었습니다.

> [!NOTE]
> 에 [일괄 업데이트 수행](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb.md) DataList 컨트롤을 사용 하 여 만든 일괄 처리를 편집 하는 자습서 인터페이스입니다. 이 자습서에는 하나는 사용 하 여 이전는 GridView 다르며 일괄 업데이트는 트랜잭션의 범위 내에서 수행 됩니다. 이 자습서를 완료 한 후 확인해 이전 자습서에서 추가 데이터베이스 트랜잭션 관련 기능을 사용 하도록 업데이트 하 고 이전 자습서로 돌아올 수 있습니다.


## <a name="examining-the-steps-for-making-all-gridview-rows-editable"></a>모든 GridView 행 편집 가능으로 설정 하는 단계를 검토 합니다.

에 설명 된 대로 [는 개요의 삽입, 업데이트 및 삭제 데이터](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) 자습서에서는 GridView는 행 단위로에 원본 데이터를 편집 하기 위한 기본 제공 지원을 제공 합니다. GridView의 어떤 행이를 통해 편집할 수 있는 정보 내부적으로 해당 [ `EditIndex` 속성](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.gridview.editindex(VS.80).aspx)합니다. 각 행을 행의 인덱스의 값이 같은 경우 참조 확인 GridView 되 고 해당 데이터 원본에 바인딩되어 처럼 `EditIndex`합니다. 이 경우 해당 행의 필드가 렌더링 되는 편집을 사용 하는 인터페이스입니다. BoundFields, 편집 인터페이스는 TextBox 인 `Text` 속성 BoundField s로 지정 된 데이터 필드의 값이 할당은 `DataField` 속성입니다. TemplateFields에 대 한는 `EditItemTemplate` 대신에 사용 되는 `ItemTemplate`합니다.

행의 편집 단추를 클릭 하면 편집 워크플로 시작 됨을 기억 하십시오. 이러한 포스트백 응용 프로그램, 설정 하는 GridView의 `EditIndex` 속성을 클릭 한 행의 인덱스 표에 데이터를 다시 바인딩 횟수입니다. 다시 게시 될 때 행의 취소 단추 클릭 시는 `EditIndex` 의 값으로 설정 되어 `-1` 표에 데이터를 다시 바인딩하기 전에 합니다. 설정 하는 인덱스가 0부터 시작 하는 GridView의 행, 하므로 `EditIndex` 를 `-1` GridView 읽기 전용 모드에서 표시 하는 효과가 있습니다.

`EditIndex` 속성 당 행을 편집 하는 데 적합 하지만 일괄 처리 편집을 위해 설계 되지 않았습니다. 전체 GridView를 편집할 수 있도록 하려면 각 행의 편집 인터페이스를 사용 하 여 렌더링 해야 합니다. 이 수행 하는 가장 쉬운 방법은를 각 편집 가능한 필드 구현 하는 해당 편집 인터페이스와 TemplateField에 정의 된 대로 만드는 것은 `ItemTemplate`합니다.

다음을 통해 여러 단계를 만들겠습니다 완전히 편집 가능한 GridView입니다. 1 단계에서에서 먼저 GridView 및 해당 ObjectDataSource를 만드세요 알아보고 TemplateFields CheckBoxField 이와 BoundFields 변환 하겠습니다. 2 단계와 3에 옮깁니다 편집 인터페이스는 TemplateFields에서 `EditItemTemplate` s를 자신의 `ItemTemplate` s입니다.

## <a name="step-1-displaying-product-information"></a>1 단계: 제품 정보를 표시합니다.

GridView 만드는 걱정 전에 있는 행을 편집할 수, s 단순히 제품 정보를 표시 하 여 시작 합니다. 열기는 `BatchUpdate.aspx` 페이지에 `BatchData` 폴더와 디자이너 도구 상자에서 끌어서는 GridView입니다. GridView s 설정 `ID` 를 `ProductsGrid` 하 고 스마트 태그를 라는 새 ObjectDataSource 바인딩할 선택 `ProductsDataSource`합니다. 구성에서 데이터를 검색 하도록 ObjectDataSource는 `ProductsBLL` s 클래스 `GetProducts` 메서드.


[![ObjectDataSource ProductsBLL 클래스를 사용 하도록 구성](batch-updating-vb/_static/image2.gif)](batch-updating-vb/_static/image3.png)

**그림 2**: 구성에 사용 하 여 ObjectDataSource는 `ProductsBLL` 클래스 ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image4.png))


[![GetProducts 메서드를 사용 하 여 제품 데이터를 검색 합니다.](batch-updating-vb/_static/image3.gif)](batch-updating-vb/_static/image5.png)

**그림 3**: 사용 하 여 제품 데이터 검색은 `GetProducts` 메서드 ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image6.png))


GridView 처럼 ObjectDataSource의 수정 기능 행 단위로에서 작동 하도록 설계 됩니다. 레코드 집합을 업데이트 하기 위해 데이터를 일괄 처리 및 BLL에 전달 하는 ASP.NET 페이지의 코드 숨김 클래스에서 약간의 코드를 작성 해야 합니다. 따라서 탭을 설정할 드롭 다운 목록을 ObjectDataSource s에서 업데이트, 삽입 및 삭제를 (없음). 마법사를 완료 하려면 마침을 클릭 합니다.


[![삽입, 업데이트에서 드롭 다운 목록을 설정 하 고 탭 (없음)를 삭제](batch-updating-vb/_static/image4.gif)](batch-updating-vb/_static/image7.png)

**그림 4**: 드롭 다운 목록에서 업데이트, 삽입 및 삭제 탭 하도록 설정 (None) ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image8.png))


데이터 소스 구성 마법사를 완료 한 후 ObjectDataSource s 선언 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](batch-updating-vb/samples/sample1.aspx)]

GridView에서 BoundFields 및 제품 데이터 필드에 대 한 CheckBoxField를 만드는 Visual Studio로 인해 데이터 소스 구성 마법사를 완료 합니다. 이 자습서에 대 한 s만 보고 제품의 이름, 범주, 가격 및 중단 된 상태를 편집 하는 사용자가을 허용 하도록 합니다. 제거 제외한 모두 `ProductName`, `CategoryName`, `UnitPrice`, 및 `Discontinued` 필드 및 이름 바꾸기는 `HeaderText` 의 처음 3 개의 속성 필드를 제품, 범주 및 가격을 각각. 마지막으로, GridView s 스마트 태그에서 페이징 사용 및 정렬 사용 확인란을 선택 합니다.

이 시점에서 GridView에 세 개의 BoundFields (`ProductName`, `CategoryName`, 및 `UnitPrice`) 및는 CheckBoxField (`Discontinued`). 이러한 4 개 필드가 TemplateFields로 변환한 다음 TemplateField s에서 편집 인터페이스를 이동 해야 `EditItemTemplate` 를 해당 `ItemTemplate`합니다.

> [!NOTE]
> 만들기 및 TemplateFields에 사용자 지정에서 살펴본는 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) 자습서입니다. TemplateFields BoundFields 및 CheckBoxField 변환 단계 살펴봅니다 및 인터페이스 정의 편집 자신의 `ItemTemplate` s 있지만 의문 사항이 나 필요한 안 리프레셔를 원하는 대로를 다시 이전이 자습서를 참조 하는 경우.


GridView s 스마트 태그에서 필드 대화 상자를 열려면 열 편집 링크를 클릭 합니다. 다음 각 필드를 선택 하 고를 TemplateField 링크로 Convert이이 필드를 클릭 합니다.


![기존 BoundFields 및 CheckBoxField TemplateFields을으로 변환](batch-updating-vb/_static/image5.gif)

**그림 5**: 기존 BoundFields 및 CheckBoxField TemplateFields을으로 변환


인터페이스에서는 편집을 이동 하려면 준비 된 각 필드를 TemplateField는, 했으므로 `EditItemTemplate` s는 `ItemTemplate` s입니다.

## <a name="step-2-creating-theproductnameunitprice-anddiscontinuedediting-interfaces"></a>2 단계: 만들기는`ProductName`,`UnitPrice`, 및`Discontinued`인터페이스 편집

만들기는 `ProductName`, `UnitPrice`, 및 `Discontinued` 편집 인터페이스는이 단계의 항목 설정 되며 간단 TemplateField s에 이미 정의 된 각 인터페이스가 대로 `EditItemTemplate`합니다. 만들기는 `CategoryName` 편집 인터페이스는 해당 범주의 DropDownList를 만드는 필요 하므로 약간 더 개입 됩니다. 이 `CategoryName` 3 단계에서에서 편집 인터페이스는 해결 했습니다.

S로 시작는 `ProductName` TemplateField 합니다. GridView s 스마트 태그에서 템플릿 편집 링크를 클릭 하 고 드릴 다운 하 여 `ProductName` TemplateField의 `EditItemTemplate`합니다. 입력란을 선택 하 고 클립보드에 복사 후는 `ProductName` TemplateField의 `ItemTemplate`합니다. TextBox s 변경 `ID` 속성을 `ProductName`합니다.

다음에 RequiredFieldValidator 추가 `ItemTemplate` 사용자 각 s 제품 이름에 대 한 값을 제공 하도록 합니다. 설정의 `ControlToValidate` 제품 이름에는 속성의 `ErrorMessage` 속성을 하면 제품의 이름을 제공 해야 합니다. 및 `Text` 속성을 \*합니다. 후 이러한 항목을 추가 하 고 `ItemTemplate`, 화면 그림 6 유사 합니다.


[![ProductName TemplateField 이제 텍스트 상자와는 RequiredFieldValidator 포함 됩니다.](batch-updating-vb/_static/image6.gif)](batch-updating-vb/_static/image9.png)

**그림 6**:는 `ProductName` TemplateField는 이제 텍스트 상자와 RequiredFieldValidator 포함 ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image10.png))


에 대 한는 `UnitPrice` 에서 텍스트를 복사 하 여 시작 편집 인터페이스는 `EditItemTemplate` 에 `ItemTemplate`합니다. 다음으로, 텍스트 상자 및 집합 앞에 $ 배치 해당 `ID` UnitPrice 속성 및 해당 `Columns` 속성을 8로 합니다.

추가적으로를 CompareValidator는 `UnitPrice` s `ItemTemplate` 사용자가 입력 한 값 보다 크거나 같음 $0.00 올바른 통화 값 인지 확인 합니다. 유효성 검사기 s 설정 `ControlToValidate` 속성을 UnitPrice, 해당 `ErrorMessage` 속성을 올바른 통화 값을 입력 해야 합니다. 모든 통화 기호.을 생략 하십시오 해당 `Text` 속성을 \*, 해당 `Type` 속성을 `Currency`, 해당 `Operator` 속성을 `GreaterThanEqual`, 및 해당 `ValueToCompare` 속성을 0입니다.


[![음수 통화 값을 입력 한 가격 되도록 CompareValidator 추가](batch-updating-vb/_static/image7.gif)](batch-updating-vb/_static/image11.png)

**그림 7**: 음수 통화 값을 입력 한 가격 되도록 CompareValidator 추가 ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image12.png))


에 대 한는 `Discontinued` TemplateField에 이미 정의 되어 있는 확인란을 사용할 수 있습니다는 `ItemTemplate`합니다. 설정 하면 해당 `ID` 단종을 및 해당 `Enabled` 속성을 `True`합니다.

## <a name="step-3-creating-thecategorynameediting-interface"></a>3 단계: 만들기는`CategoryName`편집 인터페이스

편집 인터페이스는 `CategoryName` TemplateField s `EditItemTemplate` 의 값을 표시 하는 텍스트 상자가 포함 되어는 `CategoryName` 데이터 필드입니다. 가능한 범주를 나열 하는 DropDownList으로 대체 해야 합니다.

> [!NOTE]
> [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) 자습서에 대 한 자세 하 고 전체 설명을 TextBox 달리 DropDownList를 포함 하도록 템플릿을 사용자 지정이 포함 되어 있습니다. 여기의 단계를 완료 하는 동안 상품 표시 됩니다. 만들기 및 DropDownList 범주 구성에 대 한 자세한 설명에 대 한 다시 참조는 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) 자습서입니다.


도구 상자에서 DropDownList를 끌어는 `CategoryName` TemplateField s `ItemTemplate`설정 해당 `ID` 를 `Categories`합니다. 이 시점에서 우리는 일반적으로 dropdownlist 활용의 데이터 원본 정의 스마트 태그를 통해 새 ObjectDataSource 만들기. 그러나이 내의 ObjectDataSource를 추가 합니다는 `ItemTemplate`, 되 고 각 GridView 행에 대해 만든 ObjectDataSource 인스턴스에 만들어집니다. 대신, 사용 s GridView의 TemplateFields 외부 ObjectDataSource를 만들 수 있습니다. 템플릿 편집을 종료 하 고는 ObjectDataSource 아래 디자이너 도구 상자에서 끌어는 `ProductsDataSource` ObjectDataSource 합니다. 새 ObjectDataSource 이름을 `CategoriesDataSource` 사용 하도록 구성 하 고는 `CategoriesBLL` s 클래스 `GetCategories` 메서드.


[![ObjectDataSource CategoriesBLL 클래스를 사용 하도록 구성](batch-updating-vb/_static/image8.gif)](batch-updating-vb/_static/image13.png)

**그림 8**: 구성에 사용 하 여 ObjectDataSource는 `CategoriesBLL` 클래스 ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image14.png))


[![GetCategories 메서드를 사용 하 여 범주 데이터를 검색 합니다.](batch-updating-vb/_static/image9.gif)](batch-updating-vb/_static/image15.png)

**그림 9**: 사용 하 여 범주 데이터 검색은 `GetCategories` 메서드 ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image16.png))


이 ObjectDataSource 단순히 데이터를 검색 하려면 사용 하 고, (없음)에 UPDATE 및 DELETE 탭에 있는 드롭 다운 목록을 설정 합니다. 마법사를 완료 하려면 마침을 클릭 합니다.


[![집합에 UPDATE 및 DELETE 탭 (없음)을 드롭다운 목록](batch-updating-vb/_static/image10.gif)](batch-updating-vb/_static/image17.png)

**그림 10**: (None)로 업데이트 및 삭제 탭에 드롭다운 목록이 설정 ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image18.png))


마법사를 완료 한 후의 `CategoriesDataSource` s 선언 태그는 다음과 같습니다.


[!code-aspx[Main](batch-updating-vb/samples/sample2.aspx)]

와 `CategoriesDataSource` 를 만들고 구성한 돌아가려면는 `CategoryName` TemplateField의 `ItemTemplate` DropDownList s 스마트 태그에서 데이터 소스 선택 링크를 클릭 합니다. 데이터 소스 구성 마법사에서 선택 된 `CategoriesDataSource` 첫 번째 드롭다운 목록에서 옵션을 사용 하기로 선택한 `CategoryName` 표시에 사용 하 고 `CategoryID` 값으로.


[![드롭다운 목록에서 CategoriesDataSource에 바인딩](batch-updating-vb/_static/image11.gif)](batch-updating-vb/_static/image19.png)

**그림 11**: DropDownList를 바인딩하는 `CategoriesDataSource` ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image20.png))


이 시점에서 `Categories` DropDownList의 범주를 모두 나열 되지만 선택 되지 않습니다 자동으로 아직 GridView 행에 바인딩된 제품에 대 한 적절 한 범주입니다. 설정 해야이를 위해는 `Categories` DropDownList s `SelectedValue` 제품 s `CategoryID` 값입니다. DropDownList s 스마트 태그에서 데이터 바인딩 편집 링크를 클릭 하 고 연결 된 `SelectedValue` 속성을는 `CategoryID` 그림 12에 나와 있는 것 처럼 데이터 필드입니다.


![제품의 CategoryID 값 DropDownList의 SelectedValue 속성에 바인딩](batch-updating-vb/_static/image12.gif)

**그림 12**: 제품 s 바인딩 `CategoryID` DropDownList s에 대 한 값 `SelectedValue` 속성


한 마지막 문제 남아: 제품 대상이 t 있으면는 `CategoryID` 값에 지정 된 다음 데이터 바인딩 문 `SelectedValue` 예외가 발생 합니다. 이므로 DropDownList 범주에 대 한 항목만 포함 되어 있는 해당 제품에 대 한 옵션을 제공 하지 않습니다는 `NULL` 데이터베이스에 대 한 값 `CategoryID`합니다. 이 해결 하려면 설정 DropDownList s `AppendDataBoundItems` 속성을 `True` , 드롭다운 목록에 새 항목 추가 및 생략는 `Value` 선언적 구문에서 속성입니다. 즉, 있는지 확인 하는 `Categories` DropDownList s 선언적 구문은 다음과 같습니다.


[!code-aspx[Main](batch-updating-vb/samples/sample3.aspx)]

참고 방법을 `<asp:ListItem Value="">` -하나 선택-가 `Value` 특성이 명시적으로 빈 문자열로 설정 합니다. 다시 참조는 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) 자습서에 대 한 보다 철저 한 내용은 처리 하기 위해이 추가 DropDownList 항목은 필요한 이유는 `NULL` 대/소문자 및 이유의 할당 된 `Value` 속성을 빈 문자열로 반드시 필요 합니다.

> [!NOTE]
> 잠재적인 성능 및 확장성 문제가 여기 대해서 있습니다. 각 행에 사용 하는 DropDownList 있으므로 `CategoriesDataSource` 를 데이터 원본으로는 `CategoriesBLL` s 클래스 `GetCategories` 메서드는 호출  *n*  페이지 마다 한 번 방문 여기서  *n*  는 GridView에서 행의 수입니다. 이러한  *n*  에 대 한 호출이 `GetCategories` 발생  *n*  데이터베이스에 쿼리 합니다. 요청 캐시 또는 SQL 캐시 종속성 또는 매우 짧은 시간 기반 만료를 사용 하 여 캐싱 계층을 통해 반환 된 범주를 캐시 하 여이 데이터베이스에이 영향을 떨어질 수 수 없습니다. 캐싱 옵션을 당 요청에 대 한 자세한 내용은 참조 [ `HttpContext.Items` 당 요청 캐시 저장소](http://aspnet.4guysfromrolla.com/articles/060904-1.aspx)합니다.


## <a name="step-4-completing-the-editing-interface"></a>4 단계: 완료 편집 인터페이스

म 했습니다 하려고 한 변경 사항을 GridView의 템플릿 우리의 진행 상황을 보려면 일시 중지 하지 않고 있습니다. 잠시 브라우저를 통해 진행률을 볼 수 있습니다. 사용 하 여 각 행은 렌더링 그림 13과 같이 해당 `ItemTemplate`, 셀 s 편집 인터페이스를 포함 하 합니다.


[![각 GridView 행은 편집 가능](batch-updating-vb/_static/image13.gif)](batch-updating-vb/_static/image21.png)

**그림 13**: 각 GridView 행은 편집 가능 ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image22.png))


관리 하는 것은 시점에서 몇 가지 사소한 서식 문제가 있습니다. 첫째, 유의 `UnitPrice` 소수점이 하 4 개를 포함 하는 값입니다. 이 문제를 해결 하려면 반환 된 `UnitPrice` TemplateField의 `ItemTemplate` TextBox s 스마트 태그에서 데이터 바인딩 편집 링크를 클릭 합니다. 다음으로 지정 하는 `Text` 속성 형식을 지정 하는 숫자입니다.


![Text 속성 숫자 형식](batch-updating-vb/_static/image14.gif)

**그림 14**: 형식은 `Text` 숫자로 속성


둘째, let s 가운데에 있는 확인란의 `Discontinued` 열 (대신 왼쪽 맞춤 것). 열 편집 GridView s 스마트 태그에서 클릭 하 고 선택 된 `Discontinued` 왼쪽된 아래 모서리의 필드 목록에서 TemplateField 합니다. 드릴 다운 `ItemStyle` 설정 하 고는 `HorizontalAlign` 그림 15와 같이 센터로 속성입니다.


![지원 되지 않는 확인란 가운데 맞춤](batch-updating-vb/_static/image15.gif)

**그림 15**: 센터는 `Discontinued` 확인란


다음으로 페이지로 ValidationSummary 컨트롤을 추가 하 고 설정의 `ShowMessageBox` 속성을 `True` 및 해당 `ShowSummary` 속성을 `False`합니다. 클릭 하면 단추 웹 컨트롤에, 추가, 사용자 s 변경 내용을 업데이트 합니다. 특히, 컨트롤 두 개 추가 Button 웹, 하나는 GridView 위에 있고 한 수준 아래를 두 컨트롤이 모두 설정 `Text` 속성 업데이트 제품을 합니다.

GridView s 이후 편집 인터페이스에에서 정의 되어 있는 해당 TemplateFields `ItemTemplate` s는 `EditItemTemplate` s 불필요 한 이며 삭제할 수 있습니다.

위의 만드는 서식 변경 앞에서 언급 한 후 단추 컨트롤을 추가 하 고 불필요 한 제거 `EditItemTemplate` s, s 페이지 선언적 구문은 다음과 같습니다.


[!code-aspx[Main](batch-updating-vb/samples/sample4.aspx)]

그림 16 Button 웹 컨트롤을 추가한 후 브라우저를 통해 볼 때이 페이지 및 서식 변경 사항을 보여줍니다.


[![페이지 이제에는 두 개의 업데이트 제품 단추가 포함 되어 있습니다.](batch-updating-vb/_static/image16.gif)](batch-updating-vb/_static/image23.png)

**그림 16**: The 페이지 이제 포함 두 업데이트 제품 단추 ([전체 크기 이미지를 보려면 클릭](batch-updating-vb/_static/image24.png))


## <a name="step-5-updating-the-products"></a>5 단계: 제품 업데이트

사용자가이 페이지를 방문 하는 경우 수정 내용이 및 두 개의 업데이트 제품 단추 중 하나를 클릭 합니다. 어떻게 하 든에 각 행에 대 한 사용자가 입력 한 값을 저장 해야 해당 시점에 `ProductsDataTable` 인스턴스 한 다음 다음 됩니다 전달할 BLL 메서드에 전달할 `ProductsDataTable` DAL s에 인스턴스 `UpdateWithTransaction` 메서드. `UpdateWithTransaction` 메서드를에서 만든는 [이전 자습서](wrapping-database-modifications-within-a-transaction-vb.md)를 원자성 작업으로 일괄 변경 내용 업데이트 합니다.

라는 메서드를 만듭니다 `BatchUpdate` 에 `BatchUpdate.aspx.vb` 다음 코드를 추가 합니다.


[!code-vb[Main](batch-updating-vb/samples/sample5.vb)]

이 메서드는 제품의 모든 시작에 `ProductsDataTable` BLL s에 대 한 호출을 통해 `GetProducts` 메서드. 그런 다음 열거는 `ProductGrid` GridView s [ `Rows` 컬렉션](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.gridview.rows(VS.80).aspx)합니다. `Rows` 컬렉션에 포함 된 [ `GridViewRow` 인스턴스](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.gridviewrow.aspx) GridView에 표시 된 각 행에 대 한 합니다. 최대 10 개의 행 한 페이지에 GridView s 보여 주는 이후 `Rows` 컬렉션 10 개 미만의 항목이 포함 됩니다.

각 행에 대해는 `ProductID` 에서 잡을 `DataKeys` 컬렉션과 적절 한 `ProductsRow` 에서 선택한는 `ProductsDataTable`합니다. 4 개의 TemplateField 입력된 컨트롤 프로그래밍 방식으로 참조 되 고 해당 값에 할당 된는 `ProductsRow` 인스턴스 s 속성입니다. 각 GridView 행의 값이 사용 된 후 업데이트 하는 `ProductsDataTable`, 것 BLL s에 전달 된 s `UpdateWithTransaction` 호출 하는 메서드에, 이전 자습서에서 살펴본 것 처럼 단순히 DAL의 `UpdateWithTransaction` 메서드.

이 자습서에 사용 되는 일괄 처리 업데이트 알고리즘에 따라 각 행을 업데이트는 `ProductsDataTable`의 제품 정보가 변경 되었는지 여부에 관계 없이 GridView에서 행에 해당 하는 합니다. 이러한 blind 클라우드에 없는 t 일반적으로 성능 문제를 업데이트 하는 동안 감사 된 데이터베이스 테이블에 변경 되 면 불필요 한 레코드를 발생할 수 있습니다. 에 [일괄 업데이트 수행](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb.md) 자습서 datalist 인터페이스를 업데이트 하는 일괄 처리를 탐색 하 고 실제로 사용자가 수정한 레코드 업데이트 하는 코드를 추가 합니다. 기술을 사용 하 든 지 자유롭게 [일괄 업데이트 수행](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb.md) 를 원하는 경우이 자습서에서는 코드를 업데이트 합니다.

> [!NOTE]
> 스마트 태그를 통해 GridView에 데이터 소스를 바인딩, Visual Studio에 자동으로 지정 데이터 원본 s 기본 키 값이 값은 GridView의 `DataKeyNames` 속성입니다. 하면에 바인딩되지 않은 ObjectDataSource GridView s 스마트 태그를 통해 GridView의 1 단계에서에서 설명 된 대로 경우 GridView s 수동으로 설정 해야 합니다 `DataKeyNames` 속성에 액세스 하기 위해 ProductID는 `ProductID` 통해 각 행에 대 한 값은 `DataKeys` 컬렉션입니다.


에 사용 되는 코드 `BatchUpdate` BLL s에 사용 되는 비슷합니다 `UpdateProduct` 메서드에 있는 중요 한 차이점은 `UpdateProduct` 메서드 하나만 `ProductRow` 아키텍처에서 인스턴스를 검색 합니다. 속성을 할당 하는 코드는 `ProductRow` 간에 동일한는 `UpdateProducts` 메서드와 내의 코드는 `For Each` 루프 `BatchUpdate`을 있는 그대로 전반적인 패턴입니다.

이 자습서를 완료 하려면 있어야 해야는 `BatchUpdate` 메서드를 호출 하는 경우 업데이트 제품 단추 중 하나를 클릭 합니다. 에 대 한 이벤트 처리기 만들기는 `Click` 이러한 두 항목의 이벤트 단추 컨트롤 및 이벤트 처리기에 다음 코드를 추가 합니다.


[!code-vb[Main](batch-updating-vb/samples/sample6.vb)]

호출할 먼저 `BatchUpdate`합니다. 다음으로 [ `ClientScript` 속성](https://msdn.microsoft.com/en-us/library/system.web.ui.page.clientscript(VS.80).aspx) 업데이트 되었습니다. 제품을 읽을 수 있는 messagebox를 표시 하는 JavaScript를 삽입 하는 데 사용 됩니다.

이 코드를 테스트 하는 데 1 분을 소요 됩니다. 방문 `BatchUpdate.aspx` 브라우저를 통해 된 수의 행을 편집 하 고 업데이트 제품 단추 중 하나를 클릭 합니다. 입력된 유효성 검사 오류가 없는 경우 업데이트 된 제품을 읽을 수 있는 messagebox를 볼 수 있습니다. 업데이트의 원자성을 확인 하려면을 고려해 야 임의 `CHECK` 제약 조건을 허용 하지 않는 것 처럼 `UnitPrice` 1234.56의 값입니다. 다음 `BatchUpdate.aspx`, 다양 한 s 제품 중 하나를 설정 해야 하는 레코드를 편집 `UnitPrice` 값을 사용할 수 없는 값 (1234.56). 원래 값으로 롤백될 일괄 처리 작업을 해당 하는 동안 다른 변경 내용과 업데이트 제품을 클릭 하면 때 오류가 발생 해야 합니다.

## <a name="an-alternativebatchupdatemethod"></a>대신`BatchUpdate`메서드

`BatchUpdate` 방금 메서드 검색 검사 *모든* BLL s에서 제품의 `GetProducts` 메서드 GridView에 표시 되는 해당 레코드를 업데이트 하 고 있습니다. 이 방법은 GridView 페이징, 사용 하지 않지만 용어가 들어 있을 수 있습니다 수백, 수천 또는 수만 개의 제품을 할 수 있지만 GridView에서 10 번만 행 하는 경우에 적합 합니다. 이 경우 모든 제품 수정 그 중 10 개에만 데이터베이스에서은 적합 하지 않습니다.

이러한 종류의 상황에서 다음을 사용 하는 것이 좋습니다 `BatchUpdateAlternate` 메서드 대신:


[!code-vb[Main](batch-updating-vb/samples/sample7.vb)]

`BatchMethodAlternate`비어 있는 새를 만들어 시작 `ProductsDataTable` 라는 `products`합니다. 다음 단계를 통해 GridView s `Rows` 컬렉션의 각 행 BLL s를 사용 하 여 특정 제품 정보를 가져옵니다 `GetProductByProductID(productID)` 메서드. 검색 된 `ProductsRow` 인스턴스에 해당 속성을 동일한 방식으로 업데이트는 `BatchUpdate`, 하지만에 가져온 행을 업데이트 한 후의 `products` `ProductsDataTable` DataTable s 통해 [ `ImportRow(DataRow)` 메서드](https://msdn.microsoft.com/en-us/library/system.data.datatable.importrow(VS.80).aspx).

이후에 `For Each` 루프 완료 `products` 하나가 포함 된 `ProductsRow` GridView의 각 행에 대 한 인스턴스. 각각의 이후는 `ProductsRow` 에 추가 된 인스턴스는 `products` (대신 업데이트)를 맹목적으로 전달 하는 경우는 `UpdateWithTransaction` 메서드는 `ProductsTableAdatper` 레코드의 각 데이터베이스에 삽입 하려고 합니다. 대신, 각이 행의 수정 되었다는 사실을 (추가 됨)을 지정 해야 합니다.

라는 BLL에 새 메서드를 추가 하 여이 작업을 수행할 수 수 `UpdateProductsWithTransaction`합니다. `UpdateProductsWithTransaction`아래에 표시 된 집합의 `RowState` 각각의 `ProductsRow` 인스턴스에 `ProductsDataTable` 를 `Modified` 다음 전달는 `ProductsDataTable` DAL s에 `UpdateWithTransaction` 메서드.


[!code-vb[Main](batch-updating-vb/samples/sample8.vb)]

## <a name="summary"></a>요약

GridView 기본 제공 행 편집 기능을 제공 하지만 지원 완벽 하 게 편집할 수 있는 인터페이스를 만들기 위한를 하지 않습니다. 이 자습서에서 살펴본 것 처럼 이러한 인터페이스 가능 하지만 약간의 작업이 필요 합니다. 모든 행이 편집 가능한 GridView를 만들려면 하 TemplateFields에 GridView의 필드를 변환 하 고 편집 인터페이스 내에서 정의 해야는 `ItemTemplate` s입니다. 또한 업데이트 All-형식 단추 웹 컨트롤을 GridView에서 별도 페이지에 추가 해야 합니다. 이러한 단추 `Click` GridView s 열거 해야 하는 이벤트 처리기 `Rows` 컬렉션에 대 한 변경 내용을 저장 한 `ProductsDataTable`, 업데이트 된 정보를 적절 한 BLL 메서드에 전달 합니다.

다음 자습서를 일괄 삭제에 대 한 인터페이스를 만드는 방법을 살펴보겠습니다. 각 GridView 행 하는 확인란을 포함 하 고 대신 모두를 업데이트 하는 특히-입력 단추, 선택한 행 삭제 단추를 봅시다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Teresa 머피 및 David Suru 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](wrapping-database-modifications-within-a-transaction-vb.md)
[다음](batch-deleting-vb.md)
