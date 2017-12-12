---
uid: web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-detailsview-control-cs
title: "DetailsView 컨트롤 (C#)에서 TemplateFields 사용 | Microsoft Docs"
author: rick-anderson
description: "GridView 사용할 수 있는 동일한 TemplateFields 기능 DetailsView 컨트롤과 함께 사용할 수 있습니다. 이 자습서는 한 제품 축적할 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 83efb21f-b231-446e-9356-f4c6cbcc6713
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-detailsview-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 8004937b758ee1bdb2a2df84c5ea40d47e89dd1c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="using-templatefields-in-the-detailsview-control-c"></a>DetailsView 컨트롤 (C#)에서 TemplateFields 사용
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_13_CS.exe) 또는 [PDF 다운로드](using-templatefields-in-the-detailsview-control-cs/_static/datatutorial13cs1.pdf)

> GridView 사용할 수 있는 동일한 TemplateFields 기능 DetailsView 컨트롤과 함께 사용할 수 있습니다. 이 자습서에서는 TemplateFields 포함 된 DetailsView를 사용 하 여 한 번에 한 제품을 표시 합니다.


## <a name="introduction"></a>소개

TemplateField는 BoundField, CheckBoxField, HyperLinkField, 및 다른 데이터 필드 컨트롤 보다 더 높은 수준의 데이터 렌더링에에서 유연성을 제공합니다. 에 [이전 자습서](using-templatefields-in-the-gridview-control-cs.md) 는 TemplateField을 GridView에서 사용 하 여 살펴보았습니다.

- 한 열에 여러 데이터 필드 값을 표시 합니다. 특히, 둘 다는 `FirstName` 및 `LastName` 필드 한 GridView 열으로 결합 되었습니다.
- 데이터 필드 값을 표현 하는 대체 웹 컨트롤을 사용 합니다. 표시 하는 방법에 살펴보았습니다는 `HiredDate` 달력 컨트롤을 사용 하 여 값입니다.
- 기본 데이터를 기반으로 하는 상태 정보를 표시 합니다. 반면는 `Employees` 테이블 작업에 대 한 직원의 근무 일 수를 반환 하는 열을 포함 하지 않습니다, TemplateField 및 서식 지정 메서드를 사용 하 여 이전 자습서에서 GridView 예제에서 이러한 정보를 표시할 수 있었습니다.

GridView 사용할 수 있는 동일한 TemplateFields 기능 DetailsView 컨트롤과 함께 사용할 수 있습니다. 이 자습서에서는 두 TemplateFields 포함 된 DetailsView를 사용 하 여 한 번에 한 제품을 표시 합니다. 첫 번째 TemplateField는 결합 하는 `UnitPrice`, `UnitsInStock`, 및 `UnitsOnOrder` 한 DetailsView 행에 데이터 필드입니다. 두 번째 TemplateField의 값이 표시 됩니다는 `Discontinued` 필드 있지만 형식 지정 메서드를 사용 하는 경우 "예"를 표시 하려면 `Discontinued` 은 `true`, 그렇지 않은 경우 "NO"입니다.


[![두 개의 TemplateFields는 표시를 사용자 지정 하는 데 사용 됩니다.](using-templatefields-in-the-detailsview-control-cs/_static/image2.png)](using-templatefields-in-the-detailsview-control-cs/_static/image1.png)

**그림 1**: 두 TemplateFields은 표시를 사용자 지정 하는 데 사용 됩니다 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-cs/_static/image3.png))


이제 시작 하겠습니다.

## <a name="step-1-binding-the-data-to-the-detailsview"></a>1 단계: DetailsView에 데이터 바인딩

방금 BoundFields 포함 된 DetailsView 컨트롤을 만들어 시작 한 다음 새 TemplateFields 추가 하거나 기존 BoundFields TemplateFields로 변환 하기 가장 쉽고 방식은 TemplateFields 작업할 때 이전 자습서에서 설명한 것 처럼 필요 . 따라서 DetailsView 디자이너를 통해 페이지를 추가 및 제품 목록을 반환 하는 ObjectDataSource에 바인딩 하 여이 자습서를 시작 합니다. 다음이 단계에 각 제품의 부울이 아닌 값 필드와 한 부울 값 필드 (단종)에 대해 CheckBoxField BoundFields와 DetailsView를 만들어집니다.

