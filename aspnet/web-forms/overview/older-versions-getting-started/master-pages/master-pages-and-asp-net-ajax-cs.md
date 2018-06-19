---
uid: web-forms/overview/older-versions-getting-started/master-pages/master-pages-and-asp-net-ajax-cs
title: 마스터 페이지 및 ASP.NET AJAX (C#) | Microsoft Docs
author: rick-anderson
description: ASP.NET AJAX 및 마스터 페이지를 사용 하기 위한 옵션에 설명 합니다. ScriptManagerProxy 클래스를 사용 하 여 조사 다양 한 JS 파일은 dependi를 로드 하는 방법에 대해 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/11/2008
ms.topic: article
ms.assetid: 0c55eb66-ba44-4d49-98e8-5c87fd9b1111
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/master-pages-and-asp-net-ajax-cs
msc.type: authoredcontent
ms.openlocfilehash: 87e5855354610723823da88ec961e7391c3f705f
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30888782"
---
<a name="master-pages-and-aspnet-ajax-c"></a>마스터 페이지 및 ASP.NET AJAX (C#)
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_08_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_08_CS.pdf)

> ASP.NET AJAX 및 마스터 페이지를 사용 하기 위한 옵션에 설명 합니다. ScriptManagerProxy 클래스를 사용 하 여 조사 페이지 또는 콘텐츠 페이지 m에서 ScriptManager 사용 여부에 따라 다양 한 JS 파일이 로드 되는 방법을 설명 합니다.


## <a name="introduction"></a>소개

작성 된 점점 더 많은 개발자 지난 몇 년간 [AJAX](http://en.wikipedia.org/wiki/Ajax_(programming))-웹 응용 프로그램을 사용 하도록 설정 합니다. AJAX 사용 웹 사이트를 더 빠르게 대응 하는 사용자 환경을 제공 하려면 다양 한 관련된 웹 기술을 사용 합니다. Microsoft의 수 덕분에 매우 쉽게 수행할 수는 AJAX 사용 ASP.NET 응용 프로그램을 만드는 [ASP.NET AJAX 프레임 워크](../../../../ajax/index.md)합니다. ASP.NET AJAX ASP.NET 3.5 및 Visual Studio 2008; 내장 됩니다. ASP.NET 2.0 응용 프로그램에 대 한 별도 다운로드로 제공 됩니다.

정확 하 게 하나에 추가 해야 AJAX 사용 웹 페이지를 ASP.NET AJAX 프레임 워크를 작성할 때 [ScriptManager 컨트롤](https://msdn.microsoft.com/library/bb398863.aspx) 프레임 워크를 사용 하는 각 페이지에 있습니다. 이름에서 알 수 있듯이 ScriptManager AJAX 사용 웹 페이지에서 사용 되는 클라이언트 쪽 스크립트를 관리 합니다. ScriptManager는 최소한 해당 구성을 ASP.NET AJAX 클라이언트 라이브러리는 JavaScript 파일을 다운로드 하도록 브라우저에 지시 하는 HTML을 내보냅니다. 또한 사용자 지정 JavaScript 파일, 스크립트 사용 웹 서비스 및 사용자 지정 응용 프로그램 서비스 기능 등록을 사용할 수 있습니다.

사이트 사용 하 여 마스터 페이지 (는) 하는 경우 반드시 않아도; 모든 단일 콘텐츠 페이지에 ScriptManager 컨트롤을 추가 하려면 대신, 마스터 페이지에 ScriptManager 컨트롤을 추가할 수 있습니다. 이 자습서에서는 마스터 페이지에 ScriptManager 컨트롤을 추가 하는 방법을 보여 줍니다. 특정 콘텐츠 페이지에서 사용자 지정 스크립트 및 스크립트 서비스를 등록 하려면 ScriptManagerProxy 컨트롤을 사용 하는 방법에 대해서도 설명 합니다.

> [!NOTE]
> 디자인 하거나 ASP.NET AJAX framework AJAX 사용 웹 응용 프로그램 작성이 자습서 탐색 하지 않습니다. AJAX 사용 하 여 대 한 자세한 내용은 참조는 [ASP.NET AJAX 비디오](../../../videos/aspnet-ajax/index.md) 및 [자습서](../aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax.md)뿐만이 자습서의 끝에 추가 정보 섹션에 나열 된 이러한 리소스 그룹으로 합니다.


## <a name="examining-the-markup-emitted-by-the-scriptmanager-control"></a>ScriptManager 컨트롤에서 내보낸 태그를 검토

ScriptManager 컨트롤 JavaScript 파일을 다운로드 하도록 브라우저에 해당 구성을 ASP.NET AJAX 클라이언트 라이브러리를 지시 하는 태그를 내보냅니다. 또한이 라이브러리를 초기화 하는 페이지에는 약간의 인라인 JavaScript 추가 합니다. 다음 태그 ScriptManager 컨트롤을 포함 하는 페이지의 렌더링 된 출력에 추가 된 내용을 보여 줍니다.


[!code-html[Main](master-pages-and-asp-net-ajax-cs/samples/sample1.html)]

`<script src="url"></script>` 태그 다운로드 하 고에서 JavaScript 파일을 실행 하도록 브라우저에 지시 *url*합니다. ScriptManager에서 이러한 3 개의 태그; 파일 참조 하나 `WebResource.axd`, 다른 두 파일을 참조 하는 반면, `ScriptResource.axd`합니다. 이러한 파일 웹 사이트의 파일이 실제로 존재 하지 않습니다. 대신, 이러한 파일 중 하나에 대 한 요청 웹 서버에 도착 하는 경우 ASP.NET 엔진 querystring을 검사 하 고 적절 한 JavaScript 콘텐츠를 반환 합니다. 이 세 외부 JavaScript 파일에서 제공 하는 스크립트는 ASP.NET AJAX framework 클라이언트 라이브러리를 구성 합니다. 다른 `<script>` ScriptManager에서 내보낸 태그가이 라이브러리를 초기화 하는 인라인 스크립트를 포함 합니다.

외부 스크립트 참조 및 ScriptManager에서 내보낸 인라인 스크립트는 ASP.NET AJAX 프레임 워크를 사용 하 여 프레임 워크를 사용 하지 않는 페이지에 대 한 필요 하지는 않은 페이지에 필수적입니다. 따라서만 ASP.NET AJAX 프레임 워크를 사용 하는 해당 페이지에 ScriptManager를 추가 하는 데 이상적 임을 이유 수 있습니다. 및이 충분 하지만 프레임 워크를 사용 하는 여러 페이지에 있는 경우 모든 페이지-말해도 반복적인 태스크에 ScriptManager 컨트롤 추가 남게 됩니다. 또는 다음 모든 콘텐츠 페이지에이 필요한 스크립트를 삽입 하는 마스터 페이지에 ScriptManager를 추가할 수 있습니다. 이 방법에서는 이미 마스터 페이지에 포함 되어 있으므로 ASP.NET AJAX 프레임 워크를 사용 하는 새 페이지에 ScriptManager를 추가 해야 필요가 없습니다. 1 단계에서는 마스터 페이지에 ScriptManager를 추가 하는 과정입니다.

> [!NOTE]
> 마스터 페이지의 사용자 인터페이스 내에서 AJAX 기능을 포함 하려는 경우 해당 문제에는 여지가-마스터 페이지에 ScriptManager를 포함 해야 하는 것입니다.


마스터 페이지에 ScriptManager를 추가 하는 한 한 가지 단점은에서 위의 스크립트를 내보냅니다 *모든* 페이지 여부에 관계 없이 해당 필요 합니다. 이 ASP.NET AJAX 프레임 워크의 모든 기능을 사용 하지 않는 아직 ScriptManager (마스터 페이지)를 통해 포함 되어 있는 해당 페이지에 대 한 불필요 하 게 대역폭으로 명확 하 게 이어집니다. 하지만 대역폭을 소비 하는 어느 정도?

- 실제 콘텐츠 (위와 같이) ScriptManager에서 내보낸 1KB 약간 넘는 합계를 구합니다.
- 그러나 3 개의 외부 스크립트 파일에서 참조 되는 `<script>` 요소인 450KB 대략 압축 되지 않은 데이터를 구성 하; gzip 압축을 사용 하는 웹 사이트를이 총 대역폭 100KB 근처 줄일 수 있습니다. 그러나이 스크립트 파일만 한 번 다운로드 해야 하는 것을 의미 하는 1 년 동안 브라우저에서 캐시 하는 하 고 사이트에서 다른 페이지에서 다시 사용할 수 있습니다.

최상의 경우에서 스크립트 파일이 캐시 될 때 총 비용을 지불 합니다 1KB 있는 영향은 매우 적습니다. 그러나 최악의 경우-압축의 모든 형태를 사용 하지 않는 경우 스크립트 파일 아직 다운로드 되지 및 웹 서버-대역폭 적중은 약 450KB, 초 또는 1 분까지 광대역 연결을 통해 두 개의에서 아무 곳 이나 추가 될 수 있습니다.  전화 접속 모뎀을 통해 사용자입니다. 다행히도 외부 스크립트 파일은 브라우저에 의해 캐시 되므로이 최악의 경우 발생 하 고 자주 합니다.

> [!NOTE]
> 여전히 생각 될 경우 마스터 페이지에 ScriptManager 컨트롤 배치 불편을 Web Form 고려 (의 `<form runat="server">` 마스터 페이지의 태그). 포스트백 모델을 사용 하는 모든 ASP.NET 페이지 정확 하 게 하나의 Web Form을 포함 해야 합니다. Web Form을 추가 추가 콘텐츠를 추가: 숨겨진된 양식 필드의 숫자는 `<form>` 태그 자체와 JavaScript 스크립트에서 포스트백을 시작 하는 것에 대 한 기능 필요한 경우. 이 태그 다시 게시 하지 않는 페이지에 대 한 필요는 없습니다. 이 불필요 한 태그의 마스터 페이지에서 Web Form을 제거 하 고 하나 필요로 하는 각 콘텐츠 페이지에 수동으로 추가 하 여 제거할 수 없습니다. 그러나 마스터 페이지에서 Web Form의 이점에는 불필요 하 게 특정 콘텐츠 페이지에 추가 하는 것과 단점을 보다 더 큽니다.


## <a name="step-1-adding-a-scriptmanager-control-to-the-master-page"></a>1 단계: 마스터 페이지에 ScriptManager 컨트롤 추가

ASP.NET AJAX 프레임 워크를 사용 하는 모든 웹 페이지에 ScriptManager 컨트롤을 정확 하 게 하나 포함 해야 합니다. 이 요구 사항으로 인해 일반적으로 이렇게 하면 모든 콘텐츠 페이지에 ScriptManager 컨트롤에서 자동으로 포함 하도록 있도록 마스터 페이지에 있는 단일 ScriptManager 컨트롤을 배치할 수 있습니다. 또한 ScriptManager는 ASP.NET AJAX 서버 컨트롤 UpdatePanel 및 UpdateProgress 컨트롤과 같은 중 하나 앞에 나와야 합니다. 따라서이 ScriptManager 웹 폼 내에서 모든 ContentPlaceHolder 컨트롤의 앞에 배치 하 좋습니다.

열기는 `Site.master` 하기 전에 웹 폼 내에서 페이지에 ScriptManager 컨트롤을 추가 하 고 마스터 페이지는 `<div id="topContent">` 요소 (그림 1 참조). Visual Web Developer 2008 또는 Visual Studio 2008을 사용 하는 경우 ScriptManager 컨트롤의 AJAX 확장 탭의 도구 상자에 있습니다. Visual Studio 2005를 사용 하는 경우 먼저 ASP.NET AJAX 프레임 워크를 설치 하 고 도구 상자에 컨트롤을 추가 해야 합니다. 방문는 [ASP.NET AJAX Wiki](https://github.com/DevExpress/AjaxControlToolkit/wiki) ASP.NET 2.0에 대 한 프레임 워크를 가져오려는 합니다.

페이지에 ScriptManager를 추가한 후 변경의 `ID` 에서 `ScriptManager1` 를 `MyManager`합니다.


[![마스터 페이지에 ScriptManager를 추가 합니다.](master-pages-and-asp-net-ajax-cs/_static/image2.png)](master-pages-and-asp-net-ajax-cs/_static/image1.png)

**그림 01**: 마스터 페이지에 ScriptManager를 추가 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image3.png))


## <a name="step-2-using-the-aspnet-ajax-framework-from-a-content-page"></a>2 단계: 콘텐츠 페이지에서 ASP.NET AJAX 프레임 워크를 사용 하 여

마스터 페이지에 추가 ScriptManager 컨트롤에서 모든 콘텐츠 페이지를 ASP.NET AJAX framework 기능을 이제 추가할 수 있습니다. Northwind 데이터베이스에서 임의로 선택 된 제품을 표시 하는 새 ASP.NET 페이지를 만들어 보겠습니다. ASP.NET AJAX 프레임 워크의 타이머 컨트롤이이 표시는 새 제품을 보여 주는 15 초 마다 업데이트를 사용 합니다.

명명 된 루트 디렉터리에 새 페이지를 만들어서 시작 `ShowRandomProduct.aspx`합니다. 이 새 페이지를 바인딩하는 반드시는 `Site.master` 마스터 페이지입니다.


[![새 ASP.NET 페이지를 웹 사이트에 추가](master-pages-and-asp-net-ajax-cs/_static/image5.png)](master-pages-and-asp-net-ajax-cs/_static/image4.png)

**그림 02**: 웹 사이트에 새 ASP.NET 페이지 추가 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image6.png))


