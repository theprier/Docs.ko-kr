---
uid: web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-gridview-control-cs
title: GridView 컨트롤 (C#)에서 TemplateFields 사용 | Microsoft Docs
author: rick-anderson
description: GridView는 유연성을 제공 하도록 템플릿을 사용 하 여 렌더링 하는 templatefield로 제공 합니다. 템플릿을 다양 한 정적 HTML 웹 컨트롤을 포함할 수 있습니다 및...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 11de31e8-a78a-4f96-bd75-66e994175902
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-gridview-control-cs
msc.type: authoredcontent
ms.openlocfilehash: fe84bd24824f4a0326a6e8d41c0d291c7ef585af
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37363833"
---
<a name="using-templatefields-in-the-gridview-control-c"></a>GridView 컨트롤 (C#)에서 TemplateFields 사용
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_12_CS.exe) 또는 [PDF 다운로드](using-templatefields-in-the-gridview-control-cs/_static/datatutorial12cs1.pdf)

> GridView는 유연성을 제공 하도록 템플릿을 사용 하 여 렌더링 하는 templatefield로 제공 합니다. 템플릿으로 혼합을 포함할 수 있습니다 정적 html 웹 컨트롤 및 데이터 바인딩 구문입니다. 이 자습서를 templatefield로 더 높은 수준의 GridView 컨트롤을 사용 하 여 사용자 지정을 위해 사용 하는 방법을 살펴보겠습니다.


## <a name="introduction"></a>소개

GridView에서 속성을 나타내는 필드의 집합으로 구성 되는 `DataSource` 데이터를 표시 하는 방법을 함께 렌더링된 된 출력에 포함 되도록 합니다. 가장 간단한 필드 형식이 BoundField 데이터 값을 텍스트로 표시 합니다. 다른 필드 형식 대체 HTML 요소를 사용 하 여 데이터를 표시 합니다. 확인란의 선택된 상태가 지정 된 데이터 필드를 값에 따라 달라 집니다 CheckBoxField, 예를 들어, 렌더링 이미지 필드는 이미지 소스가 지정 된 데이터 필드를 기반으로 이미지를 렌더링 합니다. 하이퍼링크 및 단추는 기본 데이터 필드 값에 따라 달라 집니다 상태가 HyperLinkField 및 ButtonField 필드 형식을 사용 하 여 렌더링할 수 있습니다.

CheckBoxField, 이미지 필드, HyperLinkField, 및 ButtonField 필드 형식 데이터의 대체 보기를 허용 하는 동안 여전히는 서식 지정에 대해 상당히 제한적입니다. CheckBoxField 이미지 필드는 단일 이미지를 표시할 수 있지만 하나의 확인란을 표시할 수 있습니다. 특정 필드를 일부 텍스트를 checkbox를 표시 해야 하는 경우에 어떻게 *고* 이미지를 다른 데이터 필드 값에 따라 모든? 또는 확인란, 이미지, 하이퍼링크 또는 단추 이외의 웹 컨트롤을 사용 하 여 데이터를 표시 하려고 한다고 될까요? 또한는 BoundField 단일 데이터 필드에 해당 표시를 제한합니다. 단일 GridView 열에 두 개 이상의 데이터 필드 값을 표시 하려면 어떻게 해야 할까요?

GridView이이 정도의 융통성을 수용 하기 위해 사용 하 여 렌더링 하는 templatefield로 제공 된 *템플릿*합니다. 템플릿으로 혼합을 포함할 수 있습니다 정적 html 웹 컨트롤 및 데이터 바인딩 구문입니다. 또한를 templatefield로 다양 한 템플릿 다양 한 상황에 대 한 렌더링을 사용자 지정 하는 데 사용할 수 있는 있습니다. 예를 들어 합니다 `ItemTemplate` 기본적으로 각 행에 대 한 셀을 렌더링 하는 데 사용 됩니다 있지만 `EditItemTemplate` 템플릿을 사용 하 여 데이터를 편집 하는 경우에 인터페이스를 사용자 지정할 수 있습니다.

이 자습서를 templatefield로 더 높은 수준의 GridView 컨트롤을 사용 하 여 사용자 지정을 위해 사용 하는 방법을 살펴보겠습니다. 에 [이전 자습서](custom-formatting-based-upon-data-cs.md) 서식을 사용 하 여 기본 데이터에 따라 사용자 지정 하는 방법에 살펴보았습니다 합니다 `DataBound` 및 `RowDataBound` 이벤트 처리기입니다. 또 다른 방법은 기반으로 기본 데이터 형식 사용자 지정 서식 템플릿 내에서 메서드를 호출 하 여 합니다. 살펴보겠습니다이 기술은이 자습서도 있습니다.

이 자습서에 대 한 직원 목록의 모양을 사용자 지정할 TemplateFields 사용 됩니다. 에서는 모든 직원을 나열 됩니다 있지만 직원의 표시 됩니다 특히 하나의 열, 고용 날짜는 달력 컨트롤 및 기간 (일)는 한 채택 되었습니다 회사의 여부를 나타내는 상태 열에서 첫 번째 및 마지막 이름입니다.


[![세 TemplateFields는 표시를 사용자 지정 하는 데 사용 됩니다.](using-templatefields-in-the-gridview-control-cs/_static/image2.png)](using-templatefields-in-the-gridview-control-cs/_static/image1.png)

**그림 1**: 세 TemplateFields는 표시를 사용자 지정 하는 데 사용 됩니다 ([큰 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image3.png))


## <a name="step-1-binding-the-data-to-the-gridview"></a>1 단계: GridView에 데이터 바인딩

Reporting TemplateFields 모양을 사용자 지정 하는 데 필요한 시나리오에서 찾을 수 있습니까 가장 먼저 BoundFields만을 포함 하는 GridView 컨트롤을 만들어 시작 하기 쉬운 새 TemplateFields를 추가 하거나를 기존 BoundFields 변환한 다음 필요에 따라 TemplateFields 합니다. 따라서 먼저이 자습서 디자이너를 통해 페이지에 GridView를 추가 및 직원의 목록을 반환 하는 ObjectDataSource에 바인딩. 이러한 단계는 employee 필드에 대해 BoundFields로 GridView를 만듭니다.

열기는 `GridViewTemplateField.aspx` 페이지 및 디자이너 도구 상자에서 GridView를 끕니다. GridView의 스마트 태그에서 호출 하는 새 ObjectDataSource 컨트롤을 추가 하려면 선택 합니다 `EmployeesBLL` 클래스의 `GetEmployees()` 메서드.


[![GetEmployees() 메서드를 호출 하 여 새 ObjectDataSource 컨트롤 추가](using-templatefields-in-the-gridview-control-cs/_static/image5.png)](using-templatefields-in-the-gridview-control-cs/_static/image4.png)

**그림 2**: 해당 Invoke 새 ObjectDataSource 컨트롤을 추가 합니다 `GetEmployees()` 메서드 ([클릭 하 여 큰 이미지 보기](using-templatefields-in-the-gridview-control-cs/_static/image6.png))


GridView이 방식으로 바인딩을 자동으로 추가 됩니다을 BoundField 각 직원 속성에 대해: `EmployeeID`, `LastName`, `FirstName`, `Title`를 `HireDate`를 `ReportsTo`, 및 `Country`합니다. 이 보고서에 대 한 보겠습니다 문제 되지를 표시 하는 `EmployeeID`, `ReportsTo`, 또는 `Country` 속성입니다. 이러한 BoundFields를 제거 하려면 다음을 수행할 수 있습니다.

- GridView의 스마트 태그에서 열 편집 링크 필드 대화 상자를 클릭 하를 사용 하 여이 대화 상자를 표시 합니다. 다음으로, 선택 왼쪽 아래에서 BoundFields 나열 하 고 빨간색 X를 클릭 합니다 BoundField 제거할 단추입니다.
- 소스 뷰에서 GridView의 선언적 구문을 수동으로 편집, 삭제는 `<asp:BoundField>` 요소를 제거 하려면 BoundField입니다.

제거한 후는 `EmployeeID`, `ReportsTo`, 및 `Country` BoundFields를 GridView의 태그와 같습니다.


[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample1.aspx)]

