---
uid: web-forms/overview/data-access/basic-reporting/displaying-data-with-the-objectdatasource-cs
title: ObjectDataSource (C#)를 사용 하 여 데이터를 표시 합니다. | Microsoft Docs
author: rick-anderson
description: 이 자습서는 havi 없이 이전 자습서에서 만든 BLL에서 검색 된 데이터를 바인딩할 수 있습니다이 컨트롤을 사용 하 여 ObjectDataSource 컨트롤 살펴보고...
ms.author: aspnetcontent
ms.date: 03/31/2010
ms.assetid: af882aef-56f5-4e9a-8f95-3977fde20e74
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/displaying-data-with-the-objectdatasource-cs
msc.type: authoredcontent
ms.openlocfilehash: f10745eee9f6ac04e670d710a4ac999c9ddda50b
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37814927"
---
<a name="displaying-data-with-the-objectdatasource-c"></a>ObjectDataSource (C#)를 사용 하 여 데이터를 표시합니다.
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_4_CS.exe) 또는 [PDF 다운로드](displaying-data-with-the-objectdatasource-cs/_static/datatutorial04cs1.pdf)

> 이 자습서의 코드를 작성 하지 않고도 이전 자습서에서 만든 BLL에서 검색 된 데이터를 바인딩할 수 있습니다이 컨트롤을 사용 하 여 ObjectDataSource 컨트롤을 살펴봅니다.


## <a name="introduction"></a>소개

이 응용 프로그램 아키텍처 및 웹 사이트 페이지 레이아웃 전체에서는 다양 한 일반적인 데이터 및 보고 관련 작업을 수행 하는 방법을 탐색 시작할 준비가 된 것입니다. 이전 자습서에서 프로그래밍 방식으로 데이터 웹 컨트롤 ASP.NET 페이지에서 BLL 및 DAL에서 데이터를 바인딩하는 방법을 살펴보았습니다. 데이터 웹 컨트롤의 할당이 구문을 `DataSource` 속성을 표시 한 다음 컨트롤의 데이터로 `DataBind()` 메서드 ASP.NET 1.x 응용 프로그램에서 사용 되는 패턴 되었으며 계속 2.0 응용 프로그램에서 사용할 수 있습니다. 그러나 ASP.NET 2.0의 새로운 데이터 소스 컨트롤 데이터로 작업 하기 위한 선언적 방식을 제공 합니다. 만든 BLL에서 검색 된 데이터를 바인딩할 수 있습니다 이러한 컨트롤을 사용 하 여 [이전 자습서](../introduction/creating-a-business-logic-layer-cs.md) 코드 줄도 작성 하지 않고도!

ASP.NET 2.0에는 5 개의 기본 제공 데이터 소스 컨트롤과 [SqlDataSource](https://msdn.microsoft.com/library/dz12d98w(vs.80).aspx)를 [AccessDataSource](https://msdn.microsoft.com/library/8e5545e1.aspx)를 [ObjectDataSource](https://msdn.microsoft.com/library/9a4kyhcx.aspx), [XmlDataSource](https://msdn.microsoft.com/library/e8d8587a(en-US,VS.80).aspx), 및 [SiteMapDataSource](https://msdn.microsoft.com/library/5ex9t96x(en-US,VS.80).aspx) 자체를 만들 수 있지만 [사용자 지정 데이터 소스 컨트롤](https://msdn.microsoft.com/library/default.asp?url=/library/dnvs05/html/DataSourceCon1.asp), 필요한 경우. 샘플 자습서 응용 프로그램 아키텍처를 개발 했습니다 때문 사용 ObjectDataSource 클래스 BLL에 대 한 합니다.


![ASP.NET 2.0에는 5 개의 기본 제공 데이터 소스 컨트롤이 포함 되어 있습니다.](displaying-data-with-the-objectdatasource-cs/_static/image1.png)

**그림 1**: ASP.NET 2.0에는 5 개의 기본 제공 데이터 소스 컨트롤이 포함 되어 있습니다.


ObjectDataSource는 몇 가지 다른 개체를 사용 하 여 작업에 대 한 프록시로 사용 합니다. ObjectDataSource를 구성 하려면 지정이 기본 개체 및 해당 메서드는 ObjectDataSource에 매핑되는 방식을 `Select`, `Insert`를 `Update`, 및 `Delete` 메서드. 이 기본 개체에 지정 하 고 해당 메서드는 ObjectDataSource에 매핑된 데이터 웹 컨트롤 ObjectDataSource 다음 바인딩할 수 있습니다. ASP.NET 웹 컨트롤을 GridView, 등 DetailsView, RadioButtonList, DropDownList, 특히 많은 데이터를 사용 하 여 제공 됩니다. 페이지 수명 주기 동안 데이터 웹 컨트롤에 해당 ObjectDataSource를 호출 하 여 수행 하는 데이터에 바인딩된 액세스 해야 `Select` 메서드를 데이터 웹 컨트롤에서 삽입, 업데이트를 지 원하는 경우 삭제 될 수 있습니다 호출에 해당 ObjectDataSource의 `Insert`하십시오 `Update`, 또는 `Delete` 메서드. 다음 다이어그램에서 볼 수 있듯이 적절 한 기본 개체의 메서드에 ObjectDataSource에서 이러한 호출은 다음 라우팅됩니다.


[![ObjectDataSource는 프록시로 사용](displaying-data-with-the-objectdatasource-cs/_static/image3.png)](displaying-data-with-the-objectdatasource-cs/_static/image2.png)

**그림 2**: 프록시로 사용 되는 ObjectDataSource ([큰 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image4.png))


삽입에 대 한 메서드를 호출 하는 ObjectDataSource를 사용할 수 있지만, 업데이트 또는 삭제만 집중적으로 살펴보겠습니다 데이터를 반환 합니다. 이후 자습서는 ObjectDataSource와 데이터를 수정 하는 웹 컨트롤 데이터를 사용 하 여 살펴봅니다.

## <a name="step-1-adding-and-configuring-the-objectdatasource-control"></a>1 단계: 추가 및 ObjectDataSource 컨트롤 구성

열어서 시작 합니다 `SimpleDisplay.aspx` 페이지에서 `BasicReporting` 폴더 디자인 뷰로 전환 하 고 다음 ObjectDataSource 컨트롤을 도구 상자 페이지의 디자인 화면으로 끕니다. ObjectDataSource; 태그를 생성 하지 때문에 디자인 화면에서 회색 상자로 표시 단순히 지정된 된 개체에서 메서드를 호출 하 여 데이터에 액세스 합니다. 데이터 웹 컨트롤을 GridView, DetailsView, FormView 등으로 ObjectDataSource에서 반환한 데이터를 표시할 수 있습니다.

> [!NOTE]
> 또는 먼저 페이지로 데이터 웹 컨트롤을 추가 하 한 스마트 태그를 선택 합니다 &lt;새 데이터 원본을&gt; 드롭 다운 목록에서 옵션입니다.


ObjectDataSource의 기본 개체 및 해당 개체의 메서드는 ObjectDataSource에 매핑되는 방식을 지정, ObjectDataSource의 스마트 태그의 데이터 소스 구성 링크를 클릭 합니다.


[![클릭 된 스마트 태그에서 데이터 원본 연결 구성](displaying-data-with-the-objectdatasource-cs/_static/image6.png)](displaying-data-with-the-objectdatasource-cs/_static/image5.png)

**그림 3**: 스마트 태그에서 구성 데이터 원본 링크를 클릭 ([큰 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image7.png))


그러면 데이터 소스 구성 마법사. 먼저 ObjectDataSource를 사용 하려면 개체를 지정 해야 했습니다. 이 화면에 있는 드롭다운 목록에 데코 레이트 하는 개체만 나열 "데이터 구성 요소만 표시" 확인란을 선택 하는 경우는 `DataObject` 특성입니다. 현재 목록 입력 데이터 집합 및 이전 자습서에서 만든 클래스 BLL에는 Tableadapter를 포함 합니다. 추가할 것을 잊어버린 경우는 `DataObject` 특성 비즈니스 논리 계층 클래스에 표시 되지 않습니다 하이 목록에 있습니다. 이 경우 (형식화 된 DataSet의 Datatable에서 Datarow를에서 다른 클래스)와 함께 클래스 BLL을 포함 해야 하는 모든 개체를 보려면 "데이터 구성 요소만 표시" 확인란을 선택 취소 합니다.

이 첫 번째 화면에서 선택 된 `ProductsBLL` 드롭 다운 목록에서 클래스 및 다음을 클릭 합니다.


[![ObjectDataSource 컨트롤을 사용 하 여 사용 하 여 개체를 지정 합니다.](displaying-data-with-the-objectdatasource-cs/_static/image9.png)](displaying-data-with-the-objectdatasource-cs/_static/image8.png)

**그림 4**: ObjectDataSource 컨트롤을 사용 하 여 사용 하 여 개체를 지정 ([큰 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image10.png))


마법사의 다음 화면 ObjectDataSource를 호출 해야 하는 방법을 선택 하 라는 메시지를 표시 합니다. 드롭다운 목록에는 이전 화면에서 선택한 개체의 데이터를 반환 하는 이러한 방법을 나열 합니다. 여기 우리 `GetProductByProductID`, `GetProducts`를 `GetProductsByCategoryID`, 및 `GetProductsBySupplierID`합니다. 선택 합니다 `GetProducts` 클릭 하 고 드롭다운 목록에서 메서드를 완료 (추가한 경우는 `DataObjectMethodAttribute` 에 `ProductBLL`의 메서드는 이전 자습서에서는이 옵션에에서 나와 있는 것 처럼 기본적으로 선택 됩니다).


[![선택 탭에서 데이터를 반환 하는 것에 대 한 메서드를 선택 합니다.](displaying-data-with-the-objectdatasource-cs/_static/image12.png)](displaying-data-with-the-objectdatasource-cs/_static/image11.png)

**그림 5**: 선택 탭에서 데이터 반환에 대 한 메서드를 선택 ([큰 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image13.png))


## <a name="configure-the-objectdatasource-manually"></a>ObjectDataSource를 수동으로 구성

ObjectDataSource의 데이터 소스 구성 마법사는 사용 하 여 개체를 지정 하 고 연결 개체의 어떤 메서드가 호출 되는 신속 하 게를 제공 합니다. 그러나 ObjectDataSource의 선언 태그에 직접 또는 속성 창을 통해 해당 속성을 통해 구성할 수 있습니다. 설정 하기만 합니다 `TypeName` 속성을 사용할 기본 개체의 형식 및 `SelectMethod` 데이터를 검색할 때 호출할 메서드를 합니다.


[!code-aspx[Main](displaying-data-with-the-objectdatasource-cs/samples/sample1.aspx)]

있을 데이터 소스 구성 마법사를 선호 하는 경우에 수동으로 해야 할 때 시간 마법사 개발자가 만든 클래스에만 나열 하는 대로 ObjectDataSource가를 구성 합니다. 바인딩하려는 ObjectDataSource.NET Framework의 클래스와 같은 경우는 [멤버 자격 클래스](https://msdn.microsoft.com/library/system.web.security.membership.aspx), 사용자 계정 정보에 액세스할 수 또는 [Directory 클래스](https://msdn.microsoft.com/library/system.io.directory.aspx) 파일 시스템 정보를 사용 하려면 ObjectDataSource의 속성을 수동으로 설정 해야 합니다.

## <a name="step-2-adding-a-data-web-control-and-binding-it-to-the-objectdatasource"></a>2 단계: 데이터 웹 컨트롤 추가 및 ObjectDataSource에 바인딩

ObjectDataSource를 페이지에 추가 하 고 구성 된 된 준비가 ObjectDataSource의에서 반환한 데이터를 표시 하려면 페이지 데이터 웹 컨트롤을 추가할 `Select` 메서드. ObjectDataSource;에 모든 데이터 웹 컨트롤을 바인딩할 수 있습니다. GridView와 DetailsView FormView에 ObjectDataSource의 데이터 표시에 대해 살펴보겠습니다.

## <a name="binding-a-gridview-to-the-objectdatasource"></a>GridView ObjectDataSource에 바인딩

GridView 컨트롤을 도구 상자에서 추가 `SimpleDisplay.aspx`의 디자인 화면입니다. GridView의 스마트 태그에서 1 단계에서에서 추가한 ObjectDataSource 컨트롤을 선택 합니다. 이 자동으로 만듭니다는 BoundField ObjectDataSource의에서 데이터에 의해 반환 된 각 속성에 대 한 GridView `Select` 메서드 (즉, 제품 DataTable에서 정의 된 속성).


[![GridView를 페이지에 추가한 ObjectDataSource에 바인딩된 및](displaying-data-with-the-objectdatasource-cs/_static/image15.png)](displaying-data-with-the-objectdatasource-cs/_static/image14.png)

**그림 6**:는 GridView에 추가한 페이지 및 ObjectDataSource에 바인딩된 ([큰 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image16.png))


그런 다음 사용자 지정, 다시 정렬 하거나 제거할 수 있습니다 GridView의 BoundFields 스마트 태그에서 열 편집 옵션을 클릭 하 여 합니다.


[![GridView의 BoundFields 편집 열 대화 상자를 통해 관리](displaying-data-with-the-objectdatasource-cs/_static/image18.png)](displaying-data-with-the-objectdatasource-cs/_static/image17.png)

**그림 7**: 관리 GridView의 BoundFields 통해 the 편집 열 대화 상자 ([큰 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image19.png))


잠시 GridView의 BoundFields, 제거, 수정 하는 `ProductID`, `SupplierID`, `CategoryID`, `QuantityPerUnit`, `UnitsInStock`를 `UnitsOnOrder`, 및 `ReorderLevel` BoundFields 합니다. BoundField 왼쪽 아래 목록에서 선택 하 고 (빨간색 X) 제거 하려면 삭제 단추를 클릭 하기만 하면 됩니다. 다음으로 BoundFields 다시 정렬 있도록를 `CategoryName` 및 `SupplierName` BoundFields 앞에 야 합니다 `UnitPrice` BoundField 이러한 BoundFields를 선택 하 고 위쪽 화살표를 클릭 합니다. 설정 된 `HeaderText` 를 나머지 BoundFields의 속성 `Products`, `Category`, `Supplier`, 및 `Price`각각. 다음에 `Price` BoundField 서식이 지정 된 통화 BoundField의 설정 `HtmlEncode` 속성을 False 및 해당 `DataFormatString` 속성을 `{0:c}`입니다. 마지막으로, 가로로 정렬를 `Price` 오른쪽에 및 `Discontinued` 를 통해 중앙에서 확인란을 선택 합니다 `ItemStyle` / `HorizontalAlign` 속성.


[!code-aspx[Main](displaying-data-with-the-objectdatasource-cs/samples/sample2.aspx)]


[![사용자 지정 된 GridView의 BoundFields](displaying-data-with-the-objectdatasource-cs/_static/image21.png)](displaying-data-with-the-objectdatasource-cs/_static/image20.png)

**그림 8**: GridView의 BoundFields 사용자 지정 된 ([큰 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image22.png))


## <a name="using-themes-for-a-consistent-look"></a>일관적인 모양에 대 한 테마를 사용 하 여

이러한 자습서 제어 수준 스타일 설정을 제거 하기 위해 노력, 가능 하면 외부 파일에 정의 된 스타일 시트를 사용 하는 대신 합니다. 합니다 `Styles.css` 파일 포함 `DataWebControlStyle`, `HeaderStyle`, `RowStyle`, 및 `AlternatingRowStyle` 웹이 자습서에 사용 되는 컨트롤의 데이터 모양 지정에 사용 해야 하는 CSS 클래스입니다. 이렇게 하려면 GridView의 설정 수 `CssClass` 속성을 `DataWebControlStyle`, 및 해당 `HeaderStyle`를 `RowStyle`, 및 `AlternatingRowStyle` 속성 `CssClass` 속성 적절 하 게 합니다.

이러한로 설정 하면 `CssClass` 속성을 명시적으로 각각의 모든 데이터에 대 한 이러한 속성 값을 설정 해야 하는 웹 컨트롤에서 웹 컨트롤이 자습서에 추가 합니다. DetailsView GridView에 대 한 기본 CSS 관련 속성을 정의 하는 쉬운 방법입니다 및 FormView 테마를 사용 하 여 제어 합니다. 테마는 컨트롤 수준 속성 설정, 이미지 및 일반적인 모양 및 느낌을 적용 하는 사이트에서 페이지에 적용할 수 있는 CSS 클래스의 컬렉션입니다.

이 테마는 모든 이미지 또는 CSS 파일에 포함 되지 않습니다 (스타일 시트를 보면 `Styles.css` 으로-웹 응용 프로그램의 루트 폴더에 정의 된,), 두 스킨을 포함 합니다. 스킨 파일이 웹 컨트롤에 대 한 기본 속성을 정의 합니다. 특히 마련 스킨 파일 GridView 및 DetailsView 컨트롤에 대 한 기본값을 나타내는 `CssClass`-관련 속성입니다.

이라는 프로젝트에 새 스킨 파일을 추가 하 여 시작 `GridView.skin` 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가 선택 하 여 합니다.


[![GridView.skin 명명 된 스킨 파일 추가](displaying-data-with-the-objectdatasource-cs/_static/image24.png)](displaying-data-with-the-objectdatasource-cs/_static/image23.png)

**그림 9**: 라는 스킨 파일을 추가 `GridView.skin` ([클릭 하 여 큰 이미지 보기](displaying-data-with-the-objectdatasource-cs/_static/image25.png))


스킨 파일에는 테마를에 배치할 필요는 `App_Themes` 폴더입니다. 이러한 폴더를 아직 없기 때문 Visual Studio는이 첫 번째 스킨을 추가 하는 경우에 만드는 내용이 제공 됩니다. 만들려면 예 클릭 합니다 `App_Theme` 폴더 새 배치 `GridView.skin` 파일입니다.


[![Visual studio에서 App_Theme 폴더 만들기](displaying-data-with-the-objectdatasource-cs/_static/image27.png)](displaying-data-with-the-objectdatasource-cs/_static/image26.png)

**그림 10**: Visual Studio 만들 수 있도록 합니다 `App_Theme` 폴더 ([클릭 하 여 큰 이미지 보기](displaying-data-with-the-objectdatasource-cs/_static/image28.png))


새 테마 만들기는이 `App_Themes` GridView 스킨 파일 이라는 폴더 `GridView.skin`합니다.


![GridView 테마에 추가한 App_Theme 폴더](displaying-data-with-the-objectdatasource-cs/_static/image29.png)

**그림 11**: The GridView 테마에 추가한에 `App_Theme` 폴더


DataWebControls GridView 테마의 이름을 (GridView 폴더를 마우스 오른쪽 단추로 클릭는 `App_Theme` 폴더 이름 바꾸기 선택). 그런 다음에 다음 태그를 입력 합니다 `GridView.skin` 파일:


[!code-aspx[Main](displaying-data-with-the-objectdatasource-cs/samples/sample3.aspx)]

에 대 한 기본 속성 정의 `CssClass`-DataWebControls 테마를 사용 하는 모든 페이지에 모든 GridView에 대 한 관련 속성입니다. DetailsView를 데이터 웹 컨트롤을 곧 사용할 것에 대 한 다른 스킨을 추가 해 보겠습니다. 새 스킨 라는 DataWebControls 테마를 추가할 `DetailsView.skin` 다음 태그를 추가 합니다.


[!code-aspx[Main](displaying-data-with-the-objectdatasource-cs/samples/sample4.aspx)]

정의 테마를 사용 하 여 마지막 단계는 ASP.NET 페이지에 테마를 적용할 것입니다. 페이지 별로 또는 웹 사이트의 모든 페이지에 대 한 테마를 적용할 수 있습니다. 웹 사이트의 모든 페이지에 대해이 테마를 사용해 보겠습니다. 이렇게 하려면 다음 태그를 추가 `Web.config`의 `<system.web>` 섹션:


[!code-xml[Main](displaying-data-with-the-objectdatasource-cs/samples/sample5.xml)]

이것이 전부입니다! 합니다 `styleSheetTheme` 테마에서 지정한 속성이 해야 하는 설정을 나타냅니다 *하지* 제어 수준에 지정 된 속성을 재정의 합니다. 테마 설정을 제어 설정 이지만 해야를 지정 하려면 사용 합니다 `theme` 대신 특성 `styleSheetTheme`; 아쉽게도 테마 설정을 통해 지정 된는 `theme` 특성 Visual Studio 디자인 뷰에서 표시 되지 않습니다. 가리킵니다 [ASP.NET 테마 및 스킨 개요](https://msdn.microsoft.com/library/ykzx33wh.aspx) 및 [서버측 스타일을 사용 하 여 테마](https://quickstarts.asp.net/quickstartv20/aspnet/doc/themes/stylesheettheme.aspx) 테마와 스킨;에 대 한 자세한 내용은 참조 [방법: ASP.NET 테마 적용](https://msdn.microsoft.com/library/0yy5hxdk(VS.80).aspx) 대 한 자세한 내용은 테마를 사용 하도록 페이지를 구성 합니다.


[![제품의 이름, 범주, 공급자, 가격 및 지원 되지 않는 정보를 표시 하는 GridView](displaying-data-with-the-objectdatasource-cs/_static/image31.png)](displaying-data-with-the-objectdatasource-cs/_static/image30.png)

**그림 12**: GridView 제품의 이름, 범주, 공급자, 가격 및 지원 되지 않는 정보를 표시 합니다 ([큰 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image32.png))


## <a name="displaying-one-record-at-a-time-in-the-detailsview"></a>DetailsView에서 한 번에 하나의 레코드를 표시합니다.

GridView가 바인딩되는 데이터 소스 컨트롤에 의해 반환 된 각 레코드에 대 한 하나의 행을 표시 합니다. 그러나 한 번에 유일한 레코드 또는 레코드 하나만 표시 해야 할 때가 있습니다. 합니다 [DetailsView 컨트롤](https://msdn.microsoft.com/library/s3w1w7t4.aspx) HTML로 렌더링 하는이 기능을 제공 `<table>` 두 개 열과 각 열 또는 컨트롤에 바인딩된 속성에 대해 한 행입니다. 단일 레코드 90도 회전된을 사용 하 여 GridView와 DetailsView를 생각할 수 있습니다.

DetailsView 컨트롤을 추가 하 여 시작 *위에* 에서 GridView `SimpleDisplay.aspx`합니다. 그런 다음 GridView와 같은 ObjectDataSource 컨트롤에 바인딩하십시오. GridView를 사용 하 여는 BoundField 추가할 ObjectDataSource의으로 반환 되는 개체의 각 속성에 대 한 DetailsView와 같은 `Select` 메서드. 유일한 차이점은 세로가 아닌 가로로 DetailsView의 BoundFields 배치 됩니다.


[![페이지에는 DetailsView를 추가 하 고 ObjectDataSource에 바인딩](displaying-data-with-the-objectdatasource-cs/_static/image34.png)](displaying-data-with-the-objectdatasource-cs/_static/image33.png)

**그림 13**: 페이지에는 DetailsView를 추가 하 고 ObjectDataSource에 바인딩합니다 ([큰 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image35.png))


GridView와 같은 DetailsView의 BoundFields ObjectDataSource에서 반환한 데이터의 추가 사용자 지정 된 표시를 작성할 수 있습니다. 그림 14에서는 해당 BoundFields 후 DetailsView를 보여 줍니다. 및 `CssClass` 속성이 모양을 GridView 예제와 비슷한 되도록 구성 되어 있어야 합니다.


[![DetailsView 단일 레코드를 보여 줍니다.](displaying-data-with-the-objectdatasource-cs/_static/image37.png)](displaying-data-with-the-objectdatasource-cs/_static/image36.png)

**그림 14**: DetailsView 단일 레코드를 보여 줍니다 ([큰 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image38.png))


참고 DetailsView에만 해당 데이터 원본에서 반환 된 첫 번째 레코드를 표시 합니다. 모든 레코드를 한 번에 하나씩 단계별로 실행 하는 데 사용할 수 하 게 DetailsView에 대 한 페이징을 사용 해야 합니다. 이렇게 하려면 Visual Studio로 돌아가서 및 DetailsView의 스마트 태그의 페이징 사용 확인란을 확인 합니다.


[![DetailsView 컨트롤에서 페이징 사용](displaying-data-with-the-objectdatasource-cs/_static/image40.png)](displaying-data-with-the-objectdatasource-cs/_static/image39.png)

**그림 15**: DetailsView 컨트롤에서 페이징 사용 ([큰 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image41.png))


[![페이징을 사용, DetailsView를 사용 하면 제품을 보려면](displaying-data-with-the-objectdatasource-cs/_static/image43.png)](displaying-data-with-the-objectdatasource-cs/_static/image42.png)

**그림 16**: DetailsView 페이징 사용을 사용 하 여 제품 중 하나를 보려는 사용자를 수 있습니다 ([큰 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image44.png))


페이징 나중에 자습서에 자세히 알아보겠습니다.

## <a name="a-more-flexible-layout-for-showing-one-record-at-a-time"></a>한 번에 하나의 레코드를 표시 하는 데 더 유연한 레이아웃

DetailsView는 ObjectDataSource에서 반환 된 각 레코드를 표시 하는 방법을에서 매우 엄격 합니다. 데이터의 유연한 보기를 바랍니다 수 있습니다. 예를 들어, 별도 행에는 제품 이름, 범주, 공급자, 가격 및 각 지원 되지 않는 정보를 표시 하는 대신 것이 좋겠습니다 제품 이름을 표시 하 고 가격을 `<h4>` category와 supplier 정보가 표시 된 제목 이름 및 글꼴 크기의 가격 아래. 및에서는 값 옆에 있는 속성 이름 (제품, 범주 및 등)를 표시 하려면 중요 하지 않을 수 있습니다.

합니다 [FormView 컨트롤이](https://msdn.microsoft.com/library/fyf1dk77.aspx) 이 수준의 사용자 지정을 제공 합니다. FormView 필드 (예: GridView 및 DetailsView 수행)를 사용 하는 대신 다양 한 정적 HTML 웹 컨트롤에 대 한 허용 되는 템플릿을 사용 하 고 [데이터 바인딩 구문을](http://www.15seconds.com/issue/040630.htm)합니다. ASP.NET에서 Repeater 컨트롤에 익숙한 경우 1.x를 생각할 수 있습니다 FormView 단일 레코드를 표시 하는 것에 대 한 반복기로 합니다.

FormView 컨트롤을 추가 합니다 `SimpleDisplay.aspx` 페이지의 디자인 화면입니다. 처음에 FormView 표시 된 회색 블록으로 우리 최소한 컨트롤을 제공 해야 함을 `ItemTemplate`입니다.


[![FormView 해야 ItemTemplate 포함](displaying-data-with-the-objectdatasource-cs/_static/image46.png)](displaying-data-with-the-objectdatasource-cs/_static/image45.png)

**그림 17**: The FormView 포함 해야 합니다는 `ItemTemplate` ([클릭 하 여 큰 이미지 보기](displaying-data-with-the-objectdatasource-cs/_static/image47.png))


FormView 기본값 만드는 FormView의 스마트 태그를 통해 데이터 소스 컨트롤에 직접 바인딩할 수 있습니다 `ItemTemplate` 자동으로 (함께 `EditItemTemplate` 하 고 `InsertItemTemplate`이면 ObjectDatatSource 컨트롤의 `InsertMethod` 및 `UpdateMethod` 속성이 설정 됩니다). 그러나이 예를 보겠습니다 데이터 FormView 바인딩하고 지정 해당 `ItemTemplate` 수동으로. FormView의을 설정 하 여 시작 `DataSourceID` 속성을 `ID` ObjectDataSource 컨트롤의 `ObjectDataSource1`합니다. 다음으로 만듭니다는 `ItemTemplate` 제품의 이름과 가격을 표시 하는 `<h4>` 요소 및 글꼴 크기는 아래에 있는 범주 및 운송 회사 이름입니다.


[!code-aspx[Main](displaying-data-with-the-objectdatasource-cs/samples/sample6.aspx)]


[![첫 번째 제품 (Chai) 사용자 지정 형식으로 표시 됩니다.](displaying-data-with-the-objectdatasource-cs/_static/image49.png)](displaying-data-with-the-objectdatasource-cs/_static/image48.png)

**그림 18**: 사용자 지정 형식에는 첫 번째 제품 (Chai) 표시 됩니다 ([큰 이미지를 보려면 클릭](displaying-data-with-the-objectdatasource-cs/_static/image50.png))


`<%# Eval(propertyName) %>` 데이터 바인딩 구문입니다. `Eval` 메서드 FormView 컨트롤에 바인딩되는 현재 개체의 지정된 된 속성의 값을 반환 합니다. Alex Homer 기사 [간체 및 ASP.NET 2.0의 데이터 바인딩 구문을 확장](http://www.15seconds.com/issue/040630.htm) databinding의 장단점에 대 한 자세한 내용은 합니다.

DetailsView를 같은 FormView만 ObjectDataSource에서 반환 된 첫 번째 레코드를 표시 합니다. 한 번에 한 제품을 단계별로 방문자를 허용 하도록 FormView에서 페이징을 사용할 수 있습니다.

## <a name="summary"></a>요약

액세스 및 비즈니스 논리 계층에서 데이터를 표시 합니다. ASP.NET 2.0 ObjectDataSource 컨트롤 덕분에 코드 줄도 작성 하지 않고 수행할 수 있습니다. ObjectDataSource는 클래스의 지정 된 메서드를 호출 하 고 결과 반환 합니다. ObjectDataSource에 바인딩되는 웹 컨트롤에 데이터에서 이러한 결과 표시할 수 있습니다. 이 자습서에서는 ObjectDataSource에 GridView, DetailsView 및 FormView 컨트롤 바인딩 살펴보았습니다.

지금까지 것만 ObjectDataSource를 사용 하 여 매개 변수가 없는 메서드를 호출 하는 방법을 살펴보았으며 예상 하는 메서드를 호출 하려고 하는 경우와 같은 매개 변수를 입력 합니다 `ProductBLL` 클래스의 `GetProductsByCategoryID(categoryID)`? 하나 이상의 매개 변수를 예상 하는 메서드를 호출 하기 위해 이러한 매개 변수에 대 한 값을 지정 하는 ObjectDataSource 구성 해야 합니다. 이 수행 하는 방법을 살펴보겠습니다 우리의 [다음 자습서](declarative-parameters-cs.md)합니다.

즐거운 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [사용자 고유의 데이터 소스 컨트롤 만들기](https://msdn.microsoft.com/library/ms364049.aspx)
- [ASP.NET 2.0의 GridView 예](https://msdn.microsoft.com/library/aa479339.aspx)
- [간소화 하 고 ASP.NET 2.0의에서 바인딩 구문 데이터 확장](http://www.15seconds.com/issue/040630.htm)
- [ASP.NET 2.0의 테마](http://www.odetocode.com/Articles/423.aspx)
- [테마를 사용 하 여 서버 쪽 스타일](https://quickstarts.asp.net/quickstartv20/aspnet/doc/themes/stylesheettheme.aspx)
- [방법: ASP.NET 테마를 프로그래밍 방식으로 적용](https://msdn.microsoft.com/library/tx35bd89.aspx)

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Hilton giesenow와 함께 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [다음](declarative-parameters-cs.md)
