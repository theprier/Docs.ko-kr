---
uid: web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-gridview-control-cs
title: "TemplateFields GridView 컨트롤 (C#)에 사용 하 여 | Microsoft Docs"
author: rick-anderson
description: "GridView 유연성을 제공 하도록 서식 파일을 사용 하 여 렌더링 하는 TemplateField를 제공 합니다. 서식 파일에는 정적 HTML 웹 컨트롤을 혼합 하 여 포함 될 수 있습니다 및..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 11de31e8-a78a-4f96-bd75-66e994175902
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-gridview-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 004f1450937cc6543cb728e01586e3c3529a57d0
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="using-templatefields-in-the-gridview-control-c"></a>GridView 컨트롤 (C#)에서 TemplateFields 사용
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_12_CS.exe) 또는 [PDF 다운로드](using-templatefields-in-the-gridview-control-cs/_static/datatutorial12cs1.pdf)

> GridView 유연성을 제공 하도록 서식 파일을 사용 하 여 렌더링 하는 TemplateField를 제공 합니다. 서식 파일에는 혼합 포함 될 수 있습니다 정적 HTML 웹 컨트롤 및 데이터 바인딩 구문입니다. 이 자습서는 TemplateField는 더 높은 수준의 GridView 컨트롤에서 사용자 지정을 달성 하기 위해 사용 하는 방법을 검토 합니다.


## <a name="introduction"></a>소개

GridView에서 속성을 나타내는 필드의 집합으로 구성 되 고 `DataSource` 데이터를 표시 하는 방법을 함께 렌더링된 된 출력에 포함 되도록 합니다. 가장 간단한 필드 형식은 BoundField 데이터 값을 텍스트로 표시 합니다. 다른 필드 형식을 대체 HTML 요소를 사용 하 여 데이터를 표시 합니다. CheckBoxField, 예를 들어; 지정 된 데이터 필드의 값에 따라 선택 된 상태가 된 확인란으로 렌더링 이미지 필드는 지정 된 데이터 필드를 기반으로 하는 이미지 원본 이미지를 렌더링 합니다. 하이퍼링크 및 기본 데이터 필드 값에 따라 달라 집니다 상태가 단추 HyperLinkField 및 ButtonField 필드 형식을 사용 하 여 렌더링할 수 있습니다.

CheckBoxField, ImageField, HyperLinkField, 및 ButtonField 필드 형식 데이터의 대체 뷰를 허용 하는 동안 여전히 서로 서식 지정에 대해 상당히 제한적입니다. CheckBoxField는 ImageField 단일 이미지를 표시할 수 있지만 하나의 확인란을 표시할 수 있습니다. 특정 필드를 checkbox 일부 텍스트를 표시 해야 하는 경우에 어떻게 *및* 이미지를 다른 데이터 필드 값에 따라 모든? 또는 어떻게 해야 할까요 확인란, 이미지, 하이퍼링크 또는 단추 이외의 다른 웹 컨트롤을 사용 하 여 데이터를 표시 하 시겠습니까? 또한 BoundField에서 단일 데이터 필드에 표시를 제한합니다. 단일 GridView 열에 두 개 이상의 데이터 필드 값을 표시 하려면 어떻게 해야 할까요?

GridView 이러한 수준의 유연성을 수용 하기 위해 사용 하 여 렌더링 하는 TemplateField는 제공 된 *템플릿*합니다. 서식 파일에는 혼합 포함 될 수 있습니다 정적 HTML 웹 컨트롤 및 데이터 바인딩 구문입니다. 또한는 TemplateField는는 다양 한 상황에 렌더링을 사용자 지정 하는 데 사용할 수 있는 서식 파일의 여러 가지가 있습니다. 예를 들어는 `ItemTemplate` 하는 데 기본적으로 각 행에 대 한 셀에 렌더링 되지만 `EditItemTemplate` 템플릿을 사용 하 여 데이터를 편집할 때 인터페이스를 사용자 지정할 수 있습니다.

