---
uid: web-forms/overview/older-versions-getting-started/master-pages/multiple-contentplaceholders-and-default-content-vb
title: 여러 ContentPlaceHolders 및 기본 콘텐츠 (VB) | Microsoft Docs
author: rick-anderson
description: 마스터 페이지에 여러 콘텐츠 자리 표시자를 추가 하는 방법 뿐만 아니라 콘텐츠 자리 표시자에 기본 콘텐츠를 지정 하는 방법을 검사 합니다.
ms.author: aspnetcontent
ms.date: 05/21/2008
ms.assetid: 866a7177-6884-451e-88f4-c934b1dd1af5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/multiple-contentplaceholders-and-default-content-vb
msc.type: authoredcontent
ms.openlocfilehash: 98cb78e03f9f7aff4a36625416188aba04512f6a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37839702"
---
<a name="multiple-contentplaceholders-and-default-content-vb"></a>여러 ContentPlaceHolders 및 기본 콘텐츠 (VB)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_02_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_02_VB.pdf)

> 마스터 페이지에 여러 콘텐츠 자리 표시자를 추가 하는 방법 뿐만 아니라 콘텐츠 자리 표시자에 기본 콘텐츠를 지정 하는 방법을 검사 합니다.


## <a name="introduction"></a>소개

이전 자습서에서 어떻게 마스터 페이지 사용 검사할 ASP.NET 개발자가 일관 된 사이트 전체 레이아웃을 만들 수 있습니다. 마스터 페이지는 모든 콘텐츠 페이지에 공통적으로 적용 되는 태그 및 페이지 별로 별로 사용자 지정할 수 있는 영역을 정의 합니다. 이전 자습서에서 만든 간단한 마스터 페이지 (`Site.master`) 및 두 개의 콘텐츠 페이지 (`Default.aspx` 및 `About.aspx`). 마스터 페이지 라는 두 ContentPlaceHolders 이루어져 `head` 및 `MainContent`에 있는 것을 `<head>` 요소 및 Web Form을 각각. 에 해당 하는 것에 대 한 태그 처리 된 동안 콘텐츠 페이지를 두 콘텐츠 컨트롤에만 지정한 `MainContent`합니다.

두 ContentPlaceHolder 컨트롤을 통해 볼 수 있듯이 `Site.master`, 마스터 페이지에는 여러 ContentPlaceHolders 포함 될 수 있습니다. 게다가 마스터 페이지 ContentPlaceHolder 컨트롤에 대 한 기본 태그를 지정할 수 있습니다. 콘텐츠 페이지 그런 다음 수 필요에 따라 자체 태그를 지정 또는 기본 태그를 사용 합니다. 이 자습서에서는 여러 콘텐츠 컨트롤을 사용 하 여 마스터 페이지에서 확인 하 고 ContentPlaceHolder 컨트롤의 기본 태그를 정의 하는 방법을 참조 하세요.

## <a name="step-1-adding-additional-contentplaceholder-controls-to-the-master-page"></a>1 단계: 마스터 페이지에 추가 ContentPlaceHolder 컨트롤 추가

많은 웹 사이트의 디자인 화면에서 페이지 단위로 사용자 지정 된 여러 영역을 포함 합니다. `Site.master`를 이전 자습서에서 만든 마스터 페이지 라는 웹 폼 내에서 단일 ContentPlaceHolder 포함 `MainContent`합니다. 특히이 ContentPlaceHolder 내에 위치한 합니다 `mainContent` `<div>` 요소입니다.

그림 1에 나와 `Default.aspx` 브라우저를 통해 볼 때. 빨간색 원이 표시 된 지역은 해당 하는 페이지별 태그 `MainContent`합니다.


[![원 안의 지역 영역을 보여 줍니다 현재 사용자 지정 가능한 페이지-기준](multiple-contentplaceholders-and-default-content-vb/_static/image2.png)](multiple-contentplaceholders-and-default-content-vb/_static/image1.png)

**그림 01**: 원 지역 페이지-기준 영역 현재 사용자 지정이 가능한 보여 줍니다 ([큰 이미지를 보려면 클릭](multiple-contentplaceholders-and-default-content-vb/_static/image3.png))


