---
uid: web-forms/overview/data-access/basic-reporting/displaying-data-with-the-objectdatasource-cs
title: "ObjectDataSource (C#)를 사용 하 여 데이터를 표시 합니다. | Microsoft Docs"
author: rick-anderson
description: "이 자습서에서는 havi 없이 이전 자습서에서 만든 BLL에서 검색 된 데이터를 바인딩할 수 있습니다이 컨트롤을 사용 하 여 ObjectDataSource 컨트롤 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: af882aef-56f5-4e9a-8f95-3977fde20e74
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/displaying-data-with-the-objectdatasource-cs
msc.type: authoredcontent
ms.openlocfilehash: 8025a4d236d126b939b44fac9114ae3d0e98f6ad
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="displaying-data-with-the-objectdatasource-c"></a>ObjectDataSource (C#)를 사용 하 여 데이터를 표시합니다.
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_4_CS.exe) 또는 [PDF 다운로드](displaying-data-with-the-objectdatasource-cs/_static/datatutorial04cs1.pdf)

> ObjectDataSource 컨트롤 코드 줄을 작성 하지 않고도 이전 자습서에서 만든 BLL에서 검색 된 데이터를 바인딩할 수 있습니다이 컨트롤을 사용 하 여이 자습서에서는!


## <a name="introduction"></a>소개

이 응용 프로그램 아키텍처 및 웹 사이트 페이지 레이아웃 완료에서는 다양 한 데이터 및 보고 관련 일반 작업을 수행 하는 방법을 보여 시작할 준비가 된 것입니다. 이전 자습서에서 프로그래밍 방식으로 데이터는 ASP.NET 페이지의 웹 컨트롤에는 DAL 및 BLL에서 데이터를 바인딩하는 방법을 살펴보았습니다. 이 구문은 데이터 웹 컨트롤의 할당 `DataSource` 속성을 표시 한 다음 컨트롤의 데이터로 `DataBind()` 메서드 ASP.NET 1.x 응용 프로그램에서 사용 되는 패턴 였으며 계속 2.0 응용 프로그램에서 사용할 수 있습니다. 그러나 ASP.NET 2.0의 새로운 데이터 소스 컨트롤 데이터로 작업 하는 선언적 방법을 제공 합니다. 만든 BLL에서 검색 된 데이터를 바인딩할 수 있습니다 이러한 컨트롤을 사용 하 여 [이전 자습서](../introduction/creating-a-business-logic-layer-cs.md) 코드 줄을 작성 하지 않고도!