열기는 `DetailsViewTemplateField.aspx` 디자이너 도구 상자에서 DetailsView를 끌어서 페이지입니다. DetailsView의 스마트 태그에서 호출 하는 새 ObjectDataSource 컨트롤을 추가 하도록 선택 된 `ProductsBLL` 클래스의 `GetProducts()` 메서드.


[![GetProducts() 메서드를 호출 하는 새 ObjectDataSource 컨트롤 추가](using-templatefields-in-the-detailsview-control-cs/_static/image5.png)](using-templatefields-in-the-detailsview-control-cs/_static/image4.png)

**그림 2**: 새 ObjectDataSource 컨트롤 해당 Invoke 추가 `GetProducts()` 메서드 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-cs/_static/image6.png))


이 보고서에 대 한 제거는 `ProductID`, `SupplierID`, `CategoryID`, 및 `ReorderLevel` BoundFields 합니다. 다음으로 BoundFields 순서를 변경 하는 `CategoryName` 및 `SupplierName` BoundFields 바로 뒤에 나타나야는 `ProductName` BoundField 합니다. 조정할 수 정도 `HeaderText` 속성 및 때 BoundFields에 대 한 서식 속성 적합 하다 고 판단 합니다. 마찬가지로 GridView와 필드 대화 상자 (DetailsView의 스마트 태그의 필드 편집 링크를 클릭 하 여 액세스할 수 있는)를 통해 또는 선언적 구문을 통해 BoundField 수준 편집을 수행할 수 있습니다. DetailsView의 마지막으로, 지울 `Height` 및 `Width` DetailsView 수 있도록 하기 위해 속성 값을 표시 하는 데이터에 따라 확장을 제어 하 고 확인란 페이징 사용에서 스마트 태그에 있습니다.

다음과 같이 변경한 후 DetailsView 컨트롤의 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample1.aspx)]

브라우저를 통해 페이지를 보려면 잠시 시간. 이 시점에서 단일 나열 된 제품 (Chai) 제품의 이름을, 범주, 공급 업체, 가격, 재고, 주문, 단위 및 지원 되지 않는 상태를 보여 주는 행과 함께 표시 됩니다.


[![일련의 BoundFields 사용 하 여 제품의 세부 정보가 표시 됩니다.](using-templatefields-in-the-detailsview-control-cs/_static/image8.png)](using-templatefields-in-the-detailsview-control-cs/_static/image7.png)

**그림 3**: BoundFields 시리즈를 사용 하 여 제품의 세부 정보가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-cs/_static/image9.png))


## <a name="step-2-combining-the-price-units-in-stock-and-units-on-order-into-one-row"></a>한 줄에 가격, 재고, 단위 및 순서에 대 한 단위를 결합 하는 2 단계:

DetailsView에 대 한 행에는 `UnitPrice`, `UnitsInStock`, 및 `UnitsOnOrder` 필드입니다. 결합할 수 있습니다 이러한 데이터 필드에 단일 행을 TemplateField와 새 TemplateField를 추가 하거나 기존 중 하나를 변환 하 여 `UnitPrice`, `UnitsInStock`, 및 `UnitsOnOrder` BoundFields를 TemplateField로 합니다. 개인적으로 기존 BoundFields 변환 않겠습니다를 하는 동안 새 TemplateField를 추가 하 여 연습해 보겠습니다.

필드 대화 상자를 표시 하도록 DetailsView의 스마트 태그에서 필드 편집 링크를 클릭 하 여 시작 합니다. 다음으로 새 TemplateField를 추가 하 고 설정의 `HeaderText` 속성을 "가격 및 인벤토리"로 이동 한다는 위쪽 하므로 새 TemplateField는 `UnitPrice` BoundField 합니다.


[![DetailsView 컨트롤에 새 TemplateField 추가](using-templatefields-in-the-detailsview-control-cs/_static/image11.png)](using-templatefields-in-the-detailsview-control-cs/_static/image10.png)

**그림 4**: 새 TemplateField DetailsView 컨트롤에 추가 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-cs/_static/image12.png))


이 새 TemplateField에 현재 표시 된 값에 포함 되기 때문는 `UnitPrice`, `UnitsInStock`, 및 `UnitsOnOrder` BoundFields, 이제 해당 구성 요소를 제거 합니다.

