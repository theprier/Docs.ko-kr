---
uid: web-forms/overview/moving-to-aspnet-20/data-bound-controls
title: 데이터 바인딩된 컨트롤 | Microsoft Docs
author: microsoft
description: 대부분의 ASP.NET 응용 프로그램 사용 어느 정도의 백 엔드 데이터 원본에서 데이터를 표시 합니다. 데이터 바인딩된 컨트롤의 상호 작용 w 중요 일부 였을...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: 0e23ff32-646d-43f3-8bec-6b2313d3abd6
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-bound-controls
msc.type: authoredcontent
ms.openlocfilehash: 5c3f6aad4b87450149189352e86106f46c765fb8
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="data-bound-controls"></a>데이터 바인딩 컨트롤
====================
by [Microsoft](https://github.com/microsoft)

> 대부분의 ASP.NET 응용 프로그램 사용 어느 정도의 백 엔드 데이터 원본에서 데이터를 표시 합니다. 데이터 바인딩된 컨트롤에는 동적 웹 응용 프로그램의 데이터와 상호 작용 중요 일부 였 합니다. ASP.NET 2.0 데이터 바인딩된 컨트롤에 새 BaseDataBoundControl 클래스 및 선언적 구문을 비롯 한 몇 가지 크게 향상 된 기능을 소개 합니다.


대부분의 ASP.NET 응용 프로그램 사용 어느 정도의 백 엔드 데이터 원본에서 데이터를 표시 합니다. 데이터 바인딩된 컨트롤에는 동적 웹 응용 프로그램의 데이터와 상호 작용 중요 일부 였 합니다. ASP.NET 2.0 데이터 바인딩된 컨트롤에 새 BaseDataBoundControl 클래스 및 선언적 구문을 비롯 한 몇 가지 크게 향상 된 기능을 소개 합니다.

BaseDataBoundControl DataBoundControl 클래스와 hierarchicaldataboundcontrol은 클래스에 대 한 기본 클래스 역할을 합니다. 이 단원에서는 DataBoundControl에서 파생 되는 다음 클래스에 설명 합니다.

- AdRotator
- 목록 컨트롤
- GridView
- FormView
- DetailsView

또한 다음과 같은 작용이 hierarchicaldataboundcontrol은 클래스에서 파생 되는 다음 클래스:

- TreeView
- 메뉴
- SiteMapPath

## <a name="databoundcontrol-class"></a>DataBoundControl 클래스

DataBoundControl 클래스는 테이블 형식와 상호 작용 하는 데 사용 되는 추상 클래스 (vb에서 MustInherit 표시) 또는 목록 스타일 데이터입니다. 다음 컨트롤은 DataBoundControl에서 파생 되는 컨트롤의 일부입니다.

## <a name="adrotator"></a>AdRotator

AdRotator 컨트롤을 사용 하면 그래픽 배너 특정 URL에 연결 된 웹 페이지에 표시할 수 있습니다. 표시 되는 그래픽 컨트롤에 대 한 속성을 사용 하 여 회전 합니다. 사용 하 여 페이지에 표시 하는 특정 ad의 빈도 구성할 수 있습니다는 **광고** 속성 및 광고 필터링 할 수 키워드 필터링을 사용 하 여 합니다.

AdRotator 컨트롤 데이터에 대 한 데이터베이스에서 XML 파일 또는 테이블 중 하나를 사용합니다. AdRotator 컨트롤을 구성 하려면 XML 파일에는 다음 특성이 사용 됩니다.

### <a name="imageurl"></a>ImageUrl
광고에 표시할 이미지의 URL입니다.

### <a name="navigateurl"></a>NavigateUrl
광고를 클릭할 때 사용자 위해 수행 해야 하는 URL입니다. 이 URL 인코딩 이어야 합니다.

### <a name="alternatetext"></a>AlternateText
대체 텍스트 도구 설명에 표시 되 고 화면 판독기가 읽은입니다. ImageUrl으로 지정 된 이미지를 사용할 수 없는 경우에 표시 됩니다.

### <a name="keyword"></a>키워드
키워드 필터링을 사용할 때 사용할 수 있는 키워드를 정의 합니다. 를 지정 하는 경우만 해당 광고 키워드 필터와 일치 하는 키워드와 함께 표시 됩니다.

### <a name="impressions"></a>광고
특정 ad 나타날 가능성이 빈도 결정 하는 가중치 수입니다. 동일한 파일의 다른 광고의 효과 주기 관련이 있습니다. XML 파일에 모든 광고에 대 한 집단 상대 값의 최대값은 2,048,000,000 1입니다.

### <a name="height"></a>높이
픽셀 단위로 광고의 높이입니다.

### <a name="width"></a>너비
픽셀 단위로 광고의 너비입니다.


> [!NOTE]
> 높이 너비 특성 AdRotator 컨트롤 자체에 대 한 너비와 높이 재정의합니다.


일반적인 XML 파일을 다음과 같을 수 있습니다.

[!code-xml[Main](data-bound-controls/samples/sample1.xml)]

위의 예제에서는 Contoso에 대 한 ad는 ASP.NET 웹 사이트에 대 한 ad로 광고 특성에 대 한 값으로 인해 표시 가능성이 두 번입니다.

위의 XML 파일에서 광고를 표시 하려면 페이지를 AdRotator 컨트롤을 추가 하 고 설정 된 **AdvertisementFile** 아래 표시 된 대로 XML 파일을 가리키도록 속성:

[!code-aspx[Main](data-bound-controls/samples/sample2.aspx)]

AdRotator 컨트롤에 대 한 데이터 원본으로 데이터베이스 테이블을 사용 하려는 경우 먼저 다음 스키마를 사용 하 여 데이터베이스를 설정 해야 합니다.

| **열 이름** | **데이터 형식** | **설명** |
| --- | --- | --- |
| ID | int | 기본 키입니다. 이 열 이름을 가질 수 있습니다. |
| ImageUrl | nvarchar(*length*) | 광고에 표시할 이미지의 상대 또는 절대 URL입니다. |
| NavigateUrl | nvarchar(*length*) | Ad에 대 한 대상 URL입니다. 값을 제공 하지 않으면 ad 하이퍼링크 표시 되지 않습니다. |
| AlternateText | nvarchar(*length*) | 이미지를 찾을 수 없는 경우 표시 되는 텍스트입니다. 일부 브라우저에서는 텍스트 도구 설명으로 표시 됩니다. 그래픽을 볼 수 없는 사용자 설명을 읽는 소리내어를 들 수 있도록 내게 필요한 옵션에 대 한 대체 텍스트도 사용 됩니다. |
| 키워드 | nvarchar(*length*) | 페이지 필터링 할 수 ad에 대 한 범주입니다. |
| 광고 | int(4) | 숫자의 광고가 표시 되는 빈도 나타내는입니다. 더 큰 숫자를 더 자주 광고가 표시 됩니다. XML 파일의 모든 상대 값의 합계 2048000000-1을 초과할 수 없습니다. |
| 너비 | int(4) | 픽셀 단위로 이미지의 너비입니다. |
| 높이 | int(4) | 픽셀 단위로 이미지의 높이입니다. |

다른 스키마가 있는 데이터베이스를 이미 만든 경우에 사용할 수 있습니다는 **AlternateTextField**, **ImageUrlField**, 및 **NavigateUrlField** 매핑할 속성이 고 기존 데이터베이스에 AdRotator 특성입니다. AdRotator 컨트롤을 데이터베이스에서 데이터를 표시 하려면 추가 데이터 소스 제어 페이지, 프로그램 데이터베이스를 가리키도록 데이터 소스 제어에 대 한 연결 문자열을 구성 및 설정 AdRotator 컨트롤 **DataSourceID** 속성 데이터 소스 컨트롤의 ID입니다. AdRotator 광고를 프로그래밍 방식으로 구성할 필요가 있는 경우 AdCreated 이벤트를 사용 합니다. AdCreated 이벤트는 두 개의 매개 변수입니다. 하나는 개체 및 기타 AdCreatedEventArgs의 인스턴스. AdCreatedEventArgs 생성 중인 ad에 대 한 참조입니다.

다음 코드 조각 ImageUrl, NavigateUrl 및 AlternateText 광고에 대 한 프로그래밍 방식으로 설정 합니다.

[!code-csharp[Main](data-bound-controls/samples/sample3.cs)]

## <a name="list-controls"></a>목록 컨트롤

목록 컨트롤 ListBox, DropDownList, CheckBoxList, RadioButtonList, 및 BulletedList 포함 됩니다. 이러한 컨트롤의 각 데이터 원본에 데이터 바인딩될 수 있습니다. 데이터 원본에 텍스트 표시로 한 필드를 사용 하 고 항목의 값으로 두 번째 필드를 선택적으로 사용할 수 있습니다. 항목 디자인 타임에 정적으로 추가할 수도 있습니다 하 고 데이터 원본에서 추가 항목을 동적 및 정적 항목을 함께 사용할 수 있습니다.

목록 컨트롤을 바인딩할 데이터 페이지를 데이터 소스 제어를 추가 하세요. 데이터 소스 제어에 대 한 SELECT 명령을 지정 하 고 데이터 소스 컨트롤의 ID로는 DataSourceID 속성 목록 컨트롤을 설정 합니다. 사용 하 여는 **DataTextField** 및 **DataValueField** 표시 텍스트 및 컨트롤에 대 한 값을 정의 하는 속성입니다. 또한 사용할 수는 **DataTextFormatString** 모양을 제어 하는 텍스트의 다음과 같은 속성:

| **식** | **설명** |
| --- | --- |
| Price: {0:C} | 숫자/소수 데이터. 리터럴을 표시 "Price:" 다음에 통화 형식으로 숫자입니다. 통화 형식에서 culture 특성에 지정 된 culture 설정에 따라 달라 집니다는 **페이지** 지시문 또는 Web.config 파일에 있습니다. |
| {0:D4} | 정수 데이터입니다. 십진수와 함께 사용할 수 없습니다. 정수 4 개의 문자 너비는 0을 채우는 필드에 표시 됩니다. |
| {0:N2}% | 숫자 데이터. 숫자 2 표시 정밀도 다음에 리터럴 "%"입니다. |
| {0:000.0} | 숫자/소수 데이터. 숫자가 소수 첫째 자리로 반올림 됩니다. 세 자리보다 작은 숫자는 0으로 채워집니다. |
| {0:D} | 날짜/시간 데이터. 표시 자세한 날짜 형식 ("1996 년, 년 8 월 6 일, 목요일")입니다. 날짜 형식은 page 지시문 또는 Web.config 파일의 문화권 설정에 따라 달라집니다. |
| {0:d} | 날짜/시간 데이터. 표시 간단한 날짜 형식 ("12/31/99"). |
| {0:yy-MM-dd} | 날짜/시간 데이터. (96-08-06) 숫자 연도-월-일 형식의 날짜를 표시합니다. |

## <a name="gridview"></a>GridView

GridView 컨트롤의 테이블 형식 데이터 표시 및 선언적 접근 방식을 사용 하 여 편집 허용 하며 DataGrid 컨트롤에 대 한 후속. 다음 기능은 GridView 컨트롤에서 사용할 수 있습니다.

- SqlDataSource 등의 소스 제어에서 데이터 바인딩.
- 기본 제공 정렬 기능입니다.
- 기본 제공 업데이트 및 삭제 기능입니다.
- 기본 제공 페이징 기능입니다.
- 기본 제공 행 선택 기능입니다.
- 동적으로 속성을 설정 하는 GridView 개체 모델에 대 한 프로그래밍 방식 액세스 이벤트를 처리 등에입니다.
- 여러 키 필드입니다.
- 하이퍼링크 열에 대 한 여러 데이터 필드입니다.
- 테마 및 스타일을 통해 모양을 사용자 지정할 수 있습니다.

**열 필드**

GridView 컨트롤의 각 열 DataControlField 개체로 나타냅니다. 기본적으로 AutoGenerateColumns 속성 설정 **true**, 데이터 원본에 각 필드에 대 한 AutoGeneratedField 개체를 만듭니다입니다. 그런 다음 각 필드는 각 필드는 데이터 소스에 표시 된 순서 대로 GridView 컨트롤의 열으로 렌더링 됩니다. 필드에 표시 되는 열을 직접 제어할 수 있습니다는 **GridView** 설정 하 여 컨트롤의 **AutoGenerateColumns** 속성을 **false** 다음 직접를 정의 열 필드 컬렉션입니다. 열 필드 형식에 따라 컨트롤의 열의 동작을 결정 합니다.

다음 표에서 사용할 수 있는 여러 열 필드 형식을 나열 합니다.

| **열 필드 형식** | **설명** |
| --- | --- |
| BoundField | 데이터 원본에서 필드의 값을 표시 합니다. GridView 컨트롤의 기본 열 형식입니다. |
| ButtonField | GridView 컨트롤의 각 항목에 대 한 명령 단추를 표시합니다. 이 추가 / 제거 단추 등의 사용자 지정 단추 컨트롤의 열을 만들 수 있습니다. |
| CheckBoxField | GridView 컨트롤의 각 항목에 대 한 확인란을 표시합니다. 열 필드 형식은이 부울 값을 사용 하는 필드를 표시 하려면 일반적으로 사용 됩니다. |
| CommandField | 미리 정의 된 선택, 편집 또는 삭제 작업을 수행 하는 명령 단추를 표시 합니다. |
| HyperLinkField | 데이터 원본의 필드의 값을 하이퍼링크로 표시 됩니다. 이 열 필드 형식을 사용 하면 두 번째 필드 하이퍼링크의 URL에 바인딩할 수 있습니다. |
| ImageField | GridView 컨트롤의 각 항목에 대 한 이미지를 표시합니다. |
| TemplateField | 지정된 된 템플릿에 따라 GridView 컨트롤의 각 항목에 대 한 사용자 정의 콘텐츠 표시 됩니다. 이 열 필드 형식에는 사용자 지정 열 필드를 만들 수 있습니다. |

열 필드 컬렉션을 선언적으로 정의 하려면 먼저 추가 중괄호와 닫는 **&lt;열&gt;** 및 GridView 컨트롤의 닫는 태그 사이입니다. 다음에 여는 태그와 닫는 간의 포함 시킬 열 필드를 나열 **&lt;열&gt;** 태그입니다. 지정 된 열은 나열 된 순서로 Columns 컬렉션에 추가 됩니다. **열** 컬렉션을 저장 하는 모든 열 컨트롤의 필드 및 GridView 컨트롤의 열 필드를 프로그래밍 방식으로 관리할 수 있습니다.

명시적으로 선언 된 열 필드를 자동으로 생성 된 열 필드와 함께에서 표시할 수 있습니다. 모두 사용 하는 명시적으로 선언 된 열 필드 뒤에 자동으로 생성 된 열 필드를 먼저 렌더링 됩니다.

## <a name="binding-to-data"></a>데이터 바인딩

GridView 컨트롤을 데이터 소스 제어에 바인딩될 수 (예: **SqlDataSource**, **ObjectDataSource**등)는 System.Collections.IEnumerable을 구현 하는 모든 데이터 소스 외에, 인터페이스 (예: System.Data.DataView, System.Collections.ArrayList, 또는 System.Collections.Hashtable). 다음 방법 중 하나를 사용 하 여 적절 한 데이터 소스 형식에 GridView 컨트롤 바인딩:

- 데이터 소스 제어에 바인딩할 GridView 컨트롤의 데이터 소스 컨트롤의 ID 값으로 설정 합니다. GridView 컨트롤의 지정 된 데이터 소스 제어에 자동으로 바인딩하고 활용할 수 데이터 소스 컨트롤의 기능을 정렬, 업데이트, 삭제 및 페이징 기능을 수행 합니다. 이것은 데이터에 바인딩하는 기본 방법입니다.
- System.Collections.IEnumerable 인터페이스를 구현 하는 데이터 원본에 바인딩할 프로그래밍 방식으로 데이터 원본에 GridView 컨트롤의 DataSource 속성을 설정 하 고 DataBind 메서드를 호출 합니다. 이 메서드를 사용 하면 기본 제공 정렬, 업데이트, 삭제 및 페이징 기능 GridView 컨트롤 제공 하지 않습니다. 이 기능을 직접 제공 해야 합니다.

## <a name="data-operations"></a>데이터 작업

GridView 컨트롤 사용자가 정렬, 업데이트, 삭제, 선택, 및 컨트롤의 항목을 페이징할 수 있는 다양 한 기본 제공 기능을 제공 합니다. GridView 컨트롤 데이터 소스 제어에 바인딩되어 GridView 컨트롤 데이터 소스 컨트롤의 기능을 사용할 수 있으며 자동 정렬, 업데이트 및 삭제 기능을 제공 합니다.

> [!NOTE]
> GridView 컨트롤 정렬, 업데이트 및 다른 유형의 데이터 원본 삭제에 대 한 지원을 제공할 수 있습니다. 그러나 이러한 작업에 대 한 구현으로 적절 한 이벤트 처리기를 제공 해야 합니다.


정렬 열 머리글을 클릭 하 여 특정 열에 대 한 GridView 컨트롤에서 항목을 정렬 하려면 사용자 수 있습니다. 정렬 기능을 사용 하려면 AllowSorting 속성을 설정 **true**합니다.

자동 업데이트, 삭제 및 선택 기능을 사용할 때의 단추를 사용할 수는 **ButtonField** 또는 **TemplateField** "편집", "Delete" 및 "Select" 명령 이름으로 열 필드 각각를 클릭 합니다. GridView 컨트롤에서 자동으로 추가할 수는 **CommandField** 열 필드는 편집, 삭제 또는 AutoGenerateEditButton, AutoGenerateDeleteButton, 또는 AutoGenerateSelectButton 속성이 로설정되어있으면선택단추**true**각각.

> [!NOTE]
> 직접 GridView 컨트롤에서 데이터 원본에 레코드 삽입 지원 되지 않습니다. 그러나 DetailsView와 함께에서 GridView 컨트롤 또는 FormView 컨트롤을 사용 하 여 레코드를 삽입 하는 것이 같습니다.


동시에 데이터 원본의 모든 레코드를 표시, 하는 대신 GridView 컨트롤 자동으로 분리할 수 레코드 페이지에 있습니다. 페이징을 사용 하도록 설정 하려면 AllowPaging 속성을 설정 **true**합니다.

## <a name="customizing-the-user-interface"></a>사용자 인터페이스 사용자 지정

컨트롤의 다른 부분에 대 한 스타일 속성을 설정 하 여 GridView 컨트롤의 모양을 사용자 지정할 수 있습니다. 다음 표에서 다른 스타일 속성을 나열합니다.

| **스타일 속성** | **설명** |
| --- | --- |
| AlternatingRowStyle | GridView 컨트롤에 교대로 반복 되는 데이터 행에 대 한 스타일 설정입니다. RowStyle 설정 간의 교대로 반복 되는 데이터 행을 표시할 때이 속성을 설정 및 **AlternatingRowStyle** 설정 합니다. |
| EditRowStyle | GridView 컨트롤에 편집 되는 행 스타일 설정입니다. |
| EmptyDataRowStyle | 데이터 원본에는 레코드가 없으면 GridView 컨트롤에 표시 되는 빈 데이터 행에 대 한 스타일 설정입니다. |
| FooterStyle | GridView 컨트롤의 바닥글 행에 대 한 스타일 설정입니다. |
| HeaderStyle | GridView 컨트롤의 머리글 행에 대 한 스타일 설정입니다. |
| PagerStyle | GridView 컨트롤의 호출기 행에 대 한 스타일 설정입니다. |
| RowStyle | GridView 컨트롤에 데이터 행에 대 한 스타일 설정입니다. 경우는 **AlternatingRowStyle** 도 속성이 설정 되어, 교대로 데이터 행을 표시할는 **RowStyle** 설정 및 **AlternatingRowStyle** 설정 합니다. |
| SelectedRowStyle | GridView 컨트롤에서 선택한 행에 대 한 스타일 설정입니다. |

표시 하거나 컨트롤의 다른 부분을 숨길 수 있습니다. 다음 표에서 표시 하거나 숨길 어느 부분을 제어 하는 속성을 나열 합니다.

| **Property** | **설명** |
| --- | --- |
| ShowFooter | 표시 하거나 GridView 컨트롤의 바닥글 섹션을 숨깁니다. |
| ShowHeader | 표시 하거나 GridView 컨트롤의 헤더 섹션을 숨깁니다. |

### <a name="events"></a>이벤트

GridView 컨트롤 프로그래밍할 수 있는 몇 가지 이벤트를 제공 합니다. 그러면 이벤트가 발생할 때마다 사용자 지정 루틴을 실행할 수 있습니다. 다음 표에서 GridView 컨트롤에서 지 원하는 이벤트를 나열 합니다.

| **Event** | **설명** |
| --- | --- |
| PageIndexChanged | 페이저 단추 중 하나를 클릭할 때 GridView 컨트롤 페이징 작업을 처리 한 후 발생 합니다. 이 이벤트는 사용자가 컨트롤에서 다른 페이지로 이동한 후 작업을 수행 해야 할 때 주로 사용 됩니다. |
| PageIndexChanging | GridView 하기 전에 컨트롤 페이징 작업을 처리 하지만 페이저 단추 중 하나를 클릭 하는 경우 발생 합니다. 이 이벤트는 자주 페이징 작업을 취소 하는 데 사용 됩니다. |
| RowCancelingEdit | 편집 모드를 종료 GridView 컨트롤 앞 행의 취소 단추를 클릭할 때 발생 합니다. 이 이벤트는 자주 취소 작업을 중지 하는 데 사용 됩니다. |
| RowCommand | GridView 컨트롤에 단추를 클릭할 때 발생 합니다. 이 이벤트는 자주 컨트롤에서 단추를 클릭 하면 작업을 수행 하는 데 사용 됩니다. |
| RowCreated | GridView 컨트롤에서 새 행을 만들 때 발생 합니다. 이 이벤트는 대개 행을 만들 때 행의 내용을 수정 합니다. |
| RowDataBound | 데이터 행 GridView 컨트롤의 데이터에 바인딩될 때 발생 합니다. 이 이벤트는 대개 행 데이터에 바인딩될 때 행의 내용을 수정 합니다. |
| RowDeleted | 행의 삭제 단추를 클릭 하면 데이터 원본에서 레코드를 삭제 하는 GridView 컨트롤 후 발생 합니다. 이 이벤트는 대개 삭제 작업의 결과 확인 합니다. |
| RowDeleting | 발생 한 행의 삭제 단추를 클릭 하면 GridView 하기 전에 컨트롤이 데이터 원본에서 레코드를 삭제 합니다. 이 이벤트는 종종 삭제 작업을 취소 하는 데 사용 됩니다. |
| RowEditing | GridView 하기 전에 컨트롤이 편집 모드로 전환 되었으면 하지만 행의 편집 단추를 클릭할 때 발생 합니다. 이 이벤트는 종종 편집 작업을 취소 하는 데 사용 됩니다. |
| RowUpdated | 행의 업데이트 단추를 클릭할 때 행을 업데이트 하는 GridView 컨트롤 후 발생 합니다. 이 이벤트는 대개 업데이트 작업의 결과 확인 합니다. |
| RowUpdating | 발생 행의 업데이트 단추를 클릭 하면 컨트롤이 GridView 하기 전에 행을 업데이트 합니다. 이 이벤트는 자주 업데이트 작업을 취소 하는 데 사용 됩니다. |
| SelectedIndexChanged | 행의 선택 단추를 클릭 하면 선택 작업을 처리 하는 GridView 컨트롤 후 발생 합니다. 이 이벤트는 컨트롤에서 행을 선택한 후 작업을 수행 하는 경우가 많습니다. |
| SelectedIndexChanging | 행의 선택 단추를 클릭 하 고, 컨트롤 GridView 하기 전에 선택 작업을 처리 하지만 때 발생 합니다. 이 이벤트는 종종 선택 작업을 취소 하는 데 사용 됩니다. |
| 정렬 | 열을 정렬 하는 하이퍼링크를 클릭 하는 경우 정렬 작업을 처리 하는 GridView 컨트롤 후 발생 합니다. 이 이벤트는 일반적으로 사용자가 열을 정렬에 대 한 하이퍼링크를 클릭 한 후 작업을 수행 하는 데 사용 됩니다. |
| 정렬 | 컨트롤이 GridView 하기 전에 정렬 작업을 처리 하지만 열을 정렬 하는 하이퍼링크를 클릭 하는 경우 발생 합니다. 이 이벤트는 정렬 작업을 취소 하거나 사용자 지정 정렬 루틴을 수행 하기 위해 종종 사용 됩니다. |

## <a name="formview"></a>FormView

FormView 컨트롤을 사용 하 여 데이터 원본에서 단일 레코드를 표시 합니다. 비슷합니다 DetailsView 컨트롤 행 필드 대신 사용자 정의 템플릿을 표시 합니다. 사용자 지정 템플릿을 만들어 보다 유연 하 게 제어 데이터가 표시 되는 방법을 제공 합니다. FormView 컨트롤에서는 다음과 같은 기능을 지원합니다.

- SqlDataSource ObjectDataSource 등 소스 컨트롤에 데이터 바인딩.
- 기본 제공 삽입 기능입니다.
- 기본 제공 업데이트 및 삭제 기능입니다.
- 기본 제공 페이징 기능입니다.
- 동적으로 속성을 설정 하려면 FormView 개체 모델에 대 한 프로그래밍 방식 액세스 이벤트를 처리 등에입니다.
- 사용자 정의 템플릿을, 테마 및 스타일을 통해 모양을 사용자 지정할 수 있습니다.

## <a name="templates"></a>템플릿

FormView 컨트롤 콘텐츠를 표시 하는 컨트롤의 다른 부분에 대 한 템플릿 만들기 해야 합니다. 대부분의 서식 파일은 선택 사항입니다. 그러나 컨트롤은 구성 모드에 대 한 템플릿을 만들어야 합니다. 예를 들어,를 지 원하는 레코드 삽입 FormView 컨트롤에 정의 된 삽입 항목 템플릿이 있어야 합니다. 다음 표에서 다양 한 템플릿을 만들 수 있는 나열 합니다.

| **템플릿 유형** | **설명** |
| --- | --- |
| EditItemTemplate | FormView 컨트롤이 편집 모드일에서 경우 데이터 행에 대 한 콘텐츠를 정의 합니다. 이 서식 파일에는 일반적으로 입력 컨트롤과 사용자 기존 레코드를 편집할 수 있는 명령 단추가 포함 되어 있습니다. |
| EmptyDataTemplate | FormView 컨트롤이 모든 레코드를 포함 하지 않는 데이터 소스에 바인딩된 경우에 표시 되는 빈 데이터 행에 대 한 콘텐츠를 정의 합니다. 이 서식 파일에는 일반적으로 사용자에 게 경고할 데이터 소스에 레코드가 포함 되어 있지 콘텐츠가 포함 됩니다. |
| FooterTemplate | 바닥글 행에 대 한 콘텐츠를 정의합니다. 이 템플릿에 일반적으로 바닥글 행에 표시 하려는 추가 콘텐츠를 포함 합니다. 대신 FooterText 속성을 설정 하 여 바닥글 행에 표시할 텍스트를 단순히 지정할 수 있습니다. |
| HeaderTemplate | 머리글 행에 대 한 콘텐츠를 정의합니다. 이 템플릿에 일반적으로 머리글 행에 표시 하려는 추가 콘텐츠를 포함 합니다. 대신 HeaderText 속성을 설정 하 여 머리글 행에 표시할 텍스트를 단순히 지정할 수 있습니다. |
| ItemTemplate | FormView 컨트롤이 읽기 전용 모드에 있을 때 데이터 행에 대 한 콘텐츠를 정의 합니다. 이 서식 파일에는 일반적으로 기존 레코드의 값을 표시 하는 내용이 들어 있습니다. |
| InsertItemTemplate | FormView 컨트롤이 삽입 모드일에서 경우 데이터 행에 대 한 콘텐츠를 정의 합니다. 이 서식 파일에는 일반적으로 입력 컨트롤과 사용자 새 레코드를 추가할 수 있는 명령 단추가 포함 되어 있습니다. |
| PagerTemplate | 페이징 기능을 활성화 하는 경우 표시 되는 호출기 행에 대 한 콘텐츠 정의 (AllowPaging 속성이로 설정 된 경우 **true**). 이 서식 파일에는 일반적으로 사용자 다른 레코드로 이동할 수 있는 컨트롤이 포함 됩니다. |

입력된 컨트롤 삽입 항목 템플릿을 확인 하 고 항목 템플릿 편집에서 양방향 바인딩 식을 사용 하 여 데이터 원본의 필드에 바인딩될 수 있습니다. 이 대 한 업데이트에 대 한 입력된 컨트롤의 값을 추출 하는 자동으로 또는 삽입 작업을 FormView 제어할을 수 있습니다. 양방향 바인딩 식에서 필드의 원래 값을 자동으로 표시 하려면 항목 템플릿을 편집할 입력된 컨트롤 할 수도 있습니다.

### <a name="binding-to-data"></a>데이터 바인딩

FormView 컨트롤을 데이터 소스 제어에 바인딩될 수 (같은 **SqlDataSource**, AccessDataSource, **ObjectDataSource** 등), 또는 구현 하는 모든 데이터 소스에는 (예: System.Data.DataView, System.Collections.ArrayList, System.Collections.Hashtable) System.Collections.IEnumerable 인터페이스입니다. 다음 방법 중 하나를 사용 하 여 FormView 컨트롤을 적절 한 데이터 원본 유형 바인딩할:

- 데이터 소스 제어에 바인딩할 FormView 컨트롤의 데이터 소스 컨트롤의 ID 값으로 설정 합니다. FormView 컨트롤의 지정 된 데이터 소스 제어에 자동으로 바인딩하고 활용할 수 데이터 소스 컨트롤의 기능을 삽입, 업데이트, 삭제 및 페이징 기능을 수행 합니다. 이것은 데이터에 바인딩하는 기본 방법입니다.
- 구현 하는 데이터 소스에 바인딩하는 **System.Collections.IEnumerable** 인터페이스 프로그래밍 방식으로 데이터 원본에 FormView 컨트롤의 DataSource 속성을 설정 하 고 다음 DataBind 메서드를 호출 합니다. 이 메서드를 사용 하면 기본 제공 삽입, 업데이트, 삭제 및 페이징 기능 FormView 컨트롤 제공 하지 않습니다. 적절 한 이벤트를 사용 하 여이 기능을 제공 해야 합니다.

## <a name="data-operations"></a>데이터 작업

FormView 컨트롤 업데이트, 삭제, 삽입 및 컨트롤의 항목을 페이징 하는 데 사용할 수 있는 다양 한 기본 제공 기능을 제공 합니다. FormView 컨트롤 데이터 소스 제어에 바인딩되어 FormView 컨트롤 데이터 소스 컨트롤의 기능을 사용할 수 있으며 자동 업데이트, 삭제, 삽입 및 페이징 기능을 제공 합니다. FormView 컨트롤 update, delete, insert 및 다른 유형의 데이터 원본과; 상호 페이징 작업에 대 한 지원을 제공할 수 있습니다. 그러나 이러한 작업에 대 한 구현으로 적절 한 이벤트 처리기를 제공 해야 합니다.

FormView 컨트롤 서식 파일을 사용 하므로 업데이트, 삭제 또는 삽입 작업을 수행 하는 명령 단추를 자동으로 생성 하는 방법을 제공 하지 않습니다. 적절 한 템플릿에 이러한 명령 단추를 직접 포함 해야 합니다. FormView 컨트롤이 인식 되어 있는 특정 단추 자신의 **CommandName** 속성이 특정 값으로 설정 합니다. 다음 표에서 FormView 컨트롤이 인식 하는 명령 단추를 나열 합니다.

| **Button** | **Commandname 값** | **설명** |
| --- | --- | --- |
| 취소 | "취소" | 작업을 취소 하 고 사용자가 입력 한 값을 취소할 수 업데이트 또는 삽입 작업에 사용 합니다. FormView 컨트롤 DefaultMode 속성에 지정 된 모드를 반환 합니다. |
| 삭제 | "Delete" | 데이터 소스에서 표시 된 레코드를 삭제 하려면 삭제 작업에 사용 합니다. ItemDeleting 및 ItemDeleted 이벤트를 발생 시킵니다. |
| 편집 | "Edit" | FormView 컨트롤 편집 모드로 전환 하 여 업데이트 작업에 사용 합니다. 에 지정 된 콘텐츠는 **EditItemTemplate** 속성은 데이터 행에 대해 표시 됩니다. |
| Insert | "삽입" | 삽입 작업에 사용자가 입력 한 값을 사용 하 여 데이터 원본에 새 레코드를 삽입 하려고 하는 데 사용 합니다. ItemInserting 및 ItemInserted 이벤트를 발생 시킵니다. |
| 새로 만들기 | "새" | FormView 컨트롤 삽입 모드로 전환할 삽입 작업에 사용 합니다. 에 지정 된 콘텐츠는 **InsertItemTemplate** 속성은 데이터 행에 대해 표시 됩니다. |
| 페이지 | "Page" | 페이징을 수행 하는 페이저 행에 있는 단추를 나타내기 위해 페이징 작업에서 사용 합니다. 페이징 작업을 지정 하려면는 **CommandArgument** "다음", "이전", "First", "마지막" 또는 탐색할 수 있는 페이지의 인덱스를 단추의 속성입니다. PageIndexChanging 및 PageIndexChanged 이벤트를 발생 시킵니다. |
| 업데이트 | "Update" | 사용자가 제공한 값이 포함 된 데이터 원본에 표시 된 레코드를 업데이트 하기 위해 업데이트 작업에 사용 합니다. ItemUpdating 및 ItemUpdated 이벤트를 발생 시킵니다. |

삭제와 달리 단추 (하 여 표시 된 레코드를 즉시 삭제)를 편집 하거나 새로 만들기 단추를 클릭 하면 편집 컨트롤이 전환 FormView 또는 각각 삽입 모드입니다. 에 포함 된 콘텐츠 편집 모드에는 **EditItemTemplate** 현재 데이터 항목에 대 한 속성이 표시 됩니다. 일반적으로 편집 항목 템플릿은 편집 단추 아래 템플릿으로 바뀝니다 업데이트 및 "취소" 단추가 되도록 정의 됩니다. 필드의 데이터 형식 (예: TextBox 또는 CheckBox 컨트롤)에 대 한 적절 한 입력된 컨트롤이 사용자 수정 하는 필드의 값으로도 일반적으로 표시 됩니다. 업데이트 단추를 클릭 하면 모든 변경 사항이 취소 단추를 클릭 데이터 원본의 레코드를 업데이트 합니다.

에 포함 된 콘텐츠와 마찬가지로,는 **InsertItemTemplate** 컨트롤이 삽입 모드일 때 데이터 항목에 대 한 속성이 표시 됩니다. Insert 항목 템플릿은 새로 만들기 단추는 삽입 및 취소 단추 대체 되 고 새 레코드에 대 한 값을 입력 하려면 사용자에 대 한 빈 입력된 컨트롤이 표시 됩니다에 일반적으로 정의 됩니다. 취소 단추를 클릭 하면 모든 변경 사항이 데이터 원본의 레코드를 삽입 삽입 단추를 클릭 합니다.

FormView 컨트롤에 사용자를 다른 데이터 원본의 레코드를 탐색할 수 있는 페이징 기능을 제공 합니다. 사용 하도록 설정 하면 페이저 행 페이지 탐색 컨트롤을 포함 하는 FormView 컨트롤에 표시 됩니다. 페이징을 사용 하려면 설정는 **AllowPaging** 속성을 **true**합니다. PagerStyle에 포함 된 개체의 속성과 PagerSettings 속성을 설정 하 여 호출기 행을 사용자 지정할 수 있습니다. 기본 제공 호출기 행 UI를 사용 하는 대신 사용 하 여 UI를 직접 만들 수는 **PagerTemplate** 속성입니다.

## <a name="customizing-the-user-interface"></a>사용자 인터페이스 사용자 지정

컨트롤의 다른 부분에 대 한 스타일 속성을 설정 하 여 FormView 컨트롤의 모양을 사용자 지정할 수 있습니다. 다음 표에서 다른 스타일 속성을 나열합니다.

| **스타일 속성** | **설명** |
| --- | --- |
| EditRowStyle | FormView 컨트롤 중인 경우에 데이터 행에 대 한 스타일 설정을 편집 모드입니다. |
| EmptyDataRowStyle | 데이터 원본에는 레코드가 없으면 FormView 컨트롤에 표시 되는 빈 데이터 행에 대 한 스타일 설정입니다. |
| FooterStyle | FormView 컨트롤의 바닥글 행에 대 한 스타일 설정입니다. |
| HeaderStyle | FormView 컨트롤의 머리글 행에 대 한 스타일 설정입니다. |
| InsertRowStyle | FormView 컨트롤 중인 경우에 데이터 행에 대 한 스타일 설정을 삽입 모드. |
| PagerStyle | 에 대 한 페이징 기능을 활성화 하는 경우 FormView 컨트롤에 표시 되는 호출기 행 스타일 설정입니다. |
| RowStyle | FormView 컨트롤이 읽기 전용 모드에 있을 때 데이터 행에 대 한 스타일 설정입니다. |

## <a name="events"></a>이벤트

FormView 컨트롤 프로그래밍할 수 있는 몇 가지 이벤트를 제공 합니다. 그러면 이벤트가 발생할 때마다 사용자 지정 루틴을 실행할 수 있습니다. 다음 표에서 FormView 컨트롤에서 지 원하는 이벤트를 나열 합니다.

| **Event** | **설명** |
| --- | --- |
| ItemCommand | FormView 컨트롤 내에서 단추를 클릭할 때 발생 합니다. 이 이벤트는 자주 컨트롤에서 단추를 클릭 하면 작업을 수행 하는 데 사용 됩니다. |
| ItemCreated | FormView 컨트롤에서 모든 FormViewRow 개체가 만들어진 후 발생 합니다. 이 이벤트는 대개 표시 되기 전에 레코드의 값을 수정 합니다. |
| ItemDeleted | 삭제 단추 발생 (단추 해당 **CommandName** 속성이 "Delete"로 설정)를 클릭 하면 되지만 FormView 컨트롤이 데이터 원본에서 레코드를 삭제 한 후 합니다. 이 이벤트는 대개 삭제 작업의 결과 확인 합니다. |
| ItemDeleting | FormView 하기 전에 컨트롤이 데이터 원본에서 레코드를 삭제 하지만 삭제 단추를 클릭할 때 발생 합니다. 이 이벤트는 종종 삭제 작업을 취소 하는 데 사용 됩니다. |
| ItemInserted | 삽입 단추 발생 (단추 해당 **CommandName** 속성이 "Insert"로 설정)를 클릭 하면 되지만 FormView 컨트롤이 레코드를 삽입 한 후 합니다. 이 이벤트는 종종 삽입 작업의 결과 확인 하는 데 사용 됩니다. |
| ItemInserting | FormView 하기 전에 레코드를 삽입 하지만 삽입 단추를 클릭할 때 발생 합니다. 이 이벤트는 자주 삽입 작업을 취소 하는 데 사용 됩니다. |
| ItemUpdated | 업데이트 단추를 사용 하는 경우에 발생 (단추 해당 **CommandName** 속성이 "업데이트"로 설정)를 클릭 하면 되지만 FormView 컨트롤이 행을 업데이트 한 후 합니다. 이 이벤트는 대개 업데이트 작업의 결과 확인 합니다. |
| ItemUpdating | FormView 하기 전에 레코드를 업데이트 하지만 업데이트 단추를 클릭할 때 발생 합니다. 이 이벤트는 자주 업데이트 작업을 취소 하는 데 사용 됩니다. |
| ModeChanged | FormView 컨트롤의 모드가 변경 후에 발생 (편집, 삽입 또는 읽기 전용 모드)에 있습니다. 이 이벤트는 자주 FormView 컨트롤의 모드가 변경 하면 작업을 수행 하는 데 사용 됩니다. |
| ModeChanging | FormView 컨트롤의 모드가 변경 되기 전에 발생 (편집, 삽입 또는 읽기 전용 모드)에 있습니다. 이 이벤트는 자주 모드 변경을 취소 하는 데 사용 됩니다. |
| PageIndexChanged | 페이저 단추 중 하나를 클릭할 때 FormView 컨트롤 페이징 작업을 처리 한 후 발생 합니다. 이 이벤트는 사용자가 컨트롤에서 다른 레코드로 이동한 후 작업을 수행 해야 할 때 주로 사용 됩니다. |
| PageIndexChanging | FormView 하기 전에 컨트롤 페이징 작업을 처리 하지만 페이저 단추 중 하나를 클릭 하는 경우 발생 합니다. 이 이벤트는 자주 페이징 작업을 취소 하는 데 사용 됩니다. |

## <a name="detailsview"></a>DetailsView

DetailsView 컨트롤 레코드의 각 필드는 테이블의 행에 표시 되는 위치는 테이블의 데이터 원본에서 단일 레코드를 표시 하려면 사용 됩니다. 마스터-세부 시나리오에 대 한 GridView 컨트롤과 함께에서 사용할 수 있습니다. DetailsView 컨트롤에는 다음 기능을 지원 합니다.

- SqlDataSource 등의 소스 제어에서 데이터 바인딩.
- 기본 제공 삽입 기능입니다.
- 기본 제공 업데이트 및 삭제 기능입니다.
- 기본 제공 페이징 기능입니다.
- 동적으로 속성을 설정 하려면 DetailsView 개체 모델에 대 한 프로그래밍 방식 액세스 이벤트를 처리 등에입니다.
- 테마 및 스타일을 통해 모양을 사용자 지정할 수 있습니다.

## <a name="row-fields"></a>행 필드

DetailsView 컨트롤의 각 데이터 행 필드 컨트롤을 선언 하 여 생성 됩니다. 여러 행 필드 형식을 컨트롤의 행의 동작을 결정 합니다. 필드 컨트롤 DataControlField에서 파생 됩니다. 다음 표에서 사용할 수 있는 여러 행 필드 형식을 나열 합니다.

| **열 필드 형식** | **설명** |
| --- | --- |
| BoundField | 데이터 원본의 필드의 값을 텍스트로 표시합니다. |
| ButtonField | DetailsView 컨트롤에 명령 단추를 표시합니다. 이 같은 프로그램 추가 / 제거 단추를 사용 하는 사용자 지정 단추 컨트롤을 사용 하 여 행을 표시할 수 있습니다. |
| CheckBoxField | DetailsView 컨트롤에서 확인란을 표시 합니다. 이 행 필드 형식은 부울 값을 사용 하는 필드를 표시 하려면 일반적으로 사용 됩니다. |
| CommandField | 기본 제공 명령 표시 편집을 수행 하는 단추 삽입 또는 DetailsView 컨트롤에서 작업을 삭제 합니다. |
| HyperLinkField | 데이터 원본의 필드의 값을 하이퍼링크로 표시 됩니다. 이 행 필드 형식을 사용 하면 두 번째 필드 하이퍼링크의 URL에 바인딩할 수 있습니다. |
| ImageField | DetailsView 컨트롤에 이미지를 표시 합니다. |
| TemplateField | 사용자 정의 콘텐츠 지정한 템플릿에 따라 DetailsView 컨트롤의 행에 대해 표시 됩니다. 이 행 필드 형식에는 사용자 지정 행 필드를 만들 수 있습니다. |

기본적으로 AutoGenerateRows 속성 설정 **true**, 데이터 원본에 바인딩할 수 있는 형식의 각 필드에 대 한 바인딩된 행 필드 개체를 자동으로 생성 합니다. 올바른 바인딩 가능한 유형은 문자열, DateTime, Decimal, Guid 및 기본 형식 집합입니다. 각 필드가 다음 행에 각 필드가 데이터 원본에 표시 되는 순서에 텍스트로 표시 됩니다.

자동으로 생성 되는 행 레코드의 모든 필드를 표시 하는 빠르고 쉬운 방법을 제공 합니다. 그러나 DetailsView의 사용할 수 있도록 컨트롤의 고급 기능 DetailsView 컨트롤에 포함할 행 필드를 명시적으로 선언 해야 합니다. 먼저 설정, 행 필드를 선언 하는 **AutoGenerateRows** 속성을 **false**합니다. 다음에 열기 및 닫기는 추가 **&lt;필드&gt;** 여는 태그와 닫는 태그 DetailsView 컨트롤 사이입니다. 마지막으로, 여는 태그와 닫는 간의 포함 시킬 행 필드를 나열 **&lt;필드&gt;** 태그입니다. 지정 된 행 필드는 나열 된 순서로 Fields 컬렉션에 추가 됩니다. **필드** 컬렉션 DetailsView 컨트롤에 있는 행 필드를 프로그래밍 방식으로 관리할 수 있습니다.

> [!NOTE]
> 자동으로 생성 된 행 필드 Fields 컬렉션에 추가 되지 않습니다.


## <a name="binding-to-data"></a>데이터 바인딩

DetailsView 컨트롤에 바인딩될 수 데이터 소스 제어와 같은 **SqlDataSource** 또는 AccessDataSource, 나 System.Data.DataView, 등의 System.Collections.IEnumerable 인터페이스를 구현 하는 모든 데이터 소스 System.Collections.ArrayList 및 System.Collections.Hashtable 합니다.

다음 방법 중 하나를 사용 하 여 적절 한 데이터 원본 유형에 DetailsView 컨트롤을 바인딩할:

- 데이터 소스 제어에 바인딩할 DetailsView 컨트롤의 데이터 소스 컨트롤의 ID 값으로 설정 합니다. DetailsView 컨트롤의 지정 된 데이터 소스 제어에 자동 바인딩됩니다. 이것은 데이터에 바인딩하는 기본 방법입니다.
- 구현 하는 데이터 소스에 바인딩하는 **System.Collections.IEnumerable** 인터페이스 프로그래밍 방식으로 데이터 원본에 DetailsView 컨트롤의 DataSource 속성을 설정 하 고 다음 DataBind 메서드를 호출 합니다.

## <a name="security"></a>보안

이 컨트롤 악의적인 클라이언트 스크립트가 포함 될 수 있습니다는 사용자 입력을 표시 하려면 사용할 수 있습니다. 응용 프로그램에 표시 하기 전에 실행 스크립트, SQL 문 또는 다른 코드에 대 한 클라이언트에서 보낸 모든 정보를 확인 합니다. ASP.NET은 사용자 입력에 있는 스크립트 블록 및 HTML에 있는 입력된 요청 유효성 검사 기능을 제공 합니다.

## <a name="data-operations"></a>데이터 작업

DetailsView 컨트롤 업데이트, 삭제, 삽입 및 컨트롤의 항목을 페이징 하는 데 사용할 수 있는 기본 제공 기능을 제공 합니다. DetailsView 컨트롤 데이터 소스 제어에 바인딩되어 DetailsView 컨트롤 데이터 소스 컨트롤의 기능을 사용할 수 있으며 자동 업데이트, 삭제, 삽입 및 페이징 기능을 제공 합니다.

DetailsView 컨트롤 update, delete, insert 및 다른 유형의 데이터 원본과; 상호 페이징 작업에 대 한 지원을 제공할 수 있습니다. 그러나 이러한 작업에 적절 한 이벤트 처리기에 대 한 구현을 제공 해야 합니다.

DetailsView 컨트롤에 자동으로 추가할 수는 **CommandField** 행 필드를 AutoGenerateEditButton,AutoGenerateDeleteButton,또는AutoGenerateInsertButton속성을설정하여편집,삭제또는새로만들기단추가있는**true**각각. 삭제와 달리 단추 (는 선택한 레코드를 즉시 삭제)를 편집 하거나 새로 만들기 단추를 클릭 하면 편집 컨트롤이 전환 DetailsView에 넣거나 모드에서는 각각. 편집 모드에서 편집 단추 업데이트 및 "취소" 단추가 바뀝니다. 사용자 수정 하는 필드의 값 필드의 데이터 형식 (예: TextBox 또는 CheckBox 컨트롤)에 대 한 적절 한 입력된 컨트롤이 표시 됩니다. 업데이트 단추를 클릭 하면 모든 변경 사항이 취소 단추를 클릭 데이터 원본의 레코드를 업데이트 합니다. 마찬가지로, 삽입 모드에서 새 단추는 삽입 및 취소 단추 대체 되 고 새 레코드에 대 한 값을 입력 하려면 사용자에 대 한 빈 입력된 컨트롤이 표시 됩니다.

DetailsView 컨트롤에 사용자를 다른 데이터 원본의 레코드를 탐색할 수 있는 페이징 기능을 제공 합니다. 사용 하도록 설정 하면 페이지 탐색 컨트롤 호출기 행에 표시 됩니다. 페이징을 사용 하도록 설정 하려면 AllowPaging 속성을 설정 **true**합니다. PagerStyle 및 PagerSettings 속성을 사용 하 여 호출기 행을 사용자 지정할 수 있습니다.

## <a name="customizing-the-user-interface"></a>사용자 인터페이스 사용자 지정

컨트롤의 다른 부분에 대 한 스타일 속성을 설정 하 여 DetailsView 컨트롤의 모양을 사용자 지정할 수 있습니다. 다음 표에서 다른 스타일 속성을 나열합니다.

| **스타일 속성** | **설명** |
| --- | --- |
| AlternatingRowStyle | DetailsView 컨트롤에 교대로 반복 되는 데이터 행 스타일 설정입니다. RowStyle 설정 간의 교대로 반복 되는 데이터 행을 표시할 때이 속성을 설정 및 **AlternatingRowStyle** 설정 합니다. |
| CommandRowStyle | DetailsView 컨트롤에 있는 기본 제공 명령 단추를 포함 하는 행 스타일 설정입니다. |
| EditRowStyle | DetailsView 컨트롤 중인 경우에 데이터 행에 대 한 스타일 설정을 편집 모드입니다. |
| EmptyDataRowStyle | 데이터 원본에는 레코드가 없으면 DetailsView 컨트롤에 표시 되는 빈 데이터 행에 대 한 스타일 설정입니다. |
| FooterStyle | DetailsView 컨트롤의 바닥글 행에 대 한 스타일 설정입니다. |
| HeaderStyle | DetailsView 컨트롤의 머리글 행에 대 한 스타일 설정입니다. |
| InsertRowStyle | DetailsView 컨트롤 중인 경우에 데이터 행에 대 한 스타일 설정을 삽입 모드. |
| PagerStyle | DetailsView 컨트롤의 호출기 행에 대 한 스타일 설정입니다. |
| RowStyle | DetailsView 컨트롤에 데이터 행 스타일 설정입니다. 경우는 **AlternatingRowStyle** 도 속성이 설정 되어, 교대로 데이터 행을 표시할는 **RowStyle** 설정 및 **AlternatingRowStyle** 설정 합니다. |
| FieldHeaderStyle | DetailsView 컨트롤의 머리글 열에 대 한 스타일 설정입니다. |

## <a name="events"></a>이벤트

DetailsView 컨트롤 프로그래밍할 수 있는 몇 가지 이벤트를 제공 합니다. 그러면 이벤트가 발생할 때마다 사용자 지정 루틴을 실행할 수 있습니다. 다음 표에서 DetailsView 컨트롤에서 지 원하는 이벤트를 나열 합니다. DetailsView 컨트롤의 기본 클래스에서 이러한 이벤트를 상속: 데이터 바인딩, 데이터 바인딩된, 삭제, Init, 부하, PreRender, 및 렌더링 합니다.

| **Event** | **설명** |
| --- | --- |
| ItemCommand | DetailsView 컨트롤에 단추를 클릭할 때 발생 합니다. |
| ItemCreated | DetailsView 컨트롤에 모든 DetailsViewRow 개체가 만들어진 후 발생 합니다. 이 이벤트는 대개 표시 되기 전에 레코드의 값을 수정 합니다. |
| ItemDeleted | 삭제 단추를 클릭할 때 DetailsView 컨트롤이 데이터 원본에서 레코드를 삭제 한 후 발생 합니다. 이 이벤트는 대개 삭제 작업의 결과 확인 합니다. |
| ItemDeleting | DetailsView 하기 전에 컨트롤이 데이터 원본에서 레코드를 삭제 하지만 삭제 단추를 클릭할 때 발생 합니다. 이 이벤트는 종종 삭제 작업을 취소 하는 데 사용 됩니다. |
| ItemInserted | DetailsView 컨트롤 레코드를 삽입 한 후 하지만 삽입 단추를 클릭할 때 발생 합니다. 이 이벤트는 종종 삽입 작업의 결과 확인 하는 데 사용 됩니다. |
| ItemInserting | DetailsView 하기 전에 레코드를 삽입 하지만 삽입 단추를 클릭할 때 발생 합니다. 이 이벤트는 자주 삽입 작업을 취소 하는 데 사용 됩니다. |
| ItemUpdated | 업데이트 단추를 클릭할 때 DetailsView 컨트롤의 행을 업데이트 하 고 나면 발생 합니다. 이 이벤트는 대개 업데이트 작업의 결과 확인 합니다. |
| ItemUpdating | DetailsView 하기 전에 레코드를 업데이트 하지만 업데이트 단추를 클릭할 때 발생 합니다. 이 이벤트는 자주 업데이트 작업을 취소 하는 데 사용 됩니다. |
| ModeChanged | DetailsView 컨트롤 (편집, 삽입 또는 읽기 전용 모드) 모드 변경 되 면 발생 합니다. 이 이벤트는 자주 DetailsView 컨트롤의 모드가 변경 하면 작업을 수행 하는 데 사용 됩니다. |
| ModeChanging | DetailsView 컨트롤 (편집, 삽입 또는 읽기 전용 모드) 모드를 변경 하기 전에 발생 합니다. 이 이벤트는 자주 모드 변경을 취소 하는 데 사용 됩니다. |
| PageIndexChanged | 페이저 단추 중 하나를 클릭할 때 DetailsView 컨트롤 페이징 작업을 처리 한 후 발생 합니다. 이 이벤트는 사용자가 컨트롤에서 다른 레코드로 이동한 후 작업을 수행 해야 할 때 주로 사용 됩니다. |
| PageIndexChanging | DetailsView 하기 전에 컨트롤 페이징 작업을 처리 하지만 페이저 단추 중 하나를 클릭 하는 경우 발생 합니다. 이 이벤트는 자주 페이징 작업을 취소 하는 데 사용 됩니다. |

## <a name="the-menu-control"></a>Menu 컨트롤

ASP.NET 2.0에서 Menu 컨트롤은 완전 한 기능의 내비게이션 시스템이 하도록 설계 되었습니다. SiteMapDataSource와 같은 계층적 데이터 원본에 쉽게 데이터 바인딩된 수 있습니다.

컨트롤의 메뉴 구조 선언적으로 또는 동적으로 정의할 수 있으며 단일 루트 노드와 하위 노드를 개수에 관계 없이 구성 됩니다. 다음 코드는 선언적으로 메뉴 컨트롤에 대 한 메뉴를 정의합니다.

[!code-aspx[Main](data-bound-controls/samples/sample4.aspx)]

위의 예에는 Home.aspx 노드는 루트 노드입니다. 다른 모든 노드는 다양 한 수준에서 루트 노드 내에 중첩 되어 있습니다.

메뉴 컨트롤은 렌더링할 수; 메뉴의 두 가지 정적 메뉴와 동적 메뉴입니다. 정적 메뉴의 항상 표시 되는 메뉴 항목으로 구성 됩니다. 동적 메뉴 에게만 표시 되는 사용자의 마우스 위로 가져갈 때 메뉴 항목으로 구성 됩니다. 선언적으로 정의 하는 메뉴가 있는 정적 메뉴의 및는 런타임에 데이터 바인딩된 메뉴가 있는 동적 메뉴에 종종 고객 혼동 수 있습니다. 사실, 동적 및 정적 메뉴 모집단의 메서드에 관련이 없는 합니다. 용어 *정적* 및 *동적* 참조 메뉴의 정적으로 기본적으로 표시 되거나만 인지 아닌지에 사용자가 동작을 수행 하는 경우에 표시 합니다.

**수준이 StaticDisplayLevels** 속성 메뉴 수준의 수 정적 이며 따라서 표시 기본적으로 구성 하는 데 사용 됩니다. 위의 예제에서는 설정는 **수준이 StaticDisplayLevels** 속성 값이 2 정적으로 홈 노드, 음악 노드 및 동영상 노드를 표시 하려면 메뉴으 리라 예상 합니다. 부모 노드를 가리킬 때 다른 모든 노드의 동적으로 표시 됩니다.

**MaximumDynamicDisplayLevels** 최대 수를 구성 하는 속성 동적 수준의 메뉴는 표시할 수 있습니다. 에 지정 된 값 보다 높은 수준에서 동적 메뉴는 **MaximumDynamicDisplayLevels** 속성이 삭제 됩니다.

> [!NOTE]
> 것이 거의 확실 MaximumDynamicDisplayLevels 속성으로 인해 렌더링에 메뉴가 표시 되지 없는 상황을 발생할 수 있습니다. 이 경우 속성에서 충분히 고객 메뉴의 표시를 허용 하도록 설정 되어 있는지를 확인 합니다.


## <a name="data-binding-the-menu-control"></a>데이터 바인딩 메뉴 컨트롤

메뉴 컨트롤은 SiteMapDataSource 또는 XMLDataSource 등 모든 계층적 데이터 원본에 바인딩할 수 있습니다. SiteMapDataSource는 자주 사용 하는 메서드는 메뉴 컨트롤에 데이터 바인딩에 대 한 Web.sitemap 파일에서 피드를 해당 스키마 메뉴 컨트롤에 알려진된 API를 제공 하기 때문에입니다. 아래 목록에는 간단한 Web.sitemap 파일을 보여 줍니다.

[!code-xml[Main](data-bound-controls/samples/sample5.xml)]

루트 siteMapNode 요소가 하나만,이 경우 홈 요소 인지 확인 합니다. 각 siteMapNode에 대 한 몇 가지 특성을 구성할 수 있습니다. 가장 일반적으로 사용 되는 특성은:

- **url** 메뉴 항목을 클릭할 때 표시할 URL을 지정 합니다. 이 특성이 없으면 클릭할 때 노드에서 단순히 게시 합니다.
- **제목** 메뉴 항목에 표시 되는 텍스트를 지정 합니다.
- **설명** 노드에 대 한 설명서로 사용 합니다. 또한 노드 위에 마우스를 가져갈 때 도구 설명으로 표시 합니다.
- **siteMapFile** 중첩된 사이트맵을 허용 합니다. 이 특성을 제대로 구성 된 ASP.NET 사이트 맵 파일을 가리켜야 합니다.
- **역할** 노드 모양에 대 한 ASP.NET 보안 트리밍에 의해 제어 하도록 허용 합니다.

Note 이러한 특성은 모두 선택적 항목, 동작 메뉴의 아닐 수도 있다는 지정 하지 않은 경우 실행 되는 것입니다. 예를 들어 경우는 *url* 특성을 지정 하지만 *설명* 특성이 아니므로, 노드가 표시 되지 것입니다 및 방법이 지정 된 URL로 이동 됩니다.

## <a name="controlling-a-menus-operation"></a>메뉴 작업을 제어합니다.

ASP.NET Menu 컨트롤;의 작동에 영향을 주는 속성이 여러 **방향** 속성을는 **DisappearAfter** 속성에는 **StaticItemFormatString** 속성 및 **StaticPopoutImageUrl**속성은이 중 일부입니다.

- **방향** 수로 설정할 수 *가로* 또는 *세로* 정적 메뉴 항목에 누적 세로 및 가로로 배치 행 또는 세로로 하는지 여부를 제어 합니다. 연결할 수 있습니다. 이 속성은 동적 메뉴에 영향을 주지 않습니다.
- **DisappearAfter** 속성 시간으로 동적 메뉴를 계속 표시 마우스 후에 구성 밖으로 이동한 합니다. 값은 500 밀리초에 지정 됩니다. 이 속성 값이-1 설정 하면 메뉴 하지 자동으로 사라집니다. 이 경우 메뉴는 메뉴의 바깥쪽을 클릭 하는 경우에 사라집니다.
- **StaticItemFormatString** 속성을 사용 하면 일관 된 스크립트를 사용 하면 메뉴 시스템에서 유지 관리 하기 쉬운 합니다. 이 속성을 지정 하는 경우 *{0}* 데이터 소스에 표시 되는 설명을 입력 해야 합니다. 예를 들어 연습 1 say Our 제품 페이지 방문에서 메뉴 항목 등을 얻으려면 우리의 {0}는 StaticItemFormatString에 대 한 페이지 방문을 지정 합니다. 런타임 시 ASP.NET는 {0}의 임의의 발생 항목을 메뉴 항목에 대 한 올바른 설명으로 바꿉니다.
- **StaticPopoutImageUrl** 속성 특정 메뉴 노드 위로 이동 하 여 액세스할 수 있는 자식 노드에 있음을 나타내는 데 사용 되는 이미지를 지정 합니다. 기본 이미지를 사용 하는 동적 메뉴 계속 됩니다.

## <a name="templated-menu-controls"></a>템플릿 기반 메뉴 컨트롤

Menu 컨트롤 템플릿 기반 컨트롤 이며 두 개의 서로 다른 ItemTemplates;에 대 한 허용 합니다. StaticItemTemplate 및는 DynamicItemTemplate 합니다. 이러한 서식 파일을 사용 하 여 쉽게 추가할 수 있습니다 서버 컨트롤 또는 사용자 정의 컨트롤 메뉴에 있습니다.

Visual Studio.NET에서 서식 파일을 편집 하려면 메뉴에서 스마트 태그 단추를 클릭 하 고 템플릿 편집을 선택 하거나 합니다. StaticItemTemplate 또는 DynamicItemTemplate 편집 간에 선택할 수 있습니다.

페이지가 로드는 StaticItemTemplate에 추가 된 모든 컨트롤은 정적 메뉴에 표시 됩니다. DynamicItemTemplate에 추가 된 모든 컨트롤은 모든 팝업 메뉴에 표시 됩니다.

## <a name="menu-events"></a>메뉴 이벤트

메뉴 컨트롤은 두 개의 고유한 이벤트를 적용 합니다. **MenuItemClicked** 및 **MenuItemDatabound** 이벤트입니다.

MenuItemClicked 이벤트는 메뉴 항목을 클릭할 때 발생 합니다. MenuItemDatabound 이벤트 메뉴 항목이 데이터 바인딩된 되었을 때 발생 합니다. **MenuEventArgs** 전달 되는 이벤트에 처리기 항목 속성을 통해 메뉴 항목에 대 한 액세스를 제공 합니다.

## <a name="controlling-a-menus-appearance"></a>메뉴 모양 제어

또한 형식 메뉴를 사용할 수 있는 많은 스타일 중 하나 이상을 사용 하 여 메뉴 컨트롤의 모양을 변경할 수 있습니다. 이 중에 **StaticMenuStyle**, **DynamicMenuStyle**, **DynamicMenuItemStyle**, **DynamicSelectedStyle**, 및 **DynamicHoverStyle**합니다. 이러한 속성은 표준 HTML 스타일 문자열을 사용 하 여 구성 됩니다. 예를 들어 다음는 동적 메뉴에 대 한 스타일을 적용 됩니다.

[!code-aspx[Main](data-bound-controls/samples/sample6.aspx)]

> [!NOTE]
> Hover 스타일 중 하나를 사용 하는 경우 추가 해야 합니다는 &lt;h e a d&gt; 요소에서 사용 하 여 페이지를는 *runat* 요소로 설정 *서버*합니다.


메뉴 컨트롤에는 또한 ASP.NET 2.0 테마의 사용할을 수 있습니다.

## <a name="the-treeview-control"></a>TreeView 컨트롤

TreeView 컨트롤 트리와 같은 구조에 데이터를 표시합니다. Menu 컨트롤을와 마찬가지로 쉽게 수는 SiteMapDataSource 같은 모든 계층적 데이터 소스에 바인딩된 데이터입니다.

ASP.NET 2.0에서 TreeView 컨트롤에 대해 질문을 하는 첫 번째 질문은 여부와 관련이 ASP.NET에 사용할 수 있는 TreeView IE WebControl 1.x 합니다. 그것이 아니야. ASP.NET 2.0 TreeView 컨트롤 기초부터 쓴 및 이전에 제공 된 IE TreeView WebControl 비해 훨씬 향상 된 기능을 제공 합니다.

않겠습니다 세부 메뉴 컨트롤과 동일한 방식으로 수행 하는 것을 사이트 맵을 TreeView 컨트롤을 바인딩할 하는 방법에 있습니다. 그러나 TreeView 컨트롤에 작동 하는 방식으로 고유한 몇 가지 차이점이 있습니다.

기본적으로 TreeView 컨트롤 완전히 확장 된 나타납니다. 초기 로드 시 확장 수준을 변경 하려면 수정 된 **ExpandDepth** 컨트롤의 속성입니다. 트리 뷰에서 특정 노드를 확장에 데이터 바인딩된 경우에 특히 유용 합니다.

## <a name="databinding-the-treeview-control"></a>TreeView 컨트롤에 데이터 바인딩

Menu 컨트롤을 달리 TreeView 수 있게 해줍니다 많은 양의 데이터를 처리 합니다. 따라서 SiteMapDataSource 또는 XMLDataSource에 데이터 바인딩 외에도 트리 뷰에서 데이터 집합 또는 기타 관계형 데이터에 바인딩된 데이터입니다. 이 경우 TreeView 컨트롤 많은 양의 데이터에 바인딩되는 컨트롤에 실제로 표시 되는 데이터에만 바인딩할 가장 좋습니다. 데이터에서 추가 데이터에 바인딩 불가 TreeView 노드를 확장 한 다음 할 수 있습니다.

이러한 경우에는 **PopulateOnDemand** TreeView의 속성 설정 해야 *true*합니다. 에 대 한 구현을 제공 해야 합니다는 **TreeNodePopulate** 메서드.

## <a name="data-binding-without-postback"></a>데이터 다시 게시 하지 않고 바인딩

처음으로 이전 예제에서 노드를 확장 하면 페이지 다시 게시 및 새로 고침을 확인 합니다. 이 예제에 아무런 문제가 없습니다 thats 많은 양의 데이터를 프로덕션 환경에서 수도 있다는 하는 한다고 가정 합니다. 더 나은 시나리오는 TreeView 여전히 동적으로 해당 노드를 채울 하는 서버에 다시 게시 하지 않고도 하나 것입니다.

설정 하 여는 **알** 및 **PopulateOnDemand** 속성을 true로 ASP.NET TreeView 컨트롤에서 노드 다시 게시 하지 않고 동적으로 채워집니다. 부모 노드가 확장 되 면 클라이언트에서 XMLHttp 요청 만들어지고 OnTreeNodePopulate 이벤트가 발생 합니다. 그런 다음 데이터에 사용 되는 XML 데이터 아일랜드로 서버 응답 자식 노드를 바인딩합니다.

ASP.NET이이 기능을 구현 하는 클라이언트 코드를 동적으로 만듭니다. &lt;스크립트&gt; AXD 파일을 가리키는 스크립트를 포함 하는 태그 생성 됩니다. 예를 들어 아래 목록에는 XMLHttp 요청을 생성 하는 스크립트 코드에 대 한 스크립트 링크가 표시 됩니다.

[!code-html[Main](data-bound-controls/samples/sample7.html)]

브라우저에서 위의 AXD 파일을 검색 하 고 열면 XMLHttp 요청을 구현 하는 코드를 표시 됩니다. 이 메서드는 스크립트 파일을 수정할 수 없도록 고객을 방지 합니다.

## <a name="controlling-the-operation-of-the-treeview-control"></a>TreeView 컨트롤의 작업을 제어합니다.

TreeView 컨트롤에 컨트롤의 작동에 영향을 주는 여러 가지 속성이 있습니다. 가장 확실 한 속성은는 **ShowCheckBoxes**, **ShowExpandCollapse**, 및 **ShowLines**합니다.

**ShowCheckBoxes** 확인란 렌더링 될 때 노드는 표시 여부 속성에 영향을 줍니다. 이 속성에 대 한 유효한 값은 **None**, **루트**, **부모**, **리프**, 및 **모든**합니다. 이러한 영향을 줄 TreeView 컨트롤 다음과 같습니다.

| **속성 값** | **효과** |
| --- | --- |
| 없음 | 모든 노드에서 확인란 표시 되지 않습니다. 이것이 기본 설정입니다. |
| 루트 | 확인란은 루트 노드에 표시 됩니다. |
| 부모 | 확인란은 해당 노드의 자식 노드는 표시 됩니다. 이러한 자식 노드는 부모 노드 또는 리프 노드 수 있습니다. |
| 리프 | Checkbox에 자식 노드가 있는 노드에 대해서만 표시 됩니다. |
| 모두 | Checkbox 모든 노드에 표시 됩니다. |

확인란을 사용 하는 경우는 **CheckedNodes** 속성은 TreeView 노드 포스트백에 체크 인 된 컬렉션을 반환 합니다.

**ShowExpandCollapse** 속성 루트와 부모 노드 옆에 확장/축소 이미지의 모양을 제어 합니다. 이 속성은로 설정 하는 경우 **false**, TreeView 하이퍼링크로 렌더링 됩니다 노드와 링크를 클릭 하 여 확장/축소 되어 있습니다.

**ShowLines** 속성 여부 줄 부모 노드 자식 노드를 연결 표시 여부를 제어 합니다. 때 **false** (기본값) 이면 줄이 더 표시 됩니다. 때 **true**, TreeView 컨트롤 이미지 줄을 사용 하 여 지정 된 폴더에는 **LineImagesFolder** 속성입니다.

TreeView 선 표시를 사용자 지정, Visual Studio.NET 2005에 선 디자이너 도구를 포함 합니다. 아래으로 TreeView 컨트롤에서 스마트 태그 단추를 사용 하 여이 도구를 액세스할 수 있습니다.


![](data-bound-controls/_static/image1.jpg)

**그림 1**


선택 하는 경우는 **선 이미지 사용자 지정** 메뉴 옵션을 TreeView 선의 모양을 구성할 수 있게 하 선 디자이너 도구를 시작 됩니다.

## <a name="treeview-events"></a>TreeView 이벤트

TreeView 컨트롤에는 다음과 같은 고유한 이벤트에 있습니다.

- 에 따라 SelectedNodeChanged 노드를 선택 하는 경우에 발생는 **SelectAction** 속성입니다.
- TreeNodeCheckChanged 노드 checkboxs 상태가 변경 되 면 발생 합니다.
- 에 따라 TreeNodeExpanded 노드를 확장 하는 경우에 발생는 **SelectAction** 속성입니다.
- TreeNodeCollapsed 노드를 축소 하는 경우에 발생 합니다.
- 바인딩된 TreeNodeDataBound 노드가 있는 경우 데이터에 발생 합니다.
- TreeNodePopulate 노드를 채울 때 발생 합니다.

**SelectAction** 속성 노드가 선택 될 때 이벤트 발생을 구성할 수 있습니다. SelectAction 속성에서는 다음 작업을 제공합니다.

- TreeNodeSelectAction.Expand 발생 TreeNodeExpanded 때 노드를 선택 합니다.
- TreeNodeSelectAction.None는 노드가 선택 되었을 때 이벤트가 발생 합니다.
- TreeNodeSelectAction.Select은 노드가 선택 되었을 때 SelectedNodeChanged 이벤트를 발생 시킵니다.
- TreeNodeSelectAction.SelectExpand는 SelectedNodeChanged 이벤트 및 TreeNodeExpanded 이벤트 노드가 선택 되었을 때 발생 합니다.

## <a name="controlling-appearance-with-styles"></a>스타일으로 모양 제어

TreeView 컨트롤 스타일으로 컨트롤의 모양을 제어 하기 위한 여러 속성을 제공 합니다. 다음 속성을 사용할 수 있습니다.

| **속성 이름** | **컨트롤** |
| --- | --- |
| HoverNodeStyle | 마우스 위로 가져갈 때 노드 스타일을 제어 합니다. |
| LeafNodeStyle | 리프 노드 스타일을 제어합니다. |
| NodeStyle | 모든 노드에 대 한 스타일을 제어합니다. 특정 노드 스타일 (예: LeafNodeStyle)이이 스타일을 재정의합니다. |
| ParentNodeStyle | 모든 부모 노드에 대 한 스타일을 제어합니다. |
| RootNodeStyle | 루트 노드에 대 한 스타일을 제어합니다. |
| SelectedNodeStyle | 선택한 노드에 대 한 스타일을 제어합니다. |

이러한 각 속성은 읽기 전용입니다. 그러나 각 반환 되도록는 **TreeNodeStyle** 개체를 해당 개체의 속성을 수정할 수를 사용 하 여는 *속성 하위 속성* 형식입니다. 예를 들어, 설정 하는 **ForeColor** 의 속성은 **SelectedNodeStyle**, 다음 구문을 사용:

[!code-aspx[Main](data-bound-controls/samples/sample8.aspx)]

위의 태그가 닫히지 않은 확인 합니다. 여기에 표시 하는 선언적 구문을 사용 하 여, HTML 코드를 사용할 경우에 트리 뷰 노드를 포함 하는 때문입니다.

스타일 속성을 사용 하 여 코드에서 지정할 수도 있습니다는 *property.subproperty* 형식입니다. 예를 들어, 설정 하는 **ForeColor** 의 속성은 **RootNodeStyle** 코드에서는 다음 구문을 사용:

[!code-csharp[Main](data-bound-controls/samples/sample9.cs)]

> [!NOTE]
> 다른 스타일 속성의 전체 목록을, TreeNodeStyle 개체에 MSDN 설명서를 참조 합니다.


## <a name="the-sitemappath-control"></a>SiteMapPath 컨트롤

SiteMapPath 컨트롤은 ASP.NET 개발자를 위한 bread crumb 탐색 컨트롤을 제공 합니다. 다른 탐색 컨트롤 처럼 쉽게 수 계층적 데이터에 바인딩된 데이터가 SiteMapDataSource XmlDataSource 등의 원본입니다.

SiteMapPath 컨트롤 SiteMapNodeItem 개체 이루어집니다. 세 가지 방법으로 노드; 루트 노드, 부모 노드, 및 현재 노드 중에서 선택 합니다. 루트 노드는 계층 구조 맨 위에 있는 노드입니다. 현재 노드는 현재 페이지를 나타냅니다. 다른 모든 노드는 부모 노드입니다.

## <a name="controlling-the-operation-of-the-sitemappath-control"></a>SiteMapPath 컨트롤의 작업을 제어합니다.

SiteMapPath 컨트롤의 작업을 제어 하는 속성은 다음과 같습니다.

| **Property** | **속성의 설명** |
| --- | --- |
| ParentLevelsDisplayed | 얼마나 많은 부모 노드 표시 여부를 제어 합니다. 기본값은-1에 표시 되는 부모 노드 수를 제한 하지 않습니다. |
| PathDirection | SiteMapPath의 방향을 제어합니다. 유효한 값은 RootToCurrent (기본값) 및 CurrentToRoot입니다. |
| PathSeparator | SiteMapPath 컨트롤의 노드를 구분 하는 문자를 제어 하는 문자열입니다. 기본값은: 합니다. |
| RenderCurrentNodeAsLink | 현재 노드가 링크로 렌더링 되는 여부를 제어 하는 부울 값입니다. 기본값은 False입니다. |
| SkipLinkText | 내게 필요한 옵션 화면 판독기가 페이지를 볼 때 하도록 지원 합니다. 이 속성에는 화면 판독기를 SiteMapPath 컨트롤을 건너뛸 수 있습니다. 이 기능을 해제 하려면 string.empty 속성을 설정 합니다. |

## <a name="templated-sitemappath-controls"></a>템플릿 기반 SiteMapPath 컨트롤

SiteMapControl 템플릿 기반 컨트롤 이며 이와 같이 컨트롤을 표시에서 사용 하기 위해 서로 다른 템플릿을 정의할 수 있습니다. SiteMapPath 컨트롤에서 서식 파일을 편집 하려면 컨트롤에서 스마트 태그 단추를 클릭 하 고 메뉴에서 템플릿 편집을 선택 합니다. 사용할 수 있는 다양 한 템플릿을 선택할 수 있는 위치는 아래와 같이 SiteMapTasks 메뉴를 표시 됩니다.


![](data-bound-controls/_static/image2.jpg)

**그림 2**


**NodeTemplate** 는 SiteMapPath의 노드에 템플릿을 참조 합니다. 이 노드는 루트 노드 또는 현재 노드 및 **RootNodeTemplate** 또는 **CurrentNodeTemplate** 가 구성, NodeTemplate 재정의 됩니다.

## <a name="sitemappath-events"></a>SiteMapPath 이벤트

SiteMapPath 컨트롤에 컨트롤 클래스;에서 파생 되지 않은 두 개의 이벤트 **ItemCreated** 이벤트 및 **ItemDataBound** 이벤트입니다. ItemCreated 이벤트 SiteMapPath 항목이 만들어질 때 발생 합니다. ItemDataBound는 SiteMapPath 노드의 데이터 바인딩 중 DataBind 메서드를 호출할 때 발생 합니다. A **SiteMapNodeItemEventArgs** 개체는 항목 속성을 통해 특정 SiteMapNodeItem에 대 한 액세스를 제공 합니다.

## <a name="controlling-appearance-with-styles"></a>스타일으로 모양 제어

다음 스타일은 SiteMapPath 컨트롤의 서식 지정에 사용할 수 있습니다.

| **속성 이름** | **컨트롤** |
| --- | --- |
| CurrentNodeStyle | 현재 노드의 텍스트의 스타일을 제어합니다. |
| RootNodeStyle | 루트 노드에 대 한 텍스트의 스타일을 제어합니다. |
| NodeStyle | CurrentNodeStyle 또는 RootNodeStyle 적용 하지 않는 것으로 가정 하는 모든 노드에 대 한 텍스트의 스타일을 제어 합니다. |

CurrentNodeStyle 또는 RootNodeStyle NodeStyle 속성이 재정의 됩니다. 이러한 각 속성은 읽기 전용 및 반환 된 **스타일** 개체입니다. 이러한 속성 중 하나를 사용 하 여 노드 모양에 영향을 주지만 반환 되는 스타일 개체의 속성을 설정 해야 합니다. 예를 들어 아래 코드는 현재 노드의 forecolor 속성을 변경합니다.

[!code-aspx[Main](data-bound-controls/samples/sample10.aspx)]

속성을 다음과 같이 프로그래밍 방식으로 적용할 수도 있습니다.

[!code-csharp[Main](data-bound-controls/samples/sample11.cs)]

> [!NOTE]
> 서식 파일을 적용 하면 스타일 적용 되지 않습니다.


## <a name="lab-1-configuring-an-aspnet-menu-control"></a>랩 1: ASP.NET Menu 컨트롤 구성

1. 새 웹 사이트를 만듭니다.
2. 파일, 새로 만들기, 파일을 선택 하 고 사이트 맵 파일 템플릿 목록에서 선택 하 여 사이트 맵 파일을 추가 합니다.
3. 사이트 맵 (기본적으로 Web.sitemap)를 열고 아래 목록에 모양이 되도록 수정 합니다. 사이트 맵 파일에 연결 하려는 페이지, 실제로 존재 하지 않지만이 연습에 대 한 문제가 되지 않습니다.

    [!code-xml[Main](data-bound-controls/samples/sample12.xml)]
4. 디자인 뷰에서 기본 Web form을 엽니다.
5. 도구 상자의 탐색 섹션에서 페이지에 새 메뉴 컨트롤을 추가 합니다.
6. 도구 상자의 데이터 섹션에서 새 SiteMapDataSource를 추가 합니다. SiteMapDataSource 사이트의 Web.sitemap 파일을 자동으로 사용 됩니다. (Web.sitemap 파일 *해야* 사이트의 루트 폴더에 있어야 합니다.)
7. 메뉴 컨트롤을 클릭 하 고 메뉴 작업 대화 상자를 표시 하려면 스마트 태그 단추를 클릭 합니다.
8. 데이터 소스 선택 드롭다운 목록에서 SiteMapDataSource1를 선택 합니다.
9. 자동 서식 링크를 클릭 하 고 메뉴에 대 한 형식을 선택 합니다.
10. 속성 창에서 설정 된 **수준이 StaticDisplayLevels** 속성을 2로 합니다. Menu 컨트롤 디자이너에서 홈, 제품 및 서비스 노드에 이제 표시 해야 합니다.
11. 메뉴를 사용 하 여 브라우저에서 페이지를 찾습니다. (사이트 map에 추가 된 적 페이지 실제로 존재 하지 않거나, 때문에 오류가 표시 됩니다는 시도를 찾는 경우.)

수준이 StaticDisplayLevels와 MaximumDynamicDisplayLevels 속성을 변경 하 여 시험해 하 고 메뉴를 렌더링 하는 방식을 어떻게 영향을 확인 합니다.

## <a name="lab-2-dynamically-binding-a-treeview-control"></a>랩 2: TreeView 컨트롤을 동적으로 바인딩

이 연습에서는 Northwind 데이터베이스가 있는 SQL Server 인스턴스에서 로컬로 실행 중인 SQL Server 한지 가정 합니다. 이러한 조건이 충족 되지 샘플에서 연결 문자열을 변경 하십시오. 트러스트 된 연결 하는 대신 SQL Server 인증을 지정 하려면 할 수 있는지 확인 합니다.

1. 새 웹 사이트를 만듭니다.
2. Default.aspx 코드 뷰로 전환 하 고 모든 코드는 아래 코드로 바꿉니다. 

    [!code-aspx[Main](data-bound-controls/samples/sample13.aspx)]
3. Treeview.aspx로 페이지를 저장 합니다.
4. 페이지를 찾습니다.
5. 페이지를 처음 표시할 때 브라우저에서 페이지의 소스를 봅니다. 클라이언트에만 표시 되는 노드 보낸 참고 합니다.
6. 임의의 노드 옆의 더하기 기호를 클릭 합니다.
7. 페이지를 다시 소스를 봅니다. 이제 새로 표시 된 노드에 있는지 확인 합니다.

## <a name="lab-3-details-view-and-editing-data-using-a-gridview-and-detailsview"></a>랩 3: 보기 및 편집 GridView 및 DetailsView를 사용 하 여 데이터에 자세히 설명

1. 새 웹 사이트를 만듭니다.
2. 웹 사이트를 새 web.config를 추가 합니다.
3. 아래와 같이 web.config 파일에 연결 문자열을 추가 합니다. 

    [!code-xml[Main](data-bound-controls/samples/sample14.xml)]

    > [!NOTE]
    > 사용자 환경에 따라 연결 문자열을 변경 해야 합니다.
4. web.config 파일을 저장한 다음 닫습니다.
5. Default.aspx를 열고 새 SqlDataSource 컨트롤을 추가 합니다.
6. SqlDataSource 컨트롤의 ID 변경 **제품**합니다.
7. 에 **SqlDataSource 작업** 메뉴를 클릭 하 여 **데이터 소스 구성**합니다.
8. 선택 **Northwind** 연결 드롭다운에서 다음을 클릭 합니다.
9. 선택 **제품** 에서 **이름** 드롭다운 하 고 확인 된 **ProductID**, **ProductName**, **UnitPrice**, 및 **UnitsInStock** 아래와 같이 확인란을 선택 합니다. 

![](data-bound-controls/_static/image3.jpg)

    **Figure 3**
10. **다음**을 클릭합니다.
11. **마침**을 클릭합니다.
12. 소스 뷰로 전환 하 고 생성 된 코드를 검사 합니다. 공지는 **SelectCommand**, **DeleteCommand**, **InsertCommand**, 및 **UpdateCommand** SqlDataSource에 추가 된 컨트롤입니다. 또한 추가 된 매개 변수를 확인 하십시오.
13. 디자인 뷰로 전환 하 고 페이지에 새 GridView 컨트롤을 추가 합니다.
14. 선택 **제품** 에서 **데이터 소스 선택** 드롭다운입니다.
15. 확인 **페이징 사용** 및 **선택 가능** 다음과 같이 합니다. 

![](data-bound-controls/_static/image4.jpg)

    **Figure 4**
16. 클릭는 **열 편집** 에 연결 하 고 있는지 확인 **필드 자동 생성** 을 선택 합니다.
17. **확인**을 클릭합니다.
18. GridView 컨트롤을 선택 하 고 클릭 단추 옆에 **DataKeyNames** 속성 창에서 속성입니다.
19. 선택 **ProductID** 에서 **사용 가능한 데이터 필드** 나열 하 고 클릭는 **&gt;** 단추를 추가 합니다.
20. 확인을 클릭합니다.
21. 페이지에 새 SqlDataSource 컨트롤을 추가 합니다.
22. SqlDataSource 컨트롤의 ID 변경 **세부 정보**합니다.
23. SqlDataSource 작업 메뉴에서 선택 **데이터 소스 구성**합니다.
24. 선택 **Northwind** 드롭다운을 클릭 하 여 **다음**합니다.
25. 선택 <strong>제품</strong> 에서 <strong>이름</strong> 드롭다운 확인 하 고는 <strong> \<강력한 / > * 확인란을 선택은 <strong>열</strong> listbox 합니다.
26. 클릭는 **여기서** 단추입니다.
27. 선택 **ProductID** 에서 **열** 드롭다운입니다.
28. 선택 **=** 연산자 드롭다운에 있습니다.
29. 선택 **제어** 에서 **소스** 드롭다운입니다.
30. 선택 **GridView1** 에서 **컨트롤 ID** 드롭다운입니다.
31. 클릭는 **추가** 단추를 WHERE 절을 추가 합니다.
32. **확인**을 클릭합니다.
33. 클릭는 **고급** 단추 및 확인 된 **생성 INSERT, UPDATE 및 DELETE 문을** 확인란을 선택 합니다.
34. **확인**을 클릭합니다.
35. 클릭 **다음** 클릭 **마침**합니다.
36. DetailsView 컨트롤을 페이지에 추가 합니다.
37. 에 **데이터 소스 선택** 드롭다운에서 선택 **세부 정보**합니다.
38. 확인 된 **편집 사용** 아래와 같이 확인란을 선택 합니다. 

![](data-bound-controls/_static/image1.gif)

    **Figure 5**
39. 페이지를 저장 하 고 Default.aspx를 찾습니다.
40. 클릭는 **선택** DetailsView 업데이트를 자동으로 볼 수 있는 다른 레코드 옆에 있는 링크입니다.
41. 클릭는 **편집** DetailsView 컨트롤에 링크 합니다.
42. 레코드를 변경 하 고 클릭 **업데이트**합니다.
