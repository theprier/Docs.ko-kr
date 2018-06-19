---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb
title: 편집을 유효성 검사 컨트롤을 추가 하 고 인터페이스 (VB) 삽입 | Microsoft Docs
author: rick-anderson
description: 이 자습서를 더 많이 제공 하는 EditItemTemplate 및 InsertItemTemplate 웹 컨트롤을 데이터에 유효성 검사 컨트롤을 추가할 얼마나 쉬운지 살펴보겠습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/17/2006
ms.topic: article
ms.assetid: e3d7028a-7a22-4a4f-babe-d53afc41c0e2
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb
msc.type: authoredcontent
ms.openlocfilehash: eda86c5481e5739b6cd9a2470889a26144302a3f
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30887943"
---
<a name="adding-validation-controls-to-the-editing-and-inserting-interfaces-vb"></a>편집을 유효성 검사 컨트롤을 추가 하 고 인터페이스 (VB)를 삽입 합니다.
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_19_VB.exe) 또는 [PDF 다운로드](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/datatutorial19vb1.pdf)

> 이 자습서에서는 EditItemTemplate 및 웹 컨트롤을 데이터의 InsertItemTemplate 간단 명료 하는 사용자 인터페이스에 유효성 검사 컨트롤을 추가 하는 것이 얼마나 쉬운지 살펴보겠습니다.


## <a name="introduction"></a>소개

예제에 GridView 및 DetailsView 컨트롤 것에 대해 알아보았으므로 세 개의 자습서가 모두 되었습니다 BoundFields와 구성 CheckBoxFields (필드 유형 GridView 또는 DetailsView 데이터 소스에 바인딩할 때 Visual Studio에서 자동으로 추가 하는 지난 컨트롤에 스마트 태그를 통해). GridView 또는 DetailsView의 행을 편집할 때 텍스트 상자에 읽기 전용으로 설정 하지 않은 이러한 BoundFields 변환 됩니다 최종 사용자를 기존 데이터를 수정할 수 있습니다. 마찬가지로 때 새 삽입 기록에 이러한 BoundFields DetailsView 컨트롤을 갖는 `InsertVisible` 속성이 `True` (기본값) 사용자는 새 레코드의 필드 값을 제공할 수 빈 입력란으로 렌더링 됩니다. 마찬가지로, 표준, 읽기 전용 인터페이스에서 비활성화 되어 있는 CheckBoxFields 편집 및 인터페이스를 삽입에 사용 가능한 확인란으로 변환 됩니다.

기본 편집 및 BoundField 및 CheckBoxField에 대 한 인터페이스를 삽입 하는 것이 도움이 동안 인터페이스에는 모든 종류의 유효성 검사에 부족 합니다. 사용자가 데이터 항목이 잘못-생략 하는 것 같은 경우는 `ProductName` 필드 또는 입력에 잘못 된 값 `UnitsInStock` (예:-50) 예외가 발생 합니다에서 중첩 된 응용 프로그램 아키텍처의 합니다. 와 같이이 예외가 정상적으로 처리할 수 있습니다 하는 동안는 [이전 자습서](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md), 편집 하거나 사용자 인터페이스를 삽입 하는 사용자가 이러한 잘못 된 데이터에 사용할 수 없음 방지 하기 위해 유효성 검사 컨트롤 포함 이상적으로 먼저 배치 합니다.

사용자 지정 된 편집 또는 삽입 인터페이스를 제공 하기 위해를 TemplateField BoundField 또는 CheckBoxField 대체 해야 합니다. 토론의 주제 였던 TemplateFields에는 [GridView 컨트롤에 사용 하 여 TemplateFields](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md) 및 [DetailsView 컨트롤에서 사용 하 여 TemplateFields](../custom-formatting/using-templatefields-in-the-detailsview-control-vb.md) 자습서는 여러 구성 될 수 있습니다 템플릿 정의 다른 행 상태에 대 한 인터페이스를 구분 합니다. TemplateField의 `ItemTemplate` 는를 사용 하는 읽기 전용 필드 또는 DetailsView 또는 GridView 컨트롤의 행을 렌더링 하는 경우 반면는 `EditItemTemplate` 및 `InsertItemTemplate` 는 편집 및 모드를 각각 삽입에 대 한 사용 하는 인터페이스를 나타냅니다.