이 자습서는 TemplateField는 더 높은 수준의 GridView 컨트롤에서 사용자 지정을 달성 하기 위해 사용 하는 방법을 검토 합니다. 에 [이전 자습서](custom-formatting-based-upon-data-cs.md) 서식을 사용 하 여 원본 데이터에 따라 사용자 지정 하는 방법에 살펴보았습니다는 `DataBound` 및 `RowDataBound` 이벤트 처리기입니다. 기본 데이터를 기반으로 서식을 사용자 지정 하는 다른 방법은 서식 템플릿 내에서 메서드를 호출 하 여 합니다. 살펴보게이 기술을이 자습서도 있습니다.

이 자습서에 대 한 TemplateFields 직원의 목록이 표시를 사용자 지정을 사용 합니다. 예에서는 모든 직원을 나열 합니다: 하지만 직원의 ½ ֳ µ 직원과 고용 날짜는 달력 컨트롤 및 일 수가 한 이용 되어 회사를 나타내는 상태 열에 하나 이상의 열에서 첫 번째 및 마지막 이름입니다.


[![세 가지 TemplateFields 표시를 사용자 지정 하는 데 사용 됩니다.](using-templatefields-in-the-gridview-control-cs/_static/image2.png)](using-templatefields-in-the-gridview-control-cs/_static/image1.png)

**그림 1**: 세 TemplateFields은 표시를 사용자 지정 하는 데 사용 됩니다 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image3.png))


## <a name="step-1-binding-the-data-to-the-gridview"></a>1 단계: GridView에 데이터 바인딩

TemplateFields 모양을 사용자 지정 하는 데 필요한 시나리오, 보고에 I 편리 우선 BoundFields만 포함 하는 GridView 컨트롤 만들기를 시작 하려면 다음을 새 TemplateFields를 추가 하거나 기존 BoundFields를 변환 필요에 따라 TemplateFields 합니다. 따라서 살펴보겠습니다이 자습서는 GridView 디자이너를 통해 페이지를 추가 및 직원의 목록을 반환 하는 ObjectDataSource에 바인딩. 이러한 단계 각각의 employee 필드에 대 한 BoundFields와는 GridView를 만들어집니다.

열기는 `GridViewTemplateField.aspx` 디자이너 도구 상자에서는 GridView를 끌어서 페이지입니다. GridView의 스마트 태그에서 호출 하는 새 ObjectDataSource 컨트롤을 추가 하도록 선택 된 `EmployeesBLL` 클래스의 `GetEmployees()` 메서드.


[![GetEmployees() 메서드를 호출 하는 새 ObjectDataSource 컨트롤 추가](using-templatefields-in-the-gridview-control-cs/_static/image5.png)](using-templatefields-in-the-gridview-control-cs/_static/image4.png)

**그림 2**: 새 ObjectDataSource 컨트롤 해당 Invoke 추가 `GetEmployees()` 메서드 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image6.png))


GridView 이런이 방식으로 바인딩 자동으로 추가 BoundField 각 직원 속성에 대해: `EmployeeID`, `LastName`, `FirstName`, `Title`, `HireDate`, `ReportsTo`, 및 `Country`합니다. 이 보고서에 대 한 보겠습니다 문제 되지을 표시 하는 `EmployeeID`, `ReportsTo`, 또는 `Country` 속성입니다. 이러한 BoundFields를 제거 하려면 다음을 수행할 수 있습니다.

- GridView의 스마트 태그에서 열 편집 링크 필드 대화 상자 클릭을 사용 하 여이 대화 상자를 엽니다. 다음으로, 왼쪽 아래에서 BoundFields 나열 빨간색 X를 클릭 하 고 선택 단추를 BoundField를 제거 합니다.
- 소스 뷰에서 GridView의 선언적 구문을 직접 편집, 삭제는 `<asp:BoundField>` 제거할 BoundField에 대 한 요소입니다.

제거한 후의 `EmployeeID`, `ReportsTo`, 및 `Country` BoundFields, GridView의 태그와 같습니다.


[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample1.aspx)]

