---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb
title: 삽입, 업데이트 및 삭제 (VB)의 개요 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 ObjectDataSource의 insert (), update ()를 매핑하는 방법을 확인 하 고 구성 하는 방법 뿐만 아니라 클래스 BLL의 메서드에 delete () 메서드...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 35b40b8f-2ca8-4ab3-9c19-f361a91a3647
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 55fab6bb7a1041a14f8734a0d2ae1238b3801149
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830295"
---
<a name="an-overview-of-inserting-updating-and-deleting-data-vb"></a>삽입, 업데이트 및 삭제 (VB) 개요
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_16_VB.exe) 또는 [PDF 다운로드](an-overview-of-inserting-updating-and-deleting-data-vb/_static/datatutorial16vb1.pdf)

> 이 자습서는 ObjectDataSource의 insert (), update ()를 매핑하는 방법을 살펴보겠습니다 및 데이터 수정 기능을 제공 하는 GridView, DetailsView 및 FormView 컨트롤을 구성 하는 방법 뿐만 아니라 클래스 BLL의 메서드에 delete () 메서드.


## <a name="introduction"></a>소개

지난 몇 가지 자습서를 통해 GridView, DetailsView 및 FormView 컨트롤을 사용 하 여 ASP.NET 페이지에서 데이터를 표시 하는 방법을 살펴보았습니다. 이러한 컨트롤은 단순히에 제공 되는 데이터를 사용 하 여 작동 합니다. 일반적으로 이러한 컨트롤 ObjectDataSource와 같은 데이터 소스 컨트롤을 사용 하 여 데이터에 액세스 합니다. ObjectDataSource ASP.NET 페이지와 원본 데이터 간의 프록시로 작동 하는 방법을 살펴보았습니다. 데이터를 표시 해야 하는 GridView, 해당 ObjectDataSource의 호출 `Select()` 에서 우리의 계층 BLL (비즈니스 논리)을 적절 한 데이터 액세스 계층의 (DAL) 메서드를 호출 하는 메서드를 호출 하는 메서드를 다시 전송 하는 TableAdapter를 `SELECT` Northwind 데이터베이스에 쿼리 합니다.

DAL에서 TableAdapters를 만들었을 때는 회수 [첫 번째 자습서](../introduction/creating-a-data-access-layer-cs.md), Visual Studio 자동으로 추가 메서드를 삽입, 업데이트 및 삭제 데이터로 기본 데이터베이스 테이블입니다. 또한 [비즈니스 논리 레이어 만들기](../introduction/creating-a-business-logic-layer-vb.md) 이러한 데이터 수정 DAL 메서드로 호출한 BLL에는 메서드를 설계 했습니다.

외에 해당 `Select()` 메서드를 ObjectDataSource 역시 `Insert()`를 `Update()`, 및 `Delete()` 메서드. 같은 `Select()` 메서드를 세 가지 방법은 메서드 기본 개체에 매핑할 수 있습니다. 데이터를 삽입, 업데이트 또는 삭제를 구성 하는 경우 기본 데이터를 수정 하기 위한 사용자 인터페이스를 제공 하는 GridView, DetailsView 및 FormView 컨트롤입니다. 이 사용자 인터페이스를 호출 합니다 `Insert()`, `Update()`, 및 `Delete()` 는 ObjectDataSource의 다음 내부 개체를 호출 하는 방법의 연결 된 메서드 (그림 1 참조).


[![BLL에 프록시로 ObjectDataSource의 insert (), update (), 및 delete () 메서드 사용](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image2.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image1.png)

**그림 1**: The ObjectDataSource `Insert()`, `Update()`, 및 `Delete()` BLL에 프록시로 제공 메서드 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image3.png))


이 자습서에서는 ObjectDataSource의 매핑하는 방법을 알아봅니다 `Insert()`, `Update()`, 및 `Delete()` 클래스 BLL은 데이터 수정을 제공 하는 GridView, DetailsView 및 FormView 컨트롤을 구성 하는 방법에 대 한 메서드를 메서드 기능입니다.

## <a name="step-1-creating-the-insert-update-and-delete-tutorials-web-pages"></a>1 단계: Insert, Update 및 Delete 자습서 웹 페이지 만들기

삽입, 업데이트 및 데이터를 삭제 하는 방법을 탐색을 시작 하기 전에 먼저 살펴보겠습니다이 자습서에는 다음 몇 가지 작업 해야 하는 웹 사이트 프로젝트에서 ASP.NET 페이지를 만들 수 있습니다. 라는 새 폴더를 추가 하 여 시작 `EditInsertDelete`합니다. 다음에 있는 각 페이지에 연결할 수 있도록 해당 폴더에 다음 ASP.NET 페이지를 추가 합니다 `Site.master` 마스터 페이지:

- `Default.aspx`
- `Basics.aspx`
- `DataModificationEvents.aspx`
- `ErrorHandling.aspx`
- `UIValidation.aspx`
- `CustomizedUI.aspx`
- `OptimisticConcurrency.aspx`
- `ConfirmationOnDelete.aspx`
- `UserLevelAccess.aspx`


![데이터 수정 관련 자습서에 대 한 ASP.NET 페이지 추가](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image4.png)

**그림 2**: 데이터 수정 관련 자습서에 대 한 ASP.NET 페이지 추가


다른 폴더와 같이 `Default.aspx` 에 `EditInsertDelete` 폴더 섹션의 자습서를 나열 됩니다. 이전에 설명한 대로 `SectionLevelTutorialListing.ascx` 사용자 컨트롤은이 기능을 제공 합니다. 따라서이 사용자 정의 컨트롤을 추가 `Default.aspx` 페이지의 디자인 뷰로 솔루션 탐색기에서 끌어 합니다.


