---
uid: web-forms/overview/older-versions-getting-started/master-pages/master-pages-and-asp-net-ajax-cs
title: 마스터 페이지 및 ASP.NET AJAX (C#) | Microsoft Docs
author: rick-anderson
description: ASP.NET AJAX 및 마스터 페이지를 사용 하기 위한 옵션에 설명 합니다. ScriptManagerProxy 클래스를 사용 하 여 살펴봅니다. 다양 한 JS 파일은 dependi를 로드 하는 방법에 대해 설명 하는 중...
ms.author: aspnetcontent
ms.date: 07/11/2008
ms.assetid: 0c55eb66-ba44-4d49-98e8-5c87fd9b1111
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/master-pages-and-asp-net-ajax-cs
msc.type: authoredcontent
ms.openlocfilehash: e8a4f9780b41c5ff77b996894d9f91a532877245
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37842486"
---
<a name="master-pages-and-aspnet-ajax-c"></a>마스터 페이지 및 ASP.NET AJAX (C#)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_08_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_08_CS.pdf)

> ASP.NET AJAX 및 마스터 페이지를 사용 하기 위한 옵션에 설명 합니다. ScriptManagerProxy 클래스를 사용 하 여 살펴봅니다. 페이지나 콘텐츠 페이지는 ScriptManager 마스터에서 사용 되는지 여부에 따라 다양 한 JS 파일이 로드 되는 방법을 설명 합니다.


## <a name="introduction"></a>소개

점점 더 많은 개발자를 구축 하는 지난 몇 년간 [AJAX](http://en.wikipedia.org/wiki/Ajax_(programming))-웹 응용 프로그램을 사용 하도록 설정 합니다. AJAX 지원 웹 사이트를 여러 가지 관련된 웹 기술 사용 하 여 반응이 빠른 사용자 환경을 제공. Microsoft의 탁월할 감사는 AJAX 사용 ASP.NET 응용 프로그램을 만드는 [ASP.NET AJAX 프레임 워크](../../../../ajax/index.md)합니다. ASP.NET AJAX는 ASP.NET 3.5 및 Visual Studio 2008에 기본 제공 되는 ASP.NET 2.0 응용 프로그램에 대 한 별도 다운로드로 제공 됩니다.

ASP.NET AJAX 프레임 워크를 사용 하 여 AJAX 사용 웹 페이지를 빌드할 때 정확 하 게 하나를 추가 해야 합니다 있습니다 [ScriptManager 컨트롤](https://msdn.microsoft.com/library/bb398863.aspx) 프레임 워크를 사용 하는 각 페이지에 있습니다. 이름에서 알 수 있듯이 ScriptManager는 AJAX 사용 웹 페이지에 사용 된 클라이언트 쪽 스크립트를 관리 합니다. ScriptManager는 최소한 해당 구성을 ASP.NET AJAX 클라이언트 라이브러리를 JavaScript 파일을 다운로드 하도록 브라우저에 지시 하는 HTML을 내보냅니다. 사용자 지정 JavaScript 파일, 스크립트 사용 웹 서비스 및 사용자 지정 응용 프로그램 서비스 기능을 등록 하려면 데도 수 있습니다.

사이트 사용 하 여 마스터 페이지 (예상) 하는 대로 하는 경우 반드시 필요가 없습니다 모든 단일 콘텐츠 페이지에 ScriptManager 컨트롤을 추가 하려면 대신, 마스터 페이지에 ScriptManager 컨트롤을 추가할 수 있습니다. 이 자습서에는 마스터 페이지에 ScriptManager 컨트롤을 추가 하는 방법을 보여 줍니다. ScriptManagerProxy 컨트롤을 사용 하 여 특정 콘텐츠 페이지에서 사용자 지정 스크립트 및 스크립트 서비스를 등록 하는 방법에 대해서도 살펴봅니다.

> [!NOTE]
> ASP.NET AJAX 프레임 워크를 사용 하 여 AJAX 사용 웹 응용 프로그램을 빌드하거나 디자인이 자습서 탐색 하지 않습니다. AJAX를 사용 하 여 대 한 자세한 내용은 참조는 [ASP.NET AJAX 비디오](../../../videos/aspnet-ajax/index.md) 및 [자습서](../aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax.md)뿐만 아니라이 자습서의 끝에 추가 정보 섹션에 나열 된 리소스만으로 합니다.


## <a name="examining-the-markup-emitted-by-the-scriptmanager-control"></a>ScriptManager 컨트롤에서 내보낸 태그를 검사 합니다.

ScriptManager 컨트롤은 해당 구성을 ASP.NET AJAX 클라이언트 라이브러리를 JavaScript 파일을 다운로드 하도록 브라우저에 지시 하는 태그를 내보냅니다. 또한이 라이브러리를 초기화 하는 페이지에 약간의 인라인 JavaScript 추가 합니다. 다음 태그에는 ScriptManager 컨트롤을 포함 하는 페이지의 렌더링된 된 출력에 추가 되는 내용을 보여 줍니다.


[!code-html[Main](master-pages-and-asp-net-ajax-cs/samples/sample1.html)]

합니다 `<script src="url"></script>` 태그 다운로드에서 JavaScript 파일을 실행 하는 브라우저를 지시 *url*합니다. ScriptManager는 이러한 3 개의 태그를; 내보냅니다. 파일을 참조 하나 `WebResource.axd`반면 다른 두 파일을 참조할 `ScriptResource.axd`합니다. 웹 사이트의 파일과 이러한 파일이 실제로 존재 하지 않습니다. 대신, 이러한 파일 중 하나에 대 한 요청을 웹 서버에 도착 하는 경우 ASP.NET 엔진 쿼리 문자열을 검사 하 고 적절 한 JavaScript 콘텐츠를 반환 합니다. 이러한 세 가지 외부 JavaScript 파일에 의해 제공 된 스크립트는 ASP.NET AJAX 프레임 워크의 클라이언트 라이브러리를 구성 합니다. 다른 `<script>` ScriptManager에서 내보낸 태그는이 라이브러리를 초기화 하는 인라인 스크립트를 포함 합니다.

외부 스크립트 참조 및 인라인 스크립트 ScriptManager에서 내보낸 필수적인 프레임 워크를 사용 하지 않는 페이지에 대 한 필요 하지는 않은 ASP.NET AJAX 프레임 워크를 사용 하 여 페이지에 대 한 합니다. 따라서만 ASP.NET AJAX 프레임 워크를 사용 하는 해당 페이지에 ScriptManager를 추가 하는 데 이상적 임을 이유 수 있습니다. 및이 충분 하지만 말해도 반복적인 작업을 모든 페이지에 ScriptManager 컨트롤을 추가를 완료 하는 프레임 워크를 사용 하는 여러 페이지에 있는 경우. 또는 다음 모든 콘텐츠 페이지에이 필요한 스크립트를 삽입 하는 마스터 페이지에 ScriptManager를 추가할 수 있습니다. 이 방법을 사용 하 여 마스터 페이지에 의해 이미 있기 때문에 ASP.NET AJAX 프레임 워크를 사용 하는 새 페이지에 ScriptManager를 추가 해야 필요가 없습니다. 1 단계에서는 마스터 페이지에 ScriptManager를 추가 하는 과정입니다.

> [!NOTE]
> 마스터 페이지의 사용자 인터페이스 내에서 AJAX 기능을 포함 하려는 경우 해당 문제에는 여지가-마스터 페이지에 ScriptManager를 포함 해야 하는 것입니다.


하나의 마스터 페이지에 ScriptManager를 추가 하는 단점은 위의 스크립트를 내보냅니다 *마다* 여부에 관계 없이 페이지에서 필요한 해당 합니다. 이 불필요 하 게 대역폭 (마스터 페이지)를 통해 포함 된 ScriptManager가 아직 ASP.NET AJAX 프레임 워크의 모든 기능을 사용 하지 않는 해당 페이지에 대 한 명확 하 게 이어집니다. 그러나 대역폭을 소비 하는 어느 정도?

- 실제 콘텐츠 (위에 표시 된) ScriptManager에서 내보낸 1KB 조금 넘게 합계를 구합니다.
- 하지만 참조 하 세 외부 스크립트 파일을 `<script>` 요소인 약 450KB의 압축 되지 않은 데이터를 구성, gzip 압축을 사용 하는 웹 사이트에서이 총 대역폭 100KB 거의 줄일 수 있습니다. 그러나 이러한 스크립트 파일은 1 년만 한 번 다운로드 해야 하는 의미에 대 한 브라우저에서 캐시 및 다음 사이트에서 다른 페이지에서 다시 사용할 수 있습니다.

최상의 경우에서 스크립트 파일은 캐시 되 면 총 비용을 지불 합니다 1KB는 영향은 매우 적습니다. 그러나 최악의 경우, 압축의 모든 형태를 사용 하지 않는 경우 스크립트 파일이 다운로드 되지 않은 아직 및 웹 서버-대역폭 적중은 약 450KB, 초 또는 1 분까지 광대역 연결을 통해 두에서 어디서 나 추가할 수 있는  전화 접속 모뎀을 통해 사용자입니다. 좋은 소식은 외부 스크립트 파일 브라우저에 의해 캐시 되므로이 최악의 시나리오 드물게 발생 합니다.

> [!NOTE]
> 여전히 판단 될 경우 마스터 페이지에 ScriptManager 컨트롤을 배치 합니다. 불편을 Web Form 것이 좋습니다 (의 `<form runat="server">` 마스터 페이지의 태그). 포스트백 모델을 사용 하는 모든 ASP.NET 페이지는 Web Form을 정확 하 게 하나를 포함 해야 합니다. Web Form 추가 추가 콘텐츠: 숨겨진된 폼 필드의 숫자는 `<form>` 자체 태그 및 스크립트에서 포스트백을 시작 하는 것에 대 한 JavaScript 함수 필요한 경우. 이 태그 페이지 다시 게시 하지는 필요 하지 않습니다. 마스터 페이지에서 Web Form을 제거 하 고 하나는 각 콘텐츠 페이지에 수동으로 추가 하 여이 불필요 한 태그를 제거할 수 없습니다. 그러나 마스터 페이지에서 Web Form의 이점에는 특정 콘텐츠 페이지에 불필요 하 게 추가할 수 없도록 단점 보다 많다고입니다.


## <a name="step-1-adding-a-scriptmanager-control-to-the-master-page"></a>1 단계: 마스터 페이지에 ScriptManager 컨트롤을 추가

ASP.NET AJAX 프레임 워크를 사용 하는 모든 웹 페이지에 ScriptManager 컨트롤을 정확 하 게 하나 있어야 합니다. 이 요구 사항으로 인해 모든 콘텐츠 페이지에 자동으로 포함 하는 ScriptManager 컨트롤에 포함 되도록 마스터 페이지에 단일 ScriptManager 컨트롤을 추가 하는 것이 일반적으로 만듭니다. 또한 ScriptManager가 UpdatePanel 및 UpdateProgress 컨트롤과 같은 ASP.NET AJAX 서버 컨트롤은 앞에 나와야 합니다. 따라서 Web Form 내 ContentPlaceHolder 컨트롤 보다 먼저 ScriptManager를 배치 하는 것이 좋습니다.

엽니다는 `Site.master` 마스터 페이지 및 하기 전에 Web Form 내 페이지에 ScriptManager 컨트롤을 추가 합니다 `<div id="topContent">` 요소 (그림 1 참조). Visual Web Developer 2008 또는 Visual Studio 2008를 사용 하는 경우 ScriptManager 컨트롤은 AJAX 확장명 탭에서 도구 상자에 있습니다. Visual Studio 2005를 사용 하는 경우 먼저 ASP.NET AJAX 프레임 워크를 설치 하 고 도구 상자 컨트롤을 추가 해야 합니다. 방문 합니다 [ASP.NET AJAX Wiki](https://github.com/DevExpress/AjaxControlToolkit/wiki) ASP.NET 2.0에 대 한 프레임 워크를 가져오려고 합니다.

변경 페이지에 ScriptManager에 추가한 후 해당 `ID` 에서 `ScriptManager1` 에 `MyManager`입니다.


[![마스터 페이지에 ScriptManager를 추가](master-pages-and-asp-net-ajax-cs/_static/image2.png)](master-pages-and-asp-net-ajax-cs/_static/image1.png)

**그림 01**: 마스터 페이지에 ScriptManager를 추가 ([큰 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image3.png))


## <a name="step-2-using-the-aspnet-ajax-framework-from-a-content-page"></a>2 단계: 콘텐츠 페이지 로부터 ASP.NET AJAX 프레임 워크 사용

마스터 페이지에 추가 되는 ScriptManager 컨트롤을 사용 하 여 모든 콘텐츠 페이지에 이제 ASP.NET AJAX 프레임 워크 기능을 추가할 수 했습니다. Northwind 데이터베이스에서 임의로 선택 된 제품을 표시 하는 새 ASP.NET 페이지를 만들어 보겠습니다. 새 제품을 보여 주는 15 초 마다이 표시를 업데이트 하는 ASP.NET AJAX 프레임 워크의 타이머 컨트롤을 사용 하겠습니다.

명명 된 루트 디렉터리에 새 페이지를 만들어 시작 `ShowRandomProduct.aspx`합니다. 이 새 페이지를 바인딩할 것을 잊지 마세요는 `Site.master` 마스터 페이지입니다.


[![웹 사이트에 새 ASP.NET 페이지를 추가 합니다.](master-pages-and-asp-net-ajax-cs/_static/image5.png)](master-pages-and-asp-net-ajax-cs/_static/image4.png)

**그림 02**: 웹 사이트에 새 ASP.NET 페이지를 추가 ([큰 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image6.png))


회수에 [ *마스터 페이지에서 제목, 메타 태그 및 기타 HTML 헤더 지정* ](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) 자습서 라는 기본 페이지를 사용자 지정 클래스를 만들었습니다 `BasePage` 있었다면 페이지 제목 생성 명시적으로 설정 합니다. 로 이동 합니다 `ShowRandomProduct.aspx` 페이지의 코드 숨김 클래스에서 파생 되 게 하 고 `BasePage` (대신에서 `System.Web.UI.Page`).

마지막으로 업데이트 된 `Web.sitemap` 이 단원에 대 한 항목을 포함 하는 파일입니다. 아래에 다음 태그를 추가 합니다 `<siteMapNode>` 콘텐츠 페이지 상호 작용 단원으로 마스터에 대 한 합니다.


[!code-xml[Main](master-pages-and-asp-net-ajax-cs/samples/sample2.xml)]

이 추가 `<siteMapNode>` 요소 단원에서 반영 됩니다 (그림 5 참조)를 나열 합니다.

### <a name="displaying-a-randomly-selected-product"></a>임의로 선택한 제품 표시

돌아가서 `ShowRandomProduct.aspx`합니다. 디자이너에서 UpdatePanel 컨트롤에 도구 상자에서 끌어 합니다 `MainContent` 콘텐츠 컨트롤 및 설정 해당 `ID` 속성을 `ProductPanel`입니다. UpdatePanel 부분 페이지 다시 게시를 통해 비동기적으로 업데이트할 수 있는 화면의 영역을 나타냅니다.

우리의 첫 번째 작업 UpdatePanel 내에서 임의로 선택한 제품에 대 한 정보를 표시 하는 것입니다. DetailsView 컨트롤을 UpdatePanel 드래그 하 여 시작 합니다. DetailsView 컨트롤의 `ID` 속성을 `ProductInfo` 지울 및 해당 `Height` 고 `Width` 속성입니다. DetailsView의 스마트 태그를 확장 하 고 데이터 소스 선택 드롭다운 목록에서 선택 DetailsView 라는 새 SqlDataSource 컨트롤을 바인딩할 `RandomProductDataSource`합니다.


[![DetailsView 새 SqlDataSource 컨트롤에 바인딩](master-pages-and-asp-net-ajax-cs/_static/image8.png)](master-pages-and-asp-net-ajax-cs/_static/image7.png)

**그림 03**: DetailsView 새 SqlDataSource 컨트롤을 바인딩할 ([큰 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image9.png))


통해 Northwind 데이터베이스에 연결 하도록 SqlDataSource 컨트롤을 구성 합니다 `NorthwindConnectionString` (에서 만든 합니다 [ *콘텐츠 페이지에서 마스터 페이지와 상호 작용* ](interacting-with-the-content-page-from-the-master-page-cs.md) 자습서). 때 select 문의 구성 사용자 지정 SQL 문을 지정 하 고 다음 쿼리를 입력 하려면 선택 합니다.


[!code-sql[Main](master-pages-and-asp-net-ajax-cs/samples/sample3.sql)]

합니다 `TOP 1` 키워드는 `SELECT` 쿼리에서 반환 된 첫 번째 레코드를 반환 합니다. 합니다 [ `NEWID()` 함수](https://msdn.microsoft.com/library/ms190348.aspx) 새 생성 [전역적으로 고유 식별자 값 (GUID)](http://en.wikipedia.org/wiki/Globally_Unique_Identifier) 에서 사용할 수 있습니다는 `ORDER BY` 임의 순서 대로 테이블의 레코드를 반환 하는 절.


[![단일, 임의로 선택 된 레코드를 반환할 수 SqlDataSource를 구성 합니다.](master-pages-and-asp-net-ajax-cs/_static/image11.png)](master-pages-and-asp-net-ajax-cs/_static/image10.png)

**그림 04**: 단일 임의로 선택한 레코드를 반환할 SqlDataSource 구성 ([큰 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image12.png))


마법사를 완료 한 후 Visual Studio 위의 쿼리에서 반환 되는 두 열에 대 한 BoundField를 만듭니다. 이 시점에서 페이지의 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](master-pages-and-asp-net-ajax-cs/samples/sample4.aspx)]

그림 5는 `ShowRandomProduct.aspx` 브라우저를 통해 볼 때 페이지입니다. 페이지를 다시 로드 하려면 브라우저의 새로 고침 단추를 클릭 합니다. 표시 되어야 합니다 `ProductName` 및 `UnitPrice` 새 임의로 선택 된 레코드에 대 한 값입니다.


[![임의 제품의 이름과 가격 표시 됩니다.](master-pages-and-asp-net-ajax-cs/_static/image14.png)](master-pages-and-asp-net-ajax-cs/_static/image13.png)

**그림 05**: 표시 되는 임의 제품 이름과 가격 ([큰 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image15.png))


### <a name="automatically-displaying-a-new-product-every-15-seconds"></a>새 제품을 자동으로 표시 15 초 마다

ASP.NET AJAX 프레임 워크는; 지정한 시간에 포스트백을 수행 하는 타이머 컨트롤 타이머의 포스트백 `Tick` 이벤트가 발생 합니다. 타이머 컨트롤이 UpdatePanel 내에 배치 하는 경우는 우리가 다시 바인딩할 수 데이터를 임의로 선택 된 새 제품을 표시 하려면 DetailsView 부분 페이지 포스트백을 트리거합니다.

이렇게 하려면 도구 상자에서 타이머를 끌어서 UpdatePanel에 넣습니다. 타이머의 변경 `ID` 에서 `Timer1` 하 `ProductTimer` 고 `Interval` 15000 60000 속성입니다. `Interval` 15000 설정 하면 15 초 마다 부분 페이지 포스트백을 트리거하는 타이머; 속성 포스트백 간격 (밀리초)의 수를 나타냅니다. 이 시점에서 타이머의 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](master-pages-and-asp-net-ajax-cs/samples/sample5.aspx)]

타이머의에 대 한 이벤트 처리기를 만들고 `Tick` 이벤트입니다. 이 이벤트 처리기에서 DetailsView의 호출 하 여 데이터 DetailsView 다시 바인딩할 필요 `DataBind` 메서드. 이렇게 DetailsView 컨트롤이 해당 데이터 소스에서 데이터를 다시 검색할 지시 선택한 새 임의로 표시 하는 레코드 선택 (마찬가지로 때 브라우저의 새로 고침 단추를 클릭 하 여 페이지를 다시 로드).


[!code-csharp[Main](master-pages-and-asp-net-ajax-cs/samples/sample6.cs)]

이것이 전부입니다! 브라우저를 통해 페이지를 다시 확인 합니다. 처음에 임의 제품의 정보가 표시 됩니다. 있으므로 편안 하 게 화면을 보고 하는 경우에 15 초 후 새 제품에 대 한 내용은 마술 대체 기존 표시를 확인할 수 있습니다.

여기에 일어나를 더 잘 보려면 표시 된 마지막 업데이트 시간을 표시 하 UpdatePanel에 레이블 컨트롤을 추가 해 보겠습니다. UpdatePanel 내에 있는 레이블 웹 컨트롤을 추가 해당 `ID` 하 `LastUpdateTime`, 선택 취소 하 고 해당 `Text` 속성. 다음으로 UpdatePanel에 대 한 이벤트 처리기를 만들고 `Load` 이벤트 및 레이블에 현재 시간을 표시 합니다. (UpdatePanel의 `Load` 전체 또는 부분 페이지 포스트백이 발생할 때마다 이벤트가 발생 합니다.)


[!code-csharp[Main](master-pages-and-asp-net-ajax-cs/samples/sample7.cs)]

전체이 변경으로 페이지에 현재 표시 된 제품 로드 된 시간이 포함 됩니다. 그림 6에서는 먼저 방문 되 면 페이지를 보여 줍니다. 그림 7는 Timer 컨트롤에 "선택" 후 새 제품에 대 한 정보를 표시 하 UpdatePanel 새로 고쳤다는 것 15 초 후 페이지를 보여줍니다.


[![페이지 로드 시 임의로 선택한 제품 표시 됩니다.](master-pages-and-asp-net-ajax-cs/_static/image17.png)](master-pages-and-asp-net-ajax-cs/_static/image16.png)

**그림 06**: 임의로 선택한 제품은 페이지 로드 시 표시 됩니다 ([큰 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image18.png))


[![새 임의로 선택한 제품 표시는 15 초 마다](master-pages-and-asp-net-ajax-cs/_static/image20.png)](master-pages-and-asp-net-ajax-cs/_static/image19.png)

**그림 07**: 새 임의로 선택한 제품 표시 되는 모든 15 초 ([큰 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image21.png))


## <a name="step-3-using-the-scriptmanagerproxy-control"></a>3 단계: ScriptManagerProxy 컨트롤 사용

ASP.NET AJAX 프레임 워크 클라이언트 라이브러리에 대 한 필요한 스크립트를 포함 하는 함께 ScriptManager는 사용자 지정 JavaScript 파일, 스크립트 사용 웹 서비스 및 사용자 지정 인증, 권한 부여 및 프로필 서비스에 대 한 참조를 등록할 수도 있습니다. 일반적으로 이러한 사용자 지정 특정 페이지에 적용 됩니다. 그러나 사용자 지정 스크립트 파일, 웹 서비스 참조 또는 인증 권한 부여 나 프로필 서비스 마스터 페이지에 ScriptManager에서 참조 되는 경우에 포함 된 *모든* 웹 사이트의 페이지입니다.

추가할 ScriptManager와 관련 된 사용자 지정 하 여 페이지 별로 ScriptManagerProxy 컨트롤을 사용 합니다. 콘텐츠 페이지에는 ScriptManagerProxy를 추가 하 고 사용자 지정 JavaScript 파일, 웹 서비스 참조 또는 인증, 권한 부여 또는 ScriptManagerProxy;에서 프로필 서비스를 등록 이 특정 콘텐츠 페이지에 이러한 서비스를 등록 하는 효과가 있습니다.

> [!NOTE]
> ASP.NET 페이지에 있는 둘 이상의 ScriptManager 컨트롤을 하나만 사용할 수 있습니다. 따라서 ScriptManager 컨트롤은 마스터 페이지에 이미 정의 되어 있으면 해당 콘텐츠 페이지에 ScriptManager 컨트롤을 추가할 수 없습니다. ScriptManagerProxy의 유일한 용도 마스터 페이지에 ScriptManager를 정의 하지만 ScriptManager 사용자 지정에서 페이지 단위로 추가 하는 기능을 아직 개발자 들을 제공 하는 것입니다.


ScriptManagerProxy 컨트롤의 작동을 확인 하려면에서 UpdatePanel 보겠습니다 보강 `ShowRandomProduct.aspx` 일시 중지 또는 재개 Timer 컨트롤에 클라이언트측 스크립트를 사용 하는 단추를 포함 합니다. Timer 컨트롤에는이 원하는 기능을 얻기 위해 사용할 수 있는 세 가지 클라이언트 쪽 방법이 있습니다.

- `_startTimer()` -Timer 컨트롤 시작
- `_raiseTick()` -다시 게시 하 고 발생 시키는 하므로 "틱" Timer 컨트롤을 사용 하면 해당 `Tick` 서버의 이벤트
- `_stopTimer()` -Timer 컨트롤을 중지 합니다.

라는 변수를 사용 하 여 JavaScript 파일을 만들어 보겠습니다 `timerEnabled` 라는 함수 및 `ToggleTimer`합니다. `timerEnabled` 변수 Timer 컨트롤은 현재 사용 여부를 나타냅니다; 기본값은 true로 합니다. 합니다 `ToggleTimer` 함수는 두 개의 입력 매개 변수로: 일시 중지/다시 시작 단추 및 클라이언트 쪽에 대 한 참조 `id` 타이머 컨트롤의 값입니다. 이 함수에 값을 설정/해제 `timerEnabled`Timer 컨트롤에 대 한 참조를 가져옵니다, 시작 또는 타이머를 중지 (값에 따라 `timerEnabled`), "일시 중지" 또는 "Resume" 단추의 표시 텍스트를 업데이트 합니다. 일시 중지/다시 시작 단추를 클릭할 때마다이 함수가 호출 됩니다.

라는 웹 사이트에 새 폴더를 만들어 시작 `Scripts`합니다. 다음으로 명명 된 Scripts 폴더로 새 파일을 추가 `TimerScript.js` JScript 파일 형식입니다.


[![스크립트 폴더에 새 JavaScript 파일을 추가 합니다.](master-pages-and-asp-net-ajax-cs/_static/image23.png)](master-pages-and-asp-net-ajax-cs/_static/image22.png)

**그림 08**: 새 JavaScript 파일을 추가 합니다 `Scripts` 폴더 ([클릭 하 여 큰 이미지 보기](master-pages-and-asp-net-ajax-cs/_static/image24.png))


[![웹 사이트에 추가한 새 JavaScript 파일](master-pages-and-asp-net-ajax-cs/_static/image26.png)](master-pages-and-asp-net-ajax-cs/_static/image25.png)

**그림 09**: 웹 사이트에 추가한 새 JavaScript 파일 ([큰 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image27.png))


다음으로, TimerScript.js 파일에 다음 스크립트를 추가 합니다.


[!code-csharp[Main](master-pages-and-asp-net-ajax-cs/samples/sample8.cs)]

이제이 사용자 지정 JavaScript 파일에 등록 해야 `ShowRandomProduct.aspx`합니다. 돌아갑니다 `ShowRandomProduct.aspx` ScriptManagerProxy 컨트롤을 페이지에 추가 하 고 설정 해당 `ID` 에 `MyManagerProxy`입니다. 사용자 지정 JavaScript를 등록 하려면 파일 디자이너에서 ScriptManagerProxy 컨트롤을 선택한 다음 속성 창으로 이동 합니다. 속성 중 하나를 스크립트 제목은입니다. 이 속성을 선택 하면 그림 10 ScriptReference 컬렉션 편집기가 표시 됩니다. 새 스크립트 참조를 포함 하 여 경로 속성에서 스크립트 파일 경로 입력 한 다음 추가 단추 클릭: `~/Scripts/TimerScript.js`합니다.


[![ScriptManagerProxy 컨트롤에 대 한 스크립트 참조를 추가 합니다.](master-pages-and-asp-net-ajax-cs/_static/image29.png)](master-pages-and-asp-net-ajax-cs/_static/image28.png)

**그림 10**: ScriptManagerProxy 컨트롤에 대 한 스크립트 참조를 추가 ([큰 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image30.png))


태그를 포함 하도록 업데이트 됩니다 선언적의 ScriptManagerProxy 컨트롤 스크립트 참조를 추가한 후는 `<Scripts>` 단일을 사용 하 여 컬렉션 `ScriptReference` 항목 태그의 다음 코드 조각으로 보여 줍니다.


[!code-aspx[Main](master-pages-and-asp-net-ajax-cs/samples/sample9.aspx)]

`ScriptReference` 항목의 렌더링 된 태그에서 JavaScript 파일에 대 한 참조를 포함 하도록 ScriptManagerProxy 지시 합니다. 즉, 사용자 지정을 등록 하 여 스크립트를 ScriptManagerProxy 합니다 `ShowRandomProduct.aspx` 페이지의 렌더링 된 출력에 다른 항목을 이제 포함 `<script src="url"></script>` 태그: `<script src="Scripts/TimerScript.js" type="text/javascript"></script>`합니다.

이제 호출할 수 있습니다 합니다 `ToggleTimer` 에 정의 된 함수 `TimerScript.js` 에서 클라이언트 스크립트에서는 `ShowRandomProduct.aspx` 페이지입니다. UpdatePanel 내에 다음 HTML을 추가 합니다.


[!code-aspx[Main](master-pages-and-asp-net-ajax-cs/samples/sample10.aspx)]

이 텍스트 "일시 중지"를 사용 하 여 단추를 표시 합니다. 때마다 클릭할 JavaScript 함수 `ToggleTimer` 가 호출 단추와 타이머 컨트롤의 id 값에 대 한 참조가 전달 (`ProductTimer`). 가져오기에 대 한 구문은 `id` 타이머 컨트롤의 값입니다. `<%=ProductTimer.ClientID%>` 값을 내보냅니다 합니다 `ProductTimer` Timer 컨트롤 `ClientID` 속성입니다. 에 [ *콘텐츠 페이지의 컨트롤 ID 명명* ](control-id-naming-in-content-pages-cs.md) 자습서 서버 쪽 간의 차이점을 설명 했습니다 `ID` 값과 결과 클라이언트 쪽 `id` 값 방법과 `ClientID` 클라이언트 쪽 반환 `id`합니다.

그림 11에서는 브라우저를 통해 처음 방문한 경우이 페이지를 보여 줍니다. 타이머를 현재 실행 되 고 15 초 마다 표시 된 제품 정보를 업데이트 합니다. 그림 12 일시 중지 단추 클릭 후 화면을 보여 줍니다. 일시 중지 단추를 클릭 합니다. 타이머를 중지 하 고 단추의 텍스트를 "Resume"를 업데이트 합니다. 제품 정보는 새로 고침 (되며 계속 15 초 마다 새로 고침) 사용자가 다시 시작 되 면 합니다.


[![타이머 컨트롤을 중지 하려면 일시 중지 단추를 클릭 합니다.](master-pages-and-asp-net-ajax-cs/_static/image32.png)](master-pages-and-asp-net-ajax-cs/_static/image31.png)

**그림 11**합니다: 타이머 컨트롤을 중지 하려면 일시 중지 단추를 클릭 ([큰 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image33.png))


[![타이머를 다시 시작 하려면 [계속] 단추를 클릭 합니다.](master-pages-and-asp-net-ajax-cs/_static/image35.png)](master-pages-and-asp-net-ajax-cs/_static/image34.png)

**그림 12**합니다: 타이머를 다시 시작 하려면 다시 시작 단추를 클릭 ([큰 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-cs/_static/image36.png))


## <a name="summary"></a>요약

ASP.NET AJAX 프레임 워크를 사용 하 여 AJAX 사용 웹 응용 프로그램을 구축 하는 경우 반드시 모든 AJAX 지원 웹 페이지에 ScriptManager 컨트롤을 포함 합니다. 이 프로세스를 용이 하 게 하려면 각 콘텐츠 페이지에 ScriptManager를 추가 하지 않고 마스터 페이지에 ScriptManager를 추가할 수 있습니다. 1 단계 2 단계에서 콘텐츠 페이지에 AJAX 기능을 구현 하는 동안 마스터 페이지에 ScriptManager를 추가 하는 방법에 설명 했습니다.

사용자 지정 스크립트를 스크립트 사용 웹 서비스에 대 한 참조를 추가 해야 하거나 사용자 지정된 인증, 권한 부여 또는 특정 콘텐츠 페이지에 프로필 서비스 콘텐츠 페이지 ScriptManagerProxy 컨트롤을 추가 하 고 다음을 구성 합니다 사용자 지정 수 있습니다. 단계 3을 ScriptManagerProxy 사용 하 여 특정 콘텐츠 페이지에 사용자 지정 JavaScript 파일을 등록 하는 방법을 검사 합니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET AJAX 프레임 워크](../../../../ajax/index.md)
- [ASP.NET AJAX 자습서](../aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax.md)
- [ASP.NET AJAX 비디오](../../../videos/aspnet-ajax/index.md)
- [Microsoft ASP.NET AJAX 사용 하 여 대화형 사용자 인터페이스 구성](http://aspnet.4guysfromrolla.com/articles/101007-1.aspx)
- [임의로 정렬 레코드 NEWID를 사용 하 여](http://www.sqlteam.com/article/using-newid-to-randomly-sort-records)
- [타이머 컨트롤 사용](http://aspnet.4guysfromrolla.com/articles/061808-1.aspx)

### <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 작성자의 여러 ASP/ASP.NET 서적과 4GuysFromRolla.com의 설립자 이며, 왔습니다 Microsoft 웹 기술을 1998 합니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 3.5 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)합니다. Scott에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com) 통하거나 저자의 블로그 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](interacting-with-the-content-page-from-the-master-page-cs.md)
> [다음](specifying-the-master-page-programmatically-cs.md)