브라우저에서 진행률을 볼 보십시오. 이 시점에서 표시 되어야 레코드가 있는 테이블에는 각 직원 및 4 개의 열에 대 한: 하나에 대 한 직원의 성을, 첫 번째 이름을 하나, 제목에 대 한 직원과 고용 날짜에 대 한 하나 있습니다.


[![LastName, FirstName, 제목 및 HireDate 필드는 각 직원에 대해 표시 됩니다.](using-templatefields-in-the-gridview-control-cs/_static/image8.png)](using-templatefields-in-the-gridview-control-cs/_static/image7.png)

**그림 3**:는 `LastName`, `FirstName`, `Title`, 및 `HireDate` 각 직원에 대 한 필드가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image9.png))


## <a name="step-2-displaying-the-first-and-last-names-in-a-single-column"></a>2 단계: 단일 열에는 첫 번째 및 마지막 이름 표시

현재 각 직원의 첫 번째 및 마지막 이름이 별도 열에 표시 됩니다. 대신 하나의 열으로 결합 좋을 것입니다. 이렇게 하려면를 TemplateField를 사용 해야 합니다. 에서는 추가 새 TemplateField, 필요한 태그와 데이터 바인딩된 구문을를 추가 하 고 다음 삭제는 `FirstName` 및 `LastName` BoundFields, 또는에서는 변환할 수는 `FirstName` BoundField를 TemplateField로 포함 하도록 TemplateField 편집 `LastName` 값을 복사한 후 제거는 `LastName` BoundField 합니다.

두 방법 모두 동일한 결과 net 그러나 개인적으로 변환이 자동으로 추가 하기 때문에 가능 하면 TemplateFields BoundFields 변환할는 `ItemTemplate` 및 `EditItemTemplate` 웹 컨트롤 및 모양 모방 하기 위해 데이터 바인딩된 구문을 사용 하 여 및는 BoundField의 기능을 추가 합니다. 이점은 적은 작업을 수행 하는 TemplateField 변환 프로세스는 수행한 일부 작업을 수행해 줍니다 대로 해야는 점입니다.

기존 BoundField를 TemplateField로 변환할 필드 대화 상자를 표시 하는 GridView의 스마트 태그를에서 열 편집 링크를 클릭 합니다. BoundField 왼쪽된 아래 모서리에 있는 목록에서 변환 하 고 오른쪽 아래 모서리에서 ""이이 필드를 TemplateField로 변환 링크를 클릭 한 다음를 선택 합니다.


[![BoundField 필드 대화 상자에서를 TemplateField로 변환](using-templatefields-in-the-gridview-control-cs/_static/image11.png)](using-templatefields-in-the-gridview-control-cs/_static/image10.png)

**그림 4**: TemplateField로는 BoundField 필드 대화 상자에서 변환 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image12.png))


계속 진행 하 고 변환 된 `FirstName` BoundField를 TemplateField로 합니다. 이 변경 후 디자이너에서 perceptive 차이점이 있습니다. BoundField의 모양과 느낌을 유지 하는 TemplateField 만듭니다는 BoundField를 TemplateField로 변환 때문입니다. 이 변환 프로세스는 BoundField의 선언적 구문-있는데도 visual 차이가 없으며이 시점에서 디자이너를 대체 `<asp:BoundField DataField="FirstName" HeaderText="FirstName" SortExpression="FirstName" />` -다음 TemplateField 구문을 사용 하 여:


[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample2.aspx)]

볼 수 있듯이 TemplateField는 두 개의 템플릿으로 구성 됩니다는 `ItemTemplate` 레이블이 있는 해당 `Text` 속성의 값으로 설정 됩니다는 `FirstName` 데이터 필드와 `EditItemTemplate` 컨트롤 TextBox와 `Text` 도 속성이 설정 되어 에 `FirstName` 데이터 필드입니다. 구문이- `<%# Bind("fieldName") %>` -나타냅니다 데이터 필드  *`fieldName`*  지정된 된 웹 컨트롤 속성에 바인딩됩니다.

