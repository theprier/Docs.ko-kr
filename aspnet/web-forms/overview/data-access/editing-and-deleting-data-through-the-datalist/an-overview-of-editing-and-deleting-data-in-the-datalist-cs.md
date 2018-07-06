---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-cs
title: DataList (C#)에서 데이터 편집 및 삭제의 개요 | Microsoft Docs
author: rick-anderson
description: DataList에서 기본 제공 편집 및 삭제 기능에 없는 동안이 자습서에서는 살펴보겠습니다 편집 및 삭제 o 지 DataList를 만드는 방법...
ms.author: aspnetcontent
ms.date: 10/30/2006
ms.assetid: c3b0c86e-fe98-41ee-b26f-ca38cddaa75e
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-cs
msc.type: authoredcontent
ms.openlocfilehash: a9be3e332ec19f78c4dcc2e78d3dd4609c27fddf
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37810487"
---
<a name="an-overview-of-editing-and-deleting-data-in-the-datalist-c"></a>DataList (C#)에서 데이터 편집 및 삭제의 개요
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_36_CS.exe) 또는 [PDF 다운로드](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/datatutorial36cs1.pdf)

> DataList에서 기본 제공 편집 및 삭제 기능에 없는 동안이 자습서에서는 살펴보겠습니다 편집 및 해당 기본 데이터의 삭제를 지 원하는 DataList를 만드는 방법.


## <a name="introduction"></a>소개

에 [An 개요의 삽입, 업데이트 및 삭제 데이터](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) 삽입, 업데이트 및 응용 프로그램 아키텍처, ObjectDataSource에 GridView, DetailsView 및 FormView 사용 하 여 데이터를 삭제 하는 방법에 살펴보았습니다 자습서 컨트롤입니다. ObjectDataSource와 이러한 세 개의 데이터 웹 컨트롤을 사용 하면 단순 데이터 수정 인터페이스를 구현 간단히 되었으며 단순히 타이머에서 틱 스마트 태그에서 확인란을 포함 합니다. 코드를 쓸 필요가 없습니다.

아쉽게도 DataList 편집 및 삭제 기능 GridView 컨트롤의 기본 제공에 부족 합니다. 선언적 데이터 소스 컨트롤 및 코드가 없는 데이터 수정 페이지를 사용할 수 없었던 경우 DataList ASP.NET의 이전 버전에서 relic는 사실이 부분적으로이 누락 된 기능. DataList ASP.NET 2.0에서 제공 하지 않습니다 기본적으로 동일한 데이터 수정 기능 GridView로, 하는 동안에 이러한 기능을 포함 하도록 ASP.NET 1.x 기법을 사용할 수 있습니다. 이 이렇게 약간의 코드를 이어야 하는데,이 자습서에서 살펴보겠지만 DataList의 일부 이벤트 및 속성이이 프로세스에 도움이 되는 위치에 있습니다.

이 자습서를 편집 하 고 해당 기본 데이터의 삭제를 지 원하는 DataList를 만드는 방법을 살펴보겠습니다. 이후 자습서에서는 고급 편집 및 삭제 시나리오, 입력된 필드 유효성 검사를 포함 하 여, 데이터 액세스 또는 비즈니스 논리 계층 및 등에서 발생 하는 예외를 정상적으로 처리를 검사 합니다.

> [!NOTE]
> 같은 DataList, Repeater 컨트롤에 삽입, 업데이트 또는 삭제에 대 한 상자 기능 부족을 부족 합니다. 이러한 기능을 추가할 수 있습니다, 있지만 DataList 속성 및 이러한 기능을 추가 하는 단순화 하는 반복기에서 찾을 수 없는 이벤트에도 포함 되어 있습니다. 따라서이 자습서 및 앞으로 편집 및 삭제에 보이는 중점적으로 엄격 하 게 DataList 합니다.


## <a name="step-1-creating-the-editing-and-deleting-tutorials-web-pages"></a>1 단계: 편집 및 삭제 자습서 웹 페이지 만들기

업데이트 하 고 DataList에서 데이터를 삭제 하는 방법을 탐색을 시작 하기 전에 s를 먼저 시간을 내어이 자습서에는 다음 몇 가지 작업 해야 하는 웹 사이트 프로젝트에서 ASP.NET 페이지를 만들 수 있습니다. 라는 새 폴더를 추가 하 여 시작 `EditDeleteDataList`합니다. 다음에 있는 각 페이지에 연결할 수 있도록 해당 폴더에 다음 ASP.NET 페이지를 추가 합니다 `Site.master` 마스터 페이지:

- `Default.aspx`
- `Basics.aspx`
- `BatchUpdate.aspx`
- `ErrorHandling.aspx`
- `UIValidation.aspx`
- `CustomizedUI.aspx`
- `OptimisticConcurrency.aspx`
- `ConfirmationOnDelete.aspx`
- `UserLevelAccess.aspx`


![이 자습서에 대 한 ASP.NET 페이지 추가](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image1.png)

**그림 1**:이 자습서에 대 한 ASP.NET 페이지 추가


다른 폴더와 같이 `Default.aspx` 에 `EditDeleteDataList` 폴더 섹션의 자습서를 나열 합니다. 이전에 설명한 대로 `SectionLevelTutorialListing.ascx` 사용자 컨트롤은이 기능을 제공 합니다. 따라서이 사용자 정의 컨트롤을 추가 `Default.aspx`의 디자인 뷰에서 페이지의 솔루션 탐색기에서 끌어 합니다.


[![Default.aspx SectionLevelTutorialListing.ascx 사용자 컨트롤 추가](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image3.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image2.png)

**그림 2**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 `Default.aspx` ([클릭 하 여 큰 이미지 보기](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image4.png))


마지막으로, 페이지에 항목으로 추가 된 `Web.sitemap` 파일입니다. 특히, DataList 및 반복기를 사용 하 여 마스터/세부 정보 보고서 후 다음 태그를 추가 `<siteMapNode>`:


[!code-xml[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample1.xml)]

업데이트 한 후 `Web.sitemap`, 잠시 브라우저를 통해 자습서 웹 사이트를 확인 합니다. 이제 왼쪽에 있는 메뉴 DataList 편집 및 삭제 자습서에 대 한 항목이 포함 됩니다.


![이제 사이트 맵 DataList 편집 및 삭제 자습서에 대 한 항목을 포함](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image5.png)

**그림 3**: 이제 사이트 맵 DataList 편집 및 삭제 자습서에 대 한 항목을 포함


## <a name="step-2-examining-techniques-for-updating-and-deleting-data"></a>2 단계: 데이터 업데이트 및 삭제에 대 한 기술을 검토

편집 및 GridView 사용 하 여 데이터를 삭제 하는 중 이므로 쉽지 내부적으로 GridView 및 ObjectDataSource는 동시에 적용 합니다. 에 설명 된 대로 합니다 [삽입, 업데이트 및 삭제와 관련 된 이벤트 검사](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs.md) 자습서에서는 행의 업데이트 단추를 클릭할 때 GridView 합니다 에양방향데이터바인딩은해당필드가자동으로할당`UpdateParameters` 해당 ObjectDataSource의 컬렉션 ObjectDataSource s 호출 `Update()` 메서드.

유감 스럽게도, DataList이 기본 제공 기능을 제공 하지 않습니다. ObjectDataSource s 매개 변수를 지정 하 고는 사용자가의 값을 할당 되어 있는지 확인 해야 하는 것이 해당 `Update()` 메서드가 호출 됩니다. 이러한 노력에 우리를 돕기 위해, DataList에는 다음 속성 및 이벤트를 제공 합니다.

- **합니다 [ `DataKeyField` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basedatalist.datakeyfield.aspx)**  DataList에서 각 항목을 고유 하 게 식별 하는 일을 할 수를 업데이트 하거나 삭제할 때 필요 합니다. 표시 된 데이터의 기본 키 필드에이 속성을 설정 합니다. DataList s 이렇게 채워집니다 [ `DataKeys` 컬렉션](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basedatalist.datakeys.aspx) 지정 된 `DataKeyField` 각 DataList 항목에 대 한 값입니다.
- **[ `EditCommand` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.editcommand.aspx)**  단추나 LinkButton, imagebutton이 될 때 발생 인 `CommandName` 속성 편집을 클릭 합니다.
- **합니다 [ `CancelCommand` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.cancelcommand.aspx)**  단추나 LinkButton, imagebutton이 될 때 발생 인 `CommandName` 속성 취소 클릭 합니다.
- **합니다 [ `UpdateCommand` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.updatecommand.aspx)**  단추나 LinkButton, imagebutton이 될 때 발생 인 `CommandName` 속성 업데이트를 클릭 합니다.
- **합니다 [ `DeleteCommand` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.deletecommand.aspx)**  단추나 LinkButton, imagebutton이 될 때 발생 인 `CommandName` 속성이 삭제를 클릭 합니다.

이러한 속성 및 이벤트를 사용 하는 DataList에서 데이터를 삭제 및 업데이트를 사용할 수 있습니다 하는 네 가지가 있습니다.

1. **ASP.NET 1.x 기술을 사용 하 여** DataList ASP.NET 2.0 및 ObjectDataSources 하기 전의 및 프로그래밍 방법을 통해 완전히 데이터를 업데이트 및 삭제할 수 있었습니다. 이 기술은 완전히 ObjectDataSource ditches 하며 우리는 데이터를 바인딩 DataList 둘 다에서 표시할 데이터를 검색 하는 비즈니스 논리 계층에서 직접 업데이트 하거나 레코드를 삭제 하는 경우.
2. **선택, 업데이트 및 삭제에 대 한 페이지에 있는 단일 ObjectDataSource 컨트롤을 사용 하 여** DataList GridView s 내재 된 편집 및 삭제 기능에 없는 동안 있는 s t 수 없는 이유에 추가할 직접. 이 방법을 사용 하 여 GridView 예제에서는 마찬가지로 ObjectDataSource를 사용 했습니다 있지만를 DataList s에 대 한 이벤트 처리기를 만들어야 `UpdateCommand` ObjectDataSource s 매개 변수 및 호출을 설정한 이벤트 해당 `Update()` 메서드.
3. **ObjectDataSource 컨트롤을 사용 하 여 선택, 하지만 업데이트 및 삭제 직접에 대해 the BLL에 대 한** 약간의 코드를 작성 하려고 하는 옵션 2를 사용 하는 경우는 `UpdateCommand` 이벤트 등에 매개 변수 값을 할당 합니다. 대신 ObjectDataSource를 사용 하 여, 선택 계속 있지만 BLL (예: 옵션 1)에 대해 직접 업데이트 및 삭제 하는 중 호출할 수 했습니다. ObjectDataSource가 할당 보다 좀 더 읽기 쉬운 코드가 개인적으로 BLL와 직접 상호 작용을 통해 데이터를 업데이트 하면 `UpdateParameters` 호출 및 해당 `Update()` 메서드.
4. **여러 ObjectDataSources 통해 선언적 수단을 사용 하 여** 이전 세 가지 방법을 모두 약간의 코드를 필요 합니다. D 있습니다 대신을 계속 사용 가능한 훨씬 선언적 구문으로 하는 경우 마지막 옵션이 페이지의 여러 ObjectDataSources를 포함 하는 것입니다. 첫 번째 ObjectDataSource BLL에서 데이터를 검색 하 고 DataList에 바인딩합니다. 다른 ObjectDataSource 업데이트에 대 한 추가 되지만 DataList s 내에서 직접 추가 `EditItemTemplate`합니다. 지원 삭제를 포함 하려면 아직 다른 ObjectDataSource은에 필요 합니다 `ItemTemplate`합니다. ObjectDataSource가 사용 하 여 포함 된 이러한 이러한 방식의 `ControlParameters` 사용자 입력된 컨트롤에 ObjectDataSource s 매개 변수를 선언적으로 바인딩할 (s DataList에서 프로그래밍 방식으로 지정 하는 대신 `UpdateCommand` 이벤트 처리기). 이 이렇게 약간의 포함 된 ObjectDataSource s를 호출 해야 하는 코드를를 여전히 필요 `Update()` 또는 `Delete()` 서로 세 가지 방법 보다 작은 명령 수 있지만 훨씬 필요 합니다. 여기 단점은 여러 ObjectDataSources 수행 매몰 페이지 전체 가독성이 떨어뜨리지입니다.

만 이러한 방법 중 하나를 사용 하도록 강제 적용 하는 경우 I d 이므로 DataList 원래이 패턴에 맞게 설계 된 최고의 유연성을 제공 하기 때문에 옵션 1 선택 합니다. DataList ASP.NET 2.0 데이터 소스 컨트롤을 사용 하 여 작업할 수 있도록 확장 되었습니다, 하는 동안이 없거나 확장 지점은 모든 공식 ASP.NET 2.0 데이터 웹 컨트롤 (GridView, DetailsView 및 FormView)의 기능입니다. 옵션 2-4 않습니다를 요구 하지 않고 있지만.

이 향후 편집 및 삭제 하는 자습서 중 사용 하 여 ObjectDataSource 데이터 검색에 표시 하 고 데이터 (옵션 3) 업데이트 및 삭제 하는 BLL에 대 한 호출을 직접.

## <a name="step-3-adding-the-datalist-and-configuring-its-objectdatasource"></a>DataList를 추가 하 고 해당 ObjectDataSource를 구성 하는 3 단계:

이 자습서에서는 제품 정보를 나열 하 고 각 제품에 대 한 사용자는 기능을 제공 이름과 가격을 편집 하 고 제품을 모두 삭제 하는 DataList를 만들겠습니다. 특히 ObjectDataSource를 사용 하 여 표시할 레코드를 검색 하지만 업데이트를 수행 하 고 BLL와 직접 상호 작용을 통해 작업을 삭제 합니다. DataList의 편집 및 삭제 기능을 구현 하는 방법에 대 한 걱정 했습니다 전에 s를 먼저 제품을 읽기 전용 인터페이스에 표시할 페이지를 가져올 수 있습니다. 이후로 ve 검사이 단계 이전 자습서에서는 하겠지만 통해 신속 하 게 합니다.

열어서 시작 합니다 `Basics.aspx` 페이지는 `EditDeleteDataList` 폴더 디자인 뷰에서 페이지 DataList를 추가 및 합니다. 다음으로 DataList s 스마트 태그에서 새 ObjectDataSource를 만듭니다. 제품 데이터를 사용 하 여 작업을 하 고 있으므로 사용 하도록 구성 된 `ProductsBLL` 클래스입니다. 검색할 *모든* 제품을 선택 합니다 `GetProducts()` 메서드 선택 탭에서 합니다.


[![ProductsBLL 클래스를 사용 하는 ObjectDataSource 구성](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image7.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image6.png)

**그림 4**: ObjectDataSource 사용 하도록 구성 된 `ProductsBLL` 클래스 ([클릭 하 여 큰 이미지 보기](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image8.png))


[![GetProducts() 메서드를 사용 하 여 제품 정보를 반환 합니다.](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image10.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image9.png)

**그림 5**: 사용 하 여 제품 정보를 반환 합니다 `GetProducts()` 메서드 ([클릭 하 여 큰 이미지 보기](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image11.png))


새 데이터를 삽입 하기 위한 GridView와 같은 DataList이 못합니다. 따라서 선택 삽입 탭에서 드롭 다운 목록에서 옵션 (없음). 또한 업데이트 하므로 UPDATE 및 DELETE 탭에 선택한 (없음) 및 삭제 BLL을 통해 프로그래밍 방식으로 수행 됩니다.


[![드롭 다운 목록 ObjectDataSource가의 삽입, 업데이트 및 삭제 하는 탭 (없음)으로 설정 되어 있는지 확인 합니다.](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image13.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image12.png)

**그림 6**: ObjectDataSource가의 삽입, 업데이트 및 삭제 하는 탭의 드롭다운 목록 (None)으로 설정 되어 있는지 확인 ([큰 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image14.png))


ObjectDataSource를 구성한 후 디자이너를 반환 합니다. 마침을 클릭 합니다. Ve ObjectDataSource 구성에 Visual Studio를 자동으로 완료 한 경우 이전 예제에서 볼 때 만듭니다는 `ItemTemplate` DropDownList에 대 한 각 데이터 필드를 표시 합니다. 대체 `ItemTemplate`의 제품 이름과 가격을 표시 하는 하나를 사용 하 여 합니다. 또한 설정 된 `RepeatColumns` 속성을 2로 합니다.

> [!NOTE]
> 에 설명 된 대로 합니다 *개요의 삽입, 업데이트 및 데이터 삭제* 자습서에서는 아키텍처는 제거 해야 하는 ObjectDataSource를 사용 하 여 데이터를 수정 하는 경우는 `OldValuesParameterFormatString` ObjectDataSource의 속성 선언적 태그 (또는 해당 기본값으로 다시 `{0}`). 그러나이 자습서에서는에 사용 중인 ObjectDataSource만 데이터를 검색 합니다. ObjectDataSource s 수정할 필요가 없습니다 따라서 `OldValuesParameterFormatString` 속성 값 (하지만 해당 대상이 t 이렇게 저하).


기본 DataList를 바꾼 후 `ItemTemplate` 을 사용자 지정 된 것으로 선언적 태그 페이지에서 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample2.aspx)]

시간을 내어 브라우저를 통해 진행 상황을 확인 합니다. 그림 7에서 알 수 있듯이, DataList 두 열에 각 제품에 대 한 제품 이름과 단위 가격을 표시 합니다.


[![제품 이름 및 가격과 2 열 DataList에 표시 됩니다.](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image16.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image15.png)

**그림 7**:의 제품 이름 및 가격과 2 열 DataList에 표시 됩니다 ([큰 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image17.png))


> [!NOTE]
> DataList 많은 업데이트 및 삭제 프로세스에 필요한 속성이 있으며 이러한 값은 뷰 상태에 저장 됩니다. 따라서는 DataList를 구축을 지 원하는 편집 하거나 데이터를 삭제 하는 경우 반드시 DataList의 뷰 상태를 사용할 수 있습니다.  
>   
>  예리한 독자는 편집 가능한 Gridview, DetailsViews를, FormViews 만들 때 뷰 상태를 사용 하지 않도록 설정할 수 있었습니다 기억할 것입니다. 이 ASP.NET 2.0 웹 컨트롤을 포함할 수 있으므로 *상태를 제어*는 보기 상태와 비슷하지만 필수 것으로 간주 되는 포스트백 간에 상태가 유지 됩니다.


단순히 trivial 상태 정보를 생략 되지만 컨트롤 상태를 포함 하는 편집 및 삭제 하는 데 필요한 상태를 유지 관리 GridView에서 상태 보기를 사용 하지 않도록 설정 합니다. ASP.NET 1.x 기간에서 만든 것, DataList 컨트롤 상태를 사용 하지 않습니다 하며 사용 하도록 설정 하는 보기 상태 이므로 있어야 합니다. 참조 [컨트롤 상태 vs. 뷰 상태](https://msdn.microsoft.com/library/1whwt1k7.aspx) 컨트롤 상태와 뷰 상태에서 어떻게 다른의 목적에 대 한 자세한 내용은 합니다.

## <a name="step-4-adding-an-editing-user-interface"></a>4 단계: 편집 사용자 인터페이스를 추가합니다.

GridView 컨트롤은 필드 (BoundFields, CheckBoxFields, TemplateFields, 및 등)의 컬렉션으로 구성 됩니다. 이러한 필드는 해당 모드에 따라 렌더링 된 태그를 조정할 수 있습니다. 예를 들어, 읽기 전용 모드에 있을 때을 BoundField 해당 데이터 필드 값을 텍스트로 표시; TextBox 웹 편집 모드에 있을 때 렌더링 컨트롤 `Text` 속성 데이터 필드 값이 할당 됩니다.

반면, DataList, 템플릿을 사용 하 여 해당 항목을 렌더링 합니다. 사용 하 여 읽기 전용 항목 렌더링 되는 `ItemTemplate` 편집 모드에서 항목을 통해 렌더링 되는 반면는 `EditItemTemplate`합니다. 이 시점에서 우리의 DataList에는 `ItemTemplate`합니다. 추가 해야 하는 항목 수준 편집 기능을 지 원하는 `EditItemTemplate` 편집할 수 있는 항목에 대해 표시할 태그를 포함 하는 합니다. 이 자습서에서는 s 제품 이름과 단위 가격이 편집을 위해 텍스트 웹 컨트롤 사용 하겠습니다.

`EditItemTemplate` (템플릿 편집 옵션을 선택 하면 DataList s 스마트 태그에서)에서 선언적으로 또는 디자이너를 통해 만들 수 있습니다. 템플릿 편집 옵션을 사용 하려면 먼저 스마트 태그에 있는 템플릿 편집 링크를 클릭 한 다음 선택 된 `EditItemTemplate` 드롭 다운 목록에서 항목입니다.


[![DataList의 EditItemTemplate 사용 하도록 선택](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image19.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image18.png)

**그림 8**: s DataList와 함께 작업 하도록 선택할 `EditItemTemplate` ([클릭 하 여 큰 이미지 보기](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image20.png))


그런 다음 제품 이름에을 입력: 및 가격: 두 TextBox 컨트롤에 도구 상자에서 끌어와서는 `EditItemTemplate` 디자이너 인터페이스. 설정 된 텍스트 상자 `ID` 속성을 `ProductName` 고 `UnitPrice`입니다.


[![제품의 이름 및 가격에 대 한 입력란을 추가 합니다.](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image22.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image21.png)

**그림 9**: 이름이 제품에 대 한 텍스트 상자 및 가격 추가 ([큰 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image23.png))


해당 제품 데이터 필드 값을 바인딩해야 합니다 `Text` 두 텍스트 상자 속성입니다. 텍스트 상자 스마트 태그에서 데이터 바인딩 편집 링크를 클릭 하 고 사용 하 여 적절 한 데이터 필드에 연결 하 여는 `Text` 그림 10에 표시 된 속성입니다.

> [!NOTE]
> 바인딩할 때 합니다 `UnitPrice` TextBox의 가격에 데이터 필드 `Text` 필드에 서식을 지정할 수 있습니다이 통화 값으로 (`{0:C}`)는 일반 숫자가 (`{0:N}`), 하거나 형식이 지정 되지 않은 상태로 둡니다.


![ProductName 및 UnitPrice 데이터 필드를 입력란의 텍스트 속성에 바인딩](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image24.png)

**그림 10**: 바인딩 합니다 `ProductName` 하 고 `UnitPrice` 데이터 필드를 `Text` 입력란의 속성


그림 10의 데이터 바인딩 편집 대화 상자는 어떻게 알 수 있습니다 *되지* GridView 또는 DetailsView를 TemplateField 또는 FormView 템플릿을 편집할 때 존재 하는 양방향 데이터 바인딩 확인란을 포함 합니다. 양방향 데이터 바인딩 기능을 자동으로 해당 ObjectDataSource s에 할당할 입력된 된 웹 컨트롤에 입력 한 값을 허용 `InsertParameters` 또는 `UpdateParameters` 삽입 되거나 데이터를 업데이트 합니다. 앞으로 살펴보겠지만 나중에이 자습서는 사용자가 변경 되 고 데이터를 업데이트할 준비가 되었음을 만듭니다 후 DataList 양방향 데이터 바인딩을 지원 하지 않습니다, 프로그래밍 방식으로 이러한 텍스트 상자에 액세스 해야 `Text` 속성과 해당 값을 전달 합니다 적절 한 `UpdateProduct` 의 메서드는 `ProductsBLL` 클래스입니다.

마지막으로 업데이트를 추가 해야 하 고 단추를 취소 합니다 `EditItemTemplate`합니다. 설명한 것 처럼를 [마스터/세부 정보 DataList와 함께 a 글머리 기호 목록의 마스터 레코드를 사용 하 여 세부 정보](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md) 자습서에서는 단추나 LinkButton, ImageButton 때 해당 `CommandName` 속성을 설정 또는 DataList, Repeater 내에서 클릭할를 DataList 또는 repeater s `ItemCommand` 이벤트가 발생 합니다. DataList에 대 한 경우는 `CommandName` 속성을 특정 값으로 설정 하면 추가적인 이벤트 에서도 발생할 수 있습니다. 특수 한 `CommandName` 다른 속성 값에 포함 합니다.

- 취소를 발생 시킵니다는 `CancelCommand` 이벤트
- 발생을 편집 합니다 `EditCommand` 이벤트
- 발생 업데이트는 `UpdateCommand` 이벤트

이러한 이벤트가 발생 하는 점을 염두 *외에* 는 `ItemCommand` 이벤트입니다.

에 추가 합니다 `EditItemTemplate` 두 개의 단추 웹 컨트롤을 하나입니다 `CommandName` 업데이트 및 다른 s 취소로 설정 됩니다. 이러한 두 단추 웹 컨트롤을 추가한 후 디자이너 다음과 비슷하게 표시 됩니다.


[![업데이트를 추가 하 고 단추는 EditItemTemplate 취소](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image26.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image25.png)

**그림 11**: 추가 업데이트 및 취소 단추를 `EditItemTemplate` ([클릭 하 여 큰 이미지 보기](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image27.png))


사용 하 여는 `EditItemTemplate` 전체 DataList s 선언적 태그 비슷합니다 다음:


[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample3.aspx)]

## <a name="step-5-adding-the-plumbing-to-enter-edit-mode"></a>5 단계: 추가 편집 모드로 전환 하는 데 필요한 기본

이 시점에서 우리의 DataList 인터페이스가 편집을 통해 정의 된 해당 `EditItemTemplate`하지만 여기가 현재 페이지를 방문 하는 사용자에 대 한 점을 나타낼 방법이 없기 s 제품 정보를 편집 하고자 합니다. 편집 단추,를 클릭 하면 렌더링 해당 DataList 항목 편집 모드에서 각 제품에 추가 해야 합니다. 편집 단추에 추가 하 여 시작 된 `ItemTemplate`를 선언적으로 또는 디자이너를 통해. S 편집 단추를 설정 하도록 `CommandName` 속성을 편집 합니다.

이 편집 단추를 추가한 후 잠시 브라우저를 통해 페이지를 봅니다. 이 또한이를 사용 하 여 각 제품 목록을 편집 단추를 포함 해야 합니다.


[![업데이트를 추가 하 고 단추는 EditItemTemplate 취소](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image29.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image28.png)

**그림 12**: 추가 업데이트 및 취소 단추를 `EditItemTemplate` ([클릭 하 여 큰 이미지 보기](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image30.png))


단추를 클릭 하면 포스트백, 않지만 *되지* 목록을 편집 모드에 제품을 제공 합니다. 하려면 제품을 편집할 수 있도록 해야 합니다.

1. DataList s 설정 [ `EditItemIndex` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx) 의 인덱스에는 `DataListItem` 있는 편집 단추를 클릭 한 것입니다.
2. DataList 데이터를 다시 바인딩해야 합니다. DataList는 다시 렌더링 하는 경우는 `DataListItem` 해당 `ItemIndex` s DataList와 함께 해당 `EditItemIndex` 사용 하 여 렌더링 됩니다 해당 `EditItemTemplate`합니다.

DataList s 이후 `EditCommand` 이벤트 편집 단추를 클릭할 때 발생을 만듭니다는 `EditCommand` 이벤트 처리기를 다음 코드로 바꿉니다.


[!code-csharp[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample4.cs)]

`EditCommand` 형식의 개체에 이벤트 처리기가 전달 `DataListCommandEventArgs` 에 대 한 참조를 포함 하는 두 번째 입력된 매개 변수로 합니다 `DataListItem` 인 편집 단추를 클릭 한 (`e.Item`). DataList s를 먼저 설정 하는 이벤트 처리기 `EditItemIndex` 에 `ItemIndex` 의 편집 가능한 `DataListItem` 다음 s DataList를 호출 하 여 데이터 DataList 다시 바인딩합니다 `DataBind()` 메서드.

이 이벤트 처리기를 추가한 후 브라우저에서 페이지를 다시 확인 합니다. 클릭 한 제품 편집 가능한 (그림 13 참조)를 사용 하면 이제 편집 단추를 클릭 합니다.


[![편집 단추는 편집 가능한 제품을 클릭 하면](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image32.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image31.png)

**그림 13**: 제품 편집 가능 하면 [편집] 단추 ([큰 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image33.png))


## <a name="step-6-saving-the-user-s-changes"></a>6 단계: 사용자가 변경 내용을 저장

이 시점에서; 아무 작업도 수행 하지 편집된 제품의 업데이트 또는 취소 단추를 클릭 합니다. DataList s에 대 한 이벤트 처리기를 생성 해야이 기능을 추가할 `UpdateCommand` 고 `CancelCommand` 이벤트입니다. 만들어 시작 합니다 `CancelCommand` 편집된 제품의 취소 단추를 클릭 하 고 DataList 미리 편집 상태로 반환을 담당 하는 경우 실행 되는 이벤트 처리기입니다.

DataList 읽기 전용 모드에서 해당 항목이 모두 렌더링 하도록 해야 합니다.

1. 설정 s DataList [ `EditItemIndex` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx) 존재 하지 않는의 인덱스에 `DataListItem` 인덱스입니다. `-1` 이후에 안전 하 게 선택 합니다 `DataListItem` 인덱스에서 시작 `0`합니다.
2. DataList 데이터를 다시 바인딩해야 합니다. 아니요 이후 `DataListItem` `ItemIndex` DataList s에 해당 하는 es `EditItemIndex`, 전체 DataList 읽기 전용 모드에서 렌더링 됩니다.

다음 이벤트 처리기 코드를 사용 하 여 이러한 단계를 수행할 수 있습니다.


[!code-csharp[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample5.cs)]

이 또한을 사용 하 여 취소 단추는 DataList 상태로 미리 편집을 클릭합니다.

마지막 이벤트 처리기를 완료 해야 합니다 `UpdateCommand` 이벤트 처리기입니다. 이 이벤트 처리기에 필요합니다.

1. 편집된 제품 s 뿐만 아니라 사용자가 입력 한 제품 이름 및 가격을 프로그래밍 방식으로 액세스 `ProductID`합니다.
2. 적절 한 호출 하 여 업데이트 프로세스를 시작할 `UpdateProduct` 의 오버 로드는 `ProductsBLL` 클래스입니다.
3. 설정 s DataList [ `EditItemIndex` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx) 존재 하지 않는의 인덱스에 `DataListItem` 인덱스입니다. `-1` 이후에 안전 하 게 선택 합니다 `DataListItem` 인덱스에서 시작 `0`합니다.
4. DataList 데이터를 다시 바인딩해야 합니다. 아니요 이후 `DataListItem` `ItemIndex` DataList s에 해당 하는 es `EditItemIndex`, 전체 DataList 읽기 전용 모드에서 렌더링 됩니다.

S 변경; 사용자를 저장 하는 1 및 2 단계 3-4 단계 돌아갈 DataList 미리 편집 상태 변경 내용이 저장 되 고에서 수행 된 단계와 동일 합니다 `CancelCommand` 이벤트 처리기입니다.

업데이트 된 제품 이름 및 가격을 가져오려면 사용 해야 합니다 `FindControl` 텍스트 웹 컨트롤 내 참조 프로그래밍 방식으로 메서드는 `EditItemTemplate`. 또한 편집된 제품 s 가져오기 해야 `ProductID` 값입니다. Visual Studio DataList s 할당에서는 처음에 바인딩할 때 ObjectDataSource DataList, `DataKeyField` 데이터 원본의 속성을 기본 키 값 (`ProductID`). DataList s에서에서이 값을 검색할 수 다음 `DataKeys` 컬렉션입니다. 잠시 있는지 확인 합니다 `DataKeyField` 실제로 속성 `ProductID`합니다.

다음 코드를 네 단계를 구현합니다.


[!code-csharp[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample6.cs)]

이벤트 처리기를 편집할된 제품의 읽어들여 시작 `ProductID` 에서 `DataKeys` 컬렉션입니다. 다음의 두 텍스트 상자는 `EditItemTemplate` 참조 및 해당 `Text` 로컬 변수에 저장 된 속성 `productNameValue` 및 `unitPriceValue`합니다. 사용 하 여는 `Decimal.Parse()` 에서 값을 읽을 수 있는 메서드를 `UnitPrice` 경우 값을 입력 하도록 하는 텍스트 상자에 통화 기호,이 여전히 올바르게 변환할 수는 `Decimal` 값입니다.

> [!NOTE]
> 값을 `ProductName` 및 `UnitPrice` 텍스트 상자 텍스트 상자 텍스트 속성 값이 지정 되어 있는 경우에 productNameValue 및 unitPriceValue 변수에 할당 됩니다. 그렇지 않으면 값 `Nothing` 되는 변수에 대 한 데이터베이스를 사용 하 여 데이터를 업데이트 하는 효과가 있는 `NULL` 값입니다. 코드 변환을 처리 하는, 빈 문자열을 데이터베이스 `NULL` GridView, DetailsView 및 FormView 컨트롤의 편집 인터페이스의 기본 동작 값입니다.


값을 읽은 후 합니다 `ProductsBLL` s 클래스 `UpdateProduct` 메서드가 호출 되 면 제품의 이름에 전달, 가격 및 `ProductID`합니다. DataList에서와 같이 정확히 동일한 논리를 사용 하 여 미리 편집 상태를 반환 하 여 완료 된 이벤트 처리기는 `CancelCommand` 이벤트 처리기입니다.

사용 하 여 합니다 `EditCommand`, `CancelCommand`, 및 `UpdateCommand` 이벤트 처리기를 완료, 이름 및 제품의 가격이 방문자를 편집할 수 있습니다. 그림 14-16 중인 편집이 워크플로 보여 줍니다.


[![읽기 전용 모드에서 모든 제품을 첫 번째 페이지를 방문 하는 경우](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image35.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image34.png)

**그림 14**: 읽기 전용 모드에 있는 모든 제품 페이지를 처음 방문 하는 경우 ([큰 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image36.png))


[![제품 이름의 가격을 업데이트 하려면 편집 단추를 클릭 합니다.](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image38.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image37.png)

**그림 15**: 제품 이름이 나 가격을 업데이트 하려면 편집 단추를 클릭 합니다. ([큰 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image39.png))


[![값을 변경한 후 읽기 전용 모드를 반환 하는 업데이트를 클릭 합니다.](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image41.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image40.png)

**그림 16**: 다음 값을 변경, return이 고 읽기 전용 모드에 대 한 업데이트를 클릭 ([큰 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image42.png))


## <a name="step-7-adding-delete-capabilities"></a>7 단계: 추가 기능 삭제

DataList를 삭제 기능을 추가 하기 위한 단계 편집 기능을 추가 하는 스크린샷과 비슷합니다. 즉, 삭제 단추를 추가 해야 합니다 `ItemTemplate` 를 클릭할 때:

1. 해당 제품 s 읽습니다 `ProductID` 를 통해를 `DataKeys` 컬렉션입니다.
2. 호출 하 여 삭제를 수행 합니다 `ProductsBLL` s 클래스 `DeleteProduct` 메서드.
3. DataList 데이터가 다시 바인딩합니다.

S에 삭제 단추를 추가 하 여 시작 된 `ItemTemplate`합니다.

단추를 클릭 하면 해당 `CommandName` 는 편집, 업데이트 또는 취소의 DataList를 발생 시킵니다 `ItemCommand` 추가 이벤트와 함께 이벤트 (편집을 사용 하는 경우에 예를 들어를 `EditCommand` 도 이벤트가). 마찬가지로, 나 단추, LinkButton, ImageButton DataList에서입니다 `CommandName` 속성이 삭제 하면 합니다 `DeleteCommand` 이벤트를 발생 시키려면 (함께 `ItemCommand`).

에 있는 편집 단추 옆에 있는 삭제 단추를 추가 합니다 `ItemTemplate`설정, 해당 `CommandName` 속성을 삭제 합니다. 추가한 후이 단추 컨트롤에 DataList의 `ItemTemplate` 선언적 구문 같아야 합니다.


[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample7.aspx)]

다음으로, DataList s에 대 한 이벤트 처리기를 만들고 `DeleteCommand` 이벤트에 다음 코드를 사용 하 여:


[!code-csharp[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample8.cs)]

삭제 단추를 클릭 하면 포스트백을 발생 시키는 및 DataList가 발생 `DeleteCommand` 이벤트입니다. 이벤트 처리기에서 클릭 한 제품 s `ProductID` 에서 액세스 하는 값을 `DataKeys` 컬렉션입니다. 호출 하 여 제품 삭제 되는 다음에 `ProductsBLL` s 클래스 `DeleteProduct` 메서드.

제품을 삭제 한 후 해당 데이터 DataList을 다시 바인딩에서는 중요 한 s (`DataList1.DataBind()`), DataList만 삭제 된 제품을 표시 하지 않으면 계속 됩니다.

## <a name="summary"></a>요약

DataList 지점에 없는 편집 및 지원 GridView 여 삭제를 클릭 하는 동안 짧은 약간의 코드를 사용 하 여 해당 향상 시킬 수 있습니다 이러한 기능을 포함 하도록 합니다. 이 자습서에서는 제품을 삭제할 수 없습니다 및 해당 이름과 가격을 편집할 수 있습니다 2 열 목록을 만드는 방법에 살펴보았습니다. 적절 한 웹 컨트롤을 포함 하는 편집 및 삭제 지원을 추가 합니다 `ItemTemplate` 및 `EditItemTemplate`, 해당 이벤트 처리기 만들기, 사용자가 입력 하 고 기본 키 값 읽기 및 비즈니스와 상호 작용 논리 계층입니다.

기본 편집 및 삭제 DataList에 기능을 추가 했지만, 더 많은 고급 기능에 부족 합니다. 예를 들어, 검사 하지 않습니다 입력된 필드-사용자가 너무의 가격을 입력 하는 경우 비용이 많이 드는, 예외가 throw 됩니다 하 여 `Decimal.Parse` 너무 변환 하려고 할 때에 비용이 많이 드는 `Decimal`합니다. 마찬가지로, 비즈니스 논리에서 데이터 또는 데이터 액세스 계층 업데이트에 문제가 있으면 사용자가 표준 오류 화면을 사용 하 여 표시 됩니다. 삭제 단추에 대 한 확인 없이, 제품을 실수로 삭제 모든 너무 가능성이 높습니다.

나중에 자습서 편집 사용자를 개선 하는 방법을 살펴보겠습니다 발생 합니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Zack Jones, Ken Pespisa 및 Randy Schmidt 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [다음](performing-batch-updates-cs.md)
