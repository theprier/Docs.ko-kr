---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-cs
title: 클라이언트 쪽 확인 (C#)을 삭제할 때 추가 | Microsoft Docs
author: rick-anderson
description: 지금까지 만든 인터페이스에서 사용자 편집 단추를 클릭을 고려 하는 경우 삭제 단추를 클릭 하 여 데이터를 실수로 삭제할 수 있습니다. 이 둘 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/17/2006
ms.topic: article
ms.assetid: f6e2a12a-2b5e-48fd-8db3-1e94a500c19a
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-cs
msc.type: authoredcontent
ms.openlocfilehash: 72b15d498e45cc519a14ecfe39111b224db88c30
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30880273"
---
<a name="adding-client-side-confirmation-when-deleting-c"></a>클라이언트 쪽 확인 (C#)을 삭제할 때 추가
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_22_CS.exe) 또는 [PDF 다운로드](adding-client-side-confirmation-when-deleting-cs/_static/datatutorial22cs1.pdf)

> 지금까지 만든 인터페이스에서 사용자 편집 단추를 클릭을 고려 하는 경우 삭제 단추를 클릭 하 여 데이터를 실수로 삭제할 수 있습니다. 이 자습서에서는 삭제 단추를 클릭할 때 표시 되는 클라이언트 쪽 확인 대화 상자를 추가 합니다.


## <a name="introduction"></a>소개

지난 몇 가지 자습서를 통해 म 했습니다 삽입, 편집 및 삭제 기능을 제공 하기 함께에서 우리의 응용 프로그램 아키텍처, ObjectDataSource, 및 데이터 웹 컨트롤을 사용 하는 방법을 설명 합니다. 에서는 검사 했습니다 인터페이스 삭제 하 고 Delete로 구성 된 지금까지 단추를 클릭 하 고 포스트백 ObjectDataSource s 호출 `Delete()` 메서드. `Delete()` 메서드 다음 전파는 실제 발급 하는 데이터 액세스 계층에서 호출 하는 비즈니스 논리 계층에서 구성 된 메서드를 호출 `DELETE` 데이터베이스로 문을 합니다.

이 사용자 인터페이스를 사용 하는 GridView, DetailsView, 또는 FormView 컨트롤을 통해 레코드를 삭제 하는 방문자, 하는 동안 삭제 단추를 클릭할 때 모든 종류의 확인 부족 합니다. 클릭할 실수로 삭제 단추 클릭을 고려 하는 경우 편집, 업데이트 하려는 이러한 레코드는 삭제 되 대신 합니다. 이 자습서에서는이 방지 하려면 삭제 단추를 클릭할 때 표시 되는 클라이언트 쪽 확인 대화 상자를 추가 합니다.

JavaScript `confirm(string)` 함수는 문자열 입력된 매개 변수를 함께 제공 두 단추-확인 하 고 (그림 1 참조)를 취소 하는 모달 대화 상자가 내부 텍스트로 표시 합니다. `confirm(string)` 어떤 단추를 클릭 하면에 따라 부울 값을 반환 하는 함수 (`true`[확인]을 클릭 하면, 및 `false` 취소를 클릭 하는 경우).


![JavaScript confirm(string) 메서드는 모달 클라이언트 쪽 Messagebox를 표시](adding-client-side-confirmation-when-deleting-cs/_static/image1.png)

**그림 1**: JavaScript `confirm(string)` 메서드 모달, 클라이언트 쪽 Messagebox를 표시 합니다.


값이 양식 제출 하는 동안 `false` 양식 전송을 취소 한 다음 클라이언트 쪽 이벤트 처리기에서 반환 됩니다. 이 기능을 사용 해야 삭제 단추의 클라이언트 쪽 `onclick` 이벤트 처리기에 대 한 호출의 값을 반환 `confirm("Are you sure you want to delete this product?")`합니다. [취소]를 클릭 하면 `confirm(string)` false를 취소 하려면 폼 제출을 발생을 반환 합니다. 없는 포스트백 t-이득 인 삭제 단추가 클릭 되었습니다 제품 삭제 됩니다. 그러나 확인 대화 상자에서 확인을 클릭 하는 경우 포스트백 백로그가 줄 지 않고 계속 있으며 제품 삭제 됩니다. 참조 [JavaScript를 사용 하 여 s `confirm()` 메서드를 제어 양식 전송](http://www.webreference.com/programming/javascript/confirm/) 이 기법에 대 한 자세한 내용은 합니다.

필요한 클라이언트 측 스크립트 추가 CommandField를 사용할 때 보다 템플릿을 사용 하는 경우 약간 다릅니다. 따라서이 자습서에서는 살펴보겠습니다 FormView와 GridView 예제입니다.

> [!NOTE]
> 클라이언트 쪽 확인 기술을 사용 하 여,이 자습서에 설명 된 것과 같은 사용자가 JavaScript 지원 브라우저로 방문 하 고 가정 JavaScript 사용 수 있는 합니다. 경우 이러한 가정을 중 하나에 해당 하지 않으면 특정 사용자에 대 한 삭제 단추를 클릭 하면 즉시 발생 합니다 (confirm messagebox를 표시 하지 않을) 다시 게시 합니다.


## <a name="step-1-creating-a-formview-that-supports-deletion"></a>1 단계: 삭제 작업을 지원 하는 FormView 만들기

에 FormView를 추가 하 여 시작 된 `ConfirmationOnDelete.aspx` 페이지에 `EditInsertDelete` 폴더를 통해 제품 정보를 다시 가져오는 새 ObjectDataSource에 바인딩는 `ProductsBLL` s 클래스 `GetProducts()` 메서드 합니다. ObjectDataSource를 구성할 수도 있도록는 `ProductsBLL` s 클래스 `DeleteProduct(productID)` ObjectDataSource s에 매핑되는 메서드 `Delete()` 메서드; INSERT 및 UPDATE 탭 드롭 다운 목록을 (없음)으로 설정 되어 있는지 확인 합니다. 마지막으로 확인 FormView s 스마트 태그에서 페이징 사용 확인란을 선택 합니다.

이러한 단계 이후 새 ObjectDataSource s 선언 태그 다음과 같이 표시 됩니다.


[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample1.aspx)]

낙관적 동시성을 사용 하지 않는 이전 예제와 같이 잠시 ObjectDataSource s 지울 `OldValuesParameterFormatString` 속성입니다.

만 지 원하는 삭제, FormView의 ObjectDataSource 컨트롤에 바인딩 되었던 이후 `ItemTemplate` 만 삭제 단추 부족 새로 추가 되거나 업데이트 단추를 제공 합니다. FormView s 선언 태그 반면는 불필요 한에 `EditItemTemplate` 및 `InsertItemTemplate`, 제거할 수 있습니다. 사용자 지정 하는 `ItemTemplate` 하므로 즉 제품의 하위 집합만 데이터 필드를 표시 합니다. I 내에서 s 제품 이름을 표시 하도록 구성한는 `<h3>` 해당 공급 업체 이름, 범주 이름 (함께 삭제 단추) 위에 제목입니다.


[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample2.aspx)]