추가 하려면는 `LastName` 데이터 필드 값을 다른 레이블 웹 컨트롤에 추가 해야이 TemplateField는 `ItemTemplate` 바인딩하고 해당 `Text` 속성을 `LastName`합니다. 이 디자이너를 통해 또는 수동으로 수행할 수 있습니다. 직접 수행 하려면 추가를 적절 한 선언적 구문은 `ItemTemplate`:


[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample3.aspx)]

디자이너를 통해 추가 GridView의 스마트 태그에서 템플릿 편집 링크를 클릭 합니다. GridView의 템플릿 편집 인터페이스를 표시 됩니다. 이 인터페이스의 스마트 태그는 GridView에 템플릿 목록이 됩니다. 드롭다운 목록에 나열 된 유일한 서식 파일은 이러한 서식 파일에 대 한 개이므로 하나의 TemplateField이 시점에서,는 `FirstName` 와 함께 TemplateField는 `EmptyDataTemplate` 및 `PagerTemplate`합니다. `EmptyDataTemplate` 서식 파일을 지정 하는 데; GridView에 바인딩된 데이터에는 결과가 GridView의 출력을 렌더링할는 `PagerTemplate`지정한 경우 페이징을 지원 되는 GridView에 대 한 페이징 인터페이스를 렌더링 하는 데 사용 됩니다.


[![GridView의 템플릿 디자이너에서 편집할 수 있습니다.](using-templatefields-in-the-gridview-control-cs/_static/image14.png)](using-templatefields-in-the-gridview-control-cs/_static/image13.png)

**그림 5**: GridView의 템플릿 수 수 편집할 통해 the 디자이너 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image15.png))


또한 표시 하려면는 `LastName` 에 `FirstName` TemplateField 도구 상자의 레이블 컨트롤을 끌어는 `FirstName` TemplateField의 `ItemTemplate` GridView에서의 템플릿 편집 인터페이스.


[![FirstName TemplateField ItemTemplate에 레이블 웹 컨트롤 추가](using-templatefields-in-the-gridview-control-cs/_static/image17.png)](using-templatefields-in-the-gridview-control-cs/_static/image16.png)

**그림 6**: 레이블 웹 컨트롤을 추가 `FirstName` TemplateField의 ItemTemplate ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image18.png))


이 시점에 TemplateField 추가 레이블 웹 컨트롤에 해당 `Text` 속성이 "Label"로 설정 합니다. 이 속성의 값을 바인딩할 수 있도록이 설정을 변경할 필요는 `LastName` 데이터 필드에 대신 합니다. 레이블 컨트롤의 스마트 태그를이 클릭이 수행 및 데이터 바인딩 편집 옵션을 선택 합니다.


[![레이블의 스마트 태그에서 편집 데이터 바인딩 옵션을 선택 합니다.](using-templatefields-in-the-gridview-control-cs/_static/image20.png)](using-templatefields-in-the-gridview-control-cs/_static/image19.png)

**그림 7**: 레이블의 스마트 태그에서 데이터 바인딩 편집 옵션을 선택 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image21.png))


그러면 데이터 바인딩 대화 상자를 표시 됩니다. 여기에서 왼쪽에 있는 목록에서 데이터 바인딩에 참여 하 고 오른쪽에 있는 드롭 다운 목록에서 데이터를 바인딩할 필드를 선택 하는 속성을 선택할 수 있습니다. 선택 된 `Text` 왼쪽에서 속성 및 `LastName` 오른쪽에서 필드를 확인을 클릭 합니다.


[![Text 속성 LastName 데이터 필드에 바인딩](using-templatefields-in-the-gridview-control-cs/_static/image23.png)](using-templatefields-in-the-gridview-control-cs/_static/image22.png)

**그림 8**: 바인딩하는 `Text` 속성을는 `LastName` 데이터 필드 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image24.png))


