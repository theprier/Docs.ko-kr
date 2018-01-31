---
uid: web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-master-page-from-the-content-page-cs
title: "콘텐츠 페이지 (C#)의 마스터 페이지와 상호 작용 | Microsoft Docs"
author: rick-anderson
description: "메서드 호출, 콘텐츠 페이지의 코드에서 속성, 마스터 페이지 등을 설정 하는 방법을 검사 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/11/2008
ms.topic: article
ms.assetid: 32d54638-71b2-491d-81f4-f7417a13a62f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-master-page-from-the-content-page-cs
msc.type: authoredcontent
ms.openlocfilehash: 977cdea38d240bcae284968de7d780ec59ab6dfd
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="interacting-with-the-master-page-from-the-content-page-c"></a>콘텐츠 페이지 (C#)의 마스터 페이지와 상호 작용
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_06_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_06_CS.pdf)

> 메서드 호출, 콘텐츠 페이지의 코드에서 속성, 마스터 페이지 등을 설정 하는 방법을 검사 합니다.


## <a name="introduction"></a>소개

마스터 페이지를 만드는 방법을에서 살펴본 지난 5 개의 자습서 진행 되는 동안 콘텐츠 영역을 정의 하 고, 마스터 페이지를 ASP.NET 페이지를 바인딩하고 페이지 관련 콘텐츠를 정의 합니다. 방문자가 특정 콘텐츠 페이지를 요청, 콘텐츠 및 마스터 페이지의 태그를 런타임에 통합된 컨트롤 계층 구조는 렌더링에 결합 합니다. 따라서 이미 관찰 한 가지 방법을 마스터 페이지와 해당 콘텐츠 페이지 중 하나를 상호 작용할 수 있는: 마스터 페이지의 ContentPlaceHolder 컨트롤로 transfuse 하는 태그를 줄이지 않고 콘텐츠 페이지.

어떤 아직 검사 하는 경우 마스터 페이지 및 콘텐츠 페이지 프로그래밍 방식으로 작용 하는 방법입니다. 마스터 페이지의 ContentPlaceHolder 컨트롤에 대 한 태그를 정의 하는 것 외에도 콘텐츠 페이지 수는 마스터 페이지의 공용 속성에 값 할당 있고 해당 공용 메서드를 호출 합니다. 마찬가지로, 마스터 페이지의 콘텐츠 페이지와 상호 작용할 수 있습니다. 마스터 및 콘텐츠 페이지 간의 프로그래밍 방식으로 상호 작용의 선언적 마크업 간의 상호 작용 보다는 덜 일반적인 상태인 동안에 그러한 프로그래밍 방식으로 상호 작용 필요한 상황 많은 시나리오가 있습니다.

이 자습서에서는 어떻게 콘텐츠 페이지 프로그래밍 방식으로 상호 작용할 수 있으며 마스터 페이지; 검사 다음 자습서 마스터 페이지의 콘텐츠 페이지와 마찬가지로 작용 하는 방법에 대해 살펴보겠습니다.

## <a name="examples-of-programmatic-interaction-between-a-content-page-and-its-master-page"></a>콘텐츠 페이지와 해당 마스터 페이지 간의 프로그래밍 방식으로 상호 작용의 예

페이지의 특정 지역에서 페이지 단위로 구성 해야, ContentPlaceHolder 컨트롤을 사용 했습니다. 하지만 대부분의 페이지는 특정 출력을 만들지만 적은 수의 페이지를 생성 해야 하는 경우 다른 값인지을 표시 하도록 사용자 지정할 필요는 어떻습니까? 하나 이러한 예제에서 검사 했습니다는 [ *기본 콘텐츠 및 여러 contentplaceholders의* ](multiple-contentplaceholders-and-default-content-cs.md) 자습서에서는 각 페이지에서 로그인 인터페이스를 표시 합니다. 대부분의 페이지는 로그인 인터페이스를 포함 해야 하는 동안 표시 되지 않아야는 소수의 페이지에 대 한 같은: 기본 로그인 페이지 (`Login.aspx`); 계정 만들기 페이지; 및 인증 된 사용자에 게 액세스할 수 있는 다른 페이지입니다. [ *여러 contentplaceholders 및 기본 콘텐츠* ](multiple-contentplaceholders-and-default-content-cs.md) 자습서 마스터 페이지에서 ContentPlaceHolder에 대 한 기본 콘텐츠를 정의 하는 방법을 보여 주었습니다 카디널리티와 다음 해당 재정의 하는 방법을 위치는 기본 콘텐츠 사용 하지 않으려는 되었습니다.

