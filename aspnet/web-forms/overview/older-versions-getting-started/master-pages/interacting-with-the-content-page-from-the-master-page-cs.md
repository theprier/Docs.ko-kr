---
uid: web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-content-page-from-the-master-page-cs
title: "마스터 페이지 (C#)에서 콘텐츠 페이지와 상호 작용 | Microsoft Docs"
author: rick-anderson
description: "메서드 호출, 마스터 페이지의 코드에서 해당 콘텐츠 페이지 등 속성을 설정 하는 방법을 검사 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/11/2008
ms.topic: article
ms.assetid: 3282df5e-516c-4972-8666-313828b90fb5
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-content-page-from-the-master-page-cs
msc.type: authoredcontent
ms.openlocfilehash: 923d291d84a47e64b31d99bcb13cfe53e5806444
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="interacting-with-the-content-page-from-the-master-page-c"></a>마스터 페이지 (C#)에서 콘텐츠 페이지와 상호 작용
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_07_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_07_CS.pdf)

> 메서드 호출, 마스터 페이지의 코드에서 해당 콘텐츠 페이지 등 속성을 설정 하는 방법을 검사 합니다.


## <a name="introduction"></a>소개

이전 자습서 콘텐츠 페이지를 프로그래밍 방식으로 해당 마스터 페이지와 상호 작용 하는 방법을 검사 합니다. 제품 추가 하는 회수 마스터 페이지 5 개의 가장 최근에 나열 하는 GridView 컨트롤을 포함 하도록 업데이트 되었습니다. 그런 다음 사용자는 새 제품을 추가할 수 있는 콘텐츠 페이지를 만들었습니다. 새 제품에 추가 되 면 콘텐츠 페이지를 방금 추가 된 제품을 포함 하는 GridView를 새로 고치려면 마스터 페이지를 지시 하는 데 필요 합니다. 이 기능은 마스터 페이지를 새로 고친에 바인딩된 데이터가 GridView에는 공용 메서드를 추가 하 고 다음 콘텐츠 페이지에서 해당 메서드를 호출 하 여 작업을 수행 했습니다.

콘텐츠 및 마스터 페이지 상호 작용의 가장 일반적인 형태 콘텐츠 페이지에서 생성 됩니다. 그러나 동작에 현재 콘텐츠 페이지 rouse 마스터 페이지 수 및 마스터 페이지 콘텐츠 페이지에도 표시 되는 데이터를 수정 하는 데 사용할 수 있는 사용자 인터페이스 요소를 포함 하는 경우 이러한 기능이 필요할 수 있습니다. 모든 제품의 가격을 두 배로, 제품 정보는 GridView에 제어를 표시 하 고 단추를 포함 하는 마스터 페이지 컨트롤을 클릭할 때 콘텐츠 페이지를 검토 합니다. 이전 자습서의 예제와 같이 훨씬 GridView 이중 가격 새로운 가격 표시 되도록 단추를 클릭 한 후 새로 고칠 수 하지만이 시나리오에서 마스터 페이지 콘텐츠 페이지 동작으로 rouse 해야 하는 것입니다.

이 자습서에는 마스터 페이지 콘텐츠 페이지에 정의 된 기능을 호출 하는 방법을 탐색 합니다.

### <a name="instigating-programmatic-interaction-via-an-event-and-event-handlers"></a>시작 이벤트 및 이벤트 처리기를 통해 프로그래밍 방식 상호 작용

마스터 페이지에서 콘텐츠 페이지 기능을 호출 하는 방식은 그 보다 좀 더 어렵습니다. 콘텐츠 페이지 콘텐츠 페이지에서 프로그래밍 방식으로 상호 작용을 시작 하는 경우 단일 마스터 페이지에 있기 때문에 공용 메서드 및 속성 이란 우리의 처리에서 알고 있습니다. 그러나 마스터 페이지 콘텐츠 페이지 수를 각각 고유한 속성 및 메서드 집합이 있을 수 있습니다. 방법, 그런 다음 우리 코드를 작성할 수 말도 런타임이 될 때까지 어떤 콘텐츠 페이지 호출 될 때 콘텐츠 페이지에서 작업을 수행할 수 마스터 페이지의?

