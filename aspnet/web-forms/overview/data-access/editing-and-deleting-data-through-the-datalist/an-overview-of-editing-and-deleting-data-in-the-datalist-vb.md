---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-vb
title: DataList (VB)에서 데이터 편집 및 삭제에 대 한 개요 | Microsoft Docs
author: rick-anderson
description: DataList에 기본 제공 편집 및 삭제 기능 부족, 하는 동안이 자습서에서는 보겠습니다를 지 원하는 편집 및 삭제 o DataList를 만드는 방법...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/30/2006
ms.topic: article
ms.assetid: 9410a23c-9697-4f07-bd71-e62b0ceac655
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: 6956777e91184a92e189db7aa716a4bd7dbbfccd
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="an-overview-of-editing-and-deleting-data-in-the-datalist-vb"></a>DataList (VB)에서 데이터 편집 및 삭제에 대 한 개요
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_36_VB.exe) 또는 [PDF 다운로드](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/datatutorial36vb1.pdf)

> DataList에 기본 제공 편집 및 삭제 기능 부족, 하는 동안이 자습서에서는 살펴보겠습니다를 편집 및 원본 데이터의 삭제를 지 원하는 DataList를 만드는 방법.


## <a name="introduction"></a>소개

에 [는 개요의 삽입, 업데이트 및 삭제 데이터](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) 삽입, 업데이트 및 응용 프로그램 아키텍처, ObjectDataSource를 GridView, DetailsView, 및 FormView를 사용 하 여 데이터를 삭제 하는 방법을 살펴보았습니다 자습서 제어 합니다. ObjectDataSource와 이러한 세 개의 데이터 웹 컨트롤을 단순 데이터 수정 인터페이스를 구현 하는 스냅인 되었습니다 및 단순히 스마트 태그에서 확인란 관련 합니다. 코드를 쓸 필요가 없습니다.

그러나 DataList 편집 및 삭제 기능 GridView 컨트롤의 기본 제공에 부족 합니다. 이 누락 된 기능을 된다는 사실에 입각 DataList의 ASP.NET 이전 버전에서 relic 선언적 데이터 소스 컨트롤과 코드 설정 되지 않은 데이터 수정 페이지 사용할 수 없었습니다. 때로 부분적으로 인 한. DataList ASP.NET 2.0에서 제공 하지 않으므로 즉시 동일 데이터 수정 기능 GridView로, 하는 동안에 이러한 기능을 포함 하도록 ASP.NET 1.x 기법을 사용할 수 있습니다. 이 접근 방식에서는 약간의 코드를 있지만,이 자습서에서는 볼 수 있겠지만, DataList에 몇 가지 이벤트 및 속성의 위해가이 프로세스에 설치 합니다.

이 자습서를 편집 및 원본 데이터의 삭제를 지 원하는 DataList를 만드는 방법을 살펴보겠습니다. 고급 편집 및 삭제 시나리오, 입력된 필드 유효성 검사를 포함 하 여, 데이터 액세스 또는 비즈니스 논리 계층 및 등에서 발생 한 예외를 정상적으로 처리 이후 자습서를 검사 합니다.

> [!NOTE]
> DataList, 같은 반복기 컨트롤에 삽입, 업데이트 또는 삭제에 대 한 상자 기능 중에 부족 합니다. 이러한 기능을 추가할 수 있습니다, 동안 DataList 속성 및 이러한 기능을 추가 하는 단순화 하는 반복기에서 찾을 수 없는 이벤트를 포함 합니다. 따라서이 자습서 및 앞으로 편집 및 삭제를 확인 하는 중점적으로 엄격 하 게 DataList 합니다.


## <a name="step-1-creating-the-editing-and-deleting-tutorials-web-pages"></a>1 단계: 편집 및 삭제 자습서 웹 페이지 만들기

업데이트 하 고 DataList에서 데이터를 삭제 하는 방법을 탐색을 시작 하기 전에 s를 먼저 잠시이 자습서와 다음 몇 가지에 대해 사용 해야 하는 웹 사이트 프로젝트에 ASP.NET 페이지를 만들 수 있습니다. 라는 새 폴더를 추가 하 여 시작 `EditDeleteDataList`합니다. 다음에 해당 폴더에 있는 각 페이지에 연결할 수 있도록 다음 ASP.NET 페이지 추가 `Site.master` 마스터 페이지:

- `Default.aspx`
- `Basics.aspx`
- `BatchUpdate.aspx`
- `ErrorHandling.aspx`
- `UIValidation.aspx`
- `CustomizedUI.aspx`
- `OptimisticConcurrency.aspx`
- `ConfirmationOnDelete.aspx`
- `UserLevelAccess.aspx`


![이 자습서에 대 한 ASP.NET 페이지 추가](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image1.png)

**그림 1**: 자습서에 대 한 ASP.NET 페이지 추가


