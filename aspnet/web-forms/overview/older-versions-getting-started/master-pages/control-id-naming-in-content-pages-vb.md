---
uid: web-forms/overview/older-versions-getting-started/master-pages/control-id-naming-in-content-pages-vb
title: 콘텐츠 페이지 (VB)에서 ID 명명 제어 | Microsoft Docs
author: rick-anderson
description: Contentplaceholder 명명 컨테이너 역할을 하 고 따라서 (FindConrol)를 통해 어려운 컨트롤을 사용 하 여 프로그래밍 방식으로 작업을 확인 하는 방법을 보여 줍니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2008
ms.topic: article
ms.assetid: dbb024a6-f043-4fc5-ad66-56556711875b
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/control-id-naming-in-content-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 1b922fb230169824659222da0b9504ec38c36d8a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37387714"
---
<a name="control-id-naming-in-content-pages-vb"></a>콘텐츠 페이지 (VB)의 이름을 지정 하는 컨트롤 ID
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_05_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_05_VB.pdf)

> Contentplaceholder 명명 컨테이너 역할을 하 고 따라서 (FindConrol)를 통해 어려운 컨트롤을 사용 하 여 프로그래밍 방식으로 작업을 확인 하는 방법을 보여 줍니다. 이 문제와 해결 방법에 살펴봅니다. 결과 ClientID 값을 프로그래밍 방식으로 액세스 하는 방법을 설명 합니다.


## <a name="introduction"></a>소개

모든 ASP.NET 서버 컨트롤에 포함는 `ID` 속성을 고유 하 게 컨트롤을 식별 하는 컨트롤은 프로그래밍 방식으로 액세스할 코드 숨김 클래스에서에서는 사용 합니다. 마찬가지로, HTML 문서에서 요소를 포함할 수 있습니다는 `id` 요소를 고유 하 게 식별 하는 특성; 이러한 `id` 값은 보통 특정 HTML 요소를 프로그래밍 방식으로 참조 하려면 클라이언트 쪽 스크립트에 사용 됩니다. 이 점을 고려 하 고 가정할 수도 있습니다는 ASP.NET 서버 컨트롤을 HTML로 렌더링 될 때 해당 `ID` 값으로 사용 되는 `id` 렌더링 된 HTML 요소의 값입니다. 이 아니므로 반드시 경우 특정 상황에서 하나의 단일 제어 `ID` 렌더링 되는 태그에 값이 여러 번 표시 될 수 있습니다. GridView 컨트롤 레이블 웹 컨트롤을 사용 하 여 templatefield로 포함 하는 것이 좋습니다는 `ID` 의 값 `ProductName`합니다. 런타임에 해당 데이터 원본에 GridView 바인딩되면이 레이블은 모든 GridView 행에 대해 한 번 반복 됩니다. 각 렌더링 레이블 요구 고유한 `id` 값입니다.

이러한 시나리오를 처리 하려면 ASP.NET에 특정 컨트롤을 컨테이너 이름으로 표시 될 수 있습니다. 명명 컨테이너 역할을 새 `ID` 네임 스페이스입니다. 명명 컨테이너 내에 나타나는 모든 서버 컨트롤에는 해당 렌더링 `id` 접두사가 붙은 `ID` 명명 컨테이너 컨트롤의 합니다. 예를 들어 합니다 `GridView` 고 `GridViewRow` 클래스는 모두 명명 컨테이너입니다. 따라서 레이블 컨트롤을 사용 하 여 GridView templatefield로에 정의 된 `ID` `ProductName` 렌더링 된 같습니다 `id` 값 `GridViewID_GridViewRowID_ProductName`합니다. 때문에 *GridViewRowID* 결과 각 GridView 행에 대해 고유한 `id` 값은 고유 합니다.

