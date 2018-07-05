---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-vb
title: (VB)를 삭제할 때 클라이언트 쪽 확인 추가 | Microsoft Docs
author: rick-anderson
description: 사용자는 지금까지 만든 인터페이스의 편집 단추 클릭을 의미 하는 경우 삭제 단추를 클릭 하 여 데이터를 실수로 삭제할 수 있습니다. 이 t...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/17/2006
ms.topic: article
ms.assetid: 6331e02e-c465-4cdf-bd3f-f07680c289d6
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-vb
msc.type: authoredcontent
ms.openlocfilehash: acab34cb362bd3e3351156a41a6826d03e5a749f
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37388269"
---
<a name="adding-client-side-confirmation-when-deleting-vb"></a>(VB)를 삭제할 때 클라이언트 쪽 확인 추가
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_22_VB.exe) 또는 [PDF 다운로드](adding-client-side-confirmation-when-deleting-vb/_static/datatutorial22vb1.pdf)

> 사용자는 지금까지 만든 인터페이스의 편집 단추 클릭을 의미 하는 경우 삭제 단추를 클릭 하 여 데이터를 실수로 삭제할 수 있습니다. 이 자습서에서 삭제 단추를 클릭할 때 표시 되는 클라이언트 쪽 확인 대화 상자를 추가 합니다.


## <a name="introduction"></a>소개

지난 몇 가지 자습서를 통해에서는 ve를 사용 하 여 응용 프로그램 아키텍처, ObjectDataSource, 및 데이터 웹 컨트롤과 함께에서 삽입, 편집 및 삭제 기능을 제공 하는 방법을 설명 합니다. 에서는 검사 ve 인터페이스 삭제 하 고 삭제로 구성 된 지금 단추를 클릭 하 고 포스트백을 발생 시키는 ObjectDataSource가 호출 하는 경우 `Delete()` 메서드. 합니다 `Delete()` 메서드 다음으로 발급 하는 실제 데이터 액세스 계층에 호출을 전파 하는 비즈니스 논리 계층에서 구성 된 메서드를 호출 `DELETE` 데이터베이스로 문입니다.

이 사용자 인터페이스에는 GridView, FormView DetailsView 컨트롤을 통해 레코드를 삭제 하는 방문자 수, 사용자가 삭제 단추를 클릭 하면 모든 종류를의 확인 없습니다. 사용자가 클릭 하면 실수로 삭제 단추 클릭을 의미 하는 경우 편집, 업데이트 하려는 해당 레코드를 삭제할 수 대신 합니다. 이 자습서에서는이 방지 하려면 삭제 단추를 클릭할 때 표시 되는 클라이언트 쪽 확인 대화 상자를 추가 합니다.

JavaScript `confirm(string)` 함수 확인 두 단추-와 함께 제공 됩니다 (그림 1 참조)를 취소 하는 모달 대화 상자 내에서 텍스트 문자열 입력된 매개 변수를 표시 합니다. 합니다 `confirm(string)` 어떤 단추에 따라 부울 값을 반환 하는 함수 (`true`확인을 클릭 하면, 및 `false` 취소 클릭 하는 경우).


![표시 됩니다는 모달 Messagebox 클라이언트 쪽 JavaScript confirm(string) 메서드](adding-client-side-confirmation-when-deleting-vb/_static/image1.png)

**그림 1**: JavaScript `confirm(string)` 모달, 클라이언트 쪽 Messagebox를 표시 하는 메서드