다른 폴더에서와 같이 `Default.aspx` 에 `EditDeleteDataList` 폴더는 해당 섹션의 자습서를 나열 합니다. 이전에 설명한 대로 `SectionLevelTutorialListing.ascx` 이 기능을 제공 하는 사용자 정의 컨트롤입니다. 따라서이 사용자 정의 컨트롤을 추가 `Default.aspx`의 디자인 뷰에서 페이지 하려면 솔루션 탐색기에서 끌어서 합니다.


[![Default.aspx로 SectionLevelTutorialListing.ascx 사용자 정의 컨트롤 추가](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image3.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image2.png)

**그림 2**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `Default.aspx` ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image4.png))


마지막으로, 페이지에 항목으로 추가 된 `Web.sitemap` 파일입니다. 특히 반복기와 DataList 마스터/세부 보고서 후 다음 태그를 추가 `<siteMapNode>`:


[!code-xml[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample1.xml)]

업데이트 한 후 `Web.sitemap`, 브라우저를 통해 자습서 웹 사이트를 보려면 보십시오. 이제 왼쪽 메뉴 DataList 편집 및 삭제 자습서에 대 한 항목이 포함 됩니다.


![이제 사이트 맵 DataList 편집 및 삭제 자습서에 대 한 항목을 포함](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image5.png)

**그림 3**: 이제 사이트 맵 DataList 편집 및 삭제 자습서에 대 한 항목을 포함


## <a name="step-2-examining-techniques-for-updating-and-deleting-data"></a>2 단계: 데이터 업데이트 및 삭제에 대 한 기술 검토

편집 및 GridView 사용 하 여 데이터를 삭제 되므로 쉽지, 내부적 GridView 및 ObjectDataSource 동시에 적용 합니다. 에 설명 된 대로 [삽입, 업데이트 및 삭제와 관련 된 이벤트를 검사](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs.md) 자습서에서는 행의 업데이트 단추를 클릭할 때 GridView는 를양방향데이터바인딩을사용하는해당필드가자동으로할당`UpdateParameters` 해당 ObjectDataSource의 컬렉션 다음 ObjectDataSource s 호출 `Update()` 메서드.

유감 스럽게도, DataList 이러한 기본 제공 기능을 제공 하지 않습니다. ObjectDataSource s 매개 변수는를 s 사용자 값이 할당 되도록 해야 우리의 해당 `Update()` 메서드를 호출 합니다. 주세요.이 노력 지원 하기 위해 DataList 다음과 같은 속성 및 이벤트를 제공 합니다.

- **[ `DataKeyField` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basedatalist.datakeyfield.aspx)**  DataList의 각 항목을 고유 하 게 식별할 수 있어야 할 업데이트나 삭제 하는 경우. 표시 된 데이터의 기본 키 필드에이 속성을 설정 합니다. DataList s 채울 이렇게 [ `DataKeys` 컬렉션](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basedatalist.datakeys.aspx) 지정 된 `DataKeyField` 각 DataList 항목에 대 한 값입니다.
- **[ `EditCommand` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.editcommand.aspx)**  단추나 LinkButton을 ImageButton 같은 경우 발생 인 `CommandName` 속성이로 설정 된 편집을 클릭 합니다.
- **[ `CancelCommand` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.cancelcommand.aspx)**  단추나 LinkButton을 ImageButton 같은 경우 발생 인 `CommandName` 속성 취소 클릭 합니다.
- **[ `UpdateCommand` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.updatecommand.aspx)**  단추, LinkButton을 또는 ImageButton 때 발생 된 `CommandName` 속성이로 설정 된 업데이트를 클릭 합니다.
- **[ `DeleteCommand` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.deletecommand.aspx)**  단추, LinkButton을 또는 ImageButton 때 발생 된 `CommandName` 속성이로 설정 되어 삭제를 클릭 합니다.

이러한 속성 및 이벤트를 사용 하 여 네 가지 방법이 있습니다 DataList에서 데이터를 삭제 하 고 업데이트를 사용할 수 있습니다.

