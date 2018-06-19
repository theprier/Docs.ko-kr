---
uid: web-forms/overview/older-versions-getting-started/master-pages/control-id-naming-in-content-pages-cs
title: 콘텐츠 페이지 (C#)에 ID 이름 지정을 제어 | Microsoft Docs
author: rick-anderson
description: ContentPlaceHolder 컨트롤 명명 컨테이너 역할을 하 고 따라서 프로그래밍 방식으로 (FindConrol)을 통해 어려운 컨트롤 사용을 확인 하는 방법을 방법을 보여 줍니다 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2008
ms.topic: article
ms.assetid: 1c7d0916-0988-4b4f-9a03-935e4b5af6af
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/control-id-naming-in-content-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 1e834c38457c8477e0c81598d32f1e98473949d7
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30891349"
---
<a name="control-id-naming-in-content-pages-c"></a>콘텐츠 페이지 (C#)의 이름을 지정 하는 컨트롤 ID
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_05_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_05_CS.pdf)

> ContentPlaceHolder 컨트롤 명명 컨테이너 역할을 하 고 따라서 프로그래밍 방식으로 컨트롤 (FindConrol)을 통해 어려운 작업을 수행할 방법을 보여 줍니다. 이 문제와 해결 방법에 살펴봅니다. 또한 결과 ClientID 값을 프로그래밍 방식으로 액세스 하는 방법을 설명 합니다.


## <a name="introduction"></a>소개

모든 ASP.NET 서버 컨트롤에 포함 된 `ID` 속성 고유 하 게 컨트롤을 식별 하 고 있는 컨트롤은 프로그래밍 방식으로 액세스할 코드 숨김 클래스에서 수단입니다. 마찬가지로, 요소는 HTML 문서에 포함 될 수 있습니다는 `id` 요소를 고유 하 게 식별 하는 특성; 이러한 `id` 값은 보통 특정 HTML 요소를 프로그래밍 방식으로 참조를 클라이언트 쪽 스크립트에 사용 됩니다. 이 점을 고려 하 고 가정할 수도 있습니다는 ASP.NET 서버 컨트롤을 HTML로 렌더링 될 때 해당 `ID` 값으로 사용 되는 `id` 렌더링 된 HTML 요소의 값입니다. 이 아닐 경우 상황에 따라 단일는 단일 제어 하기 때문에 `ID` 렌더링 된 태그에 값이 여러 번 표시 될 수 있습니다. TemplateField와 레이블 웹 컨트롤을 포함 하는 GridView 컨트롤 고려는 `ID` ProductName의 값입니다. 런타임에 해당 데이터 원본에 GridView 바인딩되면이 레이블은 모든 GridView 행에 대해 한 번씩 반복 됩니다. 각각 렌더링 레이블 요구는 고유한 `id` 값입니다.

이러한 시나리오를 처리 하려면 ASP.NET에는 특정 컨트롤 명명 컨테이너로 표시 될 수 있도록 합니다. 명명 컨테이너 역할을 새 `ID` 네임 스페이스입니다. 명명 컨테이너 내에 표시 된 서버 컨트롤의 렌더링 된가 `id` 기수가 `ID` 명명 컨테이너 컨트롤의 합니다. 예를 들어는 `GridView` 및 `GridViewRow` 클래스는 모두 명명 컨테이너입니다. 결과적으로 GridView TemplateField에 정의 된 Label 컨트롤 `ID` ProductName 렌더링 된 제공할지 `id` 값 `GridViewID_GridViewRowID_ProductName`합니다. 때문에 *GridViewRowID* 그 결과 각 GridView 행에 대해 고유한 `id` 값이 고유 합니다.

> [!NOTE]
> [ `INamingContainer` 인터페이스](https://msdn.microsoft.com/library/system.web.ui.inamingcontainer.aspx) 특정 ASP.NET 서버 컨트롤 명명 컨테이너로 작동 해야 나타내는 데 사용 됩니다. `INamingContainer` 인터페이스 서버 컨트롤을 구현 해야 하는 모든 메서드 쓰십시오 하지 않는 않으며 대신, 표식으로 사용 됩니다. 생성 되는 렌더링 된 태그의 컨트롤을이 인터페이스를 구현 하는 경우 다음 ASP.NET 엔진 자동으로 붙입니다 해당 `ID` 값은 종속 항목을 렌더링 `id` 특성 값입니다. 이 프로세스는 2 단계에서에서 더 자세하게에서 설명 합니다.


명명 컨테이너 뿐만 아니라는 렌더링 된 변경 `id` 특성 값, 있지만 어떻게 컨트롤 참조 될 수 있습니다 프로그래밍 방식으로 ASP.NET 페이지의 코드 숨김 클래스에서 영향을 줍니다. `FindControl("controlID")` 메서드는 프로그래밍 방식으로 웹 컨트롤을 참조 하는 데 주로 사용 됩니다. 그러나 `FindControl` 명명 컨테이너를 통해 침투 하지 않습니다. 직접 사용할 수 없습니다, 결과적으로 `Page.FindControl` 는 GridView 또는 기타 명명 컨테이너 내에서 컨트롤을 참조 하는 메서드.

처럼 surmised 있을 수 있습니다, 마스터 페이지 및 contentplaceholders의 둘 다 구현 되지 명명 컨테이너입니다. 이 자습서에서는 어떻게 마스터 페이지에 영향을 HTML 요소 살펴보겠습니다 `id` 프로그래밍 방식으로 사용 하 여 콘텐츠 페이지 내에서 웹 컨트롤을 참조 하는 방법 및 값 `FindControl`합니다.

## <a name="step-1-adding-a-new-aspnet-page"></a>1 단계: 새 ASP.NET 페이지를 추가합니다.

이 자습서에 설명 된 개념을 보여 주기 위해 웹 사이트를 새 ASP.NET 페이지를 추가 해 보겠습니다. 라는 새 콘텐츠 페이지를 만들고 `IDIssues.aspx` 루트 폴더에서에 바인딩하기는 `Site.master` 마스터 페이지입니다.


![콘텐츠 페이지 IDIssues.aspx 루트 폴더에 추가](control-id-naming-in-content-pages-cs/_static/image1.png)

**그림 01**: 콘텐츠 페이지 추가 `IDIssues.aspx` 루트 폴더에


Visual Studio의 마스터 페이지의 4 개 contentplaceholders의 각 콘텐츠 컨트롤을 자동으로 만듭니다. 설명한 것 처럼는 [ *여러 contentplaceholders 및 기본 콘텐츠* ](multiple-contentplaceholders-and-default-content-cs.md) 자습서, 마스터 페이지의 기본 ContentPlaceHolder 콘텐츠 대신 내보낸 콘텐츠 컨트롤이 없는 경우. 때문에 `QuickLoginUI` 및 `LeftColumnContent` contentplaceholders의이 페이지에 대 한 적합 한 기본 태그가 포함, 계속 해 서 항목 및 해당 제거에서 콘텐츠 컨트롤 `IDIssues.aspx`합니다. 이 시점에서 선언 콘텐츠 페이지의 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](control-id-naming-in-content-pages-cs/samples/sample1.aspx)]