> [!NOTE]
> 데이터 바인딩 대화 상자에는 양방향 데이터 바인딩을 수행할 것인지 여부를 나타낼 수 있습니다. 하지 않으면이 옵션을 선택 취소 구문이 `<%# Eval("LastName")%>` 대신 사용할 `<%# Bind("LastName")%>`합니다. 이 자습서에 대 한 가지 방법 중 하나는 문제가 없습니다. 양방향 데이터 바인딩을 삽입 및 데이터를 편집 하는 경우 중요 합니다. 그러나 단순히 데이터를 표시 하는 것에 대 한 어느 방법이 든 동일 하 게도 작동 합니다. 이후 자습서에서 자세히 양방향 데이터 바인딩을 설명 합니다.


브라우저를 통해이 페이지를 보려면 잠시 시간. 볼 수 있듯이 GridView에 아직 포함 되어 네 개의 열; 그러나는 `FirstName` 열이 나열 됩니다 *둘 다* 는 `FirstName` 및 `LastName` 데이터 필드의 값입니다.


[![단일 열에는 FirstName 및 LastName 값이 모두 표시 됩니다.](using-templatefields-in-the-gridview-control-cs/_static/image26.png)](using-templatefields-in-the-gridview-control-cs/_static/image25.png)

**그림 9**: 모두는 `FirstName` 및 `LastName` 값은 단일 열에 나타납니다 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image27.png))


이 첫 번째 단계를 완료 하려면 제거의 `LastName` BoundField 및 이름 바꾸기는 `FirstName` TemplateField의 `HeaderText` 속성을 "Name"입니다. 이러한 변경 된 후 GridView의 선언적 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample4.aspx)]


[![각 직원의 첫 번째 및 성을 하나의 열에 표시 됩니다.](using-templatefields-in-the-gridview-control-cs/_static/image29.png)](using-templatefields-in-the-gridview-control-cs/_static/image28.png)

**그림 10**: 각 직원의 첫 번째 및 성을 하나의 열에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image30.png))


## <a name="step-3-using-the-calendar-control-to-display-thehireddatefield"></a>3 단계: 디스플레이로 달력 컨트롤을 사용 하 여`HiredDate`필드

GridView에 텍스트로 데이터 필드 값을 표시 하는 것은 BoundField를 사용 하 여 단순하게입니다. 그러나 특정 시나리오에 대 한 가장 잘 표시 됩니다 텍스트만 대신 특정 웹 컨트롤을 사용 하 여 합니다. 이러한 사용자 지정 데이터의 표시의은 TemplateFields로 이전에 가능 합니다. 예를 들어 대신 직원의 고용 날짜를 텍스트로 표시를 보다 수 알아보겠습니다 달력 (사용 하 여 [Calendar 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar(VS.80).aspx)) 직원과 고용 날짜를 강조 표시 됩니다.

이를 위해 변환 하 여 시작 된 `HiredDate` BoundField를 TemplateField로 합니다. GridView의 스마트 태그에 파일을 필드 대화 상자를 표시 하 고 열 편집 링크를 클릭 합니다. 선택 된 `HiredDate` BoundField 및 클릭 "변환"이이 필드를 TemplateField로 합니다.


[![HiredDate BoundField를 TemplateField로 변환](using-templatefields-in-the-gridview-control-cs/_static/image32.png)](using-templatefields-in-the-gridview-control-cs/_static/image31.png)

**그림 11**: 변환는 `HiredDate` 정도 TemplateField로 BoundField ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image33.png))


2 단계에서에서 설명한 것 처럼이 BoundField 연결로 바뀝니다 포함 된 TemplateField는 `ItemTemplate` 및 `EditItemTemplate` 레이블 및 텍스트와 해당 `Text` 속성이 바인딩되는 `HiredDate` databinding구문을사용하여값`<%# Bind("HiredDate")%>`.

Calendar 컨트롤에 텍스트를 바꾸려면 레이블을 제거 하 고는 달력 컨트롤을 추가 하 여 템플릿을 편집 합니다. 디자이너에서 GridView의 스마트 태그에서 템플릿 편집을 선택 하 고 선택 된 `HireDate` TemplateField의 `ItemTemplate` 드롭 다운 목록에서 합니다. 다음 레이블 컨트롤을 삭제를 달력 컨트롤을 도구 상자에서 템플릿 편집 인터페이스도 끕니다.