> [!NOTE]
> 합니다 [ `INamingContainer` 인터페이스](https://msdn.microsoft.com/library/system.web.ui.inamingcontainer.aspx) 명명 컨테이너 특정 ASP.NET 서버 컨트롤을 작동 해야 하는지 나타내는 데 사용 됩니다. `INamingContainer` 인터페이스 서버 컨트롤을 구현 해야 하는 메서드 나와 있지 않습니다; 대신 한 표식으로 사용 됩니다. 렌더링 된 태그를 생성에서 컨트롤을이 인터페이스를 구현 하는 경우 다음 ASP.NET 엔진 자동으로 붙입니다 해당 `ID` 값을 해당 하위 항목의 렌더링 `id` 특성 값입니다. 이 프로세스는 2 단계에서에서 자세히 설명 합니다.


명명 컨테이너 뿐만 아니라는 렌더링 된 변경 `id` 특성 값, 있지만 어떻게 컨트롤 참조 될 수 있습니다 프로그래밍 방식으로 ASP.NET 페이지의 코드 숨김 클래스에서 영향을 줍니다. `FindControl("controlID")` 메서드는 일반적으로 웹 컨트롤을 프로그래밍 방식으로 참조 하는 데 사용 됩니다. 그러나 `FindControl` 명명 컨테이너를 통해 침투 하지 않습니다. 직접 사용할 수 없습니다 결과적으로 `Page.FindControl` GridView 또는 다른 명명 컨테이너 내의 컨트롤을 참조 하는 방법입니다.

정답 있는 수에 따라 마스터 페이지 및 ContentPlaceHolders 둘 다로 구현 됩니다 명명 컨테이너. 어떻게 마스터 페이지에 영향을 HTML 요소가이 자습서에서 살펴봅니다 `id` 프로그래밍 방식으로 사용 하 여 콘텐츠 페이지 내에서 웹 컨트롤을 참조 하는 방법 및 값 `FindControl`합니다.

## <a name="step-1-adding-a-new-aspnet-page"></a>1 단계: 새 ASP.NET 페이지를 추가합니다.

이 자습서에서 설명한 개념을 보여 주기 위해 웹 사이트를 새 ASP.NET 페이지를 추가 하겠습니다. 라는 새 콘텐츠 페이지를 만듭니다 `IDIssues.aspx` 루트 폴더에서에 바인딩하지는 `Site.master` 마스터 페이지입니다.


![콘텐츠 페이지 IDIssues.aspx 루트 폴더에 추가](control-id-naming-in-content-pages-vb/_static/image1.png)

**그림 01**: 콘텐츠 페이지 추가 `IDIssues.aspx` 루트 폴더에


Visual Studio는 자동으로 각 마스터 페이지의 네 가지 ContentPlaceHolders에 대 한 콘텐츠 컨트롤을 만듭니다. 설명한 것 처럼 합니다 [ *여러 ContentPlaceHolders 및 기본 콘텐츠* ](multiple-contentplaceholders-and-default-content-vb.md) 자습서, 마스터 페이지의 기본 ContentPlaceHolder 콘텐츠 대신 내보내집니다 콘텐츠 컨트롤이 없는 경우. 때문에 합니다 `QuickLoginUI` 하 고 `LeftColumnContent` ContentPlaceHolders이이 페이지에 대 한 적합 한 기본 태그를 포함, 계속 해 서 해당 제거에서 콘텐츠 컨트롤 `IDIssues.aspx`합니다. 이 시점에서 콘텐츠 페이지의 선언적 태그는 다음과 같아야 합니다.


[!code-aspx[Main](control-id-naming-in-content-pages-vb/samples/sample1.aspx)]

에 [ *마스터 페이지에서 제목, 메타 태그 및 기타 HTML 헤더 지정* ](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md) 자습서는 사용자 지정 기본 페이지 클래스를 만들었습니다 (`BasePage`) 자동으로 구성 하는 페이지 제목 경우 명시적으로 설정 합니다. 에 대 한 합니다 `IDIssues.aspx` 이 기능을 사용 하 여 페이지에서 페이지의 코드 숨김 클래스에서 파생 되어야 합니다 `BasePage` 클래스 (대신 `System.Web.UI.Page`). 다음과 같이 표시 되도록 코드 숨김 클래스의 정의 수정 합니다.


[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample2.vb)]

마지막으로 업데이트 된 `Web.sitemap` 새이 단원에 대 한 항목을 포함 하는 파일입니다. 추가 `<siteMapNode>` 요소 집합과 해당 `title` 하 고 `url` 특성을 "컨트롤 ID 이름 지정 문제" 및 `~/IDIssues.aspx`각각. 이 추가 마치면 프로그램 `Web.sitemap` 파일의 태그는 다음과 유사 합니다.


[!code-xml[Main](control-id-naming-in-content-pages-vb/samples/sample3.xml)]

그림 2에서 볼 수 있듯이에서 새 사이트 맵 항목 `Web.sitemap` 왼쪽된 열에서 단원 섹션에 즉시 반영 됩니다.


![단원 섹션에는 이제 링크를 포함 &quot;명명 문제 ID를 제어 합니다.&quot;](control-id-naming-in-content-pages-vb/_static/image2.png)

**그림 02**: 단원 섹션에는 이제 "컨트롤 ID 명명 문제"에 대 한 링크 포함


## <a name="step-2-examining-the-renderedidchanges"></a>2 단계: 렌더링 된 검사`ID`변경

