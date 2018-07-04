---
uid: web-forms/overview/data-access/paging-and-sorting/creating-a-customized-sorting-user-interface-vb
title: 사용자 지정 된 정렬 사용자 인터페이스 (VB) 만들기 | Microsoft Docs
author: rick-anderson
description: 데이터 정렬의 긴 목록을 표시 하는 경우에 매우 유용할 수 있습니다 행 구분 기호를 도입 하 여 관련된 데이터를 그룹화 합니다. 이 자습서에서는 살펴보겠습니다 자격 방법...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/15/2006
ms.topic: article
ms.assetid: f3897a74-cc6a-4032-8f68-465f155e296a
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/creating-a-customized-sorting-user-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 27ff1efb47f8e74c3b9f090af646229a9121661b
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37394562"
---
<a name="creating-a-customized-sorting-user-interface-vb"></a>사용자 지정 된 정렬 사용자 인터페이스 (VB) 만들기
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_27_VB.exe) 또는 [PDF 다운로드](creating-a-customized-sorting-user-interface-vb/_static/datatutorial27vb1.pdf)

> 데이터 정렬의 긴 목록을 표시 하는 경우에 매우 유용할 수 있습니다 행 구분 기호를 도입 하 여 관련된 데이터를 그룹화 합니다. 이 자습서는 이러한 정렬 사용자 인터페이스를 만드는 방법을 살펴보겠습니다.


## <a name="introduction"></a>소개

긴 목록을 표시 하 데이터를 정렬 하는 경우 정렬 된 열에서 다른 값의 일부만 있는 최종 사용자 것을 정확 하 게 차이 경계 발생 파악 하기가 어렵습니다. 예를 들어 제품이 81 데이터베이스 에서만 9 개 밖에 다른 범주 선택 (8 개의 고유 범주와 `NULL` 옵션). Seafood 범주에 속하는 제품을 검사 하는 사용자의 경우를 것이 좋습니다. 나열 된 페이지에서 *모든* 최상의 선택 게 범주를 함께 그룹화 하 여 결과 정렬 하는 사용자 수 결정 하는 단일 GridView에는 제품의 모든 Seafood 제품과 함께 합니다. 범주별으로 정렬 한 후 사용자 다음 해야 목록을 hunt Seafood 그룹화 된 제품의 시작 및 종료 위치를 찾고 합니다. 결과 사전순으로 정렬 되므로 범주 이름을 Seafood 제품 찾기 어렵습니다 좋겠지만 그 여전히 밀접 하 게 표의 항목 목록을 검색 합니다.

정렬 된 그룹 간의 경계를 강조 표시를 위해 많은 웹 사이트는 이러한 그룹 간에 구분 기호를 추가 하는 사용자 인터페이스를 사용 합니다. 그림 1에 나와 있는 것 처럼 구분 기호 선택 하면 보다 신속 하 게 특정 그룹을 찾 및 해당 경계를 식별할 뿐만 아니라 데이터에 존재 하는 고유한 그룹을 확인 합니다.


[![각 범주 그룹은 명확 하 게 식별](creating-a-customized-sorting-user-interface-vb/_static/image2.png)](creating-a-customized-sorting-user-interface-vb/_static/image1.png)

**그림 1**: 각 범주 그룹 명확 하 게 식별 됩니다 ([큰 이미지를 보려면 클릭](creating-a-customized-sorting-user-interface-vb/_static/image3.png))


이 자습서는 이러한 정렬 사용자 인터페이스를 만드는 방법을 살펴보겠습니다.

## <a name="step-1-creating-a-standard-sortable-gridview"></a>1 단계: 표준, 정렬 가능 GridView 만들기

GridView 향상 된 정렬 인터페이스를 제공 하는 표준, 정렬 가능 GridView을 먼저 만든 수를 추가 하는 방법에 살펴봅니다 전에 제품을 나열 합니다. 열어서 시작 합니다 `CustomSortingUI.aspx` 페이지에 `PagingAndSorting` 폴더입니다. 페이지에 GridView 추가 해당 `ID` 속성을 `ProductList`, 새 ObjectDataSource에 바인딩합니다. ObjectDataSource를 사용 하 여 구성 합니다 `ProductsBLL` s 클래스 `GetProducts()` 레코드를 선택 하는 메서드.

