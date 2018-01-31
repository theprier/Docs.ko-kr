---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs
title: "삽입, 업데이트 및 삭제 (C#)와 관련 된 이벤트 검사 | Microsoft Docs"
author: rick-anderson
description: "이 자습서에서는 전 또는 배포 시 삽입 후 발생 하는 이벤트를 사용 하 여 검토 합니다 업데이트 또는 ASP.NET 데이터 웹 컨트롤의 작업을 삭제 합니다. W..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/17/2006
ms.topic: article
ms.assetid: dab291a0-a8b5-46fa-9dd8-3d35b249201f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs
msc.type: authoredcontent
ms.openlocfilehash: 93da23d58d1ba73c5b97f42631d036dd364de24d
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="examining-the-events-associated-with-inserting-updating-and-deleting-c"></a>삽입, 업데이트 및 삭제 (C#)와 연결 된 이벤트를 검사 합니다.
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_17_CS.exe) 또는 [PDF 다운로드](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/datatutorial17cs1.pdf)

> 이 자습서에서는 전 또는 배포 시 삽입 후 발생 하는 이벤트를 사용 하 여 검토 합니다 업데이트 또는 ASP.NET 데이터 웹 컨트롤의 작업을 삭제 합니다. 편집 인터페이스만 제품 필드의 하위 집합을 업데이트 하려면 사용자 지정 하는 방법 또한 살펴보겠습니다.


## <a name="introduction"></a>소개

기본 제공 삽입, 편집 또는 삭제 GridView, DetailsView, 또는 FormView 컨트롤의 기능을 사용할 경우 최종 사용자는 새 레코드를 추가 또는 업데이트 하거나 기존 레코드를 삭제할의 프로세스를 완료 하는 경우 다양 한 단계 동안 실행 합니다. 설명한 것 처럼는 [이전 자습서](an-overview-of-inserting-updating-and-deleting-data-cs.md), 업데이트 및 취소 단추 및 텍스트 상자에 BoundFields 설정 편집 단추를 교체 하는 GridView에서 행을 편집할 때. 최종 사용자 데이터를 업데이트 하 고 업데이트를 클릭 한 후 다음 단계는 포스트백에서 수행 됩니다.

1. GridView의 ObjectDataSource 채웁니다 `UpdateParameters` 와 편집 된 레코드의 고유한 식별 필드 (통해는 `DataKeyNames` 속성) 사용자가 입력 값과 함께
2. 해당 ObjectDataSource를 호출 하는 GridView `Update()` 내부 개체에 적절 한 메서드를 호출 하는 메서드 (`ProductsDAL.UpdateProduct`,이 이전 자습서)
3. 이제 업데이트 된 변경 내용이 포함 하는 기본 데이터는 GridView에 리바운드

이 일련의 단계 동안 다양 한 이벤트를 발생 수를 사용자 지정 논리를 추가 하려면 이벤트 처리기를 만들 수 있어 필요한 부분입니다. 1 단계에서 GridView의 이전 예를 들어 `RowUpdating` 이벤트 발생 합니다. 이 시점에서 일부 유효성 검사 오류가 있는 경우 업데이트 요청을 취소할 수 있습니다. 경우는 `Update()` 메서드가 호출 되 면 ObjectDataSource의 `Updating` 발생 이벤트를 추가 하 여 모든 값을 사용자 지정할 수 있는 기회를 제공 하는 `UpdateParameters`합니다. 개체의 메서드가 ObjectDataSource의 실행 완료 된 후 원본으로 사용 된 ObjectDataSource `Updated` 이벤트가 발생 합니다. 에 대 한 이벤트 처리기는 `Updated` 이벤트 영향을 받은 행 수 및 예외가 발생 여부와 같은 업데이트 작업에 대 한 세부 정보를 검사할 수 있습니다. 2 단계, GridView의 마지막으로, 후 `RowUpdated` 이벤트 발생; 수행 정당한 업데이트 작업에 대 한 추가 정보를 검사할 이벤트 처리기에 대 한 이벤트 수 있습니다.

그림 1에서는 GridView를 업데이트할 때이 일련을의 이벤트 및 단계를 보여 줍니다. 그림 1의 이벤트 패턴은 GridView로 업데이트에 고유 하지 않습니다. 삽입, 업데이트 또는 GridView에서 데이터 삭제, DetailsView, 또는 FormView precipitates 전처리 및 후 수준에 대 한 이벤트 데이터 웹 컨트롤과 ObjectDataSource 모두 동일한 시퀀스입니다.


[![일련의 사전 및 사후 이벤트 화재는 GridView의 데이터를 업데이트 하는 경우](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image2.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image1.png)

**그림 1**: A 시리즈의 사전 및 사후 이벤트 화재 때 업데이트 데이터에는 GridView ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image3.png))