이전에 설명한 대로 [ *마스터 페이지의 제목, 메타 태그 및 기타 HTML 헤더를 지정 하* ](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) 라는 기본 페이지를 사용자 지정 클래스 만든 자습서 `BasePage` 생성 되는 페이지의 제목 인 경우 명시적으로 설정 합니다. 이동 하는 `ShowRandomProduct.aspx` 페이지의 코드 숨김 클래스에서 파생 되는 및 `BasePage` (대신에서 `System.Web.UI.Page`).

마지막으로 업데이트는 `Web.sitemap` 파일을이 단원에 대 한 항목을 포함 합니다. 아래에 다음 태그를 추가 `<siteMapNode>` 콘텐츠 페이지 상호 작용 단원으로 든 Master에 대 한:


[!code-xml[Main](master-pages-and-asp-net-ajax-cs/samples/sample2.xml)]

이 추가 `<siteMapNode>` 요소 단원에서 반영 됩니다 (그림 5 참조)를 나열 합니다.

### <a name="displaying-a-randomly-selected-product"></a>임의로 선택한 제품 표시

으로 돌아와서 `ShowRandomProduct.aspx`합니다. 디자이너에서 UpdatePanel 컨트롤에 도구 상자에서 끌어는 `MainContent` 콘텐츠 컨트롤을 설정 하 고 해당 `ID` 속성을 `ProductPanel`합니다. UpdatePanel 부분 페이지 포스트백을 통해 비동기적으로 업데이트 될 수 있는 화면에 영역을 나타냅니다.