이 자습서에서는 보겠습니다 TemplateField의에 유효성 검사 컨트롤을 추가할 얼마나 쉬운지 `EditItemTemplate` 및 `InsertItemTemplate` 간단 명료 사용자 인터페이스를 제공할 수 있습니다. 이 자습서에서 만든 예제를 사용 하는 구체적으로 [삽입, 업데이트 및 삭제와 관련 된 이벤트를 검사 하](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md) 적절 한 유효성 검사를 포함 하도록 인터페이스 자습서 및 편집 및 삽입 보완 합니다.

## <a name="step-1-replicating-the-example-fromexamining-the-events-associated-with-inserting-updating-and-deletingexamining-the-events-associated-with-inserting-updating-and-deleting-vbmd"></a>1 단계: 복제의 예제[삽입, 업데이트 및 삭제와 관련 된 이벤트 검사](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)

에 [삽입, 업데이트 및 삭제와 관련 된 이벤트를 검사](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md) 자습서 이름과 편집 가능한 GridView의 제품 가격을 나열 하는 페이지를 만들었습니다. 또한 페이지 포함 DetailsView 인 `DefaultMode` 속성이로 설정 된 `Insert`삽입 모드에서 렌더링 되므로 항상, 합니다. 이 DetailsView 사용자 수 입력 이름과 가격 새 제품에 대 한, 삽입을 클릭 하 고 시스템에 추가 하 게 (그림 1 참조).


[![이전 예제에서는 새로운 제품을 추가 하 고 기존 관계를 편집 하려면 사용자가](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image2.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image1.png)

**그림 1**: The 이전 예에서는 허용 사용자가을 새 프로젝트 추가 및 편집할 기존 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image3.png))


이 자습서의 목표는 유효성 검사 컨트롤을 제공 하는 DetailsView 및 GridView 보강 것입니다. 특히,이 유효성 검사 논리를 수행합니다.

- 하려면 삽입 되거나 편집 제품 이름을 제공 되어야
- 가격을; 레코드를 삽입할 때 제공 되어야 필요 레코드를 편집할 때 것은 여전히 가격을 필요로 할 수 있지만 GridView의에서 프로그래밍 논리를 사용 하는 `RowUpdating` 이미 있는 이전 자습서에서 이벤트 처리기
- 가격에 대 한 입력 한 값이 올바른 통화 형식 인지 확인

유효성 검사를 포함 하도록 이전 예제를 확대 살펴보면 먼저 해야의 예제를 복제 하는 `DataModificationEvents.aspx` 이 자습서에 대 한 페이지에 페이지 `UIValidation.aspx`합니다. 둘 모두를 통해 복사 하려면 해야이를 위해는 `DataModificationEvents.aspx` 페이지의 선언적 태그와 해당 소스 코드입니다. 먼저 다음 단계를 수행 하 여 선언적 태그를 통해 복사 합니다.

1. 열기는 `DataModificationEvents.aspx` Visual Studio에서 페이지
2. 페이지의 선언적 태그 (페이지 아래쪽에 원본 단추 클릭)로 이동
3. 내에서 텍스트를 복사는 `<asp:Content>` 및 `</asp:Content>` 그림 2로 태그 (줄 3-44).


[![텍스트 내에서 복사 된 &lt;asp: Content&gt; 컨트롤](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image5.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image4.png)

**그림 2**: 텍스트 내 복사는 `<asp:Content>` 컨트롤 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image6.png))


1. 열기는 `UIValidation.aspx` 페이지
2. 페이지의 선언적 태그로 이동
3. 내에서 텍스트를 붙여는 `<asp:Content>` 제어 합니다.

소스 코드를 복사한 열고는 `DataModificationEvents.aspx.vb` 페이지 및 텍스트만 복사 *내* 는 `EditInsertDelete_DataModificationEvents` 클래스입니다. 세 개의 이벤트 처리기를 복사 (`Page_Load`, `GridView1_RowUpdating`, 및 `ObjectDataSource1_Inserting`), 매개 변수 태그가 **하지** 클래스 선언에 복사 합니다. 다음 복사한 텍스트를 붙여 *내* 는 `EditInsertDelete_UIValidation` 클래스 `UIValidation.aspx.vb`합니다.

내용 및 코드를 통해 이동 후 `DataModificationEvents.aspx` 를 `UIValidation.aspx`, 브라우저에서 진행 상황을 테스트 하려면 잠시 합니다. 동일한 출력 및 각 이러한 두 페이지에 동일한 기능을 경험 나타납니다 (의 스크린 샷을 대 한 그림 1을 다시 참조 `DataModificationEvents.aspx` 실행에서).