만 포함 되도록 GridView를 다음으로 구성 합니다 `ProductName`, `CategoryName`를 `SupplierName`, 및 `UnitPrice` BoundFields 및 지원 되지 않는 CheckBoxField 합니다. 마지막으로 구성 하는 GridView가 스마트 태그에 정렬 사용 확인란을 선택 하 여 정렬을 지원 하기 위해 GridView (또는 설정 하 여 해당 `AllowSorting` 속성을 `true`). 이러한 추가 마치면는 `CustomSortingUI.aspx` 페이지 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](creating-a-customized-sorting-user-interface-vb/samples/sample1.aspx)]

브라우저에서 진행 상황을 지금 보려면 잠시 시간이 소요 됩니다. 그림 2에서는 사전순으로 범주 데이터를 정렬할 때 정렬 가능한 GridView를 보여 줍니다.


[![정렬 가능한 GridView의 데이터 범주별 정렬](creating-a-customized-sorting-user-interface-vb/_static/image5.png)](creating-a-customized-sorting-user-interface-vb/_static/image4.png)

**그림 2**: 데이터가 범주별으로 정렬 되는 정렬 가능한 GridView s ([큰 이미지를 보려면 클릭](creating-a-customized-sorting-user-interface-vb/_static/image6.png))


## <a name="step-2-exploring-techniques-for-adding-the-separator-rows"></a>2 단계: 행 구분 기호를 추가 하는 것에 대 한 기술 탐색

제네릭, 정렬 가능 GridView 전체를 사용 하 여는 GridView 각 고유한 정렬 된 그룹 앞에 구분 기호 행을 추가 하는 일을 할 수 있습니다. 하지만 어떻게 이러한 행에 삽입할 수 있습니다 GridView? 기본적으로, 필요한 GridView s 개의 행을 반복 하 정렬된 된 열 값 사이의 차이 발생 하는 위치를 확인 하 고 적절 한 구분 기호 행을 추가 합니다. 솔루션 어딘가에 GridView가 자연 스러운 것이 문제를 고려할 때는 `RowDataBound` 이벤트 처리기입니다. 설명한 대로 합니다 [데이터를 기반으로 사용자 지정 서식 지정](../custom-formatting/custom-formatting-based-upon-data-vb.md) 자습서, s 행 데이터를 기반으로 행 수준 서식 지정을 적용 하는 경우이 이벤트 처리기는 일반적으로 사용 됩니다. 그러나는 `RowDataBound` 이벤트 처리기가 솔루션을 여기서 행도이 이벤트 처리기에서 프로그래밍 방식으로 GridView에 추가할 수 없습니다. GridView의 `Rows` , 사실, 컬렉션이 읽기 전용입니다.

GridView에 추가 행을 추가 하려면 세 가지 선택 사항이 있습니다.

- GridView에 바인딩되는 실제 데이터에 이러한 메타 데이터 구분 기호 행을 추가 합니다.
- GridView를 데이터에 바인딩된 후 추가 `TableRow` 수집을 제어 하는 GridView의 인스턴스
- GridView 컨트롤을 확장 하 고 GridView의 구조를 구성할 책임이 이러한 메서드를 재정의 하는 사용자 지정 서버 컨트롤 만들기

사용자 지정 서버 컨트롤을 만들 것 가장 좋은 방법은 여러 웹 사이트에 걸쳐서 여러 웹 페이지에서이 기능이 필요한 경우입니다. 그러나 많은 양의 코드를 GridView가 내부 작업에 대해 깊이 있는 철저 한 탐색 해야 합니다. 따라서이 자습서에 대해이 옵션을 고려 하지 됩니다.

다른 두 가지 옵션 추가 구분 기호 행 되는 실제 데이터를 GridView에 바인딩됩니다 및 GridView s control 컬렉션 후 해당 바인딩된-문제를 다르게 공격 및 토론을 다룰 되었습니다.

## <a name="adding-rows-to-the-data-bound-to-the-gridview"></a>GridView에 바인딩된 데이터 행을 추가 합니다.

GridView 데이터 원본에 바인딩되는 경우 생성 된 `GridViewRow` 데이터 원본에 의해 반환 된 각 레코드에 대 한 합니다. 따라서 데이터 원본에 GridView에 바인딩하기 전에 구분 기호 레코드를 추가 하 여 필요한 구분 기호 행을 삽입할 수 했습니다. 그림 3에서는이 개념을 보여 줍니다.


