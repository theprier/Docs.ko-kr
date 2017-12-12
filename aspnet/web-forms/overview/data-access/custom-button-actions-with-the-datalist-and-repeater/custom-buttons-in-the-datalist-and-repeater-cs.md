---
uid: web-forms/overview/data-access/custom-button-actions-with-the-datalist-and-repeater/custom-buttons-in-the-datalist-and-repeater-cs
title: "DataList 및 반복기 (C#)에서 사용자 지정 단추 | Microsoft Docs"
author: rick-anderson
description: "이 자습서에서는 시스템에서 해당 associ를 표시 하려면 단추를 제공 하는 각 범주와 범주를 나열 하는 반복기를 사용 하는 인터페이스를 빌드합니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/13/2006
ms.topic: article
ms.assetid: 1f42e332-78dc-438b-9e35-0c97aa0ad929
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions-with-the-datalist-and-repeater/custom-buttons-in-the-datalist-and-repeater-cs
msc.type: authoredcontent
ms.openlocfilehash: fa4b3ea69999f0d97d20047663d302277ebdf433
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="custom-buttons-in-the-datalist-and-repeater-c"></a>DataList 및 반복기 (C#)에서 사용자 지정 단추
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_46_CS.exe) 또는 [PDF 다운로드](custom-buttons-in-the-datalist-and-repeater-cs/_static/datatutorial46cs1.pdf)

> 이 자습서에서는 시스템에서 BulletedList 컨트롤을 사용 하 여 관련된 제품을 표시 하려면 단추를 제공 하는 각 범주와 범주를 나열 하는 반복기를 사용 하는 인터페이스를 빌드합니다.


## <a name="introduction"></a>소개

지난 17 DataList 및 반복기 자습서 전체에서 우리 했습니다 모두 읽기 전용 예제 및 편집 및 삭제 예제를 생성 합니다. 편집 및 삭제 DataList 내에서 기능을 쉽게 하려면 DataList s에 단추 추가 `ItemTemplate` 를 클릭 하면 포스트백을 발생 한에 해당 하는 단추의 DataList 이벤트를 발생 시킨 `CommandName` 속성입니다. 예를 들어 단추를 추가 `ItemTemplate` 와 `CommandName` 편집의 속성 값을 사용 하면 DataList s `EditCommand` 포스트백에 대해 발생 하도록와 하나는 `CommandName` 발생 삭제는 `DeleteCommand`합니다.

또한를 편집한 삭제 단추 DataList 및 반복기 컨트롤 포함할 수도 단추, 링크, 단추가 또는 ImageButtons를 클릭 하면 일부 사용자 지정 서버 쪽 논리를 수행 합니다. 이 자습서에서는 시스템의 범주를 나열 하는 반복기를 사용 하는 인터페이스를 빌드합니다. 각 범주에 대 한 반복기 BulletedList 컨트롤을 사용 하 여에 연결 된 제품 범주를 표시 하도록 단추가 포함 됩니다 (그림 1 참조).