1. **ASP.NET 1.x 기술을 사용 하 여** DataList ASP.NET 2.0 및 ObjectDataSources 전에 존재 하 고 완전히 프로그래밍 방식으로 수단을 통해 데이터를 업데이트 및 삭제할 수 있습니다. 이 기술은 완전히는 ObjectDataSource ditches으로 이루어지며 우리는 데이터를 바인딩하는 DataList 둘 다에서 표시할 데이터를 검색 하는 비즈니스 논리 계층에서 직접 업데이트 하거나 레코드를 삭제 합니다.
2. **페이지에서 단일 ObjectDataSource 컨트롤을 사용 하 여 선택, 업데이트 및 삭제에 대 한** DataList GridView s 내재 된 편집 및 삭제 기능에 부족할 때 없어 s t 수행할 수 없는 이유에서 추가 논의 합니다. 이 접근 방식 GridView 예제에서와 동일 하 게는 ObjectDataSource를 사용 했습니다 하지만를 DataList s에 대 한 이벤트 처리기를 작성 해야 `UpdateCommand` 설정한 ObjectDataSource s 매개 변수 및 호출 하는 이벤트의 `Update()` 메서드.
3. **ObjectDataSource 컨트롤을 사용 하 여 선택 하면, 하지만 업데이트 및 삭제 직접에 대해 the BLL에 대 한** 옵션 2를 사용할 때 약간의 코드를 작성 해야는 `UpdateCommand` 이벤트, 매개 변수 값에 할당 합니다. 대신, 우리 수를 선택 하기 위한는 ObjectDataSource를 사용 하 여 있지만 BLL (예: 옵션 1)에 대 한 직접 업데이트 및 삭제 호출 합니다. ObjectDataSource s 할당 보다 더 읽기 쉬운 코드 개인적으로 직접 BLL와 결합 하 여 데이터를 업데이트 하면 `UpdateParameters` 호출 하 고 해당 `Update()` 메서드.
4. **여러 ObjectDataSources 통해 선언적 수단을 사용 하 여** 모든 이전 세 가지 방법에 약간의 코드를 필요 합니다. D 대신 보관을 사용 경우 최대한 훨씬 선언적 구문으로는 마지막 옵션은 페이지에서 여러 ObjectDataSources를 포함 합니다. 첫 번째 ObjectDataSource BLL에서 데이터를 검색 하 고 DataList에 바인딩합니다. 업데이트에 대 한 다른 ObjectDataSource가 추가 되더라도 s DataList 내에서 직접 추가 `EditItemTemplate`합니다. 지원 삭제를 포함 하려면 아직 다른 ObjectDataSource가 필요에 `ItemTemplate`합니다. ObjectDataSource 사용 하 여 포함 된 이러한이 접근 방식 `ControlParameters` 선언적으로 사용자 입력된 컨트롤에 ObjectDataSource s 매개 변수를 바인딩합니다 (DataList s에에서 프로그래밍 방식으로 지정 하는 것이 아니라 `UpdateCommand` 이벤트 처리기). 이 방법은 포함된 ObjectDataSource s 호출 하는 코드의 비트를 계속 해야 `Update()` 또는 `Delete()` 3 가지가 접근 방법의 다른 보다 작은 명령 수 있지만 필요 합니다. 단점은 여기는 여러 ObjectDataSources 않습니다 복잡해 지는 페이지 전체 가독성이 떨어뜨리지 점입니다.

만 이러한 방법 중 하나를 사용 하도록을 강제 적용할 경우 d 옵션 1 최고의 유연성을 제공 하기 때문에 선택 하므로 DataList는 원래이 패턴에 맞게 설계 되었습니다. DataList ASP.NET 2.0 데이터 소스 컨트롤과 함께 작동 하도록 확장 되었습니다, 동안 없기 모든 확장성 지점 또는 공식 ASP.NET 2.0 데이터 웹 컨트롤 (GridView, DetailsView, 및 FormView)의 기능입니다. 옵션 2-4 없는 장점이, 없이 하지만 합니다.

이 향후 편집 및 삭제 자습서를 사용 하 여 프로그램 ObjectDataSource 데이터를 검색 하기 위한 표시 (옵션 3) 데이터를 업데이트 및 삭제할 BLL으로 직접 호출 합니다.

## <a name="step-3-adding-the-datalist-and-configuring-its-objectdatasource"></a>DataList를 추가 하 고 해당 ObjectDataSource를 구성 하는 3 단계:

이 자습서에서는 제품 정보를 나열 하 고 각 제품에 대 한 사용자는 기능을 제공 이름과 가격을 편집 하 고 제품을 모두 삭제 하는 DataList를 만듭니다. 특히, ObjectDataSource를 사용 하 여 표시할 레코드를 검색 하지만 업데이트를 수행 하 고 합니다 BLL 직접와 결합 하 여 작업을 삭제 합니다. DataList 편집 및 삭제 기능을 구현 하는 방법에 대 한 걱정 म 전에 읽기 전용 인터페이스에서 제품을 표시 하려면 페이지를 먼저 가져온 s가 있습니다. 에서는 이후 했습니다 검사한 다음이 단계 이전 자습서에서 하겠지만 통해 신속 하 게 합니다.

열어 시작는 `Basics.aspx` 페이지에 `EditDeleteDataList` 폴더 및 디자인 보기에서 DataList 페이지에 추가 합니다. 다음으로 DataList s 스마트 태그에서 새 ObjectDataSource를 만듭니다. 를 제품 데이터로 작업 하 고 있으므로 사용 하도록 구성 된 `ProductsBLL` 클래스입니다. 검색할 *모든* 제품을 선택는 `GetProducts()` 선택 탭에는 메서드.