값 없이 폼 전송 하는 동안 `false` 가 반환 되는 클라이언트측 이벤트 처리기에서 폼 제출을 취소 됩니다. 이 기능을 사용 수 있다고 Delete 단추의 클라이언트측 `onclick` 이벤트 처리기에 대 한 호출의 값을 반환 `confirm("Are you sure you want to delete this product?")`합니다. 사용자가 [취소]를 클릭 하면 `confirm(string)` false에 취소 하려면 폼 제출을 발생을 반환 합니다. 다시 게시를 사용 하 여 t 작업이 적용 된 삭제 단추를 클릭 한 제품 삭제할 수 있습니다. 그러나 확인 대화 상자에서 확인을 클릭 하는 경우 포스트백 지날수록 계속 하 고 제품 삭제 됩니다. 참조 하세요 [JavaScript를 사용 하 여 s `confirm()` 컨트롤이 폼 제출을 방법](http://www.webreference.com/programming/javascript/confirm/) 이 기술에 대 한 자세한 내용은 합니다.

필요한 클라이언트 측 스크립트 추가 CommandField를 사용할 때 보다 템플릿을 사용 하는 경우 약간 다릅니다. 따라서이 자습서에서는 살펴보겠습니다 FormView 및 GridView 예제입니다.

> [!NOTE]
> 클라이언트 쪽 확인 기술을 사용 하 여,이 자습서에 설명 된 것과 같은 가정 JavaScript를 지 원하는 브라우저를 사용 하 여 사용자가 방문 하는 있고 JavaScript를 사용 하도록 설정 합니다. 특정 사용자에 대 한 true 이러한 가정을 하나 없으면 삭제 단추를 클릭 하는 즉시 포스트백을 발생 (확인 messagebox 표시 되지 않음).


## <a name="step-1-creating-a-formview-that-supports-deletion"></a>1 단계: 삭제를 지 원하는 FormView 만들기

FormView를 추가 하 여 시작 합니다 `ConfirmationOnDelete.aspx` 페이지를 `EditInsertDelete` 폴더를 통해 제품 정보를 다시 가져오는 새 ObjectDataSource에 바인딩하지는 `ProductsBLL` s 클래스 `GetProducts()` 메서드. ObjectDataSource를 구성할 수도 있도록를 `ProductsBLL` s 클래스 `DeleteProduct(productID)` 메서드가 ObjectDataSource가 매핑되는 `Delete()` 메서드 드롭 다운 목록 (없음)로 INSERT 및 UPDATE 탭 있는지 확인 합니다. 마지막으로, FormView s 스마트 태그의 페이징 사용 확인란을 확인 합니다.

이러한 단계 후 새 ObjectDataSource가 선언적 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](adding-client-side-confirmation-when-deleting-vb/samples/sample1.aspx)]

낙관적 동시성을 사용 하지 않는 이전 예제와 같이 잠시 ObjectDataSource가 지울 `OldValuesParameterFormatString` 속성입니다.

FormView s 삭제만 지 원하는 ObjectDataSource 컨트롤에 바인딩된 것 이므로 `ItemTemplate` 만 삭제 단추 없는 신규 및 업데이트 단추를 제공 합니다. FormView s 선언적 태그에 포함 되어 있습니다를 불필요 `EditItemTemplate` 및 `InsertItemTemplate`를 제거할 수 있습니다. 잠시 사용자 지정 하는 `ItemTemplate` 하므로 즉 제품의 하위 집합만 데이터 필드를 표시 합니다. I ve 구성에서 s 제품 이름을 표시 하려면 마이닝는 `<h3>` 해당 공급 업체 이름, 범주 이름 (함께 삭제 단추) 위에 제목입니다.


[!code-aspx[Main](adding-client-side-confirmation-when-deleting-vb/samples/sample2.aspx)]

이러한 변화를 통해 삭제 단추를 클릭 하 여 제품을 삭제 하는 기능을 사용 하 여 한 번에 한 제품 간을 전환 하려면 사용자를 허용 하는 웹 페이지를 완벽 하 게 작동 했습니다. 그림 2 브라우저를 통해 볼 때 지금 스크린샷을 진행 상황을 보여줍니다.


[![FormView 단일 제품에 대 한 정보를 보여 줍니다.](adding-client-side-confirmation-when-deleting-vb/_static/image3.png)](adding-client-side-confirmation-when-deleting-vb/_static/image2.png)

**그림 2**: The FormView 표시 정보에 대 한는 단일 제품 ([큰 이미지를 보려면 클릭](adding-client-side-confirmation-when-deleting-vb/_static/image4.png))


## <a name="step-2-calling-the-confirmstring-function-from-the-delete-buttons-client-side-onclick-event"></a>삭제 단추-클라이언트측 onclick 이벤트에서에서 confirm(string) 함수를 호출 하는 2 단계:

마지막 단계는 만든 FormView를 사용 하 여 구성 된 삭제 단추를 때가 방문자를 JavaScript에서 s 클릭 `confirm(string)` 함수가 호출 됩니다. 단추나 LinkButton, ImageButton의 클라이언트 쪽에 클라이언트 측 스크립트 추가 `onclick` 이벤트를 사용 하 여 수행할 수 있습니다는 `OnClientClick property`, ASP.NET 2.0에는 합니다. 값을 가질 것 이므로 `confirm(string)` 함수 반환이 속성을 설정 하기만 하면 됩니다. `return confirm('Are you certain that you want to delete this product?');`

이 변경 후 삭제 LinkButton s 선언적 구문을 같이 표시 됩니다.


[!code-aspx[Main](adding-client-side-confirmation-when-deleting-vb/samples/sample3.aspx)]

S 모두 완료 되었습니다! 그림 3 작업에서이 확인의 스크린 샷을 보여 줍니다. 확인 대화 상자를 엽니다 삭제 단추를 클릭 합니다. 사용자가 취소 클릭 하면 포스트백 취소 되 고 제품 삭제 되지 않습니다. 포스트백 계속 경우 단, 사용자가 확인 및 ObjectDataSource의 `Delete()` 메서드가 호출 되 면 삭제 하 고 데이터베이스 레코드의 정점입니다.

> [!NOTE]
> 에 전달 된 문자열을 `confirm(string)` JavaScript 함수는 아포스트로피 (인용 부호 아님)를 사용 하 여 구분 됩니다. JavaScript에서 문자열 문자 중 하나를 사용 하 여 구분할 수 있습니다. 여기에서 사용 아포스트로피 문자열 구분 기호에 전달 되도록 `confirm(string)` 에 사용 되는 구분 기호를 사용 하 여 모호성을 발생 하지는 `OnClientClick` 속성 값입니다.


[![확인은 이제 표시 된 경우 삭제 단추를 클릭](adding-client-side-confirmation-when-deleting-vb/_static/image6.png)](adding-client-side-confirmation-when-deleting-vb/_static/image5.png)

**그림 3**:는 확인은 이제 표시 된 경우 삭제 단추를 클릭 ([큰 이미지를 보려면 클릭](adding-client-side-confirmation-when-deleting-vb/_static/image7.png))


## <a name="step-3-configuring-the-onclientclick-property-for-the-delete-button-in-a-commandfield"></a>CommandField의 삭제 단추에 대 한 OnClientClick 속성을 구성 하는 3 단계:

에서 작업할 때 단추나 LinkButton, ImageButton 템플릿에서 직접 확인 대화 상자와 연결할 수 있습니다이 간단히 구성 하 여 해당 `OnClientClick` JavaScript의 결과 반환할 속성 `confirm(string)` 함수입니다. 그러나-추가 하는 필드 삭제 단추의 GridView 또는 DetailsView-CommandField 없는 `OnClientClick` 선언적으로 설정할 수 있는 속성입니다. 대신 적절 한 GridView 또는 DetailsView s에 삭제 단추를 프로그래밍 방식으로 참조 해야 합니다 `DataBound` 이벤트 처리기를 설정 하 고 해당 `OnClientClick` 속성이 있습니다.

> [!NOTE]
> S 삭제 단추를 설정 하는 경우 `OnClientClick` 속성에 적절 한 `DataBound` 이벤트 처리기에 액세스할 수는 데이터는 현재 레코드에 바인딩 되었습니다. 즉, "Are you Chai 제품을 삭제 하 시겠습니까?" 확인 메시지와 같은 특정 레코드에 대 한 세부 정보를 포함 하도록 확장할 수 있습니다. 이러한 사용자 지정 데이터 바인딩 구문을 사용 하 여 템플릿에서 가능 합니다.