ASP.NET 2.0 5 개의 기본 제공 데이터 소스 제어와 함께 제공 [SqlDataSource](https://msdn.microsoft.com/en-us/library/dz12d98w(vs.80).aspx), [AccessDataSource](https://msdn.microsoft.com/en-us/library/8e5545e1.aspx), [ObjectDataSource](https://msdn.microsoft.com/en-us/library/9a4kyhcx.aspx), [XmlDataSource](https://msdn.microsoft.com/en-us/library/e8d8587a(en-US,VS.80).aspx), 및 [SiteMapDataSource](https://msdn.microsoft.com/en-us/library/5ex9t96x(en-US,VS.80).aspx) 직접 만들 수 있지만 [사용자 지정 데이터 소스 컨트롤과](https://msdn.microsoft.com/library/default.asp?url=/library/en-us/dnvs05/html/DataSourceCon1.asp), 필요한 경우. 아키텍처에는 자습서 응용 프로그램에 대 한 개발 했습니다, 이후 사용할 예정 된 ObjectDataSource BLL 클래스에 대 한 합니다.


![ASP.NET 2.0 5 개의 기본 제공 데이터 소스 제어를 포함합니다.](displaying-data-with-the-objectdatasource-cs/_static/image1.png)

**그림 1**: ASP.NET 2.0에 5 개의 기본 제공 데이터 소스 컨트롤이 포함 됩니다.


ObjectDataSource는 몇 가지 다른 개체를 사용 하기 위한 프록시로 사용 됩니다. ObjectDataSource를 구성 하려면 지정이 내부 개체 및 해당 메서드는 ObjectDataSource에 매핑되는 방식을 `Select`, `Insert`, `Update`, 및 `Delete` 메서드. 이 내부 개체를 지정 하 고 해당 메서드는 ObjectDataSource에 매핑된 데이터 웹 컨트롤에는 ObjectDataSource 다음 바인딩할 수 있습니다. ASP.NET 웹 컨트롤을 다른 규칙 으로부터 GridView, DetailsView, RadioButtonList, 및 DropDownList를 포함 하 여 많은 데이터와 함께 제공 됩니다. 페이지 수명 주기 동안 웹 컨트롤 데이터는 해당 ObjectDataSource를 호출 하 여 수행 됩니다, 바인딩된 데이터에 액세스 해야 할 수 `Select` 메서드; 웹 컨트롤 데이터 삽입, 업데이트, 지원 또는 삭제, 있습니다 호출을 하는 경우 해당 ObjectDataSource의 `Insert`, `Update`, 또는 `Delete` 메서드. 다음 다이어그램에서 같이 적절 한 기본 개체의 메서드에 objectdatasource 이러한 호출은 다음 라우팅됩니다.


[![프록시로 ObjectDataSource 역할](displaying-data-with-the-objectdatasource-cs/_static/image3.png)](displaying-data-with-the-objectdatasource-cs/_static/image2.png)

**그림 2**: The ObjectDataSource 역할을 프록시 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image4.png))


삽입 하기 위한 메서드를 호출 하 여 ObjectDataSource를 사용할 수 있지만, 업데이트 또는 삭제, 방금에 대해 중점적으로 설명 데이터; 반환 이후 자습서 ObjectDataSource 및 웹 컨트롤에 데이터를 수정 하는 데이터를 사용 하 여 탐색 합니다.

## <a name="step-1-adding-and-configuring-the-objectdatasource-control"></a>1 단계: 추가 및 ObjectDataSource 컨트롤 구성

열어 시작는 `SimpleDisplay.aspx` 페이지에 `BasicReporting` 폴더를 디자인 뷰로 전환 하 고 다음 ObjectDataSource 컨트롤 도구 상자 페이지의 디자인 화면으로 끕니다. ObjectDataSource; 태그를 생성 하지 않으므로 디자인 화면에서 회색 상자로 표시 단순히 지정된 된 개체에서 메서드를 호출 하 여 데이터를 액세스 합니다. 데이터 GridView, DetailsView, FormView, 등의 웹 컨트롤을 여는 ObjectDataSource에서 반환 된 데이터를 표시할 수 있습니다.

> [!NOTE]
> 또는 년 5 월 첫 번째 페이지에 웹 컨트롤 데이터 추가 스마트 태그를 선택 합니다는 &lt;새 데이터 원본을&gt; 드롭 다운 목록에서 옵션입니다.


ObjectDataSource의 원본 개체와 해당 개체의 메서드는 ObjectDataSource에 매핑되는 방식을 지정 하려면 ObjectDataSource의 스마트 태그에서 데이터 소스 구성 링크를 클릭 합니다.


[![클릭 하 고 스마트 태그에서 데이터 원본 링크를 구성 합니다.](displaying-data-with-the-objectdatasource-cs/_static/image6.png)](displaying-data-with-the-objectdatasource-cs/_static/image5.png)

**그림 3**: 스마트 태그에서 구성 데이터 원본 링크를 클릭 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image7.png))


데이터 소스 구성 마법사가 표시 됩니다. 첫째,는 ObjectDataSource 작업할 개체를 지정 해야 합니다. 이 화면에서 드롭 다운 목록으로 데코레이팅 되었습니다 하는 개체만 나열 "데이터 구성 요소만 표시" 확인란을 선택 하는 경우는 `DataObject` 특성입니다. 현재 목록 형식화 된 데이터 집합 및 이전 자습서에서 만든 BLL 클래스에는 Tableadapter를 포함 합니다. 추가 하려면 잊은 경우는 `DataObject` 특성 비즈니스 논리 계층 클래스에 표시 되지 않습니다을이 목록에 있습니다. 이 경우 BLL 클래스 (함께 형식화 된 데이터 집합의 Datatable, Datarow, 및 등의 다른 클래스)을 포함 하는 모든 개체를 보려면 "데이터 구성 요소만 표시" 확인란의 선택을 취소 합니다.