이러한 이벤트를 사용 하 여 기본 제공 삽입 하려고 하는 것이 살펴봅니다이 자습서에서는 업데이트 및 삭제 기능을 ASP.NET 데이터 웹 제어 합니다. 편집 인터페이스만 제품 필드의 하위 집합을 업데이트 하려면 사용자 지정 하는 방법 또한 살펴보겠습니다.

## <a name="step-1-updating-a-productsproductnameandunitpricefields"></a>1 단계: 제품의 업데이트`ProductName`및`UnitPrice`필드

이전 자습서에서 편집 인터페이스에서 *모든* 제품 필드 되지 않은 읽기 전용 포함 되어야 합니다. 예를 들어-GridView에서 필드를 제거 하려면 `QuantityPerUnit` -데이터 웹 컨트롤 데이터 업데이트는 ObjectDataSource 설정 하지 않아야 하는 경우 `QuantityPerUnit` `UpdateParameters` 값입니다. ObjectDataSource 다음에 전달는 `null` 값에 `UpdateProduct` 편집한 데이터베이스 레코드의 변경 BLL 비즈니스 논리 계층 () 메서드를 `QuantityPerUnit` 열을 한 `NULL` 값입니다. 마찬가지로 경우 필수 필드와 같은 `ProductName`, 제거 편집 인터페이스에서 업데이트와 함께 실패 합니다는 "*'ProductName' 열에서 null을 허용 하지*" 예외. 호출 하 여 ObjectDataSource 구성 되었기 때문에이 동작에 대 한 이유는는 `ProductsBLL` 클래스의 `UpdateProduct` 메서드를 각각의 제품 필드에 대 한 입력된 매개 변수를 예상 합니다. 따라서: ObjectDataSource `UpdateParameters` 컬렉션 매개 변수는 메서드의 각 입력 매개 변수를 포함 합니다.

최종 사용자만 필드의 하위 집합을 업데이트할 수 있도록 웹 컨트롤에 데이터를 제공 하려는 경우 프로그래밍 방식으로 설정 하거나 누락 된 해야 `UpdateParameters` ObjectDataSource의 값 `Updating` 이벤트 처리기 만들기 및 BLL 메서드를 호출 하거나 필드의 하위 집합만이 필요합니다. 이 방법을 통해 살펴보겠습니다.

특히, 표시 되는 페이지를 만들어 보겠습니다 테이블만 `ProductName` 및 `UnitPrice` 편집 가능한 GridView의 필드입니다. 이 GridView 편집 인터페이스는 두 개의 표시 된 필드를 업데이트 하려는 사용자만 허용 `ProductName` 및 `UnitPrice`합니다. 편집이 인터페이스는 제품의 필드의 하위 집합에 제공 하므로 하거나 만들어야 한다는 기존 BLL를 사용 하는 ObjectDataSource `UpdateProduct` 메서드 하며 해당 특성이 제품 필드 값이 누락 설정에 프로그래밍 방식으로 해당 `Updating` 이벤트 처리기 또는 म GridView에 정의 된 필드의 하위 집합만 예상 하는 새 BLL 메서드를 만들 필요. 이 자습서에서는 보겠습니다 후자 옵션을 사용 및 만들기의 오버 로드는 `UpdateProduct` 메서드를 세 개의 입력된 매개 변수에서 사용 하는 하나의: `productName`, `unitPrice`, 및 `productID`:


[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample1.cs)]

원래 같은 `UpdateProduct` 메서드,이 오버 로드에 지정 된 데이터베이스에 제품 있는지 확인 하 여 시작 `ProductID`합니다. 반환 된 그렇지 않은 경우 `false`, 제품 정보를 업데이트 하는 요청이 실패 했음을 나타냅니다. 기존 제품 레코드를 업데이트 하지 않으면 `ProductName` 및 `UnitPrice` 필드를 적절 하 게 되 고 업데이트는 TableAdpater를 호출 하 여 커밋된 `Update()` 전달 하는 메서드는 `ProductsRow` 인스턴스.

이 추가 된 우리의 `ProductsBLL` 클래스 we're 간단한 GridView 인터페이스를 만들 수 있습니다. 열기는 `DataModificationEvents.aspx` 에 `EditInsertDelete` 폴더는 GridView 페이지에 추가 합니다. 새 ObjectDataSource를 만들고 사용 하도록 구성는 `ProductsBLL` 클래스와 해당 `Select()` 메서드 매핑을 `GetProducts` 및 해당 `Update()` 메서드 매핑을 `UpdateProduct` 는 수행 하는 오버 로드는 `productName`, `unitPrice`, 및 `productID` 입력 매개 변수입니다. 그림 2는 ObjectDataSource를 매핑할 때 데이터 원본 만들기 마법사를 보여 줍니다 `Update()` 메서드는 `ProductsBLL` 클래스의 새 `UpdateProduct` 메서드 오버 로드 합니다.