이러한 변화를 통해 단순히 삭제 단추를 클릭 하 여 제품을 삭제 하는 기능 한 번에 한 제품 간을 전환할 수 있도록 허용 하는 모든 기능을 갖춘 웹 페이지 했습니다. 그림 2는 브라우저를 통해 볼 때 진행률의 스크린 샷을 지금까지 보여줍니다.


[![FormView 단일 제품에 대 한 정보를 보여 줍니다.](adding-client-side-confirmation-when-deleting-cs/_static/image3.png)](adding-client-side-confirmation-when-deleting-cs/_static/image2.png)

**그림 2**: The FormView 표시 정보에 대 한 정도 단일 제품 ([전체 크기 이미지를 보려면 클릭](adding-client-side-confirmation-when-deleting-cs/_static/image4.png))


## <a name="step-2-calling-the-confirmstring-function-from-the-delete-buttons-client-side-onclick-event"></a>삭제 단추에서 클라이언트측 onclick 이벤트에서에서 confirm(string) 함수를 호출 하는 2 단계:

만든 FormView와 마지막 단계는 삭제 단추를 구성 하는 때 것 JavaScript 방문자가 s 클릭할 `confirm(string)` 함수를 호출 합니다. 단추, LinkButton을 또는 ImageButton의 클라이언트 쪽에 클라이언트 측 스크립트 추가 `onclick` 이벤트를 사용 하 여 수행할 수 있습니다는 `OnClientClick property`, ASP.NET 2.0의 새로운 합니다. 값이 있어야 하는 데는 `confirm(string)` 함수 반환이 속성을 설정 하기만 하면: `return confirm('Are you certain that you want to delete this product?');`

