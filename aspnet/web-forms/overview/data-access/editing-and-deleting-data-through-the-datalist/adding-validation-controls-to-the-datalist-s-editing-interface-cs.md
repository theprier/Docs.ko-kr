---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/adding-validation-controls-to-the-datalist-s-editing-interface-cs
title: DataList에 유효성 검사 컨트롤 추가 편집 인터페이스 (C#) | Microsoft Docs
author: rick-anderson
description: 이 자습서를 간단 명료 편집 사용자 없는 정수를 제공 하기 위해 DataList의 EditItemTemplate에 유효성 검사 컨트롤을 추가할 얼마나 쉬운지 살펴보겠습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/30/2006
ms.topic: article
ms.assetid: 3ecc21c5-da0e-40ab-abb4-fac1e47398ad
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/adding-validation-controls-to-the-datalist-s-editing-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: 23b7a0a4fd5786d5bbc2905022a76dfc048d44bf
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37389962"
---
<a name="adding-validation-controls-to-the-datalists-editing-interface-c"></a>DataList의 편집 인터페이스 (C#)에 유효성 검사 컨트롤 추가
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_39_CS.exe) 또는 [PDF 다운로드](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/datatutorial39cs1.pdf)

> 이 자습서를 간단 명료 편집 사용자 인터페이스를 제공 하기 위해 DataList의 EditItemTemplate에 유효성 검사 컨트롤을 추가할 얼마나 쉬운지 알아봅니다.


## <a name="introduction"></a>소개

자습서를 지금 편집 DataList에서 누락 된 제품 이름 또는 예외가 음수 가격 결과 같은 잘못 된 사용자 입력도 사전 사용자 입력된 유효성 검사 인터페이스 편집 DataLists 포함할 합니다. 에 [이전 자습서](handling-bll-and-dal-level-exceptions-cs.md) 예외 처리 코드의 DataList 추가 하는 방법을 살펴보았습니다 `UpdateCommand` catch 하 고 정상적으로 발생 하는 모든 예외에 대 한 정보를 표시 하기 위해 이벤트 처리기입니다. 그러나 이상적으로 편집 인터페이스는 이러한 잘못 된 데이터를 처음부터 입력에서 사용자를 방지 하기 위해 유효성 검사 컨트롤입니다.

이 자습서에서는 살펴보겠습니다 DataList s에 유효성 검사 컨트롤을 추가할 얼마나 쉬운지 `EditItemTemplate` 간단 명료 편집 사용자 인터페이스를 제공 하기 위해. 특히,이 자습서는 이전 자습서에서 만든 예제를 사용 하 고 적절 한 유효성 검사를 포함 하는 편집 인터페이스 확대.

## <a name="step-1-replicating-the-example-fromhandling-bll--and-dal-level-exceptionshandling-bll-and-dal-level-exceptions-csmd"></a>1 단계: 복제 예제의[BLL 및 DAL 수준의 예외 처리](handling-bll-and-dal-level-exceptions-cs.md)

에 [처리 BLL 및 DAL 수준의 예외](handling-bll-and-dal-level-exceptions-cs.md) 자습서 이름과 두 개의 열, 편집 가능한 DataList 제품의 가격을 나열 하는 페이지를 만들었습니다. 이 자습서에 대 한 우리의 목표는 DataList s 편집 인터페이스 유효성 검사 컨트롤을 포함 하도록 확장입니다. 특히이 유효성 검사 논리는:

- S 제품 이름에 제공 해야 합니다.
- 가격에 대 한 입력 한 값을 유효한 통화 형식 인지 확인
- 가격 보다 크거나 음수 이후 0에 대 한 입력 된 값이 `UnitPrice` 값 올바르지 않습니다.

먼저에서 예제를 복제 해야 전에 확장 유효성 검사를 포함 하도록 앞의 예제를 살펴볼 수 있습니다는 `ErrorHandling.aspx` 페이지에 `EditDeleteDataList` 이 자습서에서는 페이지에는 폴더 `UIValidation.aspx`합니다. 모두 복사 해야이 작업을 수행 하는 `ErrorHandling.aspx` s 선언적 태그와 해당 소스 코드 페이지입니다. 먼저 다음 단계를 수행 하 여 선언적 태그도 복사 합니다.

1. 열기는 `ErrorHandling.aspx` Visual Studio에서 페이지
2. 페이지 s 선언적 태그 (페이지의 맨 아래에 있는 원본 단추 클릭)로 이동
3. 내에서 텍스트를 복사 합니다 `<asp:Content>` 및 `</asp:Content>` 그림 1에 표시 된 것된으로 태그 (줄 3 ~ 32).


[![텍스트 내에 복사 합니다 &lt;asp: Content&gt; 컨트롤](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image2.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image1.png)

**그림 1**: 텍스트 내에 복사 합니다 `<asp:Content>` 컨트롤 ([클릭 하 여 큰 이미지 보기](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image3.png))


1. 열기는 `UIValidation.aspx` 페이지
2. 페이지 s 선언적 태그로 이동
3. 내에서 텍스트를 붙여 넣습니다는 `<asp:Content>` 제어 합니다.

소스 코드를 복사 하려면 엽니다는 `ErrorHandling.aspx.vb` 페이지 및 텍스트만 복사 *내* 는 `EditDeleteDataList_ErrorHandling` 클래스. 세 개의 이벤트 처리기를 복사 (`Products_EditCommand`, `Products_CancelCommand`, 및 `Products_UpdateCommand`)와 함께 `DisplayExceptionDetails` 메서드 없이 **하지** 클래스 선언 복사 또는 `using` 문. 복사한 텍스트를 붙여 넣습니다 *내* 는 `EditDeleteDataList_UIValidation` 클래스 `UIValidation.aspx.vb`합니다.

콘텐츠 및 코드를 통해 이동한 후 `ErrorHandling.aspx` 에 `UIValidation.aspx`, 잠시 브라우저에서 페이지를 테스트 합니다. 이러한 두 페이지 (그림 2 참조)에서 각각에 동일한 기능을 경험 및 동일한 출력이 표시 됩니다.


[![UIValidation.aspx 페이지 ErrorHandling.aspx의 기능을 모방](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image5.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image4.png)

**그림 2**: 합니다 `UIValidation.aspx` 페이지에서 기능을 모방 `ErrorHandling.aspx` ([클릭 하 여 큰 이미지 보기](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image6.png))


## <a name="step-2-adding-the-validation-controls-to-the-datalist-s-edititemtemplate"></a>2 단계: DataList의 EditItemTemplate 유효성 검사 컨트롤 추가

데이터 입력 폼을 생성할 때는 사용자가 모든 필수 필드를 입력 하는 모든 제공 된 입력 법적, 올바르게 형식이 지정 된 값에는 중요 합니다. 사용자가의 입력 유효한 지 확인 하려면 ASP.NET 입력된 웹 컨트롤을 단일 값의 유효성을 검사 하도록 설계 된 5 개의 기본 제공 유효성 검사 컨트롤을 제공 합니다.

- [RequiredFieldValidator](https://msdn.microsoft.com/library/5hbw267h(VS.80).aspx) 는 값이 제공 되었는지를 확인 합니다.
- [CompareValidator](https://msdn.microsoft.com/library/db330ayw(VS.80).aspx) 다른 웹 컨트롤 값 또는 상수 값, 값의 유효성을 검사 하거나 s 값 형식 지정된 데이터 형식에 대 한 법적으로 보장
- [RangeValidator](https://msdn.microsoft.com/library/f70d09xt.aspx) 값의 범위 내에서 값을 확인 합니다.
- [RegularExpressionValidator](https://msdn.microsoft.com/library/eahwtc9e.aspx) 에 대 한 값의 유효성을 검사 한 [정규식](http://en.wikipedia.org/wiki/Regular_expression)
- [CustomValidator](https://msdn.microsoft.com/library/9eee01cx(VS.80).aspx) 를 기준으로 사용자 지정, 사용자 정의 메서드

이러한 다섯 개의 컨트롤에 대 한 자세한 내용은 다시 참조 하는 [편집 및 삽입 인터페이스에 유효성 검사 컨트롤 추가](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md) 자습서 또는 체크 아웃 합니다 [유효성 검사 컨트롤 섹션](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/validation/default.aspx) 합니다 의[ASP.NET 퀵 스타트 자습서](https://quickstarts.asp.net)합니다.

이 자습서에 대 한 제품 이름에 대 한 값을 지정 된 되도록 RequiredFieldValidator 및 입력 한 가격 값이 0 보다 크거나 및 유효한 통화 형식으로 표시 됩니다 되도록 CompareValidator 사용 하도록 해야 합니다.

> [!NOTE]
> 반면 ASP.NET 1.x가 이러한 동일한 5 유효성 검사 컨트롤, ASP.NET 2.0에는 수많은 개선 사항이 추가 되었습니다, Internet Explorer 외에도 브라우저 및 파티션 유효성 검사 컨트롤에는 페이지 수에 대 한 지원 클라이언트 쪽 스크립트 되 고 두 개의 주 유효성 검사 그룹입니다. 2.0의 새로운 유효성 검사 컨트롤 기능에 대 한 자세한 내용은 참조 [ASP.NET 2.0의 유효성 검사 컨트롤 분석](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)합니다.


DataList s에 필요한 유효성 검사 컨트롤을 추가 하 여 시작 s `EditItemTemplate`입니다. DataList s 스마트 태그에서 템플릿 편집 링크를 클릭 하 여 디자이너를 통해 또는 선언적 구문을 통해이 작업을 수행할 수 있습니다. 디자인 보기에서 템플릿 편집 옵션을 사용 하는 프로세스를 단계별로를 s 수 있습니다. DataList s를 편집 하려면 선택한 후 `EditItemTemplate`, 후 배치를 RequiredFieldValidator 끌어와 도구 상자에서 템플릿 편집 인터페이스에 추가 된 `ProductName` 텍스트 상자에 붙여넣습니다.


[![EditItemTemplate는 RequiredFieldValidator ProductName 텍스트 뒤에 추가](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image8.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image7.png)

**그림 3**:를 RequiredFieldValidator 추가 합니다 `EditItemTemplate After` 는 `ProductName` 텍스트 상자에 붙여넣습니다 ([클릭 하 여 큰 이미지 보기](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image9.png))


모든 유효성 검사 컨트롤 단일 ASP.NET 웹 컨트롤의 입력 유효성을 검사 하 여 작동 합니다. 방금 추가한 RequiredFieldValidator에 대해 유효성을 검사 해야를 지정 해야 하므로 합니다 `ProductName` 텍스트 상자 s 유효성 검사 컨트롤을 설정 하 여 이렇게 [ `ControlToValidate` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.controltovalidate(VS.80).aspx) 에 `ID` 의 적절 한 웹 컨트롤 (`ProductName`, 이런에서). 다음으로 설정 합니다 [ `ErrorMessage` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.errormessage(VS.80).aspx) 하려면 s 제품 이름을 제공 해야 및 [ `Text` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.text(VS.80).aspx) 에 \*입니다. `Text` 속성 값을 제공 하는 경우이 유효성 검사에 실패 하는 경우 유효성 검사 컨트롤에 표시 되는 텍스트입니다. `ErrorMessage` 속성 값이 필요한 경우 ValidationSummary 컨트롤에서 사용 됩니다 합니다 `Text` 속성 값을 생략 하면는 `ErrorMessage` 속성 값이 잘못 된 입력의 유효성 검사 컨트롤에서 표시 됩니다.

RequiredFieldValidator의 이러한 세 가지 속성으로 설정한 후 화면 그림 4 유사 합니다.


[![RequiredFieldValidator의 ControlToValidate, ErrorMessage을 및 텍스트 속성 설정](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image11.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image10.png)

**그림 4**: 집합 RequiredFieldValidator s `ControlToValidate`를 `ErrorMessage`, 및 `Text` 속성 ([클릭 하 여 큰 이미지 보기](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image12.png))


추가할 RequiredFieldValidator를 사용 하 여는 `EditItemTemplate`계속의 제품 가격 텍스트 상자에 대 한 필요한 유효성 검사를 추가 하는 모든. 있으므로 `UnitPrice` 선택 사항인 RequiredFieldValidator를 추가할 t 필요 하지에서는 레코드를 편집할 때. 하지만 되도록 CompareValidator를 추가 해야 그렇게는 `UnitPrice`제공 하는 경우 이며 0 보다 크거나을 통화로 형식이 올바르게 합니다.

CompareValidator에 추가 합니다 `EditItemTemplate` 설정 및 해당 `ControlToValidate` 속성을 `UnitPrice`, 해당 `ErrorMessage` 가격에 대 한 속성 보다 크거나 0 이어야 하며 통화 기호를 포함할 수 없습니다 및 해당 `Text` 속성\*. 나타내는 합니다 `UnitPrice` 값 0 보다 크거나 같아야, CompareValidator s를 설정 해야 합니다 [ `Operator` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.operator(VS.80).aspx) 하 `GreaterThanEqual`, 해당 [ `ValueToCompare` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.valuetocompare(VS.80).aspx) 0으로 및 해당 [ `Type` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basecomparevalidator.type.aspx) 하려면 `Currency`합니다.

이러한 두 가지 유효성 검사 컨트롤, s DataList를 추가한 후 `EditItemTemplate` s 선언적 구문을 다음과 유사 합니다.


[!code-aspx[Main](adding-validation-controls-to-the-datalist-s-editing-interface-cs/samples/sample1.aspx)]

다음과 같이 변경한 후 브라우저에서 페이지를 엽니다. 이름을 생략 하거나 제품을 편집 하는 경우 유효 하지 않은 가격 값을 입력 하려는 경우 텍스트 상자 옆에 있는 별표 표시 됩니다. 그림 5에서 알 수 있듯이, $19.95 같은 통화 기호를 포함 하는 가격 잘못 된 간주 됩니다. CompareValidator s `Currency` `Type` 자릿수 구분 기호 (예: 쉼표 또는 마침표 문화권 설정에 따라) 및 선행 더하기 또는 빼기 기호를 허용 하지만 않습니다 *하지* 통화 기호를 허용 합니다. 이 동작은 현재 편집 인터페이스를 렌더링 하는 대로 사용자 perplex 수는 `UnitPrice` 통화 형식을 사용 하 여 합니다.


[![잘못 된 입력을 사용 하 여 텍스트 상자 옆에 있는 별표 표시 됩니다.](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image14.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image13.png)

**그림 5**: An 별표 표시 옆에 잘못 된 입력을 사용 하 여 텍스트 상자 ([큰 이미지를 보려면 클릭](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image15.png))


으로 유효성 검사 작동 하는 동안-인 사용자가 허용 되지 않는 레코드를 편집 하는 경우 통화 기호를 수동으로 제거 해야 합니다. 또한 없는 경우 올바른 편집을 위한 입력 모두 업데이트 하거나 취소 단추를 클릭 하면 포스트백을 호출 하는 인터페이스입니다. 이상적으로 취소 단추는 사용자가의 입력의 유효성에 관계 없이 미리 편집 상태로 DataList를 반환 합니다. 또한 DataList s의에서 제품 정보를 업데이트 하기 전에 페이지의 데이터가 유효한 지 확인 해야 `UpdateCommand` 해당 브라우저 JavaScript 지원 하지 않거나 사용자가 클라이언트 쪽 논리를 무시할 수 있습니다 유효성 검사 컨트롤에 따라 이벤트 처리기 지원을 사용 하지 않도록 설정 합니다.

## <a name="removing-the-currency-symbol-from-the-edititemtemplate-s-unitprice-textbox"></a>EditItemTemplate의 UnitPrice 텍스트에서 통화 기호를 제거합니다.

CompareValidator s를 사용 하는 경우 `Currency``Type`, 유효성을 검사할 입력 모든 통화 기호를 포함할 수 없습니다. 이러한 기호가 있으면 잘못 된 입력을 표시 하기 위해 CompareValidator 발생 합니다. 반면 편집 인터페이스의 통화 기호를 현재에 `UnitPrice` TextBox, 즉 사용자 자신의 변경 내용을 저장 하기 전에 통화 기호를 명시적으로 제거 해야 합니다. 이 해결 하는 세 가지 옵션이 있습니다.

1. 구성 합니다 `EditItemTemplate` 있도록는 `UnitPrice` 통화로 텍스트 값의 서식을 지정 하지 않습니다.
2. CompareValidator를 제거 하 고 올바르게 형식이 지정 된 통화 값을 확인 하는 RegularExpressionValidator로 바꿔 여 통화 기호를 입력 하는 사용자를 허용 합니다. 여기서 통화 값의 유효성을 검사 하는 정규식을 간단 하 게 CompareValidator는 및에 방문 하셔서 문화권 설정을 통합 하는 경우 코드를 작성 해야 합니다.
3. 유효성 검사 컨트롤을 완전히 제거 하 고 GridView에서 사용자 지정 서버 쪽 유효성 검사 논리에 의존 `RowUpdating` 이벤트 처리기입니다.

이 자습서에 대 한 옵션 1 사용 하 여 이동 s 수 있습니다. 현재는 `UnitPrice` 의 텍스트 상자에 대 한 데이터 바인딩 식으로 인해 통화 값으로 형식이 합니다 `EditItemTemplate`: `<%# Eval("UnitPrice", "{0:c}") %>`합니다. 변경 된 `Eval` 문을 `Eval("UnitPrice", "{0:n2}")`, 자릿수 두 자리 숫자로 결과 형식을 지정 합니다. 선언적 구문을 통해 직접 또는에서 데이터 바인딩 편집 링크를 클릭 하 여이 수행할 수 있습니다 합니다 `UnitPrice` DataList의 텍스트 `EditItemTemplate`합니다.

이 변경으로 편집 인터페이스에 형식이 지정 된 가격 그룹 구분 기호로 쉼표와 마침표는 소수 구분 기호로 포함 되지만 통화 기호를 해제 합니다.

> [!NOTE]
> 통화 형식은 편집할 수 있는 인터페이스에서 제거 하는 경우 필자 도움이 될 텍스트 외부 텍스트로 통화 기호를 배치 하. 이 통화 기호를 제공 하는 필요 하지 않은 사용자에 대 한 힌트로 사용 됩니다.


## <a name="fixing-the-cancel-button"></a>취소 단추를 수정합니다.

기본적으로 유효성 검사 웹 컨트롤 클라이언트 쪽에서 유효성 검사를 수행 하는 JavaScript를 내보냅니다. 단추나 LinkButton, ImageButton 클릭 하면 포스트백이 발생 하기 전에 페이지에서 유효성 검사 컨트롤 클라이언트 쪽에서 확인 됩니다. 잘못 된 데이터를 다시 게시 취소 되었습니다. 특정 단추에 대 한 그러나 데이터의 유효성을 검사 않을 재료; 이러한 경우 잘못 된 데이터로 인해 취소 포스트백 하는 것을 가장 쓸데 없는 존재 합니다.

취소 단추에는 예입니다. 사용자의 제품 이름을 생략 하는 등의 잘못 된 데이터를 입력 한 다음 결정 그녀는 대상이 t 하려는 제품을 모두 저장 및 취소 단추를 누를 한다고 가정 합니다. 현재 [취소] 단추는 제품 이름이 누락 되었고 다시 게시 되지 않도록 보고서 페이지에서 유효성 검사 컨트롤을 트리거합니다. 사용자가 일부 텍스트를 입력 해야 합니다 `ProductName` 만 편집 프로세스를 취소 하려면 텍스트 상자에 붙여넣습니다.

단추를 LinkButton 및 ImageButton 다행히도 해야는 [ `CausesValidation` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.causesvalidation.aspx) 수를 나타내는 클릭 여부 단추는 유효성 검사 논리를 시작 해야 (기본값으로 `True`). 취소 단추 s 설정할 `CausesValidation` 속성을 `False`입니다.

## <a name="ensuring-the-inputs-are-valid-in-the-updatecommand-event-handler"></a>올바른 UpdateCommand 이벤트 처리기는 입력 확인

클라이언트 쪽 스크립트 유효성 검사 컨트롤에서 내보낸 인해 사용자가 잘못 된 입력을 입력 유효성 검사 컨트롤이 취소 단추를 LinkButton으로 시작 된 모든 포스트백 또는 ImageButton 컨트롤 `CausesValidation` 속성은 `True` ( 기본값)입니다. 그러나 JavaScript 지원 비활성화 된 하나 또는 브라우저를 사용 하 여 사용자가 방문 하는 경우의 클라이언트 쪽 유효성 검사가 실행 되지 않습니다.

ASP.NET 유효성 검사 컨트롤의 모든 포스트백 되는 즉시 해당 유효성 검사 논리를 반복 하 고 보고서를 통해 페이지의 입력의 전체 유효성을 검사 합니다 [ `Page.IsValid` 속성](https://msdn.microsoft.com/library/system.web.ui.page.isvalid.aspx)합니다. 그러나 페이지 흐름 중단 되거나 되지 방식으로 값을 기반으로 모든 중지 `Page.IsValid`합니다. 개발자로 서는 확인 해야 하는 것은 `Page.IsValid` 속성의 값이 `True` 입력 데이터를 잘못 가정 하는 코드를 사용 하 여 계속 진행 하기 전에 합니다.

사용자가 JavaScript를 사용 하지 않도록 설정 하는 경우이 페이지를 방문, 제품을 편집가 너무의 가격 값을 입력 저렴 하 고, [업데이트] 단추를 클릭 하면 클라이언트 쪽 유효성 검사를 건너뛰며 및 포스트백 계속 될 것 이라고 합니다. ASP.NET 페이지가 포스트백 될 때 `UpdateCommand` 이벤트 처리기를 실행 하 고 너무 구문 분석 하려고 할 때 예외가 발생 하는 데 비용이 많이 드는 `Decimal`합니다. 예외 처리 했으므로, 이러한 예외를 정상적으로 처리할 수는 있지만 처음에 사용 하 여 계속 진행 함으로써 통해 지연에서 잘못 된 데이터를 처리할 수 있도록 합니다 `UpdateCommand` 이벤트 처리기 경우 `Page.IsValid` 의 값이 `True`합니다.

시작 부분에 다음 코드를 추가 합니다 `UpdateCommand` 이벤트 처리기 바로 앞의 `Try` 블록:


[!code-csharp[Main](adding-validation-controls-to-the-datalist-s-editing-interface-cs/samples/sample2.cs)]

이 또한이를 사용 하 여 제품 제출 된 데이터가 유효한 경우에 업데이트 하려고 합니다. T-이득 대부분의 사용자 유효성 검사 컨트롤 클라이언트 쪽 스크립트,으로 인해 잘못 된 데이터에 다시 게시 수 있지만 사용자가 해당 브라우저 JavaScript 지원 하지 또는 지원 되는 JavaScript가 클라이언트 쪽 검사를 무시 하 고 잘못 된 데이터를 제출할 사용 하지 않도록 설정 합니다.

> [!NOTE]
> 예리한 독자는 이전에 설명한 대로 GridView를 사용 하 여 데이터를 업데이트 하는 경우에서는 동작 t를 명시적으로 확인 해야 합니다.는 `Page.IsValid`의 페이지 코드 숨김 클래스에서는 속성입니다. GridView 참조 이므로이 `Page.IsValid` 속성 및 값을 반환 하는 경우에 업데이트를 사용 하 여 진행만 `True`합니다.


## <a name="step-3-summarizing-data-entry-problems"></a>3 단계: 데이터 입력 문제 요약

ASP.NET 5 유효성 검사 컨트롤 외에도 포함 합니다 [ValidationSummary 컨트롤](https://msdn.microsoft.com/library/f9h59855(VS.80).aspx), 표시는 `ErrorMessage` 잘못 된 데이터가 검색 되는 유효성 검사 컨트롤의. 웹 페이지 또는 모달, 클라이언트 쪽 messagebox를 통해 텍스트로이 요약 데이터를 표시할 수 있습니다. 가 유효성 검사 문제를 요약 하는 클라이언트 쪽 messagebox를 포함 하려면이 자습서를 향상 시킬 수 있습니다.

이렇게 하려면 디자이너 도구 상자에서 ValidationSummary 컨트롤을 끕니다. ValidationSummary 컨트롤 만들어지고 t 위치의 중요 messagebox로 요약만 표시 하도록 구성 하려는 다시 이후로. 컨트롤을 추가한 후 설정 해당 [ `ShowSummary` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showsummary(VS.80).aspx) 하 `False` 고 [ `ShowMessageBox` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showmessagebox(VS.80).aspx) 에 `True`입니다. 이 또한을 사용 하 여 유효성 검사 오류는 클라이언트 쪽 messagebox에 요약 되어 (그림 6 참조).


[![유효성 검사 오류는 클라이언트 쪽 Messagebox에 요약 되어 있습니다.](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image17.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image16.png)

**그림 6**: 유효성 검사 오류는 클라이언트 쪽 Messagebox에 요약 되어 있습니다 ([큰 이미지를 보려면 클릭](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image18.png))


## <a name="summary"></a>요약

이 자습서에서 사전 업데이트 워크플로에서 사용 하기 전에 사용자 입력이 유효한 지를 확인 하려면 유효성 검사 컨트롤을 사용 하 여 예외 발생 가능성을 줄이는 방법에 살펴보았습니다. ASP.NET는 특정 웹을 검사 하도록 설계 된 다섯 개의 유효성 검사 웹 컨트롤 제어 s 입력 및 입력된 s 유효성에 다시 보고를 제공 합니다. 이 자습서에서는 사용 했습니다 이러한 다섯 개의 컨트롤의 두는 RequiredFieldValidator 및 CompareValidator의 제품 이름을 제공한 했으며 가격 보다 크거나 0 값을 사용 하 여 통화 형식을 있는지 확인 합니다.

DataList s 편집 인터페이스에 유효성 검사 컨트롤을 추가 하는 것이를 끌어 만큼 간단 합니다 `EditItemTemplate` 선택 하 고 일련의 속성을 설정 합니다. 기본적으로 유효성 검사 컨트롤이 자동으로 내보내기 클라이언트 쪽 유효성 검사 스크립트입니다. 또한 서버 쪽 유효성 검사의 누적 결과 저장 포스트백에서 제공 된 `Page.IsValid` 속성. 설정 단추 s에 단추나 LinkButton, ImageButton 클릭 하면 클라이언트 쪽 유효성 검사를 무시 하려면 `CausesValidation` 속성을 `False`입니다. 또한 포스트백에 제출 된 데이터를 사용 하 여 모든 작업을 수행 하기 전에 있는지를 확인 합니다 `Page.IsValid` 속성이 반환 `True`합니다.

모든 자습서 편집 DataList에서는 지금 검사 ve s 제품 이름에 대 한 텍스트 상자와 다른 가격에 대 한 매우 간단한 편집 인터페이스 했습니다. 그러나 편집 인터페이스, Dropdownlist, 달력, 라디오 단추, 확인란, 등과 같은 다양 한 웹 컨트롤의 혼합을 포함할 수 있습니다. 다음 자습서는 다양 한 웹 컨트롤을 사용 하는 인터페이스를 구축 하는 방법을 살펴보겠습니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Dennis Patterson, Ken Pespisa 및 Liz Shulok 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](handling-bll-and-dal-level-exceptions-cs.md)
> [다음](customizing-the-datalist-s-editing-interface-cs.md)