[![새 UpdateProduct 오버 로드를 map ObjectDataSource의 update () 메서드](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image5.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image4.png)

**그림 2**: ObjectDataSource의 매핑 `Update()` 메서드는 새로 `UpdateProduct` 오버 로드 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image6.png))


예제에서 데이터를 편집할 수 있지만 하지를 삽입 또는 삭제 레코드 수 있는 기능을 필요로 방금 처음 이후 잠시 명시적으로 나타내기 위해 ObjectDataSource의 `Insert()` 및 `Delete()` 메서드 중 하나에 매핑할 수 없습니다는 `ProductsBLL` INSERT 및 DELETE 탭으로 이동 하 고 드롭다운 목록에서 (없음)를 선택 하 여 클래스의 메서드.


[![(없음)에서 INSERT 및 DELETE 탭에 대 한 드롭다운 목록에서 선택](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image8.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image7.png)

**그림 3**: (없음) 삽입 및 삭제 탭의 드롭다운 목록에서 선택 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image9.png))


이 마법사를 완료 한 후 확인 GridView의 스마트 태그에서 편집 사용 확인란을 선택 합니다.

데이터 원본 만들기 마법사 및 GridView에 있는 바인딩 완료와 Visual Studio에 두 컨트롤에 대 한 선언적 구문을 만들었습니다. 아래에 나와 있는 ObjectDataSource의 선언적 태그를 검사 하 여 원본 뷰로 이동 합니다.


[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample2.aspx)]

ObjectDataSource의에 대 한 매핑이 있으므로 `Insert()` 및 `Delete()` 메서드는 없는 `InsertParameters` 또는 `DeleteParameters` 섹션. 또한 이후에 `Update()` 메서드가 매핑되는 `UpdateProduct` 세 개의 입력된 매개 변수를 허용 하는 메서드 오버 로드는 `UpdateParameters` 섹션에는 3 개의 방금 `Parameter` 인스턴스.

ObjectDataSource의 `OldValuesParameterFormatString` 속성이 `original_{0}`합니다. 이 속성은 데이터 소스 구성 마법사를 사용 하는 경우 Visual Studio에서 자동으로 설정 합니다. 그러나 BLL 메서드는 원래 원하지 이후 `ProductID` 시 전달할 ObjectDataSource의 선언적 구문에서이 속성이 할당을 완전히 제거 하거나, 값입니다.

> [!NOTE]
> 단순히 제거 하는 경우는 `OldValuesParameterFormatString` 디자인 뷰에서 속성은 속성 창에서 속성 값의 선언 구문에는 여전히 존재 하지만 빈 문자열로 설정 됩니다. 제거 하거나 속성 완전히 선언적 구문에서 또는 속성 창에서 값을 기본값으로 설정, `{0}`합니다.


ObjectDataSource만에 있을 때 `UpdateParameters` 제품의 이름, 가격 및 ID에 대 한 Visual Studio가 추가 BoundField 또는 CheckBoxField GridView에서 각 제품의 필드에 대 한 합니다.


[![각 제품의 필드에 대 한 BoundField 또는 CheckBoxField를 포함 하는 GridView](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image11.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image10.png)

**그림 4**: 각 제품의 필드에 대 한 BoundField 또는 CheckBoxField를 포함 하는 GridView ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image12.png))


제품을 편집 하 고 해당 업데이트 단추를 클릭 하는 최종 사용자, GridView 읽기 전용으로 설정 되지 않은 해당 필드를 열거 합니다. ObjectDataSource의의 해당 매개 변수의 값을 설정 합니다 `UpdateParameters` 사용자가 입력 한 값을 수집 합니다. 해당 매개 변수가 없는 경우 GridView를 컬렉션에 추가 합니다. 따라서 우리의 GridView BoundFields에서는 모든 제품의 필드에 대 한 CheckBoxFields ObjectDataSource는 결국 호출 된 `UpdateProduct` 는 있지만 이러한 매개 변수를 모두 수행 하는 오버 로드는 ObjectDataSource의 선언적 태그 (그림 5 참조)만 세 개의 입력된 매개 변수를 지정 합니다. 마찬가지로, 조합한 일부 경우 읽기 전용이 아닌 경우 제품 필드에 대 한 입력된 매개 변수에 해당 하지 않는 GridView에서는 `UpdateProduct` 오버 로드, 업데이트 하는 동안 예외가 발생 합니다.


[![ObjectDataSource의 UpdateParameters 컬렉션에 매개 변수를 추가 하는 GridView 됩니다.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image14.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image13.png)

**그림 5**: The GridView 됩니다에 매개 변수 추가 ObjectDataSource `UpdateParameters` 컬렉션 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image15.png))