시간을 내어 브라우저에서 진행 상황을 보고 합니다. 이 시점에서 각 직원 및 네 개의 열을 레코드가 포함 된 테이블을 볼 수 있습니다: 직원의 성, 이름, 직함에 대 한 하나 및 입사 날짜에 하나 하나입니다.


[![LastName, FirstName, 제목 및 HireDate 필드는 각 직원에 대 한 표시 됩니다.](using-templatefields-in-the-gridview-control-cs/_static/image8.png)](using-templatefields-in-the-gridview-control-cs/_static/image7.png)

**그림 3**: 합니다 `LastName`를 `FirstName`, `Title`, 및 `HireDate` 각 직원에 대 한 필드가 표시 됩니다 ([클릭 하 여 큰 이미지 보기](using-templatefields-in-the-gridview-control-cs/_static/image9.png))


## <a name="step-2-displaying-the-first-and-last-names-in-a-single-column"></a>2 단계: 단일 열에 첫 번째 이름과 마지막 이름 표시

각 직원의 현재 성 별도 열에 표시 됩니다. 대신 단일 열으로 결합할 수 좋을 수 있습니다. 이렇게 하려면 templatefield로 사용 해야 합니다. 수 중 하나를 새 TemplateField 추가, 데이터 바인딩 구문을 확인 하 고 필요한 태그를 추가 하 고 삭제 합니다 `FirstName` 및 `LastName` BoundFields, 또는에서는 변환할 수는 `FirstName` BoundField를 TemplateField로 포함 하도록 TemplateField 편집 합니다 `LastName` 값을 복사한 다음 제거를 `LastName` BoundField 합니다.