[![ObjectDataSource ProductsBLL 클래스를 사용 하도록 구성](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image7.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image6.png)

**그림 4**: 구성에 사용 하 여 ObjectDataSource는 `ProductsBLL` 클래스 ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image8.png))


[![GetProducts() 메서드를 사용 하 여 제품 정보를 반환 합니다.](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image10.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image9.png)

**그림 5**: 사용 하 여 제품 정보를 반환 된 `GetProducts()` 메서드 ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image11.png))


GridView 처럼 DataList; 새 데이터 삽입을 위한 설계 되지 않았습니다. 따라서 선택 (None) 삽입 탭에서 드롭 다운 목록에서 옵션을 사용 합니다. 또한 이후 업데이트는 UPDATE 및 DELETE 탭을 선택 (없음) 및 삭제 BLL를 통해 프로그래밍 방식으로 수행 됩니다.


[![드롭다운 목록이 ObjectDataSource s 삽입, 업데이트 및 삭제 탭 (없음)으로 설정 되어 있는지 확인 합니다.](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image13.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image12.png)

**그림 6**: ObjectDataSource의 삽입, 업데이트 및 삭제 탭의 드롭다운 목록 (없음)으로 설정 되어 있는지 확인 ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image14.png))


ObjectDataSource를 구성한 후 디자이너를 반환 합니다. 마침을 클릭 합니다. 했습니다 ObjectDataSource 구성, Visual Studio를 자동으로 완료 하는 경우 이전 예에서 본 것으로 만듭니다는 `ItemTemplate` DropDownList에 대 한 각 데이터 필드를 표시 합니다. 이 대체 `ItemTemplate`의 제품 이름과 가격을 표시 하는 하나를 사용 합니다. 또한 설정에서 `RepeatColumns` 속성을 2로 합니다.

> [!NOTE]
> 에 설명 된 대로 *개요의 삽입, 업데이트 및 삭제 데이터* 자습서에서는 아키텍처에서는 제거 म ObjectDataSource를 사용 하 여 데이터를 수정 하는 경우는 `OldValuesParameterFormatString` ObjectDataSource s에서 속성 선언적 태그 (또는 해당 기본값으로 다시 설정 `{0}`). 하지만이 자습서에서는 사용 하 여는 ObjectDataSource만 데이터를 검색 합니다. 따라서,에서는 필요 하지 않습니다 ObjectDataSource s 수정 하려면 `OldValuesParameterFormatString` 속성 값 (있지만 것 대상이 t 그러려면 영향).


DataList 기본 바꾼 후 `ItemTemplate` 을 사용자 지정 된 것으로 선언 태그 페이지에 다음과 비슷한 표시 됩니다.


[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample2.aspx)]

잠시 브라우저를 통해 진행률을 볼 수 있습니다. 그림 7에서 볼 수 있듯이 DataList 두 열에 각 제품에 대 한 제품 이름과 단위 가격을 표시 합니다.


[![제품 이름과 가격 2 열 DataList에 표시 됩니다.](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image16.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image15.png)

**그림 7**: The 제품 이름과 가격 2 열 DataList에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image17.png))


> [!NOTE]
> DataList 다양 한 업데이트 및 삭제 하는 프로세스에 필요한 속성이 있으며 이러한 값은 뷰 상태에 저장 됩니다. 따라서 DataList를 작성을 지 원하는 편집 하거나 데이터를 삭제 하는 경우 반드시 DataList의 뷰 상태를 사용할 수 있습니다.  
>   
>  편집 가능한 Gridview, DetailsViews, 및 FormViews 만들 때 뷰 상태를 사용 하지 않도록 설정할 수 있었습니다 하 예리한 독자 기억할 것입니다. ASP.NET 2.0 웹 컨트롤을 포함할 수 있으므로이 *컨트롤 상태*역할 상태 보기와 같은 것으로 간주 필수적이 지 게시할 상태가 유지 됩니다.