첫 번째 작업이 UpdatePanel에서 임의로 선택 된 제품에 대 한 정보를 표시 하는 것입니다. DetailsView 컨트롤 UpdatePanel 드래그 하 여 시작 합니다. DetailsView 컨트롤 설정 `ID` 속성을 `ProductInfo` 지울 및 해당 `Height` 및 `Width` 속성입니다. DetailsView의 스마트 태그를 확장 하 고 데이터 소스 선택 드롭다운 목록에서 선택 DetailsView를 명명 된 새 SqlDataSource 컨트롤을 바인딩할 `RandomProductDataSource`합니다.


[![DetailsView 새 SqlDataSource 컨트롤 바인딩](master-pages-and-asp-net-ajax-cs/_static/image8.png)](master-pages-and-asp-net-ajax-cs/_static/image7.png)

**그림 03**: DetailsView에 새 SqlDataSource 컨트롤을 바인딩할 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image9.png))


SqlDataSource 컨트롤 통해 Northwind 데이터베이스에 연결을 구성할는 `NorthwindConnectionString` (에서 만든는 [ *콘텐츠 페이지의 마스터 페이지와 상호 작용* ](interacting-with-the-content-page-from-the-master-page-cs.md) 자습서). 때 select 문의 구성 중에서 선택할 사용자 지정 SQL 문을 지정 하 고 다음 쿼리를 입력 합니다.