두 방법 모두 동일한 결과 net 있지만 개인적으로 필자는 변환이 자동으로 추가 하기 때문에 가능 하면 TemplateFields BoundFields 변환할를 `ItemTemplate` 고 `EditItemTemplate` 웹 컨트롤 및 다른 모양은 모방 하는 데이터 바인딩 구문을 사용 하 여 및를 BoundField의 기능을 추가 합니다. 장점은 적은 작업을 수행 하는 templatefield로 변환 프로세스를 수행한 일부 작업에 따라이 필요 했습니다.

기존 BoundField templatefield로 변환할 필드 대화 상자를 불러오는 GridView의 스마트 태그에서 열 편집 링크를 클릭 합니다. 왼쪽된 아래 모서리에 있는 목록에서 변환 하 고 오른쪽 아래 모서리에서 "이이 필드를 TemplateField로 변환" 링크를 클릭 하 여 BoundField를 선택 합니다.


[![BoundField 필드 대화 상자에서를 TemplateField로 변환](using-templatefields-in-the-gridview-control-cs/_static/image11.png)](using-templatefields-in-the-gridview-control-cs/_static/image10.png)

**그림 4**: 필드 대화 상자에서 BoundField에를 templatefield로 변환 ([큰 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image12.png))


계속 해 서 변환 된 `FirstName` BoundField를 TemplateField로 합니다. 이 변경 후 차이가 perceptive 디자이너에서 합니다. BoundField의 모양과 느낌을 유지 하는 TemplateField 만듭니다는 BoundField templatefield로 변환 때문입니다. 이 변환 프로세스는 BoundField의 선언적 구문-있을 visual 차이가 없습니다이 시점에서 디자이너에도 불구 하 고 대체 `<asp:BoundField DataField="FirstName" HeaderText="FirstName" SortExpression="FirstName" />` -다음 TemplateField 구문을 사용 하 여:


[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample2.aspx)]

알 수 있듯이 templatefield로 두 개의 템플릿으로 구성 됩니다는 `ItemTemplate` 레이블이 있는 해당 `Text` 속성의 값으로 설정 되는 `FirstName` 데이터 필드 및 `EditItemTemplate` 컨트롤 텍스트 상자를 사용 하 여 `Text` 속성도 설정 됩니다 에 `FirstName` 데이터 필드입니다. 데이터 바인딩 구문을- `<%# Bind("fieldName") %>` -나타내는 데이터 필드 *`fieldName`* 는 지정 된 웹 컨트롤 속성에 바인딩됩니다.