호출 하 여 ObjectDataSource 되도록는 `UpdateProduct` 는 방금: 제품의 이름, 가격 및 ID를 수행 하는 오버 로드에 대 한 편집 가능한 필드를 지정 하 여 GridView를 제한 해야 테이블만 `ProductName` 및 `UnitPrice`합니다. 이 된 다른 필드를 설정 하 여 다른 BoundFields 및 CheckBoxFields를 제거 하 여 수행할 수 있습니다 `ReadOnly` 속성을 `true`, 또는 둘의 조합입니다. 이 자습서에 대 한 단순히 제거를 제외한 모든 GridView 필드는 `ProductName` 및 `UnitPrice` GridView의 선언적 태그는 같습니다 지나면 BoundFields:


[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample3.aspx)]

경우에는 `UpdateProduct` 오버 로드에서는 세 개의 입력된 매개 변수, 우리의 GridView에 두 개의 BoundFields만 있습니다. 때문에 이것이 `productID` 입력된 매개 변수는 기본 키 값은 및의 값을 통해 전달 된는 `DataKeyNames` 편집된 된 행에 대 한 속성입니다.

우리의 GridView와 함께 `UpdateProduct` 오버 로드, 사용자는 다른 제품 필드의 손실 없이 이름 및 제품의 가격을 편집할 수 있습니다.


[![인터페이스 방금 제품의 이름과 가격을 수정할 수 있습니다.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image17.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image16.png)

**그림 6**: 방금 제품의 이름과 가격 편집 인터페이스 허용 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image18.png))


> [!NOTE]
> 이전 자습서에서 설명 했 듯이 것은 매우 중요 s 뷰 상태 수 GridView (기본 동작)을 사용할 수 있도록 합니다. GridView s를 설정 하면 `EnableViewState` 속성을 `false`, 위험을 실수로 삭제 하거나 편집을 기록 하는 동시 사용자가 실행 합니다. 참조 [경고: 동시성 문제가 있는 ASP.NET 2.0 Gridview/DetailsView/FormViews 해당 편집을 원하는 및/또는 삭제 및 뷰 상태를 사용 하지 않으면](http://scottonwriting.net/sowblog/archive/2006/10/03/163215.aspx) 자세한 정보에 대 한 합니다.


## <a name="improving-theunitpriceformatting"></a>향상 된`UnitPrice`서식 지정

그림 6의 작동에 표시 된 GridView 예 동안는 `UnitPrice` 필드 형식이 전혀, 기호 및 네 개의 소수 자릿수가 없는 모든 통화 가격 디스플레이에서으로 인해 발생 합니다. 편집할 수 없는 행에 대 한 서식을 통화를 적용 하려면 설정 하기만 `UnitPrice` BoundField의 `DataFormatString` 속성을 `{0:c}` 및 해당 `HtmlEncode` 속성을 `false`합니다.


[![UnitPrice의 DataFormatString 및 HtmlEncode 속성을 적절 하 게 설정](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image20.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image19.png)

**그림 7**: 설정의 `UnitPrice`의 `DataFormatString` 및 `HtmlEncode` 그에 따라 속성 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image21.png))


이러한 변경으로 인해 편집할 수 없는 행에 서식을 통화로; 하는 가격 그러나 편집된 된 행 여전히 표시 통화 기호 없이 하 고 네 개의 소수 자릿수로 값.


[![편집할 수 없는 행은 이제 서식이 지정 된 통화 값으로](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image23.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image22.png)

**그림 8**: 편집할 수 없는 행은 이제는 통화 값 형식 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image24.png))


에 지정 된 서식 지정 지침의 `DataFormatString` BoundField의 설정 하 여 편집 인터페이스에 적용할 수 속성 `ApplyFormatInEditMode` 속성을 `true` (기본값은 `false`). 이 속성을 설정 하 여 `true`합니다.


[![UnitPrice BoundField ApplyFormatInEditMode 속성이 true로 설정](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image26.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image25.png)

**그림 9**: 설정의 `UnitPrice` BoundField의 `ApplyFormatInEditMode` 속성을 `true` ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image27.png))


값이이 변경으로 인해는 `UnitPrice` 편집한에 표시 된 행의 통화로 포맷 합니다.


[![편집 된 행의 UnitPrice 값은 이제 포맷 통화로](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image29.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image28.png)

**그림 10**: The 편집할 행의 `UnitPrice` 값이 통화로 이제 서식이 지정 됩니다 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image30.png))


그러나 $19.00 throw와 같은 텍스트 상자에 통화 기호와 함께 제품 업데이트는 `FormatException`합니다. GridView에서 ObjectDataSource에 사용자가 제공한 값을 할당 하려고 할 때 `UpdateParameters` 변환할 수 없는 컬렉션의 `UnitPrice` 에 "$19.00" 문자열을 `decimal` 매개 변수에 필요한 (11 그림 참조). 이 해결 하려면 GridView의에 대 한 이벤트 처리기를 만들 수 있습니다 `RowUpdating` 이벤트를 사용자가 제공한 구문 분석 `UnitPrice` 통화 형식으로 `decimal`합니다.