또 다른 옵션 공용 속성 또는 메서드를 로그인 인터페이스를 표시할지 여부를 나타내는 마스터 페이지 내에서 만드는 것입니다. 마스터 페이지 라는 공용 속성이 같습니다. 예를 들어 `ShowLoginUI` 값은 설정 하는 데 사용 된는 `Visible` 마스터 페이지에 로그인 컨트롤의 속성입니다. 로그인 사용자 인터페이스를 표시 되지 않아야 하는 이러한 콘텐츠 페이지 그런 다음 프로그래밍 방식으로 설정할 수는 `ShowLoginUI` 속성을 `false`합니다.

아마도 콘텐츠 및 마스터 페이지 상호 작용의 가장 일반적인 예에 대 한 특별 한 조치 콘텐츠 페이지에서 적용 한 후 새로 고쳐지도록 마스터 페이지 요구 데이터가 표시 될 때 발생 합니다. 5 개의 가장 최근에 표시 되는 GridView를 포함 하는 마스터 페이지 특정 데이터베이스 테이블에서 레코드를 추가 하는 것이 좋습니다. 하 고 해당 콘텐츠 페이지 중 하나는 동일한 테이블에 새 레코드를 추가 하기 위한 인터페이스를 포함 합니다.

사용자가 새 레코드를 추가 하려면 페이지를 방문-다섯 가지 가장 최근에 추가 된 마스터 페이지에 표시 된 레코드를 발견 합니다. 새 레코드의 열에 대 한 값을 채운 후 그녀가 양식을 전송 합니다. 마스터 페이지에 GridView에 있다고 가정할 경우 해당 `EnableViewState` true (기본값)로 설정 된 뷰 상태에서 해당 콘텐츠를 다시 로드 속성과, 결과적으로, 5 개 레코드 표시 됩니다. 그러나 데이터베이스에 새 레코드가 추가 된 합니다. 이 사용자를 혼동 될 수 있습니다.

> [!NOTE]
> 포스트백이 발생할 때마다 해당 기본 데이터 원본에 다시 바인딩합니다 있도록 GridView의 뷰 상태를 해제 하는 경우에이 여전히 표시 되지 않습니다 방금 추가 된 레코드 데이터는 datab에 새 레코드가 추가 될 때 보다 페이지 수명 주기의 앞부분에 나오는 GridView에 바인딩되므로 ase 합니다.


방금 추가 된 레코드를 마스터 페이지에 표시 되도록이 해결 하려면 데이터 원본에 다시 바인딩하려면 GridView를 지시 해야 하는 다시 게시 될 GridView의 *후* 데이터베이스에 새 레코드가 추가 되었습니다. 이렇게 하려면 마스터 페이지에 새 레코드와 해당 이벤트 처리기는 새로 고쳐져 야 하는 GridView 콘텐츠 페이지에 추가 하기 위한 인터페이스는 때문에 콘텐츠 및 마스터 페이지 간의 상호 작용 합니다.

콘텐츠 페이지에서 이벤트 처리기에서 마스터 페이지의 표시를 새로 고치는 콘텐츠 및 마스터 페이지 상호 작용에 대 한 가장 일반적인 요구 사항 중 하나 이므로이 항목을에서 자세히 살펴보겠습니다. 라는 Microsoft SQL Server 2005 Express Edition 데이터베이스를 포함 하는이 자습서에 대 한 다운로드 `NORTHWIND.MDF` 웹 사이트의에서 `App_Data` 폴더입니다. Northwind 데이터베이스는 제품, 직원 및 회사인 Northwind Traders에 대 한 판매 정보를 저장합니다.

1 단계 탐색-다섯 가지 가장 최근에 표시를 통해 마스터 페이지에 GridView에 제품을 추가 합니다. 2 단계는 새 제품을 추가 하기 위한 콘텐츠 페이지를 만듭니다. 3 단계를 마스터 페이지의 공용 속성 및 메서드를 만드는 방법을 찾은 단계 4 프로그래밍 방식으로 이러한 속성 및 메서드 콘텐츠 페이지에서와 상호 연결 하는 방법을 설명 합니다.