추가할 합니다 `LastName` 데이터 필드 값을 다른 레이블 웹 컨트롤을 추가 해야이 TemplateField 합니다 `ItemTemplate` 바인딩하고 해당 `Text` 속성을 `LastName`. 이 디자이너를 통해 또는 수동으로 수행할 수 있습니다. 그렇게 하려면 수동으로 추가 하는 적절 한 선언적 구문을 `ItemTemplate`:


[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample3.aspx)]

디자이너를 통해 추가, GridView의 스마트 태그에서 템플릿 편집 링크를 클릭 합니다. GridView의 템플릿 편집 인터페이스를 표시 됩니다. 이 인터페이스의 스마트 태그는 GridView의 템플릿 목록입니다. 있으므로 하나의 TemplateField이 시점에 드롭다운 목록에 나열 된 템플릿은 해당 템플릿에 대 한 합니다 `FirstName` 함께 TemplateField 합니다 `EmptyDataTemplate` 및 `PagerTemplate`합니다. 합니다 `EmptyDataTemplate` 서식 파일을 지정 하는 경우는 GridView;에 바인딩된 데이터의 이상 결과가 없는 경우 GridView의 출력을 렌더링 하는 `PagerTemplate`지정한 경우 페이징을 지원 되는 GridView에 대 한 페이징 인터페이스를 렌더링 하는 데 사용 됩니다.


[![GridView의 템플릿 디자이너를 통해 편집할 수 있습니다.](using-templatefields-in-the-gridview-control-cs/_static/image14.png)](using-templatefields-in-the-gridview-control-cs/_static/image13.png)

**그림 5**: GridView의 템플릿 수 수 편집을 통해 the 디자이너 ([큰 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image15.png))


도 표시할 합니다 `LastName` 에 `FirstName` TemplateField 도구에서 레이블 컨트롤을 끌어를 `FirstName` TemplateField의 `ItemTemplate` gridview에서의 템플릿 편집 인터페이스.


[![FirstName TemplateField의 ItemTemplate에 레이블 웹 컨트롤 추가](using-templatefields-in-the-gridview-control-cs/_static/image17.png)](using-templatefields-in-the-gridview-control-cs/_static/image16.png)

**그림 6**: 레이블 웹 컨트롤을 추가 합니다 `FirstName` TemplateField의 ItemTemplate ([클릭 하 여 큰 이미지 보기](using-templatefields-in-the-gridview-control-cs/_static/image18.png))


이 시점에서 templatefield로 추가 레이블 웹 컨트롤에 해당 `Text` 속성이 "Label"로 설정 합니다. 이 속성의 값에 바인딩되어 있으므로이 변경 해야 합니다 `LastName` 데이터 필드를 대신 합니다. 레이블 컨트롤의 스마트 태그를이 클릭이 수행 및 데이터 바인딩 편집 옵션을 선택 합니다.


[![레이블의 스마트 태그에서 편집 데이터 바인딩 옵션을 선택 합니다.](using-templatefields-in-the-gridview-control-cs/_static/image20.png)](using-templatefields-in-the-gridview-control-cs/_static/image19.png)

**그림 7**: 레이블의 스마트 태그에서 데이터 바인딩 편집 옵션을 선택 ([큰 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image21.png))


DataBindings 대화 상자가 표시 됩니다. 여기에서 왼쪽 목록에서 데이터 바인딩에 참여 하 고 오른쪽의 드롭다운 목록에서 데이터를 바인딩할 필드를 선택 합니다. 속성을 선택할 수 있습니다. 선택 합니다 `Text` 왼쪽에서 속성 및 `LastName` 오른쪽에서 필드를 클릭 합니다.


[![LastName 데이터 필드에 Text 속성 바인딩](using-templatefields-in-the-gridview-control-cs/_static/image23.png)](using-templatefields-in-the-gridview-control-cs/_static/image22.png)

**그림 8**: 바인딩하는 `Text` 속성을 합니다 `LastName` 데이터 필드 ([클릭 하 여 큰 이미지 보기](using-templatefields-in-the-gridview-control-cs/_static/image24.png))