실제로 설정 된 `OnClientClick` CommandField, let s에에서 삭제 단추에 대 한 속성 페이지에 GridView를 추가 합니다. 이 GridView FormView 사용 하는 동일한 ObjectDataSource 컨트롤을 사용 하도록 구성 합니다. GridView의 BoundFields 제품의 이름, 범주 및 공급자만 포함 하도록 제한할 수도 있습니다. 마지막으로, GridView가 스마트 태그에서 삭제 사용 확인란을 확인 합니다. 이렇게를 CommandField GridView s에 추가 됩니다 `Columns` 컬렉션과 해당 `ShowDeleteButton` 속성으로 설정 `true`합니다.

다음과 같이 변경한 후 GridView가 선언적 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](adding-client-side-confirmation-when-deleting-vb/samples/sample4.aspx)]

CommandField GridView s에서 프로그래밍 방식으로 액세스할 수 있는 단일 삭제 LinkButton 인스턴스가 포함 `RowDataBound` 이벤트 처리기입니다. 설정할 수 있습니다 참조 되 면 해당 `OnClientClick` 속성 적절 하 게 합니다. 에 대 한 이벤트 처리기 만들기는 `RowDataBound` 다음 코드를 사용 하 여 이벤트:


[!code-vb[Main](adding-client-side-confirmation-when-deleting-vb/samples/sample5.vb)]

이 이벤트 처리기는 데이터 행 (해당 삭제 단추에 있는)를 사용 하 여 작동 하 고 삭제 단추를 프로그래밍 방식으로 참조 하 여 시작 합니다. 일반적인 패턴을 사용 합니다.


[!code-vb[Main](adding-client-side-confirmation-when-deleting-vb/samples/sample6.vb)]

*ButtonType* 유형 CommandField-단추나 LinkButton, imagebutton이 사용 되는 단추입니다. 기본적으로 CommandField Linkbutton을를 사용 하지만 CommandField s를 통해 사용자 지정할 수 있습니다이 `ButtonType property`합니다. 합니다 *commandFieldIndex* GridView s 내 CommandField의 서 수 인덱스 `Columns` 컬렉션 반면 합니다 *controlIndex* CommandField s에 삭제 단추의 인덱스 `Controls` 컬렉션입니다. 합니다 *controlIndex* 값은 CommandField 다른 단추를 기준으로 단추의 위치에 따라 달라 집니다. 예를 들어 삭제 단추는 CommandField에 표시 되는 단추를 사용 하는 경우 인덱스 0 사용 합니다. 그러나 있는 s 삭제 단추 앞에 오는 편집 단추를 사용의 인덱스 2입니다. 삭제 단추 전에 CommandField 하 여 두 개의 추가 되기 때문에 2의 인덱스가 사용 되는 이유는: 편집 단추와는 LiteralControl s 편집 및 삭제 단추 사이의 공간을 추가 하는 데 사용 합니다.

특정 예제는 CommandField Linkbutton을 사용 하 여을 가장 왼쪽 필드에 있는 한 *commandFieldIndex* 0입니다. 다른 단추가 없습니다 있지만 CommandField에서 삭제 단추를 없으므로 사용 하 여는 *controlIndex* 0입니다.

CommandField에서 삭제 단추를 참조 한 후 다음 현재 GridView 행에 바인딩된 제품에 대 한 정보를 얻을 것입니다. 마지막으로, s 삭제 단추를 설정 했습니다 `OnClientClick`의 제품 이름을 포함 하는 적절 한 JavaScript에는 속성입니다. JavaScript 문자열에 전달 되므로 `confirm(string)` 함수의 제품 이름 내에 나타나는 모든 아포스트로피를 이스케이프 처리 해야 했습니다 아포스트로피를 사용 하 여 구분 됩니다. S 제품 이름에 아포스트로피가 사용 하 여 이스케이프 되는 특히 "`\'`"입니다.

이러한 변경 내용 전체를 사용 하 여 사용자 지정된 확인 대화 상자 (그림 4 참조) 하는 GridView 디스플레이에서 삭제 단추를 클릭 합니다. 으로 FormView에서 확인 messagebox를 사용 하 여 취소를 클릭 하면 포스트백 취소 되 삭제가 발생을 방지 합니다.

