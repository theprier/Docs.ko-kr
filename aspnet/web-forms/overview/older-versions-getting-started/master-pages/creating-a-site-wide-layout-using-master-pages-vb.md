---
uid: web-forms/overview/older-versions-getting-started/master-pages/creating-a-site-wide-layout-using-master-pages-vb
title: 마스터 페이지 (VB)를 사용 하는 사이트 전체 레이아웃 만들기 | Microsoft Docs
author: rick-anderson
description: 이 자습서는 기본 사항 마스터 페이지를 표시 합니다. 즉, 마스터 페이지은 어떻게 하나는 마스터 페이지를 만들고, cr은 어떻게 콘텐츠 자리 표시자 이란...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/21/2008
ms.topic: article
ms.assetid: 30945276-8ed9-4b27-8e50-4309244d3559
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/creating-a-site-wide-layout-using-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: d18993af7159de552db0c622fbef58e814e36ebb
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30890881"
---
<a name="creating-a-site-wide-layout-using-master-pages-vb"></a>마스터 페이지 (VB)를 사용 하는 사이트 전체 레이아웃 만들기
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_01_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_01_VB.pdf)

> 이 자습서는 기본 사항 마스터 페이지를 표시 합니다. 즉, 마스터 페이지, 마스터 페이지를 만들려면가 어떻게 하나 콘텐츠 자리 표시자 이란 어떻게 하나 만듭니까 방법을 수정 하 고 마스터 페이지는 자동으로 반영 이와 연결 된 콘텐츠 페이지, 마스터 페이지를 사용 하는 ASP.NET 페이지.


## <a name="introduction"></a>소개

잘 디자인 된 웹 사이트의 특성 하나는 일관성 있는 사이트 전체 페이지 레이아웃입니다. Www.asp.net 웹 사이트를 예로 들어 보겠습니다. 이 문서 작성 당시의 모든 페이지에서 동일한 내용이 페이지 맨 위와 맨 아래에 있습니다. 그림 1에서 볼 수 있듯이 각 페이지의 맨 Microsoft 커뮤니티의 목록이 있는 회색 막대를 표시 합니다. 사이트 로고, 대상 사이트 번역 된, 언어 및 코어 섹션의 목록 아래에 있는: 홈, 시작, 자세한 정보, 다운로드 및 붙습니다. 마찬가지로, 페이지 하단에는 www.asp.net, 저작권 정보 및 개인정보취급방침 대 한 링크에 광고 하는 방법에 대 한 정보가 포함 됩니다.