![한 가지 방법은 데이터 원본에 행 구분 기호를 추가 해야](creating-a-customized-sorting-user-interface-vb/_static/image7.png)

**그림 3**: 기술 중 하나는 행 구분 기호를 데이터 원본 추가


특별 한 구분 기호 레코드가 없습니다; 때문에 따옴표로 단어 구분 기호 레코드 사용 아니라 우리가 해야 어떤 이유로 든 플래그 일반 데이터 행이 아닌 구분 기호를 데이터 원본에서 특정 레코드를 제공 하는입니다. 이 예제에서는 바인딩 다시 것에 대 한는 `ProductsDataTable` GridView로 구성 된 인스턴스 `ProductRows`합니다. 레코드 구분 기호 행으로 설정 하 여 플래그 수에서는 해당 `CategoryID` 속성을 `-1` (이후 값 수 t 일반적으로 존재).

이 기법을 활용 하려면 d 해야 다음 단계를 수행 합니다.

1. GridView에 바인딩할 데이터를 프로그래밍 방식으로 검색 (한 `ProductsDataTable` 인스턴스)
2. GridView에 따라 데이터 정렬 `SortExpression` 고 `SortDirection` 속성
3. 반복 합니다 `ProductsRows` 에 `ProductsDataTable`차이점 정렬 된 열에 있는 곳을 찾고,
4. 각 그룹 경계에서 구분 기호 레코드를 삽입할 `ProductsRow` s가 있는 DataTable 인스턴스 `CategoryID` 로 `-1` (또는 모든 지정 된 구분 기호 레코드와 레코드를 표시 따라 결정)
5. 행 구분 기호를 삽입 한 후 프로그래밍 방식으로 데이터를 바인딩할 GridView

5 단계 외에도 d 해야 GridView s에 대 한 이벤트 처리기를 제공 `RowDataBound` 이벤트입니다. 여기에서 d 확인 `DataRow` 구분 기호 것인지 확인 하 고 행을 하나입니다 `CategoryID` 설정이 `-1`합니다. 그렇다면 d 아마도 하고자 서식 지정 또는 셀에 표시 되는 텍스트를 조정 합니다.

또한 GridView s에 대 한 이벤트 처리기를 제공 해야 할 때 위에서 설명한 것 보다 좀 더 많은 작업이 필요 정렬 그룹 경계 삽입이 기술을 사용 하 여 `Sorting` 의 추적 이벤트 및 유지 합니다 `SortExpression` 및 `SortDirection` 값입니다.

## <a name="manipulating-the-gridview-s-control-collection-after-it-s-been-databound"></a>컬렉션 뒤 s 제어 GridView s 조작 된 데이터 바인딩

GridView에 바인딩하기 전에 데이터를 메시지, 아닌 구분 기호 행을 추가할 수 있습니다 *후* GridView 데이터 바인딩 되었습니다. 데이터 바인딩 프로세스는 GridView의 컨트롤 계층 구조, 즉 실제로 구축 단순히 `Table` 인스턴스 셀 컬렉션 이루어져 있으며 각 행의 컬렉션으로 구성 합니다. GridView s control 컬렉션에 포함 되어 특히를 `Table` 해당 루트에 있는 개체를 `GridViewRow` (에서 파생 된를 `TableRow` 클래스)의 각 레코드에 대 한를 `DataSource` GridView에 바인딩된 및 `TableCell` 개체의 각 `GridViewRow` 에서 각 데이터 필드에 대 한 인스턴스는 `DataSource`합니다.

각 정렬 그룹 간에 행 구분 기호를 추가 하려면 생성 된 후이 컨트롤 계층 구조를 직접 조작할 수 했습니다. GridView가의 컨트롤 계층 구조 페이지를 렌더링 하는 시간을 기준으로 마지막으로 생성 되어 있는지 확신할 수 있습니다. 따라서이 방법은 재정의 된 `Page` s 클래스 `Render` 메서드, 이때 GridView가 최종 컨트롤 계층 구조는 필요한 구분 기호 행을 포함 하도록 업데이트 됩니다. 그림 4에서는이 프로세스를 보여 줍니다.


