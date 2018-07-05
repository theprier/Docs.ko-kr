---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/nested-data-web-controls-vb
title: 중첩 된 데이터 웹 컨트롤 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 Repeater를 사용 하는 방법을 다른 Repeater 내에 중첩 합니다. 예제에서는 두 d 내부 Repeater를 채우는 방법을 설명 하는 중...
ms.author: aspnetcontent
ms.date: 09/13/2006
ms.assetid: 8b7fcf7b-722b-498d-a4e4-7c93701e0c95
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/nested-data-web-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 45e460edb09fe9398d204e0f280dfb088a44946d
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37803180"
---
<a name="nested-data-web-controls-vb"></a>중첩 된 데이터 웹 컨트롤 (VB)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_32_VB.exe) 또는 [PDF 다운로드](nested-data-web-controls-vb/_static/datatutorial32vb1.pdf)

> 이 자습서에서는 Repeater를 사용 하는 방법을 다른 Repeater 내에 중첩 합니다. 예제에서는 선언적 및 프로그래밍 방식으로 내부 Repeater를 채우는 방법을 설명 합니다.


## <a name="introduction"></a>소개

정적 HTML 및 데이터 바인딩 구문을 외에도 웹 컨트롤 및 사용자 정의 컨트롤 템플릿이 포함할 수도 있습니다. 이러한 웹 컨트롤에는 해당 속성이 있을 수 있습니다 선언적 데이터 바인딩 구문을 통해 할당 되거나 적절 한 서버 쪽 이벤트 처리기에서 프로그래밍 방식으로 액세스할 수 있습니다.

템플릿 내에서 컨트롤을 포함 하 여에 모양과 사용자 환경을 사용자 지정 하 고 개선 될 수 있습니다. 예를 들어, 합니다 [GridView 컨트롤에서 TemplateFields 사용 하 여](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) 자습서를 TemplateField 직원의 고용 날짜를 표시 하려면, 달력 컨트롤을 추가 하 여 GridView가의 표시를 사용자 지정 하는 방법에 살펴보았습니다는 [추가 편집 및 삽입 인터페이스에 유효성 검사 컨트롤](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md) 하 고 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) 자습서에서 살펴본 편집 하는 사용자 지정 하는 방법 및 삽입 인터페이스 유효성 검사를 추가 하 여 컨트롤, 텍스트 상자, Dropdownlist, 및 기타 웹 제어합니다.

템플릿을 다른 데이터 웹 컨트롤을 포함할 수도 있습니다. 즉, 해당 템플릿 내에서 다른 DataList 또는 반복기 또는 GridView 또는 DetailsView와 등을 포함 하는 DataList을 했습니다 수 있습니다. 이러한 인터페이스를 사용 하 여 챌린지를 적절 한 데이터를 내부 데이터 웹 컨트롤에 바인딩된 합니다. ObjectDataSource를 프로그래밍 방식으로 버전을 사용 하 여 선언적 옵션 중에서 사용할 수 있는 몇 가지 방법이 있습니다.

이 자습서에서는 Repeater를 사용 하는 방법을 다른 Repeater 내에 중첩 합니다. 외부 Repeater 범주의 이름 및 설명을 표시 합니다. 데이터베이스에서 각 범주에 대 한 항목이 포함 됩니다. 각 범주 항목 s 내부 반복기에는 해당 범주에 속하는 각 제품에 대 한 정보가 표시 됩니다 (그림 1 참조) 글머리 기호 목록에서입니다. 이 예제에서는 선언적 및 프로그래밍 방식으로 내부 Repeater를 채우는 방법을 설명 합니다.


[![각 범주에 해당 제품을 함께 나와 있습니다.](nested-data-web-controls-vb/_static/image2.png)](nested-data-web-controls-vb/_static/image1.png)

**그림 1**: 각 범주에서 제품을 함께 나열 됩니다 ([큰 이미지를 보려면 클릭](nested-data-web-controls-vb/_static/image3.png))


## <a name="step-1-creating-the-category-listing"></a>1 단계: 범주 목록 만들기