에 [ *마스터 페이지의 제목, 메타 태그 및 기타 HTML 헤더를 지정 하* ](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) 자습서는 기본 페이지를 사용자 지정 클래스를 만들었습니다 (`BasePage`) 구성 하는 자동으로 페이지의 제목 경우 명시적으로 설정 합니다. 에 대 한는 `IDIssues.aspx` 이 기능을 사용 하 여 페이지에서 페이지의 코드 숨김 클래스에서 파생 되어야 합니다는 `BasePage` 클래스 (대신 `System.Web.UI.Page`). 다음과 같이 표시 되도록 코드 숨김 클래스의 정의 수정 합니다.


[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample2.cs)]

마지막으로 업데이트는 `Web.sitemap` 파일을 새이 단원에 대 한 항목을 포함 합니다. 추가 `<siteMapNode>` 요소 집합과 해당 `title` 및 `url` "컨트롤 ID 명명 문제"를 특성 및 `~/IDIssues.aspx`각각. 이 추가 마치면 프로그램 `Web.sitemap` 파일의 태그는 다음과 비슷해야 합니다.


[!code-xml[Main](control-id-naming-in-content-pages-cs/samples/sample3.xml)]

그림 2 있듯이에 새 사이트 맵 항목 `Web.sitemap` 왼쪽된 열에서 단원 섹션에 즉시 반영 됩니다.


![다음 단원 섹션에는 이제에 대 한 링크가 포함 되어 &quot;명명 문제 ID를 제어 합니다.&quot;](control-id-naming-in-content-pages-cs/_static/image2.png)

**그림 02**: 단원 섹션에는 이제 "컨트롤 ID 명명 문제"에 대 한 링크 포함


## <a name="step-2-examining-the-renderedidchanges"></a>2 단계: 렌더링 된 검사`ID`변경 내용

ASP.NET 수정 사항을 더 잘 이해 하려면 엔진에 게는 렌더링 된 `id` 서버의 값을 제어, 몇 가지 웹 컨트롤을 추가 하겠습니다는 `IDIssues.aspx` 페이지 한 다음 브라우저에 보내지는 렌더링 된 태그를 표시 합니다. 특히, 텍스트를 입력 "나이 입력 하십시오:" TextBox 웹 control이 옵니다. 추가 아래로 페이지에서 추가 단추 웹 컨트롤 및 레이블 웹 컨트롤입니다. 텍스트 상자의 설정 `ID` 및 `Columns` 속성을 `Age` 와 3을 각각. 단추의 설정 `Text` 및 `ID` 속성을 "제출" 및 `SubmitButton`합니다. 레이블 지우기 `Text` 속성 집합과 해당 `ID` 를 `Results`합니다.