[![모든 페이지에 걸쳐 일관 된 모양과 느낌을 사용 하는 www.asp.net 웹 사이트](creating-a-site-wide-layout-using-master-pages-vb/_static/image2.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image1.png)

<strong>그림 01</strong>: 일관성 확인 및 모든 페이지에서 생각 될 www.asp.net 웹 사이트 사용 ([전체 크기 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-vb/_static/image3.png))


잘 설계 된 사이트의 다른 특성에는 사이트의 모양을 변경할 수 있는 편의성입니다. 그림 1 2008 년 3 월을 기준으로 www.asp.net 홈 페이지에 나와 있지만 고이 자습서의이 게시, 모양 및 느낌 변경 수 있습니다. 아마도 메뉴 항목 위에 MVC 프레임 워크에 대 한 새 섹션을 포함 하도록 확장 됩니다. 또는 미정 서로 다른 색, 글꼴 및 레이아웃와 근본적으로 새로운 디자인의 소개 해제 됩니다. 전체 사이트에 이러한 변경 내용을 적용 하면 수천 대 사이트를 구성 하는 웹 페이지를 수정 하지 않아도 되는 빠르고 단순 프로세스 이어야 합니다.

ASP.NET에서 사이트 전체 페이지 서식 파일을 만들을 사용 하 여 수는 *마스터 페이지*합니다. 간단히 말해, 마스터 페이지는 특수 한 유형의 모든 간에 공통적으로 적용 되는 태그를 정의 하는 ASP.NET 페이지 *콘텐츠 페이지* 콘텐츠 페이지 콘텐츠 페이지 별로 사용자 지정할 수 있는 영역도 있습니다. (콘텐츠 페이지는 마스터 페이지에 바인딩되는 ASP.NET 페이지입니다.) 마스터 페이지의 레이아웃 또는 서식을 변경 될 때마다 모든 해당 콘텐츠 페이지의 출력은 마찬가지로 즉시 업데이트, 업데이트 및 단일 파일 (즉, 마스터 페이지)를 배포 하는 것 만큼 쉽게 사이트 전체 모양을 변경 내용을 적용 수 있게 해줍니다.

일련의 마스터 페이지를 사용 하 여 파악할 수 있는 자습서의 첫 번째 자습서입니다. 이 자습서 시리즈의 과정 동안 했습니다:

- 마스터 페이지와 연관 된 콘텐츠 페이지를 만들어 검사
- 다양 한 팁, 요령 및 트랩을 설명 합니다.
- 일반적인 마스터 페이지 문제 식별 및 해결 방법, 탐색
- 콘텐츠 페이지와 반대로 a에서 마스터 페이지에 액세스 하는 방법 참조
- 런타임 시, 콘텐츠 페이지의 마스터 페이지를 지정 하는 방법에 알아봅니다 및
- 다른 고급 마스터 페이지 항목입니다.

이러한 자습서를 간결 하 게 하는 프로세스를 통해 시각적으로 다량의 스크린 샷을 단계별 지침을 제공 하 게 조정 됩니다. 각 자습서 C# 및 Visual Basic 버전에서 사용할 수 있으며 사용 되는 전체 코드의 다운로드에 포함 됩니다.

기본 사항 마스터 페이지를 살펴보고이 밝힘으로써 자습서 시작합니다. 에서는 마스터 페이지의 작동 방식에 대해 설명, 마스터 페이지 및 관련된 콘텐츠 페이지 Visual Web Developer를 사용 하 여 만드는 마스터 페이지에 대 한 변경 내용 페이지에 바로 반영 됩니다는 어떻게 참조 하십시오. 이제 시작 하겠습니다.

## <a name="understanding-how-master-pages-work"></a>마스터 페이지의 작동 방식 이해

각 웹 페이지 사용자 지정 내용 외에도 일반적인 서식 지정 태그를 생성할는 필요는 일관성 있는 사이트 전체 페이지 레이아웃으로 웹 사이트를 구축 합니다. 예를 들어 자신의 고유한 콘텐츠를 보유 하는 각 자습서 또는 포럼 게시물 www.asp.net에, 이러한 각 페이지도 렌더링할 일련의 공통 `<div>` 최상위 섹션에 링크를 표시 하는 요소: 홈, 시작, 학습, 및 등입니다.

일관 된 모양과 느낌을 사용 하 여 웹 페이지를 만들기 위한 기술 중 여러 가지가 있습니다. Naïve 방법은 단순히 복사 하 고 모든 웹 페이지에는 일반적인 레이아웃 태그를 붙여 하는 하지만이 방법에는 다양 한 단점이 있습니다. 먼저 새 페이지를 만들 때마다을 복사 하 고 공유 콘텐츠 페이지에 붙여 기억 합니다. 이러한 복사 및 붙여넣기 작업은 오류 서식 파일을 새 페이지에 실수로 공유 태그의 하위 집합만 복사할 수 있습니다. 및에이 방법을 사용 하면 기존 사이트 전체 모양을 실제 패인 새 디자인을 사용 하려면 사이트에 있는 모든 단일 페이지를 편집 해야 하기 때문에 새 항목으로 대체 합니다.

ASP.NET 버전 2.0에서는 이전 페이지 종종 일반적인 태그에 배치 하는 개발자가 [사용자 정의 컨트롤](https://msdn.microsoft.com/library/y6wb1a0e.aspx) 각 페이지에 이러한 사용자 정의 컨트롤을 추가 합니다. 이 방법을 사용 하면 페이지 개발자 수동으로 모든 새 페이지에 사용자 정의 컨트롤을 추가 해야 하지만 사용자 정의 컨트롤을 수정 해야 할 일반적인 태그를 업데이트할 때 때문에 보다 쉽게 사이트 전체 수정에 대 한 허용 해야 합니다. 그러나 Visual Studio.NET 2002 및 2003-버전의 Visual Studio를 ASP.NET 1.x 응용 프로그램-사용자 정의 컨트롤을 디자인 뷰에서 회색 상자로 렌더링을 만드는 데 사용 합니다. 따라서이 방법을 사용 하는 페이지 개발자 WYSIWYG 디자인 타임 환경 얻을 수 없으며 않았습니다.

사용자 정의 컨트롤을 사용 하 여의 단점의 도입으로 ASP.NET 버전 2.0 및 Visual Studio 2005에서 해결 된 *마스터 페이지*합니다. 마스터 페이지는 특수 한 유형의 사이트 전체 태그를 정의 하는 ASP.NET 페이지 및 *영역* 연결 된 경우 *콘텐츠 페이지* 사용자 지정 태그를 정의 합니다. 1 단계에서에서 알 수 있듯이 이러한 영역 ContentPlaceHolder 컨트롤에 의해 정의 됩니다. ContentPlaceHolder 컨트롤 단순히 콘텐츠 페이지에서 사용자 지정 콘텐츠를 삽입 될 수 있습니다 위치 마스터 페이지의 컨트롤 계층 구조에서 위치를 나타냅니다.

> [!NOTE]
> 핵심 개념 및 기능 마스터 페이지의 ASP.NET 2.0 버전 이후 변경 되지 않았습니다. 그러나 Visual Studio 2008는 Visual Studio 2005에서 부족 한 된 하는 기능 중첩 된 마스터 페이지에 대 한 디자인 타임 지원을 제공 합니다. 중첩 된 마스터 페이지를 사용 하 여 이후 자습서에서 살펴보겠습니다.


그림 2 www.asp.net에 대 한 마스터 페이지의 모양을 보여줍니다. Note 마스터 페이지의 왼쪽 가운데, 각 개별 웹 페이지에 고유한 콘텐츠 위치한 ContentPlaceHolder 뿐만 아니라 일반적인 사이트 전체 레이아웃-위쪽, 아래쪽, 및 모든 페이지의 오른쪽에 태그-를 정의 합니다.


![마스터 페이지를 사용 하는 콘텐츠 페이지 콘텐츠 페이지 별로 사이트 전체 레이아웃 및 편집 가능한 영역 정의](creating-a-site-wide-layout-using-master-pages-vb/_static/image4.png)

**그림 02**: 마스터 페이지를 사용 하는 콘텐츠 페이지 콘텐츠 페이지 별로 사이트 전체 레이아웃 및 편집 가능한 영역 정의


마스터 페이지를 정의한 후에 확인란의 눈금을 통해 새 ASP.NET 페이지에 바인딩할 수 있습니다. -콘텐츠 페이지 라는-이러한 ASP.NET 페이지에는 각각의 마스터 페이지의 ContentPlaceHolder 컨트롤에 대 한 콘텐츠 컨트롤을 포함 합니다. 브라우저를 통해 콘텐츠 페이지를 방문 하는 경우 ASP.NET 엔진 마스터 페이지의 컨트롤 계층 구조를 만들고 적절 한 위치에 콘텐츠 페이지의 컨트롤 계층 구조를 삽입 합니다. 이 조합 된 컨트롤 계층 구조를 렌더링 하 고 최종 사용자의 브라우저에 반환 되는 결과 HTML입니다. 따라서 콘텐츠 페이지의 마스터 페이지 ContentPlaceHolder 컨트롤 외부에 정의 된 공통 태그와 콘텐츠 컨트롤 자체 내에 정의 된 페이지 관련 태그를 내보냅니다. 그림 3이이 개념을 보여 줍니다.


[![마스터 페이지에 요청한 페이지의 태그는 Fused](creating-a-site-wide-layout-using-master-pages-vb/_static/image6.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image5.png)

**그림 03**: 마스터 페이지에는 요청 된 페이지의 태그는 Fused ([전체 크기 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-vb/_static/image7.png))


마스터 페이지의 작동 방법을 설명한, 했으므로 마스터 페이지 및 관련된 콘텐츠 페이지 Visual Web Developer를 사용 하 여 만드는 살펴보면을 보겠습니다.

> [!NOTE]
> 많은 달성 하기 위해이 자습서 시리즈 구축 ASP.NET 웹 사이트 생성 됩니다 ASP.NET 3.5를 사용 하 여 Visual Studio 2008의 Microsoft의 무료 버전으로 [Visual Web Developer 2008](https://www.microsoft.com/express/vwd/)합니다. 아직 처리 하지 않은-걱정 ASP.NET 3.5로 업그레이드 하는 경우 이러한 자습서 작업에 설명 된 개념에 잘 ASP.NET 2.0 및 Visual Studio 2005입니다. 그러나 일부 데모 응용 프로그램에서.NET Framework 버전 3.5;에 있는 새 기능은 사용할 수 있습니다. 3.5와 관련 된 기능을 사용할 때는 버전 2.0에서에서 유사한 기능을 구현 하는 방법을 설명 하는 포함 합니다. 각 자습서 대상에서 다운로드에 사용할 수 있는 데모 응용 프로그램에.NET Framework 버전 3.5 염두에서에 둬야지 않습니다는 `Web.config` 3.5 관련 구성 요소를 포함 하는 파일입니다. 아직 다운로드 가능한 웹 응용 프로그램이 다음 컴퓨터에.NET 3.5를 설치 하는 경우에 간단히 3.5 관련 태그를 제거 하지 않고 작동 하지 것입니다 `Web.config`합니다. 참조 [나누어서 ASP.NET 버전 3.5의 `Web.config` 파일](http://www.4guysfromrolla.com/articles/121207-1.aspx) 이 항목에 대 한 자세한 내용은 합니다.


## <a name="step-1-creating-a-master-page"></a>1 단계: 마스터 페이지 만들기

만들고 마스터 및 콘텐츠 페이지를 사용 하 여 탐색할 수 있는, 전에 먼저 ASP.NET 웹 사이트가 필요 합니다. 먼저 새 파일 시스템 기반 ASP.NET 웹 사이트를 만듭니다. 이렇게 하려면 Visual Web Developer를 실행 파일 메뉴로 이동 하 고 새 웹 사이트 대화 상자를 표시 하는 새 웹 사이트를 선택 상자 (그림 4 참조). ASP.NET 웹 사이트 템플릿을 선택한, 파일 시스템에 위치 드롭 다운 목록을 설정, 웹 사이트를 배치할 폴더를 선택 및 Visual basic 언어를 설정 합니다. 이렇게 하면 새 웹 사이트에 만들어집니다는 `Default.aspx` ASP.NET 페이지는 `App_Data` 폴더 및 `Web.config` 파일입니다.

> [!NOTE]
> Visual Studio 프로젝트 관리의 두 모드를 지원: 웹 사이트 프로젝트와 웹 응용 프로그램 프로젝트입니다. 웹 사이트 프로젝트 없는 프로젝트 파일을 웹 응용 프로그램 프로젝트를 Visual Studio.NET 2002/2003에서 프로젝트 아키텍처 모방-프로젝트 파일을 포함 하 고 프로젝트의 소스 코드에 배치 단일 어셈블리로 컴파일할 때 반면는 `/bin` 폴더입니다. Visual Studio 2005 처음만 지원 되는 웹 사이트 프로젝트, 서비스 팩 1; 웹 응용 프로그램 프로젝트 모델이 다시 발생 하지만 Visual Studio 2008 둘 다 프로젝트 모델을 제공 합니다. 그러나 Visual Web Developer 2005 및 2008 edition만 지원 웹 사이트 프로젝트. 이 자습서 시리즈의 인터페이스에 대 한 웹 사이트 프로젝트 모델을 사용 하려면. Express 이외의 버전을 사용 하는 경우를 사용 하려는 [웹 응용 프로그램 프로젝트 모델](https://msdn.microsoft.com/library/aa730880(vs.80).aspx) 대신 자유롭게 있을 수 있음을 약간 다 화면 및 비교 수행 해야 하는 단계에 표시 되는 내용 간에 수 있지만 이렇게는 표시 된 스크린 샷 및이 자습서에 제공 된 지침.


[![새 파일 시스템 기반 웹 사이트 만들기](creating-a-site-wide-layout-using-master-pages-vb/_static/image9.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image8.png)

**그림 04**: New File System-Based 웹 사이트 만들기 ([전체 크기 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-vb/_static/image10.png))


다음으로, 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고, 새 항목 추가 선택 하 고, 마스터 페이지 서식 파일을 선택 하 여 마스터 페이지의 루트 디렉터리에 있는 사이트에 추가 합니다. 마스터 페이지 확장 끝나야 참고 `.master`합니다. 이 새 마스터 페이지 이름을 `Site.master` 추가를 클릭 합니다.


[![마스터 페이지를 추가할 웹 사이트에 Site.master 라는](creating-a-site-wide-layout-using-master-pages-vb/_static/image12.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image11.png)

**그림 05**: 마스터 페이지 이름이 지정 된 추가 `Site.master` 웹 사이트에 ([전체 크기 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-vb/_static/image13.png))


Visual Web Developer를 통해 새 마스터 페이지 파일을 추가 합니다. 다음과 같은 선언적 태그가 포함 된 마스터 페이지를 만듭니다.

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample1.aspx)]

선언적 태그의 첫 번째 줄은는 [ `@Master` 지시문](https://msdn.microsoft.com/library/ms228176.aspx)합니다. `@Master` 지시문은 비슷합니다는 [ `@Page` 지시문](https://msdn.microsoft.com/library/ydy4x04a.aspx) ASP.NET 페이지에 나타나는 합니다. 서버 쪽 언어 (VB) 및 위치와 마스터 페이지의 코드 숨김 클래스의 상속에 대 한 정보를 정의합니다.

`DOCTYPE` 페이지의 선언적 태그 아래에 표시 하 고는 `@Master` 지시문입니다. 페이지에는 4 개의 서버 쪽 제어와 함께 정적 HTML 포함 됩니다.

- **Web Form (의 `<form runat="server">`)** -모든 ASP.NET 페이지 일반적으로 웹 양식-및 마스터 페이지-웹 폼 내에서 표시 해야 하는 웹 컨트롤에 포함 될 수 있습니다 되므로 합니다 마스터 페이지 (추가 하지 않고 웹 폼에서 e에 Web Form을 추가 하려면 와 콘텐츠 페이지)입니다.
- **라는 ContentPlaceHolder 컨트롤 `ContentPlaceHolder1`**  -이 ContentPlaceHolder 컨트롤 웹 폼 내에서 표시 되 고 콘텐츠 페이지의 사용자 인터페이스에 대 한 영역으로 사용 합니다.
- **서버 쪽 `<head>` 요소** - `<head>` 요소에는 `runat="server"` 특성, 서버 쪽 코드를 통해 액세스할 수 있게 합니다. `<head>` 요소는 이러한 방식으로 구현 되도록 페이지의 제목 및 기타 `<head>`-관련 태그를 추가 하거나 프로그래밍 방식으로 조정할 수 있습니다. 예를 들어, ASP.NET 페이지의 설정 `Title` 속성 변경 내용을 `<title>` 에서 렌더링 된 요소는 `<head>` 서버 컨트롤입니다.
- **라는 ContentPlaceHolder 컨트롤 `head`**  -내에서이 ContentPlaceHolder 컨트롤이 표시 되는 `<head>` 서버 제어 하 고 콘텐츠를 선언적으로 사용할 수는 `<head>` 요소입니다.

이 기본 마스터 페이지 선언적 태그 마스터 페이지를 디자인 하기 위한 시작 점으로 사용 됩니다. HTML 편집 하거나 추가 웹 컨트롤이 나 contentplaceholders의 마스터 페이지에 추가 하려면 자유롭게 확인 하십시오.

> [!NOTE]
> 마스터 페이지 디자인 되었는지 확인 하는 경우 웹 폼 마스터 페이지에 포함 하 고이 Web Form 내 하나 이상의 해당 ContentPlaceHolder 컨트롤에 표시 합니다.


### <a name="creating-a-simple-site-layout"></a>간단한 사이트 레이아웃 만들기

확장 해 보겠습니다 `Site.master`의 모든 페이지를 공유 하는 사이트 레이아웃을 만드는 기본 선언적 태그: 공통 헤더를 탐색, 뉴스 및 다른 사이트 전체 콘텐츠를 "Microsoft ASP.NET에서 전원이" 아이콘을 표시 하는 바닥글와 왼쪽된 열입니다. 그림 6에서는 브라우저를 통해 해당 콘텐츠 페이지 중 하나를 볼 때 마스터 페이지의 최종 결과를 보여 줍니다. 그림 6에 있는 빨간색 원 안의 영역의 방문 페이지 됩니다 (`Default.aspx`); 다른 콘텐츠인지를 마스터 페이지에 정의 되 고 따라서 일관 된 모든 콘텐츠 페이지에 걸쳐 있습니다.


[![마스터 페이지 위쪽, 왼쪽 및 아래쪽 부분에 대 한 태그를 정의합니다.](creating-a-site-wide-layout-using-master-pages-vb/_static/image15.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image14.png)

**그림 06**: 위쪽, 왼쪽 및 아래쪽 부분에 대 한 태그를 정의 하는 마스터 페이지 ([전체 크기 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-vb/_static/image16.png))


그림 6에 나와 사이트 레이아웃을 얻기 위해 업데이트 하 여 시작는 `Site.master` 마스터 페이지는 다음과 같은 선언적 태그가 포함 되도록 합니다.

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample2.aspx)]

마스터 페이지의 레이아웃은 일련의를 사용 하 여 정의 된 `<div>` HTML 요소입니다. `topContent` `<div>` 각 페이지 위쪽에 표시 되는 태그를 포함 하는 동안는 `mainContent`, `leftContent`, 및 `footerContent` `<div>` s는 페이지의 콘텐츠, 왼쪽된 열 및 "전원이 하 여 Microsoft 표시 하는 데 사용 됩니다 ASP.NET"아이콘을 각각. 이러한 추가 하는 것 외에도 `<div>` 요소 또한 바꾼 후의 `ID` 에서 기본 ContentPlaceHolder 컨트롤의 속성 `ContentPlaceHolder1` 를 `MainContent`합니다.

이러한 다양 한 서식 및 레이아웃 규칙 `<div>` 요소에 명시 되는 [스타일 시트 (CSS)](http://en.wikipedia.org/wiki/Cascading_Style_Sheets) 파일 `Styles.css`를 통해 지정 된는 `<link>` 마스터 페이지 요소`<head>`요소입니다. 각각의 모양과 느낌을 정의 하는 이러한 다양 한 규칙 `<div>` 위에서 언급 한 요소입니다. 예를 들어는 `topContent` `<div>` "마스터 페이지 자습서" 텍스트 및 링크를 표시 하는 요소에 지정 된은 형식 지정 규칙에 `Styles.css` 다음과 같습니다.

[!code-css[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample3.css)]

이 자습서의 해당 코드를 다운로드 하 고 추가를 할 경우 컴퓨터 앞에 따라는 `Styles.css` 파일을 프로젝트입니다. 마찬가지로, 이라는 폴더를 만들려면 해야 합니다 `Images` 프로젝트를 다운로드 한 데모 웹 사이트에서 "Microsoft ASP.NET에서 전원이" 아이콘을 복사 합니다.

> [!NOTE]
> CSS 및 웹 페이지 서식을 대 한 설명은이 문서의 범위를 벗어납니다. CSS에 대 한 자세한에 대 한 참조는 [CSS 자습서](http://www.w3schools.com/css/default.asp) 에서 [W3Schools.com](http://www.w3schools.com/)합니다. 이 자습서의 해당 코드를 다운로드 하 여 CSS 설정에 재생도 확인해 `Styles.css` 다양 한 서식 규칙의 효과를 확인 합니다.


### <a name="creating-a-master-page-using-an-existing-design-template"></a>기존 디자인 서식 파일을 사용 하 여 마스터 페이지 만들기

수 년에 걸쳐 다양 한 회사 소규모-ASP.NET 웹 응용 프로그램 직접 합니다. 사용 하 여; 기존 사이트 레이아웃에 내 클라이언트 중 일부가 다른 고용 유능한 그래픽 디자이너. 몇 가지를 얻게 웹 사이트 레이아웃을 디자인 하 합니다. 그림 6에서 있음, 웹 사이트의 레이아웃 디자인 프로그래머가 태스크는 일반적으로 프로그램 의사 프로그램 세금을 수행 하는 동안 open-heart surgery 수행 하 여 회계 담당자 있는 것으로 좋습니다.

다행히 무료 HTML 디자인 서식 파일을 제공 하는 웹 사이트를 innumerous 없는-Google 검색어 "무료 웹 사이트 템플릿입니다."에 대 한 6 백만 개 이상의 결과 반환 했습니다. 내 즐겨 찾는 것 중 하나인 [OpenDesigns.org](http://opendesigns.org/)합니다. 원하는 웹 사이트 템플릿을 찾은 후 CSS 파일 및 이미지 웹 사이트 프로젝트를 추가 하 고 마스터 페이지에는 서식 파일의 HTML을 통합 합니다.

> [!NOTE]
> Microsoft는 또한 몇 가지 제공 [ASP.NET 디자인 시작 키트 템플릿 있음](https://msdn.microsoft.com/asp.net/aa336613.aspx) Visual Studio에서 새 웹 사이트 대화 상자에 통합 하는 합니다.


## <a name="step-2-creating-associated-content-pages"></a>2 단계: 콘텐츠 페이지 연결 만들기

만든 마스터 페이지, 마스터 페이지에 바인딩되는 ASP.NET 페이지를 만들기 시작 준비가 됩니다. 이러한 페이지는 라고 *콘텐츠 페이지*합니다.

새 ASP.NET 페이지를 프로젝트에 추가 하 고에 바인딩할 하겠습니다는 `Site.master` 마스터 페이지입니다. 솔루션 탐색기에서 프로젝트 이름을 단추로 클릭 하 고 새 항목 추가 옵션을 선택 합니다. 웹 양식 서식 파일을 선택 합니다. 이름을 입력 하십시오 `About.aspx`, 한 다음 그림 7에 표시 된 것 처럼 "마스터 페이지 선택" 확인란을 확인 합니다. 이렇게 선택 된 마스터 페이지 대화 상자가 표시 됩니다 상자에서 사용할 마스터 페이지를 선택할 수 있습니다 (그림 8 참조).

> [!NOTE]
> 웹 사이트 프로젝트 모델 대신 웹 응용 프로그램 프로젝트 모델을 사용 하 여 ASP.NET 웹 사이트를 만든 경우 그림 7에 표시 된 새 항목 추가 대화 상자에서 "마스터 페이지 선택" 확인란을 표시 되지 않습니다. 콘텐츠를 만들려면 웹 응용 프로그램 프로젝트를 사용 하 여 하면 모델링할 때 페이지 웹 양식 서식 파일 대신 웹 콘텐츠 양식 서식 파일을 선택 해야 합니다. 을 웹 콘텐츠 양식 서식 파일을 선택 하 고 추가 클릭 하면 다음 그림 8 에서처럼 대화 상자가 나타납니다. 마스터 페이지 선택 동일 합니다.


[![새 콘텐츠 페이지 추가](creating-a-site-wide-layout-using-master-pages-vb/_static/image18.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image17.png)

**그림 07**: 새 콘텐츠 페이지 추가 ([전체 크기 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-vb/_static/image19.png))


[![Site.master 마스터 페이지를 선택 합니다.](creating-a-site-wide-layout-using-master-pages-vb/_static/image21.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image20.png)

**그림 08**: 선택 된 `Site.master` 마스터 페이지 ([전체 크기 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-vb/_static/image22.png))


새 콘텐츠 페이지에 포함 되어 다음과 같은 선언적 태그가 볼 수 있듯이 `@Page` 는 돌아가도록 지정 마스터 페이지 및 콘텐츠 컨트롤을 각각의 마스터 페이지의 ContentPlaceHolder 컨트롤에 대 한 지시문입니다.

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample4.aspx)]

> [!NOTE]
> 1 단계에서에서 "간단한 사이트 레이아웃 만들기" 섹션의 이름을 바꾼 `ContentPlaceHolder1` 를 `MainContent`합니다. 이 ContentPlaceHolder 컨트롤의 이름을 변경 하지 않으면 경우 `ID` 동일한 방식으로 콘텐츠 페이지의 선언적 태그 약간 다 위에 표시 된 태그에서 합니다. 즉, 두 번째 콘텐츠 컨트롤의 `ContentPlaceHolderID` 반영 됩니다는 `ID` 마스터 페이지에 있는 해당 ContentPlaceHolder의를 제어 합니다.


ASP.NET 엔진의 페이지를 퓨즈 해야 콘텐츠 페이지를 렌더링 하는 경우 콘텐츠 컨트롤은 마스터 페이지의 ContentPlaceHolder 컨트롤과 합니다. 콘텐츠 페이지의 마스터 페이지를 결정 하는 ASP.NET 엔진은 `@Page` 지시문의 `MasterPageFile` 특성입니다. 이 콘텐츠 페이지에 바인딩된 위의 태그에서 볼 수 있듯이 `~/Site.master`합니다.

마스터 페이지에 두 개의 ContentPlaceHolder 컨트롤-있기 때문에 `head` 및 `MainContent` -Visual Web Developer 두 콘텐츠 컨트롤을 생성 합니다. 각 콘텐츠 컨트롤을 통해 특정 ContentPlaceHolder 참조 해당 `ContentPlaceHolderID` 속성입니다.

여기서 이전 사이트 전체 템플릿 기술을 통해 빛 마스터 페이지의 디자인 타임 지원과 함께 사용은입니다. 그림 9는 `About.aspx` Visual Web Developer의 디자인 뷰를 통해 볼 때 콘텐츠 페이지. 메모 마스터 페이지 콘텐츠 하는 동안 표시 되는 것이 회색 및 수정할 수 없습니다. 그러나 콘텐츠 컨트롤에 해당 하는 마스터 페이지의 contentplaceholders의는 편집할 수 있습니다. 와 마찬가지로 다른 ASP.NET 페이지와 원본 뷰와 디자인 뷰를 통해 웹 컨트롤을 추가 하 여 콘텐츠 페이지의 인터페이스를 만들 수 있습니다.


[![콘텐츠 페이지의 디자인 뷰에서 페이지별 및 마스터 페이지 콘텐츠를 표시합니다.](creating-a-site-wide-layout-using-master-pages-vb/_static/image24.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image23.png)

**그림 09**: The 콘텐츠 페이지의 디자인 뷰에서 표시 페이지 관련와 모두 마스터 페이지 콘텐츠 ([전체 크기 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-vb/_static/image25.png))


### <a name="adding-markup-and-web-controls-to-the-content-page"></a>콘텐츠 페이지에 태그 및 웹 컨트롤 추가

에 대 한 일부 콘텐츠를 만든 시간을 갖고자는 `About.aspx` 페이지. 대로 "the Author"에 대 한 제목 및 몇 가지 텍스트 단락을 입력 한 그림 10에 볼 수 있지만 너무 웹 컨트롤을 추가할 수 있습니다. 이 인터페이스를 만든 후 방문는 `About.aspx` 브라우저를 통해 페이지입니다.


[![브라우저를 통해 About.aspx 페이지 방문 하십시오.](creating-a-site-wide-layout-using-master-pages-vb/_static/image27.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image26.png)

**그림 10**: 방문는 `About.aspx` 정도 브라우저를 통해 페이지 ([전체 크기 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-vb/_static/image28.png))


요청 된 콘텐츠 페이지와 연결된 된 마스터 페이지가 fused 되 고 웹 서버에서 전체 렌더링을 이해 하는 것이 유용 합니다. 최종 사용자의 브라우저 결과, 퓨즈 HTML을 전송 됩니다. 이 확인 하려면 브라우저에서 보기 메뉴를 이동 하 고 소스를 선택 하 여 수신 HTML을 봅니다. 프레임이 없는 또는 하나의 창에 두 개의 다른 웹 페이지를 표시 하기 위한 기타 특수 기술 참고 합니다.

### <a name="binding-a-master-page-to-an-existing-aspnet-page"></a>마스터 페이지 기존 ASP.NET 페이지에 바인딩

이 단계에서 설명한 것 처럼 "마스터 페이지 선택" 확인란을 선택 하 고 마스터 페이지를 선택 하는 것 만큼 쉽게은 ASP.NET 웹 응용 프로그램에 새 콘텐츠 페이지를 추가 합니다. 안타깝게도, 마스터 페이지에는 기존 ASP.NET 페이지를 변환 쉽지 않습니다.

마스터 페이지를 기존 ASP.NET 페이지에 연결 하려면 다음 단계를 수행:

1. 추가 `MasterPageFile` 특성을 ASP.NET 페이지의 `@Page` 적절 한 마스터 페이지를 가리키는 지시문입니다.
2. 마스터 페이지의 contentplaceholders의 각각에 대해 콘텐츠 컨트롤을 추가 합니다.
3. 선택적으로 잘라낸 후 적절 한 콘텐츠 컨트롤에는 ASP.NET 페이지의 기존 콘텐츠를 붙여 넣습니다. ASP.NET 페이지 가능성이 있기 때문에 "선택적 으로" 여기 이미 표현 된 마스터 페이지에서와 같은 태그를 포함 하는 것이 말할는 `DOCTYPE`, `<html>` 요소와 Web Form입니다.

스크린 샷 함께이 프로세스에 대 한 단계별 지침에 대 한 체크 아웃 [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 [마스터 페이지를 사용 하 여 및 사이트 탐색](http://webproject.scottgu.com/VisualBasic/MasterPages/MasterPages.aspx) 자습서입니다. "업데이트 `Default.aspx` 및 `DataSample.aspx` 마스터 페이지를 사용 하려면" 섹션에서는 다음이 단계를 자세히 설명 합니다.

훨씬 쉽게 기존 ASP.NET 페이지 콘텐츠 페이지를 변환 하는 것 보다 새 콘텐츠 페이지를 만들 수 있기 때문에 만들 때마다 새 ASP.NET 웹 사이트는 사이트에 마스터 페이지를 추가 것을 권장 합니다. 이 마스터 페이지에 모든 새 ASP.NET 페이지를 바인딩하십시오. 초기 마스터 페이지는 매우 간단 하거나 일반; 경우 걱정 하지 마십시오 마스터 페이지를 나중에 업데이트할 수 있습니다.

> [!NOTE]
> 새 ASP.NET 응용 프로그램을 만들 때 Visual Web Developer 추가 `Default.aspx` 마스터 페이지에 연결 되지 않은 페이지입니다. 기존 ASP.NET 페이지 콘텐츠 페이지를 변환 하는 연습 하려면 계속 진행 하 고 해당 작업을 수행 `Default.aspx`합니다. 삭제할 수 있습니다 `Default.aspx` 하지만 "마스터 페이지 선택" 확인란을 선택이 시간 후 다시 추가 합니다.


## <a name="step-3-updating-the-master-pages-markup"></a>3 단계: 마스터 페이지의 태그를 업데이트합니다.

마스터 페이지의 주요 이점 중 하나는 사이트에서 다양 한 페이지에 대 한 전반적인 레이아웃을 정의 하 단일 마스터 페이지를 사용할 수 있습니다. 따라서 사이트의 모양과 느낌을 업데이트 하려면 단일 파일-마스터 페이지를 업데이트 해야 합니다.

이 문제를 보여 주기 위해 보겠습니다 가격 마스터 페이지 왼쪽된 열의 맨 위에 있는 현재 날짜를 포함 하도록 업데이트 합니다. 라는 레이블을 추가 `DateDisplay` 에 `leftContent` `<div>`합니다.

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample5.aspx)]

다음으로 만듭니다는 `Page_Load` 마스터에 대 한 이벤트 처리기 페이지 및 다음 코드를 추가 합니다.

[!code-vb[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample6.vb)]

위의 코드에서는 설정 레이블의 `Text` 속성을 현재 날짜 및 시간 형식는 요일, 월 및 두 일의 이름으로 지정 (11 그림 참조). 이러한 변경으로 인해 콘텐츠 페이지 중 하나를 다시 확인 합니다. 그림 11에서 볼 수 있듯이 결과 태그는 즉시 마스터 페이지에 변경 내용을 포함 하도록 업데이트 됩니다.


[![마스터 페이지에 변경 내용을 볼 때 반영 되는 콘텐츠 페이지](creating-a-site-wide-layout-using-master-pages-vb/_static/image30.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image29.png)

**그림 11**: 마스터 페이지의 변경 내용이 반영 때는 표시 되는 콘텐츠 페이지 ([전체 크기 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-vb/_static/image31.png))


> [!NOTE]
> 이 예제에서 알 수 있듯이, 마스터 페이지 서버 쪽 웹 컨트롤, 코드 및 이벤트 처리기를 포함할 수 있습니다.


## <a name="summary"></a>요약

마스터 페이지를 쉽게 업데이트할 수 있는 일관 된 사이트 전체 레이아웃 디자인 ASP.NET 개발자를 사용 합니다. Visual Web Developer는 다양 한 디자인 타임 지원을 제공 하는 대로 마스터 페이지와 연관 된 콘텐츠 페이지를 만들어 하는 것은 표준 ASP.NET 페이지를 만드는 것과 같이 간단 합니다.

이 자습서에서 만든 마스터 페이지 예제에는 두 개의 ContentPlaceHolder 컨트롤, head 및 MainContent 했습니다. 그러나만 지정한 기 MainContent ContentPlaceHolder 컨트롤에 대 한 태그 가격 콘텐츠 페이지에서 합니다. 다음 자습서에서는 여러 콘텐츠를 사용 하 여 살펴보겠습니다 콘텐츠 페이지의 컨트롤입니다. 또한 기본을 정의 하는 방법을 표시 태그 콘텐츠에 대 한 기본값을 사용 하 여 사이 전환 하려면 태그에에서 정의 된 마스터 페이지 및 콘텐츠 페이지에서 사용자 지정 태그를 제공 하는 방법에 마스터 페이지 내에서 제어 합니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [디자이너에 대 한 ASP.NET: 웹 표준을 사용 하 여 ASP.NET 웹 사이트를 구축에 무료 디자인 템플릿 및 지침](https://msdn.microsoft.com/asp.net/aa336602.aspx)
- [ASP.NET 마스터 페이지 개요](https://msdn.microsoft.com/library/wtxbf3hh.aspx)
- [연계 스타일 시트 (CSS) 자습서](http://www.w3schools.com/css/default.asp)
- [동적으로 페이지의 제목 설정](http://aspnet.4guysfromrolla.com/articles/051006-1.aspx)
- [Asp.net에서 마스터 페이지](http://www.odetocode.com/articles/419.aspx)
- [마스터 페이지의 빠른 시작 자습서](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/masterpages/default.aspx)

### <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 작성자 여러 ASP/ASP.NET 설명서와 4GuysFromRolla.com의 창립자의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 3.5 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. Scott에 도달할 수 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com) 또는에서 그의 블로그 통해 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)합니다.

> [!div class="step-by-step"]
> [이전](nested-master-pages-cs.md)
> [다음](multiple-contentplaceholders-and-default-content-vb.md)