ASP.NET 수정 사항을 더 잘 이해 하려면 엔진에 게는 렌더링 된 `id` 서버의 값을 제어, 몇 가지 웹 컨트롤을 추가 해 보겠습니다는 `IDIssues.aspx` 페이지 후 렌더링 되는 브라우저에 보내지는 태그를 확인 합니다. 텍스트에 특히, 형식 "나이 입력 하세요:" 텍스트 웹 컨트롤 뒤에 있습니다. 더 아래로 페이지에서 추가 단추 웹 컨트롤 및 레이블 웹 컨트롤입니다. 텍스트 상자의 설정 `ID` 하 고 `Columns` 속성을 `Age` 및 3, 각각. 설정 단추 `Text` 하 고 `ID` 속성을 "제출" 및 `SubmitButton`합니다. 레이블의 지웁니다 `Text` 속성 집합과 해당 `ID` 에 `Results`입니다.

이 시점에서 콘텐츠 컨트롤의 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](control-id-naming-in-content-pages-vb/samples/sample4.aspx)]

그림 3에서는 Visual Studio의 디자이너를 통해 볼 때 페이지를 보여 줍니다.


[![페이지에는 세 개의 웹 컨트롤이 포함 됩니다:는 텍스트, 단추 및 레이블](control-id-naming-in-content-pages-vb/_static/image4.png)](control-id-naming-in-content-pages-vb/_static/image3.png)

**그림 03**: The 페이지를 포함 세 웹 컨트롤: 텍스트, 단추 및 레이블 ([큰 이미지를 보려면 클릭](control-id-naming-in-content-pages-vb/_static/image5.png))


브라우저를 통해 페이지를 방문 하 고의 HTML 소스를 봅니다. 아래 태그로 `id` 텍스트 상자, 단추 및 레이블을 웹 컨트롤에 대 한 HTML 요소 값의 조합인 합니다 `ID` 웹 컨트롤의 값 및 `ID` 페이지에서 명명 컨테이너의 값입니다.


[!code-html[Main](control-id-naming-in-content-pages-vb/samples/sample5.html)]

이 자습서의 앞부분에서 설명 했 듯이 마스터 페이지와 해당 ContentPlaceHolders 명명 컨테이너를 제공 합니다. 결과적으로 모두 참여는 렌더링 된 `ID` 해당 중첩 된 컨트롤의 값입니다. 텍스트 상자의 걸릴 `id` 특성을 예를 들어: `ctl00_MainContent_Age`합니다. 이전에 설명한 대로 TextBox 컨트롤의 `ID` 값이 `Age`합니다. 이 각각의 ContentPlaceHolder 컨트롤로 접두사로 `ID` 값을 `MainContent`입니다. 이 값이 마스터 페이지에 접두사로 게다가 `ID` 값을 `ctl00`입니다. 최종 결과 `id` 특성 값으로 이루어진는 `ID` 마스터 페이지, ContentPlaceHolder 컨트롤을 자체 입력란의 값입니다.

그림 4에서는이 동작을 보여 줍니다. 렌더링 된 결정할 `id` 의 `Age` 텍스트 상자를 시작 합니다 `ID` TextBox 컨트롤의 값 `Age`합니다. 다음으로, 컨트롤 계층 구조로으로 작동 합니다. 각 명명 컨테이너 (복숭아색 색을 사용 하 여 해당 노드)에서 현재 렌더링 접두사 `id` 의 명명 컨테이너를 사용 하 여 `id`입니다.


![렌더링 된 id 특성은 기반에서 ID 값의 명명 컨테이너](control-id-naming-in-content-pages-vb/_static/image6.png)

**그림 04**: The 렌더링 `id` 특성에 기반을 `ID` 명명 컨테이너의 값


> [!NOTE]
> 앞에서 설명한 것 처럼를 `ctl00` 부분 렌더링 된 `id` 특성을 `ID` 마스터 페이지의 값을 궁금할 수 있습니다 어떻게이 `ID` 값에 대 한 제공. 지정 하지 않았기 하 아무 곳 이나 마스터 페이지나 콘텐츠 페이지에 있습니다. 대부분의 서버 컨트롤과 ASP.NET 페이지에서 페이지의 선언적 태그를 통해 명시적으로 추가 됩니다. 합니다 `MainContent` 각각의 ContentPlaceHolder 컨트롤로의 태그에 명시적으로 지정 된 `Site.master`; `Age` 텍스트 상자에서 정의한 `IDIssues.aspx`의 태그입니다. 지정할 수 있습니다는 `ID` 이러한 종류의 선언적 구문 또는 속성 창을 통해 컨트롤에 대 한 값입니다. 마스터 페이지 자체와 같은 다른 컨트롤을 선언적 태그에 정의 되지 않습니다. 따라서 해당 `ID` 값을 자동으로 생성 해야 합니다. ASP.NET 엔진 집합을 `ID` Id를 가진 명시적으로 설정 되지 않은 해당 컨트롤에 대 한 런타임 시 값입니다. 명명 패턴을 사용 하 여 `ctlXX`, 여기서 *XX* 정수 값인 순차적으로 증가 합니다.


