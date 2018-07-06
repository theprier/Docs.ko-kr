---
uid: web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-detailsview-control-vb
title: (VB) DetailsView 컨트롤에서 TemplateFields 사용 | Microsoft Docs
author: rick-anderson
description: GridView를 사용 하 여 사용 가능한 동일한 TemplateFields 기능 DetailsView 컨트롤과 함께 사용할 수 있습니다. 이 자습서에서는 제품 중 하나가 표시 하는 중...
ms.author: aspnetcontent
ms.date: 03/31/2010
ms.assetid: 0b91d5f8-127d-4f6a-b204-f2e2b35ef703
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-detailsview-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 5a994df097148428779c9e219ed08247d47ea1a5
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37821737"
---
<a name="using-templatefields-in-the-detailsview-control-vb"></a>(VB) DetailsView 컨트롤에서 TemplateFields 사용
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_13_VB.exe) 또는 [PDF 다운로드](using-templatefields-in-the-detailsview-control-vb/_static/datatutorial13vb1.pdf)

> GridView를 사용 하 여 사용 가능한 동일한 TemplateFields 기능 DetailsView 컨트롤과 함께 사용할 수 있습니다. 이 자습서에서 TemplateFields를 포함 하는 DetailsView를 사용 하 여 한 번에 한 제품을 표시 됩니다.


## <a name="introduction"></a>소개

TemplateField는 BoundField, CheckBoxField, HyperLinkField, 및 다른 데이터 필드 컨트롤 보다 더 높은 수준의 데이터 렌더링에에서 유연성을 제공합니다. 에 [이전 자습서](using-templatefields-in-the-gridview-control-vb.md) 를 GridView에는 TemplateField를 사용 하 여 살펴보았습니다.

- 한 열에 여러 데이터 필드 값을 표시 합니다. 특히, 둘 다를 `FirstName` 및 `LastName` 필드 하나 GridView 열으로 결합 되었습니다.
- 데이터 필드 값을 표현 하는 대체 웹 컨트롤을 사용 합니다. 표시 하는 방법에 살펴보았습니다는 `HiredDate` 달력 컨트롤을 사용 하 여 값입니다.
- 기본 데이터를 기반으로 하는 상태 정보를 표시 합니다. 하지만 `Employees` TemplateField 및 형식 지정 메서드를 사용 하 여 이전 자습서에서 GridView 예제에서 이러한 정보를 표시할 수 있었습니다, 테이블 작업에는 직원의 근무 하는 일 수를 반환 하는 열이 포함 되지 않습니다.

GridView를 사용 하 여 사용 가능한 동일한 TemplateFields 기능 DetailsView 컨트롤과 함께 사용할 수 있습니다. 이 자습서에서는 두 TemplateFields 포함 된 DetailsView를 사용 하 여 한 번에 한 제품을 표시 됩니다. 첫 번째 templatefield로 결합 합니다 `UnitPrice`, `UnitsInStock`, 및 `UnitsOnOrder` 한 DetailsView 행에 데이터 필드입니다. 두 번째 TemplateField의 값이 표시 됩니다는 `Discontinued` 필드에 있지만 경우 "예"를 표시 하려면 형식 지정 메서드를 사용 `Discontinued` 는 `True`, 그렇지 않은 경우 "아니요"입니다.


[![두 TemplateFields은 표시를 사용자 지정 하는 데 사용 됩니다.](using-templatefields-in-the-detailsview-control-vb/_static/image2.png)](using-templatefields-in-the-detailsview-control-vb/_static/image1.png)

**그림 1**: 두 TemplateFields은 표시를 사용자 지정 하는 데 사용 됩니다 ([큰 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-vb/_static/image3.png))


이제 시작 하겠습니다.

## <a name="step-1-binding-the-data-to-the-detailsview"></a>1 단계: DetailsView에 데이터 바인딩

BoundFields만 포함 된 DetailsView 컨트롤을 만들어 시작한 다음 새 TemplateFields 추가 하거나 기존 BoundFields TemplateFields로 변환할 쉬운 경우가 TemplateFields 작업할 때 이전 자습서에서 설명한 대로 필요한 . 따라서 디자이너를 통해 페이지에는 DetailsView를 추가 및 제품 목록을 반환 하는 ObjectDataSource에 바인딩하지 하 여이 자습서를 시작 합니다. 이러한 단계는 각 제품의 부울이 아닌 값 필드와 한 부울 값 필드 (Discontinued)에 대 한 CheckBoxField BoundFields로는 DetailsView를 만듭니다.

