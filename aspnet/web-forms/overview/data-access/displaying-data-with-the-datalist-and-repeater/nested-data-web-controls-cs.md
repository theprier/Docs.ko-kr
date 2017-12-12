---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/nested-data-web-controls-cs
title: "중첩 된 데이터 웹 컨트롤 (C#) | Microsoft Docs"
author: rick-anderson
description: "이 자습서를 살펴볼 것입니다는 반복기를 사용 하는 방법을 다른 반복기 내에 중첩 합니다. 이 예에서는 두 d 내부 반복을 채우는 방법을 설명 합니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/13/2006
ms.topic: article
ms.assetid: ad3cb0ec-26cf-42d7-b81b-184a34ec9f86
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/nested-data-web-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 69fa0489ff8baed1423d29ee7bfaa3157d35a76b
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="nested-data-web-controls-c"></a>중첩 된 데이터 웹 컨트롤 (C#)
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_32_CS.exe) 또는 [PDF 다운로드](nested-data-web-controls-cs/_static/datatutorial32cs1.pdf)

> 이 자습서를 살펴볼 것입니다는 반복기를 사용 하는 방법을 다른 반복기 내에 중첩 합니다. 예제를 선언적으로 또는 프로그래밍 방식으로 내부 반복을 채우는 방법을 설명 합니다.


## <a name="introduction"></a>소개

정적 HTML과 구문이 외에도 웹 컨트롤 및 사용자 정의 컨트롤 템플릿이 포함할 수도 있습니다. 이러한 웹 컨트롤의 속성을 가질 수 있습니다, 선언적 데이터 바인딩 구문을 통해 할당 된 또는 적절 한 서버 쪽 이벤트 처리기에서 프로그래밍 방식으로 액세스할 수 있습니다.

템플릿 내에서 컨트롤을 포함 하 여 모양 및 사용자 환경은 수 하 개선. 예를 들어는 [GridView 컨트롤에 사용 하 여 TemplateFields](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md) 직원의 고용 날짜를 표시 하도록 TemplateField;에 있는 Calendar 컨트롤을 추가 하 여 GridView의 표시를 사용자 지정 하는 방법에 살펴보았습니다 자습서는 [추가 유효성 검사 컨트롤을 편집 및 삽입 인터페이스](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md) 및 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) 자습서에서 살펴본를 편집 하는 사용자 지정 하는 방법 및 삽입 인터페이스 유효성 검사 추가 컨트롤, 텍스트 상자, dropdownlist 활용, 및 기타 웹 컨트롤입니다.

서식 파일에서 다른 데이터 웹 컨트롤을 포함할 수도 있습니다. 즉, 우리 해당 템플릿 내의 다른 DataList (또는 반복기 또는 GridView 또는 DetailsView, 및 등)를 포함 하는 DataList를 가질 수 있습니다. 이러한 인터페이스와 챌린지 내부 데이터 웹 컨트롤에 적절 한 데이터 바인딩된 합니다. 프로그래밍 방식으로 프로토콜로 ObjectDataSource를 사용 하 여 선언적 옵션 까지의 사용 가능한 몇 가지 다른 방법이 있습니다.

이 자습서를 살펴볼 것입니다는 반복기를 사용 하는 방법을 다른 반복기 내에 중첩 합니다. 외부 반복 범주의 이름 및 설명을 표시는 데이터베이스의 각 범주에 대 한 항목이 포함 됩니다. 각 범주 항목 s 내부 반복기에는 해당 범주에 속하는 각 제품에 대 한 정보가 표시 됩니다 (그림 1 참조) 글머리 기호 목록에서 합니다. 예제를 선언적으로 또는 프로그래밍 방식으로 내부 반복을 채우는 방법을 설명 합니다.


[![해당 제품을 함께 각 범주에 나열 된](nested-data-web-controls-cs/_static/image2.png)](nested-data-web-controls-cs/_static/image1.png)

**그림 1**: 각 범주에서 제품을 함께 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](nested-data-web-controls-cs/_static/image3.png))


## <a name="step-1-creating-the-category-listing"></a>1 단계: 범주 목록 만들기

