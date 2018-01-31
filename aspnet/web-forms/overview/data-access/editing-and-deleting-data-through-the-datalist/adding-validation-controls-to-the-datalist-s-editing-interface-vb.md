---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/adding-validation-controls-to-the-datalist-s-editing-interface-vb
title: "DataList에 유효성 검사 컨트롤 추가 (VB) 인터페이스의 편집 | Microsoft Docs"
author: rick-anderson
description: "이 자습서에서는 유효성 검사에 컨트롤을 추가할 DataList의 EditItemTemplate 간단 명료 편집 사용자 없는 정수를 제공 하기 위해 얼마나 쉬운지 보겠습니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/30/2006
ms.topic: article
ms.assetid: 6b073fc6-524d-453d-be7c-0c30986de391
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/adding-validation-controls-to-the-datalist-s-editing-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: c2daa0eaca2764dec2d6323bf1f5a4f3af2e6bbe
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="adding-validation-controls-to-the-datalists-editing-interface-vb"></a>DataList의 편집 인터페이스 (VB)에 유효성 검사 컨트롤 추가
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_39_VB.exe) 또는 [PDF 다운로드](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/datatutorial39vb1.pdf)

> 이 자습서에서는 유효성 검사에 컨트롤을 추가할 DataList의 EditItemTemplate 간단 명료 편집 사용자 인터페이스를 제공 하기 위해 얼마나 쉬운지 살펴보겠습니다.


## <a name="introduction"></a>소개

자습서를 지금까지 편집 DataList의 인터페이스 편집 DataLists를 포함 하지는 자동 관리 사용자 입력된 유효성 검사 누락 된 제품 이름이 나 예외가 음수 가격 결과 같은 잘못 된 사용자가 입력 하는 경우에 합니다. 에 [이전 자습서](handling-bll-and-dal-level-exceptions-vb.md) 예외 처리 코드의 DataList 추가 하는 방법을 검사 했습니다 `UpdateCommand` catch 하 고 적절 하 게 발생 하는 모든 예외에 대 한 정보를 표시 하기 위해 이벤트 처리기입니다. 그러나 이상적으로 편집 인터페이스를 포함 한 사용자가 처음부터 이러한 잘못 된 데이터를 입력 하지 못하게 하려면 유효성 검사 컨트롤 합니다.

이 자습서에서는 보겠습니다 DataList s에 유효성 검사 컨트롤을 추가할 얼마나 쉬운지 `EditItemTemplate` 간단 명료 편집 사용자 인터페이스를 제공 하기 위해 합니다. 특히,이 자습서는 이전 자습서에서 만든 예제를 사용 하 고 적절 한 유효성 검사를 포함 하도록 편집 인터페이스 있었던 합니다.

## <a name="step-1-replicating-the-example-fromhandling-bll--and-dal-level-exceptionshandling-bll-and-dal-level-exceptions-vbmd"></a>1 단계: 복제의 예제[BLL 및 DAL 수준의 예외 처리](handling-bll-and-dal-level-exceptions-vb.md)

에 [처리 BLL-및 DAL 수준 예외](handling-bll-and-dal-level-exceptions-vb.md) 자습서 이름과 2 열, 편집 가능한 DataList의 제품 가격을 나열 하는 페이지를 만들었습니다. 이 자습서의 목표는 유효성 검사 컨트롤을 포함 하도록 DataList s 편집 인터페이스를 확장 하 것입니다. 특히,이 유효성 검사 논리를 수행합니다.

- S 제품 이름을 제공 해야 합니다.
- 가격에 대 한 입력 한 값이 올바른 통화 형식 인지 확인
- 가격 보다 크거나 음수 이후 0에 대해 입력 한 값 `UnitPrice` 은 잘못 된 값

