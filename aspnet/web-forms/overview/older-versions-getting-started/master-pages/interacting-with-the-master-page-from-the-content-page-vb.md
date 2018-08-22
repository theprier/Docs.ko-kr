---
uid: web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-master-page-from-the-content-page-vb
title: 콘텐츠 페이지 (VB)에서 마스터 페이지와 상호 작용 | Microsoft Docs
author: rick-anderson
description: 메서드를 호출, 콘텐츠 페이지의 코드에서 마스터 페이지의 등 속성을 설정 하는 방법을 검사 합니다.
ms.author: riande
ms.date: 07/11/2008
ms.assetid: 081fe010-ba0f-4e7d-b4ba-774840b601c2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-master-page-from-the-content-page-vb
msc.type: authoredcontent
ms.openlocfilehash: 59a00305cdcaf41ac0b37649382b9c3dc9ce1b0c
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828666"
---
<a name="interacting-with-the-master-page-from-the-content-page-vb"></a>콘텐츠 페이지 (VB)에서 마스터 페이지와 상호 작용
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_06_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_06_VB.pdf)

> 메서드를 호출, 콘텐츠 페이지의 코드에서 마스터 페이지의 등 속성을 설정 하는 방법을 검사 합니다.


## <a name="introduction"></a>소개

마스터 페이지를 만드는 방법을 살펴봤습니다 지난 5 자습서의이 코스를 통해 콘텐츠 영역을 정의 하 고 마스터 페이지, ASP.NET 페이지 바인딩할 페이지별 내용을 정의 합니다. 방문자를 특정 콘텐츠 페이지를 요청 하면 콘텐츠 및 마스터 페이지의 태그는 결합 런타임에 통합된 컨트롤 계층 구조를 렌더링에 발생 합니다. 따라서 이미 살펴본 콘텐츠 페이지의 마스터 페이지와 상호 작용할 수 있는 방법의 하나: 콘텐츠 페이지를 마스터 페이지의 ContentPlaceHolder 컨트롤로 transfuse 태그를 제시 합니다.

새로운 아직 검사할 마스터 페이지 및 콘텐츠 페이지를 프로그래밍 방식으로 작용 하는 방법입니다. 마스터 페이지의 ContentPlaceHolder 컨트롤에 대 한 태그를 정의 하는 것 외에도 콘텐츠 페이지 수도 해당 마스터 페이지의 공용 속성에 값을 할당 및 해당 public 메서드를 호출 합니다. 마찬가지로, 마스터 페이지 콘텐츠 페이지와 상호 작용할 수 있습니다. 프로그래밍 방식으로 상호 마스터 및 콘텐츠 페이지는 선언적 마크업 간의 상호 작용 보다는 덜 일반적인 상태인 동안에 이러한 프로그래밍 방식 상호 작용 필요한 많은 시나리오가 있습니다.

이 자습서에서는 검사 콘텐츠 페이지의 마스터 페이지를 사용 하 여 프로그래밍 방식으로 작용 하는 방법 다음 자습서에서 마스터 페이지는 콘텐츠 페이지와 마찬가지로 조작할 수 있는 방법을 살펴보겠습니다.

## <a name="examples-of-programmatic-interaction-between-a-content-page-and-its-master-page"></a>콘텐츠 페이지와 해당 마스터 페이지 간의 프로그래밍 방식 상호 작용의 예

페이지의 특정 지역에서 페이지 별로 구성 하면 ContentPlaceHolder 컨트롤을 사용 합니다. 하지만 대부분의 페이지를 특정 출력을 만들지만 소수의 페이지를 내보냅니다 해야 하는 경우를 다른 항목이 표시 되도록 사용자 지정 해야 하는 어떨까요? 하나 이러한 예제에서 검사할 합니다 [ *여러 ContentPlaceHolders 및 기본 콘텐츠* ](multiple-contentplaceholders-and-default-content-vb.md) 자습서에는 각 페이지에는 로그인 인터페이스를 표시 합니다. 대부분의 페이지는 로그인 인터페이스를 포함 해야 하는 동안 않아야 소수의 페이지에 대 한 예: 기본 로그인 페이지 (`Login.aspx`); 계정 만들기 페이지 및 인증 된 사용자에 게 액세스할 수 있는 다른 페이지입니다. 합니다 [ *여러 ContentPlaceHolders 및 기본 콘텐츠* ](multiple-contentplaceholders-and-default-content-vb.md) 자습서에서는 마스터 페이지에 ContentPlaceHolder에 대 한 기본 콘텐츠를 정의 하는 방법을 보여 주었습니다. 및 다음에 재정의 하는 방법 페이지 위치를 기본 콘텐츠 원했던 없습니다.

