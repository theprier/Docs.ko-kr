---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs
title: "삽입, 업데이트 및 삭제 (C#)에 대 한 개요 | Microsoft Docs"
author: rick-anderson
description: "이 자습서에서는 म ObjectDataSource의 insert (), update ()를 매핑하는 방법을 확인 하 고 구성 하는 방법 뿐만 아니라 BLL의 메서드에 delete () 메서드를 클래스 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/17/2006
ms.topic: article
ms.assetid: b651dc58-93c7-4f83-a74e-3b99f6d60848
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs
msc.type: authoredcontent
ms.openlocfilehash: e483c37cc773a7255f18c26bc3609d68f71dff7d
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="an-overview-of-inserting-updating-and-deleting-data-c"></a>삽입, 업데이트 및 삭제 (C#)의 개요
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_16_CS.exe) 또는 [PDF 다운로드](an-overview-of-inserting-updating-and-deleting-data-cs/_static/datatutorial16cs1.pdf)

> 이 자습서에서는 म ObjectDataSource의 insert (), update ()를 매핑하는 방법을 확인 하 고 데이터 수정 기능을 제공 GridView, DetailsView, FormView 컨트롤을 구성 하는 방법 뿐만 아니라 BLL의 메서드에 delete () 메서드를 클래스.


## <a name="introduction"></a>소개

지난 몇 가지 자습서를 통해 GridView, DetailsView, FormView 컨트롤을 사용 하 여 ASP.NET 페이지에서 데이터를 표시 하는 방법을 검사 한 했습니다. 이러한 컨트롤은 단순히 제공 받은 데이터와 함께 작동 합니다. 일반적으로 이러한 컨트롤은 ObjectDataSource 같은 데이터 소스 제어를 사용 하 여 데이터에 액세스 합니다. ASP.NET 페이지 및 원본 데이터 간의 프록시는 ObjectDataSource 작업 방식 살펴보았습니다. 데이터를 표시 해야 하는 GridView의 ObjectDataSource 호출 `Select()` 에서 우리의 BLL 비즈니스 논리 계층 (), 적절 한 데이터 액세스 계층의 (DAL) 메서드를 호출 하는 메서드를 호출 하는 메서드를 TableAdapter에는 `SELECT` Northwind 데이터베이스에 쿼리 합니다.

에 DAL에서 Tableadapter를 만들 때 사용자에 게 이라는 [이 첫 번째 자습서](../introduction/creating-a-data-access-layer-cs.md), Visual Studio 자동으로 추가 삽입을 위한 메서드를 업데이트 하 고 데이터베이스 테이블의 기본 데이터를 삭제 합니다. 또한 [는 비즈니스 논리 계층을 만드는](../introduction/creating-a-business-logic-layer-cs.md) 이러한 데이터 수정 DAL 메서드로 호출한 BLL의 메서드를 설계 했습니다.

외에 해당 `Select()` 메서드는 ObjectDataSource 역시 `Insert()`, `Update()`, 및 `Delete()` 메서드. 마찬가지로 `Select()` 메서드를 다음 세 가지 방법 메서드는 원본 개체에서에 매핑할 수 있습니다. 데이터를 삽입, 업데이트 또는 삭제를 구성 하는 경우 기본 데이터를 수정 하기 위한 사용자 인터페이스를 제공 하는 GridView, DetailsView, FormView 컨트롤입니다. 이 사용자 인터페이스를 호출는 `Insert()`, `Update()`, 및 `Delete()` ObjectDataSource의 다음 내부 개체를 호출 하는 메서드의 연결 된 메서드 (그림 1 참조).


[![ObjectDataSource의 insert (), update (), 및 delete () 메서드 BLL에는 프록시 역](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image2.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image1.png)

**그림 1**: The ObjectDataSource `Insert()`, `Update()`, 및 `Delete()` 메서드 BLL에 프록시를 토대로 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image3.png))


이 자습서에서는 ObjectDataSource의 매핑하는 방법을 보겠습니다 `Insert()`, `Update()`, 및 `Delete()` 메서드를 제공 하는 데이터 수정에 GridView, DetailsView, FormView 컨트롤을 구성 하는 방법 뿐만 아니라는 BLL에서 클래스의 메서드에 기능입니다.

## <a name="step-1-creating-the-insert-update-and-delete-tutorials-web-pages"></a>1 단계: Insert, Update 및 Delete 자습서 웹 페이지 만들기

삽입, 업데이트 및 데이터를 삭제 하는 방법을 탐색을 시작 하기 전에 먼저 간단히 살펴보겠습니다이 자습서와 다음 몇 가지에 대해 사용 해야 하는 웹 사이트 프로젝트에 ASP.NET 페이지를 만들 수 있습니다. 라는 새 폴더를 추가 하 여 시작 `EditInsertDelete`합니다. 다음에 해당 폴더에 있는 각 페이지에 연결할 수 있도록 다음 ASP.NET 페이지 추가 `Site.master` 마스터 페이지:

- `Default.aspx`
- `Basics.aspx`
- `DataModificationEvents.aspx`
- `ErrorHandling.aspx`
- `UIValidation.aspx`
- `CustomizedUI.aspx`
- `OptimisticConcurrency.aspx`
- `ConfirmationOnDelete.aspx`
- `UserLevelAccess.aspx`


![데이터 수정 관련 자습서에 대 한 ASP.NET 페이지 추가](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image4.png)

**그림 2**: 데이터 수정 관련 자습서에 대 한 ASP.NET 페이지 추가


다른 폴더에서와 같이 `Default.aspx` 에 `EditInsertDelete` 폴더는 해당 섹션의 자습서를 나열 합니다. 이전에 설명한 대로 `SectionLevelTutorialListing.ascx` 이 기능을 제공 하는 사용자 정의 컨트롤입니다. 따라서이 사용자 정의 컨트롤을 추가 `Default.aspx` 페이지의 디자인 뷰에서 하려면 솔루션 탐색기에서 끌어서 합니다.


[![Default.aspx로 SectionLevelTutorialListing.ascx 사용자 정의 컨트롤 추가](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image6.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image5.png)

**그림 3**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `Default.aspx` ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image7.png))


마지막으로, 페이지에 항목으로 추가 된 `Web.sitemap` 파일입니다. 특히 사용자 지정 포맷 한 후 다음 태그를 추가 `<siteMapNode>`:


[!code-xml[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample1.xml)]

