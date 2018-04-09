---
uid: web-forms/overview/older-versions-getting-started/master-pages/multiple-contentplaceholders-and-default-content-cs
title: 여러 contentplaceholders 및 기본 콘텐츠 (C#) | Microsoft Docs
author: rick-anderson
description: 콘텐츠 자리 표시자의 기본 콘텐츠를 지정 하는 방법 뿐만 아니라 마스터 페이지에 여러 콘텐츠 자리 표시자를 추가 하는 방법을 검사 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/21/2008
ms.topic: article
ms.assetid: b9b9798b-027d-46cc-9636-473378e437ac
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/multiple-contentplaceholders-and-default-content-cs
msc.type: authoredcontent
ms.openlocfilehash: b60017c21b4cf45081893af08e68186009475fd2
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="multiple-contentplaceholders-and-default-content-c"></a>여러 contentplaceholders 및 기본 콘텐츠 (C#)
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_02_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_02_CS.pdf)

> 콘텐츠 자리 표시자의 기본 콘텐츠를 지정 하는 방법 뿐만 아니라 마스터 페이지에 여러 콘텐츠 자리 표시자를 추가 하는 방법을 검사 합니다.


## <a name="introduction"></a>소개

이전 자습서에서 검사 했습니다 마스터의 활성화 페이지 방식 ASP.NET 개발자가 일관 된 사이트 전체 레이아웃을 만들 수 있습니다. 마스터 페이지의 모든 해당 콘텐츠 페이지에 공통적으로 적용 되는 태그와 페이지 단위로 별로 사용자 지정할 수 있는 영역을 정의 합니다. 이전 자습서에서는 간단한 마스터 페이지를 만들었습니다 (`Site.master`)와 두 개의 콘텐츠 페이지 (`Default.aspx` 및 `About.aspx`). 마스터 페이지 라는 두 개의 contentplaceholders의 이루어져 `head` 및 `MainContent`에 위치 하는 `<head>` 요소와 Web Form 각각. 에 해당 하는 것에 대 한 태그 지정만 각 콘텐츠 페이지에 콘텐츠 컨트롤을 두 가지, 동안 `MainContent`합니다.

두 ContentPlaceHolder 제어에서 알 수 있듯이 `Site.master`, 마스터 페이지에는 여러 contentplaceholders의 포함 될 수 있습니다. 게다가, 마스터 페이지 ContentPlaceHolder 컨트롤에 대 한 기본 태그를 지정할 수 있습니다. 콘텐츠 페이지, 수 필요에 따라 자체 태그를 지정 하거나 기본 태그를 사용 합니다. 이 자습서에서는 여러 콘텐츠 컨트롤을 사용 하 여 마스터 페이지에서 확인을 ContentPlaceHolder 컨트롤의 기본 태그를 정의 하는 방법을 참조 하십시오.

## <a name="step-1-adding-additional-contentplaceholder-controls-to-the-master-page"></a>1 단계: 마스터 페이지에 추가 ContentPlaceHolder 컨트롤 추가

대부분의 웹 사이트 디자인 화면에서 페이지 단위로 별로 사용자 지정 된 여러 영역을 포함 합니다. `Site.master`마스터 페이지 이전 자습서에서 만든 포함 라는 웹 폼 내에서 단일 ContentPlaceHolder `MainContent`합니다. 특히이 ContentPlaceHolder는 내에 `mainContent` `<div>` 요소입니다.

그림 1에 나와 `Default.aspx` 브라우저를 통해 볼 때. 빨간색에서 원이 표시 된 영역에 해당 하는 페이지별 태그는 `MainContent`합니다.


[![원 안의 영역 영역을 보여 줍니다 현재 사용자 지정 가능한 페이지-기준](multiple-contentplaceholders-and-default-content-cs/_static/image2.png)](multiple-contentplaceholders-and-default-content-cs/_static/image1.png)

**그림 01**: 원 영역을 페이지 단위로 별로 영역 현재 사용자 지정이 가능한 보여 줍니다 ([전체 크기 이미지를 보려면 클릭](multiple-contentplaceholders-and-default-content-cs/_static/image3.png))


그림 1의 영역 외에 해야과 뉴스 아래에 있는 왼쪽된 열에 페이지 관련 항목을 추가 한다고 가정 섹션. 이렇게 하려면 마스터 페이지에 다른 ContentPlaceHolder 컨트롤을 추가 했습니다. 단계를 따르려면 열고는 `Site.master` 마스터 Visual Web Developer에서 페이지 및 다음 뉴스 섹션 다음 디자이너 도구 상자에서 ContentPlaceHolder 컨트롤을 끕니다. ContentPlaceHolder의 설정 `ID` 를 `LeftColumnContent`합니다.


[![마스터 페이지의 왼쪽된 열에 ContentPlaceHolder 컨트롤 추가](multiple-contentplaceholders-and-default-content-cs/_static/image5.png)](multiple-contentplaceholders-and-default-content-cs/_static/image4.png)

**그림 02**: ContentPlaceHolder 컨트롤 마스터 페이지의 왼쪽 열을 추가 ([전체 크기 이미지를 보려면 클릭](multiple-contentplaceholders-and-default-content-cs/_static/image6.png))


추가 하 여는 `LeftColumnContent` ContentPlaceHolder 마스터 페이지를 정의할 수 있습니다이 영역에 대 한 콘텐츠 페이지-기준 콘텐츠를 포함 하 여 페이지에서 컨트롤 `ContentPlaceHolderID` 로 설정 된 `LeftColumnContent`합니다. 2 단계에서에서이 프로세스를 살펴보겠습니다.

## <a name="step-2-defining-content-for-the-new-contentplaceholder-in-the-content-pages"></a>콘텐츠 페이지에서 새 ContentPlaceHolder에 대 한 콘텐츠를 정의 하는 2 단계:

Visual Web Developer 같은 콘텐츠를 자동으로 만듭니다는 웹 사이트를 새 콘텐츠 페이지에 추가 하면 선택 된 마스터 페이지에서 각 ContentPlaceHolder에 대 한 페이지에서 컨트롤입니다. 추가는 `LeftColumnContent` ContentPlaceHolder 1 단계 새 ASP.NET 페이지는 이제에서 가격 마스터 페이지에 세 개의 콘텐츠 컨트롤을 포함 합니다.

이 보여 주기 위해 명명 된 루트 디렉터리에 새 콘텐츠 페이지를 추가 `MultipleContentPlaceHolders.aspx` 에 바인딩되는 `Site.master` 마스터 페이지입니다. Visual Web Developer는 다음과 같은 선언적 태그가 포함 된이 페이지를 만듭니다.

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-cs/samples/sample1.aspx)]