예: Button 컨트롤은 ASP.NET 웹 컨트롤을 고려 합니다. Button 컨트롤 모든 ASP.NET 페이지에 나타날 수 있으며 기준인 경고할 수 있습니다 페이지 클릭 했음을 메커니즘이 필요 합니다. 사용 하 여 이렇게 *이벤트*합니다. 단추 컨트롤에서 발생 특히 해당 `Click` 이벤트 단추를 포함 하는 ASP.NET 페이지를 통해 해당 알림을에 선택적으로 응답할 수; 클릭할 때는 *이벤트 처리기*합니다.

해당 콘텐츠 페이지에서 마스터 페이지 트리거 기능 있어야이 동일한 패턴을 사용할 수 있습니다.

1. 마스터 페이지에는 이벤트를 추가 합니다.
2. 마스터 페이지 콘텐츠 페이지와 통신 해야 할 때마다 이벤트를 발생 시킵니다. 예를 들어 마스터 페이지를 사용자 가격 두 배가 되었음을 콘텐츠 페이지를 경고 하는 경우 가격의 두 배로 직후 해당 이벤트가 발생 합니다.
3. 특정 작업을 수행 해야 하는 이러한 콘텐츠 페이지에서 이벤트 처리기를 만듭니다.

이 자습서의 나머지 부분이에서는이; 소개에 설명 된 예제를 구현 합니다. 즉, 데이터베이스의 제품을 나열 하는 콘텐츠 페이지와 단추를 포함 하는 마스터 페이지 가격을 두 배로 제어 합니다.

## <a name="step-1-displaying-products-in-a-content-page"></a>1 단계: 콘텐츠 페이지에서 제품 표시

첫 번째 순서의 비즈니스는 Northwind 데이터베이스에서 제품을 나열 하는 콘텐츠 페이지를 만드는 것입니다. (이전 자습서에서 Northwind 데이터베이스 프로젝트에 추가한 [ *콘텐츠 페이지의 마스터 페이지와 상호 작용*](interacting-with-the-master-page-from-the-content-page-cs.md).) 새 ASP.NET 페이지를 추가 하 여 시작 된 `~/Admin` 라는 폴더 `Products.aspx`에 바인딩할 되므로 `Site.master` 마스터 페이지. 그림 1에서는이 페이지는 웹 사이트에 추가 된 후 솔루션 탐색기를 보여 줍니다.


[![Admin 폴더를 새 ASP.NET 페이지를 추가 합니다.](interacting-with-the-content-page-from-the-master-page-cs/_static/image2.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image1.png)

**그림 01**: 새 ASP.NET 페이지를 추가 `Admin` 폴더 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-content-page-from-the-master-page-cs/_static/image3.png))


이전에 설명한 대로 [ *마스터 페이지의 제목, 메타 태그 및 기타 HTML 헤더를 지정 하* ](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) 라는 기본 페이지를 사용자 지정 클래스 만든 자습서 `BasePage` 없는 경우 페이지의 제목을 생성 하는 명시적으로 설정 합니다. 이동 하는 `Products.aspx` 페이지의 코드 숨김 클래스에서 파생 되는 및 `BasePage` (대신에서 `System.Web.UI.Page`).

마지막으로 업데이트는 `Web.sitemap` 파일을이 단원에 대 한 항목을 포함 합니다. 아래에 다음 태그를 추가 `<siteMapNode>` 마스터 페이지 상호 작용 단원으로 든 콘텐츠에 대 한:


[!code-xml[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample1.xml)]

이 추가 `<siteMapNode>` 요소 단원에서 반영 됩니다 (그림 5 참조)를 나열 합니다.