## <a name="step-2-converting-the-boundfields-into-templatefields"></a>2 단계: TemplateFields는 BoundFields 변환

유효성 검사 컨트롤에는 편집 및 삽입 인터페이스를 추가 하려면 DetailsView 및 GridView 컨트롤에서 사용 하는 BoundFields TemplateFields로 변환 해야 합니다. 이 위해 필드 편집 및 열 편집 링크 GridView 및 DetailsView의 스마트 태그를을 각각 클릭 합니다. 여기에 BoundFields의 각를 선택 하 고 "이이 필드를 TemplateField로 변환" 링크를 클릭 합니다.


[![DetailsView의 및 GridView의 BoundFields 각 TemplateFields로 변환](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image8.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image7.png)

**그림 3**: DetailsView의 및 GridView의 BoundFields에 TemplateFields 각각 변환 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image9.png))


자체 BoundField 동일한 읽기 전용, 편집 및 삽입 인터페이스를 보여 주는 TemplateField 생성 BoundField 필드 대화 상자를 통해 TemplateField로 변환 합니다. 다음 태그는 선언적 구문을 보여 줍니다.는 `ProductName` 필드를 TemplateField로 변환한 후 DetailsView에:

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample1.aspx)]

이 TemplateField가 자동으로 생성 하는 세 개의 템플릿이 있는지 참고 `ItemTemplate`, `EditItemTemplate`, 및 `InsertItemTemplate`합니다. `ItemTemplate` 단일 데이터 필드 값이 표시 됩니다 (`ProductName`) Label 웹 컨트롤을 사용 하는 동안는 `EditItemTemplate` 및 `InsertItemTemplate` 하 고 입력란의 데이터 필드에 연결 하는 TextBox 웹 컨트롤에 데이터 필드 값을 제공할 `Text` 양방향 데이터 바인딩을 사용 하는 속성입니다. 제거 될 수 있습니다만 DetailsView이이 페이지에 삽입 하는 데를 사용 하므로 `ItemTemplate` 및 `EditItemTemplate` 두 TemplateFields에서 두지 하더라도 피해는 없지만 합니다.

GridView DetailsView의 기능을 삽입, GridView의 변환에 기본 제공 지원 하지 않으므로 `ProductName` 필드를 TemplateField로만 결과 `ItemTemplate` 및 `EditItemTemplate`:

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample2.aspx)]

"이이 필드를 TemplateField로 변환"를 클릭 하 여 Visual Studio는 해당 템플릿을 변환 된 BoundField의 사용자 인터페이스를 모방 TemplateField 만들었습니다. 브라우저를 통해이 페이지를 방문 하 여이 확인할 수 있습니다. BoundFields 대신 사용 될 때 모양 및 동작의 TemplateFields의 환경에 동일한를 찾을 수 있습니다.

> [!NOTE]
> 자유롭게 필요에 따라 서식 파일의 편집 인터페이스를 사용자 지정할 수 있습니다. 예를 들어 하려는 텍스트 상자에 있는 `UnitPrice` TemplateFields 보다 더 작은 textbox로 렌더링 되는 `ProductName` 텍스트 상자에 붙여넣습니다. 이를 위해 텍스트 상자의 설정할 수 있습니다 `Columns` 속성을 적절 한 값을 통해 절대 너비를 제공 하거나는 `Width` 속성입니다. 다음 자습서 완전히 웹 컨트롤 대체 데이터 항목으로 텍스트 상자를 대체 하 여 편집 인터페이스를 사용자 지정 하는 방법을 살펴보겠습니다.


## <a name="step-3-adding-the-validation-controls-to-the-gridviewsedititemtemplate-s"></a>3 단계: GridView의에 유효성 검사 컨트롤을 추가`EditItemTemplate` s

데이터 입력 폼을 생성할 때에는 사용자가 모든 필수 필드를 입력 하는 모든 제공 된 입력 값 법률, 올바르게 포맷 되지 않았는지 중요 합니다. 사용자의 입력이 유효한 지 확인 하려면 ASP.NET에서는 단일 입력된 컨트롤의 값의 유효성을 검사 하는 데 사용 될 하도록 설계 된 다섯 개의 기본 제공 유효성 검사 컨트롤을 제공 합니다.