또 다른 옵션 공용 속성 또는 로그인 인터페이스를 표시할지 여부를 나타내는 마스터 페이지 내에서 메서드를 만드는 것입니다. 마스터 페이지 라는 public 속성이 포함 될 수 있습니다 예를 들어 `ShowLoginUI` 값은 설정 하는 데 사용 된는 `Visible` 마스터 페이지에서 로그인 컨트롤의 속성입니다. 로그인 사용자 인터페이스를 표시 하지 않아야 하는 이러한 콘텐츠 페이지에 프로그래밍 방식으로 설정할 수 있습니다 다음 합니다 `ShowLoginUI` 속성을 `False`입니다.

아마도 콘텐츠와 마스터 페이지 상호 작용의 가장 일반적인 예에는 콘텐츠 페이지의 일부 작업을 지났는지 후 새로 고쳐져 야 마스터 페이지 요구에 데이터가 표시 될 때 발생 합니다. 5를 가장 최근에 표시 되는 GridView를 포함 하는 마스터 페이지는 특정 데이터베이스 테이블에서 레코드를 추가 하는 것이 좋습니다. 하 고 해당 콘텐츠 페이지 중 하나는 같은 테이블에 새 레코드를 추가 하기 위한 인터페이스를 포함 합니다.

사용자가 새 레코드를 추가 하려면 페이지를 방문 하면 가장 최근에 추가 된 다섯 가지 마스터 페이지에 표시 된 레코드를 확인 합니다. 새 레코드의 열에 대 한 값을 채운 후 그녀는 폼을 전송 합니다. 마스터 페이지에 GridView에 가정 하 고 해당 `EnableViewState` (기본값)을 True로 설정 하는 속성을 보기 상태에서 해당 콘텐츠를 다시 로드를 데이터베이스에 새 레코드가 추가 된 경우에 5 개의 동일한 레코드가 표시 되는 결과적으로 합니다. 이 인해 사용자가 혼동할 수 있습니다.

> [!NOTE]
> 다시 포스트백이 발생할 때마다 해당 기본 데이터 원본에 바인딩하여 있도록 GridView의 뷰 상태를 해제 하는 경우에 여전히 표시 되지 않습니다 방금 추가 된 레코드 데이터 페이지 수명 주기를 datab에 새 레코드가 추가 되는 경우 보다 앞부분 GridView에 바인딩되기 때문에 ase 합니다.


방금 추가 된 레코드를 마스터 페이지에 표시 되도록이 해결 하의 포스트백 된 데이터 소스에 바인딩할 GridView 지시 해야 온 GridView *후* 새 레코드를 데이터베이스에 추가 되었습니다. 이렇게 하려면 마스터 페이지에서 새 레코드 및 해당 이벤트 처리기는 새로 고쳐져 야 하는 GridView 콘텐츠 페이지에 추가 하기 위한 인터페이스 이므로 콘텐츠 및 마스터 페이지 간의 상호 작용 합니다.

콘텐츠 페이지에 이벤트 처리기에서 마스터 페이지의 표시를 새로 고치는 콘텐츠와 마스터 페이지 상호 작용에 대 한 가장 일반적인 요구 사항 중 하나 이므로이 항목에서는 좀 더 자세히 살펴보겠습니다. 라는 Microsoft SQL Server 2005 Express Edition 데이터베이스를 포함 하는이 자습서에 대 한 다운로드가 `NORTHWIND.MDF` 웹 사이트에서 `App_Data` 폴더입니다. Northwind 데이터베이스는 제품, 직원 및 회사인 Northwind Traders에 대 한 판매 정보를 저장합니다.

마스터 페이지에 GridView에 제품 추가 하는 다섯 가지 가장 최근에 표시 안내 하는 1 단계. 2 단계는 새 제품을 추가 하는 것에 대 한 콘텐츠 페이지를 만듭니다. 3 단계에서 마스터 페이지에서 공용 속성 및 메서드를 만드는 방법 고 4 단계에는 콘텐츠 페이지에서 이러한 메서드와 속성을 사용 하 여 프로그래밍 방식으로 상호 작용 하는 방법을 보여 줍니다.