업데이트 한 후 `Web.sitemap`, 브라우저를 통해 자습서 웹 사이트를 보려면 보십시오. 왼쪽 메뉴에는 이제 편집, 삽입 및 삭제 자습서에 대 한 항목이 포함 됩니다.


![이제 사이트 맵 편집, 삽입 및 삭제 자습서에 대 한 항목을 포함](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image8.png)

**그림 4**: 이제 사이트 맵 편집, 삽입 및 삭제 자습서에 대 한 항목을 포함


## <a name="step-2-adding-and-configuring-the-objectdatasource-control"></a>2 단계: 추가 및 ObjectDataSource 컨트롤 구성

GridView, DetailsView, 및 데이터 수정 기능 및 레이아웃에 다른 각 FormView 이후 각각을 개별적으로 검토해 보겠습니다. 그러나 자체 ObjectDataSource를 사용 하 여 각 컨트롤이 아닌 방금 만들겠습니다 모든 세 가지 컨트롤 예제를 공유할 수 있는 단일 ObjectDataSource 합니다.

열기는 `Basics.aspx` 페이지는 ObjectDataSource 디자이너 도구 상자에서 끌어서 스마트 태그에서 데이터 소스 구성 링크를 클릭 합니다. 이후는 `ProductsBLL` ObjectDataSource이이 클래스를 사용 하도록 구성 하는 편집, 삽입 및 삭제 메서드를 제공 하는 유일한 BLL 클래스입니다.


[![ObjectDataSource ProductsBLL 클래스를 사용 하도록 구성](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image10.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image9.png)

**그림 5**: 구성에 사용 하 여 ObjectDataSource는 `ProductsBLL` 클래스 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image11.png))


다음 화면에서 어떤 방법을 지정할 수 있습니다는 `ProductsBLL` 클래스는 ObjectDataSource에 매핑된 `Select()`, `Insert()`, `Update()`, 및 `Delete()` 적절 한 탭을 선택 하 고 드롭다운 목록에서 메서드를 선택 하 여 합니다. 그림 6 익숙할 지금까지, ObjectDataSource의 매핑하는 `Select()` 메서드는 `ProductsBLL` 클래스의 `GetProducts()` 메서드. `Insert()`, `Update()`, 및 `Delete()` : 위쪽 목록에서 해당 탭을 선택 하 여 메서드를 구성할 수 있습니다.


[![ObjectDataSource 이동할 모든 제품](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image13.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image12.png)

**그림 6**:는 ObjectDataSource 반환 모든 제품의 있는 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image14.png))


그림 7, 8, 9 ObjectDataSource의 업데이트, 삽입 및 삭제 표시 탭 합니다. 이러한 탭을 구성 하는 `Insert()`, `Update()`, 및 `Delete()` 메서드 호출는 `ProductsBLL` 클래스의 `UpdateProduct`, `AddProduct`, 및 `DeleteProduct` 메서드를 각각.


[![ObjectDataSource의 update () 메서드를 ProductBLL 클래스 UpdateProduct 메서드 매핑합니다](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image16.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image15.png)

**그림 7**: ObjectDataSource의 매핑 `Update()` 메서드는 `ProductBLL` 클래스의 `UpdateProduct` 메서드 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image17.png))


[![ObjectDataSource의 insert () 메서드를 ProductBLL 클래스 AddProduct 메서드 매핑합니다](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image19.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image18.png)

**그림 8**: ObjectDataSource의 매핑 `Insert()` 메서드는 `ProductBLL` 클래스의 추가 `Product` 메서드 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image20.png))


[![ObjectDataSource의 delete () 메서드를 ProductBLL 클래스 DeleteProduct 메서드 매핑합니다](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image22.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image21.png)

**그림 9**: ObjectDataSource의 매핑 `Delete()` 메서드는 `ProductBLL` 클래스의 `DeleteProduct` 메서드 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image23.png))


UPDATE, INSERT 및 DELETE 탭에 있는 드롭 다운 목록에 이미 선택 된 이러한 메서드는 것을 알 수 있습니다. 이 장치의 사용 덕분에 `DataObjectMethodAttribute` 의 메서드를 장식 하 `ProducstBLL`합니다. 예를 들어 DeleteProduct 메서드에는 다음 서명이 있습니다.


[!code-csharp[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample2.cs)]

`DataObjectMethodAttribute` 특성 인지 여부에 관계 선택, 삽입, 업데이트 또는 삭제, 기본 값은 여부에 대 한 각 방법의 용도 나타냅니다. BLL 클래스를 만들 때 이러한 특성을 생략 하면 있습니다 합니다 필요한 업데이트에서 메서드를 직접 선택 삽입 및 삭제 탭 합니다.

적절 한 확인 한 후 `ProductsBLL` 메서드는 ObjectDataSource에 매핑된 `Insert()`, `Update()`, 및 `Delete()` 메서드 마법사를 완료 하려면 마침을 클릭 합니다.

## <a name="examining-the-objectdatasources-markup"></a>ObjectDataSource의 태그를 검사합니다.

해당 마법사를 통해 ObjectDataSource를 구성한 후 생성된 된 선언적 태그를 검사 하 여 원본 뷰로 이동 합니다. `<asp:ObjectDataSource>` 태그 기본 개체 및 호출할 메서드를 지정 합니다. 또한 `DeleteParameters`, `UpdateParameters`, 및 `InsertParameters` 에 대 한 입력된 매개 변수에 매핑되는 `ProductsBLL` 클래스의 `AddProduct`, `UpdateProduct`, 및 `DeleteProduct` 메서드:


[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample3.aspx)]

각 목록은 마찬가지로 해당 관련된 메서드에 대 한 입력된 매개 변수에 매개 변수를 포함 하는 ObjectDataSource `SelectParameter` s는 입력된 매개 변수를 예상 하는 select 메서드를 호출 하는 ObjectDataSource 하도록 구성 된 경우 현재 ( 같은`GetProductsByCategoryID(categoryID)`). 값은 곧, 볼 수 있겠지만 `DeleteParameters`, `UpdateParameters`, 및 `InsertParameters` ObjectDataSource의 호출 하기 전에 GridView, DetailsView, 및 FormView에서 자동으로 설정 `Insert()`, `Update()`, 또는 `Delete()` 메서드입니다. 이러한 값에 대 한 이후 자습서에서 설명 하겠지만도 필요에 따라 프로그래밍 방식으로 설정할 수 있습니다.

ObjectDataSource를 구성 하려면 마법사를 사용 하 여 한 가지 부작용은 Visual Studio를 설정 하는 [OldValuesParameterFormatString 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.oldvaluesparameterformatstring(VS.80).aspx) 를 `original_{0}`합니다. 이 속성 값 편집 중인 데이터의 원래 값을 포함 하는 데 사용 되 고 두 가지 시나리오에서 유용:

- 경우 레코드를 편집할 때 사용자의 기본 키 값을 변경할 수 있습니다. 이 경우 새 기본 키 값과 원래 기본 키 값이 모두 제공 되어야 합니다 원래 기본 키 값을 가진 레코드를 찾을 수를 해당 값이에 따라 업데이트 수 있습니다.
- 낙관적 동시성을 사용할 때 낙관적 동시성은 두 개의 있는지를 확인 하는 기술을 동시 사용자 서로 변경 내용을 덮어쓰지 및 이후 자습서에 대 한 항목은입니다.

`OldValuesParameterFormatString` 속성은 기본 개체의 업데이트 및 삭제 메서드는 원래 값에 대 한 입력된 매개 변수 이름을 표시 합니다. 낙관적 동시성을 탐색 하는 경우이 속성 및 제품 자세히 용도 설명 합니다. 그러나 I 올 것 이제 우리의 BLL 메서드는 원래 값을 사용 하지 않을 고 따라서 반드시이 속성을 제거 했습니다. 종료는 `OldValuesParameterFormatString` 속성이 기본값 이외의 값으로 설정 (`{0}`) 데이터 웹 컨트롤 ObjectDataSource의 호출 하려고 할 때 오류가 발생 하면 `Update()` 또는 `Delete()` 메서드는 ObjectDataSource 됩니다 때문에 둘 다에 전달 하려고 시도 `UpdateParameters` 또는 `DeleteParameters` 원래 값 매개 변수 뿐만 아니라 지정 합니다.

이 그다지 형식이 명확 하지 시점 걱정, 이후 자습서에서이 속성 및 활용성 검토 합니다. 지금은 방금 반드시이 속성 선언 선언적 구문에서 완전히 제거 하거나 기본값 ({0} 개)에 값을 설정 합니다.

> [!NOTE]
> 단순히 제거 하는 경우는 `OldValuesParameterFormatString` 디자인 뷰에서 속성은 속성 창에서 속성 값의 선언 구문에는 여전히 존재 하지만 빈 문자열로 설정할 수 있습니다. 하지만 여전히 이렇게 하면 위에서 설명한 동일한 문제가 발생 합니다. 따라서 제거 하거나 속성 완전히 선언적 구문에서 또는 속성 창에서 설정 값을 기본값으로 `{0}`합니다.


## <a name="step-3-adding-a-data-web-control-and-configuring-it-for-data-modification"></a>3 단계: 데이터 웹 컨트롤을 추가 하 고 데이터 수정에 대 한 구성

ObjectDataSource가 페이지에 추가 하 고 구성 된 준비가 데이터 웹 컨트롤 모두 데이터를 표시 하 고 수정 하는 최종 사용자에 대 한 수단을 제공 하려면 페이지를 추가 합니다. 살펴보게 GridView, DetailsView, 및 FormView 개별적으로 이러한 데이터 웹 컨트롤 다르게 데이터 수정 기능 및 구성 합니다.

보겠습니다이 문서의 나머지 부분에서 매우 기본적인 편집, 삽입 및 삭제 DetailsView, GridView 통한 지원이 추가 되 고 FormView 제어 작업은 실제로을 확인란 정도 확인 하는 중입니다. 많은 미묘한 및 방금 가리키고 클릭 보다 훨씬 복잡된 이러한 기능을 제공 하는 실제 세계 경계 사례가 있습니다. 그러나이 자습서에서는 단순한 데이터 수정 기능에 증명에 전적으로 중점을 둡니다. 이후 자습서의 경우에 실제 설정에 발생 하는 문제를 검사 합니다.

## <a name="deleting-data-from-the-gridview"></a>GridView에서 데이터 삭제

GridView 디자이너 도구 상자에서 끌어 시작 합니다. 다음으로 GridView의 스마트 태그에서 드롭 다운 목록에서 선택 하 여는 ObjectDataSource GridView에 바인딩하십시오. 이 시점에서 GridView의 선언적 태그가 됩니다.


[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample4.aspx)]

스마트 태그를 통해 ObjectDataSource에 GridView 바인딩 두 가지 이점이 있습니다.

- BoundFields 및 CheckBoxFields 각는 ObjectDataSource에서 반환 된 필드에 대해 자동으로 만들어집니다. 또한, BoundField 및 CheckBoxField의 속성에 기본 필드의 메타 데이터에 따라 설정 됩니다. 예를 들어는 `ProductID`, `CategoryName`, 및 `SupplierName` 필드의 읽기 전용으로 표시 됩니다는 `ProductsDataTable` 안 수 있으므로 업데이트할 수 있는 편집 하는 경우. 이, 이러한 BoundFields'를 수용 하기 위해 [ReadOnly 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.boundfield.readonly(VS.80).aspx) 로 설정 `true`합니다.
- [DataKeyNames 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.datakeynames(VS.80).aspx) 내부 개체의 기본 키 필드에 할당 됩니다. 이 필수적인 경우이 속성 필드 (또는 필드 집합)으로 GridView 편집 하거나 데이터를 삭제 하기 위해 사용 하 여 고유한 각 레코드를 식별 합니다. 대 한 자세한 내용은 `DataKeyNames` 속성을 다시 참조는 [마스터/세부 정보 DetailView 선택 가능한 마스터 GridView 사용에 대해 자세히 설명](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) 자습서입니다.

GridView 속성 창이 나 선언 구문을 통해 ObjectDataSource에 바인딩될 수, 하는 동안 이렇게에 수동으로 추가 해야 적절 한 BoundField 및 `DataKeyNames` 태그입니다.

GridView 컨트롤 행 수준 편집 및 삭제에 대 한 기본 제공 지원을 제공합니다. 삭제를 지원 하려면 GridView 구성 삭제 단추는 열을 추가 합니다. 최종 사용자가 특정 행에 대 한 삭제 단추를 클릭 하면 포스트백 계속 하 고 다음 단계를 수행 하는 GridView 합니다.

1. ObjectDataSource의 `DeleteParameters` 값 할당
2. ObjectDataSource의 `Delete()` 메서드가 호출 되 면 지정된 된 레코드를 삭제 합니다.
3. GridView에 다시 바인딩합니다 자체는 ObjectDataSource를 호출 하 여 해당 `Select()` 메서드