이 첫 번째 화면에서 선택 된 `ProductsBLL` 드롭 다운 목록에서 클래스 하 고 다음을 클릭 합니다.


[![ObjectDataSource 컨트롤에서 사용할 개체를 지정 합니다.](displaying-data-with-the-objectdatasource-cs/_static/image9.png)](displaying-data-with-the-objectdatasource-cs/_static/image8.png)

**그림 4**: ObjectDataSource 컨트롤을 사용 하 여 개체를 지정 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image10.png))


마법사의 다음 화면은 ObjectDataSource를 호출 해야 하는 어떤 방법을 선택 하 라는 메시지를 표시 합니다. 드롭다운 목록에는 이전 화면에서 선택한 개체의 데이터를 반환 하는 이러한 방법을 나열 합니다. 여기 보면 `GetProductByProductID`, `GetProducts`, `GetProductsByCategoryID`, 및 `GetProductsBySupplierID`합니다. 선택은 `GetProducts` 드롭 다운 목록에서 클릭 방법을 완료 (추가한 경우는 `DataObjectMethodAttribute` 에 `ProductBLL`의 메서드는 이전 자습서에서이 옵션에 나와 있는 것 처럼 기본적으로 선택 됩니다).


[![선택 탭에서 데이터를 반환 하기 위해 메서드를 선택 합니다.](displaying-data-with-the-objectdatasource-cs/_static/image12.png)](displaying-data-with-the-objectdatasource-cs/_static/image11.png)

**그림 5**: SELECT 탭에서 데이터 반환에 대 한 방법을 선택 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image13.png))


## <a name="configure-the-objectdatasource-manually"></a>ObjectDataSource를 수동으로 구성

ObjectDataSource의 데이터 소스 구성 마법사는 사용 하 여 개체를 지정 하 고 연결 개체의 어떤 메서드가 호출 되는 빠른 방법을 제공 합니다. 그러나 속성 창을 통해 또는 직접 선언 태그에서에서 해당 속성을 통해 ObjectDataSource를 구성할 수, 있습니다. 설정 하기만 `TypeName` 속성을 사용할 수는 기본 개체의 형식 및 `SelectMethod` 에 데이터를 검색할 때 호출할 메서드입니다.


[!code-aspx[Main](displaying-data-with-the-objectdatasource-cs/samples/sample1.aspx)]

데이터 소스 구성 마법사를 중지 해야 ObjectDataSource를 수동으로 구성 하는 마법사만 개발자가 만든 클래스를 나열 하는 경우가 있을 수 있습니다 선호 하는 경우에. 와 같은.NET Framework의 클래스에는 ObjectDataSource를 바인딩할 하려는 경우는 [멤버 자격 클래스](https://msdn.microsoft.com/en-us/library/system.web.security.membership.aspx), 사용자 계정 정보에 액세스할 수 또는 [디렉터리 클래스](https://msdn.microsoft.com/en-us/library/system.io.directory.aspx) 파일 시스템 정보를 작성 하려면 ObjectDataSource의 속성을 수동으로 설정 해야 합니다.

## <a name="step-2-adding-a-data-web-control-and-binding-it-to-the-objectdatasource"></a>2 단계: 데이터 웹 컨트롤을 추가 하 고는 ObjectDataSource에 바인딩

웹 컨트롤 데이터는 ObjectDataSource에서 반환 된 데이터를 표시 하려면 페이지를 추가 하려면 준비 되었는지는 ObjectDataSource가 페이지에 추가 하 고 구성 된 `Select` 메서드. 모든 데이터 웹 컨트롤 ObjectDataSource;에 바인딩할 수 있습니다. GridView, DetailsView, 및 FormView에서 ObjectDataSource의 데이터 표시에서 살펴보겠습니다.

## <a name="binding-a-gridview-to-the-objectdatasource"></a>GridView에서 ObjectDataSource에 바인딩

도구 상자에서 GridView 컨트롤 추가 `SimpleDisplay.aspx`의 디자인 화면입니다. GridView의 스마트 태그에서 1 단계에서에서 추가 ObjectDataSource 컨트롤을 선택 합니다. 이 자동으로 만듭니다 BoundField ObjectDataSource의에서 데이터에 의해 반환 된 각 속성에 대 한 GridView `Select` 메서드 (즉, 제품 DataTable에 정의 된 속성).


[![페이지에는 GridView 파트가 추가 된 ObjectDataSource에 바인딩되고](displaying-data-with-the-objectdatasource-cs/_static/image15.png)](displaying-data-with-the-objectdatasource-cs/_static/image14.png)

**그림 6**: A GridView에 추가한 페이지와는 ObjectDataSource에 바인딩된 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image16.png))