마스터 페이지 명명 컨테이너 역할을 하기 때문에 마스터 페이지에 정의 된 웹 컨트롤 수도 있는 변경 렌더링 `id` 특성 값입니다. 예를 들어 합니다 `DisplayDate` 에서 마스터 페이지에 추가한 레이블을 합니다 [ *마스터 페이지를 사용 하 여 사이트 전체 레이아웃 만들기* ](creating-a-site-wide-layout-using-master-pages-vb.md) 자습서에 태그를 렌더링 하는 다음과 같은:


[!code-html[Main](control-id-naming-in-content-pages-vb/samples/sample6.html)]

유의 합니다 `id` 모두 마스터 페이지의 포함 `ID` 값 (`ctl00`) 및 `ID` Label 웹 컨트롤의 값 (`DateDisplay`).

## <a name="step-3-programmatically-referencing-web-controls-viafindcontrol"></a>3 단계를 통해 웹 컨트롤을 프로그래밍 방식으로 참조`FindControl`

모든 ASP.NET 서버 컨트롤에는 `FindControl("controlID")` 이라는 이름의 컨트롤에 대 한 컨트롤의 하위 항목을 검색 하는 메서드 *controlID*합니다. 이러한 컨트롤이 없으면 반환 됩니다. 일치 하는 컨트롤이 없으면 `FindControl` 반환 `Nothing`합니다.

`FindControl` 위치 액세스를 제어 해야 하지만에 대 한 직접 참조가 없는 시나리오에서 유용 합니다. 예를 들어 GridView와 같은 웹 컨트롤을 데이터로 작업할 때 GridView의 필드 내에서 컨트롤의 선언적 구문에서 한 번 정의 되지만 런타임 시 컨트롤의 인스턴스가 각 GridView 행에 대해 만들어집니다. 결과적으로 런타임에 생성 된 컨트롤 존재 하지만 직접 참조를 코드 숨김 클래스에서 사용할 수 없습니다. 결과적으로 사용 해야 `FindControl` GridView의 필드 내에서 특정 컨트롤을 사용 하 여 프로그래밍 방식으로 작동 합니다. (사용 하 여 대 한 자세한 내용은 `FindControl` 데이터 웹 컨트롤의 템플릿 내에서 컨트롤에 액세스 하려면 참조 [데이터를 기반으로 사용자 지정 서식 지정](../../data-access/custom-formatting/custom-formatting-based-upon-data-vb.md).) 동적으로 웹 컨트롤에 Web Form을 추가할 때 이와 동일한 시나리오에서 발생, 항목에서 설명한 [동적 데이터 입력 사용자 인터페이스 만들기](https://msdn.microsoft.com/library/aa479330.aspx)합니다.

에서는 사용 하는 `FindControl` 콘텐츠 페이지 내에서 컨트롤을 검색 하는 방법에 대 한 이벤트 처리기를 만들고는 `SubmitButton`의 `Click` 이벤트. 이벤트 처리기에서 프로그래밍 방식으로 참조 하는 다음 코드를 추가 합니다 `Age` 텍스트 상자에 붙여넣습니다 및 `Results` 레이블을 사용 하 여는 `FindControl` 메서드 다음에 메시지를 표시 하 고 `Results` 사용자의 입력을 기반으로 합니다.

> [!NOTE]
> 물론 우리가 사용할 필요가 없는 `FindControl` 이 예제에 대 한 레이블 및 텍스트 상자 컨트롤을 참조 합니다. 통해 직접 참조 수 해당 `ID` 속성 값입니다. 사용 하 여 `FindControl` 를 사용 하는 경우를 보여 주기 위해 여기서 `FindControl` 콘텐츠 페이지 로부터 합니다.


[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample7.vb)]

구문을 호출 하는 데 사용 하는 동안 합니다 `FindControl` 메서드를 처음 두 줄에서 약간 다릅니다. `SubmitButton_Click`, 기능적으로 동일 합니다. 모든 ASP.NET 서버 컨트롤을 포함 하는 재현 율을 `FindControl` 메서드. 여기에 `Page` 클래스는 모든 ASP.NET에서 코드 숨김 클래스에서 파생 되어야 합니다. 따라서 호출 `FindControl("controlID")` 호출 하는 것과 같습니다 `Page.FindControl("controlID")`를 재정의 하지 않은 것으로 가정 합니다 `FindControl` 코드 숨김 클래스 또는 사용자 지정 기본 클래스 메서드.

이 코드를 입력 한 후 참조를 `IDIssues.aspx` 브라우저를 통해 페이지에서 나가를 입력 하 고 "제출" 단추를 클릭 합니다. "제출" 단추를 클릭 하면는 `NullReferenceException` 발생 (그림 5 참조).


[![NullReferenceException이 발생](control-id-naming-in-content-pages-vb/_static/image8.png)](control-id-naming-in-content-pages-vb/_static/image7.png)

