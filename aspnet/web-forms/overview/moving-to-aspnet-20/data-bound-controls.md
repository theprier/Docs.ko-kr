---
uid: web-forms/overview/moving-to-aspnet-20/data-bound-controls
title: 데이터 바인딩된 컨트롤 | Microsoft Docs
author: microsoft
description: 대부분의 ASP.NET 응용 프로그램 백 엔드 데이터 원본에서 데이터 표시의 어느 정도에 의존 합니다. 데이터 바인딩된 컨트롤의 상호 작용 w pivotal 일부일...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 0e23ff32-646d-43f3-8bec-6b2313d3abd6
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-bound-controls
msc.type: authoredcontent
ms.openlocfilehash: b115109c7307d05dc9e620378a51a71407204740
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41835565"
---
<a name="data-bound-controls"></a>데이터 바인딩 컨트롤
====================
[Microsoft](https://github.com/microsoft)

> 대부분의 ASP.NET 응용 프로그램 백 엔드 데이터 원본에서 데이터 표시의 어느 정도에 의존 합니다. 데이터 바인딩된 컨트롤에는 동적 웹 응용 프로그램의 데이터와 상호 작용 하는 pivotal 부분 되었습니다. ASP.NET 2.0 데이터 바인딩된 컨트롤을 새 BaseDataBoundControl 클래스 등 선언적 구문에 대 한 몇 가지 향상을 소개 합니다.


대부분의 ASP.NET 응용 프로그램 백 엔드 데이터 원본에서 데이터 표시의 어느 정도에 의존 합니다. 데이터 바인딩된 컨트롤에는 동적 웹 응용 프로그램의 데이터와 상호 작용 하는 pivotal 부분 되었습니다. ASP.NET 2.0 데이터 바인딩된 컨트롤을 새 BaseDataBoundControl 클래스 등 선언적 구문에 대 한 몇 가지 향상을 소개 합니다.

BaseDataBoundControl DataBoundControl 클래스와 HierarchicalDataBoundControl 클래스에 대 한 기본 클래스로 작동합니다. 이 모듈에서는 DataBoundControl에서 파생 되는 다음 클래스 설명:

- AdRotator
- 목록 컨트롤
- GridView
- FormView
- DetailsView

HierarchicalDataBoundControl 클래스에서 파생 되는 다음 클래스를 살펴보겠습니다.

- TreeView
- 메뉴
- SiteMapPath

## <a name="databoundcontrol-class"></a>DataBoundControl 클래스

DataBoundControl 클래스는 테이블 형식 상호 작용 하는 데 사용 되는 추상 클래스 (vb에서 MustInherit 표시) 또는 목록 스타일 데이터입니다. 다음 컨트롤은 DataBoundControl에서 파생 된 컨트롤의 일부입니다.

## <a name="adrotator"></a>AdRotator

AdRotator 컨트롤을 사용 하면 특정 URL에 연결 된 웹 페이지에 그래픽 배너를 표시할 수 있습니다. 표시 되는 그래픽 컨트롤에 대 한 속성을 사용 하 여 회전 합니다. 사용 하 여 페이지에서 특정 ad 표시 하는 빈도 구성할 수 있습니다는 **인상** 속성 및 광고 필터링 할 수 있습니다 키워드 필터링을 사용 합니다.

AdRotator 컨트롤 데이터에 대 한 데이터베이스에서 XML 파일 또는 테이블을 사용 합니다. 다음 특성을 AdRotator 컨트롤을 구성 하려면 XML 파일에 사용 됩니다.

### <a name="imageurl"></a>ImageUrl
Ad에 대해 표시할 이미지의 URL입니다.

### <a name="navigateurl"></a>NavigateUrl
광고를 클릭할 때 사용자를 수행 해야 하는 URL입니다. 이 URL 인코딩 이어야 합니다.

### <a name="alternatetext"></a>AlternateText
대체 텍스트 도구 설명에 표시 되 고 화면 판독기가 읽은입니다. ImageUrl에서 지정한 이미지를 사용할 수 없는 경우에 표시 됩니다.

### <a name="keyword"></a>키워드
키워드 필터링을 사용할 때 사용할 수 있는 키워드를 정의 합니다. 지정 하면 키워드 필터와 일치 하는 키워드를 사용 하 여 해당 광고에만 표시 됩니다.

### <a name="impressions"></a>인상
특정 ad 있을 것으로 예상 되는 빈도 결정 하는 가중치 숫자입니다. 이 동일한 파일에서 다른 광고 느낌에 상대적입니다. XML 파일에 모든 광고에 대 한 집단 상대 값의 최대값은 2,048,000,000 1입니다.

### <a name="height"></a>높이
높이 (픽셀)에서 ad입니다.

### <a name="width"></a>너비
너비 (픽셀)에서 ad입니다.


> [!NOTE]
> 높이 및 너비 특성 AdRotator 컨트롤 자체에 대 한 너비와 높이 재정의합니다.


일반적인 XML 파일을 다음과 같이 표시 될 수 있습니다.

[!code-xml[Main](data-bound-controls/samples/sample1.xml)]

위의 예제에서는 Contoso에 대 한 ad는 ASP.NET 웹 사이트에 대 한 ad 인상 특성에 대 한 값으로 인해 나타날 가능성이으로 두 번입니다.

위의 XML 파일에서 광고를 표시 하려면 페이지에 AdRotator 컨트롤을 추가 하 고 설정 합니다 **클릭** 속성 아래와 같이 XML 파일을 가리키도록 합니다.

[!code-aspx[Main](data-bound-controls/samples/sample2.aspx)]

AdRotator 컨트롤에 대 한 데이터 원본으로 데이터베이스 테이블을 사용 하려는 경우 먼저 다음 스키마를 사용 하 여 데이터베이스를 설정 해야 합니다.

| **열 이름** | **데이터 형식** | **설명** |
| --- | --- | --- |
| ID | int | 기본 키입니다. 이 열에는 어떤 이름도 가질 수 있습니다. |
| ImageUrl | nvarchar(*length*) | Ad에 대해 표시할 이미지의 상대 또는 절대 URL입니다. |
| NavigateUrl | nvarchar(*length*) | Ad에 대 한 대상 URL입니다. 값을 얻을 수 없는 경우 ad 하이퍼링크 아닙니다. |
| AlternateText | nvarchar(*length*) | 이미지를 찾을 수 없는 경우 표시 되는 텍스트입니다. 일부 브라우저에서는 텍스트 도구 설명으로 표시 됩니다. 그래픽을 볼 수 없는 사용자를 소리내어 읽을 설명을 들을 수 있도록 내게 필요한 옵션에 대 한 대체 텍스트도 사용 됩니다. |
| 키워드 | nvarchar(*length*) | 페이지를 필터링 할 수 있는 ad에 대 한 범주입니다. |
| 인상 | int(4) | 광고가 표시 될 빈도의 가능성을 나타내는 숫자입니다. 더 큰 숫자를 더 자주 ad 표시 됩니다. XML 파일의 모든 상대 값의 합계 2048000000-1을 초과할 수 없습니다. |
| 너비 | int(4) | 픽셀에서 이미지의 너비입니다. |
| 높이 | int(4) | 픽셀에서 이미지의 높이입니다. |

이미 다른 스키마를 사용 하 여 데이터베이스를 만든 경우에 사용할 수 있습니다 합니다 **AlternateTextField**를 **ImageUrlField**, 및 **NavigateUrlField** 매핑할 속성을 기존 데이터베이스에 AdRotator 특성입니다. AdRotator 컨트롤의 데이터베이스에서 데이터를 표시할 추가 데이터 소스 컨트롤을 페이지로, 데이터베이스를 가리키도록 데이터 소스 컨트롤에 대 한 연결 문자열을 구성 하 고 설정 AdRotator 컨트롤의 **DataSourceID** 속성 데이터 소스 컨트롤의 ID입니다. AdRotator 광고를 프로그래밍 방식으로 구성할 필요가 있는 경우에 AdCreated 이벤트를 사용 합니다. AdCreated 이벤트는 두 매개 변수입니다. 하나는 개체 및 기타 AdCreatedEventArgs 인스턴스. AdCreatedEventArgs는 생성 되는 ad에 대 한 참조입니다.

다음 코드 조각은 ImageUrl, NavigateUrl, 및 AlternateText 광고에 대 한 프로그래밍 방식으로 설정:

[!code-csharp[Main](data-bound-controls/samples/sample3.cs)]

## <a name="list-controls"></a>목록 컨트롤

목록 컨트롤에는 ListBox, DropDownList, CheckBoxList, RadioButtonList, 및 BulletedList 포함 됩니다. 이러한 컨트롤의 각 데이터 원본에 데이터 바인딩될 수 있습니다. 데이터 원본에 하나의 필드를 사용 하 여 텍스트 표시로 하며 항목의 값으로 필요에 따라 두 번째 필드를 사용할 수 있습니다. 항목 디자인 타임에 정적으로 추가할 수도 있습니다 및 데이터 원본에서 추가 항목을 동적 및 정적 항목을 혼합할 수 있습니다.

데이터 목록 컨트롤을 바인딩하려면 페이지에 데이터 소스 컨트롤을 추가 합니다. 데이터 소스 컨트롤에 대 한 SELECT 명령을 지정 하 고 데이터 소스 컨트롤의 ID로 목록 컨트롤의 DataSourceID 속성을 설정 합니다. 사용 합니다 **DataTextField** 하 고 **DataValueField** 표시 텍스트 및 컨트롤에 대 한 값을 정의 하는 속성입니다. 또한 사용할 수는 **DataTextFormatString** 다음과 같이 표시 텍스트의 모양을 제어 하는 속성:

| **식** | **설명** |
| --- | --- |
| 가격: {0:C} | 숫자/decimal 데이터. 리터럴 표시 "가격:" 뒤에 숫자 통화 형식에서입니다. 통화 형식에서 culture 특성에 지정 된 culture 설정에 따라 합니다 **페이지** 지시문 또는 Web.config 파일에 있습니다. |
| {0:D4} | 정수 데이터입니다. 10 진수를 사용 하 여 사용할 수 없습니다. 정수는 네 가지 문자 너비는 0으로 채워집니다 필드에 표시 됩니다. |
| {0:N2}% | 숫자 데이터. 숫자 2-소수 자릿수를 표시 자릿수 다음에 리터럴 "%"입니다. |
| {0:000.0} | 숫자/decimal 데이터. 숫자가 한 자리로 반올림 됩니다. 세 자리보다 작은 숫자는 0으로 채워집니다. |
| {0:D} | 날짜/시간 데이터입니다. 표시를 위한 자세한 날짜 형식 ("1996 년, 년 8 월 6 일, 목요일")입니다. 날짜 형식은 page 지시문 또는 Web.config 파일의 문화권 설정에 따라 달라집니다. |
| {0:d} | 날짜/시간 데이터입니다. 표시 간단한 날짜 형식 ("12/31/99"). |
| {0:yy-MM-dd} | 날짜/시간 데이터입니다. (96-08-06) 숫자 연도-월-일 형식의 날짜를 표시합니다. |

## <a name="gridview"></a>GridView

GridView 컨트롤 테이블 형식 데이터 표시 및 선언적 방식을 사용 하 여 편집할 수 있습니다 및 DataGrid 컨트롤의 후속 버전입니다. 다음 기능은 GridView 컨트롤에서 사용할 수 있습니다.

- SqlDataSource와 같은 소스 컨트롤, 데이터 바인딩.
- 기본 제공 정렬 기능이 있습니다.
- 기본 제공 업데이트 및 삭제 기능입니다.
- 기본 제공 페이징 기능입니다.
- 기본 제공 행 선택 기능입니다.
- 동적으로 속성을 설정 하는 GridView 개체 모델에 프로그래밍 방식 액세스 이벤트를 처리 등에입니다.
- 여러 키 필드입니다.
- 하이퍼링크 열에 대 한 여러 데이터 필드입니다.
- 테마 및 스타일을 통해 모양을 사용자 지정할 수 있습니다.

**열 필드**

GridView 컨트롤의 각 열은 DataControlField 개체로 표시 됩니다. 기본적으로 AutoGenerateColumns 속성 설정 **true**에 데이터 소스의 각 필드에 대 한 AutoGeneratedField 개체를 만듭니다. 다음 각 필드는 데이터 소스의 각 필드에 나타나는 순서로 GridView 컨트롤에서 열으로 렌더링 됩니다. 필드에 표시 되는 열을 수동으로 제어할 수 있습니다.는 **GridView** 설정 하 여 컨트롤을 **AutoGenerateColumns** 속성을 **false** 다음 자체를 정의 열 필드 컬렉션입니다. 열 필드 형식에 따라 컨트롤의 열의 동작을 결정 합니다.

다음 표에서 사용할 수 있는 다른 열 필드 유형을 나열 합니다.

| **열 필드 형식** | **설명** |
| --- | --- |
| BoundField | 데이터 원본에서 필드의 값을 표시합니다. GridView 컨트롤의 기본 열 형식입니다. |
| ButtonField | GridView 컨트롤에서 각 항목에 대 한 명령 단추를 표시합니다. 이 옵션을 사용 하면 추가 또는 제거 단추와 같은 사용자 지정 단추 컨트롤의 열을 만들 수 있습니다. |
| CheckBoxField | GridView 컨트롤에서 각 항목에 대 한 확인란을 표시합니다. 이 열 필드 형식은 부울 값을 사용 하 여 필드를 표시 하려면 일반적으로 사용 됩니다. |
| CommandField | 미리 정의 된 선택, 편집 또는 삭제 작업을 수행 하기 위해 명령 단추를 표시 합니다. |
| HyperLinkField | 하이퍼링크로 데이터 원본의 필드의 값을 표시합니다. 이 열 필드 형식을 사용 하면 두 번째 필드 하이퍼링크의 URL에 바인딩할 수 있습니다. |
| ImageField | GridView 컨트롤에서 각 항목에 대 한 이미지를 표시합니다. |
| TemplateField | 지정한 템플릿에 따라 GridView 컨트롤에서 각 항목에 대 한 사용자 정의 내용을 표시 합니다. 이 열 필드 형식에는 사용자 지정 열 필드를 만들 수 있습니다. |

열 필드 컬렉션을 선언적으로 정의 하려면 먼저 추가 열기 및 닫기 **&lt;열&gt;** 와 GridView 컨트롤의 닫는 태그 사이입니다. 다음으로 열기 및 닫기 포함 하려는 열 필드를 나열 합니다. **&lt;열&gt;** 태그입니다. 지정 된 열은 나열 된 순서로 열 컬렉션에 추가 됩니다. 합니다 **열** 열 컨트롤의 필드 및 GridView 컨트롤의 열 필드를 프로그래밍 방식으로 관리할 수 있도록 모든 컬렉션 저장 합니다.

명시적으로 선언 된 열 필드를 자동으로 생성 된 열 필드와 함께에서 표시할 수 있습니다. 모두 사용 하는 명시적으로 선언 된 열 필드 뒤에 자동으로 생성 된 열 필드를 먼저 렌더링 됩니다.

## <a name="binding-to-data"></a>데이터 바인딩

GridView 컨트롤 데이터 소스 컨트롤을 바인딩할 수 있습니다 (같은 **SqlDataSource**를 **ObjectDataSource**등)는 System.Collections.IEnumerable을 구현 하는 모든 데이터 원본 뿐만 아니라 인터페이스 (예: System.Data.DataView, System.Collections.ArrayList, 또는 System.Collections.Hashtable). 적절 한 데이터 원본 유형에 GridView 컨트롤을 바인딩하려면 다음 방법 중 하나를 사용 합니다.

- 데이터 소스 컨트롤에 바인딩할 데이터 소스 컨트롤의 ID 값을 GridView 컨트롤의 DataSourceID 속성을 설정 합니다. GridView 컨트롤 지정 된 데이터 소스 컨트롤에 자동으로 바인딩하고 활용 데이터 소스의 정렬, 업데이트, 삭제 및 페이징 기능을 수행 하는 컨트롤의 기능입니다. 이것은 데이터 바인딩할 기본 방법입니다.
- System.Collections.IEnumerable 인터페이스를 구현 하는 데이터 원본에 바인딩할 하려면 프로그래밍 방식으로 데이터 원본에 GridView 컨트롤의 DataSource 속성을 설정 하 고 DataBind 메서드를 호출 합니다. 이 메서드를 사용 하면 기본 제공 정렬, 업데이트, 삭제 및 페이징 기능 GridView 컨트롤을 제공 하지 않습니다. 이 기능을 직접 제공 해야 합니다.

## <a name="data-operations"></a>데이터 작업

GridView 컨트롤 정렬, 업데이트, 삭제, 선택 및 컨트롤의 항목을 통해 페이지를 사용할 수 있는 많은 기본 기능을 제공 합니다. GridView 컨트롤 데이터 소스 컨트롤에 바인딩되면 GridView 컨트롤 데이터 소스 컨트롤의 기능을 활용 하 고 자동 정렬, 업데이트 및 삭제 기능을 제공할 수 있습니다.

> [!NOTE]
> GridView 컨트롤 정렬, 업데이트 및 다른 유형의 데이터 원본 삭제에 대 한 지원을 제공할 수 있습니다. 그러나 이러한 작업에 대 한 구현을 사용 하 여 적절 한 이벤트 처리기를 제공 해야 합니다.


정렬 열의 머리글을 클릭 하 여 특정 열에 대해 GridView 컨트롤에서 항목을 정렬 하는 사용자 수 있습니다. 정렬 기능을 사용 하려면 AllowSorting 속성을 설정 **true**합니다.

자동 업데이트, 삭제 및 선택 기능 때 단추를 사용할 수는 **ButtonField** 또는 **TemplateField** 명령 이름이 "편집", "Delete" 및 "Select"의 열 필드 각각를 클릭 합니다. GridView 컨트롤에서 자동으로 추가할 수는 **CommandField** 열 필드를 편집, 삭제 또는 AutoGenerateEditButton, AutoGenerateDeleteButton, 또는 AutoGenerateSelectButton 속성 에설정된경우선택단추를사용하여**true**, 각각.

> [!NOTE]
> 직접 GridView 컨트롤에서 데이터 원본에 레코드를 삽입 지원 되지 않습니다. 그러나 FormView 컨트롤을 GridView 컨트롤 DetailsView와 함께에서 사용 하 여 레코드를 삽입 하는 것이 같습니다.


동시에 데이터 원본의 모든 레코드를 표시를 하는 대신 GridView 컨트롤 자동으로 분할할 수 레코드 페이지에 있습니다. 페이징을 사용 하도록 설정, AllowPaging 속성을 설정 **true**합니다.

## <a name="customizing-the-user-interface"></a>사용자 인터페이스 사용자 지정

컨트롤의 여러 부분에 대 한 스타일 속성을 설정 하 여 GridView 컨트롤의 모양을 사용자 지정할 수 있습니다. 다음 표에서 다양 한 스타일 속성을 나열합니다.

| **스타일 속성** | **설명** |
| --- | --- |
| AlternatingRowStyle | GridView 컨트롤에 교대로 반복 되는 데이터 행 스타일 설정입니다. RowStyle 설정을 교대로 데이터 행을 표시할 때이 속성을 설정 하며 **AlternatingRowStyle** 설정 합니다. |
| EditRowStyle | GridView 컨트롤에서 편집 되는 행의 스타일 설정입니다. |
| EmptyDataRowStyle | 데이터 소스에 레코드가 없을 때 GridView 컨트롤에 표시 되는 빈 데이터 행의 스타일 설정입니다. |
| FooterStyle | GridView 컨트롤의 바닥글 행의 스타일 설정입니다. |
| HeaderStyle | GridView 컨트롤의 머리글 행의 스타일 설정입니다. |
| PagerStyle | GridView 컨트롤의 페이저 행의 스타일 설정입니다. |
| RowStyle | GridView 컨트롤의 데이터 행의 스타일 설정입니다. 경우는 **AlternatingRowStyle** 속성도 설정 됩니다, 데이터 행을 교대로 표시 됩니다는 **RowStyle** 설정 및 **AlternatingRowStyle** 설정 합니다. |
| SelectedRowStyle | GridView 컨트롤에서 선택한 행의 스타일 설정입니다. |

또한 표시 하거나 컨트롤의 다른 파트를 숨길 수 있습니다. 다음 표에서 표시 하거나 숨길는 부분을 제어 하는 속성을 보여 줍니다.

| **Property** | **설명** |
| --- | --- |
| ShowFooter | 표시 하거나 GridView 컨트롤의 바닥글 구역을 숨깁니다. |
| ShowHeader | 표시 하거나 머리글 구역에 GridView 컨트롤을 숨깁니다. |

### <a name="events"></a>이벤트

GridView 컨트롤에 대해 프로그래밍할 수 있는 몇 가지 이벤트를 제공 합니다. 이렇게 하면 이벤트가 발생할 때마다 사용자 지정 루틴을 실행할 수 있습니다. 다음 표에서 GridView 컨트롤에서 지원 되는 이벤트를 나열 합니다.

| **Event** | **설명** |
| --- | --- |
| PageIndexChanged | 페이저 단추 중 하나를 클릭할 때 GridView 컨트롤 페이징 작업을 처리 한 후 발생 합니다. 이 이벤트는 사용자가 컨트롤에서 다른 페이지로 이동한 후 작업을 수행 해야 할 경우에 주로 사용 됩니다. |
| PageIndexChanging | 페이저 단추 중 하나를 클릭 하지만 GridView 전에 컨트롤이 페이징 작업을 처리 하는 경우 발생 합니다. 이 이벤트는 페이징 작업을 취소 하는 경우가 많습니다. |
| RowCancelingEdit | 편집 모드를 종료 GridView 컨트롤 앞 행의 취소 단추를 클릭할 경우 발생 합니다. 이 이벤트는 대개 취소 작업을 중지 합니다. |
| RowCommand | GridView 컨트롤에서 단추를 클릭할 때 발생 합니다. 이 이벤트는 대개 컨트롤에서 단추를 클릭 하면 작업을 수행 합니다. |
| RowCreated | GridView 컨트롤에서 새 행을 만들 때 발생 합니다. 이 이벤트는 대개 행 만들어질 때 행의 내용을 수정 합니다. |
| RowDataBound | 데이터 행을 GridView 컨트롤의 데이터에 바인딩될 때 발생 합니다. 이 이벤트는 대개 행 데이터에 바인딩될 때 행의 내용을 수정 합니다. |
| RowDeleted | 행의 삭제 단추를 클릭할 때 GridView 컨트롤 데이터 소스의 레코드를 삭제 한 후 발생 합니다. 이 이벤트는 대개 삭제 작업의 결과 확인 합니다. |
| RowDeleting | 행의 삭제 단추를 클릭 하지만 전에 GridView 컨트롤이 데이터 소스에서 레코드를 삭제 하는 경우 발생 합니다. 이 이벤트는 삭제 작업을 취소 하는 경우가 많습니다. |
| RowEditing | 컨트롤의 편집 모드로 전환 GridView 하기 전에 행의 편집 단추를 클릭할 경우 발생 합니다. 이 이벤트는 편집 작업을 취소 하는 경우가 많습니다. |
| RowUpdated | 행의 업데이트 단추를 클릭할 때 GridView 컨트롤이 행을 업데이트 한 후 발생 합니다. 이 이벤트는 대개 업데이트 작업의 결과 확인 합니다. |
| RowUpdating | 행의 업데이트 단추를 클릭 하지만 전에 GridView 컨트롤이 행을 업데이트 하는 경우 발생 합니다. 이 이벤트는 업데이트 작업을 취소 하는 경우가 많습니다. |
| SelectedIndexChanged | 행의 선택 단추를 클릭할 때 GridView 컨트롤에서 선택 작업을 처리 한 후 발생 합니다. 이 이벤트는 대개 컨트롤에서 행을 선택한 후 작업을 수행 합니다. |
| SelectedIndexChanging | 행의 선택 단추를 클릭 하지만 GridView 이전 컨트롤이 선택 작업을 처리 하는 경우 발생 합니다. 이 이벤트는 종종 선택 작업을 취소 하려면 사용 합니다. |
| 정렬 | 열을 정렬 하는 하이퍼링크를 클릭할 때 GridView 컨트롤이 정렬 작업을 처리 한 후 발생 합니다. 이 이벤트는 사용자가 열을 정렬 하는 하이퍼링크를 클릭 한 후 작업을 수행 하려면 일반적으로 사용 됩니다. |
| 정렬 | 열을 정렬 하는 하이퍼링크를 클릭 하지만 GridView 전에 컨트롤이 정렬 작업을 처리 하는 경우 발생 합니다. 이 이벤트는 정렬 작업을 취소 하거나 정렬 루틴을 사용자 지정 하는 데 자주 사용 됩니다. |

## <a name="formview"></a>FormView

FormView 컨트롤이 데이터 원본에서 단일 레코드가 표시 됩니다. 비슷합니다 DetailsView 컨트롤 행 필드 대신 사용자 정의 템플릿을 표시 합니다. 사용자 고유의 템플릿 만들기 하면 더욱 유연 하 게 데이터가 표시 되는 방식을 제어 합니다. FormView 컨트롤이 다음 기능을 지원 합니다.

- 데이터 소스 컨트롤, SqlDataSource 및 ObjectDataSource 같은 바인딩.
- 기본 제공 삽입 기능입니다.
- 기본 제공 업데이트 및 삭제 기능입니다.
- 기본 제공 페이징 기능입니다.
- 동적으로 속성을 설정 하려면 FormView 개체 모델에 대 한 프로그래밍 방식으로 액세스 이벤트를 처리 등에입니다.
- 사용자 정의 템플릿을, 테마 및 스타일을 통해 모양을 사용자 지정할 수 있습니다.

## <a name="templates"></a>템플릿

FormView 컨트롤 콘텐츠를 표시 하는 컨트롤의 다른 부분에 대 한 템플릿 만들기 해야 합니다. 대부분의 템플릿은 선택 사항입니다. 그러나 컨트롤이 구성 모드에 대 한 템플릿을 만들어야 합니다. 예를 들어, 레코드 삽입을 지 원하는 FormView 컨트롤에 정의 된 삽입 항목 템플릿이 있어야 합니다. 다음 표에서 만들 수 있는 다양 한 템플릿을 나열 합니다.

| **템플릿 형식** | **설명** |
| --- | --- |
| EditItemTemplate | FormView 컨트롤이 편집 모드에 있을 때 데이터 행에 대 한 콘텐츠를 정의 합니다. 이 서식 파일에는 일반적으로 입력 컨트롤과 명령 단추가 있는 사용자가 기존 레코드를 편집할 수 포함 되어 있습니다. |
| 있도록 EmptyDataTemplate | FormView 컨트롤이 모든 레코드를 포함 하지 않는 데이터 원본에 바인딩되어 있을 때 표시 되는 빈 데이터 행에 대 한 콘텐츠를 정의 합니다. 이 템플릿은 일반적으로 데이터 소스에 레코드가 없는지 사용자 경고는 콘텐츠를 포함 합니다. |
| 먼저 | 바닥글 행에 대 한 콘텐츠를 정의합니다. 이 템플릿은 일반적으로 바닥글 행에 표시 하려는 모든 추가 콘텐츠를 포함 합니다. 대신 단순히 FooterText 속성을 설정 하 여 바닥글 행에 표시할 텍스트를 지정할 수 있습니다. |
| HeaderTemplate | 머리글 행에 대 한 콘텐츠를 정의합니다. 이 템플릿은 일반적으로 머리글 행에 표시 하려는 모든 추가 콘텐츠를 포함 합니다. 대신 단순히 HeaderText 속성을 설정 하 여 머리글 행에 표시할 텍스트를 지정할 수 있습니다. |
| ItemTemplate | FormView 컨트롤이 읽기 전용 모드에 있을 때 데이터 행에 대 한 콘텐츠를 정의 합니다. 이 템플릿은 일반적으로 기존 레코드의 값을 표시할 수 있는 콘텐츠를 포함 합니다. |
| InsertItemTemplate | FormView 컨트롤이 삽입 모드에 있을 때 데이터 행에 대 한 콘텐츠를 정의 합니다. 이 일반적으로 템플릿에 입력 컨트롤과 명령 단추가 있는 사용자는 새 레코드를 추가할 수 있습니다. |
| PagerTemplate | 페이징 기능을 사용 하는 경우 표시 되는 페이저 행에 대 한 콘텐츠 정의 (AllowPaging 속성이로 설정 된 경우 **true**). 일반적으로이 템플릿을 다른 레코드를 탐색할 수 있는 사용자 컨트롤을 포함 합니다. |

항목 템플릿 편집 및 삽입 항목 템플릿이 입력된 컨트롤 양방향 바인딩 식을 사용 하 여 데이터 원본의 필드를 바인딩할 수 있습니다. 따라서 FormView 컨트롤이 자동으로 업데이트에 대 한 입력된 컨트롤의 값을 추출 또는 삽입 작업을 수 있습니다. 또한 양방향 바인딩 식 편집 항목 템플릿에서 자동으로 필드의 원래 값을 표시 하려면 입력된 컨트롤을 수 있습니다.

### <a name="binding-to-data"></a>데이터 바인딩

FormView 컨트롤이 데이터 소스 컨트롤을 바인딩할 수 있습니다 (같은 **SqlDataSource**, AccessDataSource **ObjectDataSource** 등), 또는 구현 하는 모든 데이터 원본에는 (예: System.Data.DataView, System.Collections.ArrayList, System.Collections.Hashtable) System.Collections.IEnumerable 인터페이스입니다. FormView 컨트롤이 해당 데이터 원본 형식에 바인딩할 다음 방법 중 하나를 사용 합니다.

- 데이터 소스 컨트롤에 바인딩할 데이터 소스 컨트롤의 ID 값을로 FormView 컨트롤의 DataSourceID 속성을 설정 합니다. FormView 컨트롤이 자동으로 지정 된 데이터 소스 컨트롤에 바인딩합니다 되며 활용할 수 있습니다 데이터 원본의 삽입, 업데이트, 삭제 및 페이징 기능을 수행 하는 컨트롤의 기능입니다. 이것은 데이터 바인딩할 기본 방법입니다.
- 구현 하는 데이터 원본에 바인딩하는 **System.Collections.IEnumerable** 인터페이스 프로그래밍 방식으로 데이터 원본에 FormView 컨트롤의 DataSource 속성을 설정 하 고 DataBind 메서드를 호출 합니다. 이 메서드를 사용 하면 기본 삽입, 업데이트, 삭제 및 페이징 기능 FormView 컨트롤이 제공 하지 않습니다. 적절 한 이벤트를 사용 하 여이 기능을 제공 해야 합니다.

## <a name="data-operations"></a>데이터 작업

FormView 컨트롤이 업데이트, 삭제, 삽입 및 컨트롤의 항목을 통해 페이지를 사용할 수 있는 많은 기본 기능을 제공 합니다. FormView 컨트롤이 데이터 소스 컨트롤에 바인딩되면 FormView 컨트롤이 데이터 소스 컨트롤의 기능을 활용 하 고 자동 업데이트, 삭제, 삽입 및 페이징 기능을 제공할 수 있습니다. FormView 컨트롤이 update, delete, insert 및 다른 유형의 데이터 원본에 대 한 페이징 작업에 대 한 지원을 제공할 수 있습니다. 그러나 이러한 작업에 대 한 구현을 사용 하 여 적절 한 이벤트 처리기를 제공 해야 합니다.

FormView 컨트롤 템플릿을 사용 하 여, 때문에 자동으로 업데이트, 삭제 또는 삽입 작업을 수행 하기 위해 명령 단추를 생성 하는 방법은 제공 하지 않습니다. 이러한 명령 단추에서 적절 한 템플릿을 수동으로 포함 해야 합니다. FormView 컨트롤이 있는 특정 단추 인식 자신의 **CommandName** 속성이 특정 값으로 설정 합니다. 다음 표에서 FormView 컨트롤이 인식 하는 명령 단추를 보여 줍니다.

| **Button** | **Commandname 값** | **설명** |
| --- | --- | --- |
| 취소 | "취소" | 작업을 취소 하 고 사용자가 입력 한 값을 삭제 하려면 업데이트 또는 삽입 작업에 사용 합니다. FormView 컨트롤이 DefaultMode 속성에 지정 된 모드를 반환 합니다. |
| 삭제 | "Delete" | 삭제 작업에 데이터 소스에서 표시 된 레코드를 삭제 하는 데 사용 합니다. ItemDeleting 및 ItemDeleted 이벤트를 발생 시킵니다. |
| 편집 | "Edit" | 업데이트 작업에 FormView 컨트롤이 편집 모드로 전환 하는 데 사용 합니다. 에 지정 된 콘텐츠를 **EditItemTemplate** 데이터 행에 대 한 속성이 표시 됩니다. |
| Insert | "Insert" | 삽입 작업에 사용자가 입력 한 값을 사용 하 여 데이터 원본에 새 레코드를 삽입 하려고 하는 데 사용 합니다. ItemInserting 및 ItemInserted 이벤트를 발생 시킵니다. |
| 새로 만들기 | "New" | FormView 컨트롤이 삽입 모드에 삽입할 삽입 작업에 사용 합니다. 에 지정 된 콘텐츠를 **먼저** 데이터 행에 대 한 속성이 표시 됩니다. |
| 페이지 | "Page" | 페이징 작업에서는 페이징을 수행 하는 페이저 행에 단추를 나타내는 하는 데 사용 합니다. 페이징 작업을 지정 하려면 다음을 설정 합니다 **CommandArgument** 속성을 "다음", "이전", "First", "지난" 또는 탐색 하는 페이지의 인덱스입니다. PageIndexChanged 및 PageIndexChanging 이벤트를 발생 시킵니다. |
| 업데이트 | "업데이트" | 사용자가 입력 한 값을 사용 하 여 데이터 원본에 표시 된 레코드를 업데이트 하기 위해 업데이트 작업에 사용 합니다. ItemUpdating 및 ItemUpdated 이벤트를 발생 시킵니다. |

삭제와 달리 단추 (삭제 표시 된 레코드 즉시)를 편집 하거나 새로 만들기 단추를 클릭 하면 편집 컨트롤이 전환 FormView 또는 모드 각각 삽입 합니다. 에 포함 된 콘텐츠 편집 모드에는 **EditItemTemplate** 현재 데이터 항목에 대 한 속성이 표시 됩니다. 일반적으로 항목 템플릿 편집 편집 단추를 업데이트 및 취소 단추를 사용 하 여 바뀝니다 되도록 정의 됩니다. 또한 일반적으로 수정 하려면 사용자에 대 한 필드의 값 필드의 데이터 형식 (예: 입력란 또는 확인란 컨트롤)에 대 한 적절 한 입력된 컨트롤이 표시 됩니다. 모든 변경 사항이 취소 단추를 클릭 데이터 원본에서 레코드를 업데이트 [업데이트] 단추를 클릭 합니다.

에 들어 있는 콘텐츠에 마찬가지로 합니다 **먼저** 컨트롤이 삽입 모드에 있을 때 데이터 항목에 대 한 속성이 표시 됩니다. 삽입 항목 템플릿에 새 단추 삽입 및 취소 단추를 사용 하 여 대체 되 고 빈 입력된 컨트롤이 새 레코드에 대 한 값을 입력 하 여 사용자에 대해 표시 되는 일반적으로 정의 됩니다. 취소 단추를 클릭 하면 모든 변경 사항이 데이터 원본에서 레코드를 삽입 삽입 단추를 클릭 합니다.

FormView 컨트롤이 데이터 소스에서 다른 레코드를 탐색할 수 있도록 하는 페이징 기능을 제공 합니다. 사용 하도록 설정 하면 페이지 탐색 컨트롤을 포함 하는 FormView 컨트롤의 페이저 행을 표시 됩니다. 페이징에 사용 하도록 설정 합니다 **AllowPaging** 속성을 **true**합니다. PagerSettings 속성과 PagerStyle에 포함 된 개체의 속성을 설정 하 여 페이저 행을 사용자 지정할 수 있습니다. 기본 제공 페이저 행 UI를 사용 하는 대신 고유한 UI를 사용 하 여 만들 수 있습니다 합니다 **PagerTemplate** 속성입니다.

## <a name="customizing-the-user-interface"></a>사용자 인터페이스 사용자 지정

컨트롤의 여러 부분에 대 한 스타일 속성을 설정 하 여 FormView 컨트롤의 모양을 사용자 지정할 수 있습니다. 다음 표에서 다양 한 스타일 속성을 나열합니다.

| **스타일 속성** | **설명** |
| --- | --- |
| EditRowStyle | FormView 컨트롤의 경우 데이터 행의 스타일 설정을 편집 모드입니다. |
| EmptyDataRowStyle | 데이터 소스에 레코드가 없을 때 FormView 컨트롤에 표시 되는 빈 데이터 행의 스타일 설정입니다. |
| FooterStyle | FormView 컨트롤의 바닥글 행의 스타일 설정입니다. |
| HeaderStyle | FormView 컨트롤의 머리글 행의 스타일 설정입니다. |
| InsertRowStyle | FormView 컨트롤의 경우 데이터 행의 스타일 설정을 삽입 모드입니다. |
| PagerStyle | 페이징 기능을 사용 하는 경우 FormView 컨트롤에 표시 되는 페이저 행의 스타일 설정입니다. |
| RowStyle | FormView 컨트롤이 읽기 전용 모드에 있을 때 데이터 행의 스타일 설정입니다. |

## <a name="events"></a>이벤트

FormView 컨트롤에 대해 프로그래밍할 수 있는 몇 가지 이벤트를 제공 합니다. 이렇게 하면 이벤트가 발생할 때마다 사용자 지정 루틴을 실행할 수 있습니다. 다음 표에서 FormView 컨트롤에서 지원 되는 이벤트를 나열 합니다.

| **Event** | **설명** |
| --- | --- |
| ItemCommand | FormView 컨트롤에 단추를 클릭할 때 발생 합니다. 이 이벤트는 대개 컨트롤에서 단추를 클릭 하면 작업을 수행 합니다. |
| ItemCreated | FormView 컨트롤의 모든 FormViewRow 개체가 만들어진 후 발생 합니다. 이 이벤트는 대개 표시 되기 전에 레코드의 값을 수정 합니다. |
| ItemDeleted | 경우 삭제 단추 (단추를 사용 하 여 해당 **CommandName** 속성이 "Delete"로 설정)를 클릭 하면 되지만 FormView 컨트롤이 데이터 소스에서 레코드를 삭제 한 후 합니다. 이 이벤트는 대개 삭제 작업의 결과 확인 합니다. |
| ItemDeleting | FormView 전에 컨트롤이 데이터 소스에서 레코드를 삭제 하지만 삭제 단추를 클릭할 때 발생 합니다. 이 이벤트는 삭제 작업을 취소 하려면 종종 사용 됩니다. |
| ItemInserted | 경우 삽입 단추 (단추를 사용 하 여 해당 **CommandName** "Insert"로 설정 하는 속성)를 클릭 하면 되지만 FormView 컨트롤이 레코드를 삽입 한 후입니다. 이 이벤트는 대개 삽입 작업의 결과 확인 합니다. |
| ItemInserting | FormView 전에 레코드를 삽입 하지만 삽입 단추를 클릭할 때 발생 합니다. 이 이벤트는 삽입 작업을 취소 하려면 종종 사용 됩니다. |
| ItemUpdated | 경우 업데이트 단추 (단추를 사용 하 여 해당 **CommandName** "Update"로 설정 하는 속성)를 클릭 하면 되지만 FormView 컨트롤이 행을 업데이트 한 후 합니다. 이 이벤트는 대개 업데이트 작업의 결과 확인 합니다. |
| ItemUpdating | FormView 전에 레코드를 업데이트 하지만 업데이트 단추를 클릭할 때 발생 합니다. 이 이벤트는 업데이트 작업을 취소 하는 경우가 많습니다. |
| ModeChanged | FormView 컨트롤 모드를 변경한 후 발생 (하 고 편집, 삽입, 읽기 전용 모드). 이 이벤트는 대개 FormView 컨트롤 모드를 변경 하면 작업을 수행 합니다. |
| ModeChanging | FormView 컨트롤 모드를 변경 하기 전에 발생 (하 고 편집, 삽입, 읽기 전용 모드). 이 이벤트는 종종 모드 변경을 취소 하려면 사용 합니다. |
| PageIndexChanged | 페이저 단추 중 하나를 클릭할 때 FormView 컨트롤이 페이징 작업을 처리 한 후 발생 합니다. 이 이벤트는 사용자가 컨트롤의 다른 레코드를 탐색 한 후 작업을 수행 해야 할 경우에 주로 사용 됩니다. |
| PageIndexChanging | 페이저 단추 중 하나를 클릭 하지만 FormView 전에 컨트롤이 페이징 작업을 처리 하는 경우 발생 합니다. 이 이벤트는 페이징 작업을 취소 하는 경우가 많습니다. |

## <a name="detailsview"></a>DetailsView

DetailsView 컨트롤은 레코드의 각 필드를 테이블의 행에 표시 되는 위치 테이블의 데이터 원본에서 단일 레코드를 표시할 사용 됩니다. 마스터-세부 시나리오에 GridView 컨트롤을 함께 사용할 수 있습니다. DetailsView 컨트롤에는 다음 기능을 지원 합니다.

- SqlDataSource와 같은 소스 컨트롤, 데이터 바인딩.
- 기본 제공 삽입 기능입니다.
- 기본 제공 업데이트 및 삭제 기능입니다.
- 기본 제공 페이징 기능입니다.
- 동적으로 속성을 설정 하려면 DetailsView 개체 모델에 대 한 프로그래밍 방식 액세스 이벤트를 처리 등에입니다.
- 테마 및 스타일을 통해 모양을 사용자 지정할 수 있습니다.

## <a name="row-fields"></a>행 필드

DetailsView 컨트롤에서 각 데이터 행 필드 컨트롤을 선언 하 여 만들어집니다. 컨트롤의 행의 동작을 결정 하는 다른 행 필드 형식입니다. 필드 컨트롤 DataControlField에서 파생 됩니다. 다음 표에서 사용할 수 있는 다른 행 필드 유형을 나열 합니다.

| **열 필드 형식** | **설명** |
| --- | --- |
| BoundField | 데이터 원본에서 필드의 값을 텍스트로 표시합니다. |
| ButtonField | DetailsView 컨트롤에서 명령 단추를 표시합니다. 이렇게 하면 추가 또는 제거 단추 등의 사용자 지정 단추 컨트롤을 사용 하 여 행을 표시할 수 있습니다. |
| CheckBoxField | DetailsView 컨트롤에서 확인란을 표시합니다. 이 행 필드 형식은 부울 값을 사용 하 여 필드를 표시 하려면 일반적으로 사용 됩니다. |
| CommandField | 기본 제공 명령 표시 편집을 수행 하는 단추 삽입 또는 삭제 DetailsView 컨트롤에서 작업 합니다. |
| HyperLinkField | 하이퍼링크로 데이터 원본의 필드의 값을 표시합니다. 이 행 필드 형식을 사용 하면 두 번째 필드 하이퍼링크의 URL에 바인딩할 수 있습니다. |
| ImageField | DetailsView 컨트롤에서 이미지를 표시합니다. |
| TemplateField | 지정한 템플릿에 따라 DetailsView 컨트롤에서 행에 대 한 사용자 정의 내용을 표시 합니다. 이 행 필드 형식에는 사용자 지정 행 필드를 만들 수 있습니다. |

기본적으로 AutoGenerateRows 속성 설정 **true**, 데이터 원본에 바인딩할 수 있는 형식의 각 필드에 대 한 바인딩된 행 필드를 자동으로 생성 합니다. 올바른 바인딩 가능한 유형은 문자열, DateTime, Decimal, Guid 및 기본 형식 집합입니다. 각 필드 데이터 소스의 각 필드 표시 되는 순서 대로 텍스트로 행에 표시 됩니다.

자동으로 생성 되는 행 레코드의 모든 필드를 표시 하는 빠르고 쉬운 방법을 제공 합니다. 그러나 DetailsView를 사용 하 여 컨트롤의 고급 DetailsView 컨트롤에 포함할 행 필드를 명시적으로 선언 해야 하는 기능이 있습니다. 행 필드를 선언 하려면 먼저 설정 합니다 **AutoGenerateRows** 속성을 **false**합니다. 다음으로 열기 및 닫기 추가 **&lt;필드&gt;** 와 DetailsView 컨트롤의 닫는 태그 사이입니다. 마지막으로 열고 닫는 간의 포함 시킬 행 필드를 나열 합니다. **&lt;필드&gt;** 태그입니다. 지정 된 행 필드를 나열 된 순서로 Fields 컬렉션에 추가 됩니다. 합니다 **필드** 컬렉션 DetailsView 컨트롤에서 행 필드를 프로그래밍 방식으로 관리할 수 있습니다.

> [!NOTE]
> 자동으로 생성 된 행 필드 Fields 컬렉션에 추가 되지 않습니다.


## <a name="binding-to-data"></a>데이터 바인딩

DetailsView 컨트롤에 바인딩될 수는 데이터 소스 제어와 같은 **SqlDataSource** 또는 AccessDataSource, 또는 System.Data.DataView, 같은 System.Collections.IEnumerable 인터페이스를 구현 하는 모든 데이터 원본 System.Collections.ArrayList 및 System.Collections.Hashtable 합니다.

적절 한 데이터 원본 유형에 DetailsView 컨트롤을 바인딩하려면 다음 방법 중 하나를 사용 합니다.

- 데이터 소스 컨트롤에 바인딩할 데이터 소스 컨트롤의 ID 값을로 DetailsView 컨트롤의 DataSourceID 속성을 설정 합니다. DetailsView 컨트롤은 자동으로 지정 된 데이터 소스 컨트롤에 바인딩합니다. 이것은 데이터 바인딩할 기본 방법입니다.
- 구현 하는 데이터 원본에 바인딩하는 **System.Collections.IEnumerable** 인터페이스 프로그래밍 방식으로 데이터 원본에 DetailsView 컨트롤의 DataSource 속성을 설정 하 고 DataBind 메서드를 호출 합니다.

## <a name="security"></a>보안

악성 클라이언트 스크립트 포함 될 수 있는 사용자 입력을 표시 하려면이 제어를 사용할 수 있습니다. 응용 프로그램에서 표시 하기 전에 실행 스크립트, SQL 문 또는 다른 코드에 대 한 클라이언트에서 전송 되는 모든 정보를 확인 합니다. ASP.NET에서는 사용자 입력에서 차단 스크립트를 HTML 입력된 요청 유효성 검사 기능을 제공 합니다.

## <a name="data-operations"></a>데이터 작업

DetailsView 컨트롤 업데이트, 삭제, 삽입 및 컨트롤의 항목을 통해 페이지를 사용할 수 있는 기본 기능을 제공 합니다. DetailsView 컨트롤 데이터 소스 컨트롤에 바인딩되면 DetailsView 컨트롤 데이터 소스 컨트롤의 기능을 활용 하 고 자동 업데이트, 삭제, 삽입 및 페이징 기능을 제공할 수 있습니다.

DetailsView 컨트롤 update, delete, insert 및 다른 유형의 데이터 원본에 대 한 페이징 작업에 대 한 지원을 제공할 수 있습니다. 그러나 적절 한 이벤트 처리기에서 이러한 작업에 대 한 구현을 제공 해야 합니다.

DetailsView 컨트롤에서 자동으로 추가할 수는 **CommandField** AutoGenerateEditButton,AutoGenerateDeleteButton,또는AutoGenerateInsertButton속성을설정하여편집,삭제또는새로만들기단추를사용하여행필드**true**, 각각. 삭제와 달리 단추 (는 선택한 레코드를 즉시 삭제)를 편집 하거나 새로 만들기 단추를 클릭할 때 DetailsView 컨트롤이 전환 편집 또는 삽입 모드를 각각. 편집 모드에 대 한 업데이트 및 취소 단추를 사용 하 여 편집 단추가 바뀝니다. 필드의 데이터 형식 (예: 입력란 또는 확인란 컨트롤)에 대 한 적절 한 입력된 컨트롤이 수정 하려면 사용자에 대 한 필드의 값을 사용 하 여 표시 됩니다. 모든 변경 사항이 취소 단추를 클릭 데이터 원본에서 레코드를 업데이트 [업데이트] 단추를 클릭 합니다. 마찬가지로, 삽입 모드에서 새 단추 삽입 및 취소 단추를 사용 하 여 대체 되 고 새 레코드에 대 한 값을 입력 하 여 사용자에 대 한 빈 입력된 컨트롤이 표시 됩니다.

DetailsView 컨트롤 데이터 소스의 다른 레코드를 탐색할 수 있도록 하는 페이징 기능을 제공 합니다. 사용 하도록 설정 하면 페이지 탐색 컨트롤 페이저 행에 표시 됩니다. 페이징을 사용 하도록 설정, AllowPaging 속성을 설정 **true**합니다. 페이저 행 PagerStyle 및 PagerSettings 속성을 사용 하 여 사용자 지정할 수 있습니다.

## <a name="customizing-the-user-interface"></a>사용자 인터페이스 사용자 지정

컨트롤의 여러 부분에 대 한 스타일 속성을 설정 하 여 DetailsView 컨트롤의 모양을 사용자 지정할 수 있습니다. 다음 표에서 다양 한 스타일 속성을 나열합니다.

| **스타일 속성** | **설명** |
| --- | --- |
| AlternatingRowStyle | DetailsView 컨트롤에서 교대로 반복 되는 데이터 행의 스타일 설정입니다. RowStyle 설정을 교대로 데이터 행을 표시할 때이 속성을 설정 하며 **AlternatingRowStyle** 설정 합니다. |
| CommandRowStyle | DetailsView 컨트롤에서 기본 제공 명령 단추가 포함 된 행의 스타일 설정입니다. |
| EditRowStyle | DetailsView 컨트롤의 경우 데이터 행에 대 한 스타일 설정을 편집 모드입니다. |
| EmptyDataRowStyle | 데이터 소스에 레코드가 없을 때 DetailsView 컨트롤에서 표시 되는 빈 데이터 행의 스타일 설정입니다. |
| FooterStyle | DetailsView 컨트롤의 바닥글 행의 스타일 설정입니다. |
| HeaderStyle | DetailsView 컨트롤의 머리글 행의 스타일 설정입니다. |
| InsertRowStyle | DetailsView 컨트롤의 경우 데이터 행에 대 한 스타일 설정을 삽입 모드입니다. |
| PagerStyle | DetailsView 컨트롤의 페이저 행의 스타일 설정입니다. |
| RowStyle | DetailsView 컨트롤에서 데이터 행의 스타일 설정입니다. 경우는 **AlternatingRowStyle** 속성도 설정 됩니다, 데이터 행을 교대로 표시 됩니다는 **RowStyle** 설정 및 **AlternatingRowStyle** 설정 합니다. |
| FieldHeaderStyle | DetailsView 컨트롤의 헤더 열에 대 한 스타일 설정입니다. |

## <a name="events"></a>이벤트

DetailsView 컨트롤에 대해 프로그래밍할 수 있는 몇 가지 이벤트를 제공 합니다. 이렇게 하면 이벤트가 발생할 때마다 사용자 지정 루틴을 실행할 수 있습니다. 다음 표에서 DetailsView 컨트롤에서 지원 되는 이벤트를 나열 합니다. DetailsView 컨트롤 기본 클래스에서 이러한 이벤트 상속: 데이터 바인딩, 데이터 바인딩, Disposed, Init, 부하, PreRender, 및 렌더링 합니다.

| **Event** | **설명** |
| --- | --- |
| ItemCommand | DetailsView 컨트롤에서 단추를 클릭할 때 발생 합니다. |
| ItemCreated | DetailsView 컨트롤에서 모든 DetailsViewRow 개체가 만들어진 후 발생 합니다. 이 이벤트는 대개 표시 되기 전에 레코드의 값을 수정 합니다. |
| ItemDeleted | 삭제 단추를 클릭 하면 DetailsView 컨트롤이 데이터 소스에서 레코드를 삭제 한 후 발생 합니다. 이 이벤트는 대개 삭제 작업의 결과 확인 합니다. |
| ItemDeleting | 전에 DetailsView 컨트롤이 데이터 소스에서 레코드를 삭제 하지만 삭제 단추를 클릭할 때 발생 합니다. 이 이벤트는 삭제 작업을 취소 하려면 종종 사용 됩니다. |
| ItemInserted | 삽입 단추를 클릭 하면 DetailsView 컨트롤 레코드를 삽입 한 후 발생 합니다. 이 이벤트는 대개 삽입 작업의 결과 확인 합니다. |
| ItemInserting | DetailsView 전에 레코드를 삽입 하지만 삽입 단추를 클릭할 때 발생 합니다. 이 이벤트는 삽입 작업을 취소 하려면 종종 사용 됩니다. |
| ItemUpdated | 업데이트 단추를 클릭 하면 DetailsView 컨트롤이 행을 업데이트 한 후 발생 합니다. 이 이벤트는 대개 업데이트 작업의 결과 확인 합니다. |
| ItemUpdating | DetailsView 전에 레코드를 업데이트 하지만 업데이트 단추를 클릭할 때 발생 합니다. 이 이벤트는 업데이트 작업을 취소 하는 경우가 많습니다. |
| ModeChanged | DetailsView 컨트롤 (편집, 삽입 또는 읽기 전용 모드) 모드를 변경한 후에 발생 합니다. 이 이벤트는 대개 DetailsView 컨트롤 모드를 변경 하면 작업을 수행 합니다. |
| ModeChanging | DetailsView 컨트롤 (편집, 삽입 또는 읽기 전용 모드) 모드를 변경 하기 전에 발생 합니다. 이 이벤트는 종종 모드 변경을 취소 하려면 사용 합니다. |
| PageIndexChanged | 페이저 단추 중 하나를 클릭할 때 DetailsView 컨트롤이 페이징 작업을 처리 한 후 발생 합니다. 이 이벤트는 사용자가 컨트롤의 다른 레코드를 탐색 한 후 작업을 수행 해야 할 경우에 주로 사용 됩니다. |
| PageIndexChanging | 페이저 단추 중 하나를 클릭 하지만 전에 DetailsView 컨트롤 페이징 작업을 처리 하는 경우 발생 합니다. 이 이벤트는 페이징 작업을 취소 하는 경우가 많습니다. |

## <a name="the-menu-control"></a>메뉴 컨트롤

ASP.NET 2.0의 메뉴 컨트롤은 완전 한 기능의 탐색 시스템 설계 되었습니다. SiteMapDataSource와 같은 계층적 데이터 소스에 쉽게 데이터 바인딩 수 있습니다.

메뉴 컨트롤 구조를 선언적으로 또는 동적으로 정의할 수 있습니다. 그리고 단일 루트 노드와 모든 하위 노드 수가 이루어집니다. 다음 코드는 메뉴 컨트롤에 대 한 메뉴를 선언적으로 정의 합니다.

[!code-aspx[Main](data-bound-controls/samples/sample4.aspx)]

위의 예에서 Home.aspx 노드는 루트 노드입니다. 다른 모든 노드는 다양 한 수준에서 루트 노드 내에 중첩 됩니다.

메뉴 컨트롤을 렌더링할 수; 메뉴의 두 종류가 있습니다. 정적 메뉴와 동적 메뉴입니다. 정적 메뉴의 항상 표시 되는 메뉴 항목으로 구성 됩니다. 동적 메뉴 위로 마우스로 가리킬 때만 표시 됩니다는 메뉴 항목으로 구성 합니다. 고객 수 선언적으로 정의 하는 메뉴가 있는 정적 메뉴 및 런타임에 데이터 바인딩된 있는 메뉴를 사용 하 여 동적 메뉴에 자주 혼동 됩니다. 사실, 동적 및 정적 메뉴의 채우기 메서드 관련 되지 않습니다. 용어 *정적* 하 고 *동적* 참조만 여부 메뉴 인지 정적으로 기본적으로 표시 된 유일한 사용자가 동작을 수행 하는 경우에 표시 합니다.

합니다 **StaticDisplayLevels** 속성 메뉴 수준의 수 정적 이며 따라서 기본적으로 표시를 구성 하는 데 사용 됩니다. 위의 예제에서는 설정 합니다 **StaticDisplayLevels** 속성 값이 2로 인해 정적으로 홈 노드, 음악 노드에 노드와 영화를 표시 하려면 메뉴. 사용자가 부모 노드를 가리킬 때 다른 모든 노드의 동적으로 표시 됩니다.

**MaximumDynamicDisplayLevels** 속성에는 최대 구성 동적 수준의 메뉴는 표시할 수 있습니다. 지정 된 값 보다 높은 수준의 동적 메뉴의 **MaximumDynamicDisplayLevels** 속성이 삭제 됩니다.

> [!NOTE]
> 것이 거의 확실 메뉴 MaximumDynamicDisplayLevels 속성으로 인해 렌더링에 표시 되지 않습니다 여기서 상황을 발생할 수 있습니다. 이러한 경우 속성에서 충분히 고객 메뉴의 표시를 허용 하도록 설정 되어 있는지 확인 합니다.


## <a name="data-binding-the-menu-control"></a>데이터 메뉴 컨트롤 바인딩

메뉴 컨트롤 고 XMLDataSource 또는 SiteMapDataSource와 같은 모든 계층적 데이터 소스에 바인딩될 수 있습니다. SiteMapDataSource는 가장 일반적으로 사용 되는 메서드 메뉴 컨트롤에 데이터 바인딩 Web.sitemap 파일에서 피드를 해당 스키마 메뉴 컨트롤에 알려진된 API를 제공 하기 때문에입니다. 아래 목록에는 간단한 Web.sitemap 파일을 보여 줍니다.

[!code-xml[Main](data-bound-controls/samples/sample5.xml)]

하나의 루트 있으면이 예에서 홈 요소가 요소 인지 확인 합니다. 각 있으면에 대 한 몇 가지 특성을 구성할 수 있습니다. 가장 자주 사용 되는 특성을 다음과 같습니다.

- **url** 사용자가 메뉴 항목을 클릭할 때 표시할 URL을 지정 합니다. 이 특성이 없는 경우 노드를 클릭할 때 단순히 게시 합니다.
- **제목** 메뉴 항목에 표시 되는 텍스트를 지정 합니다.
- **설명** 노드에 대 한 설명서로 사용 합니다. 또한 노드 위에 마우스를 가져갈 때 도구 설명으로 표시 합니다.
- **siteMapFile** 중첩 된 사이트 맵 수 있습니다. 이 특성을 제대로 구성 된 ASP.NET 사이트 맵 파일을 가리켜야 합니다.
- **역할** 노드의 모양을 ASP.NET 보안 조정을 통해 제어할 수 있습니다.

이러한 특성은 모두 선택 사항 이지만 메뉴의 동작 되지 않을 수 있음을 지정 되지 않은 경우 예상 되는 note 합니다. 예를 들어 경우는 *url* 특성을 지정 하지만 *설명* 특성, 노드를 볼 수 없게 됩니다 아니며 없으므로 지정 된 URL로 이동 됩니다.

## <a name="controlling-a-menus-operation"></a>메뉴 작업을 제어합니다.

속성이 ASP.NET Menu 컨트롤;의 작업에 영향을 주는 몇 가지 **방향** 속성을 **DisappearAfter** 속성을는 **StaticItemFormatString** 속성 및 **StaticPopoutImageUrl**속성은 이러한 몇 가지 있습니다.

- 합니다 **방향을** 수로 설정할 수 *가로* 하거나 *세로* 정적 메뉴 항목 또는 수직 행에서 가로로 배치 되며 누적 여부를 제어 하 고 연결할 수 있습니다. 이 속성은 동적 메뉴에 영향을 주지 않습니다.
- 합니다 **DisappearAfter** 속성이 기간으로 동적 메뉴를 계속 표시 마우스 후 구성 떨어져 있는 것입니다. 값은 밀리초에서 500 기본값으로 지정 됩니다. 이 속성 값이-1 설정 하면 자동으로 사라집니다 되지 메뉴. 이런 경우 메뉴는 메뉴 외부를 클릭할 때에 사라집니다.
- 합니다 **StaticItemFormatString** 속성을 사용 하면 일관 된 스크립트를 사용 하면 메뉴 시스템에서 유지 관리 하기 쉬운 합니다. 이 속성을 지정 하는 경우 *{0}* 대신 데이터 원본에 표시 되는 설명을 입력 해야 합니다. 예를 들어, 실습 1 say 당사의 제품 페이지 방문에서 메뉴 항목 등을 위해서는 지정 방문이 {0} 는 StaticItemFormatString 페이지입니다. 런타임에 ASP.NET 모두 바뀝니다의 {0} 메뉴 항목에 대 한 올바른 설명 합니다.
- 합니다 **StaticPopoutImageUrl** 속성 특정 메뉴 노드가 있는 가리키면 액세스할 수 있는 자식 노드를 나타내는 데 사용 되는 이미지를 지정 합니다. 동적 메뉴 계속 기본 이미지를 사용 합니다.

## <a name="templated-menu-controls"></a>템플릿 기반 메뉴 컨트롤

메뉴 컨트롤은 템플릿 기반 컨트롤 및 두 개의 다른 Itemtemplate;에 대 한 허용 StaticItemTemplate 및 DynamicItemTemplate 합니다. 이러한 템플릿을 사용 하 여, 쉽게 추가할 수 있습니다 서버 컨트롤 또는 사용자 정의 컨트롤에 메뉴.

Visual Studio.NET의 서식 파일을 편집 하려면 메뉴에서 스마트 태그 단추를 클릭 하 고 템플릿 편집을 선택 하거나 합니다. 다음은 StaticItemTemplate 또는 DynamicItemTemplate 편집 선택할 수 있습니다.

StaticItemTemplate에 추가 된 모든 컨트롤 페이지를 로드할 때 정적 메뉴에 표시 됩니다. DynamicItemTemplate에 추가 된 모든 컨트롤은 모든 팝업 메뉴에 표시 됩니다.

## <a name="menu-events"></a>메뉴 이벤트

메뉴 컨트롤에 두 개의 고유한 이벤트를 적용 합니다. 합니다 **MenuItemClicked** 하며 **MenuItemDatabound** 이벤트입니다.

메뉴 항목을 클릭할 때 MenuItemClicked 이벤트가 발생 합니다. 메뉴 항목을 데이터 바인딩된 때 MenuItemDatabound 이벤트가 발생 합니다. 합니다 **MenuEventArgs** 전달 되는 이벤트 처리기는 메뉴 항목의 항목 속성을 통해 액세스를 제공 합니다.

## <a name="controlling-a-menus-appearance"></a>메뉴 모양 제어

또한 하나 이상의 서식 메뉴를 사용할 수 있는 다양 한 스타일을 사용 하는 메뉴 컨트롤의 모양을 변경할 수 있습니다. 여러 가지 방법이 **StaticMenuStyle**를 **DynamicMenuStyle**를 **DynamicMenuItemStyle**를 **DynamicSelectedStyle**, 및 **DynamicHoverStyle**합니다. 이러한 속성은 표준 HTML 스타일 문자열을 사용 하 여 구성 됩니다. 예를 들어, 다음는 동적 메뉴에 대 한 스타일을 적용 됩니다.

[!code-aspx[Main](data-bound-controls/samples/sample6.aspx)]

> [!NOTE]
> Hover 스타일 중 하나를 사용 하는 경우 추가 해야 합니다는 &lt;헤드&gt; 요소에서 사용 하 여 페이지를를 *runat* 요소로 *server*합니다.


메뉴 컨트롤에는 또한 ASP.NET 2.0 테마를 사용 하 여를 지원합니다.

## <a name="the-treeview-control"></a>TreeView 컨트롤

TreeView 컨트롤 트리 구조의 데이터를 표시합니다. 메뉴 컨트롤과 마찬가지로 쉽게 수 SiteMapDataSource와 같은 모든 계층적 데이터 소스에 바인딩된 데이터입니다.

고객에 게 ASP.NET 2.0의 TreeView 컨트롤에 대해 문의할 가능성이 있는 첫 번째 질문은 여부와 관련이 ASP.NET에 대해 사용할 수 있는 TreeView IE WebControl 1.x 합니다. 그것이 아니야. ASP.NET 2.0의 TreeView 컨트롤부터에서 쓰인 것 이며 이전에 제공 된 IE TreeView WebControl를 통해 향상을 제공 합니다.

않겠습니다 세부 정보 메뉴 컨트롤과 동일한 방식으로 수행 하는 사이트 맵에 TreeView 컨트롤을 바인딩하는 방법에 있습니다. 그러나 TreeView 컨트롤에 작동 하는 방식으로 고유한 몇 가지 차이점이 있습니다.

기본적으로 TreeView 컨트롤을 완전히 확장 된 나타납니다. 초기 로드 시 확장 수준을 변경 하려면 수정 된 **ExpandDepth** 컨트롤의 속성입니다. 이 TreeView 데이터 바인딩 시 특정 노드를 확장 하면 되는 경우에 특히 중요 합니다.

## <a name="databinding-the-treeview-control"></a>TreeView 컨트롤 데이터 바인딩

메뉴 컨트롤과 달리 TreeView에 아주 적합 많은 양의 데이터를 처리 합니다. 따라서 XMLDataSource 또는 SiteMapDataSource에 데이터 바인딩 외에도 트리 뷰에서 종종 데이터 집합 또는 다른 관계형 데이터에 바인딩된 데이터입니다. TreeView 컨트롤 많은 양의 데이터에 바인딩되는 경우에는 컨트롤에 실제로 표시 되는 데이터에만 바인딩할 적합 합니다. 데이터와 TreeView 노드는 확장 된 추가 데이터에 바인딩할 수 있습니다.

이러한 경우에는 **PopulateOnDemand** TreeView의 속성 설정 해야 *true*합니다. 에 대 한 구현을 제공 해야 합니다 **TreeNodePopulate** 메서드.

## <a name="data-binding-without-postback"></a>데이터 다시 게시 하지 않고 바인딩

처음으로 이전 예제에서 노드를 확장 하면 페이지가 다시 게시 및 새로 고침을 확인 합니다. 이 예제 에서만 문제가 아닙니다. thats 하는 것이 많은 양의 데이터를 사용 하 여 프로덕션 환경에서 상상할 수 있습니다. 더 나은 경우 하나는 트리 뷰에서 여전히 동적으로 해당 노드를 채울 하지만 서버에 다시 게시 하지 않고도 것입니다.

설정 하 여 합니다 **알** 하며 **PopulateOnDemand** 속성을 true로 ASP.NET TreeView 컨트롤을 동적으로 다시 게시 하지 않고도 노드 채워집니다. 부모 노드를 확장할 때 클라이언트에서는 XMLHttp 요청이 만들어지고 OnTreeNodePopulate 이벤트가 발생 합니다. 그런 다음 데이터에 사용 되는 XML 데이터 아일랜드를 사용 하 여 서버 응답 자식 노드를 바인딩합니다.

ASP.NET이이 기능을 구현 하는 클라이언트 코드를 동적으로 만듭니다. 합니다 &lt;스크립트&gt; AXD 파일을 가리키는 스크립트를 포함 하는 태그 생성 됩니다. 예를 들어, 아래 목록에는 XMLHttp 요청을 생성 하는 스크립트 코드에 대 한 스크립트 링크를 보여 줍니다.

[!code-html[Main](data-bound-controls/samples/sample7.html)]

브라우저에서 위의 AXD 파일을 이동 하 고 열면 XMLHttp 요청을 구현 하는 코드가 표시 됩니다. 이 메서드는 스크립트 파일을 수정에서 고객을 방지 합니다.

## <a name="controlling-the-operation-of-the-treeview-control"></a>TreeView 컨트롤의 작업을 제어합니다.

TreeView 컨트롤에 컨트롤의 작동에 영향을 주는 몇 가지 속성이 있습니다. 가장 확실 한 속성은는 **ShowCheckBoxes**를 **ShowExpandCollapse**, 및 **ShowLines**합니다.

합니다 **ShowCheckBoxes** 속성 노드 렌더링 될 때 확인 상자를 표시 하는지 여부에 영향을 줍니다. 이 속성에 대 한 유효한 값은 **None**를 **루트**를 **부모**를 **리프**, 및 **모든**합니다. 이러한 영향을 줄 TreeView 컨트롤 다음과 같습니다.

| **속성 값** | **효과** |
| --- | --- |
| 없음 | 모든 노드에서 확인란 표시 되지 않습니다. 이것이 기본 설정입니다. |
| 루트 | 확인란은 루트 노드에 표시 됩니다. |
| 부모 | 확인란은 해당 노드의 자식 노드는 표시 됩니다. 해당 자식 노드의 부모 노드 또는 리프 노드로 수 있습니다. |
| 리프 | 확인란은 자식 노드가 있는 해당 노드에 대해서만 표시 됩니다. |
| 모두 | 확인란은 모든 노드에 표시 됩니다. |

확인란을 사용 하는 경우는 **CheckedNodes** 속성은 포스트백 시 검사 되는 트리 뷰에서 노드 컬렉션을 반환 합니다.

합니다 **ShowExpandCollapse** 속성 루트 노드와 부모 노드 옆에 있는 확장/축소 이미지의 모양을 제어 합니다. 이 속성 설정 된 경우 **false**, TreeView 노드 하이퍼링크로 렌더링 되 고 링크를 클릭 하 여 확장/축소 됩니다.

합니다 **ShowLines** 속성 부모 노드를 자식 노드에 연결 줄은 표시 여부를 제어 합니다. 때 **false** (기본값), 없는 줄이 표시 됩니다. 때 **true**, TreeView 컨트롤에서 지정 된 폴더에서 줄 이미지를 사용 합니다 **LineImagesFolder** 속성입니다.

TreeView 선 표시를 사용자 지정, Visual Studio.NET 2005 줄 디자이너 도구를 포함 합니다. 아래는 TreeView 컨트롤에서 스마트 태그 단추를 사용 하 여이 도구를 액세스할 수 있습니다.


![](data-bound-controls/_static/image1.jpg)

**그림 1**


선택 하는 경우는 **선 이미지 사용자 지정** 메뉴 옵션을 TreeView 선의 모양을 구성할 수 있으므로 줄 디자이너 도구 시작 됩니다.

## <a name="treeview-events"></a>TreeView 이벤트

TreeView 컨트롤에 다음과 같은 고유한 이벤트가 있습니다.

- 에 따라 SelectedNodeChanged 노드가 선택 될 때 발생 합니다 **SelectAction** 속성입니다.
- TreeNodeCheckChanged 노드 checkboxs 상태가 변경 될 때 발생 합니다.
- 에 따라 TreeNodeExpanded 노드를 확장 하는 경우 발생 합니다 **SelectAction** 속성입니다.
- TreeNodeCollapsed 노드를 축소 하는 경우 발생 합니다.
- 데이터를 노드인 경우 TreeNodeDataBound 바인딩됩니다.
- TreeNodePopulate 노드를 채울 때 발생 합니다.

합니다 **SelectAction** 속성을 사용 하면 노드가 선택 될 때 이벤트 발생을 구성할 수 있습니다. SelectAction 속성에는 다음 작업을 제공합니다.

- TreeNodeSelectAction.Expand 시킵니다 TreeNodeExpanded 노드를 선택 하는 경우입니다.
- TreeNodeSelectAction.None는 노드가 선택 되었을 때 이벤트가 발생 시킵니다.
- TreeNodeSelectAction.Select은 노드가 선택 되었을 때 SelectedNodeChanged 이벤트를 발생 시킵니다.
- TreeNodeSelectAction.SelectExpand는 SelectedNodeChanged 이벤트와는 노드를 선택한 경우 TreeNodeExpanded 이벤트를 발생 시킵니다.

## <a name="controlling-appearance-with-styles"></a>스타일을 사용 하 여 모양 제어

TreeView 컨트롤 스타일을 사용 하 여 컨트롤의 모양을 제어 하는 것에 대 한 여러 속성을 제공 합니다. 다음 속성을 사용할 수 있습니다.

| **속성 이름** | **컨트롤** |
| --- | --- |
| HoverNodeStyle | 마우스 위로 가져갈 때 노드의 스타일을 제어 합니다. |
| LeafNodeStyle | 리프 노드의 스타일을 제어합니다. |
| NodeStyle | 모든 노드에 대 한 스타일을 제어합니다. 특정 노드 스타일 (예: LeafNodeStyle)이이 스타일을 재정의합니다. |
| ParentNodeStyle | 모든 부모 노드에 대 한 스타일을 제어합니다. |
| RootNodeStyle | 루트 노드에 대 한 스타일을 제어합니다. |
| SelectedNodeStyle | 선택한 노드의 스타일을 제어합니다. |

이러한 각 속성에는 읽기 전용입니다. 각 반환 되며이 단,을 **TreeNodeStyle** 개체 및 해당 개체의 속성을 수정할 수 있습니다 사용 하는 *속성 하위* 형식입니다. 예를 들어, 설정 하는 **ForeColor** 의 속성을 **SelectedNodeStyle**, 다음 구문을 사용:

[!code-aspx[Main](data-bound-controls/samples/sample8.aspx)]

위의 태그 닫히지 않습니다 확인 합니다. 여기에 표시 된 선언적 구문을 사용 하는 경우 Treeview 노드는 HTML 코드에서는 때문입니다.

스타일 속성을 사용 하 여 코드에서 지정할 수도 있습니다는 *property.subproperty* 형식입니다. 예를 들어, 설정 하는 **ForeColor** 의 속성을 **RootNodeStyle** 코드에서 다음 구문을 사용:

[!code-csharp[Main](data-bound-controls/samples/sample9.cs)]

> [!NOTE]
> 다른 스타일 속성의 포괄적인 목록은, TreeNodeStyle 개체의 MSDN 설명서를 참조 합니다.


## <a name="the-sitemappath-control"></a>SiteMapPath 컨트롤

SiteMapPath 컨트롤 ASP.NET 개발자를 위한 이동 경로 탐색 컨트롤을 제공합니다. 다른 탐색 컨트롤 처럼 쉽게 수 원본 XmlDataSource 또는 SiteMapDataSource와 같은 계층적 데이터에 바인딩된 데이터입니다.

SiteMapPath 컨트롤 SiteMapNodeItem 개체 이루어져 있습니다. 가지 다음 세 가지 유형의 노드 루트 노드, 부모 노드 및 현재 노드를 선택 합니다. 루트 노드는 계층 구조 맨 위에 있는 노드입니다. 현재 노드가 현재 페이지를 나타냅니다. 다른 모든 노드는 부모 노드입니다.

## <a name="controlling-the-operation-of-the-sitemappath-control"></a>SiteMapPath 컨트롤의 작업을 제어합니다.

SiteMapPath 컨트롤의 작업을 제어 하는 속성은 다음과 같습니다.

| **Property** | **속성 설명** |
| --- | --- |
| ParentLevelsDisplayed | 얼마나 많은 부모 노드 표시 여부를 제어 합니다. 기본값은-1로 표시 되는 부모 노드 수에 제한 하지 않습니다. |
| PathDirection | SiteMapPath 방향을 제어합니다. 유효한 값은 RootToCurrent (기본값) 및 CurrentToRoot입니다. |
| PathSeparator | SiteMapPath 컨트롤의 노드를 구분 하는 문자를 제어 하는 문자열입니다. 기본값은:입니다. |
| RenderCurrentNodeAsLink | 현재 노드가 링크로 렌더링 되는 여부를 제어 하는 부울 값입니다. 기본값은 False입니다. |
| SkipLinkText | 화면 판독기가 페이지를 볼 때 내게 필요한 옵션을 사용 하 여는 데 유용 합니다. 이 속성에는 SiteMapPath 컨트롤을 건너뛰기 위해 화면 판독기 수 있습니다. 이 기능을 사용 하지 않으려면 속성 String.Empty로 설정 합니다. |

## <a name="templated-sitemappath-controls"></a>템플릿 기반 SiteMapPath 컨트롤

SiteMapControl 템플릿 기반 컨트롤은 이며 이와 같이 컨트롤을 표시에서 사용 하기 위해 다양 한 템플릿을 정의할 수 있습니다. SiteMapPath 컨트롤에서 서식 파일을 편집 하려면 컨트롤에서 스마트 태그 단추를 클릭 하 고 메뉴에서 템플릿 편집을 선택 합니다. 이 사용 가능한 다양 한 템플릿을 선택할 수 있는 아래와 같이 SiteMapTasks 메뉴가 표시 됩니다.


![](data-bound-controls/_static/image2.jpg)

**그림 2**


합니다 **NodeTemplate** 템플릿은 SiteMapPath에서 모든 노드를 가리킵니다. 노드가 루트 노드 또는 현재 노드 **RootNodeTemplate** 또는 **CurrentNodeTemplate** 은 구성 NodeTemplate 재정의 됩니다.

## <a name="sitemappath-events"></a>SiteMapPath 이벤트

SiteMapPath 컨트롤에 컨트롤 클래스에서 파생 되지 않은 두 개의 이벤트 합니다 **ItemCreated** 이벤트와 **ItemDataBound** 이벤트입니다. SiteMapPath 항목이 만들어질 때 ItemCreated 이벤트가 발생 합니다. ItemDataBound는 SiteMapPath 노드의 데이터 바인딩처럼 DataBind 메서드가 호출 될 때 발생 합니다. A **SiteMapNodeItemEventArgs** 개체는 항목 속성을 통해 특정 SiteMapNodeItem에 대 한 액세스를 제공 합니다.

## <a name="controlling-appearance-with-styles"></a>스타일을 사용 하 여 모양 제어

다음 스타일은 SiteMapPath 컨트롤의 서식 지정에 사용할 수 있습니다.

| **속성 이름** | **컨트롤** |
| --- | --- |
| CurrentNodeStyle | 현재 노드에 대 한 텍스트의 스타일을 제어합니다. |
| RootNodeStyle | 루트 노드에 대 한 텍스트의 스타일을 제어합니다. |
| NodeStyle | CurrentNodeStyle 또는 RootNodeStyle 적용 하지 않았다는 가정 하는 모든 노드에 대 한 텍스트의 스타일을 제어 합니다. |

NodeStyle 속성을 CurrentNodeStyle 또는 RootNodeStyle에 의해 재정의 됩니다. 이러한 각 속성은 읽기 전용 및 반환 된 **스타일** 개체입니다. 이러한 속성 중 하나를 사용 하 여 노드의 모양에 영향을 줄에 반환 되는 스타일 개체의 속성을 설정 해야 합니다. 예를 들어 아래 코드는 현재 노드의 전경색 속성을 변경합니다.

[!code-aspx[Main](data-bound-controls/samples/sample10.aspx)]

속성은 다음과 같이 프로그래밍 방식으로 적용 될 수도 있습니다.

[!code-csharp[Main](data-bound-controls/samples/sample11.cs)]

> [!NOTE]
> 템플릿을 적용 되는 경우 스타일 적용 되지 않습니다.


## <a name="lab-1-configuring-an-aspnet-menu-control"></a>랩 1: 구성 된 ASP.NET Menu 컨트롤

1. 새 웹 사이트를 만듭니다.
2. 파일, 새로 만들기, 파일을 선택 하 여 사이트 맵 파일 템플릿 목록에서 사이트 맵 파일을 추가 합니다.
3. 사이트 맵 (기본적으로 Web.sitemap)을 열고 아래 목록 같은 표시 되도록 수정 합니다. 사이트 맵 파일에 연결 되어 페이지에 실제로 존재 하지 않지만이 연습에서는 문제가 되지 않습니다.

    [!code-xml[Main](data-bound-controls/samples/sample12.xml)]
4. 디자인 뷰에서 기본 Web form을 엽니다.
5. 도구 상자의 탐색 섹션에서 새 메뉴 컨트롤을 페이지에 추가 합니다.
6. 도구 상자의 데이터 섹션에서 새 SiteMapDataSource를 추가 합니다. SiteMapDataSource는 Web.sitemap 파일을 사용 하 여 사이트에서 자동으로 됩니다. (Web.sitemap 파일 *해야* 사이트의 루트 폴더에 있어야 합니다.)
7. 메뉴 컨트롤을 클릭 하 고 스마트 태그 메뉴 작업 대화 상자에 표시할 단추를 클릭 합니다.
8. 데이터 소스 선택 드롭다운 목록에서 SiteMapDataSource1를 선택 합니다.
9. AutoFormat 링크를 클릭 한 메뉴에 대 한 형식을 선택 합니다.
10. 속성 창에서 설정 된 **StaticDisplayLevels** 속성을 2로 합니다. 이제 메뉴 컨트롤 디자이너에서 홈, 제품 및 서비스 노드를 표시 됩니다.
11. 메뉴를 사용 하 여 브라우저에서 페이지를 찾습니다. (적 사이트 맵에 추가 페이지를 실제로 존재 하지 않거나, 때문에 오류가 표시 됩니다는에 검색을 시도 하면 됩니다.)

StaticDisplayLevels 및 MaximumDynamicDisplayLevels 속성을 변경 하 여 실험 하 고 메뉴 렌더링 되는 방식에 미치는 영향을 확인 합니다.

## <a name="lab-2-dynamically-binding-a-treeview-control"></a>랩 2: TreeView 컨트롤을 동적으로 바인딩

이 연습에는 로컬로 실행 중인 SQL Server 있으며 Northwind 데이터베이스를 SQL Server 인스턴스에 있는지 가정 합니다. 이러한 조건이 충족 되지 않으면, 예제의 연결 문자열을 변경 하십시오. 트러스트 된 연결 하는 대신 SQL Server 인증을 지정 해야도 참고 합니다.

1. 새 웹 사이트를 만듭니다.
2. Default.aspx에 대 한 코드 보기로 전환한 모든 코드를 아래 코드로 바꿉니다. 

    [!code-aspx[Main](data-bound-controls/samples/sample13.aspx)]
3. Treeview.aspx로 페이지를 저장 합니다.
4. 페이지를 찾습니다.
5. 페이지를 처음 표시할 때 브라우저에서 페이지의 소스를 봅니다. 표시 되는 노드만 클라이언트로 전송 된 참고 합니다.
6. 노드 옆에 있는 더하기 기호를 클릭 합니다.
7. 페이지의 다시 소스를 봅니다. 이제 새로 표시 된 노드에 있는지 확인 합니다.

## <a name="lab-3-details-view-and-editing-data-using-a-gridview-and-detailsview"></a>실습 3: 정보 뷰와 GridView 및 DetailsView를 사용 하 여 데이터를 편집 합니다.

1. 새 웹 사이트를 만듭니다.
2. 웹 사이트를 새 web.config를 추가 합니다.
3. 아래와 같이 web.config 파일에 연결 문자열을 추가 합니다. 

    [!code-xml[Main](data-bound-controls/samples/sample14.xml)]

    > [!NOTE]
    > 사용자 환경에 따라 연결 문자열을 변경 해야 합니다.
4. web.config 파일을 저장한 다음 닫습니다.
5. Default.aspx를 열고 새 SqlDataSource 컨트롤을 추가 합니다.
6. SqlDataSource 컨트롤의 ID를 변경 **제품**합니다.
7. 에 **SqlDataSource 작업** 메뉴에서 클릭 **데이터 소스 구성**합니다.
8. 선택 **Northwind** 연결 드롭다운에서 다음을 클릭 합니다.
9. 선택 **제품** 에서 **이름** 드롭다운 하 고 확인을 **ProductID**, **ProductName**, **UnitPrice**, 및 **UnitsInStock** 아래와 같이 확인란 합니다. 

![](data-bound-controls/_static/image3.jpg)

    **Figure 3**
10. **다음**을 클릭합니다.
11. **마침**을 클릭합니다.
12. 원본 뷰로 전환 하 고 생성 된 코드를 검사 합니다. 알림 합니다 **SelectCommand**를 **DeleteCommand**를 **InsertCommand**, 및 **UpdateCommand** SqlDataSource에 추가 된 컨트롤입니다. 또한 추가 된 매개 변수를 확인 합니다.
13. 디자인 뷰로 전환한 다음 새 GridView 컨트롤을 페이지에 추가 합니다.
14. 선택 **제품** 에서 합니다 **데이터 소스 선택** 드롭다운 합니다.
15. 확인 **페이징 사용** 하 고 **선택 가능** 아래와 같이 합니다. 

![](data-bound-controls/_static/image4.jpg)

    **Figure 4**
16. 클릭는 **열 편집** 에 연결 하 고 있는지 **필드 자동 생성** 확인란이 선택 되어 있습니다.
17. **확인**을 클릭합니다.
18. GridView 컨트롤을 선택 하 여 클릭 단추 옆에 **DataKeyNames** 속성 창에서 속성입니다.
19. 선택 **ProductID** 에서 **사용 가능한 데이터 필드** 나열 하 고 클릭 합니다 **&gt;** 단추를 추가 합니다.
20. 확인을 클릭합니다.
21. 페이지에 새 SqlDataSource 컨트롤을 추가 합니다.
22. SqlDataSource 컨트롤의 ID를 변경 **세부 정보**합니다.
23. SqlDataSource 작업 메뉴에서 선택 **데이터 소스 구성**합니다.
24. 선택할 **Northwind** 클릭 하 고 드롭다운에서에서 **다음**합니다.
25. 선택 <strong>제품</strong> 에서 <strong>이름</strong> 드롭다운 확인 하 고는 <strong> \</s o n > *에서 확인란을 선택 합니다 <strong>열</strong> listbox.
26. 클릭 합니다 **여기서** 단추입니다.
27. 선택 **ProductID** 에서 합니다 **열** 드롭다운 합니다.
28. 선택 **=** 연산자 드롭다운 목록에서.
29. 선택 **제어** 에서 합니다 **원본** 드롭다운 합니다.
30. 선택 **GridView1** 에서 합니다 **컨트롤 ID** 드롭다운 합니다.
31. 클릭 합니다 **추가** 을 WHERE 절을 추가 합니다.
32. **확인**을 클릭합니다.
33. 클릭는 **고급** 단추를 확인 합니다 **생성 INSERT, UPDATE 및 DELETE 문을** 확인란을 선택 합니다.
34. **확인**을 클릭합니다.
35. 클릭 **다음** 누릅니다 **마침**합니다.
36. DetailsView 컨트롤을 페이지에 추가 합니다.
37. 에 **데이터 원본 선택** 드롭다운에서 선택 **세부 정보**합니다.
38. 확인 합니다 **편집 사용** 아래와 같이 확인란을 선택 합니다. 

![](data-bound-controls/_static/image1.gif)

    **Figure 5**
39. 페이지를 저장 하 고 Default.aspx를 찾습니다.
40. 클릭 합니다 **선택** DetailsView 업데이트를 자동으로 확인 하려면 다른 레코드 옆에 있는 링크입니다.
41. 클릭 합니다 **편집** DetailsView 컨트롤에서 링크 합니다.
42. 레코드를 변경 하 고 클릭 **업데이트**합니다.