> [!NOTE]
> DataBindings 대화 상자를 사용 하면 양방향 데이터 바인딩을 수행할지 여부를 나타낼 수 있습니다. 두면이 옵션을 선택 취소 하는 경우 데이터 바인딩 구문을 `<%# Eval("LastName")%>` 대신 사용할 `<%# Bind("LastName")%>`합니다. 이 자습서에 대 한 어느 방법이 든 괜찮습니다. 양방향 데이터 바인딩은 삽입 하 고 데이터를 편집 하는 경우 중요 합니다. 그러나 단순히 데이터를 표시, 어느 방법이 든 작동 원활 하 게 합니다. 이후 자습서에서 자세히 양방향 데이터 바인딩을 하겠습니다.


브라우저를 통해이 페이지를 보려면 잠시 시간이 소요 됩니다. GridView 여전히 네 개의 열을 포함 알 수 있듯이 그러나 합니다 `FirstName` 열이 나열 됩니다 *둘 다* 는 `FirstName` 및 `LastName` 데이터 필드 값입니다.


[![FirstName 및 LastName 값을 모두 단일 열에 표시 됩니다.](using-templatefields-in-the-gridview-control-cs/_static/image26.png)](using-templatefields-in-the-gridview-control-cs/_static/image25.png)

**그림 9**: 모두는 `FirstName` 하 고 `LastName` 값은 단일 열에 표시 됩니다 ([클릭 하 여 큰 이미지 보기](using-templatefields-in-the-gridview-control-cs/_static/image27.png))


이 첫 번째 단계를 완료 하려면 제거 합니다 `LastName` BoundField 및 이름 바꾸기는 `FirstName` TemplateField의 `HeaderText` 속성 "Name"을 합니다. 이러한 변경 된 후 GridView의 선언적 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample4.aspx)]


[![각 직원의 첫 번째 및 마지막 이름을 하나의 열에 표시 됩니다.](using-templatefields-in-the-gridview-control-cs/_static/image29.png)](using-templatefields-in-the-gridview-control-cs/_static/image28.png)

**그림 10**: 각 직원의 첫 번째 및 마지막 이름을 하나의 열에 표시 됩니다 ([큰 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image30.png))


## <a name="step-3-using-the-calendar-control-to-display-thehireddatefield"></a>3 단계: 표시할 달력 컨트롤을 사용 하 여`HiredDate`필드

GridView에 텍스트로 데이터 필드 값을 표시 하는 것은 BoundField를 사용 하는 것으로 간단 합니다. 그러나 특정 시나리오에 대 한 데이터를 가장 잘 표현 됩니다만 텍스트 대신 특정 웹 컨트롤을 사용 하 여. 이러한 사용자 지정 데이터 표시의 TemplateFields를 사용 하 여 가능 합니다. 예를 들어 대신 직원의 고용 날짜를 텍스트로 표시 하는 보다 수 살펴보겠습니다 일정 (사용 하 여 [달력 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar(VS.80).aspx)) 고용 날짜를 사용 하 여 강조 표시 합니다.

이를 위해 변환 하 여 시작 된 `HiredDate` BoundField를 TemplateField로 합니다. GridView의 스마트 태그에 이동한 단순히 필드 대화 상자를 불러오는 열 편집 링크를 클릭 합니다. 선택 된 `HiredDate` BoundField 및 클릭 "변환"이이 필드를 TemplateField로 합니다.


[![HiredDate BoundField templatefield로 변환](using-templatefields-in-the-gridview-control-cs/_static/image32.png)](using-templatefields-in-the-gridview-control-cs/_static/image31.png)

**그림 11**: 변환 된 `HiredDate` 를 TemplateField로 BoundField ([클릭 하 여 큰 이미지 보기](using-templatefields-in-the-gridview-control-cs/_static/image33.png))


2 단계에서에서 보았듯이이 바꿉니다는 BoundField templatefield로 포함 하는 `ItemTemplate` 및 `EditItemTemplate` 레이블과 텍스트 상자를 사용 하 여 해당 `Text` 바인딩할 속성을를 `HiredDate` 데이터바인딩구문을사용하여값`<%# Bind("HiredDate")%>`.

달력 컨트롤을 사용 하 여 텍스트를 바꾸려면 레이블을 제거 하 고 달력 컨트롤을 추가 하 여 템플릿을 편집 합니다. 디자이너에서 GridView의 스마트 태그에서 템플릿 편집을 선택 하 고 선택 합니다 `HireDate` TemplateField의 `ItemTemplate` 드롭 다운 목록에서. 그런 다음 레이블 컨트롤을 삭제 하 고 템플릿 편집 인터페이스에 도구 상자에서 달력 컨트롤을 끌어.