**그림 05**: A `NullReferenceException` 발생 ([클릭 하 여 큰 이미지 보기](control-id-naming-in-content-pages-vb/_static/image9.png))


중단점을 설정 합니다 `SubmitButton_Click` 이벤트 처리기를 호출 모두 표시 됩니다 `FindControl` 반환 `Nothing`합니다. `NullReferenceException` 에 액세스 하려고 하는 경우 발생 합니다 `Age` 텍스트 상자의 `Text` 속성입니다.

문제는 `Control.FindControl` 만 검색 *제어*의 동일한 명명 컨테이너에 있는 하위 항목입니다. 새 명명 컨테이너에 대 한 호출을 구성 하는 마스터 페이지 때문 `Page.FindControl("controlID")` 하지 독립적이 마스터 페이지 개체 `ctl00`합니다. (다시 표시 하는 컨트롤 계층 구조를 보려면 그림 4 참조를 `Page` 마스터 페이지 개체의 부모로 개체 `ctl00`.) 따라서 합니다 `Results` 레이블 및 `Age` 텍스트 상자를 찾을 수 없는 및 `ResultsLabel` 및 `AgeTextBox` 의 값이 할당 됩니다 `Nothing`합니다.

두 가지 해결 방법이 이러한 과제를: 드릴 다운할 수 있습니다, 하나의 명명 컨테이너 적절 한 컨트롤에 한 번에 직접 만들 수 있습니다 또는 `FindControl` 명명 컨테이너 독립적이 메서드입니다. 이러한 각 옵션을 살펴보겠습니다.

### <a name="drilling-into-the-appropriate-naming-container"></a>적절 한 명명 컨테이너에 드릴 다운

사용 하도록 `FindControl` 참조를 `Results` 레이블 또는 `Age` 텍스트 상자를 호출 해야 `FindControl` 동일한 명명 컨테이너에서 상위 컨트롤에서 합니다. 그림 4와 같이, 합니다 `MainContent` 각각의 ContentPlaceHolder 컨트롤로의 유일한 상위 항목은 `Results` 또는 `Age` 동일한 명명 컨테이너 내에서입니다. 즉, 호출을 `FindControl` 메서드에서 `MainContent` 컨트롤 아래 코드 조각과에서 같이 올바르게 참조를 반환 합니다를 `Results` 또는 `Age` 컨트롤입니다.


[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample8.vb)]

그러나 것을 사용할 수 없습니다는 `MainContent` ContentPlaceHolder 마스터 페이지는 ContentPlaceHolder 정의 되었기 때문에 위의 구문을 사용 하는 콘텐츠 페이지의 코드 숨김 클래스에서. 대신 사용 해야 `FindControl` 에 대 한 참조를 가져오려면 `MainContent`합니다. 코드는 `SubmitButton_Click` 다음과 같이 수정을 사용 하 여 이벤트 처리기:


[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample9.vb)]

브라우저를 통해 페이지를 방문 하는 경우 나가를 입력 하 고 "제출" 단추를 클릭 한 `NullReferenceException` 발생 합니다. 에 중단점을 설정 하는 경우는 `SubmitButton_Click` 살펴보면 호출 하려고 할 때이 예외가 발생 하는 이벤트 처리기는 `MainContent` 개체의 `FindControl` 메서드. `MainContent` 개체와 같으면 `Nothing` 때문에 `FindControl` 메서드 "MainContent" 라는 개체를 찾을 수 없습니다. 기본 이유는 동일 하 게 합니다 `Results` 레이블 및 `Age` 텍스트 상자 컨트롤: `FindControl` 컨트롤 계층 구조의 위쪽에서 검색을 시작 하 고 명명 컨테이너를 침투 하지 않습니다 하지만 `MainContent` ContentPlaceHolder는 명명 컨테이너인 마스터 페이지입니다.

사용 하기 전에 `FindControl` 에 대 한 참조를 가져오려면 `MainContent`, 먼저 마스터 페이지 컨트롤에 대 한 참조 해야 합니다. 마스터 페이지에 대 한 참조가 있으면 참조를 가져올 수 있습니다는 `MainContent` 통해 ContentPlaceHolder `FindControl` 여기에서 참조 하 고는 `Results` 레이블 및 `Age` 텍스트 상자에 붙여넣습니다 (사용 하 여 다시 `FindControl`). 그러나에서는 어떻게 마스터 페이지에 대 한 참조? 검사 하 여 합니다 `id` 렌더링된 된 태그에서 특성 것은 분명 하는 마스터 페이지의 `ID` 값은 `ctl00`합니다. 사용할 수 있으므로 `Page.FindControl("ctl00")` 마스터 페이지에 대 한 참조를 가져오려면 다음 사용 하 여 해당 개체에 대 한 참조를 가져오려면 `MainContent`등입니다. 다음 코드 조각에서는이 논리를 보여 줍니다.


[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample10.vb)]