그림 1에 표시 된 지역 외에 해야 단원 및 뉴스를 아래 왼쪽된 열에 페이지별 항목 추가 imagine 섹션입니다. 이렇게 하려면 마스터 페이지에 다른 각각의 ContentPlaceHolder 컨트롤로 추가 합니다. 자습서에 따라 엽니다는 `Site.master` 마스터 Visual Web Developer에서 페이지 및 뉴스 섹션 뒤 디자이너 도구 상자에서는 각각의 ContentPlaceHolder 컨트롤로 놓습니다. 설정의 ContentPlaceHolder `ID` 에 `LeftColumnContent`입니다.


[![마스터 페이지의 왼쪽된 열에는 각각의 ContentPlaceHolder 컨트롤로 추가](multiple-contentplaceholders-and-default-content-vb/_static/image5.png)](multiple-contentplaceholders-and-default-content-vb/_static/image4.png)

**그림 02**: 마스터 페이지의 왼쪽 열에는 각각의 ContentPlaceHolder 컨트롤로 추가 ([큰 이미지를 보려면 클릭](multiple-contentplaceholders-and-default-content-vb/_static/image6.png))


추가 합니다 `LeftColumnContent` 마스터 페이지에 ContentPlaceHolder를 정의할 수 있습니다이 영역에 대 한 콘텐츠 페이지-기준 콘텐츠를 포함 하 여 페이지에서 컨트롤 `ContentPlaceHolderID` 로 설정 된 `LeftColumnContent`합니다. 2 단계에서에서이 프로세스를 살펴봅니다.

## <a name="step-2-defining-content-for-the-new-contentplaceholder-in-the-content-pages"></a>2 단계: 콘텐츠 페이지에서 새 ContentPlaceHolder에 대 한 콘텐츠 정의

Visual Web Developer는 콘텐츠를 자동으로 만듭니다 새 콘텐츠 페이지에 웹 사이트를 추가할 때 각 ContentPlaceHolder 선택한 마스터 페이지에 대 한 페이지의 컨트롤입니다. 추가한 경우에 `LeftColumnContent` ContentPlaceHolder 단계 1에서 새 ASP.NET 페이지는 이제 마스터 페이지에 있는 세 가지 콘텐츠 컨트롤.

를 설명 하기 위해이 명명 된 루트 디렉터리에 새 콘텐츠 페이지를 추가 `MultipleContentPlaceHolders.aspx` 에 바인딩되는 `Site.master` 마스터 페이지입니다. Visual Web Developer 다음 선언적 태그를 사용 하 여이 페이지를 만듭니다.

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample1.aspx)]

참조 하는 콘텐츠 컨트롤에 일부 콘텐츠를 입력 합니다 `MainContent` ContentPlaceHolders (`Content2`). 다음으로, 다음 태그를 추가 합니다 `Content3` 콘텐츠 컨트롤 (참조 하는 `LeftColumnContent` ContentPlaceHolder):

[!code-html[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample2.html)]

이 태그를 추가한 후 브라우저를 통해 페이지를 방문 합니다. 그림 3 태그에 배치 합니다 `Content3` 콘텐츠 컨트롤의 왼쪽된 열 (빨간색 원으로 표시) 뉴스 섹션 아래에 표시 됩니다. 태그에 배치 `Content2` (파란색에서 원으로 표시) 페이지의 오른쪽 부분에 표시 됩니다.


[![왼쪽된 열에는 이제 뉴스 섹션 아래에 있는 특정 페이지 콘텐츠](multiple-contentplaceholders-and-default-content-vb/_static/image8.png)](multiple-contentplaceholders-and-default-content-vb/_static/image7.png)

**그림 03**: The 왼쪽 열 이제 포함 페이지별 콘텐츠 아래에 뉴스 섹션 ([큰 이미지를 보려면 클릭](multiple-contentplaceholders-and-default-content-vb/_static/image9.png))


### <a name="defining-content-in-existing-content-pages"></a>기존 콘텐츠 페이지에서 콘텐츠 정의

새 콘텐츠 페이지를 자동으로 만들기 1 단계에서에서 추가한 ContentPlaceHolder 컨트롤을 통합 합니다. 하지만 두 개의 기존 콘텐츠 페이지- `About.aspx` 하 고 `Default.aspx` -에 콘텐츠 컨트롤에 없는 `LeftColumnContent` ContentPlaceHolder 합니다. 이러한 두 기존 페이지에서이 ContentPlaceHolder에 대 한 콘텐츠를 지정 하려면 콘텐츠 컨트롤을 직접 추가 해야 합니다.