이 시점에서 콘텐츠 컨트롤의 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](control-id-naming-in-content-pages-cs/samples/sample4.aspx)]

그림 3에서는 Visual Studio의 디자이너를 통해 볼 때 페이지를 보여 줍니다.


[![페이지에는 세 가지 웹 컨트롤에 포함:는 텍스트 상자, 단추 및 레이블](control-id-naming-in-content-pages-cs/_static/image4.png)](control-id-naming-in-content-pages-cs/_static/image3.png)

**그림 03**: The 페이지에 포함 되어 세 가지 웹 컨트롤: 텍스트 상자, 단추 및 레이블 ([전체 크기 이미지를 보려면 클릭](control-id-naming-in-content-pages-cs/_static/image5.png))


브라우저를 통해 페이지를 방문 하 고 HTML 소스를 봅니다. 를 다음 태그로 `id` 텍스트 상자, 단추 및 레이블에 웹 컨트롤에 대 한 HTML 요소의 값은의 조합은 `ID` 웹 컨트롤 값 및 `ID` 페이지에 있는 명명 컨테이너의 값입니다.


[!code-html[Main](control-id-naming-in-content-pages-cs/samples/sample5.html)]

이 자습서의 앞부분에서 설명 했 듯이 마스터 페이지와 해당 contentplaceholders의 명명 컨테이너도 사용 됩니다. 따라서 둘 다 영향을 렌더링 된 `ID` 중첩 된 해당 컨트롤의 값입니다. 텍스트 상자의 수행 `id` 예를 들어 특성: `ctl00_MainContent_Age`합니다. 이전에 설명한 대로 TextBox 컨트롤의 `ID` 값이 `Age`합니다. 이 해당 ContentPlaceHolder 컨트롤의 접두사로 `ID` 값 `MainContent`합니다. 이 값은 마스터 페이지에 접두사로 또한 `ID` 값 `ctl00`합니다. 한 순수 효과는 `id` 특성 값으로 이루어진는 `ID` 마스터 페이지, ContentPlaceHolder 컨트롤 및 TextBox 자체의 값입니다.

그림 4는이 동작을 보여 줍니다. 렌더링 된 확인 하려면 `id` 의 `Age` TextBox로 시작은 `ID` TextBox 컨트롤의 값 `Age`합니다. 그런 다음 작업을 진행 컨트롤 계층 구조입니다. 각 명명 컨테이너 (분홍색 색으로 해당 노드)에서 렌더링 현재 접두사 `id` 명명 컨테이너와 `id`합니다.


![렌더링 됨 id 특성 기반에 ID 값은 명명 컨테이너](control-id-naming-in-content-pages-cs/_static/image6.png)

**그림 04**: The 렌더링 `id` 기준 특성은는 `ID` 명명 컨테이너의 값


> [!NOTE]
> 설명한 것 처럼는 `ctl00` 는 렌더링 된 부분 `id` 구성 하는 특성의 `ID` 마스터 페이지의 값이 궁금할 수 있습니다 어떻게이 `ID` 값에 대 한 제공 합니다. 지정 하지 않았기 것 아무 곳 이나 가격 마스터 또는 콘텐츠 페이지에 있습니다. ASP.NET 페이지에서 대부분의 서버 컨트롤은 페이지의 선언적 태그를 통해 명시적으로 추가 됩니다. `MainContent` ContentPlaceHolder 컨트롤의 태그에 명시적으로 지정 된 `Site.master`; `Age` 텍스트 상자에 정의 된 `IDIssues.aspx`의 태그입니다. 지정 하는 `ID` 이러한 종류의 선언적 구문 또는 속성 창을 통해 컨트롤에 대 한 값입니다. 마스터 페이지 자체 같은 다른 컨트롤의 선언적 태그에서 정의 되지 않습니다. 따라서 해당 `ID` 값을 수행해 줍니다 자동으로 생성 해야 합니다. Asp 엔진은 `ID` Id 명시적으로 설정 되지 않은 해당 컨트롤에 대 한 런타임에 값입니다. 명명 패턴을 사용 하 여 `ctlXX`여기서 *XX* 은 순차적으로 증가 하는 정수 값입니다.