이 코드는 확실히 작동 하는 동안 것으로 가정 하는 마스터 페이지의 자동 생성 `ID` 은 항상 `ctl00`합니다. 되지 자동 생성 된 값에 대 한 가정 하는 것이 좋습니다.

다행 스럽게도 마스터 페이지에 대 한 참조를 통해 액세스할 수 합니다 `Page` 클래스의 `Master` 속성입니다. 사용 하지 않고 대신 따라서 `FindControl("ctl00")` 에 액세스 하기 위해 마스터 페이지의 참조를 가져오려면 합니다 `MainContent` ContentPlaceHolder를 대신 사용 하 여 `Page.Master.FindControl("MainContent")`. 업데이트 된 `SubmitButton_Click` 이벤트 처리기를 다음 코드로 바꿉니다.


[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample11.vb)]

이 경우 브라우저를 통해 페이지를 방문 하 나가를 입력 하 고 "제출" 단추를 클릭 하면 메시지를 표시 합니다 `Results` 레이블, 예상 대로입니다.


[![사용자의 나이 레이블에 표시 됩니다.](control-id-naming-in-content-pages-vb/_static/image11.png)](control-id-naming-in-content-pages-vb/_static/image10.png)

**그림 06**: 사용자의 나이 레이블에 표시 됩니다 ([큰 이미지를 보려면 클릭](control-id-naming-in-content-pages-vb/_static/image12.png))


### <a name="recursively-searching-through-naming-containers"></a>재귀적으로 명명 컨테이너 검색

이유는 이전 코드 예제에서는 참조를 `MainContent` 마스터 페이지에서 각각의 ContentPlaceHolder 컨트롤로 차례로 합니다 `Results` 레이블 및 `Age` TextBox 컨트롤에서 `MainContent`, 이므로 `Control.FindControl` 메서드만 검색 합니다. 내 *제어*의 명명 컨테이너입니다. 것 `FindControl` 명명 된 컨테이너 내에서 계속 적합 한 대부분의 시나리오에서 두 개의 서로 다른 명명 컨테이너에 두 개의 동일한 있을 수 있으므로 `ID` 값입니다. 이라는 레이블 웹 컨트롤을 정의 하는 GridView가 있다고 `ProductName` 해당 TemplateFields 중 하나입니다. 데이터를 런타임에 GridView에 바인딩될 때는 `ProductName` 각 GridView 행에 대해 레이블이 만들어집니다. 하는 경우 `FindControl` 모든 명명 검색할 컨테이너를 호출 `Page.FindControl("ProductName")`, 어떤 레이블 인스턴스 해야는 `FindControl` 반환? `ProductName` 첫 번째 GridView 행에서 레이블? 마지막 행에 있는 것?

이 있으면 `Control.FindControl` 만 검색 *제어*의 명명 컨테이너는 대부분의 것이 좋습니다. 고유한 있는 연결, 우리와 같은 다른 경우에도 `ID` 전체 컨테이너 이름 명명 및 신중 하 게 액세스를 제어 하는 컨트롤 계층 구조에서 각 명명 컨테이너를 참조할 필요가 없도록 하려고 합니다. 필요는 `FindControl` 너무 모든 명명 컨테이너는 재귀적으로 검색 감지 된 변형입니다. 아쉽게도.NET Framework는 이러한 메서드를 포함 되지 않습니다.

다행 스럽게도 만들 수 있습니다 고유한 `FindControl` 메서드는 재귀적으로 모든 명명 컨테이너를 검색 합니다. 실제로 사용 하 여 *확장 메서드* 우리를 넣습니다 수는 `FindControlRecursive` 메서드를 합니다 `Control` 클래스의 기존 함께 `FindControl` 메서드.

> [!NOTE]
> 확장 메서드는.NET Framework 버전 3.5 및 Visual Studio 2008과 함께 제공 되는 언어는 C# 3.0과 Visual Basic 9에 새 기능입니다. 즉, 특별 한 구문을 통해 기존 클래스 형식에 대 한 새 메서드를 만드는 개발자를 위한 확장 메서드를 사용 합니다. 이 유용한 기능에 대 한 자세한 내용은 필자의 기사를 참조 [확장 메서드를 사용 하 여 기본 형식 기능 확장](http://aspnet.4guysfromrolla.com/articles/120507-1.aspx)합니다.


확장 메서드를 만들려면 새 파일을 추가 합니다 `App_Code` 라는 폴더 `PageExtensionMethods.vb`합니다. 라는 확장 메서드를 추가 `FindControlRecursive` 입력으로 사용 하는 `String` 라는 매개 변수 `controlID`합니다. 제대로 작동 하려면 확장 메서드의 경우로 클래스를 표시 하는 중요 한 것을 `Module` 접두사로 추가 확장 메서드는 및를 `<Extension()>` 특성입니다. 또한 모든 확장 메서드가 받아들여야 첫 번째 매개 변수로 형식의 개체 확장 메서드가 적용 되는 합니다.