중첩 된 데이터 웹 컨트롤을 사용 하는 페이지를 작성 때 있습니까 디자인에 도움이 될, 작성 및 내부에 중첩된 된 컨트롤에 대 한도 걱정 하지 않고 먼저, 가장 바깥쪽 데이터 웹 컨트롤을 테스트 합니다. 따라서 이름 및 각 범주에 대 한 설명을 나열 하는 페이지에는 반복기를 추가 하는 데 필요한 단계를 검색 하 여 시작 s 사용 수 있습니다.

열어 시작는 `NestedControls.aspx` 페이지에 `DataListRepeaterBasics` 폴더 설정 페이지에 반복기 컨트롤을 추가 하 고 해당 `ID` 속성을 `CategoryList`합니다. 반복기 s 스마트 태그에서 이라는 새 ObjectDataSource를 만들려고 선택한 `CategoriesDataSource`합니다.


[![새 ObjectDataSource CategoriesDataSource 이름](nested-data-web-controls-cs/_static/image5.png)](nested-data-web-controls-cs/_static/image4.png)

**그림 2**: 새 ObjectDataSource 이름을 `CategoriesDataSource` ([전체 크기 이미지를 보려면 클릭](nested-data-web-controls-cs/_static/image6.png))


해당 데이터를 가져오는 되도록 구성 된 ObjectDataSource는 `CategoriesBLL` s 클래스 `GetCategories` 메서드.


[![ObjectDataSource CategoriesBLL 클래스의 GetCategories 메서드를 사용 하도록 구성](nested-data-web-controls-cs/_static/image8.png)](nested-data-web-controls-cs/_static/image7.png)

**그림 3**: 구성에 사용 하 여 ObjectDataSource는 `CategoriesBLL` s 클래스 `GetCategories` 메서드 ([전체 크기 이미지를 보려면 클릭](nested-data-web-controls-cs/_static/image9.png))


반복기 s 서식 파일을 지정 하려면 콘텐츠 해야 소스 보기로 이동 하 고 선언적 구문 직접 입력 합니다. 추가 `ItemTemplate` 에서 s 범주 이름을 표시 하는 `<h4>` 요소와 단락 요소에 있는 범주의 설명을 (`<p>`). Let s 단락 구분선을 사용 하 여 각 범주를 구분 하는 또한 (`<hr>`). 이러한 변경을 수행한 후 페이지 반복기 및 ObjectDataSource 다음과 유사한 선언적 구문 형식으로 포함 되어야 합니다.


[!code-aspx[Main](nested-data-web-controls-cs/samples/sample1.aspx)]

그림 4는 브라우저를 통해 볼 때 진행률을 보여줍니다.


[![각 범주의 이름 및 설명을 나열 되어 구분 하 여 단락 구분선](nested-data-web-controls-cs/_static/image11.png)](nested-data-web-controls-cs/_static/image10.png)

**그림 4**: 각 범주 이름 및 설명을 나열 되어 단락 구분선으로 구분 된 ([전체 크기 이미지를 보려면 클릭](nested-data-web-controls-cs/_static/image12.png))


## <a name="step-2-adding-the-nested-product-repeater"></a>2 단계: 중첩 된 제품 반복 추가

우리의 다음 작업은 완료 나열 범주와에 반복기를 추가 하는 `CategoryList` s `ItemTemplate` 적절 한 범주에 속한 제품에 대 한 정보를 표시 하는 합니다. 다양 한 방법으로이 내부 반복 곧 살펴보겠습니다 2 개에 대 한 데이터를 검색할 수 있습니다. 지금은 let s 만들기만 반복기 제품 내에서 `CategoryList` 반복기의 `ItemTemplate`합니다. 특히 사용 제품이 각 글머리 기호 목록에서 각 제품 목록 항목 가격과 s 제품 이름을 포함 하 여 반복기 표시 되어 s를 수 있습니다.

내부 반복기 s 선언적 구문 및 서식 파일에 수동으로 입력 해야이 반복기를 만들려면는 `CategoryList` s `ItemTemplate`합니다. 내에서 다음 태그를 추가 `CategoryList` 반복기의 `ItemTemplate`:


[!code-aspx[Main](nested-data-web-controls-cs/samples/sample2.aspx)]

## <a name="step-3-binding-the-category-specific-products-to-the-productsbycategorylist-repeater"></a>3 단계: ProductsByCategoryList 반복기에는 범주별 제품 바인딩

이 시점에서 브라우저를 통해 페이지를 방문 하면 화면이 표시 됩니다. 그림 4에서와 동일 하기 때문에 여기서 아직 모든 데이터에 바인딩할 반복기 했습니다. 적절 한 제품 레코드를 클릭 하 고 다른 항목 보다 좀 더 효율적으로 반복기에 바인딩할 수 있습니다는 몇 가지가 있습니다. 여기의 가장 큰 문제 발생 지정한 범주에 대 한 적절 한 제품입니다.

반복기 컨트롤 내부에 바인딩할 데이터 하거나 통해 액세스할 수 있습니다, 선언적에 ObjectDataSource는 `CategoryList` 반복기의 `ItemTemplate`, 또는 ASP.NET 페이지의 코드 숨김 페이지에서 프로그래밍 방식으로 합니다. 마찬가지로,이 데이터에 바인딩될 수 내부 반복 하거나 선언적으로-s 내부 반복을 통해 `DataSourceID` 속성 또는 선언적 데이터 바인딩의 구문을 사용 하거나 프로그래밍 방식으로 내부 반복기에서 참조 하 여는 `CategoryList` 반복기 s `ItemDataBound` 프로그래밍 방식으로 설정 하는 이벤트 처리기의 `DataSource` 속성과 호출 해당 `DataBind()` 메서드. 이러한 방법 중 한 가지 탐색 s를 사용 합니다.

## <a name="accessing-the-data-declaratively-with-an-objectdatasource-control-and-theitemdataboundevent-handler"></a>ObjectDataSource 컨트롤을 사용 하 여 선언적으로 데이터에 액세스 하 고`ItemDataBound`이벤트 처리기

에서는 이후이 자습서 시리즈는 ObjectDataSource를 사용 하는이 예제에 대해 데이터에 액세스 하기 위한 가장 자연 스러운 선택 전체에서 광범위 하 게 ObjectDataSource을 사용한 적입니다. `ProductsBLL` 클래스에는 `GetProductsByCategoryID(categoryID)` 지정 된에 속해 있는 해당 제품에 대 한 정보를 반환 하는 메서드  *`categoryID`* 합니다. 따라서에 ObjectDataSource 추가할 수 있습니다는 `CategoryList` 반복기의 `ItemTemplate` 이 s 클래스 메서드에서 해당 데이터에 액세스 하도록 구성 합니다.

안타깝게도, 반복기 대상이 t 디자인 뷰를 통해 편집이 ObjectDataSource 컨트롤에 대 한 선언적 구문 직접 추가 해야 하므로 해당 서식 파일을 허용 합니다. 에서는 다음 구문은 `CategoryList` 반복기 s `ItemTemplate` 이 새 ObjectDataSource를 추가한 후 (`ProductsByCategoryDataSource`):


[!code-aspx[Main](nested-data-web-controls-cs/samples/sample3.aspx)]

설정 해야 ObjectDataSource 접근 방식을 사용 하는 경우는 `ProductsByCategoryList` 반복기 s `DataSourceID` 속성을는 `ID` 는 ObjectDataSource의 (`ProductsByCategoryDataSource`). 또한 구성 요소 개발자는 우리의 ObjectDataSource에는 `<asp:Parameter>` 지정 하는 요소는  *`categoryID`*  에 전달 되는 값은 `GetProductsByCategoryID(categoryID)` 메서드. 하지만이 값 어떻게 지정 우리? 이상적으로 d 것만 설정할 수는 `DefaultValue` 의 속성은 `<asp:Parameter>` databinding 구문을 사용 하 여 요소 같이:


[!code-aspx[Main](nested-data-web-controls-cs/samples/sample4.aspx)]

안타깝게도, 데이터 바인딩 구문이 올바른지만 있는 컨트롤에는 `DataBinding` 이벤트입니다. `Parameter` 클래스에는 이러한 이벤트에 부족 하며 따라서 위의 구문 수행할 수 없습니다 런타임 오류가 발생 합니다.