으로 돌아와서 `Products.aspx`합니다. 에 대 한 콘텐츠 컨트롤에 `MainContent`, GridView 컨트롤을 추가 하 고 이름을 `ProductsGrid`합니다. GridView를 명명 된 새 SqlDataSource 컨트롤을 바인딩할 `ProductsDataSource`합니다.


[![GridView 새 SqlDataSource 컨트롤 바인딩](interacting-with-the-content-page-from-the-master-page-cs/_static/image5.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image4.png)

**그림 02**: GridView 새 SqlDataSource 컨트롤을 바인딩할 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-content-page-from-the-master-page-cs/_static/image6.png))


Northwind 데이터베이스를 사용 하 여 마법사를 구성 합니다. 이전 자습서를 작동 한 경우 명명 된 연결 문자열을 이미 있어야 `NorthwindConnectionString` 에서 `Web.config`합니다. 그림 3에 나와 있는 것 처럼 드롭 다운 목록에서이 연결 문자열을 선택 합니다.


[![SqlDataSource Northwind 데이터베이스를 사용 하도록 구성](interacting-with-the-content-page-from-the-master-page-cs/_static/image8.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image7.png)

**그림 03**: SqlDataSource Northwind 데이터베이스를 사용 하도록 구성 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-content-page-from-the-master-page-cs/_static/image9.png))


그런 다음 데이터 소스 컨트롤의 지정 `SELECT` 반환 하 고 드롭다운 목록에서 Products 테이블을 선택 하 여 문을 `ProductName` 및 `UnitPrice` 열 (그림 4 참조). 다음을 클릭 하 고 데이터 소스 구성 마법사를 완료 한 다음 끝냅니다.


[![ProductName 및 UnitPrice 필드 Products 테이블에서 반환](interacting-with-the-content-page-from-the-master-page-cs/_static/image11.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image10.png)

**그림 04**: 반환 된 `ProductName` 및 `UnitPrice` 에서 필드는 `Products` 테이블 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-content-page-from-the-master-page-cs/_static/image12.png))


그을 마쳤습니다. 마법사를 완료 한 후 Visual Studio SqlDataSource 컨트롤에 의해 반환 되는 두 개의 필드를 미러링 하는 GridView에 두 개의 BoundFields를 추가 합니다. GridView 및 SqlDataSource 컨트롤 태그는 다음과 같습니다. 그림 5에서 브라우저를 통해 볼 때 결과 보여 줍니다.


[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample2.aspx)]


[![각 제품의 가격 GridView에 나열 됩니다.](interacting-with-the-content-page-from-the-master-page-cs/_static/image14.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image13.png)

**그림 05**: 각 제품의 가격 GridView에 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-content-page-from-the-master-page-cs/_static/image15.png))


> [!NOTE]
> GridView의 모양을 정리 자유롭게 합니다. 몇 가지 제안 사항에는 서식을 통화로 표시 된 UnitPrice 값 및 배경색 및 글꼴을 사용 하 여 눈금의 모양 향상을 위해 포함 됩니다. 표시 및 ASP.NET에는 데이터 서식 지정에 대 한 자세한 내용은 참조 내 [데이터 자습서 시리즈 작업](../../data-access/index.md)합니다.


## <a name="step-2-adding-a-double-prices-button-to-the-master-page"></a>2 단계: 마스터 페이지에 두 번 가격 단추 추가

다음 작업이 추가할 단추 웹 컨트롤을 마스터 페이지를 클릭 하면 발생 합니다. 데이터베이스의 모든 제품의 가격 double입니다. 열기는 `Site.master` 마스터 페이지 및 아래에 배치 하는 디자이너에 끌어 도구 상자에서 단추를 끌어는 `RecentProductsDataSource` SqlDataSource 컨트롤 이전 자습서에서 추가 되었습니다. 단추의 설정 `ID` 속성을 `DoublePrice` 및 해당 `Text` 속성을 "Double 제품 가격"입니다.