[!code-sql[Main](master-pages-and-asp-net-ajax-cs/samples/sample3.sql)]

`TOP 1` 키워드는 `SELECT` 절 쿼리에서 반환한 첫 번째 레코드를 반환 합니다. [ `NEWID()` 함수](https://msdn.microsoft.com/library/ms190348.aspx) 새로 생성 [전역 고유 식별자 값 (GUID)](http://en.wikipedia.org/wiki/Globally_Unique_Identifier) 에 사용할 수는 `ORDER BY` 임의의 순서로 테이블의 레코드를 반환 하는 절.


[![SqlDataSource를 임의로 선택 된 단일 레코드를 반환할 수를 구성 합니다.](master-pages-and-asp-net-ajax-cs/_static/image11.png)](master-pages-and-asp-net-ajax-cs/_static/image10.png)

**그림 04**: 구성 임의로 선택 된 레코드는 단일 반환할 SqlDataSource ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image12.png))


마법사를 완료 한 후 Visual Studio는 위의 쿼리에 의해 반환 되는 두 개의 열에 대 한 BoundField를 만듭니다. 이 시점에서 페이지의 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](master-pages-and-asp-net-ajax-cs/samples/sample4.aspx)]

그림 5는 `ShowRandomProduct.aspx` 브라우저를 통해 볼 때 페이지입니다. 페이지; 다시 로드 하려면 브라우저의 새로 고침 단추를 클릭 합니다. 표시 됩니다는 `ProductName` 및 `UnitPrice` 새 임의로 선택 된 레코드에 대 한 값입니다.