열기는 `DetailsViewTemplateField.aspx` 페이지 및 디자이너 도구 상자에서을 DetailsView를 끕니다. DetailsView의 스마트 태그에서 호출 하는 새 ObjectDataSource 컨트롤을 추가 하려면 선택 합니다 `ProductsBLL` 클래스의 `GetProducts()` 메서드.


[![GetProducts() 메서드를 호출 하 여 새 ObjectDataSource 컨트롤 추가](using-templatefields-in-the-detailsview-control-vb/_static/image5.png)](using-templatefields-in-the-detailsview-control-vb/_static/image4.png)

**그림 2**: 해당 Invoke 새 ObjectDataSource 컨트롤을 추가 합니다 `GetProducts()` 메서드 ([클릭 하 여 큰 이미지 보기](using-templatefields-in-the-detailsview-control-vb/_static/image6.png))


이 보고서를 제거 합니다 `ProductID`, `SupplierID`, `CategoryID`, 및 `ReorderLevel` BoundFields 합니다. 다음으로 BoundFields 다시 정렬 되도록 합니다 `CategoryName` 및 `SupplierName` BoundFields 바로 뒤에 나타나야는 `ProductName` BoundField 합니다. 자유롭게 조정할는 `HeaderText` 속성 및 서식 속성으로 BoundFields 적절 합니다. GridView를 사용 하 여 필드 대화 상자 (DetailsView의 스마트 태그에서 필드 편집 링크를 클릭 하 여 액세스할 수 있음)를 통해 또는 선언적 구문을 통해 이러한 BoundField 수준 편집 작업을 수행할 수 있습니다 예:. DetailsView의 마지막으로 지울 `Height` 고 `Width` DetailsView를 허용 하기 위해 속성 값 표시 되는 데이터에 따라 확장을 제어 하 고 스마트 태그의 페이징 사용 확인란을 확인 합니다.

다음과 같이 변경한 후 DetailsView 컨트롤의 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample1.aspx)]

브라우저를 통해 페이지를 보려면 잠시 시간이 소요 됩니다. 이 시점에서 제품의 이름, 범주, 공급자, 가격, 재고 단위, 순서에 대 한 단위 및 지원 되지 않는 상태를 표시 하는 행이 있는 단일 나열 된 제품 (Chai) 표시 됩니다.


[![제품의 세부 정보를 사용 하 여 BoundFields 같습니다.](using-templatefields-in-the-detailsview-control-vb/_static/image8.png)](using-templatefields-in-the-detailsview-control-vb/_static/image7.png)

**그림 3**: BoundFields 시리즈를 사용 하는 제품의 세부 정보 표시 됩니다 ([큰 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-vb/_static/image9.png))


## <a name="step-2-combining-the-price-units-in-stock-and-units-on-order-into-one-row"></a>행을 가격, 재고 단위 및 순서에 대 한 단위를 결합 하는 2 단계:

DetailsView에 대 한 행을 `UnitPrice`, `UnitsInStock`, 및 `UnitsOnOrder` 필드입니다. 결합할 수 있습니다 이러한 데이터 필드를 단일 행으로 templatefield로 사용 하 여 새 templatefield로 추가 하거나 기존 중 하나를 변환 하 여 `UnitPrice`하십시오 `UnitsInStock`, 및 `UnitsOnOrder` BoundFields를 TemplateField로 합니다. 개인에 필자가 선호 기존 BoundFields 변환 하는 동안 새 templatefield로 추가 하 여 연습해 보겠습니다.

필드 대화 상자를 표시 하도록 DetailsView의 스마트 태그에서 필드 편집 링크를 클릭 하 여 시작 합니다. 그런 다음 새 templatefield로 추가 하 고 설정 해당 `HeaderText` 속성을 "가격 및 인벤토리" 하 고 이동 한다는 위에 배치 됩니다 있도록 새 TemplateField는 `UnitPrice` BoundField 합니다.


[![DetailsView 컨트롤에 새 templatefield로 추가](using-templatefields-in-the-detailsview-control-vb/_static/image11.png)](using-templatefields-in-the-detailsview-control-vb/_static/image10.png)

**그림 4**: 새 templatefield로 DetailsView 컨트롤에 추가 ([큰 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-vb/_static/image12.png))