> [!NOTE]
> 이 기술은 프로그래밍 방식으로 액세스 한 DetailsView에서 CommandField 있는 삭제 단추의 데도 사용할 수 있습니다. 그러나 DetailsView, d 만들어야에 대 한 이벤트 처리기를 `DataBound` DetailsView 없으므로 이벤트는 `RowDataBound` 이벤트입니다.


[![사용자 지정된 확인 대화 상자를 표시 GridView의 삭제 단추를 클릭 합니다.](adding-client-side-confirmation-when-deleting-vb/_static/image9.png)](adding-client-side-confirmation-when-deleting-vb/_static/image8.png)

**그림 4**: 사용자 지정 확인 대화 상자를 표시 GridView의 삭제 단추를 클릭 하면 ([큰 이미지를 보려면 클릭](adding-client-side-confirmation-when-deleting-vb/_static/image10.png))


## <a name="using-templatefields"></a>TemplateFields 사용

CommandField의 단점 중 하나는 인덱싱을 통해 해당 단추에 액세스 해야 하 고 결과 개체는 (단추, LinkButton, 또는 ImageButton) 단추를 적절 한 형식으로 캐스팅 해야 합니다. "매직 넘버" 및 하드 코드 된 형식을 사용 하 여 런타임 시까지 검색 될 수 없는 문제가 발생할 수 있습니다. 예를 들어, 사용자 또는 다른 개발자에 게 (예: 편집 단추) 나중에 특정 시점 또는 변경 CommandField에 새 단추를 추가 하는 경우는 `ButtonType` 속성을 기존 코드는 여전히 오류 없이 컴파일되지만 페이지를 방문 하는 예외를 일으킬 수 또는 코드를 작성 하는 방법 및 적용 된 변경 내용에 따라 예기치 않은 동작입니다.

GridView 및 DetailsView의 CommandFields TemplateFields 변환 하는 또 다른 방법은 합니다. 사용 하 여 templatefield로 생성 됩니다는 `ItemTemplate` 는 LinkButton (단추 또는 ImageButton)는 CommandField의 각 단추에 있는 합니다. 이러한 단추 `OnClientClick` FormView, 향상 된 것 또는 적절 한에 프로그래밍 방식으로 액세스할 수 있습니다 속성 선언적으로 할당할 수 있습니다 `DataBound` 패턴을 사용 하 여 이벤트 처리기:


[!code-vb[Main](adding-client-side-confirmation-when-deleting-vb/samples/sample7.vb)]

여기서 *controlID* s 단추의 값인 `ID` 속성입니다. 이 패턴 여전히 하드 코드 된 형식에 대 한 필요한 캐스팅 하는 동안 해당 필요가 인덱싱에 대 한 레이아웃을 런타임 오류가 발생 하지 않고 변경할 수 있습니다.

## <a name="summary"></a>요약

JavaScript `confirm(string)` 함수는 제어 양식 제출 워크플로 일반적으로 사용 되는 기술입니다. 를 실행 하는 경우 함수는 OK 및 Cancel 단추를 포함 하는 모달, 클라이언트 쪽 대화 상자를 표시 합니다. 확인을 클릭 하면 합니다 `confirm(string)` 함수에서 반환 `true`; 취소를 클릭 하면 반환 `false`합니다. 제출 프로세스 중 이벤트 처리기를 반환 하는 경우 폼 제출을 취소 하려면 브라우저의 동작을 사용 하 여이 기능을 결합 `false`, 레코드를 삭제 하는 경우 확인 messagebox를 표시 하려면 사용할 수 있습니다.

`confirm(string)` 함수를 단추 웹 컨트롤의 클라이언트 쪽을 사용 하 여 연결할 수 있습니다 `onclick` 이벤트 처리기가의 컨트롤을 통해 `OnClientClick` 속성입니다. 템플릿-FormView의 템플릿 중 하나 또는 DetailsView 또는 GridView-TemplateField 중 하나에서 삭제 단추를 사용 하 여 작업 하는 경우이 속성 선언적으로 또는 프로그래밍 방식으로이 자습서에서 살펴본 것 처럼 합니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [이전](implementing-optimistic-concurrency-vb.md)
> [다음](limiting-data-modification-functionality-based-on-the-user-vb.md)