> [!NOTE]
> 이 자습서에서는 ASP.NET에서 데이터 작업에 대해 구체적으로 원칙적인 하지 않습니다. 데이터 및 데이터를 삽입 하기 위한 콘텐츠 페이지를 표시 하는 마스터 페이지를 설정 하기 위한 단계는 완료, 아직 breezy입니다. SqlDataSource 및 GridView 컨트롤 표시 하 고 데이터를 삽입 하 고 사용 하 여에 대 한 자세한 설명에 대 한이 자습서의 끝에 추가 정보 섹션의 리소스를 참조 하십시오.


## <a name="step-1-displaying-the-five-most-recently-added-products-in-the-master-page"></a>1 단계: 마스터 페이지에서 제품 추가 5 개의 가장 최근에 표시

열기는 `Site.master` 레이블과 GridView 컨트롤을 추가 하 고 마스터 페이지는 `leftContent` `<div>`합니다. 레이블 지우기 `Text` 속성을 해당 `EnableViewState` 속성을 false로, 및 해당 `ID` 속성을 `GridMessage`; GridView의 설정 `ID` 속성을 `RecentProducts`합니다. 다음으로, 디자이너에서 GridView의 스마트 태그를 확장 하 고 새 데이터 원본에 연결 하려면 선택 합니다. 데이터 소스 구성 마법사가 시작 됩니다. Northwind 데이터베이스에 있으므로 `App_Data` 폴더는 Microsoft SQL Server 데이터베이스는 SqlDataSource (그림 1 참조)를 선택 하 여 만들려고 선택한; SqlDataSource 이름을 `RecentProductsDataSource`합니다.


[![GridView RecentProductsDataSource 라는 SqlDataSource 컨트롤에 바인딩](interacting-with-the-master-page-from-the-content-page-cs/_static/image2.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image1.png)

**그림 01**: GridView SqlDataSource 컨트롤 이라는 바인딩할 `RecentProductsDataSource` ([전체 크기 이미지를 보려면 클릭](interacting-with-the-master-page-from-the-content-page-cs/_static/image3.png))


다음 단계 어떤 연결할 데이터베이스를 지정 합니다. 선택 된 `NORTHWIND.MDF` 데이터베이스 파일 드롭 다운 목록에서 다음을 클릭 합니다. 마법사에서 연결 문자열을 저장할 제공 처음으로이 데이터베이스를 사용한 것 이기 때문에 `Web.config`합니다. 이름을 사용 하 여 연결 문자열을 저장 하 게 `NorthwindConnectionString`합니다.


[![Northwind 데이터베이스에 연결](interacting-with-the-master-page-from-the-content-page-cs/_static/image5.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image4.png)

**그림 02**: Northwind 데이터베이스에 연결 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-master-page-from-the-content-page-cs/_static/image6.png))


데이터 소스 구성 마법사에 있는 데이터를 검색 하는 데 사용 쿼리를 지정할 수 있습니다 하는 두 가지 방법을 제공 합니다.

- 사용자 지정 SQL 문 또는 저장된 프로시저를 지정 하 여 또는
- 테이블 또는 뷰를 선택 하 고 다음 반환할 열을 지정 하 여

방금 5 가장 최근에 추가 된 제품을 반환 하려는 것 이므로 사용자 지정 SQL 문을 지정 해야 합니다. 다음 SELECT 쿼리를 사용 합니다.


[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample1.sql)]

`TOP 5` 키워드 있는 쿼리에서 처음 다섯 개의 레코드만 반환 합니다. `Products` 테이블의 기본 키 `ProductID`,이 `IDENTITY` 열을 사용 하 여 특정 us를 테이블에 추가 하는 각 새 제품 이전 항목 보다 더 큰 값을 포함 합니다. 따라서을 기준으로 결과 정렬 `ProductID` 내림차순부터 가장 최근에 만든 제품을 반환 합니다.