그런 다음 사용자 지정, 다시 정렬 하거나 제거할 수 있습니다 GridView의 BoundFields 스마트 태그에서 열 편집 옵션을 클릭 하 여 합니다.


[![GridView의 BoundFields 편집 열 대화 상자를 통해 관리](displaying-data-with-the-objectdatasource-cs/_static/image18.png)](displaying-data-with-the-objectdatasource-cs/_static/image17.png)

**그림 7**: 관리 GridView의 BoundFields 통해 the 편집 열 대화 상자 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image19.png))


제거 하는 GridView의 BoundFields 수정 하는 `ProductID`, `SupplierID`, `CategoryID`, `QuantityPerUnit`, `UnitsInStock`, `UnitsOnOrder`, 및 `ReorderLevel` BoundFields 합니다. BoundField 왼쪽 아래에에서 있는 목록에서 선택 하 고 (빨간색 X) 제거 하려면 삭제 단추를 클릭 하기만 하면 합니다. 다음으로 BoundFields 다시 정렬 하는 `CategoryName` 및 `SupplierName` BoundFields 앞에 `UnitPrice` BoundField 이러한 BoundFields를 선택 하 고 위쪽 화살표를 클릭 하 여 합니다. 설정의 `HeaderText` 에 나머지 BoundFields의 속성 `Products`, `Category`, `Supplier`, 및 `Price`각각. 다음으로 `Price` BoundField의 서식이 통화로 지정는 BoundField의 설정 하 여 `HtmlEncode` 속성을 false로 및 해당 `DataFormatString` 속성을 `{0:c}`합니다. 마지막으로, 가로로 맞출지는 `Price` 오른쪽 및 `Discontinued` 통해 센터의 확인란을 선택은 `ItemStyle` / `HorizontalAlign` 속성입니다.


[!code-aspx[Main](displaying-data-with-the-objectdatasource-cs/samples/sample2.aspx)]


[![GridView의 BoundFields 사용자 지정 된](displaying-data-with-the-objectdatasource-cs/_static/image21.png)](displaying-data-with-the-objectdatasource-cs/_static/image20.png)

**그림 8**: GridView의 BoundFields 사용자 지정 된 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image22.png))


## <a name="using-themes-for-a-consistent-look"></a>테마를 사용 하 여 일관성 있는 모양을 위해

모든 권한 수준의 스타일 설정을 제거 하기 위해 노력 이러한 자습서, 가능 하면 항상 외부 파일에 정의 된 스타일 시트를 사용 하는 대신 합니다. `Styles.css` 파일에 포함 되어 `DataWebControlStyle`, `HeaderStyle`, `RowStyle`, 및 `AlternatingRowStyle` 웹이 자습서에 사용 되는 컨트롤의 데이터 모양 지정에 사용 해야 하는 CSS 클래스입니다. 이를 위해 GridView의 설정 수 `CssClass` 속성을 `DataWebControlStyle`, 및 해당 `HeaderStyle`, `RowStyle`, 및 `AlternatingRowStyle` 속성 `CssClass` 속성 적절 하 게 합니다.