SqlDataSource 컨트롤 이름을 지정 하 고 마스터 페이지 다음에 추가 `DoublePricesDataSource`합니다. 이 SqlDataSource에서 실행 하는 데 사용 됩니다는 `UPDATE` 모든 가격을 두는 문입니다. 구체적으로 설정 해야 해당 `ConnectionString` 및 `UpdateCommand` 속성을 적절 한 연결 문자열 및 `UPDATE` 문. 이 SqlDataSource 컨트롤을 호출 해야 하는 다음 `Update` 메서드 때는 `DoublePrice` 단추를 클릭 합니다. 설정 하는 `ConnectionString` 및 `UpdateCommand` 속성, SqlDataSource 컨트롤을 선택 하 고 다음 속성 창으로 이동 합니다. `ConnectionString` 속성 목록에 이미 저장 된 연결 문자열 `Web.config` ; 드롭 다운 목록에서 선택 된 `NorthwindConnectionString` 그림 6에 나와 있는 것 처럼 옵션입니다.


[![SqlDataSource는 위해를 사용 하도록 구성](interacting-with-the-content-page-from-the-master-page-cs/_static/image17.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image16.png)

**그림 06**: SqlDataSource를 사용 하 여 구성 된 `NorthwindConnectionString` ([전체 크기 이미지를 보려면 클릭](interacting-with-the-content-page-from-the-master-page-cs/_static/image18.png))


설정 하 여 `UpdateCommand` 속성을 속성 창에서 UpdateQuery 옵션을 찾습니다. 이 속성의 옵션을 선택 하면; 줄임표 단추가 표시 됩니다. 그림 7에 표시 된 명령 및 매개 변수 편집기 대화 상자를 표시 하려면이 단추를 클릭 합니다. 다음 명령을 입력 `UPDATE` 문을 대화 상자에 붙여넣습니다.


[!code-sql[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample3.sql)]

를 실행 하면이 문은 배로 `UnitPrice` 의 각 레코드에 대 한 값은 `Products` 테이블입니다.


[![SqlDataSource의 UpdateCommand 속성 설정](interacting-with-the-content-page-from-the-master-page-cs/_static/image20.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image19.png)

**그림 07**: 설정 SqlDataSource `UpdateCommand` 속성 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-content-page-from-the-master-page-cs/_static/image21.png))


이러한 속성을 설정한 다음 단추 및 SqlDataSource 컨트롤의 선언적 태그 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample4.aspx)]

호출 하는 것은 유지 하는 모든 해당 `Update` 메서드 때는 `DoublePrice` 단추를 클릭 합니다. 만들기는 `Click` 에 대 한 이벤트 처리기는 `DoublePrice` 단추 다음 코드를 추가 하 고 있습니다.


[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample5.cs)]

이 기능을 테스트 하려면 방문는 `~/Admin/Products.aspx` 페이지 1 단계에서에서 만든 하 고 "Double 제품 가격" 단추를 클릭 합니다. 포스트백을 발생 하 고 실행 단추를 클릭 하 여 `DoublePrice` 단추의 `Click` 이벤트 처리기를 모든 제품의 가격을 두 배로 합니다. 페이지를 다시 렌더링 한 다음 및 태그를 반환 하 고 다시 브라우저에 표시 합니다. 그러나 GridView 콘텐츠 페이지에서 단추가 클릭 되었습니다 "Double 제품 가격" 하기 전에 동일한 가격 나열 됩니다. GridView에 처음 로드 된 데이터에 뷰 상태에 저장 하지 않으므로 다시 로드 되지 않습니다 포스트백에서 별도로 지시 하지 않는 한 상태로 때문입니다. 다른 페이지를 방문 하 고으로 돌아 경우는 `~/Admin/Products.aspx` 페이지 업데이트 된 가격이 표시 됩니다.

## <a name="step-3-raising-an-event-when-the-prices-are-doubled"></a>3 단계: 중복 발생 한 이벤트 때 the 가격