[![달력 컨트롤을 추가 합니다 TemplateField의 ItemTemplate HireDate](using-templatefields-in-the-gridview-control-cs/_static/image35.png)](using-templatefields-in-the-gridview-control-cs/_static/image34.png)

**그림 12**: 달력 컨트롤을 추가 합니다 `HireDate` TemplateField의 `ItemTemplate` ([클릭 하 여 큰 이미지 보기](using-templatefields-in-the-gridview-control-cs/_static/image36.png))


GridView의 각 행은 달력 컨트롤을을 포함 하는 시점에서 해당 `HiredDate` TemplateField 합니다. 그러나 직원의 실제 `HiredDate` 값을 현재 월 및 날짜를 보여 주는 기본값으로 각 달력 컨트롤을 일으키는 달력 컨트롤에서 아무 곳 이나 설정 하지 않으면. 이 문제를 해결 하려면 각 직원의 할당 해야 `HiredDate` 달력 컨트롤의 [SelectedDate](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selecteddate(VS.80).aspx) 하 고 [VisibleDate](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.visibledate(VS.80).aspx) 속성입니다.

달력 컨트롤의 스마트 태그에서 데이터 바인딩 편집을 선택 합니다. 다음으로, 둘 다를 바인딩할 `SelectedDate` 하 고 `VisibleDate` 속성을는 `HiredDate` 데이터 필드입니다.


[![SelectedDate 속성과 VisibleDate HiredDate 데이터 필드에 바인딩](using-templatefields-in-the-gridview-control-cs/_static/image38.png)](using-templatefields-in-the-gridview-control-cs/_static/image37.png)

**그림 13**: 바인딩하는 `SelectedDate` 하 고 `VisibleDate` 속성을를 `HiredDate` 데이터 필드 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image39.png))


> [!NOTE]
> 달력 컨트롤의 선택한 날짜 반드시 표시 되지 않아도 됩니다. 예를 들어, 달력 월 1 일 있을<sup>st</sup>, 선택한 날짜로 1999 있지만 현재 월 및 연도가 표시 됩니다. 선택한 날짜와 표시 날짜는 달력 컨트롤의 지정 된 `SelectedDate` 고 `VisibleDate` 속성입니다. 것 이므로 모두 선택 사원의 `HiredDate` 바인딩해야 하는 두 가지이 속성을 모두 표시 되 고 있는지 확인 합니다 `HireDate` 데이터 필드.


브라우저에서 페이지 보기, 달력 이제 직원의 고용 된 날짜의 월을 표시 하 고 해당 특정 날짜를 선택 합니다.


[![직원의 HiredDate Calendar 컨트롤에 표시 됩니다.](using-templatefields-in-the-gridview-control-cs/_static/image41.png)](using-templatefields-in-the-gridview-control-cs/_static/image40.png)

**그림 14**: The 직원 `HiredDate` Calendar 컨트롤에 표시 됩니다 ([클릭 하 여 큰 이미지 보기](using-templatefields-in-the-gridview-control-cs/_static/image42.png))


> [!NOTE]
> 지금까지 살펴본 모든 예제에서는 달리이 자습서에서는 수행한 *되지* 설정 `EnableViewState` 속성을 `false` 이 GridView에 대 한 합니다. 그 이유 달력 컨트롤의 날짜를 클릭 하면 포스트백, 클릭 누계 선택한 날짜를 설정 하는 때문입니다. 그러나 GridView의 뷰 상태를 사용 하지 않도록 설정 하는 경우 다시 게시할 때마다 GridView의 데이터는 다시 바인딩 해 서 설정할 일정의 선택한 날짜는 해당 기본 데이터 원본 *다시* 은 직원에 게 `HireDate`덮어쓰기를, 사용자가 선택한 날짜입니다.