이러한 설정 하는 경우 `CssClass` 각각의 모든 데이터에 대 한 이러한 속성 값을 명시적으로 설정 해야 할 웹 컨트롤에 속성 웹 컨트롤 우리의 자습서에 추가 합니다. DetailsView, GridView에 대 한 기본 CSS 관련 속성을 정의 하는 보다 관리 하기 쉬운 방법입니다 및 FormView 테마를 사용 하 여 제어 합니다. 테마는 컨트롤 수준 속성 설정, 이미지 및 일반적인 모양과 느낌을 적용 하는 사이트 전체 페이지에 적용할 수 있는 CSS 클래스의 컬렉션입니다.

이 테마는 모든 이미지 또는 CSS 파일에 포함 되지 않습니다 (스타일 시트도 두겠습니다 `Styles.css` 로-웹 응용 프로그램의 루트 폴더에 정의 된,), 하지만 두 스킨을 포함 합니다. 스킨은 웹 컨트롤에 대 한 기본 속성을 정의 하는 파일입니다. 특히, 되 겠 GridView 및 DetailsView 컨트롤 스킨 파일을 나타내는 기본 `CssClass`-관련 속성입니다.

시작 이라는 프로젝트에 새 스킨 파일을 추가 하 여 `GridView.skin` 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가 선택 하 여 합니다.


[![GridView.skin 라는 스킨 파일](displaying-data-with-the-objectdatasource-cs/_static/image24.png)](displaying-data-with-the-objectdatasource-cs/_static/image23.png)

**그림 9**: 스킨 파일 라는 추가 `GridView.skin` ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image25.png))


에 있는 스킨 파일에 테마를 배치할 필요는 `App_Themes` 폴더입니다. 이러한 폴더를 아직 않아도 되므로 Visual Studio는 첫 번째 우리의 스킨을 추가할 때을 수행해 줍니다 하나를 만들기 위해 수행할 제공 합니다. 사용 하려면는 `App_Theme` 폴더 새 배치 `GridView.skin` 파일 있습니다.


[![Visual Studio App_Theme 폴더를 만들 수 있도록](displaying-data-with-the-objectdatasource-cs/_static/image27.png)](displaying-data-with-the-objectdatasource-cs/_static/image26.png)

**그림 10**: Visual Studio 만들 수는 `App_Theme` 폴더 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image28.png))


새 테마 만들어집니다는 `App_Themes` 스킨 파일 GridView 라는 폴더 `GridView.skin`합니다.


![GridView 테마에 추가 된 App_Theme 폴더에](displaying-data-with-the-objectdatasource-cs/_static/image29.png)

**그림 11**: The GridView 테마에 추가 된에 `App_Theme` 폴더


DataWebControls에 GridView 테마 이름 바꾸기 (에서 GridView 폴더를 마우스 오른쪽 단추로 클릭는 `App_Theme` 폴더 이름 바꾸기를 선택). 다음으로, 입력에 다음 태그는 `GridView.skin` 파일:


[!code-aspx[Main](displaying-data-with-the-objectdatasource-cs/samples/sample3.aspx)]

에 대 한 기본 속성을 정의 합니다.는 `CssClass`-DataWebControls 테마를 사용 하는 모든 페이지에서 모든 GridView에 대 한 관련 속성입니다. DetailsView 데이터 곧 사용할 예정 웹 컨트롤에 대 한 다른 스킨을 추가 해 보겠습니다. 새 스킨 라는 DataWebControls 테마에 추가 `DetailsView.skin` 다음 태그를 추가 합니다.


[!code-aspx[Main](displaying-data-with-the-objectdatasource-cs/samples/sample4.aspx)]