GridView에서 상태 표시 단순히 trivial 상태 정보를 하지 않지만 (포함 하는 편집 및 삭제 하는 데 필요한 상태) 컨트롤 상태를 유지 관리 하는 뷰를 사용 하지 않도록 설정 합니다. ASP.NET 1.x 시간 내에 만든 것 DataList 컨트롤 상태를 사용 하지 않는 하 고 따라서 뷰 상태를 사용할 수 있어야 합니다. 참조 [컨트롤 상태 vs. 뷰 상태](https://msdn.microsoft.com/library/1whwt1k7.aspx) 컨트롤 상태 및 상태 보기에서에서와 다른 목적에 대 한 자세한 내용은 합니다.

## <a name="step-4-adding-an-editing-user-interface"></a>4 단계: 편집 사용자 인터페이스를 추가합니다.

GridView 컨트롤 필드 (BoundFields, CheckBoxFields, TemplateFields, 및 등)의 컬렉션으로 구성 됩니다. 이러한 필드는 해당 모드에 따라 렌더링 된 태그를 조정할 수 있습니다. 예를 들어, 읽기 전용 모드에 있을 때 BoundField 해당 데이터 필드 값 텍스트로 표시 합니다. 편집 모드에 있을 때 TextBox 웹 렌더링 컨트롤 `Text` 속성 데이터 필드 값이 할당 됩니다.

반면에 DataList, 서식 파일을 사용 하 여 해당 항목을 렌더링 합니다. 읽기 전용 항목을 사용 하 여 렌더링 하는 `ItemTemplate` 통해 편집 모드에서 항목을 렌더링 하는 반면는 `EditItemTemplate`합니다. 이 시점에서 우리의 DataList에는 `ItemTemplate`합니다. 추가 해야 하는 항목 수준의 편집 기능을 지원 하기 위해는 `EditItemTemplate` 편집 가능한 항목에 대해 표시 되는 태그를 포함 하 합니다. 이 자습서에서는 텍스트 웹 컨트롤의 제품 이름과 단위 가격이 편집을 위해 사용 합니다.

`EditItemTemplate` (DataList s 스마트 태그에서 템플릿 편집 옵션을 선택 하면) 하 여 선언적으로 또는 디자이너를 통해 만들 수 있습니다. 템플릿 편집 옵션을 사용 하려면 먼저 스마트 태그에서 템플릿 편집 링크를 클릭 한 다음 선택에서 `EditItemTemplate` 드롭 다운 목록에서 항목입니다.


[![DataList의 EditItemTemplate 사용 하려는 경우](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image19.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image18.png)

**그림 8**: s datalist 작업 하기로 `EditItemTemplate` ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image20.png))


그런 다음 제품 이름에을 입력: 및 가격: 다음에 도구 상자에서 두 개의 TextBox 컨트롤을 끌어 놓습니다는 `EditItemTemplate` 디자이너에는 인터페이스입니다. 텍스트 상자의 설정 `ID` 속성을 `ProductName` 및 `UnitPrice`합니다.


[![제품의 이름 및 가격에 대 한 텍스트 상자를 추가 합니다.](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image22.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image21.png)

**그림 9**: 제품의 이름에 대 한 텍스트 상자 및 가격 추가 ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image23.png))


해야 해당 제품 데이터 필드 값을 바인딩하는 `Text` 의 두 텍스트 상자 속성입니다. 텍스트 상자 스마트 태그에서 데이터 바인딩 편집 링크를 클릭 하 고 적절 한 데이터 필드를 연결 하 여는 `Text` 속성을 그림 10에 나와 있는 것 처럼 합니다.

> [!NOTE]
> 바인딩할 때는 `UnitPrice` TextBox의 가격에 대 한 데이터 필드를 `Text` 필드 수 서식을 통화 값으로 (`{0:C}`)는 일반 숫자가 (`{0:N}`), 또는 형식이 지정 되지 않은 상태로 둡니다.


![ProductName 및 UnitPrice 데이터 필드는 입력란의 텍스트 속성에 바인딩](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image24.png)

**그림 10**: 바인딩하는 `ProductName` 및 `UnitPrice` 데이터 필드에 `Text` 입력란의 속성


그림 10에 데이터 바인딩 편집 대화 상자는 어떻게 확인할 *하지* GridView 또는 DetailsView를 TemplateField 또는 FormView 템플릿을 편집할 때 존재 하는 양방향 데이터 바인딩을 확인란을 포함 합니다. 해당 ObjectDataSource s에 자동으로 할당 될 입력된 웹 컨트롤에 입력 한 값이 양방향 데이터 바인딩 기능에 사용할 수 `InsertParameters` 또는 `UpdateParameters` 삽입 되거나 데이터를 업데이트 합니다. DataList 볼 수 있겠지만, 나중에이 자습서의 후 변경 하 고 데이터를 업데이트할 준비가 그녀는 사용자는 양방향 데이터 바인딩을 지원 하지 않습니다, 프로그래밍 방식으로 이러한 텍스트 상자에 액세스 해야 합니다 `Text` 속성 및 해당 값에 전달 된 적절 한 `UpdateProduct` 에서 메서드는 `ProductsBLL` 클래스입니다.

마지막으로 업데이트를 추가 해야 및 취소 단추에는 `EditItemTemplate`합니다. 설명한 것 처럼는 [마스터/세부 레코드를 사용 하는 글머리 기호 목록의 마스터 세부 정보 사용](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md) 자습서에서는 단추, LinkButton을 또는 ImageButton 하는 경우 해당 `CommandName` 속성은 반복기 또는 DataList, 내에서 클릭할는 반복기 또는 DataList의 `ItemCommand` 이벤트가 발생 합니다. DataList에 대 한 경우는 `CommandName` 속성이 특정 값으로 설정 되 면 추가 이벤트가 발생할 수 있습니다. 특수 `CommandName` 다른 규칙 으로부터 속성 값을 포함 합니다.