- [RequiredFieldValidator](https://msdn.microsoft.com/library/5hbw267h(VS.80).aspx) 는 값이 제공 되었는지를 확인 합니다.
- [CompareValidator](https://msdn.microsoft.com/library/db330ayw(VS.80).aspx) 다른 웹 컨트롤 값 또는 상수 값에 대 한 값을 확인 하거나 값의 형식이 지정된 된 데이터 형식에 대 한 법적
- [RangeValidator](https://msdn.microsoft.com/library/f70d09xt.aspx) 값의 범위 내에서 값을 확인 합니다.
- [RegularExpressionValidator](https://msdn.microsoft.com/library/eahwtc9e.aspx) 에 대 한 값의 유효성을 검사 한 [정규식](http://en.wikipedia.org/wiki/Regular_expression)
- [CustomValidator](https://msdn.microsoft.com/library/9eee01cx(VS.80).aspx) 를 기준으로 사용자 지정, 사용자 정의 메서드

이러한 다섯 개의 컨트롤에 대 한 자세한 내용은 체크 아웃 된 [유효성 검사 컨트롤 섹션](https://quickstarts.asp.net/quickstartv20/aspnet/doc/ctrlref/validation/default.aspx) 의 [ASP.NET 빠른 시작 자습서](https://asp.net/QuickStart/aspnet/)합니다.

이 자습서에서는를 사용 해야 DetailsView와 GridView의 RequiredFieldValidator `ProductName` TemplateFields 및 DetailsView의에서 RequiredFieldValidator `UnitPrice` TemplateField 합니다. CompareValidator 두 컨트롤에 추가 해야 또한 `UnitPrice` TemplateFields 하도록 입력 한 price의 값이 0이 고 올바른 통화 형식으로 표시 됩니다.

> [!NOTE]
> ASP.NET 동안 1.x에 이러한 동일한 5 개의 유효성 검사 컨트롤, ASP.NET 2.0이 다양 한 기능이 향상을 추가, Internet Explorer 이외의 브라우저와 파티션 유효성 검사 컨트롤에 페이지에는 기능에 대 한 지원 클라이언트 쪽 스크립트 되 고 두 개의 주 유효성 검사 그룹입니다. 2.0의 새로운 유효성 검사 제어 기능에 대 한 자세한 내용은 참조 [ASP.NET 2.0에서 유효성 검사 컨트롤 나누어서](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)합니다.


필요한 유효성 검사 컨트롤을 추가 하 여 시작 하겠습니다는 `EditItemTemplate` GridView의 TemplateFields에서 s입니다. 이를 위해 템플릿 편집 인터페이스를 불러오는 GridView의 스마트 태그에서 템플릿 편집 링크를 클릭 합니다. 여기에서 드롭 다운 목록에서 편집할 템플릿을 선택할 수 있습니다. 원하는 편집 인터페이스를 확장할 수 있으므로 유효성 검사 컨트롤을 추가 해야는 `ProductName` 및 `UnitPrice`의 `EditItemTemplate` s입니다.


[![ProductName 및 단가 EditItemTemplates을 확장 해야](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image11.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image10.png)

**그림 4**: 필요에 맞게 확장 된 `ProductName` 및 `UnitPrice`의 `EditItemTemplate` s ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image12.png))


에 `ProductName` `EditItemTemplate`, TextBox 후 배치는 RequiredFieldValidator 템플릿 편집 인터페이스에 도구 상자에서 끌어 추가 합니다.


[![RequiredFieldValidator ProductName EditItemTemplate에 추가](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image14.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image13.png)

**그림 5**:에 RequiredFieldValidator 추가 `ProductName` `EditItemTemplate` ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image15.png))


모든 유효성 검사 컨트롤 단일 ASP.NET 웹 컨트롤의 입력을 확인 하 여 작동 합니다. 따라서 방금 추가한 RequiredFieldValidator에 텍스트 상자에 대해 유효성을 검사 해야 나타내려면 필요는 `EditItemTemplate`; 유효성 검사 컨트롤을 설정 하 여 이렇게 [ControlToValidate 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.controltovalidate(VS.80).aspx) 에 `ID` 적절 한 웹 컨트롤입니다. 텍스트 상자는 현재 대신 흐릿한에 `ID` 의 `TextBox1`, 하지만 더 적절 한 값으로 변경해 보겠습니다. 서식 파일에 텍스트 상자를 클릭 한 다음 속성 창에서 변경 된 `ID` 에서 `TextBox1` 를 `EditProductName`합니다.


[![텍스트 상자의 ID EditProductName를 변경](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image17.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image16.png)

**그림 6**: 텍스트 상자의 변경 `ID` 를 `EditProductName` ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image18.png))


다음으로 RequiredFieldValidator 설정 `ControlToValidate` 속성을 `EditProductName`합니다. 마지막으로 설정 된 [ErrorMessage 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.errormessage(VS.80).aspx) "제품의 이름을 제공 해야 합니다"를 및 [Text 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.text(VS.80).aspx) 를 "\*"입니다. `Text` 속성 값을 제공 하는 경우는 유효성 검사에 실패 하면 유효성 검사 컨트롤에 의해 표시 되는 텍스트입니다. `ErrorMessage` 는 필수 사항인 속성 값은 경우 ValidationSummary 컨트롤이 사용는 `Text` 속성 값이 생략 되는 `ErrorMessage` 속성 값이 잘못 된 입력의 유효성 검사 컨트롤에서 표시 되는 텍스트입니다.

RequiredFieldValidator의이 세 가지 속성을 설정한 후 화면 그림 7 비슷해야 합니다.


[![RequiredFieldValidator의 ControlToValidate, ErrorMessage, 및 텍스트 속성 설정](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image20.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image19.png)

**그림 7**: RequiredFieldValidator의 설정 `ControlToValidate`, `ErrorMessage`, 및 `Text` 속성 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image21.png))


에 추가 RequiredFieldValidator와는 `ProductName` `EditItemTemplate`남아 필요한 유효성 검사를 추가할 인지 모든는 `UnitPrice` `EditItemTemplate`합니다. म 결정 하는,이 페이지에 대 한 이후는 `UnitPrice` 는 RequiredFieldValidator 추가할 필요 하지 않습니다는 경우에 선택적 레코드를 편집 합니다. 하지만 이때 되도록 CompareValidator를 추가 해야는 `UnitPrice`제공 된 경우, 통화로 형식이 올바르게 고 0 보다 크거나 합니다.

CompareValidator를 추가 하기 전에 `UnitPrice` `EditItemTemplate`에서 TextBox 웹 컨트롤의 ID를 먼저 변경 해보겠습니다 `TextBox2` 를 `EditUnitPrice`합니다. 이 변경 후 CompareValidator, 추가 설정 해당 `ControlToValidate` 속성을 `EditUnitPrice`, 해당 `ErrorMessage` "가격 보다 크거나 0 이어야 하며 통화 기호를 포함할 수 없습니다", 속성 및 해당 `Text` 속성을 "\*".

해당는 `UnitPrice` 값 해야 0 보다 크거나, CompareValidator의 설정 [연산자 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.operator(VS.80).aspx) 를 `GreaterThanEqual`, 해당 [ValueToCompare 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.valuetocompare(VS.80).aspx) "0"과 해당 [ Type 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basecomparevalidator.type.aspx) 를 `Currency`합니다. 선언적 구문에서는 다음의 `UnitPrice` TemplateField의 `EditItemTemplate` 이러한 변경이 이루어진 후:

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample3.aspx)]