마스터 페이지 자체 하는 데 사용 명명 컨테이너 때문에 마스터 페이지에 정의 된 웹 컨트롤도 변경을 렌더링 된 `id` 특성 값입니다. 예를 들어는 `DisplayDate` 에서 마스터 페이지에 추가한 레이블은 [ *마스터 페이지를 사용 하 여 사이트 전체 레이아웃 만들기* ](creating-a-site-wide-layout-using-master-pages-cs.md) 자습서에는 태그를 렌더링 하는 다음:


[!code-html[Main](control-id-naming-in-content-pages-cs/samples/sample6.html)]

`id` 특성에 모두 마스터 페이지의 `ID` 값 (`ctl00`) 및 `ID` Label 웹 컨트롤의 값 (`DateDisplay`).

## <a name="step-3-programmatically-referencing-web-controls-viafindcontrol"></a>3 단계:를 통해 웹 컨트롤을 프로그래밍 방식으로 참조`FindControl`

모든 ASP.NET 서버 컨트롤에는 `FindControl("controlID")` 라는 컨트롤에 대 한 컨트롤의 하위 항목을 검색 하는 메서드 *controlID*합니다. 이러한 컨트롤이 발견 되는 경우 반환 됩니다. 없는 일치 하는 컨트롤을 찾을 `FindControl` 반환 `null`합니다.

`FindControl` 컨트롤에 액세스 하려면 있었지만에 대 한 직접 참조가 없는 시나리오에서 유용 합니다. 예를 들어 GridView 같은 웹 컨트롤을 데이터로 작업할 때 GridView의 필드 내에서 컨트롤의 선언적 구문에서 한 번 정의 되지만 런타임 시 각 GridView 행에 대해 컨트롤의 인스턴스가 만들어집니다. 따라서 런타임에 생성 컨트롤 있지만 직접 참조 코드 숨김 클래스에서 사용할 수는 없습니다. 사용 해야 결과적으로 `FindControl` GridView의 필드 내에서 특정 컨트롤에 프로그래밍 방식으로 작동 하도록 합니다. (사용 하 여 대 한 자세한 내용은 `FindControl` 데이터 웹 컨트롤 템플릿 내에서 컨트롤에 액세스 하려면 참조 [데이터 기반 시 사용자 지정 서식](../../data-access/custom-formatting/custom-formatting-based-upon-data-cs.md).) 동일한 경우가 Web Form에 동적으로 웹 컨트롤을 추가, 항목에 설명 된 [만드는 동적 데이터 입력 사용자 인터페이스가](https://msdn.microsoft.com/library/aa479330.aspx)합니다.

사용 하 여 설명 하기 위해는 `FindControl` 콘텐츠 페이지에서 컨트롤을 검색 하는 메서드 만들기에 대 한 이벤트 처리기는 `SubmitButton`의 `Click` 이벤트입니다. 이벤트 처리기에서 프로그래밍 방식으로 참조 하는 다음 코드를 추가 `Age` 텍스트 상자 및 `Results` 레이블을 사용 하 여는 `FindControl` 메서드 다음에 메시지를 표시 하 고 `Results` 사용자의 입력에 따라 합니다.

> [!NOTE]
> 물론, 사용할 필요가 없습니다 `FindControl` 를이 예제에 대 한 레이블 및 TextBox 컨트롤을 참조 합니다. 통해 직접 참조할 수 있습니다는 `ID` 속성 값입니다. 사용 `FindControl` 사용 하는 경우 수행 되는 작업을 설명 하기 위해 여기 `FindControl` 콘텐츠 페이지에서.


[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample7.cs)]

호출 하는 데 사용 하는 구문을 동안는 `FindControl` 의 처음 두 줄의 방법이 약간씩 다릅니다 `SubmitButton_Click`, 의미상 동일 합니다. 모든 ASP.NET 서버 컨트롤을 포함 하는 회수는 `FindControl` 메서드. 여기에 `Page` 클래스는 모든 ASP.NET에서 코드 숨김 클래스에서 파생 되어야 합니다. 따라서 호출 `FindControl("controlID")` 호출 하는 것과 같습니다 `Page.FindControl("controlID")`, 재정의 하지 않은 것으로 가정는 `FindControl` 메서드 코드 숨김 클래스 또는 사용자 지정 기본 클래스입니다.

이 코드를 입력 한 후 방문는 `IDIssues.aspx` 브라우저를 통해 페이지, 나이, 입력을 "제출" 단추를 클릭 합니다. "제출" 단추를 클릭 하면는 `NullReferenceException` 발생 (그림 5 참조).


[![NullReferenceException이 발생 하는](control-id-naming-in-content-pages-cs/_static/image8.png)](control-id-naming-in-content-pages-cs/_static/image7.png)

**그림 05**: A `NullReferenceException` 발생 ([전체 크기 이미지를 보려면 클릭](control-id-naming-in-content-pages-cs/_static/image9.png))