[![표시 되는 임의의 제품의 이름과 가격](master-pages-and-asp-net-ajax-cs/_static/image14.png)](master-pages-and-asp-net-ajax-cs/_static/image13.png)

**그림 05**: 표시 되는 임의 제품의 이름과 가격 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image15.png))


### <a name="automatically-displaying-a-new-product-every-15-seconds"></a>자동으로 새 제품을 표시 15 초 마다

ASP.NET AJAX 프레임 워크; 지정된 된 시간에 포스트백을 수행 하는 타이머 컨트롤 포함 타이머의 포스트백 `Tick` 이벤트가 발생 합니다. UpdatePanel 내에서 타이머 컨트롤을 배치 하는 경우에는 म 다시 바인딩할 수 데이터를 임의로 선택 된 새 제품을 표시 하려면 DetailsView의 부분 페이지 포스트백을 트리거합니다.

이를 위해 도구 상자에서 타이머를 끌어서 UpdatePanel에 넣습니다. 타이머의 변경 `ID` 에서 `Timer1` 를 `ProductTimer` 및 해당 `Interval` 60000 속성에서 15000 까지입니다. `Interval` 15000를 설정 하면 15 초 마다 부분 페이지 포스트백을 트리거하는 타이머 발생 했는데 속성 포스트백 사이의 밀리초 수를 나타냅니다. 이 시점에서 타이머의 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](master-pages-and-asp-net-ajax-cs/samples/sample5.aspx)]

타이머의에 대 한 이벤트 처리기를 만들고 `Tick` 이벤트입니다. 이 이벤트 처리기에서 DetailsView의 호출 하 여 데이터 DetailsView 다시 바인딩할 필요 `DataBind` 메서드. 이렇게 다시 데이터를 검색 하 고 해당 데이터 소스 제어에서 DetailsView 지시 선택 하 고 새 임의로 표시 됩니다는 레코드 선택 (마찬가지로 때 브라우저의 새로 고침 단추를 클릭 하 여 페이지를 다시 로드).


[!code-csharp[Main](master-pages-and-asp-net-ajax-cs/samples/sample6.cs)]

그을 마쳤습니다. 브라우저를 통해 페이지를 다시 확인 합니다. 처음에 임의의 제품의 정보가 표시 됩니다. 화면을 꾸준히 보고 하는 경우, 15 초 후 새 제품에 대 한 정보 마법 대체 기존 표시를 확인할 수 있습니다.

명확 하 게 볼 수행, 디스플레이 마지막으로 수정한 시간을 표시 하는 UpdatePanel을 Label 컨트롤을 추가 해 보겠습니다. UpdatePanel 내부에 있는 레이블 웹 컨트롤을 추가, 설정 해당 `ID` 를 `LastUpdateTime`, 선택을 취소 하 고 해당 `Text` 속성입니다. 다음으로 UpdatePanel의에 대 한 이벤트 처리기를 만들고 `Load` 이벤트 및 레이블에 현재 시간을 표시 합니다. (UpdatePanel의 `Load` 전체 또는 일부 페이지 포스트백이 발생할 때마다 이벤트가 발생 합니다.)