이 값을 설정 하려면에 대 한 이벤트 처리기를 만들고 해야는 `CategoryList` 반복기의 `ItemDataBound` 이벤트입니다. 이전에 설명한 대로 `ItemDataBound` 이벤트 반복기에 바인딩된 각 항목에 대해 한 번씩 발생 합니다. 따라서 외부 반복에 대해이 이벤트가 발생 될 때마다 수 지정 현재 `CategoryID` 값을 `ProductsByCategoryDataSource` ObjectDataSource의 `CategoryID` 매개 변수입니다.

에 대 한 이벤트 처리기를 만들고는 `CategoryList` 반복기의 `ItemDataBound` 다음 코드를 사용 하 여 이벤트:


[!code-csharp[Main](nested-data-web-controls-cs/samples/sample5.cs)]

이 이벤트 처리기는 머리글, 바닥글 또는 구분 기호 항목 대신 항목에서는 데이터 처리 다시 확인 하 여 시작 합니다. 다음으로 참조 하는 실제 `CategoriesRow` 현재 방금 바인딩된 인스턴스 `RepeaterItem`합니다. ObjectDataSource에서 참조 하는 마지막으로 `ItemTemplate` 할당 하 고 해당 `CategoryID` 매개 변수 값을는 `CategoryID` 현재 `RepeaterItem`합니다.

이 이벤트 처리기는 `ProductsByCategoryList` 각 반복기 `RepeaterItem` 에서 해당 제품에 바인딩된는 `RepeaterItem`의 범주입니다. 그림 5는 결과 출력의 스크린샷입니다.


[![외부 반복; 각 범주를 나열합니다. 해당 범주에 대 한 제품을 나열 하는 내부](nested-data-web-controls-cs/_static/image14.png)](nested-data-web-controls-cs/_static/image13.png)

**그림 5**: 다음 외부 반복기 나열 각 범주; 내부 하나의 목록을 해당 범주에 대 한 제품 ([전체 크기 이미지를 보려면 클릭](nested-data-web-controls-cs/_static/image15.png))


## <a name="accessing-the-products-by-category-data-programmatically"></a>제품 범주 데이터를 프로그래밍 방식으로 액세스

현재 범주에 대 한 제품을 검색 하는 ObjectDataSource를 사용 하는 대신 ASP.NET 페이지의 코드 숨김 클래스에 메서드를 만들 수 (또는 `App_Code` 폴더 또는 별도 클래스 라이브러리 프로젝트)의 적절 한 집합을 반환 하는 에 전달 될 때 제품은 `CategoryID`합니다. ASP.NET 페이지의 코드 숨김 클래스에서 이러한 메서드를 놓았습니다 한 이름이 였 `GetProductsInCategory(categoryID)`합니다. 위치에서이 방법을 다음과 같은 선언 구문을 사용 하 여 내부 반복기에 현재 범주의 제품을 바인딩한 수 있습니다.:


[!code-aspx[Main](nested-data-web-controls-cs/samples/sample6.aspx)]

반복기 s `DataSource` 속성 구문이 사용 하 여 해당 데이터에서 제공 됨을 나타냅니다는 `GetProductsInCategory(categoryID)` 메서드. 이후 `Eval("CategoryID")` 형식의 값을 반환 `Object`, 개체를 캐스팅 우리는 `Integer` 에 전달 하기 전에 `GetProductsInCategory(categoryID)` 메서드. `CategoryID` 여기에서 데이터 바인딩을 통해 구문은 액세스는 `CategoryID` 에 *외부* 반복기 (`CategoryList`), 한 s의 레코드에 바인딩된는 `Categories` 테이블 합니다. 따라서 알고 있는 `CategoryID` 데이터베이스 일 수 없습니다 `NULL` 값이 때문에 맹목적으로 캐스팅할 수 있습니다는 `Eval` 있는지를 확인 하지 않고 메서드 다루는 다시 우리는 `DBNull`합니다.