[![또 다른 방법은 GridView가의 컨트롤 계층 구조를 조작합니다.](creating-a-customized-sorting-user-interface-vb/_static/image9.png)](creating-a-customized-sorting-user-interface-vb/_static/image8.png)

**그림 4**: GridView가의 컨트롤 계층 구조를 조작 하는 또 다른 방법은 ([큰 이미지를 보려면 클릭](creating-a-customized-sorting-user-interface-vb/_static/image10.png))


이 자습서에서는이 방식이 정렬 사용자 환경을 사용자 지정을 사용 하겠습니다.

> [!NOTE]
> 코드 I에 제공 된 예제 기반 m이이 자습서에 표시 [Teemu Keiski](http://aspadvice.com/blogs/joteke/default.aspx) s 블로그 [GridView 정렬 그룹화를 사용 하 여 비트를 재생](http://aspadvice.com/blogs/joteke/archive/2006/02/11/15130.aspx)합니다.


## <a name="step-3-adding-the-separator-rows-to-the-gridview-s-control-hierarchy"></a>3 단계: GridView가의 컨트롤 계층 구조에 구분 기호 행 추가

이 추가 끝 페이지 수명 주기의 하지만 실제 GridView c 하기 전에 수행 하고자 하는 해당 컨트롤 계층 구조 생성 되었으며 해당 페이지 방문에 마지막으로 만든 후 GridView가의 컨트롤 계층 구조에 구분 기호 행을 추가 하고자 하므로 HTML로 렌더링 된 제어 계층입니다. 최신 가능한 삽입할 수 있습니다이 위해 중요 한 점은 합니다 `Page` s 클래스 `Render` 이벤트는 다음 메서드 시그니처를 사용 하 여 코드 숨김 클래스에서 재정의할 수 있습니다.


[!code-vb[Main](creating-a-customized-sorting-user-interface-vb/samples/sample2.vb)]

경우는 `Page` 클래스의 원래 `Render` 메서드가 호출 되 `base.Render(writer)` 각 페이지에서 컨트롤의 렌더링 되는 해당 컨트롤 계층 구조에 따라 태그를 생성 합니다. 따라서 반드시 호출에서는 둘 다 `base.Render(writer)`페이지가 렌더링 되는 GridView s를 조작 했습니다 및 제어 호출 하기 전에 계층 `base.Render(writer)`행 구분 기호 앞 GridView가의 컨트롤 계층 구조에 추가 된 있도록 s 된 렌더링 합니다.

정렬 그룹 헤더를 삽입 하려면 먼저 데이터를 정렬는 사용자가 요청을 확인 해야 합니다. 기본적으로 GridView의 내용을 정렬 되지 않습니다 하 고 따라서 헤더를 정렬 하는 모든 그룹을 입력 해야 하는 t를 하지 것입니다.

> [!NOTE]
> 페이지가 처음 로드 될 때 특정 열으로 정렬할 GridView를 하려는 경우 호출 GridView의 `Sort` 페이지를 처음 방문할 (있지만 후속 포스트백에 없는) 메서드. 이를 위해이 호출을 추가 합니다 `Page_Load` 내에서 이벤트 처리기는 `if (!Page.IsPostBack)` 조건부입니다. 다시 참조를 [페이징 및 정렬 보고서 데이터](paging-and-sorting-report-data-vb.md) 대 한 자세한 내용은 자습서 정보는 `Sort` 메서드.


가정 하 고 정렬 된 데이터에는 다음 작업은 어떤 열을 확인 하 고으로 데이터를 정렬 하 고 값을 해당 열의 s 차이 찾을 행을 검색 합니다. 다음 코드는 데이터 정렬 되었는지 하는 데이터 정렬 된 열을 찾습니다 보장 합니다.


[!code-vb[Main](creating-a-customized-sorting-user-interface-vb/samples/sample3.vb)]

GridView에 아직 되도록 정렬 GridView의 `SortExpression` 속성이 설정 되지 것입니다. 따라서 하고자이 속성에 값이 일부 경우 구분 기호 행을 추가 합니다. 이 경우 다음는 데이터 정렬 된 열의 인덱스를 확인 해야 합니다. GridView가 반복 하 여 이렇게 `Columns` 컬렉션을 갖는 열에 대 한 검색 `SortExpression` 속성이 같으면 GridView의 `SortExpression` 속성입니다. S 열 인덱스 외에도 것도 가져오기는 `HeaderText` 구분 기호 행을 표시할 때 사용 되는 속성입니다.

데이터가 정렬 되는 열의 인덱스를 사용 하 여 GridView의 행을 열거 하는 최종 단계가입니다. 각 행에 대 한 정렬 된 열의 값을 이전 행 정렬 s 열의 값에서 다른 지 여부를 결정 해야 합니다. 따라서 새 삽입 해야 하는 경우 `GridViewRow` 컨트롤 계층 구조에는 인스턴스. 이 작업은 다음 코드를 사용 하 여 수행 됩니다.


[!code-vb[Main](creating-a-customized-sorting-user-interface-vb/samples/sample4.vb)]

프로그래밍 방식으로 참조 하 여이 코드가 시작 되는 `Table` 이라는 문자열 변수를 만들고 GridView가의 컨트롤 계층 구조의 루트에 있는 개체 `lastValue`합니다. `lastValue` 이전 행의 값을 사용 하 여 현재 행으로 정렬 하는 s 열 값과 비교 하는 데 사용 됩니다. 다음으로 GridView s `Rows` 컬렉션이 열거 되 고 각 행에 대 한 정렬 된 열의 값에 저장 됩니다는 `currentValue` 변수입니다.

> [!NOTE]
> S 셀의 특정 행의 정렬 열 값을 결정 하려면 사용 `Text` 속성입니다. 이 적합 BoundFields, 및 제외는 TemplateFields, CheckBoxFields 원하는 대로 작동 하 고 등. 곧 대체 GridView 필드를 고려 하는 방법을 살펴보겠습니다.


합니다 `currentValue` 및 `lastValue` 변수 그런 다음 비교 됩니다. 다를 경우 컨트롤 계층 구조에 새 구분 기호 행을 추가 해야 합니다. 인덱스를 확인 하 여 이렇게를 `GridViewRow` 에 `Table` s 개체 `Rows` 컬렉션, 새로 만들기 `GridViewRow` 및 `TableCell` 인스턴스 및 추가 합니다 `TableCell` 및 `GridViewRow` 를 컨트롤 계층 구조입니다.

구분 기호 s 유일한 행는 참고 `TableCell` GridView의 전체 너비를 확장 되도록 형식이 사용 하 여 형식이 합니다 `SortHeaderRowStyle` CSS 클래스 있고 해당 `Text` 속성 모두 정렬 그룹을 보여 주는 같은 이름 (예: 범주) 및 그룹 s (예: 음료) 값입니다. 마지막으로, `lastValue` 의 값으로 업데이트 됩니다 `currentValue`합니다.

정렬 그룹 머리글 행의 서식을 지정 하는 데 사용 되는 CSS 클래스 `SortHeaderRowStyle` 에 지정할 필요는 `Styles.css` 파일입니다. 자유롭게 사용 하 여 어떤 스타일 설정을 매력적입니다. 다음 사용 합니다.


[!code-css[Main](creating-a-customized-sorting-user-interface-vb/samples/sample5.css)]

현재 코드를 사용 하 여 정렬 인터페이스 정렬 그룹 헤더 추가 모든 BoundField에서 정렬 하는 경우 (공급 업체에서 정렬할 때 스크린 샷을 보여 주는 그림 5 참조). 그러나 다른 필드 형식 (예: CheckBoxField 또는 TemplateField)에서 정렬할 때 정렬 그룹 헤더 (그림 6 참조)를 찾을 수를 반환할 대상이 없습니다 됩니다.


[![정렬 인터페이스 BoundFields에서 정렬할 때 정렬 그룹 머리글 포함](creating-a-customized-sorting-user-interface-vb/_static/image12.png)](creating-a-customized-sorting-user-interface-vb/_static/image11.png)

**그림 5**: The 정렬 인터페이스 포함 정렬 그룹 헤더 때 기준으로 정렬 BoundFields ([큰 이미지를 보려면 클릭](creating-a-customized-sorting-user-interface-vb/_static/image13.png))


[![누락 된 경우 정렬 된 CheckBoxField 정렬 그룹 헤더는](creating-a-customized-sorting-user-interface-vb/_static/image15.png)](creating-a-customized-sorting-user-interface-vb/_static/image14.png)

**그림 6**: 누락 된 경우 정렬 된 CheckBoxField The 정렬 그룹 헤더는 ([큰 이미지를 보려면 클릭](creating-a-customized-sorting-user-interface-vb/_static/image16.png))


CheckBoxField에서 정렬할 때 정렬 그룹 머리글이 없는 이유는 현재 사용 하므로 방금 합니다 `TableCell` s `Text` 각 행에 대 한 정렬 된 열의 값을 확인 하는 속성입니다. CheckBoxFields에 대 한 합니다 `TableCell` s `Text` 속성은 빈 문자열은 대신 값이 상주 하는 확인란을 웹 컨트롤을 통해 사용할 수는 `TableCell` s `Controls` 컬렉션입니다.

BoundFields 이외의 형식 필드를 처리 하려면 코드를 보강 해야 위치는 `currentValue` 변수가 할당 된에 있는 확인란의 존재 여부를 확인 합니다 `TableCell` s `Controls` 컬렉션. 사용 하는 대신 `currentValue = gvr.Cells(sortColumnIndex).Text`,이 코드를 다음으로 바꿉니다.


[!code-vb[Main](creating-a-customized-sorting-user-interface-vb/samples/sample6.vb)]

이 코드는 정렬 된 열을 검사 `TableCell` 모든 컨트롤에 있는지 확인 하는 현재 행의 `Controls` 컬렉션입니다. 가 되어 첫 번째 컨트롤을 확인란을 선택 합니다 `currentValue` 변수는 예 또는 아니요, 확인란 s에 따라 설정 됩니다 `Checked` 속성. 값을 가져옵니다 그러지 합니다 `TableCell` s `Text` 속성입니다. GridView에 있을 수 있는 모든 TemplateFields 정렬 처리 하려면이 논리를 복제할 수 있습니다.

위의 코드를 추가 정렬 그룹 머리글이 있는 이제 지원 되지 않는 CheckBoxField에서 정렬 하는 경우 (그림 7 참조).


[![정렬 그룹 헤더는 이제 있는 경우 정렬 된 CheckBoxField](creating-a-customized-sorting-user-interface-vb/_static/image18.png)](creating-a-customized-sorting-user-interface-vb/_static/image17.png)

**그림 7**: The 정렬 그룹 헤더는 이제 있는 경우 정렬 된 CheckBoxField ([큰 이미지를 보려면 클릭](creating-a-customized-sorting-user-interface-vb/_static/image19.png))


> [!NOTE]
> 제품과 있다면 `NULL` 데이터베이스에 대 한 값을 `CategoryID`, `SupplierID`, 또는 `UnitPrice` 필드를 해당 값으로 표시 됩니다 GridView에서 빈 문자열만 를사용하여해당제품에대한구분기호행의텍스트즉기본적으로`NULL`범주와 같은 값을 읽이 됩니다: (있습니다 s, 범주 뒤에 없는 이름을: 범주와 마찬가지로: 음료). 여기에 표시 된 값을 원하는 경우를 설정할 수 있습니다는 BoundFields [ `NullDisplayText` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.boundfield.nulldisplaytext.aspx) 텍스트에 표시 하려는 하거나 할당할 때 렌더링 메서드의 조건문을 추가할 수 있습니다는 `currentValue` 구분 기호를 행의 `Text` 속성입니다.


## <a name="summary"></a>요약

GridView에는 정렬 인터페이스 사용자 지정에 대 한 많은 기본 제공 옵션이 포함 되지 않습니다. 그러나 하위 수준 코드의 비트를 사용 하 여이 사용자 지정된 인터페이스를 만드는 GridView가의 컨트롤 계층 구조를 조정 하 합니다. 이 자습서에서는 더 쉽게 개별 그룹 및 해당 그룹 경계를 식별 하는 정렬 가능한 GridView에 대 한 정렬 그룹 구분 기호 행을 추가 하는 방법에 살펴보았습니다. 사용자 지정된 정렬 인터페이스의 추가 예제를 체크 아웃 [Scott Guthrie](https://weblogs.asp.net/scottgu/) s [소수의 ASP.NET 2.0 GridView 정렬 팁과 요령](https://weblogs.asp.net/scottgu/archive/2006/02/11/437995.aspx) 블로그 항목입니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [이전](sorting-custom-paged-data-vb.md)