GridView의 `RowUpdating` 이벤트 형식의 개체를 두 번째 매개 변수로 받아들입니다 [GridViewUpdateEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewupdateeventargs(VS.80).aspx)를 포함 하는 `NewValues` 사전 준비 되도록 사용자가 제공한 값을 포함 하는 속성 중 하나로 ObjectDataSource의에 할당 된 `UpdateParameters` 컬렉션입니다. 기존을 덮어쓸 수 `UnitPrice` 값에 `NewValues` 10 진수 값을 사용 하 여 컬렉션에 코드의 다음 줄으로 통화 형식을 사용 하 여 구문 분석은 `RowUpdating` 이벤트 처리기:


[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample4.cs)]

사용자가 제공 하는 경우는 `UnitPrice` 값 (예: "$19.00") 하 여 계산 된 10 진수 값으로이 값을 덮어씁니다 [Decimal.Parse](https://msdn.microsoft.com/library/system.decimal.parse(VS.80).aspx), 통화로 값을 구문 분석 합니다. 올바르게 통화 기호, 쉼표, 소수점 및 이런 식으로 발생할 경우 소수점 구문 분석 하 고 사용 하 여이 [NumberStyles 열거형](https://msdn.microsoft.com/library/system.globalization.numberstyles(VS.80).aspx) 에 [System.Globalization](https://msdn.microsoft.com/library/abeh092z(VS.80).aspx) 네임 스페이스입니다.

그림 11에는 사용자가 제공한 통화 기호에 의해 발생 된 문제를 보여 줍니다. `UnitPrice`, 방식과 GridView의 `RowUpdating` 이러한 입력을 올바르게 구문 분석 하는 이벤트 처리기를 활용할 수 있습니다.


[![편집 된 행의 UnitPrice 값은 이제 포맷 통화로](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image32.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image31.png)

**그림 11**: The 편집할 행의 `UnitPrice` 값이 통화로 이제 서식이 지정 됩니다 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image33.png))


## <a name="step-2-prohibitingnull-unitprices"></a>2 단계: 금지`NULL UnitPrices`

데이터베이스 허용 하도록 구성 되는 동안 `NULL` 값에 `Products` 테이블의 `UnitPrice` 지정에서이 페이지를 방문 하는 사용자가을 수행할 열을 한 `NULL` `UnitPrice` 값입니다. 즉, 입력에 실패 한 경우는 `UnitPrice` ,이 페이지를 통해 편집 된 제품을 모두 갖도록 지정 된 가격을 사용자에 게 알리는 메시지를 표시 하려면 원하는 데이터베이스에 결과 저장 하는 것이 아니라 제품 행을 편집할 때 값입니다.

`GridViewUpdateEventArgs` GridView의로 전달 된 개체 `RowUpdating` 이벤트 처리기에는 `Cancel` 속성, 하는 경우로 설정 `true`, 업데이트 프로세스를 종료 합니다. 확장 해 보겠습니다는 `RowUpdating` 이벤트 처리기를 설정 `e.Cancel` 를 `true` 경우 이유를 설명 하는 메시지를 표시 하 고는 `UnitPrice` 값에 `NewValues` 컬렉션이 `null`합니다.

라는 페이지로 Label 웹 컨트롤을 추가 하 여 시작 `MustProvideUnitPriceMessage`합니다. 사용자 지정 하는 데 실패 하는 경우이 레이블 컨트롤에 표시 됩니다는 `UnitPrice` 제품을 업데이트할 때 값입니다. 레이블을 설정 `Text` 속성을 "는 제품에 대 한 가격을 제공 해야 합니다." 새로운 CSS 클래스를 만들었습니다 `Styles.css` 라는 `Warning` 다음 정의 사용 합니다.


[!code-css[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample5.css)]

마지막으로 레이블의 설정 `CssClass` 속성을 `Warning`합니다. 이 시점에서 디자이너 그림 12에 나와 있는 것 처럼 빨간색, 굵게, 기울임꼴에 경고 메시지가, 특대 글꼴 크기는 GridView 위에 표시 됩니다.


[![GridView 위에 레이블을 추가 되었습니다.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image35.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image34.png)

**그림 12**: A 레이블이 되었습니다 추가 위에 GridView ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image36.png))


기본적으로이 레이블의 숨김을, 따라서 설정 해당 `Visible` 속성을 `false` 에 `Page_Load` 이벤트 처리기.


[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample6.cs)]

사용자가을 지정 하지 않고 제품을 업데이트 하려고 하는 경우는 `UnitPrice`, 하 여 업데이트를 취소 하 고 경고 레이블을 표시 합니다. GridView의 보강 `RowUpdating` 다음과 같이 이벤트 처리기.


[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample7.cs)]