데이터 웹 컨트롤을 중첩 하는 페이지를 만들 경우 디자인에 도움이 될를 만들고 내부 중첩 된 컨트롤에 대 한도 걱정 하지 않고 가장 바깥쪽 데이터 웹 컨트롤을 먼저 테스트 합니다. 따라서 s를 Repeater 이름 및 각 범주에 대 한 설명을 나열 하는 페이지에 추가 하는 데 필요한 단계를 살펴보는 방법으로 시작할 수 있습니다.

열어서 시작 합니다 `NestedControls.aspx` 페이지에서 `DataListRepeaterBasics` 폴더 설정 페이지에 Repeater 컨트롤을 추가 하 고 해당 `ID` 속성을 `CategoryList`합니다. 반복기가 스마트 태그에서 이라는 새 ObjectDataSource를 만들려면 선택 `CategoriesDataSource`합니다.


[![새 ObjectDataSource CategoriesDataSource 이름](nested-data-web-controls-vb/_static/image5.png)](nested-data-web-controls-vb/_static/image4.png)

**그림 2**: 새 ObjectDataSource의 이름을 `CategoriesDataSource` ([클릭 하 여 큰 이미지 보기](nested-data-web-controls-vb/_static/image6.png))


해당 데이터를 가져오는 있도록 ObjectDataSource를 구성 합니다 `CategoriesBLL` s 클래스 `GetCategories` 메서드.


[![S CategoriesBLL 클래스 GetCategories 메서드를 사용 하는 ObjectDataSource 구성](nested-data-web-controls-vb/_static/image8.png)](nested-data-web-controls-vb/_static/image7.png)

**그림 3**: ObjectDataSource를 사용 하 여 구성 합니다 `CategoriesBLL` s 클래스 `GetCategories` 메서드 ([클릭 하 여 큰 이미지 보기](nested-data-web-controls-vb/_static/image9.png))


반복기가의 템플릿을 지정 하려면 콘텐츠 해야 소스 뷰로 이동 하 고 선언적 구문을 직접 입력 합니다. 추가 `ItemTemplate` 에서 s 범주 이름을 표시 하는 `<h4>` 단락 요소에 범주 s 설명과 요소 (`<p>`). Let s 수평선을 사용 하 여 각 범주를 구분 하는 또한 (`<hr>`). 이러한 변경을 수행한 후 페이지 반복기 및 ObjectDataSource 다음과 유사한 선언적 구문을 포함 되어야 합니다.


[!code-aspx[Main](nested-data-web-controls-vb/samples/sample1.aspx)]

그림 4에서는 브라우저를 통해 볼 때 진행 상황을 보여 줍니다.


[![각 이름이 범주와 설명이 나열 되어 단락 구분선 구분](nested-data-web-controls-vb/_static/image11.png)](nested-data-web-controls-vb/_static/image10.png)

**그림 4**: 각 범주 이름 및 설명을 나열 되어 단락 구분선으로 구분 된 ([큰 이미지를 보려면 클릭](nested-data-web-controls-vb/_static/image12.png))


## <a name="step-2-adding-the-nested-product-repeater"></a>2 단계: 추가 제품 중첩 된 반복기

전체 목록 범주를 사용 하 여이 다음 작업은 Repeater를 추가 합니다 `CategoryList` s `ItemTemplate` 적절 한 범주에 속하는 해당 제품에 대 한 정보를 표시 하는 합니다. 다양 한 방법으로 곧 살펴보겠습니다 두, 내부이 반복기에 대 한 데이터를 검색할 수 있습니다. 지금은 let s 만들면 Repeater 제품 내 합니다 `CategoryList` 반복기가의 `ItemTemplate`합니다. 특히 각 글머리 기호 목록의 각 제품 목록 항목 가격와 s 제품 이름을 포함 하 여 반복기 표시 제품이 s 수 있습니다.

내부 Repeater가 선언적 구문 및 서식 파일에 수동으로 입력 해야이 Repeater를 만들려고 합니다 `CategoryList` s `ItemTemplate`입니다. 내에서 다음 태그를 추가 합니다 `CategoryList` Repeater의 `ItemTemplate`:


[!code-aspx[Main](nested-data-web-controls-vb/samples/sample2.aspx)]