중단점을 설정 하는 경우는 `SubmitButton_Click` 이벤트 처리기를 호출 모두 나타납니다 `FindControl` 반환는 `null` 값입니다. `NullReferenceException` 에 액세스 하려고 하면 때 발생 하는 `Age` 텍스트 상자의 `Text` 속성입니다.

문제는 `Control.FindControl` 검색 *제어*의 하위 항목이 있는 *동일한 명명 컨테이너에서*합니다. 마스터 페이지를 새 명명 컨테이너에 대 한 호출 하기 때문에 `Page.FindControl("controlID")` 되지 독립적이 마스터 페이지 개체 `ctl00`합니다. (그림 4를 보여 주는 컨트롤 계층 구조를 보려면 다시 참조는 `Page` 마스터 페이지 개체의 부모로 개체 `ctl00`.) 따라서는 `Results` 레이블 및 `Age` TextBox를 찾을 수 없는 및 `ResultsLabel` 및 `AgeTextBox` 의 값이 할당 됩니다 `null`합니다.

이 시도에 두 가지 해결 방법이 없는:; 해당 컨트롤에 한 번에 하나의 명명 컨테이너를 파악할 수 고유한을 만들 수 있습니다 또는 `FindControl` 명명 컨테이너 독립적이 메서드입니다. 이러한 각 옵션을 살펴보겠습니다.

### <a name="drilling-into-the-appropriate-naming-container"></a>적절 한 명명 된 컨테이너로 드릴

사용 하도록 `FindControl` 참조에는 `Results` 레이블 또는 `Age` 텍스트 상자를 호출 해야 `FindControl` 동일한 명명 컨테이너의 상위 항목 컨트롤에서 합니다. 그림 4에서 설명한 대로 `MainContent` ContentPlaceHolder 컨트롤의 유일한 상위 항목은 `Results` 또는 `Age` 동일한 명명 컨테이너 내 합니다. 즉, 호출의 `FindControl` 에서 메서드는 `MainContent` 컨트롤 아래 코드 조각에 나와 있는 것 처럼 올바르게 반환에 대 한 참조는 `Results` 또는 `Age` 컨트롤입니다.


[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample8.cs)]

그러나 우리 작업할 수 없습니다는 `MainContent` ContentPlaceHolder는 마스터 페이지에 정의 되어 있으므로 위의 구문을 사용 하는 콘텐츠 페이지의 코드 숨김 클래스에서 ContentPlaceHolder 합니다. 대신 사용 하는 `FindControl` 에 대 한 참조를 얻으려고 `MainContent`합니다. 코드는 `SubmitButton_Click` 이벤트 처리기를 다음과 같이 수정 합니다.


[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample9.cs)]

브라우저를 통해 페이지를 방문 하는 경우 나가를 입력 하 고 "제출" 단추를 클릭 한 `NullReferenceException` 발생 합니다. 중단점을 설정 하는 경우는 `SubmitButton_Click` 이벤트 처리기를 호출 하려고 할 때이 예외가 발생 있는지 표시 됩니다는 `MainContent` 개체의 `FindControl` 메서드. `MainContent` 개체가 `null` 때문에 `FindControl` 메서드 "MainContent" 라는 개체를 찾을 수 없습니다. 와 동일 하 게는 기본 이유는는 `Results` 레이블 및 `Age` TextBox 컨트롤: `FindControl` 컨트롤 계층 구조 맨 위부터 검색을 시작 하 고 명명 컨테이너를 침투지 않습니다 되지만 `MainContent` ContentPlaceHolder는 마스터 페이지 내에서 명명 컨테이너 즉입니다.

사용할 수 있습니다 `FindControl` 에 대 한 참조를 얻으려고 `MainContent`, 먼저 마스터 페이지 컨트롤에 대 한 참조가 필요 합니다. 마스터 페이지에 대 한 참조를 일단에 대 한 참조를 가져올 수 있습니다는 `MainContent` 통해 ContentPlaceHolder `FindControl` 여기에서를 참조 하 고는 `Results` 레이블 및 `Age` 텍스트 상자에 붙여넣습니다 (다시 사용 하 여 통해 `FindControl`). 그러나 우리 어떻게 마스터 페이지에 대 한 참조? 검사 하 여는 `id` 렌더링된 된 태그에서 특성 것은 분명 하는 마스터 페이지의 `ID` 값은 `ctl00`합니다. 따라서 사용 하 여 `Page.FindControl("ctl00")` 마스터 페이지에 대 한 참조를 가져오려면 다음 사용 하 여 해당 개체에 대 한 참조를 얻으려고 `MainContent`등입니다. 다음 코드 조각에서는이 논리를 보여 줍니다.


[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample10.cs)]