> [!NOTE]
> 이 자습서는 ASP.NET에서 데이터를 사용 하 여 작업의 세부 정보 자세히 하지 않습니다. 데이터 및 데이터를 삽입 하는 것에 대 한 콘텐츠 페이지를 표시 하려면 마스터 페이지를 설정 하기 위한 단계가 완료, 아직 breezy 합니다. 에 대 한 자세한 표시 및 데이터를 삽입 하 고 SqlDataSource 및 GridView 컨트롤을 사용 하 여,이 자습서의 끝에 추가 정보 섹션의 리소스를 참조 하세요.


## <a name="step-1-displaying-the-five-most-recently-added-products-in-the-master-page"></a>1 단계: 마스터 페이지에서 제품을 추가 5를 가장 최근에 표시

Site.master 마스터 페이지를 열고 레이블 및 GridView 컨트롤을 추가 합니다 `leftContent` `<div>`합니다. 레이블의 지웁니다 `Text` 속성을 설정 해당 `EnableViewState` 속성을 `False`, 및 해당 `ID` 속성을 `GridMessage`; GridView의 설정 `ID` 속성을 `RecentProducts`입니다. 다음으로, 디자이너에서 GridView의 스마트 태그를 확장 하 고 새 데이터 원본에 연결 하려면 선택 합니다. 데이터 소스 구성 마법사가 시작 됩니다. Northwind 데이터베이스에 있으므로 합니다 `App_Data` 폴더는 Microsoft SQL Server 데이터베이스 선택 (그림 1 참조)를 선택 하 여 SqlDataSource를 만들지 않으면 SqlDataSource 이름을 `RecentProductsDataSource`입니다.