[!code-csharp[Main](master-pages-and-asp-net-ajax-cs/samples/sample7.cs)]

이 변경을 완료 페이지에는 현재 표시 된 제품 로드 된 시간이 포함 됩니다. 그림 6 처음 방문 페이지를 보여줍니다. 그림 7 Timer 컨트롤에 "선택 되어" 하 고 새 제품에 대 한 정보를 표시 하는 UpdatePanel를 새로 고칠 15 초 후 페이지를 보여줍니다.


[![임의로 선택 된 제품 페이지 로드에 표시 됩니다.](master-pages-and-asp-net-ajax-cs/_static/image17.png)](master-pages-and-asp-net-ajax-cs/_static/image16.png)

**그림 06**: 임의로 선택 된 제품 A 페이지 로드에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image18.png))


[![매 15 초 마다 새 임의로 선택한 제품 표시](master-pages-and-asp-net-ajax-cs/_static/image20.png)](master-pages-and-asp-net-ajax-cs/_static/image19.png)

**그림 07**: 매 15 초 새 임의로 선택한 제품 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image21.png))


## <a name="step-3-using-the-scriptmanagerproxy-control"></a>ScriptManagerProxy 컨트롤을 사용 하 여 3 단계:

ASP.NET AJAX framework 클라이언트 라이브러리에 대 한 필요한 스크립트를 포함 하 여 함께 ScriptManager는 스크립트 기반 웹 서비스 및 사용자 지정 인증, 권한 부여 및 프로필 서비스에 대 한 사용자 지정 JavaScript 파일을 등록할 수도 있습니다. 일반적으로 이러한 사용자 지정은 특정 페이지와 관련이 있습니다. 그러나 사용자 지정 스크립트를 파일, 웹 서비스 참조 또는 인증, 권한 부여 또는 프로필 서비스를 마스터 페이지에 ScriptManager에서 참조 되는 경우에 포함 된 *모든* 는 웹 사이트의 페이지입니다.

추가 하려면 ScriptManager 관련 사용자 지정 하 여 페이지 별로 ScriptManagerProxy 컨트롤을 사용 합니다. ScriptManagerProxy 콘텐츠 페이지에 추가 하 고 사용자 지정 JavaScript 파일, 웹 서비스 참조 또는 인증, 권한 부여 또는 ScriptManagerProxy;에서 프로필 서비스를 등록할 수 있습니다. 특정 콘텐츠 페이지에 이러한 서비스를 등록 하는 중 것과 효과가 있습니다.

> [!NOTE]
> ASP.NET 페이지에 있는 둘 이상의 ScriptManager 컨트롤을 하나만 사용할 수 있습니다. 따라서 마스터 페이지에 ScriptManager 컨트롤 이미 정의 되어 있으면 콘텐츠 페이지에 ScriptManager 컨트롤을 추가할 수 없습니다. ScriptManagerProxy 목적 마스터 페이지에 ScriptManager를 정의 하지만 포함 하 여 페이지 별로 ScriptManager 사용자 지정을 추가 하는 기능을 개발자가 제공 하는 것입니다.


ScriptManagerProxy 컨트롤의 작동을 보려면 보겠습니다에서 UpdatePanel 보강 `ShowRandomProduct.aspx` 일시 중지 또는 재개 Timer 컨트롤을 클라이언트 쪽 스크립트를 사용 하는 단추를 포함 하도록 합니다. 타이머 컨트롤에이 원하는 기능을 얻기 위해 사용할 수 있는 세 가지 클라이언트 쪽 방법이 있습니다.

- `_startTimer()` -Timer 컨트롤 시작
- `_raiseTick()` -다시 게시 하 고 발생 시키는 함으로써 Timer 컨트롤 "틱"로 인해 해당 `Tick` 서버에서 이벤트
- `_stopTimer()` -Timer 컨트롤을 중지 합니다.