이 변경 후 삭제 LinkButton s 선언적 구문 다음과 같이 표시 됩니다.


[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample3.aspx)]

모두 완료 s가입니다! 그림 3은 동작에서이 확인의 스크린 샷을 나타냅니다. 삭제 단추를 클릭 하면 확인 대화 상자가 나타납니다. 취소 단추를 클릭 하는 경우 다시 게시 취소 되 고 제품 삭제 되지 않습니다. 하지만 포스트백을 계속 하는 경우 사용자가 확인을 클릭 하 고 ObjectDataSource의 `Delete()` 메서드가 호출 되 면 삭제 하 고 데이터베이스 레코드의 정점 합니다.

> [!NOTE]
> 에 전달 되는 문자열은 `confirm(string)` JavaScript 함수 아포스트로피 (인용 부호 아님)로 구분 됩니다. JavaScript에서 문자열 문자 중 하나를 사용 하 여 구분할 수 있습니다. 여기에서 사용 아포스트로피로 전달 된 문자열에 대 한 구분 되도록 `confirm(string)` 에 사용 되는 구분 기호는 모호성을 정의 하지 않습니다는 `OnClientClick` 속성 값입니다.


[![확인은 이제 표시 때 단추를 클릭 하 고 삭제](adding-client-side-confirmation-when-deleting-cs/_static/image6.png)](adding-client-side-confirmation-when-deleting-cs/_static/image5.png)

**그림 3**: A 확인은 이제 표시 때 단추를 클릭 하면 삭제 ([전체 크기 이미지를 보려면 클릭](adding-client-side-confirmation-when-deleting-cs/_static/image7.png))


## <a name="step-3-configuring-the-onclientclick-property-for-the-delete-button-in-a-commandfield"></a>3 단계:는 CommandField에서 삭제 단추에 대 한 OnClientClick 속성 구성

에서 작업할 때는 단추나 LinkButton을 ImageButton 서식 파일에서 직접 확인 대화 상자와 연결할 수 것을 구성 하기만 하면 해당 `OnClientClick` JavaScript의 결과 반환 하는 속성 `confirm(string)` 함수입니다. 그러나, GridView 또는 DetailsView의 삭제 단추 필드에 추가-하는 CommandField 없는 `OnClientClick` 선언적으로 설정할 수 있는 속성입니다. 대신,에서는 프로그래밍 방식으로 참조 해야 적절 한 GridView 또는 DetailsView s 삭제 단추 `DataBound` 이벤트 처리기를 제거한 다음 설정의 `OnClientClick` 속성이 있습니다.

> [!NOTE]
> S 삭제 단추를 설정 하는 경우 `OnClientClick` 에서 적절 한 속성 `DataBound` 이벤트 처리기에 액세스할 수 있는 데이터는 현재 레코드에 바인딩 되었습니다. 즉, "? Chai 제품을 삭제 하 시겠습니까?" 확인 메시지와 같은 특정 레코드에 대 한 세부 정보를 포함 하도록 확장할 수 있습니다. 이러한 사용자 지정 데이터 바인딩을 구문을 사용 하 여 서식 파일에도 가능 합니다.