우리의 테마 정의 보면 ASP.NET 페이지에 테마를 적용를 마지막 단계가입니다. 페이지 단위로 또는 웹 사이트의 모든 페이지에 대 한 테마를 적용할 수 있습니다. 웹 사이트의 모든 페이지에 대 한이 테마를 사용 합니다. 이를 위해 다음 태그를 추가 `Web.config`의 `<system.web>` 섹션:


[!code-xml[Main](displaying-data-with-the-objectdatasource-cs/samples/sample5.xml)]

그을 마쳤습니다. `styleSheetTheme` 설정은 테마에서 지정한 속성이 표시 되지 않도록 나타냅니다 *하지* 제어 수준에서 지정 된 속성을 재정의 합니다. 테마 설정을 제어 설정을 종사자 해야를 지정 하려면는 `theme` 대신 특성 `styleSheetTheme`; 아쉽게도 테마 설정을 통해 지정 된는 `theme` 특성 Visual Studio 디자인 보기에 표시 되지 않습니다. 참조 [ASP.NET 테마 및 스킨 개요](https://msdn.microsoft.com/en-us/library/ykzx33wh.aspx) 및 [서버 쪽 스타일을 사용 하 여 테마](https://quickstarts.asp.net/quickstartv20/aspnet/doc/themes/stylesheettheme.aspx) 테마와 스킨;에 대 한 자세한 내용은 참조 [방법: ASP.NET 테마 적용](https://msdn.microsoft.com/en-us/library/0yy5hxdk(VS.80).aspx) 에 대 한 자세한 페이지 테마를 사용 하도록 구성 합니다.


[![GridView 제품의 이름, 범주, 공급 업체, 가격 및 지원 되지 않는 정보를 표시합니다.](displaying-data-with-the-objectdatasource-cs/_static/image31.png)](displaying-data-with-the-objectdatasource-cs/_static/image30.png)

**그림 12**: 제품의 이름, 범주, 공급 업체, 가격 및 지원 되지 않는 정보를 표시 하는 GridView ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image32.png))


## <a name="displaying-one-record-at-a-time-in-the-detailsview"></a>DetailsView에서 한 번에 하나의 레코드를 표시합니다.

연결 된 데이터 소스 제어에서 반환 된 각 레코드에 대해 하나의 행을 표시 하는 GridView입니다. 그러나 때 한 번에 유일한 레코드 또는 포함 된 단일 레코드를 표시 해야 할 경우가 있습니다. [DetailsView 컨트롤](https://msdn.microsoft.com/en-us/library/s3w1w7t4.aspx) 는 HTML로 렌더링 합니다.이 기능을 제공 `<table>` 두 개의 열과 각 열 또는 컨트롤에 바인딩된 속성에 대해 한 행입니다. DetailsView는 단일 레코드 90도 회전된 된 GridView로 생각할 수 있습니다.

DetailsView 컨트롤을 추가 하 여 시작 *위에* 에 GridView `SimpleDisplay.aspx`합니다. 다음으로, GridView로 동일한 ObjectDataSource 컨트롤에 바인딩하십시오. ObjectDataSource의 반환 되는 개체의 각 속성에 대 한 DetailsView에 추가 됩니다 BoundField GridView와 마찬가지로 `Select` 메서드. 유일한 차이점은 세로로 아닌 가로로 DetailsView의 BoundFields 레이아웃 됩니다.


[![DetailsView의 페이지에 추가 하 고는 ObjectDataSource에 바인딩](displaying-data-with-the-objectdatasource-cs/_static/image34.png)](displaying-data-with-the-objectdatasource-cs/_static/image33.png)

**그림 13**: DetailsView의 페이지에 추가 하 고는 ObjectDataSource 바인딩할 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image35.png))


GridView 처럼 DetailsView의 BoundFields는 ObjectDataSource에서 반환 된 데이터의 추가 사용자 지정 된 표시를 제공 하기 작성할 수 있습니다. 그림 14 해당 BoundFields 후 DetailsView를 표시 및 `CssClass` 속성 GridView 예제와 비슷한 모양이 확인 하도록 구성 되었습니다.