## <a name="step-3-binding-the-category-specific-products-to-the-productsbycategorylist-repeater"></a>3 단계: ProductsByCategoryList Repeater 바인딩할 범주별 제품

이 시점에서 브라우저를 통해 페이지를 방문 하면 화면이 표시 됩니다. 그림 4와 동일 하기 때문에 우리가 아직 모든 데이터에 바인딩할 Repeater를 준비 했습니다. 적절 한 제품 레코드를 선택 하 고 다른 항목 보다 효율적으로 일부 반복기에 바인딩할 수 있습니다는 몇 가지가 있습니다. 여기서 가장 큰 문제는 다시 지정한 범주에 대 한 적절 한 제품 연결입니다.

내부 Repeater 컨트롤에 바인딩할 데이터 하거나 통해 액세스할 수 있습니다 선언적으로 ObjectDataSource에는 `CategoryList` Repeater의 `ItemTemplate`, 또는 ASP.NET 페이지의 코드 숨김 페이지에서 프로그래밍 방식으로 합니다. 마찬가지로,이 데이터에 바인딩될 수 내부 Repeater 하거나 선언적으로-s 내부 Repeater를 통해 `DataSourceID` 속성 또는 선언적 데이터 바인딩 구문을 사용 하거나 프로그래밍 방식으로 내부 반복기에서 참조 하 여는 `CategoryList` Repeater s `ItemDataBound` 프로그래밍 방식으로 설정 하 고 이벤트 처리기에서 해당 `DataSource` 속성과 호출 해당 `DataBind()` 메서드. 이러한 각 접근 방식의 탐색 s 수 있습니다.

## <a name="accessing-the-data-declaratively-with-an-objectdatasource-control-and-theitemdataboundevent-handler"></a>ObjectDataSource 컨트롤을 선언적으로 사용 하 여 데이터 액세스 및`ItemDataBound`이벤트 처리기

이후로 ve ObjectDataSource 사용 하는이 예제에 대 한 데이터에 액세스 하기 위한 가장 자연 스러운 선택이 자습서 시리즈에서는 전체에서 광범위 하 게 ObjectDataSource를 사용 합니다. 합니다 `ProductsBLL` 클래스에는 `GetProductsByCategoryID(categoryID)` 속하는 지정 된 제품에 대 한 정보를 반환 하는 메서드 *`categoryID`* 합니다. ObjectDataSource에 추가할 수 있습니다 따라서 합니다 `CategoryList` 반복기가의 `ItemTemplate` 이 s 클래스 메서드에서 해당 데이터에 액세스 하도록 구성 합니다.

아쉽게도 Repeater 만들어지고 t 해당 템플릿에서이 ObjectDataSource 컨트롤에 대 한 선언적 구문을 수동으로 추가 해야 하므로 디자인 뷰를 통해 편집할 수 있습니다. 에서는 다음 구문 합니다 `CategoryList` Repeater s `ItemTemplate` 새 ObjectDataSource를 추가한 후 (`ProductsByCategoryDataSource`):


[!code-aspx[Main](nested-data-web-controls-vb/samples/sample3.aspx)]

ObjectDataSource 접근 방식을 사용 하는 경우 설정 해야 합니다 `ProductsByCategoryList` Repeater s `DataSourceID` 속성을 합니다 `ID` ObjectDataSource의 (`ProductsByCategoryDataSource`). ObjectDataSource에 되었다는 또한는 `<asp:Parameter>` 지정 하는 요소는 *`categoryID`* 에 전달 되는 값을 `GetProductsByCategoryID(categoryID)` 메서드. 그러나이 값이 어떻게 지정에서는? 이상적으로 d 수 설정 하는 것을 `DefaultValue` 의 속성을 `<asp:Parameter>` 데이터 바인딩 구문을 사용 하 여 요소 같이:


[!code-aspx[Main](nested-data-web-controls-vb/samples/sample4.aspx)]

그러나 데이터 바인딩 구문이 유효만 있는 컨트롤에는 `DataBinding` 이벤트입니다. `Parameter` 클래스에 이러한 이벤트를 부족 하 고 따라서 위의 구문 유효 하지 않은 런타임 오류가 발생 합니다.