사용자가 제품 가격을 지정 하지 않고 저장 하려고 하는 경우 업데이트가 취소 되 고 유용한 메시지가 표시 됩니다. 데이터베이스 (및 비즈니스 논리) 동안 고려한 `NULL` `UnitPrice` s,이 특정 ASP.NET 페이지가 없습니다.


[![사용자는 UnitPrice 빈 값을 벗어날 수 없습니다.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image38.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image37.png)

**그림 13**: A 사용자를 이동할 수 없도록 `UnitPrice` 빈 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image39.png))


GridView의를 사용 하는 방법을 지금까지 살펴본 것 `RowUpdating` ObjectDataSource의에 지정 된 매개 변수 값을 프로그래밍 방식으로 변경 하는 이벤트 `UpdateParameters` 컬렉션에도 취소 하는 업데이트 처리 완전히 하는 방식입니다. 이러한 개념 FormView 및 DetailsView 컨트롤에 탭으로 이전 하 고 삽입 및 삭제에 적용 합니다.

에 대 한 이벤트 처리기를 통해 ObjectDataSource 수준에서 다음이 작업을 수행 해당 `Inserting`, `Updating`, 및 `Deleting` 이벤트입니다. 이러한 이벤트는 기본 개체의 연결 된 메서드를 호출 하기 전에 발생 하 고 입력된 매개 변수 컬렉션을 수정 하거나 완전 한 작업을 취소할 수 있는 마지막 기회 기회를 제공 합니다. 이러한 세 이벤트에 대 한 이벤트 처리기 형식의 개체로 전달 [ObjectDataSourceMethodEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourcemethodeventargs(VS.80).aspx) 하는 두 가지 속성이 필요 합니다.

- [취소](https://msdn.microsoft.com/library/system.componentmodel.canceleventargs.cancel(VS.80).aspx)이며 경우로 설정 `true`, 수행 되는 작업을 취소 합니다.
- [InputParameters](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourcemethodeventargs.inputparameters(VS.80).aspx), 컬렉션의 `InsertParameters`, `UpdateParameters`, 또는 `DeleteParameters`에 대 한 이벤트 처리기가 있는지 여부에 따라는 `Inserting`, `Updating`, 또는 `Deleting` 이벤트

ObjectDataSource 수준에서 매개 변수 값으로 작업을 설명 하기 위해 보겠습니다 새 제품을 추가 하려면 사용자가 수 있는 가격 페이지에는 DetailsView를 포함 합니다. 이 DetailsView이 인터페이스를 제공 신속 하 게 데이터베이스에 새 제품을 추가 하는 데 사용 됩니다. 에 대 한 값만을 입력 하는 데 사용할 수 보겠습니다에 새 제품을 추가할 때 일관 된 사용자 인터페이스를 유지 하는 `ProductName` 및 `UnitPrice` 필드입니다. 기본적으로 DetailsView의 삽입 인터페이스에 제공 되지 않습니다는 해당 값으로 설정 됩니다는 `NULL` 데이터베이스 값입니다. 그러나 ObjectDataSource의 사용할 수 `Inserting` 를 볼 수 있겠지만, 곧 다른 기본값을 삽입 하는 이벤트입니다.

## <a name="step-3-providing-an-interface-to-add-new-products"></a>3 단계: 새 제품을 추가 하려면 인터페이스를 제공 합니다.

삭제 DetailsView GridView 위에 디자이너 도구 상자에서 끌어 해당 `Height` 및 `Width` 속성 및 바인딩 페이지에는 ObjectDataSource에 이미 존재 합니다. 그러면 BoundField 또는 CheckBoxField 각 제품의 필드에 대 한 추가 됩니다. 스마트 태그;에서 삽입 사용 옵션을 선택 해야이 DetailsView를 사용 하 여 새 제품을 추가할 것 이므로 그러나 이러한 옵션이 없을 때문에 ObjectDataSource의 `Insert()` 메서드의 메서드에 매핑되지 않은 `ProductsBLL` 클래스 (그림 3 참조 데이터 원본을 구성 하는 경우 (없음)이이 매핑이 설정 했으므로 회수).

ObjectDataSource를 구성 하려면 마법사를 실행 하는 스마트 태그에서 데이터 소스 구성 링크를 선택 합니다. 첫 번째 화면에서 ObjectDataSource;에 바인딩된 기본 개체를 변경할 수 있습니다. 그대로 `ProductsBLL`합니다. 다음 화면 ObjectDataSource의 방법 중에서 기본 개체의 매핑을 나열합니다. 에서는 명시적으로 표시 된 하는 경우에는 `Insert()` 및 `Delete()` 메서드는 메서드를 매핑하지 말아야, INSERT 및 DELETE 탭으로 이동 하는 경우 매핑이 있는지 표시 됩니다. ¿¡´는 `ProductsBLL`의 `AddProduct` 및 `DeleteProduct` 메서드 사용은 `DataObjectMethodAttribute` 특성에 대 한 기본 방법이 된다는을 `Insert()` 및 `Delete()`각각. 따라서 ObjectDataSource 마법사는 명시적으로 지정 된 다른 값이 없는 경우 마법사를 실행 하면 이러한 각 시간을 선택 합니다.

둡니다는 `Insert()` 가리키는 메서드는 `AddProduct` 메서드를 하지만 삭제 탭의 드롭다운 목록에서 (없음)으로 다시 설정 합니다.


[![삽입 탭 드롭 다운 목록을 AddProduct 메서드 설정](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image41.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image40.png)

**그림 14**: 삽입 탭의 드롭다운 목록으로 설정 된 `AddProduct` 메서드 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image42.png))