다음과 같이 변경한 후 브라우저에서 페이지를 엽니다. 이름을 생략 하거나 제품을 편집할 때 유효 하지 않은 가격 값을 입력 하려고 하면 텍스트 상자 옆에 별표가 나타납니다. 그림 8 에서처럼 $19.95 같은 통화 기호를 포함 하는 가격 값을 잘못 된 간주 됩니다. CompareValidator의 `Currency` `Type` 자릿수 구분 기호 (예: 쉼표 또는 마침표 문화권 설정에 따라) 선행 더하기 또는 빼기 기호를 허용 하지만 않습니다 *하지* 통화 기호를 허용 합니다. 이 동작은 현재 편집 인터페이스를 렌더링 하는 대로 사용자 perplex 수는 `UnitPrice` 통화 형식을 사용 하 여 합니다.

> [!NOTE]
> 이전에 설명한 대로 *삽입, 업데이트 및 삭제와 관련 된 이벤트의* BoundField의 설정 하 여 자습서 `DataFormatString` 속성을 `{0:c}` 통화로 서식을 지정 하려면. 또한 설정 하는 이유는 `ApplyFormatInEditMode` 속성을 true로 인해 GridView의 편집 인터페이스의 서식을 지정 하려면는 `UnitPrice` 통화로 합니다. Visual Studio 기록한이 설정 및 텍스트 상자의 형식를 TemplateField로는 BoundField로 변환할 때 `Text` databinding 구문을 사용 하 여 통화로 속성 `<%# Bind("UnitPrice", "{0:c}") %>`합니다.


[![잘못 된 입력이 포함 된 텍스트 상자 옆에 별표가 나타납니다.](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image23.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image22.png)

**그림 8**: An 별표 표시 하려면 "다음" 잘못 된 입력이 포함 된 텍스트 상자 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image24.png))