이 값을 설정 하려면 이벤트 처리기를 생성 해야 합니다 `CategoryList` Repeater의 `ItemDataBound` 이벤트입니다. 이전에 설명한 대로 `ItemDataBound` 이벤트가 Repeater에 바인딩된 각 항목에 대해 한 번 발생 합니다. 따라서 외부 반복기에 대해이 이벤트가 발생 될 때마다 할당할 수 있습니다 현재 `CategoryID` 값을 `ProductsByCategoryDataSource` ObjectDataSource의 `CategoryID` 매개 변수입니다.

에 대 한 이벤트 처리기를 만들고 합니다 `CategoryList` Repeater의 `ItemDataBound` 다음 코드를 사용 하 여 이벤트:


[!code-vb[Main](nested-data-web-controls-vb/samples/sample5.vb)]

이 이벤트 처리기는 머리글, 바닥글 또는 구분 기호 항목 대신 항목에서는 데이터 처리 다시 함으로써 시작 합니다. 다음으로, 참조 하는 실제 `CategoriesRow` 만 현재 바인딩된 인스턴스 `RepeaterItem`합니다. ObjectDataSource를 참조 하는 마지막으로 `ItemTemplate` 할당 및 해당 `CategoryID` 매개 변수 값을 `CategoryID` 현재 `RepeaterItem`.

이 이벤트 처리기를 사용 하 여는 `ProductsByCategoryList` 각 반복기 `RepeaterItem` 에서 해당 제품에 바인딩되는 `RepeaterItem`의 범주입니다. 그림 5에서는 결과 출력의 스크린 샷을 보여 줍니다.


[![외부 Repeater; 각 범주를 나열합니다. 해당 범주에 대 한 제품을 나열 하는 내부](nested-data-web-controls-vb/_static/image14.png)](nested-data-web-controls-vb/_static/image13.png)

**그림 5**: The 외부 Repeater 나열 각 범주; 내부 하나는 해당 범주에 대 한 제품 ([큰 이미지를 보려면 클릭](nested-data-web-controls-vb/_static/image15.png))


## <a name="accessing-the-products-by-category-data-programmatically"></a>제품 범주 데이터를 프로그래밍 방식으로 액세스

ObjectDataSource를 사용 하 여 현재 범주에 대 한 제품을 검색, 대신 ASP.NET의 페이지 코드 숨김 클래스에 메서드를 만들 수 (또는 `App_Code` 폴더 또는 별도 클래스 라이브러리 프로젝트를) 적절 한 집합을 반환 하는 에 전달 될 때 제품을 `CategoryID`입니다. ASP.NET 페이지가 코드 숨김 클래스에서는 이러한 메서드 했다는 및 명명 된 imagine `GetProductsInCategory(categoryID)`합니다. 현재 위치에서이 메서드를 사용 하 여 선언적 구문을 사용 하 여 내부 Repeater에 현재 범주에 대 한 제품을 바인딩할 수 것:


[!code-aspx[Main](nested-data-web-controls-vb/samples/sample6.aspx)]

Repeater s `DataSource` 속성에서 해당 데이터가 제공 됨을 나타내기 위해 데이터 바인딩 구문을 사용 하는 `GetProductsInCategory(categoryID)` 메서드. 하므로 `Eval("CategoryID")` 형식의 값을 반환 `Object`, 개체를 캐스팅 하는 것을 `Integer` 에 전달 하기 전에 `GetProductsInCategory(categoryID)` 메서드. `CategoryID` 여기 데이터 바인딩을 통해 구문은 액세스는 `CategoryID` 에 *외부* 반복기 (`CategoryList`), 것의 레코드에 바인딩할 입니다를 `Categories` 테이블. 있음을 알고 있으므로 `CategoryID` 데이터베이스가 있으면 안 `NULL` 맹목적으로 캐스팅할 수 것 때문 인 값을를 `Eval` 있는지를 확인 하지 않고 메서드 다시 처리 하는 것을 `DBNull`.