[![GridView RecentProductsDataSource 라는 SqlDataSource 컨트롤에 바인딩](interacting-with-the-master-page-from-the-content-page-vb/_static/image2.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image1.png)

**그림 01**: GridView 라는 SqlDataSource 컨트롤에 바인딩할 `RecentProductsDataSource` ([클릭 하 여 큰 이미지 보기](interacting-with-the-master-page-from-the-content-page-vb/_static/image3.png))


다음 단계를 요청에 연결할 데이터베이스 항목을 지정 합니다. 선택 된 `NORTHWIND.MDF` 데이터베이스 파일 드롭 다운 목록에서 다음을 클릭 합니다. 마법사에서 연결 문자열을 저장할 제공가 처음으로이 데이터베이스를 사용한 것 이기 때문에 `Web.config`입니다. 이름을 사용 하 여 연결 문자열을 저장 하 게 `NorthwindConnectionString`합니다.


[![Northwind 데이터베이스에 연결](interacting-with-the-master-page-from-the-content-page-vb/_static/image5.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image4.png)

**그림 02**: Northwind 데이터베이스에 연결 ([큰 이미지를 보려면 클릭](interacting-with-the-master-page-from-the-content-page-vb/_static/image6.png))


데이터 소스 구성 마법사는 데이터를 검색 하는 쿼리는 지정할 수 있습니다 하는 두 가지 방법을 제공 합니다.

- 사용자 지정 SQL 문 또는 저장된 프로시저를 지정 하 여 또는
- 테이블 또는 뷰를 선택 하 고 다음 반환할 열을 지정 하 여

방금 5 가장 최근에 추가 된 제품을 반환 하고자 하기 때문에 사용자 지정 SQL 문을 지정 해야 합니다. 다음 사용 하 여 `SELECT` 쿼리:


[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample1.sql)]

`TOP 5` 키워드는 쿼리에서 처음 다섯 개의 레코드만 반환 합니다. 합니다 `Products` 테이블의 기본 키 `ProductID`는 `IDENTITY` 우리 테이블에 추가 하는 각 새 제품 들이 있는 이전 항목 보다 큰 값을 보장 하는 열입니다. 따라서 기준으로 결과 정렬 `ProductID` 내림차순부터 가장 최근에 만든 제품을 반환 합니다.


[![5 개의 가장 최근에 추가 된 제품을 반환 합니다.](interacting-with-the-master-page-from-the-content-page-vb/_static/image8.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image7.png)

**그림 03**: 5 개의 가장 최근에 추가 제품을 반환 ([큰 이미지를 보려면 클릭](interacting-with-the-master-page-from-the-content-page-vb/_static/image9.png))


Visual Studio에서 마법사를 완료 한 후 표시할 GridView에 대 한 두 BoundFields 생성 합니다 `ProductName` 및 `UnitPrice` 데이터베이스에서 필드를 반환 합니다. 이 시점에서 마스터 페이지의 선언적 태그는 다음과 유사한 태그를 포함 해야 합니다.


[!code-aspx[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample2.aspx)]

태그를 포함 하는 알 수 있듯이: 웹 컨트롤 (`GridMessage`); GridView `RecentProducts`두 BoundFields; 이며 다섯 가지 가장 최근에 추가 된 제품을 반환 하는 SqlDataSource 컨트롤입니다.

이 사용 하 여 생성 하는 GridView, 구성, SqlDataSource 컨트롤 브라우저를 통해 웹 사이트를 방문 합니다. 그림 4에서 알 수 있듯이, 최근 5를 나열 하는 왼쪽된 아래 모퉁이에 표 추가 제품 표시 메시지가 표시 됩니다.


[![가장 최근에 추가 된 5 개 제품을 표시 하는 GridView](interacting-with-the-master-page-from-the-content-page-vb/_static/image11.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image10.png)

**그림 04**: 5 개의 가장 최근에 추가 제품을 표시 하는 GridView ([큰 이미지를 보려면 클릭](interacting-with-the-master-page-from-the-content-page-vb/_static/image12.png))


> [!NOTE]
> 자유롭게 GridView의 모양을 정리할 수 있습니다. 몇 가지 제안 사항이 포함 서식을 표시 `UnitPrice` 통화 및 표 모양 향상을 위해 배경색 및 글꼴을 사용 하는 값입니다.


## <a name="step-2-creating-a-content-page-to-add-new-products"></a>2 단계: 새 제품을 추가 콘텐츠 페이지 만들기

다음 작업은 사용자 수에 새 제품을 추가 하는 데는 콘텐츠 페이지를 만드는 것은 `Products` 테이블입니다. 새 콘텐츠 페이지를 추가 합니다 `Admin` 라는 폴더 `AddProduct.aspx`에 바인딩하지 하 여는 `Site.master` 마스터 페이지입니다. 그림 5는이 페이지는 웹 사이트에 추가한 후 솔루션 탐색기를 보여줍니다.


[![Admin 폴더를 새 ASP.NET 페이지를 추가 합니다.](interacting-with-the-master-page-from-the-content-page-vb/_static/image14.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image13.png)

**그림 05**: 새 ASP.NET 페이지를 추가 합니다 `Admin` 폴더 ([클릭 하 여 큰 이미지 보기](interacting-with-the-master-page-from-the-content-page-vb/_static/image15.png))


회수에 [ *마스터 페이지에서 제목, 메타 태그 및 기타 HTML 헤더 지정* ](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md) 자습서 라는 기본 페이지를 사용자 지정 클래스를 만들었습니다 `BasePage` 있었다면 페이지 제목 생성 명시적으로 설정 합니다. 로 이동 합니다 `AddProduct.aspx` 페이지의 코드 숨김 클래스에서 파생 되 게 하 고 `BasePage` (대신에서 `System.Web.UI.Page`).

마지막으로 업데이트 된 `Web.sitemap` 이 단원에 대 한 항목을 포함 하는 파일입니다. 아래에 다음 태그를 추가 합니다 `<siteMapNode>` 컨트롤 ID 이름 지정 문제 단원:


[!code-xml[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample3.xml)]

그림 6에서는이 추가 같이 `<siteMapNode>` 요소 단원 목록에 반영 됩니다.

돌아가서 `AddProduct.aspx`합니다. 콘텐츠 컨트롤에는 `MainContent` ContentPlaceHolder를 DetailsView 컨트롤을 추가 하 고 이름을 `NewProduct`입니다. DetailsView 라는 새 SqlDataSource 컨트롤을 바인딩할 `NewProductDataSource`합니다. 같은 Northwind 데이터베이스를 사용할 수 있도록 1 단계에서에서 SqlDataSource를 사용 하 여 마법사를 구성 하 고 사용자 지정 SQL 문 지정 하려면 선택 합니다. DetailsView를 사용 하 여 데이터베이스에 항목을 추가할 수는, 때문에 둘 다 지정 해야는 `SELECT` 문 및 `INSERT` 문입니다. 다음 사용 하 여 `SELECT` 쿼리:


[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample4.sql)]

그런 다음 삽입 탭에서 다음을 추가 `INSERT` 문:


[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample5.sql)]

마법사를 완료 한 후 DetailsView의 스마트 태그로 이동한 다음 "삽입 사용" 확인란을 확인 합니다. CommandField와 DetailsView를 추가 하는이 해당 `ShowInsertButton` 속성이 True로 설정 합니다. 이 DetailsView가 사용 되기 때문에 전적으로 데이터를 삽입, 설정 된 DetailsView `DefaultMode` 속성을 `Insert`입니다.

이것이 전부입니다! 이 페이지를 테스트해 보겠습니다. 방문 `AddProduct.aspx` 브라우저를 통해 이름과 가격 (그림 6 참조)를 입력 합니다.


[![데이터베이스에 새 제품 추가](interacting-with-the-master-page-from-the-content-page-vb/_static/image17.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image16.png)

**그림 06**: 데이터베이스에 새 제품 추가 ([큰 이미지를 보려면 클릭](interacting-with-the-master-page-from-the-content-page-vb/_static/image18.png))


이름 및 새 제품에 대 한 가격을 입력 한 후 삽입 단추를 클릭 합니다. 이렇게 하면 폼에 다시 게시 합니다. 포스트백에서 SqlDataSource 컨트롤의 `INSERT` 문이 실행 될; 두 매개 변수는 DetailsView의 두 텍스트 상자 컨트롤에서 사용자가 입력 한 값으로 채워집니다. 그러나 삽입이 발생 했음을 시각적 피드백이 있습니다. 새 레코드 추가 되어 있는지 확인 메시지 표시를 좋을 것입니다. 필자는 판독기에 대 한 연습으로 둡니다. 또한 DetailsView에서 새 레코드를 추가한 후 마스터 페이지에 GridView 계속 표시 하기 전에;와 동일한 5 개 레코드가 방금 추가 된 레코드는 포함 되지 않습니다. 이후 단계에서이 문제를 해결 하는 방법을 살펴보겠습니다.

> [!NOTE]
> 특정 형태의 삽입에 성공 하는 시각적 피드백을 추가 하는 것 외에도 바랍니다도 유효성 검사를 포함 된 DetailsView 삽입 인터페이스를 업데이트할 수 있습니다. 현재 검사 하지 않습니다. 사용자가에 대 한 잘못 된 값을 입력 합니다 `UnitPrice` 필드 "너무 비용이" 시스템에서 해당 문자열을 10 진수로 변환 하려고 할 때 다시 게시 될 때 예외가 throw 됩니다. 삽입 하는 사용자 지정 하는 방법은 인터페이스를 참조 합니다 [ *데이터 수정 인터페이스 사용자 지정* 자습서](https://asp.net/learn/data-access/tutorial-20-vb.aspx) 에서 내 [데이터자습서시리즈를사용하여작업](../../data-access/index.md).


## <a name="step-3-creating-public-properties-and-methods-in-the-master-page"></a>3 단계: 마스터 페이지에서 공용 속성 및 메서드 만들기

이라는 레이블 웹 컨트롤을 1 단계에서에서 추가한 `GridMessage` 마스터 페이지에 GridView 위에 있습니다. 필요에 따라 메시지를 표시 하려면이 레이블을 것입니다. 예를 들어, 새 레코드를 추가한 합니다 `Products` 테이블 하고자 할 수 있습니다 라는 메시지가 표시: "*ProductName* 데이터베이스에 추가 되었습니다." 하드 코드 마스터 페이지에서이 레이블에 대 한 텍스트를 대신 것이 좋습니다 메시지 콘텐츠 페이지에서 사용자 지정할 수입니다.

마스터 페이지 내에서 보호 된 멤버 변수로 레이블 컨트롤 구현 되기 때문에 콘텐츠 페이지에서 직접 액세스할 수 없습니다. 웹 컨트롤을 표시 하거나 해당 속성 중 하나는 수 프록시 역할을 하는 마스터 페이지에서 공용 속성을 생성 해야 마스터 페이지 콘텐츠 페이지에서 (또는 해당 문제를 마스터 페이지의 웹 컨트롤에 대 한) 내에서 레이블을 사용 하려면  액세스할 수 있습니다. 레이블의 노출 하기 위해 마스터 페이지의 코드 숨김 클래스에 다음 구문을 추가 `Text` 속성:


[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample6.vb)]

새 레코드를 추가할 때를 `Products` 콘텐츠 페이지에서 테이블을 `RecentProducts` 마스터 페이지에 GridView를 원본으로 사용 하는 데이터 원본 다시 바인딩 해야 합니다. GridView 호출을 다시 바인딩하도록 하려면 해당 `DataBind` 메서드. 마스터 페이지에 GridView 콘텐츠 페이지를 프로그래밍 방식으로 액세스할 수 없는 때문에 만들 필요가 공용 메서드를 마스터 페이지에서는 호출 될 때 것, 데이터를 GridView에 다시 바인딩합니다. 마스터 페이지의 코드 숨김 클래스에 다음 메서드를 추가 합니다.


[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample7.vb)]

사용 하 여는 `GridMessageText` 속성 및 `RefreshRecentProductsGrid` 메서드 내부에서 모든 콘텐츠 페이지 프로그래밍 방식으로 설정 하거나 읽을 수의 값을 `GridMessage` 레이블의 `Text` 속성 하거나 데이터를 다시는 `RecentProducts` GridView입니다. 4 단계에는 콘텐츠 페이지 로부터 마스터 페이지의 공용 속성 및 메서드에 액세스 하는 방법을 검사 합니다.

> [!NOTE]
> 마스터 페이지의 속성 및 메서드를 표시 해야 `Public`합니다. 경우를 명시적으로 나타내지 않습니다 이러한 속성 및 메서드 `Public`, 콘텐츠 페이지에서 액세스할 수 없습니다.


## <a name="step-4-calling-the-master-pages-public-members-from-a-content-page"></a>콘텐츠 페이지 로부터 마스터 페이지의 공용 멤버를 호출 하는 4 단계:

이제 마스터 페이지에 필요한 공용 속성 및 메서드 준비가 되었다고 이러한 속성 및 메서드를 호출 하 여 `AddProduct.aspx` 콘텐츠 페이지입니다. 특히 마스터 페이지의 설정 해야 `GridMessageText` 속성과 호출 해당 `RefreshRecentProductsGrid` 메서드 후 데이터베이스에 새 제품 추가 되었습니다. 모든 ASP.NET 데이터 웹 컨트롤 바로 앞 이나 쉽게 페이지 개발자가 프로그래밍 방식으로 작업 전이나 후 작업을 수행 하는 다양 한 작업을 완료 한 후 이벤트를 발생 합니다. 예를 들어 최종 사용자가 DetailsView의 삽입 단추를 클릭 하면에서 포스트백 DetailsView 발생 해당 `ItemInserting` 삽입 워크플로 시작 하기 전에 이벤트입니다. 그런 다음 데이터베이스에 레코드를 삽입 합니다. 그런 다음, DetailsView 발생 해당 `ItemInserted` 이벤트입니다. 따라서 새 제품 추가 된 후에 마스터 페이지를 사용 하기 위해 DetailsView의에 대 한 이벤트 처리기 만들기 `ItemInserted` 이벤트입니다.

콘텐츠 페이지의 마스터 페이지와 상호 작용할 수 프로그래밍 방식으로 두 가지가 있습니다.

- 사용 하 여 `Page.Master` 마스터 페이지에 느슨한 형 대 한 참조를 반환 하는 속성 또는
- 페이지의 마스터 페이지 형식 또는 파일 경로 통해 지정 된 `@MasterType` 지시문; 라는 페이지에 강력한 형식의 속성을 자동으로 추가이 `Master`합니다.

두 방법을 모두 살펴보겠습니다.

### <a name="using-the-loosely-typedpagemasterproperty"></a>느슨하게 형식화를 사용 하 여`Page.Master`속성

모든 ASP.NET 웹 페이지에서 파생 되어야 합니다는 `Page` 에 있는 클래스는 `System.Web.UI` 네임 스페이스입니다. 합니다 `Page` 클래스에 포함을 [ `Master` 속성](https://msdn.microsoft.com/library/system.web.ui.page.master.aspx) 페이지의 마스터 페이지에 대 한 참조를 반환 하는 합니다. 마스터 페이지는 페이지에 없는 경우 `Master` 반환 `Nothing`합니다.

합니다 `Master` 형식의 개체를 반환 [ `MasterPage` ](https://msdn.microsoft.com/library/system.web.ui.masterpage.aspx) (에 `System.Web.UI` 네임 스페이스) 모든 마스터 페이지에서 파생 되는 기본 형식입니다. 따라서를 사용 하 여 공용 속성에서는 캐스팅 해야 하는 웹 사이트의 마스터 페이지에 정의 된 메서드를 `MasterPage` 에서 반환 된 개체는 `Master` 속성을 적절 한 형식입니다. 마스터 페이지 파일 이름을 때문 `Site.master`, 코드 숨김 클래스 이름이 `Site`합니다. 따라서 다음 코드는 캐스팅 합니다 `Page.Master` 의 인스턴스에 대 한 속성을 `Site` 클래스입니다.


[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample8.vb)]

캐스팅 해는 느슨한 형 `Page.Master` 속성 사이트 형식에 속성 및 메서드를 특정 사이트에을 참조할 수 있습니다. 그림 7은 공용 속성으로 `GridMessageText` IntelliSense 드롭다운 목록에 표시 됩니다.


[![IntelliSense는이 마스터 페이지의 공용 속성 및 메서드를 보여 줍니다.](interacting-with-the-master-page-from-the-content-page-vb/_static/image20.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image19.png)

**그림 07**: IntelliSense는 마스터 페이지의 공용 속성 및 메서드를 보여 줍니다 ([큰 이미지를 보려면 클릭](interacting-with-the-master-page-from-the-content-page-vb/_static/image21.png))


> [!NOTE]
> 마스터 페이지 파일 명명 `MasterPage.master` 마스터 페이지의 코드 숨김 클래스 이름은 `MasterPage`합니다. 모호한 코드 형식에서 캐스팅 하는 경우 발생할 수 있습니다 `System.Web.UI.MasterPage` 하 여 `MasterPage` 클래스입니다. 즉, 웹 사이트 프로젝트 모델을 사용 하는 경우 약간 까다로울 수 있는 형식으로 캐스팅 하는 완전 하 게 정규화 해야 합니다. 내 제안 중 하나는 마스터 페이지를 만들 때 이름을 이외의 있는지를 확인 하는 것 `MasterPage.master` 또는 심지어 마스터 페이지에 대 한 강력한 참조를 만듭니다.


### <a name="creating-a-strongly-typed-reference-with-themastertypedirective"></a>사용 하 여 강력한 형식의 참조를 만드는`@MasterType`지시문

자세히 살펴보면 ASP.NET 페이지의 코드 숨김 클래스는 partial 클래스는 볼 수 있습니다 (참고는 `Partial` 클래스 정의에서 키워드). Partial 클래스는 C# 및 Visual Basic with.NET Framework 2.0에 도입 된 및 근본적으로 여러 파일에서 정의 해야 하는 클래스의 멤버에 대 한 허용 합니다. 코드 숨김 클래스 파일 `AddProduct.aspx.vb`, 예를 들어, 페이지 개발자가 작성 하는 코드를 포함 합니다. 코드 외에도 ASP.NET 엔진 속성을 사용 하 여 별도 클래스 파일을 자동으로 만듭니다 및 이벤트 처리기는 페이지의 클래스 계층 구조를 선언적 태그를 변환 합니다.

ASP.NET 페이지를 열어 볼 때마다 발생 하는 자동 코드 생성을 일부 대신 흥미롭고 유용한 가능성에 대 한 환경이 조성되 고 합니다. 마스터 페이지의 경우 마스터 페이지 콘텐츠 페이지에서 사용 되 고 ASP.NET 엔진 말하는 경우 생성 강력한 형식의 `Master` 우리 회사에 속성입니다.

사용 된 [ `@MasterType` 지시문](https://msdn.microsoft.com/library/ms228274.aspx) 콘텐츠 페이지의 마스터 페이지에 대 한 형식의 ASP.NET 엔진에 알림을 보내야 합니다. `@MasterType` 지시문 마스터 페이지의 형식 이름 또는 파일 경로 사용할 수 있습니다. 지정 하는 `AddProduct.aspx` 사용 하 여 페이지 `Site.master` 해당 마스터 페이지의 맨 위에 다음 지시문을 추가 `AddProduct.aspx`:


[!code-aspx[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample9.aspx)]

이 지시문은 명명 된 속성을 통해 마스터 페이지에 대 한 강력한 참조를 추가 하려면 ASP.NET 엔진 `Master`합니다. 사용 하 여는 `@MasterType` 호출 되어에서 지시문에 `Site.master` 마스터 페이지의 공용 속성 및 메서드를 통해 직접를 `Master` 모든 캐스트 하지 않고 속성.

> [!NOTE]
> 생략 하면는 `@MasterType` 지시문, 구문을 `Page.Master` 및 `Master` 동일한 작업을 반환: 페이지의 마스터 페이지에는 느슨한 형 개체입니다. 포함 하는 경우는 `@MasterType` 지시문을 다음 `Master` 지정된 마스터 페이지에 대 한 강력한 참조를 반환 합니다. `Page.Master`을 단, 여전히 느슨한 형 대 한 참조를 반환 합니다. 이 경우 이유를 보다 정확 하 게 확인 하는 방법과 `Master` 속성을 생성 때 합니다 `@MasterType` 지시문이 포함 된 내용은 [K. Scott Allen](http://odetocode.com/blogs/scott/default.aspx)의 블로그 항목 [ `@MasterType` ASP.NET 2.0](http://odetocode.com/Blogs/scott/archive/2005/07/16/1944.aspx).


### <a name="updating-the-master-page-after-adding-a-new-product"></a>새 제품을 추가한 후 마스터 페이지를 업데이트 하는 중

마스터 페이지의 public 속성 및 콘텐츠 페이지 로부터 메서드를 호출 하는 방법을 알았으므로 준비가 업데이트는 `AddProduct.aspx` 페이지 새 제품을 추가한 후 마스터 페이지를 새로 고치도록 합니다. DetailsView 컨트롤에 대 한 이벤트 처리기의 4 단계 시작 부분에서 만든 `ItemInserting` 데이터베이스에 새 제품 추가 된 후에 즉시 실행 하는 이벤트입니다. 해당 이벤트 처리기에 다음 코드를 추가 합니다.


[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample10.vb)]

위의 코드에서는 두는 느슨한 형 `Page.Master` 속성과 강력한 형식의 `Master` 속성입니다. 합니다 `GridMessageText` 속성이 "*ProductName* 표에... 추가" 방금 추가 된 제품의 값을 통해 액세스할 수는 `e.Values` 컬렉션을 방금 추가 된, 볼 수 있듯이; `ProductName` 값을 통해 액세스할 `e.Values("ProductName")`합니다.

그림 8을 `AddProduct.aspx` 데이터베이스에 새 제품-Scott 탄산 음료-직후 페이지가 추가 되었습니다. 마스터 페이지의 레이블 나오는 방금 추가 된 제품 이름 있는지 및 제품 및 해당 가격에 포함 된 GridView를 새로 고칠는 참고 합니다.


[![마스터 페이지의 레이블 및 GridView 표시 방금 추가 제품](interacting-with-the-master-page-from-the-content-page-vb/_static/image23.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image22.png)

**그림 08**:의 마스터 페이지의 레이블 및 GridView 표시 Just-Added 제품 ([큰 이미지를 보려면 클릭](interacting-with-the-master-page-from-the-content-page-vb/_static/image24.png))


## <a name="summary"></a>요약

이상적으로 마스터 페이지 및 콘텐츠 페이지 서로 완전히 별개 이며 필요 없는 수준의 상호 작용 합니다. 마스터 페이지 및 콘텐츠 페이지는 해당 목표를 염두에서에 두고 디자인 가능 해야 하는 동안 해당 마스터 페이지와 상호 작용 해야 합니다는 콘텐츠 페이지는 일반적인 시나리오는 여러 가지가 있습니다. 가장 일반적인 이유 중 하나에 중점을 둡니다 콘텐츠 페이지에서 발생 하는 일부 작업에 따라 마스터 페이지 표시의 특정 부분을 업데이트 합니다.

좋은 소식은 있다는 것에 해당 마스터 페이지를 사용 하 여 프로그래밍 방식으로 상호 작용 하는 콘텐츠 페이지를 비교적 간단 합니다. 콘텐츠 페이지에서 호출 해야 하는 기능을 캡슐화 하는 마스터 페이지에서 공용 속성 또는 메서드를 만들어 시작 합니다. 그런 다음 콘텐츠 페이지에서 마스터 페이지의 속성 및 메서드에 액세스를 통해 느슨하게 형식화 `Page.Master` 속성이 나 사용 하 여는 `@MasterType` 마스터 페이지에 대 한 강력한 참조를 만들기 위한 지시문을 합니다.

다음 자습서에서 마스터 페이지 콘텐츠 페이지 중 하나를 사용 하 여 프로그래밍 방식으로 상호 작용 하는 방법을 살펴봅니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Asp.net에서 데이터 액세스 및 업데이트](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [ASP.NET 마스터 페이지: 팁, 요령 및 트랩](http://www.odetocode.com/articles/450.aspx)
- [`@MasterType` ASP.NET 2.0의](http://odetocode.com/Blogs/scott/archive/2005/07/16/1944.aspx)
- [콘텐츠 및 마스터 페이지 간에 정보 전달](http://aspnet.4guysfromrolla.com/articles/013107-1.aspx)
- [ASP.NET 자습서에서 데이터를 사용 하 여 작업](../../data-access/index.md)

### <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 작성자의 여러 ASP/ASP.NET 서적과 4GuysFromRolla.com의 설립자 이며, 왔습니다 Microsoft 웹 기술을 1998 합니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 3.5 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)합니다. Scott에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com) 통하거나 저자의 블로그 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Zack Jones 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](control-id-naming-in-content-pages-vb.md)
> [다음](interacting-with-the-content-page-from-the-master-page-vb.md)