다음 코드를 추가 합니다 `PageExtensionMethods.vb` 파일을이 매크로 정의할 `Module` 및 `FindControlRecursive` 확장 메서드:


[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample12.vb)]

이 코드를 반환 합니다 `IDIssues.aspx` 페이지의 코드 숨김 클래스와 현재 주석 `FindControl` 메서드 호출 합니다. 에 대 한 호출으로 교체할 `Page.FindControlRecursive("controlID")`합니다. 확장 메서드에 대 한 간단한 것 IntelliSense 드롭다운 목록에 내에서 직접 표시 되어야 합니다. 그림 7에서 알 수 있듯이, 입력 하면 `Page` 기간을 누릅니다 하 고는 `FindControlRecursive` 메서드는 드롭다운 다른와 함께 IntelliSense에 포함 되어 `Control` 클래스 메서드.


[![확장 메서드 IntelliSense 드롭다운-목록에 포함 된](control-id-naming-in-content-pages-vb/_static/image14.png)](control-id-naming-in-content-pages-vb/_static/image13.png)

**그림 07**: 확장 메서드가에서 IntelliSense 드롭다운에 포함 됩니다 ([큰 이미지를 보려면 클릭](control-id-naming-in-content-pages-vb/_static/image15.png))


에 다음 코드를 입력 합니다 `SubmitButton_Click` 이벤트 처리기, 페이지를 방문 하 고, 나가를 입력 하 고, "제출" 단추를 클릭 하 여 테스트 합니다. 그림 6에 다시 표시 된 것과 같이 결과 출력 메시지 수, "age 살 됩니다."


[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample13.vb)]

> [!NOTE]
> 확장 메서드는 Visual Studio 2005를 사용 하는 경우 C# 3.0과 Visual Basic 9에 새 확장 메서드를 사용할 수 없습니다. 구현 해야 하는 대신는 `FindControlRecursive` 도우미 클래스에서 메서드. [Rick Strahl](http://www.west-wind.com/WebLog/default.aspx) 그의 블로그 게시물에서는 이러한 예제가 포함 되어 [ASP.NET Maser 페이지 및 `FindControl` ](http://www.west-wind.com/WebLog/posts/5127.aspx)합니다.


## <a name="step-4-using-the-correctidattribute-value-in-client-side-script"></a>4 단계:를 사용 하 여 올바른`id`클라이언트 쪽 스크립트에서 값을 특성

웹 컨트롤의 렌더링 된이 자습서의이 소개에서 설명한 대로, `id` 특성은 종종 프로그래밍 방식으로 특정 HTML 요소를 참조 하려면 클라이언트 쪽 스크립트에서 사용 됩니다. 다음 JavaScript에서 HTML 요소를 참조 하는 예를 들어, 해당 `id` 다음 모달 메시지 상자에 해당 값을 표시 합니다.


[!code-csharp[Main](control-id-naming-in-content-pages-vb/samples/sample14.cs)]

회수 하는 페이지는 ASP.NET는 명명 컨테이너를 렌더링된 된 HTML 요소를 포함 하지 마십시오 `id` 특성이 웹 컨트롤의 동일 `ID` 속성 값입니다. 이 때문에 하드 코딩 하 고 싶을 것 `id` JavaScript 코드에 특성 값입니다. 즉, 알고 있는 경우 액세스 하려는 합니다 `Age` 클라이언트 쪽 스크립트를 통해 텍스트 웹 컨트롤에 대 한 호출을 통해 이렇게 `document.getElementById("Age")`합니다.

이 방법의 문제는 마스터 페이지 (또는 다른 명명 컨테이너 컨트롤)를 사용 하는 경우 렌더링된 된 HTML `id` 웹 컨트롤에 있는 동의어 아닙니다 `ID` 속성입니다. 첫 번째 기울기에 브라우저를 통해 페이지를 방문 하 여 실제 결정할 소스를 볼 수 있습니다 `id` 특성입니다. 렌더링 된 알았으면 `id` 값을 붙여넣을 수 있습니다 것에 대 한 호출 `getElementById` 클라이언트 쪽 스크립트를 통해 사용 해야 하는 HTML 요소에 액세스 하 합니다. 이 방법은 이상적인 이므로 특정 변경 내용 페이지의 컨트롤 계층 구조 또는 변경 합니다 `ID` 명명 컨트롤의 속성 변경 결과 `id` 함으로써 JavaScript 코드의 주요 특성입니다.