동일 하 게 유효성 검사 동작 하는 동안-는 사용자는 허용 되지 않는 레코드를 편집할 때 통화 기호를 수동으로 제거 해야 합니다. 이 해결 하려면 세 가지 옵션이 있습니다.

1. 구성에서 `EditItemTemplate` 있도록는 `UnitPrice` 통화로 값의 서식을 지정 하지 않습니다.
2. 사용자는 CompareValidator를 제거 하 고 적절 한 형식의 통화 값에 대 한 제대로 확인 하는 RegularExpressionValidator로 바꿔 통화 기호를 허용 합니다. 여기에서 문제를 통화 값의 유효성을 검사 하는 정규식 서식이 다시 적용 된다는 점입니다 및 culture 설정을 통합 하 려 하는 경우 코드를 작성 해야 합니다.
3. 유효성 검사 컨트롤을 모두 제거 하 고 GridView의에서 서버 쪽 유효성 검사 논리에 의존 `RowUpdating` 이벤트 처리기입니다.

이 연습에 대 한 #1 옵션으로 해 보겠습니다. 현재는 `UnitPrice` 에 텍스트 상자에 대 한 데이터 바인딩 식으로 인해 통화로 형식이 고 `EditItemTemplate`: `<%# Bind("UnitPrice", "{0:c}") %>`합니다. 하도록 바인딩 문을 변경 `Bind("UnitPrice", "{0:n2}")`, 전체 자릿수 두 자리 숫자로 결과 형식을 지정 합니다. 선언적 구문 또는에서 데이터 바인딩 편집 링크를 클릭 하 여 수행할 수 있습니다는 `EditUnitPrice` 텍스트 상자에는 `UnitPrice` TemplateField의 `EditItemTemplate` (그림 9 및 10 참조).


[![TextBox의 데이터 바인딩 편집 링크를 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image26.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image25.png)

**그림 9**: 텍스트 상자의 데이터 바인딩 편집 링크를 클릭 하세요 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image27.png))


[![Bind 문에서 형식 지정자를 지정 합니다.](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image29.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image28.png)

**그림 10**: 지정에 형식 지정자는 `Bind` 문 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image30.png))


이러한 변경으로 인해 편집 인터페이스에 형식이 지정 된 가격 그룹 구분 기호로 쉼표와 소수 구분 기호로 마침표를 포함 하지만 통화 기호 생략 합니다.

> [!NOTE]
> `UnitPrice` `EditItemTemplate` 하지 못한다면 문제가 발생할으로 게시 및 시작 하 여 시작 하는 업데이트 논리를 허용 하는 RequiredFieldValidator 포함 되지 않습니다. 그러나는 `RowUpdating` 에서 복사를 통해 이벤트 처리기는 *삽입, 업데이트 및 삭제와 관련 된 이벤트를 검사 하* 자습서 포함 되도록 하는 프로그래밍 방식 검사는 `UnitPrice` 제공 됩니다. 이 논리를 제거에 두고 자유롭게-되었거나에 RequiredFieldValidator 추가 `UnitPrice` `EditItemTemplate`합니다.


## <a name="step-4-summarizing-data-entry-problems"></a>4 단계: 데이터 입력 문제 요약

ASP.NET 5 개의 유효성 검사 컨트롤 외에도 포함 되어는 [ValidationSummary 컨트롤](https://msdn.microsoft.com/library/f9h59855(VS.80).aspx)를 표시 하는 `ErrorMessage` 잘못 된 데이터를 검색 하는 이러한 유효성 검사 컨트롤의 s입니다. 웹 페이지에서 또는 모달, 클라이언트 쪽 messagebox를 통해 텍스트로이 요약 데이터를 표시할 수 있습니다. 유효성 검사 문제를 요약 하는 클라이언트 쪽 messagebox를 포함 하려면이 자습서를 향상 시킬 보겠습니다.

이를 위해 디자이너 도구 상자에서 ValidationSummary 컨트롤을 끕니다. 이후만 messagebox로의 요약을 표시 하도록 구성 하 여 유효성 검사 컨트롤의 위치 실제로 문제가 되지 않습니다. 설정 된 컨트롤을 추가한 후 해당 [ShowSummary 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showsummary(VS.80).aspx) 를 `False` 및 해당 [ShowMessageBox 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showmessagebox(VS.80).aspx) 를 `True`합니다. 이 추가 된 유효성 검사 오류는 클라이언트 쪽 messagebox에 요약 되어 있습니다.


[![유효성 검사 오류는 클라이언트 쪽 Messagebox에 요약 되어 있습니다.](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image32.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image31.png)

**그림 11**: The 유효성 검사 오류는 클라이언트 쪽 Messagebox에 요약 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image33.png))