일부 콘텐츠를 참조 하는 콘텐츠 컨트롤에 입력 된 `MainContent` contentplaceholders의 (`Content2`). 다음에 다음 태그를 추가 `Content3` 콘텐츠 컨트롤 (참조 하는 `LeftColumnContent` ContentPlaceHolder):

[!code-html[Main](multiple-contentplaceholders-and-default-content-cs/samples/sample2.html)]

이 태그를 추가한 후 브라우저를 통해 페이지를 방문 합니다. 태그에 배치 그림 3과 같이 `Content3` 콘텐츠 컨트롤 (빨간색 원) 뉴스 섹션 아래에 있는 왼쪽된 열에 표시 됩니다. 태그에 배치 `Content2` (파란색 원) 페이지의 오른쪽 부분에 표시 됩니다.


[![왼쪽된 열에는 이제 뉴스 섹션 아래에 있는 페이지 관련 내용을 포함](multiple-contentplaceholders-and-default-content-cs/_static/image8.png)](multiple-contentplaceholders-and-default-content-cs/_static/image7.png)

**그림 03**: The 왼쪽 열 이제 포함 페이지 관련 콘텐츠 아래에 뉴스 섹션 ([전체 크기 이미지를 보려면 클릭](multiple-contentplaceholders-and-default-content-cs/_static/image9.png))


### <a name="defining-content-in-existing-content-pages"></a>기존 콘텐츠 페이지의 내용 정의

새 콘텐츠 페이지를 자동으로 만들기 1 단계에서에서 추가 ContentPlaceHolder 컨트롤을 통합 합니다. 하지만 두 개의 기존 콘텐츠 분량- `About.aspx` 및 `Default.aspx` -콘텐츠 컨트롤에 대 한 없는 `LeftColumnContent` ContentPlaceHolder 합니다. 이 두 개의 기존 페이지에이 ContentPlaceHolder에 대 한 콘텐츠를 지정 하려면 콘텐츠 컨트롤을 직접 추가 해야 합니다.