이 자습서는 이론에 불과합니다 토론 사용자는 직원의 업데이트할 수 없기 때문 `HireDate`합니다. 해당 날짜를 선택할 수 없는 있도록 달력 컨트롤을 구성 하는 가장 좋은 형태일 것입니다. 하지만이 자습서는 일부 상황에서 뷰 상태 수 있어야 특정 기능을 제공 하기 위해 보여줍니다.

## <a name="step-4-showing-the-number-of-days-the-employee-has-worked-for-the-company"></a>4 단계: 회사에 근무 한 일 수를 보여 주는

지금까지 TemplateFields의 두 응용 프로그램을 살펴보았습니다.

- 하나의 열에 두 개 이상의 데이터 필드 값을 결합 하 고
- 텍스트 대신 웹 컨트롤을 사용 하 여 데이터 필드 값 표현

세 번째 TemplateFields 사용 하는 기본 데이터 GridView의에 대 한 메타 데이터를 표시 합니다. 직원의 고용 날짜를 표시할 뿐만 아니라 예를 들어에서는 수도 작업에서 사용 되어 왔습니다 총 일 수를 표시 하는 열.

아직 기본 데이터 형식으로 데이터베이스에 저장 된 것 보다 웹 페이지 보고서에 다르게 표시 되도록 해야 할 때 다른 TemplateFields 사용 시나리오에서 발생 합니다. imagine 합니다 `Employees` 테이블을 `Gender` 문자를 저장 하는 필드 `M` 또는 `F` 직원의 성별을 나타내기 위해. 웹 페이지에서이 정보를 표시 하는 경우에 "Male" 또는 "Female", "M" 또는 "F" 뿐 아니라 성별을 표시 하고자 수 있습니다.

만들어 두이 시나리오 모두를 처리할 수 있습니다는 *형식 지정 메서드에* ASP.NET 페이지의 코드 숨김 클래스에서 (또는 구현으로 별도 클래스 라이브러리에는 `static` 메서드) 템플릿에서 호출 되는 합니다. 이러한 형식 지정 메서드는 이전에 표시 하는 동일한 데이터 바인딩 구문을 사용 하 여 템플릿에서 호출 됩니다. 형식 지정 메서드가 임의 개수의 매개 변수를 가져올 수 있지만 문자열을 반환 해야 합니다. 이 반환 되는 문자열은 HTML을 템플릿에 삽입 됩니다.

이 개념을 설명 하 총 작업에는 직원의 근무 하는 일 수를 나열 하는 열을 표시 하려면이 자습서를 확장 해 보겠습니다. 이 형식 지정 메서드가 놓여질를 `Northwind.EmployeesRow` 개체 및 직원 문자열로 채택 되었습니다 일 수를 반환 합니다. 이 메서드는 ASP.NET 페이지의 코드 숨김 클래스에 추가할 수 있습니다 하지만 *해야 합니다* 로 표시 되어야 `protected` 또는 `public` 템플릿에서 액세스할 수 있도록 합니다.


[!code-csharp[Main](using-templatefields-in-the-gridview-control-cs/samples/sample5.cs)]

하므로 합니다 `HiredDate` 필드에 포함 될 수 있습니다 `NULL` 데이터베이스 값 값 아님을 먼저 확인 해야 합니다 `NULL` 계산을 사용 하 여 계속 진행 하기 전에 합니다. 경우는 `HiredDate` 값이 `NULL`, 없는 경우 단순히 문자열 "Unknown"; 반환 `NULL`, 현재 시간 사이의 차이 계산 및 `HiredDate` 값 및 일 수를 반환 합니다.

이 메서드를 활용 하는 데이터 바인딩 구문을 사용 하 여 gridview에서를 TemplateField에서 호출 해야 합니다. GridView의 스마트 태그에서 열 편집 링크를 클릭 하 고 새 templatefield로 추가 하 여 새 templatefield로 GridView에 추가 하 여 시작 합니다.


[![GridView에 새 templatefield로 추가](using-templatefields-in-the-gridview-control-cs/_static/image44.png)](using-templatefields-in-the-gridview-control-cs/_static/image43.png)

**그림 15**: GridView를 새 TemplateField 추가할 ([큰 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image45.png))