명명 된 변수로 JavaScript 파일을 만들어 보겠습니다 `timerEnabled` 및 라는 함수 `ToggleTimer`합니다. `timerEnabled` 변수 Timer 컨트롤은 현재 사용 가능 여부를 나타냅니다; 기본값은 true입니다. `ToggleTimer` 함수에서는 두 개의 입력 매개 변수를 사용할: 일시 중지/다시 시작 단추 및 클라이언트 쪽에 대 한 참조 `id` 타이머 컨트롤의 값입니다. 이 함수는 값을 설정/해제 `timerEnabled`Timer 컨트롤에 대 한 참조, 시작 또는 타이머를 중지 (값에 따라 `timerEnabled`), "일시 중지" 또는 "Resume" 단추의 표시 텍스트를 업데이트 합니다. 일시 중지/다시 시작 단추를 클릭할 때마다이 함수가 호출 됩니다.

이라는 웹 사이트에서 새 폴더를 만들어 시작 `Scripts`합니다. 다음으로, 라는 스크립트 폴더에 새 파일을 추가 `TimerScript.js` JScript 파일 형식입니다.


[![스크립트 폴더에 새 JavaScript 파일을 추가 합니다.](master-pages-and-asp-net-ajax-cs/_static/image23.png)](master-pages-and-asp-net-ajax-cs/_static/image22.png)

**그림 08**: 새 JavaScript 파일을 추가 `Scripts` 폴더 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image24.png))


[![웹 사이트에 추가 된 새 JavaScript 파일](master-pages-and-asp-net-ajax-cs/_static/image26.png)](master-pages-and-asp-net-ajax-cs/_static/image25.png)

**그림 09**: A 새 JavaScript 파일은 웹 사이트에 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image27.png))


다음으로 TimerScript.js 파일에 다음 스크립트를 추가 합니다.


[!code-csharp[Main](master-pages-and-asp-net-ajax-cs/samples/sample8.cs)]

이제이 사용자 지정 JavaScript 파일에 등록 해야 `ShowRandomProduct.aspx`합니다. 으로 돌아와서 `ShowRandomProduct.aspx` 페이지로 ScriptManagerProxy 컨트롤을 추가 하 고 설정의 `ID` 를 `MyManagerProxy`합니다. 사용자 지정 JavaScript를 등록 하려면 파일 ScriptManagerProxy 컨트롤 디자이너에서 선택 하 고 속성 창으로 이동 하십시오. 속성 중 하나를 스크립트 제목은입니다. 이 속성을 선택 하면 그림 10에 표시 되는 ScriptReference 컬렉션 편집기를 표시 합니다. 새 스크립트 참조를 포함 하 여 경로 속성에서 스크립트 파일 경로 입력 한 다음 추가 단추 클릭: `~/Scripts/TimerScript.js`합니다.


[![ScriptManagerProxy 컨트롤에 대 한 스크립트 참조를 추가 합니다.](master-pages-and-asp-net-ajax-cs/_static/image29.png)](master-pages-and-asp-net-ajax-cs/_static/image28.png)

**그림 10**: ScriptManagerProxy 컨트롤에 대 한 스크립트 참조를 추가 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image30.png))


ScriptManagerProxy 컨트롤의 스크립트 참조를 추가 하는 것의 선언적 태그를 포함 하도록 업데이트 됩니다는 `<Scripts>` 단일 컬렉션 `ScriptReference` 항목 태그의 다음 코드 조각에서는 보여 줍니다.


[!code-aspx[Main](master-pages-and-asp-net-ajax-cs/samples/sample9.aspx)]

`ScriptReference` 항목 ScriptManagerProxy 렌더링 된 태그에 JavaScript 파일에 대 한 참조를 포함 하도록 지시 합니다. 즉, 사용자 지정을 등록 하 여 스크립트에 ScriptManagerProxy는 `ShowRandomProduct.aspx` 페이지의 렌더링 된 출력에 다른 항목을 지금 포함 `<script src="url"></script>` 태그: `<script src="Scripts/TimerScript.js" type="text/javascript"></script>`합니다.

이제 호출할 수는 `ToggleTimer` 함수에 정의 된 `TimerScript.js` 에서 클라이언트 스크립트에서는 `ShowRandomProduct.aspx` 페이지. UpdatePanel 내에서 다음 HTML을 추가 합니다.


[!code-aspx[Main](master-pages-and-asp-net-ajax-cs/samples/sample10.aspx)]