이 단계에 대 한 마지막 작업을 정의 하는 것은 `ItemTemplate` 가격과 될 수 있는 재고 TemplateField에 대 한 태그 DetailsView의 템플릿 컨트롤의 선언적 구문을 통해 인터페이스를 직접 또는 디자이너에서 편집을 통해 수행 됩니다. GridView에서와 마찬가지로 DetailsView의 템플릿 편집 인터페이스 스마트 태그에서 템플릿 편집 링크를 클릭 하 여 액세스할 수 있습니다. 여기에서 드롭 다운 목록에서 편집한 후 도구 상자에서 웹 컨트롤을 추가 하려면 서식 파일을 선택할 수 있습니다.

이 자습서에 대 한 가격 및 인벤토리 TemplateField 레이블 컨트롤을 추가 하 여 시작 `ItemTemplate`합니다. 다음으로 Label 웹 컨트롤의 스마트 태그에서 데이터 바인딩 편집 링크를 클릭 하 고 바인딩합니다는 `Text` 속성을는 `UnitPrice` 필드입니다.


[![레이블의 텍스트 속성 UnitPrice 데이터 필드에 바인딩](using-templatefields-in-the-detailsview-control-cs/_static/image14.png)](using-templatefields-in-the-detailsview-control-cs/_static/image13.png)

**그림 5**: 레이블이 바인딩하려면 `Text` 속성을는 `UnitPrice` 데이터 필드 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-cs/_static/image15.png))


## <a name="formatting-the-price-as-a-currency"></a>가격으로 통화 서식 지정

이 추가 레이블 웹 컨트롤 가격 및 인벤토리 TemplateField 선택한 제품에 대 한 가격만를 이제 표시 됩니다. 그림 6 브라우저를 통해 볼 때 진행률의 스크린 샷을 지금까지 나와 있습니다.


[![가격 및 인벤토리 TemplateField 가격을 보여 줍니다.](using-templatefields-in-the-detailsview-control-cs/_static/image17.png)](using-templatefields-in-the-detailsview-control-cs/_static/image16.png)

**그림 6**: The 가격 및 인벤토리 TemplateField 가격을 보여 줍니다 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-cs/_static/image18.png))


참고 제품의 가격 통화도 지정 하지 않습니다. BoundField, 서식 지정이 가능을 설정 하 여는 `HtmlEncode` 속성을 `false` 및 `DataFormatString` 속성을 `{0:formatSpecifier}`합니다. 그러나 TemplateField 서식 지정 지침 지정 해야 합니다 databinding 구문 또는 응용 프로그램의 코드 (ASP.NET 페이지의 코드 숨김 클래스 처럼) 내에서 곳에서 정의 된 형식 지정 메서드를 사용 하 여 합니다.

를 웹 컨트롤에 사용 된 데이터 바인딩 구문에 대 한 서식을 지정 하려면 레이블의 스마트 태그에서 데이터 바인딩 편집 링크를 클릭 하 여 데이터 바인딩 대화 상자를 반환 합니다. 서식 명령 형식 드롭 다운 목록에서 직접 입력 하거나 정의 된 형식 문자열 중 하나를 선택할 수 있습니다. BoundField의와 함께 `DataFormatString` 속성을 사용 하 여 지정은 서식을 `{0:formatSpecifier}`합니다.

에 대 한는 `UnitPrice` 적절 한 드롭다운 목록에서 값을 선택 하거나 입력 하 여 지정 된 통화 서식을 사용 하 여 필드 `{0:C}` 직접 합니다.


[![통화도 가격을 서식 지정](using-templatefields-in-the-detailsview-control-cs/_static/image20.png)](using-templatefields-in-the-detailsview-control-cs/_static/image19.png)

**그림 7**: 서식을 통화로 가격 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-cs/_static/image21.png))


서식 사양에 두 번째 매개 변수로 표시 됩니다, 선언적는 `Bind` 또는 `Eval` 메서드. 방금 만든 선언적 태그에 다음 데이터 바인딩 식에서 디자이너 결과 통해 설정:


[!code-aspx[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample2.aspx)]

## <a name="adding-the-remaining-data-fields-to-the-templatefield"></a>TemplateField에 나머지 데이터 필드를 추가합니다.