[![달력 컨트롤을 추가 TemplateField의 ItemTemplate HireDate](using-templatefields-in-the-gridview-control-cs/_static/image35.png)](using-templatefields-in-the-gridview-control-cs/_static/image34.png)

**그림 12**: 달력 컨트롤을 추가 `HireDate` TemplateField의 `ItemTemplate` ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image36.png))


GridView에서 각 행은에서 달력 컨트롤을 포함 하는 시점에서 해당 `HiredDate` TemplateField 합니다. 그러나 직원의 실제 `HiredDate` 를 기본적으로 현재 월 및 날짜를 표시 하려면 각 Calendar 컨트롤을 일으키는 Calendar 컨트롤에 값이 아무 곳 이나 설정 되지 않습니다. 이 해결 하려면 각 직원의 할당 해야 `HiredDate` 달력 컨트롤의 [SelectedDate](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selecteddate(VS.80).aspx) 및 [VisibleDate](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.visibledate(VS.80).aspx) 속성입니다.

Calendar 컨트롤의 스마트 태그에서 데이터 바인딩 편집을 선택 합니다. 다음으로, 둘 다를 바인딩할 `SelectedDate` 및 `VisibleDate` 속성을는 `HiredDate` 데이터 필드입니다.


[![SelectedDate 및 VisibleDate 속성 HiredDate 데이터 필드에 바인딩](using-templatefields-in-the-gridview-control-cs/_static/image38.png)](using-templatefields-in-the-gridview-control-cs/_static/image37.png)

**그림 13**: 바인딩하는 `SelectedDate` 및 `VisibleDate` 속성을는 `HiredDate` 데이터 필드 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image39.png))


> [!NOTE]
> Calendar 컨트롤의 선택 된 날짜가 필요 반드시 볼 수 없습니다. 예를 들어 한 일정 8 월 1 일 있을 수<sup>st</sup>, 선택한 날짜로 1999 하지만 현재 월과 연도 닫아야 합니다. Calendar 컨트롤에 의해 지정 된 선택 된 날짜와 표시 날짜 `SelectedDate` 및 `VisibleDate` 속성입니다. 직원의 두 선택 해야 하므로 `HiredDate` 를 바인딩해야 하는 두 가지이 속성을 모두 표시 되 고 있는지 확인 하 고는 `HireDate` 데이터 필드입니다.


브라우저에서 페이지를 보고, 달력 이제 직원의 고용 된 날짜의 월을 표시 하 고 해당 특정 날짜를 선택 합니다.


[![직원의 HiredDate Calendar 컨트롤에 표시 됩니다.](using-templatefields-in-the-gridview-control-cs/_static/image41.png)](using-templatefields-in-the-gridview-control-cs/_static/image40.png)

**그림 14**: The 직원의 `HiredDate` Calendar 컨트롤에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image42.png))


> [!NOTE]
> 지금까지 살펴본 모든 예에서, 달리이 자습서에 수행한 *하지* 설정 `EnableViewState` 속성을 `false` 이 GridView에 대 한 합니다. 이 결정에 대 한 이유 선택 된 달력의 날짜를 클릭 하기만 해도 날짜로 설정에서 포스트백 Calendar 컨트롤의 날짜를 클릭 하면 때문입니다. 그러나 GridView의 뷰 상태를 비활성화 하는 경우 다시 게시할 때마다 GridView의 데이터는 다시 바인딩할 달력의 선택한 날짜를 설정 하면 해당 기본 데이터 원본에 *다시* 은 직원에 게 `HireDate`덮어쓰기를, 사용자가 선택한 날짜입니다.


이 자습서에 대 한이 이론에 불과합니다 토론 때문에 사용자가 직원의 업데이트할 수 없습니다 `HireDate`합니다. 해당 날짜를 선택할 수 없는 있도록 달력 컨트롤을 구성 하는 가장 좋은 될 것입니다. 그럼에도 불구 하 고이 자습서에서는 일부 환경에서는 뷰 상태를 사용 해야 한다고 특정 기능을 제공할 수 있습니다.