[![가장 최근에 추가 된 다섯 개의 제품을 반환 합니다.](interacting-with-the-master-page-from-the-content-page-cs/_static/image8.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image7.png)

**그림 03**: 다섯 개의 가장 최근에 추가 제품을 반환 합니다. ([전체 크기 이미지를 보려면 클릭](interacting-with-the-master-page-from-the-content-page-cs/_static/image9.png))


마법사를 완료 한 후 Visual Studio에서 표시 하는 GridView에 대 한 두 개의 BoundFields 생성는 `ProductName` 및 `UnitPrice` 데이터베이스에서 필드를 반환 합니다. 이 시점에서 선언적 태그 마스터 페이지에 다음과 유사한 태그를 포함 해야 합니다.


[!code-aspx[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample2.aspx)]

태그를 포함 하는 볼 수 있듯이: 웹 컨트롤 (`GridMessage`); GridView `RecentProducts`이며 두 개의 BoundFields; 가장 최근에 추가 된-다섯 가지 제품을 반환 하는 SqlDataSource 컨트롤입니다.

만든이 GridView 및 구성의 SqlDataSource 컨트롤 사용 하 여 브라우저를 통해 웹 사이트를 방문 합니다. 그림 4와 5 개의 가장 최근에 나열 하는 왼쪽된 아래 모퉁이에 표 추가 제품 표시 됩니다.


[![가장 최근에 추가 된 다섯 개의 제품을 표시 하는 GridView](interacting-with-the-master-page-from-the-content-page-cs/_static/image11.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image10.png)

**그림 04**: 다섯 개의 가장 최근에 추가 제품을 표시 하는 GridView ([전체 크기 이미지를 보려면 클릭](interacting-with-the-master-page-from-the-content-page-cs/_static/image12.png))


> [!NOTE]
> GridView의 모양을 정리 자유롭게 합니다. 몇 가지 제안 사항 표시 서식을 포함할 `UnitPrice` 통화 및 배경색 및 글꼴을 사용 하 여 눈금의 모양 향상을 위해 값입니다.


## <a name="step-2-creating-a-content-page-to-add-new-products"></a>2 단계: 새 제품을 추가할 콘텐츠 페이지 만들기

다음이 작업은 사용자를 새 제품을 추가할 수 있는 콘텐츠 페이지를 만드는 것은 `Products` 테이블입니다. 새 콘텐츠 페이지를 추가 `Admin` 라는 폴더 `AddProduct.aspx`에 바인딩할 되므로 `Site.master` 마스터 페이지입니다. 그림 5에서는이 페이지는 웹 사이트에 추가 된 후 솔루션 탐색기를 보여 줍니다.


[![Admin 폴더를 새 ASP.NET 페이지를 추가 합니다.](interacting-with-the-master-page-from-the-content-page-cs/_static/image14.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image13.png)

**그림 05**: 새 ASP.NET 페이지를 추가 `Admin` 폴더 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-master-page-from-the-content-page-cs/_static/image15.png))


이전에 설명한 대로 [ *마스터 페이지의 제목, 메타 태그 및 기타 HTML 헤더를 지정 하* ](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) 라는 기본 페이지를 사용자 지정 클래스 만든 자습서 `BasePage` 생성 되는 페이지의 제목 인 경우 명시적으로 설정 합니다. 이동 하는 `AddProduct.aspx` 페이지의 코드 숨김 클래스에서 파생 되는 및 `BasePage` (대신에서 `System.Web.UI.Page`).

마지막으로 업데이트는 `Web.sitemap` 파일을이 단원에 대 한 항목을 포함 합니다. 아래에 다음 태그를 추가 `<siteMapNode>` 제어 ID 명명 문제 단원:


[!code-xml[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample3.xml)]

이 추가 그림 6에 나와 있는 것 처럼 `<siteMapNode>` 요소과 목록에 반영 됩니다.

으로 돌아와서 `AddProduct.aspx`합니다. 에 대 한 콘텐츠 컨트롤에는 `MainContent` ContentPlaceHolder, DetailsView 컨트롤을 추가 하 고 이름을 `NewProduct`합니다. DetailsView를 명명 된 새 SqlDataSource 컨트롤을 바인딩할 `NewProductDataSource`합니다. 1 단계에서에서 SqlDataSource를 사용 하 여 마법사를 Northwind 데이터베이스를 사용 하도록 구성할 사용자 지정 SQL 문 지정 하도록 선택할 같이입니다. 데이터베이스에 항목을 추가할 DetailsView 사용될지를 하므로 둘 다 지정 해야는 `SELECT` 문 및 `INSERT` 문. 다음을 사용 하 여 `SELECT` 쿼리:


[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample4.sql)]

그런 다음 삽입 탭에서 다음을 추가 `INSERT` 문:


[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample5.sql)]

마법사를 완료 한 후 DetailsView의 스마트 태그 이동한 다음 "삽입 사용" 확인란을 선택 합니다. 인 DetailsView에는 CommandField 추가 해당 `ShowInsertButton` 속성이 true로 설정 합니다. 이 DetailsView는 데이터 삽입에 대해서만 사용 되므로, 설정 DetailsView의 `DefaultMode` 속성을 `Insert`합니다.