표시 되 고 서식이 지정 했으므로 시점에서 `UnitPrice` 데이터 필드 가격 및 인벤토리 TemplateField에 없지만 여전히 표시 해야는 `UnitsInStock` 및 `UnitsOnOrder` 필드입니다. 가격 아래와 괄호 안에 줄에서이 표시 해 보겠습니다. 디자이너에서 템플릿 편집 인터페이스에서 이러한 태그는 템플릿 내에서 커서 단순히 표시 될 텍스트를 입력 하 여 추가할 수 있습니다. 또는이 태그는 선언적 구문에서 직접 입력할 수 있습니다.

가격 및 인벤토리 TemplateField 가격 및 인벤토리 정보를 표시 되도록 static 태그, 레이블 웹 컨트롤 및 구문이 추가 같이:

*UnitPrice*  
(**재고 / 순서에:** *UnitsInStock* / *UnitsOnOrder*)

이 작업을 수행한 후 DetailsView의 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample3.aspx)]

이러한 변경 내용으로 작업 한 DetailsView 행에 대 한 가격 및 인벤토리 정보를 통합 했습니다 했습니다.


[![가격 및 인벤토리 정보는 단일 행에 표시 됩니다.](using-templatefields-in-the-detailsview-control-cs/_static/image23.png)](using-templatefields-in-the-detailsview-control-cs/_static/image22.png)

**그림 8**: The 가격 및 인벤토리 정보는 단일 행에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-cs/_static/image24.png))


## <a name="step-3-customizing-the-discontinued-field-information"></a>3 단계: 지원 되지 않는 필드 정보를 사용자 지정

`Products` 테이블의 `Discontinued` 열은 제품이 단종 되었는지 여부를 나타내는 비트 값입니다. DetailsView (또는 GridView) 데이터 소스 컨트롤을 바인딩하는 경우 부울 값 필드와 같은 `Discontinued`, 부울이 아닌 값 필드와 같은 반면 CheckBoxFields로 구현 됩니다 `ProductID`, `ProductName`, 등으로 구현 BoundFields 합니다. CheckBoxField는 그렇지 않으면 데이터 필드의 값은 True이 고 선택 되지 않은 경우 확인란이 비활성화 된 확인란으로 렌더링 합니다.

표시 하지 않고 대신 제품이 지원 되지 않는 여부 나타내는 텍스트를 표시 하는 것이 좋겠습니다 CheckBoxField 합니다. 이렇게 하려면 우리 수 CheckBoxField DetailsView에서 제거한 다음 추가 BoundField 인 `DataField` 속성이로 설정 된 `Discontinued`합니다. 이렇게 하려면 보십시오. 이 변경 후 DetailsView 하면 라는 텍스트가 표시 "true 로" 지원 되지 않는 제품 및 "False"에 대 한 제품 여전히 활성 상태에 대 한 합니다.


[![문자열 True 및 False는 표시할 때 사용 중단 된 상태](using-templatefields-in-the-detailsview-control-cs/_static/image26.png)](using-templatefields-in-the-detailsview-control-cs/_static/image25.png)

**그림 9**: 문자열 True 및 False 사용 되는 지원 되지 않는 상태를 표시 하려면 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-cs/_static/image27.png))


문자열 "True" 또는 "False", "YES"와 "NO" 인 하지만 대신 사용을 만들지 않으려는 한다고 가정 합니다. 이러한 사용자 지정을 사용 하 여를 TemplateField 및 서식 지정 방법을 수행할 수 있습니다. 형식 지정 메서드는 임의 개수의 입력된 매개 변수를 가져올 수 있지만 서식 파일에 삽입할 HTML (문자열)으로 반환 해야 합니다.

서식 지정 메서드를 추가 `DetailsViewTemplateField.aspx` 라는 페이지의 코드 숨김 클래스 `DisplayDiscontinuedAsYESorNO` 부울 입력된 매개 변수로 수락 하 고 문자열을 반환 합니다. 이 메서드는 이전 자습서에 설명 된 대로 *해야* 로 표시 되어야 `protected` 또는 `public` 서식 파일을 액세스할 수 있도록 합니다.


[!code-csharp[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample4.cs)]