[![DetailsView 단일 레코드를 표시합니다.](displaying-data-with-the-objectdatasource-cs/_static/image37.png)](displaying-data-with-the-objectdatasource-cs/_static/image36.png)

**그림 14**: DetailsView 단일 레코드를 표시 합니다. ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image38.png))


참고 DetailsView만 해당 데이터 소스에서 반환 된 첫 번째 레코드를 표시 합니다. 사용자가 한 번에 하나씩 레코드를 모두 단계별로 실행 되도록 허용 하려면 DetailsView에 대 한 페이징을 사용 하도록 설정 해야 합니다. 이렇게 하려면 Visual Studio로 반환 하 고 DetailsView의 스마트 태그에서 페이징 사용 확인란을 확인 합니다.


[![DetailsView 컨트롤에서 페이징 사용](displaying-data-with-the-objectdatasource-cs/_static/image40.png)](displaying-data-with-the-objectdatasource-cs/_static/image39.png)

**그림 15**: DetailsView 컨트롤에서 페이징 사용 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image41.png))


[![페이징을 사용, DetailsView을 허용 하는 사용자가 제품 중 하나를 볼 수](displaying-data-with-the-objectdatasource-cs/_static/image43.png)](displaying-data-with-the-objectdatasource-cs/_static/image42.png)

**그림 16**: 페이징 사용 DetailsView을 허용 하는 사용자가 제품 중 하나를 볼 수 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image44.png))


자습서를 나중에 페이징 하는 방법에 대 한 자세히 설명 합니다.

## <a name="a-more-flexible-layout-for-showing-one-record-at-a-time"></a>한 번에 하나의 레코드를 표시 하는 데 보다 유연한 레이아웃

DetailsView에는 ObjectDataSource에서 반환 된 각 레코드를 표시 하는 방법을 상당히 고정 된 관계로입니다. 데이터의 보다 유연한 보기가 좋겠습니다. 예를 들어 별도 행에는 제품 이름, 범주, 공급 업체, 가격 및 지원 되지 않는 정보를 표시 하는 대신 하려는 제품 이름을 표시 하 고에 가격는 `<h4>` 제목에서 표시 되는 범주 및 공급 업체 정보 이름 및 글꼴 크기의 가격 아래 합니다. 및에서는 값 옆에 있는 속성 이름 (제품, 범주 및 등)을 표시 하려면 중요 하지 않을 수 있습니다.

[FormView 컨트롤](https://msdn.microsoft.com/en-US/library/fyf1dk77.aspx) 사용자 지정의이 수준을 제공 합니다. FormView에서는 다양 한 웹 컨트롤에 정적 HTML 허용 하는 서식 파일 필드 (예: GridView 및 DetailsView 수행 됨)를 사용 하 여 하지 않고 사용 및 [구문이](http://www.15seconds.com/issue/040630.htm)합니다. ASP.NET에서 반복기 컨트롤에 잘 알고 있다면 경우 1.x 이라고 수 있습니다 FormView의 단일 레코드를 표시 하는 데 반복 합니다.

FormView 컨트롤을 추가 `SimpleDisplay.aspx` 페이지의 디자인 화면입니다. 처음 FormView 표시 된 회색 블록으로 us에 최소한 컨트롤의 제공 해야 함을 `ItemTemplate`합니다.


[![FormView 반드시에 ItemTemplate 포함](displaying-data-with-the-objectdatasource-cs/_static/image46.png)](displaying-data-with-the-objectdatasource-cs/_static/image45.png)

**그림 17**: The FormView 포함 되어야 합니다는 `ItemTemplate` ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image47.png))