## <a name="step-5-adding-the-validation-controls-to-the-detailsviewsinsertitemtemplate"></a>5 단계: DetailsView의에 유효성 검사 컨트롤 추가`InsertItemTemplate`

모든 작업을이 자습서에 대해 남아 DetailsView의 삽입 인터페이스에 유효성 검사 컨트롤을 추가 하는 것입니다. DetailsView의 서식 파일에 유효성 검사 컨트롤을 추가 하는 프로세스는 3 단계;에서 검사와 동일 따라서이 단계에서는 작업 보기 합니다 했습니다. GridView의와 동일한 방식으로 `EditItemTemplate` s, 확인해 이름을 바꿀 수는 `ID` 흐릿한는에서 입력란의 s `TextBox1` 및 `TextBox2` 를 `InsertProductName` 및 `InsertUnitPrice`합니다.

에 RequiredFieldValidator 추가 `ProductName` `InsertItemTemplate`합니다. 설정의 `ControlToValidate` 에 `ID` 템플릿에서 입력란의 해당 `Text` 속성을 "\*" 및 해당 `ErrorMessage` 속성을 "제품의 이름을 제공 해야 합니다"입니다.

이후는 `UnitPrice` 은에 RequiredFieldValidator 추가 새 레코드를 추가할 때이 페이지에 대 한 필요한는 `UnitPrice` `InsertItemTemplate`설정 해당 `ControlToValidate`, `Text`, 및 `ErrorMessage` 속성 적절 하 게 합니다. 마지막으로 추가 하려면 CompareValidator는 `UnitPrice` `InsertItemTemplate` 도 구성 해당 `ControlToValidate`, `Text`, `ErrorMessage`, `Type`, `Operator`, 및 `ValueToCompare` 는 와마찬가지로속성`UnitPrice`의 GridView의에서 CompareValidator `EditItemTemplate`합니다.

이러한 유효성 검사 컨트롤을 추가한 후 새 제품 경우 해당 가격은 음수 또는 해당 이름을 제공 하지 않은 경우 시스템에 추가 하거나 불법으로 형식이 지정 될 수 없습니다.


[![DetailsView의 삽입 인터페이스에 추가 된 유효성 검사 논리](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image35.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image34.png)

**그림 12**: 유효성 검사 논리가 DetailsView의 삽입 인터페이스에 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image36.png))


## <a name="step-6-partitioning-the-validation-controls-into-validation-groups"></a>6 단계: 유효성 검사 컨트롤을 유효성 검사 그룹으로 분

가격 페이지 유효성 검사 컨트롤의 논리적으로 서로 다른 두 집합으로 이루어져: GridView에 해당 하는 인터페이스의 편집 및 인터페이스 삽입의 DetailsView에 해당 하는 것입니다. 포스트백이 발생할 때 기본적으로 *모든* 페이지에서 유효성 검사 컨트롤 확인 됩니다. 그러나 레코드를 편집할 때 유효성을 검사할 DetailsView의 삽입 인터페이스의 유효성 검사 컨트롤 않도록 합니다. 그림 13 사용자가 전혀 값이 포함 된 제품을 편집 하는 경우 현재 우리의 딜레마는, 클릭 하면 업데이트 삽입 인터페이스의 이름 및 가격 값은 공백 때문에 유효성 검사 오류가 발생 합니다.


[![삽입 인터페이스의 유효성 검사 컨트롤의 공격에 사용 하면 제품 업데이트](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image38.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image37.png)

**그림 13**: 삽입 인터페이스의 유효성 검사 컨트롤의 공격에 사용 하면 제품 업데이트 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image39.png))


ASP.NET 2.0에서 유효성 검사 컨트롤을 통해 유효성 검사 그룹으로 분할 될 수 자신의 `ValidationGroup` 속성입니다. 그룹의 유효성 검사 컨트롤의 집합을 연결 하려면 간단히 설정의 `ValidationGroup` 속성을 동일한 값입니다. 이 자습서에 대 한 설정에서 `ValidationGroup` 에 GridView의 TemplateFields에서 유효성 검사 컨트롤의 속성 `EditValidationControls` 및 `ValidationGroup` 를 DetailsView의 TemplateFields의 속성 `InsertValidationControls`합니다. 이러한 변경 내용은 선언적 태그에 직접 수행 하거나 디자이너를 사용 하는 경우 속성 창을 통해 템플릿 인터페이스를 편집 합니다.