이 방법을 사용 하 여 생성 해야 합니다 `GetProductsInCategory(categoryID)` 메서드는 제공 된 지정 된 제품의 적절 한 집합을 검색 하도록 *`categoryID`* 합니다. 단순히 반환 하 여 이렇게 할 합니다 `ProductsDataTable` 반환한 합니다 `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)` 메서드. 만든 수 있도록 합니다 `GetProductsInCategory(categoryID)` 에 대 한 코드 숨김 클래스의 메서드는 `NestedControls.aspx` 페이지. 다음 코드를 사용 하 여 수행 합니다.


[!code-vb[Main](nested-data-web-controls-vb/samples/sample7.vb)]

이 메서드는 단순히 인스턴스에 만듭니다는 `ProductsBLL` 메서드의 결과 반환 하 고는 `GetProductsByCategoryID(categoryID)` 메서드. 메서드를 표시 해야 합니다는 `Public` 나 `Protected`메서드가 표시 하는 경우 `Private`, ASP.NET 페이지 s 선언적 태그에서 액세스할 수 없습니다.

이 새 기술을 사용 하도록 변경 후 잠시 브라우저를 통해 페이지를 봅니다. ObjectDataSource를 사용 하는 경우 출력을 출력에 동일 해야 하 고 `ItemDataBound` 이벤트 처리기 방법 (그림 5 스크린 샷 참조를 다시 참조).

> [!NOTE]
> 만들려는 busywork 등장이 그리 대단해는 `GetProductsInCategory(categoryID)` ASP.NET의 페이지 코드 숨김 클래스의 메서드. 간단히이 메서드의 인스턴스를 만들고, 합니다 `ProductsBLL` 클래스 및 결과 반환 합니다. 해당 `GetProductsByCategoryID(categoryID)` 메서드. 이유만이 메서드를 호출 내부 Repeater, 데이터 바인딩 구문을 통해 같은: `DataSource='<%# ProductsBLL.GetProductsByCategoryID(CType(Eval("CategoryID"), Integer)) %>'`? 이 구문은 현재 구현은 t 작업 성공 하지만 `ProductsBLL` 클래스 (있으므로 `GetProductsByCategoryID(categoryID)` 메서드는 인스턴스 메서드), 수정할 수 있습니다 `ProductsBLL` 정적 포함 하도록 `GetProductsByCategoryID(categoryID)` 메서드 포함 정적클래스가또는`Instance()` 의 새 인스턴스를 반환 하는 방법의 `ProductsBLL` 클래스입니다.


이러한 수정에 필요 하지 않게는 동안는 `GetProductsInCategory(categoryID)` ASP.NET의 페이지 코드 숨김 클래스에서 메서드를 코드 숨김 클래스의 메서드를 제공 보다 유연 하 게 앞으로 살펴보겠지만 곧를 검색 한 데이터로 작업 합니다.

## <a name="retrieving-all-of-the-product-information-at-once"></a>모든 제품 정보를 한 번에 검색

두 경계가 기술을에서는 ve 검사를 호출 하 여 현재 범주에 대 한 제품을 선택 합니다 `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)` 메서드 (첫 번째 방법은 것 이기 때문 ObjectDataSource를 통해 두 번째는 `GetProductsInCategory(categoryID)` 에서 메서드를 코드 숨김 클래스)입니다. 이 메서드를 호출할 때마다, 데이터 액세스 계층을 호출 하 여 비즈니스 논리 계층에서 행을 반환 하는 SQL 문 사용 하 여 데이터베이스 쿼리를 `Products` 테이블로 `CategoryID` 필드에 제공 된 입력된 매개 변수와 일치 합니다.

지정 된 *N* 시스템의 범주가이 방법은이 네트워크 *N* + 1 호출 데이터베이스 하나의 데이터베이스만 쿼리 범주의 모든 차례로 *N* 제품에 대 한 호출 각 범주에만 사용 합니다. 그러나 모든 범주 및 제품의 모든 다른 두 개의 데이터베이스 호출 한 번 호출에 필요한 모든 데이터를 검색할 수 있습니다, 했습니다. 이러한 제품 이므로 필터링 할 수 있으면 모든 제품을 현재 일치 하는 제품에만 `CategoryID` s 해당 범주에 바인딩된 내부 반복기입니다.