연습 설정으로는 `OnClientClick` let s는 CommandField에서 삭제 단추에 대 한 속성 페이지에는 GridView를 추가 합니다. FormView에서 사용 하는 동일한 ObjectDataSource 컨트롤을 사용 하도록이 GridView를 구성 합니다. GridView의 BoundFields 제품의 이름, 범주 및 공급 업체 포함 하도록 제한할 수도 있습니다. 마지막으로 확인 GridView s 스마트 태그에서 삭제 사용 확인란을 선택 합니다. GridView s에는 CommandField 추가 됩니다 `Columns` 사용 하 여 컬렉션의 `ShowDeleteButton` 속성이로 설정 `true`합니다.

다음과 같이 변경한 후 GridView s 선언 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample4.aspx)]

CommandField GridView s에서 프로그래밍 방식으로 액세스할 수 있는 단일 삭제 LinkButton 인스턴스가 포함 `RowDataBound` 이벤트 처리기입니다. 설정할 수 있습니다, 참조 되 면 해당 `OnClientClick` 속성 적절 하 게 합니다. 에 대 한 이벤트 처리기를 만들고는 `RowDataBound` 다음 코드를 사용 하 여 이벤트:


[!code-csharp[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample5.cs)]

이 이벤트 처리기는 데이터 행 (삭제 단추 갖습니다 하)과 함께 작동 하 고 프로그래밍 방식으로 삭제 단추를 참조 하 여 시작 됩니다. 일반적으로 다음과 같은 패턴을 사용 합니다.


[!code-csharp[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample6.cs)]

*ButtonType* LinkButton을 단추나 ImageButton CommandField-에서 사용 하 고 단추의 형식입니다. 기본적으로는 CommandField 링크 단추가를 사용 하지만 CommandField s 통해 사용자 지정할 수 있는이 `ButtonType property`합니다. *commandFieldIndex* 는 CommandField GridView s 내에서 서 수 인덱스 `Columns` 컬렉션 반면는 *controlIndex* 는 CommandField s 내 삭제 단추의 인덱스 `Controls` 컬렉션입니다. *controlIndex* 값은 CommandField에서 다른 단추를 기준으로 단추의 위치에 따라 달라 집니다. 예를 들어 삭제 단추는 CommandField에 표시 된 유일한 단추를 사용 하는 경우 인덱스 0 사용 합니다. 하지만 없어 s 삭제 단추 앞에 있는 편집 단추를 사용의 인덱스 2입니다. 삭제 단추 하기 전에 CommandField에서 두 개의 컨트롤을 추가 하기 때문에 2의 인덱스 사용 이유는: 편집 단추 및 LiteralControl s 편집 및 삭제 단추 사이의 공간을 추가 하는 데 사용 합니다.

특정 예제에서는 CommandField 링크 단추가 사용 하 고, 가장 왼쪽 필드 되는 *commandFieldIndex* 0입니다. 사용 하 여 다른 단추가 있지만 삭제 단추는 CommandField에서가 있을 경우는 *controlIndex* 0입니다.

삭제 단추는 CommandField에서를 참조 한 후 다음 현재 GridView 행에 바인딩된 제품에 대 한 정보를 얻을 했습니다. 마지막으로, s 삭제 단추 설정 `OnClientClick`의 제품 이름을 포함 하는 적절 한 JavaScript에는 속성입니다. JavaScript 문자열에 전달 되므로 `confirm(string)` 함수 아포스트로피 이전 살아야 s 제품 이름 내에 나타나는 아포스트로피가 사용 하 여 구분 합니다. 특히, s 제품 이름에 아포스트로피가로 이스케이프 "`\'`"입니다.

이러한 변경 내용으로 전체를 사용자 지정된 확인 대화 상자 (그림 4 참조)는 GridView 디스플레이에서 삭제 단추를 클릭 합니다. 로 FormView에서 확인 messagebox와 취소를 클릭 하는 경우 다시 게시 취소 되 발생 삭제 것을 방지 합니다.