대부분의 ASP.NET 웹 컨트롤과 달리 Visual Web Developer 도구 상자 콘텐츠 컨트롤 항목을 포함 하지 않습니다. 소스 보기에 콘텐츠 컨트롤의 선언적 태그에 수동으로 입력할 수 있습니다 하지만 쉽고 빠르게 방법은 디자인 뷰를 사용 하는 것입니다. 열기는 `About.aspx` 페이지 및 디자인 뷰로 전환 합니다. 그림 4에서 알 수 있듯이는 `LeftColumnContent` ContentPlaceHolder 디자인 뷰에서 표시; 위에 가져가면 표시 되는 제목 읽습니다: "LeftColumnContent (마스터)." 제목에 "Master"의 포함이이 ContentPlaceHolder에 대 한 페이지에 정의 된 콘텐츠 컨트롤이 있음을 나타냅니다. 경우와 같이 ContentPlaceHolder에 대 한 콘텐츠 컨트롤을 있으면 `MainContent`, 제목 읽기 됩니다: "*ContentPlaceHolderID* (사용자 지정)."

에 대 한 콘텐츠 컨트롤을 추가 하는 `LeftColumnContent` ContentPlaceHolder를 `About.aspx`, ContentPlaceHolder의 스마트 태그 확장 및 사용자 지정 콘텐츠 만들기 링크를 클릭 합니다.


[![About.aspx의 디자인 뷰 LeftColumnContent ContentPlaceHolder를 보여 줍니다.](multiple-contentplaceholders-and-default-content-vb/_static/image11.png)](multiple-contentplaceholders-and-default-content-vb/_static/image10.png)

**그림 04**:에 대 한 디자인 뷰 `About.aspx` 표시는 `LeftColumnContent` ContentPlaceHolder ([클릭 하 여 큰 이미지 보기](multiple-contentplaceholders-and-default-content-vb/_static/image12.png))


필요한 사용자 지정 콘텐츠 만들기 링크를 클릭 하면 생성 콘텐츠 집합 페이지의 컨트롤을 해당 `ContentPlaceHolderID` ContentPlaceHolder의 속성 `ID`합니다. 예를 들어, 사용자 지정 콘텐츠 만들기 링크를 클릭 `LeftColumnContent` 지역에 `About.aspx` 페이지로 다음 선언적 태그를 추가 합니다.

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample3.aspx)]

### <a name="omitting-content-controls"></a>콘텐츠 컨트롤을 생략합니다.

ASP.NET 마스터 페이지에 정의 된 각 ContentPlaceHolder에 대 한 모든 콘텐츠 페이지에 콘텐츠 컨트롤이 포함 되어는 필요 하지 않습니다. 콘텐츠 컨트롤을 생략 하면 ASP.NET 엔진 마스터 페이지에 ContentPlaceHolder 내에 정의 된 태그를 사용 합니다. 이 태그는 ContentPlaceHolder의 이라고 *콘텐츠를 기본* 콘텐츠 공통적으로 적용 대부분 페이지의 일부 지역에 있지만 해야 하는 소수의 페이지에 대 한 사용자 지정 시나리오에 유용 합니다. 3 단계에서는 마스터 페이지에 지정 하 여 기본 콘텐츠를 살펴봅니다.

현재 `Default.aspx` 에 대 한 두 콘텐츠 컨트롤을 포함 합니다 `head` 및 `MainContent` ContentPlaceHolders;에 대 한 콘텐츠 제어 되지 않은 `LeftColumnContent`합니다. 결과적으로, `Default.aspx` 렌더링 되는 `LeftColumnContent` ContentPlaceHolder의 기본 콘텐츠는 데 사용 됩니다. 에서는 아직이 ContentPlaceHolder에 대 한 기본 콘텐츠 정의 최종적 이므로이 영역에 대 한 태그가 없음을 내보내집니다는 합니다. 이 동작을 확인 하려면 방문 `Default.aspx` 브라우저를 통해. 그림 5에서 알 수 있듯이, 뉴스 섹션 아래의 왼쪽된 열에 태그가 없음을 내보내집니다.


[![LeftColumnContent ContentPlaceHolder에 대 한 콘텐츠는](multiple-contentplaceholders-and-default-content-vb/_static/image14.png)](multiple-contentplaceholders-and-default-content-vb/_static/image13.png)

**그림 05**: 콘텐츠 없음에 대해 렌더링 되는 `LeftColumnContent` ContentPlaceHolder ([클릭 하 여 큰 이미지 보기](multiple-contentplaceholders-and-default-content-vb/_static/image15.png))


## <a name="step-3-specifying-default-content-in-the-master-page"></a>3 단계: 마스터 페이지에서 기본 콘텐츠 지정