이 새 TemplateField에 현재 표시 되는 값에 포함 되기 때문 합니다 `UnitPrice`, `UnitsInStock`, 및 `UnitsOnOrder` BoundFields를 제거해 보겠습니다.

이 단계에 대 한 마지막 작업을 정의 하는 것은 `ItemTemplate` 가격 및 해당 되는 인벤토리 TemplateField 태그 DetailsView의 템플릿 컨트롤의 선언적 구문을 통해 인터페이스를 직접 또는 디자이너에서 편집을 통해 수행 합니다. GridView와 DetailsView의 템플릿 편집 인터페이스는 스마트 태그에 있는 템플릿 편집 링크를 클릭 하 여 액세스할 수 있습니다. 여기에서 드롭 다운 목록에서 편집한 후 모든 웹 컨트롤이 도구 상자에서 추가 템플릿을 선택할 수 있습니다.

이 자습서에 대 한 가격 및 인벤토리 TemplateField 레이블 컨트롤을 추가 하 여 시작 `ItemTemplate`합니다. 다음으로 레이블 웹 컨트롤의 스마트 태그의 데이터 바인딩 편집 링크를 클릭 하 고 바인딩하는 `Text` 속성을는 `UnitPrice` 필드.


[![레이블의 텍스트 속성 UnitPrice 데이터 필드에 바인딩](using-templatefields-in-the-detailsview-control-vb/_static/image14.png)](using-templatefields-in-the-detailsview-control-vb/_static/image13.png)

**그림 5**: 레이블의 바인딩할 `Text` 속성을 합니다 `UnitPrice` 데이터 필드 ([클릭 하 여 큰 이미지 보기](using-templatefields-in-the-detailsview-control-vb/_static/image15.png))


## <a name="formatting-the-price-as-a-currency"></a>가격은 통화로 서식 지정

이 또한이를 사용 하 여 레이블 웹 컨트롤 가격 및 인벤토리 TemplateField 선택한 제품에 대 한 가격만를 이제 표시 됩니다. 그림 6 브라우저를 통해 볼 때 지금 스크린샷을 진행 상황을 보여줍니다.


[![가격 및 인벤토리 TemplateField 가격을 보여 줍니다.](using-templatefields-in-the-detailsview-control-vb/_static/image17.png)](using-templatefields-in-the-detailsview-control-vb/_static/image16.png)

**그림 6**:의 가격 및 인벤토리 TemplateField 가격을 보여 줍니다 ([큰 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-vb/_static/image18.png))


제품의 가격 통화로 포맷 되지 않은 참고 합니다. BoundField 서식 지정 된 수를 설정 하 여 합니다 `HtmlEncode` 속성을 `False` 하며 `DataFormatString` 속성을 `{0:formatSpecifier}`입니다. 그러나 TemplateField 서식 지정 지침 지정 해야 합니다 데이터 바인딩 구문 또는 응용 프로그램의 코드 (예: ASP.NET 페이지의 코드 숨김 클래스와 같이) 내 임의 위치에 정의 된 형식 지정 메서드를 사용 하 여 합니다.

웹 컨트롤에 사용 된 데이터 바인딩 구문에 대 한 서식 지정을 지정 하려면 레이블의 스마트 태그에서 데이터 바인딩 편집 링크를 클릭 하 여 데이터 바인딩 대화 상자를 반환 합니다. 형식 드롭다운 목록에서 직접 서식 지정 지침을 입력 하거나 정의 된 형식 문자열 중 하나를 선택할 수 있습니다. BoundField의와 마찬가지로 `DataFormatString` 속성인을 사용 하 여 지정 된 서식 지정 `{0:formatSpecifier}`합니다.

에 대 한 합니다 `UnitPrice` 사용 하 여 적절 한 드롭다운 목록에서 값을 선택 하거나 입력 하 여 지정 된 통화 서식 지정 필드 `{0:C}` 손으로 합니다.


[![가격 통화 서식](using-templatefields-in-the-detailsview-control-vb/_static/image20.png)](using-templatefields-in-the-detailsview-control-vb/_static/image19.png)

**그림 7**: 형식을 통화로 가격 ([큰 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-vb/_static/image21.png))


서식 사양에 두 번째 매개 변수로 표시 됩니다는 선언적으로 정의 된 `Bind` 또는 `Eval` 메서드. 디자이너 결과 선언적 태그에 다음 데이터 바인딩 식을 통해 방금 만든 설정을:


[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample2.aspx)]