> [!NOTE]
> 이 기술은 프로그래밍 방식으로 액세스 한 DetailsView에 CommandField에서 삭제 단추 데도 사용할 수 있습니다. 그러나 Detailsview, d 만들면에 대 한 이벤트 처리기는 `DataBound` DetailsView 하지 않았으므로 이벤트는 `RowDataBound` 이벤트입니다.


[![GridView의 삭제 단추를 클릭 하면 사용자 지정된 확인 대화 상자가 표시 됩니다.](adding-client-side-confirmation-when-deleting-cs/_static/image9.png)](adding-client-side-confirmation-when-deleting-cs/_static/image8.png)

**그림 4**: 사용자 지정 확인 대화 상자를 표시 GridView의 삭제 단추를 클릭 하면 ([전체 크기 이미지를 보려면 클릭](adding-client-side-confirmation-when-deleting-cs/_static/image10.png))


## <a name="using-templatefields"></a>TemplateFields를 사용 하 여

CommandField의 단점 중 하나는 인덱싱을 통해 단추에 액세스 해야 하 고 결과 개체 (예: 단추, LinkButton을 또는 ImageButton) 적절 한 단추 형식으로 캐스팅 되어야 합니다. "매직 넘버" 및 하드 코드 된 형식을 사용 하 여 런타임이 될 때까지 검색 될 수 없는 문제가 발생할 수 있습니다. 예를 들어, 또는 다른 개발자에 게 (예: 편집 단추) 나중에 특정 시점 또는 변경 내용에서 CommandField에 새 단추를 추가 하는 경우는 `ButtonType` 속성을 기존 코드는 여전히 오류 없이 컴파일되지만 페이지를 방문 하면 예외가 발생할 수 있습니다 또는 코드를 작성 하는 방법 및 적용 된 변경 내용에 따라 예기치 않은 동작입니다.

다른 접근 방식은 TemplateFields에 GridView 및 DetailsView의 CommandFields 변환 하는 것입니다. 와 TemplateField 자동으로 생성 됩니다는 `ItemTemplate` LinkButton (또는 단추 또는 ImageButton)는 CommandField의 각 단추에 있는 합니다. 이러한 단추 `OnClientClick` 속성 FormView, 볼 하거나 적절 한에서 프로그래밍 방식으로 액세스할 수 있습니다, 선언적 할당할 수 있습니다 `DataBound` 이벤트 처리기는 다음 패턴을 사용 하 여:


[!code-csharp[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample7.cs)]

여기서 *controlID* s 단추의 값은 `ID` 속성입니다. 이 패턴은 여전히 캐스트에 대 한 하드 코드 된 형식이 필요한, 하는 동안 제거 인덱싱에 대 한 필요성 런타임 오류가 발생 하지 않고 변경 하려면 레이아웃에 대 한 허용 됩니다.

## <a name="summary"></a>요약

JavaScript `confirm(string)` 함수는 일반적으로 사용 되는 기술 제어 양식 제출 워크플로에 대 한 합니다. 를 실행 하면 함수 확인 및 취소 단추를 포함 하는 모달, 클라이언트 쪽 대화 상자를 표시 합니다. [확인]을 클릭 하면는 `confirm(string)` 함수에서 반환 `true`; 반환 취소를 클릭 하면 `false`합니다. 이 기능을 제출 하는 동안 이벤트 처리기를 반환 하는 경우 양식을 제출 하 여 취소 하는 브라우저의 동작와 결합 되어 `false`는 레코드를 삭제할 때 확인 messagebox를 표시 하는 데 사용할 수 있습니다.

`confirm(string)` 함수 단추 웹 컨트롤의 클라이언트 쪽에 연결할 수 `onclick` s 제어를 통해 이벤트 처리기 `OnClientClick` 속성입니다. 삭제 단추 템플릿-s FormView 템플릿 중 하나 또는 DetailsView 또는 GridView-TemplateField 중 하나에서 작업할 때이 속성 선언적으로 또는 프로그래밍 방식으로이 자습서에서 살펴본 것 처럼 합니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [이전](implementing-optimistic-concurrency-cs.md)
> [다음](limiting-data-modification-functionality-based-on-the-user-cs.md)