- 취소 발생은 `CancelCommand` 이벤트
- 발생 편집는 `EditCommand` 이벤트
- 발생 시키는 업데이트는 `UpdateCommand` 이벤트

이러한 이벤트는 발생 염두에서에 둬야 *외에* 는 `ItemCommand` 이벤트입니다.

에 추가 `EditItemTemplate` Button 웹 컨트롤을 두 가지, 한 개의 해당 `CommandName` 업데이트 및 Cancel로 설정 하는 다른 s로 설정 됩니다. 이 두 Button 웹 컨트롤을 추가한 후 디자이너 다음과 비슷하게 표시 됩니다.


[![추가 업데이트 및 취소 단추에는 EditItemTemplate](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image26.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image25.png)

**그림 11**: 추가 업데이트 및 취소 단추를는 `EditItemTemplate` ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image27.png))


와 `EditItemTemplate` 완료 DataList s 선언 태그 비슷해야 다음과:


[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample3.aspx)]

## <a name="step-5-adding-the-plumbing-to-enter-edit-mode"></a>5 단계: 추가 배관 편집 모드로 전환

이 시점에서 우리의 DataList에 편집 인터페이스를 통해 정의 된 해당 `EditItemTemplate`소비량이 적어지지만 거기 s 현재 나타낼 방법이 없기 가격 페이지를 방문 하는 사용자에 대 한 s 제품 정보를 편집 하고자 합니다. 편집 단추,를 클릭 하면 렌더링 해당 DataList 항목 편집 모드에서 각 제품에 추가 해야 합니다. 편집 단추에 추가 하 여 시작 된 `ItemTemplate`, 디자이너를 통해 또는 선언적으로 합니다. S 편집 단추를 설정 하도록 `CommandName` 속성을 편집 합니다.

이 편집 단추를 추가 하면 브라우저를 통해 페이지를 보려면 잠시. 이 추가 된 각 제품 목록을 편집 단추를 포함 해야 합니다.


[![추가 업데이트 및 취소 단추에는 EditItemTemplate](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image29.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image28.png)

**그림 12**: 추가 업데이트 및 취소 단추를는 `EditItemTemplate` ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image30.png))


단추를 클릭 하면에서 포스트백이 발생 하지만 않습니다 *하지* 목록을 편집 모드에 제품을 전환 합니다. 제품을 편집할 수 있도록 해야 합니다.

1. DataList s 설정 [ `EditItemIndex` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx) 의 인덱스에는 `DataListItem` 방금 편집 단추를 클릭 합니다.
2. DataList에 데이터를 다시 바인딩해야 합니다. DataList는 다시 렌더링 하는 경우는 `DataListItem` 인 `ItemIndex` datalist s 해당 `EditItemIndex` 사용 하 여 렌더링 됩니다 해당 `EditItemTemplate`합니다.

DataList s 이후 `EditCommand` 만들기, 이벤트 편집 단추를 클릭할 때 발생 한 `EditCommand` 이벤트 처리기를 다음 코드로:


[!code-vb[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample4.vb)]

`EditCommand` 형식의 개체에 이벤트 처리기가 전달 `DataListCommandEventArgs` 에 대 한 참조를 포함 하는 두 번째 입력된 매개 변수로 `DataListItem` 인 편집 단추가 클릭 되었습니다 (`e.Item`). DataList s를 먼저 설정 하는 이벤트 처리기 `EditItemIndex` 에 `ItemIndex` 의 편집 가능한 `DataListItem` 다음 s DataList를 호출 하 여 DataList에 데이터를 다시 바인딩합니다 `DataBind()` 메서드.

이 이벤트 처리기를 추가한 후 브라우저에서 페이지를 다시 확인 합니다. 지금 편집 단추를 클릭 하는 클릭 한 제품 편집 가능한 (그림 13 참조를)를 만듭니다.


[![편집 단추는 편집 가능한 제품을 클릭 하면](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image32.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image31.png)

**그림 13**: 편집 단추를 클릭 하면 제품 편집 가능한 ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image33.png))


## <a name="step-6-saving-the-user-s-changes"></a>6 단계: 사용자 s 변경 내용 저장

편집 된 제품의 업데이트 또는 취소 단추를 클릭 하는 아무 작업도 수행이 시점에서; DataList s에 대 한 이벤트 처리기를 만들어야 하는이 기능을 추가 하려면 `UpdateCommand` 및 `CancelCommand` 이벤트입니다. 만들어 시작는 `CancelCommand` 편집한 제품의 취소 단추를 클릭 하 고 DataList 편집 전 상태로 돌아갑니다 하 업무를 맡았다고 때 실행 되는 이벤트 처리기입니다.

읽기 전용 모드에 있는 해당 항목의 모든 렌더링 DataList가 하도록 설정 해야 합니다.