이 코드는 작동 확실히 동안 있다고 가정 마스터 페이지의 자동 생성 된 `ID` 항상 `ctl00`합니다. 하지 자동으로 생성 된 값에 대 한 가정을 만들 것이 좋습니다.

다행히 마스터 페이지에 대 한 참조는를 통해 액세스할 수는 `Page` 클래스의 `Master` 속성입니다. 따라서을 사용할 필요 없음 `FindControl("ctl00")` 에 액세스 하기 위해 마스터 페이지의 대 한 참조를 가져오려면는 `MainContent` ContentPlaceHolder를 대신 사용할 수 `Page.Master.FindControl("MainContent")`합니다. 업데이트는 `SubmitButton_Click` 이벤트 처리기를 다음 코드로:


[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample11.cs)]

이 이번에는 브라우저를 통해 페이지를 방문 나가를 입력 하 고 "제출" 단추를 클릭 하면 메시지를 표시는 `Results` 예상 대로 레이블을 합니다.


[![사용자의 나이 레이블에 표시 되는](control-id-naming-in-content-pages-cs/_static/image11.png)](control-id-naming-in-content-pages-cs/_static/image10.png)

**그림 06**: 레이블에 사용자의 나이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](control-id-naming-in-content-pages-cs/_static/image12.png))


### <a name="recursively-searching-through-naming-containers"></a>재귀적으로 명명 컨테이너 검색

이전 코드 예제를 참조 하는 이유는 `MainContent` ContentPlaceHolder 컨트롤의 마스터 페이지에서 다음의 `Results` 레이블 및 `Age` 텍스트 상자에서 제어 `MainContent`, ¿¡´는 `Control.FindControl` 메서드만 검색 합니다. 내에서 *제어*의 명명 컨테이너입니다. 필요 `FindControl` 명명 컨테이너에 있는 상태로 유지 되는 것이 좋습니다 대부분의 시나리오에서 두 개의 서로 다른 명명 컨테이너에 두 개의 동일한 있을 수 있으므로 `ID` 값입니다. 라는 Label 웹 컨트롤을 정의 하는 GridView의 경우를 살펴봅시다 `ProductName` TemplateFields 그 중 하나에서 합니다. 데이터가 런타임에 GridView에 바인딩될 때는 `ProductName` 레이블이 각 GridView 행에 대해 만들어집니다. 경우 `FindControl` 모든 이름 지정을 통해 검색 되 고, 컨테이너 라는 `Page.FindControl("ProductName")`, 어떤 레이블 인스턴스 해야는 `FindControl` 반환? `ProductName` 첫 번째 GridView 행에서 레이블? 마지막 행에 바꾸시겠습니까?

하므로 `Control.FindControl` 방금 검색 *제어*의 명명 컨테이너는 대부분의 경우에서 것이 좋습니다. 고유한 이상인 us, 연결 하는 것과 같은 다른 경우도 있습니다. 하지만 `ID` 모든 명명 컨테이너를 신중 하 게 액세스를 제어 하려면 제어 계층 구조에서 각 명명 컨테이너를 참조할 필요가 없도록 하려면. 발생 한 `FindControl` 너무 모든 명명 컨테이너는 재귀적으로 검색 감지 하는 variant입니다. 그러나.NET Framework는 이러한 메서드를 포함 되지 않습니다.

다행 스럽게도을 만들면 고유한 `FindControl` 메서드 모든 명명 컨테이너를 검색 하는 해당 회귀적으로 검색 합니다. 실제로 사용 하 여 *확장 메서드* म를 넣습니다 수는 `FindControlRecursive` 메서드를는 `Control` 클래스의 기존 함께 `FindControl` 메서드.

> [!NOTE]
> 확장 메서드는.NET Framework 버전 3.5 및 Visual Studio 2008과 함께 제공 되는 언어는 C# 3.0과 Visual Basic 9를 새로운 기능입니다. 즉, 특수 한 구문을 통해 기존 클래스 형식에 대 한 새 메서드를 만드는 개발자에 대 한 확장 메서드를 사용 합니다. 이 유용한 기능에 대 한 자세한 내용은 내 문서를 참조 [확장 메서드를 사용한 기본 형식 기능 확장](http://aspnet.4guysfromrolla.com/articles/120507-1.aspx)합니다.


확장 메서드를 만들려면 새 파일을 추가 `App_Code` 라는 폴더 `PageExtensionMethods.cs`합니다. 라는 확장 메서드를 추가 `FindControlRecursive` 입력으로 사용 하는 `string` 라는 매개 변수 `controlID`합니다. 제대로 작동 하려면 확장 메서드는 클래스 자체 및 해당 확장 메서드를 표시 하는 것이 중요 한 `static`합니다. 첫 번째 매개 변수는 확장 메서드가 적용 되는 형식의 개체 및이 입력된 매개 변수 뒤에 야 키워드를 사용 하는 대로 모든 확장 메서드가 동의 해야 또한 `this`합니다.