그을 마쳤습니다. 이 페이지를 테스트해 보겠습니다. 방문 `AddProduct.aspx` 브라우저를 통해 이름과 가격 (그림 6 참조)를 입력 합니다.


[![데이터베이스에 새 제품을 추가 합니다.](interacting-with-the-master-page-from-the-content-page-cs/_static/image17.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image16.png)

**그림 06**: 데이터베이스에 새 제품을 추가 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-master-page-from-the-content-page-cs/_static/image18.png))


이름 및 새 제품에 대 한 가격을 입력 한 후 삽입 단추를 클릭 합니다. 이렇게 하면 폼에 다시 게시 합니다. 다시 게시 될 SqlDataSource 컨트롤의 `INSERT` 문이 실행 됩니다; 두 매개 변수는 DetailsView의 두 텍스트 상자 컨트롤에 사용자가 입력 한 값으로 채워집니다. 그러나 삽입이 발생 했음을 시각적 알려가 않습니다. 새 레코드가 추가 된 것을 확인 하는 표시 되는 메시지가 있는 좋을 것입니다. I이 그대로 실행으로 판독기에 대 한 합니다. 또한 DetailsView에서 새 레코드를 추가한 후 마스터 페이지에 GridView 계속 표시 하기 전에;와 동일한 5 개의 레코드가 방금 추가 된 레코드는 포함 되지 않습니다. 이후 단계에서이 해결 하는 방법을 검토 합니다.

> [!NOTE]
> 특정 형태의 삽입에 성공 하는 시각적 피드백을 추가할 뿐 아니라 바랍니다도 유효성 검사를 포함 DetailsView의 삽입 인터페이스를 업데이트 해야 합니다. 현재 유효성 검사 없이입니다. 사용자가 잘못 된 값에 대 한 입력은 `UnitPrice` 필드와 같은 "너무 비용이 많이 들며," 시스템에서 해당 문자열을 10 진수로 변환 하려고 할 때 다시 게시 될 때 예외가 throw 됩니다. 삽입 하는 사용자 지정에 대 한 인터페이스를 참조는 [ *데이터 수정 인터페이스 사용자 지정* 자습서](../../data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) 에서 내 [데이터 자습서 시리즈작업](../../data-access/index.md).


## <a name="step-3-creating-public-properties-and-methods-in-the-master-page"></a>3 단계: 마스터 페이지의 공용 속성 및 메서드 만들기

1 단계에서에서 라는 Label 웹 컨트롤을 추가 했습니다 `GridMessage` 마스터 페이지에 GridView 위에 있습니다. 이 레이블은 필요에 따라 메시지를 표시 하는 데 사용 됩니다. 예를 들어에 새 레코드를 추가한 후의 `Products` 테이블 하고자 할 수 있습니다를 읽는 메시지 표시: "*ProductName* 데이터베이스에 추가 되었습니다." 하드 코딩 마스터 페이지에서이 레이블에 대 한 텍스트, 대신 메시지 콘텐츠 페이지에서 사용자 지정할 수 좋습니다.

Label 컨트롤은 마스터 페이지 내에서 보호 된 멤버 변수로 구현 되기 때문에 콘텐츠 페이지에서 직접 액세스할 수 없습니다. 마스터 페이지 콘텐츠 페이지에서 (또는 마스터 페이지의 웹 컨트롤이 해당 문제에 대 한) 내에서 레이블을 사용 하려면 공용 속성의 속성 중 하나는 기준인 수 프록시로 사용 되어 또는 웹 컨트롤을 노출 하는 마스터 페이지에서 만들려는 해야  액세스할 수 있습니다. 레이블의 노출 하는 마스터 페이지의 코드 숨김 클래스에 다음 구문을 추가 `Text` 속성:


[!code-csharp[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample6.cs)]

새 레코드에 추가 된 경우는 `Products` 콘텐츠 페이지에서 테이블의 `RecentProducts` GridView 마스터 페이지의 원본으로 사용 하는 데이터 원본 다시 바인딩 해야 합니다. GridView 호출 다시 바인딩하려면 해당 `DataBind` 메서드. 마스터 페이지에 GridView 콘텐츠 페이지에 프로그래밍 방식으로 액세스할 수 없기 때문에 만들어야 하는 공용 메서드 마스터 페이지에는 호출 될 때, GridView에 데이터를 다시 바인딩 횟수 했습니다. 마스터 페이지의 코드 숨김 클래스에 다음 메서드를 추가 합니다.


[!code-csharp[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample7.cs)]