이 접근 방식에서는 만들어야 할는 `GetProductsInCategory(categoryID)` 메서드를 적절 한 집합이 제공 된 지정 된 제품 검색  *`categoryID`* 합니다. 단순히 반환 하 여이 작업을 수행할 수 있습니다는 `ProductsDataTable` 에서 반환 되는 `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)` 메서드. 만들 s는 `GetProductsInCategory(categoryID)` 에 대 한 코드 숨김 클래스의 메서드에 우리의 `NestedControls.aspx` 페이지. 다음 코드를 사용 하 여 수행 합니다.


[!code-csharp[Main](nested-data-web-controls-cs/samples/sample7.cs)]

이 메서드는 단순히 인스턴스의 만듭니다는 `ProductsBLL` 메서드의 결과 반환 하 고는 `GetProductsByCategoryID(categoryID)` 메서드. 메서드를 표시 되어 수 `Public` 또는 `Protected`메서드가 표시 하는 경우 `Private`, ASP.NET 페이지 s 선언적 태그에서 액세스할 수 없습니다.

이 새로운 기술을 사용 하려면 이러한 변경 내용을 적용할 후 브라우저를 통해 페이지를 보려면 잠시를 이동 합니다. ObjectDataSource에서 사용 하는 경우 출력을 출력에 동일 해야 하 고 `ItemDataBound` 이벤트 처리기 방법 (그림 5 스크린 샷을 보려면 다시 참조).

> [!NOTE]
> 만들려는 busywork 보일 수는 `GetProductsInCategory(categoryID)` ASP.NET 페이지의 코드 숨김 클래스의 메서드. 즉,이 메서드 인스턴스를 만들기만의 `ProductsBLL` 클래스의 결과 반환 하 고 해당 `GetProductsByCategoryID(categoryID)` 메서드. 왜만이 메서드를 호출 구문이 내부 반복기에서에서 직접 같은: `DataSource='<%# ProductsBLL.GetProductsByCategoryID((int)(Eval("CategoryID"))) %>'`? 이 구문은 성공한 t 작업의 현재 구현 하지만 `ProductsBLL` 클래스 (이후는 `GetProductsByCategoryID(categoryID)` 메서드는 인스턴스 메서드이므로), 수정할 수 있습니다 `ProductsBLL` 정적 포함 하도록 `GetProductsByCategoryID(categoryID)` 메서드 또는 정적 를포함하는클래스`Instance()` 의 새 인스턴스를 반환 하는 메서드는 `ProductsBLL` 클래스입니다.


이러한 수정에 필요 하지는 동안는 `GetProductsInCategory(categoryID)` ASP.NET 페이지의 코드 숨김 클래스의 메서드를 코드 숨김 클래스의 메서드 있도록 보다 다양 하 게 볼 수 있겠지만, 곧 검색 데이터를 사용 합니다.

## <a name="retrieving-all-of-the-product-information-at-once"></a>모든 제품 정보를 한 번에 검색

다음 두 가지 이전 기술에서는 검사 했습니다 호출 하 여 현재 범주에 대 한 해당 제품을 잡고는 `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)` 메서드 (첫 번째 방법인 것 이기 때문 ObjectDataSource를 통해 두 번째는 `GetProductsInCategory(categoryID)` 에서 메서드는 코드 숨김 클래스)입니다. 이 메서드를 호출할 때마다, 데이터 액세스 계층, 비즈니스 논리 계층 호출에서 행을 반환 하는 SQL 문 사용 하 여 데이터베이스 쿼리는 `Products` 갖는 테이블 `CategoryID` 필드에 제공 된 입력된 매개 변수와 일치 합니다.

지정 된 *N* 범주 시스템에이 방법은 네트워크 *N* + 모든 범주를 가져오려는 쿼리 한 데이터베이스에 대 한 1 호출 차례로 *N* 제품을 가져올 호출 각 범주 레이블을 표시 합니다. 그러나 두 데이터베이스 호출 한 번의 호출 범주 및 제품을 모두 가져오려면 다른 모두 가져오려면 모든 필요한 데이터를 검색할 수, 합니다. 이러한 제품 이므로 필터링 할 수 있는 모든 제품, 현재 일치 하는 제품에만 `CategoryID` s 해당 범주에 바인딩된 내부 반복기입니다.