[![(없음) 탭 삭제 드롭 다운 목록을 설정합니다](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image44.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image43.png)

**그림 15**: (None) 삭제 탭의 드롭다운 목록을 설정 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image45.png))


다음과 같이 변경한 후 ObjectDataSource의 선언적 구문을 포함 하도록 확장 됩니다는 `InsertParameters` 아래와 같이 컬렉션:


[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample8.aspx)]

다시 추가 마법사를 다시 실행은 `OldValuesParameterFormatString` 속성입니다. 기본값을 설정 하 여이 속성의 선택을 취소 하 (`{0}`) 또는 선언적 구문에서 모두 제거 합니다.

삽입 기능을 제공 하는 ObjectDataSource를와 DetailsView의 스마트 태그 포함 합니다; 삽입 사용 확인란 디자이너에 반환 하 고이 옵션을 확인 합니다. 다음으로, 두 개의 BoundFields-된 갖도록 DetailsView를 줄이려면 `ProductName` 및 `UnitPrice` -및는 CommandField 합니다. 이 시점에서 DetailsView의 선언적 구문 같이 표시 됩니다.


[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample9.aspx)]

그림 16 브라우저를 통해이 시점에서 볼 때이 페이지를 보여줍니다. 볼 수 있듯이 DetailsView의 이름 및 (Chai) 첫 번째 제품의 가격을 나열 합니다. 그러나 원하는 사용자가 신속 하 게 데이터베이스에 새 제품을 추가 하는 방법을 제공 하는 삽입 인터페이스입니다.


[![DetailsView 현재 읽기 전용 모드에서 렌더링 됩니다.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image47.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image46.png)

**그림 16**: The DetailsView 현재 읽기 전용 모드에서 렌더링 됩니다 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image48.png))


DetailsView 하도록 설정 해야 하는 삽입 모드에 표시 하기 위해는 `DefaultMode` 속성을 `Inserting`합니다. 새 레코드를 삽입 한 후 유지을 먼저 방문 하는 경우에 삽입 모드에서 DetailsView를 렌더링 합니다. 그림 17에서 볼 수 있듯이 이러한 DetailsView 새 레코드를 추가 하기 위한 빠른 인터페이스를 제공 합니다.


[![DetailsView 새 제품을 빠르게 추가 위한 인터페이스를 제공 합니다.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image50.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image49.png)

**그림 17**: DetailsView 인터페이스를 제공 빠르게 추가 하기 위해 새 제품 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image51.png))


사용자가 제품 이름과 가격 (예: "Acme 물"과 같이 그림 17 1.99)를 입력 하 고 삽입을 클릭 포스트백 계속 하 고 데이터베이스에 추가 되는 새 제품 레코드에 인스턴트 삽입 워크플로 시작 됩니다. DetailsView의 삽입 인터페이스 및 GridView가 자동으로 다시 바인딩할 데이터 원본에 새 제품을 포함 하기 위해 그림 18과 같이 유지 관리 합니다.


![제품](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image52.png)

**그림 18**: 제품 "Acme 워터 라는" 데이터베이스에 추가 되었습니다


그림 18에서 GridView은 표시 되지 않습니다, DetailsView 인터페이스에서 부족 한 제품 필드 동안 `CategoryID`, `SupplierID`, `QuantityPerUnit`그에 할당 된 `NULL` 데이터베이스 값입니다. 다음 단계를 수행 하 여이 확인할 수 있습니다.

1. Visual Studio에서 서버 탐색기로 이동
2. 확장 된 `NORTHWND.MDF` 데이터베이스 노드
3. 마우스 오른쪽 단추로 클릭는 `Products` 데이터베이스 테이블 노드
4. 테이블 데이터 표시를 선택 합니다.

모든 레코드의 목록이 표시 됩니다.는 `Products` 테이블입니다. 볼 수 있듯이 그림 19 모든의 새 제품 열 이외의 `ProductID`, `ProductName`, 및 `UnitPrice` 가 `NULL` 값입니다.


[![NULL 값 할당 되는 제품 필드에에서 제공 되지 않은 DetailsView](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image54.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image53.png)

**그림 19**: 할당 된 The 제품 필드에에서 제공 되지 않은 DetailsView `NULL` 값 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image55.png))


