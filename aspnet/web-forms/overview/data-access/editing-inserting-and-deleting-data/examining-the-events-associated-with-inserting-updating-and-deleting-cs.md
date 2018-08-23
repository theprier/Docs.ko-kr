---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs
title: 삽입, 업데이트 및 삭제 (C#)와 관련 된 이벤트 검사 | Microsoft Docs
author: rick-anderson
description: 이전, 도중 및 삽입 이후 발생 하는 이벤트를 사용 하 여 살펴보겠습니다이 자습서에서는 업데이트 또는 ASP.NET 데이터 웹 컨트롤의 작업을 삭제 합니다. W...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: dab291a0-a8b5-46fa-9dd8-3d35b249201f
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs
msc.type: authoredcontent
ms.openlocfilehash: d8a16500388acd331042b7a9d62cf710edf3c61a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41839119"
---
<a name="examining-the-events-associated-with-inserting-updating-and-deleting-c"></a>삽입, 업데이트 및 삭제 (C#)와 관련 된 이벤트 검사
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_17_CS.exe) 또는 [PDF 다운로드](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/datatutorial17cs1.pdf)

> 이전, 도중 및 삽입 이후 발생 하는 이벤트를 사용 하 여 살펴보겠습니다이 자습서에서는 업데이트 또는 ASP.NET 데이터 웹 컨트롤의 작업을 삭제 합니다. 또한만 제품 필드의 하위 집합을 업데이트 하려면 편집 인터페이스 사용자 지정 하는 방법을 알아봅니다.


## <a name="introduction"></a>소개

기본 삽입, 편집 또는 삭제 GridView, FormView DetailsView 컨트롤의 기능을 사용 하 여, 다양 한 단계 동안 최종 사용자가 새 레코드를 추가 또는 업데이트 하거나 기존 레코드를 삭제 하는 프로세스를 완료를 실행 합니다. 설명한 대로 합니다 [이전 자습서](an-overview-of-inserting-updating-and-deleting-data-cs.md)편집 단추를 업데이트 및 Cancel 단추 및 텍스트 상자에 BoundFields 설정으로 바뀝니다 GridView의 행을 편집 하는 경우, 합니다. 최종 사용자 데이터를 업데이트 하 고 업데이트를 클릭 한 후 다음 단계를 다시 게시 될 때 수행 됩니다.

1. GridView의 ObjectDataSource의 채웁니다 `UpdateParameters` 편집할된 레코드의 고유 식별 필드를 사용 하 여 (통해는 `DataKeyNames` 속성) 사용자가 입력 한 값과 함께
2. GridView의 ObjectDataSource의 호출 `Update()` 메서드 내부 개체에 적절 한 메서드를 호출 (`ProductsDAL.UpdateProduct`, 이전 자습서에서)
3. 이제 업데이트 된 변경 내용을 포함 하는 기본 데이터를 GridView에 다시 바인딩되

이 일련의 단계 동안 이벤트 수가 발생 빠르므로 우리는 사용자 지정 논리를 추가할 이벤트 처리기를 만드는 경우 필요 합니다. 1 단계에서 GridView의 이전 예를 들어 `RowUpdating` 이벤트가 발생 합니다. 이 시점에서 일부 유효성 검사 오류가 있을 경우 업데이트 요청을 취소 수 있습니다. 경우는 `Update()` 메서드를 호출 하면 ObjectDataSource의 `Updating` 를 추가 하 여 모든 값을 사용자 지정할 수 있는 기회를 제공 하는 이벤트 발생 되는 `UpdateParameters`합니다. 개체의 메서드를 실행 하 고 ObjectDataSource의 완료 후 ObjectDataSource의 기본 `Updated` 이벤트가 발생 합니다. 에 대 한 이벤트 처리기는 `Updated` 이벤트 영향을 받은 행 수 및 예외가 발생 여부와 같은 업데이트 작업에 대 한 세부 정보를 검사할 수 있습니다. 마지막으로, 2 단계 후 GridView의 `RowUpdated` 수행만 업데이트 작업에 대 한 추가 정보를 검토 합니다.이 이벤트 수에 대 한 이벤트 처리기; 이벤트가 발생 합니다.

그림 1은 GridView를 업데이트할 때이 일련을의 이벤트 및 단계를 보여 줍니다. 그림 1의 이벤트 패턴에는 GridView를 사용 하 여 업데이트에 고유 하지 않습니다. 삽입, 업데이트 또는 GridView에서 데이터 삭제, DetailsView 또는 FormView precipitates ObjectDataSource와 데이터 웹 컨트롤에 대 한 사전 및 사후 수준 이벤트의 순서입니다.


[![일련의 사전 및 사후 이벤트 발생을 GridView에는 데이터를 업데이트 하는 경우](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image2.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image1.png)

**그림 1**: A 시리즈의 사전 및 사후 이벤트 발생 때 업데이트 데이터 GridView의 ([큰 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image3.png))


이러한 이벤트를 사용 하 여 기본 제공 삽입 확장할 살펴보겠습니다이 자습서에서는 업데이트 및 삭제 기능 ASP.NET 데이터 웹 제어 합니다. 또한만 제품 필드의 하위 집합을 업데이트 하려면 편집 인터페이스 사용자 지정 하는 방법을 알아봅니다.

## <a name="step-1-updating-a-productsproductnameandunitpricefields"></a>1 단계: 제품의 업데이트`ProductName`고`UnitPrice`필드

이전 자습서의 편집 인터페이스에서 *모든* 제품 필드 되지 않은 읽기 전용으로 포함 해야 합니다. GridView-에서 필드를 제거 한다고 말할 `QuantityPerUnit` 데이터 웹 컨트롤 데이터를 업데이트 하는 ObjectDataSource의 설정 되지 않은 경우- `QuantityPerUnit` `UpdateParameters` 값입니다. ObjectDataSource에 전달 합니다는 `null` 값을 `UpdateProduct` 계층 BLL (비즈니스 논리) 메서드를 편집된 하는 데이터베이스 레코드의 변경 `QuantityPerUnit` 열을는 `NULL` 값. 마찬가지로 경우 필수 필드를 같은 `ProductName`를 제거 됩니다 편집 인터페이스에서 업데이트를 사용 하 여 실패를 "*'ProductName' 열은 null을 허용 하지 않습니다*" 예외입니다. ObjectDataSource 호출 구성 되었기 때문에이 동작에 대 한 이유는를 `ProductsBLL` 클래스의 `UpdateProduct` 메서드를 각 제품 필드에 대 한 입력된 매개 변수를 예상 합니다. 따라서 ObjectDataSource의 `UpdateParameters` 컬렉션 매개 변수 입력 메서드의 각 매개 변수를 포함 합니다.

최종 사용자만 필드의 하위 집합을 업데이트할 수 있도록 웹 컨트롤에 데이터를 제공 하려는 경우 하거나 누락 된 프로그래밍 방식으로 설정 해야 `UpdateParameters` ObjectDataSource의 값 `Updating` 이벤트 처리기 또는 만들고는 BLL 메서드를 호출 필드의 하위 집합만이 필요합니다. 이 방법을 통해 살펴보겠습니다.

특히, 표시 되는 페이지를 만들어 보겠습니다 요소만 `ProductName` 및 `UnitPrice` 는 편집 가능한 GridView의 필드입니다. 이 GridView의 편집 인터페이스는 두 개의 표시 된 필드를 업데이트할 사용자만 허용 `ProductName` 고 `UnitPrice`입니다. 하거나 기존 BLL을 사용 하는 ObjectDataSource 생성 해야 하므로 편집이 인터페이스는 제품의 필드의 하위 집합에서 제공 `UpdateProduct` 메서드는 누락 된 제품 필드 값 설정에 프로그래밍 방식으로 해당 `Updating` 이벤트 처리기 시키거나 GridView에 정의 된 필드의 하위 집합만 필요로 하는 새 BLL 메서드를 만들기 위해 필요 합니다. 이 자습서에서는 보겠습니다 후자 옵션을 사용 하 여 만들고의 오버 로드 된 `UpdateProduct` 메서드를 세 개의 입력된 매개 변수에서 사용 하는 하나의: `productName`를 `unitPrice`, 및 `productID`:


[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample1.cs)]

원래와 같은 `UpdateProduct` 메서드를 지정 된 데이터베이스에 제품 인지 확인 하 여 시작 된이 오버 로드 `ProductID`합니다. 반환 된 그렇지 않은 경우 `false`, 제품 정보를 업데이트 요청이 실패 했음을 나타냅니다. 기존 제품 레코드의 업데이트이 고, 그렇지 `ProductName` 하 고 `UnitPrice` 그에 따라 필드 및 TableAdpater의 호출 하 여 업데이트를 커밋합니다 `Update()` 전달 하는 메서드는 `ProductsRow` 인스턴스.

이 추가 사용 하 여이 `ProductsBLL` 클래스 준비가 간소화 된 GridView 인터페이스를 만듭니다. 열기는 `DataModificationEvents.aspx` 에 `EditInsertDelete` 폴더 페이지에 GridView를 추가 합니다. 새 ObjectDataSource를 만들고 사용 하도록 구성 합니다 `ProductsBLL` 클래스와 해당 `Select()` 메서드 매핑을 `GetProducts` 및 해당 `Update()` 메서드 매핑을 `UpdateProduct` 만 사용 하는 오버 로드를 `productName`, `unitPrice`, 및 `productID` 매개 변수를 입력 합니다. 그림 2는 ObjectDataSource를 매핑할 때 데이터 원본 만들기 마법사를 보여 줍니다 `Update()` 메서드를 `ProductsBLL` 클래스의 새 `UpdateProduct` 메서드 오버 로드 합니다.


[![새 UpdateProduct 오버 로드를 map ObjectDataSource의 update () 메서드](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image5.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image4.png)

**그림 2**: ObjectDataSource의 매핑 `Update()` 새로 만들기 방법 `UpdateProduct` 오버 로드 ([클릭 하 여 큰 이미지 보기](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image6.png))


이 예에서 수 데이터를 편집할 수 있지만 하지 삽입 또는 레코드 삭제에 필요한 처음에 있으므로 잠시 명시적으로 나타내기 위해 ObjectDataSource의 `Insert()` 하 고 `Delete()` 메서드 중 하나에 매핑할 수 없습니다는 `ProductsBLL` INSERT 및 DELETE 탭으로 이동 하 고 드롭다운 목록에서 (없음)를 선택 하 여 클래스의 메서드.


[![(없음) 삽입 및 삭제 탭에 대 한 드롭다운 목록에서 선택](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image8.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image7.png)

**그림 3**: (None) 삽입 및 삭제 하는 탭의 드롭다운 목록에서 선택 ([큰 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image9.png))


이 마법사를 완료 한 후 GridView의 스마트 태그에서 편집 사용 확인란을 확인 합니다.

가 완료 되 면 데이터 원본 만들기 마법사 및 GridView에 바인딩을 사용 하 여 Visual Studio는 모두 컨트롤에 대 한 선언적 구문을 만들었습니다. ObjectDataSource의 선언 태그 아래 검사 하 여 원본 뷰로 이동 합니다.


[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample2.aspx)]

Objectdatasource의 매핑이 있으므로 `Insert()` 하 고 `Delete()` 메서드를 가지 없습니다 `InsertParameters` 또는 `DeleteParameters` 섹션입니다. 또한 이후 합니다 `Update()` 메서드가 매핑되는 `UpdateProduct` 세 개의 입력된 매개 변수를 허용 하는 메서드 오버 로드는 `UpdateParameters` 섹션에는 3 개의 방금 `Parameter` 인스턴스.

ObjectDataSource의 `OldValuesParameterFormatString` 속성이 `original_{0}`합니다. 이 속성은 데이터 소스 구성 마법사를 사용 하는 경우 Visual Studio에서 자동으로 설정 됩니다. 그러나 BLL 메서드는 원래 예상 하지 되므로 `ProductID` 값 전달, ObjectDataSource의 선언적 구문에서이 속성 할당을 완전히 제거 합니다.

> [!NOTE]
> 단순히 지울 경우는 `OldValuesParameterFormatString` 속성은 디자인 뷰에서 속성 창에서 속성 값의 선언적 구문에는 여전히 존재 하지만 빈 문자열로 설정 됩니다. 제거 하거나 완전히 선언적 구문에서 또는 속성 창에서 설정 값을 기본값으로 `{0}`합니다.


ObjectDataSource에 있지만 `UpdateParameters` 제품의 이름, 가격 및 ID에 대 한 Visual Studio에 추가 되었습니다 BoundField 또는 CheckBoxField GridView에서 각 제품의 필드에 대 한 합니다.


[![각 제품의 필드에 대 한 BoundField 또는 CheckBoxField를 포함 하는 GridView](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image11.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image10.png)

**그림 4**: 각 제품의 필드에 대 한 BoundField 또는 CheckBoxField를 포함 하는 GridView ([큰 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image12.png))


최종 사용자는 제품을 편집 하 고 해당 업데이트 단추 클릭 하면, GridView 없습니다. 읽기 전용 필드를 열거 합니다. ObjectDataSource의의 해당 매개 변수의 값을 설정 합니다 `UpdateParameters` 사용자가 입력 한 값 컬렉션입니다. 해당 매개 변수가 없는 경우 GridView를 컬렉션에 추가 합니다. 따라서이 GridView BoundFields 및 모든 제품의 필드에 대 한 CheckBoxFields 있으면 ObjectDataSource 결국 호출을 `UpdateProduct` 모든 팩트 불구 하 고 이러한 매개 변수를 사용 하는 오버 로드는 ObjectDataSource의 선언적 태그 (그림 5 참조) 세 개의 입력된 매개 변수를 지정 합니다. 마찬가지로, 일부 조합 읽기 전용이 아닌 경우 제품 필드에 대 한 입력 매개 변수에 해당 하지 않는 GridView는 `UpdateProduct` 오버 로드를 업데이트 하려고 시도할 때 예외가 발생 합니다.


[![GridView는 ObjectDataSource의 UpdateParameters 컬렉션에 매개 변수 추가](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image14.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image13.png)

**그림 5**: The GridView는 추가 매개 변수를는 ObjectDataSource `UpdateParameters` 컬렉션 ([클릭 하 여 큰 이미지 보기](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image15.png))


ObjectDataSource 호출 되도록 합니다 `UpdateProduct` 제품의 이름, 가격 및 ID를 사용 하는 오버 로드에 대 한 편집 가능한 필드에 GridView를 제한 해야만 `ProductName` 및 `UnitPrice`합니다. 이러한 다른 필드를 설정 하 여 다른 BoundFields 및 CheckBoxFields를 제거 하 여이 작업을 수행할 수 있습니다 `ReadOnly` 속성을 `true`, 또는 둘의 조합입니다. 이 자습서에서는 단순히 제거를 제외한 모든 GridView 필드를 `ProductName` 및 `UnitPrice` BoundFields, 지나면 GridView의 선언적 태그 처럼 보입니다.


[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample3.aspx)]

경우에는 `UpdateProduct` 오버 로드 세 개의 입력된 매개 변수, 우리의 GridView의 두 BoundFields만 있습니다. 왜냐하면 합니다 `productID` 입력된 매개 변수는 기본 키 값 및의 값을 통해 전달 된를 `DataKeyNames` 편집된 된 행에 대 한 속성입니다.

우리의 GridView와 함께 `UpdateProduct` 오버 로드를 다른 제품 필드의 손실 없이 이름 및 제품의 가격을 편집할 수 있습니다.


[![인터페이스 바로 제품의 이름 및 Price를 편집할 수 있습니다.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image17.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image16.png)

**그림 6**: 방금 제품의 이름과 가격 편집 인터페이스 허용 ([큰 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image18.png))


> [!NOTE]
> 이전 자습서에서 설명 했 듯이 것은 매우 중요 GridView가의 뷰 상태 수 (기본 동작)을 사용할 수 있도록 합니다. GridView가 설정 하는 경우 `EnableViewState` 속성을 `false`, 동시 사용자가 실수로 삭제 하거나 편집할 레코드의 위험이 있습니다. 참조 [경고: 동시성 문제 사용 하 여 ASP.NET 2.0 Gridview/DetailsView/FormViews 해당 지원 편집 및/또는 삭제 하 고 있는 뷰 상태를 사용 하지 않도록 설정](http://scottonwriting.net/sowblog/archive/2006/10/03/163215.aspx) 자세한 내용은 합니다.


## <a name="improving-theunitpriceformatting"></a>향상 된`UnitPrice`서식 지정

그림 6 작동의 GridView 예제 동안는 `UnitPrice` 필드 형식이 전혀, 기호 및 네 개의 소수 자릿수가 없는 모든 통화 가격이 표시를 생성 합니다. 편집할 수 없는 행의 서식을 통화에 적용 하려면 설정 하기만 합니다 `UnitPrice` BoundField의 `DataFormatString` 속성을 `{0:c}` 고 `HtmlEncode` 속성을 `false`입니다.


[![UnitPrice의 DataFormatString 및 HtmlEncode 속성을 적절 하 게 설정](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image20.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image19.png)

**그림 7**: 설정 합니다 `UnitPrice`의 `DataFormatString` 하 고 `HtmlEncode` 적절 하 게 속성 ([클릭 하 여 큰 이미지 보기](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image21.png))


가격 통화;으로 편집할 수 없는 행이 변경으로 형식 하지만 편집된 된 행 여전히 표시 통화 기호 없이 네 개의 소수 자릿수로 값입니다.


[![편집할 수 없는 행은 이제 서식이 지정 된 통화 값으로](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image23.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image22.png)

**그림 8**: 편집할 수 없는 행은 이제 통화 값으로 형식이 지정 ([큰 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image24.png))


에 지정 된 서식 지정 지침의 `DataFormatString` BoundField의을 설정 하 여 편집 인터페이스에 적용할 수 속성 `ApplyFormatInEditMode` 속성을 `true` (기본값인 `false`). 이 속성을 설정 하려면 잠시 `true`입니다.


[![UnitPrice BoundField의 ApplyFormatInEditMode 속성도 true로 설정](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image26.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image25.png)

**그림 9**: 설정 된 `UnitPrice` BoundField의 `ApplyFormatInEditMode` 속성을 `true` ([클릭 하 여 큰 이미지 보기](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image27.png))


값이이 변경으로는 `UnitPrice` 는 편집에 표시 된 행으로 포맷 합니다.


[![편집한 행의 UnitPrice 값은 이제 서식이 지정 된 통화로](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image29.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image28.png)

**그림 10**: The 편집할 행의 `UnitPrice` 이제는 통화 단위로 지정 하는 것이 가치가 ([클릭 하 여 큰 이미지 보기](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image30.png))


그러나 $19.00 throw와 같은 텍스트 상자에 통화 기호를 사용 하 여 제품 업데이트를 `FormatException`입니다. GridView는 ObjectDataSource에 사용자가 제공한 값을 할당 하려고 할 때 `UpdateParameters` 변환할 수 없는 컬렉션을 `UnitPrice` "$19.00" 문자열을 `decimal` 매개 변수에 필요한 (그림 11 참조). 이 해결 하는 GridView에 대 한 이벤트 처리기를 만들 수 있습니다 `RowUpdating` 이벤트는 사용자가 제공한 구문 분석 하도록 `UnitPrice` 통화 서식 지정으로 `decimal`입니다.

GridView의 `RowUpdating` 이벤트 형식의 개체를 두 번째 매개 변수로 수락 [GridViewUpdateEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewupdateeventargs(VS.80).aspx)를 포함 하는 `NewValues` 사전 준비 되도록 사용자가 제공한 값을 보유 하는 해당 속성 중 하나로 ObjectDataSource의 할당할 `UpdateParameters` 컬렉션입니다. 기존 덮어쓸 수 것 `UnitPrice` 값을 `NewValues` 10 진수 값을 사용 하 여 구문 분석 된 컬렉션에서 코드의 다음 줄을 사용 하 여 통화 형식을 사용 하는 `RowUpdating` 이벤트 처리기:


[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample4.cs)]

사용자가 제공한 경우는 `UnitPrice` 값 (예: "$19.00")으로 계산 된 10 진수 값을 사용 하 여이 값을 덮어씁니다 [Decimal.Parse](https://msdn.microsoft.com/library/system.decimal.parse(VS.80).aspx), 통화 값을 구문 분석 합니다. 올바르게 모든 통화 기호, 쉼표, 소수점 및 등과 발생할 경우 10 진수를 구문 분석 하 고 사용 하 여이 [NumberStyles 열거형](https://msdn.microsoft.com/library/system.globalization.numberstyles(VS.80).aspx) 에 [System.Globalization](https://msdn.microsoft.com/library/abeh092z(VS.80).aspx) 네임 스페이스입니다.

그림 11은 사용자가 제공한의 통화 기호를 야기 된 문제를 보여 줍니다 `UnitPrice`, 방법을 함께 GridView의 `RowUpdating` 이러한 입력을 올바르게 구문 분석 하는 이벤트 처리기를 활용할 수 있습니다.


[![편집한 행의 UnitPrice 값은 이제 서식이 지정 된 통화로](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image32.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image31.png)

**그림 11**: The 편집할 행의 `UnitPrice` 이제는 통화 단위로 지정 하는 것이 가치가 ([클릭 하 여 큰 이미지 보기](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image33.png))


## <a name="step-2-prohibitingnull-unitprices"></a>2 단계: 금지`NULL UnitPrices`

데이터베이스 허용 하도록 구성 되는 동안 `NULL` 값을 `Products` 테이블의 `UnitPrice` 열을 하려는 경우 사용자 지정에서이 특정 페이지를 방문 하는 `NULL` `UnitPrice` 값. 즉, 사용자 입력 하지 못한 경우는 `UnitPrice` ,이 페이지를 통해 모든 편집된 제품 있어야 함을 지정 하는 가격을 사용자에 게 알리는 메시지를 표시 하려는 데이터베이스에 결과 저장 하는 것이 아니라 제품 행을 편집 하는 경우 값입니다.

`GridViewUpdateEventArgs` GridView의에 전달 된 개체 `RowUpdating` 이벤트 처리기에는 `Cancel` 속성은 경우로 `true`, 업데이트 프로세스를 종료 합니다. 확장 해 보겠습니다를 `RowUpdating` 이벤트 처리기를 설정 `e.Cancel` 에 `true` 경우 이유를 설명 하는 메시지를 표시 하 고는 `UnitPrice` 값을 `NewValues` 컬렉션은 `null`합니다.

라는 페이지에 레이블 웹 컨트롤을 추가 하 여 시작 `MustProvideUnitPriceMessage`합니다. 사용자 지정 하는 데 실패 하는 경우이 레이블 컨트롤에 표시 됩니다는 `UnitPrice` 제품을 업데이트 하는 경우 값입니다. 레이블 설정 `Text` 속성을 "제품 가격을 제공 해야 합니다." 새로운 CSS 클래스를 만들었습니다 `Styles.css` 라는 `Warning` 다음 정의 사용 하 여:


[!code-css[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample5.css)]

마지막으로 레이블의 설정 `CssClass` 속성을 `Warning`입니다. 이 시점에서 디자이너 그림 12에 나와 있는 것 처럼 경고 메시지가 빨간색, 굵게, 기울임꼴, 초대형 글꼴 크기 GridView 위에 표시 됩니다.


[![GridView 위에 추가한 레이블은](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image35.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image34.png)

**그림 12**:는 레이블이 된 추가 위에 GridView ([큰 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image36.png))


기본적으로이 레이블을 숨길지, 설정 하므로 해당 `Visible` 속성을 `false` 에 `Page_Load` 이벤트 처리기:


[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample6.cs)]

사용자 지정 하지 않고 제품을 업데이트 하려고 하는 경우는 `UnitPrice`, 업데이트 작업을 취소 하 고 경고 레이블을 표시 합니다. GridView의 보강 `RowUpdating` 같이 이벤트 처리기:


[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample7.cs)]

사용자가 제품 가격을 지정 하지 않고 저장 하려고 하는 경우 업데이트 취소 되 고 유용한 메시지가 표시 됩니다. 데이터베이스 (및 비즈니스 논리)을 하는 동안 허용 `NULL` `UnitPrice` s,이 특정 ASP.NET 페이지 그렇지 않습니다.


[![사용자는 UnitPrice 빈 값을 벗어날 수 없습니다.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image38.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image37.png)

**그림 13**:는 사용자를 벗어날 수 없습니다 `UnitPrice` 빈 ([클릭 하 여 큰 이미지 보기](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image39.png))


GridView의를 사용 하는 방법을 살펴본 지금 `RowUpdating` 프로그래밍 방식으로 할당 된 ObjectDataSource의 매개 변수 값을 변경 하는 이벤트 `UpdateParameters` 컬렉션에도 취소 하는 업데이트 처리 완전히 방법과 합니다. 이러한 개념 FormView 및 DetailsView 컨트롤에 전달 하 고 삽입 및 삭제에 적용 합니다.

이러한 작업에 대 한 이벤트 처리기를 통해 ObjectDataSource 수준에서 수행할 수도 있습니다 해당 `Inserting`, `Updating`, 및 `Deleting` 이벤트입니다. 이러한 이벤트는 기본 개체의 연결된 된 메서드를 호출 하기 전에 발생 하 고 입력된 매개 변수 컬렉션을 수정 하거나 완전 한 작업을 취소 하는 있는 마지막 기회를 제공 합니다. 이러한 세 가지 이벤트에 대 한 이벤트 처리기 형식의 개체로 전달 됩니다 [ObjectDataSourceMethodEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourcemethodeventargs(VS.80).aspx) 있는 두 가지 속성이 필요 합니다.

- [취소](https://msdn.microsoft.com/library/system.componentmodel.canceleventargs.cancel(VS.80).aspx)는 경우로 `true`, 수행 중인 작업 취소
- [InputParameters](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourcemethodeventargs.inputparameters(VS.80).aspx), 컬렉션의 `InsertParameters`, `UpdateParameters`, 또는 `DeleteParameters`에 대 한 이벤트 처리기가 있는지 여부에 따라 합니다 `Inserting`, `Updating`, 또는 `Deleting` 이벤트

ObjectDataSource 수준에서 매개 변수 값을 사용 하 여 작업을 설명 하기 위해 새 제품을 추가 하려면 사용자를 허용 하는 페이지에는 DetailsView 포함 하겠습니다. 이 DetailsView 신속 하 게 데이터베이스에 새 제품을 추가 하기 위한 인터페이스를 제공 하 게 됩니다. 사용자만 값을 입력 하도록 허용 보겠습니다에 새 제품을 추가할 때 일관 된 사용자 인터페이스를 유지 하는 `ProductName` 고 `UnitPrice` 필드입니다. 기본적으로 DetailsView의 삽입 인터페이스에 제공 되지 않습니다는 해당 값 설정 됩니다는 `NULL` 값 데이터베이스입니다. 하지만 ObjectDataSource의 사용할 수 있습니다 `Inserting` 살펴보겠지만 곧 다른 기본값을 삽입 하는 이벤트입니다.

## <a name="step-3-providing-an-interface-to-add-new-products"></a>3 단계: 새 제품을 추가 하는 인터페이스를 제공 합니다.

지웁니다는 DetailsView GridView 위에 디자이너 도구 상자에서 끌어 해당 `Height` 및 `Width` 속성 및 바인딩 페이지에서 이미 ObjectDataSource 되도록 합니다. 그러면 BoundField 또는 CheckBoxField 각 제품의 필드에 대 한 추가 됩니다. 스마트 태그를 삽입 사용 옵션을 선택 해야이 DetailsView를 사용 하 여 새 제품을 추가할 것 이므로 그러나 이러한 옵션이 없을 때문에 ObjectDataSource의 `Insert()` 메서드 메서드에 매핑되지 않은 `ProductsBLL` 클래스 (그림 3 참조 데이터 원본을 구성 하는 경우 (없음)이이 매핑을 설정 하는 회수).

ObjectDataSource를 구성 하려면 마법사를 시작, 스마트 태그에서 데이터 소스 구성 링크를 선택 합니다. 첫 번째 화면을 사용 하면 ObjectDataSource;에 바인딩된 기본 개체를 변경할 수 있습니다. 이 설정 된 채로 두고 `ProductsBLL`합니다. 다음 화면에는 기본 개체의 ObjectDataSource의 메서드에서 매핑을 보여 줍니다. 명시적으로 지정 하는 경우에 합니다 `Insert()` 고 `Delete()` 메서드 메서드에 매핑하지 말아야, INSERT 및 DELETE 탭으로 이동 하는 경우 매핑이 있는지 표시 됩니다. 때문에 이것이 합니다 `ProductsBLL`의 `AddProduct` 및 `DeleteProduct` 메서드를 사용 합니다 `DataObjectMethodAttribute` 특성에 대 한 기본 메서드는을 `Insert()` 및 `Delete()`각각. 따라서 ObjectDataSource 마법사는 명시적으로 지정 된 다른 값이 없으면 마법사를 실행 하면 이러한 각 시간을 선택 합니다.

유지를 `Insert()` 가리키는 메서드는 `AddProduct` 메서드를 삭제 탭의 드롭다운 목록 (None)으로 다시 설정 합니다.


[![AddProduct 메서드에 삽입 탭의 드롭다운 목록 설정](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image41.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image40.png)

**그림 14**: 삽입 탭의 드롭다운 목록으로 설정 합니다 `AddProduct` 메서드 ([클릭 하 여 큰 이미지 보기](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image42.png))


[![DELETE 탭의 드롭다운 목록 (None)으로 설정](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image44.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image43.png)

**그림 15**: 삭제 탭의 드롭다운 목록 (None)으로 설정 ([큰 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image45.png))


다음과 같이 변경한 후 ObjectDataSource의 선언 구문을 포함 하도록 확장 됩니다는 `InsertParameters` 아래와 같이 컬렉션:


[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample8.aspx)]

다시 추가 마법사를 다시 실행 된 `OldValuesParameterFormatString` 속성입니다. 기본 값으로 설정 하 여이 속성의 선택을 취소 하려면 잠시 (`{0}`) 또는 선언적 구문에서 완전히 제거 합니다.

삽입 기능을 제공 하는 ObjectDataSource를 사용 하 여 DetailsView의 스마트 태그 포함 삽입 사용 확인란을 선택 합니다. 디자이너를 반환 하 고이 옵션을 확인 합니다. 다음으로 두 BoundFields-만 포함 되도록 DetailsView를 줄이려면 `ProductName` 및 `UnitPrice` -및 CommandField 합니다. 이 시점에서 DetailsView의 선언적 구문 같이 표시 됩니다.


[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample9.aspx)]

그림 16에서는 브라우저를 통해이 시점에서 볼 때이 페이지를 보여 줍니다. 알 수 있듯이 DetailsView 이름과 (Chai) 첫 번째 제품의 가격을 나열 합니다. 원하는 어떤 것 인데, 신속 하 게 데이터베이스에 새 제품을 추가 하려면 사용자에 대 한 수단을 제공 하는 삽입 인터페이스입니다.


[![DetailsView 현재 읽기 전용 모드에서 렌더링 됩니다.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image47.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image46.png)

**그림 16**: The DetailsView 현재 읽기 전용 모드에서 렌더링 됩니다 ([큰 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image48.png))


DetailsView 설정 해야 하는 삽입 모드에서 표시 하기 위해 합니다 `DefaultMode` 속성을 `Inserting`입니다. 이 처음 방문할 때 삽입 모드로 DetailsView를 렌더링 하 고 새 레코드를 삽입 한 후 유지 합니다. 그림 17에서 알 수 있듯이, 이러한는 DetailsView 새 레코드를 추가 하는 것에 대 한 빠른 인터페이스를 제공 합니다.


[![새 제품을 빠르게 추가 하기 위한 인터페이스를 제공 하는 DetailsView](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image50.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image49.png)

**그림 17**: DetailsView 인터페이스를 제공 빠르게 추가 하기 위해 새 제품 ([큰 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image51.png))


사용자 제품 이름과 가격 (예: "Acme 물"과 그림 17 에서처럼 1.99)을 입력 하 고 Insert가, 포스트백 근거가 시간과 삽입 워크플로 시작 데이터베이스에 추가 되 고 새 제품 레코드의 정점입니다. DetailsView 삽입 해당 인터페이스 및 GridView 자동으로 다시 바인딩되는 데이터 원본에 새 제품을 포함 하기 위해 그림 18 에서처럼 유지 관리 합니다.


![제품](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image52.png)

**그림 18**: 데이터베이스에 추가 되었습니다 "Acme 물" 제품


그림 18에서 GridView 표시 되지 않습니다 하지만 부족 DetailsView 인터페이스에서 product 필드 하는 동안 `CategoryID`, `SupplierID`, `QuantityPerUnit`등에 할당 된 `NULL` 값 데이터베이스입니다. 다음 단계를 수행 하 여이 확인할 수 있습니다.

1. Visual Studio에서 서버 탐색기로 이동
2. 확장 된 `NORTHWND.MDF` 데이터베이스 노드
3. 마우스 오른쪽 단추로 클릭는 `Products` 데이터베이스 테이블 노드
4. 테이블 데이터 표시를 선택 합니다.

레코드를 모두 나열 됩니다는 `Products` 테이블입니다. 볼 수 있듯이 그림 19의 모든 새 제품의 열 이외의 `ProductID`, `ProductName`, 및 `UnitPrice` 가 `NULL` 값입니다.


[![NULL 값 할당 되는 제품 필드에에서 제공 되지 DetailsView](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image54.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image53.png)

**그림 19**: 할당 되는 제품 필드에에서 제공 되지 DetailsView `NULL` 값 ([클릭 하 여 큰 이미지 보기](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image55.png))


이외의 다른 기본값을 제공 하는 것이 좋겠습니다 `NULL` 하나 이상의 이러한에 대 한 열 값 중 하나 때문에 `NULL` 모범 기본 옵션이 아닙니다 자체는 데이터베이스 열은 허용 하지 않으므로 또는 `NULL` s입니다. 이렇게 하려면에서는 프로그래밍 방식으로 값을 설정할 수 DetailsView의 매개 변수 `InputParameters` 컬렉션입니다. 이 할당 수행할 수 있습니다 하거나 이벤트 처리기는 DetailsView `ItemInserting` 이벤트 또는 ObjectDataSource의 `Inserting` 이벤트입니다. 이미 살펴보았습니다 사전 및 사후 수준 이벤트를 사용 하 여 웹 데이터 수준 제어를이 이번 ObjectDataSource의 이벤트를 사용 하 여 살펴보겠습니다.

## <a name="step-4-assigning-values-to-thecategoryidandsupplieridparameters"></a>4 단계: 값을 할당 합니다`CategoryID`고`SupplierID`매개 변수

이 자습서에 대 한 한다고는이 인터페이스를 통해 새 제품을 추가 하는 경우 응용 프로그램에 대 한 할당을 `CategoryID` 및 `SupplierID` 값이 1입니다. 앞에서 설명한 대로 ObjectDataSource에 데이터 수정 프로세스 중 해당 화재 사전 및 사후 수준 이벤트의 쌍이 있습니다. 때 해당 `Insert()` 메서드가 호출 되 면 ObjectDataSource 먼저 발생 합니다. 해당 `Inserting` 이벤트에 다음 메서드를 호출 하는 해당 `Insert()` 메서드를 매핑한 및 마지막으로 발생 합니다 `Inserted` 이벤트입니다. `Inserting` 미국 이벤트 처리기는 입력된 매개 변수를 조정 하거나 완전 한 작업을 취소 한 마지막 기회를 제공 하는 제공 합니다.

> [!NOTE]
> 하거나 가능성이 하려는 실제 응용 프로그램에서 사용자는 category와 supplier 지정 하거나 몇 가지 기준을 바탕으로이 값을 선택 하는 또는 비즈니스 논리 대신 무조건 1 ID를 선택 합니다. 하지만 예제에서는 프로그래밍 방식으로 ObjectDataSource의 미리 수준 이벤트에서 입력된 매개 변수의 값을 설정 하는 방법을 보여 줍니다.


ObjectDataSource의에 대 한 이벤트 처리기를 만들려면 잠시 `Inserting` 이벤트입니다. 이벤트 처리기의 두 번째 입력된 매개 변수 형식의 개체는 `ObjectDataSourceMethodEventArgs`, 매개 변수 컬렉션에 액세스 하는 속성이 있는 (`InputParameters`) 및 작업을 취소 하는 속성 (`Cancel`).


[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample10.cs)]

이 시점에서 `InputParameters` ObjectDataSource의 속성에 들어 `InsertParameters` DetailsView에서 할당 된 값을 사용 하 여 컬렉션입니다. 이러한 매개 변수 중 하나의 값을 변경 하려면 간단히 사용: `e.InputParameters["paramName"] = value`합니다. 따라서 설정 하는 `CategoryID` 및 `SupplierID` 1의 값을 조정 합니다 `Inserting` 다음과 같이 이벤트 처리기:


[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample11.cs)]

이 시점 (예: Acme 탄산 음료) 새 제품을 추가 합니다 `CategoryID` 및 `SupplierID` 새 제품 열 1로 설정 됩니다 (그림 20 참조).


[![새 제품 이제 해당 CategoryID 및 공급 업체 Id 값을 1로 설정](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image57.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image56.png)

**그림 20**: 새 제품 이제는 해당 `CategoryID` 하 고 `SupplierID` 값 1로 설정 ([클릭 하 여 큰 이미지 보기](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image58.png))


## <a name="summary"></a>요약

편집, 삽입 및 삭제 프로세스를 하는 동안 데이터 웹 컨트롤 및 ObjectDataSource 둘 다 수의 전처리 및 후 수준 이벤트를 통해 진행 됩니다. 이 자습서에서는 미리 수준 이벤트를 검사 하 고 하는 데 이러한 입력된 매개 변수 사용자 지정 또는 데이터 수정 작업을 취소할 데이터 웹 컨트롤 및 ObjectDataSource의 이벤트에서 완전히 둘 다는 방법을 알아보았습니다. 다음 자습서를 작성 하 고 사후 수준 이벤트에 대 한 이벤트 처리기를 사용 하는 방법을 살펴보겠습니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 인 재키 Goor 및 Liz Shulok 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](an-overview-of-inserting-updating-and-deleting-data-cs.md)
> [다음](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)