일부 웹 사이트 디자인에는 해당 콘텐츠를 하나 또는 두 개의 예외를 제외 하 고 사이트의 모든 페이지에 대해 동일 지역 포함 됩니다. 웹 사이트를 사용자 계정을 지 원하는 것이 좋습니다. 이러한 사이트 방문자가 사이트에 로그온 자격 증명을 입력할 수는 있는 로그인 페이지에 필요 합니다. 로그인 프로세스를 신속 하 게 웹 사이트 디자이너에서 사용자를 명시적으로 로그인 페이지를 방문할 필요 없이 로그인 할 수 있도록 모든 페이지의 왼쪽된 위 모서리에서 사용자 이름 및 암호 텍스트 상자를 포함할 수 있습니다. 이러한 사용자 이름 및 암호 텍스트 상자는 대부분의 페이지에 유용 하지만, 사용자의 자격 증명에 대 한 텍스트 상자에 이미 있는 로그인 페이지에서 중복 됩니다.

이 디자인을 구현 하려면 마스터 페이지의 왼쪽된 위 모퉁이에 각각의 ContentPlaceHolder 컨트롤로 만들 수 있습니다. 각 페이지의 왼쪽된 위 모서리에서 사용자 이름 및 암호 텍스트 상자를 표시 하는 데 필요한이 ContentPlaceHolder에 콘텐츠 컨트롤을 만드는 필요한 인터페이스를 추가 합니다. 로그인 페이지에서 다른 한편으로이 ContentPlaceHolder 콘텐츠 컨트롤을 추가 하는 것을 생략 하거나는 만들거나는 콘텐츠 정의 없는 태그를 사용 하 여 컨트롤입니다. 이 방법의 단점은 (로그인 페이지) 제외 하 고 사이트에 추가 하는 모든 페이지에 사용자 이름 및 암호 텍스트 상자를 추가 해야 합니다. 이 문제에 대 한 요청입니다. 페이지 또는 두 이러한 텍스트 상자를 추가 해야 할 것, 게다가 우리가 수 인터페이스를 구현 하지 올바르게 (아마도 두 개가 아닌 하나만 텍스트 상자 추가).

ContentPlaceHolder의 기본 콘텐츠로 사용자 이름 및 암호 텍스트 상자를 정의 하는 것이 좋습니다. 이렇게만 하면 재정의 된 사용자 이름 및 암호 텍스트 상자를 표시 하지 않는 몇 가지 해당 페이지에서이 기본 콘텐츠 (로그인 페이지 예를 들어). ContentPlaceHolder 컨트롤에 대해 지정 하 여 기본 콘텐츠를 보여 주기 위해 위에서 설명한 시나리오를 구현 해 보겠습니다.

> [!NOTE]
> 이 자습서의 나머지 모든 페이지가 하지만 로그인 페이지의 왼쪽된 열에는 로그인 인터페이스를 포함 하도록 웹 사이트를 업데이트 합니다. 그러나이 자습서에서는 사용자 계정을 지원 하기 위해 웹 사이트를 구성 하는 방법에 있는지 확인 하지 않습니다. 이 항목에 대 한 자세한 내용은 참조 내 [폼 인증, 권한 부여, 사용자 계정 및 역할](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md) 자습서입니다.


### <a name="adding-a-contentplaceholder-and-specifying-its-default-content"></a>ContentPlaceHolder를 추가 하 고 해당 기본 콘텐츠를 지정 합니다.

엽니다는 `Site.master` 마스터 페이지 및 왼쪽된 열 사이 다음 태그를 추가 합니다 `DateDisplay` 레이블과 단원 섹션:

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample4.aspx)]

이 태그를 추가한 후 마스터 페이지의 디자인 뷰에서 그림 6과 유사 합니다.


[![로그인 컨트롤을 포함 하는 마스터 페이지](multiple-contentplaceholders-and-default-content-vb/_static/image17.png)](multiple-contentplaceholders-and-default-content-vb/_static/image16.png)

**그림 06**: 로그인 컨트롤을 포함 하는 마스터 페이지 ([큰 이미지를 보려면 클릭](multiple-contentplaceholders-and-default-content-vb/_static/image18.png))