그러면 "일시 중지" 텍스트가 있는 단추가 표시 됩니다. 때마다 클릭할 JavaScript 함수 `ToggleTimer` 호출, 단추와 Timer 컨트롤의 id 값에 대 한 참조를 전달 (`ProductTimer`). 가져오는 구문은 `id` 타이머 컨트롤의 값입니다. `<%=ProductTimer.ClientID%>` 값을 내보내는 `ProductTimer` 타이머 컨트롤 `ClientID` 속성입니다. 에 [ *콘텐츠 페이지에서 컨트롤 ID 명명* ](control-id-naming-in-content-pages-cs.md) 자습서 서버 쪽 간의 차이점에 설명 했습니다 `ID` 값과 클라이언트 쪽 결과 `id` 값 방법과 `ClientID` 클라이언트 쪽 반환 `id`합니다.

그림 11 브라우저를 통해 먼저 방문 하는 경우이 페이지를 보여 줍니다. 타이머는 현재 실행 되 고 15 초 마다 표시 된 제품 정보를 업데이트 합니다. 그림 12는 일시 중지 단추를 클릭 한 후 화면을 보여 줍니다. 일시 중지 단추를 클릭 하면 타이머를 중지 하 고 단추의 텍스트를 "Resume"를 업데이트 합니다. 제품 정보는 새로 고침 (및 15 초 마다 새로 고쳐집니다 계속) 후 사용자가 다시 시작을 클릭 합니다.


[![타이머 컨트롤을 중지 하려면 일시 중지 단추를 클릭 합니다.](master-pages-and-asp-net-ajax-cs/_static/image32.png)](master-pages-and-asp-net-ajax-cs/_static/image31.png)

**그림 11**: Timer 컨트롤을 중지 하려면 일시 중지 단추 클릭 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image33.png))


[![타이머를 시작 하려면 [계속] 단추를 클릭 합니다.](master-pages-and-asp-net-ajax-cs/_static/image35.png)](master-pages-and-asp-net-ajax-cs/_static/image34.png)

**그림 12**: 타이머를 시작 하려면 [계속] 단추 클릭 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image36.png))


## <a name="summary"></a>요약

ASP.NET AJAX 프레임 워크를 사용 하 여 AJAX 사용 웹 응용 프로그램을 빌드하는 경우 반드시 모든 AJAX 사용 웹 페이지에 ScriptManager 컨트롤을 포함 합니다. 이 프로세스를 용이 하 게 하려면 각각의 모든 콘텐츠 페이지에 ScriptManager를 추가 하려면 기억할 필요 하지 않고 마스터 페이지에 ScriptManager 추가할 수 있습니다. 1 단계 2 단계에서 콘텐츠 페이지에서 AJAX 기능을 구현 하는 동안 마스터 페이지에 ScriptManager를 추가 하는 방법을 배웠습니다.

사용자 지정 스크립트를 스크립트 기반 웹 서비스에 대 한 참조를 추가 해야 하거나 사용자 지정된 인증, 권한 부여 또는 프로필 서비스를 특정 콘텐츠 페이지에 콘텐츠 페이지에 ScriptManagerProxy 컨트롤을 추가 하 고 다음을 구성 하는 경우는 사용자 지정 있습니다. 단계 3 특정 콘텐츠 페이지에 사용자 지정 JavaScript 파일을 등록 하는 ScriptManagerProxy를 사용 하는 방법을 검사 합니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET AJAX 프레임 워크](../../../../ajax/index.md)
- [ASP.NET AJAX 자습서](../aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax.md)
- [ASP.NET AJAX 비디오](../../../videos/aspnet-ajax/index.md)
- [Microsoft ASP.NET AJAX와 대화형 사용자 인터페이스 빌드](http://aspnet.4guysfromrolla.com/articles/101007-1.aspx)
- [NEWID 임의로 정렬 레코드를 사용 하 여](http://www.sqlteam.com/article/using-newid-to-randomly-sort-records)
- [타이머 컨트롤을 사용 하 여](http://aspnet.4guysfromrolla.com/articles/061808-1.aspx)

### <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 작성자 여러 ASP/ASP.NET 설명서와 4GuysFromRolla.com의 창립자의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 3.5 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)합니다. Scott에 도달할 수 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com) 또는에서 그의 블로그 통해 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](interacting-with-the-content-page-from-the-master-page-cs.md)
> [다음](specifying-the-master-page-programmatically-cs.md)