유효성 검사를 포함 하도록 이전 예제를 확대 살펴보면 먼저 해야의 예제를 복제 하는 `ErrorHandling.aspx` 페이지에 `EditDeleteDataList` 이 자습서에 대 한 페이지로 폴더 `UIValidation.aspx`합니다. 둘 모두를 통해 복사 하려면 해야이 작업을 수행할는 `ErrorHandling.aspx` s 선언적 태그와 해당 소스 코드 페이지입니다. 먼저 다음 단계를 수행 하 여 선언적 태그를 통해 복사 합니다.

1. 열기는 `ErrorHandling.aspx` Visual Studio에서 페이지
2. 페이지 s 선언적 태그 (페이지 아래쪽에 원본 단추 클릭)로 이동
3. 내에서 텍스트를 복사는 `<asp:Content>` 및 `</asp:Content>` 태그 (-32 3 줄)으로 그림 1에 표시 합니다.


[![텍스트 내에서 복사 된 &lt;asp: Content&gt; 컨트롤](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image2.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image1.png)

**그림 2**: 텍스트 내 복사는 `<asp:Content>` 컨트롤 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image3.png))


1. 열기는 `UIValidation.aspx` 페이지
2. 페이지 s 선언적 태그로 이동
3. 내에서 텍스트를 붙여는 `<asp:Content>` 제어 합니다.

소스 코드를 복사한 열고는 `ErrorHandling.aspx.vb` 페이지 및 텍스트만 복사 *내* 는 `EditDeleteDataList_ErrorHandling` 클래스입니다. 세 개의 이벤트 처리기를 복사 (`Products_EditCommand`, `Products_CancelCommand`, 및 `Products_UpdateCommand`)와 함께 `DisplayExceptionDetails` 메서드이지만 do **하지** 복사 클래스 선언 또는 `using` 문. 다음 복사한 텍스트를 붙여 *내* 는 `EditDeleteDataList_UIValidation` 클래스 `UIValidation.aspx.vb`합니다.

내용 및 코드를 통해 이동 후 `ErrorHandling.aspx` 를 `UIValidation.aspx`, 브라우저에서 페이지를 테스트 하 합니다. 동일한 출력이 표시 하 고 각 (그림 2 참조)는 이러한 두 페이지에 동일한 기능을 발생 해야 합니다.


[![UIValidation.aspx 페이지 ErrorHandling.aspx의 기능과 유사한](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image5.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image4.png)

**그림 2**:는 `UIValidation.aspx` 페이지의 기능과 유사한 `ErrorHandling.aspx` ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image6.png))


## <a name="step-2-adding-the-validation-controls-to-the-datalist-s-edititemtemplate"></a>2 단계: DataList의 EditItemTemplate에 유효성 검사 컨트롤 추가

데이터 입력 폼을 생성할 때에는 사용자가 모든 필수 필드를 입력 하는 법률, 형식이 올바르지 값의 모든 제공 된 입력 되지 않았는지 중요 합니다. 사용자의 입력이 유효한 지 확인 하려면 ASP.NET에서는 단일 입력된 웹 컨트롤의 값의 유효성을 검사 하도록 설계 된 다섯 개의 기본 제공 유효성 검사 컨트롤을 제공 합니다.