이 새 templatefield로 설정 `HeaderText` "의 작업에서 일"에 속성 및 해당 `ItemStyle`의 `HorizontalAlign` 속성을 `Center`입니다. 호출 하는 `DisplayDaysOnJob` 템플릿에서 메서드 추가 `ItemTemplate` 데이터 바인딩 구문을 사용 하 여:


[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample6.aspx)]

`Container.DataItem` 반환을 `DataRowView` 개체에 해당 하는 `DataSource` 레코드에 바인딩된는 `GridViewRow`합니다. 해당 `Row` 속성은 강력한 형식의 반환 `Northwind.EmployeesRow`, 전달 되는 `DisplayDaysOnJob` 메서드. 이 데이터 바인딩을 구문에서 직접 표시 될 수 있습니다는 `ItemTemplate` 선언적 구문 아래과 같이 할당할 수 있습니다 또는 `Text` Label 웹 컨트롤의 속성입니다.

> [!NOTE]
> 에 전달 하는 대신에 또는 `EmployeesRow` 인스턴스 수만 전달 합니다 `HireDate` 사용 하 여 값 `<%# DisplayDaysOnJob(Eval("HireDate")) %>`합니다. 그러나 합니다 `Eval` 메서드가 반환 되는 `object`이므로 변경 해야 할 우리의 `DisplayDaysOnJob` 형식의 입력된 매개 변수를 허용 하도록 메서드 서명을 `object`, 대신. 에서는 맹목적으로 캐스팅할 수 없습니다는 `Eval("HireDate")` 호출을 `DateTime` 때문에 `HireDate` 열에는 `Employees` 테이블에 포함 될 수 있습니다 `NULL` 값. 적용할 해야 하므로 `object` 에 대 한 입력된 매개 변수로 `DisplayDaysOnJob` 메서드, 데이터베이스 되었을 경우 확인 `NULL` 값 (사용 하 여 수행할 수 있습니다 `Convert.IsDBNull(objectToCheck)`), 그에 따라 계속 진행 합니다.


전체 전달할 여러분도 이러한 미묘한 측면이 들으로 인해 `EmployeesRow` 인스턴스. 사용에 대 한 자세한 맞춤 예제는 다음 자습서에서 살펴보겠습니다는 `Eval("columnName")` 구문 서식 지정 메서드로 입력된 매개 변수를 전달 합니다.

다음은 선언적 구문을 보여 줍니다는 GridView에 대 한를 templatefield로 추가 된 후 및 `DisplayDaysOnJob` 에서 호출 된 메서드는 `ItemTemplate`:


[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample7.aspx)]

그림 16에서는 브라우저를 통해 볼 때 완성된 된 자습서를 보여 줍니다.


[![표시 되는 직원의 근무 작업의 일 수](using-templatefields-in-the-gridview-control-cs/_static/image47.png)](using-templatefields-in-the-gridview-control-cs/_static/image46.png)

**그림 16**: The Number의 일 표시 되는 직원의 근무 작업 ([큰 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image48.png))


## <a name="summary"></a>요약

GridView 컨트롤에서 TemplateField 더 높은 수준의 다른 필드 컨트롤을 사용 하 여 사용 가능한 것 보다 데이터를 표시 하는 유연성을 허용 합니다. TemplateFields 상황에 적합 위치:

- 여러 데이터 필드를 하나의 GridView 열에 표시 해야 합니다.
- 데이터는 일반 텍스트가 아닌 웹 컨트롤을 사용 하 여 표현 가장
- 출력은 데이터를 다시 포맷 또는 메타 데이터 표시와 같은 기본 데이터에 따라 달라 집니다.

데이터의 표시를 사용자 지정 하는 것 외에도 앞으로 살펴보겠지만 나중에 자습서를 편집 하 고 데이터를 삽입할 사용 하는 사용자 인터페이스 사용자 지정 하기 위한 TemplateFields도 사용 됩니다.

다음 두 자습서를 살펴보고는 DetailsView에서 TemplateFields 사용 시작 템플릿 탐색을 계속 합니다. 그런 다음, 필드 대신 템플릿을 사용 하 여 데이터의 구조와 레이아웃의 유연성을 제공 하는 FormView에 설정 됩니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Dan Jagers 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](custom-formatting-based-upon-data-cs.md)
> [다음](using-templatefields-in-the-detailsview-control-cs.md)