## <a name="step-4-showing-the-number-of-days-the-employee-has-worked-for-the-company"></a>4 단계: 회사에 근무 한 일 수를 보여 주는

지금까지 살펴본 것 TemplateFields의 두 개의 응용 프로그램:

- 하나의 열에 두 개 이상의 데이터 필드 값을 결합 하 고
- 텍스트 대신 웹 컨트롤을 사용 하 여 데이터 필드 값 표현

세 번째 TemplateFields 사용 하는 내부 데이터 GridView의에 대 한 메타 데이터를 표시 합니다. 직원의 고용 날짜를 표시할 뿐만 아니라 예를 들어 수도 하고자 직장 가격이 총 일 수를 표시 하는 열이 있어야 합니다.

아직 TemplateFields의 또 다른 용도 기본 데이터를 데이터베이스에 저장 되는 형식 보다 웹 페이지 보고서에서 마다 다르게 표시 될 해야 할 때 시나리오에서 발생 합니다. 상상할는 `Employees` 테이블는 `Gender` 문자를 저장 하는 필드 `M` 또는 `F` 는 직원의 성별을 나타냅니다. 이 정보는 웹 페이지에 표시할 때 "Male" 또는 "Female", "M" 또는 "F" 뿐 아니라 성별을 표시 하는 것이 좋습니다.

두이 시나리오 모두를 만들어 처리할 수 있습니다는 *서식 지정 메서드에* ASP.NET 페이지의 코드 숨김 클래스에서 (또는으로 구현 하는 별도 클래스 라이브러리는 `static` 메서드)는 서식 파일에서 호출 되는 합니다. 이러한 서식 지정 메서드는 이전에 표시 하는 동일한 데이터 바인딩 구문을 사용 하 여 서식 파일에서 호출 됩니다. 형식 지정 메서드가 임의 개수의 매개 변수를 가져올 수 있지만 문자열을 반환 해야 합니다. 이 반환 된 문자열은 HTML을 템플릿에 삽입 됩니다.

이 개념을 설명 해 보겠습니다 총 작업에 대 한 직원의 근무 일 수를 나열 하는 열을 표시 하려면이 자습서를 확장 합니다. 이 형식 지정 메서드가 걸리는 `Northwind.EmployeesRow` 개체를 문자열로 직원을 이용 되어에 일 수를 반환 합니다. 이 메서드는 ASP.NET 페이지의 코드 숨김 클래스에 추가할 수 있지만 *해야* 로 표시 되어야 `protected` 또는 `public` 서식 파일을 액세스할 수 있도록 합니다.


[!code-csharp[Main](using-templatefields-in-the-gridview-control-cs/samples/sample5.cs)]

이후는 `HiredDate` 필드에 포함할 수 `NULL` 하 값이 먼저 확인 해야 하는 값을 데이터베이스 `NULL` 계산을 진행 하기 전에. 경우는 `HiredDate` 값은 `NULL`, 없는 경우 단순히 문자열 "Unknown"; 반환 `NULL`, 현재 시간 사이의 차이 계산 했습니다 및 `HiredDate` 값 및 날짜 수를 반환 합니다.

이 메서드를 활용 하 여 데이터 바인딩을 구문을 사용 하 여 GridView에서 TemplateField에서을 실행 해야 합니다. GridView의 스마트 태그에서 열 편집 링크를 클릭 하 여 새 TemplateField 추가 GridView에 새 TemplateField를 추가 하 여 시작 합니다.


[![GridView에 새 TemplateField 추가](using-templatefields-in-the-gridview-control-cs/_static/image44.png)](using-templatefields-in-the-gridview-control-cs/_static/image43.png)

**그림 15**: GridView에 새 TemplateField 추가 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image45.png))


이 새 TemplateField 설정 `HeaderText` 속성을 "the 작업에서 일" 및 해당 `ItemStyle`의 `HorizontalAlign` 속성을 `Center`합니다. 호출 하는 `DisplayDaysOnJob` 메서드는 서식 파일에서 추가 `ItemTemplate` 다음 구문이 사용:


[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample6.aspx)]