[![Default.aspx SectionLevelTutorialListing.ascx 사용자 컨트롤 추가](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image6.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image5.png)

**그림 3**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 `Default.aspx` ([클릭 하 여 큰 이미지 보기](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image7.png))


마지막으로, 페이지에 항목으로 추가 된 `Web.sitemap` 파일입니다. 특히 사용자 지정 하는 포맷 한 후 다음 태그를 추가 `<siteMapNode>`:


[!code-xml[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample1.xml)]

업데이트 한 후 `Web.sitemap`, 잠시 브라우저를 통해 자습서 웹 사이트를 확인 합니다. 왼쪽 메뉴에는 이제 편집, 삽입 및 삭제 자습서에 대 한 항목이 포함 됩니다.


![이제 사이트 맵 편집, 삽입 및 삭제 자습서에 대 한 항목을 포함](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image8.png)

**그림 4**: 이제 사이트 맵 편집, 삽입 및 삭제 자습서에 대 한 항목을 포함


## <a name="step-2-adding-and-configuring-the-objectdatasource-control"></a>2 단계: 추가 및 ObjectDataSource 컨트롤 구성

GridView, DetailsView 및 데이터 수정 기능 및 레이아웃에서 다른 각 FormView, 이후 각각을 개별적으로 검토해 보겠습니다. 그러나 자체 ObjectDataSource를 사용 하 여 각 컨트롤에 있는 것이 아니라 만들겠습니다 모든 세 가지 컨트롤 예제를 공유할 수 있는 단일 ObjectDataSource 합니다.

열기는 `Basics.aspx` 페이지 ObjectDataSource 디자이너 도구 상자에서 끌어서 스마트 태그에서 데이터 소스 구성 링크를 클릭 합니다. 이후는 `ProductsBLL` 는 ObjectDataSource이이 클래스를 사용 하도록 구성 하는 편집, 삽입 및 삭제 메서드를 제공 하는 유일한 BLL 클래스입니다.


[![ProductsBLL 클래스를 사용 하는 ObjectDataSource 구성](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image10.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image9.png)

**그림 5**: ObjectDataSource 사용 하도록 구성 된 `ProductsBLL` 클래스 ([클릭 하 여 큰 이미지 보기](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image11.png))


다음 화면에서 어떤 방법을 지정할 수 있습니다 합니다 `ProductsBLL` 클래스는 ObjectDataSource의 매핑됩니다 `Select()`, `Insert()`, `Update()`, 및 `Delete()` 적절 한 탭을 선택 하 고 드롭다운 목록에서 메서드를 선택 하 여 합니다. 그림 6, 익숙하게 느껴 지 실 이제는 ObjectDataSource의 매핑합니다 `Select()` 메서드를 합니다 `ProductsBLL` 클래스의 `GetProducts()` 메서드. 합니다 `Insert()`, `Update()`, 및 `Delete()` 메서드 맨 위에 있는 목록에서 해당 탭을 선택 하 여 구성할 수 있습니다.


[![가 ObjectDataSource 반환의 모든 제품](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image13.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image12.png)

**그림 6**:가 ObjectDataSource 반환 모든 제품의 ([큰 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image14.png))


그림 7, 8 및 9 ObjectDataSource의 업데이트, 삽입 및 삭제 표시 탭입니다. 이러한 탭을 구성 있도록를 `Insert()`, `Update()`, 및 `Delete()` 메서드를 호출 합니다 `ProductsBLL` 클래스의 `UpdateProduct`, `AddProduct`, 및 `DeleteProduct` 메서드를 각각.


[![ObjectDataSource의 update () 메서드 UpdateProduct 메서드와 같이 ProductBLL 클래스에 매핑](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image16.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image15.png)

**그림 7**: ObjectDataSource의 매핑 `Update()` 메서드는 `ProductBLL` 클래스의 `UpdateProduct` 메서드 ([클릭 하 여 큰 이미지 보기](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image17.png))


[![ObjectDataSource의 insert () 메서드를 ProductBLL 클래스의 AddProduct 메서드에 매핑하십시오.](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image19.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image18.png)

**그림 8**: ObjectDataSource의 매핑 `Insert()` 메서드는 `ProductBLL` 클래스의 추가 `Product` 메서드 ([클릭 하 여 큰 이미지 보기](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image20.png))


[![ObjectDataSource의 delete () 메서드를 ProductBLL 클래스의 DeleteProduct 메서드에 매핑하십시오.](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image22.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image21.png)

**그림 9**: ObjectDataSource의 매핑 `Delete()` 메서드는 `ProductBLL` 클래스의 `DeleteProduct` 메서드 ([클릭 하 여 큰 이미지 보기](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image23.png))


UPDATE, INSERT 및 DELETE 탭의 드롭다운 목록에 이미 선택한 이러한 메서드는 것을 알 수 있습니다. 사용 덕분 이것이 합니다 `DataObjectMethodAttribute` 의 메서드를 장식 하는 `ProducstBLL`합니다. 예를 들어 DeleteProduct 메서드 같은 시그니처가 있습니다.


[!code-vb[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample2.vb)]

`DataObjectMethodAttribute` 특성 선택, 삽입, 업데이트 또는 삭제 및 기본값을 사용 하는 것이 여부는 각 메서드를 나타냅니다. 클래스 BLL을 만들 때 이러한 특성을 생략 하는 경우 있습니다 됩니다 필요를 수동으로 업데이트에서 메서드를 선택 삽입 및 삭제 탭 합니다.

적절 한 확인 한 후 `ProductsBLL` 메서드는 ObjectDataSource의 매핑됩니다 `Insert()`를 `Update()`, 및 `Delete()` 메서드 마법사를 완료 하려면 마침을 클릭 합니다.

## <a name="examining-the-objectdatasources-markup"></a>ObjectDataSource의 태그를 검사합니다.

ObjectDataSource 마법사를 구성한 후 생성된 된 선언적 태그를 검사 하 여 원본 뷰로 이동 합니다. `<asp:ObjectDataSource>` 태그 지정 기본 개체 및 메서드를 호출 합니다. 또한 `DeleteParameters`, `UpdateParameters`, 및 `InsertParameters` 에 대 한 입력 매개 변수에 매핑되는 `ProductsBLL` 클래스의 `AddProduct`를 `UpdateProduct`, 및 `DeleteProduct` 메서드:


[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample3.aspx)]

입력 매개 변수 목록 마찬가지로 연결 된 해당 메서드를 각각에 대 한 매개 변수를 포함 하는 ObjectDataSource `SelectParameter` 가 현재는 입력 매개 변수는 선택 메서드를 호출 하도록 ObjectDataSource가 구성 하는 경우 ( 같은`GetProductsByCategoryID(categoryID)`). 앞으로 살펴보겠지만 곧 이러한 작업에 대 한 값 `DeleteParameters`, `UpdateParameters`, 및 `InsertParameters` GridView, DetailsView 및 FormView ObjectDataSource의 호출 하기 전에 자동으로 설정 됩니다 `Insert()`에 `Update()`, 또는 `Delete()` 메서드입니다. 이후 자습서에서 설명 하겠지만 이러한 값을 필요에 따라 프로그래밍 방식으로 설정할 수도 있습니다.

ObjectDataSource를 구성 하는 마법사를 사용 하 여 한 가지 부작용은 Visual Studio를 설정 하는 [OldValuesParameterFormatString 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.oldvaluesparameterformatstring(VS.80).aspx) 에 `original_{0}`입니다. 이 속성 값 편집 중인 데이터의 원래 값을 포함 하는 데 있으며 두 가지 시나리오에서 유용 합니다.

- 경우 레코드를 편집할 때 사용자의 기본 키 값을 변경할 수 있습니다. 이 경우 새 기본 키 값 및 원래 기본 키 값을 제공 해야 합니다 원래 기본 키 값을 사용 하 여 레코드를 찾을 수를 업데이트 하 고 해당 값이 적절 하 게 업데이트 수 있도록 합니다.
- 낙관적 동시성을 사용할 때 낙관적 동시성은 두 있는지를 확인 하는 기술 동시 사용자 서로 변경 내용을 덮어쓰지 및 이후 자습서에 대 한 항목입니다.

`OldValuesParameterFormatString` 속성에서 기본 개체의 업데이트 및 삭제 메서드는 원래 값에 대 한 입력된 매개 변수의 이름을 나타냅니다. 낙관적 동시성을 살펴볼 때이 속성 및 해당 용도를 자세히 설명 하겠습니다 했습니다. I 가동 시킵니다 이제 단,이 BLL 메서드에 원래 값을 사용 하지 않을 이므로 하므로 반드시이 속성을 제거 했습니다. 종료 합니다 `OldValuesParameterFormatString` 속성이 기본값 이외의 값으로 설정 (`{0}`) 데이터 웹 컨트롤 ObjectDataSource의 호출 하려고 할 때 오류가 발생 `Update()` 또는 `Delete()` 메서드 ObjectDataSource가 있으므로 둘 다에 전달 하려고 시도 합니다 `UpdateParameters` 또는 `DeleteParameters` 원래 값 매개 변수 및 지정 합니다.

이 아니면 그다지 명확이 시점에 걱정,이 속성 및 해당 유틸리티는 이후 자습서에서 살펴봅니다. 이제 방금 반드시 완전히 선언적 구문에서에서이 속성 선언을 제거 하거나 값을 기본값으로 설정 ({0}).

> [!NOTE]
> 단순히 지울 경우는 `OldValuesParameterFormatString` 속성은 디자인 뷰에서 속성 창에서 속성 값의 선언적 구문에는 여전히 존재 하지만 빈 문자열로 설정할 수 있습니다. 따라서 아쉽게도 해도 위에서 설명한 동일한 문제가 발생 합니다. 따라서 제거 하거나 완전히 선언적 구문에서 또는 속성 창에서 설정 값을 기본값으로 `{0}`합니다.


## <a name="step-3-adding-a-data-web-control-and-configuring-it-for-data-modification"></a>3 단계: 데이터 웹 컨트롤을 추가 하 고 데이터 수정에 대 한 구성

ObjectDataSource를 페이지에 추가 하 고 구성 된 된 준비가 데이터 웹 컨트롤을 페이지에 추가 데이터를 표시 및 수정할 최종 사용자에 대 한 수단을 제공 합니다. 살펴보겠습니다 GridView, DetailsView 및 FormView 개별적으로 이러한 데이터 웹 컨트롤의 데이터 수정 기능과 구성 다르게 합니다.

살펴보겠습니다이 문서의 나머지 부분에서 매우 기본적인 편집, 삽입 및 삭제 GridView DetailsView 통해 지원을 추가 및 FormView 컨트롤 처럼 실제로 하기만 하면 됩니다 확인란 가지를 확인 합니다. 많은 미묘한 측면 들 및 방금 가리키고 클릭 보다 더 복잡된 이러한 기능을 제공 하는 실제에 지 사례 있습니다. 이 자습서에서는 있지만 단순한 데이터 수정 기능 하는 데에 중점을 둡니다. 이후 자습서에서는 실제 설정에 반드시 발생할 문제를 검사 합니다.

## <a name="deleting-data-from-the-gridview"></a>GridView에서 데이터 삭제

디자이너 도구 상자에서 GridView 드래그 하 여 시작 합니다. 그런 다음 GridView의 스마트 태그의 드롭다운 목록에서 선택 하 여 ObjectDataSource GridView에 바인딩하십시오. 이 시점에서 GridView의 선언적 태그 표시 됩니다.


[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample4.aspx)]

해당 스마트 태그를 통해 ObjectDataSource에 GridView 바인딩 두 가지 이점이 있습니다.

- BoundFields 및 CheckBoxFields 각 ObjectDataSource가 반환한 필드에 대 한 자동으로 만들어집니다. 또한 BoundField 및 CheckBoxField의 속성에 기본 필드의 메타 데이터에 따라 설정 됩니다. 예를 들어 합니다 `ProductID`, `CategoryName`, 및 `SupplierName` 필드의 읽기 전용으로 표시 됩니다는 `ProductsDataTable` 없습니다 수 없으므로 업데이트할 수 있는 편집 하는 경우. 이, BoundFields'에 맞게 [읽기 전용 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.boundfield.readonly(VS.80).aspx) 로 설정 되어 `True`입니다.
- 합니다 [DataKeyNames 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.datakeynames(VS.80).aspx) 기본 개체의 기본 키 필드에 할당 됩니다. 이 때 필수 필드 (또는 필드의 집합)이이 속성은 나타냅니다 대로 편집 하거나 데이터를 삭제 하기 위해 GridView를 사용 하는 고유한 각 레코드를 식별 합니다. 대 한 자세한 내용은 합니다 `DataKeyNames` 속성을 다시 참조는 [마스터/세부 정보 DetailView와 함께 선택 가능한 마스터 GridView를 사용 하 여 세부 정보](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) 자습서입니다.

GridView 속성 창이 나 선언적 구문을 통해 ObjectDataSource에 바인딩될 수 있지만 이렇게 수동으로 추가 해야 적절 한 BoundField 및 `DataKeyNames` 태그입니다.

행 수준 편집 및 삭제에 대 한 기본 제공 지원을 제공 하는 GridView 컨트롤 합니다. 삭제를 지원 하려면 GridView 구성 삭제 단추의 열을 추가 합니다. 최종 사용자가 특정 행에 대 한 삭제 단추를 클릭 하면 포스트백 근거가 및 GridView에는 다음 단계를 수행 합니다.

1. ObjectDataSource의 `DeleteParameters` 값 할당
2. ObjectDataSource의 `Delete()` 메서드를 호출 하면 지정된 된 레코드를 삭제 합니다.
3. GridView에 다시 바인딩합니다 자체 ObjectDataSource를 호출 하 여 해당 `Select()` 메서드

에 할당 된 값을 `DeleteParameters` 의 값은는 `DataKeyNames` 있는 삭제 단추를 클릭 한 행에 대 한 필드입니다. 따라서 것이 중요 하는 GridView의 `DataKeyNames` 속성이 올바르게 설정 해야 합니다. 없을 경우는 `DeleteParameters` 의 값이 할당 됩니다 `Nothing` 1 단계에서에서 다시 없습니다 결과 2 단계에서에서 삭제 된 레코드입니다.

> [!NOTE]
> 합니다 `DataKeys` 컬렉션 즉 GridView s control 상태에 저장 됩니다는 `DataKeys` GridView가의 뷰 상태를 사용 하지 않도록 설정 된 경우에 다시 게시를 통해 값이 저장 됩니다. 그러나 것이 매우 중요 한 편집 또는 삭제 (기본 동작)을 지 원하는 Gridview에 대 한 뷰 상태 유지 사용 하도록 설정 합니다. GridView가 설정 하는 경우 `EnableViewState` 속성을 `false`편집 및 삭제 동작 것으로 충분할 단일 사용자에 대 한 되지만 이러한 동시 사용자가 실수로 수는 가능성이 있는 데이터를 삭제 하는 동시 사용자의 경우 삭제 또는 편집을 기록 하는 동작 t 의도 합니다. 내 블로그 항목을 참조 하세요 [경고: 동시성 문제 사용 하 여 ASP.NET 2.0 Gridview/DetailsView/FormViews 해당 지원 편집 및/또는 삭제 하 고 있는 뷰 상태를 사용 하지 않도록 설정](http://scottonwriting.net/sowblog/posts/10054.aspx), 자세한 내용은 합니다.


이 동일한 경고 DetailsViews FormViews에도 적용 됩니다.

GridView에 삭제 기능을 추가할 스마트 태그를 이동 하 고 삭제 사용 확인란 합니다.


![확인란 삭제 사용 확인](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image24.png)

**그림 10**: 확인란 삭제 사용 확인


GridView에는 CommandField 추가 스마트 태그에서 삭제 사용 확인란을 선택 합니다. CommandField 다음 작업 중 하나 이상을 수행 하는 단추를 사용 하 여 GridView에서 열을 렌더링: 레코드를 선택한 후, 레코드를 편집 및 레코드를 삭제 합니다. 레코드를 선택 하 여 실행 중인 CommandField를 이전에 살펴본 합니다 [마스터/세부 정보 DetailView와 함께 선택 가능한 마스터 GridView를 사용 하 여 세부 정보](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) 자습서입니다.

CommandField 번호가 `ShowXButton` 어떤 일련의 단추를 CommandField에 표시 됩니다 나타내는 속성입니다. 삭제 사용 확인란을 CommandField를 확인 하 여 해당 `ShowDeleteButton` 속성은 `True` GridView의 열 컬렉션에 추가 되었습니다.


[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample5.aspx)]

이 시점에서 믿을 지 모르겠지만, 마치고 GridView를 삭제 지원 추가. 그림 11에서 알 수 있듯이, Delete 단추 열의 브라우저를 통해이 페이지를 방문 있는 경우.


[![CommandField Delete 단추 열 추가](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image26.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image25.png)

**그림 11**:는 CommandField 추가 열의 삭제 단추 ([큰 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image27.png))


구축한 경험이이 자습서부터에서 직접 클릭 하면이 페이지를 테스트할 때 삭제 단추 경우 예외가 발생 합니다. 이러한 예외 발생 이유 및 해결 방법에 대 한 자세한 정보를 계속 합니다.

> [!NOTE]
> 함께 수반 된이 자습서는이 다운로드를 사용 하 여 수행 하는 경우 이러한 문제는 이미 고려 되어 있는지 확인 합니다. 그러나 바랍니다 발생할 수 있는 문제 및 적합 한 해결 방법을 식별 하기 위해 아래에 나열 된 세부 정보를 읽을 수 있습니다.


제품을 삭제 하려고 시도할 때, 해당 메시지는 예외가 발생 하는 경우 "*ObjectDataSource 'ObjectDataSource1' 매개 변수가 있는 ' DeleteProduct' 제네릭이 아닌 메서드를 찾을 수 없습니다: 원래 productID\_ ProductID*, "제거할 가능성이 잊은 `OldValuesParameterFormatString` ObjectDataSource의 속성입니다. 사용 하 여는 `OldValuesParameterFormatString` 둘 다에 전달 하려고 시도 하는 ObjectDataSource 속성을 지정 `productID` 하 고 `original_ProductID` 입력 매개 변수는 `DeleteProduct` 메서드. `DeleteProduct`그러나만 단일 입력된 매개 변수를 받아들이고, 따라서 예외입니다. 제거 된 `OldValuesParameterFormatString` 속성 (설정 `{0}`) 원래 입력된 매개 변수를 전달 하려고 하지 ObjectDataSource에 지시 합니다.


[![OldValuesParameterFormatString 속성 선택 취소 되었는지 확인](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image29.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image28.png)

**그림 12**: 되어 있는지 확인 합니다 `OldValuesParameterFormatString` 속성에 된 선택이 취소 아웃 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image30.png))


제거한 경우에 합니다 `OldValuesParameterFormatString` 속성을 계속 하면 예외 메시지를 사용 하 여 제품을 삭제 하려고 할 때: "*DELETE 문과 충돌 참조 제약 조건이 있는 ' FK\_순서\_세부 정보 \_제품의*. " Northwind 데이터베이스 간 외래 키 제약 조건을 포함 합니다 `Order Details` 하 고 `Products` 테이블, 즉 제품에서 하나 이상의 레코드가 있는 경우 시스템에서 삭제할 수 없습니다는 `Order Details` 테이블입니다. Northwind 데이터베이스의 모든 제품 하나 이상의 레코드에 있으므로 `Order Details`, 제품의 관련 된 주문 세부 정보 레코드를 먼저 삭제 될 때까지 제품을 모두 삭제할 수 없습니다.


[![제품 삭제를 금지 하는 외래 키 제약 조건](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image32.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image31.png)

**그림 13**: Foreign Key 제약 조건에 제품 삭제 금지 ([큰 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image33.png))


이 자습서에 대 한 바로 삭제 하겠습니다에서 레코드를 모두는 `Order Details` 테이블입니다. 실제 응용 프로그램에서을 해야 합니다.

- 주문 세부 정보를 관리 하는 다른 화면이 포함
- 보강 된 `DeleteProduct` 지정한 제품의 주문 세부 정보를 삭제 하는 논리를 포함 하는 방법
- 삭제 지정 된 제품의 주문 세부 정보를 포함 하려면 TableAdapter를 사용한 SQL 쿼리를 수정 합니다.

방금에서 레코드를 모두 삭제 합니다 `Order Details` foreign key 제약 조건을 회피 하는 테이블입니다. Visual Studio에서 서버 탐색기로 이동, 마우스 오른쪽 단추로 클릭는 `NORTHWND.MDF` 노드를 새 쿼리를 선택 합니다. 그런 다음 쿼리 창에서 다음 SQL 문을 실행 합니다. `DELETE FROM [Order Details]`


[![Order Details 테이블에서 모든 레코드를 삭제 합니다.](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image35.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image34.png)

**그림 14**: 모든 레코드를 삭제 합니다 `Order Details` 표 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image36.png))


정리 후는 `Order Details` 삭제 단추를 클릭 하면 테이블에는 오류 없이 제품 삭제 됩니다. GridView의 되도록 하려면 삭제 단추를 클릭 하면 제품 삭제 하지 않습니다, 경우 확인 `DataKeyNames` 기본 키 필드를 속성 (`ProductID`).

> [!NOTE]
> 삭제 단추를 클릭 하면 포스트백 근거가 고 레코드가 삭제 됩니다. 실수로 잘못 된 행의 삭제 단추를 클릭할 수 있기 때문에 위험할 수 있습니다. 이후 자습서에서 레코드를 삭제 하는 경우 클라이언트 쪽 확인 추가 하는 방법에 살펴보겠습니다.


## <a name="editing-data-with-the-gridview"></a>GridView 사용 하 여 데이터를 편집합니다.

GridView 컨트롤을 삭제 하는 함께 기본 제공 행 수준 편집 지원도 제공 합니다. 편집을 지원 하기 위해 GridView 구성 편집 단추 열을 추가 합니다. 행의 편집 단추 하면 해당 행이 편집 가능한 상태를 클릭 하는 최종 사용자의 관점에서는 기존 값을 포함 하 고 업데이트를 사용 하 여 편집 단추 및 취소 단추를 대체 하는 텍스트 상자에 셀을 설정 합니다. 구성을 변경한 후 해당 원하는 최종 사용자는 변경 내용을 커밋하려면 [업데이트] 단추 또는 내용을 취소 하려면 취소 단추를 클릭 수 있습니다. 두 경우 모두에서 업데이트 또는 취소를 클릭 한 후 GridView 미리 편집 상태로 돌아갑니다.

페이지 개발자 입장에서 최종 사용자가 특정 행에 대 한 편집 단추를 클릭 하면 포스트백 근거가 하 고 GridView에는 다음 단계를 수행 합니다.

1. GridView의 `EditItemIndex` 속성은 해당 편집 단추를 클릭 한 행의 인덱스에 할당
2. GridView에 다시 바인딩합니다 자체 ObjectDataSource를 호출 하 여 해당 `Select()` 메서드
3. 일치 하는 행 인덱스를 `EditItemIndex` "편집 모드입니다."에서 렌더링 됩니다 이 모드에서 편집 단추를 업데이트 및 취소 단추와 BoundFields로 바뀝니다입니다 `ReadOnly` 속성은 False (기본값) 인 TextBox 웹 컨트롤로 렌더링 되는 `Text` 속성 데이터 필드의 값으로 할당 됩니다.

이때 태그는 행의 데이터를 변경 하려면 최종 사용자가 브라우저에 반환 됩니다. 사용자가 [업데이트] 단추를 클릭 하면 포스트백이 발생할 및 GridView에는 다음 단계를 수행 합니다.

1. ObjectDataSource의 `UpdateParameters` 값 GridView의 편집 인터페이스에 최종 사용자가 입력 한 값이 할당 됩니다
2. ObjectDataSource의 `Update()` 메서드를 호출 하면 지정된 된 레코드를 업데이트 하는 중
3. GridView에 다시 바인딩합니다 자체 ObjectDataSource를 호출 하 여 해당 `Select()` 메서드

에 할당 된 기본 키 값을 `UpdateParameters` 에 지정 된 값에서 1 단계에서에서 제공 되는 `DataKeyNames` 속성을 편집된 된 행에 대 한 텍스트 웹 컨트롤의 텍스트에서 기본이 아닌 키 값을 가져오는 반면. 삭제를 사용 하 여 중요 한 것으로 GridView의 `DataKeyNames` 속성이 올바르게 설정 해야 합니다. 없을 경우는 `UpdateParameters` 기본 키 값의 값이 할당 됩니다 `Nothing` 1 단계에서에서 다시 없습니다 결과 2 단계에서에서 업데이트 된 레코드가 있습니다.

GridView의 스마트 태그 편집 사용 확인란을 선택 하면 편집 기능을 활성화할 수 있습니다.


![확인 확인란 편집 사용](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image37.png)

**그림 15**: 확인란 편집 사용 확인


(필요한 경우) 편집 사용 확인란을 CommandField 추가 검사 및 집합 해당 `ShowEditButton` 속성을 `True`입니다. CommandField 개수의 포함 앞서 보았듯이 `ShowXButton` 어떤 일련의 단추를 CommandField에 표시 됩니다 나타내는 속성입니다. 추가 편집 사용 확인란을 선택 합니다 `ShowEditButton` 기존 CommandField 속성:


[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample6.aspx)]

이것이 전부 매우 기본적인 편집 지원을 추가 합니다. 그림 16 에서처럼 편집 인터페이스는 다소 조잡 각 BoundField입니다 `ReadOnly` 속성이 `False` (기본값) 텍스트 상자로 렌더링 됩니다. 여기에 필드와 같은 `CategoryID` 및 `SupplierID`는 다른 테이블에 키입니다.


[![Chai의 편집 단추를 클릭 하면 편집 모드에서 행을 표시](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image39.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image38.png)

**그림 16**: 편집 모드에는 행을 표시 하는 클릭 Chai의 편집 단추 ([큰 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image40.png))


외래 키 값을 직접 편집 하는 사용자를 요청 하는 것 외에도 편집 인터페이스의 인터페이스는 다음과 같은 방법으로 부족 합니다.

- 사용자가 입력 한 `CategoryID` 또는 `SupplierID` 데이터베이스에 존재 하지 않는 `UPDATE` 예외가 발생 하는 외래 키 제약을 위반 합니다.
- 편집 인터페이스는 유효성 검사를 포함 하지 않습니다. 필수 값을 제공 하지 않으면 (같은 `ProductName`), 숫자 값을 필요한 경우 (예: "너무 많이!" 입력 문자열 값을 입력 하거나 에 `UnitPrice` 텍스트 상자)에서 예외가 throw 됩니다. 이후 자습서에서는 편집 사용자 인터페이스에 유효성 검사 컨트롤을 추가 하는 방법을 검사 합니다.
- 현재 *모든* 읽기 전용 되지 않는 제품 필드를 GridView에 포함 되어야 합니다. GridView에서 필드를 제거 하는 것을 가정해 `UnitPrice`GridView 데이터 업데이트를 설정 하지 않아야 하는 경우는 `UnitPrice` `UpdateParameters` 값으로, 데이터베이스 레코드의 변경 `UnitPrice` 에 `NULL` 값. 마찬가지로 경우 필수 필드와 같은 `ProductName`를 제거 됩니다 동일한 GridView에서 업데이트가 실패 합니다 "*'ProductName' 열은 null을 허용 하지 않습니다*" 위에서 언급 한 예외입니다.
- 편집 인터페이스 서식 지정 개선의 여지가 많았습니다. `UnitPrice` 소수점이 하 4와 함께 표시 됩니다. 이상적으로 `CategoryID` 고 `SupplierID` 값에는 시스템의 범주 및 공급자를 나열 하는 Dropdownlist 포함 됩니다.

이제 있으 나 사용 하 여 live 해야 하는 모든 단점은 이후 자습서에서 다루어야 합니다.

## <a name="inserting-editing-and-deleting-data-with-the-detailsview"></a>삽입, 편집 및 DetailsView 사용 하 여 데이터를 삭제 합니다.

이전 자습서에서 살펴본 대로 DetailsView 컨트롤 번를 GridView와 같은 하나의 레코드를 표시, 편집 및 현재 표시 된 레코드의 삭제를 허용 합니다. 편집 및 ASP.NET에서 워크플로 DetailsView에서 항목 삭제를 사용 하 여 최종 사용자의 환경은 GridView의 동일 합니다. 삽입 기본 제공 지원도 제공 하는 GridView에서 DetailsView 다른 위치입니다.

GridView의 데이터 수정 기능을 보여 주기 위해를 DetailsView를 추가 하 여 시작 합니다 `Basics.aspx` 기존 GridView 위에서 페이지 및 DetailsView의 스마트 태그를 통해 기존 ObjectDataSource에 바인딩합니다. 다음으로, DetailsView의 지웁니다 `Height` 및 `Width` 속성 및 스마트 태그에서 페이징 사용 옵션을 확인 합니다. 편집을 사용 하려면 삽입 및 삭제를 지원 하기만 하면 스마트 태그 편집 사용, 삽입을 사용 하도록 설정 및 삭제 사용 확인란을 확인 합니다.


![DetailsView 편집, 삽입 및 삭제를 지원 하도록 구성](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image41.png)

**그림 17**: 편집, 삽입 및 삭제 지원 DetailsView를 구성 합니다.


으로 편집, 추가 GridView를 사용 하 여 삽입 또는 삭제가 지원을 CommandField를 추가 DetailsView를 다음 선언적 구문 보여 줍니다.


[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample7.aspx)]

DetailsView를 CommandField에 대 한 기본적으로 열 컬렉션의 끝에 표시 되는 참고 합니다. DetailsView의 필드가 렌더링 되는 행으로 Insert 사용 하 여 행으로 표시 되는 CommandField 하므로 편집 및 DetailsView의 맨 위에 있는 단추를 삭제 합니다.


[![DetailsView 편집, 삽입 및 삭제를 지원 하도록 구성](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image43.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image42.png)

**그림 18**: 편집, 삽입 및 삭제 지원으로 DetailsView 구성 ([큰 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image44.png))


GridView와 마찬가지로 이벤트의 순서를 시작 삭제 단추를 클릭 합니다: 포스트백을 뒤에 ObjectDataSource의 채우기 DetailsView `DeleteParameters` 기반으로 합니다 `DataKeyNames` ; 값 및 해당 ObjectDataSource의 호출을 사용 하 여 완료 `Delete()` 실제로 데이터베이스에서 제품을 제거 하는 메서드를 합니다. GridView의 동일한 방식으로 작동 DetailsView에서 편집 합니다.

삽입에 대 한 최종 사용자가 새를 사용 하 여 표시 됩니다를 클릭 하면 단추는 "삽입 모드입니다." DetailsView를 렌더링 합니다. "삽입 모드"를 사용 하 여 새 단추 삽입 및 취소 단추와 해당 BoundFields만으로 바뀝니다입니다 `InsertVisible` 속성이 `True` (기본값) 표시 됩니다. 와 같은 자동 증분 필드로 식별 된 데이터 필드 `ProductID`에 있는 해당 [InsertVisible 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datacontrolfield.insertvisible(VS.80).aspx) 로 설정 `False` DetailsView 스마트 태그를 통해 데이터 원본에 바인딩하는 경우.

Visual Studio를 설정 하는 스마트 태그를 통해 DetailsView에 데이터 원본을 바인딩할 경우 합니다 `InsertVisible` 속성을 `False` 자동 증가 필드에 대해서만 합니다. 읽기 전용 필드와 같은 `CategoryName` 및 `SupplierName`, 하지 않는 한 "삽입 모드" 사용자 인터페이스에 표시할 해당 `InsertVisible` 속성 명시적으로 설정 됩니다 `False`합니다. 이 두 필드를 설정 하려면 잠시 `InsertVisible` 속성을 `False`, DetailsView의 선언적 구문 또는 편집 필드를 통해 스마트 태그에 연결 합니다. 그림 19 설정을 표시는 `InsertVisible` 속성을 `False` 필드 편집을 클릭 하 여 연결 합니다.


[![Northwind Traders Acme Tea 제공](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image46.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image45.png)

**그림 19**: Northwind Traders 이제 제공 Acme Tea ([큰 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image47.png))


설정한 후 합니다 `InsertVisible` 속성, 보기는 `Basics.aspx` 브라우저에서 페이지 및 새 단추를 클릭 합니다. 그림 20 새 beverage를 추가할 때 DetailsView를 보여 줍니다 Acme Tea 당사의 제품 라인에 있습니다.


[![Northwind Traders Acme Tea 제공](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image49.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image48.png)

**그림 20**: Northwind Traders 이제 제공 Acme Tea ([큰 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image50.png))


포스트백 근거가 Acme 차에 대 한 세부 정보를 입력 하 고 삽입 단추를 클릭 하면, 및 새 레코드가 추가 되는 `Products` 데이터베이스 테이블입니다. 데이터베이스 테이블에 있는 순서 대로 제품을 나열 하는이 DetailsView, 있으므로에서는 페이지로 마지막 제품 새 제품을 확인 하기 위해 합니다.


[![Acme 차에 대 한 세부 정보](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image52.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image51.png)

**그림 21**: Acme 차에 대 한 세부 정보 ([큰 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image53.png))


> [!NOTE]
> DetailsView [CurrentMode 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.currentmode(VS.80).aspx) 표시 되는 인터페이스를 나타내며 다음 값 중 하나일 수 있습니다: `Edit`를 `Insert`, 또는 `ReadOnly`합니다. 합니다 [DefaultMode 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.defaultmode(VS.80).aspx) 나타내고 DetailsView를 편집한 후 반환 되거나 insert 모드 완료 되는 영구적으로 편집 또는 삽입 모드는 DetailsView를 표시 하는 데 유용 합니다.


GridView과 동일한 제한 사항이에서 저하를 가리키고 클릭 삽입 및 DetailsView의 기능을 편집: 기존 사용자가 입력 해야 `CategoryID` 및 `SupplierID` 값 텍스트 상자를 통해; 인터페이스에 유효성 검사 논리; 모두 제품 필드를 허용 하지 않는 `NULL` 값 또는 기본값이 없는 삽입 인터페이스에서 데이터베이스 수준에서 지정 된 값을 포함 합니다.

기법을 검토해 보겠습니다를 확장 하 고 향상 GridView의 편집 인터페이스 나중에 문서 DetailsView 컨트롤의 편집 및 삽입 인터페이스에도 적용할 수 있습니다.

## <a name="using-the-formview-for-a-more-flexible-data-modification-user-interface"></a>FormView를 사용 하 여 데이터 수정 보다 유연한 사용자 인터페이스에 대 한

FormView는 데이터를 삽입, 편집 및 삭제에 대 한 기본 제공 지원을 제공 하지만 템플릿 필드 대신 사용 하기 때문에 위치가 BoundFields 또는 데이터를 제공 하는 GridView 및 DetailsView 컨트롤에서 사용 하는 CommandField 추가 하려면 수정 인터페이스입니다. 대신 사용자를 수집 하기 위한 웹 컨트롤이 새 항목을 추가할 때 입력 또는 새로 만들기를 함께 처리 되지 않은 기존 편집 편집, 삭제, 삽입, 업데이트 및 취소 단추에는이 인터페이스는 적절 한 서식 파일에 수동으로 추가 해야 합니다. 다행 스럽게도 Visual Studio 자동으로 만들어집니다 필요한 인터페이스 FormView 스마트 태그에서 드롭 다운 목록을 데이터 원본에 바인딩하는 경우.

FormView를 추가 하 여 시작을 설명 하기 위해 이러한 기술을 `Basics.aspx` 페이지 및 FormView의 스마트 태그에서 이미 만든 ObjectDataSource에 바인딩합니다. 이 생성 됩니다는 `EditItemTemplate`, `InsertItemTemplate`, 및 `ItemTemplate` 새로 만들기에 대 한 사용자의 입력 및 단추 웹 컨트롤을 수집 하는 것에 대 한 텍스트 웹 컨트롤을 사용 하 여 FormView에 대 한 편집, 삭제, 삽입, 업데이트 및 취소 단추가 있습니다. 또한: FormView `DataKeyNames` 기본 키 필드를 속성 (`ProductID`) ObjectDataSource에서 반환 되는 개체입니다. 마지막으로, FormView의 스마트 태그의 페이징 사용 옵션을 확인 합니다.

다음 FormView의에 대 한 선언적 태그를 보여 줍니다. `ItemTemplate` FormView ObjectDataSource에 바인딩된 후 합니다. 기본적으로 각 부울이 아닌 값 제품 필드에 바인딩되어 합니다 `Text` 하는 동안 각 부울 값 필드 레이블 웹 컨트롤의 속성 (`Discontinued`)에 바인딩되어는 `Checked` 비활성화 된 확인란 웹 컨트롤의 속성입니다. 새로 만들기, 편집 및 삭제 단추를 클릭할 때 특정 FormView 동작 트리거를 반드시는 자신의 `CommandName` 값을 설정할 수 `New`를 `Edit`, 및 `Delete`, 각각.


[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample8.aspx)]

그림 22 표시 FormView의 `ItemTemplate` 브라우저를 통해 볼 때. 맨 아래에서 새로 만들기, 편집 및 삭제 단추를 사용 하 여 각 제품 필드 나열 됩니다.


[![함께 새로운 각 제품 필드를 나열 하는 데이터 정렬과 FormView ItemTemplate, 편집 및 삭제 단추](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image55.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image54.png)

**그림 22**:의 데이터 정렬과 FormView `ItemTemplate` 나열 각 제품 필드과 함께 새로 만들기, 편집 및 삭제 단추 ([클릭 하 여 큰 이미지 보기](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image56.png))


GridView와 DetailsView를 삭제 단추 단추, LinkButton, 또는 ImageButton 클릭 같은입니다 `CommandName` 속성 다시 게시를 삭제 하면으로 설정 되어, ObjectDataSource의 채웁니다 `DeleteParameters` FormView의 기반`DataKeyNames`값을 호출 하는 ObjectDataSource의 `Delete()` 메서드.

편집 단추를 클릭 하면 포스트백 근거가 및 데이터를 다시 바인딩되는 `EditItemTemplate`, 편집 인터페이스를 렌더링 해야 하는 합니다. 이 인터페이스는 업데이트 및 취소 단추와 함께 데이터 편집에 대 한 웹 컨트롤이 포함 되어 있습니다. 기본값 `EditItemTemplate` 에서 생성 된 Visual Studio에는 자동 증가 필드에 대 한 레이블을 (`ProductID`), 각 부울이 아닌 값 필드에 대 한 텍스트 상자 및 각 부울 값 필드에 대 한 확인란을 선택 합니다. 이 동작은 GridView 및 DetailsView 컨트롤에서 자동으로 생성 된 BoundFields 매우 비슷합니다.

> [!NOTE]
> 한 가지 작은 문제가 FormView의 자동으로 생성 된 `EditItemTemplate` 렌더링 되었는지 TextBox 웹은 같은 읽기 전용 필드에 대 한 컨트롤은 `CategoryName` 및 `SupplierName`합니다. 이 고려 하는 방법을 살펴보겠습니다 곧 합니다.


텍스트 상자 컨트롤을 `EditItemTemplate` 가 해당 `Text` 사용 하 여 해당 데이터 필드의 값에 바인딩된 속성 *양방향 데이터 바인딩*합니다. 양방향 데이터 바인딩 가리키는 `<%# Bind("dataField") %>`, 삽입 또는 레코드를 편집 하기 위한 ObjectDataSource의 매개 변수를 채울 때 및 데이터 템플릿에 바인딩할 때 모두 데이터 바인딩을 수행 합니다. 즉, 사용자가 클릭 하면 편집 단추를 합니다 `ItemTemplate`, `Bind()` 메서드는 지정 된 데이터 필드 값을 반환 합니다. 사용 하 여 지정 된 데이터 필드 값을 해당 백 게시 사용자는 변경을 수행 하 고 업데이트를 클릭 한 후 `Bind()` ObjectDataSource의 적용할 `UpdateParameters`합니다. 또는, 단방향 databinding을 가리키는 `<%# Eval("dataField") %>`만 템플릿에 데이터를 바인딩할 때 데이터 필드 값을 검색 하는 *하지* 포스트백 될 때 데이터 원본의 매개 변수를 사용자가 입력 한 값을 반환 합니다.

다음과 같은 선언적 태그가 표시 FormView의 `EditItemTemplate`합니다. 합니다 `Bind()` 구문이 여기에서 메서드를 사용 하 고 업데이트 및 취소 단추 웹 컨트롤에 있는 해당 `CommandName` 적절 하 게 설정 하는 속성입니다.


[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample9.aspx)]

우리의 `EditItemTemplate`,이 지점에서 사용 하려고 하면 throw 되는 예외가 발생 합니다. 문제는 합니다 `CategoryName` 하 고 `SupplierName` TextBox 웹 컨트롤 필드가 렌더링 되는 `EditItemTemplate`. 하거나 이러한 텍스트 레이블을 변경 하거나 완전히 제거 해야 합니다. 단순히에서 완전히 삭제는 `EditItemTemplate`합니다.

그림 23 Chai에 대 한 편집 버튼을 클릭 한 후 브라우저에서 FormView를 보여 줍니다. 합니다 `SupplierName` 및 `CategoryName` 에 표시 된 필드를 `ItemTemplate` 는 더 이상에서 제거 했습니다는 `EditItemTemplate`합니다. [업데이트] 단추를 클릭할 때 FormView GridView 및 DetailsView 컨트롤과 동일한 일련의 단계를 진행 합니다.


[![기본적으로는 EditItemTemplate 입력란 또는 확인란 각 편집 가능한 제품 필드를 표시](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image58.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image57.png)

**그림 23**: 기본적으로 `EditItemTemplate` 표시 각 편집 가능한 제품 필드 입력란 또는 확인란 ([클릭 하 여 큰 이미지 보기](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image59.png))


삽입 단추 FormView의를 클릭할 때 `ItemTemplate` 포스트백 근거가 됩니다. 그러나 데이터가 없는 새 레코드를 추가 하는 FormView에 바인딩되어 있습니다. `InsertItemTemplate` 인터페이스 삽입 및 취소 단추와 함께 새 레코드를 추가 하는 것에 대 한 웹 컨트롤이 포함 되어 있습니다. 기본값 `InsertItemTemplate` 에서 생성 된 각 부울이 아닌 값 필드에 대 한 텍스트 상자와 비슷한 자동으로 생성 된 각 부울 값 필드에 대 한 확인란을 포함 하는 Visual Studio `EditItemTemplate`인터페이스의 합니다. TextBox 컨트롤에는 해당 `Text` 속성 양방향 데이터 바인딩을 사용 하 여 해당 해당 데이터 필드의 값에 바인딩됩니다.

다음과 같은 선언적 태그가 표시 FormView의 `InsertItemTemplate`합니다. 합니다 `Bind()` 구문이 여기에서 메서드를 사용 하 고 컨트롤 삽입 및 취소 단추 웹 컨트롤에 있는 해당 `CommandName` 적절 하 게 설정 하는 속성입니다.


[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample10.aspx)]

FormView의 자동으로 생성 된 미묘한 문제가 `InsertItemTemplate`합니다. 텍스트 웹 컨트롤은 같은 읽기 전용 필드에 대해서도 특히 만들어집니다 `CategoryName` 고 `SupplierName`입니다. 와 마찬가지로 합니다 `EditItemTemplate`, 이러한 텍스트 상자에서 제거 해야 합니다 `InsertItemTemplate`합니다.

그림 24 Acme 커피 새 제품을 추가 하는 경우 브라우저에서 FormView를 보여 줍니다. `SupplierName` 하 고 `CategoryName` 에 표시 된 필드는 `ItemTemplate` 는 더 이상만 제거 했습니다. DetailsView 컨트롤 같은 일련의 단계를 통해 FormView 진행 되는 삽입 단추를 클릭 하는 경우 새 레코드를 추가 합니다 `Products` 테이블입니다. 그림 25 삽입 한 후 FormView에서 Acme 커피 제품 세부 정보를 보여 줍니다.


[![먼저 지정 FormView의 삽입 인터페이스](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image61.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image60.png)

**그림 24**: 합니다 `InsertItemTemplate` FormView의 삽입 인터페이스를 나타냅니다 ([클릭 하 여 큰 이미지 보기](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image62.png))


[![FormView에서 Acme 커피 새 제품에 대 한 세부 정보가 표시 됩니다.](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image64.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image63.png)

**그림 25**: FormView Acme 커피 새 제품에 대 한 세부 정보 표시 됩니다 ([큰 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image65.png))


읽기 전용을 구분 하 여 편집 및 삽입 인터페이스에 세 가지 별도 템플릿을 FormView GridView 및 DetailsView 보다 더욱 정교한 수준의 이러한 인터페이스를 통해 컨트롤에 대 한 허용 합니다.

> [!NOTE]
> DetailsView, FormView의 같은 `CurrentMode` 속성은 표시 되는 인터페이스를 나타냅니다 고 `DefaultMode` 속성 모드를 나타내는 FormView 돌아갑니다 편집 후 또는 삽입 완료 되었습니다.


## <a name="summary"></a>요약

이 자습서에서는 삽입, 편집 및 GridView와 DetailsView FormView 사용해 데이터 삭제의 기본 사항을 살펴보았습니다. 이러한 컨트롤은 세 가지 모두 일정 수준의 데이터 웹 컨트롤 및 ObjectDataSource ASP.NET 페이지에서 코드를 전혀 작성 하지 않고도 사용할 수 있는 기본 제공 데이터 수정 기능을 제공 합니다. 그러나 간단한 가리키고 상당히 frail 기술 렌더링 및 단순한 데이터 수정 사용자 인터페이스를 클릭 합니다. 유효성 검사를 제공 하려면 프로그래밍 방식으로 값을 삽입, 예외를 매끄럽게 처리할 사용자 인터페이스 및 등과 해야 다음 몇 가지 자습서를 통해 살펴봅니다 기술의 해보세요 의존 합니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [이전](limiting-data-modification-functionality-based-on-the-user-cs.md)
> [다음](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)