와 `GridMessageText` 속성 및 `RefreshRecentProductsGrid` 메서드 위치에서 모든 콘텐츠 페이지 수 프로그래밍 방식으로 설정 또는 값을 읽을 `GridMessage` 레이블의 `Text` 속성 하거나 데이터를 다시는 `RecentProducts` GridView입니다. 4 단계에는 콘텐츠 페이지에서 마스터 페이지의 공용 속성 및 메서드에 액세스 하는 방법을 검사 합니다.

> [!NOTE]
> 마스터 페이지의 속성 및 메서드를 표시 하는 반드시 `public`합니다. 경우 하면 명시적으로 나타내지 않는으로 이러한 메서드와 속성 `public`, 콘텐츠 페이지에서 액세스할 수 있는 됩니다.


## <a name="step-4-calling-the-master-pages-public-members-from-a-content-page"></a>콘텐츠 페이지에서 마스터 페이지의 공용 멤버를 호출 하는 4 단계:

마스터 페이지에 필요한 공용 속성 및 메서드, 우리 했으므로 이러한 속성 및 메서드를 호출 하는 `AddProduct.aspx` 콘텐츠 페이지. 특히, 마스터 페이지를 설정 해야 `GridMessageText` 속성과 호출의 `RefreshRecentProductsGrid` 신제품 데이터베이스에 추가 된 후 메서드. 모든 ASP.NET 데이터 웹 컨트롤 바로 앞 이나 쉽게 페이지 작업 전후의 프로그래밍 방식으로 작업을 수행 하는 개발자를 위한 다양 한 작업을 완료 한 후 이벤트를 발생 합니다. 예를 들어 최종 사용자가 DetailsView의 삽입 단추를 클릭 하면에 포스트백 DetailsView 발생 시키는 해당 `ItemInserting` 삽입 워크플로 시작 하기 전에 이벤트입니다. 그런 다음 데이터베이스에 레코드를 삽입 합니다. DetailsView 발생 그런 다음, 해당 `ItemInserted` 이벤트입니다. 따라서 새 제품 추가 된 후 마스터 페이지를 사용 하려면 DetailsView의에 대 한 이벤트 처리기 만들기 `ItemInserted` 이벤트입니다.

콘텐츠 페이지의 마스터 페이지와 상호 작용할 수 있는 프로그래밍 방식으로 두 가지가 있습니다.

- 사용 하 여 `Page.Master` 마스터 페이지에 대 한 자유로운 형식의 참조는을 반환 하는 속성 또는
- 페이지의 마스터 페이지 또는 파일 경로 통해 지정 된 `@MasterType` 지시문;는 강력한 형식의 속성이 라는 페이지에 자동으로 추가 `Master`합니다.

두 방법을 모두를 살펴보겠습니다.

### <a name="using-the-loosely-typedpagemasterproperty"></a>자유로운 형식의 사용 하 여`Page.Master`속성