- [RequiredFieldValidator](https://msdn.microsoft.com/library/5hbw267h(VS.80).aspx) 는 값이 제공 되었는지를 확인 합니다.
- [CompareValidator](https://msdn.microsoft.com/library/db330ayw(VS.80).aspx) 다른 웹 컨트롤 값 또는 상수 값에 대 한 값을 확인 하거나 s 값 형식으로 지정된 된 데이터 형식에 대 한 법적
- [RangeValidator](https://msdn.microsoft.com/library/f70d09xt.aspx) 값의 범위 내에서 값을 확인 합니다.
- [RegularExpressionValidator](https://msdn.microsoft.com/library/eahwtc9e.aspx) 에 대 한 값의 유효성을 검사 한 [정규식](http://en.wikipedia.org/wiki/Regular_expression)
- [CustomValidator](https://msdn.microsoft.com/library/9eee01cx(VS.80).aspx) 를 기준으로 사용자 지정, 사용자 정의 메서드

이러한 다섯 개의 컨트롤에 대 한 자세한 내용은 다시 참조는 [편집 및 삽입 인터페이스에 유효성 검사 컨트롤 추가](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md) 자습서 또는 체크 아웃 된 [유효성 검사 컨트롤 섹션](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/validation/default.aspx) 는 의[ASP.NET 빠른 시작 자습서](https://quickstarts.asp.net)합니다.

이 자습서에 대 한 제품 이름에 대 한 값을 제공 된 되도록 RequiredFieldValidator 및 입력 한 가격의 값이 0이 고 올바른 통화 형식으로 표시 되도록 CompareValidator 사용 해야 합니다.

> [!NOTE]
> ASP.NET 동안 1.x에 이러한 동일한 5 개의 유효성 검사 컨트롤, ASP.NET 2.0이 다양 한 기능이 향상을 추가, 외에도 Internet Explorer 브라우저와 파티션 유효성 검사 컨트롤에 페이지에는 기능에 대 한 지원 클라이언트 쪽 스크립트 되 고 두 개의 주 유효성 검사 그룹입니다. 2.0의 새로운 유효성 검사 제어 기능에 대 한 자세한 내용은 참조 [ASP.NET 2.0에서 유효성 검사 컨트롤 나누어서](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)합니다.


DataList s에 필요한 유효성 검사 컨트롤을 추가 하 여 시작 s `EditItemTemplate`합니다. DataList s 스마트 태그에서 템플릿 편집 링크를 클릭 하 여 디자이너를 통해 또는 선언적 구문을 통해이 작업을 수행할 수 있습니다. 디자인 보기에서 템플릿 편집 옵션을 사용 하 여 프로세스를 통해 s 단계를 사용 합니다. DataList s 편집 하도록 선택한 후 `EditItemTemplate`, 후 배치는 RequiredFieldValidator 템플릿 편집 인터페이스에 도구 상자에서 끌어 추가 `ProductName` 텍스트 상자에 붙여넣습니다.


[![RequiredFieldValidator 다음 제품 이름 텍스트 상자는 EditItemTemplate에 추가](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image8.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image7.png)

**그림 3**:에 RequiredFieldValidator 추가 `EditItemTemplate After` 는 `ProductName` 텍스트 상자에 붙여넣습니다 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image9.png))


모든 유효성 검사 컨트롤 단일 ASP.NET 웹 컨트롤의 입력을 확인 하 여 작동 합니다. 따라서 방금 추가한 RequiredFieldValidator에 대해 유효성을 검사 해야 나타내려면 필요는 `ProductName` TextBox; s 유효성 검사 컨트롤을 설정 하 여 이렇게 [ `ControlToValidate` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.controltovalidate(VS.80).aspx) 에 `ID` 의 적절 한 웹 컨트롤 (`ProductName`,이 경우). 다음으로 설정 된 [ `ErrorMessage` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.errormessage(VS.80).aspx) 하려면 s 제품 이름을 제공 해야 및 [ `Text` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.text(VS.80).aspx) 를 \*합니다. `Text` 속성 값을 제공 하는 경우는 유효성 검사에 실패 하면 유효성 검사 컨트롤에 의해 표시 되는 텍스트입니다. `ErrorMessage` 는 필수 사항인 속성 값은 경우 ValidationSummary 컨트롤이 사용는 `Text` 속성 값이 생략 되는 `ErrorMessage` 속성 값이 잘못 된 입력의 유효성 검사 컨트롤에서 표시 됩니다.

RequiredFieldValidator의이 세 가지 속성을 설정한 후 화면 그림 4 비슷해야 합니다.


[![RequiredFieldValidator의 ControlToValidate, ErrorMessage, 및 텍스트 속성 설정](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image11.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image10.png)

**그림 4**: RequiredFieldValidator s 설정 `ControlToValidate`, `ErrorMessage`, 및 `Text` 속성 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image12.png))


에 추가 RequiredFieldValidator와는 `EditItemTemplate`의제품 가격 텍스트 상자에 대 한 필요한 유효성 검사를 계속 인지 모든 합니다. 이후는 `UnitPrice` 는 선택 사항는 RequiredFieldValidator 추가 해야 하는 t 하지 않는 레코드를 편집할 때 했습니다. 하지만 이때 되도록 CompareValidator를 추가 해야는 `UnitPrice`제공 된 경우, 통화로 형식이 올바르게 고 0 보다 크거나 합니다.

에 CompareValidator 추가 `EditItemTemplate` 설정 하 고 해당 `ControlToValidate` 속성을 `UnitPrice`, 해당 `ErrorMessage` 가격에 대 한 속성 보다 크거나 0 이어야 하며 통화 기호를 포함할 수 없습니다 및 해당 `Text` 속성\*. 해당는 `UnitPrice` 값 해야 0 보다 크거나, CompareValidator s 설정 [ `Operator` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.operator(VS.80).aspx) 를 `GreaterThanEqual`, 해당 [ `ValueToCompare` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.valuetocompare(VS.80).aspx) 0으로 및 해당 [ `Type` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basecomparevalidator.type.aspx) 를 `Currency`합니다.

DataList s 이러한 두 가지 유효성 검사 컨트롤을 추가한 후 `EditItemTemplate` s 선언적 구문 다음과 비슷해야 합니다.


[!code-aspx[Main](adding-validation-controls-to-the-datalist-s-editing-interface-vb/samples/sample1.aspx)]

다음과 같이 변경한 후 브라우저에서 페이지를 엽니다. 이름을 생략 하거나 제품을 편집할 때 유효 하지 않은 가격 값을 입력 하려고 하면 텍스트 상자 옆에 별표가 나타납니다. 그림 5에서 볼 수 있듯이 $19.95 같은 통화 기호를 포함 하는 가격 값을 잘못 된 간주 됩니다. CompareValidator s `Currency` `Type` 자릿수 구분 기호 (예: 쉼표 또는 마침표 문화권 설정에 따라) 선행 더하기 또는 빼기 기호를 허용 하지만 않습니다 *하지* 통화 기호를 허용 합니다. 이 동작은 현재 편집 인터페이스를 렌더링 하는 대로 사용자 perplex 수는 `UnitPrice` 통화 형식을 사용 하 여 합니다.


[![잘못 된 입력이 포함 된 텍스트 상자 옆에 별표가 나타납니다.](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image14.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image13.png)

**그림 5**: An 별표 표시 하려면 "다음" 잘못 된 입력이 포함 된 텍스트 상자 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image15.png))


동일 하 게 유효성 검사 동작 하는 동안-는 사용자는 허용 되지 않는 레코드를 편집할 때 통화 기호를 수동으로 제거 해야 합니다. 또한 없는 잘못 된 경우 편집을 위한 입력 모두 업데이트 하거나 취소 단추를 클릭 하면에서 포스트백을 호출 합니다 인터페이스입니다. 이상적으로 "취소" 단추가 사용자의 입력의 유효성에 관계 없이 미리 편집 상태로 DataList를 반환 합니다. 또한 s DataList의 제품 정보를 업데이트 하기 전에 s 페이지 데이터가 유효한 지 확인 해야 `UpdateCommand` 브라우저가 JavaScript t 지원 하지 않거나 사용자가 클라이언트 쪽 논리를 무시할 수 있습니다 유효성 검사 컨트롤에 따라 이벤트 처리기 지원을 사용 하지 않도록 설정 합니다.

## <a name="removing-the-currency-symbol-from-the-edititemtemplate-s-unitprice-textbox"></a>EditItemTemplate의 UnitPrice 텍스트 상자에서 통화 기호를 제거합니다.

CompareValidator s를 사용 하는 경우 `Currency``Type`, 유효성을 검사할 입력 모든 통화 기호를 포함 하지 않아야 합니다. 그러한 기호의 존재 하면 CompareValidator 입력 잘못 된 것으로 표시 합니다. 그러나 우리 편집 인터페이스의 통화 기호를 현재 포함는 `UnitPrice` TextBox, 즉 해당 변경 내용을 저장 하기 전에 사용자의 통화 기호를 명시적으로 제거 해야 합니다. 이 세 가지 옵션이 있습니다.

1. 구성에서 `EditItemTemplate` 있도록는 `UnitPrice` 통화로 TextBox 값의 서식을 지정 하지 않습니다.
2. 사용자는 CompareValidator를 제거 하 고 적절 한 형식의 통화 값을 확인 하는 RegularExpressionValidator로 바꿔 통화 기호를 허용 합니다. 여기에서 문제를 통화 값의 유효성을 검사 하는 정규식에서 CompareValidator로 간단 하지 않습니다 이며 culture 설정을 통합 하 려 하는 경우 코드를 작성 해야 합니다.
3. 유효성 검사 컨트롤을 모두 제거 하 고 GridView s에서 사용자 지정 서버 쪽 유효성 검사 논리에 의존 `RowUpdating` 이벤트 처리기입니다.

옵션 1이 자습서와 함께 s를 사용 합니다. 현재는 `UnitPrice` 에 텍스트 상자에 대 한 데이터 바인딩 식으로 인해 통화 값으로 형식이 지정 되는 `EditItemTemplate`: `<%# Eval("UnitPrice", "{0:c}") %>`합니다. 변경의 `Eval` 문을 `Eval("UnitPrice", "{0:n2}")`, 전체 자릿수 두 자리 숫자로 결과 형식을 지정 합니다. 선언적 구문 또는에서 데이터 바인딩 편집 링크를 클릭 하 여 수행할 수 있습니다는 `UnitPrice` s DataList의 TextBox `EditItemTemplate`합니다.

이러한 변경으로 인해 편집 인터페이스에 형식이 지정 된 가격 그룹 구분 기호로 쉼표와 소수 구분 기호로 마침표를 포함 하지만 통화 기호 생략 합니다.

> [!NOTE]
> 통화 형식을 편집할 수 있는 인터페이스에서 제거 하는 경우 I 도움이 될 텍스트 TextBox 외부 통화 기호를 삽입 합니다. 이 통화 기호를 제공 하는 필요 하지 않은 사용자에 게 힌트로 갖습니다.


## <a name="fixing-the-cancel-button"></a>"취소" 단추가 수정

기본적으로 유효성 검사 웹 컨트롤에는 클라이언트 쪽 유효성 검사를 수행 하는 JavaScript을 내보냅니다. 단추, LinkButton을 또는 ImageButton 클릭 하면 페이지에서 유효성 검사 컨트롤 포스트백에서 발생 하기 전에 클라이언트 쪽에서 확인 됩니다. 잘못 된 데이터 포스트백이 취소 됩니다. 특정 단추에 대 한 하지만 데이터의 유효성을 검사 못할 수도 있습니다 자재; 이 경우 데이터가 잘못 되어 취소 포스트백을 성가신 합니다.

취소 단추에는 이러한는 예입니다. 사용자가 s 제품 이름을 생략 하는 등의 잘못 된 데이터를 입력한 다음 제품을 모두 저장 하려면 그녀는 대상이 t 필요에 따라 결정 및 취소 단추에 도달 한다고 가정 합니다. 현재, "취소" 단추가 제품 이름은 누락 이며 다시 게시 되지 않도록 보고서를 페이지에서 유효성 검사 컨트롤을 트리거합니다. 우리의 사용자가 일부 텍스트를 입력 하 고 `ProductName` 를 편집 하는 프로세스를 취소 합니다. 텍스트 상자에 붙여넣습니다.

단추, LinkButton을 및 ImageButton가 다행히는 [ `CausesValidation` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.causesvalidation.aspx) 수를 나타내는 클릭 여부 단추는 유효성 검사 논리를 시작 해야 할 (기본적으로 `True`). 취소 단추 s 설정 `CausesValidation` 속성을 `False`합니다.

## <a name="ensuring-the-inputs-are-valid-in-the-updatecommand-event-handler"></a>유효 합니다. UpdateCommand 이벤트 처리기는 입력 되었는지 확인

클라이언트 쪽 스크립트 유효성 검사 컨트롤에서 내보낸으로 인해 사용자가 잘못 된 입력을 입력 유효성 검사 컨트롤 LinkButton 단추에서 시작 된 모든 포스트백을 취소 하거나 ImageButton 컨트롤 `CausesValidation` 속성은 `True` ( 기본값)입니다. 그러나 구식된 브라우저 또는 JavaScript 지원 사용 하지 않도록 설정 되어 있는 사용자가 방문 하는 경우에 클라이언트 쪽 유효성 검사 실행 되지 않습니다.

ASP.NET 유효성 검사 컨트롤의 모든 다시 게시 하는 즉시 유효성 검사 논리를 반복 하 고 보고서를 통해 페이지의 입력의 전체 유효성은 [ `Page.IsValid` 속성](https://msdn.microsoft.com/library/system.web.ui.page.isvalid.aspx)합니다. 그러나 페이지 흐름 하지 중단 되거나 중지의 값에 따라 방식으로 모든 `Page.IsValid`합니다. 개발자는 취급 해야 되도록는 `Page.IsValid` 속성의 값은 `True` 전에 유효한 가정 하는 코드를 계속 입력 데이터를 필터링 합니다.

사용자는 사용 하지 않도록 설정 하는 JavaScript, 가격 페이지 방문, 제품을 편집가 너무의 가격 값을 입력 비용이 많이 들며, 업데이트 단추를 클릭 하 고 클라이언트 쪽 유효성 검사를 건너뛰며 ´ ë · 다시 게시 됩니다. ASP.NET 페이지 s 다시 게시 될 `UpdateCommand` 이벤트 처리기를 실행 하 고 너무 구문 분석 하려고 할 때 예외가 발생 하는 데 비용이 많이 `Decimal`합니다. 예외 처리 한, 이러한 예외를 제대로 처리 될 됩니다 있지만으로 계속 하 여 처음부터 통해 지연에서 잘못 된 데이터를 처리할 수 있도록 하므로 `UpdateCommand` 이벤트 처리기 경우 `Page.IsValid` 값 `True`합니다.

다음 코드의 시작 부분에 추가 `UpdateCommand` 이벤트 처리기 바로 앞의 `Try` 블록:


[!code-vb[Main](adding-validation-controls-to-the-datalist-s-editing-interface-vb/samples/sample2.vb)]

이 추가 제품에서는 제출 된 데이터가 유효한 경우에 업데이트 하려고 합니다. T-이득 대부분의 사용자가 포스트백 유효성 검사 컨트롤 클라이언트 쪽 스크립트 인해 잘못 된 데이터 수 있지만 사용자 브라우저가 JavaScript 지원 하지 않는 또는 지원 되는 JavaScript 클라이언트 검사를 무시 하 고 잘못 된 데이터를 제출할 비활성화 합니다.

> [!NOTE]
> 예리한 독자 이라는 것을 GridView로 데이터를 업데이트 하는 경우 우리 않았음에도 t를 명시적으로 확인 해야 합니다.는 `Page.IsValid`의 페이지 코드 숨김 클래스의 속성입니다. GridView 참조 때문에 이것이 `Page.IsValid` 와 진행의 값을 반환 하는 경우에 업데이트에 대 한 속성 `True`합니다.


## <a name="step-3-summarizing-data-entry-problems"></a>3 단계: 데이터 입력 문제 요약

ASP.NET 5 개의 유효성 검사 컨트롤 외에도 포함 되어는 [ValidationSummary 컨트롤](https://msdn.microsoft.com/library/f9h59855(VS.80).aspx)를 표시 하는 `ErrorMessage` 잘못 된 데이터를 검색 하는 이러한 유효성 검사 컨트롤의 s입니다. 웹 페이지에서 또는 모달, 클라이언트 쪽 messagebox를 통해 텍스트로이 요약 데이터를 표시할 수 있습니다. S 유효성 검사 문제를 요약 하는 클라이언트 쪽 messagebox를 포함 하려면이 자습서를 향상 시킬 수 있도록 합니다.

이를 위해 디자이너 도구 상자에서 ValidationSummary 컨트롤을 끕니다. ValidationSummary 컨트롤 대상이 t 위치 중요 이후 다시 messagebox의 요약만 표시 되도록 구성 하려면 했습니다. 설정 된 컨트롤을 추가한 후 해당 [ `ShowSummary` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showsummary(VS.80).aspx) 를 `False` 및 해당 [ `ShowMessageBox` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showmessagebox(VS.80).aspx) 를 `True`합니다. 이 추가 된 유효성 검사 오류가 클라이언트 쪽 messagebox에 요약 되어 있습니다 (그림 6 참조).


[![유효성 검사 오류는 클라이언트 쪽 Messagebox에 요약 되어 있습니다.](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image17.png)](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image16.png)

**그림 6**: The 유효성 검사 오류는 클라이언트 쪽 Messagebox에 요약 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](adding-validation-controls-to-the-datalist-s-editing-interface-vb/_static/image18.png))


## <a name="summary"></a>요약

이 자습서의 사전 업데이트 워크플로에서 사용 하기 전에 사용자 입력이 유효한 지를 확인 하려면 유효성 검사 컨트롤을 사용 하 여 예외가 발생할 가능성을 줄이는 방법에 살펴보았습니다. ASP.NET은 특정 웹 검사 하도록 설계 된 다섯 개의 유효성 검사 웹 컨트롤의 입력 제어 및 입력된 s 유효성에 다시 보고를 제공 합니다. 이 자습서에서는 이러한 다섯 개의 컨트롤 중 두 가지는 RequiredFieldValidator와는 CompareValidator를 사용 s 제품 이름을 제공 하 고 가격 보다 크거나 0 값을 사용 하는 통화 형식에 있는지 확인 합니다.

DataList s 편집 인터페이스에 유효성 검사 컨트롤을 추가 하는 것은 배치 표에 끌기 정도로 간단는 `EditItemTemplate` 선택 하 고 일련의 속성을 설정 합니다. 기본적으로 유효성 검사 컨트롤 자동으로 내보내기 클라이언트 쪽 유효성 검사 스크립트입니다. 또한 다시 게시 될 누적 결과에 저장 하면 서버 쪽 유효성 검사를 제공는 `Page.IsValid` 속성입니다. 단추, LinkButton을 또는 ImageButton을 클릭할 때 클라이언트 쪽 유효성 검사를 무시 하려면 s 단추 설정 `CausesValidation` 속성을 `False`합니다. 또한 포스트백에 제출 된 데이터가 있는 모든 작업을 수행 하기 전에 확인는 `Page.IsValid` 속성에서 반환 `True`합니다.

자습서를 편집 하 여 DataList의 모든에서는 지금까지 검사 했습니다의 제품 이름에 대 한 텍스트 상자 및 가격에 대 한 다른 편집 매우 간단한 인터페이스 (가) 필요 합니다. 그러나 편집 인터페이스 dropdownlist 활용, 일정, 라디오 단추, 확인란, 등의 다른 웹 컨트롤의 혼합을 포함할 수 있습니다. 다음 자습서는 다양 한 웹 컨트롤을 사용 하는 인터페이스를 작성 하는 방법을 살펴보겠습니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자가 Dennis Patterson, Ken Pespisa 및 Liz Shulok 합니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](handling-bll-and-dal-level-exceptions-vb.md)
[다음](customizing-the-datalist-s-editing-interface-vb.md)