이 ContentPlaceHolder `QuickLoginUI`, 로그인 웹 컨트롤이 기본 콘텐츠로 사용 합니다. 로그인 컨트롤은 사용자에 게 사용자 이름과 로그인 단추와 함께 암호를 요구 하는 사용자 인터페이스를 나타냅니다. 로그인 단추를 클릭 하면 로그인 컨트롤이 멤버 자격 API에 대 한 사용자의 자격 증명 내부적으로 유효성을 검사 합니다. 실제로이 로그인 컨트롤을 사용 하려면 한 멤버 자격을 사용 하도록 사이트를 구성 해야 합니다. 이 항목에서는이 자습서의 범위를 벗어납니다. 참조 내 [폼 인증, 권한 부여, 사용자 계정 및 역할](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md) 사용자 계정을 지 원하는 웹 응용 프로그램에 대 한 자세한 내용은 자습서입니다.

자유롭게 로그인 컨트롤의 동작 또는 모양을 사용자 지정할 수 있습니다. 두 가지 속성 설정: `TitleText` 고 `FailureAction`입니다. `TitleText` 컨트롤의 사용자 인터페이스의 맨 위에 있는 "Log In"으로 기본값이 있는 속성 값이 표시 됩니다. 이 속성 설정으로 텍스트를 "로그인"을 표시 하는 `<h3>` 요소입니다. `FailureAction` 속성 사용자의 자격 증명이 잘못 된 경우 수행할 작업을 나타냅니다. 값이 기본값으로 `Refresh`, 동일한 페이지에 사용자를 유지 하 고 로그인 컨트롤 내에서 오류 메시지를 표시 합니다. 되도록 변경 했으므로 `RedirectToLoginPage`, 잘못 된 자격 증명 시 로그인 페이지로 사용자를 전송 하는 합니다. 로그인 페이지에는 추가 지침 및 옵션을 쉽게 왼쪽된 열에 맞지 않는 포함 될 수 있으므로 사용자가 실패 하면 다른 페이지에서 로그인을 시도 하는 경우 해당 사용자를 로그인 페이지로 전송 싶습니다. 예를 들어, 로그인 페이지는 암호를 잊은 경우를 검색 하거나 새 계정을 만드는 옵션을 포함할 수 있습니다.

### <a name="creating-the-login-page-and-overriding-the-default-content"></a>로그인 페이지를 만들고 기본 콘텐츠를 재정의 합니다.

다음 단계 완료 마스터 페이지를 사용 하 여 로그인 페이지를 만드는 것입니다. ASP.NET 페이지 라는 사이트의 루트 디렉터리에 추가 `Login.aspx`를 바인딩하지는 `Site.master` 마스터 페이지입니다. 에 정의 된 ContentPlaceHolders 마다 하나씩, 이렇게 네 가지 콘텐츠 컨트롤을 사용 하 여 페이지를 만듭니다 `Site.master`합니다.

로그인 컨트롤을 추가 합니다 `MainContent` 콘텐츠 컨트롤입니다. 마찬가지로, 모든 콘텐츠를 자유롭게는 `LeftColumnContent` 지역입니다. 그러나 콘텐츠 컨트롤을 유지 해야 합니다 `QuickLoginUI` ContentPlaceHolder 비어 있습니다. 이렇게 하면 로그인 컨트롤이 로그인 페이지의 왼쪽된 열에 표시 되지 않습니다.

에 대 한 콘텐츠를 정의한 후 합니다 `MainContent` 및 `LeftColumnContent` 지역 로그인 페이지의 선언적 태그는 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample5.aspx)]

그림 7에서는 브라우저를 통해 볼 때이 페이지를 보여 줍니다. 이 페이지에 대 한 콘텐츠 컨트롤을 지정 하기 때문에 `QuickLoginUI` ContentPlaceHolder, 마스터 페이지에 지정 된 기본 내용을 재정의 합니다. Net은 Login 컨트롤 마스터 페이지의 디자인 뷰 (그림 6 참조)에 렌더링 되지 않습니다이 페이지에 표시 되도록 합니다.


[![로그인 페이지 Represses QuickLoginUI ContentPlaceHolder의 기본 콘텐츠](multiple-contentplaceholders-and-default-content-vb/_static/image20.png)](multiple-contentplaceholders-and-default-content-vb/_static/image19.png)

**그림 07**:의 로그인 페이지 Represses 합니다 `QuickLoginUI` ContentPlaceHolder의 기본 콘텐츠 ([클릭 하 여 큰 이미지 보기](multiple-contentplaceholders-and-default-content-vb/_static/image21.png))


### <a name="using-the-default-content-in-new-pages"></a>새 페이지에서 기본 콘텐츠를 사용 하 여