FormView 기본 만드는 FormView의 스마트 태그를 통해 데이터 소스 제어에 직접 바인딩할 수 있습니다 `ItemTemplate` 자동으로 (함께 `EditItemTemplate` 및 `InsertItemTemplate`경우 ObjectDatatSource 컨트롤의 `InsertMethod` 및 `UpdateMethod` 속성 설정). 그러나이 예에서는 보겠습니다 데이터를 FormView 바인딩하고 지정 해당 `ItemTemplate` 수동으로 합니다. FormView의 설정 하 여 시작 `DataSourceID` 속성을는 `ID` ObjectDataSource 컨트롤의 `ObjectDataSource1`합니다. 다음으로 만듭니다는 `ItemTemplate` 제품의 이름 및에서 가격을 표시 하는 `<h4>` 요소 및 글꼴 크기에는 아래에 있는 범주와 운송 업체 이름이 있습니다.


[!code-aspx[Main](displaying-data-with-the-objectdatasource-cs/samples/sample6.aspx)]


[![첫 번째 제품 (Chai) 사용자 지정 형식으로 표시 됩니다.](displaying-data-with-the-objectdatasource-cs/_static/image49.png)](displaying-data-with-the-objectdatasource-cs/_static/image48.png)

**그림 18**: 첫 번째 제품 (Chai) 사용자 지정 형식으로 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image50.png))


`<%# Eval(propertyName) %>` 구문이 됩니다. `Eval` 메서드 FormView 컨트롤에 바인딩되는 현재 개체에 대 한 지정된 된 속성의 값을 반환 합니다. 체크 아웃 Alex Homer 문서 [간체 및 ASP.NET 2.0에서 데이터 바인딩 구문을 확장](http://www.15seconds.com/issue/040630.htm) 대 한 자세한 내용은 세부적인 데이터 바인딩의 한계입니다.

FormView는 DetailsView, 같은 ObjectDataSource에서 반환 된 첫 번째 레코드를 표시 됩니다. 한 번에 한 제품을 단계별로 실행 되도록 방문자를 허용 하도록 FormView에서 페이징 사용 가능 합니다.

## <a name="summary"></a>요약

ASP.NET 2.0 ObjectDataSource 컨트롤 덕분에 코드 줄도 작성 하지 않고 비즈니스 논리 계층에서 데이터 액세스 및 표시를 수행할 수 있습니다. ObjectDataSource 클래스의 지정 된 메서드를 호출 하 고 결과 반환 합니다. 이러한 결과 데이터는 ObjectDataSource에 바인딩된 웹 컨트롤에 표시할 수 있습니다. 이 자습서는 ObjectDataSource에 GridView, DetailsView, FormView 컨트롤 바인딩 살펴보았습니다.

지금까지 살펴본 매개 변수가 없는 메서드를 호출 하 여 ObjectDataSource를 사용 하는 방법을 하지만 입력 매개 변수에 같은 예상 하는 메서드를 호출 하려는 경우에 어떻게는 `ProductBLL` 클래스의 `GetProductsByCategoryID(categoryID)`? 하나 이상의 매개 변수를 예상 하는 메서드를 호출 하기 위해에서는 이러한 매개 변수에 대 한 값을 지정 하려면 ObjectDataSource를 구성 해야 합니다. 이 수행 하는 방법을 살펴보려는 우리의 [다음 자습서](declarative-parameters-cs.md)합니다.

만족도 매우 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [고유한 데이터 소스 컨트롤 만들기](https://msdn.microsoft.com/en-us/library/ms364049.aspx)
- [ASP.NET 2.0에 대 한 GridView 예제](https://msdn.microsoft.com/en-us/library/aa479339.aspx)
- [간소화 되 고 데이터 구문을 ASP.NET 2.0에서에서 바인딩 확장](http://www.15seconds.com/issue/040630.htm)
- [ASP.NET 2.0에서 테마](http://www.odetocode.com/Articles/423.aspx)
- [테마를 사용 하 여 서버 쪽 스타일](https://quickstarts.asp.net/quickstartv20/aspnet/doc/themes/stylesheettheme.aspx)
- [방법: ASP.NET 테마를 프로그래밍 방식으로 적용](https://msdn.microsoft.com/en-us/library/tx35bd89.aspx)

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Hilton Giesenow 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[다음](declarative-parameters-cs.md)