[![글머리 기호 목록에서 범주의 제품 표시 제품 링크 표시를 클릭합니다.](custom-buttons-in-the-datalist-and-repeater-cs/_static/image2.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image1.png)

**그림 1**: 글머리 기호 목록에서 범주의 제품 제품 표시 링크 표시를 클릭 하면 ([전체 크기 이미지를 보려면 클릭](custom-buttons-in-the-datalist-and-repeater-cs/_static/image3.png))


## <a name="step-1-adding-the-custom-button-tutorial-web-pages"></a>1 단계: 사용자 지정 단추 자습서 웹 페이지 추가

사용자 지정 단추를 추가 하는 방법을 살펴보기 전에 먼저이 자습서에 사용 해야 하는 웹 사이트 프로젝트에서 ASP.NET 페이지를 만들 잠시 s가 있습니다. 라는 새 폴더를 추가 하 여 시작 `CustomButtonsDataListRepeater`합니다. 다음에 있는 각 페이지에 연결할 수 있도록 해당 폴더에 다음과 같은 두 ASP.NET 페이지를 추가 `Site.master` 마스터 페이지:

- `Default.aspx`
- `CustomButtons.aspx`


![사용자 지정 단추와 관련 된 자습서에 대 한 ASP.NET 페이지 추가](custom-buttons-in-the-datalist-and-repeater-cs/_static/image4.png)

**그림 2**: 사용자 지정 단추와 관련 된 자습서에 대 한 ASP.NET 페이지 추가


다른 폴더에서와 같이 `Default.aspx` 에 `CustomButtonsDataListRepeater` 폴더는 해당 섹션의 자습서를 나열 합니다. 이전에 설명한 대로 `SectionLevelTutorialListing.ascx` 이 기능을 제공 하는 사용자 정의 컨트롤입니다. 이 사용자 정의 컨트롤을 추가 `Default.aspx`의 디자인 뷰에서 페이지 하려면 솔루션 탐색기에서 끌어서 합니다.


[![Default.aspx로 SectionLevelTutorialListing.ascx 사용자 정의 컨트롤 추가](custom-buttons-in-the-datalist-and-repeater-cs/_static/image6.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image5.png)

**그림 3**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `Default.aspx` ([전체 크기 이미지를 보려면 클릭](custom-buttons-in-the-datalist-and-repeater-cs/_static/image7.png))


마지막으로, 페이지에 항목으로 추가 된 `Web.sitemap` 파일입니다. 특히 반복기와 DataList 페이징 및 정렬 한 후 다음 태그를 추가 `<siteMapNode>`:


[!code-xml[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample1.xml)]

업데이트 한 후 `Web.sitemap`, 브라우저를 통해 자습서 웹 사이트를 보려면 보십시오. 왼쪽 메뉴에는 이제 편집, 삽입 및 삭제 자습서에 대 한 항목이 포함 됩니다.


![이제 사이트 맵 사용자 지정 단추 자습서에 대 한 항목을 포함](custom-buttons-in-the-datalist-and-repeater-cs/_static/image8.png)

**그림 4**: 이제 사이트 맵 사용자 지정 단추 자습서에 대 한 항목을 포함


## <a name="step-2-adding-the-list-of-categories"></a>2 단계: 추가 범주 목록

해야 표시 제품 LinkButton 함께 모든 범주를 나열 하는 반복기를 만들려면이 자습서를 클릭 하면 관련된 범주가의 제품이 글머리 기호 목록에 표시 됩니다. S 시스템에 범주를 나열 하는 단순 반복기를 처음 만들 수 있도록 합니다. 열어 시작는 `CustomButtons.aspx` 페이지에 `CustomButtonsDataListRepeater` 폴더입니다. 도구 상자에서 디자이너와 세트가으로 반복기를 끌어 해당 `ID` 속성을 `Categories`합니다. 다음으로 반복기 s 스마트 태그에서 새 데이터 소스 컨트롤을 만듭니다. 특히 이라는 새 ObjectDataSource 컨트롤을 만들어 `CategoriesDataSource` 에서 해당 데이터를 선택 하 고 `CategoriesBLL` s 클래스 `GetCategories()` 메서드.


[![ObjectDataSource CategoriesBLL 클래스의 GetCategories() 메서드를 사용 하도록 구성](custom-buttons-in-the-datalist-and-repeater-cs/_static/image10.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image9.png)

**그림 5**: 구성에 사용 하 여 ObjectDataSource는 `CategoriesBLL` s 클래스 `GetCategories()` 메서드 ([전체 크기 이미지를 보려면 클릭](custom-buttons-in-the-datalist-and-repeater-cs/_static/image11.png))


DataList 컨트롤은 Visual Studio의 기본 생성을 달리 `ItemTemplate` 데이터 원본에 따라, s 템플릿에 수동으로 정의 해야 합니다. 또한 s 템플릿에 만들고 편집할 선언적으로 (즉, 없어 s 없습니다 템플릿 편집 옵션을 반복기 s 스마트 태그).

원본 탭 왼쪽된 아래에서 클릭 하 고 추가 `ItemTemplate` 에서 s 범주 이름을 표시 하는 `<h3>` 요소와 해당 설명이 있는 단락 태그; 포함 한 `SeparatorTemplate` 단락 구분선을 표시 하는 (`<hr />`) 각 사이 범주입니다. 추가적으로 인 LinkButton 해당 `Text` 속성이 제품 표시로 설정 합니다. 다음이 단계를 완료 한 후 페이지 s 선언적 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample2.aspx)]

그림 6 브라우저를 통해 볼 때 페이지를 보여줍니다. 각 범주 이름 및 설명을 나열 됩니다. 제품 표시 단추를 클릭 하면 포스트백을 발생 하지만 모든 작업을 아직 수행 하지 않습니다.


[![표시 제품 LinkButton 함께 각 범주의 이름 및 설명을 표시 됩니다.](custom-buttons-in-the-datalist-and-repeater-cs/_static/image13.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image12.png)

**그림 6**: 표시 제품 LinkButton 함께 각 범주 이름 및 설명이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](custom-buttons-in-the-datalist-and-repeater-cs/_static/image14.png))