때문에에 GridView의 `~/Admin/Products.aspx` 페이지 가격 더블링 즉시 반영 하지 않습니다, 사용자는 "Double 제품 가격" 단추를 클릭 하지 않은 또는 작동 하지 않는 당연히 생각할 수 있습니다. 해 볼 수 단추를 클릭 하면 시간, 가격을 나중에 다시 두 배로 몇 가지 더 합니다. 모눈에 콘텐츠 있어야이 문제를 해결 페이지 새로운 가격 바로 표시 두 배가 됩니다.

사용자가을 클릭할 때마다 마스터 페이지에서 이벤트를 발생 해야이 자습서의 앞부분에서 설명 했 듯이 `DoublePrice` 단추입니다. 이벤트는 흥미로운 문제가 발생 한 다른 클래스 (이벤트 구독자)의 집합을 다른 알림 하는 방법 하나의 클래스 (이벤트 게시자)입니다. 이 예제에서는 마스터 페이지는 이벤트 게시자; 이러한 콘텐츠 페이지는 경우에 대 한 고려 하는 `DoublePrice` 단추를 클릭 하면 구독자는 합니다.

클래스를 만들어 이벤트 구독는 *이벤트 처리기*, 발생 하는 이벤트에 대 한 응답으로 실행 되는 방법인 합니다. 가 정의 하 여 발생 하는 이벤트를 정의 하는 게시자는 *이벤트 대리자*합니다. 이벤트 대리자 이벤트 처리기에 동의 해야 입력된 매개 변수를 지정 합니다. .NET Framework에서 이벤트 대리자 반환 하지 않는 모든 값 및 두 개의 입력된 매개 변수를 허용 합니다.

- `Object`, 이벤트 소스를 식별 하 고
- 파생 된 클래스`System.EventArgs`

이벤트 처리기에 전달 된 두 번째 매개 변수는 이벤트에 대 한 추가 정보를 포함할 수 있습니다. 기본 `EventArgs` 클래스 정보에 따라 통과 하지 못하면, 다양 한 확장 하는 클래스를 포함 하는.NET Framework `EventArgs` 추가 속성을 포함 합니다. 예를 들어 한 `CommandEventArgs` 인스턴스에 응답 하는 이벤트 처리기로 전달 되는 `Command` 이벤트, 두 정보 속성을 포함 하 고: `CommandArgument` 및 `CommandName`합니다.

> [!NOTE]
> 만드는 방법에 대 한 자세한 내용은 시키고 이벤트를 처리 참조 [이벤트 및 대리자](https://msdn.microsoft.com/en-us/library/17sde2xt.aspx) 및 [영어로 간단한 이벤트 대리자](http://www.codeproject.com/KB/cs/eventdelegates.aspx)합니다.


정의 하는 이벤트에는 다음 구문을 사용 합니다.


[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample6.cs)]

하기 때문에 경고 콘텐츠 페이지는 사용자가 클릭 하 여 `DoublePrice` 단추 및 기타 추가 정보에 따라 통과 필요가 없다면, 이벤트 대리자를 사용할 수 있습니다 `EventHandler`, 두 번째 피연산자로으로 허용 하는 이벤트 처리기를 정의 하는 매개 변수 형식의 개체로 `System.EventArgs`합니다. 마스터 페이지에서 이벤트를 만들려면, 마스터 페이지의 코드 숨김 클래스에 다음 코드 줄을 추가 합니다.


[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample7.cs)]

명명 된 마스터 페이지에는 공용 이벤트를 추가 하는 위의 코드 `PricesDoubled`합니다. 이제 가격의 두 배로 이후이 이벤트가 발생 해야 합니다. 발생 시키는 이벤트에는 다음 구문을 사용 합니다.


[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample8.cs)]

여기서 *보낸 사람* 및 *eventArgs* 는 구독자의 이벤트 처리기에 전달 하려는 값입니다.

업데이트는 `DoublePrice` `Click` 이벤트 처리기를 다음 코드로:


[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample9.cs)]