에 할당 된 값은 `DeleteParameters` 의 값에 `DataKeyNames` 인 삭제 단추를 클릭 한 행에 대 한 필드입니다. 따라서 것이 중요 하는 GridView `DataKeyNames` 속성이 올바르게 설정 합니다. 없을 경우는 `DeleteParameters` 할당할는 `null` 값이 다시 발생 하지 않을 모든 단계 1에서 2 단계에서에서 레코드를 삭제 합니다.

> [!NOTE]
> `DataKeys` GridView의 컨트롤 상태에 있음을 의미 하는 컬렉션은 저장 된 `DataKeys` GridView의 뷰 상태 비활성화 된 경우에 다시 게시를 통해 값이 저장 됩니다. 그러나 것이 매우 중요 한 상태 보기를 지 원하는 편집 또는 삭제 (기본 동작) Gridview에 대 한 사용 하도록 설정 되어 있습니다. GridView s를 설정 하면 `EnableViewState` 속성을 `false`, 편집 및 삭제 동작이 올바로 작동 한 명의 사용자에 대 한 있지만 이러한 동시 사용자가 실수로 있습니다 가능성 있는 데이터를 삭제 하는 동시 사용자 인 경우 삭제 또는 편집 레코드는 않았음에도 t 추가할지 여부. 내 블로그 항목을 참조 [경고: 동시성 문제가 있는 ASP.NET 2.0 Gridview/DetailsView/FormViews 해당 편집을 원하는 및/또는 삭제 및 뷰 상태를 사용 하지 않으면](http://scottonwriting.net/sowblog/archive/2006/10/03/163215.aspx), 자세한 정보에 대 한 합니다.


이 동일한 경고 DetailsViews FormViews에도 적용 됩니다.

삭제 기능에는 GridView를 추가 하려면 스마트 태그에 이동 하 고 삭제 사용 확인란을 선택 합니다.


![확인 확인란 삭제 사용](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image24.png)

**그림 10**: 삭제 확인란 사용 확인


GridView에는 CommandField 추가 스마트 태그에서 삭제 사용 확인란을 선택 합니다. 다음 작업 중 하나 이상을 수행 하기 위한 단추가 있는 GridView에서 열을 렌더링 하는 CommandField:는 레코드를 선택 하는 레코드를 편집 하 고 레코드를 삭제 합니다. 이전에 CommandField에서 레코드를 선택 하면 작업에서 살펴본는 [마스터/세부 정보 DetailView 선택 가능한 마스터 GridView 사용에 대해 자세히 설명](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) 자습서입니다.

CommandField 번호가 `ShowXButton` 속성을 나타내는 어떤 일련의 단추는 CommandField에 표시 됩니다. CommandField 삭제 사용 확인란을 선택 하 여 해당 `ShowDeleteButton` 속성은 `true` GridView의 Columns 컬렉션에 추가 되었습니다.


[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample5.aspx)]

이 시점에서 믿을 지 모르겠지만, 작업이 끝났을 GridView에 대 한 삭제 사항! 그림 11에서 볼 수 있듯이 Delete 단추의 열 브라우저를 통해이 페이지를 방문 있는 경우에 합니다.


[![CommandField 삭제 단추 열 추가](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image26.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image25.png)

**그림 11**:는 CommandField는 열을 삭제 단추가 추가 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image27.png))


구축한 경험이이 자습서에서는 처음부터 직접 클릭 하면이 페이지를 테스트할 때 삭제 단추는 예외가 발생 합니다. 계속 이러한 예외 발생 이유 및 패키지를 수정 하는 방법에 대 한 자세한 내용은 읽어보세요.

> [!NOTE]
> 이 자습서와 함께 제공 되는 다운로드를 사용 하 여 따라 했다면, 하는 경우 이러한 문제는 이미 대상으로 고려 합니다. 그러나 확인해 발생할 수 있는 문제 및 적합 한 해결 방법을 확인 하려면 아래에 나열 된 세부 정보를 읽을 수 있습니다.


해당 메시지는 예외를 제품을 삭제 하려고 하면 발생 하는 경우 "*ObjectDataSource 'ObjectDataSource1' 매개 변수가 있는 ' DeleteProduct' 제네릭이 아닌 메서드를 찾을 수 없습니다: 원래 productID\_ ProductID*, "가능성이 제거 하지 않았습니다 고 `OldValuesParameterFormatString` 는 ObjectDataSource에서 속성입니다. 와 `OldValuesParameterFormatString` 둘 다에 전달 하려는 시도 ObjectDataSource 속성을 지정 `productID` 및 `original_ProductID` 입력 매개 변수는 `DeleteProduct` 메서드. `DeleteProduct`그러나만 단일 입력된 매개 변수를 허용, 따라서 예외입니다. 제거는 `OldValuesParameterFormatString` 속성 (속성을 설정 또는 `{0}`)는 원래 입력된 매개 변수를 전달 하려고 하 ObjectDataSource 지시 합니다.


[![OldValuesParameterFormatString 속성 처리가 지워졌습니다 확인](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image29.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image28.png)

**그림 12**: 확인 된 `OldValuesParameterFormatString` 속성에 된 선택이 취소 아웃 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image30.png))


제거 했던 경우에는 `OldValuesParameterFormatString` 속성을 계속 받아볼 수 예외 메시지와 함께 제품을 삭제 하려고 할 때: "*DELETE 문은 참조 제약 조건과 충돌 했습니다. ' FK\_순서\_세부 정보 \_제품의*. " Northwind 데이터베이스 간 외래 키 제약 조건을 포함 된 `Order Details` 및 `Products` 테이블, 즉 제품에 대 한 하나 이상의 레코드가 있는 경우 시스템에서 삭제할 수 없습니다는 `Order Details` 테이블입니다. Northwind 데이터베이스의 모든 제품 하나 이상의 레코드에 있으므로 `Order Details`, 제품의 관련된 주문 세부 정보 레코드를 먼저 삭제 될 때까지 제품을 모두 삭제할 수 없습니다.


[![제품 삭제를 금지 하는 외래 키 제약 조건](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image32.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image31.png)

**그림 13**: 제품 삭제를 금지 하는 외래 키 제약 조건 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image33.png))


이 자습서에 대 한 보겠습니다 삭제에 레코드가 모두는 `Order Details` 테이블입니다. 실제 응용 프로그램에서 해야 하나:

- 주문 세부 정보를 관리할 수 있는 다른 화면이 있어야 합니다.
- 확장 하 고 `DeleteProduct` 지정한 제품의 주문 정보를 삭제 하는 논리를 포함 하는 메서드
- 지정된 된 제품의 주문 정보 삭제를 포함 하도록 TableAdapter에서 사용 하는 SQL 쿼리를 수정 합니다.