## <a name="step-3-executing-server-side-logic-when-the-show-products-linkbutton-is-clicked"></a>3 단계: 실행 하는 서버 쪽 논리가 때 the 표시 제품 LinkButton 클릭

포스트백이 발생할 단추나 LinkButton을 DataList 또는 반복기에서 템플릿 내에서 ImageButton을 클릭 하면 언제 든 지와 DataList 또는 반복기의 `ItemCommand` 이벤트 발생 합니다. 외에 `ItemCommand` 이벤트를 제어 하는 경우 다른, 보다 구체적인 이벤트를 발생도 될 수 있습니다 DataList의 단추 `CommandName` (삭제, 편집, 취소, 업데이트 또는 Select) 하는 예약 된 문자열 중 하나로 속성이 설정 되어 있지만 `ItemCommand` 이벤트는 *항상* 발생 합니다.

반복기 또는 DataList 내에서 단추를 클릭 하면 종종 해야 어느 단추를 클릭 하는 경우 있을 수 있음을 여러 편집 하는 모두 같은 컨트롤 내에서 단추 및 삭제 단추 및 아마도 몇 가지 추가 정보 (예: 전달 기본 키 값의 해당 단추를 클릭 한 항목). 단추, LinkButton을 및 ImageButton 제공 두 속성 값을 가진에 전달 되는 `ItemCommand` 이벤트 처리기.

- `CommandName`일반적으로 각 단추에 서식 파일을 식별 하는 데 필요한 문자열
- `CommandArgument`기본 키 값 등의 일부 데이터 필드의 값을 유지 하는 일반적으로 사용

이 예제에서는 설정 LinkButton s `CommandName` 속성 ShowProducts 및 bind 현재 레코드 s 기본 키 값을 `CategoryID` 에 `CommandArgument` 구문이 사용 하 여 속성 `CategoryArgument='<%# Eval("CategoryID") %>'`합니다. 이러한 두 속성을 지정한 후 LinkButton s 선언적 구문 다음과 같이 표시 됩니다.


[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample3.aspx)]

단추를 클릭할 때, 포스트백이 발생할 및 DataList 또는 반복기의 `ItemCommand` 이벤트 발생 합니다. 이벤트 처리기 단추 s 전달 `CommandName` 및 `CommandArgument` 값입니다.

S 반복기에 대 한 이벤트 처리기를 만들고 `ItemCommand` 이벤트 처리기에 전달 된 이벤트와 두 번째 매개 변수 메모 (라는 `e`). 이 두 번째 매개 변수는 형식 [ `RepeaterCommandEventArgs` ](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.repeatercommandeventargs.aspx) 다음 네 가지 속성이 있습니다.

- `CommandArgument`s 클릭 한 단추의 값 `CommandArgument` 속성
- `CommandName`s 단추의 값 `CommandName` 속성
- `CommandSource`클릭 된 단추 컨트롤에 대 한 참조
- `Item`에 대 한 참조는 [ `RepeaterItem` ](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.repeateritem.aspx) 으로 반복기에 바인딩된 각 레코드는 매니페스트; 클릭 된 단추의 포함 하는`RepeaterItem`

선택한 범주의 s 이후 `CategoryID` 를 통해 전달 되는 `CommandArgument` 속성에서 선택한 범주와 관련 된 제품의 집합을 가져올 수 있습니다는 `ItemCommand` 이벤트 처리기입니다. 이러한 제품 BulletedList 컨트롤에 바인딩할 수 다음는 `ItemTemplate` (어떤 것 추가할 아직 했습니다). 유지 되는 경우 다음 BulletedList를 추가 하는 모든 참조는 `ItemCommand` 이벤트 처리기의 경우 4 단계에서에서 해결할 선택한 범주에 대 한 제품 집합에 바인딩합니다.

> [!NOTE]
> DataList s `ItemCommand` 형식의 개체를 전달 된 이벤트 처리기 [ `DataListCommandEventArgs` ](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.datalistcommandeventargs.aspx)과 같은 4 개의 속성을 제공 하는 `RepeaterCommandEventArgs` 클래스입니다.


## <a name="step-4-displaying-the-selected-category-s-products-in-a-bulleted-list"></a>4 단계: 글머리 기호 목록에서 선택한 범주의 제품 표시