모든 ASP.NET 웹 페이지에서 파생 되어야 합니다는 `Page` 에 있는 클래스는 `System.Web.UI` 네임 스페이스입니다. `Page` 클래스를 포함 한 [ `Master` 속성](https://msdn.microsoft.com/library/system.web.ui.page.master.aspx) 페이지의 마스터 페이지에 대 한 참조를 반환 하 합니다. 마스터 페이지의 페이지에 없는 경우 `Master` 반환 `null`합니다.

`Master` 형식의 개체를 반환 [ `MasterPage` ](https://msdn.microsoft.com/library/system.web.ui.masterpage.aspx) (에 `System.Web.UI` 네임 스페이스)가 모든 마스터 페이지에서 파생 되는 기본 유형입니다. 따라서를 공용 속성을 사용 하거나 캐스팅 해야 했습니다 웹 사이트의 마스터 페이지에 정의 된 메서드는 `MasterPage` 에서 반환 된 개체는 `Master` 속성을 적절 한 형식입니다. 이 마스터 페이지 파일 이름을 때문에 `Site.master`, 코드 숨김 클래스 이름이 `Site`합니다. 따라서 다음 코드 캐스트는 `Page.Master` 사이트 클래스의 인스턴스에 대 한 속성.


[!code-csharp[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample8.cs)]

으로 캐스팅 았 자유로운 형식의 `Page.Master` 속성을는 `Site` 유형 속성 및 메서드를 사이트에만 참조할 수 있습니다. 그림 7 보듯이 공용 속성 `GridMessageText` IntelliSense 드롭다운에 나타납니다.


[![IntelliSense는 마스터 페이지의 공용 속성 및 메서드 표시](interacting-with-the-master-page-from-the-content-page-cs/_static/image20.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image19.png)

**그림 07**: IntelliSense 마스터 페이지의 공용 속성 및 메서드 표시 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-master-page-from-the-content-page-cs/_static/image21.png))


> [!NOTE]
> 마스터 페이지 파일의 이름을 `MasterPage.master` 마스터 페이지의 코드 숨김 클래스 이름이 다음 `MasterPage`합니다. 모호한 코드 형식에서 캐스팅 하는 경우 발생할 수 있습니다 `System.Web.UI.MasterPage` 하 여 `MasterPage` 클래스입니다. 즉, 웹 사이트 프로젝트 모델을 사용 하는 때가 약간 까다로울 수 있습니다, 캐스팅 하는 형식을 완전 하 게 정규화 해야 할 수도 있습니다. 되도록 하거나 마스터 페이지를 만들 때 이름을 지정 하 고 것 이외의 것 `MasterPage.master` 하거나 더 좋은 마스터 페이지에는 강력한 형식의 참조를 만듭니다.


### <a name="creating-a-strongly-typed-reference-with-themastertypedirective"></a>사용 하 여 강력한 형식의 참조 만들기는`@MasterType`지시문

자세히 보면 ASP.NET 페이지의 코드 숨김 클래스의 partial 클래스 인지 확인할 수 있습니다 (참고는 `partial` 클래스 정의에서 키워드)입니다. Partial 클래스는 C# 및 Visual Basic.net으로 빌드된 Framework 2.0에 도입 된 및 간단히 말하면 여러 파일에서 정의 되어야 하는 클래스의 멤버에 대 한 허용 합니다. 코드 숨김 클래스 파일- `AddProduct.aspx.cs`, 예를 들어, 페이지 개발자 작성 하는 코드를 포함 합니다. 코드 외에도 ASP.NET 엔진 속성을 가진 별도 클래스 파일을 자동으로 만듭니다 및 이벤트 처리기에 있는 페이지의 클래스 계층 구조도 선언적 태그를 변환 합니다.

ASP.NET 페이지를 열어 볼 때마다 발생 하는 자동 코드 생성을 사용 하면 일부 대신 흥미롭고 유용한 가능성에 대 한 어 합니다. 마스터 페이지의 경우 어떤 마스터 페이지 콘텐츠 페이지에서 사용 되 고 ASP.NET 엔진 위치도 제공 하는 경우 생성 강력한 형식의 `Master` 속성을 수행해 줍니다.

사용 하 여는 [ `@MasterType` 지시문](https://msdn.microsoft.com/library/ms228274.aspx) 콘텐츠 페이지의 마스터 페이지 형식의 ASP.NET 엔진에 알릴 수 있습니다. `@MasterType` 지시문 마스터 페이지의 유형 이름 또는 해당 파일 경로 사용할 수 있습니다. 지정 하는 `AddProduct.aspx` 사용 하 여 페이지 `Site.master` 의 마스터 페이지의 맨 위에 다음 지시문을 추가 `AddProduct.aspx`:


[!code-aspx[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample9.aspx)]

이 지시문은 라는 속성을 통해 마스터 페이지에는 강력한 형식의 참조를 추가 하려면 ASP.NET 엔진 `Master`합니다. 와 `@MasterType` 원위치에서 지시문를 호출할 수 있습니다는 `Site.master` 마스터 페이지의 공용 속성 및 메서드를 통해 직접는 `Master` 캐스트나 없는 속성입니다.

> [!NOTE]
> 생략 하면는 `@MasterType` 지시문, 구문을 `Page.Master` 및 `Master` 동일한 작업을 반환: 자유로운 형식의 개체 페이지의 마스터 페이지입니다. 포함 하는 경우는 `@MasterType` 지시문 다음 `Master` 강력한 형식의 지정된 된 마스터 페이지 참조를 반환 합니다. `Page.Master`그러나 여전히 자유로운 형식의 참조를 반환 합니다. 이 경우 이유를 보다 철저 한 확인에 대 한 방법과 `Master` 속성을 생성 때는 `@MasterType` 지시문이 포함 되, 참조 [K. Scott Allen](http://odetocode.com/blogs/scott/default.aspx)의 블로그 항목 [ `@MasterType` ASP.NET 2.0](http://odetocode.com/Blogs/scott/archive/2005/07/16/1944.aspx).


### <a name="updating-the-master-page-after-adding-a-new-product"></a>새 제품을 추가한 후 마스터 페이지를 업데이트 합니다.

마스터 페이지의 공용 속성 및 콘텐츠 페이지의 메서드를 호출 하는 방법을 알았으므로 준비가 업데이트는 `AddProduct.aspx` 페이지를 새 제품을 추가한 후 마스터 페이지가 새로 고쳐집니다. DetailsView 컨트롤에 대 한 이벤트 처리기의 4 단계 시작 부분에서 만든 `ItemInserting` 신제품 데이터베이스에 추가 된 후에 즉시 실행 하는 이벤트입니다. 해당 이벤트 처리기에 다음 코드를 추가 합니다.


[!code-csharp[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample10.cs)]

위의 코드는 모두는 느슨한 형 사용 `Page.Master` 속성과 강력한 형식의 `Master` 속성입니다. `GridMessageText` 속성이로 설정 된 "*ProductName* 눈금...에 추가" 방금 추가 된 제품의 값이를 통해 액세스할 수는 `e.Values` 컬렉션은 방금 추가 된, 볼 수 있듯이; `ProductName` 값을 통해 액세스 되 `e.Values["ProductName"]`합니다.

그림 8의 `AddProduct.aspx` 페이지가 새 제품-Scott의 탄산 음료-후 즉시 데이터베이스에 추가 되었습니다. 불과하며 방금 추가 된 제품 이름을 마스터 페이지의 레이블에 표시 됩니다는 GridView가 새로 고쳐지지는 제품 및 해당 가격을 포함 하도록 합니다.


[![마스터 페이지의 레이블 및 GridView 방금 추가 된 제품을 보여 줍니다.](interacting-with-the-master-page-from-the-content-page-cs/_static/image23.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image22.png)

**그림 08**: The 마스터 페이지의 레이블 및 GridView Just-Added 제품을 보여 줍니다 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-master-page-from-the-content-page-cs/_static/image24.png))


## <a name="summary"></a>요약

이상적으로 마스터 페이지 및 콘텐츠 페이지는 서로 완전히 분리 하 고 필요 없는 수준의 상호 작용 합니다. 마스터 페이지 및 페이지 콘텐츠를 해당 목표를 염두에서에 두고 설계 해야, 일반적인 시나리오는 콘텐츠 페이지 해야 해당 마스터 페이지와 상호 작용할 수가 있습니다. 가장 일반적인 이유 중 하나에 중점을 둡니다 콘텐츠 페이지에서 발생 한 상황 일부 동작에 따라 마스터 페이지 표시의 특정 부분을 업데이트 합니다.

다행히도 프로그래밍 방식으로 해당 마스터 페이지와 상호 작용 하는 콘텐츠 페이지를 상대적으로 간단 하 게 된다는 점입니다. 콘텐츠 페이지에서 호출 해야 하는 기능을 캡슐화 하는 마스터 페이지에서 공용 속성 또는 메서드를 만들어 시작 합니다. 그런 다음 콘텐츠 페이지에서 마스터 페이지의 속성 및 메서드에 액세스 자유로운 형식의 통해 `Page.Master` 속성이 나 사용 하 여는 `@MasterType` 마스터 페이지에는 강력한 형식의 참조를 만들기 위한 지시문입니다.

다음 자습서 마스터 페이지 콘텐츠 페이지 중 하 나와 프로그래밍 방식으로 상호 작용 하는 방법을 알아봅니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Asp.net에서 데이터 액세스 및 업데이트](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [ASP.NET 마스터 페이지: 팁, 요령 및 트랩](http://www.odetocode.com/articles/450.aspx)
- [`@MasterType`ASP.NET 2.0에서](http://odetocode.com/Blogs/scott/archive/2005/07/16/1944.aspx)
- [콘텐츠 및 마스터 페이지 사이의 정보 전달](http://aspnet.4guysfromrolla.com/articles/013107-1.aspx)
- [ASP.NET 자습서에서 데이터 작업](../../data-access/index.md)

### <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 작성자 여러 ASP/ASP.NET 설명서와 4GuysFromRolla.com의 창립자의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 3.5 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)합니다. Scott에 도달할 수 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com) 또는에서 그의 블로그 통해 [http://ScottOnWriting.NET](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Zack jones 이면 특정 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](control-id-naming-in-content-pages-cs.md)
[다음](interacting-with-the-content-page-from-the-master-page-cs.md)