`Container.DataItem`반환 된 `DataRowView` 개체에 해당 하는 `DataSource` 레코드에 바인딩된는 `GridViewRow`합니다. 해당 `Row` 속성 강력한 형식의 반환 `Northwind.EmployeesRow`로 전달 되는 `DisplayDaysOnJob` 메서드. 이 데이터 바인딩 구문을 직접 나타날 수 있습니다는 `ItemTemplate` (에서처럼 아래 선언적 구문) 또는에 지정할 수는 `Text` Label 웹 컨트롤의 속성입니다.

> [!NOTE]
> 에 전달 하는 대신에 또는 `EmployeesRow` 인스턴스, 우리 전달할 수에 `HireDate` 를 사용 하 여 값 `<%# DisplayDaysOnJob(Eval("HireDate")) %>`합니다. 그러나는 `Eval` 메서드가 반환 되는 `object`이므로 변경 해야 할 우리의 `DisplayDaysOnJob` 메서드 시그니처를 형식의 입력된 매개 변수를 허용 하도록 `object`, 대신 합니다. म 맹목적으로 캐스팅할 수 없습니다는 `Eval("HireDate")` 에 대 한 호출는 `DateTime` 때문에 `HireDate` 열에는 `Employees` 포함 하 여 `NULL` 값입니다. 따라서에 동의 해야 한다는 의미는 `object` 에 대 한 입력된 매개 변수로 `DisplayDaysOnJob` 메서드를 확인 하는 데이터베이스를 갖는 경우 `NULL` 값 (를 사용 하 여 수행할 수 `Convert.IsDBNull(objectToCheck)`), 그에 따라 계속 진행 합니다.


이러한 미묘한 인해 선택한 이유는 전체에 전달 하도록 `EmployeesRow` 인스턴스. 다음 자습서에서 사용 하기 위한 더 많은 맞춤 예제 보겠습니다는 `Eval("columnName")` 를 서식 지정 메서드에 입력된 매개 변수 전달에 대 한 구문입니다.

다음 테이블에 나와 선언적 구문 우리의 GridView에 대 한 TemplateField는 추가 된 후와 `DisplayDaysOnJob` 에서 호출 하는 메서드는 `ItemTemplate`:


[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample7.aspx)]

브라우저를 통해 볼 때 그림 16 완성 된 자습서를 보여 줍니다.


[![표시 되는 직원의 근무 하 고 작업에 대해의 일 수](using-templatefields-in-the-gridview-control-cs/_static/image47.png)](using-templatefields-in-the-gridview-control-cs/_static/image46.png)

**그림 16**: The Number의 일 표시 되는 직원의 근무 직장 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image48.png))


## <a name="summary"></a>요약

GridView 컨트롤에 TemplateField 더 높은 수준의 다른 필드 컨트롤과 함께 사용할 수 있는 것 보다 데이터를 표시 하는 유연성을 허용 합니다. 상황에 맞는 이상적인 TemplateFields는 여기서:

- 여러 개의 데이터 필드를 한 GridView 열에 표시 해야 합니다.
- 데이터는 일반 텍스트 대신 웹 컨트롤을 사용 하 여 가장 잘 표현
- 출력 메타 데이터를 표시 하는 등 또는 데이터를 다시 포맷 기본 데이터에 따라 다릅니다.

데이터의 표시를 사용자 지정 하는 것 외에도 볼 수 있겠지만, 이후 자습서를 편집 하 고 데이터를 삽입할 사용 되는 사용자 인터페이스 사용자 지정 하기 위한 TemplateFields도 사용 됩니다.

다음 두 자습서에서는 계속 TemplateFields DetailsView에서 사용 하 여 보는 것으로 시작 하는 서식 파일을 탐색 합니다. 그런 다음, FormView를 사용 하 여 서식 파일 필드 대신이 대화 상자 레이아웃 및 데이터 구조에서 더욱 유연 하 설정 합니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Dan Jagers 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](custom-formatting-based-upon-data-cs.md)
[다음](using-templatefields-in-the-detailsview-control-cs.md)