대부분의 ASP.NET 웹 컨트롤과 달리 Visual 웹 개발자 도구 상자 콘텐츠 컨트롤 항목을 포함 하지 않습니다. 소스 뷰에 콘텐츠 컨트롤의 선언적 태그에 수동으로 입력할 수 있습니다 하지만 쉽고 빠르게 방법은 디자인 뷰를 사용 하는 것입니다. 열기는 `About.aspx` 페이지 및 디자인 뷰로 전환 합니다. 그림 4에서 알 수 있듯이는 `LeftColumnContent` ContentPlaceHolder 디자인 보기에 표시 됩니다. 즉, 표시 되는 제목 읽어 위로 마우스를 가져가면, 하는 경우: "LeftColumnContent (마스터)." 제목에 "Master"의 포함이이 ContentPlaceHolder에 대 한 페이지에 정의 된 콘텐츠 컨트롤이 임을 나타냅니다. 에 대 한 경우 처럼 ContentPlaceHolder에 대 한 콘텐츠 컨트롤 있으면 `MainContent`, 제목이 표시 됩니다: "*ContentPlaceHolderID* (사용자 지정)."

에 대 한 콘텐츠 컨트롤을 추가 하는 `LeftColumnContent` 를 ContentPlaceHolder `About.aspx`, ContentPlaceHolder의 스마트 태그를 확장 하 고 사용자 지정 콘텐츠 만들기 링크를 클릭 합니다.


[![디자인 뷰 About.aspx LeftColumnContent ContentPlaceHolder를 보여 줍니다.](multiple-contentplaceholders-and-default-content-cs/_static/image11.png)](multiple-contentplaceholders-and-default-content-cs/_static/image10.png)

**그림 04**: The 디자인 보기에 대 한 `About.aspx` 표시는 `LeftColumnContent` ContentPlaceHolder ([전체 크기 이미지를 보려면 클릭](multiple-contentplaceholders-and-default-content-cs/_static/image12.png))


사용자 지정 콘텐츠 만들기 링크를 클릭 하면에서는 오류가 발생 하는 데 필요한 콘텐츠 페이지 및 집합에서 컨트롤을 해당 `ContentPlaceHolderID` 속성 ContentPlaceHolder의을 `ID`합니다. 예를 들어 사용자 지정 콘텐츠 만들기 링크를 클릭 `LeftColumnContent` 의 영역 `About.aspx` 페이지에 다음 선언 태그를 추가 합니다.

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-cs/samples/sample3.aspx)]

### <a name="omitting-content-controls"></a>콘텐츠 컨트롤을 생략합니다.

ASP.NET에서 모든 콘텐츠 페이지 마스터 페이지에 정의 된 각 ContentPlaceHolder에 대 한 콘텐츠 컨트롤을 포함 하는 필요 하지 않습니다. 콘텐츠 컨트롤을 생략 하면 ASP.NET 엔진 마스터 페이지에서 ContentPlaceHolder 내에 정의 된 태그를 사용 합니다. 이 태그는 ContentPlaceHolder 라고 *기본 페이지* 되며 여기서 콘텐츠 일부 지역은 대부분의 페이지, 간에 공통적으로 적용 하지만 사용자 지정 해야 소수의 페이지에 대 한 시나리오에서 유용 합니다. 3 단계를 마스터 페이지에 지정 하 여 기본 콘텐츠를 탐색합니다.

현재 `Default.aspx` 에 대 한 두 개의 콘텐츠 컨트롤이 포함 된 `head` 및 `MainContent` contentplaceholders의;에 콘텐츠 컨트롤에 없는 `LeftColumnContent`합니다. 따라서, `Default.aspx` 렌더링 되는 `LeftColumnContent` ContentPlaceHolder의 기본 콘텐츠를 사용 합니다. 아직이 ContentPlaceHolder에 대 한 모든 기본 콘텐츠 정의 때문에이 영역에 없는 태그는 내보내집니다 한 순수 효과 합니다. 이 동작을 확인 하려면 방문 `Default.aspx` 브라우저를 통해 합니다. 그림 5에서 볼 수 있듯이 뉴스 섹션 아래에 있는 왼쪽된 열에 없는 태그가 내보내집니다.


[![LeftColumnContent ContentPlaceHolder에 대 한 콘텐츠는](multiple-contentplaceholders-and-default-content-cs/_static/image14.png)](multiple-contentplaceholders-and-default-content-cs/_static/image13.png)

**그림 05**: 콘텐츠 없음에 대해 렌더링 되는 `LeftColumnContent` ContentPlaceHolder ([전체 크기 이미지를 보려면 클릭](multiple-contentplaceholders-and-default-content-cs/_static/image15.png))