## <a name="adding-the-remaining-data-fields-to-the-templatefield"></a>나머지 데이터 필드를 templatefield로 추가

이 시점에서는 표시 하 고 형식이 지정 합니다 `UnitPrice` 데이터 가격 및 인벤토리 TemplateField 필드가 있지만 여전히 표시 해야 합니다 `UnitsInStock` 및 `UnitsOnOrder` 필드. 가격은 아래와 괄호 안에 줄에서 이러한 값을 표시 해 보겠습니다. 디자이너에서 템플릿 편집 인터페이스에서 이러한 태그는 템플릿 내에서 커서 위치 지정 하기만 하면 표시할 텍스트를 입력 하 여 추가할 수 있습니다. 또는이 태그는 선언적 구문에서 직접 입력할 수 있습니다.

가격 및 인벤토리 TemplateField 가격 및 인벤토리 정보를 표시 되도록 정적 태그, 레이블 웹 컨트롤 및 데이터 바인딩 구문을 추가 다음과 같이 합니다.

*UnitPrice*  
(**재고 / 주문:** *UnitsInStock* / *UnitsOnOrder*)

이 작업을 수행한 후 DetailsView의 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample3.aspx)]

이러한 변경 내용으로 단일 DetailsView 행에 가격 및 인벤토리 정보를 통합 했으며 합니다.


[![가격 및 인벤토리 정보를 단일 행에 표시 됩니다.](using-templatefields-in-the-detailsview-control-vb/_static/image23.png)](using-templatefields-in-the-detailsview-control-vb/_static/image22.png)

**그림 8**:의 가격 및 인벤토리 정보는 단일 행에 표시 됩니다 ([큰 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-vb/_static/image24.png))


## <a name="step-3-customizing-the-discontinued-field-information"></a>3 단계: 지원 되지 않는 필드 정보를 사용자 지정

합니다 `Products` 테이블의 `Discontinued` 열은 제품이 단종 되었는지 여부를 나타내는 비트 값입니다. DetailsView (또는 GridView) 데이터 소스 컨트롤을 바인딩하는 경우 부울 값 필드와 같은 `Discontinued`에 부울이 아닌 값 필드와 같은 반면 CheckBoxFields로 구현 됩니다 `ProductID`, `ProductName`, 등으로 구현 됩니다 BoundFields 합니다. CheckBoxField 그렇지 않은 경우 데이터 필드의 값은 True이 고 확인 되지 않은 경우 검사는 비활성화 된 확인란으로 렌더링 합니다.

표시 하지 않고 대신 제품이 단종 된 지 여부를 나타내는 텍스트를 표시 해야 할 수도 있으므로 CheckBoxField 합니다. 이렇게 하려면에서는 수를 CheckBoxField DetailsView에서 제거한 다음 추가 BoundField입니다 `DataField` 속성 설정한 `Discontinued`합니다. 시간을 내어이 작업을 수행 합니다. 이 변경 후 DetailsView 텍스트가 표시 "true 로" 지원 되지 않는 제품 및 "False" 여전히 활성화 되어 있는 제품에 대 한 합니다.


[![True 및 False는 사용 하는 지원 되지 않는 상태를 표시 하려면](using-templatefields-in-the-detailsview-control-vb/_static/image26.png)](using-templatefields-in-the-detailsview-control-vb/_static/image25.png)

**그림 9**: 문자열 True 및 False 되는 지원 되지 않는 상태를 표시 하려면 ([큰 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-vb/_static/image27.png))


문자열 "True" 또는 "False", "YES" 및 "NO" 인 대신 사용할을 않으려는 가정해 보겠습니다. 이러한 사용자 지정 된 templatefield로 및 형식 지정 메서드를 사용 하 여 수행할 수 있습니다. 형식 지정 메서드는 임의 개수의 입력된 매개 변수에서 가져올 수 있지만 템플릿에 삽입할 (문자열로) HTML을 반환 해야 합니다.

서식 지정 메서드를 추가 하는 `DetailsViewTemplateField.aspx` 라는 페이지의 코드 숨김 클래스 `DisplayDiscontinuedAsYESorNO` 받아들이는 `Northwind.ProductsRow` 개체를 입력된 매개 변수로 문자열을 반환 합니다. 이 메서드는 이전 자습서에서 설명 했 듯이 *해야 합니다* 로 표시 되어야 `Protected` 또는 `Public` 템플릿에서 액세스할 수 있도록 합니다.