선택한 범주의의 제품의 반복 내에서 표시 될 수 있습니다 `ItemTemplate` 개수에 관계 없이 컨트롤을 사용 하 여 합니다. 또 다른 중첩 된 반복기, DataList, DropDownList, GridView, 및 등을 추가할 수도 있습니다. 글머리 기호 목록으로 제품을 표시 하려면 할 것 이므로 BulletedList 컨트롤을 사용 하겠습니다 하지만. 돌아가기는 `CustomButtons.aspx` s 선언 태그 페이지, BulletedList 컨트롤을 추가 `ItemTemplate` 표시 제품 LinkButton 후 합니다. BulletedLists s 설정 `ID` 를 `ProductsInCategory`합니다. BulletedList을 통해 지정 된 데이터 필드의 값이 표시는 `DataTextField` 속성; 이므로이 컨트롤에 바인딩된, 설정 제품 정보는 `DataTextField` 속성을 `ProductName`합니다.


[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample4.aspx)]

에 `ItemCommand` 이벤트 처리기를 사용 하 여이 컨트롤 참조 `e.Item.FindControl("ProductsInCategory")` 선택한 범주와 관련 된 제품의 집합에 바인딩합니다.


[!code-csharp[Main](custom-buttons-in-the-datalist-and-repeater-cs/samples/sample5.cs)]

작업을 수행 하기 전에 `ItemCommand` 이벤트 처리기 것 s 먼저 들어오는 값을 확인 하는 것이 좋습니다 `CommandName`합니다. 이후는 `ItemCommand` 될 때 이벤트 처리기 발생 *모든* 에 있는 경우 여러 단추 템플릿 사용 단추를 클릭는 `CommandName` 를 수행 하는 작업을 구분 하는 값입니다. 검사는 `CommandName` 여기 이론에 불과합니다, 한 번의 단추만 개이므로 이지만 좋은 습관 폼입니다. 다음으로 `CategoryID` 선택한 범주의 검색 되는 `CommandArgument` 속성. BulletedList 컨트롤 템플릿의 참조 하 고 결과에 바인딩된는 `ProductsBLL` s 클래스 `GetProductsByCategoryID(categoryID)` 메서드.

와 같은 한 DataList 내에서 단추를 사용 하는 이전 자습서에서 [는 개요의 편집 및 DataList의 데이터를 삭제](../editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md), 것으로 확인을 통해 지정된 된 항목의 기본 키 값의 `DataKeys` 컬렉션입니다. 반복기에 없는이 방법은 DataList와 잘 작동 하는 동안 한 `DataKeys` 속성입니다. 대신, s 단추를 통해와 같은 기본 키 값을 제공 하는 것에 대 한 다른 접근 방식은 사용 해야 했습니다 `CommandArgument` 속성 또는 숨겨진된 Label 웹 컨트롤 템플릿 내에서 기본 키 값을 할당 하 고 해당 값은 에다시기록하여`ItemCommand`이벤트 처리기를 사용 하 여 `e.Item.FindControl("LabelID")`합니다.

완료 한 후는 `ItemCommand` 이벤트 처리기를 충분히 브라우저에서이 페이지를 테스트해 보십시오. 그림 7에서 볼 수 있듯이 표시 제품을 클릭 하면 링크 포스트백 시키고 유효성 검사는 BulletedList의 선택된 된 범주에 대 한 제품을 표시 합니다. 또한 다른 범주의 제품 표시 링크를 클릭할 경우에이 제품 정보 남아 note 합니다.

> [!NOTE]
> 한 번에 하나의 범주의 제품 나와 되도록이 보고서의 동작을 수정 하려면, 단순히 s BulletedList 컨트롤 설정 `EnableViewState` 속성을 `False`합니다.


[![BulletedList 하는 데 선택한 범주에 속하는 제품 표시](custom-buttons-in-the-datalist-and-repeater-cs/_static/image16.png)](custom-buttons-in-the-datalist-and-repeater-cs/_static/image15.png)

**그림 7**: A BulletedList는 선택한 범주에 속하는 제품을 표시 하는 데 사용 됩니다 ([전체 크기 이미지를 보려면 클릭](custom-buttons-in-the-datalist-and-repeater-cs/_static/image17.png))


## <a name="summary"></a>요약

DataList 및 반복기 컨트롤 개수에 관계 없이 단추, 링크, 단추가 또는 ImageButtons 해당 템플릿 내에 포함할 수 있습니다. 이러한 단추를 클릭 하면 포스트백을 발생 시키고는 `ItemCommand` 이벤트입니다. 사용자 지정 서버 쪽 작업 단추 클릭을 연결 하려면에 대 한 이벤트 처리기를 만들고는 `ItemCommand` 이벤트입니다. 이 이벤트 처리기에서 먼저 들어오는 확인 `CommandName` 값을 어느 단추를 클릭 합니다. S 단추를 통해 필요에 따라 추가 정보를 제공할 수 `CommandArgument` 속성입니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Dennis Patterson 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[다음](custom-buttons-in-the-datalist-and-repeater-vb.md)