## <a name="step-3-specifying-default-content-in-the-master-page"></a>3 단계: 마스터 페이지의 기본 내용 지정

일부 웹 사이트 디자인 하나 또는 두 개의 예외를 제외 하 고 사이트의 모든 페이지에 대해 동일 콘텐츠인지 영역을 포함 합니다. 사용자 계정을 지원 웹 사이트를 고려해 야 합니다. 이러한 사이트 방문자를 사이트에 로그온 자격 증명를 입력할 수 있는 로그인 페이지를 필요 합니다. 로그인 프로세스를 촉진 하기 위해 웹 사이트 디자이너는 사용자가 명시적으로 로그인 페이지를 방문 하 여 필요 없이 로그인 할 수 있도록 모든 페이지의 왼쪽된 위 모서리에서 사용자 이름 및 암호 텍스트 상자를 포함할 수 있습니다. 이러한 사용자 이름 및 암호 입력란은 대부분의 페이지에 유용 하지만, 사용자의 자격 증명에 대 한 텍스트 상자에 이미 포함 하는 로그인 페이지에서 중복 됩니다.

이 디자인을 구현 하려면 마스터 페이지의 왼쪽된 위 모서리에서 ContentPlaceHolder 컨트롤을 만들 수 있습니다. 각 페이지의 맨 왼쪽된 위에 있는 사용자 이름 및 암호 텍스트 상자를 표시 하기 위해 필요에이 ContentPlaceHolder에 콘텐츠 컨트롤을 만들 하 고 필요한 인터페이스를 추가 합니다. 반면에 로그인 페이지이 ContentPlaceHolder이에 대 한 콘텐츠 컨트롤을 추가 하는 것을 생략 하거나 것 하거나 콘텐츠 해지기 정의 없는 태그로 제어 합니다. 이 방법의 단점은 (로그인 페이지)를 제외한 사이트에 추가 하는 모든 페이지에 사용자 이름 및 암호 텍스트 상자에 추가 해야 해야 한다는 점입니다. 이 문제에 대 한 요청입니다. We're를 페이지 또는 두 이러한 입력란을 추가 하려면 분실할 가능성도 또는 심각한 문제 우리 수 인터페이스를 구현 하지 올바르게 (아마도 2 개가 아닌 하나만 textbox 추가).

ContentPlaceHolder의 기본 콘텐츠도 사용자 이름 및 암호 텍스트 상자를 정의 하는 것이 좋습니다. 이렇게 함으로써만 하면 사용자 이름 및 암호 텍스트 상자를 표시 하지 않는 이러한 몇 가지 페이지에서이 기본 콘텐츠 재정의할 (로그인 페이지, 예를 들어). ContentPlaceHolder 컨트롤에 대해 지정 하 여 기본 콘텐츠를 설명 하기 위해 지금까지 설명한 시나리오를 구현 해 보겠습니다.

> [!NOTE]
> 이 자습서의 나머지 부분에서는 모든 페이지 하지만 로그인 페이지의 왼쪽된 열에서 로그인 인터페이스를 포함 하도록 웹 사이트를 업데이트 합니다. 그러나이 자습서는 사용자 계정을 지원 하기 위해 웹 사이트를 구성 하는 방법을 검사 하지 않습니다. 이 항목에 대 한 자세한 내용은 참조 내 [폼 인증, 권한 부여, 사용자 계정 및 역할](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md) 자습서입니다.


### <a name="adding-a-contentplaceholder-and-specifying-its-default-content"></a>ContentPlaceHolder는 추가 하 고 해당 기본 내용 지정

열기는 `Site.master` 왼쪽된 열 사이 다음 태그를 추가 하 고 마스터 페이지는 `DateDisplay` 레이블 및 단원 섹션:

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-cs/samples/sample4.aspx)]

이 태그를 추가한 후 그림 6 마스터 페이지의 디자인 뷰에서 비슷해야 합니다.


[![마스터 페이지에 로그인 컨트롤을 포함 됩니다.](multiple-contentplaceholders-and-default-content-cs/_static/image17.png)](multiple-contentplaceholders-and-default-content-cs/_static/image16.png)

**그림 06**: 로그인 컨트롤을 포함 하는 마스터 페이지 ([전체 크기 이미지를 보려면 클릭](multiple-contentplaceholders-and-default-content-cs/_static/image18.png))