1. DataList s 설정 [ `EditItemIndex` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx) 존재 하지의 인덱스에 `DataListItem` 인덱스입니다. `-1` 것은 안전 하므로 `DataListItem` 인덱스에서 시작 `0`합니다.
2. DataList에 데이터를 다시 바인딩해야 합니다. No 이후 `DataListItem` `ItemIndex` DataList s에 해당 하는 es `EditItemIndex`, 전체 DataList는 읽기 전용 모드에서 렌더링 됩니다.

다음 이벤트 처리기 코드와 다음이 단계를 수행할 수 있습니다.


[!code-vb[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample5.vb)]

이 추가 된 상태로 미리 편집 취소 단추 반환 DataList를 클릭합니다.

마지막 이벤트 처리기를 완료 해야는 `UpdateCommand` 이벤트 처리기입니다. 이 이벤트 처리기를 해야합니다.

1. 편집 된 제품 s 뿐만 아니라 사용자가 입력 한 제품 이름 및 가격을 프로그래밍 방식으로 액세스 `ProductID`합니다.
2. 적절 한 호출 하 여 업데이트 프로세스를 시작할 `UpdateProduct` 에 오버 로드는 `ProductsBLL` 클래스입니다.
3. DataList s 설정 [ `EditItemIndex` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx) 존재 하지의 인덱스에 `DataListItem` 인덱스입니다. `-1` 것은 안전 하므로 `DataListItem` 인덱스에서 시작 `0`합니다.
4. DataList에 데이터를 다시 바인딩해야 합니다. No 이후 `DataListItem` `ItemIndex` DataList s에 해당 하는 es `EditItemIndex`, 전체 DataList는 읽기 전용 모드에서 렌더링 됩니다.

단계 1 및 2는 s 변경; 사용자를 저장 해야 3 단계와 4 DataList 미리 편집 상태로 되돌리려면 후 변경 내용이 저장 되 고에서 수행 된 단계와 동일는 `CancelCommand` 이벤트 처리기입니다.

사용 해야 업데이트 된 제품 이름 및 가격을 가져오려면는 `FindControl` TextBox 웹 컨트롤 내 참조 프로그래밍 방식으로 메서드는 `EditItemTemplate`합니다. 편집 된 제품 s 가져올 해야 `ProductID` 값입니다. Visual Studio에서는 처음에 ObjectDataSource DataList에 바인딩된 DataList s 할당 `DataKeyField` 에 기본 키 값은 데이터 원본의 속성 (`ProductID`). DataList s에서에서이 값을 검색할 수 다음 `DataKeys` 컬렉션입니다. 잠시 되어 있는지 확인 하 고 `DataKeyField` 실제로 속성이 `ProductID`합니다.

다음 코드는 네 가지 단계를 구현합니다.


[!code-vb[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample6.vb)]

이벤트 처리기에서 s 편집 된 제품에 대 한 읽기 시작 `ProductID` 에서 `DataKeys` 컬렉션입니다. 다음의 두 텍스트 상자는 `EditItemTemplate` 참조 및 해당 `Text` 지역 변수에 저장 된 속성 `productNameValue` 및 `unitPriceValue`합니다. 사용 하 여는 `Decimal.Parse()` 에서 값을 읽을 수 있는 메서드는 `UnitPrice` 되는 경우 값을 입력 하도록 하는 텍스트 상자에 통화 기호,이 여전히 제대로으로 변환할 수는 `Decimal` 값입니다.

> [!NOTE]
> 값은 `ProductName` 및 `UnitPrice` 입력란 입력란 텍스트 속성 값이 지정 되어 있는 경우에 productNameValue 및 unitPriceValue 변수에 할당 됩니다. 그렇지 않으면 값이 `Nothing` 에 사용 되는 변수를 데이터베이스와 데이터를 업데이트 하는 효과가 있는 `NULL` 값입니다. 즉, 코드 처리 변환 빈 데이터베이스에 대 한 문자열 `NULL` GridView, DetailsView, FormView 컨트롤의 편집 인터페이스의 기본 동작 값입니다.


값을 읽은 후의 `ProductsBLL` s 클래스 `UpdateProduct` 메서드는, 가격, 제품의 이름에 전달 하 고 `ProductID`합니다. DataList에서와 같이 정확히 동일한 논리를 사용 하 여 미리 편집 상태로 반환 하 여 이벤트 처리기가 완료 되 고 `CancelCommand` 이벤트 처리기입니다.

와 `EditCommand`, `CancelCommand`, 및 `UpdateCommand` 방문자의 이름 및 제품의 가격을 편집할 수, 이벤트 처리기를 완료 합니다. 그림 14-16이 편집 워크플로 실행을 보여 합니다.


