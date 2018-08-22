---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs
title: 편집에 유효성 검사 컨트롤 추가 및 삽입 인터페이스 (C#) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 EditItemTemplate 및 데이터 웹 컨트롤을 먼저 더에 유효성 검사 컨트롤을 추가 하려면 얼마나 쉬운지 살펴보겠습니다...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 2086cb1a-ab78-49ae-9c0b-03891c69776a
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs
msc.type: authoredcontent
ms.openlocfilehash: 4990ce2c15465873ef08aeb697780d98a186b3c6
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41826866"
---
<a name="adding-validation-controls-to-the-editing-and-inserting-interfaces-c"></a>편집에 유효성 검사 컨트롤 추가 및 삽입 인터페이스 (C#)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_19_CS.exe) 또는 [PDF 다운로드](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/datatutorial19cs1.pdf)

> 이 자습서를 EditItemTemplate 데이터 웹 컨트롤을 먼저를 간단 명료 사용자 인터페이스를 제공 유효성 검사 컨트롤을 추가 하려면 얼마나 쉬운지 알아봅니다.


## <a name="introduction"></a>소개

세 개의 자습서가 모든 구성 BoundFields 및 CheckBoxFields (필드 형식 데이터 원본에 GridView 또는 DetailsView를 바인딩할 때 Visual Studio에서 자동으로 추가 된 있습니다 지난 살펴보았습니다 예제에서 GridView 및 DetailsView 컨트롤 컨트롤에 스마트 태그를 통해). GridView 또는 DetailsView의 행을 편집할 때 텍스트 상자에 읽기 전용 되지 않는 이러한 BoundFields 변환 됩니다 최종 사용자는 기존 데이터를 수정할 수 있습니다. 마찬가지로, 경우 새로 삽입 기록 해당 BoundFields DetailsView 컨트롤에 있는 `InsertVisible` 속성이 `true` (기본값) 사용자는 새 레코드의 필드 값을 제공할 수 있습니다 빈 입력란으로 렌더링 됩니다. 마찬가지로, 표준, 읽기 전용 인터페이스에서 비활성화 되는 CheckBoxFields 편집 및 삽입 인터페이스에 설정 된 확인란으로 변환 됩니다.

편집 및 삽입 인터페이스 BoundField 및 CheckBoxField 기본 도움이 될 수 있지만, 인터페이스에 모든 종류를의 유효성 검사는 없습니다. 사용자가 데이터 항목 실수-생략 같은 경우는 `ProductName` 필드에 잘못 된 값을 입력 또는 `UnitsInStock` (예:-50) 예외에서 발생 하면 중첩 된 응용 프로그램 아키텍처의 합니다. 에 설명 된 대로이 예외가 정상적으로 처리할 수 있지만 [이전 자습서](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md), 편집 또는 삽입 사용자 인터페이스는 사용자가 이러한 잘못 된 데이터에를 입력 하지 못하게 하려면 유효성 검사 컨트롤 포함 이상적으로 먼저 배치 합니다.

사용자 지정된 편집 또는 삽입 인터페이스를 제공 하기 위해 BoundField 또는 CheckBoxField templatefield로 대체 해야 합니다. TemplateFields 토론의 주제 였던에 [GridView 컨트롤에서 TemplateFields 사용 하 여](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md) 하 고 [DetailsView 컨트롤에서 TemplateFields 사용 하 여](../custom-formatting/using-templatefields-in-the-detailsview-control-cs.md) 자습서, 여러 구성 될 수 있습니다 템플릿 정의 다른 행 상태에 대 한 인터페이스를 분리 합니다. TemplateField `ItemTemplate` 사용 되는 읽기 전용 필드 또는, DetailsView 또는 GridView 컨트롤의 행을 렌더링할 때 반면를 `EditItemTemplate` 및 `InsertItemTemplate` 편집 모드를 각각 삽입에 사용 하 여 인터페이스를 나타냅니다.

이 자습서에서는 살펴보겠습니다 TemplateField의 유효성 검사 컨트롤에 추가할 얼마나 쉬운지 `EditItemTemplate` 고 `InsertItemTemplate` 간단 명료 사용자 인터페이스를 제공 합니다. 이 자습서에서 만든 예제를 사용 하는 예는 [삽입, 업데이트 및 삭제와 관련 된 이벤트 검사](examining-the-events-associated-with-inserting-updating-and-deleting-cs.md) 자습서 및 보완 편집 및 삽입 인터페이스 적절 한 유효성 검사를 포함 합니다.

## <a name="step-1-replicating-the-example-fromexamining-the-events-associated-with-inserting-updating-and-deletingexamining-the-events-associated-with-inserting-updating-and-deleting-csmd"></a>1 단계: 복제 예제의[삽입, 업데이트 및 삭제와 관련 된 이벤트 검사](examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)

에 [삽입, 업데이트 및 삭제와 관련 된 이벤트 검사](examining-the-events-associated-with-inserting-updating-and-deleting-cs.md) 자습서 이름과 편집 가능한 GridView의 제품 가격을 나열 하는 페이지를 만들었습니다. 페이지는 DetailsView를 포함 하는 또한입니다 `DefaultMode` 속성이로 설정 된 `Insert`, 삽입 모드에 있으므로 항상 렌더링 합니다. 이 DetailsView에서 사용자 수는 신제품에 대 한 이름 및 가격을 입력, 삽입을 클릭 한 시스템에 추가 하면 (그림 1 참조).


[![새 제품을 추가 하 여 기존 관계를 편집 하면 앞의 예제](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image2.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image1.png)

**그림 1**:은 이전 예제에서는 허용 사용자가 새 제품 추가 및 편집 기존 ([큰 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image3.png))


이 자습서에 대 한 우리의 목표는 DetailsView 및 GridView 유효성 검사 컨트롤 수 있도록 확장입니다. 특히이 유효성 검사 논리는:

- 삽입 하거나 제품을 편집할 때에 이름을 제공 해야 합니다.
- 레코드를 삽입 하는 경우 가격을 제공 해야 합니다. 에서는 가격을 계속 해야 하지만 GridView의에 프로그래밍 방식으로 논리를 사용 하는 레코드를 편집할 때 `RowUpdating` 이미 이전 자습서에서 이벤트 처리기
- 가격에 대 한 입력 한 값을 유효한 통화 형식 인지 확인

먼저에서 예제를 복제 해야 유효성 검사를 포함 하도록 앞의 예제를 확대 살펴보면 전에 합니다 `DataModificationEvents.aspx` 이 자습서에서는 페이지에 페이지 `UIValidation.aspx`합니다. 모두 복사 해야이 작업을 수행 하는 `DataModificationEvents.aspx` 페이지의 선언적 태그와 해당 소스 코드입니다. 먼저 다음 단계를 수행 하 여 선언적 태그도 복사 합니다.

1. 열기는 `DataModificationEvents.aspx` Visual Studio에서 페이지
2. 페이지의 선언적 태그 (페이지의 맨 아래에 있는 원본 단추 클릭)로 이동
3. 내에서 텍스트를 복사 합니다 `<asp:Content>` 및 `</asp:Content>` 그림 2에 표시 된 것된으로 태그 (44-3 줄).


[![텍스트 내에 복사 합니다 &lt;asp: Content&gt; 컨트롤](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image5.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image4.png)

**그림 2**: 텍스트 내에 복사 합니다 `<asp:Content>` 컨트롤 ([클릭 하 여 큰 이미지 보기](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image6.png))


1. 열기는 `UIValidation.aspx` 페이지
2. 페이지의 선언적 태그로 이동
3. 내에서 텍스트를 붙여 넣습니다는 `<asp:Content>` 제어 합니다.

소스 코드를 복사 하려면 엽니다는 `DataModificationEvents.aspx.cs` 페이지 및 텍스트만 복사 *내* 는 `EditInsertDelete_DataModificationEvents` 클래스. 세 개의 이벤트 처리기를 복사 (`Page_Load`, `GridView1_RowUpdating`, 및 `ObjectDataSource1_Inserting`), 않지만 **하지** 복사 클래스 선언 또는 `using` 문입니다. 복사한 텍스트를 붙여 넣습니다 *내* 는 `EditInsertDelete_UIValidation` 클래스 `UIValidation.aspx.cs`합니다.

콘텐츠 및 코드를 통해 이동 하 고 나면 `DataModificationEvents.aspx` 에 `UIValidation.aspx`, 브라우저에서 진행 상황을 테스트 하려면 잠시 합니다. 동일한 출력 및 이러한 두 페이지의 각 동일한 기능이 표시 됩니다 (스크린 샷 그림 1을 다시 참조 `DataModificationEvents.aspx` 작업에서).

## <a name="step-2-converting-the-boundfields-into-templatefields"></a>2 단계: TemplateFields는 BoundFields 변환

편집 및 삽입 인터페이스에 유효성 검사 컨트롤을 추가할 GridView 및 DetailsView 컨트롤에서 사용 하는 BoundFields TemplateFields 변환할 필요 합니다. 이 위해 GridView 및 DetailsView의 스마트 태그에 열 편집 및 필드 편집 링크를 각각 클릭 합니다. 여기서는 BoundFields의 각를 선택 하 고 "이이 필드를 TemplateField로 변환 하 는" 링크를 클릭 합니다.


[![TemplateFields DetailsView의 및 GridView의 BoundFields의 각 변환](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image8.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image7.png)

**그림 3**: 각각의 GridView와 DetailsView의 BoundFields에 TemplateFields 변환 ([큰 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image9.png))


필드 대화 상자를 통해 templatefield로 변환 하는 BoundField 자체 BoundField로 동일한 읽기 전용, 편집 및 삽입 인터페이스를 보여 주는 templatefield로 생성 합니다. 다음 태그에 대 한 선언적 구문을 보여 줍니다는 `ProductName` 필드를 TemplateField로 변환 된 후 DetailsView에:

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/samples/sample1.aspx)]

이 TemplateField가 자동으로 생성 하는 세 가지 템플릿을 참고 `ItemTemplate`, `EditItemTemplate`, 및 `InsertItemTemplate`합니다. `ItemTemplate` 단일 데이터 필드 값이 표시 됩니다 (`ProductName`) Label 웹 컨트롤을 사용 하는 동안 합니다 `EditItemTemplate` 및 `InsertItemTemplate` 데이터 필드 값의 텍스트 상자를 사용 하 여 데이터 필드를 연결 하는 텍스트 웹 컨트롤에 있는 `Text` 양방향 데이터 바인딩을 사용 하는 속성입니다. 이 페이지에 삽입 하기 위한 DetailsView 사용만 제거할 수 있습니다 합니다 `ItemTemplate` 및 `EditItemTemplate` 두 TemplateFields에서 그대로 하더라도 피해는 없지만 합니다.

GridView DetailsView의 기능을 삽입, 변환 GridView의 기본 제공을 지원 하지 않으므로 `ProductName` 필드를 TemplateField로만 결과 `ItemTemplate` 고 `EditItemTemplate`:

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/samples/sample2.aspx)]

"이이 필드를 TemplateField로 변환"을 클릭 하면 Visual Studio는 해당 템플릿이 변환된 BoundField의 사용자 인터페이스를 모방 templatefield로 만들었습니다. 브라우저를 통해이 페이지를 방문 하 여이 확인할 수 있습니다. BoundFields 대신 사용 된 모양 및 동작을 TemplateFields의 동일 환경에는 찾을 수 있습니다.

> [!NOTE]
> 필요에 따라 서식 파일의 편집 인터페이스 사용자 지정 해도 됩니다. 예를 들어, 하려는 텍스트 상자에는 `UnitPrice` 보다 작은 텍스트 상자로 렌더링 TemplateFields는 `ProductName` 텍스트 상자에 붙여넣습니다. 이렇게 하려면 텍스트 상자의 설정할 수 있습니다 `Columns` 속성을 적절 한 값을 바꾸거나를 통해 절대 너비는 `Width` 속성입니다. 다음 자습서에서 완전히 대체 데이터 항목 웹 컨트롤을 사용 하 여 텍스트를 대체 하 여 편집 인터페이스를 사용자 지정 하는 방법을 살펴보겠습니다.


## <a name="step-3-adding-the-validation-controls-to-the-gridviewsedititemtemplate-s"></a>3 단계: GridView의 유효성 검사 컨트롤 추가`EditItemTemplate` s

데이터 입력 폼을 생성할 때는 사용자가 모든 필수 필드를 입력 하 고 모든 제공 된 입력을 법률, 올바르게 형식이 지정 된 값에는 중요 합니다. 사용자의 입력이 올바른지 확인 하려면 ASP.NET 입력된 컨트롤을 단일 값의 유효성을 검사 하는 데 사용할 설계 된 5 개의 기본 제공 유효성 검사 컨트롤을 제공 합니다.

- [RequiredFieldValidator](https://msdn.microsoft.com/library/5hbw267h(VS.80).aspx) 는 값이 제공 되었는지를 확인 합니다.
- [CompareValidator](https://msdn.microsoft.com/library/db330ayw(VS.80).aspx) 를 기준으로 다른 웹 컨트롤 값 또는 상수 값 또는 값의 형식이 지정된 된 데이터 형식에 대 한 법적 인지 확인
- [RangeValidator](https://msdn.microsoft.com/library/f70d09xt.aspx) 값의 범위 내에서 값을 확인 합니다.
- [RegularExpressionValidator](https://msdn.microsoft.com/library/eahwtc9e.aspx) 에 대 한 값의 유효성을 검사 한 [정규식](http://en.wikipedia.org/wiki/Regular_expression)
- [CustomValidator](https://msdn.microsoft.com/library/9eee01cx(VS.80).aspx) 를 기준으로 사용자 지정, 사용자 정의 메서드

이러한 다섯 개의 컨트롤에 대 한 자세한 내용은 체크 아웃 합니다 [유효성 검사 컨트롤 섹션](https://quickstarts.asp.net/quickstartv20/aspnet/doc/ctrlref/validation/default.aspx) 의 합니다 [ASP.NET 퀵 스타트 자습서](https://asp.net/QuickStart/aspnet/)합니다.

이 자습서에서는 사용 해야 DetailsView와 GridView의 RequiredFieldValidator `ProductName` TemplateFields 및 DetailsView의에서 RequiredFieldValidator `UnitPrice` TemplateField 합니다. CompareValidator 두 컨트롤에 추가 해야 또한 `UnitPrice` TemplateFields는 입력 한 가격 값을 0 보다 크거나 있고 유효한 통화 형식으로 표시 됩니다.

> [!NOTE]
> 반면 ASP.NET 1.x가 이러한 동일한 5 유효성 검사 컨트롤, ASP.NET 2.0에는 수많은 개선 사항이 추가 되었습니다, Internet Explorer 이외의 브라우저 및 파티션 유효성 검사 컨트롤에는 페이지 수에 대 한 지원 클라이언트 쪽 스크립트 되 고 두 개의 주 유효성 검사 그룹입니다. 2.0의 새로운 유효성 검사 컨트롤 기능에 대 한 자세한 내용은 참조 [ASP.NET 2.0의 유효성 검사 컨트롤 분석](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)합니다.


필요한 유효성 검사 컨트롤을 추가 하 여 시작 해 보겠습니다는 `EditItemTemplate` GridView의 TemplateFields의 합니다. 이렇게 하려면 템플릿 편집 인터페이스를 표시 하려면 GridView의 스마트 태그에서 템플릿 편집 링크를 클릭 합니다. 여기에서 드롭 다운 목록에서 편집할 템플릿을 선택할 수 있습니다. 편집 인터페이스 보강 하고자 하므로 유효성 검사 컨트롤을 추가 해야 합니다 `ProductName` 하 고 `UnitPrice`의 `EditItemTemplate` s입니다.


[![ProductName 및 UnitPrice의 EditItemTemplates 확장 해야](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image11.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image10.png)

**그림 4**: 확장 해야 합니다 `ProductName` 하 고 `UnitPrice`의 `EditItemTemplate` s ([클릭 하 여 큰 이미지 보기](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image12.png))


에 `ProductName` `EditItemTemplate`, 텍스트 상자 후 배치를 RequiredFieldValidator 끌어와 도구 상자에서 템플릿 편집 인터페이스에 추가 합니다.


[![RequiredFieldValidator ProductName EditItemTemplate 추가](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image14.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image13.png)

**그림 5**:를 RequiredFieldValidator를 추가 합니다 `ProductName` `EditItemTemplate` ([클릭 하 여 큰 이미지 보기](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image15.png))


모든 유효성 검사 컨트롤 단일 ASP.NET 웹 컨트롤의 입력 유효성을 검사 하 여 작동 합니다. 방금 추가한 RequiredFieldValidator에서 텍스트 상자에 대 한 유효성을 검사 해야를 지정 해야 하므로 합니다 `EditItemTemplate`; 유효성 검사 컨트롤의 설정 하 여 이렇게 [ControlToValidate 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.controltovalidate(VS.80).aspx) 에 `ID` 적절 한 웹 컨트롤입니다. 텍스트 상자 현재 흐릿한 대신에 `ID` 의 `TextBox1`, 하지만 적절 하 게를 변경해 보겠습니다. 템플릿에서 텍스트 상자를 클릭 한 다음 속성 창에서 변경 된 `ID` 에서 `TextBox1` 에 `EditProductName`입니다.


[![텍스트 상자의 ID EditProductName로 변경](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image17.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image16.png)

**그림 6**: 텍스트 상자의 변경할 `ID` 하 `EditProductName` ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image18.png))


RequiredFieldValidator의 다음으로 설정 `ControlToValidate` 속성을 `EditProductName`입니다. 마지막으로 설정 합니다 [ErrorMessage 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.errormessage(VS.80).aspx) "제품의 이름을 제공 해야 합니다" 및 [Text 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.text(VS.80).aspx) 에 "\*"입니다. `Text` 속성 값을 제공 하는 경우이 유효성 검사에 실패 하는 경우 유효성 검사 컨트롤에 표시 되는 텍스트입니다. `ErrorMessage` 속성 값이 필요한 경우 ValidationSummary 컨트롤에서 사용 됩니다는 `Text` 속성 값을 생략 하면는 `ErrorMessage` 속성 값이 잘못 된 입력의 유효성 검사 컨트롤에서 표시 되는 텍스트입니다.

RequiredFieldValidator의 이러한 세 가지 속성을 설정한 다음 화면은 해야 그림 7과 유사 합니다.


[![RequiredFieldValidator의 ControlToValidate, ErrorMessage을 및 텍스트 속성 설정](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image20.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image19.png)

**그림 7**: RequiredFieldValidator의 설정 `ControlToValidate`하십시오 `ErrorMessage`, 및 `Text` 속성 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image21.png))


추가할 RequiredFieldValidator를 사용 하 여 합니다 `ProductName` `EditItemTemplate`남아 필요한 유효성 검사를 추가 하는 모든 합니다 `UnitPrice` `EditItemTemplate`합니다. 이 페이지를 결정 하므로 `UnitPrice` 옵션은 레코드를 편집, 필요가 RequiredFieldValidator를 추가 합니다. 하지만 되도록 CompareValidator를 추가 해야 그렇게는 `UnitPrice`제공 하는 경우 이며 0 보다 크거나을 통화로 형식이 올바르게 합니다.

CompareValidator를 추가 하기 전에 합니다 `UnitPrice` `EditItemTemplate`에서 텍스트 웹 컨트롤의 ID를 먼저 변경해 보겠습니다 `TextBox2` 에 `EditUnitPrice`합니다. 이렇게 변경한 후 CompareValidator, 추가 설정 해당 `ControlToValidate` 속성을 `EditUnitPrice`, 해당 `ErrorMessage` 속성을 "가격 보다 크거나 0 이어야 합니다 하 고 통화 기호를 포함할 수 없습니다", 고 `Text` 속성 "\*".

나타내는 합니다 `UnitPrice` 값 수를 0 보다 크거나, CompareValidator의 설정 해야 합니다 [연산자 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.operator(VS.80).aspx) 하려면 `GreaterThanEqual`, 해당 [ValueToCompare 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.valuetocompare(VS.80).aspx) "0" 및 해당 [ 형식 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basecomparevalidator.type.aspx) 에 `Currency`입니다. 선언적 구문에서는 다음 합니다 `UnitPrice` TemplateField의 `EditItemTemplate` 이러한 변경이 이루어진 후:

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/samples/sample3.aspx)]

다음과 같이 변경한 후 브라우저에서 페이지를 엽니다. 이름을 생략 하거나 제품을 편집 하는 경우 유효 하지 않은 가격 값을 입력 하려는 경우 텍스트 상자 옆에 있는 별표 표시 됩니다. 그림 8에서 알 수 있듯이, $19.95 같은 통화 기호를 포함 하는 가격 잘못 된 간주 됩니다. CompareValidator의 `Currency` `Type` 자릿수 구분 기호 (예: 쉼표 또는 마침표 문화권 설정에 따라) 및 선행 더하기 또는 빼기 기호를 허용 하지만 않습니다 *하지* 통화 기호를 허용 합니다. 이 동작은 현재 편집 인터페이스를 렌더링 하는 대로 사용자 perplex 수는 `UnitPrice` 통화 형식을 사용 하 여 합니다.

> [!NOTE]
> 회수에 *삽입, 업데이트 및 삭제와 관련 된 이벤트* BoundField의 설정 자습서 `DataFormatString` 속성을 `{0:c}` 통화로 서식을 지정 하기 위해. 설정 또한 합니다 `ApplyFormatInEditMode` 속성을 true로, GridView를 일으키는 편집 인터페이스 형식을 지정 하는 `UnitPrice` 통화로 합니다. Visual Studio 기록한이 설정 및 텍스트의 서식이 지정 된 BoundField를 TemplateField로으로 변환할 때 `Text` 속성이 데이터 바인딩 구문을 사용 하는 통화로 `<%# Bind("UnitPrice", "{0:c}") %>`합니다.


[![잘못 된 입력을 사용 하 여 텍스트 상자 옆에 있는 별표 표시 됩니다.](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image23.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image22.png)

**그림 8**: An 별표 표시 옆에 잘못 된 입력을 사용 하 여 텍스트 상자 ([큰 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image24.png))


으로 유효성 검사 작동 하는 동안-인 사용자가 허용 되지 않는 레코드를 편집 하는 경우 통화 기호를 수동으로 제거 해야 합니다. 이 문제를 해결 하는 세 가지 옵션이 했습니다.

1. 구성 합니다 `EditItemTemplate` 있도록는 `UnitPrice` 통화로 형식이 값입니다.
2. CompareValidator를 제거 하 고 올바르게 형식이 지정 된 통화 값에 대 한 제대로 확인 하는 RegularExpressionValidator로 바꿔 여 통화 기호를 입력 하는 사용자를 허용 합니다. 여기서 문제 통화 값의 유효성을 검사 하는 정규식 깔끔한는 및에 방문 하셔서 문화권 설정을 통합 하는 경우 코드를 작성 해야 합니다.
3. 유효성 검사 컨트롤을 완전히 제거 하 고 GridView의에서 서버 쪽 유효성 검사 논리에 의존 `RowUpdating` 이벤트 처리기입니다.

이 연습에 대 한 옵션 # 1을 사용 하 여 이동 합니다. 현재는 `UnitPrice` 의 텍스트 상자에 대 한 데이터 바인딩 식으로 인해 통화로 형식이 합니다 `EditItemTemplate`: `<%# Bind("UnitPrice", "{0:c}") %>`합니다. 바인딩 문을 변경 `Bind("UnitPrice", "{0:n2}")`, 전체 자릿수 두 자리 숫자로 결과 형식을 지정 합니다. 선언적 구문을 통해 직접 또는에서 데이터 바인딩 편집 링크를 클릭 하 여이 수행할 수 있습니다 합니다 `EditUnitPrice` 텍스트 상자는 `UnitPrice` TemplateField의 `EditItemTemplate` (그림 9 및 10 참조).


[![텍스트 상자의 데이터 바인딩 편집 링크를 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image26.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image25.png)

**그림 9**: 텍스트 상자의 데이터 바인딩 편집 링크를 클릭 합니다 ([큰 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image27.png))


[![바인딩 문에서 형식 지정자를 지정 합니다.](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image29.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image28.png)

**그림 10**:에 형식 지정자를 지정 합니다 `Bind` 문 ([클릭 하 여 큰 이미지 보기](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image30.png))


이 변경으로 편집 인터페이스에 형식이 지정 된 가격 그룹 구분 기호로 쉼표와 마침표는 소수 구분 기호로 포함 되지만 통화 기호를 해제 합니다.

> [!NOTE]
> 합니다 `UnitPrice` `EditItemTemplate` 충돌에 포스트백을 시작 하는 업데이트 논리를 허용 하는 RequiredFieldValidator 포함 되지 않습니다. 그러나 합니다 `RowUpdating` 에서 복사 하는 이벤트 처리기는 *삽입, 업데이트 및 삭제와 관련 된 이벤트 검사* 자습서 포함 되도록 하는 프로그래밍 방식으로 검사는 `UnitPrice` 제공 됩니다. 이 논리를 제거 하려면 그대로에서 자유롭게-되었거나를 RequiredFieldValidator 추가 합니다 `UnitPrice` `EditItemTemplate`.


## <a name="step-4-summarizing-data-entry-problems"></a>4 단계: 데이터 입력 문제 요약

ASP.NET 5 유효성 검사 컨트롤 외에도 포함 합니다 [ValidationSummary 컨트롤](https://msdn.microsoft.com/library/f9h59855(VS.80).aspx), 표시는 `ErrorMessage` 잘못 된 데이터가 검색 되는 유효성 검사 컨트롤의. 웹 페이지 또는 모달, 클라이언트 쪽 messagebox를 통해 텍스트로이 요약 데이터를 표시할 수 있습니다. 모든 유효성 검사 문제를 요약 하는 클라이언트 쪽 messagebox를 포함 하려면이 자습서를 개선해 보겠습니다.

이렇게 하려면 디자이너 도구 상자에서 ValidationSummary 컨트롤을 끕니다. 요약을 messagebox로만 표시 하도록 구성 하려고 하므로 유효성 검사 컨트롤의 위치 실제로 중요 하지 않습니다. 컨트롤을 추가한 후 설정 해당 [ShowSummary 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showsummary(VS.80).aspx) 하 `false` 고 [ShowMessageBox 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showmessagebox(VS.80).aspx) 에 `true`입니다. 이 또한을 사용 하 여 유효성 검사 오류는 클라이언트 쪽 messagebox에 요약 되어 있습니다.


[![유효성 검사 오류는 클라이언트 쪽 Messagebox에 요약 되어 있습니다.](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image32.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image31.png)

**그림 11**: 유효성 검사 오류는 클라이언트 쪽 Messagebox에 요약 되어 있습니다 ([큰 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image33.png))


## <a name="step-5-adding-the-validation-controls-to-the-detailsviewsinsertitemtemplate"></a>5 단계: DetailsView의 유효성 검사 컨트롤 추가`InsertItemTemplate`

이 자습서에 DetailsView의 삽입 인터페이스에 유효성 검사 컨트롤을 추가 합니다. DetailsView의 템플릿에 유효성 검사 컨트롤을 추가 하는 프로세스 단계 3에서 검사는 같습니다. 따라서이 단계에서는 작업을 통해 거침 됩니다 것입니다. GridView의와 마찬가지로 `EditItemTemplate` 개이면 바랍니다 이름을 바꾸려면 합니다 `ID` 은 흐릿한에서 입력란의 `TextBox1` 및 `TextBox2` 를 `InsertProductName` 및 `InsertUnitPrice`합니다.

RequiredFieldValidator를 추가 합니다 `ProductName` `InsertItemTemplate`합니다. 설정 합니다 `ControlToValidate` 에 `ID` 템플릿에서 입력란의 해당 `Text` 속성을 "\*" 고 `ErrorMessage` 속성을 "제품의 이름을 제공 해야 합니다".

있으므로 `UnitPrice` 는를 RequiredFieldValidator 추가 새 레코드를 추가 하는 경우이 페이지에 대 한 필요한를 `UnitPrice` `InsertItemTemplate`설정, 해당 `ControlToValidate`, `Text`, 및 `ErrorMessage` 속성 적절 하 게 합니다. CompareValidator를 마지막으로 추가 합니다 `UnitPrice` `InsertItemTemplate` 구성도 해당 `ControlToValidate`, `Text`, `ErrorMessage`, `Type`, `Operator`, 및 `ValueToCompare` 합니다 를사용하여수행한것처럼속성`UnitPrice`의 gridview의 CompareValidator `EditItemTemplate`합니다.

이러한 유효성 검사 컨트롤을 추가한 후 새 제품을 가격은 음수인 경우 또는 해당 이름이 제공 되지 않은 경우 시스템에 추가 하거나 형식이 잘못 될 수 없습니다.


[![DetailsView의 삽입 인터페이스에 유효성 검사 논리가 추가 되었습니다.](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image35.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image34.png)

**그림 12**: DetailsView의 삽입 인터페이스에 유효성 검사 논리가 추가 되었습니다 ([큰 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image36.png))


## <a name="step-6-partitioning-the-validation-controls-into-validation-groups"></a>6 단계: 유효성 검사 컨트롤을 유효성 검사 그룹으로 분

페이지 유효성 검사 컨트롤의 논리적으로 서로 다른 두 집합의 구성: GridView에 해당 하는 인터페이스의 편집 및 인터페이스 삽입의 DetailsView에 해당 하는 것입니다. 기본적으로 포스트백이 발생할 때 *모든* 유효성 검사 컨트롤의 페이지 확인 됩니다. 그러나 레코드를 편집할 때 원하지 DetailsView의 삽입 인터페이스의 유효성 검사 컨트롤의 유효성을 검사 합니다. 그림 13 사용자가 완벽 하 게 올바른 값을 사용 하 여 제품을 편집 하는 경우 현재이 딜레마를 보여 줍니다, 그리고 클릭 하면 업데이트 삽입 인터페이스에 이름과 가격 값이 비어 있으므로 유효성 검사 오류가 발생 합니다.


[![공격에 삽입 하는 인터페이스의 유효성 검사 컨트롤 제품을 업데이트 하면](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image38.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image37.png)

**그림 13**:의 공격에 삽입 인터페이스의 유효성 검사 컨트롤 제품을 업데이트 하면 ([큰 이미지를 보려면 클릭](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image39.png))


ASP.NET 2.0의 유효성 검사 컨트롤을 통해 유효성 검사 그룹 분할할 수 해당 `ValidationGroup` 속성입니다. 단순히 설정 그룹의 유효성 검사 컨트롤 집합에 연결 하려면 해당 `ValidationGroup` 속성을 동일한 값입니다. 이 자습서에 대 한 설정 합니다 `ValidationGroup` 에 GridView의 TemplateFields에서 유효성 검사 컨트롤의 속성 `EditValidationControls` 및 `ValidationGroup` 속성에는 DetailsView TemplateFields의 `InsertValidationControls`. 이러한 변경 내용을 선언적 태그에서 직접 수행할 수 있습니다 하거나 디자이너를 사용 하는 경우 속성 창을 통해 템플릿 인터페이스를 편집 합니다.

유효성 검사 외에도 컨트롤, 단추 및 ASP.NET 2.0의 컨트롤 단추와 관련 된 포함을 `ValidationGroup` 속성입니다. 유효성 검사 그룹의 유효성 검사기의 유효성 검사 포스트백이 같은 단추를 통해 유도 될 경우에 `ValidationGroup` 속성을 설정 합니다. 트리거 DetailsView의 삽입 단추에 대 한 예를 들어 순서로 합니다 `InsertValidationControls` CommandField의 설정 해야 하는 유효성 검사 그룹 `ValidationGroup` 속성을 `InsertValidationControls` (그림 14 참조). 또한 GridView의 설정의 CommandField `ValidationGroup` 속성을 `EditValidationControls`입니다.


[![DetailsView 집합의 InsertValidationControls CommandField의 ValidationGroup 속성](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image41.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image40.png)

**그림 14**: DetailsView의 설정의 CommandField `ValidationGroup` 속성을 `InsertValidationControls` ([클릭 하 여 큰 이미지 보기](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image42.png))


이러한 변경 이후 TemplateFields 및 CommandFields GridView의 고 DetailsView 다음과 비슷하게 표시 됩니다.

DetailsView의 TemplateFields 및 CommandField

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/samples/sample4.aspx)]

GridView의 CommandField 및 TemplateFields

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/samples/sample5.aspx)]

이 시점에서 편집 전용 유효성 검사 컨트롤 실행 GridView의 업데이트 단추를 클릭 하는 경우에 및 삽입 전용 유효성 검사 컨트롤 화재 DetailsView의 삽입 단추를 클릭 하 여 그림 13 강조 표시 된 문제를 해결 하는 경우에 합니다. 그러나이 변경으로 인해 ValidationSummary 제어권 더 이상 표시 잘못 된 데이터를 입력할 때. ValidationSummary 컨트롤을 포함 한 `ValidationGroup` 속성 및 해당 유효성 검사 그룹의 해당 유효성 검사 컨트롤에 대 한 요약 정보 표시만 합니다. 따라서이 페이지에 대해 하나씩 두 개의 유효성 검사 컨트롤에 해야 합니다 `InsertValidationControls` 유효성 검사 그룹 및 `EditValidationControls`합니다.

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/samples/sample6.aspx)]

이 추가 사용 하 여 자습서 완료 되었습니다!

## <a name="summary"></a>요약

BoundFields 모두 편집 및 삽입 인터페이스에 제공 하는 동안 인터페이스를 사용자 지정할 수 없습니다. 일반적으로 편집 및 삽입 사용자가 올바른 형식으로 필요한 입력을 입력 하는 있는지 확인 하는 인터페이스에 유효성 검사 컨트롤을 추가 하려고 합니다. 이렇게 하려면 해야 TemplateFields BoundFields를 변환 하 고 적절 한 템플릿에 유효성 검사 컨트롤 추가. 이 자습서의 예제에서는 확장 된 *삽입, 업데이트 및 삭제와 관련 된 이벤트 검사* 인터페이스 및 GridView의 자습서에서는 두 DetailsView에 유효성 검사 컨트롤 추가 삽입 인터페이스를 편집 합니다. 뿐만 ValidationSummary 컨트롤을 사용 하 여 유효성 검사 요약 정보를 표시 하는 방법 및 페이지의 유효성 검사 컨트롤을 고유한 유효성 검사 그룹으로 분할 하는 방법에 살펴보았습니다.

이 자습서에서 보았듯이 TemplateFields 편집 및 삽입 인터페이스에 유효성 검사 컨트롤을 포함 하도록 확장 될 수 있습니다. TemplateFields 확장 될 수도 있습니다 추가 입력된 웹 컨트롤을 포함 하도록 더 적합 한 웹 컨트롤로 바꾸려는 텍스트를 사용 하도록 설정 합니다. 다음 자습서에서 외래 키를 편집 하는 경우 적합 한 데이터 바인딩된 DropDownList 컨트롤과 TextBox 컨트롤을 대체 하는 방법을 알아봅니다 (같은 `CategoryID` 나 `SupplierID` 에 `Products` 테이블).

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자는 Liz Shulok 및 Zack Jones 있었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)
> [다음](customizing-the-data-modification-interface-cs.md)