다음 코드를 추가 하는 `PageExtensionMethods.cs` 이 클래스를 정의 하려면 클래스 파일 및 `FindControlRecursive` 확장 메서드:


[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample12.cs)]

이 코드 위치에서을 반환 하는 `IDIssues.aspx` 페이지의 코드 숨김 클래스와 현재 주석 `FindControl` 메서드를 호출 합니다. 에 대 한 호출 바꿉니다 `Page.FindControlRecursive("controlID")`합니다. 확장 메서드에 대 한 유용한 IntelliSense 드롭 다운 목록 내에서 직접 나타나는입니다. 그림 7에서 볼 수 있듯이 때 페이지를 입력 한 다음 시간에 도달는 `FindControlRecursive` 메서드 드롭 다운 다른 함께 IntelliSense에 포함 되어 `Control` 클래스 메서드.


[![확장 메서드에 IntelliSense 드롭다운 메뉴에 포함 된](control-id-naming-in-content-pages-cs/_static/image14.png)](control-id-naming-in-content-pages-cs/_static/image13.png)

**그림 07**: 확장 메서드에 IntelliSense 드롭다운 메뉴에 포함 됩니다 ([전체 크기 이미지를 보려면 클릭](control-id-naming-in-content-pages-cs/_static/image15.png))


다음 코드를 입력의 `SubmitButton_Click` 이벤트 처리기, 페이지를 방문 하 고, 나가를 입력 하 고, "제출" 단추를 클릭 하 여 테스트 합니다. 그림 6에 다시 표시 된 것과 같이 결과 출력 메시지 됩니다, 그리고 "age 살이!"


[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample13.cs)]

> [!NOTE]
> 확장 메서드는 Visual Studio 2005를 사용 하는 경우 C# 3.0과 Visual Basic 9에 새 확장 메서드를 사용할 수 없습니다. 구현 해야 하는 대신,는 `FindControlRecursive` 도우미 클래스에서 메서드. [Rick Strahl](http://www.west-wind.com/WebLog/default.aspx) 에 대 한 예는 블로그 게시물을 [ASP.NET 메이저 페이지 및 `FindControl` ](http://www.west-wind.com/WebLog/posts/5127.aspx)합니다.


## <a name="step-4-using-the-correctidattribute-value-in-client-side-script"></a>4 단계:를 사용 하 여 올바른`id`특성 값에 클라이언트 쪽 스크립트

이 자습서 소개에서 설명한 대로, 웹 컨트롤의 렌더링 된 `id` 특성은 종종 특정 HTML 요소를 프로그래밍 방식으로 참조를 클라이언트 쪽 스크립트에서 사용 됩니다. 다음 JavaScript에서 HTML 요소를 참조 하는 예를 들어 해당 `id` 모달 메시지 상자에 해당 값을 표시 합니다.


[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample14.cs)]

Asp.net에서 페이지는 없다는 것을 기억 명명 컨테이너, 렌더링된 된 HTML 요소를 포함 하지 마십시오 `id` 특성은 웹 컨트롤에 동일한 `ID` 속성 값입니다. 이 때문에 하드 코드에 캐시는 `id` JavaScript 코드에 특성 값입니다. 즉, 알고 있는 경우 액세스 하려는 `Age` 클라이언트 쪽 스크립트를 통해 텍스트 웹 컨트롤에 대 한 호출을 통해 이렇게 `document.getElementById("Age")`합니다.

이 방법의 문제는 마스터 페이지 (또는 다른 명명 컨테이너 컨트롤)를 사용 하는 경우 렌더링 된 HTML `id` 웹 컨트롤의와 다릅니다 `ID` 속성입니다. 브라우저를 통해 페이지를 방문 하는 실제 확인 하려면 소스를 볼 수 있습니다 프로그램 첫 번째 기울기 `id` 특성입니다. 렌더링 된 것을 알고 있다면 `id` 값 있습니다에 붙여 넣을 수에 대 한 호출 `getElementById` 클라이언트 쪽 스크립트를 통해 작업할 필요한 HTML 요소에 액세스 합니다. 이 방법은 특정 변경 내용 페이지의 컨트롤 계층 구조 때문에 적합 하지 않습니다는 또는로 변경는 `ID` 명명 컨트롤의 속성 변경 결과 `id` 함으로써 프로그램 JavaScript 코드를 깰 특성입니다.