[![첫 번째 페이지를 방문, 모든 제품이 있는 경우 읽기 전용 모드](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image35.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image34.png)

**그림 14**: 읽기 전용 모드에 있는 모든 제품 페이지 처음 방문 하는 경우 ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image36.png))


[![제품 이름, 가격 s를 업데이트 하려면 편집 단추를 클릭 합니다.](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image38.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image37.png)

**그림 15**: 제품 이름이 나 가격을 업데이트 하려면 [편집] 단추를 클릭 ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image39.png))


[![값을 변경한 후 업데이트 읽기-쓰기 모드로 돌아가려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image41.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image40.png)

**그림 16**: 후 값을 변경, 읽기 전용 모드로 반환에 대 한 업데이트를 클릭 ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/_static/image42.png))


## <a name="step-7-adding-delete-capabilities"></a>7 단계: 삭제 기능 추가

DataList에 삭제 기능을 추가 하는 단계는 편집 기능을 추가 하는 것과 비슷합니다. 즉, 하려면 삭제 단추를 추가 해야는 `ItemTemplate` 를 클릭 하면:

1. 해당 제품 s 읽기가 `ProductID` 통해는 `DataKeys` 컬렉션입니다.
2. Delete를 호출 하 여 수행 된 `ProductsBLL` s 클래스 `DeleteProduct` 메서드.
3. DataList에 데이터를 다시 바인딩합니다.

삭제 단추를 추가 하 여 시작 s는 `ItemTemplate`합니다.

단추를 클릭 하면 해당 `CommandName` 편집, 업데이트, 되었거나 취소 발생 DataList s `ItemCommand` 추가 이벤트와 함께 이벤트 (편집을 사용 하는 경우에 예를 들어는 `EditCommand` 도 이벤트가). 마찬가지로, 모든 단추, LinkButton을 또는 DataList에서 ImageButton 인 `CommandName` 속성이 원인을 삭제는 `DeleteCommand` 이벤트를 발생 시키려면 (와 함께 `ItemCommand`).

삭제 단추 옆에 있는 편집 단추를 추가 `ItemTemplate`설정 해당 `CommandName` 속성을 삭제 합니다. 추가한 후이 단추 컨트롤 여 DataList의 `ItemTemplate` 선언적 구문 같아야 합니다.


[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample7.aspx)]

다음으로 DataList s에 대 한 이벤트 처리기를 만들고 `DeleteCommand` 다음 코드를 사용 하 여 이벤트:


[!code-vb[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-vb/samples/sample8.vb)]

포스트백 삭제 단추를 클릭 하 고 s DataList 발생 `DeleteCommand` 이벤트입니다. 이벤트 처리기에서 클릭 한 제품 s `ProductID` 값에서 액세스 되는 `DataKeys` 컬렉션입니다. 호출 하 여 제품 삭제 되는 다음으로 `ProductsBLL` s 클래스 `DeleteProduct` 메서드.

제품을 삭제 한 후 그 s DataList에 데이터를 다시 바인딩에서는 중요 한 (`DataList1.DataBind()`), 그렇지 않으면 DataList 방금 삭제 된 제품을 표시 하도록 계속 됩니다.

## <a name="summary"></a>요약

DataList는 지점에 부족 하 고 편집 및 삭제 지원 GridView 받을 클릭, 코드의 짧은 비트 것 향상 될 수 있습니다 이러한 기능을 포함 하도록 합니다. 이 자습서에서는 제품 이름과 가격을 편집할 수 없습니다 및 삭제할 수 있는 2 열 목록을 만드는 방법에 살펴보았습니다. 적절 한 웹 컨트롤을 포함 하는 것은 편집 및 삭제 지원 추가 `ItemTemplate` 및 `EditItemTemplate`, 해당 이벤트 처리기 만들기, 사용자 입력 하 고 기본 키 값 읽기 및 비즈니스와 상호 작용 논리 계층입니다.

기본 편집 및 삭제 DataList에 기능을 추가 했으므로 하는 동안에 고급 기능에 부족 합니다. 예를 들어 있는 입력된 필드 유효성 검사는 없습니다-사용자가 너무의 가격을 입력 하는 경우 비용이 많이 들며, 예외가 throw 됩니다 여 `Decimal.Parse` 너무 변환 하려고 할 때에 비용이 많이 드는 `Decimal`합니다. 마찬가지로, 비즈니스 논리에서 데이터 또는 데이터 액세스 계층 업데이트에 문제가 있으면 사용자가 표준 오류 화면이 표시 수입니다. 모든 종류의 삭제 단추에서 확인 하지 않고 제품을 실수로 삭제 모든 너무 가능성이 높습니다.

나중에 편집 사용자를 개선 하는 방법을 살펴보려는 자습서 발생 합니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자가 Zack jones 이면 특정, Ken Pespisa 및 Randy Schmidt 합니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](customizing-the-datalist-s-editing-interface-cs.md)
> [다음](performing-batch-updates-vb.md)