이 ContentPlaceHolder `QuickLoginUI`, 기본 콘텐츠로 로그인 웹 컨트롤이 있습니다. Login 컨트롤에는 사용자에 게 자신의 사용자 이름과 로그인 단추와 암호를 요청 하는 사용자 인터페이스가 표시 됩니다. 다음 로그인 단추를 클릭 하면 Login 컨트롤 내부적으로 구성원 API에 대 한 사용자의 자격 증명을 확인 합니다. 실제로이 로그인 컨트롤을 사용 하려면 다음을 멤버 자격을 사용 하도록 사이트를 구성 해야 합니다. 이 항목은이 자습서;의 범위를 벗어납니다. 참조 내 [폼 인증, 권한 부여, 사용자 계정 및 역할](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md) 사용자 계정을 지 원하는 웹 응용 프로그램에 대 한 자세한 내용은 자습서입니다.

자유롭게 로그인 컨트롤의 동작이 나 모양을 사용자 지정할 수 있습니다. 두 가지 속성 설정: `TitleText` 및 `FailureAction`합니다. `TitleText` 기본값 "로그인"은으로, 속성 값, 컨트롤의 사용자 인터페이스의 위쪽에 표시 됩니다. 이 속성 설정 "로그인" 텍스트를 표시 하는 `<h3>` 요소입니다. `FailureAction` 속성은 사용자의 자격 증명이 잘못 된 경우 수행할 작업을 나타냅니다. 값이 기본값으로 `Refresh`, 동일한 페이지에 사용자를 유지 하 고 로그인 컨트롤 내에서 실패 메시지를 표시 합니다. 에 변경 했으므로 `RedirectToLoginPage`, 잘못 된 자격 증명 발생할 경우 로그인 페이지에 사용자를 전달 하 합니다. 사용자에 게 보낼 로그인 페이지에 로그인 페이지에는 추가 지침 및 옵션을 쉽게 왼쪽된 열에 맞지 않는 포함 될 수 있으므로 사용자가 실패 하면 다른 페이지에서 로그인 할 때 않겠습니다. 예를 들어 로그인 페이지를 암호를 잊은 경우를 검색 하거나 새 계정을 만드는 옵션을 포함할 수 있습니다.

### <a name="creating-the-login-page-and-overriding-the-default-content"></a>로그인 페이지를 만들고 기본 콘텐츠를 재정의 합니다.

완료 마스터 페이지와 다음 단계를 로그인 페이지를 만드는 것입니다. ASP.NET 페이지 라는 사이트의 루트 디렉터리에 추가 `Login.aspx`에 바인딩하기는 `Site.master` 마스터 페이지입니다. 에 정의 된 각는 contentplaceholders의 대 한, 이렇게 4 개의 콘텐츠 컨트롤이 있는 페이지를 만듭니다 `Site.master`합니다.

로그인 컨트롤을 추가 `MainContent` 콘텐츠 컨트롤을 합니다. 마찬가지로, 모든 콘텐츠를 자유롭게는 `LeftColumnContent` 영역입니다. 하지만에 대 한 콘텐츠 컨트롤에서 나갈 수 있는지를 확인는 `QuickLoginUI` ContentPlaceHolder 비어 있습니다. 이렇게 하면 하는 로그인 컨트롤 로그인 페이지의 왼쪽된 열에 나타나지 않습니다.

에 대 한 콘텐츠를 정의 하 고 나면는 `MainContent` 및 `LeftColumnContent` 영역, 로그인 페이지의 선언적 태그 다음과 같이 표시 됩니다.

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-cs/samples/sample5.aspx)]

그림 7 브라우저를 통해 볼 때이 페이지를 보여 줍니다. 이 페이지에 콘텐츠 컨트롤을 지정 하기 때문에 `QuickLoginUI` 마스터 페이지에 지정 된 기본 콘텐츠 재정의 ContentPlaceHolder 합니다. 한 순수 효과 Login 컨트롤 마스터 페이지의 디자인 뷰 (그림 6 참조)에 렌더링 되지 않습니다이 페이지에 표시 되도록 합니다.


[![로그인 페이지 Represses QuickLoginUI ContentPlaceHolder 기본 콘텐츠](multiple-contentplaceholders-and-default-content-cs/_static/image20.png)](multiple-contentplaceholders-and-default-content-cs/_static/image19.png)

**그림 07**: Represses의 로그인 페이지는 `QuickLoginUI` ContentPlaceHolder의 기본 콘텐츠 ([전체 크기 이미지를 보려면 클릭](multiple-contentplaceholders-and-default-content-cs/_static/image21.png))


### <a name="using-the-default-content-in-new-pages"></a>기본 콘텐츠를 사용 하 여 새 페이지에서