뿐만 아니라 유효성 검사 컨트롤, 단추 및 단추와 관련 된 컨트롤 ASP.NET 2.0에 포함 된 `ValidationGroup` 속성입니다. 유효성 검사 그룹의 유효성 검사기가 유효성을 확인만 때 포스트백으로 인해 발생 같은 단추 `ValidationGroup` 속성을 설정 합니다. 트리거할 DetailsView의 삽입 단추에 대 한 예를 들어 순서로 `InsertValidationControls` CommandField의 공간을 유효성 검사 그룹 `ValidationGroup` 속성을 `InsertValidationControls` (그림 14 참조). 또한 GridView의 설정 CommandField의 `ValidationGroup` 속성을 `EditValidationControls`합니다.


[![DetailsView 집합의 InsertValidationControls CommandField의 ValidationGroup 속성](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image41.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image40.png)

**그림 14**: DetailsView의 설정 CommandField의 `ValidationGroup` 속성을 `InsertValidationControls` ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image42.png))


이러한 변경 된 후 DetailsView 및 GridView의 TemplateFields와 CommandFields 다음과 비슷하게 표시 됩니다.

DetailsView의 TemplateFields 및 CommandField

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample4.aspx)]

GridView의 CommandField 및 TemplateFields

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample5.aspx)]

이 시점에서 편집 관련 유효성 검사 컨트롤 실행 GridView의 [업데이트] 단추를 클릭할 때에 및 삽입 전용 유효성 검사 컨트롤 화재 DetailsView의 삽입 단추를 클릭 하 여 그림 13 강조 표시 하는 문제를 해결 하는 경우에 합니다. 그러나 이러한 변경으로 인해 ValidationSummary 제어권 더 이상 표시 잘못 된 데이터를 입력할 때. ValidationSummary 컨트롤에도 포함 되어는 `ValidationGroup` 속성 및 해당 유효성 검사 그룹에서 해당 유효성 검사 컨트롤에 대 한 요약 정보 표시만 합니다. 따라서 두 개의 유효성 검사 컨트롤에 대 한이 페이지에 있는 해야는 `InsertValidationControls` 유효성 검사 그룹 되 고 다른 하나 `EditValidationControls`합니다.

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample6.aspx)]

이 추가 된 사용이 자습서를 완료!

## <a name="summary"></a>요약

BoundFields 삽입 및 편집 인터페이스 둘 다 제공 수, 인터페이스를 사용자 지정할 수 없습니다. 일반적으로, 편집 및 사용자를 올바른 형식에 필요한 입력에 들어가는지 확인에 대 한 인터페이스를 삽입에 유효성 검사 컨트롤을 추가 하려고 합니다. 이를 위해 우리는 BoundFields TemplateFields로 변환 하 고 적절 한 템플릿에 유효성 검사 컨트롤을 추가 해야 합니다. 이 자습서의 예제 확장는 *삽입, 업데이트 및 삭제와 관련 된 이벤트를 검사* 인터페이스 및 GridView의 자습서에서는 두 DetailsView에 유효성 검사 컨트롤 추가 삽입의 인터페이스를 편집 합니다. 또한 ValidationSummary 컨트롤을 사용 하 여 유효성 검사 요약 정보를 표시 하는 방법과 페이지에 유효성 검사 컨트롤 고유한 유효성 검사 그룹으로 분리 하는 방법에 살펴보았습니다.

이 자습서에서 살펴본 것 처럼 TemplateFields 편집 및 삽입 인터페이스 유효성 검사 컨트롤을 포함 하도록 확장할 수를 허용 합니다. TemplateFields 수도 포함 하도록 확장할 수 추가 입력된 웹 컨트롤에 더 적합 한 웹 컨트롤을 교체 하는 입력란을 사용 하도록 설정 합니다. 다음이 자습서에서 외래 키를 편집 하는 경우에 적합 한 데이터 바인딩 DropDownList 컨트롤과 TextBox 컨트롤을 대체 하는 방법을 보겠습니다 (같은 `CategoryID` 또는 `SupplierID` 에 `Products` 테이블).

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Liz Shulok 및 Zack jones 이면 특정 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md)
> [다음](customizing-the-data-modification-interface-vb.md)