이외의 다른 기본값을 제공 하는 것이 좋겠습니다 `NULL` 하나 이상의 이러한에 대 한 열 값인 때문에 `NULL` 없는 가장 적합 한 기본 옵션 또는 데이터베이스 열 자체 허용 되지 않기 때문 `NULL` s입니다. 이를 위해 설정할 수 있습니다 프로그래밍 방식으로 DetailsView의 매개 변수 값 `InputParameters` 컬렉션입니다. 이 할당 가능 하거나 이벤트에 처리기 DetailsView의에 대 한 `ItemInserting` 이벤트 또는 ObjectDataSource의 `Inserting` 이벤트입니다. 이미 찾았습니다 한 사전 및 사후 수준 이벤트를 사용 하 여 웹 데이터 수준을 제어,이 이번 ObjectDataSource의 이벤트를 사용 하 여 살펴보겠습니다입니다.

## <a name="step-4-assigning-values-to-thecategoryidandsupplieridparameters"></a>4 단계: 값을 할당 하는`CategoryID`및`SupplierID`매개 변수

이 자습서에 대 한 한다고 가정 하에이 인터페이스를 통해 새 제품 추가할 때 응용 프로그램에 대 한 할당 해야는 `CategoryID` 및 `SupplierID` 값이 1입니다. 앞서 언급 했 듯이 ObjectDataSource가 데이터 수정 프로세스 중 해당 화재 사전 및 사후 수준 이벤트 쌍을 가집니다. 때 해당 `Insert()` 메서드가 호출 되 면는 ObjectDataSource 먼저 발생 합니다. 해당 `Inserting` 이벤트의 경우 다음 메서드를 호출 하는 해당 `Insert()` 메서드에 매핑되지 않았습니다. 및 마지막으로 발생는 `Inserted` 이벤트입니다. `Inserting` us 이벤트 처리기를 입력된 매개 변수를 조정 하거나 완전 한 후 작업을 취소 한 마지막 기회를 제공 하는 제공 합니다.

> [!NOTE]
> 중 하나 사용 하는 경우가 실제 응용 프로그램에서 사용자는 범주와 공급 업체를 지정 하거나 몇 가지 기준에 따라에 대 한이 값을 선택 하는 또는 비즈니스 논리 (맹목적으로 선택 하는 대신 ID 1). 하지만 예제에서는 프로그래밍 방식으로 ObjectDataSource의 미리 수준 이벤트에서 입력된 매개 변수 값을 설정 하는 방법을 보여 줍니다.


ObjectDataSource의에 대 한 이벤트 처리기를 만들려면 잠시 `Inserting` 이벤트입니다. 이벤트 처리기의 두 번째 입력된 매개 변수 형식의 개체는 `ObjectDataSourceMethodEventArgs`, 매개 변수 컬렉션에 액세스 하는 속성이 있는 (`InputParameters`) 작업을 취소 하는 속성 (`Cancel`).


[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample10.cs)]

이 시점에서 `InputParameters` 속성 포함 ObjectDataSource의 `InsertParameters` DetailsView에서 할당 된 값을 사용 하 여 컬렉션입니다. 이러한 매개 변수 중 하나의 값을 변경 하려면 단순히 사용: `e.InputParameters["paramName"] = value`합니다. 따라서 설정 하는 `CategoryID` 및 `SupplierID` 조정 값을 각각 1에는 `Inserting` 이벤트 처리기는 다음과 같습니다:


[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample11.cs)]

이 시간 (예: Acme 탄산 음료) 새 제품을 추가 하는 경우는 `CategoryID` 및 `SupplierID` 신제품의 열을 1로 설정 (그림 20 참조).


[![새 제품 이제에 들어 있는 CategoryID 및 공급 업체 Id 값을 1로 설정](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image57.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image56.png)

**그림 20**: 새 제품 이제가 해당 `CategoryID` 및 `SupplierID` 값 1로 설정 ([전체 크기 이미지를 보려면 클릭](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image58.png))


## <a name="summary"></a>요약

편집, 삽입 및 삭제 프로세스를 하는 동안 데이터 웹 컨트롤 및 ObjectDataSource에서 모두 다양 한 전처리 및 후 수준 이벤트를 통해 진행 됩니다. 이 자습서에서는 미리 수준 이벤트를 검사 하 고 사용 하는 방법을 이러한 입력된 매개 변수를 사용자 지정 하거나 데이터 수정 작업을 취소할 데이터 웹 컨트롤 및 ObjectDataSource의 이벤트에서 완전히 둘 다 보여 준다는 사실을 알았습니다. 다음 자습서를 작성 하 고 사후 수준 이벤트에 대 한 이벤트 처리기를 사용 하는 방법을 살펴보겠습니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 인 재키 Goor 및 Liz Shulok 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](an-overview-of-inserting-updating-and-deleting-data-cs.md)
[다음](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)