로그인 페이지를 제외한 모든 페이지의 왼쪽된 열에서 로그인 컨트롤을 표시 하려고 합니다. 이를 위해 로그인 페이지를 제외한 모든 콘텐츠 페이지에 콘텐츠 컨트롤을 생략 해야는 `QuickLoginUI` ContentPlaceHolder 합니다. 콘텐츠 컨트롤을 생략 하 여 ContentPlaceHolder의 기본 콘텐츠를 대신 사용 됩니다.

기존 콘텐츠 페이지- `Default.aspx`, `About.aspx`, 및 `MultipleContentPlaceHolders.aspx` -에 콘텐츠 컨트롤을 포함 하지 않는 `QuickLoginUI` ContentPlaceHolder 제어 하는 마스터 페이지에 추가 하기 전에 만들어진 때문에 있습니다. 따라서 이러한 기존 페이지 업데이트할 필요가 없습니다. 웹 사이트에 추가 하는 새 페이지에 콘텐츠 컨트롤을 포함 하는 반면는 `QuickLoginUI` ContentPlaceHolder 기본적으로 합니다. 따라서 이러한 제거 해야 해야 콘텐츠 (म 하지 않으려는 경우 재정의 ContentPlaceHolder의 기본 콘텐츠 로그인 페이지의 경우) 새 콘텐츠 페이지를 추가 하는 각 시간을 제어 합니다.

콘텐츠 컨트롤을 제거 하려면 수동으로 소스 뷰에서 해당 선언 태그를 삭제 하거나, 디자인 뷰에서 기본값 마스터의 콘텐츠 링크를 선택 하세요. 스마트 태그에서입니다. 콘텐츠 컨트롤을 제거 하는 방법 중 하나 효과 net 동일한 페이지를 생성 합니다.

그림 8 나와 `Default.aspx` 브라우저를 통해 볼 때. 이전에 설명한 대로 `Default.aspx` 에 대 한 선언적 태그-에 지정 된 두 개의 콘텐츠 컨트롤은만 `head` 되 고 다른 하나 `MainContent`합니다. 결과적으로 기본에 대 한 콘텐츠는 `LeftColumnContent` 및 `QuickLoginUI` contentplaceholders의 표시 됩니다.


[![기본 콘텐츠 LeftColumnContent 및 QuickLoginUI contentplaceholders의 대 한 표시 됩니다.](multiple-contentplaceholders-and-default-content-cs/_static/image23.png)](multiple-contentplaceholders-and-default-content-cs/_static/image22.png)

**그림 08**: The Default에 대 한 콘텐츠는 `LeftColumnContent` 및 `QuickLoginUI` contentplaceholders의 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](multiple-contentplaceholders-and-default-content-cs/_static/image24.png))


## <a name="summary"></a>요약

마스터 페이지에는 임의 개수의 contentplaceholders의 ASP.NET 마스터 페이지 모델을 사용 합니다. 더구나 contentplaceholders의 포함 있다는 해당 하는 경우에 내보내집니다 기본 콘텐츠를 콘텐츠 콘텐츠 페이지에 컨트롤을 합니다. 이 자습서에서는 마스터 페이지에 추가 ContentPlaceHolder 컨트롤을 포함 하는 방법과 신규 및 기존 ASP.NET 페이지에서 이러한 새 contentplaceholders의 대 한 콘텐츠 컨트롤을 정의 하는 방법에 살펴보았습니다. 또한 살펴보았습니다 기본을 지정 하는 ContentPlaceHolder의 콘텐츠는 그렇지 않으면 사용자 지정 해야 하는 페이지의 일부만 특정 지역 내에서 콘텐츠를 표준화 하는 위치는 시나리오에서 유용 합니다.

다음 자습서에서는 살펴봅니다는 `head` 더 자세하게에서 ContentPlaceHolder을 선언적으로 또는 프로그래밍 방식으로 페이지 단위로 별로 제목, 메타 태그 및 기타 HTML 헤더를 정의 하는 방법을 표시 합니다.

만족도 매우 프로그래밍!

### <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 작성자 여러 ASP/ASP.NET 설명서와 4GuysFromRolla.com의 창립자의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 3.5 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. Scott에 도달할 수 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com) 또는에서 그의 블로그 통해 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Suchi Banerjee 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)합니다.

> [!div class="step-by-step"]
> [이전](creating-a-site-wide-layout-using-master-pages-cs.md)
> [다음](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)