이 메서드는 입력된 매개 변수를 확인 (`discontinued`) 경우 "예"를 반환 하 고 `true`, 그렇지 않으면 "NO"입니다.

> [!NOTE]
> 형식 지정 메서드가 포함 될 수 있는 데이터 필드에 전달 된 우리는 이전 자습서 회수 검사에서 `NULL` s 필요가 있는지 확인 하는 직원의 `HiredDate` 속성 값을 데이터베이스를 갖는 `NULL` 하기 전에 값 에 액세스 하는 `EmployeesRow`의 `HiredDate` 속성입니다. 이러한 확인은 이후 여기 필요 하지 않습니다는 `Discontinued` 열 데이터베이스 수 `NULL` 할당 된 값입니다. 또한,이 때문에 부울 입력 매개 변수 대신에 동의 하는 메서드를 사용할 수는 `ProductsRow` 인스턴스 또는 형식 매개 변수가 `object`합니다.


이 서식 지정 방법을 완료 했으므로 이제 남은 것은 TemplateField에서 호출 하 `ItemTemplate`합니다. TemplateField 제거 하거나 만들려면는 `Discontinued` BoundField 새 TemplateField를 추가 하거나 변환 하 고는 `Discontinued` BoundField를 TemplateField로 합니다. 그런 다음 선언 태그 뷰에서 TemplateField를 호출 하는 ItemTemplate만 포함 되도록 편집는 `DisplayDiscontinuedAsYESorNO` 현재 값을 전달 하는 메서드를 `ProductRow` 인스턴스의 `Discontinued` 속성입니다. 이 통해 액세스할 수는 `Eval` 메서드. 특히,는 TemplateField 태그 같이 표시 됩니다.


[!code-aspx[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample5.aspx)]

이렇게 하면는 `DisplayDiscontinuedAsYESorNO` DetailsView를 렌더링할 때 호출 될 메서드를 전달 된 `ProductRow` 인스턴스의 `Discontinued` 값입니다. 이후는 `Eval` 메서드 반환 형식의 값 `object`, 하지만 `DisplayDiscontinuedAsYESorNO` 메서드에서 입력된 매개 변수 형식의 예상 `bool`, 캐스팅 했습니다는 `Eval` 메서드 반환 값을 `bool`합니다. `DisplayDiscontinuedAsYESorNO` 메서드는 다음 반환 하 여 "YES" 또는 "NO" 값에 따라 수신 합니다. 반환 된 값이이 DetailsView에 표시할 항목을 행 (그림 10 참조).


[![예 또는 아니요 값은 이제 지원 되지 않는 행에 표시](using-templatefields-in-the-detailsview-control-cs/_static/image29.png)](using-templatefields-in-the-detailsview-control-cs/_static/image28.png)

**그림 10**: 예 또는 아니요 값은 이제 지원 되지 않는 행에 표시 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-detailsview-control-cs/_static/image30.png))


## <a name="summary"></a>요약

DetailsView 컨트롤에 TemplateField 더 높은 수준의 유연성은 다른 필드 제어 기능과 함께 사용할 수 있는 한 상황에 맞는 이상적인는 데이터를 표시 하면 여기서:

- 여러 개의 데이터 필드를 한 GridView 열에 표시 해야 합니다.
- 데이터는 일반 텍스트 대신 웹 컨트롤을 사용 하 여 가장 잘 표현
- 출력 메타 데이터를 표시 하는 등 또는 데이터를 다시 포맷 기본 데이터에 따라 다릅니다.

TemplateFields는 더 높은 수준의 DetailsView의 기본 데이터 렌더링에 유연성을 허용 하는 동안 DetailsView 출력 여전히 느낌 약간 얻을 각 필드는 HTML의 한 행으로 렌더링 됨에 따라 `<table>`합니다.

FormView 컨트롤은 높은 수준의 렌더링된 된 출력을 구성에 유연성을 제공 합니다. FormView 포함 필드 않으며 일련의 서식 파일 (`ItemTemplate`, `EditItemTemplate`, `HeaderTemplate`등). FormView이 다음 자습서에서는 렌더링 된 레이아웃의 더 많은 제어를 달성 하기 위해 사용 하는 방법을 살펴보겠습니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Dan Jagers 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](using-templatefields-in-the-gridview-control-cs.md)
[다음](using-the-formview-s-templates-cs.md)
