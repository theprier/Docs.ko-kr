---
uid: web-forms/overview/data-access/custom-button-actions-with-the-datalist-and-repeater/custom-buttons-in-the-datalist-and-repeater-cs
title: 사용자 지정 단추 DataList 및 반복기 (C#) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 해당 associ에 표시할 단추를 제공 하는 각 범주를 사용 하 여 시스템에서 범주를 나열 하는 반복기를 사용 하는 인터페이스를 빌드 해 보겠습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/13/2006
ms.topic: article
ms.assetid: 1f42e332-78dc-438b-9e35-0c97aa0ad929
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions-with-the-datalist-and-repeater/custom-buttons-in-the-datalist-and-repeater-cs
msc.type: authoredcontent
ms.openlocfilehash: 802f52e8e4e1ca1addec3321503ac92474ffd6b8
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37369488"
---
<a name="custom-buttons-in-the-datalist-and-repeater-c"></a>DataList 및 반복기 (C#)의 사용자 지정 단추
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_46_CS.exe) 또는 [PDF 다운로드](custom-buttons-in-the-datalist-and-repeater-cs/_static/datatutorial46cs1.pdf)

> 이 자습서에서는 BulletedList 컨트롤을 사용 하 여 연결 된 제품에 표시할 단추를 제공 하는 각 범주를 사용 하 여 시스템에서 범주를 나열 하는 반복기를 사용 하는 인터페이스를 빌드 해 보겠습니다.


## <a name="introduction"></a>소개

지난 17 DataList 및 반복기 자습서 전체에서에서는 ve 모두 읽기 전용 예제 및 편집 및 삭제 예제를 생성 합니다. 편집 및 삭제 DataList 내에서 기능을 위해 단추에 추가한 s DataList `ItemTemplate` 를 클릭 하면 포스트백을 발생 하 고 s 단추에 해당 하는 DataList 이벤트를 발생 시킨 `CommandName` 속성입니다. 예를 들어, 단추를 추가 합니다 `ItemTemplate` 사용 하 여를 `CommandName` 속성은 편집 하면 DataList s `EditCommand` 포스트백에서 발생 개를 `CommandName` 발생 삭제는 `DeleteCommand`.

또한를 편집 하 고 삭제 단추 DataList 및 반복기 컨트롤을 포함할 수도 Linkbutton을 단추나 ImageButtons,를 클릭 하면 일부 사용자 지정 서버 쪽 논리를 수행 합니다. 이 자습서에서는 시스템의 범주를 나열 하는 반복기를 사용 하는 인터페이스를 빌드 해 보겠습니다. 각 범주에 대 한 반복기 BulletedList 컨트롤을 사용 하 여 연결 된 제품 범주를 표시 하도록 단추가 포함 됩니다 (그림 1 참조).


[![글머리 기호 목록에서 범주의 제품 표시 제품 링크 표시를 클릭합니다.](custom-buttons-in-the-datalist-and-repeater-cs/_static/image2.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image1.png)

**그림 1**: 글머리 기호 목록의 s 제품 범주 제품 표시 링크 표시를 클릭 ([큰 이미지를 보려면 클릭](custom-buttons-in-the-datalist-and-repeater-cs/_static/image3.png))


## <a name="step-1-adding-the-custom-button-tutorial-web-pages"></a>1 단계: 사용자 지정 단추 자습서 웹 페이지 추가

사용자 지정 단추를 추가 하는 방법을 살펴보기 전에 s를 먼저 시간을 내어이 자습서용 해야 하는 웹 사이트 프로젝트에서 ASP.NET 페이지를 만들 수 있습니다. 라는 새 폴더를 추가 하 여 시작 `CustomButtonsDataListRepeater`합니다. 다음에 있는 각 페이지에 연결할 수 있도록 해당 폴더에 다음 두 ASP.NET 페이지를 추가 합니다 `Site.master` 마스터 페이지:

- `Default.aspx`
- `CustomButtons.aspx`


![사용자 지정 단추 관련 자습서에 대 한 ASP.NET 페이지 추가](custom-buttons-in-the-datalist-and-repeater-cs/_static/image4.png)

**그림 2**: 사용자 지정 단추 관련 자습서에 대 한 ASP.NET 페이지 추가


다른 폴더와 같이 `Default.aspx` 에 `CustomButtonsDataListRepeater` 폴더 섹션의 자습서를 나열 됩니다. 이전에 설명한 대로 `SectionLevelTutorialListing.ascx` 사용자 컨트롤은이 기능을 제공 합니다. 이 사용자 정의 컨트롤을 추가 `Default.aspx`의 디자인 뷰에서 페이지의 솔루션 탐색기에서 끌어 합니다.


[![Default.aspx SectionLevelTutorialListing.ascx 사용자 컨트롤 추가](custom-buttons-in-the-datalist-and-repeater-cs/_static/image6.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image5.png)

**그림 3**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 `Default.aspx` ([클릭 하 여 큰 이미지 보기](custom-buttons-in-the-datalist-and-repeater-cs/_static/image7.png))


마지막으로, 페이지에 항목으로 추가 된 `Web.sitemap` 파일입니다. 특히, DataList 및 반복기를 사용 하 여 페이징 및 정렬 한 후 다음 태그를 추가 `<siteMapNode>`:


[!code-xml[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample1.xml)]

업데이트 한 후 `Web.sitemap`, 잠시 브라우저를 통해 자습서 웹 사이트를 확인 합니다. 왼쪽 메뉴에는 이제 편집, 삽입 및 삭제 자습서에 대 한 항목이 포함 됩니다.


![이제 사이트 맵 사용자 지정 단추 자습서에 대 한 항목을 포함](custom-buttons-in-the-datalist-and-repeater-cs/_static/image8.png)

**그림 4**: 이제 사이트 맵 사용자 지정 단추 자습서에 대 한 항목을 포함


## <a name="step-2-adding-the-list-of-categories"></a>2 단계: 추가 범주 목록

이 자습서에 대 한 제품 LinkButton 표시와 함께 모든 범주를 나열 하는 반복기를 생성 해야 하는, 클릭 하면 관련된 범주가의 제품 글머리 기호 목록에 표시 됩니다. S를 시스템의 범주를 나열 하는 간단한 Repeater를 처음 만들 수 있습니다. 열어서 시작 합니다 `CustomButtons.aspx` 페이지에 `CustomButtonsDataListRepeater` 폴더입니다. Repeater 집합과 디자이너 도구 상자에서 끌어 해당 `ID` 속성을 `Categories`입니다. 다음으로 반복기가 스마트 태그에서 새 데이터 소스 컨트롤을 만듭니다. 특히 이라는 새 ObjectDataSource 컨트롤을 만들어 `CategoriesDataSource` 에서 해당 데이터를 선택 하 여 `CategoriesBLL` s 클래스 `GetCategories()` 메서드.


[![CategoriesBLL 클래스의 GetCategories() 메서드를 사용 하는 ObjectDataSource 구성](custom-buttons-in-the-datalist-and-repeater-cs/_static/image10.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image9.png)

**그림 5**: ObjectDataSource를 사용 하 여 구성 합니다 `CategoriesBLL` s 클래스 `GetCategories()` 메서드 ([클릭 하 여 큰 이미지 보기](custom-buttons-in-the-datalist-and-repeater-cs/_static/image11.png))


Visual Studio는 기본 생성 DataList 컨트롤을 달리 `ItemTemplate` 데이터 원본에 따라 s 반복기 템플릿을 수동으로 정의 해야 합니다. 반복기가의 템플릿 해야 생성 및 선언적 편집 또한 (즉, 있는 s 편집 템플릿이 옵션에서 반복기가 스마트 태그에).

원본 탭 왼쪽된 아래 모퉁이에서 클릭 하 고 추가 `ItemTemplate` 에서 s 범주 이름을 표시 하는 `<h3>` 요소 및 해당 설명을 단락에서 태그; 포함을 `SeparatorTemplate` 단락 구분선을 표시 하는 (`<hr />`) 간의 범주입니다. 추가적으로 LinkButton 사용 하 여 해당 `Text` 속성이 제품 표시로 설정 합니다. 다음이 단계를 완료 한 후 페이지 s 선언적 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample2.aspx)]

그림 6에서는 브라우저를 통해 볼 때 페이지를 보여 줍니다. 각 범주 이름 및 설명을 나열 됩니다. 제품 표시 단추를 클릭 하면 포스트백을 발생 시키는 하지만 모든 작업을 아직 수행 하지 않습니다.


[![각 범주 이름이 설명과 함께 표시 됩니다, 제품 LinkButton 표시](custom-buttons-in-the-datalist-and-repeater-cs/_static/image13.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image12.png)

**그림 6**: 제품 LinkButton 표시와 함께 각 범주 이름 및 설명이 표시 됩니다 ([큰 이미지를 보려면 클릭](custom-buttons-in-the-datalist-and-repeater-cs/_static/image14.png))


## <a name="step-3-executing-server-side-logic-when-the-show-products-linkbutton-is-clicked"></a>3 단계: 서버 쪽 논리 때 the 표시 제품 LinkButton 실행 클릭

포스트백이 발생할 단추나 LinkButton, ImageButton DataList 또는 반복기에서 템플릿 내에서 클릭 하면 언제 든 지 및 DataList 또는 Repeater의 `ItemCommand` 이벤트가 발생 합니다. 외에 `ItemCommand` 이벤트, DataList 컨트롤 수 있습니다 하는 경우에 다른, 보다 구체적인 이벤트를 발생 s 단추 `CommandName` (삭제, 편집, 취소, 업데이트 또는 선택) 하는 예약 된 문자열 중 하나를 설정 하지만 `ItemCommand` 이벤트는 *항상* 발생 합니다.

DataList 또는 Repeater 내에서 단추를 클릭 하면 종종 해야 (될 수 있습니다 여러 편집을 모두 같은 컨트롤에 단추 및 삭제 단추 경우)에서 클릭 된 단추 및 아마도 일부 추가 정보 (예: 전달 기본 키 값의 해당 단추를 클릭 한 항목). 단추를 LinkButton 및 ImageButton 값에 전달 되는 두 가지 속성을 제공 합니다 `ItemCommand` 이벤트 처리기:

- `CommandName` 서식 파일의 각 단추를 식별 하는 데 일반적으로 문자열로
- `CommandArgument` 기본 키 값과 같은 일부 데이터 필드의 값을 유지 하는 데 주로 사용

이 예에서는 LinkButton s를 설정 `CommandName` ShowProducts 바인딩 현재 레코드 s 기본 키 값을 속성 `CategoryID` 에 `CommandArgument` 데이터 바인딩 구문을 사용 하 여 속성 `CategoryArgument='<%# Eval("CategoryID") %>'`합니다. 이러한 두 속성을 지정한 후 LinkButton s 선언적 구문을 다음과 같이 표시 됩니다.


[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample3.aspx)]

단추를 클릭할 때, 포스트백이 발생할 및 DataList 또는 Repeater의 `ItemCommand` 이벤트가 발생 합니다. 이벤트 처리기 단추 s 되는지를 `CommandName` 고 `CommandArgument` 값입니다.

S 반복기에 대 한 이벤트 처리기를 만듭니다 `ItemCommand` 이벤트 처리기에 전달 된 이벤트와 두 번째 매개 변수를 참고 (라는 `e`). 이 두 번째 매개 변수는 형식 [ `RepeaterCommandEventArgs` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeatercommandeventargs.aspx) 있고 다음 네 가지 속성:

- `CommandArgument` s 클릭 한 단추의 값 `CommandArgument` 속성
- `CommandName` s 단추의 값 `CommandName` 속성
- `CommandSource` 클릭 된 단추 컨트롤에 대 한 참조
- `Item` 에 대 한 참조를 [ `RepeaterItem` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeateritem.aspx) 클릭 된 단추를 포함 하는;으로 반복기에 바인딩된 각 레코드는 매니페스트를 `RepeaterItem`

선택한 범주의 s 이후 `CategoryID` 를 통해 전달 되는 `CommandArgument` 속성 집합에서 선택한 범주와 관련 된 제품을 가져올 수 있습니다는 `ItemCommand` 이벤트 처리기. 이러한 제품 BulletedList 컨트롤에 바인딩된 다음 수는 `ItemTemplate` (어떤 것 추가할 아직 ve). 참조 모두 그대로 유지 한 다음, BulletedList, 추가 하는 것은 `ItemCommand` 이벤트 처리기를 4 단계에서에서 해결할는 선택한 범주에 대 한 제품 집합에 바인딩합니다.

> [!NOTE]
> S DataList `ItemCommand` 이벤트 처리기가 형식의 개체를 전달 [ `DataListCommandEventArgs` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistcommandeventargs.aspx), 같은 네 가지 속성을 제공 하는 `RepeaterCommandEventArgs` 클래스입니다.


## <a name="step-4-displaying-the-selected-category-s-products-in-a-bulleted-list"></a>4 단계: 글머리 기호 목록에서 선택한 범주의 제품 표시

S Repeater 내 선택한 범주의 제품을 표시할 수 있습니다 `ItemTemplate` 모든 다양 한 컨트롤을 사용 합니다. 또 다른 중첩 된 Repeater, DataList, DropDownList, GridView 및 등에 추가할 수 있었습니다. 글머리 기호 목록으로 제품을 표시할 것 이므로 BulletedList 컨트롤 사용 하겠습니다 그러나. 반환 합니다 `CustomButtons.aspx` s 선언적 태그를 페이지, BulletedList 컨트롤을 추가 합니다 `ItemTemplate` 제품 LinkButton 표시 한 후 합니다. 집합 BulletedLists s `ID` 에 `ProductsInCategory`입니다. BulletedList를 통해 지정 된 데이터 필드의 값을 표시 합니다 `DataTextField` 속성에이 컨트롤에 바인딩되어 설정, 제품 정보를 포함 하므로 합니다 `DataTextField` 속성을 `ProductName`.


[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample4.aspx)]

에 `ItemCommand` 이벤트 처리기를 사용 하 여이 컨트롤 참조 `e.Item.FindControl("ProductsInCategory")` 선택한 범주와 관련 된 제품 집합에 바인딩합니다.


[!code-csharp[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample5.cs)]

작업을 수행 하기 전에 합니다 `ItemCommand` 이벤트 처리기를이 s 먼저 들어오는 값을 확인 하는 것이 좋습니다 `CommandName`합니다. 이후를 `ItemCommand` 이벤트 처리기를 실행 하는 경우 *모든* 템플릿 사용에서 단추를 여러 개 있는 경우 단추를 클릭 합니다 `CommandName` 값에 수행할 동작을 파악 하기. 검사는 `CommandName` 여기는 생각해 볼 여지가 단추 하나만 있으므로 이지만 폼에 좋은 습관입니다. 다음으로 `CategoryID` 선택한 범주에서 검색 되는 `CommandArgument` 속성. BulletedList 컨트롤 템플릿에서 다음 참조 하 고 결과에 연결 합니다 `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)` 메서드.

같은 DataList, 내에서 단추를 사용 하는 이전 자습서 [An 개요의 편집 및 DataList에서 데이터 삭제](../editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md)를 통해 지정된 된 항목의 기본 키 값을 확인 했습니다는 `DataKeys` 컬렉션입니다. Repeater에 없는이 이렇게 DataList와 잘 작동 하는 동안는 `DataKeys` 속성입니다. 단추 s 통해 같은 기본 키 값을 제공 하는 것에 대 한 대체 방법을 사용 해야 합니다 대신 `CommandArgument` 속성 합니다 년대에서해당값을읽고숨겨진된Label웹컨트롤템플릿내에서기본키값을할당하거나`ItemCommand`이벤트 처리기를 사용 하 여 `e.Item.FindControl("LabelID")`입니다.

완료 한 후의 `ItemCommand` 이벤트 처리기를 잠시이 페이지를 브라우저에서 테스트 합니다. 그림 7에서 알 수 있듯이, 클릭 하면 표시 제품 링크 포스트백을 발생 시키는 고를 BulletedList에 선택한 범주에 대 한 제품 표시. 또한 다른 범주의 제품 표시 링크를 클릭할 경우에이 제품 정보 남아 note 합니다.

> [!NOTE]
> 한 번에 하나의 범주의 제품 나와 되도록이 보고서의 동작을 수정 하려면, s BulletedList 컨트롤을 설정 하면 됩니다 `EnableViewState` 속성을 `False`입니다.


[![선택한 범주의 제품을 전시 하기를 BulletedList는](custom-buttons-in-the-datalist-and-repeater-cs/_static/image16.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image15.png)

**그림 7**: 선택한 범주의 제품을 전시 하기는 BulletedList는 ([큰 이미지를 보려면 클릭](custom-buttons-in-the-datalist-and-repeater-cs/_static/image17.png))


## <a name="summary"></a>요약

DataList 및 반복기 컨트롤에는 임의 개수의 단추, Linkbutton, 또는 ImageButtons 해당 템플릿 내에서 포함할 수 있습니다. 이러한 단추를 클릭 하면 포스트백을 발생 시키고는 `ItemCommand` 이벤트입니다. 클릭 되는 단추를 사용 하 여 사용자 지정 서버 쪽 작업에 연결 하려면 만들기에 대 한 이벤트 처리기는 `ItemCommand` 이벤트입니다. 이 이벤트 처리기에서 먼저 들어오는 확인 `CommandName` 단추를 클릭 했는지 확인 하는 값입니다. 추가 정보 필요에 따라 단추 s 통해 제공 될 수 있습니다 `CommandArgument` 속성입니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Dennis Patterson 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [다음](custom-buttons-in-the-datalist-and-repeater-vb.md)