다행 스럽게도 하는 `id` 렌더링 되는 특성 값이 웹 컨트롤을 통해 서버 쪽 코드에서 액세스할 수 있는 [ `ClientID` 속성](https://msdn.microsoft.com/library/system.web.ui.control.clientid.aspx). 이 속성을 사용 하 여 확인 해야 하는 `id` 클라이언트 쪽 스크립트에서 사용 되는 값을 특성입니다. 예를 들어 페이지에는 JavaScript 함수를 추가할를 호출 하면 값을 표시 합니다 `Age` 모달 메시지 상자에 텍스트 상자에 다음 코드를 추가 `Page_Load` 이벤트 처리기:


[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample15.vb)]

위 코드의 값을 삽입 합니다 `Age` 텍스트 상자의 `ClientID` 속성에 대 한 JavaScript 호출을 `getElementById`입니다. 브라우저를 통해이 페이지를 방문 하 고 HTML 소스를 보고 하는 경우 다음 JavaScript 코드를 찾을 수 있습니다.


[!code-html[Main](control-id-naming-in-content-pages-vb/samples/sample16.html)]

알림 방법을 올바른 `id` 특성 값, `ctl00_MainContent_Age`를 호출 내에 나타납니다 `getElementById`합니다. 이 값이 런타임에 계산 되므로 이후 변경 페이지 컨트롤 계층 구조에 관계 없이 작동 합니다.

> [!NOTE]
> JavaScript 예제에는 단순히 올바르게 서버 컨트롤에서 렌더링 된 HTML 요소를 참조 하는 JavaScript 함수를 추가 하는 방법을 보여 줍니다. 이 함수를 사용 하 여 문서를 로드 하거나 특정 사용자의 일부 동작에서 다소 때 함수를 호출 하는 JavaScript를 작성 해야 합니다. 이 대 한 자세한 내용은 관련 항목을 읽을 [클라이언트 쪽 스크립트를 사용 하 여 작업](https://msdn.microsoft.com/library/aa479302.aspx)합니다.


## <a name="summary"></a>요약

특정 ASP.NET 서버 컨트롤의 역할을 명명 컨테이너는 렌더링 된 영향을 미칩니다 `id` 여 canvassed 컨트롤의 범위와 해당 하위 컨트롤의 값 특성을 `FindControl` 메서드. 마스터 페이지와 관련 하 여 자체 마스터 페이지와 해당 ContentPlaceHolder 컨트롤에 컨테이너 이름 명명 됩니다. 따라서 프로그래밍 방식으로 사용 하는 콘텐츠 페이지 내에서 컨트롤을 참조 하도록 명시 좀 더 많은 작업을 저장 해야 `FindControl`합니다. 이 자습서에서는 두 가지 기술을 살펴보았습니다: ContentPlaceHolder 컨트롤로 드릴링 하 고 호출 해당 `FindControl` ; 메서드와 고유한 롤링 `FindControl` 모든 명명 컨테이너를 통해 구현은 재귀적으로 검색 합니다.

명명 컨테이너 소개 웹 컨트롤 참조와 관련 하 여 서버 쪽 문제, 외에 클라이언트 쪽 문제가 있습니다. 없는 경우 컨테이너 웹 컨트롤의 명명 `ID` 속성 값 및 렌더링 `id` 특성 값은 동일한 것입니다. 하지만 명명 컨테이너에는 렌더링 된 추가 `id` 특성이 모두 포함 합니다 `ID` 웹 컨트롤 및 해당 컨트롤 계층의 상위 구조에서 명명 컨테이너의 값입니다. 이러한 명명 문제는 비-문제를 사용 하는 웹 컨트롤의 `ClientID` 렌더링 된 결정할 속성 `id` 클라이언트 쪽 스크립트에서 값을 특성입니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 마스터 페이지 및 `FindControl`](http://www.west-wind.com/WebLog/posts/5127.aspx)
- [동적 데이터 입력 사용자 인터페이스 만들기](https://msdn.microsoft.com/library/aa479330.aspx)
- [확장 메서드를 사용 하 여 기본 형식 기능 확장](http://aspnet.4guysfromrolla.com/articles/120507-1.aspx)
- [방법: ASP.NET 마스터 페이지 콘텐츠를 참조 합니다.](https://msdn.microsoft.com/library/xxwa0ff0.aspx)
- [마스터 페이지: 팁, 요령 및 트랩](http://www.odetocode.com/articles/450.aspx)
- [클라이언트 쪽 스크립트를 사용 하 여 작업](https://msdn.microsoft.com/library/aa479302.aspx)

### <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 작성자의 여러 ASP/ASP.NET 서적과 4GuysFromRolla.com의 설립자 이며, 왔습니다 Microsoft 웹 기술을 1998 합니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 3.5 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. Scott에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com) 통하거나 저자의 블로그 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Zack Jones와 Suchi Barnerjee 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)합니다.

> [!div class="step-by-step"]
> [이전](urls-in-master-pages-vb.md)
> [다음](interacting-with-the-master-page-from-the-content-page-vb.md)