다행 스럽게도 하는 `id` 렌더링 되는 특성 값은 웹 컨트롤을 통해 서버 쪽 코드에 액세스할 수 없으므로 [ `ClientID` 속성](https://msdn.microsoft.com/library/system.web.ui.control.clientid.aspx)합니다. 확인 하려면이 속성을 사용 해야는 `id` 특성 클라이언트 쪽 스크립트에 사용 되는 값입니다. 예를 들어, 페이지에는 JavaScript 함수를 추가 하는 호출의 값이 표시 됩니다는 `Age` 모달 메시지 상자에 텍스트 상자에 다음 코드를 추가 `Page_Load` 이벤트 처리기:


[!code-javascript[Main](control-id-naming-in-content-pages-cs/samples/sample15.js)]

값을 삽입 하는 위의 코드는 `Age` 하는 JavaScript 호출에 TextBox의 ClientID 속성 `getElementById`합니다. 브라우저를 통해이 페이지를 방문 하 고 HTML 소스를 볼 경우 다음 JavaScript 코드를 찾을 수 있습니다.


[!code-html[Main](control-id-naming-in-content-pages-cs/samples/sample16.html)]

알림 방법을 올바른 `id` 특성 값, `ctl00_MainContent_Age`에 대 한 호출 내에 표시 `getElementById`합니다. 이 값을 런타임 시 계산 되므로 이후 변경 페이지 컨트롤 계층 구조에 관계 없이 작동 합니다.

> [!NOTE]
> JavaScript 예제에는 단순히 올바르게 서버 컨트롤에서 렌더링 된 HTML 요소를 참조 하는 JavaScript 기능을 추가 하는 방법을 보여 줍니다. 이 함수를 사용 하거나 특정 사용자의 일부 동작에서 다소 문서를 로드 하는 경우 함수를 호출 하는 JavaScript 작성 해야 합니다. 자세한 내용은 다음에 대 한 관련 항목을 읽을 [클라이언트 쪽 스크립트 작업](https://msdn.microsoft.com/library/aa479302.aspx)합니다.


## <a name="summary"></a>요약

ASP.NET 서버 컨트롤의 역할을 명명 컨테이너에 영향을 주는 렌더링 된 특정 `id` 여 canvassed 컨트롤의 범위와 해당 하위 컨트롤의 값을 특성은 `FindControl` 메서드. 마스터 페이지와 관련 하 여 마스터 페이지 자체와 해당 ContentPlaceHolder 컨트롤은 명명 컨테이너입니다. 따라서 사용 하 여 콘텐츠 페이지 내에서 컨트롤을 프로그래밍 방식으로 참조를 좀 더 세이프 작업을 저장 해야 `FindControl`합니다. 이 자습서에서는 두 가지 기법을 검사 했습니다: ContentPlaceHolder 컨트롤로 드릴링 및 호출 해당 `FindControl` ; 메서드와 고유한 롤링 `FindControl` 모든 명명 컨테이너를 통해 검색 구현 해당 회귀적으로 검색 합니다.

웹 컨트롤 참조와 관련 하 여 명명 컨테이너 소개 하는 서버 쪽 문제 외에 클라이언트 쪽 문제가 있습니다. 명명 컨테이너 웹 컨트롤의 없으면에서 `ID` 속성 값 및 렌더링 `id` 특성 값은 동일한 합니다. 하지만 명명 컨테이너는 렌더링 된 추가 `id` 특성이 모두 포함 됩니다는 `ID` 웹 컨트롤 및 해당 컨트롤 계층의 상위 구조에 명명 컨테이너가의 값입니다. 웹 컨트롤을 사용 하 여으로 이러한 명명 문제는 중요 하지 `ClientID` 속성을 렌더링 된 `id` 특성 값에 클라이언트 쪽 스크립트입니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 마스터 페이지 및 `FindControl`](http://www.west-wind.com/WebLog/posts/5127.aspx)
- [동적 데이터 입력 사용자 인터페이스 만들기](https://msdn.microsoft.com/library/aa479330.aspx)
- [확장 메서드를 사용한 기본 형식 기능 확장](http://aspnet.4guysfromrolla.com/articles/120507-1.aspx)
- [방법: ASP.NET 마스터 페이지 콘텐츠를 참조 합니다.](https://msdn.microsoft.com/library/xxwa0ff0.aspx)
- [뜸 페이지: 팁, 요령 및 트랩](http://www.odetocode.com/articles/450.aspx)
- [클라이언트 쪽 스크립트 사용](https://msdn.microsoft.com/library/aa479302.aspx)

### <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 작성자 여러 ASP/ASP.NET 설명서와 4GuysFromRolla.com의 창립자의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 3.5 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. Scott에 도달할 수 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com) 또는에서 그의 블로그 통해 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Zack Jones 및 Suchi Barnerjee 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)합니다.

> [!div class="step-by-step"]
> [이전](urls-in-master-pages-cs.md)
> [다음](interacting-with-the-master-page-from-the-content-page-cs.md)