방금에서 레코드를 모두 삭제는 `Order Details` foreign key 제약 조건을 방지 하기 위해 테이블입니다. Visual Studio에서 서버 탐색기로 이동 마우스 오른쪽 단추로 클릭는 `NORTHWND.MDF` 노드를 새 쿼리를 선택 합니다. 그런 다음 쿼리 창에서 다음 SQL 문을 실행 합니다.`DELETE FROM [Order Details]`


[![Order Details 테이블에서 모든 레코드를 삭제 합니다.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image35.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image34.png)

**그림 14**: 모든 레코드가 삭제는 `Order Details` 테이블 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image36.png))


정리 후는 `Order Details` 테이블 삭제 단추를 클릭 하는 오류 없이 제품 삭제 됩니다. 삭제 단추를 클릭 하 여 제품 삭제 되지 않습니다, GridView의 되도록 확인 `DataKeyNames` 기본 키 필드 속성 (`ProductID`).

> [!NOTE]
> 삭제 단추를 클릭 하면 계속 다시 게시 하 고 레코드가 삭제 됩니다. 실수로 잘못 된 행의 삭제 단추를 클릭할 수 있기 때문에 위험할 수 있습니다. 이후 자습서에서 레코드를 삭제 하는 경우 클라이언트 쪽 확인 메시지를 추가 하는 방법을 살펴보겠습니다.


## <a name="editing-data-with-the-gridview"></a>GridView 사용 하 여 데이터를 편집합니다.

삭제, 함께 GridView 컨트롤은 또한 기본적으로 행 수준 편집 지원을 제공합니다. 편집을 지원 하려면 GridView 구성 편집 단추 열을 추가 합니다. 행의 편집 단추는 해당 편집 가능 될 행을 클릭 하면 최종 사용자의 관점에서 기존 값을 포함 하 고 업데이트로 편집 단추 및 취소 단추를 교체 하는 텍스트 상자에 있는 셀을 켭니다. 원하는 변경에 확인 한 후 최종 사용자는 변경 내용을 적용 하려면 [업데이트] 단추 또는 내용을 취소 하려면 취소 단추를 클릭 수 합니다. 두 경우 모두, 업데이트 또는 취소 클릭 한 후 GridView 미리 편집 상태로 돌아갑니다.

페이지 개발자의 관점에서 최종 사용자가 특정 행에 대 한 편집 단추를 클릭 하면 계속 다시 게시 하 고 다음 단계를 수행 하는 GridView:

1. GridView의 `EditItemIndex` 속성이 있는 편집 단추를 클릭 한 행의 인덱스에 할당 됩니다
2. GridView에 다시 바인딩합니다 자체는 ObjectDataSource를 호출 하 여 해당 `Select()` 메서드
3. 일치 하는 행 인덱스는 `EditItemIndex` "편집 모드입니다." 렌더링 이 모드에서는 편집 단추는 업데이트 및 취소 단추 및 BoundFields로 대체 인 `ReadOnly` 속성은 False (기본값) TextBox 웹 갖는 컨트롤로 렌더링 되는 `Text` 속성은 데이터 필드의 값에 할당 됩니다.

이 시점에서 태그를 최종 사용자가 행의 데이터를 변경 하려면 브라우저에 반환 됩니다. 사용자가 업데이트 단추를 클릭 하면 포스트백 발생 하 고 다음 단계를 수행 하는 GridView.

1. ObjectDataSource의 `UpdateParameters` 값 GridView의 편집 인터페이스에 최종 사용자가 입력 한 값이 할당 됩니다
2. ObjectDataSource의 `Update()` 메서드가 호출 되 면 지정된 된 레코드를 업데이트 합니다.
3. GridView에 다시 바인딩합니다 자체는 ObjectDataSource를 호출 하 여 해당 `Select()` 메서드

에 할당 된 기본 키 값은 `UpdateParameters` 1 단계에서 지정 된 값에서 제공 된 `DataKeyNames` 속성을 기본이 아닌 키 값은 편집된 된 행에 대 한 TextBox 웹 컨트롤의 텍스트에서 제공 하는 반면 합니다. 와 마찬가지로 삭제, 중요 하는 GridView `DataKeyNames` 속성이 올바르게 설정 합니다. 없을 경우는 `UpdateParameters` 기본 키 값을 할당할는 `null` 값에는 발생 하지 것입니다 단계 1에서 2 단계에서에서 레코드를 업데이트 합니다.

단순히 GridView의 스마트 태그에 있는 편집 사용 확인란을 선택 하 여 편집 기능을 활성화할 수 있습니다.


![확인 확인란 편집 사용](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image37.png)

**그림 15**: 편집 확인란 사용 확인


편집 사용 확인란 (필요한 경우)는 CommandField를 추가 합니다를 확인 하 고 집합의 `ShowEditButton` 속성을 `true`합니다. 앞에서 설명한 대로 CommandField의 수를 포함 하는 `ShowXButton` 속성을 나타내는 어떤 일련의 단추는 CommandField에 표시 됩니다. 추가 편집 사용 확인란을 선택는 `ShowEditButton` 속성을 기존 CommandField:


[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample6.aspx)]

그 하는 데 필요한 기본적인 편집 지원을 추가 합니다. 그림 16 에서처럼 편집 인터페이스는 다소 조잡 각 BoundField 인 `ReadOnly` 속성이 `false` (기본값)를 맞추면 TextBox로 렌더링 됩니다. 과 같은 필드 여기에 `CategoryID` 및 `SupplierID`는 다른 테이블에는 키입니다.


[![Chai의 편집 단추를 클릭 하면 행이 편집 모드에 표시](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image39.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image38.png)

**그림 16**: 편집 모드에는 행을 표시 하는 클릭 하면 Chai의 편집 단추 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image40.png))


외래 키 값을 직접 편집 하는 사용자가 요구할 뿐 아니라 편집 인터페이스의 인터페이스는 다음과 같은 방법으로 없는:

- 사용자가 입력 한 `CategoryID` 또는 `SupplierID` 데이터베이스에 존재 하지 않는 `UPDATE` 예외를 발생 외래 키 제약 위반 합니다.
- 편집 인터페이스는 모든 유효성 검사를 포함 되지 않습니다. 필수 값을 제공 하지 않으면 (예: `ProductName`), 숫자 값 (예: "너무 많이!"을 입력 필요한 문자열 값을 입력 하거나 에 `UnitPrice` textbox), 예외가 throw 됩니다. 이후 자습서를 편집 하는 사용자 인터페이스에 유효성 검사 컨트롤을 추가 하는 방법을 검사 합니다.
- 현재 *모든* 제품 아닌 필드는 읽기 전용 GridView에 포함 되어야 합니다. GridView에서 필드를 제거 하는 것, 예를 들어 `UnitPrice`GridView 데이터 업데이트를 설정 하지 않아야 하는 경우는 `UnitPrice` `UpdateParameters` 값으로, 데이터베이스 레코드의 변경 `UnitPrice` 에 `NULL` 값입니다. 마찬가지로 경우 필수 필드와 같은 `ProductName`, 제거 되 동일한 GridView에서 업데이트가 실패 합니다 "*'ProductName' 열에서 null을 허용 하지*" 위에서 언급 한 예외입니다.
- 편집 인터페이스 서식을 개선의 여지가 않기도 합니다. `UnitPrice` 소수점이 하 4와 함께 표시 됩니다. 이상적으로 `CategoryID` 및 `SupplierID` 값 범주와 공급 업체 시스템에 나열 된 dropdownlist 활용 포함 됩니다.

다음은 하지만 지금은 대 한 라이브 해야 하는 모든 단점 이후 자습서에서 해결 합니다.

## <a name="inserting-editing-and-deleting-data-with-the-detailsview"></a>삽입, 편집 및 DetailsView 사용 하 여 데이터를 삭제 합니다.

이전 자습서에서 살펴본 대로 DetailsView 컨트롤 한 번에 한, GridView 처럼 한 레코드를 표시, 편집 및 현재 표시 된 레코드의 삭제에 대 한 허용 합니다. GridView의는 모두 최종 사용자의 경험을 편집 하 고 DetailsView 및 ASP.NET 측면에서 워크플로에서 항목을 삭제 합니다. DetailsView GridView에서와 다른 위치 삽입 기본 제공 지원을 제공 한다는입니다.

GridView의 데이터 수정 기능을 보여 주기 위해 DetailsView에 추가 하 여 시작는 `Basics.aspx` 위에 기존 GridView 페이지 하 고 DetailsView의 스마트 태그를 통해 기존 ObjectDataSource에 바인딩합니다. DetailsView의 비웁니다 다음 `Height` 및 `Width` 속성 및 스마트 태그에서 페이징 사용 옵션을 확인 합니다. 편집을 사용 하려면 삽입 및 삭제를 지원 하기만 하면 스마트 태그에 편집 사용, 삽입 사용 및 삭제 사용 확인란을 확인 합니다.


![DetailsView 편집, 삽입 및 삭제 지원 구성](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image41.png)

**그림 17**: 편집, 삽입 및 삭제 지원으로 DetailsView를 구성 합니다.


으로 편집, 추가 GridView와 삽입 또는 삭제가 지원은 CommandField에 추가 DetailsView, 선언적 구문은 다음과 같이 됩니다.


[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample7.aspx)]

이때는 CommandField DetailsView에 대 한 기본적으로 열 컬렉션의 끝에 나타납니다. DetailsView의 필드가으로 렌더링 되는 이후 행, 편집 및 삭제 단추 DetailsView의 맨 아래에 CommandField 삽입 된 행으로 나타납니다.


[![DetailsView 편집, 삽입 및 삭제 지원 구성](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image43.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image42.png)

**그림 18**: 편집, 삽입 및 삭제 지원으로 DetailsView 구성 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image44.png))


GridView에서와 마찬가지로 이벤트의 동일한 시퀀스를 시작 삭제 단추를 클릭 하면: 포스트백; a DetailsView의 ObjectDataSource 채우기 뒤 `DeleteParameters` 에 따라는 `DataKeyNames` 값 및 해당 ObjectDataSource를 호출 하 여 완료 `Delete()` 실제로 데이터베이스에서 제품을 제거 하는 메서드. DetailsView에서 편집도 하 고 있는 GridView의 동일한 방식으로 작동 합니다.

삽입에 대 한 최종 사용자는 새로 표시 됩니다 단추를 클릭 하면 "삽입 모드입니다." DetailsView를 렌더링 합니다. 삽입 및 취소 단추와 해당 BoundFields만으로 바뀝니다 새 단추 "삽입 모드" 인 `InsertVisible` 속성이로 설정 되어 `true` (기본값) 표시 됩니다. 와 같은 자동 증분 필드로 식별 된 데이터 필드 `ProductID`, 있어야 해당 [InsertVisible 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datacontrolfield.insertvisible(VS.80).aspx) 로 설정 `false` DetailsView 스마트 태그를 통해 데이터 소스에 바인딩하는 경우.

스마트 태그를 통해 DetailsView에 데이터 소스를 바인딩, Visual Studio 설정에서 `InsertVisible` 속성을 `false` 자동 증가 필드에 대해서만 합니다. 읽기 전용 필드와 같은 `CategoryName` 및 `SupplierName`, 하지 않는 한 "삽입 모드" 사용자 인터페이스에 표시 될 자신의 `InsertVisible` 속성이 명시적으로로 설정 된 `false`합니다. 이 두 필드를 설정 하려면 잠시 `InsertVisible` 속성을 `false`, 필드 편집 또는 DetailsView의 선언적 구문에서 스마트 태그에 연결 합니다. 그림 19 설정이 표시는 `InsertVisible` 속성을 `false` 필드 편집을 클릭 하 여 연결 합니다.


[![Northwind Traders는 이제 Acme 찻잔 제공](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image46.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image45.png)

**그림 19**: Northwind Traders 이제 제공 Acme 찻잔 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image47.png))


설정한 후의 `InsertVisible` 속성, 보기는 `Basics.aspx` 브라우저에서 페이지 하 고 새 단추를 클릭 합니다. 그림 20 새 음료를 추가할 때 DetailsView 표시 Acme 찻잔 우리의 제품 라인에 있습니다.


[![Northwind Traders는 이제 Acme 찻잔 제공](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image49.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image48.png)

**그림 20**: Northwind Traders 이제 제공 Acme 찻잔 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image50.png))


포스트백 Acme 찻잔에 대 한 세부 정보를 입력 하 고 삽입 단추를 클릭 한 후 계속 하 고 새 레코드에 추가 되는 `Products` 데이터베이스 테이블입니다. 데이터베이스 테이블에 있는 순서 대로 제품을 나열 하는이 DetailsView, 이후 우리 페이지로 이동해 마지막으로 제품 새 제품을 확인 하기 위해 합니다.


