---
uid: web-forms/overview/older-versions-getting-started/master-pages/creating-a-site-wide-layout-using-master-pages-cs
title: 마스터 페이지 (C#)를 사용 하 여 사이트 전체 레이아웃 만들기 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 기본 사항 마스터 페이지를 보여 줍니다. 즉, 마스터 페이지 있을까요 하나 마스터 페이지를 만들고, cr은 어떻게 콘텐츠 자리 표시자를 이란...
ms.author: riande
ms.date: 05/21/2008
ms.assetid: 78f8d194-03b9-44a5-8255-90e7cd1c2ee1
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/creating-a-site-wide-layout-using-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 3bdb533c1cb724d57152e676a75af8067a6828d8
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824075"
---
<a name="creating-a-site-wide-layout-using-master-pages-c"></a>마스터 페이지 (C#)를 사용 하 여 사이트 전체 레이아웃 만들기
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_01_CS.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_01_CS.pdf)

> 이 자습서에서는 기본 사항 마스터 페이지를 보여 줍니다. 즉, 마스터 페이지, 마스터 페이지를 만들려면지 않습니다 어떻게 하나 콘텐츠 자리 표시자 무엇지 않습니다 하나 만드는 방법을 수정 하는 방법을 마스터 페이지를 자동으로 반영 됩니다 해당 연결 된 콘텐츠 페이지의 마스터 페이지를 사용 하는 ASP.NET 페이지입니다.


## <a name="introduction"></a>소개

잘 디자인 된 웹 사이트의 하나의 특성에는 일관성 있는 사이트 전체 페이지 레이아웃입니다. www.asp.net 웹 사이트를 예로 들어 보겠습니다. 이 문서 작성 당시 모든 페이지에 페이지의 아래쪽과 위쪽에 있는 동일한 콘텐츠 그림 1에서 볼 수 있듯이 각 페이지의 맨 Microsoft 커뮤니티의 목록이 있는 회색 막대를 표시 합니다. 사이트 로고는 사이트 번역도 마쳤고, 언어 및 core 섹션의 목록 아래에: 홈, 시작, 학습, 다운로드 및 등입니다. 마찬가지로 페이지의 맨 아래 www.asp.net, 저작권, 개인정보취급방침 대 한 링크에 광고 정보를 포함 합니다.


[![모든 페이지에 걸쳐 일관 된 모양과 느낌을 사용 하는 www.asp.net 웹 사이트](creating-a-site-wide-layout-using-master-pages-cs/_static/image2.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image1.png)

<strong>그림 01</strong>: www.asp.net 웹 사이트에는 일관성 확인 및 모든 페이지에서 느낌 ([큰 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-cs/_static/image3.png))


잘 설계 된 사이트의 다른 특성은 사이트의 모양을 변경할 수 있는 간편 하 게 합니다. 그림 1은 2008 년 3 월을 기준으로 www.asp.net 홈 페이지를 보여 줍니다 않지만 이제 사이의이 자습서의이 게시 모양 및 느낌과 변경 될 수 있습니다. 아마도 맨 위에 있는 메뉴 항목은 MVC 프레임 워크에 대 한 새 섹션을 포함 하도록 확장 됩니다. 또는 아마도 다른 색, 글꼴 및 레이아웃을 사용 하 여 근본적으로 새로운 디자인의 소개 해제 됩니다. 전체 사이트에 이러한 변경 내용을 적용 수천 개의 사이트를 구성 하는 웹 페이지를 수정 하지 않아도 되는 빠르고 간단한 프로세스 여야 합니다.

ASP.NET에서 사이트 전체 페이지 템플릿 만들기가 사용 하 여 가능한 *마스터 페이지*합니다. 마스터 페이지는 특별 한 유형의 모든 간에 공통 되는 태그를 정의 하는 ASP.NET 페이지 말해 *콘텐츠 페이지는* 콘텐츠 페이지에서 콘텐츠 페이지 별로 사용자 지정할 수 있는 지역 뿐만 아니라 합니다. (콘텐츠 페이지는 마스터 페이지에 바인딩되는 ASP.NET 페이지입니다.) 마스터 페이지의 레이아웃 또는 서식을 변경 될 때마다 모든 해당 콘텐츠 페이지의 출력 마찬가지로 즉시 업데이트 됩니다, 업데이트 및 단일 파일 (즉, 마스터 페이지)를 배포 하는 것 만큼 쉽습니다 사이트 전체 모양을 변경 내용을 적용 수 있습니다.

마스터 페이지를 사용 하 여 탐색 하는 자습서 시리즈의 첫 번째 자습서입니다. 이 자습서 시리즈의이 과정을 통해 했습니다.

- 마스터 페이지와 연관 된 콘텐츠 페이지를 만들어 검사
- 다양 한 팁, 요령 및 트랩을 설명 합니다.
- 마스터 페이지의 일반적인 문제를 식별 및 해결 방법 탐색
- 콘텐츠 페이지와 반대로 a에서 마스터 페이지를 액세스 하는 방법을 참조 하세요.
- 런타임에 콘텐츠 페이지의 마스터 페이지를 지정 하는 방법 및
- 기타 고급 항목에서는 마스터 페이지입니다.

이 자습서는 간결 하 게 되며 프로세스를 안내 하는 시각적으로 스크린 샷을 많은 단계별 지침을 제공 하도록 설계 되었습니다. 각 자습서는 C# 및 Visual Basic 버전에서 사용할 수 및 사용 된 전체 코드를 다운로드 하 여 포함 합니다.

이 첫 자습서 마스터 페이지 기본 사항부터 시작합니다. 마스터 페이지의 작동 방식에 대해 설명, 마스터 페이지 및 Visual Web Developer를 사용 하 여 연결 된 콘텐츠 페이지를 만드는 확인 하 고는 콘텐츠 페이지에 즉시 반영 하는 마스터 페이지에 변경 하는 방법을 참조 하세요. 이제 시작 하겠습니다.

## <a name="understanding-how-master-pages-work"></a>마스터 페이지의 작동 방식 이해

일관 된 사이트 전체 페이지 레이아웃을 사용 하 여 웹 사이트 빌드는 각 웹 페이지 사용자 지정 내용 외에도 일반적인 서식 지정 태그를 내보낼 필요 합니다. 예를 들어, 각 자습서 또는 포럼 게시물 www.asp.net에서 자신의 고유한 콘텐츠가 하는 동안 이러한 각 페이지도 렌더링할 일련의 일반적인 `<div>` 최상위 섹션에 링크를 표시 하는 요소: 홈, 시작, 학습, 및 등입니다.

일관 된 모양과 느낌을 사용 하 여 웹 페이지를 만드는 방법은 여러 가지가 있습니다. 순진한 방법을 간단히 복사 하 고 모든 웹 페이지에 일반적인 레이아웃 태그를 붙여 이지만이 방법은 단점이 많습니다. 먼저 새 페이지가 생성 될 때마다 복사 하 여 페이지에 공유 된 콘텐츠를 붙여 기억해 야 합니다. 이러한 복사 및 붙여넣기 작업에 오류에 대 한 제거 새 페이지에 실수로 공유 태그의 하위 집합만 복사할 수 있습니다. 및에이 방법을 통해 기존 사이트 전체 모양을 실제 고통 새로운 모양과 느낌을 사용 하려면 사이트의 모든 단일 페이지를 편집 해야 하기 때문에 새 항목으로 대체 합니다.

ASP.NET 버전 2.0에서는 이전 페이지 개발자가 종종 일반적인 태그를 배치 [사용자 정의 컨트롤](https://msdn.microsoft.com/library/y6wb1a0e.aspx) 후 각 페이지에 이러한 사용자 정의 컨트롤을 추가 합니다. 이 방법은 페이지 개발자 수동으로 모든 새 페이지에 사용자 정의 컨트롤을 추가 해야 하지만 사용자 컨트롤에 대해서만 수정 하는 데 필요한 일반적인 태그를 업데이트 하는 경우 사이트 전체에 쉽게 수정할 수는 필요 합니다. 아쉽게도 Visual Studio.NET 2002 및 2003-Visual Studio 버전에는 사용자 정의 컨트롤을 디자인 뷰에서 회색 상자로 렌더링 ASP.NET 1.x 응용 프로그램을 만드는 데. 따라서이 방법을 사용 하는 페이지 개발자는 WYSIWYG 디자인 타임 환경을 이용할 수 있습니다 하지 않았습니다.

사용자 정의 컨트롤을 사용 하 여의 단점을 보완 도입 ASP.NET 버전 2.0 및 Visual Studio 2005에서 해결 되었습니다 *마스터 페이지*합니다. 마스터 페이지는 특수 한 유형의 사이트 전체 태그를 정의 하는 ASP.NET 페이지 및 *지역* 연결 된 경우 *콘텐츠 페이지는* 사용자 지정 태그를 정의 합니다. 1 단계에서에서 보이는 이러한 지역 ContentPlaceHolder 컨트롤에 의해 정의 됩니다. 각각의 ContentPlaceHolder 컨트롤로 간단히 마스터 페이지의 컨트롤 계층 구조에 있는 콘텐츠 페이지에서 사용자 지정 콘텐츠를 주입할 수 있습니다 위치를 나타냅니다.

> [!NOTE]
> 핵심 개념과 기능 마스터 페이지의 ASP.NET 2.0 버전 이후 변경 되지 않았습니다. 그러나 Visual Studio 2008에는 Visual Studio 2005의 부족 했습니다 하는 기능 중첩된 마스터 페이지에 대 한 디자인 타임 지원을 제공 합니다. 이후 자습서에서 중첩 된 마스터 페이지를 사용 하 여 살펴보겠습니다.


그림 2 www.asp.net에 대 한 마스터 페이지 모양을 보여 줍니다. 마스터 페이지 왼쪽-가운데에서 각 개별 웹 페이지에 대 한 고유한 콘텐츠를 위치한 ContentPlaceHolder 뿐만 아니라-위쪽, 아래쪽 및 오른쪽의 모든 페이지에서 태그-일반적인 사이트 전체 레이아웃을 정의 하는 note 합니다.


![마스터 페이지 콘텐츠 페이지에서 콘텐츠 페이지 별로 사이트 전체 레이아웃 및 편집 가능한 영역 정의](creating-a-site-wide-layout-using-master-pages-cs/_static/image4.png)

**그림 02**: 마스터 페이지 콘텐츠 페이지에서 콘텐츠 페이지 별로 사이트 전체 레이아웃 및 편집 가능한 영역 정의


마스터 페이지를 정의한 후에 눈금의 확인란을 통해 새 ASP.NET 페이지에 바인딩할 수 있습니다. 이러한 ASP.NET 페이지-콘텐츠 페이지 라는-각 마스터 페이지의 ContentPlaceHolder 컨트롤에 대 한 콘텐츠 컨트롤을 포함 합니다. 브라우저를 통해 콘텐츠 페이지를 방문 하는 경우 ASP.NET 엔진 마스터 페이지의 컨트롤 계층 구조를 만들고 적절 한 위치에 콘텐츠 페이지의 컨트롤 계층 구조를 삽입 합니다. 이 결합 된 컨트롤 계층 구조는 렌더링 및 최종 사용자의 브라우저에 반환 되는 결과 HTML입니다. 따라서 콘텐츠 페이지 ContentPlaceHolder 컨트롤 외부에서 해당 마스터 페이지에 정의 하는 일반적인 태그와 콘텐츠 컨트롤 자체 내에 정의 된 페이지-관련 태그를 모두 내보냅니다. 그림 3에서는이 개념을 보여 줍니다.


[![마스터 페이지에는 요청 된 페이지의 태그를 결합 하는](creating-a-site-wide-layout-using-master-pages-cs/_static/image6.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image5.png)

**그림 03**: 마스터 페이지에는 요청 된 페이지의 태그를 결합 하는 ([큰 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-cs/_static/image7.png))


마스터 페이지 작동 하는 방법을 살펴보았습니다 했으므로 마스터 페이지 및 Visual Web Developer를 사용 하 여 연결 된 콘텐츠 페이지를 만들기에 대해를 살펴보겠습니다.

> [!NOTE]
> 많은 도달 하기 위해이 자습서 시리즈 전체에 걸쳐 구축 하는 ASP.NET 웹 사이트 만들어집니다 ASP.NET 3.5를 사용 하 여 Visual Studio 2008의 Microsoft의 무료 버전과 [Visual Web Developer 2008](https://www.microsoft.com/express/vwd/)합니다. ASP.NET 3.5로 업그레이드 걱정-아직 처리 하지 않은 경우 이러한 자습서에 설명 된 개념에 잘 ASP.NET 2.0 및 Visual Studio 2005입니다. 하지만 일부 데모 응용 프로그램은.NET framework 버전 3.5; 새로운 기능을 사용할 수 있습니다 3.5 관련 기능을 사용 하는 경우 버전 2.0에서에서 유사한 기능을 구현 하는 방법에 설명 하는 포함 합니다. 자습서 각 대상에서 다운로드에 사용할 수 있는 데모 응용 프로그램에는.NET Framework 버전 3.5는에서 보관 하나요는 `Web.config` 3.5 관련 구성 요소 및 3.5 관련 네임 스페이스에 대 한 참조를 포함 하는 파일을 `using` ASP.NET 페이지의 코드 숨김 클래스에는 문입니다. 결론부터 말하자면, 다운로드할 수 있는 웹 응용 프로그램이 다음 컴퓨터에.NET 3.5를 설치 하려면 아직 3.5 관련 태그를 제거 하지 않고 작동 하지 것입니다 `Web.config`합니다. 참조 [분석 ASP.NET 버전 3.5의 `Web.config` 파일](http://www.4guysfromrolla.com/articles/121207-1.aspx) 이 항목에 대 한 자세한 내용은 합니다. 제거 해야 합니다 `using` 3.5 관련 네임 스페이스를 참조 하는 문입니다.


## <a name="step-1-creating-a-master-page"></a>1 단계: 마스터 페이지 만들기

만들고 마스터 및 콘텐츠 페이지를 사용 하 여 탐색할 수 있는, ASP.NET 웹 사이트를 먼저 해야 합니다. 새 파일 시스템 기반 ASP.NET 웹 사이트를 만들어 시작 합니다. 이렇게 하려면 Visual Web Developer 시작 파일 메뉴로 이동 하 고 새 웹 사이트 대화 상자를 표시 하는 새 웹 사이트를 선택 상자 (그림 4 참조). ASP.NET 웹 사이트 템플릿을 선택, 파일 시스템 위치 드롭 다운 목록 설정, 웹 사이트를 배치할 폴더를 선택 및 C# 언어를 설정 합니다. 이 사용 하 여 새 웹 사이트를 만듭니다는 `Default.aspx` ASP.NET 페이지는 `App_Data` 폴더 및 `Web.config` 파일입니다.

> [!NOTE]
> Visual Studio는 프로젝트 관리의 두 가지 모드를 지원 합니다: 웹 사이트 프로젝트와 웹 응용 프로그램 프로젝트입니다. 프로젝트 아키텍처에 Visual Studio.NET 2002/2003을 모방 하는 웹 응용 프로그램 프로젝트-프로젝트 파일을 포함 하 고 프로젝트의 소스 코드에 배치 되는 단일 어셈블리로 컴파일할 때 반면 웹 사이트 프로젝트 없는 프로젝트 파일을 `/bin` 폴더입니다. 하지만 visual Studio 2005는 지원 되는 웹 사이트를 처음에 프로젝트를 [웹 응용 프로그램 프로젝트 모델](https://msdn.microsoft.com/library/aa730880(vs.80).aspx) 서비스 팩 1로 다시 도입 되었습니다 Visual Studio 2008 프로젝트 모델을 모두 제공합니다. 그러나 Visual Web Developer 2005 및 2008 edition만 지원 웹 사이트 프로젝트입니다. 이 자습서 시리즈에서 내 데모 웹 사이트 프로젝트 모델로 사용 합니다. Express 이외의 버전을 사용 하는 웹 응용 프로그램 프로젝트 모델을 대신 사용 하려는 경우 자유롭게 있을 수 있다는 일부 불일치 화면 표시 된 스크린샷 및 instructio 및 수행 해야 하는 단계에 표시 되는 내용 간에 수 있지만 이렇게 이 자습서에서 제공 하는 ns.


[![새 파일 시스템 기반 웹 사이트 만들기](creating-a-site-wide-layout-using-master-pages-cs/_static/image9.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image8.png)

**그림 04**: New File System-Based 웹 사이트 만들기 ([큰 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-cs/_static/image10.png))


다음으로, 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고, 새 항목 추가 선택 하 고, 마스터 페이지 템플릿을 선택 하 여 사이트의 루트 디렉터리에 마스터 페이지를 추가 합니다. 마스터 페이지 확장명으로 끝나야 하는 참고 `.master`합니다. 이 새 마스터 페이지 이름을 `Site.master` 추가를 클릭 합니다.


[![마스터 페이지 추가 웹 사이트에 Site.master 라는](creating-a-site-wide-layout-using-master-pages-cs/_static/image12.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image11.png)

**그림 05**: 마스터 페이지 이름이 지정 된 추가 `Site.master` 웹 사이트 ([클릭 하 여 큰 이미지 보기](creating-a-site-wide-layout-using-master-pages-cs/_static/image13.png))


Visual Web Developer를 통해 새 마스터 페이지 파일을 추가 합니다. 다음 선언적 태그를 사용 하 여 마스터 페이지를 만듭니다.

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample1.aspx)]

선언적 태그의 첫 번째 줄은는 [ `@Master` 지시문](https://msdn.microsoft.com/library/ms228176.aspx)합니다. 합니다 `@Master` 지시문은 비슷합니다는 [ `@Page` 지시문](https://msdn.microsoft.com/library/ydy4x04a.aspx) ASP.NET 페이지에 표시 됩니다. 서버 쪽 언어 (C#) 및 위치 및 마스터 페이지의 코드 숨김 클래스의 상속에 대 한 정보를 정의합니다.

합니다 `DOCTYPE` 페이지의 선언적 태그 아래에 나타나고는 `@Master` 지시문입니다. 페이지에 정적 HTML 4 개의 서버 쪽 컨트롤이 함께 포함 됩니다.

- **Web Form (합니다 `<form runat="server">`)** -일반적으로 웹 양식이-및 마스터 페이지는 Web Form-내에서 표시 되어야 하는 웹 컨트롤을 포함할 수 있습니다 되므로 합니다 웹 폼 마스터 페이지 (추가 하지 않고 Web Form e에 추가할 모든 ASP.NET 페이지 대 한 ach 콘텐츠 페이지)입니다.
- **ContentPlaceHolder 컨트롤인 `ContentPlaceHolder1`**  -이 각각의 ContentPlaceHolder 컨트롤로 Web Form 내에서 표시 되 고 콘텐츠 페이지의 사용자 인터페이스에 대 한 지역으로 사용 됩니다.
- **서버 쪽 `<head>` 요소** - `<head>` 요소에는 `runat="server"` 특성, 서버 쪽 코드를 통해 액세스할 수 있도록 합니다. 합니다 `<head>` 요소에는 이러한 방식으로 구현 됩니다 있도록 페이지의 제목 및 기타 `<head>`-관련 태그를 추가 하거나 프로그래밍 방식으로 조정할 수 있습니다. 예를 들어, ASP.NET 페이지의 설정 `Title` 속성 변경 내용을 합니다 `<title>` 요소에서 렌더링는 `<head>` 서버 컨트롤입니다.
- **라는 ContentPlaceHolder 컨트롤 `head`**  -내에서이 각각의 ContentPlaceHolder 컨트롤로 표시 되는 `<head>` 서버 컨트롤을 사용 하 여 콘텐츠를 선언적으로 추가할 수 있습니다는 `<head>` 요소.

이 기본 마스터 페이지 선언적 태그는 사용자 고유의 마스터 페이지를 디자인 하기 위한 시작 지점으로 사용 됩니다. HTML 편집 하거나 추가 웹 컨트롤 또는 ContentPlaceHolders 마스터 페이지에 추가할 자유롭게 확인 하십시오.

> [!NOTE]
> 마스터 페이지 디자인을 확인 하는 경우 마스터 페이지는 Web Form을 포함 하 고이 Web Form 내에 하나 이상의 각각의 ContentPlaceHolder 컨트롤로 나타납니다.


### <a name="creating-a-simple-site-layout"></a>간단한 사이트 레이아웃 만들기

확장 `Site.master`의 모든 페이지를 공유 하는 사이트 레이아웃을 만드는 기본 선언적 태그: 공용 헤더, 탐색, 뉴스 및 다른 사이트 전체 콘텐츠 및 "Microsoft ASP.NET으로 전원이" 아이콘을 표시 하는 바닥글을 사용 하 여 왼쪽된 열입니다. 그림 6에서는 브라우저를 통해 콘텐츠 페이지 중 하나를 볼 때 마스터 페이지의 최종 결과를 보여 줍니다. 그림 6의 빨간색 원으로 표시 된 항목된 영역 방문 페이지에 따라 다릅니다 (`Default.aspx`); 모든 콘텐츠 페이지에 걸쳐 마스터 페이지에 정의 되 고 따라서 일치를 하는 다른 콘텐츠입니다.


[![위쪽, 왼쪽 및 아래쪽 부분에 대 한 태그를 정의 하는 마스터 페이지](creating-a-site-wide-layout-using-master-pages-cs/_static/image15.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image14.png)

**그림 06**: 위쪽, 왼쪽 및 아래쪽 부분에 대 한 태그를 정의 하는 마스터 페이지 ([큰 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-cs/_static/image16.png))


그림 6 에서처럼 사이트 레이아웃을 달성 하려면 업데이트 하 여 시작 합니다 `Site.master` 마스터 페이지는 다음과 같은 선언적 태그가 포함 되도록 합니다.

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample2.aspx)]

마스터 페이지의 레이아웃을 사용 하 여 정의 됩니다 `<div>` HTML 요소입니다. 합니다 `topContent` `<div>` 각 페이지의 위쪽에 표시 되는 태그를 포함 하는 동안 합니다 `mainContent`를 `leftContent`, 및 `footerContent` `<div>` s는 페이지의 콘텐츠, 왼쪽된 열 및 "제공 하 여 Microsoft 표시 하는 데 사용 됩니다 ASP.NET"아이콘을 각각. 이러한 추가 하는 것 외에도 `<div>` 요소인도 바꾼 합니다 `ID` 에서 기본 ContentPlaceHolder 컨트롤의 속성 `ContentPlaceHolder1` 에 `MainContent`.

에 대 한 다양 한 서식 및 레이아웃 규칙 `<div>` 요소는 정확 하 게 합니다 [스타일 시트 (CSS)](http://en.wikipedia.org/wiki/Cascading_Style_Sheets) 파일 `Styles.css`를 통해 지정 된를 &lt;링크&gt; 요소에는 마스터 페이지의 &lt;head&gt; 요소입니다. 각각의 모양과 느낌을 정의 하는 이러한 다양 한 규칙 `<div>` 위에서 언급 한 요소입니다. 예를 들어를 `topContent` `<div>` "마스터 페이지 자습서" 텍스트 및 링크를 표시 하는 요소에 지정 된 서식 지정 규칙에 `Styles.css` 다음과 같습니다.

[!code-css[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample3.css)]

이 자습서의 함께 제공 되는 코드를 다운로드 및 추가 해야 하는 경우에 따라 컴퓨터에서을 `Styles.css` 프로젝트 파일입니다. 마찬가지로, 명명 된 이미지 폴더를 만들고 프로젝트에 다운로드 된 데모 웹 사이트에서 "Microsoft ASP.NET으로 전원이" 아이콘을 복사 해야 합니다.

> [!NOTE]
> CSS 및 웹 페이지 서식을 설명은이 문서의 범위를 벗어납니다. CSS에 자세한 체크 아웃 합니다 [CSS 자습서](http://www.w3schools.com/css/default.asp) 에서 [W3Schools.com](http://www.w3schools.com/)합니다. 이 자습서의 함께 제공 되는 코드를 다운로드 하 여 CSS 설정이 재생도 바랍니다 `Styles.css` 다양 한 서식 지정 규칙의 영향을 확인 하려면.


### <a name="creating-a-master-page-using-an-existing-design-template"></a>기존 디자인 템플릿을 사용 하 여 마스터 페이지 만들기

년에 걸쳐 다양 한 소규모-회사에 대 한 ASP.NET 웹 응용 프로그램 작성 했습니다. 내 클라이언트 중 일부가 했습니다 사용할; 기존 사이트 레이아웃 다른 유능한 그래픽 디자이너를 고용 합니다. 몇 가지 웹 사이트 레이아웃을 디자인을 위임 합니다. 그림 6에서 알 수 있듯이, 웹 사이트의 레이아웃을 디자인 하려면 프로그래머가 태스크는 일반적으로 과장에 세금을 수행 하는 동안 open-heart surgery 수행 하 여 회계사 것으로 좋습니다.

다행 스럽게도 가지 무료 HTML 디자인 템플릿을 제공 하는 innumerous websites-Google에서 검색 용어 "무료 웹 사이트 템플릿입니다." 6 백만 개 결과 반환 했습니다. 내 즐겨찾기 항목 중 하나인 [OpenDesigns.org](http://opendesigns.org/)합니다. 원하는 웹 사이트 템플릿을 찾으면 CSS 파일 및 이미지를 웹 사이트 프로젝트에 추가 하 고 마스터 페이지에는 서식 파일의 HTML을 통합 합니다.

> [!NOTE]
> Microsoft는 다양 한도 제공 합니다. [무료 ASP.NET 디자인 시작 키트 템플릿](https://msdn.microsoft.com/asp.net/aa336613.aspx) Visual Studio에서 새 웹 사이트 대화 상자에 통합 합니다.


## <a name="step-2-creating-associated-content-pages"></a>2 단계: 콘텐츠 페이지에 연결 만들기

만든 마스터 페이지에서는 마스터 페이지에 바인딩되는 ASP.NET 페이지 만들기를 시작할 준비가 된 것입니다. 이러한 페이지 라고 *콘텐츠 페이지는*합니다.

보겠습니다 프로젝트에 새 ASP.NET 페이지를 추가 하 고를 바인딩하는 `Site.master` 마스터 페이지입니다. 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 새 항목 추가 옵션을 선택 합니다. 웹 양식 서식 파일을 선택, 이름 `About.aspx`, 그림 7 에서처럼 "마스터 페이지 선택" 확인란을 확인 하 고 있습니다. 이렇게 선택 된 마스터 페이지 대화 상자가 표시 됩니다 (그림 8 참조)에서 사용 하 여 마스터 페이지를 선택할 수 있는 상자입니다.

> [!NOTE]
> 웹 응용 프로그램 프로젝트 모델을 사용 하 여 웹 사이트 프로젝트 모델 대신 ASP.NET 웹 사이트를 만든 경우 그림 7의 새 항목 추가 대화 상자에서 "마스터 페이지 선택" 확인란을 표시 되지 않습니다. 콘텐츠 만들기 페이지 모델 웹 응용 프로그램 프로젝트를 사용 하는 경우 웹 양식 서식 파일 대신 웹 콘텐츠 폼 템플릿을 선택 해야 합니다. 웹 콘텐츠 폼 템플릿을 선택 하 고 추가 클릭 하면을 그림 8 에서처럼 대화 상자가 표시 됩니다 마스터 페이지 선택 동일 합니다.


[![새 콘텐츠 페이지 추가](creating-a-site-wide-layout-using-master-pages-cs/_static/image18.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image17.png)

**그림 07**: 새 콘텐츠 페이지 추가 ([큰 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-cs/_static/image19.png))


[![Site.master 마스터 페이지를 선택 합니다.](creating-a-site-wide-layout-using-master-pages-cs/_static/image21.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image20.png)

**그림 08**: 선택 된 `Site.master` 마스터 페이지 ([클릭 하 여 큰 이미지 보기](creating-a-site-wide-layout-using-master-pages-cs/_static/image22.png))


새 콘텐츠 페이지에 포함 된 다음 선언적 태그에서 알 수 있듯이는 `@Page` 를 가리키지만 마스터 페이지 및 콘텐츠 컨트롤을 각 마스터 페이지의 ContentPlaceHolder 컨트롤에 대 한 지시문입니다.

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample4.aspx)]

> [!NOTE]
> 1 단계에서에서 "간단한 사이트 레이아웃 만들기" 섹션에서 이름을 바꾼 `ContentPlaceHolder1` 에 `MainContent`입니다. 이 각각의 ContentPlaceHolder 컨트롤로 이름을 변경 하지 않으면 경우 `ID` 동일한 방법으로 콘텐츠 페이지의 선언적 태그는 약간 다를 위에 표시 된 태그에서. 즉, 두 번째 콘텐츠 컨트롤의 `ContentPlaceHolderID` 반영 됩니다는 `ID` 해당 ContentPlaceHolder의 마스터 페이지에서 제어 합니다.


ASP.NET 엔진 페이지의 fuse 해야 콘텐츠 페이지를 렌더링 하는 경우 콘텐츠는 마스터 페이지의 ContentPlaceHolder 컨트롤로 컨트롤입니다. ASP.NET 엔진에서 콘텐츠 페이지의 마스터 페이지를 결정 합니다 `@Page` 지시문의 `MasterPageFile` 특성입니다. 위의 태그에서 알 수 있듯이,이 콘텐츠 페이지에 바인딩되어 `~/Site.master`합니다.

마스터 페이지에 두 개의 ContentPlaceHolder 컨트롤-있어서 `head` 고 `MainContent` -Visual Web Developer 두 콘텐츠 컨트롤을 생성 합니다. 각 콘텐츠 컨트롤 참조를 통해 특정 ContentPlaceHolder 해당 `ContentPlaceHolderID` 속성입니다.

여기서 이전 사이트 전체 템플릿 기법을 통해 마스터 페이지 반짝이 디자인 타임 지원을입니다. 그림 9를 `About.aspx` Visual Web Developer의 디자인 뷰를 통해 볼 때 콘텐츠 페이지입니다. 마스터 페이지 콘텐츠를 하는 동안 표시 되는 참고를 회색으로 표시 되 고 수정할 수 없습니다. 그러나 콘텐츠 컨트롤이 해당 마스터 페이지의 ContentPlaceHolders 하 되는 경우 편집할 수 있습니다. 것 처럼, 다른 ASP.NET 페이지를 사용 하 여 원본 또는 디자인 뷰를 통해 웹 컨트롤을 추가 하 여 콘텐츠 페이지의 인터페이스를 만들 수 있습니다.


[![콘텐츠 페이지의 디자인 뷰에서 페이지별 및 마스터 페이지 콘텐츠를 표시합니다.](creating-a-site-wide-layout-using-master-pages-cs/_static/image24.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image23.png)

**그림 09**: The 콘텐츠 페이지의 디자인 보기 표시는 페이지별과 마스터 페이지 콘텐츠 ([큰 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-cs/_static/image25.png))


### <a name="adding-markup-and-web-controls-to-the-content-page"></a>콘텐츠 페이지에 태그 및 웹 컨트롤 추가

잠시 시간에 대 한 일부 콘텐츠를 만들 수는 `About.aspx` 페이지입니다. 그림 10에서 참조는 "작성자 정보" 제목 및 몇 가지 텍스트 단락을 입력 하지만 너무 웹 컨트롤을 추가할 수 있습니다. 이 인터페이스를 만든 후 방문는 `About.aspx` 브라우저를 통해 페이지입니다.


[![브라우저를 통해 about.aspx로 페이지를 참조 하세요.](creating-a-site-wide-layout-using-master-pages-cs/_static/image27.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image26.png)

**그림 10**: 방문 합니다 `About.aspx` 브라우저를 통해 페이지 ([클릭 하 여 큰 이미지 보기](creating-a-site-wide-layout-using-master-pages-cs/_static/image28.png))


요청 된 콘텐츠 페이지와 연결 된 해당 마스터 페이지가 결합 되 고 웹 서버에서 완전히 전체 렌더링을 이해 하는 것이 반드시 합니다. 최종 사용자의 브라우저 결과, 퓨즈 HTML을 전송 됩니다. 이 확인 하려면 보기 메뉴로 이동 하 고 소스를 선택 하 여 브라우저에서 받은 HTML을 봅니다. 프레임이 없는 또는 기타 특수 기술을 단일 창에 두 개의 다른 웹 페이지를 표시 하는 것에 대 한 참고 합니다.

### <a name="binding-a-master-page-to-an-existing-aspnet-page"></a>기존 ASP.NET 페이지에 마스터 페이지를 바인딩

이 단계에서 보았듯이 "마스터 페이지 선택" 확인란을 선택 하 고 마스터 페이지를 선택 하는 것 만큼 쉽습니다는 ASP.NET 웹 응용 프로그램에 새 콘텐츠 페이지를 추가 합니다. 그러나 마스터 페이지에 기존 ASP.NET 페이지를 변환으로 쉽지 않습니다.

기존 ASP.NET 페이지에 마스터 페이지를 바인딩하려면 다음 단계를 수행 해야 합니다.

1. 추가 합니다 `MasterPageFile` ASP.NET 페이지의 특성 `@Page` 해당 마스터 페이지를 가리키는 지시문입니다.
2. 마스터 페이지에서 ContentPlaceHolders의 각 콘텐츠 컨트롤을 추가 합니다.
3. 선택적으로 잘라내기 및 적절 한 콘텐츠 컨트롤에 기존 ASP.NET 페이지의 콘텐츠를 붙여 넣습니다. ASP.NET 페이지 가능성이 있기 때문에 "선택적" 여기 이미 표현 된 마스터 페이지에서와 같은 태그를 포함 하는 것이 말할 합니다 `DOCTYPE`, `<html>` 요소 및 Web Form입니다.

스크린 샷와 함께이 프로세스에 대 한 단계별 지침에 대 한 체크 아웃 [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 [사용 하 여 마스터 페이지 및 사이트 탐색](http://webproject.scottgu.com/CSharp/MasterPages/MasterPages.aspx) 자습서입니다. "업데이트 `Default.aspx` 고 `DataSample.aspx` 마스터 페이지를 사용 하려면" 섹션에서는 이러한 단계를 자세히 설명 합니다.

훨씬 쉽게 콘텐츠 페이지에 기존 ASP.NET 페이지를 변환 하는 것 보다 새 콘텐츠 페이지를 만들 수 있기 때문에 만들 때마다 새 ASP.NET 웹 사이트를 사이트에 마스터 페이지를 추가할 것을 권장 합니다. 이 마스터 페이지에 모든 새 ASP.NET 페이지를 바인딩하십시오. 초기 마스터 페이지는 매우 단순 하거나 일반; 경우 걱정 하지 마세요 나중에 마스터 페이지를 업데이트할 수 있습니다.

> [!NOTE]
> 새 ASP.NET 응용 프로그램을 만들 때 Visual Web Developer 추가 `Default.aspx` 마스터 페이지에 얽매이지 않는 페이지입니다. 실제로 콘텐츠 페이지에 기존 ASP.NET 페이지를 변환 하려는 경우 계속 해 서 사용 하 여 이렇게 `Default.aspx`합니다. 삭제할 수 있습니다 `Default.aspx` , 이번 "마스터 페이지 선택" 확인란을 선택한 다음 다시 추가 합니다.


## <a name="step-3-updating-the-master-pages-markup"></a>3 단계: 마스터 페이지의 태그를 업데이트합니다.

마스터 페이지의 주요 이점 중 하나는 사이트에서 다양 한 페이지에 대 한 전체 레이아웃을 정의 하는 단일 마스터 페이지를 사용할 수 있습니다. 따라서 사이트의 모양과 느낌을 업데이트 한 파일-마스터 페이지를 업데이트 해야 합니다.

이 문제를 보여 주기 위해 왼쪽 열의 맨 위에 있는 현재 날짜를 포함 하는 마스터 페이지를 업데이트 해 보겠습니다. 이라는 레이블을 추가 `DateDisplay` 에 `leftContent` `<div>`합니다.

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample5.aspx)]

다음으로 만듭니다는 `Page_Load` 마스터에 대 한 이벤트 처리기 페이지 및 다음 코드를 추가 합니다.

[!code-csharp[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample6.cs)]

위의 코드에 레이블 설정 `Text` 는 요일, 월 및 두 일의 이름으로 속성을 현재 날짜 및 시간 형식 (그림 11 참조). 이 변경으로 콘텐츠 페이지 중 하나를 다시 확인 합니다. 그림 11에서 알 수 있듯이, 결과 태그는 즉시 마스터 페이지에 변경 내용을 포함 하도록 업데이트 됩니다.


[![마스터 페이지 변경 사항이 반영 때는 표시 된 콘텐츠 페이지](creating-a-site-wide-layout-using-master-pages-cs/_static/image30.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image29.png)

**그림 11**: 마스터 페이지에는 변경 내용이 반영 때는 표시 된 콘텐츠 페이지 ([큰 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-cs/_static/image31.png))


> [!NOTE]
> 이 예제에서 알 수 있듯이, 마스터 페이지 서버 쪽 웹 컨트롤, 코드 및 이벤트 처리기를 포함할 수 있습니다.


## <a name="summary"></a>요약

마스터 페이지를 쉽게 업데이트할 수 있는 일관 된 사이트 전체 레이아웃을 디자인 하는 ASP.NET 개발자를 사용 합니다. 마스터 페이지와 연관 된 콘텐츠 페이지를 만들어 Visual Web Developer는 다양 한 디자인 타임 지원을 제공은 표준 ASP.NET 페이지를 만드는 것 만큼 간단 합니다.

이 자습서에서 만든 마스터 페이지 예제에서는 두 개의 ContentPlaceHolder 컨트롤 했습니다 `head` 고 `MainContent`입니다. 하지만에 대 한 태그만 지정한는 `MainContent` ContentPlaceHolder, 콘텐츠 페이지에 컨트롤입니다. 다음 자습서에서에 대해 살펴봅니다 여러 콘텐츠를 사용 하는 콘텐츠 페이지의 컨트롤입니다. 또한 기본값을 정의 하는 방법을 표시 태그 콘텐츠에 대 한 기본값을 사용 하 여 사이 전환 하려면 태그에에서 정의 된 마스터 페이지 및 콘텐츠 페이지에서 사용자 지정 태그를 제공 하는 방법으로 마스터 페이지 내에서 제어 합니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [디자이너를 위한 ASP.NET: 웹 표준을 이용한 ASP.NET 웹 사이트 구축에 무료 디자인 템플릿 및 지침](https://msdn.microsoft.com/asp.net/aa336602.aspx)
- [ASP.NET 마스터 페이지 개요](https://msdn.microsoft.com/library/wtxbf3hh.aspx)
- [연계 스타일 시트 (CSS) 자습서](http://www.w3schools.com/css/default.asp)
- [동적 페이지 제목 설정](http://aspnet.4guysfromrolla.com/articles/051006-1.aspx)
- [ASP.NET의 마스터 페이지](http://www.odetocode.com/articles/419.aspx)
- [마스터 페이지 퀵 스타트 자습서](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/masterpages/default.aspx)

### <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 작성자의 여러 ASP/ASP.NET 서적과 4GuysFromRolla.com의 설립자 이며, 왔습니다 Microsoft 웹 기술을 1998 합니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 3.5 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. Scott에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com) 통하거나 저자의 블로그 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)합니다.

> [!div class="step-by-step"]
> [다음](multiple-contentplaceholders-and-default-content-cs.md)