[!code-vb[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample4.vb)]

이 메서드는 입력된 매개 변수 확인 (`discontinued`) 경우 "예"를 반환 하 고 `True`고, 그렇지 않으면 "아니요"입니다.

> [!NOTE]
> 포함 될 수 있는 데이터 필드에서 통과 된 것은 이전 자습서 회수 검사할 서식 지정 메서드에 `NULL` s 고 따라서 확인 하는 데 필요한 직원의 `HiredDate` 속성 값을 데이터베이스 했습니다 `NULL` 값 이전 에 액세스 하는 `EmployeesRow`의 `HiredDate` 속성입니다. 이러한 확인은 되었으므로 여기 필요 하지 않습니다 합니다 `Discontinued` 열 데이터베이스를 가질 수 `NULL` 할당 된 값입니다. 또한이 때문에 메서드가 부울 값을 허용 하지 않고 매개 변수 입력을 수락할 수를 `ProductsRow` 인스턴스 또는 형식 매개 변수가 `Object`합니다.


전체이 서식 지정 메서드를 사용 하 여 주기를 TemplateField의에서 호출 해야 `ItemTemplate`합니다. TemplateField를 제거 하거나 만들려면 합니다 `Discontinued` BoundField 새 templatefield로 추가 하거나 변환 합니다 `Discontinued` BoundField를 TemplateField로 합니다. 그런 다음 선언적 태그 뷰에서 templatefield로 호출 하는 ItemTemplate만 포함 되도록 편집 합니다 `DisplayDiscontinuedAsYESorNO` 메서드를 현재 값을 전달 `ProductRow` 인스턴스의 `Discontinued` 속성입니다. 이 통해 액세스할 수는 `Eval` 메서드. 특히를 TemplateField 태그 같이 표시 됩니다.


[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample5.aspx)]

이렇게 하면 합니다 `DisplayDiscontinuedAsYESorNO` DetailsView를 렌더링할 때 호출 될 메서드를 전달 합니다 `ProductRow` 인스턴스의 `Discontinued` 값. 하므로 `Eval` 형식의 값을 반환 하는 메서드 `Object`, 하지만 `DisplayDiscontinuedAsYESorNO` 메서드는 형식의 입력된 매개 변수를 필요로 `Boolean`, 캐스팅 했습니다를 `Eval` 메서드 반환 값을 `Boolean`. `DisplayDiscontinuedAsYESorNO` 메서드는 다음 반환 하 여 "YES" 또는 "NO" 값에 따라 수신 합니다. 반환된 된 값이이 DetailsView에 표시 되는 항목을 행 (그림 10 참조).


[![예 또는 아니요 값은 이제 지원 되지 않는 행에 표시](using-templatefields-in-the-detailsview-control-vb/_static/image29.png)](using-templatefields-in-the-detailsview-control-vb/_static/image28.png)

**그림 10**: 예 또는 아니요 값 이제 지원 되지 않는 행에 표시 됩니다 ([큰 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-vb/_static/image30.png))


## <a name="summary"></a>요약

DetailsView 컨트롤에서 TemplateField는 높은 수준의 유연성을 사용할 수 있는 다른 필드 컨트롤을 사용 하 여 상황에 적합 한 보다 데이터를 표시 하면 여기서:

- 여러 데이터 필드를 하나의 GridView 열에 표시 해야 합니다.
- 데이터는 일반 텍스트가 아닌 웹 컨트롤을 사용 하 여 표현 가장
- 출력은 데이터를 다시 포맷 또는 메타 데이터 표시와 같은 기본 데이터에 따라 달라 집니다.

TemplateFields 뛰어난 DetailsView의 기본 데이터 렌더링에 유연성을 허용 하는 동안 DetailsView 출력 여전히 느낌 약간 얻을 각 필드가 HTML에 행으로 렌더링 되는 대로 `<table>`입니다.

FormView 컨트롤이 유연 하 게 렌더링 된 출력을 구성할 제어력을 제공 합니다. FormView 필드는 없지만 일련의 서식 파일 대신 방금 없습니다 (`ItemTemplate`, `EditItemTemplate`, `HeaderTemplate`등). 다음 자습서에서 렌더링 된 레이아웃의 더 많은 제어를 위해 FormView를 사용 하는 방법을 살펴보겠습니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Dan Jagers 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](using-templatefields-in-the-gridview-control-vb.md)
> [다음](using-the-formview-s-templates-vb.md)