[![Acme 찻잔에 대 한 세부 정보](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image52.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image51.png)

**그림 21**: Acme 찻잔에 대 한 세부 정보 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image53.png))


> [!NOTE]
> DetailsView의 [CurrentMode 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.currentmode(VS.80).aspx) 표시 되는 인터페이스를 나타내며 다음 값 중 하나일 수 있습니다: `Edit`, `Insert`, 또는 `ReadOnly`합니다. [DefaultMode 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.defaultmode(VS.80).aspx) 나타내고 DetailsView 편집 후를 반환 하거나 삽입 모드 완료 되는 영구적으로 편집 하거나 삽입 모드 DetailsView를 표시할 때 유용 합니다.


GridView과 동일한 제한 사항이에서 저하 가리키고 클릭 삽입 및 DetailsView의 기능을 편집: 기존 사용자를 입력 해야 `CategoryID` 및 `SupplierID` textbox 통해 값; 인터페이스에 유효성 검사 논리, 모든 허용 하지 않는 제품 필드 `NULL` 값 또는 기본값이 없는 데이터베이스 수준에서 지정 된 값이 삽입 인터페이스에 포함 되어야 합니다.

기술을 살펴보겠습니다을 확장 하 고 향상 GridView의 편집 인터페이스 나중에 문서를 DetailsView 컨트롤의 편집 및 인터페이스를 삽입에 적용할 수 있습니다.

## <a name="using-the-formview-for-a-more-flexible-data-modification-user-interface"></a>FormView를 사용 하 여 보다 유연한 데이터 수정 사용자 인터페이스에 대 한

FormView는 데이터를 삽입, 편집 및 삭제에 대 한 기본 제공 지원을 제공 하지만 서식 파일 필드 대신 사용 하기 때문에 화면은 BoundFields 또는 데이터를 제공 하는 GridView 및 DetailsView 컨트롤에서 사용 하는 CommandField 추가 하려면 수정 인터페이스입니다. 대신, 사용자를 수집 하기 위한 웹 컨트롤이 새 항목을 추가 하는 경우 입력 또는 편집 함께 새로 만들기, 기존 구성을 편집, 삭제, 삽입, 업데이트 및 취소 단추에는이 인터페이스는 적절 한 서식 파일에 수동으로 추가 해야 합니다. 다행히도 Visual Studio 자동으로 만들어집니다에서 필요한 인터페이스 FormView 드롭 다운 목록에서의 스마트 태그를 통해 데이터 원본에 바인딩할 때.

을 설명 하기 위해 이러한 기법을 FormView를 추가 하 여 시작는 `Basics.aspx` 페이지이 고 FormView의 스마트 태그에서 이미 만든 ObjectDataSource에 바인딩합니다. 자동으로 생성 됩니다는 `EditItemTemplate`, `InsertItemTemplate`, 및 `ItemTemplate` 새로 만들기에 대 한 사용자의 입력 및 Button 웹 컨트롤을 수집 하는 것에 대 한 TextBox 웹 컨트롤이 FormView에 대 한 편집, 삭제, 삽입, 업데이트 및 취소 단추입니다. 또한: FormView `DataKeyNames` 기본 키 필드 속성 (`ProductID`)는 objectdatasource 반환 되는 개체입니다. 마지막으로, 스마트 태그는 FormView에서 페이징 사용 옵션을 확인 합니다.

다음 FormView의에 대 한 선언적 태그를 보여 줍니다. `ItemTemplate` FormView는 ObjectDataSource에 바인딩된 후 합니다. 기본적으로 각 부울이 아닌 값 제품 필드에 바인딩되어는 `Text` 하는 동안 각 부울 값 필드 레이블 웹 컨트롤의 속성 (`Discontinued`)에 바인딩된는 `Checked` 비활성화 된 CheckBox 웹 컨트롤의 속성입니다. 새로 만들기, 편집 및 삭제 단추를 클릭 하면 특정 FormView 동작 트리거를 명령적 되었을 자신의 `CommandName` 값으로 설정 되어 `New`, `Edit`, 및 `Delete`각각.


[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample8.aspx)]

그림 22 표시 FormView의 `ItemTemplate` 브라우저를 통해 볼 때. 각 제품 필드 새로 만들기, 편집 및 삭제 단추가 맨 아래에 나열 됩니다.


[![정렬과 FormView ItemTemplate 함께 새로운 각 제품 필드를 나열, 편집 및 삭제 단추](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image55.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image54.png)

**그림 22**: The 정렬과 FormView `ItemTemplate` 나열 각 제품 필드와 함께 새로 만들기, 편집 및 삭제 단추와 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image56.png))


GridView 및 삭제 단추 단추, LinkButton을 또는 ImageButton 클릭 하면 DetailsView와 함께 해당 `CommandName` 속성 다시 게시를 삭제 하면으로 설정 되어, ObjectDataSource의 채웁니다 `DeleteParameters` FormView의 기반`DataKeyNames`값을 ObjectDataSource의 호출 `Delete()` 메서드.

편집 단추를 클릭할 때 포스트백 계속 하 고 데이터를 다시 바인딩할 되는 `EditItemTemplate`, 편집 인터페이스 렌더링 담당 하는 합니다. 이 인터페이스는 업데이트 및 취소 단추와 함께 데이터를 편집 하기 위한 웹 컨트롤을 포함 합니다. 기본 `EditItemTemplate` 에 의해 생성 된 Visual Studio에는 모든 자동 증가 필드에 대 한 레이블을 (`ProductID`), 각 부울이 아닌 값 필드에 대 한 텍스트 상자 및 각 부울 값 필드에 대 한 확인란을 선택 합니다. 이 동작은 GridView 및 DetailsView 컨트롤에 자동으로 생성 된 BoundFields 매우 비슷합니다.

> [!NOTE]
> FormView의 자동으로 생성 한 가지 작은 문제는 `EditItemTemplate` 렌더링 TextBox 웹은 읽기 전용과 같은 해당 필드에 대 한 제어는 `CategoryName` 및 `SupplierName`합니다. 이 고려 하는 방법을 살펴보려는 곧 합니다.