이 기능을 제공 하기만 하면 약간의 수정 된 `GetProductsInCategory(categoryID)` ASP.NET의 페이지 코드 숨김 클래스는 메서드. 맹목적으로 결과 반환 하는 대신를 `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)` 메서드를 원하므로 대신 처음으로 액세스 *모든* 제품 (t 되지 않았고 해당 하는 경우 되었습니다 이미 액세스)의 필터링된 된 보기에만 다음 다시 돌아와 전달 기능을 기반으로 제품 `CategoryID`합니다.


[!code-vb[Main](nested-data-web-controls-vb/samples/sample8.vb)]

페이지 수준 변수의 추가 `allProducts`합니다. 이 모든 제품에 대 한 정보를 보유 하 고 처음 채워집니다는 `GetProductsInCategory(categoryID)` 메서드가 실행 됩니다. 확인 한 후 합니다 `allProducts` 메서드를 갖는 행만 있도록 DataTable의 결과 필터링, 개체 생성 되어 채워집니다 `CategoryID` 지정 된 일치 `CategoryID` 액세스할 수 있습니다. 이 방법은 데이터베이스에서 액세스 하는 횟수를 줄입니다 *N* + 2까지 1입니다.

이 향상 된이 기능 변경 내용 페이지의 렌더링 된 태그를 제공 하지 않습니다 또는 다른 접근 방식 보다 다시 적은 수의 레코드 표시 합니다. 단순히 데이터베이스에 대 한 호출의 수를 줄입니다.

> [!NOTE]
> 직관적으로 데이터베이스 액세스의 수를 줄이면 성능이 향상 되는 이유 있습니다 하나입니다. 그러나이 아닐 경우. 제품 수가 많은 경우 해당 `CategoryID` 는 `NULL`, 예제에 대 한 호출에는 `GetProducts` 메서드 표시 되지 않는 제품의 숫자를 반환 합니다. 또한 모든 제품이 반환 낭비 될 수 있습니다 하는 경우 페이징 구현한 경우에 해당 될 수 있는 범주의 하위 집합을 표시만 다시 있습니다.


언제 든 지는 두 가지 기술 중 성능 분석, 응용 프로그램 s 일반적인 사례 시나리오에 맞게 조정 하는 제어 된 테스트를 실행 해만 surefire 측정값이입니다.

## <a name="summary"></a>요약

이 자습서에 대해 살펴보았습니다 웹 컨트롤 내에서 다른 데이터를 중첩 하는 방법을 특히 글머리 기호 목록에서 각 범주에 대 한 제품을 나열 하는 내부 Repeater를 사용 하 여 각 범주에 대 한 항목을 표시 하는 외부 Repeater를 검사 합니다. 중첩 된 사용자 인터페이스를 만드는 가장 큰 문제에 액세스 하 고 내부 데이터 웹 컨트롤에 올바른 데이터 바인딩 있다는 점입니다. 다양 한 기술 사용할 수 있는,이 자습서에서는 검사할 두 가지가 있습니다. 외부 데이터 웹 컨트롤의 ObjectDataSource를 사용 하는 첫 번째 방법은 검사 `ItemTemplate` 을 통해 내부 데이터 웹 컨트롤에 바인딩된는 해당 `DataSourceID` 속성입니다. 두 번째 방법은 ASP.NET 페이지의 코드 숨김 클래스에서 메서드를 통해 데이터에 액세스 합니다. 이 메서드는 내부 데이터 웹 컨트롤 s 바인딩할 수 `DataSource` 데이터 바인딩 구문을 통해 속성입니다.

이 자습서에서 검사 하는 중첩 된 사용자 인터페이스 Repeater 내에 중첩 하는 반복기를 사용 하는 동안 이러한 기술은 다른 데이터 웹 컨트롤을 확장할 수 있습니다. GridView 또는 DataList 내는 GridView 내에서 반복기를 중첩할 수 있으며 등 수 있습니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Zack Jones와 Liz Shulok 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](showing-multiple-records-per-row-with-the-datalist-control-vb.md)