이전 처럼는 `Click` 호출 하 여 시작 된 이벤트 처리기는 `DoublePricesDataSource` SqlDataSource 컨트롤의 `Update` 모든 제품의 가격을 두 배로 메서드. 다음 이벤트 처리기에 대 한 두 개의 추가 있습니다. 첫째는 `RecentProducts` GridView의 데이터가 새로 고쳐집니다. 이 GridView 이전 자습서에서 마스터 페이지에 추가 된 하 고 가장 최근에 추가한 다섯 개의 제품을 표시 합니다. 이 표를 새로 고치려면이 이러한 5 개 제품에 대 한 바로 이중 가격 표시 되도록 해야 합니다. 그런 다음,는 `PricesDoubled` 이벤트가 발생 합니다. 마스터 페이지 자체에 대 한 참조 (`this`) 이벤트 처리기 이벤트 소스와 빈으로 보내집니다 `EventArgs` 개체는 이벤트 인수로 전송 됩니다.

## <a name="step-4-handling-the-event-in-the-content-page"></a>4 단계: 콘텐츠 페이지에서 이벤트를 처리합니다.

마스터 페이지의 발생이 시점에서 해당 `PricesDoubled` 이벤트 때마다는 `DoublePrice` 단추 컨트롤을 클릭 합니다. 그러나이 절반에 불과합니다-구독자에서 이벤트를 처리 해야 합니다. 이 두 단계: 이벤트 처리기를 만들고 이벤트 처리기는 이벤트가 발생할 때 실행 되도록 이벤트 작성 코드를 추가 합니다.

이벤트 처리기를 만들어 시작 `Master_PricesDoubled`합니다. 정의 방법으로 인해는 `PricesDoubled` 마스터 페이지에서 이벤트의 이벤트 처리기의 두 입력된 매개 변수 형식 이어야 합니다 `Object` 및 `EventArgs`각각. 이벤트 처리기 호출에는 `ProductsGrid` GridView의 `DataBind` 메서드 표에 데이터를 다시 바인딩해야 합니다.


[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample10.cs)]

이벤트 처리기에 대 한 코드 작성을 완료 하지만 아직를 이유임 마스터 페이지의 연결 `PricesDoubled` 이벤트를이 이벤트 처리기입니다. 다음 구문을 통해 이벤트 처리기에 이벤트를 연결 하는 구독자.


[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample11.cs)]

*게시자* 이벤트에서 제공 하는 개체에 대 한 참조 *eventName*, 및 *methodName* 해당 하는 서명이 있는 구독자에 정의 된 이벤트 처리기의 이름 에 *eventDelegate*합니다. 즉, 이벤트 대리자 인지 `EventHandler`, 다음 *methodName* 값을 반환 하지 않는 고 형식의 매개 변수 2 개의 입력을 수락 하는 구독자에 있는 메서드의 이름 이어야 합니다 `Object` 및 `EventArgs`, 각각.

이 이벤트 배선 코드 페이지 방문을 첫 번째 및 후속 포스트백에서 실행 해야 하 고 시점 이벤트를 발생 시킬 때 앞에 오는 페이지 수명 주기에서 발생 해야 합니다. 이벤트 작성 코드를 추가 하는 좋은 시간은 페이지 수명 주기의 초기 단계에서 생성 되는 PreInit 단계입니다.

열기 `~/Admin/Products.aspx` 만듭니다는 `Page_PreInit` 이벤트 처리기.


[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample12.cs)]

이 작성 코드를 완료 하기 위해 콘텐츠 페이지에서 마스터 페이지에 프로그래밍 방식으로 참조를 해야 합니다. 이전 자습서에서 설명한 대로,이 작업을 수행 하는 두 가지 있습니다.

- 자유로운 형식의 캐스팅 하 여 `Page.Master` 속성을 적절 한 마스터 페이지 형식 또는
- 추가 하 여 한 `@MasterType` 지시어는 `.aspx` 페이지 및 사용 하 여 강력한 형식의 `Master` 속성입니다.