이 기능을 제공 하려면만 하면 약간의 수정 된 `GetProductsInCategory(categoryID)` ASP.NET 페이지의 코드 숨김 클래스의 메서드. 맹목적으로의 결과 반환 하는 대신는 `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)` 메서드를 활용해 서 대신 처음으로 액세스 *모든* 제품 (t를 않은 경우 되었습니다 이미 액세스)의 필터링된 된 보기에만 다음 다시 돌아와 전달 된 기능에 제품 기반 `CategoryID`합니다.


[!code-csharp[Main](nested-data-web-controls-cs/samples/sample8.cs)]

페이지 수준 변수 추가 `allProducts`합니다. 모든 제품에 대 한 정보를 보유 하며, 처음으로 채워진는 `GetProductsInCategory(categoryID)` 메서드가 호출 됩니다. 확인 한 후의 `allProducts` 를 갖는 행만 DataTable의 결과 필터링 하는 메서드, 개체를 만들고 채울 `CategoryID` 지정 된 일치 `CategoryID` 액세스할 수 있습니다. 이 방법은 데이터베이스에서 액세스 하는 횟수를 줄여 *N* 두 아래쪽으로 1을 더한 값입니다.

이 향상 된이 기능 페이지의 렌더링 된 태그에 모든 변경 내용이 발생 하지 않도록 하거나 다른 방식에 비해 다시 더 적은 레코드 가져오기. 단순히 데이터베이스에 대 한 호출 수를 줄입니다.

> [!NOTE]
> 데이터베이스 액세스의 수를 줄이면 성능이 향상 제어 됩니다 직관적으로 이유 수 하나입니다. 그러나이 아닐 경우. 제품의 많은 수 있는 경우 해당 `CategoryID` 은 `NULL`, 예, 다음에 대 한 호출에 대 한는 `GetProducts` 메서드 막대가 표시 되지 제품의 수를 반환 합니다. 또한 모든 제품이 반환 될 수 있습니다 불필요 하는 경우만 페이징을 구현 하는 경우 대/소문자를 될 수 있는 범주의 하위 집합을 표시 된 합니다.


항상 그렇지는 있는 경우 두 가지 방법의 성능 분석, 제어 된 응용 프로그램 s 일반적인 사례 시나리오에 맞게 테스트를 실행 해만 surefire 측정값이입니다.

## <a name="summary"></a>요약

이 자습서에서는 살펴본 하나의 데이터 다른 내에서 웹 컨트롤을 중첩 하는 방법을 구체적으로 외부 반복기 글머리 기호 목록에서 각 범주에 대 한 제품을 나열 하는 내부 반복기와 각 범주에 대 한 항목을 표시 하는 방법을 검사 합니다. 중첩 된 사용자 인터페이스를 빌드하는 가장 큰 문제에 액세스 하 고 내부 데이터 웹 컨트롤에 올바른 데이터를 바인딩 있다는 점입니다. 다양 한 방법 사용할 수 있는,이 자습서에서는 검사 했습니다 중 다음 두 가지가 있습니다. 검사 하는 첫 번째 방법은 웹 컨트롤 s 외부 데이터에는 ObjectDataSource를는 `ItemTemplate` 를 통해 내부 데이터 웹 컨트롤에 바인딩된 해당 `DataSourceID` 속성입니다. ASP.NET 페이지의 코드 숨김 클래스의 메서드를 통해 데이터를 액세스 하는 두 번째 방법입니다. 이 메서드는 내부 데이터의 웹 컨트롤에 바인딩할 수 다음 `DataSource` databinding 구문을 통해 속성입니다.

이 자습서에서 검사 하는 중첩 된 사용자 인터페이스는 반복기 내에 중첩 된 반복으로 사용 되지만 이러한 기술은 다른 데이터 웹 컨트롤을 확장할 수 있습니다. GridView 또는 DataList 내에서 GridView 내에서 반복기를 중첩할 수 있으며 등 수 있습니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Zack Jones 및 Liz Shulok 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](showing-multiple-records-per-row-with-the-datalist-control-cs.md)
[다음](displaying-data-with-the-datalist-and-repeater-controls-vb.md)