TextBox 컨트롤에 `EditItemTemplate` 가 자신의 `Text` 속성에 사용 하는 해당 데이터 필드의 값에 바인딩할 *양방향 데이터 바인딩을*합니다. 양방향 데이터 바인딩을 가리키는 `<%# Bind("dataField") %>`, 서식 파일에 데이터 바인딩 및 삽입 또는 레코드 편집 하기 위한 ObjectDataSource의 매개 변수를 채울 때 두 데이터 바인딩을 수행 합니다. 즉, 사용자가 클릭할 때에서 편집 단추는 `ItemTemplate`, `Bind()` 메서드가 지정 된 데이터 필드 값을 반환 합니다. 값이를 사용 하 여 지정 된 데이터 필드에 해당 하는 다시 게시 변경한 사용자를 업데이트 후 `Bind()` ObjectDataSource의에 적용 되 `UpdateParameters`합니다. 단방향 데이터 바인딩 표시 또는 `<%# Eval("dataField") %>`만 서식 파일에 데이터를 바인딩할 때 데이터 필드 값을 검색 하는 *하지* 다시 게시 될 때 데이터 원본 매개 변수를 사용자가 입력 한 값을 반환 합니다.

다음 선언 태그 표시 FormView의 `EditItemTemplate`합니다. `Bind()` 메서드 여기 구문이 사용 되 고 업데이트 및 취소 단추 웹 컨트롤에는 해당 `CommandName` 속성이 적절 하 게 설정 합니다.

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample9.aspx)]

우리의 `EditItemTemplate`, 지금은,를 사용 하려고 하면 throw 하면 예외가 발생 합니다. 문제는 `CategoryName` 및 `SupplierName` TextBox 웹에 컨트롤로 렌더링 되는 필드는 `EditItemTemplate`합니다. 하거나 이러한 입력란 레이블을 변경 하거나 완전히 제거 해야 합니다. 단순히에서 완전히 삭제는 `EditItemTemplate`합니다.

그림 23 chai 편집 버튼을 클릭 한 후 브라우저에서 FormView를 보여 줍니다. `SupplierName` 및 `CategoryName` 에 표시 된 필드는 `ItemTemplate` 에서 제거한 것으로 표시 되어 더 이상는 `EditItemTemplate`합니다. 업데이트 단추를 클릭할 때 FormView GridView 및 DetailsView 컨트롤으로 동일한 일련의 단계를 진행 합니다.


[![기본적으로는 EditItemTemplate TextBox 또는 확인란으로 각 편집 가능한 제품 필드를 표시](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image58.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image57.png)

**그림 23**: 기본적으로 `EditItemTemplate` 표시 Each 편집 가능한 제품 필드 TextBox 또는 확인란 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image59.png))


삽입 단추 FormView의를 클릭할 때 `ItemTemplate` 포스트백 계속 합니다. 그러나 데이터가 없는 새 레코드를 추가 하는 FormView에 바인딩됩니다. `InsertItemTemplate` 인터페이스 삽입 및 취소 단추와 함께 새 레코드를 추가 하기 위한 웹 컨트롤에 포함 되어 있습니다. 기본 `InsertItemTemplate` 에 의해 생성 된 각 부울이 아닌 값 필드에 대 한 텍스트 상자와 비슷한 자동으로 생성 된 각 부울 값 필드에 대 한 확인란을 포함 하는 Visual Studio `EditItemTemplate`의 인터페이스입니다. TextBox 컨트롤에는 해당 `Text` 속성 양방향 데이터 바인딩을 사용 하 여 해당 데이터 필드의 값에 바인딩합니다.

다음 선언 태그 표시 FormView의 `InsertItemTemplate`합니다. `Bind()` 메서드 여기 구문이 사용 되 고 삽입 및 취소 단추 웹 컨트롤에는 해당 `CommandName` 속성이 적절 하 게 설정 합니다.


[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample10.aspx)]

FormView의 자동으로 생성 된 때 주의 해야 하는 `InsertItemTemplate`합니다. TextBox 웹 컨트롤은 읽기 전용과 같은 해당 필드에 대해서도 생성 됩니다 특히 `CategoryName` 및 `SupplierName`합니다. 와 함께 `EditItemTemplate`에서 이러한 입력란을 제거 해야는 `InsertItemTemplate`합니다.

그림 24 Acme 커피 새 제품을 추가 하는 경우 브라우저에서 FormView를 보여 줍니다. `SupplierName` 및 `CategoryName` 에 표시 된 필드는 `ItemTemplate` 방금 제거한 것으로 표시 되어 더 이상. 삽입 단추 DetailsView 컨트롤과 같은 일련의 단계를 통해 FormView 수입을 누르면에 새 레코드를 추가 `Products` 테이블입니다. 그림 25 삽입 한 후 FormView의 Acme 커피 제품 세부 정보를 보여 줍니다.


[![InsertItemTemplate FormView의 삽입 인터페이스를 지정합니다.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image61.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image60.png)

**그림 24**:는 `InsertItemTemplate` FormView의 삽입 인터페이스를 나타냅니다 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image62.png))


[![FormView 신제품 Acme 커피에 대 한 세부 정보가 표시 됩니다.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image64.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image63.png)

**그림 25**: FormView에 새 제품 Acme 커피에 대 한 세부 정보 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image65.png))


읽기 전용 구분해,으로 편집 하 고 세 개의 별도 템플릿이 인터페이스 삽입 FormView DetailsView 및 GridView 보다 더 세부적인 수준의 이러한 인터페이스에 대 한 제어에 대 한 허용 됩니다.

> [!NOTE]
> DetailsView, FormView의 같은 `CurrentMode` 속성은 표시 되는 인터페이스를 나타냅니다 및 해당 `DefaultMode` 속성 모드를 나타내며 FormView 돌아갑니다 편집 후 또는 삽입 완료 되었습니다.


## <a name="summary"></a>요약

이 자습서에서는 삽입, 편집 및 GridView, DetailsView, 및 FormView를 사용 하 여 데이터를 삭제 하는 기본적인 검사 했습니다. 이러한 컨트롤의 세 가지 모두 특정 수준의 데이터 웹 컨트롤 및는 ObjectDataSource 덕분에 ASP.NET 페이지에 코드를 전혀 작성 하지 않고도 사용할 수 있는 기본 제공 데이터 수정 기능을 제공 합니다. 그러나 단순 가리키고 상당히 frail 기술 렌더링 및 naïve 데이터 수정 사용자 인터페이스를 클릭 합니다. 유효성 검사를 제공 하려면 프로그래밍 방식으로 값을 삽입할 정상적으로 예외 처리, 사용자 인터페이스 사용자 지정 및, 해야 다음 여러 자습서를 통해 설명 하는 방법 표시에 의존 합니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

>[!div class="step-by-step"]
[다음](examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)