로그인 페이지를 제외한 모든 페이지의 왼쪽된 열에서 로그인 컨트롤을 표시 하려고 합니다. 이 위해 로그인 페이지를 제외 하 고 모든 콘텐츠 페이지에 대 한 콘텐츠 컨트롤을 생략 해야 합니다 `QuickLoginUI` ContentPlaceHolder 합니다. 콘텐츠 컨트롤을 생략 하 여 ContentPlaceHolder의 기본 콘텐츠를 대신 사용 됩니다.

기존 콘텐츠 페이지- `Default.aspx`, `About.aspx`, 및 `MultipleContentPlaceHolders.aspx` -에 대 한 콘텐츠 컨트롤을 포함 하지 마십시오 `QuickLoginUI` 마스터 페이지에는 각각의 ContentPlaceHolder 컨트롤로 추가 하기 전에 생성 된 때문입니다. 따라서 이러한 기존 페이지 업데이트할 필요가 없습니다. 그러나 웹 사이트에 추가 하는 새 페이지에 콘텐츠 컨트롤을 포함 합니다 `QuickLoginUI` ContentPlaceHolder를 기본적으로 합니다. 따라서 반드시이 제거 해야 콘텐츠에서는 없다면 추가 하는 새 콘텐츠 페이지 (로그인 페이지의 경우와 같이 ContentPlaceHolder의 기본 콘텐츠를 재정의 하려면 원하는) 각 시간을 제어 합니다.

콘텐츠 컨트롤을 제거 하려면 수동으로 소스 뷰에서 해당 선언적 태그를 삭제 하거나, 디자인 뷰에서 마스터의 콘텐츠 링크를 기본값으로 선택 스마트 태그에서입니다. 콘텐츠 컨트롤을 제거 하는 방법 중 하나 효과 net 동일한 페이지를 생성 합니다.

그림 8 나와 `Default.aspx` 브라우저를 통해 볼 때. 이전에 설명한 대로 `Default.aspx` 에 대 한 선언적 태그-에 지정 된 두 콘텐츠 컨트롤에만 `head` 개와 `MainContent`합니다. 결과적으로 기본에 대 한 콘텐츠를 `LeftColumnContent` 고 `QuickLoginUI` ContentPlaceHolders 표시 됩니다.


[![표시 되는 기본 콘텐츠 LeftColumnContent 및 QuickLoginUI ContentPlaceHolders는](multiple-contentplaceholders-and-default-content-vb/_static/image23.png)](multiple-contentplaceholders-and-default-content-vb/_static/image22.png)

**그림 08**: The Default에 대 한 콘텐츠를 `LeftColumnContent` 하 고 `QuickLoginUI` ContentPlaceHolders 표시 됩니다 ([클릭 하 여 큰 이미지 보기](multiple-contentplaceholders-and-default-content-vb/_static/image24.png))


## <a name="summary"></a>요약

마스터 페이지에는 임의 개수의 ContentPlaceHolders ASP.NET 마스터 페이지 모델을 허용합니다. 게다가 ContentPlaceHolders 포함 기본 콘텐츠는 해당 하는 경우에 내보내집니다. 콘텐츠는 콘텐츠 페이지의 컨트롤입니다. 이 자습서에서는 마스터 페이지에서 추가 ContentPlaceHolder 컨트롤을 포함 하는 방법 및 이러한 새 ContentPlaceHolders 신규 및 기존 ASP.NET 페이지에 대 한 콘텐츠 컨트롤을 정의 하는 방법에 살펴보았습니다. 살펴봤습니다 기본값 지정을 ContentPlaceHolder에서 콘텐츠를 그렇지 않으면 사용자 지정 해야 하는 페이지의 일부만 특정 지역 내에서 콘텐츠를 표준화 하는 위치 하는 시나리오에서 유용 합니다.

다음 자습서에서는 검토를 `head` 자세히 ContentPlaceHolder을 선언적으로 프로그래밍 방식으로 제목, 메타 태그 및 기타 HTML 헤더 페이지 별로 개별로 정의 하는 방법을 확인 합니다.

즐거운 프로그래밍!

### <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 작성자의 여러 ASP/ASP.NET 서적과 4GuysFromRolla.com의 설립자 이며, 왔습니다 Microsoft 웹 기술을 1998 합니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 3.5 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. Scott에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com) 통하거나 저자의 블로그 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Suchi Banerjee 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)합니다.

> [!div class="step-by-step"]
> [이전](creating-a-site-wide-layout-using-master-pages-vb.md)
> [다음](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md)