후자의 방법을 사용할 경우 사용 합니다. 다음 추가 `@MasterType` 페이지의 선언적 태그의 맨 위에 지시문:


[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample13.aspx)]

다음 이벤트 배선을 코드를 추가 `Page_PreInit` 이벤트 처리기.


[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample14.cs)]

이 코드 위치에서 있는 콘텐츠 페이지에 GridView를 새로 고칠 때마다는 `DoublePrice` 단추를 클릭 합니다.

그림 8과 9이이 동작을 보여 줍니다. 그림 8 처음 방문 페이지를 보여줍니다. 값 모두에 가격 참고는 `RecentProducts` (마스터 페이지의 왼쪽된 열)에 GridView 및 `ProductsGrid` (콘텐츠 페이지)에서 GridView입니다. 그림 9에서는 직후 화면 동일한는 `DoublePrice` 단추를 클릭 합니다. 볼 수 있듯이 새로운 가격 두 Gridview에 즉시 반영 됩니다.


[![초기 가격 값](interacting-with-the-content-page-from-the-master-page-cs/_static/image23.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image22.png)

**그림 08**: 초기 가격 값의 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-content-page-from-the-master-page-cs/_static/image24.png))


[![Just-Doubled 가격은 Gridview에 표시 됩니다.](interacting-with-the-content-page-from-the-master-page-cs/_static/image26.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image25.png)

**그림 09**: The Just-Doubled 가격은 Gridview에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-content-page-from-the-master-page-cs/_static/image27.png))


## <a name="summary"></a>요약

이상적으로 마스터 페이지 및 콘텐츠 페이지는 서로 완전히 분리 하 고 필요 없는 수준의 상호 작용 합니다. 그러나 마스터 페이지 또는 마스터 페이지 또는 콘텐츠 페이지에서 수정할 수 있는 데이터를 표시 하는 콘텐츠 페이지를 설정한 경우 할 수 있습니다에 콘텐츠 페이지 (또는 반대로 a) 경고 마스터 페이지를 디스플레이 업데이트할 수 있도록 데이터를 수정 하는 경우. 콘텐츠 페이지의 마스터 페이지;와 프로그래밍 방식으로 상호 작용 하는 방법을 살펴보았습니다 이전 자습서 이 자습서에서는 마스터 페이지 시작 상호 작용 하는 방법을에서 찾았습니다.

콘텐츠 및 마스터 페이지 간의 프로그래밍 방식으로 상호 작용 콘텐츠 또는 마스터 페이지에서 가져온 것일 수 있습니다, 하는 동안 사용 되는 상호 작용 패턴의 발생 위치에 따라 달라 집니다. 차이가 때문을 콘텐츠 페이지에는 단일 마스터 페이지에 있지만 마스터 페이지 콘텐츠 페이지 수를 가질 수 있습니다. 것이 아니라 콘텐츠 페이지와 직접 상호 작용 하는 마스터 페이지, 마스터 페이지에 몇 가지 작업이 수행 되어 신호를 보내는 이벤트를 발생 하는 것이 좋습니다. 이러한 콘텐츠 페이지 작업을 고려 하는 이벤트 처리기를 만들 수 있습니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Asp.net에서 데이터 액세스 및 업데이트](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [이벤트 및 대리자](https://msdn.microsoft.com/en-us/library/17sde2xt.aspx)
- [콘텐츠 및 마스터 페이지 사이의 정보 전달](http://aspnet.4guysfromrolla.com/articles/013107-1.aspx)
- [ASP.NET 자습서에서 데이터 작업](../../data-access/index.md)

### <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 작성자 여러 ASP/ASP.NET 설명서와 4GuysFromRolla.com의 창립자의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 3.5 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)합니다. Scott에 도달할 수 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com) 또는에서 그의 블로그 통해 [http://ScottOnWriting.NET](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Suchi Banerjee 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](interacting-with-the-master-page-from-the-content-page-cs.md)
[다음](master-pages-and-asp-net-ajax-cs.md)
